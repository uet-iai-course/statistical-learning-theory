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
| $\Pi_{\mathcal H}(m)$ | Hàm tăng trưởng | Bài 03 |
| $T$, $\eta_t$ | Số vòng lặp, độ dài bước | Bài 05–08 |
| $G$, $\beta$, $\lambda$ | Hằng số Lipschitz hoặc cận gradient, hằng số trơn, hệ số chính quy hóa | |
| $R$ | Cận khoảng cách khởi tạo $\lVert w_1-w^*\rVert$ | Bài 05; không dùng $R$ cho rủi ro |
| $\widehat{\mathfrak R}_S(\mathcal F)$ | Độ phức tạp Rademacher thực nghiệm | Bài 07 |
| $D_{\mathcal X}$ | Phân bố biên của $X$ | Bài 01 |
| $\eta(x)=\Pr(Y=1\mid X=x)$ | Xác suất có điều kiện của nhãn 1 | Luôn viết kèm đối số; khác độ dài bước $\eta_t$ (luôn có chỉ số) |
| $h_{\mathrm{Bayes}}$, $L_D^{\mathrm{Bayes}}$ | Hàm phân lớp tối ưu Bayes, rủi ro Bayes | Không dùng $f_D$ của UML (dễ lẫn với hàm gán nhãn $f$) |
| $\mathcal M_{\mathcal X}$ | Lớp mọi hàm phân lớp đo được trên $\mathcal X$ | Bài 01 |
| $\epsilon_{\mathrm{opt}}$ | Dung sai tối ưu của ERM xấp xỉ | Bài 01; $\operatorname{opt}_S$ ở Bài 04 |
| $\xi$, $A(S;\xi)$ | Nguồn ngẫu nhiên nội tại của thuật toán học | **Không dùng ở Bài 01** (người dùng 2026-10-30: Bài 01 viết $A(S)$, thuật toán tất định); đưa vào khi cần thuật toán ngẫu nhiên (từ Bài 05, SGD) |
| $M(\epsilon,\delta)$ | Hàm cỡ mẫu tồn tại trong định nghĩa học PAC | $m_A$, $m_{\mathcal H}$ dành cho giá trị nhỏ nhất, nhận giá trị trong $\mathbb N\cup\{\infty\}$; $\mathbb N=\{1,2,\ldots\}$ |
| $\beta(m,\delta)$ | Cận tổng quát hóa cho mọi thuật toán ERM | Bài 01; không dùng $\varepsilon$ (dễ lẫn với $\epsilon$) |
| $D_\eta$, $D_f$, $D_1$; $S_\eta$, $S_f$, $\tilde S_f$ | Các phân bố và mẫu của ví dụ sàng lọc (Bài 01) | Dùng trong Bài 01–02 và bài tập của hai bài (Bài 02 dùng lại ví dụ sàng lọc, quyết định của điều phối viên 2026-10-30); giữ nguyên nghĩa của Bài 01 |
| $\mathbb E$, $\Pr$, $\mathbb 1[\cdot]$ | Kì vọng, xác suất, hàm chỉ thị | Ghi chỉ số phân bố khi có nhiều nguồn ngẫu nhiên: $\mathbb E_{S\sim D^m}$ |

Quy ước: giả thiết đo được cho các hàm lỗi và cận trên đúng được dùng khi cần; phân biệt cận dưới đúng (infimum) với giá trị nhỏ nhất (minimum) và chỉ giả sử đạt được khi dùng một nghiệm tối ưu cụ thể. Mỗi bài thêm kí hiệu riêng vào bảng kí hiệu của ghi chú, không đổi nghĩa kí hiệu trong bảng này.
