# System Analysis & Improvement Proposal (AS-IS / TO-BE Specification)

## 1. Thông tin Tổng quan (System Overview)
* **Tên hệ thống / Dự án:** [Tên dự án hoặc module cần nâng cấp]
* **Bối cảnh nghiệp vụ:** [Mô tả ngắn gọn mô hình kinh doanh và mục đích vận hành của hệ thống]
* **Thành phần kiến trúc hiện tại:**
  * Backend / Services: [Ví dụ: Monolith Service, REST API Engine]
  * Frontend / Clients: [Ví dụ: Web Application, Mobile App, Admin Portal]
  * Cơ sở dữ liệu: [Ví dụ: RDBMS chính, Cache layer, File storage]
  * Dịch vụ bên thứ ba (Third-party): [Ví dụ: Payment Gateway, Shipping Partner, Notification Service]

---

## 2. Phân tích Hiện trạng (Current State - AS-IS)

### 2.1. Quy trình Nghiệp vụ Hiện tại (AS-IS Workflows)
*(Mô tả tuần tự các bước xử lý hiện tại của các luồng nghiệp vụ cốt lõi)*

* **[Mã WF, ví dụ: WF-01]: [Tên quy trình, ví dụ: Quy trình Bán hàng & Đặt hàng]**
  * *Luồng thực thi:* [Bước 1] $\rightarrow$ [Bước 2] $\rightarrow$ [Bước 3] $\rightarrow$ [Bước 4]
  * *Đặc điểm xử lý:* [Mô tả cách hệ thống lưu trữ, chuyển trạng thái hoặc tương tác external services]
* **[Mã WF, ví dụ: WF-02]: [Tên quy trình, ví dụ: Quy trình Nhập kho / Quản lý Tồn kho]**
  * *Luồng thực thi:* [Bước 1] $\rightarrow$ [Bước 2] $\rightarrow$ [Bước 3]
  * *Đặc điểm xử lý:* [Mô tả thao tác thủ công, cơ chế đồng bộ hoặc xử lý batch hiện tại]

### 2.2. Điểm nghẽn & Rủi ro Kỹ thuật (Problems & Root Causes)

| Problem ID | Hiện tượng kỹ thuật (Technical Symptom) | Nguyên nhân cốt lõi (Root Cause) | Tác động & Rủi ro nghiệp vụ (Business Impact) |
| :--- | :--- | :--- | :--- |
| **PRB-01** | [Ví dụ: Dữ liệu tồn kho bị sai lệch khi tải cao] | [Ví dụ: Thiếu cơ chế kiểm soát đồng thời (Concurrency Control)] | [Ví dụ: Bán vượt tồn kho (Overselling), hủy đơn hàng loạt] |
| **PRB-02** | [Ví dụ: Callback/Webhook xử lý nhiều lần] | [Ví dụ: Thiếu cơ chế Idempotency khi nhận tín hiệu gateway] | [Ví dụ: Sai lệch trạng thái thanh toán hoặc duplicate giao dịch] |
| **PRB-03** | [Ví dụ: Trạng thái đơn chuyển đổi tự do] | [Ví dụ: Quản lý trạng thái bằng CRUD trực tiếp, thiếu State Machine] | [Ví dụ: Đơn hàng nhảy vào trạng thái phi logic, gãy luồng vận hành] |
| **PRB-04** | [Ví dụ: Nhập liệu thủ công dễ phát sinh lỗi] | [Ví dụ: Thiếu schema validation và quy trình phê duyệt (approval)] | [Ví dụ: Sai lệch số liệu đối soát, mất thời gian khắc phục thủ công] |

---

## 3. Mục tiêu Cải tiến Định lượng (Improvement Objectives)

| Objective ID | Mục tiêu kỹ thuật & nghiệp vụ (Objective Statement) | Tiêu chí đo lường hoàn thành (Metric / Acceptance Target) |
| :--- | :--- | :--- |
| **OBJ-01** | [Ví dụ: Đảm bảo tính toàn vẹn tồn kho dưới tải đồng thời] | [Ví dụ: 0% lỗi Overselling trong điều kiện concurrent transactions] |
| **OBJ-02** | [Ví dụ: Tăng độ tin cậy khi tích hợp dịch vụ thanh toán] | [Ví dụ: 100% duplicate webhook được phát hiện và xử lý an toàn (Idempotent)] |
| **OBJ-03** | [Ví dụ: Kiểm soát chặt chẽ vòng đời thực thể nghiệp vụ] | [Ví dụ: 100% chuyển đổi trạng thái phải tuân thủ State Transition Table] |
| **OBJ-04** | [Ví dụ: Giảm thiểu sai sót và tự động hóa khâu nhập dữ liệu] | [Ví dụ: Chặn 100% dữ liệu sai schema trước khi ghi nhận vào DB] |

---

