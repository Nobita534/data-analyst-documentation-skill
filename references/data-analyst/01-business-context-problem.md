# Tài liệu Bối cảnh & Định nghĩa Vấn đề Kinh doanh (Business Context & Problem Statement)

## 1. Thông tin tổng quan (Metadata)
* **Tên bài toán / Dự án:** [Điền tên ngắn gọn, rõ ràng]
* **Người yêu cầu (Stakeholder / Sponsor):** [Phòng ban / Vị trí cụ thể, ví dụ: Head of Marketing, Product Owner]
* **Người thực hiện phân tích (Owner):** [Tên Data Analyst / Analytics Engineer]
* **Ngày khởi tạo & Trạng thái:** [YYYY-MM-DD] | [Draft / Under Review / Approved]

---

## 2. Bối cảnh kinh doanh (Business Context & Background)
* **Tổng quan thị trường & sản phẩm:** [Mô tả ngắn gọn sản phẩm, mô hình kinh doanh, luồng vận hành chính đang diễn ra].
* **Động lực thúc đẩy phân tích:** [Sự kiện gì kích hoạt yêu cầu này? Ví dụ: sau chiến dịch quảng cáo tháng trước, sau khi thay đổi giao diện, xuất hiện đối thủ cạnh tranh mới].

---

## 3. Vấn đề cốt lõi (Problem Statement)
*Áp dụng công thức 3 vế: [Thực trạng hiện tại] nhưng [Nỗi đau / Sự cố phát sinh], dẫn đến [Hậu quả / Khoảng cách so với kỳ vọng].*

* **Mô tả chi tiết vấn đề:** 
  * *Ví dụ:* Số lượng người đăng ký mới trong Quý 1/2026 tăng 25%, nhưng tỷ lệ giữ chân sau 30 ngày (Day-30 Retention) giảm mạnh từ 40% xuống còn 18%, khiến chi phí thu hút khách hàng (CAC) bị lãng phí.
* **Mức độ ảnh hưởng kinh doanh (Business Impact):**
  * **Tài chính / Doanh thu:** [Ước tính thiệt hại trực tiếp hoặc chi phí cơ hội, ví dụ: Lãng phí 200M ngân sách ads/tháng].
  * **Vận hành / Người dùng:** [Tỷ lệ rời bỏ, thời gian gián đoạn hoặc trải nghiệm khách hàng bị giảm sút].

---

## 4. Mục tiêu & Tiêu chí thành công (Objectives & Success Criteria)
* **Mục tiêu của bài phân tích (Analysis Objectives):**
  * Làm rõ nguyên nhân chính khiến khách hàng dừng sử dụng sản phẩm sau chu kỳ đầu tiên.
  * Phân nhóm (segmentation) nhóm khách hàng rời bỏ nhiều nhất theo kênh và hành vi.
* **Tiêu chí thành công (Definition of Success):**
  * Đưa ra được ít nhất 3 đề xuất can thiệp cụ thể dựa trên số liệu cho team Product/Growth trước ngày [YYYY-MM-DD].
  * Xác định được nhóm đặc tính (features) có mức tương quan giữ chân cao nhất.

---

## 5. Ranh giới & Phạm vi (Scope & Boundaries)
* **Trong phạm vi phân tích (In-Scope):**
  * Dữ liệu hành vi người dùng trên nền tảng Mobile App (iOS & Android).
  * Khoảng thời gian: Từ ngày [YYYY-MM-DD] đến [YYYY-MM-DD].
  * Đối tượng: Toàn bộ user đăng ký mới phát sinh trong khoảng thời gian trên.
* **Ngoài phạm vi phân tích (Out-of-Scope):**
  * Hành vi người dùng trên nền tảng Website.
  * Chi tiết dữ liệu tài chính kế toán / dòng tiền thực thu (sẽ xử lý ở giai đoạn sau).

---

## 6. Tiền đề & Giả định ban đầu (Assumptions & Constraints)
* **Giả định (Assumptions):**
  * Hệ thống logging sự kiện (Tracking events) hoạt động ổn định và không bị gián đoạn dữ liệu trong khung thời gian khảo sát.
  * Một tài khoản (User ID) tương ứng với một người dùng duy nhất (không xét tài khoản dùng chung).
* **Ràng buộc (Constraints):**
  * Thời gian hoàn thành bản phân tích: Tối đa 5 ngày làm việc.
  * Chỉ sử dụng dữ liệu nội bộ trên Data Warehouse hiện tại, chưa tích hợp nguồn bên thứ ba.