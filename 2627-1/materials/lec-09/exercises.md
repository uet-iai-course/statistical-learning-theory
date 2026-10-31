# Bài tập Bài 09 — Học chuỗi và mô hình sinh

Định nghĩa, kết quả và ví dụ được dẫn theo số hiệu của ghi chú Bài 09 và của các ghi chú Bài 01–08. Kí hiệu theo bảng kí hiệu chung và §1–§2 của ghi chú, gồm:

- **§1–§6.** $\mathcal A$: bảng chữ, phần tử gọi là kí tự (token); $x_{1:n}$, $x_j$, $x_{<j}$: chuỗi, kí tự ở vị trí $j$, tiền tố; $n$, $n(x)$: độ dài; $x^{(i)}$: quan sát thứ $i$ của mẫu; $k$, $u_j$: độ dài ngữ cảnh và cửa sổ thứ $j$ (Định nghĩa 09.1); $\mathtt E$: kí tự kết thúc (Nhận xét 09.5); $\ell(\theta,x)=-\ln p_\theta(x)$ và $\ell_{\mathrm{len}}$: hàm lỗi log và hàm lỗi chuẩn hóa theo độ dài (Định nghĩa 09.6).
- **§4, §7.** $p_\theta$, $\theta\in\Theta$: mô hình; $p_D$: hàm xác suất (hoặc mật độ) của phân bố thật $D$; $\mathrm H$, $\mathrm h$, $\mathrm{KL}$: entropy, entropy vi phân, phân kì Kullback–Leibler (Định nghĩa 09.7); $\mathrm{Ber}(\theta)$: phân bố Bernoulli; $m_1$: số quan sát bằng $1$ (Ví dụ 09.2).
- **§8–§9.** $v\in\mathcal V$: biến ẩn; $q_\phi$, $\phi\in\Phi$: phân bố biến phân; $\operatorname{ELBO}(\theta,\phi;x)$: cận dưới bằng chứng (Định nghĩa 09.11), viết $\operatorname{ELBO}(\theta,q;x)$ khi $q$ là một hàm xác suất cho trước trên $\mathcal V$; $\zeta$: nhiễu phụ; $\kappa$: hàm dưới kì vọng (Mệnh đề 09.15).

Kí hiệu chỉ dùng trong một bài được đặt tên tại chỗ. Viết tắt: phân kì Kullback–Leibler (Kullback–Leibler divergence, KL), cận dưới bằng chứng (evidence lower bound, ELBO), ước lượng hợp lý cực đại (maximum likelihood estimation, MLE), hạ gradient ngẫu nhiên (stochastic gradient descent, SGD), lỗi bình phương trung bình (mean squared error, MSE). Logarit là logarit tự nhiên; entropy và phân kì KL đo bằng nat.

Bảy bài đầu là bài gốc của học phần; Bài tập 09.6 có phần tính bắt buộc trên số đã chạy và phần thực nghiệm tùy chọn. Ba bài sau chọn từ mục bài tập §24.8 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* (Shalev-Shwartz và Ben-David, 2014; viết tắt UML); Bài tập 09.10 là bài tùy chọn. UML viết $\log$ và cực đại hóa log độ hợp lý; ở đây viết $\ln$ và tối thiểu hóa hàm lỗi log.

## Bài tập gốc

### Bài tập 09.1 (Độ hợp lý, hàm lỗi log trung bình và độ bối rối từ một bảng)

**Mức độ:** tính toán, khái niệm. **Mục tiêu:** mục tiêu học tập 1; tính độ hợp lý của một chuỗi từ bảng xác suất có điều kiện, đọc độ bối rối, và thêm kí tự kết thúc khi độ dài thay đổi.

::: exercise Bài tập 09.1
Một mô hình bigram (bigram model) $p_\theta$ trên $\mathcal A=\{\mathtt A,\mathtt B,\mathtt C\}$ rút kí tự đầu theo hàng "(đầu chuỗi)" của bảng dưới, rồi rút mỗi kí tự tiếp theo theo hàng của kí tự đứng ngay trước. Kí hiệu $\pi_0(b)$ là ô ở hàng đầu, cột $b$, và $\pi(a,b)$ là ô ở hàng $a$, cột $b$.

| Kí tự đứng trước | $\mathtt A$ | $\mathtt B$ | $\mathtt C$ |
|---|---|---|---|
| (đầu chuỗi) | $0{,}5$ | $0{,}25$ | $0{,}25$ |
| $\mathtt A$ | $0{,}2$ | $0{,}5$ | $0{,}3$ |
| $\mathtt B$ | $0{,}4$ | $0{,}4$ | $0{,}2$ |
| $\mathtt C$ | $0{,}1$ | $0{,}1$ | $0{,}8$ |

**(a)** Với độ dài cố định $n=4$, tính độ hợp lý, hàm lỗi log, hàm lỗi log trung bình theo kí tự và độ bối rối (perplexity) của hai chuỗi $\mathtt{ABBC}$ và $\mathtt{CCCC}$.

**(b)** So hai độ bối rối ở (a) với độ bối rối của mô hình đều trên $\mathcal A$. Độ bối rối của một chuỗi nhỏ hơn $3$ cho biết gì về các xác suất có điều kiện mà mô hình gán cho các kí tự của chuỗi đó? Hàm lỗi log trung bình theo kí tự của một chuỗi có phải là một rủi ro kì vọng không?

**(c)** Tính $\Pr(x_3=\mathtt C\mid x_1=\mathtt A)$ và $\Pr(x_3=\mathtt C\mid x_1=\mathtt C)$ dưới $p_\theta$. Mô hình có ngữ cảnh bậc $1$; kí tự $x_3$ có độc lập với $x_1$ không?

**(d)** Bỏ giả thiết độ dài cố định và thêm kí tự kết thúc $\mathtt E$. Kí tự đầu vẫn rút theo $\pi_0$. Sau mỗi kí tự $a\in\mathcal A$, mô hình rút $\mathtt E$ với xác suất $\tfrac14$ và rút $b\in\mathcal A$ với xác suất $\tfrac34\pi(a,b)$. Tính xác suất của chuỗi $\mathtt{ABBC}$ (kết thúc bằng $\mathtt E$). Chứng minh rằng độ dài $n(x)$ có phân bố hình học (geometric distribution) trên $\{1,2,\ldots\}$, tổng các xác suất bằng $1$, và tính kì vọng của $n(x)$.
:::

::: hint Gợi ý 1
Phần (a). Dùng Mệnh đề 09.3(a)–(b) và Định nghĩa 09.4. Phần (c). Lấy tổng theo kí tự thứ hai (công thức xác suất toàn phần). Phần (d). Nhóm các chuỗi theo độ dài, rồi lấy tổng theo các kí tự với độ dài cố định.
:::

::: hint Gợi ý 2
Phần (a). Bốn thừa số của $\mathtt{ABBC}$ là $\pi_0(\mathtt A)$, $\pi(\mathtt A,\mathtt B)$, $\pi(\mathtt B,\mathtt B)$, $\pi(\mathtt B,\mathtt C)$. Phần (d). Một chuỗi độ dài $n$ có $n-1$ thừa số $\tfrac34$ và một thừa số $\tfrac14$; tổng theo các kí tự của tích các ô của bảng bằng $1$ theo Mệnh đề 09.3(c). Với $0<r<1$, $\sum_{n\ge1}nr^{n-1}=1/(1-r)^2$.
:::

::: solution Lời giải Bài tập 09.1
**(a) Hai chuỗi.**

**Bước 1: độ hợp lý của $\mathtt{ABBC}$.** Theo Mệnh đề 09.3(a), độ hợp lý là tích bốn xác suất có điều kiện:
$$
\begin{aligned}
p_\theta(\mathtt{ABBC})&=0{,}5\cdot0{,}5\cdot0{,}4\cdot0{,}2\\
&=0{,}02 .
\end{aligned}
$$

**Bước 2: hàm lỗi log của $\mathtt{ABBC}$.** Theo Mệnh đề 09.3(b), hàm lỗi là tổng bốn số hạng $-\ln0{,}5$, $-\ln0{,}5$, $-\ln0{,}4$, $-\ln0{,}2$:
$$
\begin{aligned}
\ell&=\ln2+\ln2+\ln2{,}5+\ln5\\
&=\ln50\approx3{,}9120 .
\end{aligned}
$$
Chia cho $n=4$, hàm lỗi log trung bình theo kí tự là $0{,}9780$. Độ bối rối là $e^{0{,}9780}=50^{1/4}\approx2{,}6591$.

**Bước 3: chuỗi $\mathtt{CCCC}$.** Độ hợp lý là $0{,}25\cdot0{,}8^3=0{,}128$. Hàm lỗi log là
$$
\begin{aligned}
\ell&=\ln4+3\ln1{,}25\\
&\approx1{,}3863+0{,}6694\\
&=2{,}0557 .
\end{aligned}
$$
Chia cho $4$ được $0{,}5139$; độ bối rối là $e^{0{,}5139}\approx1{,}6719$.

**(b) Đọc độ bối rối.**

**Bước 1: mô hình đều.** Mô hình đều gán $\tfrac13$ cho mọi kí tự, nên độ bối rối của nó bằng $3$ trên mọi chuỗi (đoạn sau Định nghĩa 09.4). Hai độ bối rối ở (a), $2{,}6591$ và $1{,}6719$, đều nhỏ hơn $3$.

**Bước 2: ý nghĩa.** Độ bối rối là nghịch đảo của trung bình nhân các xác suất có điều kiện, vì $\exp\big(\tfrac1n\ell\big)=p_\theta(x_{1:n})^{-1/n}$. Với $\mathtt{ABBC}$, trung bình nhân là $0{,}02^{1/4}\approx0{,}376$; với $\mathtt{CCCC}$, nó là $0{,}128^{1/4}\approx0{,}598$. Độ bối rối nhỏ hơn $3$ nghĩa là trung bình nhân này lớn hơn $\tfrac13$.

**Bước 3: không phải rủi ro kì vọng.** Đại lượng này là hàm lỗi trên một quan sát, chia cho độ dài. Rủi ro kì vọng là kì vọng theo $D$ (Định nghĩa 01.1); để so hai mô hình, ta cần trung bình trên một mẫu kiểm tra độc lập (Ví dụ 09.8).

**(c) Kí tự cách nhau hai vị trí.**

**Bước 1: xác suất có điều kiện.** Theo Mệnh đề 09.3(c), xác suất có điều kiện của $x_3$ khi biết $x_1$, $x_2$ là $\pi(x_2,\cdot)$. Lấy tổng theo $x_2$:
$$
\begin{aligned}
&\Pr(x_3=\mathtt C\mid x_1=\mathtt A)\\
&=0{,}2\cdot0{,}3+0{,}5\cdot0{,}2\\
&\quad+0{,}3\cdot0{,}8\\
&=0{,}40,\\
&\Pr(x_3=\mathtt C\mid x_1=\mathtt C)\\
&=0{,}1\cdot0{,}3+0{,}1\cdot0{,}2\\
&\quad+0{,}8\cdot0{,}8\\
&=0{,}69 .
\end{aligned}
$$

**Bước 2: kết luận.** Hai xác suất có điều kiện khác nhau, nên $x_3$ không độc lập với $x_1$. Ngữ cảnh bậc $1$ chỉ nói rằng xác suất có điều kiện của $x_3$ khi biết $x_{<3}$ chỉ phụ thuộc $x_2$ (Định nghĩa 09.4). Kí tự $x_1$ ảnh hưởng tới $x_3$ qua phân bố của $x_2$.

**(d) Kí tự kết thúc.**

**Bước 1: chuỗi $\mathtt{ABBC}$.** Ba lần chuyển mỗi lần nhân thêm $\tfrac34$, và lần rút $\mathtt E$ sau $\mathtt C$ nhân thêm $\tfrac14$:
$$
\begin{aligned}
&0{,}02\cdot\big(\tfrac34\big)^3\cdot\tfrac14\\
&=\tfrac{27}{12\,800}\approx0{,}0021 .
\end{aligned}
$$

**Bước 2: phân bố của độ dài.** Đặt $Q_n(x_{1:n})=\pi_0(x_1)\prod_{j=2}^n\pi(x_{j-1},x_j)$, tích các ô của bảng. Theo Mệnh đề 09.3(c), $\sum_{x_{1:n}\in\mathcal A^n}Q_n(x_{1:n})=1$. Mọi chuỗi độ dài $n$ có xác suất $\big(\tfrac34\big)^{n-1}\tfrac14\,Q_n(x_{1:n})$, nên
$$
\begin{aligned}
&\Pr\big(n(x)=n\big)\\
&=\big(\tfrac34\big)^{n-1}\tfrac14\sum_{x_{1:n}}Q_n(x_{1:n})\\
&=\big(\tfrac34\big)^{n-1}\tfrac14 .
\end{aligned}
$$
Đây là phân bố hình học trên $\{1,2,\ldots\}$ với xác suất kết thúc $\tfrac14$.

**Bước 3: tổng bằng $1$.** Tổng của cấp số nhân là $\sum_{n\ge1}\tfrac14\big(\tfrac34\big)^{n-1}=\tfrac14\cdot\frac1{1-3/4}=1$. Mô hình kết thúc với xác suất $1$, nên các xác suất của các chuỗi hữu hạn có tổng $1$ (Nhận xét 09.5).

**Bước 4: kì vọng.** Theo công thức của Gợi ý 2 với $r=\tfrac34$,
$$
\begin{aligned}
\mathbb E\,n(x)&=\tfrac14\sum_{n\ge1}n\big(\tfrac34\big)^{n-1}\\
&=\tfrac14\cdot16=4 .
\end{aligned}
$$

