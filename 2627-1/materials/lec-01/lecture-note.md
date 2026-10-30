# Bài 01 — Mô hình học: rủi ro, tối thiểu hóa rủi ro thực nghiệm và học PAC

Một thuật toán học (learning algorithm) nhận một mẫu hữu hạn các quan sát (example) và trả về một hàm dự đoán (predictor), tức một quy tắc gán nhãn cho mỗi đầu vào. Câu hỏi trung tâm của bài là: học nghĩa là gì? Cụ thể, trước khi biết mẫu nào sẽ xuất hiện, khi nào ta nói một hàm dự đoán chọn ra từ một mẫu ngẫu nhiên đã học được? Để trả lời, chúng ta cần ba đối tượng. Thứ nhất là cặp rủi ro. Rủi ro kì vọng (population risk) là mức sai trung bình của hàm dự đoán trên một quan sát mới rút từ phân bố dữ liệu (data-generating distribution). Rủi ro thực nghiệm (empirical risk) là mức sai trung bình trên các quan sát của mẫu. Thứ hai là quy tắc tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM): chọn hàm dự đoán sai ít nhất trên mẫu. Thứ ba là định nghĩa học xấp xỉ với xác suất cao (probably approximately correct, PAC): với xác suất cao theo mẫu, hàm học được có rủi ro kì vọng gần mức tốt nhất.

## Câu hỏi mở đầu

Xét một chỉ số đo có năm mức $1,2,3,4,5$. Giả sử một người có bệnh khi và chỉ khi chỉ số của người đó từ mức 3 trở lên, và mỗi mức chiếm $20\%$ dân số; các số này chỉ để minh họa. Một mẫu huấn luyện (training sample) gồm bốn người: hai người ở mức 1 và 2 không có bệnh, hai người ở mức 4 và 5 có bệnh. Hàm phân lớp (classifier) thứ nhất báo dương tính khi chỉ số từ 3 trở lên; hàm thứ hai báo dương tính khi chỉ số từ 4 trở lên.

**Câu hỏi.** Hai hàm phân lớp cùng khớp mọi quan sát huấn luyện. Vì sao có thể chỉ một trong hai dự đoán đúng các quan sát mới?

Hàm thứ nhất phân lớp đúng mọi người; hàm thứ hai sai với những người ở mức 3, tức với xác suất $0{,}2$.

Hai hàm có tốt như nhau vì đều phân lớp hoàn hảo trên mẫu huấn luyện không? Không: mẫu không chứa người nào ở mức 3, nơi duy nhất hai hàm khác nhau. Trường hợp cực đoan là một hàm chỉ lặp lại nhãn của các quan sát đã thấy và báo âm tính ở mọi điểm khác: nó khớp mẫu nhưng có thể sai trên mọi quan sát mới.

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Phát biểu đầy đủ một bài toán học thống kê: tập đầu vào, tập nhãn, phân bố dữ liệu, mẫu, lớp giả thuyết, hàm lỗi, thuật toán học, đối tượng so sánh. Chỉ ra đại lượng nào cố định, đại lượng nào ngẫu nhiên và ngẫu nhiên theo phân bố nào.
2. Tính rủi ro kì vọng, rủi ro thực nghiệm, tập nghiệm ERM, rủi ro Bayes (Bayes risk) và rủi ro vượt mức (excess risk) trong một bài toán hữu hạn; xác định ngưỡng tối ưu khi hàm lỗi (loss function) có chi phí bất đối xứng.
3. Chứng minh rủi ro thực nghiệm của một giả thuyết cố định là ước lượng không chệch (unbiased estimator) của rủi ro kì vọng, và chỉ ra bước hỏng khi giả thuyết được chọn theo mẫu.
4. Viết định nghĩa học PAC trong trường hợp khả thực (realizable) và bất khả tri (agnostic) với đúng thứ tự lượng từ; phân biệt tham số độ chính xác với tham số độ tin cậy, và độ phức tạp mẫu (sample complexity) của một thuật toán với độ phức tạp mẫu của một lớp.
5. Dựng phản ví dụ thuật toán ghi nhớ, chứng minh hàm phân lớp ghi nhớ có rủi ro thực nghiệm bằng 0 và rủi ro kì vọng bằng 1, và giải thích vì sao cần thiên kiến quy nạp (inductive bias) hoặc kiểm soát thuật toán.

## Kiến thức tiên quyết

- Kì vọng và tính tuyến tính của kì vọng; tính tuyến tính đúng cho mọi tổng hữu hạn biến ngẫu nhiên khả tích, không cần độc lập.
- Xác suất có điều kiện; kì vọng có điều kiện và tính chất tháp (tower property) $\mathbb E[\mathbb E[U\mid X]]=\mathbb E U$ (chỉ dùng trong chứng minh ở Phụ lục B).
- Hàm, tập hợp, hàm chỉ thị $\mathbb 1[\cdot]$; phân bố đều $U[0,1]$ trên $[0,1]$.
- Bất đẳng thức $1-x\le e^{-x}$ với mọi $x\in\mathbb R$ (chỉ dùng trong bài tập).

Chưa cần bất đẳng thức tập trung (concentration inequality).

Một khẳng định đúng *hầu chắc chắn* (almost surely) nếu nó đúng ngoài một biến cố có xác suất $0$. Một điểm có xác suất dương là một *nguyên tử* (atom) của phân bố; phân bố *không có nguyên tử* (atomless) nếu mọi điểm có xác suất $0$, như $U[0,1]$.

**Câu hỏi ôn nhanh.**

1. Cho $X\sim U[0,1]$. Tính $\Pr\big(X\in\{0{,}1;\ 0{,}5;\ 0{,}9\}\big)$.
2. Cho biến ngẫu nhiên $Z_1$ với $\mathbb E Z_1=\mu$ và đặt $Z_2=Z_1$. Tính $\mathbb E\big[(Z_1+Z_2)/2\big]$.
3. Rút $m$ lần độc lập, mỗi lần đều trên $\{1,2,3,4,5\}$. Tính xác suất không lần nào ra số 3.

::: solution Lời giải câu hỏi ôn nhanh
1. Bằng $0$: xác suất của hợp ba điểm không vượt quá tổng ba xác suất, mỗi xác suất bằng $0$.
2. Bằng $\mu$, theo tính tuyến tính của kì vọng, dù $Z_1$ và $Z_2$ hoàn toàn phụ thuộc nhau.
3. Bằng $0{,}8^m$: mỗi lần rút tránh số 3 với xác suất $0{,}8$, và các lần rút độc lập.
:::

## 1. Thiết lập bài toán

Trong học phần này, trước khi phát biểu bất kì cận nào, chúng ta nêu rõ tám thành phần sau.

1. **Tập đầu vào** (input space) $\mathcal X$ và **tập nhãn** (label set) $\mathcal Y$. Một quan sát là một cặp $z=(x,y)$ thuộc tập quan sát $\mathcal Z=\mathcal X\times\mathcal Y$. Trong phân lớp nhị phân (binary classification), $\mathcal Y=\{0,1\}$; trong hồi quy (regression), $\mathcal Y=\mathbb R$.
2. **Phân bố dữ liệu** $D$ trên $\mathcal Z$, tức phân bố của cặp ngẫu nhiên $Z=(X,Y)$. Vì $D$ là phân bố đồng thời, cùng một đầu vào $x$ có thể đi với cả hai nhãn; nhãn tất định $Y=f(X)$, với *hàm gán nhãn* (labeling function) $f:\mathcal X\to\mathcal Y$, là một trường hợp riêng.
3. **Mẫu huấn luyện** $S=(Z_1,\ldots,Z_m)\sim D^m$, gồm $m$ quan sát độc lập cùng phân bố (independent and identically distributed, i.i.d.) theo $D$. Mẫu là một dãy, nên một quan sát có thể lặp lại. Số $m$ là cỡ mẫu (sample size).
4. **Lớp giả thuyết** (hypothesis class) $\mathcal H$, một tập các hàm $h:\mathcal X\to\mathcal Y$, được chọn trước khi lấy mẫu. Mỗi $h\in\mathcal H$ là một giả thuyết (hypothesis), tức một hàm dự đoán; trong phân lớp ta gọi $h$ là hàm phân lớp.
5. **Hàm lỗi** (loss function) $\ell(h,z)\ge0$, đo mức sai của $h$ trên quan sát $z$.
6. **Thuật toán học** $A$, nhận mẫu $S$ và trả về hàm dự đoán $A(S)$. Mọi thuật toán học trong bài là tất định: cùng một mẫu cho cùng một hàm dự đoán.
7. **Mục tiêu và đối tượng so sánh** (comparator). Với mỗi hàm dự đoán $h$, *rủi ro kì vọng* $L_D(h)$ là kì vọng của $\ell(h,Z)$ theo một quan sát mới $Z\sim D$, độc lập với $S$. Mục tiêu là rủi ro kì vọng $L_D(A(S))$ nhỏ. Đối tượng so sánh chính là $\inf_{h\in\mathcal H}L_D(h)$, mức tốt nhất trong lớp. Đối tượng so sánh thứ hai là *rủi ro Bayes* (Bayes risk), mức thấp nhất của rủi ro kì vọng trên mọi hàm phân lớp.
8. **Tài nguyên.** Tài nguyên được xét là cỡ mẫu $m$; thời gian tính chưa được xét.

Thuật toán học chỉ thấy mẫu $S$, không thấy $D$, xác suất có điều kiện $\eta(x)=\Pr(Y=1\mid X=x)$, $f$ hay $L_D$. Một quy tắc cần biết $D$ để chạy vì vậy không phải là thuật toán học.

Bảng dưới phân loại các đại lượng của bài theo nguồn ngẫu nhiên. Vì thuật toán tất định, nguồn ngẫu nhiên duy nhất là mẫu.

| Loại | Đại lượng |
|---|---|
| Cố định (không ngẫu nhiên) | $D$, $\mathcal H$, $\ell$, thuật toán $A$ như một quy tắc, mỗi $h\in\mathcal H$ cho trước, $L_D(h)$ với $h$ cho trước, $\inf_{h\in\mathcal H}L_D(h)$ |
| Ngẫu nhiên theo $S\sim D^m$ | $S$, $A(S)$, $L_D(A(S))$ |

## 2. Kí hiệu và giả thiết

Kí hiệu chung theo bảng kí hiệu của học phần và §1. Bảng dưới gồm các kí hiệu riêng của bài dùng ngay từ ví dụ ở §3; mỗi kí hiệu khác được đặt tên tại định nghĩa của nó.

| Kí hiệu | Ý nghĩa |
|---|---|
| $D_{\mathcal X}$, $\eta(x)=\Pr(Y=1\mid X=x)\in[0,1]$ | phân bố biên (marginal distribution) của $X$, xác suất có điều kiện của nhãn 1 |

**Đọc lần đầu.** Mỗi tập $\mathcal X$, $\mathcal Y$, $\mathcal Z$ trong bài đi kèm một σ-đại số (σ-algebra), họ các tập con được gán xác suất. Một hàm là đo được (measurable) khi ảnh ngược của mỗi tập trong σ-đại số đích thuộc σ-đại số nguồn. Khi $\mathcal X$, $\mathcal Y$ hữu hạn và mọi tập con được coi là đo được, mọi điều kiện đo được trong bài tự thỏa và có thể coi là điều kiện kỹ thuật.

Hai giả thiết thống kê dưới đây được dẫn bằng nhãn trong dòng **Giả thiết.** của các kết quả.

- **(T1) Lấy mẫu.** $Z_1,\ldots,Z_m$ độc lập cùng phân bố theo $D$. Một số kết quả chỉ cần dạng yếu: mỗi $Z_i$ có phân bố $D$, không cần độc lập. Dòng **Giả thiết.** của các kết quả đó ghi rõ điều này.
- **(T2) Hàm lỗi.** $\ell\ge0$ và $\ell(h,\cdot)$ đo được với mọi $h\in\mathcal H$; khi hàm lỗi không bị chặn, cần thêm $L_D(h)<\infty$.

Các giả thiết còn lại được nêu ở chỗ chúng được dùng lần đầu. Tính đo được của thuật toán học nằm ở §4. Giả thiết tối ưu nằm ở §5: thuật toán giải đúng hay chỉ giải gần đúng bài toán chọn giả thuyết của nó. Giả thiết lớp chứa một giả thuyết có rủi ro kì vọng bằng $0$ nằm ở §6. Không kết quả nào trong bài dùng giả thiết lồi, trơn hay Lipschitz.

## 3. Ví dụ xuyên suốt

Ví dụ sau đủ nhỏ để tính bằng tay. Các khái niệm từ §4 đến §8 được tính trên ví dụ này và trên ứng dụng sàng lọc đặt sau nó.

::: example Ví dụ 01.1 (Sàng lọc theo ngưỡng trên năm mức đo)
Tập đầu vào $\mathcal X=\{1,2,3,4,5\}$ là năm mức của một chỉ số đo; tập nhãn $\mathcal Y=\{0,1\}$, với $Y=1$ là có bệnh. Phân bố biên $D_{\mathcal X}$ đều: mỗi mức có xác suất $0{,}2$. Lớp giả thuyết là các hàm ngưỡng
$$
\begin{aligned}
h_t(x)&=\mathbb 1[x\ge t],\\
\mathcal H&=\{h_t:\ t\in\{1,\ldots,6\}\},
\end{aligned}
$$
trong đó $h_1\equiv1$ báo dương tính với mọi người và $h_6\equiv0$ không báo ai. Hàm lỗi là hàm lỗi 0–1 (0–1 loss) $\ell_{0\text{-}1}(h,(x,y))=\mathbb 1[h(x)\ne y]$, đếm một lỗi mỗi khi dự đoán sai. Phân bố là giá trị giả định để minh họa, không phải số liệu lâm sàng.

Hai phiên bản của ví dụ khác nhau ở phân bố của nhãn. Phân bố $D_\eta$ có nhiễu, cho bởi xác suất có điều kiện $\eta(x)$; phân bố $D_f$ có nhãn tất định $Y=f(X)$, cho bởi hàm gán nhãn $f$.

| $x$ | $1$ | $2$ | $3$ | $4$ | $5$ |
|---|---|---|---|---|---|
| $D_{\mathcal X}(x)$ | $0{,}2$ | $0{,}2$ | $0{,}2$ | $0{,}2$ | $0{,}2$ |
| $\eta(x)$ dưới $D_\eta$ | $0$ | $\tfrac14$ | $\tfrac34$ | $\tfrac25$ | $1$ |
| $f(x)$ dưới $D_f$ | $0$ | $0$ | $1$ | $1$ | $1$ |

