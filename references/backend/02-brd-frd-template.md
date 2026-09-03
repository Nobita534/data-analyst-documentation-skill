# Business & Functional Requirements Specification (BRD & FRD)

## 1. Thông tin Tổng quan (Document Information)
* **Tên tính năng / Module:** [Tên module, ví dụ: Inventory Management & Order Processing]
* **Phiên bản tài liệu:** [v1.0 / Draft / Approved]
* **Mức độ ưu tiên tổng thể:** [Critical / High / Medium]
* **Mục tiêu kỹ thuật:** [Mô tả ngắn gọn chức năng cần xây dựng hoặc nâng cấp trong backend]

---

## 2. Quy tắc Nghiệp vụ Bất biến (Business Rules - BR)
*Các ràng buộc logic cốt lõi mà mã nguồn backend bắt buộc phải tuân thủ, không phụ thuộc vào giao diện người dùng.*

| Rule ID | Tên quy tắc (Rule Name) | Phát biểu logic chi tiết (Logic Statement) | Hành vi khi vi phạm (Violation Behavior) |
| :--- | :--- | :--- | :--- |
| **BR-01** | [Ví dụ: Kiểm tra số lượng tồn khi checkout] | [Ví dụ: Số lượng đặt mua của từng item phải <= số lượng tồn khả dụng (available_stock = physical_stock - held_stock)] | Từ chối tạo đơn, trả về mã lỗi `422 Unprocessable Entity` kèm danh sách SKU hết hàng |
| **BR-02** | [Ví dụ: Thời hạn giữ hàng tạm thời (Stock Hold Timeout)] | [Ví dụ: Khi đơn hàng ở trạng thái `PAYMENT_PENDING`, hệ thống chỉ giữ hàng trong tối đa 15 phút] | Quá 15 phút không nhận được webhook thanh toán thành công, tự động nhả held_stock về available_stock |
| **BR-03** | [Ví dụ: Tính bất biến của giao dịch thanh toán (Idempotency)] | [Ví dụ: Mỗi mã giao dịch đối tác (transaction_id) chỉ được phép ghi nhận thành công đúng một lần] | Nếu request trùng transaction_id gửi đến, trả về status hiện tại mà không thực hiện cộng/trừ tiền hay đổi trạng thái lần hai |
| **BR-04** | [Ví dụ: Toàn vẹn phiếu nhập kho] | [Ví dụ: Phiếu nhập kho chỉ được phép commit vào tồn kho khi 100% SKU trong file nhập đã tồn tại trong catalog] | Hủy toàn bộ batch import, rollback transaction, xuất danh sách lỗi chi tiết theo từng dòng |

---

## 3. Đặc tả Yêu cầu Chức năng (Functional Requirements - FRD)

*(Lặp lại khối đặc tả dưới đây cho từng nhóm tính năng hoặc use case cụ thể)*

### FR-[Mã số]: [Tên chức năng, ví dụ: Quản lý Giữ tồn kho và Trừ kho Atomic]
* **Mã yêu cầu:** FR-[Mã số, ví dụ: FR-INV-01]
* **Mức độ ưu tiên:** [P0 (Bắt buộc) / P1 (Quan trọng) / P2 (Nâng cao)]
* **Actor thực hiện:** [Khách hàng vãng lai / Thành viên / Hệ thống tự động (System Cron) / Admin]
* **Mô tả chức năng:** [Mô tả luồng xử lý dữ liệu của backend khi nhận request]
* **Dữ liệu đầu vào (Input Parameters):**
  * `order_id` (UUID / BIGINT, Bắt buộc): Định danh đơn hàng cần xử lý.
  * `items` (Array, Bắt buộc): Danh sách sản phẩm gồm `sku_id` (INT) và `quantity` (INT, > 0).
* **Quy trình xử lý logic Backend (Processing Steps):**
  1. Mở một Database Transaction (`BEGIN TRANSACTION`).
  2. Khóa dòng dữ liệu tồn kho bằng cơ chế Pessimistic Lock (`SELECT ... FOR UPDATE`) hoặc kiểm tra Atomic Update (`stock = stock - quantity WHERE stock >= quantity`).
  3. Kiểm tra tính hợp lệ của số lượng tồn theo `BR-01`.
  4. Nếu đủ tồn kho: Giảm `available_stock`, tăng `held_stock`, ghi log vào bảng lịch sử giao dịch tồn kho (`inventory_transactions`). Commit Transaction.
  5. Nếu không đủ tồn kho: Rollback Transaction, ghi log thất bại.
