# Rà soát 2 — Chính xác toán học, Bài 10 (bản đóng băng `lec10-draft-frozen.md`, 1017 dòng)

Người rà: tác tử rà soát độc lập (chỉ đọc repo). Phương pháp: tự chứng minh lại mọi kết quả; tính lại mọi con số bằng `reviews10/r2/check.py` (phân số chính xác, sai phân hữu hạn, liệt kê quỹ đạo, mô phỏng); chạy lại `exp_lec10_pg_replay.py` (1,5 giây, mọi số khớp Phụ lục C và Ví dụ 10.11). Nguồn đã đối chiếu: UML §21.3 (tr. PDF 300–301, Định lý 21.15); Sutton–Barto tr. PDF 346 (trạng thái đầu cố định $s_0$, $J(\theta)=v_{\pi_\theta}(s_0)$), 348 ((13.5) dạng $\propto$), 350 (REINFORCE cập nhật từng bước), 351 (giá trị nền "even a random variable, as long as it does not vary with a"; câu về hội tụ); Kirkpatrick 2017 tr. 3 (xấp xỉ Laplace, đường chéo Fisher, phạt $\sum_i\frac\lambda2F_i(\theta_i-\theta^*_{A,i})^2$). Số hiệu chéo đã grep: 01.1, 01.5, 01.6, 01.9, 01.22, 01.24, 02.7, 02.8, 02.10, 02.14, 03.15, 04.11, 04.17, 05.10–05.16, 05.18, 06.2, 07.11, 08.12, 09.1, 09.2, 09.4, 09.8, 09.12, 09.14, 09.15, Phụ lục B Bài 09: đều tồn tại, đúng tên.

## Tổng kết theo mức

| Mức | Số |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 1 |
| trung bình | 2 |
| nhẹ | 7 |

Không phát hiện lỗi trong phát biểu hay chứng minh của các định lý/mệnh đề; mọi con số đúng. Lỗi nghiêm trọng là câu kết của Ví dụ 10.16 dùng số của một mô hình khác (Phụ lục C) mà không nói, mâu thuẫn với chính mô hình của ví dụ. Năm chuẩn của blueprint §E (Lecture 10) đều được tôn trọng (xem cuối tệp).

## Danh sách kết quả

