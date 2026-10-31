# Bài tập Bài 05 — Hạ gradient, hạ gradient ngẫu nhiên và cận tối ưu

Định nghĩa, kết quả và ví dụ được dẫn theo số hiệu của ghi chú Bài 05. Kí hiệu theo bảng kí hiệu chung và §2 của ghi chú, gồm:

- **§2–§4.** $w\in\mathbb R^p$ là véc-tơ tham số, $h_w(x)=\langle w,x\rangle$ là hàm điểm số (score function), $\tilde y=2y-1$ là nhãn $\pm1$, $\partial F(w)$ là dưới vi phân (subdifferential), tập các dưới gradient (subgradient) tại $w$; $C_x$, $C_y$ là cận của $\lVert x\rVert$, $\lvert y\rvert$.
- **§5.** $\operatorname{proj}_W$ là phép chiếu Euclid (Euclidean projection) lên tập lồi đóng $W$; $B$ là bán kính của $W$ khi $W$ là quả cầu tâm $0$.
- **§6–§7.** $\varphi(w,\xi)$, $\psi(w)$ là ánh xạ oracle và trung bình của nó; $\xi_t$, $\mathcal F_t$, $g_t$ là lần rút, lịch sử và gradient ngẫu nhiên ở bước $t$; $\bar w_T$ là điểm lặp trung bình (averaged iterate); $R$ là cận của $\lVert w_1-u\rVert$; $\Delta_t=\lVert w_t-u\rVert^2$.
- **§10.** $b$ là kích thước lô (batch size) của lô nhỏ (mini-batch), $\sigma^2$ là phương sai của gradient ngẫu nhiên, $G_F$ là cận của $\lVert\psi\rVert$.

Giả thiết (C), (G1), (G2) theo ghi chú. Viết tắt: hạ gradient (gradient descent, GD), hạ gradient ngẫu nhiên (stochastic gradient descent, SGD). Mẫu $S$ cố định; mọi xác suất và kì vọng lấy theo nguồn ngẫu nhiên của thuật toán, trừ khi ghi khác. Độ chênh tối ưu (suboptimality) luôn là độ chênh của chính hàm mục tiêu mà thuật toán tối thiểu hóa.

Sáu bài đầu là bài gốc của học phần. Sáu bài sau chọn từ mục bài tập §9.6, §12.6 và §14.8 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* (Shalev-Shwartz và Ben-David, 2014; viết tắt UML). UML viết $\rho$ cho hằng số Lipschitz, $R$ hoặc $B$ cho cận chuẩn của dữ liệu và $w^\star$ cho véc-tơ tách có chuẩn nhỏ nhất; ở đây viết $G$, $C_x$ và $w^\circ$.

## Bài tập gốc

### Bài tập 05.1 (Tính lồi và dưới vi phân của hàm lỗi bản lề)

**Mức độ:** khái niệm, tính toán. **Mục tiêu:** mục tiêu học tập 1; dưới vi phân tại điểm không khả vi.

::: exercise Bài tập 05.1
Cho $x\in\mathbb R^p$ với $x\ne0$, nhãn $y\in\{0,1\}$ và $\tilde y=2y-1$. Hàm lỗi bản lề (hinge loss) của hàm điểm số $h_w$ trên quan sát $(x,y)$ là
$$
\ell(w)=\max\{0,\,1-\tilde y\langle w,x\rangle\}.
$$

**(a)** Chứng minh $\ell$ lồi trên $\mathbb R^p$ trực tiếp từ Định nghĩa 05.1.

**(b)** Gọi $w_0$ là một điểm gãy, tức $\tilde y\langle w_0,x\rangle=1$. Chứng minh
$$
\partial\ell(w_0)=\{-\alpha\tilde yx:\alpha\in[0,1]\}.
$$
Suy ra khẳng định ở phần kết luận của Ví dụ 05.2.

**(c)** Lấy $x=(2,1)$ và $y=0$. Tìm một dưới gradient của $\ell$ tại $w=0$ và tại $w=(-1,0)$, và viết dưới vi phân tại $w_0=(-0{,}4;-0{,}2)$.

**(d)** Mẫu $S$ gồm hai quan sát $((1,2),1)$ và $((2,1),0)$, với hàm lỗi bản lề. Tìm một dưới gradient của $L_S$ tại $w=0$.
:::

::: hint Gợi ý 1
Phần (a). Mỗi nhánh của cực đại là hàm afin, và với hàm afin bất đẳng thức của Định nghĩa 05.1 là đẳng thức. Phần (b). Chiều "$\supseteq$" đã có trong Ví dụ 05.2. Với chiều "$\subseteq$", cho $v\in\partial\ell(w_0)$ và thử bất đẳng thức dưới gradient tại vài điểm $u$ thích hợp.
:::

::: hint Gợi ý 2
Phần (b). Viết $v=cx+r$ với $r\perp x$. Điểm $u=w_0+r$ cho $r=0$. Sau đó thử $u=w_0-s\tilde yx$ với $s=1$ và $s=-1$.
:::

::: solution Lời giải Bài tập 05.1
**(a) Tính lồi.**

**Bước 1: nhánh afin.** Đặt $a(w)=1-\tilde y\langle w,x\rangle$. Với $w,u\in\mathbb R^p$ và $\alpha\in[0,1]$, tính tuyến tính của tích vô hướng cho
$$
\begin{aligned}
&a(\alpha w+(1-\alpha)u)\\
&\quad=\alpha a(w)+(1-\alpha)a(u).
\end{aligned}
$$

**Bước 2: cực đại.** Vì $a\le\ell$ và $\alpha,1-\alpha\ge0$, vế phải ở Bước 1 không quá $\alpha\ell(w)+(1-\alpha)\ell(u)$. Vì $\ell\ge0$, số $0$ cũng không quá $\alpha\ell(w)+(1-\alpha)\ell(u)$. Cực đại của $0$ và $a(\alpha w+(1-\alpha)u)$ chính là $\ell(\alpha w+(1-\alpha)u)$, nên
$$
\begin{aligned}
&\ell(\alpha w+(1-\alpha)u)\\
&\quad\le\alpha\ell(w)+(1-\alpha)\ell(u).
\end{aligned}
$$

**(b) Dưới vi phân tại điểm gãy.**

**Bước 1: chiều "$\supseteq$".** Tại $w_0$, ta có $a(w_0)=0=\ell(w_0)$, nên cả hai nhánh đạt cực đại. Nhánh hằng $0$ có gradient $0$, nhánh $a$ có gradient $-\tilde yx$. Theo Mệnh đề 05.3(a) và (c), $0$ và $-\tilde yx$ thuộc $\partial\ell(w_0)$. Với $\alpha\in[0,1]$, nhân bất đẳng thức dưới gradient của $-\tilde yx$ với $\alpha$, của $0$ với $1-\alpha$, rồi cộng: $-\alpha\tilde yx\in\partial\ell(w_0)$.

**Bước 2: thành phần vuông góc.** Cho $v\in\partial\ell(w_0)$. Viết $v=cx+r$, với $c=\langle v,x\rangle/\lVert x\rVert^2$ và $r\perp x$. Lấy $u=w_0+r$. Khi đó $\langle u,x\rangle=\langle w_0,x\rangle$, nên $\ell(u)=0$. Bất đẳng thức dưới gradient cho
$$
\begin{aligned}
0&\ge\ell(w_0)+\langle cx+r,r\rangle\\
&=c\langle x,r\rangle+\lVert r\rVert^2\\
&=\lVert r\rVert^2 .
\end{aligned}
$$
Vậy $r=0$ và $v=cx$.

**Bước 3: đổi biến.** Vì $\tilde y^2=1$, ta viết $c=-\alpha\tilde y$ với $\alpha=-c\tilde y$. Lấy $u=w_0-s\tilde yx$ với $s\in\mathbb R$. Do $\tilde y\langle w_0,x\rangle=1$,
$$
\begin{aligned}
1-\tilde y\langle u,x\rangle&=s\lVert x\rVert^2,\\
\langle v,u-w_0\rangle&=\alpha s\lVert x\rVert^2 .
\end{aligned}
$$
Do đó $\ell(u)=\max\{0,s\lVert x\rVert^2\}$.

**Bước 4: hai điểm thử.** Với $s=1$, bất đẳng thức dưới gradient cho $\lVert x\rVert^2\ge\alpha\lVert x\rVert^2$, tức $\alpha\le1$. Với $s=-1$, nó cho $0\ge-\alpha\lVert x\rVert^2$, tức $\alpha\ge0$. Cả hai bước chia cho $\lVert x\rVert^2>0$, nên cần $x\ne0$.

**Bước 5: Ví dụ 05.2.** Ở đó $x=(1,2)$, $\tilde y=1$ và $\langle w_0,x\rangle=1$ tại $w_0=(0{,}5;0{,}25)$. Theo Bước 1–4, dưới vi phân tại $w_0$ là $\{-\alpha(1,2):\alpha\in[0,1]\}$, đúng bằng đoạn nối $0$ và $(-1,-2)$.

**(c) Ba điểm với $x=(2,1)$, $y=0$.**

**Bước 1: hàm lỗi.** Ta có $\tilde y=-1$, nên $\ell(w)=\max\{0,1+\langle w,x\rangle\}$ và $-\tilde yx=(2,1)$.

**Bước 2: điểm $w=0$.** Ta có $1+\langle0,x\rangle=1>0$. Theo tính liên tục, nhánh afin lớn hơn $0$ trên một lân cận của $0$, nên $\ell$ khả vi tại $0$ với gradient $(2,1)$. Theo Mệnh đề 05.3(a), $(2,1)\in\partial\ell(0)$.

**Bước 3: điểm $w=(-1,0)$.** Ta có $1+\langle w,x\rangle=1-2=-1<0$, nên $\ell=0$ trên một lân cận của $w$, và $0\in\partial\ell(w)$.

**Bước 4: điểm gãy.** Tại $w_0=(-0{,}4;-0{,}2)$, $\langle w_0,x\rangle=-0{,}8-0{,}2=-1$, nên $\tilde y\langle w_0,x\rangle=1$. Theo (b),
$$
\partial\ell(w_0)=\{\alpha(2,1):\alpha\in[0,1]\}.
$$

**(d) Dưới gradient của $L_S$.**

**Bước 1: quan sát thứ nhất.** $\tilde y_1=1$ và $1-\langle0,(1,2)\rangle=1>0$, nên gradient tại $0$ là $-\tilde y_1x_1=(-1,-2)$.

**Bước 2: quan sát thứ hai.** $\tilde y_2=-1$ và $1+\langle0,(2,1)\rangle=1>0$, nên gradient tại $0$ là $-\tilde y_2x_2=(2,1)$.

**Bước 3: trung bình.** Theo Mệnh đề 05.3(b),
$$
\begin{aligned}
&\tfrac12\big[(-1,-2)+(2,1)\big]\\
&\quad=(0{,}5;-0{,}5)\in\partial L_S(0).
\end{aligned}
$$

**Kiểm tra lại.** Ở (c), với $\alpha=1{,}2$ và $u=w_0+x=(1{,}6;0{,}8)$, ta có $\ell(u)=1+4=5$, trong khi $\ell(w_0)+\langle1{,}2x,x\rangle=6>5$; vậy $1{,}2\,x\notin\partial\ell(w_0)$, khớp với (b). Ở (d), tại $u=(1,-1)$, cả hai hàm lỗi bằng $2$, nên $L_S(u)=2=L_S(0)+\langle(0{,}5;-0{,}5),u\rangle$.
:::

### Bài tập 05.2 (Bất đẳng thức một bước và vai của phép chiếu)

**Mức độ:** chứng minh, tính toán, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 1; chỗ dùng tính lồi của $W$ và điều kiện $u\in W$.

::: exercise Bài tập 05.2
Thiết lập gồm bốn thành phần.

- **Tập.** $W\subset\mathbb R^p$ khác rỗng, đóng, lồi.
- **Bước.** $w,g\in\mathbb R^p$ và $\eta>0$.
- **Điểm sau bước.** $w^+\in W$.
- **Điểm so sánh.** $u\in W$.

**(a)** Giả sử $\lVert w^+-u\rVert\le\lVert w-\eta g-u\rVert$. Chứng minh, không dùng chứng minh trong ghi chú, rằng
$$
\begin{aligned}
&\langle g,w-u\rangle\\
&\quad\le\frac{\lVert w-u\rVert^2-\lVert w^+-u\rVert^2}{2\eta}\\
&\qquad+\frac\eta2\lVert g\rVert^2 .
\end{aligned}
$$
Suy ra Mệnh đề 05.13 cho $w^+=\operatorname{proj}_W(w-\eta g)$ từ Bổ đề 05.8(b), và chỉ ra dòng duy nhất dùng phép chiếu và điều kiện $u\in W$. Chứng minh dấu bằng xảy ra khi $W=\mathbb R^p$.

**(b)** Trong $\mathbb R$, gọi $w^+$ là điểm gần $w-\eta g$ nhất trong $W$. Xét hai trường hợp:

- **Tập không lồi.** $W=\{-1,1\}$, $w=0$, $g=0{,}2$, $\eta=1$, $u=1$.
- **Điểm so sánh ngoài $W$.** $W=[-1,1]$, $w=1$, $g=-1$, $\eta=1$, $u=3$.

