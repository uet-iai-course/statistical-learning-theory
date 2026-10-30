# Bài tập Bài 03 — Chiều VC và hàm phân lớp tuyến tính

Các bài tập dưới đây đi kèm ghi chú Bài 03 và dẫn định nghĩa, kết quả, ví dụ theo số hiệu của ghi chú. Kí hiệu theo bảng kí hiệu chung của học phần và §2 của ghi chú: $d$ là chiều Vapnik–Chervonenkis (VC dimension), gọi tắt là chiều VC; $p$ là số chiều đặc trưng; $\Pi_{\mathcal H}$ là hàm tăng trưởng (growth function); $\rho_m$ là bán kính VC của Định lý 03.15; $\mathbf e_1,\ldots,\mathbf e_p$ là các véc-tơ đơn vị của $\mathbb R^p$. Thu hẹp $\mathcal H_C$ của lớp lên bộ điểm $C$ gồm các cách gán nhãn (labeling) thực hiện được, và lớp *tách trọn* (shatters) một tập khi thực hiện được mọi cách gán nhãn của tập đó.

Các lớp $\mathcal H_{\mathrm{thr}}$, $\mathcal H_{\mathrm{int}}$, $\mathcal H^p_{\mathrm{aff}}$, $\mathcal H^p_{\mathrm{hom}}$ và quy ước $h_{w,b}(x)=\mathbb 1[\langle w,x\rangle+b\ge0]$ theo ghi chú; $h_{\equiv0}$ là hàm hằng $0$. Thuật ngữ theo ghi chú: mẫu bóng (ghost sample), rủi ro vượt mức (excess risk), độc lập afin (affinely independent), đơn hình (simplex). Hai chữ viết tắt theo ghi chú: tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM) và học xấp xỉ với xác suất cao (probably approximately correct, PAC). Hàm lỗi là hàm lỗi 0–1; $\ln$ là lôgarit tự nhiên, $\log_2$ là lôgarit cơ số $2$.

Sáu bài đầu là bài gốc của học phần. Sáu bài sau chọn từ mục bài tập §6.8 và §9.6 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* (Shalev-Shwartz và Ben-David, 2014; viết tắt UML), phát biểu lại theo kí hiệu của học phần; UML viết $d$ cho số chiều đặc trưng, ở đây viết $p$. Câu hỏi cuối buổi của ghi chú là trường hợp $p=2$ của Bài tập 03.9.

## Bài tập gốc

### Bài tập 03.1 (Hàm tăng trưởng của lớp hàm ngưỡng trên tập hữu hạn)

**Mức độ:** tính toán, chứng minh. **Mục tiêu:** mục tiêu học tập 2; tính hàm tăng trưởng khi bộ điểm được phép lặp, so sánh với tổng nhị thức của bổ đề Sauer–Shelah và với $2^m$.

::: exercise Bài tập 03.1
Gọi $\mathcal H^{(6)}_{\mathrm{thr}}=\{h_t:\ t=1,\ldots,6\}$, với $h_t(x)=\mathbb 1[x\ge t]$, là lớp sáu hàm ngưỡng của Ví dụ 01.1 trên $\mathcal X=\{1,\ldots,5\}$. Theo Định nghĩa 03.11, giá trị lớn nhất trong $\Pi_{\mathcal H}(m)$ lấy trên mọi bộ $m$ điểm, kể cả bộ có điểm lặp.

**(a)** Chứng minh $\Pi_{\mathcal H^{(6)}_{\mathrm{thr}}}(m)=\min\{m+1,6\}$ với mọi $m\ge1$. Tính giá trị tại $m=3$ và $m=8$.

**(b)** Lớp $\mathcal H^{(6)}_{\mathrm{thr}}$ có chiều VC bằng $1$ (Mệnh đề 03.5(b)). Xác định các giá trị $m$ tại đó Bổ đề 03.12(a) đạt dấu bằng cho lớp này. Với $m\ge6$, cận nào trong hai cận $\sum_{j\le1}\binom mj$ và $\min\{2^m,\lvert\mathcal H^{(6)}_{\mathrm{thr}}\rvert\}$ cho đúng giá trị của hàm tăng trưởng?

**(c)** Trên $\mathcal X=\mathbb R$, xét lớp hàm ngưỡng hai phía
$$
\begin{aligned}
\mathcal H^{\pm}_{\mathrm{thr}}=\ &\{x\mapsto\mathbb 1[x\ge t]:\ t\in\mathbb R\}\\
\cup\ &\{x\mapsto\mathbb 1[x\le t]:\ t\in\mathbb R\}.
\end{aligned}
$$
Chứng minh $\Pi_{\mathcal H^{\pm}_{\mathrm{thr}}}(m)=2m$ với mọi $m\ge1$, rồi suy ra chiều VC của lớp. So sánh $\Pi_{\mathcal H^{\pm}_{\mathrm{thr}}}(m)$ với tổng nhị thức của Bổ đề 03.12(a) và với $2^m$ tại $m=1,2,3,10$.
:::

::: hint Gợi ý 1
Phần (a). Với một bộ $m\le5$ điểm phân biệt, dùng Bước 1 của Ví dụ 03.4 và kiểm rằng các ngưỡng cần dùng nằm trong $\{1,\ldots,6\}$. Một bộ điểm của $\{1,\ldots,5\}$ có nhiều nhất năm điểm phân biệt.
:::

::: hint Gợi ý 2
Phần (c). Trên $x_1<\cdots<x_m$, cách gán nhãn của $\mathbb 1[x\ge t]$ gồm một dãy nhãn $0$ rồi một dãy nhãn $1$; cách gán nhãn của $\mathbb 1[x\le t]$ gồm một dãy nhãn $1$ rồi một dãy nhãn $0$. Đếm mỗi họ, rồi trừ các cách gán nhãn có mặt trong cả hai họ.
:::

::: hint Gợi ý 3
Phần (c). Hai họ chung nhau đúng hai cách gán nhãn: toàn $0$ và toàn $1$. Một bộ có $k<m$ điểm phân biệt cho nhiều nhất $2k$ cách gán nhãn.
:::

::: solution Lời giải Bài tập 03.1
**(a) Sáu hàm ngưỡng.** Viết gọn $\Pi$ cho $\Pi_{\mathcal H^{(6)}_{\mathrm{thr}}}$.

**Bước 1: bộ điểm phân biệt, $m\le5$.** Lấy $x_1<\cdots<x_m$ trong $\{1,\ldots,5\}$. Như Bước 1 của Ví dụ 03.4, cách gán nhãn của $h_t$ xác định bởi số nhãn $0$ đứng đầu, từ $0$ đến $m$. Mỗi số đó thực hiện được trong lớp: ngưỡng $t=x_i$ ($i=1,\ldots,m$) cho nhãn $0$ trên $x_1,\ldots,x_{i-1}$ và nhãn $1$ từ $x_i$ trở đi; ngưỡng $t=x_m+1\le6$ cho toàn $0$. Vậy bộ này có đúng $m+1$ cách gán nhãn.

**Bước 2: bộ có điểm lặp.** Các điểm trùng nhau nhận cùng nhãn, nên một bộ có $k$ điểm phân biệt có cùng số cách gán nhãn với tập $k$ điểm đó, tức $k+1$ theo Bước 1. Mọi bộ $m$ điểm có $k\le\min\{m,5\}$.

**Bước 3: kết luận.** Lấy giá trị lớn nhất theo $k$:
$$
\begin{aligned}
\Pi(m)&=\min\{m,5\}+1\\
&=\min\{m+1,6\}.
\end{aligned}
$$
Do đó $\Pi(3)=4$ và $\Pi(8)=6$. Một bộ tám điểm chứa đủ năm mức đo cho sáu cách gán nhãn, mỗi hàm một cách.

**(b) So với hai cận.**

**Bước 1: tổng nhị thức.** Với $d=1$, tổng nhị thức là $\binom m0+\binom m1=1+m$. Nó bằng $\Pi(m)$ khi và chỉ khi $m+1\le6$, tức $m\le5$.

**Bước 2: $m\ge6$.** Ta có $\Pi(m)=6=\lvert\mathcal H^{(6)}_{\mathrm{thr}}\rvert<2^m$, nên cận $\min\{2^m,\lvert\mathcal H^{(6)}_{\mathrm{thr}}\rvert\}$ cho đúng giá trị, còn tổng nhị thức $m+1$ vượt quá nó. Cận của Bổ đề 03.12 chỉ phụ thuộc $d$, không phụ thuộc $\lvert\mathcal H\rvert$.

**(c) Hàm ngưỡng hai phía.**

**Bước 1: hai họ trên điểm phân biệt.** Lấy $x_1<\cdots<x_m$. Các hàm $\mathbb 1[x\ge t]$ cho $m+1$ cách "một dãy $0$ rồi một dãy $1$" ($t\le x_1$, $t\in(x_{i-1},x_i]$ hoặc $t>x_m$). Các hàm $\mathbb 1[x\le t]$ cho $m+1$ cách "một dãy $1$ rồi một dãy $0$" ($t<x_1$, $t\in[x_i,x_{i+1})$ hoặc $t\ge x_m$).

**Bước 2: phần chung.** Một cách gán nhãn thuộc cả hai họ vừa không giảm vừa không tăng theo chỉ số, nên là hằng: toàn $0$ hoặc toàn $1$. Do đó số cách gán nhãn là
$$
(m+1)+(m+1)-2=2m .
$$

**Bước 3: bộ có điểm lặp.** Một bộ có $k<m$ điểm phân biệt cho $2k<2m$ cách gán nhãn. Vậy $\Pi_{\mathcal H^{\pm}_{\mathrm{thr}}}(m)=2m$.

**Bước 4: chiều VC.** Ta có $\Pi(2)=4=2^2$ và $\Pi(3)=6<2^3$ cho lớp này. Theo đoạn sau Định nghĩa 03.11, $\Pi_{\mathcal H}(m)=2^m$ khi và chỉ khi $m\le d$, nên $d=2$.

**Bước 5: so sánh.** Với $d=2$, tổng nhị thức là $1+m+\binom m2=\binom{m+1}2+1$. Bảng dưới viết $\Pi$ thay cho $\Pi_{\mathcal H^{\pm}_{\mathrm{thr}}}$.

| $m$ | $\Pi(m)$ | tổng | $2^m$ |
|---|---|---|---|
| $1$ | $2$ | $2$ | $2$ |
| $2$ | $4$ | $4$ | $4$ |
| $3$ | $6$ | $7$ | $8$ |
| $10$ | $20$ | $56$ | $1024$ |

Bổ đề 03.12(a) đạt dấu bằng khi $m\le2$ và không đạt từ $m=3$. Lớp $\mathcal H_{\mathrm{int}}$, cũng có $d=2$, đạt dấu bằng với mọi $m$ (Ví dụ 03.5).

**Kiểm tra lại.** Trên $(1,2,3)$, sáu cách gán nhãn là $000$, $001$, $011$, $111$, $110$, $100$; hai cách còn thiếu là $010$ và $101$. Thêm hai hàm hằng vào $\mathcal H^{\pm}_{\mathrm{thr}}$ ta được $\mathcal H^1_{\mathrm{aff}}$ (đoạn sau Định nghĩa 03.7), có $d=2$ theo Mệnh đề 03.9(a) với $p=1$, khớp Bước 4.
:::

### Bài tập 03.2 (Chiều VC của lớp khoảng bằng cận dưới và cận trên)

**Mức độ:** chứng minh, khái niệm. **Mục tiêu:** mục tiêu học tập 1; cận dưới, cận trên, và nhận ra một lập luận chỉ có một trong hai phần.

::: exercise Bài tập 03.2
**(a)** Trên $\mathbb R$, xét lớp khoảng mở $\mathcal H^{\circ}_{\mathrm{int}}=\{x\mapsto\mathbb 1[u<x<v]:\ u<v\}$. Chứng minh chiều VC của lớp bằng $2$, và chỉ ra chỗ khác với chứng minh Mệnh đề 03.6.

**(b)** Xét lớp hợp của hai khoảng đóng $\mathcal H_{2\mathrm{int}}$, gồm các hàm $x\mapsto\mathbb 1[x\in I_1\cup I_2]$ với $I_1=[u_1,v_1]$, $I_2=[u_2,v_2]$, $u_1\le v_1$ và $u_2\le v_2$. Chứng minh chiều VC của lớp bằng $4$.