**Kiểm tra lại.** Theo Bước 2, $\Pr(n(x)=4)=\tfrac{27}{256}$. Chia xác suất ở Bước 1 cho số này được $\tfrac{27}{12\,800}\cdot\tfrac{256}{27}=0{,}02$, nên khi biết độ dài bằng $4$, chuỗi $\mathtt{ABBC}$ có đúng xác suất của (a).
:::

### Bài tập 09.2 (Rò rỉ thông tin khi chia ngẫu nhiên cửa sổ chồng lấn)

**Mức độ:** khái niệm, chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 3; đếm các cửa sổ chung một giá trị, tính mức rò rỉ của một hàm dự đoán ghi nhớ dùng nhiều cửa sổ hơn hàm của Ví dụ 09.5, và chia mẫu kiểm tra theo thời gian.

::: exercise Bài tập 09.2
Xét Thiết lập B (Định nghĩa 09.1) như Ví dụ 09.5: một chuỗi $x_1,\ldots,x_n$ độc lập cùng phân bố $N(0,1)$, cửa sổ $u_i$ với $i=k+1,\ldots,n$, bước trượt $1$, hàm lỗi bình phương.

**(a)** Với $k+1\le j\le n-k$, đếm số cửa sổ chứa giá trị $x_j$, ở ngữ cảnh hoặc ở đích. Với hai chỉ số $i<i'$, khi nào $u_i$ và $u_{i'}$ không có giá trị chung?

**(b)** Mỗi cửa sổ được đưa vào mẫu kiểm tra với xác suất $f\in(0,1)$, độc lập với các cửa sổ khác và với các giá trị của chuỗi. Xét hàm dự đoán sau cho cửa sổ kiểm tra $u_j$. Với $r=1,\ldots,k-1$ theo thứ tự, nó tìm một cửa sổ huấn luyện có $k-r$ giá trị đầu của ngữ cảnh bằng $k-r$ giá trị cuối của ngữ cảnh của $u_j$. Nếu tìm thấy, nó trả về giá trị ở vị trí $k-r+1$ của ngữ cảnh đó. Nếu không tìm thấy với $r$ nào, nó trả về $0$.

- **(i)** Chứng minh rằng, với xác suất $1$, hàm dự đoán trả về đúng $x_j$ khi ít nhất một trong các cửa sổ $u_{j+1},\ldots,u_{j+k-1}$ thuộc mẫu huấn luyện.
- **(ii)** Bỏ qua các cửa sổ gần cuối chuỗi, tính gần đúng MSE kiểm tra kì vọng theo $f$ và $k$.
- **(iii)** Tính giá trị đó với $(k,f)=(10;\,0{,}2)$ và $(3;\,0{,}5)$, rồi so với hàm dự đoán của Ví dụ 09.5.

**(c)** Lấy $n=5000$, $k=10$, và chọn $998$ cửa sổ liên tiếp ở giữa chuỗi làm mẫu kiểm tra. Dùng (a) để xác định các cửa sổ phải bỏ khỏi mẫu huấn luyện, sao cho không cửa sổ huấn luyện nào có giá trị chung với một cửa sổ kiểm tra. Còn lại bao nhiêu cửa sổ huấn luyện?

**(d)** Với cách chia ở (c), một hàm dự đoán $\hat h$ được học từ các cửa sổ huấn luyện rồi đánh giá trên $998$ cửa sổ kiểm tra. Kiểm từng giả thiết của Hệ quả 02.10. Hệ quả này có cho một khoảng tin cậy cho rủi ro của $\hat h$ không?
:::

::: hint Gợi ý 1
Phần (a). Cửa sổ $u_i$ gồm các giá trị $x_{i-k},\ldots,x_i$. Phần (b)(i). Viết ngữ cảnh của $u_{j+r}$ và so $k-r$ giá trị đầu của nó với ngữ cảnh của $u_j$. Phần (d). Hệ quả 02.10 cần (T1), (T2), (T3) và một giả thuyết không phụ thuộc mẫu.
:::

::: hint Gợi ý 2
Phần (b)(i). Ngữ cảnh của $u_{j+r}$ là $(x_{j+r-k},\ldots,x_{j+r-1})$, chứa $x_j$ ở vị trí $k-r+1$. Hai cửa sổ khác nhau trùng $k-r\ge1$ giá trị liên tục với xác suất $0$. Phần (b)(ii). Hàm dự đoán trả về $0$ chỉ khi cả $k-1$ cửa sổ đều ở mẫu kiểm tra. Phần (d). Hai cửa sổ kiểm tra liền nhau chung $k$ giá trị; $x_j^2$ không bị chặn.
:::

::: solution Lời giải Bài tập 09.2
**(a) Các cửa sổ chứa một giá trị.**

**Bước 1: đếm.** Cửa sổ $u_i$ chứa $x_{i-k},\ldots,x_i$, nên nó chứa $x_j$ khi và chỉ khi $i-k\le j\le i$, tức $j\le i\le j+k$. Với $k+1\le j\le n-k$, mọi chỉ số này hợp lệ, nên có $k+1$ cửa sổ: $u_j$ chứa $x_j$ ở đích, $u_{j+1},\ldots,u_{j+k}$ chứa $x_j$ ở ngữ cảnh.

**Bước 2: hai cửa sổ rời nhau.** Với $i<i'$, $u_i$ dùng các chỉ số $i-k,\ldots,i$ và $u_{i'}$ dùng $i'-k,\ldots,i'$. Hai đoạn này rời nhau khi và chỉ khi $i<i'-k$, tức $i'-i\ge k+1$.

**(b) Hàm dự đoán dùng nhiều cửa sổ.**

**Bước 1: vị trí của $x_j$.** Ngữ cảnh của $u_{j+r}$ là $(x_{j+r-k},\ldots,x_{j+r-1})$. Với $1\le r\le k-1$, $k-r$ giá trị đầu của nó là $x_{j+r-k},\ldots,x_{j-1}$, đúng là $k-r$ giá trị cuối của ngữ cảnh $(x_{j-k},\ldots,x_{j-1})$ của $u_j$. Giá trị ở vị trí $k-r+1$ của nó là $x_{j+r-k+(k-r)}=x_j$.

**Bước 2: chứng minh (i).** Nếu $u_{j+r}$ thuộc mẫu huấn luyện, phép tìm ở bước $r$ thấy nó. Một cửa sổ khác cũng khớp $k-r\ge1$ giá trị liên tục độc lập chỉ với xác suất $0$. Do đó, với xác suất $1$, phép tìm đầu tiên thành công trả về $x_j$.

**Bước 3: MSE (ii).** Hàm dự đoán trả về $0$ khi cả $k-1$ cửa sổ $u_{j+1},\ldots,u_{j+k-1}$ đều ở mẫu kiểm tra; biến cố này có xác suất $f^{k-1}$ và độc lập với các giá trị của chuỗi. Khi đó lỗi là $x_j^2$, với kì vọng $1$; nếu không, lỗi bằng $0$. Do đó
$$
\mathbb E\,\mathrm{MSE}\approx f^{k-1}.
$$

**Bước 4: số (iii).** Với $(k,f)=(10;\,0{,}2)$: $0{,}2^9\approx5{,}1\cdot10^{-7}$. Với $(3;\,0{,}5)$: $0{,}5^2=0{,}25$. Hàm dự đoán của Ví dụ 09.5 chỉ dùng $u_{j+1}$, nên MSE của nó xấp xỉ $f$, tức $0{,}2$ và $0{,}5$.

**Bước 5: so sánh.** Với $k=10$, $f=0{,}2$, MSE kiểm tra khoảng $5\cdot10^{-7}$, trong khi mọi hàm dự đoán có rủi ro ít nhất $1$ trên dữ liệu mới (Ví dụ 09.5, Thiết lập).

**(c) Chia theo thời gian với khoảng đệm.**

**Bước 1: cửa sổ phải bỏ.** Gọi các cửa sổ kiểm tra là $u_a,\ldots,u_b$ với $b-a+1=998$. Theo (a), một cửa sổ $u_i$ không có giá trị chung với cửa sổ kiểm tra nào khi và chỉ khi $i\le a-k-1$ hoặc $i\ge b+k+1$. Do đó ta bỏ $k=10$ cửa sổ ở mỗi phía của phần kiểm tra.

**Bước 2: đếm.** Có $5000-10=4990$ cửa sổ. Số cửa sổ huấn luyện còn lại là
$$
4990-998-2\cdot10=3972 .
$$

**(d) Giả thiết của Hệ quả 02.10.**

**Bước 1: giả thuyết cố định.** Các giá trị của chuỗi độc lập, và cửa sổ huấn luyện không chung giá trị với cửa sổ kiểm tra, nên $\hat h$ độc lập với các cửa sổ kiểm tra. Với một chuỗi thời gian có các giá trị phụ thuộc nhau, khoảng đệm $k$ không bảo đảm điều này.

**Bước 2: (T1).** Theo (a), $u_j$ và $u_{j+1}$ chung $k$ giá trị. Nếu $\hat h$ dùng ngữ cảnh, lỗi trên hai cửa sổ kiểm tra liền nhau phụ thuộc nhau, nên (T1) không thỏa với quan sát là cửa sổ.

**Bước 3: (T3).** Lỗi bình phương với đích $N(0,1)$ không bị chặn, nên (T3) không thỏa. Ngay cả với $\hat h\equiv0$, khi các lỗi $x_j^2$ độc lập, chúng vẫn không bị chặn (Nhận xét 02.11).

**Bước 4: kết luận.** Hệ quả 02.10 không cho khoảng tin cậy; một bảo đảm cần giả thiết về sự phụ thuộc và một cận cho hàm lỗi (Thiết lập B, §1).

**Kiểm tra lại.** Với $k=2$, hàm dự đoán ở (b) chỉ có bước $r=1$, tức quy tắc tra cứu của Ví dụ 09.5, và $f^{k-1}=f$ khớp MSE xấp xỉ $0{,}2$ ở Ví dụ 09.5, Bước 2.
:::

### Bài tập 09.3 (Entropy chéo, entropy và phân kì KL)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 2; chứng minh $\mathrm{KL}\ge0$ theo một đường khác ghi chú, tính các đại lượng của Mệnh đề 09.8 trên một ví dụ, và đọc điều kiện giá theo hai chiều của phân kì KL.

::: exercise Bài tập 09.3
Cho $\mathcal X=\{1,2,3\}$ và $p_D=(\tfrac12,\tfrac14,\tfrac14)$.

**(a)** Với $\mathcal X$ hữu hạn, chứng minh Mệnh đề 09.8(b) bằng bất đẳng thức Jensen cho hàm lõm $\ln$, không dùng $\ln t\le t-1$. Chỉ ra chỗ dùng điều kiện "$p_\theta>0$ trên giá của $p_D$" và chỗ dùng tính lõm ngặt để có điều kiện dấu bằng.

**(b)** Với $p_\theta$ đều trên $\mathcal X$, tính $\mathrm H(p_D)$, entropy chéo $L_D(\theta)$ và $\mathrm{KL}(p_D\Vert p_\theta)$, kiểm Mệnh đề 09.8(a), rồi tính $\mathrm{KL}(p_\theta\Vert p_D)$.

**(c)** Với $p_\theta=(\tfrac12,\tfrac12,0)$, tính $L_D(\theta)$, $\mathrm{KL}(p_D\Vert p_\theta)$ và $\mathrm{KL}(p_\theta\Vert p_D)$. Ước lượng hợp lý cực đại tổng thể làm nhỏ nhất chiều nào (Hệ quả 09.9)? Với chiều đó, một mô hình gán xác suất $0$ cho một quan sát có thể xảy ra bị đánh giá thế nào?

**(d)** Gọi $p_U$ là mật độ của phân bố đều trên $[0,\tfrac12]$. Tính $\mathrm h(p_U)$. Với $b\ge2$ nguyên và $\Delta=2^{-b}$, chia $[0,\tfrac12]$ thành các ô độ dài $\Delta$ và gọi $\tilde p_\Delta$ là phân bố rời rạc của chỉ số ô chứa $X\sim p_U$. Chứng minh $\mathrm H(\tilde p_\Delta)=\mathrm h(p_U)-\ln\Delta$, tính với $b=4$ và $b=8$, và nêu giới hạn khi $\Delta\to0$.
:::

::: hint Gợi ý 1
Phần (a). Bất đẳng thức Jensen cho hàm lõm $g$ và các trọng số $w_x\ge0$ có tổng $1$: $\sum_xw_xg(t_x)\le g\big(\sum_xw_xt_x\big)$. Lấy trọng số $p_D(x)$ trên giá của $p_D$. Phần (d). Mỗi ô có xác suất $\Delta/(1/2)=2\Delta$.
:::

::: hint Gợi ý 2
Phần (a). Với $t_x=p_\theta(x)/p_D(x)$, ta có $\sum_{p_D>0}p_D(x)t_x=\sum_{p_D>0}p_\theta(x)\le1$. Với $\ln$ lõm ngặt, dấu bằng của Jensen xảy ra khi và chỉ khi mọi $t_x$ có trọng số dương bằng nhau. Phần (c). Số hạng của $x=3$ trong $\mathrm{KL}(p_D\Vert p_\theta)$ là $\tfrac14\ln\frac{1/4}0$.
:::

::: solution Lời giải Bài tập 09.3
**(a) Chứng minh bằng bất đẳng thức Jensen.**

