# Bài 01 — Mô hình học: rủi ro, tối thiểu hóa rủi ro thực nghiệm và học PAC

Một thuật toán học (learning algorithm) nhận một tập hữu hạn các *quan sát* (example) và trả về một *hàm dự đoán* (predictor), là một quy tắc gán nhãn cho mỗi đầu vào. Câu hỏi trung tâm của bài là: **học có nghĩa là gì?** Cụ thể, khi nào ta nói một hàm dự đoán đã học được, trước cả khi sử dụng nó để dự đoán?

Để trả lời, chúng ta sẽ tìm hiểu ba đối tượng chính của Học thống kê.

- Rủi ro của hàm dự đoán, bao gồm: *Rủi ro kì vọng* (population risk, expected risk) là mức sai trung bình của hàm dự đoán trên một quan sát mới rút từ phân bố dữ liệu (data-generating distribution). *Rủi ro thực nghiệm* (empirical risk) là mức sai trung bình trên một tập mẫu quan sát.
- *Quy tắc tối thiểu hóa rủi ro thực nghiệm* (empirical risk minimization, ERM): là quy tắc chọn hàm dự đoán sai ít nhất trên tập mẫu quan sát.
- *Học xấp xỉ với xác suất cao* (probably approximately correct, PAC): với xác suất cao theo phân bố của tập mẫu quan sát, hàm dự đoán học được có rủi ro kì vọng gần mức tốt nhất.

## Câu hỏi mở đầu

Xét một chỉ số y tế $x$ có năm mức $\{1,2,3,4,5\}$. Giả sử một người có bệnh ($y=1$) khi và chỉ khi chỉ số $x$ của người đó từ mức 3 trở lên, và mỗi mức chiếm $20\%$ dân số.

Một *tập huấn luyện* (training sample) gồm bốn người: hai người ở mức 1 và 2 không có bệnh, hai người ở mức 4 và 5 có bệnh. Tập huấn luyện $S$ gồm:
- $(x_1, y_1) = (1, 0)$
- $(x_2, y_2) = (2, 0)$
- $(x_3, y_3) = (4, 1)$
- $(x_4, y_4) = (5, 1)$

Xét hai hàm dự đoán, trong tình huống này, còn gọi là hàm phân lớp (classifier). Hàm thứ nhất báo dương tính khi chỉ số từ 3 trở lên; hàm thứ hai báo dương tính khi chỉ số từ 4 trở lên. Nghĩa là
- $h_3(x) = \mathbb 1[x\geq 3]$
- $h_4(x) = \mathbb 1[x\geq 4]$

trong đó chỉ số dưới của $h$ là ngưỡng báo dương tính, và $\mathbb 1[p]$ là hàm chỉ báo (indicator) bằng $1$ nếu mệnh đề $p$ đúng, và bằng $0$ nếu $p$ sai.

**Câu hỏi.** Hiệu quả của hai hàm phân lớp này như thế nào?

Hai hàm phân lớp cùng khớp mọi quan sát trong tập huấn luyện (dự đoán hoàn hảo trên tập huấn luyện). Nhưng xét trên toàn bộ phân bố của chỉ số $x$, hàm $h_3$ phân lớp đúng hoàn toàn còn hàm $h_4$ sai với những người ở mức 3, tức với xác suất $0{,}2$.

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Phát biểu đầy đủ một bài toán học thống kê: tập đầu vào, tập nhãn, phân bố dữ liệu, mẫu, lớp giả thuyết, hàm lỗi, thuật toán học, đối tượng so sánh. Chỉ ra đại lượng nào cố định, đại lượng nào ngẫu nhiên và ngẫu nhiên theo phân bố nào.
2. Tính rủi ro kì vọng, rủi ro thực nghiệm, tập nghiệm ERM, rủi ro Bayes (Bayes risk) và rủi ro vượt mức (excess risk) trong một bài toán hữu hạn; xác định ngưỡng tối ưu khi hàm lỗi (loss function) có chi phí bất đối xứng.
3. Chứng minh rủi ro thực nghiệm của một giả thuyết cố định là *ước lượng không chệch* (unbiased estimator) của rủi ro kì vọng.
4. Viết định nghĩa học PAC trong trường hợp khả diễn (realizable) và bất khả diễn (agnostic); phân biệt độ phức tạp mẫu (sample complexity) của một thuật toán với độ phức tạp mẫu của một lớp.
5. Dựng phản ví dụ cho thuật toán ghi nhớ, chứng minh hàm phân lớp chỉ ghi nhớ có rủi ro thực nghiệm bằng 0 và rủi ro kì vọng bằng 1, và giải thích vì sao cần thiên kiến quy nạp (inductive bias) hoặc kiểm soát thuật toán.

## Kiến thức tiên quyết

- Kì vọng và tính tuyến tính của kì vọng.
- Xác suất có điều kiện; kì vọng có điều kiện và tính chất $\mathbb E[\mathbb E[U\mid X]]=\mathbb E[U]$.
- Hàm, tập hợp, hàm chỉ báo $\mathbb 1[\cdot]$.
- Phân bố đều $U[0,1]$ trên $[0,1]$.
- Bất đẳng thức $1-x\le e^{-x}$ với mọi $x\in\mathbb R$.
- Một khẳng định đúng *hầu chắc chắn* (almost surely) nếu nó đúng ngoài một biến cố có xác suất $0$.

**Câu hỏi ôn nhanh.**

1. Cho $X\sim U[0,1]$. Tính $\Pr\big(X\in\{0{,}1;\ 0{,}5;\ 0{,}9\}\big)$.
2. Cho biến ngẫu nhiên $Z_1$ với $\mathbb E Z_1=\mu$ và đặt $Z_2=Z_1$. Tính $\mathbb E\big[(Z_1+Z_2)/2\big]$.
3. Rút $m$ lần độc lập, mỗi lần đều trên $\{1,2,3,4,5\}$. Tính xác suất không lần nào ra số 3.

::: solution Lời giải câu hỏi ôn nhanh
1. Bằng $0$: xác suất của hợp ba điểm không vượt quá tổng ba xác suất, mỗi xác suất bằng $0$.
2. Bằng $\mu$, theo tính tuyến tính của kì vọng, dù $Z_1$ và $Z_2$ hoàn toàn phụ thuộc nhau.
3. Bằng $0{,}8^m$: mỗi lần rút không ra số 3 với xác suất $0{,}8$, và các lần rút độc lập.
:::

## 1. Thiết lập bài toán

Trong học phần này, trước khi phát biểu bất kì mệnh đề nào, chúng ta nêu rõ tám thành phần sau.

1. **Tập đầu vào** (input space) $\mathcal X$ và **tập nhãn** (label set) $\mathcal Y$. Một quan sát là một cặp $z=(x,y)$ thuộc tập quan sát $\mathcal Z=\mathcal X\times\mathcal Y$. Ví dụ: trong phân lớp nhị phân (binary classification), $\mathcal Y=\{0,1\}$; trong hồi quy (regression), $\mathcal Y=\mathbb R$.
2. **Phân bố dữ liệu** $D$ trên $\mathcal Z$, tức phân bố của cặp ngẫu nhiên $Z=(X,Y)$. Vì $D$ là phân bố liên hợp (joint distribution), cùng một đầu vào $x$ có thể đi với nhiều nhãn $y$ khác nhau (nếu $D(Y=y\mid X=x)>0$); trường hợp có *hàm gán nhãn* (labeling function, target function) $f:\mathcal X\to\mathcal Y$, là một trường hợp riêng (khi đó $D(Y=f(x)\mid X=x)=1$).
3. **Tập huấn luyện** $S=(Z_1,\ldots,Z_m)\sim D^m$, gồm $m$ quan sát độc lập cùng phân bố (independent and identically distributed, i.i.d.) theo $D$. Số $m$ là cỡ mẫu (sample size).
4. **Lớp giả thuyết** (hypothesis class) $\mathcal H$, một tập các hàm $h:\mathcal X\to\mathcal Y$, được chọn trước khi lấy mẫu. Mỗi $h\in\mathcal H$ là một giả thuyết (hypothesis), tức một hàm dự đoán; trong phân lớp ta gọi $h$ là hàm phân lớp.
5. **Hàm lỗi** (loss function) $\ell(h,z)\ge0$, đo mức sai của $h$ trên quan sát $z$.
6. **Thuật toán học** $A$, nhận mẫu $S$ và trả về hàm dự đoán $A(S)\in\mathcal H$.
7. **Mục tiêu**. Với mỗi hàm dự đoán $h$, *rủi ro kì vọng* $$L_D(h) = \mathbb E_D[\ell(h, Z)]$$ là kì vọng của $\ell(h,Z)$ theo một quan sát mới $Z\sim D$, độc lập với tập huấn luyện $S$. Nói chung, ta muốn rủi ro kì vọng $L_D(A(S))$ nhỏ và tốt nhất là bằng $\inf_{h\in\mathcal H}L_D(h)$.
8. **Tài nguyên.** Tài nguyên được xét là cỡ mẫu $m$.

Thuật toán học không được phép biết phân bố $D(z)$ hay $D(y\mid x)$ mà chỉ được sử dụng tập huấn luyện $S$ được lấy mẫu từ $D$. Một quy tắc cần biết $D$ để chạy vì vậy không phải là thuật toán học.

Bảng dưới phân loại các đại lượng của bài theo nguồn ngẫu nhiên.

| Loại | Đại lượng |
|---|---|
| Cố định (không ngẫu nhiên) | $D$, $\mathcal H$, $\ell$, thuật toán $A$, $L_D(h)$ với $h$ cho trước, $\inf_{h\in\mathcal H}L_D(h)$ |
| Ngẫu nhiên theo $S\sim D^m$ | $S$, $A(S)$, $L_D(A(S))$ |
| Thuật toán $A$ có thể sinh các đại lượng ngẫu nhiên $\xi$ trong quá trình huấn luyện (ví dụ lấy mẫu mini-batch) | $A(S;\xi)$, $L_D(A(S;\xi))$ |

## 2. Kí hiệu và giả thiết

Kí hiệu chung theo bảng kí hiệu của học phần và §1. Bảng dưới gồm các kí hiệu riêng của bài dùng ngay từ ví dụ ở §3; mỗi kí hiệu khác được đặt tên tại định nghĩa của nó.

| Kí hiệu | Ý nghĩa |
|---|---|
| $D_{\mathcal X}(x)$ | phân bố biên (marginal distribution) của $X$ |
| $\eta(x)=\Pr(Y=1\mid X=x)$ | xác suất có điều kiện của nhãn 1 trong trường hợp phân lớp nhị phân |

**Đọc lần đầu.** Mỗi tập $\mathcal X$, $\mathcal Y$, $\mathcal Z$ trong bài đi kèm một σ-đại số (σ-algebra), họ các tập con được gán xác suất. Một hàm là đo được (measurable) khi ảnh ngược của mỗi tập trong σ-đại số đích thuộc σ-đại số nguồn.

Bài này sử dụng hai giả thiết thống kê dưới đây (phần **Giả thiết.** của các kết quả).

- **(T1) Lấy mẫu.** $Z_1,\ldots,Z_m$ độc lập cùng phân bố theo $D$. Một số kết quả chỉ cần dạng yếu: mỗi $Z_i$ có phân bố $D$, không cần độc lập.
- **(T2) Hàm lỗi.** $\ell\ge0$ và $\ell(h,\cdot)$ đo được với mọi $h\in\mathcal H$; khi hàm lỗi không bị chặn, ta cần $L_D(h)<\infty$.

## 3. Ví dụ xuyên suốt

Ví dụ sau đủ nhỏ để tính bằng tay.

::: example Ví dụ 01.1 (Sàng lọc theo ngưỡng trên năm mức đo)

**Đầu vào và nhãn.**
- $\mathcal X=\{1,2,3,4,5\}$ là năm mức của một chỉ số đo;
- $\mathcal Y=\{0,1\}$, với $Y=1$ là có bệnh.
- Phân bố biên $D_{\mathcal X}$ đều: mỗi mức có xác suất $0{,}2$.

**Lớp giả thuyết.** Các hàm ngưỡng
$$
\begin{aligned}
h_t(x)&=\mathbb 1[x\ge t],\\
\mathcal H&=\{h_t:\ t\in\{1,\ldots,6\}\},
\end{aligned}
$$
trong đó $h_1\equiv1$ luôn báo dương tính với mọi người và $h_6\equiv0$ luôn báo âm tính.

**Hàm lỗi.** Hàm lỗi 0–1 (0–1 loss) $\ell_{0\text{-}1}(h,(x,y))=\mathbb 1[h(x)\ne y]$, đếm một lỗi mỗi khi dự đoán sai.

**Phân bố dữ liệu.**
Phân bố liên hợp:
$$D(x,y) = D_\mathcal X(x) D(y\mid x)$$
Trong ví dụ này, xét hai phiên bản. Phân bố nhãn ngẫu nhiên
$$D_\eta(y\mid x)=\eta(x)^y (1-\eta(x))^{1-y}$$
với xác suất có điều kiện $\eta(x)=\Pr(Y=1\mid X=x)$; và phân bố nhãn tất định
$$D_f(y\mid x) = \begin{cases}
1 & y = f(x)\\
0 & y\neq f(x)
\end{cases}$$
với hàm gán nhãn $f:\mathcal X\rightarrow \mathcal Y$.

| $x$ | $1$ | $2$ | $3$ | $4$ | $5$ |
|---|---|---|---|---|---|
| $D_{\mathcal X}(x)$ | $0{,}2$ | $0{,}2$ | $0{,}2$ | $0{,}2$ | $0{,}2$ |
| $\eta(x)$  | $0$ | $\tfrac14$ | $\tfrac34$ | $\tfrac25$ | $1$ |
| $f(x)$  | $0$ | $0$ | $1$ | $1$ | $1$ |

*Dữ liệu có nhiễu* từ phân bố $D_\eta$ với cỡ mẫu $m=6$:
$$
\begin{aligned}
S_\eta=\big(&(1,0),(2,0),(2,1),\\
&(3,1),(4,0),(5,1)\big).
\end{aligned}
$$

*Dữ liệu tất định* từ phân bố $D_f$ với $f=h_3$, tức có bệnh khi và chỉ khi $x\ge3$, cỡ mẫu $m=4$:
$$
\begin{aligned}
S_f=\big(&(1,0),(2,0),\\
&(4,1),(5,1)\big).
\end{aligned}
$$
:::

::: application Sàng lọc y tế với chi phí bất đối xứng

**Đầu vào và nhãn.** Trong một chương trình sàng lọc (screening), đầu vào $x\in\mathcal X\subseteq\mathbb R^p$ là véc-tơ các chỉ số đo của một người, nhãn $y\in\{0,1\}$ là tình trạng bệnh. Nhãn có nhiễu: hai người có cùng chỉ số đo có thể ở hai tình trạng khác nhau, như tại mức $x=2$ của $D_\eta$, nơi $\eta(2)=\tfrac14$.

**Hai loại lỗi.**
- Âm tính giả (false negative - FN): hàm dự đoán báo âm tính đối với người bệnh;
- Dương tính giả (false positive - FP): hàm dự đoán báo dương tính đối với người khoẻ.

**Hàm lỗi có trọng số.** Gán cho hai loại lỗi này các chi phí $c_{FN}>0$ và $c_{FP}>0$, ta được *hàm lỗi có trọng số* (cost-weighted loss)
$$
\begin{aligned}
&\ell_c\big(h,(x,y)\big)\\
&\quad=c_{FN}\,\mathbb 1[y=1,\ h(x)=0]\\
&\qquad+c_{FP}\,\mathbb 1[y=0,\ h(x)=1],
\end{aligned}
$$
nhận giá trị trong $\{0,c_{FP},c_{FN}\}$. Khi $c_{FP}=c_{FN}=1$, $\ell_c$ trở thành hàm lỗi 0–1.

**Chi phí trong ví dụ sàng lọc.** Ta lấy $(c_{FP},c_{FN})=(1,4)$: bỏ sót một người bệnh đắt gấp bốn lần đưa một người khỏe đi xét nghiệm thêm.

**Câu hỏi thực hành.** Nên đặt ngưỡng báo dương tính ở đâu khi hai loại lỗi có chi phí khác nhau?
:::

## 4. Rủi ro kì vọng và bài toán học thống kê

Chất lượng của một hàm dự đoán $h$ phải được đo trên quan sát mới lấy mẫu từ $D$.

::: definition Định nghĩa 01.1 (Hàm lỗi và rủi ro kì vọng)
Cho tập quan sát $\mathcal Z$, một phân bố $D$ (và σ-đại số) trên $\mathcal Z$ và một lớp giả thuyết $\mathcal H$. Một *hàm lỗi* là một ánh xạ $\ell:\mathcal H\times\mathcal Z\to[0,\infty)$ sao cho $\ell(h,\cdot)$ đo được với mọi $h\in\mathcal H$. *Rủi ro kì vọng* của $h\in\mathcal H$ là
$$
L_D(h)=\mathbb E_{Z\sim D}\,\ell(h,Z).
$$
:::

