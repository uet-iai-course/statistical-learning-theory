# Bài tập Bài 04 — Phân tích sai số, tối thiểu hóa rủi ro cấu trúc và chọn mô hình

Các bài tập dẫn định nghĩa, kết quả và ví dụ theo số hiệu của ghi chú Bài 04. Kí hiệu theo bảng kí hiệu chung và §2 của ghi chú, gồm:

- **§4.** $L^*$ là rủi ro tham chiếu (reference risk), $\operatorname{opt}_S$ là sai số tối ưu thực nghiệm (empirical optimization error).
- **§5.** $f^*$, $\bar f$, $\sigma^2(x)$ là hàm hồi quy, dự đoán trung bình và phương sai nhiễu.
- **§6–§7.** $q_k$, $\mathrm{pen}_k$ là trọng số và số hạng phạt (penalty) của lớp $k$; $k(h)$ là chỉ số nhỏ nhất của lớp chứa $h$; $k_{\max}$ là số lớp của một họ hữu hạn.
- **§8.** $V$, $m_v$, $L_V$ là mẫu xác thực (validation sample), cỡ của nó và rủi ro trên nó; $K$ là số ứng viên.

Giả thiết (T1)–(T7), (M) và thuật ngữ theo ghi chú: sai số xấp xỉ (approximation error), độ chệch (bias), phương sai (variance), bất đẳng thức oracle (oracle inequality), học không đều (nonuniform learning). Viết tắt: tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM), tối thiểu hóa rủi ro cấu trúc (structural risk minimization, SRM), học xấp xỉ với xác suất cao (probably approximately correct, PAC), chiều Vapnik–Chervonenkis (VC dimension), gọi tắt là chiều VC. Hàm lỗi là hàm lỗi 0–1 khi không ghi rõ; $\ln$ là lôgarit tự nhiên; $\delta=0{,}05$ trong mọi phép tính số.

Sáu bài đầu là bài gốc của học phần. Bảy bài sau chọn từ mục bài tập §5.5, §7.8 và §11.5 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* (Shalev-Shwartz và Ben-David, 2014; viết tắt UML). UML viết $w$ cho trọng số và $m^{NUL}$ cho hàm cỡ mẫu của học không đều; ở đây viết $q$ và $M$.

## Bài tập gốc

### Bài tập 04.1 (Cận ba thành phần cho ERM xấp xỉ)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 1; cận ba thành phần cho ERM xấp xỉ.

::: exercise Bài tập 04.1
Cho lớp $\mathcal H$, hàm lỗi $\ell$ thỏa (T2), (T3), rủi ro tham chiếu $L^*$ như ở Định nghĩa 04.1 và một $\epsilon_{\mathrm{opt}}$-ERM $A$ trên $\mathcal H$ (Định nghĩa 01.12).

**(a)** Chứng minh: nếu $S$ là $r$-đại diện đối với $(\mathcal H,\ell,D)$ thì
$$
\begin{aligned}
&L_D(A(S))-L^*\\
&\le\Big[\inf_{h\in\mathcal H}L_D(h)-L^*\Big]\\
&\quad+2r+\epsilon_{\mathrm{opt}} .
\end{aligned}
$$
Chọn $L^*$ và $r$ để suy ra Hệ quả 02.16(b) và Hệ quả 03.16(b). Với lớp thỏa (T4), thay giả thiết $\epsilon_{\mathrm{opt}}$-ERM bằng: $\operatorname{opt}_S(A(S))\le\epsilon_{\mathrm{opt}}$ trên một biến cố đo được có xác suất ít nhất $1-\delta_2$. Chứng minh cận của Hệ quả 02.16(b) đúng với xác suất ít nhất $1-\delta-\delta_2$.

**(b)** Xét mẫu $S_\eta$ của Ví dụ 01.5, lớp sáu hàm ngưỡng $h_t$ và hàm lỗi 0–1. Tính $\operatorname{opt}_{S_\eta}(h_t)$ với $t=1,\ldots,6$. Với đầu ra $\tilde h=h_4$, $L^*=0{,}18$ (rủi ro Bayes, Ví dụ 01.10) và $r=0{,}18$, tính ba số hạng của Mệnh đề 04.3(a), vế phải của cận, và so với $L_{D_\eta}(h_4)-L^*$.

**(c)** Trên $S_\eta$, tính hiệu $L_{D_\eta}(\tilde h)-L_{D_\eta}(\hat h)$ với $\tilde h=h_4$ và với $\tilde h=h_5$, cho từng nghiệm ERM $\hat h$, và đặt cạnh $\operatorname{opt}_{S_\eta}(\tilde h)$. Xác định dấu của các hiệu và cho biết mỗi hiệu đổi thế nào khi đổi nghiệm ERM làm mốc.
:::

::: hint Gợi ý 1
Phần (a). Viết điều kiện của Định nghĩa 01.12 bằng $\operatorname{opt}_S$; với phần xác suất, dùng bất đẳng thức hợp cho hai biến cố hỏng. Phần (b). Rủi ro thực nghiệm nhỏ nhất trên $S_\eta$ là $\tfrac13$ (Ví dụ 01.5).
:::

::: hint Gợi ý 2
Phần (b). Theo §6 của Bài 02, $S_\eta$ là $\epsilon$-đại diện khi và chỉ khi $\epsilon\ge0{,}18$. Phần (c). Tập nghiệm ERM trên $S_\eta$ là $\{h_2,h_3,h_5\}$; rủi ro kì vọng của chúng ở Ví dụ 01.5.
:::

::: solution Lời giải Bài tập 04.1
**(a) Dạng cho ERM xấp xỉ.**

**Bước 1: sai số tối ưu.** Theo Định nghĩa 01.12, $L_S(A(S))\le\inf_{h\in\mathcal H}L_S(h)+\epsilon_{\mathrm{opt}}$ trên mọi mẫu. Trừ $\inf_{h\in\mathcal H}L_S(h)$ ở hai vế, ta được $\operatorname{opt}_S(A(S))\le\epsilon_{\mathrm{opt}}$ (Định nghĩa 04.2).

**Bước 2: cận.** Mệnh đề 04.3(a) đúng cho mọi đầu ra, nên đúng với $\tilde h=A(S)$; thay $\operatorname{opt}_S(A(S))$ bằng cận $\epsilon_{\mathrm{opt}}$ của Bước 1.

**Bước 3: lớp hữu hạn.** Lấy $L^*=\min_{h\in\mathcal H}L_D(h)$, một rủi ro tham chiếu; số hạng thứ nhất bằng $0$. Với (T4) và $r=r_m$, Định lý 02.14(a) cho biến cố "$S$ là $r_m$-đại diện" xác suất ít nhất $1-\delta$. Trên biến cố đó,
$$
\begin{aligned}
L_D(A(S))&\le\min_{h\in\mathcal H}L_D(h)\\
&\quad+2r_m+\epsilon_{\mathrm{opt}},
\end{aligned}
$$
tức Hệ quả 02.16(b).

**Bước 4: lớp có chiều VC hữu hạn.** Với hàm lỗi 0–1, (T5), (M), $L^*=\inf_{h\in\mathcal H}L_D(h)$ và $r=\rho_m$, Định lý 03.15(a) cho Hệ quả 03.16(b).

**Bước 5: bộ giải đúng với xác suất cao.** Gọi $E_1$ là biến cố "$S$ là $r_m$-đại diện" và $E_2$ là biến cố "$\operatorname{opt}_S(A(S))\le\epsilon_{\mathrm{opt}}$". Trên $E_1\cap E_2$, Bước 2–3 cho cận của Hệ quả 02.16(b). Theo bất đẳng thức hợp, $\Pr\big((E_1\cap E_2)^c\big)\le\delta+\delta_2$.

**(b) Ba số hạng trên $S_\eta$.**

**Bước 1: sai số tối ưu thực nghiệm.** Theo Ví dụ 01.5, $L_{S_\eta}(h_t)$ với $t=1,\ldots,6$ là $\tfrac12,\tfrac13,\tfrac13,\tfrac12,\tfrac13,\tfrac12$, và giá trị nhỏ nhất là $\tfrac13$. Trừ $\tfrac13$, ta được
$$
\operatorname{opt}_{S_\eta}(h_t)=\tfrac16,\ 0,\ 0,\ \tfrac16,\ 0,\ \tfrac16 .
$$

**Bước 2: tính đại diện.** Theo §6 của Bài 02, độ lệch lớn nhất trên $S_\eta$ là $\tfrac12-0{,}32=0{,}18$ (tại $h_4$), nên Mệnh đề 04.3(a) áp dụng được với $r=0{,}18$.

**Bước 3: ba số hạng.** Sai số xấp xỉ là $\min_tL_{D_\eta}(h_t)-L^*=0{,}22-0{,}18=0{,}04$. Số hạng thống kê là $2r=0{,}36$. Sai số tối ưu thực nghiệm của $h_4$ là $\tfrac16$.

**Bước 4: so sánh.** Vế phải là $0{,}04+0{,}36+\tfrac16\approx0{,}5667$, còn giá trị thật là $L_{D_\eta}(h_4)-L^*=0{,}32-0{,}18=0{,}14$. Cận lớn hơn khoảng $0{,}43$, chủ yếu do $2r$.

**(c) Hiệu theo rủi ro kì vọng.**

**Bước 1: sáu hiệu.** Theo Ví dụ 01.5, $L_{D_\eta}(h_2)=0{,}32$, $L_{D_\eta}(h_3)=0{,}22$, $L_{D_\eta}(h_4)=0{,}32$, $L_{D_\eta}(h_5)=0{,}28$. Theo thứ tự mốc $\hat h=h_2,h_3,h_5$:
$$
\begin{aligned}
\tilde h=h_4:&\quad0;\ 0{,}10;\ 0{,}04,\\
\tilde h=h_5:&\quad-0{,}04;\ 0{,}06;\ 0 .
\end{aligned}
$$
Sai số tối ưu thực nghiệm là $\operatorname{opt}_{S_\eta}(h_4)=\tfrac16$ và $\operatorname{opt}_{S_\eta}(h_5)=0$.

**Bước 2: dấu và mốc.** Với $\tilde h=h_5$, một nghiệm ERM chính xác, hiệu âm khi mốc là $h_2$ và dương khi mốc là $h_3$. Mỗi đầu ra cho ba giá trị, tùy quy tắc chọn khi bằng nhau; $\operatorname{opt}_{S_\eta}(\tilde h)$ chỉ phụ thuộc $\tilde h$ và mẫu.

**Kiểm tra lại.** $\inf_hL_{S_\eta}(h)+\operatorname{opt}_{S_\eta}(h_4)=\tfrac13+\tfrac16=\tfrac12=L_{S_\eta}(h_4)$.
:::

### Bài tập 04.2 (Phân tích độ chệch–phương sai lấy trung bình theo đầu vào)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 2; nhãn kiểm tra độc lập, độ chệch so với sai số xấp xỉ.

::: exercise Bài tập 04.2
Dùng hàm lỗi bình phương, $L_D(f)=\mathbb E\big(f(X)-Y\big)^2$. Mẫu huấn luyện $S$ có phân bố bất kì; thuật toán cho $\hat f_S:\mathcal X\to\mathbb R$, với $(s,x)\mapsto\hat f_s(x)$ đo được. Quan sát kiểm tra $(X,Y)\sim D$ độc lập với $S$, $\mathbb EY^2<\infty$ và $\mathbb E\hat f_S(X)^2<\infty$. Các đại lượng $f^*$, $\sigma^2(x)$, $\bar f(x)$, $\operatorname{Var}_S(\hat f_S(x))$ theo Định nghĩa 04.5.

**(a)** Chứng minh
$$
\begin{aligned}
&\mathbb E_S\big[L_D(\hat f_S)\big]\\
&=\mathbb E_X\Big[\big(\bar f(X)-f^*(X)\big)^2\\
&\qquad+\operatorname{Var}_S\big(\hat f_S(X)\big)\\
&\qquad+\sigma^2(X)\Big],
\end{aligned}
$$
bằng cách tách ba số hạng như chứng minh Mệnh đề 04.6, không dẫn mệnh đề đó. Với mỗi số hạng chéo, chỉ ra điều kiện độc lập mà nó cần. Suy ra: với mọi hàm đo được $f$ có $\mathbb Ef(X)^2<\infty$, $L_D(f)\ge\mathbb E\,\sigma^2(X)$, với dấu bằng khi và chỉ khi $f=f^*$ hầu chắc chắn theo $D_{\mathcal X}$.