**Bước 1: trường hợp $p_\theta$ bằng $0$ trên giá.** Gọi $\mathcal S=\{x:p_D(x)>0\}$. Nếu có $x\in\mathcal S$ với $p_\theta(x)=0$, số hạng của $x$ trong $\mathrm{KL}(p_D\Vert p_\theta)$ bằng $+\infty$, các số hạng khác hữu hạn vì $\mathcal X$ hữu hạn, nên $\mathrm{KL}=+\infty\ge0$ và $p_\theta\ne p_D$. Điều kiện giá dùng ở đây: khi nó thỏa, các tỉ số dưới đây dương.

**Bước 2: Jensen.** Giả sử $p_\theta>0$ trên $\mathcal S$ và đặt $t_x=p_\theta(x)/p_D(x)>0$ với $x\in\mathcal S$. Các trọng số $p_D(x)$, $x\in\mathcal S$, có tổng $1$, và $\ln$ lõm, nên
$$
\begin{aligned}
&-\mathrm{KL}(p_D\Vert p_\theta)\\
&=\sum_{x\in\mathcal S}p_D(x)\ln t_x\\
&\le\ln\Big(\sum_{x\in\mathcal S}p_D(x)t_x\Big)\\
&=\ln\Big(\sum_{x\in\mathcal S}p_\theta(x)\Big)\\
&\le\ln1=0 .
\end{aligned}
$$
Bất đẳng thức cuối dùng $\sum_{x\in\mathcal S}p_\theta(x)\le1$ và $\ln$ tăng.

**Bước 3: dấu bằng.** Nếu $\mathrm{KL}=0$, cả hai bất đẳng thức là đẳng thức. Vì $\ln$ lõm ngặt, dấu bằng của Jensen buộc mọi $t_x$, $x\in\mathcal S$, bằng một hằng số $c$, tức $p_\theta=c\,p_D$ trên $\mathcal S$. Dấu bằng thứ hai buộc $\sum_{\mathcal S}p_\theta=1$, nên $c=1$ và $p_\theta=0$ ngoài $\mathcal S$. Do đó $p_\theta=p_D$. Ngược lại, nếu $p_\theta=p_D$ thì mọi $t_x=1$ và $\mathrm{KL}=0$.

**(b) Mô hình đều.**

**Bước 1: entropy.** Theo Định nghĩa 09.7,
$$
\begin{aligned}
\mathrm H(p_D)&=\tfrac12\ln2+2\cdot\tfrac14\ln4\\
&=\tfrac32\ln2\approx1{,}0397 .
\end{aligned}
$$

**Bước 2: entropy chéo.** Mọi $p_\theta(x)=\tfrac13$, nên $L_D(\theta)=\ln3\approx1{,}0986$.

**Bước 3: phân kì KL thuận.**
$$
\begin{aligned}
&\mathrm{KL}(p_D\Vert p_\theta)\\
&=\tfrac12\ln\tfrac32+2\cdot\tfrac14\ln\tfrac34\\
&\approx0{,}2027-0{,}1438=0{,}0589 .
\end{aligned}
$$
Ta có $1{,}0397+0{,}0589=1{,}0986$, đúng Mệnh đề 09.8(a).

**Bước 4: chiều ngược lại.**
$$
\begin{aligned}
&\mathrm{KL}(p_\theta\Vert p_D)\\
&=\tfrac13\ln\tfrac23+2\cdot\tfrac13\ln\tfrac43\\
&\approx-0{,}1352+0{,}1918\\
&=0{,}0566 .
\end{aligned}
$$
Hai chiều khác nhau, nên phân kì KL không đối xứng.

**(c) Mô hình bỏ một điểm của giá.**

**Bước 1: chiều thuận.** $p_D(3)=\tfrac14>0=p_\theta(3)$, nên theo Mệnh đề 09.8(a), $L_D(\theta)=\mathrm{KL}(p_D\Vert p_\theta)=+\infty$.

**Bước 2: chiều ngược.** Giá của $p_\theta$ là $\{1,2\}$, nên tổng chỉ chạy trên hai điểm:
$$
\begin{aligned}
&\mathrm{KL}(p_\theta\Vert p_D)\\
&=\tfrac12\ln\tfrac{1/2}{1/2}+\tfrac12\ln\tfrac{1/2}{1/4}\\
&=\tfrac12\ln2\approx0{,}3466 .
\end{aligned}
$$

**Bước 3: đọc kết quả.** Ước lượng hợp lý cực đại tổng thể làm nhỏ nhất chiều thuận $\mathrm{KL}(p_D\Vert p_\theta)$ (Hệ quả 09.9(a)). Với chiều này, mô hình gán xác suất $0$ cho một quan sát có xác suất dương dưới $D$ có rủi ro $+\infty$ và bị loại. Chiều ngược lại chỉ đo trên giá của $p_\theta$ và cho giá trị hữu hạn $0{,}3466$.

**(d) Rời rạc hóa entropy vi phân.**

**Bước 1: entropy vi phân.** $p_U=2$ trên $[0,\tfrac12]$, nên $\mathrm h(p_U)=-\int_0^{1/2}2\ln2\,dx=-\ln2\approx-0{,}6931$.

**Bước 2: phân bố của chỉ số ô.** Có $\tfrac1{2\Delta}=2^{b-1}$ ô, mỗi ô có xác suất $2\Delta$. Do đó
$$
\begin{aligned}
\mathrm H(\tilde p_\Delta)&=-\ln(2\Delta)\\
&=-\ln2-\ln\Delta\\
&=\mathrm h(p_U)-\ln\Delta .
\end{aligned}
$$

**Bước 3: số.** Với $\Delta=2^{-b}$, $\mathrm H(\tilde p_\Delta)=(b-1)\ln2$: bằng $3\ln2\approx2{,}0794$ khi $b=4$ và $7\ln2\approx4{,}8520$ khi $b=8$.

**Bước 4: giới hạn.** Khi $\Delta\to0$, $-\ln\Delta\to+\infty$, nên $\mathrm H(\tilde p_\Delta)\to+\infty$, trong khi $\mathrm h(p_U)=-\ln2$ cố định và âm. Entropy vi phân không phải giới hạn của entropy rời rạc.

**Kiểm tra lại.** Ở (b), $\mathrm{KL}(p_D\Vert p_\theta)=\ln3-\tfrac32\ln2$, vì entropy chéo với mô hình đều bằng $\ln\lvert\mathcal X\rvert$; hiệu này bằng $0{,}0589$, khớp Bước 3.
:::

### Bài tập 09.4 (Cận dưới bằng chứng và điều kiện dấu bằng)

**Mức độ:** chứng minh, tính toán, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 4 và 5; chứng minh trực tiếp cận dưới với biến ẩn hữu hạn, tách cận thành số hạng tái tạo và KL trên một hỗn hợp (mixture) Gauss, xét giá của phân bố biến phân, và chỉ ra gradient theo đường đi bị chệch với biến ẩn rời rạc.

::: exercise Bài tập 09.4
**(a)** Cho $\mathcal V$ hữu hạn, $x$ cố định với $0<p_\theta(x)<\infty$, và một hàm xác suất $q$ trên $\mathcal V$ với $p_\theta(x,v)>0$ trên giá của $q$. Chứng minh $\operatorname{ELBO}(\theta,q;x)\le\ln p_\theta(x)$ trực tiếp từ $\ln t\le t-1$, với $t=p_\theta(x,v)/\big(q(v)\,p_\theta(x)\big)$, không đi qua đồng nhất thức của Định lý 09.12(a). Chỉ ra chỗ dùng từng giả thiết, và suy ra điều kiện dấu bằng.

**(b)** Một hỗn hợp hai Gauss: $v\in\{1,2\}$ với $\Pr(v=1)=\Pr(v=2)=\tfrac12$; $x\mid v=1\sim N(-1,1)$ và $x\mid v=2\sim N(1,1)$. Quan sát $x=0{,}5$. Tính $p_\theta(x)$, $\ln p_\theta(x)$ và hậu nghiệm $\Pr(v=2\mid x)$. Với $q(2)=0{,}5$ và $q(2)=0{,}9$, tính ELBO và *khe* (gap) $\ln p_\theta(x)-\operatorname{ELBO}$. Với $q(2)=0{,}9$, kiểm khe bằng $\mathrm{KL}\big(q\Vert p_\theta(\cdot\mid x)\big)$, rồi tính số hạng tái tạo, $\mathrm{KL}$ tới tiên nghiệm, và kiểm Định lý 09.12(c).

**(c)** Trong mô hình của (b), lấy $q(2)=1$. Giá của $q$ nhỏ hơn giá của hậu nghiệm; ELBO có hữu hạn không? Tính khe. Sau đó thêm giá trị $v=3$ với tiên nghiệm $(0{,}45;\,0{,}45;\,0{,}1)$ và $x\mid v=3$ đều trên $[2,3]$, và lấy $q=(0{,}45;\,0{,}45;\,0{,}1)$. Tính ELBO và chỉ ra giả thiết nào của Định lý 09.12 không thỏa.

**(d)** Trong mô hình của (b), đặt $q_\phi(2)=\phi$, $q_\phi(1)=1-\phi$ với $\phi\in(0,1)$, và tái tham số hóa $v=1+\mathbb 1[U_0<\phi]$ với $U_0$ đều trên $[0,1]$. Tính $\frac{d}{d\phi}\operatorname{ELBO}$ tại $\phi=\tfrac12$. Với $\kappa(\phi,U_0)=\ln p_\theta(x,v)-\ln q_\phi(v)$, tính kì vọng của ước lượng theo đường đi $\partial_\phi\kappa(\phi,U_0)$ tại $\phi=\tfrac12$. Điều kiện nào của Mệnh đề 09.15 không thỏa?
:::

::: hint Gợi ý 1
Phần (a). Viết $\operatorname{ELBO}-\ln p_\theta(x)$ thành một tổng theo $v$ trên giá của $q$ của $q(v)\ln t$. Phần (b). Công thức xác suất toàn phần và công thức Bayes như câu ôn nhanh 3, với mật độ Gauss thay cho xác suất. Phần (d). Viết ELBO thành hàm của $\phi$ rồi lấy đạo hàm.
:::

::: hint Gợi ý 2
Phần (a). Sau khi dùng $\ln t\le t-1$, tổng còn lại là $\sum_{q(v)>0}p_\theta(v\mid x)-1$. Phần (b). Gọi $\rho_0$ là mật độ của $N(0,1)$; hai mật độ có điều kiện tại $x=0{,}5$ là $\rho_0(1{,}5)$ và $\rho_0(0{,}5)$, và tỉ số của chúng bằng $e^{-1}$. Phần (c). Với $q(2)=1$, $\operatorname{ELBO}=\ln p_\theta(x,2)$. Phần (d). Với $U_0$ cố định và $\phi\ne U_0$, $v$ không đổi khi $\phi$ thay đổi ít, nên chỉ số hạng $-\ln q_\phi(v)$ phụ thuộc $\phi$.
:::

::: solution Lời giải Bài tập 09.4
**(a) Chứng minh trực tiếp.**

**Bước 1: viết hiệu (dùng $0<p_\theta(x)<\infty$).** Gọi $\mathcal S_q=\{v:q(v)>0\}$. Vì $\ln p_\theta(x)$ hữu hạn và $\sum_{\mathcal S_q}q(v)=1$, ta trừ được nó dưới tổng:
$$
\begin{aligned}
&\operatorname{ELBO}(\theta,q;x)-\ln p_\theta(x)\\
&=\sum_{v\in\mathcal S_q}q(v)\ln\frac{p_\theta(x,v)}{q(v)\,p_\theta(x)} .
\end{aligned}
$$
Mỗi tỉ số dương vì $p_\theta(x,v)>0$ trên $\mathcal S_q$; giả thiết giá dùng ở đây, nên mọi số hạng hữu hạn.

**Bước 2: $\ln t\le t-1$.** Áp dụng cho từng số hạng:
$$
\begin{aligned}
&\operatorname{ELBO}-\ln p_\theta(x)\\
&\le\sum_{v\in\mathcal S_q}q(v)\Big(\frac{p_\theta(x,v)}{q(v)\,p_\theta(x)}-1\Big)\\
&=\sum_{v\in\mathcal S_q}p_\theta(v\mid x)-1\le0 .
\end{aligned}
$$
Dòng cuối dùng định nghĩa hậu nghiệm $p_\theta(v\mid x)=p_\theta(x,v)/p_\theta(x)$, xác định vì $0<p_\theta(x)<\infty$, và tổng của hậu nghiệm trên $\mathcal S_q$ không quá $1$.

**Bước 3: dấu bằng.** Dấu bằng cần $t=1$ tại mọi $v\in\mathcal S_q$, tức $q(v)=p_\theta(v\mid x)$ trên $\mathcal S_q$, và $\sum_{\mathcal S_q}p_\theta(v\mid x)=1$, tức hậu nghiệm bằng $0$ ngoài $\mathcal S_q$. Hai điều kiện này nghĩa là $q=p_\theta(\cdot\mid x)$. Ngược lại, với $q$ là hậu nghiệm, mọi $t=1$.

**(b) Hỗn hợp hai Gauss.**

**Bước 1: bằng chứng.** $\rho_0(1{,}5)\approx0{,}129518$ và $\rho_0(0{,}5)\approx0{,}352065$. Theo công thức xác suất toàn phần,
$$
\begin{aligned}
p_\theta(0{,}5)&=\tfrac12\rho_0(1{,}5)+\tfrac12\rho_0(0{,}5)\\
&\approx0{,}2408,
\end{aligned}
$$
và $\ln p_\theta(0{,}5)\approx-1{,}4238$.

