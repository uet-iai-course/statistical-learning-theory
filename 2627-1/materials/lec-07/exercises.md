# Bài tập Bài 07 — Mạng nơ-ron, năng lực mô hình và tham số hóa thừa

Định nghĩa, kết quả và ví dụ được dẫn theo số hiệu của ghi chú Bài 07 và của các ghi chú Bài 01–06. Kí hiệu theo bảng kí hiệu chung và §2 của ghi chú, gồm:

- **§4–§5.** $\operatorname{ReLU}(t)=\max\{0,t\}$ (rectified linear unit); $f_\theta$ và $h_\theta=\mathbb 1[f_\theta\ge0]$: hàm điểm số (score function) và hàm phân lớp của mạng với tham số $\theta=(\Theta_1,b_1,\ldots,\Theta_J,b_J)$ (Định nghĩa 07.1); $J$, $N_j$: độ sâu, số nơ-ron của lớp nơ-ron thứ $j$; $P$: số tham số được huấn luyện; $\mathcal H_{J,N}$: lớp kiến trúc (architecture class, Định nghĩa 07.5).
- **§6–§7.** $\sigma_i$: biến Rademacher; $\widehat{\mathfrak R}(A)$, $\widehat{\mathfrak R}_S(\mathcal F)$, $\mathfrak R_m(\mathcal F)$: độ phức tạp Rademacher của một tập véc-tơ, thực nghiệm và tổng thể (Định nghĩa 07.7); $\tau_i$, $\operatorname{err}_\tau$: nhãn ngẫu nhiên và lỗi khớp (Mệnh đề 07.9); $\mathcal G$: lớp hàm lỗi giá trị trong $[0,1]$.
- **§8–§9.** $\mathcal F_B=\{h_w:\lVert w\rVert\le B\}$; $C_x$: cận của $\lVert x\rVert$; $\gamma$: lề; $L^{<\gamma}_S$: tỉ lệ vi phạm lề (margin violation rate, Định nghĩa 07.15); $\chi(x)$ và $\hat w$: véc-tơ đặc trưng ngẫu nhiên và nghiệm nội suy chuẩn nhỏ nhất (minimum-norm interpolant) của thí nghiệm mở đầu (Ví dụ 07.3).

Kí hiệu chỉ dùng trong một bài được đặt tên tại chỗ. Viết tắt: hạ gradient ngẫu nhiên (stochastic gradient descent, SGD), tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM).

Sáu bài đầu là bài gốc của học phần; Bài tập 07.6 có phần tính bắt buộc trên số đã chạy và phần thực nghiệm tùy chọn. Ba bài sau chọn từ mục bài tập §20.9 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* (Shalev-Shwartz và Ben-David, 2014; viết tắt UML); Bài tập 07.9 là bài tùy chọn với phát biểu đã sửa. UML viết $\tau_{\mathcal H}$ cho hàm tăng trưởng, lấy giá trị lớn nhất trên các tập $m$ điểm phân biệt, viết $\sigma$ cho hàm kích hoạt và $\rho$ cho hằng số Lipschitz; ở đây viết $\Pi_{\mathcal H}$ với bộ điểm cho phép lặp (Định nghĩa 03.11), $\varsigma$ và $G$.

## Bài tập gốc

### Bài tập 07.1 (Phép hoặc loại trừ bằng mạng ReLU và bằng hàm phân lớp afin)

**Mức độ:** khái niệm, chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 1; kiểm một mạng ReLU nhỏ biểu diễn đúng một hàm Boole, và tách việc phân lớp đúng bốn điểm khỏi hàm mà mạng tính trên cả mặt phẳng.

::: exercise Bài tập 07.1
Xét bốn quan sát của Ví dụ 07.1 và mạng $f_\theta$ của Mệnh đề 07.2.

**(a)** Mạng thứ hai có cùng kiến trúc ($p=2$, $J=2$, $N_1=2$, ReLU), với tham số $\theta_{\mathrm{II}}$ gồm
$$
\begin{aligned}
\Theta_1&=\begin{pmatrix}1&-1\\-1&1\end{pmatrix},\quad b_1=0,\\
\Theta_2&=(1,\,1),\quad b_2=-\tfrac12 .
\end{aligned}
$$
Tính $f_{\theta_{\mathrm{II}}}$ tại bốn điểm của $\{0,1\}^2$ và kiểm $h_{\theta_{\mathrm{II}}}(x)=x_1\oplus x_2$.

**(b)** Chứng minh trực tiếp bằng các bất đẳng thức tuyến tính rằng không hàm $h_{w,b}\in\mathcal H^2_{\mathrm{aff}}$ nào phân lớp đúng cả bốn quan sát. Nêu một hàm của lớp phân lớp đúng ba quan sát.

**(c)** Mô tả hai miền $\{x\in\mathbb R^2:f_\theta(x)\ge0\}$ và $\{x\in\mathbb R^2:f_{\theta_{\mathrm{II}}}(x)\ge0\}$. Hai mạng gán nhãn nào cho $x=(\tfrac12,\tfrac12)$?

**(d)** Với $x\in\{0,1\}^3$ và $s=x_1+x_2+x_3$, xét
$$
\begin{aligned}
&f_{\theta_{\mathrm{par}}}(x)=\operatorname{ReLU}(s)\\
&\quad-2\operatorname{ReLU}(s-1)\\
&\quad+2\operatorname{ReLU}(s-2)-\tfrac12 .
\end{aligned}
$$
Viết tham số $\theta_{\mathrm{par}}$ của một mạng độ sâu $2$ (Định nghĩa 07.1) có hàm điểm số này, đếm số tham số, và chứng minh $h_{\theta_{\mathrm{par}}}(x)=x_1\oplus x_2\oplus x_3$ tại cả tám điểm; hàm Boole này là *tính chẵn lẻ* (parity) của ba bit.
:::

::: hint Gợi ý 1
Phần (a). Tổng của $\operatorname{ReLU}(t)$ và $\operatorname{ReLU}(-t)$ là một hàm quen thuộc của $t$. Phần (b). Viết điều kiện "phân lớp đúng" tại mỗi điểm thành một bất đẳng thức theo $(w_1,w_2,b)$. Phần (c). Hàm $f_\theta$ chỉ phụ thuộc $x$ qua $s=x_1+x_2$.
:::

::: hint Gợi ý 2
Phần (b). Điểm $(0,0)$ cho $b<0$; cộng hai bất đẳng thức tại $(1,0)$ và $(0,1)$ rồi so với điều kiện tại $(1,1)$. Phần (c). Tính $f_\theta$ trên ba khoảng $s\le0$, $0\le s\le1$, $s\ge1$. Phần (d). Lớp ẩn có ba nơ-ron, mọi hàng của $\Theta_1$ bằng $(1,1,1)$.
:::

::: solution Lời giải Bài tập 07.1
**(a) Mạng thứ hai.**

**Bước 1: lớp ẩn.** $\Theta_1x+b_1=(x_1-x_2,\ x_2-x_1)^\top$. Một trong hai số $\pm(x_1-x_2)$ không âm và số kia không dương, nên
$$
\begin{aligned}
&f_{\theta_{\mathrm{II}}}(x)\\
&=\operatorname{ReLU}(x_1-x_2)\\
&\quad+\operatorname{ReLU}(x_2-x_1)-\tfrac12\\
&=\lvert x_1-x_2\rvert-\tfrac12 .
\end{aligned}
$$

**Bước 2: bốn giá trị.** Tại $(0,0)$ và $(1,1)$, $\lvert x_1-x_2\rvert=0$ và $f_{\theta_{\mathrm{II}}}=-\tfrac12$. Tại $(1,0)$ và $(0,1)$, $\lvert x_1-x_2\rvert=1$ và $f_{\theta_{\mathrm{II}}}=\tfrac12$. Do đó $h_{\theta_{\mathrm{II}}}(x)=1$ khi và chỉ khi đúng một tọa độ bằng $1$, tức $h_{\theta_{\mathrm{II}}}(x)=x_1\oplus x_2$. Bốn giá trị trùng với bốn giá trị của $f_\theta$ ở Mệnh đề 07.2.

**(b) Hàm phân lớp afin.**

**Bước 1: bốn điều kiện.** Với $h_{w,b}(x)=\mathbb 1[\langle w,x\rangle+b\ge0]$, phân lớp đúng bốn quan sát nghĩa là
$$
\begin{aligned}
(0,0)\mapsto0:&\quad b<0,\\
(1,0)\mapsto1:&\quad w_1+b\ge0,\\
(0,1)\mapsto1:&\quad w_2+b\ge0,\\
(1,1)\mapsto0:&\quad w_1+w_2+b<0 .
\end{aligned}
$$

**Bước 2: mâu thuẫn.** Cộng điều kiện thứ hai và thứ ba: $w_1+w_2+2b\ge0$, tức $w_1+w_2+b\ge-b$. Theo điều kiện thứ nhất, $-b>0$, nên $w_1+w_2+b>0$, trái với điều kiện thứ tư. Không có $(w,b)$ nào thỏa cả bốn điều kiện.

**Bước 3: ba quan sát.** Hàm $h_{w,b}$ với $w=(1,1)$, $b=-\tfrac12$ của Ví dụ 07.1, Bước 3, chỉ sai tại $(1,1)$, nên $L_S(h_{w,b})=\tfrac14$.

**(c) Hai miền.**

**Bước 1: $f_\theta$ theo $s$.** Theo Bước 1 của chứng minh Mệnh đề 07.2, $f_\theta(x)=\operatorname{ReLU}(s)-2\operatorname{ReLU}(s-1)-\tfrac12$ với mọi $x\in\mathbb R^2$. Với $s\ge1$, $f_\theta=s-2(s-1)-\tfrac12=\tfrac32-s$, nên trên ba khoảng của $s$:
$$
\begin{aligned}
s\le0:&\ f_\theta=-\tfrac12,\\
0\le s\le1:&\ f_\theta=s-\tfrac12,\\
s\ge1:&\ f_\theta=\tfrac32-s .
\end{aligned}
$$

**Bước 2: miền của $f_\theta$.** Do đó $f_\theta(x)\ge0$ khi và chỉ khi $\tfrac12\le x_1+x_2\le\tfrac32$: miền là dải đóng giữa hai đường thẳng song song $x_1+x_2=\tfrac12$ và $x_1+x_2=\tfrac32$. Hai điểm $(0,0)$ ($s=0$) và $(1,1)$ ($s=2$) nằm ngoài dải, hai điểm nhãn $1$ nằm trong.

**Bước 3: miền của $f_{\theta_{\mathrm{II}}}$.** Theo (a), $f_{\theta_{\mathrm{II}}}(x)\ge0$ khi và chỉ khi $\lvert x_1-x_2\rvert\ge\tfrac12$: miền là hợp của hai nửa mặt phẳng đóng $x_1-x_2\ge\tfrac12$ và $x_2-x_1\ge\tfrac12$.

**Bước 4: điểm giữa.** Tại $(\tfrac12,\tfrac12)$, $s=1$ nên $f_\theta=\tfrac12$ và $h_\theta=1$; còn $x_1-x_2=0$ nên $f_{\theta_{\mathrm{II}}}=-\tfrac12$ và $h_{\theta_{\mathrm{II}}}=0$. Hai mạng cùng kiến trúc, cùng phân lớp đúng bốn quan sát, nhưng gán nhãn khác nhau cho một điểm ngoài mẫu. Phân lớp đúng mẫu chỉ xác định hàm phân lớp trên các điểm của mẫu.

**(d) Tính chẵn lẻ của ba bit.**

**Bước 1: tham số.** Lấy $p=3$, $J=2$, $N_1=3$, ba hàng của $\Theta_1$ đều bằng $(1,1,1)$, $b_1=(0,-1,-2)^\top$, $\Theta_2=(1,-2,2)$ và $b_2=-\tfrac12$. Khi đó $\Theta_1x+b_1=(s,\ s-1,\ s-2)^\top$ và $f_{\theta_{\mathrm{par}}}$ là hàm của đề. Theo Định nghĩa 07.1, số tham số là $N_1(p+1)+1\cdot(N_1+1)=3\cdot4+4=16$.

**Bước 2: bốn giá trị của $s$.** Trên $\{0,1\}^3$, $s\in\{0,1,2,3\}$, và
$$
\begin{aligned}
s=0:&\quad0-0+0-\tfrac12=-\tfrac12,\\
s=1:&\quad1-0+0-\tfrac12=\tfrac12,\\
s=2:&\quad2-2+0-\tfrac12=-\tfrac12,\\
s=3:&\quad3-4+2-\tfrac12=\tfrac12 .
\end{aligned}
$$

