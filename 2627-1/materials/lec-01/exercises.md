# Bài tập Bài 01 — Mô hình học: rủi ro, tối thiểu hóa rủi ro thực nghiệm và học PAC

Các bài tập dưới đây đi kèm ghi chú Bài 01 và dẫn định nghĩa, mệnh đề, ví dụ theo số hiệu của ghi chú. Kí hiệu theo bảng kí hiệu chung của học phần, §2 của ghi chú và các định nghĩa của ghi chú; $h_t(x)=\mathbb 1[x\ge t]$ là hàm ngưỡng. Hai chữ viết tắt theo ghi chú: tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM) và học xấp xỉ với xác suất cao (probably approximately correct, PAC). Hàm lỗi là hàm lỗi 0–1 khi không ghi rõ, $\ln$ là logarit tự nhiên và $\mathbb N=\{1,2,\ldots\}$. Năm bài đầu là bài gốc của học phần; sáu bài sau chọn từ mục bài tập §2.4 và §3.5 của UML, phát biểu lại theo kí hiệu của học phần.

## Bài tập gốc

### Bài tập 01.1 (Thiết lập bài toán học cho lọc thư rác và dự báo nhiệt độ)

**Mức độ:** khái niệm. **Mục tiêu:** mục tiêu học tập 1; phân biệt hàm dự đoán với hàm lỗi.

::: exercise Bài tập 01.1
Xét hai bài toán.

*Lọc thư rác* (spam filtering). Mỗi thư điện tử được mô tả bằng véc-tơ $x\in\{0,1\}^p$, trong đó $x_j=1$ khi từ thứ $j$ của một từ điển $p$ từ có mặt trong thư. Nhãn $y=1$ nếu thư là thư rác; hàm phân lớp báo $1$ nghĩa là chặn thư. Chặn nhầm một thư thường có chi phí $4$, để lọt một thư rác có chi phí $1$.

*Dự báo nhiệt độ.* Từ $p$ chỉ số đo hôm nay tại một trạm khí tượng, cần dự báo nhiệt độ ngày mai tại trạm đó, tính bằng độ C.

**(a)** Với mỗi bài toán, nêu tám thành phần của §1 trong ghi chú. Đó là tập đầu vào $\mathcal X$ và tập nhãn $\mathcal Y$; phân bố $D$; mẫu $S$; một lớp giả thuyết $\mathcal H$ hợp lý; hàm lỗi $\ell$ cùng miền giá trị; một thuật toán học $A$; mục tiêu và đối tượng so sánh; tài nguyên. Chỉ ra thành phần nào là giả thiết của người lập mô hình, không suy ra được từ mô tả bài toán.

**(b)** Xếp các đại lượng $\ell(h,z)$ với $h$, $z$ cho trước, $L_D(h)$, $L_S(h)$, $A(S)$, $L_D(A(S))$ và $\inf_{h\in\mathcal H}L_D(h)$ vào hai loại của bảng ở §1: cố định và ngẫu nhiên theo $S$.

**(c)** Một học viên viết cho bài toán lọc thư rác: "hàm lỗi là $h(x)=\mathbb 1[\langle w,x\rangle\ge b]$". Chỉ ra chỗ nhầm và viết đúng vai trò của $h$ và của $\ell$.

**(d)** Với chi phí đã cho, xác định ngưỡng trên $\eta(x)=\Pr(Y=1\mid X=x)$ mà quy tắc Bayes dưới hàm lỗi có trọng số $\ell_c$ dùng để chặn thư. Giải thích vì sao không nên giả sử $(D,\mathcal H)$ khả thực trong bài toán lọc thư rác.
:::

::: hint Gợi ý 1
Phần (a). Với mỗi thành phần, xác định ai chọn nó (tự nhiên, người lập mô hình hay thuật toán) và nó được chọn trước hay sau khi thấy mẫu.
:::

::: hint Gợi ý 2
Phần (c). Hàm dự đoán nhận một đầu vào $x$ và trả về một nhãn. Hàm lỗi nhận một hàm dự đoán và một quan sát $(x,y)$, rồi trả về một số không âm.
:::

::: hint Gợi ý 3
Phần (d). Dùng Mệnh đề 01.23(b). Ở đây dương tính giả là chặn một thư thường ($h(x)=1$, $y=0$).
:::

::: solution Lời giải Bài tập 01.1
**(a)** Bảng dưới nêu tám thành phần; dấu (gt) đánh dấu giả thiết của người lập mô hình.

| Thành phần | Lọc thư rác | Dự báo nhiệt độ |
|---|---|---|
| $\mathcal X$, $\mathcal Y$ | $\{0,1\}^p$, $\{0,1\}$ | $\mathbb R^p$, $\mathbb R$ |
| $D$ | phân bố đồng thời, chưa biết, của (véc-tơ từ, nhãn) | phân bố chưa biết trên $\mathbb R^p\times\mathbb R$; (gt) $\mathbb E\lVert X\rVert^2<\infty$, $\mathbb EY^2<\infty$ |
| $S$ | $m$ thư đã gán nhãn; (gt) độc lập cùng phân bố | $m$ cặp (chỉ số ngày $i$, nhiệt độ ngày $i+1$); (gt) độc lập cùng phân bố |
| $\mathcal H$ | (gt) hàm phân lớp tuyến tính (linear classifier) $x\mapsto\mathbb 1[\langle w,x\rangle\ge b]$ | (gt) $\{x\mapsto\langle w,x\rangle:\ w\in\mathbb R^p\}$ của Ví dụ 01.3 |
| $\ell$, miền giá trị | (gt) $\ell_c$ với $c_{FP}=4$, $c_{FN}=1$; $\{0,1,4\}$ | (gt) hàm lỗi bình phương; $[0,\infty)$ |
| $A$ | ERM dưới $\ell_c$ trên $\mathcal H$, với một quy tắc chọn khi bằng nhau cố định | ERM dưới hàm lỗi bình phương (bình phương tối thiểu, least squares) |
| Mục tiêu, đối tượng so sánh | $L^c_D(A(S))$ nhỏ; $\inf_{h\in\mathcal H}L^c_D(h)$, rồi rủi ro Bayes dưới $\ell_c$ | $L_D(A(S))$ nhỏ; $\inf_wL_D(h_w)$ |
| Tài nguyên | cỡ mẫu $m$ | cỡ mẫu $m$ |

Với dự báo nhiệt độ, giả thiết độc lập khó biện minh: hai ngày liên tiếp phụ thuộc nhau và phân bố đổi theo mùa. Hàm lỗi bình phương không bị chặn; nhờ điều kiện mô-men, $D$ là phân bố có rủi ro hữu hạn trên $\mathcal H$ (Ví dụ 01.3, Định nghĩa 01.3).

**(b)** Cố định: $\ell(h,z)$, $L_D(h)$ và $\inf_{h\in\mathcal H}L_D(h)$, vì chỉ phụ thuộc $D$, $\mathcal H$, $\ell$. Ngẫu nhiên theo $S$: $L_S(h)$, $A(S)$ và $L_D(A(S))$.

**(c)** Công thức đã viết là một giả thuyết $h_{w,b}\in\mathcal H$, tức một hàm dự đoán $\mathcal X\to\{0,1\}$. Hàm lỗi là ánh xạ $\ell:\mathcal H\times\mathcal Z\to[0,\infty)$ so dự đoán $h(x)$ với nhãn thật $y$, ở đây $\ell_c(h,(x,y))=4\cdot\mathbb 1[y=0,h(x)=1]+\mathbb 1[y=1,h(x)=0]$.

**(d)** Theo Mệnh đề 01.23(b), quy tắc Bayes dưới $\ell_c$ chặn thư có đầu vào $x$ khi và chỉ khi
$$
\eta(x)\ge\frac{c_{FP}}{c_{FP}+c_{FN}}=\frac45 .
$$
Hai thư có cùng tập từ có thể có nhãn khác nhau, một thư là thư rác và thư kia không, nên có thể $\eta(x)\in(0,1)$ trên một tập có xác suất dương. Khi đó rủi ro Bayes dương (Phụ lục B, đoạn "Rủi ro Bayes") và không lớp nào có một hàm rủi ro $0$. Mô hình phù hợp là học PAC bất khả tri (Định nghĩa 01.25).

**Kiểm tra lại.** Ứng dụng sàng lọc của ghi chú có $(c_{FP},c_{FN})=(1,4)$ và ngưỡng $\tfrac15$; ở đây $(4,1)$ cho ngưỡng $\tfrac45$, tức ngưỡng tăng theo $c_{FP}$. Một lỗi thường gặp là đưa $\eta$ vào thuật toán: thuật toán chỉ thấy $S$.
:::

### Bài tập 01.2 (Hai nghiệm ERM, quy tắc Bayes và rủi ro vượt mức)

**Mức độ:** tính toán. **Mục tiêu:** mục tiêu học tập 2; tập nghiệm ERM và quy tắc chọn khi bằng nhau.

::: exercise Bài tập 01.2
Cho $\mathcal X=\{1,\ldots,6\}$, $\mathcal Y=\{0,1\}$ và phân bố $D$ cho bởi bảng sau (giá trị dựng để luyện tập):

| $x$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ |
|---|---|---|---|---|---|---|
| $D_{\mathcal X}(x)$ | $0{,}1$ | $0{,}2$ | $0{,}2$ | $0{,}2$ | $0{,}2$ | $0{,}1$ |
| $\eta(x)$ | $0$ | $\tfrac15$ | $\tfrac25$ | $\tfrac35$ | $\tfrac9{10}$ | $\tfrac7{10}$ |

Lớp giả thuyết là $\mathcal H=\{h_t:\ t=1,\ldots,7\}$. Thuật toán $A_{\min}$ (hoặc $A_{\max}$) trả về $h_t$ với $t$ nhỏ nhất (hoặc lớn nhất) trong tập nghiệm ERM. Một mẫu cỡ $m=7$ đã được quan sát:
$$
\begin{aligned}
S=\big(&(1,0),(2,0),(3,1),(4,0),\\
&(4,1),(5,0),(6,1)\big).
\end{aligned}
$$

**(a)** Tính $L_S(h_t)$ với $t=1,\ldots,7$, tập nghiệm ERM, $A_{\min}(S)$ và $A_{\max}(S)$.

**(b)** Tính $L_D(h_t)$ với $t=1,\ldots,7$, hàm phân lớp tối ưu Bayes $h_{\mathrm{Bayes}}$ và rủi ro Bayes $L_D^{\mathrm{Bayes}}$. Tính rủi ro vượt mức của $A_{\min}(S)$ và $A_{\max}(S)$ so với $\mathcal H$ và so với rủi ro Bayes.

**(c)** Xét hàm lỗi có trọng số $\ell_c$ với $(c_{FP},c_{FN})=(3,1)$. Xác định ngưỡng của quy tắc Bayes, quy tắc Bayes dưới $\ell_c$ và rủi ro Bayes dưới $\ell_c$; quy tắc này có thuộc $\mathcal H$ không? Tính $\min_tL^c_D(h_t)$ và nghiệm ERM dưới $\ell_c$ trên $S$. Tính rủi ro vượt mức của nghiệm đó so với $\mathcal H$ và so với rủi ro Bayes, rồi kiểm tra đẳng thức
$$
\begin{aligned}
&L_D(h)-L_D^{\mathrm{Bayes}}\\
&\quad=\Big[L_D(h)-\inf_{h'\in\mathcal H}L_D(h')\Big]\\
&\qquad+\Big[\inf_{h'\in\mathcal H}L_D(h')-L_D^{\mathrm{Bayes}}\Big]
\end{aligned}
$$
của §7, với $L$ là rủi ro dưới $\ell_c$.

