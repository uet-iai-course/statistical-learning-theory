# Bài 05 — Hạ gradient, hạ gradient ngẫu nhiên và cận tối ưu

Bài 04 đo bộ giải bằng sai số tối ưu thực nghiệm $\operatorname{opt}_S$ (Định nghĩa 04.2) nhưng chưa cho cách tính một nghiệm có $\operatorname{opt}_S$ nhỏ. Bài 04 kết thúc bằng hai câu hỏi: sau $T$ vòng lặp, độ chênh tối ưu (suboptimality) của mục tiêu còn bao nhiêu, và mỗi vòng tốn bao nhiêu phép tính?

Câu hỏi trung tâm của bài là tối ưu ngẫu nhiên làm giảm một hàm mục tiêu nhanh đến mức nào. Thuật toán chính là hạ gradient ngẫu nhiên (stochastic gradient descent, SGD) có chiếu; hạ gradient (gradient descent, GD) có chiếu là trường hợp tất định của nó. Các công cụ là hàm lồi (convex function), dưới gradient (subgradient), phép chiếu (projection) lên một tập lồi đóng, oracle gradient ngẫu nhiên (stochastic gradient oracle), tổng triệt tiêu (telescoping sum) và lô nhỏ (mini-batch).

## Câu hỏi mở đầu

Tập huấn luyện gồm $m=10^6$ hồ sơ; mỗi hồ sơ là một quan sát gồm một véc-tơ chỉ số đo và một nhãn. Cần tìm véc-tơ trọng số $w$ của một hàm phân lớp tuyến tính bằng cách tối thiểu hóa rủi ro thực nghiệm (empirical risk) $L_S(w)$ với hàm lỗi logistic (logistic loss).

Một bước GD cần gradient của hàm lỗi trên cả $10^6$ quan sát. SGD chọn ngẫu nhiên một quan sát và đi một bước theo gradient của hàm lỗi trên riêng quan sát đó, nên mỗi bước rẻ hơn $10^6$ lần. Kì vọng của véc-tơ này theo quan sát được chọn bằng gradient của $L_S$.

**Câu hỏi.** Mỗi bước của SGD có làm $L_S$ giảm không? Nếu không, SGD bảo đảm được gì sau $T$ bước, và cần bao nhiêu bước?

Không nhất thiết, kể cả theo kì vọng. Trên mẫu ba quan sát ở §6, từ một điểm lặp (iterate) có $L_S=0{,}0639$, cả ba lựa chọn quan sát đều làm $L_S$ tăng, lên $0{,}0694$, $0{,}0710$ hoặc $0{,}1021$ (trung bình $0{,}0808$). Một bước GD với cùng độ dài bước (step size, còn gọi là tốc độ học) đưa $L_S$ xuống $0{,}0614$. Kì vọng của véc-tơ được rút bằng gradient tại điểm hiện tại. Bước đi còn mang phần nhiễu, và phần nhiễu có thể lớn hơn phần giảm do gradient.

Bảo đảm của SGD (§7) là một cận kì vọng tại trung bình các điểm lặp. Với hàm lỗi logistic ở §3, $10^4$ bước đủ để độ chênh tối ưu kì vọng không quá $0{,}05$ so với giá trị nhỏ nhất của $L_S$ trên quả cầu $\lVert w\rVert\le5$. Số gradient phải tính bằng $1\%$ số gradient của một bước GD. Theo cận tương ứng, $10^4$ bước GD cũng đủ, mỗi bước $10^6$ gradient.

Mọi cận của bài chặn độ chênh tối ưu của chính hàm mục tiêu mà thuật toán tối thiểu hóa, ở đây là $L_S$. Quan hệ với rủi ro kì vọng (population risk) $L_D$ là câu hỏi cuối buổi (§13).

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Chứng minh cận kì vọng cho hạ gradient ngẫu nhiên có chiếu trên một hàm mục tiêu lồi, và chỉ ra bước nào dùng phép chiếu, bước nào dùng tính lồi, bước nào dùng tính không chệch của oracle và bước nào dùng cận mô-men bậc hai.
2. Phát biểu tính không chệch có điều kiện của gradient ngẫu nhiên khi biết lịch sử, và kiểm tra nó cho cách rút một quan sát ngẫu nhiên có hoàn lại từ mẫu huấn luyện.
3. Chọn độ dài bước và số vòng lặp từ cận để đạt một độ chênh tối ưu cho trước theo kì vọng, và tính số vòng lặp cần thêm khi muốn bảo đảm với xác suất cao.
4. So sánh hạ gradient, hạ gradient ngẫu nhiên và hạ gradient với lô nhỏ theo số lần cập nhật và theo số quan sát phải xử lý.
5. Dựng phản ví dụ khi bỏ tính lồi, cận mô-men bậc hai hay tính không chệch của oracle, và giải thích vì sao cận không nói gì về điểm lặp cuối.

## Kiến thức tiên quyết

- **Từ Bài 01.**
  - **Thuật toán học:** Định nghĩa 01.4 và đoạn sau Định nghĩa 01.18.
  - **Rủi ro thực nghiệm và ERM xấp xỉ:** Định nghĩa 01.6, 01.12 và hai mức (O1), (O2).
  - **Hồi quy tuyến tính với hàm lỗi bình phương (squared loss):** Ví dụ 01.3.
  - **Cận dưới đúng:** Nhận xét 01.26.
- **Từ Bài 02.** Giả thiết (T1); bất đẳng thức Markov (Bổ đề 02.2).
- **Từ Bài 03.** Nửa không gian thuần nhất $h_{w,0}(x)=\mathbb 1[\langle w,x\rangle\ge0]$ (Định nghĩa 03.7) và hàm lỗi 0–1 (0–1 loss).
- **Từ Bài 04.** Sai số ước lượng (Định nghĩa 04.1), sai số tối ưu thực nghiệm (Định nghĩa 04.2), Mệnh đề 04.3.
- **Giải tích.** Tích vô hướng $\langle\cdot,\cdot\rangle$, chuẩn Euclid $\lVert\cdot\rVert$; khai triển $\lVert a-a'\rVert^2=\lVert a\rVert^2-2\langle a,a'\rangle+\lVert a'\rVert^2$; bất đẳng thức Cauchy–Schwarz; đạo hàm theo hướng.
- **Xác suất.** $\sigma$-đại số ($\sigma$-algebra) sinh bởi các biến ngẫu nhiên; kì vọng có điều kiện (conditional expectation); tính chất tháp (tower property) $\mathbb E\,\mathbb E[V\mid\mathcal G]=\mathbb EV$; quy tắc lấy ra đại lượng đã biết (taking out what is known); biến ngẫu nhiên độc lập.

**Câu hỏi ôn nhanh.**

1. Cho $a=(1,0)$ và $a'=(0{,}5;0{,}5)$. Tính $\lVert a-a'\rVert^2$ trực tiếp và qua $\lVert a\rVert^2-2\langle a,a'\rangle+\lVert a'\rVert^2$.
2. Biến ngẫu nhiên $V\ge0$ có $\mathbb EV\le0{,}02$. Chặn $\Pr(V\ge0{,}1)$.
3. Chỉ số $I$ có phân bố đều trên $\{1,2,3\}$, với $q_1=0$, $q_2=2$, $q_3=0$. Tính $\mathbb Eq_I$, $\mathbb Eq_I^2$ và kiểm tra $\mathbb Eq_I^2=(\mathbb Eq_I)^2+\operatorname{Var}(q_I)$.

::: solution Lời giải câu hỏi ôn nhanh
1. Ta có $a-a'=(0{,}5;-0{,}5)$, nên $\lVert a-a'\rVert^2=0{,}25+0{,}25=0{,}5$. Theo khai triển,
$$
\begin{aligned}
&\lVert a\rVert^2-2\langle a,a'\rangle+\lVert a'\rVert^2\\
&\quad=1-2\cdot0{,}5+0{,}5\\
&\quad=0{,}5 .
\end{aligned}
$$
2. Theo Bổ đề 02.2 với $\alpha=0{,}1$,
$$
\begin{aligned}
&\Pr(V\ge0{,}1)\\
&\quad\le\frac{0{,}02}{0{,}1}=0{,}2 .
\end{aligned}
$$
3. Ta có $\mathbb Eq_I=\tfrac13(0+2+0)=\tfrac23$ và $\mathbb Eq_I^2=\tfrac13(0+4+0)=\tfrac43$. Các độ lệch $q_i-\tfrac23$ là $-\tfrac23$, $\tfrac43$, $-\tfrac23$, nên
$$
\begin{aligned}
\operatorname{Var}(q_I)&=\tfrac13\big(\tfrac49+\tfrac{16}9+\tfrac49\big)\\
&=\tfrac89,
\end{aligned}
$$
và $(\mathbb Eq_I)^2+\operatorname{Var}(q_I)=\tfrac49+\tfrac89=\tfrac43$.
:::

## 1. Thiết lập bài toán

Bài toán có tám thành phần, tương ứng với §1 Bài 01 nhưng nhìn từ phía bộ giải: mẫu đã có, và cần tính một nghiệm gần tối ưu của một hàm mục tiêu với chi phí cho trước.

1. **Hàm mục tiêu.** Một hàm $F:\mathbb R^p\to\mathbb R$ của véc-tơ tham số $w$; trường hợp chính là $F=L_S$ với mẫu $S$ đã cố định.
2. **Tập tham số.** $W\subset\mathbb R^p$, khác rỗng, đóng và lồi (khái niệm ở §4); trong các ví dụ, $W$ là một quả cầu.
3. **Dữ liệu.** Mẫu $S=(z_1,\ldots,z_m)$ đã quan sát và cố định; mọi xác suất lấy theo nguồn ngẫu nhiên của thuật toán, trừ khi nói khác.
4. **Nguồn ngẫu nhiên của thuật toán.** Các lần rút độc lập $\xi_1,\xi_2,\ldots$, chẳng hạn chỉ số rút đều có hoàn lại từ $S$ (§6).
5. **Thuật toán.** GD có chiếu và SGD có chiếu, với độ dài bước $\eta>0$ hằng và số vòng lặp $T$ chọn trước.
6. **Đầu ra.** Trung bình của các điểm lặp (§6).
7. **Đối tượng so sánh.** Một điểm $u\in W$ bất kì; khi tồn tại, một nghiệm tối ưu $w^*$ của $F$ trên $W$; hoặc cận dưới đúng của $F$ trên $W$. *Độ chênh tối ưu* của $w\in W$ là $F(w)-F(u)$ so với $u$, hoặc $F(w)-\inf_{w'\in W}F(w')$ so với cả $W$; khi $F=L_S$, đại lượng sau là sai số tối ưu thực nghiệm $\operatorname{opt}_S$ (Định nghĩa 04.2, §9).
8. **Tài nguyên.** Số vòng lặp $T$ và số gradient trên một quan sát: một vòng GD trên $L_S$ tốn $m$, một vòng SGD tốn một.

Các đại lượng của bài chia theo nguồn ngẫu nhiên như bảng dưới.

| Loại | Đại lượng |
|---|---|
| Cố định | $S$, $F$, $W$, điểm khởi tạo $w_1$, $\eta$, $T$, các hằng số trong cận, mọi $u\in W$ và $F(u)$, $\inf_{w\in W}F(w)$ |
| Ngẫu nhiên theo $\xi_1,\xi_2,\ldots$ | chỉ số rút ở mỗi bước, gradient ngẫu nhiên, các điểm lặp từ $w_2$, trung bình các điểm lặp và giá trị của $F$ tại đó |

Với GD, dòng thứ hai trống và mọi cận là tất định. Ở §9, khi $S\sim D^m$, các đại lượng của dòng thứ nhất trở thành hàm của $S$; các cận của bài đúng với mọi giá trị của $S$.

## 2. Kí hiệu và giả thiết

Bảng dưới gồm các kí hiệu riêng dùng từ §3; kí hiệu khác được đặt tên tại định nghĩa.

| Kí hiệu | Ý nghĩa |
|---|---|
| $w\in\mathbb R^p$ | véc-tơ tham số |
| $h_w(x)=\langle w,x\rangle$ | *hàm điểm số* (score function) $\mathcal X\to\mathbb R$, trong hồi quy và trong phân lớp |
| $h_{w,0}=\mathbb 1[h_w\ge0]$ | hàm phân lớp của Định nghĩa 03.7, chỉ dùng cho lỗi 0–1 |
| $\ell(w,z)$, $L_S(w)$, $L_D(w)$ | viết thay cho $\ell(h_w,z)$, $L_S(h_w)$, $L_D(h_w)$, với hàm lỗi của dự đoán thực $h_w(x)$ |
| $\eta$, $T$ | độ dài bước hằng (không chỉ số, khác $\eta(x)$ của Bài 01), số vòng lặp |
| $\xi$ | nguồn ngẫu nhiên của thuật toán |
| $\tilde y=2y-1$ | nhãn $\pm1$ ứng với nhãn $y\in\{0,1\}$ |
| $B$ | bán kính của $W$ khi $W$ là một quả cầu tâm $0$ (khác cận $\lvert Y\rvert\le B$ của Bài 04) |
| $C_x$, $C_y$ | cận của $\lVert x\rVert$ và của $\lvert y\rvert$ trên dữ liệu |

Giả thiết thống kê (T1) (các quan sát độc lập cùng phân bố $D$) chỉ được dùng ở §9 và ở câu hỏi cuối buổi, vì $S$ cố định. Giả thiết tối ưu được nêu ở chỗ dùng: (G1) oracle không chệch, (G2) mô-men bậc hai bị chặn (§6) và (C) tính lồi của hàm mục tiêu và tập tham số (§7).

## 3. Ví dụ xuyên suốt

::: example Ví dụ 05.1 (Hồi quy ba quan sát trong mặt phẳng)
**Thiết lập.** Cho $p=2$, $\mathcal X=\mathbb R^2$, $\mathcal Y=\mathbb R$ và mẫu cố định
$$
\begin{aligned}
z_1&=((1,0),\,1),\\
z_2&=((0,1),\,-1),\\
z_3&=((0{,}6;0{,}8),\,0).
\end{aligned}
$$
Lớp giả thuyết gồm các hàm $h_w(x)=\langle w,x\rangle$ của Ví dụ 01.3, với hàm lỗi bình phương $\ell(w,(x,y))=(\langle w,x\rangle-y)^2$. Hàm mục tiêu là $F=L_S$. Ví dụ chưa có đại lượng ngẫu nhiên nào; nguồn ngẫu nhiên được thêm ở §6.

**Bước 1: cận dữ liệu.** Ta có $\lVert x_i\rVert=1$ với mọi $i$ (với $x_3$: $0{,}36+0{,}64=1$) và $\lvert y_i\rvert\le1$, nên $C_x=C_y=1$.

**Bước 2: giá trị tại $w=0$.** Ba hàm lỗi tại $w=0$ bằng $y_i^2$, tức $1$, $1$ và $0$. Do đó
$$
\begin{aligned}
L_S(0)&=\tfrac13(1+1+0)\\
&=\tfrac23\approx0{,}6667 .
\end{aligned}
$$

**Bước 3: chi phí của một gradient.** Gradient của $L_S$ là trung bình của ba gradient của hàm lỗi trên từng quan sát (§4); với $m$ quan sát, nó cần $m$ véc-tơ như vậy.

**Kết luận.** Hàm mục tiêu là $L_S$ của mẫu đã cho, không phải rủi ro kì vọng; ràng buộc $\lVert w\rVert\le1$ được thêm ở §6.
:::

::: application Hồi quy logistic trên một triệu hồ sơ
**Đặc trưng.** Có $m=10^6$ hồ sơ. Véc-tơ $x$ gồm các chỉ số đo đã chuẩn hóa và một tọa độ hằng thay cho hệ số tự do, chia tỉ lệ sao cho $\lVert x\rVert\le1$. Nhãn $y\in\{0,1\}$ và $\tilde y=2y-1$.

**Hàm lỗi.** Hồi quy logistic (logistic regression) dùng hàm lỗi logistic của hàm điểm số $h_w$,
$$
\ell(w,(x,y))=\ln\big(1+e^{-\tilde y\langle w,x\rangle}\big),
$$
thay cho hàm lỗi 0–1 của $h_{w,0}$, vì hàm lỗi 0–1 không lồi theo $w$ (§4).

**Tập tham số.** $W=\{w:\lVert w\rVert\le B\}$ với $B=5$ (giá trị giả định); $w_1=0$.

**Câu hỏi thực hành.** Cần bao nhiêu bước SGD và bao nhiêu bước GD để độ chênh tối ưu của $L_S$ không quá $0{,}05$, và mỗi phương pháp tính bao nhiêu gradient trên một quan sát? Ứng dụng không dùng số liệu thật.
:::

Trong cả hai ví dụ, hàm lỗi trên từng quan sát là một hàm lồi của $w$ (định nghĩa và kiểm tra ở §4 và Bài tập 05.8).

