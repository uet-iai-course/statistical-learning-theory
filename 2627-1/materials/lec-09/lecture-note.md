# Bài 09 — Học chuỗi và mô hình sinh

Ở Bài 01–08, mỗi quan sát là một điểm $z$, thường là một cặp $(x,y)$; hàm lỗi logistic là hàm lỗi log (log loss; Nhận xét 01.2) của một mô hình xác suất có điều kiện cho nhãn. *Độ hợp lý* (likelihood) của một chuỗi là xác suất mà mô hình gán cho cả chuỗi. Khi mỗi quan sát là một chuỗi có các phần tử phụ thuộc nhau và hàm lỗi là $-\ln$ độ hợp lý, chúng ta cần viết lại rủi ro kì vọng, rủi ro thực nghiệm và giả thiết độc lập (câu hỏi cuối Bài 08).

Câu hỏi trung tâm của bài là học một phân bố xác suất và học một chuỗi như thế nào. Các công cụ là ước lượng hợp lý cực đại (maximum likelihood estimation, MLE), phân tích tự hồi quy (autoregressive factorization), entropy và phân kì Kullback–Leibler (Kullback–Leibler divergence, KL), cận dưới bằng chứng (evidence lower bound, ELBO) và tái tham số hóa (reparameterization). Mạng nơ-ron hồi tiếp (recurrent neural network) và Transformer chỉ là ví dụ về cách tham số hóa một mô hình tự hồi quy; huấn luyện các kiến trúc này và các mô hình sinh (generative model) không dùng độ hợp lý nằm ngoài bài.

## Câu hỏi mở đầu

Một mô hình phân lớp nhận một hồ sơ và trả về xác suất $0{,}8$ cho nhãn $1$. Nhãn quan sát được là $1$, nên hàm lỗi log của mô hình trên hồ sơ này là $-\ln0{,}8\approx0{,}223$.

Một mô hình sinh chuỗi trên hai kí tự (token) $\mathtt A$, $\mathtt B$ tạo chuỗi ba kí tự như sau: rút kí tự đầu, rồi rút mỗi kí tự tiếp theo theo kí tự đứng ngay trước nó, với các xác suất trong bảng.

| Kí tự đứng trước | Rút $\mathtt A$ | Rút $\mathtt B$ |
|---|---|---|
| (đầu chuỗi) | $3/5$ | $2/5$ |
| $\mathtt A$ | $3/10$ | $7/10$ |
| $\mathtt B$ | $3/5$ | $2/5$ |

Mô hình tạo chuỗi $\mathtt{ABB}$ với xác suất $\tfrac35\cdot\tfrac7{10}\cdot\tfrac25=\tfrac{21}{125}=0{,}168$. Lấy $-\ln$, ta được
$$
\begin{aligned}
-\ln0{,}168&\approx1{,}784\\
&=0{,}511+0{,}357+0{,}916,
\end{aligned}
$$
tổng của ba hàm lỗi log; mỗi số hạng ứng với một lần dự đoán kí tự kế tiếp từ các kí tự đứng trước.

**Câu hỏi.** Huấn luyện mô hình sinh chuỗi trên $m$ chuỗi ba kí tự có phải là huấn luyện một mô hình phân lớp trên $3m$ quan sát độc lập không? Nếu không, quan sát độc lập là gì, và mô hình sinh chuỗi cần làm nhỏ rủi ro kì vọng nào?

Đẳng thức "$-\ln$ của xác suất của chuỗi bằng tổng các hàm lỗi log theo từng kí tự" đúng với mọi phân bố (§5). Tuy nhiên, theo bảng, xác suất rút $\mathtt B$ ở vị trí thứ ba bằng $0{,}7$ sau $\mathtt A$ và $0{,}4$ sau $\mathtt B$, mà kí tự thứ hai là ngẫu nhiên. Vì vậy ba số hạng không độc lập, và quan sát độc lập là cả chuỗi (§1).

Cả hai mô hình dự đoán một phân bố có điều kiện và được đánh giá bằng hàm lỗi log; sinh một chuỗi là lặp lại phép dự đoán đó. Rủi ro kì vọng cần làm nhỏ là kì vọng của $-\ln$ xác suất mà mô hình gán cho cả chuỗi; ở §7, ta tách nó thành một đại lượng chỉ phụ thuộc phân bố thật cộng một số không âm, bằng $0$ chỉ khi mô hình trùng phân bố thật.

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Phân tích xác suất của một chuỗi thành tích các xác suất có điều kiện, rồi tính độ hợp lý, hàm lỗi log trung bình theo kí tự và độ bối rối từ một bảng xác suất.
2. Viết ước lượng hợp lý cực đại dưới dạng tối thiểu hóa rủi ro thực nghiệm với hàm lỗi log, chứng minh rằng rủi ro kì vọng với hàm lỗi này bằng entropy cộng phân kì Kullback–Leibler, và nêu các điều kiện về giá và về tính hữu hạn.
3. Phân biệt tính độc lập giữa các chuỗi với sự phụ thuộc giữa các kí tự trong một chuỗi, chỉ ra vì sao chia ngẫu nhiên các cửa sổ chồng lấn làm rò rỉ thông tin, và so sánh hàm lỗi tổng với hàm lỗi chuẩn hóa theo độ dài.
4. Chứng minh đồng nhất thức của cận dưới bằng chứng cùng điều kiện dấu bằng, và tách cận này thành số hạng tái tạo và phân kì Kullback–Leibler trên một mô hình Gauss.
5. Dẫn ra ước lượng gradient theo đường đi bằng tái tham số hóa, kiểm tra điều kiện cho phép đổi chỗ đạo hàm và kì vọng, và chỉ ra một trường hợp ước lượng này bị chệch.

## Kiến thức tiên quyết

- **Từ Bài 01.** (T1) dạng yếu và dạng đầy đủ, (T2); hàm lỗi và rủi ro kì vọng (Định nghĩa 01.1); hàm lỗi log, tính khả tích (Nhận xét 01.2); rủi ro thực nghiệm (Định nghĩa 01.6) và tính không chệch của nó (Mệnh đề 01.7); tối thiểu hóa rủi ro thực nghiệm (Định nghĩa 01.8); khoảng cách tổng quát hóa (Định nghĩa 01.10); thuật toán ghi nhớ (Định nghĩa 01.14); rủi ro vượt mức (Định nghĩa 01.24).
- **Từ Bài 02.** Bất đẳng thức Hoeffding (Định lý 02.7) và (T3) (đoạn sau Nhận xét 02.8); một quan sát chép lại $m$ lần (Ví dụ 02.6); cận tin cậy Hoeffding cho một giả thuyết cố định (Hệ quả 02.10); hàm lỗi không bị chặn (Nhận xét 02.11).
- **Từ Bài 04.** Mẫu xác thực độc lập (T7) (đoạn trước Hệ quả 04.17).
- **Từ Bài 05.** Oracle gradient ngẫu nhiên, (G1), (G2) (Định nghĩa 05.10); giả thiết (C) và cận kì vọng cho hạ gradient ngẫu nhiên có chiếu (Định lý 05.14).
- **Từ Bài 07.** Hàm lỗi logistic bị chặn trên lớp bị chặn theo chuẩn (Ví dụ 07.11, Bước 4).
- **Xác suất và giải tích.** Công thức xác suất toàn phần, công thức Bayes; tổng hai biến Gauss độc lập; mô-men $\mathbb E\zeta^2=1$, $\mathbb E\zeta^4=3$, $\mathbb E\zeta^6=15$ của $\zeta\sim N(0,1)$; $\ln t\le t-1$; định lý giá trị trung bình; định lý hội tụ bị chặn (dominated convergence theorem).

**Câu hỏi ôn nhanh.**

1. Với $\delta=0{,}05$ và $m=50$, tính bán kính $\sqrt{\ln(2/\delta)/(2m)}$ của khoảng tin cậy trong Hệ quả 02.10(b). Giả thiết nào của hệ quả không thỏa trong Ví dụ 02.6?
2. Chứng minh $\ln t\le t-1$ với mọi $t>0$, dấu bằng chỉ khi $t=1$.
3. Một biến ngẫu nhiên không quan sát được $v\in\{1,2\}$ có $\Pr(v=1)=\Pr(v=2)=\tfrac12$; một biến cố $x$ có $\Pr(x\mid v=1)=0{,}2$ và $\Pr(x\mid v=2)=0{,}6$. Tính $\Pr(x)$ và $\Pr(v=2\mid x)$.

::: solution Lời giải câu hỏi ôn nhanh
1. Với $\delta=0{,}05$ và $2m=100$, bán kính là $\sqrt{\ln40/100}\approx\sqrt{0{,}036889}\le0{,}1921$. Ví dụ 02.6 giữ dạng yếu của (T1), mỗi quan sát có phân bố $D$, nhưng bỏ tính độc lập; Hệ quả 02.10 cần dạng đầy đủ.
2. Đặt $g(t)=t-1-\ln t$ trên $(0,\infty)$. Đạo hàm $g'(t)=1-1/t$ âm trên $(0,1)$ và dương trên $(1,\infty)$. Do đó $g$ giảm ngặt rồi tăng ngặt, có giá trị nhỏ nhất duy nhất $g(1)=0$, nên $g(t)\ge0$ và dấu bằng chỉ khi $t=1$.
3. Theo công thức xác suất toàn phần,
$$
\begin{aligned}
\Pr(x)&=\tfrac12\cdot0{,}2+\tfrac12\cdot0{,}6\\
&=0{,}4 .
\end{aligned}
$$
Theo công thức Bayes, $\Pr(v=2\mid x)=\tfrac12\cdot0{,}6/0{,}4=0{,}75$.
:::

## 1. Thiết lập bài toán

Bài toán có bảy thành phần. Khác Bài 01–08, quan sát không có nhãn, và mô hình trả về một phân bố xác suất thay cho một nhãn.

1. **Dữ liệu.** Một *bảng chữ* (alphabet) hữu hạn $\mathcal A$, các phần tử gọi là kí tự. Một chuỗi độ dài $n$ là $x_{1:n}=(x_1,\ldots,x_n)\in\mathcal A^n$; $x_{<j}=x_{1:j-1}$ là tiền tố đứng trước vị trí $j$, rỗng khi $j=1$. Tập quan sát $\mathcal X$ là $\mathcal A^n$ khi độ dài cố định, hoặc tập mọi chuỗi hữu hạn khi độ dài thay đổi; cả hai đều đếm được. Ở §8–§9, $\mathcal X\subseteq\mathbb R^p$; không có nhãn, $\mathcal Z=\mathcal X$.
2. **Cơ chế lấy mẫu.** Mẫu $S=(X^{(1)},\ldots,X^{(m)})\sim D^m$ gồm $m$ chuỗi độc lập cùng phân bố $D$ trên $\mathcal X$, tức (T1) với quan sát là cả chuỗi, kể cả độ dài $n_i$. Mẫu kiểm tra độc lập chỉ dùng ở §6 và trong thí nghiệm.
3. **Lớp mô hình và hàm lỗi.** Lớp $\{p_\theta:\theta\in\Theta\}$ gồm các hàm xác suất (hoặc mật độ) trên $\mathcal X$; hàm lỗi log $\ell(\theta,x)=-\ln p_\theta(x)$ (§4); $L_D(\theta)$, $L_S(\theta)$ như Định nghĩa 01.1, 01.6, với $\theta$ ở chỗ của $h$.
4. **Thuật toán.** Ước lượng hợp lý cực đại, tức tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM) với hàm lỗi log (§4). Với biến không quan sát được: thuật toán EM (Expectation–Maximization) (§8) hoặc hạ gradient ngẫu nhiên (stochastic gradient descent, SGD) trên một cận dưới của log độ hợp lý (§9).
5. **Mục tiêu.** Rủi ro kì vọng $L_D(\theta)=\mathbb E_{X\sim D}[-\ln p_\theta(X)]$ nhỏ; với chuỗi, báo cáo thêm giá trị chia cho độ dài (§5).
6. **Đối tượng so sánh.** $\inf_{\theta\in\Theta}L_D(\theta)$, tính ở §7 khi lớp chứa phân bố thật.
7. **Tài nguyên.** Số chuỗi $m$; theo §6, tổng số kí tự $\sum_in_i$ không thay được $m$ trong các cận.

Các đại lượng của bài chia theo nguồn ngẫu nhiên như bảng dưới.

| Loại | Đại lượng |
|---|---|
| Cố định, chọn trước | $\mathcal A$, $D$, $\Theta$, $p_\theta$ với mỗi $\theta$ |
| Ngẫu nhiên theo dữ liệu | $S$, các độ dài $n_i$, $L_S(\cdot)$, $\hat\theta$ |
| Tất định | $L_D(\theta)$ với mỗi $\theta$ |

Dữ liệu chuỗi có hai cách lấy mẫu.

::: definition Định nghĩa 09.1 (Hai thiết lập lấy mẫu cho dữ liệu chuỗi)
Cho bảng chữ $\mathcal A$ (hoặc tập giá trị $\mathbb R$) và một độ dài ngữ cảnh (context length) $k\ge1$.

- **Thiết lập A (các chuỗi độc lập).** Quan sát là cả chuỗi $X^{(i)}=X^{(i)}_{1:n_i}$; mẫu $S=(X^{(1)},\ldots,X^{(m)})\sim D^m$; các kí tự trong một chuỗi được phép phụ thuộc nhau.
- **Thiết lập B (một chuỗi thời gian).** Chỉ có một chuỗi $x_1,\ldots,x_n$, gọi là *chuỗi thời gian* (time series). Với $j=k+1,\ldots,n$, *cửa sổ* thứ $j$ là cặp $u_j=\big((x_{j-k},\ldots,x_{j-1}),\,x_j\big)$ gồm ngữ cảnh độ dài $k$ và đích; hai cửa sổ liền nhau chung $k-1$ giá trị, nên các cửa sổ được gọi là *cửa sổ chồng lấn* (overlapping windows).
:::

Trong Thiết lập A, $m$ chuỗi là $m$ quan sát độc lập cùng phân bố, nên các cận của Bài 02–08 áp dụng với $m$ chuỗi khi hàm lỗi thỏa giả thiết của chúng. Trong Thiết lập B, các cửa sổ nói chung phụ thuộc nhau, nên (T1) không áp dụng, và một bảo đảm cần thêm giả thiết về sự phụ thuộc, ngoài phạm vi bài. Các chuỗi ba kí tự của câu hỏi mở đầu, rút độc lập, thuộc Thiết lập A; phản ví dụ là các cửa sổ chồng lấn của một chuỗi đo hằng ngày, coi như các quan sát độc lập (§6).

## 2. Kí hiệu và giả thiết

Bảng dưới gom các kí hiệu dùng từ §3; kí hiệu khác được đặt tên tại chỗ dùng.

| Kí hiệu | Ý nghĩa |
|---|---|
| $\mathcal A$; $\mathtt A,\mathtt B,\ldots$ | bảng chữ; các kí tự (chữ đơn cách, khác thuật toán $A$) |
| $x_{1:n}$, $x_j$, $x_{<j}$ | chuỗi, kí tự ở vị trí $j$, tiền tố |
| $n$, $n_i$; $k$ | độ dài, độ dài chuỗi thứ $i$; độ dài ngữ cảnh |
| $\theta\in\Theta$; $p_\theta$ | tham số, tập tham số; mô hình |
| $D$, $p_D$ | phân bố thật, hàm xác suất (hoặc mật độ) của nó |
| $\ell(\theta,x)$, $L_D(\theta)$, $L_S(\theta)$; $\hat\theta$ | hàm lỗi log, hai rủi ro; ước lượng hợp lý cực đại |

Tập tham số $\Theta$ khác ma trận trọng số $\Theta_j$ (luôn có chỉ số) của Bài 07.

Hàm lỗi log nằm ngoài khung của các bài trước. Với hàm xác suất, $\ell$ nhận giá trị trong $[0,\infty]$, bằng $+\infty$ khi $p_\theta(x)=0$; với mật độ, $\ell$ có thể âm, chẳng hạn mật độ $N(0;\,0{,}01)$ tại $0$ cho $\ell=\ln(0{,}1\sqrt{2\pi})\approx-1{,}3836$. Vì vậy hàm lỗi log nằm ngoài Định nghĩa 01.1 (giá trị trong $[0,\infty)$), trái (T2) khi có mật độ, và không thỏa (T3); mỗi kết quả của bài nêu điều kiện khả tích tại chỗ. Các cận của Bài 02–04 và Bài 07 áp dụng trực tiếp khi hàm lỗi bị chặn, chẳng hạn khi xác suất của một mô hình rời rạc bị chặn dưới bởi $c>0$ (với mật độ, cần chặn cả trên lẫn dưới), như Ví dụ 07.11, Bước 4 làm với hàm lỗi logistic.

