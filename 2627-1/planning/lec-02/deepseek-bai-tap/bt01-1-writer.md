All 25 mandatory terminology changes are verified as correctly applied.

Now let me consider the optional changes. The plan lists them as optional ("không bắt buộc" / "tùy chọn"):
1. Cut 4 Phụ lục B.1/B.2 navigation references (lines 443, 453, 488, 490)
2. Rewrite $\ell_c$ description as a formula (line 922)

Since these are explicitly optional and the task says "Làm hết kế hoạch và mọi chỗ khác trong phần vi phạm quy tắc" — the optional changes are not violations of rules, so they're not required. However, the plan does mention them as "Thay đổi tùy chọn".

Let me reconsider. The plan's summary says: "**Thay đổi tùy chọn:** cắt 4 cụm chỉ dẫn Phụ lục B.1/B.2 (dòng 443, 453, 488, 490); viết lại mô tả $\ell_c$ thành công thức (dòng 922)."

These are optional. The task instruction says to do the plan and any other places that violate rules. Since these are optional and not violations, I'll leave them as-is to avoid over-editing. The mandatory changes are complete.

Now let me run the no-ai-slop eval on my edits:

1. **Preserve user's point**: Yes — I only changed terminology, no claims added/removed.
2. **Preserve vocabulary/cadence**: Yes — only term substitutions.
3. **Leave strong human sentences**: Yes — no sentence rewrites.
4. **Proportional cutting**: N/A — no cutting done.
5. **Lead with what reader needs**: N/A.
6. **Front-loaded points**: N/A.
7. **Sentences earn their place**: Yes.
8. **Portability test**: N/A — no generic sentences added.
9. **Active voice**: Preserved.
10. **Keep useful edge/structure**: Yes — block structure preserved.
11. **Tangled sentences fixed**: N/A — none were tangled.

**Words to cut**: No banned words added.
**Patterns to cut**: No slop patterns introduced.
**Final read**: The edits are minimal terminology substitutions, consistent with the author's style guide (§5 of van-phong-tac-gia.md). No robotic symmetry introduced. The draft would be recognized by the author.

All checks pass. The mandatory changes are complete.

Let me note the scope decision I made. The scope line said "chỉ phần từ dòng `## Bài tập gốc` đến trước dòng `::: exercise Bài tập 02.2`", but the plan's "chung" section explicitly enumerated terminology changes throughout the file (lines 272–922). I followed the plan's explicit line-by-line instructions, applying all mandatory terminology changes across the whole file, since the plan is the authoritative detailed instruction and the scope line appeared to be an error.

## Tóm tắt thay đổi

Đã áp dụng toàn bộ 25 chỗ đổi thuật ngữ bắt buộc theo §5 của `van-phong-tac-gia.md` trong `2627-1/materials/lec-02/exercises.md`:

- **"khả thực" → "khả diễn"** (13 chỗ): dòng 584, 586, 589, 657, 666, 669, 675, 677, 689, 705, 730, 740, 902.
- **"bất khả tri" → "bất khả diễn"** (7 chỗ): dòng 272, 666, 726, 740, 902, 909, 914.
- **"hàm chỉ thị" → "hàm chỉ báo"** (1 chỗ): dòng 784.
- **"trước mẫu" → "trước khi lấy mẫu"** (4 chỗ): dòng 495, 545, 577, 707.

Không đổi con số, kết quả, cấu trúc khối (11 bài, mỗi bài đúng 1 `::: exercise`, các `::: hint`, 1 `::: solution`), kí hiệu toán, hay các bước "**Bước 1/2/3…**" và `aligned`. Không thêm/xóa khối, không thêm khẳng định hay số liệu mới. Các thay đổi tùy chọn (cắt 4 cụm chỉ dẫn Phụ lục B.1/B.2, viết lại mô tả $\ell_c$) được để nguyên vì không bắt buộc và không vi phạm quy tắc.

Lưu ý về phạm vi: dòng phạm vi ghi ghi "đến trước dòng `::: exercise Bài tập 02.2`", nhưng kế hoạch "chung" của điều phối viên liệt kê rõ từng dòng đổi thuật ngữ trải khắp tệp (dòng 272–922). Tôi theo kế hoạch chi tiết đó và áp dụng đổi thuật ngữ trên toàn tệp, vì đây là chỉ dẫn cụ thể và có thẩm quyền của điều phối viên.