## 4. Hàm lồi, dưới gradient và tính Lipschitz

Hàm lỗi 0–1 của Bài 01–04 không lồi theo $w$, và hàm lỗi bản lề (hinge loss) không khả vi tại các điểm gãy, nơi $\tilde y\langle w,x\rangle=1$. Một phương pháp dùng gradient cần một véc-tơ đóng vai gradient ở những điểm không khả vi, và một điều kiện để từ thông tin tại một điểm suy ra được cận dưới cho $F$ trên toàn không gian.

::: definition Định nghĩa 05.1 (Tập lồi và hàm lồi)
Cho $p\ge1$. Tính lồi được định nghĩa cho tập và cho hàm.

- **Tập lồi.** Tập $W\subset\mathbb R^p$ là *tập lồi* (convex set) nếu $\alpha w+(1-\alpha)u\in W$ với mọi $w,u\in W$ và mọi $\alpha\in[0,1]$.
- **Hàm lồi.** Hàm $F:\mathbb R^p\to\mathbb R$ là *hàm lồi* nếu với mọi $w,u\in\mathbb R^p$ và mọi $\alpha\in[0,1]$,
  $$
  \begin{aligned}
  &F(\alpha w+(1-\alpha)u)\\
  &\quad\le\alpha F(w)\\
  &\qquad+(1-\alpha)F(u).
  \end{aligned}
  $$
:::

Đồ thị của hàm lồi nằm dưới mọi dây cung. Hàm lồi ở đây nhận giá trị hữu hạn trên toàn $\mathbb R^p$.

Từ định nghĩa suy ra *bất đẳng thức lồi hữu hạn* (còn gọi là bất đẳng thức Jensen hữu hạn): với $w_1,\ldots,w_k\in\mathbb R^p$, $\alpha_t\ge0$ và $\sum_{t=1}^k\alpha_t=1$,
$$
F\Big(\sum_{t=1}^k\alpha_tw_t\Big)\le\sum_{t=1}^k\alpha_tF(w_t).
$$
Chứng minh bằng quy nạp theo $k$. Với $k\ge2$ và $\alpha_k<1$, viết $\sum_t\alpha_tw_t=(1-\alpha_k)\bar v+\alpha_kw_k$ với $\bar v=\sum_{t<k}\frac{\alpha_t}{1-\alpha_k}w_t$; áp dụng Định nghĩa 05.1 cho cặp $(\bar v,w_k)$ rồi giả thiết quy nạp cho $\bar v$. Cùng lập luận cho thấy một tổ hợp lồi hữu hạn của các điểm thuộc tập lồi $W$ thuộc $W$. Bất đẳng thức này áp dụng cho từng dãy điểm cố định và không chứa kì vọng.

Các tập và hàm sau là lồi: quả cầu $\{w:\lVert w\rVert\le B\}$; hàm $w\mapsto\lVert w\rVert^2$; hàm $w\mapsto(\langle w,x\rangle-y)^2$ với $(x,y)$ cố định; cực đại của hai hàm afin. Các tập và hàm sau không lồi: tập $\{-1,1\}\subset\mathbb R$ và mặt cầu $\{w:\lVert w\rVert=1\}$; hàm $f(w)=(w^2-1)^2$ trên $\mathbb R$, vì $f(0)=1>\tfrac12f(-1)+\tfrac12f(1)=0$; rủi ro thực nghiệm với hàm lỗi 0–1, xem như hàm của $w$ (Bài tập 05.7).

::: definition Định nghĩa 05.2 (Dưới gradient và dưới vi phân)
Cho $F:\mathbb R^p\to\mathbb R$ và $w\in\mathbb R^p$. Véc-tơ $v\in\mathbb R^p$ là một *dưới gradient* của $F$ tại $w$ nếu với mọi $u\in\mathbb R^p$,
$$
F(u)\ge F(w)+\langle v,u-w\rangle .
$$
Bất đẳng thức này được gọi là *bất đẳng thức dưới gradient* (subgradient inequality). Tập mọi dưới gradient của $F$ tại $w$ là *dưới vi phân* (subdifferential) của $F$ tại $w$, kí hiệu $\partial F(w)$.
:::

Theo bất đẳng thức dưới gradient, đồ thị của $F$ nằm trên siêu phẳng afin đi qua $(w,F(w))$ với hệ số góc $v$. Với $v=0$, bất đẳng thức trở thành $F(u)\ge F(w)$ với mọi $u$; vậy $0\in\partial F(w)$ khi và chỉ khi $w$ là điểm cực tiểu toàn cục của $F$ trên $\mathbb R^p$.

Với $F$ lồi và hữu hạn trên $\mathbb R^p$, dưới vi phân tại mọi điểm khác rỗng, và $\partial F(w)=\{\nabla F(w)\}$ khi $F$ khả vi tại $w$ (UML §14.2). Chỉ bao hàm $\nabla F(w)\in\partial F(w)$ được dùng; nó được chứng minh ngay sau đây.

Với $f(w)=\lvert w\rvert$ trên $\mathbb R$, ta có $\partial f(w)=\{1\}$ khi $w>0$, $\partial f(w)=\{-1\}$ khi $w<0$, và $\partial f(0)=[-1,1]$: tại $0$, mọi $v$ với $\lvert v\rvert\le1$ thỏa $\lvert u\rvert\ge vu$. Hàm không lồi $f(w)=(w^2-1)^2$ có $f'(0)=0$, nhưng $0\notin\partial f(0)$ vì $f(1)=0<f(0)=1$. Một điểm có gradient bằng $0$ được gọi là *điểm dừng* (stationary point); với hàm không lồi, điểm dừng không nhất thiết là cực tiểu toàn cục.

::: proposition Mệnh đề 05.3 (Ba quy tắc tính dưới gradient) — chứng minh đầy đủ
**Giả thiết.**

- **Hàm.** $F,F_1,\ldots,F_m:\mathbb R^p\to\mathbb R$; $F$ lồi ở phần (a).
- **Điểm.** $w\in\mathbb R^p$.

**Bảo đảm.** Ba khẳng định tất định.

- **(a) Hàm khả vi.** Nếu $F$ lồi và khả vi tại $w$ thì $\nabla F(w)\in\partial F(w)$.
- **(b) Trung bình.** Nếu $v_i\in\partial F_i(w)$ với $i=1,\ldots,m$ thì
  $$
  \begin{aligned}
  &\frac1m\sum_{i=1}^mv_i\\
  &\quad\in\partial\Big(\frac1m\sum_{i=1}^mF_i\Big)(w).
  \end{aligned}
  $$
- **(c) Cực đại.** Nếu $F=\max\{F_1,\ldots,F_m\}$, $F_j(w)=F(w)$ và $v\in\partial F_j(w)$ thì $v\in\partial F(w)$.
:::

::: proof Chứng minh Mệnh đề 05.3
**Lộ trình.** Phần (a) dùng định nghĩa hàm lồi trên một đoạn thẳng ngắn dần; phần (b) và (c) chỉ dùng bất đẳng thức dưới gradient.

**Bước 1 (phần a).** Cố định $u\in\mathbb R^p$. Với $\alpha\in(0,1]$, Định nghĩa 05.1 cho
$$
\begin{aligned}
&F(w+\alpha(u-w))\\
&\quad\le(1-\alpha)F(w)+\alpha F(u).
\end{aligned}
$$
Chuyển $F(w)$ sang vế trái và chia cho $\alpha>0$, ta được
$$
\begin{aligned}
&\frac{F(w+\alpha(u-w))-F(w)}{\alpha}\\
&\quad\le F(u)-F(w).
\end{aligned}
$$
Tính lồi của $F$ được dùng ở đây. Khi $\alpha\downarrow0$, vế trái tiến tới đạo hàm theo hướng $u-w$, bằng $\langle\nabla F(w),u-w\rangle$ vì $F$ khả vi tại $w$. Vậy $F(u)\ge F(w)+\langle\nabla F(w),u-w\rangle$ với mọi $u$.

**Bước 2 (phần b).** Cộng $m$ bất đẳng thức dưới gradient $F_i(u)\ge F_i(w)+\langle v_i,u-w\rangle$ rồi chia cho $m$.

**Bước 3 (phần c).** Với mọi $u$,
$$
\begin{aligned}
F(u)&\ge F_j(u)\\
&\ge F_j(w)+\langle v,u-w\rangle\\
&=F(w)+\langle v,u-w\rangle .
\end{aligned}
$$
Bất đẳng thức thứ nhất do $F$ là cực đại, bất đẳng thức thứ hai do $v\in\partial F_j(w)$, đẳng thức cuối do $F_j(w)=F(w)$.

$\square$ Phần (b) là lý do gradient của hàm lỗi trên một quan sát rút đều từ mẫu có trung bình là một dưới gradient của $L_S$ (§6).
:::

::: example Ví dụ 05.2 (Dưới gradient của hàm lỗi bản lề)
**Thiết lập.** Một quan sát $x=(1,2)$, $y=1$, nên $\tilde y=1$. Hàm lỗi bản lề của hàm điểm số $h_w$ trên quan sát này là
$$
\ell(w)=\max\{0,\,1-\tilde y\langle w,x\rangle\},
$$
cực đại của hai hàm afin, nên lồi. Hai nhánh có gradient $0$ và $-\tilde yx=(-1,-2)$.

**Bước 1: điểm $w=0$.** Tại $w=0$, $\tilde y\langle w,x\rangle=0<1$, nên chỉ nhánh $1-\tilde y\langle w,x\rangle$ đạt cực đại, và $\ell(0)=1$. Theo Mệnh đề 05.3(a) và (c), $(-1,-2)$ là một dưới gradient tại $0$.

**Bước 2: điểm gãy $w_0=(0{,}5;0{,}25)$.** Tại $w_0$, $\langle w_0,x\rangle=0{,}5+0{,}5=1$, nên hai nhánh cùng bằng $0$. Theo Mệnh đề 05.3(c), cả $0$ và $(-1,-2)$ là dưới gradient tại $w_0$. Với $\alpha\in[0,1]$, nhân bất đẳng thức dưới gradient của $(-1,-2)$ với $\alpha$, của $0$ với $1-\alpha$, rồi cộng; ta thấy $(-\alpha,-2\alpha)$ cũng là dưới gradient.

**Bước 3: ngoài đoạn $[0,1]$.** Với $\alpha=1{,}2$, tức $v=(-1{,}2;-2{,}4)$, lấy $u=w_0-0{,}1x=(0{,}4;0{,}05)$. Khi đó $\langle u,x\rangle=0{,}4+0{,}1=0{,}5$, nên $\ell(u)=0{,}5$, trong khi
$$
\begin{aligned}
&\ell(w_0)+\langle v,u-w_0\rangle\\
&\quad=0+(-1{,}2)(-0{,}1)\\
&\qquad+(-2{,}4)(-0{,}2)\\
&\quad=0{,}6>0{,}5 .
\end{aligned}
$$
Bất đẳng thức dưới gradient sai, nên $(-1{,}2;-2{,}4)\notin\partial\ell(w_0)$.

**Bước 4: điểm $w=(1,1)$.** Tại $w=(1,1)$, $\langle w,x\rangle=3>1$, nên $\ell=0$ gần $w$ và $0$ là một dưới gradient.

**Kết luận.** Tại điểm gãy, dưới vi phân chứa đoạn nối $0$ và $(-1,-2)$ và không chứa $(-1{,}2;-2{,}4)$; Bài tập 05.1 chứng minh nó đúng bằng đoạn này. Ngoài điểm gãy, dưới vi phân có một phần tử.
:::

::: example Ví dụ 05.3 (Tính lồi và gradient trong ví dụ hồi quy)
**Thiết lập.** Mẫu và hàm lỗi bình phương của Ví dụ 05.1.

**Bước 1: tính lồi.** Hàm $s\mapsto(s-y)^2$ lồi trên $\mathbb R$ và $\langle\alpha w+(1-\alpha)u,x\rangle=\alpha\langle w,x\rangle+(1-\alpha)\langle u,x\rangle$, nên $w\mapsto\ell(w,z)$ thỏa Định nghĩa 05.1. Cộng ba bất đẳng thức đó rồi chia cho $3$, ta thấy $L_S$ lồi.

**Bước 2: gradient trên một quan sát.** Theo quy tắc đạo hàm hàm hợp,
$$
\begin{aligned}
&\nabla_w\ell(w,(x,y))\\
&\quad=2(\langle w,x\rangle-y)\,x .
\end{aligned}
$$
Tại $w=0$, ba véc-tơ này là $-2y_ix_i$:
$$
(-2,0),\quad(0,2),\quad(0,0).
$$

**Bước 3: gradient đầy đủ.** Theo Mệnh đề 05.3(a) và (b),
$$
\begin{aligned}
&\nabla L_S(0)\\
&\quad=\tfrac13\big[(-2,0)+(0,2)\\
&\qquad+(0,0)\big]\\
&\quad=\big(-\tfrac23,\tfrac23\big).
\end{aligned}
$$

**Kết luận.** Rút đều một chỉ số cho một véc-tơ có trung bình bằng $\nabla L_S(0)$.
:::

Bước đi theo dưới gradient cần thêm một cận cho độ dài của nó.

::: definition Định nghĩa 05.4 (Hàm Lipschitz)
Cho $C\subset\mathbb R^p$ và $G\ge0$. Hàm $F:\mathbb R^p\to\mathbb R$ là *$G$-Lipschitz* trên $C$ nếu với mọi $w,u\in C$,
$$
\lvert F(w)-F(u)\rvert\le G\lVert w-u\rVert .
$$
:::

Giá trị của $F$ thay đổi không quá $G$ lần khoảng cách giữa hai điểm. Hàm lỗi bản lề và hàm lỗi logistic là $\lVert x\rVert$-Lipschitz trên $\mathbb R^p$ như hàm của $w$ (Bài tập 05.8, 05.9). Hàm $w\mapsto w^2$ không Lipschitz trên $\mathbb R$, vì $\lvert w^2-0^2\rvert/\lvert w-0\rvert=\lvert w\rvert$ không bị chặn. Tương tự, hàm lỗi bình phương không Lipschitz trên toàn $\mathbb R^p$. Trên quả cầu bán kính $B$, với $\lVert x\rVert\le C_x$ và $\lvert y\rvert\le C_y$, gradient $2(\langle w,x\rangle-y)x$ có chuẩn không quá $2(BC_x+C_y)C_x$, nên theo phần (a) của mệnh đề dưới đây, hàm lỗi là $2(BC_x+C_y)C_x$-Lipschitz trên quả cầu.

::: proposition Mệnh đề 05.5 (Hằng số Lipschitz và chuẩn của dưới gradient) — chứng minh đầy đủ
**Giả thiết.**

- **Hàm.** $F:\mathbb R^p\to\mathbb R$ lồi.
- **Tập.** $U\subset\mathbb R^p$; ở phần (b), $U$ mở.
- **Hằng số.** $G\ge0$.

**Bảo đảm.** Hai khẳng định tất định.

- **(a) Dưới gradient bị chặn kéo theo Lipschitz.** Nếu tại mỗi $u\in U$ có một $v_u\in\partial F(u)$ với $\lVert v_u\rVert\le G$ thì $F$ là $G$-Lipschitz trên $U$.
- **(b) Lipschitz kéo theo dưới gradient bị chặn.** Nếu $F$ là $G$-Lipschitz trên $U$ thì $\lVert v\rVert\le G$ với mọi $w\in U$ và mọi $v\in\partial F(w)$.
:::

::: proof Chứng minh Mệnh đề 05.5
**Lộ trình.** Phần (a) dùng bất đẳng thức dưới gradient và Cauchy–Schwarz; phần (b) thử bất đẳng thức dưới gradient theo hướng của $v$.

**Bước 1 (phần a).** Với $w,u\in U$, bất đẳng thức dưới gradient tại $u$ với điểm $w$ cho
$$
\begin{aligned}
F(u)-F(w)&\le\langle v_u,u-w\rangle\\
&\le G\lVert u-w\rVert .
\end{aligned}
$$
Bất đẳng thức thứ hai là Cauchy–Schwarz. Đổi vai $w$ và $u$, ta được $F(w)-F(u)\le G\lVert u-w\rVert$.

**Bước 2 (phần b).** Cho $w\in U$ và $v\in\partial F(w)$ với $v\ne0$. Vì $U$ mở, điểm $u=w+\alpha v/\lVert v\rVert$ thuộc $U$ khi $\alpha>0$ đủ nhỏ; tính mở được dùng ở đây. Bất đẳng thức dưới gradient và tính Lipschitz cho
$$
\begin{aligned}
\alpha\lVert v\rVert&=\langle v,u-w\rangle\\
&\le F(u)-F(w)\\
&\le G\alpha .
\end{aligned}
$$
Chia cho $\alpha$, ta được $\lVert v\rVert\le G$.

