# Specs — Tài liệu Đặc tả Tính năng

Thư mục này chứa các bộ 3 file Đặc tả (Requirements + Design + Tasks) theo quy trình **Spec-Driven Development** (Kiến trúc Kiro).

> **Quy tắc bắt buộc (HC-1 trong `AGENTS.md`):** Mọi tính năng mới hoặc sửa lỗi phức tạp đều PHẢI có Spec được duyệt trước khi viết code. Không "Vibe Coding".

---

## Cách tạo Spec mới

Dùng slash command trong Gemini CLI:

```
/spec-new <feature_name> <type>
```

Ví dụ:
```
/spec-new fct-retail-overdraft fact
/spec-new dim-retail-product dim
/spec-new fix-scd2-gap bugfix
```

Lệnh này tạo 3 file trong `specs/{feature_name}/`:
- `requirements.md` — Yêu cầu theo chuẩn EARS (Entity-Action-Result-Scenario)
- `design.md` — Thiết kế kỹ thuật chi tiết
- `tasks.md` — Danh sách task triển khai có thể check off

Chỉ chạy `/spec-implement` khi cả 3 file đã được **user approve**.

---

## Specs hiện có

| Spec | Loại | Trạng thái |
|:---|:---|:---|
| `fct-retail-casa/` | Snapshot FACT | ✅ Hoàn thành |
| `fct-retail-funds-transfer/` | Transaction FACT | ✅ Hoàn thành |
| `fct-retail-card-doc/` | Transaction FACT | ✅ Hoàn thành |
| `fct-retail-loan/` | Snapshot FACT | ✅ Hoàn thành |

---

## Templates

Thư mục `templates/` chứa mẫu cho từng loại spec:

| Template | Dùng cho |
|:---|:---|
| `requirements-template.md` | Yêu cầu theo chuẩn EARS |
| `design-template.md` | Thiết kế Engine + SQL patterns |
| `tasks-template.md` | Task checklist triển khai |
| `bugfix-template.md` | Root cause + fix plan cho bug |

---

## Cấu trúc 1 Spec hoàn chỉnh

```
specs/{feature_name}/
├── requirements.md    ← EARS requirements, acceptance criteria
├── design.md          ← Engine class, SQL patterns, data flow
└── tasks.md           ← Ordered task list, check off khi làm xong
```

Xem ví dụ tại `specs/fct-retail-casa/` cho Snapshot FACT hoặc `specs/fct-retail-funds-transfer/` cho Transaction FACT.
