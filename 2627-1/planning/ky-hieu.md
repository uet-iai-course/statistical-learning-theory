# Bảng kí hiệu chung của học phần

Mọi ghi chú và bài tập dùng đúng bảng này (theo blueprint mục A, tức kí hiệu của UML). Sách *Học máy thống kê* là mẫu văn phong và thuật ngữ tiếng Việt, nhưng kí hiệu của sách khác ($\mathcal P$ cho phân bố, $D$ cho tập dữ liệu, $n$ cho cỡ mẫu, $\mathrm{err}_{\mathcal P}$ cho rủi ro); không dùng kí hiệu của sách trong học phần này.

| Kí hiệu | Ý nghĩa | Ghi chú |
|---|---|---|
| $\mathcal X$, $\mathcal Y$, $\mathcal Z=\mathcal X\times\mathcal Y$ | Tập đầu vào, tập nhãn, tập quan sát | Với ước lượng mật độ, $\mathcal Z=\mathcal X$ |
| $Z=(X,Y)$ | Một quan sát ngẫu nhiên | Chữ hoa cho biến ngẫu nhiên, chữ thường cho giá trị |
| $D$ | Phân bố sinh dữ liệu trên $\mathcal Z$ | Không dùng $D$ cho tập dữ liệu |
| $S=(Z_1,\ldots,Z_m)\sim D^m$ | Mẫu huấn luyện gồm $m$ quan sát độc lập cùng phân bố | Ghi rõ khi giả thiết độc lập không áp dụng |
| $m$ | Cỡ mẫu | Không dùng $n$ cho cỡ mẫu |
| $\mathcal H$ | Lớp giả thuyết | Cố định trước khi quan sát mẫu, trừ khi nói khác |
| $h$ | Một giả thuyết (hàm dự đoán) $\mathcal X\to\mathcal Y$ | Với bài toán phân lớp: hàm phân lớp |
| $\ell(h,z)$ | Hàm lỗi của $h$ trên quan sát $z$ | $\ell_{0\text{-}1}$ cho lỗi 0–1 |
| $L_D(h)=\mathbb E_{Z\sim D}\,\ell(h,Z)$ | Rủi ro kì vọng | Kì vọng theo mẫu của nó viết $\mathbb E_S[L_D(A(S))]$ |
| $L_S(h)=\frac1m\sum_{i=1}^m\ell(h,Z_i)$ | Rủi ro thực nghiệm | |
| $A$, $A(S)$, $\hat h$ | Thuật toán học, hàm dự đoán học được | $\hat h$ khi $A$ là ERM |
| $\epsilon$, $\delta$ | Tham số độ chính xác và xác suất thất bại | |
| $m_{\mathcal H}(\epsilon,\delta)$ | Độ phức tạp mẫu | |
| $d$ | Chiều VC | Không dùng $d$ cho số chiều đặc trưng |
| $p$ | Số chiều đặc trưng | |
| $\Pi_{\mathcal H}(m)$ | Hàm tăng trưởng | Bài 03; cực đại trên bộ $m$ điểm (cho phép lặp) |
| $\mathcal H_C$ | Thu hẹp của $\mathcal H$ lên bộ điểm $C=(x_1,\ldots,x_k)$ | Bài 03; không dùng chỉ số $S$ cho lớp chọn theo mẫu (viết $\mathcal G_S$) |
| $\operatorname{VCdim}(\mathcal H)$ | Chiều VC khi có nhiều lớp | Bài 03; $d$ là kí hiệu chính |
| $m^{UC}_{\mathcal H}(\epsilon,\delta)$ | Hàm cỡ mẫu hội tụ đều của lớp | Bài 03 |
| $\rho_m$ | Bán kính VC $\sqrt{8\ln(4\Pi_{\mathcal H}(2m)/\delta)/m}$ | Bài 03; khác $r_m$ của Định lý 02.14 |
| $S'=(Z'_1,\ldots,Z'_m)$, $\sigma_i$ | Mẫu bóng, dấu ngẫu nhiên | Bài 03, chỉ trong chứng minh; $\sigma_i$ không phải độ lệch chuẩn |
| $\mathbf e_i$ | Véc-tơ đơn vị thứ $i$ của $\mathbb R^p$ | In đứng, khác số $e$ |
| (T5), (M) | Lớp cố định trước mẫu (có thể vô hạn); điều kiện đo được (lớp con đếm được xấp xỉ theo từng điểm) | Bài 03; (T4) là (T5) cộng hữu hạn |
| $L^*$ | Rủi ro tham chiếu | Bài 04; $L^*\le\inf_{h\in\mathcal H}L_D(h)$ |
| $\operatorname{opt}_S(\tilde h)$, $\tilde h$ | Sai số tối ưu thực nghiệm; đầu ra của một bộ giải bất kì | Bài 04 |
| $\mathcal H_k$, $d_k$, $q_k$ | Lớp thứ $k$ của một họ lớp, chiều VC của nó, trọng số | Bài 04; không dùng $w$ cho trọng số lớp |
| $\mathrm{rad}_{\mathcal H}(m,\delta')$, $\mathrm{pen}_k$ | Bán kính hội tụ đều; số hạng phạt $\mathrm{rad}_{\mathcal H_k}(m,\delta q_k)$ | Bài 04; không dùng $p_k$ (vì $p$ là số chiều đặc trưng) |
| $\tau$ | Dung sai của bài toán có phạt (SRM) | Bài 04; khác $\epsilon_{\mathrm{opt}}$ (một lớp) |
| $M(\epsilon,\delta,h)$ | Hàm cỡ mẫu của học không đều | Bài 04 |
| $f^*$, $\hat f_S$, $\bar f$, $\sigma^2(x)$ | Hàm hồi quy, ước lượng, dự đoán trung bình, phương sai nhiễu | Bài 04, chỉ với hàm lỗi bình phương; $\sigma^2(x)$ khác dấu ngẫu nhiên $\sigma_i$ |
| $\zeta_i$ | Nhiễu cộng của nhãn | Bài 04; không dùng $\xi$ hay $\epsilon_i$ |
| $\mathcal P_j$, $\hat f^{(j)}$, $x_0$ | Lớp đa thức một biến bậc không quá $j$, nghiệm bình phương tối thiểu trên nó, điểm kiểm tra | Bài 04 |
| $\hat h_k$, $(\hat k,\hat h)$, $k(h)$ | Nghiệm ERM trên $\mathcal H_k$; nghiệm SRM; chỉ số nhỏ nhất của lớp chứa $h$ | Bài 04 |
| $A_{\mathrm{SRM}}$, $M_k(\epsilon)$ | Thuật toán SRM với xác suất thất bại $1/m$; cỡ mẫu theo lớp | Bài 04 |
| $g_j$, $\hat g$ | Ứng viên, ứng viên được chọn theo mẫu xác thực | Bài 02, Bài 04 |
| $k_{\max}$, $\mathrm{pr}_k$ | Số lớp của một danh sách hữu hạn lớp; phép chiếu lên $k$ tọa độ đầu | Bài 04; $K$ giữ nghĩa số phần tử của một danh sách hữu hạn giả thuyết hay ứng viên; không dùng $\pi$ cho phép chiếu |
| $v^\star$ | Giá trị tối ưu của mục tiêu có phạt | Bài 04, chỉ trong Phụ lục A, B; $\varphi$ ở Bài 02, 04 là hàm phụ cục bộ trong chứng minh, từ Bài 05 là ánh xạ oracle |
| $V=(V_1,\ldots,V_{m_v})$, $m_v$, $L_V$ | Mẫu xác thực, cỡ mẫu xác thực, rủi ro trên mẫu xác thực | Bài 04; không dùng $n$, $T$ |
| (T6), (T7) | Họ lớp, bán kính và trọng số cố định trước mẫu; mẫu xác thực độc lập | Bài 04; (T5) là (T6) với một lớp |
| $T$, $\eta_t$ | Số vòng lặp, độ dài bước | Bài 05–08 |
| $G$, $\beta$, $\lambda$ | Hằng số Lipschitz hoặc cận gradient, hằng số trơn, hệ số chính quy hóa | |
| $R$ | Cận khoảng cách khởi tạo $\lVert w_1-u\rVert$ (hoặc $\lVert w_1-w^*\rVert$) | Bài 05; không dùng $R$ cho rủi ro |
| $w\in W\subset\mathbb R^p$; $\ell(w,z)$, $L_S(w)$, $L_D(w)$; $h_w$ | Véc-tơ tham số, tập tham số (khác rỗng, đóng, lồi); hàm lỗi và rủi ro theo tham số; hàm điểm số $h_w(x)=\langle w,x\rangle$ (hàm phân lớp tương ứng là $h_{w,0}=\mathbb 1[h_w\ge0]$, Định nghĩa 03.7) | Bài 05; $W$ ở Bài 02, 04 chỉ là biến cục bộ trong chứng minh |
| $\tilde y=2y-1$ | Nhãn $\pm1$ cho hàm lỗi bản lề, logistic | Bài 05; nhãn học phần là $\{0,1\}$ |
| $B$; $C_x$, $C_y$ | Bán kính của $W$ khi $W$ là quả cầu; cận của $\lVert x\rVert$, $\lvert y\rvert$ | Bài 05; Bài 04 dùng $B$ cho cận $\lvert Y\rvert$ (Nhận xét 04.18) |
| $F$, $\partial F(w)$, $w^*$, $u$ | Hàm mục tiêu; dưới vi phân; nghiệm tối ưu trên $W$ khi tồn tại; điểm so sánh bất kì trong $W$ | Bài 05 |
| $\operatorname{proj}_W$ | Phép chiếu Euclid lên $W$ | Bài 05; không dùng $\Pi_W$ (hàm tăng trưởng), $\pi$, $\mathrm{pr}_k$ |
| $\Xi$, $P_\xi$, $\xi_t$, $i_t$ | Tập giá trị và phân bố của nguồn ngẫu nhiên, lần rút thứ $t$, chỉ số rút từ $S$ | Bài 05; $P_\xi$ là phân bố của một lần rút ở Định nghĩa 05.10 và của cả dãy $\xi$ ở Định nghĩa 05.18 (ghi rõ tại chỗ) |
| $\varphi(w,\xi)$, $\psi(w)$ | Ánh xạ oracle (gradient ngẫu nhiên), trung bình của nó | Bài 05 |
| $\mathcal F_t$ | Lịch sử $\sigma(\xi_1,\ldots,\xi_t)$ | Bài 05; luôn có chỉ số, khác $F$ và lớp hàm $\mathcal F$ (Bài 07) |
| $g_t$; $v(w)$, $v_t$ | Gradient ngẫu nhiên tại bước $t$; quy tắc chọn dưới gradient, giá trị của nó trong GD | Bài 05; $g_j$ (ứng viên) không dùng cùng bài |
| $w_t$, $\bar w_T$, $\tilde w_T$, $w_{T+1}$ | Điểm lặp; trung bình đều; trung bình có trọng số; điểm lặp cuối | Bài 05 |
| (C), (G1), (G2) | Tính lồi của $F$ và $W$; oracle không chệch; mô-men bậc hai bị chặn | Bài 05; khác (O1), (O2) của Bài 01 |
| $\Delta_t$ | $\lVert w_t-u\rVert^2$ trong chứng minh | Bài 05, chỉ trong chứng minh |
| $U$; $k_{1:t-1}$; $\Phi$, $\bar\Phi$ | Tập mở (Mệnh đề 05.5); một lịch sử rời rạc; hàm trong bổ đề đóng băng | Bài 05, cục bộ; không dùng $A$ (thuật toán) hay $h$ (giả thuyết) cho các đối tượng này |
| $\theta$, $\gamma$, $q_i$, $a'$ | Điểm được chiếu (§5, Mệnh đề 05.13, Phụ lục A); hệ số nhân của độ dài bước (Ví dụ 05.8); giá trị trong câu ôn nhanh; véc-tơ phụ trong khai triển | Bài 05, cục bộ |
| $b$; $\varphi_b$; $G_F$, $\sigma^2$, $G_b$ | Kích thước lô; gradient lô; cận $\lVert\psi\rVert$, phương sai gradient ngẫu nhiên, $G_b^2=G_F^2+\sigma^2/b$ | Bài 05, mục lô nhỏ; $\sigma^2$ khác $\sigma^2(x)$ (Bài 04) và $\sigma_i$ (Bài 03); không dùng $b$ cho hệ số tự do trong Bài 05 |
| $\nu_t$ | Nhiễu gradient | Bài 05, bài tập mức sàn |
| $\delta'$ | Xác suất thất bại theo $\xi$ | Bài 05; khác $\delta$ (theo $S$) |
| $\operatorname{diam}(W)$ | Đường kính của $W$ | Bài 05 |
| $\epsilon_{\mathrm{stab}}(m)$ | Hệ số ổn định đều | Bài 06, 08; không dùng $\beta_m$ ($\beta$ là hằng số trơn, $\beta(m,\delta)$ của Bài 01) |
| $s^{(i)}$, $S^{(i)}$; $z'$, $Z'$ | Mẫu lân cận (thay quan sát thứ $i$ bằng $z'$ hay $Z'$); quan sát thay thế | Bài 06; không dùng cặp "$S,S'$" (mẫu bóng của Bài 03) |
| $F_{S,\lambda}$, $F_{s,\lambda}$; $\hat w_S$, $\hat w_s$, $\hat w_{S,\lambda}$ | Mục tiêu có chính quy hóa $L_S+\tfrac\lambda2\lVert\cdot\rVert^2$; nghiệm của nó | Bài 06; không dùng $F_S$ cho $L_S$ |
| $\lambda^*$ | Hệ số chính quy hóa làm nhỏ nhất cận, $2G/(B\sqrt m)$ | Bài 06 |
| $W_B$ | $\{u\in W:\lVert u\rVert\le B\}$, tập điểm so sánh có chuẩn không quá $B$ | Bài 06; ở đây $B$ là cận chuẩn của điểm so sánh, khác bán kính của $W$ khi $W$ là quả cầu |
| $\tilde w$ | Đầu ra của một thuật toán bất kì trên $W$ | Bài 06 (không chỉ số); khác $\tilde w_T$ của Bài 05 |
| $v(w,z)$ | Quy tắc dưới gradient đo được trên một quan sát | Bài 05 (Hệ quả 05.19), Bài 06 |
| (L) | Với mọi $z\in\mathcal Z$, $\ell(\cdot,z)$ là $G$-Lipschitz trên $W$ | Bài 06; khác (C), (G1), (G2), (T1)–(T7), (O1), (O2) |
| $\bar Y$, $c_t$, $q$ | Trung bình nhãn trong mẫu; hệ số của nhãn thứ $t$ trong $\bar w_T$; $1-2\eta$ | Bài 06, cục bộ (ví dụ câu hỏi mở đầu, Phụ lục D) |
| $G_\lambda$, $r_\lambda$ | Hằng số Lipschitz và bán kính nghiệm khi $W=\mathbb R^p$, dữ liệu bị chặn | Bài 06, chỉ bài tập |
| $\widehat{\mathfrak R}_S(\mathcal F)$ | Độ phức tạp Rademacher thực nghiệm | Bài 07 |
| $D_{\mathcal X}$ | Phân bố biên của $X$ | Bài 01 |
| $\eta(x)=\Pr(Y=1\mid X=x)$ | Xác suất có điều kiện của nhãn 1 | Luôn viết kèm đối số; $\eta$ không đối số là độ dài bước hằng (Bài 05), $\eta_t$ là độ dài bước thay đổi |
| $h_{\mathrm{Bayes}}$, $L_D^{\mathrm{Bayes}}$ | Hàm phân lớp tối ưu Bayes, rủi ro Bayes | Không dùng $f_D$ của UML (dễ lẫn với hàm gán nhãn $f$) |
| $\mathcal M_{\mathcal X}$ | Lớp mọi hàm phân lớp đo được trên $\mathcal X$ | Bài 01 |
| $\epsilon_{\mathrm{opt}}$ | Dung sai tối ưu của ERM xấp xỉ | Bài 01; $\operatorname{opt}_S$ ở Bài 04 |
| $\xi$, $A(S;\xi)$ | Nguồn ngẫu nhiên nội tại của thuật toán học | **Không dùng ở Bài 01** (người dùng 2026-10-30: Bài 01 viết $A(S)$, thuật toán tất định); đưa vào khi cần thuật toán ngẫu nhiên (từ Bài 05, SGD) |
| $M(\epsilon,\delta)$ | Hàm cỡ mẫu tồn tại trong định nghĩa học PAC | $m_A$, $m_{\mathcal H}$ dành cho giá trị nhỏ nhất, nhận giá trị trong $\mathbb N\cup\{\infty\}$; $\mathbb N=\{1,2,\ldots\}$ |
| $\beta(m,\delta)$ | Cận tổng quát hóa cho mọi thuật toán ERM | Bài 01; không dùng $\varepsilon$ (dễ lẫn với $\epsilon$) |
| $D_\eta$, $D_f$, $D_1$; $S_\eta$, $S_f$, $\tilde S_f$ | Các phân bố và mẫu của ví dụ sàng lọc (Bài 01) | Dùng trong Bài 01–02 và bài tập của hai bài (Bài 02 dùng lại ví dụ sàng lọc, quyết định của điều phối viên 2026-10-30); Bài 04 dẫn lại con số; giữ nguyên nghĩa của Bài 01 |
| $\mathbb E$, $\Pr$, $\mathbb 1[\cdot]$ | Kì vọng, xác suất, hàm chỉ thị | Ghi chỉ số phân bố khi có nhiều nguồn ngẫu nhiên: $\mathbb E_{S\sim D^m}$ |

Quy ước: giả thiết đo được cho các hàm lỗi và cận trên đúng được dùng khi cần; phân biệt cận dưới đúng (infimum) với giá trị nhỏ nhất (minimum) và chỉ giả sử đạt được khi dùng một nghiệm tối ưu cụ thể. Mỗi bài thêm kí hiệu riêng vào bảng kí hiệu của ghi chú, không đổi nghĩa kí hiệu trong bảng này.