$\square$ Phần (b) cho cận $G$ của bước GD ở §7. Trên một tập đóng, phần (b) cần $F$ Lipschitz trên một tập mở chứa tập đó, vì bất đẳng thức dưới gradient đòi mọi $u\in\mathbb R^p$; vì vậy $F$ được giả sử hữu hạn trên $\mathbb R^p$.
:::

Không kết quả nào của bài dùng hai tính chất sau. Tính lồi mạnh là giả thiết của cận nhanh hơn trong UML §14.4.4.

::: definition Định nghĩa 05.6 (Hàm trơn và hàm lồi mạnh)
Cho $F:\mathbb R^p\to\mathbb R$, $\beta>0$ và $\lambda>0$.

- **Trơn.** $F$ là *$\beta$-trơn* ($\beta$-smooth) nếu $F$ khả vi và $\lVert\nabla F(w)-\nabla F(u)\rVert\le\beta\lVert w-u\rVert$ với mọi $w,u$.
- **Lồi mạnh.** $F$ là *$\lambda$-lồi mạnh* ($\lambda$-strongly convex) nếu với mọi $w,u$ và mọi $\alpha\in[0,1]$,
  $$
  \begin{aligned}
  &F(\alpha w+(1-\alpha)u)\\
  &\le\alpha F(w)+(1-\alpha)F(u)\\
  &\quad-\tfrac\lambda2\alpha(1-\alpha)\lVert w-u\rVert^2 .
  \end{aligned}
  $$
:::

Hàm $\beta$-trơn có gradient thay đổi không quá $\beta$ lần khoảng cách; hàm $\lambda$-lồi mạnh nằm dưới dây cung ít nhất một lượng bậc hai. Hằng số $\beta$ khác hàm $\beta(m,\delta)$ của Bài 01; $\lambda$ trùng hệ số chính quy hóa của Bài 06, vì $\tfrac\lambda2\lVert w\rVert^2$ là $\lambda$-lồi mạnh. Trong Ví dụ 05.1, $L_S$ là $\tfrac23$-lồi mạnh và $\tfrac43$-trơn (Bài tập 05.12); hàm lỗi bản lề không trơn và không lồi mạnh.

Mỗi dưới gradient, theo định nghĩa, cho một cận dưới toàn cục của $F$; với $F$ lồi, dưới gradient tồn tại tại mọi điểm và gradient là một dưới gradient (Mệnh đề 05.3(a)). Cận $G$ trên chuẩn của dưới gradient chặn độ dài mỗi bước.

## 5. Phép chiếu lên tập lồi đóng

Trong Ví dụ 05.3, gradient của hàm lỗi bình phương là $2(\langle w,x\rangle-y)x$, nên chuẩn của nó tăng theo $\lVert w\rVert$; một cận $G$ chỉ đúng trên một tập bị chặn. Thuật toán cần đưa mỗi điểm lặp trở lại tập đó mà không làm tăng khoảng cách tới các điểm của tập.

::: definition Định nghĩa 05.7 (Phép chiếu Euclid lên tập lồi đóng)
Cho $W\subset\mathbb R^p$ khác rỗng, đóng, lồi và $\theta\in\mathbb R^p$. *Phép chiếu Euclid* (Euclidean projection) của $\theta$ lên $W$ là điểm $\operatorname{proj}_W(\theta)\in W$ thỏa
$$
\lVert \theta-\operatorname{proj}_W(\theta)\rVert=\min_{u\in W}\lVert \theta-u\rVert .
$$
:::

Điểm gần nhất này tồn tại vì $W$ đóng và duy nhất vì $W$ lồi (Phụ lục A). Ta có $\operatorname{proj}_W(\theta)=\theta$ khi và chỉ khi $\theta\in W$; với $W=\mathbb R^p$, phép chiếu là ánh xạ đồng nhất. Bỏ một trong hai giả thiết, định nghĩa hỏng.

Với $W=\{-1,1\}\subset\mathbb R$ (không lồi) và $\theta=0$, có hai điểm gần nhất. Với $W$ là quả cầu mở $\{w:\lVert w\rVert<1\}$ (không đóng) và $\theta$ ở ngoài $W$, không có điểm gần nhất.

::: lemma Bổ đề 05.8 (Bất đẳng thức của phép chiếu) — phác thảo (chứng minh đầy đủ ở Phụ lục A)
**Giả thiết.** $W\subset\mathbb R^p$ khác rỗng, đóng, lồi; $\theta\in\mathbb R^p$; $\pi=\operatorname{proj}_W(\theta)$.

**Bảo đảm.** Hai khẳng định tất định.

- **(a) Bất đẳng thức biến phân.** $\pi$ là điểm duy nhất của $W$ thỏa, với mọi $u\in W$,
  $$
  \langle \theta-\pi,\,u-\pi\rangle\le0 .
  $$
- **(b) Khoảng cách tới các điểm của $W$.** Với mọi $u\in W$,
  $$
  \begin{aligned}
  &\lVert\pi-u\rVert^2\\
  &\quad\le\lVert \theta-u\rVert^2\\
  &\qquad-\lVert \theta-\pi\rVert^2\\
  &\quad\le\lVert \theta-u\rVert^2 .
  \end{aligned}
  $$
:::

Bất đẳng thức ở (a) được gọi là *bất đẳng thức biến phân* (variational inequality): góc giữa $\theta-\pi$ và mọi hướng từ $\pi$ vào $W$ là góc vuông hoặc góc tù.

::: proof Chứng minh Bổ đề 05.8 (phác thảo)
**Lộ trình.** Phần (b) suy ra từ (a) bằng khai triển bình phương. Bước 2 chỉ chứng minh rằng $\pi$ thỏa bất đẳng thức biến phân; tính duy nhất ở (a) nằm ở Phụ lục A.

**Bước 1 (phần b từ phần a).** Viết $\theta-u=(\theta-\pi)+(\pi-u)$ và khai triển:
$$
\begin{aligned}
&\lVert \theta-u\rVert^2\\
&\quad=\lVert \theta-\pi\rVert^2+\lVert\pi-u\rVert^2\\
&\qquad+2\langle \theta-\pi,\pi-u\rangle .
\end{aligned}
$$
Theo (a), $\langle \theta-\pi,\pi-u\rangle=-\langle \theta-\pi,u-\pi\rangle\ge0$. Bỏ số hạng này ta được bất đẳng thức thứ nhất của (b); bất đẳng thức thứ hai do $\lVert \theta-\pi\rVert^2\ge0$.

**Bước 2 (ý của phần a).** Cho $u\in W$. Vì $W$ lồi, điểm $\pi+\alpha(u-\pi)$ thuộc $W$ với mọi $\alpha\in[0,1]$; tính lồi của $W$ được dùng ở đây. Hàm
$$
\alpha\mapsto\lVert\pi+\alpha(u-\pi)-\theta\rVert^2
$$
đạt giá trị nhỏ nhất trên $[0,1]$ tại $\alpha=0$, theo định nghĩa của $\pi$. Do đó đạo hàm phải của hàm này tại $0$, bằng $-2\langle \theta-\pi,u-\pi\rangle$, không âm.

$\square$ Phần (b) là chỗ duy nhất phép chiếu đi vào chứng minh ở §7.
:::

Cộng hai bất đẳng thức biến phân cho $\theta$ và $\theta'$ rồi dùng Cauchy–Schwarz, ta được $\lVert\operatorname{proj}_W(\theta)-\operatorname{proj}_W(\theta')\rVert\le\lVert \theta-\theta'\rVert$, tức phép chiếu *không giãn* (nonexpansive) (Phụ lục A). Tính không giãn kéo theo tính liên tục của phép chiếu, cần cho tính đo được của các điểm lặp (Phụ lục B); chứng minh của định lý chính không dùng nó trực tiếp.

::: example Ví dụ 05.4 (Phép chiếu lên quả cầu)
**Thiết lập.** $W=\{w:\lVert w\rVert\le B\}$ với $B>0$.

**Bước 1: công thức.** Phép chiếu là
$$
\begin{aligned}
&\operatorname{proj}_W(\theta)\\
&\quad=\begin{cases}\theta,&\lVert \theta\rVert\le B,\\ B\theta/\lVert \theta\rVert,&\lVert \theta\rVert>B.\end{cases}
\end{aligned}
$$

**Bước 2: kiểm tra bất đẳng thức biến phân.** Xét $\lVert \theta\rVert>B$ và $\pi=B\theta/\lVert \theta\rVert$, nên $\theta-\pi=(1-B/\lVert \theta\rVert)\theta$. Với $u\in W$,
$$
\begin{aligned}
&\langle \theta-\pi,u-\pi\rangle\\
&\quad=\Big(1-\frac B{\lVert \theta\rVert}\Big)\\
&\qquad\cdot\big(\langle \theta,u\rangle-B\lVert \theta\rVert\big)\\
&\quad\le0,
\end{aligned}
$$
vì thừa số thứ nhất dương và $\langle \theta,u\rangle\le\lVert \theta\rVert\,\lVert u\rVert\le B\lVert \theta\rVert$ (Cauchy–Schwarz). Theo tính duy nhất ở Bổ đề 05.8(a), $\pi$ là phép chiếu.

**Bước 3: bằng số.** Lấy $B=1$ và $\theta=(1,-1)$. Khi đó $\lVert \theta\rVert=\sqrt2\approx1{,}4142>1$ và
$$
\begin{aligned}
\pi&=\tfrac1{\sqrt2}(1,-1)\\
&\approx(0{,}7071;-0{,}7071).
\end{aligned}
$$
Với $u=(1,0)\in W$, ta có $\pi-u\approx(-0{,}2929;-0{,}7071)$, nên $\lVert\pi-u\rVert\approx\sqrt{0{,}0858+0{,}5}\approx0{,}7654$, nhỏ hơn $\lVert\theta-u\rVert=1$. Với $\theta-\pi\approx(0{,}2929;-0{,}2929)$ và $u-\pi\approx(0{,}2929;0{,}7071)$, ta có $\langle\theta-\pi,u-\pi\rangle\approx0{,}0858-0{,}2071=-0{,}1213\le0$.

**Kết luận.** Chiếu lên quả cầu tốn cỡ $p$ phép tính. Véc-tơ $\theta=(1,-1)$ xuất hiện lại ở bước thứ hai của SGD (§6).
:::

Với một tập lồi đóng tổng quát, tính $\operatorname{proj}_W$ là một bài toán tối ưu riêng; các ví dụ của bài chỉ dùng quả cầu và đoạn thẳng.

## 6. Oracle gradient ngẫu nhiên và hai thuật toán

Một gradient của $L_S$ tốn $m$ gradient trên từng quan sát (Ví dụ 05.3). SGD thay nó bằng một véc-tơ ngẫu nhiên rẻ hơn, có trung bình đúng.

::: algorithm Thuật toán 05.9 (Hạ gradient có chiếu)
**Đầu vào.** Bốn thành phần sau.

- **Hàm mục tiêu.** $F:\mathbb R^p\to\mathbb R$ lồi, với một quy tắc chọn $v(w)\in\partial F(w)$ cho mỗi $w\in W$.
- **Tập tham số.** $W$ khác rỗng, đóng, lồi.
- **Độ dài bước.** $\eta>0$.
- **Số vòng lặp.** $T\ge1$.

**Khởi tạo.** $w_1\in W$.

**Cập nhật.** Với $t=1,\ldots,T$: đặt $v_t=v(w_t)$ và $w_{t+1}=\operatorname{proj}_W(w_t-\eta v_t)$.

**Đầu ra.** $\bar w_T=\frac1T\sum_{t=1}^Tw_t$.

**Điều kiện dừng.** Sau đúng $T$ vòng; $T$ chọn trước.

**Chi phí.** $T$ lần tính dưới gradient và $T$ phép chiếu; với $F=L_S$, mỗi lần tính là $m$ dưới gradient trên một quan sát.
:::

Ta gọi $\bar w_T$ là *điểm lặp trung bình* (averaged iterate) và $w_{T+1}$ là *điểm lặp cuối* (last iterate); $\bar w_T\in W$ vì $W$ lồi (§4). Tên "hạ gradient" được giữ cả khi $v_t$ là dưới gradient (UML: subgradient descent).

::: definition Định nghĩa 05.10 (Oracle gradient ngẫu nhiên và lịch sử)
Cho $F:\mathbb R^p\to\mathbb R$ lồi, $W\subset\mathbb R^p$ khác rỗng, đóng, lồi và $G\ge0$. Oracle gồm các thành phần sau.

- **Nguồn ngẫu nhiên.** Một biến ngẫu nhiên $\xi$ nhận giá trị trong tập $\Xi$, với phân bố $P_\xi$; các lần rút $\xi_1,\xi_2,\ldots$ độc lập, cùng phân bố $P_\xi$.
- **Ánh xạ oracle.** Một ánh xạ $\varphi:\mathbb R^p\times\Xi\to\mathbb R^p$, đo được theo cặp $(w,\xi)$; véc-tơ $\varphi(w,\xi)$ là *gradient ngẫu nhiên* (stochastic gradient) tại $w$.
- **Trung bình.** $\psi(w)=\mathbb E_\xi\,\varphi(w,\xi)$ với $w\in W$.
- **(G1) Tính không chệch.** $\psi(w)\in\partial F(w)$ với mọi $w\in W$.
- **(G2) Cận mô-men bậc hai.** $\mathbb E_\xi\lVert\varphi(w,\xi)\rVert^2\le G^2$ với mọi $w\in W$.
- **Lịch sử.** *Lịch sử* (history) đến bước $t$ là $\mathcal F_t=\sigma(\xi_1,\ldots,\xi_t)$ với $t\ge1$; $\mathcal F_0$ là $\sigma$-đại số tầm thường.

Cặp $(\varphi,P_\xi)$ thỏa (G1) và (G2) được gọi là một *oracle gradient ngẫu nhiên* cho $F$ trên $W$ với hằng số $G$.
:::

(G1) và (G2) là mệnh đề tất định về từng $w\in W$. Theo (G2) và bất đẳng thức Cauchy–Schwarz, $\mathbb E_\xi\lVert\varphi(w,\xi)\rVert<\infty$, nên $\psi(w)$ xác định. Khai triển bình phương như câu ôn nhanh 3, với số hạng chéo có kì vọng $0$, cho đẳng thức
$$
\begin{aligned}
&\mathbb E_\xi\lVert\varphi(w,\xi)\rVert^2\\
&=\lVert\psi(w)\rVert^2+\mathbb E_\xi\lVert\varphi(w,\xi)-\psi(w)\rVert^2,
\end{aligned}
$$
(G2) kéo theo $\lVert\psi(w)\rVert\le G$. Kì vọng có điều kiện theo $\mathcal F_{t-1}$ là trung bình theo các lần rút từ bước $t$ khi $t-1$ lần rút đầu đã biết.

Trường hợp chính là $F=L_S$ với $\Xi=\{1,\ldots,m\}$, $P_\xi$ đều, và $\varphi(w,i)=v(w,z_i)$ là một dưới gradient của $\ell(\cdot,z_i)$ tại $w$. Khi chỉ số được rút *có hoàn lại*, các $\xi_t$ độc lập, và $\psi(w)=\frac1m\sum_iv(w,z_i)\in\partial L_S(w)$ theo Mệnh đề 05.3(b).

Ba trường hợp sau nằm ngoài Định nghĩa 05.10 hoặc cho oracle của một hàm khác.

- **Phân bố rút không đều.** Oracle không chệch cho một hàm khác $L_S$ (§8).
- **Xáo trộn lại sau mỗi vòng qua dữ liệu (random reshuffling).** Rút không hoàn lại trong mỗi vòng qua dữ liệu (epoch), nên các $\xi_t$ không độc lập. Với $m=2$, lần rút thứ hai của mỗi vòng đã xác định.
- **Oracle phụ thuộc thời điểm.** $\varphi$ phụ thuộc thêm vào $t$ hay vào các điểm lặp trước, nên $g_t$ không có dạng $\varphi(w_t,\xi_t)$.

::: example Ví dụ 05.5 (Oracle rút một quan sát trong ví dụ hồi quy)
**Thiết lập.** Mẫu của Ví dụ 05.1, $W=\{w:\lVert w\rVert\le1\}$ (tức $B=1$), $\Xi=\{1,2,3\}$ với phân bố đều, và
$$
\varphi(w,i)=2(\langle w,x_i\rangle-y_i)\,x_i .
$$

**Bước 1: kiểm tra (G1).** Theo Ví dụ 05.3 và Mệnh đề 05.3(b), $\psi(w)=\frac13\sum_i\varphi(w,i)=\nabla L_S(w)$; tại $w=0$, $\psi(0)=(-\tfrac23,\tfrac23)$.

