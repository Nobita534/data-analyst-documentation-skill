# Skill Business Analyst

Bộ skill hỗ trợ phân tích nghiệp vụ và chuyển đổi yêu cầu chưa rõ ràng thành các tài liệu đặc tả có cấu trúc, định lượng và sẵn sàng cho đội Data hoặc Engineering triển khai.

## Tổng quan

Skill này đóng vai trò cầu nối giữa:

- **Business Stakeholders**: mục tiêu, vấn đề và quy tắc nghiệp vụ.
- **Data Analysts**: câu hỏi phân tích, logic lọc, công thức metric và output schema.
- **Backend Developers**: đặc tả chức năng, use case, quy trình và API contract.

Skill tập trung vào việc **viết specification**, không trực tiếp truy vấn dữ liệu, chạy tính toán hoặc viết báo cáo phân tích hoàn chỉnh.

## Cấu trúc repo

```text
.
├── SKILL.md
├── README.md
└── references/
    ├── data-analyst/
    │   ├── 01-business-context-problem.md
    │   ├── 02-business-question-requirement.md
    │   └── 03-metric-dictionary.md
    └── backend/
        ├── 01-as-is-to-be.md
        ├── 02-brd-frd-template.md
        ├── 03-use-case-spec.md
        ├── 04-activity-bpmn.md
        └── 05-api-design-spec.md
```

## Nội dung chính

### Track Data Analyst

- Xác định bối cảnh và vấn đề kinh doanh.
- Chuẩn hóa business questions, slicing dimensions và filtering logic.
- Xây dựng metric dictionary với công thức, granularity, điều kiện loại trừ và SQL tham chiếu.

### Track Backend & Engineering

- Phân tích quy trình **AS-IS / TO-BE** và gap analysis.
- Viết BRD/FRD gồm business rules, functional specifications và non-functional requirements.
- Mô tả actors, preconditions, happy path, alternate flows và exception flows trong use case.
- Mô hình hóa quy trình bằng Mermaid.
- Đặc tả API gồm HTTP method, URL, payload, query parameters và status codes.

## Cách sử dụng

1. Đọc [SKILL.md](SKILL.md) để nắm vai trò, operating modes và các ràng buộc bắt buộc.
2. Chọn template phù hợp trong thư mục `references/`.
3. Cung cấp đủ bối cảnh: mục tiêu, đối tượng sử dụng, dữ liệu hoặc hệ thống liên quan và phạm vi cần đặc tả.
4. Tạo tài liệu theo đúng section headers và thứ tự của template tương ứng.
5. Kiểm tra output theo Definition of Done trước khi bàn giao cho Data hoặc Engineering.

## Nguyên tắc đầu ra

- Dùng thông tin cụ thể, kiểu dữ liệu, công thức và boundary values thay cho mô tả định tính.
- Giữ đúng section headers của template, không tự ý thêm section ngoài phạm vi.
- Chỉ tạo đúng số lượng item mà yêu cầu nêu ra.
- Nêu rõ xử lý lỗi, giá trị null, gián đoạn mạng và trạng thái không hợp lệ.
- Đảm bảo Mermaid hợp lệ và các công thức metric có numerator, denominator, exclusions và SQL tham chiếu khi cần.
- Khi yêu cầu có rủi ro logic hoặc không khả thi về dữ liệu, phải chỉ ra trade-off và đề xuất phương án phù hợp.

## Trạng thái

Repo hiện cung cấp các template và hướng dẫn nền tảng cho việc đặc tả nghiệp vụ, dữ liệu, backend và API.
