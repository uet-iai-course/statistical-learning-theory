# Bài 02 — Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn

Mệnh đề 01.7 cho đẳng thức $\mathbb E_S[L_S(h)]=L_D(h)$ với một giả thuyết (hypothesis) $h$ chọn trước khi lấy mẫu. Đẳng thức đó không cho biết rủi ro thực nghiệm (empirical risk) $L_S(h)$ lệch khỏi rủi ro kì vọng (population risk) $L_D(h)$ bao nhiêu trên một mẫu cụ thể. Trong khi đó, học xấp xỉ với xác suất cao (probably approximately correct, PAC) theo Định nghĩa 01.25 cần một bảo đảm với xác suất cao cho $L_D(A(S))$.

Câu hỏi trung tâm của bài là: khi lớp giả thuyết (hypothesis class) chỉ có hữu hạn ứng viên (candidate), cần bao nhiêu quan sát để $L_S$ nằm gần $L_D$, trước hết cho một giả thuyết chọn trước, sau đó cho giả thuyết chọn theo chính mẫu đó? Chúng ta dùng hai công cụ: bất đẳng thức tập trung (concentration inequality), cụ thể là bất đẳng thức Hoeffding, và bất đẳng thức hợp (union bound). Từ hai công cụ này ta suy ra cỡ mẫu đủ cho tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM) trên lớp hữu hạn, trong trường hợp bất khả tri (agnostic) và trường hợp khả thực (realizable).

## Câu hỏi mở đầu

Một hàm phân lớp (classifier) sai $5\%$ trên một mẫu xác thực (validation sample) gồm $1000$ quan sát, độc lập với dữ liệu đã dùng để huấn luyện nó.

**Câu hỏi.** Với độ tin cậy $95\%$, rủi ro kì vọng của hàm này có thể lớn đến đâu? Câu trả lời thay đổi thế nào nếu hàm này được chọn trong $1000$ ứng viên vì có tỉ lệ lỗi thấp nhất trên chính mẫu xác thực đó?

Có dùng được cùng một câu trả lời cho hàm được chọn như cho một hàm cố định trước khi xem mẫu không? Không: hàm được chọn vì tỉ lệ lỗi của nó thấp, nên tỉ lệ lỗi đó nghiêng về phía thấp hơn rủi ro kì vọng. Câu trả lời bằng số cho một hàm cố định nằm ở §5, cho một hàm chọn trong $1000$ ứng viên nằm ở §6.

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Phát biểu và chứng minh các bất đẳng thức Markov, Chebyshev và Hoeffding, và chỉ ra bước nào của mỗi chứng minh dùng tính độc lập, bước nào dùng tính bị chặn.
2. Tính và so sánh xác suất đuôi chính xác, cận Chebyshev và cận Hoeffding cho rủi ro thực nghiệm của một giả thuyết cố định; dựng cận tin cậy một phía và khoảng tin cậy hai phía cho rủi ro kì vọng.
3. Chứng minh cận hội tụ đều trên lớp hữu hạn bằng bất đẳng thức hợp, suy ra bảo đảm cho mọi nghiệm ERM, và giải thích vì sao cận cho từng giả thuyết cố định không áp dụng được cho giả thuyết chọn theo mẫu.
4. Tính cỡ mẫu đủ để ước lượng rủi ro, để đạt rủi ro vượt mức nhỏ trong trường hợp bất khả tri và để học trong trường hợp khả thực, và giải thích vì sao chỉ so sánh được các cỡ mẫu cùng loại bảo đảm.
5. Giải thích vì sao, theo các cận của bài, cỡ mẫu đủ trong trường hợp bất khả tri tăng theo bình phương nghịch đảo của độ chính xác, còn cỡ mẫu đủ trong trường hợp khả thực tăng theo nghịch đảo.
6. Dựng phản ví dụ cho thấy kết luận sai khi bỏ tính độc lập của các quan sát, tính bị chặn của hàm lỗi, hoặc hệ số đếm số ứng viên trong bất đẳng thức hợp.

## Kiến thức tiên quyết

- **Từ Bài 01.**
  - Rủi ro kì vọng, rủi ro thực nghiệm và tính không chệch của $L_S(h)$ với $h$ cố định (Định nghĩa 01.1, 01.6, Mệnh đề 01.7).
  - Thuật toán học, thuật toán ERM và $\epsilon_{\mathrm{opt}}$-ERM (Định nghĩa 01.4, 01.8, 01.12); giả thuyết chọn theo mẫu (Nhận xét 01.9).
  - Tính khả thực, hai định nghĩa học PAC, độ tin cậy lấy theo mẫu (Định nghĩa 01.16, 01.18, 01.25, Nhận xét 01.19).
  - Rủi ro Bayes (Bayes risk) và quy tắc Bayes (Định nghĩa 01.22, Mệnh đề 01.23); cận tổng quát hóa cho mọi thuật toán ERM (Định nghĩa 01.28, Hệ quả 01.29).
  - Ví dụ sàng lọc (Ví dụ 01.1, 01.2, 01.5, 01.6, 01.9, 01.10); lớp $\mathcal M_{\mathcal X}$ (Ví dụ 01.8).
- **Xác suất.** Phương sai $\operatorname{Var}V=\mathbb EV^2-(\mathbb EV)^2$; phương sai của tổng các biến độc lập bằng tổng các phương sai; kì vọng của tích các biến độc lập không âm bằng tích các kì vọng. Phân bố Bernoulli (Bernoulli distribution) $\mathrm{Bernoulli}(q)$ nhận giá trị $1$ với xác suất $q$ và $0$ với xác suất $1-q$. Tổng của $m$ biến $\mathrm{Bernoulli}(q)$ độc lập có phân bố nhị thức (binomial distribution) $\mathrm{Bin}(m;q)$: tổng nhận giá trị $k$ với xác suất $\binom mk q^k(1-q)^{m-k}$. Xác suất của hợp hai biến cố rời nhau bằng tổng hai xác suất.
- **Giải tích.** Đồ thị của một hàm lồi trên một đoạn nằm dưới dây cung (chord) nối hai đầu mút; khai triển Taylor với phần dư Lagrange (Taylor expansion with Lagrange remainder, chỉ dùng ở Phụ lục A); $1-x\le e^{-x}$ với mọi $x\in\mathbb R$; bất đẳng thức Bernoulli $(1-x)^m\ge1-mx$ với $x\in[0,1]$ và $m\ge1$.

**Câu hỏi ôn nhanh.**

1. Cho $V\sim\mathrm{Bernoulli}(q)$. Tính $\operatorname{Var}V$ và giá trị lớn nhất của nó khi $q$ chạy trên $[0,1]$.
2. Cho biến ngẫu nhiên $Z_1$ với $\operatorname{Var}Z_1=\sigma^2$ và đặt $Z_2=Z_1$. Tính $\operatorname{Var}\big((Z_1+Z_2)/2\big)$, rồi tính lại khi $Z_1$, $Z_2$ độc lập cùng phân bố.
3. Cho $m\ge1$ và $\epsilon>0$. Tìm $\tau>0$ làm nhỏ nhất biểu thức $-\tau\epsilon+\tau^2/(8m)$.

::: solution Lời giải câu hỏi ôn nhanh
1. Vì $V^2=V$, ta có $\mathbb EV^2=q$, nên $\operatorname{Var}V=q-q^2=q(1-q)$. Giá trị lớn nhất là $\tfrac14$, đạt tại $q=\tfrac12$.
2. Khi $Z_2=Z_1$, $(Z_1+Z_2)/2=Z_1$, nên phương sai bằng $\sigma^2$. Khi hai biến độc lập, phương sai của tổng bằng $2\sigma^2$, nên phương sai của trung bình bằng $2\sigma^2/4=\sigma^2/2$. Kì vọng của trung bình như nhau trong hai trường hợp (câu ôn nhanh 2 của Bài 01), nhưng độ phân tán khác nhau.
3. Đạo hàm theo $\tau$ là $-\epsilon+\tau/(4m)$, bằng $0$ tại $\tau=4m\epsilon$; biểu thức là hàm bậc hai lồi, nên đây là điểm nhỏ nhất. Giá trị nhỏ nhất là $-4m\epsilon^2+16m^2\epsilon^2/(8m)=-2m\epsilon^2$.
:::

## 1. Thiết lập bài toán

Bài toán giữ tám thành phần của §1 Bài 01, với các lựa chọn sau.

1. **Tập quan sát và phân bố dữ liệu.** $\mathcal Z=\mathcal X\times\mathcal Y$ và một phân bố $D$ trên $\mathcal Z$, cố định nhưng chưa biết.
2. **Mẫu.** $S=(Z_1,\ldots,Z_m)\sim D^m$, gồm $m$ quan sát độc lập cùng phân bố (independent and identically distributed, i.i.d.).
3. **Lớp giả thuyết.** $\mathcal H$ hữu hạn, với $K=\lvert\mathcal H\rvert$ phần tử, chọn trước khi lấy mẫu.
4. **Hàm lỗi** (loss function). $\ell$, nhận giá trị trong một đoạn bị chặn, chủ yếu $[0,1]$, như hàm lỗi 0–1 (0–1 loss).
5. **Quy tắc dùng mẫu.** Một giả thuyết $h$ cố định, chỉ được đánh giá trên $S$; một nghiệm $\hat h$ của thuật toán ERM bất kì, với mọi quy tắc chọn khi bằng nhau (tie-breaking rule); hoặc đầu ra của một $\epsilon_{\mathrm{opt}}$-ERM.
6. **Mục tiêu.** Bốn đại lượng cần chặn: $\lvert L_S(h)-L_D(h)\rvert$ với $h$ cố định; cùng đại lượng đó đồng thời cho mọi $h\in\mathcal H$; rủi ro vượt mức (excess risk) $L_D(\hat h)-\min_{h\in\mathcal H}L_D(h)$; rủi ro $L_D(\hat h)$ khi lớp khả thực.
7. **Đối tượng so sánh.** $\min_{h\in\mathcal H}L_D(h)$, mức tốt nhất trong lớp; giá trị nhỏ nhất tồn tại vì $\mathcal H$ hữu hạn.
8. **Tài nguyên.** Cỡ mẫu $m$. Câu trả lời là một cỡ mẫu đủ, viết theo $K$, $\epsilon$, $\delta$ và độ dài miền giá trị của hàm lỗi.

Bảng dưới phân loại các đại lượng của bài theo nguồn ngẫu nhiên.

| Loại | Đại lượng |
|---|---|
| Cố định | $D$, $\mathcal H$, $\ell$, mỗi $h\in\mathcal H$, $L_D(h)$, $\min_{h\in\mathcal H}L_D(h)$, tập $\{h\in\mathcal H:L_D(h)>\epsilon\}$ với $\epsilon$ cho trước |
| Ngẫu nhiên theo $S\sim D^m$ | $S$, $L_S(h)$, $\max_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$, $\hat h$, $L_D(\hat h)$ |

## 2. Kí hiệu và giả thiết

Kí hiệu chung theo bảng kí hiệu của học phần và Bài 01. Bảng dưới gồm các kí hiệu dùng ngay từ §3; mỗi kí hiệu khác được đặt tên tại định nghĩa của nó.

| Kí hiệu | Ý nghĩa |
|---|---|
| $K=\lvert\mathcal H\rvert$ | số giả thuyết của lớp hữu hạn |
| $\ln$ | lôgarit tự nhiên |
| $D_\eta$, $h_t$ | phân bố có nhiễu và các hàm ngưỡng của ví dụ sàng lọc (Ví dụ 01.1) |
| $\ell_{0\text{-}1}$ | hàm lỗi 0–1 |
| $\epsilon$ | độ lệch giữa $L_S(h)$ và $L_D(h)$ ở §4–§6; mức rủi ro vượt mức ở §7; mức rủi ro ở §8; ở các mục khác, nghĩa được nêu khi dùng |

Hai giả thiết thống kê của Bài 01 được dùng lại.

- **(T1) Lấy mẫu.** $Z_1,\ldots,Z_m$ độc lập cùng phân bố theo $D$. Ở dạng yếu, mỗi $Z_i$ có phân bố $D$, không cần độc lập.
- **(T2) Hàm lỗi.** $\ell\ge0$ và $\ell(h,\cdot)$ đo được với mọi $h\in\mathcal H$.

Hai giả thiết mới được nêu ở chỗ dùng lần đầu: (T3) hàm lỗi bị chặn ở §5 và (T4) lớp hữu hạn chọn trước mẫu ở §6. Giả thiết tối ưu (O1) của Bài 01 (thuật toán trả về một nghiệm ERM chính xác) được dùng từ §6; (O2) chỉ dùng ở §7. Giả thiết khả thực chỉ dùng ở §8.

## 3. Ví dụ xuyên suốt

Ví dụ sàng lọc của Bài 01 được dùng lại. Ví dụ dưới nhắc lại bản có nhiễu.

::: example Ví dụ 02.1 (Các đại lượng của ví dụ sàng lọc dùng lại trong bài)
**Thiết lập.** $\mathcal X=\{1,\ldots,5\}$, $\mathcal Y=\{0,1\}$, phân bố biên (marginal distribution) $D_{\mathcal X}$ đều. Lớp $\mathcal H=\{h_t:t=1,\ldots,6\}$ gồm sáu hàm ngưỡng $h_t(x)=\mathbb 1[x\ge t]$, nên $K=6$.

**Bản có nhiễu $D_\eta$.** Xác suất có điều kiện của nhãn 1 là $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$ tại $x=1,\ldots,5$. Dưới hàm lỗi 0–1 (Ví dụ 01.2):

| $t$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ |
|---|---|---|---|---|---|---|
| $L_{D_\eta}(h_t)$ | $0{,}52$ | $0{,}32$ | $\mathbf{0{,}22}$ | $0{,}32$ | $0{,}28$ | $0{,}48$ |

Mức tốt nhất trong lớp là $0{,}22$, đạt tại $h_3$.

**Phân bố của rủi ro thực nghiệm.** Dưới $D_\eta$ và hàm lỗi 0–1, $\ell_{0\text{-}1}(h_3,Z)$ bằng $1$ khi $h_3$ sai trên $Z$, với xác suất $L_{D_\eta}(h_3)=0{,}22$. Do đó
$$
\ell_{0\text{-}1}(h_3,Z)\sim\mathrm{Bernoulli}(0{,}22).
$$
Khi $S\sim D_\eta^m$ theo (T1), $mL_S(h_3)$ là tổng của $m$ biến như vậy, độc lập, nên $mL_S(h_3)\sim\mathrm{Bin}(m;0{,}22)$.
:::

::: application Chọn một hàm phân lớp trong $K$ ứng viên trên một mẫu xác thực
**Ứng viên.** $K$ hàm phân lớp đã được huấn luyện trên một tập dữ liệu khác, chẳng hạn với các siêu tham số khác nhau.

**Mẫu xác thực.** Một mẫu $S$ cỡ $m$, độc lập với dữ liệu huấn luyện. Ta chọn ứng viên có tỉ lệ lỗi nhỏ nhất trên $S$.

