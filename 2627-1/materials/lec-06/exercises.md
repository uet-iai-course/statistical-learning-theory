# Bài tập Bài 06 — Học bằng hạ gradient ngẫu nhiên, chính quy hóa và tính ổn định

Định nghĩa, kết quả và ví dụ được dẫn theo số hiệu của ghi chú Bài 06 và của các ghi chú Bài 01–05. Kí hiệu theo bảng kí hiệu chung và §2 của ghi chú, gồm:

- **§4–§5.** $v(w,z)$: quy tắc dưới gradient đo được; $\bar w_T$: điểm lặp trung bình của Thuật toán 05.11; $\operatorname{opt}_S$: sai số tối ưu thực nghiệm.
- **§6–§8.** $F_{S,\lambda}=L_S+\tfrac\lambda2\lVert\cdot\rVert^2$: mục tiêu có chính quy hóa, với nghiệm $\hat w_S$ trên $W$; $S^{(i)}$: mẫu lân cận, thay quan sát thứ $i$ bằng quan sát thay thế $Z'$; $\epsilon_{\mathrm{stab}}(m)$: hệ số ổn định; (L): với mọi $z\in\mathcal Z$, $\ell(\cdot,z)$ là $G$-Lipschitz trên $W$.
- **§9.** $W_B=\{u\in W:\lVert u\rVert\le B\}$ và $\lambda^*=2G/(B\sqrt m)$.

Kí hiệu chỉ dùng trong một bài (như $r_\lambda$, $G_\lambda$ ở Bài tập 06.5) được đặt tên tại chỗ. Viết tắt: hạ gradient ngẫu nhiên (stochastic gradient descent, SGD), tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM).

Sáu bài đầu là bài gốc của học phần; ý thực nghiệm của Bài tập 06.6 là tùy chọn. Năm bài sau chọn từ mục bài tập §13.7 và §14.8 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* (Shalev-Shwartz và Ben-David, 2014; viết tắt UML); Bài tập 06.11 là bài tùy chọn. UML viết $\rho$ cho hằng số Lipschitz, $d$ cho số chiều đặc trưng và dùng số hạng chính quy hóa $\lambda\lVert w\rVert^2$; ở đây viết $G$, $p$ và $\tfrac\lambda2\lVert w\rVert^2$.

## Bài tập gốc

### Bài tập 06.1 (Hàm mà gradient ngẫu nhiên không chệch trong hai chế độ lấy mẫu)

**Mức độ:** khái niệm, tính toán. **Mục tiêu:** mục tiêu học tập 1; phân biệt gradient ngẫu nhiên không chệch cho $L_S$ khi biết mẫu với gradient ngẫu nhiên không chệch cho $L_D$.

::: exercise Bài tập 06.1
Hàm lỗi $\ell$, quy tắc dưới gradient $v$, tập $W$, điểm khởi tạo $w_1$ và độ dài bước $\eta$ thỏa các giả thiết của Hệ quả 06.2. SGD có chiếu (Thuật toán 05.11) chạy trong hai chế độ của §1.

**(a)** Chế độ A: các quan sát mới $Z_1,Z_2,\ldots$ độc lập cùng phân bố $D$ và $g_t=v(w_t,Z_t)$. Với $\mathcal F_{t-1}=\sigma(Z_1,\ldots,Z_{t-1})$ và $\psi(w)=\mathbb E_{Z\sim D}\,v(w,Z)$, chứng minh
$$
\begin{aligned}
&\mathbb E[g_t\mid\mathcal F_{t-1}]\\
&\quad=\psi(w_t)\in\partial L_D(w_t).
\end{aligned}
$$
Chỉ ra chỗ dùng tính độc lập của $Z_t$ với $Z_1,\ldots,Z_{t-1}$.

**(b)** Chế độ B: mẫu $S=(Z_1,\ldots,Z_m)\sim D^m$ được lưu lại; các chỉ số $i_1,i_2,\ldots$ độc lập, đều trên $\{1,\ldots,m\}$ và độc lập với $S$; $g_t=v(w_t,Z_{i_t})$. Chứng minh rằng khi biết $S$ và $i_1,\ldots,i_{t-1}$, kì vọng có điều kiện của $g_t$ là một dưới gradient của $L_S$ tại $w_t$.

**(c)** Lấy phân bố $D$ của câu hỏi mở đầu ($X=1$, $Y$ nhận $1$ và $-1$ với xác suất $\tfrac12$), hàm lỗi bình phương, $W=[-1,1]$, $w_1=0$, $\eta\in(0,\tfrac12)$ và chế độ B với $m\ge2$; $Y_j$ là nhãn của $Z_j$. Tính $w_2$, $\mathbb E[g_2\mid S,i_1]$ và $\mathbb E[g_2\mid w_2]$, rồi so với $L_D'(w_2)$. Tính độ chệch $\mathbb E[g_2\mid w_2]-L_D'(w_2)$ với $m=3$.

**(d)** Với cùng phân bố, SGD đi một vòng qua mẫu theo thứ tự như Nhận xét 06.3, tức $g_t=2(w_t-Y_t)$. Tính $\mathbb E[g_2\mid w_2]$ và chỉ ra giả thiết làm độ chệch bằng $0$.
:::

::: hint Gợi ý 1
Phần (a). Điểm lặp $w_t$ là hàm của $Z_1,\ldots,Z_{t-1}$ (Bổ đề 05.12(a) với $\xi_t=Z_t$); cố định $w_t$ rồi lấy kì vọng theo $Z_t$, sau đó dùng Bổ đề 06.1(b). Phần (b). Khi biết $S$, chế độ B là oracle rút một quan sát của Bài 05 cho $F=L_S$; dùng Mệnh đề 05.3(b).
:::

::: hint Gợi ý 2
Phần (c). $g_1=-2Y_{i_1}$. Khi biết $Y_{i_1}=y$, chỉ số $i_2$ trùng $i_1$ với xác suất $\tfrac1m$; khi $i_2\ne i_1$, nhãn $Y_{i_2}$ độc lập với $Y_{i_1}$ và có kì vọng $0$.
:::

::: solution Lời giải Bài tập 06.1
**(a) Chế độ A.**

**Bước 1: điểm lặp.** Theo Bổ đề 05.12(a) với $\xi_t=Z_t$, $w_t$ là một hàm đo được của $Z_1,\ldots,Z_{t-1}$, tức đo được theo $\mathcal F_{t-1}$.

**Bước 2: kì vọng có điều kiện; tính độc lập.** Các $Z_j$ độc lập, nên $Z_t$ độc lập với $\mathcal F_{t-1}$; tính độc lập được dùng ở đây. Cố định $w_t=w$ và lấy kì vọng theo $Z_t\sim D$ (như Bổ đề 05.12(b)):
$$
\begin{aligned}
&\mathbb E[g_t\mid\mathcal F_{t-1}]\\
&=\mathbb E_{Z\sim D}\,v(w,Z)\big|_{w=w_t}\\
&=\psi(w_t).
\end{aligned}
$$

**Bước 3: dưới gradient của $L_D$.** Theo giả thiết cận gradient của Hệ quả 06.2 và bất đẳng thức Cauchy–Schwarz, $\mathbb E\lVert v(w,Z)\rVert\le G<\infty$ với mọi $w\in W$. Bổ đề 06.1(b) cho $\psi(w_t)\in\partial L_D(w_t)$.

**(b) Chế độ B.**

**Bước 1: cố định mẫu.** Khi biết $S=s=(z_1,\ldots,z_m)$, nguồn ngẫu nhiên duy nhất là các chỉ số, và $w_t$ là hàm của $i_1,\ldots,i_{t-1}$. Chỉ số $i_t$ độc lập với chúng và đều trên $\{1,\ldots,m\}$, nên
$$
\begin{aligned}
&\mathbb E[g_t\mid S,i_1,\ldots,i_{t-1}]\\
&\quad=\frac1m\sum_{j=1}^mv(w_t,z_j).
\end{aligned}
$$

**Bước 2: dưới gradient của $L_S$.** Mỗi $v(w_t,z_j)$ là một dưới gradient của $\ell(\cdot,z_j)$ tại $w_t$. Theo Mệnh đề 05.3(b), trung bình của chúng thuộc $\partial L_s(w_t)$. Điểm $w_t$ phụ thuộc $s$, nên vế phải nói chung không thuộc $\partial L_D(w_t)$.

**(c) Phân bố của câu hỏi mở đầu.**

**Bước 1: bước thứ nhất.** $g_1=2(w_1-Y_{i_1})=-2Y_{i_1}$, nên $w_1-\eta g_1=2\eta Y_{i_1}$. Vì $2\eta<1$, điểm này thuộc $W$ và phép chiếu không tác động:
$$
w_2=2\eta Y_{i_1}.
$$

**Bước 2: biết mẫu.** Với $\bar Y=\tfrac1m\sum_jY_j$, Bước 1 của (b) cho
$$
\begin{aligned}
\mathbb E[g_2\mid S,i_1]&=2(w_2-\bar Y)\\
&=L_S'(w_2).
\end{aligned}
$$

**Bước 3: chỉ biết điểm lặp.** Vì $\eta>0$, biết $w_2$ tương đương biết $y=Y_{i_1}$. Với xác suất $\tfrac1m$, $i_2=i_1$ và $Y_{i_2}=y$. Với xác suất $1-\tfrac1m$, $i_2\ne i_1$; khi đó $Y_{i_2}$ độc lập với $Y_{i_1}$ và có kì vọng $0$. Do đó
$$
\begin{aligned}
\mathbb E[Y_{i_2}\mid w_2]&=\tfrac ym,\\
\mathbb E[g_2\mid w_2]&=2w_2-\tfrac{2y}m .
\end{aligned}
$$

**Bước 4: độ chệch.** Vì $L_D(w)=w^2+1$, ta có $L_D'(w_2)=2w_2$, và độ chệch bằng $-2y/m$. Với $m=3$, độ chệch là $-\tfrac23\approx-0{,}667$ khi $y=1$ và $0{,}667$ khi $y=-1$: bước tiếp theo bị kéo về phía nhãn đã dùng ở bước một. Độ chệch giảm theo $m$ nhưng khác $0$ với mọi $m$.

**(d) Một vòng theo thứ tự.**

**Bước 1: hai bước đầu.** Như (c), $w_2=2\eta Y_1$ và $g_2=2(w_2-Y_2)$.

**Bước 2: tính độc lập.** $Y_2$ độc lập với $Y_1$, tức với $w_2$, và có kì vọng $0$, nên
$$
\mathbb E[g_2\mid w_2]=2w_2=L_D'(w_2).
$$
Độ chệch bằng $0$. Giả thiết được dùng là quan sát của bước $t$ độc lập với các quan sát đã dùng, như Bước 2 của (a). Ở (c), giả thiết này hỏng vì $i_2$ có thể trùng $i_1$.

**Kiểm tra lại.** Với $m=3$, liệt kê $72$ trường hợp đồng khả năng của $(Y_1,Y_2,Y_3,i_1,i_2)$ cho $\mathbb E[g_2-2w_2\mid Y_{i_1}=1]=-\tfrac23$.
:::

### Bài tập 06.2 (Lập luận đổi vai cho khoảng cách tổng quát hóa kì vọng)

**Mức độ:** chứng minh, tính toán, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 3; vai của dạng đầy đủ của (T1) trong lập luận đổi vai.

::: exercise Bài tập 06.2
Cho $\mathcal Z$ hữu hạn, phân bố $D$ trên $\mathcal Z$ với xác suất $D(z)$ của từng điểm, hàm lỗi $\ell\ge0$ và một thuật toán tất định $A$.

**(a)** Giả sử $A$ ổn định đều với hệ số $\epsilon_{\mathrm{stab}}(m)$ (Định nghĩa 06.9). Viết lại chứng minh Định lý 06.10 với mọi kì vọng là tổng hữu hạn theo các $D(z)$, không dùng định lý Fubini. Chỉ ra dòng dùng tính độc lập của $Z'$ với $S$ và dòng dùng dạng đầy đủ của (T1).

**(b)** Lấy $\mathcal Z=\{0,1\}$, $D(0)=D(1)=\tfrac12$, hàm lỗi $\ell(w,z)=(w-z)^2$ với $w\in[0,1]$ và thuật toán trung bình $A(s)=\bar z=\tfrac1m\sum_iz_i$.

- **(b1)** Với $m=2$, liệt kê bốn mẫu để tính $\mathbb EL_D(A(S))$, $\mathbb EL_S(A(S))$ và khoảng cách tổng quát hóa kì vọng. Tính trung bình thay một $\tfrac1m\sum_i\mathbb E\big[\ell(A(S^{(i)}),Z_i)-\ell(A(S),Z_i)\big]$.
- **(b2)** Chứng minh hệ số ổn định đều nhỏ nhất của $A$ với cỡ mẫu $m$ là $2/m-1/m^2$. So với cận $2/m$ suy từ tính $2$-Lipschitz của $\ell(\cdot,z)$ trên $[0,1]$.

**(c)** Giữ $D$, hàm lỗi và $A$ của (b), nhưng lấy $Z_1=Z_2=\cdots=Z_m$ với $Z_1\sim D$: mỗi $Z_i$ có phân bố $D$ (dạng yếu của (T1)) nhưng các quan sát không độc lập. Lấy $Z'\sim D$ độc lập với $Z_1$. Với $m=2$, tính $\mathbb E[L_D(A(S))-L_S(A(S))]$ và trung bình thay một, rồi chỉ ra bước hỏng của (a). Chứng minh rằng với $m\ge4$, bất đẳng thức của Định lý 06.10 sai.

**(d)** Tính $\mathbb E\lvert L_D(A(S))-L_S(A(S))\rvert$ cho thuật toán ở (b1). Dựa vào Ví dụ 06.5, giải thích vì sao lập luận đổi vai không chặn được $\mathbb E\lvert L_D-L_S\rvert$ nói chung.
:::

