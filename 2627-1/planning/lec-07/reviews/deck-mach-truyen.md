# Duyệt deck Bài 07 — Vai 5 `mach-truyen` (mạch truyện, liên kết, thống nhất thứ tự với ghi chú)

Người duyệt: tác tử vai 5, chỉ đọc. Ngày 2026-11-16. Bản đóng băng: `2627-1/lecture-07-mang-no-ron-tham-so-hoa-thua.html` (55 trang, 7 mạch). Đối chiếu: `materials/lec-07/lecture-note.md`, `exercises.md`, `planning/lec-07/storyboard.md` (mục 16), `review-log.md` § "Bộ trang chiếu", decks 01–06.

Đã chạy (thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-07/rv-mach-truyen/nav.py`, Playwright, 1600×900):

- `#/1`…`#/7` mở đúng `L07-1-01`, `L07-2-00`, …, `L07-7-00`; bấm sáu liên kết của trang Nội dung (`#/2`…`#/7`) tới đúng sáu trang tiêu đề mạch, tiêu đề khớp chữ liên kết; tổng 55 trang.
- Hai liên kết viewer ở `L07-7-07` trả 200, mở đúng ghi chú và tệp bài tập Bài 07, có nút "Bộ trang chiếu" trỏ về deck (`&deck=` hoạt động); không page error, không request lỗi.
- `deck_lint.py`: 0 phát hiện.

## 1. Bảng chức năng từng trang

| Trang | Vai trò trong mạch | Kết nối vào | Kết nối ra |
|---|---|---|---|
| 1-01 | bìa, luận điểm một câu có điều kiện | — | câu hỏi về năng lực thống kê |
| 1-02 | nhắc lại 03.15, 03.9, 04.3, 02.7, 02.10; kí hiệu Bài 05 | Bài 02–05 | $\rho_m$ dùng ở 2-11, 6-01; ba số hạng 04.3 dùng ở 2-06 |
| 1-03 | năm mục tiêu | — | mục tiêu 1→mạch 2, 2→3, 3→4, 4→5, 5→6–7 |
| 1-04 | Nội dung, sáu liên kết `#/2`–`#/7` | — | — |
| 1-05 | một hộp "Câu hỏi:" | — | trả lời ở 7-03 |
| 1-06 | thí nghiệm nhãn thật/hoán vị, "Câu hỏi: vì sao lỗi kiểm tra khác nhau?" | 1-05 | 2-11, 3-05, 4-04, 6-03, 6-04 dùng lại |
| 2-00 | dẫn mạch 2 | 1-06 | — |
| 2-01 | thiết lập, giả thiết (T1), (T3), (T5), (M) | 1-06 | mọi phát biểu sau dùng các nhãn này |
| 2-02 | Ví dụ 07.1; câu hỏi phân lớp văn bản | 1-02 (03.15) | 2-04/2-05 (phép hoặc loại trừ); 6-01 (văn bản) |
| 2-03 | Định nghĩa 07.1 | 2-01 | 2-04 |
| 2-04 | trực quan + Mệnh đề 07.2 | 2-02, 2-03 | 2-05 |
| 2-05 | ý tưởng chứng minh 07.2; bỏ lớp ẩn thì hỏng | 2-04, 2-02 | 2-06 |
| 2-06 | Nhận xét 07.3; ba năng lực ↔ ba số hạng 04.3 | 1-02 (04.3), 2-05 | 2-07 (số hạng tối ưu); 2-08 (số hạng thống kê) — **câu nối thiếu trên mặt trang** (P4) |
| 2-07 | Bài tập 07.5(c): hàm mục tiêu không lồi | 2-04, 2-06 | — |
| 2-08 | Định nghĩa 07.4: tham số hóa thừa, nội suy | Bài 03 (Nhận xét 03.10) | 2-09, 2-11 |
| 2-09 | Định nghĩa 07.5: lớp kiến trúc, lớp bị chặn theo chuẩn, mô hình do huấn luyện chọn | 2-08 | 2-10, 5-05, 6-04 |
| 2-10 | Ví dụ 07.2: đổi tỉ lệ | 2-04, 2-09 | 6-06 (ghi chú), 7-03 (ghi chú) |
| 2-11 | Ví dụ 07.3: $P$, $d$, $\rho_m$ như nhau với hai loại nhãn | 1-06, 2-08, 2-09, 1-02 | 3-01 (giới hạn của chiều VC) |
| 3-00 | dẫn mạch 3 | 2-11 | — |
| 3-01 | Định nghĩa 07.7; câu nối 2→3 | 2-11 | 3-02, 3-03 |
| 3-02 | Ví dụ 07.4 (bảng bốn lớp) + Bổ đề 07.8 | 3-01 | 3-06 (đối chiếu $\tfrac14$); Bổ đề 07.8 không dùng lại trên mặt trang nào (P9) |
| 3-03 | trực quan + Mệnh đề 07.9 | 3-01 | 3-04, 3-05 |
| 3-04 | ý tưởng chứng minh 07.9 | 3-03 | 3-05 |
| 3-05 | Ví dụ 07.5: $\widehat{\mathfrak R}=\tfrac12$ với $P=2000$ và $P=1$ | 2-11, 3-03(c) | 4-04, 7-05 |
| 3-06 | Bài tập 07.2(c) | 3-02, 3-03 | — |
| 4-00 | dẫn mạch 4 | 3-05 | — |
| 4-01 | Bổ đề 07.10; vì sao Hoeffding không đủ | 1-02 (Hoeffding) | 4-03 bước 4 |
| 4-02 | trực quan + Định lý 07.11 | 3-01, 3-03, 2-01 | 4-03, 4-04, 5-06 bước 1 |
| 4-03 | ý tưởng chứng minh 07.11; nhắc đối xứng hóa và mẫu bóng | Bài 03, 4-01 | 4-04, 4-05 |
| 4-04 | Ví dụ 07.6; câu nối 4→5 ("cần lớp nhỏ hơn …") | 3-05, 4-02 | 5-01 |
| 4-05 | Bài tập 07.2(b) | 4-02, 4-03, 1-02 (02.10) | — |
| 5-00 | dẫn mạch 5 | 4-04 | — |
| 5-01 | trực quan + Mệnh đề 07.13; câu nối (lớp ẩn cố định) | 2-11, 4-04 | 5-02, 5-06 bước 3 |
| 5-02 | ý tưởng chứng minh 07.13 + Ví dụ 07.7 | 5-01 | 5-07 |
| 5-03 | Bổ đề 07.14 | 3-01, 1-02 (Lipschitz) | 5-04, 5-06 |
| 5-04 | Định nghĩa 07.15, hình hàm lỗi dốc | 5-03 ("0–1 không Lipschitz") | 5-05 |
| 5-05 | trực quan + Hệ quả 07.16 | 5-01, 5-03, 5-04 | 5-06, 6-01 |
| 5-06 | ý tưởng chứng minh 07.16; chọn $\gamma$ theo $S$ thì hỏng | 4-02, 5-03, 5-01 | 6-02 |
| 5-07 | Bài tập 07.3(d) | 5-01 | — |
| 6-00 | dẫn mạch 6 | 5-05 | — |
| 6-01 | Ví dụ 07.8: trả lời câu hỏi văn bản của 2-02 | 2-02, 5-05 | — (liên kết ngược 2-02 chỉ ở ghi chú, P10) |
| 6-02 | Nhận xét 07.17 (lưới lề) | 5-06, Bài 04 | 6-04, 7-06 |
| 6-03 | Ví dụ 07.10 bước 1–2: chuẩn, lề chuẩn hóa | 1-06, 2-11 | 6-04, 7-03 |
| 6-04 | Ví dụ 07.10 bước 3–4: cận $>1$, tập kiểm tra | 6-02, 6-03, 1-02 (02.10) | 7-03 |
| 6-05 | Ví dụ 07.11: bỏ "hàm lỗi trong $[0,1]$" | 4-02, 5-01, 5-03 | 7-06 câu 4 |
| 6-06 | Nhận xét 07.18 (đọc thêm), câu nối 6→7 | 2-10 (ghi chú), 5-05 | 7-02 |
| 7-00 | dẫn mạch Tổng kết | — | — |
| 7-01, 7-02 | bảng tổng kết năm kết quả | toàn deck | 7-03 |
| 7-03 | Vấn đề trung tâm cuối | 1-05 | — (P2) |
| 7-04, 7-05 | bài tập tổng hợp 07.4(b), (c) | 2-08, 3-03, 3-05, 4-04; **Định lý 02.14, (T4) chưa nhắc** (P1) | — |
| 7-06 | bốn câu tự kiểm tra (= §12 (a), (c) và hai câu từ 07.9, 07.11) | 3-03, 4-03, 5-05, 6-05 | — |
| 7-07 | bảng `Mục \| Bài tập`, liên kết viewer | — | — |
| 7-08 | tài liệu, dòng Bài 08 | — | Bài 08 |

Mỗi trang nội dung phục vụ câu hỏi của mạch mình; không có trang trùng chức năng. Câu hỏi hoặc ý cốt lõi của từng mạch xuất hiện trên mặt trang trước nửa sau của mạch: dòng dẫn mạch ở 2-00…6-00, cộng dòng mở đầu ở 3-01, 4-01, 5-01, 6-02. Mạch 2 dài 12 trang có hai cụm (biểu diễn, 2-01…2-07; đếm tham số, 2-08…2-11) nhưng chỉ dòng dẫn mạch nối hai cụm (P4).

## 2. Bảng đối chiếu trang → mục ghi chú

| Mạch | Trang | Mục, khối của ghi chú | Thứ tự |
|---|---|---|---|
| 1 | 1-01…1-05 | đoạn mở đầu, Mục tiêu học tập, Kiến thức tiên quyết, §13 | khớp |
| 1 | 1-06 | Câu hỏi mở đầu, Phụ lục D | khớp (đặt sau Vấn đề trung tâm như deck 06) |
| 2 | 2-01 | §1, §2 | khớp |
| 2 | 2-02 | §3: Ví dụ 07.1, khối ứng dụng | khớp |
| 2 | 2-03…2-06 | §4: Định nghĩa 07.1, Mệnh đề 07.2, Nhận xét 07.3 | khớp |
| 2 | 2-07 | Bài tập 07.5(c) (mục tiêu §4) | khớp |
| 2 | 2-08…2-11 | §5: Định nghĩa 07.4, 07.5, Ví dụ 07.2, 07.3 (Nhận xét 07.6 ở ghi chú diễn giả) | khớp |
| 3 | 3-01…3-05 | §6: Định nghĩa 07.7, Bổ đề 07.8 + Ví dụ 07.4, Mệnh đề 07.9, Ví dụ 07.5 | Bổ đề 07.8 đặt sau Ví dụ 07.4 trên cùng trang (ghi chú: bổ đề trước); lý do ở storyboard 16.2, chấp nhận được |
| 3 | 3-06 | Bài tập 07.2(c) | khớp |
| 4 | 4-01…4-04 | §7: Bổ đề 07.10, Định lý 07.11, chứng minh, Ví dụ 07.6 (Nhận xét 07.12 ở ghi chú diễn giả) | khớp |
| 4 | 4-05 | Bài tập 07.2(b) | khớp |
| 5 | 5-01…5-06 | §8: Mệnh đề 07.13, Ví dụ 07.7, Bổ đề 07.14, Định nghĩa 07.15, Hệ quả 07.16 | khớp; lề chuẩn hóa (§8, sau Định nghĩa 07.15) chuyển sang 6-03, nơi dùng đến, có ghi trong nguồn của 6-03 và storyboard 16.2: chấp nhận được |
| 5 | 5-07 | Bài tập 07.3(d) | khớp |
| 6 | 6-01…6-06 | §9: Ví dụ 07.8, Nhận xét 07.17, Ví dụ 07.10, 07.11, Nhận xét 07.18 (Ví dụ 07.9 ở ghi chú diễn giả 6-05) | khớp |
| 7 | 7-01…7-03 | §10 | khớp |
| 7 | 7-04, 7-05 | Bài tập 07.4(b), (c) | khớp |
| 7 | 7-06 | §12 (a), (c); Mệnh đề 07.9; Định lý 07.11 | khớp |
| 7 | 7-07, 7-08 | §11, §12 đoạn cuối, §13 | khớp |

Mỗi mạch ứng với các mục liên tiếp: mạch 2 ↔ §1–§5 (gộp đã được điều phối viên chấp nhận, kèm điều kiện câu nối trên mặt trang), mạch 3 ↔ §6, mạch 4 ↔ §7, mạch 5 ↔ §8, mạch 6 ↔ §9, mạch 7 ↔ §10–§13.

## 3. Kiểm cấu trúc và tính liên tục

| Điểm kiểm | Kết quả |
|---|---|
| Số mạch, trang Nội dung, `#/N` | 7 mạch; Nội dung liệt kê mạch 2–7 với `<ol start="2">`, sáu liên kết `#/2`…`#/7` mở đúng trang tiêu đề mạch (đã bấm thử) |
| Vấn đề trung tâm mở đầu (1-05) | một hộp, một "Câu hỏi:" thật, chữ thường, không kí hiệu mới; năm câu trả lời theo mạch ở ghi chú diễn giả |
| Vấn đề trung tâm cuối (7-03) | trả lời đúng hướng nhưng chưa thành câu trả lời bằng lời cho cả bài; thiếu phạm vi và giới hạn (P2) |
| Tổng kết không thêm khái niệm mới | đạt, trừ "Nhận xét 07.6" lần đầu lên mặt trang ở 7-02 (P7) và Định lý 02.14, (T4) chưa nhắc ở 7-04/7-05 (P1) |
| Thứ tự trang Tổng kết | bảng tổng kết → Vấn đề trung tâm → bài tập tổng hợp (đề, lời giải) → câu hỏi tự kiểm tra → bài tập về nhà → tài liệu tham khảo: đúng `CLAUDE.md` |
| Câu hỏi tự kiểm tra | bốn câu, mỗi câu trả lời được từ ghi chú (Mệnh đề 07.9(b); chứng minh Định lý 07.11 Bước 4; §12 (a); §12 (c)) |
| Bảng `Mục \| Bài tập` (7-07) | khớp `exercises.md`: 07.1, 07.5, 07.7, 07.8, 07.9 cần đến §4–§5 (mạch 2); 07.2 cần Định lý 07.11 ở (b) (mạch 4); 07.3(e) cần Ví dụ 07.11, 07.4(a) cần Ví dụ 07.10, 07.6 cần Nhận xét 07.17 (mạch 6). Tên mục trùng chữ tiêu đề mạch. Mạch 3 và 5 không có bài nào mà kiến thức cuối cùng cần đến nằm ở đó: đúng quy tắc |
| Trang bài tập ↔ `exercises.md` | 2-07 (07.5(c)), 3-06 (07.2(c)), 4-05 (07.2(b)), 5-07 (07.3(d)), 7-04/7-05 (07.4(b), (c)) mang số hiệu trên mặt trang, đúng phần, có "Lời giải:" |
| Liên kết viewer, bài sau | hai liên kết `&deck=` đúng; "Bài 08: Tính ổn định của SGD và tổng quát hóa trong học sâu." khớp tiêu đề ghi chú Bài 08, chữ thường như dòng "Bài 07" của deck 06 |
| Xem trước bài sau trên mặt trang | không; Bài 08 chỉ ở dòng cuối 7-08 và ghi chú diễn giả |
| Từ khóa mạch trên mặt trang | mọi mục của `strand-keys` (mạch 2–6) có trên ít nhất một mặt trang nội dung của mạch |
| Hành trình khái niệm | Mệnh đề 07.2: 2-02 → 2-04 → 2-05 (bỏ lớp ẩn); Mệnh đề 07.9: 3-02 → 3-03 → 3-04 → 3-05, 3-06; Định lý 07.11: 4-02 → 4-03 → 4-04 → 4-05, 6-05; Mệnh đề 07.13: 5-01 → 5-02 (Ví dụ 07.7) → 5-07; Hệ quả 07.16: 5-04 → 5-05 → 5-06 → 6-01, 6-02. Mỗi kết quả chính có trang "Ý tưởng chứng minh" riêng |

**Liên tục với deck 01–06.**

| Mục | Deck trước | Deck 07 | Đánh giá |
|---|---|---|---|
| Chiều VC, Định lý 03.15 | L03: $\rho_m=\sqrt{8\ln(4\Pi_{\mathcal H}(2m)/\delta)/m}$ | 1-02 nhắc đúng dạng, đúng giả thiết; 2-11, 6-01 dùng $\rho_m$ | đạt; kí hiệu $d$ chưa nêu trên mặt trang (P8) |
| Đối xứng hóa, mẫu bóng | L03 "Kỹ thuật. Đối xứng hóa (symmetrization)", từ khóa "mẫu bóng · đổi chỗ" | 4-03 "Nhắc lại: đối xứng hóa và mẫu bóng (Bài 03)", một dòng; bước 2 "Đổi chỗ" | đạt, đúng tên kỹ thuật |
| Chia xác suất thất bại theo trọng số | L04, tiêu đề trang cùng tên | 6-02 "Nhắc lại: chia xác suất thất bại theo trọng số (Bài 04)" | đạt |
| Định lý 02.14, (T4) | L02-5-03: (T1)–(T4), $r_m=\sqrt{\ln(2K/\delta)/(2m)}$ | 7-04, 7-05 dùng "Định lý 02.14(a)", "$r_m$", "(T4)" mà không nhắc lại | P1 |
| Bổ đề Hoeffding | L02 | 4-01 "bổ đề Hoeffding chặn từng bước"; 1-02 chỉ nhắc Định lý 02.7 | P11 |
| Tính ổn định, Bài 06 | L06-7-03 mặt trang: "mạng nơ-ron: hàm lỗi không lồi"; dòng cuối L06 hỏi đại lượng cho lớp mạng khớp cả nhãn ngẫu nhiên | lý do cận ổn định không dùng được chỉ ở ghi chú diễn giả 1-01, 2-01; mẫu lân cận (Định nghĩa 06.9) ở ghi chú diễn giả 4-03 | P6 |
| Bố cục mạch 1, Tổng kết | L06: Tiên quyết → Mục tiêu → Nội dung → Vấn đề trung tâm → ví dụ dẫn nhập; bảng tổng kết tách "(tiếp)" | giống | đạt |
| Số hiệu ví dụ trên mặt trang | L06 ghi "**Ví dụ 06.k.**" ở mọi trang ví dụ | deck 07 chỉ ghi Ví dụ 07.1, 07.7 | P3 |
| Vấn đề trung tâm cuối | L06-7-03 mở bằng một câu trần thuật trả lời, kết bằng giới hạn | 7-03 mở bằng cụm danh từ, không nêu giới hạn | P2 |

## 4. Phát hiện

| # | Mức độ | Trang chiếu | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|---|
| P1 | nghiêm trọng | L07-7-04, L07-7-05 | Bài tập tổng hợp dùng Định lý 02.14(a), bán kính $r_m$ và giả thiết (T4) mà không trang nào trước đó nhắc lại; người học không kiểm được giả thiết hay tính $r_m$ từ deck. Vi phạm "định nghĩa hoặc nhắc lại trước khi dùng"; mạch Tổng kết không được đưa vào kết quả mới. | 7-04: "Kiểm giả thiết, tính $r_m$ của Định lý 02.14(a)."; 7-05: "(T4) lớp hữu hạn; $r_m=\sqrt{\ln(2\cdot3/\delta)/(2m)}$". 1-02 chỉ nhắc 03.15, 03.9, 04.3, 02.7, 02.10; 2-01 chỉ đặt (T1), (T3), (T5), (M). Ghi chú phần tiên quyết cũng không có 02.14 (đề xuất đã ghi trong `review-log.md`). | Thêm một dòng đầu 7-04: "**Nhắc lại:** Định lý 02.14(a): (T1), hàm lỗi trong $[0,1]$, (T4) lớp hữu hạn chọn trước; với xác suất ít nhất $1-\delta$, $\sup_{h}\lvert L_S(h)-L_D(h)\rvert\le r_m=\sqrt{\ln(2\lvert\mathcal H\rvert/\delta)/(2m)}$." Viết $\lvert\mathcal H\rvert$, không $K$, theo quyết định mục 11.12. Đếm lại mật độ 7-04 (trần 60); nếu vượt, chuyển câu "Có tham số hóa thừa …" sang dòng (c) hoặc rút gọn đề theo chữ `exercises.md`. |
| P2 | trung bình | L07-7-03 | Trang Vấn đề trung tâm cuối chưa trả lời bằng lời cho cả bài: dòng đầu là cụm danh từ, dòng 2 dùng "nó" chỉ sang dòng khác; không nêu phạm vi (cận theo chuẩn chỉ cho lớp tuyến tính, tức lớp ẩn cố định) và hai giới hạn §10 dùng để trả lời câu hỏi mở đầu (cận $>1$ ở $m=200$ nên lỗi báo trên tập kiểm tra; cận không giải thích vì sao huấn luyện chọn chuẩn nhỏ). "mô hình được chọn" lệch thuật ngữ chốt "mô hình do huấn luyện chọn". Deck 06 (L06-7-03) mở bằng một câu trả lời đầy đủ và kết bằng giới hạn. | 7-03: "Độ phức tạp Rademacher của lớp chứa mô hình được chọn." / "(T1), (T3), (T5), (M): … nó chặn …"; ghi chú §10: "Khi cận lớn hơn $1$, cần báo lỗi trên một tập kiểm tra độc lập", "Mạng sâu. Cận tuyến tính không chuyển sang mạng sâu"; `thuat-ngu.md` dòng 371. | Viết lại, giữ ≤ 60 âm tiết: câu mở "Đại lượng đó là độ phức tạp Rademacher của một lớp chọn trước chứa mô hình do huấn luyện chọn, không phải số tham số." rồi ba dòng: "Với (T1), (T3), (T5), (M), độ phức tạp này chặn khoảng cách tổng quát hóa với xác suất ít nhất $1-\delta$."; "Lớp tuyến tính bị chặn theo chuẩn (lớp ẩn cố định): số hạng $2BC_x/(\gamma\sqrt m)$, không phụ thuộc $p$."; "Thí nghiệm: hai lượt khác nhau ở mô hình do huấn luyện chọn, chuẩn trung bình khác $11{,}85$ lần; cận lớn hơn $1$, lỗi báo trên tập kiểm tra." Câu về chuẩn nhỏ do quỹ đạo tối ưu giữ ở ghi chú diễn giả. |
| P3 | trung bình | L07-3-02 (và 2-10, 2-11, 3-05, 4-04, 6-01, 6-03, 6-04, 6-05) | 3-06 dẫn "khớp Ví dụ 07.4" trên mặt trang nhưng 3-02 không ghi số hiệu Ví dụ 07.4 (bài học "trang chứa ví dụ phải ghi số hiệu ấy"). Các trang ví dụ khác cũng không ghi số, trong khi ghi chú diễn giả dẫn Ví dụ 07.2 (6-06), 07.5, 07.6 (7-04), 07.10, 07.11 (7-06, 7-07): người học không tìm được trang tương ứng. Deck 06 ghi "**Ví dụ 06.k.**" ở mọi trang ví dụ. | 3-06: "$1/2-1/4=1/4$, khớp Ví dụ 07.4."; 3-02 mặt trang không có chuỗi "07.4" (kiểm bằng script). | Thêm nhãn `<strong>Ví dụ 07.k.</strong>` ở đầu dòng dữ kiện đầu tiên: 2-10 (07.2), 2-11 (07.3), 3-02 (07.4), 3-05 (07.5), 4-04 (07.6), 6-01 (07.8), 6-03 và 6-04 (07.10, ghi "Bước 1–2", "Bước 3–4" ở ghi chú diễn giả), 6-05 (07.11). Bắt buộc tối thiểu: 3-02. |
| P4 | trung bình | L07-2-07 → L07-2-08 | Mạch 2 gộp §1–§5 được chấp nhận với điều kiện "có câu nối trên mặt trang", nhưng ở ranh giới hai cụm (biểu diễn và tối ưu, 2-03…2-07; đếm tham số, 2-08…2-11) không mặt trang nào nói vì sao chuyển sang số tham số. 2-08 mở bằng "Nhắc lại:" rồi định nghĩa. Lý do (số hạng $2r$ đo năng lực thống kê; số tham số là thước đo đầu tiên cho kích thước của lớp) chỉ ở ghi chú diễn giả 2-06 và 2-08. | `review-log.md`: "Mục 11.1 mạch 2 gộp §1–§5 — chấp nhận, có câu nối trên mặt trang"; ghi chú diễn giả 2-06: "Số hạng thứ hai, khi $S$ là $r$-đại diện, đo năng lực thống kê."; ghi chú diễn giả 2-08: "số tham số là đại lượng đầu tiên để đo kích thước của lớp". | Thêm dòng mở 2-08, trước "Nhắc lại:": "Số hạng $2r$ đo năng lực thống kê; số tham số là thước đo đầu tiên cho kích thước của lớp." Đếm lại mật độ (trần 60); có thể rút "Nhắc lại:" còn "Nhận xét 03.10: $\mathcal H_{\sin}$ một tham số, $d=\infty$; lớp (iii) ba hàm." |
| P5 | trung bình | L07-3-01 | Câu nối mạch 2→3 chỉ nêu một nửa lý do của ghi chú. Ghi chú: cần đại lượng "xác định cho cả lớp hàm giá trị thực … và nhỏ đi khi lớp bị chặn theo chuẩn". Thiếu vế sau, mạch 3 kết ở 3-05 bằng $\widehat{\mathfrak R}=\tfrac12$ cho cả hai loại nhãn, giống chiều VC ở 2-11; người học không thấy trên mặt trang lý do đổi công cụ, vốn chỉ hiện ra ở mạch 5. | 3-01: "Chiều VC đếm cách gán nhãn; hàm điểm số, hàm lỗi cần đại lượng cho giá trị thực."; ghi chú, câu cuối §5. Vế "nhỏ đi khi lớp bị chặn theo chuẩn" chỉ ở ghi chú diễn giả 3-00. | Sửa thành: "Chiều VC đếm cách gán nhãn; cần đại lượng cho hàm giá trị thực, nhỏ đi khi lớp bị chặn theo chuẩn." |
| P6 | trung bình | L07-2-01 | Liên tục với Bài 06: lý do cận ổn định của Bài 06 không dùng được cho mạng (cần hàm lỗi lồi theo tham số) là nửa động cơ của bài (đoạn mở đầu ghi chú, §1) và là câu kết mặt trang của L06-7-03, nhưng deck 07 chỉ nói trong ghi chú diễn giả 1-01, 2-01. Mặt trang 2-01 ghi "không cần tính lồi" mà không đối chiếu. | 2-01: "…; (M); không cần tính lồi."; ghi chú §1: "Khác Bài 05–06, hàm lỗi có thể không lồi theo tham số"; L06-7-03: "mạng nơ-ron: hàm lỗi không lồi". | 2-01, dòng giả thiết: "…; (M); không cần tính lồi, khác Bài 05–06." Hoặc thêm vào 1-02 một dòng "Nhắc lại:" cận ổn định Bài 06 cần hàm lỗi lồi. |
| P7 | nhẹ | L07-7-02 | "Đọc thêm: Nhận xét 07.6, 07.18." Nhận xét 07.6 chưa có trên mặt trang nào (chỉ ở ghi chú diễn giả 2-11), nên mạch Tổng kết đưa ra một khối mới. | 2-11 ghi chú diễn giả: "Nhận xét 07.6 (đọc thêm, UML §20.4) …"; mặt trang 2-11 không có. | Bỏ "07.6" khỏi dòng 7-02 (giữ ở ghi chú diễn giả 7-02), hoặc thêm một dòng ngắn trên 2-11 nếu mật độ cho phép. |
| P8 | nhẹ | L07-2-02, L07-2-11, L07-6-01 | Kí hiệu $d$ (chiều VC) dùng trên mặt trang mà chưa nêu; 1-02 viết "chiều VC của $\mathcal H^p_{\mathrm{aff}}$ là $p+1$" không có $d$. | 2-02: "$d=p&gt;2m$"; 2-11: "$m\le d\le N$"; 6-01: "$d=p&gt;2m$". | 1-02: "Mệnh đề 03.9: chiều VC $d$ của $\mathcal H^p_{\mathrm{aff}}$ là $p+1$, …". |
| P9 | nhẹ | L07-3-02 | Bổ đề 07.8 đặt trên mặt trang nhưng không mặt trang sau nào dùng; vai trò trong mạch không thấy được. Chỗ dùng ngầm trên mặt trang là 6-05 (lớp $\{\tfrac12+\langle w,x\rangle\}$ cùng độ phức tạp với $\mathcal F_B$). | 6-05 dòng 3: "$\{\tfrac12+\langle w,x\rangle\}$ trong $[0,1]$, độ phức tạp $\le10^{-8}$"; Bổ đề 07.8 chỉ được dẫn ở ghi chú diễn giả 4-04, 5-03, 6-05. | Thêm "(Bổ đề 07.8)" vào dòng đó của 6-05. |
| P10 | nhẹ | L07-6-01 | Trang trả lời câu hỏi phân lớp văn bản của 2-02 nhưng mặt trang không nói như vậy; liên kết ngược chỉ có trong ghi chú diễn giả. | Ghi chú diễn giả 6-01: "đó là câu trả lời cho câu hỏi thực hành". | Dòng 3 của 6-01: "Bảo đảm cho câu hỏi phân lớp văn bản (Hệ quả 07.16): với xác suất ít nhất $0{,}95$, …". |
| P11 | nhẹ | L07-4-01 | "Trực quan." dùng "bổ đề Hoeffding" (Bổ đề 02.6); 1-02 chỉ nhắc bất đẳng thức Hoeffding (Định lý 02.7). | 4-01: "bổ đề Hoeffding chặn từng bước"; 1-02: "Bất đẳng thức hợp, Hoeffding (Định lý 02.7), Hệ quả 02.10." | 1-02: "Bất đẳng thức hợp, bổ đề Hoeffding (Bổ đề 02.6), bất đẳng thức Hoeffding (Định lý 02.7), Hệ quả 02.10." |
| P12 | nhẹ | L07-2-09 → L07-2-10 | Mặt trang 2-10 không nói ví dụ phục vụ điều gì sau 2-09. Ghi chú mở ví dụ bằng "Một hàm có thể có nhiều véc-tơ tham số với chuẩn khác nhau"; hệ quả cho lớp $\mathcal H_{J,N}(B)$ (hàm thuộc lớp hay không tùy cách tham số hóa) không hiện trên mặt trang. | 2-10 "Diễn giải: một hàm có chuẩn tham số $\sqrt{10{,}25}\approx3{,}20$ hay $\sqrt{500{,}30}\approx22{,}37$; tích chuẩn phổ không đổi." | Thêm vào "Diễn giải:" vế kết của ghi chú: "…: chuẩn tham số không xác định được từ hàm; tích chuẩn phổ không đổi." |
| P13 | nhẹ | L07-7-08 (ghi chú diễn giả) | Ghi chú diễn giả bỏ câu §12 nối Bài 06 với câu hỏi Bài 08 ("Bài 06 chặn khoảng cách tổng quát hóa qua tính ổn định đều, một tính chất của thuật toán chứ không của lớp"), là mắt nối 06 → 07 → 08. | Ghi chú §12, đoạn cuối. | Thêm câu đó trước câu "Bài 08 hỏi: …". |

Số phát hiện: 0 chặn bàn giao, 1 nghiêm trọng, 5 trung bình, 7 nhẹ. Mọi đề xuất thêm chữ phải được người biên tập đếm lại mật độ (trần 60, mục tiêu ≤ 40) và chạy lại `footer_check.py`.

## 5. Đề xuất sửa ghi chú

- Phần "Kiến thức tiên quyết" không có Định lý 02.14 và (T4), trong khi Bài tập 07.4(b) dùng cả hai. Đề xuất này đã có trong `review-log.md` (mục "Bộ trang chiếu"); nhắc lại vì nó cũng là gốc của P1.
- Không có đề xuất mới về thứ tự mục: thứ tự §1–§13 cho được một mạch trang liên tục.

## 6. Kết luận

**đạt khi sửa.** Mạch truyện theo đúng thứ tự mục của ghi chú. Liên kết `#/N`, viewer và dòng bài sau đúng. Bảng `Mục | Bài tập` khớp `exercises.md`. Cần sửa P1 (nhắc lại Định lý 02.14 và (T4) trước bài tập tổng hợp) và các điểm trung bình P2–P6 trước khi bàn giao.
