# Bài tập Bài 02 — Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn

Các bài tập dưới đây đi kèm ghi chú Bài 02 và dẫn định nghĩa, kết quả, ví dụ theo số hiệu của ghi chú. Kí hiệu theo bảng kí hiệu chung của học phần và §2 của ghi chú: $K=\lvert\mathcal H\rvert$, các giả thiết (T1)–(T4), (O1), (O2), các bán kính tin cậy $r_m$, $r_m^{+}$ của Định lý 02.14; $h_t(x)=\mathbb 1[x\ge t]$ là hàm ngưỡng của ví dụ sàng lọc. Hai chữ viết tắt theo ghi chú: tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM) và học xấp xỉ với xác suất cao (probably approximately correct, PAC). Hàm lỗi là hàm lỗi 0–1 khi không ghi rõ, $\ln$ là lôgarit tự nhiên. Sáu bài đầu là bài gốc của học phần. Năm bài sau chọn từ mục bài tập §2.4, §3.5 và §4.5 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* (Shalev-Shwartz và Ben-David, 2014; viết tắt UML), phát biểu lại theo kí hiệu của học phần.

## Bài tập gốc

### Bài tập 02.1 (Markov, Chebyshev và các giả thiết yếu hơn)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 1; bước nào của mỗi chứng minh dùng tính độc lập.

::: exercise Bài tập 02.1
**(a)** Cho biến ngẫu nhiên $V\ge0$ với $\mathbb EV<\infty$ và một ngưỡng $\alpha>0$. Chứng minh rằng bất đẳng thức Markov (Bổ đề 02.2) xảy ra dấu bằng, tức $\Pr(V\ge\alpha)=\mathbb EV/\alpha$, khi và chỉ khi $V\in\{0,\alpha\}$ hầu chắc chắn. Với mỗi $\mu\in(0,\alpha]$, dựng một biến như vậy có $\mathbb EV=\mu$.

**(b)** Cho $V_1,\ldots,V_m$ có phương sai hữu hạn, $\operatorname{Var}V_i\le\sigma^2$, với $\mu_i=\mathbb EV_i$, $\bar V_m=\frac1m\sum_{i=1}^mV_i$ và $\bar\mu_m=\frac1m\sum_{i=1}^m\mu_i$. Giả sử các biến *không tương quan từng đôi* (pairwise uncorrelated): *hiệp phương sai* (covariance) $\operatorname{Cov}(V_i,V_j)=\mathbb E[(V_i-\mu_i)(V_j-\mu_j)]$ bằng $0$ với mọi $i\ne j$. Chứng minh rằng kết luận của Bổ đề 02.3(b) vẫn đúng: với mọi $\epsilon>0$,
$$
\Pr\big(\lvert\bar V_m-\bar\mu_m\rvert\ge\epsilon\big)\le\frac{\sigma^2}{m\epsilon^2}.
$$

**(c)** Cho $V_1$, $V_2$ độc lập, mỗi biến có phân bố $\mathrm{Bernoulli}(\tfrac12)$, và $V_3=V_1\oplus V_2$, trong đó $\oplus$ là phép cộng modulo $2$: $V_3=1$ khi đúng một trong hai biến $V_1$, $V_2$ bằng $1$. Chứng minh rằng ba biến *độc lập từng đôi* (pairwise independent), tức mỗi cặp hai biến độc lập, nhưng ba biến không độc lập. Giải thích vì sao phần (b) áp dụng được cho ba biến này, và tính $\operatorname{Var}\big((V_1+V_2+V_3)/3\big)$.

**(d)** Với ba biến của (c), $\tau\in\mathbb R$ và $x=e^{\tau}$, tính $\mathbb Ee^{\tau(V_1+V_2+V_3)}$ và $\prod_{i=1}^3\mathbb Ee^{\tau V_i}$. Chứng minh rằng tích trừ kì vọng của tổng bằng $(x-1)^3/8$, và so sánh hai giá trị tại $\tau=1$ và $\tau=-1$.

**(e)** Bước 1 của chứng minh Định lý 02.7 chỉ cần bất đẳng thức $\mathbb Ee^{\tau\sum_iV_i}\le\prod_i\mathbb Ee^{\tau V_i}$ với $\tau>0$; phần (b) của định lý áp dụng bước đó cho các biến $-V_i$. Dùng (d) để xác định phần nào của Định lý 02.7 còn đúng cho ba biến của (c), và tính $\Pr(\bar V_3-\tfrac12\le-\tfrac12)$ để so với cận $e^{-2m\epsilon^2}$ tại $m=3$, $\epsilon=\tfrac12$.

**(f)** Lấy $\epsilon=\delta=0{,}05$ và các biến $V_i$ nhận giá trị trong $[0,1]$. Tính cỡ mẫu đủ để $\Pr(\lvert\bar V_m-\bar\mu_m\rvert\ge\epsilon)\le\delta$ theo cận Chebyshev không phụ thuộc phân bố (Bổ đề 02.3(b) với $\sigma^2=\tfrac14$, Ví dụ 02.3) và theo bất đẳng thức Hoeffding (Định lý 02.7(c)). Nếu các $V_i$ chỉ độc lập từng đôi, cỡ mẫu nào trong hai cỡ mẫu này vẫn được Bổ đề 02.3 hoặc Định lý 02.7 bảo đảm?
:::

::: hint Gợi ý 1
Phần (a). Bước 1 của chứng minh Bổ đề 02.2 cho biến $V-\alpha\,\mathbb 1[V\ge\alpha]$ không âm. Phần (c). Liệt kê bốn giá trị đồng khả năng của cặp $(V_1,V_2)$ cùng giá trị của $V_3$.
:::

::: hint Gợi ý 2
Phần (a). Một biến không âm có kì vọng $0$ thì bằng $0$ hầu chắc chắn. Phần (b). Khai triển $\operatorname{Var}\big(\sum_iV_i\big)=\mathbb E\big(\sum_i(V_i-\mu_i)\big)^2$ thành tổng các phương sai và các hiệp phương sai.
:::

::: hint Gợi ý 3
Phần (d). Tổng $V_1+V_2+V_3$ chỉ nhận hai giá trị $0$ và $2$; khai triển $(1+x)^3$. Phần (e). Dấu của $(x-1)^3$ đổi tại $\tau=0$. Biến cố $\{\bar V_3\le0\}$ là biến cố tổng bằng $0$.
:::

::: solution Lời giải Bài tập 02.1
**(a) Dấu bằng của bất đẳng thức Markov.**

**Bước 1: hiệu hai vế.** Đặt $W=V-\alpha\,\mathbb 1[V\ge\alpha]$. Theo Bước 1 của chứng minh Bổ đề 02.2, $W\ge0$, và
$$
\mathbb EW=\mathbb EV-\alpha\Pr(V\ge\alpha).
$$
Dấu bằng của bất đẳng thức Markov xảy ra khi và chỉ khi $\mathbb EW=0$.

**Bước 2: khi nào $\mathbb EW=0$.** Một biến không âm có kì vọng $0$ khi và chỉ khi nó bằng $0$ hầu chắc chắn. Trên $\{V\ge\alpha\}$, $W=V-\alpha$, nên $W=0$ nghĩa là $V=\alpha$. Trên $\{V<\alpha\}$, $W=V$, nên $W=0$ nghĩa là $V=0$. Vậy $\mathbb EW=0$ khi và chỉ khi $V\in\{0,\alpha\}$ hầu chắc chắn.

**Bước 3: dựng biến.** Cho $V=\alpha$ với xác suất $\mu/\alpha\in(0,1]$ và $V=0$ trong trường hợp còn lại. Khi đó $\mathbb EV=\mu$ và $\Pr(V\ge\alpha)=\mu/\alpha$. Vậy khi chỉ biết $\mathbb EV=\mu\le\alpha$, không có cận nào nhỏ hơn $\mu/\alpha$ đúng cho mọi biến không âm có kì vọng $\mu$.

**(b) Chỉ cần không tương quan từng đôi.**

**Bước 1: phương sai của tổng.** Đặt $W_i=V_i-\mu_i$. Khai triển bình phương của tổng:
$$
\begin{aligned}
&\operatorname{Var}\Big(\sum_iV_i\Big)=\mathbb E\Big(\sum_iW_i\Big)^2\\
&=\sum_i\mathbb EW_i^2+\sum_{i\ne j}\mathbb E[W_iW_j]\\
&=\sum_i\operatorname{Var}V_i\\
&\quad+\sum_{i\ne j}\operatorname{Cov}(V_i,V_j).
\end{aligned}
$$

**Bước 2: dùng giả thiết.** Mọi hiệp phương sai bằng $0$, nên $\operatorname{Var}\bar V_m=\frac1{m^2}\sum_i\operatorname{Var}V_i\le\sigma^2/m$.

**Bước 3: kết luận.** Vì $\mathbb E\bar V_m=\bar\mu_m$, áp dụng Bổ đề 02.3(a) cho $\bar V_m$, ta được cận $\sigma^2/(m\epsilon^2)$. Chứng minh của Bổ đề 02.3(b) chỉ dùng tính độc lập để triệt tiêu các hiệp phương sai.

**(c) Độc lập từng đôi nhưng không độc lập.**

**Bước 1: bảng giá trị.** Bốn giá trị của $(V_1,V_2)$ đồng khả năng, mỗi giá trị có xác suất $\tfrac14$:

| $(V_1,V_2)$ | $(0,0)$ | $(0,1)$ | $(1,0)$ | $(1,1)$ |
|---|---|---|---|---|
| $V_3$ | $0$ | $1$ | $1$ | $0$ |
| $V_1+V_2+V_3$ | $0$ | $2$ | $2$ | $2$ |

**Bước 2: từng cặp.** $V_3=1$ ở hai trong bốn trường hợp, nên $V_3\sim\mathrm{Bernoulli}(\tfrac12)$. Cặp $(V_1,V_3)$ nhận bốn giá trị $(0,0)$, $(0,1)$, $(1,1)$, $(1,0)$, mỗi giá trị với xác suất $\tfrac14=\tfrac12\cdot\tfrac12$; vậy $V_1$ và $V_3$ độc lập. Cặp $(V_2,V_3)$ tương tự.

**Bước 3: không độc lập.** $\Pr(V_1=V_2=V_3=1)=0$, trong khi tích ba xác suất biên là $\tfrac18$.

**Bước 4: áp dụng (b).** Độc lập từng đôi kéo theo hiệp phương sai bằng $0$, nên (b) áp dụng được với $\sigma^2=\tfrac14$ (câu ôn nhanh 1), và
$$
\begin{aligned}
\operatorname{Var}\Big(\frac{V_1+V_2+V_3}3\Big)&=\frac{3\cdot\tfrac14}{9}\\
&=\frac1{12}.
\end{aligned}
$$

**(d) Hàm sinh mô-men của tổng.**

**Bước 1: hai vế.** Theo bảng, tổng bằng $0$ với xác suất $\tfrac14$ và bằng $2$ với xác suất $\tfrac34$. Mỗi $V_i$ có $\mathbb Ee^{\tau V_i}=(1+x)/2$. Do đó
$$
\begin{aligned}
\mathbb Ee^{\tau(V_1+V_2+V_3)}&=\frac{1+3x^2}4,\\
\prod_{i=1}^3\mathbb Ee^{\tau V_i}&=\frac{(1+x)^3}8.
\end{aligned}
$$

**Bước 2: hiệu.** Khai triển $(1+x)^3=1+3x+3x^2+x^3$:
$$
\begin{aligned}
&\frac{(1+x)^3}8-\frac{2+6x^2}8\\
&\quad=\frac{x^3-3x^2+3x-1}8\\
&\quad=\frac{(x-1)^3}8.
\end{aligned}
$$

**Bước 3: hai giá trị của $\tau$.** Tại $\tau=1$, kì vọng của tổng $\approx5{,}7918$ nhỏ hơn tích $\approx6{,}4259$. Tại $\tau=-1$, kì vọng của tổng $\approx0{,}3515$ lớn hơn tích $\approx0{,}3199$. Đẳng thức của Bổ đề 02.5(b) sai với mọi $\tau\ne0$; hiệu dương khi $\tau>0$ và âm khi $\tau<0$.

**(e) Phần nào của Định lý 02.7 còn đúng.**