**Bước 2: kiểm tra (G2).** Với $w\in W$, theo bất đẳng thức tam giác và Cauchy–Schwarz,
$$
\begin{aligned}
&\lVert\varphi(w,i)\rVert\\
&\quad=2\lvert\langle w,x_i\rangle-y_i\rvert\,\lVert x_i\rVert\\
&\quad\le2\big(\lVert w\rVert\lVert x_i\rVert+\lvert y_i\rvert\big)\lVert x_i\rVert\\
&\quad\le2(BC_x+C_y)C_x=4 .
\end{aligned}
$$
Do đó $\mathbb E_i\lVert\varphi(w,i)\rVert^2\le16$, và (G2) đúng với $G=4$.

**Bước 3: ngoài $W$.** Tại $w=(10,0)$, ta có $\varphi(w,1)=2(10-1)(1,0)=(18,0)$, chuẩn $18>4$. Cận hỏng ngoài $W$.

**Kết luận.** (G2) cần một tập tham số bị chặn; $G=4$ là cận cho trường hợp xấu nhất trên $W$.
:::

::: algorithm Thuật toán 05.11 (Hạ gradient ngẫu nhiên có chiếu)
**Đầu vào.** Bốn thành phần sau.

- **Tập tham số.** $W$ khác rỗng, đóng, lồi.
- **Oracle.** Một oracle gradient ngẫu nhiên $(\varphi,P_\xi)$ theo Định nghĩa 05.10.
- **Độ dài bước.** $\eta>0$.
- **Số vòng lặp.** $T\ge1$.

**Khởi tạo.** $w_1\in W$, tất định.

**Cập nhật.** Với $t=1,\ldots,T$:

1. rút $\xi_t\sim P_\xi$, độc lập với các lần rút trước;
2. đặt $g_t=\varphi(w_t,\xi_t)$;
3. đặt $w_{t+1}=\operatorname{proj}_W(w_t-\eta g_t)$.

**Đầu ra.** $\bar w_T=\frac1T\sum_{t=1}^Tw_t$.

**Điều kiện dừng.** Sau đúng $T$ vòng; $T$ và $\eta$ chọn trước khi chạy, và $\eta$ có thể phụ thuộc $T$.

**Chi phí.** $T$ lần gọi oracle và $T$ phép chiếu; khi rút từ $S$ với lớp tuyến tính, mỗi lần gọi là một gradient trên một quan sát, cỡ $p$ phép tính.
:::

Điểm lặp $w_t$ chỉ phụ thuộc $\xi_1,\ldots,\xi_{t-1}$, nên $\bar w_T$ phụ thuộc $\xi_1,\ldots,\xi_{T-1}$. Đầu ra $\bar w_T$ phụ thuộc cả mẫu và các lần rút $\xi_t$, như đoạn sau Định nghĩa 01.18 đã báo trước (§9). Với $W=\mathbb R^p$, thuật toán là SGD không chiếu.

::: example Ví dụ 05.6 (Ba bước hạ gradient ngẫu nhiên có chiếu trong ví dụ hồi quy)
**Thiết lập.** Oracle của Ví dụ 05.5, $w_1=0$ và $\eta=0{,}5$, lớn để từng bước thấy rõ (không phải giá trị của §7). Các chỉ số rút được là $i_1=1$ và $i_2=2$.

**Bước 1: điểm lặp $w_2$.** Tại $w_1=0$, $g_1=\varphi(0,1)=(-2,0)$ và $w_1-\eta g_1=(1,0)$, có chuẩn $1$, nằm trong $W$. Vậy $w_2=(1,0)$. Các phần dư $\langle w_2,x_i\rangle-y_i$ là $0$, $1$, $0{,}6$, nên
$$
\begin{aligned}
L_S(w_2)&=\tfrac13(0+1+0{,}36)\\
&\approx0{,}4533 .
\end{aligned}
$$

**Bước 2: điểm lặp $w_3$.** Tại $w_2$, $g_2=\varphi(w_2,2)=2(0+1)(0,1)=(0,2)$ và $w_2-\eta g_2=(1,-1)$, có chuẩn $1{,}4142>1$. Theo Ví dụ 05.4, $w_3\approx(0{,}7071;-0{,}7071)$. Các phần dư là $-0{,}2929$, $0{,}2929$, $-0{,}1414$, nên
$$
\begin{aligned}
&L_S(w_3)\\
&\quad\approx\tfrac13(0{,}0858+0{,}0858\\
&\qquad+0{,}0200)\\
&\quad\approx0{,}0639 .
\end{aligned}
$$

**Bước 3: mọi lựa chọn ở bước thứ ba.** Với mỗi chỉ số $i_3$, ta tính $g_3$, điểm $w_3-\eta g_3$ và $w_4$ sau khi chiếu.

- **$i_3=1$.** $g_3\approx(-0{,}5858;0)$; điểm $(1;-0{,}7071)$, chuẩn $1{,}2247$, chiếu thành $w_4\approx(0{,}8165;-0{,}5774)$; $L_S(w_4)\approx0{,}0710$.
- **$i_3=2$.** $g_3\approx(0;0{,}5858)$; điểm $(0{,}7071;-1)$, chuẩn $1{,}2247$, chiếu thành $w_4\approx(0{,}5774;-0{,}8165)$; $L_S(w_4)\approx0{,}1021$.
- **$i_3=3$.** $g_3\approx(-0{,}1697;-0{,}2263)$; điểm $(0{,}7920;-0{,}5940)$, chuẩn $0{,}9899\le1$, nên $w_4$ là chính điểm này; $L_S(w_4)\approx0{,}0694$.

Trung bình theo $i_3$ là $\mathbb EL_S(w_4)\approx0{,}0808>0{,}0639$: bước thứ ba làm $L_S$ tăng với mọi lựa chọn, nên tăng cả theo kì vọng.

**Bước 4: một bước GD.** Từ $w_3$, $\nabla L_S(w_3)\approx(-0{,}2518;0{,}1198)$, nên $w_3-\eta\nabla L_S(w_3)\approx(0{,}8330;-0{,}7670)$, có chuẩn $1{,}1324>1$. Chiếu lên $W$ cho $(0{,}7356;-0{,}6774)$ và $L_S\approx0{,}0614<0{,}0639$.

**Bước 5: đối tượng so sánh.** Giá trị nhỏ nhất của $L_S$ trên $W$ là $0{,}06112$, đạt tại $w^*\approx(0{,}7473;-0{,}6645)$, trên biên của $W$ (Phụ lục D). Nghiệm bình phương tối thiểu (least squares) không ràng buộc là $(1{,}06;-0{,}92)$, có chuẩn $1{,}404>1$ và $L_S\approx0{,}00667$.

**Kết luận.** Một bước SGD có thể làm $L_S$ tăng, kể cả theo kì vọng theo chỉ số rút. Đối tượng so sánh là giá trị nhỏ nhất trên $W$, không phải trên $\mathbb R^2$.
:::

Chứng minh ở §7 chỉ dùng trung bình của gradient ngẫu nhiên khi các lần rút trước đã biết. Bổ đề sau nối hai giả thiết tất định (G1), (G2) với trung bình đó.

::: lemma Bổ đề 05.12 (Kì vọng có điều kiện theo lịch sử) — phác thảo (chứng minh cho $\Xi$ hữu hạn; trường hợp tổng quát ở Phụ lục B)
**Giả thiết.**

- **Oracle.** $(\varphi,P_\xi)$ cho $F$ trên $W$ với hằng số $G$ (Định nghĩa 05.10).
- **Thuật toán.** Các điểm lặp $w_t$ và gradient ngẫu nhiên $g_t$ của Thuật toán 05.11, với $w_1\in W$ tất định.
- **Điểm so sánh.** $u\in W$ cố định.

**Bảo đảm.** Với mọi $t\ge1$ (ngẫu nhiên chỉ đến từ các lần rút $\xi_t$):

- **(a) Điểm lặp.** $w_t\in W$, và $w_t$ là một hàm đo được của $(\xi_1,\ldots,\xi_{t-1})$.
- **(b) Kì vọng có điều kiện.** Hầu chắc chắn (almost surely),
  $$
  \begin{aligned}
  &\mathbb E[g_t\mid\mathcal F_{t-1}]\\
  &\quad=\psi(w_t)\in\partial F(w_t),\\
  &\mathbb E\big[\lVert g_t\rVert^2\mid\mathcal F_{t-1}\big]\\
  &\quad\le G^2 .
  \end{aligned}
  $$
- **(c) Kì vọng không điều kiện.** $\mathbb E\lvert F(w_t)\rvert<\infty$, $\langle g_t,w_t-u\rangle$ khả tích, $\mathbb E\lVert g_t\rVert^2\le G^2$ và
  $$
  \begin{aligned}
  &\mathbb E\langle g_t,w_t-u\rangle\\
  &\quad=\mathbb E\langle\psi(w_t),w_t-u\rangle .
  \end{aligned}
  $$
:::

::: proof Chứng minh Bổ đề 05.12 (trường hợp $\Xi$ hữu hạn)
**Lộ trình.** Khi lịch sử cố định, điểm lặp cố định và lần rút mới vẫn có phân bố $P_\xi$.

Giả sử $\Xi$ hữu hạn và $P_\xi(k)>0$ với mọi $k\in\Xi$. Khi đó mỗi biến cố $\{(\xi_1,\ldots,\xi_{t-1})=k_{1:t-1}\}$, trong đó $k_{1:t-1}=(k_1,\ldots,k_{t-1})\in\Xi^{t-1}$, có xác suất dương nhờ $P_\xi(k)>0$. Trên biến cố đó, $\mathbb E[\cdot\mid\mathcal F_{t-1}]$ bằng kì vọng có điều kiện theo chính biến cố đó, kí hiệu $\mathbb E[\cdot\mid k_{1:t-1}]$.

**Bước 1 (phần a).** Quy nạp theo $t$: $w_1\in W$ tất định, và $w_{t+1}=\operatorname{proj}_W(w_t-\eta\varphi(w_t,\xi_t))$ thuộc $W$ và là hàm của $(\xi_1,\ldots,\xi_t)$. Với $\Xi$ hữu hạn, mọi hàm của $(\xi_1,\ldots,\xi_t)$ đều đo được.

**Bước 2 (phần b).** Cố định một lịch sử $k_{1:t-1}$. Trên biến cố $\{(\xi_1,\ldots,\xi_{t-1})=k_{1:t-1}\}$, điểm lặp $w_t$ bằng một điểm cố định $w(k_{1:t-1})\in W$. Vì $\xi_t$ độc lập với $(\xi_1,\ldots,\xi_{t-1})$, phân bố có điều kiện của $\xi_t$ trên biến cố này vẫn là $P_\xi$; tính độc lập được dùng ở đây. Do đó
$$
\begin{aligned}
&\mathbb E[g_t\mid k_{1:t-1}]\\
&\quad=\sum_{k\in\Xi}P_\xi(k)\,\varphi(w(k_{1:t-1}),k)\\
&\quad=\psi(w(k_{1:t-1})),
\end{aligned}
$$
và $\psi(w(k_{1:t-1}))\in\partial F(w(k_{1:t-1}))$ theo (G1). Cùng phép tính với $\lVert\varphi\rVert^2$ và (G2) tại $w(k_{1:t-1})\in W$ cho $\mathbb E[\lVert g_t\rVert^2\mid k_{1:t-1}]\le G^2$.

**Bước 3 (phần c).** Mọi biến ngẫu nhiên ở đây nhận hữu hạn giá trị, nên các kì vọng hữu hạn. Theo tính chất tháp, lấy trung bình theo $k_{1:t-1}$ với trọng số $\Pr(k_{1:t-1})$. Khi biết $k_{1:t-1}$, véc-tơ $w_t-u=w(k_{1:t-1})-u$ cố định và được lấy ra khỏi kì vọng có điều kiện:
$$
\begin{aligned}
&\mathbb E\langle g_t,w_t-u\rangle\\
&=\textstyle\sum\Pr(k_{1:t-1})\,\big\langle\mathbb E[g_t\mid k_{1:t-1}],\\
&\qquad w(k_{1:t-1})-u\big\rangle\\
&=\textstyle\sum\Pr(k_{1:t-1})\,\big\langle\psi(w(k_{1:t-1})),\\
&\qquad w(k_{1:t-1})-u\big\rangle\\
&=\mathbb E\langle\psi(w_t),w_t-u\rangle ,
\end{aligned}
$$
trong đó các tổng lấy theo mọi $k_{1:t-1}\in\Xi^{t-1}$. Tương tự, $\mathbb E\lVert g_t\rVert^2=\sum\Pr(k_{1:t-1})\,\mathbb E[\lVert g_t\rVert^2\mid k_{1:t-1}]\le G^2$.

$\square$ Đây là chỗ duy nhất cấu trúc ngẫu nhiên của thuật toán đi vào chứng minh ở §7. Trường hợp $\Xi$ tổng quát cần bổ đề đóng băng và một lập luận về tính hữu hạn của các kì vọng (Phụ lục B).
:::

Gradient ngẫu nhiên không chệch khi biết lịch sử. Theo kì vọng có điều kiện, bình phương khoảng cách tới một điểm $u\in W$ giảm ít nhất $2\eta(F(w_t)-F(u))-\eta^2G^2$ (§7).

## 7. Bất đẳng thức một bước và cận kì vọng

Khoảng cách từ điểm lặp tới một điểm so sánh $u\in W$ thay đổi theo một khai triển đại số, và khai triển đó chỉ có thêm một số hạng $\eta^2\lVert g\rVert^2$, có mặt cả khi $g$ là gradient đúng.

::: proposition Mệnh đề 05.13 (Bất đẳng thức một bước) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Tập.** $W\subset\mathbb R^p$ khác rỗng, đóng, lồi.
- **Bước.** $w,g\in\mathbb R^p$, $\eta>0$ và $w^+=\operatorname{proj}_W(w-\eta g)$.
- **Điểm so sánh.** $u\in W$.

**Bảo đảm.** Tất định, không dùng tính lồi của hàm mục tiêu hay xác suất:
$$
\begin{aligned}
&\langle g,w-u\rangle\\
&\quad\le\frac{\lVert w-u\rVert^2-\lVert w^+-u\rVert^2}{2\eta}\\
&\qquad+\frac\eta2\lVert g\rVert^2 .
\end{aligned}
$$
Khi $W=\mathbb R^p$, dấu bằng xảy ra.
:::

::: proof Chứng minh Mệnh đề 05.13
**Lộ trình.** Khai triển bình phương khoảng cách trước và sau một bước; bất đẳng thức then chốt là Bổ đề 05.8(b).

**Bước 1 (phép chiếu).** Theo Bổ đề 05.8(b) với $\theta=w-\eta g$ và $u\in W$,
$$
\begin{aligned}
&\lVert w^+-u\rVert^2\\
&\quad\le\lVert w-\eta g-u\rVert^2\\
&\quad=\lVert w-u\rVert^2-2\eta\langle g,w-u\rangle\\
&\qquad+\eta^2\lVert g\rVert^2 .
\end{aligned}
$$
Bất đẳng thức là chỗ duy nhất dùng phép chiếu và điều kiện $u\in W$; đẳng thức là khai triển $\lVert a-a'\rVert^2$ với $a=w-u$, $a'=\eta g$. Khi $W=\mathbb R^p$, $w^+=w-\eta g$ và bất đẳng thức là đẳng thức.

**Bước 2 (chuyển vế).** Chuyển $2\eta\langle g,w-u\rangle$ sang vế trái, $\lVert w^+-u\rVert^2$ sang vế phải, rồi chia cho $2\eta>0$.

$\square$ Khi $\langle g,w-u\rangle$ lớn, tức bước đi hướng về $u$, khoảng cách tới $u$ giảm, trừ số hạng $\tfrac\eta2\lVert g\rVert^2$.
:::

::: example Ví dụ 05.7 (Bất đẳng thức một bước tại bước thứ hai)
**Thiết lập.** Bước thứ hai của Ví dụ 05.6: $w=w_2=(1,0)$, $g=g_2=(0,2)$, $\eta=0{,}5$, $w^+=w_3$, và $u=w^*$.

**Bước 1: khoảng cách.** $\lVert w_2-w^*\rVert^2\approx0{,}5053$ và $\lVert w_3-w^*\rVert\approx0{,}0586$, nên $\lVert w_3-w^*\rVert^2\approx0{,}0034$. Điểm chưa chiếu $(1,-1)$ có $\lVert(1,-1)-w^*\rVert\approx0{,}4200$, bình phương $\approx0{,}1764$.

**Bước 2: hai vế.** Vế trái là $\langle g,w-u\rangle\approx1{,}3289$. Với $2\eta=1$ và $\tfrac\eta2\lVert g\rVert^2=0{,}25\cdot4=1$, vế phải là
$$
\begin{aligned}
\frac{0{,}5053-0{,}0034}{1}+1&\approx1{,}5019 .
\end{aligned}
$$