**(b)** Không có đầu vào: $Y_1,\ldots,Y_m$ và nhãn kiểm tra $Y$ độc lập cùng phân bố, kì vọng $\mu$, phương sai $\sigma^2$. *Ước lượng co* (shrinkage estimator) là $\gamma\bar Y$ với $\gamma\in[0,1]$. Tính độ chệch, phương sai và lỗi kiểm tra kì vọng $\mathbb E(\gamma\bar Y-Y)^2$. Tìm $\gamma^*$ làm lỗi nhỏ nhất theo $\mu$, $\sigma^2$, $m$, rồi tính lỗi tại $\gamma=1;\ 0{,}8;\ 0{,}5;\ 0$ và $\gamma^*$ khi $m=4$, $\mu=1$, $\sigma^2=1$. Giải thích vì sao không tính được $\gamma^*$ từ dữ liệu.

**(c)** Lấy nhãn kiểm tra là $Y_1$, nằm trong mẫu. Chứng minh
$$
\begin{aligned}
&\mathbb E(\gamma\bar Y-Y_1)^2\\
&=\mathbb E(\gamma\bar Y-Y)^2-\tfrac{2\gamma\sigma^2}m .
\end{aligned}
$$
Tính giá trị tại bốn $\gamma$ của (b) và tìm $\gamma$ làm đại lượng này nhỏ nhất. So với $\gamma^*$.

**(d)** Trong thiết lập của (b), xét lớp các hàm hằng và $L^*=\sigma^2$. Tính sai số xấp xỉ của lớp và độ chệch của $\gamma\bar Y$ tại $\gamma=0{,}8$ với các số của (b), và giải thích vì sao hai số khác nhau.
:::

::: hint Gợi ý 1
Phần (a). Tách $\hat f_S(X)-Y=(\hat f_S(X)-\bar f(X))+(\bar f(X)-f^*(X))+(f^*(X)-Y)$. Với mỗi số hạng chéo, lấy kì vọng có điều kiện theo đại lượng làm một thừa số trở thành hằng.
:::

::: hint Gợi ý 2
Phần (a). Vì $(X,Y)$ độc lập với $S$, $\mathbb E[Y\mid S,X]=\mathbb E[Y\mid X]=f^*(X)$. Phần (c). Tách như Ví dụ 04.5; số hạng chéo mới chứa $\operatorname{Cov}(\bar Y,Y_1)$.
:::

::: solution Lời giải Bài tập 04.2
**(a) Dạng lấy trung bình theo đầu vào.**

**Bước 1: tách.** Viết tắt $\hat f=\hat f_S(X)$, $\bar f=\bar f(X)$, $f^*=f^*(X)$. Ta có
$$
\begin{aligned}
\hat f-Y&=(\hat f-\bar f)+(\bar f-f^*)\\
&\quad+(f^*-Y).
\end{aligned}
$$
Theo định lý Fubini, $\bar f(x)$ và $\operatorname{Var}_S(\hat f_S(x))$ xác định với hầu hết $x$. Theo bất đẳng thức Jensen, $\mathbb E\bar f(X)^2\le\mathbb E\hat f_S(X)^2<\infty$ và $\mathbb Ef^*(X)^2\le\mathbb EY^2<\infty$, nên theo bất đẳng thức Cauchy–Schwarz mọi tích của ba số hạng khả tích.

**Bước 2: ba bình phương.** Vì $X$ độc lập với $S$, $\mathbb E[(\hat f-\bar f)^2\mid X]=\operatorname{Var}_S(\hat f_S(X))$. Theo định nghĩa, $\mathbb E[(f^*-Y)^2\mid X]=\sigma^2(X)$.

**Bước 3: số hạng chéo không cần độc lập.** $\bar f-f^*$ là hàm của $X$ và $\mathbb E[f^*-Y\mid X]=0$, nên
$$
\mathbb E\big[(\bar f-f^*)(f^*-Y)\big]=0 .
$$

**Bước 4: số hạng chéo cần $X$ độc lập với $S$.** Khi biết $X$, $S$ giữ nguyên phân bố, nên $\mathbb E[\hat f-\bar f\mid X]=\bar f(X)-\bar f(X)=0$ và
$$
\mathbb E\big[(\hat f-\bar f)(\bar f-f^*)\big]=0 .
$$

**Bước 5: số hạng chéo cần $(X,Y)$ độc lập với $S$.** Khi biết $(S,X)$, thừa số $\hat f-\bar f$ là hằng, và $\mathbb E[Y\mid S,X]=\mathbb E[Y\mid X]=f^*(X)$ vì $(X,Y)$ độc lập với $S$. Do đó
$$
\begin{aligned}
&\mathbb E\big[(\hat f-\bar f)(f^*-Y)\big]\\
&=\mathbb E\big[(\hat f-\bar f)\,\mathbb E[f^*-Y\mid S,X]\big]\\
&=0 .
\end{aligned}
$$
Đây là chỗ cần nhãn kiểm tra độc lập với mẫu (Ví dụ 04.5).

**Bước 6: cộng lại.** Bình phương ở Bước 1 và lấy kì vọng, dùng Bước 2–5; vế trái là $\mathbb E_S[L_D(\hat f_S)]$ theo định lý Fubini.

**Bước 7: rủi ro Bayes.** Với $f$ cố định, $\hat f_S=f$ với mọi $S$, nên $\bar f=f$ và phương sai bằng $0$:
$$
\begin{aligned}
L_D(f)&=\mathbb E\big(f(X)-f^*(X)\big)^2\\
&\quad+\mathbb E\,\sigma^2(X)\\
&\ge\mathbb E\,\sigma^2(X).
\end{aligned}
$$
Dấu bằng xảy ra khi và chỉ khi $f=f^*$ hầu chắc chắn theo $D_{\mathcal X}$; vậy $\mathbb E\,\sigma^2(X)$ là rủi ro Bayes của hàm lỗi bình phương.

**(b) Ước lượng co.**

**Bước 1: độ chệch và phương sai.** $\mathbb E[\gamma\bar Y]=\gamma\mu$, nên độ chệch là $(\gamma-1)\mu$; $\operatorname{Var}(\gamma\bar Y)=\gamma^2\sigma^2/m$.

**Bước 2: lỗi kiểm tra kì vọng.** $Y$ độc lập với mẫu, $\mathbb EY=\mu$, $\operatorname{Var}Y=\sigma^2$, nên theo Mệnh đề 04.6 với $f^*=\mu$,
$$
\begin{aligned}
&\mathbb E(\gamma\bar Y-Y)^2\\
&=(1-\gamma)^2\mu^2+\tfrac{\gamma^2\sigma^2}m+\sigma^2 .
\end{aligned}
$$

**Bước 3: bốn giá trị.** Với $m=4$, $\mu=1$, $\sigma^2=1$, ba số hạng là độ chệch bình phương $(1-\gamma)^2$, phương sai $\gamma^2/4$ và $1$:
$$
\begin{aligned}
\gamma=1:&\ 0+0{,}25+1=1{,}25,\\
\gamma=0{,}8:&\ 0{,}04+0{,}16+1\\
&\ =1{,}20,\\
\gamma=0{,}5:&\ 0{,}25+0{,}0625+1\\
&\ =1{,}3125,\\
\gamma=0:&\ 1+0+1=2{,}00.
\end{aligned}
$$

**Bước 4: giá trị tối ưu.** Đạo hàm theo $\gamma$ bằng $-2(1-\gamma)\mu^2+2\gamma\sigma^2/m$; nó bằng $0$ khi
$$
\begin{aligned}
\gamma^*&=\frac{\mu^2}{\mu^2+\sigma^2/m}\\
&=\frac1{1+0{,}25}=0{,}8 .
\end{aligned}
$$
Hàm là bậc hai lồi, nên đây là giá trị nhỏ nhất. Co từ $\gamma=1$ xuống $0{,}8$ giảm phương sai $0{,}09$, thêm $0{,}04$ độ chệch bình phương.

**Bước 5: không tính được.** $\gamma^*$ phụ thuộc $\mu$ và $\sigma^2$, hai đại lượng chưa biết.

**(c) Nhãn kiểm tra nằm trong mẫu.**

**Bước 1: tách.** $\gamma\bar Y-Y_1=(\gamma\bar Y-\gamma\mu)+(\gamma\mu-\mu)+(\mu-Y_1)$. Ba bình phương như ở (b); hai số hạng chéo chứa hằng số $\gamma\mu-\mu$ có kì vọng $0$.

**Bước 2: số hạng chéo còn lại.** Vì $\operatorname{Cov}(\bar Y,Y_1)=\tfrac1m\operatorname{Var}(Y_1)=\sigma^2/m$,
$$
\begin{aligned}
&2\,\mathbb E\big[(\gamma\bar Y-\gamma\mu)(\mu-Y_1)\big]\\
&=-2\gamma\operatorname{Cov}(\bar Y,Y_1)=-\tfrac{2\gamma\sigma^2}m .
\end{aligned}
$$
Cộng lại, ta được đẳng thức cần chứng minh.

**Bước 3: bốn giá trị.** Trừ hiệu $2\gamma\sigma^2/m=\gamma/2$ khỏi các lỗi ở (b):
$$
\begin{aligned}
\gamma=1:&\ \ 1{,}25-0{,}5=0{,}75,\\
\gamma=0{,}8:&\ \ 1{,}20-0{,}4=0{,}80,\\
\gamma=0{,}5:&\ \ 1{,}3125-0{,}25\\
&\ \ =1{,}0625,\\
\gamma=0:&\ \ 2{,}00-0=2{,}00.
\end{aligned}
$$

**Bước 4: giá trị nhỏ nhất.** Đạo hàm của đại lượng ở (c) theo $\gamma$ là
$$
\begin{aligned}
&-2(1-\gamma)\mu^2+\tfrac{2\gamma\sigma^2}m-\tfrac{2\sigma^2}m\\
&=-2(1-\gamma)\big(\mu^2+\tfrac{\sigma^2}m\big)\le0
\end{aligned}
$$
trên $[0,1]$, nên giá trị nhỏ nhất đạt tại $\gamma=1$, không co.

**Kết luận.** Chọn $\gamma$ theo lỗi trên nhãn đã dùng để huấn luyện cho $\gamma=1$, lỗi báo cáo $0{,}75$; trên nhãn mới, lỗi là $1{,}25$, so với $1{,}20$ của $\gamma^*=0{,}8$.

**(d) Độ chệch và sai số xấp xỉ.**

**Bước 1: sai số xấp xỉ.** Với hàm hằng $c$, $\mathbb E(c-Y)^2=(c-\mu)^2+\sigma^2$, nhỏ nhất tại $c=\mu$, một hàm của lớp. Do đó sai số xấp xỉ là $\sigma^2-\sigma^2=0$.

**Bước 2: độ chệch.** Theo (b), độ chệch của $0{,}8\bar Y$ là $(0{,}8-1)\mu=-0{,}2\mu$, bằng $-0{,}2$ với $\mu=1$.

**Bước 3: lý do.** Sai số xấp xỉ là tính chất của lớp, chứa hàm tốt nhất $\mu$; độ chệch là tính chất của thuật toán, có dự đoán trung bình $0{,}8\mu$, khác $\mu$ khi $\mu\ne0$.

**Kiểm tra lại.** Với $\gamma=1$, (c) cho lại $0{,}75$ của Ví dụ 04.5. Ở (d), với $\gamma=1$ cả hai số bằng $0$.
:::

### Bài tập 04.3 (Trọng số $q_k=6/(\pi^2k^2)$ và số hạng phạt của từng lớp)

**Mức độ:** tính toán, khái niệm. **Mục tiêu:** mục tiêu học tập 3, 5; điều kiện trên trọng số của (T6).

::: exercise Bài tập 04.3
Xét trọng số $q_k=6/(\pi^2k^2)$, $k\ge1$.

**(a)** Kiểm tra $\sum_kq_k=1$ và $\ln(1/q_k)=2\ln k+\ln(\pi^2/6)$.

**(b)** Với trọng số $2^{-k}$ của Bài tập 02.6, số hạng $\ln(1/q_k)$ tương ứng là $k\ln2$. Lập bảng $\ln(1/q_k)$ và $k\ln2$ với $k=1,\ldots,7$. Xác định các $k$ mà trọng số $2^{-k}$ cho số hạng lớn hơn, và chứng minh điều đó đúng với mọi $k\ge6$.

**(c)** Cho một họ đếm được các lớp hữu hạn $\mathcal H_1,\mathcal H_2,\ldots$ cố định trước mẫu, $\lvert\mathcal H_k\rvert=2^k$, hàm lỗi thỏa (T2), (T3), và bán kính của Định lý 02.14(a). Với $q_k=2^{-k}$, chứng minh
$$
\begin{aligned}
\mathrm{pen}_k^2&=\tfrac1{2m}\Big((2k+1)\ln2\\
&\qquad+\ln\tfrac1\delta\Big),
\end{aligned}
$$
rồi tính $\mathrm{pen}_k$ với $m=1000$ và $k=1,2,5,10,20$. Tính lại với $q_k=6/(\pi^2k^2)$ và so sánh hai dãy trọng số.

