# Kiểm lại sau biên tập deck Bài 06 — lượt 1 (chỉ đọc)

Vai: kiểm lại sau biên tập (general-purpose, Opus 5.5). Ngày 2026-11-16. Không sửa tệp nào ngoài báo cáo này.

Đầu vào: deck sau sửa `2627-1/lecture-06-on-dinh-chinh-quy-hoa.html`, `img/lec-06/`; bản đóng băng (thư mục nháp `lec-06/master/frozen/`); năm báo cáo `reviews/deck-*.md`; `review-log.md` § "Năm báo cáo duyệt và quyết định của điều phối viên"; `storyboard.md` mục 15–17; `materials/lec-06/lecture-note.md`, `exercises.md`. `no-ai-slop` chế độ Detect đã nạp.

## 0. Kiểm máy (chạy lại, thư mục nháp `lec-06/recheck/`)

| Công cụ | Kết quả |
|---|---|
| diff theo trang (`recheck/diff.txt`) | 40/55 trang đổi (mặt trang hoặc ghi chú diễn giả); SVG đổi: `danh-doi-khop-on-dinh.svg` (hai nhãn) |
| `deck_lint.py` | **1 phát hiện**: `L06-2-08 \| LINES6 \| 7 dòng > 6`. Mục 17 storyboard ghi "`deck_lint.py` 0" là sai; `review-log.md` có ghi 2-08 bảy dòng |
| `footer_check.py` | 0 trang chạm chân trang |
| `deck_check.py --shots` | slides=55, console 0, pageerrors 0, failed 0, `.katex-error` 0; OVERFLOW chỉ ở các trang có `\sqrt` (báo động giả đã biết); SYLL ở 1-01 (bìa) và 7-02 (65, trần 80 của bảng tổng kết) |
| Mật độ (script đếm của người viết) | trung vị 42 trang nội dung: bản đóng băng 49, bản sau sửa **56**; 8 trang 59–60 (2-01, 2-02, 2-03, 2-12, 4-05, 4-07, 5-02, 6-05) |
| Dòng > 20 âm tiết mới sinh do sửa | 1-02 (23), 2-08 (27), 2-11 (35), 3-03 (33), 4-04 (27), 5-02 (24) |

Ảnh đã xem (1600×900 và 390×844, cả `-end`) của 1-02, 2-01, 2-08, 2-09, 2-11, 3-03, 3-04, 4-02, 4-03, 4-04, 5-01, 5-02, 6-04, 6-05, 7-01, 7-02, 7-03: tấm ghép `recheck/sheet-w-*.png`, `recheck/sheet-n-*.png`. Không trang nào tràn khung hay chồng chữ; ở 390 px công thức hiển thị của 2-08, 2-09, 4-03, 5-02 và bảng 2-11, 3-04 cuộn ngang tại chỗ (đúng quyết định điều phối viên); 7-01, 7-02 ở 390 px xuống dòng trong ô, đọc được.

## 1. Đối chiếu phát hiện được chấp nhận

Mọi dòng trong bảng mục 17 của storyboard đã đối chiếu với diff. Trạng thái tóm tắt; chỉ ghi chi tiết các dòng không phải "đã sửa".

| Báo cáo | Tổng phát hiện | Đã sửa | Sửa chưa đủ | Chưa sửa (có lý do được chấp nhận) |
|---|---:|---:|---:|---:|
| học viên | 20 | 15 | 3 | 2 |
| toán học | 13 | 12 | 1 | 0 |
| chuyên gia | 13 | 13 | 0 | 0 |
| sư phạm | 27 | 25 | 2 | 0 |
| mạch truyện | 13 | 12 | 0 | 1 |