**Kết luận.** Nếu không chiếu, vế phải dùng $0{,}1764$ thay cho $0{,}0034$ và bằng đúng $1{,}3289$. Phép chiếu giảm khoảng cách từ $0{,}42$ xuống $0{,}0586$, nên bất đẳng thức là ngặt: $1{,}3289<1{,}5019$.
:::

Chứng minh của định lý dưới đây cộng bất đẳng thức một bước theo $t$ và lấy kì vọng. Ngoài phép chiếu, định lý cần giả thiết sau, gọi là (C): hàm mục tiêu $F:\mathbb R^p\to\mathbb R$ lồi, và tập tham số $W\subset\mathbb R^p$ khác rỗng, đóng, lồi.

::: theorem Định lý 05.14 (Cận kì vọng cho hạ gradient ngẫu nhiên có chiếu) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau.

- **Hàm mục tiêu và tập tham số.** (C).
- **Oracle.** $(\varphi,P_\xi)$ thỏa (G1) và (G2) với hằng số $G$ (Định nghĩa 05.10).
- **Thuật toán.** Thuật toán 05.11 với $w_1\in W$ tất định, $\eta>0$ hằng và $T\ge1$.
- **Điểm so sánh.** $u\in W$ tất định, bất kì.

**Bảo đảm.** Theo kì vọng theo $\xi_1,\ldots,\xi_{T-1}$,
$$
\begin{aligned}
&\mathbb E\big[F(\bar w_T)\big]-F(u)\\
&\quad\le\frac{\lVert w_1-u\rVert^2}{2\eta T}+\frac{\eta G^2}{2}.
\end{aligned}
$$
Đại lượng được chặn là độ chênh tối ưu của $F$, hàm mà oracle không chệch, tại điểm lặp trung bình. Số hạng thứ nhất giảm như $1/T$, số hạng thứ hai tỉ lệ với $\eta$ và không giảm theo $T$. Cận phụ thuộc $p$, $m$ chỉ qua $G$, $\lVert w_1-u\rVert$. Định lý không cần nghiệm tối ưu tồn tại, chỉ là cận theo kì vọng (không phải với xác suất cao), và không nói gì về điểm lặp cuối $w_{T+1}$.
:::

::: proof Chứng minh Định lý 05.14
**Lộ trình.** Áp dụng Mệnh đề 05.13 ở mỗi bước, cộng lại thành một tổng triệt tiêu, lấy kì vọng, rồi dùng tính lồi để chuyển sang điểm lặp trung bình. Đặt $\Delta_t=\lVert w_t-u\rVert^2$.

**Bước 1 (một bước; phép chiếu).** Mệnh đề 05.13 với $w=w_t$, $g=g_t$, $w^+=w_{t+1}$ cho, trên từng quỹ đạo (với mỗi dãy giá trị cụ thể của $\xi_1,\ldots,\xi_T$),
$$
\begin{aligned}
&\langle g_t,w_t-u\rangle\\
&\quad\le\frac{\Delta_t-\Delta_{t+1}}{2\eta}+\frac\eta2\lVert g_t\rVert^2 .
\end{aligned}
$$
Tính lồi và tính đóng của $W$, cùng điều kiện $u\in W$, được dùng ở đây.

**Bước 2 (tổng triệt tiêu).** Cộng theo $t=1,\ldots,T$. Trong $\sum_t(\Delta_t-\Delta_{t+1})=\Delta_1-\Delta_{T+1}$, các số hạng giữa triệt tiêu. Bỏ $-\Delta_{T+1}\le0$, ta được
$$
\begin{aligned}
\sum_{t=1}^T\langle g_t,w_t-u\rangle&\le\frac{\Delta_1}{2\eta}\\
&\quad+\frac\eta2\sum_{t=1}^T\lVert g_t\rVert^2 .
\end{aligned}
$$

**Bước 3 (kì vọng; tính không chệch).** Theo Bổ đề 05.12(c), $\mathbb E\langle g_t,w_t-u\rangle=\mathbb E\langle\psi(w_t),w_t-u\rangle$; tính không chệch (G1) được dùng ở đây, qua kì vọng có điều kiện theo lịch sử. Vì $\psi(w_t)\in\partial F(w_t)$, định nghĩa của dưới gradient tại $w_t$, áp dụng với điểm $u$, cho
$$
\begin{aligned}
&\langle\psi(w_t),w_t-u\rangle\\
&\quad\ge F(w_t)-F(u).
\end{aligned}
$$
Bước này chỉ dùng (G1). Tính lồi của $F$ là điều kiện để (G1) thỏa được: với $F$ lồi, $\partial F(w)\ne\varnothing$ tại mọi $w$. Ngược lại, (G1) tại mọi điểm của $W$ buộc $F$ lồi trên $W$: cộng hai bất đẳng thức dưới gradient tại $\alpha w+(1-\alpha)w'\in W$ với trọng số $\alpha$ và $1-\alpha$.

**Bước 4 (mô-men bậc hai).** Theo Bổ đề 05.12(c), $\mathbb E\lVert g_t\rVert^2\le G^2$; (G2) chỉ được dùng ở số hạng $\tfrac\eta2\lVert g_t\rVert^2$. Lấy kì vọng ở Bước 2 và dùng Bước 3, Bước 4:
$$
\begin{aligned}
&\sum_{t=1}^T\mathbb E\big[F(w_t)-F(u)\big]\\
&\quad\le\frac{\Delta_1}{2\eta}+\frac{\eta TG^2}{2}.
\end{aligned}
$$

**Bước 5 (trung bình; tính lồi của $F$ và $W$).** Theo bất đẳng thức lồi hữu hạn với trọng số $1/T$, trên từng quỹ đạo,
$$
F(\bar w_T)\le\frac1T\sum_{t=1}^TF(w_t),
$$
và $\bar w_T\in W$ vì $W$ lồi. Lấy kì vọng, kết hợp với Bước 4 và chia cho $T$, ta được bảo đảm.

$\square$ Với $u$ là một nghiệm tối ưu, cận của độ chênh tối ưu kì vọng giảm như $1/T$ về số hạng $\eta G^2/2$ của cận; hệ quả dưới đây chọn $\eta$ để cân bằng hai số hạng.
:::

Tính lồi của $F$ dùng ở Bước 5 và là điều kiện để (G1) ở Bước 3 thỏa được. Với đầu ra là một điểm lặp chọn đều ngẫu nhiên trong $w_1,\ldots,w_T$, độc lập với các lần rút, Bước 5 không cần bất đẳng thức lồi.

::: corollary Hệ quả 05.15 (Độ dài bước theo số vòng lặp) — chứng minh đầy đủ
**Giả thiết.** Như Định lý 05.14, thêm hai thành phần.

- **Hằng số.** $G>0$ và $R>0$.
- **Độ dài bước.** $\eta=R/(G\sqrt T)$.

**Bảo đảm.** Lấy kì vọng theo $\xi$:

- **(a) Một điểm so sánh.** Với mọi $u\in W$ thỏa $\lVert w_1-u\rVert\le R$,
  $$
  \mathbb EF(\bar w_T)-F(u)\le\frac{RG}{\sqrt T}.
  $$
- **(b) Cận dưới đúng.** Với $F_R=\inf\{F(u):u\in W,\ \lVert u-w_1\rVert\le R\}$, ta có $\mathbb EF(\bar w_T)-F_R\le RG/\sqrt T$. Nếu $F$ có một nghiệm tối ưu $w^*$ trên $W$ với $\lVert w_1-w^*\rVert\le R$, thì $\mathbb EF(\bar w_T)-F(w^*)\le RG/\sqrt T$; nếu $\lVert w_1-u\rVert\le R$ với mọi $u\in W$, thì $F_R=\inf_{w\in W}F(w)$.
- **(c) Số vòng lặp.** Với $\epsilon>0$, điều kiện $T\ge R^2G^2/\epsilon^2$ đủ để các vế trái ở (a) và (b) không quá $\epsilon$.

Vì $\eta$ phụ thuộc $T$, $T$ được cố định trước khi chạy.
:::

::: proof Chứng minh Hệ quả 05.15
**Lộ trình.** Thay $\eta$ vào Định lý 05.14, rồi lấy cận dưới đúng theo $u$.

**Bước 1 (phần a).** Với $\lVert w_1-u\rVert\le R$ và $\eta=R/(G\sqrt T)$,
$$
\begin{aligned}
\frac{\lVert w_1-u\rVert^2}{2\eta T}&\le\frac{R^2G\sqrt T}{2RT}\\
&=\frac{RG}{2\sqrt T},\\
\frac{\eta G^2}2&=\frac{RG}{2\sqrt T}.
\end{aligned}
$$
Cộng hai số hạng, ta được $RG/\sqrt T$.

**Bước 2 (phần b).** Vế phải ở (a) không phụ thuộc $u$. Lấy cận trên đúng theo $u$ của $\mathbb EF(\bar w_T)-F(u)$ trên tập $\{u\in W:\lVert u-w_1\rVert\le R\}$, ta được $\mathbb EF(\bar w_T)-F_R\le RG/\sqrt T$. Hai trường hợp riêng là $u=w^*$ và tập trên bằng $W$.

**Bước 3 (phần c).** $RG/\sqrt T\le\epsilon$ khi và chỉ khi $T\ge R^2G^2/\epsilon^2$.

$\square$ Muốn giảm cận của độ chênh tối ưu kì vọng một nửa, cần gấp bốn lần số vòng lặp.
:::

Giá trị $\eta=R/(G\sqrt T)$ làm vế phải của Định lý 05.14, với $\lVert w_1-u\rVert=R$, nhỏ nhất theo $\eta>0$ (Bài tập 05.4).

::: example Ví dụ 05.8 (Số vòng lặp và độ dài bước khi $R=1$, $G=4$)
**Thiết lập.** Oracle của Ví dụ 05.5: $W=\{w:\lVert w\rVert\le1\}$, $w_1=0$ và $G=4$. Mọi $u\in W$ thỏa $\lVert w_1-u\rVert\le1$, nên $R=1$, và theo Hệ quả 05.15(b) đối tượng so sánh là $\min_WL_S=0{,}06112$.

**Bước 1: hằng số.** $R^2G^2=1\cdot16=16$.

**Bước 2: số vòng lặp.** Theo Hệ quả 05.15(c), $T\ge16/\epsilon^2$. Với $\epsilon=0{,}2$; $0{,}1$; $0{,}05$, ta được $T\ge400$; $1600$; $6400$.

**Bước 3: độ dài bước và bảo đảm.** Với $T=1600$, ta có $\sqrt T=40$ và
$$
\eta=\frac1{4\cdot40}=0{,}00625 .
$$
Bảo đảm là $\mathbb E_\xi L_S(\bar w_{1600})\le0{,}06112+0{,}1=0{,}16112$.

**Bước 4: độ nhạy theo độ dài bước.** Với $\eta=\gamma\,\eta^*$, trong đó $\eta^*=R/(G\sqrt T)$ và $\gamma>0$, hai số hạng của vế phải Định lý 05.14 (với $\lVert w_1-u\rVert=R$) là
$$
\begin{aligned}
\frac{R^2}{2\gamma\eta^*T}&=\frac{RG}{2\gamma\sqrt T},\\
\frac{\gamma\eta^*G^2}2&=\frac{\gamma RG}{2\sqrt T},
\end{aligned}
$$
nên vế phải bằng $\frac{RG}{\sqrt T}\cdot\frac{\gamma+1/\gamma}2$. Thừa số này bằng $1{,}25$ khi $\gamma=2$ hoặc $\gamma=\tfrac12$, và bằng $5{,}05$ khi $\gamma=10$.

**Bước 5: độ dài bước của Ví dụ 05.6.** Với $\eta=0{,}5$ và $T=1600$, vế phải là
$$
\begin{aligned}
&\frac1{2\cdot0{,}5\cdot1600}+\frac{0{,}5\cdot16}2\\
&\quad=0{,}000625+4\\
&\quad=4{,}000625 .
\end{aligned}
$$
Trên $W$, mỗi hàm lỗi không quá $(BC_x+C_y)^2=4$ (Ví dụ 05.5), nên độ chênh tối ưu không quá $4<4{,}000625$: cận không cho thông tin.

**Kết luận.** Với $\epsilon=0{,}1$, Hệ quả 05.15 cho $T=1600$ và $\eta=0{,}00625$; lệch hai lần so với $\eta^*$ chỉ làm cận tăng $25\%$.
:::

GD là trường hợp oracle tất định: $g_t=v(w_t)\in\partial F(w_t)$. Cùng lập luận cho một cận tất định.

::: corollary Hệ quả 05.16 (Cận cho hạ gradient có chiếu) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau.

- **Hàm mục tiêu và tập tham số.** (C).
- **Dưới gradient.** Một quy tắc $v(w)\in\partial F(w)$ với $\lVert v(w)\rVert\le G$ cho mọi $w\in W$, trong đó $G>0$; điều kiện này thỏa khi $F$ là $G$-Lipschitz trên một tập mở chứa $W$ (Mệnh đề 05.5(b)).
- **Thuật toán.** Thuật toán 05.9 với $\eta=R/(G\sqrt T)$, $R>0$.
- **Điểm so sánh.** $u\in W$ với $\lVert w_1-u\rVert\le R$.

**Bảo đảm.** Tất định: $F(\bar w_T)-F(u)\le RG/\sqrt T$, và $T\ge R^2G^2/\epsilon^2$ vòng lặp đủ để vế trái không quá $\epsilon$.
:::

::: proof Chứng minh Hệ quả 05.16
**Lộ trình.** Lặp lại Bước 1, 2 và 5 của chứng minh Định lý 05.14 trên quỹ đạo duy nhất. Bước 3 và 4 không cần kì vọng: $\langle v_t,w_t-u\rangle\ge F(w_t)-F(u)$ theo bất đẳng thức dưới gradient, và $\lVert v_t\rVert^2\le G^2$ theo giả thiết. Thay $\eta$ như Bước 1 của chứng minh Hệ quả 05.15.

$\square$ Theo các cận này, GD và SGD cần cùng số vòng lặp khi $G$ như nhau; mỗi vòng GD trên $L_S$ tốn gấp $m$ lần.
:::

::: example Ví dụ 05.9 (Hạ gradient và hạ gradient ngẫu nhiên cho hồi quy logistic)
**Thiết lập.** Ứng dụng ở §3: $m=10^6$, $\lVert x_i\rVert\le1$, $W=\{w:\lVert w\rVert\le5\}$ (giá trị giả định), $w_1=0$ và $\epsilon=0{,}05$.

**Bước 1: hằng số $G$.** Gradient của hàm lỗi logistic trên một quan sát là
$$
\nabla_w\ell(w,(x,y))=-\frac{\tilde y\,x}{1+e^{\tilde y\langle w,x\rangle}},
$$
có chuẩn không quá $\lVert x\rVert\le1$ vì mẫu số lớn hơn $1$. Do đó (G2) đúng với $G=1$ cho oracle rút một quan sát, và $\lVert\nabla L_S(w)\rVert\le1$ cho GD (trung bình của các véc-tơ như vậy).

**Bước 2: hằng số $R$.** Với mọi $u\in W$, $\lVert w_1-u\rVert\le5$, nên $R=5$.

**Bước 3: số vòng lặp và độ dài bước.** Theo Hệ quả 05.15(c) và 05.16,
$$
\begin{aligned}
T&\ge\frac{25\cdot1}{0{,}0025}=10^4,\\
\eta&=\frac5{1\cdot\sqrt{10^4}}=0{,}05 .
\end{aligned}
$$

**Bước 4: chi phí.** SGD tính $10^4$ gradient trên một quan sát, bằng $1\%$ của một bước GD. GD tính $10^4\cdot10^6=10^{10}$ gradient như vậy.

**Kết luận.** Với SGD, $\mathbb E_\xi L_S(\bar w_T)-\min_WL_S\le0{,}05$; với GD, cùng cận đúng tất định.
:::

::: remark Nhận xét 05.17 (Độ dài bước thay đổi) — đọc thêm
**Giả thiết.** Như Định lý 05.14, với một dãy tất định $\eta_t>0$ thay cho $\eta$ trong Thuật toán 05.11 và đầu ra là trung bình có trọng số $\tilde w_T=\sum_t\eta_tw_t/\sum_t\eta_t$.

**Bảo đảm.** Theo kì vọng theo $\xi$,
$$
\begin{aligned}
&\mathbb EF(\tilde w_T)-F(u)\\
&\quad\le\frac{\lVert w_1-u\rVert^2+G^2\sum_{t=1}^T\eta_t^2}{2\sum_{t=1}^T\eta_t}
\end{aligned}
$$
(Phụ lục C). Với $\eta_t=R/(G\sqrt t)$, $R=1$, $G=4$ và $T=1600$, vế phải không quá $0{,}2281$, so với $0{,}1$ của độ dài bước hằng ở Ví dụ 05.8, vì $\sum_t\eta_t^2$ tăng như $\ln T$. Đổi lại, $\eta_t$ không phụ thuộc $T$; với trung bình đều cần thêm $W$ bị chặn (Bài tập 05.11).
:::