**Bước 1: đuôi trên.** Khi $\tau>0$, $x>1$ và $(x-1)^3>0$, nên kì vọng của tổng không vượt quá tích. Bước 1 của chứng minh Định lý 02.7 chỉ cần bất đẳng thức này, nên Định lý 02.7(a) vẫn đúng cho ba biến này.

**Bước 2: đuôi dưới.** Phần (b) áp dụng Bước 1 cho các biến $-V_i$, tức cần bất đẳng thức với $\tau<0$ cho các $V_i$. Theo (d), bất đẳng thức đó sai.

**Bước 3: vi phạm cụ thể.** Với $m=3$, $\bar\mu_3=\tfrac12$. Biến cố $\bar V_3-\tfrac12\le-\tfrac12$ là biến cố tổng bằng $0$, có xác suất $\tfrac14$. Cận của Định lý 02.7(b) là $e^{-2\cdot3\cdot\frac14}=e^{-1{,}5}\approx0{,}2231<\tfrac14$. Vậy Định lý 02.7(b) sai cho ba biến độc lập từng đôi này.

**(f) Hai cỡ mẫu.**

**Bước 1: Chebyshev.** Cận $1/(4m\epsilon^2)\le\delta$ khi và chỉ khi $m\ge1/(4\delta\epsilon^2)$:
$$
\begin{aligned}
4\delta\epsilon^2&=4\cdot0{,}05\cdot0{,}0025\\
&=0{,}0005,\\
\frac1{0{,}0005}&=2000.
\end{aligned}
$$

**Bước 2: Hoeffding.** Cận $2e^{-2m\epsilon^2}\le\delta$ khi và chỉ khi $m\ge\ln(2/\delta)/(2\epsilon^2)$:
$$
\begin{aligned}
\frac{\ln40}{2\cdot0{,}0025}&\approx\frac{3{,}6889}{0{,}005}\\
&\approx737{,}8,
\end{aligned}
$$
làm tròn lên được $738$.

**Bước 3: khi chỉ có độc lập từng đôi.** Phần (b) vẫn cho cận Chebyshev, nên $2000$ quan sát vẫn đủ. Cận hai phía của Định lý 02.7 cần cả đuôi dưới, và (e) cho thấy đuôi dưới có thể sai. Vậy với các biến chỉ độc lập từng đôi, cỡ mẫu $738$ không còn căn cứ.

**Kiểm tra lại.** Từ bảng, tổng $T$ có $\mathbb ET=\tfrac32$ và $\mathbb ET^2=3$, nên $\operatorname{Var}(T/3)=\tfrac34/9=\tfrac1{12}$, khớp (c).
:::

### Bài tập 02.2 (Bất đẳng thức Hoeffding với miền giá trị khác nhau)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 1, 2; phương pháp Chernoff khi mỗi biến có một miền giá trị riêng, cận tin cậy dựng từ cận đuôi.

::: exercise Bài tập 02.2
Cho $V_1,\ldots,V_m$ độc lập, không cần cùng phân bố, với $a_i\le V_i\le b_i$ hầu chắc chắn và $a_i<b_i$. Đặt $\mu_i=\mathbb EV_i$, $\bar V_m=\frac1m\sum_{i=1}^mV_i$, $\bar\mu_m=\frac1m\sum_{i=1}^m\mu_i$ và
$$
C=\sum_{i=1}^m(b_i-a_i)^2.
$$

**(a)** Chứng minh khẳng định của Nhận xét 02.8: với mọi $\epsilon>0$,
$$
\begin{aligned}
&\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\\
&\quad\le\exp\Big(-\frac{2m^2\epsilon^2}C\Big).
\end{aligned}
$$
Suy ra cận cùng dạng cho đuôi dưới và cận hai phía.

**(b)** Chứng minh rằng khi mọi $b_i-a_i$ bằng $b-a$, cận ở (a) trở về Định lý 02.7(a), và với mọi dãy đoạn, cận ở (a) không lớn hơn cận của Định lý 02.7(a) với đoạn chung $[\min_ia_i,\max_ib_i]$.

**(c)** Lấy $m=1000$ và $\epsilon=0{,}1$; $900$ biến đầu nhận giá trị trong $[0,1]$, $100$ biến sau nhận giá trị trong $[0,4]$. Tính cận đuôi trên theo (a) và theo Định lý 02.7(a) với đoạn chung $[0,4]$.

**(d)** Từ (a), dựng một cận trên tin cậy một phía và một khoảng tin cậy hai phía mức $1-\delta$ cho $\bar\mu_m$, theo nghĩa của Định nghĩa 02.9 với $\bar\mu_m$ thay cho $L_D(h)$. Với dữ liệu của (c) và $\delta=0{,}05$, tính hai bán kính và so với hai bán kính khi dùng đoạn chung $[0,4]$.
:::

::: hint Gợi ý 1
Đi lại các bước của chứng minh Định lý 02.7. Khi áp dụng bổ đề Hoeffding (Bổ đề 02.6), giữ đoạn $[a_i,b_i]$ riêng của từng biến.
:::

::: hint Gợi ý 2
Sau khi tách kì vọng theo tính độc lập (Bổ đề 02.5(b)) và chặn từng thừa số bằng Bổ đề 02.6, số mũ là $-\tau\epsilon+\tau^2C/(8m^2)$. Tìm $\tau>0$ làm nhỏ nhất hàm bậc hai này như câu ôn nhanh 3. Phần (b): $C\le m(b-a)^2$.
:::

::: hint Gợi ý 3
Phần (d). Giải $\exp(-2m^2r^2/C)=\delta$ và $2\exp(-2m^2r^2/C)=\delta$ theo $r$, như Bước 3–4 của chứng minh Hệ quả 02.10.
:::

::: solution Lời giải Bài tập 02.2
**(a) Cận với các miền giá trị khác nhau.**

**Bước 1: phương pháp Chernoff.** Với $\tau>0$ cố định, áp dụng Bổ đề 02.5(a) cho biến $\bar V_m-\bar\mu_m$ với mức $\epsilon$, rồi Bổ đề 02.5(b) cho $m$ biến độc lập $(V_i-\mu_i)/m$:
$$
\begin{aligned}
&\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\\
&\le e^{-\tau\epsilon}\,\mathbb Ee^{\tau(\bar V_m-\bar\mu_m)}\\
&=e^{-\tau\epsilon}\prod_{i=1}^m\mathbb Ee^{(\tau/m)(V_i-\mu_i)}.
\end{aligned}
$$
Tính độc lập được dùng ở đẳng thức.

**Bước 2: bổ đề Hoeffding cho từng biến.** Bổ đề 02.6 với $V_i\in[a_i,b_i]$ và tham số $\tau/m$ chặn thừa số thứ $i$ bởi $\exp\big(\tau^2(b_i-a_i)^2/(8m^2)\big)$. Nhân $m$ thừa số:
$$
\begin{aligned}
&\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\\
&\quad\le\exp\Big(-\tau\epsilon+\frac{\tau^2C}{8m^2}\Big).
\end{aligned}
$$
Tính bị chặn được dùng ở đây.

**Bước 3: chọn $\tau$.** Đạo hàm của số mũ theo $\tau$ là $-\epsilon+\tau C/(4m^2)$, bằng $0$ tại $\tau=4m^2\epsilon/C>0$; số mũ là hàm bậc hai lồi, nên đây là điểm nhỏ nhất. Thay vào hai số hạng:
$$
\begin{aligned}
-\tau\epsilon&=-\frac{4m^2\epsilon^2}C,\\
\frac{\tau^2C}{8m^2}&=\frac{16m^4\epsilon^2}{C^2}\cdot\frac C{8m^2}\\
&=\frac{2m^2\epsilon^2}C.
\end{aligned}
$$
Tổng là $-2m^2\epsilon^2/C$.

**Bước 4: đuôi dưới và hai phía.** Các biến $-V_i$ độc lập, nhận giá trị trong $[-b_i,-a_i]$, cùng $C$. Biến cố $\{\bar V_m-\bar\mu_m\le-\epsilon\}$ là đuôi trên của trung bình các $-V_i$, nên có cùng cận. Hai biến cố đuôi rời nhau, nên cận hai phía là $2\exp(-2m^2\epsilon^2/C)$.

**(b) So sánh với Định lý 02.7.** Khi mọi $b_i-a_i=b-a$, ta có $C=m(b-a)^2$ và $2m^2\epsilon^2/C=2m\epsilon^2/(b-a)^2$, đúng số mũ của Định lý 02.7(a). Với $a=\min_ia_i$, $b=\max_ib_i$, mọi $V_i$ nằm trong $[a,b]$ và $b_i-a_i\le b-a$, nên $C\le m(b-a)^2$ và $2m^2\epsilon^2/C\ge2m\epsilon^2/(b-a)^2$, nên cận ở (a) không lớn hơn cận dùng đoạn chung.

**(c) Một mẫu có hai loại miền giá trị.**

**Bước 1: tính $C$.**
$$
\begin{aligned}
C&=900\cdot1^2+100\cdot4^2\\
&=900+1600=2500.
\end{aligned}
$$

**Bước 2: cận theo (a).** Ta có $2m^2\epsilon^2=2\cdot10^6\cdot0{,}01=20\,000$, nên cận là $\exp(-20\,000/2500)=e^{-8}\approx3{,}4\cdot10^{-4}$.

**Bước 3: cận theo đoạn chung $[0,4]$.** Số mũ là $2\cdot1000\cdot0{,}01/16=1{,}25$, nên cận là $e^{-1{,}25}\approx0{,}287$, lớn hơn khoảng $850$ lần.

**(d) Cận tin cậy.**

**Bước 1: cận một phía.** Đặt $r^{+}=\sqrt{C\ln(1/\delta)/(2m^2)}$, nghiệm dương của $\exp(-2m^2r^2/C)=\delta$. Theo cận đuôi dưới ở (a), $\Pr(\bar V_m-\bar\mu_m\le-r^{+})\le\delta$. Biến cố bù nằm trong $\{\bar\mu_m\le\bar V_m+r^{+}\}$, nên $\bar V_m+r^{+}$ là cận trên tin cậy mức $1-\delta$.

**Bước 2: khoảng hai phía.** Đặt $r=\sqrt{C\ln(2/\delta)/(2m^2)}$, nghiệm dương của $2\exp(-2m^2r^2/C)=\delta$. Theo cận hai phía ở (a), $\bar V_m\pm r$ chứa $\bar\mu_m$ với xác suất ít nhất $1-\delta$. Hai đầu mút ngẫu nhiên qua $\bar V_m$, còn $\bar\mu_m$ cố định.

**Bước 3: thay số.** Với $C=2500$ và $m=1000$, $C/(2m^2)=1{,}25\cdot10^{-3}$:
$$
\begin{aligned}
r^{+}&=\sqrt{1{,}25\cdot10^{-3}\cdot\ln20}\\
&\approx\sqrt{1{,}25\cdot10^{-3}\cdot2{,}9957}\\
&\approx0{,}0612,\\
r&=\sqrt{1{,}25\cdot10^{-3}\cdot\ln40}\\
&\approx\sqrt{1{,}25\cdot10^{-3}\cdot3{,}6889}\\
&\approx0{,}0679.
\end{aligned}
$$

**Bước 4: đoạn chung.** Với đoạn $[0,4]$, $C$ được thay bằng $1000\cdot16=16\,000$ và $C/(2m^2)=8\cdot10^{-3}$, nên $r^{+}\approx0{,}1548$ và $r\approx0{,}1718$. Mỗi bán kính lớn gấp $\sqrt{16\,000/2500}=\sqrt{6{,}4}\approx2{,}53$ lần bán kính dùng $C=2500$.

**Kiểm tra lại.** Nếu cả $1000$ biến nằm trong $[0,1]$ thì $C=1000$ và số mũ ở (c) là $20\,000/1000=20=2\cdot1000\cdot0{,}01$, khớp Định lý 02.7(a). Với $C=m$, bán kính $r^{+}$ ở (d) trở về $\sqrt{\ln(1/\delta)/(2m)}$ của Hệ quả 02.10(c).
:::

### Bài tập 02.3 (Hệ số hai trong bảo đảm của ERM)