::: hint Gợi ý 1
Phần (a). Viết $\mathbb E\,\ell(A(S),Z')$ thành tổng theo $(s,z')\in\mathcal Z^{m+1}$ với trọng số $\Pr(S=s)\,D(z')$, rồi đổi biến bằng phép đổi chỗ tọa độ thứ $i$ và tọa độ cuối. Phần (b2). Trung bình $\bar z$ đổi đúng $\tfrac1m$ hoặc không đổi khi thay một quan sát.
:::

::: hint Gợi ý 2
Phần (b2). $\lvert(a-z)^2-(b-z)^2\rvert=\lvert a-b\rvert\,\lvert a+b-2z\rvert$. Phần (c). Khi mọi quan sát bằng nhau, $A(S)=Z_1$ và $L_S(A(S))=0$; trọng số $\Pr(S=s)$ không còn là tích, nên phép đổi chỗ ở (a) làm đổi trọng số.
:::

::: solution Lời giải Bài tập 06.2
**(a) Chứng minh bằng tổng hữu hạn.**

**Bước 1: rủi ro kì vọng; tính độc lập của $Z'$.** Theo định nghĩa của $L_D$,
$$
\begin{aligned}
&\mathbb EL_D(A(S))\\
&=\sum_s\Pr(S=s)\\
&\quad\cdot\sum_{z'}D(z')\,\ell(A(s),z').
\end{aligned}
$$
Vì $Z'$ độc lập với $S$, $\Pr(S=s,Z'=z')=\Pr(S=s)D(z')$, nên vế phải bằng $\mathbb E\,\ell(A(S),Z')$. Tính độc lập của $Z'$ được dùng ở dòng này.

**Bước 2: đổi vai; dạng đầy đủ của (T1).** Theo dạng đầy đủ của (T1), $\Pr(S=s)=D(z_1)\cdots D(z_m)$, nên trọng số
$$
\begin{aligned}
P(s,z')&=D(z_1)\cdots D(z_m)\\
&\quad\cdot D(z')
\end{aligned}
$$
là một tích, không đổi khi đổi chỗ $z_i$ và $z'$. Phép đổi chỗ $\tau_i:(s,z')\mapsto(s^{(i)},z_i)$ là song ánh của $\mathcal Z^{m+1}$ và giữ trọng số. Đổi biến theo $\tau_i$ trong tổng:
$$
\begin{aligned}
&\sum_{s,z'}P(s,z')\,\ell(A(s),z')\\
&=\sum_{s,z'}P(s,z')\,\ell(A(s^{(i)}),z_i).
\end{aligned}
$$
Dạng đầy đủ của (T1) được dùng ở dòng này.

**Bước 3: rủi ro thực nghiệm.** Vì $\sum_{z'}D(z')=1$,
$$
\begin{aligned}
&\mathbb EL_S(A(S))=\frac1m\sum_{i=1}^m\\
&\quad\sum_{s,z'}P(s,z')\,\ell(A(s),z_i).
\end{aligned}
$$

**Bước 4: hiệu; tính ổn định.** Trừ Bước 3 khỏi trung bình theo $i$ của Bước 1–2:
$$
\begin{aligned}
&\mathbb E\big[L_D(A(S))\\
&\quad-L_S(A(S))\big]\\
&=\frac1m\sum_{i=1}^m\sum_{s,z'}P(s,z')\\
&\quad\cdot\big[\ell(A(s^{(i)}),z_i)\\
&\qquad-\ell(A(s),z_i)\big].
\end{aligned}
$$
Theo Định nghĩa 06.9 với quan sát kiểm tra $z_i$, mỗi ngoặc vuông nằm trong $[-\epsilon_{\mathrm{stab}}(m),\epsilon_{\mathrm{stab}}(m)]$. Các trọng số không âm và có tổng $1$, nên trị tuyệt đối của vế trái không quá $\epsilon_{\mathrm{stab}}(m)$. Mọi tổng đều hữu hạn, nên không cần giả thiết khả tích.

**(b1) Liệt kê với $m=2$.**

**Bước 1: bảng.** Rủi ro kì vọng là $L_D(w)=\tfrac12w^2+\tfrac12(1-w)^2$. Bốn mẫu có cùng xác suất $\tfrac14$:

- **$s=(0,0)$.** $\bar z=0$, $L_D=\tfrac12$, $L_S=0$.
- **$s=(0,1)$ và $(1,0)$.** $\bar z=\tfrac12$, $L_D=\tfrac14$, $L_S=\tfrac12\big(\tfrac14+\tfrac14\big)=\tfrac14$.
- **$s=(1,1)$.** $\bar z=1$, $L_D=\tfrac12$, $L_S=0$.

**Bước 2: hai kì vọng.** Lấy trung bình theo bốn mẫu:
$$
\begin{aligned}
&\mathbb EL_D(A(S))\\
&=\tfrac14\big(\tfrac12+\tfrac14+\tfrac14+\tfrac12\big)\\
&=0{,}375,\\
&\mathbb EL_S(A(S))\\
&=\tfrac14\big(0+\tfrac14+\tfrac14+0\big)\\
&=0{,}125 .
\end{aligned}
$$
Khoảng cách tổng quát hóa kì vọng là $0{,}25$, bằng $2\sigma^2/m$ với $\sigma^2=\operatorname{Var}Z=\tfrac14$.

**Bước 3: trung bình thay một.** Hai chỉ số cho cùng giá trị; xét $i=1$. Ba biến $Z',Z_2,Z_1$ độc lập, cùng kì vọng $\tfrac12$ và phương sai $\tfrac14$, nên
$$
\begin{aligned}
&\mathbb E\big[\big(\tfrac{Z'+Z_2}2-Z_1\big)^2\big]\\
&=\operatorname{Var}\tfrac{Z'+Z_2}2+\operatorname{Var}Z_1\\
&=\tfrac18+\tfrac14=0{,}375,\\
&\mathbb E\,\ell(A(S),Z_1)=\tfrac14\mathbb E(Z_2-Z_1)^2\\
&=\tfrac14\cdot\tfrac12=0{,}125 .
\end{aligned}
$$
Trung bình thay một bằng $0{,}375-0{,}125=0{,}25$, đúng bằng khoảng cách tổng quát hóa kì vọng như Bước 4 của (a).

**(b2) Hệ số ổn định đều.**

**Bước 1: cận trên.** Gọi $a$ và $b$ là trung bình trên $s$ và trên $s^{(i)}$; khi đó $a,b\in[0,1]$ và $\lvert a-b\rvert\in\{0,\tfrac1m\}$. Với $\lvert a-b\rvert=\tfrac1m$, ta có $a+b\in[\tfrac1m,2-\tfrac1m]$, nên với $z\in\{0,1\}$,
$$
\begin{aligned}
&\lvert(a-z)^2-(b-z)^2\rvert\\
&=\lvert a-b\rvert\,\lvert a+b-2z\rvert\\
&\le\tfrac1m\big(2-\tfrac1m\big)=\tfrac2m-\tfrac1{m^2}.
\end{aligned}
$$

**Bước 2: đạt được.** Lấy $s=(0,\ldots,0)$, $z'=1$ và $z=1$: $a=0$, $b=\tfrac1m$, và hiệu hàm lỗi là $1-(1-\tfrac1m)^2=\tfrac2m-\tfrac1{m^2}$. Với $m=2$, hệ số nhỏ nhất là $0{,}75$.

**Bước 3: so với cận Lipschitz.** $\lvert\partial_w\ell\rvert=2\lvert w-z\rvert\le2$ trên $[0,1]$ và $\lvert a-b\rvert\le\tfrac1m$, nên cận Lipschitz là $\tfrac2m$, bằng $1$ khi $m=2$. Định lý 06.10 cho $0{,}25\le0{,}75$.

**(c) Mẫu gồm các bản sao.**

**Bước 1: khoảng cách tổng quát hóa với $m=2$.** $S=(Z_1,Z_1)$, nên $A(S)=Z_1$ và $L_S(A(S))=0$. Theo Bước 1 của (b1), $L_D(0)=L_D(1)=\tfrac12$, nên khoảng cách tổng quát hóa kì vọng bằng $0{,}5$.

**Bước 2: trung bình thay một.** Với $i=1$, $A(S^{(1)})=\tfrac12(Z'+Z_1)$ và $\ell(A(S^{(1)}),Z_1)=\tfrac14(Z'-Z_1)^2$, có kì vọng $\tfrac14\cdot\tfrac12=0{,}125$; còn $\ell(A(S),Z_1)=0$. Chỉ số $i=2$ cho cùng giá trị, nên trung bình thay một bằng $0{,}125\ne0{,}5$.

**Bước 3: bước hỏng.** Bước 1 và Bước 3 của (a) vẫn đúng. Bước 2 hỏng: $\Pr(S=s)=D(z_1)\,\mathbb 1[z_2=z_1]$ không phải tích. Chẳng hạn $(s,z')=((0,0),1)$ có trọng số $\tfrac12\cdot\tfrac12=\tfrac14$, còn ảnh $((1,0),0)$ của nó có trọng số $0$ vì $\Pr(S=(1,0))=0$.

**Bước 4: $m\ge4$.** Với $m$ bản sao, $A(S)=Z_1$ và khoảng cách tổng quát hóa kì vọng vẫn bằng $0{,}5$. Hệ số ổn định đều không phụ thuộc $D$, nên theo (b2) nó là $2/m-1/m^2$, bằng $0{,}4375$ khi $m=4$ và giảm theo $m$. Vậy $0{,}5>\epsilon_{\mathrm{stab}}(m)$ với mọi $m\ge4$: không có dạng đầy đủ của (T1), kết luận của Định lý 06.10 sai.

**(d) Kì vọng của trị tuyệt đối.**

**Bước 1: tính.** Theo bảng của (b1), $L_D-L_S$ bằng $\tfrac12$, $0$, $0$, $\tfrac12$ trên bốn mẫu, nên $\mathbb E\lvert L_D-L_S\rvert=0{,}25$. Hiệu không âm trên mọi mẫu, nên ở đây hai đại lượng trùng nhau.

**Bước 2: vì sao không có cận chung.** Lập luận đổi vai là đẳng thức giữa các kì vọng của hiệu có dấu, và trị tuyệt đối không đi qua phép lấy kì vọng đó. Ví dụ 06.5 có $\epsilon_{\mathrm{stab}}=0$ nhưng $\mathbb E\lvert L_D-L_S\rvert=0{,}1230$ với $m=10$.

**Kiểm tra lại.** Với $m=3$, $5/9\approx0{,}556>0{,}5$, nên ở (c) bất đẳng thức của Định lý 06.10 chỉ sai từ $m=4$.
:::

### Bài tập 06.3 (Cận khoảng cách giữa hai nghiệm của ERM có chính quy hóa)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 4; chỗ dùng từng giả thiết trong cận $2G/(\lambda m)$ và nguồn gốc của hằng số $2$.

::: exercise Bài tập 06.3
Giả thiết như Mệnh đề 06.11: $W$ khác rỗng, đóng, lồi; $\ell(\cdot,z)$ lồi trên $\mathbb R^p$, không âm trên $W$; (L) đúng với hằng số $G$; $\lambda>0$; mẫu $s$, chỉ số $i$, quan sát thay thế $z'$ và mẫu lân cận $s^{(i)}$. Đặt $\hat w=\hat w_s$ và $\hat w'=\hat w_{s^{(i)}}$.

**(a)** Chứng minh $\lVert\hat w-\hat w'\rVert\le2G/(\lambda m)$ bằng cách cộng hai bất đẳng thức tăng trưởng bậc hai. Ghi rõ dòng dùng tính lồi của $W$, dòng dùng tính lồi của $\ell(\cdot,z)$ và dòng dùng (L).

**(b)** Chỉ dùng tăng trưởng bậc hai của $F_{s,\lambda}$ quanh $\hat w$ và bất đẳng thức $F_{s^{(i)},\lambda}(\hat w')\le F_{s^{(i)},\lambda}(\hat w)$, chứng minh $\lVert\hat w-\hat w'\rVert\le4G/(\lambda m)$. Giải thích vì sao hằng số gấp đôi.

**(c)** Trên Ví dụ 06.4 với $\lambda=1$ ($G=4$, $m=4$), tính các vế của chuỗi bất đẳng thức ở (a) và ở (b), rồi so khoảng cách thật với hai cận.
:::

::: hint Gợi ý 1
Phần (a). Mỗi nghiệm làm nhỏ nhất mục tiêu của chính nó; viết tăng trưởng bậc hai của mỗi mục tiêu tại nghiệm của mục tiêu kia. Hai mục tiêu chỉ khác nhau ở một quan sát.
:::

::: hint Gợi ý 2
Phần (a). Dùng Bổ đề 06.8(c) cho $F_{s,\lambda}$ tại $\hat w'$ và cho $F_{s^{(i)},\lambda}$ tại $\hat w$; hiệu $F_{s,\lambda}-F_{s^{(i)},\lambda}$ bằng $\tfrac1m[\ell(\cdot,z_i)-\ell(\cdot,z')]$. Phần (b). Viết $F_{s,\lambda}(\hat w')-F_{s,\lambda}(\hat w)$ bằng $F_{s^{(i)},\lambda}(\hat w')-F_{s^{(i)},\lambda}(\hat w)$ cộng hai hiệu hàm lỗi chia cho $m$; số hạng thứ nhất không dương.
:::

::: solution Lời giải Bài tập 06.3
**(a) Lập luận đối xứng.**

**Bước 1: tính lồi mạnh; tính lồi của $\ell$.** Mỗi $\ell(\cdot,z)$ lồi, nên $L_s$ và $L_{s^{(i)}}$ lồi. Theo Bổ đề 06.8(a), $F_{s,\lambda}$ và $F_{s^{(i)},\lambda}$ là $\lambda$-lồi mạnh. Tính lồi của $\ell$ được dùng ở bước này.

**Bước 2: hai bất đẳng thức tăng trưởng; tính lồi của $W$.** $\hat w$ và $\hat w'$ thuộc $W$. Theo Bổ đề 06.7, cho $F_{s,\lambda}$ tại $\hat w'$ và cho $F_{s^{(i)},\lambda}$ tại $\hat w$:
$$
\begin{aligned}
&F_{s,\lambda}(\hat w')-F_{s,\lambda}(\hat w)\\
&\quad\ge\tfrac\lambda2\lVert\hat w-\hat w'\rVert^2,\\
&F_{s^{(i)},\lambda}(\hat w)-F_{s^{(i)},\lambda}(\hat w')\\
&\quad\ge\tfrac\lambda2\lVert\hat w-\hat w'\rVert^2 .
\end{aligned}
$$
Tính lồi của $W$ được dùng ở Bước 1 của chứng minh Bổ đề 06.7.

**Bước 3: cộng và triệt tiêu.** Hai mẫu chung $m-1$ quan sát và cùng số hạng chính quy hóa, nên $F_{s,\lambda}-F_{s^{(i)},\lambda}=\tfrac1m\big[\ell(\cdot,z_i)-\ell(\cdot,z')\big]$. Cộng hai bất đẳng thức:
$$
\begin{aligned}
&\lambda\lVert\hat w-\hat w'\rVert^2\\
&\le\tfrac1m\big[\ell(\hat w',z_i)-\ell(\hat w,z_i)\big]\\
&\quad+\tfrac1m\big[\ell(\hat w,z')-\ell(\hat w',z')\big].
\end{aligned}
$$

**Bước 4: (L).** $\hat w,\hat w'\in W$, nên (L) với $z_i$ và với $z'$ chặn mỗi ngoặc vuông bởi $G\lVert\hat w-\hat w'\rVert$; (L) được dùng ở đây. Vế phải không quá $2G\lVert\hat w-\hat w'\rVert/m$. Nếu $\hat w\ne\hat w'$, chia cho $\lambda\lVert\hat w-\hat w'\rVert$; nếu $\hat w=\hat w'$, vế trái của cận bằng $0$.

**(b) Lập luận một phía.**

**Bước 1: một bất đẳng thức tăng trưởng.** Như Bước 2 của (a), $\tfrac\lambda2\lVert\hat w-\hat w'\rVert^2\le F_{s,\lambda}(\hat w')-F_{s,\lambda}(\hat w)$.

**Bước 2: tách vế phải.** Theo đẳng thức của Bước 3 trong (a),
$$
\begin{aligned}
&F_{s,\lambda}(\hat w')-F_{s,\lambda}(\hat w)\\
&=F_{s^{(i)},\lambda}(\hat w')-F_{s^{(i)},\lambda}(\hat w)\\
&\quad+\tfrac1m\big[\ell(\hat w',z_i)-\ell(\hat w,z_i)\big]\\
&\quad+\tfrac1m\big[\ell(\hat w,z')-\ell(\hat w',z')\big].
\end{aligned}
$$

**Bước 3: tính tối ưu và (L).** Dòng thứ nhất của vế phải không dương vì $\hat w'$ là điểm nhỏ nhất của $F_{s^{(i)},\lambda}$ trên $W$. Hai dòng sau không quá $2G\lVert\hat w-\hat w'\rVert/m$. Do đó $\tfrac\lambda2\lVert\hat w-\hat w'\rVert^2\le2G\lVert\hat w-\hat w'\rVert/m$, tức $\lVert\hat w-\hat w'\rVert\le4G/(\lambda m)$.

**Bước 4: hằng số.** Vế phải của hai lập luận như nhau. Ở (a), vế trái là $\tfrac\lambda2+\tfrac\lambda2=\lambda$ nhân $\lVert\hat w-\hat w'\rVert^2$; ở (b), bất đẳng thức tăng trưởng thứ hai được thay bằng tính tối ưu, nên vế trái mất $\tfrac\lambda2\lVert\hat w-\hat w'\rVert^2$ và hằng số gấp đôi.

**(c) Bằng số với $\lambda=1$.**

**Bước 1: hai nghiệm.** Theo Ví dụ 06.4, $\hat w=10/21$ và $\hat w'=2/21$, nên $\lvert\hat w-\hat w'\rvert=8/21\approx0{,}3810$.

**Bước 2: chuỗi của (a).** Theo Ví dụ 06.6, Bước 2, hai hiệu hàm lỗi là $240/441$ và $432/441$, nên
$$
\begin{aligned}
&\lambda\lvert\hat w-\hat w'\rvert^2=\tfrac{64}{441}\approx0{,}1451\\
&\le\tfrac14\cdot\tfrac{672}{441}=\tfrac8{21}\approx0{,}3810\\
&\le\tfrac{2\cdot4}{4}\cdot\tfrac8{21}\approx0{,}7619 .
\end{aligned}
$$

**Bước 3: hai hiệu mục tiêu.** $F_{s,\lambda}(w)=1{,}3125w^2-1{,}25w+0{,}75$ đạt cực tiểu tại $\hat w$, nên $F_{s,\lambda}(w)-F_{s,\lambda}(\hat w)=1{,}3125(w-\hat w)^2$. Với $(\hat w'-\hat w)^2=\tfrac{64}{441}$,
$$
\begin{aligned}
&F_{s,\lambda}(\hat w')-F_{s,\lambda}(\hat w)\\
&=1{,}3125\cdot\tfrac{64}{441}=\tfrac4{21}\approx0{,}1905 .
\end{aligned}
$$
Tương tự, $F_{s^{(i)},\lambda}(\hat w')-F_{s^{(i)},\lambda}(\hat w)=-\tfrac4{21}$.

**Bước 4: chuỗi của (b).** Thay vào Bước 1–3 của (b):
$$
\begin{aligned}
&\tfrac\lambda2\lvert\hat w-\hat w'\rvert^2\approx0{,}0726\\
&\le-0{,}1905+0{,}3810=0{,}1905\\
&\le0+0{,}7619 .
\end{aligned}
$$

**Bước 5: so sánh.** Hai cận là $2$ và $4$, so với khoảng cách thật $0{,}3810$: lỏng khoảng $5$ và $10$ lần.

**Kiểm tra lại.** Ở Bước 4 của (c), $0{,}1905>0{,}0726$ vì $L_s$ tự nó đã $1{,}625$-lồi mạnh; Bổ đề 06.7 chỉ dùng độ cong $\lambda=1$ của số hạng chính quy hóa.
:::

### Bài tập 06.4 (Chọn hệ số chính quy hóa khi biết cận chuẩn của điểm so sánh)

**Mức độ:** tính toán, khái niệm. **Mục tiêu:** mục tiêu học tập 4, 5; chọn $\lambda$ theo cận, cái giá khi đoán sai chuẩn của điểm so sánh, và lý do không chọn $\lambda$ trên mẫu huấn luyện.

::: exercise Bài tập 06.4
Giả thiết như Hệ quả 06.13. Với một điểm so sánh $u\in W$ có $\lVert u\rVert\le B$, phần (a) của hệ quả cho $\mathbb E_SL_D(\hat w_S)-L_D(u)\le Q(\lambda)$, trong đó
$$
Q(\lambda)=\frac{2G^2}{\lambda m}+\frac{\lambda B^2}2 .
$$

**(a)** Tìm $\lambda>0$ làm nhỏ nhất $Q$ và giá trị nhỏ nhất. Suy ra cỡ mẫu đủ để giá trị nhỏ nhất không quá $\epsilon$.

**(b)** Với $\lambda=c\lambda^*$ và $c>0$, chứng minh $Q(c\lambda^*)=Q(\lambda^*)\cdot\tfrac12(c+1/c)$. Tính thừa số $\tfrac12(c+1/c)$ với $c=2$, $c=\tfrac12$ và $c=10$.

**(c)** Hồi quy logistic với $\lVert x\rVert\le4$ và $W=\mathbb R^p$: gradient của hàm lỗi có chuẩn không quá $\lVert x\rVert$ (Ví dụ 05.9), nên (L) đúng với $G=4$. Cho $m=1600$. Hệ số được chọn theo (a) với $B_0=1$, trong khi điểm so sánh có chuẩn $B=2$. Viết $Q$ tại hệ số đó theo $G$, $m$, $B_0$, $B$, tính giá trị và so với $Q(\lambda^*)$ tính với $B=2$. Tính hệ số ổn định của Mệnh đề 06.11 tại hai hệ số đó.

**(d)** Với cùng mẫu $S$, lấy $0<\lambda_1<\lambda_2$ và gọi $\hat w_1$, $\hat w_2$ là hai nghiệm tương ứng. Chứng minh $\lVert\hat w_1\rVert\ge\lVert\hat w_2\rVert$ và $L_S(\hat w_1)\le L_S(\hat w_2)$. Kiểm tra bằng các số của Ví dụ 06.4. Vì sao không chọn $\lambda$ trong một lưới bằng $L_S$ trên chính mẫu huấn luyện? Nêu cách chọn bằng mẫu xác thực và điều kiện của Hệ quả 04.17 về hàm lỗi.
:::

::: hint Gợi ý 1
Phần (a). Bất đẳng thức trung bình cộng–trung bình nhân, như câu hỏi ôn nhanh 3. Phần (d). Dùng tính tối ưu của mỗi nghiệm cho mục tiêu của chính nó, so với nghiệm kia.
:::

::: hint Gợi ý 2
Phần (b). $2G^2/(c\lambda^*m)=GB/(c\sqrt m)$ và $c\lambda^*B^2/2=cGB/\sqrt m$. Phần (c). Hệ số đã chọn là $\lambda_0=2G/(B_0\sqrt m)$. Phần (d). Viết $F_{S,\lambda_1}(\hat w_1)\le F_{S,\lambda_1}(\hat w_2)$ và $F_{S,\lambda_2}(\hat w_2)\le F_{S,\lambda_2}(\hat w_1)$ rồi cộng.
:::

::: solution Lời giải Bài tập 06.4
**(a) Hệ số tốt nhất theo cận.**

**Bước 1: dạng chung.** Đặt $a=2G^2/m$ và $b=B^2/2$, nên $Q(\lambda)=a/\lambda+b\lambda$. Theo bất đẳng thức trung bình cộng–trung bình nhân, $Q(\lambda)\ge2\sqrt{ab}$, với dấu bằng khi $a/\lambda=b\lambda$, tức $\lambda=\sqrt{a/b}$.

**Bước 2: thay số.** Ta có
$$
\begin{aligned}
\lambda^*&=\sqrt{\frac{4G^2}{mB^2}}=\frac{2G}{B\sqrt m},\\
Q(\lambda^*)&=2\sqrt{\frac{G^2B^2}m}=\frac{2GB}{\sqrt m}.
\end{aligned}
$$

**Bước 3: cỡ mẫu.** $2GB/\sqrt m\le\epsilon$ khi và chỉ khi $m\ge4G^2B^2/\epsilon^2$. Đây là Hệ quả 06.13(c).

**(b) Hệ số lệch một thừa số $c$.**

**Bước 1: hai số hạng.** Với $\lambda=c\lambda^*$,
$$
\begin{aligned}
\frac{2G^2}{c\lambda^*m}&=\frac{2G^2B\sqrt m}{2cGm}=\frac{GB}{c\sqrt m},\\
\frac{c\lambda^*B^2}2&=\frac{cGB}{\sqrt m}.
\end{aligned}
$$

**Bước 2: tổng.** $Q(c\lambda^*)=\tfrac{GB}{\sqrt m}(c+\tfrac1c)=Q(\lambda^*)\cdot\tfrac12(c+\tfrac1c)$.

**Bước 3: bằng số.** Với $c=2$ và $c=\tfrac12$, thừa số là $\tfrac12(2+0{,}5)=1{,}25$; với $c=10$, thừa số là $\tfrac12(10+0{,}1)=5{,}05$. Lệch $\lambda^*$ một thừa số $2$ làm cận tăng $25\%$; lệch một thừa số $10$ làm cận gấp $5{,}05$ lần.

**(c) Đoán sai chuẩn của điểm so sánh.**

**Bước 1: hệ số đã chọn.** $\sqrt m=40$ và $\lambda_0=2\cdot4/(1\cdot40)=0{,}2$.

**Bước 2: dạng tổng quát.** Với $\lambda_0=2G/(B_0\sqrt m)$,
$$
\begin{aligned}
Q(\lambda_0)&=\frac{GB_0}{\sqrt m}+\frac{GB^2}{B_0\sqrt m}\\
&=\frac G{\sqrt m}\Big(B_0+\frac{B^2}{B_0}\Big).
\end{aligned}
$$

**Bước 3: bằng số.** Với $G/\sqrt m=0{,}1$, $Q(\lambda_0)=0{,}1\cdot(1+4)=0{,}5$.

**Bước 4: so với hệ số đúng.** Với $B=2$, $\lambda^*=8/80=0{,}1$ và $Q(\lambda^*)=16/40=0{,}4$. Ở đây $\lambda_0=2\lambda^*$, nên tỉ số $0{,}5/0{,}4=1{,}25$ là thừa số của (b) với $c=2$. Cận $0{,}5$ vẫn đúng, vì phần (a) của Hệ quả 06.13 đúng với mọi $\lambda>0$ và mọi $u\in W$.

**Bước 5: hệ số ổn định của hồi quy logistic.** Theo Mệnh đề 06.11(b) với $G=4$, $m=1600$:
$$
\begin{aligned}
\epsilon_{\mathrm{stab}}&=\frac{2\cdot16}{0{,}2\cdot1600}=0{,}1\quad(\lambda_0),\\
\epsilon_{\mathrm{stab}}&=\frac{2\cdot16}{0{,}1\cdot1600}=0{,}2\quad(\lambda^*).
\end{aligned}
$$
Tại $\lambda_0=2\lambda^*$, hệ số ổn định giảm một nửa, từ $0{,}2$ xuống $0{,}1$, còn số hạng khớp $\lambda B^2/2$ tăng từ $0{,}2$ lên $0{,}4$; hai tổng là $0{,}4$ và $0{,}5$, như Bước 4.

**(d) Chọn $\lambda$ trên mẫu huấn luyện.**

**Bước 1: chuẩn của nghiệm.** Hai bất đẳng thức tối ưu là
$$
\begin{aligned}
&L_S(\hat w_1)+\tfrac{\lambda_1}2\lVert\hat w_1\rVert^2\\
&\quad\le L_S(\hat w_2)+\tfrac{\lambda_1}2\lVert\hat w_2\rVert^2,\\
&L_S(\hat w_2)+\tfrac{\lambda_2}2\lVert\hat w_2\rVert^2\\
&\quad\le L_S(\hat w_1)+\tfrac{\lambda_2}2\lVert\hat w_1\rVert^2 .
\end{aligned}
$$
Cộng lại, các số hạng $L_S$ triệt tiêu và còn $\tfrac{\lambda_2-\lambda_1}2\big(\lVert\hat w_1\rVert^2-\lVert\hat w_2\rVert^2\big)\ge0$. Vì $\lambda_2>\lambda_1$, ta được $\lVert\hat w_1\rVert\ge\lVert\hat w_2\rVert$.

**Bước 2: rủi ro thực nghiệm.** Theo bất đẳng thức thứ nhất và Bước 1,
$$
\begin{aligned}
L_S(\hat w_1)&\le L_S(\hat w_2)\\
&\quad+\tfrac{\lambda_1}2\big(\lVert\hat w_2\rVert^2-\lVert\hat w_1\rVert^2\big)\\
&\le L_S(\hat w_2).
\end{aligned}
$$

**Bước 3: Ví dụ 06.4.** Bước 1–2 vẫn đúng khi $\lambda_1=0$ nếu nghiệm tồn tại. Với $\lambda=0,1,4$, nghiệm là $0{,}7692$; $0{,}4762$; $0{,}2222$ (giảm) và $L_S(\hat w_S)$ là $0{,}2692$; $0{,}3390$; $0{,}5123$ (tăng).

**Bước 4: hệ quả cho việc chọn $\lambda$.** Theo Bước 2, chọn theo $L_S$ luôn cho $\lambda$ nhỏ nhất của lưới, tức hệ số có số hạng ổn định $2G^2/(\lambda m)$ lớn nhất: $L_S(\hat w_S)$ không đo khoảng cách tổng quát hóa.

**Bước 5: mẫu xác thực.** Cố định trước một lưới $\Lambda$ gồm $K$ giá trị, tính $\hat w_{S,\lambda}$ trên $S$ với mọi $\lambda\in\Lambda$, rồi chọn ứng viên có rủi ro nhỏ nhất trên một mẫu xác thực $V$ độc lập với $S$. Hệ quả 04.17(a) chặn phần vượt so với ứng viên tốt nhất bởi $2\sqrt{\ln(2K/\delta)/(2m_v)}$, với xác suất ít nhất $1-\delta$, khi hàm lỗi nhận giá trị trong $[0,1]$ ((T3)). Với hồi quy ridge trên quả cầu đơn vị và $\lvert y\rvert\le1$, hàm lỗi không quá $4$, nên ta áp dụng cho hàm lỗi chia $4$.

**Kiểm tra lại.** Dạng tổng quát ở (c) với $B_0=B$ cho lại $2GB/\sqrt m$; với $B_0=4$, $B=2$, nó cho $0{,}1\cdot(4+1)=0{,}5$, như (b) dự báo với $c=\tfrac12$.
:::

### Bài tập 06.5 (Hồi quy ridge khi dữ liệu không bị chặn hoặc tập tham số không bị chặn)

**Mức độ:** kiểm tra giả thiết, chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 5; giả thiết (L) với hàm lỗi bình phương, và cận cho chuẩn của nghiệm thay cho tập tham số bị chặn.

::: exercise Bài tập 06.5
Hồi quy ridge: $\ell(w,(x,y))=(\langle w,x\rangle-y)^2$ và $\lambda>0$.

**(a)** Trong Ví dụ 06.9 ($p=1$, $W=\mathbb R$, $\lambda=1$, $m=100$), chứng minh rằng đạo hàm của hàm lỗi trên quan sát $(M,0)$ tại $\hat w_S=\tfrac23$ không bị chặn theo $M$, nên không có $G$ hữu hạn cho (L). Với $M=10$, tính lại $\hat w_{S^{(100)}}$ và thay đổi của hàm lỗi tại $(1,1)$.

**(b)** Dữ liệu bị chặn: $\lVert x\rVert\le C_x$ và $\lvert y\rvert\le C_y$ trên $\mathcal Z$, còn $W=\mathbb R^p$. Chứng minh rằng với mọi mẫu $s$,
$$
\lVert\hat w_s\rVert\le r_\lambda=C_y\sqrt{2/\lambda}.
$$
Suy ra $\hat w_s$ cũng là nghiệm của ERM có chính quy hóa trên quả cầu $\{w:\lVert w\rVert\le r_\lambda\}$, và ERM có chính quy hóa trên $\mathbb R^p$ ổn định đều với hệ số $2G_\lambda^2/(\lambda m)$, trong đó $G_\lambda=2(C_xr_\lambda+C_y)C_x$.

**(c)** Với $C_x=C_y=1$ và $m=1000$, tính $r_\lambda$, $G_\lambda$ và $2G_\lambda^2/(\lambda m)$ cho $\lambda=1$; $0{,}1$; $0{,}01$. Hệ số này tăng theo bậc nào của $1/\lambda$ khi $\lambda\to0$?

**(d)** So với cận $192C_x^2C_y^2/(\lambda m)$ của Nhận xét 06.12: kiểm điều kiện $\lambda\ge8C_x^2/m$, tính cận với ba giá trị $\lambda$ ở (c), và nêu hai khác biệt giữa hai cận.
:::

::: hint Gợi ý 1
Phần (b). So giá trị nhỏ nhất của $F_{s,\lambda}$ với giá trị của nó tại một điểm cụ thể của $\mathbb R^p$; sau đó chặn $F_{s,\lambda}(\hat w_s)$ từ dưới.
:::

::: hint Gợi ý 2
Phần (b). Lấy điểm $0$ và dùng $\ell\ge0$. Một điểm thuộc một tập con của $\mathbb R^p$ và làm nhỏ nhất $F$ trên $\mathbb R^p$ thì làm nhỏ nhất $F$ trên tập con đó. Trên quả cầu bán kính $r_\lambda$, cận của Bài 05 (đoạn sau Định nghĩa 05.4) cho hằng số Lipschitz $G_\lambda$.
:::

::: solution Lời giải Bài tập 06.5
**(a) Dữ liệu không bị chặn.**

**Bước 1: đạo hàm.** Với quan sát $(M,0)$, đạo hàm theo $w$ của $(wM-0)^2$ là $2wM^2$. Tại $w=\tfrac23$, nó bằng $\tfrac43M^2$, tức $133{,}3$ với $M=10$ và $13\,333$ với $M=100$. Không có $G$ hữu hạn nào chặn đạo hàm này với mọi $M$.

**Bước 2: hai nghiệm với $M=10$.** Theo công thức một chiều của Ví dụ 06.4 với $\lambda m/2=50$,
$$
\begin{aligned}
\hat w_S&=\frac{100}{100+50}\approx0{,}6667,\\
\hat w_{S^{(100)}}&=\frac{99}{99+100+50}=\frac{99}{249}\\
&\approx0{,}3976 .
\end{aligned}
$$

**Bước 3: thay đổi hàm lỗi.** Tại $(1,1)$, hàm lỗi là $(w-1)^2$:
$$
\begin{aligned}
&(0{,}3976-1)^2-\big(\tfrac23-1\big)^2\\
&\approx0{,}3629-0{,}1111\approx0{,}2518,
\end{aligned}
$$
khớp Bước 3 của Ví dụ 06.9.

**(b) Dữ liệu bị chặn, $W=\mathbb R^p$.**

**Bước 1: so với điểm $0$.** Vì $\hat w_s$ làm nhỏ nhất $F_{s,\lambda}$,
$$
\begin{aligned}
F_{s,\lambda}(\hat w_s)&\le F_{s,\lambda}(0)=\frac1m\sum_iy_i^2\\
&\le C_y^2 .
\end{aligned}
$$

**Bước 2: dùng $\ell\ge0$.** $L_s\ge0$, nên $F_{s,\lambda}(\hat w_s)\ge\tfrac\lambda2\lVert\hat w_s\rVert^2$. Ghép với Bước 1, $\lVert\hat w_s\rVert^2\le2C_y^2/\lambda$, tức $\lVert\hat w_s\rVert\le r_\lambda$. Cận chỉ dùng $C_y$ và $\lambda$, nên đúng cho mọi mẫu, kể cả $s^{(i)}$.

**Bước 3: thu về quả cầu.** Đặt $W_{r_\lambda}=\{w:\lVert w\rVert\le r_\lambda\}$, khác rỗng, đóng, lồi. $\hat w_s\in W_{r_\lambda}$ và làm nhỏ nhất $F_{s,\lambda}$ trên $\mathbb R^p\supseteq W_{r_\lambda}$, nên làm nhỏ nhất $F_{s,\lambda}$ trên $W_{r_\lambda}$; theo Bổ đề 06.8, đó là nghiệm duy nhất trên $W_{r_\lambda}$. Vậy trên mọi mẫu, ERM có chính quy hóa trên $\mathbb R^p$ và trên $W_{r_\lambda}$ cho cùng đầu ra.

**Bước 4: (L) trên $W_{r_\lambda}$.** Với $w\in W_{r_\lambda}$ và $(x,y)\in\mathcal Z$, gradient $2(\langle w,x\rangle-y)x$ có chuẩn không quá $2(r_\lambda C_x+C_y)C_x=G_\lambda$. Theo Mệnh đề 05.5(a), (L) đúng trên $W_{r_\lambda}$ với hằng số $G_\lambda$.

**Bước 5: hệ số ổn định.** Mệnh đề 06.11(b) với tập tham số $W_{r_\lambda}$ cho $\epsilon_{\mathrm{stab}}(m)=2G_\lambda^2/(\lambda m)$; theo Bước 3, đây cũng là hệ số của ERM có chính quy hóa trên $\mathbb R^p$.

**(c) Bằng số với $C_x=C_y=1$, $m=1000$.** Ta có $r_\lambda=\sqrt{2/\lambda}$ và $G_\lambda=2(r_\lambda+1)$.

- **$\lambda=1$.** $r_\lambda\approx1{,}4142$, $G_\lambda\approx4{,}8284$, $G_\lambda^2\approx23{,}314$, hệ số $\approx46{,}63/1000\le0{,}0467$.
- **$\lambda=0{,}1$.** $r_\lambda\approx4{,}4721$, $G_\lambda\approx10{,}944$, $G_\lambda^2\approx119{,}78$, hệ số $\approx239{,}55/100\le2{,}3956$.
- **$\lambda=0{,}01$.** $r_\lambda\approx14{,}142$, $G_\lambda\approx30{,}284$, $G_\lambda^2\approx917{,}14$, hệ số $\approx1834{,}3/10\approx183{,}43$.

Khi $\lambda\to0$, $G_\lambda^2\approx8C_x^4C_y^2/\lambda$, nên hệ số xấp xỉ $16C_x^4C_y^2/(\lambda^2m)$, bậc $\lambda^{-2}$; từ $\lambda=0{,}1$ xuống $0{,}01$, nó tăng khoảng $77$ lần.

**(d) So với Nhận xét 06.12.**

**Bước 1: điều kiện.** $8C_x^2/m=0{,}008$, nhỏ hơn cả ba giá trị $\lambda$.

**Bước 2: bằng số.** $192/(\lambda m)$ bằng $0{,}192$; $1{,}92$; $19{,}2$ với $\lambda=1$; $0{,}1$; $0{,}01$.

**Bước 3: hai khác biệt.** Nhận xét 06.12 chặn một phía khoảng cách tổng quát hóa kì vọng qua một dạng ổn định theo trung bình, còn (b) cho hệ số ổn định đều. Cận của Nhận xét 06.12 có bậc $\lambda^{-1}$, nên nhỏ hơn khi $\lambda\le0{,}1$ ($1{,}92<2{,}3956$; $19{,}2<183{,}43$) và lớn hơn khi $\lambda=1$ ($0{,}192>0{,}0467$).

**Kiểm tra lại.** Ở Ví dụ 06.4 với $\lambda=1$ trên $W=[-1,1]$, nghiệm $0{,}4762$ cũng là nghiệm trên $\mathbb R$ và có chuẩn không quá $r_1=\sqrt2\approx1{,}4142$, đúng như (b).
:::

### Bài tập 06.6 (Thay một quan sát và đo độ nhạy, thực nghiệm tùy chọn)

**Mức độ:** tính toán, thực nghiệm (tùy chọn). **Mục tiêu:** mục tiêu học tập 5; đo độ nhạy của nghiệm khi thay một quan sát và đọc đánh đổi khớp–ổn định trên dữ liệu.

::: exercise Bài tập 06.6
**(a)** (Bắt buộc, tính tay.) Lập lại Bước 2–3 của Ví dụ 06.4 với $\lambda=2$: tính $\hat w_S$, $\hat w_{S^{(4)}}$, khoảng cách giữa hai nghiệm và $L_S(\hat w_S)$. So khoảng cách với cận $2G/(\lambda m)$ của Mệnh đề 06.11. Xếp bốn giá trị $\lambda\in\{0,1,2,4\}$ theo khoảng cách và theo $L_S(\hat w_S)$.

**(b)** (Thực nghiệm, tùy chọn.) Viết giao thức thực nghiệm đo độ nhạy của hồi quy ridge trên $W=\mathbb R^p$ với dữ liệu tổng hợp thỏa $\lVert x\rVert\le1$, $\lvert y\rvert\le1$: cách sinh dữ liệu, lưới $\lambda$, cách thay một quan sát, các đại lượng đo trên một tập kiểm tra độc lập, số lần lặp, cách báo cáo, đại lượng lý thuyết để so sánh và phạm vi của kết luận.

**(c)** (Thực nghiệm, tùy chọn.) Cho mẫu $S$ gồm bốn quan sát trong $\mathbb R^2\times\mathbb R$:
$$
\begin{aligned}
z_1&=((0{,}8;0{,}6),1),\\
z_2&=((0{,}6;0{,}8),-1),\\
z_3&=((0{,}7;0{,}7),0),\\
z_4&=((-0{,}6;-0{,}8),-1),
\end{aligned}
$$
và mẫu $S^{(4)}$ thay $z_4$ bằng $z'=((0{,}8;0{,}6),1)$. Với hàm lỗi bình phương và $W=\mathbb R^2$, vẽ các đường mức (level curves) của $F_{S,\lambda}$ và $F_{S^{(4)},\lambda}$ với $\lambda=0{,}01$ và $\lambda=1$, đánh dấu hai nghiệm trên mỗi hình. Giải thích hình dạng các đường mức bằng ma trận đạo hàm bậc hai (Hessian matrix) của $F_{S,\lambda}$.
:::

::: hint Gợi ý 1
Phần (a). Dùng công thức ở Bước 2 của Ví dụ 06.4; với $\lambda=2$, mẫu số là $3{,}25+2\lambda=7{,}25$.
:::

::: hint Gợi ý 2
Phần (c). $F_{S,\lambda}$ là đa thức bậc hai theo $w$, có ma trận đạo hàm bậc hai $H_\lambda=\tfrac2m\sum_ix_ix_i^\top+\lambda I$ và nghiệm $\hat w_S=H_\lambda^{-1}\cdot\tfrac2m\sum_iy_ix_i$. Đường mức của một đa thức bậc hai như vậy là các elip có trục theo các véc-tơ riêng của $H_\lambda$.
:::

::: solution Lời giải Bài tập 06.6
**(a) Tính tay với $\lambda=2$.**

**Bước 1: hai nghiệm.** Theo Bước 2 của Ví dụ 06.4,
$$
\begin{aligned}
\hat w_S&=\frac{2{,}5}{7{,}25}=\frac{10}{29}\approx0{,}3448,\\
\hat w_{S^{(4)}}&=\frac{0{,}5}{7{,}25}=\frac2{29}\approx0{,}0690 .
\end{aligned}
$$

**Bước 2: khoảng cách và cận.** Khoảng cách là $8/29\approx0{,}2759$. Với $G=4$ và $m=4$, cận là $2\cdot4/(2\cdot4)=1$, lỏng khoảng $3{,}6$ lần.

**Bước 3: rủi ro thực nghiệm.** Thay $w=10/29$ vào $L_S$ của Ví dụ 06.1:
$$
\begin{aligned}
&L_S(\hat w_S)\\
&=\tfrac14\big(3{,}25\cdot\tfrac{100}{841}-\tfrac{50}{29}+3\big)\\
&\approx\tfrac14(0{,}3864-1{,}7241+3)\\
&\approx0{,}4156 .
\end{aligned}
$$

**Bước 4: bốn giá trị $\lambda$.** Với $\lambda=0,1,2,4$, khoảng cách là $0{,}6154$; $0{,}3810$; $0{,}2759$; $0{,}1778$ (giảm), còn $L_S(\hat w_S)$ là $0{,}2692$; $0{,}3390$; $0{,}4156$; $0{,}5123$ (tăng).

**(b) Giao thức thực nghiệm.**

- **Dữ liệu.** Chọn trước $p$, $m$ (chẳng hạn $p=20$, $m=200$) và hạt giống ngẫu nhiên (random seed). Sinh $x$ đều trên quả cầu đơn vị và $y$ bằng một hàm tuyến tính cố định của $x$ cộng nhiễu, cắt về $[-1,1]$.
- **Lưới và phép thay.** Lưới $\lambda$ cố định trước, cách đều theo thang logarit (chẳng hạn từ $10^{-3}$ đến $10$). Mỗi lần lặp rút $S\sim D^m$, một chỉ số $i$ đều và một quan sát mới $Z'\sim D$; với mỗi $\lambda$, giải hệ $H_\lambda w=\tfrac2m\sum_iy_ix_i$ (Gợi ý 2) cho $S$ và cho $S^{(i)}$.
- **Đại lượng đo.** Khoảng cách $\lVert\hat w_S-\hat w_{S^{(i)}}\rVert$; thay đổi lớn nhất của dự đoán $\lvert\langle\hat w_S-\hat w_{S^{(i)}},x\rangle\rvert$ trên một tập kiểm tra độc lập (chẳng hạn $10\,000$ quan sát); rủi ro của $\hat w_S$ trên tập kiểm tra đó, ước lượng của $L_D(\hat w_S)$.
- **Lặp và báo cáo.** Ít nhất $50$ lần lặp với mẫu mới; với mỗi $\lambda$, báo cáo trung bình, độ lệch chuẩn và sai số chuẩn, vẽ theo $\lambda$ trên trục logarit kèm thanh sai số. Vẽ thêm cận $2G_\lambda/(\lambda m)$ của Bài tập 06.5(b); vì $\lVert x\rVert\le1$, cận này chặn cả hai đại lượng đầu.
- **Kết quả mong đợi và phạm vi.** Khoảng cách giảm theo $\lambda$ và nằm dưới cận; rủi ro kiểm tra có thể giảm rồi tăng. Đường cong là minh họa cho $D$, $p$, $m$ đã chọn, không phải chứng minh: cận đúng trên mọi mẫu, còn thực nghiệm chỉ cho giá trị điển hình. Chỉ so hai giá trị $\lambda$ khi hiệu lớn hơn vài sai số chuẩn, và không chọn $\lambda$ bằng chính tập kiểm tra dùng để báo cáo (Bài tập 06.4(d)).

**(c) Đường mức hai chiều.**

**Bước 1: ma trận đạo hàm bậc hai.** Với $S$, $H_\lambda=\tfrac2m\sum_ix_ix_i^\top+\lambda I$. Bốn véc-tơ $x_i$ nằm gần đường thẳng qua gốc theo phương $(1,1)$, nên $\tfrac2m\sum_ix_ix_i^\top$ có một trị riêng gần $0$ với véc-tơ riêng gần phương $(1,-1)$. Bằng số, trị riêng của $H_\lambda$ là $0{,}0375$ và $1{,}9725$ khi $\lambda=0{,}01$; là $1{,}0275$ và $2{,}9625$ khi $\lambda=1$.

**Bước 2: hình dạng đường mức.** Đường mức của $F_{S,\lambda}$ là các elip có bán trục theo mỗi véc-tơ riêng tỉ lệ với nghịch đảo căn bậc hai của trị riêng tương ứng. Tỉ số giữa trục dài và trục ngắn là $\sqrt{1{,}9725/0{,}0375}\approx7{,}3$ khi $\lambda=0{,}01$ và $\sqrt{2{,}9625/1{,}0275}\approx1{,}7$ khi $\lambda=1$. Với $\lambda$ nhỏ, $F_{S,\lambda}$ gần như phẳng theo phương $(1,-1)$; số hạng $\lambda I$ thêm độ cong $\lambda$ theo mọi phương.

**Bước 3: hai nghiệm.** Giải hệ của Gợi ý 2:

- **$\lambda=0{,}01$.** $\hat w_S\approx(1{,}9012;-1{,}4276)$, $\hat w_{S^{(4)}}\approx(3{,}7145;-3{,}6198)$, khoảng cách $\approx2{,}8449$.
- **$\lambda=1$.** $\hat w_S\approx(0{,}1763;0{,}0629)$, $\hat w_{S^{(4)}}\approx(0{,}2528;-0{,}0228)$, khoảng cách $\approx0{,}1149$.

**Bước 4: đọc hình.** Với $\lambda=0{,}01$, thay một quan sát dời nghiệm $2{,}84$ dọc theo phương phẳng, gần phương $(1,-1)$. Với $\lambda=1$, các đường mức gần tròn hơn và nghiệm chỉ dời $0{,}11$, ít hơn khoảng $25$ lần: độ cong $\lambda$ của số hạng chính quy hóa giới hạn khoảng dời của nghiệm, như trong chứng minh Mệnh đề 06.11.

**Kiểm tra lại.** Ở (a), đạo hàm $\tfrac14(6{,}5\cdot\tfrac{10}{29}-5)+2\cdot\tfrac{10}{29}=\tfrac14\cdot\big(-\tfrac{80}{29}\big)+\tfrac{20}{29}=0$, nên $\hat w_S=10/29$ là điểm dừng. Ở (c), $\hat w_S$ với $\lambda=1$ thỏa $H_1\hat w_S=\tfrac12\sum_iy_ix_i=(0{,}4;0{,}3)$, với $H_1$ có các phần tử $1{,}925$; $0{,}965$; $2{,}065$: $1{,}925\cdot0{,}1763+0{,}965\cdot0{,}0629\approx0{,}4$.
:::

## Bài tập chọn từ UML

### Bài tập 06.7 (Cận với xác suất cao và tăng độ tin cậy từ một cận kì vọng; UML Bài tập 13.1, phát biểu đã chỉnh hằng số)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 5; đổi một bảo đảm theo kì vọng thành bảo đảm với xác suất cao, và so cái giá của bất đẳng thức Markov với cách chia khối.

::: exercise Bài tập 06.7
Cho lớp $\mathcal H$, hàm lỗi $\ell$ thỏa (T2) và một thuật toán tất định $A$ học đúng lớp, tức $A(S)\in\mathcal H$. Giả sử có một hàm $\bar m(\epsilon)$ (cỡ mẫu cho mức kì vọng, khác độ phức tạp mẫu $m_{\mathcal H}(\epsilon,\delta)$) sao cho với mọi $\epsilon>0$, mọi phân bố $D$ có $\inf_{\mathcal H}L_D<\infty$ và mọi $m\ge \bar m(\epsilon)$,
$$
\begin{aligned}
&\mathbb E_{S\sim D^m}L_D(A(S))\\
&\quad\le\inf_{h\in\mathcal H}L_D(h)+\epsilon .
\end{aligned}
$$
Phát biểu ở (b) đã chỉnh hằng số so với UML; phần (d) giải thích vì sao.

**(a)** Cho $\delta\in(0,1)$ và $m\ge \bar m(\epsilon\delta)$. Chứng minh
$$
\begin{aligned}
&\Pr_S\big[L_D(A(S))\\
&\qquad-\inf_{\mathcal H}L_D\ge\epsilon\big]\le\delta .
\end{aligned}
$$
Chỉ ra chỗ cần $A(S)\in\mathcal H$.

**(b)** Giả sử thêm $\ell$ nhận giá trị trong $[0,1]$, tức (T3). Đặt $k=\lceil\log_2(2/\delta)\rceil$. Thủ tục dùng $k$ khối huấn luyện, mỗi khối $\bar m(\epsilon/4)$ quan sát, và một mẫu xác thực $V$ cỡ $m_v\ge8\ln(4k/\delta)/\epsilon^2$; mọi khối và $V$ là các phần rời nhau của một mẫu độc lập cùng phân bố $D$. Thủ tục chạy $A$ trên khối thứ $j$ để được $h_j$, rồi trả về $\hat g$ là ứng viên có rủi ro nhỏ nhất trên $V$. Chứng minh rằng với xác suất ít nhất $1-\delta$,
$$
L_D(\hat g)\le\inf_{\mathcal H}L_D+\epsilon .
$$

**(c)** Lấy hàm lỗi $\ell(w,(x,y))=\tfrac14(\langle w,x\rangle-y)^2$ với $\lVert x\rVert\le1$, $\lvert y\rvert\le1$, lớp $W$ là quả cầu đơn vị, và $A$ là ERM có chính quy hóa với $\lambda^*$. Chứng minh $\ell$ nhận giá trị trong $[0,1]$, (L) đúng với $G=1$, và theo Hệ quả 06.13(c) có thể lấy $\bar m(\epsilon)=\lceil4/\epsilon^2\rceil$. Với $\epsilon=0{,}1$, tính cỡ mẫu theo (a) và theo (b) khi $\delta=0{,}05$ và khi $\delta=0{,}001$.

**(d)** UML dùng khối cỡ $\bar m(\epsilon/2)$, $k=\lceil\log_2(1/\delta)\rceil$ khối và mẫu xác thực cỡ $\ln(4k/\delta)/\epsilon^2$. Với các hằng số đó, lập luận của (b) cho cận nào cho $L_D(\hat g)$, và với xác suất thất bại bao nhiêu?
:::

::: hint Gợi ý 1
Phần (a). Xét dấu của $L_D(A(S))-\inf_{\mathcal H}L_D$ khi $A(S)\in\mathcal H$, rồi dùng một bất đẳng thức chỉ cần kì vọng. Phần (b). Chia sai số cho phép $\epsilon$ làm hai nửa: một nửa cho khối tốt nhất, một nửa cho bước chọn trên $V$; chia $\delta$ cũng vậy.
:::

::: hint Gợi ý 2
Phần (a). Bổ đề 02.2 với ngưỡng $\epsilon$. Phần (b). Gọi một khối là hỏng khi $L_D(h_j)-\inf_{\mathcal H}L_D\ge\epsilon/2$; dùng (a) với $\epsilon/2$ và xác suất $\tfrac12$ cho từng khối, rồi tính độc lập giữa các khối. Dùng Hệ quả 04.17(a) với $K=k$ ứng viên và xác suất thất bại $\delta/2$: số hạng $2\sqrt{\ln(4k/\delta)/(2m_v)}$ không quá $\epsilon/2$ khi $m_v\ge8\ln(4k/\delta)/\epsilon^2$.
:::

::: solution Lời giải Bài tập 06.7
**(a) Bất đẳng thức Markov.**

**Bước 1: biến không âm; học đúng lớp.** Đặt $\Gamma_S=L_D(A(S))-\inf_{\mathcal H}L_D$. Vì $A(S)\in\mathcal H$, $L_D(A(S))\ge\inf_{\mathcal H}L_D$, nên $\Gamma_S\ge0$. Đây là chỗ duy nhất cần $A(S)\in\mathcal H$: với một thuật toán học ngoài lớp, $\Gamma_S$ có thể âm và Bổ đề 02.2 không áp dụng.

**Bước 2: kì vọng.** Với $m\ge \bar m(\epsilon\delta)$, giả thiết cho $\mathbb E\Gamma_S\le\epsilon\delta<\infty$.

**Bước 3: Markov.** Bổ đề 02.2 với ngưỡng $\epsilon$ cho
$$
\Pr_S[\Gamma_S\ge\epsilon]\le\frac{\mathbb E\Gamma_S}\epsilon\le\delta .
$$

**(b) Chia khối và xác thực.**

**Bước 1: một khối.** Khối thứ $j$ có $\bar m(\epsilon/4)$ quan sát, nên $\mathbb E[L_D(h_j)-\inf_{\mathcal H}L_D]\le\epsilon/4=\tfrac\epsilon2\cdot\tfrac12$. Phần (a) với độ chính xác $\epsilon/2$ và xác suất $\tfrac12$ cho: khối $j$ hỏng với xác suất không quá $\tfrac12$.

**Bước 2: mọi khối hỏng.** Các khối là các phần rời nhau của một mẫu độc lập cùng phân bố, nên $h_1,\ldots,h_k$ độc lập. Vì $k\ge\log_2(2/\delta)$, xác suất để mọi khối đều hỏng không quá
$$
\Big(\frac12\Big)^k=2^{-k}\le\frac\delta2 .
$$
Gọi $E_1$ là biến cố có ít nhất một khối không hỏng, tức $\min_jL_D(h_j)<\inf_{\mathcal H}L_D+\epsilon/2$; $\Pr(E_1)\ge1-\delta/2$.

**Bước 3: mẫu xác thực.** Các ứng viên $h_1,\ldots,h_k$ chỉ phụ thuộc các khối huấn luyện, còn $V$ độc lập với chúng, nên (T7) đúng; hàm lỗi thỏa (T3). Hệ quả 04.17(a) với $K=k$ và xác suất thất bại $\delta/2$ cho, với xác suất ít nhất $1-\delta/2$,
$$
\begin{aligned}
L_D(\hat g)&\le\min_jL_D(h_j)\\
&\quad+2\sqrt{\frac{\ln(4k/\delta)}{2m_v}}.
\end{aligned}
$$
Với $m_v\ge8\ln(4k/\delta)/\epsilon^2$, số hạng cuối không quá $2\sqrt{\epsilon^2/16}=\epsilon/2$. Gọi biến cố này là $E_2$.

**Bước 4: bất đẳng thức hợp.** $\Pr(E_1^c\cup E_2^c)\le\delta/2+\delta/2=\delta$. Trên $E_1\cap E_2$,
$$
\begin{aligned}
L_D(\hat g)&<\inf_{\mathcal H}L_D+\tfrac\epsilon2+\tfrac\epsilon2\\
&=\inf_{\mathcal H}L_D+\epsilon .
\end{aligned}
$$

**(c) Hồi quy ridge chia $4$.**

**Bước 1: miền giá trị.** Với $\lVert w\rVert\le1$, $\lvert\langle w,x\rangle-y\rvert\le\lVert w\rVert\lVert x\rVert+\lvert y\rvert\le2$, nên $0\le\ell\le\tfrac14\cdot4=1$.

**Bước 2: hằng số Lipschitz.** Gradient $\tfrac12(\langle w,x\rangle-y)x$ có chuẩn không quá $\tfrac12\cdot2\cdot1=1$ trên $W$. Theo Mệnh đề 05.5(a), (L) đúng với $G=1$. Hàm lỗi lồi, nên Hệ quả 06.13(c) với $B=1$ ($W_B=W$) cho mức kì vọng $\epsilon$ khi $m\ge4/\epsilon^2$; ta lấy $\bar m(\epsilon)=\lceil4/\epsilon^2\rceil$. Đầu ra $\hat w_S$ thuộc $W$, nên $A$ học đúng lớp.

**Bước 3: $\delta=0{,}05$.** Theo (a), cần $\bar m(0{,}005)=4/0{,}000025=160\,000$. Theo (b):
$$
\begin{aligned}
&k=\lceil\log_240\rceil=\lceil5{,}32\rceil=6,\\
&\bar m(0{,}025)=4/0{,}000625\\
&\quad=6400,\\
&8\ln(480)/0{,}01\approx4939{,}03,
\end{aligned}
$$
nên $m_v=4940$ và tổng là $6\cdot6400+4940=43\,340$, ít hơn khoảng $3{,}7$ lần.

**Bước 4: $\delta=0{,}001$.** Theo (a), cần $4/(10^{-4})^2=4\cdot10^8$. Theo (b):
$$
\begin{aligned}
&k=\lceil\log_22000\rceil=11,\\
&m_v=\lceil8\ln(44\,000)/0{,}01\rceil\\
&\quad=\lceil8553{,}56\rceil=8554,\\
&11\cdot6400+8554=78\,954 .
\end{aligned}
$$

Bất đẳng thức Markov trả thừa số $1/\delta^2$; cách chia khối chỉ trả thừa số cỡ $\log_2(1/\delta)$.

**(d) Hằng số của UML.**

**Bước 1: các khối.** Với khối cỡ $\bar m(\epsilon/2)$, phần (a) với độ chính xác $\epsilon$ và xác suất $\tfrac12$ cho mỗi khối có $L_D(h_j)-\inf_{\mathcal H}L_D\ge\epsilon$ với xác suất không quá $\tfrac12$. Với $k=\lceil\log_2(1/\delta)\rceil$, xác suất mọi khối như vậy chỉ được chặn bởi $2^{-k}\le\delta$, không phải $\delta/2$.

**Bước 2: mẫu xác thực.** Với $m_v=\ln(4k/\delta)/\epsilon^2$, số hạng của Hệ quả 04.17(a) với xác suất thất bại $\delta/2$ là $2\sqrt{\epsilon^2/2}=\sqrt2\,\epsilon$.

**Bước 3: kết hợp.** Với xác suất ít nhất $1-\delta-\delta/2=1-3\delta/2$, ta có $L_D(\hat g)<\inf_{\mathcal H}L_D+(1+\sqrt2)\epsilon\approx\inf_{\mathcal H}L_D+2{,}414\epsilon$. Các hằng số đã chỉnh ở (b) đưa cả hai số về đúng $\epsilon$ và $\delta$.

**Kiểm tra lại.** Với $\delta=0{,}05$, $k=5$ cho $2^{-5}=0{,}03125>0{,}025=\delta/2$, nên $k=6$ là nhỏ nhất; $2^{-6}\approx0{,}0156\le0{,}025$.
:::

### Bài tập 06.8 (Học được mà không có hội tụ đều; UML Bài tập 13.2)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 3, 4, 5; một bảo đảm cấp thuật toán không phụ thuộc số chiều, trong khi bảo đảm cấp lớp qua hội tụ đều cần cỡ mẫu tăng theo số chiều.

::: exercise Bài tập 06.8
Cho $p\ge1$, $W=\{w\in\mathbb R^p:\lVert w\rVert\le1\}$ và $\mathcal Z=W\times\{0,1\}^p$; một quan sát là $z=(x,\alpha)$. Hàm lỗi
$$
\ell(w,(x,\alpha))=\sum_{j=1}^p\alpha_j(x_j-w_j)^2
$$
là bình phương khoảng cách từ $w$ tới $x$, chỉ tính trên các tọa độ $j$ có $\alpha_j=1$. Lớp giả thuyết là $W$; bài toán là ước lượng một "tâm" của phân bố của $x$ khi một số tọa độ bị tắt.

**(a)** Chứng minh $\ell(\cdot,z)$ lồi, không âm, và (L) đúng với $G=4$. Suy ra từ Hệ quả 06.13(c) rằng ERM có chính quy hóa với $\lambda^*$ ($B=1$) thỏa $\mathbb E_SL_D(\hat w_S)-\inf_WL_D\le8/\sqrt m$ với mọi $D$ trên $\mathcal Z$, nên cỡ mẫu đủ cho mức $\epsilon$ không phụ thuộc $p$.

**(b)** Xét phân bố $D$: $x=0$ chắc chắn, còn $\alpha_1,\ldots,\alpha_p$ độc lập, mỗi $\alpha_j$ nhận $0$ và $1$ với xác suất $\tfrac12$. Tính $L_D(w)$. Chứng minh: nếu có $j$ với $\alpha_j=0$ ở mọi quan sát của $S$ thì $S$ không $\epsilon$-đại diện đối với $(W,\ell,D)$ (Định nghĩa 02.13) với mọi $\epsilon<\tfrac12$. Chứng minh xác suất của biến cố "có $j$ như vậy" bằng $1-(1-2^{-m})^p$ và không nhỏ hơn $1-\exp(-p2^{-m})$. Tính xác suất này với $m=10$ khi $p=1000$ và khi $p=10^4$.

**(c)** Cho $\epsilon<\tfrac12$ và $\delta\in(0,1)$. Chứng minh rằng nếu
$$
m<\log_2\frac{p}{\ln\big(1/(1-\delta)\big)}
$$
thì dưới phân bố của (b), xác suất để $S$ là $\epsilon$-đại diện nhỏ hơn $1-\delta$. Tính ngưỡng với $p=10^4$ và $\delta=0{,}05$. Kết luận gì về cỡ mẫu cần cho hội tụ đều khi $p$ tăng? Kết quả này có mâu thuẫn với Định lý 03.17 không?
:::

::: hint Gợi ý 1
Phần (a). Gradient của $\ell(\cdot,(x,\alpha))$ có tọa độ thứ $j$ là $2\alpha_j(w_j-x_j)$; dùng Mệnh đề 05.5(a). Phần (b). Với $x=0$, $\ell(w,(0,\alpha))=\sum_j\alpha_jw_j^2$; tìm một điểm của $W$ có $L_S=0$ khi một tọa độ bị tắt trên cả mẫu.
:::

::: hint Gợi ý 2
Phần (b). So $L_S(\mathbf e_j)$ với $L_D(\mathbf e_j)$; dùng $1-t\le e^{-t}$ với mọi $t$. Phần (c). Biến cố ở (b) kéo theo $S$ không $\epsilon$-đại diện, nên xác suất $S$ là $\epsilon$-đại diện không quá $(1-2^{-m})^p$.
:::

::: solution Lời giải Bài tập 06.8
**(a) Cận cho ERM có chính quy hóa.**

**Bước 1: lồi, không âm.** Mỗi số hạng $\alpha_j(x_j-w_j)^2$ là hàm lồi, không âm của $w$ vì $\alpha_j\ge0$; tổng của chúng cũng vậy.

**Bước 2: hằng số Lipschitz.** Gradient là véc-tơ có tọa độ $2\alpha_j(w_j-x_j)$. Vì $\alpha_j\in\{0,1\}$, chuẩn của nó không quá $2\lVert w-x\rVert$. Với $w,x\in W$,
$$
2\lVert w-x\rVert\le2(\lVert w\rVert+\lVert x\rVert)\le4 .
$$
Theo Mệnh đề 05.5(a), (L) đúng với $G=4$. Hàm lỗi đo được và $0\le\ell\le\lVert w-x\rVert^2\le4$, nên (T2) đúng và $L_D$ hữu hạn trên $W$.

**Bước 3: Hệ quả 06.13(c).** Với $B=1$, $W_B=W$, $G=4$ và $\lambda^*=8/\sqrt m$,
$$
\begin{aligned}
&\mathbb E_SL_D(\hat w_S)-\inf_WL_D\\
&\quad\le\frac{2\cdot4\cdot1}{\sqrt m}=\frac8{\sqrt m}.
\end{aligned}
$$
Cỡ mẫu $m\ge64/\epsilon^2$ đủ cho mức $\epsilon$, với mọi $p$; chẳng hạn $m\ge6400$ với $\epsilon=0{,}1$.

**(b) Một mẫu không đại diện.**

**Bước 1: rủi ro kì vọng.** Với $x=0$, $\ell(w,(0,\alpha))=\sum_j\alpha_jw_j^2$ và $\mathbb E\alpha_j=\tfrac12$, nên $L_D(w)=\tfrac12\lVert w\rVert^2$.

**Bước 2: mẫu không đại diện.** Giả sử $\alpha_j=0$ ở mọi quan sát của $S$. Véc-tơ đơn vị $\mathbf e_j$ thuộc $W$, và $\ell(\mathbf e_j,(0,\alpha))=\alpha_j=0$ trên mọi quan sát, nên $L_S(\mathbf e_j)=0$. Ngoài ra $L_D(\mathbf e_j)=\tfrac12$. Do đó $\lvert L_S(\mathbf e_j)-L_D(\mathbf e_j)\rvert=\tfrac12>\epsilon$, và $S$ không $\epsilon$-đại diện.

**Bước 3: xác suất.** Với $j$ cố định, xác suất để $\alpha_j=0$ ở cả $m$ quan sát là $2^{-m}$. Các $\alpha_j$ của mọi quan sát độc lập, nên biến cố "không có $j$ nào như vậy" có xác suất $(1-2^{-m})^p$, và biến cố cần tính có xác suất $1-(1-2^{-m})^p$.

**Bước 4: cận dưới.** Vì $1-t\le e^{-t}$, $(1-2^{-m})^p\le\exp(-p2^{-m})$, nên xác suất ở Bước 3 không nhỏ hơn $1-\exp(-p2^{-m})$.

**Bước 5: bằng số với $m=10$.** $2^{-10}=1/1024$.

- **$p=1000$.** $1-(1023/1024)^{1000}\approx0{,}6236$; cận dưới $1-e^{-1000/1024}\approx0{,}6234$.
- **$p=10^4$.** $1-(1023/1024)^{10^4}\approx0{,}9999$.

Với $10$ quan sát, mẫu không $\epsilon$-đại diện với xác suất khoảng $62\%$ khi $p=1000$ và trên $0{,}9999$ khi $p=10^4$.

**(c) Cỡ mẫu cho hội tụ đều.**

**Bước 1: đổi điều kiện.** Điều kiện $m<\log_2\big(p/\ln(1/(1-\delta))\big)$ tương đương $p2^{-m}>\ln\big(1/(1-\delta)\big)$, tức $\exp(-p2^{-m})<1-\delta$.

**Bước 2: xác suất đại diện.** Theo Bước 2 của (b), mẫu chỉ có thể $\epsilon$-đại diện khi không có $j$ nào với $\alpha_j=0$ ở mọi quan sát. Theo Bước 3–4 của (b) và Bước 1, xác suất để $S$ là $\epsilon$-đại diện không quá
$$
\begin{aligned}
(1-2^{-m})^p&\le\exp(-p2^{-m})\\
&<1-\delta .
\end{aligned}
$$

**Bước 3: ngưỡng.** Với $\delta=0{,}05$, $\ln(1/0{,}95)\approx0{,}05129$ và
$$
\begin{aligned}
\log_2\frac{10^4}{0{,}05129}&\approx\log_2194\,957\\
&\approx17{,}57 .
\end{aligned}
$$
Mọi $m\le17$ đều không đủ cho hội tụ đều với $\epsilon<\tfrac12$, $\delta=0{,}05$, trong khi cận ở (a) không thay đổi.

**Bước 4: kết luận.** Cỡ mẫu cần cho hội tụ đều ít nhất bằng $\log_2p-\log_2\ln\big(1/(1-\delta)\big)$, tăng không giới hạn khi $p\to\infty$, còn cận ở (a) không dùng $p$. Vì vậy, với cùng một cỡ mẫu, cận ở (a) đúng cho mọi $p$, còn hội tụ đều hỏng khi $p$ đủ lớn; đó là nghĩa của tên bài.

**Bước 5: so với Định lý 03.17.** Không mâu thuẫn: định lý đó nói về phân lớp nhị phân với hàm lỗi 0–1. Ở đây hàm lỗi khác, và bảo đảm của (a) là cấp thuật toán, cho đầu ra của ERM có chính quy hóa, không cho mọi giả thuyết của lớp.

**Kiểm tra lại.** Với $m=1$ và $p=1$, xác suất ở (b) là $1-(1-\tfrac12)=\tfrac12$, đúng bằng $\Pr(\alpha_1=0)$. Với $p=10^4$, $m=17$ cho $(1-2^{-17})^{10^4}\approx0{,}927<0{,}95$, khớp Bước 3 của (c).
:::

### Bài tập 06.9 (Ổn định thay một theo trung bình và gần đúng ERM theo kì vọng đủ cho học; UML Bài tập 13.3)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 2, 3; ghép đẳng thức của lập luận đổi vai với phân tích rủi ro của Mệnh đề 06.5.

::: exercise Bài tập 06.9
Cho lớp $\mathcal H$, hàm lỗi $\ell$ thỏa (T2), một thuật toán tất định $A$ (đầu ra $A(S)$ không nhất thiết thuộc $\mathcal H$) và hai hàm $\epsilon_1(m)$, $\epsilon_2(m)$. Với $S\sim D^m$ theo (T1), $Z'\sim D$ độc lập với $S$ và $S^{(i)}$ như trong chứng minh Định lý 06.10, ta dùng hai định nghĩa sau.

- **Ổn định thay một theo trung bình.** $A$ là *ổn định thay một theo trung bình* (on-average-replace-one stable) với tốc độ $\epsilon_1(m)$ nếu với mọi $D$,
  $$
  \begin{aligned}
  &\frac1m\sum_{i=1}^m\mathbb E\Big[\\
  &\quad\ell(A(S^{(i)}),Z_i)\\
  &\quad-\ell(A(S),Z_i)\Big]\le\epsilon_1(m)
  \end{aligned}
  $$
  (Phụ lục E của ghi chú).
- **Gần đúng ERM theo kì vọng.** $A$ là *gần đúng ERM theo kì vọng* (asymptotic empirical risk minimizer, AERM) với tốc độ $\epsilon_2(m)$ nếu với mọi $D$,
  $$
  \begin{aligned}
  &\mathbb E_S\Big[L_S(A(S))\\
  &\quad-\inf_{h\in\mathcal H}L_S(h)\Big]\le\epsilon_2(m).
  \end{aligned}
  $$

**(a)** Giả sử thêm: $\mathbb EL_D(A(S))<\infty$, có $h_0\in\mathcal H$ với $L_D(h_0)<\infty$, và $\inf_{\mathcal H}L_S$ đo được theo $S$. Chứng minh rằng với mọi $D$,
$$
\begin{aligned}
&\mathbb E_SL_D(A(S))\\
&\le\inf_{h\in\mathcal H}L_D(h)\\
&\quad+\epsilon_1(m)+\epsilon_2(m).
\end{aligned}
$$
Phát biểu dùng cận dưới đúng, không giả sử có giả thuyết đạt giá trị nhỏ nhất của $L_D$. Chỉ ra chỗ cần dạng đầy đủ của (T1) và chỗ dạng yếu là đủ.

**(b)** Xét ERM có chính quy hóa dưới các giả thiết của Hệ quả 06.13, với lớp $\mathcal H=W_B$ cho một $B>0$. Chứng minh rằng nó ổn định thay một theo trung bình với tốc độ $2G^2/(\lambda m)$ và gần đúng ERM theo kì vọng (đối với $W_B$) với tốc độ $\lambda B^2/2$. Suy ra Hệ quả 06.13(c) từ (a).
:::

::: hint Gợi ý 1
Phần (a). Thêm bớt $L_S(A(S))$ và $\inf_{\mathcal H}L_S$, như trong chứng minh Mệnh đề 06.5; mỗi định nghĩa chặn một số hạng.
:::

::: hint Gợi ý 2
Phần (a). Số hạng $\mathbb E[L_D(A(S))-L_S(A(S))]$ là vế trái của định nghĩa ổn định thay một theo trung bình (đẳng thức ở Phụ lục E). So $\inf_{\mathcal H}L_S$ với $L_S(h)$ cho một $h$ cố định. Trước khi trừ, kiểm $\mathbb EL_S(A(S))<\infty$ từ giả thiết gần đúng ERM và $h_0$. Phần (b). Bước 1 của chứng minh Hệ quả 06.13 cho $L_S(\hat w_S)\le L_S(u)+\tfrac\lambda2\lVert u\rVert^2$ với mọi $u\in W$.
:::

::: solution Lời giải Bài tập 06.9
**(a) Tốc độ học $\epsilon_1+\epsilon_2$.**

**Bước 1: số hạng cuối; dạng yếu của (T1).** Với mỗi $h\in\mathcal H$ cố định, $\inf_{\mathcal H}L_S\le L_S(h)$ trên mọi mẫu. Lấy kì vọng; theo Mệnh đề 01.7, chỉ cần mỗi $Z_i$ có phân bố $D$:
$$
\begin{aligned}
0&\le\mathbb E\inf_{\mathcal H}L_S\\
&\le\mathbb EL_S(h)=L_D(h).
\end{aligned}
$$
Lấy cận dưới đúng theo $h\in\mathcal H$: $\mathbb E\inf_{\mathcal H}L_S\le\inf_{\mathcal H}L_D$. Với $h=h_0$, số này hữu hạn.

**Bước 2: rủi ro thực nghiệm khả tích.** Theo giả thiết gần đúng ERM và Bước 1,
$$
\begin{aligned}
&\mathbb EL_S(A(S))\\
&\le\epsilon_2(m)+\mathbb E\inf_{\mathcal H}L_S\\
&\le\epsilon_2(m)+\inf_{\mathcal H}L_D<\infty .
\end{aligned}
$$

**Bước 3: khoảng cách tổng quát hóa; dạng đầy đủ của (T1).** Hai kì vọng $\mathbb EL_D(A(S))$ và $\mathbb EL_S(A(S))$ hữu hạn. Theo các đẳng thức ở Bước 1–3 của chứng minh Định lý 06.10 (Phụ lục E, mục Đẳng thức), khoảng cách tổng quát hóa kì vọng bằng vế trái của định nghĩa ổn định thay một theo trung bình. Do đó
$$
\begin{aligned}
&\mathbb E\big[L_D(A(S))\\
&\quad-L_S(A(S))\big]\le\epsilon_1(m).
\end{aligned}
$$
Phép đổi vai $Z_i\leftrightarrow Z'$ ở đây cần dạng đầy đủ của (T1).

**Bước 4: cộng.** Viết $\mathbb EL_D(A(S))=\mathbb E[L_D(A(S))-L_S(A(S))]+\mathbb EL_S(A(S))$ và dùng Bước 3, Bước 2:
$$
\begin{aligned}
\mathbb EL_D(A(S))&\le\epsilon_1(m)+\epsilon_2(m)\\
&\quad+\inf_{\mathcal H}L_D .
\end{aligned}
$$

**Bước 5: hai giả thiết không cần.** Bước 1 lấy cận dưới đúng theo mọi $h$, nên không cần $h$ đạt $\inf_{\mathcal H}L_D$ và không cần $A(S)\in\mathcal H$.

**(b) ERM có chính quy hóa.**

**Bước 1: ổn định.** Theo Mệnh đề 06.11(b), ERM có chính quy hóa ổn định đều với $\epsilon_{\mathrm{stab}}(m)=2G^2/(\lambda m)$. Mỗi hiệu trong tổng của định nghĩa ổn định thay một theo trung bình có trị tuyệt đối không quá $\epsilon_{\mathrm{stab}}(m)$ (Phụ lục E, mục So với ổn định đều), nên $\epsilon_1(m)=2G^2/(\lambda m)$, với mọi $D$.

**Bước 2: gần đúng ERM.** Với mọi $u\in W_B$, Bước 1 của chứng minh Hệ quả 06.13 cho
$$
\begin{aligned}
L_S(\hat w_S)&\le L_S(u)+\tfrac\lambda2\lVert u\rVert^2\\
&\le L_S(u)+\tfrac\lambda2B^2 .
\end{aligned}
$$
Lấy cận dưới đúng theo $u\in W_B$: $L_S(\hat w_S)-\inf_{W_B}L_S\le\lambda B^2/2$ trên mọi mẫu, nên $\epsilon_2(m)=\lambda B^2/2$.

**Bước 3: giả thiết phụ.** $\mathbb EL_D(\hat w_S)<\infty$ theo Phụ lục C, Bước 3; mọi $h_0\in W_B$ có $L_D(h_0)<\infty$; $\inf_{W_B}L_S$ đo được vì $L_S$ liên tục nên cận dưới đúng có thể lấy trên một tập con đếm được trù mật của $W_B$.

**Bước 4: Hệ quả 06.13(c).** Theo (a),
$$
\begin{aligned}
&\mathbb E_SL_D(\hat w_S)-\inf_{W_B}L_D\\
&\quad\le\frac{2G^2}{\lambda m}+\frac{\lambda B^2}2 .
\end{aligned}
$$
Với $\lambda=\lambda^*$, hai số hạng đều bằng $GB/\sqrt m$ (Phụ lục C, Bước 4), và tổng là $2GB/\sqrt m$. Đầu ra $\hat w_S$ có thể nằm ngoài $W_B$; (a) không cần $A(S)\in\mathcal H$.

**Kiểm tra lại.** Lập luận của (a) vẫn đúng với thuật toán có nguồn ngẫu nhiên riêng, vì Bước 1–3 của chứng minh Định lý 06.10 đã có $\xi$. Với chương trình thứ hai của Ví dụ 06.3, trung bình thay một (bằng khoảng cách tổng quát hóa kì vọng) là $0{,}4750$ và kì vọng của sai số tối ưu thực nghiệm là $0{,}0011$; tổng $0{,}4761$ chặn rủi ro vượt mức kì vọng $0{,}2261$, khớp Bước 5 của ví dụ đó.
:::

### Bài tập 06.10 (Dạng bậc nhất của tính lồi mạnh; UML Bài tập 14.1)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 4; cùng kĩ thuật với Bổ đề 06.7, ở dạng có dưới gradient.

::: exercise Bài tập 06.10
Cho $f:\mathbb R^p\to\mathbb R$ là $\lambda$-lồi mạnh (Định nghĩa 05.6), $w\in\mathbb R^p$ và $v\in\partial f(w)$ (Định nghĩa 05.2).

**(a)** Chứng minh rằng với mọi $u\in\mathbb R^p$,
$$
\begin{aligned}
\langle w-u,v\rangle&\ge f(w)-f(u)\\
&\quad+\tfrac\lambda2\lVert w-u\rVert^2 .
\end{aligned}
$$

**(b)** Suy ra hai hệ quả: nếu $0\in\partial f(w^*)$ thì $f(w)-f(w^*)\ge\tfrac\lambda2\lVert w-w^*\rVert^2$ với mọi $w$ (Bổ đề 06.7 với $W=\mathbb R^p$); và với $v\in\partial f(w)$, $v'\in\partial f(u)$,
$$
\langle v-v',w-u\rangle\ge\lambda\lVert w-u\rVert^2 .
$$

**(c)** Kiểm tra (a) bằng số với $f(w)=w^2$ ($\lambda=2$) tại $w=1$, $u=0$; và với $f(w)=\lvert w\rvert+w^2$ ($\lambda=2$) tại $w=0$, $v=\tfrac12$, $u=1$.
:::

::: hint Gợi ý 1
Như chứng minh Bổ đề 06.7: xét điểm $w+\alpha(u-w)$ với $\alpha\in(0,1]$, chặn $f$ tại đó từ trên bằng tính lồi mạnh và từ dưới bằng bất đẳng thức dưới gradient tại $w$.
:::

::: hint Gợi ý 2
Chia cho $\alpha>0$ trước khi cho $\alpha\to0^+$. Phần (b). Viết (a) cho cặp $(w,v)$ và cho cặp $(u,v')$ rồi cộng.
:::

::: solution Lời giải Bài tập 06.10
**(a) Dạng bậc nhất.**

**Bước 1: chặn trên.** Với $\alpha\in(0,1]$, đặt $w_\alpha=w+\alpha(u-w)=\alpha u+(1-\alpha)w$. Định nghĩa 05.6 với cặp $(u,w)$ và trọng số $\alpha$ cho
$$
\begin{aligned}
&f(w_\alpha)\le\alpha f(u)+(1-\alpha)f(w)\\
&\quad-\tfrac\lambda2\alpha(1-\alpha)\lVert u-w\rVert^2 .
\end{aligned}
$$

**Bước 2: chặn dưới.** Bất đẳng thức dưới gradient tại $w$ với điểm $w_\alpha$:
$$
f(w_\alpha)\ge f(w)+\alpha\langle v,u-w\rangle .
$$

**Bước 3: ghép và chia.** Ghép Bước 1, Bước 2, trừ $f(w)$ ở hai vế và chia cho $\alpha>0$:
$$
\begin{aligned}
&\langle v,u-w\rangle\le f(u)-f(w)\\
&\quad-\tfrac\lambda2(1-\alpha)\lVert u-w\rVert^2 .
\end{aligned}
$$

**Bước 4: giới hạn.** Cho $\alpha\to0^+$: $\langle v,u-w\rangle\le f(u)-f(w)-\tfrac\lambda2\lVert u-w\rVert^2$. Đổi dấu hai vế, ta được bất đẳng thức cần chứng minh.

**(b) Hai hệ quả.**

**Bước 1: tăng trưởng bậc hai.** Áp dụng (a) tại $w^*$ với dưới gradient $0$ và điểm so sánh $w$: $0\ge f(w^*)-f(w)+\tfrac\lambda2\lVert w^*-w\rVert^2$. Theo Định nghĩa 05.2, $0\in\partial f(w^*)$ khi và chỉ khi $w^*$ là điểm cực tiểu của $f$ trên $\mathbb R^p$; đây là Bổ đề 06.7 với $W=\mathbb R^p$.

**Bước 2: hai bất đẳng thức.** (a) cho cặp $(w,v)$ với điểm $u$, và cho cặp $(u,v')$ với điểm $w$:
$$
\begin{aligned}
&\langle w-u,v\rangle\ge f(w)-f(u)\\
&\quad+\tfrac\lambda2\lVert w-u\rVert^2,\\
&\langle u-w,v'\rangle\ge f(u)-f(w)\\
&\quad+\tfrac\lambda2\lVert w-u\rVert^2 .
\end{aligned}
$$

**Bước 3: cộng.** Các giá trị hàm triệt tiêu, còn $\langle v-v',w-u\rangle\ge\lambda\lVert w-u\rVert^2$.

**(c) Bằng số.**

**Bước 1: $f(w)=w^2$.** Hàm này thỏa Định nghĩa 05.6 với $\lambda=2$ và dấu bằng (đẳng thức ở Kiến thức tiên quyết). Tại $w=1$, $v=f'(1)=2$; với $u=0$, vế trái là $(1-0)\cdot2=2$, vế phải là $1-0+\tfrac22\cdot1=2$. Dấu bằng xảy ra.

**Bước 2: $f(w)=\lvert w\rvert+w^2$.** Hàm này là tổng của hàm lồi $\lvert w\rvert$ và hàm $2$-lồi mạnh $w^2$, nên $2$-lồi mạnh (Bước 1 của chứng minh Bổ đề 06.8). Tại $w=0$, $\partial f(0)=[-1,1]\ni\tfrac12$. Với $u=1$, vế trái là $(0-1)\cdot\tfrac12=-\tfrac12$ và vế phải là $0-2+1=-1$, nên $-\tfrac12\ge-1$.

**Kiểm tra lại.** Với $f(w)=w^2$, $v=2w$ và $v'=2u$, bất đẳng thức của (b) thành $2(w-u)^2\ge2(w-u)^2$, dấu bằng.
:::

### Bài tập 06.11 (Tùy chọn: lồi mạnh theo chuẩn bất kì; UML Bài tập 13.4, ý 1–3)

**Mức độ:** chứng minh. **Mục tiêu:** phần mở rộng của §6 và §8; chỗ các chứng minh dùng chuẩn Euclid và chỗ không dùng.

::: exercise Bài tập 06.11
Cho $\lVert\cdot\rVert$ là một chuẩn bất kì trên $\mathbb R^p$, không nhất thiết là chuẩn Euclid. Hàm $f:\mathbb R^p\to\mathbb R$ là *$\lambda$-lồi mạnh theo $\lVert\cdot\rVert$* nếu bất đẳng thức của Định nghĩa 05.6 đúng khi thay chuẩn Euclid bằng $\lVert\cdot\rVert$.

**(a)** Chứng minh hai khẳng định với mọi chuẩn: (i) nếu $f$ là $\lambda$-lồi mạnh theo $\lVert\cdot\rVert$ và $g$ lồi thì $f+g$ là $\lambda$-lồi mạnh theo $\lVert\cdot\rVert$; (ii) Bổ đề 06.7 đúng khi tính lồi mạnh và khoảng cách đều lấy theo $\lVert\cdot\rVert$. Chỉ ra bước nào của §6 cần chuẩn Euclid.

**(b)** Với chuẩn $\lVert w\rVert_\infty=\max\{\lvert w_1\rvert,\lvert w_2\rvert\}$ trên $\mathbb R^2$, chứng minh $f(w)=\tfrac12\lVert w\rVert_\infty^2$ không $\mu$-lồi mạnh theo $\lVert\cdot\rVert_\infty$ với mọi $\mu>0$.

**(c)** Cho hàm chính quy hóa $\Omega:\mathbb R^p\to\mathbb R$ là $\lambda$-lồi mạnh theo $\lVert\cdot\rVert$, và hàm lỗi với $\ell(\cdot,z)$ lồi và $G$-Lipschitz theo cùng chuẩn, tức $\lvert\ell(w,z)-\ell(w',z)\rvert\le G\lVert w-w'\rVert$ với mọi $w,w',z$. Quy tắc $A$ trả về điểm nhỏ nhất của $L_s+\Omega$ trên $\mathbb R^p$ (giả sử điểm này tồn tại). Chứng minh $\lVert A(s)-A(s^{(i)})\rVert\le2G/(\lambda m)$ và $A$ ổn định đều với hệ số $2G^2/(\lambda m)$. So với tốc độ $2\rho^2/(\lambda_{\mathrm{UML}}m)$ mà UML nêu khi $\Omega$ là $2\lambda_{\mathrm{UML}}$-lồi mạnh.
:::

::: hint Gợi ý 1
Phần (a). Chứng minh của Bổ đề 06.7 chỉ dùng bất đẳng thức trong định nghĩa và tính lồi của $W$. Phần (b). Xét đoạn nối $(1,1)$ và $(1,-1)$.
:::

::: hint Gợi ý 2
Phần (c). Làm lại Bước 1–4 của chứng minh Mệnh đề 06.11 với $L_s+\Omega$ thay cho $F_{s,\lambda}$; số hạng $\Omega$ triệt tiêu như số hạng chính quy hóa.
:::

::: solution Lời giải Bài tập 06.11
**(a) Hai khẳng định với mọi chuẩn.**

**Bước 1: tổng.** Với $w,u$ và $\alpha\in[0,1]$, cộng bất đẳng thức lồi mạnh của $f$ với bất đẳng thức lồi của $g$:
$$
\begin{aligned}
&(f+g)(\alpha w+(1-\alpha)u)\\
&\le\alpha(f+g)(w)\\
&\quad+(1-\alpha)(f+g)(u)\\
&\quad-\tfrac\lambda2\alpha(1-\alpha)\lVert w-u\rVert^2 .
\end{aligned}
$$
Chuẩn chỉ xuất hiện qua số $\lVert w-u\rVert$, nên lập luận không phụ thuộc chuẩn.

**Bước 2: Bổ đề 06.7.** Chứng minh của Bổ đề 06.7 dùng tính lồi của $W$, tính cực tiểu của $u$ và bất đẳng thức của định nghĩa, rồi chia cho $\alpha$ và lấy giới hạn. Không bước nào dùng tích vô hướng, nên bổ đề đúng với $\lVert\cdot\rVert$.

**Bước 3: bước cần chuẩn Euclid.** Bước 1 của chứng minh Bổ đề 06.8 dùng đẳng thức của $\lVert\alpha a+(1-\alpha)a'\rVert^2$ (Kiến thức tiên quyết), chỉ đúng với chuẩn sinh từ một tích vô hướng; (b) cho thấy $\tfrac12\lVert\cdot\rVert^2$ có thể không lồi mạnh theo chuẩn khác.

**(b) Chuẩn $\ell_\infty$.**

**Bước 1: một đoạn thẳng.** Lấy $w=(1,1)$, $u=(1,-1)$. Mọi điểm $(1,t)$ với $t\in[-1,1]$ của đoạn nối hai điểm có $\lVert(1,t)\rVert_\infty=1$, nên $f=\tfrac12$ trên cả đoạn. Ngoài ra $\lVert w-u\rVert_\infty=\lVert(0,2)\rVert_\infty=2$.

**Bước 2: vi phạm định nghĩa.** Với $\alpha=\tfrac12$, tính $\mu$-lồi mạnh đòi hỏi
$$
\begin{aligned}
\tfrac12&\le\tfrac12\cdot\tfrac12+\tfrac12\cdot\tfrac12-\tfrac\mu2\cdot\tfrac14\cdot4\\
&=\tfrac12-\tfrac\mu2,
\end{aligned}
$$
sai với mọi $\mu>0$. Hàm $f$ lồi nhưng hằng trên một đoạn thẳng, nên không có độ cong dương theo phương đó. Với chuẩn $\ell_1$, đoạn nối $\mathbf e_1$ và $\mathbf e_2$ cho cùng hiện tượng.

**(c) Tính ổn định theo chuẩn bất kì.**

**Bước 1: lồi mạnh và nghiệm duy nhất.** $L_s$ lồi, nên theo (a)(i), $F=L_s+\Omega$ là $\lambda$-lồi mạnh theo $\lVert\cdot\rVert$. Theo (a)(ii) với $W=\mathbb R^p$, điểm nhỏ nhất $\hat w=A(s)$ thỏa $F(w)-F(\hat w)\ge\tfrac\lambda2\lVert w-\hat w\rVert^2$; điểm nhỏ nhất là duy nhất như Bước 3 của chứng minh Bổ đề 06.8.

**Bước 2: cộng hai bất đẳng thức.** Đặt $\hat w'=A(s^{(i)})$ và $F'=L_{s^{(i)}}+\Omega$. Như Bước 1–2 của chứng minh Mệnh đề 06.11, cộng hai bất đẳng thức tăng trưởng; $F-F'=\tfrac1m[\ell(\cdot,z_i)-\ell(\cdot,z')]$ vì $\Omega$ triệt tiêu:
$$
\begin{aligned}
&\lambda\lVert\hat w-\hat w'\rVert^2\\
&\le\tfrac1m\big[\ell(\hat w',z_i)-\ell(\hat w,z_i)\big]\\
&\quad+\tfrac1m\big[\ell(\hat w,z')-\ell(\hat w',z')\big].
\end{aligned}
$$

**Bước 3: Lipschitz theo $\lVert\cdot\rVert$.** Mỗi ngoặc vuông không quá $G\lVert\hat w-\hat w'\rVert$, nên $\lVert\hat w-\hat w'\rVert\le2G/(\lambda m)$. Với mọi $z$, $\lvert\ell(\hat w,z)-\ell(\hat w',z)\rvert\le G\lVert\hat w-\hat w'\rVert\le2G^2/(\lambda m)$.

**Bước 4: so với UML.** Với $\Omega$ là $2\lambda_{\mathrm{UML}}$-lồi mạnh, $\lambda=2\lambda_{\mathrm{UML}}$ và hệ số ở Bước 3 là $G^2/(\lambda_{\mathrm{UML}}m)$, một nửa tốc độ $2\rho^2/(\lambda_{\mathrm{UML}}m)$ với $\rho=G$. Lập luận một phía của Bài tập 06.3(b) cho đúng tốc độ của UML (Phụ lục E, mục Hằng số).

**Kiểm tra lại.** Với chuẩn Euclid và $\Omega=\tfrac\lambda2\lVert\cdot\rVert^2$, (c) cho lại Mệnh đề 06.11 với $W=\mathbb R^p$.
:::
