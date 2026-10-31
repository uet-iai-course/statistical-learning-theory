# Biên tập vòng 1 — Bài 07

Biên tập viên: người viết bản thảo (2026-10-31). Căn cứ: `reviews/0-quyet-dinh.md` (ưu tiên cao nhất), năm báo cáo `reviews/1-hoc-vien.md` … `5-mach.md`. Số dòng theo bản đóng băng `lec07-draft-frozen.md`. `no-ai-slop` chế độ Edit. Không commit.

**Số tiếng (`wc -w`).** Trước: thân bài 11 999, phụ lục 1 634. Sau: thân bài 11 954, phụ lục 1 715. Tệp 1 103 dòng (trước 1 088).

**Kiểm tra sau sửa.** `forward_refs.py` 0; sync và `--check` OK; `git diff --check` sạch; 40 khối mở, cân bằng, không lồng; không chữ có dấu trong `\text{}`. Viewer qua HTTP và `file://` ở 1600×900 và 390×844, mọi `details` mở: 0 `.katex-error`, 0 lỗi trang, 0 request hỏng, 0 công thức hay bảng tràn (lần đo đầu sau sửa có 3 chỗ tràn: Định nghĩa 07.1, Bảo đảm Mệnh đề 07.2, bảng Ví dụ 07.4; đã sửa). Ảnh ở scratchpad `editor07/shots/`, `editor07/blk*.png`.

**Script.** `exp_lec07_random_labels.py` in thêm `chuan_theta2` $=\lVert\hat w\rVert/\sqrt N$ (N1): trung bình $20{,}475$ ($7{,}86$–$38{,}48$) với nhãn thật và $242{,}672$ ($151{,}86$–$314{,}21$) với nhãn hoán vị; các số khác không đổi.

## Quyết định của điều phối viên