Mỗi giả thiết (C), (G1), (G2) của Định lý 05.14 đi vào những bước đã ghi trong chứng minh, và cận không nói gì khi thiếu một trong ba.

## 8. Vai trò của từng giả thiết

Mỗi ví dụ dưới đây, với $p=1$, giữ các giả thiết còn lại của Định lý 05.14 và bỏ một giả thiết, hoặc đổi đầu ra.

::: example Ví dụ 05.10 (Hàm mục tiêu không lồi)
**Thiết lập.** $f(w)=\min\{(w-1)^2,\,(w+1)^2+0{,}5\}$ trên $W=[-2,2]$. Gọi $(w+1)^2+0{,}5$ là nhánh trái và $(w-1)^2$ là nhánh phải; hai nhánh bằng nhau tại $w=-0{,}125$, và nhánh trái nhỏ hơn khi $w<-0{,}125$. GD dùng đạo hàm của nhánh đang nhỏ hơn, với $w_1=-1{,}5$. Hàm $f$ không lồi: giá trị nhỏ nhất toàn cục là $0$, đạt tại $w=1$, còn $w=-1$ là một cực tiểu địa phương với $f(-1)=0{,}5$.

**Bước 1: các giả thiết khác.** $W$ lồi đóng. Trên $W$, $\lvert f'\rvert\le2{,}25$ (giá trị lớn nhất tại $w=-0{,}125$, trên nhánh phải), nên $G=2{,}25$. Với $u=1$, $R=\lvert w_1-1\rvert=2{,}5$.

**Bước 2: độ dài bước của Hệ quả 05.16.** Với $T=1600$,
$$
\begin{aligned}
\eta&=\frac{2{,}5}{2{,}25\cdot40}\approx0{,}02778,\\
\frac{RG}{\sqrt T}&=0{,}140625 .
\end{aligned}
$$

**Bước 3: các điểm lặp.** Trên nhánh trái, $w_{t+1}+1=(1-2\eta)(w_t+1)$. Mọi điểm lặp nằm trong $[-1{,}5;-1]$, bên trái $-0{,}125$, và tiến về $-1$. Lấy trung bình cấp số nhân,
$$
\begin{aligned}
&\bar w_{1600}+1\\
&\quad=-0{,}5\cdot\frac{1-(1-2\eta)^{1600}}{2\eta\cdot1600}\\
&\quad\approx-0{,}0056,
\end{aligned}
$$
nên $\bar w_{1600}\approx-1{,}0056$ và $f(\bar w_{1600})\approx0{,}5000$.

**Bước 4: so với cận.** Độ chênh $0{,}5000-0>0{,}140625$: kết luận của Hệ quả 05.16 sai.

**Bước 5: bất đẳng thức dưới gradient.** Trên nhánh trái, với $s=w+1$,
$$
\begin{aligned}
&f(w)+f'(w)(1-w)\\
&\quad=s^2+0{,}5+2s(2-s)\\
&\quad=-s^2+4s+0{,}5,
\end{aligned}
$$
dương khi $w>-1{,}1213$. Từ vòng $t=26$, $w_t\in(-1{,}1213;-1)$, nên $f(1)=0<f(w_t)+f'(w_t)(1-w_t)$.

**Kết luận.** $f'(w_t)$ không phải dưới gradient tại $w_t$, tức (G1) hỏng, do $f$ không lồi; Bước 3 của chứng minh hỏng.
:::

::: example Ví dụ 05.11 (Mô-men bậc hai không bị chặn)
**Thiết lập.** Mẫu $S=((1,0),(3,0))$, hàm lỗi bình phương, nên $F(w)=L_S(w)=\tfrac12(w^2+9w^2)=5w^2$. Lấy $W=\mathbb R$ (không chiếu), oracle rút đều có hoàn lại, $\varphi(w,i)=2x_i^2w$, $\eta=0{,}15$ và $w_1=1$.

**Bước 1: GD.** $w_{t+1}=(1-10\eta)w_t=-0{,}5\,w_t\to0$.

**Bước 2: SGD.** $w_{t+1}=(1-2\eta x_{i_t}^2)w_t=a_tw_t$, với $2\eta=0{,}3$, thừa số $a_t$ bằng $1-0{,}3\cdot1=0{,}7$ hoặc $1-0{,}3\cdot9=-1{,}7$, mỗi giá trị có xác suất $\tfrac12$.

**Bước 3: phân kì.** Ta có $\mathbb E\ln\lvert a_t\rvert=\tfrac12(\ln0{,}7+\ln1{,}7)\approx0{,}087>0$. Theo luật số lớn (law of large numbers), $\tfrac1t\ln\lvert w_{t+1}\rvert\to0{,}087$, nên $\lvert w_t\rvert\to\infty$ hầu chắc chắn. Ngoài ra $\mathbb Ea_t^2=\tfrac12(0{,}49+2{,}89)=1{,}69$, nên $\mathbb Ew_{t+1}^2=1{,}69^t$.

**Bước 4: giả thiết hỏng.** $\mathbb E\lVert\varphi(w,\xi)\rVert^2=\tfrac12\big[(2w)^2+(18w)^2\big]=164w^2$, không bị chặn trên $\mathbb R$: (G2) hỏng, và Bước 4 của chứng minh hỏng.

**Bước 5: sửa bằng phép chiếu.** Chiếu lên $W=[-1,1]$ cho $G^2=164$, $G\approx12{,}81$, và Định lý 05.14 áp dụng. Cận có ích khi $\eta=R/(G\sqrt T)$: với $u=0$ và $R=1$, cận là $12{,}81/\sqrt T$.

**Kết luận.** Với cùng độ dài bước, GD hội tụ còn SGD phân kì; Bước 4 của chứng minh cần (G2).
:::

::: example Ví dụ 05.12 (Điểm lặp cuối với độ dài bước hằng)
**Thiết lập.** $f(w)=\lvert w\rvert$, $W=[-1,1]$, $G=1$, GD với dưới gradient $\operatorname{sign}(w)$, $\eta=0{,}2$ và $w_1=0{,}1$.

**Bước 1: các điểm lặp.** Các điểm lặp là $0{,}1;-0{,}1;0{,}1;\ldots$, nên $f(w_t)=0{,}1$ với mọi $t$.

**Bước 2: điểm lặp trung bình.** $\bar w_T=0$ khi $T$ chẵn.

**Bước 3: vế phải.** Với $u=0$, vế phải của Định lý 05.14 là $0{,}01/(0{,}4T)+0{,}1=0{,}025/T+0{,}1$.

**Kết luận.** Điểm lặp cuối không hội tụ với độ dài bước hằng, nhưng ví dụ không vi phạm cận, vì $f(w_t)$ bằng số hạng $\eta G^2/2=0{,}1$ của cận.
:::

::: example Ví dụ 05.13 (Oracle chệch)
**Thiết lập.** Mẫu $S=((1,0),(1,1))$, hàm lỗi bình phương, $L_S(w)=\tfrac12[w^2+(w-1)^2]$, cực tiểu tại $0{,}5$ với $\min L_S=0{,}25$. Lấy $W=[-1,1]$ và $w_1=0$. Oracle rút chỉ số $1$ với xác suất $0{,}9$ và chỉ số $2$ với xác suất $0{,}1$; với $w\in W$, $\lvert\varphi(w,i)\rvert=2\lvert w-y_i\rvert\le4$, nên (G2) đúng với $G=4$.

**Bước 1: (G1) hỏng.** $\psi(w)=0{,}9\cdot2w+0{,}1\cdot2(w-1)=2w-0{,}2$, trong khi $L_S'(w)=2w-1$.

**Bước 2: hàm thực sự được tối thiểu hóa.** $\psi$ là đạo hàm của $\tilde F(w)=0{,}9w^2+0{,}1(w-1)^2$, cực tiểu tại $0{,}1$; Định lý 05.14 áp dụng cho $\tilde F$.

**Bước 3: độ chênh.** Ta có $L_S(w)=(w-0{,}5)^2+0{,}25$ và $\tilde F(w)=(w-0{,}1)^2+0{,}09$, nên $L_S(0{,}1)-L_S(0{,}5)=0{,}41-0{,}25=0{,}16$. Khi $T$ tăng với độ dài bước của Hệ quả 05.15, $\mathbb E(\bar w_T-0{,}1)^2=\mathbb E\tilde F(\bar w_T)-\min\tilde F\to0$, nên $\mathbb EL_S(\bar w_T)-0{,}25=\mathbb E(\bar w_T-0{,}5)^2\to0{,}16$, không về $0$.

**Kết luận.** Oracle xác định hàm mục tiêu được tối thiểu hóa. Khi kì vọng của oracle không phải dưới gradient của $F$, Bước 3 của chứng minh hỏng.
:::

Với $F(w)=\tfrac a2w^2$, độ dài bước hằng và nhiễu gradient có phương sai dương, điểm lặp cuối không hội tụ tới nghiệm tối ưu mà dao động quanh nó. Mức dao động là một *mức sàn sai số* (error floor), tỉ lệ với $\eta$ khi $\eta$ nhỏ. Bài tập 05.6 tính mức này và cho thấy lấy trung bình xóa được nó.

## 9. Hạ gradient ngẫu nhiên trên rủi ro thực nghiệm

Hệ quả 05.15 chặn độ chênh tối ưu $F(\bar w_T)-\inf_WF$ theo kì vọng (khi $\lVert w_1-u\rVert\le R$ với mọi $u\in W$); với $F=L_S$, đó là $\operatorname{opt}_S(\bar w_T)$ của Định nghĩa 04.2, còn Bài 01 đặt hai mức (O1), (O2) tất định cho bộ giải. SGD là một thuật toán ngẫu nhiên, nên đầu ra của nó là một biến ngẫu nhiên ngay cả khi mẫu đã cố định.

::: definition Định nghĩa 05.18 (Thuật toán học có nguồn ngẫu nhiên riêng)
Cho tập quan sát $\mathcal Z$, lớp giả thuyết $\mathcal H$ và hàm lỗi $\ell$ như Định nghĩa 01.4. Cho thêm một biến ngẫu nhiên $\xi$ nhận giá trị trong một tập $\Xi$ với phân bố $P_\xi$; $\xi$ có thể là một dãy các lần rút. Một *thuật toán học có nguồn ngẫu nhiên riêng* (randomized learning algorithm) là một họ ánh xạ $A_m:\mathcal Z^m\times\Xi\to\mathcal H$, $m\ge1$, sao cho ánh xạ $(s,\xi,z)\mapsto\ell(A_m(s;\xi),z)$ đo được theo bộ ba, với $s$ chạy trên $\mathcal Z^m$. Ta viết $A(S;\xi)$, với $\xi$ độc lập với $S$.
:::

Định nghĩa 01.4 là trường hợp $\Xi$ có một điểm. Xác suất trong các định nghĩa PAC của Bài 01 khi đó lấy theo cặp $(S,\xi)$ với phân bố tích $D^m\otimes P_\xi$; một bảo đảm theo $\xi$ đúng với mọi $S$ cố định thì cũng đúng theo cặp $(S,\xi)$.

SGD có chiếu trên $L_S$ với chỉ số rút đều có hoàn lại là một thuật toán như vậy. Lớp $\mathcal H=\{h_w:w\in W\}$ là lớp hàm điểm số, nhận giá trị trong $\mathbb R$ thay cho $\mathcal Y$. Đầu ra là $A(S;\xi)=\bar w_T$, và $\xi=(\xi_1,\ldots,\xi_{T-1})$ có phân bố tích của $T-1$ lần rút theo phân bố của Định nghĩa 05.10, không phụ thuộc $S$.

::: corollary Hệ quả 05.19 (Hạ gradient ngẫu nhiên trên rủi ro thực nghiệm) — chứng minh đầy đủ
**Giả thiết.** Năm thành phần sau.

- **Mẫu.** $s=(z_1,\ldots,z_m)$ bất kì, cố định.
- **Hàm lỗi.** Với mỗi $z$, $\ell(\cdot,z):\mathbb R^p\to[0,\infty)$ lồi; một quy tắc dưới gradient đo được $v(w,z)\in\partial\ell(\cdot,z)(w)$ với $\lVert v(w,z_i)\rVert\le G$ cho mọi $w\in W$ và mọi $i$, trong đó $G>0$.
- **Tập tham số.** $W$ khác rỗng, đóng, lồi, bị chặn; $w_1\in W$; $R\ge\sup_{u\in W}\lVert w_1-u\rVert$, chẳng hạn $R=B$ khi $W$ là quả cầu bán kính $B$ và $w_1=0$.
- **Oracle.** $\xi_t=i_t$ đều trên $\{1,\ldots,m\}$, rút có hoàn lại; $\varphi(w,i)=v(w,z_i)$.
- **Thuật toán.** Thuật toán 05.11 với $\eta=R/(G\sqrt T)$; đầu ra $\bar w_T$.

**Bảo đảm.** Với $\operatorname{opt}_s(w)=L_s(w)-\inf_{w'\in W}L_s(w')$ (Định nghĩa 04.2 áp dụng cho lớp hàm điểm số $\{h_w:w\in W\}$ và hàm lỗi $\ell$):

- **(a) Theo kì vọng.** $\mathbb E_\xi\operatorname{opt}_s(\bar w_T)\le RG/\sqrt T$, với mọi mẫu $s$.
- **(b) Với xác suất cao.** Với $\epsilon_{\mathrm{opt}}>0$, $\delta'\in(0,1)$ (xác suất thất bại theo $\xi$, khác $\delta$ theo $S$) và $T\ge R^2G^2/(\delta'^2\epsilon_{\mathrm{opt}}^2)$,
  $$
  \Pr_\xi\big[\operatorname{opt}_s(\bar w_T)\ge\epsilon_{\mathrm{opt}}\big]\le\delta' .
  $$

Đại lượng được chặn là sai số tối ưu thực nghiệm $\operatorname{opt}_s(\bar w_T)$; xác suất và kì vọng lấy theo $\xi$.
:::

::: proof Chứng minh Hệ quả 05.19
**Lộ trình.** Kiểm tra (G1), (G2) cho $F=L_s$, áp dụng Hệ quả 05.15(b), rồi dùng bất đẳng thức Markov.

**Bước 1 (oracle).** Theo Mệnh đề 05.3(b), $\psi(w)=\frac1m\sum_iv(w,z_i)\in\partial L_s(w)$, tức (G1) với $F=L_s$. Ngoài ra
$$
\begin{aligned}
&\mathbb E\lVert\varphi(w,\xi)\rVert^2\\
&\quad=\frac1m\sum_{i=1}^m\lVert v(w,z_i)\rVert^2\le G^2,
\end{aligned}
$$
tức (G2).

**Bước 2 (phần a).** Mọi $u\in W$ thỏa $\lVert w_1-u\rVert\le R$, nên Hệ quả 05.15(b) cho $\mathbb E_\xi L_s(\bar w_T)-\inf_WL_s\le RG/\sqrt T$.

**Bước 3 (phần b).** Vì $\bar w_T\in W$, $\operatorname{opt}_s(\bar w_T)\ge0$. Theo bất đẳng thức Markov (Bổ đề 02.2) và phần (a),
$$
\begin{aligned}
&\Pr_\xi\big[\operatorname{opt}_s(\bar w_T)\ge\epsilon_{\mathrm{opt}}\big]\\
&\quad\le\frac{RG}{\epsilon_{\mathrm{opt}}\sqrt T}\le\delta',
\end{aligned}
$$
trong đó bất đẳng thức cuối do điều kiện trên $T$.

$\square$ SGD có chiếu là một bộ giải cho ERM trên lớp tham số hóa bởi $W$, với $\operatorname{opt}_s$ kiểm soát theo kì vọng, hoặc với xác suất ít nhất $1-\delta'$ theo $\xi$. Đây là bảo đảm cho một thuật toán cụ thể, không phải cho lớp $\{h_w:w\in W\}$ (Nhận xét 01.21).
:::

::: example Ví dụ 05.14 (Giá của bảo đảm với xác suất cao)
**Thiết lập.** Như Ví dụ 05.8: $R=1$, $G=4$; thêm $\epsilon_{\mathrm{opt}}=0{,}1$ và $\delta'=0{,}05$.

**Bước 1: theo kì vọng.** Theo Ví dụ 05.8, $T=1600$ cho $\mathbb E_\xi\operatorname{opt}_S\le0{,}1$.