**Bước 2: hậu nghiệm.** Theo công thức Bayes, với tỉ số $\rho_0(1{,}5)/\rho_0(0{,}5)=e^{-(2{,}25-0{,}25)/2}=e^{-1}$,
$$
\begin{aligned}
&\Pr(v=2\mid x)\\
&=\frac{\rho_0(0{,}5)}{\rho_0(0{,}5)+\rho_0(1{,}5)}\\
&=\frac1{1+e^{-1}}\approx0{,}7311 .
\end{aligned}
$$

**Bước 3: ELBO với $q(2)=0{,}5$.** Hai số hạng là $\tfrac12\ln\frac{\rho_0(1{,}5)/2}{1/2}$ và $\tfrac12\ln\frac{\rho_0(0{,}5)/2}{1/2}$:
$$
\begin{aligned}
\operatorname{ELBO}&=\tfrac12\ln\rho_0(1{,}5)\\
&\quad+\tfrac12\ln\rho_0(0{,}5)\\
&\approx\tfrac12(-2{,}0439-1{,}0439)\\
&=-1{,}5439 .
\end{aligned}
$$
Khe là $-1{,}4238+1{,}5439=0{,}1201$.

**Bước 4: ELBO với $q(2)=0{,}9$.** Hai mật độ đồng thời là $p_\theta(x,1)\approx0{,}064759$ và $p_\theta(x,2)\approx0{,}176033$, nên
$$
\begin{aligned}
\operatorname{ELBO}&=0{,}1\ln\tfrac{0{,}064759}{0{,}1}\\
&\quad+0{,}9\ln\tfrac{0{,}176033}{0{,}9}\\
&\approx-0{,}0434-1{,}4685\\
&=-1{,}5120 .
\end{aligned}
$$
Khe là $-1{,}4238+1{,}5120=0{,}0882$.

**Bước 5: tái tạo và KL.** Mật độ có điều kiện của $x$ là $\rho_0(1{,}5)$ khi $v=1$ và $\rho_0(0{,}5)$ khi $v=2$. Với $q(2)=0{,}9$, số hạng tái tạo (Định lý 09.12(c)) là
$$
\begin{aligned}
&0{,}1\ln\rho_0(1{,}5)+0{,}9\ln\rho_0(0{,}5)\\
&\approx-0{,}2044-0{,}9395\\
&=-1{,}1439 .
\end{aligned}
$$
Phân kì KL tới tiên nghiệm $(\tfrac12,\tfrac12)$ là
$$
\begin{aligned}
&0{,}1\ln\tfrac{0{,}1}{0{,}5}+0{,}9\ln\tfrac{0{,}9}{0{,}5}\\
&\approx-0{,}1609+0{,}5290\\
&=0{,}3681 .
\end{aligned}
$$
Hiệu $-1{,}1439-0{,}3681=-1{,}5120$ trùng ELBO của Bước 4.

**Bước 6: khe bằng phân kì KL.** Với hậu nghiệm $(0{,}2689;\,0{,}7311)$,
$$
\begin{aligned}
&\mathrm{KL}\big(q\Vert p_\theta(\cdot\mid x)\big)\\
&=0{,}1\ln\tfrac{0{,}1}{0{,}2689}+0{,}9\ln\tfrac{0{,}9}{0{,}7311}\\
&\approx-0{,}0989+0{,}1871=0{,}0882,
\end{aligned}
$$
trùng khe của Bước 4, đúng Định lý 09.12(a). Phân bố $q(2)=0{,}9$ gần hậu nghiệm hơn $q(2)=0{,}5$, và khe nhỏ hơn.

**(c) Hai trường hợp về giá.**

**Bước 1: $q(2)=1$.** Giá của $q$ là $\{2\}$ và $p_\theta(x,2)>0$, nên giả thiết của (a) thỏa. $\operatorname{ELBO}=\ln p_\theta(x,2)\approx\ln0{,}176033\approx-1{,}7371$, hữu hạn. Khe là
$$
\begin{aligned}
&\ln p_\theta(x)-\operatorname{ELBO}\\
&=-1{,}4238+1{,}7371\\
&=0{,}3133\\
&=-\ln\Pr(v=2\mid x).
\end{aligned}
$$
Khe dương vì $q\ne p_\theta(\cdot\mid x)$.

**Bước 2: thêm $v=3$.** Mật độ đều trên $[2,3]$ bằng $0$ tại $x=0{,}5$, nên $p_\theta(x,3)=0$, trong khi $q(3)=0{,}1>0$. Số hạng của $v=3$ là $0{,}1\ln\frac0{0{,}1}=-\infty$, và hai số hạng còn lại hữu hạn, nên $\operatorname{ELBO}=-\infty$.

**Bước 3: giả thiết không thỏa.** Định lý 09.12 cần $p_\theta(x,v)>0$ cho $q$-hầu hết $v$; ở đây $q$ đặt khối lượng $0{,}1$ ở chỗ $p_\theta(x,v)=0$. Bất đẳng thức $\operatorname{ELBO}\le\ln p_\theta(x)$ đúng tầm thường, như câu cuối của Định lý 09.12.

**(d) Biến ẩn rời rạc.**

**Bước 1: đạo hàm đúng.** $\operatorname{ELBO}(\phi)=(1-\phi)\ln\frac{p_\theta(x,1)}{1-\phi}+\phi\ln\frac{p_\theta(x,2)}{\phi}$. Đạo hàm của $-(1-\phi)\ln(1-\phi)-\phi\ln\phi$ là $\ln\frac{1-\phi}\phi$, nên
$$
\begin{aligned}
\frac{d}{d\phi}\operatorname{ELBO}&=\ln\frac{p_\theta(x,2)}{\phi}\\
&\quad-\ln\frac{p_\theta(x,1)}{1-\phi}.
\end{aligned}
$$
Tại $\phi=\tfrac12$, vế phải bằng $\ln\frac{\rho_0(0{,}5)}{\rho_0(1{,}5)}=1$ (Bước 2 của (b)).

**Bước 2: ước lượng theo đường đi.** Với $U_0\ne\phi$, $v$ không đổi quanh $\phi$, nên chỉ $-\ln q_\phi(v)$ phụ thuộc $\phi$. Đạo hàm là $-1/\phi$ khi $v=2$ và $1/(1-\phi)$ khi $v=1$. Tại $\phi=\tfrac12$, ước lượng bằng $-2$ hoặc $2$, mỗi giá trị với xác suất $\tfrac12$, nên kì vọng bằng $0\ne1$ và ước lượng bị chệch.

**Bước 3: điều kiện bị vi phạm.** Với $U_0$ cố định, $\phi\mapsto v$ nhảy tại $\phi=U_0\in(0,1)$, nên $\kappa(\cdot,U_0)$ không khả vi tại đó. Không có tập ngoại lệ chung cho mọi $\phi$, nên (i) của Mệnh đề 09.15 không thỏa, như Ví dụ 09.12, Bước 3–4.

**Kiểm tra lại.** Ở (b), với $q$ bằng hậu nghiệm, $\operatorname{ELBO}=0{,}2689\ln\frac{0{,}064759}{0{,}2689}+0{,}7311\ln\frac{0{,}176033}{0{,}7311}\approx-1{,}4238$; cả hai tỉ số bằng $p_\theta(0{,}5)$, nên ELBO bằng $\ln p_\theta(0{,}5)$ và khe bằng $0$.
:::

### Bài tập 09.5 (Mục tiêu theo kí tự và theo chuỗi với hai độ dài chuỗi)

**Mức độ:** tính toán, chứng minh. **Mục tiêu:** mục tiêu học tập 3; so hai mục tiêu của Định nghĩa 09.6 trên một phân bố mới, rồi chứng minh điểm cực tiểu tổng thể của hàm lỗi chuẩn hóa theo độ dài.

::: exercise Bài tập 09.5
Cho $\mathcal A=\{\mathtt 0,\mathtt 1\}$. Phân bố $D$ cho chuỗi $\mathtt{11}$ (độ dài $2$) và chuỗi $\mathtt{010000}$ (độ dài $6$), mỗi chuỗi với xác suất $\tfrac12$. Như Ví dụ 09.6, mô hình coi các kí tự độc lập, mỗi kí tự là $\mathtt 1$ với xác suất $\theta\in(0,1)$, và xác suất của $\mathtt E$ có tham số riêng, nên ta bỏ số hạng của $\mathtt E$.

**(a)** Tìm điểm cực tiểu của rủi ro kì vọng với hàm lỗi tổng và với hàm lỗi chuẩn hóa theo độ dài.

**(b)** Cho $D$ bất kì có giá hữu hạn trên các chuỗi có $n(x)\ge1$; gọi $s(x)$ là số kí tự $\mathtt 1$ của chuỗi $x$, và giả sử $0<\mathbb E_Ds(X)<\mathbb E_Dn(X)$ và $0<\mathbb E_D[s(X)/n(X)]<1$. Chứng minh rằng với cùng mô hình, hàm lỗi tổng cho $\theta=\mathbb E_Ds(X)/\mathbb E_Dn(X)$, còn hàm lỗi chuẩn hóa cho $\theta=\mathbb E_D[s(X)/n(X)]$.

**(c)** Bỏ mô hình kí tự độc lập. Lớp mô hình là mọi hàm xác suất $p$ trên tập đếm được $\mathcal X$ các chuỗi hữu hạn, với hàm lỗi $\ell_{\mathrm{len}}(p,x)=-\ln p(x)/n(x)$. Đặt $c=\mathbb E_D[1/n(X)]$ và $\tilde p(x)=p_D(x)/\big(c\,n(x)\big)$, và giả sử $\mathrm H(\tilde p)<\infty$. Chứng minh rằng $\mathbb E_D\,\ell_{\mathrm{len}}(p,X)$ nhỏ nhất khi và chỉ khi $p=\tilde p$. Tính $\tilde p$ cho $D$ của (a), và so với điểm cực tiểu của hàm lỗi tổng trên cùng lớp.

**(d)** Chứng minh rằng trong (c), hai hàm lỗi có cùng điểm cực tiểu khi và chỉ khi mọi chuỗi trong giá của $p_D$ có cùng độ dài.
:::

::: hint Gợi ý 1
Phần (a). Viết hàm lỗi của mỗi chuỗi theo số kí tự $\mathtt 1$ và số kí tự $\mathtt 0$, rồi lấy đạo hàm theo $\theta$. Phần (c). Kéo hệ số $1/n(x)$ vào trọng số của tổng và chuẩn hóa các trọng số thành một hàm xác suất.
:::

::: hint Gợi ý 2
Phần (b). Rủi ro kì vọng có dạng $-a\ln\theta-b\ln(1-\theta)$ với $a,b>0$, nhỏ nhất tại $\theta=a/(a+b)$. Phần (c). $\mathbb E_D\,\ell_{\mathrm{len}}(p,X)=c\sum_x\tilde p(x)\big(-\ln p(x)\big)$; áp dụng Mệnh đề 09.8 với $\tilde p$ ở chỗ của $p_D$.
:::

::: solution Lời giải Bài tập 09.5
**(a) Hai điểm cực tiểu.**

**Bước 1: hàm lỗi của từng chuỗi.** Chuỗi $\mathtt{11}$ có hai kí tự $\mathtt 1$, nên hàm lỗi là $-2\ln\theta$. Chuỗi $\mathtt{010000}$ có một kí tự $\mathtt 1$ và năm kí tự $\mathtt 0$, nên hàm lỗi là $-\ln\theta-5\ln(1-\theta)$.

**Bước 2: hàm lỗi tổng.** Rủi ro kì vọng là
$$
\begin{aligned}
&\tfrac12(-2\ln\theta)\\
&\quad+\tfrac12\big(-\ln\theta-5\ln(1-\theta)\big)\\
&=-\tfrac32\ln\theta-\tfrac52\ln(1-\theta).
\end{aligned}
$$
Đạo hàm $-\tfrac3{2\theta}+\tfrac5{2(1-\theta)}$ bằng $0$ khi $3(1-\theta)=5\theta$, tức $\theta=\tfrac38$. Hàm $-a\ln\theta-b\ln(1-\theta)$ với $a,b>0$ lồi, nên đây là điểm cực tiểu, bằng tần suất của $\mathtt 1$ trên cả tám kí tự.

**Bước 3: hàm lỗi chuẩn hóa.** Chia hàm lỗi của chuỗi ngắn cho $2$, của chuỗi dài cho $6$:
$$
\begin{aligned}
&\tfrac12(-\ln\theta)\\
&\quad+\tfrac12\big(-\tfrac16\ln\theta-\tfrac56\ln(1-\theta)\big)\\
&=-\tfrac7{12}\ln\theta-\tfrac5{12}\ln(1-\theta).
\end{aligned}
$$
Đạo hàm $-\tfrac7{12\theta}+\tfrac5{12(1-\theta)}$ bằng $0$ khi $7(1-\theta)=5\theta$, tức $\theta=\tfrac7{12}=\tfrac12(1+\tfrac16)$, trung bình của tần suất trong từng chuỗi.

**Bước 4: so sánh.** Hàm lỗi chuẩn hóa cho mỗi kí tự của chuỗi ngắn trọng số $\tfrac14$ và mỗi kí tự của chuỗi dài trọng số $\tfrac1{12}$, nên hai kí tự $\mathtt 1$ của chuỗi ngắn quyết định kết quả.

**(b) Trường hợp tổng quát.**

**Bước 1: hàm lỗi tổng.** Chuỗi $x$ có hàm lỗi $-s(x)\ln\theta-\big(n(x)-s(x)\big)\ln(1-\theta)$. Lấy kì vọng theo $D$ được dạng của Gợi ý 2 với $a=\mathbb E_Ds(X)$ và $b=\mathbb E_Dn(X)-\mathbb E_Ds(X)$, cả hai dương theo giả thiết.