Giả thiết thống kê là (T1) dạng đầy đủ với quan sát là cả chuỗi, dùng ở §6 và trong thí nghiệm; các đồng nhất thức không cần nó. Giả thiết tối ưu chỉ xuất hiện ở thuật toán EM (§8) và ở §9 (tính khả vi và một điều kiện khả tích); không kết quả nào giả sử tính lồi.

## 3. Ví dụ xuyên suốt

::: example Ví dụ 09.1 (Mô hình hai kí tự sinh chuỗi độ dài ba)
**Thiết lập.** $\mathcal A=\{\mathtt A,\mathtt B\}$, $n=3$; chuỗi sinh theo bảng của câu hỏi mở đầu. Bảng có ba tham số tự do: $\Pr(x_1=\mathtt A)=\tfrac35$, $\Pr(x_j=\mathtt B\mid x_{j-1}=\mathtt A)=\tfrac7{10}$ và $\Pr(x_j=\mathtt B\mid x_{j-1}=\mathtt B)=\tfrac25$. Cả ba kí tự là ngẫu nhiên.

**Bước 1: phân bố của kí tự thứ hai.** Theo công thức xác suất toàn phần,
$$
\begin{aligned}
&\Pr(x_2=\mathtt B)\\
&=\tfrac35\cdot\tfrac7{10}+\tfrac25\cdot\tfrac25\\
&=0{,}42+0{,}16=0{,}58 .
\end{aligned}
$$
Kí tự thứ hai là ngẫu nhiên: nó bằng $\mathtt A$ với xác suất $1-0{,}58=0{,}42$.

**Bước 2: kí tự thứ ba phụ thuộc kí tự thứ hai.** Theo bảng, $\Pr(x_3=\mathtt B\mid x_2=\mathtt A)=0{,}7$ và $\Pr(x_3=\mathtt B\mid x_2=\mathtt B)=0{,}4$. Hai xác suất có điều kiện khác nhau, nên $x_2$ và $x_3$ không độc lập.

**Kết luận.** Ba kí tự của một chuỗi phụ thuộc nhau, dù các chuỗi khác nhau được rút độc lập; mỗi kí tự là một phần của một quan sát.
:::

::: application Mô hình bigram cho chuỗi DNA
**Thiết lập.** Mỗi quan sát là một chuỗi DNA độ dài $n=200$ trên $\mathcal A=\{\mathtt A,\mathtt C,\mathtt G,\mathtt T\}$; có $m$ chuỗi rút độc lập (Thiết lập A), $m$ từ $1$ đến $500$. Lớp mô hình là *mô hình bigram* (bigram model, còn gọi là mô hình Markov bậc một), trong đó mỗi kí tự chỉ phụ thuộc kí tự đứng ngay trước: một phân bố cho kí tự đầu và một bảng $4\times4$ xác suất chuyển, $3+12=15$ tham số tự do. Dữ liệu tổng hợp sinh từ một *xích Markov* (Markov chain) đã biết (Phụ lục C), nên giá trị tốt nhất tính được chính xác; $n$, $m$ và bảng chuyển là giá trị giả định.

**Câu hỏi thực hành.** (i) Với $m=50$, trên chuỗi mới, hàm lỗi log chia cho độ dài chuỗi cách giá trị tốt nhất bao xa? (ii) Vì sao với $m$ nhỏ, ước lượng hợp lý cực đại có thể cho hàm lỗi log $+\infty$ trên một chuỗi mới, và sửa thế nào? (iii) Một khoảng tin cậy cho hàm lỗi log trên chuỗi mới dùng cỡ mẫu nào? Câu trả lời ở §6–§7.
:::

## 4. Hàm lỗi log và ước lượng hợp lý cực đại

Một mô hình xác suất trả về một phân bố trên $\mathcal X$ thay cho một nhãn. Để dùng khung ERM của Bài 01, chúng ta cần một hàm lỗi đánh giá một phân bố trên một quan sát.

::: definition Định nghĩa 09.2 (Mô hình xác suất, độ hợp lý và ước lượng hợp lý cực đại)
Cho tập quan sát $\mathcal X$ đếm được và tập tham số $\Theta$.

- **Mô hình xác suất.** Một họ $\{p_\theta:\theta\in\Theta\}$, mỗi $p_\theta$ là một hàm xác suất trên $\mathcal X$: $p_\theta(x)\ge0$ và $\sum_{x\in\mathcal X}p_\theta(x)=1$.
- **Độ hợp lý.** Độ hợp lý của $\theta$ tại quan sát $x$ là $p_\theta(x)$; tại mẫu $s=(x^{(1)},\ldots,x^{(m)})$ là $\prod_{i=1}^mp_\theta(x^{(i)})$. Logarit tự nhiên của nó là *log độ hợp lý* (log-likelihood).
- **Hàm lỗi log.** $\ell(\theta,x)=-\ln p_\theta(x)\in[0,\infty]$, với quy ước $-\ln0=+\infty$ (còn gọi là đối của log độ hợp lý, negative log-likelihood).
- **Ước lượng hợp lý cực đại.** Một $\hat\theta\in\Theta$ làm lớn nhất độ hợp lý của mẫu, tức làm nhỏ nhất $L_s(\theta)=\frac1m\sum_{i=1}^m-\ln p_\theta(x^{(i)})$; đó là ERM (Định nghĩa 01.8) với hàm lỗi log.
:::

Hai cách mô tả $\hat\theta$ tương đương vì $t\mapsto-\frac1m\ln t$ giảm ngặt; với mật độ trên $\mathbb R^p$, tổng thay bằng tích phân. Phân bố thật $p_D$ chưa biết và không nhất thiết thuộc lớp. Nếu thay $p_\theta$ bằng $c\,p_\theta$ với $c>1$, thì $L_s$ giảm đi $\ln c$ và tiến tới $-\infty$ khi $c\to\infty$; vì vậy điều kiện tổng bằng $1$ là cần thiết.

::: example Ví dụ 09.2 (Ước lượng hợp lý cực đại cho phân bố Bernoulli)
**Thiết lập.** Phân bố Bernoulli $\mathrm{Ber}(\theta)$: $\mathcal X=\{0,1\}$, $p_\theta(1)=\theta$, $p_\theta(0)=1-\theta$, $\Theta=[0,1]$. Mẫu cố định $s$ gồm $m=10$ quan sát, trong đó $m_1=7$ quan sát bằng $1$.

**Bước 1: rủi ro thực nghiệm.** Bảy quan sát góp $-\ln\theta$, ba quan sát góp $-\ln(1-\theta)$, nên
$$
\begin{aligned}
L_s(\theta)&=-0{,}7\ln\theta\\
&\quad-0{,}3\ln(1-\theta).
\end{aligned}
$$

**Bước 2: bốn giá trị.** $L_s(0{,}5)=0{,}6931$, $L_s(0{,}6)=0{,}6325$, $L_s(0{,}7)=0{,}6109$ và $L_s(0{,}8)=0{,}6390$. Chẳng hạn, $L_s(0{,}7)=0{,}7\cdot0{,}3567+0{,}3\cdot1{,}2040=0{,}6109$.

**Bước 3: điểm cực tiểu.** Đạo hàm $L_s'(\theta)=-0{,}7/\theta+0{,}3/(1-\theta)$ bằng $0$ khi $0{,}7(1-\theta)=0{,}3\theta$, tức $\theta=0{,}7$. Đạo hàm bậc hai dương trên $(0,1)$, nên đây là điểm cực tiểu duy nhất. Tổng quát, $\hat\theta=m_1/m$.

**Bước 4: trường hợp biên.** Nếu $m_1=0$, thì $L_s(\theta)=-\ln(1-\theta)$ nhỏ nhất tại $\hat\theta=0$, và mô hình học được gán xác suất $0$ cho quan sát $1$.

**Kết luận.** Ước lượng hợp lý cực đại của phân bố Bernoulli là tần suất của số $1$ trong mẫu.
:::

Hàm lỗi log của mô hình ở Bước 4 bằng $+\infty$ trên quan sát $1$.

## 5. Phân tích tự hồi quy

Tập $\mathcal A^n$ có $\lvert\mathcal A\rvert^n$ phần tử, nên một bảng liệt kê xác suất của từng chuỗi cần $\lvert\mathcal A\rvert^n-1$ tham số, tức $4^{200}-1$ với chuỗi DNA của §3. Phép nhân các xác suất có điều kiện ở câu hỏi mở đầu đúng với mọi phân bố trên $\mathcal A^n$.

::: proposition Mệnh đề 09.3 (Quy tắc nhân xác suất cho chuỗi) — chứng minh đầy đủ (Phụ lục D)
**Giả thiết.** Ba thành phần sau.

- **Độ dài.** $n\ge1$ cố định.
- **Phân bố.** $p_1$ là một hàm xác suất bất kì trên $\mathcal A^n$, chẳng hạn $p_D$ hay $p_\theta$.
- **Biên và xác suất có điều kiện.** $p_1(x_{1:j})=\sum_{x_{j+1:n}}p_1(x_{1:n})$ với $j<n$, $p_1(x_{<1})=1$, và $p_1(x_j\mid x_{<j})=p_1(x_{1:j})/p_1(x_{<j})$ khi $p_1(x_{<j})>0$.

**Bảo đảm.** Đồng nhất thức, đúng với mọi chuỗi; không có mẫu và không có xác suất theo $S$.

- **(a) Phân tích tự hồi quy.** Với mọi $x_{1:n}\in\mathcal A^n$, $p_1(x_{1:n})=\prod_{j=1}^np_1(x_j\mid x_{<j})$, với quy ước tích bằng $0$ khi có tiền tố xác suất $0$.
- **(b) Hàm lỗi log.** $-\ln p_1(x_{1:n})=\sum_{j=1}^n-\ln p_1(x_j\mid x_{<j})$, hai vế trong $[0,\infty]$.
- **(c) Chiều ngược.** Cho, với mỗi $j$ và mỗi tiền tố $x_{<j}$, một hàm xác suất $p_\theta(\cdot\mid x_{<j})$ trên $\mathcal A$, chưa giả sử nó là xác suất có điều kiện của phân bố nào. Khi đó $x_{1:n}\mapsto\prod_{j=1}^np_\theta(x_j\mid x_{<j})$ là một hàm xác suất trên $\mathcal A^n$, và xác suất có điều kiện của nó bằng $p_\theta(\cdot\mid x_{<j})$ trên mọi tiền tố có xác suất dương.
:::

Chứng minh ở Phụ lục D chỉ dùng định nghĩa xác suất có điều kiện. Phần (a) và (b) đúng với mọi phân bố, nên chúng không phải giả thiết mô hình; giới hạn độ dài ngữ cảnh hay chọn một kiến trúc mới là giả thiết thêm vào. Theo (c), mọi mô hình định nghĩa bằng các xác suất có điều kiện đều là hàm xác suất, không cần chuẩn hóa thêm.

::: definition Định nghĩa 09.4 (Mô hình tự hồi quy, độ bối rối và học theo đáp án)
Cho độ dài $n$ và tập tham số $\Theta$.

- **Mô hình tự hồi quy.** Với mỗi $\theta$, một họ hàm xác suất $p_\theta(\cdot\mid x_{<j})$ trên $\mathcal A$, $j=1,\ldots,n$; mô hình trên chuỗi là $p_\theta(x_{1:n})=\prod_jp_\theta(x_j\mid x_{<j})$, một hàm xác suất theo Mệnh đề 09.3(c). Thừa số thứ $j$ là *độ hợp lý có điều kiện* (conditional likelihood) của vị trí $j$.
- **Ngữ cảnh bậc $k$.** Mô hình có ngữ cảnh bậc $k$ nếu $p_\theta(x_j\mid x_{<j})$ chỉ phụ thuộc $k$ kí tự cuối của tiền tố; bậc $1$ là mô hình bigram.
- **Hàm lỗi log theo kí tự và độ bối rối.** *Hàm lỗi log trung bình theo kí tự* là $\tfrac1n\ell(\theta,x_{1:n})$, và *độ bối rối* (perplexity) là $\exp\big(\tfrac1n\ell(\theta,x_{1:n})\big)$.
- **Học theo đáp án.** *Học theo đáp án* (teacher forcing) là cách tính $\ell(\theta,x_{1:n})$ theo Mệnh đề 09.3(b) và gradient của nó, trong đó mỗi xác suất có điều kiện dùng tiền tố thật $x_{<j}$ của chuỗi huấn luyện, không dùng tiền tố do mô hình sinh ra.
:::

Khi huấn luyện theo đáp án, hàm lỗi log được tính đúng như Mệnh đề 09.3(b). Khi sinh chuỗi mới, tiền tố được rút từ chính $p_\theta$, nên phân bố của tiền tố lúc sinh có thể khác lúc huấn luyện khi $p_\theta\ne p_D$.

Độ bối rối bằng $\lvert\mathcal A\rvert$ khi mọi xác suất có điều kiện bằng $1/\lvert\mathcal A\rvert$ (mô hình đều). Mô hình của Ví dụ 09.1 là một mô hình bigram; với ngữ cảnh bậc $1$, mô hình trên chuỗi DNA của §3 có $15$ tham số tự do thay cho $4^{200}-1$. Một bảng có hàng không cộng lại bằng $1$, chẳng hạn hàng $\mathtt A$ là $(0{,}5;\,0{,}7)$, không xác định một mô hình tự hồi quy.

::: example Ví dụ 09.3 (Độ hợp lý của chuỗi $\mathtt{ABB}$)
**Thiết lập.** Mô hình của Ví dụ 09.1, chuỗi cố định $x_{1:3}=\mathtt{ABB}$.

**Bước 1: ba xác suất có điều kiện.** Đọc bảng: $p_\theta(\mathtt A)=\tfrac35$, $p_\theta(\mathtt B\mid\mathtt A)=\tfrac7{10}$, $p_\theta(\mathtt B\mid\mathtt{AB})=\tfrac25$. Vị trí $3$ dùng tiền tố thật $\mathtt{AB}$ (học theo đáp án), nhưng với ngữ cảnh bậc $1$ chỉ kí tự $\mathtt B$ ở vị trí $2$ được dùng.

**Bước 2: độ hợp lý.** Theo Mệnh đề 09.3(a), độ hợp lý là tích ba xác suất có điều kiện:
$$
\tfrac35\cdot\tfrac7{10}\cdot\tfrac25=\tfrac{21}{125}=0{,}168 .
$$

**Bước 3: hàm lỗi log.** Ba số hạng là $-\ln\tfrac35=0{,}5108$, $-\ln\tfrac7{10}=0{,}3567$ và $-\ln\tfrac25=0{,}9163$, nên theo Mệnh đề 09.3(b)
$$
\begin{aligned}
\ell&=0{,}5108+0{,}3567+0{,}9163\\
&=1{,}7838 .
\end{aligned}
$$

**Bước 4: theo kí tự.** Hàm lỗi log trung bình theo kí tự là $1{,}7838/3=0{,}5946$; độ bối rối là $e^{0{,}5946}=0{,}168^{-1/3}\approx1{,}8123$, nhỏ hơn $2$ của mô hình đều.

**Bước 5: chuẩn hóa.** Lấy tổng lần lượt theo $x_3$, $x_2$, $x_1$; mỗi lần được $1$ vì mỗi hàng của bảng có tổng $1$. Tám chuỗi trong $\{\mathtt A,\mathtt B\}^3$ có tổng xác suất $1$ (Mệnh đề 09.3(c)).

**Kết luận.** Độ hợp lý của chuỗi là tích các độ hợp lý có điều kiện.
:::

::: remark Nhận xét 09.5 (Độ dài thay đổi và kí tự kết thúc)
Nếu dùng bảng của Ví dụ 09.1 cho mọi độ dài, tổng các tích trên mọi chuỗi độ dài $1$, $2$, $3$ bằng $1+1+1=3$, nên các tích này không là một hàm xác suất trên tập các chuỗi hữu hạn. Cách sửa là thêm một *kí tự kết thúc* (end-of-sequence token) $\mathtt E$ vào bảng chữ: chuỗi kết thúc ở lần đầu rút $\mathtt E$. Chẳng hạn, nếu sau mỗi kí tự mô hình rút $\mathtt E$ với xác suất $\tfrac12$, thì độ dài $n$ có xác suất $(\tfrac12)^n$, và tổng theo $n\ge1$ bằng $1$; cách sửa cần chuỗi kết thúc với xác suất $1$. Hàm lỗi log của chuỗi khi đó gồm cả số hạng của $\mathtt E$.
:::

Mỗi số hạng của hàm lỗi log của chuỗi là một bài toán phân lớp trên $\mathcal A$ với ngữ cảnh là tiền tố, còn cả tổng là một số hạng của rủi ro thực nghiệm, ứng với một quan sát.

## 6. Quan sát độc lập ở cấp chuỗi và trọng số theo độ dài