| Phát hiện | Trạng thái | Bằng chứng / đánh giá |
|---|---|---|
| học viên · mật độ sát trần | sửa chưa đủ | 1-06 (60→57), 3-03 (60→53), 6-05 (60→59) giảm; trung vị tăng 49→56 vì các dòng thêm theo yêu cầu khác. Đề xuất cắt cụ thể ở mục 4 |
| học viên · dòng > 20 âm tiết | sửa chưa đủ | 3-02, 6-05, 4-02 đã hết; sáu dòng dài mới (mục 0). Đề xuất ở mục 4 |
| học viên · công thức bị cắt ở 390 px | chưa sửa, chấp nhận | quyết định điều phối viên (cuộn tại chỗ); 4-03 đã rút bằng $\tilde w$ |
| học viên · chữ SVG nhỏ ở 390 px | chưa sửa, chấp nhận | số trên hình có trong chữ/bảng (6-04: "$\lambda^*=0{,}2$, cận $0{,}2$"; 3-04: bảng và "Diễn giải:") |
| học viên · bảng ở 390 px (3-04 bỏ cột) | đã sửa, nhưng sinh xung đột thuật ngữ ở 2-11 | xem K8 |
| toán học · 7-03 dòng rút gọn thiếu giả thiết | sửa chưa đủ | dòng quan sát mới bỏ (giả thiết sang ghi chú diễn giả, chấp nhận); dòng chính quy hóa sửa phần "không âm", "$\lambda^*$ chọn trước" nhưng bỏ mất lớp so sánh $W_B$ và (T1): xem K1 |
| sư phạm · 4-01 mảnh câu | sửa chưa đủ (chấp nhận) | "Với mọi $s\in\mathcal Z^m$, kể cả $s$ có xác suất $0$; …": có giới từ mở đầu, đọc được; lý do trần 60 hợp lệ |
| sư phạm · 7-03 cấu trúc, "Tối ưu là học" cụt | sửa chưa đủ | câu dẫn đã là đoạn, "gradient ngẫu nhiên" đủ tên; câu dẫn kết bằng ":" nhưng ba mục sau không cùng loại (số của ví dụ, một kết quả, một giới hạn): xem K1 |
| mạch truyện · M1 câu hỏi §5 | đã sửa | "Câu hỏi:" trên 2-08; câu trả lời ở ghi chú diễn giả 2-08 và "Trực quan." 2-09 trên mặt trang (trang liền sau) — đạt |
| mạch truyện · M4 7-03 | đã sửa (phần mặt trang) | có $0{,}0006$/$0{,}2261$, giới hạn SGD nhiều vòng; câu ghi chú diễn giả mới sai số học: xem K2 |
| mạch truyện · N6 liên kết deck 05 | chưa sửa, chấp nhận | ngoài phạm vi ghi, việc của bước xuất bản |
| Quyết định riêng của điều phối viên (tính lồi chỉ ở Hệ quả 06.2, Mệnh đề 06.11; cơ chế bỏ $\lambda>0$; nhãn "Mục tiêu:", "Cấp thuật toán:"; số Ví dụ 06.2, 06.3; Bổ đề 06.8(a)(b)(c); $0{,}3810$ hai nghĩa; câu nối 2→3, 4→5; "Nhắc lại:" Bài 05 và ba kỹ thuật) | đã sửa | 7-03 dòng cuối, ghi chú diễn giả 4-03, 7-03; 5-02 ghi chú diễn giả; 2-01 "Cần chặn …", 4-03 "Bảo đảm cấp thuật toán: …"; 2-06, 2-11; 3-03; 5-03; 3-01, 5-01; 1-02, 2-03, 4-04, 4-05 |

**Lệch mới do người sửa tự đề xuất.**

- *Bảng tổng kết 2 + 3 hàng (7-01/7-02):* đạt. Thứ tự hàng theo thứ tự mục ghi chú (§4, §5 | §7, §8, §9); 7-01 có thêm $\eta$, $u\in W$; 7-02 65 âm tiết (trần 80); `footer_check` 0. Ghi chú diễn giả chuyển đúng câu "Bỏ dạng đầy đủ của (T1)" sang 7-02 cùng hàng Định lý 06.10.
- *3-04 bỏ cột $\hat w_{S^{(4)}}$:* đạt về toán (ghi chú diễn giả: "bằng một phần năm $\hat w_S$: $0{,}1538$; $0{,}0952$; $0{,}0444$", đúng vì $0{,}5/2{,}5=1/5$; 5-05 có số $\lambda=2$). Bảng vẫn cuộn ở 390 px, nhưng "Diễn giải:" chứa đủ số. Hệ quả phụ: K8.
- *3-03 "Trực quan." chuyển vào ghi chú diễn giả:* chấp nhận. Bổ đề 06.7, 06.8 là công cụ của Mệnh đề 06.11 (ghi chú diễn giả 7-02); cơ chế độ cong được nhìn thấy ngay ở trang sau (Hình 06.1 và "Diễn giải:" 3-04: khoảng cách $0{,}6154\to0{,}1778$) và được nêu bằng lời ở "Trực quan." 5-01 ("độ cong $\lambda$ giữ điểm cực tiểu dịch cỡ $(2G/m)/\lambda$") trước kết quả chính. Hành trình khái niệm của kết quả chính (Mệnh đề 06.11) vẫn đủ. Mặt trang 3-03 còn thuần phát biểu; không cần thêm chữ (mật độ). Một lỗi nhỏ ở cách viết Bổ đề 06.8: K13.

