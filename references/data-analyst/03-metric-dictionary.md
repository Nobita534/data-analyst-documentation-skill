# Metric Dictionary & Business Logic Specification (Từ điển Chỉ số & Logic Đo lường)

## 1. Bảng Tổng mục Chỉ số (Metric Master Index)

| Mã Metric | Tên chỉ số (Metric Name) | Tên hiển thị (Display Name) | Phân loại | Cấp độ ưu tiên | Chủ sở hữu nghiệp vụ (Owner) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **MET-01** | `customer_retention_rate_d30` | Tỷ lệ giữ chân Day-30 | Core / KPI | P0 | Product Team |
| **MET-02** | `gross_merchandise_value` | Tổng giá trị giao dịch (GMV) | Financial | P0 | Business Ops |
| **MET-03** | `average_order_value` | Giá trị trung bình đơn (AOV) | Efficiency | P1 | Growth Team |

---

## 2. Đặc tả Chi tiết từng Chỉ số (Detailed Metric Specifications)

*(Lặp lại khối cấu trúc chuẩn này cho từng Metric trong dự án)*

### [Mã Metric]: [Tên kỹ thuật - Snake_case]
* **Tên hiển thị trên Dashboard:** [Tên tiếng Việt hoặc tiếng Anh dùng cho người xem báo cáo]
* **Phân loại chỉ số:** [North Star Metric / Core KPI / Supporting Metric / Guardrail Metric]
* **Định nghĩa nghiệp vụ (Business Definition):** [Diễn giải bằng lời bình dân: Chỉ số này phản ánh điều gì trong thực tế kinh doanh?]

#### A. Công thức & Logic tính toán (Mathematical Formulation)
* **Công thức toán học:**
  $$\text{Metric} = \frac{\text{Tử số (Numerator)}}{\text{Mẫu số (Denominator)}} \times 100$$
* **Diễn giải thành phần:**
  * **Tử số:** [Cách đếm hoặc tổng hợp, ví dụ: `COUNT(DISTINCT user_id)` có hành động X]
  * **Mẫu số:** [Cơ số so sánh, ví dụ: `COUNT(DISTINCT user_id)` trong tập ban đầu]
* **Đơn vị đo lường (Unit):** [Phần trăm (%), Tiền tệ (VND/USD), Số đếm nguyên (Integer), Thời gian (Giây/Ngày)]
* **Định dạng hiển thị (Display Format):** [Ví dụ: `0.00%`, `#,##0 VND`, `0.0`]

#### B. Phạm vi tính toán & Ràng buộc lọc (Granularity & Filtering)
* **Mức độ chi tiết của dòng dữ liệu (Granularity):** [Ví dụ: Tính trên cấp độ 1 User theo từng Cohort ngày/tháng]
* **Điều kiện bao gồm (Inclusion Rules):** [Ví dụ: `status IN ('COMPLETED', 'DELIVERED')`]
* **Điều kiện loại trừ (Exclusion Rules):** 
  * Loại trừ giao dịch thử nghiệm (`is_test = true`).
  * Loại trừ đơn hàng có giá trị voucher vượt 100% giá trị sản phẩm.
* **Xử lý giá trị biên & Dữ liệu thiếu (Edge Cases & Null Handling):**
  * Trường hợp mẫu số bằng 0 (`Denominator = 0`): Trả về `0` hoặc `NULL` (tránh lỗi Division by Zero).
  * Xử lý trường hợp hoàn tiền/hủy sau chu kỳ báo cáo: [Ghi rõ lùi về ngày phát sinh hay trừ vào ngày hủy].

#### C. Chiều phân tích khả dụng (Supported Slice Dimensions)
* Danh sách các chiều có thể dùng để lọc/cắt lát chỉ số này:
  * Theo thời gian: [Ngày, Tuần, Tháng, Quý, Năm].
  * Theo thực thể: [Chi nhánh, Kênh tiếp thị, Nhóm khách hàng, Vùng miền, Danh mục sản phẩm].

#### D. Mã truy vấn tham chiếu mẫu (Reference SQL Implementation)
```sql
-- Logic truy vấn chuẩn để các thành viên hoặc các công cụ BI tái sử dụng
SELECT 
    dimension_col,
    COUNT(DISTINCT CASE WHEN condition_met THEN user_id END) * 1.0 
    / NULLIF(COUNT(DISTINCT user_id), 0) AS metric_value
FROM source_table
WHERE is_valid = TRUE
GROUP BY dimension_col;