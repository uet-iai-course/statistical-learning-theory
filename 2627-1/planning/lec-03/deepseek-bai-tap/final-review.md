# Báo cáo phản biện — `2627-1/materials/lec-03/exercises.md` (diff so với HEAD)

Tôi đã đọc toàn bộ tệp bài tập, ghi chú Bài 03 (chỉ đọc), ghi chú Bài 01/02 (để đối chiếu dẫn chiếu), `van-phong-tac-gia.md` và `thuat-ngu.md`, rồi kiểm từng dòng trong diff.

## Kết luận chung

**Không phát hiện lỗi nào cần sửa.** Toàn bộ các thay đổi trong diff đều nhất quán với quy tắc văn phong tác giả, thuật ngữ chuẩn, và mọi dẫn chiếu tới ghi chú Bài 03 đã sửa vẫn còn đúng. Không có khối đánh số, con số, kết quả hay công thức nào bị đổi; không thêm khẳng định mới; cấu trúc khối exercise/hint/solution giữ nguyên (12 exercise, 12 solution, 35 hint — không thêm/bớt khối nào).

## Bảng phát hiện

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|
| — | — | Không có phát hiện nào | Xem tóm tắt kiểm tra bên dưới | — |

## Tóm tắt kiểm tra đã thực hiện

**1. Thuật ngữ (đối chiếu `thuat-ngu.md` §5, §7 và `van-phong-tac-gia.md` §5):**
- `khả thực` → `khả diễn` (dòng 774, 799, 840, 846, 856) và `bất khả tri` → `bất khả diễn` (dòng 779, 848, 850) — đúng. Không còn sót `khả thực`/`bất khả tri`/`chỉ thị` nào trong tệp.
- `mẫu` → `tập huấn luyện` khi chỉ dữ liệu huấn luyện (dòng 231, 789, 801, 812) — đúng. Các trường hợp giữ "mẫu" đều hợp lệ: "mẫu bóng", "cỡ mẫu", "lấy mẫu", "mẫu gộp", "xem mẫu" (khớp ghi chú dòng 23, 643, 648, 885 dùng "sau khi xem mẫu").
- `véc-tơ chỉ thị` → `véc-tơ chỉ báo` (dòng 516) — đúng.
- "trước khi lấy mẫu" (dòng 380, 446) — đúng, không có "trước mẫu".
- "nghiêm ngặt" (dòng 114, 647) — đúng, không dùng "ngặt".

**2. Dẫn chiếu tới ghi chú Bài 03 (đã sửa, chỉ đọc):**
- Dòng 250: "hai lý do (i), (ii) ở §7" — đúng, các lý do (i),(ii) nằm ở §7 (ghi chú dòng 537–538). Việc bỏ "đứng trước (T5)" là cắt câu điều hướng, đúng quy tắc.
- Dòng 436: "trường hợp $d=0$" — đúng, ghi chú dòng 579 nêu "Khi $d=0$, … $\Pi_{\mathcal H}=1$". Bỏ "đoạn sau Định lý 03.15" là cắt câu điều hướng, đúng quy tắc.
- Dòng 472: bỏ câu "Bài tập 03.8(a) chứng minh bất đẳng thức của (d) bằng quy nạp." — đây là câu điều hướng chéo, cắt đúng quy tắc; lời giải 03.6(d) dùng lập luận phép dồn nên không phụ thuộc câu này.
- Các dẫn chiếu khác đều còn tồn tại trong ghi chú: Định nghĩa 03.3/03.7/03.11, Mệnh đề 03.5/03.6/03.9, Nhận xét 03.4/03.10, Ví dụ 03.3–03.10, Bổ đề 03.8/03.12, Hệ quả 03.16, Định lý 03.15/03.17, Phụ lục A/B/C (C.1–C.7), "Chỗ dùng" trong lộ trình chứng minh.
- Dẫn chiếu chéo Bài 01/02: Định nghĩa 01.4/01.16/01.18/01.20, Nhận xét 01.26/01.30, Định lý 02.7/02.14, Bổ đề 02.3/02.12, Hệ quả 02.16 — tất cả còn tồn tại và nội dung khớp (vd. Nhận xét 01.26 dòng 1006 đúng với khẳng định ở dòng 848; $r_m^2=\ln(2K/\delta)/(2m)$ của Định lý 02.14 khớp dòng 750 lec-02).

**3. Cấu trúc khối và lời giải từng bước:**
- Số khối exercise/hint/solution không đổi (12/35/12). Không khối nào bị thêm/bớt.
- Đánh số lại Bước 2/3/4 → 5/6/7 trong Bài tập 03.7(b) (dòng 576–580) làm số bước chạy liên tục 1–7 toàn lời giải; không gộp bước tính toán thật sự, không phá dẫn chiếu (hint và "Kiểm tra lại" không tham chiếu số bước).
- Không xóa nhãn "**Lộ trình.**" hay câu lộ trình nào; không có "Đáp án" (chỉ "Lời giải").

**4. Con số, kết quả, công thức, KaTeX:**
- Mọi thay đổi trong diff đều là văn bản thuần (sửa chính tả, thuật ngữ, cắt câu điều hướng, đánh số bước); không đổi kí hiệu toán, con số hay kết quả. Các công thức `$...$`/`$$...$$` và `aligned` giữ nguyên, KaTeX hợp lệ.
- Các phép tính trong lời giải (vd. $\rho_{1000}=\sqrt{8\ln80/1000}\approx0{,}187$, tỉ số $16$, điều kiện $m\epsilon^2\ge2\ln4\approx2{,}77$) đã kiểm lại và đúng — không bị diff đụng tới.

**5. Tiếng Việt và ngữ pháp sau khi cắt:**
- "kiểm rằng" → "kiểm tra rằng" (dòng 33), "kiểm giả thiết" → "kiểm tra giả thiết" (dòng 178), "khoảng một điểm" → "các khoảng một điểm" (dòng 114) — đều là sửa chính tả/ngữ pháp đúng.
- Các câu sau khi cắt (dòng 250, 436, 472) còn đúng ngữ pháp và nghĩa.

**6. no-ai-slop:** Các thay đổi không đưa vào filler, câu rào đón, mở bài giả tạo, kết luận sáo rỗng, hay định dạng thừa; giữ giọng tác giả.

**Ghi chú thông tin (không phải phát hiện):** hai chỗ cắt câu điều hướng (dòng 250, 436) và một câu dẫn chéo (dòng 472) đều nằm trong phạm vi quy tắc "cắt câu điều hướng/báo trước", nên không cần sửa. Không có thay đổi nào ngoài tệp bài tập.