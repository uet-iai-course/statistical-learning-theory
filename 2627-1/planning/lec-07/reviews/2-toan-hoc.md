# Rà soát 2 — Chính xác toán học, Bài 07 (bản đóng băng `lec07-draft-frozen.md`)

Người rà: R2 (chỉ đọc repo). Tính toán: `reviews07/r2/nums.py`, `reviews07/r2/sv.py`; đầu ra thí nghiệm chạy lại: `reviews07/r2/exp_out.txt`.
Nguồn đã đối chiếu trên PDF: UML tr. 272–273 (Claim 20.1, Thm 20.2, 20.5), 275 (chứng minh Thm 20.6, $(em)^{|E|}$), 276 (Thm 20.7), 378–379 (Lemma 26.4, Thm 26.5), 384–385 (Thm 26.12–26.14); BFT tr. 2–3 (định nghĩa (1.2), Theorem 1.1, $W$, $\lVert\cdot\rVert_{p,q}$).

## Tổng kết theo mức

| Mức | Số phát hiện |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 1 |
| nhẹ | 8 |

Mọi kết quả chứng minh lại được; mọi hằng số chính ($2\widehat{\mathfrak R}_S+3\sqrt{\ln(2/\delta)/(2m)}$, $2BC_x/(\gamma\sqrt m)$, $\ln(4/\delta)$ của cận hai phía, $\exp(-2t^2/\sum c_k^2)$) đúng. Mọi số của thí nghiệm khớp lần chạy lại. Phát hiện chủ yếu là phạm vi của (T1) với nhãn hoán vị và cách làm tròn cận trên.

## Kết quả chứng minh lại