| Mã | Vị trí (bản đóng băng) | Cách sửa |
|---|---|---|
| N1 | dòng 9, 27; Ví dụ 07.3, 07.10; Phụ lục D | Một quy ước: lớp ra nhận đầu ra ẩn chia $\sqrt N$, chuẩn báo là $\lVert w\rVert$ trên đặc trưng chuẩn hóa. Câu hỏi mở đầu nói rõ việc chia $\sqrt N$ và quy tắc chọn nghiệm chuẩn nhỏ nhất; Ví dụ 07.3 ghi $\lVert\Theta_2\rVert=\lVert w\rVert/\sqrt N$; Ví dụ 07.10 báo thêm $20{,}5$ và $242{,}7$; Phụ lục D liệt kê đại lượng này. Phần phạt, lề chuẩn hóa dùng $\lVert w\rVert$ và $C_x$ của $\chi$, nhất quán. |
| TB1 | Ví dụ 07.6, 07.10, §10, Phụ lục D | Ví dụ 07.6 tách Bước 2 (nhãn thật) và Bước 3 (nhãn hoán vị: (T1) không thỏa, vế phải chỉ để so sánh); Ví dụ 07.10 Bước 3 ghi "chỉ để so sánh"; (ii) "hàm đã chọn độc lập với $5000$ điểm kiểm tra", chỉ cho nhãn thật; §10 "lỗi kiểm tra với nhãn thật"; Phụ lục D thêm hai câu. |
| TB2 | nhiều chỗ | $0{,}2408$; $0{,}2577$; $0{,}5153$; $0{,}0889$; $0{,}2889$; $0{,}0408$; $t\approx0{,}0961$ (có câu giải thích làm tròn lên); $351$. Kiểm thêm: bán kính $0{,}0193$ (là cận), §13 $0{,}1185$ (cận của UML), $C_x$ đầu dưới $1{,}517$, đầu dưới chuẩn hoán vị $6791$. Giữ $0{,}2881$, $0{,}0815$, $0{,}8147$, $1{,}2881$, $0{,}2815$ (đã đúng chiều). |
| TB3 | Tiên quyết | Ghi tên khối như Bài 06; thêm Ví dụ 03.1, Định nghĩa 04.1, 05.18, 06.9; "Bước 1–4" của Định lý 03.15; bỏ Ví dụ 05.10 (không dẫn). |
| TB4 | Cầu nối §12 | Thêm câu nối Phụ lục D (giới hạn của hạ gradient), Bài 06 "tính chất của thuật toán chứ không của lớp", câu hỏi Bài 08 nêu "hàm lỗi lồi, trơn và Lipschitz"; bỏ "nhưng với hàm lỗi lồi". |
| TB5 | Nhận xét 07.18 | $\rho_j\to G_j$; chỉ số nhãn $y'$ (không dùng $j$); thêm "Khi $\lVert x_i\rVert\le C_x$"; bất biến đổi tỉ lệ chỉ cho mạng ReLU không hệ số tự do. Giữ $k$ cho số nhãn (khối khác Nhận xét 07.17, không trùng nghĩa trong cùng khối). |
| TB6 | Ví dụ 07.7 | Một thiết lập nêu cả hai bộ điểm; $x_1=x_2=1$; $\mathbf e_i$ gọi tên; tiêu đề đổi. |
| TB7 | Ví dụ 07.4 | Bảng ba cột (bộ dấu, Bước 2, Bước 3) cùng hàng tổng; một câu ví dụ cho dòng đầu. Bảng bốn–năm cột tràn ở 390 px nên bỏ cột $\sigma_1$, $\sigma_2+\sigma_3$. Tiêu đề bỏ "tính tay". |
| TB8 | "phần phạt" | "Số hạng phạt" là tổng hai số hạng (§1, Hệ quả 07.16, Ví dụ 07.8); "số hạng Rademacher" là $2BC_x/(\gamma\sqrt m)$ (Ví dụ 07.10, §10, Phụ lục D). |
| TB9 | dòng 27, 588, 844, 847, 1088 | Thuật ngữ "cận không cho thông tin (vacuous bound)" đặt ở Ví dụ 07.6; bỏ ẩn dụ "chứng nhận rỗng"; "bằng chứng, không phải chứng minh" giữ ở câu hỏi mở đầu và §10, cắt ở Ví dụ 07.10 và Phụ lục D. |
| TB10 | Định nghĩa 07.1; Mệnh đề 07.2, 07.9 | Viết đệ quy $a_0=x$, $a_j=\varsigma(\Theta_ja_{j-1}+b_j)$; Mệnh đề 07.2: tham số viết trong câu, Bảo đảm viết qua $s$ trong dòng; Mệnh đề 07.9(a) qua $\operatorname{err}_\tau(h)$ (định nghĩa trong Giả thiết). Đã chụp ở 390 px. Chữ $a_j$ trùng chữ $a$ (véc-tơ của §6) nhưng khác mục; ghi ở `outline.md` §13. |
| TB11 | §12 (b) | Đề cho $L^{<\gamma}_S(h_{\hat w})=0{,}04$; lời giải nói cận vẫn là $0{,}2815$. |
| TB12 | §13, Ví dụ 07.9, 07.11 | §13 thêm UML §28.1 (đã đọc tr. 392: cận trên bất khả tri qua Rademacher); Ví dụ 07.11 Bước 4 thêm cận logistic $L_D\le L_S+2BC_x/\sqrt m+3K\sqrt{\ln(2/\delta)/(2m)}$, $K=\ln(1+e^{BC_x})$; Ví dụ 07.9 Bước 5 nối bán kính $r$ của Mệnh đề 04.3; bỏ dẫn Nhận xét 02.11 cho hàm lỗi bản lề. |
| TB13 | Ví dụ 07.3 B4, 07.8 B3, dòng 161 | Thêm lý do $2^m$ (hai bản sao cùng nhãn) và công thức $\rho_m$; Ví dụ 07.8: $d\ge2m\Rightarrow\Pi(2m)=2^{2m}$, $\rho_m\ge\sqrt{16\ln2}$; thay không-ví dụ hàm ghi nhớ bằng $\mathbb 1[x\in\mathbb Q]$ (tập $\{f_\theta\ge0\}$ đóng) — ngắn hơn, vẫn giữ một không-ví dụ cho Định nghĩa 07.1. |

## Phát hiện nhẹ và từng người rà

