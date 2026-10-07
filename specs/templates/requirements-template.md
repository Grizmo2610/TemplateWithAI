# Requirements Document: <Feature Name>

## Introduction
[Tóm tắt 2-3 câu về tính năng này: làm gì, dành cho ai, giá trị mang lại. Ví dụ: Thêm bảng FCT_RETAIL_LOAN để phục vụ báo cáo nợ xấu.]

## Requirements

### Requirement 1: [Tên ngắn gọn, vd: Ingest Metadata]

**User Story:** As a Data Engineer, I want the system to ingest the raw DDL, so that a valid Knowledge Base file is created.

### Acceptance Criteria
1. WHEN the user provides a valid DDL file,
   THE SYSTEM SHALL parse the table name, columns, and primary keys correctly.
2. WHEN the parsing is complete,
   THE SYSTEM SHALL generate a markdown file in `knowledge/tables/` following the standard schema.
3. IF the DDL file is malformed or unsupported,
   THEN THE SYSTEM SHALL reject the operation with a specific syntax error message.

### Requirement 2: [Tên ngắn gọn, vd: Generate Data Engine]

**User Story:** As a Data Engineer, I want the system to create a vectorized data engine, so that millions of rows can be generated efficiently.

### Acceptance Criteria
1. WHEN the Knowledge Base is approved,
   THE SYSTEM SHALL generate a Python class inheriting from `BaseFactAssembler` or `BaseDimEvolver`.
2. THE SYSTEM SHALL use Polars expressions (Vectorized) for all data transformations without any `for` loops.
3. WHERE foreign keys exist,
   THE SYSTEM SHALL use `.sample()` from pre-loaded ActivePools instead of SQL JOINs.
4. IF a referenced ActivePool is missing during execution,
   THEN THE SYSTEM SHALL raise a `KeyError` and halt execution safely.