Với mỗi trường hợp, tính hai vế của bất đẳng thức ở (a) và chỉ ra các bất đẳng thức của Bổ đề 05.8(b) bị hỏng.

**(c)** Tại bước thứ ba của Ví dụ 05.6 với $i_3=1$ ($w=w_3\approx(0{,}7071;-0{,}7071)$, $g=g_3\approx(-0{,}5858;0)$, $\eta=0{,}5$, $W$ là quả cầu đơn vị), lấy $u=w^*$. Tính hai vế của Mệnh đề 05.13 và vế phải khi bỏ phép chiếu. Bước này đưa điểm lặp lại gần $u$ hay ra xa $u$?
:::

::: hint Gợi ý 1
Phần (a). Khai triển $\lVert(w-u)-\eta g\rVert^2$. Phần (b). Trường hợp đầu có $w-\eta g=-0{,}2$, trường hợp sau có $w-\eta g=2$. Phần (c). $w^+$ đã có trong Ví dụ 05.6, Bước 3.
:::

::: solution Lời giải Bài tập 05.2
**(a) Chứng minh.**

**Bước 1: giả thiết.** Bình phương giả thiết:
$$
\begin{aligned}
&\lVert w^+-u\rVert^2\\
&\quad\le\lVert w-\eta g-u\rVert^2 .
\end{aligned}
$$
Đây là chỗ duy nhất $w^+$ đi vào lập luận.

**Bước 2: khai triển.** Với $a=w-u$ và $a'=\eta g$,
$$
\begin{aligned}
&\lVert w-\eta g-u\rVert^2\\
&\quad=\lVert w-u\rVert^2-2\eta\langle g,w-u\rangle\\
&\qquad+\eta^2\lVert g\rVert^2 .
\end{aligned}
$$

**Bước 3: chuyển vế.** Ghép Bước 1 và Bước 2, chuyển $2\eta\langle g,w-u\rangle$ sang vế trái và $\lVert w^+-u\rVert^2$ sang vế phải, rồi chia cho $2\eta>0$.

**Bước 4: phép chiếu.** Theo Bổ đề 05.8(b) với $\theta=w-\eta g$ và $u\in W$, điểm $w^+=\operatorname{proj}_W(w-\eta g)$ thỏa giả thiết của (a). Đây là dòng duy nhất dùng phép chiếu, tính lồi của $W$ và điều kiện $u\in W$.

**Bước 5: dấu bằng.** Khi $W=\mathbb R^p$, $w^+=w-\eta g$, nên Bước 1 là đẳng thức, và Bước 2, Bước 3 cũng vậy.

**(b) Hai trường hợp hỏng.**

**Bước 1: tập không lồi.** $w-\eta g=-0{,}2$ cách $-1$ là $0{,}8$ và cách $1$ là $1{,}2$, nên $w^+=-1$. Hai vế là
$$
\begin{aligned}
&\langle g,w-u\rangle=0{,}2\cdot(-1)\\
&\quad=-0{,}2,\\
&\tfrac{1}{2\eta}\big(\lvert w-u\rvert^2-\lvert w^+-u\rvert^2\big)\\
&\quad=\tfrac{1-4}2=-1{,}5,\\
&\tfrac\eta2g^2=0{,}02 .
\end{aligned}
$$
Vế phải là $-1{,}48<-0{,}2$, nên bất đẳng thức sai.

**Bước 2: Bổ đề 05.8(b) trong trường hợp đầu.** Với $\theta=-0{,}2$, $\pi=-1$: $\lvert\pi-u\rvert^2=4$, trong khi $\lvert\theta-u\rvert^2-\lvert\theta-\pi\rvert^2=1{,}44-0{,}64=0{,}8$ và $\lvert\theta-u\rvert^2=1{,}44$. Cả hai bất đẳng thức của Bổ đề 05.8(b) đều hỏng; Mệnh đề 05.13 chỉ dùng bất đẳng thức thứ hai.

**Bước 3: điểm so sánh ngoài $W$.** $w-\eta g=2$, nên $w^+=1$. Vế trái là $(-1)(1-3)=2$. Vế phải là
$$
\begin{aligned}
&\tfrac{\lvert1-3\rvert^2-\lvert1-3\rvert^2}{2}+\tfrac12\cdot1\\
&\quad=0{,}5<2 .
\end{aligned}
$$

**Bước 4: Bổ đề 05.8(b) trong trường hợp sau.** Với $\theta=2$, $\pi=1$, $u=3\notin W$: $\lvert\pi-u\rvert^2=4$, trong khi $\lvert\theta-u\rvert^2-\lvert\theta-\pi\rvert^2=1-1=0$ và $\lvert\theta-u\rvert^2=1$. Cả hai bất đẳng thức hỏng; bổ đề chỉ đúng với $u\in W$.

**(c) Bước thứ ba với $i_3=1$.**

**Bước 1: vế trái.** $w-u\approx(-0{,}0402;-0{,}0427)$, nên $\langle g,w-u\rangle\approx(-0{,}5858)(-0{,}0402)\approx0{,}0236$.

**Bước 2: điểm sau bước.** $w-\eta g\approx(1;-0{,}7071)$ có chuẩn $1{,}2247>1$; theo Ví dụ 05.6, $w^+\approx(0{,}8165;-0{,}5774)$.

**Bước 3: ba khoảng cách.** Từ $w-u$ ở Bước 1, $\lVert w-u\rVert^2\approx0{,}00162+0{,}00182\approx0{,}00344$, tính với $w^*$ chưa làm tròn (Ví dụ 05.7 in $0{,}0034$). Ta có $w^+-u\approx(0{,}0692;0{,}0871)$, nên $\lVert w^+-u\rVert^2\approx0{,}01237$; và $(w-\eta g)-u\approx(0{,}2527;-0{,}0427)$, nên $\lVert w-\eta g-u\rVert^2\approx0{,}06566$.

**Bước 4: vế phải.** $\lVert g\rVert^2\approx0{,}3431$, nên $\tfrac\eta2\lVert g\rVert^2\approx0{,}08579$. Với $2\eta=1$,
$$
\begin{aligned}
&0{,}00344-0{,}01237+0{,}08579\\
&\quad\approx0{,}0769>0{,}0236 .
\end{aligned}
$$
Khi bỏ phép chiếu, vế phải là $0{,}00344-0{,}06566+0{,}08579\approx0{,}0236$, bằng vế trái như (a) khẳng định.

**Bước 5: ra xa $u$.** $\lVert w^+-u\rVert^2\approx0{,}01237>0{,}00344$, nên bước này đưa điểm lặp ra xa $w^*$. Bất đẳng thức vẫn đúng nhờ số hạng $\tfrac\eta2\lVert g\rVert^2$.

**Kiểm tra lại.** Hiệu hai vế phải ở (c) là $0{,}0769-0{,}0236=0{,}0533\approx0{,}06566-0{,}01237$, đúng bằng lượng phép chiếu làm giảm $\lVert\cdot-u\rVert^2$.
:::

### Bài tập 05.3 (Bước kì vọng có điều kiện trong chứng minh)

**Mức độ:** chứng minh, tính toán, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 2, 5; tính không chệch khi biết lịch sử, và điều xảy ra khi các lần rút phụ thuộc nhau.

::: exercise Bài tập 05.3
Thiết lập của Ví dụ 05.6 gồm bốn thành phần.

- **Mẫu và oracle.** Mẫu của Ví dụ 05.1 và oracle của Ví dụ 05.5; chỉ số rút đều có hoàn lại (sampling with replacement) trên $\{1,2,3\}$.
- **Tập tham số.** $W=\{w:\lVert w\rVert\le1\}$.
- **Thuật toán.** Thuật toán 05.11 với $w_1=0$ và $\eta=0{,}5$.
- **Điểm so sánh.** $u=w^*\approx(0{,}7473;-0{,}6645)$, với $L_S(w^*)\approx0{,}06112$ (Ví dụ 05.6, Bước 5).

**(a)** Cho $\Xi$ hữu hạn với $P_\xi(k)>0$ với mọi $k\in\Xi$. Không dẫn Bổ đề 05.12, viết $\mathbb E\langle g_2,w_2-u\rangle$ thành tổng kép theo $(k_1,k_2)\in\Xi^2$ và chứng minh
$$
\begin{aligned}
&\mathbb E\langle g_2,w_2-u\rangle\\
&\quad=\mathbb E\langle\psi(w_2),w_2-u\rangle .
\end{aligned}
$$
Chỉ ra chỗ dùng tính độc lập của $\xi_2$ với $\xi_1$, tính chất tháp và quy tắc lấy ra đại lượng đã biết.

**(b)** Trong thiết lập trên, tính ba giá trị có thể của $w_2$ và $\psi(w_2)$. Tính $\mathbb E\langle g_2,w_2-u\rangle$ bằng cách liệt kê chín cặp $(i_1,i_2)$ đồng khả năng, và bằng vế phải của (a). Tính thêm $\mathbb EL_S(w_2)$.

**(c)** Thay lần rút thứ hai bằng $i_2=i_1$. Tính $\mathbb E\langle g_2,w_2-u\rangle$. Chỉ ra giả thiết bị vi phạm và bước hỏng trong chứng minh Định lý 05.14.
:::

::: hint Gợi ý 1
Phần (a). $w_2$ là hàm của $\xi_1$: trên biến cố $\{\xi_1=k_1\}$, $w_2$ bằng một điểm cố định $w(k_1)$. Tính tổng theo $k_2$ trước. Phần (b). Mỗi $\lVert x_i\rVert=1$ và $2\eta=1$.
:::

::: hint Gợi ý 2
Phần (b). Các điểm $w_2$ là $(1,0)$, $(0,-1)$ và $0$. Phần (c). Với $2\eta\lVert x_i\rVert^2=1$, một bước theo quan sát $i$ làm phần dư của chính quan sát đó bằng $0$.
:::

::: solution Lời giải Bài tập 05.3
**(a) Tổng kép.**

**Bước 1: điểm lặp.** $w_2=\operatorname{proj}_W\big(w_1-\eta\varphi(w_1,\xi_1)\big)$ chỉ phụ thuộc $\xi_1$. Gọi $w(k_1)$ là giá trị của nó khi $\xi_1=k_1$. Khi đó $g_2=\varphi(w(k_1),\xi_2)$ trên biến cố $\{\xi_1=k_1\}$.

**Bước 2: tính độc lập.** Vì $\xi_1$, $\xi_2$ độc lập cùng phân bố $P_\xi$, $\Pr(\xi_1=k_1,\xi_2=k_2)=P_\xi(k_1)P_\xi(k_2)$. Do đó
$$
\begin{aligned}
&\mathbb E\langle g_2,w_2-u\rangle\\
&=\sum_{k_1}P_\xi(k_1)\\
&\quad\cdot\sum_{k_2}P_\xi(k_2)\\
&\qquad\cdot\langle\varphi(w(k_1),k_2),\\
&\qquad\quad w(k_1)-u\rangle .
\end{aligned}
$$
Tổng trong là $\mathbb E[\langle g_2,w_2-u\rangle\mid\xi_1=k_1]$; phân bố có điều kiện của $\xi_2$ vẫn là $P_\xi$ nhờ tính độc lập.

**Bước 3: lấy ra đại lượng đã biết.** Với $k_1$ cố định, $w(k_1)-u$ là véc-tơ hằng, nên tổng trong bằng
$$
\begin{aligned}
&\Big\langle\sum_{k_2}P_\xi(k_2)\varphi(w(k_1),k_2),\\
&\qquad w(k_1)-u\Big\rangle\\
&=\langle\psi(w(k_1)),w(k_1)-u\rangle .
\end{aligned}
$$

**Bước 4: tính chất tháp.** Tổng ngoài lấy trung bình các kì vọng có điều kiện theo trọng số $P_\xi(k_1)$, nên bằng $\mathbb E\langle\psi(w_2),w_2-u\rangle$. Với $t$ bất kì, cùng lập luận chạy với lịch sử $k_{1:t-1}$ thay cho $k_1$.

**(b) Chín cặp.**

**Bước 1: ba giá trị của $w_2$.** Theo Ví dụ 05.5, $g_1=\varphi(0,i_1)=-2y_{i_1}x_{i_1}$, nên $w_1-\eta g_1=y_{i_1}x_{i_1}$:

- **$i_1=1$.** Điểm $(1,0)$, chuẩn $1$, nên $w_2=(1,0)$.
- **$i_1=2$.** Điểm $(0,-1)$, chuẩn $1$, nên $w_2=(0,-1)$.
- **$i_1=3$.** $y_3=0$, nên $w_2=0$.

**Bước 2: trung bình của oracle.** Với phần dư $r_i=\langle w_2,x_i\rangle-y_i$, ta có $\psi(w_2)=\tfrac23\sum_ir_ix_i$.