*Bản có nhiễu*, phân bố $D_\eta$: $\Pr(Y=1\mid X=x)=\eta(x)$. Mẫu cụ thể, cỡ $m=6$:
$$
\begin{aligned}
S_\eta=\big(&(1,0),(2,0),(2,1),\\
&(3,1),(4,0),(5,1)\big).
\end{aligned}
$$

*Bản nhãn tất định*, phân bố $D_f$: nhãn tất định $Y=f(X)$ với $f=h_3$, tức có bệnh khi và chỉ khi $x\ge3$. Mẫu của câu hỏi mở đầu, cỡ $m=4$:
$$
\begin{aligned}
S_f=\big(&(1,0),(2,0),\\
&(4,1),(5,1)\big).
\end{aligned}
$$
:::

::: application Sàng lọc y tế với chi phí bất đối xứng
Trong một chương trình sàng lọc (screening), đầu vào $x\in\mathcal X\subseteq\mathbb R^p$ là véc-tơ các chỉ số đo của một người, nhãn $y\in\{0,1\}$ là tình trạng bệnh. Nhãn có nhiễu: hai người có cùng chỉ số đo có thể ở hai tình trạng khác nhau, như tại mức $x=2$ của $D_\eta$, nơi $\eta(2)=\tfrac14$.

Âm tính giả (false negative) bỏ sót người bệnh; dương tính giả (false positive) đưa người khỏe đi xét nghiệm thêm. Gán cho hai loại lỗi này các chi phí $c_{FN}>0$ và $c_{FP}>0$, ta được hàm lỗi có trọng số
$$
\begin{aligned}
&\ell_c\big(h,(x,y)\big)\\
&\quad=c_{FN}\,\mathbb 1[y=1,\ h(x)=0]\\
&\qquad+c_{FP}\,\mathbb 1[y=0,\ h(x)=1],
\end{aligned}
$$
nhận giá trị trong $\{0,c_{FP},c_{FN}\}$; khi $c_{FP}=c_{FN}=1$, $\ell_c$ trở thành hàm lỗi 0–1. Hàm lỗi này là hàm lỗi có trọng số (cost-weighted loss). Trong ví dụ sàng lọc ta lấy $(c_{FP},c_{FN})=(1,4)$: bỏ sót một người bệnh đắt gấp bốn lần đưa một người khỏe đi xét nghiệm thêm. Chi phí này cũng là giá trị giả định. Câu hỏi thực hành: nên đặt ngưỡng báo dương tính ở đâu khi hai loại lỗi có chi phí khác nhau?
:::

Để trả lời câu hỏi về ngưỡng, chúng ta cần rủi ro kì vọng dưới $\ell_c$ và quy tắc Bayes; rủi ro kì vọng được định nghĩa chính xác ở §4, quy tắc Bayes ở §7.

## 4. Rủi ro kì vọng và bài toán học thống kê

Chất lượng của một hàm dự đoán $h$ phải đo trên quan sát mới rút từ $D$, không trên mẫu đã dùng để chọn $h$. Rủi ro kì vọng của §1 đo đúng đại lượng đó; để nó có nghĩa, hàm lỗi phải đo được.

::: definition Định nghĩa 01.1 (Hàm lỗi và rủi ro kì vọng)
Cho tập quan sát $\mathcal Z$ với một σ-đại số, một phân bố $D$ trên $\mathcal Z$ và một lớp giả thuyết $\mathcal H$. Một *hàm lỗi* là một ánh xạ $\ell:\mathcal H\times\mathcal Z\to[0,\infty)$ sao cho $\ell(h,\cdot)$ đo được với mọi $h\in\mathcal H$. *Rủi ro kì vọng* của $h\in\mathcal H$ là
$$
L_D(h)=\mathbb E_{Z\sim D}\,\ell(h,Z),
$$
một số trong $[0,\infty]$.
:::

Với $h$ cho trước, $L_D(h)$ là một số: không ngẫu nhiên, nhưng chưa biết. Hàm lỗi 0–1 cho $L_D(h)=\Pr(h(X)\ne Y)$, gọi là *xác suất lỗi* của $h$; hàm lỗi có trọng số $\ell_c$ cho rủi ro kí hiệu $L_D^c(h)$; hàm lỗi bình phương (squared loss) $\ell(h,(x,y))=(h(x)-y)^2$ dùng khi $\mathcal Y=\mathbb R$.

Một số chỉ số đánh giá không viết được dưới dạng rủi ro. Với $h$ và $\ell$ cố định, ánh xạ $D\mapsto L_D(h)$ là afin theo phép trộn phân bố. Giá trị dự đoán dương (precision) $\Pr(Y=1\mid h(X)=1)$ là tỉ số của hai kì vọng và nói chung không afin (Phụ lục C.4), nên nó không có dạng $\mathbb E\,\ell(h,Z)$ với một $\ell$ không phụ thuộc $D$.

::: example Ví dụ 01.2 (Rủi ro kì vọng của các hàm ngưỡng dưới hai hàm lỗi)
Xét bản có nhiễu của Ví dụ 01.1: phân bố $D_\eta$, lớp sáu hàm ngưỡng $h_t$, $(c_{FP},c_{FN})=(1,4)$; không có mẫu, mọi đại lượng đều cố định. Hàm $h_t$ sai tại mức $x<t$ khi $Y=1$ và tại mức $x\ge t$ khi $Y=0$, nên
$$
\begin{aligned}
&L_{D_\eta}(h_t)\\
&\quad=0{,}2\Big[\sum_{x<t}\eta(x)\\
&\qquad+\sum_{x\ge t}\big(1-\eta(x)\big)\Big],
\end{aligned}
$$
và tương tự
$$
\begin{aligned}
&L^c_{D_\eta}(h_t)\\
&\quad=0{,}2\Big[c_{FN}\sum_{x<t}\eta(x)\\
&\qquad+c_{FP}\sum_{x\ge t}\big(1-\eta(x)\big)\Big].
\end{aligned}
$$
Chẳng hạn với $t=3$, hai tổng là $0+\tfrac14=0{,}25$ và $\tfrac14+\tfrac35+0=0{,}85$, nên $L_{D_\eta}(h_3)=0{,}2\cdot1{,}1=0{,}22$ và $L^c_{D_\eta}(h_3)=0{,}2\,(4\cdot0{,}25+0{,}85)=0{,}37$. Các giá trị còn lại tính tương tự (Phụ lục C.1):

| $t$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ |
|---|---|---|---|---|---|---|
| $L_{D_\eta}(h_t)$ | $0{,}52$ | $0{,}32$ | $\mathbf{0{,}22}$ | $0{,}32$ | $0{,}28$ | $0{,}48$ |
| $L^c_{D_\eta}(h_t)$ | $0{,}52$ | $\mathbf{0{,}32}$ | $0{,}37$ | $0{,}92$ | $1{,}12$ | $1{,}92$ |

Dưới hàm lỗi 0–1, hàm tốt nhất trong $\mathcal H$ là $h_3$, với $\min_tL_{D_\eta}(h_t)=0{,}22$. Dưới $\ell_c$, hàm tốt nhất là $h_2$: khi bỏ sót đắt gấp bốn, báo dương tính thêm cho mức 2 (nơi $\eta(2)=\tfrac14$) làm rủi ro giảm từ $0{,}37$ xuống $0{,}32$. Hai hàm lỗi chọn ra hai hàm tốt nhất khác nhau trong cùng một lớp.
:::

Khung rủi ro không gắn với phân lớp: chỉ cần đổi tập nhãn và hàm lỗi, cùng định nghĩa áp dụng cho hồi quy.

::: example Ví dụ 01.3 (Hồi quy tuyến tính với hàm lỗi bình phương)
Cho $\mathcal X=\mathbb R^p$, $\mathcal Y=\mathbb R$, một phân bố $D$ trên $\mathbb R^p\times\mathbb R$, lớp $\mathcal H=\{h_w:x\mapsto\langle w,x\rangle,\ w\in\mathbb R^p\}$ và hàm lỗi bình phương. Không có mẫu; $L_D(h_w)=\mathbb E\big(\langle w,X\rangle-Y\big)^2\in[0,\infty]$ là một hàm tất định của $w$. Theo $(a-b)^2\le2a^2+2b^2$ và bất đẳng thức Cauchy–Schwarz $\langle w,x\rangle^2\le\lVert w\rVert^2\lVert x\rVert^2$,
$$
\begin{aligned}
&\big(\langle w,X\rangle-Y\big)^2\\
&\quad\le 2\langle w,X\rangle^2+2Y^2\\
&\quad\le 2\lVert w\rVert^2\lVert X\rVert^2+2Y^2 .
\end{aligned}
$$
Lấy kì vọng hai vế, ta được $L_D(h_w)\le2\lVert w\rVert^2\,\mathbb E\lVert X\rVert^2+2\,\mathbb EY^2$, nên điều kiện mô-men $\mathbb E\lVert X\rVert^2<\infty$, $\mathbb EY^2<\infty$ đủ để mọi $h_w$ có rủi ro hữu hạn.
:::

::: remark Nhận xét 01.2 (Tính khả tích khi hàm lỗi không bị chặn)
Điều kiện $\mathbb EY^2<\infty$ trong Ví dụ 01.3 là cần thiết để mọi $h_w$ có rủi ro hữu hạn: nếu $\mathbb EY^2=\infty$, hàm $h_0\equiv0$ có $L_D(h_0)=\mathbb EY^2=\infty$, và mọi so sánh rủi ro với $h_0$ mất nghĩa. Hàm lỗi log (log loss) bằng $-\ln$ của xác suất mà hàm dự đoán gán cho nhãn đúng. Hàm lỗi này và hàm lỗi bình phương đều không bị chặn, nên các cận của Bài 02 cho hàm lỗi trong $[0,1]$ không tự chuyển sang chúng.
:::

Với hàm lỗi không bị chặn, chúng ta cần tách riêng những phân bố mà mọi rủi ro trong lớp đều hữu hạn.

::: definition Định nghĩa 01.3 (Phân bố có rủi ro hữu hạn)
Cho lớp giả thuyết $\mathcal H$ và hàm lỗi $\ell$ trên tập quan sát $\mathcal Z$. Một phân bố $D$ trên $\mathcal Z$ được gọi là *phân bố có rủi ro hữu hạn* (finite-risk distribution) trên $\mathcal H$ nếu $L_D(h)<\infty$ với mọi $h\in\mathcal H$.
:::

Khi $\ell$ bị chặn, như $\ell_{0\text{-}1}$ hay $\ell_c$, mọi phân bố đều có rủi ro hữu hạn; với lớp tuyến tính của Ví dụ 01.3, điều kiện mô-men là đủ.

Rủi ro kì vọng đánh giá một hàm dự đoán cho trước. Khi học, hàm dự đoán được chọn từ mẫu. Vì vậy, trước khi phát biểu bài toán học thống kê, chúng ta cần nói rõ thuật toán học nhận gì và trả về gì.

::: definition Định nghĩa 01.4 (Thuật toán học)
Cho tập quan sát $\mathcal Z$, lớp giả thuyết $\mathcal H$ và hàm lỗi $\ell$. Một *thuật toán học* là một họ ánh xạ $A_m:\mathcal Z^m\to\mathcal H$, $m\ge1$, sao cho ánh xạ $(s,z)\mapsto\ell(A_m(s),z)$ đo được trên $\mathcal Z^m\times\mathcal Z$. Ta viết $A(S)$ thay cho $A_m(S)$.
:::

Thuật toán học không nhận $D$. Điều kiện đo được chỉ để $L_D(A(S))$ là một biến ngẫu nhiên, và tự thỏa khi $\mathcal X$, $\mathcal Y$ hữu hạn và mọi tập con đều đo được (Phụ lục A). Đầu ra thuộc $\mathcal H$, tức thuật toán học đúng lớp (proper learning). Quy tắc "trả về $\mathbb 1[\eta(x)\ge\tfrac12]$" không phải là thuật toán học, vì nó cần biết $\eta$ (§1).

Ghép rủi ro kì vọng và thuật toán học vừa định nghĩa với các thành phần còn lại của §1, ta được bài toán học thống kê.

::: definition Định nghĩa 01.5 (Bài toán học thống kê)
Cho tập quan sát $\mathcal Z=\mathcal X\times\mathcal Y$, một lớp giả thuyết $\mathcal H$ và một hàm lỗi $\ell$, cả hai được chọn trước khi lấy mẫu. *Bài toán học thống kê* (statistical learning problem) với $\mathcal H$ và $\ell$ như sau. Một phân bố dữ liệu $D$ trên $\mathcal Z$ cố định nhưng chưa biết; khi $\ell$ không bị chặn, $D$ có rủi ro hữu hạn trên $\mathcal H$ (Định nghĩa 01.3). Thông tin duy nhất về $D$ là một mẫu $S=(Z_1,\ldots,Z_m)\sim D^m$ gồm $m$ quan sát i.i.d. theo $D$. Cần một thuật toán học $A$ (Định nghĩa 01.4) sao cho hiệu
$$
L_D\big(A(S)\big)-\inf_{h\in\mathcal H}L_D(h)
$$
nhỏ, trong đó $L_D$ là rủi ro kì vọng của Định nghĩa 01.1 và $\inf_{h\in\mathcal H}L_D(h)$ là mức tốt nhất trong lớp; hiệu này không âm vì $A(S)\in\mathcal H$. Thuật toán $A$ được chọn trước khi lấy mẫu và không phụ thuộc $D$, nên yêu cầu trên phải đúng với mọi $D$ có thể xảy ra. Nói gọn, mục tiêu là tối thiểu hóa rủi ro kì vọng trên $\mathcal H$ khi không tính được $L_D$.
:::

Trong Định nghĩa 01.5 có ba loại đại lượng. Phân bố $D$ cố định nhưng chưa biết, và thuật toán không đọc được nó. Lớp $\mathcal H$ và hàm lỗi $\ell$ được chọn trước, không phụ thuộc mẫu. Mẫu $S$ ngẫu nhiên theo $D^m$, nên hàm học được $A(S)$ và rủi ro $L_D(A(S))$ của nó cũng ngẫu nhiên, như dòng thứ hai của bảng ở §1.