**(d)** Với hàm lỗi 0–1, giả sử $q_{k_0}=0$ với một chỉ số $k_0$, các trọng số khác dương và có tổng không quá $1$. Chỉ ra bước nào của chứng minh Bổ đề 04.9 không còn áp dụng được, và bảo đảm nào còn lại cho $\mathcal H_{k_0}$.

**(e)** Lấy $q_k=1/k$, $k=1,\ldots,k_{\max}$. Chỉ ra bước hỏng của chứng minh Bổ đề 04.9. Trong thiết lập của Ví dụ 04.8 ($m=10$, $k_{\max}=1000$), tính xác suất kết luận của bổ đề sai, và giải thích vì sao con số này không cứu được bảo đảm. Với $q_k=1$ (không chia), tìm $k_{\max}$ nhỏ nhất để xác suất này vượt $\delta$.
:::

::: hint Gợi ý 1
Phần (a) dùng $\sum_{k\ge1}1/k^2=\pi^2/6$. Phần (b). Xét hàm $g(k)=k\ln2-2\ln k-\ln(\pi^2/6)$ và đạo hàm của nó theo $k$ thực.
:::

::: hint Gợi ý 2
Phần (d). Bước 2 của chứng minh cần $\delta q_k\in(0,1)$. Phần (e). Trong Ví dụ 04.8, biến cố hỏng của lớp $k$ rỗng khi bán kính không nhỏ hơn $\tfrac12$.
:::

::: solution Lời giải Bài tập 04.3
**(a) Tổng và số hạng lôgarit.** Ta có
$$
\begin{aligned}
\sum_{k\ge1}q_k&=\tfrac6{\pi^2}\sum_{k\ge1}\tfrac1{k^2}\\
&=\tfrac6{\pi^2}\cdot\tfrac{\pi^2}6=1,
\end{aligned}
$$
và $\ln(1/q_k)=\ln(\pi^2k^2/6)=2\ln k+\ln(\pi^2/6)$, với $\ln(\pi^2/6)\approx0{,}4977$.

**(b) Hai dãy số hạng.**

**Bước 1: bảng.** Làm tròn đến bốn chữ số:

| $k$ | $\ln(1/q_k)$ | $k\ln2$ |
|---|---|---|
| $1$ | $0{,}4977$ | $0{,}6931$ |
| $2$ | $1{,}8840$ | $1{,}3863$ |
| $3$ | $2{,}6949$ | $2{,}0794$ |
| $4$ | $3{,}2703$ | $2{,}7726$ |
| $5$ | $3{,}7166$ | $3{,}4657$ |
| $6$ | $4{,}0812$ | $4{,}1589$ |
| $7$ | $4{,}3895$ | $4{,}8520$ |

**Bước 2: đọc bảng.** Trọng số $2^{-k}$ cho số hạng lớn hơn tại $k=1$ và $k=6,7$; tại $k=2,\ldots,5$, trọng số $6/(\pi^2k^2)$ cho số hạng lớn hơn.

**Bước 3: mọi $k\ge6$.** Đặt $g(k)=k\ln2-2\ln k-\ln(\pi^2/6)$ với $k$ thực. Ta có $g'(k)=\ln2-2/k>0$ khi $k>2/\ln2\approx2{,}885$, nên $g$ tăng trên $[3,\infty)$. Theo bảng, $g(6)=4{,}1589-4{,}0812>0$, nên $g(k)>0$ với mọi $k\ge6$.

**(c) Lớp hữu hạn có $2^k$ phần tử.**

**Bước 1: công thức với $q_k=2^{-k}$.** Theo Định lý 02.14(a) tại $\delta'=\delta2^{-k}$,
$$
\begin{aligned}
\ln\tfrac{2\lvert\mathcal H_k\rvert}{\delta q_k}&=\ln\tfrac{2\cdot2^k\cdot2^k}\delta\\
&=(2k+1)\ln2+\ln\tfrac1\delta,
\end{aligned}
$$
và $\mathrm{pen}_k^2$ là số này chia cho $2m$.

**Bước 2: công thức với $q_k=6/(\pi^2k^2)$.** Thay $k\ln2$ của $\ln(1/q_k)$ bằng $2\ln k+\ln(\pi^2/6)$: số trong ngoặc là $(k+1)\ln2+\ln(1/\delta)+2\ln k+\ln(\pi^2/6)$.

**Bước 3: số.** Với $m=1000$, $\ln(1/\delta)=\ln20\approx2{,}9957$, chia số trong ngoặc cho $2000$ rồi lấy căn:

| $k$ | $q_k=2^{-k}$ | $q_k=\tfrac6{\pi^2k^2}$ |
|---|---|---|
| $1$ | $0{,}0504$ | $0{,}0494$ |
| $2$ | $0{,}0568$ | $0{,}0590$ |
| $5$ | $0{,}0729$ | $0{,}0737$ |
| $10$ | $0{,}0937$ | $0{,}0887$ |
| $20$ | $0{,}1253$ | $0{,}1096$ |

Ví dụ, $k=10$, $q_k=2^{-k}$: $\sqrt{(21\ln2+2{,}9957)/2000}\approx\sqrt{17{,}552/2000}\approx0{,}0937$.

**Bước 4: so sánh.** Hai dãy khác nhau không quá khoảng $4\%$ khi $k\le5$, theo đúng chiều của bảng ở (b). Khi $k=20$, $2^{-k}$ làm số hạng phạt lớn hơn khoảng $14\%$, vì nó nhân đôi phần $k\ln2$ của $\ln\lvert\mathcal H_k\rvert$.

**(d) Một trọng số bằng $0$.**

**Bước 1: bước hỏng.** Bước 2 của chứng minh Bổ đề 04.9 dùng Định nghĩa 04.8 với $\delta'=\delta q_k\in(0,1)$. Với $q_{k_0}=0$, $\delta'=0$ nằm ngoài miền của bán kính, nên $\mathrm{pen}_{k_0}$ không được định nghĩa.

**Bước 2: điều kiện.** Để Bước 2 vẫn đúng tại $k_0$, cần $\Pr(B_{k_0})\le\delta q_{k_0}=0$ với mọi $D$.

**Bước 3: một phân bố.** Lấy $h\in\mathcal H_{k_0}$ và một phân bố dưới đó $h$ phân lớp sai với xác suất $p\in(0,1)$. Khi đó $L_S(h)=1$ với xác suất $p^m>0$, và độ lệch bằng $1-p$.

**Bước 4: kết luận.** Mọi số hạng phạt thỏa Bước 2 tại $k_0$ không nhỏ hơn $\sup_p(1-p)=1$. Với $\mathrm{pen}_{k_0}=1$, $B_{k_0}=\varnothing$ theo (T3); bảo đảm cho $\mathcal H_{k_0}$ chỉ còn $\lvert L_S(h)-L_D(h)\rvert\le1$. Với hàm lỗi tổng quát thỏa (T3), $1$ vẫn hợp lệ nhưng có thể không nhỏ nhất.

**(e) Trọng số có tổng lớn hơn $1$.**

**Bước 1: bước hỏng.** $\sum_{k\le1000}1/k\approx7{,}4855>1$. Bước 3 của chứng minh Bổ đề 04.9 chỉ cho $\Pr\big(\bigcup_kB_k\big)\le\sum_k\delta q_k\approx0{,}3743$, không cho $\le\delta$.

**Bước 2: bán kính.** Lớp $k$ có một phần tử, nên bán kính tại $\delta/k$ là $\sqrt{\ln(40k)/20}$. Nó nhỏ hơn $\tfrac12$ khi và chỉ khi $\ln(40k)<5$, tức $k<e^5/40\approx3{,}71$: các giá trị tại $k=1,2,3,4$ là $0{,}4295$; $0{,}4681$; $0{,}4893$; $0{,}5037$.

**Bước 3: xác suất thất bại.** Với $k\ge4$, độ lệch $\lvert L_S(h_k)-\tfrac12\rvert\le\tfrac12$ không vượt bán kính, nên $B_k=\varnothing$. Với $k\le3$, như Bước 2 của Ví dụ 04.8, $\Pr(B_k)=2^{-9}$, và các biến cố độc lập. Do đó xác suất kết luận sai là
$$
1-(1-2^{-9})^3\approx0{,}0058 .
$$

**Bước 4: vì sao không đủ.** Bổ đề phải đúng với mọi $D$ và mọi họ; $0{,}0058$ là của một phân bố, và chứng minh không còn cho cận $\delta$.

**Bước 5: phản ví dụ với $q_k=1$.** Mỗi bán kính là $0{,}4295<\tfrac12$, nên mọi lớp có $\Pr(B_k)=2^{-9}$, và xác suất thất bại là $1-(1-2^{-9})^{k_{\max}}$. Nó vượt $0{,}05$ khi và chỉ khi
$$
\begin{aligned}
k_{\max}&>\frac{\ln0{,}95}{\ln(1-2^{-9})}\approx26{,}24 .
\end{aligned}
$$
Với $k_{\max}=26$, xác suất là $0{,}0496\le0{,}05$; với $k_{\max}=27$, là $0{,}0514>0{,}05$. Vậy $k_{\max}=27$.

**Kiểm tra lại.** Với $k=1$, số trong ngoặc của hai cột ở (c) là $5{,}0752$ và $4{,}8797$, khác nhau $\ln2-\ln(\pi^2/6)\approx0{,}195$.
:::

### Bài tập 04.4 (Chọn lớp bằng SRM từ một bảng)

**Mức độ:** tính toán, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 3; lựa chọn của SRM và điều kiện bán kính hợp lệ.

::: exercise Bài tập 04.4
Các phần (a)–(c) dùng thiết lập của Ví dụ 04.9: ứng dụng ở §3, dạng chiều VC của bán kính, $\delta'=\delta q_k$, nghiệm ERM chính xác $\hat h_k$ trên mỗi lớp và các rủi ro thực nghiệm giả định của bảng trong ví dụ đó.

**(a)** Giả sử họ được kéo dài thành $25$ lớp lồng nhau (thêm $15$ chỉ số giả định), với $d_k=k+1$, $q_k=6/(\pi^2k^2)$, $m=10^4$ và rủi ro thực nghiệm giả định $L_S(\hat h_k)=0{,}155$ khi $k\ge10$. Chạy Thuật toán 04.12: xác định các lớp được duyệt, lớp làm thuật toán dừng, số lần gọi bộ giải, và giải thích vì sao các lớp sau không cần giải ERM.

**(b)** Với mười lớp của Ví dụ 04.9, thay $q_k$ bằng $1/10$, rồi bằng $2^{-k}$. Tính các tổng tại $k=2,3,4$ và kiểm tra lựa chọn.

**(c)** Với $m=10^5$ và cùng các rủi ro thực nghiệm giả định, tính $\mathrm{pen}_k$, $k=1,\ldots,10$, và lựa chọn của SRM. Sau đó đổi riêng $L_S(\hat h_4)$ thành $0{,}166$; kiểm tra các giá trị giả định vẫn không tăng theo $k$, rồi xác định lựa chọn mới.

**(d)** Xét phân bố của Ví dụ 04.10, $m=1000$, hai lớp cố định trước mẫu $\mathcal H_1=\{h\equiv1\}$ và $\mathcal H_2$ gồm các hàm $\mathbb 1_F$ với $F$ là một tập con hữu hạn của $[0,1]$, và $q_1=q_2=\tfrac12$. Người dùng lấy $\mathrm{pen}_1\approx0{,}04681$ (Bước 2 của Ví dụ 04.10) và đặt $\mathrm{pen}_2=0{,}1$ tùy ý. Xác định:

1. khi nào SRM chọn một hàm của $\mathcal H_2$, và hàm nào;
2. rủi ro kì vọng của hàm đó;
3. vế phải của Định lý 04.11(b) nếu áp dụng định lý;
4. định nghĩa bị vi phạm;
5. chỗ khác với Ví dụ 04.10.
:::

::: hint Gợi ý 1
Phần (a). Thuật toán 04.12 dừng khi $\mathrm{pen}_k\ge v$, với $v$ là tổng nhỏ nhất đã có; $\ln(4/(\delta q_k))=\ln80+2\ln k+\ln(\pi^2/6)$.
:::

::: hint Gợi ý 2
Phần (c). Các lớp lồng nhau, nên $L_S(\hat h_k)$ không tăng theo $k$. Phần (d). Trên mẫu, $\inf_{h\in\mathcal H_2}L_S(h)=0$, đạt tại $\mathbb 1_{F_+}$, với $F_+$ là tập các đầu vào có nhãn $1$; so độ lệch của hàm này với $0{,}1$.
:::

::: solution Lời giải Bài tập 04.4
**(a) Thuật toán 04.12 trên họ $25$ lớp.**