- **$w_2=(1,0)$.** Phần dư $0$; $1$; $0{,}6$, nên $\psi=\tfrac23\big[(0,1)+0{,}6\,(0{,}6;0{,}8)\big]=\tfrac23(0{,}36;1{,}48)\approx(0{,}24;0{,}9867)$.
- **$w_2=(0,-1)$.** Phần dư $-1$; $0$; $-0{,}8$, nên $\psi=\tfrac23\big[-(1,0)-0{,}8\,(0{,}6;0{,}8)\big]=\tfrac23(-1{,}48;-0{,}64)\approx(-0{,}9867;-0{,}4267)$.
- **$w_2=0$.** Phần dư $-1$; $1$; $0$, nên $\psi=\tfrac23(-1,1)=\big(-\tfrac23,\tfrac23\big)$.

**Bước 3: một ô tính đủ.** Lấy $(i_1,i_2)=(1,2)$. Khi đó $w_2=(1,0)$, $g_2=\varphi(w_2,2)=2(0+1)(0,1)=(0,2)$ và $w_2-u\approx(0{,}2527;0{,}6645)$, nên
$$
\begin{aligned}
\langle g_2,w_2-u\rangle&\approx2\cdot0{,}6645\\
&\approx1{,}3289 .
\end{aligned}
$$

**Bước 4: đường chéo.** Khi $i_2=i_1$, bước thứ nhất đã đưa phần dư của quan sát $i_1$ về $0$ (vì $2\eta\lVert x_{i_1}\rVert^2=1$, xem (c)), nên $g_2=0$ và ô bằng $0$.

**Bước 5: chín ô.** Tính như Bước 3 với $w^*$ chưa làm tròn, theo $i_2=1,2,3$:
$$
\begin{aligned}
i_1=1:&\ \ 0;\ 1{,}3289;\ 0{,}8198,\\
i_1=2:&\ \ 1{,}4947;\ 0;\ 1{,}1469,\\
i_1=3:&\ \ 1{,}4947;\ 1{,}3289;\ 0 .
\end{aligned}
$$
Tổng chín ô là $7{,}6139$, nên $\mathbb E\langle g_2,w_2-u\rangle\approx7{,}6139/9\approx0{,}8460$.

**Bước 6: vế phải của (a).** Trung bình theo hàng cho $\langle\psi(w_2),w_2-u\rangle$; chẳng hạn hàng đầu là $(0+1{,}3289+0{,}8198)/3\approx0{,}7162$. Ba hàng cho $0{,}7162$; $0{,}8805$; $0{,}9412$, với trung bình $2{,}5379/3\approx0{,}8460$, khớp Bước 5.

**Bước 7: rủi ro thực nghiệm.** $L_S(1,0)\approx0{,}4533$ (Ví dụ 05.6), $L_S(0,-1)=\tfrac13(1+0+0{,}64)\approx0{,}5467$ và $L_S(0)\approx0{,}6667$. Vậy $\mathbb EL_S(w_2)\approx1{,}6667/3\approx0{,}5556$.

**(c) Lần rút thứ hai phụ thuộc lần thứ nhất.**

**Bước 1: giá trị.** Với $i_2=i_1=i$, ta có $w_2=w_1-2\eta(\langle w_1,x_i\rangle-y_i)x_i$ (phép chiếu không tác động), nên
$$
\begin{aligned}
&\langle w_2,x_i\rangle-y_i\\
&\quad=(\langle w_1,x_i\rangle-y_i)\\
&\qquad\cdot(1-2\eta\lVert x_i\rVert^2)\\
&\quad=0 .
\end{aligned}
$$
Do đó $g_2=0$ và $\mathbb E\langle g_2,w_2-u\rangle=0$: đó là đường chéo ở (b).

**Bước 2: giả thiết bị vi phạm.** $i_2$ vẫn có phân bố đều, nhưng không độc lập với $i_1$, trái với Định nghĩa 05.10 (các lần rút độc lập) và dòng 1 của Thuật toán 05.11. Khi đó $\mathbb E[g_2\mid\mathcal F_1]=\varphi(w_2,i_1)\ne\psi(w_2)$, nên Bổ đề 05.12(b) hỏng.

**Bước 3: bước hỏng.** Bước 3 của chứng minh Định lý 05.14 cần $\mathbb E\langle g_2,w_2-u\rangle\ge\mathbb E L_S(w_2)-L_S(u)$. Ở đây vế trái là $0$, vế phải là $0{,}5556-0{,}06112\approx0{,}4944$.

**Kiểm tra lại.** Ô $(1,2)$ là vế trái $1{,}3289$ của Ví dụ 05.7. Ở (b), bất đẳng thức dưới gradient cho $\mathbb E\langle\psi(w_2),w_2-u\rangle\ge0{,}4944$, và $0{,}8460$ thỏa điều này.
:::

### Bài tập 05.4 (Chọn độ dài bước từ cận)

**Mức độ:** tính toán, khái niệm. **Mục tiêu:** mục tiêu học tập 3; độ dài bước, số vòng lặp và hằng số $G$ chưa biết chính xác.

::: exercise Bài tập 05.4
Với $R,G>0$ và $\lVert w_1-u\rVert=R$, vế phải của Định lý 05.14 là
$$
Q(\eta,T)=\frac{R^2}{2\eta T}+\frac{\eta G^2}2 .
$$

**(a)** Với $a,b>0$, tìm giá trị nhỏ nhất của $a/\eta+b\eta$ trên $\eta>0$ và điểm đạt nó. Suy ra độ dài bước và cận của Hệ quả 05.15.

**(b)** Cố định $\eta>0$ không phụ thuộc $T$ và $\epsilon>0$. Chứng minh có $T$ với $Q(\eta,T)\le\epsilon$ khi và chỉ khi $\eta<2\epsilon/G^2$, và tìm $T$ nhỏ nhất. Với $R=1$, $G=4$, $\epsilon=0{,}1$ (Ví dụ 05.8), tính kết quả khi $\eta=0{,}01$ và $\eta=0{,}0125$. Tìm $\eta$ làm $T$ nhỏ nhất.

**(c)** Chỉ biết một ước lượng $\hat G$ của $G$. Người dùng chọn $T=\lceil R^2\hat G^2/\epsilon^2\rceil$ và $\eta=R/(\hat G\sqrt T)$. Với $R=1$, $G=4$, $\epsilon=0{,}1$, tính $T$, $\eta$ và $Q(\eta,T)$ khi $\hat G=8$ và khi $\hat G=2$. Trường hợp nào giữ được bảo đảm $\epsilon$?
:::

::: hint Gợi ý 1
Phần (a). Bất đẳng thức giữa trung bình cộng và trung bình nhân (AM–GM) cho hai số dương $a/\eta$ và $b\eta$. Phần (b). Số hạng $\eta G^2/2$ không giảm theo $T$.
:::

::: hint Gợi ý 2
Phần (b). Khi $\eta<2\epsilon/G^2$, điều kiện $Q\le\epsilon$ tương đương $T\ge R^2/\big(\eta(2\epsilon-\eta G^2)\big)$; cực đại mẫu số theo $\eta$.
:::

::: solution Lời giải Bài tập 05.4
**(a) Độ dài bước tối ưu.**

**Bước 1: AM–GM.** Với $\eta>0$,
$$
\begin{aligned}
\frac a\eta+b\eta&\ge2\sqrt{\frac a\eta\cdot b\eta}\\
&=2\sqrt{ab},
\end{aligned}
$$
với dấu bằng khi và chỉ khi $a/\eta=b\eta$, tức $\eta=\sqrt{a/b}$.

**Bước 2: thay hằng số.** Với $a=R^2/(2T)$ và $b=G^2/2$, ta được $\eta^*=\sqrt{R^2/(TG^2)}=R/(G\sqrt T)$ và giá trị nhỏ nhất $2\sqrt{R^2G^2/(4T)}=RG/\sqrt T$, đúng như Hệ quả 05.15(a).

**(b) Độ dài bước cố định.**

**Bước 1: điều kiện cần.** Với mọi $T$, $Q(\eta,T)>\eta G^2/2$. Nếu $\eta\ge2\epsilon/G^2$ thì $\eta G^2/2\ge\epsilon$, nên $Q(\eta,T)>\epsilon$ với mọi $T$.

**Bước 2: số vòng lặp.** Nếu $\eta<2\epsilon/G^2$, điều kiện $Q(\eta,T)\le\epsilon$ tương đương $R^2/(2\eta T)\le\epsilon-\eta G^2/2$, tức
$$
T\ge T_\eta=\frac{R^2}{\eta(2\epsilon-\eta G^2)} .
$$
Số vòng lặp nhỏ nhất là $\lceil T_\eta\rceil$.

**Bước 3: bằng số.** Ngưỡng là $2\epsilon/G^2=0{,}2/16=0{,}0125$.

- **$\eta=0{,}01$.** Số hạng $\eta G^2/2=0{,}08$, $2\epsilon-\eta G^2=0{,}2-0{,}16=0{,}04$, và $T_\eta=1/(0{,}01\cdot0{,}04)=2500$.
- **$\eta=0{,}0125$.** Số hạng $\eta G^2/2=0{,}1=\epsilon$, nên không $T$ nào đủ.

**Bước 4: độ dài bước tốt nhất.** Mẫu số $\eta(2\epsilon-\eta G^2)$ là một parabol theo $\eta$, đạt cực đại $\epsilon^2/G^2$ tại $\eta=\epsilon/G^2=0{,}00625$. Khi đó $T_\eta=R^2G^2/\epsilon^2=1600$, đúng như Ví dụ 05.8.

**(c) Ước lượng sai hằng số $G$.**

**Bước 1: $\hat G=8$.** $T=64/0{,}01=6400$, $\sqrt T=80$, $\eta=1/(8\cdot80)=0{,}0015625$. Khi đó
$$
\begin{aligned}
Q&=\frac1{2\cdot0{,}0015625\cdot6400}\\
&\quad+\frac{0{,}0015625\cdot16}2\\
&=0{,}05+0{,}0125=0{,}0625 .
\end{aligned}
$$

**Bước 2: $\hat G=2$.** $T=4/0{,}01=400$, $\sqrt T=20$, $\eta=1/(2\cdot20)=0{,}025$. Khi đó
$$
\begin{aligned}
Q&=\frac1{2\cdot0{,}025\cdot400}\\
&\quad+\frac{0{,}025\cdot16}2\\
&=0{,}05+0{,}2=0{,}25 .
\end{aligned}
$$

**Bước 3: kết luận.** Với $\hat G=8$, cận $0{,}0625\le0{,}1$ vẫn đúng, đổi lại số vòng lặp gấp $(\hat G/G)^2=4$ lần. Với $\hat G=2$, số hạng $\eta G^2/2=0{,}2$ đã vượt $\epsilon$, nên bảo đảm mất. Đánh giá thấp $G$ làm mất bảo đảm; đánh giá cao chỉ làm tăng số vòng lặp.

**Kiểm tra lại.** Ở (c), $\eta$ bằng $\eta^*(T)$ nhân $\gamma=G/\hat G$, tức $\gamma=\tfrac12$ hoặc $2$. Theo Ví dụ 05.8, Bước 4, $Q=\tfrac{RG}{\sqrt T}\cdot1{,}25$, cho $\tfrac4{80}\cdot1{,}25=0{,}0625$ và $\tfrac4{20}\cdot1{,}25=0{,}25$.
:::

### Bài tập 05.5 (Số lần cập nhật và số quan sát của GD, SGD và lô nhỏ)

**Mức độ:** tính toán, khái niệm. **Mục tiêu:** mục tiêu học tập 3, 4; so sánh theo cận, và giá của bảo đảm với xác suất cao.

::: exercise Bài tập 05.5
Thiết lập theo Ví dụ 05.15, trừ phương sai $\sigma^2$: $G_F^2=1$, $R=1$, $m=10^4$, $\epsilon=0{,}1$, và số bước của lô cỡ $b$
$$
T(b)=\Big\lceil\frac{R^2(G_F^2+\sigma^2/b)}{\epsilon^2}\Big\rceil .
$$
GD cần $R^2G_F^2/\epsilon^2$ bước (Hệ quả 05.16 với $G=G_F$).

**(a)** Lấy $\sigma^2=3$ (giá trị giả định, khác $\sigma^2=15$ của Ví dụ 05.15). Lập bảng số bước và số quan sát cho $b=1,3,16,64$ và cho GD. Từ kích thước lô nào số bước gần như không giảm nữa? So với Ví dụ 05.15.

**(b)** Chứng minh $T(b)$ không quá $1{,}1$ lần số bước của GD khi và chỉ khi $b\ge10\,\sigma^2/G_F^2$. Tính $b$ nhỏ nhất và số quan sát khi đó, với $\sigma^2=3$ và với $\sigma^2=15$.

**(c)** Tại một $w$ cố định, bốn quan sát cho gradient một chiều $\varphi(w,i)=1,2,4,9$, với $i$ rút đều; lấy $b=2$.

- **(c1)** Tính phương sai của gradient lô khi hai chỉ số rút độc lập có hoàn lại, và khi rút một cặp không hoàn lại (sampling without replacement), liệt kê sáu cặp.
- **(c2)** Gradient lô không hoàn lại có không chệch không? Giả thiết nào của Mệnh đề 05.20 không thỏa, và kết luận (b) của mệnh đề còn đúng không?