**Bước 2: với xác suất cao.** Theo Hệ quả 05.19(b),
$$
\begin{aligned}
T&\ge\frac{16}{0{,}0025\cdot0{,}01}=640\,000 .
\end{aligned}
$$
Số vòng lặp đủ theo cận tăng $1/\delta'^2=400$ lần.

**Bước 3: ứng dụng.** Với Ví dụ 05.9, $\epsilon_{\mathrm{opt}}=0{,}05$ và $\delta'=0{,}05$, điều kiện đủ là $T\ge10^4/0{,}0025=4\,000\,000$ bước, tức $4\,000\,000$ gradient trên một quan sát, bằng chi phí của bốn bước GD.

**Kết luận.** Bất đẳng thức Markov chỉ dùng kì vọng, nên tốn thừa số $1/\delta'^2$. Bài tập 05.5(d) giảm giá này bằng nhiều lần chạy độc lập.
:::

Mức (O2) của Bài 01 đòi $\operatorname{opt}_S\le\epsilon_{\mathrm{opt}}$ trên mọi mẫu, một cách tất định; SGD chỉ đạt mức này với xác suất ít nhất $1-\delta'$ theo $\xi$. Đại lượng $\operatorname{opt}_S$ là số hạng của bộ giải trong Mệnh đề 04.3. Mệnh đề 04.3 cần hàm lỗi trong $[0,1]$ và một bán kính hội tụ đều cho lớp với hàm lỗi đó. Do đó nó không ghép trực tiếp được với hàm lỗi logistic hay bình phương ở đây; cận thống kê cho hàm lỗi lồi và Lipschitz thuộc Bài 06–07.

## 10. Lô nhỏ

Ví dụ 05.9 so hai đầu mút: một quan sát mỗi bước và cả mẫu mỗi bước. Lô nhỏ lấy trung bình $b$ gradient ngẫu nhiên ở mỗi bước, và trung bình đó đổi hằng số $G$ trong cận.

::: proposition Mệnh đề 05.20 (Gradient lô nhỏ) — đọc thêm
**Giả thiết.** Ba thành phần sau.

- **Oracle gốc.** $(\varphi,P_\xi)$ như Định nghĩa 05.10, thỏa (G1); (G2) thay bằng hai cận dưới đây.
- **Phương sai và độ lớn.** $\sigma^2\ge0$ và $G_F\ge0$ thỏa $\mathbb E_\xi\lVert\varphi(w,\xi)-\psi(w)\rVert^2\le\sigma^2$ và $\lVert\psi(w)\rVert\le G_F$ với mọi $w\in W$.
- **Lô.** Kích thước lô (batch size) $b\ge1$; $\bar\xi=(\xi^{(1)},\ldots,\xi^{(b)})$ gồm $b$ lần rút độc lập theo $P_\xi$, và gradient lô $\varphi_b(w,\bar\xi)=\frac1b\sum_{j=1}^b\varphi(w,\xi^{(j)})$.

**Bảo đảm.** Với mọi $w\in W$, kì vọng lấy theo $\bar\xi$:

- **(a) Kì vọng.** $\mathbb E\varphi_b(w,\bar\xi)=\psi(w)$;
- **(b) Phương sai.** $\mathbb E\lVert\varphi_b(w,\bar\xi)-\psi(w)\rVert^2\le\sigma^2/b$;
- **(c) Mô-men bậc hai.** $\mathbb E\lVert\varphi_b(w,\bar\xi)\rVert^2\le G_F^2+\sigma^2/b=:G_b^2$.

Do đó $(\varphi_b,P_\xi^{\otimes b})$ là một oracle gradient ngẫu nhiên với hằng số $G_b$; Định lý 05.14 và Hệ quả 05.15 cho $T\ge R^2G_b^2/\epsilon^2$ bước, tức $bT$ lần gọi oracle gốc.
:::

Ở đây $\sigma^2$ là phương sai của gradient ngẫu nhiên, khác phương sai nhiễu $\sigma^2(x)$ của Bài 04 và dấu ngẫu nhiên $\sigma_i$ của Bài 03.

::: proof Chứng minh Mệnh đề 05.20
**Lộ trình.** Tính tuyến tính của kì vọng cho (a); khai triển bình phương của một tổng cho (b); đẳng thức sau Định nghĩa 05.10 cho (c).

**Bước 1 (a).** Mỗi số hạng có kì vọng $\psi(w)$.

**Bước 2 (b).** Đặt $e_j=\varphi(w,\xi^{(j)})-\psi(w)$. Ta có
$$
\begin{aligned}
&\mathbb E\Big\lVert\frac1b\sum_je_j\Big\rVert^2\\
&\quad=\frac1{b^2}\sum_j\mathbb E\lVert e_j\rVert^2\\
&\qquad+\frac1{b^2}\sum_{j\ne k}\mathbb E\langle e_j,e_k\rangle .
\end{aligned}
$$
Với $j\ne k$, $e_j$ và $e_k$ độc lập, có kì vọng $0$, nên $\mathbb E\langle e_j,e_k\rangle=0$; bước này chỉ cần các $e_j$ không tương quan từng đôi. Tổng thứ nhất không quá $b\sigma^2/b^2=\sigma^2/b$.

**Bước 3 (c).** $\mathbb E\lVert\varphi_b\rVert^2=\lVert\psi(w)\rVert^2+\mathbb E\lVert\varphi_b-\psi(w)\rVert^2\le G_F^2+\sigma^2/b$.

$\square$ Chỉ phần phương sai chia cho $b$; phần $G_F^2$ là độ lớn của gradient thật và không đổi theo $b$.
:::

::: example Ví dụ 05.15 (Số bước và số quan sát theo kích thước lô)
**Thiết lập.** $G_F^2=1$ và $\sigma^2=15$, nên $G^2=16$ khi $b=1$, như Ví dụ 05.8; $R=1$, $\epsilon=0{,}1$ và $m=10^4$. $G_F^2$, $\sigma^2$ và $m$ là giá trị giả định, khác ứng dụng ở §3.

**Bước 1: công thức.** Số bước là $T(b)=\big\lceil R^2(G_F^2+\sigma^2/b)/\epsilon^2\big\rceil=\lceil100(1+15/b)\rceil$, và số quan sát phải xử lý là $bT(b)$. Chẳng hạn, $T(4)=\lceil100\cdot4{,}75\rceil=475$.

**Bước 2: bảng.** Với GD, Hệ quả 05.16 với $G=G_F=1$ cho $100$ bước, mỗi bước $m=10^4$ quan sát.

| $b$ | $T(b)$ | Số quan sát |
|---|---|---|
| $1$ | $1600$ | $1600$ |
| $4$ | $475$ | $1900$ |
| $16$ | $194$ | $3104$ |
| $64$ | $124$ | $7936$ |
| $256$ | $106$ | $27\,136$ |
| GD | $100$ | $10^6$ |

**Bước 3: đọc bảng.** Số quan sát $bT(b)\approx R^2(bG_F^2+\sigma^2)/\epsilon^2$ tăng theo $b$; số bước giảm nhanh đến khoảng $b=\sigma^2/G_F^2=15$, rồi gần như đứng yên ở mức $100$ của GD.

**Kết luận.** Theo các cận, lô lớn giảm số lần cập nhật nhưng tăng số quan sát phải xử lý.
:::

::: example Ví dụ 05.16 (Lô gồm các bản sao của một quan sát)
**Thiết lập.** Rút một chỉ số $i$ và chép nó $b$ lần vào lô; oracle gốc có phương sai đúng bằng $\sigma^2$.

**Bước 1: phương sai.** $\varphi_b=\varphi(w,i)$, nên phương sai vẫn là $\sigma^2$, không chia cho $b$.

**Bước 2: giả thiết hỏng.** Các phần tử của lô không độc lập; với $j\ne k$, $\mathbb E\langle e_j,e_k\rangle=\sigma^2$ chứ không bằng $0$.

**Kết luận.** Mệnh đề 05.20 cần các phần tử của lô không tương quan.
:::

Mọi so sánh của §7 và §10 là so sánh giữa các cận trên dưới (C), (G2), không phải so sánh thời gian chạy.

## 11. Ý nghĩa, tác động và giới hạn

Một bước SGD có thể làm $L_S$ tăng (Ví dụ 05.6); bảo đảm của SGD là cận kì vọng $RG/\sqrt T$ cho điểm lặp trung bình. Với hồi quy logistic trên $10^6$ hồ sơ, theo cận, $10^4$ bước SGD đủ cho mức kì vọng $0{,}05$ với chi phí bằng $1\%$ một bước GD (Ví dụ 05.9).

Độ dài bước $\eta=R/(G\sqrt T)$ được rút ra từ cận; lệch mười lần làm cận tăng $5{,}05$ lần (Ví dụ 05.8). Độ dài bước giảm dần không cần biết $T$, đổi lại cận $0{,}2281$ thay cho $0{,}1$ (Nhận xét 05.17). Trong ví dụ hồi quy, theo các cận, $1600$ bước đủ cho bảo đảm theo kì vọng và $640\,000$ bước đủ cho bảo đảm với xác suất ít nhất $0{,}95$ theo $\xi$ (Ví dụ 05.14). Với lô nhỏ, theo cận, chỉ phần phương sai giảm theo $b$ (Ví dụ 05.15).

Bỏ một trong ba giả thiết sau, bảo đảm có thể hỏng.

- **Tính lồi.** Đạo hàm không còn là dưới gradient, tức (G1) hỏng; độ chênh $0{,}5$ so với cận $0{,}140625$ (Ví dụ 05.10).
- **Mô-men bậc hai bị chặn.** SGD phân kì trong khi GD hội tụ, với $\mathbb E\lVert g\rVert^2=164w^2$ (Ví dụ 05.11).
- **Oracle không chệch.** Độ chênh của $L_S$ tiến tới $0{,}16$ khi $T$ tăng, không về $0$ (Ví dụ 05.13).

Định lý không nói gì về điểm lặp cuối: trong Ví dụ 05.12, điểm lặp cuối dao động ở mức $f=0{,}1$ và không hội tụ về $0$, trong khi điểm lặp trung bình bằng $0$ khi $T$ chẵn.

Mọi cận của bài nói về hàm mục tiêu mà oracle không chệch; với chỉ số rút từ $S$, đó là $L_S$. Các cận không nói gì về $L_D$, cũng không nói gì về tỉ lệ lỗi phân lớp khi tối thiểu hóa hàm lỗi bản lề hay logistic. Tính lồi là điều kiện của (G1) và của Bước 5 trong chứng minh, nên các cận không chuyển sang mạng nơ-ron mà không có lập luận mới.

## 12. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 05](material-viewer.html?doc=materials/lec-05/exercises.md). Sáu bài đầu là bài gốc, sáu bài sau chọn từ UML.

1. **Bài tập 05.1** (Tính lồi và dưới vi phân của hàm lỗi bản lề): mục tiêu 1.
2. **Bài tập 05.2** (Bất đẳng thức một bước và vai của phép chiếu): mục tiêu 1.
3. **Bài tập 05.3** (Bước kì vọng có điều kiện trong chứng minh): mục tiêu 2, 5.
4. **Bài tập 05.4** (Chọn độ dài bước từ cận): mục tiêu 3.
5. **Bài tập 05.5** (Số lần cập nhật và số quan sát của GD, SGD và lô nhỏ): mục tiêu 3, 4.
6. **Bài tập 05.6** (Mức sàn sai số với độ dài bước hằng, thực nghiệm tùy chọn): mục tiêu 5.
7. **Bài tập 05.7** (Cực tiểu địa phương của rủi ro thực nghiệm với hàm lỗi 0–1; UML Bài tập 12.1): mục tiêu 5.
8. **Bài tập 05.8** (Hồi quy logistic: lồi, Lipschitz và trơn; UML Bài tập 12.2): mục tiêu 1.
9. **Bài tập 05.9** (Hàm lỗi bản lề là Lipschitz; UML Bài tập 12.3): mục tiêu 1.
10. **Bài tập 05.10** (Perceptron như hạ gradient trên một hàm lồi; UML Bài tập 14.3, ý 1–3): mục tiêu 1, 3.
11. **Bài tập 05.11** (Độ dài bước giảm dần với phép chiếu; UML Bài tập 14.4, thêm phép chiếu): mục tiêu 1, 3.
12. **Bài tập 05.12** (Tùy chọn: ma trận $\sum_ix_ix_i^\top$ khả nghịch và tính lồi mạnh; UML Bài tập 9.2, thêm tính lồi mạnh): phần mở rộng của §4.

## 13. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Phân bố $D$ trên $\mathbb R\times\mathbb R$: $X=1$, còn $Y$ nhận $1$ và $-1$ với xác suất $\tfrac12$ mỗi giá trị. Mẫu chỉ có một quan sát, $S=((1,1))$. Hàm lỗi bình phương $\ell(w,(x,y))=(wx-y)^2$, $W=[-1,1]$, $w_1=0$. SGD có chiếu rút chỉ số đều trên $\{1\}$, với $T=1600$ và độ dài bước của Hệ quả 05.15.

(a) Viết $\psi(w)$. Nó là đạo hàm của $L_S$ hay của $L_D$?

(b) Tính $G$, $R$, $\eta$ và cận mà Hệ quả 05.15 cho. Cận đó chặn đại lượng nào?

(c) Tính $\bar w_{1600}$, $L_S(\bar w_{1600})$ và $L_D(\bar w_{1600})$, và so với $\min_WL_D$.

::: solution Lời giải câu hỏi cuối buổi
**(a)** Ta có $L_S(w)=(w-1)^2$ và
$$
\begin{aligned}
L_D(w)&=\tfrac12(w-1)^2\\
&\quad+\tfrac12(w+1)^2\\
&=w^2+1 .
\end{aligned}
$$
Oracle trả về $\varphi(w,1)=2(w-1)$, nên $\psi(w)=2(w-1)=L_S'(w)$, còn $L_D'(w)=2w$. Oracle không chệch cho $L_S$. Chỉ có một chỉ số, nên oracle tất định và SGD trùng GD.

**(b)** Trên $W$, $\lvert\psi(w)\rvert=2\lvert w-1\rvert\le4$, nên $G=4$. Mọi $u\in W$ thỏa $\lvert w_1-u\rvert\le1$, nên $R=1$. Do đó $\eta=1/(4\cdot40)=0{,}00625$, và Hệ quả 05.15(b) cho
$$
\begin{aligned}
&L_S(\bar w_{1600})-\min_WL_S\\
&\quad\le\frac{1\cdot4}{40}=0{,}1,
\end{aligned}
$$
với $\min_WL_S=L_S(1)=0$. Cận chặn sai số tối ưu thực nghiệm $\operatorname{opt}_S$, không chặn $L_D$.

**(c)** Mọi điểm lặp nằm trong $[0,1]$, nên phép chiếu không tác động. Cập nhật $w_{t+1}=w_t-2\eta(w_t-1)$ cho $1-w_{t+1}=(1-2\eta)(1-w_t)=0{,}9875\,(1-w_t)$, nên $1-w_t=0{,}9875^{t-1}$. Lấy trung bình và dùng tổng cấp số nhân,
$$
\begin{aligned}
1-\bar w_{1600}&=\frac1{1600}\sum_{t=1}^{1600}0{,}9875^{t-1}\\
&=\frac{1-0{,}9875^{1600}}{1600\cdot0{,}0125}\\
&\approx\frac1{20}=0{,}05,
\end{aligned}
$$
vì $0{,}9875^{1600}\approx1{,}8\cdot10^{-9}$.
Vậy $\bar w_{1600}\approx0{,}95$, $L_S(\bar w_{1600})\approx0{,}0025\le0{,}1$ và $L_D(\bar w_{1600})\approx0{,}9025+1=1{,}9025$. Với lớp hàm điểm số $\{h_w:w\in W\}$, $\min_WL_D=L_D(0)=1$, nên sai số ước lượng của $\bar w_{1600}$ (Định nghĩa 04.1) khoảng $0{,}9025$, trong khi sai số tối ưu thực nghiệm chỉ khoảng $0{,}0025$.
:::

Khi chỉ số được rút từ mẫu $S$, oracle không chệch cho $L_S$, và Định lý 05.14 kiểm soát sai số tối ưu thực nghiệm $\operatorname{opt}_S$. Trong câu hỏi cuối buổi, $\operatorname{opt}_S$ nhỏ trong khi $L_D$ còn xa mức tốt nhất.

Bài 06 so sánh hai cách dùng dữ liệu có cùng phép cập nhật: rút một quan sát mới từ $D$ ở mỗi bước, hoặc chạy nhiều vòng qua cùng mẫu $S$. Câu hỏi cho Bài 06 là: với mỗi cách, gradient ngẫu nhiên không chệch cho hàm nào, và khi nào tối thiểu hóa trên $S$ cũng kiểm soát được $L_D$? Chính quy hóa và tính ổn định của thuật toán là hai công cụ của Bài 06.