**Bước 1: công thức.** $\mathrm{pen}_k=\sqrt{8(a_k+b_k)/10^4}$, với $a_k=d_k\ln(2e\cdot10^4/d_k)$ và $b_k=\ln80+2\ln k+\ln(\pi^2/6)\approx4{,}880+2\ln k$.

**Bước 2: ba lớp đầu.** Theo Ví dụ 04.9, sau $k=1,2,3$, $v$ lần lượt là $0{,}4423$; $0{,}3790$; $0{,}3650$.

**Bước 3: các lớp $4$ đến $18$.** Số hạng phạt tăng theo $k$. Tại $k=18$, $a_{18}\approx151{,}22$, $b_{18}\approx10{,}660$ và $\mathrm{pen}_{18}=\sqrt{8\cdot161{,}88/10^4}\approx0{,}3599<0{,}3650$, nên thuật toán gọi bộ giải ở mỗi lớp. Không lớp nào thay $v$: với $k\le10$ theo Ví dụ 04.9, với $11\le k\le18$ vì $0{,}155+\mathrm{pen}_k\ge0{,}4421$.

**Bước 4: một ô, $k=19$.** $d_{19}=20$, $\ln(2e\cdot10^4/20)\approx7{,}9078$, nên $a_{19}\approx158{,}16$; $b_{19}\approx4{,}880+5{,}889=10{,}769$. Do đó
$$
\begin{aligned}
\mathrm{pen}_{19}&\approx\sqrt{8\cdot168{,}92/10^4}\\
&\approx\sqrt{0{,}13514}\approx0{,}3676 .
\end{aligned}
$$

**Bước 5: dừng.** $\mathrm{pen}_{19}\ge v\approx0{,}3650$, nên thuật toán dừng ở lớp $19$ trước khi gọi bộ giải. Với $k\ge19$ và $h\in\mathcal H_k$, $L_S(h)+\mathrm{pen}_k\ge\mathrm{pen}_{19}>v$, vì $L_S\ge0$ và $\mathrm{pen}$ không giảm. Bộ giải được gọi $18$ lần thay cho $25$; đầu ra vẫn là $\hat k=3$.

**(b) Hai dãy trọng số khác.**

**Bước 1: $q_k=1/10$.** $b_k=\ln800\approx6{,}685$ với mọi $k$. Tại $k=3$, $a_3\approx38{,}069$ và $\mathrm{pen}_3=\sqrt{8\cdot44{,}753/10^4}\approx0{,}1892$. Các tổng tại $k=2,3,4$ là
$$
\begin{aligned}
0{,}210+0{,}1699&=0{,}3799,\\
0{,}175+0{,}1892&=0{,}3642,\\
0{,}170+0{,}2062&=0{,}3762.
\end{aligned}
$$

**Bước 2: $q_k=2^{-k}$.** $b_k=\ln80+k\ln2$; tại $k=3$, $b_3\approx6{,}461$ và $\mathrm{pen}_3=\sqrt{8\cdot44{,}530/10^4}\approx0{,}1887$. Các tổng tại $k=2,3,4$ là
$$
\begin{aligned}
0{,}210+0{,}1678&=0{,}3778,\\
0{,}175+0{,}1887&=0{,}3637,\\
0{,}170+0{,}2071&=0{,}3771.
\end{aligned}
$$

**Bước 3: các lớp còn lại.** Tại $k=1$, các tổng là $0{,}4473$ và $0{,}4428$; với $k\ge5$, tổng nhỏ nhất đạt tại $k=5$: $0{,}3875$ ($q_k=1/10$) và $0{,}3896$ ($q_k=2^{-k}$).

**Bước 4: kết luận.** Theo Bước 1–3, tổng nhỏ nhất ở $k=3$ với cả hai dãy. Trọng số chỉ đi vào qua $b_k$, nhỏ so với $a_k$.

**(c) Cỡ mẫu $m=10^5$.**

**Bước 1: số hạng phạt.** Với $m=10^5$, $a_k=d_k\ln(2e\cdot10^5/d_k)$ và $\mathrm{pen}_k=\sqrt{8(a_k+b_k)/10^5}$:

| $k$ | $\mathrm{pen}_k$ | tổng |
|---|---|---|
| $1$ | $0{,}0489$ | $0{,}3489$ |
| $2$ | $0{,}0584$ | $0{,}2684$ |
| $3$ | $0{,}0659$ | $\mathbf{0{,}2409}$ |
| $4$ | $0{,}0725$ | $0{,}2425$ |
| $5$ | $0{,}0783$ | $0{,}2443$ |
| $10$ | $0{,}1013$ | $0{,}2563$ |

Các tổng tại $k=6,\ldots,9$ nằm trong $[0{,}2466;\,0{,}2533]$.

**Bước 2: lựa chọn.** SRM vẫn chọn $\hat k=3$, nhưng tổng tại $k=4$ chỉ lớn hơn khoảng $0{,}0015$, so với $0{,}0130$ khi $m=10^4$.

**Bước 3: đổi một giá trị.** Dãy giả định mới $0{,}300$; $0{,}210$; $0{,}175$; $0{,}166$; $0{,}166$; $0{,}163$; … vẫn không tăng. Tổng tại $k=4$ thành $0{,}166+0{,}0725\approx0{,}2385<0{,}2409$, nên SRM chọn $\hat k=4$.

**(d) Số hạng phạt không lấy từ một bán kính.**

**Bước 1: hai mục tiêu.** Với xác suất $1$, các đầu vào trong mẫu đôi một khác nhau, và mọi $\mathbb 1_F$ với $F$ chứa đúng các đầu vào nhãn $1$ của mẫu, chẳng hạn $\mathbb 1_{F_+}$, có $L_S=0$; mục tiêu của $\mathcal H_2$ bằng $0{,}1$. Mục tiêu của $\mathcal H_1$ là $L_S(h\equiv1)+0{,}04681$, với $L_S(h\equiv1)$ là tỉ lệ nhãn $0$.

**Bước 2: lựa chọn.** SRM chọn một hàm như vậy khi
$$
\begin{aligned}
L_S(h\equiv1)&>0{,}1-0{,}04681\\
&=0{,}05319,
\end{aligned}
$$
tức khi mẫu có ít nhất $54$ nhãn $0$. Số nhãn $0$ có phân bố $\mathrm{Bin}(1000;0{,}2)$; tính trực tiếp từ phân bố nhị thức, xác suất có không quá $53$ nhãn $0$ khoảng $1{,}1\cdot10^{-40}$.

**Bước 3: rủi ro.** Mọi tập hữu hạn có xác suất $0$ dưới $U[0,1]$, nên mọi $\mathbb 1_F$ có $L_D(\mathbb 1_F)=\Pr(Y=1)=0{,}8$ (Bước 1 của Ví dụ 04.10).

**Bước 4: vế phải nếu áp dụng sai.** Với $k=1$, $\inf_{h\in\mathcal H_1}L_D(h)+2\,\mathrm{pen}_1=0{,}2+2\cdot0{,}04681\approx0{,}2936$. Với $k=2$, giá trị là $0{,}8+0{,}2=1$. Vế phải là $0{,}2936$, còn rủi ro thật là $0{,}8$; cận trên tin cậy của Định lý 04.11(a) báo $0+0{,}1=0{,}1$.

**Bước 5: định nghĩa bị vi phạm.** Theo Định nghĩa 04.8, $\mathrm{pen}_2$ phải là $\mathrm{rad}_{\mathcal H_2}(m,\delta q_2)$ của một bán kính hội tụ đều. Dưới phân bố này, trên mọi mẫu có đầu vào đôi một khác nhau,
$$
\begin{aligned}
&\sup_{h\in\mathcal H_2}\lvert L_S(h)-L_D(h)\rvert\\
&\ge\lvert0-0{,}8\rvert=0{,}8,
\end{aligned}
$$
nên $\Pr\big[\sup_h\lvert L_S(h)-L_D(h)\rvert\le0{,}1\big]=0<1-\delta q_2$. Mọi bán kính hội tụ đều của $\mathcal H_2$ không nhỏ hơn $0{,}8$ tại mọi $\delta'\in(0,1)$.

**Bước 6: khác Ví dụ 04.10.** Ở đó lớp $\mathcal G_S$ dựng sau khi xem mẫu; ở đây phần hỏng của (T6) là bán kính.

**Kiểm tra lại.** Ở (a), nếu bỏ điều kiện dừng, bảy lớp còn lại có tổng không nhỏ hơn $0{,}155+0{,}3676=0{,}5226>0{,}3650$, nên đầu ra không đổi.
:::

### Bài tập 04.5 (Dùng lại thích nghi một mẫu xác thực)

**Mức độ:** kiểm tra giả thiết, khái niệm. **Mục tiêu:** mục tiêu học tập 5; chỗ hỏng của (T7).

::: exercise Bài tập 04.5
Dùng phân bố của Ví dụ 04.10, hàm lỗi 0–1, mẫu huấn luyện $S$ và mẫu xác thực $V$ với $m_v=1000$.

**(a)** Có $K=10$ ứng viên $g_1,\ldots,g_{10}$ là hàm của $S$, trong đó $g_1\equiv1$, và $V$ thỏa (T7) đối với chúng. Sau khi xem $V$, người phân tích thêm $g_{11}=\mathbb 1_{F_+(V)}$, với $F_+(V)$ là tập các đầu vào nhãn $1$ trong $V$, rồi chọn $\hat g$ làm $L_V$ nhỏ nhất trong $11$ ứng viên. Chặn dưới $L_D(\hat g)-\min_{j\le11}L_D(g_j)$ khi $\hat g=g_{11}$, so với vế phải của Hệ quả 04.17(a) với $K=11$, và chỉ ra giả thiết bị vi phạm.

**(b)** Một quy trình tinh chỉnh $J$ vòng gồm bốn thành phần sau.

- **Khởi tạo.** $g^{(0)}$, một hàm của $S$.
- **Phép sửa.** Ở vòng $j$, $K_0$ ánh xạ định sẵn trước khi xem $V$, áp vào $g^{(j-1)}$ và được phép dùng $S$; một trong số đó là phép giữ nguyên.
- **Quy tắc chọn.** $g^{(j)}$ là kết quả của phép sửa có $L_V$ nhỏ nhất.
- **Đầu ra.** $\hat g=g^{(J)}$.

Chứng minh rằng với xác suất ít nhất $1-\delta$ theo $(S,V)$, đồng thời với mọi $j\le J$,
$$
\begin{aligned}
L_D(\hat g)&\le L_D(g^{(j)})\\
&\quad+2\sqrt{\tfrac{\ln(2K_0^J/\delta)}{2m_v}} .
\end{aligned}
$$
Tính vế phải với $K_0=10$, $J=5$ và so với $0{,}1095$ của Ví dụ 04.12.

**(c)** Giả sử phép sửa ở mỗi vòng do người phân tích nghĩ ra sau khi xem $L_V$ của vòng trước. Giải thích vì sao lập luận của (b) không còn áp dụng. Nêu cách đánh giá đầu ra để có lại một bảo đảm.
:::

::: hint Gợi ý 1
Phần (b). Khi biết $S$, mỗi dãy lựa chọn $(c_1,\ldots,c_J)\in\{1,\ldots,K_0\}^J$ xác định một mô hình.
:::

::: hint Gợi ý 2
Phần (b). Áp dụng Định lý 02.14(a) cho mẫu $V$ và danh sách mọi mô hình đạt được, sau khi lấy điều kiện theo $S$ như Bước 1 của chứng minh Hệ quả 04.17. Vì phép giữ nguyên luôn có, $L_V(g^{(j)})$ không tăng theo $j$.
:::

::: solution Lời giải Bài tập 04.5
**(a) Một ứng viên dựng từ mẫu xác thực.**

**Bước 1: hai rủi ro.** Như Bước 1 của Ví dụ 04.10, với $V$ thay cho $S$: $L_V(g_{11})=0$ và $L_D(g_{11})=0{,}8$.

**Bước 2: so với cận.** Vì $L_V\ge0$, $g_{11}$ luôn làm $L_V$ nhỏ nhất, nên quy tắc chọn được phép trả về nó. Vì $L_D(g_1)=0{,}2$, ta có $\min_jL_D(g_j)\le0{,}2$ và
$$
\begin{aligned}
&L_D(\hat g)-\min_jL_D(g_j)\\
&\quad\ge0{,}8-0{,}2=0{,}6 .
\end{aligned}
$$
Vế phải của Hệ quả 04.17(a) với $K=11$ là $2\sqrt{\ln440/2000}\approx0{,}1103$.

**Bước 3: giả thiết hỏng.** (T7) đòi các ứng viên là hàm của $S$; $g_{11}$ dùng chính các quan sát của $V$, nên Bước 1 của chứng minh Hệ quả 04.17 không áp dụng.

**(b) Quy trình nhiều vòng với phép sửa định sẵn.**