Nhờ điều kiện rủi ro hữu hạn, hiệu trong định nghĩa là một số thực. Hiệu đó phải nhỏ đến đâu, với xác suất nào theo $S$, và trên họ phân bố $D$ nào? Ba câu hỏi này được trả lời ở §6 và §7. Từ đây ta gọi tắt bài toán học thống kê là *bài toán học*.

::: example Ví dụ 01.4 (Bài toán học trong ví dụ sàng lọc)
Xét bản có nhiễu của Ví dụ 01.1: $\mathcal X=\{1,\ldots,5\}$, $\mathcal Y=\{0,1\}$, lớp sáu hàm ngưỡng, hàm lỗi 0–1, cỡ mẫu $m=6$. Theo Ví dụ 01.2, mức tốt nhất trong lớp là $\inf_tL_{D_\eta}(h_t)=L_{D_\eta}(h_3)=0{,}22$. Thuật toán không biết bảng $\eta$ của Ví dụ 01.1; thông tin duy nhất là một mẫu $S\sim D_\eta^6$, chẳng hạn $S_\eta$. Bài toán học là chọn trước một quy tắc $A$ biến mỗi mẫu cỡ $6$ thành một ngưỡng $\hat t$, sao cho $L_{D_\eta}(h_{\hat t})-0{,}22$ nhỏ. Một mẫu khác rút từ $D_\eta^6$ có thể cho ngưỡng khác, nên hiệu này ngẫu nhiên theo $S$.

Ở bản nhãn tất định, mức tốt nhất là $L_{D_f}(h_3)=0$. Trên mẫu $S_f$ của câu hỏi mở đầu (cỡ $m=4$), $h_3$ và $h_4$ đều phân lớp đúng mọi quan sát, nhưng $L_{D_f}(h_4)=0{,}2$; chỉ nhìn mẫu, ta không biết nên trả về hàm nào.
:::

Hiệu trong Định nghĩa 01.5 không tính được, vì $L_D(h)$ là kì vọng theo $D$ chưa biết, kể cả khi $h$ cho trước. Chúng ta cần một đại lượng tính được từ $S$ thay cho $L_D(h)$, cần biết khi nào thay được như vậy, và cần một quy tắc chọn giả thuyết dựa trên đại lượng này.

## 5. Rủi ro thực nghiệm và tối thiểu hóa rủi ro thực nghiệm

Đại lượng tính được từ dữ liệu là trung bình của hàm lỗi trên các quan sát của mẫu.

::: definition Định nghĩa 01.6 (Rủi ro thực nghiệm)
Cho hàm lỗi $\ell$ và một mẫu $S=(z_1,\ldots,z_m)\in\mathcal Z^m$. *Rủi ro thực nghiệm* của $h\in\mathcal H$ trên $S$ là
$$
L_S(h)=\frac1m\sum_{i=1}^m\ell(h,z_i).
$$
:::

Rủi ro thực nghiệm là rủi ro kì vọng dưới *phân bố thực nghiệm* (empirical distribution) của $S$, phân bố đều trên $m$ phần tử của dãy $S$ (một quan sát lặp lại $k$ lần được tính $k$ lần). Với hàm lỗi 0–1, $L_S(h)$ là tỉ lệ lỗi (error rate) của $h$ trên mẫu. Khi $S\sim D^m$, cả $L_S(h)$ với $h$ cho trước lẫn $L_S(A(S))$ đều là biến ngẫu nhiên theo $S$, tức thuộc dòng thứ hai của bảng ở §1. Với $L_S(A(S))$, kết luận này có được nhờ điều kiện đo được của Định nghĩa 01.4.

::: example Ví dụ 01.5 (Rủi ro thực nghiệm trên một mẫu cỡ 6)
Xét mẫu cụ thể $S_\eta$ của Ví dụ 01.1 (phân bố $D_\eta$, cỡ $m=6$), lớp sáu hàm ngưỡng, hàm lỗi 0–1; mẫu đã quan sát, nên các rủi ro thực nghiệm là số. Chẳng hạn $h_3$ báo dương tính cho $x\in\{3,4,5\}$ nên sai trên $(2,1)$ và $(4,0)$, tức $L_{S_\eta}(h_3)=\tfrac26=\tfrac13$. Đặt cạnh rủi ro kì vọng của Ví dụ 01.2:

| $t$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ |
|---|---|---|---|---|---|---|
| $L_{S_\eta}(h_t)$ | $\tfrac12$ | $\tfrac13$ | $\tfrac13$ | $\tfrac12$ | $\tfrac13$ | $\tfrac12$ |
| $L_{D_\eta}(h_t)$ | $0{,}52$ | $0{,}32$ | $0{,}22$ | $0{,}32$ | $0{,}28$ | $0{,}48$ |

Ba hàm $h_2$, $h_3$, $h_5$ có cùng rủi ro thực nghiệm $\tfrac13$ nhưng rủi ro kì vọng $0{,}32$, $0{,}22$, $0{,}28$: trên mẫu này, chỉ dựa vào rủi ro thực nghiệm, ta không phân biệt được hàm tốt nhất của lớp với hai hàm kém hơn.
:::

Với một giả thuyết chọn trước khi thấy mẫu, kì vọng của rủi ro thực nghiệm bằng rủi ro kì vọng, kể cả khi các quan sát không độc lập và hàm lỗi không bị chặn.

::: proposition Mệnh đề 01.7 (Tính không chệch của rủi ro thực nghiệm với giả thuyết cố định) — chứng minh đầy đủ
**Giả thiết.** Dạng yếu của (T1): $Z_1,\ldots,Z_m$ là các biến ngẫu nhiên trên cùng một không gian xác suất, mỗi $Z_i$ có phân bố $D$; không giả sử chúng độc lập. Giả thuyết $h\in\mathcal H$ cố định, không phụ thuộc $S=(Z_1,\ldots,Z_m)$. (T2), và $L_D(h)<\infty$; điều kiện cuối chỉ để hai vế là số thực.

**Bảo đảm.** Với mọi $m\ge1$,
$$
\mathbb E_S\big[L_S(h)\big]=L_D(h).
$$
Đây là bảo đảm theo kì vọng, so một đại lượng thực nghiệm với một đại lượng tổng thể (population quantity); nó không chặn độ lệch $\lvert L_S(h)-L_D(h)\rvert$ trên một mẫu cụ thể.
:::

::: proof Chứng minh Mệnh đề 01.7
**Lộ trình.** Tính kì vọng của từng số hạng trong $L_S(h)$, rồi dùng tính tuyến tính của kì vọng.

**Bước 1 (mỗi số hạng là biến ngẫu nhiên khả tích).** Vì $h$ cố định và $\ell(h,\cdot)$ đo được, $\ell(h,Z_i)$ là một biến ngẫu nhiên không âm chỉ phụ thuộc $Z_i$; giả thiết $h$ không phụ thuộc $S$ được dùng ở đây. Vì $Z_i$ có phân bố $D$, ta có
$$
\begin{aligned}
\mathbb E\,\ell(h,Z_i)
&=\int_{\mathcal Z}\ell(h,z)\,dD(z)\\
&=L_D(h)<\infty,
\end{aligned}
$$
trong đó giả thiết cùng phân bố biên và $L_D(h)<\infty$ được dùng.

**Bước 2 (tính tuyến tính).** Kì vọng của một tổng hữu hạn các biến khả tích bằng tổng các kì vọng, nên
$$
\begin{aligned}
\mathbb E_S\big[L_S(h)\big]
&=\frac1m\sum_{i=1}^m\mathbb E\,\ell(h,Z_i)\\
&=L_D(h).
\end{aligned}
$$
Tính tuyến tính đúng cả khi các $Z_i$ không độc lập; giả thiết độc lập chỉ cần khi chặn độ lệch của $L_S(h)$ (Bài 02).

$\square$ Rủi ro thực nghiệm của một giả thuyết chọn trước khi thấy mẫu là ước lượng không chệch (unbiased estimator) của rủi ro kì vọng. Vì vậy, để ước lượng rủi ro kì vọng của một hàm dự đoán, ta tính rủi ro thực nghiệm của nó trên một mẫu độc lập với mẫu dùng để chọn nó.
:::

Đẳng thức của Mệnh đề 01.7 đúng cho trung bình theo mẫu; trên một mẫu cụ thể, $L_S(h)$ có thể khác $L_D(h)$. Trong Ví dụ 01.5, $L_{S_\eta}(h_3)=\tfrac13$, trong khi $\mathbb E_S\big[L_S(h_3)\big]=L_{D_\eta}(h_3)=0{,}22$ với $S\sim D_\eta^6$.

Dựa trên Mệnh đề 01.7, quy tắc chọn đơn giản nhất cho bài toán học của Định nghĩa 01.5 là thay $L_D$ chưa biết bằng $L_S$ và chọn giả thuyết có rủi ro thực nghiệm nhỏ nhất.

::: definition Định nghĩa 01.8 (Tối thiểu hóa rủi ro thực nghiệm)
Cho lớp giả thuyết $\mathcal H$, hàm lỗi $\ell$ và mẫu $S$. *Tập nghiệm ERM* trên $S$ là
$$
\begin{aligned}
&\arg\min_{h\in\mathcal H}L_S(h)=\big\{h\in\mathcal H:\\
&\qquad L_S(h)=\inf_{h'\in\mathcal H}L_S(h')\big\},
\end{aligned}
$$
trong đó $\inf$ là cận dưới đúng (infimum). Mỗi phần tử $\hat h$ của tập này là một *nghiệm ERM*. Giả sử tập nghiệm ERM khác rỗng với mọi mẫu $S$. Một thuật toán học $A$ được gọi là *thuật toán ERM* trên $\mathcal H$ nếu $A(S)\in\arg\min_{h\in\mathcal H}L_S(h)$ với mọi $S$.
:::

Quy tắc ERM chỉ xác định tập nghiệm; một thuật toán ERM cụ thể còn cần một *quy tắc chọn khi bằng nhau* (tie-breaking). Tập nghiệm phụ thuộc $S$, nên ngẫu nhiên khi $S\sim D^m$. Trên lớp hàm ngưỡng của Ví dụ 01.1, hai quy tắc chọn khi bằng nhau cho hai thuật toán ERM. Trên một mẫu $S$ bất kì, $A_{\max}$ (hoặc $A_{\min}$) trả về $h_t$ với $t$ lớn nhất (hoặc nhỏ nhất) trong tập nghiệm ERM. Cả hai chỉ đọc mẫu.

::: example Ví dụ 01.6 (Các nghiệm ERM trên mẫu sàng lọc)
Xét lớp sáu hàm ngưỡng, hàm lỗi 0–1 và hai mẫu cụ thể của Ví dụ 01.1; các mẫu đã quan sát, nên mọi đại lượng là số. Trên $S_\eta$, theo Ví dụ 01.5, tập nghiệm ERM là $\{h_2,h_3,h_5\}$. Hai quy tắc chọn khi bằng nhau cho hai kết quả, so với mức tốt nhất trong lớp $\min_tL_{D_\eta}(h_t)=0{,}22$:

| Quy tắc chọn | Hàm trả về | $L_{D_\eta}$ | $L_{D_\eta}-0{,}22$ |
|---|---|---|---|
| ngưỡng nhỏ nhất ($A_{\min}$) | $h_2$ | $0{,}32$ | $0{,}10$ |
| ngưỡng lớn nhất ($A_{\max}$) | $h_5$ | $0{,}28$ | $0{,}06$ |

Chỉ $h_3$ đạt mức $0{,}22$, nhưng hai thuật toán trong bảng trả về $h_2$ và $h_5$; một quy tắc chọn $h_3$ khi bằng nhau sẽ đạt mức đó.

Dưới $D_f$, $h_3$ khớp mọi mẫu, nên tập nghiệm ERM gồm các $h_t$ với $t$ lớn hơn mọi giá trị $x$ có nhãn 0 và không vượt quá mọi giá trị $x$ có nhãn 1 trong $S$. Do đó $A_{\max}$ chọn $\hat t$ bằng giá trị $x$ nhỏ nhất trong các quan sát có nhãn 1, hoặc $\hat t=6$ khi mẫu không có nhãn 1; vì vậy $\hat t\in\{3,\ldots,6\}$. Thuật toán $A_{\min}$ chọn $\hat t$ bằng $1$ cộng giá trị $x$ lớn nhất trong các quan sát có nhãn 0, hoặc $\hat t=1$ khi mẫu không có nhãn 0; vì vậy $\hat t\in\{1,2,3\}$.

Trên $S_f$, $h_3$ và $h_4$ là hai nghiệm ERM duy nhất ($h_2$ sai trên $(2,0)$, $h_5$ sai trên $(4,1)$); $A_{\min}$ chọn $h_3$, có $L_{D_f}=0$, còn $A_{\max}$ chọn $h_4$, có $L_{D_f}=0{,}2$. Khi có nhiều nghiệm ERM, quy tắc chọn khi bằng nhau quyết định rủi ro kì vọng của hàm trả về; đó là phần đầu của câu trả lời cho câu hỏi mở đầu.
:::

Thuật toán ERM chọn giả thuyết theo chính mẫu dùng để tính $L_S$, nên giả thiết $h$ cố định của Mệnh đề 01.7 không còn thỏa.

::: remark Nhận xét 01.9 (Giả thuyết chọn theo mẫu)
Bước 1 của chứng minh Mệnh đề 01.7 hỏng khi thay $h$ bằng $A(S)$: số hạng $\ell(A(S),Z_i)$ phụ thuộc toàn bộ $S$, kể cả $Z_i$, nên nói chung $\mathbb E_S\big[L_S(A(S))\big]\ne\mathbb E_S\big[L_D(A(S))\big]$. Chẳng hạn dưới $D_f$, $h_3$ khớp mọi mẫu nên $A_{\max}$ luôn khớp mẫu, và $\mathbb E_S\big[L_S(A_{\max}(S))\big]=0$. Biến cố mẫu không chứa $x=3$ có xác suất $0{,}8^m$; trên biến cố đó, $A_{\max}$ chọn $\hat t\ge4$ và sai tại $x=3$, nên $\mathbb E_S\big[L_{D_f}(A_{\max}(S))\big]\ge0{,}2\cdot0{,}8^m>0$.