**(c)** Hai lời giải của (b) chưa đầy đủ. Lời giải thứ nhất vẽ mười sáu cách gán nhãn của tập $\{1,2,3,4\}$, mỗi cách kèm một hàm của lớp thực hiện nó, rồi kết luận $d=4$. Lời giải thứ hai chỉ ra cách gán nhãn $(1,0,1,0,1)$ của tập $\{1,2,3,4,5\}$ không thực hiện được, rồi kết luận $d\le4$. Theo Nhận xét 03.4, mỗi lời giải thiếu phần nào?
:::

::: hint Gợi ý 1
Phần (a). Cách gán nhãn toàn $0$ cần một khoảng không chứa điểm nào của tập. Phần (b). Một khoảng chứa hai điểm thì chứa mọi điểm nằm giữa chúng; đếm số khối nhãn $1$ liên tiếp trong một cách gán nhãn của bốn điểm.
:::

::: hint Gợi ý 2
Phần (b). Với năm điểm $x_1<\cdots<x_5$ và cách gán nhãn $(1,0,1,0,1)$, ba điểm $x_1$, $x_3$, $x_5$ phải nằm trong hai khoảng.
:::

::: solution Lời giải Bài tập 03.2
**(a) Khoảng mở.** Chứng minh đi theo Mệnh đề 03.6, với hai chỗ khác: ở cận trên, các bất đẳng thức đổi thành nghiêm ngặt; ở cận dưới, khoảng một điểm $[0,0]$, $[1,1]$ không thuộc lớp, nên được thay bằng $(-1,\tfrac12)$, $(\tfrac12,2)$.

**Bước 1: cận dưới.** Với $C=\{0,1\}$, các khoảng $(-1,2)$, $(-1,\tfrac12)$, $(\tfrac12,2)$, $(2,3)$ thực hiện lần lượt $(1,1)$, $(1,0)$, $(0,1)$, $(0,0)$. Do đó $d\ge2$.

**Bước 2: cận trên.** Lấy ba điểm bất kì $x_1<x_2<x_3$ và cách gán nhãn $(1,0,1)$. Nếu $\mathbb 1[u<x<v]$ thực hiện nó thì $u<x_1$ và $x_3<v$, nên $u<x_2<v$ và $x_2$ nhận nhãn $1$, mâu thuẫn. Vậy $d\le2$.

**(b) Hợp hai khoảng.**

**Bước 1: số khối nhãn $1$.** Lấy $C=\{1,2,3,4\}$. Trong một cách gán nhãn của $(1,2,3,4)$, các nhãn $1$ tạo thành nhiều nhất hai khối điểm liên tiếp: ba khối cần ít nhất ba nhãn $1$ và hai nhãn $0$ ngăn cách, tức năm điểm.

**Bước 2: cận dưới.** Mỗi khối $\{i,\ldots,i'\}$ được thực hiện bởi khoảng $[i,i']$. Khoảng không dùng đến được đặt là $[10,10]$, và cách toàn $0$ dùng hai khoảng $[10,10]$. Cả mười sáu cách gán nhãn thực hiện được, nên $d\ge4$.

**Bước 3: cận trên.** Lấy năm điểm bất kì $x_1<\cdots<x_5$ và cách gán nhãn $(1,0,1,0,1)$. Giả sử hợp $I_1\cup I_2$ của hai khoảng thực hiện nó. Ba điểm $x_1$, $x_3$, $x_5$ nằm trong $I_1\cup I_2$, nên theo nguyên lý chuồng bồ câu (pigeonhole principle), hai trong ba điểm nằm trong cùng một khoảng $I$. Hai điểm đó có một điểm nhãn $0$ nằm giữa ($x_2$ hoặc $x_4$), và $I$ chứa điểm này, mâu thuẫn. Vậy $d\le4$.

**(c) Hai phần còn thiếu.**

**Lời giải thứ nhất** chỉ có cận dưới $d\ge4$. Phần thiếu là cận trên: mọi tập năm điểm không bị tách trọn, như Bước 3 của (b).

**Lời giải thứ hai** chỉ có một tập năm điểm không bị tách trọn, và theo Nhận xét 03.4 điều đó không cho $d\le4$ (Ví dụ 03.3, Bước 2: một tập ba điểm không bị tách trọn dù $d=3$). Bước 3 của (b) chỉ dùng thứ tự của năm điểm, nên đúng cho mọi tập năm điểm. Lời giải thứ hai cũng thiếu cận dưới.

**Kiểm tra lại.** Liệt kê mọi hợp hai khoảng có đầu mút trên lưới bước $\tfrac12$ trong $[0,6]$: tập $\{1,2,3,4\}$ nhận đủ $16$ cách gán nhãn, tập $\{1,\ldots,5\}$ nhận $31$ cách, chỉ thiếu $(1,0,1,0,1)$. Số $31$ bằng tổng $\sum_{j=0}^{4}\binom5j$ của Bổ đề 03.12(a).
:::

### Bài tập 03.3 (Cận dưới cho nửa không gian afin qua điểm độc lập afin)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 1; cận dưới qua một hệ tuyến tính khả nghịch, phân biệt nửa không gian afin với nửa không gian thuần nhất.

::: exercise Bài tập 03.3
**(a)** Cho $p+1$ điểm độc lập afin $x_0,x_1,\ldots,x_p\in\mathbb R^p$. Gọi $M$ là ma trận vuông cấp $p+1$ có hàng thứ $i$ là $(x_i^\top,1)$, $i=0,\ldots,p$. Chứng minh $M$ khả nghịch, rồi suy ra tập $\{x_0,\ldots,x_p\}$ bị $\mathcal H^p_{\mathrm{aff}}$ tách trọn.

**(b)** Với $p=2$, các điểm $(1,1)$, $(2,1)$, $(1,3)$ và cách gán nhãn $(1,0,1)$, giải hệ tuyến tính của (a).

**(c)** Chứng minh $\mathcal H^p_{\mathrm{hom}}$ tách trọn mọi tập $p$ véc-tơ độc lập tuyến tính, và không tách trọn tập nào chứa gốc tọa độ. Suy ra tập $\{0,\mathbf e_1,\ldots,\mathbf e_p\}$ bị $\mathcal H^p_{\mathrm{aff}}$ tách trọn nhưng không bị $\mathcal H^p_{\mathrm{hom}}$ tách trọn.
:::

::: hint Gợi ý 1
Phần (a). Ma trận vuông khả nghịch khi các hàng độc lập tuyến tính. Giả sử $\sum_i\lambda_i(x_i^\top,1)=0$, rồi đọc riêng tọa độ cuối và $p$ tọa độ đầu.
:::

::: hint Gợi ý 2
Phần (a). Từ $\sum_i\lambda_i=0$ suy ra $\sum_{i=0}^{p}\lambda_ix_i=\sum_{i=1}^{p}\lambda_i(x_i-x_0)$. Khi $M$ khả nghịch, giải $M\,(w;b)=(2y_0-1,\ldots,2y_p-1)$, với $(w;b)$ là véc-tơ cột ghép $w$ với $b$.
:::

::: hint Gợi ý 3
Phần (c). Với mọi $w$, $\langle w,0\rangle=0\ge0$.
:::

::: solution Lời giải Bài tập 03.3
**(a) Điểm độc lập afin bị tách trọn.**

**Bước 1: các hàng độc lập tuyến tính.** Giả sử $\sum_{i=0}^{p}\lambda_i(x_i^\top,1)=0$. Tọa độ cuối cho $\sum_i\lambda_i=0$, và $p$ tọa độ đầu cho $\sum_i\lambda_ix_i=0$. Do đó
$$
\begin{aligned}
&\textstyle\sum_{i=1}^{p}\lambda_i(x_i-x_0)\\
&\quad=\textstyle\sum_{i=0}^{p}\lambda_ix_i-\big(\sum_{i=0}^{p}\lambda_i\big)x_0\\
&\quad=0 .
\end{aligned}
$$
Vì $x_1-x_0,\ldots,x_p-x_0$ độc lập tuyến tính, $\lambda_1=\cdots=\lambda_p=0$, và $\lambda_0=-\sum_{i\ge1}\lambda_i=0$. Các hàng độc lập, nên $M$ khả nghịch.

**Bước 2: giải hệ.** Cho một cách gán nhãn $(y_0,\ldots,y_p)$, đặt $c_i=2y_i-1\in\{-1,1\}$ và lấy véc-tơ cột $(w;b)\in\mathbb R^{p+1}$, ghép $w$ với $b$, bằng $M^{-1}c$. Hàng thứ $i$ của $M\,(w;b)=c$ là $\langle w,x_i\rangle+b=c_i$, số này không âm khi và chỉ khi $y_i=1$. Vậy $h_{w,b}$ thực hiện cách gán nhãn đã cho; cả $2^{p+1}$ cách thực hiện được, và chiều VC của $\mathcal H^p_{\mathrm{aff}}$ ít nhất $p+1$.

**(b) Một hệ cụ thể.**

**Bước 1: kiểm giả thiết.** Hai véc-tơ $(2,1)-(1,1)=(1,0)$ và $(1,3)-(1,1)=(0,2)$ độc lập tuyến tính, nên ba điểm độc lập afin.

**Bước 2: hệ phương trình.** Hệ $\langle w,x_i\rangle+b=2y_i-1$ là
$$
\begin{aligned}
w_1+w_2+b&=1&&\text{(1)},\\
2w_1+w_2+b&=-1&&\text{(2)},\\
w_1+3w_2+b&=1&&\text{(3)}.
\end{aligned}
$$

**Bước 3: khử.** Lấy hiệu từng cặp phương trình:
$$
\begin{aligned}
\text{(2)}-\text{(1)}:&\ \ w_1=-2,\\
\text{(3)}-\text{(1)}:&\ \ w_2=0,\\
\text{(1)}:&\ \ b=1-w_1-w_2\\
&\ \ \ =3.
\end{aligned}
$$
Giá trị của $\langle w,x\rangle+b$ tại ba điểm là $1$, $-1$, $1$, cho đúng nhãn $1,0,1$.

**(c) Nửa không gian thuần nhất.**

**Bước 1: véc-tơ độc lập tuyến tính.** Cho $x_1,\ldots,x_p$ độc lập tuyến tính, gọi $N$ là ma trận có hàng thứ $i$ là $x_i^\top$; $N$ khả nghịch. Với cách gán nhãn $y$, lấy $w=N^{-1}c$, $c_i=2y_i-1$. Khi đó $\langle w,x_i\rangle=c_i$, nên $h_{w,0}$ thực hiện $y$.

**Bước 2: tập chứa gốc.** Với mọi $w$, $h_{w,0}(0)=\mathbb 1[0\ge0]=1$. Mọi cách gán nhãn có nhãn $0$ tại gốc đều không thực hiện được, nên tập chứa gốc không bị tách trọn.

**Bước 3: đỉnh đơn hình.** Tập $\{0,\mathbf e_1,\ldots,\mathbf e_p\}$ độc lập afin, nên bị $\mathcal H^p_{\mathrm{aff}}$ tách trọn theo (a); nó chứa gốc, nên không bị $\mathcal H^p_{\mathrm{hom}}$ tách trọn theo Bước 2.

**Kiểm tra lại.** Với $p=1$, điểm $0$, $1$ và cách gán nhãn $(1,0)$, công thức của Mệnh đề 03.9 cho $b=1$, $w=-2$; hàm $\mathbb 1[-2x+1\ge0]=\mathbb 1[x\le\tfrac12]$ cho nhãn $1$ tại $0$ và $0$ tại $1$.
:::

### Bài tập 03.4 (So sánh cỡ mẫu theo chiều VC và nguồn gốc hằng số $8$)

**Mức độ:** tính toán, khái niệm. **Mục tiêu:** mục tiêu học tập 3, 4; cỡ mẫu đủ cho ERM theo chiều VC, so với lớp đã rời rạc hóa; vai trò của mẫu bóng, của từng bước và từng giả thiết trong chứng minh Định lý 03.15.

::: exercise Bài tập 03.4
Hàm lỗi là hàm lỗi 0–1 và $\delta=0{,}05$. Trong (a), (b), (e), $\epsilon$ là cận cho rủi ro vượt mức của mọi nghiệm ERM, đúng với mọi phân bố (Hệ quả 03.16); trong (c), $\epsilon$ là độ lệch đều, như trong chứng minh Định lý 03.15. Ví dụ 03.9 đã tính các cỡ mẫu tại $\epsilon=0{,}1$.