**Bước 2: cực tiểu của $-a\ln\theta-b\ln(1-\theta)$.** Đạo hàm $-a/\theta+b/(1-\theta)$ âm trên $\big(0,\tfrac a{a+b}\big)$ và dương trên $\big(\tfrac a{a+b},1\big)$, nên điểm cực tiểu duy nhất là $\theta=a/(a+b)=\mathbb E_Ds(X)/\mathbb E_Dn(X)$.

**Bước 3: hàm lỗi chuẩn hóa.** Chia hàm lỗi của $x$ cho $n(x)$ rồi lấy kì vọng: $a=\mathbb E_D[s(X)/n(X)]$, $b=1-a$, cả hai dương. Theo Bước 2, $\theta=\mathbb E_D[s(X)/n(X)]$.

**(c) Lớp mọi phân bố.**

**Bước 1: chuẩn hóa trọng số.** Vì $n(x)\ge1$, ta có $0<c\le1$, và $\tilde p\ge0$ với $\sum_x\tilde p(x)=\mathbb E_D[1/n(X)]/c=1$; $\tilde p$ là một hàm xác suất.

**Bước 2: viết lại rủi ro.** Với mọi hàm xác suất $p$,
$$
\begin{aligned}
&\mathbb E_D\,\ell_{\mathrm{len}}(p,X)\\
&=\sum_xp_D(x)\frac{-\ln p(x)}{n(x)}\\
&=c\sum_x\tilde p(x)\big(-\ln p(x)\big).
\end{aligned}
$$

**Bước 3: Mệnh đề 09.8.** Tổng ở Bước 2 là entropy chéo của $p$ dưới $\tilde p$. Theo Mệnh đề 09.8(a) với $\tilde p$ ở chỗ của $p_D$ (cần $\mathrm H(\tilde p)<\infty$),
$$
\begin{aligned}
&\mathbb E_D\,\ell_{\mathrm{len}}(p,X)\\
&=c\big(\mathrm H(\tilde p)+\mathrm{KL}(\tilde p\Vert p)\big).
\end{aligned}
$$
Theo Mệnh đề 09.8(b), vế phải nhỏ nhất khi và chỉ khi $p=\tilde p$, vì $c>0$.

**Bước 4: số.** Với $D$ của (a), $c=\tfrac12\cdot\tfrac12+\tfrac12\cdot\tfrac16=\tfrac13$, nên $\tilde p(\mathtt{11})=\tfrac14/\tfrac13=\tfrac34$ và $\tilde p(\mathtt{010000})=\tfrac1{12}/\tfrac13=\tfrac14$. Với hàm lỗi tổng, Mệnh đề 09.8(b) cho điểm cực tiểu $p=p_D=(\tfrac12,\tfrac12)$. Hàm lỗi chuẩn hóa dồn thêm xác suất cho chuỗi ngắn.

**(d) Khi nào hai mục tiêu trùng nhau.** Theo (c), hai điểm cực tiểu là $\tilde p$ và $p_D$. Nếu mọi chuỗi của giá có độ dài $n_0$, thì $c=1/n_0$ và $\tilde p=p_D$. Ngược lại, nếu $\tilde p=p_D$, thì $c\,n(x)=1$ với mọi $x$ có $p_D(x)>0$, nên $n(x)=1/c$ là hằng số trên giá.

**Kiểm tra lại.** Với $D$ của Ví dụ 09.6 (chuỗi $\mathtt{11}$ và mười kí tự $\mathtt 0$), $\mathbb E_Ds(X)=1$ và $\mathbb E_Dn(X)=6$, nên công thức (b) cho $\theta=\tfrac16$ với hàm lỗi tổng và $\tfrac12(1+0)=\tfrac12$ với hàm lỗi chuẩn hóa, khớp hai giá trị của ví dụ.
:::

### Bài tập 09.6 (Mô hình bigram, hàm lỗi log kiểm tra và chuỗi sinh ra; thực nghiệm tùy chọn)

**Mức độ:** tính toán (bắt buộc), khái niệm (bắt buộc), thực nghiệm (tùy chọn). **Mục tiêu:** mục tiêu học tập 3; đọc lỗi kiểm tra qua nhiều hạt giống ngẫu nhiên (random seed), so nó với một chuỗi sinh ra, và tách kết quả thí nghiệm khỏi chứng minh.

::: exercise Bài tập 09.6
Thí nghiệm của Ví dụ 09.8 (giao thức ở Phụ lục C: xích Markov trên $\{\mathtt A,\mathtt C,\mathtt G,\mathtt T\}$, $n=200$, $200$ chuỗi kiểm tra độc lập, mười hạt giống $0,\ldots,9$) cho các số dưới đây. "Lỗi kiểm tra" là hàm lỗi log trung bình theo kí tự trên mẫu kiểm tra. Với mỗi hạt giống, mô hình làm trơn cộng một (add-one smoothing) và mô hình thật được đánh giá trên cùng mẫu kiểm tra. Cột "Hiệu" ghi trung bình qua mười hạt giống của hiệu (làm trơn trừ thật, cùng hạt giống). Trong ngoặc là độ lệch chuẩn (standard deviation) của mười hiệu.

| $m$ | Làm trơn | Hiệu (độ lệch chuẩn) |
|---|---|---|
| $1$ | $1{,}122$ | $0{,}0316$ ($0{,}0130$) |
| $5$ | $1{,}097$ | $0{,}0067$ ($0{,}0035$) |
| $50$ | $1{,}091$ | $0{,}00071$ ($0{,}00040$) |
| $500$ | $1{,}088$ | $0{,}00008$ ($0{,}00005$) |

Với $m=50$, độ lệch chuẩn qua mười hạt giống của lỗi kiểm tra là $0{,}0041$ với mô hình làm trơn và $0{,}0040$ với mô hình thật. Mọi xác suất của mười mô hình làm trơn học với $m=50$ không nhỏ hơn $0{,}087$.

Xét thêm mô hình bigram $p_{\mathrm{alt}}$ có kí tự đầu rút đều. Mỗi hàng của bảng chuyển giữ nguyên kí tự với xác suất $0{,}46$ và chia $0{,}54$ còn lại cho ba kí tự kia theo tỉ lệ của hàng tương ứng ở Phụ lục C; hàng $\mathtt A$ là $(0{,}46;\,0{,}27;\,0{,}135;\,0{,}135)$. Trên mười mẫu kiểm tra của dòng $m=50$, hiệu giữa lỗi kiểm tra của $p_{\mathrm{alt}}$ và của mô hình thật có trung bình $0{,}0392$ và độ lệch chuẩn $0{,}0012$.

Chuỗi sinh ra của Phụ lục C ($40$ kí tự từ mô hình làm trơn học trên $m=50$ chuỗi của hạt giống $0$) có $18$ trong $39$ cặp liền nhau giữ nguyên kí tự. Đường chéo của bảng chuyển học được là $0{,}595$; $0{,}605$; $0{,}592$; $0{,}600$. Trong $200\,000$ chuỗi $40$ kí tự rút từ mô hình học được, số cặp giữ nguyên có trung bình $23{,}3$ và độ lệch chuẩn $3{,}06$.

**(a)** (Bắt buộc, tính toán.)

- **(i)** Với mỗi $m$, tính *sai số chuẩn* (standard error) của hiệu theo hạt giống và tỉ số giữa hiệu trung bình và sai số chuẩn. Ở $m=50$, so với sai số chuẩn khi coi hai mô hình được đánh giá trên hai nhóm mẫu kiểm tra độc lập.
- **(ii)** Tính kì vọng của lỗi kiểm tra của $p_{\mathrm{alt}}$ trừ giá trị tốt nhất $\mathrm H(p_D)/200$, rồi so với hiệu đo được $0{,}0392$.
- **(iii)** So $18$ cặp giữ nguyên với phân bố mô phỏng dưới mô hình học được và với kì vọng dưới $p_{\mathrm{alt}}$. Một chuỗi $40$ kí tự có phân biệt được mô hình học được với $p_{\mathrm{alt}}$ không? Lỗi kiểm tra trên $200$ chuỗi có phân biệt được không?

**(b)** (Bắt buộc, khái niệm.)

- **(i)** Với $\delta=0{,}05$, dùng cách của Ví dụ 09.4 để tính bán kính tin cậy Hoeffding cho lỗi kiểm tra của một mô hình làm trơn học với $m=50$. Cỡ mẫu trong cận là bao nhiêu? So bán kính với độ lệch chuẩn qua hạt giống.
- **(ii)** Nêu những kết luận các số trên cho phép và những kết luận chúng không cho phép.

**(c)** (Thực nghiệm, tùy chọn.) Viết một chương trình chỉ dùng NumPy theo Phụ lục C và tái lập dòng $m=50$. Sau đó, với mỗi hạt giống, sinh $200$ chuỗi $40$ kí tự từ mô hình làm trơn và đo tỉ lệ cặp giữ nguyên. Ghi dự đoán trước khi chạy. Bài không cần huấn luyện mô hình lớn.
:::

::: hint Gợi ý 1
Phần (a)(i). Hai mô hình dùng chung mẫu kiểm tra trong mỗi hạt giống, nên đơn vị ngẫu nhiên là hạt giống. Phần (a)(ii). Lấy kì vọng hai vế của Mệnh đề 09.3(b) như Ví dụ 09.8, Bước 1. Phần (b)(i). Ví dụ 09.4 cần một mô hình không phụ thuộc mẫu kiểm tra và một cận dưới $c$ cho các xác suất.
:::

::: hint Gợi ý 2
Phần (a)(i). Sai số chuẩn bằng độ lệch chuẩn của mười hiệu chia $\sqrt{10}\approx3{,}162$; với hai nhóm độc lập, nó là $\sqrt{s_1^2+s_2^2}/\sqrt{10}$. Phần (a)(ii). Mọi kí tự có phân bố đều (Phụ lục C), và mọi hàng có cùng $\mathrm{KL}$ giữa hàng thật và hàng của $p_{\mathrm{alt}}$. Phần (a)(iii). Dưới $p_{\mathrm{alt}}$, mỗi cặp giữ nguyên với xác suất $0{,}46$ bất kể kí tự đứng trước. Phần (b)(i). Mô hình được học trước khi rút mẫu kiểm tra.
:::

::: solution Lời giải Bài tập 09.6
**(a) Tính trên số đã chạy.**

**Bước 1: sai số chuẩn của hiệu theo hạt giống.** Mỗi ô ghi sai số chuẩn, rồi tỉ số giữa hiệu trung bình và sai số chuẩn.

| $m$ | Sai số chuẩn | Tỉ số |
|---|---|---|
| $1$ | $0{,}0041$ | $7{,}7$ |
| $5$ | $0{,}0011$ | $6{,}0$ |
| $50$ | $0{,}00013$ | $5{,}7$ |
| $500$ | $0{,}000016$ | $5{,}1$ |

Ví dụ, ở $m=50$: $0{,}00040/3{,}162\approx0{,}000125$ và $0{,}00071/0{,}000125\approx5{,}7$. Ở mọi $m$, hiệu lớn hơn năm lần sai số chuẩn, nên trên cùng mẫu kiểm tra, mô hình làm trơn cho lỗi kiểm tra cao hơn mô hình thật.

**Bước 2: hai nhóm độc lập.** Ở $m=50$, coi hai nhóm độc lập cho
$$
\begin{aligned}
&\frac{\sqrt{0{,}0041^2+0{,}0040^2}}{\sqrt{10}}\\
&\approx\frac{0{,}00573}{3{,}162}\approx0{,}0018 .
\end{aligned}
$$
Khi đó tỉ số chỉ còn $0{,}00071/0{,}0018\approx0{,}4$. Lỗi kiểm tra của hai mô hình dao động cùng nhau theo mẫu kiểm tra, và hiệu trong từng hạt giống loại phần dao động chung này.

**Bước 3: kì vọng của lỗi kiểm tra của $p_{\mathrm{alt}}$.** Theo Mệnh đề 09.3(b), lấy kì vọng theo $p_D$. Phân bố của kí tự đầu dưới $p_{\mathrm{alt}}$ trùng phân bố thật, nên số hạng thứ nhất không góp phần vượt. Với $j\ge2$, khi biết $x_{j-1}$, số hạng thứ $j$ có kì vọng có điều kiện bằng entropy chéo giữa hàng thật và hàng của $p_{\mathrm{alt}}$, tức entropy của hàng thật cộng $\mathrm{KL}$ giữa hai hàng (Mệnh đề 09.8(a)). Với hàng $\mathtt A$, gọi phân kì này là $K_{\mathtt A}$:
$$
\begin{aligned}
K_{\mathtt A}&=0{,}6\ln\tfrac{0{,}6}{0{,}46}\\
&\quad+0{,}2\ln\tfrac{0{,}2}{0{,}27}\\
&\quad+2\cdot0{,}1\ln\tfrac{0{,}1}{0{,}135}\\
&\approx0{,}15942-0{,}06002\\
&\quad-0{,}06002\\
&=0{,}03938 .
\end{aligned}
$$
Mỗi hàng khác của hai bảng là cùng một hoán vị của hàng $\mathtt A$, nên phân kì có cùng giá trị. Có $199$ số hạng chuyển trên $200$ kí tự, nên phần vượt trên giá trị tốt nhất là $\tfrac{199}{200}\cdot0{,}03938\approx0{,}0392$, khớp hiệu đo được.

