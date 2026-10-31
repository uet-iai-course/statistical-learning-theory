# Rà lại toán học sau biên tập vòng 1 — Bài 06 (R2)

Đối tượng: `lec06-r1-frozen.md` (trùng byte với `2627-1/materials/lec-06/lecture-note.md`, đã kiểm bằng `diff -q`), diff `lec06-r1.udiff`. Script: `reviews06/r2/check_r1.py` (số mới), `reviews06/r2/svg.py` (Hình 06.1), `reviews06/r2/check.py` (số cũ).

**Tổng kết:** 10/10 phát hiện cũ đã sửa đúng (#3 đúng phần giả thiết (T3), nhưng câu mới thêm về hồi quy logistic sinh một lỗi mới). Phát hiện mới: `chặn bàn giao` 0; `nghiêm trọng` 0; `trung bình` 1; `nhẹ` 2. Mọi số mới và cũ tính lại đều khớp; Hình 06.1 khớp số.

## 1. Phát hiện cũ

| # | mức cũ | vị trí cũ → mới | kết luận | ghi chú |
|---|---|---|---|---|
| 1 | chặn bàn giao | Định lý 06.10 Bước 2 → dòng 665–681; câu cuối khối định lý dòng 644 | ✓ | Dựng lại: (i) "cả hai vế bằng $\mathbb EL_D$ theo Bước 1" đúng, vì vế trái là Bước 1 cho $(S,Z')$, vế phải là Bước 1 cho cặp $(S^{(i)},Z_i)$, trong đó $Z_i$ độc lập với $(S^{(i)},\xi)$ và $S^{(i)}\sim D^m$ (cũng suy ra trực tiếp từ đẳng thức đổi chỗ). (ii) Với $(s,z')$ cố định, Định nghĩa 06.9 tại $z=z_i$ cho $\mathbb E_\xi\ell(A(s;\xi),z_i)\le\mathbb E_\xi\ell(A(s^{(i)};\xi),z_i)+\epsilon_{\mathrm{stab}}$. (iii) Lấy kì vọng theo $(S,Z')$ đúng thứ tự: $\xi$ độc lập với $(S,Z')$, hàm không âm, nên Fubini–Tonelli cho $\mathbb E_{S,Z'}\mathbb E_\xi=\mathbb E$. Kết quả $\mathbb E\ell(A(S;\xi),Z_i)\le\mathbb EL_D+\epsilon_{\mathrm{stab}}<\infty$. Câu cuối khối định lý ("Giả thiết khả tích và tính ổn định đều kéo theo …") nay đúng. |
| 2 | trung bình | Phụ lục E(iii) → dòng 1297 | ✓ | $\ell(A(s),z)=\mathbb 1[z\in\{z_1..z_m\}]$ nên $\ell(A(S),Z_i)=1$; mỗi hiệu $\ell(A(S^{(i)}),Z_i)-1\le0$, nên điều kiện một phía đúng với $\epsilon\equiv0$ dưới mọi $D$ (không cần $D$ liên tục). Với $z_i$ xuất hiện đúng một lần và $z'\ne z_i$, hàm lỗi tại $z_i$ đổi $1\to0$; hàm lỗi nhận giá trị trong $\{0,1\}$ nên hệ số nhỏ nhất đúng bằng $1$. Điều kiện "đúng một lần" là cần: nếu $z_i$ lặp, thay một bản sao không đổi đầu ra. (Ngầm cần $\lvert\mathcal Z\rvert\ge2$, hiển nhiên.) |
| 3 | trung bình | Nhận xét 06.14 → dòng 1051; §10 dòng 1068 | một phần | Giả thiết (T3) đã thêm. Số khối và cỡ mẫu xác thực đúng (kiểm dưới đây). Câu mới về hồi quy logistic sai về toán: phát hiện mới N1. |
| 4 | nhẹ | UML §12.2.2 → dòng 884, 1140 | ✓ | §12.2.1 (Ví dụ 12.9) và §12.2.2 tách đúng. |
| 5 | nhẹ | UML §14.5.1 → dòng 1146 | ✓ | Chỉ giữ khác biệt đếm $T$ / $T-1$; đúng (UML rút $z$ ở mọi $t=1..T$). |
| 6 | nhẹ | (L) và tập mở → dòng 740 | ✓ | |
| 7 | nhẹ | công thức ridge một chiều → dòng 570 | ✓ | |
| 8 | nhẹ | $1{,}7988$ → dòng 624 | ✓ | $304/169$ tại $z=(1,-1)$, là cực đại trên $\mathcal Z$. |
| 9 | nhẹ | Phụ lục A câu cuối → dòng 1179 | ✓ | |
| 10 | nhẹ | (a) cầu nối dòng 1134; (b) tên mục UML dòng 1295 | ✓ | |

## 2. Các phần toán đã đổi, dựng lại

| Phần | Kết luận | Ghi chú |
|---|---|---|
| Ví dụ 06.3 Bước 3 (dòng 403–410) | ✓ | $\mathbb E\bar w^2=\sum c_t^2+\sum_{t\ne s}c_tc_s\Pr(i_t=i_s)=\sum c_t^2+\tfrac14[(\sum c_t)^2-\sum c_t^2]=\tfrac14(\sum c_t)^2+\tfrac34\sum c_t^2=0{,}226059$ (hai dạng trùng tới $10^{-16}$). |
| Ví dụ 06.5, thiết lập mới (dòng 721–735) | ✓ | $h_0\equiv0$, $Y=\mathbb 1[X>\tfrac12]$ nên $\ell(h_0,Z)=Y\sim\mathrm{Bernoulli}(\tfrac12)$, $L_D(h_0)=\tfrac12$, hàm $\mathbb 1[x>\tfrac12]$ có rủi ro $0$. Công thức nhị thức đúng. Lập luận $1/\sqrt{2\pi m}$: $\sigma=1/(2\sqrt m)$, $\sigma\sqrt{2/\pi}=1/\sqrt{2\pi m}$, đúng (xấp xỉ chuẩn, nêu là "gần"). Định lý 06.10 với $\epsilon_{\mathrm{stab}}=0$ cho khoảng cách $=0$. |
| Ví dụ 06.7 Bước 3 (dòng 845–852) | ✓ | Cộng hai bất đẳng thức tăng trưởng với hệ số $\mu=2/m$: $\mu d^2\le 2Gd/m$, nên $d\le G=4$ với mọi $m$. |
| Ví dụ 06.8 (bỏ $G$ khỏi hàm lỗi) | ✓ | $\ell=10-zw$, $1$-Lipschitz, không âm trên $[-10,10]$; $\hat w=\bar z/\lambda\in W$; khoảng cách tổng quát hóa $=\mathbb E\bar z^2/\lambda=1/(\lambda m)=0{,}1$. |
| Ví dụ 06.9, $M=m$ (dòng 882) | ✓ | $\hat w_S=m/(m+m/2)=2/3$ với mọi $m$; $\hat w'=(m-1)/(m-1+m^2+m/2)\to0$; thay đổi hàm lỗi $\to1-\tfrac19=0{,}8889$ (tính: $0{,}8695$; $0{,}8869$; $0{,}8887$ với $m=10^2,10^3,10^4$). |
| Ví dụ 06.11 Bước 3 (dòng 1010–1018) | ✓ | $\epsilon_{\mathrm{stab}}=2/(4\cdot10^{-4}\cdot10^6)=0{,}005$; $\tfrac{\lambda^*}2B^2=2\cdot10^{-4}\cdot25=0{,}005$; tổng $0{,}01$. Hai cận ở kết luận cùng so với $\min_{\lVert u\rVert\le5}L_D$. |
| Nhận xét 06.14, chia khối (dòng 1051) | ✓ phần $[0,1]$; ✗ câu logistic | $k=\lceil\log_2(2/\delta)\rceil$: Markov cho mỗi khối hỏng (vượt $\epsilon/2$) với xác suất $\le\tfrac12$, cả $k$ khối hỏng $\le2^{-k}\le\delta/2$. Hệ quả 04.17(a) với $K=k$, $\delta/2$: bán kính $2\sqrt{\ln(4k/\delta)/(2m_v)}\le\epsilon/2\iff m_v\ge8\ln(4k/\delta)/\epsilon^2$. Với $\delta=0{,}05$, $\epsilon=0{,}1$: $k=6$, $m_v=4939{,}03\to4940$. Tổng $\le\epsilon$ với xác suất $\ge1-\delta$. |
| Bổ đề 06.8 sau $\square$ (dòng 547); câu dòng 234, 254 | ✓ (ghi chú nhẹ N3) | |
| Mệnh đề 06.5 Bước 1 (lí do hữu hạn) | ✓ | |
| Hệ quả 06.2, định nghĩa "rủi ro vượt mức kì vọng" (dòng 242) | ✓ | Khớp Định nghĩa 01.24 (so với lớp) và 04.1. Các lần dùng sau đều ghi rõ đối tượng so sánh ($u$, $W$, $W_B$). |
| Bảng kí hiệu $B$, $R$, $W_B$; §1 mục 6 | ✓ | Nhất quán với Ví dụ 06.1, 06.10, Hệ quả 06.13(c). |
| §10 (dòng 1064–1068), §13 hằng số | ✓ | Thừa số 8 so với 4: một phía cho $4G^2/(\lambda m)+\tfrac\lambda2B^2$, tối ưu bằng $GB\sqrt{8/m}$, trùng UML; đối xứng cho $2GB/\sqrt m$. Câu "khác biệt đến từ lập luận đối xứng" đúng. Bài tập 06.8 / UML 13.2: tốc độ hội tụ đều tăng theo $\log d$, đúng. |
| Hệ quả 06.13, câu "bất đẳng thức oracle" | ✓ | Khớp cách dùng ở Định lý 04.11. |
| Phụ lục D (đổi chỉ số) | ✓ | $w_k=2\eta\sum_{t<k}q^{k-1-t}y_t$, $c_t=(1-q^{T-t})/T$, công thức tổng không đổi. |
| Hình 06.1 (SVG mới) | ✓ | Đường cong khớp $F$ (sai số ≤ 0,002); điểm đánh dấu $w=0{,}7689;\,0{,}1540;\,0{,}2222;\,0{,}0442$, tung độ khớp; nhãn $0{,}615$, $0{,}178$, chú giải "mẫu $S^{(4)}$". |

## 3. Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | Nhận xét 06.14, ý "Chia khối và xác thực", câu cuối (dòng 1051) | Nếu chọn ứng viên trên mẫu xác thực bằng hàm lỗi 0–1, Hệ quả 04.17 chỉ bảo đảm rủi ro **0–1** của ứng viên được chọn gần mức tốt nhất. Nó không bảo đảm rủi ro **logistic** vượt mức không quá $\epsilon$, là đại lượng mà thủ tục chia khối hướng tới. Câu này đổi hàm lỗi mục tiêu giữa hai giai đoạn, nên thủ tục không còn cho bảo đảm xác suất cao cho $L_D$ logistic. | Hệ quả 04.17(a): $L_D(\hat g)\le\min_jL_D(g_j)+2\sqrt{\ln(2K/\delta)/(2m_v)}$, với cùng $\ell$ dùng để chọn và để đo. Không có bất đẳng thức chuyển hàm lỗi 0–1 về hàm lỗi logistic theo chiều cần. | Thay câu cuối bằng: "Với hồi quy logistic, hàm lỗi trên các ứng viên bị chặn: $F_{S,\lambda}(\hat w_S)\le F_{S,\lambda}(0)=\ln2$ cho $\lVert\hat w_S\rVert\le\sqrt{2\ln2/\lambda}$, nên $\ell\le\ln2+\sqrt{2\ln2/\lambda}$ khi $\lVert x\rVert\le1$; chia hàm lỗi cho cận này để dùng Hệ quả 04.17, và cỡ mẫu xác thực tăng theo bình phương của cận." (Với $\lambda^*=4\cdot10^{-4}$, cận là $\approx59{,}6$.) Nếu không muốn thêm chi tiết, bỏ câu và giữ điều kiện hàm lỗi trong $[0,1]$. |
| nhẹ | Bổ đề 06.8, câu sau $\square$ (dòng 547) | "$\hat w_S$ là đầu ra xác định của một thuật toán học" cần tính đo được của $s\mapsto\hat w_s$ (Định nghĩa 01.4), điều mà câu cũ ở đây nêu là giả thiết. Câu mới bỏ ý này; tính đo được chỉ còn được nêu ở cuối Phụ lục A. | Định nghĩa 01.4 và Định nghĩa 05.18 đòi $(s,z)\mapsto\ell(A(s),z)$ đo được. | Thêm "(với tính đo được của $s\mapsto\hat w_s$ giả sử như cuối Phụ lục A)". |
| nhẹ | Phụ lục E, định nghĩa (dòng 1287) | "một hàm giảm $\epsilon(m)$" trong khi phản ví dụ dùng $\epsilon\equiv0$, không giảm ngặt. | UML Def. 13.3: "monotonically decreasing", hiểu là không tăng. | Viết "một hàm không tăng $\epsilon(m)$". |