**Phép chọn.** Khi lấy điều kiện theo dữ liệu huấn luyện, $K$ ứng viên là một lớp hữu hạn cố định đối với $S$, nên phép chọn là ERM trên lớp này; lập luận chi tiết ở §6.

**Câu hỏi thực hành.** Báo cáo rủi ro kì vọng của hàm được chọn thế nào? Cỡ mẫu xác thực $m$ phải tăng thế nào khi số ứng viên $K$ tăng?
:::

Cả hai câu hỏi thực hành cần một cận cho độ lệch $\lvert L_S(h)-L_D(h)\rvert$, trước hết với một $h$ cố định.

## 4. Xác suất đuôi, bất đẳng thức Markov và Chebyshev

Mệnh đề 01.7 cho $\mathbb E_S[L_S(h)]=L_D(h)$, nhưng trên mẫu $S_\eta$ cỡ $6$ của Ví dụ 01.5, $L_{S_\eta}(h_3)=\tfrac13$ trong khi $L_{D_\eta}(h_3)=0{,}22$. Chúng ta cần chặn xác suất để $L_S(h)$ lệch khỏi $L_D(h)$ ít nhất một lượng cho trước.

::: definition Định nghĩa 02.1 (Xác suất đuôi và cận đuôi)
Cho biến ngẫu nhiên $V$ khả tích và một độ lệch $\epsilon>0$. *Xác suất đuôi* (tail probability) của $V$ tại $\epsilon$ có ba dạng.

- **Đuôi trên.** $\Pr(V-\mathbb EV\ge\epsilon)$.
- **Đuôi dưới.** $\Pr(V-\mathbb EV\le-\epsilon)$.
- **Đuôi hai phía.** $\Pr(\lvert V-\mathbb EV\rvert\ge\epsilon)$.

Một *cận đuôi* (tail bound) là một cận trên của một trong ba xác suất này.
:::

Mọi biến cố đuôi trong bài dùng dấu "$\ge$". Đoạn cầu nối cuối Bài 01 viết biến cố lệch với dấu "$>$"; biến cố đó nằm trong biến cố "$\ge$", nên mọi cận dưới đây cũng chặn nó. Một cận đuôi có ích khi nó nhỏ hơn $1$ và tính được mà không cần biết phân bố của $V$.

Xác suất $\Pr(V\ge\mathbb EV)$ không phải một xác suất đuôi, vì nó không có độ lệch $\epsilon>0$. Với $V=L_S(h_3)$ dưới $D_\eta$ và $m=100$, xác suất này bằng $\Pr\big(\mathrm{Bin}(100;0{,}22)\ge22\big)\approx0{,}539$, không nhỏ dù mẫu đã có $100$ quan sát.

::: example Ví dụ 02.2 (Xác suất đuôi chính xác của rủi ro thực nghiệm của $h_3$)
**Thiết lập.** Phân bố $D_\eta$ của Ví dụ 02.1, hàm lỗi 0–1, giả thuyết $h_3$ cố định, mẫu ngẫu nhiên $S\sim D_\eta^m$ theo (T1), độ lệch $\epsilon=0{,}1$. Đại lượng ngẫu nhiên là $L_S(h_3)$, với kì vọng $0{,}22$ (Mệnh đề 01.7). Cần tính xác suất đuôi hai phía $\Pr\big(\lvert L_S(h_3)-0{,}22\rvert\ge0{,}1\big)$.

**Bước 1: phân bố của $L_S(h_3)$.** Theo Ví dụ 02.1, $L_S(h_3)=k/m$ với $k\sim\mathrm{Bin}(m;0{,}22)$.

**Bước 2: các giá trị lệch xa khi $m=6$.** Ba giá trị nhỏ nhất của $k$ cho độ lệch
$$
\begin{aligned}
k=0:&\quad\lvert0-0{,}22\rvert=0{,}22,\\
k=1:&\quad\lvert\tfrac16-0{,}22\rvert\approx0{,}0533,\\
k=2:&\quad\lvert\tfrac26-0{,}22\rvert\approx0{,}1133.
\end{aligned}
$$
Từ $k=2$ trở đi độ lệch tăng theo $k$, nên điều kiện "độ lệch $\ge0{,}1$" đúng với mọi $k\ne1$.

**Bước 3: xác suất khi $m=6$.** Biến cố đuôi là phần bù của $\{k=1\}$, nên
$$
\begin{aligned}
&\Pr\big(\lvert L_S(h_3)-0{,}22\rvert\ge0{,}1\big)\\
&\quad=1-6\cdot0{,}22\cdot0{,}78^5\\
&\quad\approx1-0{,}3811=0{,}6189.
\end{aligned}
$$
Tức là trên khoảng $62\%$ các mẫu cỡ $6$, tỉ lệ lỗi của $h_3$ lệch khỏi $0{,}22$ ít nhất $0{,}1$.

**Bước 4: $m=100$ và $m=200$.** Biến cố đuôi gồm các $k\le12$ hoặc $k\ge32$ khi $m=100$, và các $k\le24$ hoặc $k\ge64$ khi $m=200$. Cộng các xác suất nhị thức trên các $k$ đó (Phụ lục B.1), ta được
$$
\begin{aligned}
m=100:&\quad\approx0{,}0211,\\
m=200:&\quad\approx8{,}9\cdot10^{-4}.
\end{aligned}
$$

**Bước 5: ý nghĩa.** Với $m=100$, khoảng $2\%$ các mẫu cho tỉ lệ lỗi lệch khỏi $0{,}22$ ít nhất $0{,}1$; với $m=200$, chưa đến $0{,}1\%$ các mẫu.

**Kết luận.** Ta tính được các xác suất này vì đã biết $D_\eta$. Khi $D$ chưa biết, chúng ta cần một cận đuôi không dùng $D$.
:::

Cận đơn giản nhất chỉ dùng kì vọng của một biến không âm. Trong bổ đề dưới, $\alpha$ là một ngưỡng cho chính $V$, không phải độ lệch khỏi kì vọng.

::: lemma Bổ đề 02.2 (Bất đẳng thức Markov) — chứng minh đầy đủ
**Giả thiết.** $V\ge0$ hầu chắc chắn (almost surely), $\mathbb EV<\infty$ và $\alpha>0$. Không cần tính độc lập hay tính bị chặn.

**Bảo đảm.**
$$
\Pr(V\ge\alpha)\le\frac{\mathbb EV}{\alpha}.
$$
Đây là một cận trên của $\Pr(V\ge\alpha)$ chỉ dùng kì vọng, đúng cho mọi biến ngẫu nhiên không âm khả tích.
:::

::: proof Chứng minh Bổ đề 02.2
**Lộ trình.** So sánh hai biến ngẫu nhiên tại từng điểm, rồi lấy kì vọng.

**Bước 1 (bất đẳng thức từng điểm).** Ta có $\alpha\,\mathbb 1[V\ge\alpha]\le V$. Trên biến cố $\{V\ge\alpha\}$, vế trái bằng $\alpha\le V$. Trên biến cố $\{V<\alpha\}$, vế trái bằng $0\le V$; giả thiết $V\ge0$ được dùng ở đây.

**Bước 2 (lấy kì vọng).** Kì vọng bảo toàn thứ tự và $\mathbb E\,\mathbb 1[V\ge\alpha]=\Pr(V\ge\alpha)$, nên $\alpha\Pr(V\ge\alpha)\le\mathbb EV$. Chia hai vế cho $\alpha$; giả thiết $\alpha>0$ được dùng ở đây.

$\square$ Khi chỉ biết kì vọng, cận chỉ giảm như $1/\alpha$; với $V=L_S(h)$, cận không giảm khi $m$ tăng.
:::

Bình phương độ lệch là một biến không âm có kì vọng bằng phương sai. Áp dụng Bổ đề 02.2 cho biến này, ta được một cận hai phía.

::: lemma Bổ đề 02.3 (Bất đẳng thức Chebyshev) — chứng minh đầy đủ
**Giả thiết.** Hai trường hợp.

- **(a) Một biến.** $V$ với $\mathbb EV^2<\infty$, và $\epsilon>0$.
- **(b) Trung bình của $m$ biến.** $V_1,\ldots,V_m$ độc lập, $\operatorname{Var}V_i\le\sigma^2$ với mọi $i$, và $\epsilon>0$. Đặt $\mu_i=\mathbb EV_i$, $\bar V_m=\frac1m\sum_{i=1}^mV_i$ và $\bar\mu_m=\frac1m\sum_{i=1}^m\mu_i$.

**Bảo đảm.** Hai cận đuôi hai phía.

- **(a)** $\Pr(\lvert V-\mathbb EV\rvert\ge\epsilon)\le\operatorname{Var}V/\epsilon^2$.
- **(b)** $\Pr(\lvert\bar V_m-\bar\mu_m\rvert\ge\epsilon)\le\sigma^2/(m\epsilon^2)$, giảm như $1/m$.
:::

::: proof Chứng minh Bổ đề 02.3
**Lộ trình.** Áp dụng bất đẳng thức Markov cho bình phương độ lệch, rồi tính phương sai của trung bình.

**Bước 1 (phần a).** Vì $x\mapsto x^2$ tăng trên $[0,\infty)$, hai biến cố $\{\lvert V-\mathbb EV\rvert\ge\epsilon\}$ và $\{(V-\mathbb EV)^2\ge\epsilon^2\}$ trùng nhau. Biến $(V-\mathbb EV)^2$ không âm, có kì vọng $\operatorname{Var}V$, nên Bổ đề 02.2 với ngưỡng $\alpha=\epsilon^2>0$ cho (a).

**Bước 2 (phần b).** Theo tính độc lập, phương sai của tổng bằng tổng các phương sai, nên
$$
\begin{aligned}
\operatorname{Var}\bar V_m
&=\frac1{m^2}\sum_{i=1}^m\operatorname{Var}V_i\\
&\le\frac{m\sigma^2}{m^2}=\frac{\sigma^2}m.
\end{aligned}
$$
Tính độc lập chỉ được dùng ở đẳng thức đầu; Bài tập 02.1 cho thấy chỉ cần các $V_i$ không tương quan từng đôi (pairwise uncorrelated). Vì $\mathbb E\bar V_m=\bar\mu_m$, phần (a) với $V=\bar V_m$ cho (b).

$\square$ Tính độc lập làm phương sai của trung bình giảm theo $1/m$, nên xác suất để rủi ro thực nghiệm lệch xa khỏi rủi ro kì vọng giảm ít nhất theo $1/m$.
:::

::: example Ví dụ 02.3 (Cận Markov và cận Chebyshev cho rủi ro thực nghiệm của $h_3$)
**Thiết lập.** Như Ví dụ 02.2: phân bố $D_\eta$, hàm lỗi 0–1, $h_3$ cố định, $S\sim D_\eta^m$ theo (T1), độ lệch $\epsilon=0{,}1$, với $m=6$, $100$ và $200$.

**Bước 1: cận Markov cho đuôi trên.** Biến $L_S(h_3)$ không âm, có kì vọng $0{,}22$. Bổ đề 02.2 với ngưỡng $\alpha=0{,}22+0{,}1=0{,}32$ cho
$$
\begin{aligned}
\Pr\big(L_S(h_3)\ge0{,}32\big)&\le\frac{0{,}22}{0{,}32}\\
&=0{,}6875
\end{aligned}
$$
với mọi $m$. Giá trị chính xác, tính bằng tổng nhị thức như Ví dụ 02.2, là $0{,}3937$; $0{,}0134$; $6{,}9\cdot10^{-4}$ ở $m=6$, $100$ và $200$. Cận Markov không giảm khi $m$ tăng.

**Bước 2: phương sai.** Theo câu ôn nhanh 1, $\operatorname{Var}\ell_{0\text{-}1}(h_3,Z)=0{,}22\cdot0{,}78=0{,}1716$. Theo (T1) và Bước 2 của chứng minh Bổ đề 02.3, $\operatorname{Var}L_S(h_3)=0{,}1716/m$.

**Bước 3: cận Chebyshev khi biết phương sai.** Bổ đề 02.3(b) với $\sigma^2=0{,}1716$ và $\epsilon=0{,}1$ cho
$$
\frac{0{,}1716}{m\cdot0{,}01}=\frac{17{,}16}m,
$$
bằng $2{,}86$; $0{,}1716$; $0{,}0858$ ở $m=6$, $100$ và $200$. Ở $m=6$ cận lớn hơn $1$, nên không cho thông tin.

**Bước 4: cận Chebyshev không phụ thuộc phân bố.** Khi không biết $L_D(h)$, ta cần một cận phương sai cho mọi biến $V\in[0,1]$ với kì vọng $\mu$. Vì $V^2\le V$, ta có $\mathbb EV^2\le\mu$, nên
$$
\begin{aligned}
\operatorname{Var}V&\le\mu-\mu^2\\
&=\mu(1-\mu)\le\tfrac14.
\end{aligned}
$$
Bổ đề 02.3(b) với $\sigma^2=\tfrac14$ cho $1/(4m\epsilon^2)=25/m$, bằng $4{,}17$; $0{,}25$; $0{,}125$ ở $m=6$, $100$ và $200$.

**Bước 5: cỡ mẫu.** Cận không phụ thuộc phân bố không vượt quá $\delta$ khi $m\ge1/(4\delta\epsilon^2)$. Với $\epsilon=0{,}1$ và $\delta=0{,}05$,
$$
\frac1{4\cdot0{,}05\cdot0{,}01}=\frac1{0{,}002}=500.
$$
Tức là $500$ quan sát đủ để $L_S(h)$ nằm trong khoảng $0{,}1$ quanh $L_D(h)$ với xác suất ít nhất $0{,}95$, cho mọi hàm lỗi nhận giá trị trong $[0,1]$.

**Kết luận.** Cận Chebyshev đúng mà không cần biết $D$, nhưng nó chỉ giảm như $1/m$, và cỡ mẫu cần tăng như $1/\delta$.
:::

Để cỡ mẫu tăng như $\ln(1/\delta)$ thay vì $1/\delta$, chúng ta cần dùng thêm thông tin về $V$ ngoài phương sai.

## 5. Phương pháp Chernoff và bất đẳng thức Hoeffding

Một biến bị chặn có mọi mô-men hữu hạn, và kì vọng của hàm mũ $e^{\tau V}$ chứa mọi mô-men đó.

::: definition Định nghĩa 02.4 (Hàm sinh mô-men)
Cho biến ngẫu nhiên $V$. *Hàm sinh mô-men* (moment generating function) của $V$ là hàm
$$
\tau\mapsto\mathbb Ee^{\tau V}\in(0,\infty],\qquad\tau\in\mathbb R.
$$
:::

Khi $a\le V\le b$, ta có $e^{\tau V}\le e^{\lvert\tau\rvert\max\{\lvert a\rvert,\lvert b\rvert\}}$, nên hàm sinh mô-men hữu hạn với mọi $\tau$. Chẳng hạn, với $V\sim\mathrm{Bernoulli}(q)$, hàm sinh mô-men là $1-q+qe^{\tau}$.