| Kết quả | Đánh giá | Ghi chú |
|---|---|---|
| Bổ đề 10.3 (a), (b) | ✓ | (a): điểm cực tiểu trong của hàm không âm khả vi, cần $\Theta$ mở, đã ghi. (b): đạo hàm tổng hữu hạn trên tập chỉ số không phụ thuộc $\theta$. Điều kiện đủ và đúng chỗ dùng. |
| Ví dụ 10.3 (giá $U[0,\theta]$) | ✓ | $J'=\tfrac12$; kì vọng gradient log $-1/\theta$; $\mathbb E[A\cdot(-1/\theta)]=-\tfrac12$. |
| Định lý 10.4 | ✓ | Bước 1–3 đúng; $\mu_0$, $P$ chỉ vào ở Bước 3; khả vi của $\ln p_\theta$ trên giá đúng. "Không chặn phương sai, không nói về cực đại" đúng. |
| Nhận xét 10.5 + Phụ lục A Bước 1–5 | ✓ | Định lý giá trị trung bình trên đoạn trong quả cầu ⊂ $U$, hội tụ bị chặn cho đạo hàm theo hướng và cho tính liên tục của đạo hàm riêng, rồi "đạo hàm riêng liên tục ⇒ khả vi": đúng. Bước 5 cho $R\equiv1$ cần hàm trội cho $\lVert\nabla p_\theta\rVert$, đã ghi. |
| Phụ lục A Bước 6 (chính sách Gauss) | ✓ | Đã kiểm: $(a-\mu)^2\ge a^2/2-\mu^2$ (từ $a^2\le2(a-\mu)^2+2\mu^2$); $\mathcal N_\omega(a-\mu)\le e^{K^2/(2\omega^2)}\mathcal N_\omega(0)e^{-a^2/(4\omega^2)}$; $\lvert a-\mu\rvert\le\lvert a\rvert+K$; hàm trội = đa thức × Gauss × xác suất chuyển ($\le1$, tổng trên $\mathcal S^H$ hữu hạn) khả tích theo đếm × Lebesgue. Phác thảo đúng; chỉ có trùng chữ $K$ (xem phát hiện). |
| Thuật toán 10.6 + đoạn sau | ✓ (nhẹ) | $\mathbb E[\hat g_j\mid\tau_{<j}]=\nabla J(\theta_j)$ đúng ($\theta_1$, $\eta_j$ tất định). Câu "Khác Định nghĩa 05.10 …" xem phát hiện N3. |
| Ví dụ 10.6 (luật chuyển phụ thuộc $\theta$) | ✓ | Đạo hàm thật $0{,}125$ (sai phân hữu hạn $0{,}12500$), kì vọng ước lượng $-0{,}25$. |
| Ví dụ 10.7 (điểm dừng là cực tiểu) | ✓ | $q=0{,}375$, $\theta=\ln0{,}6\approx-0{,}5108$, $J=0{,}375$, $J''_\theta=3{,}2(q(1-q))^2=0{,}17578$; đi lên từ $-1$ → $J\to0{,}6$; từ $-0{,}4$ → $J\to1$ (mô phỏng). |
| Mệnh đề 10.7 + Phụ lục B | ✓ | Phân tích $p_\theta=\Pr(\mathbf h)\pi(a_t\mid s_t)\Pr(\mathbf h^+\mid\mathbf h,a_t)$; tổng trong bằng $\sum_a\nabla\pi=0$. Nhận xét "(a) không cần $\mu_0$, $P$ độc lập $\theta$" đúng. |
| Hệ quả 10.8 | ✓ | Đúng cho mọi $b_t$ là hàm của $\mathcal F_t$. |
| Ví dụ 10.9 (giá trị nền phụ thuộc hành động) | ✓ | $\mathbb E[A(A-\tfrac34)]=\tfrac3{16}$; kì vọng $\tfrac38-\tfrac{3\gamma}{16}$. |
| Nhận xét 10.9 (i) | ✓ | Số hạng thừa $-\nabla b_\theta\ln\pi_\theta$, kì vọng có điều kiện $\nabla b_\theta\cdot\mathrm H(\pi_\theta)$; $\ln2\approx0{,}6931$. |
| Nhận xét 10.9 (ii) | ✗ (trung bình) | Phát biểu quá rộng: xem T1. |
| Định nghĩa 10.10, 10.11 | ✓ | Độ quên $\ge0$ vì cực đại chứa $k=K$; chuẩn hóa $1/(K-1)$ khớp số hạng. |
| Mệnh đề 10.13 (a)–(d) | ✓ | $\lvert w\rvert+\lvert1-w\rvert\ge1$; $L_A+L_B=(w-\tfrac12)^2+\tfrac14$; $w_\lambda=1/(1+\lambda)$ duy nhất ($1+\lambda>0$); $L_A$ giảm, $L_B$ tăng theo $\lambda\ge0$; (d) $1-\alpha=1/(1+\lambda)\iff\alpha=\lambda/(1+\lambda)$; phạt $=\lambda L_A$. |
| Nhận xét 10.14 (EWC) | ✓ | Khớp Kirkpatrick tr. 3: xấp xỉ Laplace (MacKay), độ chính xác chéo bằng đường chéo Fisher, phạt $\frac\lambda2F_i(\theta_i-\theta^*_{A,i})^2$ đúng dạng Định nghĩa 10.12. Bổ đề 10.3(b) cho kì vọng $0$ khi $Y\sim p_{w^{(1)}}(\cdot\mid X)$: đúng (cần $w^{(1)}$ trong tập mở). |
| Ví dụ 10.15 (phạt đường chéo) | ✓ (nhẹ) | Đối xứng $(w_1,w_2)\mapsto(-w_2,-w_1)$, $v=2/(2+\lambda)$, $L_B=\tfrac29$, $\tfrac89$ (kiểm bằng tối ưu số). Bước 2 dùng $\Omega$ không chéo, ngoài Định nghĩa 10.12 (N5). |
| Ví dụ 10.16 (phát lại hữu hạn) | ✗ (nghiêm trọng, ở câu kết) | Bước 1–3 đúng ($\alpha^2/(2M)$ đúng cả với $\alpha$ tổng quát vì $w_M=(1-\alpha)+\alpha\bar Z_M$). Câu kết sai mô hình: S1. |
| Định nghĩa 10.15 | ✓ | |
| Nhận xét 10.16 (cận hối tiếc, $w_1$ tổng quát) | ✓ | Mệnh đề 05.13 (tất định, có chiếu) + bất đẳng thức dưới gradient, tổng triệt tiêu: $\frac{\lVert w_1-u\rVert^2}{2\eta}+\frac{\eta G^2T}2$; $\eta=B/(G\sqrt T)$ cho $BG\sqrt T$. UML Định lý 21.15 dùng $w^{(1)}=0$, $\lVert w^\star\rVert$ — tổng quát hóa đúng, ghi nguồn đúng. |
| Ví dụ 10.17 | ✓ | Xem bảng số. |
| Câu hỏi mở đầu, ôn nhanh, cuối buổi (a)–(f) | ✓ | |

