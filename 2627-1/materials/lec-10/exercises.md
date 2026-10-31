# Bài tập Bài 10 — Gradient chính sách và học liên tục

Định nghĩa, kết quả và ví dụ được dẫn theo số hiệu của ghi chú Bài 10 và của các ghi chú Bài 01–09. Kí hiệu theo bảng kí hiệu chung và §2 của ghi chú, gồm:

- **Phần A (§4–§6).** Quá trình quyết định Markov (Markov decision process, MDP) tầm nhìn hữu hạn $(\mathcal S,\mathcal A,\mu_0,P,r,H)$ (Định nghĩa 10.1); tác tử (agent), lượt (episode), chính sách (policy) $\pi_\theta$; gradient log (score function) $\nabla_\theta\ln\pi_\theta$; quỹ đạo $\tau$, tổng phần thưởng (return) $R(\tau)$, phần thưởng $r_t$ ở bước $t$, mục tiêu $J(\theta)$ (Định nghĩa 10.2); ước lượng $\hat g$ của Định lý 10.4; tổng phần thưởng từ bước $t$ (reward-to-go) $R_{\ge t}$, lịch sử $\mathcal F_t$, giá trị nền (baseline) $b_t(\mathcal F_t)$ (§6).
- **Phần B (§7–§9).** Số nhiệm vụ (task) $K$, ngân sách bộ nhớ $M$, tham số $w^{(k)}$ sau nhiệm vụ $k$ (Định nghĩa 10.10); ma trận đánh giá (evaluation matrix) $\mathrm{acc}_{k,i}$ và $\mathrm{acc}^\circ_i$, chuyển đổi ngược (backward transfer), chuyển đổi xuôi (forward transfer), độ quên (forgetting measure) (Định nghĩa 10.11); hệ số chính quy hóa $\lambda$, ma trận trọng số $\Omega$, tỉ lệ phát lại $\alpha$, rủi ro trên bộ đệm $L_{\mathrm{buf}}$ (Định nghĩa 10.12); hối tiếc (regret) $\mathrm{Regret}_T(u)$ với điểm so sánh $u$ (Định nghĩa 10.15).

Bài toán bandit hai hành động với chính sách sigmoid là bài toán của Ví dụ 10.1: $\pi_\theta(1)=1/(1+e^{-\theta})$, $\pi_\theta(0)=1-\pi_\theta(1)$, $\theta\in\mathbb R$, một lượt gồm một hành động $A\in\{0,1\}$. Chính sách bảng là chính sách $\pi_\theta(1\mid s)=1/(1+e^{-\theta_s})$ của đoạn sau Định nghĩa 10.1. Logarit là logarit tự nhiên.

Bảy bài đầu là bài gốc của học phần; Bài tập 10.6 là bài thiết kế thí nghiệm, có phần tính trên số đã chạy. Hai bài sau chọn từ mục bài tập §21.7 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* (Shalev-Shwartz và Ben-David, 2014; viết tắt UML); Bài tập 10.9 là bài tùy chọn.

## Bài tập gốc

### Bài tập 10.1 (Thuật toán REINFORCE cho bài toán bandit hai hành động)

**Mức độ:** tính toán, chứng minh, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 2 và 3; kiểm ước lượng gradient log bằng đạo hàm trực tiếp, kiểm điều kiện đổi chỗ đạo hàm và kì vọng, viết phương sai thành hàm của giá trị nền, và đọc dấu của một bước cập nhật.

::: exercise Bài tập 10.1
Xét bài toán bandit hai hành động với chính sách sigmoid, phần thưởng tất định $r(1)=4$, $r(0)=0$, tại $\theta=-\ln3$.

**(a)** Tính $\pi_\theta(1)$, $J(\theta)$ và $J'(\theta)$ bằng đạo hàm trực tiếp.

**(b)** Viết ước lượng $\hat g$ của Định lý 10.4 cho một lượt. Liệt kê các giá trị của nó cùng xác suất, kiểm rằng kì vọng bằng $J'(\theta)$, và tính phương sai.

**(c)** Với hằng số $b$, đặt $\hat g_b=\big(r(A)-b\big)\big(A-\pi_\theta(1)\big)$. Chứng minh rằng
$$
\begin{aligned}
&\operatorname{Var}(\hat g_b)\\
&=\operatorname{Var}(\hat g_{b^*})\\
&\quad+\pi(1-\pi)(b-b^*)^2,
\end{aligned}
$$
với $\pi=\pi_\theta(1)$ và $b^*=(1-\pi)\,r(1)+\pi\,r(0)$. Tính $b^*$, $\operatorname{Var}(\hat g_{b^*})$ và phương sai khi $b=J(\theta)$. Giải thích vì sao $b^*\ne J(\theta)$.

**(d)** Một bước của Thuật toán 10.6 với giá trị nền $b$ đặt $\theta'=\theta+\eta\,\hat g_b$, với $\eta>0$. Với mỗi $b\in\{0,\,J(\theta),\,5\}$, tính xác suất để $\theta'<\theta$. So sánh hai giá trị nền $J(\theta)$ và $5$.

**(e)** Tính $J''(\theta)$ tại điểm này, rồi xác định tập các $\theta\in\mathbb R$ trên đó $J$ lõm.

**(f)** Thay bài toán bandit bằng một hành động liên tục $A>0$ có mật độ $p_\theta(a)=\theta e^{-\theta a}$, $\theta>0$, và phần thưởng $r(a)=\mathbb 1[a\le1]$. Kiểm ba điều kiện của Nhận xét 10.5. Tại $\theta=1$, tính $J'(1)$ bằng đạo hàm trực tiếp và bằng $\mathbb E\big[r(A)\,\partial_\theta\ln p_\theta(A)\big]$. Điều kiện nào phân biệt bài này với Ví dụ 10.3?
:::

::: hint Gợi ý 1
Phần (a), (e). Dùng câu ôn nhanh 2 của ghi chú cho đạo hàm của $\pi_\theta(1)$. Phần (b). Gradient log bằng $A-\pi_\theta(1)$ (Ví dụ 10.4, Bước 1). Phần (c). Phương sai là một hàm bậc hai của $b$. Phần (f). Giá $(0,\infty)$ của mật độ không phụ thuộc $\theta$.
:::

::: hint Gợi ý 2
Phần (c). Kì vọng của $\hat g_b$ không phụ thuộc $b$ (Hệ quả 10.8), nên chỉ cần khai triển $\mathbb E\hat g_b^2$ theo hai giá trị của $A$ rồi đặt $b=b^*+(b-b^*)$. Phần (d). Vì $\eta>0$, dấu của $\theta'-\theta$ là dấu của $\hat g_b$. Phần (e). Đạo hàm của $\pi(1-\pi)$ theo $\theta$ là $\pi(1-\pi)(1-2\pi)$. Phần (f). Trên $(\theta_0/2,2\theta_0)$, $\lvert\partial_\theta p_\theta(a)\rvert\le(1+2\theta_0a)e^{-\theta_0a/2}$.
:::

::: solution Lời giải Bài tập 10.1
**(a) Đạo hàm trực tiếp.**

**Bước 1: xác suất.** Vì $e^{-\theta}=e^{\ln3}=3$, ta có $\pi_\theta(1)=1/(1+3)=\tfrac14$.

**Bước 2: mục tiêu.** $J(\theta)=4\,\pi_\theta(1)+0\cdot\pi_\theta(0)=4\cdot\tfrac14=1$.

**Bước 3: đạo hàm.** Theo câu ôn nhanh 2, $\frac{d}{d\theta}\pi_\theta(1)=\pi_\theta(1)\big(1-\pi_\theta(1)\big)$, nên
$$
\begin{aligned}
J'(\theta)&=4\,\pi_\theta(1)\big(1-\pi_\theta(1)\big)\\
&=4\cdot\tfrac14\cdot\tfrac34=\tfrac34 .
\end{aligned}
$$

**(b) Ước lượng gradient log.**

**Bước 1: công thức.** Với $H=1$, $R(\tau)=r(A)$ và gradient log bằng $A-\tfrac14$, nên $\hat g=r(A)\big(A-\tfrac14\big)$.

**Bước 2: hai giá trị.**

- $A=1$ (xác suất $\tfrac14$): $\hat g=4\cdot\tfrac34=3$;
- $A=0$ (xác suất $\tfrac34$): $\hat g=0\cdot(-\tfrac14)=0$.

**Bước 3: kì vọng.** $\mathbb E\hat g=\tfrac14\cdot3+\tfrac34\cdot0=\tfrac34$, đúng $J'(\theta)$ của (a).

**Bước 4: phương sai.**
$$
\begin{aligned}
\operatorname{Var}(\hat g)&=\tfrac14\cdot3^2-\big(\tfrac34\big)^2\\
&=\tfrac{36}{16}-\tfrac9{16}=\tfrac{27}{16}.
\end{aligned}
$$

**(c) Phương sai theo giá trị nền.**

**Bước 1: mô-men bậc hai.** Với $A=1$, $\hat g_b=(r(1)-b)(1-\pi)$; với $A=0$, $\hat g_b=-(r(0)-b)\pi$. Do đó
$$
\begin{aligned}
\mathbb E\hat g_b^2&=\pi(1-\pi)^2\big(r(1)-b\big)^2\\
&\quad+(1-\pi)\pi^2\big(r(0)-b\big)^2 .
\end{aligned}
$$
Theo Hệ quả 10.8, $\mathbb E\hat g_b=J'(\theta)$ với mọi $b$, nên $\operatorname{Var}(\hat g_b)=\mathbb E\hat g_b^2-J'(\theta)^2$ chỉ phụ thuộc $b$ qua $\mathbb E\hat g_b^2$.

**Bước 2: thay $b=b^*+d$.** Đặt $d=b-b^*$ và $\Delta r=r(1)-r(0)$. Theo định nghĩa của $b^*$, $r(1)-b^*=\pi\Delta r$ và $r(0)-b^*=-(1-\pi)\Delta r$. Khai triển hai bình phương ở Bước 1 với $r(1)-b=\pi\Delta r-d$ và $r(0)-b=-(1-\pi)\Delta r-d$, ta được ba nhóm số hạng.

- Số hạng không chứa $d$: $\pi(1-\pi)^2\pi^2\Delta r^2+(1-\pi)\pi^2(1-\pi)^2\Delta r^2$, tức $\mathbb E\hat g_{b^*}^2$.
- Số hạng bậc nhất theo $d$: $-2d\,\pi(1-\pi)^2\pi\Delta r+2d\,(1-\pi)\pi^2(1-\pi)\Delta r=0$.
- Số hạng bậc hai: $d^2\big(\pi(1-\pi)^2+(1-\pi)\pi^2\big)=d^2\pi(1-\pi)$.

Trừ $J'(\theta)^2$ ở cả hai vế, ta được đẳng thức của đề.

**Bước 3: giá trị nền tốt nhất.** Với $\pi=\tfrac14$: $b^*=\tfrac34\cdot4+\tfrac14\cdot0=3$. Hai giá trị của $\hat g_3$ là $(4-3)\cdot\tfrac34=\tfrac34$ và $(0-3)(-\tfrac14)=\tfrac34$, nên $\operatorname{Var}(\hat g_{b^*})=0$.

**Bước 4: giá trị nền $b=J(\theta)=1$.** Theo đẳng thức của đề,
$$
\begin{aligned}
\operatorname{Var}(\hat g_1)&=0+\tfrac14\cdot\tfrac34\cdot(1-3)^2\\
&=\tfrac3{16}\cdot4=\tfrac34 .
\end{aligned}
$$
Giá trị nền $J$ giảm phương sai từ $\tfrac{27}{16}$ xuống $\tfrac34$.

**Bước 5: vì sao $b^*\ne J$.** $J=\pi\,r(1)+(1-\pi)\,r(0)$ gán cho $r(1)$ trọng số $\pi$. Theo Bước 1, $b^*$ gán cho $r(1)$, $r(0)$ trọng số tỉ lệ với $\pi(1-\pi)^2$ và $(1-\pi)\pi^2$, tức xác suất của hành động nhân bình phương gradient log; hành động hiếm hơn có gradient log lớn hơn, nên phần thưởng của nó nặng hơn trong $b^*$. Hai giá trị nền trùng nhau khi và chỉ khi $\pi=\tfrac12$ hoặc $r(1)=r(0)$.

**(d) Dấu của một bước.**