Khi bỏ tính bị chặn, hàm sinh mô-men có thể bằng $\infty$. Lấy một biến có đuôi nặng (heavy tail): $V$ nhận giá trị $j=1,2,\ldots$ với xác suất tỉ lệ với $1/j^3$. Khi đó $\mathbb EV<\infty$ vì $\sum_jj/j^3<\infty$. Tuy nhiên, với mọi $\tau>0$ các số hạng $e^{\tau j}/j^3$ tiến tới $\infty$, nên $\mathbb Ee^{\tau V}=\infty$.

::: lemma Bổ đề 02.5 (Phương pháp Chernoff) — chứng minh đầy đủ
**Giả thiết.** Hai phần.

- **(a) Một biến.** $V$ là một biến ngẫu nhiên bất kì và $\alpha\in\mathbb R$.
- **(b) Tổng độc lập.** $V=\sum_{i=1}^mV_i$ với $V_1,\ldots,V_m$ độc lập.

**Bảo đảm.** Hai khẳng định tất định về xác suất và kì vọng.

- **(a)** Với mọi $\tau>0$, $\Pr(V\ge\alpha)\le e^{-\tau\alpha}\,\mathbb Ee^{\tau V}$; do đó $\Pr(V\ge\alpha)\le\inf_{\tau>0}e^{-\tau\alpha}\,\mathbb Ee^{\tau V}$.
- **(b)** Với mọi $\tau\in\mathbb R$, $\mathbb Ee^{\tau V}=\prod_{i=1}^m\mathbb Ee^{\tau V_i}$.
:::

::: proof Chứng minh Bổ đề 02.5
**Lộ trình.** Áp dụng bất đẳng thức Markov cho hàm mũ, rồi tách kì vọng của tích bằng tính độc lập.

**Bước 1 (phần a).** Với $\tau>0$, hàm $x\mapsto e^{\tau x}$ tăng ngặt, nên $\{V\ge\alpha\}=\{e^{\tau V}\ge e^{\tau\alpha}\}$. Nếu $\mathbb Ee^{\tau V}=\infty$, bất đẳng thức đúng tầm thường. Nếu không, biến $e^{\tau V}$ không âm, khả tích, và $e^{\tau\alpha}>0$, nên Bổ đề 02.2 cho $\Pr(V\ge\alpha)\le e^{-\tau\alpha}\,\mathbb Ee^{\tau V}$. Bất đẳng thức đúng với mọi $\tau>0$, nên đúng cho cận dưới đúng (infimum) theo $\tau$.

**Bước 2 (phần b).** Ta có $e^{\tau V}=\prod_ie^{\tau V_i}$. Các biến $e^{\tau V_i}$ không âm và độc lập vì các $V_i$ độc lập, nên kì vọng của tích bằng tích các kì vọng. Tính độc lập chỉ được dùng ở đây.

$\square$ Phương pháp Chernoff có ba bước: bất đẳng thức Markov cho hàm mũ, tách theo tính độc lập, chọn $\tau$ tốt nhất. Để áp dụng nó cho rủi ro thực nghiệm, chúng ta còn cần chặn $\mathbb Ee^{\tau V_i}$ cho một biến bị chặn.
:::

::: lemma Bổ đề 02.6 (Bổ đề Hoeffding) — phác thảo
**Giả thiết.** $a\le V\le b$ hầu chắc chắn, với $a<b$. Không cần $\mathbb EV=0$.

**Bảo đảm.** Với mọi $\tau\in\mathbb R$,
$$
\mathbb Ee^{\tau(V-\mathbb EV)}\le\exp\Big(\frac{\tau^2(b-a)^2}8\Big).
$$
Đây là một bất đẳng thức tất định về một kì vọng; vế phải chỉ phụ thuộc độ dài $b-a$ của miền giá trị.
:::

::: proof Chứng minh Bổ đề 02.6 (phác thảo)
**Lộ trình.** Đưa về biến có kì vọng $0$, chặn hàm mũ bằng dây cung, rồi chặn một hàm của một biến thực.

**Bước 1 (kì vọng bằng 0).** Đặt $W=V-\mathbb EV$, $a'=a-\mathbb EV$ và $b'=b-\mathbb EV$. Khi đó $a'\le W\le b'$, $\mathbb EW=0$ và $b'-a'=b-a>0$. Vì $a\le\mathbb EV\le b$, ta có $a'\le0\le b'$.

**Bước 2 (dây cung).** Hàm $w\mapsto e^{\tau w}$ lồi, nên trên đoạn $[a',b']$ đồ thị của nó nằm dưới dây cung. Mọi giá trị của $W$ nằm trong đoạn này; tính bị chặn được dùng ở đây:
$$
\begin{aligned}
e^{\tau w}&\le\frac{b'-w}{b'-a'}\,e^{\tau a'}\\
&\quad+\frac{w-a'}{b'-a'}\,e^{\tau b'}.
\end{aligned}
$$
Thay $w=W$, lấy kì vọng và dùng $\mathbb EW=0$, ta được
$$
\mathbb Ee^{\tau W}\le\frac{b'e^{\tau a'}-a'e^{\tau b'}}{b'-a'}.
$$

**Bước 3 (đổi biến).** Đặt $\theta=-a'/(b'-a')\in[0,1]$ và $u=\tau(b-a)$. Khi đó $1-\theta=b'/(b'-a')$, $\tau a'=-\theta u$ và $\tau b'=\tau a'+u=(1-\theta)u$. Vế phải ở Bước 2 bằng
$$
\begin{aligned}
&(1-\theta)e^{-\theta u}+\theta e^{(1-\theta)u}\\
&\quad=e^{-\theta u}\big(1-\theta+\theta e^{u}\big)\\
&\quad=e^{\varphi(u)},
\end{aligned}
$$
trong đó $\varphi(u)=-\theta u+\ln(1-\theta+\theta e^u)$.

**Bước 4 (bất đẳng thức một biến).** Theo Phụ lục A, $\varphi(u)\le u^2/8$ với mọi $u\in\mathbb R$. Thay $u=\tau(b-a)$ được bảo đảm.

$\square$ Sau khi trừ kì vọng, hàm sinh mô-men của một biến bị chặn không vượt quá $e^{\tau^2(b-a)^2/8}$, bất kể phân bố của biến đó.
:::

Ghép hai bổ đề cuối, ta được cận đuôi chính của bài.

::: theorem Định lý 02.7 (Bất đẳng thức Hoeffding) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Biến ngẫu nhiên.** $V_1,\ldots,V_m$ độc lập, không cần cùng phân bố, với $\mu_i=\mathbb EV_i$, $\bar V_m=\frac1m\sum_{i=1}^mV_i$ và $\bar\mu_m=\frac1m\sum_{i=1}^m\mu_i$.
- **Miền giá trị.** $a\le V_i\le b$ hầu chắc chắn với mọi $i$, trong đó $a<b$.
- **Độ lệch.** $\epsilon>0$.

**Bảo đảm.** Ba cận đuôi.

- **(a) Đuôi trên.** $\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\le\exp\!\big(-2m\epsilon^2/(b-a)^2\big)$.
- **(b) Đuôi dưới.** $\Pr(\bar V_m-\bar\mu_m\le-\epsilon)\le\exp\!\big(-2m\epsilon^2/(b-a)^2\big)$.
- **(c) Hai phía.** $\Pr(\lvert\bar V_m-\bar\mu_m\rvert\ge\epsilon)\le2\exp\!\big(-2m\epsilon^2/(b-a)^2\big)$.

Đây là các cận với xác suất cao cho trung bình thực nghiệm quanh trung bình tổng thể. Chúng giảm theo hàm mũ của $m\epsilon^2$ và chỉ phụ thuộc phân bố qua độ dài $b-a$.
:::

::: proof Chứng minh Định lý 02.7
**Lộ trình.** Áp dụng phương pháp Chernoff cho $\bar V_m-\bar\mu_m$, tách theo tính độc lập, chặn từng thừa số bằng bổ đề Hoeffding, rồi chọn $\tau$.

**Bước 1 (phần a, với $\tau>0$ cố định).** Ta viết $\bar V_m-\bar\mu_m=\sum_{i=1}^m(V_i-\mu_i)/m$, một tổng của $m$ biến độc lập. Khi đó
$$
\begin{aligned}
&\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\\
&\le e^{-\tau\epsilon}\,\mathbb Ee^{\tau(\bar V_m-\bar\mu_m)}\\
&=e^{-\tau\epsilon}\prod_{i=1}^m\mathbb Ee^{(\tau/m)(V_i-\mu_i)}\\
&\le e^{-\tau\epsilon}\prod_{i=1}^me^{\tau^2(b-a)^2/(8m^2)}\\
&=\exp\Big(-\tau\epsilon+\frac{\tau^2(b-a)^2}{8m}\Big).
\end{aligned}
$$
Bất đẳng thức thứ nhất là Bổ đề 02.5(a) cho biến $\bar V_m-\bar\mu_m$ với mức $\alpha=\epsilon$. Đẳng thức tiếp theo là Bổ đề 02.5(b) cho $m$ biến độc lập $(V_i-\mu_i)/m$; tính độc lập được dùng ở đây. Bất đẳng thức thứ hai là Bổ đề 02.6 cho $V_i\in[a,b]$ với tham số $\tau/m$, tức $\mathbb Ee^{(\tau/m)(V_i-\mu_i)}\le e^{(\tau/m)^2(b-a)^2/8}$; tính bị chặn được dùng ở đây.

**Bước 2 (chọn $\tau$).** Số mũ là một hàm bậc hai lồi của $\tau$. Như câu ôn nhanh 3, với $(b-a)^2$ nhân thêm vào số hạng bậc hai, nó nhỏ nhất tại $\tau=4m\epsilon/(b-a)^2$. Thay giá trị này vào hai số hạng của số mũ, ta được
$$
\begin{aligned}
-\tau\epsilon&=-\frac{4m\epsilon^2}{(b-a)^2},\\
\frac{\tau^2(b-a)^2}{8m}&=\frac{2m\epsilon^2}{(b-a)^2},
\end{aligned}
$$
nên số mũ bằng $-2m\epsilon^2/(b-a)^2$. Thay vào Bước 1 được (a).

**Bước 3 (phần b).** Các biến $-V_1,\ldots,-V_m$ độc lập và nhận giá trị trong $[-b,-a]$, một đoạn cũng có độ dài $b-a$. Biến cố $\{\bar V_m-\bar\mu_m\le-\epsilon\}$ là biến cố đuôi trên của trung bình các biến $-V_i$, nên phần (a) cho chúng cho (b).

**Bước 4 (phần c).** Vì $\epsilon>0$, hai biến cố của (a) và (b) rời nhau, và hợp của chúng là biến cố của (c). Xác suất của hợp hai biến cố rời nhau bằng tổng hai xác suất, nên (c) là tổng hai cận. Không bước nào dùng tính cùng phân bố.

$\square$ Cận hai phía không vượt quá $\delta$ khi $m\ge(b-a)^2\ln(2/\delta)/(2\epsilon^2)$: cỡ mẫu tăng như $\ln(2/\delta)$, không như $1/\delta$ của bất đẳng thức Chebyshev.
:::

::: remark Nhận xét 02.8 (Các biến có miền giá trị khác nhau)
Khi $a_i\le V_i\le b_i$ với các đoạn khác nhau, chứng minh của Định lý 02.7 cho
$$
\begin{aligned}
&\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\\
&\quad\le\exp\Big(-\frac{2m^2\epsilon^2}{\sum_{i=1}^m(b_i-a_i)^2}\Big).
\end{aligned}
$$
Khi mọi $b_i-a_i$ bằng $b-a$, cận trở về Định lý 02.7(a) (Bài tập 02.2).
:::

Để áp dụng Định lý 02.7 cho rủi ro thực nghiệm, ta cần thêm một giả thiết về hàm lỗi.

- **(T3) Hàm lỗi bị chặn.** $0\le\ell(h,z)\le1$ với mọi $h\in\mathcal H$ và $z\in\mathcal Z$.

Hàm lỗi 0–1 thỏa (T3). Hàm lỗi có trọng số $\ell_c$ của ứng dụng sàng lọc ở Bài 01, với $(c_{FP},c_{FN})=(1,4)$, nhận giá trị trong $\{0,1,4\}\subset[0,4]$ nên không thỏa (T3). Định lý 02.7 vẫn áp dụng được cho hàm lỗi nhận giá trị trong một đoạn $[a,b]$. Khi đó các cỡ mẫu dựng từ Định lý 02.7 ở §5–§7 nhân thêm $(b-a)^2$, bằng $16$ với $\ell_c$, và các bán kính nhân thêm $b-a$ (Bài tập 02.11). §8 chỉ xét hàm lỗi 0–1.

Để báo cáo rủi ro kì vọng của một hàm cố định, chúng ta cần một khoảng tính được từ mẫu và chứa $L_D(h)$ với xác suất cao, cho mọi phân bố.

::: definition Định nghĩa 02.9 (Cận tin cậy và khoảng tin cậy)
Cho hàm lỗi $\ell$ thỏa (T3), một giả thuyết $h$ cố định, cỡ mẫu $m\ge1$ và $\delta\in(0,1)$.

- **Cận trên tin cậy.** Một hàm đo được $\overline L_\delta:\mathcal Z^m\to\mathbb R$ là *cận trên tin cậy* (upper confidence bound) mức $1-\delta$ cho $L_D(h)$ nếu với mọi phân bố $D$ trên $\mathcal Z$,
  $$
  \begin{aligned}
  &\Pr_{S\sim D^m}\big[L_D(h)\\
  &\qquad\le\overline L_\delta(S)\big]\ge1-\delta.
  \end{aligned}
  $$
- **Khoảng tin cậy.** Một cặp hàm đo được $(\underline L_\delta,\overline L_\delta)$ là *khoảng tin cậy* (confidence interval) mức $1-\delta$ cho $L_D(h)$ nếu với mọi $D$,
  $$
  \begin{aligned}
  &\Pr_{S\sim D^m}\big[\underline L_\delta(S)\le L_D(h)\\
  &\qquad\le\overline L_\delta(S)\big]\ge1-\delta.
  \end{aligned}
  $$

Cận dưới tin cậy được định nghĩa tương tự. Cận trên tin cậy là một *cận một phía* (one-sided bound), khoảng tin cậy là một *cận hai phía* (two-sided bound).
:::

Hai đầu mút là hàm của $S$, nên ngẫu nhiên; $L_D(h)$ cố định. Lượng từ "với mọi $D$" đứng sau hàm: hàm được chọn trước và không biết $D$, như thứ tự lượng từ của Định nghĩa 01.18. Xác suất $1-\delta$ lấy theo các lần lấy mẫu lặp lại, không phải xác suất hậu nghiệm (posterior probability; Nhận xét 01.19).

