# Kiểm lại sau biên tập — deck Bài 05, lượt 2 (2026-11-15)

Vai: kiểm lại sau biên tập (chỉ đọc). Đầu vào: deck hiện tại `2627-1/lecture-05-ha-gradient-ngau-nhien.html`; `reviews/deck-kiem-lai-1.md` (12 mục nhẹ); `storyboard.md` mục 17, bảng "Lượt 2", và mục 16 (ngoại lệ 3-01); ghi chú `materials/lec-05/lecture-note.md`. `no-ai-slop` chế độ Detect trên câu mới.

**Kết luận: đạt.** Còn mở 2 phát hiện, đều nhẹ: 0 chặn bàn giao, 0 nghiêm trọng, 0 trung bình.

## 1. Cách kiểm

- So từng trang với bản đóng băng: vẫn 55 trang, cùng ID. Các trang đổi ở lượt 2 đúng với bảng "Lượt 2": 1-01, 1-06, 4-02, 4-03, 4-05, 4-09, 6-01, 6-02, 6-03, 6-04, 7-01, 7-03, cùng ghi chú diễn giả 7-00 và 7-03 (thêm "cho"). Không thấy trang nào đổi ngoài bảng.
- `deck_lint.py`: 1 phát hiện, `L05-7-04 | SYLL60 | 68 > 60` (ngoại lệ đã chấp nhận).
- `footer_check.py`: 0 trang.
- `deck_check.py --shots` trên 12 trang đổi (báo cáo cho cả 55 trang): console 0, pageerrors 0, failed 0, `.katex-error` 0. Mọi OVERFLOW đều là `path` SVG (đuôi `\sqrt`). Không trang nào có `docScrollW > 390`. Mật độ không đổi so với lượt 1 (7-02 có 75 âm tiết, 7-04 có 66).
- Đã xem ảnh 1600×900 và 390×844 (cả ảnh `-end`) của các trang đổi; tờ ghép ở `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-05/recheck2/sheets/`.

## 2. Mười hai mục của lượt 1

| # | Trang | Trạng thái | Bằng chứng |
|---|---|---|---|
| 1 | 1-01 | đã sửa | "…, hạ gradient ngẫu nhiên có chiếu có cận của độ chênh tối ưu kì vọng tại điểm lặp trung bình tỉ lệ nghịch với căn bậc hai của số vòng lặp." Thuật toán làm chủ ngữ; vẫn một câu, có điều kiện. |
| 2 | 1-06 | đã sửa, còn nhẹ #A | Số đúng: $0{,}0710$, $0{,}1021$, $0{,}0694$ đều $>0{,}0639$ (ba lựa chọn $i_3=1,2,3$ tại $w_3$, trung bình $0{,}0808$); bước GD cho $0{,}0614<0{,}0639$. Hai bước đầu ($\tfrac23\to0{,}4533\to0{,}0639$) không còn bị bao trong "mọi". Câu chữ còn thiếu tân ngữ (xem #A). |
| 3 | 4-03 (ghi chú diễn giả) | đã sửa | "Phần tiến của bước $t$ là $(\Delta_t-\Delta_{t+1})/(2\eta)$ …; theo kì vọng, nó ít nhất $F(w_t)-F(u)-\eta G^2/2$, và tổng các phần tiến không quá $\Delta_1/(2\eta)$." Kiểm lại: lấy kì vọng bất đẳng thức một bước và dùng Bổ đề 05.12(c), (G1), (G2) được $\mathbb E[(\Delta_t-\Delta_{t+1})/(2\eta)]\ge\mathbb E[F(w_t)-F(u)]-\eta G^2/2$. Tổng triệt tiêu bằng $(\Delta_1-\Delta_{T+1})/(2\eta)\le\Delta_1/(2\eta)$. Đúng. |
| 4 | 4-03, 7-00, 7-03 | đã sửa | "hàm mà oracle không chệch cho" xuất hiện 7 lần (mặt trang 4-03, ghi chú 4-03, 7-00, 7-03); không còn chỗ nào thiếu "cho". |
| 5 | 4-05 | đã sửa | "với SGD, lấy kì vọng: $\mathbb EF(\bar w_T)-F(u)\le\frac1T\sum_t\mathbb Ec_t$". Đúng: bất đẳng thức lồi hữu hạn trên từng quỹ đạo cho $\mathbb EF(\bar w_T)-F(u)\le\frac1T\sum_t\mathbb E[F(w_t)-F(u)]$, và $\mathbb E[F(w_t)-F(u)]\le\mathbb Ec_t$ theo Bổ đề 05.12(c) cùng (G1). |
| 6 | 4-09 | đã sửa | "Với GD, oracle tất định $g_t=v(w_t)$: (G2) thành $\lVert v\rVert\le G$." Trích Mệnh đề 05.5 đã chuyển xuống ghi chú diễn giả, đặt đúng chỗ ("khi $F$ là $G$-Lipschitz"). Dòng Hệ quả 05.16 giữ "$v(w)\in\partial F(w)$". |
| 7 | 6-01, 6-02 | đã sửa, còn nhẹ #B | 6-01 viết "$F=L_s$, … $s$ cố định", khớp ghi chú. 6-02 "Trực quan." chỉ giữ ý mới, không còn lặp 6-01. |
| 8 | 6-02 | đã sửa | "$\delta'\in(0,1)$" không còn "theo $\xi$"; $\Pr_\xi$ trên công thức và ghi chú diễn giả "Xác suất thất bại $\delta'$ lấy theo $\xi$, khác $\delta$ theo $S$" khớp ghi chú dòng 1069. |
| 9 | 6-03 | đã sửa | "SGD đạt mức (O2) với xác suất $\ge1-\delta'$: khi $\delta'=0{,}05$, khoảng 95/100 lần chạy độc lập trên cùng $s$ cho $\operatorname{opt}_s<\epsilon_{\mathrm{opt}}$." Xem nhận xét về nghĩa xác suất ở mục 3. |
| 10 | 6-04 | đã sửa | "Nhắc lại:" đứng trước "Mệnh đề 05.20."; mọi kí hiệu trong dòng ($\varphi$, $\psi$, $\xi^{(j)}$) đã có ở 3-03 và dòng đầu 6-04. |
| 11 | 7-03 | đã sửa | "Cận chặn $\operatorname{opt}_S\approx0{,}0025$; sai số ước lượng vẫn $\approx0{,}9025$." Hai số khớp 7-01. |
| 12 | 4-02, 4-09, 7-01 (390 px) | đã sửa | Ảnh `-end`: "$1{,}5019.$", "$10^4,$ $\eta=0{,}05.$" không còn dấu câu đứng đầu dòng. Ở 7-01, KaTeX ngắt dòng sau dấu "=" nên "$1.$" xuống dòng cùng số, không còn dấu câu đứng riêng. |