| Người rà / mã | Dòng | Cách sửa hoặc lý do không áp dụng |
|---|---|---|
| R1 (2r) | 224 | "$r$ là bán kính đại diện của mẫu". |
| R1 (§1 mục 4) | 80 | Tách §8 (hàm lỗi dốc) và §9 (bình phương). |
| R1, R5 F11 | bảng §2 | $B$ "(§5, §8)". |
| R1 | Ví dụ 07.2 B4 | Thêm $\lVert\Theta_2u\rVert=\lvert u_1-2u_2\rvert$. |
| R1, R3 F9 | dòng 9 | $c\to b$. |
| R1 | Phụ lục D | Thứ tự rút mảng; hai lượt dùng chung điểm và lớp ẩn. |
| R1, R4 #44 | dòng 25 | "thực hiện được mọi cách gán nhãn"; cụm đồng vị dời sau. |
| R1 | dòng 345 | Viết lại câu "cận trên đúng chọn hàm". |
| R1, R4, R5 F17 | 27, 847, 1088, 888 | Xem TB9; câu kết §9 còn một câu. |
| R1 #16 | dòng 605 | Cắt "đơn giản nhất". |
| R2 (M) | Ví dụ 07.6 | Giới hạn vào mẫu mà lớp tách trọn. |
| R2 (iii) | §8 | "trong cả hai trường hợp $\tilde yf\le0$" (một chiều). |
| R2 $2G$ | sau Bổ đề 07.14 | Thêm "dạng này thường được phát biểu với hằng số $2G$". |
| R2 | Nhận xét 07.18 | Xem TB5. |
| R2 | Phụ lục A | Trường hợp $\tilde D_k$ hằng và mọi $c_k=0$. |
| R2 | Phụ lục C(iii) | Thêm tính đo được của cận trên đúng theo $(S,S',\sigma)$. |
| R2 (tùy chọn) | Hệ quả 07.16 | **Không áp dụng**: một lần McDiarmid đổi hằng số blueprint; quyết định điều phối viên giữ $3\sqrt{\ln(2/\delta)/(2m)}$. |
| R3 F2–F9 | | F2 TB1; F3 TB2; F4, F5 TB5; F6 Nhận xét 07.3 nói "mạng sigmoid"; F7, F8 TB12; F9 R1. |
| R4 #13–#19 | | TB3, TB10, TB6, TB7, TB8, TB9. |
| R4 #20 | 316 | Cắt câu đầu. |
| R4 #21 | 188 | Cắt. |
| R4 #22 | 134, 138 | Viết lại 134; cắt câu đầu 138. |
| R4 #23 | ứng dụng | Một câu "Các giá trị $p$ và $BC_x/\gamma$ là giả định"; giữ ngoặc ở Ví dụ 07.8. |
| R4 #24 | tiêu đề | "Phân lớp văn bản". |
| R4 #25, R5 F15 | 9, 14, 16, 80, 110 | ReLU (rectified linear unit), permuted labels, "hạt giống ngẫu nhiên", score function, loss class. |
| R4 #26 | 234, 691 | Bỏ tiếng Anh lặp. |
| R4 #27 | Định nghĩa 07.5 | "lớp con bị chặn theo chuẩn" một tên. `thuat-ngu.md` ghi "lớp bị chặn theo chuẩn": đề xuất điều phối viên sửa (ngoài phạm vi ghi). |
| R4 #28–#30 | 110, 96, 161, 246, 892 | Tách câu dài; §10 tách đoạn "ba câu hỏi". |
| R4 #31 | 224 | Viết lại câu ba câu hỏi. |
| R4 #32, R5 | 480, 601, 757, 807 | Cắt 480, câu hai của 601 và 757; 807 viết lại. |
| R4 #33 | 888 | Cắt. |
| R4 #34 | 291, 307, 782, 684 | Bỏ dấu hai chấm "tiết lộ". |
| R4 #35 | 221, 239, 669 | Viết lại chủ thể. Câu 345: xem R1. |
| R4 #36, R5 F16 | 255 | "Một hàm có thể có nhiều véc-tơ tham số với chuẩn khác nhau, như ví dụ sau." |
| R4 #37–#39 | 605, 412, 307 | Đã sửa; Ví dụ 07.3 B4 có công thức $\rho_m$. |
| R4 #40 | Ví dụ 07.8 B4 | Thêm phép thay cho trường hợp đầu. |
| R4 #41, #42 | Mệnh đề 07.2, 07.9 | Xem TB10. Bước 1 chứng minh 07.2 giữ hai dòng (một dòng tràn 390 px). |
| R4 #43 | 896, 904, 922 | Đã sửa cả ba. |
| R4 #45 | tiêu đề 07.4; 828 | Đã sửa. |
| R4 #46 | 3, 963, 1021 | Đã sửa; thêm: "Phụ lục A/B chứng minh …" trong thân bài viết lại thành "Chứng minh (Phụ lục A) …". |
| R4 #47 | 349 | Cắt con trỏ bổ đề co. |
| R5 F1, F2, F3 | | TB3, TB4, TB5. |
| R5 F4–F7 | | TB12; F6 TB13. |
| R5 F8, F9 | | Thêm câu dẫn trước Bổ đề 07.8, Ví dụ 07.11, Nhận xét 07.18; câu mở §9 báo đủ các khối. |
| R5 F10 | 892 | Bỏ dẫn "(Mệnh đề 07.2)" cho số $\tfrac14$; không dẫn Ví dụ 05.10 (đã bỏ khỏi tiên quyết). |
| R5 F12, F13, F14 | | $P$ thay $\lvert E\rvert$; chỉ số $y'$; tiêu đề Ví dụ 07.2. |

## Chỗ cắt bù chữ (ngoài các mục cắt người rà đề xuất)

Định nghĩa 07.1: bỏ câu "hàm phân lớp là ngưỡng … như Định nghĩa 03.7" và "Kiến trúc được chọn trước; tham số chọn theo dữ liệu". Nhận xét 07.3: gộp câu Boole và câu xấp xỉ phổ quát. Định nghĩa 07.5: gộp đoạn bảo đảm cấp lớp. §6: rút đoạn đọc Định nghĩa 07.7 và câu nhãn thật. Ví dụ 07.4: bỏ Kết luận phụ. Ví dụ 07.5 B1: gộp câu. Bổ đề 07.10: rút đoạn sau bổ đề. Định lý 07.11: bỏ câu "Cận đúng đồng thời cho mọi $g$ …" ở đoạn đọc (R5), rút Bước 1–2, câu sau $\square$. Ví dụ 07.6: bỏ $m=10^6$. Ví dụ 07.7: Kết luận một câu. Bổ đề 07.14: thay lộ trình bằng "Chứng minh (Phụ lục B) xử lý từng tọa độ". Ví dụ 07.9: Kết luận rút. Ví dụ 07.10: bỏ mục (i) cũ (lặp §10), rút Thiết lập và Bước 1. Ví dụ 07.11: Kết luận rút. Nhận xét 07.18: bỏ "độ sâu vào cận qua tích và tổng". §10: rút năm gạch đầu dòng. §13: rút mục "Mạng nơ-ron" và "Lớp tuyến tính".

## Vòng 2 (2026-10-31)

Căn cứ: `reviews/6-ra-lai-toan.md` (4 điểm nhẹ) và `reviews/7-ra-lai-mach.md` (N1–N9); số dòng theo bản `lec07-r1-frozen.md`. `no-ai-slop` chế độ Edit.

**Số tiếng.** Thân bài 11 954 → 11 994; phụ lục 1 715 → 1 743.

**Kiểm tra.** `forward_refs.py` 0; sync và `--check` OK; `git diff --check` sạch; 80 dòng `:::`. Viewer qua HTTP và `file://` ở 1600×900 và 390×844: 0 `.katex-error`, 0 tràn, 0 lỗi trang, 0 request hỏng; cổng 8791 đã tắt.

| Mã | Dòng | Cách sửa |
|---|---|---|
| Toán 1 (làm tròn) | 20, 832, 839, 1103 | Quy ước theo điều phối viên: khoảng quan sát làm tròn gần nhất, chỉ cận trên của định lý làm tròn lên. $6791{,}53\to6792$; $C_x$ $1{,}517566\to1{,}518$. Các số khác đã là gần nhất ($351$, $1721$, $14\,052$, $1{,}544$, $0{,}014$–$0{,}036$, $1{,}87\cdot10^{-3}$, $9{,}6\cdot10^{-5}$, $75$–$372$, $1467$–$3047$, độ lệch chuẩn). Phụ lục D thêm một câu nêu quy ước. |
| Toán 2 | 590, 1097 | "(tổng các nhãn hoán vị bằng tổng các nhãn thật)". |
| Toán 3 | 898 | "Với $M_j=0$, $R_\Theta$ không đổi …; với ReLU, hàm $F_\Theta$ cũng không đổi …". |
| Toán 4 | 864 | "Với $B$ chọn trước mẫu, …"; đặt tên "rủi ro logistic kì vọng $L_D(w)$ và thực nghiệm $L_S(w)$". Thiết lập ($\lVert x\rVert\le1$) giữ: Bước 4 là phát biểu tổng quát với $C_x$. |
| N1 | 486 | Câu mở §7 bản rút gọn (+22). |
| N2 | 206 | "khi $S$ là $r$-đại diện (Định nghĩa 02.13)". |
| N3 | 41, 43 | Bỏ "thuật toán ghi nhớ", Định nghĩa 01.14, Bổ đề 03.12. |
| N4 | 875 | Theo đề xuất. |
| N5 | 25, 235, 808, 905 | Tách câu theo đề xuất. 195 và 609 không tách: 195 là câu kết chứng minh với hai vế song song, 609 đã có dấu chấm phẩy ngăn hai ý; tách sẽ phải lặp chủ ngữ. |
| N6 | 111, 135, 206 | Theo đề xuất. |
| N7 | 907 | Cắt câu mở đoạn. |
| N8 | 971 | Theo đề xuất. |
| N9 | 864, 872 | Chỉ thêm vế cho Kết luận; không đổi nhãn bước (bù chữ, theo chỉ dẫn điều phối viên). |

**Cắt bù chữ.** §10: bỏ câu "Ví dụ 07.9 cho hội tụ đều ($0{,}2577$ ở $m=10^4$) …" (lặp Kết luận Ví dụ 07.9; lời hứa Bài 06 dòng 854 vẫn giữ ở Ví dụ 07.9). Ví dụ 07.10 Bước 4(i): "cận như vậy không cho biết mô hình tốt hay kém" → "cận không cho thông tin" (dùng thuật ngữ đã đặt ở Ví dụ 07.6).
