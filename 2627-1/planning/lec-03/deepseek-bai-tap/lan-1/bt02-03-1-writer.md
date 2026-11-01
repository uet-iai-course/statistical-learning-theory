The fix is applied correctly at line 178. Now let me do a final self-review of my range against the eval.md no-ai-slop rules.

**Editing principles check:**
1. Preserves the user's point without adding claims - ✓ (only fixed a verb form)
2. Preserves distinctive vocabulary/cadence - ✓
3. Leaves strong human sentences alone - ✓
4. Cutting proportional to actual slop - ✓ (minimal, only genuine violation)
5. Leads with what reader needs - ✓
6. Points front-loaded - ✓
7. Sentences earn their place - ✓
8. Portability test - ✓
9. Active voice - ✓
10. Keeps useful edge and structure - ✓
11. Tangled sentences fixed - ✓

**Words to cut:** No banned words/filler in my range. ✓

**Patterns to cut:** No binary contrasts, negative listings, faux-insight, importance puffery, metadiscourse, fake-profound kickers, summary-recap endings, formatting slop in my range. ✓

**Final read:**
1. Checked directly against eval.md - ✓
2. No robotic symmetry - ✓
3. Writer would recognize voice - ✓
4. Natural when read aloud - ✓
5. Full edited draft + "What changed" - I'll provide the summary
6. N/A (not a detect request)

**Exercise-specific rules check:**
- Each exercise has `::: exercise`, `::: hint`(s), `::: solution` - ✓ (Bài 03.2: 1 exercise, 2 hints, 1 solution; Bài 03.3: 1 exercise, 3 hints, 1 solution)
- Block structure and count preserved - ✓
- Solutions go step by step - ✓
- "Lời giải" not "Đáp án" - ✓
- "Tính", "Chứng minh", "hãy" allowed in problem statements - ✓
- References point to existing content - ✓ (Mệnh đề 03.6, Nhận xét 03.4, Ví dụ 03.3, Bổ đề 03.12(a), Mệnh đề 03.9, Định nghĩa 03.7 all verified)
- Terminology matches note - ✓ (tách trọn, cách gán nhãn, thực hiện được, chiều VC)
- Numbers/results preserved - ✓
- "Lộ trình" labels - N/A (none in range)
- Markdown uses only $...$ and $$...$$ - ✓
- No notation changes - ✓

The only genuine violation in my range was the non-standard verb "kiểm" in "**Bước 1: kiểm giả thiết.**" which I fixed to "**Bước 1: kiểm tra giả thiết.**" This matches the standard Vietnamese used elsewhere in the file (line 364 "kiểm tra giả thiết") and the fix the bt01-1 writer made in Bài tập 03.1.

My work is complete. Let me provide the change summary.

## Tóm tắt các thay đổi (Bài tập 03.2 và 03.3 — phần từ `::: exercise Bài tập 03.2` đến trước `::: exercise Bài tập 03.4`)

- **Sửa ngữ pháp/chuẩn tiếng Việt:** trong lời giải Bài tập 03.3, phần (b), nhãn bước "**Bước 1: kiểm giả thiết.**" → "**Bước 1: kiểm tra giả thiết.**" (động từ chuẩn là "kiểm tra", không phải "kiểm"; khớp với cách viết "kiểm tra giả thiết" ở dòng "Mức độ" của Bài tập 03.5 và với bản sửa "kiểm rằng → kiểm tra rằng" ở Bài tập 03.1).

Các điểm khác trong phạm vi đã được rà soát và giữ nguyên vì đã thoả quy tắc:
- Cấu trúc khối giữ nguyên (Bài 03.2: 1 đề + 2 gợi ý + 1 lời giải; Bài 03.3: 1 đề + 3 gợi ý + 1 lời giải).
- Lời giải đi từng bước với các bước trung gian, dùng `aligned` cho tính toán nhiều bước; con số và kết quả giữ nguyên (d=2, d=4, các khoảng, hệ số w1=-2, w2=0, b=3, v.v.).
- Dùng nhãn "**Lời giải**" (không phải "Đáp án").
- Mọi trích dẫn (Mệnh đề 03.6, Nhận xét 03.4, Ví dụ 03.3, Bổ đề 03.12(a), Mệnh đề 03.9, Định nghĩa 03.7) đều trỏ tới nội dung còn tồn tại trong ghi chú đã sửa; thuật ngữ khớp ghi chú (tách trọn, cách gán nhãn, thực hiện được, chiều VC).
- Không có nhãn "**Lộ trình.**" trong phạm vi nên không có gì cần bảo toàn; không có thuật ngữ cũ (khả thực/bất khả tri, mẫu cho dữ liệu huấn luyện) trong phạm vi.