**Bước 4: chuỗi sinh ra.** Dưới mô hình học được, $18$ cách trung bình $23{,}3$ khoảng $(18-23{,}3)/3{,}06\approx-1{,}7$ độ lệch chuẩn. Dưới $p_{\mathrm{alt}}$, số cặp giữ nguyên có kì vọng $39\cdot0{,}46\approx17{,}9$. Con số $18$ gần kì vọng dưới $p_{\mathrm{alt}}$ hơn, dù chuỗi được sinh từ mô hình học được. Một chuỗi $40$ kí tự không phân biệt được hai mô hình.

**Bước 5: lỗi kiểm tra.** Hiệu $0{,}0392$ của $p_{\mathrm{alt}}$ lớn hơn khoảng $33$ lần độ lệch chuẩn $0{,}0012$ của nó, nên một mẫu kiểm tra $200$ chuỗi tách được $p_{\mathrm{alt}}$ khỏi mô hình thật. So với mô hình học được, hiệu trung bình là $0{,}0392-0{,}00071\approx0{,}0385$; theo bất đẳng thức tam giác cho độ lệch chuẩn, độ lệch chuẩn của hiệu này không quá $0{,}0012+0{,}00040=0{,}0016$, nhỏ hơn khoảng $24$ lần hiệu. Lỗi kiểm tra cũng tách $p_{\mathrm{alt}}$ khỏi mô hình học được.

**(b) Phạm vi của kết luận.**

**Bước 1: cận Hoeffding.** Mô hình làm trơn được học trước khi rút mẫu kiểm tra, nên nó cố định đối với mẫu kiểm tra. Mỗi số hạng của hàm lỗi log thuộc $[0,\ln(1/c)]$ với $\ln(1/0{,}087)\approx2{,}4418$. Theo Ví dụ 09.4, Bước 2–3, với $200$ chuỗi kiểm tra, bán kính theo kí tự là
$$
\begin{aligned}
&\ln(1/c)\sqrt{\ln(2/\delta)/(2\cdot200)}\\
&\approx2{,}4418\cdot0{,}09603\le0{,}2345 .
\end{aligned}
$$
Cỡ mẫu trong cận là $200$ chuỗi, không phải $40\,000$ kí tự.

**Bước 2: so với dao động đo được.** Bán kính $0{,}2345$ lớn hơn khoảng $57$ lần độ lệch chuẩn $0{,}0041$ qua hạt giống. Cận đúng với mọi phân bố có hàm lỗi trong đoạn đó, nên nó lỏng với xích Markov này.

**Bước 3: kết luận được phép.** Trong thiết lập của Phụ lục C, lỗi kiểm tra của mô hình làm trơn tiến về giá trị tốt nhất $1{,}0904$ khi $m$ tăng, và hiệu với mô hình thật giảm từ $0{,}0316$ ở $m=1$ xuống $0{,}00008$ ở $m=500$.

**Bước 4: kết luận không được phép.** Các số là kết quả thí nghiệm cho một thiết lập, không phải chứng minh. Chúng không cho tốc độ giảm của hiệu với phân bố khác, với lớp mô hình không chứa phân bố thật, với mạng nơ-ron hay với Thiết lập B.

**(c) Một giao thức mẫu.**

**Bước 1: dự đoán.** Đường chéo của các bảng học được gần $0{,}6$, nên dự đoán tỉ lệ giữ nguyên gần $0{,}6$.

**Bước 2: chương trình.** Học mô hình làm trơn với $m=50$ theo thứ tự rút của Phụ lục C, rồi sinh $200$ chuỗi bằng một bộ sinh riêng để không đổi các số của dòng $m=50$. Đơn vị quan sát là một chuỗi sinh ra, vì các cặp trong một chuỗi phụ thuộc nhau.

**Bước 3: một lần chạy.** Một lần chạy cho trung bình $0{,}597$ qua mười hạt giống (từ $0{,}586$ đến $0{,}621$), khớp dự đoán.

**Kiểm tra lại.** Với $m=1$, hiệu $0{,}0316$ khớp con số "khoảng $0{,}032$" của Ví dụ 09.8, Bước 4. Cận ở (b) với $c=0{,}05$ và $50$ chuỗi cho $0{,}5754$, đúng Ví dụ 09.4, Bước 3.
:::

### Bài tập 09.7 (SGD với gradient theo đường đi cho một mục tiêu lồi)

**Mức độ:** kiểm tra giả thiết, tính toán. **Mục tiêu:** mục tiêu học tập 5; kiểm (C), (G1), (G2) của Định lý 05.14 cho gradient tái tham số hóa, và đọc giới hạn của kết quả.

::: exercise Bài tập 09.7
Xét mô hình của Ví dụ 09.9 tại $x=2$ với $\theta$ cố định; chỉ tối ưu $w=(\mu,\sigma)$ của $q_\phi=N(\mu,\sigma^2)$. Hàm mục tiêu là $F(\mu,\sigma)=-\operatorname{ELBO}(\mu,\sigma)$ của Phụ lục A(iii), xác định trên $\Phi=\mathbb R\times(0,\infty)$. Lấy $W=[0,2]\times[\tfrac12,1]$, $w_1=(0,1)$, nguồn ngẫu nhiên $\zeta\sim N(0,1)$ và ánh xạ oracle $\varphi(w,\zeta)=-\nabla_{\mu,\sigma}\kappa(\mu,\sigma,\zeta)$, với $\kappa$ của Ví dụ 09.11.

**(a)** Định nghĩa 05.10 và (C) cần một hàm lồi xác định trên toàn $\mathbb R^2$. Dựng một hàm lồi, khả vi $\tilde F$ trên $\mathbb R^2$ trùng $F$ trên $\mathbb R\times[\tfrac14,\infty)$, và kiểm (C) cho $(\tilde F,W)$.

**(b)** Kiểm (G1): dùng Mệnh đề 09.15 để chứng minh $\mathbb E\varphi(w,\zeta)=\nabla F(w)\in\partial\tilde F(w)$ với mọi $w\in W$. Lân cận ở Ví dụ 09.11, Bước 4 không chứa điểm $(2,\tfrac12)$ của $W$.

**(c)** Kiểm (G2): tính $\mathbb E\lVert\varphi(w,\zeta)\rVert^2$ và giá trị lớn nhất của nó trên $W$, rồi suy ra $G$.

**(d)** Với $T=10^4$, tính $R$, độ dài bước và cận của Hệ quả 05.15 cho $\mathbb EF(\bar w_T)-\min_\Phi F$. Đại lượng này bằng kì vọng của phân kì KL nào? Một mô phỏng (Thuật toán 05.11 với độ dài bước trên, $20$ hạt giống) cho trung bình $0{,}00014$ của đại lượng này; so với cận.

**(e)** Thay $W$ bằng $[0,2]\times[\sigma_0,1]$. Tính $G$ với $\sigma_0=0{,}1$ và nêu điều xảy ra khi $\sigma_0\to0$. Kết luận có chuyển sang việc học đồng thời $\theta$ và $\phi$ của một mô hình có mạng nơ-ron không?
:::

::: hint Gợi ý 1
Phần (a). $F$ là tổng của một hàm theo $\mu$ và $g(\sigma)=\sigma^2-\ln\sigma$ (cộng hằng số); chỉ cần thác triển $g$ sang $\sigma<\tfrac14$ sao cho đạo hàm vẫn không giảm. Phần (c). Dùng $\mathbb E\zeta=\mathbb E\zeta^3=0$, $\mathbb E\zeta^2=1$, $\mathbb E\zeta^4=3$.
:::

::: hint Gợi ý 2
Phần (a). Thay $g$ trên $(-\infty,\tfrac14)$ bằng tiếp tuyến của nó tại $\tfrac14$. Phần (b). Quanh $(\mu_0,\sigma_0)$, lấy $U=\{\lvert\mu-\mu_0\rvert<1,\ \sigma_0/2<\sigma<2\sigma_0\}$; trên $U$, $1/\sigma<2/\sigma_0$. Phần (c). Viết $\varphi=(\varphi_\mu,\varphi_\sigma)$ với $\varphi_\mu=2\mu-2+\sigma\zeta$ và $\varphi_\sigma=-(2-\mu)\zeta+\sigma\zeta^2+\sigma-1/\sigma$. Hai số hạng của $\mathbb E\lVert\varphi\rVert^2$ theo $\mu$ và theo $\sigma$ tách rời và đều lồi.
:::

::: solution Lời giải Bài tập 09.7
**(a) Giả thiết (C).**

**Bước 1: tách biến.** Theo Phụ lục A(iii),
$$
\begin{aligned}
F(\mu,\sigma)&=a_0+\tfrac12(2-\mu)^2\\
&\quad+\tfrac12\mu^2+g(\sigma),
\end{aligned}
$$
với $a_0=\tfrac12\ln(2\pi)-\tfrac12$ và $g(\sigma)=\sigma^2-\ln\sigma$. Phần theo $\mu$ lồi trên $\mathbb R$; $g''(\sigma)=2+1/\sigma^2>0$, nên $g$ lồi trên $(0,\infty)$.

**Bước 2: thác triển.** Đặt $\tilde g=g$ trên $[\tfrac14,\infty)$ và $\tilde g(\sigma)=g(\tfrac14)+g'(\tfrac14)(\sigma-\tfrac14)$ trên $(-\infty,\tfrac14)$, với $g'(\tfrac14)=\tfrac12-4=-3{,}5$. Hàm $\tilde g$ khả vi liên tục, và $\tilde g'$ không giảm (hằng $-3{,}5$, rồi bằng $g'$ tăng), nên $\tilde g$ lồi. Đặt $\tilde F$ như $F$ với $\tilde g$ thay cho $g$. Khi đó $\tilde F$ lồi, khả vi trên $\mathbb R^2$ và trùng $F$ trên $\mathbb R\times[\tfrac14,\infty)$, một tập chứa một lân cận của $W$.

**Bước 3: tập tham số.** $W$ là tích hai đoạn đóng, nên khác rỗng, đóng, lồi. Vậy $(\tilde F,W)$ thỏa (C). Định lý 05.14 chỉ dùng hàm mục tiêu trên $W$, nơi $\tilde F=F$.

**(b) Giả thiết (G1).**

**Bước 1: điều kiện (i).** Với mọi $\zeta$, $\kappa(\mu,\sigma,\zeta)$ là đa thức theo $(\mu,\sigma,\zeta)$ cộng $\ln\sigma^2$, nên khả vi liên tục trên $\Phi$; $N_0=\varnothing$. $\Phi$ mở.

**Bước 2: điều kiện (ii).** Cố định $(\mu_0,\sigma_0)\in\Phi$ và $U$ như Gợi ý 2. Theo Ví dụ 09.11, Bước 2, trên $U$,
$$
\begin{aligned}
\lvert\partial_\mu\kappa\rvert&\le\lvert2-2\mu\rvert+\sigma\lvert\zeta\rvert\\
&\le(4+2\lvert\mu_0\rvert)+2\sigma_0\lvert\zeta\rvert,\\
\lvert\partial_\sigma\kappa\rvert&\le(3+\lvert\mu_0\rvert)\lvert\zeta\rvert+2\sigma_0\zeta^2\\
&\quad+2\sigma_0+2/\sigma_0 .
\end{aligned}
$$
Do đó $\lVert\nabla\kappa\rVert\le C_0(1+\zeta^2)=M(\zeta)$ với một hằng số $C_0$ phụ thuộc $(\mu_0,\sigma_0)$, và $\mathbb EM(\zeta)=2C_0<\infty$.

**Bước 3: điều kiện (iii) và kết luận.** $\kappa$ là đa thức bậc hai theo $\zeta$ với hệ số hữu hạn, nên $\mathbb E\lvert\kappa\rvert<\infty$. Theo Mệnh đề 09.15, $\operatorname{ELBO}=\mathbb E\kappa$ khả vi và $\nabla\operatorname{ELBO}=\mathbb E\nabla\kappa$. Đổi dấu, $\mathbb E\varphi(w,\zeta)=\nabla F(w)=(2\mu-2,\ 2\sigma-1/\sigma)$. Với $w\in W$, $\nabla F(w)=\nabla\tilde F(w)\in\partial\tilde F(w)$ theo Mệnh đề 05.3(a). Định nghĩa 05.10 cần $\varphi$ xác định trên cả $\mathbb R^2$; đặt $\varphi=0$ khi $\sigma\le0$, vì thuật toán chỉ gọi oracle tại các điểm của $W$.

**(c) Giả thiết (G2).**

**Bước 1: thành phần $\mu$.** $\mathbb E\varphi_\mu^2=(2\mu-2)^2+\sigma^2$.

**Bước 2: thành phần $\sigma$.** Viết $\varphi_\sigma=b\zeta+\sigma\zeta^2+e$ với $b=-(2-\mu)$, $e=\sigma-1/\sigma$. Các số hạng chéo chứa $\mathbb E\zeta$ hoặc $\mathbb E\zeta^3$ bằng $0$, nên
$$
\begin{aligned}
\mathbb E\varphi_\sigma^2&=b^2+3\sigma^2+e^2+2\sigma e\\
&=(2-\mu)^2+5\sigma^2\\
&\quad+(\sigma-1/\sigma)^2-2 .
\end{aligned}
$$