Hàm hằng $\overline L_\delta\equiv1$ là cận trên tin cậy ở mọi mức, vì $L_D(h)\le1$ theo (T3), nhưng nó không cho thông tin. Ngược lại, $\overline L(S)=L_S(h)$ không phải cận trên tin cậy mức $0{,}95$: dưới $D_\eta$ với $m=100$, biến cố $L_{D_\eta}(h_3)\le L_S(h_3)$ có xác suất $\Pr\big(L_S(h_3)\ge0{,}22\big)\approx0{,}539<0{,}95$.

::: corollary Hệ quả 02.10 (Cận tin cậy Hoeffding cho một giả thuyết cố định) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau.

- **Mẫu.** $S=(Z_1,\ldots,Z_m)\sim D^m$ theo (T1), $m\ge1$.
- **Hàm lỗi.** $\ell$ thỏa (T2) và (T3).
- **Giả thuyết.** $h\in\mathcal H$ cố định, không phụ thuộc $S$.
- **Tham số.** $\delta\in(0,1)$.

**Bảo đảm.** Bốn khẳng định, xác suất lấy theo $S\sim D^m$.

- **(a) Cận đuôi.** Với mọi $\epsilon>0$, $\Pr\big(\lvert L_S(h)-L_D(h)\rvert\ge\epsilon\big)\le2e^{-2m\epsilon^2}$.
- **(b) Khoảng tin cậy.** $L_S(h)\pm\sqrt{\ln(2/\delta)/(2m)}$ là khoảng tin cậy mức $1-\delta$ cho $L_D(h)$.
- **(c) Cận trên tin cậy.** $L_S(h)+\sqrt{\ln(1/\delta)/(2m)}$ là cận trên tin cậy mức $1-\delta$ cho $L_D(h)$.
- **(d) Cỡ mẫu.** Nếu $m\ge\ln(2/\delta)/(2\epsilon^2)$, thì với xác suất ít nhất $1-\delta$, $\lvert L_S(h)-L_D(h)\rvert\le\epsilon$.

Đây là các bảo đảm với xác suất cao; chúng so một đại lượng thực nghiệm với một đại lượng tổng thể và không phụ thuộc $D$.
:::

::: proof Chứng minh Hệ quả 02.10
**Lộ trình.** Áp dụng Định lý 02.7 cho giá trị của hàm lỗi trên từng quan sát, rồi giải phương trình "cận bằng $\delta$".

**Bước 1 (các biến của định lý).** Đặt $V_i=\ell(h,Z_i)$. Vì $h$ cố định, mỗi $V_i$ chỉ phụ thuộc $Z_i$; giả thiết $h$ không phụ thuộc $S$ được dùng ở đây, như ở Bước 1 của chứng minh Mệnh đề 01.7. Theo (T1), các $V_i$ độc lập và $\mu_i=L_D(h)$ với mọi $i$. Theo (T3), $V_i\in[0,1]$. Khi đó $\bar V_m=L_S(h)$ và $\bar\mu_m=L_D(h)$.

**Bước 2 (phần a).** Định lý 02.7(c) với $a=0$, $b=1$.

**Bước 3 (phần b).** Đặt $r=\sqrt{\ln(2/\delta)/(2m)}$, nghiệm dương của $2e^{-2mr^2}=\delta$. Theo (a), biến cố $\{\lvert L_S(h)-L_D(h)\rvert\ge r\}$ có xác suất không quá $\delta$, nên biến cố bù $\{\lvert L_S(h)-L_D(h)\rvert<r\}$ có xác suất ít nhất $1-\delta$. Biến cố bù nằm trong $\{L_S(h)-r\le L_D(h)\le L_S(h)+r\}$. Ta gọi $r$ là *bán kính tin cậy* (confidence radius) hai phía.

**Bước 4 (phần c).** Đặt $r^{+}=\sqrt{\ln(1/\delta)/(2m)}$, nghiệm dương của $e^{-2m(r^{+})^2}=\delta$. Định lý 02.7(b) cho $\Pr\big(L_S(h)-L_D(h)\le-r^{+}\big)\le\delta$, và biến cố bù nằm trong $\{L_D(h)\le L_S(h)+r^{+}\}$. Số $r^{+}$ là bán kính tin cậy một phía.

**Bước 5 (phần d).** Điều kiện $m\ge\ln(2/\delta)/(2\epsilon^2)$ tương đương với $r\le\epsilon$. Trên biến cố của Bước 3, $\lvert L_S(h)-L_D(h)\rvert<r\le\epsilon$.

$\square$ Bán kính của khoảng tin cậy giảm như $1/\sqrt m$; đổi sang cận một phía chỉ đổi $\ln(2/\delta)$ thành $\ln(1/\delta)$.
:::

::: example Ví dụ 02.4 (Ba cách chặn cùng một xác suất đuôi)
**Thiết lập.** Như Ví dụ 02.2: phân bố $D_\eta$, hàm lỗi 0–1, $h_3$ cố định, $S\sim D_\eta^m$ theo (T1), độ lệch $\epsilon=0{,}1$, với $m=100$ và $m=200$.

**Bước 1: cận Hoeffding.** Hệ quả 02.10(a) với $\epsilon=0{,}1$ cho $2e^{-2m\cdot0{,}01}=2e^{-0{,}02m}$, tức
$$
\begin{aligned}
m=100:&\quad2e^{-2}\approx0{,}2707,\\
m=200:&\quad2e^{-4}\approx0{,}0366.
\end{aligned}
$$

**Bước 2: bảng so sánh.** Đặt cạnh giá trị chính xác (Ví dụ 02.2) và hai cận Chebyshev (Ví dụ 02.3):

| Xác suất đuôi tại $0{,}1$ | $m=100$ | $m=200$ |
|---|---|---|
| Giá trị chính xác | $0{,}0211$ | $8{,}9\cdot10^{-4}$ |
| Chebyshev, biết phương sai | $0{,}1716$ | $0{,}0858$ |
| Chebyshev, không phụ thuộc phân bố | $0{,}25$ | $0{,}125$ |
| Hoeffding | $0{,}2707$ | $0{,}0366$ |

**Bước 3: đọc bảng.** Ở $m=100$, cả hai cận Chebyshev nhỏ hơn cận Hoeffding; ở $m=200$, cận Hoeffding nhỏ nhất. Với $\epsilon=0{,}1$, cận Chebyshev không phụ thuộc phân bố $25/m$ nhỏ hơn cận Hoeffding $2e^{-0{,}02m}$ chỉ khi $m\le107$, lúc cả hai cận còn trên khoảng $0{,}23$ (tại $m=107$: $0{,}2336<0{,}2353$; tại $m=108$: $0{,}2315>0{,}2307$). Mọi cận đều lớn hơn giá trị chính xác nhiều lần; ở $m=100$, cận Hoeffding gấp khoảng $13$ lần.

**Bước 4: cỡ mẫu theo $\delta$.** Giữ $\epsilon=0{,}1$, nên $4\epsilon^2=0{,}04$ và $2\epsilon^2=0{,}02$. Theo Bước 5 của Ví dụ 02.3, cận Chebyshev không phụ thuộc phân bố đủ khi $m\ge1/(4\delta\epsilon^2)$. Theo Hệ quả 02.10(d), cận Hoeffding đủ khi $m\ge\ln(2/\delta)/(2\epsilon^2)$. Thay số cho hai mức $\delta$:

- **$\delta=0{,}05$, Chebyshev.** $1/(0{,}05\cdot0{,}04)=500$.
- **$\delta=0{,}05$, Hoeffding.** $\ln40\approx3{,}6889$; $3{,}6889/0{,}02\approx184{,}4$; làm tròn lên được $185$.
- **$\delta=0{,}001$, Chebyshev.** $1/(0{,}001\cdot0{,}04)=25\,000$.
- **$\delta=0{,}001$, Hoeffding.** $\ln2000\approx7{,}6009$; $7{,}6009/0{,}02\approx380{,}05$; làm tròn lên được $381$.

Giảm $\delta$ đi $50$ lần làm cỡ mẫu đủ theo Chebyshev tăng $50$ lần, theo Hoeffding khoảng $2$ lần.

**Kết luận.** Cỡ mẫu đủ theo Hoeffding tăng như $\ln(1/\delta)$, theo Chebyshev như $1/\delta$; ở §6, $\delta$ được chia cho số ứng viên.
:::

::: example Ví dụ 02.5 (Khoảng tin cậy cho một hàm phân lớp cố định có tỉ lệ lỗi 5%)
**Thiết lập.** Ứng dụng ở §3 với một hàm phân lớp $h$ cố định trước khi xem mẫu xác thực $S$; hàm lỗi 0–1; $m=1000$; tỉ lệ lỗi quan sát được $L_S(h)=0{,}05$; $\delta=0{,}05$. Đây là phần thứ nhất của câu hỏi mở đầu.

**Bước 1: lôgarit.** $\ln(2/0{,}05)=\ln40\approx3{,}6889$.

**Bước 2: bán kính hai phía.** Theo Hệ quả 02.10(b),
$$
\begin{aligned}
\sqrt{\frac{\ln40}{2\cdot1000}}&=\sqrt{\frac{3{,}6889}{2000}}\\
&\approx0{,}0429.
\end{aligned}
$$

**Bước 3: khoảng tin cậy.** Khoảng là $[0{,}05-0{,}0429;\ 0{,}05+0{,}0429]\approx[0{,}007;\ 0{,}093]$.

**Bước 4: cận một phía.** Theo Hệ quả 02.10(c), với $\ln(1/0{,}05)=\ln20\approx2{,}9957$,
$$
\begin{aligned}
&0{,}05+\sqrt{\frac{2{,}9957}{2000}}\\
&\quad\approx0{,}05+0{,}0387=0{,}0887.
\end{aligned}
$$

**Bước 5: ý nghĩa.** Với độ tin cậy $95\%$, theo nghĩa của Nhận xét 01.19, rủi ro kì vọng của hàm cố định không quá khoảng $8{,}9\%$.

**Kết luận.** Cận một phía $8{,}9\%$ chặt hơn đầu mút $9{,}3\%$ của khoảng hai phía. Phần thứ hai của câu hỏi mở đầu cần một cận cho hàm được chọn theo $S$.
:::

Hệ quả 02.10 dùng (T1) ở Bước 1 qua tính độc lập của các $V_i$. Trong ví dụ sau, ta bỏ tính độc lập và giữ các giả thiết còn lại.

::: example Ví dụ 02.6 (Một quan sát chép lại $m$ lần)
**Thiết lập.** Lấy $Z\sim D_\eta$ và đặt $Z_1=\cdots=Z_m=Z$: một quan sát được chép lại $m$ lần. Mỗi $Z_i$ vẫn có phân bố $D_\eta$, nên dạng yếu của (T1) thỏa, nhưng các $Z_i$ không độc lập. Giả thuyết $h_3$, hàm lỗi 0–1.

**Bước 1: rủi ro thực nghiệm.** Mọi số hạng trong $L_S(h_3)$ bằng nhau, nên $L_S(h_3)=\ell_{0\text{-}1}(h_3,Z)\in\{0,1\}$.

**Bước 2: kì vọng.** Mệnh đề 01.7 chỉ cần dạng yếu của (T1), nên $\mathbb EL_S(h_3)=0{,}22$, như câu ôn nhanh 2 của Bài 01.

**Bước 3: độ lệch.** Vì $L_S(h_3)\in\{0,1\}$, ta có $\lvert L_S(h_3)-0{,}22\rvert\ge0{,}22$ chắc chắn, với mọi $m$. Do đó xác suất đuôi hai phía bằng $1$ tại mọi độ lệch $\epsilon\le0{,}22$; ta lấy $\epsilon=0{,}2$.

**Bước 4: áp dụng sai Định lý 02.7.** Nếu bỏ qua tính độc lập, Hệ quả 02.10(a) với $\epsilon=0{,}2$ và $m=100$ cho
$$
2e^{-2\cdot100\cdot0{,}04}=2e^{-8}\approx6{,}7\cdot10^{-4},
$$
mâu thuẫn với xác suất $1$ ở Bước 3.

**Bước 5: chỗ hỏng.** Bổ đề 02.5(b) không áp dụng được: $\mathbb Ee^{\tau\sum_i\ell(h_3,Z_i)}=\mathbb Ee^{\tau m\,\ell(h_3,Z)}$, nói chung khác tích $\big(\mathbb Ee^{\tau\ell(h_3,Z)}\big)^m$.

**Kết luận.** Khi các quan sát không độc lập, $L_S(h_3)$ vẫn có kì vọng $0{,}22$ nhưng không tập trung quanh kì vọng khi $m$ tăng, nên Định lý 02.7 cần giả thiết độc lập.
:::

::: remark Nhận xét 02.11 (Hàm lỗi không bị chặn)
Định lý 02.7 dùng tính bị chặn qua Bổ đề 02.6. Xét $V_1,\ldots,V_m$ độc lập cùng phân bố, nhận giá trị $M$ với xác suất $1/M$ và $0$ trong trường hợp còn lại, nên $\mathbb EV_i=1$; lấy $M=m^2$. Theo bất đẳng thức Bernoulli,
$$
\begin{aligned}
\Pr(\bar V_m=0)&=\Big(1-\frac1{m^2}\Big)^m\\
&\ge1-\frac1m.
\end{aligned}
$$
Khi $m=100$, cận dưới này bằng $1-1/100=0{,}99$ (giá trị đúng $\approx0{,}9900$). Trên biến cố $\{\bar V_m=0\}$, $\lvert\bar V_m-1\rvert=1$.

Định lý 02.7 với miền $[0,M]$ và $\epsilon=1$ cho cận $2e^{-2/m^3}\approx2$, nên không có mâu thuẫn. Tuy nhiên, với mỗi $m$, phân bố trên cho $\Pr(\lvert\bar V_m-1\rvert\ge\epsilon)\ge1-1/m$ với mọi $\epsilon\in(0,1]$. Vì vậy không có hàm $g(m,\epsilon)$ tiến về $0$ khi $m\to\infty$ mà chặn xác suất đuôi này đồng thời cho mọi phân bố không âm có kì vọng $1$. Với từng phân bố cố định, luật số lớn (law of large numbers) vẫn đúng.

Hàm lỗi bình phương (squared loss) với một nhãn hiếm có giá trị rất lớn, hay hàm lỗi log (log loss) khi hàm dự đoán gán xác suất rất nhỏ cho nhãn đúng, tạo ra đúng tình huống này; Bài 06 xét chúng với giả thiết khác.
:::

Bỏ tính độc lập (Ví dụ 02.6), cận của Định lý 02.7 sai. Bỏ tính bị chặn (Nhận xét 02.11), không còn cận đuôi nào chỉ phụ thuộc $m$ và $\epsilon$, tiến về $0$ khi $m\to\infty$ và đúng cho mọi phân bố. Phần còn lại của bài giữ cả hai giả thiết.

## 6. Bất đẳng thức hợp và hội tụ đều trên lớp hữu hạn