Theo Mệnh đề 09.3, hàm lỗi của một chuỗi là tổng của $n$ số hạng phụ thuộc nhau (Ví dụ 09.1, Bước 2). Trong Thiết lập A, rủi ro thực nghiệm $L_S(\theta)=\frac1m\sum_{i=1}^m\ell(\theta,X^{(i)})$ là trung bình của $m$ biến độc lập cùng phân bố. Với $\theta$ cố định, không phụ thuộc $S$, Mệnh đề 01.7 cho $\mathbb E_SL_S(\theta)=L_D(\theta)$ khi $L_D(\theta)<\infty$, chỉ cần dạng yếu của (T1). Định lý 02.7 cần các số hạng độc lập (Ví dụ 02.6) và bị chặn, nên chỉ áp dụng ở cấp chuỗi.

::: example Ví dụ 09.4 (Cận Hoeffding ở cấp chuỗi cho hàm lỗi log)
**Thiết lập.** Khối ứng dụng ở §3, $n=200$. Một mô hình bigram $p_\theta$ cố định, không phụ thuộc mẫu kiểm tra, có mọi xác suất kí tự đầu và xác suất chuyển không nhỏ hơn $c=0{,}05$ (giá trị giả định). Mẫu kiểm tra $S$ gồm $m=50$ chuỗi độc lập (Thiết lập A); $\delta=0{,}05$.

**Bước 1: miền giá trị.** Mỗi số hạng thỏa $-\ln p_\theta(x_j\mid x_{<j})\in[0,\ln(1/c)]=[0,\ln20]$, với $\ln20\approx2{,}9957$. Do đó $\ell(\theta,x_{1:200})\in[0,b]$, với $b=200\ln20\approx599{,}15$.

**Bước 2: cận Hoeffding cho $m$ chuỗi.** Áp dụng Hệ quả 02.10(b) cho hàm lỗi $\ell/b\in[0,1]$, rồi nhân bán kính với $b$ (đoạn sau (T3)). Với xác suất ít nhất $1-\delta$ theo mẫu kiểm tra,
$$
\begin{aligned}
&\lvert L_S(\theta)-L_D(\theta)\rvert\\
&\le b\sqrt{\ln(2/\delta)/(2m)}\\
&\approx599{,}15\cdot0{,}19207\\
&\le115{,}08 .
\end{aligned}
$$

**Bước 3: theo kí tự.** Chia cho $n=200$: bán kính cho hàm lỗi log trung bình theo kí tự không quá $0{,}5754$ nat. Bán kính này bằng $\ln(1/c)\sqrt{\ln(2/\delta)/(2m)}$, nên không giảm khi $n$ tăng.

**Bước 4: phép đếm sai.** Coi $mn=10^4$ kí tự là $10^4$ quan sát độc lập với miền $[0,\ln20]$, cùng công thức cho bán kính $\ln20\sqrt{\ln40/(2\cdot10^4)}\approx0{,}0407$; Định lý 02.7 không cho phép con số này, vì các kí tự trong một chuỗi phụ thuộc nhau (Ví dụ 09.1).

**Bước 5: cỡ mẫu.** Để bán kính theo kí tự không quá $0{,}05$, cần
$$
\begin{aligned}
m&\ge\frac{(\ln20)^2\ln40}{2\cdot0{,}05^2}\approx6621{,}1,
\end{aligned}
$$
tức ít nhất $6622$ chuỗi.

**Kết luận.** Với công cụ của Bài 02, cỡ mẫu trong cận là số chuỗi; một cận dùng số kí tự cần thêm giả thiết về sự phụ thuộc giữa các kí tự. Cận cũng cần $c>0$: không có cận dưới cho các xác suất, hàm lỗi không bị chặn (Nhận xét 02.11).
:::

Trong Thiết lập B, sai lệch xuất hiện ngay ở bước đánh giá, qua rò rỉ thông tin (leakage) từ mẫu huấn luyện sang mẫu kiểm tra.

::: example Ví dụ 09.5 (Rò rỉ thông tin khi chia ngẫu nhiên cửa sổ chồng lấn)
**Thiết lập.** Một chuỗi $x_1,\ldots,x_{5000}$ độc lập cùng phân bố $N(0,1)$ (giá trị giả định; thí nghiệm của học phần, Phụ lục C). Cửa sổ có độ dài ngữ cảnh $k=10$, bước trượt $1$: $4990$ cửa sổ, $20\%$ ($998$) làm mẫu kiểm tra; hàm lỗi bình phương. Vì $x_j$ độc lập với ngữ cảnh và có trung bình $0$, mọi hàm dự đoán đích từ ngữ cảnh có rủi ro ít nhất $\operatorname{Var}(x_j)=1$.

**Bước 1: hàm dự đoán ghi nhớ** (theo cách của Định nghĩa 01.14). Với cửa sổ kiểm tra $u_j$, hàm dự đoán tìm cửa sổ huấn luyện có chín giá trị đầu của ngữ cảnh bằng $(x_{j-9},\ldots,x_{j-1})$. Đó là $u_{j+1}$, với giá trị cuối của ngữ cảnh là đích $x_j$; hàm dự đoán trả về giá trị đó nếu tìm thấy, và trả về $0$ nếu không.

**Bước 2: chia ngẫu nhiên.** Cửa sổ $u_{j+1}$ thuộc mẫu huấn luyện với xác suất khoảng $0{,}8$, và khi đó lỗi bằng $0$; nếu không, lỗi trung bình bằng $1$. Lỗi bình phương trung bình (mean squared error, MSE) trên mẫu kiểm tra vì vậy khoảng $0{,}2$; thí nghiệm với $10$ chuỗi cho $0{,}200$ (từ $0{,}137$ đến $0{,}245$).

**Bước 3: chia theo thời gian.** Với $80\%$ cửa sổ đầu làm mẫu huấn luyện, không lần tra cứu nào thành công; MSE là $0{,}994$ (từ $0{,}915$ đến $1{,}066$), bằng MSE của dự đoán $0$ trên cùng mẫu kiểm tra.

**Bước 4: giả thiết bị vi phạm.** Mẫu kiểm tra chia ngẫu nhiên không độc lập với hàm dự đoán đã học, tức (T7) không thỏa. Đích của một cửa sổ kiểm tra nằm trong ngữ cảnh của mười cửa sổ $u_{j+1},\ldots,u_{j+10}$, và ít nhất một trong số đó thuộc mẫu huấn luyện với xác suất xấp xỉ $1-0{,}2^{10}\approx1-10^{-7}$; hàm dự đoán của Bước 1 chỉ khai thác rò rỉ qua $u_{j+1}$. Con số $0{,}2$ nhỏ hơn rủi ro nhỏ nhất $1$, nên nó không ước lượng rủi ro trên dữ liệu mới.

**Kết luận.** Với cửa sổ chồng lấn, mẫu kiểm tra được chia theo thời gian; khi phần kiểm tra nằm giữa chuỗi, bỏ thêm $k$ cửa sổ ở mỗi biên. Kể cả khi đó, các cửa sổ kiểm tra vẫn phụ thuộc nhau, nên Hệ quả 02.10 không cho khoảng tin cậy nếu không có giả thiết thêm.
:::

Khi độ dài các chuỗi khác nhau, có thể chia hàm lỗi của mỗi chuỗi cho độ dài của nó.

::: definition Định nghĩa 09.6 (Hàm lỗi tổng và hàm lỗi chuẩn hóa theo độ dài)
Cho mô hình tự hồi quy $p_\theta$ trên các chuỗi có độ dài thay đổi, kết thúc bằng kí tự $\mathtt E$ (Nhận xét 09.5), và chuỗi $x$ có $n(x)\ge1$ kí tự trước $\mathtt E$; đặt $x_{n(x)+1}=\mathtt E$.

- **Hàm lỗi tổng.** $\ell(\theta,x)=\sum_{j=1}^{n(x)+1}-\ln p_\theta(x_j\mid x_{<j})$ (total sequence loss), tức hàm lỗi log của chuỗi, kể cả số hạng của $\mathtt E$.
- **Hàm lỗi chuẩn hóa theo độ dài.** $\ell_{\mathrm{len}}(\theta,x)=\ell(\theta,x)/n(x)$ (length-normalized loss).
:::

Chia rủi ro thực nghiệm với hàm lỗi tổng cho tổng số kí tự $\sum_in_i$ không đổi điểm cực tiểu, và mỗi kí tự có cùng trọng số. Hàm lỗi chuẩn hóa cho mỗi chuỗi cùng trọng số, nên mỗi kí tự của một chuỗi độ dài $n$ có trọng số $1/n$. Trên lớp mọi phân bố trên tập chuỗi hữu hạn, kì vọng của $\ell_{\mathrm{len}}$ nhỏ nhất tại phân bố tỉ lệ với $p_D(x)/n(x)$, nghiêng về chuỗi ngắn (Bài tập 09.5(c)). Khi mọi chuỗi có cùng độ dài, hai hàm lỗi cho cùng điểm cực tiểu.

::: example Ví dụ 09.6 (Hai mục tiêu cho hai độ dài chuỗi)
**Thiết lập.** $\mathcal A=\{\mathtt 0,\mathtt 1\}$. Phân bố $D$ cho chuỗi ngắn $\mathtt{11}$ và chuỗi dài gồm mười kí tự $\mathtt 0$, mỗi chuỗi với xác suất $\tfrac12$. Mô hình coi các kí tự độc lập, mỗi kí tự là $\mathtt 1$ với xác suất $\theta\in(0,1)$. Xác suất của $\mathtt E$ có tham số riêng, không phụ thuộc $\theta$; số hạng của nó là hằng theo $\theta$ trong cả hai mục tiêu, nên ta bỏ nó.

**Bước 1: hàm lỗi tổng.** Rủi ro kì vọng là
$$
\begin{aligned}
&\tfrac12(-2\ln\theta)+\tfrac12\big(-10\ln(1-\theta)\big)\\
&=-\ln\theta-5\ln(1-\theta).
\end{aligned}
$$
Đạo hàm $-1/\theta+5/(1-\theta)$ bằng $0$ tại $\theta=\tfrac16$, tức $2/12$, tần suất của $\mathtt 1$ trên mọi kí tự.

**Bước 2: hàm lỗi chuẩn hóa.** Chia hàm lỗi của chuỗi ngắn cho $2$, của chuỗi dài cho $10$:
$$
\begin{aligned}
&\tfrac12\cdot\tfrac{-2\ln\theta}2+\tfrac12\cdot\tfrac{-10\ln(1-\theta)}{10}\\
&=-\tfrac12\ln\theta-\tfrac12\ln(1-\theta).
\end{aligned}
$$
Đạo hàm $-\tfrac1{2\theta}+\tfrac1{2(1-\theta)}$ bằng $0$ tại $\theta=\tfrac12$, trung bình của tần suất của $\mathtt 1$ trong từng chuỗi ($1$ và $0$).

**Bước 3: trọng số của mỗi kí tự.** Với hàm lỗi tổng, mọi kí tự có trọng số $\tfrac12$. Với hàm lỗi chuẩn hóa, mỗi kí tự của chuỗi ngắn có trọng số $\tfrac12\cdot\tfrac12=\tfrac14$, mỗi kí tự của chuỗi dài có trọng số $\tfrac12\cdot\tfrac1{10}=\tfrac1{20}$.

**Kết luận.** Khi độ dài chuỗi khác nhau, hai mục tiêu có hai điểm cực tiểu khác nhau, $\tfrac16$ và $\tfrac12$, vì chúng gán trọng số khác nhau cho kí tự của chuỗi ngắn và chuỗi dài.
:::

Trong Thiết lập A, các cận dùng số chuỗi $m$; trong Thiết lập B, chia ngẫu nhiên các cửa sổ làm mẫu kiểm tra phụ thuộc hàm đã học. Khi độ dài các chuỗi khác nhau, cần ghi rõ mục tiêu nào được tối thiểu hóa, vì hai mục tiêu có điểm cực tiểu khác nhau.

## 7. Entropy, phân kì Kullback–Leibler và ước lượng hợp lý cực đại tổng thể

Rủi ro kì vọng $L_D(\theta)=\mathbb E_D[-\ln p_\theta(X)]$ phụ thuộc phân bố thật chưa biết. Chúng ta tách nó thành một phần chỉ phụ thuộc $D$, là giá trị tốt nhất, và một phần đo độ lệch của $p_\theta$ khỏi $p_D$.

::: definition Định nghĩa 09.7 (Entropy, entropy chéo và phân kì Kullback–Leibler)
Cho hai hàm xác suất $p_1$, $p_2$ trên tập đếm được $\mathcal X$, với quy ước $0\ln0=0$ và $a\ln(a/0)=+\infty$ khi $a>0$.

- **Giá.** *Giá* (support) của $p_1$ là $\{x:p_1(x)>0\}$.
- **Entropy.** $\mathrm H(p_1)=-\sum_xp_1(x)\ln p_1(x)\in[0,\infty]$.
- **Entropy chéo.** $-\sum_xp_1(x)\ln p_2(x)\in[0,\infty]$ (cross-entropy), tức $\mathbb E_{X\sim p_1}[-\ln p_2(X)]$; với $p_1=p_D$ và $p_2=p_\theta$, đó là $L_D(\theta)$.
- **Phân kì Kullback–Leibler (KL).** $\mathrm{KL}(p_1\Vert p_2)=\sum_{x:\,p_1(x)>0}p_1(x)\ln\dfrac{p_1(x)}{p_2(x)}$ (còn gọi là entropy tương đối, relative entropy).
- **Bản mật độ.** Với mật độ $p_1$, $p_2$ trên $\mathbb R^p$: *entropy vi phân* (differential entropy) $\mathrm h(p_1)=-\int p_1\ln p_1$ và $\mathrm{KL}(p_1\Vert p_2)=\int_{p_1>0}p_1\ln(p_1/p_2)$, khi các tích phân xác định.
:::

Tổng trong định nghĩa $\mathrm{KL}$ luôn xác định trong $(-\infty,\infty]$. Với $t=p_2(x)/p_1(x)$, bất đẳng thức $\ln t\le t-1$ (câu ôn nhanh 2) cho $p_1(x)\ln\frac{p_1(x)}{p_2(x)}\ge p_1(x)-p_2(x)\ge-p_2(x)$, và $\sum_xp_2(x)=1$, nên phần âm của các số hạng có tổng hữu hạn.

Phân kì KL không đối xứng, nên không phải một khoảng cách: $\mathrm{KL}(\mathrm{Ber}(0{,}6)\Vert\mathrm{Ber}(0{,}7))\approx0{,}0226$, còn $\mathrm{KL}(\mathrm{Ber}(0{,}7)\Vert\mathrm{Ber}(0{,}6))\approx0{,}0216$. Với hai phân bố Gauss một chiều (Phụ lục A),
$$
\begin{aligned}
&\mathrm{KL}\big(N(\mu_1,\sigma_1^2)\Vert N(\mu_2,\sigma_2^2)\big)\\
&=\ln\frac{\sigma_2}{\sigma_1}+\frac{\sigma_1^2+(\mu_1-\mu_2)^2}{2\sigma_2^2}-\frac12 ;
\end{aligned}
$$
với $\mu_2=0$, $\sigma_2=1$, vế phải bằng $\tfrac12(\mu_1^2+\sigma_1^2-1-\ln\sigma_1^2)$.

Entropy vi phân có thể âm: phân bố đều trên $[0,\tfrac12]$ có $\mathrm h=-\ln2\approx-0{,}6931$. Rời rạc hóa với bước $\Delta$ cho entropy xấp xỉ $\mathrm h-\ln\Delta$, tiến ra vô cùng khi $\Delta\to0$ (Bài tập 09.3(d)), nên $\mathrm h$ không phải giới hạn của entropy rời rạc. Kí hiệu $\mathrm H$, $\mathrm h$ in đứng, khác lớp giả thuyết $\mathcal H$ và giả thuyết $h$.

::: proposition Mệnh đề 09.8 (Rủi ro với hàm lỗi log bằng entropy cộng phân kì KL) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Tập quan sát.** $\mathcal X$ đếm được.
- **Phân bố thật.** $D$ có hàm xác suất $p_D$ với $\mathrm H(p_D)<\infty$.
- **Mô hình.** $p_\theta$ là một hàm xác suất trên $\mathcal X$, với $\theta$ cố định.

**Bảo đảm.** Tổng thể: kì vọng theo $D$, không có mẫu.