**Bước 3: so với nhãn.** $f_{\theta_{\mathrm{par}}}(x)\ge0$ khi và chỉ khi $s\in\{1,3\}$, tức $s$ lẻ. Phép hoặc loại trừ của ba bit bằng $1$ khi và chỉ khi số bit bằng $1$ là lẻ, nên $h_{\theta_{\mathrm{par}}}(x)=x_1\oplus x_2\oplus x_3$ tại cả tám điểm (một điểm với $s=0$, ba với $s=1$, ba với $s=2$, một với $s=3$).

**Kiểm tra lại.** Với $D$ đều trên bốn quan sát của Ví dụ 07.1 và $L^*=0$, sai số xấp xỉ (Định nghĩa 04.1) của lớp kiến trúc $J=2$, $N_1=2$ bằng $0$ theo (a), còn của $\mathcal H^2_{\mathrm{aff}}$ bằng $\tfrac14$ theo (b). Giá trị $f_\theta(\tfrac12,\tfrac12)=\tfrac12$ ở (c) khớp đoạn sau Mệnh đề 07.2.
:::

### Bài tập 07.2 (Độ phức tạp Rademacher của lớp một phần tử và lớp hai phần tử)

**Mức độ:** tính toán, khái niệm. **Mục tiêu:** mục tiêu học tập 2; độ phức tạp Rademacher đến từ việc chọn hàm sau khi thấy bộ dấu, nối với lỗi khớp nhãn ngẫu nhiên; ý (b) đọc lại chứng minh Định lý 07.11 để thấy cái giá của cận phụ thuộc dữ liệu với một lớp nhỏ.

::: exercise Bài tập 07.2
**(a)** Chứng minh $\widehat{\mathfrak R}(\{a\})=0$ với mọi $a\in\mathbb R^m$. Với $m=3$ và $a=(0{,}3;0{,}7;0{,}2)$, lập bảng giá trị của $\sum_i\sigma_ia_i$ theo tám bộ dấu, nêu giá trị lớn nhất và trung bình của $\tfrac13\sum_i\sigma_ia_i$, và giải thích vì sao độ phức tạp bằng $0$ dù có bộ dấu cho giá trị dương.

**(b)** Cho một hàm $g:\mathcal Z\to[0,1]$ cố định trước mẫu. Chứng minh $\mathfrak R_m(\{g\})=0$ với mọi phân bố $D$. Viết Định lý 07.11(b) cho lớp $\{g\}$, tính số hạng tin cậy với $m=200$, $\delta=0{,}05$ và so với cận trên tin cậy của Hệ quả 02.10(c). Chỉ ra bước của chứng minh Định lý 07.11 làm cận yếu hơn với lớp một phần tử.

