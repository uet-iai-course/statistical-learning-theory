# Rà lại toán học sau biên tập vòng 1 — Bài 10 (người rà 2)

Đối tượng: `lec10-r1-frozen.md` (1040 dòng; `cmp` trùng `2627-1/materials/lec-10/lecture-note.md`), diff `lec10-r1.udiff`, `reviews/0-quyet-dinh.md`, `bien-tap-vong-1.md`. Chỉ đọc repo, không commit. Tính lại: `reviews10/r2b/check2.py` (phân số chính xác, mô phỏng); chạy lại `exp_lec10_pg_replay.py` ở lượt trước (số không đổi; Phụ lục C khớp từng số). Đã đọc lại chứng minh Mệnh đề 08.12 (lec-08, Phụ lục E) để kiểm câu nối ở Ví dụ 10.7, và Định nghĩa 09.1 để kiểm Phụ lục D.

## Tổng kết theo mức

| Mức | Số phát hiện mới |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 0 |
| nhẹ | 3 |

Mọi phát hiện cũ của người rà 2 đã được sửa đúng (10/10). Mọi phần toán đã đổi đều đúng; mọi số mới khớp. Ba điểm nhẹ là cách diễn đạt, không làm sai kết quả.

## Phát hiện cũ (`2-toan-hoc.md`)

| Mã cũ | Nội dung | Trạng thái | Kiểm |
|---|---|---|---|
| S1 (nghiêm trọng) | Kết luận Ví dụ 10.16 lẫn mô hình | ✓ | Dòng 769: $\mathbb EL_A(w_M)=\tfrac58+\tfrac1{8M}$ ($M=1,10,100$: $\tfrac34$, $\tfrac{51}{80}$, $\tfrac{501}{800}$) giảm về $L_A(\tfrac12)=\tfrac58$, không về $\min L_A=\tfrac12$: đúng. Câu thí nghiệm nêu rõ mô hình khác ($L_A=\tfrac12(w^2+0{,}25)$; $L_A(1)=0{,}625$, $L_A(\tfrac12)=0{,}25$, min $0{,}125$); bỏ "$0{,}331$ gần $0{,}25$". Phụ lục C dòng 988 báo mô hình khác. |
| T1 (trung bình) | Nhận xét 10.9(ii) | ✓ | Dòng 551: phần thưởng trước bước $t$ là hàm của $\mathcal F_t$ nên hợp lệ (Mệnh đề 10.7(a), Phụ lục B Bước 4); dẫn đúng Ví dụ 10.10, Bước 3. |
| T2 (trung bình) | §10, "$225$ lần", "$\alpha^2/(2M)$" | ✓ | Dòng 831, 835 gắn với Ví dụ 10.11 và 10.16. |
| N3 | "Khác Định nghĩa 05.10" | ✓ (còn một điểm diễn đạt, M1) | Dòng 406. |
| N4 | Mệnh đề 08.12 thiếu giả thiết | ✓ | Dòng 419: $J$ $\beta$-trơn, bị chặn trên ($F_*=-\sup J>-\infty$), phương sai có điều kiện bị chặn, $\eta\le1/\beta$ hằng, $\Theta=\mathbb R$. Chứng minh 08.12 (Bước 1–2) chỉ dùng cận trên bậc hai và kì vọng, phương sai có điều kiện theo lịch sử, nên câu nối "ở đây là các lượt trước" đúng; khả tích $\mathbb E\lvert J(\theta_j)\rvert<\infty$ có sẵn vì $J$ bị chặn. |
| N5 | $M$, $K$ trùng nghĩa | ✓ | Hàm trội $\Lambda$; hằng số $C_\mu$; số gia $\Delta$. |
| N6 | $B$ thay $R$ | ✓ | Nhận xét 10.16, Ví dụ 10.17 dùng $R$, "như Hệ quả 05.15". |
| N7 | $\Omega$ không chéo ngoài định nghĩa | ✓ | Định nghĩa 10.12: $\Omega$ đối xứng nửa xác định dương. |
| N8 | Mẫu gộp phân tầng | ✓ | Dòng 615: "tối thiểu hóa rủi ro thực nghiệm cho rủi ro trung bình $\frac1K\sum_kL_k$ (khi các mẫu cùng cỡ)". |
| N9 | "Chính sách tốt nhất" | ✓ | Ví dụ 10.11 Bước 1: trong họ sigmoid, $J\to c+0{,}6$ khi $\pi_\theta(1)\to1$. |

## Phần toán đã đổi (dựng lại)

