The current state of my scope (lines 909-990) is now correct:

- **Line 909:** "cỡ mẫu bất khả diễn" ✓ (already correct)
- **Line 914:** "thuật toán học PAC bất khả diễn" ✓ (already correct)
- **Line 922:** formula rewrite applied ✓
- **Line 978:** reference to Ví dụ 02.9 kept ✓

The first two replacements failed because the text was already in the correct state ("bất khả diễn") when I attempted them — the file had already been updated (likely by a concurrent process or the coordinator's earlier application). My successful replacement was the $\ell_c$ formula rewrite on line 922.

Let me verify the whole scope for any remaining term violations. Checking lines 909-990 for "khả thực", "bất khả tri", "hàm chỉ thị", "trước mẫu", "Đáp án", "mẫu huấn luyện", "phân bố đồng thời", "bản có nhiễu":

From the read, none of these appear in lines 909-990. All terms are correct:
- "khả diễn" / "bất khả diễn" ✓
- "tập huấn luyện" ✓
- "phân bố" ✓
- "Lời giải" ✓

Structure check: Bài tập 02.11 has 1 `::: exercise` (line 911), 3 `::: hint` (lines 927, 931, 935), 1 `::: solution` (line 939). ✓

Step-by-step solution with "**Bước 1/2/3/4**" labels and `aligned` blocks preserved. ✓

No "**Lộ trình.**" label present (correct — exercises don't have it). ✓

All numbers preserved (17,539; 17,538.04; 16·1096.13; 1097; 240; 5.4806; etc.). ✓

Markdown uses only `$...$` and `$$...$$`. ✓

No navigation pointers to cut in my scope (the Phụ lục B.1/B.2 references at lines 443, 453, 488, 490 are outside my scope). ✓

No slop patterns detected. ✓

Let me run the no-ai-slop eval checks:

**Editing principles:**
1. Preserved the point, no added claims/stats ✓
2. Preserved vocabulary/cadence ✓
3. Left strong sentences alone ✓
4. Cutting proportional (only term changes + one optional formula rewrite) ✓
5. Leads with what reader needs ✓
6. Points front-loaded ✓
7. Sentences earn their place ✓
8. No generic sentences ✓
9. Active voice ✓
10. Kept structure ✓
11. No tangled sentences introduced ✓

**Words to cut:** No banned words added ✓

**Patterns to cut:** No binary contrasts, no faux-insight, no metadiscourse added ✓

**Final read:**
1. Checked against eval ✓
2. No robotic symmetry ✓
3. Writer would recognize voice ✓
4. Sounds natural ✓
5. Full draft + What changed section ✓
6. N/A (edit mode) ✓

All checks pass. My work is complete.

## Tóm tắt thay đổi

Trong phạm vi được giao (Bài tập 02.11, dòng 909–990):

1. **Dòng 922 (đề, phần b):** viết lại mô tả hàm lỗi $\ell_c$ bằng lời thành công thức phân trường hợp: `$\ell_c(h,(x,y))=4\cdot\mathbb 1[h(x)=0,\,y=1]+\mathbb 1[h(x)=1,\,y=0]$`. Giữ nguyên các giá trị (1, 4, 0) và không đổi kí hiệu toán.

2. **Dòng 909 và 914:** các cụm "bất khả tri" đã ở trạng thái đúng "bất khả diễn" khi tôi đọc lại (tệp đã được cập nhật trước đó); không cần sửa thêm.

3. **Dòng 978:** giữ nguyên dẫn chiếu hợp lệ tới Ví dụ 02.9 (lấy con số $17\,538{,}04=16\cdot1096{,}13$).

Không có thay đổi nào khác cần thiết trong phạm vi: không còn "khả thực", "bất khả tri", "hàm chỉ thị", "trước mẫu", "Đáp án" trong phần này; cấu trúc khối (1 `::: exercise`, 3 `::: hint`, 1 `::: solution`), các bước "**Bước 1–4**", `aligned`, mọi con số/kết quả và nhãn đều được giữ nguyên.