**Mức độ:** khái niệm, chứng minh (phần (b) là phần thử thách). **Mục tiêu:** mục tiêu học tập 3; vai trò của từng phép so sánh trong bảo đảm cho nghiệm ERM.

::: exercise Bài tập 02.3
Cho $S\sim D^m$ theo (T1), hàm lỗi $\ell$ thỏa (T2) và (T3), lớp $\mathcal H$ thỏa (T4) với $K\ge1$ phần tử, và $\delta\in(0,1)$. Gọi $h_{\mathcal H}\in\arg\min_{h\in\mathcal H}L_D(h)$ là một phần tử tốt nhất trong lớp, xác định bởi $D$, và $\hat h$ là một nghiệm ERM bất kì trên $S$. Bước 2 của chứng minh Hệ quả 02.16 dùng chuỗi
$$
\begin{aligned}
L_D(\hat h)&\le L_S(\hat h)+r\\
&\le L_S(h_{\mathcal H})+r\\
&\le L_D(h_{\mathcal H})+2r
\end{aligned}
$$
trên biến cố "$S$ là $r$-đại diện" (Định nghĩa 02.13).

**(a)** Với bất đẳng thức thứ nhất và thứ ba, xác định chiều lệch được dùng ($L_D-L_S\le r$ hay $L_S-L_D\le r$) và giả thuyết tại đó nó được dùng. Giải thích vì sao bất đẳng thức thứ nhất cần một cận đúng đồng thời cho mọi $h\in\mathcal H$, còn bất đẳng thức thứ ba chỉ cần một cận cho một giả thuyết cố định.

**(b)** (Thử thách.) Đặt $r'=\sqrt{\ln((K+1)/\delta)/(2m)}$. Chứng minh rằng với xác suất ít nhất $1-\delta$, mọi nghiệm ERM $\hat h$ thỏa $L_D(\hat h)\le\min_{h\in\mathcal H}L_D(h)+2r'$. Suy ra mọi thuật toán ERM là thuật toán học PAC bất khả tri với $M'(\epsilon,\delta)=\lceil2\ln((K+1)/\delta)/\epsilon^2\rceil$, và $M'$ không lớn hơn hàm cỡ mẫu $M(\epsilon,\delta)=\lceil2\ln(2K/\delta)/\epsilon^2\rceil$ của Hệ quả 02.16(c).

**(c)** Với $K=100$, $\delta=0{,}05$ và $\epsilon=0{,}1$, tính $M'(\epsilon,\delta)$ và so với $M(\epsilon,\delta)=1659$ của Ví dụ 02.12.
:::

::: hint Gợi ý 1
Phần (a). Biến cố "$S$ là $r$-đại diện" là giao của hai họ biến cố, $L_D(h)-L_S(h)\le r$ và $L_S(h)-L_D(h)\le r$ với mọi $h\in\mathcal H$. Xét xem mỗi bất đẳng thức trong chuỗi dùng biến cố nào.
:::

::: hint Gợi ý 2
Phần (a). Giả thuyết $\hat h$ phụ thuộc $S$; giả thuyết $h_{\mathcal H}$ chỉ phụ thuộc $D$. So với Ví dụ 02.7.
:::

::: hint Gợi ý 3
Phần (b). Dùng $K$ biến cố một phía $\{L_D(h)-L_S(h)\ge r\}$, $h\in\mathcal H$, và một biến cố $\{L_S(h_{\mathcal H})-L_D(h_{\mathcal H})\ge r\}$. Định lý 02.7 chặn xác suất của mỗi biến cố bởi $e^{-2mr^2}$.
:::

::: solution Lời giải Bài tập 02.3
**(a) Hai phép so sánh.**

**Bất đẳng thức thứ nhất.** $L_D(\hat h)\le L_S(\hat h)+r$ dùng chiều $L_D-L_S\le r$ tại $\hat h$. Giả thuyết $\hat h$ được chọn theo $S$, nên biến cố cần dùng phải đúng cho mọi ứng viên mà $\hat h$ có thể nhận: $\{L_D(h)-L_S(h)\le r\ \ \forall h\in\mathcal H\}$. Ở Ví dụ 02.7, tỉ lệ lỗi $5\%$ trở xuống có xác suất $0{,}6\%$ cho một ứng viên cố định và $99{,}7\%$ cho ứng viên được chọn.

**Bất đẳng thức thứ hai.** $L_S(\hat h)\le L_S(h_{\mathcal H})$ là (O1), không dùng xác suất.

**Bất đẳng thức thứ ba.** $L_S(h_{\mathcal H})\le L_D(h_{\mathcal H})+r$ dùng chiều $L_S-L_D\le r$ tại $h_{\mathcal H}$. Giả thuyết $h_{\mathcal H}$ không phụ thuộc $S$, nên một cận cho một giả thuyết cố định là đủ.

**Đếm biến cố.** Hệ quả 02.16 dùng $2K$ biến cố đuôi. Chuỗi trên chỉ cần $K$ biến cố đuôi một phía và một biến cố đuôi tại $h_{\mathcal H}$. Hệ số $2$ trong $2r$ đến từ hai phép so sánh, không đến từ biến cố hai phía.

**(b) Cận với $K+1$ biến cố.**

**Bước 1: biến cố tốt.** Với $r>0$, đặt
$$
\begin{aligned}
E=\{&L_D(h)-L_S(h)<r\\
&\quad\forall h\in\mathcal H\}\\
\cap\{&L_S(h_{\mathcal H})-L_D(h_{\mathcal H})<r\}.
\end{aligned}
$$

**Bước 2: bước tất định.** Trên $E$, với mọi nghiệm ERM $\hat h$, chuỗi của đề bài cho $L_D(\hat h)<L_D(h_{\mathcal H})+2r$: bất đẳng thức thứ nhất dùng phần đầu của $E$ tại $h=\hat h\in\mathcal H$, bất đẳng thức thứ hai dùng (O1), bất đẳng thức thứ ba dùng phần sau của $E$.

**Bước 3: từng biến cố xấu.** Phần bù của $E$ là hợp của $K+1$ biến cố: $B_h$ với $h\in\mathcal H$ và $B_0$, trong đó
$$
\begin{aligned}
B_h&=\{L_D(h)-L_S(h)\ge r\},\\
B_0&=\{L_S(h_{\mathcal H})-L_D(h_{\mathcal H})\\
&\qquad\ge r\}.
\end{aligned}
$$
Mỗi $h\in\mathcal H$ cố định đối với $S$ theo (T4), và $h_{\mathcal H}$ cố định vì chỉ phụ thuộc $D$. Như ở Bước 1 của chứng minh Hệ quả 02.10, Định lý 02.7(b) cho $\Pr(B_h)\le e^{-2mr^2}$ và Định lý 02.7(a) cho $\Pr(B_0)\le e^{-2mr^2}$.

**Bước 4: bất đẳng thức hợp.** Bổ đề 02.12 cho $\Pr(E^c)\le(K+1)e^{-2mr^2}$, bằng $\delta$ khi $r=r'$. Vậy với xác suất ít nhất $1-\delta$, mọi nghiệm ERM có $L_D(\hat h)\le\min_{h\in\mathcal H}L_D(h)+2r'$.

**Bước 5: cỡ mẫu.** Ta có $2r'\le\epsilon$ khi và chỉ khi $m\ge2\ln((K+1)/\delta)/\epsilon^2$; lấy phần nguyên trên được $M'$. Với $K\ge1$, $K+1\le2K$, nên $M'\le M$; hai hàm bằng nhau khi $K=1$.

**(c) Thay số.**

**Bước 1: lôgarit.**
$$
\begin{aligned}
\ln\frac{K+1}\delta&=\ln2020\approx7{,}6109,\\
\ln\frac{2K}\delta&=\ln4000\approx8{,}2940.
\end{aligned}
$$

**Bước 2: cỡ mẫu.** $2\cdot7{,}6109/0{,}01\approx1522{,}2$, nên $M'(0{,}1;0{,}05)=1523$, ít hơn $1659$ là $136$ quan sát, khoảng $8\%$. Hiệu hai lôgarit là $\ln(2K/(K+1))<\ln2$, nên ở $\epsilon=0{,}1$ phần tiết kiệm không quá $139$ quan sát ($2\ln2/0{,}01\approx138{,}6$), dù $K$ lớn đến đâu.

**Kiểm tra lại.** Với $K=1$, $r'=\sqrt{\ln(2/\delta)/(2m)}$ trùng $r_m$. Với $K=100$ và $m=1523$, $2r'=2\sqrt{7{,}6109/3046}\approx0{,}09997\le0{,}1$.
:::

### Bài tập 02.4 (Phản ví dụ cho bất đẳng thức hợp bỏ hệ số $K$)

**Mức độ:** kiểm tra giả thiết, tính toán. **Mục tiêu:** mục tiêu học tập 6; vai trò của số ứng viên trong cận đồng thời.

::: exercise Bài tập 02.4
Một học viên lập luận như sau: "Với mỗi $h\in\mathcal H$ cố định, Hệ quả 02.10(a) cho $\Pr(\lvert L_S(h)-L_D(h)\rvert\ge\epsilon)\le2e^{-2m\epsilon^2}$. Vì vậy, với xác suất ít nhất $1-2e^{-2m\epsilon^2}$, mọi $h\in\mathcal H$ có $\lvert L_S(h)-L_D(h)\rvert<\epsilon$."

Xét $\mathcal X=\{0,1\}^K$ và $\mathcal Y=\{0,1\}$. Dưới phân bố $D$, các tọa độ $X_1,\ldots,X_K$ của $X$ độc lập, mỗi tọa độ có phân bố $\mathrm{Bernoulli}(\tfrac12)$, và nhãn $Y=0$ chắc chắn. Lớp $\mathcal H=\{h_1,\ldots,h_K\}$ gồm $h_k(x)=x_k$, hàm lỗi 0–1, mẫu $S\sim D^m$ với $m=10$, và $\epsilon=0{,}4$.

**(a)** Tính $L_D(h_k)$ và cận $2e^{-2m\epsilon^2}$ của học viên. Với một $k$ cố định, tính chính xác $\Pr(\lvert L_S(h_k)-L_D(h_k)\rvert\ge\epsilon)$ và so với cận đó.

**(b)** Tính chính xác $\Pr(\exists k:\ L_S(h_k)=0)$ khi $K=1000$ và khi $K=5000$. Kết luận về khẳng định của học viên.

**(c)** Chứng minh rằng kết quả của (b) không mâu thuẫn với Định lý 02.14(a), và chỉ ra bước của chứng minh Định lý 02.14 mà học viên đã bỏ qua.
:::

::: hint Gợi ý 1
Vì $Y=0$, giả thuyết $h_k$ sai trên một quan sát khi và chỉ khi tọa độ thứ $k$ của quan sát đó bằng $1$. Biến cố $L_S(h_k)=0$ nghĩa là cả $m$ quan sát có tọa độ thứ $k$ bằng $0$.
:::

::: hint Gợi ý 2
Tỉ lệ lỗi $L_S(h_k)$ chỉ phụ thuộc tọa độ thứ $k$ của các quan sát, nên $K$ tỉ lệ lỗi độc lập, như Bước 2 của Ví dụ 02.7. Tính xác suất của biến cố bù "không $k$ nào có $L_S(h_k)=0$".
:::

::: hint Gợi ý 3
Phần (c). Tính vế phải của bất đẳng thức ở Bước 3 trong chứng minh Định lý 02.14 khi $r=0{,}4$ và $K=1000$.
:::

::: solution Lời giải Bài tập 02.4
**(a) Một giả thuyết cố định.**

**Bước 1: rủi ro kì vọng.** $h_k$ sai khi và chỉ khi $X_k=1$, nên $L_D(h_k)=\tfrac12$.

**Bước 2: cận của học viên.** $2m\epsilon^2=2\cdot10\cdot0{,}16=3{,}2$, nên $2e^{-3{,}2}\approx0{,}0815$.