**(d)** Lấy $R=1$, $G=4$, $\epsilon_{\mathrm{opt}}=0{,}1$, $\delta'=0{,}05$ như Ví dụ 05.14. Chạy SGD có chiếu $k$ lần độc lập trên cùng mẫu $S$, mỗi lần với số bước đủ cho $\mathbb E_\xi\operatorname{opt}_S\le\epsilon_{\mathrm{opt}}/2$, rồi giữ đầu ra có $L_S$ nhỏ nhất ($L_S$ tính chính xác, $m$ lần tính hàm lỗi mỗi đầu ra). Chứng minh xác suất để đầu ra được giữ có $\operatorname{opt}_S\ge\epsilon_{\mathrm{opt}}$ không quá $2^{-k}$. Tìm $k$ nhỏ nhất, tổng số bước SGD, và so với $640\,000$ bước của Ví dụ 05.14.
:::

::: hint Gợi ý 1
Phần (a). Số quan sát là $bT(b)\approx R^2(bG_F^2+\sigma^2)/\epsilon^2$. Phần (c). Với rút không hoàn lại, khi biết phần tử thứ nhất, phần tử thứ hai đều trên ba giá trị còn lại. Phần (d). Áp dụng bất đẳng thức Markov cho từng lần chạy, rồi dùng tính độc lập giữa các lần chạy.
:::

::: hint Gợi ý 2
Phần (d). Mọi đầu ra có cùng số trừ $\inf_WL_S$, nên đầu ra có $L_S$ nhỏ nhất cũng có $\operatorname{opt}_S$ nhỏ nhất.
:::

::: solution Lời giải Bài tập 05.5
**(a) Bảng với $\sigma^2=3$.**

**Bước 1: công thức.** $R^2/\epsilon^2=100$, nên $T(b)=\lceil100(1+3/b)\rceil$. Chẳng hạn $T(16)=\lceil100\cdot1{,}1875\rceil=\lceil118{,}75\rceil=119$.

**Bước 2: bảng.** GD cần $100$ bước, mỗi bước $m=10^4$ quan sát.

| $b$ | $T(b)$ | Số quan sát |
|---|---|---|
| $1$ | $400$ | $400$ |
| $3$ | $200$ | $600$ |
| $16$ | $119$ | $1904$ |
| $64$ | $105$ | $6720$ |
| GD | $100$ | $10^6$ |

**Bước 3: đọc bảng.** Số bước giảm nhanh đến $b=\sigma^2/G_F^2=3$, tại đó $T(3)=200$, gấp đôi số bước của GD. Sau đó phần vượt $T(b)-100\approx300/b$ giảm theo $1/b$: còn $19$ ở $b=16$ và $5$ ở $b=64$. Số quan sát $bT(b)\approx100(b+3)$ tăng gần tuyến tính theo $b$. Ở Ví dụ 05.15, với $\sigma^2=15$, điểm đổi chiều là $b\approx15$. Phương sai nhỏ hơn thì lô nhỏ hơn đã gần số bước của GD.

**(b) Lô gần bằng GD.**

**Bước 1: điều kiện.** Số bước của GD là $100$, một số nguyên, nên $T(b)\le110$ khi và chỉ khi $100(1+\sigma^2/b)\le110$, tức $\sigma^2/b\le0{,}1$, tức $b\ge10\,\sigma^2$ (với $G_F^2=1$).

**Bước 2: $\sigma^2=3$.** $b=30$, $T(30)=110$, số quan sát $30\cdot110=3300$.

**Bước 3: $\sigma^2=15$.** $b=150$, $T(150)=110$, số quan sát $150\cdot110=16\,500$. Cả hai còn nhỏ hơn nhiều so với $10^6$ quan sát của GD.

**(c) Rút không hoàn lại.**

**Bước 1: một lần rút.** Trung bình là $(1+2+4+9)/4=4$. Các độ lệch là $-3,-2,0,5$, nên $\sigma^2=(9+4+0+25)/4=9{,}5$.

**Bước 2: có hoàn lại.** Hai lần rút độc lập, nên số hạng chéo ở Bước 2 của chứng minh Mệnh đề 05.20 bằng $0$, và đẳng thức ở bước đó cho phương sai của lô là $9{,}5/2=4{,}75$.

**Bước 3: không hoàn lại.** Sáu cặp đồng khả năng có trung bình $1{,}5$; $2{,}5$; $5$; $3$; $5{,}5$; $6{,}5$. Trung bình của chúng là $24/6=4$, nên gradient lô không chệch. Độ lệch bình phương là $6{,}25$; $2{,}25$; $1$; $1$; $2{,}25$; $6{,}25$, nên phương sai là $19/6\approx3{,}1667$.

**Bước 4: hiệp phương sai.** Hai phần tử của lô không độc lập, nên giả thiết của Mệnh đề 05.20 không thỏa.

- **Độ lệch.** Gọi $e_1$, $e_2$ là độ lệch của hai phần tử khỏi $4$.
- **Kì vọng có điều kiện.** Tổng bốn độ lệch bằng $0$, nên khi biết $e_1$, kì vọng của $e_2$ là $-e_1/3$.
- **Hiệp phương sai.** Do đó $\mathbb Ee_1e_2=-\mathbb Ee_1^2/3=-\sigma^2/3\approx-3{,}1667$.

**Bước 5: kết luận (b) của mệnh đề.** Chứng minh Mệnh đề 05.20(b) chỉ cần $\mathbb Ee_1e_2\le0$ để có cận $\sigma^2/b$. Ở đây
$$
\begin{aligned}
&\tfrac14\big(2\sigma^2+2\,\mathbb Ee_1e_2\big)\\
&\quad=\tfrac14(19-6{,}3333)\\
&\quad\approx3{,}1667\le4{,}75 .
\end{aligned}
$$
Kết luận (b) vẫn đúng, dù giả thiết độc lập không thỏa.

**(d) Nhiều lần chạy.**

**Bước 1: một lần chạy.** Gọi $X_j=\operatorname{opt}_S$ của đầu ra lần chạy $j$. Vì đầu ra thuộc $W$, $X_j\ge0$, và $\mathbb EX_j\le\epsilon_{\mathrm{opt}}/2$. Theo bất đẳng thức Markov (Bổ đề 02.2), $\Pr(X_j\ge\epsilon_{\mathrm{opt}})\le\tfrac12$.

**Bước 2: đầu ra được giữ.** $\operatorname{opt}_S=L_S-\inf_WL_S$ với cùng số trừ, nên đầu ra được giữ có $\operatorname{opt}_S=\min_jX_j$. Biến cố $\{\min_jX_j\ge\epsilon_{\mathrm{opt}}\}$ là giao của $k$ biến cố $\{X_j\ge\epsilon_{\mathrm{opt}}\}$, độc lập vì các lần chạy dùng các lần rút độc lập. Do đó xác suất của nó không quá $2^{-k}$.

**Bước 3: số lần chạy.** $2^{-k}\le0{,}05$ tương đương $k\ge\log_220\approx4{,}32$, nên $k=5$ và $2^{-5}=0{,}03125$.

**Bước 4: chi phí.** Mỗi lần chạy cần $T=R^2G^2/(\epsilon_{\mathrm{opt}}/2)^2=16/0{,}0025=6400$ bước. Tổng là $5\cdot6400=32\,000$ bước, cộng $5m$ lần tính hàm lỗi để so $L_S$. Nếu một lần tính hàm lỗi tốn ngang một gradient trên một quan sát, cách này rẻ hơn $640\,000$ bước khi $32\,000+5m<640\,000$, tức $m<121\,600$.

**Kiểm tra lại.** Ở (a), $T(3)=\lceil100\cdot2\rceil=200$. Ở (b), $1+3/30=1{,}1$ đúng bằng ngưỡng. Ở (d), $k=4$ cho $2^{-4}=0{,}0625>0{,}05$, nên $k=5$ là nhỏ nhất.
:::

### Bài tập 05.6 (Mức sàn sai số với độ dài bước hằng, thực nghiệm tùy chọn)

**Mức độ:** chứng minh, tính toán, kiểm tra giả thiết, thực nghiệm (tùy chọn). **Mục tiêu:** mục tiêu học tập 5; điểm lặp cuối so với điểm lặp trung bình, và oracle không có cận mô-men bậc hai.

::: exercise Bài tập 05.6
Thiết lập gồm năm thành phần.

- **Hàm mục tiêu.** $F(w)=\tfrac a2w^2$ trên $\mathbb R$, với $a>0$; $\min F=0$ tại $w=0$.
- **Tập tham số.** $W=\mathbb R$, không chiếu.
- **Oracle.** Gradient ngẫu nhiên $g_t=aw_t+\nu_t$.
- **Nhiễu.** Nhiễu gradient $\nu_1,\nu_2,\ldots$ độc lập, cùng phân bố, $\mathbb E\nu_t=0$, $\operatorname{Var}\nu_t=\sigma^2>0$.
- **Độ dài bước và khởi tạo.** $\eta\in(0,2/a)$ hằng, $w_1$ tất định; đặt $r=1-\eta a$.

**(a)** Chứng minh $q_t=\mathbb Ew_t^2$ thỏa $q_{t+1}=r^2q_t+\eta^2\sigma^2$.

**(b)** Chứng minh $q_t\to q_\infty=\eta\sigma^2/\big(a(2-\eta a)\big)$, và tính giới hạn của $\mathbb EF(w_t)$, tức mức sàn sai số (error floor) của điểm lặp cuối. Tính giới hạn này với $a=\sigma^2=1$ và $\eta=0{,}1$; $0{,}05$; $0{,}01$, và so với $\eta\sigma^2/4$.

**(c)** Với $w_1=0$, chứng minh
$$
\begin{aligned}
\bar w_T&=-\frac1{aT}\sum_{s=1}^{T-1}\big(1-r^{T-s}\big)\nu_s,\\
\mathbb E\bar w_T^2&=\frac{\sigma^2}{a^2T^2}\sum_{k=1}^{T-1}(1-r^k)^2 .
\end{aligned}
$$
Tính $\mathbb E\bar w_T^2$ với $a=\sigma^2=1$, $\eta=0{,}1$, $T=2000$, và so với $\sigma^2/(a^2T)$.

**(d)** Vì sao Định lý 05.14 không áp dụng trực tiếp cho oracle này trên $\mathbb R$? Với $W=[-1,1]$ có chiếu và $a=\sigma^2=1$, tính hằng số $G$ nhỏ nhất của (G2) và số hạng $\eta G^2/2$ của cận tại $\eta=0{,}1$.

**(e)** Thay $\nu_t$ bằng biến ngẫu nhiên nhận giá trị nguyên khác $0$ với $\Pr(\nu=k)=\Pr(\nu=-k)=c/k^3$, $k=1,2,\ldots$, trong đó $c=1/(2\zeta(3))$ và $\zeta(3)=\sum_{k\ge1}k^{-3}\approx1{,}2021$. Chứng minh (G1) đúng và $\mathbb Eg_t^2=\infty$ tại mọi $w_t$, kể cả khi $w_t\in[-1,1]$. Chứng minh rằng, không chiếu, $\mathbb EF(\bar w_T)=\infty$ với mọi $T\ge2$ và mọi $\eta>0$. Có chiếu lên $W=[-1,1]$, Định lý 05.14 cho được cận nào?

**(f)** (Thực nghiệm, tùy chọn.) Viết giao thức kiểm tra (b), (c) và (e) bằng mô phỏng: tham số, số lần chạy, đại lượng báo cáo, điều được kết luận.
:::

::: hint Gợi ý 1
Phần (a). $w_{t+1}=r w_t-\eta\nu_t$, và $w_t$ chỉ phụ thuộc $\nu_1,\ldots,\nu_{t-1}$. Phần (c). Viết $w_t$ theo $\nu_1,\ldots,\nu_{t-1}$, đổi thứ tự hai tổng, dùng $1-r=\eta a$.
:::

::: hint Gợi ý 2
Phần (e). $\sum_kk^{-2}<\infty$ nhưng $\sum_kk^{-1}=\infty$. Trong $\bar w_T$, chỉ $w_T$ chứa $\nu_{T-1}$; lấy kì vọng có điều kiện khi biết $\nu_1,\ldots,\nu_{T-2}$.
:::

::: solution Lời giải Bài tập 05.6
**(a) Truy hồi.**

**Bước 1: cập nhật.** $w_{t+1}=w_t-\eta(aw_t+\nu_t)=r w_t-\eta\nu_t$.

**Bước 2: bình phương.** Theo quy nạp, $w_t$ là hàm của $\nu_1,\ldots,\nu_{t-1}$ với $\mathbb Ew_t^2<\infty$, nên độc lập với $\nu_t$ và $\mathbb E[w_t\nu_t]=\mathbb Ew_t\cdot\mathbb E\nu_t=0$. Do đó
$$
\begin{aligned}
q_{t+1}&=r^2q_t-2r\eta\,\mathbb E[w_t\nu_t]\\
&\quad+\eta^2\mathbb E\nu_t^2\\
&=r^2q_t+\eta^2\sigma^2 .
\end{aligned}
$$

**(b) Mức sàn sai số.**