Ngoại lệ 3-01 (dòng 27 âm tiết) đã ghi ở storyboard mục 16, dòng 1027.

## 3. Toán và nghĩa xác suất ở 6-03

Câu "khoảng 95/100 lần chạy độc lập trên cùng $s$" đúng nghĩa xác suất theo $\xi$. Tập $s$ cố định, mỗi lần chạy dùng một dãy $\xi=(\xi_1,\ldots,\xi_{T-1})$ mới và độc lập. Hệ quả 05.19(b) cho mỗi lần chạy $\Pr_\xi[\operatorname{opt}_s(\bar w_T)<\epsilon_{\mathrm{opt}}]\ge1-\delta'=0{,}95$, nên số lần thành công trong 100 lần chạy có kì vọng ít nhất 95. Bảo đảm là cận dưới, nên tỉ lệ thật có thể cao hơn; cách đọc chặt là "ít nhất khoảng 95". Câu trên deck giữ đúng chữ của ghi chú ("có khoảng 95 lần", câu sau $\square$ của Hệ quả 05.19) và đúng mẫu tác giả nêu trong `../CLAUDE.md` § The author's voice ("trong 100 lần huấn luyện, có khoảng 95 lần …"). Vì vậy tôi không ghi đây là phát hiện. Nếu tác giả muốn đổi thành "ít nhất khoảng 95" thì đổi cùng lúc ở ghi chú và deck.

Các phần toán khác trên trang đổi đã kiểm ở mục 2 (#2, #3, #5) và đều khớp. Số trên 4-02, 4-09, 7-01, 7-03 không đổi so với lượt 1, chỉ đổi dấu câu hoặc câu chữ.

## 4. Mạch truyện (trang đổi ±2)

- 1-05 → 1-06 → 2-00: câu hỏi mở đầu vẫn nối với số $10^6$ và với ví dụ ba quan sát.
- 4-02 → 4-03 → 4-04 → 4-05 → 4-06: không đổi thứ tự. Kết luận theo kì vọng ở 4-05 khớp bước 5 của 4-04.
- 4-08 → 4-09 → 4-10: liền mạch.
- 6-00 → 6-01 → 6-02 → 6-03 → 6-04 → 6-05: 6-01 nêu đầu ra ngẫu nhiên khi $s$ cố định; 6-02 nêu phạm vi của bảo đảm; 6-03 nêu ý nghĩa thao tác; 6-04 nhắc lại kỹ thuật trước mệnh đề. Không còn lặp ý.
- 7-00 → 7-01 → 7-02 → 7-03 → 7-04: số $0{,}0025$ và $0{,}9025$ của 7-01 được dùng lại ở 7-03.

## 5. Phát hiện còn mở

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | 1-06 (#A) | Câu mới thiếu tân ngữ của "làm tăng" và không nói "sau" là sau điểm nào; câu hỏi dùng dấu phẩy nối hai mệnh đề, thiếu liên từ | "Ba quan sát, $L_S=0{,}0639$: mọi lựa chọn của bước SGD sau làm tăng ($0{,}0710$; …), GD giảm ($0{,}0614$)."; "SGD bảo đảm gì cho $L_S$ sau $T$ bước, cần bao nhiêu bước?" | "Ba quan sát, tại điểm có $L_S=0{,}0639$: mọi lựa chọn của bước SGD tiếp theo làm $L_S$ tăng (…), bước GD làm giảm ($0{,}0614$)."; "… sau $T$ bước, và cần bao nhiêu bước?" (đếm lại âm tiết, trần 60) |
| nhẹ | 6-02 (#B) | "Trực quan." là câu không chủ ngữ, ghép ba mảnh; author's voice yêu cầu chủ ngữ trực tiếp | "Bảo đảm cho một thuật toán, trên $s$ cố định; chặn $\operatorname{opt}_s$, không chặn $L_D$." | "Hệ quả 05.19 bảo đảm cho một thuật toán trên $s$ cố định: nó chặn $\operatorname{opt}_s$, không chặn $L_D$." |

Văn phong (Detect) trên các câu mới khác (1-01, 4-05, 4-09, 6-01, 6-03, 6-04, 7-03, ghi chú 4-03): không thấy mẫu nào trong danh sách `no-ai-slop`, không câu rào đón, không nhãn ngoài danh sách. Ghi chú diễn giả mới không có ID trang hay câu quy trình.

## 6. Đề xuất sửa ghi chú

Không có đề xuất mới. Nếu tác giả muốn cách đọc chặt cho câu "khoảng 95 lần" thì đổi ở ghi chú trước (xem mục 3).