**Bước 3: giá trị lớn nhất trên $W$.** Cộng hai thành phần và nhóm theo biến. Phần theo $\mu$ là $(2\mu-2)^2+(2-\mu)^2=5\mu^2-12\mu+8$. Phần theo $\sigma$ là $\sigma^2+5\sigma^2+(\sigma^2-2+1/\sigma^2)-2=7\sigma^2+1/\sigma^2-4$. Do đó
$$
\begin{aligned}
\mathbb E\lVert\varphi\rVert^2&=\big(5\mu^2-12\mu+8\big)\\
&\quad+\big(7\sigma^2+1/\sigma^2-4\big).
\end{aligned}
$$
Hai ngoặc lồi, nên lớn nhất tại đầu mút. Ngoặc đầu bằng $8$ tại $\mu=0$ và $4$ tại $\mu=2$; ngoặc sau bằng $1{,}75$ tại $\sigma=\tfrac12$ và $4$ tại $\sigma=1$. Giá trị lớn nhất là $12$ tại $(0,1)$, nên (G2) thỏa với $G=\sqrt{12}=2\sqrt3\approx3{,}4641$.

**(d) Cận của Hệ quả 05.15.**

**Bước 1: hằng số.** Điểm của $W$ xa $w_1=(0,1)$ nhất là $(2,\tfrac12)$, nên $R=\sqrt{4+0{,}25}\approx2{,}0616$ và mọi $u\in W$ có $\lVert w_1-u\rVert\le R$. Độ dài bước là
$$
\begin{aligned}
\eta=\frac R{G\sqrt T}&\approx\frac{2{,}0616}{3{,}4641\cdot100}\\
&\approx0{,}00595 .
\end{aligned}
$$

**Bước 2: đối tượng so sánh.** Điểm cực tiểu của $F$ trên $\Phi$ là $(1,1/\sqrt2)$ (Phụ lục A(iii)), thuộc $W$ vì $\tfrac12\le0{,}7071\le1$. Theo Hệ quả 05.15(b), $F_R=\min_WF=\min_\Phi F=-\ln p_\theta(2)\approx2{,}2655$.

**Bước 3: cận.**
$$
\begin{aligned}
&\mathbb EF(\bar w_T)-\min_\Phi F\\
&\le\frac{RG}{\sqrt T}=\frac{\sqrt{51}}{100}\le0{,}0715 .
\end{aligned}
$$

**Bước 4: ý nghĩa.** Theo Định lý 09.12(a), $F(w)-\min_\Phi F=\ln p_\theta(2)-\operatorname{ELBO}(w)=\mathrm{KL}\big(q_w\Vert p_\theta(\cdot\mid2)\big)$. Cận nói rằng kì vọng của phân kì KL từ $q_{\bar w_T}$ tới hậu nghiệm $N(1,\tfrac12)$ không quá $0{,}0715$. Trung bình mô phỏng $0{,}00014$ nhỏ hơn cận khoảng $500$ lần; cận đúng cho mọi hàm lồi có cùng $R$ và $G$.

**(e) Giới hạn.**

**Bước 1: $\sigma_0$ nhỏ.** Ngoặc thứ hai ở (c), Bước 3 có số hạng $1/\sigma^2$. Với $\sigma_0=0{,}1$, nó bằng $0{,}07+100-4=96{,}07$ tại $\sigma=0{,}1$, nên $G^2=8+96{,}07$ và $G\approx10{,}20$. Khi $\sigma_0\to0$, $G\to\infty$, nên (G2) không thỏa trên $[0,2]\times(0,1]$, một tập cũng không đóng. Ngoài ra cần $\sigma_0\le1/\sqrt2$ để điểm cực tiểu thuộc $W$.

**Bước 2: không chuyển sang học sâu.** Ở đây $\theta$ cố định và chỉ có một quan sát; cận nói về độ chênh tối ưu, không về $L_D$. Khi học đồng thời $\theta$ và $\phi$ với mạng nơ-ron, $-\operatorname{ELBO}$ nói chung không lồi (§9), (C) không thỏa và Định lý 05.14 không áp dụng.

**Kiểm tra lại.** Tại $w_1=(0,1)$, $\mathbb E\varphi=(-2,1)$, khớp gradient $(2,-1)$ của ELBO ở Ví dụ 09.11, Bước 1 sau khi đổi dấu; tổng các phương sai $1+6=7$ của ví dụ cộng $\lVert(-2,1)\rVert^2=5$ cho $12$, đúng giá trị của (c) tại $(0,1)$.
:::

## Bài tập chọn từ UML

### Bài tập 09.8 (Ước lượng hợp lý cực đại của phương sai Gauss bị chệch; UML Bài tập 24.1)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 2; viết ước lượng hợp lý cực đại thành ERM với hàm lỗi log cho mật độ, và thấy rằng nó không nhất thiết không chệch. Ý (a), (c) và số ở (b) do học phần thêm.

::: exercise Bài tập 09.8
Cho $x^{(1)},\ldots,x^{(m)}$ độc lập cùng phân bố $N(\mu,\sigma^2)$, cả $\mu$ và $\sigma^2>0$ chưa biết; mô hình là họ mật độ $N(\mu,\sigma^2)$ với $(\mu,\sigma^2)\in\mathbb R\times(0,\infty)$.

**(a)** Với mẫu $s$ có ít nhất hai giá trị khác nhau, viết rủi ro thực nghiệm $L_s(\mu,\sigma^2)$ với hàm lỗi log và chứng minh ước lượng hợp lý cực đại là $\hat\mu=\bar x=\frac1m\sum_ix^{(i)}$ và $\hat\sigma^2=\frac1m\sum_i(x^{(i)}-\bar x)^2$.

**(b)** Chứng minh $\mathbb E\hat\sigma^2=\frac{m-1}m\sigma^2$, nên $\hat\sigma^2$ bị chệch. Lập luận dùng giả thiết Gauss ở đâu? Tính $\mathbb E\hat\sigma^2$ với $m=5$, $\sigma^2=4$.

**(c)** Với $m=1$, chứng minh $\inf L_s=-\infty$, nên không có ước lượng hợp lý cực đại. Nối kết quả này với tính chất của hàm lỗi log cho mật độ ở §2 của ghi chú.
:::

::: hint Gợi ý 1
Phần (a). Với $\sigma^2$ cố định, tối thiểu hóa theo $\mu$ trước, rồi theo $\sigma^2$. Phần (b). Tách $x^{(i)}-\bar x=(x^{(i)}-\mu)-(\bar x-\mu)$.
:::

::: hint Gợi ý 2
Phần (a). $\sum_i(x^{(i)}-\mu)^2=\sum_i(x^{(i)}-\bar x)^2+m(\bar x-\mu)^2$. Phần (b). $\mathbb E(\bar x-\mu)^2=\operatorname{Var}\bar x=\sigma^2/m$ nhờ tính độc lập. Phần (c). Đặt $\mu=x^{(1)}$ và cho $\sigma^2\to0$.
:::

::: solution Lời giải Bài tập 09.8
**(a) Ước lượng hợp lý cực đại.**

**Bước 1: rủi ro thực nghiệm.** Hàm lỗi log của mật độ Gauss tại $x$ là $\tfrac12\ln(2\pi\sigma^2)+(x-\mu)^2/(2\sigma^2)$. Lấy trung bình:
$$
\begin{aligned}
&L_s(\mu,\sigma^2)\\
&=\tfrac12\ln(2\pi\sigma^2)\\
&\quad+\frac1{2\sigma^2m}\sum_{i=1}^m(x^{(i)}-\mu)^2 .
\end{aligned}
$$

**Bước 2: theo $\mu$.** Khai triển $(x^{(i)}-\mu)^2=\big((x^{(i)}-\bar x)+(\bar x-\mu)\big)^2$ và dùng $\sum_i(x^{(i)}-\bar x)=0$: tổng bình phương bằng $mV_s+m(\bar x-\mu)^2$ với $V_s=\frac1m\sum_i(x^{(i)}-\bar x)^2$. Với mọi $\sigma^2$, nó nhỏ nhất tại $\mu=\bar x$.

**Bước 3: theo $\sigma^2$.** Đặt $\nu=\sigma^2$. Tại $\mu=\bar x$, $L_s=\tfrac12\ln(2\pi)+\tfrac12\ln\nu+V_s/(2\nu)$. Đạo hàm theo $\nu$ là $\frac1{2\nu}-\frac{V_s}{2\nu^2}=\frac{\nu-V_s}{2\nu^2}$, âm khi $\nu<V_s$ và dương khi $\nu>V_s$. Vì mẫu có hai giá trị khác nhau, $V_s>0$, nên $\hat\sigma^2=V_s$ là điểm cực tiểu duy nhất.

**(b) Độ chệch.**

**Bước 1: tách tổng.** Với $\mu$ là trung bình thật, đẳng thức của (a), Bước 2 cho
$$
\begin{aligned}
m\hat\sigma^2&=\sum_i(x^{(i)}-\mu)^2\\
&\quad-m(\bar x-\mu)^2 .
\end{aligned}
$$

**Bước 2: kì vọng.** $\mathbb E\sum_i(x^{(i)}-\mu)^2=m\sigma^2$. Các quan sát độc lập, nên $\operatorname{Var}\bar x=\sigma^2/m$ và $\mathbb E\,m(\bar x-\mu)^2=\sigma^2$. Do đó $\mathbb E\,m\hat\sigma^2=(m-1)\sigma^2$.

**Bước 3: phạm vi.** Bước 1–2 chỉ dùng tính độc lập và phương sai hữu hạn; giả thiết Gauss chỉ dùng ở (a) để xác định ước lượng. Với $m=5$, $\sigma^2=4$: $\mathbb E\hat\sigma^2=\tfrac45\cdot4=3{,}2$. Chia cho $m-1$ thay cho $m$ cho một ước lượng không chệch.

**(c) Một quan sát.** Với $m=1$ và $\mu=x^{(1)}$, $L_s=\tfrac12\ln(2\pi\sigma^2)\to-\infty$ khi $\sigma^2\to0$. Do đó không có điểm cực tiểu. Với mật độ, hàm lỗi log có thể âm và không bị chặn dưới (§2 của ghi chú). Khi mọi quan sát bằng nhau, lập luận không đổi.

**Kiểm tra lại.** Với $m=2$, $\hat\sigma^2=\tfrac14(x^{(1)}-x^{(2)})^2$ và $\mathbb E(x^{(1)}-x^{(2)})^2=2\sigma^2$, nên $\mathbb E\hat\sigma^2=\tfrac12\sigma^2=\tfrac{m-1}m\sigma^2$.
:::

### Bài tập 09.9 (Ước lượng hợp lý cực đại có chính quy hóa cho phân bố Bernoulli; UML Bài tập 24.2)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 2; hai quan sát giả chặn dưới các xác suất của mô hình, và cho một cận với xác suất cao cho rủi ro vượt mức với hàm lỗi log.

::: exercise Bài tập 09.9
Cho $D=\mathrm{Ber}(\theta^\star)$ với $\theta^\star\in[0,1]$ chưa biết, mẫu $S\sim D^m$ có $m_1$ quan sát bằng $1$, và mô hình $p_\theta=\mathrm{Ber}(\theta)$ với $\theta\in(0,1)$. Xét mục tiêu có chính quy hóa
$$
\begin{aligned}
J_S(\theta)&=L_S(\theta)-\tfrac1m\ln\theta\\
&\quad-\tfrac1m\ln(1-\theta).
\end{aligned}
$$

**(a)** Chứng minh $J_S$ tỉ lệ với rủi ro thực nghiệm trên mẫu thêm hai quan sát giả $1$ và $0$, rồi suy ra điểm cực tiểu $\hat\theta=(1+m_1)/(m+2)$. Tính $\hat\theta$ với $m=10$, $m_1=7$.

**(b)** Với $\delta\in(0,1)$, chứng minh rằng với xác suất ít nhất $1-\delta$,
$$
\begin{aligned}
\lvert\hat\theta-\theta^\star\rvert&\le\epsilon_m,\\
\epsilon_m&=\tfrac1{m+2}\\
&\quad+\sqrt{\ln(2/\delta)/(2m)} .
\end{aligned}
$$

**(c)** Giả sử $\epsilon_m\le\tfrac16$. Chứng minh rằng trên biến cố của (b),
$$
\begin{aligned}
&L_D(\hat\theta)-L_D(\theta^\star)\le B_m,\\
&B_m=2\epsilon_m\\
&\quad\times\big(1+\ln(2\epsilon_m(m+2))\big).
\end{aligned}
$$
Tính $\epsilon_m$ và $B_m$ với $\delta=0{,}05$ và $m=100$, $1000$, $10^4$.
:::

::: hint Gợi ý 1
Phần (b). Tách $\hat\theta-\theta^\star$ thành $\hat\theta-\mathbb E\hat\theta$ và $\mathbb E\hat\theta-\theta^\star$; dùng Định lý 02.7 cho phần thứ nhất. Phần (c). Theo Mệnh đề 09.8(a), hiệu rủi ro là $\mathrm{KL}\big(\mathrm{Ber}(\theta^\star)\Vert\mathrm{Ber}(\hat\theta)\big)$. Do đối xứng giữa $0$ và $1$, chỉ cần xét $\theta^\star\le\tfrac12$; chia hai trường hợp $\theta^\star>2\epsilon_m$ và $\theta^\star\le2\epsilon_m$.
:::

::: hint Gợi ý 2
Phần (c). Áp dụng $\ln t\le t-1$ với $t=p_1(x)/p_2(x)$ cho $\mathrm{KL}(p_1\Vert p_2)\le\sum_x(p_1(x)-p_2(x))^2/p_2(x)$. Khi $\theta^\star>2\epsilon_m$, ta có $\hat\theta>\epsilon_m$ và $1-\hat\theta\ge\tfrac13$. Khi $\theta^\star\le2\epsilon_m$, dùng $\hat\theta\ge\frac1{m+2}$ cho số hạng $\theta^\star\ln(\theta^\star/\hat\theta)$.
:::