## 2. Toán trên nội dung đã đổi (tính lại)

| Nội dung | Kết quả |
|---|---|
| 2-01 (T1) dạng đầy đủ/dạng yếu | khớp ghi chú §2 dòng 150 nguyên nghĩa; "Chế độ A … theo (T1)" mặc định dạng đầy đủ như ghi chú dòng 103 |
| 2-02 $G=2(BC_x+C_y)C_x=2(1+1)\cdot1=4$ | đúng |
| 3-01 $\sum x_iy_i$: $1+0+0{,}5+1=2{,}5\to1+0+0{,}5-1=0{,}5$; $0{,}5/3{,}25=0{,}1538$; dịch $0{,}6154$, $0{,}6154/2=0{,}308$ | số đúng; cách viết sai: K3 |
| 3-04 $\lambda=1$: $2{,}5/5{,}25=0{,}4762$, $0{,}0952$, hiệu $0{,}3810$; $L_S=(3{,}25\cdot0{,}2268-2{,}381+3)/4=0{,}3390$; $\lambda=4$: $0{,}2222$, $0{,}1778$, $L_S=0{,}5123$ | đúng |
| 4-01 $\hat w=10/13$, $2/13$; $(23/13)^2-(15/13)^2=304/169=1{,}7988$; ghi chú diễn giả "từ $(23/13)^2$ xuống $(15/13)^2$" | đúng |
| 4-03 bảo đảm với $\tilde w=A(S;\xi)$ | đúng, khớp Định lý 06.10; "không dùng kích thước của lớp giả thuyết" khớp câu sau $\square$ của ghi chú |
| 4-04 bước 3 "khoảng cách bằng $\tfrac1m\sum_i\mathbb E[\ell(A(S^{(i)};\xi),Z_i)-\ell(A(S;\xi),Z_i)]$" | đúng (bước 1, 2 lấy trung bình theo $i$ rồi trừ bước 3), đứng sau định lý nên không trái N2 |
| 4-07 (b1) $\mathbb EL_D=(\tfrac12+\tfrac14+\tfrac14+\tfrac12)/4=0{,}375$, $\mathbb EL_S=0{,}125$; (b2) $(2-\tfrac12)/2=0{,}75$ | đúng |
| 5-01 dòng nối $0{,}6154\to0{,}1778$ | đúng |
| 5-02 ghi chú diễn giả: độ cong $\mu=2/m$ cho $\mu\lVert\hat w-\hat w'\rVert^2\le\tfrac{2G}m\lVert\hat w-\hat w'\rVert$, nên $\lVert\hat w-\hat w'\rVert\le G$ | đúng, khớp Ví dụ 06.7 Bước 3; tên "độ dịch $2G/m$" không chuẩn: K9 |
| 5-03 $\lambda\lVert\cdot\rVert^2=64/441=0{,}1451$; $\tfrac14(240+432)/441=168/441=8/21=0{,}3810$; $2\cdot4\cdot(8/21)/4=16/21=0{,}7619$; $240/441=(19/21)^2-(11/21)^2$, $432/441=(31/21)^2-(23/21)^2$ | đúng |
| 6-05 $2\cdot4/(0{,}1\sqrt m)\le0{,}05\Rightarrow m\ge2\,560\,000=400\cdot6400$; Markov với $\alpha$ | đúng |
| 7-01/7-02 các hàng | đúng, khớp phát biểu ghi chú |
| 7-03 mặt trang | dòng chính quy hóa thiếu $W_B$, (T1): K1 |
| 7-03 ghi chú diễn giả | "Phần chênh $0{,}2261$ … là khoảng cách $0{,}4750$" sai số học: K2 |
| F2 (`danh-doi-khop-on-dinh.svg`) | nhãn "tổng" tại $x=456$ (khoảng $\lambda\approx0{,}35$), nơi hai đường cách nhau rõ; nhãn đáy "λ* = 0,2, tổng 0,2" khớp alt; đạt |

