VERDICT: yêu cầu sửa

Tôi đã tự kiểm lại từng phát hiện của báo cáo phản biện trên tệp `2627-1/materials/lec-03/lecture-note.md` (dòng 238–337, §5) và đối chiếu với `exercises.md`. Cả bốn phát hiện đều chính xác và nằm trong phạm vi §5. Các thay đổi trong diff của §5 đều đúng hướng và không cắt mất con số hay kết quả nào; không có phát hiện nào sai cần bỏ.

**Lí do yêu cầu sửa:** Hai câu điều hướng tới Phụ lục A còn sót trong tiêu đề hai khối đánh số (Bổ đề 03.8, Mệnh đề 03.9) vi phạm trực tiếp quy tắc cắt "Phụ lục B chứng minh …" (CLAUDE.md "Navigation and forward pointers"; `van-phong-tac-gia.md` §7 mục 3). Người đọc không cần mở Phụ lục để lấy số hay phát biểu — phát biểu của bổ đề/mệnh đề đã nêu đầy đủ trong khối. Đây là lỗi trung bình, thuộc phạm vi §5, cần sửa.

**Danh sách sửa cụ thể cho writer:**

1. **Dòng 259 (bắt buộc).** Văn bản hiện có:
   `::: lemma Bổ đề 03.8 (Phân hoạch Radon) — chứng minh đầy đủ ở Phụ lục A`
   Văn bản đích:
   `::: lemma Bổ đề 03.8 (Phân hoạch Radon)`

2. **Dòng 274 (bắt buộc).** Văn bản hiện có:
   `::: proposition Mệnh đề 03.9 (Chiều VC của lớp nửa không gian) — chứng minh đầy đủ (cận trên của phần (b) ở Phụ lục A)`
   Văn bản đích:
   `::: proposition Mệnh đề 03.9 (Chiều VC của lớp nửa không gian)`

3. **Dòng 293 (khuyến nghị).** Văn bản hiện có:
   `…vì ma trận có các hàng $(x_i^\top,1)$ khả nghịch (Bài tập 03.3).`
   Văn bản đích:
   `…vì ma trận có các hàng $(x_i^\top,1)$ khả nghịch.`
   (Khẳng định đã nêu đủ trong câu; dẫn chiếu bài tập là con trỏ điều hướng, không cần mở để lấy số/phát biểu.)

4. **Dòng 333 (khuyến nghị).** Văn bản hiện có:
   `…nên $d=\infty$ (Bài tập 03.5).`
   Văn bản đích:
   `…nên $d=\infty$.`
   (Tương tự, khẳng định $d=\infty$ đã nêu đủ.)

**Ghi chú không phải lỗi (giữ nguyên):** dòng 257 "Bổ đề dưới đây khẳng định điều này…" (dẫn tới khối liền kề) và dòng 310 "Lớp của ứng dụng ở §3…" (dẫn tới đối tượng cụ thể cần mở để biết lớp nào) — đúng theo quy tắc "giữ khi người đọc cần mở để lấy số/phát biểu".

**Xác nhận các thay đổi diff của §5 đều hợp lệ:** in nghiêng thuật ngữ mới "nửa không gian" (dòng 240); cắt "quy ước này được dùng trong chứng minh cận trên dưới đây" (dòng 253); "được chứng minh ở Phụ lục A bằng…" → "dùng…" (dòng 308); cắt "ở Bước 1 của chứng minh trên" (dòng 316); "**Kết luận.**" → "Tóm lại," (dòng 324); cắt "nhận xét sau cho thấy…" (dòng 327). Mọi khối đánh số, con số ($d=p+1$, $d=p$, $d=11$, $d=3$, $d=\infty$, $d=1$, $b=1$, $w=(-2,0)$, $b=-1$, $w=(2,2)$, $z=(\tfrac12,\tfrac12)$, $14$ cách, $8$ cách) đều nguyên vẹn.