**Câu hỏi.** Tại sao không nên đo chất lượng của hàm dự đoán trên tập huấn luyện?

Với $h$ cho trước, $L_D(h)$ là một số, không phải biến ngẫu nhiên, nhưng chưa biết vì chưa biết $D$. Ví dụ:
- Hàm lỗi $\ell_{0\text{-}1}$ cho $L_D(h)=\Pr(h(X)\ne Y)$ gọi là *xác suất lỗi* của $h$;
- Hàm lỗi có trọng số $\ell_c$ cho rủi ro kí hiệu $L_D^c(h)$;
- Hàm lỗi bình phương (squared loss) $\ell(h,(x,y))=(h(x)-y)^2$ dùng khi $\mathcal Y=\mathbb R$.

::: example Ví dụ 01.2 (Rủi ro kì vọng của các hàm ngưỡng $h_t$)

**Thiết lập.** Xét bản có nhiễu của Ví dụ 01.1: phân bố $D_\eta$, lớp sáu hàm ngưỡng $h_t$, $(c_{FP},c_{FN})=(1,4)$.

**Công thức rủi ro của $h_t$.** Hàm $h_t$ sai tại mức $x<t$ khi $Y=1$ và tại mức $x\ge t$ khi $Y=0$:
$$
\begin{aligned}
&\Pr(Y\neq h_t(X)\mid X=x)\\
&\quad= \begin{cases}
\eta(x) & x < t\\
1-\eta(x) & x \ge t
\end{cases}
\end{aligned}
$$
Mỗi mức có xác suất $0{,}2$, nên
$$
\begin{aligned}
L_{D_\eta}(h_t)
&=0{,}2\Big[\sum_{x<t}\eta(x)\\
&\quad+\sum_{x\ge t}\big(1-\eta(x)\big)\Big].
\end{aligned}
$$
Dưới $\ell_c$, mỗi lỗi bỏ sót có chi phí $c_{FN}$ và mỗi lỗi báo nhầm có chi phí $c_{FP}$, nên tương tự
$$
\begin{aligned}
&L^c_{D_\eta}(h_t)\\
&\quad=0{,}2\Big[c_{FN}\sum_{x<t}\eta(x)\\
&\qquad+c_{FP}\sum_{x\ge t}\big(1-\eta(x)\big)\Big].
\end{aligned}
$$
**Tính tại $t=3$.** Hai tổng là
$$
\begin{aligned}
\sum_{x<3}\eta(x)&=0+\tfrac14=0{,}25,\\
\sum_{x\ge3}\big(1-\eta(x)\big)&=\tfrac14+\tfrac35+0\\
&=0{,}85.
\end{aligned}
$$
Thay hai tổng vào hai công thức trên, ta được
$$
\begin{aligned}
L_{D_\eta}(h_3)&=0{,}2\,(0{,}25+0{,}85)\\
&=0{,}2\cdot1{,}1=0{,}22,\\
L^c_{D_\eta}(h_3)&=0{,}2\,(4\cdot0{,}25+0{,}85)\\
&=0{,}2\cdot1{,}85=0{,}37.
\end{aligned}
$$
Như vậy, $h_3$ phân lớp sai với xác suất $0{,}22$, và chi phí trung bình của nó trên một người là $0{,}37$.

**Các ngưỡng còn lại.** Cùng cách tính cho bảng sau (Phụ lục C.1):

| $t$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ |
|---|---|---|---|---|---|---|
| $L_{D_\eta}(h_t)$ | $0{,}52$ | $0{,}32$ | $\mathbf{0{,}22}$ | $0{,}32$ | $0{,}28$ | $0{,}48$ |
| $L^c_{D_\eta}(h_t)$ | $0{,}52$ | $\mathbf{0{,}32}$ | $0{,}37$ | $0{,}92$ | $1{,}12$ | $1{,}92$ |

**Kết luận.** Dưới hàm lỗi 0–1, hàm tốt nhất trong $\mathcal H$ là $h_3$, với $\min_tL_{D_\eta}(h_t)=0{,}22$. Dưới $\ell_c$, hàm tốt nhất là $h_2$: khi bỏ sót đắt gấp bốn, báo dương tính thêm cho mức 2 (nơi $\eta(2)=\tfrac14$) làm rủi ro giảm từ $0{,}37$ xuống $0{,}32$. Hai hàm lỗi chọn ra hai hàm tốt nhất khác nhau.
:::

Tương tự, bài toán hồi quy cũng có thể áp dụng khung rủi ro trên. Ta chỉ cần đổi tập nhãn và hàm lỗi, cùng định nghĩa áp dụng cho hồi quy.

::: example Ví dụ 01.3 (Hồi quy tuyến tính với hàm lỗi bình phương)

**Thiết lập.** Cho $\mathcal X=\mathbb R^p$, $\mathcal Y=\mathbb R$, một phân bố $D$ trên $\mathbb R^p\times\mathbb R$, lớp $\mathcal H=\{h_w:x\mapsto\langle w,x\rangle,\ w\in\mathbb R^p\}$ và hàm lỗi bình phương $\ell(h, (x,y))=(y-h(x))^2$.

$$L_D(h_w)=\mathbb E_D\big(\langle w,X\rangle-Y\big)^2$$

**Rủi ro bị chặn.** Sử dụng các bất đẳng thức $(a-b)^2\le2a^2+2b^2$ và $\langle w,x\rangle^2\le\lVert w\rVert^2\lVert x\rVert^2$ (Cauchy–Schwarz),
$$
\begin{aligned}
&\big(\langle w,X\rangle-Y\big)^2\\
&\quad\le 2\langle w,X\rangle^2+2Y^2\\
&\quad\le 2\lVert w\rVert^2\lVert X\rVert^2+2Y^2 .
\end{aligned}
$$
Kì vọng của hai vế thỏa
$$
\begin{aligned}
L_D(h_w)&\le2\lVert w\rVert^2\,\mathbb E\lVert X\rVert^2\\
&\quad+2\,\mathbb EY^2 .
\end{aligned}
$$

Vế phải hữu hạn với mọi $w$ khi $\mathbb E\lVert X\rVert^2<\infty$ và $\mathbb EY^2<\infty$, nên điều kiện tồn tại mô-men bậc 2 đủ để mọi $h_w$ có rủi ro hữu hạn.
:::

::: remark Nhận xét 01.2 (Tính khả tích khi hàm lỗi không bị chặn)
Điều kiện $\mathbb EY^2<\infty$ trong Ví dụ 01.3 là cần thiết để mọi $h_w$ có rủi ro hữu hạn: nếu $\mathbb EY^2=\infty$, hàm $h_0\equiv0$ có $L_D(h_0)=\mathbb EY^2=\infty$ nên mọi so sánh rủi ro với $h_0$ mất ý nghĩa.
:::

Với hàm lỗi không bị chặn, chúng ta cần tách riêng những phân bố mà mọi rủi ro trong lớp giả thuyết đều hữu hạn.

::: definition Định nghĩa 01.3 (Phân bố có rủi ro hữu hạn)
Cho lớp giả thuyết $\mathcal H$ và hàm lỗi $\ell$ trên tập quan sát $\mathcal Z$. Một phân bố $D$ trên $\mathcal Z$ được gọi là *phân bố có rủi ro hữu hạn* (finite-risk distribution) trên $\mathcal H$ nếu $L_D(h)<\infty$ với mọi $h\in\mathcal H$.
:::

Khi $\ell$ bị chặn, như $\ell_{0\text{-}1}$ hay $\ell_c$, mọi phân bố đều có rủi ro hữu hạn; với lớp tuyến tính của Ví dụ 01.3, điều kiện tồn tại mô-men bậc 2 là đủ.

Rủi ro kì vọng đánh giá một hàm dự đoán cho trước. Khi học, hàm dự đoán được chọn từ mẫu. Vì vậy, trước khi phát biểu bài toán học thống kê, chúng ta cần nói rõ thuật toán học nhận gì và trả về gì.

::: definition Định nghĩa 01.4 (Thuật toán học)
Cho tập quan sát $\mathcal Z$, lớp giả thuyết $\mathcal H$ và hàm lỗi $\ell$. Một *thuật toán học* là một họ ánh xạ $A_m:\mathcal Z^m\to\mathcal H$, $m\ge1$, sao cho ánh xạ $(s,z)\mapsto\ell(A_m(s),z)$ đo được trên $\mathcal Z^m\times\mathcal Z$. Để cho gọn, ta viết $A(S)$ thay cho $A_m(S)$.
:::

Đầu vào của thuật toán học không phải là phân bố $D$ mà là tập huấn luyện $S\sim D^m$. Do đó, $L_D(A(S))$ là một biến ngẫu nhiên dẫn xuất từ biến ngẫu nhiên $S\sim D^m$.

Đầu ra của thuật toán học thuộc $\mathcal H$, tức thuật toán học lựa chọn hàm dự đoán trong lớp $\mathcal H$ (proper learning).

Ghép rủi ro kì vọng và thuật toán học vừa định nghĩa với các thành phần còn lại của §1, ta được bài toán học thống kê.

::: definition Định nghĩa 01.5 (Bài toán học thống kê)
*Bài toán học thống kê* (statistical learning problem) với lớp $\mathcal H$ và hàm lỗi $\ell$ gồm các thành phần sau.

- **Tập quan sát.** $\mathcal Z=\mathcal X\times\mathcal Y$, cố định.
- **Lớp giả thuyết và hàm lỗi.** $\mathcal H$ và $\ell$, chọn trước khi lấy mẫu.
- **Phân bố dữ liệu.** $D$ trên $\mathcal Z$, cố định nhưng chưa biết; khi $\ell$ không bị chặn, $D$ có rủi ro hữu hạn trên $\mathcal H$ (Định nghĩa 01.3).
- **Tập huấn luyện.** $S=(Z_1,\ldots,Z_m)\sim D^m$, gồm $m$ quan sát i.i.d. theo $D$, là thông tin duy nhất về $D$.
- **Thuật toán học.** $A$ (Định nghĩa 01.4), chọn trước khi lấy mẫu và không phụ thuộc $D$, trả về $A(S)\in\mathcal H$.
- **Mục tiêu.** Hiệu giữa rủi ro kì vọng của $A(S)$ (Định nghĩa 01.1) và mức tốt nhất trong lớp $\mathcal H$ nhỏ nhất có thể mà không biết $D$:
  $$
  L_D\big(A(S)\big)-\inf_{h\in\mathcal H}L_D(h).
  $$

Hiệu này không âm vì $A(S)\in\mathcal H$. Tóm lại, mục tiêu là **tối thiểu hóa rủi ro kì vọng** trên $\mathcal H$ khi không tính được $L_D$.
:::

Vì mẫu $S$ ngẫu nhiên theo $D^m$, hàm học được $A(S)$ và rủi ro $L_D(A(S))$ của nó cũng ngẫu nhiên. Câu hỏi chính của Học thống kê là
- Hiệu trên có thể nhỏ đến đâu? Với xác suất nào theo $S$? Và trên họ phân bố $D$ nào?

::: example Ví dụ 01.4 (Bài toán học trong ví dụ sàng lọc)

**Thiết lập.** Xét bản có nhiễu của Ví dụ 01.1: $\mathcal X=\{1,\ldots,5\}$, $\mathcal Y=\{0,1\}$, lớp sáu hàm ngưỡng, hàm lỗi 0–1, cỡ mẫu $m=6$.

**Mức tốt nhất trong lớp.** Theo Ví dụ 01.2, $\inf_tL_{D_\eta}(h_t)=L_{D_\eta}(h_3)=0{,}22$.

**Thông tin của thuật toán.** Thông tin duy nhất là một tập huấn luyện $S\sim D_\eta^6$, chẳng hạn $S_\eta$ (thuật toán học không biết $D_\eta$ và $\eta$).

**Bài toán học.** Cần chọn trước một quy tắc $A$ biến mỗi tập huấn luyện $S$ cỡ $m=6$ thành một ngưỡng $\hat t = \hat t(S)$, sao cho $$L_{D_\eta}(h_{\hat t})-0{,}22$$ nhỏ. Một tập $S$ khác rút từ $D_\eta^6$ có thể cho ngưỡng khác, nên hiệu này ngẫu nhiên theo $S$.

**Trường hợp nhãn tất định.** Dưới $D_f$, mức tốt nhất là $L_{D_f}(h_3)=0$. Trên mẫu $S_f$ (cỡ $m=4$), $h_3$ và $h_4$ đều phân lớp đúng mọi quan sát. Tuy nhiên $h_4$ sai tại mức $x=3$, nên $L_{D_f}(h_4)=0{,}2$. Trong trường hợp này, nếu chỉ nhìn vào tập huấn luyện, ta không biết nên lựa chọn hàm nào trong $\{h_3, h_4\}$.
:::

Hiệu trong Định nghĩa 01.5 không tính được, vì $L_D(h)$ là kì vọng theo $D$ chưa biết, kể cả khi $h$ cho trước. Chúng ta cần một đại lượng tính được từ $S$ thay cho $L_D(h)$, cần biết khi nào thay được như vậy, và cần một quy tắc chọn giả thuyết dựa trên đại lượng này.

## 5. Rủi ro thực nghiệm và tối thiểu hóa rủi ro thực nghiệm

Đại lượng tính được từ dữ liệu là trung bình của hàm lỗi trên các quan sát của tập huấn luyện.

::: definition Định nghĩa 01.6 (Rủi ro thực nghiệm)
Cho hàm lỗi $\ell$ và một tập huấn luyện $S=(z_1,\ldots,z_m)\in\mathcal Z^m$. *Rủi ro thực nghiệm* của $h\in\mathcal H$ trên $S$ là
$$
L_S(h)=\frac1m\sum_{i=1}^m\ell(h,z_i).
$$
:::

Nghĩa là, $L_S(h)$ là rủi ro kì vọng dưới *phân bố thực nghiệm* (empirical distribution) của $S$, phân bố gán xác suất $\tfrac1m$ cho mỗi lần xuất hiện của một quan sát trong $S$. Với hàm lỗi 0–1, $L_S(h)$ là tỉ lệ lỗi (error rate) của $h$ trên tập huấn luyện.

::: example Ví dụ 01.5 (Rủi ro thực nghiệm trên một tập huấn luyện cỡ 6)
**Thiết lập.** Xét tập huấn luyện $S_\eta$ của Ví dụ 01.1 (phân bố $D_\eta$, cỡ mẫu $m=6$),
$$
\begin{aligned}
S_\eta=\big(&(1,0),(2,0),(2,1),\\
&(3,1),(4,0),(5,1)\big),
\end{aligned}
$$
lớp sáu hàm ngưỡng $h_t(x)=\mathbb 1[x\ge t]$ và hàm lỗi 0–1.

**Tính $L_{S_\eta}(h_3)$.** Hàm $h_3$ báo dương tính cho $x\in\{3,4,5\}$ và âm tính cho $x\in\{1,2\}$. So với nhãn trong $S_\eta$, nó sai trên $(2,1)$ và $(4,0)$, đúng trên bốn quan sát còn lại. Theo Định nghĩa 01.6,
$$
L_{S_\eta}(h_3)=\frac26=\frac13,
$$
tức $h_3$ phân lớp sai một phần ba số quan sát trong $S_\eta$.

**Các ngưỡng còn lại.** Với mỗi $t$, ta đếm số quan sát mà $h_t$ phân lớp sai rồi chia cho $6$:
$$
\begin{aligned}
&L_{S_\eta}(h_t)\\
&\quad=\frac16\,\#\{i:\ h_t(x_i)\ne y_i\}.
\end{aligned}
$$
Bảng dưới đặt kết quả cạnh rủi ro kì vọng của Ví dụ 01.2.

| $t$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ |
|---|---|---|---|---|---|---|
| số lỗi trên $S_\eta$ | $3$ | $2$ | $2$ | $3$ | $2$ | $3$ |
| $L_{S_\eta}(h_t)$ | $\tfrac12$ | $\tfrac13$ | $\tfrac13$ | $\tfrac12$ | $\tfrac13$ | $\tfrac12$ |
| $L_{D_\eta}(h_t)$ | $0{,}52$ | $0{,}32$ | $0{,}22$ | $0{,}32$ | $0{,}28$ | $0{,}48$ |

**Kết luận.** Ba hàm $h_2$, $h_3$, $h_5$ có cùng rủi ro thực nghiệm $\tfrac13$ nhưng rủi ro kì vọng lần lượt là $0{,}32$, $0{,}22$, $0{,}28$. Do đó, nếu chỉ dựa vào rủi ro thực nghiệm trên $S_\eta$, ta không phân biệt được hàm tốt nhất $h_3$ với hai hàm kém hơn.
:::