Hệ quả 02.10 chặn $\lvert L_S(h)-L_D(h)\rvert$ cho một $h$ chọn trước khi lấy mẫu. Thuật toán ERM chọn $\hat h$ sau khi thấy $S$, nên chúng ta cần một cận đúng đồng thời cho mọi $h\in\mathcal H$. Trước hết, ta tính chính xác xác suất để một ứng viên cố định, và để ứng viên được chọn, có tỉ lệ lỗi thấp hơn rủi ro kì vọng một khoảng cho trước.

::: example Ví dụ 02.7 (Thiên lệch do chọn trong 1000 ứng viên)
**Thiết lập.** Ta dựng một bài toán tính được chính xác. Lấy $K=1000$, $\mathcal X=\{0,1\}^K$ và nhãn $Y=0$ chắc chắn. Các tọa độ của $X$ độc lập, mỗi tọa độ bằng $1$ với xác suất $0{,}07$. Ứng viên thứ $j$ là $g_j(x)=x_j$, tọa độ thứ $j$ của $x$. Hàm lỗi 0–1, mẫu xác thực $S\sim D^m$ với $m=1000$. Theo (T1) và cách dựng, $mK$ tọa độ của các quan sát trong $S$ độc lập.

**Rủi ro kì vọng.** Ứng viên $g_j$ sai khi và chỉ khi tọa độ thứ $j$ bằng $1$, nên $L_D(g_j)=0{,}07$ với mọi $j$. Cấu trúc độc lập này chỉ dựng ra để tính chính xác, không mô tả các mô hình thực.

**Bước 1: một ứng viên cố định.** Theo (T1), $1000\,L_S(g_j)\sim\mathrm{Bin}(1000;0{,}07)$, nên (Phụ lục B.2)
$$
\begin{aligned}
&\Pr\big(L_S(g_j)\le0{,}05\big)\\
&=\Pr\big(\mathrm{Bin}(1000;0{,}07)\le50\big)\\
&\approx0{,}00593.
\end{aligned}
$$
Một ứng viên cố định có tỉ lệ lỗi $5\%$ trở xuống với xác suất khoảng $0{,}6\%$.

**Bước 2: ứng viên tốt nhất trên mẫu.** Tỉ lệ lỗi $L_S(g_j)$ chỉ phụ thuộc tọa độ thứ $j$ của các quan sát, và các tọa độ khác nhau độc lập, nên $K$ tỉ lệ lỗi độc lập. Do đó
$$
\begin{aligned}
&\Pr\big(\min_jL_S(g_j)\le0{,}05\big)\\
&\quad=1-(1-0{,}00593)^{1000}\\
&\quad\approx1-0{,}0026=0{,}9974.
\end{aligned}
$$

**Bước 3: ý nghĩa.** Ứng viên có tỉ lệ lỗi nhỏ nhất trên mẫu có tỉ lệ lỗi $5\%$ trở xuống với xác suất khoảng $99{,}7\%$, dù rủi ro kì vọng của nó là $7\%$.

**Kết luận.** Tỉ lệ lỗi của ứng viên được chọn lệch xuống so với rủi ro kì vọng; hiện tượng này gọi là *thiên lệch do chọn* (selection bias). Xác suất của một biến cố tính cho $h$ cố định không chuyển sang $\hat h$.
:::

Để có một cận đồng thời, chúng ta cần chặn xác suất để ít nhất một trong $K$ biến cố xấu xảy ra.

::: lemma Bổ đề 02.12 (Bất đẳng thức hợp) — chứng minh đầy đủ
**Giả thiết.** $B_1,\ldots,B_K$ là các biến cố bất kì trên cùng một không gian xác suất; không cần độc lập, không cần rời nhau.

**Bảo đảm.**
$$
\Pr\Big(\bigcup_{k=1}^KB_k\Big)\le\sum_{k=1}^K\Pr(B_k).
$$
:::

::: proof Chứng minh Bổ đề 02.12
**Lộ trình.** Chứng minh cho hai biến cố, rồi quy nạp theo $K$.

**Bước 1 (hai biến cố).** Với hai biến cố $E$, $F$, ta có $E\cup F=E\cup(F\setminus E)$, hợp của hai biến cố rời nhau. Vì $F\setminus E\subseteq F$,
$$
\begin{aligned}
&\Pr(E\cup F)\\
&\quad=\Pr(E)+\Pr(F\setminus E)\\
&\quad\le\Pr(E)+\Pr(F).
\end{aligned}
$$

**Bước 2 (quy nạp).** Áp dụng Bước 1 cho $E=\bigcup_{k<K}B_k$ và $F=B_K$, rồi dùng giả thiết quy nạp cho $E$.

$\square$ Bất đẳng thức hợp không cần biết các biến cố phụ thuộc nhau thế nào. Nó gần chặt khi các biến cố gần rời nhau và lỏng khi chúng chồng lên nhau.
:::

Với một dãy đếm được $B_1,B_2,\ldots$, ta áp dụng bổ đề cho $K$ biến cố đầu rồi cho $K\to\infty$; tính liên tục của xác suất cho $\Pr(\bigcup_kB_k)\le\sum_k\Pr(B_k)$. Bài tập 02.6 dùng dạng này.

Biến cố cần có xác suất cao là biến cố mọi giả thuyết của lớp có rủi ro thực nghiệm gần rủi ro kì vọng.

::: definition Định nghĩa 02.13 (Mẫu $\epsilon$-đại diện)
Cho lớp $\mathcal H$, hàm lỗi $\ell$, phân bố $D$ và $\epsilon>0$. Một mẫu $s\in\mathcal Z^m$ được gọi là *$\epsilon$-đại diện* ($\epsilon$-representative) đối với $(\mathcal H,\ell,D)$ nếu $\lvert L_s(h)-L_D(h)\rvert\le\epsilon$ với mọi $h\in\mathcal H$, trong đó $L_s(h)$ là rủi ro thực nghiệm trên mẫu cố định $s$ (Định nghĩa 01.6). Với $S\sim D^m$, biến cố "$S$ là $\epsilon$-đại diện" được gọi là *biến cố hội tụ đều* (uniform convergence event).
:::

Tính đại diện phụ thuộc $D$ chưa biết, nên không kiểm tra được từ $s$. Với $\mathcal H$ hữu hạn, biến cố hội tụ đều là giao của $K$ biến cố đo được, nên đo được. Trên mẫu $S_\eta$ của Ví dụ 01.5, các hiệu $L_{S_\eta}(h_t)-L_{D_\eta}(h_t)$ với $t=1,\ldots,6$ (Ví dụ 01.5 trừ Ví dụ 01.2) lần lượt là $-0{,}02$; $0{,}0133$; $0{,}1133$; $0{,}18$; $0{,}0533$; $0{,}02$. Do đó $S_\eta$ là $\epsilon$-đại diện khi và chỉ khi $\epsilon\ge0{,}18$; nó không là $0{,}1$-đại diện, vì $h_3$ và $h_4$ lệch hơn $0{,}1$.

Để có cận đồng thời, ta cần một lớp cố định đối với mẫu.

- **(T4) Lớp hữu hạn chọn trước mẫu.** $\mathcal H$ hữu hạn, $K=\lvert\mathcal H\rvert\ge1$, được chọn trước và không phụ thuộc $S$.

::: theorem Định lý 02.14 (Hội tụ đều trên lớp hữu hạn) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau.

- **Mẫu.** $S\sim D^m$ theo (T1), $m\ge1$.
- **Hàm lỗi.** $\ell$ thỏa (T2) và (T3).
- **Lớp.** $\mathcal H$ thỏa (T4).
- **Tham số.** $\delta\in(0,1)$.

**Bảo đảm.** Đặt hai bán kính tin cậy
$$
\begin{aligned}
r_m&=\sqrt{\frac{\ln(2K/\delta)}{2m}},\\
r_m^{+}&=\sqrt{\frac{\ln(K/\delta)}{2m}},
\end{aligned}
$$
phụ thuộc ngầm vào $K$ và $\delta$. Xác suất lấy theo $S\sim D^m$.

- **(a) Hai phía.** Với xác suất ít nhất $1-\delta$, $S$ là $r_m$-đại diện, tức $\lvert L_S(h)-L_D(h)\rvert\le r_m$ đồng thời cho mọi $h\in\mathcal H$.
- **(b) Một phía.** Với xác suất ít nhất $1-\delta$, $L_D(h)\le L_S(h)+r_m^{+}$ đồng thời cho mọi $h\in\mathcal H$.
- **(c) Cỡ mẫu.** Với $\epsilon>0$, nếu $m\ge\ln(2K/\delta)/(2\epsilon^2)$ thì $S$ là $\epsilon$-đại diện với xác suất ít nhất $1-\delta$.

Bảo đảm đúng đồng thời cho mọi $h$, phụ thuộc $K$ qua $\ln K$ và không phụ thuộc $D$. Với $K=1$, $r_m$ và $r_m^{+}$ trở về các bán kính $r$, $r^{+}$ của Hệ quả 02.10, và (a), (b) trở về Hệ quả 02.10(b), (c).
:::

::: proof Chứng minh Định lý 02.14
**Lộ trình.** Viết biến cố hỏng thành hợp các biến cố hỏng của từng giả thuyết, chặn từng biến cố bằng bất đẳng thức Hoeffding, rồi cộng lại bằng bất đẳng thức hợp.

**Bước 1 (biến cố hỏng).** Với $r>0$ và $h\in\mathcal H$, đặt $B_h=\{\lvert L_S(h)-L_D(h)\rvert\ge r\}$. Nếu $S$ không là $r$-đại diện thì có một $h$ với $\lvert L_S(h)-L_D(h)\rvert>r$, nên
$$
\begin{aligned}
&\{\exists h\in\mathcal H:\\
&\quad\lvert L_S(h)-L_D(h)\rvert>r\}\\
&\quad\subseteq\bigcup_{h\in\mathcal H}B_h.
\end{aligned}
$$

**Bước 2 (từng giả thuyết).** Theo (T4), mỗi $h\in\mathcal H$ cố định đối với $S$, nên Hệ quả 02.10(a) áp dụng được và $\Pr(B_h)\le2e^{-2mr^2}$. Giả thiết (T4) được dùng ở đây; (T1) và (T3) đi vào qua Hệ quả 02.10.

**Bước 3 (bất đẳng thức hợp).** Áp dụng Bổ đề 02.12 cho $K$ biến cố $B_h$, ta được
$$
\begin{aligned}
\Pr\Big(\bigcup_{h\in\mathcal H}B_h\Big)
&\le\sum_{h\in\mathcal H}\Pr(B_h)\\
&\le2Ke^{-2mr^2}.
\end{aligned}
$$
Giả thiết (T4) được dùng lần nữa: tổng có $K$ số hạng. Bước này không dùng tính độc lập giữa các $B_h$; chúng được tính trên cùng một mẫu và nói chung phụ thuộc mạnh.

**Bước 4 (phần a).** Với $r=r_m$, ta có $2Ke^{-2mr_m^2}=\delta$. Biến cố bù của hợp có xác suất ít nhất $1-\delta$ và nằm trong biến cố "$S$ là $r_m$-đại diện".

**Bước 5 (phần b).** Thay $B_h$ bằng biến cố một phía $\{L_S(h)-L_D(h)\le-r\}$. Định lý 02.7(b), áp dụng như ở Bước 1 của chứng minh Hệ quả 02.10, chặn xác suất của nó bởi $e^{-2mr^2}$. Bất đẳng thức hợp cho $Ke^{-2mr^2}$, bằng $\delta$ khi $r=r_m^{+}$.

**Bước 6 (phần c).** Điều kiện $m\ge\ln(2K/\delta)/(2\epsilon^2)$ tương đương với $r_m\le\epsilon$, và một mẫu $r_m$-đại diện là $\epsilon$-đại diện.

$\square$ Mọi giả thuyết trong $\mathcal H$ chọn theo $S$, bằng bất kì quy tắc nào, đều được hưởng cận này, vì cận đúng cho mọi $h\in\mathcal H$ cùng lúc. Giá của tính đồng thời là thay $\ln(2/\delta)$ bằng $\ln(2K/\delta)=\ln K+\ln(2/\delta)$.
:::

Vì phần (b) đúng đồng thời cho mọi $h\in\mathcal H$, với mọi giả thuyết $\hat h\in\mathcal H$ chọn theo $S$ bằng một quy tắc đo được (Phụ lục C) và mọi $D$, ta có $\Pr_S\big[L_D(\hat h)\le L_S(\hat h)+r_m^{+}\big]\ge1-\delta$. Như vậy $L_S(\hat h)+r_m^{+}$ là một cận trên tin cậy theo nghĩa mở rộng của Định nghĩa 02.9 cho giả thuyết chọn theo mẫu.

::: example Ví dụ 02.8 (Bán kính tin cậy sau khi chọn trong $K$ ứng viên)
**Thiết lập.** Ứng dụng ở §3: $K$ ứng viên, mẫu xác thực cỡ $m=1000$, hàm lỗi 0–1, $\delta=0{,}05$. Hàm được chọn $\hat h$ có $L_S(\hat h)=0{,}05$. Đây là phần thứ hai của câu hỏi mở đầu.

**Bước 1: vì sao định lý áp dụng.** Gọi $T$ là dữ liệu huấn luyện các ứng viên và $E$ là biến cố "$L_D(h)\le L_S(h)+r_m^{+}$ với mọi ứng viên $h$". Khi biết $T$, $K$ ứng viên cố định. Vì $S$ độc lập với $T$, khi biết $T$ mẫu $S$ vẫn có phân bố $D^m$ (Nhận xét 01.9). Do đó (T1) và (T4) thỏa dưới xác suất có điều kiện, và Định lý 02.14(b) cho $\Pr(E\mid T)\ge1-\delta$ với mọi giá trị của $T$. Lấy kì vọng theo $T$, ta được $\Pr(E)=\mathbb E\big[\Pr(E\mid T)\big]\ge1-\delta$.

**Bước 2: $K=1000$.** Bán kính một phía là
$$
\begin{aligned}
\ln(K/\delta)&=\ln20\,000\\
&\approx9{,}9035,\\
r_m^{+}&=\sqrt{9{,}9035/2000}\\
&\approx0{,}0704,
\end{aligned}
$$
nên cận trên là $0{,}05+0{,}0704=0{,}1204$.

**Bước 3: $K=5000$.** Ta có $\ln(5000/0{,}05)=\ln100\,000\approx11{,}5129$ và $r_m^{+}=\sqrt{11{,}5129/2000}\approx0{,}0759$, nên cận trên là $0{,}05+0{,}0759=0{,}1259$.

**Bước 4: so với hàm cố định.** Bán kính một phía tăng từ $0{,}0387$ (Ví dụ 02.5) lên $0{,}0704$ khi chọn trong $1000$ ứng viên; tăng số ứng viên thêm năm lần chỉ thêm khoảng $0{,}005$.

