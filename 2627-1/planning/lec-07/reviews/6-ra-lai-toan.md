# Rà lại toán học sau biên tập vòng 1 — Bài 07 (người rà 2)

Đối tượng: `lec07-r1-frozen.md` (1103 dòng; trùng `materials/lec-07/lecture-note.md`). Đầu vào phụ: `lec07-r1.udiff`, `reviews/0-quyet-dinh.md`, `bien-tap-vong-1.md`. Tính toán: `reviews07/r2/nums_r1.py`; script thí nghiệm chạy lại: `reviews07/r2/exp_out_r1.txt`. Đối chiếu thêm UML tr. 282 (Bài tập 20.1: sigmoid).

## Tổng kết theo mức

| Mức | Số phát hiện mới |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 0 |
| nhẹ | 4 |

Mọi phát hiện cũ đã được xử lý, trừ gợi ý tùy chọn mà điều phối viên quyết định không áp dụng. Mọi phần toán mới đều dựng lại được và mọi số mới đều đúng. Còn bốn điểm nhẹ: cách làm tròn khoảng chưa nhất quán, và diễn đạt ở ba chỗ.

## Phát hiện cũ (rà 2, bản đóng băng đầu)

| Mức cũ | Phát hiện | Trạng thái | Bằng chứng (dòng `lec07-r1-frozen.md`) |
|---|---|---|---|
| trung bình | Nhãn hoán vị không thỏa (T1); bán kính kiểm tra chỉ cho nhãn thật; "cố định trước khi rút" | ✓ | 590 (Ví dụ 07.6 Bước 3), 843 ("chỉ để so sánh, vì (T1) không thỏa"), 848 ("Với nhãn thật, … độc lập với $5000$ điểm kiểm tra"), 905, 917, 1097 |
| nhẹ | Cận trên làm tròn xuống | ✓ | 69–72 ($0{,}0961$, có câu giải thích), 582, 772, 776, 786, 804, 806, 909, 955, 970 |
| nhẹ | "không cần kiểm (M)" cần giới hạn vào mẫu tách trọn | ✓ | 584, 588 |
| nhẹ | Tính chất (iii) chỉ một chiều | ✓ | 705 |
| nhẹ | Hằng số $2G$ của bản có trị tuyệt đối | ✓ | 688 |
| nhẹ | Nhận xét 07.18: hệ số tự do khi đổi tỉ lệ | ✓ (còn một điểm diễn đạt, xem phát hiện mới N3) | 898 |
| nhẹ | Phụ lục A: trường hợp suy biến | ✓ | 1009, 1029 |
| nhẹ | Phụ lục C(iii): tính đo được của các cận trên đúng ở Bước 1–2 | ✓ | 1090 |
| nhẹ (tùy chọn) | Một lần McDiarmid ở Hệ quả 07.16 | không áp dụng, theo quyết định của điều phối viên (giữ hằng số blueprint); chấp nhận | 725 |

## Dựng lại các phần toán đã đổi