Với một giả thuyết chọn trước khi có tập huấn luyện, rủi ro thực nghiệm là một ước lượng không chệch của rủi ro kì vọng, tức kì vọng của nó theo $S$ bằng rủi ro kì vọng.

::: proposition Mệnh đề 01.7 (Tính không chệch của rủi ro thực nghiệm với giả thuyết cố định) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau.

- **Tập huấn luyện.** $S=(Z_1,\ldots,Z_m)$ theo dạng yếu của (T1): $Z_1,\ldots,Z_m$ là các biến ngẫu nhiên trên cùng một không gian xác suất, mỗi $Z_i$ có phân bố $D$; không giả sử chúng độc lập.
- **Giả thuyết được xét.** $h\in\mathcal H$, cố định, không phụ thuộc $S$.
- **Hàm lỗi.** $\ell$, thỏa (T2).
- **Rủi ro kì vọng.** $L_D(h)<\infty$.

**Bảo đảm.** Với mọi $m\ge1$,
$$
\mathbb E_S\big[L_S(h)\big]=L_D(h).
$$
Đây là bảo đảm theo kì vọng, so một đại lượng thực nghiệm với một đại lượng tổng thể (population quantity); nó không chặn độ lệch $\lvert L_S(h)-L_D(h)\rvert$ trên một tập huấn luyện cụ thể.
:::

::: proof Chứng minh Mệnh đề 01.7
**Lộ trình.** Tính kì vọng của từng số hạng trong $L_S(h)$, rồi dùng tính tuyến tính của kì vọng.

**Bước 1 (mỗi số hạng là biến ngẫu nhiên khả tích).** Vì $h$ cố định và $\ell(h,\cdot)$ đo được, $\ell(h,Z_i)$ là một biến ngẫu nhiên không âm chỉ phụ thuộc $Z_i$; giả thiết $h$ không phụ thuộc $S$ được dùng ở đây. Vì $Z_i$ có phân bố $D$, ta có
$$
\begin{aligned}
\mathbb E\,\ell(h,Z_i)&=\int_{\mathcal Z}\ell(h,z)\,dD(z)\\
&=L_D(h)<\infty,
\end{aligned}
$$
trong đó giả thiết cùng phân bố biên và $L_D(h)<\infty$ được dùng.

**Bước 2 (tính tuyến tính).** Kì vọng của một tổng hữu hạn các biến khả tích bằng tổng các kì vọng, nên
$$
\begin{aligned}
\mathbb E_S\big[L_S(h)\big]&=\frac1m\sum_{i=1}^m\mathbb E\,\ell(h,Z_i)\\
&=L_D(h).
\end{aligned}
$$
Tính tuyến tính đúng cả khi các $Z_i$ không độc lập, nên bước này chỉ dùng dạng yếu của (T1).

$\square$ Rủi ro thực nghiệm của một giả thuyết chọn trước khi có tập huấn luyện là ước lượng không chệch của rủi ro kì vọng. Vì vậy, để ước lượng rủi ro kì vọng của một hàm dự đoán, ta tính rủi ro thực nghiệm của nó trên một tập dữ liệu độc lập với tập huấn luyện dùng để chọn nó.
:::

Trên một tập huấn luyện cụ thể, $L_S(h)$ có thể khác $L_D(h)$. Trong Ví dụ 01.5, $L_{S_\eta}(h_3)=\tfrac13$, trong khi
$$
\mathbb E_{S\sim D_\eta^6}\big[L_S(h_3)\big]=L_{D_\eta}(h_3)=0{,}22.
$$

Dựa trên Mệnh đề 01.7, quy tắc chọn đơn giản nhất là thay $L_D$ chưa biết bằng $L_S$ và chọn giả thuyết có rủi ro thực nghiệm nhỏ nhất.

::: definition Định nghĩa 01.8 (Tối thiểu hóa rủi ro thực nghiệm)
Cho lớp giả thuyết $\mathcal H$ và hàm lỗi $\ell$. Với mỗi tập huấn luyện $S$, *tập nghiệm ERM* trên $S$ là
$$
\begin{aligned}
&\arg\min_{h\in\mathcal H}L_S(h)=\Big\{h\in\mathcal H:\\
&\qquad L_S(h)=\inf_{h'\in\mathcal H}L_S(h')\Big\},
\end{aligned}
$$
trong đó $\inf$ là cận dưới đúng (infimum). Mỗi phần tử $\hat h$ của tập này là một *nghiệm ERM*. Giả sử tập nghiệm ERM khác rỗng với mọi $S$. Một thuật toán học $A$ được gọi là *thuật toán ERM* trên $\mathcal H$ nếu với mọi $S$,
$$
A(S)\in\arg\min_{h\in\mathcal H}L_S(h).
$$
:::

Quy tắc ERM chỉ xác định tập nghiệm; một thuật toán ERM cụ thể còn cần một *quy tắc chọn khi bằng nhau* (tie-breaking). Trên lớp hàm ngưỡng của Ví dụ 01.1, hai quy tắc chọn khi bằng nhau cho hai thuật toán ERM:

- $A_{\min}(S)=h_{\hat t}$ với $\hat t=\min\big\{t:\ h_t\in\arg\min_{h\in\mathcal H}L_S(h)\big\}$;
- $A_{\max}(S)=h_{\hat t}$ với $\hat t=\max\big\{t:\ h_t\in\arg\min_{h\in\mathcal H}L_S(h)\big\}$.

::: example Ví dụ 01.6 (Các nghiệm ERM trên tập huấn luyện sàng lọc)
**Thiết lập.** Xét lớp sáu hàm ngưỡng, hàm lỗi 0–1 và hai tập huấn luyện $S_\eta$, $S_f$ của Ví dụ 01.1.

**Trên $S_\eta$.** Theo Ví dụ 01.5, rủi ro thực nghiệm nhỏ nhất là $\tfrac13$, đạt tại $h_2$, $h_3$, $h_5$, nên
$$
\arg\min_{h\in\mathcal H}L_{S_\eta}(h)=\{h_2,h_3,h_5\}.
$$
Hai quy tắc chọn khi bằng nhau cho hai kết quả, so với mức tốt nhất trong lớp $\min_tL_{D_\eta}(h_t)=0{,}22$:

| Quy tắc chọn | Hàm trả về | $L_{D_\eta}$ | $L_{D_\eta}-0{,}22$ |
|---|---|---|---|
| ngưỡng nhỏ nhất ($A_{\min}$) | $h_2$ | $0{,}32$ | $0{,}10$ |
| ngưỡng lớn nhất ($A_{\max}$) | $h_5$ | $0{,}28$ | $0{,}06$ |

Chỉ $h_3$ đạt mức $0{,}22$, nhưng cả $A_{\min}$ và $A_{\max}$ đều không chọn $h_3$.

**Tập nghiệm ERM dưới $D_f$.** Vì $h_3$ khớp mọi tập huấn luyện lấy mẫu từ $D_f$, ta có $\min_tL_S(h_t)=0$ và
$$
\begin{aligned}
&\arg\min_{h\in\mathcal H}L_S(h)\\
&\quad=\big\{h_t:\\
&\qquad\max\{x_i:\ y_i=0\}<t\\
&\qquad\le\min\{x_i:\ y_i=1\}\big\},
\end{aligned}
$$
với quy ước cực đại của tập rỗng bằng $0$ và cực tiểu của tập rỗng bằng $6$. Do đó hai thuật toán chọn như sau.

- **$A_{\max}$.** $\hat t=\min\{x_i:\ y_i=1\}$, nên $\hat t\in\{3,\ldots,6\}$.
- **$A_{\min}$.** $\hat t=1+\max\{x_i:\ y_i=0\}$, nên $\hat t\in\{1,2,3\}$.

**Trên $S_f$.** Các nhãn 0 nằm tại $x\in\{1,2\}$ và các nhãn 1 tại $x\in\{4,5\}$, nên điều kiện trên là $2<t\le4$. Do đó $h_3$ và $h_4$ là hai nghiệm ERM duy nhất ($h_2$ sai trên $(2,0)$, $h_5$ sai trên $(4,1)$).

- $A_{\min}$ chọn $\hat t=2+1=3$, tức $h_3$, có $L_{D_f}(h_3)=0$.
- $A_{\max}$ chọn $\hat t=4$, tức $h_4$, có $L_{D_f}(h_4)=0{,}2$.

**Kết luận.** Khi có nhiều nghiệm ERM, quy tắc chọn khi bằng nhau quyết định rủi ro kì vọng của hàm trả về, như với $h_3$ và $h_4$ của câu hỏi mở đầu.
:::

**Câu hỏi.** Với một thuật toán ERM $A$, kì vọng của $L_S(A(S))$ có bằng kì vọng của $L_D(A(S))$ không?

::: remark Nhận xét 01.9 (Giả thuyết chọn theo tập huấn luyện)
Khi thay $h$ bằng $A(S)$, giả thiết $h$ không phụ thuộc $S$ của Mệnh đề 01.7 không thỏa, nên Bước 1 của chứng minh hỏng: số hạng $\ell(A(S),Z_i)$ phụ thuộc toàn bộ $S$, kể cả $Z_i$. Do đó, nói chung,
$$
\begin{aligned}
&\mathbb E_S\big[L_S(A(S))\big]\\
&\quad\ne\mathbb E_S\big[L_D(A(S))\big].
\end{aligned}
$$
Ví dụ, dưới $D_f$ với thuật toán $A_{\max}$:

- vì $h_3$ khớp mọi tập huấn luyện lấy mẫu từ $D_f$, nghiệm ERM $A_{\max}(S)$ cũng khớp $S$, nên $\mathbb E_S\big[L_S(A_{\max}(S))\big]=0$;
- biến cố $S$ không chứa $x=3$ có xác suất $0{,}8^m$; trên biến cố đó, $A_{\max}$ chọn $\hat t\ge4$ và sai tại $x=3$, nên $\mathbb E_S\big[L_{D_f}(A_{\max}(S))\big]\ge0{,}2\cdot0{,}8^m>0$.

Đây là câu trả lời cho câu hỏi sau Định nghĩa 01.1: trên chính tập huấn luyện đã dùng để chọn hàm dự đoán, rủi ro thực nghiệm có thể đánh giá thấp rủi ro kì vọng, như với $A_{\max}$ ở trên.