**(d)** Trên tập đầu vào $\mathbb R$, với lớp $\{h_t:\ t\in\mathbb R\}$ và mẫu
$$
\begin{aligned}
S'=\big(&(0{,}3;\,0),(1{,}1;\,1),\\
&(1{,}8;\,0),(2{,}5;\,1),\\
&(3{,}4;\,1)\big),
\end{aligned}
$$
tính $L_{S'}(h_t)$ như một hàm của $t$ và tập nghiệm ERM. Giải thích vì sao trên $S'$ quy tắc "chọn ngưỡng nhỏ nhất trong tập nghiệm ERM" không chọn được hàm nào, còn quy tắc "chọn ngưỡng lớn nhất" chọn được. Quy tắc sau có xác định một thuật toán trên mọi mẫu không?
:::

::: hint Gợi ý 1
Phần (a). Dùng Thuật toán 01.13: đếm $c_0(x)$, $c_1(x)$, rồi cập nhật $E(t+1)=E(t)-c_0(t)+c_1(t)$.
:::

::: hint Gợi ý 2
Phần (b). Hàm $h_t$ sai tại $x<t$ khi $Y=1$ và tại $x\ge t$ khi $Y=0$; tính khối lượng nhãn 1 và nhãn 0 tại từng mức. Với rủi ro Bayes, xem đoạn "Trường hợp $\mathcal X$ rời rạc" ở Phụ lục B.
:::

::: hint Gợi ý 3
Phần (c). Ngưỡng là $\tfrac34$; so sánh $\eta(5)=\tfrac9{10}$ với $\eta(6)=\tfrac7{10}$.
:::

::: solution Lời giải Bài tập 01.2
**(a)** Các số đếm tại $x=1,\ldots,6$ là $c_0=(1,1,0,1,1,0)$ và $c_1=(0,0,1,1,0,1)$. Theo Thuật toán 01.13, $E(1)=\sum_xc_0(x)=4$, và các cập nhật cho

| $t$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ | $7$ |
|---|---|---|---|---|---|---|---|
| $E(t)$ | $4$ | $3$ | $2$ | $3$ | $3$ | $2$ | $3$ |
| $L_S(h_t)$ | $\tfrac47$ | $\tfrac37$ | $\tfrac27$ | $\tfrac37$ | $\tfrac37$ | $\tfrac27$ | $\tfrac37$ |

Tập nghiệm ERM là $\{h_3,h_6\}$, nên $A_{\min}(S)=h_3$ và $A_{\max}(S)=h_6$.

**(b)** Đặt $a(x)=D_{\mathcal X}(x)\,\eta(x)$ và $b(x)=D_{\mathcal X}(x)\,(1-\eta(x))$, khối lượng nhãn 1 và nhãn 0 tại $x$; khi đó $L_D(h_t)=\sum_{x<t}a(x)+\sum_{x\ge t}b(x)$:

| $x$ hoặc $t$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ | $7$ |
|---|---|---|---|---|---|---|---|
| $a(x)$ | $0$ | $0{,}04$ | $0{,}08$ | $0{,}12$ | $0{,}18$ | $0{,}07$ | |
| $b(x)$ | $0{,}1$ | $0{,}16$ | $0{,}12$ | $0{,}08$ | $0{,}02$ | $0{,}03$ | |
| $L_D(h_t)$ | $0{,}51$ | $0{,}41$ | $0{,}29$ | $\mathbf{0{,}25}$ | $0{,}29$ | $0{,}45$ | $0{,}49$ |

Theo Mệnh đề 01.23(a), $h_{\mathrm{Bayes}}(x)=\mathbb 1[\eta(x)\ge\tfrac12]$. Bất đẳng thức $\eta(x)\ge\tfrac12$ chỉ đúng tại $x=4,5,6$, nên $h_{\mathrm{Bayes}}=h_4\in\mathcal H$ và
$$
\begin{aligned}
&L_D^{\mathrm{Bayes}}=\sum_x\min\{a(x),b(x)\}\\
&\quad=0+0{,}04+0{,}08\\
&\qquad+0{,}08+0{,}02+0{,}03\\
&\quad=0{,}25=\min_tL_D(h_t).
\end{aligned}
$$
Hai loại rủi ro vượt mức trùng nhau: $0{,}29-0{,}25=0{,}04$ cho $A_{\min}(S)=h_3$ và $0{,}45-0{,}25=0{,}20$ cho $A_{\max}(S)=h_6$.

**(c)** Theo Mệnh đề 01.23(b), ngưỡng là $c_{FP}/(c_{FP}+c_{FN})=\tfrac34$. Chỉ $\eta(5)=\tfrac9{10}$ đạt ngưỡng, còn $\eta(6)=\tfrac7{10}<\tfrac34$. Quy tắc Bayes dưới $\ell_c$ là $\mathbb 1[x=5]$, không là hàm ngưỡng. Rủi ro Bayes dưới $\ell_c$ là
$$
\begin{aligned}
&\sum_x\min\{a(x),3b(x)\}\\
&\quad=0+0{,}04+0{,}08\\
&\qquad+0{,}12+0{,}06+0{,}07\\
&\quad=0{,}37 .
\end{aligned}
$$
Với hàm ngưỡng, $L^c_D(h_t)=\sum_{x<t}a(x)+3\sum_{x\ge t}b(x)$:

| $t$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ | $7$ |
|---|---|---|---|---|---|---|---|
| $L^c_D(h_t)$ | $1{,}53$ | $1{,}23$ | $0{,}79$ | $0{,}51$ | $\mathbf{0{,}39}$ | $0{,}51$ | $0{,}49$ |

nên $\min_tL^c_D(h_t)=L^c_D(h_5)=0{,}39$. Trên $S$, số lỗi có trọng số $\sum_{x<t}c_1(x)+3\sum_{x\ge t}c_0(x)$ lần lượt là $12,9,6,7,5,2,3$, nên nghiệm ERM dưới $\ell_c$ là $h_6$, duy nhất. Rủi ro vượt mức của $h_6$ là $0{,}51-0{,}39=0{,}12$ so với $\mathcal H$ và $0{,}51-0{,}37=0{,}14$ so với rủi ro Bayes. Đẳng thức được nghiệm đúng: $0{,}14=0{,}12+(0{,}39-0{,}37)$, trong đó $0{,}02$ là giá phải trả khi chỉ chọn trong lớp hàm ngưỡng.

**(d)** Khi $t$ vượt qua một điểm $x_i$ của mẫu (từ $t=x_i$ sang $t>x_i$), dự đoán tại $x_i$ đổi từ $1$ sang $0$. Vì vậy $L_{S'}(h_t)$ hằng trên sáu khoảng đóng bên phải:

| $t$ | $t\le0{,}3$ | $(0{,}3;1{,}1]$ | $(1{,}1;1{,}8]$ | $(1{,}8;2{,}5]$ | $(2{,}5;3{,}4]$ | $t>3{,}4$ |
|---|---|---|---|---|---|---|
| $L_{S'}(h_t)$ | $\tfrac25$ | $\tfrac15$ | $\tfrac25$ | $\tfrac15$ | $\tfrac25$ | $\tfrac35$ |

Tập nghiệm ERM là $\{h_t:\ t\in(0{,}3;1{,}1]\cup(1{,}8;2{,}5]\}$. Cận dưới đúng $0{,}3$ không thuộc tập, vì $h_{0{,}3}$ sai trên $(0{,}3;0)$. Với mọi $t$ trong tập, có $t'\in(0{,}3;t)$ cũng thuộc tập, nên "ngưỡng nhỏ nhất" không tồn tại. Giá trị lớn nhất $t=2{,}5$ thuộc tập, nên quy tắc thứ hai chọn được $h_{2{,}5}$ trên $S'$. Trên mọi mẫu, các khoảng hằng của $L_S(h_t)$ đều đóng bên phải, nên khi tập nghiệm bị chặn trên thì nó có phần tử lớn nhất. Các khoảng đó cũng đều mở bên trái hoặc không bị chặn dưới, nên quy tắc ngưỡng nhỏ nhất không chọn được hàm nào trên bất kì mẫu nào.

Quy tắc thứ hai không xác định một thuật toán trên mọi mẫu. Gọi $x_{(m)}$ là giá trị $x$ lớn nhất trong mẫu; mọi $h_t$ với $t>x_{(m)}$ báo $0$ trên cả mẫu. Khi dự đoán toàn $0$ là tối ưu, chẳng hạn khi mọi nhãn bằng $0$, tập nghiệm chứa $(x_{(m)},\infty)$ và không có phần tử lớn nhất; cần một quy ước như $t=x_{(m)}+1$.

**Kiểm tra lại.** $E(1)$ bằng số nhãn 0 ($4$), $E(7)$ bằng số nhãn 1 ($3$), và $L_D(h_1)+L_D(h_7)=0{,}51+0{,}49=1$. Hai hàm lỗi xếp hạng $h_3$ và $h_6$ ngược nhau ($0{,}29<0{,}45$ dưới hàm lỗi 0–1, $0{,}79>0{,}51$ dưới $\ell_c$).
:::

### Bài tập 01.3 (Tính không chệch và giả thuyết chọn theo mẫu)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 3.

::: exercise Bài tập 01.3
Xét bản khả thực $D_f$ của ví dụ sàng lọc: $X$ đều trên $\{1,\ldots,5\}$ và $Y=f(X)=\mathbb 1[X\ge3]$. Lớp giả thuyết gồm sáu hàm ngưỡng $h_t$, $t=1,\ldots,6$, hàm lỗi 0–1. Thuật toán $A_1$ chỉ đọc quan sát đầu tiên $Z_1=(X_1,Y_1)$ của mẫu và trả về hàm ngưỡng khớp nó:
$$
\begin{aligned}
&A_1(S)=h_T,\\
&T=\begin{cases}X_1&\text{khi }Y_1=1,\\X_1+1&\text{khi }Y_1=0.\end{cases}
\end{aligned}
$$

**(a)** Cho $h$ cố định và $Z_1,\ldots,Z_m$ là các biến ngẫu nhiên, mỗi biến có phân bố $D$, không nhất thiết độc lập. Chứng minh $\mathbb E\big[L_S(h)\big]=L_D(h)$. Kiểm tra trên trường hợp $Z_1=\cdots=Z_m$ dưới $D_f$ với $h=h_4$, và so phân bố của $L_S(h_4)$ với trường hợp $S\sim D_f^m$.

Trong các phần còn lại, $S=(Z_1,\ldots,Z_m)\sim D_f^m$ với $m\ge1$.

**(b)** Thay $h$ bằng $A_1(S)$ trong $L_S(h)=\frac1m\sum_{i=1}^m\ell(h,Z_i)$. Chỉ ra bước nào của chứng minh ở (a) không còn đúng với số hạng $i=1$, và giải thích vì sao kết luận của bước đó vẫn đúng với các số hạng $i\ge2$.

**(c)** Tính chính xác $\mathbb E_S\big[L_S(A_1(S))\big]$ và $\mathbb E_S\big[L_{D_f}(A_1(S))\big]$ theo $m$, rồi so sánh tại $m=2$.

**(d)** Thuật toán $A_2$ trả về $h_{X_1}$, bỏ qua $Y_1$. Tính lại hai kì vọng của (c) và so sánh dấu của hiệu $\mathbb E_S[L_{D_f}(A(S))]-\mathbb E_S[L_S(A(S))]$ ở hai thuật toán.

**(e)** Cho $S'\sim D_f^{m'}$ độc lập với $S$. Chứng minh $\mathbb E\big[L_{S'}(A_1(S))\big]=\mathbb E_S\big[L_{D_f}(A_1(S))\big]$.
:::

::: hint Gợi ý 1
Phần (b). Biến ngẫu nhiên $T$ là một hàm của $Z_1$ và chỉ nhận hữu hạn giá trị, nên $\ell(h_T,Z_i)=\sum_t\mathbb 1[T=t]\,\ell(h_t,Z_i)$.
:::

::: hint Gợi ý 2
Phần (b). Với $i\ge2$, $\mathbb 1[T=t]$ là hàm của $Z_1$ và $\ell(h_t,Z_i)$ là hàm của $Z_i$, hai biến độc lập. Với $i=1$, $A_1$ được dựng để khớp $Z_1$, nên $\ell(A_1(S),Z_1)=0$ trên mọi mẫu.
:::

::: hint Gợi ý 3
Phần (c). Dưới $D_f$, $L_{D_f}(h_t)=0{,}2\,\lvert t-3\rvert$. Lập bảng giá trị của $T$ theo $X_1\in\{1,\ldots,5\}$.
:::

::: solution Lời giải Bài tập 01.3
**(a)** Chứng minh có hai bước. Thứ nhất, vì $h$ cố định, $\ell(h,Z_i)$ chỉ phụ thuộc $Z_i$, và $Z_i$ có phân bố $D$, nên $\mathbb E\,\ell(h,Z_i)=L_D(h)$. Thứ hai, theo tính tuyến tính của kì vọng, $\mathbb E[L_S(h)]=\frac1m\sum_i\mathbb E\,\ell(h,Z_i)=L_D(h)$. Không bước nào dùng tính độc lập.

Khi $Z_1=\cdots=Z_m=(X,Y)$, ta có $L_S(h_4)=\mathbb 1[X=3]$, vì $h_4$ và $f$ chỉ khác nhau tại $x=3$; biến này nhận giá trị $0$ hoặc $1$, với kì vọng $0{,}2=L_{D_f}(h_4)$. Khi $S\sim D_f^m$, $L_S(h_4)$ là tỉ lệ quan sát tại $x=3$, cùng kì vọng nhưng tập trung quanh $0{,}2$ khi $m$ lớn.

**(b)** Bước thứ nhất hỏng. Với $h=h_T$,
$$
\begin{aligned}
&\ell(h_T,Z_i)\\
&\quad=\sum_{t=1}^6\mathbb 1[T=t]\,\ell(h_t,Z_i).
\end{aligned}
$$
Với $i\ge2$, $\mathbb 1[T=t]$ là hàm của $Z_1$, còn $\ell(h_t,Z_i)$ là hàm của $Z_i$; theo (T1) hai biến độc lập, nên kì vọng của tích bằng tích các kì vọng và
$$
\begin{aligned}
&\mathbb E\,\ell(h_T,Z_i)\\
&\quad=\sum_t\Pr(T=t)\,L_{D_f}(h_t)\\
&\quad=\mathbb E_S\big[L_{D_f}(h_T)\big].
\end{aligned}
$$
Với $i=1$, cả hai thừa số là hàm của $Z_1$, nên không tách được kì vọng.

**(c)** Dưới $D_f$, $h_t$ và $f=h_3$ khác nhau đúng tại các mức nằm giữa $\min\{t,3\}$ và $\max\{t,3\}-1$, nên $L_{D_f}(h_t)=0{,}2\,\lvert t-3\rvert$. Phân bố của $T$:

| $X_1$ | $1$ | $2$ | $3$ | $4$ | $5$ |
|---|---|---|---|---|---|
| $T$ | $2$ | $3$ | $3$ | $4$ | $5$ |
| $L_{D_f}(h_T)$ | $0{,}2$ | $0$ | $0$ | $0{,}2$ | $0{,}4$ |

Do đó kì vọng theo mẫu của rủi ro kì vọng là
$$
\begin{aligned}
&\mathbb E_S\big[L_{D_f}(A_1(S))\big]\\
&\quad=0{,}2\,(0{,}2+0+0\\
&\qquad+0{,}2+0{,}4)=0{,}16 .
\end{aligned}
$$
Số hạng $i=1$ của $L_S$ bằng $0$ trên mọi mẫu, và theo (b) mỗi số hạng $i\ge2$ có kì vọng $0{,}16$, nên
$$
\begin{aligned}
&\mathbb E_S\big[L_S(A_1(S))\big]\\
&\quad=\frac1m\big(0+(m-1)\cdot0{,}16\big)\\
&\quad=0{,}16\cdot\frac{m-1}m .
\end{aligned}
$$
Tại $m=2$, hai kì vọng là $0{,}08$ và $0{,}16$: rủi ro thực nghiệm đánh giá thấp một lượng $0{,}16/m$.

**(d)** Với $A_2$, $T=X_1$ và $h_{X_1}(X_1)=1$, nên số hạng $i=1$ bằng $\mathbb 1[Y_1=0]=\mathbb 1[X_1\le2]$, có kì vọng $0{,}4$. Kì vọng theo mẫu của rủi ro kì vọng là $\mathbb E_S[L_{D_f}(h_{X_1})]=0{,}2\,(0{,}4+0{,}2+0+0{,}2+0{,}4)=0{,}24$, nên
$$
\begin{aligned}
&\mathbb E_S\big[L_S(A_2(S))\big]\\
&\quad=\frac1m\big(0{,}4+(m-1)\cdot0{,}24\big)\\
&\quad=0{,}24+\frac{0{,}16}m .
\end{aligned}
$$
Tại $m=2$, hai kì vọng là $0{,}32$ và $0{,}24$. Hiệu $\mathbb E_S[L_{D_f}(A(S))]-\mathbb E_S[L_S(A(S))]$ bằng $+0{,}16/m$ với $A_1$ và $-0{,}16/m$ với $A_2$: khi giả thuyết được chọn theo mẫu, độ lệch có thể theo cả hai chiều.

**(e)** Như ở (b), với $\mathbb 1[T=t]$ là hàm của $S$ và $L_{S'}(h_t)$ là hàm của $S'$, hai biến độc lập:
$$
\begin{aligned}
&\mathbb E\big[L_{S'}(h_T)\big]\\
&\quad=\sum_t\Pr(T=t)\,\mathbb E\big[L_{S'}(h_t)\big]\\
&\quad=\sum_t\Pr(T=t)\,L_{D_f}(h_t)\\
&\quad=0{,}16 ,
\end{aligned}
$$
trong đó đẳng thức thứ hai là (a) áp dụng cho từng $h_t$ cố định. Đây là cách sửa của Nhận xét 01.9.

**Kiểm tra lại.** Liệt kê đủ $25$ mẫu cỡ $2$ cho $\tfrac2{25}=0{,}08$ và $\tfrac8{25}=0{,}32$. Với một thuật toán ERM $\hat A$, chiều độ lệch cố định: $L_S(\hat A(S))\le L_S(h)$ trên mọi mẫu, nên theo (a), $\mathbb E_S[L_S(\hat A(S))]\le\inf_{h\in\mathcal H}L_D(h)\le\mathbb E_S[L_D(\hat A(S))]$.
:::

### Bài tập 01.4 (Hàm phân lớp ghi nhớ và hai rủi ro)

**Mức độ:** chứng minh, tính toán, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 5; dùng chặt chẽ các tập có xác suất $0$.

::: exercise Bài tập 01.4
Cho $\mathcal X=[0,1]$ với σ-đại số Borel, $\mathcal Y=\{0,1\}$, lớp $\mathcal H=\mathcal M_{\mathcal X}$, hàm lỗi 0–1 và thuật toán ghi nhớ $A_{\mathrm{gn}}$: tại mỗi điểm của mẫu, $A_{\mathrm{gn}}(s)$ trả về nhãn đa số (nhãn $1$ khi số phiếu bằng nhau), và trả về $0$ ở mọi điểm khác (Định nghĩa 01.14).

**(a)** Giả sử $D_{\mathcal X}$ không có nguyên tử và $Y=f(X)$ chắc chắn, với $f:[0,1]\to\{0,1\}$ đo được. Chứng minh rằng với mọi mẫu $s$ có nhãn $y_i=f(x_i)$, ta có $L_s(A_{\mathrm{gn}}(s))=0$ và $L_D(A_{\mathrm{gn}}(s))=\Pr(f(X)=1)$. Tính hai rủi ro khi $D_{\mathcal X}=U[0,1]$ và $f(x)=\mathbb 1[x>0{,}7]$, rồi so với rủi ro của $f$ và của hàm hằng $0$.

**(b)** Chỉ ra nơi Bước 3 của chứng minh Mệnh đề 01.15 dùng tính hữu hạn của tập $F=\{x_1,\ldots,x_m\}$. Chỉ ra chỗ sai trong lập luận: "mỗi điểm của $[0,1]$ có xác suất $0$ dưới $U[0,1]$, nên mọi tập con Borel của $[0,1]$ có xác suất $0$".

**(c)** Bỏ giả thiết không có nguyên tử: với xác suất $\tfrac12$, $X=0$ (một khối lượng điểm, point mass, tại $0$); với xác suất $\tfrac12$, $X$ đều trên $[0,1]$; và $Y=1$ chắc chắn. Tính $L_D(A_{\mathrm{gn}}(s))$ theo mẫu $s$, rồi tính $\mathbb E_S\big[L_D(A_{\mathrm{gn}}(S))\big]$ và giới hạn của nó khi $m\to\infty$. So sánh với Ví dụ 01.11.
:::

::: hint Gợi ý 1
Phần (a). Tách biến cố lỗi trên một quan sát mới $(X,Y)$ theo hai trường hợp $X\in F$ và $X\notin F$, với $F$ là tập các điểm của mẫu.
:::

::: hint Gợi ý 2
Phần (a). Tập $F$ hữu hạn nên là tập Borel, và theo bất đẳng thức hợp $\Pr(X\in F)\le\sum_{i=1}^m\Pr(X=x_i)$.
:::

::: hint Gợi ý 3
Phần (c). Xét riêng hai trường hợp $0\in F$ và $0\notin F$; mỗi $X_i$ khác $0$ với xác suất $\tfrac12$.
:::

::: solution Lời giải Bài tập 01.4
**(a)** Cố định một mẫu $s$ với $y_i=f(x_i)$. Tại mỗi $x\in F$, mọi quan sát của $s$ tại $x$ có nhãn $f(x)$, nên $A_{\mathrm{gn}}(s)(x)=f(x)$ và $L_s(A_{\mathrm{gn}}(s))=0$. Ngoài $F$, $A_{\mathrm{gn}}(s)=0$, nên trên quan sát mới $(X,f(X))$ nó sai khi và chỉ khi $X\notin F$ và $f(X)=1$. Các tập $F$ và $\{f=1\}$ đều Borel, nên
$$
\begin{aligned}
&L_D\big(A_{\mathrm{gn}}(s)\big)\\
&\quad=\Pr\big(f(X)=1\big)\\
&\qquad-\Pr\big(X\in F,f(X)=1\big).
\end{aligned}
$$
Số hạng cuối nằm giữa $0$ và $\Pr(X\in F)\le\sum_i\Pr(X=x_i)=0$, theo bất đẳng thức hợp và giả thiết không có nguyên tử. Vậy $L_D(A_{\mathrm{gn}}(s))=\Pr(f(X)=1)$ với mọi mẫu $s$, không chỉ hầu chắc chắn; $F$ là tập cố định khi lấy xác suất theo $X$.

Với $U[0,1]$ và $f=\mathbb 1[x>0{,}7]$: $L_S(A_{\mathrm{gn}}(S))=0$ và $L_D(A_{\mathrm{gn}}(S))=0{,}3$, bằng rủi ro của hàm hằng $0$, trong khi nghiệm ERM $f\in\mathcal H$ có rủi ro $0$.

**(b)** Bất đẳng thức hợp được áp dụng cho một hợp hữu hạn; hợp đếm được cũng được, theo tính cộng tính đếm được. Câu trích áp dụng nó cho hợp không đếm được $[0,1]=\bigcup_{x\in[0,1]}\{x\}$, nơi không có quy tắc như vậy: $\Pr(X\in[0,1])=1$ dù mỗi điểm có xác suất $0$.

**(c)** Mọi mẫu rút từ $D$ có mọi nhãn bằng $1$, và với các mẫu đó $A_{\mathrm{gn}}(s)=\mathbb 1_F$, sai khi và chỉ khi $X\notin F$. Phần đều gán xác suất $0$ cho $F$, nên $\Pr(X\in F)=\tfrac12\,\mathbb 1[0\in F]$ và
$$
\begin{aligned}
&L_D\big(A_{\mathrm{gn}}(s)\big)\\
&\quad=\begin{cases}\tfrac12&\text{khi }0\in F,\\1&\text{khi }0\notin F.\end{cases}
\end{aligned}
$$
Mỗi $X_i$ khác $0$ với xác suất $\tfrac12$, độc lập, nên $\Pr(0\notin S)=2^{-m}$ và
$$
\begin{aligned}
&\mathbb E_S\big[L_D(A_{\mathrm{gn}}(S))\big]\\
&\quad=\tfrac12\big(1-2^{-m}\big)+2^{-m}\\
&\quad=\tfrac12+\tfrac12\cdot2^{-m},
\end{aligned}
$$
bằng $\tfrac34$ tại $m=1$ và tiến về $\tfrac12$. Hàm phân lớp ghi nhớ chỉ đúng trên các điểm đã xuất hiện trong mẫu, và trong các điểm đó chỉ nguyên tử có khối lượng dương, nên rủi ro bằng $1$ trừ tổng khối lượng các nguyên tử đã xuất hiện; trong Ví dụ 01.11, mọi khối lượng nằm ở nguyên tử, nên kì vọng $0{,}8^m$ tiến về $0$.

**Kiểm tra lại.** Với $f\equiv1$, công thức (a) cho rủi ro $1$, đúng Mệnh đề 01.15(b); với $f\equiv0$, nó cho $0$, vì nhãn mặc định $0$ của $A_{\mathrm{gn}}$ đúng ở mọi nơi. Một lỗi thường gặp là coi $F$ là tập ngẫu nhiên khi tính $L_D(A_{\mathrm{gn}}(s))$; rủi ro kì vọng được tính với mẫu cố định.
:::

### Bài tập 01.5 (Định nghĩa học PAC với đủ lượng từ)

**Mức độ:** khái niệm, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 4; thứ tự lượng từ, vai trò của $\epsilon$ và $\delta$.

::: exercise Bài tập 01.5
**(a)** Viết khẳng định "$A$ là thuật toán học PAC cho $\mathcal H$" (Định nghĩa 01.18) thành một dòng lượng từ, rồi viết phủ định của nó. Viết phủ định của "$\mathcal H$ học được PAC".

**(b)** Viết dòng lượng từ cho "$A$ là thuật toán học PAC bất khả tri cho $\mathcal H$" (Định nghĩa 01.25) và chỉ ra hai chỗ khác với (a).

**(c)** Lấy $\mathcal X=\mathbb N$ với mọi tập con đo được, $\mathcal H=\mathcal M_{\mathcal X}$ (mọi hàm $\mathbb N\to\{0,1\}$), hàm lỗi 0–1 và thuật toán ghi nhớ $A_{\mathrm{gn}}$ (Định nghĩa 01.14). Chứng minh:

1. với mọi $D$ mà $(D,\mathcal H)$ khả thực và mọi $\epsilon,\delta\in(0,1)$, tồn tại $m_0$ sao cho $\Pr_{S\sim D^m}\big[L_D(A_{\mathrm{gn}}(S))\le\epsilon\big]\ge1-\delta$ với mọi $m\ge m_0$;
2. với mọi $\epsilon\in(0,\tfrac12)$ và mọi $m$, tồn tại $D$ khả thực với $\Pr_{S\sim D^m}\big[L_D(A_{\mathrm{gn}}(S))\le\epsilon\big]=0$.

Rút ra kết luận về hai thứ tự "$\forall D\ \exists m_0$" và "$\exists M\ \forall D$".

**(d)** Xét bản khả thực $D_f$ của ví dụ sàng lọc ($X$ đều trên $\{1,\ldots,5\}$, $Y=\mathbb 1[X\ge3]$), lớp sáu hàm ngưỡng và thuật toán $A_{\max}$ trả về ngưỡng lớn nhất trong tập nghiệm ERM. Theo Ví dụ 01.9, $\Pr_S[L_{D_f}(A_{\max}(S))\le0{,}1]\ge0{,}95$ khi $m\ge14$. Trên mẫu $S_f=((1,0),(2,0),(4,1),(5,1))$, $A_{\max}$ trả về $h_4$. Nói câu nào dưới đây đúng và giải thích:

1. "Hàm phân lớp học được dự đoán sai với xác suất không quá $0{,}05$."
2. "Với xác suất ít nhất $0{,}95$ theo mẫu huấn luyện cỡ $m\ge14$, hàm phân lớp học được có xác suất lỗi không quá $0{,}1$."
3. "Ít nhất $95\%$ số người được sàng lọc nhận kết quả đúng."
4. "Đã có mẫu $S_f$; xác suất để $L_{D_f}(A_{\max}(S_f))\le0{,}1$ là $0{,}95$."

**(e)** Dưới bản có nhiễu $D_\eta$ của ví dụ sàng lọc, $\min_tL_{D_\eta}(h_t)=0{,}22$. Giải thích vì sao câu 2 không thể đúng dưới $D_\eta$, và viết câu đúng thay cho nó.
:::

::: hint Gợi ý 1
Phần (a). Viết các lượng từ theo đúng thứ tự xuất hiện trong Định nghĩa 01.18, rồi phủ định lần lượt từ trái sang phải.
:::

::: hint Gợi ý 2
Phần (c). Với ý 1, chọn một tập hữu hạn $K\subset\mathbb N$ có $D_{\mathcal X}(\mathbb N\setminus K)\le\epsilon$. Với ý 2, một mẫu cỡ $m$ chứa nhiều nhất $m$ điểm khác nhau.
:::

::: hint Gợi ý 3
Phần (d). Tách hai xác suất: xác suất lỗi $L_D(h)$ của một hàm cố định, lấy theo một quan sát mới; và xác suất theo mẫu huấn luyện, mà $\delta$ chặn.
:::

::: solution Lời giải Bài tập 01.5
**(a)** Trong dòng sau, $D$ chạy trên các phân bố mà $(D,\mathcal H)$ khả thực:
$$
\begin{aligned}
&\exists M:(0,1)^2\to\mathbb N\\
&\forall\epsilon,\delta\in(0,1)\ \ \forall D\\
&\forall m\ge M(\epsilon,\delta):\\
&\Pr_{S\sim D^m}\big[L_D(A(S))\le\epsilon\big]\\
&\qquad\ge1-\delta .
\end{aligned}
$$
Giá trị $M(\epsilon,\delta)$ chọn được độc lập cho từng cặp, nên phủ định là
$$
\begin{aligned}
&\exists\epsilon,\delta\in(0,1)\\
&\forall m_0\in\mathbb N\ \ \exists D\ \ \exists m\ge m_0:\\
&\Pr_{S\sim D^m}\big[L_D(A(S))\le\epsilon\big]\\
&\qquad<1-\delta ,
\end{aligned}
$$
tức $m_A(\epsilon,\delta)=\infty$ với ít nhất một cặp $(\epsilon,\delta)$. "$\mathcal H$ không học được PAC" nghĩa là dòng phủ định đúng với mọi thuật toán $A$ có đầu ra trong $\mathcal H$, với $(\epsilon,\delta)$ được phép phụ thuộc $A$.

**(b)** Dòng lượng từ giữ nguyên thứ tự, với biến cố mới:
$$
\begin{aligned}
&\exists M\ \ \forall\epsilon,\delta\in(0,1)\\
&\forall D\ \ \forall m\ge M(\epsilon,\delta):\\
&\Pr_{S\sim D^m}\Big[L_D(A(S))\\
&\quad\le\inf_{h\in\mathcal H}L_D(h)+\epsilon\Big]\ge1-\delta .
\end{aligned}
$$
Hai chỗ khác: $D$ chạy trên mọi phân bố có rủi ro hữu hạn trên $\mathcal H$ thay vì các phân bố khả thực, và $\epsilon$ được cộng vào $\inf_{h\in\mathcal H}L_D(h)$ thay vì vào $0$.

**(c)1.** Cho $D$ khả thực: $Y=f(X)$ hầu chắc chắn với một $f\in\mathcal M_{\mathcal X}$, nên hầu chắc chắn mọi nhãn của mẫu bằng $f$ tại điểm tương ứng. Vì $\sum_xD_{\mathcal X}(x)=1$, có một tập hữu hạn $K$ với $D_{\mathcal X}(\mathbb N\setminus K)\le\epsilon$; đặt $K_+=\{x\in K:\ D_{\mathcal X}(x)>0\}$. Như ở Bài tập 01.4(a), $A_{\mathrm{gn}}(S)$ đúng tại mọi điểm đã xuất hiện. Khi mọi điểm của $K_+$ xuất hiện, tập lỗi nằm trong $(\mathbb N\setminus K)\cup(K\setminus K_+)$, có khối lượng không quá $\epsilon$. Theo bất đẳng thức hợp,
$$
\begin{aligned}
&\Pr_S\big[L_D(A_{\mathrm{gn}}(S))>\epsilon\big]\\
&\quad\le\sum_{x\in K_+}\big(1-D_{\mathcal X}(x)\big)^m .
\end{aligned}
$$
Vế phải là tổng hữu hạn, giảm theo $m$ và tiến về $0$, nên có $m_0$ như yêu cầu; $m_0$ phụ thuộc $D$.

**(c)2.** Cho $m$ và $\epsilon<\tfrac12$. Lấy $D_{\mathcal X}$ đều trên $\{1,\ldots,2m\}$ và $Y=1$ chắc chắn; $(D,\mathcal H)$ khả thực với $h^\star\equiv1$. Mẫu cỡ $m$ bỏ sót ít nhất $m$ điểm của $\{1,\ldots,2m\}$, tại đó $A_{\mathrm{gn}}(S)$ trả $0$ trong khi nhãn là $1$. Vậy trên mọi mẫu $L_D(A_{\mathrm{gn}}(S))\ge\tfrac m{2m}=\tfrac12>\epsilon$.

Với mọi hàm $M$, lấy $m=M(\epsilon,\delta)$ và phân bố trên thì bất đẳng thức của Định nghĩa 01.18 sai. Vậy $A_{\mathrm{gn}}$ thỏa "$\forall D\ \exists m_0$" nhưng không thỏa "$\exists M\ \forall D$", thứ tự lượng từ của định nghĩa học PAC.

**(d)** Câu 2 đúng: nó là bất đẳng thức của Định nghĩa 01.18 với $\epsilon=0{,}1$, $\delta=0{,}05$ cho riêng $D_f$, đúng theo Ví dụ 01.9; dưới hàm lỗi 0–1, $L_D(h)$ là xác suất lỗi. Câu 1 nhầm vai trò: xác suất dự đoán sai trên một quan sát mới là $L_D(A(S))$, được chặn bởi $\epsilon=0{,}1$, và chỉ trên một biến cố có xác suất ít nhất $1-\delta$ theo mẫu. Câu 3 sai hai lần: trên biến cố thành công, tỉ lệ người nhận kết quả đúng chỉ được bảo đảm là $1-L_D(A(S))\ge0{,}9$, và biến cố đó không chắc chắn xảy ra. Câu 4 sai vì sau khi có $S_f$, $L_{D_f}(h_4)=0{,}2$ là một số cố định lớn hơn $0{,}1$; không còn xác suất nào để gán (Nhận xét 01.19), và cỡ $m=4$ cũng chưa đạt ngưỡng $14$.

**(e)** Dưới $D_\eta$, mọi hàm ngưỡng có $L_{D_\eta}(h_t)\ge0{,}22>0{,}1$, nên không thuật toán học đúng lớp nào đạt được câu 2. Bảo đảm thích hợp là bất khả tri. Nếu $A$ là thuật toán học PAC bất khả tri cho lớp hàm ngưỡng với hàm $M$ (Định nghĩa 01.25), thì với mọi $m\ge M(0{,}1;\,0{,}05)$, với xác suất ít nhất $0{,}95$ theo mẫu, $L_{D_\eta}(A(S))\le0{,}22+0{,}1=0{,}32$. Cỡ mẫu $14$ của Ví dụ 01.9 được tính cho $D_f$ và $A_{\max}$, nên không chuyển sang $D_\eta$. ERM trên một lớp hữu hạn là một thuật toán như vậy (Bài 02).

**Kiểm tra lại.** Hai lỗi thường gặp: đặt $\forall D$ trước $\exists M$, và phủ định "$\ge1-\delta$" thành "$\le1-\delta$". Cỡ mẫu $14$ của Ví dụ 01.9 chỉ là một khẳng định dạng "$\forall D\ \exists m_0$".
:::

## Bài tập chọn từ UML

### Bài tập 01.6 (Hàm phân lớp ghi nhớ là một đa thức có ngưỡng; UML Bài tập 2.1)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 5; một lớp mô tả bằng hữu hạn hệ số vẫn có thể chứa hàm phân lớp ghi nhớ.

::: exercise Bài tập 01.6
Cho $\mathcal X=\mathbb R^p$ với σ-đại số Borel và $\mathcal Y=\{0,1\}$. *Lớp đa thức có ngưỡng* (thresholded polynomials) là
$$
\begin{aligned}
\mathcal H_{\mathrm{poly}}=\big\{&x\mapsto\mathbb 1[q(x)\ge0]:\\
&q\in\mathbb R[x_1,\ldots,x_p]\big\},
\end{aligned}
$$
trong đó $\mathbb R[x_1,\ldots,x_p]$ là tập các đa thức $p$ biến với hệ số thực, không giới hạn bậc. Với một mẫu $s$, gọi $F_1(s)$ là tập các điểm $x_i$ của mẫu mà $A_{\mathrm{gn}}(s)(x_i)=1$, tức các điểm có nhãn đa số bằng $1$ (Định nghĩa 01.14).

**(a)** Dựng một đa thức $q_s$ sao cho với mọi $x\in\mathbb R^p$, $A_{\mathrm{gn}}(s)(x)=1$ khi và chỉ khi $q_s(x)\ge0$. Nêu bậc của $q_s$, kể cả khi $F_1(s)=\varnothing$.

**(b)** Suy ra $A_{\mathrm{gn}}$ là một thuật toán ERM trên $\mathcal H_{\mathrm{poly}}$.

**(c)** Xét phân bố $D$: $X$ đều trên $[0,1]^p$ và $Y=1$ chắc chắn. Chứng minh $L_S(A_{\mathrm{gn}}(S))=0$ và $L_D(A_{\mathrm{gn}}(S))=1$ trên mọi mẫu, trong khi $\mathcal H_{\mathrm{poly}}$ chứa một nghiệm ERM có rủi ro kì vọng $0$. Dùng khái niệm thiên kiến quy nạp (§5) để giải thích vì sao bỏ giới hạn bậc làm mất bảo đảm học.
:::

::: hint Gợi ý 1
Phần (a). Cần một đa thức không dương trên $\mathbb R^p$ và bằng $0$ đúng tại các điểm của $F_1(s)$.
:::

::: hint Gợi ý 2
Phần (a). Với $z\in\mathbb R^p$, $\lVert x-z\rVert^2=\sum_{j=1}^p(x_j-z_j)^2$ là đa thức bậc $2$ theo $x$, không âm, và bằng $0$ khi và chỉ khi $x=z$.
:::

::: hint Gợi ý 3
Phần (c). Lặp lại Bước 2 và Bước 3 của chứng minh Mệnh đề 01.15 với $[0,1]^p$ thay cho $[0,1]$; hàm hằng $1$ là $\mathbb 1[q\ge0]$ với $q\equiv0$.
:::

::: solution Lời giải Bài tập 01.6
**(a)** Đặt
$$
q_s(x)=-\prod_{z\in F_1(s)}\lVert x-z\rVert^2 ,
$$
với tích lấy trên các điểm phân biệt của $F_1(s)$ và tích rỗng bằng $1$, tức $q_s\equiv-1$ khi $F_1(s)=\varnothing$. Đa thức $q_s$ có bậc $2\lvert F_1(s)\rvert\le2m$. Mỗi thừa số không âm, nên $q_s\le0$, và $q_s(x)=0$ khi và chỉ khi một thừa số bằng $0$, tức $x\in F_1(s)$. Do đó $\mathbb 1[q_s\ge0]=\mathbb 1_{F_1(s)}=A_{\mathrm{gn}}(s)$ theo Định nghĩa 01.14.

**(b)** Theo Bước 2 của chứng minh Mệnh đề 01.15, $A_{\mathrm{gn}}(s)$ đạt rủi ro thực nghiệm nhỏ nhất trên mọi hàm $\mathcal X\to\{0,1\}$. Vì $A_{\mathrm{gn}}(s)\in\mathcal H_{\mathrm{poly}}$, nó đạt $\min_{h\in\mathcal H_{\mathrm{poly}}}L_s(h)$ với mọi mẫu $s$. Điều kiện đo được của Định nghĩa 01.4 được kiểm như Phụ lục A(iii), vì $\mathbb R^p$ cũng là không gian mêtric khả li.

**(c)** Vì $Y=1$, $F_1(S)=F=\{X_1,\ldots,X_m\}$, $A_{\mathrm{gn}}(S)=\mathbb 1_F$ và $L_S(A_{\mathrm{gn}}(S))=0$. Phân bố đều trên $[0,1]^p$ gán xác suất $0$ cho mỗi điểm, nên theo bất đẳng thức hợp $\Pr(X\in F)=0$ và $L_D(A_{\mathrm{gn}}(S))=1$. Đa thức $q\equiv0$ cho hàm hằng $1\in\mathcal H_{\mathrm{poly}}$, một nghiệm ERM có rủi ro $0$. Như trong Hệ quả 01.29, $A_{\mathrm{gn}}$ không là thuật toán học PAC cho $\mathcal H_{\mathrm{poly}}$.

Thiên kiến quy nạp là một cam kết về dạng hàm dự đoán, đặt ra trước khi thấy dữ liệu. Theo (a), trên mọi tập hữu hạn điểm, $\mathcal H_{\mathrm{poly}}$ thực hiện được mọi cách gán nhãn, như $\mathcal M_{\mathcal X}$, nên trên mẫu hữu hạn nó không cam kết gì. Giới hạn bậc là một cam kết thật. Xét $p=1$ và một đa thức $q\not\equiv0$ có bậc không quá $k$ sao cho tập $\{q\ge0\}$ hữu hạn. Với một điểm $x_0$, nếu $q(x_0)>0$ hoặc $x_0$ là nghiệm bội lẻ của $q$, thì $q\ge0$ trên một khoảng sát $x_0$. Do đó mỗi điểm $x_0$ của tập $\{q\ge0\}$ là nghiệm bội chẵn của $q$, và tập này có nhiều nhất $k/2$ điểm.

**Kiểm tra lại.** Bình phương trong $\lVert x-z\rVert^2$ là cần thiết. Với $p=1$ và $F_1(s)=\{0,1\}$, đa thức $-x(x-1)$ không âm trên cả đoạn $[0,1]$, còn $-x^2(x-1)^2$ chỉ bằng $0$ tại $0$ và $1$.
:::

### Bài tập 01.7 (Tính đơn điệu của độ phức tạp mẫu; UML Bài tập 3.1)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 4; độ phức tạp mẫu của thuật toán và của lớp.

::: exercise Bài tập 01.7
Cho lớp $\mathcal H$ các hàm phân lớp nhị phân, hàm lỗi 0–1 và trường hợp khả thực. Độ phức tạp mẫu $m_A(\epsilon,\delta)$ của thuật toán $A$ là số $m_0\in\mathbb N$ nhỏ nhất sao cho bất đẳng thức của Định nghĩa 01.18 đúng với mọi $D$ khả thực và mọi $m\ge m_0$ (bằng $\infty$ nếu không có $m_0$ nào); độ phức tạp mẫu của lớp là $m_{\mathcal H}(\epsilon,\delta)=\min_Am_A(\epsilon,\delta)$ (Định nghĩa 01.20).

**(a)** Chứng minh rằng với mọi thuật toán $A$: nếu $0<\epsilon_1\le\epsilon_2<1$ thì $m_A(\epsilon_1,\delta)\ge m_A(\epsilon_2,\delta)$; nếu $0<\delta_1\le\delta_2<1$ thì $m_A(\epsilon,\delta_1)\ge m_A(\epsilon,\delta_2)$.

**(b)** Suy ra $m_{\mathcal H}$ không tăng theo từng biến, kể cả khi giá trị nhỏ nhất tại hai cặp $(\epsilon,\delta)$ đạt được bởi hai thuật toán khác nhau.

**(c)** Một hàm $M$ thỏa Định nghĩa 01.18 cho thuật toán $A$ có nhất thiết không tăng theo từng biến không? Chứng minh hoặc cho phản ví dụ.
:::

::: hint Gợi ý 1
Phần (a). Viết $m_A(\epsilon,\delta)$ là phần tử nhỏ nhất của tập $B_A(\epsilon,\delta)$ các $m_0$ thỏa điều kiện, rồi so sánh hai tập; biến cố $\{L_D(A(S))\le\epsilon_1\}$ nằm trong $\{L_D(A(S))\le\epsilon_2\}$.
:::

::: hint Gợi ý 2
Phần (b). Chọn thuật toán đạt $m_{\mathcal H}$ tại cặp khó hơn, $(\epsilon_1,\delta)$.
:::

::: solution Lời giải Bài tập 01.7
**(a)** Gọi $B_A(\epsilon,\delta)$ là tập các $m_0\in\mathbb N$ sao cho $\Pr_{S\sim D^m}[L_D(A(S))\le\epsilon]\ge1-\delta$ với mọi $D$ khả thực và mọi $m\ge m_0$; khi đó $m_A(\epsilon,\delta)=\min B_A(\epsilon,\delta)$, với $\min\varnothing=\infty$. Nếu $\epsilon_1\le\epsilon_2$, biến cố thành công với $\epsilon_1$ nằm trong biến cố thành công với $\epsilon_2$, nên xác suất của biến cố sau không nhỏ hơn. Do đó $B_A(\epsilon_1,\delta)\subseteq B_A(\epsilon_2,\delta)$, nên phần tử nhỏ nhất của $B_A(\epsilon_2,\delta)$ nhỏ hơn hoặc bằng phần tử nhỏ nhất của $B_A(\epsilon_1,\delta)$: $m_A(\epsilon_2,\delta)\le m_A(\epsilon_1,\delta)$. Khi $B_A(\epsilon_1,\delta)=\varnothing$, vế phải bằng $\infty$ nên bất đẳng thức vẫn đúng. Nếu $\delta_1\le\delta_2$ thì $1-\delta_1\ge1-\delta_2$, nên $B_A(\epsilon,\delta_1)\subseteq B_A(\epsilon,\delta_2)$ và kết luận tương tự.

**(b)** Cho $\epsilon_1\le\epsilon_2$. Giá trị nhỏ nhất trong định nghĩa $m_{\mathcal H}$ đạt được, vì mọi tập con khác rỗng của $\mathbb N\cup\{\infty\}$ có phần tử nhỏ nhất; gọi $A_1$ là một thuật toán có $m_{A_1}(\epsilon_1,\delta)=m_{\mathcal H}(\epsilon_1,\delta)$. Theo định nghĩa của $m_{\mathcal H}$ và (a),
$$
\begin{aligned}
m_{\mathcal H}(\epsilon_2,\delta)
&\le m_{A_1}(\epsilon_2,\delta)\\
&\le m_{A_1}(\epsilon_1,\delta)\\
&=m_{\mathcal H}(\epsilon_1,\delta).
\end{aligned}
$$
Lập luận không cần $A_1$ tối ưu tại $(\epsilon_2,\delta)$; với biến $\delta$, lập luận giống hệt. Lập luận không cần giả thiết $\mathcal H$ học được PAC của UML.

**(c)** Không. Nếu $M$ thỏa Định nghĩa 01.18 cho $A$ thì mọi hàm $M'\ge M$ cũng thỏa. Lấy lớp một phần tử $\mathcal H=\{h_{\equiv0}\}$ và thuật toán luôn trả về $h_{\equiv0}$: với mọi $D$ khả thực, $L_D(h_{\equiv0})=0$, nên $M\equiv1$ thỏa định nghĩa. Hàm $M'(\epsilon,\delta)=1+1000\cdot\mathbb 1[\epsilon>\tfrac12]$ cũng thỏa, nhưng $M'(0{,}6;\,\delta)=1001>M'(0{,}4;\,\delta)=1$. Tính đơn điệu thuộc về hàm nhỏ nhất $m_A$, không thuộc về mọi hàm cỡ mẫu đủ.

**Kiểm tra lại.** Lập luận của (a) cũng áp dụng cho cỡ mẫu tính riêng cho một phân bố: trong Ví dụ 01.9, với $A_{\max}$ dưới $D_f$ và $\delta=0{,}05$, cỡ mẫu cần là $14$ khi $\epsilon=0{,}1$ và $6$ khi $\epsilon=0{,}25$. Lỗi thường gặp ở (b) là giả sử một thuật toán duy nhất đạt $m_{\mathcal H}$ tại mọi cặp $(\epsilon,\delta)$ (Nhận xét 01.21).
:::

### Bài tập 01.8 (Lớp hàm chỉ thị của một điểm; UML Bài tập 3.2)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 4; thiết kế thuật toán ERM với quy tắc chọn khi bằng nhau, cận độ phức tạp mẫu.

::: exercise Bài tập 01.8
Cho tập đầu vào $\mathcal X$ đếm được (hữu hạn hoặc vô hạn đếm được) với mọi tập con đo được, $\mathcal Y=\{0,1\}$ và hàm lỗi 0–1. *Lớp hàm chỉ thị của một điểm* (class of singletons) là $\mathcal H_{\mathrm{sg}}=\{h_z:\ z\in\mathcal X\}\cup\{h_-\}$, trong đó $h_z(x)=\mathbb 1[x=z]$ và $h_-\equiv0$. Khi $(D,\mathcal H_{\mathrm{sg}})$ khả thực, mọi nhãn bằng $0$ hầu chắc chắn, trừ có thể tại một điểm $z^\star$.

**(a)** Mô tả một thuật toán ERM trên $\mathcal H_{\mathrm{sg}}$, đúng trên mọi mẫu (kể cả mẫu không khớp được bởi giả thuyết nào), và nêu số phép tính. Trên một mẫu khớp được bởi một giả thuyết của $\mathcal H_{\mathrm{sg}}$, thuật toán trả về gì?

**(b)** Chứng minh $\mathcal H_{\mathrm{sg}}$ học được PAC và $m_{\mathcal H_{\mathrm{sg}}}(\epsilon,\delta)\le\lceil\ln(1/\delta)/\epsilon\rceil$.

**(c)** Lấy $\mathcal X=\mathbb N$ và thuật toán $B$: nếu mẫu có quan sát $(x_i,1)$ thì trả về $h_{x_i}$ với $i$ nhỏ nhất như vậy; nếu không, trả về $h_z$ với $z$ là số tự nhiên nhỏ nhất không xuất hiện trong mẫu. Chứng minh $B$ trả về một nghiệm ERM trên mọi mẫu khớp được bởi một giả thuyết của $\mathcal H_{\mathrm{sg}}$. Với $D_{\mathcal X}$ đều trên $\{1,\ldots,9\}$, $Y=0$ chắc chắn, $\epsilon=0{,}1$, $\delta=0{,}05$ và $m=30\ge\lceil\ln(1/\delta)/\epsilon\rceil$, chứng minh $\Pr_S\big[L_D(B(S))>\epsilon\big]>\delta$.
:::

::: hint Gợi ý 1
Phần (a). Gọi $a_z$, $b_z$ là số quan sát nhãn 1, nhãn 0 tại $z$. Đếm số lỗi của $h_-$ và của $h_z$ theo các số này.
:::

::: hint Gợi ý 2
Phần (b). Khi giả thuyết đúng là $h_{z^\star}$, thuật toán ở (a) chỉ thất bại nếu $z^\star$ không xuất hiện trong mẫu và $D_{\mathcal X}(z^\star)>\epsilon$. Dùng $1-x\le e^{-x}$.
:::

::: hint Gợi ý 3
Phần (c). Gọi $E_j$ là biến cố điểm $j$ không xuất hiện trong mẫu. Chứng minh $\mathbb 1[\bigcup_jE_j]\ge\sum_j\mathbb 1[E_j]-\sum_{j<k}\mathbb 1[E_j]\,\mathbb 1[E_k]$ bằng cách đếm số biến cố xảy ra.
:::

::: solution Lời giải Bài tập 01.8
**(a)** Với mẫu $s$, đặt $a_z=\#\{i:\ x_i=z,\ y_i=1\}$, $b_z=\#\{i:\ x_i=z,\ y_i=0\}$ và $N_1=\sum_za_z$. Hàm $h_-$ sai trên mọi quan sát nhãn 1, tức $N_1$ lỗi. Hàm $h_z$ đúng trên các quan sát nhãn 1 tại $z$, sai trên các quan sát nhãn 0 tại $z$ và trên mọi quan sát nhãn 1 ở nơi khác, tức $N_1-a_z+b_z$ lỗi; với $z$ không xuất hiện, số này bằng $N_1$. Thuật toán: tính $g_z=a_z-b_z$ cho mọi $z$ xuất hiện; nếu $\max_zg_z>0$, trả về $h_z$ với $z$ đạt giá trị lớn nhất xuất hiện sớm nhất trong mẫu; nếu không, trả về $h_-$. Đây là thuật toán ERM trên mọi mẫu, và khi $\max_zg_z\le0$ nó chọn $h_-$ trong số các nghiệm bằng nhau. Sắp xếp mẫu theo $x$ rồi đếm cần $O(m\log m)$ phép tính.

Trên một mẫu khớp được bởi một giả thuyết của $\mathcal H_{\mathrm{sg}}$, nhãn 1 chỉ xuất hiện tại một điểm, nên thuật toán trả về $h_{x_i}$ nếu có quan sát $(x_i,1)$ và $h_-$ nếu không. Gọi thuật toán này là $A_{\mathrm{sg}}$.

**(b)** Cho $D$ khả thực với giả thuyết không lỗi $h^\star$; hầu chắc chắn mọi nhãn của mẫu bằng $h^\star(x_i)$. Nếu $h^\star=h_-$, mẫu không có nhãn 1 và $A_{\mathrm{sg}}$ trả về $h_-$, rủi ro $0$. Nếu $h^\star=h_{z^\star}$, đặt $\rho=D_{\mathcal X}(z^\star)$. Khi $z^\star$ xuất hiện, nó mang nhãn 1 và $A_{\mathrm{sg}}$ trả về $h_{z^\star}$, rủi ro $0$. Khi $z^\star$ vắng mặt, $A_{\mathrm{sg}}$ trả về $h_-$, có rủi ro $\Pr(Y=1)=\rho$.

Do đó thất bại chỉ xảy ra khi $\rho>\epsilon$ và $z^\star$ vắng mặt; nếu $\rho\le\epsilon$, thuật toán không bao giờ thất bại. Khi $\rho>\epsilon$,
$$
\begin{aligned}
&\Pr_S\big[L_D(A_{\mathrm{sg}}(S))>\epsilon\big]\\
&\quad=(1-\rho)^m\\
&\quad<(1-\epsilon)^m\le e^{-\epsilon m},
\end{aligned}
$$
trong đó bất đẳng thức cuối là $1-x\le e^{-x}$. Vế phải không quá $\delta$ khi $m\ge\ln(1/\delta)/\epsilon$, nên $m_{\mathcal H_{\mathrm{sg}}}(\epsilon,\delta)\le m_{A_{\mathrm{sg}}}(\epsilon,\delta)\le\lceil\ln(1/\delta)/\epsilon\rceil$.

**(c)** Trên một mẫu khớp được có nhãn 1, $B$ trả về cùng hàm như $A_{\mathrm{sg}}$. Trên một mẫu không có nhãn 1, $h_z$ với $z$ không xuất hiện trong mẫu phân lớp đúng mọi quan sát, nên là nghiệm ERM; $B$ chỉ khác $A_{\mathrm{sg}}$ ở quy tắc chọn khi bằng nhau.

Dưới phân bố đã cho, nếu cả chín điểm $1,\ldots,9$ xuất hiện thì $B$ trả về $h_z$ với $z\ge10$, rủi ro $0$; nếu một điểm vắng mặt thì $z\le9$ và rủi ro là $\tfrac19>0{,}1$. Vậy xác suất thất bại là $\Pr(\bigcup_{j=1}^9E_j)$, với $\Pr(E_j)=(\tfrac89)^{30}$ và $\Pr(E_j\cap E_k)=(\tfrac79)^{30}$ khi $j<k$. Nếu đúng $J$ biến cố xảy ra thì $J-\binom J2\le\mathbb 1[J\ge1]$: hai vế bằng $0$ khi $J=0$, và với $J\ge1$, $1-J+\binom J2=\tfrac{(J-1)(J-2)}2\ge0$. Vì $\mathbb EJ=\sum_j\Pr(E_j)$ và $\mathbb E\binom J2=\sum_{j<k}\Pr(E_j\cap E_k)$, lấy kì vọng hai vế cho
$$
\begin{aligned}
\Pr\Big(\bigcup_jE_j\Big)
&\ge9\Big(\frac89\Big)^{30}\\
&\quad-\binom92\Big(\frac79\Big)^{30}\\
&\approx0{,}2628-0{,}0191\\
&=0{,}2437>0{,}05 .
\end{aligned}
$$
Khi mẫu không có nhãn 1, $A_{\mathrm{sg}}$ chỉ có thể sai tại $z^\star$, còn $B$ sai khi bất kì điểm nào trong chín điểm có khối lượng lớn hơn $\epsilon$ vắng mặt.

**Kiểm tra lại.** Tại $\epsilon=0{,}1$, $\delta=0{,}05$: $\lceil10\ln20\rceil=\lceil29{,}96\rceil=30$ và $(1-\epsilon)^{30}\approx0{,}0424\le e^{-3}\approx0{,}0498\le0{,}05$. Trường hợp $D_{\mathcal X}(z^\star)\le\epsilon$ thường bị bỏ sót: khi đó $h_-$ đã có rủi ro không quá $\epsilon$.
:::

### Bài tập 01.9 (Lớp hình tròn đồng tâm và lớp hàm ngưỡng; UML Bài tập 3.3)

**Mức độ:** chứng minh, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 4; cận độ phức tạp mẫu không phụ thuộc phân bố, kể cả khi phân bố có nguyên tử.

::: exercise Bài tập 01.9
Cho $\mathcal X=\mathbb R^2$ với σ-đại số Borel, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và *lớp hình tròn đồng tâm* (concentric circles) $\mathcal H_\circ=\{h_r:\ r\ge0\}$, với $h_r(x)=\mathbb 1[\lVert x\rVert\le r]$, tức $h_r$ gán nhãn 1 cho các điểm của hình tròn đóng tâm $0$ bán kính $r$. Giả sử $(D,\mathcal H_\circ)$ khả thực với giả thuyết không lỗi $h_{r^\star}$.

**(a)** Thuật toán $A_\circ$ trả về $h_{\hat r}$ với $\hat r=\max\{\lVert x_i\rVert:\ y_i=1\}$, và $\hat r=0$ khi mẫu không có nhãn 1. Chứng minh $A_\circ$ trả về một nghiệm ERM trên mọi mẫu khớp được bởi một giả thuyết của $\mathcal H_\circ$, và $\hat r\le r^\star$ hầu chắc chắn.

**(b)** Chứng minh rằng với mọi $\epsilon,\delta\in(0,1)$, mọi $D$ khả thực và mọi $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$,
$$
\Pr_{S\sim D^m}\big[L_D(A_\circ(S))\le\epsilon\big]\ge1-\delta ,
$$
nên $m_{\mathcal H_\circ}(\epsilon,\delta)\le\lceil\ln(1/\delta)/\epsilon\rceil$. Lập luận phải đúng cả khi $D_{\mathcal X}$ có nguyên tử, chẳng hạn khi mọi khối lượng dồn vào một điểm $u$ với $\lVert u\rVert=r^\star$.

**(c)** Trên $\mathcal X=\{1,\ldots,K\}$, xét lớp hàm ngưỡng $\{h_t:\ t=1,\ldots,K+1\}$ và thuật toán $A_{\max}$ trả về $h_t$ với $t$ lớn nhất trong tập nghiệm ERM. Chứng minh $m_{A_{\max}}(\epsilon,\delta)\le\lceil\ln(1/\delta)/\epsilon\rceil$ bằng lập luận của (b). Tính cận khi $\epsilon=0{,}1$, $\delta=0{,}05$ và so với cỡ mẫu $14$ mà Ví dụ 01.9 tính cho riêng $D_f$.
:::

::: hint Gợi ý 1
Phần (b). Khi $\hat r\le r^\star$, hàm $h_{\hat r}$ chỉ sai trên vành (annulus) $\{\hat r<\lVert x\rVert\le r^\star\}$, nơi nhãn thật là $1$.
:::

::: hint Gợi ý 2
Phần (b). Có thể không tồn tại bán kính nào mà vành tương ứng có khối lượng đúng bằng $\epsilon$. Đặt $G(r)=D_{\mathcal X}(\{r<\lVert x\rVert\le r^\star\})$ và $r_\epsilon=\inf\{r\in[0,r^\star]:\ G(r)\le\epsilon\}$, rồi chứng minh vành đóng (closed annulus) $\{r_\epsilon\le\lVert x\rVert\le r^\star\}$ có khối lượng ít nhất $\epsilon$.
:::

::: hint Gợi ý 3
Phần (b). Nếu một quan sát rơi vào vành đóng đó thì $\hat r\ge r_\epsilon$ và thuật toán thành công.
:::

::: solution Lời giải Bài tập 01.9
**(a)** Giả sử mẫu $s$ khớp với $h_r$: điểm nhãn 1 có chuẩn không quá $r$, điểm nhãn 0 có chuẩn lớn hơn $r$. Khi đó $\hat r\le r$; mọi điểm nhãn 1 có chuẩn không quá $\hat r$ và mọi điểm nhãn 0 có chuẩn lớn hơn $r\ge\hat r$, nên $L_s(h_{\hat r})=0$. Dưới $D$ khả thực, $Y=h_{r^\star}(X)$ hầu chắc chắn, nên hầu chắc chắn mẫu khớp với $h_{r^\star}$ và $\hat r\le r^\star$. Hàm $s\mapsto\hat r(s)$ là giá trị lớn nhất của hữu hạn hàm đo được $\lVert x_i\rVert\,\mathbb 1[y_i=1]$, nên $(s,x)\mapsto\lVert x\rVert-\hat r(s)$ đo được. Do đó $(s,(x,y))\mapsto\mathbb 1\big[\mathbb 1[\lVert x\rVert\le\hat r(s)]\ne y\big]$ đo được, và điều kiện của Định nghĩa 01.4 thỏa.

**(b)** Hầu chắc chắn, $h_{\hat r}$ và $h_{r^\star}$ khác nhau đúng trên vành $\{\hat r<\lVert x\rVert\le r^\star\}$, nơi nhãn thật là $1$, nên
$$
\begin{aligned}
&L_D\big(h_{\hat r}\big)=G(\hat r),\\
&G(r)=D_{\mathcal X}\big(\{r<\lVert x\rVert\le r^\star\}\big),
\end{aligned}
$$
với $r\in[0,r^\star]$. Hàm $G$ không tăng và liên tục phải (right-continuous): khi $r_n\downarrow r$, các vành $\{r_n<\lVert x\rVert\le r^\star\}$ tăng lên $\{r<\lVert x\rVert\le r^\star\}$, nên $G(r_n)\to G(r)$ theo tính liên tục của xác suất.

Nếu $G(0)\le\epsilon$ thì $L_D(h_{\hat r})\le G(0)\le\epsilon$ hầu chắc chắn. Giả sử $G(0)>\epsilon$ và đặt
$$
r_\epsilon=\inf\{r\in[0,r^\star]:G(r)\le\epsilon\}.
$$
Tập này khác rỗng vì $G(r^\star)=0$. Theo tính liên tục phải, $G(r_\epsilon)\le\epsilon$; vì $G(0)>\epsilon$, $r_\epsilon>0$ và $G(r)>\epsilon$ với mọi $r<r_\epsilon$. Khi $r\uparrow r_\epsilon$, các vành $\{r<\lVert x\rVert\le r^\star\}$ giảm xuống vành đóng $C=\{r_\epsilon\le\lVert x\rVert\le r^\star\}$, nên
$$
D_{\mathcal X}(C)=\lim_{r\uparrow r_\epsilon}G(r)\ge\epsilon .
$$

Thất bại nghĩa là $G(\hat r)>\epsilon$, kéo theo $\hat r<r_\epsilon$ vì $G$ không tăng và $G(r_\epsilon)\le\epsilon$. Nếu một quan sát $x_i$ rơi vào $C$ thì $\lVert x_i\rVert\le r^\star$, nên hầu chắc chắn $y_i=1$ và $\hat r\ge\lVert x_i\rVert\ge r_\epsilon$. Vậy, ngoài một biến cố có xác suất $0$, thất bại kéo theo không quan sát nào rơi vào $C$, và
$$
\begin{aligned}
&\Pr_S\big[L_D(h_{\hat r})>\epsilon\big]\\
&\quad\le\big(1-D_{\mathcal X}(C)\big)^m\\
&\quad\le(1-\epsilon)^m\le e^{-\epsilon m}\le\delta
\end{aligned}
$$
khi $m\ge\ln(1/\delta)/\epsilon$.

Với phân bố dồn vào điểm $u$, $G(r)=1$ khi $r<r^\star$ và $G(r^\star)=0$, nên không vành nào có khối lượng đúng bằng $\epsilon$; lập luận trên cho $r_\epsilon=r^\star$ và $D_{\mathcal X}(C)=1$.

**(c)** Cho $D$ khả thực với giả thuyết không lỗi $h_{t^\star}$. Hầu chắc chắn mẫu khớp với $h_{t^\star}$. Khi đó tập nghiệm ERM gồm các $t$ lớn hơn mọi $x$ có nhãn 0 và không vượt quá mọi $x$ có nhãn 1, nên $A_{\max}$ trả về $h_{\hat t}$ với $\hat t$ là $x$ nhỏ nhất có nhãn 1 (hoặc $K+1$). Như $A_\circ$, thuật toán chọn vùng dương nhỏ nhất khớp mẫu, nên $\hat t\ge t^\star$ và vùng lỗi là $\{t^\star,\ldots,\hat t-1\}$. Đặt $G(t)=D_{\mathcal X}(\{t^\star,\ldots,t-1\})$, không giảm theo $t$, nên $L_D(h_{\hat t})=G(\hat t)$.

Nếu $G(K+1)\le\epsilon$ thì không bao giờ thất bại. Nếu không, gọi $k$ là mức lớn nhất trong $\{t^\star,\ldots,K\}$ có $G(k)\le\epsilon$ (có $k$ vì $G(t^\star)=0$), và đặt $C=\{t^\star,\ldots,k\}$, khi đó $D_{\mathcal X}(C)=G(k+1)>\epsilon$. Nếu một quan sát rơi vào $C$, nó có nhãn 1 hầu chắc chắn, nên $\hat t\le k$ và $G(\hat t)\le G(k)\le\epsilon$. Phần còn lại giống hệt (b), và $m_{A_{\max}}(\epsilon,\delta)\le\lceil\ln(1/\delta)/\epsilon\rceil$.

Với $\epsilon=0{,}1$, $\delta=0{,}05$, cận là $\lceil10\ln20\rceil=\lceil29{,}96\rceil=30$, đúng con số ở §9 của ghi chú. Dưới $D_f$, $t^\star=3$ và $G(4)=0{,}2>0{,}1$, nên $C=\{3\}$ và xác suất thất bại là $0{,}8^m$; cỡ $14$ chỉ đủ cho phân bố đó, còn cận $30$ đúng cho mọi phân bố khả thực.

**Kiểm tra lại.** Tại $m=30$, $e^{-3}\approx0{,}0498\le0{,}05$; tại $m=29$, $e^{-2{,}9}\approx0{,}0550>0{,}05$, nên $30$ là cỡ mẫu nhỏ nhất mà cận $e^{-\epsilon m}$ bảo đảm. Lỗi thường gặp ở (b) là chọn bán kính có khối lượng vành đúng bằng $\epsilon$, như khi $D_{\mathcal X}$ liên tục; khi $D_{\mathcal X}$ có nguyên tử, bán kính đó có thể không tồn tại.
:::

### Bài tập 01.10 (Học PAC bất khả tri kéo theo học PAC khả thực; UML Bài tập 3.6)

**Mức độ:** chứng minh, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 4; quan hệ giữa hai định nghĩa học PAC.

::: exercise Bài tập 01.10
Cho lớp $\mathcal H$ các hàm phân lớp nhị phân trên $\mathcal X$ và hàm lỗi 0–1.

**(a)** Cho $A$ là thuật toán học PAC bất khả tri cho $\mathcal H$ (Định nghĩa 01.25) với hàm $M$. Chứng minh $A$ là thuật toán học PAC cho $\mathcal H$ trong trường hợp khả thực (Định nghĩa 01.18) với cùng hàm $M$. Suy ra mọi lớp học được PAC bất khả tri đều học được PAC.

**(b)** Chiều ngược lại sai ở mức thuật toán. Trên $\mathcal X=\{1,\ldots,5\}$ với lớp sáu hàm ngưỡng, thuật toán $A'$ trả về $h_{\hat t}$, trong đó $\hat t$ là giá trị $x$ nhỏ nhất có nhãn 1 trong mẫu, hoặc $6$ khi mẫu không có nhãn 1. Chứng minh $A'$ là thuật toán học PAC trong trường hợp khả thực. Với $D$ có $D_{\mathcal X}$ đều, $\eta(1)=\tfrac12$ và $\eta(x)=0$ khi $x\ge2$, chứng minh rằng với mọi $\epsilon\in(0;\,0{,}8)$ và mọi $m$,
$$
\begin{aligned}
&\Pr_S\Big[L_D(A'(S))\\
&\qquad\le\inf_{h\in\mathcal H}L_D(h)+\epsilon\Big]=0{,}9^m ,
\end{aligned}
$$
rồi kết luận $A'$ không là thuật toán học PAC bất khả tri.
:::

::: hint Gợi ý 1
Phần (a). Với $D$ khả thực, tính $\inf_{h\in\mathcal H}L_D(h)$. Hàm lỗi 0–1 bị chặn, nên mọi phân bố có rủi ro hữu hạn (Định nghĩa 01.3).
:::

::: hint Gợi ý 2
Phần (b). Trên mẫu khớp được bởi một hàm ngưỡng, $A'$ trả về đúng hàm mà $A_{\max}$ trả về; dùng Bài tập 01.9(c). Dưới phân bố có nhiễu, mỗi quan sát bằng $(1,1)$ với xác suất $0{,}1$.
:::

::: solution Lời giải Bài tập 01.10
**(a)** Hàm lỗi 0–1 nhận giá trị trong $[0,1]$, nên mọi phân bố có rủi ro hữu hạn trên $\mathcal H$, và họ phân bố của Định nghĩa 01.25 chứa mọi $D$ khả thực. Với $D$ khả thực, có $h^\star\in\mathcal H$ với $L_D(h^\star)=0$, nên $\inf_{h\in\mathcal H}L_D(h)=0$ và biến cố của Định nghĩa 01.25 là $\{L_D(A(S))\le\epsilon\}$, đúng biến cố của Định nghĩa 01.18. Vậy với mọi $\epsilon,\delta$, mọi $D$ khả thực và mọi $m\ge M(\epsilon,\delta)$, bất đẳng thức bất khả tri là bất đẳng thức khả thực. Trong cả hai định nghĩa, $A(S)\in\mathcal H$, nên không cần đổi thuật toán.

**(b)** *Trường hợp khả thực.* Trên mẫu khớp được bởi một hàm ngưỡng, tập nghiệm ERM gồm các $h_t$ với $t$ lớn hơn mọi $x$ có nhãn 0 và không vượt quá mọi $x$ có nhãn 1. Do đó $A_{\max}$ trả về đúng $h_{\hat t}$. Dưới $D$ khả thực, mẫu khớp được với xác suất $1$, nên $A'(S)=A_{\max}(S)$ hầu chắc chắn, và theo Bài tập 01.9(c), $A'$ thỏa Định nghĩa 01.18 với $M(\epsilon,\delta)=\lceil\ln(1/\delta)/\epsilon\rceil$.

*Trường hợp có nhiễu.* Dưới $D$ đã cho, nhãn 1 chỉ xuất hiện tại $x=1$. Hàm $h_6\equiv0$ có rủi ro $\Pr(Y=1)=0{,}2\cdot\tfrac12=0{,}1$. Với $2\le t\le5$, $h_t$ báo dương tính tại $6-t$ mức có $\eta=0$, nên $L_D(h_t)=0{,}1+0{,}2\,(6-t)\ge0{,}3$; $h_1$ có rủi ro $\Pr(Y=0)=0{,}9$. Vậy $\inf_{h\in\mathcal H}L_D(h)=0{,}1$.

Mỗi quan sát bằng $(1,1)$ với xác suất $0{,}1$. Nếu mẫu chứa một quan sát như vậy thì $\hat t=1$ và $L_D(A'(S))=0{,}9>0{,}1+\epsilon$ khi $\epsilon<0{,}8$. Nếu không, mẫu không có nhãn 1, $\hat t=6$ và $A'$ đạt đúng $0{,}1$. Xác suất thành công vì vậy bằng $0{,}9^m$. Với $\delta<0{,}1$ và mọi hàm $M$, tại $m=M(\epsilon,\delta)\ge1$ ta có $0{,}9^m\le0{,}9<1-\delta$, nên $A'$ không thỏa Định nghĩa 01.25.

**Kiểm tra lại.** Tại $m=1$, thuật toán thành công khi và chỉ khi quan sát duy nhất khác $(1,1)$, với xác suất $1-0{,}2\cdot\tfrac12=0{,}9$, khớp công thức. Phần (b) nói về một thuật toán, không về lớp: lớp hàm ngưỡng hữu hạn, và Bài 02 chứng minh ERM trên lớp hữu hạn là thuật toán học PAC bất khả tri.
:::

### Bài tập 01.11 (Tính tối ưu của quy tắc Bayes và so sánh thuật toán; UML Bài tập 3.8, thử thách)

**Mức độ:** chứng minh (bài thử thách). **Mục tiêu:** mục tiêu học tập 2; tính tối ưu của quy tắc Bayes và giới hạn của việc so sánh hai thuật toán.

::: exercise Bài tập 01.11
Cho $\mathcal X$ với một σ-đại số chứa mọi tập một điểm và $\mathcal Y=\{0,1\}$. Một *hàm dự đoán xác suất* (probabilistic label predictor) là một hàm đo được $h:\mathcal X\to[0,1]$; trên đầu vào $x$, nó tung một đồng xu độc lập, ra $1$ với xác suất $h(x)$, và dự đoán nhãn bằng kết quả đó. Hàm lỗi là $\ell(h,(x,y))=\lvert h(x)-y\rvert$; khi $h$ nhận giá trị trong $\{0,1\}$, đây là hàm lỗi 0–1. Xét các thuật toán học tất định với cỡ mẫu $m\ge1$ cố định, trả về hàm dự đoán xác suất. Ta nói *$A$ tốt hơn $B$ đối với $D$* nếu $L_D(A(s))\le L_D(B(s))$ với mọi mẫu $s\in(\mathcal X\times\{0,1\})^m$, kể cả những mẫu có xác suất $0$ dưới $D^m$.

**(a)** Chứng minh $\lvert h(x)-y\rvert$ là xác suất dự đoán sai trên $(x,y)$, và với mọi phân bố $D$ trên $\mathcal X\times\{0,1\}$, $L_D(h_{\mathrm{Bayes}})\le L_D(h)$ với mọi hàm dự đoán xác suất $h$.

**(b)** Chứng minh rằng với mọi $D$, tồn tại một thuật toán $A_D$ tốt hơn mọi thuật toán khác đối với $D$.

**(c)** Chứng minh rằng với mọi thuật toán $A$, tồn tại một phân bố $D$ và một thuật toán $B$ sao cho $A$ không tốt hơn $B$ đối với $D$.
:::

::: hint Gợi ý 1
Phần (a). Tính rủi ro có điều kiện tại một $x$ cố định như một hàm của giá trị $h(x)$.
:::

::: hint Gợi ý 2
Phần (a). Rủi ro có điều kiện là $h(x)(1-\eta(x))+(1-h(x))\eta(x)$, một hàm afin của $h(x)\in[0,1]$; giá trị nhỏ nhất của một hàm afin trên một đoạn đạt tại một đầu mút.
:::

::: hint Gợi ý 3
Phần (c). Cố định trước một mẫu $s_0$ và một điểm $x_0$, đọc giá trị $A(s_0)(x_0)$, rồi chọn $D$ dồn mọi khối lượng vào một điểm của $\mathcal X\times\{0,1\}$.
:::

::: solution Lời giải Bài tập 01.11
**(a)** Trên $(x,y)$, đồng xu cho dự đoán $1$ với xác suất $h(x)$. Nếu $y=0$, xác suất sai là $h(x)=\lvert h(x)-0\rvert$; nếu $y=1$, xác suất sai là $1-h(x)=\lvert h(x)-1\rvert$. Cho $\eta$ như trong Mệnh đề 01.23. Vì $h$ đo được, phép tính ở Bước 1 của Phụ lục B cho, hầu chắc chắn, $\mathbb E[\lvert h(X)-Y\rvert\mid X]=\varphi_X(h(X))$, trong đó
$$
\varphi_x(u)=\eta(x)+u\,\big(1-2\eta(x)\big),
$$
với $u\in[0,1]$. Hàm afin này đạt giá trị nhỏ nhất $\min\{\eta(x),1-\eta(x)\}$ tại $u=1$ khi $\eta(x)>\tfrac12$, tại $u=0$ khi $\eta(x)<\tfrac12$, và tại mọi $u$ khi $\eta(x)=\tfrac12$. Kiểm tra ba trường hợp cho
$$
\begin{aligned}
&\varphi_x(u)-\min\{\eta(x),1-\eta(x)\}\\
&\quad=\lvert2\eta(x)-1\rvert\\
&\qquad\cdot\lvert u-h_{\mathrm{Bayes}}(x)\rvert\ge0 .
\end{aligned}
$$
Thay $u=h(X)$ và lấy kì vọng theo tính chất tháp, ta được
$$
\begin{aligned}
&L_D(h)-L_D(h_{\mathrm{Bayes}})\\
&\quad=\mathbb E\Big[\lvert2\eta(X)-1\rvert\\
&\qquad\cdot\lvert h(X)-h_{\mathrm{Bayes}}(X)\rvert\Big]\\
&\quad\ge0,
\end{aligned}
$$
tổng quát hóa công thức ở đoạn "Tính không duy nhất" của Phụ lục B. Tung đồng xu không giảm được rủi ro.

**(b)** Đặt $A_D(s)=h_{\mathrm{Bayes}}$ của $D$ với mọi mẫu $s$. Đây là một ánh xạ hằng từ mẫu vào hàm phân lớp, nên là một thuật toán học tất định. Với mọi thuật toán $B$ và mọi mẫu $s$, theo (a), $L_D(A_D(s))=L_D(h_{\mathrm{Bayes}})\le L_D(B(s))$. Thuật toán $A_D$ không đọc $D$ khi chạy: $D$ chỉ dùng để chọn hằng $h_{\mathrm{Bayes}}$. Quy tắc "cho $D$, trả về quy tắc Bayes của $D$" thì nhận $D$ làm đầu vào, nên không phải một thuật toán học (§1).

**(c)** Cho $A$. Chọn một điểm $x_0\in\mathcal X$ và mẫu $s_0=((x_0,0),\ldots,(x_0,0))$. Đặt $u_0=A(s_0)(x_0)\in[0,1]$, rồi chọn $y_0=1$ nếu $u_0<\tfrac12$ và $y_0=0$ nếu $u_0\ge\tfrac12$. Lấy $D$ dồn mọi khối lượng vào điểm $(x_0,y_0)$, và $B$ là thuật toán luôn trả về hàm hằng $y_0$. Khi đó
$$
\begin{aligned}
L_D\big(A(s_0)\big)&=\lvert u_0-y_0\rvert\ge\tfrac12,\\
L_D\big(B(s_0)\big)&=0,
\end{aligned}
$$
nên $A$ không tốt hơn $B$ đối với $D$. Khi $y_0=1$, mẫu $s_0$ có xác suất $0$ dưới $D^m$; lời giải dùng đúng cách đọc "với mọi mẫu" của định nghĩa.

**Kiểm tra lại.** Thử (c) với $A=A_{D_0}$ của (b) cho một phân bố $D_0$ cố định. Với chính $D_0$, $A$ tốt hơn mọi thuật toán, nên lập luận "chọn một $D$ bất kì" không chứng minh được (c). Phép dựng ở (c) chọn $D$ theo giá trị $A(s_0)(x_0)=h^{D_0}_{\mathrm{Bayes}}(x_0)$ và đặt nhãn ngược lại tại $x_0$, nên $A$ thua $B$ trên $s_0$.
:::