**(c)** Với hai véc-tơ $a,a'\in\mathbb R^m$, chứng minh
$$
\begin{aligned}
&\widehat{\mathfrak R}(\{a,a'\})\\
&=\frac1{2m}\,\mathbb E\Big\lvert\sum_{i=1}^m\sigma_i(a_i-a'_i)\Big\rvert .
\end{aligned}
$$
Áp dụng cho $a=(1,0,0)$, $a'=(0,1,1)$ và so với Ví dụ 07.4. Coi $a$, $a'$ là giá trị của hai hàm phân lớp trên ba điểm; tính $\mathbb E_\tau\min\operatorname{err}_\tau$ bằng cách liệt kê tám giá trị của $\tau$, và kiểm Mệnh đề 07.9(a).

**(d)** Quy ước có trị tuyệt đối (nhắc ở §6, sau Định nghĩa 07.7) dùng $\mathbb E_\sigma\sup_{a\in A}\big\lvert\tfrac1m\sum_i\sigma_ia_i\big\rvert$. Tính đại lượng này cho lớp một phần tử ở (a). Quy ước nào giữ được Bổ đề 07.8 với $c=1$?
:::

::: hint Gợi ý 1
Phần (a). Trên một tập một phần tử, không có phép chọn. Phần (b). Trên mỗi mẫu, $\widehat{\mathfrak R}_S(\{g\})$ là độ phức tạp của một tập một phần tử. Phần (c). Viết giá trị lớn nhất của hai số qua tổng và hiệu của chúng.
:::

::: hint Gợi ý 2
Phần (b). Trong Bước 4 của chứng minh Định lý 07.11, đếm số lần dùng bất đẳng thức McDiarmid và xác suất thất bại của mỗi lần; với lớp một phần tử, $\Psi=L_D(g)-L_S(g)$ có kì vọng $0$. Phần (c). $\max\{u,v\}=\tfrac{u+v}2+\tfrac{\lvert u-v\rvert}2$, và $(\sigma_1,-\sigma_2,-\sigma_3)$ có cùng phân bố với $(\sigma_1,\sigma_2,\sigma_3)$.
:::

::: solution Lời giải Bài tập 07.2
**(a) Lớp một phần tử.**

**Bước 1: không có phép chọn.** Cận trên đúng trên $\{a\}$ là giá trị tại $a$. Vì $\mathbb E\sigma_i=0$,
$$
\widehat{\mathfrak R}(\{a\})=\frac1m\sum_{i=1}^ma_i\,\mathbb E\sigma_i=0 .
$$

**Bước 2: bảng với $a=(0{,}3;0{,}7;0{,}2)$.**

| $\sigma$ | $\sum_i\sigma_ia_i$ |
|---|---|
| $(-,-,-)$ | $-1{,}2$ |
| $(-,-,+)$ | $-0{,}8$ |
| $(-,+,-)$ | $0{,}2$ |
| $(-,+,+)$ | $0{,}6$ |
| $(+,-,-)$ | $-0{,}6$ |
| $(+,-,+)$ | $-0{,}2$ |
| $(+,+,-)$ | $0{,}8$ |
| $(+,+,+)$ | $1{,}2$ |

Chia cho $3$, giá trị lớn nhất của $\tfrac13\sum_i\sigma_ia_i$ là $0{,}4$, tại $(+,+,+)$. Bộ dấu $\sigma$ và bộ dấu $-\sigma$ cho hai giá trị đối nhau, nên trung bình của tám giá trị bằng $0$.

**Bước 3: ý nghĩa.** Độ phức tạp lấy trung bình theo $\sigma$ của giá trị lớn nhất mà lớp đạt được với từng bộ dấu. Với một hàm, giá trị $0{,}4$ tại $(+,+,+)$ bị bù bởi $-0{,}4$ tại $(-,-,-)$. Một lớp có nhiều hàm chọn, với mỗi bộ dấu, một hàm cho giá trị lớn, và trung bình của các giá trị lớn nhất đó dương.

**(b) Lớp một phần tử trong Định lý 07.11.**

**Bước 1: độ phức tạp.** Trên mỗi mẫu, $\widehat{\mathfrak R}_S(\{g\})=\widehat{\mathfrak R}(\{(g(Z_1),\ldots,g(Z_m))\})=0$ theo (a). Do đó $\mathfrak R_m(\{g\})=\mathbb E_S0=0$ với mọi $D$.

**Bước 2: định lý.** Lớp $\{g\}$ cố định trước mẫu, nhận giá trị trong $[0,1]$ và thỏa (M) với $\mathcal G_0=\{g\}$. Định lý 07.11(b) cho: với xác suất ít nhất $1-\delta$,
$$
L_D(g)\le L_S(g)+3\sqrt{\frac{\ln(2/\delta)}{2m}} .
$$

**Bước 3: số.** Với $m=200$ và $\delta=0{,}05$,
$$
\begin{aligned}
3\sqrt{\ln40/400}&\le0{,}2881,\\
\sqrt{\ln20/400}&\le0{,}0866,
\end{aligned}
$$
với $\ln20\approx2{,}9957$. Dòng thứ nhất là số hạng tin cậy của Ví dụ 07.6, Bước 1; dòng thứ hai là cận trên tin cậy của Hệ quả 02.10(c). Cận của Định lý 07.11 lớn hơn khoảng $3{,}33$ lần.

**Bước 4: bước làm cận yếu đi.** Bước 4 của chứng minh dùng bất đẳng thức McDiarmid hai lần, mỗi lần với xác suất thất bại $\delta/2$: một lần cho $\Psi$, cho số hạng $t=\sqrt{\ln(2/\delta)/(2m)}$, và một lần để thay $\mathfrak R_m$ bằng $\widehat{\mathfrak R}_S$, thêm $2t$. Với lớp một phần tử, $\widehat{\mathfrak R}_S=\mathfrak R_m=0$ trên mọi mẫu, nên lần thứ hai thừa. Còn $\Psi=L_D(g)-L_S(g)$ có kì vọng $0$; một lần bất đẳng thức McDiarmid với xác suất thất bại $\delta$ và $c_i=1/m$ cho đúng Hệ quả 02.10(c), như đoạn sau Bổ đề 07.10. Thừa số $3$ và $\ln(2/\delta)$ là giá của một cận phụ thuộc dữ liệu đúng cho mọi lớp.

**(c) Lớp hai phần tử.**

**Bước 1: công thức.** Đặt $u=\tfrac1m\sum_i\sigma_ia_i$ và $v=\tfrac1m\sum_i\sigma_ia'_i$. Vì $\max\{u,v\}=\tfrac{u+v}2+\tfrac{\lvert u-v\rvert}2$ và $\mathbb E(u+v)=0$,
$$
\begin{aligned}
&\widehat{\mathfrak R}(\{a,a'\})=\mathbb E\max\{u,v\}\\
&=\tfrac12\mathbb E\lvert u-v\rvert\\
&=\tfrac1{2m}\mathbb E\big\lvert\textstyle\sum_i\sigma_i(a_i-a'_i)\big\rvert .
\end{aligned}
$$

**Bước 2: áp dụng.** $a-a'=(1,-1,-1)$, nên tổng trong trị tuyệt đối là $\sigma_1-\sigma_2-\sigma_3$, cùng phân bố với $\sigma_1+\sigma_2+\sigma_3$. Theo câu ôn nhanh 1, kì vọng của trị tuyệt đối bằng $1{,}5$, nên
$$
\widehat{\mathfrak R}(\{a,a'\})=\frac{1{,}5}{2\cdot3}=\frac14,
$$
đúng giá trị ở Bước 2 của Ví dụ 07.4.

**Bước 3: nhãn ngẫu nhiên.** Gọi $h_a$, $h_{a'}$ là hai hàm phân lớp có giá trị $a$, $a'$ trên ba điểm. Bảng ghi số điểm sai của mỗi hàm theo $\tau=(\tau_1,\tau_2,\tau_3)$:

| $\tau$ | $h_a$ | $h_{a'}$ | nhỏ nhất |
|---|---|---|---|
| $(0,0,0)$ | $1$ | $2$ | $1$ |
| $(0,0,1)$ | $2$ | $1$ | $1$ |
| $(0,1,0)$ | $2$ | $1$ | $1$ |
| $(0,1,1)$ | $3$ | $0$ | $0$ |
| $(1,0,0)$ | $0$ | $3$ | $0$ |
| $(1,0,1)$ | $1$ | $2$ | $1$ |
| $(1,1,0)$ | $1$ | $2$ | $1$ |
| $(1,1,1)$ | $2$ | $1$ | $1$ |

Tổng cột cuối bằng $6$, nên $\mathbb E_\tau\min\operatorname{err}_\tau=6/(8\cdot3)=\tfrac14$. Mệnh đề 07.9(a) cho $\widehat{\mathfrak R}=\tfrac12-\tfrac14=\tfrac14$, khớp Bước 2. Hai hàm khớp nhãn ngẫu nhiên với lỗi trung bình $\tfrac14$, thấp hơn mức $\tfrac12$ của một hàm cố định; phần chênh $\tfrac14$ bằng độ phức tạp.

**(d) Quy ước có trị tuyệt đối.**

**Bước 1: tính.** Theo bảng ở (a), bốn giá trị của $\lvert\sum_i\sigma_ia_i\rvert$ là $1{,}2$; $0{,}8$; $0{,}2$; $0{,}6$, mỗi giá trị xuất hiện hai lần. Do đó
$$
\begin{aligned}
\mathbb E\Big\lvert\tfrac13\textstyle\sum_i\sigma_ia_i\Big\rvert&=\frac{2\cdot2{,}8}{8\cdot3}\\
&=\frac7{30}\approx0{,}2333 .
\end{aligned}
$$

**Bước 2: tính bất biến khi dịch.** Với trị tuyệt đối, tập $\{0\}$ cho $0$, còn $\{a\}=\{0\}+a$ cho $0{,}2333$: dịch bởi một véc-tơ làm đổi giá trị, nên Bổ đề 07.8 với $c=1$, $\bar a=a$ không còn đúng. Quy ước của học phần cho $0$ với mọi lớp một phần tử, giữ được Bổ đề 07.8 và cách hiểu ở Bước 3 của (a). Nhờ đó, cộng một hằng số vào hàm lỗi không đổi độ phức tạp (Nhận xét 07.12).

**Kiểm tra lại.** Theo bất đẳng thức Jensen, $\mathbb E\lvert\sigma_1+\sigma_2+\sigma_3\rvert=1{,}5\le\sqrt3\approx1{,}7321$ (câu ôn nhanh 1), nên giá trị $\tfrac14$ ở (c) không vượt $\sqrt3/6\approx0{,}2887$; nó cũng không vượt $\tfrac12$ (Mệnh đề 07.9(c)).
:::

### Bài tập 07.3 (Cận độ phức tạp Rademacher cho lớp tuyến tính bị chặn theo chuẩn)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 4; mở rộng chứng minh Mệnh đề 07.13 cho lớp có hệ số tự do, chỉ chỗ dùng từng giả thiết, xác định khi nào cận chặt, và tính cận theo lề.

::: exercise Bài tập 07.3
Cho $B>0$, $B_0\ge0$ và bộ điểm cố định $x_1,\ldots,x_m\in\mathbb R^p$ với $\lVert x_i\rVert\le C_x$. Xét lớp hàm điểm số afin
$$
\begin{aligned}
\mathcal F_{B,B_0}=\{&x\mapsto\langle w,x\rangle+b:\\
&\lVert w\rVert\le B,\ \lvert b\rvert\le B_0\};
\end{aligned}
$$
với $B_0=0$, đây là lớp $\mathcal F_B$ của Mệnh đề 07.13.

**(a)** Chứng minh
$$
\widehat{\mathfrak R}_{x_{1:m}}(\mathcal F_{B,B_0})\le\frac{BC_x+B_0}{\sqrt m}.
$$
Ghi tại mỗi bước giả thiết được dùng: quả cầu Euclid, tính độc lập và kì vọng $0$ của các $\sigma_i$, cận $C_x$.

**(b)** Cách thứ hai thêm vào mỗi $x_i$ một tọa độ bằng $1$ rồi áp dụng Mệnh đề 07.13 trong $\mathbb R^{p+1}$. Viết cận thu được, chứng minh nó không nhỏ hơn cận ở (a), và tính hai cận với $B=2$, $B_0=1$, $C_x=1$, $m=2500$.

**(c)** Với $B_0=0$, chứng minh bất đẳng thức thứ nhất của Mệnh đề 07.13 là đẳng thức khi và chỉ khi $\langle x_i,x_j\rangle=0$ với mọi $i\ne j$. Kiểm với $x_1=(1,0)$, $x_2=(1,1)$.

**(d)** Nhúng các điểm vào $\mathbb R^{p'}$, $p'>p$, bằng cách thêm $p'-p$ tọa độ $0$. Chứng minh độ phức tạp của $\mathcal F_B$ trên các điểm mới bằng độ phức tạp trên các điểm cũ, và so với chiều VC của $\mathcal H^p_{\mathrm{hom}}$ và $\mathcal H^{p'}_{\mathrm{hom}}$.

**(e)** Trong ứng dụng hồi quy logistic của Bài 05 ($m=10^6$, $\lVert x\rVert\le1$, $B=5$), tính cận của $\widehat{\mathfrak R}_S(\mathcal F_5)$. Với $\delta=0{,}05$, tính số hạng phạt của Hệ quả 07.16 với $\gamma=1$, và cận cho hàm lỗi logistic ở Bước 4 của Ví dụ 07.11.
:::

::: hint Gợi ý 1
Phần (a). Hai tham số $w$ và $b$ chạy độc lập. Phần (c). Xem bước nào trong chứng minh Mệnh đề 07.13 có thể là bất đẳng thức thực sự, và khi nào bước đó thành đẳng thức.
:::

::: hint Gợi ý 2
Phần (a). Phần theo $b$ của cận trên đúng bằng $\tfrac{B_0}m\lvert\sum_i\sigma_i\rvert$, và $\mathbb E\lvert\sum_i\sigma_i\rvert\le\sqrt{\mathbb E(\sum_i\sigma_i)^2}$. Phần (c). Bất đẳng thức Jensen cho hàm lõm chặt $t\mapsto\sqrt t$ là đẳng thức khi và chỉ khi $\lVert v_\sigma\rVert^2$ không phụ thuộc $\sigma$; tính mô-men bậc hai của $\lVert v_\sigma\rVert^2-\sum_i\lVert x_i\rVert^2$.
:::

::: solution Lời giải Bài tập 07.3
**(a) Lớp có hệ số tự do.** Đặt $v_\sigma=\sum_{i=1}^m\sigma_ix_i\in\mathbb R^p$.

**Bước 1: tách cận trên đúng.** Tập tham số là tích của quả cầu $\{\lVert w\rVert\le B\}$ và đoạn $\{\lvert b\rvert\le B_0\}$, nên với mỗi $\sigma$,
$$
\begin{aligned}
&\sup_{w,b}\tfrac1m\textstyle\sum_i\sigma_i\big(\langle w,x_i\rangle+b\big)\\
&=\sup_{\lVert w\rVert\le B}\tfrac1m\langle w,v_\sigma\rangle\\
&\quad+\sup_{\lvert b\rvert\le B_0}\tfrac bm\textstyle\sum_i\sigma_i .
\end{aligned}
$$

**Bước 2: hai cận trên đúng; quả cầu Euclid.** Theo bất đẳng thức Cauchy–Schwarz, như Bước 1 của chứng minh Mệnh đề 07.13, số hạng đầu bằng $\tfrac Bm\lVert v_\sigma\rVert$; quả cầu Euclid được dùng ở đây. Số hạng sau bằng $\tfrac{B_0}m\lvert\sum_i\sigma_i\rvert$, đạt tại $b=\pm B_0$ cùng dấu với $\sum_i\sigma_i$.

**Bước 3: bất đẳng thức Jensen; tính độc lập và kì vọng $0$.** Theo Bước 2–3 của chứng minh Mệnh đề 07.13, $\mathbb E\lVert v_\sigma\rVert\le\sqrt{\sum_i\lVert x_i\rVert^2}$. Cùng lập luận cho tổng các dấu: vì $\mathbb E[\sigma_i\sigma_j]=0$ với $i\ne j$ và $\sigma_i^2=1$,
$$
\begin{aligned}
\mathbb E\big\lvert\textstyle\sum_i\sigma_i\big\rvert&\le\sqrt{\mathbb E\big(\textstyle\sum_i\sigma_i\big)^2}\\
&=\sqrt m .
\end{aligned}
$$
Tính độc lập và kì vọng $0$ của các $\sigma_i$ được dùng ở hai số hạng chéo.

**Bước 4: cận dữ liệu.** Lấy kì vọng hai vế của Bước 1 và dùng $\lVert x_i\rVert\le C_x$:
$$
\begin{aligned}
&\widehat{\mathfrak R}_{x_{1:m}}(\mathcal F_{B,B_0})\\
&\le\frac Bm\sqrt{mC_x^2}+\frac{B_0\sqrt m}m\\
&=\frac{BC_x+B_0}{\sqrt m}.
\end{aligned}
$$

**(b) Thêm tọa độ hằng.**

**Bước 1: bao hàm.** Đặt $\tilde x_i=(x_i,1)$, nên $\lVert\tilde x_i\rVert\le\sqrt{C_x^2+1}$. Với $\lVert w\rVert\le B$, $\lvert b\rvert\le B_0$, ta có $\langle w,x_i\rangle+b=\langle(w,b),\tilde x_i\rangle$ và $\lVert(w,b)\rVert\le\sqrt{B^2+B_0^2}$. Tập véc-tơ giá trị của $\mathcal F_{B,B_0}$ trên các $x_i$ nằm trong tập véc-tơ giá trị của lớp tuyến tính bán kính $\sqrt{B^2+B_0^2}$ trên các $\tilde x_i$. Cận trên đúng trên tập lớn hơn không nhỏ hơn, nên Mệnh đề 07.13 cho
$$
\begin{aligned}
&\widehat{\mathfrak R}_{x_{1:m}}(\mathcal F_{B,B_0})\\
&\le\frac{\sqrt{B^2+B_0^2}\,\sqrt{C_x^2+1}}{\sqrt m}.
\end{aligned}
$$

**Bước 2: so sánh.** Theo bất đẳng thức Cauchy–Schwarz cho hai véc-tơ $(B,B_0)$ và $(C_x,1)$ trong $\mathbb R^2$, $BC_x+B_0\le\sqrt{B^2+B_0^2}\sqrt{C_x^2+1}$, nên cận ở (a) không lớn hơn.

**Bước 3: số.** Với $B=2$, $B_0=1$, $C_x=1$, $\sqrt m=50$, cận (a) bằng $(2+1)/50=0{,}06$, còn cận (b) bằng
$$
\frac{\sqrt5\cdot\sqrt2}{50}=\frac{\sqrt{10}}{50}\le0{,}0633 .
$$

**(c) Trường hợp đẳng thức.**

**Bước 1: chỉ có một bất đẳng thức thực sự.** Trong chứng minh Mệnh đề 07.13, Bước 1 và Bước 3 là đẳng thức. Do đó bất đẳng thức thứ nhất là đẳng thức khi và chỉ khi bất đẳng thức Jensen ở Bước 2 là đẳng thức: $\mathbb E\sqrt Y=\sqrt{\mathbb EY}$ với $Y=\lVert v_\sigma\rVert^2$. Hàm $t\mapsto\sqrt t$ lõm chặt trên $[0,\infty)$ và mỗi bộ dấu có xác suất $2^{-m}>0$, nên đẳng thức xảy ra khi và chỉ khi $Y$ như nhau với mọi $\sigma$.

**Bước 2: phần phụ thuộc $\sigma$.** Khai triển bình phương chuẩn,
$$
\begin{aligned}
&Y-\textstyle\sum_i\lVert x_i\rVert^2\\
&=2\textstyle\sum_{i<j}\sigma_i\sigma_j\langle x_i,x_j\rangle .
\end{aligned}
$$
Tổng bên phải có kì vọng $0$, nên $Y$ không đổi khi và chỉ khi tổng này bằng $0$ với mọi $\sigma$, tức khi và chỉ khi mô-men bậc hai của nó bằng $0$.

**Bước 3: mô-men bậc hai.** Với hai cặp $i<j$ và $k<l$, $\mathbb E[\sigma_i\sigma_j\sigma_k\sigma_l]=1$ nếu $\{i,j\}=\{k,l\}$; nếu không, một chỉ số xuất hiện đúng một lần và kì vọng bằng $0$ do tính độc lập. Do đó mô-men bậc hai của tổng ở Bước 2 bằng $\sum_{i<j}\langle x_i,x_j\rangle^2$, bằng $0$ khi và chỉ khi mọi $\langle x_i,x_j\rangle=0$.

**Bước 4: kiểm với $x_1=(1,0)$, $x_2=(1,1)$.** Ở đây $\langle x_1,x_2\rangle=1\ne0$. Véc-tơ $v_\sigma$ là $\pm(2,1)$ hoặc $\pm(0,1)$, với chuẩn $\sqrt5$ hoặc $1$, mỗi trường hợp xác suất $\tfrac12$. Do đó
$$
\widehat{\mathfrak R}=\frac B2\cdot\frac{1+\sqrt5}2\approx0{,}8090B,
$$
còn cận là $\tfrac B2\sqrt3\approx0{,}8660B$: bất đẳng thức là thực sự.

**(d) Nhúng vào không gian lớn hơn.**

**Bước 1: cùng tập véc-tơ giá trị.** Gọi $\hat x_i=(x_i,0)\in\mathbb R^{p'}$ và viết $w=(w',w'')$ với $w'\in\mathbb R^p$. Khi đó $\langle w,\hat x_i\rangle=\langle w',x_i\rangle$. Nếu $\lVert w\rVert\le B$ thì $\lVert w'\rVert\le B$; ngược lại, mỗi $w'$ với $\lVert w'\rVert\le B$ cho $w=(w',0)$ với $\lVert w\rVert\le B$. Hai tập véc-tơ giá trị trùng nhau, nên hai độ phức tạp bằng nhau.

**Bước 2: so với chiều VC.** Theo Mệnh đề 03.9(b), $\mathcal H^p_{\mathrm{hom}}$ có chiều VC $p$ và $\mathcal H^{p'}_{\mathrm{hom}}$ có chiều VC $p'$. Chiều VC tăng theo số chiều của không gian, còn độ phức tạp của $\mathcal F_B$ trên các điểm cho trước và cận $BC_x/\sqrt m$ không đổi.

**(e) Ứng dụng hồi quy logistic.**

**Bước 1: độ phức tạp.** Theo Mệnh đề 07.13, $\widehat{\mathfrak R}_S(\mathcal F_5)\le5\cdot1/\sqrt{10^6}=0{,}005$.

**Bước 2: cận theo lề.** Với $\gamma=1$, số hạng Rademacher là $2\cdot5\cdot1/(1\cdot1000)=0{,}01$. Số hạng tin cậy là
$$
3\sqrt{\frac{\ln40}{2\cdot10^6}}\approx0{,}004074 .
$$
Theo Hệ quả 07.16, với xác suất ít nhất $0{,}95$, đồng thời cho mọi $\lVert w\rVert\le5$,
$$
L_D(h_{w,0})\le L^{<1}_S(h_w)+0{,}0141 .
$$

**Bước 3: hàm lỗi logistic.** Với $K=\ln(1+e^5)\approx5{,}0067$, Bước 4 của Ví dụ 07.11 cho số hạng
$$
\begin{aligned}
&\frac{2BC_x}{\sqrt m}+3K\sqrt{\frac{\ln40}{2\cdot10^6}}\\
&=0{,}01+3\cdot5{,}0067\cdot0{,}001358\\
&\le0{,}0304 .
\end{aligned}
$$
Do đó, với xác suất ít nhất $0{,}95$, rủi ro logistic thỏa $L_D(w)\le L_S(w)+0{,}0304$ đồng thời cho mọi $\lVert w\rVert\le5$.

**Kiểm tra lại.** Với $m=1$, cận trên đúng ở Bước 1 của (a) bằng $B\lVert x_1\rVert+B_0$ với cả hai dấu của $\sigma_1$ (lấy $w=\pm Bx_1/\lVert x_1\rVert$, $b=\pm B_0$), nên $\widehat{\mathfrak R}=B\lVert x_1\rVert+B_0$, đúng bằng cận (a) với $C_x=\lVert x_1\rVert$.
:::

### Bài tập 07.4 (Số tham số, cỡ mẫu và lỗi kiểm tra)

**Mức độ:** khái niệm, kiểm tra giả thiết, tính toán. **Mục tiêu:** mục tiêu học tập 3, 5; tỉ số $P/m$ không quyết định lỗi kiểm tra hay sự tồn tại của một bảo đảm; chỗ dùng từng giả thiết của Định lý 07.11.

::: exercise Bài tập 07.4
**(a)** Xét hai lượt huấn luyện của câu hỏi mở đầu, với nhãn thật và với nhãn hoán vị (permuted labels), và sáu đại lượng: $P$, $P/m$, độ phức tạp Rademacher thực nghiệm của lớp kiến trúc trên các điểm huấn luyện, lỗi huấn luyện, lỗi kiểm tra, $\lVert\hat w\rVert$. Theo câu hỏi mở đầu và các Ví dụ 07.3, 07.5, 07.10, xếp mỗi đại lượng vào nhóm như nhau hay nhóm khác nhau, rồi rút ra kết luận về vai trò của $P/m$.

**(b)** Lớp của Nhận xét 03.10(iii) được viết với $p=10^6$ tham số. Với mẫu $S\sim D^m$ theo (T1), $m=200$, $\delta=0{,}05$ và hàm lỗi 0–1, kiểm các giả thiết của Định lý 02.14 và tính bán kính $r_m$ của phần (a). Cách tham số hóa này có tham số hóa thừa so với $m=200$ theo Định nghĩa 07.4 không?

**(c)** Lớp $\mathcal H_{\sin}$ của Nhận xét 03.10(ii) có $P=1$. Trên một mẫu có $200$ đầu vào $2^{-1},\ldots,2^{-200}$, tính $\mathbb E_\tau\min_{h\in\mathcal H_{\sin}}\operatorname{err}_\tau(h)$, và vế phải của Định lý 07.11(b) với $\delta=0{,}05$ cho một nghiệm ERM, với nhãn bất kì.

**(d)** Định lý 07.11 cần ba giả thiết: mẫu theo (T1), hàm lỗi nhận giá trị trong $[0,1]$, lớp hàm lỗi cố định trước mẫu. Với mỗi giả thiết, nêu một bước của chứng minh dùng nó, và một tình huống trong Bài 07 mà giả thiết đó không thỏa.
:::

::: hint Gợi ý 1
Phần (a). Xếp mỗi đại lượng vào một trong bốn nhóm: kiến trúc, lớp, mẫu, hàm do huấn luyện chọn. Phần (b). Đếm số hàm phân biệt của lớp, không đếm tham số. Phần (d). Với mỗi giả thiết, tìm một đẳng thức hay một cận trong chứng minh sẽ sai khi bỏ giả thiết đó.
:::

::: hint Gợi ý 2
Phần (b). Lớp có $K=3$ hàm, và $r_m=\sqrt{\ln(2K/\delta)/(2m)}$. Phần (c). Lớp tách trọn bộ điểm (Ví dụ 07.5, Bước 2); dùng Mệnh đề 07.9(a), (b). Phần (d). Tiêu đề mỗi bước trong chứng minh Định lý 07.11 ghi giả thiết dùng ở bước đó; tìm các tình huống vi phạm trong Ví dụ 07.6, Ví dụ 07.11 và Nhận xét 07.17.
:::

::: solution Lời giải Bài tập 07.4
**(a) Hai lượt huấn luyện của thí nghiệm.**

**Bước 1: các đại lượng như nhau.** Kiến trúc, lớp ẩn và các điểm huấn luyện như nhau, nên $P=2000$ và $P/m=10$ (Ví dụ 07.3, Bước 2). Lớp kiến trúc tách trọn $200$ điểm huấn luyện (Ví dụ 07.3, Bước 3), nên độ phức tạp Rademacher thực nghiệm của nó bằng $\tfrac12$, và theo Mệnh đề 07.9(b), lớp hàm lỗi 0–1 có cùng giá trị với cả hai loại nhãn (Ví dụ 07.5, Bước 1). Lỗi huấn luyện bằng $0$ trong cả hai lượt.

**Bước 2: các đại lượng khác nhau.** Lỗi kiểm tra trung bình là $0{,}023$ với nhãn thật và $0{,}501$ với nhãn hoán vị. Chuẩn $\lVert\hat w\rVert$ trung bình là $916$ và $10\,853$ (Ví dụ 07.10, Bước 2). Cả hai là đại lượng của hàm do huấn luyện chọn.

**Bước 3: kết luận.** $P/m$ và độ phức tạp của lớp kiến trúc chỉ phụ thuộc kiến trúc và các điểm, nên không phân biệt được hai lượt; lỗi kiểm tra khác nhau gần $22$ lần. Riêng $P/m$ không quyết định lỗi kiểm tra.

**(b) Nhiều tham số, ba hàm.**

**Bước 1: giả thiết.** Theo Nhận xét 03.10(iii), lớp chỉ gồm ba hàm $\mathbb 1[x\ge0]$, $\mathbb 1[x\le0]$ và hằng $1$, theo dấu của $w_1+\cdots+w_p$; lớp cố định trước mẫu, nên thỏa (T4) với $K=3$. Hàm lỗi 0–1 thỏa (T2) và (T3). Mẫu thỏa (T1) theo đề.

**Bước 2: bán kính.** Theo Định lý 02.14(a),
$$
\begin{aligned}
r_m&=\sqrt{\frac{\ln(2\cdot3/0{,}05)}{2\cdot200}}\\
&=\sqrt{\frac{\ln120}{400}}\le0{,}1095,
\end{aligned}
$$
với $\ln120\approx4{,}7875$.

**Bước 3: tham số hóa thừa.** $P=10^6>m=200$, nên cách tham số hóa này là tham số hóa thừa, với $P/m=5000$. Dù vậy, với xác suất ít nhất $0{,}95$, mọi hàm của lớp, kể cả nghiệm ERM, có $\lvert L_S-L_D\rvert\le0{,}1095$. Tham số hóa thừa không ngăn một bảo đảm.

**(c) Một tham số, không có bảo đảm.**

**Bước 1: nhãn ngẫu nhiên.** Theo Ví dụ 07.5, Bước 2, $\mathcal H_{\sin}$ tách trọn $\{2^{-1},\ldots,2^{-200}\}$, nên với mọi $\tau$ có một hàm của lớp khớp đúng cả $200$ nhãn: $\mathbb E_\tau\min\operatorname{err}_\tau=0$. Theo Mệnh đề 07.9(a), độ phức tạp của lớp trên các điểm này bằng $\tfrac12$; theo (b) của mệnh đề, lớp hàm lỗi 0–1 có cùng giá trị với mọi nhãn.

**Bước 2: vế phải.** Một nghiệm ERM có $L_S=0$ với mọi nhãn, nên theo Ví dụ 07.6, Bước 1, vế phải của Định lý 07.11(b) là
$$
\begin{aligned}
&0+2\cdot\tfrac12+0{,}2881\\
&=1{,}2881>1 .
\end{aligned}
$$
Cận không cho thông tin, dù $P/m=0{,}005$.

**Bước 3: kết luận.** Theo (b) và (c), $P/m$ lớn không ngăn một bảo đảm, và $P/m$ nhỏ không đủ cho một bảo đảm. Đại lượng cần đo là năng lực của lớp chứa hàm được chọn.

**(d) Ba giả thiết của Định lý 07.11.**

- **Mẫu theo (T1).** Dùng ở Bước 1 (mẫu bóng có cùng phân bố, Mệnh đề 01.7), Bước 2 (phép đổi chỗ $Z_i\leftrightarrow Z'_i$ không đổi phân bố) và Bước 4 (bất đẳng thức McDiarmid cần các quan sát độc lập). Không thỏa với nhãn hoán vị: tổng các nhãn hoán vị bằng tổng các nhãn thật, nên các cặp $(x_i,y_i)$ không độc lập (Ví dụ 07.6, Bước 3).
- **Giá trị trong $[0,1]$.** Dùng ở Bước 3: thay một quan sát làm mỗi $L_s(g)$ đổi không quá $1/m$, cho hằng số sai phân $c_i=1/m$. Không thỏa khi đặt lớp điểm số, hay hàm lỗi logistic trên $\mathbb R^p$, vào chỗ lớp hàm lỗi (Ví dụ 07.11).
- **Lớp cố định trước mẫu.** Dùng ở Bước 1: với mỗi $g$ cố định, $L_D(g)=\mathbb E_{S'}L_{S'}(g)$, và cận trên đúng lấy trên một tập hàm không phụ thuộc $S$. Không thỏa khi lấy $B=\lVert\hat w\rVert$ hay $\gamma$ bằng lề nhỏ nhất sau khi xem mẫu (Nhận xét 07.17, Ví dụ 07.10, Bước 3).

**Kiểm tra lại.** Ở (b), cận một phía của Định lý 02.14(b) là $\sqrt{\ln60/400}\le0{,}1012$, nhỏ hơn $r_m$ vì không cần chia $\delta$ cho hai phía. Ở (c), vế phải lớn hơn $1$ với mọi nhãn, kể cả nhãn hoàn toàn ngẫu nhiên.
:::

### Bài tập 07.5 (Xấp xỉ phổ quát và việc tìm một mạng tốt bằng SGD)

**Mức độ:** khái niệm, chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 1; một kết quả về biểu diễn chỉ chặn sai số xấp xỉ, không bảo đảm rằng phép huấn luyện tìm được hàm tốt.

::: exercise Bài tập 07.5
Xét bốn quan sát của Ví dụ 07.1 với nhãn $\tilde y\in\{\pm1\}$, kiến trúc $p=2$, $J=2$, $N_1=2$, ReLU, và hàm mục tiêu
$$
F(\theta)=\frac14\sum_{i=1}^4\Big(f_\theta(x_i)-\frac{\tilde y_i}2\Big)^2 .
$$

**(a)** Chứng minh $F(\theta)=0$ tại tham số $\theta$ của Mệnh đề 07.2. Suy ra sai số xấp xỉ (Định nghĩa 04.1) của lớp kiến trúc với hàm lỗi 0–1, $D$ đều trên bốn quan sát và $L^*=0$.

**(b)** Chạy hạ gradient trên $F$, khởi tạo tại $\theta=0$ (mọi ma trận trọng số và hệ số tự do bằng $0$), với độ dài bước $\eta>0$ bất kì và quy ước bất kì cho đạo hàm của ReLU tại $0$. Chứng minh rằng $\Theta_1$, $b_1$, $\Theta_2$ bằng $0$ ở mọi bước, rồi tính lỗi 0–1 trên bốn quan sát của hàm phân lớp trả về. Kết luận còn đúng với SGD rút một quan sát mỗi bước không?

**(c)** Gọi $\theta_{\mathrm{swap}}$ là tham số thu được từ $\theta$ của Mệnh đề 07.2 khi đổi chỗ hai nơ-ron ẩn (hai hàng của $\Theta_1$, hai tọa độ của $b_1$, hai tọa độ của $\Theta_2$). Chứng minh $F(\theta_{\mathrm{swap}})=0$, tính $F$ tại trung điểm $\theta_{\mathrm{mid}}=\tfrac12(\theta+\theta_{\mathrm{swap}})$, và kết luận về tính lồi của $F$.

**(d)** Viết ba số hạng của Mệnh đề 04.3 cho hàm phân lớp trả về ở (b). Số hạng nào tạo ra toàn bộ rủi ro vượt mức? Một kết quả xấp xỉ phổ quát (Nhận xét 07.3) chặn số hạng nào?
:::

::: hint Gợi ý 1
Phần (b). Viết đạo hàm riêng của $f_\theta(x)$ theo từng khối tham số $\Theta_1$, $b_1$, $\Theta_2$, $b_2$; tìm thừa số bằng $0$ tại $\theta=0$. Phần (c). Đổi chỗ hai nơ-ron ẩn không đổi hàm điểm số.
:::

::: hint Gợi ý 2
Phần (b). Đạo hàm theo $\Theta_2$ chứa $\operatorname{ReLU}(\Theta_1x+b_1)$; đạo hàm theo $\Theta_1$ và $b_1$ chứa $\Theta_2$. Dùng quy nạp theo số bước; với $b_2$, dùng $\sum_i\tilde y_i=0$. Phần (c). Tại $\theta_{\mathrm{mid}}$, $b_1=(-\tfrac12,-\tfrac12)^\top$ và $\Theta_2=(-\tfrac12,-\tfrac12)$.
:::

::: solution Lời giải Bài tập 07.5
**(a) Một nghiệm khớp đúng.** Theo Mệnh đề 07.2, $f_\theta$ nhận $-\tfrac12$, $\tfrac12$, $\tfrac12$, $-\tfrac12$ tại $(0,0)$, $(1,0)$, $(0,1)$, $(1,1)$, đúng bằng $\tilde y_i/2$. Mọi số hạng của $F$ bằng $0$, nên $F(\theta)=0$. Hàm $h_\theta$ phân lớp đúng cả bốn quan sát, nên với $D$ đều trên chúng, $\inf_{\mathcal H_{2,2}}L_D=0$ và sai số xấp xỉ bằng $0-L^*=0$.

**(b) Hạ gradient khởi tạo tại $0$.**

**Bước 1: đạo hàm của hàm điểm số.** Với $z=\Theta_1x+b_1$ và $a_1=\operatorname{ReLU}(z)$, ta có $f_\theta(x)=\Theta_2a_1+b_2$. Gọi $\operatorname{ReLU}'(z)\in\mathbb R^2$ là véc-tơ đạo hàm của ReLU tại hai tọa độ của $z$, theo một quy ước bất kì tại $0$. Khi đó
$$
\begin{aligned}
\nabla_{b_2}f_\theta&=1,\\
\nabla_{\Theta_2}f_\theta&=a_1^\top,\\
\nabla_{b_1}f_\theta&=\Theta_2^\top\odot\operatorname{ReLU}'(z),\\
\nabla_{\Theta_1}f_\theta&=\nabla_{b_1}f_\theta\;x^\top,
\end{aligned}
$$
với $\odot$ là phép nhân theo tọa độ. Gradient của $F$ theo mỗi khối là $\tfrac12\sum_i\big(f_\theta(x_i)-\tilde y_i/2\big)$ nhân với đạo hàm tương ứng tại $x_i$.

**Bước 2: quy nạp.** Ở bước $t=1$, ba khối $\Theta_1$, $b_1$, $\Theta_2$ bằng $0$ theo cách khởi tạo. Giả sử chúng bằng $0$ ở bước $t$. Khi đó $z=0$ và $a_1=\operatorname{ReLU}(0)=0$, nên đạo hàm theo $\Theta_2$ bằng $0$. Vì $\Theta_2=0$, đạo hàm theo $b_1$ và $\Theta_1$ bằng $0$ với mọi quy ước cho $\operatorname{ReLU}'(0)$. Bước hạ gradient không đổi ba khối này, nên chúng bằng $0$ ở bước $t+1$.

**Bước 3: hệ số tự do của lớp ra.** Với ba khối bằng $0$, $f_\theta\equiv b_2$ và
$$
\frac{\partial F}{\partial b_2}=\frac12\sum_{i=1}^4\Big(b_2-\frac{\tilde y_i}2\Big)=2b_2,
$$
vì $\sum_i\tilde y_i=0$. Từ $b_2=0$, mọi bước giữ $b_2=0$.

**Bước 4: lỗi.** Hàm trả về là $f_\theta\equiv0$, nên $h_\theta\equiv\mathbb 1[0\ge0]=1$: hai quan sát nhãn $0$ bị phân lớp sai, lỗi 0–1 bằng $\tfrac12$. Giá trị mục tiêu là $F=\tfrac14$, trong khi giá trị nhỏ nhất là $0$ theo (a).

**Bước 5: SGD.** Gradient trên một quan sát có cùng các thừa số ở Bước 1, nên lập luận của Bước 2 giữ nguyên: $\Theta_1$, $b_1$, $\Theta_2$ bằng $0$ ở mọi bước. Chỉ $b_2$ thay đổi, theo các quan sát được rút. Hàm phân lớp là hằng, nên sai đúng hai trong bốn quan sát: lỗi vẫn bằng $\tfrac12$.

**(c) Hàm mục tiêu không lồi.**

**Bước 1: đổi chỗ.** Hai hàng của $\Theta_1$ đều bằng $(1,1)$, nên $\theta_{\mathrm{swap}}$ có $\Theta_1$ như cũ, $b_1=(-1,0)^\top$, $\Theta_2=(-2,1)$, $b_2=-\tfrac12$. Hai nơ-ron ẩn chỉ đổi thứ tự trong tổng, nên $f_{\theta_{\mathrm{swap}}}=f_\theta$ và $F(\theta_{\mathrm{swap}})=0$.

**Bước 2: trung điểm.** $\theta_{\mathrm{mid}}$ có $\Theta_1$ như cũ, $b_1=(-\tfrac12,-\tfrac12)^\top$, $\Theta_2=(-\tfrac12,-\tfrac12)$, $b_2=-\tfrac12$. Với $s=x_1+x_2$, hai nơ-ron ẩn cùng tính $\operatorname{ReLU}(s-\tfrac12)$, nên
$$
f_{\theta_{\mathrm{mid}}}(x)=-\operatorname{ReLU}\big(s-\tfrac12\big)-\tfrac12 .
$$

**Bước 3: giá trị của $F$.** Tại $s=0,1,2$, hàm nhận $-\tfrac12$, $-1$, $-2$. Hiệu với $\tilde y_i/2$ là $0$ tại $(0,0)$, $-\tfrac32$ tại $(1,0)$ và $(0,1)$, và $-2+\tfrac12=-\tfrac32$ tại $(1,1)$. Do đó
$$
\begin{aligned}
F(\theta_{\mathrm{mid}})&=\frac14\cdot3\cdot\frac94\\
&=\frac{27}{16}=1{,}6875 .
\end{aligned}
$$

**Bước 4: kết luận.** Nếu $F$ lồi thì $F(\theta_{\mathrm{mid}})\le\tfrac12F(\theta)+\tfrac12F(\theta_{\mathrm{swap}})=0$. Vì $1{,}6875>0$, $F$ không lồi; các bảo đảm hội tụ của Bài 05 cho hàm lồi không áp dụng, như Ví dụ 05.10.

**(d) Ba số hạng của Mệnh đề 04.3.**

**Bước 1: thiết lập.** $D$ đều trên bốn quan sát và mẫu gồm đúng bốn quan sát này, nên $L_D(h)=L_S(h)$ với mọi $h$: mẫu là $r$-đại diện với mọi $r>0$. Lấy $L^*=0$ và $\tilde h$ là hàm phân lớp hằng $1$ của (b).

**Bước 2: ba số hạng.** Sai số xấp xỉ bằng $0$ theo (a). Số hạng $2r$ nhỏ tùy ý. Sai số tối ưu thực nghiệm là $\operatorname{opt}_S(\tilde h)=L_S(\tilde h)-\inf_{\mathcal H_{2,2}}L_S=\tfrac12-0$. Rủi ro vượt mức $L_D(\tilde h)-L^*=\tfrac12$ đến hết từ số hạng tối ưu.

**Bước 3: vai trò của kết quả xấp xỉ.** Một kết quả xấp xỉ phổ quát chỉ chặn số hạng đầu: lớp chứa một hàm tốt. Nó không nói gì về $\operatorname{opt}_S$; với hàm kích hoạt dấu, ba nơ-ron ẩn và một nơ-ron hằng, tìm nghiệm ERM đã là bài toán NP-khó (Nhận xét 07.3, UML §20.5).

**Kiểm tra lại.** Tại $\theta=0$, $F(0)=\tfrac14\cdot4\cdot\tfrac14=\tfrac14$, khớp Bước 4 của (b). Ở (c), $\theta_{\mathrm{mid}}$ phân lớp đúng $(0,0)$, $(1,1)$ và sai $(1,0)$, $(0,1)$: trung điểm của hai nghiệm khớp đúng có lỗi 0–1 bằng $\tfrac12$.
:::

### Bài tập 07.6 (Nhãn thật và nhãn hoán vị, thực nghiệm tùy chọn)

**Mức độ:** tính toán, khái niệm, thực nghiệm (tùy chọn). **Mục tiêu:** mục tiêu học tập 5; đọc lỗi kiểm tra, chuẩn và số hạng Rademacher qua nhiều hạt giống ngẫu nhiên (random seed) và cỡ mẫu, và tách bằng chứng thí nghiệm khỏi chứng minh.

::: exercise Bài tập 07.6
Thí nghiệm của câu hỏi mở đầu (giao thức ở Phụ lục D) được chạy lại với $m\in\{100,200,400,800\}$, cùng $N=2000$, $5000$ điểm kiểm tra và mười hạt giống ngẫu nhiên $0,\ldots,9$. Trong mọi lần chạy, lỗi huấn luyện bằng $0$, lề nhỏ nhất bằng $1$, và $C_x$ của Ví dụ 07.10 nằm trong khoảng $1{,}517$–$1{,}544$. Ba bảng dưới ghi các đại lượng qua mười lần chạy.

Lỗi kiểm tra trung bình:

| $m$ | Nhãn thật | Nhãn hoán vị |
|---|---|---|
| $100$ | $0{,}0340$ | $0{,}499$ |
| $200$ | $0{,}0230$ | $0{,}501$ |
| $400$ | $0{,}0147$ | $0{,}499$ |
| $800$ | $0{,}0134$ | $0{,}499$ |

Với nhãn thật, độ lệch chuẩn của lỗi kiểm tra qua mười lần chạy là $0{,}0099$; $0{,}0074$; $0{,}0040$; $0{,}0050$ theo thứ tự bốn cỡ mẫu.

Chuẩn $\lVert\hat w\rVert$ với nhãn thật:

| $m$ | Trung bình | Nhỏ nhất – lớn nhất |
|---|---|---|
| $100$ | $446{,}7$ | $253$–$871$ |
| $200$ | $915{,}7$ | $351$–$1721$ |
| $400$ | $2301{,}3$ | $1111$–$3317$ |
| $800$ | $5744{,}7$ | $3532$–$9250$ |

Chuẩn $\lVert\hat w\rVert$ với nhãn hoán vị:

| $m$ | Trung bình | Nhỏ nhất – lớn nhất |
|---|---|---|
| $100$ | $3774{,}2$ | $2731$–$8750$ |
| $200$ | $10\,852{,}6$ | $6792$–$14\,052$ |
| $400$ | $27\,739{,}3$ | $18\,312$–$46\,585$ |
| $800$ | $125\,453$ | $76\,307$–$316\,483$ |

**(a)** (Bắt buộc, tính toán.)

- **(i)** Tính tỉ số giữa chuẩn trung bình với nhãn hoán vị và với nhãn thật cho từng $m$.
- **(ii)** Lấy $\gamma=1$. Chứng minh trung bình qua mười lần chạy của số hạng Rademacher $2\lVert\hat w\rVert C_x/(\gamma\sqrt m)$ với nhãn thật ít nhất bằng $3\bar B/\sqrt m$, trong đó $\bar B$ là trung bình của $\lVert\hat w\rVert$ qua mười lần chạy. Tính cận dưới này cho bốn giá trị $m$.
- **(iii)** Tìm số mũ $\alpha$ sao cho chuẩn trung bình với nhãn thật tăng như $m^\alpha$ từ $m=100$ đến $m=800$. So chiều biến thiên của số hạng Rademacher với chiều biến thiên của lỗi kiểm tra.

**(b)** (Bắt buộc, khái niệm.) Nêu những kết luận mà ba bảng cho phép, và những kết luận mà chúng không cho phép. Với nhãn thật, hiệu lỗi kiểm tra trung bình giữa $m=400$ và $m=800$ có lớn hơn sai số chuẩn của hiệu không? Vì sao các cận của Bài 07 không áp dụng cho cột nhãn hoán vị?

**(c)** (Thực nghiệm, tùy chọn.) Viết một giao thức tái lập ba bảng chỉ với thư viện NumPy, chạy nó, rồi thêm một biến thể tự chọn (chẳng hạn nhãn ngẫu nhiên độc lập với $x$, hay một giá trị $N$ khác). Ghi điều cần quan sát trước khi chạy biến thể.
:::

::: hint Gợi ý 1
Phần (a)(ii). Với $C_x$ và $m$ cố định, số hạng Rademacher tỉ lệ với $\lVert\hat w\rVert$. Phần (a)(iii). Lấy logarit của tỉ số hai chuẩn và chia cho logarit của tỉ số hai cỡ mẫu.
:::

::: hint Gợi ý 2
Phần (a)(ii). Trong mỗi lần chạy, $C_x\ge1{,}5$, nên số hạng ít nhất $3\lVert\hat w\rVert/\sqrt m$; lấy trung bình hai vế. Phần (b). Sai số chuẩn của một trung bình qua mười lần chạy là độ lệch chuẩn chia $\sqrt{10}$. Với nhãn hoán vị, tổng các nhãn huấn luyện bằng tổng các nhãn thật.
:::

::: solution Lời giải Bài tập 07.6
**(a) Tính trên số đã chạy.**

**Bước 1: tỉ số hai chuẩn.** Chia chuẩn trung bình với nhãn hoán vị cho chuẩn trung bình với nhãn thật:

| $m$ | Tỉ số |
|---|---|
| $100$ | $3774{,}2/446{,}7\approx8{,}45$ |
| $200$ | $10\,852{,}6/915{,}7\approx11{,}85$ |
| $400$ | $27\,739{,}3/2301{,}3\approx12{,}05$ |
| $800$ | $125\,453/5744{,}7\approx21{,}84$ |

Với mỗi $m$, chuẩn lớn nhất với nhãn thật nhỏ hơn chuẩn nhỏ nhất với nhãn hoán vị.

**Bước 2: cận dưới của số hạng Rademacher.** Trong mỗi lần chạy, $C_x\ge1{,}517\ge1{,}5$ và $\gamma=1$, nên số hạng ít nhất $3\lVert\hat w\rVert/\sqrt m$. Lấy trung bình qua mười lần chạy, trung bình của số hạng ít nhất $3\bar B/\sqrt m$. Thay số, làm tròn xuống vì đây là cận dưới:

| $m$ | $3\bar B/\sqrt m$ | Cận dưới |
|---|---|---|
| $100$ | $3\cdot446{,}7/10$ | $134{,}0$ |
| $200$ | $3\cdot915{,}7/\sqrt{200}$ | $194{,}2$ |
| $400$ | $3\cdot2301{,}3/20$ | $345{,}1$ |
| $800$ | $3\cdot5744{,}7/\sqrt{800}$ | $609{,}3$ |

Mọi giá trị lớn hơn $1$, nên Hệ quả 07.16 không cho thông tin ở cả bốn cỡ mẫu. Cận hợp lệ dùng lưới $B_k=2^k\ge\lVert\hat w\rVert$ của Nhận xét 07.17, nên số hạng của nó còn lớn hơn.

**Bước 3: số mũ.** Từ $m=100$ đến $m=800$, cỡ mẫu tăng $8$ lần và chuẩn trung bình tăng $5744{,}7/446{,}7\approx12{,}86$ lần, nên
$$
\alpha=\frac{\ln12{,}86}{\ln8}\approx\frac{2{,}554}{2{,}079}\approx1{,}23 .
$$
Mỗi lần $m$ gấp đôi, chuẩn tăng $2{,}05$; $2{,}51$; $2{,}50$ lần, đều lớn hơn $\sqrt2\approx1{,}414$.

**Bước 4: hai chiều biến thiên.** Số hạng Rademacher tỉ lệ với $\lVert\hat w\rVert/\sqrt m$, tức tăng như $m^{1{,}23-0{,}5}=m^{0{,}73}$: từ $m=100$ đến $m=800$, cận dưới ở Bước 2 tăng khoảng $4{,}55$ lần. Trong cùng khoảng, lỗi kiểm tra với nhãn thật giảm từ $0{,}034$ xuống $0{,}013$. Với nghiệm nội suy chuẩn nhỏ nhất trong thí nghiệm này, cận theo chuẩn không theo dõi được lỗi kiểm tra.

**(b) Phạm vi của kết luận.**

**Bước 1: kết luận được phép.** Các kết luận sau chỉ đúng cho thiết lập đã chạy (phân bố, kiến trúc, lớp ẩn, nghiệm nội suy chuẩn nhỏ nhất, bốn cỡ mẫu, mười hạt giống).

- **Hai loại nhãn.** Ở mọi $m$, nhãn thật cho lỗi kiểm tra thấp hơn nhiều và chuẩn nhỏ hơn; chuẩn lớn nhất với nhãn thật nhỏ hơn chuẩn nhỏ nhất với nhãn hoán vị.
- **Lỗi kiểm tra.** Với nhãn thật, lỗi kiểm tra giảm từ $m=100$ đến $m=400$.
- **Số hạng Rademacher.** Số hạng này lớn hơn $1$ ở mọi $m$ và tăng theo $m$.

**Bước 2: kết luận không được phép.** Ba bảng là bằng chứng thí nghiệm, không phải chứng minh. Chúng không chứng tỏ chuẩn quyết định lỗi kiểm tra với mọi mạng hay mọi thuật toán huấn luyện, không cho biết điều gì ngoài bốn cỡ mẫu đã chạy, và không cho thấy cận theo chuẩn giải thích được lỗi kiểm tra.

**Bước 3: hai cỡ mẫu lớn nhất.** Sai số chuẩn của một trung bình qua mười lần chạy là độ lệch chuẩn chia $\sqrt{10}\approx3{,}16$. Với $m=400$, $m=800$ và hiệu của hai trung bình khi coi hai nhóm độc lập:
$$
\begin{aligned}
&0{,}0040/3{,}16\approx0{,}0013,\\
&0{,}0050/3{,}16\approx0{,}0016,\\
&\sqrt{0{,}0013^2+0{,}0016^2}\approx0{,}002 .
\end{aligned}
$$

Hai nhóm dùng chung mười hạt giống, nên không độc lập hoàn toàn. Ghép cặp theo hạt giống, mười hiệu lỗi kiểm tra giữa $m=400$ và $m=800$ cùng hạt giống có độ lệch chuẩn khoảng $0{,}0061$ (số này cần dữ liệu từng lần chạy, không có trong bảng), nên sai số chuẩn của hiệu là $0{,}0061/3{,}16\approx0{,}0019$.

Cả hai sai số chuẩn lớn hơn hiệu $0{,}0147-0{,}0134=0{,}0013$, nên ba bảng không cho phép kết luận lỗi kiểm tra giảm từ $m=400$ đến $m=800$.

**Bước 4: nhãn hoán vị.** Tổng các nhãn hoán vị bằng tổng các nhãn thật, nên các cặp $(x_i,y_i)$ không độc lập và (T1) không thỏa (Ví dụ 07.6, Bước 3; Phụ lục D). Nhãn kiểm tra cũng được hoán vị, nên Hệ quả 02.10 không áp dụng cho lỗi kiểm tra của cột này. Cột nhãn hoán vị chỉ dùng để so sánh.

**(c) Một giao thức mẫu.**

- **Dữ liệu.** Điểm $x$ đều trên hình tròn đơn vị, nhãn thật $y=\mathbb 1[x_1+0{,}5x_2\ge0]$; mẫu huấn luyện $m$ điểm và mẫu kiểm tra $5000$ điểm, rút độc lập.
- **Mạng và huấn luyện.** $N=2000$ nơ-ron ẩn rút một lần, độc lập với mẫu, rồi cố định; nghiệm nội suy chuẩn nhỏ nhất trên $\chi(x)$, tính bằng bình phương tối thiểu; kiểm hạng của ma trận đặc trưng bằng $m$ trước khi dùng nghiệm.
- **Nhãn so sánh.** Một hoán vị đều của nhãn huấn luyện và một hoán vị độc lập của nhãn kiểm tra, trên cùng các điểm và cùng lớp ẩn.
- **Lặp lại.** Mười hạt giống (hoặc nhiều hơn), mỗi hạt giống cố định thứ tự rút: điểm huấn luyện, điểm kiểm tra, lớp ẩn, hai hoán vị.
- **Đại lượng đo và báo cáo.** Lỗi huấn luyện, lỗi kiểm tra, $\lVert\hat w\rVert$, lề nhỏ nhất, $C_x$, lề chuẩn hóa, số hạng Rademacher; báo trung bình, độ lệch chuẩn, nhỏ nhất và lớn nhất theo $m$. Mẫu kiểm tra chỉ dùng để báo cáo, không để chọn gì.
- **Biến thể.** Với nhãn ngẫu nhiên độc lập với $x$, (T1) thỏa. Điều cần quan sát được ghi trước khi chạy, chẳng hạn lỗi kiểm tra có gần $0{,}5$ không và chuẩn gần cột nào của bảng.
- **Phạm vi.** Bảng hay đường cong thu được là bằng chứng cho thiết lập đã chọn, không phải định lý.

**Kiểm tra lại.** Với $m=200$, tỉ số $11{,}85$ khớp Ví dụ 07.10, và cận dưới $194{,}2$ nằm trong khoảng $75$–$372$ của số hạng Rademacher ở ví dụ đó.
:::

## Bài tập chọn từ UML

### Bài tập 07.7 (Hàm tăng trưởng của lớp tích; UML Bài tập 20.3)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 5; công cụ đếm cho cận chiều VC của mạng ngưỡng (Nhận xét 07.6), một cận chỉ phụ thuộc kiến trúc.

::: exercise Bài tập 07.7
Mở rộng Định nghĩa 03.1 và 03.11 cho lớp $\mathcal H$ các hàm $\mathcal X\to\mathcal Y$ với $\mathcal Y$ hữu hạn bất kì: với bộ $C=(x_1,\ldots,x_m)\in\mathcal X^m$ (cho phép lặp), $\mathcal H_C=\{(h(x_1),\ldots,h(x_m)):h\in\mathcal H\}\subseteq\mathcal Y^m$ và $\Pi_{\mathcal H}(m)=\max_C\lvert\mathcal H_C\rvert$.

Cho hai lớp $\mathcal H_1$, $\mathcal H_2$ các hàm $\mathcal X\to\mathcal Y_1$ và $\mathcal X\to\mathcal Y_2$, với $\mathcal Y_1$, $\mathcal Y_2$ hữu hạn. *Lớp tích* (product class) $\mathcal H_1\times\mathcal H_2$ gồm các hàm $x\mapsto(h_1(x),h_2(x))$ với $h_1\in\mathcal H_1$, $h_2\in\mathcal H_2$. Phần (a) là UML Bài tập 20.3; (b), (c) do học phần thêm.

**(a)** Chứng minh $\Pi_{\mathcal H_1\times\mathcal H_2}(m)\le\Pi_{\mathcal H_1}(m)\,\Pi_{\mathcal H_2}(m)$ với mọi $m\ge1$.

**(b)** Với $\mathcal X=\{1,2\}$ và $\mathcal Y_1=\mathcal Y_2=\{0,1\}$, dựng hai lớp, mỗi lớp hai hàm, sao cho bất đẳng thức ở (a) là bất đẳng thức thực sự khi $m=1$.

**(c)** *Hàm kích hoạt ngưỡng* (threshold activation) là $\varsigma(t)=\mathbb 1[t\ge0]$, bản giá trị $\{0,1\}$ của hàm kích hoạt dấu ở Nhận xét 07.6. Một lớp nơ-ron ẩn gồm $N_1$ nơ-ron với hàm kích hoạt này cho ánh xạ $x\mapsto\big(\mathbb 1[\langle v_j,x\rangle+b_{1j}\ge0]\big)_{j=1}^{N_1}$ từ $\mathbb R^p$ vào $\{0,1\}^{N_1}$, với $v_j\in\mathbb R^p$ và $b_{1j}\in\mathbb R$ tùy ý. Chứng minh hàm tăng trưởng của lớp các ánh xạ này không quá $(em)^{N_1(p+1)}$ với mọi $m\ge1$.
:::

::: hint Gợi ý 1
Phần (a). Cố định một bộ $C$ và so $(\mathcal H_1\times\mathcal H_2)_C$ với tích Descartes $(\mathcal H_1)_C\times(\mathcal H_2)_C$. Phần (b). Với $m=1$, tìm điểm mà tại đó mỗi lớp đạt $\Pi(1)=2$. Phần (c). Mỗi nơ-ron là một hàm của $\mathcal H^p_{\mathrm{aff}}$.
:::

::: hint Gợi ý 2
Phần (a). Sắp lại các tọa độ cho một song ánh giữa $(\mathcal H_1\times\mathcal H_2)_C$ và $(\mathcal H_1)_C\times(\mathcal H_2)_C$. Phần (b). Chọn hai lớp đạt giá trị lớn nhất của hàm tăng trưởng tại hai điểm khác nhau. Phần (c). Quy nạp theo $N_1$ bằng (a). Với $m\ge p+1$, dùng Bổ đề 03.12 với $d=p+1$; với $m<p+1$, dùng $\Pi\le2^m$ và $2<e$.
:::

::: solution Lời giải Bài tập 07.7
**(a) Lớp tích.**

**Bước 1: một bộ điểm cố định.** Cố định $C=(x_1,\ldots,x_m)$. Mỗi phần tử của $(\mathcal H_1\times\mathcal H_2)_C$ là một bộ $m$ cặp $(h_1(x_i),h_2(x_i))$, $i=1,\ldots,m$. Sắp lại các tọa độ, ta được cặp gồm hai bộ $(h_1(x_i))_{i\le m}$ và $(h_2(x_i))_{i\le m}$, thuộc $(\mathcal H_1)_C\times(\mathcal H_2)_C$. Phép sắp lại có nghịch đảo, nên là đơn ánh. Nó là toàn ánh: với mọi cặp thu hẹp của $h_1\in\mathcal H_1$ và $h_2\in\mathcal H_2$, hàm $x\mapsto(h_1(x),h_2(x))$ thuộc lớp tích. Do đó
$$
\begin{aligned}
&\lvert(\mathcal H_1\times\mathcal H_2)_C\rvert\\
&=\lvert(\mathcal H_1)_C\rvert\cdot\lvert(\mathcal H_2)_C\rvert .
\end{aligned}
$$

**Bước 2: hàm tăng trưởng.** Theo định nghĩa, $\lvert(\mathcal H_i)_C\rvert\le\Pi_{\mathcal H_i}(m)$ với mọi $C$. Do đó $\lvert(\mathcal H_1\times\mathcal H_2)_C\rvert\le\Pi_{\mathcal H_1}(m)\Pi_{\mathcal H_2}(m)$ với mọi $C$, và lấy giá trị lớn nhất theo $C$ cho bất đẳng thức cần chứng minh. Đẳng thức ở Bước 1 đúng với từng $C$; hai lớp có thể đạt giá trị lớn nhất tại hai bộ khác nhau, nên với hàm tăng trưởng chỉ có bất đẳng thức.

**(b) Bất đẳng thức thực sự.** Kí hiệu một hàm trên $\{1,2\}$ bằng cặp giá trị $(h(1),h(2))$. Lấy $\mathcal H_1=\{(0,0),(0,1)\}$, chỉ khác nhau tại điểm $2$, và $\mathcal H_2=\{(0,0),(1,0)\}$, chỉ khác nhau tại điểm $1$. Với $m=1$:

- **Từng lớp.** $\Pi_{\mathcal H_1}(1)=2$ (tại $C=(2)$) và $\Pi_{\mathcal H_2}(1)=2$ (tại $C=(1)$); tích bằng $4$.
- **Lớp tích tại $C=(1)$.** Các cặp $(h_1(1),h_2(1))$ là $(0,0)$ và $(0,1)$: hai giá trị.
- **Lớp tích tại $C=(2)$.** Các cặp $(h_1(2),h_2(2))$ là $(0,0)$ và $(1,0)$: hai giá trị.

Do đó $\Pi_{\mathcal H_1\times\mathcal H_2}(1)=2<4$.

**(c) Một lớp nơ-ron ngưỡng.**

**Bước 1: một nơ-ron.** Mỗi nơ-ron là hàm $x\mapsto\mathbb 1[\langle v,x\rangle+b\ge0]$ của $\mathcal H^p_{\mathrm{aff}}$, có chiều VC $d=p+1$ (Mệnh đề 03.9(a)).

**Bước 2: một cận cho mọi $m$.** Nếu $m\ge p+1$, Bổ đề 03.12(a), (b) cho
$$
\begin{aligned}
\Pi_{\mathcal H^p_{\mathrm{aff}}}(m)&\le\Big(\frac{em}{p+1}\Big)^{p+1}\\
&\le(em)^{p+1}.
\end{aligned}
$$
Nếu $1\le m<p+1$, thì $\Pi_{\mathcal H^p_{\mathrm{aff}}}(m)\le2^m<e^m\le e^{p+1}\le(em)^{p+1}$. Vậy $\Pi_{\mathcal H^p_{\mathrm{aff}}}(m)\le(em)^{p+1}$ với mọi $m\ge1$.

**Bước 3: quy nạp theo số nơ-ron.** Tham số của các nơ-ron chọn độc lập với nhau, nên lớp ánh xạ của $k$ nơ-ron đầu là lớp tích của lớp ánh xạ của $k-1$ nơ-ron đầu (giá trị trong $\{0,1\}^{k-1}$) và $\mathcal H^p_{\mathrm{aff}}$. Theo (a) và quy nạp, hàm tăng trưởng của lớp $N_1$ nơ-ron không quá
$$
\big(\Pi_{\mathcal H^p_{\mathrm{aff}}}(m)\big)^{N_1}\le(em)^{N_1(p+1)} .
$$

**Kiểm tra lại.** Với $p=1$, $N_1=2$, $m=2$: mỗi nơ-ron tách trọn hai điểm phân biệt của $\mathbb R$, nên lớp đạt cả $4^2=16$ bộ giá trị trong $(\{0,1\}^2)^2$, đúng bằng $\Pi_{\mathcal H^1_{\mathrm{aff}}}(2)^2=16$; cận $(2e)^4\approx874$ đúng nhưng lỏng.
:::

### Bài tập 07.8 (Hàm tăng trưởng của lớp hàm hợp; UML Bài tập 20.4)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 5; ghép Bài tập 07.7 với bổ đề Sauer–Shelah để chặn chiều VC của một lớp mạng ngưỡng bằng số tham số, độc lập với nhãn.

::: exercise Bài tập 07.8
Dùng hàm tăng trưởng của Bài tập 07.7. Cho lớp $\mathcal H_1$ các hàm $\mathcal X\to\mathcal X'$ và lớp $\mathcal H_2$ các hàm $\mathcal X'\to\mathcal Y$, với $\mathcal X'$, $\mathcal Y$ hữu hạn. *Lớp hàm hợp* (composition class) là $\mathcal H_2\circ\mathcal H_1=\{h_2\circ h_1:h_1\in\mathcal H_1,\ h_2\in\mathcal H_2\}$. Phần (a) là UML Bài tập 20.4; (b), (c) do học phần thêm.

**(a)** Chứng minh $\Pi_{\mathcal H_2\circ\mathcal H_1}(m)\le\Pi_{\mathcal H_2}(m)\,\Pi_{\mathcal H_1}(m)$ với mọi $m\ge1$.

**(b)** UML lấy giá trị lớn nhất trên các tập $m$ điểm phân biệt. Với $\mathcal X'=\{0,1\}$ và $m=3$, chỉ ra bước của (a) cần định nghĩa cho phép điểm lặp.

**(c)** Xét lớp hàm phân lớp $h_\theta$ của kiến trúc $J=2$ (Định nghĩa 07.1) với hàm kích hoạt ngưỡng của Bài tập 07.7(c) ở lớp ẩn, và $P=N_1(p+1)+N_1+1$ tham số. Chứng minh hàm tăng trưởng của lớp không quá $(em)^P$, rồi suy ra: nếu $(em)^P<2^m$ thì chiều VC của lớp nhỏ hơn $m$. Với $p=9$, $N_1=9$, tính $P$, tìm $m$ nhỏ nhất thỏa $(em)^P<2^m$, và nêu cận trên cho chiều VC.
:::

::: hint Gợi ý 1
Phần (a). Cố định một bộ $C$ và nhóm các hàm của lớp hàm hợp theo thu hẹp của $h_1$ lên $C$. Phần (c). Viết $h_\theta$ thành hợp của ánh xạ lớp ẩn và một hàm phân lớp afin trên $\{0,1\}^{N_1}$.
:::

::: hint Gợi ý 2
Phần (a). Với $u=(h_1(x_1),\ldots,h_1(x_m))$, các bộ $(h_2(u_1),\ldots,h_2(u_m))$ tạo thành thu hẹp của $\mathcal H_2$ lên bộ $u$, và $u$ có thể có điểm lặp. Phần (c). Lớp ra là thu hẹp của $\mathcal H^{N_1}_{\mathrm{aff}}$ lên $\{0,1\}^{N_1}$; so $P\ln(em)$ với $m\ln2$.
:::

::: solution Lời giải Bài tập 07.8
**(a) Lớp hàm hợp.**

**Bước 1: nhóm theo hàm trong.** Cố định $C=(x_1,\ldots,x_m)$. Với $h_1\in\mathcal H_1$, đặt $u=(h_1(x_1),\ldots,h_1(x_m))\in(\mathcal H_1)_C$. Vì $(h_2\circ h_1)(x_i)=h_2(u_i)$,
$$
(\mathcal H_2\circ\mathcal H_1)_C=\bigcup_{u\in(\mathcal H_1)_C}(\mathcal H_2)_u,
$$
với $(\mathcal H_2)_u=\{(h_2(u_1),\ldots,h_2(u_m)):h_2\in\mathcal H_2\}$.

**Bước 2: mỗi nhóm; điểm lặp.** Mỗi $u$ là một bộ $m$ điểm của $\mathcal X'$, có thể có điểm lặp. Định nghĩa $\Pi_{\mathcal H_2}(m)$ lấy giá trị lớn nhất trên mọi bộ như vậy, nên $\lvert(\mathcal H_2)_u\rvert\le\Pi_{\mathcal H_2}(m)$.

**Bước 3: đếm.** Lực lượng của hợp các tập $(\mathcal H_2)_u$ không quá tổng lực lượng của chúng, nên
$$
\begin{aligned}
&\lvert(\mathcal H_2\circ\mathcal H_1)_C\rvert\\
&\le\lvert(\mathcal H_1)_C\rvert\,\Pi_{\mathcal H_2}(m)\\
&\le\Pi_{\mathcal H_1}(m)\,\Pi_{\mathcal H_2}(m).
\end{aligned}
$$
Lấy giá trị lớn nhất theo $C$ cho bất đẳng thức cần chứng minh.

**(b) Vai trò của điểm lặp.**

**Bước 1: $\mathcal X'$ có ít hơn $m$ điểm.** Với $\mathcal X'=\{0,1\}$ và $m=3$, mọi bộ $u\in\{0,1\}^3$ đều có điểm lặp, và $\{0,1\}$ không có tập con ba phần tử. Theo định nghĩa của UML, giá trị lớn nhất ở Bước 2 của (a) lấy trên một họ rỗng, nên hàm tăng trưởng theo định nghĩa đó không xác định tại $m=3$ (hoặc bằng $0$ nếu quy ước giá trị lớn nhất trên họ rỗng là $0$), trong khi $\lvert(\mathcal H_2)_u\rvert\ge1$. Do đó bất đẳng thức ở Bước 2 của (a) không còn đúng.

**Bước 2: $\mathcal X'$ có ít nhất $m$ điểm.** Một bộ có điểm lặp ứng với một tập ít hơn $m$ điểm, và Bước 2 của (a) cần thêm tính không giảm của hàm tăng trưởng theo $m$.

**Bước 3: định nghĩa của học phần.** Định nghĩa 03.11 cho phép điểm lặp, nên $\Pi_{\mathcal H_2}(m)$ xác định với mọi $m$ và không giảm theo $m$ (đoạn sau Định nghĩa 03.11). Trong mạng, $\mathcal X'=\{0,1\}^{N_1}$ là tập hữu hạn, và trường hợp của Bước 1 xảy ra khi $m>2^{N_1}$.

**(c) Lớp mạng ngưỡng.**

**Bước 1: viết thành lớp hàm hợp.** Với $a_1=\varsigma(\Theta_1x+b_1)\in\{0,1\}^{N_1}$, ta có $h_\theta(x)=\mathbb 1[\Theta_2a_1+b_2\ge0]$. Do đó lớp là $\mathcal H_2\circ\mathcal H_1$ của (a), với $\mathcal H_1$ là lớp ánh xạ lớp ẩn của Bài tập 07.7(c) và $\mathcal H_2$ là thu hẹp của $\mathcal H^{N_1}_{\mathrm{aff}}$ lên $\mathcal X'=\{0,1\}^{N_1}$.

**Bước 2: hai hàm tăng trưởng.** Theo Bài tập 07.7(c), $\Pi_{\mathcal H_1}(m)\le(em)^{N_1(p+1)}$. Mỗi bộ điểm của $\mathcal X'$ là một bộ điểm của $\mathbb R^{N_1}$, nên theo Bước 2 của Bài tập 07.7(c) với $N_1$ thay cho $p$, $\Pi_{\mathcal H_2}(m)\le(em)^{N_1+1}$.

**Bước 3: ghép.** Theo (a),
$$
\begin{aligned}
\Pi(m)&\le(em)^{N_1(p+1)+N_1+1}\\
&=(em)^P ,
\end{aligned}
$$
với $P$ đúng là số tham số của Định nghĩa 07.1.

**Bước 4: chiều VC.** Nếu chiều VC $d\ge m$ thì $\Pi(m)=2^m$ (đoạn sau Định nghĩa 03.11), nên $2^m\le(em)^P$. Do đó, nếu $(em)^P<2^m$ thì $d<m$.

**Bước 5: số.** Với $p=9$, $N_1=9$: $P=9\cdot10+10=100$. Bất đẳng thức $(em)^{100}<2^m$ tương đương $100(1+\ln m)<m\ln2$:
$$
\begin{aligned}
m=1162:&\quad805{,}79>805{,}44,\\
m=1163:&\quad805{,}88<806{,}13 .
\end{aligned}
$$
Hàm $m\ln2-100(1+\ln m)$ tăng khi $m>100/\ln2\approx144{,}3$, và với $m\le144$ thì $(em)^{100}\ge e^{100}>2^{144}\ge2^m$. Do đó $m=1163$ là giá trị nhỏ nhất, và chiều VC không quá $1162$, khoảng $11{,}6P$.

**Bước 6: ý nghĩa.** Cận chỉ phụ thuộc kiến trúc qua $P$, nên đúng như nhau cho nhãn thật và nhãn hoán vị (Nhận xét 07.6).

**Kiểm tra lại.** Với $P=100$, $(em)^P/2^m=\exp\big(100(1+\ln m)-m\ln2\big)$ bằng khoảng $1{,}42$ tại $m=1162$ và $0{,}78$ tại $m=1163$, khớp Bước 5.
:::

### Bài tập 07.9 (Tùy chọn: xấp xỉ đều hàm Lipschitz một biến bằng mạng một lớp ẩn; UML Bài tập 20.1, phát biểu đã sửa: hàm kích hoạt ReLU, một biến)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 1; dựng tường minh một mạng xấp xỉ đều, với số nơ-ron tăng theo $G/\epsilon$; số ô của cách chia hình lập phương tăng theo hàm mũ của số chiều.

::: exercise Bài tập 07.9
Phát biểu đã sửa so với UML: UML dùng hàm kích hoạt sigmoid và đầu vào trong một hình lập phương nhiều chiều; ở đây phần (a), (b) dùng ReLU với một biến.

Cho $f:[-1,1]\to[-1,1]$ là $G$-Lipschitz (Định nghĩa 05.4), $\epsilon>0$, số nguyên $k\ge1$ và các nút $t_i=-1+2i/k$, $i=0,\ldots,k$.

**(a)** Tìm tham số của một mạng ReLU với $p=1$, $J=2$, $N_1=k$ sao cho $f_\theta(t_i)=f(t_i)$ với mọi $i$ và $f_\theta$ tuyến tính trên mỗi đoạn $[t_i,t_{i+1}]$; $f_\theta$ là *hàm nội suy tuyến tính từng khúc* (piecewise linear interpolant) của $f$.

**(b)** Chứng minh $\lvert f(x)-f_\theta(x)\rvert\le G/k$ và $f_\theta(x)\in[-1,1]$ với mọi $x\in[-1,1]$; suy ra $k=\max\{1,\lceil G/\epsilon\rceil\}$ nơ-ron là đủ. Với $f(x)=\lvert x-0{,}1\rvert-0{,}5$ và $k=10$, chứng minh cận $G/k$ đạt được.

**(c)** Với $f:[-1,1]^p\to[-1,1]$ là $G$-Lipschitz theo chuẩn Euclid, chia $[-1,1]^p$ thành $k^p$ hình lập phương cạnh $2/k$ và xấp xỉ $f$ trên mỗi hình bằng giá trị tại tâm. Tìm $k$ đủ cho sai số $\epsilon$, và tính số hình lập phương khi $G=1$, $\epsilon=0{,}1$, $p=1,2,10$.

**(d)** Chứng minh không hàm liên tục $\tilde f$ nào trên $[-1,1]$ thỏa $\lvert\tilde f(x)-\mathbb 1[x\ge0]\rvert<\tfrac12$ với mọi $x$; suy ra điều đó cho mọi mạng có hàm kích hoạt liên tục. Giải thích vì sao cách chia ở (c), khi thực hiện bằng một mạng như vậy, cần xử lý riêng các điểm gần biên hình lập phương, còn cách dựng ở (a) thì không.
:::

::: hint Gợi ý 1
Phần (a). Trên đoạn đầu tiên chỉ cần một nơ-ron; mỗi nút tiếp theo thêm một nơ-ron làm đổi độ dốc. Phần (b). Viết $x$ thành tổ hợp lồi của hai nút kề nhau. Phần (d). Xét giới hạn trái tại $0$.
:::

::: hint Gợi ý 2
Phần (a). Với độ dốc $\mu_i=k\big(f(t_{i+1})-f(t_i)\big)/2$ trên đoạn thứ $i$ và $\mu_{-1}=0$, thử $f_\theta(x)=f(-1)+\sum_{i=0}^{k-1}(\mu_i-\mu_{i-1})\operatorname{ReLU}(x-t_i)$. Phần (b). Với $x=(1-\alpha)t_j+\alpha t_{j+1}$, sai số không quá $(1-\alpha)\lvert f(x)-f(t_j)\rvert+\alpha\lvert f(x)-f(t_{j+1})\rvert$.
:::

::: solution Lời giải Bài tập 07.9
**(a) Mạng nội suy.**

**Bước 1: tham số.** Với $\mu_i$ như Gợi ý 2, lấy $\Theta_1=(1,\ldots,1)^\top\in\mathbb R^{k\times1}$, $b_1=(-t_0,\ldots,-t_{k-1})^\top$, $\Theta_2=(\Delta\mu_0,\ldots,\Delta\mu_{k-1})$ với $\Delta\mu_i=\mu_i-\mu_{i-1}$ và $b_2=f(-1)$. Nơ-ron thứ $i$ tính $\operatorname{ReLU}(x-t_i)$; mạng có $2k+(k+1)=3k+1$ tham số.

**Bước 2: trên đoạn $[t_j,t_{j+1}]$.** Nơ-ron $i\le j$ có $x-t_i\ge0$, nơ-ron $i>j$ có $x-t_i\le0$, nên
$$
\begin{aligned}
f_\theta(x)&=f(t_0)\\
&\quad+\sum_{i=0}^{j}\Delta\mu_i(x-t_i).
\end{aligned}
$$
Ta chứng minh vế phải bằng $f(t_j)+\mu_j(x-t_j)$ bằng quy nạp theo $j$. Với $j=0$, đúng vì $\mu_{-1}=0$. Nếu đúng với $j-1$ thì vế phải với $j$ bằng
$$
\begin{aligned}
&f(t_{j-1})+\mu_{j-1}(x-t_{j-1})\\
&\quad+\Delta\mu_j(x-t_j)\\
&=f(t_{j-1})+\mu_{j-1}(t_j-t_{j-1})\\
&\quad+\mu_j(x-t_j)\\
&=f(t_j)+\mu_j(x-t_j),
\end{aligned}
$$
vì $\mu_{j-1}(t_j-t_{j-1})=f(t_j)-f(t_{j-1})$. Do đó $f_\theta$ tuyến tính trên mỗi đoạn, bằng $f$ tại $t_j$, và tại $t_{j+1}$ bằng $f(t_j)+\mu_j\cdot2/k=f(t_{j+1})$.

**(b) Sai số đều.**

**Bước 1: tổ hợp lồi.** Với $x\in[t_j,t_{j+1}]$, viết $x=(1-\alpha)t_j+\alpha t_{j+1}$, $\alpha\in[0,1]$. Theo (a), $f_\theta(x)=(1-\alpha)f(t_j)+\alpha f(t_{j+1})$, nằm giữa hai giá trị của $f$ trong $[-1,1]$, nên thuộc $[-1,1]$.

**Bước 2: tính Lipschitz.** Vì $\lvert x-t_j\rvert=2\alpha/k$ và $\lvert x-t_{j+1}\rvert=2(1-\alpha)/k$,
$$
\begin{aligned}
&\lvert f(x)-f_\theta(x)\rvert\\
&\le(1-\alpha)\lvert f(x)-f(t_j)\rvert\\
&\quad+\alpha\lvert f(x)-f(t_{j+1})\rvert\\
&\le\frac{4\alpha(1-\alpha)G}k\le\frac Gk,
\end{aligned}
$$
vì $\alpha(1-\alpha)\le\tfrac14$. Với $k=\max\{1,\lceil G/\epsilon\rceil\}$, $G/k\le\epsilon$. Chẳng hạn $G=1$, $\epsilon=0{,}1$ cần $k=10$ nơ-ron ẩn và $31$ tham số.

**Bước 3: cận đạt được.** Hàm $f(x)=\lvert x-0{,}1\rvert-0{,}5$ là $1$-Lipschitz, nhận giá trị trong $[-0{,}5;0{,}6]$. Với $k=10$, các nút gồm $0$ và $0{,}2$, với $f(0)=f(0{,}2)=-0{,}4$, nên $f_\theta=-0{,}4$ trên $[0;0{,}2]$. Tại $x=0{,}1$, $f(0{,}1)=-0{,}5$ và sai số bằng $0{,}1=G/k$.

**(c) Chia hình lập phương trong $p$ chiều.**

**Bước 1: điều kiện trên $k$.** Mỗi điểm của một hình lập phương cạnh $2/k$ lệch tâm không quá $1/k$ theo từng tọa độ, nên cách tâm không quá $\sqrt p/k$ theo chuẩn Euclid. Theo tính Lipschitz, sai số không quá $G\sqrt p/k$, và không quá $\epsilon$ khi $k\ge G\sqrt p/\epsilon$.

**Bước 2: số.** Với $G=1$, $\epsilon=0{,}1$, $k=\lceil\sqrt p/0{,}1\rceil$:

| $p$ | $k$ | $k^p$ |
|---|---|---|
| $1$ | $10$ | $10$ |
| $2$ | $\lceil14{,}14\rceil=15$ | $225$ |
| $10$ | $\lceil31{,}62\rceil=32$ | $2^{50}\approx1{,}13\cdot10^{15}$ |

Đây là số ô của riêng cách chia này, không phải cận dưới cho mọi mạng; cận dưới theo hàm mũ của $p$ là kết quả của UML §20.3 (Nhận xét 07.3).

**(d) Hàm liên tục và hàm chỉ thị.**

**Bước 1: mâu thuẫn.** Giả sử $\tilde f$ liên tục và $\lvert\tilde f(x)-\mathbb 1[x\ge0]\rvert<\tfrac12$ với mọi $x$. Với $x<0$, $\tilde f(x)<\tfrac12$; tại $0$, $\tilde f(0)>\tfrac12$. Theo tính liên tục, $\tilde f(0)=\lim_{x\to0^-}\tilde f(x)\le\tfrac12$, mâu thuẫn. Do đó sai số đều khi xấp xỉ hàm chỉ thị bằng một hàm liên tục ít nhất $\tfrac12$.

**Bước 2: hệ quả cho cách chia.** Mạng với hàm kích hoạt liên tục (ReLU, sigmoid) có hàm điểm số liên tục. Hàm hằng từng ô ở (c) nhảy tại biên các ô, nên một mạng không thể bằng nó gần biên. Một mạng dựng theo cách chia này phải được chứng minh riêng là, tại các điểm gần biên, đầu ra vẫn cách $f$ không quá $\epsilon$. Cách dựng ở (a) không gặp vấn đề này vì $f_\theta$ liên tục và bằng $f$ tại mọi nút.

**Kiểm tra lại.** Với $k=1$, $f_\theta$ là dây cung nối $(-1,f(-1))$ và $(1,f(1))$; với $f(x)=1-\lvert x\rvert$ ($G=1$), dây cung bằng $0$ và sai số tại $0$ bằng $1=G/k$.
:::