## 4. Mô hình Mục tiêu (Target State - TO-BE)

### 4.1. Năng lực Hệ thống Đề xuất (Target Capabilities)
* **[Tên năng lực 1, ví dụ: Controlled Inventory Management]:** [Mô tả giải pháp kiểm soát tính toàn vẹn và quy trình xác thực dữ liệu]
* **[Tên năng lực 2, ví dụ: Resilient External Integration]:** [Mô tả giải pháp xử lý webhook, retry mechanism và tính bất biến]
* **[Tên năng lực 3, ví dụ: Deterministic State Lifecycle]:** [Mô tả giải pháp kiểm soát vòng đời thực thể theo quy tắc chặt chẽ]

### 4.2. Đặc tả Luồng Quy trình Mục tiêu (TO-BE Workflows)

* **[Mã WF, ví dụ: TO-BE-WF-01]: [Tên quy trình, ví dụ: Quản lý Vòng đời Đơn hàng]**
  * *Bảng chuyển đổi trạng thái (State Transition Table):*
    | Trạng thái hiện tại | Sự kiện kích hoạt (Event) | Trạng thái tiếp theo | Điều kiện ràng buộc (Guard Condition) |
    | :--- | :--- | :--- | :--- |
    | `[STATE_A]` | [Hành động / Sự kiện] | `[STATE_B]` | [Điều kiện bắt buộc để chuyển trạng thái] |
    | `[STATE_B]` | [Hành động / Sự kiện] | `[STATE_C]` | [Điều kiện bắt buộc để chuyển trạng thái] |
    | `[STATE_B]` | [Sự kiện hủy / Timeout] | `[STATE_CANCELLED]` | [Điều kiện giải phóng tài nguyên / hoàn trả] |

* **[Mã WF, ví dụ: TO-BE-WF-02]: [Tên quy trình, ví dụ: Cơ chế Kiểm soát Đồng thời / Giữ hàng]**
  * *Nguyên tắc xử lý:* [Mô tả ngắn gọn cơ chế kiểm tra điều kiện, lock hoặc atomic operation]

* **[Mã WF, ví dụ: TO-BE-WF-03]: [Tên quy trình, ví dụ: Quy trình Nhập & Kiểm duyệt Dữ liệu theo Lô]**
  * *Luồng thực thi:* [Nguồn dữ liệu] $\rightarrow$ [Xác thực schema/nghiệp vụ] $\rightarrow$ [Phê duyệt] $\rightarrow$ [Cập nhật cơ sở dữ liệu]

---

## 5. Ma trận Phân tích Khoảng trống (Gap Analysis Matrix)
*Ánh xạ trực tiếp từ Hiện trạng (AS-IS) sang Giải pháp Mục tiêu (TO-BE).*

| Mã hạng mục | Hiện trạng (AS-IS) | Khoảng trống kỹ thuật (Gap / Root Cause) | Năng lực mục tiêu (TO-BE Solution) |
| :--- | :--- | :--- | :--- |
| **GAP-01** | [Mô tả cách làm hiện tại] | [Thiếu sót kỹ thuật / Điểm gãy cốt lõi] | [Cơ chế / Năng lực giải quyết ở hệ thống mới] |
| **GAP-02** | [Mô tả cách làm hiện tại] | [Thiếu sót kỹ thuật / Điểm gãy cốt lõi] | [Cơ chế / Năng lực giải quyết ở hệ thống mới] |
| **GAP-03** | [Mô tả cách làm hiện tại] | [Thiếu sót kỹ thuật / Điểm gãy cốt lõi] | [Cơ chế / Năng lực giải quyết ở hệ thống mới] |

---

## 6. Ranh giới Phạm vi Triển khai (Scope & Boundaries)

### 6.1. Thuộc phạm vi (In-Scope)
* [Liệt kê các module, nghiệp vụ hoặc thành phần kỹ thuật trực tiếp triển khai trong phiên bản này]
* [Liệt kê các luồng kiểm thử hoặc kịch bản tích hợp cốt lõi cần hoàn thành]

### 6.2. Ngoài phạm vi & Biện minh Kỹ thuật (Out-of-Scope & Justification)

| Hạng mục đề xuất hoãn / Loại trừ | Lý do loại trừ (Business & Technical Justification) |
| :--- | :--- |
| [Ví dụ: Microservices Architecture] | [Hệ thống hiện tại chưa đạt ngưỡng tải phức tạp; Monolith tối ưu chi phí vận hành] |
| [Ví dụ: Distributed Message Broker (Kafka)] | [Hàng đợi tích hợp sẵn đáp ứng đủ throughput; tránh phát sinh chi phí hạ tầng] |
| [Ví dụ: Mô hình AI / Recommendation Engine phức tạp] | [Chưa có đủ volume dữ liệu hành vi người dùng để huấn luyện hiệu quả] |