**Bước 3: xác suất chính xác.** Theo (T1), số lỗi $j=10\,L_S(h_k)$ có phân bố $\mathrm{Bin}(10;\tfrac12)$. Điều kiện $\lvert j/10-\tfrac12\rvert\ge0{,}4$ đúng khi $j\in\{0,1,9,10\}$, nên
$$
\begin{aligned}
&\Pr\big(\lvert L_S(h_k)-\tfrac12\rvert\ge0{,}4\big)\\
&\quad=\frac{1+10+10+1}{1024}\\
&\quad=\frac{22}{1024}\approx0{,}0215.
\end{aligned}
$$
Giá trị này nhỏ hơn $0{,}0815$: cận cho một giả thuyết cố định đúng.

**(b) Xác suất có một giả thuyết khớp mẫu.**

**Bước 1: một giả thuyết.** $L_S(h_k)=0$ khi cả $10$ quan sát có $X_k=0$, với xác suất $2^{-10}=1/1024$. Trên biến cố này, $\lvert L_S(h_k)-L_D(h_k)\rvert=\tfrac12\ge0{,}4$.

**Bước 2: tính độc lập giữa các giả thuyết.** Biến cố $\{L_S(h_k)=0\}$ chỉ phụ thuộc tọa độ thứ $k$ của $m$ quan sát. Theo (T1) và cách dựng $D$, các tọa độ khác nhau độc lập, nên $K$ biến cố này độc lập và
$$
\begin{aligned}
&\Pr\big(\exists k:\ L_S(h_k)=0\big)\\
&\quad=1-\big(1-2^{-10}\big)^K.
\end{aligned}
$$

**Bước 3: thay số.**
$$
\begin{aligned}
K=1000:&\ \ 1-e^{1000\ln(1-2^{-10})}\\
&\ \ \approx1-e^{-0{,}9770}\\
&\ \ \approx0{,}6236,\\
K=5000:&\ \ 1-e^{5000\ln(1-2^{-10})}\\
&\ \ \approx1-e^{-4{,}8852}\\
&\ \ \approx0{,}9924.
\end{aligned}
$$

**Bước 4: kết luận.** Với $K=1000$, xác suất để có một $h$ lệch ít nhất $0{,}4$ không nhỏ hơn $0{,}6236$, lớn hơn nhiều so với $0{,}0815$. Khẳng định của học viên sai.

**(c) Đối chiếu với Định lý 02.14.**

**Bước 1: cận đúng.** Theo Bước 3 của chứng minh Định lý 02.14 với $r=0{,}4$, xác suất để $S$ không là $0{,}4$-đại diện không quá $2Ke^{-3{,}2}\approx0{,}0815K$, tức khoảng $81{,}5$ khi $K=1000$. Cận không cho thông tin, nên không mâu thuẫn với (b).

**Bước 2: bước bị bỏ qua.** Học viên bỏ Bước 3, bước áp dụng Bổ đề 02.12 cho $K$ biến cố $B_h$, và gán cho hợp $K$ biến cố xác suất của một biến cố. Ở đây tổng các xác suất $\Pr(L_S(h_k)=0)$ là $1000/1024\approx0{,}977$, cùng bậc độ lớn với xác suất $0{,}6236$ của hợp, vì các biến cố độc lập và mỗi biến cố có xác suất nhỏ.

**Kiểm tra lại.** Với $K=1$, xác suất ở (b) là $1/1024\approx0{,}001<0{,}0815$, đúng với Hệ quả 02.10; xác suất này vượt $0{,}0815$ từ $K=88$.
:::

### Bài tập 02.5 (So sánh cận giải tích với mô phỏng Bernoulli, tùy chọn)

**Mức độ:** thực nghiệm (tùy chọn). **Mục tiêu:** mục tiêu học tập 2; đọc một cận đuôi như một phát biểu về tần suất trên nhiều lần lấy mẫu.

::: exercise Bài tập 02.5
Sản phẩm cần nộp là một giao thức và một báo cáo, không cần mã. Xét phân bố $D_\eta$ của Ví dụ 02.1, giả thuyết $h_3$ cố định và hàm lỗi 0–1. Với $S\sim D_\eta^m$ theo (T1), $L_S(h_3)=k/m$ với $k\sim\mathrm{Bin}(m;0{,}22)$. Lấy $\epsilon=0{,}1$ và $m\in\{100,200\}$.

**(a)** Viết giao thức gồm $R$ lần lặp độc lập; mỗi lần sinh một mẫu và ghi biến cố thất bại $\{\lvert L_S(h_3)-0{,}22\rvert\ge0{,}1\}$. Ước lượng xác suất thất bại bằng *tần suất thất bại* (failure frequency) $\hat p$, tỉ lệ số lần thất bại trên $R$, kèm *sai số chuẩn* (standard error) $\sqrt{\hat p(1-\hat p)/R}$. Nêu cách kiểm tra biến cố để tránh sai số làm tròn tại các giá trị biên.

**(b)** Nêu giá trị mà $\hat p$ ước lượng ở mỗi cỡ mẫu và sai số chuẩn khi $R=10^4$. Chọn $R$ để ở $m=200$ sai số chuẩn không quá $10\%$ giá trị cần ước lượng.

**(c)** Nêu nội dung của báo cáo, và giải thích vì sao một lần chạy ($R=1$) không kiểm tra được cận nào của Ví dụ 02.4.

**(d)** (Mở rộng.) Mô tả cách lặp lại Ví dụ 02.7 bằng mô phỏng và nêu giá trị mà các tần suất cần ước lượng.
:::

::: hint Gợi ý 1
Mỗi lần lặp chỉ cần sinh số lỗi $k\sim\mathrm{Bin}(m;0{,}22)$. Tần suất $\hat p$ là trung bình của $R$ biến Bernoulli độc lập.
:::

::: hint Gợi ý 2
Phương sai của $\hat p$ là $p(1-p)/R$ (câu ôn nhanh 1 và Bước 2 của chứng minh Bổ đề 02.3); giá trị $p$ ở Ví dụ 02.2. Các giá trị biên được liệt kê ở Phụ lục B.1.
:::

::: solution Lời giải Bài tập 02.5
**(a) Giao thức.**

1. Cố định $m$, $R$ và một *hạt giống ngẫu nhiên* (random seed) cho bộ sinh số; ghi hạt giống vào báo cáo.
2. Với $r=1,\ldots,R$: sinh $k_r\sim\mathrm{Bin}(m;0{,}22)$ độc lập; đặt $F_r=1$ nếu $k_r\le12$ hoặc $k_r\ge32$ (khi $m=100$), nếu $k_r\le24$ hoặc $k_r\ge64$ (khi $m=200$), và $F_r=0$ trong trường hợp còn lại.
3. Tính $\hat p=\frac1R\sum_rF_r$ và sai số chuẩn.

Biến cố được kiểm tra bằng ngưỡng nguyên. Bốn giá trị biên $k=12$, $32$, $24$, $64$ cho độ lệch đúng bằng $0{,}1$ (Phụ lục B.1). Nếu tính $\lvert k/m-0{,}22\rvert$ bằng số dấu phẩy động độ chính xác đơn (single precision), $k=32$ và $k=64$ bị ghi sai.

**(b) Giá trị cần ước lượng và số lần lặp.**

**Bước 1: giá trị cần ước lượng.** Các $F_r$ độc lập, có phân bố $\mathrm{Bernoulli}(p)$, với $p$ là xác suất đuôi chính xác của Ví dụ 02.2: $p\approx0{,}0211$ khi $m=100$ và $p\approx8{,}9\cdot10^{-4}$ khi $m=200$. Do đó $\mathbb E\hat p=p$ và $\operatorname{Var}\hat p=p(1-p)/R$.

**Bước 2: sai số chuẩn khi $R=10^4$.** Khi $m=100$,
$$
\begin{aligned}
&\sqrt{0{,}0211\cdot0{,}9789}\cdot10^{-2}\\
&\quad\approx0{,}0014,
\end{aligned}
$$
khoảng $7\%$ của $p$. Khi $m=200$,
$$
\begin{aligned}
&\sqrt{8{,}94\cdot0{,}9991}\cdot10^{-4}\\
&\quad\approx3{,}0\cdot10^{-4},
\end{aligned}
$$
khoảng $33\%$ của $p$; số lần thất bại kì vọng chỉ khoảng $9$.

**Bước 3: chọn $R$.** Điều kiện $\sqrt{p(1-p)/R}\le0{,}1p$ tương đương với
$$
\begin{aligned}
R&\ge\frac{1-p}{0{,}01\,p}\\
&\approx\frac{0{,}9991}{8{,}94\cdot10^{-6}}\approx1{,}12\cdot10^5.
\end{aligned}
$$
Chọn chẳng hạn $R=1{,}2\cdot10^5$.

**(c) Báo cáo.** Báo cáo gồm $m$, $R$, hạt giống, số lần thất bại, $\hat p$ kèm sai số chuẩn, giá trị chính xác $p$ và bảng cận của Ví dụ 02.4 Bước 2. Theo Bổ đề 02.3(a) cho $\hat p$, với xác suất ít nhất $\tfrac89$, $\hat p$ nằm trong $p\pm3\sqrt{p(1-p)/R}$. Các cận của Ví dụ 02.4 lớn hơn $p$ nhiều lần, vì chúng đúng cho mọi phân bố trên $[0,1]$, còn $\hat p$ chỉ đo một phân bố.

Một lần chạy cho $\hat p=F_1\in\{0,1\}$. Cận đuôi là phát biểu về tỉ lệ các mẫu thất bại khi lấy mẫu lặp lại (Nhận xét 01.19), nên chỉ tần suất trên nhiều lần chạy độc lập mới so được với nó.

**(d) Thiên lệch do chọn.** Mỗi lần lặp sinh $k_1,\ldots,k_{1000}$ độc lập, $k_j\sim\mathrm{Bin}(1000;0{,}07)$, rồi ghi hai chỉ thị: $\mathbb 1[k_1\le50]$ cho một ứng viên cố định và $\mathbb 1[\min_jk_j\le50]$ cho ứng viên có tỉ lệ lỗi nhỏ nhất. Theo Ví dụ 02.7 và Phụ lục B.2, hai tần suất ước lượng $\approx0{,}0059$ và $\approx0{,}9974$.

**Kiểm tra lại.** Với biến cố "$>0{,}1$" thay cho "$\ge0{,}1$", tần suất sẽ quanh $0{,}0109$ và $4{,}9\cdot10^{-4}$ (Phụ lục B.1).
:::

### Bài tập 02.6 (Bất đẳng thức hợp có trọng số trên lớp đếm được)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 3; cận đồng thời trên một họ vô hạn đếm được cố định trước mẫu.

::: exercise Bài tập 02.6
Cho một họ đếm được các giả thuyết $\mathcal H=\{h_1,h_2,\ldots\}$ và các trọng số $w_k\ge0$ với $\sum_kw_k\le1$; cả họ và trọng số được chọn trước khi lấy mẫu. Cho $S\sim D^m$ theo (T1), hàm lỗi $\ell$ thỏa (T2) và (T3), và $\delta\in(0,1)$. Với mỗi $k$ có $w_k>0$, đặt
$$
r_{m,k}=\sqrt{\frac{\ln(2/(w_k\delta))}{2m}}.
$$

**(a)** Chứng minh *bất đẳng thức hợp có trọng số* (weighted union bound) sau: với xác suất ít nhất $1-\delta$, đồng thời với mọi $k$ có $w_k>0$, $\lvert L_S(h_k)-L_D(h_k)\rvert\le r_{m,k}$. Suy ra rằng với mọi chỉ số $\hat k$ chọn theo $S$ (bằng một quy tắc đo được) sao cho $w_{\hat k}>0$, ta có $L_D(h_{\hat k})\le L_S(h_{\hat k})+r_{m,\hat k}$ với xác suất ít nhất $1-\delta$. Kiểm tra rằng trọng số đều $w_k=1/K$ trên $K$ giả thuyết cho lại Định lý 02.14(a).

**(b)** Lấy $w_k=2^{-k}$, $m=1000$ và $\delta=0{,}05$. Tính $r_{m,k}$ với $k=1$, $10$, $30$ và so với bán kính $r_m$ của Định lý 02.14 khi $K=1000$.

**(c)** Xét cấu trúc của Bài tập 02.4 với $K=1000$, $m=10$ và $\delta=0{,}05$. Một học viên chọn trọng số sau khi xem mẫu: trọng số $1$ cho giả thuyết có tỉ lệ lỗi nhỏ nhất trên $S$ và $0$ cho các giả thuyết khác, rồi báo cáo bán kính $\sqrt{\ln(2/\delta)/(2m)}$ cho giả thuyết đó. Chỉ ra bước nào của (a) không còn đúng, và chứng minh bằng số rằng bảo đảm báo cáo sai.
:::