**Bước 5: so với Ví dụ 02.7.** Ở đó, mọi ứng viên có rủi ro kì vọng $0{,}07$, với $K=1000$ và $m=1000$. Vì $L_S\ge0$, ta có $L_D(g_j)-L_S(g_j)\le0{,}07<r_m^{+}\approx0{,}0704$ chắc chắn cho mọi $j$. Biến cố của Định lý 02.14(b) vì vậy xảy ra với xác suất $1$, và thiên lệch do chọn ở Ví dụ 02.7 nằm trong bán kính $r_m^{+}$.

**Kết luận.** Với độ tin cậy $95\%$, rủi ro kì vọng không quá khoảng $8{,}9\%$ cho một hàm cố định và khoảng $12\%$ cho hàm được chọn trong $1000$ ứng viên; đó là câu trả lời cho câu hỏi mở đầu.
:::

::: remark Nhận xét 02.15 (Cận tổng quát hóa cho mọi thuật toán ERM trên lớp hữu hạn)
Với hàm lỗi 0–1 và $\mathcal H$ hữu hạn, $\beta(m,\delta)=r_m^{+}$ là một cận tổng quát hóa cho mọi thuật toán ERM theo Định nghĩa 01.28. Với mọi thuật toán ERM $\hat A$, ta có $\hat A(S)\in\mathcal H$, nên trên biến cố của Định lý 02.14(b), $L_D(\hat A(S))-L_S(\hat A(S))\le r_m^{+}$. Biến cố này không phụ thuộc quy tắc chọn và có xác suất ít nhất $1-\delta$ với mọi $D$. Trái với Hệ quả 01.29, nơi mọi cận như vậy trên lớp $\mathcal M_{\mathcal X}$ gồm mọi hàm phân lớp đo được (Ví dụ 01.8) với $\mathcal X=[0,1]$ đều ít nhất bằng $1$, trên một lớp hữu hạn cận này tiến về $0$ khi $m\to\infty$. Các đại lượng dùng ở đây đo được với lớp hữu hạn (Phụ lục C).
:::

Định lý 02.14 chặn $L_D(\hat h)$ bằng $L_S(\hat h)$ cộng một bán kính tin cậy, nhưng chưa so $L_D(\hat h)$ với mức tốt nhất trong lớp $\min_{h\in\mathcal H}L_D(h)$.

## 7. ERM trên lớp hữu hạn trong trường hợp bất khả tri

Bước còn lại là chuyển cận đồng thời của Định lý 02.14 thành cận cho rủi ro vượt mức của nghiệm ERM. Bước này dùng giả thiết tối ưu của Bài 01: (O1) thuật toán trả về một nghiệm ERM chính xác, hoặc (O2) chỉ trả về một $\epsilon_{\mathrm{opt}}$-ERM.

::: corollary Hệ quả 02.16 (Rủi ro vượt mức của ERM trên lớp hữu hạn) — chứng minh đầy đủ
**Giả thiết.** Năm thành phần sau.

- **Mẫu.** $S\sim D^m$ theo (T1), $m\ge1$.
- **Hàm lỗi.** $\ell$ thỏa (T2) và (T3).
- **Lớp.** $\mathcal H$ thỏa (T4).
- **Thuật toán.** Theo (O1), một thuật toán ERM bất kì trên $\mathcal H$, với mọi quy tắc chọn khi bằng nhau; hoặc theo (O2), một $\epsilon_{\mathrm{opt}}$-ERM $A$.
- **Tham số.** $\delta\in(0,1)$, với $r_m=\sqrt{\ln(2K/\delta)/(2m)}$ như ở Định lý 02.14.

**Bảo đảm.** Xác suất lấy theo $S\sim D^m$.

- **(a) ERM chính xác.** Với xác suất ít nhất $1-\delta$, đồng thời cho mọi nghiệm ERM $\hat h$ trên $S$,
  $$
  \begin{aligned}
  L_D(\hat h)&\le\min_{h\in\mathcal H}L_D(h)\\
  &\quad+2r_m.
  \end{aligned}
  $$
- **(b) ERM xấp xỉ.** Trên cùng biến cố,
  $$
  \begin{aligned}
  L_D(A(S))&\le\min_{h\in\mathcal H}L_D(h)\\
  &\quad+2r_m+\epsilon_{\mathrm{opt}}.
  \end{aligned}
  $$
- **(c) Học PAC bất khả tri.** Mọi thuật toán ERM trên $\mathcal H$ là thuật toán học PAC bất khả tri (Định nghĩa 01.25) với
  $$
  M(\epsilon,\delta)=\Big\lceil\frac{2\ln(2K/\delta)}{\epsilon^2}\Big\rceil;
  $$
  do đó mọi lớp hữu hạn học được PAC bất khả tri.

Đây là bảo đảm với xác suất cao cho rủi ro vượt mức so với lớp, không phụ thuộc $D$. Theo (T3), mọi $D$ có rủi ro hữu hạn trên $\mathcal H$.
:::

Trong phần (c), $\epsilon$ là mức rủi ro vượt mức; độ lệch đồng thời tương ứng là $\epsilon/2$, vì $2r_m\le\epsilon$ khi và chỉ khi $r_m\le\epsilon/2$. Khi độ phức tạp mẫu (sample complexity) của Định nghĩa 01.20 được mở rộng sang trường hợp bất khả tri, phần (c) cho $m_{\mathcal H}(\epsilon,\delta)\le M(\epsilon,\delta)$.

::: proof Chứng minh Hệ quả 02.16
**Lộ trình.** Một bước tất định trên biến cố $r$-đại diện, rồi Định lý 02.14.

**Bước 1 (đối tượng so sánh).** Vì $\mathcal H$ hữu hạn theo (T4), tồn tại $h_{\mathcal H}\in\arg\min_{h\in\mathcal H}L_D(h)$, phần tử tốt nhất trong lớp. Giả thuyết $h_{\mathcal H}$ xác định bởi $D$, không phụ thuộc $S$.

**Bước 2 (bước tất định).** Giả sử $S$ là $r$-đại diện và $\hat h$ là một nghiệm ERM trên $S$. Khi đó
$$
\begin{aligned}
L_D(\hat h)&\le L_S(\hat h)+r\\
&\le L_S(h_{\mathcal H})+r\\
&\le L_D(h_{\mathcal H})+2r.
\end{aligned}
$$
Bất đẳng thức thứ nhất dùng tính đại diện tại $\hat h$. Bất đẳng thức thứ hai dùng (O1): $\hat h$ có rủi ro thực nghiệm nhỏ nhất trên $\mathcal H$. Bất đẳng thức thứ ba dùng tính đại diện tại $h_{\mathcal H}$. Dưới (O2), bất đẳng thức thứ hai thành $L_S(A(S))\le L_S(h_{\mathcal H})+\epsilon_{\mathrm{opt}}$ theo Định nghĩa 01.12, nên vế phải thêm $\epsilon_{\mathrm{opt}}$.

**Bước 3 (phần a, b).** Bước 2 đúng cho mọi nghiệm ERM cùng lúc, trên một biến cố không phụ thuộc thuật toán. Theo Định lý 02.14(a), biến cố "$S$ là $r_m$-đại diện" có xác suất ít nhất $1-\delta$.

**Bước 4 (phần c).** Ta có $2r_m\le\epsilon$ khi và chỉ khi $m\ge2\ln(2K/\delta)/\epsilon^2$. Lấy phần nguyên trên được $M(\epsilon,\delta)\in\mathbb N$. Với mọi $D$ và mọi $m\ge M(\epsilon,\delta)$, phần (a) cho bất đẳng thức của Định nghĩa 01.25.

$\square$ Hệ số $2$ đến từ hai phép so sánh, tại $\hat h$ và tại $h_{\mathcal H}$ (Bài tập 02.3); bảo đảm không phụ thuộc quy tắc chọn khi bằng nhau.
:::

::: example Ví dụ 02.9 (ERM trên lớp hàm ngưỡng dưới $D_\eta$)
**Thiết lập.** Phân bố $D_\eta$, lớp sáu hàm ngưỡng ($K=6$), hàm lỗi 0–1, $\epsilon=0{,}1$, $\delta=0{,}05$. Mức tốt nhất trong lớp là $0{,}22$ (Ví dụ 02.1). Cần cỡ mẫu $M(\epsilon,\delta)$ của Hệ quả 02.16(c).

**Bước 1: lôgarit.** $2K/\delta=12/0{,}05=240$, và $\ln240\approx5{,}4806$.

**Bước 2: thay vào công thức.** Thay $\ln240$ và $\epsilon^2=0{,}01$ vào $2\ln(2K/\delta)/\epsilon^2$:
$$
\frac{2\ln240}{0{,}1^2}=\frac{2\cdot5{,}4806}{0{,}01}\approx1096{,}1.
$$

**Bước 3: làm tròn lên.** $M(0{,}1;0{,}05)=\lceil1096{,}1\rceil=1097$.

**Bước 4: ý nghĩa.** Với ít nhất $1097$ quan sát, mọi nghiệm ERM có $L_{D_\eta}(\hat h)\le0{,}22+0{,}1=0{,}32$ với xác suất ít nhất $0{,}95$, dù thuật toán là $A_{\min}$ hay $A_{\max}$ (chọn ngưỡng nhỏ nhất hay lớn nhất khi bằng nhau, Ví dụ 01.6).

**Bước 5: mẫu cỡ 6.** Ở $m=6$,
$$
\begin{aligned}
r_6=\sqrt{\frac{\ln240}{12}}&\approx\sqrt{0{,}4567}\\
&\approx0{,}676,
\end{aligned}
$$
nên $2r_6\approx1{,}35>1$ và cận không cho thông tin. Vì vậy cận không loại trừ kết quả của Ví dụ 01.6, nơi $A_{\min}$ trả về $h_2$ trên $S_\eta$ với rủi ro vượt mức $0{,}10$.

**Kết luận.** Cỡ mẫu $1097$ đủ cho mọi phân bố trên $\{1,\ldots,5\}\times\{0,1\}$.
:::

Theo lý do (ii) ở §7 của Bài 01, khi $\mathcal X$ hữu hạn, ERM trên $\mathcal M_{\mathcal X}$ đạt rủi ro Bayes cộng $\epsilon$ cho mọi $D$. Hệ quả 02.16 cho khẳng định đó một cỡ mẫu cụ thể.

::: example Ví dụ 02.10 (ERM trên mọi hàm phân lớp của một tập đầu vào hữu hạn)
**Thiết lập.** $\mathcal X$ hữu hạn, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1, phân bố $D$ bất kì. Lớp $\mathcal H=\mathcal M_{\mathcal X}$ là lớp mọi hàm phân lớp đo được $\mathcal X\to\{0,1\}$ (Ví dụ 01.8); với $\mathcal X$ hữu hạn, nó gồm $K=2^{\lvert\mathcal X\rvert}$ hàm.

**Bước 1: đối tượng so sánh.** Theo Định nghĩa 01.22 và Mệnh đề 01.23(a), $h_{\mathrm{Bayes}}\in\mathcal M_{\mathcal X}$, nên $\min_{h\in\mathcal M_{\mathcal X}}L_D(h)=L_D^{\mathrm{Bayes}}$.

**Bước 2: cỡ mẫu tổng quát.** Vì $\ln(2K/\delta)=\lvert\mathcal X\rvert\ln2+\ln(2/\delta)$, Hệ quả 02.16(c) cho: với
$$
m\ge\frac{2\big(\lvert\mathcal X\rvert\ln2+\ln(2/\delta)\big)}{\epsilon^2},
$$
mọi nghiệm ERM có $L_D(\hat h)\le L_D^{\mathrm{Bayes}}+\epsilon$ với xác suất ít nhất $1-\delta$.

**Bước 3: ví dụ sàng lọc.** Với $\lvert\mathcal X\rvert=5$, lớp gồm $2^5=32$ hàm. Với $\epsilon=0{,}1$ và $\delta=0{,}05$,
$$
\begin{aligned}
5\ln2+\ln40&\approx3{,}4657\\
&\quad+3{,}6889\\
&=7{,}1546,\\
\frac{2\cdot7{,}1546}{0{,}01}&\approx1430{,}9,
\end{aligned}
$$
nên $M=\lceil1430{,}9\rceil=1431$.

**Bước 4: ý nghĩa dưới $D_\eta$.** Rủi ro Bayes của $D_\eta$ là $0{,}18$ (Ví dụ 01.10). Với ít nhất $1431$ quan sát, mọi nghiệm ERM trên $\mathcal M_{\mathcal X}$ có $L_{D_\eta}(\hat h)\le0{,}18+0{,}1=0{,}28$ với xác suất ít nhất $0{,}95$.

**Bước 5: phụ thuộc vào $\lvert\mathcal X\rvert$.** Cỡ mẫu tăng tuyến tính theo $\lvert\mathcal X\rvert$, phù hợp với Nhận xét 01.30. Khi $\mathcal X$ vô hạn, cận này không cho gì.

**Kết luận.** Ở $\epsilon=0{,}1$, cỡ mẫu đủ khi đối tượng so sánh là rủi ro Bayes là $1431$, hơn $1097$ của Ví dụ 02.9 là $334$ quan sát.
:::

Các cỡ mẫu $1097$ và $1431$ tỉ lệ với $1/\epsilon^2$: giảm $\epsilon$ một nửa nhân chúng lên khoảng bốn lần.

## 8. Lớp hữu hạn trong trường hợp khả thực

Khi lớp chứa một giả thuyết có rủi ro $0$, nghiệm ERM hầu chắc chắn phân lớp đúng mọi quan sát của mẫu. Chúng ta chỉ cần chặn xác suất để một giả thuyết có rủi ro trên $\epsilon$ cũng phân lớp đúng mọi quan sát của mẫu.

::: proposition Mệnh đề 02.17 (Cỡ mẫu cho lớp hữu hạn trong trường hợp khả thực) — chứng minh đầy đủ
**Giả thiết.** Sáu thành phần sau.

- **Bài toán.** $\mathcal Y=\{0,1\}$, hàm lỗi 0–1.
- **Mẫu.** $S\sim D^m$ theo (T1), $m\ge1$.
- **Lớp.** $\mathcal H$ thỏa (T4).
- **Tính khả thực.** $(D,\mathcal H)$ khả thực (Định nghĩa 01.16); chỉ phần (c) dùng thành phần này.
- **Thuật toán.** Theo (O1), một thuật toán ERM bất kì trên $\mathcal H$, với mọi quy tắc chọn khi bằng nhau; chỉ phần (c) dùng thành phần này.
- **Tham số.** $\epsilon,\delta\in(0,1)$.

**Bảo đảm.** Đặt $\mathcal H_{>\epsilon}=\{h\in\mathcal H:L_D(h)>\epsilon\}$, một tập cố định, xác định bởi $D$ chứ không bởi $S$. Xác suất lấy theo $S\sim D^m$.