**Bước 1: $b=0$.** Hai giá trị của $\hat g_0$ là $3$ và $0$ (phần (b)), đều không âm, nên $\Pr(\theta'<\theta)=0$. Với xác suất $\tfrac34$, bước cập nhật bằng $0$.

**Bước 2: $b=J(\theta)=1$.** Hai giá trị $(4-1)\cdot\tfrac34=\tfrac94$ và $(0-1)(-\tfrac14)=\tfrac14$ đều dương, nên $\Pr(\theta'<\theta)=0$.

**Bước 3: $b=5$.** Với $A=1$: $\hat g_5=(4-5)\cdot\tfrac34=-\tfrac34$; với $A=0$: $\hat g_5=(0-5)(-\tfrac14)=\tfrac54$. Do đó $\Pr(\theta'<\theta)=\Pr(A=1)=\tfrac14$.

**Bước 4: so sánh.** Theo đẳng thức ở (c), $\operatorname{Var}(\hat g_5)=\tfrac3{16}(5-3)^2=\tfrac34$, bằng phương sai khi $b=1$, vì $1$ và $5$ cách $b^*=3$ cùng một khoảng. Hai ước lượng có cùng kì vọng và cùng phương sai, nhưng với $b=5$, bước cập nhật ngược dấu với $J'$ đúng khi tác tử chọn hành động tốt hơn.

**(e) Tính lõm.**

**Bước 1: đạo hàm bậc hai.** Từ (a), $J'(\theta)=4\pi(1-\pi)$ với $\pi=\pi_\theta(1)$. Vì $\frac{d}{d\theta}\pi=\pi(1-\pi)$, đạo hàm của $\pi(1-\pi)$ là $(1-2\pi)\,\pi(1-\pi)$, nên
$$
\begin{aligned}
J''(\theta)&=4\pi(1-\pi)(1-2\pi)\\
&=4\cdot\tfrac3{16}\cdot\tfrac12=\tfrac38>0 .
\end{aligned}
$$

**Bước 2: miền lõm.** $4\pi(1-\pi)>0$ với mọi $\theta$, nên $J''(\theta)\le0$ khi và chỉ khi $\pi_\theta(1)\ge\tfrac12$, tức $\theta\ge0$. Do đó $J$ lõm trên $[0,\infty)$ và không lõm trên mọi khoảng chứa một điểm $\theta<0$. Điểm $\theta=-\ln3$ nằm ngoài miền lõm.

**(f) Một hành động liên tục.**

**Bước 1: ba điều kiện của Nhận xét 10.5.** Phần thưởng thuộc $\{0,1\}$, nên bị chặn.

- **Mật độ.** $p_\theta$ là mật độ theo độ đo Lebesgue trên $(0,\infty)$; độ đo nền và giá $(0,\infty)$ không phụ thuộc $\theta$.
- **Khả vi.** $\partial_\theta p_\theta(a)=e^{-\theta a}(1-\theta a)$, liên tục theo $\theta$ với mọi $a$.
- **Hàm trội.** Cố định $\theta_0>0$ và lấy $U=(\theta_0/2,2\theta_0)$. Với $\theta\in U$, $\lvert1-\theta a\rvert\le1+2\theta_0a$ và $e^{-\theta a}\le e^{-\theta_0a/2}$. Vì $\lvert r\rvert\le1$, hàm $\Lambda(a)=(1+2\theta_0a)e^{-\theta_0a/2}$ là hàm trội, với $\int_0^\infty\Lambda=\frac2{\theta_0}+\frac8{\theta_0}=\frac{10}{\theta_0}<\infty$.

**Bước 2: đạo hàm trực tiếp.** $J(\theta)=\Pr(A\le1)=1-e^{-\theta}$, nên $J'(1)=e^{-1}\approx0{,}3679$.

**Bước 3: gradient log.** $\ln p_\theta(a)=\ln\theta-\theta a$, nên $\partial_\theta\ln p_\theta(a)=\frac1\theta-a$, bằng $1-a$ tại $\theta=1$. Tích phân từng phần cho $\int_0^1ae^{-a}\,da=1-2e^{-1}$, nên
$$
\begin{aligned}
&\mathbb E\big[\mathbb 1[A\le1](1-A)\big]\\
&=\textstyle\int_0^1(1-a)e^{-a}\,da\\
&=(1-e^{-1})-(1-2e^{-1})\\
&=e^{-1},
\end{aligned}
$$
đúng $J'(1)$, như Nhận xét 10.5 bảo đảm.

**Bước 4: so với Ví dụ 10.3.** Ở Ví dụ 10.3, giá $[0,\theta]$ di chuyển theo $\theta$, nên $\theta\mapsto p_\theta(a)$ nhảy tại $\theta=a$ và điều kiện khả vi không thỏa. Ở đây giá cố định và $p_\theta(a)$ khả vi liên tục theo $\theta$.

**Kiểm tra lại.** Với $r(1)=4$, $r(0)=0$, công thức $b^*=r(1)\big(1-\pi_\theta(1)\big)+r(0)\pi_\theta(1)$ của Ví dụ 10.8, Bước 3 cho $4\cdot\tfrac34=3$, khớp (c). Đẳng thức ở (c) với $b=0$ cho $\tfrac3{16}\cdot9=\tfrac{27}{16}$, khớp (b).
:::

### Bài tập 10.2 (Giá trị nền hợp lệ và giá trị nền gây chệch)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 3; tính độ chệch do một giá trị nền phụ thuộc hành động, chỉ ra rằng $r_0$ gây chệch ở bước $0$ nhưng hợp lệ ở bước $1$, và chứng minh công thức entropy của Nhận xét 10.9(i).

::: exercise Bài tập 10.2
Xét một MDP tầm nhìn hữu hạn và một chính sách như Định lý 10.4.

**(a)** Cho một hàm $\tilde b:\mathcal S\times\mathcal A\to\mathbb R$ bất kì và một bước $t$. Chứng minh rằng
$$
\begin{aligned}
&\mathbb E\big[\tilde b(S_t,A_t)\\
&\qquad\cdot\nabla\ln\pi_\theta(A_t\mid S_t)\big]\\
&=\mathbb E\Big[\textstyle\sum_{a\in\mathcal A}\tilde b(S_t,a)\\
&\qquad\cdot\nabla\pi_\theta(a\mid S_t)\Big].
\end{aligned}
$$
Với chính sách bảng trên $\mathcal A=\{0,1\}$, suy ra tọa độ $\theta_s$ của vế trái bằng
$$
\begin{aligned}
&\Pr(S_t=s)\,\pi_\theta(1\mid s)\\
&\quad\cdot\big(1-\pi_\theta(1\mid s)\big)\\
&\quad\cdot\big(\tilde b(s,1)-\tilde b(s,0)\big).
\end{aligned}
$$
Suy ra rằng khi $\Pr(S_t=s)>0$, giá trị nền $\tilde b(S_t,A_t)$ giữ tọa độ $\theta_s$ của kì vọng khi và chỉ khi $\tilde b(s,1)=\tilde b(s,0)$.

**(b)** Trên MDP hai bước của Ví dụ 10.2 tại $\theta=0$, dùng ước lượng của Mệnh đề 10.7(b) và trừ phần thưởng của bước đầu $r_0$ khỏi số hạng $t=0$, tức thay $R_{\ge0}$ bằng $R_{\ge0}-r_0$. Tính kì vọng của tọa độ $\theta_{s_0}$ bằng (a), rồi kiểm lại trên bảng tám quỹ đạo. So với $\partial J/\partial\theta_{s_0}=-0{,}025$ (Ví dụ 10.5).

**(c)** Cũng trên MDP đó, giữ nguyên số hạng $t=0$ và trừ $r_0$ khỏi số hạng $t=1$, tức thay $R_{\ge1}$ bằng $R_{\ge1}-r_0$. Giá trị nền này có hợp lệ theo Hệ quả 10.8 không? Tính kì vọng và phương sai của tọa độ $\theta_{s_1}$, rồi so với phương sai $\tfrac9{16}$ của ước lượng (ii) trong Ví dụ 10.10.

**(d)** Giá trị nền $b_\theta(S_t)$ dùng chung tham số với chính sách, và ước lượng được tính bằng gradient theo $\theta$ của $\big(R_{\ge t}-b_\theta(S_t)\big)\ln\pi_\theta(A_t\mid S_t)$. Chứng minh rằng số hạng thêm vào có kì vọng có điều kiện, khi biết $\mathcal F_t$, bằng $\nabla b_\theta(S_t)\cdot\mathrm H\big(\pi_\theta(\cdot\mid S_t)\big)$, với $\mathrm H$ là entropy (Định nghĩa 09.7). Tính kì vọng của ước lượng này cho bài toán bandit của Ví dụ 10.8 ($r(1)=3$, $r(0)=1$, $\theta=\ln3$) với $b_\theta=\theta$, và so với $J'(\ln3)=\tfrac38$.
:::

::: hint Gợi ý 1
Phần (a). Điều kiện hóa theo $\mathcal F_t$ như Bước 1 của chứng minh Mệnh đề 10.7; giá trị nền ở đây là một hàm của $A_t$, nên chưa đưa được ra ngoài. Phần (b). Áp dụng (a) với $t=0$ và $\tilde b(s,a)=r(s,a)$. Phần (d). Lấy đạo hàm của tích theo quy tắc nhân.
:::

::: hint Gợi ý 2
Phần (a). Với chính sách bảng, $\nabla\pi_\theta(1\mid s)=\pi_\theta(1\mid s)\big(1-\pi_\theta(1\mid s)\big)e_s$ và $\nabla\pi_\theta(0\mid s)=-\nabla\pi_\theta(1\mid s)$, với $e_s$ là véc-tơ đơn vị của tọa độ $\theta_s$. Phần (c). Kiểm xem $r_0$ có là hàm của $\mathcal F_1=(S_0,A_0,S_1)$ không. Phần (d). Khi biết $\mathcal F_t$, $\mathbb E\ln\pi_\theta(A_t\mid S_t)=-\mathrm H\big(\pi_\theta(\cdot\mid S_t)\big)$.
:::

::: solution Lời giải Bài tập 10.2
**(a) Giá trị nền phụ thuộc hành động.**

**Bước 1: kì vọng có điều kiện.** Khi biết $\mathcal F_t$, $A_t\sim\pi_\theta(\cdot\mid S_t)$ (§6). Lấy tổng trên các $a$ có $\pi_\theta(a\mid S_t)>0$:
$$
\begin{aligned}
&\mathbb E\big[\tilde b(S_t,A_t)\\
&\qquad\cdot\nabla\ln\pi_\theta(A_t\mid S_t)\,\big|\,\mathcal F_t\big]\\
&=\textstyle\sum_a\pi_\theta(a\mid S_t)\,\tilde b(S_t,a)\\
&\qquad\cdot\nabla\ln\pi_\theta(a\mid S_t)\\
&=\textstyle\sum_a\tilde b(S_t,a)\nabla\pi_\theta(a\mid S_t),
\end{aligned}
$$
trong đó đẳng thức thứ hai dùng Bổ đề 10.3(a). Các $a$ có $\pi_\theta(a\mid S_t)=0$ có $\nabla\pi_\theta(a\mid S_t)=0$, cũng theo Bổ đề 10.3(a), nên tổng lấy được trên cả $\mathcal A$.

**Bước 2: tính chất tháp.** Lấy kì vọng hai vế theo $\mathcal F_t$, ta được đẳng thức của đề.

**Bước 3: chính sách bảng.** $\pi_\theta(1\mid s)$ chỉ phụ thuộc $\theta_s$ và có đạo hàm $\pi_\theta(1\mid s)\big(1-\pi_\theta(1\mid s)\big)$ theo $\theta_s$ (câu ôn nhanh 2), còn $\pi_\theta(0\mid s)=1-\pi_\theta(1\mid s)$; do đó
$$
\begin{aligned}
&\textstyle\sum_a\tilde b(S_t,a)\nabla\pi_\theta(a\mid S_t)\\
&=\pi_\theta(1\mid S_t)\big(1-\pi_\theta(1\mid S_t)\big)\\
&\quad\cdot\big(\tilde b(S_t,1)-\tilde b(S_t,0)\big)\,e_{S_t}.
\end{aligned}
$$
Tọa độ $\theta_s$ khác $0$ chỉ khi $S_t=s$; lấy kì vọng, ta được công thức của đề.

**Bước 4: kết luận.** $\pi_\theta(1\mid s)\big(1-\pi_\theta(1\mid s)\big)>0$ với mọi $\theta$. Khi $\Pr(S_t=s)>0$, tọa độ $\theta_s$ bằng $0$ khi và chỉ khi $\tilde b(s,1)=\tilde b(s,0)$.

**(b) Phần thưởng của bước đầu trong số hạng $t=0$.**

**Bước 1: áp dụng (a).** $\tilde b(s_0,a)=r(s_0,a)$, nên $\tilde b(s_0,1)-\tilde b(s_0,0)=0-1=-1$. Với $\Pr(S_0=s_0)=1$ và $\pi_0(1\mid s_0)=\tfrac12$, số hạng trừ đi có kì vọng $1\cdot\tfrac14\cdot(-1)=-\tfrac14$.

**Bước 2: kì vọng của tọa độ $\theta_{s_0}$.** Vì $S_1\in\{s_1,s_2\}$, chỉ số hạng $t=0$ có tọa độ $\theta_{s_0}$ khác $0$; theo Mệnh đề 10.7(b) và Ví dụ 10.5, khi chưa trừ, nó có kì vọng $-0{,}025$. Trừ đi số hạng có kì vọng $-0{,}25$:
$$
-0{,}025-(-0{,}25)=0{,}225 .
$$

**Bước 3: kiểm trên bảng.** $R_{\ge0}-r_0=r_1$. Từ bảng của Ví dụ 10.2, Bước 1, $r_1=R(\tau)-r_0$, với $r_0=0$ khi $a_0=1$ và $r_0=1$ khi $a_0=0$. Nhân xác suất, $r_1$ và $a_0-\tfrac12$:
$$
\begin{aligned}
&\tfrac12(0{,}2\cdot3+0{,}2\cdot1\\
&\qquad+0{,}05\cdot1)\\
&-\tfrac12(0{,}05\cdot3+0{,}05\cdot1\\
&\qquad+0{,}2\cdot1)\\
&=0{,}425-0{,}2=0{,}225 .
\end{aligned}
$$

**Bước 4: ý nghĩa.** Kì vọng $0{,}225$ ngược dấu với $-0{,}025$. Phần thưởng $r_0=r(S_0,A_0)$ phụ thuộc $A_0$, nên nó không là hàm của $\mathcal F_0=(S_0)$ và vi phạm giả thiết của Hệ quả 10.8. Ước lượng này chỉ thấy phần thưởng ở bước sau, nơi hành động $1$ có lợi, và bỏ khoản mất $1$ ở bước đầu (Ví dụ 10.5, Kết luận).

**(c) Phần thưởng của bước đầu trong số hạng $t=1$.**

**Bước 1: tính hợp lệ.** $r_0=r(S_0,A_0)$ là hàm của $\mathcal F_1=(S_0,A_0,S_1)$, nên Hệ quả 10.8 áp dụng với $b_1(\mathcal F_1)=r_0$. Kì vọng của các tọa độ $\theta_{s_1}$, $\theta_{s_2}$ giữ nguyên $0{,}25$ và $-0{,}125$. Đây là trường hợp phần thưởng nhận trước bước $t$ của Nhận xét 10.9(ii).

**Bước 2: các giá trị của tọa độ $\theta_{s_1}$.** Tọa độ này bằng $(r_1-r_0)(a_1-\tfrac12)$ trên các quỹ đạo qua $s_1$ và bằng $0$ trên các quỹ đạo khác (xác suất $\tfrac12$). Trên quỹ đạo đầu tiên của bảng, nó bằng $(3-0)\cdot\tfrac12=1{,}5$.

| Quỹ đạo | Xác suất | Giá trị |
|---|---|---|
| $(s_0,1,s_1,1)$ | $0{,}2$ | $1{,}5$ |
| $(s_0,1,s_1,0)$ | $0{,}2$ | $-0{,}5$ |
| $(s_0,0,s_1,1)$ | $0{,}05$ | $1$ |
| $(s_0,0,s_1,0)$ | $0{,}05$ | $0$ |

**Bước 3: kì vọng và phương sai.** Kì vọng là $0{,}3-0{,}1+0{,}05+0=0{,}25$. Mô-men bậc hai là $0{,}2\cdot2{,}25+0{,}2\cdot0{,}25+0{,}05\cdot1=0{,}55$, nên phương sai là
$$
0{,}55-0{,}25^2=0{,}4875 .
$$

**Bước 4: so sánh.** Phương sai giảm từ $\tfrac9{16}=0{,}5625$ xuống $0{,}4875$. Cùng một đại lượng $r_0$ gây chệch ở (b) và hợp lệ ở đây. Hệ quả 10.8 so giá trị nền với lịch sử của bước mà nó được trừ: $r_0$ là hàm của $\mathcal F_1$ nhưng không là hàm của $\mathcal F_0$.

**(d) Giá trị nền có chung tham số.**

**Bước 1: quy tắc nhân.**
$$
\begin{aligned}
&\nabla\Big[\big(R_{\ge t}-b_\theta(S_t)\big)\\
&\qquad\cdot\ln\pi_\theta(A_t\mid S_t)\Big]\\
&=\big(R_{\ge t}-b_\theta(S_t)\big)\\
&\qquad\cdot\nabla\ln\pi_\theta(A_t\mid S_t)\\
&\quad-\nabla b_\theta(S_t)\,\ln\pi_\theta(A_t\mid S_t).
\end{aligned}
$$
Số hạng thứ nhất là số hạng của Hệ quả 10.8 với $b_t(\mathcal F_t)=b_\theta(S_t)$; số hạng thứ hai là số hạng thêm vào.

**Bước 2: kì vọng có điều kiện.** $\nabla b_\theta(S_t)$ là hàm của $\mathcal F_t$. Khi biết $\mathcal F_t$, $A_t\sim\pi_\theta(\cdot\mid S_t)$, nên
$$
\begin{aligned}
&\mathbb E\big[-\nabla b_\theta(S_t)\\
&\qquad\cdot\ln\pi_\theta(A_t\mid S_t)\,\big|\,\mathcal F_t\big]\\
&=-\nabla b_\theta(S_t)\\
&\quad\cdot\textstyle\sum_a\pi_\theta(a\mid S_t)\ln\pi_\theta(a\mid S_t)\\
&=\nabla b_\theta(S_t)\\
&\qquad\cdot\mathrm H\big(\pi_\theta(\cdot\mid S_t)\big),
\end{aligned}
$$
theo định nghĩa entropy (Định nghĩa 09.7).

**Bước 3: bài toán bandit.** Tại $\theta=\ln3$, $\pi_\theta(1)=\tfrac34$ và $\nabla b_\theta=1$. Entropy là
$$
\begin{aligned}
\mathrm H&=-\tfrac34\ln\tfrac34-\tfrac14\ln\tfrac14\\
&\approx0{,}2158+0{,}3466=0{,}5623 .
\end{aligned}
$$
Kì vọng của ước lượng là $\tfrac38+0{,}5623\approx0{,}9373$, gấp khoảng $2{,}5$ lần đạo hàm đúng.

**Kiểm tra lại.** Với bài toán bandit của Ví dụ 10.9, $\tilde b(A)=\kappa A$ cho $\tilde b(1)-\tilde b(0)=\kappa$, và công thức (a) cho số hạng trừ đi có kì vọng $\tfrac34\cdot\tfrac14\cdot\kappa=\tfrac{3\kappa}{16}$, khớp $\tfrac38-\tfrac{3\kappa}{16}$ của ví dụ đó. Với $\theta=0$, công thức (d) cho $\mathrm H=\ln2\approx0{,}6931$, khớp Nhận xét 10.9(i).
:::

### Bài tập 10.3 (Các giả thiết của Định lý 05.14 trong tối ưu chính sách)

**Mức độ:** kiểm tra giả thiết, chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 1 và 5; viết thuật toán REINFORCE thành hạ gradient ngẫu nhiên với một oracle của Định nghĩa 05.10, kiểm từng giả thiết của Định lý 05.14, và xác định giả thiết nào không thỏa.

::: exercise Bài tập 10.3
Thuật toán 10.6 đi lên theo gradient, còn Bài 05 phân tích phương pháp đi xuống. Đặt $F=-J$ và $\varphi=-\hat g$.

**(a)** Xét một MDP tầm nhìn hữu hạn với chính sách bảng trên $\mathcal A=\{0,1\}$, $\theta\in\mathbb R^{\mathcal S}$. Viết một lượt chạy theo $\pi_\theta$ thành $\tau=g(\theta,\xi)$, với $\xi$ là một bộ biến đều trên $[0,1)$ có phân bố không phụ thuộc $\theta$. Từ đó xác định nguồn ngẫu nhiên, ánh xạ oracle và trung bình $\psi$ của Định nghĩa 05.10, và chứng minh $\psi(\theta)=\nabla F(\theta)$ với mọi $\theta$. Thuật toán 10.6 với độ dài bước hằng ứng với thuật toán nào của Bài 05?

**(b)** Giả sử $\lvert r(s,a)\rvert\le C_r$ và $\lVert\nabla\ln\pi_\theta(a\mid s)\rVert\le C_\pi$ với mọi $\theta,s,a$. Chứng minh $\mathbb E_\xi\lVert\varphi(\theta,\xi)\rVert^2\le(H^2C_rC_\pi)^2$ với mọi $\theta$, rồi tìm $C_\pi$ cho chính sách bảng. Với bài toán bandit của Ví dụ 10.1 ($r(1)=3$, $r(0)=1$), tính đúng $\mathbb E_\xi\varphi(\theta,\xi)^2$ theo $\pi=\pi_\theta(1)$ và giá trị lớn nhất của nó trên $W=[0,2]$.

**(c)** Vẫn với bài toán bandit đó:

- **(i)** Xác định tập các $\theta$ trên đó $F$ lồi. Chứng minh rằng $\psi(-2)\notin\partial F(-2)$, với dưới vi phân theo Định nghĩa 05.2.
- **(ii)** Dựng một hàm $\tilde F:\mathbb R\to\mathbb R$ lồi, khả vi, bằng $F$ trên $[0,\infty)$, và kiểm (C), (G1), (G2) cho $\tilde F$ trên $W=[0,2]$.
- **(iii)** Với $w_1=0$, $T=10\,000$ và Hệ quả 05.15, tính độ dài bước và một cận dưới cho $\mathbb EJ(\bar\theta_T)$, với $\bar\theta_T$ là đầu ra của Thuật toán 05.11.

**(d)** Giải thích vì sao cách làm của (c) không cho một bảo đảm cho Thuật toán 10.6 trên một MDP bất kì. Dùng Ví dụ 10.7 cho một trường hợp cụ thể.
:::

::: hint Gợi ý 1
Phần (a). Rút mỗi biến của lượt bằng một biến đều và hàm phân phối ngược, như Phụ lục C rút hành động. Phần (b). Chặn $\lvert R(\tau)\rvert$ và chuẩn của tổng các gradient log bằng bất đẳng thức tam giác. Phần (c)(ii). Thay $F$ trên $(-\infty,0)$ bằng một hàm afin.
:::

::: hint Gợi ý 2
Phần (b). Với $f(\pi)=\pi(1-\pi)(9-8\pi)$, đạo hàm $f'(\pi)=24\pi^2-34\pi+9$ có hai nghiệm $\pi\approx0{,}3523$ và $\pi\approx1{,}0643$. Phần (c)(i). Một véc-tơ $v$ là dưới gradient tại $w$ chỉ khi đồ thị của $F$ nằm trên đường thẳng qua $(w,F(w))$ với hệ số góc $v$ trên cả $\mathbb R$; thử điểm $u=0$. Phần (c)(ii). Dùng tiếp tuyến của $F$ tại $0$. Phần (d). Theo đoạn sau Định nghĩa 05.2, $0\in\partial F(w)$ khi và chỉ khi $w$ là điểm cực tiểu toàn cục của $F$.
:::

::: solution Lời giải Bài tập 10.3
**(a) Lượt chạy như một oracle.**

**Bước 1: biểu diễn lượt.** Lấy $\xi=(U_{\mathrm{init}},U_0,\ldots,U_{H-1},V_0,\ldots,V_{H-2})$, gồm $2H$ biến đều trên $[0,1)$, độc lập. Đánh số $\mathcal S$ và rút:

- $S_0$ là trạng thái đầu tiên có hàm phân phối của $\mu_0$ vượt $U_{\mathrm{init}}$;
- $A_t=\mathbb 1\big[U_t<\pi_\theta(1\mid S_t)\big]$;
- $S_{t+1}$ là trạng thái đầu tiên có hàm phân phối của $P(\cdot\mid S_t,A_t)$ vượt $V_t$.

Khi đó $\tau=g(\theta,\xi)$ có phân bố $p_\theta$ của Định nghĩa 10.2, và phân bố của $\xi$ không phụ thuộc $\theta$.

**Bước 2: ba thành phần.** Nguồn ngẫu nhiên là $\xi$ với $\Xi=[0,1)^{2H}$; các lượt $j=1,2,\ldots$ dùng các bộ $\xi_1,\xi_2,\ldots$ độc lập cùng phân bố. Ánh xạ oracle là $\varphi(\theta,\xi)=-\hat g\big(g(\theta,\xi)\big)$. Với mỗi quỹ đạo $\tau'$, tập $\{(\theta,\xi):g(\theta,\xi)=\tau'\}$ là giao hữu hạn của các tập $\{U_t<\pi_\theta(1\mid s_t)\}$ hay phần bù của chúng và các điều kiện chỉ theo $U_{\mathrm{init}}$, $V_t$; mỗi tập đo được theo cặp vì $\theta\mapsto\pi_\theta(1\mid s)$ liên tục. Do đó $\varphi(\theta,\xi)=\sum_{\tau'}\mathbb 1[g(\theta,\xi)=\tau']\big(-\hat g_\theta(\tau')\big)$, với $\hat g_\theta(\tau')$ là ước lượng của Định lý 10.4 tại $\theta$. Vậy $\varphi$ là tổng hữu hạn của tích một hàm chỉ thị đo được theo cặp với một hàm liên tục theo $\theta$, nên đo được theo cặp $(\theta,\xi)$.

**Bước 3: trung bình.** Vì $g(\theta,\xi)\sim p_\theta$, theo Định lý 10.4,
$$
\begin{aligned}
\psi(\theta)&=-\mathbb E_\xi\hat g\big(g(\theta,\xi)\big)\\
&=-\mathbb E_{\tau\sim p_\theta}\hat g(\tau)\\
&=-\nabla J(\theta)=\nabla F(\theta).
\end{aligned}
$$
Oracle không chệch với mọi $\theta\in\mathbb R^{\mathcal S}$.

**Bước 4: thuật toán.** Với $\eta_j=\eta$, cập nhật $\theta_{j+1}=\theta_j+\eta\hat g_j=\theta_j-\eta\,\varphi(\theta_j,\xi_j)$ là bước của Thuật toán 05.11 với $W=\mathbb R^{\mathcal S}$, tức không chiếu. Tham số $\theta_j$ chỉ phụ thuộc $\xi_1,\ldots,\xi_{j-1}$, như $w_t$ ở Bài 05. Thuật toán 10.6 trả về điểm lặp cuối, còn Thuật toán 05.11 trả về điểm lặp trung bình.

**(b) Giả thiết (G2).**

**Bước 1: cận tổng quát.** $\lvert R(\tau)\rvert\le\sum_t\lvert r_t\rvert\le HC_r$, và theo bất đẳng thức tam giác $\big\lVert\sum_t\nabla\ln\pi_\theta(A_t\mid S_t)\big\rVert\le HC_\pi$. Do đó với mọi $\theta$ và $\xi$,
$$
\begin{aligned}
&\lVert\varphi(\theta,\xi)\rVert\\
&=\lvert R(\tau)\rvert\\
&\quad\cdot\Big\lVert\textstyle\sum_t\nabla\ln\pi_\theta(A_t\mid S_t)\Big\rVert\\
&\le H^2C_rC_\pi .
\end{aligned}
$$
Bình phương rồi lấy kì vọng, ta được (G2) với $G=H^2C_rC_\pi$ trên cả $\mathbb R^{\mathcal S}$.

**Bước 2: chính sách bảng.** Theo Ví dụ 10.4, Bước 1, áp dụng cho từng trạng thái, $\nabla\ln\pi_\theta(a\mid s)=\big(a-\pi_\theta(1\mid s)\big)e_s$, có chuẩn $\lvert a-\pi_\theta(1\mid s)\rvert<1$. Vậy $C_\pi=1$. Với bài toán bandit, $H=1$ và $C_r=3$, nên $G=3$.

**Bước 3: giá trị đúng.** Với $A=1$, $\varphi=-3(1-\pi)$; với $A=0$, $\varphi=-1\cdot(0-\pi)=\pi$. Do đó
$$
\begin{aligned}
\mathbb E_\xi\varphi^2&=\pi\cdot9(1-\pi)^2\\
&\quad+(1-\pi)\pi^2\\
&=\pi(1-\pi)(9-8\pi).
\end{aligned}
$$

**Bước 4: giá trị lớn nhất trên $W$.** Trên $W=[0,2]$, $\pi$ chạy từ $\tfrac12$ đến $\pi_2(1)\approx0{,}8808$. Đạo hàm $f'(\pi)=24\pi^2-34\pi+9$ có hai nghiệm $\pi=\frac{34\pm\sqrt{292}}{48}$, tức $0{,}3523$ và $1{,}0643$, và $f'<0$ giữa hai nghiệm; khoảng này chứa $[\tfrac12;\,0{,}8808]$. Vậy giá trị lớn nhất đạt tại $\theta=0$:
$$
\tfrac12\cdot\tfrac12\cdot(9-4)=1{,}25,
$$
và (G2) thỏa trên $W$ với $G=\sqrt{1{,}25}\approx1{,}1180$.

**(c) Giả thiết (C).**

**(i) Miền lồi.**

**Bước 1: đạo hàm bậc hai.** $J(\theta)=1+2\pi_\theta(1)$, nên $F''(\theta)=-J''(\theta)=-2\pi(1-\pi)(1-2\pi)$, như Bài tập 10.1(e). $F''\ge0$ khi và chỉ khi $\pi\ge\tfrac12$, tức $\theta\ge0$. $F$ lồi trên $[0,\infty)$; vì $F''<0$ trên $(-\infty,0)$, $F$ không lồi trên mọi khoảng chứa một điểm âm.

**Bước 2: tại $\theta=-2$.** $\pi_{-2}(1)\approx0{,}1192$, nên $F(-2)\approx-1{,}2384$ và $\psi(-2)=F'(-2)=-2\pi(1-\pi)\approx-0{,}2100$. Tại $u=0$, đường thẳng qua $(-2,F(-2))$ với hệ số góc $\psi(-2)$ có giá trị
$$
\begin{aligned}
&-1{,}2384+(-0{,}2100)\cdot2\\
&=-1{,}6584>F(0)=-2 .
\end{aligned}
$$
Bất đẳng thức dưới gradient sai tại $u=0$, nên $\psi(-2)\notin\partial F(-2)$. Oracle không chệch theo nghĩa $\psi=\nabla F$, nhưng dạng $\psi(w)\in\partial F(w)$ của (G1) cần $F$ lồi.

**(ii) Mở rộng lồi.**

**Bước 1: định nghĩa.** $F(0)=-2$ và $F'(0)=-2\cdot\tfrac14=-\tfrac12$. Đặt
$$
\tilde F(\theta)=\begin{cases}-2-\tfrac12\theta,&\theta<0,\\F(\theta),&\theta\ge0.\end{cases}
$$

**Bước 2: tính lồi.** Hai đạo hàm một phía tại $0$ cùng bằng $-\tfrac12$, nên $\tilde F$ khả vi. $\tilde F'$ bằng $-\tfrac12$ trên $(-\infty,0)$ và bằng $F'=-2\pi(1-\pi)$ trên $[0,\infty)$, tăng từ $-\tfrac12$ về $0$ vì $\pi(1-\pi)$ giảm khi $\pi\ge\tfrac12$. Một hàm khả vi có đạo hàm không giảm thì lồi, nên $\tilde F$ lồi. $W=[0,2]$ khác rỗng, đóng, lồi; vậy $(\tilde F,W)$ thỏa (C).

**Bước 3: (G1) và (G2).** Với $\theta\in W$, $\psi(\theta)=F'(\theta)=\tilde F'(\theta)\in\partial\tilde F(\theta)$ theo Mệnh đề 05.3(a). Ánh xạ $\varphi$ xác định với mọi $\theta\in\mathbb R$, và Định nghĩa 05.10 chỉ đòi (G1), (G2) trên $W$. (G2) thỏa với $G\approx1{,}1180$ theo (b).

**(iii) Cận của Hệ quả 05.15.**

**Bước 1: hằng số.** Mọi $u\in W$ có $\lvert w_1-u\rvert\le2$, nên $R=2$. Độ dài bước là
$$
\begin{aligned}
\eta=\frac R{G\sqrt T}&=\frac2{1{,}1180\cdot100}\\
&\approx0{,}01789 .
\end{aligned}
$$

**Bước 2: điểm so sánh.** $J$ tăng, nên $\min_W\tilde F=F(2)=-J(2)$, với $J(2)=1+2\pi_2(1)\approx2{,}7616$. Theo Hệ quả 05.15(b),
$$
\begin{aligned}
&\mathbb E\tilde F(\bar\theta_T)-F(2)\\
&\le\frac{RG}{\sqrt T}=\frac{2\sqrt{1{,}25}}{100}\\
&\le0{,}0224 .
\end{aligned}
$$

**Bước 3: đọc theo $J$.** $\bar\theta_T\in W$ nên $\tilde F(\bar\theta_T)=-J(\bar\theta_T)$, và
$$
\begin{aligned}
\mathbb EJ(\bar\theta_T)&\ge2{,}7616-0{,}0224\\
&=2{,}7392 .
\end{aligned}
$$
Cận so với điểm tốt nhất của $W$; cận trên đúng $3$ của $J$ không đạt trong $W$ hay trong $\mathbb R$.

**(d) Giới hạn.**

**Bước 1: chọn $W$ cần biết phần thưởng.** Với phần thưởng tổng quát, $J''(\theta)=\big(r(1)-r(0)\big)\pi(1-\pi)(1-2\pi)$. Miền lồi của $F$ là $[0,\infty)$ khi $r(1)>r(0)$ và $(-\infty,0]$ khi $r(1)<r(0)$. Chọn $W=[0,2]$ dùng dấu của $r(1)-r(0)$, đúng điều tác tử chưa biết.

**Bước 2: Ví dụ 10.7.** Ở đó $J''>0$ tại điểm dừng $\theta=\ln0{,}6$, nên $F=-J$ lõm trên một lân cận của điểm này, và không khoảng nào chứa điểm dừng cho (C). Tại điểm dừng, $\psi=\nabla F=0$. Theo đoạn sau Định nghĩa 05.2, $0\in\partial F$ chỉ tại điểm cực tiểu toàn cục của $F$, nhưng $F=-0{,}375$ tại đó trong khi $F\to-1$ khi $\theta\to\infty$. Vậy (G1) không thỏa tại điểm dừng.

**Bước 3: điều còn lại.** Oracle của (a) không chệch, và (G2) đúng trên cả không gian khi phần thưởng và gradient log bị chặn. Giả thiết không thỏa là (C). Không có (C), Mệnh đề 08.12 chỉ cho điểm dừng xấp xỉ (Ví dụ 10.7, Kết luận), và điểm dừng có thể là điểm cực tiểu của $J$.

**Kiểm tra lại.** Tại $\theta=0$, $\varphi$ bằng $-1{,}5$ hoặc $0{,}5$ với xác suất $\tfrac12$ mỗi giá trị. Trung bình là $-0{,}5=F'(0)$, và mô-men bậc hai là $\tfrac12(2{,}25+0{,}25)=1{,}25$, khớp (b), Bước 4.
:::

### Bài tập 10.4 (Độ chính xác phân lớp trung bình cuối cùng, chuyển đổi và độ quên từ một ma trận đánh giá)

**Mức độ:** tính toán, chứng minh, khái niệm. **Mục tiêu:** mục tiêu học tập 4; tính các độ đo của Định nghĩa 10.11, chứng minh quan hệ giữa độ quên và chuyển đổi ngược, và gắn một khoảng tin cậy cho các độ đo.

::: exercise Bài tập 10.4
Một giao thức học liên tục với $K=3$ nhiệm vụ phân lớp cho ma trận đánh giá dưới đây (giá trị giả định), hàng là thời điểm $k$, cột là nhiệm vụ $i$, và $\mathrm{acc}^\circ=(0{,}85;\,0{,}86;\,0{,}90)$.

| $k$ | $i=1$ | $i=2$ | $i=3$ |
|---|---|---|---|
| $1$ | $0{,}85$ | $0{,}20$ | $0{,}25$ |
| $2$ | $0{,}90$ | $0{,}88$ | $0{,}30$ |
| $3$ | $0{,}75$ | $0{,}60$ | $0{,}91$ |

**(a)** Tính độ chính xác phân lớp trung bình cuối cùng, chuyển đổi ngược, độ quên của từng nhiệm vụ cũ cùng độ quên trung bình, và chuyển đổi xuôi.

**(b)** Chứng minh rằng với mọi ma trận đánh giá, độ quên trung bình không nhỏ hơn đối của chuyển đổi ngược, và dấu bằng xảy ra khi và chỉ khi mỗi nhiệm vụ $i<K$ đạt độ chính xác phân lớp lớn nhất ngay ở hàng $i$. Chỉ ra nhiệm vụ gây chênh lệch ở (a).

**(c)** Mỗi ô của ma trận và mỗi $\mathrm{acc}^\circ_i$ được tính trên mẫu kiểm tra của nhiệm vụ $i$, gồm $n=2000$ quan sát, độc lập với mọi dữ liệu huấn luyện và với bộ nhớ (Định nghĩa 10.10). Gọi giá trị tổng thể của một ô là $1-L_{D_i}(w^{(k)})$ với hàm lỗi 0–1. Với $\delta=0{,}05$, xác định một khoảng chứa đồng thời giá trị tổng thể của chuyển đổi ngược và của chuyển đổi xuôi với xác suất ít nhất $1-\delta$. Dấu của đại lượng nào được xác định?

**(d)** Mô hình $w^{(3)}$ có phân lớp tốt trên mọi nhiệm vụ không? Con số nào trả lời câu hỏi này, và vì sao độ chính xác phân lớp trung bình cuối cùng không đủ?
:::

::: hint Gợi ý 1
Phần (a). Dùng đúng các công thức của Định nghĩa 10.11, như Ví dụ 10.13. Phần (b). So từng số hạng của hai trung bình. Phần (c). Áp dụng Hệ quả 02.10 cho từng ô khi các tham số đã cố định, rồi dùng cận hợp.
:::

::: hint Gợi ý 2
Phần (b). Với $i<K$, $\max_{i\le k\le K}\mathrm{acc}_{k,i}\ge\mathrm{acc}_{i,i}$. Phần (c). Hai độ đo dùng bảy ô khác nhau: $\mathrm{acc}_{1,1}$, $\mathrm{acc}_{2,2}$, $\mathrm{acc}_{3,1}$, $\mathrm{acc}_{3,2}$, $\mathrm{acc}_{3,3}$, $\mathrm{acc}^\circ_2$, $\mathrm{acc}^\circ_3$. Mỗi độ đo là trung bình của hai hiệu; mỗi hiệu sai lệch không quá hai lần bán kính.
:::

::: solution Lời giải Bài tập 10.4
**(a) Bốn độ đo.**

**Bước 1: độ chính xác phân lớp trung bình cuối cùng.** Trung bình hàng $3$:
$$
\begin{aligned}
&\tfrac13(0{,}75+0{,}60+0{,}91)\\
&=\tfrac{2{,}26}3\approx0{,}7533 .
\end{aligned}
$$

**Bước 2: chuyển đổi ngược.**
$$
\begin{aligned}
&\tfrac12\big[(0{,}75-0{,}85)\\
&\qquad+(0{,}60-0{,}88)\big]\\
&=\tfrac12(-0{,}10-0{,}28)=-0{,}19 .
\end{aligned}
$$

**Bước 3: độ quên.** Nhiệm vụ 1 đạt đỉnh $0{,}90$ ở hàng $2$, nên độ quên là $0{,}90-0{,}75=0{,}15$. Nhiệm vụ 2 đạt đỉnh $0{,}88$ ở hàng $2$, nên độ quên là $0{,}88-0{,}60=0{,}28$. Độ quên trung bình là $\tfrac12(0{,}15+0{,}28)=0{,}215$.

**Bước 4: chuyển đổi xuôi.**
$$
\begin{aligned}
&\tfrac12\big[(0{,}88-0{,}86)\\
&\qquad+(0{,}91-0{,}90)\big]\\
&=\tfrac12(0{,}02+0{,}01)=0{,}015 .
\end{aligned}
$$

**(b) Độ quên và chuyển đổi ngược.**

**Bước 1: từng nhiệm vụ.** Với $i<K$, hàng $i$ nằm trong tập $\{i,\ldots,K\}$ của phép lấy cực đại, nên
$$
\begin{aligned}
&\max_{i\le k\le K}\mathrm{acc}_{k,i}-\mathrm{acc}_{K,i}\\
&\ge\mathrm{acc}_{i,i}-\mathrm{acc}_{K,i},
\end{aligned}
$$
với dấu bằng khi và chỉ khi cực đại đạt tại hàng $i$.

**Bước 2: lấy trung bình.** Cộng theo $i=1,\ldots,K-1$ và chia cho $K-1$. Vế trái là độ quên trung bình; vế phải là $-\frac1{K-1}\sum_{i<K}(\mathrm{acc}_{K,i}-\mathrm{acc}_{i,i})$, tức đối của chuyển đổi ngược. Dấu bằng của tổng xảy ra khi và chỉ khi dấu bằng xảy ra ở mọi $i$.

**Bước 3: ma trận của đề.** $0{,}215\ge0{,}19$. Nhiệm vụ 2 có đỉnh ở hàng $2$, nên không gây chênh lệch. Nhiệm vụ 1 đạt $0{,}85$ ở hàng $1$ và đỉnh $0{,}90$ ở hàng $2$; chênh lệch $\tfrac12(0{,}90-0{,}85)=0{,}025$ đúng bằng $0{,}215-0{,}19$.

**(c) Khoảng tin cậy.**

**Bước 1: từng ô.** Ta điều kiện hóa theo mọi dữ liệu huấn luyện và nguồn ngẫu nhiên của các thuật toán; các đại lượng này độc lập với các mẫu kiểm tra (Định nghĩa 10.10). Khi đó $w^{(k)}$ và các mô hình của $\mathrm{acc}^\circ_i$ cố định, nên giá trị tổng thể của mỗi ô là một số; số này vẫn phụ thuộc dữ liệu huấn luyện. Mẫu kiểm tra của nhiệm vụ $i$ là một mẫu $D_i^{n}$, và hàm lỗi 0–1 thỏa (T3). Theo Hệ quả 02.10(b), với xác suất ít nhất $1-\delta'$, mỗi ô lệch giá trị tổng thể không quá $\sqrt{\ln(2/\delta')/(2n)}$.

**Bước 2: cận hợp.** Hai độ đo dùng bảy ô: $\mathrm{acc}_{1,1}$, $\mathrm{acc}_{2,2}$, $\mathrm{acc}_{3,1}$, $\mathrm{acc}_{3,2}$, $\mathrm{acc}_{3,3}$, $\mathrm{acc}^\circ_2$, $\mathrm{acc}^\circ_3$. Lấy $\delta'=\delta/7$; bảy khẳng định cùng đúng với xác suất ít nhất $1-\delta$, với bán kính
$$
\begin{aligned}
\epsilon&=\sqrt{\ln(14/0{,}05)/4000}\\
&=\sqrt{\ln280/4000}\\
&\approx\sqrt{0{,}0014087}\\
&\le0{,}0376 .
\end{aligned}
$$
Hai ô của một nhiệm vụ dùng chung một mẫu kiểm tra, nên chúng phụ thuộc nhau; cận hợp không cần tính độc lập.

**Bước 3: hai độ đo.** Mỗi hiệu hai ô lệch không quá $2\epsilon$, nên trung bình của hai hiệu cũng lệch không quá $2\epsilon\le0{,}0752$. Với xác suất ít nhất $0{,}95$, đồng thời
$$
\begin{aligned}
\Delta_{\mathrm b}&\in[-0{,}2652;\ -0{,}1148],\\
\Delta_{\mathrm f}&\in[-0{,}0602;\ 0{,}0902],
\end{aligned}
$$
với $\Delta_{\mathrm b}$, $\Delta_{\mathrm f}$ là giá trị tổng thể của chuyển đổi ngược và chuyển đổi xuôi. Chuyển đổi ngược tổng thể âm; dấu của chuyển đổi xuôi chưa xác định, vì $0{,}015<0{,}0752$. Xác suất có điều kiện của khẳng định này ít nhất $0{,}95$ với mọi giá trị của dữ liệu huấn luyện; lấy kì vọng theo dữ liệu đó, xác suất không điều kiện, theo cả dữ liệu huấn luyện và mẫu kiểm tra, cũng ít nhất $0{,}95$.

**(d) Phân lớp trên mọi nhiệm vụ.**

**Bước 1: con số cần xem.** Để biết $w^{(3)}$ có phân lớp tốt trên mọi nhiệm vụ không, cần ô nhỏ nhất của hàng cuối, $\min_i\mathrm{acc}_{3,i}=0{,}60$, ở nhiệm vụ 2. So với $\mathrm{acc}^\circ_2=0{,}86$ của mô hình chỉ học nhiệm vụ 2, mô hình cuối thấp hơn $0{,}26$. Vậy $w^{(3)}$ không phân lớp tốt trên mọi nhiệm vụ.

**Bước 2: trung bình không đủ.** Trung bình cuối cùng $0{,}7533$ cộng $0{,}91$ của nhiệm vụ mới với $0{,}60$ của nhiệm vụ 2; một ma trận có hàng cuối $(0{,}7533;\,0{,}7533;\,0{,}7533)$ cho cùng trung bình mà không nhiệm vụ nào dưới $0{,}75$.

**Kiểm tra lại.** Theo (b), độ quên trung bình trừ đối của chuyển đổi ngược bằng $\tfrac1{K-1}\sum_{i<K}\big(\max_k\mathrm{acc}_{k,i}-\mathrm{acc}_{i,i}\big)=\tfrac12(0{,}05+0)=0{,}025$, khớp $0{,}215-0{,}19$.
:::

### Bài tập 10.5 (Hai nhiệm vụ bậc hai với ba hệ số chính quy hóa)

**Mức độ:** tính toán, chứng minh. **Mục tiêu:** mục tiêu học tập 5; mô tả đánh đổi bền vững–mềm dẻo bằng tập các điểm tối ưu Pareto, và tính trọng số tầm quan trọng cần để phạt bậc hai khớp phát lại khi rủi ro cũ có độ cong khác $1$.

::: exercise Bài tập 10.5
Xét thiết lập của Mệnh đề 10.13: $L_A(w)=w^2/2$, $L_B(w)=(w-1)^2/2$, $w^{(1)}=0$.

**(a)** Với $\lambda\in\{\tfrac12,2,4\}$, tính $w_\lambda$, $L_A(w_\lambda)$, $L_B(w_\lambda)$ và tỉ lệ phát lại $\alpha$ cho cùng điểm cực tiểu. Tìm $\lambda$ nhỏ nhất bảo đảm $L_A(w_\lambda)\le0{,}02$, và giá trị của $L_B$ khi đó.

**(b)** Một điểm $w$ là *tối ưu Pareto* (Pareto optimal) nếu không có $w'$ nào với $L_A(w')\le L_A(w)$, $L_B(w')\le L_B(w)$ và ít nhất một bất đẳng thức ngặt. Chứng minh rằng tập các điểm tối ưu Pareto là $[0,1]$, và tập $\{w_\lambda:\lambda\ge0\}$ là $(0,1]$.

**(c)** Đổi rủi ro cũ thành $L_A(w)=2w^2$, vẫn với $w^{(1)}=0$. Tính điểm cực tiểu của phát lại với rủi ro cũ đầy đủ, $\alpha=\tfrac12$; của chính quy hóa tham số với $\Omega=1$, $\lambda=1$; và với $\Omega=4$, $\lambda=1$. Với $\alpha\in[0,1)$ tổng quát, tìm điều kiện trên $\lambda\Omega$ để chính quy hóa tham số cho cùng điểm cực tiểu với phát lại.

**(d)** Với rủi ro cũ của (c), tính giá trị nhỏ nhất của $L_A+L_B$ và so với giá trị của nó tại điểm cực tiểu của phép phạt với $\Omega=1$, $\lambda=1$.
:::

::: hint Gợi ý 1
Phần (a). Dùng Mệnh đề 10.13(c)–(d). Phần (b). Xét riêng ba trường hợp $w<0$, $0\le w\le1$, $w>1$, và so khoảng cách tới $0$ và tới $1$. Phần (c). Mỗi bài toán là cực tiểu hóa một hàm bậc hai lồi ngặt; đặt đạo hàm bằng $0$.
:::

::: hint Gợi ý 2
Phần (b). Với $0\le w\le1$ và $w'\ne w$, hoặc $w'<w$ thì $w'$ xa $1$ hơn, hoặc $w'>w$ thì $w'$ xa $0$ hơn. Phần (c). Đạo hàm của hàm mục tiêu phát lại là $(1-\alpha)(w-1)+4\alpha w$. Phần (d). $L_A+L_B$ tỉ lệ với hàm mục tiêu của phát lại với $\alpha=\tfrac12$.
:::

::: solution Lời giải Bài tập 10.5
**(a) Ba hệ số.**

**Bước 1: công thức.** Theo Mệnh đề 10.13(c)–(d), $w_\lambda=\frac1{1+\lambda}$, $L_A(w_\lambda)=\frac1{2(1+\lambda)^2}$, $L_B(w_\lambda)=\frac{\lambda^2}{2(1+\lambda)^2}$ và $\alpha=\frac\lambda{1+\lambda}$.

**Bước 2: $\lambda=\tfrac12$.** $w_\lambda=1/\tfrac32=\tfrac23$; $L_A=\tfrac12\cdot\tfrac49=\tfrac29$; $L_B=\tfrac12\cdot\tfrac19=\tfrac1{18}$; $\alpha=\tfrac12/\tfrac32=\tfrac13$.

| $\lambda$ | $w_\lambda$ | $L_A$ | $L_B$ | $\alpha$ |
|---|---|---|---|---|
| $\tfrac12$ | $\tfrac23$ | $\tfrac29$ | $\tfrac1{18}$ | $\tfrac13$ |
| $2$ | $\tfrac13$ | $\tfrac1{18}$ | $\tfrac29$ | $\tfrac23$ |
| $4$ | $\tfrac15$ | $\tfrac1{50}$ | $\tfrac8{25}$ | $\tfrac45$ |

**Bước 3: yêu cầu về rủi ro cũ.** $L_A(w_\lambda)\le0{,}02$ khi và chỉ khi $(1+\lambda)^2\ge\frac1{0{,}04}=25$, tức $\lambda\ge4$. Hệ số nhỏ nhất là $\lambda=4$, với $L_A=\tfrac1{50}=0{,}02$ và $L_B=\tfrac8{25}=0{,}32$. Rủi ro cũ nhỏ hơn khoảng mười một lần so với $\lambda=\tfrac12$ đổi lấy rủi ro mới tăng gần sáu lần, từ $\tfrac1{18}\approx0{,}056$ lên $0{,}32$.

**(b) Các điểm tối ưu Pareto.**

**Bước 1: $w\in[0,1]$.** Lấy $w'\ne w$. Nếu $w'<w\le1$ thì $\lvert w'-1\rvert>\lvert w-1\rvert$, nên $L_B(w')>L_B(w)$. Nếu $w'>w\ge0$ thì $\lvert w'\rvert>\lvert w\rvert$, nên $L_A(w')>L_A(w)$. Trong cả hai trường hợp, $w'$ không thỏa cả hai bất đẳng thức, nên $w$ tối ưu Pareto.

**Bước 2: $w\notin[0,1]$.** Nếu $w<0$, điểm $w'=0$ cho $L_A(0)=0<L_A(w)$ và $L_B(0)=\tfrac12<L_B(w)$. Nếu $w>1$, điểm $w'=1$ cho $L_B(1)=0<L_B(w)$ và $L_A(1)=\tfrac12<L_A(w)$. Vậy $w$ không tối ưu Pareto.

**Bước 3: ảnh của $\lambda\mapsto w_\lambda$.** Hàm $\lambda\mapsto\frac1{1+\lambda}$ liên tục, giảm ngặt trên $[0,\infty)$, bằng $1$ tại $\lambda=0$ và tiến về $0$ khi $\lambda\to\infty$. Ảnh là $(0,1]$. Điểm $w=0$, tức tham số cũ, không ứng với $\lambda$ hữu hạn nào; theo Mệnh đề 10.13(d), nó cũng không ứng với $\alpha\in[0,1)$ nào.

**(c) Rủi ro cũ có độ cong $4$.**

**Bước 1: phát lại.** Đạo hàm của $(1-\alpha)L_B+\alpha L_A$ là $(1-\alpha)(w-1)+4\alpha w$, bằng $0$ tại
$$
w=\frac{1-\alpha}{1+3\alpha}.
$$
Với $\alpha=\tfrac12$: $w=\tfrac12/\tfrac52=\tfrac15$.

**Bước 2: chính quy hóa tham số.** Đạo hàm của $L_B+\frac{\lambda\Omega}2w^2$ là $(w-1)+\lambda\Omega w$, bằng $0$ tại $w=\frac1{1+\lambda\Omega}$. Với $\Omega=1$, $\lambda=1$: $w=\tfrac12$. Với $\Omega=4$, $\lambda=1$: $w=\tfrac15$.

**Bước 3: điều kiện trùng nhau.** $\frac1{1+\lambda\Omega}=\frac{1-\alpha}{1+3\alpha}$ khi và chỉ khi $1+\lambda\Omega=\frac{1+3\alpha}{1-\alpha}$, tức
$$
\lambda\Omega=\frac{4\alpha}{1-\alpha}.
$$
Với $\Omega=4$, đó là $\lambda=\frac\alpha{1-\alpha}$, đúng quan hệ của Mệnh đề 10.13(d). Phạt $\frac{4\lambda}2w^2$ bằng $\lambda L_A(w)$, vì $\Omega=4$ là đạo hàm bậc hai của $L_A$; với $\Omega=1$, phép phạt chỉ bằng $\tfrac\lambda4L_A$ và đặt nhiệm vụ cũ nhẹ hơn bốn lần (Nhận xét 10.14(ii)).

**(d) Tổng hai rủi ro.**

**Bước 1: giá trị nhỏ nhất.** $L_A+L_B=2\big(\tfrac12L_A+\tfrac12L_B\big)$, nên điểm cực tiểu là điểm của phát lại với $\alpha=\tfrac12$, $w=\tfrac15$:
$$
\begin{aligned}
&2\cdot\tfrac1{25}+\tfrac12\cdot\tfrac{16}{25}\\
&=\tfrac2{25}+\tfrac8{25}=\tfrac25 .
\end{aligned}
$$

**Bước 2: phép phạt với $\Omega=1$.** Tại $w=\tfrac12$: $L_A=2\cdot\tfrac14=\tfrac12$, $L_B=\tfrac18$, tổng $\tfrac58$. Tổng lớn hơn giá trị nhỏ nhất $\tfrac25$ là $\tfrac9{40}$. Cận dưới $\tfrac14$ của Mệnh đề 10.13(a) đổi thành $\tfrac25$ khi độ cong của rủi ro cũ đổi.

**Kiểm tra lại.** Ở (a), $L_A+L_B$ bằng $\tfrac29+\tfrac1{18}=\tfrac5{18}$, $\tfrac5{18}$, $\tfrac1{50}+\tfrac8{25}=\tfrac{17}{50}$, đều không nhỏ hơn $\tfrac14$ của Mệnh đề 10.13(a). Ở (c), với $\alpha=\tfrac12$, công thức $\lambda\Omega=\frac{4\alpha}{1-\alpha}$ cho $4$, khớp $\Omega=4$, $\lambda=1$.
:::

### Bài tập 10.6 (Thiết kế một so sánh giữa tinh chỉnh và phát lại)

**Mức độ:** thực nghiệm (thiết kế), tính toán, khái niệm. **Mục tiêu:** mục tiêu học tập 4; đặc tả một giao thức so sánh công bằng, đọc một thí nghiệm có chung hạt giống bằng sai số chuẩn của hiệu, và tách kết quả thí nghiệm khỏi chứng minh.

::: exercise Bài tập 10.6
Cần so sánh tinh chỉnh (fine-tuning) với phát lại (replay) (Định nghĩa 10.12) trên $K=3$ nhiệm vụ phân lớp, mỗi nhiệm vụ có một mẫu huấn luyện và một mẫu kiểm tra riêng.

**(a)** Viết một giao thức so sánh gồm: thứ tự nhiệm vụ; ngân sách bộ nhớ; ngân sách tính toán; mẫu kiểm tra; cách chọn siêu tham số (độ dài bước $\eta$, tỉ lệ phát lại $\alpha$) không làm rò rỉ thông tin; định danh nhiệm vụ; số hạt giống (random seed) và nội dung báo cáo. Với mỗi thành phần, nêu một cách làm sai và hậu quả của nó.

**(b)** Thí nghiệm của Phụ lục C ($K=2$, hồi quy, $20$ hạt giống $0,\ldots,19$) dùng cùng hạt giống cho mọi $M$: với mỗi hạt giống, mọi $M$ có cùng dữ liệu, cùng mẫu kiểm tra và cùng $w$ sau nhiệm vụ A. Sau nhiệm vụ A, rủi ro kiểm tra trung bình là $0{,}125$ trên A (độ lệch chuẩn $0{,}002$) và $0{,}614$ trên B. Sau nhiệm vụ B:

| $M$ | Rủi ro A | Rủi ro B |
|---|---|---|
| $0$ | $0{,}624$ ($0{,}051$) | $0{,}126$ ($0{,}003$) |
| $5$ | $0{,}331$ ($0{,}132$) | $0{,}218$ ($0{,}076$) |
| $50$ | $0{,}256$ ($0{,}036$) | $0{,}248$ ($0{,}038$) |
| $1000$ | $0{,}252$ ($0{,}042$) | $0{,}255$ ($0{,}045$) |

Trong ngoặc là độ lệch chuẩn qua $20$ hạt giống. Hiệu rủi ro kiểm tra trên A giữa hai giá trị $M$ liền nhau, tính trong từng hạt giống, có trung bình và độ lệch chuẩn: $M=0$ trừ $M=5$: $0{,}292$ ($0{,}123$); $M=5$ trừ $M=50$: $0{,}075$ ($0{,}117$); $M=50$ trừ $M=1000$: $0{,}005$ ($0{,}043$).

- **(i)** Viết ma trận đánh giá theo rủi ro kiểm tra ($2\times2$) cho $M=0$ và $M=50$. Tính độ quên trên nhiệm vụ A theo thang rủi ro (rủi ro cuối trừ rủi ro nhỏ nhất trước đó) và tổng hai rủi ro cuối. So tổng với cận dưới tổng thể $\min_w\big(L_A(w)+L_B(w)\big)$ của mô hình ở Phụ lục C.
- **(ii)** Tính sai số chuẩn (standard error) của ba hiệu và tỉ số giữa hiệu trung bình và sai số chuẩn. Ở cặp $M=50$, $M=1000$, so với sai số chuẩn khi coi hai nhóm độc lập.
- **(iii)** Nêu những kết luận các số trên cho phép và những kết luận chúng không cho phép.

**(c)** Giao thức của Phụ lục C thiếu những thành phần nào của giao thức ở (a)?
:::

::: hint Gợi ý 1
Phần (a). Đi lần lượt qua các thành phần của Định nghĩa 10.10; với mỗi thành phần, xét phương pháp nào được lợi nếu hai phương pháp được đối xử khác nhau. Phần (b)(ii). Với chung hạt giống, đơn vị ngẫu nhiên là hạt giống.
:::

::: hint Gợi ý 2
Phần (a). Chọn mô hình bằng mẫu xác thực cần (T7) (Hệ quả 04.17); mẫu kiểm tra chỉ dùng một lần, sau mọi lựa chọn. Phần (b)(i). Viết $L_A+L_B$ của Phụ lục C thành một hàm của $w$. Phần (b)(ii). Sai số chuẩn bằng độ lệch chuẩn của hiệu chia $\sqrt{20}\approx4{,}472$; với hai nhóm độc lập, nó là $\sqrt{s_1^2+s_2^2}/\sqrt{20}$.
:::

::: solution Lời giải Bài tập 10.6
**(a) Một giao thức.**

- **Thứ tự nhiệm vụ.** Chạy cả $3!=6$ thứ tự, hoặc ít nhất hai thứ tự chọn trước, cho mọi phương pháp. Sai: một thứ tự duy nhất. Hậu quả: độ quên đo được có thể là tính chất của thứ tự đó.
- **Ngân sách bộ nhớ.** Cùng $M$ quan sát cũ cho mọi phương pháp có dùng bộ nhớ; tinh chỉnh có $M=0$, nên chạy phát lại ở nhiều giá trị $M$ và báo cả đường cong theo $M$. Sai: phát lại giữ toàn bộ dữ liệu cũ. Hậu quả: phát lại gần như thành huấn luyện chung, nên không còn đo tác dụng của một bộ nhớ hạn chế.
- **Ngân sách tính toán.** Cùng số lần tính gradient trên một quan sát cho mỗi nhiệm vụ. Sai: mỗi bước phát lại tính hai gradient, tinh chỉnh tính một. Hậu quả: phát lại được thêm tính toán, ngoài thông tin của bộ đệm.
- **Mẫu kiểm tra.** Tách mẫu kiểm tra của mỗi nhiệm vụ trước mọi bước khác; nó không vào mẫu huấn luyện, bộ đệm hay mẫu xác thực. Sai: rút bộ đệm từ dữ liệu có chứa mẫu kiểm tra. Hậu quả: rủi ro kiểm tra trên nhiệm vụ cũ bị ước lượng thấp hơn giá trị tổng thể.
- **Chọn siêu tham số.** Chọn $\eta$, $\alpha$ bằng mẫu xác thực tách từ dữ liệu huấn luyện, theo (T7), với cùng quy tắc cho hai phương pháp. Ghi rõ mẫu xác thực của thời điểm $k$ chỉ dùng dữ liệu mà giao thức cho thấy tại thời điểm đó; nếu chọn một lần cho cả dãy nhiệm vụ, ghi rằng cách chọn đã dùng thông tin của các nhiệm vụ sau. Sai: chọn $\alpha$ theo ma trận đánh giá trên mẫu kiểm tra. Hậu quả: Hệ quả 02.10 không còn áp dụng cho các ô, và phương pháp có nhiều siêu tham số hơn được lợi.
- **Định danh nhiệm vụ.** Nêu rõ có hay không, giống nhau cho hai phương pháp. Sai: chỉ một phương pháp được biết nhiệm vụ khi dự đoán. Hậu quả: hai phương pháp giải hai bài toán khác nhau (đoạn sau Định nghĩa 10.10).
- **Hạt giống.** Ít nhất $10$ hạt giống, dùng chung cho mọi phương pháp; báo trung bình, độ lệch chuẩn của hiệu theo hạt giống và sai số chuẩn của hiệu. Sai: một hạt giống. Hậu quả: không tách được hiệu giữa phương pháp khỏi dao động.
- **Báo cáo.** Cả ma trận đánh giá, ba độ đo của Định nghĩa 10.11 theo quy ước nêu trước, ô nhỏ nhất của hàng cuối, các $\mathrm{acc}^\circ_i$ và một mô hình huấn luyện chung làm đối chứng. Sai: chỉ báo độ chính xác phân lớp trung bình cuối cùng. Hậu quả: một nhiệm vụ bị quên có thể bị che (Bài tập 10.4(d)).

**(b) Tính trên số đã chạy.** Các số là kết quả thí nghiệm cho một thiết lập, không phải chứng minh.

**Bước 1: ma trận đánh giá.** Hàng là thời điểm, cột là nhiệm vụ; hàng đầu chung cho mọi $M$.

| | A | B |
|---|---|---|
| sau A | $0{,}125$ | $0{,}614$ |
| sau B, $M=0$ | $0{,}624$ | $0{,}126$ |
| sau B, $M=50$ | $0{,}256$ | $0{,}248$ |

**Bước 2: độ quên theo thang rủi ro.** Với rủi ro, độ quên là rủi ro cuối trừ rủi ro nhỏ nhất trước đó (đổi chiều so sánh, đoạn sau Định nghĩa 10.11). Với $M=0$: $0{,}624-0{,}125=0{,}499$. Với $M=50$: $0{,}256-0{,}125=0{,}131$.

**Bước 3: tổng hai rủi ro.** Tổng cuối là $0{,}624+0{,}126=0{,}750$ với $M=0$ và $0{,}256+0{,}248=0{,}504$ với $M=50$. Theo Phụ lục C, $L_A+L_B=\tfrac12\big(w^2+(w-1)^2\big)+0{,}25$, nhỏ nhất tại $w=\tfrac12$, bằng $\tfrac12\cdot\tfrac12+0{,}25=0{,}5$, tức cận $\tfrac14$ của Mệnh đề 10.13(a) cộng phần nhiễu $0{,}25$. Với $M=50$, tổng cách cận dưới $0{,}004$; phát lại đặt $w$ gần điểm thỏa hiệp, không bỏ được đánh đổi.

**Bước 4: sai số chuẩn của hiệu.** Chia độ lệch chuẩn cho $\sqrt{20}\approx4{,}472$:

| Cặp $M$ | Sai số chuẩn | Tỉ số |
|---|---|---|
| $0$ và $5$ | $0{,}0275$ | $10{,}6$ |
| $5$ và $50$ | $0{,}0262$ | $2{,}9$ |
| $50$ và $1000$ | $0{,}0096$ | $0{,}5$ |

Ví dụ, ở cặp đầu, $0{,}123/4{,}472\approx0{,}0275$ và $0{,}292/0{,}0275\approx10{,}6$.

**Bước 5: hai nhóm độc lập.** Ở cặp $50$ và $1000$,
$$
\begin{aligned}
&\sqrt{0{,}036^2+0{,}042^2}/4{,}472\\
&\approx0{,}0553/4{,}472\approx0{,}0124 .
\end{aligned}
$$
Sai số chuẩn của hiệu theo hạt giống, $0{,}0096$, nhỏ hơn, vì hai lần chạy cùng hạt giống có chung dữ liệu và mẫu kiểm tra.

**Bước 6: kết luận được phép.** Trong thiết lập của Phụ lục C, bộ đệm $5$ quan sát giảm rủi ro kiểm tra trên A so với tinh chỉnh, với hiệu gấp khoảng $10$ lần sai số chuẩn. Bộ đệm $50$ quan sát giảm tiếp, với hiệu gấp khoảng $3$ lần sai số chuẩn. Giữa $M=50$ và $M=1000$, hiệu $0{,}005$ nhỏ hơn sai số chuẩn, nên thí nghiệm không phân biệt được hai giá trị.

**Bước 7: kết luận không được phép.** Các số không cho biết phát lại tốt hơn tinh chỉnh với mạng nơ-ron, với phân lớp, với thứ tự nhiệm vụ khác hay với nhiều hơn hai nhiệm vụ. Chúng không chứng minh rủi ro giảm như $\tfrac1{8M}$; công thức đó thuộc mô hình của Ví dụ 10.16, khác mô hình ở đây.

**(c) Thiếu sót của Phụ lục C.** Chỉ có thứ tự A rồi B; mỗi bước phát lại tính hai gradient, tinh chỉnh tính một. Ngoài ra, $\eta=0{,}02$ và $\alpha=\tfrac12$ cố định, không có mẫu xác thực và không nêu cách chọn; bảng chỉ ghi rủi ro sau nhiệm vụ B, không có đối chứng huấn luyện chung đo bằng thí nghiệm, và không ghi hiệu theo hạt giống.

**Kiểm tra lại.** Ở cặp $M=0$ và $M=5$, sai số chuẩn khi coi hai nhóm độc lập là $\sqrt{0{,}051^2+0{,}132^2}/4{,}472\approx0{,}0316$, lớn hơn $0{,}0275$ theo hạt giống, cùng chiều với Bước 5. Độ quên $0{,}499$ của tinh chỉnh gần $L_A(1)-L_A(0)=\tfrac12$ của rủi ro tổng thể, vì $w$ cuối là $0{,}998$ (Phụ lục C).
:::

### Bài tập 10.7 (Năm câu hỏi tổng kết cho hai thiết lập khác)

**Mức độ:** khái niệm, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 1 và 5; áp năm câu hỏi của câu (f) ở §12 cho hai thiết lập chưa có trong Phụ lục D, và chỉ ra giả thiết nào của Bài 01–08 còn đúng.

::: exercise Bài tập 10.7
Năm câu hỏi của câu (f) ở §12 là: quá trình sinh dữ liệu; mục tiêu; đối tượng so sánh; các đại lượng ngẫu nhiên; các giả thiết của Bài 01–08 cần thay đổi. Trả lời năm câu hỏi cho hai thiết lập sau.

**(i)** Đánh giá một chính sách $\pi_\theta$ của một MDP tầm nhìn hữu hạn bằng $m$ lượt, với $\theta$ cố định trước khi chạy (như Ví dụ 10.12).

**(ii)** Học một mô hình dự đoán giá trị kế tiếp từ $k$ giá trị trước, với hàm lỗi log, trên các cửa sổ chồng lấn của một chuỗi thời gian duy nhất $x_1,\ldots,x_n$ (Thiết lập B của Định nghĩa 09.1).
:::

::: hint Gợi ý 1
Dùng bốn danh sách của Phụ lục D làm mẫu. Với (T1), phân biệt dạng đầy đủ (độc lập cùng phân bố) và dạng yếu (mỗi quan sát có phân bố $D$, không cần độc lập) của Bài 01.
:::

::: hint Gợi ý 2
Phần (i). Quan sát là cả một lượt, như một chuỗi trong Thiết lập A. Phần (ii). Hai cửa sổ liền nhau chung $k-1$ giá trị; nếu chuỗi dừng, mọi cửa sổ có cùng phân bố. Hàm lỗi log bị chặn chỉ khi các xác suất của mô hình bị chặn dưới (Ví dụ 09.4).
:::

::: solution Lời giải Bài tập 10.7
**(i) Đánh giá một chính sách cố định.**

- **Quá trình sinh dữ liệu.** Các lượt $\tau_1,\ldots,\tau_m$ độc lập cùng phân bố $p_\theta$ (Định nghĩa 10.2). Trong một lượt, các bước phụ thuộc nhau, nhưng quan sát là cả lượt.
- **Mục tiêu.** Ước lượng số $J(\theta)$ bằng trung bình $\frac1m\sum_jR(\tau_j)$; không có bước chọn mô hình.
- **Đối tượng so sánh.** Không có lớp giả thuyết hay điểm tốt nhất; đại lượng cần đo là sai số $\big\lvert\frac1m\sum_jR(\tau_j)-J(\theta)\big\rvert$.
- **Đại lượng ngẫu nhiên.** Các lượt, các $R(\tau_j)$ và trung bình của chúng; $\theta$, $\mu_0$, $P$, $r$ cố định.
- **Giả thiết.** (T1) đúng ở dạng đầy đủ với quan sát là lượt. (T3) thay bằng miền $[Hr_{\min},Hr_{\max}]$ của $R(\tau)$, nên bán kính của Hệ quả 02.10 nhân với $H(r_{\max}-r_{\min})$ (đoạn sau Nhận xét 02.8). Không cần (C) hay giả thiết tối ưu nào.

**(ii) Một chuỗi thời gian với cửa sổ chồng lấn.**

- **Quá trình sinh dữ liệu.** Một chuỗi $x_1,\ldots,x_n$; các cửa sổ $u_j$, $j=k+1,\ldots,n$, chung giá trị với nhau và nói chung phụ thuộc nhau.
- **Mục tiêu.** Hàm lỗi log kì vọng của giá trị kế tiếp khi biết $k$ giá trị trước, lấy theo phân bố của một cửa sổ. Đại lượng này chỉ là một số cố định khi mọi cửa sổ có cùng phân bố, chẳng hạn khi chuỗi dừng.
- **Đối tượng so sánh.** Cận dưới đúng của mục tiêu trên lớp mô hình đã chọn.
- **Đại lượng ngẫu nhiên.** Cả chuỗi, do đó mọi cửa sổ, rủi ro thực nghiệm trên các cửa sổ và tham số học được.
- **Giả thiết.** (T1) ở dạng đầy đủ không thỏa, vì các cửa sổ phụ thuộc nhau; dạng yếu thỏa khi chuỗi dừng, nên rủi ro thực nghiệm của một mô hình cố định vẫn là ước lượng không chệch, nhưng Hệ quả 02.10 không áp dụng. (T3) không thỏa, vì hàm lỗi log không bị chặn; nó chỉ được thay bằng một miền $[0,\ln(1/c)]$ khi mọi xác suất của mô hình không nhỏ hơn $c>0$ (Ví dụ 09.4).

**Kiểm tra lại.** Với MDP của Ví dụ 10.2, $H=2$, $r_{\min}=0$, $r_{\max}=3$, nên miền $[Hr_{\min},Hr_{\max}]$ của (i) là $[0,6]$, chứa miền $[0,4]$ mà Ví dụ 10.12 dùng. Miền $[0,6]$ cho bán kính lớn hơn $1{,}5$ lần; miền hẹp hơn đến từ việc phần thưởng ở bước đầu chỉ thuộc $\{0,1\}$.
:::

## Bài tập chọn từ UML

### Bài tập 10.8 (Chuyển từ học trực tuyến sang học theo lô; UML Bài tập 21.5)

**Mức độ:** chứng minh, tính toán, kiểm tra giả thiết. **Mục tiêu:** mục tiêu học tập 5; dùng một cận số lỗi trên mọi dãy để chặn rủi ro kì vọng khi dữ liệu độc lập cùng phân bố, và chỉ ra bước dùng giả thiết đó. Ý (b), (c) do học phần thêm.

::: exercise Bài tập 10.8
Xét bài toán phân lớp nhị phân với miền $\mathcal X$ và lớp $\mathcal H$ các hàm $\mathcal X\to\{0,1\}$. Một thuật toán *học trực tuyến* (online learning) tất định $A$ nhận lần lượt các cặp $(x_1,y_1),(x_2,y_2),\ldots$; ở vòng $t$, trước khi thấy $y_t$, nó dự đoán bằng một giả thuyết $h_t:\mathcal X\to\{0,1\}$ chỉ phụ thuộc $(x_1,y_1),\ldots,(x_{t-1},y_{t-1})$. Thuật toán $A$ có *cận số lỗi* (mistake bound) $M_A(\mathcal H)<\infty$ nếu trên mọi dãy có $y_t=h^\star(x_t)$ với một $h^\star\in\mathcal H$, số vòng $t$ có $h_t(x_t)\ne y_t$ không quá $M_A(\mathcal H)$. Các hàm được giả sử đo được. Ý (a) là một phép *chuyển từ học trực tuyến sang học theo lô* (online-to-batch conversion).

**(a)** Cho $x_1,\ldots,x_T$ độc lập cùng phân bố $D$ trên $\mathcal X$, $y_t=h^\star(x_t)$ với $h^\star\in\mathcal H$ cố định, và $L_D(h)=\Pr_{x\sim D}\big(h(x)\ne h^\star(x)\big)$. Chỉ số $r$ rút đều trên $\{1,\ldots,T\}$, độc lập với các $x_t$. Chứng minh rằng
$$
\mathbb E\big[L_D(h_r)\big]\le\frac{M_A(\mathcal H)}T,
$$
với kì vọng lấy theo các $x_t$ và theo $r$.

**(b)** Suy ra một cận cho $\Pr\big(L_D(h_r)\ge\epsilon\big)$. Với $M_A(\mathcal H)=10$, tính vế phải ở (a) khi $T=1000$, và tìm $T$ đủ để $\Pr\big(L_D(h_r)\ge0{,}05\big)\le0{,}05$.

**(c)** Đổi dãy: $x_1,\ldots,x_{T/2}$ rút từ $D_1$, $x_{T/2+1},\ldots,x_T$ rút từ $D_2$, mọi $x_t$ độc lập, cùng $h^\star$, $T$ chẵn. Bước nào của (a) còn đúng? Đại lượng nào được chặn, và nó có chặn rủi ro trên $D_1$ của các giả thuyết dùng ở cuối dãy không?
:::

::: hint Gợi ý 1
Phần (a). Lập luận "quan sát mới" ở Bước 1 của chứng minh Hệ quả 06.2: giả thuyết dùng ở vòng $t$ không phụ thuộc $x_t$. Phần (b). $L_D(h_r)\ge0$, và (a) chặn kì vọng của nó.
:::

::: hint Gợi ý 2
Phần (a). Với $h_t$ cố định khi biết $x_1,\ldots,x_{t-1}$, kì vọng có điều kiện của $\mathbb 1[h_t(x_t)\ne y_t]$ là $L_D(h_t)$. Cận số lỗi đúng với mọi dãy, nên đúng sau khi lấy kì vọng. Phần (b). Dùng bất đẳng thức Markov. Phần (c). Viết $D_t$ cho phân bố của $x_t$ và lặp lại (a) với $L_{D_t}$.
:::

::: solution Lời giải Bài tập 10.8
**(a) Rủi ro kì vọng của giả thuyết chọn ngẫu nhiên.**

**Bước 1: một vòng.** $h_t$ là hàm của $x_1,\ldots,x_{t-1}$, vì các nhãn được xác định bởi $h^\star$. Biến $x_t$ độc lập với $x_1,\ldots,x_{t-1}$ và có phân bố $D$. Khi biết $x_1,\ldots,x_{t-1}$, $h_t$ cố định, nên
$$
\begin{aligned}
&\mathbb E\big[\mathbb 1[h_t(x_t)\ne y_t]\\
&\qquad\big|\,x_1,\ldots,x_{t-1}\big]\\
&=\Pr_{x\sim D}\big(h_t(x)\ne h^\star(x)\big)\\
&=L_D(h_t).
\end{aligned}
$$
Theo tính chất tháp, $\mathbb E\,\mathbb 1[h_t(x_t)\ne y_t]=\mathbb EL_D(h_t)$. Đây là chỗ dùng giả thiết độc lập cùng phân bố.

**Bước 2: cộng theo $t$.** Dãy được gán nhãn bởi $h^\star\in\mathcal H$, nên với mọi giá trị của $x_1,\ldots,x_T$,
$$
\textstyle\sum_{t=1}^T\mathbb 1[h_t(x_t)\ne y_t]\le M_A(\mathcal H).
$$
Lấy kì vọng và dùng Bước 1: $\sum_{t=1}^T\mathbb EL_D(h_t)\le M_A(\mathcal H)$.

**Bước 3: chỉ số ngẫu nhiên.** $r$ độc lập với các $x_t$ và nhận mỗi giá trị với xác suất $\tfrac1T$, nên
$$
\begin{aligned}
\mathbb EL_D(h_r)&=\tfrac1T\textstyle\sum_{t=1}^T\mathbb EL_D(h_t)\\
&\le\frac{M_A(\mathcal H)}T .
\end{aligned}
$$

**(b) Cận xác suất.**

**Bước 1: bất đẳng thức Markov.** $L_D(h_r)\ge0$, nên với $\epsilon>0$,
$$
\begin{aligned}
\Pr\big(L_D(h_r)\ge\epsilon\big)&\le\frac{\mathbb EL_D(h_r)}\epsilon\\
&\le\frac{M_A(\mathcal H)}{T\epsilon}.
\end{aligned}
$$

**Bước 2: số.** Với $M_A=10$, $T=1000$: $\mathbb EL_D(h_r)\le0{,}01$. Điều kiện $\frac{10}{T\cdot0{,}05}\le0{,}05$ tương đương $T\ge\frac{10}{0{,}0025}=4000$.

**(c) Hai phân bố.**

**Bước 1: Bước 1 của (a).** Các $x_t$ vẫn độc lập, nên khi biết $x_1,\ldots,x_{t-1}$, $x_t$ có phân bố $D_t$ ($D_1$ khi $t\le T/2$, $D_2$ khi $t>T/2$). Bước 1 đúng với $L_{D_t}$ thay cho $L_D$.

**Bước 2: Bước 2 và 3.** Dãy vẫn được gán nhãn bởi $h^\star$, nên cận số lỗi vẫn áp dụng, và
$$
\tfrac1T\textstyle\sum_{t=1}^T\mathbb EL_{D_t}(h_t)\le\frac{M_A(\mathcal H)}T .
$$

**Bước 3: đại lượng được chặn.** Các $h_t$ với $t>T/2$ chỉ được đo trên $D_2$, nên cận không nói gì về $L_{D_1}(h_T)$. Đại lượng này giống hối tiếc ở Ví dụ 10.17: nó cộng hàm lỗi tại thời điểm của từng vòng, và không chặn độ quên. Phần đầu dãy chỉ cho $\frac1T\sum_{t\le T/2}\mathbb EL_{D_1}(h_t)\le M_A/T$, tức trung bình trên $D_1$ của các giả thuyết dùng ở nửa đầu không quá $2M_A/T$.

**Kiểm tra lại.** Với $M_A=0$, thuật toán không mắc lỗi trên mọi dãy khả thực, nên mọi $h_t$ trùng $h^\star$ trên toàn $\mathcal X$, vì $x_t$ có thể là điểm bất kì, và (a) cho $\mathbb EL_D(h_r)=0$, đúng.
:::

### Bài tập 10.9 (Tùy chọn: mẹo nhân đôi; UML Bài tập 21.4)

**Mức độ:** chứng minh, tính toán. **Mục tiêu:** mục tiêu học tập 5; chọn độ dài bước của Nhận xét 10.16 mà không cần biết trước số vòng $T$, và tính cái giá của việc không biết $T$. Ý (b), (c) do học phần thêm.

::: exercise Bài tập 10.9
Cho một thuật toán học trực tuyến $A$ (Định nghĩa 10.15) có tham số phụ thuộc số vòng. *Mẹo nhân đôi* (doubling trick): với $m=0,1,2,\ldots$, khởi động lại $A$ với số vòng $2^m$ và chạy nó trên các vòng $t=2^m,\ldots,2^{m+1}-1$; dừng khi hết $T$ vòng, nên đoạn cuối có thể bị cắt.

**(a)** Giả sử với mọi $m$ và mọi $u\in W$, tổng hàm lỗi của $A$ trên đoạn thứ $m$ trừ tổng hàm lỗi của $u$ trên đoạn đó không quá $\alpha\sqrt{2^m}$, kể cả khi đoạn bị cắt. Chứng minh rằng với mọi $T\ge1$ và mọi $u\in W$,
$$
\mathrm{Regret}_T(u)\le\frac{\sqrt2}{\sqrt2-1}\,\alpha\sqrt T,
$$
và suy ra cùng cận cho hối tiếc tĩnh.

**(b)** Giả sử $W$ bị chặn và $R\ge\sup_{u\in W}\lVert w_1-u\rVert$. Chứng minh rằng hạ gradient trực tuyến của Nhận xét 10.16, khởi động lại tại $w_1$ với $\eta=R/(G\sqrt{2^m})$ ở đoạn thứ $m$, thỏa giả thiết của (a) với $\alpha=RG$, kể cả trên đoạn bị cắt.

**(c)** Với $\alpha=1$ và $T=1000$, tính số đoạn, tổng $\sum_m\alpha\sqrt{2^m}$ trên các đoạn đã dùng, cận của (a), và so với $\alpha\sqrt T$ của trường hợp biết trước $T$.
:::

::: hint Gợi ý 1
Phần (a). Hối tiếc với một $u$ cố định là tổng của các hối tiếc theo đoạn với cùng $u$. Phần (b). Cận của Nhận xét 10.16 với $T$ thay bằng độ dài đoạn và $\eta$ cố định.
:::

::: hint Gợi ý 2
Phần (a). Gọi $M$ là số nguyên lớn nhất với $2^M\le T$; các đoạn $m=0,\ldots,M$ phủ $T$ vòng. Tổng $\sum_{m=0}^M(\sqrt2)^m$ là tổng cấp số nhân. Phần (b). Vế phải $\frac{R^2}{2\eta}+\frac{\eta G^2L}2$ tăng theo độ dài $L$ của đoạn.
:::

::: solution Lời giải Bài tập 10.9
**(a) Cận cho hối tiếc.**

**Bước 1: các đoạn.** Đoạn thứ $m$ gồm các vòng từ $2^m$ đến $2^{m+1}-1$, dài $2^m$. Gọi $I_m$ là tập các vòng của đoạn thứ $m$ và $M=\lfloor\log_2T\rfloor$, nên $2^M\le T<2^{M+1}$. Vòng $T$ thuộc đoạn $M$, nên các đoạn $m=0,\ldots,M$ phủ đúng $T$ vòng, đoạn $M$ có thể bị cắt.

**Bước 2: tách hối tiếc.** Với $u$ cố định, $\mathrm{Regret}_T(u)$ là tổng theo $t$ của $\ell(w_t,z_t)-\ell(u,z_t)$, nên bằng tổng các hối tiếc theo đoạn với cùng $u$. Theo giả thiết,
$$
\mathrm{Regret}_T(u)\le\alpha\textstyle\sum_{m=0}^M2^{m/2}.
$$

**Bước 3: tổng cấp số nhân.**
$$
\begin{aligned}
\textstyle\sum_{m=0}^M2^{m/2}&=\frac{2^{(M+1)/2}-1}{\sqrt2-1}\\
&<\frac{\sqrt2\cdot2^{M/2}}{\sqrt2-1}\\
&\le\frac{\sqrt2}{\sqrt2-1}\sqrt T,
\end{aligned}
$$
vì $2^{M/2}\le\sqrt T$. Nhân với $\alpha$, ta được cận của đề.

**Bước 4: hối tiếc tĩnh.** Vế phải không phụ thuộc $u$, nên lấy cận trên đúng theo $u\in W$ ta được cùng cận cho $\sup_u\mathrm{Regret}_T(u)$. Điểm so sánh tốt nhất của từng đoạn có thể khác nhau; vì $\sup_u\sum_m\le\sum_m\sup_u$, lấy cận trên đúng theo từng đoạn trước cũng cho cùng cận.

**(b) Hạ gradient trực tuyến.**

**Bước 1: một đoạn.** Ở đoạn $m$, thuật toán bắt đầu lại tại $w_1$ với $\eta$ cố định, nên với mọi $u\in W$ (theo giả thiết, $\lVert w_1-u\rVert\le R$), chứng minh của Nhận xét 10.16 áp dụng cho các vòng của đoạn. Gọi $L\le2^m$ là độ dài đoạn. Khi đó
$$
\begin{aligned}
&\textstyle\sum_{t\in I_m}\big(\ell(w_t,z_t)-\ell(u,z_t)\big)\\
&\le\frac{R^2}{2\eta}+\frac{\eta G^2L}2 .
\end{aligned}
$$

**Bước 2: thay $\eta$.** Vế phải tăng theo $L$, nên không quá giá trị tại $L=2^m$. Với $\eta=R/(G\sqrt{2^m})$, hai số hạng cùng bằng $\tfrac12RG\sqrt{2^m}$, tổng là $RG\sqrt{2^m}$ (như Bước 1 của chứng minh Hệ quả 05.15). Vậy giả thiết của (a) thỏa với $\alpha=RG$, kể cả trên đoạn bị cắt.

**(c) Số với $T=1000$.**

**Bước 1: các đoạn.** $2^9=512\le1000<1024$, nên $M=9$ và có $10$ đoạn; đoạn cuối gồm $489$ vòng, từ $512$ đến $1000$, thay vì $512$ vòng.

**Bước 2: tổng.**
$$
\begin{aligned}
\textstyle\sum_{m=0}^92^{m/2}&=\frac{2^5-1}{\sqrt2-1}\\
&=\frac{31}{0{,}41421}\approx74{,}84 .
\end{aligned}
$$

**Bước 3: cận của (a).** $\frac{\sqrt2}{\sqrt2-1}\approx3{,}4142$ và $\sqrt{1000}\approx31{,}623$, nên cận không quá $107{,}97$ (làm tròn lên).

**Bước 4: so sánh.** Khi biết trước $T$, Nhận xét 10.16 cho $\alpha\sqrt T\approx31{,}62$. Với $T=1000$, mẹo nhân đôi cho tổng $74{,}84$, gấp khoảng $2{,}4$ lần; hằng số chung $3{,}41$ là cái giá trong trường hợp xấu nhất theo $T$.

**Kiểm tra lại.** Với $T=1$: $M=0$, một đoạn dài $1$, tổng bằng $\alpha$, nhỏ hơn cận $3{,}41\alpha$. Với $T=1000$: tổng $74{,}84$ nhỏ hơn cận $107{,}97$, khớp Bước 3 của (a).
:::