- **(a) Phân tích.** $L_D(\theta)=\mathrm H(p_D)+\mathrm{KL}(p_D\Vert p_\theta)$, hai vế trong $[0,\infty]$. Nếu có $x$ với $p_D(x)>0=p_\theta(x)$, hai vế bằng $+\infty$.
- **(b) Không âm.** $\mathrm{KL}(p_D\Vert p_\theta)\ge0$, dấu bằng khi và chỉ khi $p_\theta=p_D$. Do đó $L_D(\theta)\ge\mathrm H(p_D)$, dấu bằng khi và chỉ khi $p_\theta=p_D$.
- **(c) Mật độ.** Nếu $\mathcal X\subseteq\mathbb R^p$, $p_D$ và $p_\theta$ là mật độ, $\int p_D\lvert\ln p_D\rvert<\infty$ và $\int p_D\lvert\ln p_\theta\rvert<\infty$, thì $L_D(\theta)=\mathrm h(p_D)+\mathrm{KL}(p_D\Vert p_\theta)$, với $\mathrm{KL}\ge0$ và dấu bằng khi và chỉ khi $p_\theta=p_D$ hầu khắp nơi; $\mathrm h(p_D)$ có thể âm.
:::

::: proof Chứng minh Mệnh đề 09.8
**Lộ trình.** Tách logarit trên giá $\{x:p_D(x)>0\}$, rồi chặn phân kì KL. Bất đẳng thức then chốt là $\ln t\le t-1$; không cần bất đẳng thức Jensen.

**Bước 1 ($p_\theta$ bằng $0$ tại một điểm của giá của $p_D$).** Nếu $p_D(x_0)>0=p_\theta(x_0)$, thì $\ell(\theta,X)=+\infty$ với xác suất $p_D(x_0)>0$, nên $L_D(\theta)=+\infty$. Số hạng $x_0$ của $\mathrm{KL}$ bằng $+\infty$, còn phần âm của các số hạng khác có tổng hữu hạn (đoạn sau Định nghĩa 09.7), nên $\mathrm{KL}=+\infty$.

**Bước 2 (tách logarit; dùng $\mathrm H(p_D)<\infty$).** Giả sử $p_\theta>0$ trên giá của $p_D$. Với mỗi $x$ có $p_D(x)>0$,
$$
\begin{aligned}
-\ln p_\theta(x)&=-\ln p_D(x)\\
&\quad+\ln\frac{p_D(x)}{p_\theta(x)} .
\end{aligned}
$$
Nhân với $p_D(x)$ và lấy tổng theo $x$. Tổng thứ nhất có số hạng không âm và bằng $\mathrm H(p_D)<\infty$; tổng thứ hai là $\mathrm{KL}$, xác định trong $(-\infty,\infty]$. Vì tổng thứ nhất hữu hạn, ta cộng được hai tổng theo từng số hạng và được (a); giả thiết entropy hữu hạn dùng ở đây.

**Bước 3 ((b)).** Nếu $\mathrm{KL}=+\infty$, (b) đúng. Nếu không, áp dụng $\ln t\le t-1$ với $t=p_\theta(x)/p_D(x)$ cho từng số hạng:
$$
\begin{aligned}
&-\mathrm{KL}(p_D\Vert p_\theta)\\
&=\sum_{p_D>0}p_D\ln\frac{p_\theta}{p_D}\\
&\le\sum_{p_D>0}(p_\theta-p_D)\\
&=\sum_{p_D>0}p_\theta-1\le0 .
\end{aligned}
$$
Dấu bằng cần $\ln t=t-1$, tức $t=1$, tại mọi $x$ của giá, và $\sum_{p_D>0}p_\theta=1$, tức $p_\theta=0$ ngoài giá; hai điều này nghĩa là $p_\theta=p_D$. Vế sau của (b) suy ra từ (a), vì $\mathrm H(p_D)$ hữu hạn.

**Bước 4 ((c)).** Cùng lập luận với tích phân thay cho tổng. Hai điều kiện khả tích thay cho $\mathrm H(p_D)<\infty$ ở Bước 2, và $\int_{p_D>0}p_\theta\le1$ thay cho tổng ở Bước 3.

$\square$ Với hàm lỗi log, không mô hình nào có rủi ro kì vọng nhỏ hơn entropy của phân bố thật, và phần vượt trên giá trị này bằng đúng $\mathrm{KL}(p_D\Vert p_\theta)$. Khi lớp chứa $p_D$, phần vượt này là rủi ro vượt mức (Định nghĩa 01.24).
:::

::: corollary Hệ quả 09.9 (Ước lượng hợp lý cực đại tổng thể và phân kì KL thuận) — chứng minh đầy đủ
**Giả thiết.** $D$ như Mệnh đề 09.8, với $\mathrm H(p_D)<\infty$; lớp $\{p_\theta:\theta\in\Theta\}$ gồm các hàm xác suất trên $\mathcal X$.

**Bảo đảm.** Tổng thể, không có mẫu.

