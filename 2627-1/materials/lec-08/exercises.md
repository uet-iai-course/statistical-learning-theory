# Bài tập Bài 08 — Tính ổn định của SGD và tổng quát hóa trong học sâu

Định nghĩa, kết quả và ví dụ được dẫn theo số hiệu của ghi chú Bài 08 và của các ghi chú Bài 01–07. Kí hiệu theo bảng kí hiệu chung và §1–§2 của ghi chú, gồm:

- **§1–§4.** $s=(z_1,\ldots,z_m)$: mẫu cố định; $s^{(i)}$, $z'$: mẫu lân cận và quan sát thay thế (Định nghĩa 06.9); $\xi=(i_1,\ldots,i_T)$: dãy chỉ số; $w_t$, $w'_t$: điểm lặp của hai lần chạy ghép cặp (coupled runs) trên $s$ và $s^{(i)}$, $\Delta_t=\lVert w_t-w'_t\rVert$ (Định nghĩa 08.2); $w_{T+1}$, $\bar w_T$: điểm lặp cuối và điểm lặp trung bình (Thuật toán 08.1); $\ell_{\mathrm H}$: hàm lỗi Huber (Ví dụ 08.1).
- **§2, §5–§7.** (S): hàm lỗi lồi và $\beta$-trơn trên $\mathbb R^p$; (G): $\lVert\nabla\ell(w,z)\rVert\le G$ trên $W$; $\Gamma_{\eta,z}(w)=w-\eta\nabla\ell(w,z)$: ánh xạ bước gradient (gradient step map); $\epsilon_{\mathrm{stab}}(m)$: hệ số ổn định (stability coefficient, Định nghĩa 06.9); $\sum_t\eta_t$: ngân sách độ dài bước (cumulative step-size budget).
- **§8–§9.** $R\ge\sup_{u\in W}\lVert w_1-u\rVert$; $\eta^*$, $T^*$: độ dài bước và số bước làm nhỏ nhất cận ghép (Hệ quả 08.8, Ví dụ 08.7); $\operatorname{opt}_s(w)=L_s(w)-\inf_WL_s$ (Định nghĩa 04.2); $F$, $F_*=\inf F$, $\sigma^2$: hàm mục tiêu, giá trị nhỏ nhất và cận phương sai của Mệnh đề 08.12.

Kí hiệu chỉ dùng trong một bài được đặt tên tại chỗ. Viết tắt: hạ gradient ngẫu nhiên (stochastic gradient descent, SGD). "Thí nghiệm mở đầu" là thí nghiệm hồi quy logistic của câu hỏi mở đầu, với giao thức ở Phụ lục F.

Cả tám bài là bài gốc của học phần; Bài tập 08.6 có phần tính bắt buộc trên số đã chạy và phần thực nghiệm tùy chọn. Không có bài từ giáo trình *Understanding Machine Learning* (Shalev-Shwartz và Ben-David, 2014): các bài phù hợp của chương 12–14 đã dùng ở Bài 05–06, và mục bài tập §20.9 không có bài về SGD hay tính ổn định.

## Bài tập gốc

### Bài tập 08.1 (Bất đẳng thức truy hồi và thừa số $1/m$)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 1 và 3; tìm nguồn gốc của thừa số $1/m$ qua hai biến thể của Thuật toán 08.1 và một ví dụ nhỏ.

::: exercise Bài tập 08.1
Giữ (S), (G), $W$ khác rỗng, đóng, lồi, $w_1=w'_1\in W$ tất định và $0<\eta_t\le2/\beta$ tất định. Cho $s$, $i$, $z'$ và $s^{(i)}$ như Định nghĩa 06.9.

**(a)** Xét *SGD theo lô nhỏ* (mini-batch SGD) với kích thước lô $b\ge1$. Ở bước $t$, thuật toán rút $b$ chỉ số $j_{t,1},\ldots,j_{t,b}$ đều trên $\{1,\ldots,m\}$, có hoàn lại, độc lập với nhau và với các bước trước. Sau đó nó đặt $w_{t+1}=\operatorname{proj}_W\big(w_t-\eta_t\bar g_t\big)$, trong đó $\bar g_t=\frac1b\sum_{r=1}^b\nabla\ell(w_t,z_{j_{t,r}})$. Hai lần chạy ghép cặp dùng chung khởi tạo, các $\eta_t$ và mọi chỉ số $j_{t,r}$; lần chạy trên $s^{(i)}$ dùng $z'$ ở mọi vị trí có $j_{t,r}=i$. Gọi $n_t$ là số vị trí $r$ có $j_{t,r}=i$. Chứng minh bất đẳng thức truy hồi (recurrence inequality) sau, với mọi giá trị của các chỉ số:
$$
\Delta_{t+1}\le\Delta_t+\frac{2G\eta_t\,n_t}b ,
$$
rồi suy ra $\mathbb E\Delta_{T+1}\le\frac{2G}m\sum_{t=1}^T\eta_t$ và một hệ số ổn định cho điểm lặp cuối. Cận có phụ thuộc $b$ không?

**(b)** Xét lại Thuật toán 08.1 ($b=1$), nhưng mỗi $i_t$ được rút độc lập theo một phân bố $(\rho_1,\ldots,\rho_m)$ trên $\{1,\ldots,m\}$, cố định trước khi thấy mẫu, với mọi $\rho_j>0$. Chỉ ra bước duy nhất của chứng minh Mệnh đề 08.5 thay đổi, và viết hệ số ổn định của điểm lặp cuối theo $\max_j\rho_j$. Tính hệ số này với $m=100$, $G=1$, $\eta_t=0{,}1$, $T=100$, khi $50$ quan sát có $\rho_j=0{,}015$ và $50$ quan sát có $\rho_j=0{,}005$, rồi so với rút đều. Vì sao phân bố $\rho$ phải được chọn trước khi thấy mẫu?

**(c)** Xét ví dụ Huber của Ví dụ 08.2: $s=(0,1,2,3)$, $s^{(4)}=(0,1,2,-3)$, $w_1=w'_1=0$, chỉ số rút đều có hoàn lại, nhưng với độ dài bước $\eta=1$. Tính $\mathbb E\Delta_2$ và $\mathbb E\Delta_3$ bằng cách liệt kê, so với cận của Mệnh đề 08.5(b), và chỉ ra các dãy $(i_1,i_2)$ có $\Delta_3$ nhỏ hơn ngặt cận của Mệnh đề 08.5(a) trên dãy đó.
:::

::: hint Gợi ý 1
Phần (a). Ở một bước của lô nhỏ, một số vị trí của lô dùng cùng quan sát cho hai lần chạy, các vị trí còn lại dùng $z_i$ và $z'$. So sánh với hai trường hợp trong chứng minh Mệnh đề 08.5. Phần (b). Tìm chỗ trong chứng minh dùng phân bố của $i_t$. Phần (c). Kiểm điều kiện độ dài bước, rồi nhóm $16$ dãy theo $i_1$ như Ví dụ 08.4.
:::

::: hint Gợi ý 2
Phần (a). Đặt $f_t(w)=\frac1b\sum_{r:\,j_{t,r}\ne i}\ell(w,z_{j_{t,r}})$. Hàm này lồi và $\beta$-trơn, nên Bổ đề 08.4(b) áp dụng cho $w\mapsto w-\eta_t\nabla f_t(w)$; phần còn lại của bước là $\frac{\eta_tn_t}b$ nhân một gradient tại $z_i$ hoặc $z'$. Mỗi vị trí của lô bằng $i$ với xác suất $1/m$. Phần (c). Với $\eta=1$, bước chung với $z=0$ đưa mọi $w\in[-1,1]$ về $0$.
:::

::: solution Lời giải Bài tập 08.1
**(a) SGD theo lô nhỏ.**

