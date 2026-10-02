# TEAM — Day04, K4-L3B

**Làm nhóm.** Mỗi người tự viết và commit phần INDIVIDUAL của mình.

## Thông tin bài nộp

- Tên nhóm: Northstar Helpdesk
- Người đại diện / MSSV: Nguyen Huy Cuong / 2A202602842
- Tên repo: `K4-L3B-Day04-NguyenHuyCuong-2A202602842--Prompt-Engineering-Tool-Calling-Labs`
- URL repo, nhánh nộp, commit chốt: GitHub `main`, commit sau khi push
- Deadline áp dụng và link thông báo đổi hạn nếu có:

## Thành viên

| Họ và tên | MSSV | GitHub | Vai trò và công việc | File/commit/PR |
|---|---|---|---|---|
| Nguyen Huy Cuong | 2A202602842 | cuongnh04 | Prompt, tool contract, eval cases, report integration | `starter_v0/artifacts`, `starter_v0/data/eval_group.json` |

## Nhận xét chung

- Kết quả và bằng chứng: 10 original group cases, improved safety prompt, fixed tool declarations, and static validation. Live provider evidence is blocked by the configured Gemini key returning `400 API_KEY_INVALID`.
- Thay đổi hiệu quả nhất: Explicit routing, latest-turn correction, and fresh confirmation for every ticket payload.
- Giới hạn còn lại: v0-v3 live runs, UI transcript, and adversarial run require a valid provider key.
- Cách phân công và tích hợp: Individual submission; all artifacts are integrated under `starter_v0/`.

## INDIVIDUAL

Sao chép mục này cho từng thành viên.

### Nguyen Huy Cuong — 2A202602842

- Phần việc và file/commit/PR: `starter_v0/artifacts/system_prompt.md`, `starter_v0/artifacts/tools.yaml`, `starter_v0/data/eval_group.json`, `starter_v0/artifacts/REPORT.md`.
- Quyết định, khó khăn và cách xử lý: Kept IT Helpdesk scope and used explicit safety boundaries; live Gemini validation was stopped at the provider authentication error.
- Điều đã học: Tool routing and argument correctness are separate from answer quality; write actions need a fresh confirmation boundary.
- AI/công cụ đã dùng và cách kiểm tra: VS Code/Copilot-assisted edits reviewed against registry, schemas, fixed datasets, and local validation scripts.
- Thời điểm đã tự nộp URL repo chung trên VLearn: Chưa nộp.