**Bước 1: danh sách thực tế.** Khi biết $S$, mỗi dãy lựa chọn $(c_1,\ldots,c_J)$ cho một mô hình xác định. Gọi $\mathcal G(S)$ là tập các mô hình đó; nó là hàm của $S$ và có không quá $K=K_0^J$ phần tử. Mô hình trung gian $g^{(j)}$ cũng thuộc $\mathcal G(S)$: nó là mô hình của dãy gồm $j$ lựa chọn đã làm, tiếp theo $J-j$ lần giữ nguyên.

**Bước 2: biến cố.** Theo (T7), khi biết $S$, mẫu $V$ có phân bố $D^{m_v}$ và $\mathcal G(S)$ là một lớp hữu hạn cố định. Theo Định lý 02.14(a), với xác suất có điều kiện ít nhất $1-\delta$, với mọi $g\in\mathcal G(S)$,
$$
\begin{aligned}
&\lvert L_V(g)-L_D(g)\rvert\le r,\\
&r=\sqrt{\tfrac{\ln(2K_0^J/\delta)}{2m_v}},
\end{aligned}
$$
rồi lấy kì vọng theo $S$ như Bước 3 của chứng minh Hệ quả 04.17.

**Bước 3: chuỗi bất đẳng thức.** Phép giữ nguyên có mặt ở mọi vòng, nên $L_V(g^{(j)})\le L_V(g^{(j-1)})$ và $L_V(\hat g)\le L_V(g^{(j)})$ với mọi $j$. Trên biến cố của Bước 2,
$$
\begin{aligned}
L_D(\hat g)&\le L_V(\hat g)+r\\
&\le L_V(g^{(j)})+r\\
&\le L_D(g^{(j)})+2r .
\end{aligned}
$$

**Bước 4: số.** Với $K_0=10$, $J=5$, $\ln(4\cdot10^6)\approx15{,}2018$, nên
$$
\begin{aligned}
2r&=2\sqrt{15{,}2018/2000}\\
&\approx2\cdot0{,}0872\approx0{,}1744,
\end{aligned}
$$
so với $0{,}1095$ của Ví dụ 04.12.

**(c) Phép sửa nghĩ ra sau khi xem kết quả.**

**Bước 1: danh sách không cố định.** Phép sửa ở vòng $j$ phụ thuộc các giá trị $L_V$ của vòng trước. Khi đó $g^{(j)}$ không thuộc một danh sách định trước theo $S$, và Bước 1 của (b) hỏng; trường hợp cực đoan là $g_{11}$ của (a).

**Bước 2: cách sửa.** Đánh giá đầu ra trên một mẫu mới $V'$ cỡ $m'_v$, độc lập với $S$ và $V$. Khi biết $(S,V)$, $\hat g$ cố định, nên theo Hệ quả 02.10(c), $L_{V'}(\hat g)+\sqrt{\ln(1/\delta)/(2m'_v)}$ là cận trên tin cậy mức $1-\delta$ ($0{,}0387$ khi $m'_v=1000$).

**Kiểm tra lại.** Với $J=1$, $\ln(2K_0^J/\delta)=\ln400$ và (b) cho lại $0{,}1095$ của Ví dụ 04.12.
:::

### Bài tập 04.6 (Chọn bậc đa thức bằng ba quy tắc, thực nghiệm tùy chọn)

**Mức độ:** thực nghiệm (tùy chọn). **Mục tiêu:** mục tiêu học tập 2, 5; một so sánh có tập kiểm tra độc lập.

::: exercise Bài tập 04.6
Sản phẩm cần nộp là một giao thức và một báo cáo. Học viên tự chọn và ghi rõ: hàm hồi quy tổng hợp $f^*$ trên $[-1,1]$, phân bố đầu vào, hai mức phương sai nhiễu $\sigma^2$ và cỡ mẫu $m$. Hàm lỗi là hàm lỗi bình phương; các lớp là $\mathcal P_j$, $j=1,\ldots,15$, với nghiệm bình phương tối thiểu $\hat f^{(j)}$.

**(a)** Viết giao thức gồm $R\ge100$ lần lặp độc lập. Mỗi lần sinh một mẫu huấn luyện cỡ $m$ và áp dụng ba quy tắc chọn bậc:

1. bậc có rủi ro thực nghiệm nhỏ nhất;
2. bậc có rủi ro thực nghiệm cộng một số hạng phạt nhỏ nhất, với công thức và hằng số ghi rõ;
3. bậc có $L_V$ nhỏ nhất, với nghiệm khớp trên phần huấn luyện và $V$ là phần còn lại của mẫu theo một tỉ lệ ghi rõ.

Rủi ro của hàm được chọn được ước lượng trên một tập kiểm tra (test set) lớn, sinh riêng.

**(b)** Nêu các đại lượng cần báo cáo cho mỗi quy tắc và mỗi mức nhiễu: bậc được chọn và lỗi kiểm tra, dưới dạng trung bình và độ phân tán qua $R$ lần lặp.

**(c)** Nêu điều báo cáo được phép kết luận và điều không được phép kết luận.
:::

::: hint Gợi ý 1
Các tham số cố định trước khi chạy: $f^*$, $\sigma^2$, $m$, tỉ lệ chia, công thức phạt, hạt giống ngẫu nhiên.
:::

::: hint Gợi ý 2
Xem Ví dụ 04.1 cho quy tắc 1, và giả thiết hàm lỗi của Định lý 04.11, Hệ quả 04.17 cho phần (c).
:::

::: solution Lời giải Bài tập 04.6
Các con số chỉ đến từ lần chạy của học viên.

**Thiết kế.**

- **Ghi trước.** Mọi tham số của gợi ý 1, $R$ và cỡ tập kiểm tra được ghi trước khi chạy.
- **Độc lập.** Tập kiểm tra chỉ dùng để đánh giá; quy tắc 3 khớp trên ít dữ liệu hơn hai quy tắc kia.
- **Tính toán.** Với bậc $15$, giải bằng cơ sở đa thức Legendre hoặc phân tích QR, không qua hệ phương trình chuẩn.

**Báo cáo.**

- **Bậc được chọn.** Bảng tần suất cho mỗi quy tắc và mỗi mức nhiễu. Các lớp lồng nhau, nên bậc $15$ luôn đạt rủi ro thực nghiệm nhỏ nhất (Ví dụ 04.1); khi có bằng nhau (chẳng hạn $m\le16$), báo cáo ghi quy tắc chọn khi bằng nhau.
- **Lỗi kiểm tra.** Trung bình, độ lệch chuẩn và sai số chuẩn của trung bình (độ lệch chuẩn chia $\sqrt R$); hai quy tắc chỉ khác nhau khi hiệu lớn hơn vài sai số chuẩn.

**Kết luận.** Số liệu báo cáo là bằng chứng thực nghiệm cho một $f^*$, $\sigma^2$, $m$ đã chọn, không phải chứng minh. Định nghĩa 04.8, Định lý 04.11 và Hệ quả 04.17 cần hàm lỗi trong $[0,1]$ (T3), mà hàm lỗi bình phương không thỏa. Quy tắc 3 có bảo đảm khi $\lvert Y\rvert\le B$ và dự đoán được cắt vào $[-B,B]$ (Nhận xét 04.18). Quy tắc 2 cần thêm điều đó và một số hạng phạt là bán kính hội tụ đều của lớp đã cắt.

**Kiểm tra lại.** Nếu lỗi kiểm tra trung bình nhỏ hơn rủi ro Bayes $\mathbb E\,\sigma^2(X)$ (Bài tập 04.2(a)) quá vài sai số chuẩn, tập kiểm tra đã rò rỉ vào bước chọn hoặc chương trình có lỗi.
:::

## Bài tập chọn từ UML

### Bài tập 04.7 (Hai lớp hình chữ nhật trên hai và năm đặc trưng; UML Bài tập 5.2)

**Mức độ:** khái niệm, tính toán. **Mục tiêu:** mục tiêu học tập 1, 3; so hai lớp lồng nhau.

::: exercise Bài tập 04.7
Cần dự đoán một biến cố tim mạch (nhãn $1$) từ huyết áp, chỉ số khối cơ thể, tuổi, mức vận động, thu nhập. Mỗi chỉ số nhận giá trị trong một khoảng đóng bị chặn $I_j$ có độ dài dương, nên $\mathcal X=I_1\times\cdots\times I_5$. Lớp $\mathcal R_5$ là lớp hình chữ nhật song song với trục $\mathcal H^5_{\mathrm{rec}}$ của Bài tập 03.9, thu hẹp lên $\mathcal X$. Lớp $\mathcal R_2$ gồm các hàm $x\mapsto g(x_1,x_2)$ với $g\in\mathcal H^2_{\mathrm{rec}}$, trong đó $x_1$ là huyết áp và $x_2$ là chỉ số khối cơ thể. Hai thuật toán là ERM trên $\mathcal R_2$ và ERM trên $\mathcal R_5$; giả sử hai lớp thỏa (M), như lớp khoảng ở Nhận xét 03.14.

**(a)** Chứng minh $\mathcal R_2\subseteq\mathcal R_5$, suy ra quan hệ giữa hai sai số xấp xỉ với cùng $L^*$, và nêu chiều VC của hai lớp. Dùng Mệnh đề 04.3 để nêu ưu điểm và nhược điểm của mỗi thuật toán.

**(b)** Với nghiệm ERM chính xác, tính dạng chiều VC của bán kính (với $m\ge d$, nó là vế phải thứ nhất của Định lý 03.15(b)) cho hai lớp tại $m=10^3,10^4,10^5$. Gọi $a_2$, $a_5$ là sai số xấp xỉ của hai lớp. Xác định điều kiện trên $a_2-a_5$ để cận của Hệ quả 03.16(a) cho $\mathcal R_5$ nhỏ hơn cận cho $\mathcal R_2$, và giải thích cỡ mẫu ảnh hưởng thế nào đến lựa chọn.

**(c)** Khi không biết $a_2-a_5$, dùng SRM trên họ $(\mathcal R_2,\mathcal R_5)$ với $q_1=q_2=\tfrac12$ và dạng chiều VC của bán kính. Gọi $\hat h_{(2)}$, $\hat h_{(5)}$ là nghiệm ERM trên hai lớp và $\hat h$ là đầu ra của SRM. Tính hai số hạng phạt tại $m=10^4$, và viết quy tắc chọn theo hai rủi ro thực nghiệm.
:::

::: hint Gợi ý 1
Phần (a). Thêm ba cạnh $I_3$, $I_4$, $I_5$ vào một hình chữ nhật của hai chỉ số đầu. Chiều VC của $\mathcal R_2$ dùng lập luận phép chiếu ở Phụ lục C của ghi chú.
:::

::: hint Gợi ý 2
Phần (b). Gọi $\rho^{(d)}$ là bán kính tại chiều VC $d$; hai cận là $L^*+a_2+2\rho^{(4)}$ và $L^*+a_5+2\rho^{(10)}$. Phần (c). Mỗi lớp nhận $\delta'=\delta/2$.
:::

::: solution Lời giải Bài tập 04.7
**(a) Hai lớp lồng nhau.**

**Bước 1: bao hàm.** Lấy $g=h_R\in\mathcal H^2_{\mathrm{rec}}$ với $R=[a_1,b_1]\times[a_2,b_2]$, và đặt $R'=[a_1,b_1]\times[a_2,b_2]\times I_3\times I_4\times I_5$. Với $x\in\mathcal X$, ba tọa độ cuối luôn nằm trong $I_3$, $I_4$, $I_5$, nên $\mathbb 1[x\in R']=\mathbb 1[(x_1,x_2)\in R]$. Hàm $h_\varnothing$ thuộc cả hai lớp. Vậy $\mathcal R_2\subseteq\mathcal R_5$.

**Bước 2: sai số xấp xỉ.** Cận dưới đúng trên một tập lớn hơn không lớn hơn, nên $a_5\le a_2$ với cùng $L^*$ (đoạn sau Định nghĩa 04.1).

**Bước 3: chiều VC.** Theo Bài tập 03.9, $\mathcal H^p_{\mathrm{rec}}$ có chiều VC $2p$; tập tách trọn của bài đó dịch và co được vào $\mathcal X$, nên $\mathcal R_5$ có chiều VC $10$. Lớp $\mathcal R_2$ là $\mathcal H^2_{\mathrm{rec}}$ ghép với phép chiếu lên hai tọa độ đầu, nên có chiều VC $4$ (Phụ lục C của ghi chú).

**Bước 4: ưu và nhược.** Theo Mệnh đề 04.3, $\mathcal R_5$ có sai số xấp xỉ không lớn hơn nhưng bán kính lớn hơn; $\mathcal R_2$ có bán kính nhỏ hơn nhưng bỏ qua tuổi, mức vận động và thu nhập.