| Phần | Kết luận | Ghi chú |
|---|---|---|
| N1, quy ước chuẩn (9, 27, 281, 841, 960, 1101) | ✓ | Lớp ra tác động lên $a_1=\operatorname{ReLU}(\Theta_1x+b_1)$ với $\Theta_2=w^\top/\sqrt N$, nên $f_\theta=\langle w,\chi\rangle$ và $\lVert\Theta_2\rVert=\lVert w\rVert/\sqrt N$. Nghiệm chuẩn nhỏ nhất theo $w$ và theo $\Theta_2$ trùng nhau (tỉ lệ $1/\sqrt N$). Chuẩn báo trong bài là $\lVert w\rVert$; lề chuẩn hóa $\gamma/(\lVert\hat w\rVert C_x)$ và số hạng Rademacher $2\lVert\hat w\rVert C_x/(\gamma\sqrt m)$ dùng cùng cặp $(w,\chi)$, nhất quán. $20{,}475$ và $242{,}672$ khớp script; tỉ số $11{,}852$ không đổi. |
| (T1) với nhãn hoán vị (590, 843, 848, 1097) | ✓ | Các cặp $(X_i,Y_{\pi(i)})$ không độc lập. Cặp $(X_i,\tau_i)$ với $\tau_i$ độc lập với $x$ thì i.i.d. nên thỏa (T1). Diễn đạt "tổng các nhãn cố định": xem N2. |
| Ví dụ 07.11 Bước 4, cận logistic (864–870) | ✓ | Với $\lvert\langle w,x\rangle\rvert\le BC_x$, giá trị nằm trong $[\ln(1+e^{-BC_x}),K]\subset[0,K]$. Đạo hàm $-1/(1+e^t)\in(-1,0)$ nên hàm $1$-Lipschitz theo điểm số (kiểm số: $\max\lvert\ell'\rvert=1$). Sau khi chia cho $K$: $(1/K)$-Lipschitz, độ phức tạp $\le BC_x/(K\sqrt m)$; Định lý 07.11 rồi nhân $K$ cho $2BC_x/\sqrt m+3K\sqrt{\ln(2/\delta)/(2m)}$. (M) đúng nhờ liên tục theo $w$. Thiếu "B chọn trước mẫu": xem N4. |
| Nhận xét 07.18 (880–898) | ✓ | $G_j$ khớp $\rho_i$ của BFT; $y'$ không trùng $j$. Giả thiết $\lVert x_i\rVert\le C_x$ cho $\lVert X\rVert_2/m\le C_x/\sqrt m$. Nhân $\Theta_j$ với $c>0$ và chia $\Theta_{j+1}$ cho $c$ giữ $\prod\lVert\Theta\rVert_{\mathrm{op}}$; mỗi $r_j$ thuần nhất bậc $0$. Thuần nhất dương của ReLU giữ hàm $F_\Theta$, cả khi $\varsigma_J$ ở lớp ra là ReLU. |
| Không-ví dụ $\mathbb 1[x\in\mathbb Q]$ (161) | ✓ | $f_\theta$ liên tục nên $\{f_\theta\ge0\}=f_\theta^{-1}([0,\infty))$ đóng; $\mathbb Q$ không đóng. Kết luận đúng với mọi $J$ (kể cả $J=1$) và mọi hàm kích hoạt liên tục. |
| Ví dụ 07.8 Bước 3 (778) | ✓ | $d\ge2m$: một tập $2m$ điểm bị tách trọn, nên $\Pi(2m)=2^{2m}$ và $\rho_m\ge\sqrt{8\cdot2m\ln2/m}=\sqrt{16\ln2}=3{,}3302$. |
| Ví dụ 07.3 Bước 4 (289–296) | ✓ | Hai bản sao cùng nhãn và lớp tách trọn $m$ điểm phân biệt, nên có đúng $2^m$ cách gán nhãn; $\rho_m\ge\sqrt{8(m\ln2+\ln(4/\delta))/m}>\sqrt{8\ln2}=2{,}3548$. |
| Bảng Ví dụ 07.4 (396–410) | ✓ | Cột Bước 2: $-1,0,0,2,1,1,1,2$, tổng $6$. Cột Bước 3: $0,1,0,2,0,1,1,3$, tổng $8$. Liệt kê lại cả tám bộ dấu. |
| Câu hỏi cuối buổi (b) (941, 955) | ✓ | Đề cho $L^{<\gamma}_S(h_{\hat w})=0{,}04$; cận $0{,}2815$; với lưới: $\delta q_1=0{,}025$, $3\sqrt{\ln80/5000}=0{,}088812\le0{,}0889$, cận $0{,}288812\le0{,}2889$. |
| Định nghĩa 07.1 dạng đệ quy (147–153) | ✓ | Với $J=1$, $f_\theta=\Theta_1x+b_1$ (vòng lặp rỗng); với $J=2$ trùng dòng 156. |
| Ví dụ 07.9 Bước 5, bán kính $r$ (806) | ✓ | Với $\ell/4$ thỏa (T3), vế phải chia $4$ là bán kính đại diện của Mệnh đề 04.3. |
| Nhận xét 07.3 (201) | ✓ | UML Bài tập 20.1 và Thm 20.5 phát biểu cho sigmoid (tr. 273, 282). |
| Các phần khác có trong diff | ✓ | Câu ôn nhanh 2 (63); Ví dụ 07.7 (660–670) với $v_\sigma=\sigma_1+\sigma_2$ và $\mathbb E\lvert v_\sigma\rvert=1$; Mệnh đề 07.9(a) qua $\operatorname{err}_\tau$; bán kính $r$ (206); $P$ thay $\lvert E\rvert$ (302). |

## Bảng số

| Vị trí | Ghi chú | Tính được | Khớp? |
|---|---|---|---|
| 69 | $t\approx0{,}0961$ | $0{,}096032$; $e^{-400\cdot0{,}0961^2}=0{,}02487\le0{,}025$ | ✓ |
| 582 | $0{,}2881$; $0{,}0815$; $0{,}0408$ | $0{,}288097$; $0{,}081486$; $0{,}040743$ | ✓ (cận làm tròn lên) |
| 586 | $1{,}2881$ | $1{,}288097$ | ✓ |
| 293, 778 | $2{,}35$; $3{,}33$ | $2{,}3548$; $3{,}3302$ | ✓ (cận dưới) |
| 772, 776, 786, 909 | $0{,}0408$; $0{,}2408$ | $0{,}040743$; $0{,}240743$ | ✓ |
| 784 | $57\,957{,}2$ → $57\,958$; $231\,829$; $3690$ | $57\,957{,}21$; $231\,828{,}86$; $3689{,}72$ | ✓ |
| 804 | $0{,}8147$; $0{,}2577$; $0{,}0815$; $25{,}7625$; $66\,371$ | $0{,}814681$; $0{,}257625$; $0{,}081468$; $25{,}762486$; $\lceil66\,370{,}57\rceil$ | ✓ |
| 806 | $2\epsilon\le0{,}5153$ | $0{,}515250$ | ✓ |
| 832, 1103 | $C_x$ $1{,}517$–$1{,}544$ | $1{,}517566$–$1{,}543962$ | ✓ (làm tròn ra ngoài) |
| 838 | $916$ ($351$–$1721$) | $915{,}67$ ($351{,}478$–$1720{,}82$) | ✓ |
| 838 | lề chuẩn hóa $3{,}8\cdot10^{-4}$–$1{,}87\cdot10^{-3}$ | $3{,}804\cdot10^{-4}$–$1{,}8748\cdot10^{-3}$ | ✓ gần nhất; đầu trên chưa làm tròn ra ngoài (N1) |
| 839 | $10\,853$ ($6791$–$14\,052$) | $10\,852{,}6$ ($6791{,}53$–$14\,051{,}9$) | ✓ |
| 839 | lề chuẩn hóa $4{,}6\cdot10^{-5}$–$9{,}6\cdot10^{-5}$ | $4{,}642\cdot10^{-5}$–$9{,}639\cdot10^{-5}$ | ✓ gần nhất; đầu trên (N1) |
| 841 | $11{,}85$; $20{,}5$; $242{,}7$ | $11{,}8521$; $20{,}4750$; $242{,}6715$ (script: $20{,}475$; $242{,}672$) | ✓ |
| 843, 917 | $75$–$372$; $1467$–$3047$; "lớn hơn $75$" | $75{,}43$–$371{,}74$; $1467{,}12$–$3046{,}70$ | ✓ |
| 848, 917 | $\le0{,}0193$ | $0{,}019206$ | ✓ |
| 952 | $0{,}16$; $0{,}0815$; $0{,}2815$ | $0{,}16$; $0{,}081486$; $0{,}281486$ | ✓ |
| 955 | $0{,}0889$; $0{,}2889$ | $0{,}088812$; $0{,}288812$ | ✓ |
| 970 | $0{,}1185$; $0{,}0408$ | $0{,}118417$; $0{,}040743$ | ✓ |
| 20–21, 1103 | lỗi kiểm tra $0{,}023$ ($0{,}014$–$0{,}036$), $0{,}501$ ($0{,}480$–$0{,}512$); độ lệch chuẩn $0{,}0074$, $0{,}0095$ | $0{,}02298$ ($0{,}0140$–$0{,}0364$), $0{,}50108$ ($0{,}480$–$0{,}512$); $0{,}007357$, $0{,}009526$ | ✓ gần nhất; $0{,}036$ (N1) |
| 262, 271, 273 | $10{,}25$; $500{,}30$; $4{,}4721$; $3{,}20$; $22{,}37$ | như cũ | ✓ |
| Script | hạng $200$ (và $400$), lề nhỏ nhất $1$, lỗi huấn luyện $0$ | như ghi | ✓ |

## Bảng phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | 20, 838, 839 | Quy ước làm tròn khoảng quan sát chưa nhất quán. Chuẩn, $C_x$ và số hạng Rademacher được làm tròn ra ngoài ($351$, $1721$, $6791$, $14\,052$, $1{,}517$, $1{,}544$, $75$, $372$, $1467$, $3047$). Đầu trên của lề chuẩn hóa và của lỗi kiểm tra lại làm tròn gần nhất (xuống). | $1{,}8748\cdot10^{-3}\to1{,}87\cdot10^{-3}$; $9{,}639\cdot10^{-5}\to9{,}6\cdot10^{-5}$; $0{,}0364\to0{,}036$. | Làm tròn ra ngoài: $1{,}88\cdot10^{-3}$, $9{,}7\cdot10^{-5}$, $0{,}037$; hoặc ghi một lần rằng các khoảng quan sát làm tròn gần nhất và đưa $351$, $6791$ về cùng quy ước. Đây là số mô tả, không phải cận, nên chỉ cần nhất quán. |
| nhẹ | 590, 1097 | "tổng các nhãn cố định" có thể bị hiểu là tổng tất định. Tổng nhãn của mẫu hoán vị bằng tổng nhãn thật của các điểm, vẫn ngẫu nhiên theo mẫu; sự phụ thuộc đến từ ràng buộc chung đó. | Phụ lục D: hoán vị đều của $200$ nhãn huấn luyện. | "… không độc lập (tổng các nhãn hoán vị bằng tổng các nhãn thật) …". |
| nhẹ | 898 | "Với ReLU và $M_j=0$, $R_\Theta$ không đổi khi …" gắn ReLU vào tính bất biến của $R_\Theta$. Thực ra $R_\Theta$ bất biến với mọi hàm kích hoạt (tích chuẩn phổ giữ nguyên, $r_j$ thuần nhất bậc $0$). ReLU chỉ cần để hàm $F_\Theta$ không đổi. | (1.2) của BFT; Bước 2 Ví dụ 07.2 dùng thuần nhất dương. | "Với $M_j=0$, $R_\Theta$ không đổi khi nhân $\Theta_j$ với $c>0$ và chia $\Theta_{j+1}$ cho $c$; với ReLU, hàm $F_\Theta$ cũng không đổi, như Bước 2 của Ví dụ 07.2 (mạng ở đây không có hệ số tự do)." |
| nhẹ | 856, 864 | Bước 4 không nói $B$ chọn trước mẫu, trong khi đây là giả thiết cần cho cận logistic mới (lớp hàm lỗi cố định trước mẫu). Thiết lập ghi $\lVert x\rVert\le1$ nhưng công thức dùng $C_x$. Ngoài ra $L_D(w)$, $L_S(w)$ cho rủi ro logistic chưa được đặt tên. | Định lý 07.11 cần lớp cố định trước mẫu; Hệ quả 07.16 ghi rõ "$B>0$ cố định trước mẫu". | "Với $B$ chọn trước mẫu, $\lVert w\rVert\le B$ và $\lVert x\rVert\le C_x$, …"; đặt $L^{\log}_D(w)$, $L^{\log}_S(w)$ hoặc ghi "rủi ro logistic kì vọng và thực nghiệm $L_D(w)$, $L_S(w)$". |
