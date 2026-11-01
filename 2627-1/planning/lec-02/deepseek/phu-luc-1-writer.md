Both edits are confirmed. Let me now run through the no-ai-slop eval checks for the Phụ lục section.

**Editing principles:**
1. Preserve the point without adding claims — ✓ (only terminology change and cutting a navigation pointer)
2. Preserve vocabulary/cadence — ✓
3. Leave strong human sentences alone — ✓ (only minimal edits)
4. Cutting proportional to slop — ✓ (only cut one navigation pointer)
5-11. ✓

**Words to cut:** No banned words introduced. ✓

**Patterns to cut:**
- Navigation pointer "như ở Phụ lục A(iv) của Bài 01" cut — ✓
- No binary contrasts, rhetorical setups, etc. introduced. ✓

**Final read:**
- Checked against eval.md directly — ✓
- No robotic symmetry — ✓
- Author's voice preserved — ✓
- Natural — ✓
- Full edited draft + What changed — I'll provide the summary.

Let me verify the terminology change is complete. The plan's terminology list: "khả thực" → "khả diễn". I changed the table header. Let me confirm there are no other "khả thực" occurrences in the Phụ lục section (lines 1066-1141). From my reading, line 1130 was the only one.

Let me also double-check there are no other navigation pointers or issues in the Phụ lục that I might have missed. Let me review the section once more:

- Line 1070: "Bước 4 của chứng minh Bổ đề 02.6 cần bất đẳng thức một biến dưới đây." — This identifies which lemma's proof step needs the inequality. It's context for the appendix's purpose, not navigation. Keep.
- Line 1106: "Thay $u=\tau(b-a)$ vào Bước 3 của chứng minh Bổ đề 02.6" — legitimate cross-reference within the proof. Keep.
- Line 1111, 1119, 1128: references to Ví dụ 02.2, 02.3, 02.7, 02.12 — these identify which examples the appendix supports. Keep.
- Line 1138: "Phụ lục A(v) của Bài 01" — kept per plan (needed to identify the measurability condition).
- Line 1141: "Định nghĩa 01.4" — kept (identifies the definition). "như ở Phụ lục A(iv) của Bài 01" — cut (navigation pointer).

All checks pass. The edits are complete and minimal.

## Tóm tắt các thay đổi (Phụ lục, dòng 1066–1141)

1. **Bảng B.3 (dòng 1130):** đổi thuật ngữ "khả thực" → "khả diễn" theo §5 của `van-phong-tac-gia.md`.
2. **Mục C (dòng 1141):** cắt cụm điều hướng "như ở Phụ lục A(iv) của Bài 01" — lập luận đã được trình bày đầy đủ trong câu, người đọc không cần mở nơi được dẫn; giữ nguyên "Định nghĩa 01.4" (dẫn chiếu cần để định danh điều kiện đo được).

**Giữ nguyên:** dòng 1138 "Phụ lục A(v) của Bài 01" (dẫn chiếu cần để định danh điều kiện đo được, theo kế hoạch); mọi khối đánh số, con số, kết quả và nhãn trong Phụ lục A, B, C; các dẫn chiếu Ví dụ 02.2/02.3/02.7/02.12 và Bổ đề 02.6 (định danh nội dung được hỗ trợ). Không thêm khẳng định, số liệu hay nguồn mới; không đổi kí hiệu toán; Markdown chỉ dùng `$...$`/`$$...$$`.