**(b) Bán kính và cỡ mẫu.**

**Bước 1: bán kính.** Gọi $\rho^{(d)}$ là bán kính tại chiều VC $d$, với $(\rho^{(d)})^2=\tfrac8m\big(d\ln\tfrac{2em}d+\ln80\big)$:

| $m$ | $d=4$ | $d=10$ |
|---|---|---|
| $10^3$ | $0{,}5157$ | $0{,}7341$ |
| $10^4$ | $0{,}1843$ | $0{,}2689$ |
| $10^5$ | $0{,}0643$ | $0{,}0953$ |

**Bước 2: điều kiện.** Theo Hệ quả 03.16(a), hai cận cho $L_D(\hat h)-L^*$ là $a_2+2\rho^{(4)}$ và $a_5+2\rho^{(10)}$. Cận của $\mathcal R_5$ nhỏ hơn khi và chỉ khi
$$
a_2-a_5>2\big(\rho^{(10)}-\rho^{(4)}\big),
$$
tức hơn $0{,}4369$; $0{,}1693$; $0{,}0619$ tại $m=10^3,10^4,10^5$.

**Bước 3: ảnh hưởng của cỡ mẫu.** Với $10^3$ quan sát, ba chỉ số thêm phải giảm sai số xấp xỉ hơn $0{,}44$ thì cận mới ưu tiên $\mathcal R_5$; với $10^5$ quan sát, chỉ cần hơn $0{,}062$. Tại $m=10^3$, $2\rho^{(4)}\approx1{,}03$ và $2\rho^{(10)}\approx1{,}47$, nên cả hai cận lớn hơn $1$ và không cho thông tin; phép so chỉ có nghĩa từ khoảng $m=10^4$.

**(c) SRM trên hai lớp.**

**Bước 1: số hạng phạt.** Tại $\delta'=0{,}025$, $\ln(4/\delta')=\ln160\approx5{,}075$. Với $d=4$: $4\ln(2e\cdot10^4/4)\approx38{,}069$, cộng $5{,}075$, nhân $8\cdot10^{-4}$ được $0{,}03452$, nên $\mathrm{pen}_1\approx0{,}1858$. Cùng cách tính với $d=10$ cho $\mathrm{pen}_2\approx0{,}2699$.

**Bước 2: quy tắc.** SRM chọn $\mathcal R_5$ khi và chỉ khi $L_S(\hat h_{(5)})+0{,}2699<L_S(\hat h_{(2)})+0{,}1858$, tức khi rủi ro thực nghiệm giảm hơn $0{,}0841$ nhờ ba chỉ số thêm. Theo Định lý 04.11(b), với xác suất ít nhất $0{,}95$,
$$
\begin{aligned}
&L_D(\hat h)-L^*\\
&\le\min\{a_2+0{,}3716,\\
&\qquad a_5+0{,}5399\}.
\end{aligned}
$$

**Kiểm tra lại.** Hiệu $0{,}5399-0{,}3716=0{,}1683$ gần ngưỡng $0{,}1693$ của (b) tại $m=10^4$.
:::

### Bài tập 04.8 (Trọng số không giảm có tổng hữu hạn bằng $0$; UML Bài tập 7.2)

**Mức độ:** chứng minh. **Mục tiêu:** mục tiêu học tập 3. Ý (b) xử lý trường hợp mọi trọng số bằng $0$.

::: exercise Bài tập 04.8
Cho lớp vô hạn đếm được $\mathcal H=\{h_1,h_2,\ldots\}$ cho phân lớp nhị phân, các $h_n$ đôi một khác nhau, và trọng số $q:\mathcal H\to[0,1]$.

**(a)** Chứng minh: nếu $\sum_nq(h_n)\le1$ và $q$ không giảm theo chỉ số ($q(h_i)\le q(h_j)$ khi $i<j$) thì $q(h_n)=0$ với mọi $n$.

**(b)** Coi mỗi $h_n$ là một lớp một phần tử. Giải thích vì sao trọng số bằng $0$ ở (a) không cho số hạng phạt nào dùng được trong Bổ đề 04.9 và Hệ quả 04.15, và suy ra không có trọng số không giảm nào thỏa (T6).
:::

::: hint Gợi ý 1
Phần (a). Giả sử có một trọng số dương và xét tổng của phần đuôi của dãy.
:::

::: hint Gợi ý 2
Phần (a). Nếu $q(h_j)=c>0$ thì $q(h_n)\ge c$ với mọi $n\ge j$. Phần (b) dùng Bài tập 04.3(d).
:::

::: solution Lời giải Bài tập 04.8
**(a) Mọi trọng số bằng $0$.** Giả sử có $j$ với $q(h_j)=c>0$. Theo tính không giảm, $q(h_n)\ge c$ với mọi $n\ge j$, và các $h_n$ đôi một khác nhau, nên
$$
\begin{aligned}
\sum_nq(h_n)&\ge\sum_{n\ge j}q(h_n)\\
&\ge\sum_{n\ge j}c=\infty,
\end{aligned}
$$
trái với $\sum_nq(h_n)\le1$. Vậy mọi trọng số bằng $0$.

**(b) Trọng số bằng $0$.**

**Bước 1: (T6) hỏng.** Dãy toàn $0$ có tổng $0\le1$ và không giảm, nên thỏa cả hai điều kiện của (a). Tuy nhiên (T6) đòi $q_k>0$, và với $q(h_n)=0$, xác suất thất bại $\delta q(h_n)=0$ nằm ngoài miền của bán kính.

**Bước 2: số hạng phạt.** Theo Bài tập 04.3(d), với hàm lỗi 0–1, mọi số hạng phạt hợp lệ tại xác suất thất bại $0$ không nhỏ hơn $1$.

**Bước 3: hệ quả.** Cận của Định lý 04.11(b) không nhỏ hơn $2$, và cỡ mẫu $M_k(\epsilon)$ của Hệ quả 04.15 không hữu hạn với $\epsilon<2$. Theo (a), không có trọng số không giảm nào vừa dương vừa có tổng không quá $1$.

**Kiểm tra lại.** Trọng số giảm $6/(\pi^2n^2)$ dương và có tổng $1$; (a) chỉ loại các trọng số không ưu tiên chỉ số nhỏ.
:::

### Bài tập 04.9 (Trọng số từ chỉ số lớp và số phần tử; UML Bài tập 7.3)

**Mức độ:** chứng minh, tính toán (phần (c) là phần thử thách). **Mục tiêu:** mục tiêu học tập 3; trọng số trên từng giả thuyết.

::: exercise Bài tập 04.9
Cho $\mathcal H=\bigcup_{k\ge1}\mathcal H_k$, mỗi $\mathcal H_k$ hữu hạn, khác rỗng, cố định trước mẫu; các lớp có thể chồng nhau. Với $h\in\mathcal H$, đặt $k(h)=\min\{k:h\in\mathcal H_k\}$. Cho trọng số $q_k>0$ trên các lớp với $\sum_kq_k\le1$.

**(a)** Tìm trọng số $q:\mathcal H\to(0,1]$ chỉ phụ thuộc $k(h)$ và $\lvert\mathcal H_{k(h)}\rvert$, với $\sum_{h\in\mathcal H}q(h)\le1$. Cho một ví dụ mà tổng nhỏ hơn hẳn $1$ dù $\sum_kq_k=1$.

**(b)** Coi mỗi $h$ là một lớp một phần tử với trọng số $q(h)$ và bán kính của Định lý 02.14(a). Chứng minh số hạng phạt của $h$ bằng số hạng phạt của lớp $\mathcal H_{k(h)}$ trong Bổ đề 04.9 với trọng số $q_{k(h)}$. Tính số hạng này khi $\lvert\mathcal H_k\rvert=2^k$, $q_k=2^{-k}$, $k(h)=3$, $m=1000$.

**(c)** (Thử thách.) Dựng trọng số dương có tổng không quá $1$ khi mỗi $\mathcal H_k$ đếm được, có thể vô hạn.
:::

::: hint Gợi ý 1
Phần (a). Thử $q(h)=q_{k(h)}/\lvert\mathcal H_{k(h)}\rvert$, rồi nhóm các $h$ theo giá trị của $k(h)$.
:::

::: hint Gợi ý 2
Phần (a). $\{h:k(h)=k\}\subseteq\mathcal H_k$, và bao hàm có thể chặt. Phần (c). Liệt kê $\mathcal H_k=\{h_{k,1},h_{k,2},\ldots\}$ và nhân $q_k$ với một trọng số theo vị trí trong danh sách.
:::

::: solution Lời giải Bài tập 04.9
**(a) Trọng số theo lớp đầu tiên.**

**Bước 1: định nghĩa.** Đặt $q(h)=q_{k(h)}/\lvert\mathcal H_{k(h)}\rvert$; nó dương và chỉ phụ thuộc $k(h)$ và $\lvert\mathcal H_{k(h)}\rvert$.

**Bước 2: tổng.** Các tập $\{h:k(h)=k\}$, $k\ge1$, rời nhau và phủ $\mathcal H$, và $\{h:k(h)=k\}\subseteq\mathcal H_k$. Do đó
$$
\begin{aligned}
\sum_{h\in\mathcal H}q(h)&=\sum_kq_k\frac{N_k}{\lvert\mathcal H_k\rvert}\\
&\le\sum_kq_k\le1 ,
\end{aligned}
$$
trong đó $N_k=\lvert\{h:k(h)=k\}\rvert\le\lvert\mathcal H_k\rvert$.

**Bước 3: tổng nhỏ hơn hẳn $1$.** Lấy $\mathcal H_k=\{g_1,\ldots,g_k\}$ lồng nhau và $q_k=2^{-k}$. Khi đó $\{h:k(h)=k\}=\{g_k\}$, $q(g_k)=2^{-k}/k$, và
$$
\begin{aligned}
\sum_kq(g_k)&=\sum_k\frac{2^{-k}}k\\
&=\ln2\approx0{,}693 .
\end{aligned}
$$

**(b) Hai số hạng phạt.**

**Bước 1: đẳng thức.** Với $k=k(h)$, bán kính của lớp một phần tử tại $\delta q(h)$ là
$$
\begin{aligned}
\sqrt{\tfrac{\ln(2/(\delta q(h)))}{2m}}&=\sqrt{\tfrac{\ln(2\lvert\mathcal H_k\rvert/(\delta q_k))}{2m}},
\end{aligned}
$$
đúng bằng $\mathrm{pen}_k=\mathrm{rad}_{\mathcal H_k}(m,\delta q_k)$ với bán kính của Định lý 02.14(a).

**Bước 2: số.** Với $k=3$, $q(h)=2^{-3}/2^3=2^{-6}$ và
$$
\begin{aligned}
\ln\tfrac2{\delta q(h)}&=7\ln2+\ln20\\
&\approx7{,}848,\\
\sqrt{7{,}848/2000}&\approx0{,}0626 .
\end{aligned}
$$
Đây là công thức của Bài tập 04.3(c) với $q_k=2^{-k}$ tại $k=3$.

**(c) Lớp đếm được.** Liệt kê $\mathcal H_k=\{h_{k,1},h_{k,2},\ldots\}$ trước mẫu và gọi $j(h)$ là vị trí của $h$ trong danh sách của $\mathcal H_{k(h)}$. Đặt $q(h)=q_{k(h)}2^{-j(h)}>0$. Như Bước 2 của (a),
$$
\begin{aligned}
\sum_hq(h)&\le\sum_kq_k\sum_{j\ge1}2^{-j}\\
&\le1 .
\end{aligned}
$$

**Kiểm tra lại.** Với các lớp rời nhau, $\{h:k(h)=k\}=\mathcal H_k$ và tổng ở (a) bằng đúng $\sum_kq_k$.
:::

### Bài tập 04.10 (Bất đẳng thức oracle cho độ dài mô tả; UML Bài tập 7.4)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 3; trọng số Kraft.

::: exercise Bài tập 04.10
Cho lớp $\mathcal H$, một *ngôn ngữ mô tả* (description language) $\mathrm{d}:\mathcal H\to\{0,1\}^*$ đơn ánh và không tiền tố (Nhận xét 04.13), và $\lvert h\rvert$ là độ dài của $\mathrm{d}(h)$. Hàm lỗi 0–1, $S\sim D^m$ theo (T1), $\delta\in(0,1)$. Quy tắc *độ dài mô tả tối thiểu* (minimum description length, MDL) trả về $h_S$ làm nhỏ nhất
$$
\Phi(h)=L_S(h)+\sqrt{\tfrac{\lvert h\rvert+\ln(2/\delta)}{2m}} ,
$$
chọn đo được khi có nhiều nghiệm. Với $B>0$, đặt $\mathcal H_B=\{h:\lvert h\rvert\le B\}$, giả sử khác rỗng, và $h^*_B\in\arg\min_{h\in\mathcal H_B}L_D(h)$.