**(a)** Với $\epsilon=0{,}05$ và $d\in\{3,11\}$, dùng máy tính (chia đôi khoảng) để tìm cỡ mẫu nhỏ nhất $m\ge d$ thỏa điều kiện của dạng trực tiếp (Ví dụ 03.9, Bước 1)
$$
\begin{aligned}
&\frac{32}m\Big(d\ln\frac{2em}d+\ln\frac4\delta\Big)\\
&\quad\le\epsilon^2 .
\end{aligned}
$$
Tính thêm cỡ mẫu $M(\epsilon,\delta)$ của Hệ quả 03.16(c).

**(b)** Với dạng trực tiếp, tính tỉ số giữa cỡ mẫu của $d=11$ và của $d=3$ tại $\epsilon=0{,}05$, và tỉ số giữa cỡ mẫu tại $\epsilon=0{,}05$ và tại $\epsilon=0{,}1$. Giải thích vì sao tỉ số thứ nhất nhỏ hơn $11/3$ và tỉ số thứ hai lớn hơn $4$.

**(c)** Câu cuối của chứng minh Định lý 03.15 nêu hai nguồn của hằng số $8$ trong $\rho_m^2$. Tính số mũ ở mỗi bước để kiểm lại tỉ số $16$ giữa hằng số đó và hằng số $\tfrac12$ trong $r_m^2=\ln(2K/\delta)/(2m)$ của Định lý 02.14. Nếu ở Bước 1 dùng Định lý 02.7 thay cho Bổ đề 02.3, cần điều kiện nào trên $m\epsilon^2$ để xác suất lệch ít nhất $\epsilon/2$ không quá $\tfrac12$? Bán kính $\rho_m$ có thay đổi không?

**(d)** Một lập luận bỏ mẫu bóng như sau. Trên mẫu $S$, lớp chỉ cho nhiều nhất $\Pi_{\mathcal H}(m)$ cách gán nhãn; áp dụng Định lý 02.7 cho từng cách gán nhãn và Bổ đề 02.12 cho mọi cách, nên với xác suất ít nhất $1-\delta$,
$$
\begin{aligned}
&\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\\
&\quad\le\sqrt{\ln(2\Pi_{\mathcal H}(m)/\delta)/(2m)} .
\end{aligned}
$$
Tính vế phải cho lớp $\mathcal M_{[0,1]}$ và phân bố của Ví dụ 03.6 tại $m=1000$. So với độ lệch đều thật, rồi chỉ ra bước nào của chứng minh Định lý 03.15 tránh được lỗi này.

**(e)** Lớp $\mathcal H^2_{\mathrm{aff}}$ có ba tham số thực $(w_1,w_2,b)$. Nếu mỗi tham số được lưu bằng $64$ bit, lớp đã rời rạc hóa có $K\le2^{192}$ hàm. Như Ví dụ 03.10 với $q=3$, tính cỡ mẫu $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$ của Hệ quả 02.16(c) với $\epsilon=0{,}1$, so với $132\,992$ của Ví dụ 03.9 ($d=3$), và tách tỉ số thành phần do hằng số và phần do số hạng lôgarit.

**(f)** Với mỗi giả thiết (T1), (T5), (M) và tính bị chặn của hàm lỗi, chỉ ra bước của chứng minh Định lý 03.15 dùng nó.
:::

::: hint Gợi ý 1
Phần (a). Vế trái của điều kiện giảm theo $m\ge d$ (Ví dụ 03.9, Bước 1), nên tìm cỡ mẫu nhỏ nhất bằng chia đôi khoảng. Phần (c). So sánh số mũ trong chứng minh Định lý 02.14 với số mũ trong bất đẳng thức then chốt của chứng minh Định lý 03.15.
:::

::: hint Gợi ý 2
Phần (b). Cỡ mẫu trực tiếp xấp xỉ nghiệm của $m=32\big(d\ln(2em/d)+\ln80\big)/\epsilon^2$; xác định số hạng nào nhân với $d$. Phần (d). Đọc lại hai lý do (i), (ii) đứng trước (T5) ở §7 của ghi chú. Phần (f). Đọc các dòng "Chỗ dùng" trong lộ trình chứng minh và câu cuối của Phụ lục C.
:::

::: hint Gợi ý 3
Phần (e). Hai cỡ mẫu có dạng (hằng số)(lôgarit)$/\epsilon^2$; so riêng hai hằng số $32$, $2$ và hai số hạng $d\ln(2em/d)+\ln(4/\delta)$, $\ln(2K/\delta)$.
:::

::: solution Lời giải Bài tập 03.4
**(a) Cỡ mẫu tại $\epsilon=0{,}05$.**

**Bước 1: điều kiện.** Theo Hệ quả 03.16(a) và dạng trực tiếp của Định lý 03.15(b), rủi ro vượt mức không quá $2\rho_m\le0{,}05$ khi $m\ge d$ và vế trái của điều kiện không quá $\epsilon^2=0{,}0025$, với $\ln(4/\delta)=\ln80\approx4{,}3820$.

**Bước 2: giải số.** Chia đôi khoảng cho $589\,118$ với $d=3$ và $1\,999\,657$ với $d=11$. Kiểm tại hai đầu:

- $d=3$: vế trái bằng khoảng $0{,}0024999964$ tại $m=589\,118$ và $0{,}0025000003$ tại $m=589\,117$.
- $d=11$: vế trái bằng khoảng $0{,}0024999991$ tại $m=1\,999\,657$ và $0{,}0025000002$ tại $m=1\,999\,656$.

**Bước 3: dạng đóng.** Ta có $64/\epsilon^2=25\,600$, $128/\epsilon^2=51\,200$ và $\ln51\,200\approx10{,}8435$. Hai ngoặc là $3\cdot10{,}8435+4{,}3820=36{,}9125$ và $11\cdot10{,}8435+4{,}3820=123{,}6605$. Nhân với $25\,600$:
$$
\begin{aligned}
d=3:&\ \ 25\,600\cdot36{,}9125\\
&\ \ \approx944\,960{,}3,\\
d=11:&\ \ 25\,600\cdot123{,}6605\\
&\ \ \approx3\,165\,708{,}0,
\end{aligned}
$$
làm tròn lên được $944\,961$ và $3\,165\,709$. Mọi con số là cỡ mẫu đủ theo cận của bài.

**(b) Hai tỉ số.**

**Bước 1: tỉ số theo $d$.** $1\,999\,657/589\,118\approx3{,}39<11/3\approx3{,}67$.

**Bước 2: vì sao nhỏ hơn $11/3$.** Tại cỡ mẫu nhỏ nhất, $m\approx12\,800\big(d\ln(2em/d)+\ln80\big)$, nên tỉ số xấp xỉ bằng tỉ số của hai ngoặc, $3\cdot13{,}881+4{,}382\approx46{,}02$ và $11\cdot13{,}804+4{,}382\approx156{,}22$.
Số hạng $\ln80$ không nhân với $d$, và $\ln(2em/d)$ nhỏ hơn một chút khi $d=11$ vì $m/d$ nhỏ hơn ($181\,787$ so với $196\,373$). Cả hai kéo tỉ số xuống dưới $11/3$.

**Bước 3: tỉ số theo $\epsilon$.** $589\,118/132\,992\approx4{,}43$ và $1\,999\,657/447\,194\approx4{,}47$. Thừa số $1/\epsilon^2$ cho $4$; phần dôi ra đến từ $\ln(2em/d)$, tăng thêm khoảng $\ln4{,}43\approx1{,}49$ khi cỡ mẫu tăng.

**(c) Hằng số $8$.**

**Bước 1: số mũ của Định lý 02.14.** Định lý 02.7 cho biến trong $[0,1]$ với độ lệch $r$ có số mũ $-2mr^2$, tức hệ số $2$ trước $mr^2$.