**Bước 1: điểm bất động.** $q_\infty=r^2q_\infty+\eta^2\sigma^2$ cho $q_\infty=\eta^2\sigma^2/(1-r^2)$. Vì $1-r^2=\eta a(2-\eta a)$, ta được $q_\infty=\eta\sigma^2/\big(a(2-\eta a)\big)$.

**Bước 2: hội tụ.** Trừ hai đẳng thức, $q_{t+1}-q_\infty=r^2(q_t-q_\infty)$. Với $\eta\in(0,2/a)$, $\lvert r\rvert<1$, nên $q_t\to q_\infty$ với mọi $w_1$.

**Bước 3: giá trị hàm.** $\mathbb EF(w_t)=\tfrac a2q_t$, nên
$$
\mathbb EF(w_t)\to\frac{\eta\sigma^2}{2(2-\eta a)} .
$$
Đây là mức sàn sai số của điểm lặp cuối: $\mathbb EF(w_t)$ không về $\min F=0$.

**Bước 4: bằng số.** Với $a=\sigma^2=1$:

- **$\eta=0{,}1$.** $0{,}1/(2\cdot1{,}9)\approx0{,}02632$, so với $\eta\sigma^2/4=0{,}025$.
- **$\eta=0{,}05$.** $0{,}05/(2\cdot1{,}95)\approx0{,}01282$, so với $0{,}0125$.
- **$\eta=0{,}01$.** $0{,}01/(2\cdot1{,}99)\approx0{,}002513$, so với $0{,}0025$.

Mức sàn tỉ lệ với $\eta$ khi $\eta$ nhỏ, và chia đôi $\eta$ thì mức sàn giảm khoảng một nửa.

**(c) Điểm lặp trung bình.**

**Bước 1: nghiệm của truy hồi.** Với $w_1=0$, quy nạp theo Bước 1 của (a) cho
$$
w_t=-\eta\sum_{s=1}^{t-1}r^{t-1-s}\nu_s .
$$

**Bước 2: đổi thứ tự tổng.** Số hạng $\nu_s$ có mặt trong $w_{s+1},\ldots,w_T$, nên
$$
\begin{aligned}
\sum_{t=1}^Tw_t&=-\eta\sum_{s=1}^{T-1}\nu_s\sum_{j=0}^{T-1-s}r^j\\
&=-\eta\sum_{s=1}^{T-1}\nu_s\frac{1-r^{T-s}}{1-r}.
\end{aligned}
$$
Chia cho $T$ và dùng $1-r=\eta a$, ta được công thức của $\bar w_T$.

**Bước 3: mô-men bậc hai.** Các $\nu_s$ độc lập, kì vọng $0$, nên các số hạng chéo có kì vọng $0$, và
$$
\mathbb E\bar w_T^2=\frac{\sigma^2}{a^2T^2}\sum_{s=1}^{T-1}(1-r^{T-s})^2 .
$$
Đổi chỉ số $k=T-s$ cho dạng cần chứng minh.

**Bước 4: bằng số.** Với $r=0{,}9$ và $T=2000$, khai triển bình phương và cộng ba cấp số nhân:
$$
\begin{aligned}
&\sum_{k=1}^{1999}(1-0{,}9^k)^2\\
&\quad\approx1999-2\cdot\frac{0{,}9}{0{,}1}+\frac{0{,}81}{0{,}19}\\
&\quad\approx1985{,}26,
\end{aligned}
$$
vì $0{,}9^{1999}$ không đáng kể. Do đó $\mathbb E\bar w_T^2\approx1985{,}26/(4\cdot10^6)\approx0{,}000496$, gần $\sigma^2/(a^2T)=0{,}0005$, và $\mathbb EF(\bar w_T)\approx0{,}000248$.

**Bước 5: so sánh.** Với cùng $\eta=0{,}1$, điểm lặp cuối dừng ở mức $0{,}02632$, còn $\mathbb EF(\bar w_T)$ giảm như $1/T$. Lấy trung bình xóa mức sàn.

**(d) Giả thiết (G2).**

**Bước 1: trên $\mathbb R$.** $\mathbb E_\nu(aw+\nu)^2=a^2w^2+\sigma^2$ không bị chặn trên $\mathbb R$, nên (G2) không đúng với hằng số $G$ nào.

**Bước 2: trên $[-1,1]$.** $\sup_{\lvert w\rvert\le1}(a^2w^2+\sigma^2)=2$, nên $G=\sqrt2\approx1{,}4142$ và $\eta G^2/2=0{,}1$ tại $\eta=0{,}1$. Số hạng này của cận cùng tỉ lệ với $\eta$ như mức sàn $0{,}02632$ ở (b), và lớn hơn khoảng bốn lần.

**(e) Nhiễu không có mô-men bậc hai.**

**Bước 1: (G1).** $\mathbb E\lvert\nu\rvert=2c\sum_kk^{-2}=\zeta(2)/\zeta(3)\approx1{,}3684<\infty$, và $\mathbb E\nu=0$ do đối xứng. Do đó $\psi(w)=aw=F'(w)$, tức (G1) đúng.

**Bước 2: (G2) hỏng.** $\mathbb E\nu^2=2c\sum_kk^{-1}=\infty$. Với $w$ cố định, $(aw+\nu)^2\ge\tfrac12\nu^2-a^2w^2$, nên $\mathbb E(aw+\nu)^2=\infty$, kể cả khi $\lvert w\rvert\le1$.

**Bước 3: không chiếu.** Với $T\ge2$, chỉ $w_T=r w_{T-1}-\eta\nu_{T-1}$ chứa $\nu_{T-1}$, nên $\bar w_T=X-\tfrac\eta T\nu_{T-1}$, với $X$ là hàm của $\nu_1,\ldots,\nu_{T-2}$, độc lập với $\nu_{T-1}$. Khi biết $X=x$, Bước 2 với $\tfrac\eta T\nu$ thay cho $\nu$ cho $\mathbb E\big(x-\tfrac\eta T\nu_{T-1}\big)^2=\infty$. Theo tính chất tháp, $\mathbb E\bar w_T^2=\infty$, nên $\mathbb EF(\bar w_T)=\infty$.

**Bước 4: có chiếu.** Mọi điểm lặp và $\bar w_T$ thuộc $[-1,1]$, nên $\mathbb EF(\bar w_T)\le a/2$. Bước 2 cho thấy (G2) không đúng với $G$ hữu hạn nào, nên Bước 4 của chứng minh Định lý 05.14 không thực hiện được và định lý không cho cận nào. Cận $a/2$ chỉ đến từ tính bị chặn của $W$.

**(f) Giao thức thực nghiệm.**

- **Tham số.** Ghi trước: $a$, $\sigma^2$, các giá trị $\eta$, $T$, $w_1$, phân bố nhiễu (chẳng hạn phân bố chuẩn (normal distribution) cho (b), (c); phân bố của (e)), hạt giống ngẫu nhiên.
- **Lặp.** $N\ge100$ lần chạy độc lập; mỗi lần ghi $F(w_t)$ và $F(\bar w_t)$ trên một lưới các $t$.
- **Báo cáo.** Tại mỗi $t$: trung bình, độ lệch chuẩn và sai số chuẩn của trung bình qua $N$ lần chạy. Với nhiễu của (e), báo cáo thêm trung vị và các phân vị: trung bình mẫu của một đại lượng có kì vọng vô hạn không ổn định khi tăng $N$.
- **Kết luận.** Chỉ so trung bình mẫu với các giá trị tính được ở (b), (c), trong phạm vi vài sai số chuẩn. Với nhiễu của (e), chỉ mô tả trung vị và phân vị của $F(\bar w_t)$; không kết luận về $\mathbb EF(\bar w_t)$ từ trung bình mẫu. Đường cong là minh họa, không phải chứng minh, kể cả cho các tham số đã chọn.

**Kiểm tra lại.** Ở (a), với $w_1=0$, $q_2=\eta^2\sigma^2=0{,}01$ khi $\eta=0{,}1$, $\sigma^2=1$, khớp $\mathbb E(\eta\nu_1)^2$. Ở (b), $q_\infty=0{,}0526$ gấp khoảng $106$ lần $\mathbb E\bar w_{2000}^2=0{,}000496$.
:::

## Bài tập chọn từ UML

### Bài tập 05.7 (Cực tiểu địa phương của rủi ro thực nghiệm với hàm lỗi 0–1; UML Bài tập 12.1)

**Mức độ:** khái niệm, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 5; bỏ tính lồi thì cực tiểu địa phương không còn là cực tiểu toàn cục.

::: exercise Bài tập 05.7
Lấy $\mathcal X=\mathbb R^2$, nhãn $y\in\{0,1\}$, hàm phân lớp $h_{w,0}(x)=\mathbb 1[\langle w,x\rangle\ge0]$ (Định nghĩa 03.7) và hàm lỗi 0–1. Xem $L_S(w)=\frac1m\sum_i\mathbb 1[h_{w,0}(x_i)\ne y_i]$ là hàm của $w\in\mathbb R^2$. Điểm $w$ là *cực tiểu địa phương* (local minimum) của $L_S$ nếu có $\epsilon>0$ sao cho $L_S(w)\le L_S(w')$ với mọi $w'$ thỏa $\lVert w'-w\rVert\le\epsilon$.

**(a)** Tìm một mẫu $S$ và một cực tiểu địa phương $w$ của $L_S$ không phải cực tiểu toàn cục. Ghi rõ bán kính $\epsilon$ và một điểm có $L_S$ nhỏ hơn $L_S(w)$.

**(b)** Chứng minh: nếu $F:\mathbb R^p\to\mathbb R$ lồi thì mọi cực tiểu địa phương của $F$ là cực tiểu toàn cục. Suy ra $L_S$ ở (a) không lồi, và chỉ ra hai điểm cùng một trọng số $\alpha$ vi phạm Định nghĩa 05.1.

**(c)** Tính gradient của $L_S$ ở (a) tại các điểm $L_S$ khả vi. GD với gradient này làm gì?
:::

::: hint Gợi ý 1
Phần (a). $L_S$ chỉ đổi giá trị khi $w$ đi qua một đường thẳng $\langle w,x_i\rangle=0$. Tìm một điểm $w$ mà mọi điểm đủ gần $w$ phân lớp sai đúng những quan sát mà $w$ phân lớp sai. Phần (b). Nếu $F(u)<F(w)$, xét các điểm $w+\alpha(u-w)$ với $\alpha$ nhỏ.
:::

::: hint Gợi ý 2
Phần (a). Hai quan sát là đủ, chẳng hạn $((1,0),1)$ và $((1,1),0)$. Chọn $w$ phân lớp sai quan sát thứ nhất và đúng quan sát thứ hai, cách cả hai đường thẳng $\langle w,x_i\rangle=0$ một khoảng dương.
:::

::: solution Lời giải Bài tập 05.7
**(a) Một cực tiểu địa phương.**

**Bước 1: mẫu.** Lấy $S$ gồm $((1,0),1)$ và $((1,1),0)$. Quan sát thứ nhất bị phân lớp sai khi $\langle w,(1,0)\rangle<0$, quan sát thứ hai khi $\langle w,(1,1)\rangle\ge0$. Do đó
$$
\begin{aligned}
L_S(w)&=\tfrac12\,\mathbb 1[\langle w,(1,0)\rangle<0]\\
&\quad+\tfrac12\,\mathbb 1[\langle w,(1,1)\rangle\ge0].
\end{aligned}
$$

**Bước 2: điểm $w=(-1,-1)$.** $\langle w,(1,0)\rangle=-1$ và $\langle w,(1,1)\rangle=-2$, nên $L_S(w)=\tfrac12$.

**Bước 3: lân cận.** Lấy $\epsilon=\tfrac12$ và $\lVert w'-w\rVert\le\tfrac12$. Theo Cauchy–Schwarz,
$$
\begin{aligned}
\langle w',(1,0)\rangle&\le-1+\tfrac12<0,\\
\langle w',(1,1)\rangle&\le-2+\tfrac{\sqrt2}2<0 .
\end{aligned}
$$
Vậy $w'$ phân lớp sai quan sát thứ nhất, đúng quan sát thứ hai, và $L_S(w')=\tfrac12=L_S(w)$.

**Bước 4: điểm tốt hơn.** $w^*=(1,-2)$ có $\langle w^*,(1,0)\rangle=1\ge0$ và $\langle w^*,(1,1)\rangle=-1<0$, nên $L_S(w^*)=0<\tfrac12$.

**(b) Hàm lồi.**

**Bước 1: phản chứng.** Giả sử $w$ là cực tiểu địa phương với bán kính $\epsilon$ và có $u$ với $F(u)<F(w)$. Với $\alpha\in(0,1]$, đặt $z_\alpha=w+\alpha(u-w)$. Theo Định nghĩa 05.1,
$$
\begin{aligned}
F(z_\alpha)&\le(1-\alpha)F(w)+\alpha F(u)\\
&<F(w).
\end{aligned}
$$

**Bước 2: mâu thuẫn.** Chọn $\alpha\le\epsilon/\lVert u-w\rVert$; khi đó $\lVert z_\alpha-w\rVert\le\epsilon$ và $F(z_\alpha)<F(w)$, trái với tính cực tiểu địa phương. Vậy $L_S$ ở (a), có một cực tiểu địa phương không toàn cục, không lồi.