**(a)** Chứng minh $\lvert\mathcal H_B\rvert\le2^B$ và $h_S$, $h^*_B$ tồn tại.

**(b)** Chứng minh rằng với xác suất ít nhất $1-\delta$, đồng thời với mọi $B$,
$$
\begin{aligned}
L_D(h_S)&\le L_D(h^*_B)\\
&\quad+2\sqrt{\tfrac{B+\ln(2/\delta)}{2m}} .
\end{aligned}
$$
Chỉ ra chỗ dùng tính không tiền tố.

**(c)** Tính vế phải của (b) với $B=100$, $m=10^4$, và so với cận của Hệ quả 02.16(a) cho ERM trên $\mathcal H_B$.
:::

::: hint Gợi ý 1
Bất đẳng thức Kraft $\sum_h2^{-\lvert h\rvert}\le1$ cho trọng số $q_h=2^{-\lvert h\rvert}$. Phần (a). Mỗi $h\in\mathcal H_B$ có $2^{-\lvert h\rvert}\ge2^{-B}$.
:::

::: hint Gợi ý 2
Phần (b). Số hạng phạt của Bổ đề 04.9 cho lớp $\{h\}$ là $\sqrt{(\lvert h\rvert\ln2+\ln(2/\delta))/(2m)}$, không vượt quá số hạng trong $\Phi$ vì $\ln2<1$. Lặp lại chuỗi ba bất đẳng thức của chứng minh Định lý 04.11.
:::

::: solution Lời giải Bài tập 04.10
**(a) Tồn tại.**

**Bước 1: số phần tử.** Theo bất đẳng thức Kraft, dùng tính không tiền tố,
$$
\lvert\mathcal H_B\rvert\,2^{-B}\le\sum_{h\in\mathcal H_B}2^{-\lvert h\rvert}\le1,
$$
nên $\lvert\mathcal H_B\rvert\le2^B$. Lớp $\mathcal H_B$ hữu hạn và khác rỗng, nên $h^*_B$ tồn tại.

**Bước 2: nghiệm MDL.** Cố định $h_0\in\mathcal H$. Vì $L_S\ge0$, mọi $h$ có số hạng căn lớn hơn $\Phi(h_0)$ có $\Phi(h)>\Phi(h_0)$. Các $h$ còn lại có $\lvert h\rvert\le B_0=2m\Phi(h_0)^2-\ln(2/\delta)$, nên thuộc $\mathcal H_{B_0}$, hữu hạn theo Bước 1 và chứa $h_0$. Giá trị nhỏ nhất của $\Phi$ trên $\mathcal H_{B_0}$ là giá trị nhỏ nhất trên $\mathcal H$.

**(b) Bất đẳng thức oracle.**