- **(a) Một giả thuyết xấu.** Với mỗi $h\in\mathcal H_{>\epsilon}$, $\Pr\big(L_S(h)=0\big)<(1-\epsilon)^m\le e^{-\epsilon m}$.
- **(b) Mọi giả thuyết xấu.** $\Pr\big(\exists h\in\mathcal H_{>\epsilon}:L_S(h)=0\big)\le Ke^{-\epsilon m}$.
- **(c) Nghiệm ERM.** Dưới giả thiết khả thực, với xác suất ít nhất $1-Ke^{-\epsilon m}$, mọi nghiệm ERM $\hat h$ trên $S$ có $L_D(\hat h)\le\epsilon$. Nếu $m\ge\ln(K/\delta)/\epsilon=[\ln K+\ln(1/\delta)]/\epsilon$, xác suất này ít nhất $1-\delta$; do đó mọi thuật toán ERM là thuật toán học PAC (Định nghĩa 01.18) với $M(\epsilon,\delta)=\lceil\ln(K/\delta)/\epsilon\rceil$.

Đây là bảo đảm với xác suất cao cho rủi ro tuyệt đối, với đối tượng so sánh $0$ và một biến cố một phía.
:::

Trong Mệnh đề 02.17, $\epsilon$ là mức rủi ro. Theo Định nghĩa 01.20, phần (c) cho $m_{\mathcal H}(\epsilon,\delta)\le\lceil\ln(K/\delta)/\epsilon\rceil$.

::: proof Chứng minh Mệnh đề 02.17
**Lộ trình.** Tính xác suất để một giả thuyết xấu khớp mẫu, cộng trên các giả thuyết xấu bằng bất đẳng thức hợp, rồi dùng tính khả thực để nghiệm ERM khớp mẫu.

**Bước 1 (phần a).** $L_S(h)=0$ khi và chỉ khi $h(X_i)=Y_i$ với mọi $i$. Mỗi quan sát được $h$ phân lớp đúng với xác suất $1-L_D(h)$, và theo (T1) các quan sát độc lập, nên $\Pr(L_S(h)=0)=(1-L_D(h))^m$. Vì $L_D(h)>\epsilon$ và $1-x\le e^{-x}$, ta có $(1-L_D(h))^m<(1-\epsilon)^m\le e^{-\epsilon m}$. Tính độc lập được dùng ở đây.

**Bước 2 (phần b).** Tập $\mathcal H_{>\epsilon}$ cố định, nên Bước 1 áp dụng cho từng phần tử. Áp dụng Bổ đề 02.12 cho các biến cố $\{L_S(h)=0\}$, $h\in\mathcal H_{>\epsilon}$, với $\lvert\mathcal H_{>\epsilon}\rvert\le K$ theo (T4), ta được (b).

**Bước 3 (phần c).** Dưới giả thiết khả thực, giả thuyết $h^\star$ có rủi ro $0$ của Định nghĩa 01.16 thỏa $L_S(h^\star)=0$ hầu chắc chắn (đoạn sau Định nghĩa 01.16), nên mọi nghiệm ERM có $L_S(\hat h)=0$ hầu chắc chắn. Do đó, trừ một biến cố có xác suất $0$, biến cố "có một nghiệm ERM $\hat h$ với $L_D(\hat h)>\epsilon$" nằm trong biến cố của (b), vì nghiệm đó thuộc $\mathcal H_{>\epsilon}$ và có $L_S(\hat h)=0$. Tính khả thực chỉ được dùng ở bước này.

**Bước 4 (cỡ mẫu).** Ta có $Ke^{-\epsilon m}\le\delta$ khi và chỉ khi $m\ge\ln(K/\delta)/\epsilon$; lấy phần nguyên trên được $M(\epsilon,\delta)$.

$\square$ Bỏ tính khả thực, (a) và (b) vẫn đúng, nhưng nghiệm ERM không còn khớp mẫu; khi đó cần Hệ quả 02.16.
:::

::: example Ví dụ 02.11 (Bốn mức cỡ mẫu cho bản nhãn tất định)
**Thiết lập.** Phân bố $D_f$ của Ví dụ 01.1: $D_{\mathcal X}$ đều trên $\{1,\ldots,5\}$ và nhãn tất định $Y=f(X)$ với $f=h_3$. Với lớp sáu hàm ngưỡng, cặp $(D_f,\mathcal H)$ khả thực và $h^\star=h_3$. Hàm lỗi 0–1, $\epsilon=0{,}1$, $\delta=0{,}05$.

**Bước 1: mọi nghiệm ERM trên mọi lớp $6$ phần tử.** Mệnh đề 02.17(c) với $K=6$:
$$
\begin{aligned}
\ln(6/0{,}05)&=\ln120\approx4{,}7875,\\
4{,}7875/0{,}1&\approx47{,}87,
\end{aligned}
$$
nên $M=\lceil47{,}87\rceil=48$.

**Bước 2: mọi nghiệm ERM trên lớp hàm ngưỡng.** Xét một phân bố khả thực bất kì với $h^\star=h_{t^\star}$. Theo Bước 3 của chứng minh Mệnh đề 02.17, trừ một biến cố có xác suất $0$, có một nghiệm ERM với rủi ro trên $\epsilon$ chỉ khi có một ngưỡng xấu khớp mẫu. Một ngưỡng $t<t^\star$ khớp mẫu khi và chỉ khi mẫu không có quan sát nào tại các mức $t,\ldots,t^\star-1$, một tập lớn dần khi $t$ giảm.

Nếu có ngưỡng xấu bên trái, gọi $t_L$ là ngưỡng lớn nhất nhỏ hơn $t^\star$ có rủi ro trên $\epsilon$. Mọi ngưỡng xấu bên trái khớp mẫu chỉ khi $h_{t_L}$ khớp mẫu, nên hợp các biến cố đó có xác suất nhỏ hơn $(1-\epsilon)^m$ (Mệnh đề 02.17(a)). Tương tự, nếu có ngưỡng xấu bên phải, gọi $t_R$ là ngưỡng nhỏ nhất lớn hơn $t^\star$ có rủi ro trên $\epsilon$; mọi ngưỡng xấu bên phải khớp mẫu chỉ khi $h_{t_R}$ khớp mẫu.

Áp dụng bất đẳng thức hợp cho hai chuỗi, ta được xác suất thất bại nhỏ hơn $2(1-\epsilon)^m\le2e^{-\epsilon m}$, không quá $\delta$ khi
$$
\begin{aligned}
m&\ge\frac{\ln(2/\delta)}{\epsilon}=\frac{\ln40}{0{,}1}\\
&\approx\frac{3{,}6889}{0{,}1}\approx36{,}89,
\end{aligned}
$$
nên $37$ quan sát đủ cho mọi nghiệm ERM và mọi phân bố khả thực.

**Bước 3: riêng $A_{\max}$ trên lớp hàm ngưỡng.** Hầu chắc chắn $h_{t^\star}$ khớp mẫu, nên thuộc tập nghiệm ERM; $A_{\max}$ chọn ngưỡng lớn nhất trong tập đó (Ví dụ 01.6), nên $\hat t\ge t^\star$. Chỉ còn chuỗi bên phải, nên đủ khi $e^{-\epsilon m}\le\delta$, tức
$$
\begin{aligned}
m&\ge\frac{\ln(1/\delta)}{\epsilon}=\frac{\ln20}{0{,}1}\\
&\approx\frac{2{,}9957}{0{,}1}\approx29{,}96.
\end{aligned}
$$
Làm tròn lên được $30$, cỡ mẫu ở §9 của Bài 01 (lập luận của Bài tập 01.9).

**Bước 4: riêng $A_{\max}$ dưới $D_f$.** Theo Ví dụ 01.9, $A_{\max}$ thất bại khi và chỉ khi mẫu không có quan sát nào tại $x=3$, với xác suất $0{,}8^m$. Vì $0{,}8^{13}\approx0{,}0550>0{,}05$ và $0{,}8^{14}\approx0{,}0440\le0{,}05$, nên cỡ mẫu nhỏ nhất là $14$.

**Bước 5: phạm vi của bốn con số.**

- **$48$.** Mọi nghiệm ERM, mọi lớp $6$ phần tử, mọi phân bố khả thực.
- **$37$.** Mọi nghiệm ERM trên lớp hàm ngưỡng, mọi phân bố khả thực.
- **$30$.** Riêng $A_{\max}$ trên lớp hàm ngưỡng, mọi phân bố khả thực.
- **$14$.** Riêng $A_{\max}$ và riêng $D_f$.

**Bước 6: nguồn của các khoảng cách.** Từ $48$ xuống $37$: Mệnh đề 02.17 cộng $K=6$ số hạng $e^{-\epsilon m}$, trong khi các biến cố "ngưỡng xấu khớp mẫu" lồng nhau thành hai chuỗi. Từ $37$ xuống $30$: $A_{\max}$ chỉ lệch về một phía.

**Kết luận.** Với cùng $\epsilon$ và $\delta$, bốn số đều là cỡ mẫu đủ, với phạm vi hẹp dần; mỗi bước xuống dùng thêm cấu trúc của lớp, của thuật toán hoặc của phân bố.
:::

Ba cỡ mẫu của §6–§8 trả lời câu hỏi thực hành thứ hai của ứng dụng ở §3.

::: example Ví dụ 02.12 (Bảng cỡ mẫu cho $K$ ứng viên)
**Thiết lập.** Ứng dụng ở §3 với $\delta=0{,}05$, $K\in\{1,100,1000\}$ và $\epsilon\in\{0{,}05;\ 0{,}1\}$. Ba công thức cỡ mẫu ứng với ba bảo đảm khác nhau, với $\epsilon$ theo ba nghĩa khác nhau, nên các số chỉ so sánh được trong cùng một cột.

- **Ước lượng đồng thời $\pm\epsilon$.** $\lceil\ln(2K/\delta)/(2\epsilon^2)\rceil$, theo Định lý 02.14(c); với $K=1$ là Hệ quả 02.10(d).
- **Rủi ro vượt mức $\le\epsilon$.** $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$, theo Hệ quả 02.16(c).
- **Khả thực, rủi ro $\le\epsilon$.** $\lceil\ln(K/\delta)/\epsilon\rceil$, theo Mệnh đề 02.17(c).

**Bước 1: lôgarit.**

| $K$ | $1$ | $100$ | $1000$ |
|---|---|---|---|
| $\ln(2K/\delta)$ | $3{,}6889$ | $8{,}2940$ | $10{,}5966$ |
| $\ln(K/\delta)$ | $2{,}9957$ | $7{,}6009$ | $9{,}9035$ |

**Bước 2: một ô tính đầy đủ.** Với $K=100$, $\epsilon=0{,}1$ và bảo đảm rủi ro vượt mức,
$$
\begin{aligned}
\frac{2\cdot8{,}2940}{0{,}01}&=1658{,}8,\\
\lceil1658{,}8\rceil&=1659.
\end{aligned}
$$

**Bước 3: bảng.** Mỗi ô ghi cỡ mẫu tại $\epsilon=0{,}05$ / $\epsilon=0{,}1$ (giá trị trước khi làm tròn ở Phụ lục B.3).

| $K$ | ước lượng $\pm\epsilon$ | rủi ro vượt mức $\le\epsilon$ | khả thực |
|---|---|---|---|
| $1$ | $738$ / $185$ | — | — |
| $100$ | $1659$ / $415$ | $6636$ / $1659$ | $153$ / $77$ |
| $1000$ | $2120$ / $530$ | $8478$ / $2120$ | $199$ / $100$ |

Với $K=1$, ERM trả về ứng viên duy nhất, nên rủi ro vượt mức bằng $0$ với mọi $m$, và rủi ro bằng $0$ khi khả thực. Hai công thức vẫn cho số dương vì các cận không dùng điều này; bảng ghi "—".

**Bước 4: nhân $K$ lên $10$ lần.** Lôgarit tăng $\ln10\approx2{,}3026$. Ở $\epsilon=0{,}1$, cỡ mẫu tăng thêm:

- **Cột ước lượng.** $2{,}3026/0{,}02\approx115{,}1$, chẳng hạn $415\to530$.
- **Cột rủi ro vượt mức.** $2\cdot2{,}3026/0{,}01\approx460{,}5$, chẳng hạn $1659\to2120$.
- **Cột khả thực.** $2{,}3026/0{,}1\approx23{,}0$, chẳng hạn $77\to100$.

**Bước 5: so sánh công bằng.** Trong cột ước lượng, hàng $K=1$ ứng với một giả thuyết cố định (Hệ quả 02.10(d)).

Cột rủi ro vượt mức bằng cột ước lượng tại $\epsilon/2$, vì cần hai độ lệch $\epsilon/2$, nên ở các hàng $K=100$ và $K=1000$ nó gấp khoảng $4$ lần cột ước lượng.

Cột khả thực chặn rủi ro tuyệt đối với một biến cố một phía, dưới giả thiết khả thực; số của nó nhỏ hơn vì bảo đảm khác và giả thiết mạnh hơn.

**Kết luận.** Nhân số ứng viên lên $10$ lần chỉ cộng một lượng cố định vào cỡ mẫu đủ.
:::

Hai cột cuối của bảng tăng theo hai tốc độ khác nhau khi $\epsilon$ giảm.

