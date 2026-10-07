# Implementation Tasks: <Feature Name>

## Metadata
- **Spec Directory:** `specs/<feature-name>/`
- **Requirements Approved On:** [YYYY-MM-DD]
- **Design Approved On:** [YYYY-MM-DD]

## Pre-conditions
- [ ] `requirements.md` đã được review và chốt (Approved).
- [ ] `design.md` đã được review và chốt (Approved).

## Tasks

### Task 1: [Tiêu đề task - Ví dụ: Khởi tạo file Knowledge Base]
- [ ] **Status**: pending | in-progress | completed
- **Output**: [File sẽ tạo ra/sửa đổi. Vd: `knowledge/tables/datamart/retail_dtm/fct_retail_loan.md`]
- **Linked Requirements**: REQ-1.1, REQ-1.2
- **Dependencies**: none
- **Verification**: Mở file lên và xác nhận nội dung đúng chuẩn Markdown, không có lỗi cú pháp.

### Task 2: [Tiêu đề task - Ví dụ: Viết Data Engine]
- [ ] **Status**: pending | in-progress | completed
- **Output**: `src/forge/models/datamart/retail_dtm/fct_retail_loan.py`
- **Linked Requirements**: REQ-2.1, REQ-2.2
- **Dependencies**: Task 1
- **Verification**: Chạy test script độc lập hoặc compile thành công không lỗi syntax.

### Task 3: [Tiêu đề task - Ví dụ: Viết Unit Test cho Engine]
- [ ] **Status**: pending | in-progress | completed
- **Output**: `tests/unit/models/datamart/retail_dtm/test_fct_retail_loan.py`
- **Linked Requirements**: REQ-2.1, REQ-2.2
- **Dependencies**: Task 2
- **Verification**: Viết test script truyền mock data vào hàm `_generate_measures` và `assert` thành công (Không có lỗi TypeError hay ColumnNotFound).

### Task 4: [Tiêu đề task - Ví dụ: Tích hợp vào Daily Pipeline]
- [ ] **Status**: pending | in-progress | completed
- **Output**: `src/forge/pipelines/daily_pipeline.py`
- **Linked Requirements**: REQ-2.3
- **Dependencies**: Task 3
- **Verification**: Lệnh `python -m src.forge.cli run` chạy thành công không quăng Exception.

### Task 5: Integration and Audit
- [ ] **Status**: pending | in-progress | completed
- **Output**: Oracle Database Data
- **Linked Requirements**: ALL
- **Dependencies**: Task 1, 2, 3, 4
- **Verification**: Lệnh `python -m src.forge.cli audit` pass 100% (No orphaned foreign keys).

## Post-conditions
- [ ] Tất cả Tasks đã được đánh dấu `completed`.
- [ ] Toàn bộ hệ thống chạy ổn định (Audit Pass).
- [ ] Các file Spec (`req`, `design`, `tasks`) đã được lưu trữ hoàn chỉnh.