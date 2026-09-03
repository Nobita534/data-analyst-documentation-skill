# Business Questions & Analytical Requirements (Câu hỏi Phân tích & Yêu cầu Dữ liệu)

## 1. Bản đồ Chuyển dịch Bài toán sang Câu hỏi (Problem-to-Question Mapping)
*Ánh xạ trực tiếp từ mục tiêu ở file `01-business-context-problem.md` sang các câu hỏi định lượng.*

| Mã BQ | Câu hỏi Kinh doanh Cốt lõi (Business Question) | Loại phân tích | Quyết định/Hành động liên đới (Actionable Decision) | Mức độ ưu tiên |
| :--- | :--- | :--- | :--- | :--- |
| **BQ-01** | [Ví dụ: Tỷ lệ hoàn đơn tập trung cao nhất ở nhóm ngành hàng nào?] | Descriptive | Tạm dừng hoặc tối ưu quy trình kiểm duyệt ngành hàng đó | P0 (Bắt buộc) |
| **BQ-02** | [Ví dụ: Có sự tương quan giữa thời gian giao hàng và tỷ lệ hủy đơn không?] | Diagnostic | Thiết lập lại cam kết SLA vận chuyển cho từng tuyến đường | P1 (Quan trọng) |
| **BQ-03** | [Ví dụ: Điểm nghẽn lớn nhất khiến user bỏ giỏ hàng nằm ở bước nào?] | Diagnostic | Đơn giản hóa luồng thanh toán (Checkout flow) | P0 (Bắt buộc) |

---

## 2. Đặc tả Chi tiết từng Câu hỏi Phân tích (Detailed Analytical Specs)

*(Lặp lại khối đặc tả này cho từng BQ đã liệt kê ở Bảng trên)*

### [Mã BQ]: [Tên câu hỏi kinh doanh]
* **Mục tiêu phân tích:** [Cần rút ra kết luận gì sau khi chạy câu hỏi này?]
* **Giả thuyết nghiệp vụ (Business Hypothesis):** [Kỳ vọng/dự đoán ban đầu trước khi xem số liệu là gì?]
* **Chỉ số đo lường chính (Primary Metrics):** [Tên các chỉ số, ví dụ: Return Rate, Total Loss Amount]
* **Chiều phân tích / Cắt lát (Dimensions):**
  * Theo thời gian: [Theo ngày, theo tuần, theo tháng, theo giờ trong ngày]
  * Theo đối tượng/phân khúc: [Ngành hàng, Khu vực địa lý, Nhóm khách hàng (New vs Existing)]
* **Điều kiện lọc & Loại trừ (Filters & Exclusions):**
  * Điều kiện lấy: [Trạng thái đơn hàng = 'Completed' HOẶC 'Returned']
  * Loại trừ: [Loại trừ tài khoản test, đơn hàng có giá trị = 0]
* **Cấu trúc bảng đầu ra mong đợi (Expected Output Schema):**
  | Tên cột (Column Name) | Kiểu dữ liệu (Data Type) | Diễn giải ý nghĩa |
  | :--- | :--- | :--- |
  | `category_name` | VARCHAR | Tên danh mục sản phẩm |
  | `total_orders` | INT | Tổng số đơn hàng phát sinh |
  | `returned_orders` | INT | Số lượng đơn bị hoàn trả |
  | `return_rate` | DECIMAL(5,2) | Tỷ lệ hoàn đơn (%) |
* **Kế hoạch trực quan hóa (Visualization Plan):**
  * Loại biểu đồ đề xuất: [Biểu đồ cột chồng, Bar chart phân cấp, Heatmap...]
  * Thông điệp chính cần thể hiện trên biểu đồ: [Điểm nổi bật cần đập vào mắt người xem ngay lập tức]

---

## 3. Ma trận Khả thi Dữ liệu (Data Readiness & Availability Matrix)
*Kiểm tra xem dataset hiện có đủ trường để trả lời toàn bộ các BQ hay không.*

| Mã BQ | Các trường dữ liệu cần có (Required Fields) | Nguồn/Bảng dữ liệu thực tế (Source Table) | Tình trạng dữ liệu (Data Status) | Giải pháp thay thế (Fallback Plan) |
| :--- | :--- | :--- | :--- | :--- |
| **BQ-01** | `category_id`, `status`, `created_at` | `orders`, `products` | Đầy đủ | Không cần |
| **BQ-02** | `shipping_time`, `cancellation_reason` | `deliveries` | Thiếu lý do hủy (null 40%) | Dùng `cancellation_time` làm proxy |