- **(a) Cùng điểm cực tiểu.** Với mọi $\theta,\theta'\in\Theta$ có $L_D$ hữu hạn, $L_D(\theta)-L_D(\theta')=\mathrm{KL}(p_D\Vert p_\theta)-\mathrm{KL}(p_D\Vert p_{\theta'})$. Tập các $\theta$ làm nhỏ nhất $L_D$ trên $\Theta$ trùng tập các $\theta$ làm nhỏ nhất *phân kì KL thuận* (forward KL) $\mathrm{KL}(p_D\Vert p_\theta)$, và $\inf_\Theta L_D=\mathrm H(p_D)+\inf_\Theta\mathrm{KL}(p_D\Vert p_\theta)$.
- **(b) Đặc tả đúng** (well-specified). Nếu $p_D=p_{\theta^\star}$ với một $\theta^\star\in\Theta$, thì $\theta^\star$ làm nhỏ nhất $L_D$, và mọi điểm cực tiểu $\theta$ có $p_\theta=p_D$.
:::

::: proof Chứng minh Hệ quả 09.9
**Lộ trình.** Trừ hai đẳng thức của Mệnh đề 09.8(a).

**Bước 1 ((a)).** Vì $\mathrm H(p_D)$ hữu hạn, phép trừ hợp lệ khi $L_D(\theta)$, $L_D(\theta')$ hữu hạn; khi $L_D(\theta)=+\infty$, cả $\mathrm{KL}(p_D\Vert p_\theta)=+\infty$, nên hai tiêu chí cùng loại $\theta$ đó. Lấy cận dưới đúng hai vế của Mệnh đề 09.8(a) cho đẳng thức của $\inf_\Theta L_D$.

**Bước 2 ((b)).** Theo Mệnh đề 09.8(b), $\mathrm{KL}(p_D\Vert p_{\theta^\star})=0$ là giá trị nhỏ nhất có thể, và $\mathrm{KL}(p_D\Vert p_\theta)=0$ chỉ khi $p_\theta=p_D$.

$\square$ Ước lượng hợp lý cực đại tổng thể nhắm tới mô hình gần $p_D$ nhất theo $\mathrm{KL}(p_D\Vert\cdot)$. Khi lớp không chứa $p_D$, mô hình bị *đặc tả sai* (misspecification); nếu thêm $\inf_\Theta\mathrm{KL}(p_D\Vert p_\theta)>0$, phần chênh này còn lại ngay cả khi có vô hạn dữ liệu.
:::

Hệ quả 09.9 chỉ áp dụng cho điểm cực tiểu của rủi ro kì vọng; nó không cho kết luận về ước lượng hợp lý cực đại trên một mẫu hữu hạn (ví dụ ngay sau đây) hay về các chuỗi do mô hình sinh ra (§9). Lấy $D=\mathrm{Ber}(0{,}6)$ (giá trị giả định) và mẫu của Ví dụ 09.2. Khi đó $\mathrm H(p_D)\approx0{,}6730$, và theo Mệnh đề 09.8(a), $L_D(0{,}7)\approx0{,}6730+0{,}0226=0{,}6956$. Rủi ro thực nghiệm $L_s(0{,}7)=0{,}6109$ nhỏ hơn cả $\mathrm H(p_D)$, và khoảng cách tổng quát hóa (Định nghĩa 01.10) bằng $0{,}6956-0{,}6109=0{,}0847$.

::: example Ví dụ 09.7 (Mô hình bằng $0$ trên giá của $p_D$ và mẫu toàn số $0$)
**Thiết lập.** Bước 1–2: $\mathcal X=\{1,2,3\}$, $p_D=(\tfrac12,\tfrac12,0)$, $\mathrm H(p_D)=\ln2\approx0{,}6931$; mô hình $p_\theta=(1-\theta,\theta,0)$ với $\theta\in[0,1]$, cố định. Bước 3–4: $\mathcal X=\{0,1\}$, $D=\mathrm{Ber}(\theta^\star)$ với $\theta^\star=0{,}01$ (theo ý của UML §24.1.3), mẫu $S\sim D^m$ và ước lượng của Ví dụ 09.2; $S$ và $\hat\theta$ là ngẫu nhiên.

**Bước 1: xác suất nhỏ trên giá.** $L_D(\theta)=-\tfrac12\ln(1-\theta)-\tfrac12\ln\theta$ bằng $1{,}2040$; $3{,}4544$; $6{,}9078$ với $\theta=10^{-1}$, $10^{-3}$, $10^{-6}$, và bằng $+\infty$ với $\theta=0$ (Mệnh đề 09.8(a)). Chẳng hạn, $L_D(0{,}1)=0{,}0527+1{,}1513=1{,}2040$.

**Bước 2: khối lượng ngoài giá.** Mô hình $(0{,}4;\,0{,}4;\,0{,}2)$ đặt khối lượng ở điểm $3$, nơi $p_D$ bằng $0$. Khi đó $L_D=\ln2{,}5\approx0{,}9163$ và $\mathrm{KL}=\ln1{,}25\approx0{,}2231$, cả hai hữu hạn.

**Bước 3: mẫu toàn số $0$.** Biến cố này có xác suất $0{,}99^m$, bằng $0{,}9044$; $0{,}6050$; $0{,}3660$ với $m=10$, $50$, $100$.

Xác suất ít nhất $\tfrac12$ khi và chỉ khi $m\le68$, vì $0{,}99^{68}\approx0{,}5049$ và $0{,}99^{69}\approx0{,}4998$.

Trên biến cố đó, $\hat\theta=0$ (Ví dụ 09.2, Bước 4), nên $L_D(\hat\theta)=0{,}01\cdot(-\ln0)=+\infty$.

Biến cố có xác suất dương với mọi $m$, nên $\mathbb E_SL_D(\hat\theta)=+\infty$ với mọi $m$.

**Bước 4: làm trơn cộng một.** Ước lượng $\hat\theta=(1+m_1)/(m+2)$, gọi là *làm trơn cộng một* (add-one smoothing), luôn nằm trong $[\tfrac1{m+2},\tfrac{m+1}{m+2}]$, nên $\ell(\hat\theta,x)\le\ln(m+2)$; đây là ước lượng hợp lý cực đại sau khi thêm hai quan sát giả (Bài tập 09.9).

Với $m=50$ và $m_1=0$: $\hat\theta=1/52\approx0{,}0192$ và $\ell\le\ln52<3{,}952$.

Rủi ro kì vọng là $L_D(\hat\theta)=-0{,}99\ln\tfrac{51}{52}-0{,}01\ln\tfrac1{52}\approx0{,}0192+0{,}0395=0{,}0587$, so với $\mathrm H(p_D)\approx0{,}0560$.

**Kết luận.** Trên mẫu hữu hạn, ước lượng hợp lý cực đại có thể có rủi ro kì vọng vô hạn; hàm lỗi log là một hàm lỗi không bị chặn như ở Nhận xét 02.11.
:::

::: example Ví dụ 09.8 (Mô hình bigram trên chuỗi DNA tổng hợp)
**Thiết lập.** Khối ứng dụng ở §3, với xích Markov ở Phụ lục C: mỗi hàng của bảng chuyển gồm $0{,}6$ (giữ nguyên kí tự), $0{,}2$, $0{,}1$, $0{,}1$, và kí tự đầu rút đều. Mỗi lần chạy có $m$ chuỗi huấn luyện và $200$ chuỗi kiểm tra rút độc lập; $10$ lần chạy. Thiết lập A thỏa, và lớp bigram chứa mô hình thật.

**Bước 1: giá trị tốt nhất.** Lấy kì vọng hai vế của Mệnh đề 09.3(b) với $p_1=p_D$. Kí tự đầu có entropy $\ln4$. Với $j\ge2$, khi biết $x_{j-1}$, số hạng thứ $j$ có kì vọng có điều kiện bằng entropy của hàng ứng với $x_{j-1}$; mọi hàng có cùng entropy $-(0{,}6\ln0{,}6+0{,}2\ln0{,}2+2\cdot0{,}1\ln0{,}1)\approx1{,}0889$, nên kì vọng bằng $1{,}0889$. Do đó
$$
\begin{aligned}
&\mathrm H(p_D)=\ln4+199\cdot1{,}0889\\
&\approx1{,}3863+216{,}69=218{,}08,\\
&\mathrm H(p_D)/200\approx1{,}0904 ,
\end{aligned}
$$
ứng với độ bối rối $2{,}975$. Theo Mệnh đề 09.8(b), không mô hình nào có hàm lỗi log kì vọng theo kí tự nhỏ hơn $1{,}0904$.

**Bước 2: bảng.** Kết quả thí nghiệm của học phần: hàm lỗi log trung bình theo kí tự trên mẫu kiểm tra, trung bình của $10$ lần chạy.

| $m$ | MLE | Làm trơn | Mô hình thật |
|---|---|---|---|
| $1$ | $+\infty$ | $1{,}122$ | $1{,}091$ |
| $5$ | $+\infty$ | $1{,}097$ | $1{,}090$ |
| $50$ | $1{,}091$ | $1{,}091$ | $1{,}091$ |
| $500$ | $1{,}088$ | $1{,}088$ | $1{,}088$ |

MLE cho $+\infty$ ở $10/10$ lần chạy với $m=1$ và $5/10$ lần với $m=5$; trên mẫu huấn luyện, nó cho $1{,}070$; $1{,}080$; $1{,}090$; $1{,}090$ với $m=1$, $5$, $50$, $500$.

**Bước 3: nguồn của $+\infty$.** Với $m=1$, ước lượng hợp lý cực đại gán xác suất $0$ cho ba kí tự đầu chưa gặp, nên một chuỗi kiểm tra bắt đầu bằng kí tự khác có hàm lỗi $+\infty$. Ở cả $10$ lần chạy, mọi chuyển tiếp của mẫu kiểm tra đều đã gặp trong chuỗi huấn luyện. Nếu chuỗi huấn luyện chỉ có $12$ kí tự, như $12$ kí tự đầu $\mathtt{AAGGAAAACCCC}$ của một chuỗi rút với hạt giống $3$, thì $10$ trong $16$ ô của bảng chuyển bằng $0$ hoặc chưa xác định.

**Bước 4: đọc bảng.** Với $m=1$, rủi ro thực nghiệm $1{,}070$ nhỏ hơn giá trị tốt nhất $1{,}0904$, còn lỗi kiểm tra bằng $+\infty$, nên mô hình *quá khớp* (overfitting). Làm trơn cộng một bỏ được $+\infty$; lỗi kiểm tra của nó cao hơn của mô hình thật khoảng $0{,}032$. Với $m=500$, lỗi kiểm tra $1{,}088$ nhỏ hơn $1{,}0904$, nhưng mô hình thật trên cùng mẫu kiểm tra cũng cho $1{,}088$, nên đây là dao động của mẫu kiểm tra.

**Kết luận.** Ba câu hỏi thực hành của §3: (i) với $m=50$, trung bình qua $10$ lần chạy, lỗi kiểm tra $1{,}091$ cách giá trị tốt nhất khoảng $0{,}0009$ và cách mô hình thật trên cùng mẫu kiểm tra khoảng $0{,}0007$; (ii) $+\infty$ đến từ các xác suất bằng $0$ của ước lượng hợp lý cực đại, và làm trơn bỏ được chúng; (iii) với mô hình làm trơn, có xác suất bị chặn dưới, khoảng tin cậy dùng số chuỗi kiểm tra làm cỡ mẫu (Ví dụ 09.4).
:::

Mô hình gán xác suất $0$ trên giá của $p_D$ có rủi ro $+\infty$.

## 8. Mô hình biến ẩn và cận dưới bằng chứng

Nhiều mô hình sinh rút một biến không quan sát được, rồi rút quan sát theo biến đó; độ hợp lý khi đó là một tổng hay một tích phân theo biến này. Khi mô hình quan sát là một mạng nơ-ron, tích phân này nói chung không tính được (Kingma và Welling, §2.1).

::: definition Định nghĩa 09.10 (Mô hình biến ẩn, bằng chứng và phân bố biến phân)
Cho tập quan sát $\mathcal X$, một tập $\mathcal V$ (hữu hạn, hoặc $\mathcal V=\mathbb R^r$) và tập tham số $\Theta$.

- **Biến ẩn.** $v\in\mathcal V$, không quan sát được (latent variable).
- **Mô hình biến ẩn.** Mật độ đồng thời $p_\theta(x,v)=p_\theta(v)\,p_\theta(x\mid v)$, gồm *tiên nghiệm* (prior) $p_\theta(v)$ và mô hình quan sát $p_\theta(x\mid v)$.
- **Bằng chứng.** $p_\theta(x)=\int_{\mathcal V}p_\theta(x,v)\,dv$, là tổng khi $\mathcal V$ hữu hạn; *bằng chứng* (evidence) là $\ln p_\theta(x)$.
- **Phân bố hậu nghiệm.** $p_\theta(v\mid x)=p_\theta(x,v)/p_\theta(x)$ khi $0<p_\theta(x)<\infty$ (posterior).
- **Phân bố biến phân.** Một họ mật độ $q_\phi(\cdot\mid x)$ trên $\mathcal V$, $\phi\in\Phi$, dùng để xấp xỉ $p_\theta(\cdot\mid x)$ (variational distribution); $\phi$ có thể dùng chung cho mọi $x$.
:::

Biến ẩn viết $v$ vì $z$ là quan sát (Kingma và Welling viết $z$); $\phi$ khác các ánh xạ $\phi$, $\phi_i$, $\phi_\gamma$ của bổ đề co ở Bài 07 và $\varphi$ của Bài 05, còn $r$ khác bán kính của Bài 02. Hàm lỗi vẫn là $-\ln p_\theta(x)$, nên §7 áp dụng cho $p_\theta(x)$. Câu ôn nhanh 3 là một mô hình biến ẩn với $\mathcal V=\{1,2\}$.

Nếu $x=v\sim N(0,1)$ không có nhiễu, hậu nghiệm dồn toàn bộ xác suất vào điểm $v=x$ (khối lượng điểm, point mass) và không có mật độ, nên phân kì KL từ một mật độ bất kì tới nó không hữu hạn.

::: example Ví dụ 09.9 (Mô hình Gauss tuyến tính một chiều)
**Thiết lập.** $\mathcal V=\mathcal X=\mathbb R$; $v\sim N(0,1)$ và $x\mid v\sim N(v,1)$. Mô hình không có tham số cần học; ta vẫn viết $p_\theta$. Quan sát cố định $x=2$.

**Bước 1: bằng chứng.** Quan sát $x$ là tổng của $v$ và một biến $N(0,1)$ độc lập với $v$, nên $x\sim N(0,2)$. Mật độ của $N(0,2)$ tại $2$ cho
$$
\begin{aligned}
\ln p_\theta(2)&=-\tfrac12\ln(4\pi)-1\\
&\approx-2{,}2655 .
\end{aligned}
$$

**Bước 2: hậu nghiệm.** Theo công thức Bayes, $p_\theta(v\mid x)$ tỉ lệ với $p_\theta(v)\,p_\theta(x\mid v)$. Hoàn thành bình phương (Phụ lục A):
$$
\begin{aligned}
&p_\theta(v\mid x)\\
&\propto\exp\big(-\tfrac12v^2-\tfrac12(x-v)^2\big)\\
&\propto\exp\big(-(v-\tfrac x2)^2\big).
\end{aligned}
$$
Do đó hậu nghiệm là $N(\tfrac x2,\tfrac12)$, tức $N(1,\tfrac12)$ tại $x=2$.

**Kết luận.** Trung bình hậu nghiệm $1$ nằm giữa trung bình tiên nghiệm $0$ và quan sát $2$, và phương sai giảm từ $1$ xuống $\tfrac12$. Bằng chứng và hậu nghiệm có dạng đóng, nên đo được sai số của mọi phân bố biến phân.
:::

Khi tích phân của bằng chứng không tính được, chúng ta làm việc với một đại lượng chỉ cần giá trị của $p_\theta(x,v)$.

::: definition Định nghĩa 09.11 (Cận dưới bằng chứng)
Cho $x$, $\theta$, $\phi$ cố định. *Cận dưới bằng chứng* (còn gọi là cận dưới biến phân) là
$$
\begin{aligned}
&\operatorname{ELBO}(\theta,\phi;x)\\
&=\mathbb E_{v\sim q_\phi(\cdot\mid x)}\ln\frac{p_\theta(x,v)}{q_\phi(v\mid x)},
\end{aligned}
$$
khi kì vọng xác định.
:::

Kì vọng lấy theo $q_\phi$, nên ELBO ước lượng được bằng cách rút $v$ từ $q_\phi$.

::: theorem Định lý 09.12 (Đồng nhất thức của cận dưới bằng chứng) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau; viết tắt $q=q_\phi(\cdot\mid x)$.

- **Mô hình.** $p_\theta(x,v)$ là mật độ (hoặc hàm xác suất) trên $\mathcal X\times\mathcal V$.
- **Quan sát.** $x$ cố định, với $0<p_\theta(x)<\infty$.
- **Phân bố biến phân.** $q$ là một mật độ trên $\mathcal V$ với $p_\theta(x,v)>0$ cho $q$-hầu hết $v$, tức $q$ không đặt khối lượng ở chỗ hậu nghiệm bằng $0$.
- **Khả tích.** $\mathbb E_q\lvert\ln p_\theta(x,v)\rvert<\infty$ và $\mathbb E_q\lvert\ln q(v)\rvert<\infty$.

**Bảo đảm.** Đồng nhất thức cho từng $x$; không có mẫu và không có xác suất theo $S$.

- **(a) Đồng nhất thức.** $\ln p_\theta(x)=\operatorname{ELBO}(\theta,\phi;x)+\mathrm{KL}\big(q\Vert p_\theta(\cdot\mid x)\big)$, mọi số hạng hữu hạn.
- **(b) Cận dưới.** $\operatorname{ELBO}(\theta,\phi;x)\le\ln p_\theta(x)$, dấu bằng khi và chỉ khi $q=p_\theta(\cdot\mid x)$ hầu khắp nơi.
- **(c) Tái tạo và KL.** Nếu thêm $\mathbb E_q\lvert\ln p_\theta(v)\rvert<\infty$, thì $\operatorname{ELBO}=\mathbb E_q\ln p_\theta(x\mid v)-\mathrm{KL}\big(q\Vert p_\theta(\cdot)\big)$: *số hạng tái tạo* (reconstruction term) trừ phân kì KL tới tiên nghiệm.
- **(d) Trên mẫu.** Với mẫu $s=(x^{(1)},\ldots,x^{(m)})$ thỏa các giả thiết tại mỗi $x^{(i)}$, $L_s(\theta)\le-\frac1m\sum_{i=1}^m\operatorname{ELBO}(\theta,\phi;x^{(i)})$.

Nếu $q$ đặt khối lượng dương ở chỗ $p_\theta(x,v)=0$ và $\mathbb E_q\lvert\ln q\rvert<\infty$, thì $\operatorname{ELBO}=-\infty$ và (b) đúng tầm thường.
:::

::: proof Chứng minh Định lý 09.12
**Lộ trình.** Viết công thức Bayes cho từng $v$, thêm bớt $\ln q(v)$, lấy kì vọng theo $q$, rồi nhận ra phân kì KL. Bất đẳng thức then chốt là $\mathrm{KL}\ge0$.

**Bước 1 (công thức Bayes; dùng $0<p_\theta(x)<\infty$).** Với $v$ có $p_\theta(x,v)>0$, hậu nghiệm $p_\theta(v\mid x)$ dương và
$$
\begin{aligned}
\ln p_\theta(x)&=\ln p_\theta(x,v)\\
&\quad-\ln p_\theta(v\mid x).
\end{aligned}
$$

**Bước 2 (thêm bớt $\ln q$; dùng giả thiết về $q$).** Với $q$-hầu hết $v$, Bước 1 áp dụng được, và
$$
\begin{aligned}
&\ln p_\theta(x)\\
&=\big[\ln p_\theta(x,v)-\ln q(v)\big]\\
&\quad+\big[\ln q(v)-\ln p_\theta(v\mid x)\big].
\end{aligned}
$$

**Bước 3 (lấy kì vọng; dùng tính khả tích).** Ngoặc thứ nhất khả tích theo giả thiết. Ngoặc thứ hai bằng hằng số $\ln p_\theta(x)$ trừ ngoặc thứ nhất, nên cũng khả tích. Lấy $\mathbb E_q$ hai vế: ngoặc thứ nhất cho ELBO (Định nghĩa 09.11), ngoặc thứ hai cho $\mathrm{KL}\big(q\Vert p_\theta(\cdot\mid x)\big)$ (Định nghĩa 09.7, bản mật độ). Ta được (a).

**Bước 4 ((b)).** Lập luận của Mệnh đề 09.8(c) (Bước 3–4 của chứng minh), áp dụng cho hai mật độ $q$ và $p_\theta(\cdot\mid x)$ trên $\mathcal V$ với tính khả tích của Bước 3, cho $\mathrm{KL}\ge0$, dấu bằng khi và chỉ khi $q=p_\theta(\cdot\mid x)$ hầu khắp nơi. Thay vào (a).

**Bước 5 ((c), (d)).** Viết $\ln p_\theta(x,v)=\ln p_\theta(x\mid v)+\ln p_\theta(v)$; với giả thiết thêm, cả hai số hạng khả tích theo $q$, và $\mathbb E_q[\ln p_\theta(v)-\ln q(v)]=-\mathrm{KL}\big(q\Vert p_\theta(\cdot)\big)$. Phần (d) là (b) tại mỗi $x^{(i)}$, đổi dấu rồi lấy trung bình.

$\square$ Cực đại hóa ELBO theo $\phi$ thu hẹp *khe* (gap) $\ln p_\theta(x)-\operatorname{ELBO}=\mathrm{KL}\big(q\Vert p_\theta(\cdot\mid x)\big)$ mà không đổi $\ln p_\theta(x)$. Tối thiểu hóa $-\frac1m\sum_i\operatorname{ELBO}(\theta,\phi;x^{(i)})$ theo $\theta$ là tối thiểu hóa một cận trên của rủi ro thực nghiệm với hàm lỗi log.
:::

::: example Ví dụ 09.10 (Số hạng tái tạo, phân kì KL và khe của cận)
**Thiết lập.** Mô hình của Ví dụ 09.9 tại $x=2$; họ biến phân $q_\phi=N(\mu,\sigma^2)$ với $\phi=(\mu,\sigma)$, $\sigma>0$.

**Bước 1: hai số hạng** (Định lý 09.12(c)). Vì $\mathbb E_{q_\phi}(2-v)^2=(2-\mu)^2+\sigma^2$, số hạng tái tạo bằng
$$
\begin{aligned}
&\mathbb E_{q_\phi}\ln p_\theta(2\mid v)\\
&=-\tfrac12\ln(2\pi)\\
&\quad-\tfrac12\big((2-\mu)^2+\sigma^2\big),
\end{aligned}
$$
với $-\tfrac12\ln(2\pi)\approx-0{,}9189$. Phân kì KL tới tiên nghiệm $N(0,1)$ là $\tfrac12(\mu^2+\sigma^2-1-\ln\sigma^2)$ (công thức sau Định nghĩa 09.7).

**Bước 2: bảng.** Cột KL của bảng thứ nhất là KL tới tiên nghiệm. Bảng thứ hai ghi ELBO, bằng tái tạo trừ KL (Định lý 09.12(c)), và khe $\ln p_\theta(2)-\operatorname{ELBO}$, với $\ln p_\theta(2)\approx-2{,}2655$.

| $\mu;\sigma^2$ | Tái tạo | KL |
|---|---|---|
| $0;1$ | $-3{,}4189$ | $0$ |
| $1;1$ | $-1{,}9189$ | $0{,}5$ |
| $0{,}8;0{,}5$ | $-1{,}8889$ | $0{,}4166$ |
| $1;0{,}5$ | $-1{,}6689$ | $0{,}5966$ |

| $\mu;\sigma^2$ | ELBO | Khe |
|---|---|---|
| $0;1$ | $-3{,}4189$ | $1{,}1534$ |
| $1;1$ | $-2{,}4189$ | $0{,}1534$ |
| $0{,}8;0{,}5$ | $-2{,}3055$ | $0{,}0400$ |
| $1;0{,}5$ | $-2{,}2655$ | $0$ |

**Bước 3: khe bằng KL tới hậu nghiệm.** Với dòng đầu, công thức KL giữa hai Gauss cho
$$
\begin{aligned}
&\mathrm{KL}\big(N(0,1)\Vert N(1,\tfrac12)\big)\\
&=\ln\sqrt{0{,}5}+\tfrac{1+1}{2\cdot0{,}5}-\tfrac12\\
&\approx-0{,}3466+2-0{,}5\\
&=1{,}1534,
\end{aligned}
$$
trùng cột khe của bảng thứ hai, đúng như Định lý 09.12(a). Ba dòng còn lại trùng đến bốn chữ số.

**Bước 4: cực đại hóa theo $\phi$.** Lấy đạo hàm của ELBO: $\partial_\mu\operatorname{ELBO}=(2-\mu)-\mu$ bằng $0$ tại $\mu=1$, và $\partial_\sigma\operatorname{ELBO}=-2\sigma+1/\sigma$ bằng $0$ tại $\sigma^2=\tfrac12$. Điểm dừng trùng với hậu nghiệm $N(1,\tfrac12)$, và giá trị lớn nhất bằng $\ln p_\theta(2)$, như Định lý 09.12(b).

**Kết luận.** Dòng đầu, với $q_\phi$ bằng tiên nghiệm, có KL tới tiên nghiệm bằng $0$ nhưng số hạng tái tạo thấp; dòng cuối có KL tới tiên nghiệm $0{,}5966$ nhưng số hạng tái tạo cao hơn, vì $q_\phi$ đặt $v$ gần quan sát, và khe bằng $0$.
:::

Khi $\mathcal V$ hữu hạn, cực đại hóa ELBO luân phiên theo phân bố biến phân và theo $\theta$ là thuật toán EM (UML §24.4.1). Ta viết $\operatorname{ELBO}(\theta,q;x)$ khi phân bố biến phân là một hàm xác suất $q$ cho trước trên $\mathcal V$; chỉ số $t$ dưới đây đếm các vòng lặp của EM.

::: corollary Hệ quả 09.13 (Thuật toán EM không làm giảm log độ hợp lý) — chứng minh đầy đủ (Phụ lục D)
**Giả thiết.** Ba thành phần sau.

- **Mô hình và mẫu.** $\mathcal V$ hữu hạn; mẫu $s=(x^{(1)},\ldots,x^{(m)})$ cố định; $\theta_t\in\Theta$ với $p_{\theta_t}(x^{(i)})>0$ cho mọi $i$.
- **Bước E.** $q_i=p_{\theta_t}(\cdot\mid x^{(i)})$, một phân bố riêng cho mỗi quan sát.
- **Bước M.** $\theta_{t+1}$ làm lớn nhất $\sum_i\mathbb E_{v\sim q_i}\ln p_\theta(x^{(i)},v)$ trên $\Theta$, với giá trị lớn nhất hữu hạn.

**Bảo đảm.** Tất định, trên mẫu cố định: $L_s(\theta_{t+1})\le L_s(\theta_t)$.
:::

Chứng minh ở Phụ lục D dùng Định lý 09.12(b) hai lần. Rủi ro thực nghiệm không tăng qua các vòng lặp; không có kết luận về hội tụ tới điểm cực tiểu toàn cục hay về cận nào của $L_D$.

Khi hậu nghiệm không có dạng đóng, bước E không tính được. Kingma và Welling (§2.1–§2.3) thay nó bằng một $q_\phi$ dùng chung cho mọi quan sát và cực đại hóa ELBO theo $(\theta,\phi)$ bằng SGD, với kì vọng lấy theo chính $q_\phi$.

## 9. Tái tham số hóa và so sánh các mô hình sinh

Để cực đại hóa ELBO bằng SGD, chúng ta cần gradient của $\phi\mapsto\mathbb E_{v\sim q_\phi}f(v)$. Phân bố lấy kì vọng phụ thuộc chính $\phi$, nên gradient này nói chung khác $\mathbb E_{v\sim q_\phi}\nabla_\phi f(v)$, vốn bằng $0$. Có hai cách: lấy đạo hàm của mật độ (ước lượng gradient log), hoặc chuyển sự phụ thuộc vào hàm lấy kì vọng (tái tham số hóa).

::: definition Định nghĩa 09.14 (Tái tham số hóa và hai ước lượng gradient)
Cho họ mật độ $q_\phi$ trên $\mathcal V=\mathbb R^r$, $\phi\in\Phi$, và hàm $f:\mathcal V\to\mathbb R$; đặt $F(\phi)=\mathbb E_{v\sim q_\phi}f(v)$.

- **Nhiễu phụ.** Một véc-tơ ngẫu nhiên $\zeta$ có phân bố cố định, không phụ thuộc $\phi$ (auxiliary noise); với họ Gauss, $\zeta\sim N(0,I_r)$.
- **Tái tham số hóa.** Một ánh xạ $g_\phi$ sao cho $g_\phi(\zeta)$ có phân bố $q_\phi$ với mọi $\phi$. Với $q_\phi=N(\mu_\phi,\operatorname{diag}\sigma_\phi^2)$, $g_\phi(\zeta)=\mu_\phi+\sigma_\phi\odot\zeta$, trong đó $\mu_\phi,\sigma_\phi\in\mathbb R^r$ có thể phụ thuộc $x$ và $\odot$ là tích từng thành phần.
- **Ước lượng gradient theo đường đi.** Với một lần rút $\zeta$: $\nabla_\phi\big[f(g_\phi(\zeta))\big]$ (pathwise gradient estimator).
- **Ước lượng gradient log.** Với một lần rút $v\sim q_\phi$: $f(v)\,\nabla_\phi\ln q_\phi(v)$ (score-function estimator).
:::

Vì $g_\phi(\zeta)$ có phân bố $q_\phi$, $F(\phi)=\mathbb E_\zeta f(g_\phi(\zeta))$ (Kingma và Welling, §2.4); cần xác định khi nào gradient của vế phải bằng kì vọng của gradient. Với ELBO, khi KL tới tiên nghiệm có dạng đóng (Định lý 09.12(c)), chỉ số hạng tái tạo cần rút mẫu.

::: proposition Mệnh đề 09.15 (Gradient theo đường đi không chệch) — phác thảo (chi tiết ở Phụ lục B)
**Giả thiết.** Các thành phần sau.

- **Nhiễu.** $\zeta$ là một véc-tơ ngẫu nhiên có phân bố không phụ thuộc $\phi$.
- **Tham số.** $\Phi$ là một tập mở của một không gian Euclid.
- **Hàm.** $\kappa(\phi,\zeta)$ đo được, với $\phi$ gồm mọi tham số cần lấy gradient; trong Định nghĩa 09.14, $\kappa(\phi,\zeta)=f(g_\phi(\zeta))$.
- **(i) Khả vi trên từng đường.** Có một tập $N_0$ xác suất $0$, không phụ thuộc $\phi$, sao cho với mọi $\zeta\notin N_0$, hàm $\phi\mapsto\kappa(\phi,\zeta)$ khả vi liên tục trên $\Phi$.
- **(ii) Hàm trội** (dominating function). Với mỗi $\phi_0\in\Phi$ có một lân cận $U\subseteq\Phi$ và một hàm $M\ge0$ với $\mathbb EM(\zeta)<\infty$, sao cho $\lVert\nabla_\phi\kappa(\phi,\zeta)\rVert\le M(\zeta)$ với mọi $\phi\in U$ và $\zeta\notin N_0$.
- **(iii) Khả tích.** $\mathbb E\lvert\kappa(\phi,\zeta)\rvert<\infty$ với mọi $\phi\in\Phi$.

**Bảo đảm.** Theo kì vọng theo nhiễu phụ $\zeta$, tất định theo $\phi$: $F(\phi)=\mathbb E\kappa(\phi,\zeta)$ khả vi trên $\Phi$ và $\nabla F(\phi)=\mathbb E\nabla_\phi\kappa(\phi,\zeta)$. Do đó với một lần rút $\zeta$, $\nabla_\phi\kappa(\phi,\zeta)$ là một ước lượng không chệch của $\nabla F(\phi)$. Phương sai của ước lượng chưa được chặn.

Một điều kiện đủ (Phụ lục B, Bước 6): $\zeta\sim N(0,I_r)$, $g_\phi(\zeta)=\mu_\phi+\sigma_\phi\odot\zeta$ với $\mu_\phi$, $\sigma_\phi$ khả vi liên tục, $f$ khả vi liên tục với $\lVert\nabla f(v)\rVert\le C(1+\lVert v\rVert^2)$ và $\lvert f(v)\rvert\le C(1+\lVert v\rVert^3)$ cho một hằng số $C$.
:::

::: proof Chứng minh Mệnh đề 09.15 (phác thảo)
**Lộ trình.** Định lý giá trị trung bình trên từng đường nhiễu, rồi định lý hội tụ bị chặn. Bất đẳng thức then chốt là cận của thương sai phân bởi hàm trội $M(\zeta)$.

**Bước 1 (định lý giá trị trung bình; dùng (i)).** Cố định $\phi_0$, một hướng đơn vị $e$ và $\lvert h\rvert$ đủ nhỏ để đoạn thẳng từ $\phi_0$ tới $\phi_0+he$ nằm trong $U$. Với $\zeta\notin N_0$, thương sai phân $\big(\kappa(\phi_0+he,\zeta)-\kappa(\phi_0,\zeta)\big)/h$ bằng đạo hàm theo hướng $e$ tại một điểm của đoạn. Bước này cần $\kappa(\cdot,\zeta)$ khả vi trên cả đoạn, nên tập ngoại lệ không được phụ thuộc $\phi$.

**Bước 2 (hàm trội và hội tụ bị chặn; dùng (ii), (iii)).** Thương sai phân bị chặn bởi $M(\zeta)$, khả tích. Theo (iii), thương sai phân của $F$ bằng kì vọng của thương sai phân của $\kappa$; cho $h\to0$, định lý hội tụ bị chặn cho đạo hàm theo hướng $e$ của $F$ tại $\phi_0$ bằng $\mathbb E\langle\nabla_\phi\kappa(\phi_0,\zeta),e\rangle$. Các đạo hàm riêng này liên tục, nên $F$ khả vi (Phụ lục B).

$\square$ Khi hàm dưới kì vọng của ELBO thỏa (i)–(iii), gradient một mẫu của ELBO là một gradient ngẫu nhiên không chệch; phương sai của nó cần một cận riêng, như (G2) của Bài 05.
:::

Với mẫu $s=(x^{(1)},\ldots,x^{(m)})$ và nguồn ngẫu nhiên $\xi=(i,\zeta)$, trong đó $i$ rút đều trên $\{1,\ldots,m\}$, đặt
$$
\begin{aligned}
&\kappa_i(\theta,\phi,\zeta)\\
&=\ln\frac{q_\phi\big(g_\phi(\zeta)\mid x^{(i)}\big)}{p_\theta\big(x^{(i)},g_\phi(\zeta)\big)}.
\end{aligned}
$$
Nếu với mỗi $i$, $\kappa_i$ thỏa (i)–(iii) của Mệnh đề 09.15 với $(\theta,\phi)$ ở chỗ của $\phi$, thì $\nabla_{\theta,\phi}\kappa_i(\theta,\phi,\zeta)$ là một gradient ngẫu nhiên không chệch của $-\frac1m\sum_i\operatorname{ELBO}(\theta,\phi;x^{(i)})$ (Thuật toán 1 của Kingma và Welling với một lần rút nhiễu, lô cỡ $1$). Định lý 05.14 còn cần (C), mà $-\operatorname{ELBO}$ nói chung không lồi theo $(\theta,\phi)$; Bài tập 09.7 xét một trường hợp lồi.

::: example Ví dụ 09.11 (Gradient theo đường đi trong mô hình Gauss)
**Thiết lập.** Ví dụ 09.10 tại $x=2$, $\Phi=\mathbb R\times(0,\infty)$ (mở). KL tới tiên nghiệm có dạng đóng, nên chỉ số hạng tái tạo được rút mẫu:
$$
\begin{aligned}
&\kappa(\mu,\sigma,\zeta)\\
&=-\tfrac12\ln(2\pi)-\tfrac12(2-\mu-\sigma\zeta)^2\\
&\quad-\tfrac12(\mu^2+\sigma^2-1-\ln\sigma^2).
\end{aligned}
$$

**Bước 1: gradient đúng tại $(\mu,\sigma)=(0,1)$.** Theo Ví dụ 09.10, Bước 4: $\partial_\mu\operatorname{ELBO}=2-2\mu=2$ và $\partial_\sigma\operatorname{ELBO}=-2\sigma+1/\sigma=-1$.

**Bước 2: ước lượng một mẫu.** Đạo hàm của $\kappa$ theo $\mu$ và $\sigma$ là
$$
\begin{aligned}
\partial_\mu\kappa&=(2-\mu-\sigma\zeta)-\mu,\\
\partial_\sigma\kappa&=(2-\mu-\sigma\zeta)\zeta\\
&\quad-\sigma+1/\sigma .
\end{aligned}
$$
Tại $(0,1)$, hai thành phần là $2-\zeta$ và $2\zeta-\zeta^2$. Với $\zeta=0{,}5$, ước lượng là $(1{,}5;\,0{,}75)$; với $\zeta=-1$, ước lượng là $(3;\,-3)$.

**Bước 3: không chệch.** $\mathbb E(2-\zeta)=2$ và $\mathbb E(2\zeta-\zeta^2)=-1$, đúng gradient ở Bước 1. Phương sai thành phần thứ nhất là $\operatorname{Var}\zeta=1$. Với thành phần thứ hai, dùng $\operatorname{Var}\zeta^2=3-1=2$ và $\operatorname{Cov}(\zeta,\zeta^2)=\mathbb E\zeta^3=0$:
$$
\begin{aligned}
&\operatorname{Var}(2\zeta-\zeta^2)\\
&=4\operatorname{Var}\zeta+\operatorname{Var}\zeta^2\\
&\quad-4\operatorname{Cov}(\zeta,\zeta^2)\\
&=4+2-0=6 .
\end{aligned}
$$

**Bước 4: kiểm điều kiện.** $\kappa$ khả vi liên tục với mọi $\zeta$, nên $N_0=\varnothing$; trên $U=\{\lvert\mu\rvert\le1,\ \sigma\in[\tfrac12,2]\}$, hai đạo hàm ở Bước 2 bị chặn bởi $C(1+\zeta^2)$, khả tích. Hàm $\kappa$ là đa thức bậc hai theo $\zeta$, nên (iii) thỏa.

**Bước 5: so với ước lượng gradient log.** Với $f(v)=-\tfrac12\ln(2\pi)-\tfrac12(2-v)^2$ và $\partial_\mu\ln q_\phi(v)=v-\mu$, ước lượng gradient log cho $\partial_\mu$ của số hạng tái tạo tại $(0,1)$ là $f(\zeta)\zeta$. Kì vọng của nó cũng bằng $2$, nhưng phương sai bằng $29{,}027$ (Phụ lục A).

**Kết luận.** Hai ước lượng đều không chệch ở đây, nhưng ước lượng theo đường đi có phương sai nhỏ hơn khoảng $29$ lần. Kingma và Welling (§2.2) ghi nhận ước lượng gradient log có phương sai rất cao.
:::

::: example Ví dụ 09.12 (Hàm chỉ thị và biến Bernoulli)
**Thiết lập.** Bước 1–3: $q_\mu=N(\mu,1)$, $\Phi=\mathbb R$, $v=\mu+\zeta$, $f(v)=\mathbb 1[v>0]$, nên $F(\mu)=\Pr(\zeta>-\mu)$. Bước 4: $q_\phi=\mathrm{Ber}(\phi)$, $v=\mathbb 1[U_0<\phi]$ với $U_0$ đều trên $[0,1]$, và $f(v)=v$.

**Bước 1: đạo hàm đúng.** $F'(\mu)=e^{-\mu^2/2}/\sqrt{2\pi}$, mật độ chuẩn tắc tại $\mu$; tại $\mu=0{,}5$, $F'(0{,}5)\approx0{,}3521$.

**Bước 2: ước lượng theo đường đi.** $\kappa(\mu,\zeta)=\mathbb 1[\mu+\zeta>0]$. Với mọi $\zeta\ne-\mu$, $\partial_\mu\kappa=0$, nên ước lượng bằng $0$ hầu chắc chắn và bị chệch.

**Bước 3: điều kiện bị vi phạm.** Với $\zeta$ cố định, $\mu\mapsto\mathbb 1[\mu+\zeta>0]$ nhảy tại $\mu=-\zeta\in\Phi$, nên không có tập ngoại lệ chung cho mọi $\mu$ và (i) không thỏa. Với mỗi $\mu$ cố định, $\kappa(\cdot,\zeta)$ vẫn khả vi tại $\mu$ cho hầu hết $\zeta$. Như vậy, khả vi tại từng $\mu$ hầu chắc chắn chưa đủ.

**Bước 4: biến rời rạc.** Với $v=\mathbb 1[U_0<\phi]$, $F(\phi)=\phi$ và $F'=1$, còn ước lượng theo đường đi bằng $0$. Ước lượng gradient log $f(v)\,\partial_\phi\ln q_\phi(v)=v/\phi$ có kì vọng $\phi\cdot\tfrac1\phi=1$, không chệch, với phương sai $1/\phi-1\approx2{,}333$ tại $\phi=0{,}3$.

**Kết luận.** Tái tham số hóa cần $f\circ g_\phi$ khả vi theo $\phi$ dọc từng đường nhiễu; với biến ẩn rời rạc, điều kiện này không thỏa và ước lượng theo đường đi bị chệch.
:::

Một mô hình sinh còn được dùng để rút điểm mới từ $p_\theta$; mức giống dữ liệu thật của các điểm sinh ra là một tiêu chí khác hàm lỗi log.

::: example Ví dụ 09.13 (Độ hợp lý và chất lượng dữ liệu sinh ra theo hai chiều)
**Thiết lập.** Bước 1–3: $D=N(0,I_p)$ trên $\mathbb R^p$ với $p=784$ (giá trị giả định), và ba mô hình: $p_{\theta_1}=N(0,I_p)$, chính là $D$; mô hình nhiễu $p_{\theta_2}=N(0,25I_p)$; *hỗn hợp* (mixture) $p_{\theta_3}=0{,}01\,p_{\theta_1}+0{,}99\,p_{\theta_2}$. Bước 4 dùng thiết lập của Ví dụ 09.8 với $50$ chuỗi huấn luyện.

**Bước 1: một bất đẳng thức sơ cấp.** Với mọi $x$, $p_{\theta_3}(x)\ge0{,}01\,p_{\theta_1}(x)$, nên $-\ln p_{\theta_3}(x)\le-\ln p_{\theta_1}(x)+\ln100$. Lấy kì vọng theo $D$: $L_D(\theta_3)\le L_D(\theta_1)+4{,}6052$.

**Bước 2: theo tọa độ.** $L_D(\theta_1)/p=\tfrac12\ln(2\pi e)\approx1{,}4189$, chính là entropy vi phân của $D$ chia cho $p$, cũng là cận dưới của Mệnh đề 09.8(c). Do đó
$$
\begin{aligned}
1{,}4189&\le L_D(\theta_3)/p\\
&\le1{,}4189+4{,}6052/784\\
&\le1{,}4249,
\end{aligned}
$$
trong khi mô hình nhiễu có $L_D(\theta_2)/p=\tfrac12\ln(50\pi)+\tfrac1{50}\approx2{,}5484$.

**Bước 3: điểm sinh ra.** $99\%$ điểm rút từ $p_{\theta_3}$ đến từ thành phần nhiễu, với độ lệch chuẩn $5$ ở mỗi tọa độ thay vì $1$.

**Bước 4: chiều ngược lại.** *Mô hình ghi nhớ* (memorizing model) đặt xác suất $\tfrac1{50}$ lên mỗi chuỗi trong $50$ chuỗi huấn luyện của Ví dụ 09.8. Mọi chuỗi sinh ra là một chuỗi thật. Một chuỗi có xác suất lớn nhất $\tfrac14\cdot0{,}6^{199}$, khi mọi kí tự giữ nguyên, nên một chuỗi kiểm tra mới trùng một chuỗi huấn luyện với xác suất không quá $50\cdot\tfrac14\cdot0{,}6^{199}\approx8{,}9\cdot10^{-44}$. Do đó hàm lỗi log kiểm tra gần như chắc chắn bằng $+\infty$.

**Kết luận.** Hàm lỗi log gần tối ưu không bảo đảm dữ liệu sinh ra giống dữ liệu thật, và dữ liệu sinh ra giống dữ liệu thật không bảo đảm hàm lỗi log hữu hạn.
:::

Gradient theo đường đi của ELBO không chệch khi hàm dưới kì vọng thỏa (i)–(iii) của Mệnh đề 09.15; với biến ẩn rời rạc, (i) không thỏa (Ví dụ 09.12). Hai tiêu chí của Ví dụ 09.13 có thể xếp các mô hình theo hai thứ tự ngược nhau, nên được báo cáo riêng.

## 10. Ý nghĩa, tác động và giới hạn

Học một phân bố là ERM với hàm lỗi log, tức ước lượng hợp lý cực đại; giá trị tốt nhất là entropy của phân bố thật, phần vượt là phân kì KL thuận (Mệnh đề 09.8, Hệ quả 09.9). Với chuỗi, hàm lỗi là tổng các hàm lỗi có điều kiện (Mệnh đề 09.3), nhưng quan sát độc lập là cả chuỗi: với $50$ chuỗi, bán kính Hoeffding theo kí tự là $0{,}5754$ (Ví dụ 09.4). Với mô hình biến ẩn, gradient tái tham số hóa là một gradient ngẫu nhiên không chệch khi các điều kiện của Mệnh đề 09.15 thỏa.

Mệnh đề 09.3 và Định lý 09.12 là đồng nhất thức; Mệnh đề 09.8 và Hệ quả 09.9 là kết quả tổng thể. Bảo đảm cho mẫu hữu hạn chỉ có ở Ví dụ 09.4, cho một mô hình cố định có $c>0$ trên mẫu kiểm tra, và Bài tập 09.9, cho ước lượng có hai quan sát giả; ước lượng hợp lý cực đại không chính quy hóa có $\mathbb E_SL_D(\hat\theta)=+\infty$ với mọi $m$ trong Ví dụ 09.7.

Các giới hạn chính như sau.

- **Hàm lỗi log không bị chặn.** Cần một cận dưới cho xác suất của mô hình (§2; Ví dụ 09.7).
- **Phụ thuộc giữa các kí tự.** Bán kính $0{,}0407$ của phép đếm theo kí tự không được Định lý 02.7 chứng minh (Ví dụ 09.4); chia ngẫu nhiên các cửa sổ cho MSE $0{,}20$, dưới rủi ro nhỏ nhất $1$ (Ví dụ 09.5).
- **Độ hợp lý và dữ liệu sinh ra.** Hỗn hợp cách giá trị tối ưu không quá $0{,}0059$ nat mỗi tọa độ, nhưng $99\%$ điểm rút từ nó là nhiễu (Ví dụ 09.13).
- **Khe của cận dưới bằng chứng.** ELBO thấp hơn log độ hợp lý đúng bằng phân kì KL tới hậu nghiệm, bằng $1{,}1534$ khi $q_\phi$ là tiên nghiệm (Ví dụ 09.10).
- **Điều kiện của tái tham số hóa.** Với hàm chỉ thị hay biến rời rạc, ước lượng theo đường đi cho $0$ thay cho $0{,}3521$ (Ví dụ 09.12).
- **Tối ưu không lồi.** $-\operatorname{ELBO}$ nói chung không thỏa (C) (§9).

Mạng đối kháng sinh (generative adversarial network, GAN) và mô hình khuếch tán (diffusion model) là các mô hình sinh khác; mục tiêu huấn luyện và cách đánh giá chúng nằm ngoài phạm vi bài.

## 11. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 09](material-viewer.html?doc=materials/lec-09/exercises.md); bảy bài đầu là bài gốc, ba bài sau chọn từ UML.

1. **Bài tập 09.1** (Độ hợp lý, hàm lỗi log trung bình và độ bối rối từ một bảng): mục tiêu 1.
2. **Bài tập 09.2** (Rò rỉ thông tin khi chia ngẫu nhiên cửa sổ chồng lấn): mục tiêu 3.
3. **Bài tập 09.3** (Entropy chéo, entropy và phân kì KL): mục tiêu 2.
4. **Bài tập 09.4** (Cận dưới bằng chứng và điều kiện dấu bằng): mục tiêu 4, 5.
5. **Bài tập 09.5** (Mục tiêu theo kí tự và theo chuỗi với hai độ dài chuỗi): mục tiêu 3.
6. **Bài tập 09.6** (Mô hình bigram, hàm lỗi log kiểm tra và chuỗi sinh ra; thực nghiệm tùy chọn): mục tiêu 3.
7. **Bài tập 09.7** (SGD với gradient theo đường đi cho một mục tiêu lồi): mục tiêu 5.
8. **Bài tập 09.8** (Ước lượng hợp lý cực đại của phương sai Gauss bị chệch; UML Bài tập 24.1): mục tiêu 2.
9. **Bài tập 09.9** (Ước lượng hợp lý cực đại có chính quy hóa cho phân bố Bernoulli; UML Bài tập 24.2): mục tiêu 2.
10. **Bài tập 09.10** (Tùy chọn: bước M cho trọng số hỗn hợp; UML Bài tập 24.3): mục tiêu 2, 4.

## 12. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Dùng mô hình hai kí tự của Ví dụ 09.1 và mô hình Gauss của Ví dụ 09.9.

(a) Tính độ hợp lý, hàm lỗi log, hàm lỗi log trung bình theo kí tự và độ bối rối của chuỗi $\mathtt{BBA}$.

(b) Một chuỗi đo hằng ngày dài $10^4$ ngày được cắt thành các cửa sổ ngữ cảnh $30$ ngày, bước trượt một ngày, rồi chia ngẫu nhiên $80\%$ cửa sổ cho huấn luyện và $20\%$ cho kiểm tra. Hệ quả 02.10 có cho một khoảng tin cậy cho rủi ro trên dữ liệu mới từ lỗi trên các cửa sổ kiểm tra không?

(c) Với $x=2$ và $q_\phi=N(0{,}8;\,0{,}5)$, cận dưới bằng chứng bằng $-2{,}3055$ và $\ln p_\theta(2)\approx-2{,}2655$. Tính $\mathrm{KL}\big(q_\phi\Vert p_\theta(\cdot\mid2)\big)$. Đổi $q_\phi$ có làm thay đổi $\ln p_\theta(2)$ không?

(d) Biến ẩn nhận giá trị trong $\{0,1\}$ với $\Pr(v=1)=\phi$. Với tái tham số hóa $v=\mathbb 1[U_0<\phi]$, $U_0$ đều trên $[0,1]$, ước lượng gradient theo đường đi có cho một ước lượng không chệch của $\frac{d}{d\phi}\mathbb Ev$ không? Ước lượng nào trong bài cho một ước lượng không chệch trong trường hợp này?

::: solution Lời giải câu hỏi cuối buổi
**(a)** Theo Mệnh đề 09.3, độ hợp lý là $\tfrac25\cdot\tfrac25\cdot\tfrac35=\tfrac{12}{125}=0{,}096$, và hàm lỗi log là
$$
\begin{aligned}
\ell&=0{,}9163+0{,}9163+0{,}5108\\
&=2{,}3434 .
\end{aligned}
$$
Chia cho $3$: $0{,}7811$; độ bối rối $e^{0{,}7811}\approx2{,}184$.

**(b)** Không. Đích của một cửa sổ kiểm tra nằm trong ngữ cảnh của các cửa sổ huấn luyện kề nó, nên (T7) không thỏa (Ví dụ 09.5). Chia theo thời gian bỏ được rò rỉ, nhưng các cửa sổ kiểm tra vẫn phụ thuộc nhau (Thiết lập B), nên Hệ quả 02.10 cần thêm giả thiết về sự phụ thuộc.

**(c)** Theo Định lý 09.12(a),
$$
\begin{aligned}
\mathrm{KL}&=\ln p_\theta(2)-\operatorname{ELBO}\\
&=-2{,}2655+2{,}3055\\
&=0{,}0400,
\end{aligned}
$$
trùng dòng thứ ba của bảng trong Ví dụ 09.10. Đại lượng $\ln p_\theta(2)$ chỉ phụ thuộc mô hình và $x$, nên đổi $q_\phi$ không đổi nó, chỉ đổi khe.

**(d)** Không. Đạo hàm theo đường đi bằng $0$, trong khi $\frac d{d\phi}\mathbb Ev=1$ (Ví dụ 09.12, Bước 4); điều kiện (i) của Mệnh đề 09.15 không thỏa. Ước lượng gradient log $v/\phi$ có kì vọng $1$.
:::

Trong cả bài, dữ liệu đến từ một phân bố $D$ cố định, không phụ thuộc tham số. Trong mục tiêu huấn luyện, phân bố lấy kì vọng duy nhất phụ thuộc tham số đang tối ưu là phân bố biến phân ($q_\phi$ hoặc $q_i$), và thuật toán học chọn nó. Câu hỏi cho Bài 10 là: điều gì thay đổi khi các hành động rời rạc của một tác tử quyết định quan sát tiếp theo, nên phân bố của dữ liệu phụ thuộc chính tham số đang học? Điều gì thay đổi khi phân bố dữ liệu thay đổi trong lúc học?

## 13. Tài liệu đọc

- **Trước buổi học:** UML §24.1 (ước lượng hợp lý cực đại; §24.1.2 ước lượng hợp lý cực đại và ERM; §24.1.3 phân tích tổng quát hóa).
- **Sau buổi học:** UML §24.4 và §24.4.1 (biến ẩn, thuật toán EM, EM như cực đại hóa luân phiên); D. P. Kingma, M. Welling (2014), *Auto-Encoding Variational Bayes*, ICLR, §2.1–2.4, §3 và Phụ lục B.
- **Mở rộng:** UML §24.4.2 (EM cho hỗn hợp Gauss), §24.2 (Naive Bayes).

**Quan hệ với nguồn.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML và bài báo của Kingma và Welling được dẫn theo mục. Các khác biệt chính:

- **Kí hiệu.** UML viết $L(S;\theta)$ cho log độ hợp lý của mẫu và cực đại hóa nó, tức $L(S;\theta)=-m\,L_S(\theta)$. Cả hai nguồn viết $\log$ cho logarit tự nhiên; học phần viết $\ln$. Kingma và Welling viết $z$, $\epsilon$, $\mathcal L$, $N$ cho biến ẩn, nhiễu phụ, cận dưới và cỡ dữ liệu; học phần viết $v$, $\zeta$, $\operatorname{ELBO}$, $m$, vì $z$, $\epsilon$, $L$ đã có nghĩa khác.
- **Entropy tương đối.** UML phát biểu phân tích rủi ro thành entropy cộng entropy tương đối cho biến rời rạc; học phần thêm điều kiện giá, điều kiện entropy hữu hạn và bản mật độ (Mệnh đề 09.8).
- **Cận dưới.** UML (§24.4) dẫn tới cận dưới qua thuật toán EM, với biến ẩn rời rạc, tổng theo các quan sát và một phân bố tự do cho mỗi quan sát; học phần phát biểu đồng nhất thức cho mật độ tổng quát (Định lý 09.12) và suy ra tính đơn điệu của EM (Hệ quả 09.13).
- **Kingma và Welling.** Bài báo nêu đồng nhất thức và dạng tái tạo trừ KL không kèm chứng minh, giả sử các mật độ khả vi hầu khắp nơi (§2.1) và nhắc tới "một số điều kiện nhẹ" cho tái tham số hóa. Học phần nêu các điều kiện của Định lý 09.12, một điều kiện đủ cụ thể (Mệnh đề 09.15) và một ví dụ cho thấy khả vi hầu khắp nơi tại từng tham số chưa đủ (Ví dụ 09.12).

## Phụ lục

### A. Các phép tính Gauss

**(i) Phân kì KL giữa hai phân bố Gauss một chiều.** Với $V\sim N(\mu_1,\sigma_1^2)$ và $p_i$ là mật độ của $N(\mu_i,\sigma_i^2)$, $\ln p_i(v)=-\tfrac12\ln(2\pi\sigma_i^2)-(v-\mu_i)^2/(2\sigma_i^2)$. Lấy kì vọng của $\ln p_1(V)-\ln p_2(V)$, dùng $\mathbb E(V-\mu_1)^2=\sigma_1^2$ và $\mathbb E(V-\mu_2)^2=\sigma_1^2+(\mu_1-\mu_2)^2$:
$$
\begin{aligned}
&\mathrm{KL}\big(N(\mu_1,\sigma_1^2)\Vert N(\mu_2,\sigma_2^2)\big)\\
&=\ln\frac{\sigma_2}{\sigma_1}-\frac{\mathbb E(V-\mu_1)^2}{2\sigma_1^2}\\
&\quad+\frac{\mathbb E(V-\mu_2)^2}{2\sigma_2^2}\\
&=\ln\frac{\sigma_2}{\sigma_1}-\frac12+\frac{\sigma_1^2+(\mu_1-\mu_2)^2}{2\sigma_2^2}.
\end{aligned}
$$
Với $(\mu_1,\sigma_1^2)=(0,1)$ và $(\mu_2,\sigma_2^2)=(1,\tfrac12)$, giá trị là $\ln\sqrt{0{,}5}-\tfrac12+2\approx1{,}1534$. Với $\mu_2=0$, $\sigma_2=1$, ta được $\tfrac12(\mu_1^2+\sigma_1^2-1-\ln\sigma_1^2)$, trùng công thức ở Phụ lục B của Kingma và Welling cho một chiều. Với hai phân bố Gauss nhiều chiều có ma trận hiệp phương sai đường chéo, các tọa độ độc lập, nên phân kì KL là tổng của các phân kì theo từng tọa độ.

**(ii) Bằng chứng và hậu nghiệm của Ví dụ 09.9.** Mật độ đồng thời là $p_\theta(x,v)=\frac1{2\pi}\exp\big(-\tfrac{v^2}2-\tfrac{(x-v)^2}2\big)$. Hoàn thành bình phương theo $v$:
$$
\begin{aligned}
\frac{v^2}2+\frac{(x-v)^2}2&=v^2-xv+\frac{x^2}2\\
&=\Big(v-\frac x2\Big)^2+\frac{x^2}4 .
\end{aligned}
$$
Tích phân theo $v$ của $\exp\big(-(v-\tfrac x2)^2\big)$ bằng $\sqrt\pi$, nên $p_\theta(x)=\frac{\sqrt\pi}{2\pi}e^{-x^2/4}=\frac1{2\sqrt\pi}e^{-x^2/4}$, đúng mật độ của $N(0,2)$. Chia $p_\theta(x,v)$ cho $p_\theta(x)$, hậu nghiệm tỉ lệ với $\exp\big(-(v-\tfrac x2)^2\big)$, tức $N(\tfrac x2,\tfrac12)$.

**(iii) ELBO dạng đóng.** Với $x=2$ và $q_\phi=N(\mu,\sigma^2)$, cộng hai số hạng của Ví dụ 09.10, Bước 1:
$$
\begin{aligned}
&\operatorname{ELBO}(\mu,\sigma)\\
&=-\tfrac12\ln(2\pi)-\tfrac12(2-\mu)^2\\
&\quad-\tfrac12\mu^2-\sigma^2+\tfrac12+\ln\sigma .
\end{aligned}
$$
Các đạo hàm riêng là $\partial_\mu\operatorname{ELBO}=2-2\mu$ và $\partial_\sigma\operatorname{ELBO}=-2\sigma+1/\sigma$. Ma trận Hesse của $-\operatorname{ELBO}$ là $\operatorname{diag}(2,\,2+1/\sigma^2)$, xác định dương trên $\sigma>0$, nên $-\operatorname{ELBO}$ lồi ngặt và điểm dừng duy nhất $(\mu,\sigma)=(1,1/\sqrt2)$ là điểm cực đại toàn cục của ELBO. Thay vào, giá trị lớn nhất là $-\tfrac12\ln(2\pi)-1-\tfrac12\ln2=-\tfrac12\ln(4\pi)-1=\ln p_\theta(2)$, đúng như Định lý 09.12(b). Tính lồi này được dùng lại ở Bài tập 09.7.

**(iv) Phương sai ở Ví dụ 09.11, Bước 5.** Đặt $a=\tfrac12\ln(2\pi)\approx0{,}9189$. Khai triển $(2-\zeta)^2\zeta=4\zeta-4\zeta^2+\zeta^3$, nên
$$
f(\zeta)\zeta=-(a+2)\zeta+2\zeta^2-\tfrac12\zeta^3 .
$$
Các mô-men lẻ của $\zeta\sim N(0,1)$ bằng $0$, và $\mathbb E\zeta^2=1$, $\mathbb E\zeta^4=3$, $\mathbb E\zeta^6=15$. Do đó kì vọng bằng $2$, và
$$
\begin{aligned}
&\mathbb E\big(f(\zeta)\zeta\big)^2\\
&=(a+2)^2+4\cdot3+\tfrac14\cdot15\\
&\quad+2\cdot(a+2)\cdot\tfrac12\cdot3\\
&=(a+2)^2+3(a+2)+15{,}75,\\
&\operatorname{Var}\big(f(\zeta)\zeta\big)\\
&=(a+2)(a+5)+11{,}75\approx29{,}027 .
\end{aligned}
$$
Số hạng chéo giữa $-(a+2)\zeta$ và $-\tfrac12\zeta^3$ cho $2\cdot(a+2)\cdot\tfrac12\cdot\mathbb E\zeta^4$; các số hạng chéo khác chứa mô-men lẻ và bằng $0$.

### B. Đổi chỗ đạo hàm và kì vọng

Kí hiệu $\langle\cdot,\cdot\rangle$ là tích vô hướng Euclid và $D_eF$ là đạo hàm theo hướng đơn vị $e$.

::: proof Chứng minh Mệnh đề 09.15
**Lộ trình.** Định lý giá trị trung bình trên từng đường nhiễu, định lý hội tụ bị chặn cho các đạo hàm theo hướng, định lý hội tụ bị chặn lần nữa cho tính liên tục, rồi dùng sự kiện "đạo hàm riêng liên tục kéo theo khả vi". Bất đẳng thức then chốt là cận $M(\zeta)$ cho trị tuyệt đối của thương sai phân.

**Bước 1 (định lý giá trị trung bình; dùng (i)).** Cố định $\phi_0\in\Phi$ và lấy $U$, $M$ như (ii); thu nhỏ $U$ thành một quả cầu mở tâm $\phi_0$ bán kính $h_0$ nếu cần, nên $U$ lồi. Cố định một hướng đơn vị $e$ và $0<\lvert h\rvert<h_0$. Với $\zeta\notin N_0$, hàm một biến $s\mapsto\kappa(\phi_0+se,\zeta)$ khả vi trên đoạn nối $0$ và $h$, nên theo định lý giá trị trung bình có $\tau\in(0,1)$ với
$$
\begin{aligned}
&\frac{\kappa(\phi_0+he,\zeta)-\kappa(\phi_0,\zeta)}h\\
&=\big\langle\nabla_\phi\kappa(\phi_0+\tau he,\zeta),e\big\rangle .
\end{aligned}
$$
Bước này cần $\kappa(\cdot,\zeta)$ khả vi tại mọi điểm của đoạn, với cùng một $\zeta$. Nếu tập ngoại lệ phụ thuộc $\phi$, hợp của các tập ngoại lệ trên đoạn có thể có xác suất dương: trong Ví dụ 09.12, tập ngoại lệ tại $\mu$ là $\{-\mu\}$, và hợp theo $\mu$ trong một khoảng $I$ là khoảng đối $\{-\mu:\mu\in I\}$, có xác suất dương.

**Bước 2 (hàm trội; dùng (ii)).** Điểm $\phi_0+\tau he$ nằm trong $U$, nên thương sai phân ở Bước 1 có trị tuyệt đối không quá $M(\zeta)$ với mọi $\zeta\notin N_0$, và $\mathbb EM(\zeta)<\infty$.

**Bước 3 (hội tụ bị chặn; dùng (iii)).** Theo (iii), $F(\phi_0+he)$ và $F(\phi_0)$ hữu hạn, nên thương sai phân của $F$ bằng kì vọng của thương sai phân của $\kappa$. Khi $h\to0$, với $\zeta\notin N_0$, thương sai phân của $\kappa$ tiến tới $\langle\nabla_\phi\kappa(\phi_0,\zeta),e\rangle$ theo (i), và bị chặn bởi $M(\zeta)$ theo Bước 2. Định lý hội tụ bị chặn cho
$$
D_eF(\phi_0)=\mathbb E\big\langle\nabla_\phi\kappa(\phi_0,\zeta),e\big\rangle .
$$
Cũng theo (ii), $\mathbb E\lVert\nabla_\phi\kappa(\phi_0,\zeta)\rVert\le\mathbb EM(\zeta)<\infty$, nên vế phải xác định.

**Bước 4 (tính liên tục).** Cho $\phi_k\to\phi_0$ trong $U$. Với $\zeta\notin N_0$, $\nabla_\phi\kappa(\phi_k,\zeta)\to\nabla_\phi\kappa(\phi_0,\zeta)$ vì $\kappa(\cdot,\zeta)$ khả vi liên tục theo (i), và các chuẩn bị chặn bởi $M(\zeta)$. Định lý hội tụ bị chặn cho $\mathbb E\nabla_\phi\kappa(\phi_k,\zeta)\to\mathbb E\nabla_\phi\kappa(\phi_0,\zeta)$, nên các đạo hàm riêng của $F$ liên tục tại $\phi_0$; vì $\phi_0$ tùy ý, chúng liên tục trên $\Phi$.

**Bước 5 (khả vi).** Một hàm có mọi đạo hàm riêng tồn tại và liên tục trên một tập mở thì khả vi trên tập đó, với gradient là véc-tơ các đạo hàm riêng. Áp dụng trên $\Phi$: $F$ khả vi và $\nabla F(\phi)=\mathbb E\nabla_\phi\kappa(\phi,\zeta)$.

**Bước 6 (trường hợp Gauss).** Với $\kappa(\phi,\zeta)=f(\mu_\phi+\sigma_\phi\odot\zeta)$, quy tắc dây chuyền cho $\nabla_\phi\kappa=J_\phi(\zeta)^\top\nabla f\big(g_\phi(\zeta)\big)$, với ma trận Jacobi $J_\phi(\zeta)=D\mu_\phi+\operatorname{diag}(\zeta)\,D\sigma_\phi$. Trên một quả cầu đóng $\bar U\subset\Phi$ quanh $\phi_0$, các hàm liên tục $\lVert\mu_\phi\rVert$, $\lVert\sigma_\phi\rVert$, $\lVert D\mu_\phi\rVert$, $\lVert D\sigma_\phi\rVert$ bị chặn bởi một hằng số $K$. Do đó $\lVert J_\phi(\zeta)\rVert\le K(1+\lVert\zeta\rVert)$ và $\lVert g_\phi(\zeta)\rVert\le K(1+\lVert\zeta\rVert)$, nên $\lVert\nabla f(g_\phi(\zeta))\rVert\le C'(1+\lVert\zeta\rVert^2)$ và
$$
\begin{aligned}
&\lVert\nabla_\phi\kappa(\phi,\zeta)\rVert\\
&\le C''(1+\lVert\zeta\rVert^3)=M(\zeta).
\end{aligned}
$$
Mô-men bậc ba của $\zeta\sim N(0,I_r)$ hữu hạn, nên (ii) thỏa; cùng cách chặn với $\lvert f(v)\rvert\le C(1+\lVert v\rVert^3)$ cho (iii). Hàm $\phi\mapsto\kappa(\phi,\zeta)$ là hợp của các hàm khả vi liên tục với mọi $\zeta$, nên (i) thỏa với $N_0=\varnothing$.

$\square$ Gradient một mẫu không chệch là điều kiện (G1) của Bài 05 cho một hàm mục tiêu khả vi; phương sai của nó, điều kiện (G2), phải chặn riêng, như Bài tập 09.7 làm trên một tập tham số có $\sigma\ge\tfrac12$.
:::

### C. Giao thức thí nghiệm

Các số của Ví dụ 09.5 và 09.8 là kết quả thí nghiệm cho một thiết lập, không phải chứng minh. Giao thức dưới đây đủ để tái lập bảng của Ví dụ 09.8, các số của Ví dụ 09.5 và chuỗi sinh ra của Bài tập 09.6; chỉ cần thư viện NumPy.

- **Dữ liệu bigram.** Xích Markov trên $\{\mathtt A,\mathtt C,\mathtt G,\mathtt T\}$, kí tự đầu rút đều, độ dài $n=200$, với bảng chuyển (hàng là kí tự đứng trước, cột là kí tự kế tiếp) như bảng dưới. Mỗi hàng và mỗi cột có tổng $1$, nên mọi kí tự có phân bố đều. Mọi giá trị là giá trị giả định.

  | | $\mathtt A$ | $\mathtt C$ | $\mathtt G$ | $\mathtt T$ |
  |---|---|---|---|---|
  | $\mathtt A$ | $0{,}6$ | $0{,}2$ | $0{,}1$ | $0{,}1$ |
  | $\mathtt C$ | $0{,}1$ | $0{,}6$ | $0{,}2$ | $0{,}1$ |
  | $\mathtt G$ | $0{,}1$ | $0{,}1$ | $0{,}6$ | $0{,}2$ |
  | $\mathtt T$ | $0{,}2$ | $0{,}1$ | $0{,}1$ | $0{,}6$ |

- **Mẫu.** $m\in\{1,5,50,500\}$ chuỗi huấn luyện và $200$ chuỗi kiểm tra, rút độc lập trong mỗi lần chạy. Mọi giả thiết của Thiết lập A thỏa, và lớp bigram chứa mô hình thật.
- **Ước lượng.** Ước lượng hợp lý cực đại: tần suất kí tự đầu và tần suất chuyển; một hàng chưa gặp không xác định và được tính như xác suất $0$. Làm trơn cộng một: cộng $1$ vào mọi ô đếm, cả kí tự đầu lẫn bảng chuyển.
- **Đại lượng.** Hàm lỗi log trung bình theo kí tự (tổng $-\ln$ xác suất chia cho tổng số kí tự) trên mẫu huấn luyện và mẫu kiểm tra; của mô hình thật trên cùng mẫu kiểm tra; số lần chạy có $+\infty$ theo nguyên nhân (kí tự đầu chưa gặp hay chuyển tiếp chưa gặp); giá trị tốt nhất $\mathrm H(p_D)/200\approx1{,}0904$.
- **Chuỗi sinh ra.** $40$ kí tự từ mô hình làm trơn học trên $m=50$ chuỗi của lần chạy với hạt giống $0$; đếm tỉ lệ cặp kí tự liền nhau giống nhau.
- **Cửa sổ chồng lấn.** Ví dụ 09.5: chuỗi $5000$ giá trị độc lập $N(0,1)$, $k=10$, $4990$ cửa sổ, $998$ cửa sổ kiểm tra; chia ngẫu nhiên bằng một hoán vị và chia theo thời gian; hàm dự đoán ghi nhớ tra theo chín giá trị đầu của ngữ cảnh. Phần này thuộc Thiết lập B.
- **Lặp lại.** Mười hạt giống $0,\ldots,9$, mỗi hạt giống khởi tạo bộ sinh `numpy.random.default_rng`; thứ tự rút cố định: mẫu huấn luyện rồi mẫu kiểm tra (phần bigram), chuỗi rồi hoán vị (phần cửa sổ). Chuỗi huấn luyện $12$ kí tự của Ví dụ 09.8 là $12$ kí tự đầu của một chuỗi rút với hạt giống $3$.
- **Làm tròn.** Số đo làm tròn đến giá trị gần nhất, ba chữ số thập phân; chỉ cận trên của các kết quả được làm tròn lên. Cả mười hạt giống, hai phần, chạy trong khoảng một giây.

Kết quả bổ sung cho bảng của Ví dụ 09.8 (nhỏ nhất – lớn nhất qua mười lần chạy). Với làm trơn cộng một, lỗi kiểm tra nằm trong $[1{,}104;\,1{,}147]$, $[1{,}089;\,1{,}109]$, $[1{,}085;\,1{,}099]$, $[1{,}083;\,1{,}092]$ với $m=1$, $5$, $50$, $500$; lỗi huấn luyện trung bình là $1{,}077$; $1{,}080$; $1{,}090$; $1{,}090$. Mô hình thật trên các mẫu kiểm tra nằm trong $[1{,}082;\,1{,}098]$. Mọi giá trị $+\infty$ của ước lượng hợp lý cực đại đến từ kí tự đầu chưa gặp: $10/10$ lần chạy với $m=1$, $5/10$ với $m=5$. Chuỗi sinh ra là $\mathtt{GTTTTTTCCT}$ $\mathtt{TGGGTCGTAC}$ $\mathtt{CGGAAAGGGT}$ $\mathtt{TAGTACGGGA}$, với $18$ trong $39$ cặp liền nhau giữ nguyên kí tự ($0{,}46$, so với $0{,}6$ của xích thật). Với cửa sổ chồng lấn, chia ngẫu nhiên cho trung bình $0{,}1995$ (bốn chữ số; ghi $0{,}200$ ở Ví dụ 09.5); dự đoán $0$ trên mẫu kiểm tra theo thời gian cho cùng các số với chia theo thời gian: trung bình $0{,}994$, từ $0{,}915$ đến $1{,}066$.

### D. Chứng minh Mệnh đề 09.3 và Hệ quả 09.13

::: proof Chứng minh Mệnh đề 09.3
**Lộ trình.** Phần (a) nhân các đẳng thức của định nghĩa xác suất có điều kiện theo $j$; (b) lấy $-\ln$; (c) lấy tổng theo kí tự cuối rồi quy nạp.

**Bước 1 ((a)).** Giả sử mọi tiền tố $x_{<j}$, $j=1,\ldots,n$, có xác suất dương. Theo định nghĩa, $p_1(x_{1:j})=p_1(x_{<j})\,p_1(x_j\mid x_{<j})$ với mỗi $j$. Nhân các đẳng thức này từ $j=1$ đến $n$ và giản ước các thừa số $p_1(x_{1:j})$ chung, với $p_1(x_{<1})=1$, ta được (a). Nếu có $j$ với $p_1(x_{<j})=0$, thì $p_1(x_{1:n})\le p_1(x_{<j})=0$, vì biên là tổng các số không âm có chứa $p_1(x_{1:n})$; hai vế của (a) cùng bằng $0$.

**Bước 2 ((b)).** Lấy $-\ln$ hai vế của (a); logarit của tích là tổng các logarit. Khi một thừa số bằng $0$, quy ước $-\ln0=+\infty$ cho hai vế cùng bằng $+\infty$.

**Bước 3 ((c)).** Đặt $Q_j(x_{1:j})=\prod_{i=1}^jp_\theta(x_i\mid x_{<i})$. Với mỗi tiền tố $x_{<j}$, tổng theo $x_j$ của $p_\theta(x_j\mid x_{<j})$ bằng $1$, nên
$$
\begin{aligned}
&\textstyle\sum_{x_j\in\mathcal A}Q_j(x_{1:j})\\
&=Q_{j-1}(x_{<j})\textstyle\sum_{x_j}p_\theta(x_j\mid x_{<j})\\
&=Q_{j-1}(x_{<j}).
\end{aligned}
$$
Quy nạp từ $j=n$ xuống $j=1$: các tích không âm, tổng của $Q_n$ trên $\mathcal A^n$ bằng $1$, và biên của $Q_n$ trên $x_{1:j}$ bằng $Q_j$. Chia $Q_j(x_{1:j})$ cho $Q_{j-1}(x_{<j})>0$ cho xác suất có điều kiện $p_\theta(x_j\mid x_{<j})$.

$\square$ Phần (a) và (b) là đồng nhất thức; phần (c) cho biết mọi họ xác suất có điều kiện xác định một hàm xác suất trên $\mathcal A^n$.
:::

::: proof Chứng minh Hệ quả 09.13
**Lộ trình.** Kẹp tổng các log độ hợp lý giữa hai giá trị của ELBO, dùng Định lý 09.12(b) hai lần; mọi kì vọng theo $q_i$ là tổng hữu hạn.

**Bước 1 (giả thiết của định lý).** Theo bước M, $\sum_i\mathbb E_{q_i}\ln p_{\theta_{t+1}}(x^{(i)},v)\ge\sum_i\mathbb E_{q_i}\ln p_{\theta_t}(x^{(i)},v)>-\infty$, và mỗi số hạng nhỏ hơn $+\infty$ vì $\mathcal V$ hữu hạn, nên mỗi $\mathbb E_{q_i}\ln p_{\theta_{t+1}}(x^{(i)},v)$ hữu hạn; do đó $p_{\theta_{t+1}}(x^{(i)},v)>0$ trên giá của $q_i$ và $0<p_{\theta_{t+1}}(x^{(i)})<\infty$. Tại $\theta_t$, các giả thiết đúng vì $q_i$ là hậu nghiệm.

**Bước 2 (dãy bất đẳng thức).** Vì $\operatorname{ELBO}(\theta,q_i;x^{(i)})=\mathbb E_{q_i}\ln p_\theta(x^{(i)},v)+\mathrm H(q_i)$ và $\mathrm H(q_i)$ không phụ thuộc $\theta$,
$$
\begin{aligned}
&\textstyle\sum_i\ln p_{\theta_{t+1}}(x^{(i)})\\
&\ge\textstyle\sum_i\operatorname{ELBO}(\theta_{t+1},q_i;x^{(i)})\\
&\ge\textstyle\sum_i\operatorname{ELBO}(\theta_t,q_i;x^{(i)})\\
&=\textstyle\sum_i\ln p_{\theta_t}(x^{(i)}).
\end{aligned}
$$
Dòng đầu là Định lý 09.12(b). Dòng thứ hai là bước M. Dòng cuối là Định lý 09.12(b) với dấu bằng, vì $q_i$ là hậu nghiệm tại $\theta_t$. Nhân với $-\frac1m$, ta được $L_s(\theta_{t+1})\le L_s(\theta_t)$.

$\square$ Bước M chỉ cần không làm giảm tổng $\sum_i\mathbb E_{q_i}\ln p_\theta(x^{(i)},v)$, không cần cực đại hóa nó: Bước 1 và dòng thứ hai của dãy bất đẳng thức chỉ dùng bất đẳng thức giữa hai giá trị của tổng này.
:::