Cách sửa là đánh giá $A(S)$ trên một tập dữ liệu mới $S'$ lấy mẫu từ $D$, độc lập với $S$. Khi lấy điều kiện theo $S$, hàm $A(S)$ cố định đối với $S'$, nên Mệnh đề 01.7 áp dụng được cho $L_{S'}(A(S))$.
:::

Với hàm học được, độ lệch giữa rủi ro kì vọng và rủi ro thực nghiệm trên chính tập huấn luyện dùng để chọn nó là đại lượng sau.

::: definition Định nghĩa 01.10 (Khoảng cách tổng quát hóa)
Cho thuật toán học $A$ và tập huấn luyện $S$. *Khoảng cách tổng quát hóa* (generalization gap) của $A$ trên $S$ là
$$
L_D\big(A(S)\big)-L_S\big(A(S)\big).
$$
:::

Khoảng cách tổng quát hóa là một biến ngẫu nhiên theo $S$ và có thể âm. Ví dụ: trên $S_\eta$, $A_{\max}$ trả về $h_5$, và
$$
\begin{aligned}
L_{D_\eta}(h_5)-L_{S_\eta}(h_5)&=0{,}28-\tfrac13\\
&=-\tfrac4{75}.
\end{aligned}
$$
Với $h$ cố định, $\mathbb E_S[L_D(h)-L_S(h)]=0$ theo Mệnh đề 01.7. Với hàm học được, kì vọng này có thể dương: dưới $D_f$, theo Nhận xét 01.9,
$$
\begin{aligned}
&\mathbb E_S\big[L_{D_f}(A_{\max}(S))\\
&\qquad-L_S(A_{\max}(S))\big]\\
&\quad\ge0{,}2\cdot0{,}8^m.
\end{aligned}
$$

::: remark Nhận xét 01.11 (Sự tồn tại nghiệm ERM và quy tắc chọn khi bằng nhau)
Với hàm lỗi 0–1, $L_S(h)$ chỉ nhận giá trị trong tập hữu hạn $\{0,\tfrac1m,\ldots,1\}$, nên cận dưới đúng của $L_S$ trên $\mathcal H$ đạt được. Do đó tập nghiệm ERM khác rỗng với mọi lớp $\mathcal H$ khác rỗng, kể cả lớp vô hạn. Giá trị nhỏ nhất có thể dương: trên lớp gồm cả $2^5=32$ hàm $\{1,\ldots,5\}\to\{0,1\}$, $\min_hL_{S_\eta}(h)=\tfrac16$, vì tại $x=2$, $S_\eta$ có cả nhãn 0 và nhãn 1.

Với hàm lỗi khác, tập nghiệm ERM có thể rỗng. Khi tập nghiệm có nhiều phần tử, một bảo đảm "cho mọi nghiệm ERM" mạnh hơn một bảo đảm "cho một nghiệm ERM".
:::

::: example Ví dụ 01.7 (Cận dưới đúng không đạt được của rủi ro thực nghiệm)
**Thiết lập.** Cho $\mathcal X=\mathcal Y=\mathbb R$, lớp $\mathcal H_+=\{h_w:x\mapsto wx,\ w>0\}$, hàm lỗi bình phương và tập huấn luyện một quan sát $S=((1,0))$.

**Rủi ro thực nghiệm.** Với $m=1$ và quan sát $(x,y)=(1,0)$,
$$
L_S(h_w)=(w\cdot1-0)^2=w^2 .
$$

**Cận dưới đúng.** Khi $w\to0^+$, $w^2\to0$, nên $\inf_{w>0}w^2=0$. Nhưng $w^2>0$ với mọi $w>0$, nên cận dưới đúng này không đạt tại $w>0$ nào.

**Kết luận.** Tập nghiệm ERM trên $S$ rỗng, nên giả thiết của Định nghĩa 01.8 không thỏa và không có thuật toán ERM trên $\mathcal H_+$.
:::

Khi tập nghiệm ERM có thể rỗng, hoặc khi thuật toán tối ưu chỉ cho nghiệm gần đúng, chúng ta cần khái niệm yếu hơn sau, gọi là ERM xấp xỉ (approximate ERM).

::: definition Định nghĩa 01.12 (ERM xấp xỉ)
Cho lớp giả thuyết $\mathcal H$, hàm lỗi $\ell$ và $\epsilon_{\mathrm{opt}}\ge0$. Một thuật toán học $A$ được gọi là *$\epsilon_{\mathrm{opt}}$-ERM* trên $\mathcal H$ nếu với mọi tập huấn luyện $S$,
$$
L_S(A(S))\le\inf_{h\in\mathcal H}L_S(h)+\epsilon_{\mathrm{opt}}.
$$
:::

Ba điểm sau suy ra trực tiếp từ Định nghĩa 01.12.

- Vì $\ell\ge0$, cận dưới đúng $\inf_{h\in\mathcal H}L_S(h)$ hữu hạn, nên khi $\epsilon_{\mathrm{opt}}>0$ luôn có giả thuyết thỏa bất đẳng thức trên.
- Khi $\epsilon_{\mathrm{opt}}=0$ và tập nghiệm ERM khác rỗng với mọi $S$, một $0$-ERM chính là một thuật toán ERM.
- Trong Ví dụ 01.7, với $\epsilon_{\mathrm{opt}}>0$, một $\epsilon_{\mathrm{opt}}$-ERM được phép trả về mọi $h_w$ với $w\in(0,\sqrt{\epsilon_{\mathrm{opt}}}\,]$, vì $w^2\le0+\epsilon_{\mathrm{opt}}$. Nghĩa là, ERM xấp xỉ vẫn có nghiệm khi tập nghiệm ERM rỗng.

Từ hai định nghĩa trên, ta có hai mức của *giả thiết tối ưu*, tách khỏi các giả thiết thống kê (T1), (T2):

- **(O1)** thuật toán tính được một nghiệm ERM chính xác;
- **(O2)** thuật toán chỉ tính được một $\epsilon_{\mathrm{opt}}$-ERM.

Hai giả thiết này không đặt điều kiện nào lên $D$.

Với lớp hàm ngưỡng trên một tập đầu vào hữu hạn, toàn bộ tập nghiệm ERM tính được bằng một lượt đếm.

::: algorithm Thuật toán 01.13 (ERM cho lớp hàm ngưỡng trên tập đầu vào hữu hạn)
**Đầu vào.** Ba thành phần sau.

- **Tập huấn luyện.** $S=((x_1,y_1),\ldots,(x_m,y_m))$ với $x_i\in\{1,\ldots,K\}$, $y_i\in\{0,1\}$.
- **Lớp giả thuyết.** $\{h_t=\mathbb 1[x\ge t]:\ t=1,\ldots,K+1\}$.
- **Hàm lỗi.** $\ell_{0\text{-}1}$.

**Khởi tạo.** Tính các số đếm $c_y(x)=\#\{i:\ x_i=x,\ y_i=y\}$ với $x\in\{1,\ldots,K\}$, $y\in\{0,1\}$. Đặt $E(1)=\sum_{x=1}^Kc_0(x)$, số lỗi của $h_1\equiv1$.

**Cập nhật.** Với $t=1,\ldots,K$, đặt $E(t+1)=E(t)-c_0(t)+c_1(t)$. Khi ngưỡng tăng từ $t$ lên $t+1$, chỉ dự đoán tại $x=t$ đổi từ $1$ sang $0$: các quan sát nhãn 0 tại $t$ hết sai, các quan sát nhãn 1 tại $t$ trở thành sai.

**Đầu ra.** Ba đại lượng sau.

- **Rủi ro thực nghiệm.** $L_S(h_t)=E(t)/m$ với mọi $t$.
- **Tập nghiệm ERM.** $\{h_t:\ E(t)=\min_{t'}E(t')\}$.
- **Một nghiệm ERM.** $h_t$ với $t$ là ngưỡng nhỏ nhất (hoặc lớn nhất) mà $E(t)$ đạt giá trị nhỏ nhất.

**Điều kiện dừng.** Dừng sau $K$ lần cập nhật.

**Chi phí.** $O(m)$ phép tính cho các số đếm và $O(K)$ cho các cập nhật, tổng cộng $O(m+K)$.
:::

Trên $S_\eta$ với $K=5$, các số đếm là $c_0=(1,1,0,1,0)$ và $c_1=(0,1,1,0,1)$. Khởi tạo $E(1)=1+1+0+1+0=3$, rồi cập nhật
$$
\begin{aligned}
E(2)&=3-1+0=2,\\
E(3)&=2-1+1=2,\\
E(4)&=2-0+1=3,\\
E(5)&=3-1+0=2,\\
E(6)&=2-0+1=3,
\end{aligned}
$$
nên $E=(3,2,2,3,2,3)$, khớp bảng số lỗi của Ví dụ 01.5. Chọn ngưỡng nhỏ nhất hay lớn nhất ở dòng **Một nghiệm ERM** cho đúng $A_{\min}$ hay $A_{\max}$.

Trên $S_\eta$, quy tắc chọn khi bằng nhau làm rủi ro kì vọng dưới $D_\eta$ thay đổi từ $0{,}22$ đến $0{,}32$. Trên một lớp đủ lớn, nó có thể làm rủi ro thay đổi từ $0$ đến $1$. Thuật toán sau chọn nghiệm ERM bằng cách ghi nhớ tập huấn luyện.

::: definition Định nghĩa 01.14 (Thuật toán ghi nhớ)
Cho tập đầu vào $\mathcal X$ với một σ-đại số chứa mọi tập một điểm, và $\mathcal Y=\{0,1\}$. Với một tập huấn luyện $s=((x_1,y_1),\ldots,(x_m,y_m))$, hàm $A_{\mathrm{gn}}(s):\mathcal X\to\{0,1\}$ nhận giá trị như sau.

- **Điểm trong tập huấn luyện.** Tại mỗi $x\in\{x_1,\ldots,x_m\}$, $A_{\mathrm{gn}}(s)(x)$ là nhãn chiếm đa số trong các quan sát của $s$ tại $x$, với nhãn $1$ khi số phiếu bằng nhau.
- **Điểm ngoài tập huấn luyện.** Tại mỗi $x\notin\{x_1,\ldots,x_m\}$, $A_{\mathrm{gn}}(s)(x)=0$.

Thuật toán $s\mapsto A_{\mathrm{gn}}(s)$ được gọi là *thuật toán ghi nhớ* (memorizing algorithm), và $A_{\mathrm{gn}}(s)$ là *hàm phân lớp ghi nhớ* (memorizing classifier).
:::

Ví dụ: trên $\mathcal X=\{1,\ldots,5\}$, $A_{\mathrm{gn}}(S_f)=\mathbb 1[x\in\{4,5\}]=h_4$. Hàm phân lớp ghi nhớ không dùng cấu trúc nào của $\mathcal X$. Dưới phân bố sau, nó sai trên một quan sát mới với xác suất $1$.

::: example Ví dụ 01.8 (Phân bố đều trên $[0,1]$ với nhãn hằng)
Với một tập đầu vào $\mathcal X$ có σ-đại số, kí hiệu $\mathcal M_{\mathcal X}$ là lớp mọi hàm phân lớp đo được $\mathcal X\to\{0,1\}$. Thiết lập của ví dụ gồm các thành phần sau.

- **Tập đầu vào và tập nhãn.** $\mathcal X=[0,1]$ với σ-đại số Borel, $\mathcal Y=\{0,1\}$.
- **Phân bố dữ liệu.** $D$: $X\sim U[0,1]$ và $Y=1$ chắc chắn.
- **Lớp giả thuyết.** $\mathcal H=\mathcal M_{\mathcal X}$.
- **Hàm lỗi.** $\ell_{0\text{-}1}$.
- **Tập huấn luyện.** $S=((X_1,1),\ldots,(X_m,1))$, với cỡ mẫu $m\ge1$ tùy ý.

Trong ví dụ này:

- lớp $\mathcal M_{\mathcal X}$ chứa hàm hằng $h_{\equiv1}$, có rủi ro $0$, và hàm chỉ báo $\mathbb 1_F$ của mọi tập hữu hạn $F\subset[0,1]$;
- một điểm $x$ với $\Pr(X=x)>0$ là một *nguyên tử* (atom) của phân bố; $U[0,1]$ *không có nguyên tử* (atomless), vì $\Pr(X=x)=0$ với mọi $x\in[0,1]$.
:::

::: proposition Mệnh đề 01.15 (Hàm phân lớp ghi nhớ có rủi ro kì vọng bằng 1) — chứng minh đầy đủ
**Giả thiết.** Năm thành phần sau, gồm thiết lập của Ví dụ 01.8 cùng thuật toán ghi nhớ.

- **Tập đầu vào.** $\mathcal X=[0,1]$ với σ-đại số Borel.
- **Phân bố dữ liệu.** $D$, phân bố của $(X,1)$ với $X\sim U[0,1]$.
- **Lớp giả thuyết.** $\mathcal H=\mathcal M_{\mathcal X}$.
- **Hàm lỗi.** $\ell_{0\text{-}1}$, thỏa (T2).
- **Thuật toán.** $A_{\mathrm{gn}}$.

**Bảo đảm.** Ba khẳng định sau đúng tất định, với mọi cỡ mẫu $m\ge1$ và mọi tập huấn luyện.

- **(a)** Với mọi tập huấn luyện $s$, $A_{\mathrm{gn}}(s)\in\mathcal H$ là một nghiệm ERM, nên $A_{\mathrm{gn}}$ là một thuật toán ERM trên $\mathcal H$, và dưới $D$, $L_S(A_{\mathrm{gn}}(S))=0$.
- **(b)** Dưới $D$, $L_D(A_{\mathrm{gn}}(S))=1$, nên khoảng cách tổng quát hóa bằng $1$ với mọi $m$.
- **(c)** Hàm hằng $h_{\equiv1}$ cũng là nghiệm ERM trên mọi tập huấn luyện dưới $D$, và $L_D(h_{\equiv1})=0=\inf_{h\in\mathcal H}L_D(h)$.
:::

::: proof Chứng minh Mệnh đề 01.15
**Lộ trình.** Kiểm tra hàm phân lớp ghi nhớ thuộc lớp, tính rủi ro thực nghiệm, rồi tính rủi ro kì vọng. Tính chất then chốt là một tập hữu hạn có xác suất $0$ dưới $U[0,1]$.

**Bước 1 (thuộc lớp).** Hàm $A_{\mathrm{gn}}(s)$ bằng $1$ trên một tập con của tập hữu hạn $F=\{x_1,\ldots,x_m\}$ và bằng $0$ ở nơi khác. Mọi tập con hữu hạn của $[0,1]$ là tập Borel, nên $A_{\mathrm{gn}}(s)\in\mathcal M_{\mathcal X}=\mathcal H$; giả thiết lớp gồm mọi hàm phân lớp đo được được dùng ở đây. Điều kiện đo được của Định nghĩa 01.4 được kiểm ở Phụ lục A(iii).

**Bước 2 (rủi ro thực nghiệm).** Rủi ro thực nghiệm của một hàm chỉ phụ thuộc giá trị của nó trên $F$, và tại mỗi điểm của $F$ số lỗi nhỏ nhất đạt được khi dự đoán nhãn đa số. Vì $A_{\mathrm{gn}}(s)$ làm đúng như vậy và thuộc $\mathcal H$, nó là một nghiệm ERM. Dưới $D$, mọi nhãn bằng $1$, nên $A_{\mathrm{gn}}(S)=\mathbb 1_F$ và $L_S(A_{\mathrm{gn}}(S))=0$.

**Bước 3 (rủi ro kì vọng).** Vì $Y=1$ chắc chắn, $A_{\mathrm{gn}}(S)$ sai trên $(X,Y)$ khi và chỉ khi $X\notin F$. Theo bất đẳng thức hợp (union bound),
$$
\begin{aligned}
\Pr(X\in F)&\le\sum_{i=1}^m\Pr(X=x_i)\\
&=0 .
\end{aligned}
$$
Do đó $L_D(A_{\mathrm{gn}}(S))=\Pr(X\notin F)=1$. Đẳng thức $\Pr(X=x_i)=0$ dùng giả thiết $D_{\mathcal X}$ không có nguyên tử.

**Bước 4 (một nghiệm ERM tốt).** Hàm hằng $h_{\equiv1}$ đúng trên mọi $(X,1)$, nên $L_S(h_{\equiv1})=L_D(h_{\equiv1})=0$, và $0$ là cận dưới đúng của $L_D\ge0$ trên $\mathcal H$.

$\square$ Trên lớp chứa mọi hàm phân lớp đo được, hai nghiệm ERM trên cùng một tập huấn luyện có rủi ro kì vọng $0$ và $1$, nên quy tắc chọn khi bằng nhau quyết định toàn bộ rủi ro kì vọng. Hàm phân lớp ghi nhớ là trường hợp cực đoan của **quá khớp** (overfitting).
:::

Chọn lớp giả thuyết trước khi có tập huấn luyện là một *thiên kiến quy nạp* (inductive bias), tức một cam kết về dạng của hàm dự đoán. Lớp $\mathcal M_{\mathcal X}$ của Ví dụ 01.8 không cam kết gì: trên mỗi tập huấn luyện, vô số hàm của lớp khớp mọi quan sát, với rủi ro kì vọng từ $0$ đến $1$.

Lớp hàm ngưỡng cam kết rằng dự đoán không giảm khi chỉ số đo tăng. Ví dụ: xét tập huấn luyện $\tilde S_f=((1,0),(3,1),(5,1))$ lấy mẫu từ $D_f$.

- Hàm phân lớp ghi nhớ là $A_{\mathrm{gn}}(\tilde S_f)=\mathbb 1[x\in\{3,5\}]\notin\mathcal H$. Hàm này sai tại $x=4$, nên có rủi ro $0{,}2$.
- Trong lớp hàm ngưỡng, chỉ $h_2$ (rủi ro $0{,}2$) và $h_3$ (rủi ro $0$) khớp $\tilde S_f$. Cả hai dự đoán đúng tại $x=4$, vì mọi hàm ngưỡng dương tính tại $x=3$ cũng dương tính tại $x=4$. Nghĩa là, lớp hàm ngưỡng loại được lỗi của hàm phân lớp ghi nhớ tại $x=4$.

Trên $S_f$, ngược lại, hàm phân lớp ghi nhớ trùng với $h_4\in\mathcal H$, nên lớp hàm ngưỡng không loại được nó.

Giá của thiên kiến quy nạp là lớp giả thuyết có thể không chứa hàm dự đoán tốt nhất. Quy tắc chọn khi bằng nhau là một thiên kiến khác, ở mức thuật toán. Vì $h_3$ và $h_4$ cùng có rủi ro thực nghiệm $0$ trên $S_f$, một bảo đảm học phải phát biểu trực tiếp cho $L_D(A(S))$ và phải cho phép thất bại trên những tập huấn luyện như $S_f$.

## 6. Học PAC trong trường hợp khả diễn

Để trả lời hai câu hỏi đầu sau Định nghĩa 01.5, hiệu nhỏ đến đâu và với xác suất nào theo $S$, chúng ta cần hai tham số.

- **Xác suất thất bại** (failure probability) $\delta>0$. Dưới $D_f$, $S_f$ không chứa quan sát nào tại $x=3$, và một tập huấn luyện cỡ $m$ bỏ sót mức này với xác suất $0{,}8^m$. Xác suất này dương với mọi $m$, nên mọi bảo đảm phải cho phép thất bại với một xác suất $\delta$ theo $S$.
- **Tham số độ chính xác** (accuracy parameter) $\epsilon>0$. Trên các tập huấn luyện còn lại, bảo đảm chỉ đòi $L_D(A(S))-\inf_{h\in\mathcal H}L_D(h)\le\epsilon$.

Ví dụ: nếu mức 3 chỉ chiếm $0{,}001$ dân số, một tập huấn luyện $500$ người bỏ sót mức này với xác suất $0{,}999^{500}\approx0{,}61$. Tham số $\epsilon$ cho phép bỏ qua những vùng có khối lượng xác suất (probability mass) nhỏ như vậy.

Trường hợp đơn giản nhất là khi lớp chứa một giả thuyết có rủi ro kì vọng bằng $0$.

::: definition Định nghĩa 01.16 (Tính khả diễn)
Cho hàm lỗi 0–1, một lớp giả thuyết $\mathcal H$ và một phân bố $D$ trên $\mathcal X\times\{0,1\}$. Cặp $(D,\mathcal H)$ được gọi là *khả diễn* (realizable) nếu tồn tại $h^\star\in\mathcal H$ với $L_D(h^\star)=0$.
:::

Trong Định nghĩa 01.16, giá trị nhỏ nhất $0$ phải đạt được tại một phần tử của $\mathcal H$. Giả thiết $(D,\mathcal H)$ khả diễn được gọi là *giả thiết khả diễn* (realizability assumption).

Khi $(D,\mathcal H)$ khả diễn, $Y=h^\star(X)$ hầu chắc chắn. Do đó, với xác suất $1$ theo $S\sim D^m$, $L_S(h^\star)=0$ và mọi nghiệm ERM có rủi ro thực nghiệm bằng $0$. Ví dụ: $(D_f,\mathcal H)$ của Ví dụ 01.1 khả diễn với $h^\star=h_3$.

::: remark Nhận xét 01.17 (Khả diễn là tính chất của cặp $(D,\mathcal H)$)
Tính khả diễn thay đổi khi thay một trong hai thành phần.

- **Cùng phân bố $D_f$.** Cặp với lớp hàm ngưỡng khả diễn; cặp với lớp hai hàm hằng $\{h_1,h_6\}$ thì không, vì $L_{D_f}(h_1)=0{,}4$ và $L_{D_f}(h_6)=0{,}6$.
- **Cùng lớp hàm ngưỡng.** Cặp với $D_f$ khả diễn; cặp với $D_\eta$ thì không, vì $\min_tL_{D_\eta}(h_t)=0{,}22>0$.
- **Cùng phân bố $D_\eta$, mọi lớp.** Không khả diễn: tại $x=2$, mọi hàm phân lớp $g$ sai với xác suất ít nhất $0{,}2\cdot\min\{\tfrac14,\tfrac34\}=0{,}05$, nên $L_{D_\eta}(g)\ge0{,}05$.

Điều kiện $\inf=0$ khác điều kiện $\min=0$. Ví dụ: lấy $X\sim U[0,1]$, $Y=\mathbb 1[X>\tfrac12]$ và
$$
\begin{aligned}
\mathcal H&=\{g_k:\ k\ge2\},\\
g_k(x)&=\mathbb 1\big[x\ge\tfrac12+\tfrac1k\big].
\end{aligned}
$$
Hàm $g_k$ chỉ sai trên khoảng $(\tfrac12,\tfrac12+\tfrac1k)$, nên $L_D(g_k)=\tfrac1k$. Do đó $\inf_kL_D(g_k)=0$ nhưng không đạt, và cặp này không khả diễn.
:::

::: definition Định nghĩa 01.18 (Học PAC trong trường hợp khả diễn)
Cho tập đầu vào $\mathcal X$, tập nhãn $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và lớp giả thuyết $\mathcal H$; kí hiệu $\mathbb N=\{1,2,\ldots\}$. Một thuật toán học $A$ được gọi là *thuật toán học PAC* cho $\mathcal H$ nếu tồn tại một hàm $M:(0,1)^2\to\mathbb N$ sao cho bất đẳng thức
$$
\Pr_{S\sim D^m}\big[L_D(A(S))\le\epsilon\big]\ge1-\delta
$$
đúng với mọi lựa chọn của ba thành phần sau.

- **Tham số độ chính xác và xác suất thất bại.** $\epsilon,\delta\in(0,1)$.
- **Phân bố dữ liệu.** $D$ trên $\mathcal X\times\mathcal Y$, với $(D,\mathcal H)$ khả diễn.
- **Cỡ mẫu.** $m\ge M(\epsilon,\delta)$.

Lớp $\mathcal H$ được gọi là *học được PAC* (PAC learnable) nếu tồn tại một thuật toán học PAC cho $\mathcal H$.
:::

**Câu hỏi.** Cỡ mẫu đủ trong Định nghĩa 01.18 có được phép phụ thuộc vào phân bố $D$ không?

Viết gọn, thứ tự lượng từ của định nghĩa là
$$
\begin{aligned}
&\exists A\ \ \exists M\ \ \forall\epsilon,\delta\in(0,1)\\
&\forall D\ \ \forall m\ge M(\epsilon,\delta):\\
&\qquad\Pr_{S\sim D^m}\big[L_D(A(S))\le\epsilon\big]\ge1-\delta ,
\end{aligned}
$$
trong đó $D$ chạy trên các phân bố mà $(D,\mathcal H)$ khả diễn. Ta đọc thứ tự lượng từ như sau.

- **$\exists M$ đứng trước $\forall D$.** Cỡ mẫu đủ chỉ phụ thuộc $(\epsilon,\delta)$, không phụ thuộc $D$; bảo đảm là *không phụ thuộc phân bố* (distribution-free). Nếu đổi chỗ thành "$\forall D\ \exists m$", ta được một khái niệm yếu hơn, trong đó cỡ mẫu được phép phụ thuộc phân bố chưa biết.
- **$\exists A$ đứng trước $\forall D$.** Thuật toán phải được chọn trước khi biết $D$, đúng như yêu cầu $D$ chưa biết trong Định nghĩa 01.5.
- **$\exists A$ đứng trước $\forall\epsilon,\delta$.** Thuật toán không nhận $\epsilon$, $\delta$ làm đầu vào.

Xác suất được lấy theo $S\sim D^m$, với $D$ cố định bên trong dấu $\Pr$. Tham số độ chính xác $\epsilon$ là ngưỡng cho rủi ro kì vọng, còn $1-\delta$ là *độ tin cậy* (confidence). Với $(D,\mathcal H)$ khả diễn, $\inf_{h\in\mathcal H}L_D(h)=0$, nên bất đẳng thức của Định nghĩa 01.18 chính là mục tiêu của Định nghĩa 01.5 với độ chính xác $\epsilon$ và độ tin cậy $1-\delta$.

Định nghĩa 01.4 chỉ xét thuật toán tất định. Một thuật toán sinh thêm đại lượng ngẫu nhiên $\xi$ độc lập với $S$, như khi lấy mẫu mini-batch, cần một định nghĩa mở rộng với đầu ra $A(S;\xi)$; khi đó xác suất trong Định nghĩa 01.18 được lấy theo cả $S$ và $\xi$.

::: remark Nhận xét 01.19 (Độ tin cậy lấy theo các lần lấy tập huấn luyện)
Xác suất $1-\delta$ được tính trước khi lấy mẫu, theo các lần lấy mẫu giả định lặp lại từ cùng $D$. Sau khi đã có $S$, $L_D(A(S))$ là một số: hoặc không vượt quá $\epsilon$, hoặc vượt quá. Do đó, khi $\delta=0{,}05$, câu "với xác suất $0{,}95$" có thể hiểu theo nghĩa: trong 100 lần huấn luyện, thì có khoảng 95 lần tìm được giả thuyết $A(S)$ có rủi ro nhiều nhất là $\epsilon$.
:::

Trong Định nghĩa 01.18, chỉ cần tồn tại một hàm $M$; giá trị nhỏ nhất có thể của $M$ đo lượng dữ liệu mà thuật toán cần.

::: definition Định nghĩa 01.20 (Độ phức tạp mẫu)
Cho $\mathcal X$, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và lớp $\mathcal H$ như trong Định nghĩa 01.18. Cho $\epsilon,\delta\in(0,1)$. *Độ phức tạp mẫu* (sample complexity) được định nghĩa cho một thuật toán và cho lớp giả thuyết.

- **Độ phức tạp mẫu của thuật toán.** $m_A(\epsilon,\delta)$ của thuật toán học $A$ là số $m_0\in\mathbb N$ nhỏ nhất sao cho bất đẳng thức xác suất của Định nghĩa 01.18 đúng với mọi $D$ mà $(D,\mathcal H)$ khả diễn và mọi $m\ge m_0$; khi không có $m_0$ nào như vậy, $m_A(\epsilon,\delta)=\infty$.
- **Độ phức tạp mẫu của lớp.** $m_{\mathcal H}(\epsilon,\delta)$ là giá trị nhỏ nhất của $m_A(\epsilon,\delta)$ trên mọi thuật toán học $A$ cho $\mathcal H$, lấy riêng cho từng cặp $(\epsilon,\delta)$:
  $$
  m_{\mathcal H}(\epsilon,\delta)=\min_{A}m_A(\epsilon,\delta).
  $$
:::

Hai giá trị nhỏ nhất tồn tại vì mọi tập con khác rỗng của $\mathbb N\cup\{\infty\}$ có phần tử nhỏ nhất. Lớp $\mathcal H$ học được PAC khi và chỉ khi có một thuật toán $A$ với $m_A(\epsilon,\delta)<\infty$ cho mọi $(\epsilon,\delta)$; khi đó $A$ cùng $M=m_A$ thỏa Định nghĩa 01.18.

::: remark Nhận xét 01.21 (Độ phức tạp mẫu của thuật toán và của lớp)
Ba điểm sau làm rõ Định nghĩa 01.20.

**Cận trên và cận dưới.** Vì $m_{\mathcal H}\le m_A$ với mọi $A$, một cận trên cho $m_{\mathcal H}$ chỉ cần một thuật toán tốt; một cận dưới phải lập luận cho mọi thuật toán.

**Thuật toán đạt $m_{\mathcal H}$.** Trong Định nghĩa 01.20, cũng như ở giáo trình *Understanding Machine Learning: From Theory to Algorithms* (Shalev-Shwartz và Ben-David, 2014; viết tắt UML), §3.1, $m_{\mathcal H}$ được lấy riêng cho từng cặp $(\epsilon,\delta)$, nên thuật toán đạt nó có thể đổi theo cặp. Do đó, nếu chỉ dùng định nghĩa, từ $m_{\mathcal H}(\epsilon,\delta)<\infty$ với mọi $(\epsilon,\delta)$ ta chưa suy ra được một thuật toán dùng được cho mọi cặp.

**Mọi cỡ mẫu từ $m_0$ trở lên.** Bảo đảm phải đúng với mọi $m\ge m_0$, vì thành công ở cỡ $m$ không kéo theo thành công ở cỡ $m+1$. Ví dụ: gọi $D_1$ là phân bố trên $\{1,\ldots,5\}\times\{0,1\}$ với
$$
D_1(x,y)=0{,}2\cdot\mathbb 1[y=1],
$$
tức $D_{\mathcal X}$ đều và $Y=1$ chắc chắn; $(D_1,\mathcal H)$ khả diễn với $h^\star=h_1$. Trên lớp hàm ngưỡng, xét thuật toán
$$
A(S)=\begin{cases}
A_{\max}(S) & m\ \text{chẵn},\\
h_6\equiv0 & m\ \text{lẻ}.
\end{cases}
$$

- **Cỡ mẫu chẵn.** Thuật toán thất bại với xác suất không quá $0{,}8^m$.
- **Cỡ mẫu lẻ.** Vì $L_{D_1}(h_6)=1$, thuật toán thất bại chắc chắn với mọi $\epsilon\in(0,1)$.

Do đó $m_A(\epsilon,\delta)=\infty$ với mọi $(\epsilon,\delta)$.
:::

::: example Ví dụ 01.9 (Xác suất thất bại và cỡ mẫu cho một phân bố khả diễn)
**Thiết lập.** Xét phân bố $D_f$ của Ví dụ 01.1, lớp sáu hàm ngưỡng, hàm lỗi 0–1, tập huấn luyện $S\sim D_f^m$ và thuật toán ERM $A_{\max}$. Kí hiệu $\hat t\in\{3,4,5,6\}$ là ngưỡng mà $A_{\max}$ chọn, tức $A_{\max}(S)=h_{\hat t}$.

**Bước 1: rủi ro theo ngưỡng.** Vì $f=h_3$, hàm $h_{\hat t}$ sai đúng tại các mức $x\in\{3,\ldots,\hat t-1\}$. Có $\hat t-3$ mức như vậy, mỗi mức có xác suất $0{,}2$, nên
$$
\begin{aligned}
&L_{D_f}\big(A_{\max}(S)\big)\\
&\quad=0{,}2\,(\hat t-3)\\
&\quad\in\{0;\ 0{,}2;\ 0{,}4;\ 0{,}6\}.
\end{aligned}
$$

**Bước 2: xác suất rủi ro dương.** Theo Ví dụ 01.6, $\hat t$ là giá trị $x$ nhỏ nhất có nhãn 1 trong $S$ (hoặc $6$), nên $\hat t=3$ khi và chỉ khi $S$ có quan sát tại $x=3$. Do đó rủi ro dương khi và chỉ khi không quan sát nào của $S$ nằm tại $x=3$. Theo (T1), các quan sát độc lập, và mỗi quan sát khác $3$ với xác suất $0{,}8$, nên
$$
\begin{aligned}
&\Pr_{S\sim D_f^m}\Big[L_{D_f}\big(A_{\max}(S)\big)>0\Big]\\
&\quad=0{,}8^m .
\end{aligned}
$$

**Bước 3: cỡ mẫu khi $\epsilon=0{,}1$, $\delta=0{,}05$.** Theo Bước 1, giá trị dương nhỏ nhất của rủi ro là $0{,}2>0{,}1$. Vì vậy biến cố thành công $L_{D_f}(A_{\max}(S))\le0{,}1$ trùng với biến cố $L_{D_f}(A_{\max}(S))=0$, và cần $0{,}8^m\le0{,}05$. Dãy $0{,}8^m$ giảm theo $m$, và
$$
\begin{aligned}
0{,}8^{13}&\approx0{,}0550>0{,}05,\\
0{,}8^{14}&\approx0{,}0440\le0{,}05,
\end{aligned}
$$
nên điều kiện này đúng khi và chỉ khi $m\ge14$. Nghĩa là, với ít nhất $14$ quan sát, $A_{\max}$ trả về $h_3$ với xác suất ít nhất $0{,}95$.

**Bước 4: cỡ mẫu khi $\epsilon=0{,}25$, $\delta=0{,}05$.** Vì $0{,}2\le0{,}25<0{,}4$, thất bại khi và chỉ khi $\hat t\ge5$, tức cả $x=3$ và $x=4$ vắng mặt. Mỗi quan sát nằm ngoài $\{3,4\}$ với xác suất $0{,}6$, nên xác suất thất bại là $0{,}6^m$. Vì
$$
\begin{aligned}
0{,}6^{5}&\approx0{,}0778>0{,}05,\\
0{,}6^{6}&\approx0{,}0467\le0{,}05,
\end{aligned}
$$
cần $m\ge6$. Khi nới $\epsilon$ từ $0{,}1$ lên $0{,}25$, cỡ mẫu cần giảm từ $14$ xuống $6$.

**Bước 5: kì vọng.** Theo Phụ lục C.2,
$$
\begin{aligned}
&\mathbb E_S\big[L_{D_f}(A_{\max}(S))\big]\\
&\quad=0{,}2\,(0{,}8^m+0{,}6^m+0{,}4^m).
\end{aligned}
$$
Tại $m=10$, tổng trong ngoặc xấp xỉ $0{,}1135$, nên kì vọng xấp xỉ $0{,}2\cdot0{,}1135\approx0{,}0227$. Trong khi đó $\mathbb E_S\big[L_S(A_{\max}(S))\big]=0$, vì $A_{\max}$ khớp mọi tập huấn luyện lấy mẫu từ $D_f$.

**Bước 6: đọc theo các lần lấy mẫu lặp lại.** Ở $m=14$, xác suất thất bại là $0{,}8^{14}\approx0{,}0440$. Nghĩa là, nếu lặp lại nhiều lần việc lấy một tập huấn luyện cỡ $14$, khoảng $4{,}4\%$ số tập huấn luyện cho một hàm phân lớp có rủi ro kì vọng ít nhất $0{,}2$.

**Kết luận.** Các cỡ mẫu $14$ và $6$ chỉ đủ cho riêng $A_{\max}$ và riêng $D_f$, nên không phải $m_{A_{\max}}(\epsilon,\delta)$; chúng chỉ cho một khẳng định dạng "$\forall D\ \exists m$". Cỡ mẫu $m_0$ trong Định nghĩa 01.20 phải đúng cho mọi phân bố khả diễn, còn các con số này thay đổi khi khối lượng xác suất của điểm $x=3$ thay đổi.
:::

Dưới $D_\eta$, không lớp nào khả diễn, nên Định nghĩa 01.18 không áp dụng được cho bài toán sàng lọc. Chúng ta cần bỏ giả thiết khả diễn.

## 7. Học PAC bất khả diễn và quy tắc Bayes

Dưới $D_\eta$, mọi hàm phân lớp có rủi ro ít nhất $0{,}05$ (Nhận xét 01.17), nên yêu cầu $L_D(A(S))\le\epsilon$ không đạt được khi $\epsilon<0{,}05$. Mức rủi ro dùng để so với $L_D(A(S))$ được gọi là *đối tượng so sánh* (comparator). Trong Định nghĩa 01.5, đối tượng so sánh là $\inf_{h\in\mathcal H}L_D(h)$; trong trường hợp khả diễn, nó bằng $0$. Dưới $D_\eta$, đối tượng so sánh phải là một mức dương. Mức thấp nhất có thể trên mọi hàm phân lớp là đại lượng sau.

::: definition Định nghĩa 01.22 (Rủi ro Bayes)
Cho tập nhãn $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và một phân bố $D$ trên $\mathcal X\times\{0,1\}$. *Rủi ro Bayes* (Bayes risk) của $D$ là
$$
L_D^{\mathrm{Bayes}}=\inf_{g\in\mathcal M_{\mathcal X}}L_D(g).
$$
Với hàm lỗi $\ell_c$, cận dưới đúng $\inf_{g\in\mathcal M_{\mathcal X}}L^c_D(g)$ được gọi là rủi ro Bayes dưới $\ell_c$.
:::

Rủi ro Bayes chỉ phụ thuộc $D$, không phụ thuộc lớp $\mathcal H$ hay tập huấn luyện.

::: proposition Mệnh đề 01.23 (Quy tắc Bayes cho hàm lỗi 0–1 và hàm lỗi có trọng số) — đọc thêm
**Giả thiết.** Bốn thành phần sau.

- **Phân bố dữ liệu.** $D$ trên $\mathcal X\times\{0,1\}$, với phân bố biên $D_{\mathcal X}$.
- **Xác suất có điều kiện của nhãn 1.** $\eta:\mathcal X\to[0,1]$, một hàm đo được với $\eta(X)=\Pr(Y=1\mid X)$ hầu chắc chắn.
- **Hàm lỗi.** $\ell_{0\text{-}1}$ trong phần (a), $\ell_c$ với $c_{FP},c_{FN}>0$ trong phần (b); cả hai thỏa (T2).
- **Tập hàm được xét.** $\mathcal M_{\mathcal X}$, mọi hàm phân lớp đo được, không giới hạn trong một lớp $\mathcal H$.

**Bảo đảm.** Hai khẳng định sau về đại lượng tổng thể.

- **(a)** Hàm phân lớp tối ưu Bayes (Bayes optimal classifier) $h_{\mathrm{Bayes}}(x)=\mathbb 1[\eta(x)\ge\tfrac12]$ thuộc $\mathcal M_{\mathcal X}$ và $L_D(h_{\mathrm{Bayes}})\le L_D(g)$ với mọi $g\in\mathcal M_{\mathcal X}$, nên
  $$
  \begin{aligned}
  &L_D^{\mathrm{Bayes}}\\
  &\quad=L_D(h_{\mathrm{Bayes}})\\
  &\quad=\mathbb E\min\{\eta(X),\\
  &\qquad\quad1-\eta(X)\}.
  \end{aligned}
  $$
- **(b)** Dưới $\ell_c$, hàm $x\mapsto\mathbb 1\big[\eta(x)\ge c_{FP}/(c_{FP}+c_{FN})\big]$ có rủi ro nhỏ nhất trên $\mathcal M_{\mathcal X}$, bằng $\mathbb E\min\{c_{FN}\,\eta(X),\ c_{FP}(1-\eta(X))\}$.

Nói chung hàm tối ưu không duy nhất. Khi $\eta(X)$ bằng ngưỡng ($\tfrac12$ trong (a), $c_{FP}/(c_{FP}+c_{FN})$ trong (b)) với xác suất $0$, hàm tối ưu là duy nhất nếu bỏ qua một tập có xác suất $0$. Dưới $D_\eta$, điều kiện này thỏa với $\ell_{0\text{-}1}$ (ngưỡng $\tfrac12$) và với $\ell_c$ khi $(c_{FP},c_{FN})=(1,4)$ (ngưỡng $\tfrac15$).
:::

Chứng minh nằm ở Phụ lục B: tại từng điểm $x$, ta chọn nhãn có rủi ro có điều kiện (conditional risk) nhỏ hơn, rồi lấy kì vọng theo $X$. Phần (b) trả lời câu hỏi thực hành của ứng dụng sàng lọc: ngưỡng báo dương tính trên $\eta(x)$ là $c_{FP}/(c_{FP}+c_{FN})$, và ngưỡng này bằng $\tfrac12$ chỉ khi $c_{FP}=c_{FN}$.

::: example Ví dụ 01.10 (Quy tắc Bayes trong ví dụ sàng lọc)
**Thiết lập.** Xét phân bố $D_\eta$ của Ví dụ 01.1, lớp sáu hàm ngưỡng, hàm lỗi 0–1 và hàm lỗi $\ell_c$ với $(c_{FP},c_{FN})=(1,4)$.

**Hàm Bayes dưới hàm lỗi 0–1.** Theo Mệnh đề 01.23(a), hàm Bayes báo dương tính đúng tại các mức có $\eta(x)\ge\tfrac12$. Điều kiện này đúng tại $x=3$ ($\eta=\tfrac34$) và $x=5$ ($\eta=1$), sai tại $x=1$, $x=2$ và $x=4$ ($\eta=\tfrac25$). Do đó $h_{\mathrm{Bayes}}=\mathbb 1[x\in\{3,5\}]$, một hàm không thuộc lớp hàm ngưỡng.

**Rủi ro Bayes dưới hàm lỗi 0–1.** Theo Mệnh đề 01.23(a), $L_{D_\eta}^{\mathrm{Bayes}}$ là kì vọng của $\min\{\eta(X),1-\eta(X)\}$. Tại năm mức, giá trị này lần lượt là $0;\ \tfrac14;\ \tfrac14;\ \tfrac25;\ 0$, nên
$$
\begin{aligned}
&L_{D_\eta}^{\mathrm{Bayes}}\\
&\quad=0{,}2\Big(0+\tfrac14+\tfrac14+\tfrac25+0\Big)\\
&\quad=0{,}2\cdot0{,}9=0{,}18 .
\end{aligned}
$$
Mức tốt nhất trong lớp là $\min_tL_{D_\eta}(h_t)=0{,}22$, cao hơn rủi ro Bayes một lượng $0{,}22-0{,}18=0{,}04$.

**Hàm Bayes dưới $\ell_c$.** Với $(c_{FP},c_{FN})=(1,4)$, ngưỡng của Mệnh đề 01.23(b) là
$$
\frac{c_{FP}}{c_{FP}+c_{FN}}=\frac1{1+4}=\frac15 .
$$
Vì $\eta(x)\ge\tfrac15$ tại $x\in\{2,3,4,5\}$ và $\eta(1)=0$, hàm Bayes dưới $\ell_c$ là $h_2\in\mathcal H$.

**Rủi ro Bayes dưới $\ell_c$.** Hàm $h_2$ báo âm tính tại $x=1$, nơi $\eta(1)=0$, nên không bỏ sót người bệnh nào; nó báo nhầm tại các mức $2$ đến $5$ với xác suất có điều kiện $1-\eta(x)$. Theo công thức của Ví dụ 01.2,
$$
\begin{aligned}
&L^c_{D_\eta}(h_2)\\
&\quad=0{,}2\,\Big(0+\tfrac34+\tfrac14+\tfrac35+0\Big)\\
&\quad=0{,}2\cdot1{,}6=0{,}32.
\end{aligned}
$$
Theo Mệnh đề 01.23(b), giá trị này là rủi ro Bayes dưới $\ell_c$; nó bằng $\min_tL^c_{D_\eta}(h_t)$ ở Ví dụ 01.2.

**Kết luận.** Lớp hàm ngưỡng chứa hàm Bayes dưới hàm lỗi có trọng số nhưng không chứa hàm Bayes dưới hàm lỗi 0–1.
:::

Hai đối tượng so sánh, $\inf_{h\in\mathcal H}L_D(h)$ và $L_D^{\mathrm{Bayes}}$, cho hai cách đo một hàm dự đoán tốt đến đâu.

::: definition Định nghĩa 01.24 (Rủi ro vượt mức)
Cho $D$, $\mathcal H$, $\ell$ và một hàm dự đoán $h$ với $L_D(h)<\infty$. *Rủi ro vượt mức* (excess risk) của $h$:

- so với $\mathcal H$ là $L_D(h)-\inf_{h'\in\mathcal H}L_D(h')$;
- so với rủi ro Bayes, trong phân lớp, là $L_D(h)-L_D^{\mathrm{Bayes}}$.
:::

Khi nói đến rủi ro vượt mức, ta phải nêu đối tượng so sánh. Trong phân lớp, mọi rủi ro đều hữu hạn vì $\ell_{0\text{-}1}$ và $\ell_c$ bị chặn, và hai rủi ro vượt mức liên hệ qua đẳng thức
$$
\begin{aligned}
&L_D(h)-L_D^{\mathrm{Bayes}}\\
&\quad=\Big[L_D(h)-\inf_{h'\in\mathcal H}L_D(h')\Big]\\
&\qquad+\Big[\inf_{h'\in\mathcal H}L_D(h')-L_D^{\mathrm{Bayes}}\Big],
\end{aligned}
$$
trong đó số hạng thứ hai chỉ phụ thuộc lớp đã chọn, không phụ thuộc $h$.

Ví dụ: dưới $D_\eta$ với hàm lỗi 0–1, lấy $h=h_2$. Theo Ví dụ 01.2, $L_{D_\eta}(h_2)=0{,}32$ và $\min_tL_{D_\eta}(h_t)=0{,}22$; theo Ví dụ 01.10, $L^{\mathrm{Bayes}}_{D_\eta}=0{,}18$. Do đó
$$
\begin{aligned}
&L_{D_\eta}(h_2)-\min_tL_{D_\eta}(h_t)\\
&\quad=0{,}32-0{,}22=0{,}10,\\
&\min_tL_{D_\eta}(h_t)-L^{\mathrm{Bayes}}_{D_\eta}\\
&\quad=0{,}22-0{,}18=0{,}04,\\
&L_{D_\eta}(h_2)-L^{\mathrm{Bayes}}_{D_\eta}\\
&\quad=0{,}32-0{,}18=0{,}14.
\end{aligned}
$$
Hiệu $0{,}04$ chỉ phụ thuộc lớp hàm ngưỡng, còn hiệu $0{,}10$ là phần rủi ro mất thêm do chọn $h_2$ thay cho $h_3$.

**Câu hỏi.** Nên so $L_D(A(S))$ với $\inf_{h\in\mathcal H}L_D(h)$ hay với rủi ro Bayes $L_D^{\mathrm{Bayes}}$?

Đối tượng so sánh của định nghĩa tiếp theo là $\inf_{h\in\mathcal H}L_D(h)$, không phải $L_D^{\mathrm{Bayes}}$, vì hai lý do.

- **(i)** Rủi ro của đầu ra một thuật toán học đúng lớp luôn ít nhất bằng $\inf_{h\in\mathcal H}L_D(h)$; hiệu $0{,}04$ của Ví dụ 01.10 không giảm khi $m$ tăng.
- **(ii)** Khi $\mathcal X$ vô hạn, không thuật toán nào bảo đảm được $L_D(A(S))\le L_D^{\mathrm{Bayes}}+\epsilon$ cho mọi $D$ với cỡ mẫu không phụ thuộc $D$, kể cả khi đầu ra được phép nằm ngoài $\mathcal H$ (UML §5.1). Khi $\mathcal X$ hữu hạn, như trong ví dụ sàng lọc, yêu cầu đó đạt được bằng ERM trên $\mathcal M_{\mathcal X}$ (Bài 02).

Vì vậy, với một thuật toán đúng lớp, $\inf_{h\in\mathcal H}L_D(h)$ là cận dưới đúng của rủi ro của đầu ra: không thuật toán đúng lớp nào có rủi ro nhỏ hơn mức này. Phần chênh so với rủi ro Bayes là số hạng thứ hai của đẳng thức trên, tức giá của thiên kiến quy nạp.

::: definition Định nghĩa 01.25 (Học PAC bất khả diễn)
Cho tập quan sát $\mathcal Z$, lớp giả thuyết $\mathcal H$ và hàm lỗi $\ell:\mathcal H\times\mathcal Z\to[0,\infty)$. Một thuật toán học $A$ được gọi là *thuật toán học PAC bất khả diễn* cho $\mathcal H$ nếu tồn tại một hàm $M:(0,1)^2\to\mathbb N$ sao cho bất đẳng thức
$$
\begin{aligned}
&\Pr_{S\sim D^m}\Big[L_D(A(S))\\
&\quad\le\inf_{h\in\mathcal H}L_D(h)+\epsilon\Big]\\
&\quad\ge1-\delta
\end{aligned}
$$
đúng với mọi lựa chọn của ba thành phần sau.

- **Tham số độ chính xác và xác suất thất bại.** $\epsilon,\delta\in(0,1)$.
- **Phân bố dữ liệu.** $D$ trên $\mathcal Z$, với $D$ có rủi ro hữu hạn trên $\mathcal H$ (Định nghĩa 01.3).
- **Cỡ mẫu.** $m\ge M(\epsilon,\delta)$.

Lớp $\mathcal H$ được gọi là *học được PAC bất khả diễn* (agnostic PAC learnable) nếu tồn tại một thuật toán học PAC bất khả diễn cho $\mathcal H$.
:::

So với Định nghĩa 01.18, Định nghĩa 01.25 thay đổi ba thành phần và giữ nguyên thứ tự lượng từ.

- **Thiết lập.** Tập quan sát $\mathcal Z$ và hàm lỗi $\ell\ge0$ bất kì, thay cho phân lớp nhị phân với hàm lỗi 0–1.
- **Biến cố.** Rủi ro vượt mức của $A(S)$ so với $\mathcal H$, tức hiệu trong Định nghĩa 01.5, không quá $\epsilon$.
- **Họ phân bố.** Mọi $D$ có rủi ro hữu hạn trên $\mathcal H$, thay cho mọi $D$ mà $(D,\mathcal H)$ khả diễn. Định nghĩa không đòi nhãn tất định, nên áp dụng được cho $D_\eta$.

Độ phức tạp mẫu của Định nghĩa 01.20 mở rộng sang thiết lập này với họ phân bố và biến cố mới.

Với hàm lỗi không bị chặn, như hàm lỗi bình phương của Ví dụ 01.3, yêu cầu này cho mọi phân bố có rủi ro hữu hạn nói chung không thỏa được; bảo đảm không phụ thuộc phân bố cần thêm giả thiết, chẳng hạn hàm lỗi bị chặn.

::: remark Nhận xét 01.26 (Cận dưới đúng thay cho giá trị nhỏ nhất)
Trong Định nghĩa 01.25, ta viết $\inf$ vì giá trị nhỏ nhất có thể không tồn tại (Nhận xét 01.17), còn cận dưới đúng luôn tồn tại trong $[0,\infty)$. Hai cách viết trùng nhau khi cận dưới đúng đạt được, như $\min_tL_{D_\eta}(h_t)=0{,}22$.

Với hàm lỗi 0–1 và $(D,\mathcal H)$ khả diễn, $\inf_{h\in\mathcal H}L_D(h)=0$ và biến cố của Định nghĩa 01.25 trùng với biến cố của Định nghĩa 01.18. Do đó mọi thuật toán học PAC bất khả diễn cho $\mathcal H$ cũng là thuật toán học PAC cho $\mathcal H$ trong trường hợp khả diễn, với cùng hàm $M$.
:::

::: remark Nhận xét 01.27 (Học đúng lớp và học ngoài lớp)
Theo Định nghĩa 01.4, $A(S)\in\mathcal H$. Trong *học ngoài lớp* (improper learning; UML gọi là representation-independent learning), đầu ra được phép thuộc một lớp lớn hơn, còn đối tượng so sánh vẫn là $\inf_{h\in\mathcal H}L_D(h)$. Một thuật toán ngoài lớp có thể có rủi ro thấp hơn đối tượng so sánh. Ví dụ: dưới $D_\eta$, hàm $\mathbb 1[x\in\{3,5\}]$ không thuộc lớp hàm ngưỡng và có rủi ro $0{,}18<0{,}22$.
:::

Hai định nghĩa học PAC trả lời câu hỏi **học có nghĩa là gì**. Trong bài toán học thống kê (Định nghĩa 01.5), học là chọn từ tập huấn luyện $S\sim D^m$ một hàm dự đoán $A(S)$ thỏa
$$
L_D(A(S))\le\inf_{h\in\mathcal H}L_D(h)+\epsilon
$$
với xác suất ít nhất $1-\delta$ theo $S$, khi $m$ vượt một ngưỡng không phụ thuộc phân bố. Rủi ro thực nghiệm không có mặt trong yêu cầu này.

## 8. Giới hạn của rủi ro thực nghiệm

Để phát biểu Mệnh đề 01.15 bằng ngôn ngữ học PAC, chúng ta cần gọi tên loại cận mà nó bác bỏ: một cận cho khoảng cách tổng quát hóa, đúng cho mọi thuật toán ERM trên lớp.

::: definition Định nghĩa 01.28 (Cận tổng quát hóa cho mọi thuật toán ERM)
Cho tập đầu vào $\mathcal X$, tập nhãn $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và lớp giả thuyết $\mathcal H$. Một hàm $\beta:\mathbb N\times(0,1)\to[0,\infty)$ được gọi là *cận tổng quát hóa cho mọi thuật toán ERM* trên $\mathcal H$ nếu
$$
\begin{aligned}
&\forall\hat A\ \ \forall D\\
&\forall m\ge1\ \ \forall\delta\in(0,1):\\
&\Pr_{S\sim D^m}\Big[L_D\big(\hat A(S)\big)-L_S\big(\hat A(S)\big)\\
&\qquad\le\beta(m,\delta)\Big]\ge1-\delta ,
\end{aligned}
$$
trong đó $\hat A$ là một thuật toán ERM bất kì trên $\mathcal H$ (ứng với một quy tắc chọn khi bằng nhau bất kì thỏa điều kiện đo được của Định nghĩa 01.4), còn $D$ là một phân bố bất kì trên $\mathcal X\times\mathcal Y$.
:::

Cận tầm thường $\beta\equiv1$ luôn thỏa, vì $L_D\le1$ với hàm lỗi 0–1.

**Câu hỏi.** Trên lớp $\mathcal M_{\mathcal X}$ của Ví dụ 01.8, có cận tổng quát hóa nào cho mọi thuật toán ERM nhỏ hơn cận tầm thường $\beta\equiv1$ không?

::: corollary Hệ quả 01.29 (Rủi ro thực nghiệm nhỏ không đủ làm bảo đảm học) — chứng minh đầy đủ
**Giả thiết.** Tám thành phần sau, gồm thiết lập của Ví dụ 01.8 cùng (T1) và (O1).

- **Tập đầu vào.** $\mathcal X=[0,1]$ với σ-đại số Borel.
- **Phân bố dữ liệu.** $D$, phân bố của $(X,1)$ với $X\sim U[0,1]$, dùng cho cả hai phần.
- **Lớp giả thuyết.** $\mathcal H=\mathcal M_{\mathcal X}$.
- **Hàm lỗi.** $\ell_{0\text{-}1}$, thỏa (T2).
- **Tập huấn luyện.** $S\sim D^m$, theo (T1).
- **Thuật toán.** Thuật toán ERM chính xác theo (O1), thỏa điều kiện đo được của Định nghĩa 01.4: $\hat A$ bất kì trong Định nghĩa 01.28 ở phần (a), $A_{\mathrm{gn}}$ (Mệnh đề 01.15(a)) ở phần (b).
- **Tính khả diễn.** $(D,\mathcal M_{\mathcal X})$ khả diễn (Định nghĩa 01.16), có từ Mệnh đề 01.15(c); chỉ phần (b) dùng thành phần này.
- **Cận tổng quát hóa.** $\beta$, theo Định nghĩa 01.28.

**Bảo đảm.** Hai khẳng định sau.

- **(a)** Mọi cận tổng quát hóa cho mọi thuật toán ERM trên $\mathcal M_{\mathcal X}$ thỏa $\beta(m,\delta)\ge1$ với mọi $m$, $\delta$, nên với mỗi $\delta\in(0,1)$, $\beta(m,\delta)$ không tiến về $0$ khi $m\to\infty$.
- **(b)** Dưới phân bố khả diễn $D$ của Ví dụ 01.8, $\Pr_S\big[L_D(A_{\mathrm{gn}}(S))\le\epsilon\big]=0$ với mọi $\epsilon\in(0,1)$ và mọi $m$, nên $A_{\mathrm{gn}}$ không là thuật toán học PAC cho $\mathcal M_{\mathcal X}$, và theo Nhận xét 01.26 cũng không là thuật toán học PAC bất khả diễn.

Lớp $\mathcal M_{\mathcal X}$ với $\mathcal X=[0,1]$ không học được PAC (UML §5.1), nhưng khẳng định đó cần một lập luận cho mọi thuật toán, không suy ra từ hệ quả này.
:::

::: proof Chứng minh Hệ quả 01.29
**Lộ trình.** Áp dụng Mệnh đề 01.15 và đọc xác suất của một biến cố tất định.

**Bước 1 (phần a).** Theo Mệnh đề 01.15(a) và Phụ lục A(iii), $A_{\mathrm{gn}}$ là một thuật toán ERM đo được. Cặp $(A_{\mathrm{gn}},D)$ là phản ví dụ: bất đẳng thức của Định nghĩa 01.28 phải đúng với mọi thuật toán ERM và mọi phân bố, nên phải đúng với $\hat A=A_{\mathrm{gn}}$ và $D$. Theo Mệnh đề 01.15(a)(b), khoảng cách tổng quát hóa bằng $1-0=1$ trên mọi tập huấn luyện, nên biến cố trong Định nghĩa 01.28 là $\{1\le\beta(m,\delta)\}$, không phụ thuộc $S$, và
$$
\begin{aligned}
&\Pr_{S\sim D^m}\big[1\le\beta(m,\delta)\big]\\
&\quad=\mathbb 1\big[\beta(m,\delta)\ge1\big].
\end{aligned}
$$
Vì $1-\delta>0$, xác suất này ít nhất bằng $1-\delta$ chỉ khi $\beta(m,\delta)\ge1$.

**Bước 2 (phần b).** Theo Mệnh đề 01.15(c), $(D,\mathcal M_{\mathcal X})$ khả diễn với $h^\star=h_{\equiv1}$. Theo Mệnh đề 01.15(b), $L_D(A_{\mathrm{gn}}(S))=1>\epsilon$ với mọi $S$ và mọi $\epsilon<1$, nên xác suất thành công bằng $0<1-\delta$ với mọi $m$, và $m_{A_{\mathrm{gn}}}(\epsilon,\delta)=\infty$.

Hai giả thiết của Mệnh đề 01.15 được dùng: lớp chứa hàm phân lớp ghi nhớ qua phần (a), và $D_{\mathcal X}$ không có nguyên tử qua phần (b).

$\square$ Chỉ biết $L_S$ nhỏ thì chưa đủ để bảo đảm học: một bảo đảm học phải dùng cấu trúc của lớp giả thuyết hoặc tính chất của một thuật toán cụ thể.
:::

Ta bỏ giả thiết không có nguyên tử của Mệnh đề 01.15(b), giữ nguyên nhãn hằng và thuật toán ghi nhớ.

::: example Ví dụ 01.11 (Hàm phân lớp ghi nhớ khi phân bố có nguyên tử)
**Thiết lập.**

- **Tập đầu vào và phân bố dữ liệu.** $\mathcal X=\{1,\ldots,5\}$ và phân bố $D_1(x,y)=0{,}2\cdot\mathbb 1[y=1]$ của Nhận xét 01.21.
- **Lớp giả thuyết và hàm lỗi.** Lớp $\mathcal M_{\mathcal X}$ gồm cả $32$ hàm $\mathcal X\to\{0,1\}$, hàm lỗi 0–1.
- **Tập huấn luyện và thuật toán.** $S\sim D_1^m$ và $A_{\mathrm{gn}}$.

So với Ví dụ 01.8, tập đầu vào đổi từ $[0,1]$ sang $\{1,\ldots,5\}$ và $D_1$ đều trên năm điểm, nên mỗi điểm là một nguyên tử có xác suất $0{,}2$; nhãn vẫn hằng và thuật toán vẫn là $A_{\mathrm{gn}}$.

**Điểm sai của hàm học được.** Theo Bước 2 của chứng minh Mệnh đề 01.15, $A_{\mathrm{gn}}(S)$ là một nghiệm ERM. Mọi nhãn bằng $1$, nên theo Định nghĩa 01.14,
$$
\begin{aligned}
&A_{\mathrm{gn}}(S)(x)\\
&\quad=\mathbb 1\big[x\in\{X_1,\ldots,X_m\}\big].
\end{aligned}
$$
Do đó $A_{\mathrm{gn}}(S)$ sai đúng tại các điểm chưa xuất hiện trong $S$.

**Xác suất một điểm vắng mặt.** Mỗi quan sát khác một điểm $x$ cho trước với xác suất $0{,}8$, và các quan sát độc lập, nên mỗi điểm vắng mặt trong $S$ với xác suất $0{,}8^m$.

**Kì vọng của rủi ro.** Rủi ro bằng tổng khối lượng $0{,}2$ của các điểm vắng mặt,
$$
\begin{aligned}
&L_{D_1}(A_{\mathrm{gn}}(S))\\
&\quad=0{,}2\sum_{x=1}^5\\
&\qquad\mathbb 1\big[x\notin\{X_1,\ldots,X_m\}\big].
\end{aligned}
$$
Theo tính tuyến tính của kì vọng,
$$
\begin{aligned}
&\mathbb E_S\big[L_{D_1}(A_{\mathrm{gn}}(S))\big]\\
&\quad=5\cdot0{,}2\cdot0{,}8^m=0{,}8^m .
\end{aligned}
$$
Tại $m=10$, giá trị này bằng $0{,}8^{10}\approx0{,}107$, và nó tiến về $0$ khi $m\to\infty$.

**Kết luận.** Dưới $D_1$, toàn bộ khối lượng xác suất nằm trên năm nguyên tử, nên kì vọng của rủi ro bằng $0{,}8^m$ và tiến về $0$. Khẳng định $L_D(A_{\mathrm{gn}}(S))=1$ của Mệnh đề 01.15(b) vì vậy cần giả thiết không có nguyên tử.
:::

::: remark Nhận xét 01.30 (Phản ví dụ ghi nhớ và định lý không có bữa trưa miễn phí)
Định lý không có bữa trưa miễn phí (no-free-lunch theorem, UML §5.1) khẳng định rằng với mỗi thuật toán, tồn tại một phân bố làm thuật toán thất bại khi cỡ mẫu nhỏ so với $\lvert\mathcal X\rvert$, dù dưới phân bố đó nhãn là $f(X)$ với một hàm gán nhãn $f$. Mệnh đề 01.15 chỉ xét một thuật toán ERM và một phân bố. Dưới phân bố đó, hàm hằng $h_{\equiv1}$ cũng là nghiệm ERM với rủi ro $0$, nên Mệnh đề 01.15 không chứng minh định lý không có bữa trưa miễn phí.
:::

Vì nghiệm ERM $\hat h$ được chọn theo $S$ (Nhận xét 01.9), một bảo đảm cho ERM cần kiểm soát $L_S(h)-L_D(h)$ đồng thời cho mọi $h\in\mathcal H$.

## 9. Ý nghĩa, tác động và giới hạn

Hai loại phát biểu học PAC cho hai loại bảo đảm.

- "Lớp $\mathcal H$ học được PAC" là bảo đảm cho lớp: tồn tại một thuật toán học PAC cho $\mathcal H$.
- "$A$ là thuật toán học PAC cho $\mathcal H$" là bảo đảm cho một thuật toán cụ thể; chỉ phát biểu này cho biết nên chạy thuật toán nào.

Định nghĩa học PAC không bảo đảm gì về một dự đoán riêng lẻ và không so với rủi ro Bayes: dưới $D_\eta$, hiệu $\min_tL_{D_\eta}(h_t)-L^{\mathrm{Bayes}}_{D_\eta}=0{,}04$ không giảm khi $m$ tăng. Định nghĩa cũng không xét thời gian tính và không áp dụng khi các quan sát không độc lập cùng phân bố.

Từ các định nghĩa của bài, ta rút ra bốn quyết định thực hành.

- Hàm lỗi phải phản ánh chi phí của từng loại lỗi; dưới $\ell_c$, ngưỡng tối ưu trên $\eta(x)$ là $c_{FP}/(c_{FP}+c_{FN})$.
- Lớp $\mathcal H$ phải được cố định trước khi xem dữ liệu.
- Rủi ro của $\hat h$ phải được ước lượng trên một tập dữ liệu độc lập với tập huấn luyện (Nhận xét 01.9).
- Quy tắc chọn khi bằng nhau phải được ghi lại, vì trên $S_\eta$ nó làm rủi ro kì vọng dưới $D_\eta$ thay đổi từ $0{,}22$ đến $0{,}32$.

Với lớp hàm ngưỡng và $A_{\max}$, cỡ mẫu $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$ đủ cho mọi phân bố khả diễn; lập luận dùng bất đẳng thức $1-x\le e^{-x}$ và được trình bày chi tiết trong Bài tập 01.9. Khi $\epsilon=0{,}1$ và $\delta=0{,}05$,
$$
\begin{aligned}
\Big\lceil\frac{\ln(1/0{,}05)}{0{,}1}\Big\rceil
&=\lceil10\ln20\rceil\\
&=\lceil29{,}96\ldots\rceil=30,
\end{aligned}
$$
nên điều kiện là $m\ge30$. Cỡ $14$ của Ví dụ 01.9 chỉ đủ riêng cho $D_f$.

## 10. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 01](material-viewer.html?doc=materials/lec-01/exercises.md). Năm bài đầu là bài gốc, sáu bài sau chọn từ UML; mỗi dòng ghi mục tiêu học tập mà bài kiểm tra.

1. **Bài tập 01.1** (Thiết lập bài toán học cho lọc thư rác và dự báo nhiệt độ): mục tiêu 1.
2. **Bài tập 01.2** (Hai nghiệm ERM, quy tắc Bayes và rủi ro vượt mức): mục tiêu 2.
3. **Bài tập 01.3** (Tính không chệch và giả thuyết chọn theo tập huấn luyện): mục tiêu 3.
4. **Bài tập 01.4** (Hàm phân lớp ghi nhớ và hai rủi ro): mục tiêu 5.
5. **Bài tập 01.5** (Định nghĩa học PAC với đủ lượng từ): mục tiêu 4.
6. **Bài tập 01.6** (Hàm phân lớp ghi nhớ là một đa thức có ngưỡng; UML Bài tập 2.1): mục tiêu 5.
7. **Bài tập 01.7** (Tính đơn điệu của độ phức tạp mẫu; UML Bài tập 3.1): mục tiêu 4.
8. **Bài tập 01.8** (Lớp hàm chỉ báo của một điểm; UML Bài tập 3.2): mục tiêu 4.
9. **Bài tập 01.9** (Lớp hình tròn đồng tâm và lớp hàm ngưỡng; UML Bài tập 3.3): mục tiêu 4.
10. **Bài tập 01.10** (Học PAC bất khả diễn kéo theo học PAC khả diễn; UML Bài tập 3.6): mục tiêu 4.
11. **Bài tập 01.11** (Tính tối ưu của quy tắc Bayes và so sánh thuật toán; UML Bài tập 3.8, thử thách): mục tiêu 2.

## 11. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Trong $L_D(A(S))$, phân bố $D$ cố định. Đại lượng nào ngẫu nhiên, và ngẫu nhiên theo phân bố nào?

**Câu hỏi phụ.**

1. Trên tập huấn luyện $S_\eta$, nghiệm ERM trên lớp hàm ngưỡng có rủi ro kì vọng dưới $D_\eta$ bằng bao nhiêu?
2. Với $\delta=0{,}05$, có thể nói hàm phân lớp vừa học đúng với xác suất $95\%$ không?

::: solution Lời giải câu hỏi cuối buổi
**Câu hỏi chính.** Hàm học được $A(S)$ là ngẫu nhiên, vì nó là hàm của tập huấn luyện $S\sim D^m$. Do đó $L_D(A(S))$ là một biến ngẫu nhiên theo $D^m$. Khi thuật toán sinh thêm đại lượng ngẫu nhiên $\xi$, $L_D(A(S;\xi))$ ngẫu nhiên theo cả $S$ và $\xi$.

**Câu hỏi phụ (1).** Trên $S_\eta$, tập nghiệm ERM là $\{h_2,h_3,h_5\}$, nên kết quả tùy quy tắc chọn khi bằng nhau (Ví dụ 01.6):

- $0{,}32$ nếu chọn $h_2$ (như $A_{\min}$);
- $0{,}22$ nếu chọn $h_3$;
- $0{,}28$ nếu chọn $h_5$ (như $A_{\max}$).

**Câu hỏi phụ (2).** Không. Số $0{,}95$ là xác suất theo các lần lấy tập huấn luyện lặp lại: trong 100 lần huấn luyện, có khoảng 95 lần hàm học được có rủi ro kì vọng không quá $\epsilon$ (Nhận xét 01.19). Nó không phải xác suất một dự đoán cụ thể đúng.
:::

Hai hàm $h_3$ và $h_4$ của câu hỏi mở đầu chỉ khác nhau tại $x=3$, và $S_f$ không chứa $x=3$.

- Trên $S_f$, $A_{\min}$ chọn $h_3$ (rủi ro $0$), còn $A_{\max}$ chọn $h_4$ (rủi ro $0{,}2$).
- $S_f$ cũng có thể đến từ phân bố có hàm gán nhãn $h_4$, và mọi hàm phân lớp có rủi ro ít nhất $0{,}2$ dưới một trong hai phân bố. Do đó, trên $S_f$, không thuật toán nào trả về được một hàm có rủi ro $0$ dưới cả hai phân bố.
- Học PAC chỉ đòi xác suất gặp những tập huấn luyện như $S_f$ đủ nhỏ, với một ngưỡng cỡ mẫu chung cho mọi phân bố. Với $A_{\max}$ dưới $D_f$, xác suất đó là $0{,}8^m\le0{,}05$ khi $m\ge14$ (Ví dụ 01.9); với thuật toán ghi nhớ trên lớp của Ví dụ 01.8, không cỡ mẫu nào đủ.

Trong Ví dụ 01.9, ta tính được $\Pr[L_{D_f}(A_{\max}(S))>0]$ vì đã biết $D_f$. Khi $D$ chưa biết, chúng ta cần chặn $\Pr\big(\lvert L_S(h)-L_D(h)\rvert>\epsilon\big)$ cho từng $h$ cố định, với giả thiết các quan sát độc lập và hàm lỗi bị chặn. Bài 02 trả lời câu hỏi sau. Khi $\mathcal H$ hữu hạn và $D$ chưa biết, cần bao nhiêu quan sát để $\lvert L_S(h)-L_D(h)\rvert\le\epsilon$ với xác suất ít nhất $1-\delta$? Câu hỏi được đặt trước cho một giả thuyết cố định, rồi cho nghiệm ERM chọn từ $\lvert\mathcal H\rvert$ ứng viên. Công cụ là bất đẳng thức Hoeffding và bất đẳng thức hợp.

## 12. Tài liệu đọc

- **Trước buổi học:** UML §§2.1–2.2 (mô hình học, ERM, quá khớp).
- **Sau buổi học:** UML §2.3 (thiên kiến quy nạp; §2.3.1 là phần mở đầu của Bài 02), §§3.1–3.2 (học PAC, học PAC bất khả diễn, hàm lỗi tổng quát); các bài tập UML §2.4 và §3.5 đã chọn ở §10.
- **Mở rộng:** UML §5.1 (định lý không có bữa trưa miễn phí; Nhận xét 01.30).

**Quan hệ với giáo trình UML.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục. Các khác biệt so với UML:

- **Phân bố dữ liệu.** UML Chương 2 viết $L_{(D,f)}(h)$ cho nhãn tất định $Y=f(X)$; ở đây $D$ là phân bố liên hợp ngay từ đầu.
- **Mức tốt nhất trong lớp.** Ở đây dùng $\inf_{h\in\mathcal H}L_D(h)$; UML dùng $\min$.
- **ERM xấp xỉ.** Có ở đây (Định nghĩa 01.12), không có trong UML Chương 2–3.
- **Họ phân bố của học PAC bất khả diễn.** Ở đây là các phân bố có rủi ro hữu hạn; UML §3.2.2 lấy mọi phân bố.
- **Tính đo được.** Ở đây đòi tính đo được đồng thời theo tập huấn luyện và theo quan sát (Phụ lục A); UML chỉ đòi từng $\ell(h,\cdot)$ đo được.

## Phụ lục

### A. Tính đo được

Các định nghĩa học PAC chỉ có nghĩa khi các biến cố trong dấu $\Pr$ đo được. Các điều kiện dưới đây bảo đảm điều đó.

**(i) Rủi ro của một giả thuyết cố định.** Trong Định nghĩa 01.1, $\ell(h,\cdot)$ đo được, nên $\ell(h,Z)$ là biến ngẫu nhiên không âm và $L_D(h)=\int\ell(h,z)\,dD(z)$ xác định trong $[0,\infty]$. Không cần khả tích ở bước này; khả tích chỉ cần khi trừ hai rủi ro hoặc khi dùng Mệnh đề 01.7.

**(ii) Rủi ro của hàm học được.** Theo Định nghĩa 01.4, ánh xạ $(s,z)\mapsto\ell(A_m(s),z)$ đo được trên $\mathcal Z^m\times\mathcal Z$. Ánh xạ này không âm, nên theo định lý Tonelli hàm
$$
\begin{aligned}
s\mapsto{}&\int_{\mathcal Z}\ell\big(A_m(s),z\big)\,dD(z)\\
&=L_D\big(A_m(s)\big)
\end{aligned}
$$
đo được trên $\mathcal Z^m$. Do đó $L_D(A(S))$ là một biến ngẫu nhiên với giá trị trong $[0,\infty]$, và các biến cố trong Định nghĩa 01.18 và 01.25 có xác suất. UML chỉ đòi từng $\ell(h,\cdot)$ đo được. Điều kiện đó không đủ: khi $h=A(S)$ thay đổi theo tập huấn luyện, cần tính đo được đồng thời theo tập huấn luyện và theo quan sát.

**(iii) Thuật toán ghi nhớ.** Với $s=((x_1,y_1),\ldots,(x_m,y_m))$ và $x\in[0,1]$, tập $G_i=\{(s,x):\ x=x_i\}$ là ảnh ngược của đường chéo $\{(u,u)\}$ qua ánh xạ liên tục $(s,x)\mapsto(x_i,x)$, nên đóng. Các không gian $\mathcal Z^m\times\mathcal Z$ ở đây là không gian mêtric khả li, nên σ-đại số Borel của chúng trùng với σ-đại số tích mà Định nghĩa 01.4 dùng; tập đóng $G_i$ vì vậy đo được theo σ-đại số tích. Do đó các hàm
$$
c(s,x)=\sum_{i=1}^m\mathbb 1[(s,x)\in G_i],
$$
$$
v(s,x)=\sum_{i=1}^m(2y_i-1)\,\mathbb 1[(s,x)\in G_i]
$$
(số quan sát tại $x$, và hiệu giữa số nhãn 1 và số nhãn 0 tại $x$) là tổng hữu hạn của các hàm đo được, nên đo được. Theo Định nghĩa 01.14,
$$
\begin{aligned}
A_{\mathrm{gn}}(s)(x)&=\mathbb 1\big[c(s,x)\ge1\big]\\
&\quad\cdot\mathbb 1\big[v(s,x)\ge0\big],
\end{aligned}
$$
nên $(s,x)\mapsto A_{\mathrm{gn}}(s)(x)$ đo được, và $(s,(x,y))\mapsto\mathbb 1[A_{\mathrm{gn}}(s)(x)\ne y]$ đo được. Thuật toán $A_{\mathrm{gn}}$ vì vậy thỏa điều kiện của Định nghĩa 01.4.

**(iv) Tập đầu vào hữu hạn.** Khi $\mathcal X$ hữu hạn, $\mathcal Y=\{0,1\}$ và mọi tập con đều đo được, mọi hàm trên $\mathcal Z^m\times\mathcal Z$ đo được, và lớp $\mathcal H$ hữu hạn. Khi đó $\ell(A_m(s),z)=\sum_{h\in\mathcal H}\mathbb 1[A_m(s)=h]\,\ell(h,z)$, nên điều kiện của Định nghĩa 01.4 tự thỏa. Đây là trường hợp của ví dụ sàng lọc.

**(v) Lớp vô hạn.** Với một lớp vô hạn tổng quát, các đại lượng dạng $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$, cần cho hội tụ đều (uniform convergence), có thể không đo được.

### B. Quy tắc Bayes

Chứng minh Mệnh đề 01.23 dùng kì vọng có điều kiện và tính chất $\mathbb E[\mathbb E[U\mid X]]=\mathbb E[U]$; các tính chất khác của $h_{\mathrm{Bayes}}$ suy ra từ cùng phép tính.

::: proof Chứng minh Mệnh đề 01.23
**Lộ trình.** Tính rủi ro có điều kiện tại $X=x$, tối thiểu hóa nó tại từng điểm bằng cách so sánh hai lựa chọn $0$ và $1$, rồi lấy kì vọng theo $D_{\mathcal X}$ bằng tính chất $\mathbb E[\mathbb E[U\mid X]]=\mathbb E[U]$.

**Bước 1 (rủi ro có điều kiện).** Cho $g\in\mathcal M_{\mathcal X}$. Lỗi 0–1 của $g$ viết được thành
$$
\begin{aligned}
&\mathbb 1[g(X)\ne Y]\\
&\quad=\mathbb 1[Y=1]\,\mathbb 1[g(X)=0]\\
&\qquad+\mathbb 1[Y=0]\,\mathbb 1[g(X)=1].
\end{aligned}
$$
Vì $g(X)$ là hàm đo được của $X$, các thừa số chứa $g(X)$ được đưa ra ngoài kì vọng có điều kiện theo $X$, nên hầu chắc chắn
$$
\begin{aligned}
&\mathbb E\big[\mathbb 1[g(X)\ne Y]\mid X\big]\\
&=\mathbb 1[g(X)=0]\\
&\qquad\cdot\Pr(Y=1\mid X)\\
&\quad+\mathbb 1[g(X)=1]\\
&\qquad\cdot\Pr(Y=0\mid X)\\
&=\eta(X)\,\mathbb 1[g(X)=0]\\
&\quad+\big(1-\eta(X)\big)\,\mathbb 1[g(X)=1].
\end{aligned}
$$
Định nghĩa của $\eta$ và tính đo được của $g$ được dùng ở đây.

**Bước 2 (tối thiểu hóa từng điểm).** Tại mỗi $x$, vế phải bằng $\eta(x)$ nếu $g(x)=0$ và bằng $1-\eta(x)$ nếu $g(x)=1$, nên nó không nhỏ hơn $\min\{\eta(x),1-\eta(x)\}$. Dấu bằng xảy ra khi $g(x)=1$ đúng lúc $\eta(x)\ge\tfrac12$ (khi $\eta(x)=\tfrac12$ hai lựa chọn bằng nhau), chẳng hạn khi $g=h_{\mathrm{Bayes}}$. Tập $\{x:\eta(x)\ge\tfrac12\}$ đo được vì $\eta$ đo được, nên $h_{\mathrm{Bayes}}\in\mathcal M_{\mathcal X}$.

**Bước 3 (lấy kì vọng).** Theo tính chất $\mathbb E[\mathbb E[U\mid X]]=\mathbb E[U]$ với $U=\mathbb 1[g(X)\ne Y]$ và Bước 2,
$$
\begin{aligned}
&L_D(g)\\
&\quad=\mathbb E\Big[\mathbb E\big[\mathbb 1[g(X)\ne Y]\mid X\big]\Big]\\
&\quad\ge\mathbb E\min\{\eta(X),1-\eta(X)\}\\
&\quad=L_D(h_{\mathrm{Bayes}}).
\end{aligned}
$$
Lấy cận dưới đúng theo $g$ cho đẳng thức của phần (a).

**Bước 4 (hàm lỗi có trọng số).** Với $\ell_c$, cùng lập luận áp dụng cho rủi ro có điều kiện
$$
\begin{aligned}
&c_{FN}\,\eta(X)\,\mathbb 1[g(X)=0]\\
&\quad+c_{FP}\,(1-\eta(X))\\
&\qquad\cdot\mathbb 1[g(X)=1].
\end{aligned}
$$
Dự đoán $1$ tại $x$ không tệ hơn dự đoán $0$ khi và chỉ khi
$$
\begin{aligned}
&c_{FP}\big(1-\eta(x)\big)\le c_{FN}\,\eta(x)\\
&\quad\iff\eta(x)\ge\frac{c_{FP}}{c_{FP}+c_{FN}},
\end{aligned}
$$
trong đó phép tương đương dùng $c_{FP}+c_{FN}>0$.

$\square$ Rủi ro Bayes là mức thấp nhất mà mọi hàm phân lớp đạt được, và nó đạt được bằng một quy tắc ngưỡng trên $\eta(x)$; ngưỡng phụ thuộc hàm lỗi.
:::

**Sự tồn tại của $\eta$.** Kì vọng có điều kiện $\mathbb E[\mathbb 1[Y=1]\mid X]$ là một biến ngẫu nhiên đo được theo σ-đại số sinh bởi $X$. Theo bổ đề Doob–Dynkin, tồn tại hàm đo được $\eta:\mathcal X\to\mathbb R$ với $\mathbb E[\mathbb 1[Y=1]\mid X]=\eta(X)$ hầu chắc chắn. Vì kì vọng có điều kiện này nằm trong $[0,1]$ hầu chắc chắn, có thể thay $\eta$ bằng $\min\{\max\{\eta,0\},1\}$ mà không đổi đẳng thức, nên có thể giả sử $\eta$ nhận giá trị trong $[0,1]$. Hai hàm $\eta$ như vậy bằng nhau trừ trên một tập có xác suất $0$ dưới $D_{\mathcal X}$.

**Tính không duy nhất.** Bước 2 cho thấy tại mỗi $x$, rủi ro có điều kiện của $g$ vượt rủi ro có điều kiện của $h_{\mathrm{Bayes}}$ đúng $\lvert2\eta(x)-1\rvert$ khi $g(x)\ne h_{\mathrm{Bayes}}(x)$, và bằng nhau khi $g(x)=h_{\mathrm{Bayes}}(x)$. Lấy kì vọng, ta được với mọi $g\in\mathcal M_{\mathcal X}$
$$
\begin{aligned}
&L_D(g)-L_D(h_{\mathrm{Bayes}})\\
&\quad=\mathbb E\Big[\lvert2\eta(X)-1\rvert\\
&\qquad\cdot\mathbb 1\big[g(X)\ne h_{\mathrm{Bayes}}(X)\big]\Big].
\end{aligned}
$$
Do đó $g$ đạt rủi ro Bayes khi và chỉ khi $g(X)=h_{\mathrm{Bayes}}(X)$ hầu chắc chắn trên biến cố $\{\eta(X)\ne\tfrac12\}$; trên tập $\{\eta=\tfrac12\}$ và trên mọi tập có xác suất $0$, $g$ có thể nhận giá trị tùy ý. Với $\ell_c$, trọng số là $\lvert c_{FN}\,\eta(X)-c_{FP}(1-\eta(X))\rvert$ và tập tương ứng là $\{\eta=c_{FP}/(c_{FP}+c_{FN})\}$. Dưới $D_\eta$, $h_3$ khác $h_{\mathrm{Bayes}}$ chỉ tại $x=4$, nên $L_{D_\eta}(h_3)-L^{\mathrm{Bayes}}_{D_\eta}=0{,}2\cdot\lvert2\cdot0{,}4-1\rvert=0{,}04$, khớp Ví dụ 01.10.

**Rủi ro Bayes.** Theo Mệnh đề 01.23(a), rủi ro Bayes bằng $0$ khi và chỉ khi $\eta(X)\in\{0,1\}$ hầu chắc chắn, tức nhãn là hàm tất định của đầu vào. Nếu $\eta(X)\in(0,1)$ trên một biến cố có xác suất dương, rủi ro Bayes dương và không cặp $(D,\mathcal H)$ nào khả diễn, như với $D_\eta$.

**Trường hợp $\mathcal X$ rời rạc.** Khi $\mathcal X$ hữu hạn hoặc đếm được, $\eta(x)=\Pr(Y=1,X=x)/\Pr(X=x)$ tại mọi $x$ với $\Pr(X=x)>0$, và $\eta$ tùy ý tại các điểm còn lại. Các kì vọng trong Mệnh đề 01.23 trở thành tổng, chẳng hạn $L_D^{\mathrm{Bayes}}=\sum_xD_{\mathcal X}(x)\min\{\eta(x),1-\eta(x)\}$; Ví dụ 01.10 dùng đúng công thức này.

### C. Tính toán chi tiết cho ví dụ xuyên suốt

**C.1 Rủi ro kì vọng dưới $D_\eta$.** Với $D_{\mathcal X}(x)=0{,}2$,
$$
L_{D_\eta}(h_t)=0{,}2\big[a(t)+b(t)\big],
$$
$$
L^c_{D_\eta}(h_t)=0{,}2\big[c_{FN}\,a(t)+c_{FP}\,b(t)\big],
$$
trong đó $a(t)=\sum_{x<t}\eta(x)$ là khối lượng nhãn 1 bị bỏ sót và $b(t)=\sum_{x\ge t}(1-\eta(x))$ là khối lượng nhãn 0 bị báo nhầm. Với $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$ và $(c_{FP},c_{FN})=(1,4)$:

| $t$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ |
|---|---|---|---|---|---|---|
| $a(t)$ | $0$ | $0$ | $0{,}25$ | $1$ | $1{,}4$ | $2{,}4$ |
| $b(t)$ | $2{,}6$ | $1{,}6$ | $0{,}85$ | $0{,}6$ | $0$ | $0$ |
| $L_{D_\eta}(h_t)=0{,}2\,(a+b)$ | $0{,}52$ | $0{,}32$ | $0{,}22$ | $0{,}32$ | $0{,}28$ | $0{,}48$ |
| $L^c_{D_\eta}(h_t)=0{,}2\,(4a+b)$ | $0{,}52$ | $0{,}32$ | $0{,}37$ | $0{,}92$ | $1{,}12$ | $1{,}92$ |

Kiểm tra lại: $a(t)+b(t)$ tại $t=1$ bằng $\sum_x(1-\eta(x))=5-2{,}4=2{,}6$, và tại $t=6$ bằng $\sum_x\eta(x)=2{,}4$.

**C.2 Kì vọng theo $S$ của rủi ro kì vọng của $A_{\max}$ dưới $D_f$.** Đặt $N=\hat t-3\in\{0,1,2,3\}$, nên $L_{D_f}(A_{\max}(S))=0{,}2N$.

Vì $N=\sum_{k=1}^3\mathbb 1[N\ge k]$ (mỗi $k\le N$ đóng góp một đơn vị), tính tuyến tính của kì vọng cho
$$
\mathbb EN=\sum_{k=1}^3\Pr(N\ge k).
$$

Biến cố $N\ge k$ xảy ra khi và chỉ khi không quan sát nào của $S$ nằm trong $\{3,\ldots,2+k\}$, một tập có khối lượng $0{,}2k$, nên $\Pr(N\ge k)=(1-0{,}2k)^m$ với $k=1,2,3$. Do đó
$$
\begin{aligned}
&\mathbb E_S\big[L_{D_f}(A_{\max}(S))\big]\\
&\quad=0{,}2\,\big(0{,}8^m+0{,}6^m+0{,}4^m\big).
\end{aligned}
$$
Tại $m=10$, ba lũy thừa là
$$
\begin{aligned}
0{,}8^{10}&\approx0{,}10737,\\
0{,}6^{10}&\approx0{,}00605,\\
0{,}4^{10}&\approx0{,}00010,
\end{aligned}
$$
với tổng $\approx0{,}11353$; nhân $0{,}2$ được $\approx0{,}0227$.

Cùng lập luận cho hai xác suất của Ví dụ 01.9:
$$
\begin{aligned}
&\Pr\big[L_{D_f}(A_{\max}(S))>0\big]\\
&\quad=\Pr(N\ge1)=0{,}8^m,\\
&\Pr\big[L_{D_f}(A_{\max}(S))>0{,}25\big]\\
&\quad=\Pr(N\ge2)=0{,}6^m.
\end{aligned}
$$

Rủi ro thực nghiệm $L_S(A_{\max}(S))=0$ với mọi tập huấn luyện lấy mẫu từ $D_f$, vì mọi quan sát âm nằm ở $\{1,2\}$, dưới mọi quan sát dương.