::: hint Gợi ý 1
Với mỗi $k$, chọn bán kính sao cho biến cố "giả thuyết $h_k$ lệch ít nhất bán kính đó" có xác suất không quá $w_k\delta$.
:::

::: hint Gợi ý 2
Họ biến cố là đếm được. Dùng dạng đếm được của bất đẳng thức hợp ở đoạn ngay sau Bổ đề 02.12.
:::

::: hint Gợi ý 3
Phần (c). Hệ quả 02.10(a) cần giả thuyết và bán kính cố định đối với $S$. Dùng phần (b) của Bài tập 02.4: với xác suất khoảng $0{,}62$, giả thuyết được chọn có tỉ lệ lỗi $0$.
:::

::: solution Lời giải Bài tập 02.6
**(a) Bất đẳng thức hợp có trọng số.**

**Bước 1: từng giả thuyết.** Với $w_k>0$, đặt $B_k=\{\lvert L_S(h_k)-L_D(h_k)\rvert\ge r_{m,k}\}$. Giả thuyết $h_k$ và số $r_{m,k}$ được chọn trước khi lấy mẫu, nên Hệ quả 02.10(a) áp dụng được:
$$
\begin{aligned}
\Pr(B_k)&\le2e^{-2mr_{m,k}^2}\\
&=2\exp\Big(-\ln\frac2{w_k\delta}\Big)\\
&=w_k\delta.
\end{aligned}
$$
(T1) và (T3) đi vào qua Hệ quả 02.10.

**Bước 2: bất đẳng thức hợp đếm được.** Theo dạng đếm được của Bổ đề 02.12 và $\sum_kw_k\le1$,
$$
\begin{aligned}
\Pr\Big(\bigcup_{k:\,w_k>0}B_k\Big)
&\le\sum_{k:\,w_k>0}w_k\delta\\
&\le\delta.
\end{aligned}
$$
Với xác suất ít nhất $1-\delta$, không $B_k$ nào xảy ra, tức $\lvert L_S(h_k)-L_D(h_k)\rvert<r_{m,k}$ với mọi $k$ có $w_k>0$.

**Bước 3: chỉ số chọn theo mẫu.** Trên biến cố của Bước 2, bất đẳng thức đúng cho mọi $k$ có $w_k>0$ cùng lúc, nên đúng cho $k=\hat k$ bất kể $\hat k$ được chọn thế nào. Bán kính $r_{m,\hat k}$ ngẫu nhiên qua $\hat k$, nhưng mỗi $r_{m,k}$ cố định trước mẫu. Giả thuyết có $w_k=0$ không có bảo đảm nào; họ đếm được phải chứa mọi giả thuyết có thể được chọn về sau.

**Bước 4: trọng số đều.** Với $w_k=1/K$, $k=1,\ldots,K$, ta có $\sum_kw_k=1$ và $\ln(2/(w_k\delta))=\ln(2K/\delta)$, nên $r_{m,k}=r_m$ với mọi $k$, và (a) là Định lý 02.14(a).

**(b) Trọng số $2^{-k}$.**

**Bước 1: ba bán kính.** $\sum_{k\ge1}2^{-k}=1$. Với $w_k=2^{-k}$, $\ln(2/(w_k\delta))=\ln(2^{k+1}/0{,}05)$ và $2m=2000$:
$$
\begin{aligned}
k=1:&\ \ \ln80\approx4{,}3820,\\
&\ \ r_{m,1}\approx0{,}0468,\\
k=10:&\ \ \ln40\,960\approx10{,}6204,\\
&\ \ r_{m,10}\approx0{,}0729,\\
k=30:&\ \ \ln\big(2^{31}/0{,}05\big)\\
&\ \ \approx24{,}4833,\\
&\ \ r_{m,30}\approx0{,}1106.
\end{aligned}
$$

**Bước 2: so với trọng số đều.** Với $K=1000$ và $m=1000$, $\ln40\,000\approx10{,}5966$ và $r_{1000}=\sqrt{10{,}5966/2000}\approx0{,}0728$. Giả thuyết thứ $k$ trả thêm $k\ln2$ vào lôgarit; vì $2^{10}=1024$, giả thuyết thứ $10$ có bán kính gần bằng bán kính này.

**(c) Trọng số chọn sau khi xem mẫu.**

**Bước 1: bước hỏng.** Bước 1 của (a) cần $h_k$ và $r_{m,k}$ cố định đối với $S$. Ở đây giả thuyết nhận trọng số $1$ là nghiệm ERM, phụ thuộc $S$, nên Hệ quả 02.10(a) không áp dụng được cho nó.

**Bước 2: bán kính báo cáo.**
$$
\sqrt{\frac{\ln40}{20}}\approx\sqrt{0{,}1844}\approx0{,}4295.
$$

**Bước 3: xác suất thất bại.** Theo Bài tập 02.4(b), với xác suất khoảng $0{,}6236$, một $h_k$ có $L_S(h_k)=0$; khi đó giả thuyết được chọn có tỉ lệ lỗi $0$ và rủi ro kì vọng $\tfrac12$. Độ lệch $\tfrac12$ lớn hơn $0{,}4295$, nên bảo đảm báo cáo sai với xác suất ít nhất $0{,}6236$, so với $\delta=0{,}05$.

**Bước 4: cách sửa.** Trọng số phải cố định trước mẫu. Trọng số đều $1/1000$ cho bán kính $r_{10}=\sqrt{\ln40\,000/20}\approx0{,}728$ ở $m=10$, lớn hơn độ lệch $\tfrac12$ của giả thuyết được chọn.

**Kiểm tra lại.** Với $k=1$, $r_{m,1}\approx0{,}0468$, lớn hơn bán kính $\sqrt{\ln40/2000}\approx0{,}0429$ của một giả thuyết cố định (Ví dụ 02.5): trọng số $\tfrac12$ làm lôgarit tăng thêm $\ln2$.
:::

## Bài tập chọn từ UML

### Bài tập 02.7 (Hình chữ nhật song song với trục trong trường hợp khả thực; UML Bài tập 2.3, ý 1–2)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 4; cỡ mẫu khả thực cho một lớp vô hạn, kể cả khi phân bố có nguyên tử.

::: exercise Bài tập 02.7
Cho $\mathcal X=\mathbb R^2$ với σ-đại số Borel, $\mathcal Y=\{0,1\}$ và hàm lỗi 0–1. Với $a_1\le b_1$ và $a_2\le b_2$, tập $R=[a_1,b_1]\times[a_2,b_2]$ là một *hình chữ nhật song song với trục* (axis-aligned rectangle), và $h_R(x)=\mathbb 1[x\in R]$. Lớp $\mathcal H_{\mathrm{rec}}$ gồm mọi $h_R$ và hàm âm toàn phần $h_\varnothing\equiv0$, thêm vào để thuật toán có đầu ra khi mẫu không có điểm dương. Giả sử $(D,\mathcal H_{\mathrm{rec}})$ khả thực (Định nghĩa 01.16) với giả thuyết không lỗi $h^\star$, và $S\sim D^m$ theo (T1).

Trên một mẫu $s$, thuật toán $A_{\mathrm{rec}}$ trả về $h_\varnothing$ khi $s$ không có quan sát nhãn $1$. Trong trường hợp còn lại, nó trả về $h_{R(s)}$, với $R(s)$ là hình chữ nhật nhỏ nhất chứa mọi điểm $x_i$ có $y_i=1$.

**(a)** Chứng minh rằng $A_{\mathrm{rec}}$ trả về một nghiệm ERM trên mọi mẫu khớp được bởi một giả thuyết của $\mathcal H_{\mathrm{rec}}$.

**(b)** Chứng minh rằng với mọi $\epsilon,\delta\in(0,1)$ và mọi $m\ge4\ln(4/\delta)/\epsilon$,
$$
\begin{aligned}
&\Pr_{S\sim D^m}\big[L_D(A_{\mathrm{rec}}(S))\le\epsilon\big]\\
&\quad\ge1-\delta.
\end{aligned}
$$
Lập luận phải đúng cả khi phân bố biên $D_{\mathcal X}$ có *nguyên tử* (atom), tức điểm có xác suất dương; khi đó có thể không có dải nào sát cạnh hình chữ nhật có khối lượng đúng bằng $\epsilon/4$.

**(c)** Tính cỡ mẫu ở (b) khi $\epsilon=0{,}1$ và $\delta=0{,}05$. Giải thích vì sao Mệnh đề 02.17 không cho cận này, và bất đẳng thức hợp ở (b) được áp dụng cho những biến cố nào.
:::

::: hint Gợi ý 1
Hầu chắc chắn mọi điểm dương của mẫu nằm trong hình chữ nhật đích $R^\star$ của $h^\star$, nên $R(S)\subseteq R^\star$ và thuật toán chỉ sai trên $R^\star\setminus R(S)$.
:::

::: hint Gợi ý 2
Cắt từ $R^\star$ bốn dải sát bốn cạnh. Dải bên trái là $\{x\in R^\star:\ x_1\le c_1\}$, với $c_1$ nhỏ nhất sao cho dải có khối lượng ít nhất $\epsilon/4$. Chứng minh dải mở $\{x\in R^\star:\ x_1<c_1\}$ có khối lượng không quá $\epsilon/4$, như cách làm với vành đóng ở Bài tập 01.9.
:::

::: hint Gợi ý 3
Nếu mẫu có một điểm trong mỗi dải đóng, chứng minh $R^\star\setminus R(S)$ nằm trong hợp bốn dải mở. Sau đó dùng bất đẳng thức hợp cho bốn biến cố "không quan sát nào rơi vào dải $i$".
:::

::: solution Lời giải Bài tập 02.7
**(a) Thuật toán là ERM trên mẫu khớp được.** Nếu $s$ không có điểm dương, mọi nhãn bằng $0$ và $h_\varnothing$ đúng trên cả mẫu. Nếu không, giả thuyết khớp mẫu là một $h_R$ với $R$ chứa mọi điểm dương và không chứa điểm âm nào. Mỗi tọa độ của các điểm dương nằm trong đoạn tương ứng của $R$, nên $R(s)\subseteq R$. Điểm dương nằm trong $R(s)$, điểm âm nằm ngoài $R\supseteq R(s)$, nên $L_s(h_{R(s)})=0$. Bốn cạnh của $R(s)$ là giá trị nhỏ nhất hoặc lớn nhất của hữu hạn hàm đo được của mẫu, nên điều kiện đo được của Định nghĩa 01.4 thỏa như ở Bài tập 01.9(a).

**(b) Cỡ mẫu $4\ln(4/\delta)/\epsilon$.**

**Bước 1: vùng lỗi.** Nếu $h^\star=h_\varnothing$, hầu chắc chắn mẫu không có điểm dương và rủi ro bằng $0$. Giả sử $h^\star=h_{R^\star}$ và đặt $P=D_{\mathcal X}$. Hầu chắc chắn mẫu khớp với $h^\star$ (đoạn sau Định nghĩa 01.16) và mọi điểm dương nằm trong $R^\star$, nên $R(S)\subseteq R^\star$ (quy ước $R(S)=\varnothing$ khi đầu ra là $h_\varnothing$). Đầu ra sai đúng trên $R^\star\setminus R(S)$, nên $L_D(A_{\mathrm{rec}}(S))=P(R^\star\setminus R(S))$. Nếu $P(R^\star)\le\epsilon$, rủi ro không quá $\epsilon$ với mọi mẫu; từ đây giả sử $P(R^\star)>\epsilon$.

**Bước 2: dải bên trái.** Đặt $F_1(t)=P(\{x\in R^\star:\ x_1\le t\})$. Hàm này không giảm và liên tục phải theo tính liên tục của xác suất. Tại cạnh phải của $R^\star$, nó bằng $P(R^\star)>\epsilon/4$. Đặt $c_1=\min\{t:\ F_1(t)\ge\epsilon/4\}$; giá trị nhỏ nhất đạt được nhờ tính liên tục phải. Ta có
$$
\begin{aligned}
T_1&=\{x\in R^\star:\ x_1\le c_1\},\\
U_1&=\{x\in R^\star:\ x_1<c_1\},\\
P(T_1)&\ge\epsilon/4,\quad P(U_1)\le\epsilon/4.
\end{aligned}
$$
Bất đẳng thức thứ hai đúng vì $F_1(t)<\epsilon/4$ với mọi $t<c_1$ và $P(U_1)=\lim_{t\uparrow c_1}F_1(t)$.

