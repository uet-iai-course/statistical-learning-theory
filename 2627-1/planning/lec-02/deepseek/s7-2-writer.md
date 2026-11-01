Both fixes are correctly applied. The "Lộ trình." label line is removed (proof now begins directly with Bước 1), and the "Theo (T3), mọi $D$ có rủi ro hữu hạn trên $\mathcal H$." sentence is removed from line 771.

Let me run the no-ai-slop eval checks on the final §7 state.

**Editing principles:**
1. Preserves the user's point — no claims, examples, stats added. ✓
2. Preserves author's vocabulary/cadence. ✓
3. Leaves strong human sentences alone. ✓
4. Cutting proportional to slop — only removed navigation pointers, obvious statements, reader-guidance. ✓
5. Leads with what reader needs. ✓
6. Points front-loaded. ✓
7. Sentences earn their place. ✓
8. Generic sentences made specific or cut. ✓
9. Active voice with human subjects. ✓
10. Keeps useful edge and structure. ✓
11. Tangled sentences fixed, clear cadence intact. ✓

**Words to cut:** No banned words, filler, empty adverbs, inflated claims. ✓

**Patterns to cut:**
1. No binary contrasts, negative listings, rhetorical setups, throat-clearing openers. ✓
2. No faux-insight setups, colon reveals, fake-strong verbs, synonym cycling, robotic rhythm. ✓
3. No importance puffery or weasel attribution. ✓
4. Interpretive metadiscourse removed — the "Lộ trình." reader-guidance label was removed. ✓
5. No fake-profound kicker lines. ✓
6. No summary-recap endings — "Tóm lại" sentences are legitimate conclusions of computations, not recap endings. ✓
7. No formatting slop. ✓
8. Colons sentence case. ✓
9. Em dashes used sparingly. ✓

**Final read:**
1. Checked directly against the file. ✓
2. No robotic symmetry, repeated sentence shapes, stacked punchy fragments. ✓
3. Writer would recognize the voice. ✓
4. Sounds natural read aloud. ✓
5. Full edited draft + What changed section. ✓
6. N/A (edit mode). ✓

All checks pass. The §7 section now fully conforms to the author's style rules.

## What changed

Applied the four planned §7 changes (already present in the file and verified correct) plus two minor fixes flagged by the reviewer:

1. **Line 771** — removed the obvious-statement sentence "Theo (T3), mọi $D$ có rủi ro hữu hạn trên $\mathcal H$." (a "câu nói hiển nhiên" per rule 3, since (T3) already bounds the loss in [0,1]). The sentence now reads: "Đây là bảo đảm với xác suất cao cho rủi ro vượt mức so với lớp, không phụ thuộc $D$."

2. **Line 777** — removed the reader-guidance label "**Lộ trình.** Một bước tất định trên biến cố $r$-đại diện, rồi Định lý 02.14." (metacommentary per no-ai-slop "Patterns to cut 4" and the step-label rule). The proof now begins directly with "**Bước 1 (đối tượng so sánh).**".

**Verified intact** (all cited by `exercises.md`): Hệ quả 02.16(c) formula $M(\epsilon,\delta)=\lceil2\ln(2K/\delta)/\epsilon^2\rceil$ (line 767), Ví dụ 02.9's $1097$ (line 808), all numbers ($1096{,}1$, $r_6\approx0{,}676$, $2r_6\approx1{,}35$, $3{,}4657$, $3{,}6889$, $7{,}1546$, $1430{,}9$, $1431$, $0{,}28$, $334$), all numbered blocks, and the "bất khả diễn" terminology throughout §7. No claims, numbers, or sources were added.