**Bước 1: tách một bước thành hai phần.** Các vị trí $r$ có $j_{t,r}\ne i$ dùng cùng quan sát $z_{j_{t,r}}$ cho hai lần chạy. Với $f_t$ như Gợi ý 2, $g_t=\nabla\ell(w_t,z_i)$ và $g'_t=\nabla\ell(w'_t,z')$, hai phép cập nhật là
$$
\begin{aligned}
w_{t+1}&=\operatorname{proj}_W\big(w_t-\eta_t\nabla f_t(w_t)\\
&\qquad-\tfrac{\eta_tn_t}b\,g_t\big),\\
w'_{t+1}&=\operatorname{proj}_W\big(w'_t-\eta_t\nabla f_t(w'_t)\\
&\qquad-\tfrac{\eta_tn_t}b\,g'_t\big).
\end{aligned}
$$

**Bước 2: phần chung không giãn ((S) và $\eta_t\le2/\beta$).** Hàm $f_t$ là tổng của $b-n_t$ hàm lồi nhân hệ số $\tfrac1b$, nên lồi. Gradient của nó là $\tfrac{b-n_t}b\beta$-Lipschitz, do đó $\beta$-Lipschitz, tức $f_t$ là $\beta$-trơn. Khi $n_t=b$, $f_t=0$. Theo Bổ đề 08.4(b), ánh xạ $\Gamma_t(w)=w-\eta_t\nabla f_t(w)$ không giãn.

**Bước 3: một bước (phép chiếu, bất đẳng thức tam giác, (G)).** Phép chiếu lên $W$ không giãn, nên
$$
\begin{aligned}
\Delta_{t+1}&\le\big\lVert\Gamma_t(w_t)-\Gamma_t(w'_t)\big\rVert\\
&\quad+\tfrac{\eta_tn_t}b\big(\lVert g_t\rVert+\lVert g'_t\rVert\big)\\
&\le\Delta_t+\tfrac{2G\eta_tn_t}b .
\end{aligned}
$$
Dòng cuối dùng Bước 2 và (G) tại $w_t,w'_t\in W$.

**Bước 4: cộng dọc quỹ đạo.** Vì $\Delta_1=0$, cộng bất đẳng thức của Bước 3 từ $t=1$ đến $T$ cho $\Delta_{T+1}\le\frac{2G}b\sum_t\eta_tn_t$.

**Bước 5: kì vọng.** Số $n_t$ là tổng của $b$ biến chỉ báo $\mathbb 1[j_{t,r}=i]$, mỗi biến có kì vọng $1/m$, nên $\mathbb En_t=b/m$. Theo tính tuyến tính của kì vọng,
$$
\begin{aligned}
\mathbb E\Delta_{T+1}&\le\frac{2G}b\sum_{t=1}^T\eta_t\,\frac bm\\
&=\frac{2G}m\sum_{t=1}^T\eta_t .
\end{aligned}
$$

**Bước 6: hệ số ổn định.** Bước 1–3 của chứng minh Định lý 08.6 chỉ dùng (G), tính lồi của $W$ và cận của $\mathbb E_\xi\Delta_{T+1}$, nên cho $\epsilon_{\mathrm{stab}}(m)=\frac{2G^2}m\sum_t\eta_t$. Cận không phụ thuộc $b$. Với $b=1$, $n_t=\mathbb 1[i_t=i]$ và Bước 3 là Mệnh đề 08.5(a). Thừa số $1/m$ là tỉ lệ kì vọng $\mathbb En_t/b$ của các vị trí trong lô dùng quan sát khác biệt.

**(b) Rút chỉ số không đều.**

**Bước 1: bước thay đổi.** Bước 1–3 của chứng minh Mệnh đề 08.5 đúng trên từng quỹ đạo và không dùng phân bố của $i_t$. Chỉ Bước 4 thay đổi: $\mathbb E\,\mathbb 1[i_t=i]=\rho_i$, nên $\mathbb E\Delta_{T+1}\le2G\rho_i\sum_t\eta_t$.

**Bước 2: hệ số ổn định.** Định nghĩa 06.9 đòi cận cho mọi chỉ số $i$, nên ta lấy $\max_j\rho_j$:
$$
\begin{aligned}
\epsilon_{\mathrm{stab}}(m)&=2G^2\Big(\max_j\rho_j\Big)\\
&\quad\times\sum_{t=1}^T\eta_t .
\end{aligned}
$$
Với rút đều, $\max_j\rho_j=1/m$ và ta được lại Định lý 08.6(b).

**Bước 3: thay số.** Hai nhóm cho tổng xác suất $50\cdot0{,}015+50\cdot0{,}005=1$, và $\max_j\rho_j=0{,}015$. Ngân sách là $0{,}1\cdot100=10$. Với rút không đều, hệ số ổn định là $2\cdot1\cdot0{,}015\cdot10=0{,}3$. Với rút đều, nó là $2\cdot1\cdot\tfrac1{100}\cdot10=0{,}2$. Cận tăng $m\max_j\rho_j=1{,}5$ lần, vì nó phải đúng cả khi quan sát bị thay là một quan sát có $\rho_j=0{,}015$, được rút với xác suất gấp $1{,}5$ lần $1/m$.

**Bước 4: vì sao chọn $\rho$ trước khi thấy mẫu.** Thuật toán phải có dạng $A(S;\xi)$ với $\xi$ độc lập với $S$ (Định nghĩa 05.18), và Định lý 06.10 dùng điều kiện này. Nếu $\rho$ phụ thuộc mẫu, chẳng hạn tỉ lệ với chuẩn gradient trên $s$, thì $\xi$ có hai phân bố khác nhau trên $s$ và $s^{(i)}$. Khi đó không thể cho hai lần chạy dùng chung $\xi$ mà mỗi lần chạy vẫn giữ đúng phân bố của nó.

**(c) Ví dụ Huber với $\eta=1$.**

**Bước 1: điều kiện và cận.** Theo Ví dụ 08.1, $\beta=G=1$, nên $\eta=1\le2/\beta=2$. Cận của Mệnh đề 08.5(b) là $\frac{2G\eta T}m=\frac T2$. Ở mỗi bước, $w_{t+1}=w_t-\partial_w\ell_{\mathrm H}(w_t,z)$, với đạo hàm là $w_t-z$ cắt vào $[-1,1]$.

**Bước 2: $T=1$.** Nếu $i_1\ne4$, hai lần chạy dùng cùng quan sát và $\Delta_2=0$. Nếu $i_1=4$, ta có $w_2=0-(-1)=1$ và $w'_2=0-1=-1$, nên $\Delta_2=2$. Do đó $\mathbb E\Delta_2=\tfrac24=\tfrac12$, đúng bằng cận.

**Bước 3: $T=2$, nhóm $i_1\ne4$ ($12$ dãy).** Bước đầu cho $w_2=w'_2$, bằng $0$ khi $i_1=1$ và bằng $1$ khi $i_1\in\{2,3\}$. Nếu $i_2\ne4$, $\Delta_3=0$. Nếu $i_2=4$, ta có $w_2-3\le-2$ và $w_2+3\ge3$, nên hai đạo hàm là $-1$ và $1$, và $\Delta_3=2$. Tổng của nhóm là $3\cdot2=6$.

**Bước 4: $T=2$, nhóm $i_1=4$ ($4$ dãy).** Ta có $w_2=1$, $w'_2=-1$. Bảng tính bước thứ hai.

| $i_2$ | $w_3$ | $w'_3$ | $\Delta_3$ |
|---|---|---|---|
| $1$ | $0$ | $0$ | $0$ |
| $2$ | $1$ | $0$ | $1$ |
| $3$ | $2$ | $0$ | $2$ |
| $4$ | $2$ | $-2$ | $4$ |

Chẳng hạn với $i_2=2$: $w_2-1=0$ cho $w_3=1$, còn $w'_2-1=-2$ bị cắt thành $-1$, nên $w'_3=-1+1=0$. Tổng của nhóm là $0+1+2+4=7$.

**Bước 5: kì vọng.**
$$
\begin{aligned}
\mathbb E\Delta_3&=\frac{6+7}{16}=\frac{13}{16}\\
&=0{,}8125<1 .
\end{aligned}
$$

**Bước 6: các dãy có phần hụt.** Theo Mệnh đề 08.5(a), trên mỗi dãy $\Delta_3\le2\big(\mathbb 1[i_1=4]+\mathbb 1[i_2=4]\big)$. Mọi bước khác biệt ở trên làm $\Delta$ tăng đúng $2=2G\eta$. Chỉ hai dãy cho $\Delta_3$ nhỏ hơn cận trên quỹ đạo:

- **$(4,1)$.** Bước chung với $z=0$ đưa cả $1$ và $-1$ về $0$, vì trên $[-1,1]$ ánh xạ bước là $w\mapsto w-w=0$ (hệ số giãn $\lvert1-\eta\rvert=0$, Ví dụ 08.3). Phần hụt là $2$.
- **$(4,2)$.** Bước chung với $z=1$ giữ $w_2=1$ và đưa $w'_2=-1$ về $0$. Phần hụt là $1$.

Tổng phần hụt trên $16$ dãy là $3$; chia cho $16$, ta được $\tfrac3{16}=1-\tfrac{13}{16}$, đúng bằng hiệu giữa cận và $\mathbb E\Delta_3$.

**Kiểm tra lại.** Cùng phép liệt kê với $\eta=\tfrac12$ cho $\mathbb E\Delta_3=\tfrac{29}{64}$, khớp Ví dụ 08.4.
:::

### Bài tập 08.2 (Ngân sách độ dài bước của ba lịch độ dài bước)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 3 và 4; so cận ổn định với cận tối ưu của ba lịch độ dài bước (step-size schedule).

::: exercise Bài tập 08.2
Xét hồi quy logistic với $\lVert x\rVert\le1$ trên toàn $\mathcal X$ (Ví dụ 08.5: $G=1$, $\beta=\tfrac14$), $m=10^4$ quan sát, $W$ là quả cầu tâm $0$ bán kính $5$ và $w_1=0$. Thuật toán 08.1 chạy với một trong ba lịch: $\eta_t=0{,}05$; $\eta_t=5/t$; $\eta_t=5/\sqrt t$.

**(a)** Chứng minh bằng cách so sánh tổng với tích phân rằng với mọi $T\ge1$,
$$
\begin{aligned}
\ln(T+1)&\le\sum_{t=1}^T\frac1t\le1+\ln T,\\
\sum_{t=1}^T\frac1{\sqrt t}&\le2\sqrt T-1 .
\end{aligned}
$$

**(b)** Kiểm điều kiện độ dài bước của Định lý 08.6 cho ba lịch. Với $T=10^4$ và $T=10^5$, tính ngân sách độ dài bước và cận của Định lý 08.6 cho khoảng cách tổng quát hóa kì vọng (expected generalization gap) của $w_{T+1}$. Tính trước hết bằng (a), rồi bằng các giá trị tính bằng máy $\sum_{t\le10^4}1/t\approx9{,}7876$, $\sum_{t\le10^5}1/t\approx12{,}0901$, $\sum_{t\le10^4}t^{-1/2}\approx198{,}5446$, $\sum_{t\le10^5}t^{-1/2}\approx630{,}9968$.

**(c)** Nhận xét 05.17 (đọc thêm của Bài 05) chặn độ chênh tối ưu $\mathbb E_\xi L_s(\tilde w_T)-L_s(u)$ của trung bình có trọng số $\tilde w_T=\sum_t\eta_tw_t/\sum_t\eta_t$; ở đây gọi vế phải là *cận tối ưu*. Với mọi $u\in W$ và $R\ge\lVert w_1-u\rVert$,
$$
\begin{aligned}
&\mathbb E_\xi L_s(\tilde w_T)-L_s(u)\\
&\le\frac{R^2+G^2\sum_t\eta_t^2}{2\sum_t\eta_t}.
\end{aligned}
$$
Kiểm giả thiết của nhận xét với $F=L_s$ và oracle rút đều một quan sát. Tính vế phải cho ba lịch với $T=10^4$ và $T=10^5$, dùng thêm $\sum_{t\le10^4}1/t^2\approx1{,}6448$ và $\sum_{t\le10^5}1/t^2\approx1{,}6449$. Giải thích vì sao lịch $5/t$ có cận ổn định nhỏ nhất nhưng cận tối ưu chỉ giảm như $1/\ln T$.

Cận ở (b) nói về $w_{T+1}$, cận ở (c) nói về $\tilde w_T$, nên không cộng được hai cận này thành một cận rủi ro.
:::

::: hint Gợi ý 1
Phần (a). Hàm $x\mapsto1/x$ và $x\mapsto1/\sqrt x$ giảm trên $(0,\infty)$; đặt mỗi số hạng của tổng cạnh tích phân trên một đoạn độ dài $1$. Phần (b). Định lý 08.6(c) cho cận $\frac{2G^2}m\sum_t\eta_t$. Phần (c). Với $u\in W$, $\lVert w_1-u\rVert\le5$.
:::

::: hint Gợi ý 2
Phần (a). Với $t\ge1$, $\int_t^{t+1}dx/x\le1/t$; với $t\ge2$, $1/t\le\int_{t-1}^tdx/x$ và $1/\sqrt t\le\int_{t-1}^tx^{-1/2}dx$. Phần (c). Với lịch $5/t$, $\sum_t\eta_t^2=25\sum_t1/t^2\le25\cdot2$, còn $\sum_t\eta_t\ge5\ln(T+1)$.
:::

::: solution Lời giải Bài tập 08.2
**(a) So sánh với tích phân.**

**Bước 1: cận dưới của tổng điều hòa.** Với $t\ge1$ và $x\in[t,t+1]$, $1/x\le1/t$, nên $\int_t^{t+1}dx/x\le1/t$. Cộng từ $t=1$ đến $T$:
$$
\ln(T+1)=\int_1^{T+1}\frac{dx}x\le\sum_{t=1}^T\frac1t .
$$

**Bước 2: cận trên của tổng điều hòa.** Với $t\ge2$ và $x\in[t-1,t]$, $1/t\le1/x$, nên $1/t\le\int_{t-1}^tdx/x$. Giữ riêng số hạng $t=1$:
$$
\begin{aligned}
\sum_{t=1}^T\frac1t&\le1+\int_1^T\frac{dx}x\\
&=1+\ln T .
\end{aligned}
$$

**Bước 3: tổng của $t^{-1/2}$.** Cùng lập luận với $x\mapsto x^{-1/2}$:
$$
\begin{aligned}
\sum_{t=1}^T\frac1{\sqrt t}&\le1+\int_1^Tx^{-1/2}dx\\
&=1+2\sqrt T-2\\
&=2\sqrt T-1 .
\end{aligned}
$$

**(b) Ngân sách và cận ổn định.**

**Bước 1: điều kiện.** Điều kiện của Định lý 08.6 là $\eta_t\le2/\beta=8$. Ba lịch có $\eta_t\le0{,}05$, $\eta_t\le5$ và $\eta_t\le5$, nên đều thỏa. Các giả thiết khác thỏa theo Ví dụ 08.5; $W$ là quả cầu nên đóng, lồi.

**Bước 2: ngân sách.** Lịch hằng có ngân sách $0{,}05T$, tức $500$ và $5000$. Theo (a), hai lịch còn lại có
$$
\begin{aligned}
5\sum_t\tfrac1t&\le5(1+\ln T),\\
5\sum_t\tfrac1{\sqrt t}&\le5(2\sqrt T-1).
\end{aligned}
$$
Bảng ghi ngân sách của hai lịch này. Mỗi ô ghi giá trị tính bằng máy (từ các tổng đã cho), rồi cận theo (a), làm tròn lên.

| Lịch | $T=10^4$ | $T=10^5$ |
|---|---|---|
| $5/t$ | $48{,}94$; $51{,}06$ | $60{,}45$; $62{,}57$ |
| $5/\sqrt t$ | $992{,}72$; $995$ | $3154{,}98$; $3157{,}28$ |

**Bước 3: cận ổn định.** Với $G=1$ và $m=10^4$, cận là $2\sum_t\eta_t/10^4$. Bảng ghi cận theo giá trị tính bằng máy (làm tròn lên); cận theo (a) ghi sau dấu chấm phẩy.

| Lịch | $T=10^4$ | $T=10^5$ |
|---|---|---|
| $0{,}05$ | $0{,}1$ | $1$ |
| $5/t$ | $0{,}0098$; $0{,}0103$ | $0{,}0121$; $0{,}0126$ |
| $5/\sqrt t$ | $0{,}1986$; $0{,}199$ | $0{,}6310$; $0{,}6315$ |

Lịch hằng có cận tăng tuyến tính theo $T$; lịch $5/t$ có cận tăng như $\ln T$; lịch $5/\sqrt t$ có cận tăng như $\sqrt T$.

**(c) Cận tối ưu.**

**Bước 1: giả thiết của Nhận xét 05.17.** Hàm $L_s$ lồi theo (S) và $W$ đóng, lồi, nên (C) đúng. Oracle rút đều một quan sát không chệch cho $\nabla L_s$ và thỏa (G2) với $G=1$ theo (G), như Bước 1 của chứng minh Hệ quả 05.19. Với $u\in W$, $\lVert w_1-u\rVert\le5$, nên lấy $R=5$.

**Bước 2: tổng các bình phương.** Lịch hằng có $\sum_t\eta_t^2=0{,}0025T$, tức $25$ và $250$. Lịch $5/t$ có $25\cdot1{,}6448\approx41{,}12$ và $25\cdot1{,}6449\approx41{,}12$. Lịch $5/\sqrt t$ có $25\sum_t1/t$, tức $244{,}69$ và $302{,}25$.

**Bước 3: thay số.** Với $T=10^4$:
$$
\begin{aligned}
0{,}05:&\ \tfrac{25+25}{2\cdot500}=0{,}05,\\
5/t:&\ \tfrac{25+41{,}12}{2\cdot48{,}94}\le0{,}6756,\\
5/\sqrt t:&\ \tfrac{25+244{,}69}{2\cdot992{,}72}\le0{,}1359 .
\end{aligned}
$$
Với $T=10^5$:
$$
\begin{aligned}
0{,}05:&\ \tfrac{25+250}{2\cdot5000}=0{,}0275,\\
5/t:&\ \tfrac{25+41{,}12}{2\cdot60{,}45}\le0{,}5470,\\
5/\sqrt t:&\ \tfrac{25+302{,}25}{2\cdot3154{,}98}\le0{,}0519 .
\end{aligned}
$$

**Bước 4: lịch $5/t$.** Như (a), $\sum_t1/t^2\le1+\int_1^\infty x^{-2}dx=2$, nên $\sum_t\eta_t^2\le50$. Theo (a), ngân sách ít nhất $5\ln(T+1)$. Do đó vế phải của (c) không quá
$$
\frac{25+50}{10\ln(T+1)}=\frac{7{,}5}{\ln(T+1)},
$$
và vế phải cũng ít nhất $\frac{25}{10(1+\ln T)}$, nên nó giảm như $1/\ln T$. Ngân sách chỉ tăng như $\ln T$. Nó nằm ở tử số của cận ổn định, nên cận này nhỏ; nó nằm ở mẫu số của cận tối ưu, nên số hạng $R^2/(2\sum_t\eta_t)$ giảm chậm.

**Bước 5: đọc hai bảng.** Với $T=10^4$, ba lịch cho các cặp (ổn định; tối ưu) là $(0{,}1;\,0{,}05)$, $(0{,}0098;\,0{,}6756)$ và $(0{,}1986;\,0{,}1359)$. Lịch có cận ổn định nhỏ có cận tối ưu lớn, và ngược lại. Hai cận nói về hai đầu ra khác nhau, nên ta chỉ so sánh chúng, không cộng chúng; cận ghép hợp lệ cho một đầu ra là Hệ quả 08.8.

**Kiểm tra lại.** Với lịch hằng và $T=10^4$, $\eta=0{,}05=R/(G\sqrt T)$, và cận tối ưu $0{,}05$ bằng $RG/\sqrt T$, khớp Hệ quả 05.15. Cận ổn định $0{,}1$ với $\eta=0{,}05$, $T=10^4$, $m=10^4$ bằng $100$ lần cận $0{,}001$ của Ví dụ 08.5, Bước 2, vì $m$ nhỏ hơn $100$ lần.
:::

### Bài tập 08.3 (Bước chứng minh không còn đúng khi bỏ tính lồi)

**Mức độ:** chứng minh, kiểm tra giả thiết, tính toán. **Mục tiêu:** mục tiêu học tập 2 và 5; chứng minh tính không giãn trong một trường hợp riêng, chỉ chỗ tính lồi đi vào chứng minh, và đo khoảng cách khi bỏ nó.

::: exercise Bài tập 08.3
**(a)** Xét hàm lỗi Huber của Ví dụ 08.1 ($\beta=1$) với $z$ cố định, và đặt $d(w)=\partial_w\ell_{\mathrm H}(w,z)$. Không dùng Bổ đề 08.4, chứng minh trực tiếp rằng với $0\le\eta\le2$ và mọi $u,v\in\mathbb R$,
$$
\lvert\Gamma_{\eta,z}(u)-\Gamma_{\eta,z}(v)\rvert\le\lvert u-v\rvert,
$$
chỉ dùng hai tính chất của $d$: không giảm và $1$-Lipschitz. Tính chất nào đến từ tính lồi? Nêu một cặp $u,v$ cho thấy kết luận sai khi $\eta=3$.

Các ý (b)–(e) dùng hàm lỗi cosin của Ví dụ 08.8, $\ell(w,z)=1+\cos(w-z)$ trên $W=\mathbb R$, với $\beta=G=1$.

**(b)** Đặt $f(w)=\ell(w,0)=1+\cos w$. Tìm $u,v$ sao cho bất đẳng thức của tính đồng bức (co-coercivity, Định nghĩa 08.3) với $\beta=1$ sai. Trong chứng minh Bổ đề 08.4(a) ở Phụ lục A, với $u=0$, chỉ ra dòng không còn đúng, và kiểm bằng số rằng bất đẳng thức then chốt của chứng minh sai tại $u=0$, $v=\pi/2$. Bước 1 của chứng minh đó còn đúng không?

**(c)** Liệt kê các bước của chứng minh Mệnh đề 08.5 và Định lý 08.6. Với mỗi bước, nêu nó dùng tính lồi của hàm lỗi, tính lồi của $W$, (G) hay điều kiện độ dài bước, và bước nào không còn đúng với hàm lỗi cosin.

**(d)** Trong Ví dụ 08.8 ($m=100$, mọi $z_j=0$, $z'=0{,}01$, $\eta=0{,}1$, $i_1=i$ và $i_t\ne i$ với $t\ge2$), ta có $w_t=0$ với mọi $t$, nên $\Delta_t=\lvert w'_t\rvert$, và $\Delta_2=0{,}1\sin0{,}01$. Chứng minh rằng nếu $\Delta_t\le\tfrac12$ thì
$$
\begin{aligned}
1+0{,}1\cos\tfrac12&\le\frac{\Delta_{t+1}}{\Delta_t}\le1{,}1 .
\end{aligned}
$$
Suy ra chỉ số $t$ đầu tiên có $\Delta_t>\tfrac12$ nằm trong một khoảng, và tính khoảng đó.

**(e)** Mệnh đề 08.10(c) với $\beta=G=1$, $m=100$, $T=100$ cho khoảng $275{,}6$ khi $\eta_t=0{,}1$ (đoạn sau Mệnh đề 08.10). Tính một cận trên của vế phải với $\eta_t=0{,}1/t$, dùng $\prod_{k=t+1}^T(1+\beta c/k)\le(T/t)^{\beta c}$ và so sánh tổng với tích phân. So hai kết quả với cận lồi $\frac{2G}m\sum_t\eta_t$ của cùng hai lịch.
:::

::: hint Gợi ý 1
Phần (a). Viết $\Gamma_{\eta,z}(u)-\Gamma_{\eta,z}(v)$ theo $u-v$ và $d(u)-d(v)$. Phần (b). Vế trái của bất đẳng thức đồng bức có thể âm khi hàm không lồi. Bước 2 của Phụ lục A khẳng định một điểm là cực tiểu toàn cục của hàm phụ $q_u$; tìm $q_0$. Phần (d). Ánh xạ bước ở các bước chung là $\varphi(w)=w+0{,}1\sin w$, với $\varphi(0)=0$; dùng định lý giá trị trung bình.
:::

::: hint Gợi ý 2
Phần (a). Với $u>v$, đặt $\delta=d(u)-d(v)$; hai tính chất cho $0\le\delta\le u-v$. Phần (b). Lấy $u=0$, $v=\tfrac12$; $q_0=f$ vì $f'(0)=0$. Phần (d). Với $w\in[-\tfrac12,0)$, $\varphi(w)=\varphi'(\zeta)w$ với $\zeta\in(w,0)$ và $\varphi'(\zeta)=1+0{,}1\cos\zeta$. Cận trên $1{,}1$ đúng ở mọi bước, cận dưới chỉ khi $\Delta_t\le\tfrac12$. Phần (e). $\sum_{t=1}^{100}t^{-1{,}1}\le1+\int_1^{100}x^{-1{,}1}dx$.
:::

::: solution Lời giải Bài tập 08.3
**(a) Bước gradient của hàm lỗi Huber.**

**Bước 1: hai tính chất của $d$.** Theo Ví dụ 08.1, $d(w)$ là $w-z$ cắt vào $[-1,1]$. Hàm này không giảm, vì $\ell_{\mathrm H}(\cdot,z)$ lồi, và $1$-Lipschitz, vì $\ell_{\mathrm H}(\cdot,z)$ là $1$-trơn.

**Bước 2: hiệu hai ảnh.** Khi $u=v$, hai vế bằng $0$. Không mất tổng quát, giả sử $u>v$, và đặt $\delta=d(u)-d(v)$. Tính không giảm cho $\delta\ge0$; tính $1$-Lipschitz cho $\delta\le u-v$. Với $\Gamma=\Gamma_{\eta,z}$,
$$
\Gamma(u)-\Gamma(v)=(u-v)-\eta\delta .
$$

**Bước 3: chặn hai phía.** Vì $0\le\delta\le u-v$ và $\eta\ge0$,
$$
\begin{aligned}
(1-\eta)(u-v)&\le\Gamma(u)-\Gamma(v)\\
&\le u-v .
\end{aligned}
$$
Với $0\le\eta\le2$, $\lvert1-\eta\rvert\le1$, nên $\lvert\Gamma(u)-\Gamma(v)\rvert\le u-v$.

**Bước 4: vai trò của hai giả thiết.** Tính không giảm của $d$, tức tính lồi, cho cận trên $u-v$; nếu $\delta$ có thể âm, hiệu có thể vượt $u-v$, như hàm lõm của Ví dụ 08.3. Điều kiện $\eta\le2=2/\beta$ cho cận dưới. Với $\eta=3$, $z=0$, $u=0{,}2$ và $v=-0{,}2$, ánh xạ bước trên $[-1,1]$ là $w\mapsto w-3w=-2w$, nên $\lvert\Gamma(u)-\Gamma(v)\rvert=0{,}8=2\lvert u-v\rvert$.

**(b) Tính đồng bức và Phụ lục A.**

**Bước 1: bất đẳng thức đồng bức sai.** Ta có $f'(w)=-\sin w$. Với $u=0$, $v=\tfrac12$, vế trái của bất đẳng thức đồng bức là
$$
\begin{aligned}
&\big(f'(\tfrac12)-f'(0)\big)\cdot\tfrac12\\
&=-\tfrac12\sin\tfrac12\approx-0{,}2397,
\end{aligned}
$$
còn vế phải là $\big(f'(\tfrac12)-f'(0)\big)^2=\sin^2\tfrac12\approx0{,}2298$. Vế trái âm, nên nhỏ hơn vế phải; $f'$ không $1$-đồng bức.

**Bước 2: dòng không còn đúng.** Với $u=0$, $f'(0)=0$, nên hàm phụ là $q_0(v)=f(v)-0\cdot v=1+\cos v$ và $q_0'(0)=0$. Bước 2 của Phụ lục A dùng bất đẳng thức dưới gradient của hàm lồi để suy ra $u$ là điểm cực tiểu toàn cục của $q_u$ từ $\nabla q_u(u)=0$. Ở đây $q_0(0)=2$ là giá trị lớn nhất của $q_0$, còn cực tiểu toàn cục là $q_0(\pi)=0$. Dòng này sai, và đây là dòng duy nhất của Phụ lục A dùng tính lồi.

**Bước 3: bất đẳng thức then chốt sai.** Với $u=0$, $v=\pi/2$:
$$
\begin{aligned}
&f(v)-f(u)=1-2=-1,\\
&f'(u)(v-u)\\
&\quad+\tfrac12\big(f'(v)-f'(u)\big)^2\\
&=0+\tfrac12(-1)^2=\tfrac12 .
\end{aligned}
$$
Ta có $-1<\tfrac12$, nên bất đẳng thức then chốt sai.

**Bước 4: Bước 1 của Phụ lục A.** Cận trên bậc hai (còn gọi là bổ đề hạ) chỉ dùng tính $1$-trơn, nên vẫn đúng. Chẳng hạn với $u=0$, $v=\pi/2$: $f(v)-f(u)-f'(u)(v-u)=-1\le\tfrac12(\pi/2)^2$.

**(c) Vai trò của từng giả thiết.** Bảng ghi giả thiết mà mỗi bước dùng.

| Bước | Dùng | Với cosin |
|---|---|---|
| 08.5, Bước 1 | lồi, trơn, $\eta_t\le2/\beta$, $W$ lồi | sai |
| 08.5, Bước 2 | (G), $W$ lồi | đúng |
| 08.5, Bước 3 | không | đúng |
| 08.5, Bước 4 | xác suất biên của $i_t$ | đúng |
| 08.6, Bước 1 | (G), $W$ lồi | đúng |
| 08.6, Bước 2 | 08.5(b) | sai |
| 08.6, Bước 3 | ghép cặp | đúng |
| 08.6, Bước 4 | (G), $W$ lồi, (T2) | đúng |
| 08.6, Bước 5 | (T1), phần (b) | sai |

Hai dòng "sai" của Định lý 08.6 chỉ sai vì chúng dùng Mệnh đề 08.5(b) hoặc kết luận của Bước 2.

Tính lồi của hàm lỗi chỉ đi vào qua Bổ đề 08.4(a), ở Bước 1 của Mệnh đề 08.5. Với hàm lỗi cosin, $W=\mathbb R$ lồi và (G) đúng với $G=1$, nên chỉ bước chung không còn đúng.

**(d) Khoảng cách tăng theo hàm mũ.**

**Bước 1: ánh xạ bước.** Với $z=0$, đạo hàm của hàm lỗi là $-\sin w$, nên bước chung là $\varphi(w)=w+0{,}1\sin w$. Ta có $\varphi(0)=0$ và $\varphi'(w)=1+0{,}1\cos w\in[0{,}9;\,1{,}1]$.

**Bước 2: dấu của $w'_t$.** $w'_2=0{,}1\sin(-0{,}01)<0$. Hàm $\varphi$ tăng, $\varphi(-\pi)=-\pi$, và $\varphi(w)<w$ khi $w\in(-\pi,0)$. Do đó mọi $w'_t$ với $t\ge2$ nằm trong $(-\pi,0)$, và $\Delta_t=-w'_t$.

**Bước 3: hai cận cho một bước.** Theo định lý giá trị trung bình, $\varphi(w'_t)=\varphi'(\zeta)w'_t$ với $\zeta$ nằm giữa $w'_t$ và $0$, nên $\Delta_{t+1}=\varphi'(\zeta)\Delta_t$. Luôn có $\varphi'(\zeta)\le1{,}1$. Khi $\Delta_t\le\tfrac12$, ta có $\lvert\zeta\rvert\le\tfrac12$ và $\cos\zeta\ge\cos\tfrac12$, nên $\varphi'(\zeta)\ge1+0{,}1\cos\tfrac12\approx1{,}08776$.

**Bước 4: chặn chỉ số đầu tiên.** Đặt $\tau$ là chỉ số đầu tiên có $\Delta_\tau>\tfrac12$, và $\Delta_2=0{,}1\sin0{,}01\approx0{,}00099998$, nên $\ln(0{,}5/\Delta_2)\approx6{,}2146$.

- **Cận dưới của $\tau$.** Theo Bước 3, $\Delta_t\le1{,}1^{t-2}\Delta_2$ với mọi $t$. Nếu $\Delta_\tau>\tfrac12$ thì $(\tau-2)\ln1{,}1>6{,}2146$, tức $\tau-2>65{,}2$, nên $\tau\ge68$.
- **Cận trên của $\tau$.** Nếu $\Delta_t\le\tfrac12$ với mọi $t\le76$, Bước 3 cho $\Delta_{76}\ge1{,}08776^{74}\Delta_2\approx0{,}505>\tfrac12$, mâu thuẫn. Do đó $\tau\le76$.

Tính bằng máy cho $\tau=68$, đúng bằng cận dưới.

**Bước 5: ý nghĩa.** Mệnh đề 08.10(a) cho hệ số giãn trên $1+\beta\eta=1{,}1$; Bước 3 cho hệ số giãn dưới $1{,}0878$ trên đoạn $\lvert w\rvert\le\tfrac12$. Trên quỹ đạo này, khoảng cách tăng ít nhất theo cơ số $1{,}0878$ mỗi bước cho đến khi vượt $\tfrac12$, gần cơ số $1{,}1$ của cận; tốc độ hàm mũ của Mệnh đề 08.10 xảy ra trên một quỹ đạo cụ thể.

**(e) Độ dài bước hằng và độ dài bước giảm.**

**Bước 1: cận với $\eta_t=0{,}1/t$.** Với $c=0{,}1$, $\beta c=0{,}1$, và theo bất đẳng thức tích đã cho,
$$
\begin{aligned}
\mathbb E\Delta_{T+1}&\le\frac{2}{100}\sum_{t=1}^{100}\frac{0{,}1}t\\
&\qquad\times\Big(\frac{100}t\Big)^{0{,}1}\\
&=0{,}002\cdot100^{0{,}1}\\
&\qquad\times\sum_{t=1}^{100}t^{-1{,}1}.
\end{aligned}
$$

**Bước 2: so sánh với tích phân.** Như Bài tập 08.2(a),
$$
\begin{aligned}
\sum_{t=1}^{100}t^{-1{,}1}&\le1+\int_1^{100}x^{-1{,}1}dx\\
&=1+10\big(1-100^{-0{,}1}\big)\\
&\approx4{,}6904 .
\end{aligned}
$$
Với $100^{0{,}1}\approx1{,}5849$, vế phải không quá $0{,}002\cdot1{,}5849\cdot4{,}6904\le0{,}0149$. Tính tổng bằng máy ($\approx4{,}2780$) cho $0{,}0136$.

**Bước 3: so với cận lồi.** Ngân sách của lịch $0{,}1/t$ là $0{,}1\sum_{t\le100}1/t\approx0{,}5187$, nên cận lồi là $\frac2{100}\cdot0{,}5187\approx0{,}0104$. Ngân sách của lịch hằng là $10$, nên cận lồi là $0{,}2$. Bảng so sánh:

| Lịch | Cận lồi | Cận không lồi |
|---|---|---|
| $0{,}1$ | $0{,}2$ | $\approx275{,}6$ |
| $0{,}1/t$ | $\approx0{,}0104$ | $\le0{,}0149$ |

**Bước 4: đọc bảng.** Thừa số $\prod_{k>t}(1+\beta\eta_k)$ không quá $e^{\beta\sum_k\eta_k}$, tức hàm mũ của ngân sách. Với lịch hằng, $e^{10}\approx22\,026$; với lịch $0{,}1/t$, $e^{0{,}5187}\approx1{,}68$. Không có tính lồi, cận nhân thêm một thừa số hàm mũ của ngân sách, nên cận chỉ dùng được khi ngân sách nhỏ, như với độ dài bước giảm.

**Kiểm tra lại.** Ở (a), hệ số $2$ khi $\eta=3$ khớp cột Huber của Ví dụ 08.3. Ở (d), $\Delta_3/\Delta_2\approx1{,}1000$, khớp Bước 4 của Ví dụ 08.8, và nằm trong $[1{,}0878;\,1{,}1]$. Giá trị $\Delta_{58}\approx0{,}207$ của Ví dụ 08.8 nhỏ hơn $\tfrac12$, phù hợp với $\tau=68$.
:::

### Bài tập 08.4 (Gradient nhỏ, rủi ro thực nghiệm nhỏ và rủi ro kì vọng nhỏ)

**Mức độ:** khái niệm, chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 5; tách tính dừng (stationarity), sai số tối ưu thực nghiệm và rủi ro kì vọng, và nối mỗi đại lượng với bảo đảm chặn nó.

::: exercise Bài tập 08.4
**(a)** Xét mẫu của Ví dụ 08.8 (mọi $z_j=0$, $m=100$) và $F=L_s$, $L_s(w)=1+\cos w$. Kiểm các giả thiết của Mệnh đề 08.12 cho SGD rút đều một quan sát, với $\eta=0{,}1$ và $w_1=0$, và tìm hằng số $\sigma^2$ nhỏ nhất. Tính vế phải của mệnh đề và vế trái trên quỹ đạo này, rồi tính $\operatorname{opt}_s(w_1)$ với $W=\mathbb R$.

**(b)** Cho $W\subset\mathbb R^p$ khác rỗng, lồi, bị chặn, với đường kính $\operatorname{diam}(W)=\sup_{u,v\in W}\lVert u-v\rVert$, và $L_s$ lồi, khả vi trên $\mathbb R^p$. Chứng minh rằng với mọi $w\in W$,
$$
\begin{aligned}
\operatorname{opt}_s(w)&\le\lVert\nabla L_s(w)\rVert\\
&\quad\times\operatorname{diam}(W).
\end{aligned}
$$
Bất đẳng thức này có đúng cho $L_s$ của (a) với $W=[-4,4]$ không?

**(c)** Trong thí nghiệm mở đầu, sau $100$ vòng qua dữ liệu, Phụ lục F ghi ba trung bình qua $20$ hạt giống ngẫu nhiên (random seed). Chuẩn gradient $\lVert\nabla L_S\rVert$ là $0{,}004$; lỗi logistic là $0{,}134$ trên mẫu huấn luyện và $1{,}053$ trên mẫu kiểm tra. Đại lượng nào nhỏ, đại lượng nào không? Kết quả nào của bài chặn từng đại lượng, và vì sao (b) không áp dụng cho thí nghiệm này?

**(d)** Với hồi quy logistic, $F=L_s$, $W=\mathbb R^p$, $w_1=0$, $\beta=\tfrac14$, $F(0)-F_*\le\ln2$ và $\sigma^2\le1$ (đoạn sau Mệnh đề 08.12), $T=10^4$: tính vế phải của Mệnh đề 08.12 với $\eta=4=1/\beta$, tìm $\eta$ làm nhỏ nhất vế phải và giá trị nhỏ nhất. So với giá trị $0{,}0153$ của $\eta=0{,}05$.
:::

::: hint Gợi ý 1
Phần (a). So sánh $\nabla\ell(w,z_j)$ giữa các quan sát của mẫu. Phần (b). Viết bất đẳng thức dưới gradient tại $w$ cho một điểm $u\in W$ bất kì. Phần (d). Vế phải có dạng $a/\eta+b\eta$.
:::

::: hint Gợi ý 2
Phần (a). Mọi quan sát của mẫu bằng $0$, nên gradient ngẫu nhiên không có nhiễu. Phần (b). $L_s(u)\ge L_s(w)+\langle\nabla L_s(w),u-w\rangle\ge L_s(w)-\lVert\nabla L_s(w)\rVert\,\lVert u-w\rVert$; lấy cận dưới đúng theo $u\in W$. Phần (d). Với $a=2(F(w_1)-F_*)/T$ và $b=\beta\sigma^2$, giá trị nhỏ nhất là $2\sqrt{ab}$ tại $\eta=\sqrt{a/b}$; kiểm $\eta\le1/\beta$.
:::

::: solution Lời giải Bài tập 08.4
**(a) Điểm dừng (stationary point) là điểm cực đại.**

**Bước 1: giả thiết.** $F(w)=1+\cos w$ có $F''(w)=-\cos w\in[-1,1]$, nên $F$ là $1$-trơn, và $F_*=0$. Gradient ngẫu nhiên là $g_t=-\sin(w_t-z_{i_t})=-\sin w_t=F'(w_t)$ với mọi chỉ số, nên không chệch và $\mathbb E[(g_t-F'(w_t))^2\mid\mathcal F_{t-1}]=0$. Hằng số nhỏ nhất là $\sigma^2=0$. Điều kiện $\eta=0{,}1\le1/\beta=1$ thỏa, và nguồn ngẫu nhiên có hữu hạn giá trị nên giả thiết khả tích đúng.

**Bước 2: hai vế.** Vế phải là
$$
\frac{2(F(0)-0)}{0{,}1\,T}+0=\frac{40}T .
$$
Vì $F'(0)=0$, mọi điểm lặp bằng $0$, nên vế trái bằng $0$.

**Bước 3: sai số tối ưu.** $\operatorname{opt}_s(0)=F(0)-\inf_{\mathbb R}F=2-0=2$, giá trị lớn nhất có thể của hàm lỗi. Mệnh đề 08.12 đúng với vế trái bằng $0$, nhưng điểm trả về có rủi ro thực nghiệm lớn nhất.

**(b) Gradient nhỏ với hàm lồi.**

**Bước 1: bất đẳng thức dưới gradient.** Với $u\in W$, vì $L_s$ lồi và khả vi, rồi theo Cauchy–Schwarz,
$$
\begin{aligned}
L_s(u)&\ge L_s(w)\\
&\quad+\langle\nabla L_s(w),u-w\rangle\\
&\ge L_s(w)-\lVert\nabla L_s(w)\rVert\\
&\qquad\times\operatorname{diam}(W).
\end{aligned}
$$
Dòng thứ hai dùng $\lVert u-w\rVert\le\operatorname{diam}(W)$ vì $u,w\in W$.

**Bước 2: cận dưới đúng.** Vế phải không phụ thuộc $u$, nên lấy cận dưới đúng theo $u\in W$ ta được $\inf_WL_s\ge L_s(w)-\lVert\nabla L_s(w)\rVert\operatorname{diam}(W)$, tức bất đẳng thức cần chứng minh.

**Bước 3: hàm không lồi.** Với $L_s(w)=1+\cos w$ và $W=[-4,4]$ (đường kính $8$), tại $w=0$ vế phải bằng $0\cdot8=0$, còn $\operatorname{opt}_s(0)=2-\min_{[-4,4]}(1+\cos w)=2$ vì $\pi\in[-4,4]$. Bất đẳng thức sai; Bước 1 cần tính lồi.

**(c) Ba đại lượng trong thí nghiệm.**

**Bước 1: đọc số.** Chuẩn gradient $0{,}004$ nhỏ. Lỗi huấn luyện $0{,}134$ nhỏ so với $\ln2\approx0{,}693$ tại $w_1=0$. Lỗi kiểm tra $1{,}053$ ước lượng $L_D$ của điểm lặp cuối và lớn hơn $L_D(w_1)=\ln2$, nên theo ước lượng này, điểm lặp cuối có rủi ro kì vọng lớn hơn điểm khởi tạo.

**Bước 2: kết quả tương ứng.** Mệnh đề 08.12 chặn tính dừng (trung bình bình phương chuẩn gradient dọc quỹ đạo). Với hàm lỗi lồi và $W$ bị chặn, (b) chuyển chuẩn gradient thành cận cho sai số tối ưu thực nghiệm. Rủi ro kì vọng cần thêm khoảng cách tổng quát hóa; trong thí nghiệm này khoảng cách đó là $0{,}919$, và cận $t/200$ của Định lý 08.6 bằng $100$.

**Bước 3: (b) không áp dụng.** Thí nghiệm dùng $W=\mathbb R^p$, không bị chặn, nên $\operatorname{diam}(W)=\infty$. Hơn nữa (b) chỉ chặn đại lượng thực nghiệm $\operatorname{opt}_s$, còn lỗi kiểm tra $1{,}053$ gồm cả khoảng cách tổng quát hóa $0{,}919$.

**(d) Độ dài bước trong Mệnh đề 08.12.**

**Bước 1: $\eta=4$.**
$$
\begin{aligned}
&\frac{2\ln2}{4\cdot10^4}+\tfrac14\cdot4\cdot1\\
&\approx0{,}0000347+1\\
&\le1{,}0001 .
\end{aligned}
$$
Số hạng $\beta\eta\sigma^2=1$ chiếm gần hết vế phải.

**Bước 2: độ dài bước tốt nhất.** Với $a=2\ln2/10^4\approx1{,}386\cdot10^{-4}$ và $b=\tfrac14$,
$$
\begin{aligned}
\eta&=\sqrt{a/b}\approx0{,}02355\le4,\\
2\sqrt{ab}&\approx0{,}011774\le0{,}0118 .
\end{aligned}
$$

**Bước 3: so sánh.** Ba độ dài bước $0{,}02355$, $0{,}05$, $4$ cho các cận $0{,}0118$, $0{,}0153$, $1{,}0001$ cho trung bình của $\lVert\nabla L_s(w_t)\rVert^2$. Theo bất đẳng thức Jensen, trung bình của $\lVert\nabla L_s(w_t)\rVert$ (lấy theo $t$ và theo kì vọng) không quá $\sqrt{0{,}0118}\approx0{,}109$ với độ dài bước tốt nhất. Cả ba cận chỉ nói về gradient, không nói về $L_s$ hay $L_D$.

**Kiểm tra lại.** Với $\eta=0{,}05$, $\frac{2\ln2}{500}+0{,}0125\approx0{,}0153$, khớp đoạn sau Mệnh đề 08.12. Ở (a), $L_s(w)=1+\cos w$ khớp Bước 2 của Ví dụ 08.8 ($L_s(0)=2$).
:::

### Bài tập 08.5 (Kiểm tra giả thiết cho một thiết lập huấn luyện mạng ReLU)

**Mức độ:** kiểm tra giả thiết, khái niệm, tính toán. **Mục tiêu:** mục tiêu học tập 5; kiểm giả thiết của Định lý 08.6 cho một mạng ReLU và nêu cái giá của hai cách sửa.

::: exercise Bài tập 08.5
Một báo cáo mô tả việc huấn luyện mạng ReLU của Định nghĩa 07.1 với $J=2$, $N$ nơ-ron ẩn và mọi trọng số được huấn luyện. Hàm lỗi là hàm lỗi logistic theo véc-tơ tham số $\theta$, đặc trưng thỏa $\lVert x\rVert\le1$, mẫu gồm $m=5\cdot10^4$ quan sát độc lập cùng phân bố, và thuật toán là SGD không chiếu với $\eta=0{,}1$ và $T=10^5$. Báo cáo viết: "Theo Định lý 08.6 với $G=1$, khoảng cách tổng quát hóa kì vọng không quá $2\cdot1^2\cdot0{,}1\cdot10^5/(5\cdot10^4)=0{,}4$."

**(a)** Xét trường hợp nhỏ nhất: $p=1$, $N=1$, $x=1$, $\tilde y=1$, trọng số ra bằng $1$ và hệ số tự do bằng $0$, chỉ trọng số ẩn $\theta\in\mathbb R$ được huấn luyện, nên hàm lỗi là $\ell(\theta)=\ln\big(1+e^{-\operatorname{ReLU}(\theta)}\big)$. Tính đạo hàm trái và đạo hàm phải tại $\theta=0$. Hàm này có $\beta$-trơn không? Có lồi không?

**(b)** Xét hai tham số $\theta=(\theta_1,\theta_2)\in\mathbb R^2$ và $f_\theta(x)=\theta_2\operatorname{ReLU}(\theta_1x)$, với $x=1$, $\tilde y=1$. Chứng minh rằng không có hằng số $G$ nào để (G) đúng trên $\mathbb R^2$.

**(c)** Lập bảng các giả thiết của Định lý 08.6 cho thiết lập của báo cáo: thỏa, không thỏa, hay không xác định. Con số $0{,}4$ có căn cứ không?

**(d)** Nêu hai cách sửa thiết lập để có một cận ổn định, và cái giá của mỗi cách: (i) cố định lớp ẩn trước khi thấy mẫu, chỉ huấn luyện lớp ra như mạng của Ví dụ 07.3; (ii) thay ReLU bằng một hàm kích hoạt trơn có đạo hàm cấp một và cấp hai bị chặn, và chiếu lên một tập $W$ lồi, bị chặn.
:::

::: hint Gợi ý 1
Phần (a). Trên $\theta<0$ hàm lỗi là hằng. Hàm lồi trên $\mathbb R$ có đạo hàm phải không nhỏ hơn đạo hàm trái. Phần (b). Gradient theo $\theta_1$ chứa thừa số $\theta_2$.
:::

::: hint Gợi ý 2
Phần (b). Với $\theta_1>0$, $\partial\ell/\partial\theta_1=-\theta_2/(1+e^{\theta_1\theta_2})$; lấy $\theta_1=1/\theta_2$ và cho $\theta_2\to\infty$. Phần (d)(i). Với lớp ẩn cố định, hàm lỗi là hàm lỗi logistic của một mô hình tuyến tính trên đặc trưng $\chi(x)$ (Ví dụ 08.10, Bước 3). Phần (d)(ii). Tính lồi vẫn không có; xem Mệnh đề 08.10.
:::

::: solution Lời giải Bài tập 08.5
**(a) Một nơ-ron.**

**Bước 1: hai đạo hàm một phía.** Với $\theta<0$, $\operatorname{ReLU}(\theta)=0$ và $\ell(\theta)=\ln2$, nên đạo hàm trái tại $0$ bằng $0$. Với $\theta>0$, $\ell(\theta)=\ln(1+e^{-\theta})$ có đạo hàm $-1/(1+e^\theta)$, dần tới $-\tfrac12$ khi $\theta\to0^+$; đạo hàm phải tại $0$ bằng $-\tfrac12$.

**Bước 2: tính trơn.** Hai đạo hàm một phía khác nhau, nên $\ell$ không khả vi tại $0$, và không $\beta$-trơn với $\beta$ nào (Định nghĩa 05.6 đòi gradient tồn tại và Lipschitz).

**Bước 3: tính lồi.** Đạo hàm phải $-\tfrac12$ nhỏ hơn đạo hàm trái $0$, nên $\ell$ không lồi. Bằng số:
$$
\begin{aligned}
&\ell(0)=\ln2\approx0{,}6931,\\
&\tfrac12\big(\ell(-1)+\ell(1)\big)\\
&=\tfrac12\big(\ln2+\ln(1+e^{-1})\big)\\
&\approx\tfrac12(0{,}6931+0{,}3133)\\
&\approx0{,}5032 .
\end{aligned}
$$
Giá trị tại trung điểm lớn hơn trung bình hai đầu mút.

**(b) Không có cận gradient đều.**

**Bước 1: gradient.** Với $\theta_1>0$, $f_\theta(1)=\theta_1\theta_2$ và $\ell(\theta)=\ln(1+e^{-\theta_1\theta_2})$, nên
$$
\frac{\partial\ell}{\partial\theta_1}=\frac{-\theta_2}{1+e^{\theta_1\theta_2}} .
$$

**Bước 2: dãy điểm.** Với $\theta_2>0$ và $\theta_1=1/\theta_2$, $\theta_1\theta_2=1$ và $\lvert\partial\ell/\partial\theta_1\rvert=\theta_2/(1+e)$. Đại lượng này vượt mọi $G$ khi $\theta_2>G(1+e)$. Vì vậy (G) không đúng trên $\mathbb R^2$ với hằng số nào. Cận $G=1$ của báo cáo là cận của hồi quy logistic tuyến tính, nơi gradient theo $w$ là $x$ nhân một số trong $(-1,1)$.

**(c) Bảng giả thiết.**

| Giả thiết | Kết luận |
|---|---|
| (T1) | thỏa (độc lập cùng phân bố) |
| (T2) | thỏa |
| $W$ lồi | thỏa ($W$ là toàn bộ không gian tham số) |
| (S): lồi | không thỏa (a) |
| (S): trơn | không thỏa (a) |
| (G) | không thỏa (b) |
| $\eta_t\le2/\beta$ | không xác định |

Với (T2): $\ell\ge0$, và tại tham số khởi tạo cố định, $f_\theta$ liên tục nên bị chặn trên quả cầu đơn vị, do đó $L_D$ hữu hạn. Ba giả thiết tối ưu không thỏa, nên Định lý 08.6 không áp dụng và con số $0{,}4$ không có căn cứ. Điều này không có nghĩa là khoảng cách thật lớn; học phần không có cận cho thiết lập này (đoạn sau Ví dụ 08.10).

**(d) Hai cách sửa.**

**Bước 1: cố định lớp ẩn.** Lớp ẩn rút trước khi thấy mẫu và giữ cố định; chỉ véc-tơ $w$ của lớp ra được huấn luyện trên $\chi(x)$ của Ví dụ 07.3. Hàm lỗi logistic theo $w$ thỏa (S) với $\beta=G^2/4$ và (G) với $G=\sup_x\lVert\chi(x)\rVert$ (Ví dụ 08.10, Bước 3). Cận của Định lý 08.6 là
$$
\frac{2G^2\cdot0{,}1\cdot10^5}{5\cdot10^4}=0{,}4\,G^2,
$$
với điều kiện $0{,}1\le8/G^2$. Con số $0{,}4$ chỉ đúng khi $G\le1$; với $G=1{,}5$, cận là $0{,}9$. Cái giá: mô hình là một mô hình tuyến tính trên đặc trưng cố định, lớp ẩn không học.

**Bước 2: hằng số trên $W$.** Với hàm kích hoạt trơn và phép chiếu, trên $W$ lồi, bị chặn, hàm lỗi có gradient liên tục và bị chặn, nên (G) đúng với một $G$ hữu hạn; vì hàm kích hoạt có đạo hàm cấp hai bị chặn, gradient Lipschitz trên $W$ với một hằng số $\beta_W$. Tính lồi vẫn không có, vì đổi chỗ hai nơ-ron ẩn cho cùng hàm (Ví dụ 08.10, Bước 3).

**Bước 3: cận không lồi.** Bước 1 của Phụ lục D chỉ dùng gradient tại hai điểm lặp, đều thuộc $W$, nên lập luận của Mệnh đề 08.10 cho thừa số $(1+\beta_W\eta)^T$; với $\beta_W=1$, $\eta=0{,}1$, $T=10^5$, thừa số này là $1{,}1^{10^5}>10^{4139}$. Cận không cho thông tin. Nhận xét 08.11 dùng độ dài bước giảm như $c/t$, nhưng được phát biểu cho SGD không chiếu với hàm lỗi trong $[0,1]$. Để áp dụng cho (ii), cần chia hàm lỗi cho cận trên của nó và kiểm lại lập luận khi có phép chiếu.

**Kiểm tra lại.** Ở (a), $-1/(1+e^\theta)\to-\tfrac12$ khi $\theta\to0^+$, khớp đạo hàm phải. Ở (b), với $\theta_2=10$ và $\theta_1=\tfrac1{10}$, $\lvert\partial\ell/\partial\theta_1\rvert=10/(1+e)\approx2{,}69>1$, lớn hơn $G=1$ của báo cáo.
:::

### Bài tập 08.6 (Thực nghiệm tùy chọn: hai lần chạy ghép cặp theo thời gian)

**Mức độ:** tính toán (bắt buộc), khái niệm (bắt buộc), thực nghiệm (tùy chọn). **Mục tiêu:** mục tiêu học tập 5; đọc số đo qua nhiều hạt giống và tách bằng chứng thí nghiệm khỏi chứng minh.

::: exercise Bài tập 08.6
Thí nghiệm mở đầu (Phụ lục F: $p=100$, $m=200$, $5000$ quan sát kiểm tra độc lập, SGD không chiếu, $w_1=0$) được chạy với hai độ dài bước $\eta\in\{0{,}25;\,0{,}5\}$ và cùng $20$ hạt giống $0,\ldots,19$. Thứ tự rút của Phụ lục F không phụ thuộc $\eta$, nên với mỗi hạt giống, hai độ dài bước dùng cùng mẫu huấn luyện, mẫu kiểm tra, mẫu lân cận và dãy chỉ số. Sau $e$ vòng qua dữ liệu, số bước là $t=200e$. Các bảng dưới đây là số liệu cho phần (a) và (b). Bốn bảng ghi trung bình qua $20$ hạt giống; cột $\eta=0{,}5$ trùng các số của ghi chú.

Khoảng cách tổng quát hóa ước lượng (lỗi logistic kiểm tra trừ lỗi logistic huấn luyện):

| Vòng | $\eta=0{,}25$ | $\eta=0{,}5$ |
|---|---|---|
| $0{,}5$ | $0{,}025$ | $0{,}045$ |
| $1$ | $0{,}046$ | $0{,}079$ |
| $5$ | $0{,}147$ | $0{,}213$ |
| $10$ | $0{,}212$ | $0{,}298$ |
| $20$ | $0{,}299$ | $0{,}419$ |
| $50$ | $0{,}461$ | $0{,}650$ |
| $100$ | $0{,}651$ | $0{,}919$ |

Khoảng cách $\Delta_{t+1}$ giữa hai lần chạy ghép cặp:

| Vòng | $\eta=0{,}25$ | $\eta=0{,}5$ |
|---|---|---|
| $0{,}5$ | $0{,}073$ | $0{,}142$ |
| $1$ | $0{,}124$ | $0{,}233$ |
| $5$ | $0{,}523$ | $0{,}873$ |
| $10$ | $0{,}931$ | $1{,}472$ |
| $20$ | $1{,}447$ | $2{,}219$ |
| $50$ | $2{,}531$ | $3{,}732$ |
| $100$ | $3{,}745$ | $5{,}458$ |

Tỉ lệ đổi nhãn dự đoán (prediction flip rate) trên mẫu kiểm tra:

| Vòng | $\eta=0{,}25$ | $\eta=0{,}5$ |
|---|---|---|
| $0{,}5$ | $0{,}015$ | $0{,}015$ |
| $1$ | $0{,}016$ | $0{,}016$ |
| $5$ | $0{,}021$ | $0{,}022$ |
| $10$ | $0{,}023$ | $0{,}026$ |
| $20$ | $0{,}024$ | $0{,}026$ |
| $50$ | $0{,}028$ | $0{,}031$ |
| $100$ | $0{,}031$ | $0{,}034$ |

Lỗi phân lớp trên mẫu kiểm tra:

| Vòng | $\eta=0{,}25$ | $\eta=0{,}5$ |
|---|---|---|
| $0{,}5$ | $0{,}384$ | $0{,}383$ |
| $1$ | $0{,}361$ | $0{,}356$ |
| $5$ | $0{,}314$ | $0{,}309$ |
| $10$ | $0{,}303$ | $0{,}301$ |
| $20$ | $0{,}300$ | $0{,}301$ |
| $50$ | $0{,}300$ | $0{,}304$ |
| $100$ | $0{,}305$ | $0{,}312$ |

Bốn cặp thời điểm có cùng ngân sách $\eta t\in\{50;500;1000;5000\}$: $\eta=0{,}25$ ở $1$, $10$, $20$, $100$ vòng và $\eta=0{,}5$ ở $0{,}5$, $5$, $10$, $50$ vòng. Với mỗi cặp và mỗi hạt giống, lấy hiệu (giá trị của $\eta=0{,}25$ trừ giá trị của $\eta=0{,}5$). Bảng ghi trung bình và, trong ngoặc, độ lệch chuẩn (standard deviation) của $20$ hiệu.

| $\eta t$ | Khoảng cách | Lỗi phân lớp |
|---|---|---|
| $50$ | $0{,}0019$ ($0{,}0048$) | $-0{,}0218$ ($0{,}0151$) |
| $500$ | $-0{,}0010$ ($0{,}0074$) | $-0{,}0061$ ($0{,}0068$) |
| $1000$ | $0{,}0013$ ($0{,}0059$) | $-0{,}0015$ ($0{,}0064$) |
| $5000$ | $0{,}0008$ ($0{,}0096$) | $0{,}0012$ ($0{,}0040$) |

Ở $\eta t=5000$, độ lệch chuẩn của khoảng cách qua $20$ hạt giống là $0{,}0847$ với $\eta=0{,}25$ và $0{,}0817$ với $\eta=0{,}5$.

**(a)** (Bắt buộc, tính toán.)

- **(i)** Kiểm giả thiết của Định lý 08.6 cho $\eta=0{,}25$, viết cận của nó theo số vòng $e$ cho hai độ dài bước, và tính tỉ số giữa cận và khoảng cách đo được ở $0{,}5$ và $100$ vòng với $\eta=0{,}25$.
- **(ii)** Với bốn cặp cùng ngân sách, tính *sai số chuẩn* (standard error) của hiệu theo hạt giống, cho khoảng cách và cho lỗi phân lớp. Hiệu nào lớn hơn hai lần sai số chuẩn của nó? Ở $\eta t=5000$, so sai số chuẩn này với sai số chuẩn khi coi hai nhóm là độc lập.
- **(iii)** Với $\eta=0{,}5$, tìm số mũ $\alpha$ sao cho khoảng cách đo được tăng như $t^\alpha$ từ $10$ đến $100$ vòng; làm tương tự với $\Delta$. So với số mũ của cận.

**(b)** (Bắt buộc, khái niệm.) Nêu những kết luận mà các bảng cho phép và những kết luận chúng không cho phép. Vì sao Định lý 08.6 không chặn tỉ lệ đổi nhãn và lỗi phân lớp? Vì sao không được đọc đường cong khoảng cách như đường cong của cận?

**(c)** (Thực nghiệm, tùy chọn.) Viết một chương trình chỉ dùng NumPy theo Phụ lục F, tái lập cột $\eta=0{,}5$, rồi chạy một biến thể tự chọn: $m=400$, không lật nhãn, xáo trộn lại sau mỗi vòng qua dữ liệu, hay $\eta=1$. Ghi dự đoán về các đại lượng trước khi chạy.
:::

::: hint Gợi ý 1
Phần (a)(i). Với $G=1$ và $m=200$, cận là $2\eta t/200$; thay $t=200e$. Phần (a)(ii). Hai độ dài bước dùng chung hạt giống, nên đơn vị ngẫu nhiên là hạt giống. Phần (a)(iii). Lấy logarit của tỉ số hai giá trị và chia cho $\ln10$.
:::

::: hint Gợi ý 2
Phần (a)(ii). Sai số chuẩn của trung bình $20$ hiệu là độ lệch chuẩn của các hiệu chia $\sqrt{20}\approx4{,}472$. Khi coi hai nhóm độc lập, sai số chuẩn của hiệu hai trung bình là $\sqrt{s_1^2+s_2^2}/\sqrt{20}$. Phần (b). Hàm lỗi 0–1 không liên tục theo $w$; cận của Định lý 08.6 là cận trên cho một kì vọng.
:::

::: solution Lời giải Bài tập 08.6
**(a) Tính trên số đã chạy.**

**Bước 1: giả thiết và cận.** Như Ví dụ 08.6, Bước 1: (T1), (T2), (S) với $\beta=\tfrac14$ và (G) với $G=1$ đều thỏa, $W=\mathbb R^p$, và $\eta=0{,}25\le8$. Cận của Định lý 08.6 là
$$
\begin{aligned}
\frac{2G^2\eta t}m&=\frac{2\eta\cdot200e}{200}=2\eta e,
\end{aligned}
$$
tức $0{,}5e$ với $\eta=0{,}25$ và $e$ với $\eta=0{,}5$. Cận chỉ phụ thuộc ngân sách $\eta t$.

**Bước 2: tỉ số cận trên khoảng cách.** Với $\eta=0{,}25$, ở $0{,}5$ vòng tỉ số là $0{,}25/0{,}025=10$; ở $100$ vòng là $50/0{,}651\approx76{,}8$. Với $\eta=0{,}5$, Ví dụ 08.6 cho $11{,}1$ và $108{,}8$.

**Bước 3: sai số chuẩn của hiệu theo hạt giống.** Sai số chuẩn bằng độ lệch chuẩn của các hiệu chia cho $\sqrt{20}$. Mỗi ô ghi sai số chuẩn, rồi tỉ số giữa trị tuyệt đối của trung bình hiệu và sai số chuẩn.

| $\eta t$ | Khoảng cách | Lỗi phân lớp |
|---|---|---|
| $50$ | $0{,}0011$; $1{,}7$ | $0{,}0034$; $6{,}5$ |
| $500$ | $0{,}0017$; $0{,}6$ | $0{,}0015$; $4{,}0$ |
| $1000$ | $0{,}0013$; $1{,}0$ | $0{,}0014$; $1{,}0$ |
| $5000$ | $0{,}0021$; $0{,}4$ | $0{,}0009$; $1{,}3$ |

Không hiệu khoảng cách nào vượt hai lần sai số chuẩn. Hiệu lỗi phân lớp ở $\eta t=50$ và $\eta t=500$ vượt: ở hai ngân sách này, $\eta=0{,}25$ cho lỗi phân lớp kiểm tra thấp hơn.

**Bước 4: hiệu theo hạt giống và hai nhóm độc lập.** Ở $\eta t=5000$, coi hai nhóm độc lập cho
$$
\begin{aligned}
\frac{\sqrt{0{,}0847^2+0{,}0817^2}}{\sqrt{20}}&\approx\frac{0{,}1177}{4{,}472}\\
&\approx0{,}0263,
\end{aligned}
$$
lớn hơn sai số chuẩn của hiệu theo hạt giống ($0{,}0021$) khoảng $12$ lần. Hai nhóm dùng chung mẫu và dãy chỉ số, nên khoảng cách của hai nhóm tương quan mạnh theo hạt giống; công thức độc lập bỏ qua tương quan này.

**Bước 5: số mũ.** Từ $10$ đến $100$ vòng, $t$ tăng $10$ lần. Với $\eta=0{,}5$, số mũ của khoảng cách là
$$
\begin{aligned}
\alpha&=\frac{\ln(0{,}919/0{,}298)}{\ln10}\\
&\approx\frac{1{,}126}{2{,}303}\approx0{,}49,
\end{aligned}
$$
và số mũ của $\Delta$ là
$$
\begin{aligned}
\alpha&=\frac{\ln(5{,}458/1{,}472)}{\ln10}\\
&\approx\frac{1{,}311}{2{,}303}\approx0{,}57 .
\end{aligned}
$$
Cận tăng như $t^1$, tức tăng $10$ lần; khoảng cách tăng $3{,}08$ lần và $\Delta$ tăng $3{,}71$ lần.

**(b) Phạm vi của kết luận.**

**Bước 1: kết luận được phép.** Các kết luận sau chỉ đúng cho thiết lập đã chạy ($D$ của Phụ lục F, $p=100$, $m=200$, hai độ dài bước, $20$ hạt giống).

- **Ngân sách.** Ở cùng ngân sách $\eta t$, hai độ dài bước cho khoảng cách đo được khác nhau không quá hai lần sai số chuẩn của hiệu theo hạt giống, và $\Delta$ gần nhau ($1{,}447$ so với $1{,}472$ ở $\eta t=1000$).
- **Hình dạng.** Khoảng cách và $\Delta$ nằm dưới cận ở mọi thời điểm và tăng chậm hơn tuyến tính (số mũ khoảng $0{,}5$–$0{,}6$ từ $10$ đến $100$ vòng).
- **Dự đoán và lỗi phân lớp.** Tỉ lệ đổi nhãn tăng từ $0{,}015$ lên $0{,}031$–$0{,}034$. Lỗi phân lớp kiểm tra gần như không đổi (khoảng $0{,}30$–$0{,}31$) từ $10$ đến $100$ vòng, trong khi khoảng cách logistic tăng hơn ba lần. Ở ngân sách nhỏ, lỗi phân lớp phụ thuộc cả $\eta$, không chỉ $\eta t$.

**Bước 2: kết luận không được phép.** Các bảng là bằng chứng thí nghiệm, không phải chứng minh. Chúng không chứng tỏ khoảng cách tăng như căn bậc hai của ngân sách với phân bố, cỡ mẫu hay mô hình khác, và không chứng tỏ điều gì về mạng nơ-ron không lồi.

**Bước 3: vì sao định lý không chặn hai đại lượng.** Tỉ lệ đổi nhãn và lỗi phân lớp dùng hàm lỗi 0–1, không liên tục theo $w$, nên không Lipschitz; Bước 1 của chứng minh Định lý 08.6 không áp dụng cho chúng. Một $\Delta$ nhỏ vẫn có thể đổi nhãn những quan sát kiểm tra nằm gần siêu phẳng quyết định.

**Bước 4: đường cong và cận.** Định lý 08.6 cho một cận trên của khoảng cách tổng quát hóa kì vọng, đúng với mọi phân bố thỏa giả thiết. Đường cong đo được là một ước lượng cho một phân bố, có sai số do $20$ hạt giống và $5000$ quan sát kiểm tra. Khoảng cách đo được nằm dưới cận ở mọi thời điểm của bảng, nhưng hình dạng của đường cong (số mũ $0{,}49$) không suy ra được từ cận (số mũ $1$).

**(c) Một giao thức mẫu.**

- **Tái lập.** Theo đúng Phụ lục F: dữ liệu, thứ tự rút trong mỗi hạt giống, ba lần chạy, bảy thời điểm đo. So cột $\eta=0{,}5$ với bảng; sai lệch ở chữ số thứ ba có thể do làm tròn.
- **Biến thể.** Đổi đúng một thành phần. Ghi trước khi chạy cận mới của Định lý 08.6 và điều cần quan sát, chẳng hạn với $m=400$ cận giảm một nửa ở cùng số bước, còn khoảng cách đo được thay đổi thế nào thì chưa biết. Với xáo trộn lại, Định lý 08.6 vẫn áp dụng (Phụ lục B); với $\eta=1$, điều kiện $\eta\le8$ vẫn thỏa.
- **Đo và báo cáo.** Mẫu kiểm tra độc lập, chỉ dùng để báo cáo; ít nhất $20$ hạt giống; trung bình, độ lệch chuẩn, nhỏ nhất và lớn nhất. Khi hai cấu hình dùng chung hạt giống, báo sai số chuẩn của hiệu tính theo từng hạt giống.

**Kiểm tra lại.** Cột $\eta=0{,}5$ khớp câu hỏi mở đầu ($0{,}045$; $0{,}079$; $0{,}213$; $0{,}419$; $0{,}919$), Ví dụ 08.6 ($\Delta$ và tỉ lệ đổi nhãn) và Phụ lục F ($0{,}298$, $0{,}650$ ở $10$, $50$ vòng; lỗi phân lớp $0{,}383$ ở nửa vòng). Ở $100$ vòng, khoảng cách $0{,}651$ của $\eta=0{,}25$ khớp Phụ lục F.
:::

### Bài tập 08.7 (SGD có chiếu nhiều vòng cho hồi quy bình phương)

**Mức độ:** kiểm tra giả thiết, tính toán. **Mục tiêu:** mục tiêu học tập 3; áp dụng Hệ quả 08.7 cho chương trình chạy nhiều vòng của Bài 06 và so cận với khoảng cách tổng quát hóa kì vọng tính đúng theo số bước.

::: exercise Bài tập 08.7
Xét chương trình của Ví dụ 06.3: $x=1$, $y=\pm1$ với xác suất $\tfrac12$, hàm lỗi $\ell(w,(x,y))=(wx-y)^2$, $W=[-1,1]$, $w_1=0$, $m=4$, $\eta=0{,}00625$, chỉ số rút đều có hoàn lại, đầu ra $\bar w_T$. Theo Bước 5 của Ví dụ 06.3 và Phụ lục D của Bài 06, với $q=1-2\eta$ và các hệ số $c_t=(1-q^{T-t})/T$, khoảng cách tổng quát hóa kì vọng của $\bar w_T$, kí hiệu $\psi(T)$ trong bài này, là
$$
\begin{aligned}
\psi(T)&=\frac2m\sum_{t=1}^{T-1}c_t\\
&=\frac2m\Big(1-\frac{1-q^T}{2\eta T}\Big).
\end{aligned}
$$

**(a)** Với $\lvert x\rvert\le1$ và $\lvert y\rvert\le1$, kiểm (S) trên $\mathbb R$ với $\beta=2$, (G) trên $W$ với $G=4$, và điều kiện độ dài bước. Chứng minh rằng (G) không đúng trên $W=\mathbb R$ với hằng số nào.

**(b)** Với $T\in\{11;161;1600\}$, tính cận của Hệ quả 08.7 và $\psi(T)$. Tìm $T$ lớn nhất để cận của Hệ quả 08.7 không vượt độ rộng miền giá trị của hàm lỗi trên $W$; làm tương tự với cận của Định lý 08.6 cho điểm lặp cuối.

**(c)** Chứng minh $\psi(T)<2/m$ với mọi $T$. So chiều biến thiên của cận và của $\psi(T)$, và nêu cận này cho thông tin khi nào.
:::

::: hint Gợi ý 1
Phần (a). Tính hai đạo hàm theo $w$. Phần (b). Hệ quả 08.7 với độ dài bước hằng cho $G^2\eta(T-1)/m$; trên $W$, $\lvert wx-y\rvert\le2$. Phần (c). Mỗi $c_t$ nằm trong $[0,1/T]$.
:::

::: hint Gợi ý 2
Phần (a). $\partial_w\ell=2(wx-y)x$ và $\partial_w^2\ell=2x^2$; với $x=1$, $y=0$, đạo hàm bằng $2w$. Phần (b). Cận là $0{,}025(T-1)$; giải $0{,}025(T-1)\le4$. Phần (c). $c_t=(1-q^{T-t})/T$ với $0<q<1$.
:::

::: solution Lời giải Bài tập 08.7
**(a) Hằng số.**

**Bước 1: (S).** $\partial_w^2\ell=2x^2\in[0,2]$ với mọi $w\in\mathbb R$, nên $\ell(\cdot,(x,y))$ lồi và đạo hàm của nó là $2$-Lipschitz trên $\mathbb R$; do đó (S) đúng với $\beta=2$.

**Bước 2: (G) trên $W$.** Với $\lvert w\rvert\le1$, $\lvert\partial_w\ell\rvert=2\lvert wx-y\rvert\lvert x\rvert\le2(1+1)\cdot1=4$.

**Bước 3: (G) trên $\mathbb R$.** Với $x=1$, $y=0$, $\lvert\partial_w\ell\rvert=2\lvert w\rvert$ vượt mọi $G$ khi $\lvert w\rvert>G/2$. Vì vậy cần phép chiếu lên $W$ bị chặn; Thuật toán 08.1 giữ mọi điểm lặp trong $W$.

**Bước 4: độ dài bước.** $\eta=0{,}00625\le2/\beta=1$.

**(b) Cận và giá trị đúng.**

**Bước 1: cận.** Hệ quả 08.7 cho
$$
\begin{aligned}
&\frac{G^2\eta(T-1)}m\\
&=\frac{16\cdot0{,}00625}4(T-1)\\
&=0{,}025(T-1),
\end{aligned}
$$
tức $0{,}25$; $4$; $39{,}975$ với $T=11$; $161$; $1600$.

**Bước 2: $\psi(T)$.** Với $q=0{,}9875$:

- **$T=11$.** $q^{11}\approx0{,}8708$, $2\eta T=0{,}1375$, nên $\psi=\tfrac12\big(1-0{,}1292/0{,}1375\big)\approx\tfrac12\cdot0{,}0602\approx0{,}0301$.
- **$T=161$.** $q^{161}\approx0{,}1320$, $2\eta T=2{,}0125$, nên $\psi\approx\tfrac12\big(1-0{,}8680/2{,}0125\big)\approx\tfrac12\cdot0{,}5687\approx0{,}2843$.
- **$T=1600$.** $q^{1600}\approx1{,}8\cdot10^{-9}$, $2\eta T=20$, nên $\psi\approx\tfrac12\cdot0{,}95=0{,}4750$.

**Bước 3: ngưỡng có thông tin.** Trên $W$, $\lvert wx-y\rvert\le2$, nên hàm lỗi nằm trong $[0,4]$ và mọi khoảng cách tổng quát hóa không quá $4$. Điều kiện $0{,}025(T-1)\le4$ cho $T\le161$, khoảng $40$ vòng qua $4$ quan sát. Cận của Định lý 08.6 cho điểm lặp cuối là $2G^2\eta T/m=0{,}05T$; điều kiện $0{,}05T\le4$ cho $T\le80$, tức $20$ vòng.

**(c) Hai chiều biến thiên.**

**Bước 1: chặn $\psi$.** Vì $0<q<1$, mỗi $c_t=(1-q^{T-t})/T$ nằm trong $[0,1/T]$, nên $\sum_{t=1}^{T-1}c_t\le(T-1)/T<1$ và $\psi(T)<2/m=0{,}5$.

**Bước 2: so sánh.** Tỉ số cận trên giá trị đúng là $0{,}25/0{,}0301\approx8{,}3$ ở $T=11$, $4/0{,}2843\approx14{,}1$ ở $T=161$ và $39{,}975/0{,}4750\approx84{,}2$ ở $T=1600$. Cận tăng tuyến tính theo $T$; $\psi(T)$ tăng nhưng bị chặn bởi $0{,}5$.

**Bước 3: khi nào cận có thông tin.** Cận đúng với mọi $T$, nhưng chỉ cho thông tin khi $G^2\eta(T-1)/m$ nhỏ hơn độ rộng $4$ của miền giá trị, tức ngân sách $\eta(T-1)$ nhỏ hơn $4m/G^2=1$. Chương trình của Bài 06 có ngân sách $0{,}00625\cdot1599\approx10$, nên cận $39{,}975$ không cho thông tin.

**Kiểm tra lại.** Với $T=1600$, cận $39{,}975$ và giá trị đúng $0{,}4750$ khớp đoạn sau Hệ quả 08.7 và Ví dụ 06.3, Bước 5.
:::

### Bài tập 08.8 (Số bước tốt nhất với độ dài bước cố định)

**Mức độ:** chứng minh, tính toán, khái niệm. **Mục tiêu:** mục tiêu học tập 4; làm nhỏ nhất cận ghép theo số bước và tách nó khỏi số bước tốt nhất cho lỗi kiểm tra.

::: exercise Bài tập 08.8
Gọi $B(T)$ là vế phải của Hệ quả 08.8(a):
$$
\begin{aligned}
B(T)&=\frac{R^2}{2\eta T}+\frac{\eta G^2}2\\
&\quad+\frac{\eta G^2(T-1)}m .
\end{aligned}
$$

**(a)** Với $\eta$, $R$, $G$, $m$ cố định, coi $T>0$ là biến liên tục. Tìm $T^*$ làm nhỏ nhất $B$ và chứng minh
$$
\begin{aligned}
B(T^*)&=RG\sqrt{\frac2m}\\
&\quad+\frac{\eta G^2}2-\frac{\eta G^2}m .
\end{aligned}
$$

**(b)** Với thiết lập của Ví dụ 08.7 ($m=10^4$, $R=5$, $G=1$, $\beta=\tfrac14$), tính $T^*$ và $B(T^*)$ cho $\eta=0{,}1$ và $\eta=0{,}02$. Khi $\eta\to0$, $B(T^*)$ tiến về đâu? So với Hệ quả 08.8(b).

**(c)** $T^*$ có phải số bước làm lỗi kiểm tra nhỏ nhất không? Trả lời bằng thí nghiệm mở đầu, và nêu cách chọn số bước hợp lệ.
:::

::: hint Gợi ý 1
Phần (a). $B$ có dạng $a/T+bT+c$ với $a,b>0$. Phần (c). Kiểm giả thiết của Hệ quả 08.8 cho thí nghiệm mở đầu.
:::

::: hint Gợi ý 2
Phần (a). $a=R^2/(2\eta)$, $b=\eta G^2/m$; giá trị nhỏ nhất của $a/T+bT$ là $2\sqrt{ab}$ tại $T=\sqrt{a/b}$. Phần (c). Thí nghiệm dùng $W=\mathbb R^p$ và đầu ra $w_{T+1}$.
:::

::: solution Lời giải Bài tập 08.8
**(a) Số bước tốt nhất.**

**Bước 1: dạng của $B$.** $B(T)=a/T+bT+c$ với $a=\frac{R^2}{2\eta}$, $b=\frac{\eta G^2}m$, $c=\frac{\eta G^2}2-\frac{\eta G^2}m$.

**Bước 2: điểm cực tiểu.** $B'(T)=-a/T^2+b$ bằng $0$ tại $T^*=\sqrt{a/b}$, và $B''(T)=2a/T^3>0$, nên đó là điểm cực tiểu trên $(0,\infty)$:
$$
T^*=\sqrt{\frac{R^2m}{2\eta^2G^2}}=\frac{R\sqrt{m/2}}{\eta G}.
$$

**Bước 3: giá trị.** Tại $T^*$, $a/T^*=bT^*=\sqrt{ab}$, nên
$$
\begin{aligned}
&a/T^*+bT^*\\
&=2\sqrt{\frac{R^2}{2\eta}\cdot\frac{\eta G^2}m}\\
&=\frac{2RG}{\sqrt{2m}}=RG\sqrt{\frac2m}.
\end{aligned}
$$
Cộng $c$ ta được công thức cần chứng minh.

**(b) Thay số.**

**Bước 1: điều kiện.** Hai độ dài bước $0{,}1$ và $0{,}02$ không vượt $2/\beta=8$. Ta có $RG\sqrt{2/m}=5\sqrt{2\cdot10^{-4}}\approx0{,}070711$ và $R\sqrt{m/2}/G\approx353{,}55$.

**Bước 2: $\eta=0{,}1$.** $T^*\approx3535{,}5$ và
$$
\begin{aligned}
B(T^*)&\approx0{,}070711\\
&\quad+0{,}05-0{,}00001\\
&\le0{,}1208 .
\end{aligned}
$$

**Bước 3: $\eta=0{,}02$.** $T^*\approx17\,677{,}7$ và
$$
\begin{aligned}
B(T^*)&\approx0{,}070711\\
&\quad+0{,}01-0{,}000002\\
&\le0{,}0808 .
\end{aligned}
$$

**Bước 4: $\eta\to0$.** Hai số hạng cuối dần về $0$, nên $B(T^*)\to RG\sqrt{2/m}\le0{,}0708$, trong khi $T^*\to\infty$. Đây cũng là giới hạn của cận ở Hệ quả 08.8(b) khi $T\to\infty$. Độ dài bước nhỏ cần nhiều bước hơn và cho cận nhỏ hơn, nhưng cận không xuống dưới $0{,}0708$, vẫn lớn hơn cận $0{,}0500$ của một vòng với quan sát mới (Ví dụ 08.7).

**(c) Số bước của cận và số bước của lỗi kiểm tra.**

**Bước 1: giả thiết.** Thí nghiệm mở đầu dùng $W=\mathbb R^p$, không bị chặn, nên không có $R$ hữu hạn, và đầu ra là $w_{T+1}$. Hệ quả 08.8 không áp dụng, nên không có $T^*$ cho thí nghiệm này.

**Bước 2: hai hàm lỗi.** Trong bảy thời điểm đo, lỗi logistic trên mẫu kiểm tra nhỏ nhất ở $5$ vòng ($0{,}589$; ở $10$ vòng là $0{,}603$). Lỗi phân lớp trên mẫu kiểm tra là $0{,}309$; $0{,}301$; $0{,}312$ ở $5$, $20$, $100$ vòng. Số bước tốt nhất phụ thuộc hàm lỗi dùng để đánh giá.

**Bước 3: ý nghĩa của $T^*$.** Ngay cả khi Hệ quả 08.8 áp dụng, $T^*$ làm nhỏ nhất một tổng hai cận trên, không phải tổng hai đại lượng thật, nên không chứng minh lỗi kiểm tra nhỏ nhất ở đó.

**Bước 4: chọn số bước hợp lệ.** Chọn số bước trước khi chạy, hoặc bằng một mẫu xác thực độc lập với mẫu huấn luyện (Định nghĩa 08.9; §8 của Bài 04). Mẫu kiểm tra chỉ dùng để báo cáo; nếu dùng nó để chọn số bước, lỗi kiểm tra báo cáo không còn là ước lượng không chệch.

**Kiểm tra lại.** Với $\eta=0{,}05$, công thức (a) cho $T^*\approx7071$ và $B(T^*)\approx0{,}070711+0{,}025-0{,}000005\le0{,}0958$, khớp Ví dụ 08.7, Bước 3.
:::