**Bước 2: mẫu bóng (Bước 1 của chứng minh).** Độ lệch $\epsilon$ giữa $L_S$ và $L_D$ chỉ cho độ lệch $\epsilon/2$ giữa $L_{S'}$ và $L_S$. Bình phương cho thừa số $4$.

**Bước 3: Hoeffding (Bước 4 của chứng minh).** Các biến $\sigma_i(\ell(h,Z'_i)-\ell(h,Z_i))$ nằm trong $[-1,1]$, miền dài $2$, nên Định lý 02.7 chia số mũ cho $2^2=4$. Gộp lại,
$$
-\frac{2m(\epsilon/2)^2}{2^2}=-\frac{m\epsilon^2}8,
$$
hệ số đổi từ $2$ thành $\tfrac18$, tỉ số $16$.

**Bước 4: Hoeffding ở Bước 1.** Theo Định lý 02.7(c) với miền dài $1$,
$$
\begin{aligned}
&\Pr\big(\lvert L_{S'}(h_S)-L_D(h_S)\rvert\\
&\qquad\ge\tfrac\epsilon2\mid S\big)\\
&\quad\le2e^{-2m(\epsilon/2)^2}\\
&\quad=2e^{-m\epsilon^2/2}.
\end{aligned}
$$
Vế phải không quá $\tfrac12$ khi và chỉ khi $m\epsilon^2\ge2\ln4\approx2{,}77$; Bổ đề 02.3 cần $m\epsilon^2\ge2$.

**Bước 5: bán kính không đổi.** Cả hai cách cho cùng hệ số $2$ trong bổ đề mẫu bóng, nên bất đẳng thức then chốt và $\rho_m$ không đổi. Tại $\epsilon=\rho_m$, $m\rho_m^2\ge8\ln4\approx11{,}09$, nên cả hai điều kiện đều thỏa.

**(d) Lập luận bỏ mẫu bóng.**

**Bước 1: vế phải.** Mọi tập hữu hạn bị $\mathcal M_{[0,1]}$ tách trọn (Ví dụ 03.6, Bước 1), nên $\Pi(m)=2^m$. Tại $m=1000$, $\delta=0{,}05$:
$$
\begin{aligned}
&\frac{1000\ln2+\ln40}{2000}\\
&\quad\approx\frac{693{,}15+3{,}69}{2000}\approx0{,}3484,
\end{aligned}
$$
và căn bậc hai cho khoảng $0{,}590$.

**Bước 2: so với độ lệch thật.** Theo Ví dụ 03.6, Bước 2, độ lệch đều bằng $1$ trên mọi mẫu. Biến cố "độ lệch đều không quá $0{,}590$" có xác suất $0$, nên lập luận sai.

**Bước 3: chỗ sai.** Một cách gán nhãn trên $S$ không xác định $L_D(h)$, nên không ứng với một biến cố hỏng duy nhất. Tập các cách gán nhãn còn phụ thuộc $S$. Đó là lý do (i), (ii) ở §7 của ghi chú.

**Bước 4: cách sửa.** Bước 1 của chứng minh Định lý 03.15 thay $L_D$ bằng $L_{S'}$, nên mọi đại lượng chỉ phụ thuộc cách gán nhãn trên $2m$ điểm. Sau Bước 2, nguồn ngẫu nhiên còn lại là $\sigma$, độc lập với các cách gán nhãn (Bước 3).

**(e) So với lớp đã rời rạc hóa.**

**Bước 1: cỡ mẫu.** $2K/\delta\le2^{193}\cdot20$, nên
$$
\begin{aligned}
\ln\frac{2K}\delta&\le193\ln2+\ln20\\
&\approx133{,}777+2{,}996\\
&=136{,}773,
\end{aligned}
$$
và cỡ mẫu là $\lceil200\cdot136{,}773\rceil=\lceil27\,354{,}6\rceil=27\,355$.

**Bước 2: tỉ số.** $132\,992/27\,355\approx4{,}86$.

**Bước 3: tách tỉ số.** Tại $m=132\,992$, ngoặc của cận VC là $3\ln(2em/3)+\ln80\approx37{,}178+4{,}382=41{,}560$. Do đó
$$
\begin{aligned}
\frac{32\cdot41{,}560}{2\cdot136{,}773}&=16\cdot0{,}3039\\
&\approx4{,}86 .
\end{aligned}
$$
Hằng số làm cận VC lớn gấp $16$ lần. Số hạng lôgarit của cận VC chỉ bằng khoảng $30\%$ số hạng $\ln(2K/\delta)$, vì $d\ln(2em/d)$ đếm cách gán nhãn còn $\ln K$ đếm các giá trị $64$ bit.

**(f) Chỗ dùng từng giả thiết** (lộ trình chứng minh và Phụ lục C).

- **(T1).** Bước 1 (C.2): $S'$ độc lập với $S$, để dùng Bổ đề 02.3 khi biết $S$. Bước 2 (C.3): các cặp $(Z_i,Z'_i)$ độc lập cùng phân bố, để đổi chỗ không làm đổi phân bố.
- **Tính bị chặn của hàm lỗi.** Bước 1 (C.2): phương sai không quá $\tfrac14$. Bước 4 (C.4): các số hạng $\sigma_i(\ell(h,Z'_i)-\ell(h,Z_i))$ nằm trong $[-1,1]$ để dùng Định lý 02.7.
- **(T5).** Bước 3 (C.4): số cách gán nhãn trên mẫu gộp không quá $\Pi_{\mathcal H}(2m)$ vì lớp không đổi theo $(S,S')$. Bài tập 03.5(c) và Ví dụ 03.8 cho thấy bước này hỏng khi bỏ (T5).
- **(M).** Bước 1 (C.1): các cận trên đúng đo được và $h_S$ được chọn đo được theo $S$; C.7 dùng lại tính đo được cho phần (c) của định lý.

**Kiểm tra lại.** $32\cdot41{,}560/0{,}01\approx132\,991$, khớp với $132\,992$ sau khi làm tròn lên ở Ví dụ 03.9.
:::

### Bài tập 03.5 (Số tham số, lớp chọn sau khi xem mẫu và chiều VC)

**Mức độ:** chứng minh, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 5; dựng phản ví dụ khi thay chiều VC bằng số tham số và khi lớp được chọn sau khi xem mẫu.

::: exercise Bài tập 03.5
**(a)** Trên $\mathbb R$, xét lớp $\mathcal H_{\sin}=\{x\mapsto\mathbb 1[\sin(\theta x)>0]:\ \theta\in\mathbb R\}$. Cho $k\ge1$, các điểm $x_i=2^{-i}$, $i=1,\ldots,k$, một cách gán nhãn $y\in\{0,1\}^k$, và
$$
\theta=\pi\Big(1+\sum_{j=1}^{k}(1-y_j)2^j\Big).
$$
Chứng minh $\mathbb 1[\sin(\theta x_i)>0]=y_i$ với mọi $i$, rồi suy ra khẳng định $d=\infty$ của Nhận xét 03.10(ii).

**(b)** Nhận xét 03.10(iii) có một lớp $p$ tham số với chiều VC bằng $1$. Dùng lớp đó và (a) để chứng minh số tham số thực dùng để viết một lớp không là cận trên của chiều VC, và cũng không là cận dưới. Vì sao đẳng thức $d=p+1$ của $\mathcal H^p_{\mathrm{aff}}$ không mâu thuẫn với kết luận này?

**(c)** Cho phân bố $D$ trên $[0,1]\times\{0,1\}$: $X\sim U[0,1]$ và $Y$ có phân bố $\mathrm{Bernoulli}(\tfrac12)$, độc lập với $X$. Sau khi xem mẫu $S\sim D^m$, đặt $F_1=\{X_i:\ Y_i=1\}$ và chọn lớp một hàm $\mathcal G_S=\{\mathbb 1_{F_1}\}$.

- Tìm chiều VC của $\mathcal G_S$.
- Chứng minh rằng với xác suất $1$, độ lệch đều trên $\mathcal G_S$ bằng $\tfrac12$.
- Tính bán kính $\rho_m$ của Định lý 03.15(a), áp dụng như thể $\mathcal G_S$ cố định, tại $m=1000$, $\delta=0{,}05$, và xác định giả thiết bị vi phạm.
- So sánh với cận của Định lý 02.7(c) cho một hàm chọn trước khi lấy mẫu.
:::

::: hint Gợi ý 1
Phần (a). Viết $\theta x_i/\pi=N_i+f_i$ với $N_i$ nguyên và $0<f_i<1$; khi đó dấu của $\sin(\theta x_i)$ là dấu của $(-1)^{N_i}$.
:::

::: hint Gợi ý 2
Phần (a). Tách tổng $\sum_j(1-y_j)2^{j-i}$ thành ba phần $j>i$, $j=i$, $j<i$. Phần $j>i$ là số nguyên chẵn; phần $j<i$ cộng với $2^{-i}$ nằm trong $[2^{-i},1-2^{-i}]$.
:::

::: hint Gợi ý 3
Phần (c). $U[0,1]$ không có nguyên tử (atom), nên với xác suất $1$ các $X_i$ đôi một khác nhau và một điểm mới $X$ không thuộc tập hữu hạn $F_1$. Lớp một hàm có $\Pi_{\mathcal G_S}(m)=1$.
:::

::: solution Lời giải Bài tập 03.5
**(a) Một tham số, chiều VC vô hạn.**

**Bước 1: tách tổng.** Với mỗi $i$,
$$
\begin{aligned}
\frac{\theta x_i}\pi&=2^{-i}+\textstyle\sum_{j>i}(1-y_j)2^{j-i}\\
&\quad+(1-y_i)\\
&\quad+\textstyle\sum_{j<i}(1-y_j)2^{j-i}.
\end{aligned}
$$

**Bước 2: phần nguyên và phần lẻ.** Mỗi số hạng $2^{j-i}$ với $j>i$ là số chẵn, nên $E_i=\sum_{j>i}(1-y_j)2^{j-i}$ là số nguyên chẵn. Đặt $f_i=2^{-i}+\sum_{j<i}(1-y_j)2^{j-i}$. Khi đó
$$
\begin{aligned}
2^{-i}\le f_i&\le2^{-i}+\sum_{j=1}^{i-1}2^{j-i}\\
&=1-2^{-i},
\end{aligned}
$$
nên $0<f_i<1$, và $\theta x_i/\pi=N_i+f_i$ với $N_i=E_i+(1-y_i)$.

**Bước 3: dấu.** $\sin(\theta x_i)=\sin(\pi N_i+\pi f_i)=(-1)^{N_i}\sin(\pi f_i)$, với $\sin(\pi f_i)>0$. $N_i$ chẵn khi và chỉ khi $1-y_i=0$. Vậy $\sin(\theta x_i)>0$ khi và chỉ khi $y_i=1$.

**Bước 4: kết luận.** Với mọi $k$, tập $\{2^{-1},\ldots,2^{-k}\}$ bị tách trọn, nên $d=\infty$, dù lớp chỉ có một tham số.

**(b) Số tham số và chiều VC.**

**Bước 1: không là cận trên.** Theo (a), lớp một tham số $\mathcal H_{\sin}$ có $d=\infty$.

**Bước 2: không là cận dưới.** Lớp của Nhận xét 03.10(iii) có $p$ tham số $w_1,\ldots,w_p$ nhưng chỉ gồm ba hàm $\mathbb 1[x\ge0]$, $\mathbb 1[x\le0]$, hằng $1$, và có $d=1$. Với $p\ge2$, $d<p$.

**Bước 3: nửa không gian afin.** Với $\mathcal H^p_{\mathrm{aff}}$, đẳng thức $d=p+1$ được chứng minh riêng cho lớp đó (Mệnh đề 03.9), không suy ra từ việc đếm tham số.

**(c) Một hàm chọn sau khi xem mẫu.**

**Bước 1: chiều VC.** Một hàm cho đúng một cách gán nhãn trên mỗi điểm, nên không điểm nào bị tách trọn và chiều VC bằng $0$.

**Bước 2: rủi ro thực nghiệm.** Với xác suất $1$, các $X_i$ đôi một khác nhau, nên $\mathbb 1_{F_1}(X_i)=Y_i$ với mọi $i$ và $L_S(\mathbb 1_{F_1})=0$.

**Bước 3: rủi ro kì vọng.** Cặp mới $(X,Y)$ độc lập với $S$, và $\Pr(X\in F_1)=0$ vì $F_1$ hữu hạn. Do đó hàm dự đoán $0$ hầu chắc chắn và sai khi $Y=1$, nên $L_D(\mathbb 1_{F_1})=\tfrac12$. Độ lệch đều bằng $\tfrac12$ với xác suất $1$.

**Bước 4: áp dụng sai Định lý 03.15.** Với $\Pi=1$ (đoạn sau Định lý 03.15, trường hợp $d=0$),
$$
\begin{aligned}
\rho_{1000}&=\sqrt{8\ln80/1000}\\
&\approx\sqrt{0{,}03506}\\
&\approx0{,}187<\tfrac12 .
\end{aligned}
$$
Mâu thuẫn xảy ra vì $\mathcal G_S$ phụ thuộc $S$, trái (T5). Ở Bước 3 của chứng minh, khi đổi chỗ $Z_i\leftrightarrow Z'_i$, lớp cũng đổi theo, như Ví dụ 03.8.

**Bước 5: so với một hàm cố định.** Với $h$ chọn trước khi lấy mẫu, Định lý 02.7(c) cho, với xác suất ít nhất $0{,}95$,
$$
\begin{aligned}
&\lvert L_S(h)-L_D(h)\rvert\\
&\quad\le\sqrt{\ln40/2000}\\
&\quad\approx0{,}043 .
\end{aligned}
$$
Hàm $\mathbb 1_{F_1}$ được chọn sau khi xem mẫu nên có độ lệch $\tfrac12$.

**Kiểm tra lại.** Với $k=3$ và $y=(1,0,1)$, $\theta=\pi(1+4)=5\pi$; ba góc $5\pi/2$, $5\pi/4$, $5\pi/8$ có sin bằng $1$, $-\tfrac{\sqrt2}2$, khoảng $0{,}924$, cho nhãn $1$, $0$, $1$.
:::

### Bài tập 03.6 (Một cách chứng minh khác của bổ đề Sauer–Shelah, tùy chọn)

**Mức độ:** chứng minh (tùy chọn, thử thách). **Mục tiêu:** mục tiêu học tập 2; chặn số cách gán nhãn bằng số tập con bị tách trọn qua phép dồn, rồi suy ra bổ đề Sauer–Shelah.

::: exercise Bài tập 03.6
Cho $n\ge1$ và tập khác rỗng $Y\subseteq\{0,1\}^n$, coi như một lớp hàm trên tập vị trí $\{1,\ldots,n\}$ như ở Phụ lục B; kí hiệu $\operatorname{sh}(Y)$ là họ các tập vị trí bị $Y$ tách trọn, kể cả tập rỗng. Với $y\in\{0,1\}^n$ và vị trí $i$, gọi $y^{(i)}$ là véc-tơ thu được từ $y$ khi đặt tọa độ thứ $i$ bằng $0$. *Phép dồn* (shifting) theo vị trí $i$ biến mỗi $y\in Y$ thành $T_i(y)=y^{(i)}$ khi $y_i=1$ và $y^{(i)}\notin Y$, và giữ $T_i(y)=y$ trong các trường hợp còn lại; đặt $T_i(Y)=\{T_i(y):\ y\in Y\}$.

**(a)** Chứng minh $T_i$ là đơn ánh trên $Y$, nên $\lvert T_i(Y)\rvert=\lvert Y\rvert$.

**(b)** Chứng minh $\operatorname{sh}(T_i(Y))\subseteq\operatorname{sh}(Y)$.

**(c)** Đặt $w(Y)=\sum_{y\in Y}\sum_{j=1}^{n}y_j$. Chứng minh nếu $T_i(Y)\ne Y$ thì $w(T_i(Y))<w(Y)$. Suy ra khi áp dụng lặp lại $T_1,\ldots,T_n$, sau hữu hạn bước ta được tập $Y^*$ với $T_i(Y^*)=Y^*$ với mọi $i$.

**(d)** Chứng minh $Y^*$ tách trọn tập vị trí $\{j:\ y_j=1\}$ của mỗi $y\in Y^*$. Suy ra $\lvert Y\rvert\le\lvert\operatorname{sh}(Y)\rvert$, rồi suy ra Bổ đề 03.12(a).

Bài tập 03.8(a) chứng minh bất đẳng thức của (d) bằng quy nạp.
:::

::: hint Gợi ý 1
Phần (a). Nếu $T_i(y)=T_i(y')$ với $y\ne y'$, xét ba trường hợp: phép dồn không đổi véc-tơ nào, đổi cả hai, hay đổi đúng một. Phần (c). Mỗi véc-tơ bị đổi mất đúng một tọa độ bằng $1$.
:::

::: hint Gợi ý 2
Phần (b). Tách hai trường hợp $i\notin B$ và $i\in B$. Nếu $u\in T_i(Y)$ và $u_i=1$ thì $u$ không bị đổi, nên $u\in Y$ và $u^{(i)}\in Y$.
:::

::: hint Gợi ý 3
Phần (d). Từ $T_j(Y^*)=Y^*$: nếu $y\in Y^*$ và $y_j=1$ thì $y^{(j)}\in Y^*$. Lặp lại, mọi véc-tơ $z\le y$ theo từng tọa độ đều thuộc $Y^*$.
:::

::: solution Lời giải Bài tập 03.6
**(a) Phép dồn là đơn ánh.** Giả sử $y\ne y'$ thuộc $Y$ và $T_i(y)=T_i(y')$.

- **Không véc-tơ nào bị đổi.** Khi đó $y=y'$, vô lý.
- **Cả hai bị đổi.** Khi đó $y^{(i)}=y'^{(i)}$ và $y_i=y'_i=1$, nên $y=y'$, vô lý.
- **Chỉ $y$ bị đổi.** Khi đó $y^{(i)}=y'\in Y$, trái với điều kiện đổi $y^{(i)}\notin Y$.

Vậy $T_i$ là đơn ánh.

**(b) Tập bị tách trọn không tăng.** Cho $B\in\operatorname{sh}(T_i(Y))$.

**Bước 1: $i\notin B$.** $T_i$ chỉ đổi tọa độ thứ $i$, nên $T_i(y)$ và $y$ trùng nhau trên $B$. Hai tập $T_i(Y)$ và $Y$ cho cùng các cách gán nhãn trên $B$, nên $B\in\operatorname{sh}(Y)$.

**Bước 2: một nhận xét.** Nếu $u=T_i(y)$ có $u_i=1$ thì $y_i=1$ và $y$ không bị đổi, nên $u=y\in Y$ và $y^{(i)}\in Y$.

**Bước 3: $i\in B$.** Lấy một cách gán nhãn $z$ của $B$. Nếu $z_i=1$, véc-tơ $u\in T_i(Y)$ khớp $z$ trên $B$ có $u_i=1$, nên $u\in Y$ theo Bước 2. Nếu $z_i=0$, gọi $z'$ là $z$ với tọa độ $i$ đổi thành $1$ và lấy $u\in T_i(Y)$ khớp $z'$; theo Bước 2, $u^{(i)}\in Y$, và $u^{(i)}$ khớp $z$ trên $B$. Vậy $B\in\operatorname{sh}(Y)$.

**(c) Quá trình dừng.**

**Bước 1: đếm $w$.** Theo (a), $T_i$ là song ánh từ $Y$ lên $T_i(Y)$. Mỗi véc-tơ bị đổi mất đúng một tọa độ $1$, nên $w(T_i(Y))=w(Y)-k$, với $k$ là số véc-tơ bị đổi. Nếu $T_i(Y)\ne Y$ thì $k\ge1$ và $w$ giảm.

**Bước 2: dừng.** Vì $w$ là số nguyên không âm, chỉ có hữu hạn lần giảm; quá trình dừng ở $Y^*$ khi một lượt $T_1,\ldots,T_n$ không đổi gì. Theo (a) và (b), $\lvert Y^*\rvert=\lvert Y\rvert$ và $\operatorname{sh}(Y^*)\subseteq\operatorname{sh}(Y)$.

**(d) Kết luận.**

**Bước 1: $Y^*$ đóng khi giảm.** Theo Bước 1 của (c), $w(T_j(Y^*))=w(Y^*)-k$; vì $T_j(Y^*)=Y^*$ nên $k=0$, tức $T_j$ không đổi véc-tơ nào của $Y^*$. Do đó nếu $y\in Y^*$ và $y_j=1$ thì $y^{(j)}\in Y^*$. Lặp lại, mọi $z$ với $z\le y$ theo từng tọa độ đều thuộc $Y^*$.

**Bước 2: tách trọn giá của $y$.** Đặt $B=\{j:\ y_j=1\}$. Với mỗi cách gán nhãn của $B$, véc-tơ $z$ bằng cách gán nhãn đó trên $B$ và bằng $0$ ngoài $B$ thỏa $z\le y$, nên $z\in Y^*$. Vậy $B\in\operatorname{sh}(Y^*)$.

**Bước 3: đếm.** $y$ là véc-tơ chỉ thị của $B$, nên $y\mapsto B$ là đơn ánh, và
$$
\begin{aligned}
\lvert Y\rvert=\lvert Y^*\rvert&\le\lvert\operatorname{sh}(Y^*)\rvert\\
&\le\lvert\operatorname{sh}(Y)\rvert .
\end{aligned}
$$

**Bước 4: bổ đề Sauer–Shelah.** Cho bộ $C=(x_1,\ldots,x_m)$ và $Y=\mathcal H_C$. Như Bước 6 của Phụ lục B, một tập vị trí bị $Y$ tách trọn gồm các điểm đôi một khác nhau bị $\mathcal H$ tách trọn, nên có nhiều nhất $d$ phần tử. Do đó $\lvert\mathcal H_C\rvert\le\lvert\operatorname{sh}(Y)\rvert\le\sum_{j=0}^{d}\binom mj$; lấy giá trị lớn nhất theo $C$ được Bổ đề 03.12(a).

**Kiểm tra lại.** Với $Y=\{00,10,11\}$, $T_1$ giữ $10$ (vì $00\in Y$) và đổi $11$ thành $01$; $T_1(Y)=\{00,10,01\}$ cố định với $T_2$. Ta có $\lvert\operatorname{sh}(Y)\rvert=\lvert\{\varnothing,\{1\},\{2\}\}\rvert=3=\lvert Y\rvert$.
:::

## Bài tập chọn từ UML

### Bài tập 03.7 (Chiều VC của hai lớp trên tập hữu hạn; UML Bài tập 6.2)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 1; tính chiều VC bằng điều kiện cần và đủ để một tập bị tách trọn.

::: exercise Bài tập 03.7
Cho tập hữu hạn $\mathcal X$ có $n\ge1$ phần tử và số nguyên $k$ với $0\le k\le n$. Với $h:\mathcal X\to\{0,1\}$, gọi $\lvert h\rvert$ là số điểm có nhãn $1$. Xét hai lớp
$$
\begin{aligned}
\mathcal H_{=k}&=\{h:\ \lvert h\rvert=k\},\\
\mathcal H^{0/1}_{\le k}&=\{h:\ \lvert h\rvert\le k\\
&\qquad\vee\ n-\lvert h\rvert\le k\}.
\end{aligned}
$$
Lớp thứ hai gồm các hàm có nhiều nhất $k$ nhãn $1$ hoặc nhiều nhất $k$ nhãn $0$.

**(a)** Chứng minh $\operatorname{VCdim}(\mathcal H_{=k})=\min\{k,n-k\}$.

**(b)** Chứng minh $\operatorname{VCdim}(\mathcal H^{0/1}_{\le k})=\min\{2k+1,n\}$.
:::

::: hint Gợi ý 1
Một tập $C$ có $c$ phần tử bị tách trọn khi và chỉ khi mọi cách gán nhãn của $C$ mở rộng được thành một hàm của lớp trên cả $\mathcal X$. Với cả hai lớp, khả năng mở rộng chỉ phụ thuộc số nhãn $1$ của cách gán nhãn, gọi là $s$.
:::

::: hint Gợi ý 2
Phần (a). Có một mở rộng với đúng $k$ nhãn $1$ khi và chỉ khi $0\le k-s\le n-c$. Phần (b). Để có ít nhãn $1$ nhất, gán $0$ cho mọi điểm ngoài $C$; để có ít nhãn $0$ nhất, gán $1$.
:::

::: hint Gợi ý 3
Phần (b). Nếu $c\ge2k+2$, xét cách gán nhãn có $s=k+1$.
:::

::: solution Lời giải Bài tập 03.7
**Bước 1: rút về số nhãn $1$.** Cho $C\subseteq\mathcal X$ có $c$ phần tử và một cách gán nhãn $z$ của $C$ có $s$ nhãn $1$, $0\le s\le c$. Một mở rộng của $z$ chọn nhãn cho $n-c$ điểm ngoài $C$; nếu $t$ trong số đó nhận nhãn $1$ thì hàm có $s+t$ nhãn $1$, với $0\le t\le n-c$.

**(a) Lớp $\mathcal H_{=k}$.**

**Bước 2: điều kiện cho một cách gán nhãn.** Có mở rộng thuộc $\mathcal H_{=k}$ khi và chỉ khi tồn tại $t=k-s$ với $0\le k-s\le n-c$.

**Bước 3: điều kiện cho mọi cách gán nhãn.** $C$ bị tách trọn khi và chỉ khi điều kiện đúng với mọi $s\in\{0,\ldots,c\}$. Với $s=c$, cần $c\le k$; với $s=0$, cần $k\le n-c$, tức $c\le n-k$. Ngược lại, nếu $c\le\min\{k,n-k\}$ thì với mọi $s\le c$, ta có $k-s\ge k-c\ge0$ và $k-s\le k\le n-c$.

**Bước 4: kết luận.** Mọi tập có $\min\{k,n-k\}$ phần tử bị tách trọn và không tập lớn hơn nào bị tách trọn, nên $\operatorname{VCdim}(\mathcal H_{=k})=\min\{k,n-k\}$.

**(b) Lớp $\mathcal H^{0/1}_{\le k}$.**

**Bước 2: điều kiện cho một cách gán nhãn.** Gán $0$ ngoài $C$ cho hàm có đúng $s$ nhãn $1$, ít nhất có thể; gán $1$ ngoài $C$ cho hàm có đúng $c-s$ nhãn $0$, ít nhất có thể. Vậy $z$ mở rộng được khi và chỉ khi $s\le k$ hoặc $c-s\le k$.

**Bước 3: điều kiện cho mọi cách gán nhãn.** Nếu $c\le2k+1$ và $s>k$ thì $s\ge k+1\ge c-k$, tức $c-s\le k$; mọi $s$ đều thỏa. Nếu $c\ge2k+2$, giá trị $s=k+1\le c$ cho $s>k$ và $c-s\ge k+1>k$; cách gán nhãn đó không mở rộng được.

**Bước 4: kết luận.** $C$ bị tách trọn khi và chỉ khi $c\le2k+1$; vì $c\le n$, $\operatorname{VCdim}(\mathcal H^{0/1}_{\le k})=\min\{2k+1,n\}$.

**Kiểm tra lại.** Với $n=5$, $k=1$: (a) cho $1$, vì hai điểm không nhận được cách gán nhãn $(1,1)$; (b) cho $3$: trên bốn điểm, cách gán nhãn có hai nhãn $1$ và hai nhãn $0$ không mở rộng được.
:::

### Bài tập 03.8 (Bốn trường hợp dấu bằng của bổ đề Sauer–Shelah; UML Bài tập 6.4)

**Mức độ:** chứng minh, khái niệm. **Mục tiêu:** mục tiêu học tập 2; chặn số cách gán nhãn bằng số tập con bị tách trọn, và nhận ra khi nào mỗi bất đẳng thức của bổ đề Sauer–Shelah đạt dấu bằng.

::: exercise Bài tập 03.8
Cho lớp $\mathcal H$ khác rỗng các hàm $\mathcal X\to\{0,1\}$ có chiều VC $d<\infty$ và tập hữu hạn $C\subseteq\mathcal X$ có $n$ phần tử.

**(a)** Gọi $\operatorname{sh}_{\mathcal H}(C)$ là họ các tập con $B\subseteq C$ bị $\mathcal H$ tách trọn, kể cả tập rỗng. Chứng minh
$$
\lvert\mathcal H_C\rvert\le\lvert\operatorname{sh}_{\mathcal H}(C)\rvert\le\sum_{j=0}^{d}\binom nj .
$$
Chứng minh bất đẳng thức thứ nhất bằng quy nạp theo $n$, đồng thời cho mọi lớp khác rỗng.

**(b)** Trên $\mathbb R$, xét lớp hai hàm $\mathcal G=\{g_0,g_1\}$ với $g_0\equiv0$ và $g_1(x)=\mathbb 1[x\ge0]$. Chứng minh $\operatorname{VCdim}(\mathcal G)=1$. Tìm bốn tập hữu hạn $C\subseteq\mathbb R$ sao cho hai bất đẳng thức của (a) lần lượt cho bốn tổ hợp $(=,=)$, $(<,=)$, $(=,<)$, $(<,<)$.

**(c)** Chứng minh với $\mathcal H_{\mathrm{thr}}$, cả hai bất đẳng thức của (a) là đẳng thức với mọi tập hữu hạn khác rỗng $C\subseteq\mathbb R$.
:::

::: hint Gợi ý 1
Phần (a). Tách $C=C'\cup\{x\}$ như Bước 1 của chứng minh Bổ đề 03.12: $\lvert\mathcal H_C\rvert=\lvert\mathcal H_{C'}\rvert+\lvert Y_1\rvert$, với $Y_1$ là tập các cách gán nhãn của $C'$ mở rộng được theo cả hai nhãn của $x$.
:::

::: hint Gợi ý 2
Phần (a). $Y_1$ là thu hẹp lên $C'$ của lớp con $\mathcal H'\subseteq\mathcal H$ gồm các $h$ có cách gán nhãn trên $C'$ thuộc $Y_1$. Nếu $\mathcal H'$ tách trọn $B\subseteq C'$ thì $\mathcal H$ tách trọn $B\cup\{x\}$. Phần (b). Điểm $x$ bị $\mathcal G$ tách trọn khi và chỉ khi $x\ge0$.
:::

::: hint Gợi ý 3
Phần (b). Thử $C=\{1\}$, $\{1,2\}$, $\{-1,1\}$, $\{-1,1,2\}$.
:::

::: solution Lời giải Bài tập 03.8
**(a) Hai bất đẳng thức.**

**Bước 1: bất đẳng thức thứ hai.** Một tập bị tách trọn có nhiều nhất $d$ phần tử, và $C$ có $\binom nj$ tập con $j$ phần tử.

**Bước 2: khẳng định quy nạp.** Khẳng định $P(n)$: với mọi lớp khác rỗng $\mathcal H$ và mọi tập $C$ có $n$ phần tử, $\lvert\mathcal H_C\rvert\le\lvert\operatorname{sh}_{\mathcal H}(C)\rvert$. Với $n=0$, $\mathcal H_\varnothing$ chỉ có cách gán nhãn rỗng, và tập rỗng bị tách trọn, nên hai vế bằng $1$.

**Bước 3: tách điểm cuối.** Cho $n\ge1$, $C=C'\cup\{x\}$ với $x\notin C'$, và gọi $Y_1$ là tập các cách gán nhãn của $C'$ mở rộng được theo cả hai nhãn của $x$. Mỗi cách gán nhãn trong $\mathcal H_{C'}$ mở rộng thành một hoặc hai cách gán nhãn của $C$, và thành hai khi và chỉ khi nó thuộc $Y_1$. Do đó $\lvert\mathcal H_C\rvert=\lvert\mathcal H_{C'}\rvert+\lvert Y_1\rvert$.

**Bước 4: số hạng thứ nhất.** Theo $P(n-1)$, $\lvert\mathcal H_{C'}\rvert$ không vượt quá số tập con của $C$ bị tách trọn và không chứa $x$.

**Bước 5: số hạng thứ hai.** Nếu $Y_1=\varnothing$, số hạng này bằng $0$. Nếu $Y_1\ne\varnothing$, lớp con $\mathcal H'\subseteq\mathcal H$ gồm các $h$ có cách gán nhãn trên $C'$ thuộc $Y_1$ là khác rỗng, và $(\mathcal H')_{C'}=Y_1$. Theo $P(n-1)$, $\lvert Y_1\rvert\le\lvert\operatorname{sh}_{\mathcal H'}(C')\rvert$.

**Bước 6: chuyển sang $\mathcal H$.** Giả sử $\mathcal H'$ tách trọn $B\subseteq C'$. Mỗi cách gán nhãn của $B$ khớp với một $u\in Y_1$, và cả hai mở rộng của $u$ theo nhãn của $x$ thuộc $\mathcal H_C$. Vậy $\mathcal H$ tách trọn $B\cup\{x\}$, và $B\mapsto B\cup\{x\}$ là đơn ánh vào họ các tập con bị tách trọn chứa $x$.

**Bước 7: cộng lại.** Hai họ ở Bước 4 và Bước 6 rời nhau và hợp lại nằm trong $\operatorname{sh}_{\mathcal H}(C)$, nên $\lvert\mathcal H_C\rvert\le\lvert\operatorname{sh}_{\mathcal H}(C)\rvert$.

**(b) Một lớp, bốn tổ hợp.**

**Bước 1: chiều VC.** Với $x\ge0$, $g_0(x)=0$ và $g_1(x)=1$, nên $\{x\}$ bị tách trọn; với $x<0$, cả hai hàm cho $0$. Hai điểm cần bốn cách gán nhãn, nhiều hơn hai hàm, nên $d=1$ và vế phải của (a) là $1+n$.

**Bước 2: bảng.** Với mọi $C$ chứa một điểm không âm, $\lvert\mathcal G_C\rvert=2$; các tập bị tách trọn là $\varnothing$ và các điểm không âm đơn lẻ. Xét $C_1=\{1\}$, $C_2=\{1,2\}$, $C_3=\{-1,1\}$, $C_4=\{-1,1,2\}$; cột $\lvert\operatorname{sh}\rvert$ ghi $\lvert\operatorname{sh}_{\mathcal G}(C)\rvert$.

| $C$ | $\lvert\mathcal G_C\rvert$ | $\lvert\operatorname{sh}\rvert$ | $1+n$ |
|---|---|---|---|
| $C_1$ | $2$ | $2$ | $2$ |
| $C_2$ | $2$ | $3$ | $3$ |
| $C_3$ | $2$ | $2$ | $3$ |
| $C_4$ | $2$ | $3$ | $4$ |

Bốn hàng cho lần lượt $(=,=)$, $(<,=)$, $(=,<)$, $(<,<)$.

**Bước 3: đọc bảng.** Bất đẳng thức thứ nhất là bất đẳng thức nghiêm ngặt khi $C$ có ít nhất hai điểm không âm: mỗi điểm cho một tập bị tách trọn, nhưng lớp chỉ có hai hàm. Bất đẳng thức thứ hai là bất đẳng thức nghiêm ngặt khi $C$ có ít nhất một điểm âm: tập một điểm đó không bị tách trọn.

**(c) Hàm ngưỡng.**

**Bước 1: số cách gán nhãn.** Với $C$ có $n\ge1$ điểm, $\lvert(\mathcal H_{\mathrm{thr}})_C\rvert=n+1$ (Ví dụ 03.4, Bước 1).

**Bước 2: số tập bị tách trọn.** Mọi tập một điểm $\{x\}$ bị tách trọn, vì $h_x(x)=1$ và $h_{x+1}(x)=0$. Theo Bước 2 của chứng minh Mệnh đề 03.5, không tập hai điểm nào bị tách trọn. Vậy số tập bị tách trọn là $1+n$.

**Bước 3: kết luận.** Vế phải với $d=1$ cũng là $1+n$. Đây là lý do Bổ đề 03.12(a) đạt dấu bằng ở Ví dụ 03.5, Bước 1.

**Kiểm tra lại.** Với $\mathcal H_{\mathrm{thr}}$ và $C=\{1,2,3\}$: bốn cách gán nhãn $000$, $001$, $011$, $111$; các tập bị tách trọn là $\varnothing$ và ba tập một điểm; tổng nhị thức là $1+3=4$.
:::

### Bài tập 03.9 (Hình chữ nhật song song với trục trong $\mathbb R^p$; UML Bài tập 6.5)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 1; cận dưới bằng một tập tường minh, cận trên cho mọi tập $2p+1$ điểm.

::: exercise Bài tập 03.9
Cho $p\ge1$. Với $a_j\le b_j$, $j=1,\ldots,p$, tập $R=[a_1,b_1]\times\cdots\times[a_p,b_p]$ là một hình chữ nhật song song với trục trong $\mathbb R^p$ và $h_R(x)=\mathbb 1[x\in R]$. Lớp $\mathcal H^p_{\mathrm{rec}}$ gồm mọi $h_R$ và hàm $h_\varnothing\equiv0$; với $p=2$, đây là lớp $\mathcal H_{\mathrm{rec}}$ của Bài tập 02.7. Chứng minh $\operatorname{VCdim}(\mathcal H^p_{\mathrm{rec}})=2p$. Trường hợp $p=2$ là câu hỏi cuối buổi của ghi chú.
:::

::: hint Gợi ý 1
Cận dưới: tìm $2p$ điểm, hai điểm trên mỗi trục tọa độ, đối xứng qua gốc. Cận trên: với mỗi tọa độ $j$, chọn một điểm có tọa độ thứ $j$ nhỏ nhất và một điểm có tọa độ thứ $j$ lớn nhất trong tập.
:::

::: hint Gợi ý 2
Cận dưới: dùng $\pm\mathbf e_1,\ldots,\pm\mathbf e_p$. Khi $a_l\le0\le b_l$ với mọi $l$, hình chữ nhật chứa $\mathbf e_j$ khi và chỉ khi $b_j\ge1$.
:::

::: hint Gợi ý 3
Cận trên: một hình chữ nhật chứa mọi điểm được chọn thì chứa, ở mỗi tọa độ, đoạn từ giá trị nhỏ nhất đến giá trị lớn nhất của tập.
:::

::: solution Lời giải Bài tập 03.9
**Bước 1: tập và tham số.** Lấy $C=\{\mathbf e_1,\ldots,\mathbf e_p,-\mathbf e_1,\ldots,-\mathbf e_p\}$, gồm $2p$ điểm phân biệt, và gọi $P$ là tập các điểm nhận nhãn $1$ trong một cách gán nhãn. Với mỗi $j$, đặt $a_j=-1$ khi $-\mathbf e_j\in P$ và $a_j=-\tfrac12$ khi ngược lại; đặt $b_j=1$ khi $\mathbf e_j\in P$ và $b_j=\tfrac12$ khi ngược lại.

**Bước 2: cận dưới.** Vì $a_l\le-\tfrac12<0<\tfrac12\le b_l$, mọi tọa độ bằng $0$ nằm trong đoạn tương ứng. Do đó $\mathbf e_j\in R$ khi và chỉ khi $b_j\ge1$, tức $\mathbf e_j\in P$; tương tự $-\mathbf e_j\in R$ khi và chỉ khi $-\mathbf e_j\in P$. Khi $P=\varnothing$, $R=[-\tfrac12,\tfrac12]^p$ không chứa điểm nào của $C$. Vậy $C$ bị tách trọn và $d\ge2p$.

**Bước 3: cận trên, chọn điểm.** Lấy một tập $2p+1$ điểm phân biệt. Với mỗi $j$, chọn một điểm có tọa độ thứ $j$ nhỏ nhất và một điểm có tọa độ thứ $j$ lớn nhất. Có nhiều nhất $2p$ điểm được chọn, nên còn ít nhất một điểm $x$. Gán nhãn $1$ cho các điểm được chọn và nhãn $0$ cho mọi điểm còn lại, trong đó có $x$.

**Bước 4: cách gán nhãn không thực hiện được.** Nếu $h_R$ thực hiện nó, $R$ chứa các điểm được chọn. Khi đó, với mọi $j$, $a_j$ không lớn hơn giá trị nhỏ nhất và $b_j$ không nhỏ hơn giá trị lớn nhất của tọa độ thứ $j$ trên tập. Do đó $R$ chứa mọi điểm của tập, kể cả $x$, mâu thuẫn.

**Bước 5: hàm $h_\varnothing$.** Hàm $h_\varnothing$ gán nhãn $0$ cho các điểm được chọn, nên cũng không thực hiện được cách gán nhãn này. Vậy $d\le2p$.

**Bước 6: trường hợp $p=2$.** Khi đó $C$ là bốn điểm của câu hỏi cuối buổi, và Bước 3–5 là phần cận trên trong lời giải câu hỏi đó.

**Kiểm tra lại.** Với $p=1$, $\mathcal H^1_{\mathrm{rec}}$ là lớp khoảng đóng thêm $h_\varnothing$; trên tập hữu hạn, $h_\varnothing$ trùng một khoảng một điểm nằm ngoài tập, nên $2p=2$ khớp Mệnh đề 03.6.
:::

### Bài tập 03.10 (Lớp hội Boole; UML Bài tập 6.6)

**Mức độ:** chứng minh (phần (d) là phần thử thách). **Mục tiêu:** mục tiêu học tập 1; cận trên từ số phần tử của lớp, cận dưới bằng một tập tường minh, và vai trò của giả thiết $p\ge2$.

::: exercise Bài tập 03.10
Dùng định nghĩa của Bài tập 02.8: $\mathcal X=\{0,1\}^p$; $\mathcal U_p$ gồm $2p$ hàm $x\mapsto x_j$ và $x\mapsto\bar x_j=1-x_j$ (các biến hoặc phủ định của biến); với $L\subseteq\mathcal U_p$, hội $h_L(x)=\prod_{u\in L}u(x)$; hội của tập rỗng là hàm hằng $1$. Gọi $\mathcal H^p_{\mathrm{conj}}=\{h_L:\ L\subseteq\mathcal U_p\}$.

**(a)** Nhắc lại từ Bài tập 02.8(a): $\lvert\mathcal H^p_{\mathrm{conj}}\rvert\le3^p+1$.

**(b)** Với $p\ge2$, chứng minh $\operatorname{VCdim}(\mathcal H^p_{\mathrm{conj}})\le p\log_23$. Chứng minh khẳng định này sai khi $p=1$.

**(c)** Chứng minh $\mathcal H^p_{\mathrm{conj}}$ tách trọn $\{\mathbf e_1,\ldots,\mathbf e_p\}$.

**(d)** (Thử thách.) Với $p\ge2$, chứng minh $\operatorname{VCdim}(\mathcal H^p_{\mathrm{conj}})\le p$, nên chiều VC bằng $p$.

**(e)** Lớp *hội đơn điệu* (monotone conjunction) $\mathcal H^p_{\mathrm{mon}}$ gồm các $h_L$ với $L\subseteq\{x_1,\ldots,x_p\}$ (không có phủ định) và hàm $h_{\equiv0}$. Chứng minh $\operatorname{VCdim}(\mathcal H^p_{\mathrm{mon}})=p$ với mọi $p\ge1$.
:::

::: hint Gợi ý 1
Phần (b). $d$ là số nguyên và $2^d\le\lvert\mathcal H\rvert$; xét khi nào $2^d=3^p+1$. Phần (c). Với cách gán nhãn có tập chỉ số dương $J$, loại các véc-tơ $\mathbf e_j$, $j\notin J$, bằng phủ định của biến.
:::

::: hint Gợi ý 2
Phần (b). Xét số dư của $3^p+1$ khi chia cho $8$. Phần (d). Giả sử $C=\{c_1,\ldots,c_{p+1}\}$ bị tách trọn; lấy $h_i$ cho nhãn $0$ tại $c_i$ và nhãn $1$ tại các điểm khác, rồi chọn $u_i$ trong hội của $h_i$ với $u_i(c_i)=0$. Có $p+1$ hàm $u_i$ và chỉ $p$ biến. Phần (e). Đếm số hàm của $\mathcal H^p_{\mathrm{mon}}$; cho cận dưới, dùng các điểm $\mathbf 1-\mathbf e_j$, với $\mathbf 1=(1,\ldots,1)$.
:::

::: hint Gợi ý 3
Phần (d). Nếu $u_i$ và $u_j$ dùng cùng một biến thì chúng là phủ định của nhau; xét giá trị của chúng tại một điểm thứ ba $c_l$.
:::

::: solution Lời giải Bài tập 03.10
**(a) Số hàm.** Theo Bài tập 02.8(a), $\lvert\mathcal H^p_{\mathrm{conj}}\rvert=3^p+1$.

**(b) Cận theo số hàm.**

**Bước 1.** Tách trọn $d$ điểm cần $2^d$ hàm khác nhau, nên $2^d\le3^p+1$.

**Bước 2: $p\ge2$.** Giả sử $2^d=3^p+1$. Vì $3^p+1\ge10$, $d\ge4$ và $8$ chia hết $3^p+1$. Nhưng $3^2=9$ chia $8$ dư $1$, nên $3^p$ chia $8$ dư $3$ khi $p$ lẻ và dư $1$ khi $p$ chẵn; $3^p+1$ dư $4$ hoặc $2$, mâu thuẫn. Do đó $2^d\le3^p$, tức $d\le p\log_23$.

**Bước 3: $p=1$.** $\mathcal H^1_{\mathrm{conj}}=\{x_1,\bar x_1,1,0\}$ gồm cả bốn hàm trên $\{0,1\}$, nên tách trọn $\mathcal X$ và $d=2>\log_23\approx1{,}585$. Giả thiết $p\ge2$ không bỏ được.

**(c) Tách trọn các véc-tơ đơn vị.**

**Bước 1: chọn hội.** Cho cách gán nhãn với tập chỉ số dương $J$, lấy $L=\{\bar x_j:\ j\notin J\}$. Véc-tơ $\mathbf e_i$ chỉ có tọa độ thứ $i$ bằng $1$, nên $h_L(\mathbf e_i)=\prod_{j\notin J}(1-(\mathbf e_i)_j)$ bằng $1$ khi và chỉ khi $i\in J$.

**Bước 2: hai trường hợp biên.** $J=\{1,\ldots,p\}$ cho $L=\varnothing$, hàm hằng $1$; $J=\varnothing$ cho $h_L(\mathbf e_i)=0$ với mọi $i$. Vậy $d\ge p$.

**(d) Cận trên $p$.**

**Bước 1: các hàm $h_i$.** Giả sử $C=\{c_1,\ldots,c_{p+1}\}$ bị tách trọn và lấy $h_i=h_{L_i}$ với $h_i(c_i)=0$, $h_i(c_j)=1$ khi $j\ne i$.

**Bước 2: các hàm $u_i$.** Vì $h_i(c_i)=0$, có $u_i\in L_i$ với $u_i(c_i)=0$. Vì $h_i(c_j)=1$, mọi phần tử của $L_i$ bằng $1$ tại $c_j$, nên $u_i(c_j)=1$ với mọi $j\ne i$.

**Bước 3: chuồng bồ câu.** $p+1$ hàm $u_i$ dùng $p$ biến, nên có $i\ne j$ với $u_i$, $u_j$ cùng dùng biến $x_k$. Ta có $u_i(c_j)=1\ne0=u_j(c_j)$, nên $u_i\ne u_j$, tức $u_j=1-u_i$.

**Bước 4: điểm thứ ba.** Vì $p\ge2$, có chỉ số $l\notin\{i,j\}$. Theo Bước 2, $u_i(c_l)=1$ và $u_j(c_l)=1$, trái với $u_j=1-u_i$. Không tập $p+1$ điểm nào bị tách trọn; cùng (c), $d=p$. Với $p=1$ không có điểm thứ ba, khớp với Bước 3 của (b).

**(e) Hội đơn điệu.**

**Bước 1: các hàm khác nhau.** Gọi $\mathbf 1_L$ là véc-tơ có tọa độ $1$ đúng tại các chỉ số của biến trong $L$. Ta có $h_{L'}(\mathbf 1_L)=1$ khi và chỉ khi $L'\subseteq L$. Nếu $L\ne L'$, đổi vai trò nếu cần để $L'\not\subseteq L$; khi đó $h_{L'}(\mathbf 1_L)=0\ne1=h_L(\mathbf 1_L)$.

**Bước 2: cận trên.** Mọi $h_L$ bằng $1$ tại $\mathbf 1$, nên khác $h_{\equiv0}$. Vậy $\lvert\mathcal H^p_{\mathrm{mon}}\rvert=2^p+1$, và $2^d\le2^p+1<2^{p+1}$ cho $d\le p$.

**Bước 3: cận dưới.** Đặt $c_j=\mathbf 1-\mathbf e_j$. Khi đó $h_L(c_j)=1$ khi và chỉ khi $x_j\notin L$. Với tập chỉ số dương $J$, lấy $L=\{x_j:\ j\notin J\}$. Vậy $\{c_1,\ldots,c_p\}$ bị tách trọn và $d=p$.

**Kiểm tra lại.** Với $p=2$: (b) cho $2^d\le9$, tức $d\le3$; (d) và việc liệt kê mười hàm của $\mathcal H^2_{\mathrm{conj}}$ đều cho $d=2$.
:::

### Bài tập 03.11 (Chiều VC vô hạn kéo theo không học được PAC; UML Bài tập 6.10)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 5; chứng minh đầy đủ Định lý 03.17(a) và phép kéo theo (4)⇒(6) của Định lý 03.17(b), với hằng số tự dẫn ra, và phát biểu định lý cơ bản.

::: exercise Bài tập 03.11
Cho $\mathcal X$ có σ-đại số, lớp $\mathcal H$ khác rỗng các hàm đo được $\mathcal X\to\{0,1\}$, hàm lỗi 0–1 và thuật toán học theo Định nghĩa 01.4.

**(a)** Giả sử $\mathcal H$ tách trọn một tập $C$ có $k$ phần tử, và $1\le m<k$. Chứng minh với mọi thuật toán học $A$, có một phân bố $D$ trên $\mathcal X\times\{0,1\}$, phụ thuộc $A$ và $m$, thỏa ba điều sau.

- **Phân bố biên.** Phân bố biên (marginal distribution) $D_{\mathcal X}$ là phân bố đều trên $C$.
- **Khả thực.** $(D,\mathcal H)$ khả thực (Định nghĩa 01.16).
- **Rủi ro kì vọng.** $\mathbb E_{S\sim D^m}[L_D(A(S))]\ge(k-m)/(2k)$.

**(b)** Cho biến ngẫu nhiên $\theta\in[0,1]$ với $\mathbb E\theta\ge\mu$ và số $a\in[0,\mu)$. Chứng minh $\Pr(\theta>a)\ge(\mu-a)/(1-a)$. Kết hợp với (a) khi $k=2m$ để suy ra Định lý 03.17(a).

**(c)** Suy ra nếu $d=\infty$ thì $\mathcal H$ không học được PAC và không học được PAC bất khả tri. Phát biểu sáu khẳng định tương đương của Định lý 03.17(b), và chỉ ra phép kéo theo nào được chứng minh ở đây.

**(d)** Giả sử $d<\infty$. Chứng minh với mọi $\epsilon\in(0,\tfrac18]$ và $\delta\in(0,\tfrac17)$, độ phức tạp mẫu của Định nghĩa 01.20 thỏa $m_{\mathcal H}(\epsilon,\delta)\ge\lfloor d/2\rfloor+1$.
:::

::: hint Gợi ý 1
Phần (a). Dùng lập luận của định lý không có bữa trưa miễn phí (Nhận xét 01.30; UML §5.1) trên tập $C$, với các phân bố đều trên $C$ và nhãn cho bởi các hàm thuộc lớp. Phần (b). Chặn $\mathbb E\theta$ bởi $a\Pr(\theta\le a)+\Pr(\theta>a)$.
:::

::: hint Gợi ý 2
Phần (a). Chọn nhãn $f$ trên $C$ ngẫu nhiên, đều trên $\{0,1\}^C$, và chứng minh trung bình theo $f$ của $\mathbb E_S[L_{D_f}(A(S))]$ không nhỏ hơn $(k-m)/(2k)$; khi đó có một $f$ đạt ít nhất trung bình. Tại một điểm $c\in C$ không xuất hiện trong mẫu, nhãn $f(c)$ độc lập với mọi thứ thuật toán thấy.
:::

::: hint Gợi ý 3
Phần (c). Lấy $\epsilon=\delta=\tfrac18$ và $m=M(\tfrac18,\tfrac18)$, rồi dùng một tập $2m$ phần tử bị tách trọn. Phần (d). Với $2m\le d$, một tập $d$ phần tử bị tách trọn chứa $2m$ điểm bị tách trọn.
:::

::: solution Lời giải Bài tập 03.11
**(a) Rủi ro kì vọng trên một tập bị tách trọn.**

**Bước 1: họ phân bố.** Với mỗi $f\in\{0,1\}^C$, vì $C$ bị tách trọn, có $h_f\in\mathcal H$ trùng $f$ trên $C$. Gọi $D_f$ là phân bố của $(U,f(U))$ với $U$ đều trên $C$. Khi đó $L_{D_f}(h_f)=0$, nên $(D_f,\mathcal H)$ khả thực.

**Bước 2: chặn dưới rủi ro.** Với mẫu có tập đầu vào $V=\{X_1,\ldots,X_m\}$ và mọi hàm $g$,
$$
\begin{aligned}
&L_{D_f}(g)\\
&\quad=\tfrac1k\textstyle\sum_{c\in C}\mathbb 1[g(c)\ne f(c)]\\
&\quad\ge\tfrac1k\textstyle\sum_{c\in C\setminus V}\mathbb 1[g(c)\ne f(c)].
\end{aligned}
$$

**Bước 3: lấy nhãn ngẫu nhiên.** Lấy $F$ đều trên $\{0,1\}^C$, độc lập với $X_1,\ldots,X_m$ đều trên $C$, và $S=((X_i,F(X_i)))_{i\le m}$; khi biết $F=f$, $S\sim D_f^m$.

**Bước 4: một điểm chưa thấy.** Cố định $X_1,\ldots,X_m$ và các nhãn $F(c)$, $c\in V$. Khi đó $S$ cố định, và $A(S)$ cố định vì $A$ là một ánh xạ của mẫu (Định nghĩa 01.4). Với $c\notin V$, $F(c)$ vẫn đều trên $\{0,1\}$ và độc lập với những gì đã cố định, nên $A(S)$ sai tại $c$ với xác suất có điều kiện $\tfrac12$.

**Bước 5: trung bình.** Theo Bước 2, Bước 4 và $\lvert V\rvert\le m$,
$$
\begin{aligned}
&\mathbb E\big[L_{D_F}(A(S))\\
&\qquad\mid X_1,\ldots,X_m,F|_V\big]\\
&\quad\ge\frac{k-\lvert V\rvert}{2k}\ge\frac{k-m}{2k}.
\end{aligned}
$$

**Bước 6: chọn $f$.** Lấy kì vọng, $2^{-k}\sum_f\mathbb E_{S\sim D_f^m}[L_{D_f}(A(S))]\ge(k-m)/(2k)$, nên có một $f$ với $\mathbb E_{S\sim D_f^m}[L_{D_f}(A(S))]\ge(k-m)/(2k)$. Lấy $D=D_f$; phân bố này phụ thuộc $A$ và $m$.

**(b) Từ kì vọng sang xác suất.**

**Bước 1.** Vì $\theta\le a$ trên $\{\theta\le a\}$ và $\theta\le1$,
$$
\begin{aligned}
\mathbb E\theta&\le a\Pr(\theta\le a)+\Pr(\theta>a)\\
&=a+(1-a)\Pr(\theta>a).
\end{aligned}
$$
Vì $1-a>0$, $\Pr(\theta>a)\ge(\mathbb E\theta-a)/(1-a)\ge(\mu-a)/(1-a)$.

**Bước 2: thay số.** Với $k=2m$, (a) cho $\mu=(2m-m)/(4m)=\tfrac14$. Lấy $\theta=L_D(A(S))$ và $a=\tfrac18$:
$$
\frac{1/4-1/8}{1-1/8}=\frac{1/8}{7/8}=\frac17 .
$$
Vậy $\Pr_{S\sim D^m}[L_D(A(S))>\tfrac18]\ge\tfrac17$ với một phân bố khả thực tập trung trên $C$: đây là Định lý 03.17(a).

**(c) Chiều VC vô hạn và định lý cơ bản.**

**Bước 1: tập bị tách trọn.** Theo Định nghĩa 03.3, khi $d=\infty$, với mọi $m$ có một tập $2m$ phần tử bị tách trọn.

**Bước 2: không có thuật toán học PAC.** Giả sử $A$ là thuật toán học PAC với hàm $M$. Lấy $\epsilon=\delta=\tfrac18$ và $m=M(\tfrac18,\tfrac18)$. Theo (b), có $D$ khả thực với $\Pr[L_D(A(S))>\tfrac18]\ge\tfrac17>\delta$, trái với Định nghĩa 01.18.

**Bước 3: trường hợp bất khả tri.** Theo Nhận xét 01.26, một thuật toán học PAC bất khả tri cũng là thuật toán học PAC, nên cũng không tồn tại.

**Bước 4: định lý cơ bản.** Dưới (M), sáu khẳng định sau tương đương: $\mathcal H$ có tính chất hội tụ đều; mọi thuật toán ERM là thuật toán học PAC bất khả tri; $\mathcal H$ học được PAC bất khả tri; $\mathcal H$ học được PAC; mọi thuật toán ERM là thuật toán học PAC; $d<\infty$. Bước 2 là phản đảo của phép kéo theo (4)⇒(6), "học được PAC kéo theo $d<\infty$"; Bước 3 thêm (3)⇒(6) qua (3)⇒(4). Cả hai bước không dùng (M).

**(d) Cận dưới cho độ phức tạp mẫu.**

**Bước 1: trường hợp tầm thường.** Khi $d\le1$, vế phải bằng $1$, và bất đẳng thức đúng vì $m_{\mathcal H}(\epsilon,\delta)\in\mathbb N\cup\{\infty\}$.

**Bước 2: thất bại tại mọi $m\le\lfloor d/2\rfloor$.** Giả sử $d\ge2$ và lấy $m$ với $1\le m\le\lfloor d/2\rfloor$. Một tập $d$ phần tử bị tách trọn chứa $2m$ điểm bị tách trọn. Theo (b), với mọi $A$ có $D$ khả thực với $\Pr[L_D(A(S))>\tfrac18]\ge\tfrac17>\delta$. Vì $\epsilon\le\tfrac18$, ta có $\Pr[L_D(A(S))\le\epsilon]<1-\delta$.

**Bước 3: kết luận.** Bất đẳng thức của Định nghĩa 01.18 sai tại mọi $m\le\lfloor d/2\rfloor$, nên $m_A(\epsilon,\delta)\ge\lfloor d/2\rfloor+1$ với mọi $A$, và $m_{\mathcal H}$ cũng vậy.

**Kiểm tra lại.** Với $k=2$, $m=1$, điểm chưa thấy mang khối lượng $\tfrac12$ và bị đoán sai với xác suất $\tfrac12$, nên trung bình rủi ro ít nhất $\tfrac14=(2-1)/4$, khớp (a).
:::

### Bài tập 03.12 (Hình cầu đóng trong $\mathbb R^p$; UML Bài tập 9.6)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 1; cận trên qua một phép nâng chiều và Mệnh đề 03.9, cận dưới bằng một tập tường minh.

::: exercise Bài tập 03.12
Cho $p\ge1$. Với $v\in\mathbb R^p$ và $r>0$, đặt $B_{v,r}(x)=\mathbb 1[\lVert x-v\rVert\le r]$, và gọi $\mathcal H^p_{\mathrm{ball}}=\{B_{v,r}:\ v\in\mathbb R^p,\ r>0\}$ là lớp hình cầu đóng.

**(a)** Đặt $\varphi(x)=(x,\lVert x\rVert^2)\in\mathbb R^{p+1}$. Chứng minh nếu $\mathcal H^p_{\mathrm{ball}}$ tách trọn $\{x_1,\ldots,x_k\}$ thì $\mathcal H^{p+1}_{\mathrm{aff}}$ tách trọn $\{\varphi(x_1),\ldots,\varphi(x_k)\}$. Suy ra $\operatorname{VCdim}(\mathcal H^p_{\mathrm{ball}})\le p+2$.

**(b)** Chứng minh $\mathcal H^p_{\mathrm{ball}}$ tách trọn $\{0,\mathbf e_1,\ldots,\mathbf e_p\}$. Suy ra $p+1\le\operatorname{VCdim}(\mathcal H^p_{\mathrm{ball}})\le p+2$.
:::

::: hint Gợi ý 1
Phần (a). Khai triển $\lVert x-v\rVert^2\le r^2$ và đưa về dạng $\langle w,\varphi(x)\rangle+b\ge0$.
:::

::: hint Gợi ý 2
Phần (b). Gọi $A$ là tập các véc-tơ đơn vị nhận nhãn $1$ và $a=\lvert A\rvert$. Lấy tâm $v=\sum_{\mathbf e_i\in A}\mathbf e_i$ và tính bình phương khoảng cách từ $v$ tới $0$, tới $\mathbf e_i\in A$ và tới $\mathbf e_i\notin A$.
:::

::: hint Gợi ý 3
Phần (b). Ba bình phương khoảng cách là $a$, $a-1$, $a+1$. Chọn $r^2$ giữa các giá trị đó theo nhãn của gốc; cách gán nhãn toàn $0$ cần một hình cầu nằm xa.
:::

::: solution Lời giải Bài tập 03.12
**(a) Nâng chiều.**

**Bước 1: hình cầu là nửa không gian sau khi nâng.** Với $w=(2v,-1)$ và $b=r^2-\lVert v\rVert^2$,
$$
\begin{aligned}
&\lVert x-v\rVert^2\le r^2\\
&\iff\lVert x\rVert^2-2\langle v,x\rangle\\
&\qquad+\lVert v\rVert^2\le r^2\\
&\iff\langle2v,x\rangle-\lVert x\rVert^2\\
&\qquad+r^2-\lVert v\rVert^2\ge0\\
&\iff\langle w,\varphi(x)\rangle+b\ge0 .
\end{aligned}
$$
Vậy $B_{v,r}(x)=h_{w,b}(\varphi(x))$ với $h_{w,b}\in\mathcal H^{p+1}_{\mathrm{aff}}$; điểm trên mặt cầu nhận nhãn $1$, khớp quy ước $\ge0$ của Định nghĩa 03.7.

**Bước 2: chuyển tách trọn.** $\varphi$ là đơn ánh, nên $\varphi(x_1),\ldots,\varphi(x_k)$ phân biệt. Nếu $B_{v,r}$ thực hiện một cách gán nhãn trên các $x_i$ thì $h_{w,b}$ thực hiện cùng cách gán nhãn trên các $\varphi(x_i)$.

**Bước 3: kết luận.** Theo Mệnh đề 03.9(a) trong $\mathbb R^{p+1}$, $k\le p+2$, nên $\operatorname{VCdim}(\mathcal H^p_{\mathrm{ball}})\le p+2$.

**(b) Tách trọn đỉnh đơn hình.**

**Bước 1: khoảng cách.** Gọi $A$ là tập các véc-tơ đơn vị nhận nhãn $1$, $a=\lvert A\rvert$, và $v=\sum_{\mathbf e_i\in A}\mathbf e_i$. Khi đó
$$
\begin{aligned}
\lVert0-v\rVert^2&=a,\\
\lVert\mathbf e_i-v\rVert^2&=a-1\quad(\mathbf e_i\in A),\\
\lVert\mathbf e_i-v\rVert^2&=a+1\quad(\mathbf e_i\notin A).
\end{aligned}
$$

**Bước 2: chọn bán kính.**

- **Gốc nhận nhãn $1$.** Lấy $r^2=a+\tfrac12$: hình cầu chứa $A$ và $0$, không chứa các $\mathbf e_i\notin A$.
- **Gốc nhận nhãn $0$, $a\ge1$.** Lấy $r^2=a-\tfrac12>0$: hình cầu chứa $A$, không chứa $0$ và các $\mathbf e_i\notin A$.
- **Toàn $0$.** Lấy $v=-3\mathbf e_1$, $r=1$: khoảng cách tới $0$, $\mathbf e_1$, $\mathbf e_i$ ($i\ge2$) là $3$, $4$, $\sqrt{10}$, đều lớn hơn $1$.

**Bước 3: kết luận.** Cả $2^{p+1}$ cách gán nhãn thực hiện được, nên $p+1\le\operatorname{VCdim}(\mathcal H^p_{\mathrm{ball}})\le p+2$.

**Kiểm tra lại.** Với $p=1$, $\mathcal H^1_{\mathrm{ball}}$ là lớp các đoạn $[v-r,v+r]$, một lớp con của $\mathcal H_{\mathrm{int}}$, nên chiều VC không quá $2$ theo Mệnh đề 03.6; cùng (b), nó bằng $2=p+1$.
:::