## 14. Tài liệu đọc

- **Trước buổi học:** UML §12.1 (tính lồi, tính Lipschitz, tính trơn), §14.1 (hạ gradient).
- **Sau buổi học:** UML §14.2 (dưới gradient), §14.3 (hạ gradient ngẫu nhiên), §14.4.1 (bước chiếu), §9.2 (hồi quy tuyến tính), §12.2 (bài toán học lồi); các bài tập UML §9.6, §12.6, §14.8 đã chọn ở §12.
- **Mở rộng:** UML §14.4.2–14.4.4 (độ dài bước thay đổi, các cách lấy trung bình khác, hàm lồi mạnh), §12.3 (hàm lỗi thay thế, surrogate loss). UML §12.3 gọi hiệu giữa hai giá trị nhỏ nhất là "optimization error"; tên này không được dùng ở đây, vì sai số tối ưu thực nghiệm $\operatorname{opt}_S$ của Bài 04 là một đại lượng khác.

**Quan hệ với giáo trình UML.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục. Các khác biệt chính:

- **Thiết lập.** UML §14.3 xét điểm khởi tạo $0$, không chiếu, gradient ngẫu nhiên bị chặn hầu chắc chắn và một độ dài bước đã chọn. Ở đây có phép chiếu (UML §14.4.1), điểm khởi tạo bất kì trong $W$, cận mô-men bậc hai và mọi $\eta$.
- **Đối tượng so sánh.** UML phát biểu §14.1 và §14.3 với một nghiệm tối ưu trên quả cầu (§14.1.1 ghi rằng lập luận đúng cho mọi điểm so sánh). Ở đây kết quả đúng với mọi $u$ trong một tập lồi đóng $W$, kể cả khi không có nghiệm tối ưu.
- **Oracle.** UML đặt điều kiện lên kì vọng có điều kiện của véc-tơ cập nhật; ở đây điều kiện đó là một bổ đề (Bổ đề 05.12), suy ra từ ánh xạ $\varphi(w,\xi)$ và các lần rút độc lập.
- **Kí hiệu.** Phép chiếu viết $\operatorname{proj}_W$; UML viết phép chiếu dạng $\arg\min$, còn kí hiệu $\Pi_W$ của đề cương học phần trùng hàm tăng trưởng $\Pi_{\mathcal H}$ của Bài 03. Hằng số Lipschitz là $G$ (UML: $\rho$).
- **Lô nhỏ.** Mệnh đề 05.20 không có trong các mục UML trên.

## Phụ lục

### A. Phép chiếu lên tập lồi đóng

Các khẳng định sau Định nghĩa 05.7 và phần còn lại của Bổ đề 05.8 được chứng minh dưới đây. Cố định $W\subset\mathbb R^p$ khác rỗng, đóng, lồi và $\theta\in\mathbb R^p$.

::: proof Chứng minh các khẳng định về phép chiếu
**Lộ trình.** Sự tồn tại dùng tính compact, tính duy nhất dùng đẳng thức hình bình hành, đặc trưng biến phân dùng khai triển bình phương, tính không giãn dùng hai bất đẳng thức biến phân.

**Bước 1 (tồn tại; $W$ đóng).** Lấy $w_0\in W$ và đặt $K=W\cap\{u:\lVert u-\theta\rVert\le\lVert w_0-\theta\rVert\}$. Tập $K$ khác rỗng, đóng (giao của hai tập đóng) và bị chặn, nên compact. Hàm liên tục $u\mapsto\lVert u-\theta\rVert$ đạt giá trị nhỏ nhất trên $K$ tại một điểm $\pi$. Mọi $u\in W\setminus K$ có $\lVert u-\theta\rVert>\lVert w_0-\theta\rVert\ge\lVert\pi-\theta\rVert$, nên $\pi$ là điểm gần $\theta$ nhất trong $W$. Với quả cầu mở và $\theta$ ở ngoài, $K$ không đóng và bước này hỏng.

**Bước 2 (duy nhất; $W$ lồi).** Giả sử $\pi_1\ne\pi_2$ cùng đạt khoảng cách nhỏ nhất $r$. Trung điểm $\mu=\tfrac12(\pi_1+\pi_2)$ thuộc $W$ vì $W$ lồi. Theo đẳng thức hình bình hành (parallelogram law),
$$
\begin{aligned}
&\lVert \theta-\mu\rVert^2\\
&\quad=\tfrac12\lVert \theta-\pi_1\rVert^2+\tfrac12\lVert \theta-\pi_2\rVert^2\\
&\qquad-\tfrac14\lVert\pi_1-\pi_2\rVert^2\\
&\quad<r^2,
\end{aligned}
$$
mâu thuẫn với tính nhỏ nhất của $r$.

**Bước 3 (Bổ đề 05.8(a)).** Bước 2 của chứng minh Bổ đề 05.8 cho thấy $\pi=\operatorname{proj}_W(\theta)$ thỏa bất đẳng thức biến phân. Ngược lại, giả sử $\pi'\in W$ thỏa $\langle \theta-\pi',u-\pi'\rangle\le0$ với mọi $u\in W$. Với mọi $u\in W$,
$$
\begin{aligned}
&\lVert u-\theta\rVert^2\\
&\quad=\lVert u-\pi'\rVert^2+\lVert\pi'-\theta\rVert^2\\
&\qquad-2\langle \theta-\pi',u-\pi'\rangle\\
&\quad\ge\lVert\pi'-\theta\rVert^2 .
\end{aligned}
$$
Vậy $\pi'$ là một điểm gần $\theta$ nhất trong $W$, và $\pi'=\pi$ theo Bước 2.

**Bước 4 (không giãn).** Cho $\theta'\in\mathbb R^p$ và $\pi'=\operatorname{proj}_W(\theta')$. Bất đẳng thức biến phân cho $\theta$ với $u=\pi'$, và cho $\theta'$ với $u=\pi$, là
$$
\begin{aligned}
\langle \theta-\pi,\pi'-\pi\rangle&\le0,\\
\langle \theta'-\pi',\pi-\pi'\rangle&\le0 .
\end{aligned}
$$
Cộng hai bất đẳng thức và sắp xếp lại, ta được $\lVert\pi-\pi'\rVert^2\le\langle \theta-\theta',\pi-\pi'\rangle\le\lVert \theta-\theta'\rVert\,\lVert\pi-\pi'\rVert$, theo Cauchy–Schwarz. Chia cho $\lVert\pi-\pi'\rVert$ khi nó dương, ta được $\lVert\pi-\pi'\rVert\le\lVert \theta-\theta'\rVert$. Đặc biệt, $\operatorname{proj}_W$ liên tục.

$\square$ Phép chiếu lên một tập lồi đóng khác rỗng xác định tốt, được đặc trưng bởi bất đẳng thức biến phân, và không giãn.
:::

### B. Kì vọng có điều kiện với nguồn ngẫu nhiên tổng quát

Khi $\Xi$ là một không gian đo bất kì, chứng minh Bổ đề 05.12 cần bổ đề đóng băng và một cận cho $\lVert w_t-u\rVert$.

::: proof Chứng minh Bổ đề 05.12 (trường hợp tổng quát)
**Lộ trình.** Tính đo được của điểm lặp theo quy nạp; kì vọng có điều kiện qua bổ đề đóng băng; tính hữu hạn của các kì vọng qua một cận cho $\lVert w_t-u\rVert$.

**Bước 1 (tính đo được).** Giả sử $w_t$ là hàm đo được của $(\xi_1,\ldots,\xi_{t-1})$. Vì $\varphi$ đo được theo cặp, $g_t=\varphi(w_t,\xi_t)$ là hàm đo được của $(\xi_1,\ldots,\xi_t)$. Phép chiếu liên tục (Phụ lục A), nên $w_{t+1}=\operatorname{proj}_W(w_t-\eta g_t)$ cũng đo được. Quy nạp bắt đầu từ $w_1$ tất định.

**Bước 2 (bổ đề đóng băng).** Chứng minh dùng *bổ đề đóng băng* (freezing lemma) sau, phát biểu không chứng minh. Cho bốn thành phần:

- **$\sigma$-đại số.** $\mathcal G$.
- **Biến đã biết.** $V$ đo được theo $\mathcal G$.
- **Biến độc lập.** $\xi$ độc lập với $\mathcal G$.
- **Hàm.** $\Phi$ đo được, với $\Phi\ge0$ hoặc $\mathbb E\lVert\Phi(V,\xi)\rVert<\infty$.

Khi đó, hầu chắc chắn,
$$
\begin{aligned}
\mathbb E[\Phi(V,\xi)\mid\mathcal G]&=\bar\Phi(V),\\
\bar\Phi(v)&=\mathbb E\,\Phi(v,\xi).
\end{aligned}
$$
Áp dụng với $\mathcal G=\mathcal F_{t-1}$, $V=w_t$ và $\xi=\xi_t$, độc lập với $\mathcal F_{t-1}$. Với $\Phi=\lVert\varphi\rVert^2\ge0$, ta có $\mathbb E[\lVert g_t\rVert^2\mid\mathcal F_{t-1}]=\bar\Phi(w_t)\le G^2$ theo (G2), vì $w_t\in W$. Lấy kì vọng, $\mathbb E\lVert g_t\rVert^2\le G^2$, nên $\mathbb E\lVert g_t\rVert<\infty$. Với $\Phi=\varphi$, ta có $\mathbb E[g_t\mid\mathcal F_{t-1}]=\psi(w_t)\in\partial F(w_t)$ theo (G1). Đây là phần (b).

**Bước 3 (tính hữu hạn).** Theo Bổ đề 05.8(b) và bất đẳng thức tam giác,
$$
\begin{aligned}
&\lVert w_{t+1}-u\rVert\\
&\quad\le\lVert w_t-\eta g_t-u\rVert\\
&\quad\le\lVert w_t-u\rVert+\eta\lVert g_t\rVert .
\end{aligned}
$$
Dùng $(a+b)^2\le2a^2+2b^2$ và quy nạp, $\mathbb E\lVert w_t-u\rVert^2<\infty$ với mọi $t$. Theo Cauchy–Schwarz hai lần, $\mathbb E\lvert\langle g_t,w_t-u\rangle\rvert\le(\mathbb E\lVert g_t\rVert^2)^{1/2}(\mathbb E\lVert w_t-u\rVert^2)^{1/2}<\infty$. Với $w\in W$, (G1) và $\lVert\psi\rVert\le G$ trên $W$ cho hai bất đẳng thức dưới gradient tại $w$ và tại $u$, nên $\lvert F(w)-F(u)\rvert\le G\lVert w-u\rVert$. Hàm $F$ lồi và hữu hạn trên $\mathbb R^p$ nên liên tục, do đó $F(w_t)$ đo được, và $\mathbb E\lvert F(w_t)\rvert\le\lvert F(u)\rvert+G\,\mathbb E\lVert w_t-u\rVert<\infty$. Cùng cận áp dụng cho $\bar w_T\in W$.

**Bước 4 (phần c).** Tích $\langle g_t,w_t-u\rangle$ khả tích và $w_t-u$ đo được theo $\mathcal F_{t-1}$. Theo tính chất tháp và quy tắc lấy ra đại lượng đã biết,
$$
\begin{aligned}
&\mathbb E\langle g_t,w_t-u\rangle\\
&\quad=\mathbb E\big\langle\mathbb E[g_t\mid\mathcal F_{t-1}],w_t-u\big\rangle\\
&\quad=\mathbb E\langle\psi(w_t),w_t-u\rangle .
\end{aligned}
$$

$\square$ Định lý 05.14 không cần lựa chọn đo được (measurable selection) nào ngoài tính đo được của $\varphi$. Một lựa chọn đo được chỉ cần khi dựng oracle từ dưới vi phân $\partial\ell(\cdot,z)$; với hàm lỗi bình phương, bản lề và logistic, các công thức tường minh của bài là đo được Borel.
:::

### C. Chứng minh Nhận xét 05.17

::: proof Chứng minh Nhận xét 05.17
**Lộ trình.** Như chứng minh Định lý 05.14, với trọng số $\eta_t$ thay cho trọng số đều.

**Bước 1 (một bước).** Mệnh đề 05.13 với độ dài bước $\eta_t$, nhân hai vế với $\eta_t>0$, cho
$$
\begin{aligned}
\eta_t\langle g_t,w_t-u\rangle&\le\tfrac12(\Delta_t-\Delta_{t+1})\\
&\quad+\tfrac{\eta_t^2}2\lVert g_t\rVert^2 .
\end{aligned}
$$

**Bước 2 (tổng và kì vọng).** Cộng theo $t$ và bỏ $-\Delta_{T+1}\le0$. Bổ đề 05.12 vẫn đúng với dãy $\eta_t$ tất định, với cùng chứng minh; Bước 3 và 4 của chứng minh Định lý 05.14 cho
$$
\begin{aligned}
&\sum_{t=1}^T\eta_t\,\mathbb E\big[F(w_t)-F(u)\big]\\
&\quad\le\tfrac12\Delta_1+\tfrac{G^2}2\sum_{t=1}^T\eta_t^2 .
\end{aligned}
$$

**Bước 3 (trung bình có trọng số).** Theo bất đẳng thức lồi hữu hạn với trọng số $\eta_t/\sum_s\eta_s$, $F(\tilde w_T)\le\sum_t\eta_tF(w_t)/\sum_s\eta_s$ trên từng quỹ đạo. Lấy kì vọng và chia cho $\sum_t\eta_t$, ta được cận của Nhận xét 05.17.

**Bước 4 (bằng số).** Với $\eta_t=1/(4\sqrt t)$ và $T=1600$, ta có $\sum_t\eta_t\approx19{,}638$ và $\sum_t\eta_t^2=\tfrac1{16}\sum_{t\le1600}\tfrac1t\approx\tfrac{7{,}9553}{16}\approx0{,}4972$. Do đó
$$
\begin{aligned}
\frac{1+16\cdot0{,}4972}{2\cdot19{,}638}&\approx\frac{8{,}955}{39{,}276}\\
&\approx0{,}2280 .
\end{aligned}
$$
Tổng $\sum_{t\le T}1/t$ xấp xỉ $\ln T+0{,}577$, nên thừa số $\ln T$ đến từ số hạng $G^2\sum_t\eta_t^2$.

$\square$ Độ dài bước giảm dần cho cận lớn hơn cận của độ dài bước hằng một thừa số cỡ $\ln T$.
:::

### D. Tính toán chi tiết cho ví dụ hồi quy

**Dạng bậc hai.** Với mẫu của Ví dụ 05.1, khai triển $L_S(w)=\tfrac13\sum_i(\langle w,x_i\rangle-y_i)^2$ cho
$$
L_S(w)=w^\top Mw-2c^\top w+\tfrac23,
$$
trong đó $M=\tfrac13\sum_ix_ix_i^\top=\begin{pmatrix}0{,}4533&0{,}16\\0{,}16&0{,}5467\end{pmatrix}$ và $c=\tfrac13\sum_iy_ix_i=(\tfrac13,-\tfrac13)$. Gradient là $\nabla L_S(w)=2(Mw-c)$.

**Nghiệm không ràng buộc.** Giải $Mw=c$, ta được $w=(1{,}06;-0{,}92)$, có chuẩn $1{,}404>1$ và $L_S\approx0{,}00667$. Điểm này nằm ngoài $W=\{w:\lVert w\rVert\le1\}$.

**Nghiệm trên quả cầu.** Tìm $w^*$ với $\lVert w^*\rVert=1$ và $\nabla L_S(w^*)=-2\kappa w^*$ cho một $\kappa\ge0$, tức $(M+\kappa I)w^*=c$. Hàm $\kappa\mapsto\lVert(M+\kappa I)^{-1}c\rVert$ giảm; giải $\lVert(M+\kappa I)^{-1}c\rVert=1$ bằng chia đôi, ta được $\kappa\approx0{,}1350$, $w^*\approx(0{,}7473;-0{,}6645)$ và $L_S(w^*)\approx0{,}06112$.

**Kiểm tra tối ưu.** Với mọi $u\in W$, $\langle w^*,u\rangle\le1$ theo Cauchy–Schwarz, nên
$$
\begin{aligned}
&\langle\nabla L_S(w^*),u-w^*\rangle\\
&\quad=-2\kappa\big(\langle w^*,u\rangle-1\big)\ge0 .
\end{aligned}
$$
Theo Mệnh đề 05.3(a), $L_S(u)\ge L_S(w^*)+\langle\nabla L_S(w^*),u-w^*\rangle\ge L_S(w^*)$. Vậy $w^*$ là nghiệm tối ưu của $L_S$ trên $W$. Theo Bổ đề 05.8(a), điều kiện trên tương đương với $w^*=\operatorname{proj}_W\big(w^*-\eta\nabla L_S(w^*)\big)$ với mọi $\eta>0$.