::: solution Lời giải Bài tập 09.9
**(a) Hai quan sát giả.**

**Bước 1: viết lại.** Gọi $s'$ là $S$ thêm một quan sát $1$ (góp $-\ln\theta$) và một quan sát $0$ (góp $-\ln(1-\theta)$). Tổng các hàm lỗi trên $s'$ bằng $mJ_S(\theta)$, nên $J_S(\theta)=\frac{m+2}m\,L_{s'}(\theta)$.

**Bước 2: điểm cực tiểu.** Hệ số $\frac{m+2}m>0$ không đổi điểm cực tiểu. Theo Ví dụ 09.2, Bước 3, áp dụng cho $s'$ có $m+2$ quan sát và $1+m_1$ số $1$, $\hat\theta=(1+m_1)/(m+2)$. Với $m=10$, $m_1=7$: $\hat\theta=\tfrac8{12}=\tfrac23$. Ta luôn có $\frac1{m+2}\le\hat\theta\le\frac{m+1}{m+2}$.

**(b) Cận với xác suất cao.**

**Bước 1: độ chệch.** $\mathbb E\hat\theta=(1+m\theta^\star)/(m+2)$, nên $\lvert\mathbb E\hat\theta-\theta^\star\rvert=\lvert1-2\theta^\star\rvert/(m+2)\le\frac1{m+2}$.

**Bước 2: phần ngẫu nhiên.** $\hat\theta-\mathbb E\hat\theta=\frac m{m+2}\big(\frac{m_1}m-\theta^\star\big)$. Các quan sát nằm trong $[0,1]$ và độc lập, nên theo Định lý 02.7(c), với xác suất ít nhất $1-\delta$, $\lvert\frac{m_1}m-\theta^\star\rvert\le\sqrt{\ln(2/\delta)/(2m)}$.

**Bước 3: bất đẳng thức tam giác.** Vì $\frac m{m+2}\le1$, trên biến cố của Bước 2, $\lvert\hat\theta-\theta^\star\rvert\le\epsilon_m$.

**(c) Cận rủi ro.**

**Bước 1: rủi ro vượt mức.** $\mathrm H(\mathrm{Ber}(\theta^\star))\le\ln2$, và $\hat\theta\in(0,1)$, nên theo Mệnh đề 09.8(a), $L_D(\hat\theta)-L_D(\theta^\star)=\mathrm{KL}(\theta^\star\Vert\hat\theta)$, viết tắt cho phân kì giữa hai phân bố Bernoulli. Đổi vai $0$ và $1$ biến $\theta^\star$, $\hat\theta$ thành $1-\theta^\star$, $1-\hat\theta$ và giữ nguyên $\mathrm{KL}$, nên giả sử $\theta^\star\le\tfrac12$. Ta làm việc trên biến cố của (b).

**Bước 2: cận bằng tổng bình phương.** Với $t=p_1(x)/p_2(x)$, $\ln t\le t-1$ cho
$$
\begin{aligned}
&\mathrm{KL}(p_1\Vert p_2)\\
&\le\sum_x\frac{p_1(x)^2}{p_2(x)}-1\\
&=\sum_x\frac{(p_1(x)-p_2(x))^2}{p_2(x)}.
\end{aligned}
$$
Gọi vế phải là $\chi^2(p_1\Vert p_2)$. Với hai phân bố Bernoulli, nó bằng $(\theta^\star-\hat\theta)^2/\big(\hat\theta(1-\hat\theta)\big)$.

**Bước 3: trường hợp $\theta^\star>2\epsilon_m$.** Khi đó $\hat\theta\ge\theta^\star-\epsilon_m>\epsilon_m$ và $1-\hat\theta\ge1-\tfrac12-\tfrac16=\tfrac13$. Theo Bước 2,
$$
\mathrm{KL}\le\frac{\epsilon_m^2}{\epsilon_m\cdot\frac13}=3\epsilon_m .
$$
Theo định nghĩa, $\epsilon_m\ge\frac1{m+2}$, nên $2\epsilon_m(m+2)\ge2$ và $B_m\ge2\epsilon_m(1+\ln2)>3\epsilon_m$.

**Bước 4: trường hợp $\theta^\star\le2\epsilon_m$, số hạng thứ nhất.** Số hạng $\theta^\star\ln(\theta^\star/\hat\theta)$ không quá $\theta^\star\ln\big(\theta^\star(m+2)\big)$ vì $\hat\theta\ge\frac1{m+2}$. Hàm $y\mapsto y\ln(y(m+2))$ âm khi $y(m+2)<1$ và tăng khi $y(m+2)\ge1$, nên trên $[0,2\epsilon_m]$ nó không quá $2\epsilon_m\ln(2\epsilon_m(m+2))$, một số dương.

**Bước 5: số hạng thứ hai.** Ta có $\hat\theta\le\theta^\star+\epsilon_m\le3\epsilon_m\le\tfrac12$, nên $1-\hat\theta\ge\tfrac12$. Theo $\ln t\le t-1$,
$$
\begin{aligned}
&(1-\theta^\star)\ln\frac{1-\theta^\star}{1-\hat\theta}\\
&\le\frac{(1-\theta^\star)(\hat\theta-\theta^\star)}{1-\hat\theta}\\
&\le2\epsilon_m .
\end{aligned}
$$
Cộng hai số hạng: $\mathrm{KL}\le B_m$.

**Bước 6: số.** Với $\delta=0{,}05$, $\ln40\approx3{,}6889$.

| $m$ | $\epsilon_m$ | $B_m$ |
|---|---|---|
| $100$ | $0{,}1457$ | $1{,}279$ |
| $1000$ | $0{,}04395$ | $0{,}4815$ |
| $10^4$ | $0{,}01369$ | $0{,}1810$ |

Với $m=100$, các phép tính là
$$
\begin{aligned}
&\epsilon_m=\tfrac1{102}+\sqrt{3{,}6889/200}\\
&\quad\approx0{,}00980+0{,}13581\\
&\quad=0{,}14561,\\
&2\epsilon_m(m+2)\approx29{,}70,\\
&B_m\approx0{,}2912\cdot(1+3{,}391)\\
&\quad\approx1{,}2789 .
\end{aligned}
$$
Cận đúng với mọi $\theta^\star$ và giảm theo tốc độ $\ln m/\sqrt m$.

**Kiểm tra lại.** Tính bằng máy với phân bố nhị thức, phân vị $95\%$ của $\mathrm{KL}(\theta^\star\Vert\hat\theta)$, lấy lớn nhất theo $\theta^\star$ trên lưới bước $0{,}001$ của $[0,\tfrac12]$, là $0{,}0210$; $0{,}0020$; $0{,}0002$ với $m=100$; $1000$; $10^4$. Mọi giá trị nằm dưới $B_m$.
:::

### Bài tập 09.10 (Tùy chọn: bước M cho trọng số hỗn hợp; UML Bài tập 24.3)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 2 và 4; giải phần trọng số của bước M (Hệ quả 09.13) bằng tính không âm của phân kì KL. UML đặt bài này trong thuật toán EM cho hỗn hợp Gauss (UML §24.4.2).

::: exercise Bài tập 09.10
Cho $\nu=(\nu_1,\ldots,\nu_K)$ với mọi $\nu_y\ge0$ và $\sum_y\nu_y>0$. Bài toán là tìm
$$
\max_c\ \sum_{y=1}^K\nu_y\ln c_y
$$
trên tập các véc-tơ $c=(c_1,\ldots,c_K)$ có mọi $c_y>0$ và $\sum_yc_y=1$.

**(a)** Xét một mô hình hỗn hợp $p_\theta(x,v)=c_v\,p_\theta(x\mid v)$ với $v\in\{1,\ldots,K\}$, trong đó trọng số hỗn hợp $c=(c_1,\ldots,c_K)$ là một phần của $\theta$ và các mật độ có điều kiện không phụ thuộc $c$. Chứng minh rằng phần phụ thuộc $c$ của hàm mục tiêu ở bước M của Hệ quả 09.13 có dạng trên, và xác định $\nu$.

**(b)** Đặt $c^\star=\nu/\sum_y\nu_y$. Chứng minh $c^\star$ là một véc-tơ xác suất và
$$
\begin{aligned}
&\sum_y\nu_y\ln c_y\\
&=\Big(\sum_y\nu_y\Big)\big(-\mathrm H(c^\star)\\
&\qquad-\mathrm{KL}(c^\star\Vert c)\big).
\end{aligned}
$$

**(c)** Suy ra $c^\star$ là nghiệm khi mọi $\nu_y>0$. Điều gì xảy ra khi có $\nu_y=0$? Tính nghiệm, giá trị lớn nhất và giá trị tại $c$ đều với $\nu=(2,1,1)$.
:::

::: hint Gợi ý 1
Phần (a). Viết $\ln p_\theta(x^{(i)},v)=\ln c_v+\ln p_\theta(x^{(i)}\mid v)$ và đổi thứ tự hai tổng theo $i$ và $v$. Phần (b). Thay $\nu_y=\big(\sum_{y'}\nu_{y'}\big)c^\star_y$.
:::

::: hint Gợi ý 2
Phần (b). $c^\star_y\ln c_y=c^\star_y\ln c^\star_y-c^\star_y\ln(c^\star_y/c_y)$ với $c^\star_y>0$; các số hạng có $c^\star_y=0$ bằng $0$. Phần (c). Áp dụng Mệnh đề 09.8(b) cho hai hàm xác suất trên $\{1,\ldots,K\}$.
:::

::: solution Lời giải Bài tập 09.10
**(a) Bước M.** Với các phân bố $q_i$ của bước E, hàm mục tiêu của bước M là
$$
\begin{aligned}
&\textstyle\sum_{i,v}q_i(v)\ln p_\theta(x^{(i)},v)\\
&=\sum_v\Big(\sum_iq_i(v)\Big)\ln c_v\\
&\quad+\textstyle\sum_{i,v}q_i(v)\ln p_\theta(x^{(i)}\mid v).
\end{aligned}
$$
Số hạng thứ hai không phụ thuộc $c$. Phần phụ thuộc $c$ có dạng của bài toán với $\nu_v=\sum_iq_i(v)\ge0$ và $\sum_v\nu_v=m>0$.

**(b) Viết lại mục tiêu.**

**Bước 1: véc-tơ xác suất.** $c^\star_y\ge0$ vì $\nu_y\ge0$, và $\sum_yc^\star_y=1$.

**Bước 2: đẳng thức.** Đặt $\nu_+=\sum_y\nu_y$. Với $c$ thỏa ràng buộc, các số hạng có $\nu_y=0$ bằng $0$, nên
$$
\begin{aligned}
&\sum_y\nu_y\ln c_y\\
&=\nu_+\sum_{c^\star_y>0}c^\star_y\ln c_y\\
&=\nu_+\Big(\sum_{c^\star_y>0}c^\star_y\ln c^\star_y\\
&\qquad-\sum_{c^\star_y>0}c^\star_y\ln\frac{c^\star_y}{c_y}\Big),
\end{aligned}
$$
tức $\nu_+\big(-\mathrm H(c^\star)-\mathrm{KL}(c^\star\Vert c)\big)$ theo Định nghĩa 09.7. Mọi số hạng hữu hạn vì $c_y>0$.

**(c) Nghiệm.**

**Bước 1: mọi $\nu_y>0$.** Khi đó $c^\star_y>0$, nên $c^\star$ thỏa ràng buộc. Theo (b), làm lớn nhất mục tiêu tương đương làm nhỏ nhất $\mathrm{KL}(c^\star\Vert c)$, vì $\nu_+>0$ và $\mathrm H(c^\star)$ không phụ thuộc $c$. Theo Mệnh đề 09.8(b), $\mathrm{KL}(c^\star\Vert c)\ge0$, dấu bằng khi và chỉ khi $c=c^\star$. Vậy $c^\star$ là nghiệm duy nhất.

**Bước 2: có $\nu_y=0$.** Khi đó $c^\star_y=0$, nên $c^\star$ vi phạm ràng buộc $c_y>0$. Theo (b), mục tiêu không vượt $-\nu_+\mathrm H(c^\star)$ và tiến tới giá trị này khi $c\to c^\star$ với mọi $c_y>0$, vì chỉ các số hạng có $c^\star_y>0$ tham gia $\mathrm{KL}$. Giá trị đó không đạt tại điểm nào thỏa ràng buộc, vì $\mathrm{KL}(c^\star\Vert c)=0$ chỉ khi $c=c^\star$; bài toán không có nghiệm. Nếu nới ràng buộc thành $c_y\ge0$, với quy ước $0\ln0=0$, thì $c^\star$ là nghiệm.

**Bước 3: số.** Với $\nu=(2,1,1)$, $\nu_+=4$ và $c^\star=(\tfrac12,\tfrac14,\tfrac14)$. Giá trị lớn nhất là
$$
\begin{aligned}
2\ln\tfrac12+2\ln\tfrac14&=-6\ln2\\
&\approx-4{,}1589 .
\end{aligned}
$$
Tại $c$ đều, giá trị là $4\ln\tfrac13\approx-4{,}3944$. Hiệu $0{,}2356$ bằng $4\,\mathrm{KL}\big(c^\star\Vert(\tfrac13,\tfrac13,\tfrac13)\big)$.

**Kiểm tra lại.** Theo Bài tập 09.3(b), $\mathrm{KL}\big((\tfrac12,\tfrac14,\tfrac14)\Vert(\tfrac13,\tfrac13,\tfrac13)\big)\approx0{,}0589$, và $4\cdot0{,}0589=0{,}2356$, khớp hiệu ở Bước 3.
:::