* **Dữ liệu đầu ra & Trạng thái (Output & State Change):**
  * Thành công: Trả về trạng thái `200 OK` hoặc `201 Created` kèm `reservation_id` và `expires_at`.
  * Thất bại: Trả về lỗi định dạng chuẩn JSON (`code`, `message`, `error_details`).
* **Tiêu chí chấp thuận (Acceptance Criteria - Given/When/Then):**
  * *AC-01:* **Given** sản phẩm SKU-01 có available_stock = 1, **When** 2 request checkout cùng gửi tới đồng thời cho SKU-01, **Then** chỉ có đúng 1 request thành công, request còn lại nhận mã lỗi `OUT_OF_STOCK` (0% overselling).
  * *AC-02:* **Given** đơn hàng đang giữ kho, **When** hệ thống chạy cronjob quét các đơn quá 15 phút chưa thanh toán, **Then** trạng thái đơn chuyển sang `EXPIRED` và held_stock được hoàn trả chính xác.

---

## 4. Đặc tả Yêu cầu Phi chức năng (Non-Functional Requirements - NFR)

| Nhóm yêu cầu (Category) | Chỉ số đo lường (Target Metric) | Phương pháp kiểm chứng (Verification Method) |
| :--- | :--- | :--- |
| **Hiệu năng (Performance)** | Latency API tạo đơn và trừ kho < 200ms tại P95 dưới tải 200 concurrent users | Load Testing bằng k6 / JMeter trên môi trường Staging |
| **Tính sẵn sàng & Khả năng chịu lỗi (Resilience)** | Xử lý lỗi graceful degradation: Khi cổng thanh toán bên thứ ba mất kết nối, hệ thống không bị treo request và trả mã `503 Gateway Timeout` trong vòng 3 giây | Chaos Engineering / Mock API timeout |
| **Tính nhất quán dữ liệu (Data Consistency)** | Mức cô lập giao dịch tối thiểu Read Committed hoặc Serializable cho các bảng tiền tệ và tồn kho; 100% các cập nhật liên quan nhiều bảng phải bọc trong Transaction | Unit test kiểm tra Rollback khi có lỗi runtime |
| **Bảo mật (Security & Auditing)** | Xác thực API bằng Bearer Token (JWT/Sanctum); 100% dữ liệu webhook từ bên thứ ba phải được xác thực chữ ký số (HMAC Signature Verification); lưu audit log cho mọi thao tác nhập/điều chỉnh tồn kho | Security Code Review & Penetration Testing |

---

## 5. Ma trận Truy vết Yêu cầu (Traceability Matrix)
*Ánh xạ từ Mục tiêu cải tiến (File 01) sang Luật nghiệp vụ và Yêu cầu chức năng.*

| Mã Objective (File 01) | Mã Business Rule (BR) | Mã Functional Requirement (FR) | Mã Test Case (QA Reference) |
| :--- | :--- | :--- | :--- |
| **OBJ-01** (Chống overselling) | **BR-01** (Kiểm tra tồn kho) | **FR-INV-01** (Atomic Inventory Hold) | `TC_INV_CONCURRENCY_01` |
| **OBJ-02** (Xử lý thanh toán tin cậy) | **BR-03** (Idempotency Payment) | **FR-PAY-01** (Webhook Signature & Deduplication) | `TC_PAY_IDEMPOTENCY_01` |
| **OBJ-03** (Kiểm soát vòng đời đơn) | **BR-02** (Hết hạn giữ hàng) | **FR-ORD-01** (Order State Machine Transition) | `TC_ORD_STATE_MACHINE_01` |
| **OBJ-04** (Nhập kho an toàn) | **BR-04** (Toàn vẹn phiếu nhập) | **FR-INB-01** (Batch Goods Receipt Validation) | `TC_INB_BATCH_VALIDATE_01` |