| Vị trí | Đánh giá | Kiểm |
|---|---|---|
| N2, dòng 786 (hối tiếc $o(T)$) | ✓ | $\frac1T\sum_t\ell(w_t,z_t)-\min_u\frac1T\sum_t\ell(u,z_t)=\frac1T\sup_u\mathrm{Regret}_T(u)$; hối tiếc tĩnh $o(T)$ cho cận trên $o(1)$, có thể âm (Ví dụ 10.17: $-116{,}97$). Đúng. |
| Đoạn sau Thuật toán 10.6, dòng 406 | ✓ (nhẹ M1) | Viết $\tau_j=\Phi(\theta_j,\xi_j)$ với $\xi_j$ là các biến đều độc lập cùng phân bố: $\varphi(\theta,\xi)=-\hat g(\Phi(\theta,\xi))$, $\psi=-\nabla J$; (G2) thỏa với chính sách bảng (ước lượng bị chặn). Trở ngại là (G1) với $\partial F$ của $F=-J$ và tính lồi (C). |
| Ví dụ 10.6 Bước 2 | ✓ | $S_1$ không phụ thuộc $A_0$; $A_1$ khi biết $S_1$ không phụ thuộc $A_0$; nên $r_1\perp A_0$ và $\mathbb E[r_1(A_0-\tfrac12)]=0$; phần còn lại $-0{,}25$. Tọa độ $\theta_{s_0}$ của $\nabla\ln\pi(A_1\mid S_1)$ bằng $0$ vì $S_1\ne s_0$. |
| Ví dụ 10.7 Kết luận | ✓ | Xem N4. |
| Nhận xét 10.9(ii); Ví dụ 10.10 Bước 3 | ✓ | Ước lượng (i): $\tfrac12,\tfrac12$ (phương sai $0$); (ii): $\tfrac32,-\tfrac12$, phương sai $\tfrac12(\tfrac94+\tfrac14)-\tfrac14=1$; $b^*=2$. |
| Ví dụ 10.10 Bước 1–2 (bảng) | ✓ | Bước 1: tọa độ $\theta_{s_1}$ của (ii) nhận $\tfrac32$, $-\tfrac12$ (xác suất $\tfrac14$ mỗi giá trị), $0$ (xác suất $\tfrac12$); $\mathbb E X^2=\tfrac{10}{16}$, phương sai $\tfrac9{16}=0{,}5625$. Bảng (phân số chính xác): (i) $\tfrac{1619}{1600},\tfrac{11}{16},\tfrac{79}{320}$; (ii) $\tfrac{1619}{1600},\tfrac9{16},\tfrac3{64}$; (iii) $\tfrac{197}{800},\tfrac1{16},\tfrac1{64}$: khớp. Vết $1{,}94625$; $1{,}62125$; $0{,}324375$; tỉ số $6{,}000$ và $4{,}998$ ("khoảng năm lần"): đúng. Cột $\theta_{s_0}$ của (i), (ii) trùng vì $R_{\ge0}=R(\tau)$: đúng. |
| Nhận xét 10.14(ii) | ✓ (nhẹ M2) | Tại điểm cực tiểu $w^{(1)}$ của rủi ro cũ (khả vi hai lần), $L_A(w)\approx L_A(w^{(1)})+\tfrac12(w-w^{(1)})^\top\nabla^2L_A(w^{(1)})(w-w^{(1)})$. Fisher = Hesse của rủi ro log tại tham số thật khi mô hình chứa phân bố có điều kiện thật (đẳng thức thông tin, tập nhãn hữu hạn, khả vi hai lần); kiểm số bằng hồi quy logistic: Hesse và Fisher thực nghiệm khớp tới $10^{-3}$. Vì $\mathcal I_A$ ở (i) lấy tại $w^{(1)}$, đẳng thức cần $w^{(1)}$ là tham số thật, đúng như câu ghi "tại tham số thật". |
| Ví dụ 10.15 Bước 3 | ✓ | $\tfrac12(2v-2)^2=2(v-1)^2$, phạt $\tfrac\lambda2\cdot2v^2=\lambda v^2$; $4(v-1)+2\lambda v=0\Rightarrow v=\frac2{2+\lambda}$. |
| Ví dụ 10.16 Bước 3 (dạng tổng quát) | ✓ | $(1-\alpha)(w-1)+\alpha(w-\bar Z_M)=0\Rightarrow w_M=(1-\alpha)+\alpha\bar Z_M$; độ lệch so với $L_A(1-\alpha)$ là $\tfrac12\operatorname{Var}w_M=\alpha^2/(2M)$; mô phỏng $M=7$, $\alpha\in\{0{,}3;0{,}5;0{,}8\}$ khớp. |
| Ví dụ 10.17 Bước 1, 4 | ✓ | Hối tiếc tĩnh = hối tiếc so với $u=\tfrac12$ vì $u=\tfrac12$ cực tiểu hóa tổng. Quy nạp: $w_2=z_1$ với mọi $w_1$; nếu $w_t=\bar z_{1:t-1}$ thì $w_{t+1}=\tfrac{t-1}t\bar z_{1:t-1}+\tfrac1tz_t=\bar z_{1:t}\in[0,1]$ nên phép chiếu không tác động. Tính lại: hối tiếc $0{,}18765\to0{,}19$; $w_{T+1}=0{,}5$. |
| Ví dụ 10.2 Bước 4 (tổng mới) | ✓ | $0{,}6+0{,}2+0+0{,}05+0{,}2+0{,}1+0{,}2+0{,}4=1{,}75$. |
| Ví dụ 10.5 Kết luận | ✓ | $\tfrac14(1{,}7-1{,}8)=-0{,}025$. |
| Phụ lục C, đối chiếu script | ✓ | Rút $U$ bằng `rng.random()` trên $[0,1)$, $A_j=1$ khi $U<\pi_{\theta_j}(1)$, rồi $U'$ cho nhấp; cập nhật `th += eta*(r-b)*(a-s)` khớp công thức; $b_j=$ `tot/j` ($0$ khi $j=1$); độ lệch chuẩn `ddof=1`; bộ đệm `choice(..., replace=False)`; chỉ số phát lại `buf[rng.integers(M)]` mỗi bước, tức có hoàn lại; thứ tự rút khớp. Mọi số khớp. |
| Phụ lục D | ✓ | Thiết lập A/B của Định nghĩa 09.1 dùng đúng; Thiết lập B vi phạm (T1) vì cửa sổ chồng lấn phụ thuộc (khớp lec-09). (T3), (T2) với hàm lỗi log đúng như Bài 09. |
| Câu hỏi mở đầu, §1, Định nghĩa 10.10–10.11, §10 | ✓ | Không có thay đổi toán học khác; các số của Ví dụ 10.13 giữ nguyên. |

