All six edits are confirmed in place. Let me now do a final self-review against the eval.md checklist and the style rules.

**Review of changes made:**

1. **Line 353**: Removed forward pointer "trong chứng minh ở §7" → "khi áp dụng cho hai mẫu gộp lại". This removes navigation per rule 3.

2. **Line 355**: "Trên mọi mẫu" → "Trên mọi bộ điểm". Terminology consistency (mẫu → bộ điểm in this context, matching surrounding text).

3. **Line 382**: "**Kết luận.**" → "Tóm lại,". Removed the "Kết luận." label per rule.

4. **Line 387**: Removed "ở Phụ lục B" forward pointer from Bổ đề 03.12 header.

5. **Line 399**: Removed "ở Phụ lục B" forward pointer from Lộ trình, reworded to "được bỏ qua trong phác thảo này". Kept the "**Lộ trình.**" label per rule.

6. **Line 469**: "**Kết luận.**" → "Tóm lại,". Removed the "Kết luận." label.

**No-ai-slop eval check:**

1. **Preserve user's point without adding claims**: ✓ All edits only cut navigation pointers and relabeled conclusions; no new claims, numbers, or sources added.
2. **Preserve vocabulary/cadence**: ✓ Minimal edits, kept the author's voice.
3. **Leave strong human sentences alone**: ✓ Only touched navigation pointers and "Kết luận." labels.
4. **Proportional cutting**: ✓ Only cut forward pointers, no aggressive compression.
5. **Lead with what reader needs**: ✓
6. **Front-loaded points**: ✓
7. **Sentences earn their place**: ✓
8. **Portability test**: ✓
9. **Active voice**: ✓
10. **Keep useful edge and structure**: ✓ All numbered blocks, numbers, results, and labels cited by exercises preserved.
11. **Tangled sentences fixed**: ✓

**Words to cut**: No banned words introduced.

**Patterns to cut**: Removed navigation/forward pointers ("ở §7", "ở Phụ lục B"). Removed "Kết luận." labels.

**Final read**:
- No robotic symmetry introduced.
- The draft reads naturally.
- All numbered blocks (Định nghĩa 03.11, Bổ đề 03.12, Ví dụ 03.4, 03.5) and all numbers preserved.
- Markdown only uses $...$ and $$...$$.
- No math notation changed.

The section §6 is now consistent with the author's style. All hard constraints are satisfied: no numbered blocks removed, no numbers changed, no results cut, no new claims added, terminology consistent.

## Danh sách các thay đổi đã làm (phần §6, dòng 341–473)

1. **Dòng 353**: bỏ con trỏ điều hướng "trong chứng minh ở §7" → "khi áp dụng cho hai mẫu gộp lại".
2. **Dòng 355**: "Trên mọi mẫu" → "Trên mọi bộ điểm" (thuật ngữ nhất quán với mạch văn).
3. **Dòng 382**: bỏ nhãn "**Kết luận.**" → "Tóm lại," (Ví dụ 03.4).
4. **Dòng 387**: bỏ con trỏ "ở Phụ lục B" khỏi tiêu đề Bổ đề 03.12.
5. **Dòng 399**: bỏ con trỏ "ở Phụ lục B" khỏi "**Lộ trình của (a).**", thay bằng "được bỏ qua trong phác thảo này"; giữ nhãn "**Lộ trình.**".
6. **Dòng 469**: bỏ nhãn "**Kết luận.**" → "Tóm lại," (Ví dụ 03.5).

Không đổi khối đánh số, con số, kết quả, nhãn mà `exercises.md` trích dẫn; không thêm khẳng định hay số liệu mới; không đổi kí hiệu toán; Markdown chỉ dùng `$...$` và `$$...$$`.