| Kết quả | Kết luận | Ghi chú |
|---|---|---|
| Định nghĩa 07.1: đếm tham số $\sum N_j(N_{j-1}+1)$; $J=1$ cho $h_{w,b}$; $9$ tham số | ✓ | |
| Không-ví dụ ghi nhớ: $\{f_\theta\ge0\}$ hợp $\le N_1+1$ khoảng | ✓ | $p=1$: $\le N_1$ điểm gãy, trên mỗi khúc $f$ afin nên $\{f\ge0\}$ là một khoảng; $m$ điểm rời nhau cần $m$ thành phần liên thông. Định nghĩa 01.14 cho $A_{\mathrm{gn}}=1$ đúng tại các điểm nhãn $1$. |
| Ví dụ 07.1 (giá trị afin, $L_S=\tfrac14$, dẫn Ví dụ 03.3 Bước 3 = cách gán nhãn bù) | ✓ | |
| Mệnh đề 07.2 (XOR), điểm $(\tfrac12,\tfrac12)$, lề $\tfrac12$ | ✓ | |
| Ví dụ 07.2 (thuần nhất dương, $5c^2+5/c^2+\tfrac14$, chuẩn phổ $2c$, $\sqrt5/c$) | ✓ | |
| Ví dụ 07.3 (đếm $2000$/$6000$; tách trọn qua hạng; $d\le N$; $\Pi(2m)\ge2^m$ với điểm lặp, hợp lệ theo Định nghĩa 03.11; $\rho_m\ge\sqrt{8\ln2}$) | ✓ | Hạng $200$ vững: giá trị kì dị nhỏ nhất $9{,}1\cdot10^{-5}$–$3{,}2\cdot10^{-4}$, dung sai của `matrix_rank` khoảng $2{,}8\cdot10^{-13}$. |
| $0\le\widehat{\mathfrak R}(A)\le\sup\max_i\lvert a_i\rvert$ | ✓ | |
| Bổ đề 07.8 | ✓ | |
| Ví dụ 07.4 ($0,\tfrac14,\tfrac13,\tfrac12$; hai dãy giá trị lớn nhất) | ✓ | liệt kê lại cả tám bộ dấu |
| Mệnh đề 07.9 (a), (b), (c); quy ước $\{0,1\}$: $\sigma h=\tau-\mathbb 1[h\ne\tau]$; quy ước $\pm1$: $\sigma h=1-2\cdot\mathbb 1[h\ne\sigma]$, hằng số $1$, hệ số $2$ | ✓ | |
| Ví dụ 07.5 (dẫn Nhận xét 03.10(ii) với $\{2^{-i}\}$; (iii) cho $(0,1),(1,0),(1,1)$, thiếu $(0,0)$) | ✓ | khớp Bài 03 |
| Bổ đề 07.10 McDiarmid; giảm về Định lý 02.7(a),(b) với $c_i=(b-a)/m$ | ✓ | |
| Phụ lục A: $g_{k-1}=\mathbb Eg_k(\cdot,V_k)$ (Fubini, độc lập); $\tilde D_k$ có kì vọng $0$, dao động $\le c_k$ nên nằm trong đoạn dài $\le c_k$; Bổ đề 02.6; Bước 5 lặp Fubini đúng vì $D_k$, $k<m$, là hàm của $V_{1:m-1}$; $\kappa=4t/\sum c_k^2$ cho $-2t^2/\sum c_k^2$; nhận xét $[-c_k,c_k]$ cho $-t^2/(2\sum c_k^2)$ và hằng số $6$ | ✓ | trường hợp suy biến: phát hiện N7 |
| Định lý 07.11 (a): $\Psi\le\mathbb E_{S'}\sup$; đổi chỗ; tách sup; $-\sigma\sim\sigma$ | ✓ | lớp cố định trước mẫu dùng đúng chỗ (Bước 1) |
| Định lý 07.11 (b): sai phân $1/m$ cho $\Psi$ và $\widehat{\mathfrak R}_s$ (Phụ lục C(ii)); $t=\sqrt{\ln(2/\delta)/(2m)}$ cho $\delta/2$; đuôi trên cho $\Psi$, đuôi dưới cho $\widehat{\mathfrak R}_S$; $2(\widehat{\mathfrak R}_S+t)+t=2\widehat{\mathfrak R}_S+3t$ | ✓ | |
| Phụ lục C (i) đổi chỗ là hoán vị tọa độ của $D^{2m}$; (iii) (M) + hội tụ bị chặn | ✓ | phạm vi đo được: phát hiện N8 |
| Nhận xét 07.12 ($1-\mathcal G$, Bổ đề 07.8 với $c=-1$, $\bar a=\mathbf 1$, $\delta/2$ mỗi phía → $\ln(4/\delta)$) | ✓ | |
| Mệnh đề 07.13 (đẳng thức ở Bước 1 cả khi $v_\sigma=0$; Jensen; số hạng chéo) | ✓ | |
| Ví dụ 07.7 ($B/2$ so với $0{,}7071B$; trực chuẩn đạt dấu bằng) | ✓ | |
| Bổ đề 07.14 và Phụ lục B (gộp hai sup theo $(a,a')$, đối xứng bỏ trị tuyệt đối, lặp theo tọa độ, $G=0$ và $G>0$ qua Bổ đề 07.8); không cần $\phi_i(0)=0$; phản ví dụ $A=\{0\}$, $\phi_i\equiv1$ cho $0$ và $0{,}5$ | ✓ | |
| Định nghĩa 07.15 (i)–(iii): $\phi_\gamma$ là $(1/\gamma)$-Lipschitz, kẹp $\mathbb 1[t\le0]\le\phi_\gamma\le\mathbb 1[t<\gamma]$; sai phân lớp kéo theo $\tilde yf\le0$ | ✓ | diễn đạt "tức": phát hiện N4 |
| Hệ quả 07.16 ($B$, $\gamma$ chọn trước mẫu; (M) qua $w$ hữu tỉ; co với $\phi_i(a)=\phi_\gamma(\tilde y_ia)$; $2BC_x/(\gamma\sqrt m)$; bất biến theo $(cw,c\gamma,cB)$) | ✓ | |
| Ví dụ 07.9 ($\ell/4\in[0,1]$; $\lvert\phi_i'\rvert\le1$ trên $[-1,1]$, Mệnh đề 05.5(a) không cần $U$ lồi; nhân $4$ cho $8/\sqrt m+12\sqrt{\ln(4/\delta)/(2m)}$; rủi ro vượt mức $\le2\epsilon$) | ✓ | |
| Nhận xét 07.17 ($\sum1/(k(k+1))=1$; $\ln(2/(\delta q_k))=\ln(2/\delta)+\ln(k(k+1))$; như Bổ đề 04.9) | ✓ | |
| Ví dụ 07.10 ($\lvert\chi_j(x)\rvert\le(1+\lvert b_{1j}\rvert)/\sqrt N$; lề bằng $1$; $B_k=2^k\ge\lVert\hat w\rVert$) | ✓ | điều kiện theo lớp ẩn cố định; phạm vi (T1): phát hiện T1 |
| Ví dụ 07.11 (lớp $\tfrac12+\langle w,x\rangle$; $\{h_{w,0}:\lVert w\rVert\le10^{-6}\}=\mathcal H^p_{\mathrm{hom}}$; logistic trong $[0,\ln(1+e^{BC_x})]$) | ✓ | |
| Nhận xét 07.18 so với BFT Theorem 1.1 và (1.2): mạng không hệ số tự do, $\varsigma_j(0)=0$, $\rho_j$-Lipschitz; $R_\Theta=(\prod\rho_j\lVert\Theta_j\rVert_{\mathrm{op}})(\sum r_j^{2/3})^{3/2}$, $r_j=\lVert\Theta_j^\top-M_j^\top\rVert_{2,1}/\lVert\Theta_j\rVert_{\mathrm{op}}$; $\lVert A\rVert_{2,1}$ của BFT là tổng chuẩn các **cột** của $A$, nên $\lVert\Theta^\top-M^\top\rVert_{2,1}$ = tổng chuẩn các hàng của $\Theta-M$; $W=\max\{d,d_1,\ldots,d_L\}$ gồm $p$, $k$, các độ rộng; đồng thời mọi $\gamma>0$, mọi $\Theta$; vế mẫu $\le$ tỉ lệ lề $\le\gamma$; $\lVert X\rVert_2/m\le C_x/\sqrt m$ | ✓ | về đổi tỉ lệ với hệ số tự do: phát hiện N6 |
| Nhận xét 07.3, 07.6 so với UML: Claim 20.1 (độ sâu 2, hàm dấu), Thm 20.2 (cỡ mũ), Thm 20.5 (sigmoid, Lipschitz, cỡ mũ), Thm 20.7 ($k\ge3$ nơ-ron cùng một nơ-ron hằng, NP-khó), $(em)^{\lvert E\rvert}$ và $O(\lvert E\rvert\log\lvert E\rvert)$; số bài tập UML 20.1, 20.3 (tích), 20.4 (hợp), 20.5 (sigmoid) | ✓ | |
| §13: UML Thm 26.5(2) có $4c\sqrt{2\ln(4/\delta)/m}$; Lemma 26.4 hai phía, không chứng minh; §26.2 chuẩn hóa $B=1$ (Lemma 26.10); Thm 26.12 dùng phần (1) (kì vọng) | ✓ | |
| Chuẩn blueprint §E: loại bảo đảm (xác suất cao theo $S$, cấp lớp) nêu trong mọi định lý; hàm lỗi trong $[0,1]$ (bình phương chia $4$, logistic chia $\ln(1+e^{BC_x})$); cận tuyến tính chỉ dùng cho lớp ra với lớp ẩn cố định, không chuyển sang mạng sâu (Nhận xét 07.18, §10) | ✓ | |

## Bảng số

Quy ước: "khớp" khi số ghi đúng tới chữ số cuối theo làm tròn gần nhất; "↑" đánh dấu cận trên bị làm tròn xuống (theo quy tắc phải làm tròn lên).

| Vị trí | Ghi chú | Tính được | Khớp? |
|---|---|---|---|
| Ôn nhanh 1 | $1{,}5$; $\sqrt3\approx1{,}7321$ | $1{,}5$; $1{,}73205$ | ✓ |
| Ôn nhanh 3 | $t\approx0{,}0960$ | $0{,}096032$; tại $t=0{,}0960$ cận là $0{,}02506>0{,}025$ | ↑ (nên $0{,}0961$) |
| Ví dụ 07.1 | $-\tfrac12,\tfrac12,\tfrac12,\tfrac32$; $\tfrac14$ | như ghi | ✓ |
| Mệnh đề 07.2 | $-\tfrac12,\tfrac12,\tfrac12,-\tfrac12$; $f(\tfrac12,\tfrac12)=\tfrac12$ | như ghi | ✓ |
| Ví dụ 07.2 | $10{,}25$; $21{,}5$; $500{,}30$; $3{,}20$; $22{,}37$; $2\sqrt5\approx4{,}4721$ | $10{,}25$; $21{,}5$; $500{,}30$; $3{,}2016$; $22{,}3674$; $4{,}47214$ | ✓ |
| Ví dụ 07.3 | $P=2000$, $6000$ cố định, $P/m=10$, $\sqrt{8\ln2}\approx2{,}35$ | $2{,}35482$ | ✓ |
| Ví dụ 07.4 | $0$; $\tfrac14$ (tổng $6$); $\tfrac13$ (tổng $8$); $\tfrac12$ | $0$; $0{,}25$; $0{,}3333$; $0{,}5$ | ✓ |
| §8 phản ví dụ co | $0{,}5$ | $0{,}5$ | ✓ |
| Ví dụ 07.6 | $0{,}2881$; $0{,}0815$; $0{,}0407$; $0{,}0041$; $1{,}2881$ | $0{,}288097$; $0{,}081486$; $0{,}040743$; $0{,}0040743$; $1{,}288097$ | ✓ (gần nhất); $0{,}0407$ ↑ ($0{,}0408$) |
| Ví dụ 07.7 | $B/2$; $0{,}7071B$; $B/2$ | $1\cdot B/2$; $0{,}70711B$; $0{,}5B$ | ✓ |
| Ví dụ 07.8 | $0{,}2$; $0{,}0407$; $0{,}2407$ | $0{,}2$; $0{,}040743$; $0{,}240743$ | ↑ ($0{,}2408$) |
| Ví dụ 07.8 | $3\sqrt{\ln40/2}\approx4{,}0743$ | $4{,}074305$ | ✓ |
| Ví dụ 07.8 | $57\,958$; $231\,829$; $3690$ | $\lceil57\,957{,}21\rceil$; $\lceil231\,828{,}86\rceil$; $\lceil3689{,}72\rceil$ | ✓ |
| Ví dụ 07.8 | $\rho_m\ge3{,}33$ | $\sqrt{16\ln2}=3{,}3302$ | ✓ |
| Ví dụ 07.9 | $\ln80\approx4{,}3820$; $0{,}8147$; $0{,}2576$; $0{,}0815$ | $4{,}382027$; $0{,}814681$; $0{,}257625$; $0{,}081468$ | $0{,}2576$ ↑ ($0{,}2577$) |
| Ví dụ 07.9 | $25{,}7625$; $66\,371$ | $25{,}762486$; $\lceil66\,370{,}57\rceil$ | ✓ |
| Ví dụ 07.9 | $2\epsilon=0{,}5152$ | $0{,}515250$ | ↑ ($0{,}5153$) |
| Ví dụ 07.10 | $C_x$ $1{,}518$–$1{,}544$ | $1{,}5176$–$1{,}5440$ | ✓ |
| Ví dụ 07.10 | $\lVert\hat w\rVert$ thật: TB $916$ ($352$–$1721$) | $915{,}67$ ($351{,}48$–$1720{,}82$) | ✓ |
| Ví dụ 07.10 | hoán vị: TB $10\,853$ ($6792$–$14\,052$) | $10\,852{,}6$ ($6791{,}53$–$14\,051{,}9$) | ✓ |
| Ví dụ 07.10 | lề chuẩn hóa thật $3{,}8\cdot10^{-4}$–$1{,}87\cdot10^{-3}$; hoán vị $4{,}6\cdot10^{-5}$–$9{,}6\cdot10^{-5}$ | $3{,}804\cdot10^{-4}$–$1{,}8748\cdot10^{-3}$; $4{,}642\cdot10^{-5}$–$9{,}639\cdot10^{-5}$ | ✓ |
| Ví dụ 07.10 | tỉ số $11{,}85$ | $11{,}8521$ | ✓ |
| Ví dụ 07.10 | phần phạt $75$–$372$; $1467$–$3047$ | $75{,}43$–$371{,}74$; $1467{,}12$–$3046{,}70$ | ✓ |
| Ví dụ 07.10 (iii), §10 | bán kính $0{,}0192$ | $0{,}019206$ | ✓ (gần nhất; ↑ cho $0{,}0193$ nếu coi là cận) |
| Câu hỏi mở đầu | lỗi KT thật $0{,}023$ ($0{,}014$–$0{,}036$); hoán vị $0{,}501$ ($0{,}480$–$0{,}512$); lỗi HL $0$ | $0{,}02298$ ($0{,}0140$–$0{,}0364$); $0{,}50108$ ($0{,}4800$–$0{,}5120$); $0$ | ✓ |
| Phụ lục D | độ lệch chuẩn $0{,}0074$; $0{,}0095$; lề nhỏ nhất $1$; hạng $200$ | $0{,}007357$; $0{,}009526$; $1$ (sai số $10^{-13}$); $200$ (cả $400$ trên $400$ điểm) | ✓ |
| §12 (a) | $0{,}16$; $0{,}0815$; $0{,}2815$ | $0{,}16$; $0{,}081486$; $0{,}281486$ | ✓ |
| §12 (b) | $\delta q_1=0{,}025$; $0{,}0888$; $0{,}2888$ | $0{,}025$; $0{,}088812$; $0{,}288812$ | ↑ ($0{,}0889$; $0{,}2889$) |
| §12 (c) | $0{,}04$; $0{,}16$ | $2/50=0{,}04$; $0{,}16$ | ✓ |
| §13 | UML $0{,}1184$; học phần $0{,}0407$ | $0{,}118417$; $0{,}040743$ | ✓ |

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | Câu hỏi mở đầu; Ví dụ 07.6 Bước 2; Ví dụ 07.10 Bước 4(iii); §10 gạch "Cận không cho thông tin"; Phụ lục D | Với nhãn hoán vị, mẫu huấn luyện và mẫu kiểm tra không thỏa (T1): một hoán vị đều của $m$ nhãn cho các cặp $(X_i,Y_{\pi(i)})$ hoán đổi được nhưng không độc lập (số nhãn $1$ cố định). Ghi chú vẫn tính vế phải của Định lý 07.11 "như nhau cho nhãn thật và nhãn hoán vị" và dẫn Hệ quả 02.10(b) (giả thiết (T1)) cho bán kính $0{,}0192$ của lỗi kiểm tra mà không giới hạn vào nhãn thật. Thêm nữa, (iii) viết "hàm đã chọn cố định trước khi rút $5000$ điểm kiểm tra", trong khi giao thức (Phụ lục D, script) rút điểm kiểm tra thứ hai, trước lớp ẩn và huấn luyện; điều đúng là hàm đã chọn độc lập với mẫu kiểm tra. | Phụ lục D: "Một hoán vị đều của $200$ nhãn huấn luyện, và một hoán vị đều độc lập của $5000$ nhãn kiểm tra"; "thứ tự rút cố định: điểm huấn luyện, điểm kiểm tra, lớp ẩn …". Hệ quả 02.10 giả thiết "$S\sim D^m$ theo (T1)" và "$h$ cố định, không phụ thuộc $S$". | (iii): "Với nhãn thật, hàm đã chọn độc lập với $5000$ điểm kiểm tra, nên Hệ quả 02.10(b) cho …". Thêm một câu ở Ví dụ 07.6 Bước 2 hoặc Phụ lục D: "Nhãn hoán vị là một phép xấp xỉ của nhãn độc lập với $x$; các cặp của mẫu hoán vị không độc lập, nên các định lý cấp lớp chỉ áp dụng chặt chẽ cho nhãn thật; với nhãn hoán vị, các con số chỉ dùng để so sánh." Ở Ví dụ 07.6, giữ khẳng định về giá trị $\widehat{\mathfrak R}_S=\tfrac12$ (không phụ thuộc nhãn, Mệnh đề 07.9(b)), bỏ hoặc rào phần "vế phải … như nhau cho nhãn hoán vị". |
| nhẹ | Ôn nhanh 3; Ví dụ 07.6 Bước 1; Ví dụ 07.8 Bước 2–3 và Kết luận; Ví dụ 07.9 Bước 4–5; §10; §12 (b); §13 | Cận trên làm tròn xuống, trái quy tắc "cận trên làm tròn lên". | $0{,}240743\to0{,}2407$; $0{,}257625\to0{,}2576$; $0{,}515250\to0{,}5152$; $0{,}288812\to0{,}2888$; $0{,}088812\to0{,}0888$; $0{,}040743\to0{,}0407$; $t=0{,}096032\to0{,}0960$ cho $e^{-400t^2}=0{,}02506>0{,}025$. | Sửa thành $0{,}2408$ (Ví dụ 07.8, Kết luận, §10), $0{,}2577$ (Ví dụ 07.9, §10), $0{,}5153$, $0{,}0889$ và $0{,}2889$ (§12 b), $0{,}0408$ (Ví dụ 07.6, 07.8, §13), $t\approx0{,}0961$ (hoặc "$t=\sqrt{\ln40/400}\approx0{,}0960$, lấy $t\ge0{,}0961$"). Giữ $0{,}2881$, $0{,}2815$, $0{,}0815$, $0{,}8147$, $1{,}2881$ (đã đúng chiều). |
| nhẹ | Ví dụ 07.6 Bước 2 | "Vế phải lớn hơn $1$ … nên không cần kiểm (M)" dựa vào $\widehat{\mathfrak R}_S(\mathcal G)=\tfrac12$, chỉ đúng trên những mẫu mà lớp tách trọn $200$ điểm (đã thấy trong mười lần chạy qua hạng $200$), không được chứng minh cho mọi $S$. | Ví dụ 07.3 Bước 3 và Ví dụ 07.5 Bước 1 dựa vào hạng quan sát được. | "Trên mỗi mẫu mà lớp tách trọn các điểm huấn luyện (cả mười lần chạy), vế phải không nhỏ hơn $1$ với mọi $g$, nên bất đẳng thức đúng tầm thường trên các mẫu đó." |
| nhẹ | §8, tính chất (iii) sau Định nghĩa 07.15 | "sai tại $z$ khi …, tức $\tilde yf(x)\le0$" đọc như tương đương; thực ra chỉ một chiều: $y=1$, $f(x)=0$ cho lề $0$ nhưng phân lớp đúng. | $\mathbb 1[f\ge0]$ với $f=0$ trả $1$. | "…; trong cả hai trường hợp $\tilde yf(x)\le0$." |
| nhẹ | §8, đoạn sau Bổ đề 07.14 | Câu "với định nghĩa dùng $\mathbb E\sup\lvert\cdot\rvert$, cần thêm điều kiện đó" có thể khiến người đọc hiểu rằng hằng số vẫn là $G$; dạng có trị tuyệt đối thường được phát biểu với $\phi_i(0)=0$ và hằng số $2G$ (Ledoux–Talagrand). | Không có nguồn trong ghi chú cho hằng số của dạng có trị tuyệt đối. | Thêm "(và hằng số thường là $2G$)" hoặc bỏ hẳn so sánh hằng số, chỉ giữ ví dụ $A=\{0\}$. |
| nhẹ | Nhận xét 07.18, câu "Với $M_j=0$, $R_\Theta$ không đổi khi đổi tỉ lệ như Ví dụ 07.2" | Mạng của BFT không có hệ số tự do, còn phép đổi tỉ lệ của Ví dụ 07.2 nhân cả $b_1$ và giữ $b_2$; bất biến chỉ nói về hai ma trận trọng số. | BFT (1.1): $F_A(x)=\sigma_L(A_L\cdots\sigma_1(A_1x))$, không có hệ số tự do. | "… không đổi khi nhân $\Theta_j$ với $c$ và chia $\Theta_{j+1}$ cho $c$, như Bước 4 của Ví dụ 07.2." |
| nhẹ | Phụ lục A, Bước 4 và Bước 6 | Bổ đề 02.6 giả thiết $a<b$; khi $\sup\tilde D_k=\inf\tilde D_k$ (chẳng hạn $c_k=0$) cần nói cận đúng tầm thường. Lựa chọn $\kappa=4t/\sum_kc_k^2$ cần $\sum_kc_k^2>0$. | Bổ đề 02.6: "$a\le V\le b$ … với $a<b$". | Thêm: "Nếu $\tilde D_k$ hằng thì $\tilde D_k(V_k)=0$ và cận đúng tầm thường." và "Nếu mọi $c_k=0$ thì $Q$ hằng và xác suất bằng $0$." |
| nhẹ | Định lý 07.11 Bước 0; Phụ lục C(iii) | Bước 0 và C(iii) chỉ khẳng định $\Psi$ và $\widehat{\mathfrak R}_S$ đo được, nhưng Bước 1–2 lấy kì vọng của $\sup_g\frac1m\sum_i(g(Z'_i)-g(Z_i))$ và bản có $\sigma$, là hàm của $(S,S',\sigma)$. Cùng lập luận áp dụng, nhưng chưa được nói ra. | Bước 1: "Lấy kì vọng theo $S$ (định lý Fubini), $\mathbb E\Psi$ không quá kì vọng theo $(S,S')$ của $\sup_g\ldots$". | C(iii), câu cuối: "Cùng lập luận cho tính đo được của $\widehat{\mathfrak R}_s(\mathcal G)$ và của các cận trên đúng theo $(S,S',\sigma)$ ở Bước 1–2." |
| nhẹ (tùy chọn) | Hệ quả 07.16; Ví dụ 07.8 | Cận đúng nhưng lỏng hơn cần thiết: Mệnh đề 07.13 chặn $\widehat{\mathfrak R}_S$ tất định, nên lần dùng McDiarmid thứ hai không cần; một lần cho $\Psi$ cùng $\mathbb E\Psi\le2\mathfrak R_m\le2BC_x/(\gamma\sqrt m)$ cho số hạng tin cậy $\sqrt{\ln(1/\delta)/(2m)}$ ($0{,}0122$ thay cho $0{,}0408$ khi $m=10^4$, $\delta=0{,}05$). Không phải lỗi. | Định lý 07.11 Bước 4; UML Thm 26.12 cũng dùng dạng kì vọng. | Có thể thêm một câu sau Hệ quả 07.16: "Vì cận của Mệnh đề 07.13 không phụ thuộc mẫu, chỉ cần một lần bất đẳng thức McDiarmid; số hạng tin cậy giảm còn $\sqrt{\ln(1/\delta)/(2m)}$." Không bắt buộc; nếu thêm thì cập nhật các số liên quan. |