## Bảng phát hiện mới (dòng theo `lec10-r1-frozen.md`)

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | dòng 406 | Hai câu liền nhau tự mâu thuẫn: "ta được một oracle như Định nghĩa 05.10" rồi "vì Định nghĩa 05.10 … cần $-J$ lồi". Ngoài ra "các biến đều độc lập với các lượt trước" chưa đủ: Định nghĩa 05.10 cần các $\xi_j$ độc lập cùng phân bố. | Định nghĩa 05.10 (lec-05 dòng 503–511): "Cho $F$ lồi", các lần rút $\xi_1,\xi_2,\ldots$ độc lập cùng phân bố | "Viết mỗi lượt như một hàm của $\theta_j$ và các biến đều $\xi_j$ độc lập cùng phân bố, ta được nguồn ngẫu nhiên và ánh xạ oracle như Định nghĩa 05.10, với $\psi=-\nabla J$ (Bài tập 10.3). Điều còn thiếu là (C): Định nghĩa 05.10 và Định lý 05.14 cần $-J$ lồi." |
| nhẹ | dòng 735 | "khai triển Taylor bậc hai … với $\Omega$ là ma trận Hesse" chỉ đúng khi $\lambda=1$, hoặc khi $\lambda\Omega$ là ma trận Hesse, và khi rủi ro cũ khả vi hai lần; "bằng đúng phần tăng" cũng cần $\lambda\Omega=\nabla^2L_A$. Mệnh đề 10.13 có độ cong $1$, nên đẳng thức ở đó ứng với $\lambda=1$. | Mệnh đề 10.13, câu sau $\square$: phạt $=\lambda L_A$ | "Với $\lambda\Omega$ bằng ma trận Hesse của rủi ro cũ tại $w^{(1)}$, phạt bậc hai là phần bậc hai của khai triển Taylor quanh điểm cực tiểu $w^{(1)}$; nó bằng đúng phần tăng của rủi ro cũ khi rủi ro cũ là hàm bậc hai (Mệnh đề 10.13, $\lambda=1$)." |
| nhẹ | dòng 626 ("khác dấu"), 834 ("đổi dấu") | Hai quy ước cho độ quên $0$ và $-0{,}03$ ở nhiệm vụ 2 (Ví dụ 10.13, Bước 5); $0$ không mang dấu, nên "khác dấu/đổi dấu" chưa đúng nghĩa. | Ví dụ 10.13, Bước 5 và Kết luận ("bằng $0$ hay $-0{,}03$") | "… cho độ quên không âm theo quy ước này và âm theo quy ước kia"; §10: "Đổi quy ước đo có thể làm độ quên âm (Ví dụ 10.13)." |