::: remark Nhận xét 02.18 (Hai tốc độ theo độ chính xác)
Trong trường hợp khả thực, với mỗi giả thuyết cố định có rủi ro trên $\epsilon$, biến cố "giả thuyết đó khớp mẫu" có xác suất nhỏ hơn $(1-\epsilon)^m$. Để loại biến cố này, ta không cần ước lượng $L_D(h)$ với độ chính xác $\epsilon$. Trong trường hợp bất khả tri, rủi ro có thể gần $\tfrac12$ và phương sai của $\ell(h,Z)$ tới $\tfrac14$ (Ví dụ 02.3), nên độ lệch chuẩn của $L_S(h)$ cỡ $1/\sqrt m$ và cỡ mẫu tỉ lệ với $1/\epsilon^2$. Bất đẳng thức Bernstein (Bernstein's inequality) dùng cả phương sai. Nó cho tốc độ gần $1/\epsilon$ khi phương sai cỡ $\epsilon$ hoặc nhỏ hơn, và $1/\epsilon^2$ khi phương sai cỡ hằng số (đọc thêm, Phụ lục B.5 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* của Shalev-Shwartz và Ben-David (2014), viết tắt UML). Chúng ta chưa chứng minh tốc độ $1/\epsilon^2$ là cần thiết; một cận dưới phải lập luận cho mọi thuật toán, và Bài 03 phát biểu (không chứng minh) một cận dưới như vậy.
:::

Các cỡ mẫu tổng quát của Định lý 02.14, Hệ quả 02.16 và Mệnh đề 02.17 tăng theo $\ln K$ và dùng (T4): lớp phải hữu hạn và cố định trước mẫu.

## 9. Ý nghĩa, tác động và giới hạn

Ta đã có bốn cỡ mẫu đủ: cho một giả thuyết cố định (Hệ quả 02.10), cho $K$ giả thuyết đồng thời (Định lý 02.14), cho rủi ro vượt mức của ERM (Hệ quả 02.16) và cho trường hợp khả thực (Mệnh đề 02.17); Ví dụ 02.12 đặt chúng cạnh nhau. Với câu hỏi mở đầu, rủi ro kì vọng không quá khoảng $8{,}9\%$ cho một hàm cố định và khoảng $12\%$ cho hàm được chọn trong $1000$ ứng viên.

Định lý 02.14 là bảo đảm cho lớp: nó đúng cho mọi giả thuyết của lớp chọn theo $S$. Hệ quả 02.16 và Mệnh đề 02.17 là bảo đảm cho mọi thuật toán ERM, với mọi quy tắc chọn khi bằng nhau; ở Mệnh đề 01.15, trên lớp vô hạn $\mathcal M_{\mathcal X}$ với $\mathcal X=[0,1]$, quy tắc chọn quyết định rủi ro kì vọng giữa $0$ và $1$.

Theo các cận của bài, với lớp cố định trước mẫu và hàm lỗi bị chặn, cỡ mẫu đủ chỉ tăng thêm một lượng tỉ lệ với $\ln K$, nhờ các cận đuôi mũ (Hoeffding; $(1-\epsilon)^m$ khi khả thực). Nếu dùng cận Chebyshev không phụ thuộc phân bố, mỗi giả thuyết phải có xác suất thất bại $\delta/K$, tức $1/(4m\epsilon^2)\le\delta/K$, hay $m\ge K/(4\delta\epsilon^2)$. Với $K=1000$ và $\epsilon=\delta=0{,}05$, đó là $2\,000\,000$ quan sát, so với $2120$ ở Ví dụ 02.12.

Các cận của bài là bảo thủ, vì chúng phải đúng cho mọi phân bố (Ví dụ 02.4). Bất đẳng thức hợp lỏng khi các giả thuyết giống nhau (Ví dụ 02.11). Các kết quả cũng không chuyển sang hàm lỗi không bị chặn (Nhận xét 02.11).

Lớp phải cố định trước mẫu dùng để đánh giá, theo (T4). Giả sử danh sách ứng viên được lập sau khi xem tỉ lệ lỗi trên $S$, hoặc $S$ được dùng lại để thiết kế ứng viên mới theo tỉ lệ lỗi cũ; cách dùng thứ hai gọi là *dùng lại thích nghi* (adaptive reuse). Khi đó ta có một *lớp phụ thuộc dữ liệu* (data-dependent class), và Bước 2 của chứng minh Định lý 02.14 không còn đúng.

Hai cách sửa đơn giản là lấy một mẫu xác thực mới, hoặc cố định trước một họ đếm được các giả thuyết với trọng số và chia $\delta$ theo trọng số (Bài tập 02.6; Bài 04). Họ đếm được đó phải chứa mọi ứng viên có thể được lập ra sau này.

## 10. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 02](material-viewer.html?doc=materials/lec-02/exercises.md). Sáu bài đầu là bài gốc, năm bài sau chọn từ UML; mỗi dòng ghi mục tiêu học tập mà bài kiểm tra.

1. **Bài tập 02.1** (Markov, Chebyshev và các giả thiết yếu hơn): mục tiêu 1.
2. **Bài tập 02.2** (Bất đẳng thức Hoeffding với miền giá trị khác nhau): mục tiêu 1.
3. **Bài tập 02.3** (Hệ số hai trong bảo đảm của ERM): mục tiêu 3.
4. **Bài tập 02.4** (Phản ví dụ cho bất đẳng thức hợp bỏ hệ số $K$): mục tiêu 6.
5. **Bài tập 02.5** (So sánh cận giải tích với mô phỏng Bernoulli, tùy chọn): mục tiêu 2.
6. **Bài tập 02.6** (Bất đẳng thức hợp có trọng số trên lớp đếm được): mục tiêu 3.
7. **Bài tập 02.7** (Hình chữ nhật song song với trục trong trường hợp khả thực; UML Bài tập 2.3, ý 1–2): mục tiêu 4.
8. **Bài tập 02.8** (Lớp hội Boole; UML Bài tập 3.4): mục tiêu 4, 5.
9. **Bài tập 02.9** (Quan sát độc lập nhưng không cùng phân bố; UML Bài tập 3.5): mục tiêu 1.
10. **Bài tập 02.10** (Kì vọng và xác suất cao; UML Bài tập 4.1): mục tiêu 1.
11. **Bài tập 02.11** (Hàm lỗi có trọng số trong $[0,4]$; UML Bài tập 4.2): mục tiêu 4.

## 11. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Một hàm phân lớp được chọn trong $200$ ứng viên vì có tỉ lệ lỗi nhỏ nhất, $8\%$, trên một mẫu xác thực gồm $2000$ quan sát. Tính một cận trên tin cậy $95\%$ cho rủi ro kì vọng của nó. Cận này đúng cho những hàm nào?

**Câu hỏi phụ.** Bước nào của chứng minh Định lý 02.14 hỏng nếu danh sách $200$ ứng viên được lập sau khi xem tỉ lệ lỗi trên chính mẫu xác thực đó?

::: solution Lời giải câu hỏi cuối buổi
**Câu hỏi chính.** Như Ví dụ 02.8, lấy điều kiện theo dữ liệu huấn luyện thì $200$ ứng viên là một lớp cố định đối với mẫu xác thực, và Định lý 02.14(b) áp dụng với $K=200$, $m=2000$, $\delta=0{,}05$:
$$
\begin{aligned}
\ln(K/\delta)&=\ln4000\\
&\approx8{,}2940,\\
r_m^{+}&=\sqrt{8{,}2940/4000}\\
&\approx0{,}0455.
\end{aligned}
$$
Cận trên là $0{,}08+0{,}0455\approx0{,}126$. Cận đúng đồng thời cho cả $200$ ứng viên, nên đúng cho hàm được chọn, dù hàm đó được chọn theo mẫu.

**Câu hỏi phụ.** Bước 2: Hệ quả 02.10 cần mỗi $h$ cố định đối với $S$. Khi danh sách được lập sau khi xem $S$, giả thiết (T4) không còn thỏa.
:::

Lớp hàm ngưỡng trên $\mathbb R$ và lớp nửa không gian (halfspace) trong $\mathbb R^p$ là vô hạn, nên cận theo $\ln\lvert\mathcal H\rvert$ của Định lý 02.14 không cho gì. Tuy vậy, trong trường hợp khả thực, ta đã có cận cỡ mẫu cho hai lớp vô hạn: lớp hình tròn đồng tâm (Bài tập 01.9) và lớp hình chữ nhật song song với trục (Bài tập 02.7). Câu hỏi cho Bài 03 là: với một lớp vô hạn, đại lượng nào thay cho $\ln\lvert\mathcal H\rvert$?

## 12. Tài liệu đọc

- **Trước buổi học:** UML Phụ lục B.1–B.2 (Markov, Chebyshev); đọc lại §2.3.1 (lớp hữu hạn trong trường hợp khả thực).
- **Sau buổi học:** UML Phụ lục B.3–B.4 (Chernoff, Hoeffding), §§4.1–4.2 (hội tụ đều đủ cho học được; lớp hữu hạn học được PAC bất khả tri); các bài tập UML §2.4, §3.5 và §4.5 đã chọn ở §10.
- **Mở rộng:** UML Phụ lục B.5 (bất đẳng thức Bennett và Bernstein, các cận dùng phương sai).

**Quan hệ với giáo trình UML.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục. Các khác biệt chính:

- **Bất đẳng thức tập trung.** Hoeffding không cần tính cùng phân bố và dùng biến cố "$\ge$"; Markov với $\alpha>0$; Chebyshev cho trung bình của các biến không cùng phân bố.
- **Phương pháp Chernoff.** Phát biểu tổng quát thành một bổ đề; hàm sinh mô-men có tên riêng; bất đẳng thức $\varphi(u)\le u^2/8$ được chứng minh đầy đủ ở Phụ lục A.
- **Trường hợp khả thực.** Viết với phân bố đồng thời $D$ thay cho cặp $(D,f)$ của UML Chương 2.
- **ERM.** Các bảo đảm có thêm dạng ERM xấp xỉ.
- **Hội tụ đều.** Mẫu $\epsilon$-đại diện chỉ dùng như một biến cố; tính chất hội tụ đều của một lớp để Bài 03.

## Phụ lục

### A. Bất đẳng thức một biến của bổ đề Hoeffding

Bước 4 của chứng minh Bổ đề 02.6 cần bất đẳng thức một biến dưới đây. Cho $\theta\in[0,1]$ và, với $u\in\mathbb R$,
$$
\varphi(u)=-\theta u+\ln\big(1-\theta+\theta e^u\big).
$$
Đối số của $\ln$ là một tổ hợp lồi của $1$ và $e^u$, nên ít nhất bằng $\min\{1,e^u\}>0$; do đó $\varphi$ xác định và khả vi vô hạn lần trên $\mathbb R$.

::: proof Chứng minh $\varphi(u)\le u^2/8$ với mọi $u\in\mathbb R$
**Lộ trình.** Tính $\varphi(0)$, $\varphi'(0)$, chặn $\varphi''$, rồi dùng khai triển Taylor với phần dư Lagrange tại $0$.

**Bước 1 (giá trị tại $0$).** $\varphi(0)=0+\ln(1-\theta+\theta)=\ln1=0$.

**Bước 2 (đạo hàm bậc nhất).** Đặt
$$
\rho(u)=\frac{\theta e^u}{1-\theta+\theta e^u}\in[0,1].
$$
Khi đó $\varphi'(u)=-\theta+\rho(u)$, và $\rho(0)=\theta$, nên $\varphi'(0)=0$.

**Bước 3 (đạo hàm bậc hai).** Theo quy tắc đạo hàm của thương,
$$
\begin{aligned}
\rho'(u)&=\frac{\theta e^u(1-\theta)}{(1-\theta+\theta e^u)^2}\\
&=\rho(u)\big(1-\rho(u)\big),
\end{aligned}
$$
vì $1-\rho(u)=(1-\theta)/(1-\theta+\theta e^u)$. Do đó $\varphi''(u)=\rho(u)(1-\rho(u))$, phương sai của một biến Bernoulli với tham số $\rho(u)$, và $\varphi''(u)\le\tfrac14$ theo câu ôn nhanh 1.

**Bước 4 (khai triển Taylor).** Với mỗi $u$, tồn tại $c_u$ nằm giữa $0$ và $u$ sao cho
$$
\begin{aligned}
\varphi(u)&=\varphi(0)+\varphi'(0)\,u\\
&\quad+\tfrac12\varphi''(c_u)\,u^2\\
&=\tfrac12\varphi''(c_u)\,u^2\\
&\le\frac{u^2}8.
\end{aligned}
$$

$\square$ Thay $u=\tau(b-a)$ vào Bước 3 của chứng minh Bổ đề 02.6, ta được $\mathbb Ee^{\tau(V-\mathbb EV)}\le e^{\varphi(u)}\le e^{\tau^2(b-a)^2/8}$.
:::

### B. Tính toán chi tiết cho các ví dụ

**B.1 Xác suất đuôi chính xác của $L_S(h_3)$ (Ví dụ 02.2, 02.3).** Với $k\sim\mathrm{Bin}(m;0{,}22)$, điều kiện $\lvert k/m-0{,}22\rvert\ge0{,}1$ tương đương với $k\le0{,}12m$ hoặc $k\ge0{,}32m$.

- **$m=100$.** $\Pr(k\le12)\approx0{,}00779$ và $\Pr(k\ge32)\approx0{,}01336$, tổng $\approx0{,}02115$.
- **$m=200$.** $\Pr(k\le24)\approx2{,}01\cdot10^{-4}$ và $\Pr(k\ge64)\approx6{,}93\cdot10^{-4}$, tổng $\approx8{,}94\cdot10^{-4}$.
- **$m=6$.** Đuôi trên $\Pr(k\ge2)=1-0{,}78^6-6\cdot0{,}22\cdot0{,}78^5\approx1-0{,}2252-0{,}3811=0{,}3937$.

Các số hạng $\Pr(k\ge32)$ ở $m=100$ và $\Pr(k\ge64)$ ở $m=200$ là giá trị chính xác của đuôi trên trong Ví dụ 02.3. Hai giá trị $k/m$ chạm đúng biên ($k=12$, $32$ khi $m=100$; $k=24$, $64$ khi $m=200$). Với biến cố "$>0{,}1$" thay cho "$\ge0{,}1$", các số hạng biên bị loại và hai xác suất hai phía giảm còn $\approx0{,}0109$ và $\approx4{,}9\cdot10^{-4}$; ở $m=6$ hai biến cố trùng nhau.

**B.2 Ví dụ 02.7.** Tổng nhị thức cho $\Pr\big(\mathrm{Bin}(1000;0{,}07)\le50\big)\approx0{,}005930$. Khi đó
$$
\begin{aligned}
(1-0{,}00593)^{1000}&=e^{1000\ln(1-0{,}00593)}\\
&\approx e^{-5{,}947}\approx0{,}0026,
\end{aligned}
$$
nên xác suất để ít nhất một ứng viên có tỉ lệ lỗi $5\%$ trở xuống là $\approx0{,}9974$.

**B.3 Bảng của Ví dụ 02.12.** Giá trị trước khi lấy phần nguyên trên, theo thứ tự $\epsilon=0{,}05$ / $\epsilon=0{,}1$:

| $K$ | ước lượng $\pm\epsilon$ | rủi ro vượt mức $\le\epsilon$ | khả thực |
|---|---|---|---|
| $1$ | $737{,}8$ / $184{,}4$ | — | — |
| $100$ | $1658{,}8$ / $414{,}7$ | $6635{,}2$ / $1658{,}8$ | $152{,}02$ / $76{,}01$ |
| $1000$ | $2119{,}3$ / $529{,}8$ | $8477{,}3$ / $2119{,}3$ | $198{,}1$ / $99{,}03$ |

### C. Tính đo được với lớp hữu hạn

Với lớp hữu hạn, điều kiện đo được nêu ở Phụ lục A(v) của Bài 01 tự thỏa.

- **Độ lệch lớn nhất.** $\max_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$ là giá trị lớn nhất của hữu hạn hàm đo được của $S$, nên đo được.
- **Thuật toán ERM.** Xét một thuật toán ERM chọn khi bằng nhau theo một thứ tự ưu tiên cố định trên $\mathcal H$, như $A_{\min}$ và $A_{\max}$. Thuật toán nhận hữu hạn giá trị. Tập các mẫu $s$ mà nó trả về một $h$ cho trước là một tổ hợp Boole của các tập $\{s:L_s(h)\le L_s(h')\}$ và $\{s:L_s(h)<L_s(h')\}$, $h'\in\mathcal H$, nên đo được. Khi đó $\ell(A_m(s),z)=\sum_{h\in\mathcal H}\mathbb 1[A_m(s)=h]\,\ell(h,z)$ là tổng hữu hạn các tích hàm đo được, nên thuật toán thỏa điều kiện đo được đồng thời của Định nghĩa 01.4, như ở Phụ lục A(iv) của Bài 01. Cùng lập luận đúng cho mọi quy tắc chọn $s\mapsto\hat h(s)\in\mathcal H$ mà mỗi tập $\{s:\hat h(s)=h\}$ đo được.