## Bảng số (tính lại; `reviews10/r2/check.py`)

| Vị trí | Bản thảo | Tính lại | Kết luận |
|---|---|---|---|
| Mở đầu | $0{,}5$; $0{,}74$; $L_A$ lên $\tfrac12$ | $0{,}5$; $0{,}74$; $0{,}5$ | ✓ |
| Ôn nhanh 1 | $\ln40\approx3{,}6889$; $\le0{,}0608$ | $3{,}68888$; $0{,}060736$ | ✓ (làm tròn lên) |
| Ví dụ 10.1 | $J=\tfrac52$, $J'=\tfrac38$ | $\tfrac52$, $\tfrac38$ | ✓ |
| Ví dụ 10.2 | 8 xác suất, 8 tổng; $1{,}7$; $1{,}8$; $J=1{,}75$ | khớp từng dòng; $1{,}75$ | ✓ |
| Ví dụ 10.4 | $\pm0{,}75$; $\tfrac38$; $0$ | khớp | ✓ |
| Ví dụ 10.5 | $0{,}85$; $0{,}9$; $(-0{,}025;0{,}25;-0{,}125)$ | khớp; sai phân hữu hạn $(-0{,}02500;0{,}25000;-0{,}12500)$ | ✓ |
| Ví dụ 10.6 | $J=1{,}75$; $0{,}125$ vs $-0{,}25$ | $1{,}75$; FD $0{,}12500$; $-0{,}25$ | ✓ |
| Ví dụ 10.7 | $0{,}375$; $-0{,}5108$; $0{,}1758$; $0{,}2689$; $0{,}4013$ | $-0{,}51083$; $0{,}17578$; $0{,}26894$; $0{,}40131$ | ✓ |
| Ví dụ 10.8 | phương sai $\tfrac{27}{64},\tfrac3{16},0,\tfrac{147}{64}$; giá trị $\tfrac18,\tfrac98$, $-\tfrac12,3$; $b^*=\tfrac32$; "hơn năm lần" | khớp; $147/27=5{,}44$ | ✓ |
| Ví dụ 10.9 | $\tfrac3{16}$; $0$ | khớp | ✓ |
| Ví dụ 10.10 | vết $1{,}94625$; $1{,}62125$; $0{,}324375$; "đúng sáu lần"; Bước 2: $\tfrac12,\tfrac12$ (pv $0$), $\tfrac32,-\tfrac12$ (pv $1$), $b^*=2$ | khớp; tỉ số $6{,}000$ | ✓ |
| Ví dụ 10.11 | $0{,}05$; $0{,}1225$; $27{,}6225$; $0{,}06$; "khoảng $225$ lần" | khớp; $27{,}6225/0{,}1225=225{,}49$ | ✓ |
| Ví dụ 10.11 Bước 4 / Phụ lục C | $0{,}969/0{,}970/0{,}509/0{,}969$; $49$ lần; độ lệch chuẩn, khoảng | script khớp từng số | ✓ |
| Ví dụ 10.12 | $0{,}042947$; $\le0{,}1718$; $11\,804{,}4\to11\,805$ | $0{,}0429469$; $0{,}171788$; $11\,804{,}41$ | ✓ |
| Ví dụ 10.13 | $0{,}81$; $-0{,}11$; $0{,}10$, $0{,}17$, $0{,}135$; $0{,}025$; sửa hàng 3: $0{,}005$; $0{,}07$, $0$; $-0{,}03$ | khớp | ✓ |
| Ví dụ 10.14 | bảng 5 giá trị; tổng $\tfrac12,\tfrac5{16},\tfrac14,\tfrac5{16},\tfrac{41}{100}$; $\alpha$ | khớp (phân số chính xác) | ✓ |
| Ví dụ 10.15 | $v=\tfrac23$, $L_B=\tfrac29\approx0{,}2222$; $v=\tfrac13$, $\tfrac89\approx0{,}8889$ | khớp (tối ưu số) | ✓ |
| Ví dụ 10.16 | $\alpha^2/(2M)$; $0{,}125$; $0{,}0125$; $0{,}00125$ | công thức đúng; mô phỏng $0{,}1253$; $0{,}01263$; $0{,}001262$ | ✓ (Bước 3); câu kết: S1 |
| Phụ lục C phần phát lại | $0{,}011$; bảng 4 hàng; B: $0{,}126/0{,}218/0{,}248/0{,}255$ | script khớp | ✓ |
| Ví dụ 10.17 | $125$; $\le31{,}63$; $-116{,}97$; $w_{T+1}\approx1$; $0{,}19$; $\tfrac12$; $\tfrac18$ | $\sqrt{1000}=31{,}6228$; $-116{,}9673$; $w_{T+1}=0{,}9999999$; $0{,}18765$; $0{,}5$ | ✓ |
| Nhận xét 10.9(i) | $\ln2\approx0{,}6931$ | $0{,}693147$ | ✓ |
| Cuối buổi (a), (d) | $J'(0)=\tfrac12$; $1$, $0$; $\tfrac45,\tfrac8{25},\tfrac1{50},\tfrac15$ | khớp | ✓ |
| Cuối buổi (c), (e) | $-0{,}25$ vs $0{,}125$; $-116{,}97$, $L_A\approx\tfrac12$ | khớp | ✓ |

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | Ví dụ 10.16, Kết luận (dòng 749) | Câu kết so số thí nghiệm với "$0{,}25$ của điểm thỏa hiệp" và "$0{,}125$ của riêng nhiệm vụ A", nhưng trong mô hình của chính ví dụ ($Z\sim N(0,1)$, $L_A(w)=\tfrac12(w^2+1)$) điểm thỏa hiệp cho $L_A(\tfrac12)=0{,}625$, riêng A cho $0{,}5$, tinh chỉnh cho $L_A(1)=1$. Các số $0{,}25$, $0{,}125$, $0{,}624$ thuộc mô hình hồi quy $y=wx$ khác hẳn của Phụ lục C ($L_A=\tfrac12(w^2+0{,}25)$). Người đọc tự tính sẽ thấy $0{,}624\approx L_A(\tfrac12)=0{,}625$ của ví dụ, tức đọc ngược nghĩa. Thêm nữa, $0{,}331$ ($M=5$) không "gần $0{,}25$". | dòng 732 (thiết lập), 749 (kết luận), 1003–1006 (Phụ lục C); `check.py`: $L_A(\tfrac12)=0{,}625$, $L_A(0)=0{,}5$, $L_A(1)=1$ | Nói rõ thí nghiệm dùng một mô hình khác: "Thí nghiệm của học phần (Phụ lục C) dùng hồi quy $y=wx$, với $L_A(w)=\tfrac12(w^2+0{,}25)$: rủi ro kiểm tra trên A sau nhiệm vụ B là $0{,}624$ khi tinh chỉnh ($L_A(1)=0{,}625$) và $0{,}331$; $0{,}256$; $0{,}252$ với $M=5$, $50$, $1000$; hai giá trị sau gần $0{,}25=L_A(\tfrac12)$ của điểm thỏa hiệp, không gần $0{,}125$ của riêng nhiệm vụ A." Hoặc đổi thiết lập của ví dụ sang mô hình của Phụ lục C. |
| trung bình | Nhận xét 10.9(ii) (dòng 533) | "Giá trị nền tính từ phần thưởng của chính lượt đang dùng phụ thuộc hành động của lượt đó, nên vi phạm giả thiết của Hệ quả 10.8" sai khi $H\ge2$: phần thưởng $r_{t'}$ với $t'<t$ của chính lượt là hàm của $\mathcal F_t$, là giá trị nền hợp lệ cho bước $t$ (Mệnh đề 10.7(a)); Ví dụ 10.10 Bước 2 dùng đúng điều này ($-2$ đóng vai giá trị nền tốt nhất). | Mệnh đề 10.7(a), Phụ lục B Bước 4; Ví dụ 10.10 Bước 2 | "Giá trị nền dùng hành động hay phần thưởng từ bước $t$ trở đi của chính lượt đang dùng, chẳng hạn $R(\tau)$ hay $r(A_t)$, không là hàm của $\mathcal F_t$, nên vi phạm giả thiết của Hệ quả 10.8; phần thưởng nhận trước bước $t$ thì hợp lệ." |
| trung bình | §10, danh sách giới hạn, dòng 812 và 816 | Hai dòng phát biểu như kết quả chung một con số chỉ đúng trong một ví dụ: "dịch phần thưởng nhân phương sai khoảng $225$ lần", "Bộ đệm $M$ quan sát thêm $\alpha^2/(2M)$ vào rủi ro cũ theo kì vọng". $\alpha^2/(2M)$ dựa vào $\operatorname{Var}Z=1$, hàm lỗi bình phương và $L_B$ biết đủ; $225$ dựa vào $c=10$, xác suất nhấp $0{,}6/0{,}4$. | Ví dụ 10.11 Bước 2, Ví dụ 10.16 Bước 3 | Viết "trong Ví dụ 10.11, dịch phần thưởng $c=10$ nhân phương sai khoảng $225$ lần"; "trong Ví dụ 10.16, bộ đệm $M$ quan sát thêm $\alpha^2/(2M)$ …". |
| nhẹ | Đoạn sau Thuật toán 10.6 (dòng 397) | "Khác Định nghĩa 05.10, phân bố của nguồn ngẫu nhiên ở cập nhật $j$ phụ thuộc $\theta_j$" dễ gợi rằng khung oracle của Bài 05 không dùng được. Viết $\tau_j=\Phi(\theta_j,\xi_j)$ với $\xi_j$ là các biến đều độc lập cùng phân bố thì Định nghĩa 05.10 thỏa với $\varphi(\theta,\xi)=-\hat g(\Phi(\theta,\xi))$; trở ngại thật là (C). Ví dụ 10.7 cũng dùng Mệnh đề 08.12, vốn lấy lịch sử "như Định nghĩa 05.10". | Định nghĩa 05.10 (lec-05 dòng 503–511); Mệnh đề 08.12 (lec-08 dòng 776–781) | Thêm nửa câu: "… phụ thuộc $\theta_j$; viết lượt như một hàm của $\theta_j$ và các biến đều độc lập thì đưa được về Định nghĩa 05.10, nhưng Định lý 05.14 còn cần (C), tức $-J$ lồi." |
| nhẹ | Ví dụ 10.7, Kết luận | "Mệnh đề 08.12 áp dụng cho $F=-J$ khi $J$ trơn và ước lượng có phương sai bị chặn" bỏ hai giả thiết của 08.12: độ dài bước hằng $\eta\le1/\beta$ và $W=\mathbb R^p$ (có, vì $\Theta=\mathbb R$). | lec-08 dòng 776–790 | "… khi $J$ là $\beta$-trơn, ước lượng có phương sai bị chặn và độ dài bước hằng $\eta\le1/\beta$ …". |
| nhẹ | Nhận xét 10.5, Phụ lục A (dòng 306, 914–940) và Bước 6 (dòng 949) | Trùng kí hiệu: $M(\tau)$ là hàm trội, trong khi `ky-hieu.md` dành $M$ cho ngân sách bộ nhớ của chính Bài 10 (ghi "khác hàm trội (Bài 09)"); $K$ ở Bước 6 là hằng số chặn, trong khi $K$ là số nhiệm vụ. | `ky-hieu.md` dòng 113, 115 | Đổi hàm trội thành $\bar M$ hoặc $M_U$ (hoặc ghi rõ "khác ngân sách bộ nhớ $M$ ở §7"); đổi hằng số ở Bước 6 thành $C_\mu$. |
| nhẹ | Nhận xét 10.16, Ví dụ 10.17 Bước 2 | Dùng $B$ cho cận $\lVert w_1-u\rVert$, trong khi Bài 05 dùng $R$ cho đúng vai này ($\eta=R/(G\sqrt T)$, Hệ quả 05.15–05.16) và $B$ cho bán kính quả cầu; dòng 645 lại nói "$\mathcal B$ khác bán kính $B$ của Bài 05". | lec-05 dòng 845, 880–890; `ky-hieu.md` dòng 108 ("$R$ trần là cận khoảng cách Bài 05") | Dùng $R$ như Bài 05 (vì $R(\tau)$ luôn có đối số), hoặc nêu lí do đổi. |
| nhẹ | Định nghĩa 10.12 vs Ví dụ 10.15 Bước 2 | Định nghĩa đòi $\Omega$ đường chéo, nhưng Bước 2 dùng phạt với ma trận Hesse đầy đủ, nằm ngoài định nghĩa. | dòng 641, 722 | Nới định nghĩa thành "$\Omega$ đối xứng nửa xác định dương; thường chọn đường chéo", hoặc ghi ở Bước 2 "phạt với $\Omega$ không chéo, ngoài Định nghĩa 10.12". |
| nhẹ | Đoạn sau Định nghĩa 10.10 (dòng 595) | "Huấn luyện một lần trên mọi dữ liệu … với các mẫu cùng cỡ, là học có giám sát với phân bố $\frac1K\sum_kD_k$": mẫu gộp là mẫu phân tầng, không phải $m$ quan sát độc lập cùng phân bố hỗn hợp; rủi ro thực nghiệm chỉ là ước lượng không chệch của rủi ro hỗn hợp. | Định nghĩa 10.10 (các $S^{(k)}\sim D_k^{m_k}$) | "… là tối thiểu hóa rủi ro thực nghiệm cho rủi ro trung bình $\frac1K\sum_kL_k$, không phải học liên tục." |
| nhẹ | Ví dụ 10.11 Bước 1 | "chính sách tốt nhất vẫn là chọn nội dung $1$": chính sách tất định này không thuộc họ sigmoid; cận trên đúng $c+0{,}6$ chỉ đạt khi $\theta\to\infty$ (như Ví dụ 10.1). | Ví dụ 10.1, Kết luận | "… nên cận trên đúng của $J$ vẫn tiến tới khi $\pi_\theta(1)\to1$." |

## Chuẩn blueprint §E (Lecture 10)

| Chuẩn | Bản thảo |
|---|---|
| REINFORCE là đồng nhất thức về gradient, không bảo đảm hội tụ | ✓ dòng 268, 413, 808, 906 (không chép câu hội tụ của Sutton–Barto tr. 351) |
| Định lý 05.14 không áp dụng cho $J$ không lõm | ✓ đoạn sau Thuật toán 10.6, Ví dụ 10.7 |
| Giá trị nền không luôn giảm phương sai | ✓ Ví dụ 10.8 ($b=5$), Ví dụ 10.10 Bước 2 (tổng từ bước $t$) |
| Không có định lý học liên tục phổ quát | ✓ dòng 5, 682, 808 |
| Hối tiếc tĩnh nhỏ không bảo đảm độ quên nhỏ | ✓ Ví dụ 10.17, §10 |