**Bước 3: vi phạm trực tiếp.** Lấy $w=(-1,-1)$, $u=(1,3)$ và $\alpha=0{,}6$. Ta có $L_S(u)=\tfrac12$, vì $u$ phân lớp đúng quan sát thứ nhất và sai quan sát thứ hai. Điểm $0{,}6\,w+0{,}4\,u=(-0{,}2;0{,}6)$ có $\langle\cdot,(1,0)\rangle=-0{,}2<0$ và $\langle\cdot,(1,1)\rangle=0{,}4\ge0$, nên $L_S=1$, trong khi $0{,}6\cdot\tfrac12+0{,}4\cdot\tfrac12=0{,}5<1$.

**(c) Gradient.**

**Bước 1: tính.** $L_S$ là hằng trên mỗi miền mở giới hạn bởi hai đường thẳng $\langle w,(1,0)\rangle=0$ và $\langle w,(1,1)\rangle=0$, nên khả vi với gradient $0$ tại mọi điểm ngoài hai đường thẳng đó; trên chúng, $L_S$ không liên tục.

**Bước 2: hệ quả.** GD với gradient $0$ đứng yên tại điểm khởi tạo, nên $L_S$ không đổi. Mọi điểm trong miền chứa $(-1,-1)$ là *điểm dừng* (stationary point) với $L_S=\tfrac12$. Gradient của hàm lỗi 0–1 không chỉ hướng giảm. Hàm lỗi bản lề và hàm lỗi logistic (§3, §4) lồi và có gradient khác $0$ ở đây.

**Kiểm tra lại.** Với hàm lỗi bản lề trên cùng mẫu, tại $(-1,-1)$ quan sát thứ nhất có hàm lỗi $1-(-1)=2$ và gradient $(-1,0)$, quan sát thứ hai có hàm lỗi $\max\{0,1-2\}=0$ và gradient $0$. Gradient của $L_S$ là $(-0{,}5;0)\ne0$, nên một bước GD làm $\langle w,(1,0)\rangle$ tăng.
:::

### Bài tập 05.8 (Hồi quy logistic: lồi, Lipschitz và trơn; UML Bài tập 12.2)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 1; kiểm tra các hằng số dùng ở Ví dụ 05.9.

::: exercise Bài tập 05.8
Cho $x\in\mathbb R^p$ với $\lVert x\rVert\le C_x$, nhãn $y\in\{0,1\}$, $\tilde y=2y-1$, và hàm lỗi logistic (logistic loss)
$$
\ell(w)=\ln\big(1+e^{-\tilde y\langle w,x\rangle}\big).
$$
Đặt $f(s)=\ln(1+e^{-s})$ trên $\mathbb R$, nên $\ell(w)=f(\tilde y\langle w,x\rangle)$.

**(a)** Chứng minh $f$ lồi, rồi suy ra $\ell$ lồi trên $\mathbb R^p$.

**(b)** Chứng minh $\ell$ là $\lVert x\rVert$-Lipschitz trên $\mathbb R^p$, nên là $C_x$-Lipschitz.

**(c)** Chứng minh $\ell$ là $C_x^2/4$-trơn (smooth) theo Định nghĩa 05.6.

**(d)** Trên $W=\{w:\lVert w\rVert\le B\}$, tìm khoảng giá trị của $\ell$, và tính nó với $B=5$, $C_x=1$ (ứng dụng ở §3). Suy ra các tính chất của $L_S$ với hàm lỗi logistic và hằng số $G$ của Ví dụ 05.9.
:::

::: hint Gợi ý 1
$f'(s)=-1/(1+e^s)$ và $f''(s)=e^s/(1+e^s)^2$. Phần (a). Đạo hàm tăng kéo theo bất đẳng thức dưới gradient tại mọi điểm (định lý giá trị trung bình).
:::

::: hint Gợi ý 2
Phần (c). Viết $f''(s)=q(1-q)$ với $q=1/(1+e^{-s})$. Phần (b), (c). $\lvert\tilde y\langle w-u,x\rangle\rvert\le\lVert x\rVert\,\lVert w-u\rVert$.
:::

::: solution Lời giải Bài tập 05.8
**(a) Tính lồi.**

**Bước 1: đạo hàm.** $f'(s)=-e^{-s}/(1+e^{-s})=-1/(1+e^s)\in(-1,0)$ và $f''(s)=e^s/(1+e^s)^2>0$, nên $f'$ tăng.