Cách sửa là đánh giá $A(S)$ trên một mẫu mới $S'$ rút từ $D$, độc lập với $S$: khi lấy điều kiện theo $S$, hàm $A(S)$ cố định đối với $S'$, nên Mệnh đề 01.7 áp dụng được cho $L_{S'}(A(S))$.
:::

Nhận xét 01.9 cho thấy $\mathbb E_S\big[L_S(A(S))\big]$ có thể khác $\mathbb E_S\big[L_D(A(S))\big]$; ta đặt tên riêng cho hiệu giữa hai rủi ro của hàm học được.

::: definition Định nghĩa 01.10 (Khoảng cách tổng quát hóa)
Cho thuật toán học $A$ và mẫu $S$. *Khoảng cách tổng quát hóa* (generalization gap) của $A$ trên $S$ là
$$
L_D\big(A(S)\big)-L_S\big(A(S)\big).
$$
:::

Khoảng cách tổng quát hóa có dấu và là một biến ngẫu nhiên theo $S$; kì vọng của nó bằng $0$ với $h$ cố định (Mệnh đề 01.7) nhưng có thể khác $0$ với hàm học được. Trên $S_f$, chẳng hạn, $A_{\max}$ trả về $h_4$ với $L_{S_f}(h_4)=0$ và $L_{D_f}(h_4)=0{,}2$, nên khoảng cách tổng quát hóa bằng $0{,}2$.

::: remark Nhận xét 01.11 (Sự tồn tại nghiệm ERM và quy tắc chọn khi bằng nhau)
Với hàm lỗi 0–1, $L_S(h)$ chỉ nhận giá trị trong tập hữu hạn $\{0,\tfrac1m,\ldots,1\}$, nên cận dưới đúng của $L_S$ trên $\mathcal H$ đạt được và tập nghiệm ERM khác rỗng với mọi lớp $\mathcal H$ khác rỗng, kể cả lớp vô hạn. Giá trị nhỏ nhất có thể dương: trên lớp cả $2^5=32$ hàm $\{1,\ldots,5\}\to\{0,1\}$, $\min L_{S_\eta}=\tfrac16$, vì tại $x=2$ mẫu $S_\eta$ có cả nhãn 0 lẫn nhãn 1. Với hàm lỗi khác, tập nghiệm có thể rỗng, như trong ví dụ sau. Khi tập nghiệm có nhiều phần tử, một bảo đảm "cho mọi nghiệm ERM" mạnh hơn một bảo đảm "cho một nghiệm ERM".
:::

::: example Ví dụ 01.7 (Cận dưới đúng không đạt được của rủi ro thực nghiệm)
Cho $\mathcal X=\mathcal Y=\mathbb R$, lớp $\mathcal H_+=\{h_w:x\mapsto wx,\ w>0\}$, hàm lỗi bình phương và mẫu một quan sát $S=((1,0))$. Khi đó $L_S(h_w)=w^2$, với cận dưới đúng $\inf_{w>0}w^2=0$ không đạt tại $w>0$ nào. Tập nghiệm ERM trên mẫu này rỗng, nên giả thiết của Định nghĩa 01.8 không thỏa và không có thuật toán ERM trên $\mathcal H_+$.
:::

Khi tập nghiệm ERM có thể rỗng, hoặc khi thuật toán tối ưu chỉ cho nghiệm gần đúng, chúng ta cần một khái niệm yếu hơn: ERM xấp xỉ (approximate ERM).

::: definition Định nghĩa 01.12 (ERM xấp xỉ)
Cho $\epsilon_{\mathrm{opt}}\ge0$. Một thuật toán học $A$ được gọi là *$\epsilon_{\mathrm{opt}}$-ERM* trên $\mathcal H$ nếu
$$
L_S(A(S))\le\inf_{h\in\mathcal H}L_S(h)+\epsilon_{\mathrm{opt}}
$$
với mọi mẫu $S$.
:::

Vì $\ell\ge0$, cận dưới đúng $\inf_{h\in\mathcal H}L_S(h)$ hữu hạn, nên với $\epsilon_{\mathrm{opt}}>0$ luôn có giả thuyết thỏa bất đẳng thức trên; với $\epsilon_{\mathrm{opt}}=0$ và tập nghiệm khác rỗng với mọi mẫu, định nghĩa trở lại thuật toán ERM. Trong Ví dụ 01.7, với $\epsilon_{\mathrm{opt}}>0$, một $\epsilon_{\mathrm{opt}}$-ERM được phép trả về mọi $h_w$ với $w\in(0,\sqrt{\epsilon_{\mathrm{opt}}}\,]$, vì $w^2\le0+\epsilon_{\mathrm{opt}}$; ERM xấp xỉ vẫn xác định ở nơi thuật toán ERM không tồn tại.

Từ hai định nghĩa trên, ta có hai mức của giả thiết tối ưu, tách khỏi các giả thiết thống kê (T1), (T2): (O1) thuật toán tính được một nghiệm ERM chính xác, hoặc (O2) chỉ tính được một $\epsilon_{\mathrm{opt}}$-ERM. Cả hai mức không đặt điều kiện nào lên $D$.

Với lớp hàm ngưỡng trên một tập đầu vào hữu hạn, toàn bộ tập nghiệm ERM tính được bằng một lượt đếm.

::: algorithm Thuật toán 01.13 (ERM cho lớp hàm ngưỡng trên tập đầu vào hữu hạn)
**Đầu vào.** Mẫu $S=((x_1,y_1),\ldots,(x_m,y_m))$ với $x_i\in\{1,\ldots,K\}$, $y_i\in\{0,1\}$; lớp $\{h_t=\mathbb 1[x\ge t]:\ t=1,\ldots,K+1\}$; hàm lỗi 0–1.

**Khởi tạo.** Tính các số đếm $c_y(x)=\#\{i:\ x_i=x,\ y_i=y\}$ với $x\in\{1,\ldots,K\}$, $y\in\{0,1\}$. Đặt $E(1)=\sum_{x=1}^Kc_0(x)$, số lỗi của $h_1\equiv1$.

**Cập nhật.** Với $t=1,\ldots,K$, đặt $E(t+1)=E(t)-c_0(t)+c_1(t)$. Khi ngưỡng tăng từ $t$ lên $t+1$, chỉ dự đoán tại $x=t$ đổi từ $1$ sang $0$: các quan sát nhãn 0 tại $t$ hết sai, các quan sát nhãn 1 tại $t$ trở thành sai.

**Đầu ra.** $L_S(h_t)=E(t)/m$ với mọi $t$; tập nghiệm ERM $\{h_t:\ E(t)=\min_{t'}E(t')\}$; một nghiệm ERM là ngưỡng nhỏ nhất (hoặc lớn nhất) đạt giá trị nhỏ nhất.

**Điều kiện dừng.** Dừng sau $K$ lần cập nhật.

**Chi phí.** $O(m)$ phép tính cho các số đếm và $O(K)$ cho các cập nhật, tổng cộng $O(m+K)$.
:::

Trên $S_\eta$ với $K=5$, các số đếm là $c_0=(1,1,0,1,0)$ và $c_1=(0,1,1,0,1)$, nên $E=(3,2,2,3,2,3)$, khớp Ví dụ 01.5. Hai phiên bản của đầu ra là $A_{\min}$ và $A_{\max}$.

Trên $S_\eta$, quy tắc chọn khi bằng nhau đổi rủi ro kì vọng dưới $D_\eta$ giữa $0{,}22$ và $0{,}32$. Trên một lớp đủ lớn, nó có thể đổi rủi ro từ $0$ sang $1$. Trong các nghiệm ERM, thuật toán sau chọn nghiệm chỉ lặp lại mẫu.

::: definition Định nghĩa 01.14 (Thuật toán ghi nhớ)
Cho tập đầu vào $\mathcal X$ với một σ-đại số chứa mọi tập một điểm, và $\mathcal Y=\{0,1\}$. Với một mẫu $s=((x_1,y_1),\ldots,(x_m,y_m))$, hàm $A_{\mathrm{gn}}(s):\mathcal X\to\{0,1\}$ nhận giá trị như sau. Tại mỗi $x\in\{x_1,\ldots,x_m\}$, $A_{\mathrm{gn}}(s)(x)$ là nhãn chiếm đa số trong các quan sát của $s$ tại $x$, với nhãn $1$ khi số phiếu bằng nhau; tại mọi điểm khác, $A_{\mathrm{gn}}(s)(x)=0$. Thuật toán tất định $s\mapsto A_{\mathrm{gn}}(s)$ được gọi là *thuật toán ghi nhớ* (memorizing algorithm), và $A_{\mathrm{gn}}(s)$ là *hàm phân lớp ghi nhớ* (memorizing classifier).
:::

Hàm phân lớp ghi nhớ không dùng cấu trúc nào của $\mathcal X$; trên $S_f$, chẳng hạn, $A_{\mathrm{gn}}(S_f)=\mathbb 1[x\ge4]=h_4$. Điều kiện đo được đồng thời trong Định nghĩa 01.4 được kiểm ở Phụ lục A cho hai trường hợp dùng trong bài: $\mathcal X=[0,1]$ và $\mathcal X$ hữu hạn. Trong ví dụ sau, ta dựng một lớp và một phân bố mà dưới đó hàm phân lớp ghi nhớ sai trên mọi quan sát mới.

::: example Ví dụ 01.8 (Phân bố đều trên $[0,1]$ với nhãn hằng)
Với một tập đầu vào $\mathcal X$ có σ-đại số, kí hiệu $\mathcal M_{\mathcal X}$ là lớp mọi hàm phân lớp đo được $\mathcal X\to\{0,1\}$. Tập đầu vào ở đây là $\mathcal X=[0,1]$ với σ-đại số Borel, tập nhãn $\mathcal Y=\{0,1\}$. Phân bố $D$: $X\sim U[0,1]$ và $Y=1$ chắc chắn. Lớp giả thuyết $\mathcal H=\mathcal M_{\mathcal X}$ gồm mọi hàm phân lớp đo được $[0,1]\to\{0,1\}$; hàm lỗi $\ell_{0\text{-}1}$; cỡ mẫu $m\ge1$ tùy ý. Mẫu $S=((X_1,1),\ldots,(X_m,1))$ là ngẫu nhiên; mọi nhãn trong mẫu bằng 1.

Lớp $\mathcal M_{\mathcal X}$ chứa hàm hằng $1$, có rủi ro $0$, và hàm chỉ thị của mọi tập hữu hạn; $U[0,1]$ không có nguyên tử. Cả hàm hằng $1$ lẫn hàm phân lớp ghi nhớ đều khớp mọi mẫu rút từ $D$; rủi ro kì vọng của hai hàm này được tính trong mệnh đề sau.
:::

::: proposition Mệnh đề 01.15 (Hàm phân lớp ghi nhớ có rủi ro kì vọng bằng 1) — chứng minh đầy đủ
**Giả thiết.** Thiết lập của Ví dụ 01.8: $\mathcal X=[0,1]$ với σ-đại số Borel, $D$ là phân bố của $(X,1)$ với $X\sim U[0,1]$, $\mathcal H=\mathcal M_{\mathcal X}$, hàm lỗi 0–1 (T2). Thuật toán là $A_{\mathrm{gn}}$; cỡ mẫu $m\ge1$ tùy ý.

**Bảo đảm.** Khẳng định tất định, đúng với mọi mẫu: (a) Với mọi mẫu $s$, $A_{\mathrm{gn}}(s)\in\mathcal H$ là một nghiệm ERM, nên $A_{\mathrm{gn}}$ là một thuật toán ERM trên $\mathcal H$; dưới $D$, $L_S(A_{\mathrm{gn}}(S))=0$. (b) Dưới $D$, $L_D(A_{\mathrm{gn}}(S))=1$, nên khoảng cách tổng quát hóa bằng $1$ với mọi $m$. (c) Hàm hằng $h_{\equiv1}$ cũng là nghiệm ERM trên mọi mẫu dưới $D$, và $L_D(h_{\equiv1})=0=\inf_{h\in\mathcal H}L_D(h)$.
:::

::: proof Chứng minh Mệnh đề 01.15
**Lộ trình.** Kiểm tra hàm phân lớp ghi nhớ thuộc lớp, tính rủi ro thực nghiệm, rồi tính rủi ro kì vọng. Tính chất then chốt là một tập hữu hạn có xác suất $0$ dưới $U[0,1]$.

**Bước 1 (thuộc lớp).** Hàm $A_{\mathrm{gn}}(s)$ bằng $1$ trên một tập con của tập hữu hạn $F=\{x_1,\ldots,x_m\}$ và bằng $0$ ở nơi khác. Mọi tập con hữu hạn của $[0,1]$ là tập Borel, nên $A_{\mathrm{gn}}(s)\in\mathcal M_{\mathcal X}=\mathcal H$; giả thiết lớp gồm mọi hàm phân lớp đo được được dùng ở đây. Điều kiện đo được đồng thời trong Định nghĩa 01.4 được kiểm ở Phụ lục A(iii).

**Bước 2 (rủi ro thực nghiệm).** Rủi ro thực nghiệm của một hàm chỉ phụ thuộc giá trị của nó trên $F$, và tại mỗi điểm của $F$ số lỗi nhỏ nhất đạt được khi dự đoán nhãn đa số. Vì $A_{\mathrm{gn}}(s)$ làm đúng như vậy và thuộc $\mathcal H$, nó là một nghiệm ERM; tập nghiệm khác rỗng theo Nhận xét 01.11. Dưới $D$, mọi nhãn bằng $1$, nên $A_{\mathrm{gn}}(S)=\mathbb 1_F$ và $L_S(A_{\mathrm{gn}}(S))=0$.

**Bước 3 (rủi ro kì vọng).** Vì $Y=1$ chắc chắn, $A_{\mathrm{gn}}(S)$ sai trên $(X,Y)$ khi và chỉ khi $X\notin F$. Theo bất đẳng thức hợp (union bound) và vì $U[0,1]$ không có nguyên tử,
$$
\begin{aligned}
\Pr(X\in F)
&\le\sum_{i=1}^m\Pr(X=x_i)\\
&=0 .
\end{aligned}
$$
Do đó $L_D(A_{\mathrm{gn}}(S))=\Pr(X\notin F)=1$. Giả thiết $D_{\mathcal X}$ không có nguyên tử được dùng ở đây.

**Bước 4 (một nghiệm ERM tốt).** Hàm hằng $h_{\equiv1}$ đúng trên mọi $(X,1)$, nên $L_S(h_{\equiv1})=L_D(h_{\equiv1})=0$, và $0$ là cận dưới đúng của $L_D\ge0$ trên $\mathcal H$.

$\square$ Trên lớp chứa mọi hàm phân lớp đo được, hai nghiệm ERM trên cùng một mẫu có rủi ro kì vọng $0$ và $1$, nên quy tắc chọn khi bằng nhau quyết định toàn bộ rủi ro kì vọng. Hàm phân lớp ghi nhớ là trường hợp cực đoan của quá khớp (overfitting).
:::

Chọn lớp giả thuyết trước khi thấy mẫu là một *thiên kiến quy nạp* (inductive bias): một cam kết về dạng của hàm dự đoán, đặt ra trước khi có dữ liệu. Lớp $\mathcal M_{\mathcal X}$ của Ví dụ 01.8 là phản ví dụ: nó không cam kết gì, nên trên mỗi mẫu có vô số hàm của lớp khớp mẫu, với rủi ro kì vọng trải từ $0$ đến $1$.

Lớp hàm ngưỡng cam kết rằng dự đoán dương tính không giảm khi chỉ số đo tăng. Trên mẫu $\tilde S_f=((1,0),(3,1),(5,1))$ rút từ $D_f$, hàm phân lớp ghi nhớ là $\mathbb 1[x\in\{3,5\}]\notin\mathcal H$, sai tại $x=4$ nên có rủi ro $0{,}2$. Lớp hàm ngưỡng chỉ giữ lại $h_2$ (rủi ro $0{,}2$) và $h_3$ (rủi ro $0$), vì mọi hàm ngưỡng dương tính tại $x=3$ cũng dương tính tại $x=4$. Trên $S_f$, ngược lại, hàm phân lớp ghi nhớ trùng với $h_4$, và lớp không loại được ứng viên nào.

Lớp giả thuyết có thể không chứa hàm dự đoán tốt nhất; đó là giá của thiên kiến quy nạp. Quy tắc chọn khi bằng nhau là một thiên kiến khác, đặt ở mức thuật toán. Vì $h_3$ và $h_4$ cùng có rủi ro thực nghiệm $0$ trên $S_f$, một bảo đảm học phải phát biểu trực tiếp cho $L_D(A(S))$ và phải cho phép thất bại trên những mẫu như $S_f$.

## 6. Học PAC trong trường hợp khả thực

Hiệu $L_D(A(S))-\inf_{h\in\mathcal H}L_D(h)$ trong Định nghĩa 01.5 phải nhỏ theo nghĩa nào? Mẫu $S_f$ của câu hỏi mở đầu cho thấy chữ "nhỏ" cần hai tham số.

Dưới $D_f$, mẫu $S_f$ không chứa quan sát nào tại $x=3$, và một mẫu cỡ $m$ bỏ sót mức này với xác suất $0{,}8^m$, dương với mọi $m$. Không thuật toán nào tránh được những mẫu như vậy, nên mọi bảo đảm phải cho phép một xác suất thất bại (failure probability) $\delta>0$ theo mẫu. Bảo đảm cũng phải cho phép một sai số $\epsilon>0$ về rủi ro.

Nếu mức 3 chỉ chiếm $0{,}001$ dân số, một mẫu $500$ người bỏ sót nó với xác suất $0{,}999^{500}\approx0{,}61$; tham số $\epsilon$ cho phép bỏ qua những vùng có khối lượng xác suất (probability mass) nhỏ như vậy. Trường hợp đơn giản nhất là khi lớp chứa một giả thuyết có rủi ro kì vọng bằng $0$.

::: definition Định nghĩa 01.16 (Tính khả thực)
Cho hàm lỗi 0–1, một lớp giả thuyết $\mathcal H$ và một phân bố $D$ trên $\mathcal X\times\{0,1\}$. Cặp $(D,\mathcal H)$ được gọi là *khả thực* (realizable) nếu tồn tại $h^\star\in\mathcal H$ với $L_D(h^\star)=0$.
:::

Trong Định nghĩa 01.16, giá trị nhỏ nhất $0$ phải đạt được tại một phần tử của $\mathcal H$; điều kiện $\inf_{h\in\mathcal H}L_D(h)=0$ yếu hơn. Một kết quả chỉ dùng giả thiết khả thực (realizability assumption), tức giả thiết $(D,\mathcal H)$ khả thực, khi nêu rõ nó. Khi $(D,\mathcal H)$ khả thực, $Y=h^\star(X)$ hầu chắc chắn, nên với xác suất $1$ theo $S\sim D^m$, ta có $L_S(h^\star)=0$ và mọi nghiệm ERM có rủi ro thực nghiệm bằng $0$. Cặp $(D_f,\mathcal H)$ của Ví dụ 01.1 khả thực với $h^\star=h_3$; cặp $(D_\eta,\mathcal H)$ thì không, vì $\min_tL_{D_\eta}(h_t)=0{,}22>0$.

::: remark Nhận xét 01.17 (Khả thực là tính chất của cặp $(D,\mathcal H)$)
Tính khả thực đổi khi đổi một trong hai thành phần. Cùng phân bố $D_f$: cặp với lớp hàm ngưỡng khả thực, cặp với lớp hai hàm hằng $\{h_1,h_6\}$ thì không, vì $L_{D_f}(h_1)=0{,}4$ và $L_{D_f}(h_6)=0{,}6$. Cùng lớp hàm ngưỡng: khả thực với $D_f$, không với $D_\eta$. Phân bố $D_\eta$ không khả thực với bất kì lớp nào: tại $x=2$, mọi hàm phân lớp $g$ sai với xác suất ít nhất $0{,}2\cdot\min\{\tfrac14,\tfrac34\}=0{,}05$, nên $L_{D_\eta}(g)\ge0{,}05$.

Điều kiện $\inf=0$ khác điều kiện $\min=0$. Lấy $X\sim U[0,1]$, $Y=\mathbb 1[X>\tfrac12]$ và $\mathcal H=\{\mathbb 1[x\ge\tfrac12+\tfrac1k]:\ k\ge2\}$. Giả thuyết thứ $k$ chỉ sai trên khoảng $(\tfrac12,\tfrac12+\tfrac1k)$, nên có rủi ro $\tfrac1k$. Cận dưới đúng của rủi ro trên lớp bằng $0$ nhưng không đạt, và cặp này không khả thực.
:::

::: definition Định nghĩa 01.18 (Học PAC trong trường hợp khả thực)
Cho tập đầu vào $\mathcal X$, tập nhãn $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và lớp giả thuyết $\mathcal H$; kí hiệu $\mathbb N=\{1,2,\ldots\}$. Một thuật toán học $A$ được gọi là *thuật toán học PAC* cho $\mathcal H$ nếu tồn tại một hàm $M:(0,1)^2\to\mathbb N$ sao cho với mọi $\epsilon,\delta\in(0,1)$, mọi phân bố $D$ trên $\mathcal X\times\mathcal Y$ mà $(D,\mathcal H)$ khả thực, và mọi $m\ge M(\epsilon,\delta)$,
$$
\begin{aligned}
&\Pr_{S\sim D^m}\Big[L_D\big(A(S)\big)\le\epsilon\Big]\\
&\qquad\ge1-\delta .
\end{aligned}
$$
Lớp $\mathcal H$ được gọi là *học được PAC* (PAC learnable) nếu tồn tại một thuật toán học PAC cho $\mathcal H$.
:::

Viết gọn, thứ tự lượng từ của định nghĩa là
$$
\begin{aligned}
&\exists A\ \ \exists M\ \ \forall\epsilon,\delta\in(0,1)\\
&\forall D\ \ \forall m\ge M(\epsilon,\delta):\\
&\Pr_{S\sim D^m}\big[L_D(A(S))\le\epsilon\big]\ge1-\delta ,
\end{aligned}
$$
trong đó $D$ chạy trên các phân bố mà $(D,\mathcal H)$ khả thực. Vì $\exists M$ đứng trước $\forall D$, cỡ mẫu đủ chỉ phụ thuộc $(\epsilon,\delta)$; bảo đảm là *không phụ thuộc phân bố* (distribution-free). Vì $\forall D$ đứng sau $\exists A\,\exists M$, thuật toán và cỡ mẫu phải được chọn trước khi biết $D$; đây là cách viết hình thức của giả thiết $D$ chưa biết trong Định nghĩa 01.5.

Xác suất được lấy theo $S$, với $D$ cố định bên trong dấu $\Pr$. Thuật toán $A$ đứng trước $\forall\epsilon,\delta$, nên nó không nhận $\epsilon$, $\delta$ làm đầu vào. Tham số độ chính xác (accuracy parameter) $\epsilon$ là ngưỡng cho rủi ro kì vọng, còn $1-\delta$ là *độ tin cậy* (confidence). Nếu đổi chỗ thành "$\forall D\ \exists m$", ta được một khái niệm yếu hơn, trong đó cỡ mẫu được phép phụ thuộc phân bố chưa biết.

Với $(D,\mathcal H)$ khả thực, $\inf_{h\in\mathcal H}L_D(h)=0$, nên Định nghĩa 01.18 làm chính xác mục tiêu của Định nghĩa 01.5: hiệu $L_D(A(S))-0$ không vượt quá $\epsilon$ với xác suất ít nhất $1-\delta$ theo $S$, khi $m\ge M(\epsilon,\delta)$.

Khi Bài 05 mở rộng Định nghĩa 01.4 cho thuật toán dùng nguồn ngẫu nhiên riêng, như hạ gradient ngẫu nhiên (stochastic gradient descent, SGD), xác suất được lấy theo cả mẫu và nguồn ngẫu nhiên đó.

::: remark Nhận xét 01.19 (Độ tin cậy lấy theo mẫu, không phải xác suất hậu nghiệm)
Xác suất $1-\delta$ được tính trước khi lấy mẫu, theo các lần lấy mẫu giả định lặp lại từ cùng $D$. Sau khi đã thấy $S$, $L_D(A(S))$ là một số cố định, hoặc không vượt quá $\epsilon$, hoặc vượt quá. Câu "với xác suất $0{,}95$" vì vậy không phải xác suất hậu nghiệm (posterior probability) của biến cố $L_D(A(S))\le\epsilon$ khi biết $S$, cũng không phải xác suất chẩn đoán đúng cho một người cụ thể; đại lượng sau liên quan đến $\eta(x)$.
:::

Trong Định nghĩa 01.18, chỉ cần tồn tại một hàm $M$; giá trị nhỏ nhất có thể của $M$ đo lượng dữ liệu mà thuật toán cần.

::: definition Định nghĩa 01.20 (Độ phức tạp mẫu)
Cho $\mathcal X$, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và lớp $\mathcal H$ như trong Định nghĩa 01.18. Với một thuật toán học $A$ và $\epsilon,\delta\in(0,1)$, *độ phức tạp mẫu* (sample complexity) $m_A(\epsilon,\delta)$ của $A$ là số $m_0\in\mathbb N$ nhỏ nhất sao cho bất đẳng thức xác suất của Định nghĩa 01.18 đúng với mọi $D$ mà $(D,\mathcal H)$ khả thực và mọi $m\ge m_0$; khi không có $m_0$ nào như vậy, $m_A(\epsilon,\delta)=\infty$. Độ phức tạp mẫu của lớp $\mathcal H$ là
$$
m_{\mathcal H}(\epsilon,\delta)=\min_{A}m_A(\epsilon,\delta),
$$
trong đó giá trị nhỏ nhất lấy trên mọi thuật toán học cho $\mathcal H$, riêng cho từng cặp $(\epsilon,\delta)$.
:::

Hai giá trị nhỏ nhất tồn tại vì mọi tập con khác rỗng của $\mathbb N\cup\{\infty\}$ có phần tử nhỏ nhất. Lớp $\mathcal H$ học được PAC khi và chỉ khi có một thuật toán $A$ với $m_A(\epsilon,\delta)<\infty$ cho mọi $(\epsilon,\delta)$; khi đó $A$ cùng $M=m_A$ thỏa Định nghĩa 01.18.

::: remark Nhận xét 01.21 (Độ phức tạp mẫu của thuật toán và của lớp)
Vì $m_{\mathcal H}\le m_A$ với mọi $A$, để có một cận trên cho $m_{\mathcal H}$, chỉ cần một thuật toán tốt; để có một cận dưới, ta phải lập luận cho mọi thuật toán (Bài 03). Như ở giáo trình *Understanding Machine Learning: From Theory to Algorithms* của Shalev-Shwartz và Ben-David (2014), viết tắt UML (§3.1), $m_{\mathcal H}$ lấy riêng cho từng cặp $(\epsilon,\delta)$, nên thuật toán đạt nó có thể đổi theo cặp. Vì vậy, nếu chỉ dùng định nghĩa, từ $m_{\mathcal H}(\epsilon,\delta)<\infty$ với mọi $(\epsilon,\delta)$ ta chưa suy ra được một thuật toán dùng được cho mọi cặp.

Bảo đảm phải đúng với mọi $m\ge m_0$, vì thành công ở cỡ $m$ không kéo theo thành công ở cỡ $m+1$. Xét lớp hàm ngưỡng và thuật toán chạy $A_{\max}$ khi $m$ chẵn, trả về $h_6\equiv0$ khi $m$ lẻ. Gọi $D_1$ là phân bố trên $\{1,\ldots,5\}\times\{0,1\}$ với $D_{\mathcal X}$ đều và $Y=1$ chắc chắn, khả thực với $h^\star=h_1$. Vì $L_{D_1}(h_6)=1$, thuật toán thất bại chắc chắn ở mọi cỡ mẫu lẻ với mọi $\epsilon\in(0,1)$, dù ở cỡ mẫu chẵn nó thất bại với xác suất không quá $0{,}8^m$; do đó $m_A(\epsilon,\delta)=\infty$ với mọi $(\epsilon,\delta)$.
:::

::: example Ví dụ 01.9 (Xác suất thất bại và cỡ mẫu cho một phân bố khả thực)
Xét phân bố $D_f$ của Ví dụ 01.1, lớp sáu hàm ngưỡng, hàm lỗi 0–1, mẫu ngẫu nhiên $S\sim D_f^m$ và thuật toán ERM $A_{\max}$. Đại lượng ngẫu nhiên là ngưỡng $\hat t\in\{3,4,5,6\}$ mà $A_{\max}$ chọn. Hàm $h_{\hat t}$ sai đúng tại các mức $x\in\{3,\ldots,\hat t-1\}$, nên $L_{D_f}(A_{\max}(S))=0{,}2\,(\hat t-3)\in\{0;\ 0{,}2;\ 0{,}4;\ 0{,}6\}$.

Rủi ro dương khi và chỉ khi không quan sát nào của $S$ rơi vào $x=3$; các quan sát độc lập và mỗi quan sát tránh $x=3$ với xác suất $0{,}8$, nên
$$
\begin{aligned}
&\Pr_{S\sim D_f^m}\Big[L_{D_f}\big(A_{\max}(S)\big)>0\Big]\\
&\qquad=0{,}8^m .
\end{aligned}
$$
Với $\epsilon=0{,}1$ và $\delta=0{,}05$, biến cố thành công $L_{D_f}(A_{\max}(S))\le0{,}1$ trùng với biến cố $L_{D_f}(A_{\max}(S))=0$, nên cần $0{,}8^m\le0{,}05$. Vì $0{,}8^{13}\approx0{,}0550$ và $0{,}8^{14}\approx0{,}0440$, điều kiện này đúng khi và chỉ khi $m\ge14$. Với $\epsilon=0{,}25$, thất bại khi và chỉ khi $\hat t\ge5$, tức cả $x=3$ và $x=4$ vắng mặt, với xác suất $0{,}6^m$; vì $0{,}6^5\approx0{,}0778$ và $0{,}6^6\approx0{,}0467$, cần $m\ge6$.

Theo kì vọng, $\mathbb E_S\big[L_{D_f}(A_{\max}(S))\big]=0{,}2\,(0{,}8^m+0{,}6^m+0{,}4^m)\approx0{,}0227$ tại $m=10$ (Phụ lục C.2), trong khi $\mathbb E_S\big[L_S(A_{\max}(S))\big]=0$. Đọc theo các lần lấy mẫu lặp lại: ở $m=14$, khoảng $4{,}4\%$ các mẫu huấn luyện cho một hàm phân lớp có rủi ro kì vọng ít nhất $0{,}2$.

Các cỡ mẫu $14$ và $6$ chỉ đủ cho riêng $A_{\max}$ và riêng $D_f$, nên không phải $m_{A_{\max}}(\epsilon,\delta)$; chúng là khẳng định dạng "$\forall D\ \exists m$". Cỡ mẫu $m_0$ trong Định nghĩa 01.20 phải đúng cho mọi phân bố khả thực, còn các con số này thay đổi khi khối lượng xác suất của điểm $x=3$ thay đổi.
:::

Định nghĩa 01.18 và Ví dụ 01.9 xét trường hợp nhãn là hàm tất định của đầu vào. Dưới $D_\eta$, nhãn tại $x=2$ bằng $1$ với xác suất $\tfrac14$, nên không lớp nào khả thực với $D_\eta$, và Định nghĩa 01.18 không áp dụng được cho bài toán sàng lọc. Chúng ta cần bỏ giả thiết khả thực.

## 7. Học PAC bất khả tri và quy tắc Bayes

Dưới $D_\eta$, không hàm phân lớp nào có rủi ro nhỏ hơn $0{,}05$ (Nhận xét 01.17), nên yêu cầu $L_D(A(S))\le\epsilon$ không đạt được khi $\epsilon<0{,}05$. Đối tượng so sánh phải là một mức rủi ro dương, và mức thấp nhất có thể là đại lượng sau.

::: definition Định nghĩa 01.22 (Rủi ro Bayes)
Cho tập nhãn $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và một phân bố $D$ trên $\mathcal X\times\{0,1\}$. *Rủi ro Bayes* của $D$ là
$$
L_D^{\mathrm{Bayes}}=\inf_{g\in\mathcal M_{\mathcal X}}L_D(g).
$$
Với hàm lỗi $\ell_c$, cận dưới đúng $\inf_{g\in\mathcal M_{\mathcal X}}L^c_D(g)$ được gọi là rủi ro Bayes dưới $\ell_c$.
:::

Rủi ro Bayes là một đại lượng tổng thể của $D$, không phụ thuộc lớp $\mathcal H$ hay mẫu. Mệnh đề sau cho biết hàm nào đạt mức đó.

::: proposition Mệnh đề 01.23 (Quy tắc Bayes cho hàm lỗi 0–1 và hàm lỗi có trọng số) — đọc thêm
**Giả thiết.** $D$ là một phân bố trên $\mathcal X\times\{0,1\}$ với phân bố biên $D_{\mathcal X}$; $\eta:\mathcal X\to[0,1]$ là một hàm đo được với $\eta(X)=\Pr(Y=1\mid X)$ hầu chắc chắn (Phụ lục B chứng minh $\eta$ tồn tại). (T2), với (a) hàm lỗi 0–1 hoặc (b) hàm lỗi $\ell_c$, $c_{FP},c_{FN}>0$. Đối tượng so sánh là $\mathcal M_{\mathcal X}$, không giới hạn trong một lớp $\mathcal H$; không có mẫu.

**Bảo đảm.** (a) Hàm phân lớp tối ưu Bayes (Bayes optimal classifier) $h_{\mathrm{Bayes}}(x)=\mathbb 1[\eta(x)\ge\tfrac12]$ thuộc $\mathcal M_{\mathcal X}$ và $L_D(h_{\mathrm{Bayes}})\le L_D(g)$ với mọi $g\in\mathcal M_{\mathcal X}$, nên
$$
\begin{aligned}
&L_D^{\mathrm{Bayes}}\\
&\quad=L_D(h_{\mathrm{Bayes}})\\
&\quad=\mathbb E\min\{\eta(X),1-\eta(X)\}.
\end{aligned}
$$
(b) Dưới $\ell_c$, hàm $x\mapsto\mathbb 1\big[\eta(x)\ge c_{FP}/(c_{FP}+c_{FN})\big]$ có rủi ro nhỏ nhất trên $\mathcal M_{\mathcal X}$, bằng $\mathbb E\min\{c_{FN}\,\eta(X),\ c_{FP}(1-\eta(X))\}$. Nói chung hàm tối ưu không duy nhất. Khi $\eta(X)$ bằng ngưỡng với xác suất $0$, như dưới $D_\eta$, hàm tối ưu là duy nhất nếu bỏ qua một tập có xác suất $0$. Bảo đảm là về đại lượng tổng thể.
:::

Phát biểu của Mệnh đề 01.23 được dùng trong bài và trong bài tập; chứng minh là phần đọc thêm (Phụ lục B). Trong chứng minh, tại từng điểm $x$ ta chọn nhãn có rủi ro có điều kiện (conditional risk) nhỏ hơn, rồi lấy kì vọng bằng tính chất tháp. Dưới $\ell_c$, ngưỡng $\tfrac12$ chỉ đúng khi $c_{FP}=c_{FN}$; phần (b) trả lời câu hỏi thực hành của ứng dụng sàng lọc ở §3, với ngưỡng $c_{FP}/(c_{FP}+c_{FN})$ trên $\eta(x)$.

::: example Ví dụ 01.10 (Quy tắc Bayes trong ví dụ sàng lọc)
Xét phân bố $D_\eta$ của Ví dụ 01.1 và lớp sáu hàm ngưỡng; không có mẫu, mọi đại lượng cố định. Dưới hàm lỗi 0–1, $\eta(x)\ge\tfrac12$ đúng tại $x=3$ ($\eta=\tfrac34$) và $x=5$ ($\eta=1$), sai tại $x=4$ ($\eta=\tfrac25$). Do đó $h_{\mathrm{Bayes}}=\mathbb 1[x\in\{3,5\}]$, một hàm không phải hàm ngưỡng, và
$$
\begin{aligned}
&L_{D_\eta}^{\mathrm{Bayes}}\\
&\quad=0{,}2\Big(0+\tfrac14+\tfrac14+\tfrac25+0\Big)\\
&\quad=0{,}18 .
\end{aligned}
$$
Mức tốt nhất trong lớp là $\min_tL_{D_\eta}(h_t)=0{,}22$, cao hơn rủi ro Bayes $0{,}04$.

Dưới $\ell_c$ với $(c_{FP},c_{FN})=(1,4)$, ngưỡng là $\tfrac15$; vì $\eta(x)\ge\tfrac15$ tại $x\in\{2,3,4,5\}$, hàm Bayes dưới $\ell_c$ là $h_2\in\mathcal H$, với rủi ro $0{,}2\,(0+\tfrac34+\tfrac14+\tfrac35+0)=0{,}32$, bằng $\min_tL^c_{D_\eta}(h_t)$ ở Ví dụ 01.2. Lớp hàm ngưỡng chứa hàm Bayes dưới hàm lỗi có trọng số nhưng không chứa hàm Bayes dưới hàm lỗi 0–1.
:::

Hai đối tượng so sánh, $\inf_{h\in\mathcal H}L_D(h)$ và $L_D^{\mathrm{Bayes}}$, cho hai cách đo một hàm dự đoán tốt đến đâu.

::: definition Định nghĩa 01.24 (Rủi ro vượt mức)
Cho $D$, $\mathcal H$, $\ell$ và một hàm dự đoán $h$ với $L_D(h)<\infty$. *Rủi ro vượt mức* của $h$ so với $\mathcal H$ là $L_D(h)-\inf_{h'\in\mathcal H}L_D(h')$. Trong phân lớp, rủi ro vượt mức của $h$ so với rủi ro Bayes là $L_D(h)-L_D^{\mathrm{Bayes}}$.
:::

Rủi ro vượt mức luôn phải ghi so với đối tượng nào. Trong phân lớp, mọi rủi ro đều hữu hạn vì $\ell_{0\text{-}1}$ và $\ell_c$ bị chặn, và hai đại lượng liên hệ qua đẳng thức
$$
\begin{aligned}
&L_D(h)-L_D^{\mathrm{Bayes}}\\
&\quad=\Big[L_D(h)-\inf_{h'\in\mathcal H}L_D(h')\Big]\\
&\qquad+\Big[\inf_{h'\in\mathcal H}L_D(h')-L_D^{\mathrm{Bayes}}\Big],
\end{aligned}
$$
trong đó số hạng thứ hai chỉ phụ thuộc lớp đã chọn, không phụ thuộc $h$ (Bài 04 đặt tên cho hai số hạng). Dưới $D_\eta$, $h_2$ có rủi ro vượt mức $0{,}10$ so với $\mathcal H$ và $0{,}14$ so với rủi ro Bayes; số hạng thứ hai bằng $0{,}04$.

Đối tượng so sánh của định nghĩa tiếp theo là $\inf_{h\in\mathcal H}L_D(h)$, không phải $L_D^{\mathrm{Bayes}}$, vì ba lý do.

(i) Rủi ro của đầu ra một thuật toán học đúng lớp luôn ít nhất bằng $\inf_{h\in\mathcal H}L_D(h)$; hiệu $0{,}04$ của Ví dụ 01.10 không giảm khi $m$ tăng. (ii) Khi $\mathcal X$ vô hạn, không thuật toán nào bảo đảm được $L_D(A(S))\le L_D^{\mathrm{Bayes}}+\epsilon$ cho mọi $D$ với cỡ mẫu không phụ thuộc $D$, kể cả khi đầu ra được phép nằm ngoài $\mathcal H$ (UML §5.1). Khi $\mathcal X$ hữu hạn, như trong ví dụ sàng lọc, yêu cầu đó đạt được bằng ERM trên $\mathcal M_{\mathcal X}$ (Bài 02).

(iii) Vì vậy $\inf_{h\in\mathcal H}L_D(h)$ là đối tượng so sánh mạnh nhất cho một thuật toán đúng lớp, và trong định nghĩa sau, rủi ro của đầu ra phải tiến tới nó với cỡ mẫu không phụ thuộc phân bố. Giá phải trả là số hạng thứ hai của đẳng thức trên, tức giá của thiên kiến quy nạp.

::: definition Định nghĩa 01.25 (Học PAC bất khả tri)
Cho tập quan sát $\mathcal Z$, lớp giả thuyết $\mathcal H$ và hàm lỗi $\ell:\mathcal H\times\mathcal Z\to[0,\infty)$. Một thuật toán học $A$ được gọi là *thuật toán học PAC bất khả tri* cho $\mathcal H$ nếu tồn tại một hàm $M:(0,1)^2\to\mathbb N$ sao cho với mọi $\epsilon,\delta\in(0,1)$, mọi phân bố $D$ có rủi ro hữu hạn trên $\mathcal H$ (Định nghĩa 01.3) và mọi $m\ge M(\epsilon,\delta)$,
$$
\begin{aligned}
&\Pr_{S\sim D^m}\Big[L_D\big(A(S)\big)\\
&\quad\le\inf_{h\in\mathcal H}L_D(h)+\epsilon\Big]\ge1-\delta .
\end{aligned}
$$
Lớp $\mathcal H$ được gọi là *học được PAC bất khả tri* (agnostic PAC learnable) nếu tồn tại một thuật toán như vậy.
:::

Biến cố trong dấu $\Pr$ xảy ra khi rủi ro vượt mức của $A(S)$ so với $\mathcal H$ không quá $\epsilon$. Rủi ro vượt mức này là hiệu trong Định nghĩa 01.5. Định nghĩa 01.25 vì vậy làm chính xác mục tiêu của Định nghĩa 01.5 cho mọi phân bố có rủi ro hữu hạn, không cần giả thiết khả thực. Thứ tự lượng từ giống Định nghĩa 01.18, với "$(D,\mathcal H)$ khả thực" thay bằng "$D$ có rủi ro hữu hạn trên $\mathcal H$"; vì không đòi nhãn tất định, định nghĩa áp dụng được cho $D_\eta$. Độ phức tạp mẫu của Định nghĩa 01.20 mở rộng sang thiết lập này với họ phân bố và biến cố mới.

Với hàm lỗi không bị chặn, yêu cầu cho mọi phân bố có rủi ro hữu hạn nói chung không thỏa được; bảo đảm đều theo phân bố cần thêm giả thiết hàm lỗi bị chặn hoặc Lipschitz (Bài 05–06). Ví dụ 01.3 vì vậy chỉ minh họa định nghĩa rủi ro, không phải một lớp học được PAC bất khả tri.

::: remark Nhận xét 01.26 (Cận dưới đúng thay cho giá trị nhỏ nhất)
Trong Định nghĩa 01.25, ta viết $\inf$ vì giá trị nhỏ nhất có thể không tồn tại (Nhận xét 01.17), còn cận dưới đúng luôn tồn tại trong $[0,\infty)$; hai cách viết trùng nhau khi cận dưới đúng đạt được, như $\min_tL_{D_\eta}(h_t)=0{,}22$. Với hàm lỗi 0–1 và $(D,\mathcal H)$ khả thực, $\inf_{h\in\mathcal H}L_D(h)=0$ và biến cố của Định nghĩa 01.25 trùng với biến cố của Định nghĩa 01.18. Do đó mọi thuật toán học PAC bất khả tri cho $\mathcal H$ cũng là thuật toán học PAC cho $\mathcal H$ trong trường hợp khả thực, với cùng hàm $M$ (Bài tập 01.10).
:::

::: remark Nhận xét 01.27 (Học đúng lớp và học ngoài lớp)
Theo Định nghĩa 01.4, $A(S)\in\mathcal H$. Trong *học ngoài lớp* (improper learning, UML gọi là representation-independent learning), đầu ra được phép thuộc một lớp lớn hơn, còn đối tượng so sánh vẫn là $\inf_{h\in\mathcal H}L_D(h)$. Một thuật toán ngoài lớp có thể có rủi ro thấp hơn đối tượng so sánh: dưới $D_\eta$, hàm $\mathbb 1[x\in\{3,5\}]$ không thuộc lớp hàm ngưỡng và có rủi ro $0{,}18<0{,}22$.
:::

Hai định nghĩa học PAC trả lời câu hỏi học nghĩa là gì. Trong bài toán học thống kê của Định nghĩa 01.5, học là chọn từ mẫu $S\sim D^m$ một hàm dự đoán có rủi ro kì vọng không vượt quá $\inf_{h\in\mathcal H}L_D(h)+\epsilon$. Yêu cầu này phải đúng với xác suất ít nhất $1-\delta$ theo mẫu, khi $m$ vượt một ngưỡng không phụ thuộc phân bố. Rủi ro thực nghiệm không có mặt trong yêu cầu đó. Ứng viên tự nhiên là ERM, nhưng thuật toán ERM của Mệnh đề 01.15 không đạt yêu cầu này; chúng ta cần phát biểu điều đó bằng ngôn ngữ học PAC. Cỡ mẫu cần cho một lớp cụ thể là câu hỏi của Bài 02.

## 8. Giới hạn của rủi ro thực nghiệm

Để đọc Mệnh đề 01.15 bằng ngôn ngữ học PAC, chúng ta cần gọi tên loại cận mà nó bác bỏ: một cận cho khoảng cách tổng quát hóa, đúng cho mọi thuật toán ERM trên lớp.

::: definition Định nghĩa 01.28 (Cận tổng quát hóa cho mọi thuật toán ERM)
Cho tập đầu vào $\mathcal X$, tập nhãn $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và lớp giả thuyết $\mathcal H$. Một hàm $\beta:\mathbb N\times(0,1)\to[0,\infty)$ được gọi là *cận tổng quát hóa cho mọi thuật toán ERM* trên $\mathcal H$ nếu với mọi thuật toán ERM $\hat A$ trên $\mathcal H$, tức với mọi quy tắc chọn khi bằng nhau thỏa điều kiện đo được của Định nghĩa 01.4,
$$
\begin{aligned}
&\forall D\ \ \forall m\ge1\ \ \forall\delta\in(0,1):\\
&\Pr_{S\sim D^m}\Big[L_D\big(\hat A(S)\big)-L_S\big(\hat A(S)\big)\\
&\qquad\le\beta(m,\delta)\Big]\ge1-\delta ,
\end{aligned}
$$
trong đó $D$ chạy trên mọi phân bố trên $\mathcal X\times\mathcal Y$.
:::

Hàm $\beta(m,\delta)$ chặn trên khoảng cách tổng quát hóa $L_D(\hat A(S))-L_S(\hat A(S))$ với xác suất ít nhất $1-\delta$, chung cho mọi thuật toán ERM và mọi phân bố. Cận tầm thường $\beta\equiv1$ luôn thỏa, vì $L_D\le1$ với hàm lỗi 0–1.

::: corollary Hệ quả 01.29 (Rủi ro thực nghiệm nhỏ không đủ làm bảo đảm học) — chứng minh đầy đủ
**Giả thiết.** Thiết lập của Ví dụ 01.8 ($\mathcal X=[0,1]$, hàm lỗi 0–1, $\mathcal H=\mathcal M_{\mathcal X}$), với (T1): $S\sim D^m$. (O1): các thuật toán được xét là thuật toán ERM chính xác, thỏa điều kiện đo được của Định nghĩa 01.4. Phần (b) dùng tính khả thực (Định nghĩa 01.16) của $(D,\mathcal M_{\mathcal X})$, có từ Mệnh đề 01.15(c); $\beta$ theo Định nghĩa 01.28.

**Bảo đảm.** (a) Mọi cận tổng quát hóa cho mọi thuật toán ERM trên $\mathcal M_{\mathcal X}$ thỏa $\beta(m,\delta)\ge1$ với mọi $m$, $\delta$; do đó với mỗi $\delta\in(0,1)$, $\beta(m,\delta)$ không tiến về $0$ khi $m\to\infty$. (b) Dưới phân bố khả thực $D$ của Ví dụ 01.8, $\Pr_S\big[L_D(A_{\mathrm{gn}}(S))\le\epsilon\big]=0$ với mọi $\epsilon\in(0,1)$ và mọi $m$, nên $A_{\mathrm{gn}}$ không là thuật toán học PAC cho $\mathcal M_{\mathcal X}$, và theo Nhận xét 01.26 cũng không là thuật toán học PAC bất khả tri.

Lớp $\mathcal M_{\mathcal X}$ với $\mathcal X=[0,1]$ không học được PAC, nhưng để chứng minh điều đó, ta phải lập luận cho mọi thuật toán (UML §5.1; Bài 03).
:::

::: proof Chứng minh Hệ quả 01.29
**Lộ trình.** Áp dụng Mệnh đề 01.15 và đọc xác suất của một biến cố tất định.

**Bước 1 (phần a).** Theo Mệnh đề 01.15(a) và Phụ lục A(iii), $A_{\mathrm{gn}}$ là một thuật toán ERM đo được, nên Định nghĩa 01.28 áp dụng cho $\hat A=A_{\mathrm{gn}}$. Theo Mệnh đề 01.15(a)(b), khoảng cách tổng quát hóa bằng $1-0=1$ trên mọi mẫu, nên biến cố trong Định nghĩa 01.28 là $\{1\le\beta(m,\delta)\}$, không phụ thuộc $S$, và
$$
\begin{aligned}
&\Pr_{S\sim D^m}\big[1\le\beta(m,\delta)\big]\\
&\quad=\mathbb 1\big[\beta(m,\delta)\ge1\big].
\end{aligned}
$$
Vì $1-\delta>0$, xác suất này ít nhất bằng $1-\delta$ chỉ khi $\beta(m,\delta)\ge1$.

**Bước 2 (phần b).** Theo Mệnh đề 01.15(c), $(D,\mathcal M_{\mathcal X})$ khả thực với $h^\star=h_{\equiv1}$. Theo Mệnh đề 01.15(b), $L_D(A_{\mathrm{gn}}(S))=1>\epsilon$ với mọi $S$ và mọi $\epsilon<1$, nên xác suất thành công bằng $0<1-\delta$ với mọi $m$, và $m_{A_{\mathrm{gn}}}(\epsilon,\delta)=\infty$.

Hai giả thiết của Mệnh đề 01.15 được dùng: lớp chứa hàm phân lớp ghi nhớ qua phần (a), và $D_{\mathcal X}$ không có nguyên tử qua phần (b).

$\square$ Một bảo đảm học phải dùng cấu trúc của lớp (Bài 02–03) hoặc tính chất của một thuật toán cụ thể (Bài 06, 08); chỉ biết $L_S$ nhỏ thì chưa đủ.
:::

Trong ví dụ sau, ta bỏ giả thiết không có nguyên tử của Mệnh đề 01.15(b) và giữ nguyên nhãn hằng cùng thuật toán ghi nhớ.

::: example Ví dụ 01.11 (Hàm phân lớp ghi nhớ khi phân bố có nguyên tử)
Lấy $\mathcal X=\{1,\ldots,5\}$, phân bố $D_1$ của Nhận xét 01.21 ($D_{\mathcal X}$ đều, $Y=1$ chắc chắn), lớp $\mathcal M_{\mathcal X}$ gồm cả $32$ hàm $\mathcal X\to\{0,1\}$, hàm lỗi 0–1, mẫu ngẫu nhiên $S\sim D_1^m$ và thuật toán $A_{\mathrm{gn}}$. So với Ví dụ 01.8, chỉ có một thay đổi: mỗi điểm của $\mathcal X$ là một nguyên tử. Theo Bước 2 của chứng minh Mệnh đề 01.15, $A_{\mathrm{gn}}(S)$ là một nghiệm ERM; nó sai đúng tại các điểm chưa xuất hiện trong mẫu, mỗi điểm vắng mặt với xác suất $0{,}8^m$, nên theo tính tuyến tính của kì vọng
$$
\begin{aligned}
&\mathbb E_S\big[L_{D_1}(A_{\mathrm{gn}}(S))\big]\\
&\quad=5\cdot0{,}2\cdot0{,}8^m\\
&\quad=0{,}8^m .
\end{aligned}
$$
Tại $m=10$, giá trị này bằng $0{,}8^{10}\approx0{,}107$, và nó tiến về $0$ khi $m\to\infty$ (Phụ lục C.3). Kết luận rủi ro bằng $1$ của Mệnh đề 01.15(b) vì vậy cần giả thiết không có nguyên tử.
:::

::: remark Nhận xét 01.30 (Phản ví dụ ghi nhớ và định lý không có bữa trưa miễn phí)
Định lý không có bữa trưa miễn phí (no-free-lunch theorem, UML §5.1) khẳng định: với mỗi thuật toán, tồn tại một phân bố làm thuật toán thất bại khi cỡ mẫu nhỏ so với $\lvert\mathcal X\rvert$, dù phân bố đó khả thực bởi một hàm gán nhãn $f$. Mệnh đề 01.15 chỉ xét một thuật toán ERM và một phân bố. Dưới phân bố đó, hàm hằng $1$ cũng là nghiệm ERM với rủi ro $0$, nên Mệnh đề 01.15 không chứng minh định lý không có bữa trưa miễn phí.
:::

Vì $\hat h$ được chọn theo $S$ (Nhận xét 01.9), một bảo đảm cho ERM cần kiểm soát $L_S(h)-L_D(h)$ đồng thời cho mọi $h\in\mathcal H$.

## 9. Ý nghĩa, tác động và giới hạn

Phát biểu "lớp $\mathcal H$ học được PAC" là bảo đảm cho lớp: nó chỉ nói tồn tại một thuật toán. Phát biểu "$A$ là thuật toán học PAC cho $\mathcal H$" là bảo đảm cho một thuật toán cụ thể, và chỉ nó cho biết nên chạy thuật toán nào.

Định nghĩa học PAC không bảo đảm gì về một dự đoán riêng lẻ (Nhận xét 01.19) và không so với rủi ro Bayes: hiệu $0{,}04$ dưới $D_\eta$ không giảm khi tăng $m$. Nó không nói về thời gian tính và không áp dụng khi các quan sát không độc lập cùng phân bố.

Từ các định nghĩa của bài, ta rút ra vài quyết định thực hành. Hàm lỗi phải chọn theo chi phí thật của từng loại lỗi, với ngưỡng tối ưu $c_{FP}/(c_{FP}+c_{FN})$ trên $\eta(x)$, và lớp $\mathcal H$ phải cố định trước khi xem dữ liệu. Rủi ro của $\hat h$ được ước lượng trên một mẫu độc lập (Nhận xét 01.9). Quy tắc chọn khi bằng nhau cần được ghi lại, vì trên $S_\eta$ nó đổi rủi ro kì vọng dưới $D_\eta$ giữa $0{,}22$ và $0{,}32$.

Bài tập 01.9 chứng minh cận cỡ mẫu $\lceil\ln(1/\delta)/\epsilon\rceil$ cho lớp hình tròn đồng tâm. Cùng lập luận, áp dụng cho lớp hàm ngưỡng với $A_{\max}$, cho thấy $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$ đủ cho mọi phân bố khả thực; khi $\epsilon=0{,}1$, $\delta=0{,}05$, điều kiện này là $m\ge\lceil10\ln20\rceil=30$.

## 10. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 01](material-viewer.html?doc=materials/lec-01/exercises.md). Năm bài đầu là bài gốc, sáu bài sau chọn từ UML; mỗi dòng ghi mục tiêu học tập mà bài kiểm tra.

1. **Bài tập 01.1** (Thiết lập bài toán học cho lọc thư rác và dự báo nhiệt độ): mục tiêu 1.
2. **Bài tập 01.2** (Hai nghiệm ERM, quy tắc Bayes và rủi ro vượt mức): mục tiêu 2.
3. **Bài tập 01.3** (Tính không chệch và giả thuyết chọn theo mẫu): mục tiêu 3.
4. **Bài tập 01.4** (Hàm phân lớp ghi nhớ và hai rủi ro): mục tiêu 5.
5. **Bài tập 01.5** (Định nghĩa học PAC với đủ lượng từ): mục tiêu 4.
6. **Bài tập 01.6** (Hàm phân lớp ghi nhớ là một đa thức có ngưỡng; UML Bài tập 2.1): mục tiêu 5.
7. **Bài tập 01.7** (Tính đơn điệu của độ phức tạp mẫu; UML Bài tập 3.1): mục tiêu 4.
8. **Bài tập 01.8** (Lớp hàm chỉ thị của một điểm; UML Bài tập 3.2): mục tiêu 4.
9. **Bài tập 01.9** (Lớp hình tròn đồng tâm và lớp hàm ngưỡng; UML Bài tập 3.3): mục tiêu 4.
10. **Bài tập 01.10** (Học PAC bất khả tri kéo theo học PAC khả thực; UML Bài tập 3.6): mục tiêu 4.
11. **Bài tập 01.11** (Tính tối ưu của quy tắc Bayes và so sánh thuật toán; UML Bài tập 3.8, thử thách): mục tiêu 2.

## 11. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Trong $L_D(A(S))$, phân bố $D$ cố định. Đại lượng nào ngẫu nhiên, và ngẫu nhiên theo phân bố nào?

**Câu hỏi phụ.** (1) Trên mẫu $S_\eta$, nghiệm ERM trên lớp hàm ngưỡng có rủi ro kì vọng dưới $D_\eta$ bằng bao nhiêu? (2) Với $\delta=0{,}05$, có thể nói hàm phân lớp vừa học đúng với xác suất $95\%$ không?

::: solution Lời giải câu hỏi cuối buổi
Hàm học được $A(S)$ là ngẫu nhiên, vì nó là hàm của mẫu $S\sim D^m$. Do đó $L_D(A(S))$ là một biến ngẫu nhiên theo $D^m$; đây là dòng thứ hai của bảng ở §1.

(1) Tùy quy tắc chọn khi bằng nhau: $0{,}32$ nếu chọn $h_2$ (như $A_{\min}$), $0{,}22$ nếu chọn $h_3$, $0{,}28$ nếu chọn $h_5$ (như $A_{\max}$); xem Ví dụ 01.6. (2) Không. Số $0{,}95$ là xác suất, theo các lần lấy mẫu lặp lại, để rủi ro kì vọng của hàm học được không quá $\epsilon$. Nó không phải xác suất một dự đoán cụ thể đúng, cũng không phải xác suất hậu nghiệm (Nhận xét 01.19).
:::

Hai hàm $h_3$ và $h_4$ của câu hỏi mở đầu chỉ khác nhau tại $x=3$, và $S_f$ không chứa $x=3$; trên $S_f$, $A_{\min}$ chọn $h_3$ (rủi ro $0$), còn $A_{\max}$ chọn $h_4$ (rủi ro $0{,}2$). Mẫu $S_f$ cũng có thể đến từ phân bố có hàm gán nhãn $h_4$, và mọi hàm phân lớp có rủi ro ít nhất $0{,}2$ dưới một trong hai phân bố. Vì vậy, trên $S_f$, không thuật toán tất định nào trả về được một hàm có rủi ro $0$ dưới cả hai phân bố. Trong học PAC, chỉ cần xác suất gặp những mẫu như $S_f$ đủ nhỏ, với một ngưỡng cỡ mẫu chung cho mọi phân bố. Với $A_{\max}$ dưới $D_f$, xác suất đó là $0{,}8^m\le0{,}05$ khi $m\ge14$ (Ví dụ 01.9); với thuật toán ghi nhớ trên lớp của Ví dụ 01.8, không cỡ mẫu nào đủ.

Trong Ví dụ 01.9, ta tính được $\Pr[L_{D_f}(A_{\max}(S))>0]$ vì đã biết $D_f$. Khi $D$ chưa biết, chúng ta cần chặn $\Pr\big(\lvert L_S(h)-L_D(h)\rvert>\epsilon\big)$ cho từng $h$ cố định; cận của Bài 02 dùng giả thiết các quan sát độc lập và hàm lỗi bị chặn. Câu hỏi cho Bài 02 là: khi $\mathcal H$ hữu hạn và $D$ chưa biết, cần bao nhiêu quan sát để $L_S$ nằm trong khoảng $\epsilon$ quanh $L_D$ với xác suất ít nhất $1-\delta$? Bài 02 trả lời câu hỏi này trước cho một giả thuyết cố định, rồi cho nghiệm ERM chọn từ $\lvert\mathcal H\rvert$ ứng viên. Công cụ là bất đẳng thức Hoeffding và bất đẳng thức hợp.

## 12. Tài liệu đọc

- **Trước buổi học:** UML §§2.1–2.2 (mô hình học, ERM, quá khớp).
- **Sau buổi học:** UML §2.3 (thiên kiến quy nạp; §2.3.1 là phần mở đầu của Bài 02), §§3.1–3.2 (học PAC, học PAC bất khả tri, hàm lỗi tổng quát); các bài tập UML §2.4 và §3.5 đã chọn ở §10.
- **Mở rộng:** UML §5.1 (định lý không có bữa trưa miễn phí; Nhận xét 01.30).

**Quan hệ với giáo trình UML.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục. UML Chương 2 viết $L_{(D,f)}(h)$ cho nhãn tất định $Y=f(X)$; ở đây $D$ là phân bố đồng thời ngay từ đầu. Các khác biệt còn lại: $\inf$ thay cho $\min$; ERM xấp xỉ, không có trong UML Chương 2–3. Ở đây, bảo đảm học PAC bất khả tri chỉ cần đúng cho phân bố có rủi ro hữu hạn, trong khi UML §3.2.2 lấy mọi phân bố. Hai điểm cuối là tính đo được đồng thời (Phụ lục A) và phép so sánh với xác suất hậu nghiệm (Nhận xét 01.19).

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
đo được trên $\mathcal Z^m$. Do đó $L_D(A(S))$ là một biến ngẫu nhiên với giá trị trong $[0,\infty]$, và các biến cố trong Định nghĩa 01.18 và 01.25 có xác suất. UML chỉ đòi từng $\ell(h,\cdot)$ đo được. Điều kiện đó không đủ: khi $h=A(S)$ thay đổi theo mẫu, cần tính đo được đồng thời theo mẫu và theo quan sát.

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
A_{\mathrm{gn}}(s)(x)
&=\mathbb 1\big[c(s,x)\ge1\big]\\
&\quad\cdot\mathbb 1\big[v(s,x)\ge0\big],
\end{aligned}
$$
nên $(s,x)\mapsto A_{\mathrm{gn}}(s)(x)$ đo được, và $(s,(x,y))\mapsto\mathbb 1[A_{\mathrm{gn}}(s)(x)\ne y]$ đo được. Thuật toán $A_{\mathrm{gn}}$ vì vậy thỏa điều kiện của Định nghĩa 01.4.

**(iv) Tập đầu vào hữu hạn.** Khi $\mathcal X$ hữu hạn, $\mathcal Y=\{0,1\}$ và mọi tập con đều đo được, mọi hàm trên $\mathcal Z^m\times\mathcal Z$ đo được, và lớp $\mathcal H$ hữu hạn. Khi đó $\ell(A_m(s),z)=\sum_{h\in\mathcal H}\mathbb 1[A_m(s)=h]\,\ell(h,z)$, nên điều kiện của Định nghĩa 01.4 tự thỏa. Đây là trường hợp của ví dụ sàng lọc.

**(v) Lớp vô hạn.** Với một lớp vô hạn tổng quát, các đại lượng dạng $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$, cần cho hội tụ đều (uniform convergence), có thể không đo được. Mỗi khi dùng các đại lượng này, Bài 02–03 nêu rõ giả thiết đo được.

### B. Quy tắc Bayes

Chứng minh Mệnh đề 01.23 cần kì vọng có điều kiện và tính chất tháp; các tính chất của $h_{\mathrm{Bayes}}$ suy ra từ cùng phép tính.

::: proof Chứng minh Mệnh đề 01.23
**Lộ trình.** Tính rủi ro có điều kiện tại $X=x$, tối thiểu hóa nó tại từng điểm bằng cách so sánh hai lựa chọn $0$ và $1$, rồi lấy kì vọng theo $D_{\mathcal X}$ bằng tính chất tháp.

**Bước 1 (rủi ro có điều kiện).** Cho $g\in\mathcal M_{\mathcal X}$. Lỗi 0–1 của $g$ viết được thành $\mathbb 1[Y=1]\,\mathbb 1[g(X)=0]+\mathbb 1[Y=0]\,\mathbb 1[g(X)=1]$. Vì $g(X)$ là hàm đo được của $X$, các thừa số chứa $g(X)$ được đưa ra ngoài kì vọng có điều kiện theo $X$, nên hầu chắc chắn
$$
\begin{aligned}
&\mathbb E\big[\mathbb 1[g(X)\ne Y]\mid X\big]\\
&=\mathbb 1[g(X)=0]\,\Pr(Y=1\mid X)\\
&\quad+\mathbb 1[g(X)=1]\,\Pr(Y=0\mid X)\\
&=\eta(X)\,\mathbb 1[g(X)=0]\\
&\quad+\big(1-\eta(X)\big)\,\mathbb 1[g(X)=1].
\end{aligned}
$$
Định nghĩa của $\eta$ và tính đo được của $g$ được dùng ở đây.

**Bước 2 (tối thiểu hóa từng điểm).** Tại mỗi $x$, vế phải bằng $\eta(x)$ nếu $g(x)=0$ và bằng $1-\eta(x)$ nếu $g(x)=1$, nên nó không nhỏ hơn $\min\{\eta(x),1-\eta(x)\}$. Dấu bằng xảy ra khi $g(x)=1$ đúng lúc $\eta(x)\ge\tfrac12$ (khi $\eta(x)=\tfrac12$ hai lựa chọn bằng nhau), chẳng hạn khi $g=h_{\mathrm{Bayes}}$. Tập $\{x:\eta(x)\ge\tfrac12\}$ đo được vì $\eta$ đo được, nên $h_{\mathrm{Bayes}}\in\mathcal M_{\mathcal X}$.

**Bước 3 (lấy kì vọng).** Theo tính chất tháp và Bước 2,
$$
\begin{aligned}
&L_D(g)\\
&\quad=\mathbb E\Big[\mathbb E\big[\mathbb 1[g(X)\ne Y]\mid X\big]\Big]\\
&\quad\ge\mathbb E\min\{\eta(X),1-\eta(X)\}\\
&\quad=L_D(h_{\mathrm{Bayes}}).
\end{aligned}
$$
Lấy cận dưới đúng theo $g$ cho đẳng thức của phần (a).

**Bước 4 (hàm lỗi có trọng số).** Với $\ell_c$, cùng lập luận cho rủi ro có điều kiện $c_{FN}\,\eta(X)\,\mathbb 1[g(X)=0]+c_{FP}\,(1-\eta(X))\,\mathbb 1[g(X)=1]$. Dự đoán $1$ tại $x$ không tệ hơn dự đoán $0$ khi và chỉ khi
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

**Rủi ro Bayes.** Theo Mệnh đề 01.23(a), rủi ro Bayes bằng $0$ khi và chỉ khi $\eta(X)\in\{0,1\}$ hầu chắc chắn, tức nhãn là hàm tất định của đầu vào. Nếu $\eta(X)\in(0,1)$ trên một biến cố có xác suất dương, rủi ro Bayes dương và không cặp $(D,\mathcal H)$ nào khả thực, như với $D_\eta$.

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

**C.2 Kì vọng theo mẫu của rủi ro kì vọng của $A_{\max}$ dưới $D_f$.** Đặt $N=\hat t-3\in\{0,1,2,3\}$, nên $L_{D_f}(A_{\max}(S))=0{,}2N$. Vì $N=\sum_{k=1}^3\mathbb 1[N\ge k]$ (mỗi $k\le N$ đóng góp một đơn vị), tính tuyến tính của kì vọng cho $\mathbb EN=\sum_{k=1}^3\Pr(N\ge k)$. Biến cố $N\ge k$ xảy ra khi và chỉ khi không quan sát nào của $S$ rơi vào $\{3,\ldots,2+k\}$, một tập có khối lượng $0{,}2k$, nên $\Pr(N\ge k)=(1-0{,}2k)^m$ với $k=1,2,3$. Do đó
$$
\begin{aligned}
&\mathbb E_S\big[L_{D_f}(A_{\max}(S))\big]\\
&\quad=0{,}2\,\big(0{,}8^m+0{,}6^m+0{,}4^m\big).
\end{aligned}
$$
Tại $m=10$: $0{,}8^{10}\approx0{,}10737$, $0{,}6^{10}\approx0{,}00605$, $0{,}4^{10}\approx0{,}00010$, tổng $\approx0{,}11353$, nhân $0{,}2$ được $\approx0{,}0227$. Cùng lập luận cho $\Pr[L_{D_f}(A_{\max}(S))>0]=\Pr(N\ge1)=0{,}8^m$ và $\Pr[L_{D_f}(A_{\max}(S))>0{,}25]=\Pr(N\ge2)=0{,}6^m$ của Ví dụ 01.9. Rủi ro thực nghiệm $L_S(A_{\max}(S))=0$ với mọi mẫu rút từ $D_f$, vì mọi quan sát âm nằm ở $\{1,2\}$, dưới mọi quan sát dương.

**C.3 Hàm phân lớp ghi nhớ trên tập đầu vào hữu hạn.** Dưới $D_1$ (nhãn hằng $1$), $A_{\mathrm{gn}}(S)$ sai tại $x$ khi và chỉ khi $x$ không xuất hiện trong $S$, nên $L_{D_1}(A_{\mathrm{gn}}(S))=0{,}2\sum_{x=1}^5\mathbb 1[x\notin S]$. Mỗi chỉ thị có kì vọng $0{,}8^m$, nên kì vọng của rủi ro bằng $5\cdot0{,}2\cdot0{,}8^m=0{,}8^m$; tại $m=10$, $0{,}8^{10}=0{,}1073741824\approx0{,}107$. Dưới $D_f$, hàm phân lớp ghi nhớ chỉ sai tại các điểm dương $x\in\{3,4,5\}$ chưa xuất hiện, nên cùng lập luận cho kì vọng $0{,}6\cdot0{,}8^m\approx0{,}0644$ tại $m=10$. Giá trị này giảm cùng tốc độ $0{,}8^m$ với $0{,}0227$ của $A_{\max}$ trên lớp hàm ngưỡng (C.2), nhưng hệ số của $0{,}8^m$ lớn gấp ba.

**C.4 Giá trị dự đoán dương không phải một rủi ro.** Với $h$ và $\ell$ cố định, rủi ro dưới hỗn hợp $\lambda P_1+(1-\lambda)P_2$ bằng $\lambda L_{P_1}(h)+(1-\lambda)L_{P_2}(h)$. Giá trị dự đoán dương là tỉ số $\mathbb E\big[Y\,\mathbb 1[h(X)=1]\big]/\Pr(h(X)=1)$ và không có tính chất này. Lấy $P_1$ với $h(X)=1$ và $Y=1$ chắc chắn (giá trị dự đoán dương bằng $1$), và $P_2$ với $\Pr(h(X)=1)=\tfrac12$, $Y=0$ chắc chắn (bằng $0$). Dưới hỗn hợp đều, tử số bằng $\tfrac12$ và mẫu số bằng $\tfrac34$, nên giá trị dự đoán dương bằng $\tfrac23\ne\tfrac12$. Nếu nó bằng $L_D(h)$ với một hàm lỗi $\ell$ không phụ thuộc $D$, nó phải afin theo $D$, mâu thuẫn. Nó còn không xác định khi $\Pr(h(X)=1)=0$.