**Bước 3: ba dải còn lại.** Làm tương tự cho cạnh phải ($T_2=\{x_1\ge c_2\}$, $U_2=\{x_1>c_2\}$), cạnh dưới ($T_3=\{x_2\le c_3\}$, $U_3=\{x_2<c_3\}$) và cạnh trên ($T_4=\{x_2\ge c_4\}$, $U_4=\{x_2>c_4\}$), mọi dải lấy trong $R^\star$. Khi $P$ dồn vào một điểm $u\in R^\star$, $F_1$ nhảy từ $0$ lên $1$ tại $u_1$, nên $c_1=u_1$, $P(T_1)=1$ và $P(U_1)=0$: không dải nào có khối lượng đúng $\epsilon/4$, nhưng hai bất đẳng thức của Bước 2 vẫn đúng.

**Bước 4: bước tất định.** Giả sử mỗi $T_i$ chứa một điểm của mẫu. Các điểm đó hầu chắc chắn có nhãn $1$, nên $R(S)=[\hat a_1,\hat b_1]\times[\hat a_2,\hat b_2]$ thỏa $\hat a_1\le c_1$, $\hat b_1\ge c_2$, $\hat a_2\le c_3$, $\hat b_2\ge c_4$. Một điểm $x\in R^\star\setminus R(S)$ có $x_1<\hat a_1$, hoặc $x_1>\hat b_1$, hoặc $x_2<\hat a_2$, hoặc $x_2>\hat b_2$, nên thuộc một dải mở $U_i$. Do đó
$$
\begin{aligned}
L_D(A_{\mathrm{rec}}(S))&\le\sum_{i=1}^4P(U_i)\\
&\le4\cdot\frac\epsilon4=\epsilon.
\end{aligned}
$$

**Bước 5: xác suất thất bại.** Gọi $E_i$ là biến cố "không quan sát nào của $S$ rơi vào $T_i$". Theo Bước 4, trừ một biến cố có xác suất $0$, biến cố thất bại nằm trong $E_1\cup\cdots\cup E_4$. Các dải chỉ phụ thuộc $D$. Theo (T1) và $1-x\le e^{-x}$,
$$
\begin{aligned}
\Pr(E_i)&=\big(1-P(T_i)\big)^m\\
&\le\Big(1-\frac\epsilon4\Big)^m\le e^{-\epsilon m/4}.
\end{aligned}
$$
Bổ đề 02.12 cho xác suất thất bại không quá $4e^{-\epsilon m/4}$, và vế này không quá $\delta$ khi và chỉ khi $m\ge4\ln(4/\delta)/\epsilon$.

**(c) Thay số và ý nghĩa.**

**Bước 1: cỡ mẫu.** $4/\delta=80$ và $\ln80\approx4{,}3820$, nên $4\ln80/0{,}1\approx175{,}3$, làm tròn lên được $176$. Tức là $176$ quan sát đủ cho mọi phân bố khả thực.

**Bước 2: vai trò của bất đẳng thức hợp.** Lớp $\mathcal H_{\mathrm{rec}}$ vô hạn, nên cận $\ln(K/\delta)/\epsilon$ của Mệnh đề 02.17 không cho gì. Ở (b), bất đẳng thức hợp được áp dụng cho bốn biến cố $E_1,\ldots,E_4$ xác định bởi $D$, không cho các giả thuyết. $A_{\mathrm{rec}}$ chọn hình chữ nhật nhỏ nhất khớp mẫu, nên chỉ sai ở bốn phía của $R^\star$.

**Kiểm tra lại.** Tại $m=176$, $4e^{-4{,}4}\approx0{,}0491\le0{,}05$; tại $m=175$, $4e^{-4{,}375}\approx0{,}0504>0{,}05$.
:::

### Bài tập 02.8 (Lớp hội Boole; UML Bài tập 3.4)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 4 và 5; cỡ mẫu khả thực và bất khả tri cho cùng một lớp, hai tốc độ theo độ chính xác.

::: exercise Bài tập 02.8
Cho $\mathcal X=\{0,1\}^p$, $\mathcal Y=\{0,1\}$ và hàm lỗi 0–1. Với mỗi $j\in\{1,\ldots,p\}$, hàm $x\mapsto x_j$ là một biến và hàm $x\mapsto\bar x_j=1-x_j$ là phủ định của biến đó. Ta gọi chung $2p$ hàm này là các *biến hoặc phủ định của biến* (literal) và kí hiệu tập của chúng là $\mathcal U_p$. Với $L\subseteq\mathcal U_p$, *hội* (conjunction) $h_L(x)=\prod_{u\in L}u(x)$ bằng $1$ khi và chỉ khi mọi $u\in L$ bằng $1$ tại $x$; hội của tập rỗng là hàm hằng $1$, và một tập chứa cả $x_j$ lẫn $\bar x_j$ cho hàm hằng $0$. *Lớp hội Boole* (Boolean conjunctions) $\mathcal H_{\mathrm{conj}}$ gồm mọi $h_L$. Giả sử $(D,\mathcal H_{\mathrm{conj}})$ khả thực (Định nghĩa 01.16) và $S\sim D^m$ theo (T1).

**(a)** Chứng minh $\lvert\mathcal H_{\mathrm{conj}}\rvert=3^p+1$, đếm theo hàm.

**(b)** Thuật toán loại dần $A_{\mathrm{conj}}$ bắt đầu với $L=\mathcal U_p$. Với mỗi quan sát $(x_i,y_i)$ có $y_i=1$, nó loại khỏi $L$ mọi $u$ có $u(x_i)=0$, rồi trả về $h_L$. Chứng minh rằng $A_{\mathrm{conj}}$ trả về một nghiệm ERM trên mọi mẫu khớp được bởi một giả thuyết của $\mathcal H_{\mathrm{conj}}$, với $O(mp)$ phép tính.

**(c)** Dùng Mệnh đề 02.17(c), tính một cỡ mẫu đủ cho mọi thuật toán ERM trên $\mathcal H_{\mathrm{conj}}$ và mọi phân bố khả thực. Chứng minh cỡ mẫu này tăng tuyến tính theo $p$, và tính nó khi $p=10$, $\epsilon=0{,}1$, $\delta=0{,}05$.

**(d)** Với cùng lớp, $p$, $\epsilon$, $\delta$, tính cỡ mẫu $M(\epsilon,\delta)$ của Hệ quả 02.16(c). Giải thích vì sao, dưới một phân bố khả thực, hai cỡ mẫu của (c) và (d) bảo đảm cùng một biến cố. Tính lại cả hai khi $\epsilon=0{,}05$, rồi dùng chứng minh của Mệnh đề 02.17 và Hệ quả 02.16 để giải thích vì sao một cỡ mẫu tăng như $1/\epsilon$ còn cỡ mẫu kia tăng như $1/\epsilon^2$.
:::

::: hint Gợi ý 1
Phần (a). Một tập $L\subseteq\mathcal U_p$ không chứa cặp $x_j$, $\bar x_j$ nào được xác định bởi một lựa chọn cho mỗi $j$ trong ba khả năng: không có biến $j$, có $x_j$, có $\bar x_j$.
:::

::: hint Gợi ý 2
Phần (b). Nếu mẫu khớp với $h_{L^\star}$, với $L^\star$ không chứa cặp mâu thuẫn, thì mỗi điểm dương làm mọi $u\in L^\star$ bằng $1$, nên không phần tử nào của $L^\star$ bị loại.
:::

::: hint Gợi ý 3
Phần (d). Dưới phân bố khả thực, $\min_hL_D(h)=0$. So số mũ của $(1-\epsilon)^m\le e^{-\epsilon m}$ trong chứng minh Mệnh đề 02.17 với số mũ của $e^{-2m(\epsilon/2)^2}$ trong chứng minh Hệ quả 02.16.
:::

::: solution Lời giải Bài tập 02.8
**(a) Số hàm trong lớp.**

**Bước 1: tập không mâu thuẫn.** Gọi $L\subseteq\mathcal U_p$ là không mâu thuẫn nếu nó không chứa cặp $x_j$, $\bar x_j$ nào. Có $3^p$ tập như vậy. Với $L$ không mâu thuẫn, $h_L(x)=1$ khi và chỉ khi $x_j=1$ với mọi $x_j\in L$ và $x_j=0$ với mọi $\bar x_j\in L$; tập các điểm đó khác rỗng, nên $h_L$ không là hàm hằng $0$.

**Bước 2: hai tập khác nhau cho hai hàm khác nhau.** Cho $L\ne L'$ không mâu thuẫn; đổi vai trò nếu cần, có $u\in L\setminus L'$, chẳng hạn $u=x_j$ (trường hợp $\bar x_j$ tương tự). Vì $x_j\notin L'$, có điểm $x$ với $h_{L'}(x)=1$ và $x_j=0$, và tại đó $h_L(x)=0$.

**Bước 3: đếm.** Các tập không mâu thuẫn cho $3^p$ hàm khác nhau, không hàm nào là hằng $0$; mọi tập mâu thuẫn cho hàm hằng $0$. Vậy $\lvert\mathcal H_{\mathrm{conj}}\rvert=3^p+1$.

**(b) Thuật toán loại dần.** Nếu mẫu $s$ không có điểm dương, $L=\mathcal U_p$ là tập mâu thuẫn, nên $h_L\equiv0$, đúng trên mọi quan sát. Nếu không, giả thuyết khớp mẫu là $h_{L^\star}$ với $L^\star$ không mâu thuẫn. Mọi $u\in L^\star$ bằng $1$ tại mỗi điểm dương, nên không bị loại, và $L\supseteq L^\star$.

Mỗi $u$ còn trong $L$ bằng $1$ tại mọi điểm dương, vì nếu không nó đã bị loại; vậy $h_L=1$ trên các điểm dương. Tại một điểm âm $x_i$, $h_{L^\star}(x_i)=0$, nên có $u\in L^\star\subseteq L$ với $u(x_i)=0$, và $h_L(x_i)=0$. Do đó $L_s(h_L)=0$. Mỗi điểm dương cần kiểm tra $2p$ phần tử của $\mathcal U_p$, nên tổng cộng $O(mp)$ phép tính.

**(c) Cỡ mẫu khả thực.**

**Bước 1: công thức.** Lớp hữu hạn với $K=3^p+1$, cố định trước mẫu. Mệnh đề 02.17(c) cho
$$
\begin{aligned}
&M_{\mathrm{kt}}(\epsilon,\delta)\\
&\quad=\Big\lceil\frac{\ln(3^p+1)+\ln(1/\delta)}\epsilon\Big\rceil.
\end{aligned}
$$
Vì $3^p<3^p+1\le2\cdot3^p$, ta có $p\ln3<\ln(3^p+1)\le p\ln3+\ln2$, nên cỡ mẫu tăng tuyến tính theo $p$.

**Bước 2: thay số.** Với $p=10$, $K=59\,050$:
$$
\begin{aligned}
&\ln59\,050+\ln20\\
&\quad\approx10{,}9861+2{,}9957\\
&\quad=13{,}9819,
\end{aligned}
$$
và $13{,}9819/0{,}1\approx139{,}8$, nên $M_{\mathrm{kt}}(0{,}1;0{,}05)=140$.

**(d) So với cỡ mẫu bất khả tri.**

**Bước 1: công thức của Hệ quả 02.16(c).** $2K/\delta=2\,362\,000$ và $\ln2\,362\,000\approx14{,}6750$, nên $2\cdot14{,}6750/0{,}01\approx2935{,}004$ và $M(0{,}1;0{,}05)=2936$.

**Bước 2: cùng một biến cố.** Hệ quả 02.16 đúng cho mọi $D$, kể cả $D$ khả thực. Khi đó $\min_hL_D(h)=0$, nên bảo đảm $L_D(\hat h)\le\min_hL_D(h)+\epsilon$ trở thành $L_D(\hat h)\le\epsilon$, đúng bảo đảm của Mệnh đề 02.17(c). Hai cỡ mẫu $140$ và $2936$ vì thế so sánh được.