## 3. Mạch truyện trên trang đổi ±2 và ranh giới mạch

- 1-06 → 2-00 → 2-01: dòng dẫn 2-00 bỏ "lưu lại" (K12); còn lại liền mạch.
- 2-07 → 2-08 → 2-09: 2-07 kết bằng $L_S'(w_t)$ khác $L_D'(w_t)$; 2-08 "Câu hỏi:" nối đúng; 2-09 "Trực quan." trả lời câu hỏi trên mặt trang. Đạt.
- 2-11 → 2-12 → 3-00 → 3-01: "cần cận theo tính chất thuật toán, không qua hội tụ đều" → 3-01 "nghiệm đổi bao nhiêu khi thay một quan sát" (M2). Đạt; cách nói K15.
- 4-07 → 5-00 → 5-01: câu nối "Định lý 06.10 cần hệ số ổn định nhỏ; Ví dụ 06.4: …" (M3). Đạt.
- 4-03 → 4-04 → 4-05: tiêu đề 4-04 "Ý tưởng chứng minh: Định lý 06.10"; công thức trung bình thay một xuất hiện ở bước 3 rồi được đặt tên ở 4-05. Đạt. Mặt trang 4-04 gọi bước 4 là "lấy điều kiện rồi bỏ điều kiện (Bài 04)", ghi chú diễn giả gọi là "định lý Fubini": không mâu thuẫn (cùng một bước khi $\xi$ độc lập), K16 gợi ý một câu nối.
- 6-06 → 7-00 → 7-01 → 7-02 → 7-03 → 7-04: thứ tự hàng theo ghi chú; 7-03 khép câu hỏi 1-05 và ví dụ 1-06 ($0{,}0006$/$0{,}2261$). Đạt, trừ K1, K2, K6.
- Định nghĩa trước khi dùng: (C), (G1), (G2), $\varphi$, $\bar w_T$, SGD, Thuật toán 05.11 (1-02) trước 1-06, 2-04, 2-05; lồi mạnh (3-03) trước Bổ đề 06.7; $G=2(BC_x+C_y)C_x$ (2-02) trước 5-01; (T1) (2-01) trước 2-05, 2-09, 4-03. Đạt.

## 4. Mật độ: đề xuất cắt cụ thể

Đếm theo quy ước `deck_lint.py` (KaTeX không tính). Mục tiêu: mọi trang ≤ 57, 2-08 ≤ 6 dòng.