**Bước 1: biến cố.** Vì $\mathrm d$ đơn ánh vào $\{0,1\}^*$, các lớp $\{h\}$ lập thành một danh sách đếm được cố định trước mẫu. Mỗi lớp có bán kính $\sqrt{\ln(2/\delta')/(2m)}$ (Định lý 02.14(a) với $K=1$) và trọng số $q_h=2^{-\lvert h\rvert}>0$, với $\sum_hq_h\le1$ theo bất đẳng thức Kraft; đây là chỗ dùng tính không tiền tố. Theo Bổ đề 04.9, với xác suất ít nhất $1-\delta$, với mọi $h$,
$$
\begin{aligned}
&\lvert L_S(h)-L_D(h)\rvert\\
&\le\sqrt{\tfrac{\lvert h\rvert\ln2+\ln(2/\delta)}{2m}}\le P(h),
\end{aligned}
$$
với $P(h)=\sqrt{(\lvert h\rvert+\ln(2/\delta))/(2m)}$, vì $\ln2<1$.

**Bước 2: chuỗi bất đẳng thức.** Trên biến cố đó,
$$
\begin{aligned}
L_D(h_S)&\le L_S(h_S)+P(h_S)\\
&\le L_S(h^*_B)+P(h^*_B)\\
&\le L_D(h^*_B)+2P(h^*_B)\\
&\le L_D(h^*_B)\\
&\quad+2\sqrt{\tfrac{B+\ln(2/\delta)}{2m}} .
\end{aligned}
$$
Bất đẳng thức thứ nhất và thứ ba dùng Bước 1, thứ hai dùng định nghĩa của $h_S$, thứ tư dùng $\lvert h^*_B\rvert\le B$. Biến cố không phụ thuộc $B$, nên cận đúng đồng thời cho mọi $B$.

**(c) Số.** Với $\ln40\approx3{,}689$,
$$
\begin{aligned}
2\sqrt{\tfrac{100+3{,}689}{2\cdot10^4}}&\approx2\cdot0{,}0720\\
&\approx0{,}1440 .
\end{aligned}
$$
ERM trên $\mathcal H_B$ ($\lvert\mathcal H_B\rvert\le2^{100}$, $B$ chọn trước) có cận $2\sqrt{(100\ln2+\ln40)/(2\cdot10^4)}\approx0{,}1208$.

**Kiểm tra lại.** Với $\lvert h\rvert\ln2$ thay cho $\lvert h\rvert$ trong $\Phi$, cùng chuỗi cho $0{,}1208$ đồng thời cho mọi $B$ (Định lý 04.11(b), $\tau=0$).
:::

### Bài tập 04.11 (Hợp nhiều khoảng: học được không đều nhưng không học được PAC; UML Bài tập 7.5, ý 3–5)

**Mức độ:** chứng minh (phần (d) là phần thử thách). **Mục tiêu:** mục tiêu học tập 4; học không đều so với học PAC.

::: exercise Bài tập 04.11
Cho $\mathcal X=[0,1]$ với σ-đại số Borel và hàm lỗi 0–1. Với $n\ge1$, lớp $\mathcal H_n$ gồm các hàm $\mathbb 1[x\in I_1\cup\cdots\cup I_n]$, trong đó mỗi $I_i$ là một khoảng đóng $[u_i,v_i]\subseteq[0,1]$ hoặc tập rỗng. Đặt $\mathcal H=\bigcup_n\mathcal H_n$. Ý 1–2 của UML Bài tập 7.5 là Định lý 04.16(a) nên không dùng; (a)–(c) là ý 4; (d) gộp ý 3 và 5 cho hàm phân lớp đo được.

**(a)** Chứng minh chiều VC của $\mathcal H_n$ bằng $2n$.

**(b)** Chứng minh $\mathcal H$ có chiều VC vô hạn và không học được PAC.

**(c)** Chứng minh $\mathcal H$ học được không đều bằng Hệ quả 04.15, kể cả điều kiện (M). Nêu hai điểm khác với Ví dụ 04.11.

**(d)** (Thử thách.) Cho $\mathcal X$ vô hạn với một σ-đại số chứa mọi tập một điểm, và $\mathcal M_{\mathcal X}$ là lớp mọi hàm phân lớp đo được. Chứng minh $\mathcal M_{\mathcal X}$ không học được không đều. Được dùng Định lý 04.16(a).
:::

::: hint Gợi ý 1
Phần (a). Trên $x_1<\cdots<x_N$, một cách gán nhãn thực hiện được trong $\mathcal H_n$ khi và chỉ khi các nhãn $1$ tạo thành không quá $n$ khối điểm liên tiếp (Bài tập 03.2(b) là trường hợp $n=2$).
:::

::: hint Gợi ý 2
Phần (c). Xấp xỉ đầu mút bằng số hữu tỉ, từ ngoài vào. Phần (d). Theo Định lý 04.16(a), $\mathcal M_{\mathcal X}=\bigcup_k\mathcal H_k$ với chiều VC $d_k<\infty$. Chọn các tập hữu hạn rời nhau $C_k$ có $d_k+1$ phần tử.
:::

::: hint Gợi ý 3
Phần (d). Trên mỗi $C_k$, lấy một cách gán nhãn $f_k$ không thực hiện được trong $\mathcal H_k$; ghép các $f_k$ và gán $0$ ở các điểm còn lại.
:::

::: solution Lời giải Bài tập 04.11
**(a) Chiều VC của $\mathcal H_n$.**

**Bước 1: số khối.** Xét $x_1<\cdots<x_N$ và một cách gán nhãn có $b$ khối nhãn $1$ liên tiếp. Nếu $b\le n$, mỗi khối $\{x_i,\ldots,x_{i'}\}$ là giao của tập điểm với $[x_i,x_{i'}]$, và các khoảng thừa là tập rỗng; cách gán nhãn thực hiện được. Đảo lại, giả sử cách gán nhãn thực hiện được. Mỗi khoảng không chứa điểm nhãn $0$, và giao của nó với tập điểm là một dãy điểm liên tiếp, nên nó chứa điểm của nhiều nhất một khối; cần ít nhất $b$ khoảng, tức $b\le n$.

**Bước 2: cận dưới.** Với $N=2n$, $b$ khối cần ít nhất $2b-1$ điểm, nên $b\le n$; mọi cách gán nhãn thực hiện được và $2n$ điểm phân biệt bất kì bị tách trọn.

**Bước 3: cận trên.** Với $N=2n+1$ điểm bất kì, cách gán nhãn $(1,0,1,\ldots,0,1)$ có $n+1$ khối, nên không thực hiện được. Vậy chiều VC bằng $2n$.

**(b) Lớp hợp.** Một tập $N$ điểm bị $\mathcal H_{\lceil N/2\rceil}\subseteq\mathcal H$ tách trọn theo (a), nên $\mathcal H$ có chiều VC vô hạn. Theo Định lý 03.17(a), $\mathcal H$ không học được PAC, và theo Nhận xét 01.26 cũng không học được PAC bất khả tri.

**(c) Học được không đều.**

**Bước 1: điều kiện (M).** Lấy lớp con các hàm có đầu mút hữu tỉ. Với $[u,v]$, chọn các số hữu tỉ $u^{(t)}\le u$, $u^{(t)}\uparrow u$ và $v^{(t)}\ge v$, $v^{(t)}\downarrow v$ trong $[0,1]$. Điểm $x\in[u,v]$ luôn thuộc $[u^{(t)},v^{(t)}]$; điểm $x\notin[u,v]$ nằm ngoài $[u^{(t)},v^{(t)}]$ khi $t$ đủ lớn. Hàm chỉ thị của một hợp là giá trị lớn nhất của hữu hạn hàm chỉ thị, nên cũng hội tụ theo từng điểm.

**Bước 2: áp dụng Hệ quả 04.15.** Danh sách $\mathcal H_n$ đếm được, cố định trước mẫu; $d_n=2n$, (M) thỏa; lấy $q_n=6/(\pi^2n^2)$. Với một cách chọn nghiệm đo được, Hệ quả 04.15(a) cho $A_{\mathrm{SRM}}$ là thuật toán học không đều cho $\mathcal H$, với $k(h)$ là số khoảng nhỏ nhất cần để viết $h$. Cỡ mẫu đủ $M(\epsilon,\delta,h)$ tăng theo $k(h)$ và không bị chặn trên $\mathcal H$. Điều này chưa loại trừ một cỡ mẫu chung; theo (b), $\mathcal H$ không học được PAC (Định lý 03.17(a)), nên không thuật toán nào có cỡ mẫu chung như Định nghĩa 01.25 đòi.

**Bước 3: khác Ví dụ 04.11.** Lớp ở đó đếm được và được chia thành các lớp một phần tử với bán kính của Định lý 02.14(a); ở đây mỗi $\mathcal H_n$ không đếm được, và số hạng phạt là bán kính VC $\rho_m$, cần (M).

**(d) Lớp mọi hàm đo được.**

**Bước 1: giả sử ngược lại.** Nếu $\mathcal M_{\mathcal X}$ học được không đều, theo Định lý 04.16(a), $\mathcal M_{\mathcal X}=\bigcup_k\mathcal H_k$ với $d_k<\infty$.

**Bước 2: các tập rời nhau.** Vì $\mathcal X$ vô hạn, ta chọn lần lượt các tập hữu hạn rời nhau $C_1,C_2,\ldots$ với $\lvert C_k\rvert=d_k+1$; phần còn lại sau mỗi bước vẫn vô hạn.

**Bước 3: các cách gán nhãn.** $\lvert C_k\rvert>d_k$, nên $\mathcal H_k$ không tách trọn $C_k$: có $f_k:C_k\to\{0,1\}$ không trùng với thu hẹp lên $C_k$ của bất kì $h\in\mathcal H_k$.

**Bước 4: ghép.** Đặt $f=f_k$ trên $C_k$ và $f=0$ ngoài $\bigcup_kC_k$. Tập $\{f=1\}$ là hợp đếm được của các tập một điểm, nên đo được và $f\in\mathcal M_{\mathcal X}$. Với mọi $k$, thu hẹp của $f$ lên $C_k$ là $f_k$, nên $f\notin\mathcal H_k$. Vậy $f\notin\bigcup_k\mathcal H_k=\mathcal M_{\mathcal X}$, mâu thuẫn.

Với $\mathcal X=[0,1]$, lớp $\mathcal M_{[0,1]}$ của Ví dụ 03.6 không học được không đều.

**Kiểm tra lại.** Với $n=2$, (a) cho chiều VC $4$, khớp Bài tập 03.2(b).
:::

### Bài tập 04.12 (Thất bại của kiểm tra chéo để lại một quan sát; UML Bài tập 11.1)

**Mức độ:** tính toán, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 5; không chệch nhưng không tập trung.

::: exercise Bài tập 04.12
Nhãn $Y\sim\mathrm{Bernoulli}(\tfrac12)$ độc lập với đầu vào, hàm lỗi 0–1, $S=(Z_1,\ldots,Z_m)\sim D^m$ với $m\ge2$. Thuật toán $A$ xét *tính chẵn lẻ* (parity) $P(S)=\big(\sum_iY_i\big)\bmod2$ của các nhãn trong mẫu và trả về hàm hằng $P(S)$. Ước lượng *để lại một quan sát* (leave-one-out) là
$$
L_{\mathrm{loo}}(S)=\frac1m\sum_{i=1}^m\ell\big(A(S^{-i}),Z_i\big),
$$
với $S^{-i}$ là mẫu bỏ quan sát thứ $i$.

**(a)** Tính $L_D(A(S))$ và chứng minh $\lvert L_{\mathrm{loo}}(S)-L_D(A(S))\rvert=\tfrac12$ trên mọi mẫu.

**(b)** Chứng minh mỗi số hạng $\ell(A(S^{-i}),Z_i)$ có kì vọng bằng $\mathbb E\,L_D(A(S^{-i}))$. Tính $\operatorname{Var}(L_{\mathrm{loo}})$, so với phương sai của trung bình $m$ số hạng độc lập cùng phân bố, và giải thích vì sao Hệ quả 04.17 không áp dụng.
:::

::: hint Gợi ý 1
Tính chẵn lẻ của $S^{-i}$ là $P(S)\oplus Y_i$, với $\oplus$ là phép cộng theo modulo $2$.
:::

::: hint Gợi ý 2
So sánh $P(S)\oplus Y_i$ với $Y_i$ trong hai trường hợp $Y_i=0$ và $Y_i=1$.
:::

::: solution Lời giải Bài tập 04.12
**(a) Độ lệch luôn bằng $\tfrac12$.**

**Bước 1: rủi ro thật.** Một hàm hằng $c\in\{0,1\}$ sai khi $Y\ne c$, với xác suất $\tfrac12$, nên $L_D(A(S))=\tfrac12$ trên mọi mẫu.

**Bước 2: từng số hạng.** Bỏ $Z_i$ làm tính chẵn lẻ đổi đúng khi $Y_i=1$, nên $A(S^{-i})$ là hàm hằng $P(S)\oplus Y_i$. Hàm này sai trên $Z_i$ khi và chỉ khi $P(S)\oplus Y_i\ne Y_i$, tức khi $P(S)=1$.

**Bước 3: ước lượng.** Mọi số hạng bằng $\mathbb 1[P(S)=1]$, nên $L_{\mathrm{loo}}(S)=P(S)\in\{0,1\}$ và
$$
\begin{aligned}
&\lvert L_{\mathrm{loo}}(S)-L_D(A(S))\rvert\\
&=\lvert P(S)-\tfrac12\rvert=\tfrac12 .
\end{aligned}
$$

**(b) Không chệch nhưng không tập trung.**

**Bước 1: kì vọng.** $Z_i$ độc lập với $S^{-i}$, nên kì vọng có điều kiện của $\ell(A(S^{-i}),Z_i)$ khi biết $S^{-i}$ là $L_D(A(S^{-i}))$; lấy kì vọng theo $S^{-i}$. Ở đây cả hai vế bằng $\tfrac12$, vì $P(S)$ có phân bố $\mathrm{Bernoulli}(\tfrac12)$.

**Bước 2: phương sai.** $L_{\mathrm{loo}}=P(S)$, nên $\operatorname{Var}(L_{\mathrm{loo}})=\tfrac14$ với mọi $m$. Trung bình của $m$ số hạng độc lập cùng phân bố $\mathrm{Bernoulli}(\tfrac12)$ có phương sai $\tfrac1{4m}$.

**Bước 3: giả thiết hỏng.** Hệ quả 04.17 cần mẫu xác thực độc lập với hàm được đánh giá (T7). Ở đây $Z_i$ nằm trong dữ liệu huấn luyện của mọi số hạng khác, các số hạng bằng nhau, nên không có tập trung (Nhận xét 04.18).

**Kiểm tra lại.** Nhãn $(1,1,0)$: $P(S)=0$; ba mẫu bỏ một quan sát có tính chẵn lẻ $1,1,0$, dự đoán đúng cả ba, nên $L_{\mathrm{loo}}=0$.
:::

### Bài tập 04.13 (ERM trên hợp các lớp so với chia huấn luyện–xác thực; UML Bài tập 11.2)

**Mức độ:** tính toán, khái niệm. **Mục tiêu:** mục tiêu học tập 3, 5; ERM trên hợp so với xác thực.

::: exercise Bài tập 04.13
Cho $k_{\max}$ lớp hữu hạn $\mathcal H_1,\ldots,\mathcal H_{k_{\max}}$ cố định trước mẫu, không nhất thiết lồng nhau; hàm lỗi 0–1; $m$ quan sát độc lập cùng phân bố. Đặt $\mathcal H=\bigcup_k\mathcal H_k$. Để so sánh bằng số, học phần thêm giả thiết $\lvert\mathcal H_k\rvert=2^k$, không có trong đề UML.

- **Cách 1.** ERM trên $\mathcal H$ với cả $m$ quan sát.
- **Cách 2.** Chia mẫu thành $(1-\alpha)m$ quan sát huấn luyện và mẫu xác thực $V$ cỡ $m_v=\alpha m$. Với mỗi $k$, $\hat h_k$ là nghiệm ERM trên $\mathcal H_k$ tính từ phần huấn luyện; $\hat g$ làm $L_V$ nhỏ nhất trong $\hat h_1,\ldots,\hat h_{k_{\max}}$.

**(a)** Chứng minh rằng với xác suất ít nhất $1-\delta$, cách 1 cho
$$
\begin{aligned}
L_D(\hat h)&\le\min_{h\in\mathcal H}L_D(h)\\
&\quad+2\sqrt{\tfrac{\ln(2^{k_{\max}+2}/\delta)}{2m}} .
\end{aligned}
$$

**(b)** Cố định trước mẫu một chỉ số $j$. Chứng minh rằng với xác suất ít nhất $1-\delta$, cách 2 cho
$$
\begin{aligned}
L_D(\hat g)&\le\min_{h\in\mathcal H_j}L_D(h)\\
&\quad+2\sqrt{\tfrac{\ln(2^{j+2}/\delta)}{2(1-\alpha)m}}\\
&\quad+2\sqrt{\tfrac{\ln(4k_{\max}/\delta)}{2\alpha m}} .
\end{aligned}
$$

**(c)** Lấy $m=10^4$, $\alpha=0{,}2$, $k_{\max}=10,100,1000$. Tính hai cận khi giả thuyết tốt nhất của $\mathcal H$ nằm trong $\mathcal H_1$ ($j=1$), và khi nó chỉ nằm trong $\mathcal H_{k_{\max}}$ ($j=k_{\max}$). Mô tả các trường hợp mỗi cách cho cận nhỏ hơn.
:::

::: hint Gợi ý 1
Phần (a). $\lvert\mathcal H\rvert\le\sum_k2^k<2^{k_{\max}+1}$; dùng Hệ quả 02.16(a). Phần (b). Dùng $\delta/2$ cho phần huấn luyện trên riêng $\mathcal H_j$ và $\delta/2$ cho bước chọn.
:::

::: hint Gợi ý 2
Phần (b). Bước chọn là Hệ quả 04.17(a) với $K=k_{\max}$ ứng viên; (T7) thỏa vì $V$ tách khỏi phần huấn luyện. Lớp $\mathcal H_j$ được cố định trước mẫu, nên phần huấn luyện không cần chia $\delta$ cho các lớp.
:::

::: solution Lời giải Bài tập 04.13
**(a) Cách 1.** $\mathcal H$ hữu hạn, cố định trước mẫu và $\lvert\mathcal H\rvert<2^{k_{\max}+1}$, nên Hệ quả 02.16(a) cho cận với $r_m=\sqrt{\ln(2\lvert\mathcal H\rvert/\delta)/(2m)}\le\sqrt{\ln(2^{k_{\max}+2}/\delta)/(2m)}$.

**(b) Cách 2.**

**Bước 1: phần huấn luyện.** Lớp $\mathcal H_j$ thỏa (T4) với $2^j$ phần tử. Theo Hệ quả 02.16(a) tại $\delta/2$ trên $(1-\alpha)m$ quan sát, với xác suất ít nhất $1-\delta/2$,
$$
\begin{aligned}
L_D(\hat h_j)&\le\min_{h\in\mathcal H_j}L_D(h)\\
&\quad+2\sqrt{\tfrac{\ln(2^{j+2}/\delta)}{2(1-\alpha)m}},
\end{aligned}
$$
vì $2\cdot2^j/(\delta/2)=2^{j+2}/\delta$.

**Bước 2: bước chọn.** Các ứng viên là hàm của phần huấn luyện, và $V$ độc lập với phần đó, nên (T7) thỏa. Theo Hệ quả 04.17(a) tại $\delta/2$ với $K=k_{\max}$, với xác suất ít nhất $1-\delta/2$,
$$
\begin{aligned}
L_D(\hat g)&\le\min_kL_D(\hat h_k)\\
&\quad+2\sqrt{\tfrac{\ln(4k_{\max}/\delta)}{2\alpha m}} .
\end{aligned}
$$

**Bước 3: ghép.** Theo bất đẳng thức hợp, hai biến cố cùng xảy ra với xác suất ít nhất $1-\delta$. Thay $\min_kL_D(\hat h_k)\le L_D(\hat h_j)$ và Bước 1 vào Bước 2, ta được cận cần chứng minh.

**(c) Số.**

**Bước 1: ba thành phần.** Với $\delta=0{,}05$:

- **Cách 1.** $2\sqrt{\ln(2^{k_{\max}+2}/0{,}05)/20\,000}$.
- **Phần huấn luyện của cách 2, $j=1$.** $2\sqrt{\ln160/16\,000}\approx0{,}0356$.
- **Bước chọn.** $2\sqrt{\ln(80k_{\max})/4000}$, tức $0{,}0818$; $0{,}0948$; $0{,}1063$ tại $k_{\max}=10,100,1000$.

**Bước 2: bảng.** Các cận cộng thêm vào $\min_{h\in\mathcal H}L_D(h)$; cột cuối là cách 2 với $j=1$:

| $k_{\max}$ | cách 1 | cách 2 |
|---|---|---|
| $10$ | $0{,}0476$ | $0{,}1174$ |
| $100$ | $0{,}1214$ | $0{,}1304$ |
| $1000$ | $0{,}3735$ | $0{,}1419$ |

Với $k_{\max}=1000$, cách 1: $1002\ln2+\ln20\approx697{,}53$ và $2\sqrt{697{,}53/20\,000}\approx0{,}3735$.

**Bước 3: khi nào cách 2 tốt hơn.** Cách 1 trả $\ln\lvert\mathcal H\rvert\approx k_{\max}\ln2$, cách 2 chỉ trả $\ln(4k_{\max}/\delta)$ ở bước chọn. Với $j=1$: tại $k_{\max}=118$, cách 1 cho $0{,}13128$ và cách 2 cho $0{,}13129$; tại $k_{\max}=119$, $0{,}13181$ và $0{,}13133$. Vậy cách 2 cho cận nhỏ hơn từ $k_{\max}=119$.

**Bước 4: khi nào cách 1 tốt hơn.** Khi $k_{\max}$ nhỏ, hoặc khi giả thuyết tốt nhất chỉ nằm trong lớp lớn nhất. Khi $j=k_{\max}$, cả hai cách trả khoảng $k_{\max}\ln2$, nhưng cách 2 dùng $8000$ quan sát và thêm bước chọn; cận của nó là $0{,}1349$; $0{,}2305$; $0{,}5238$ tại $k_{\max}=10,100,1000$, đều lớn hơn cách 1.

**Kiểm tra lại.** Với $k_{\max}=1$, cách 2 cho $0{,}0356+2\sqrt{\ln80/4000}\approx0{,}1018$, còn cách 1 cho $2\sqrt{\ln160/20\,000}\approx0{,}0319$.
:::