**Bước 3: giảm $\epsilon$ một nửa.**
$$
\begin{aligned}
\text{(c)}:&\ \ 13{,}9819/0{,}05\approx279{,}6,\\
\text{(d)}:&\ \ 2\cdot14{,}6750/0{,}0025\\
&\ \ \approx11\,740{,}02.
\end{aligned}
$$
Làm tròn lên được $280$ và $11\,741$: cỡ mẫu khả thực tăng $2$ lần, cỡ mẫu bất khả tri tăng khoảng $4$ lần.

**Bước 4: hai nguồn của hai tốc độ.** Trong chứng minh Mệnh đề 02.17, một giả thuyết có rủi ro trên $\epsilon$ khớp mẫu với xác suất nhỏ hơn $(1-\epsilon)^m\le e^{-\epsilon m}$; số mũ tỉ lệ với $\epsilon$. Một quan sát bị phân lớp sai là đủ để loại giả thuyết đó.

Trong chứng minh Hệ quả 02.16, bước tất định cần $\lvert L_S(h)-L_D(h)\rvert\le\epsilon/2$ cho mọi $h$, và Định lý 02.7 cho xác suất lệch $2e^{-m\epsilon^2/2}$; số mũ tỉ lệ với $\epsilon^2$. Khi $L_D(h)$ gần $\tfrac12$, độ lệch chuẩn của $L_S(h)$ cỡ $1/(2\sqrt m)$ và chỉ xuống cỡ $\epsilon$ khi $m$ cỡ $1/\epsilon^2$. Đây là tốc độ của các cận đủ; Nhận xét 02.18 bàn tính cần thiết của tốc độ này.

**Kiểm tra lại.** Với $p=1$, lớp gồm $1$, $x_1$, $\bar x_1$ và $0$, đúng $3+1=4$ hàm. Với $p=3$ và mẫu $((1,0,0),1)$, $((1,1,0),1)$, $((0,1,0),0)$, $((1,1,1),0)$, thuật toán loại $\bar x_1$, $x_2$, $x_3$ ở điểm dương thứ nhất và $\bar x_2$ ở điểm dương thứ hai, rồi trả về $h_L$ với $L=\{x_1,\bar x_3\}$; hàm này báo $0$ tại cả hai điểm âm.
:::

### Bài tập 02.9 (Quan sát độc lập nhưng không cùng phân bố; UML Bài tập 3.5)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 1; bước nào dùng tính độc lập, bước nào dùng tính cùng phân bố.

::: exercise Bài tập 02.9
Cho tập đầu vào $\mathcal X$, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1, một lớp hữu hạn $\mathcal H$ gồm $K$ hàm phân lớp và một hàm $f\in\mathcal H$. Cho $D_1,\ldots,D_m$ là các phân bố trên $\mathcal X\times\mathcal Y$, dưới mỗi phân bố đó $Y=f(X)$ hầu chắc chắn. Các quan sát $Z_i=(X_i,Y_i)\sim D_i$, $i=1,\ldots,m$, độc lập nhưng không nhất thiết cùng phân bố. Phân bố trung bình $\bar D_m=\frac1m\sum_{i=1}^mD_i$ gán cho mỗi biến cố $B$ xác suất $\frac1m\sum_iD_i(B)$. Cho $\epsilon\in(0,1)$.

**(a)** Chứng minh $L_{\bar D_m}(h)=\frac1m\sum_{i=1}^mL_{D_i}(h)=\mathbb E\,L_S(h)$ với mọi $h\in\mathcal H$.

**(b)** Chứng minh
$$
\begin{aligned}
&\Pr\big(\exists h\in\mathcal H:\ L_{\bar D_m}(h)>\epsilon,\\
&\qquad L_S(h)=0\big)\le Ke^{-\epsilon m}.
\end{aligned}
$$

**(c)** Suy ra rằng với xác suất ít nhất $1-Ke^{-\epsilon m}$, mọi nghiệm ERM $\hat h$ có $L_{\bar D_m}(\hat h)\le\epsilon$. Bảo đảm này nói gì về $L_{D_i}(\hat h)$ với một $i$ cố định?

**(d)** Chặn $\Pr(L_S(h)=0)$ cho một $h$ có $L_{\bar D_m}(h)>\epsilon$ bằng Định lý 02.7 thay cho cách làm ở (b), và so sánh hai số mũ. Chỉ ra bước dùng tính độc lập trong mỗi cách.
:::

::: hint Gợi ý 1
Phần (b). Với một $h$ cố định, viết $\Pr(L_S(h)=0)$ thành tích của $m$ xác suất, dùng tính độc lập.
:::

::: hint Gợi ý 2
Dùng bất đẳng thức trung bình cộng–trung bình nhân (arithmetic mean–geometric mean inequality, AM–GM): với $u_1,\ldots,u_m\ge0$, $\big(\prod_iu_i\big)^{1/m}\le\frac1m\sum_iu_i$. Áp dụng cho $u_i=1-L_{D_i}(h)$.
:::

::: hint Gợi ý 3
Tập $\{h\in\mathcal H:\ L_{\bar D_m}(h)>\epsilon\}$ cố định vì $\bar D_m$ không phụ thuộc mẫu. Cộng trên tập này bằng Bổ đề 02.12, như Bước 2 của chứng minh Mệnh đề 02.17.
:::

::: solution Lời giải Bài tập 02.9
**(a) Rủi ro dưới phân bố trung bình.** Hàm lỗi 0–1 là hàm chỉ thị của $B_h=\{(x,y):\ h(x)\ne y\}$, nên theo định nghĩa của $\bar D_m$,
$$
\begin{aligned}
L_{\bar D_m}(h)&=\bar D_m(B_h)\\
&=\frac1m\sum_{i=1}^mD_i(B_h)\\
&=\frac1m\sum_{i=1}^mL_{D_i}(h).
\end{aligned}
$$
Mặt khác $\mathbb E\,\ell(h,Z_i)=L_{D_i}(h)$, nên $\mathbb EL_S(h)$ bằng cùng trung bình đó. Bước này không dùng tính độc lập.

**(b) Cận $Ke^{-\epsilon m}$.**

**Bước 1: một giả thuyết, dùng tính độc lập.** Cố định $h$ và đặt $\rho_i=L_{D_i}(h)$. $L_S(h)=0$ khi và chỉ khi $h(X_i)=Y_i$ với mọi $i$, nên theo tính độc lập, $\Pr(L_S(h)=0)=\prod_{i=1}^m(1-\rho_i)$.

**Bước 2: bất đẳng thức AM–GM.** Với $u_i=1-\rho_i\ge0$ và (a),
$$
\begin{aligned}
&\prod_{i=1}^m(1-\rho_i)\\
&\le\Big(\frac1m\sum_{i=1}^m(1-\rho_i)\Big)^m\\
&=\big(1-L_{\bar D_m}(h)\big)^m.
\end{aligned}
$$

**Bước 3: giả thuyết xấu.** Nếu $L_{\bar D_m}(h)>\epsilon$ thì $0\le1-L_{\bar D_m}(h)<1-\epsilon$, nên
$$
\begin{aligned}
\Pr\big(L_S(h)=0\big)&<(1-\epsilon)^m\\
&\le e^{-\epsilon m}.
\end{aligned}
$$

**Bước 4: bất đẳng thức hợp.** Tập $\mathcal H_{>\epsilon}=\{h\in\mathcal H:\ L_{\bar D_m}(h)>\epsilon\}$ chỉ phụ thuộc $D_1,\ldots,D_m$ và có không quá $K$ phần tử. Áp dụng Bổ đề 02.12 cho các biến cố $\{L_S(h)=0\}$, $h\in\mathcal H_{>\epsilon}$, ta được cận $Ke^{-\epsilon m}$.

**(c) Hệ quả cho ERM.** Vì $f\in\mathcal H$ và $Y_i=f(X_i)$ hầu chắc chắn, $L_S(f)=0$ hầu chắc chắn, nên mọi nghiệm ERM có $L_S(\hat h)=0$ hầu chắc chắn. Trừ một biến cố có xác suất $0$, biến cố "có một nghiệm ERM với $L_{\bar D_m}(\hat h)>\epsilon$" nằm trong biến cố của (b). Như Mệnh đề 02.17, $m\ge\ln(K/\delta)/\epsilon$ đủ để xác suất ở đề ít nhất $1-\delta$.

Với một $i$ cố định, (a) chỉ cho $L_{D_i}(\hat h)\le mL_{\bar D_m}(\hat h)\le m\epsilon$; bảo đảm không chuyển sang một phân bố riêng lẻ.

**(d) Cách dùng Định lý 02.7.** Các biến $V_i=\ell(h,Z_i)\in[0,1]$ độc lập, với $\bar\mu_m=L_{\bar D_m}(h)$ theo (a); Định lý 02.7 không cần chúng cùng phân bố. Trên $\{L_S(h)=0\}$, $\bar V_m-\bar\mu_m=-L_{\bar D_m}(h)<-\epsilon$, nên Định lý 02.7(b) cho $\Pr(L_S(h)=0)\le e^{-2m\epsilon^2}$. Số mũ $2\epsilon^2$ nhỏ hơn $\epsilon$ khi $\epsilon<\tfrac12$; với $\epsilon=0{,}1$, đó là $e^{-0{,}02m}$ so với $e^{-0{,}1m}$. Cận của (b) chặt hơn và cho tốc độ $1/\epsilon$ như Nhận xét 02.18.

Cách (b) dùng tính độc lập ở Bước 1, khi viết xác suất thành tích; Định lý 02.7 dùng nó ở Bổ đề 02.5(b). Không cách nào dùng tính cùng phân bố.

**Kiểm tra lại.** Khi mọi $D_i$ bằng $D$, bất đẳng thức AM–GM xảy ra dấu bằng và (b) trở về Mệnh đề 02.17(b). Nếu $\rho_1=1$, tích ở Bước 1 bằng $0$: một giả thuyết luôn sai dưới $D_1$ không thể khớp mẫu.
:::

### Bài tập 02.10 (Kì vọng và xác suất cao; UML Bài tập 4.1)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 1, 6; chuyển giữa bảo đảm theo kì vọng và bảo đảm với xác suất cao, vai trò của tính bị chặn.

::: exercise Bài tập 02.10
Cố định một thuật toán học $A$, một phân bố $D$ trên $\mathcal Z$ và một hàm lỗi $\ell$ nhận giá trị trong $[0,1]$. Với mỗi $m$, lấy $S\sim D^m$ và đặt $V_m=L_D(A(S))$, một biến ngẫu nhiên trong $[0,1]$.

**(a)** Chứng minh rằng nếu $\lim_{m\to\infty}\mathbb E_{S\sim D^m}[V_m]=0$ thì với mọi $\epsilon>0$ và $\delta>0$ có $m(\epsilon,\delta)\in\mathbb N$ sao cho $\Pr(V_m>\epsilon)<\delta$ với mọi $m\ge m(\epsilon,\delta)$.

**(b)** Chứng minh chiều ngược lại. Chỉ ra chỗ dùng giả thiết hàm lỗi bị chặn, và cho một dãy biến không âm $V_m$ có $\Pr(V_m>\epsilon)\to0$ với mọi $\epsilon>0$ nhưng $\mathbb EV_m$ không tiến về $0$.

**(c)** Giả sử thêm $\mathbb E[V_m]\le1/\sqrt m$ với mọi $m$. Dùng cận Markov $\Pr(V_m>\epsilon)\le\mathbb EV_m/\epsilon$ ở Bước 1 của (a), với dấu "$<\delta$", tính $m(\epsilon,\delta)$ nhỏ nhất mà cận này cho khi $\epsilon=0{,}1$ và $\delta\in\{0{,}05;\ 0{,}001\}$. So cách cỡ mẫu này phụ thuộc vào $\delta$ với cỡ mẫu Hoeffding ở Ví dụ 02.4.

**(d)** Giải thích vì sao tính chất ở (a) yếu hơn yêu cầu của Định nghĩa 01.18, dù có cùng dạng.
:::