| Trang | Hiện | Đề xuất | Ước sau |
|---|---:|---|---:|
| 2-08 | 56, 7 dòng | Chuyển ví dụ "$0$ với $h$ cố định" vào ghi chú diễn giả (đã có ý này ở ghi chú diễn giả 2-09, 4-02); hai ví dụ còn lại một đoạn: "**Ví dụ.** $1$ với thuật toán ghi nhớ (memorizing algorithm) $A_{\mathrm{gn}}$ (Ví dụ 01.8); $0{,}5=1{,}25-0{,}75$ với $A(S)=\bar Y$, $Y_i=\pm1$, $m=4$, $\ell(w,y)=(w-y)^2$." (hai mục song song, không cần danh sách) | 52, 4 dòng |
| 2-02 | 60 | Câu hỏi: "**Câu hỏi:** bảo đảm nào cho $\mathbb EL_D(\bar w_T)-\inf_{\lVert w\rVert\le5}L_D$ khi SGD đi đúng một vòng qua $10^6$ hồ sơ?" | 52 |
| 2-01 | 59 | "(T1) dạng đầy đủ: độc lập cùng phân bố $D$; dạng yếu: mỗi $Z_i\sim D$." | 56 |
| 2-03 | 59 | "**Trực quan.** $w_t$ chưa thấy $Z_t$, và $Z_t\sim D$ khi biết $\mathcal F_{t-1}$: dưới gradient trên $Z_t$ có trung bình là dưới gradient của $L_D$ tại $w_t$." | 54 |
| 2-12 | 59 | Dòng đề: "**Bài tập 06.1.** Thiết lập của Ví dụ 06.2 với $\eta\in(0,\tfrac12)$; $Y_j$ là nhãn của $Z_j$, $\bar Y=\tfrac1m\sum_jY_j$." (giữ nguyên câu hỏi (c), (d) theo `exercises.md` dòng 35) | 52 |
| 4-05 | 60 | Bỏ "(Định lý 06.10)" ở dòng "Dùng khi …" (định lý vừa chứng minh ở 4-04; ghi chú diễn giả đã nói) | 57 |
| 4-07 | 60 | (b2): "… so với cận Lipschitz $2/m$." (ý "từ tính $2$-Lipschitz của $\ell(\cdot,z)$" vào ghi chú diễn giả) | 55 |
| 5-02 | 60, dòng 24 | "**Kỹ thuật.** Cộng hai bất đẳng thức tăng trưởng bậc hai đối xứng; lập luận một phía cho hằng số $4G/(\lambda m)$." | 57 |
| 6-05 | 59 | "**Nhận xét 06.14.** Các cận của Bài 06: kì vọng, một thuật toán; Bài 02–04: xác suất ít nhất $1-\delta$, cả lớp." | 56 |
| 2-11 | 54, dòng 35 | Tách "Diễn giải:" thành hai đoạn: "**Diễn giải:** rủi ro vượt mức kì vọng $0{,}2261>RG/\sqrt T=0{,}1$ dù $\mathbb E\operatorname{opt}_S\approx0{,}0011$." / "Phần lớn vế phải của (b) là khoảng cách tổng quát hóa kì vọng $0{,}4750$, cần cận theo tính chất thuật toán, không qua hội tụ đều." (6 dòng) | 52 |
| 3-03 | 53, dòng 33 | Tách Bổ đề 06.8 lại thành hai đoạn "Giả thiết:" / "Bảo đảm:" (5 dòng) | 53 |

## 5. Phát hiện còn mở

Định dạng: `mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa`.