**Bước 2: bất đẳng thức dưới gradient.** Cho $s,s'\in\mathbb R$. Theo định lý giá trị trung bình, $f(s')-f(s)=f'(c)(s'-s)$ với $c$ nằm giữa $s$ và $s'$. Nếu $s'>s$ thì $f'(c)\ge f'(s)$; nếu $s'<s$ thì $f'(c)\le f'(s)$ và $s'-s<0$. Cả hai trường hợp cho $f(s')\ge f(s)+f'(s)(s'-s)$.

**Bước 3: từ dưới gradient sang tính lồi.** Với $z=\alpha s+(1-\alpha)s'$, Bước 2 tại điểm $z$ cho hai bất đẳng thức
$$
\begin{aligned}
f(s)&\ge f(z)+f'(z)(s-z),\\
f(s')&\ge f(z)+f'(z)(s'-z).
\end{aligned}
$$
Nhân bất đẳng thức đầu với $\alpha$, bất đẳng thức sau với $1-\alpha$, rồi cộng. Vì $\alpha(s-z)+(1-\alpha)(s'-z)=0$, ta được $\alpha f(s)+(1-\alpha)f(s')\ge f(z)$.

**Bước 4: hàm của $w$.** $w\mapsto\tilde y\langle w,x\rangle$ là tuyến tính, nên như Bước 1 của Ví dụ 05.3, $\ell(\alpha w+(1-\alpha)u)=f\big(\alpha s_w+(1-\alpha)s_u\big)\le\alpha\ell(w)+(1-\alpha)\ell(u)$, với $s_w=\tilde y\langle w,x\rangle$.

**(b) Tính Lipschitz.**

**Bước 1: gradient.** Theo quy tắc đạo hàm hàm hợp, $\nabla\ell(w)=f'(s_w)\,\tilde yx$, nên $\lVert\nabla\ell(w)\rVert=\lvert f'(s_w)\rvert\,\lVert x\rVert\le\lVert x\rVert$.

**Bước 2: Mệnh đề 05.5.** Theo Mệnh đề 05.3(a), $\nabla\ell(w)\in\partial\ell(w)$ tại mọi $w$. Mệnh đề 05.5(a) với $U=\mathbb R^p$ và $G=\lVert x\rVert$ cho $\ell$ là $\lVert x\rVert$-Lipschitz, nên $C_x$-Lipschitz.

**Bước 3: hằng số không giảm được.** Nếu $\ell$ là $G'$-Lipschitz trên $\mathbb R^p$ (mở), Mệnh đề 05.5(b) cho $\lvert f'(s_w)\rvert\,\lVert x\rVert\le G'$ với mọi $w$. Lấy $w=-t\tilde yx$; khi $t\to\infty$, $s_w=-t\lVert x\rVert^2\to-\infty$ và $\lvert f'(s_w)\rvert\to1$. Vậy $G'\ge\lVert x\rVert$.

**(c) Tính trơn.**

**Bước 1: cận cho $f''$.** Với $q=1/(1+e^{-s})\in(0,1)$, ta có $f''(s)=q(1-q)\le\tfrac14$ theo bất đẳng thức AM–GM.

**Bước 2: $f'$ là $\tfrac14$-Lipschitz.** Theo định lý giá trị trung bình, $\lvert f'(s)-f'(s')\rvert=f''(c)\lvert s-s'\rvert\le\tfrac14\lvert s-s'\rvert$.

**Bước 3: gradient của $\ell$.** Với $w,u\in\mathbb R^p$,
$$
\begin{aligned}
&\lVert\nabla\ell(w)-\nabla\ell(u)\rVert\\
&\quad=\lvert f'(s_w)-f'(s_u)\rvert\,\lVert x\rVert\\
&\quad\le\tfrac14\lvert\langle w-u,x\rangle\rvert\,\lVert x\rVert\\
&\quad\le\tfrac14\lVert x\rVert^2\lVert w-u\rVert .
\end{aligned}
$$
Bất đẳng thức cuối là Cauchy–Schwarz. Vậy $\ell$ là $C_x^2/4$-trơn.

**(d) Giá trị trên $W$.**

**Bước 1: khoảng giá trị.** Với $w\in W$, $\lvert s_w\rvert\le BC_x$ theo Cauchy–Schwarz, và $f$ giảm, nên $\ell(w)\in\big[\ln(1+e^{-BC_x}),\ln(1+e^{BC_x})\big]$.

**Bước 2: bằng số.** Với $B=5$, $C_x=1$: $\ln(1+e^{-5})\approx0{,}0067$ và $\ln(1+e^5)\approx5{,}0068$ (làm tròn lên).

**Bước 3: rủi ro thực nghiệm.** $L_S$ là trung bình của các hàm như trên với $\lVert x_i\rVert\le C_x$, nên lồi, $C_x$-Lipschitz và $C_x^2/4$-trơn (bất đẳng thức tam giác cho trung bình). Với $C_x=1$, Bước 1 của (b) cho chuẩn của gradient trên một quan sát không quá $1$, tức $G=1$ như Ví dụ 05.9.

**Kiểm tra lại.** $f''(0)=\tfrac14$, nên hằng số $\tfrac14$ của Bước 1 trong (c) đạt được; $f(0)=\ln2\approx0{,}6931$ là $L_S(0)$ trong ứng dụng ở §3.
:::

### Bài tập 05.9 (Hàm lỗi bản lề là Lipschitz; UML Bài tập 12.3)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 1; hằng số Lipschitz và giới hạn của tính trơn.

::: exercise Bài tập 05.9
Cho $x\in\mathbb R^p$ với $0<\lVert x\rVert\le C_x$, nhãn $y\in\{0,1\}$, $\tilde y=2y-1$, và hàm lỗi bản lề $\ell(w)=\max\{0,1-\tilde y\langle w,x\rangle\}$.

**(a)** Chứng minh $\ell$ là $\lVert x\rVert$-Lipschitz trên $\mathbb R^p$, nên $C_x$-Lipschitz, theo hai cách: qua Mệnh đề 05.5(a) với dưới gradient của Bài tập 05.1, và trực tiếp từ bất đẳng thức $\lvert\max\{0,s\}-\max\{0,s'\}\rvert\le\lvert s-s'\rvert$.

**(b)** Chứng minh hằng số $\lVert x\rVert$ không giảm được. Kiểm tra bằng số với quan sát của Ví dụ 05.2, tại $w_0=(0{,}5;0{,}25)$ và $u=w_0-0{,}1x$.

**(c)** Chứng minh $\ell$ không $\beta$-trơn với $\beta>0$ nào.
:::

::: hint Gợi ý 1
Phần (b). Đi từ một điểm gãy theo hướng $-\tilde yx$. Phần (c). Tính đạo hàm theo hướng $-\tilde yx$ và theo hướng ngược lại tại một điểm gãy.
:::

::: solution Lời giải Bài tập 05.9
**(a) Hai cách.**

**Cách 1, Bước 1: dưới gradient bị chặn.** Tại $w$ với $\tilde y\langle w,x\rangle<1$, $-\tilde yx$ là dưới gradient; với $\tilde y\langle w,x\rangle>1$, $0$ là dưới gradient; tại điểm gãy, $-\alpha\tilde yx$ với $\alpha\in[0,1]$ (Bài tập 05.1(b)). Mọi véc-tơ này có chuẩn không quá $\lVert x\rVert$.

**Cách 1, Bước 2.** Mệnh đề 05.5(a) với $U=\mathbb R^p$ và $G=\lVert x\rVert$ cho tính $\lVert x\rVert$-Lipschitz.

**Cách 2, Bước 1: hàm $\max\{0,\cdot\}$.** Nếu $s,s'\ge0$, hiệu bằng $\lvert s-s'\rvert$. Nếu $s,s'\le0$, hiệu bằng $0$. Nếu $s\ge0\ge s'$, hiệu là $s\le s-s'$; trường hợp ngược lại tương tự.

**Cách 2, Bước 2.** Với $s=1-\tilde y\langle w,x\rangle$, $s'=1-\tilde y\langle u,x\rangle$,
$$
\begin{aligned}
\lvert\ell(w)-\ell(u)\rvert&\le\lvert\langle w-u,x\rangle\rvert\\
&\le\lVert x\rVert\,\lVert w-u\rVert .
\end{aligned}
$$

**(b) Hằng số không giảm được.**

**Bước 1: tổng quát.** Cho $w_0$ là một điểm gãy và $u=w_0-t\tilde yx$ với $t>0$. Theo Bước 3 trong lời giải Bài tập 05.1(b), $\ell(u)=t\lVert x\rVert^2$, trong khi $\ell(w_0)=0$ và $\lVert u-w_0\rVert=t\lVert x\rVert$. Tỉ số là $\lVert x\rVert$.

**Bước 2: bằng số.** Với $x=(1,2)$, $\tilde y=1$, $t=0{,}1$: $u=(0{,}4;0{,}05)$, $\ell(u)=0{,}1\cdot5=0{,}5$ (khớp Ví dụ 05.2), $\lVert u-w_0\rVert=0{,}1\sqrt5\approx0{,}2236$. Tỉ số $0{,}5/0{,}2236\approx2{,}236=\sqrt5=\lVert x\rVert$.

**(c) Không trơn.**

**Bước 1: đạo hàm theo hai hướng.** Tại điểm gãy $w_0$, đặt $d=-\tilde yx$. Theo (b), với $t>0$, $\big(\ell(w_0+td)-\ell(w_0)\big)/t=\lVert x\rVert^2$. Với $u=w_0-td$, ta có $\tilde y\langle u,x\rangle=1+t\lVert x\rVert^2>1$, nên $\ell(u)=0$ và tỉ số tương ứng bằng $0$.

**Bước 2: kết luận.** Nếu $\ell$ khả vi tại $w_0$, đạo hàm theo hướng $-d$ phải bằng $-\lVert x\rVert^2\ne0$, nhưng Bước 1 cho nó bằng $0$. Vậy $\ell$ không khả vi tại $w_0$, nên không thỏa Định nghĩa 05.6 với $\beta$ nào.

**Kiểm tra lại.** Với mẫu nhiều quan sát và $\lVert x_i\rVert\le C_x$, $L_S$ là $C_x$-Lipschitz như trung bình các hàm $C_x$-Lipschitz, nên oracle rút một quan sát thỏa (G2) với $G=C_x$.
:::

### Bài tập 05.10 (Perceptron như hạ gradient trên một hàm lồi; UML Bài tập 14.3, ý 1–3)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 1, 3; áp dụng Hệ quả 05.16 cho một hàm lồi không khả vi và chọn số vòng lặp. Bài bỏ phần so sánh với Batch Perceptron (UML §9.1.2) của ý 3.

::: exercise Bài tập 05.10
Cho mẫu $S=((x_1,y_1),\ldots,(x_m,y_m))$ với $x_i\in\mathbb R^p$, $y_i\in\{0,1\}$, $\tilde y_i=2y_i-1$ và $C_x=\max_i\lVert x_i\rVert>0$. Giả sử tập
$$
K=\{w:\tilde y_i\langle w,x_i\rangle\ge1\ \forall i\}
$$
khác rỗng. Đặt
$$
f(w)=\max_{1\le i\le m}\big(1-\tilde y_i\langle w,x_i\rangle\big).
$$

**(a)** Chứng minh $K$ có đúng một phần tử có chuẩn nhỏ nhất, kí hiệu $w^\circ$.

**(b)** Tính giá trị nhỏ nhất của $f$ trên quả cầu $\{w:\lVert w\rVert\le\lVert w^\circ\rVert\}$. Chứng minh: nếu $f(w)<1$ thì $h_{w,0}$ phân lớp đúng mọi quan sát của $S$.

**(c)** Với $w$ cho trước, nêu một dưới gradient của $f$ tại $w$, số phép tính để tìm nó và một cận cho chuẩn của nó.

**(d)** Chạy Thuật toán 05.9 trên $f$ với $W=\mathbb R^p$, $w_1=0$, $\eta=\lVert w^\circ\rVert/(C_x\sqrt T)$ và dưới gradient của (c), chọn chỉ số nhỏ nhất khi có nhiều chỉ số đạt cực đại. Chứng minh $\bar w_T$ phân lớp đúng $S$ khi $T>\lVert w^\circ\rVert^2C_x^2$, và tính cận của $f(\bar w_T)$ khi $\lVert w^\circ\rVert=10$, $C_x=1$, $T=101$. Chứng minh hướng của $\bar w_T$ không phụ thuộc $\eta>0$, rồi giải thích vì sao có thể chạy thuật toán mà không biết $\lVert w^\circ\rVert$.
:::

::: hint Gợi ý 1
Phần (a). $K$ lồi và đóng; dùng Định nghĩa 05.7 và Phụ lục A. Phần (b). Giả sử $\lVert w\rVert\le\lVert w^\circ\rVert$ và $f(w)<0$, rồi co $w$ về một điểm của $K$.
:::

::: hint Gợi ý 2
Phần (b). Chia $w$ cho $\min_i\tilde y_i\langle w,x_i\rangle$. Phần (d). Hệ quả 05.16 với $u=w^\circ$, $R=\lVert w^\circ\rVert$, $G=C_x$. Chỉ số đạt cực đại của $1-\tilde y_i\langle w,x_i\rangle$ là chỉ số đạt cực tiểu của $\tilde y_i\langle w,x_i\rangle$, không đổi khi nhân $w$ với một số dương.
:::

::: solution Lời giải Bài tập 05.10
**(a) Phần tử có chuẩn nhỏ nhất.**

**Bước 1: $K$ lồi đóng.** Mỗi tập $\{w:\tilde y_i\langle w,x_i\rangle\ge1\}$ là một nửa không gian đóng, nên lồi và đóng; giao của chúng cũng vậy, và khác rỗng theo giả thiết.

**Bước 2: phép chiếu.** Phần tử có chuẩn nhỏ nhất của $K$ là điểm của $K$ gần $0$ nhất, tức $\operatorname{proj}_K(0)$ (Định nghĩa 05.7). Theo Phụ lục A, nó tồn tại và duy nhất. Vì $0\notin K$, $w^\circ\ne0$.

**(b) Giá trị nhỏ nhất trên quả cầu.**

**Bước 1: $f(w^\circ)\le0$.** Vì $w^\circ\in K$, mọi số hạng $1-\tilde y_i\langle w^\circ,x_i\rangle\le0$.

**Bước 2: $f\ge0$ trên quả cầu.** Giả sử $\lVert w\rVert\le\lVert w^\circ\rVert$ và $f(w)<0$. Khi đó $c=\min_i\tilde y_i\langle w,x_i\rangle=1-f(w)>1$, nên $w/c\in K$ và $\lVert w/c\rVert<\lVert w\rVert\le\lVert w^\circ\rVert$, trái với tính nhỏ nhất của $\lVert w^\circ\rVert$. Vậy $f\ge0$ trên quả cầu, và cùng Bước 1, giá trị nhỏ nhất là $f(w^\circ)=0$.

**Bước 3: phân lớp đúng.** Nếu $f(w)<1$ thì $\tilde y_i\langle w,x_i\rangle>0$ với mọi $i$. Với $y_i=1$, $\langle w,x_i\rangle>0$ nên $h_{w,0}(x_i)=1$; với $y_i=0$, $\langle w,x_i\rangle<0$ nên $h_{w,0}(x_i)=0$.

**(c) Dưới gradient.** Chọn $j$ đạt cực đại của $1-\tilde y_i\langle w,x_i\rangle$; việc này cần $m$ tích vô hướng. Nhánh $j$ là hàm afin với gradient $-\tilde y_jx_j$, nên theo Mệnh đề 05.3(a) và (c), $-\tilde y_jx_j\in\partial f(w)$, với chuẩn $\lVert x_j\rVert\le C_x$.

**(d) Hạ gradient.**

**Bước 1: thuật toán.** Từ $w_1=0$, mỗi vòng tìm $j$ có $\tilde y_j\langle w_t,x_j\rangle$ nhỏ nhất và đặt $w_{t+1}=w_t+\eta\tilde y_jx_j$. Đầu ra là $\bar w_T$. Với $\eta=1$, đây là phép cập nhật của Perceptron (UML §9.1.2), áp dụng cho quan sát có $\tilde y_j\langle w_t,x_j\rangle$ nhỏ nhất; đó là lý do của tên bài.

**Bước 2: giả thiết của Hệ quả 05.16.** $f$ là cực đại của các hàm afin, nên lồi; $W=\mathbb R^p$ khác rỗng, đóng, lồi; dưới gradient có chuẩn không quá $G=C_x$ tại mọi $w$. Điểm so sánh $u=w^\circ$ có $\lVert w_1-u\rVert=\lVert w^\circ\rVert=R$.

**Bước 3: cận.** Hệ quả 05.16 và $f(w^\circ)=0$ cho
$$
f(\bar w_T)\le\frac{\lVert w^\circ\rVert C_x}{\sqrt T},
$$
nhỏ hơn $1$ khi và chỉ khi $T>\lVert w^\circ\rVert^2C_x^2$. Theo (b), khi đó $\bar w_T$ phân lớp đúng $S$.

**Bước 4: bằng số.** Với $\lVert w^\circ\rVert=10$, $C_x=1$: cần $T>100$. Với $T=101$, cận là $10/\sqrt{101}\approx0{,}9951<1$. Với $T=100$, cận bằng $1$ và không đủ.

**Bước 5: hướng của $\bar w_T$.** Gọi $(w'_t)$ là dãy điểm lặp với $\eta=1$. Quy nạp: $w_1=0=\eta w'_1$; nếu $w_t=\eta w'_t$ thì $\tilde y_i\langle w_t,x_i\rangle=\eta\,\tilde y_i\langle w'_t,x_i\rangle$, nên cùng chỉ số $j$ được chọn, và $w_{t+1}=\eta(w'_t+\tilde y_jx_j)=\eta w'_{t+1}$. Vậy $\bar w_T=\eta\bar w'_T$, và $\tilde y_i\langle\bar w_T,x_i\rangle$ cùng dấu với $\tilde y_i\langle\bar w'_T,x_i\rangle$.

**Bước 6: không cần biết $\lVert w^\circ\rVert$.** Theo Bước 5, chạy với $\eta=1$ cho cùng các quan sát được phân lớp đúng, nên độ dài bước không cần $\lVert w^\circ\rVert$. Số vòng lặp đủ theo cận vẫn phụ thuộc $\lVert w^\circ\rVert$. Vì $S$ có sẵn, có thể dừng ở $T$ đầu tiên mà $\bar w_T$ phân lớp đúng $S$; theo Bước 3, điều này xảy ra muộn nhất ở $T=\lfloor\lVert w^\circ\rVert^2C_x^2\rfloor+1$. Lập luận cần $W=\mathbb R^p$: phép chiếu lên một quả cầu phá tính tỉ lệ.

**Kiểm tra lại.** Với $m=1$, $x_1=(0{,}1;0)$, $y_1=1$: $w^\circ=(10,0)$, $C_x=0{,}1$, nên $T=2$ đủ. Khi đó $\eta=10/(0{,}1\sqrt2)\approx70{,}71$, $w_2=\eta x_1$, $\bar w_2=\eta x_1/2\approx(3{,}5355;0)$ và $f(\bar w_2)\approx1-0{,}3536=0{,}6464$, không quá cận $1/\sqrt2\approx0{,}7072$.
:::

### Bài tập 05.11 (Độ dài bước giảm dần với phép chiếu; UML Bài tập 14.4, thêm phép chiếu)

**Mức độ:** chứng minh, kiểm tra giả thiết, tính toán. **Mục tiêu:** mục tiêu học tập 1, 3; tổng triệt tiêu với trọng số thay đổi, vai của tập bị chặn, và số vòng lặp cần cho một độ chênh cho trước.

::: exercise Bài tập 05.11
UML Bài tập 14.4 yêu cầu một cận tương tự định lý về SGD của UML §14.3 cho độ dài bước $\eta_t$ giảm theo $1/\sqrt t$, trong thiết lập không có phép chiếu. Ở đây thêm phép chiếu. Giả thiết của Định lý 05.14 giữ nguyên, với $W=\{w:\lVert w\rVert\le B\}$, $w_1\in W$, nhưng Thuật toán 05.11 dùng
$$
\eta_t=\frac B{G\sqrt t},\quad t=1,\ldots,T,
$$
và đầu ra vẫn là trung bình đều $\bar w_T=\frac1T\sum_{t=1}^Tw_t$.

**(a)** Chứng minh với mọi $u\in W$,
$$
\mathbb EF(\bar w_T)-F(u)\le\frac{3BG}{\sqrt T}.
$$

**(b)** Chỉ ra bước cần $W$ bị chặn. Vì sao chứng minh Định lý 05.14 với $\eta$ hằng không cần điều này?

**(c)** Với $B=1$, $G=4$, $T=1600$, tính cận của (a) và giá trị của cận trung gian trước khi dùng $\sum_{t\le T}t^{-1/2}\le2\sqrt T-1$. So với cận $0{,}1$ của độ dài bước hằng (Ví dụ 05.8) và khoảng $0{,}228$ của trung bình có trọng số (Nhận xét 05.17).

**(d)** Với $B=1$, $G=4$ và $\epsilon=0{,}1$, tìm $T$ nhỏ nhất để cận của (a) không quá $\epsilon$, và so với $1600$ vòng của Ví dụ 05.8. Mỗi cách cần biết $T$ trước khi chạy hay không?
:::

::: hint Gợi ý 1
Áp dụng Mệnh đề 05.13 với $\eta_t$ ở bước $t$, rồi cộng. Tổng $\sum_t(\Delta_t-\Delta_{t+1})/(2\eta_t)$ không còn triệt tiêu; nhóm lại theo $\Delta_t$, tức lấy tổng Abel (Abel summation).
:::

::: hint Gợi ý 2
Hệ số của $\Delta_t$ với $2\le t\le T$ là $\tfrac1{2\eta_t}-\tfrac1{2\eta_{t-1}}\ge0$, và $\Delta_t\le(2B)^2$. So sánh $t^{-1/2}$ với $\int_{t-1}^ts^{-1/2}\,ds$.
:::

::: solution Lời giải Bài tập 05.11
**(a) Cận.**

**Bước 1: một bước.** Mệnh đề 05.13 với độ dài bước $\eta_t$ cho, trên từng quỹ đạo,
$$
\begin{aligned}
\langle g_t,w_t-u\rangle&\le\frac{\Delta_t-\Delta_{t+1}}{2\eta_t}\\
&\quad+\frac{\eta_t}2\lVert g_t\rVert^2 .
\end{aligned}
$$

**Bước 2: tổng Abel.** Nhóm các số hạng theo $\Delta_t$:
$$
\begin{aligned}
&\sum_{t=1}^T\frac{\Delta_t-\Delta_{t+1}}{2\eta_t}\\
&=\frac{\Delta_1}{2\eta_1}-\frac{\Delta_{T+1}}{2\eta_T}\\
&\quad+\sum_{t=2}^T\Delta_t\Big(\frac1{2\eta_t}-\frac1{2\eta_{t-1}}\Big).
\end{aligned}
$$

**Bước 3: dùng $W$ bị chặn.** Mọi $w_t$ thuộc $W$ (Bổ đề 05.12(a)) và $u\in W$, nên $\Delta_t\le(2B)^2=4B^2$. Vì $\eta_t$ giảm, các hệ số trong ngoặc không âm. Bỏ $-\Delta_{T+1}/(2\eta_T)\le0$, rồi cộng các hệ số:
$$
\begin{aligned}
\sum_{t=1}^T\frac{\Delta_t-\Delta_{t+1}}{2\eta_t}&\le\frac{4B^2}{2\eta_T}\\
&=2BG\sqrt T .
\end{aligned}
$$

**Bước 4: kì vọng.** Bổ đề 05.12 vẫn đúng với dãy $\eta_t$ tất định (Phụ lục C của ghi chú). Như Bước 3 và 4 của chứng minh Định lý 05.14, $\mathbb E\langle g_t,w_t-u\rangle\ge\mathbb E[F(w_t)-F(u)]$ và $\mathbb E\lVert g_t\rVert^2\le G^2$. Do đó
$$
\begin{aligned}
&\sum_{t=1}^T\mathbb E\big[F(w_t)-F(u)\big]\\
&\quad\le2BG\sqrt T+\frac{G^2}2\sum_{t=1}^T\eta_t\\
&\quad=2BG\sqrt T+\frac{BG}2\sum_{t=1}^T\frac1{\sqrt t}.
\end{aligned}
$$

**Bước 5: tổng $t^{-1/2}$.** Với $t\ge2$, $t^{-1/2}\le\int_{t-1}^ts^{-1/2}\,ds$, nên $\sum_{t=1}^Tt^{-1/2}\le1+\int_1^Ts^{-1/2}\,ds=2\sqrt T-1$. Vế phải ở Bước 4 không quá $3BG\sqrt T-BG/2\le3BG\sqrt T$.

**Bước 6: trung bình.** Theo bất đẳng thức lồi hữu hạn với trọng số $1/T$, $F(\bar w_T)\le\frac1T\sum_tF(w_t)$. Lấy kì vọng và chia cho $T$, ta được cận.

**(b) Vai của tập bị chặn.**

**Bước 1: chỗ dùng.** Bước 3 cần $\Delta_t\le4B^2$ với mọi $2\le t\le T$, vì các $\Delta_t$ này xuất hiện với hệ số dương. Phép chiếu giữ $w_t\in W$, và $W$ bị chặn cho cận.

**Bước 2: độ dài bước hằng.** Với $\eta_t=\eta$, các hệ số $\tfrac1{2\eta_t}-\tfrac1{2\eta_{t-1}}$ bằng $0$, tổng triệt tiêu chỉ còn $\Delta_1$ và $-\Delta_{T+1}$, nên Định lý 05.14 không cần $W$ bị chặn. Trong thiết lập không chiếu của UML, các $\Delta_t$ không có cận trước, và lập luận ở Bước 3 không áp dụng được.

**(c) Bằng số.**

**Bước 1: cận.** $3BG/\sqrt T=12/40=0{,}3$.

**Bước 2: cận trung gian.** $\sum_{t\le1600}t^{-1/2}\approx78{,}552$, không quá $2\cdot40-1=79$. Với $2BG\sqrt T=2\cdot4\cdot40=320$ và $BG/2=2$, vế phải ở Bước 4 chia cho $T$ là
$$
\begin{aligned}
&\frac{320+2\cdot78{,}552}{1600}\\
&\quad\approx\frac{477{,}11}{1600}\approx0{,}2982 .
\end{aligned}
$$

**Bước 3: so sánh.** Theo các cận, độ dài bước hằng $\eta=R/(G\sqrt T)$ cho $0{,}1$, trung bình có trọng số cho khoảng $0{,}228$, trung bình đều với $\eta_t$ giảm dần cho $0{,}3$.

**(d) Số vòng lặp.**

**Bước 1: điều kiện.** $3BG/\sqrt T\le\epsilon$ tương đương $\sqrt T\ge3BG/\epsilon=12/0{,}1=120$, tức $T\ge14\,400$.

**Bước 2: so sánh.** Con số này gấp $9$ lần $1600$ của Ví dụ 05.8, đúng bằng bình phương của thừa số $3$ trong cận.

**Bước 3: biết $T$ trước.** Độ dài bước hằng $\eta=R/(G\sqrt T)$ phụ thuộc $T$, nên $T$ phải cố định trước khi chạy. Dãy $\eta_t=B/(G\sqrt t)$ không phụ thuộc $T$: có thể chạy tiếp và đọc cận $3BG/\sqrt T$ tại bất kì $T$ nào.

**Kiểm tra lại.** Ở Bước 3 của (a), tổng các hệ số là $\tfrac1{2\eta_1}+\sum_{t=2}^T\big(\tfrac1{2\eta_t}-\tfrac1{2\eta_{t-1}}\big)=\tfrac1{2\eta_T}=\tfrac{G\sqrt T}{2B}$; nhân với $4B^2$ cho $2BG\sqrt T$. Ở (d), $3\cdot4/\sqrt{14\,400}=12/120=0{,}1$.
:::

### Bài tập 05.12 (Tùy chọn: ma trận $\sum_ix_ix_i^\top$ khả nghịch và tính lồi mạnh; UML Bài tập 9.2, thêm tính lồi mạnh)

**Mức độ:** chứng minh, tính toán (tùy chọn). **Mục tiêu:** phần mở rộng của §4; hằng số lồi mạnh và trơn của Định nghĩa 05.6 cho hàm lỗi bình phương.

::: exercise Bài tập 05.12
Cho $x_1,\ldots,x_m\in\mathbb R^p$ và $A=\sum_{i=1}^mx_ix_i^\top$, ma trận của hệ phương trình chuẩn (normal equations) trong bình phương tối thiểu (least squares; UML §9.2). Gọi $\lambda_{\min}(A)$, $\lambda_{\max}(A)$ là trị riêng nhỏ nhất và lớn nhất của $A$.

**(a)** Biểu diễn $v^\top Av$ qua các tích vô hướng $\langle v,x_i\rangle$. Từ đó tìm điều kiện cần và đủ trên $x_1,\ldots,x_m$ để $A$ khả nghịch, và chứng minh.

**(b)** Với $y_i\in\mathbb R$ và hàm lỗi bình phương, $L_S(w)=\frac1m\sum_i(\langle w,x_i\rangle-y_i)^2$. Chứng minh $L_S$ là $\lambda$-lồi mạnh (strongly convex) với $\lambda=2\lambda_{\min}(A)/m$ và $\beta$-trơn với $\beta=2\lambda_{\max}(A)/m$. Khi các $x_i$ không sinh $\mathbb R^p$, chứng minh $L_S$ không $\lambda$-lồi mạnh với $\lambda>0$ nào.

**(c)** Với mẫu của Ví dụ 05.1, tính $A$, các trị riêng của nó, $\lambda$ và $\beta$.
:::

::: hint Gợi ý 1
Phần (b). Với ma trận đối xứng $M$ và $q(w)=w^\top Mw$, hiệu $\alpha q(w)+(1-\alpha)q(u)-q(\alpha w+(1-\alpha)u)$ bằng $\alpha(1-\alpha)(w-u)^\top M(w-u)$. Phần afin của $L_S$ không đóng góp vào hiệu này.
:::

::: solution Lời giải Bài tập 05.12
**(a) Khả nghịch.**

**Bước 1: dạng toàn phương.** $v^\top Av=\sum_iv^\top x_ix_i^\top v=\sum_i\langle v,x_i\rangle^2$.

**Bước 2: chiều "sinh kéo theo khả nghịch".** Giả sử các $x_i$ sinh $\mathbb R^p$ và $Av=0$. Khi đó $v^\top Av=0$, nên $\langle v,x_i\rangle=0$ với mọi $i$. Vì $v$ là tổ hợp tuyến tính của các $x_i$, ta có $\langle v,v\rangle=0$, tức $v=0$. Ma trận vuông $A$ đơn ánh nên khả nghịch.

**Bước 3: chiều ngược lại.** Nếu các $x_i$ sinh một không gian con thực sự $V$, lấy $v\ne0$ trong phần bù trực giao của $V$. Khi đó $Av=\sum_ix_i\langle x_i,v\rangle=0$, nên $A$ không khả nghịch.

**(b) Lồi mạnh và trơn.**

**Bước 1: dạng bậc hai.** Khai triển, $L_S(w)=\frac1m\big(w^\top Aw-2c^\top w+\sum_iy_i^2\big)$ với $c=\sum_iy_ix_i$.

**Bước 2: đẳng thức dây cung.** Với $z=\alpha w+(1-\alpha)u$, khai triển $q(z)=\alpha^2q(w)+2\alpha(1-\alpha)w^\top Mu+(1-\alpha)^2q(u)$. Do đó
$$
\begin{aligned}
&\alpha q(w)+(1-\alpha)q(u)-q(z)\\
&\ =\alpha(1-\alpha)\\
&\qquad\cdot\big[q(w)+q(u)-2w^\top Mu\big]\\
&\ =\alpha(1-\alpha)\\
&\qquad\cdot(w-u)^\top M(w-u).
\end{aligned}
$$
Với hàm afin, hiệu tương ứng bằng $0$.

**Bước 3: lồi mạnh.** Áp dụng Bước 2 với $M=A/m$. Theo định lý phổ, $(w-u)^\top A(w-u)\ge\lambda_{\min}(A)\lVert w-u\rVert^2$, nên
$$
\begin{aligned}
&\alpha L_S(w)+(1-\alpha)L_S(u)\\
&\qquad-L_S(z)\\
&\quad\ge\frac{\lambda_{\min}(A)}m\,\alpha(1-\alpha)\\
&\qquad\cdot\lVert w-u\rVert^2,
\end{aligned}
$$
đúng là Định nghĩa 05.6 với $\tfrac\lambda2=\lambda_{\min}(A)/m$.

**Bước 4: trơn.** $\nabla L_S(w)=\tfrac2m(Aw-c)$, nên $\lVert\nabla L_S(w)-\nabla L_S(u)\rVert=\tfrac2m\lVert A(w-u)\rVert\le\tfrac{2\lambda_{\max}(A)}m\lVert w-u\rVert$, vì $A$ đối xứng nửa xác định dương.

**Bước 5: không sinh.** Lấy $v\ne0$ như Bước 3 của (a) và $u=w+v$. Theo Bước 2, hiệu dây cung là $\tfrac{\alpha(1-\alpha)}mv^\top Av=0$, nhỏ hơn $\tfrac\lambda2\alpha(1-\alpha)\lVert v\rVert^2$ với mọi $\lambda>0$ và $\alpha\in(0,1)$. Dọc hướng $v$, $L_S$ là hằng.

**(c) Ví dụ hồi quy.**

**Bước 1: ma trận.** $x_1x_1^\top=\operatorname{diag}(1,0)$, $x_2x_2^\top=\operatorname{diag}(0,1)$, còn $x_3x_3^\top$ có các phần tử $0{,}36$; $0{,}48$; $0{,}48$; $0{,}64$. Do đó
$$
A=\begin{pmatrix}1{,}36&0{,}48\\0{,}48&1{,}64\end{pmatrix}.
$$

**Bước 2: trị riêng.** $\operatorname{tr}A=3$ và $\det A=1{,}36\cdot1{,}64-0{,}48^2=2{,}2304-0{,}2304=2$. Phương trình đặc trưng $\mu^2-3\mu+2=0$ cho $\mu=1$ và $\mu=2$.

**Bước 3: hằng số.** Với $m=3$: $\lambda=2\cdot1/3=\tfrac23$ và $\beta=2\cdot2/3=\tfrac43$, đúng như câu sau Định nghĩa 05.6.

**Kiểm tra lại.** $A/3$ là ma trận $M$ ở Phụ lục D của ghi chú: $1{,}36/3\approx0{,}4533$, $0{,}48/3=0{,}16$, $1{,}64/3\approx0{,}5467$.
:::
