All six edits are confirmed in place. Let me verify the changes against the eval criteria:

1. **Line 123**: "Trên một mẫu cố định" → "Trên một tập huấn luyện cố định" ✓
2. **Line 136**: "không phụ thuộc phân bố hay mẫu" → "không phụ thuộc phân bố hay tập huấn luyện"; "lấy từ mẫu" → "lấy từ tập huấn luyện"; "trên mẫu đó" → "trên tập huấn luyện đó" ✓
3. **Line 161**: "**Kết luận.**" → "Tóm lại," ✓
4. **Line 172**: "như vừa thấy sau Định nghĩa 03.1" → "vì cách gán nhãn $(1,0)$ không thực hiện được" ✓
5. **Line 194**: "không có phân bố hay mẫu ngẫu nhiên" → "không có phân bố hay tập huấn luyện ngẫu nhiên" ✓
6. **Line 200**: "(đoạn sau Định nghĩa 03.2)" removed ✓

Let me run through the no-ai-slop eval checks:

**Editing principles:**
1. Preserves the user's point without adding claims — ✓ (only terminology and navigation-pointer changes)
2. Preserves distinctive vocabulary/cadence — ✓ (minimal changes)
3. Leaves strong human sentences alone — ✓
4. Cutting proportional to actual slop — ✓ (only removed navigation pointers and "Kết luận." label)
5. Leads with what reader needs — ✓
6. Points front-loaded — ✓
7. Sentences earn their place — ✓
8. Generic sentences pass portability test — ✓
9. Active voice — ✓
10. Keeps useful edge and structure — ✓
11. Tangled sentences fixed — ✓

**Words to cut:** No banned words introduced.

**Patterns to cut:**
1. Binary contrasts, negative listings, rhetorical setups — ✓ (none introduced)
2. Faux-insight setups, colon reveals — ✓
3. Importance puffery — ✓
4. Interpretive metadiscourse — ✓ (removed navigation pointers)
5. Fake-profound kicker lines — ✓
6. Summary-recap endings — ✓
7. Formatting slop — ✓
8. Colons sentence case — ✓
9. Em dashes — ✓ (none added)

**Final read:**
1. Checked directly against eval.md — ✓
2. Avoids robotic symmetry — ✓
3. Writer would recognize the draft — ✓
4. Sounds natural — ✓
5. Full edited draft + What changed — ✓ (below)
6. N/A (not a detect request)

All constraints satisfied:
- Vietnamese academic standard ✓
- All numbered blocks preserved (Định nghĩa 03.1–03.3, Nhận xét 03.4, Mệnh đề 03.5–03.6, Ví dụ 03.2) ✓
- All numbers preserved ✓
- All results and labels cited by exercises preserved ✓
- Only cut sentences, not results ✓
- No new claims, numbers, or sources added ✓
- Markdown uses only $...$ and $$...$$ ✓
- No math notation changed ✓

## What changed

Edited §4 (lines 121–236) of `2627-1/materials/lec-03/lecture-note.md`:

1. **Thuật ngữ "mẫu" → "tập huấn luyện"** (3 chỗ): "Trên một mẫu cố định" → "Trên một tập huấn luyện cố định"; "không phụ thuộc phân bố hay mẫu" → "…hay tập huấn luyện"; "lấy từ mẫu" → "lấy từ tập huấn luyện"; "trên mẫu đó" → "trên tập huấn luyện đó" (dòng 123, 136).
2. **Bỏ nhãn "**Kết luận.**"** trong Ví dụ 03.2, thay bằng "Tóm lại," (dòng 161).
3. **Bỏ câu điều hướng** "như vừa thấy sau Định nghĩa 03.1", thay bằng nêu trực tiếp lý do "vì cách gán nhãn $(1,0)$ không thực hiện được" (dòng 172).
4. **Thuật ngữ "mẫu ngẫu nhiên" → "tập huấn luyện ngẫu nhiên"** trong Bảo đảm của Mệnh đề 03.5 (dòng 194).
5. **Bỏ câu điều hướng** "(đoạn sau Định nghĩa 03.2)" trong Bước 1 của chứng minh Mệnh đề 03.5 (dòng 200).