| Mã | Mức độ | Trang chiếu | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|---|
| K1 | trung bình | L06-7-03 | Dòng chính quy hóa bỏ lớp so sánh và (T1): "rủi ro vượt mức kì vọng" trong deck là so với $W$ (2-04), còn Hệ quả 06.13(c) chặn so với $W_B$; khi $W\supsetneq W_B$ khẳng định sai. Dòng "mở đầu:" không nêu đại lượng (bài học deck 02). Câu dẫn kết ":" nhưng ba mục không cùng loại. | "chính quy hóa, $\ell$ lồi, không âm, (L), $\lambda^*$ chọn trước: rủi ro vượt mức kì vọng $\le2GB/\sqrt m$;" — ghi chú Hệ quả 06.13(c): "$\mathbb E_SL_D(\hat w_S)-\inf_{W_B}L_D\le2GB/\sqrt m$"; 7-02 hàng Hệ quả 06.13 viết đúng | Viết lại (≈ 58 âm tiết): đoạn "Tối ưu là học khi gradient ngẫu nhiên không chệch cho $L_D$, hoặc khi khoảng cách tổng quát hóa kì vọng và $\mathbb E\operatorname{opt}_S$ cùng nhỏ." rồi danh sách: "$\mathbb EL_D(\bar w_T)-1$: $0{,}0006$ với quan sát mới, $0{,}2261$ khi dùng lại $S$;" / "ERM có chính quy hóa, $\ell$ lồi, không âm, (L), (T1), $\lambda^*$ chọn trước: $\mathbb E_SL_D(\hat w_S)-\inf_{W_B}L_D\le2GB/\sqrt m$;" / dòng K6 |
| K2 | trung bình | L06-7-03 (ghi chú diễn giả) | Câu đồng nhất hai số khác nhau ($0{,}2261\ne0{,}4750$); cùng lỗi "phần chênh" sư phạm đã bắt ở 2-11. | "Phần chênh $0{,}2261$ của ví dụ mở đầu là khoảng cách $0{,}4750$, và chạy thêm vòng không làm nó giảm." — ghi chú diễn giả 2-11: "$0{,}4750-0{,}2489=0{,}2261$" | "Ở ví dụ mở đầu, $\mathbb E\operatorname{opt}_S\approx0{,}0011$, còn khoảng cách tổng quát hóa kì vọng bằng $0{,}4750$; chạy thêm vòng không làm nó giảm." |
| K3 | trung bình | L06-3-01 | Lỗi mới do gộp dòng: KaTeX đọc thành "$0{,}6154\approx0{,}31$". | "dịch $0{,}6154\approx0{,}31$ lần đường kính $2$ của $W$" (bản đóng băng: "dịch $0{,}6154$, khoảng $0{,}31$ lần đường kính") | "dịch $0{,}6154$, khoảng $0{,}31$ lần đường kính $2$ của $W$" |
| K4 | trung bình | L06-2-08 | 7 dòng nội dung (trần 6); `deck_lint.py` báo 1, không phải 0 như mục 17 storyboard. | `L06-2-08 \| LINES6 \| 7 dòng > 6` | Theo mục 4 (bỏ ví dụ $h$ cố định khỏi mặt trang, hai ví dụ một đoạn) |
| K5 | trung bình | toàn deck | Trung vị mật độ 56 (đóng băng 49), 8 trang 59–60, 6 dòng > 20 âm tiết mới. | mục 0 | Áp dụng các cắt ở mục 4; sửa mục 15, 17 storyboard theo số đo lại |
| K6 | nhẹ | L06-7-03 | "(không lồi)" gắn cho cả "SGD nhiều vòng", trong khi ví dụ SGD nhiều vòng của bài có hàm lỗi lồi; "riêng" mơ hồ. | "SGD nhiều vòng, mạng nơ-ron (không lồi): cần hệ số ổn định riêng." — ghi chú §10: "Định lý 06.10 cần một hệ số ổn định cho chính SGD"; §12: "Với mạng nơ-ron, hàm lỗi … không lồi, nên Mệnh đề 06.11 không áp dụng" | "SGD nhiều vòng: cần hệ số ổn định của chính SGD; mạng nơ-ron: hàm lỗi không lồi." |
| K7 | nhẹ | L06-7-03 (ghi chú diễn giả) | Điều kiện của cận gắn vào "không chệch": tính không chệch cần Bổ đề 06.1, còn $G$, $R$, $\eta$ là điều kiện của cận $RG/\sqrt T$. | "khi đó gradient ngẫu nhiên không chệch cho rủi ro kì vọng (cần $\ell$ lồi, cận mô-men $G$, $\lVert w_1-u\rVert\le R$, $\eta=R/(G\sqrt T)$)" | "…không chệch cho rủi ro kì vọng; cận $RG/\sqrt T$ cần thêm cận mô-men $G$, $\lVert w_1-u\rVert\le R$ với mọi $u\in W$ và $\eta=R/(G\sqrt T)$." |
| K8 | nhẹ | L06-2-11, L06-3-04, L06-5-03 | "khoảng cách" hai nghĩa trong hai bảng liên tiếp mạch: khoảng cách tổng quát hóa kì vọng (2-11) và khoảng cách giữa hai nghiệm (3-04, 5-03). Lỗi mới do rút tiêu đề cột 2-11. | 2-11 cột "khoảng cách" = $0{,}4750$; 3-04 cột "khoảng cách" = $\lvert\hat w_S-\hat w_{S^{(4)}}\rvert$ | 2-11: tiêu đề cột $\mathbb E[L_D-L_S]$ (KaTeX, hẹp, không tính âm tiết) |
| K9 | nhẹ | L06-5-02 (ghi chú diễn giả) | $2G/m$ là hằng số Lipschitz của hiệu hai mục tiêu (5-01 "Trực quan."), không phải "độ dịch"; độ dịch là $(2G/m)/\lambda$. | "cùng bậc với độ dịch $2G/m$" | "cùng bậc với hằng số Lipschitz $2G/m$ của hiệu hai mục tiêu" |
| K10 | nhẹ | L06-4-03 (ghi chú diễn giả) | Nói quá: định lý còn cần (T1) dạng đầy đủ, $\xi$ độc lập, (T2), khả tích (chính câu cuối ghi chú diễn giả nêu). | "chỉ cần tính ổn định đều." | "điều kiện trên thuật toán chỉ là tính ổn định đều." |
| K11 | nhẹ | L06-2-01 | (T2) và tính lồi viết chung một dòng sau nhãn "(T2):", đọc như lồi thuộc (T2); ghi chú tách "Hàm lỗi lồi". | "(T2): $\ell\ge0$, $\ell(w,\cdot)$ đo được, $L_D<\infty$ trên $W$; $\ell(w,z)$ lồi theo $w$." | "(T2): …; hàm lỗi lồi: $\ell(\cdot,z)$ lồi." |
| K12 | nhẹ | L06-6-00, L06-2-00 (dòng dẫn) | 6-00 rút tên thuật ngữ ("cân khớp với ổn định"); 2-00 bỏ "lưu lại", tên của chế độ B (quyết định L6). | 6-00: "Hệ số chính quy hóa cân khớp với ổn định và xác định cỡ mẫu đủ cho một mức rủi ro vượt mức kì vọng."; 2-00: "… trên tập huấn luyện không chệch cho rủi ro thực nghiệm." | 6-00 (25 âm tiết): "Hệ số chính quy hóa cân độ khớp với tính ổn định và xác định cỡ mẫu cho mức rủi ro vượt mức kì vọng."; 2-00: "… trên tập huấn luyện lưu lại không chệch cho rủi ro thực nghiệm." (25) |
| K13 | nhẹ | L06-3-03 | Bổ đề 06.8 (b) thiếu "trên $W$"; "cực tiểu" dùng cho điểm. | "(b) có cực tiểu; (c) cực tiểu $\hat w_s$ duy nhất" | "(b) có điểm cực tiểu trên $W$; (c) điểm cực tiểu $\hat w_s$ duy nhất, …" (kèm tách đoạn ở mục 4) |
| K14 | nhẹ | L06-4-01 | Hệ số ổn định có đối số $m$; dòng mới viết thiếu. | "ERM ở dòng đầu: $\epsilon_{\mathrm{stab}}\ge1{,}7988$" | "$\epsilon_{\mathrm{stab}}(4)\ge1{,}7988$" |
| K15 | nhẹ | L06-3-01 | `no-ai-slop` Detect: "xét ở đây" nói về chính văn bản, dấu hai chấm kiểu nhãn. | "Tính chất xét ở đây: nghiệm đổi bao nhiêu khi thay một quan sát." | "Tính chất của thuật toán cần đo là độ dịch của nghiệm khi thay một quan sát." |
| K16 | nhẹ | L06-4-02; L06-4-04 (ghi chú diễn giả) | 4-02: "hiệu" không có tiền ngữ trên mặt trang. 4-04: mặt trang gọi bước 4 là kỹ thuật Bài 04, ghi chú diễn giả chỉ nói Fubini; thiếu câu nối. | 4-02: "ổn định đều chặn hiệu."; 4-04 ghi chú diễn giả: "theo định lý Fubini ta lấy kì vọng theo $\xi$ trước" | 4-02: "ổn định đều chặn hiệu giữa hàm lỗi tại $Z_i$ khi thay và khi giữ." (kiểm trần); 4-04: thêm "đây là bước lấy điều kiện rồi bỏ điều kiện của Bài 04, hợp lệ nhờ định lý Fubini vì $\xi$ độc lập với $(S,Z')$." |

Không thấy dấu hiệu `no-ai-slop` khác trong văn bản mới (không câu khẩu hiệu, không câu nói về mặt trang, không "Trang này …", không ID trang trong ghi chú diễn giả).

## 6. Kết luận

Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 5 trung bình (K1–K5), 11 nhẹ (K6–K16). **đạt khi sửa.** K1–K4 là sửa vài dòng; K5 theo bảng mục 4. Sau khi sửa: chạy lại `deck_lint.py` (kỳ vọng 0), `footer_check.py`, `deck_check.py`, xem ảnh 390 px `-end` của 2-08, 2-11, 3-01, 3-03, 7-03, và kiểm lại toán cùng mạch truyện ±2 của 7-03, 2-08, 3-01.