::: hint Gợi ý 1
Phần (a). Bất đẳng thức Markov cho $V_m$. Phần (b). Tách $\mathbb EV_m$ trên hai biến cố $\{V_m\le\epsilon\}$ và $\{V_m>\epsilon\}$.
:::

::: hint Gợi ý 2
Phần (a). Cần dấu "$<\delta$" chặt; chọn $m(\epsilon,\delta)$ sao cho $\mathbb EV_m\le\epsilon\delta/2$.
:::

::: hint Gợi ý 3
Phần (b). $\mathbb EV_m\le\epsilon+\Pr(V_m>\epsilon)$ vì $V_m\le1$. Với $\eta>0$ cho trước, chọn $\epsilon=\delta=\eta/2$.
:::

::: solution Lời giải Bài tập 02.10
**(a) Từ kì vọng sang xác suất cao.**

**Bước 1: bất đẳng thức Markov.** $V_m\ge0$, nên Bổ đề 02.2 với ngưỡng $\epsilon$ cho
$$
\begin{aligned}
\Pr(V_m>\epsilon)&\le\Pr(V_m\ge\epsilon)\\
&\le\frac{\mathbb EV_m}\epsilon.
\end{aligned}
$$

**Bước 2: chọn $m(\epsilon,\delta)$.** Vì $\mathbb EV_m\to0$, có $m(\epsilon,\delta)$ sao cho $\mathbb EV_m\le\epsilon\delta/2$ với mọi $m\ge m(\epsilon,\delta)$. Khi đó $\Pr(V_m>\epsilon)\le\delta/2<\delta$. Chọn $\mathbb EV_m\le\epsilon\delta$ chỉ cho "$\le\delta$".

**(b) Từ xác suất cao sang kì vọng.**

**Bước 1: tách kì vọng.** Trên $\{V_m\le\epsilon\}$, $V_m\le\epsilon$; trên $\{V_m>\epsilon\}$, $V_m\le1$ vì hàm lỗi nhận giá trị trong $[0,1]$. Do đó
$$
\begin{aligned}
\mathbb EV_m&=\mathbb E\big[V_m\mathbb 1[V_m\le\epsilon]\big]\\
&\quad+\mathbb E\big[V_m\mathbb 1[V_m>\epsilon]\big]\\
&\le\epsilon+\Pr(V_m>\epsilon).
\end{aligned}
$$
Tính bị chặn chỉ được dùng ở đây.

**Bước 2: chọn tham số.** Cho $\eta>0$ và lấy $\epsilon=\delta=\eta/2$. Với $m\ge m(\eta/2,\eta/2)$, $\Pr(V_m>\eta/2)<\eta/2$, nên $0\le\mathbb EV_m<\eta$. Vậy $\mathbb EV_m\to0$.

**Bước 3: khi bỏ tính bị chặn.** Cho $V_m=m$ với xác suất $1/m$ và $V_m=0$ trong trường hợp còn lại. Với mọi $\epsilon>0$, $\Pr(V_m>\epsilon)\le1/m\to0$, nhưng $\mathbb EV_m=1$ với mọi $m$. Bước 1 hỏng vì trên $\{V_m>\epsilon\}$ biến không bị chặn bởi $1$.

**(c) Cỡ mẫu theo cận Markov.**

**Bước 1: điều kiện.** Cận Markov cho $\Pr(V_m>\epsilon)\le1/(\epsilon\sqrt m)$, nhỏ hơn $\delta$ khi và chỉ khi $m>1/(\epsilon\delta)^2$.

**Bước 2: thay số.**
$$
\begin{aligned}
\delta=0{,}05:&\ \ \epsilon\delta=0{,}005,\\
&\ \ 1/(\epsilon\delta)^2=40\,000,\\
\delta=0{,}001:&\ \ \epsilon\delta=10^{-4},\\
&\ \ 1/(\epsilon\delta)^2=10^8,
\end{aligned}
$$
nên $m(\epsilon,\delta)=40\,001$ và $10^8+1$. Cách chọn $\mathbb EV_m\le\epsilon\delta/2$ ở Bước 2 của (a) cho $m\ge4/(\epsilon\delta)^2$, tức lớn hơn khoảng $4$ lần.

**Bước 3: so sánh.** Giảm $\delta$ đi $50$ lần làm cỡ mẫu này tăng $2500$ lần, tức như $1/\delta^2$. Ở Ví dụ 02.4, với cùng $\epsilon=0{,}1$, cỡ mẫu Hoeffding tăng từ $185$ lên $381$, tức như $\ln(1/\delta)$. Phép so này chỉ so cách phụ thuộc vào $\delta$, vì hai cỡ mẫu bảo đảm hai biến cố khác nhau.

**(d) Theo từng phân bố, không phải PAC.** Trong (a), $m(\epsilon,\delta)$ có thể phụ thuộc $D$; Định nghĩa 01.18 cần một hàm $M(\epsilon,\delta)$ dùng chung cho mọi $D$ khả thực. Trong trường hợp bất khả tri (Định nghĩa 01.25), nếu $A$ trả về giả thuyết trong một lớp $\mathcal H$ có $\inf_{h\in\mathcal H}L_D(h)>0$ thì $V_m$ không tiến về $0$; khi đó (a), (b) vẫn đúng với $V_m$ thay bằng rủi ro vượt mức $L_D(A(S))-\inf_{h\in\mathcal H}L_D(h)\in[0,1]$.

**Kiểm tra lại.** Với $m=40\,001$, $1/(0{,}1\sqrt{40\,001})\approx0{,}049999<0{,}05$; với $m=40\,000$, giá trị đúng bằng $0{,}05$, chưa đạt dấu "$<$".
:::

### Bài tập 02.11 (Hàm lỗi có trọng số trong $[0,4]$; UML Bài tập 4.2)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 4; cỡ mẫu bất khả tri khi hàm lỗi nhận giá trị trong một đoạn $[a,b]$.

::: exercise Bài tập 02.11
Cho $S\sim D^m$ theo (T1), lớp $\mathcal H$ thỏa (T4) với $K$ phần tử, và hàm lỗi $\ell$ thỏa (T2) với $a\le\ell(h,z)\le b$ cho mọi $h$, $z$, trong đó $0\le a<b$; giả thiết này thay cho (T3).

**(a)** Chứng minh rằng mọi thuật toán ERM trên $\mathcal H$ là thuật toán học PAC bất khả tri (Định nghĩa 01.25) với
$$
\begin{aligned}
&M(\epsilon,\delta)\\
&\quad=\Big\lceil\frac{2(b-a)^2\ln(2K/\delta)}{\epsilon^2}\Big\rceil.
\end{aligned}
$$

**(b)** Xét ví dụ sàng lọc: $\mathcal X=\{1,\ldots,5\}$, lớp sáu hàm ngưỡng $h_t$, $t=1,\ldots,6$, và hàm lỗi có trọng số $\ell_c$ với $(c_{FP},c_{FN})=(1,4)$: $\ell_c(h,(x,y))$ bằng $1$ khi $h(x)=1$, $y=0$, bằng $4$ khi $h(x)=0$, $y=1$, và bằng $0$ khi $h(x)=y$. Với $\epsilon=0{,}1$ (tính theo đơn vị chi phí) và $\delta=0{,}05$, tính $M(\epsilon,\delta)$ và so với cỡ mẫu $1097$ của Ví dụ 02.9.

**(c)** Đặt $\ell'=\ell_c/4$. Chứng minh rằng hai cách tính cho cùng một cỡ mẫu: Hệ quả 02.16(c) với hàm lỗi $\ell'$ và độ chính xác $\epsilon/4$, và phần (a) với hàm lỗi $\ell_c$ và độ chính xác $\epsilon$.
:::

::: hint Gợi ý 1
Với một giả thuyết cố định, áp dụng Định lý 02.7(c) cho các biến $\ell(h,Z_i)\in[a,b]$.
:::

::: hint Gợi ý 2
Đi lại chứng minh Định lý 02.14 với bán kính mới, rồi Bước 2 của chứng minh Hệ quả 02.16. Bước tất định không dùng miền giá trị của hàm lỗi.
:::

::: hint Gợi ý 3
Phần (c). Nhân hàm lỗi với một hằng số dương không đổi tập nghiệm ERM, và nhân mọi rủi ro, kể cả rủi ro vượt mức, với cùng hằng số.
:::

::: solution Lời giải Bài tập 02.11
**(a) Cỡ mẫu với miền $[a,b]$.**

**Bước 1: một giả thuyết.** Với $h$ cố định, các biến $\ell(h,Z_i)$ độc lập theo (T1), nhận giá trị trong $[a,b]$ và có kì vọng $L_D(h)$. Định lý 02.7(c) cho
$$
\begin{aligned}
&\Pr\big(\lvert L_S(h)-L_D(h)\rvert\ge r\big)\\
&\quad\le2\exp\Big(-\frac{2mr^2}{(b-a)^2}\Big).
\end{aligned}
$$

**Bước 2: bất đẳng thức hợp.** Theo (T4) và Bổ đề 02.12, xác suất để $S$ không là $r$-đại diện không quá $2K\exp(-2mr^2/(b-a)^2)$, bằng $\delta$ khi $r=(b-a)\sqrt{\ln(2K/\delta)/(2m)}=(b-a)\,r_m$.

**Bước 3: bước tất định.** Trên biến cố "$S$ là $(b-a)r_m$-đại diện", Bước 2 của chứng minh Hệ quả 02.16 cho mọi nghiệm ERM $L_D(\hat h)\le\min_{h\in\mathcal H}L_D(h)+2(b-a)r_m$. Bước này chỉ dùng (O1) và tính đại diện.

**Bước 4: cỡ mẫu.** Ta có
$$
\begin{aligned}
&2(b-a)r_m\le\epsilon\\
&\iff\frac{\ln(2K/\delta)}{2m}\\
&\qquad\le\frac{\epsilon^2}{4(b-a)^2}\\
&\iff\\&\quad m\ge\frac{2(b-a)^2\ln(2K/\delta)}{\epsilon^2}.
\end{aligned}
$$
Lấy phần nguyên trên được $M(\epsilon,\delta)$. Vì $\ell\le b$, mọi $D$ có rủi ro hữu hạn trên $\mathcal H$, nên điều kiện của Định nghĩa 01.25 thỏa với mọi $D$.

**(b) Ví dụ sàng lọc với $\ell_c$.**

**Bước 1: miền giá trị.** $\ell_c$ nhận giá trị trong $\{0,1,4\}\subset[0,4]$, nên $(b-a)^2=16$.

**Bước 2: lôgarit.** $2K/\delta=12/0{,}05=240$ và $\ln240\approx5{,}4806$.

**Bước 3: cỡ mẫu.**
$$
\begin{aligned}
\frac{2\cdot16\cdot5{,}4806}{0{,}01}&\approx17\,538{,}04,\\
M(0{,}1;0{,}05)&=17\,539.
\end{aligned}
$$
Trước khi làm tròn, $17\,538{,}04=16\cdot1096{,}13$, đúng $16$ lần giá trị của Ví dụ 02.9.

**(c) Đổi thang đo.** Với $\ell'=\ell_c/4\in[0,1]$, mọi rủi ro chia cho $4$, và tập nghiệm ERM không đổi. Rủi ro vượt mức dưới $\ell_c$ không quá $\epsilon$ khi và chỉ khi rủi ro vượt mức dưới $\ell'$ không quá $\epsilon/4$. Hệ quả 02.16(c) cho $\ell'$ với độ chính xác $\epsilon/4$:
$$
\begin{aligned}
&\Big\lceil\frac{2\ln(2K/\delta)}{(\epsilon/4)^2}\Big\rceil\\
&\quad=\Big\lceil\frac{32\ln(2K/\delta)}{\epsilon^2}\Big\rceil,
\end{aligned}
$$
đúng công thức của (a) với $(b-a)^2=16$. Hệ số $16$ là bình phương tỉ số giữa độ dài miền giá trị và độ dài $1$ của hàm lỗi 0–1.

**Kiểm tra lại.** Với $m=17\,539$, $2\cdot4\cdot\sqrt{\ln240/35\,078}\approx0{,}099997\le0{,}1$; với $m=17\,538$, giá trị này là $\approx0{,}1000001>0{,}1$.
:::
