# Bài 03 — Chiều VC và hàm phân lớp tuyến tính

Định lý 02.14 và Hệ quả 02.16 cho cỡ mẫu đủ theo $\ln K$, trong đó $K=\lvert\mathcal H\rvert$ là số giả thuyết (hypothesis) của một lớp giả thuyết (hypothesis class) hữu hạn, chọn trước khi lấy mẫu. Lớp hàm ngưỡng (threshold) trên $\mathbb R$ và lớp hàm phân lớp tuyến tính (linear classifier) trong $\mathbb R^p$ có vô số phần tử, nên hai kết quả đó không áp dụng được.

Ngoài vài lớp có cấu trúc riêng, như ở Bài tập 01.9 và 02.7, chúng ta chưa có cận cỡ mẫu cho lớp vô hạn. Câu hỏi trung tâm của bài là: đại lượng nào của một lớp vô hạn thay cho $\ln\lvert\mathcal H\rvert$ trong cận cỡ mẫu? Ba công cụ là chiều Vapnik–Chervonenkis (VC dimension), gọi tắt là chiều VC, hàm tăng trưởng (growth function) và mẫu bóng (ghost sample). Chúng cho một cận hội tụ đều (uniform convergence) trên lớp có chiều VC hữu hạn và một bảo đảm cho tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM). Kết quả cuối là định lý cơ bản (fundamental theorem) của học xấp xỉ với xác suất cao (probably approximately correct, PAC) cho phân lớp nhị phân (binary classification).

## Câu hỏi mở đầu

Mỗi hàm ngưỡng $h_t(x)=\mathbb 1[x\ge t]$, $t\in\mathbb R$, được xác định bởi một số thực $t$, và trên năm mức đo của ví dụ sàng lọc, cả lớp chỉ cho sáu hàm khác nhau.

**Câu hỏi.** Bao nhiêu quan sát là đủ để, với xác suất ít nhất $0{,}95$ và với mọi phân bố, mọi nghiệm ERM trên lớp hàm ngưỡng có rủi ro vượt mức (excess risk) không quá $0{,}1$?

Không thể đếm số tham số thay cho $\ln\lvert\mathcal H\rvert$: lớp các hàm $x\mapsto\mathbb 1[\sin(\theta x)>0]$, $\theta\in\mathbb R$, cũng chỉ có một tham số, nhưng nhận được mọi tổ hợp nhãn $0$, $1$ trên những tập điểm lớn tùy ý. Đại lượng cần tìm đếm số tổ hợp nhãn mà lớp tạo ra trên các tập điểm hữu hạn. Câu trả lời bằng số cho lớp hàm ngưỡng: theo cận của bài, $54\,330$ quan sát là đủ.

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Tính chiều VC của lớp hàm ngưỡng, lớp khoảng và lớp nửa không gian bằng cận dưới và cận trên, và nhận ra một lập luận chỉ có một trong hai phần.
2. Tính hàm tăng trưởng của các lớp đơn giản, so sánh với cận Sauer–Shelah và với số mọi cách gán nhãn, và giải thích vì sao số cách gán nhãn bị chặn bởi một đa thức của số điểm khi chiều VC hữu hạn.
3. Trình bày năm bước chứng minh cận hội tụ đều theo chiều VC và chỉ ra chỗ dùng từng giả thiết. Giải thích vì sao không lấy bất đẳng thức hợp trên các cách gán nhãn của chính tập huấn luyện.
4. Tính cận độ lệch đều và cỡ mẫu đủ cho ERM từ chiều VC, và so sánh với cận của lớp hữu hạn sau khi rời rạc hóa tham số, chỉ ra nguồn chênh lệch.
5. Phát biểu định lý cơ bản cho phân lớp nhị phân, và dựng phản ví dụ khi bỏ chiều VC hữu hạn, khi lớp được chọn sau khi xem mẫu, hoặc khi thay chiều VC bằng số tham số.

## Kiến thức tiên quyết

- **Từ Bài 01.**
  - Thuật toán học và điều kiện đo được của nó (Định nghĩa 01.4); ERM, $\epsilon_{\mathrm{opt}}$-ERM và hai mức (O1), (O2) của giả thiết tối ưu (Định nghĩa 01.8, 01.12); sự tồn tại nghiệm ERM với hàm lỗi 0–1 (Nhận xét 01.11).
  - Lớp $\mathcal M_{\mathcal X}$ và hàm phân lớp ghi nhớ (Ví dụ 01.8, Mệnh đề 01.15); tính khả diễn, hai định nghĩa học PAC, độ phức tạp mẫu (sample complexity; Định nghĩa 01.16, 01.18, 01.20, 01.25; Nhận xét 01.17, 01.21, 01.26).
  - Hệ quả 01.29, Nhận xét 01.30 (định lý không có bữa trưa miễn phí); ví dụ sàng lọc (Ví dụ 01.1); Phụ lục A(v) (tính đo được với lớp vô hạn).
- **Từ Bài 02.** Bất đẳng thức Chebyshev (Bổ đề 02.3), bất đẳng thức Hoeffding (Định lý 02.7) và bất đẳng thức hợp (union bound; Bổ đề 02.12). Mẫu $\epsilon$-đại diện (Định nghĩa 02.13), Định lý 02.14, Hệ quả 02.16, Ví dụ 02.6, Nhận xét 02.18; các giả thiết (T1)–(T4).
- **Đại số tuyến tính và hình học.** $p+1$ véc-tơ trong $\mathbb R^p$ phụ thuộc tuyến tính; hệ phương trình tuyến tính thuần nhất có nhiều ẩn hơn phương trình có nghiệm khác $0$; ma trận vuông khả nghịch. Một *tổ hợp lồi* (convex combination) của $x_1,\ldots,x_k$ là $\sum_i\lambda_ix_i$ với $\lambda_i\ge0$, $\sum_i\lambda_i=1$; *bao lồi* (convex hull) $\operatorname{conv}\{x_1,\ldots,x_k\}$ là tập mọi tổ hợp lồi đó. Các điểm $x_0,\ldots,x_k$ là *độc lập afin* (affinely independent) khi $x_1-x_0,\ldots,x_k-x_0$ độc lập tuyến tính.
- **Tổ hợp và giải tích.** Hệ số nhị thức, công thức Pascal (Pascal's rule) $\binom mj=\binom{m-1}j+\binom{m-1}{j-1}$, khai triển nhị thức; $1+x\le e^x$ với mọi $x\in\mathbb R$.

**Câu hỏi ôn nhanh.**

1. Tính $\sum_{j=0}^{2}\binom5j$ và so sánh với $2^5$.
2. Cho ba điểm $(0,0)$, $(1,0)$, $(0,1)$ của $\mathbb R^2$. Tìm $w\in\mathbb R^2$ và $b\in\mathbb R$ sao cho $\mathbb 1[\langle w,x\rangle+b\ge0]$ bằng $0$ tại $(0,0)$ và bằng $1$ tại hai điểm còn lại.
3. Cho $V_1,\ldots,V_m$ độc lập, $\mathbb EV_i=0$, $-1\le V_i\le1$, đặt $\bar V_m=\frac1m\sum_{i=1}^mV_i$ và cho $\epsilon>0$. Dùng Định lý 02.7 để chặn $\Pr(\lvert\bar V_m\rvert\ge\epsilon)$.

::: solution Lời giải câu hỏi ôn nhanh
1. $\binom50+\binom51+\binom52=1+5+10=16$, bằng nửa của $2^5=32$.
2. Chẳng hạn $b=-1$ và $w=(2,2)$. Giá trị của $\langle w,x\rangle+b$ tại ba điểm là $-1$, $1$, $1$, nên hàm chỉ báo cho $0$, $1$, $1$.
3. Miền giá trị $[-1,1]$ dài $b-a=2$, nên Định lý 02.7(c) cho
$$
\begin{aligned}
&\Pr(\lvert\bar V_m\rvert\ge\epsilon)\\
&\quad\le2\exp(-2m\epsilon^2/4)\\
&\quad=2e^{-m\epsilon^2/2}.
\end{aligned}
$$
:::

## 1. Thiết lập bài toán

Bài toán giữ tám thành phần của §1 Bài 02, với các lựa chọn sau.

1. **Tập quan sát và phân bố dữ liệu.** $\mathcal Z=\mathcal X\times\{0,1\}$, với $\mathcal X$ có một σ-đại số (σ-algebra) ($\mathbb R^p$ với σ-đại số Borel trong các ví dụ); phân bố $D$ trên $\mathcal Z$ cố định nhưng chưa biết.
2. **Tập huấn luyện.** $S=(Z_1,\ldots,Z_m)\sim D^m$, với $Z_i=(X_i,Y_i)$, theo (T1).
3. **Lớp giả thuyết.** $\mathcal H$ gồm các hàm phân lớp (classifier) đo được $\mathcal X\to\{0,1\}$, có thể vô hạn, chọn trước khi lấy mẫu.
4. **Hàm lỗi.** Hàm lỗi 0–1 (0–1 loss) $\ell_{0\text{-}1}(h,(x,y))=\mathbb 1[h(x)\ne y]$; nó thỏa (T2) và (T3).
5. **Quy tắc dùng mẫu.** Một thuật toán ERM bất kì trên $\mathcal H$, hoặc một $\epsilon_{\mathrm{opt}}$-ERM.
6. **Mục tiêu.** Hai đại lượng cần chặn:
   - Độ lệch đều (uniform deviation): $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$ giữa rủi ro thực nghiệm (empirical risk) và rủi ro kì vọng (population risk);
   - Rủi ro vượt mức (excess risk): $L_D(\hat h)-\inf_{h\in\mathcal H}L_D(h)$ của nghiệm ERM $\hat h$.
7. **Đối tượng so sánh.** Mức tốt nhất trong lớp giả thuyết $$\inf_{h\in\mathcal H}L_D(h),$$ với lớp vô hạn, cận dưới đúng này có thể không đạt (Nhận xét 01.17).
8. **Tài nguyên.** Cỡ mẫu $m$. Câu trả lời là một cỡ mẫu đủ, viết theo một đại lượng của lớp, $\epsilon$ và $\delta$, không theo $\lvert\mathcal H\rvert$.

Các đại lượng của bài chia theo nguồn ngẫu nhiên như bảng dưới.

| Loại | Đại lượng |
|---|---|
| Cố định | $D$, $\mathcal H$, mỗi $h\in\mathcal H$, $L_D(h)$, $\inf_{h\in\mathcal H}L_D(h)$ |
| Ngẫu nhiên theo $S\sim D^m$ | $S$, $L_S(h)$, véc-tơ giá trị $(h(X_1),\ldots,h(X_m))$ của mỗi $h$, độ lệch đều, $\hat h$, $L_D(\hat h)$ |

## 2. Kí hiệu và giả thiết

Kí hiệu chung theo bảng kí hiệu của học phần và Bài 01–02. Bảng dưới gồm các kí hiệu dùng trong bài; chiều VC, hàm tăng trưởng và mỗi kí hiệu khác được đặt tên tại định nghĩa của nó.

| Kí hiệu | Ý nghĩa |
|---|---|
| $h_t(x)=\mathbb 1[x\ge t]$, $t\in\mathbb R$ | hàm ngưỡng, cùng công thức với Ví dụ 01.1 |
| $p$ | số chiều đặc trưng, $\mathcal X=\mathbb R^p$ |
| $\langle w,x\rangle$ | tích vô hướng trong $\mathbb R^p$ |
| $\ln$ | lôgarit tự nhiên |
| $\epsilon$ | độ lệch đều ở §7; cận cho rủi ro vượt mức ở §8, trừ các phát biểu khả diễn ở §8, nơi $\epsilon$ là cận cho rủi ro |

Các giả thiết thống kê của Bài 01–02 được dùng lại, với (T4) thay bằng (T5) để cho phép lớp vô hạn.

- **(T1) Lấy mẫu.** $Z_1,\ldots,Z_m$ độc lập cùng phân bố theo $D$.
- **(T2) Hàm lỗi.** $\ell\ge0$ và $\ell(h,\cdot)$ đo được với mọi $h\in\mathcal H$.
- **(T3) Hàm lỗi bị chặn.** $\ell(h,z)\in[0,1]$ với mọi $h\in\mathcal H$ và mọi $z\in\mathcal Z$.
- **(T5) Lớp cố định trước khi lấy mẫu.** $\mathcal H$, hữu hạn hoặc vô hạn, được chọn trước và không phụ thuộc $S$. Giả thiết (T4) của Bài 02 là (T5) cộng điều kiện $\mathcal H$ hữu hạn.
- **(M) Lớp xấp xỉ được bởi một lớp con đếm được.** Có một lớp con đếm được (countable subclass) $\mathcal H_0\subseteq\mathcal H$ sao cho mỗi $h\in\mathcal H$ là giới hạn theo từng điểm (pointwise limit) của một dãy $h_k\in\mathcal H_0$, tức $h_k(x)\to h(x)$ với mọi $x\in\mathcal X$.
- **(O1) Thuật toán trả về một nghiệm ERM chính xác.** $\hat h\in\arg\min_{h\in\mathcal H}L_S(h)$.
- **(O2) Thuật toán trả về một nghiệm $\epsilon_{\mathrm{opt}}$-ERM.** $\hat h\in\mathcal H$ với $L_S(\hat h)\le\inf_{h\in\mathcal H}L_S(h)+\epsilon_{\mathrm{opt}}$.
- **Khả diễn.** Phân bố $D$ khả diễn đối với $\mathcal H$ (Định nghĩa 01.16): có $h^\star\in\mathcal H$ với $L_D(h^\star)=0$.

Không kết quả nào dùng giả thiết lồi, trơn hay Lipschitz.

## 3. Ví dụ xuyên suốt

::: example Ví dụ 03.1 (Lớp hàm ngưỡng trên đường thẳng thực)
**Thiết lập.** $\mathcal X=\mathbb R$, $\mathcal Y=\{0,1\}$ và lớp
$$
\begin{aligned}
h_t(x)&=\mathbb 1[x\ge t],\\
\mathcal H_{\mathrm{thr}}&=\{h_t:\ t\in\mathbb R\}.
\end{aligned}
$$
Công thức trùng với Ví dụ 01.1, nhưng $t$ chạy trên $\mathbb R$ thay cho $\{1,\ldots,6\}$. Ví dụ chỉ xét lớp và các bộ điểm, không cần phân bố.

**Bước 1: lớp vô hạn.** Với hai ngưỡng $t<t'$, hai hàm $h_t$ và $h_{t'}$ khác nhau đúng trên khoảng $[t,t')$. Do đó mỗi ngưỡng cho một hàm khác, và $\mathcal H_{\mathrm{thr}}$ có vô số phần tử.

**Bước 2: Định lý 02.14 không áp dụng.** Định lý 02.14 cần $K=\lvert\mathcal H\rvert$ hữu hạn, nên ở đây bán kính $r_m=\sqrt{\ln(2K/\delta)/(2m)}$ không xác định.

**Bước 3: số véc-tơ giá trị trên một mẫu.** Xét các đầu vào $x_1<\cdots<x_m$. Véc-tơ $(h_t(x_1),\ldots,h_t(x_m))$ chỉ phụ thuộc số điểm $x_i$ nằm bên trái $t$, một số nguyên từ $0$ đến $m$. Do đó lớp vô hạn này chỉ cho $m+1$ véc-tơ khác nhau trên $m$ điểm phân biệt.

Rủi ro thực nghiệm $L_S(h_t)$ chỉ phụ thuộc véc-tơ trên, nên trên mỗi mẫu nó nhận nhiều nhất $m+1$ giá trị khác nhau khi $t$ chạy trên $\mathbb R$. Điều này chưa cho phép thay $K$ bằng $m+1$ trong Định lý 02.14.
:::

::: application Hàm phân lớp tuyến tính trên mười chỉ số đo
**Đặc trưng.** Mỗi người được mô tả bởi $p=10$ chỉ số đo, nên $x\in\mathbb R^{10}$.

**Lớp.** Các hàm $h_{w,b}(x)=\mathbb 1[\langle w,x\rangle+b\ge0]$ với $w\in\mathbb R^{10}$ và $b\in\mathbb R$: kết quả dương tính khi một tổ hợp tuyến tính của các chỉ số đo vượt ngưỡng $-b$.

**Câu hỏi thực hành.** Bao nhiêu quan sát là đủ để rủi ro vượt mức của mọi nghiệm ERM không quá $0{,}1$ với xác suất ít nhất $0{,}95$, với mọi phân bố? Con số đó thay đổi thế nào khi chỉ dùng hai chỉ số đo thay cho mười?
:::

Cả hai lớp đều vô hạn, nên chúng ta cần một đại lượng đo lớp trên các tập điểm hữu hạn.

## 4. Thu hẹp, tách trọn và chiều VC

Định lý 02.14 đếm $K=\lvert\mathcal H\rvert$ giả thuyết. Trên một tập huấn luyện cố định, $L_S(h)$ chỉ phụ thuộc các giá trị của $h$ tại $m$ đầu vào, nên ta cần đếm số véc-tơ giá trị khác nhau mà lớp tạo ra trên các đầu vào đó.

::: definition Định nghĩa 03.1 (Thu hẹp của một lớp lên một bộ điểm)
Cho lớp $\mathcal H$ các hàm $\mathcal X\to\{0,1\}$, số nguyên $k\ge1$ và bộ điểm $C=(x_1,\ldots,x_k)\in\mathcal X^k$, trong đó các điểm có thể trùng nhau. Mỗi $y\in\{0,1\}^k$ được gọi là một *cách gán nhãn* (labeling) của $C$, tức một tổ hợp nhãn $0$, $1$ trên các điểm của $C$. *Thu hẹp* (restriction) của $\mathcal H$ lên $C$ là tập
$$
\begin{aligned}
\mathcal H_C=\big\{&(h(x_1),\ldots,h(x_k)):\\
&h\in\mathcal H\big\}\subseteq\{0,1\}^k .
\end{aligned}
$$
Một cách gán nhãn thuộc $\mathcal H_C$ được gọi là *thực hiện được* (realized) bởi $\mathcal H$. Với một tập hữu hạn $C\subseteq\mathcal X$, ta liệt kê các phần tử của nó theo một thứ tự cố định và dùng cùng kí hiệu $\mathcal H_C$.
:::

Thu hẹp chỉ phụ thuộc $\mathcal H$ và $C$, không phụ thuộc phân bố hay tập huấn luyện. Ta luôn có $\lvert\mathcal H_C\rvert\le\min\{\lvert\mathcal H\rvert,2^k\}$, vì mỗi hàm cho một véc-tơ và có $2^k$ véc-tơ nhị phân độ dài $k$. Với $C=(X_1,\ldots,X_m)$ lấy từ tập huấn luyện, $L_S(h)=\frac1m\sum_i\mathbb 1[h(X_i)\ne Y_i]$ là hàm của véc-tơ $(h(X_1),\ldots,h(X_m))$, nên trên tập huấn luyện đó $L_S$ chỉ phụ thuộc $h$ qua $\lvert\mathcal H_C\rvert$ véc-tơ.

Một cách gán nhãn có thể không thực hiện được. Với $\mathcal H_{\mathrm{thr}}$ và $C=(1,2)$, cách gán nhãn $(1,0)$ đòi $1\ge t$ và $2<t$, vô lý.

::: example Ví dụ 03.2 (Sáu hàm ngưỡng của ví dụ sàng lọc là một thu hẹp)
**Thiết lập.** Lớp $\mathcal H_{\mathrm{thr}}$ của Ví dụ 03.1 và bộ điểm $C=(1,2,3,4,5)$, năm mức đo của Ví dụ 01.1. Ví dụ không cần phân bố.

**Bước 1: chia theo vị trí của $t$.** Có ba trường hợp.

- Với $t\le1$, mọi điểm thỏa $x\ge t$, nên $h_t$ cho $(1,1,1,1,1)$.
- Với $t\in(k-1,k]$, $k=2,\ldots,5$, các điểm $1,\ldots,k-1$ nhận nhãn $0$ và các điểm $k,\ldots,5$ nhận nhãn $1$.
- Với $t>5$, $h_t$ cho $(0,0,0,0,0)$.

**Bước 2: liệt kê.** Thu hẹp gồm sáu véc-tơ
$$
\begin{aligned}
&(1,1,1,1,1),\ (0,1,1,1,1),\\
&(0,0,1,1,1),\ (0,0,0,1,1),\\
&(0,0,0,0,1),\ (0,0,0,0,0).
\end{aligned}
$$
Đây đúng là giá trị của sáu hàm $h_1,\ldots,h_6$ của Ví dụ 01.1 trên $\{1,\ldots,5\}$.

**Bước 3: đếm.** $\lvert\mathcal H_C\rvert=6$, trong khi $C$ có $2^5=32$ cách gán nhãn.

Tóm lại, lớp sáu hàm ngưỡng mà Bài 02 dùng với $K=6$ chính là thu hẹp của một lớp vô hạn lên năm điểm.
:::

Nếu lớp thực hiện được mọi cách gán nhãn của một tập điểm thì, dù các nhãn quan sát trên tập đó là gì, lớp vẫn có một giả thuyết với rủi ro thực nghiệm bằng $0$.

::: definition Định nghĩa 03.2 (Tập bị tách trọn)
Cho lớp $\mathcal H$ các hàm $\mathcal X\to\{0,1\}$ và tập hữu hạn $C\subseteq\mathcal X$ có $k$ phần tử. Ta nói $\mathcal H$ *tách trọn* (shatters) $C$ nếu $\lvert\mathcal H_C\rvert=2^k$, tức mọi cách gán nhãn của $C$ đều thực hiện được bởi $\mathcal H$. Quy ước: tập rỗng bị tách trọn bởi mọi lớp khác rỗng.
:::

Tách trọn là tính chất của cặp $(\mathcal H,C)$, không có $D$ hay $S$. Mọi tập con $B$ của một tập bị tách trọn $C$ cũng bị tách trọn: mở rộng một cách gán nhãn của $B$ thành một cách gán nhãn của $C$ một cách tùy ý, rồi lấy giả thuyết thực hiện cách gán nhãn mở rộng. Định nghĩa dùng tập, nên một bộ có điểm lặp không được xét: hai điểm trùng nhau luôn nhận cùng nhãn.

Lớp $\mathcal H_{\mathrm{thr}}$ tách trọn $\{0\}$, vì $h_0(0)=1$ và $h_1(0)=0$. Nó không tách trọn $\{1,2\}$, vì cách gán nhãn $(1,0)$ không thực hiện được.

::: definition Định nghĩa 03.3 (Chiều VC)
Cho lớp $\mathcal H$ khác rỗng các hàm $\mathcal X\to\{0,1\}$. *Chiều Vapnik–Chervonenkis* của $\mathcal H$, kí hiệu $d$, hoặc $\operatorname{VCdim}(\mathcal H)$ khi có nhiều lớp, là số phần tử lớn nhất của một tập hữu hạn bị $\mathcal H$ tách trọn. Nếu với mọi $k$ có một tập $k$ phần tử bị tách trọn thì $d=\infty$.
:::

Vì tập rỗng bị tách trọn, $d\ge0$. Ta có $d=0$ khi và chỉ khi không điểm nào bị tách trọn, tức mọi hàm của lớp trùng nhau trên $\mathcal X$. Chiều VC không phụ thuộc $D$, $m$ hay cách tham số hóa lớp.

Một lớp hữu hạn tách trọn một tập $d$ phần tử thì có ít nhất $2^d$ hàm, nên $d\le\log_2\lvert\mathcal H\rvert$; với lớp sáu hàm ngưỡng, $\log_26\approx2{,}585$, nên $d\le2$.

::: remark Nhận xét 03.4 (Cận dưới và cận trên cho chiều VC)
Để chứng minh $d=k$ cần hai phần. **Cận dưới:** một tập $k$ phần tử bị tách trọn, nên $d\ge k$. **Cận trên:** mọi tập $k+1$ phần tử không bị tách trọn, nên $d\le k$, vì một tập lớn hơn bị tách trọn sẽ chứa một tập con $k+1$ phần tử bị tách trọn.

Có hai lỗi đối xứng. Lỗi thứ nhất là kết luận $d=k$ từ một tập $k$ phần tử bị tách trọn; tập đó chỉ cho $d\ge k$. Lỗi thứ hai là kết luận $d\le k$ từ một tập $k+1$ phần tử không bị tách trọn; cận trên cần mọi tập $k+1$ phần tử.
:::

::: proposition Mệnh đề 03.5 (Chiều VC của lớp hàm ngưỡng) — chứng minh đầy đủ
**Giả thiết.** Hai trường hợp.

- **(a) Trên đường thẳng.** $\mathcal X=\mathbb R$ và lớp $\mathcal H_{\mathrm{thr}}$.
- **(b) Trên năm mức đo.** $\mathcal X=\{1,\ldots,5\}$ và lớp sáu hàm ngưỡng $\{h_t:t=1,\ldots,6\}$ của Ví dụ 01.1.

**Bảo đảm.** Chiều VC của cả hai lớp bằng $1$; khẳng định tất định về lớp, không có phân bố hay tập huấn luyện ngẫu nhiên.
:::

::: proof Chứng minh Mệnh đề 03.5
**Lộ trình.** Cận dưới bằng một điểm bị tách trọn; cận trên bằng một cách gán nhãn không thực hiện được trên mọi cặp điểm. Tính chất then chốt là $h_t(x)$ không giảm theo $x$.

**Bước 1 (cận dưới).** Trường hợp (a): $\{0\}$ bị tách trọn. Trường hợp (b): $h_1(1)=1$ và $h_2(1)=0$, nên $\{1\}$ bị tách trọn. Do đó $d\ge1$.

**Bước 2 (cận trên).** Lấy hai điểm bất kì $x_1<x_2$ của $\mathcal X$. Cách gán nhãn $(1,0)$ đòi $x_1\ge t$ và $x_2<t$, tức $x_2<t\le x_1$, mâu thuẫn với $x_1<x_2$. Lập luận này đúng cho mọi $t\in\mathbb R$, nên đúng cho cả hai lớp. Không tập hai phần tử nào bị tách trọn, nên $d\le1$.

$\square$ Lớp $\mathcal H_{\mathrm{thr}}$ vô hạn nhưng có chiều VC bằng $1$; chiều VC đo khả năng gán nhãn tự do của lớp, không đo số phần tử.
:::

::: proposition Mệnh đề 03.6 (Chiều VC của lớp khoảng đóng) — chứng minh đầy đủ
**Giả thiết.** $\mathcal X=\mathbb R$ và lớp khoảng đóng (closed interval)
$$
\begin{aligned}
h_{u,v}(x)&=\mathbb 1[u\le x\le v],\\
\mathcal H_{\mathrm{int}}&=\{h_{u,v}:\ u\le v\}.
\end{aligned}
$$

**Bảo đảm.** $\operatorname{VCdim}(\mathcal H_{\mathrm{int}})=2$; khẳng định tất định về lớp.
:::

::: proof Chứng minh Mệnh đề 03.6
**Lộ trình.** Cận dưới bằng bốn khoảng tường minh trên hai điểm; cận trên bằng một cách gán nhãn không thực hiện được trên mọi bộ ba điểm. Tính chất then chốt là tập $\{x:h(x)=1\}$ là một khoảng.

**Bước 1 (cận dưới).** Lấy $C=\{0,1\}$. Bốn cách gán nhãn của $(0,1)$ được thực hiện như sau.

- $(1,1)$ bởi khoảng $[0,1]$.
- $(1,0)$ bởi khoảng $[0,0]$.
- $(0,1)$ bởi khoảng $[1,1]$.
- $(0,0)$ bởi khoảng $[2,2]$.

Do đó $d\ge2$. Hàm hằng $0$ không thuộc $\mathcal H_{\mathrm{int}}$; khoảng một điểm $[2,2]$ nằm ngoài $C$ thay cho nó.

**Bước 2 (cận trên).** Lấy ba điểm bất kì $x_1<x_2<x_3$ và cách gán nhãn $(1,0,1)$. Nếu $h_{u,v}$ thực hiện nó thì $u\le x_1$ và $x_3\le v$, nên $u\le x_2\le v$ và $h_{u,v}(x_2)=1$, mâu thuẫn. Không tập ba phần tử nào bị tách trọn, nên $d\le2$.

$\square$ Hai lớp $\mathcal H_{\mathrm{thr}}$ và $\mathcal H_{\mathrm{int}}$ có cùng lực lượng (cardinality) với $\mathbb R$ nhưng chiều VC khác nhau.
:::

Cả hai chứng minh cận trên dùng thứ tự của các điểm trên đường thẳng.

## 5. Nửa không gian và hàm phân lớp tuyến tính

Trong $\mathbb R^p$ không có thứ tự như vậy, nên cận trên cho lớp *nửa không gian* (halfspace) cần một công cụ hình học: định lý Radon (Radon's theorem).

::: definition Định nghĩa 03.7 (Nửa không gian afin và nửa không gian thuần nhất)
Cho $p\ge1$ và $\mathcal X=\mathbb R^p$. Với $w\in\mathbb R^p$ và $b\in\mathbb R$, đặt
$$
h_{w,b}(x)=\mathbb 1[\langle w,x\rangle+b\ge0].
$$
Hai lớp được xét là:

- **Nửa không gian afin.** $\mathcal H^p_{\mathrm{aff}}=\{h_{w,b}:\ w\in\mathbb R^p,\ b\in\mathbb R\}$, lớp *nửa không gian afin* (affine halfspace), còn gọi là lớp hàm phân lớp tuyến tính afin; mỗi $h_{w,b}$ là một hàm phân lớp tuyến tính.
- **Nửa không gian thuần nhất.** $\mathcal H^p_{\mathrm{hom}}=\{h_{w,0}:\ w\in\mathbb R^p\}$, lớp *nửa không gian thuần nhất* (homogeneous halfspaces), không có hệ số tự do.
:::

Các điểm trên *siêu phẳng* (hyperplane) $\{x:\langle w,x\rangle+b=0\}$ nhận nhãn $1$. Với $w=0$, $h_{0,b}$ là hàm hằng: hằng $1$ khi $b\ge0$, hằng $0$ khi $b<0$.

Với $p=1$, lớp $\mathcal H^1_{\mathrm{aff}}$ gồm các hàm $\mathbb 1[x\ge t]$ (khi $w>0$), $\mathbb 1[x\le t]$ (khi $w<0$) và hai hàm hằng.

Trong mặt phẳng, hai đường chéo của hình vuông đơn vị cắt nhau tại tâm $(\tfrac12,\tfrac12)$, nên bốn đỉnh chia thành hai cặp có bao lồi giao nhau. Bổ đề dưới đây khẳng định điều này cho mọi $p+2$ điểm của $\mathbb R^p$.

::: lemma Bổ đề 03.8 (Phân hoạch Radon)
**Giả thiết.** $p\ge1$ và $p+2$ điểm $x_1,\ldots,x_{p+2}\in\mathbb R^p$.

**Bảo đảm.** Có hai tập chỉ số khác rỗng, rời nhau $I$, $J$ với $I\cup J=\{1,\ldots,p+2\}$, và một điểm
$$
\begin{aligned}
z\in{}&\operatorname{conv}\{x_i:i\in I\}\\
&\cap\operatorname{conv}\{x_j:j\in J\}.
\end{aligned}
$$
Ta gọi $(I,J)$ là một *phân hoạch Radon* (Radon partition). Khẳng định tất định.
:::

Ý chứng minh: hệ $\sum_ia_ix_i=0$, $\sum_ia_i=0$ có $p+1$ phương trình và $p+2$ ẩn $a_i$, nên có nghiệm khác $0$; các chỉ số có $a_i>0$ và các chỉ số còn lại cho $I$ và $J$.

::: proposition Mệnh đề 03.9 (Chiều VC của lớp nửa không gian)
**Giả thiết.** $p\ge1$; hai lớp $\mathcal H^p_{\mathrm{aff}}$ và $\mathcal H^p_{\mathrm{hom}}$ của Định nghĩa 03.7.

**Bảo đảm.** Hai khẳng định tất định về lớp, phụ thuộc số chiều đặc trưng $p$.

- **(a) Nửa không gian afin.** $\operatorname{VCdim}(\mathcal H^p_{\mathrm{aff}})=p+1$.
- **(b) Nửa không gian thuần nhất.** $\operatorname{VCdim}(\mathcal H^p_{\mathrm{hom}})=p$.
:::

::: proof Chứng minh Mệnh đề 03.9
**Lộ trình.** Gọi $\mathbf e_1,\ldots,\mathbf e_p$ là các véc-tơ đơn vị của $\mathbb R^p$ (in đứng để khác số $e$). Cận dưới bằng nghiệm tường minh trên $0,\mathbf e_1,\ldots,\mathbf e_p$, các đỉnh của một *đơn hình* (simplex), tức bao lồi của $p+1$ điểm độc lập afin; cận trên của (a) bằng Bổ đề 03.8.

**Bước 1 ((a), cận dưới).** Lấy $C=\{0,\mathbf e_1,\ldots,\mathbf e_p\}$, gồm $p+1$ điểm, và một cách gán nhãn $(y_0,y_1,\ldots,y_p)$ bất kì. Đặt
$$
\begin{aligned}
b&=2y_0-1,\\
w_i&=2y_i-1-b,
\end{aligned}
$$
với $i=1,\ldots,p$. Khi đó $\langle w,0\rangle+b=2y_0-1$ và $\langle w,\mathbf e_i\rangle+b=w_i+b=2y_i-1$. Số $2y-1$ bằng $1$ khi $y=1$ và bằng $-1$ khi $y=0$, nên $h_{w,b}$ thực hiện đúng cách gán nhãn đã cho. Do đó $d\ge p+1$. Cùng lập luận đúng cho mọi $p+1$ điểm độc lập afin, vì ma trận có các hàng $(x_i^\top,1)$ khả nghịch.

**Bước 2 ((a), cận trên).** Lấy $p+2$ điểm phân biệt $x_1,\ldots,x_{p+2}$ và một phân hoạch Radon $(I,J)$ với điểm $z$ theo Bổ đề 03.8. Xét cách gán nhãn $1$ trên $I$ và $0$ trên $J$. Giả sử $h_{w,b}$ thực hiện nó, và đặt $g(x)=\langle w,x\rangle+b$. Khi đó $g(x_i)\ge0$ với $i\in I$ và $g(x_j)<0$ với $j\in J$.

Viết $z=\sum_{i\in I}\lambda_ix_i=\sum_{j\in J}\mu_jx_j$ với các hệ số không âm, mỗi họ có tổng $1$. Vì $g$ afin, ta có
$$
\begin{aligned}
g(z)&=\textstyle\sum_{i\in I}\lambda_ig(x_i)\ge0,\\
g(z)&=\textstyle\sum_{j\in J}\mu_jg(x_j)<0,
\end{aligned}
$$
mâu thuẫn. Bất đẳng thức nghiêm ngặt ở dòng thứ hai dùng quy ước $\ge0$ của Định nghĩa 03.7: phía nghiêm ngặt $g<0$ nằm trên $J$, và $J\ne\varnothing$, nên một tổ hợp lồi của các số âm là số âm. Không tập $p+2$ điểm nào bị tách trọn, nên $d\le p+1$.

**Bước 3 ((b), cận dưới).** Với $C=\{\mathbf e_1,\ldots,\mathbf e_p\}$ và cách gán nhãn $(y_1,\ldots,y_p)$, lấy $w=\sum_i(2y_i-1)\mathbf e_i$. Khi đó $\langle w,\mathbf e_i\rangle=2y_i-1$, nên $h_{w,0}$ thực hiện cách gán nhãn đó, và $d\ge p$.

**Bước 4 ((b), cận trên).** Cận trên $d\le p$ được chứng minh ở Phụ lục A bằng phụ thuộc tuyến tính của $p+1$ véc-tơ trong $\mathbb R^p$.

$\square$ Lớp của ứng dụng ở §3 là $\mathcal H^{10}_{\mathrm{aff}}$, nên có chiều VC $d=11$; nếu chỉ dùng hai chỉ số đo, lớp $\mathcal H^2_{\mathrm{aff}}$ có $d=3$.
:::

::: example Ví dụ 03.3 (Nửa không gian trong mặt phẳng trên ba và bốn điểm)
**Thiết lập.** $p=2$ và lớp $\mathcal H^2_{\mathrm{aff}}$ của các nửa mặt phẳng, có $d=3$ theo Mệnh đề 03.9(a).

**Bước 1: ba điểm không thẳng hàng.** Lấy $(0,0)$, $(1,0)$, $(0,1)$, các đỉnh của đơn hình. Công thức $b=2y_0-1$, $w_i=2y_i-1-b$ cho cả tám cách gán nhãn. Chẳng hạn, với cách gán nhãn $(1,0,1)$, ta được $b=1$, $w=(-2,0)$, và $\langle w,x\rangle+b$ bằng $1$, $-1$, $1$ tại ba điểm. Với cách gán nhãn $(0,1,1)$, công thức cho đúng lời giải $b=-1$, $w=(2,2)$ của câu ôn nhanh 2.

**Bước 2: ba điểm thẳng hàng.** Lấy $(0,0)$, $(1,0)$, $(2,0)$. Trên đường thẳng chứa ba điểm, mỗi $h_{w,b}$ là một nửa đường thẳng hoặc một hàm hằng, nên cách gán nhãn $(1,0,1)$ không thực hiện được. Tập này không bị tách trọn, dù $d=3$: theo Nhận xét 03.4, một tập không bị tách trọn không cho cận trên.

**Bước 3: bốn đỉnh hình vuông.** Lấy $(0,0)$, $(1,0)$, $(1,1)$, $(0,1)$. Cách gán nhãn "chéo" ($1$ tại $(0,0)$ và $(1,1)$, $0$ tại hai đỉnh kia) không thực hiện được, theo Bước 2 của chứng minh Mệnh đề 03.9 với phân hoạch Radon gồm hai đường chéo và $z=(\tfrac12,\tfrac12)$. Đổi vai $I$ và $J$, cách gán nhãn bù cũng không thực hiện được. Mười bốn cách còn lại thực hiện được: hai hàm hằng, bốn cách tách riêng một đỉnh, bốn cách tách hai đỉnh kề nhau bằng một đường song song với một cạnh, và bốn phần bù của cách tách một đỉnh.

**Bước 4: một điểm trong tam giác.** Với $(0,0)$, $(3,0)$, $(0,3)$ và điểm $(1,1)=\tfrac13(0,0)+\tfrac13(3,0)+\tfrac13(0,3)$, cách gán nhãn $1$ tại ba đỉnh và $0$ tại $(1,1)$ không thực hiện được, theo Bước 2 của chứng minh Mệnh đề 03.9 với $J=\{(1,1)\}$.

Tóm lại, mỗi cấu hình bốn điểm thiếu ít nhất một cách gán nhãn, khớp với $d=3$; lý do chung là Bổ đề 03.8.
:::

Câu hỏi mở đầu khẳng định số tham số không thay được $\ln\lvert\mathcal H\rvert$. Với nửa không gian afin, hai số trùng nhau; điều đó không đúng nói chung.

::: remark Nhận xét 03.10 (Số tham số và chiều VC)
Số tham số và chiều VC của ba lớp như sau.

- **(i) Nửa không gian afin.** $\mathcal H^p_{\mathrm{aff}}$ có $p+1$ tham số $(w,b)$ và $d=p+1$ (Mệnh đề 03.9).
- **(ii) Một tham số, chiều VC vô hạn.** Lớp $\mathcal H_{\sin}=\{x\mapsto\mathbb 1[\sin(\theta x)>0]:\ \theta\in\mathbb R\}$ có một tham số, nhưng với mọi $k$, tập $\{2^{-1},2^{-2},\ldots,2^{-k}\}$ bị tách trọn, nên $d=\infty$.
- **(iii) Nhiều tham số, chiều VC bằng $1$.** Trên $\mathbb R$, lớp $\{x\mapsto\mathbb 1[(w_1+\cdots+w_p)x\ge0]:\ w\in\mathbb R^p\}$ có $p$ tham số nhưng chỉ gồm ba hàm $\mathbb 1[x\ge0]$, $\mathbb 1[x\le0]$ và hằng $1$, theo dấu của $w_1+\cdots+w_p$; đây là $\mathcal H^1_{\mathrm{hom}}$, viết với $p$ tham số thay cho một. Theo Mệnh đề 03.9(b), $d=1$.

Số tham số không cho cận trên, cũng không cho cận dưới, của chiều VC.
:::

Chiều VC là số điểm lớn nhất của một tập bị lớp tách trọn; nó chưa cho biết lớp tạo ra bao nhiêu cách gán nhãn trên $m>d$ điểm.

## 6. Hàm tăng trưởng và bổ đề Sauer–Shelah

Định lý 02.14 cộng $K$ biến cố hỏng. Với lớp vô hạn, đại lượng thay cho $K$ là số cách gán nhãn mà lớp tạo ra trên các điểm, lấy trong trường hợp xấu nhất.

::: definition Định nghĩa 03.11 (Hàm tăng trưởng)
Cho lớp $\mathcal H$ các hàm $\mathcal X\to\{0,1\}$ và số nguyên $m\ge1$. *Hàm tăng trưởng* (growth function) của $\mathcal H$ là
$$
\Pi_{\mathcal H}(m)=\max_{C}\,\lvert\mathcal H_C\rvert ,
$$
trong đó giá trị lớn nhất lấy trên mọi bộ $C=(x_1,\ldots,x_m)\in\mathcal X^m$.
:::

Đối số của $\Pi_{\mathcal H}$ là số điểm: cỡ mẫu $m$ khi áp dụng cho $(X_1,\ldots,X_m)$, và $2m$ khi áp dụng cho hai mẫu gộp lại.

Giá trị lớn nhất lấy trên mọi bộ điểm, nên $\Pi_{\mathcal H}(m)$ là một số tất định. Trên mọi tập huấn luyện, $\lvert\mathcal H_{(X_1,\ldots,X_m)}\rvert\le\Pi_{\mathcal H}(m)$; số bên trái là ngẫu nhiên.

Bộ điểm được phép có điểm lặp. Nhờ vậy $\Pi_{\mathcal H}(m)$ xác định cả khi $\mathcal X$ có ít hơn $m$ điểm, và không giảm theo $m$: thêm vào bộ một điểm lặp không làm giảm số cách gán nhãn. Ta cũng có $\Pi_{\mathcal H}(m)\le\min\{2^m,\lvert\mathcal H\rvert\}$.

Với chiều VC $d$, ta có $\Pi_{\mathcal H}(m)=2^m$ khi và chỉ khi $m\le d$. Nếu $m\le d$, lấy $m$ điểm của một tập bị tách trọn có ít nhất $m$ phần tử; theo tính chất tập con, chúng bị tách trọn. Ngược lại, một bộ có điểm lặp cho nhiều nhất $2^{m-1}$ cách gán nhãn, và một bộ $m$ điểm phân biệt có đủ $2^m$ cách gán nhãn là một tập bị tách trọn, nên $m\le d$.

::: example Ví dụ 03.4 (Hàm tăng trưởng của lớp hàm ngưỡng và lớp khoảng)
**Thiết lập.** Hai lớp $\mathcal H_{\mathrm{thr}}$ (Ví dụ 03.1) và $\mathcal H_{\mathrm{int}}$ (Mệnh đề 03.6) trên $\mathbb R$; một bộ $m\ge1$ điểm.

**Bước 1: hàm ngưỡng trên điểm phân biệt.** Với $x_1<\cdots<x_m$, cách gán nhãn của $h_t$ là một dãy số $0$ rồi một dãy số $1$. Nó xác định bởi số nhãn $1$, từ $0$ đến $m$, và mỗi số đó thực hiện được bằng một ngưỡng $t\le x_1$, $t>x_m$ hoặc $t\in(x_{i-1},x_i]$. Do đó có đúng $m+1$ cách.

**Bước 2: bộ có điểm lặp.** Các điểm trùng nhau nhận cùng nhãn, nên cách gán nhãn của bộ xác định bởi cách gán nhãn trên $k<m$ điểm phân biệt của nó, và có nhiều nhất $k+1\le m$ cách.

**Bước 3: kết luận cho hàm ngưỡng.** Từ hai bước trên,
$$
\Pi_{\mathcal H_{\mathrm{thr}}}(m)=m+1 .
$$

**Bước 4: lớp khoảng trên điểm phân biệt.** Với $x_1<\cdots<x_m$, cách gán nhãn của $h_{u,v}$ hoặc toàn $0$, hoặc là một khối liền các nhãn $1$ từ chỉ số $i$ đến chỉ số $i'\ge i$. Mỗi khối như vậy thực hiện được bởi khoảng $[x_i,x_{i'}]$, và cách toàn $0$ bởi một khoảng một điểm nằm ngoài bộ.

**Bước 5: đếm cho lớp khoảng.** Số cặp $i\le i'$ là $\binom m2+m=\binom{m+1}2$; thêm cách toàn $0$. Bộ có điểm lặp cho ít cách hơn như ở Bước 2, nên
$$
\Pi_{\mathcal H_{\mathrm{int}}}(m)=\binom{m+1}2+1 .
$$

**Bước 6: số cụ thể.** Tại $m=5$, hai hàm tăng trưởng bằng $6$ và $\binom62+1=16$, so với $2^5=32$; số $16$ là tổng $\sum_{j=0}^{2}\binom5j$.

Tóm lại, hai hàm tăng trưởng là đa thức bậc $1$ và bậc $2$ của $m$; bậc trùng với chiều VC.
:::

Với mọi lớp có chiều VC $d$ hữu hạn, hàm tăng trưởng bị chặn bởi một đa thức bậc $d$.

::: lemma Bổ đề 03.12 (Bổ đề Sauer–Shelah) — phác thảo cho (a), chứng minh đầy đủ cho (b)
**Giả thiết.** $\mathcal H$ khác rỗng, gồm các hàm $\mathcal X\to\{0,1\}$, có chiều VC $d<\infty$; $m\ge1$.

**Bảo đảm.** Hai bất đẳng thức tất định, tổ hợp.

- **(a) Tổng nhị thức.** $\Pi_{\mathcal H}(m)\le\sum_{j=0}^{d}\binom mj$, với quy ước $\binom mj=0$ khi $j>m$.
- **(b) Dạng đóng.** Nếu $1\le d\le m$ thì $\sum_{j=0}^{d}\binom mj\le\big(em/d\big)^d$.
:::

::: proof Chứng minh Bổ đề 03.12 (phác thảo cho (a), đầy đủ cho (b))
**Lộ trình của (a).** Quy nạp kép (double induction) theo $(m,d)$, tách các cách gán nhãn theo nhãn của điểm cuối, rồi dùng công thức Pascal; các trường hợp gốc và điểm lặp được xử lí ở Phụ lục B.

**Bước 1 (đẳng thức đếm).** Cố định bộ $C=(x_1,\ldots,x_m)$, đặt $C'=(x_1,\ldots,x_{m-1})$, và gọi $Y_1$ là tập các cách gán nhãn của $C'$ mở rộng được theo cả hai nhãn của $x_m$. Mỗi cách gán nhãn của $C'$ mở rộng được thành một hoặc hai cách gán nhãn của $C$, nên
$$
\lvert\mathcal H_C\rvert=\lvert\mathcal H_{C'}\rvert+\lvert Y_1\rvert .
$$

**Bước 2 (quy nạp và công thức Pascal).** Nếu $Y_1$ tách trọn một tập $B$ các điểm của $C'$ thì $\mathcal H$ tách trọn $B\cup\{x_m\}$, nên $Y_1$ có chiều VC không quá $d-1$. Giả thiết quy nạp, phát biểu cho mọi tập cách gán nhãn của $m-1$ vị trí, cho $\lvert\mathcal H_{C'}\rvert\le\sum_{j\le d}\binom{m-1}j$ và $\lvert Y_1\rvert\le\sum_{j\le d-1}\binom{m-1}j$. Công thức Pascal cộng hai tổng thành $\sum_{j=0}^{d}\binom mj$; lấy giá trị lớn nhất trên các bộ $C$ được (a).

**Bước 3 ((b), đầy đủ).** Vì $1\le d\le m$, ta có $m/d\ge1$. Do đó
$$
\begin{aligned}
&\sum_{j=0}^{d}\binom mj\\
&\quad\le\sum_{j=0}^{d}\binom mj(m/d)^{d-j}\\
&\quad=(m/d)^d\sum_{j=0}^{d}\binom mj(d/m)^j\\
&\quad\le(m/d)^d\sum_{j=0}^{m}\binom mj(d/m)^j\\
&\quad=(m/d)^d(1+d/m)^m\\
&\quad\le(m/d)^de^d .
\end{aligned}
$$
Bất đẳng thức thứ nhất dùng $(m/d)^{d-j}\ge1$ với $j\le d$. Bất đẳng thức thứ hai thêm các số hạng không âm với $d<j\le m$; giả thiết $d\le m$ được dùng ở đây. Đẳng thức tiếp theo là khai triển nhị thức. Bất đẳng thức cuối là $1+x\le e^x$ với $x=d/m$, nâng lên lũy thừa $m$.

Khi $m<d$, tổng trong (a) bằng $2^m$, và dạng đóng có thể sai: với $m=1$, $d=3$, ta có $(e/3)^3\approx0{,}744<2$.

$\square$ Khi $1\le d\le m$, ta có $\ln\Pi_{\mathcal H}(m)\le d\ln(em/d)$, không vượt quá cỡ $d\ln m$, trong khi $\ln2^m=m\ln2$ tăng tuyến tính theo $m$.
:::

::: example Ví dụ 03.5 (Ba cách đếm cách gán nhãn)
**Thiết lập.** Ba lớp $\mathcal H_{\mathrm{thr}}$ ($d=1$), $\mathcal H_{\mathrm{int}}$ ($d=2$) và $\mathcal H^2_{\mathrm{aff}}$ ($d=3$). Cần so sánh hàm tăng trưởng với tổng trong Bổ đề 03.12(a), với dạng đóng của Bổ đề 03.12(b) và với $2^m$.

**Bước 1: $d=1$.** Tổng nhị thức là $\binom m0+\binom m1=1+m$, bằng $\Pi_{\mathcal H_{\mathrm{thr}}}(m)$ của Ví dụ 03.4.

**Bước 2: $d=2$.** Tổng nhị thức là
$$
\begin{aligned}
&1+m+\binom m2\\
&\quad=\binom{m+1}2+1,
\end{aligned}
$$
bằng $\Pi_{\mathcal H_{\mathrm{int}}}(m)$. Với cả hai lớp, Bổ đề 03.12(a) đạt dấu bằng.

**Bước 3: nửa mặt phẳng, $m\le3$.** Vì $d=3$, $\Pi_{\mathcal H^2_{\mathrm{aff}}}(m)=2^m$ khi $m\le3$.

**Bước 4: nửa mặt phẳng, $m=4$.** Với bốn điểm phân biệt, Bổ đề 03.8 cho một phân hoạch Radon $(I,J)$. Theo Bước 2 của chứng minh Mệnh đề 03.9, cả cách gán nhãn "$1$ trên $I$, $0$ trên $J$" lẫn cách gán nhãn bù đều không thực hiện được. Một bộ bốn điểm có điểm lặp cho nhiều nhất $2^3$ cách. Do đó $\Pi_{\mathcal H^2_{\mathrm{aff}}}(4)\le14$, và hình vuông của Ví dụ 03.3 đạt $14$.

**Bước 5: so với tổng nhị thức.** Tổng nhị thức với $d=3$ cho phép $15$, nên ở đây Bổ đề 03.12(a) không đạt dấu bằng.

**Bước 6: hai bảng.** Bảng thứ nhất ghi hàm tăng trưởng; với nửa mặt phẳng, các giá trị với $m\ge5$ không được tính ở đây.

| $m$ | $\mathcal H_{\mathrm{thr}}$ | $\mathcal H_{\mathrm{int}}$ | $\mathcal H^2_{\mathrm{aff}}$ |
|---|---|---|---|
| $1$ | $2$ | $2$ | $2$ |
| $2$ | $3$ | $4$ | $4$ |
| $3$ | $4$ | $7$ | $8$ |
| $4$ | $5$ | $11$ | $14$ |
| $5$ | $6$ | $16$ | — |
| $20$ | $21$ | $211$ | — |

Bảng thứ hai ghi ba cận trên cho một lớp có $d=3$: tổng nhị thức, dạng đóng và $2^m$. Cột dạng đóng để trống khi $m<3$, vì Bổ đề 03.12(b) cần $d\le m$.

| $m$ | tổng | $(em/3)^3$ | $2^m$ |
|---|---|---|---|
| $1$ | $2$ | — | $2$ |
| $2$ | $4$ | — | $4$ |
| $3$ | $8$ | $20{,}09$ | $8$ |
| $4$ | $15$ | $47{,}61$ | $16$ |
| $5$ | $26$ | $92{,}99$ | $32$ |

**Bước 7: đọc bảng.** Tại $m=20$, tổng nhị thức với $d=3$ bằng $1351$ và dạng đóng bằng $5951{,}27$, so với $2^{20}=1\,048\,576$ cách gán nhãn. Với $3\le m\le5$, dạng đóng $(em/3)^3$ còn lớn hơn $2^m$.

Tóm lại, dạng đóng lỏng hơn tổng nhị thức khi $m$ nhỏ, nhưng đủ để thấy lôgarit của số cách gán nhãn không vượt quá cỡ $d\ln m$.
:::

Nếu $d\ln(em/d)$ thay được cho $\ln K$ trong Định lý 02.14, độ lệch đều sẽ có cỡ $\sqrt{d\ln m/m}$.

## 7. Hội tụ đều trên lớp có chiều VC hữu hạn

Để biến ước lượng cuối §6 thành một bảo đảm, chúng ta cần biến cố "$S$ là $\epsilon$-đại diện" (Định nghĩa 02.13) có xác suất ít nhất $1-\delta$ với mọi phân bố khi $m$ đủ lớn. Định nghĩa sau gọi đó là một tính chất của lớp.

::: definition Định nghĩa 03.13 (Tính chất hội tụ đều của một lớp)
Cho $\mathcal X$, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và lớp $\mathcal H$ các hàm $\mathcal X\to\{0,1\}$. Với phân bố $D$ trên $\mathcal Z=\mathcal X\times\mathcal Y$, $m\ge1$ và $\epsilon>0$, gọi $E_m(D,\epsilon)$ là tập các mẫu $s\in\mathcal Z^m$ là $\epsilon$-đại diện đối với $(\mathcal H,\ell_{0\text{-}1},D)$ (Định nghĩa 02.13), tức
$$
\sup_{h\in\mathcal H}\lvert L_s(h)-L_D(h)\rvert\le\epsilon .
$$
Lớp $\mathcal H$ có *tính chất hội tụ đều* (uniform convergence property) nếu tồn tại hàm $M:(0,1)^2\to\mathbb N$ sao cho tập $E_m(D,\epsilon)$ đo được và
$$
\Pr_{S\sim D^m}\big[S\in E_m(D,\epsilon)\big]\ge1-\delta
$$
với mọi lựa chọn của ba thành phần sau.

- **Tham số.** $\epsilon,\delta\in(0,1)$.
- **Phân bố dữ liệu.** $D$ bất kì trên $\mathcal Z$.
- **Cỡ mẫu.** $m\ge M(\epsilon,\delta)$.

Với mỗi $(\epsilon,\delta)$, gọi $m^{UC}_{\mathcal H}(\epsilon,\delta)$ là số $m_0\in\mathbb N$ nhỏ nhất sao cho điều kiện trên đúng với mọi $D$ và mọi $m\ge m_0$, và $m^{UC}_{\mathcal H}(\epsilon,\delta)=\infty$ khi không có $m_0$ nào. Hàm $(\epsilon,\delta)\mapsto m^{UC}_{\mathcal H}(\epsilon,\delta)$ được gọi là *hàm cỡ mẫu hội tụ đều* (uniform convergence sample size).
:::

Thứ tự lượng từ giống Định nghĩa 01.18: $\exists M$ đứng trước $\forall D$, nên cỡ mẫu không phụ thuộc phân bố. Đây là tính chất của lớp; không có thuật toán nào trong định nghĩa.

Một lớp hữu hạn chọn trước khi lấy mẫu có tính chất hội tụ đều, với $m^{UC}_{\mathcal H}(\epsilon,\delta)\le\lceil\ln(2K/\delta)/(2\epsilon^2)\rceil$ theo Định lý 02.14(c). Ví dụ sau là một lớp không có tính chất này.

::: example Ví dụ 03.6 (Lớp mọi hàm phân lớp đo được trên $[0,1]$)
**Thiết lập.** $\mathcal X=[0,1]$ với σ-đại số Borel, lớp $\mathcal M_{[0,1]}$ của Ví dụ 01.8, hàm lỗi 0–1 và phân bố $D$ của Ví dụ 01.8: $X\sim U[0,1]$, $Y=1$ chắc chắn.

**Bước 1: chiều VC.** Lấy một tập hữu hạn $C\subseteq[0,1]$ và một cách gán nhãn bất kì của nó. Gọi $F_1\subseteq C$ là tập các điểm nhãn $1$. Hàm $\mathbb 1_{F_1}$ là hàm Borel, nên thuộc $\mathcal M_{[0,1]}$, và nó thực hiện cách gán nhãn đó. Mọi tập hữu hạn bị tách trọn, nên $d=\infty$.

**Bước 2: độ lệch đều.** Với mỗi tập huấn luyện, đặt $F=\{X_1,\ldots,X_m\}$. Theo Mệnh đề 01.15, hàm $\mathbb 1_F$ có $L_S(\mathbb 1_F)=0$ và $L_D(\mathbb 1_F)=1$. Do đó độ lệch đều bằng $1$ trên mọi mẫu.

**Bước 3: định nghĩa không thỏa.** Với $\epsilon<1$, tập $E_m(D,\epsilon)$ rỗng với mọi $m$. Tập rỗng đo được và có xác suất $0<1-\delta$, nên không hàm $M$ nào thỏa Định nghĩa 03.13.

Tóm lại, với lớp này, hội tụ đều hỏng với mọi cỡ mẫu. Mệnh đề 01.15(c) vẫn đúng: dưới $D$ này, hàm hằng $1$ là một nghiệm ERM có rủi ro $0$. Điều không còn đúng là bảo đảm đồng thời cho mọi giả thuyết của lớp.
:::

Với lớp có $d$ hữu hạn, Bổ đề 03.12 chặn số cách gán nhãn trên $m$ điểm. Để dùng nó thay cho $K$ trong chứng minh Định lý 02.14, chúng ta cần thêm hai điều: các đại lượng dạng $\sup_{h\in\mathcal H}$ phải đo được, và mỗi biến cố hỏng phải ứng với một giả thuyết cố định đối với mẫu.

Với lớp vô hạn, độ lệch đều $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$ là cận trên đúng của vô hạn biến ngẫu nhiên, nên có thể không đo được. Điều kiện (M) ở §2 đủ cho mọi lớp của bài.

Dưới (M), trên mọi mẫu, độ lệch đều trên $\mathcal H$ bằng độ lệch đều trên $\mathcal H_0$. Lý do: $L_S(h)$ chỉ dùng hữu hạn điểm, nên $L_S(h_k)=L_S(h)$ khi $k$ đủ lớn; và $L_D(h_k)\to L_D(h)$ theo định lý hội tụ bị chặn (bounded convergence theorem). Do đó độ lệch đều là cận trên đúng của một họ đếm được biến ngẫu nhiên, nên đo được, và tập $E_m(D,\epsilon)$ của Định nghĩa 03.13 đo được với mọi $D$. Không có một điều kiện như vậy, các xác suất dưới đây có thể không xác định.

::: remark Nhận xét 03.14 (Điều kiện (M) cho các lớp của bài)
Với lớp hàm ngưỡng, lấy $\mathcal H_0=\{h_t:t\in\mathbb Q\}$. Với $t$ bất kì, lấy dãy hữu tỉ $t_k\uparrow t$: khi $x\ge t$, $h_{t_k}(x)=1$; khi $x<t$, $h_{t_k}(x)=0$ với $k$ đủ lớn. Dãy $t_k\downarrow t$ với $t_k>t$ không dùng được, vì nó hội tụ về $\mathbb 1[x>t]$, sai tại $x=t$. Lớp khoảng và lớp nửa không gian afin cũng thỏa (M), với lớp con gồm các tham số hữu tỉ.

Lớp hữu hạn thỏa (M) với $\mathcal H_0=\mathcal H$.
:::

Trên một mẫu $S$, lớp chỉ tạo ra $\lvert\mathcal H_{(X_1,\ldots,X_m)}\rvert\le\Pi_{\mathcal H}(m)$ cách gán nhãn.

**Câu hỏi.** Có thể lấy bất đẳng thức hợp trên các cách gán nhãn của chính tập huấn luyện không? Không, vì hai lý do.

- **(i)** $L_D(h)$ không xác định bởi cách gán nhãn của $h$ trên $S$: hai hàm có cùng cách gán nhãn trên $S$ có thể có rủi ro kì vọng khác nhau. Vì vậy một cách gán nhãn không ứng với một biến cố hỏng duy nhất.
- **(ii)** Tập các cách gán nhãn phụ thuộc $S$, nên đó là một lớp chọn theo mẫu, đúng điều mà (T4) cấm.

Cách sửa là thay $L_D(h)$ bằng rủi ro thực nghiệm trên một mẫu thứ hai, độc lập, cũng cỡ $m$. Khi đó mọi đại lượng chỉ phụ thuộc $h$ qua cách gán nhãn của $h$ trên $2m$ điểm. Phép thay này cần lớp cố định đối với cả hai mẫu, nghĩa là giả thiết (T5).

::: theorem Định lý 03.15 (Hội tụ đều trên lớp có chiều VC hữu hạn) — phác thảo
**Giả thiết.** Bốn thành phần sau.

- **Tập huấn luyện.** $S\sim D^m$ theo (T1), $m\ge1$.
- **Hàm lỗi.** Hàm lỗi 0–1, $\mathcal Y=\{0,1\}$.
- **Lớp.** $\mathcal H$ thỏa (T5) và (M), có chiều VC $d$.
- **Tham số.** $\delta\in(0,1)$.

**Bảo đảm.** Đặt *bán kính VC*
$$
\rho_m=\sqrt{\frac{8\ln\big(4\Pi_{\mathcal H}(2m)/\delta\big)}m},
$$
phụ thuộc ngầm vào $\mathcal H$ và $\delta$. Xác suất lấy theo $S\sim D^m$.

- **(a) Dạng hàm tăng trưởng.** Với mọi $m\ge1$, với xác suất ít nhất $1-\delta$,
  $$
  \sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\le\rho_m .
  $$
- **(b) Dạng chiều VC.** Nếu $1\le d\le m$ thì
  $$
  \begin{aligned}
  &\rho_m\\
  &\le\sqrt{\tfrac8m(d\ln\tfrac{2em}d+\ln\tfrac4\delta)}\\
  &\le4\sqrt{\tfrac1m(d\ln\tfrac{em}d+\ln\tfrac2\delta)}.
  \end{aligned}
  $$
- **(c) Tính chất hội tụ đều.** Nếu $1\le d<\infty$ thì $\mathcal H$ có tính chất hội tụ đều, với
  $$
  \begin{aligned}
  m^{UC}_{\mathcal H}(\epsilon,\delta)\le\Big\lceil&\frac{16}{\epsilon^2}\Big(d\ln\frac{32}{\epsilon^2}\\
  &+\ln\frac4\delta\Big)\Big\rceil .
  \end{aligned}
  $$

Vì độ lệch đều không vượt quá $1$, các vế phải ở (a) và (b) có thể thay bằng $\min\{1,\cdot\}$. Đây là cận với xác suất cao cho độ lệch giữa đại lượng thực nghiệm và đại lượng tổng thể, đồng thời cho mọi $h\in\mathcal H$; nó không phụ thuộc $D$, khi $d\ge1$ giảm theo $m$ như $\sqrt{\ln m/m}$, và phụ thuộc $\delta$ qua $\ln(1/\delta)$.
:::

Khi $d=\infty$, $\Pi_{\mathcal H}(2m)=2^{2m}$, nên $\rho_m\ge\sqrt{16\ln2}\approx3{,}33$: phần (a) vẫn đúng nhưng không cho thông tin. Khi $d=0$, mọi hàm của lớp trùng nhau, $\Pi_{\mathcal H}=1$, và (a) cho $\sqrt{8\ln(4/\delta)/m}$.

::: proof Chứng minh Định lý 03.15 (lộ trình)
**Lộ trình.** Với $\epsilon>0$ thỏa $m\epsilon^2\ge2$, bất đẳng thức then chốt là
$$
\begin{aligned}
&\Pr\big[\sup_h\lvert L_D(h)-L_S(h)\rvert>\epsilon\big]\\
&\le2\Pr\big[\sup_h\lvert L_{S'}(h)-L_S(h)\rvert\\
&\qquad>\epsilon/2\big]\\
&\le4\,\Pi_{\mathcal H}(2m)\,e^{-m\epsilon^2/8}.
\end{aligned}
$$
Bất đẳng thức thứ nhất đến từ Bước 1, bất đẳng thức thứ hai từ Bước 2–4.

**Bước 1 (mẫu bóng).** Lấy mẫu bóng $S'=(Z'_1,\ldots,Z'_m)\sim D^m$ độc lập với $S$; nó chỉ dùng trong chứng minh. Giả sử có $h$, chọn theo $S$, với $\lvert L_S(h)-L_D(h)\rvert>\epsilon$. Khi biết $S$, theo Bổ đề 02.3 với $\operatorname{Var}\le\tfrac14$, $L_{S'}(h)$ nằm trong khoảng $\epsilon/2$ quanh $L_D(h)$ với xác suất ít nhất $1-1/(m\epsilon^2)\ge\tfrac12$; khi đó $\lvert L_{S'}(h)-L_S(h)\rvert>\epsilon/2$. Do đó biến cố có mẫu bóng có xác suất ít nhất một nửa xác suất biến cố ban đầu; đây là hệ số $2$. Chỗ dùng: (T1) cho tính độc lập của $S'$ với $S$, tính bị chặn của hàm lỗi cho cận phương sai, (M) để chọn $h$ đo được theo $S$.

**Bước 2 (đổi chỗ với dấu ngẫu nhiên).** Đổi chỗ (swapping) $Z_i\leftrightarrow Z'_i$ không đổi phân bố của $(S,S')$. Do đó họ $\big(L_{S'}(h)-L_S(h)\big)_{h\in\mathcal H}$ có cùng phân bố đồng thời với họ
$$
\frac1m\sum_{i=1}^m\sigma_i\big(\ell(h,Z'_i)-\ell(h,Z_i)\big),
$$
trong đó các *dấu ngẫu nhiên* (random signs) $\sigma_i$ độc lập, nhận $\pm1$ với xác suất $\tfrac12$, độc lập với $(S,S')$; chúng cũng chỉ dùng trong chứng minh. Chỗ dùng: (T1), các cặp $(Z_i,Z'_i)$ độc lập cùng phân bố.

**Bước 3 (cách gán nhãn trên mẫu gộp).** Khi biết $(S,S')$, tổng trên chỉ phụ thuộc $h$ qua cách gán nhãn của $h$ trên *mẫu gộp* (combined sample) $(X_1,\ldots,X_m,X'_1,\ldots,X'_m)$, một bộ $2m$ điểm có thể có điểm lặp. Theo Định nghĩa 03.11, có nhiều nhất $\Pi_{\mathcal H}(2m)$ cách gán nhãn như vậy. Chỗ dùng: (T5). Khác với lý do (ii) ở trên, nguồn ngẫu nhiên còn lại là $\sigma$, độc lập với các cách gán nhãn.

**Bước 4 (Hoeffding và bất đẳng thức hợp).** Với một cách gán nhãn cố định, các số hạng $\sigma_i(\cdot)$ độc lập, có kì vọng $0$ và nằm trong $[-1,1]$. Định lý 02.7 với miền dài $2$, như câu ôn nhanh 3, cho xác suất lệch ít nhất $\epsilon/2$ không quá $2e^{-m\epsilon^2/8}$. Áp dụng Bổ đề 02.12 cho nhiều nhất $\Pi_{\mathcal H}(2m)$ cách gán nhãn rồi lấy kì vọng theo $(S,S')$, ta được bất đẳng thức then chốt.

**Bước 5 (giải theo $\delta$ và bổ đề Sauer–Shelah).** Đặt vế phải bằng $\delta$, ta được $\epsilon=\rho_m$. Điều kiện của Bước 1 tự thỏa, vì $m\rho_m^2=8\ln(4\Pi_{\mathcal H}(2m)/\delta)\ge8\ln4\approx11{,}09>2$. Phần (b) là Bổ đề 03.12(b) tại $2m$ điểm, cùng hai bất đẳng thức $d\ln(2em/d)\le(1+\ln2)\,d\ln(em/d)$ và $\ln(4/\delta)\le2\ln(2/\delta)$. Phần (c) suy từ (b) bằng bất đẳng thức tiếp tuyến $\ln u\le u/u_0+\ln u_0-1$.

$\square$ Hằng số $8$ trong $\rho_m$ đến từ hai nguồn: độ lệch bị chia đôi ở Bước 1 và miền dài $2$ ở Bước 4; đó là giá của mẫu bóng.
:::

::: example Ví dụ 03.7 (Cận độ lệch đều cho $d=3$ và $d=11$)
**Thiết lập.** Lớp $\mathcal H^2_{\mathrm{aff}}$ ($d=3$, hai chỉ số đo) và lớp $\mathcal H^{10}_{\mathrm{aff}}$ của ứng dụng ở §3 ($d=11$), theo Mệnh đề 03.9; cả hai thỏa (M) theo Nhận xét 03.14. Hàm lỗi 0–1, $\delta=0{,}05$, $m\in\{10^3,10^4,10^5\}$. Cần tính hai vế phải của Định lý 03.15(b); gọi vế phải thứ nhất là dạng trực tiếp, vế phải thứ hai là dạng hằng số $4$.

**Bước 1: số hạng của $\delta$.** $\ln(4/\delta)=\ln80\approx4{,}3820$.

**Bước 2: một ô tính đầy đủ.** Với $d=3$ và $m=10^4$,
$$
\begin{aligned}
&\frac{2em}d=\frac{2e\cdot10^4}3\approx18\,122,\\
&3\ln18\,122\approx3\cdot9{,}8049\\
&\quad=29{,}415,\\
&\frac{8(29{,}415+4{,}382)}{10^4}\\
&\quad\approx0{,}027037,
\end{aligned}
$$
nên dạng trực tiếp cho $\sqrt{0{,}027037}\approx0{,}1644$.

**Bước 3: bảng.** Mỗi ô ghi dạng trực tiếp / dạng hằng số $4$ của Định lý 03.15(b).

| $d$ | $m=10^3$ | $m=10^4$ | $m=10^5$ |
|---|---|---|---|
| $3$ | $0{,}464$ / $0{,}621$ | $0{,}164$ / $0{,}223$ | $0{,}0571$ / $0{,}0779$ |
| $11$ | $0{,}762$ / $1{,}014$ | $0{,}280$ / $0{,}379$ | $0{,}0993$ / $0{,}136$ |

Ô $1{,}014$ lớn hơn $1$, nên sau khi cắt ở $1$ nó không cho thông tin.

**Bước 4: tốc độ theo $m$.** Nhân $m$ lên $10$ lần làm cận giảm từ $2{,}7$ đến $2{,}9$ lần, ít hơn $\sqrt{10}\approx3{,}16$, vì $\ln m$ tăng.

Tóm lại, với mười chỉ số đo, cận độ lệch đều là $0{,}762$ ở $10^3$ quan sát và $0{,}280$ ở $10^4$ quan sát; đây là cận trên của độ lệch đều, không phải giá trị của nó. Dạng hằng số $4$ lớn hơn dạng trực tiếp từ $1{,}33$ đến $1{,}37$ lần.
:::

Định lý 03.15 dùng (T5) ở Bước 3. Trong ví dụ sau, ta bỏ (T5) và giữ chiều VC nhỏ.

::: example Ví dụ 03.8 (Hai hàm chọn sau khi xem mẫu)
**Thiết lập.** Phân bố $D$ của Ví dụ 03.6 trên $[0,1]\times\{0,1\}$, hàm lỗi 0–1. Với mỗi mẫu $S$, đặt $F=\{X_1,\ldots,X_m\}$ và lớp
$$
\mathcal G_S=\{h_{\equiv0},\ \mathbb 1_F\},
$$
gồm hàm hằng $0$ và hàm chỉ báo của $F$. Lớp này được chọn sau khi xem mẫu.

**Bước 1: chiều VC.** $\mathcal G_S$ có hai hàm, nên chiều VC không quá $\log_22=1$. Hai hàm khác nhau tại $X_1$, nên $\{X_1\}$ bị tách trọn và chiều VC bằng $1$.

**Bước 2: độ lệch đều.** $L_S(\mathbb 1_F)=0$ và $L_D(\mathbb 1_F)=1$ (Mệnh đề 01.15), nên độ lệch đều trên $\mathcal G_S$ bằng $1$ với xác suất $1$.

**Bước 3: áp dụng sai Định lý 03.15.** Nếu bỏ qua (T5), phần (b) với $d=1$, $m=1000$, $\delta=0{,}05$, $\ln(2e\cdot1000)\approx8{,}601$ và $\ln80\approx4{,}382$ cho
$$
\begin{aligned}
\rho_m&\le\sqrt{\tfrac8{1000}(8{,}601+4{,}382)}\\
&\approx0{,}322,
\end{aligned}
$$
mâu thuẫn với độ lệch $1$ ở Bước 2.

**Bước 4: chỗ hỏng.** Bước 3 của chứng minh Định lý 03.15 cần các cách gán nhãn trên mẫu gộp thuộc một lớp cố định. Ở đây lớp phụ thuộc $S$, nên sau khi đổi chỗ $Z_i\leftrightarrow Z'_i$, lớp cũng đổi theo.

Tóm lại, chiều VC nhỏ không đủ; lớp phải cố định trước khi lấy mẫu.
:::

Bỏ tính độc lập của các quan sát, như khi chép lại một quan sát ở Ví dụ 02.6, làm hỏng Bước 1 và Bước 2 của chứng minh: Bước 1 cần các $Z'_i$ độc lập để dùng Bổ đề 02.3(b), Bước 2 cần các cặp $(Z_i,Z'_i)$ độc lập cùng phân bố.

## 8. ERM, định lý cơ bản và cận dưới

Định lý 03.15 chặn độ lệch đều trên một lớp vô hạn; thuật toán ERM cần một cận cho rủi ro vượt mức của nghiệm $\hat h$. Với lớp vô hạn, giá trị nhỏ nhất của $L_D$ trên $\mathcal H$ có thể không đạt, nên phép so sánh với phần tử tốt nhất trong lớp ở Hệ quả 02.16 phải viết lại cho mọi $h\in\mathcal H$.

::: corollary Hệ quả 03.16 (Rủi ro vượt mức của ERM trên lớp có chiều VC hữu hạn) — chứng minh đầy đủ
**Giả thiết.** Năm thành phần sau.

- **Tập huấn luyện.** $S\sim D^m$ theo (T1), $m\ge1$.
- **Hàm lỗi.** Hàm lỗi 0–1.
- **Lớp.** $\mathcal H$ thỏa (T5) và (M), có chiều VC $d$ với $1\le d<\infty$.
- **Thuật toán.** Theo (O1), một thuật toán ERM bất kì trên $\mathcal H$ thỏa điều kiện đo được của Định nghĩa 01.4, với mọi quy tắc chọn khi bằng nhau; hoặc theo (O2), một $\epsilon_{\mathrm{opt}}$-ERM $A$.
- **Tham số.** $\delta\in(0,1)$, với $\rho_m$ như ở Định lý 03.15.

**Bảo đảm.** Xác suất lấy theo $S\sim D^m$.

- **(a) ERM chính xác.** Với xác suất ít nhất $1-\delta$, đồng thời cho mọi nghiệm ERM $\hat h$ trên $S$,
  $$
  \begin{aligned}
  L_D(\hat h)&\le\inf_{h\in\mathcal H}L_D(h)\\
  &\quad+2\rho_m ;
  \end{aligned}
  $$
  khi $d\le m$, có thể thay $\rho_m$ bằng một trong hai vế phải của Định lý 03.15(b).
- **(b) ERM xấp xỉ.** Trên cùng biến cố, $L_D(A(S))\le\inf_{h\in\mathcal H}L_D(h)+2\rho_m+\epsilon_{\mathrm{opt}}$.
- **(c) Học PAC bất khả diễn.** Mọi thuật toán ERM như trên là thuật toán học PAC bất khả diễn (Định nghĩa 01.25) với
  $$
  \begin{aligned}
  M(\epsilon,\delta)=\Big\lceil&\frac{64}{\epsilon^2}\Big(d\ln\frac{128}{\epsilon^2}\\
  &+\ln\frac4\delta\Big)\Big\rceil ;
  \end{aligned}
  $$
  khi có ít nhất một thuật toán ERM như vậy, $\mathcal H$ học được PAC bất khả diễn và $m_{\mathcal H}(\epsilon,\delta)\le M(\epsilon,\delta)$.

Đây là bảo đảm với xác suất cao cho rủi ro vượt mức so với lớp, không phụ thuộc $D$.
:::

Trong phần (c), $\epsilon$ là cận cho rủi ro vượt mức; độ lệch đều tương ứng là $\epsilon/2$. Độ phức tạp mẫu $m_{\mathcal H}$ ở đây là bản mở rộng sang trường hợp bất khả diễn. Với hàm lỗi 0–1, nghiệm ERM tồn tại trên mọi mẫu, kể cả với lớp vô hạn (Nhận xét 01.11).

::: proof Chứng minh Hệ quả 03.16
**Lộ trình.** Một bước tất định trên biến cố $r$-đại diện, rồi Định lý 03.15.

**Bước 1 (bước tất định).** Giả sử $S$ là $r$-đại diện và $\hat h$ là một nghiệm ERM trên $S$. Với mọi $h\in\mathcal H$,
$$
\begin{aligned}
L_D(\hat h)&\le L_S(\hat h)+r\\
&\le L_S(h)+r\\
&\le L_D(h)+2r.
\end{aligned}
$$
Bất đẳng thức thứ nhất dùng tính đại diện tại $\hat h$, bất đẳng thức thứ hai dùng (O1), bất đẳng thức thứ ba dùng tính đại diện tại $h$. Dưới (O2), bất đẳng thức thứ hai thành $L_S(A(S))\le L_S(h)+\epsilon_{\mathrm{opt}}$, vì $\inf_{h'}L_S(h')\le L_S(h)$.

**Bước 2 (cận dưới đúng).** Vế trái không phụ thuộc $h$. Lấy cận dưới đúng theo $h\in\mathcal H$ ở vế phải, ta được $L_D(\hat h)\le\inf_{h\in\mathcal H}L_D(h)+2r$. Bước này không cần một phần tử tốt nhất $h_{\mathcal H}$ tồn tại, khác với Bước 1 của chứng minh Hệ quả 02.16.

**Bước 3 (phần a, b).** Bước 1–2 đúng cho mọi nghiệm ERM cùng lúc. Theo Định lý 03.15(a), biến cố "$S$ là $\rho_m$-đại diện" có xác suất ít nhất $1-\delta$; lấy $r=\rho_m$.

**Bước 4 (phần c).** Ta có $2\rho_m\le\epsilon$ khi và chỉ khi $\rho_m\le\epsilon/2$. Theo Định lý 03.15(c) với $\epsilon/2$ thay cho $\epsilon$, khi $m\ge M(\epsilon,\delta)$, biến cố "$S$ là $\epsilon/2$-đại diện" đo được và có xác suất ít nhất $1-\delta$, vì $16/(\epsilon/2)^2=64/\epsilon^2$ và $32/(\epsilon/2)^2=128/\epsilon^2$. Bước 1–2 với $r=\epsilon/2$ cho bất đẳng thức của Định nghĩa 01.25 với mọi $D$ và mọi $m\ge M(\epsilon,\delta)$.

$\square$ Hệ số $2$ đến từ hai phép so sánh, tại $\hat h$ và tại $h$; cận dưới đúng thay cho giá trị nhỏ nhất mà không làm thay đổi hằng số.
:::

::: example Ví dụ 03.9 (Cỡ mẫu cho rủi ro vượt mức $0{,}1$)
**Thiết lập.** $\epsilon=0{,}1$ là cận cho rủi ro vượt mức, $\delta=0{,}05$; bảo đảm cho mọi thuật toán ERM và mọi phân bố. Ba lớp: $d=1$ (lớp hàm ngưỡng của câu hỏi mở đầu), $d=3$ (nửa mặt phẳng, hai chỉ số đo), $d=11$ (mười chỉ số đo).

**Bước 1: điều kiện.** Theo Hệ quả 03.16(a) với dạng trực tiếp của Định lý 03.15(b), rủi ro vượt mức không quá $2\rho_m\le0{,}1$ khi $m\ge d$ và
$$
\tfrac{32}m\big(d\ln\tfrac{2em}d+4{,}382\big)\le0{,}01 .
$$
Vế trái giảm theo $m\ge d$: với $c=4{,}382$, đạo hàm của $\big(d\ln\tfrac{2em}d+c\big)/m$ bằng $\big(d-d\ln\tfrac{2em}d-c\big)/m^2<0$, vì $\ln\tfrac{2em}d\ge\ln(2e)>1$ khi $m\ge d$ và $c>0$. Do đó cỡ mẫu nhỏ nhất thỏa điều kiện cũng đủ cho mọi cỡ mẫu lớn hơn.

**Bước 2: giải số.** Chia đôi khoảng tìm cỡ mẫu nhỏ nhất, ta được
$$
\begin{aligned}
d=1:&\quad54\,330,\\
d=3:&\quad132\,992,\\
d=11:&\quad447\,194.
\end{aligned}
$$

**Bước 3: kiểm một ô.** Với $d=1$, vế trái bằng khoảng $0{,}0099999$ tại $m=54\,330$ và $0{,}0100001$ tại $m=54\,329$; cần bảy chữ số vì hai giá trị rất gần $0{,}01$.

**Bước 4: dạng đóng.** Dạng đóng $M(0{,}1;0{,}05)$ của Hệ quả 03.16(c) cho $88\,572$, $209\,624$, $693\,832$, lớn hơn các số ở Bước 2 từ $1{,}55$ đến $1{,}63$ lần.

**Bước 5: dạng hằng số $4$.** Thay dạng trực tiếp bằng dạng hằng số $4$ của Định lý 03.15(b), ta được $103\,939$, $261\,198$, $889\,572$.

Tóm lại, theo cận của bài, $54\,330$ quan sát là đủ cho câu hỏi mở đầu, và $447\,194$ quan sát là đủ cho câu hỏi thực hành với mười chỉ số đo. Chuyển từ hai lên mười chỉ số đo nhân cỡ mẫu khoảng $3{,}36$ lần, gần tỉ số $11/3\approx3{,}67$ của hai chiều VC. Mọi con số là cỡ mẫu đủ, không phải cỡ mẫu cần.
:::

Một tham số thực lưu trên máy tính chỉ nhận hữu hạn giá trị, nên có thể so cận VC với cận của lớp hữu hạn sau khi rời rạc hóa (discretization).

::: example Ví dụ 03.10 (So sánh với lớp hữu hạn sau khi rời rạc hóa)
**Thiết lập.** Mỗi tham số thực được lưu bằng $64$ bit, nên lớp đã rời rạc hóa với $q$ tham số có $K\le2^{64q}$ hàm. Hệ quả 02.16(c) cho cỡ mẫu $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$, với $\epsilon=0{,}1$ và $\delta=0{,}05$, tức $2K/\delta\le2^{64q+1}\cdot20$.

**Bước 1: một ngưỡng, $q=1$.** $\ln(2^{65}\cdot20)=65\ln2+\ln20\approx48{,}050$, nên cỡ mẫu là $\lceil200\cdot48{,}050\rceil=9611$, so với $54\,330$ của Ví dụ 03.9 ($d=1$).

**Bước 2: mười chỉ số đo, $q=11$.** $705\ln2+\ln20\approx491{,}664$, nên cỡ mẫu là $98\,333$, so với $447\,194$ ($d=11$).

**Bước 3: lớp hữu hạn sáu hàm ngưỡng.** Để tách riêng ảnh hưởng của hằng số, xét lớp sáu hàm của Ví dụ 03.2: nó hữu hạn ($K=6$) và có $\Pi_{\mathcal H}(2m)\le6$, nên cả bán kính VC lẫn bán kính $r_m$ của Định lý 02.14 áp dụng. Lấy $m=1000$ và $\delta=0{,}05$.

**Bước 4: hai bán kính.** Ta có
$$
\begin{aligned}
&4\cdot6/0{,}05=480,\\
&\rho_m\le\sqrt{8\ln480/1000}\\
&\quad\approx\sqrt{8\cdot6{,}174/1000}\\
&\quad\approx0{,}2222,\\
&2K/\delta=240,\\
&r_m=\sqrt{\ln240/2000}\\
&\quad\approx\sqrt{5{,}481/2000}\\
&\quad\approx0{,}0523.
\end{aligned}
$$

Tóm lại, với các hằng số của bài, cỡ mẫu theo cận VC lớn hơn cỡ mẫu của lớp đã rời rạc hóa từ $4{,}5$ đến $5{,}7$ lần (Bước 1–2), và bán kính VC lớn hơn $r_m$ khoảng $4{,}25$ lần (Bước 4), chủ yếu do hằng số $8$ của mẫu bóng. Đổi lại, cận VC áp dụng cho chính lớp vô hạn, không phụ thuộc cách lưu tham số và không có sai số xấp xỉ do lưới.
:::

Định lý 03.15 và Hệ quả 03.16 cho điều kiện đủ: dưới (M), chiều VC hữu hạn kéo theo học được. Định lý sau phát biểu điều kiện cần, và gom các khái niệm học của Bài 01–03 vào một danh sách tương đương. Định lý không có bữa trưa miễn phí được dẫn theo §5.1 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* của Shalev-Shwartz và Ben-David (2014), viết tắt UML.

::: theorem Định lý 03.17 (Định lý cơ bản của học PAC cho phân lớp nhị phân) — phác thảo (điều kiện cần: UML §5.1, §6.4)
**Giả thiết.** Bốn thành phần sau.

- **Bài toán.** $\mathcal X$ có σ-đại số, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1.
- **Tập huấn luyện.** $S\sim D^m$ theo (T1).
- **Lớp.** $\mathcal H$ khác rỗng, có chiều VC $d\in\{0,1,2,\ldots\}\cup\{\infty\}$.
- **Thuật toán.** Thuật toán học theo Định nghĩa 01.4; ở phần (b), có ít nhất một thuật toán ERM trên $\mathcal H$ thỏa Định nghĩa 01.4.

**Bảo đảm.** Hai khẳng định về lớp.

- **(a) Điều kiện cần, không dùng (M).** Nếu $\mathcal H$ tách trọn một tập có $2m$ phần tử thì với mọi thuật toán học $A$ có một phân bố $D$, khả diễn đối với $\mathcal H$ và tập trung trên tập đó, sao cho
  $$
  \begin{aligned}
  &\Pr_{S\sim D^m}\big[L_D(A(S))>1/8\big]\\
  &\quad\ge1/7 .
  \end{aligned}
  $$
  Do đó nếu $d=\infty$ thì $\mathcal H$ không học được PAC, và theo Nhận xét 01.26 cũng không học được PAC bất khả diễn.
- **(b) Sáu khẳng định tương đương, dưới (M).**
  1. $\mathcal H$ có tính chất hội tụ đều.
  2. Mọi thuật toán ERM trên $\mathcal H$ là thuật toán học PAC bất khả diễn.
  3. $\mathcal H$ học được PAC bất khả diễn.
  4. $\mathcal H$ học được PAC.
  5. Mọi thuật toán ERM trên $\mathcal H$ là thuật toán học PAC.
  6. $d<\infty$.

Ở (a), lượng từ là "với mọi thuật toán, tồn tại phân bố"; ở (3), (4) của (b), lượng từ là "tồn tại thuật toán".
:::

Khi $d=\infty$, phần (a) cho kết luận như sau: lấy $\epsilon<1/8$ và $\delta<1/7$; với mọi $m$, lớp tách trọn một tập $2m$ phần tử, nên thuật toán thất bại với xác suất ít nhất $1/7>\delta$.

UML §6.4 phát biểu định lý này. Các phép kéo theo của (b) đến từ các kết quả sau.

- **(6)⇒(1).** Định lý 03.15(c) khi $d\ge1$; Định lý 03.15(a) với $\Pi_{\mathcal H}=1$ khi $d=0$.
- **(1)⇒(2).** Bước tất định của Hệ quả 03.16 với $r=\epsilon/2$ và $M(\epsilon,\delta)=m^{UC}_{\mathcal H}(\epsilon/2,\delta)$.
- **(2)⇒(3) và (5)⇒(4).** Theo định nghĩa, vì có một thuật toán ERM.
- **(2)⇒(5) và (3)⇒(4).** Nhận xét 01.26.
- **(4)⇒(6).** Phần (a), dựa trên định lý không có bữa trưa miễn phí (Nhận xét 01.30; UML §5.1).

::: corollary Hệ quả 03.18 (Lớp mọi hàm phân lớp đo được trên $[0,1]$ không học được PAC) — chứng minh đầy đủ (dựa trên Định lý 03.17(a))
**Giả thiết.** $\mathcal X=[0,1]$ với σ-đại số Borel, $\mathcal H=\mathcal M_{[0,1]}$, hàm lỗi 0–1.

**Bảo đảm.** Không thuật toán học nào (Định nghĩa 01.4) là thuật toán học PAC cho $\mathcal M_{[0,1]}$. Cụ thể, với mọi thuật toán $A$ và mọi $m$, có một phân bố khả diễn $D$ với $\Pr_{S\sim D^m}[L_D(A(S))>1/8]\ge1/7$.
:::

::: proof Chứng minh Hệ quả 03.18
**Lộ trình.** Định lý 03.17(a) được thừa nhận; chỉ cần kiểm giả thiết của nó.

**Bước 1.** Theo Bước 1 của Ví dụ 03.6, $\mathcal M_{[0,1]}$ tách trọn mọi tập hữu hạn, nên với mọi $m$ nó tách trọn một tập $2m$ phần tử.

**Bước 2.** Áp dụng Định lý 03.17(a) cho tập đó và cho $A$.

$\square$ Hệ quả 01.29(b) chỉ bác bỏ một thuật toán ERM dưới một phân bố. Ở đây mọi thuật toán đều thất bại dưới một phân bố chọn theo thuật toán; dưới phân bố cố định của Ví dụ 01.8, hàm hằng $1$ vẫn học được (Mệnh đề 01.15(c)).
:::

Để biết tốc độ $1/\epsilon^2$ có cần thiết hay không, ta cần một cận dưới định lượng, đúng cho mọi thuật toán.

::: theorem Định lý 03.19 (Cận dưới cho độ phức tạp mẫu) — đọc thêm
**Giả thiết.** Bài toán và mẫu như Định lý 03.17, tức hàm lỗi 0–1 và $S\sim D^m$ theo (T1); lớp $\mathcal H$ có chiều VC $d$.

**Bảo đảm.** Có các hằng số phổ quát $c>0$ và $\epsilon_0,\delta_0\in(0,1)$ sao cho với mọi $\epsilon\in(0,\epsilon_0)$, $\delta\in(0,\delta_0)$, mọi thuật toán học $A$ và mọi cỡ mẫu $m$:

- **(a) Bất khả diễn.** Nếu $1\le d<\infty$ và $m<c\,(d+\ln(1/\delta))/\epsilon^2$ thì có một phân bố $D$ trên $\mathcal X\times\{0,1\}$ với
  $$
  \begin{aligned}
  &\Pr_{S\sim D^m}\big[L_D(A(S))\\
  &\quad>\inf_{h}L_D(h)+\epsilon\big]>\delta .
  \end{aligned}
  $$
- **(b) Khả diễn.** Nếu $2\le d<\infty$ và $m<c\,(d+\ln(1/\delta))/\epsilon$ thì có một phân bố $D$ khả diễn đối với $\mathcal H$ với $\Pr_{S\sim D^m}[L_D(A(S))>\epsilon]>\delta$.

Lượng từ là "với mọi thuật toán, tồn tại phân bố", như Nhận xét 01.21 đòi cho một cận dưới.
:::

Theo (a), tốc độ $1/\epsilon^2$ trong trường hợp bất khả diễn là cần thiết. UML §6.4 phát biểu hai cận dưới này với hằng số tuyệt đối; UML §28.2 chứng minh phần (a); UML không chứng minh phần (b). Cận trên $M(\epsilon,\delta)$ của Hệ quả 03.16(c) lớn hơn cận dưới một thừa số cỡ $\ln(1/\epsilon)$; bỏ thừa số này cần kỹ thuật xích (chaining), ngoài phạm vi của học phần (UML §28.1).

## 9. Ý nghĩa, tác động và giới hạn

Dưới (M), một lớp vô hạn học được khi chiều VC của nó hữu hạn: đại lượng $\ln\lvert\mathcal H\rvert$ của Bài 02 được thay bằng $\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$. Định lý 03.15 là bảo đảm cho lớp; Hệ quả 03.16 là bảo đảm cho mọi thuật toán ERM trên lớp đó.

Chiều VC, không phải số tham số, xác định cỡ mẫu đủ (Nhận xét 03.10). Với nửa không gian afin trên $p$ đặc trưng, $d=p+1$, nên cỡ mẫu đủ tăng gần tuyến tính theo số đặc trưng (Ví dụ 03.9).

Các cận của bài là bảo thủ. Hằng số $8$ của mẫu bóng làm cỡ mẫu theo cận VC lớn hơn cỡ mẫu của lớp đã rời rạc hóa vài lần (Ví dụ 03.10). Phân tích VC kiểm soát cả lớp và mọi phân bố, nên có thể lỏng cho một thuật toán hay một phân bố cụ thể; Định lý 03.19 chỉ khẳng định cỡ mẫu ít nhất cỡ $(d+\ln(1/\delta))/\epsilon^2$ là cần trong trường hợp xấu nhất.

Các kết quả chỉ áp dụng cho phân lớp nhị phân với hàm lỗi 0–1. Phép đếm cách gán nhãn ở Bước 3 của chứng minh Định lý 03.15 cần hàm lỗi xác định bởi nhãn dự đoán trong $\{0,1\}$; hàm lỗi bình phương và hàm lỗi log còn có thể không bị chặn (Nhận xét 02.11). Phân lớp nhiều lớp (multiclass classification), chi phí tính toán của ERM và độ phức tạp Rademacher nằm ngoài bài.

Hai ví dụ cho thấy giả thiết nào không bỏ được. Bỏ (T5), cận của Định lý 03.15 sai dù $d=1$ (Ví dụ 03.8). Bỏ (T1), rủi ro thực nghiệm có thể không tập trung (Ví dụ 02.6). Khi $d=\infty$, phần (a) vẫn đúng nhưng không cho thông tin, và lớp ở Ví dụ 03.6 không có tính chất hội tụ đều.

Trong trường hợp khả diễn, Định lý 03.19(b) chỉ cho cận dưới cỡ $(d+\ln(1/\delta))/\epsilon$.

## 10. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 03](material-viewer.html?doc=materials/lec-03/exercises.md). Sáu bài đầu là bài gốc, sáu bài sau chọn từ UML; mỗi dòng ghi mục tiêu mà bài kiểm tra.

1. **Bài tập 03.1** (Hàm tăng trưởng của lớp hàm ngưỡng trên tập hữu hạn): mục tiêu 2.
2. **Bài tập 03.2** (Chiều VC của lớp khoảng bằng cận dưới và cận trên): mục tiêu 1.
3. **Bài tập 03.3** (Cận dưới cho nửa không gian afin qua điểm độc lập afin): mục tiêu 1.
4. **Bài tập 03.4** (So sánh cỡ mẫu theo chiều VC và nguồn gốc hằng số $8$): mục tiêu 3, 4.
5. **Bài tập 03.5** (Số tham số, lớp chọn sau khi xem mẫu và chiều VC): mục tiêu 5.
6. **Bài tập 03.6** (Một cách chứng minh khác của bổ đề Sauer–Shelah, tùy chọn): mục tiêu 2.
7. **Bài tập 03.7** (Chiều VC của hai lớp trên tập hữu hạn; UML Bài tập 6.2): mục tiêu 1.
8. **Bài tập 03.8** (Bốn trường hợp dấu bằng của bổ đề Sauer–Shelah; UML Bài tập 6.4): mục tiêu 2.
9. **Bài tập 03.9** (Hình chữ nhật song song với trục trong $\mathbb R^p$; UML Bài tập 6.5): mục tiêu 1.
10. **Bài tập 03.10** (Lớp hội Boole; UML Bài tập 6.6): mục tiêu 1.
11. **Bài tập 03.11** (Chiều VC vô hạn kéo theo không học được PAC; UML Bài tập 6.10): mục tiêu 5.
12. **Bài tập 03.12** (Hình cầu đóng trong $\mathbb R^p$; UML Bài tập 9.6): mục tiêu 1.

## 11. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Bốn điểm $(1,0)$, $(0,1)$, $(-1,0)$, $(0,-1)$ cùng mười sáu hình chữ nhật, mỗi hình thực hiện một cách gán nhãn, có chứng minh được lớp hình chữ nhật song song với trục $\mathcal H_{\mathrm{rec}}$ của Bài tập 02.7 có chiều VC bằng $4$ không? Nếu chưa, viết phần còn thiếu.

**Câu hỏi phụ.** Bốn đỉnh của hình vuông đơn vị không bị $\mathcal H_{\mathrm{rec}}$ tách trọn. Điều này có mâu thuẫn với kết luận $d=4$ không?

::: solution Lời giải câu hỏi cuối buổi
**Câu hỏi chính.** Chưa. Bốn điểm và mười sáu hình chữ nhật chỉ cho cận dưới $d\ge4$ (Nhận xét 03.4). Phần thiếu là cận trên: mọi tập năm điểm không bị tách trọn.

Lấy năm điểm phân biệt. Chọn một điểm có hoành độ nhỏ nhất, một điểm có hoành độ lớn nhất, một điểm có tung độ nhỏ nhất và một điểm có tung độ lớn nhất; có nhiều nhất bốn điểm được chọn, nên còn ít nhất một điểm $x$. Gán nhãn $1$ cho các điểm được chọn và nhãn $0$ cho mọi điểm còn lại, trong đó có $x$.

Gọi $a_1\le a_2$ là hoành độ nhỏ nhất và lớn nhất, $b_1\le b_2$ là tung độ nhỏ nhất và lớn nhất của năm điểm. Một hình chữ nhật $[u_1,v_1]\times[u_2,v_2]$ chứa các điểm được chọn thì $u_1\le a_1$, $a_2\le v_1$, $u_2\le b_1$ và $b_2\le v_2$, nên chứa cả $x$. Hàm $h_\varnothing\equiv0$ của Bài tập 02.7 gán nhãn $0$ cho các điểm được chọn, nên cũng không thực hiện được cách gán nhãn này. Vậy $d=4$.

**Câu hỏi phụ.** Không mâu thuẫn. Một tập bốn điểm không bị tách trọn không cho cận trên (Nhận xét 03.4). Với hình vuông, cách gán nhãn $1$ tại hai đỉnh đối diện và $0$ tại hai đỉnh còn lại không thực hiện được, vì hình chữ nhật nhỏ nhất chứa hai đỉnh đối diện là cả hình vuông.
:::

Thay hai chỉ số đo bằng mười chỉ số đo làm lớp lớn hơn. Theo đẳng thức sau Định nghĩa 01.24, với nghiệm ERM $\hat h$,
$$
\begin{aligned}
&L_D(\hat h)-L_D^{\mathrm{Bayes}}\\
&\quad=\Big[\inf_{h\in\mathcal H}L_D(h)-L_D^{\mathrm{Bayes}}\Big]\\
&\qquad+\Big[L_D(\hat h)-\inf_{h\in\mathcal H}L_D(h)\Big].
\end{aligned}
$$
Khi lớp lớn hơn, số hạng thứ nhất không tăng: mỗi hàm phân lớp tuyến tính trên hai chỉ số là một hàm trên mười chỉ số với hệ số $0$ cho tám chỉ số còn lại. Cận cho số hạng thứ hai, rủi ro vượt mức so với lớp, bằng hai lần cận độ lệch đều (Hệ quả 03.16(a)). Ở $m=10^4$, cận độ lệch đều tăng từ $0{,}164$ lên $0{,}280$ (Ví dụ 03.7), nên cận cho rủi ro vượt mức tăng từ $0{,}329$ lên $0{,}560$. Câu hỏi cho Bài 04 là: với một cỡ mẫu cho trước, nên chọn lớp nào giữa các lớp lồng nhau như vậy?

## 12. Tài liệu đọc

- **Trước buổi học:** UML §6.1–6.3 (lớp vô hạn có thể học được; chiều VC; các ví dụ).
- **Sau buổi học:** UML §6.4–6.5 (định lý cơ bản; chứng minh, gồm bổ đề Sauer và hội tụ đều), §9.1.3 (chiều VC của nửa không gian), §5.1 (định lý không có bữa trưa miễn phí); các bài tập UML §6.8 và §9.6 đã chọn ở §10.
- **Mở rộng:** UML Chương 28 (§28.1: cận hội tụ đều qua độ phức tạp Rademacher; §28.2: cận dưới cho trường hợp bất khả diễn; §28.3: cận trên cho trường hợp khả diễn).

**Quan hệ với giáo trình UML.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục. Các khác biệt chính:

- **Quy ước lớp.** Hàm ngưỡng $\mathbb 1[x\ge t]$ thay cho $\mathbb 1[x<a]$, khoảng đóng thay cho khoảng mở, nhãn $\{0,1\}$ với quy ước $\ge0$ thay cho nhãn $\pm1$; chứng minh cận trên xử lý phía nghiêm ngặt.
- **Hàm tăng trưởng.** Lấy giá trị lớn nhất trên bộ điểm, cho phép điểm lặp, thay cho tập điểm.
- **Bổ đề Sauer–Shelah.** Quy nạp kép theo $(m,d)$; UML quy nạp theo $m$ cho một khẳng định mạnh hơn. Dạng đóng $(em/d)^d$ đúng với mọi $1\le d\le m$; UML cần $m>d+1$.
- **Hội tụ đều.** Cận với xác suất cao qua mẫu bóng (bất đẳng thức Chebyshev) và bất đẳng thức Hoeffding với miền dài $2$, hằng số tường minh, phụ thuộc $\ln(1/\delta)$. UML §6.5 chặn kì vọng của độ lệch đều rồi dùng bất đẳng thức Markov, nên cận phụ thuộc $1/\delta$.
- **Nửa không gian.** Cận trên qua định lý Radon (Phụ lục A); UML §9.1 dùng phụ thuộc tuyến tính sau khi nâng chiều.
- **ERM, định lý cơ bản, cận dưới.** Bảo đảm cho ERM với cận dưới đúng; định lý cơ bản tách riêng điều kiện cần, không dùng (M); cận dưới phát biểu với miền $\epsilon<\epsilon_0$, $\delta<\delta_0$ và $d\ge2$ cho phần khả diễn.
- **Định lý không có bữa trưa miễn phí.** UML §5.1 viết $L_D(A(S))\ge1/8$; Định lý 03.17(a) viết $>1/8$, suy ra từ cùng cận $\mathbb E[L_D(A(S))]\ge1/4$ của chứng minh đó.

## Phụ lục

### A. Phân hoạch Radon và cận trên cho nửa không gian thuần nhất

Bổ đề 03.8 và cận trên của Mệnh đề 03.9(b) có chung một ý chứng minh: một hệ tuyến tính có nhiều ẩn hơn phương trình có nghiệm khác $0$, và các chỉ số được tách theo dấu của nghiệm.

::: proof Chứng minh Bổ đề 03.8
**Lộ trình.** Tìm một quan hệ phụ thuộc afin giữa $p+2$ điểm, rồi tách các hệ số theo dấu.

**Bước 1 (hệ tuyến tính).** Xét hệ ẩn $a=(a_1,\ldots,a_{p+2})\in\mathbb R^{p+2}$:
$$
\begin{aligned}
\textstyle\sum_{i=1}^{p+2}a_ix_i&=0,\\
\textstyle\sum_{i=1}^{p+2}a_i&=0.
\end{aligned}
$$
Phương trình thứ nhất gồm $p$ phương trình vô hướng, nên hệ có $p+1$ phương trình và $p+2$ ẩn. Do đó hệ có một nghiệm $a\ne0$.

**Bước 2 (hai tập chỉ số).** Đặt $I=\{i:a_i>0\}$ và $J=\{j:a_j\le0\}$; hai tập rời nhau và có hợp là $\{1,\ldots,p+2\}$. Vì $a\ne0$ và $\sum_ia_i=0$, nghiệm có ít nhất một hệ số dương và ít nhất một hệ số âm. Do đó $I\ne\varnothing$, và $J$ chứa chỉ số có hệ số âm nên $J\ne\varnothing$.

**Bước 3 (điểm chung).** Đặt $\alpha=\sum_{i\in I}a_i>0$. Từ $\sum_ia_i=0$ ta có $\sum_{j\in J}(-a_j)=\alpha$, và từ phương trình thứ nhất,
$$
z=\sum_{i\in I}\frac{a_i}\alpha x_i=\sum_{j\in J}\frac{-a_j}\alpha x_j .
$$
Các hệ số ở mỗi vế không âm và có tổng $1$, nên $z$ thuộc cả hai bao lồi.

$\square$ Phân hoạch Radon tồn tại cho mọi $p+2$ điểm của $\mathbb R^p$, kể cả khi có điểm trùng nhau.
:::

::: proof Chứng minh cận trên của Mệnh đề 03.9(b)
**Lộ trình.** Với $p+1$ điểm bất kì, dùng một quan hệ phụ thuộc tuyến tính để chỉ ra một cách gán nhãn mà không $h_{w,0}$ nào thực hiện được.

**Bước 1 (phụ thuộc tuyến tính).** Cho $x_1,\ldots,x_{p+1}\in\mathbb R^p$. Vì $p+1$ véc-tơ trong $\mathbb R^p$ phụ thuộc tuyến tính, có $a\ne0$ với $\sum_ia_ix_i=0$. Đổi dấu $a$ nếu cần, ta giả sử có ít nhất một $a_i>0$. Đặt $I=\{i:a_i>0\}\ne\varnothing$ và $J=\{j:a_j<0\}$. Với mọi $w$, lấy tích vô hướng với $w$:
$$
\sum_{i\in I}a_i\langle w,x_i\rangle=\sum_{j\in J}\lvert a_j\rvert\langle w,x_j\rangle .
$$

**Bước 2 (trường hợp $J\ne\varnothing$).** Xét một cách gán nhãn có nhãn $1$ trên $I$ và nhãn $0$ trên $J$. Nếu $h_{w,0}$ thực hiện nó thì $\langle w,x_i\rangle\ge0$ với $i\in I$ và $\langle w,x_j\rangle<0$ với $j\in J$. Khi đó vế trái của đẳng thức ở Bước 1 không âm, còn vế phải âm vì $J\ne\varnothing$, mâu thuẫn.

**Bước 3 (trường hợp $J=\varnothing$).** Xét một cách gán nhãn có nhãn $0$ trên $I$. Nếu $h_{w,0}$ thực hiện nó thì $\langle w,x_i\rangle<0$ với $i\in I$, nên $\sum_{i\in I}a_i\langle w,x_i\rangle<0$. Nhưng tổng này bằng $\langle w,\sum_ia_ix_i\rangle=0$, mâu thuẫn.

**Bước 4 (chỗ dùng quy ước).** Ở cả hai trường hợp, phía nghiêm ngặt $\langle w,x\rangle<0$ được đặt trên một tập chỉ số khác rỗng ($J$ ở Bước 2, $I$ ở Bước 3). Đây là chỗ quy ước $\ge0$ của Định nghĩa 03.7 được dùng.

$\square$ Không tập $p+1$ điểm nào bị $\mathcal H^p_{\mathrm{hom}}$ tách trọn, nên $\operatorname{VCdim}(\mathcal H^p_{\mathrm{hom}})\le p$; cùng Bước 3 của chứng minh Mệnh đề 03.9, ta được $\operatorname{VCdim}(\mathcal H^p_{\mathrm{hom}})=p$.
:::

### B. Bổ đề Sauer–Shelah, chứng minh đầy đủ

Đặt $\Phi(n,d)=\sum_{j=0}^{d}\binom nj$ với $n,d\ge0$ nguyên, theo quy ước $\binom nj=0$ khi $j>n$. Một tập $Y\subseteq\{0,1\}^n$ được coi là một lớp hàm trên tập vị trí $\{1,\ldots,n\}$; tập vị trí $B$ bị $Y$ tách trọn khi các véc-tơ của $Y$, hạn chế lên $B$, cho đủ $2^{\lvert B\rvert}$ cách gán nhãn.

::: proof Chứng minh Bổ đề 03.12(a)
**Lộ trình.** Chứng minh khẳng định sau bằng quy nạp kép theo $(n,d)$, rồi áp dụng cho $Y=\mathcal H_C$.

**Khẳng định $P(n,d)$.** Nếu $Y\subseteq\{0,1\}^n$ không tách trọn tập vị trí nào có $d+1$ phần tử thì $\lvert Y\rvert\le\Phi(n,d)$.

**Bước 1 (trường hợp gốc $n=0$).** $\{0,1\}^0$ có đúng một phần tử, véc-tơ rỗng, nên $\lvert Y\rvert\le1=\Phi(0,d)$ với mọi $d$.

**Bước 2 (trường hợp gốc $d=0$).** Nếu $Y$ có hai véc-tơ khác nhau, chúng khác nhau tại một vị trí $i$, và $Y$ tách trọn $\{i\}$. Do đó $Y$ không tách trọn vị trí nào khi và chỉ khi $\lvert Y\rvert\le1=\Phi(n,0)$.

**Bước 3 (tách theo vị trí cuối).** Cho $n\ge1$, $d\ge1$, và giả sử $P(n-1,d)$, $P(n-1,d-1)$ đúng. Gọi $Y'\subseteq\{0,1\}^{n-1}$ là tập các véc-tơ của $Y$ bỏ tọa độ cuối, và
$$
\begin{aligned}
&Y_1=\big\{y'\in\{0,1\}^{n-1}:\\
&\qquad(y',0)\in Y,\ (y',1)\in Y\big\}.
\end{aligned}
$$
Mỗi $y'\in Y'$ ứng với một hoặc hai phần tử của $Y$, và ứng với hai phần tử khi và chỉ khi $y'\in Y_1$. Do đó $\lvert Y\rvert=\lvert Y'\rvert+\lvert Y_1\rvert$.

**Bước 4 (giả thiết quy nạp).** Giả thiết quy nạp áp dụng cho hai họ véc-tơ nhãn $Y'$ và $Y_1$ trong $\{0,1\}^{n-1}$. Nếu $Y'$ tách trọn một tập vị trí $B\subseteq\{1,\ldots,n-1\}$ thì $Y$ cũng tách trọn $B$; vậy $Y'$ không tách trọn tập $d+1$ vị trí nào, và $\lvert Y'\rvert\le\Phi(n-1,d)$. Nếu $Y_1$ tách trọn $B$ thì $Y$ tách trọn $B\cup\{n\}$: mỗi cách gán nhãn của $B$ khớp với một $y'\in Y_1$, và cả $(y',0)$ lẫn $(y',1)$ thuộc $Y$. Vậy $Y_1$ không tách trọn tập $d$ vị trí nào, và $\lvert Y_1\rvert\le\Phi(n-1,d-1)$.

**Bước 5 (công thức Pascal).** Với $j\ge1$, $\binom{n-1}j+\binom{n-1}{j-1}=\binom nj$, kể cả khi $j>n-1$ theo quy ước trên. Do đó
$$
\begin{aligned}
\lvert Y\rvert&\le\Phi(n-1,d)\\
&\quad+\Phi(n-1,d-1)\\
&=\binom{n-1}0+\sum_{j=1}^{d}\binom{n-1}j\\
&\quad+\sum_{j=1}^{d}\binom{n-1}{j-1}\\
&=\binom n0+\sum_{j=1}^{d}\binom nj\\
&=\Phi(n,d).
\end{aligned}
$$
Mọi cặp $(n,d)$ với $n,d\ge1$ được đưa về hai cặp có $n$ nhỏ hơn, nên quy nạp theo $n$ (với mọi $d$ cùng lúc) chứng minh $P(n,d)$ cho mọi $n,d\ge0$.

**Bước 6 (áp dụng cho $\mathcal H$).** Cho $\mathcal H$ có chiều VC $d$ và một bộ $C=(x_1,\ldots,x_m)$. Đặt $Y=\mathcal H_C\subseteq\{0,1\}^m$. Nếu $Y$ tách trọn một tập vị trí $B$, các điểm $x_i$, $i\in B$, đôi một khác nhau, vì hai vị trí có cùng điểm luôn nhận cùng nhãn; khi đó $\mathcal H$ tách trọn tập $\{x_i:i\in B\}$ gồm $\lvert B\rvert$ điểm, nên $\lvert B\rvert\le d$. Theo $P(m,d)$, $\lvert\mathcal H_C\rvert\le\Phi(m,d)$. Lấy giá trị lớn nhất trên các bộ $C$ được (a).

$\square$ Khi điểm cuối $x_m$ trùng một điểm trước nó, không véc-tơ nào của $\mathcal H_C$ có hai nhãn khác nhau tại hai vị trí đó, nên $Y_1=\varnothing$ và Bước 3 cho $\lvert\mathcal H_C\rvert=\lvert\mathcal H_{C'}\rvert$; trường hợp này nằm sẵn trong lập luận trên.
:::

### C. Chứng minh đầy đủ Định lý 03.15

Trong phụ lục, $S=(Z_1,\ldots,Z_m)$ và mẫu bóng $S'=(Z'_1,\ldots,Z'_m)$ gồm $2m$ quan sát độc lập cùng phân bố $D$, hàm lỗi là hàm lỗi 0–1, $\mathcal H$ thỏa (T5) và (M), và $\epsilon>0$. Với $h\in\mathcal H$, đặt $a_i(h)=\ell(h,Z'_i)-\ell(h,Z_i)\in\{-1,0,1\}$, nên $L_{S'}(h)-L_S(h)=\frac1m\sum_ia_i(h)$.

::: proof Chứng minh Định lý 03.15
**Lộ trình.** Bảy bước: tính đo được, bổ đề mẫu bóng, đổi chỗ, lấy điều kiện theo mẫu gộp, ghép, bổ đề Sauer–Shelah, và phần (c).

**Bước C.1 (tính đo được và phép chọn).** Liệt kê $\mathcal H_0=\{g_1,g_2,\ldots\}$. Theo đoạn "Dưới (M), …" ở §7, với mọi cặp mẫu $(S,S')$,
$$
\begin{aligned}
&\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\\
&\quad=\sup_k\lvert L_S(g_k)-L_D(g_k)\rvert,\\
&\sup_{h\in\mathcal H}\lvert L_{S'}(h)-L_S(h)\rvert\\
&\quad=\sup_k\lvert L_{S'}(g_k)-L_S(g_k)\rvert;
\end{aligned}
$$
đẳng thức thứ hai đúng vì $L_{S'}$ và $L_S$ cùng chỉ dùng hữu hạn điểm. Cùng lý do cho $\sup_h\lvert\frac1m\sum_i\sigma_ia_i(h)\rvert=\sup_k\lvert\frac1m\sum_i\sigma_ia_i(g_k)\rvert$ với mọi $\sigma\in\{-1,1\}^m$. Các vế phải là cận trên đúng của dãy biến ngẫu nhiên, nên đo được. Gọi $B_\epsilon$ là biến cố $\{\sup_h\lvert L_S(h)-L_D(h)\rvert>\epsilon\}$. Trên $B_\epsilon$, đặt $h_S=g_k$ với $k$ nhỏ nhất thỏa $\lvert L_S(g_k)-L_D(g_k)\rvert>\epsilon$; ngoài $B_\epsilon$, đặt $h_S=g_1$. Mỗi tập $\{h_S=g_k\}$ đo được, và $h_S$ chỉ phụ thuộc $S$.

**Bước C.2 (bổ đề mẫu bóng).** Giả sử $m\epsilon^2\ge2$. Khi biết $S$, giả thuyết $h_S$ cố định, và vì $S'$ độc lập với $S$, các $\ell(h_S,Z'_i)$ độc lập, có kì vọng $L_D(h_S)$ và phương sai không quá $\tfrac14$ (Ví dụ 02.3, Bước 4). Bổ đề 02.3(b) với độ lệch $\epsilon/2$ cho
$$
\begin{aligned}
&\Pr\big(\lvert L_{S'}(h_S)-L_D(h_S)\rvert\\
&\qquad\ge\epsilon/2\mid S\big)\\
&\quad\le\frac{1/4}{m\epsilon^2/4}=\frac1{m\epsilon^2}\le\frac12 .
\end{aligned}
$$
Trên $B_\epsilon$, nếu $\lvert L_{S'}(h_S)-L_D(h_S)\rvert<\epsilon/2$ thì theo bất đẳng thức tam giác
$$
\begin{aligned}
&\lvert L_{S'}(h_S)-L_S(h_S)\rvert\\
&\quad\ge\lvert L_D(h_S)-L_S(h_S)\rvert\\
&\qquad-\lvert L_{S'}(h_S)-L_D(h_S)\rvert\\
&\quad>\epsilon-\epsilon/2=\epsilon/2 .
\end{aligned}
$$
Gọi $W$ là biến cố $\{\sup_h\lvert L_{S'}(h)-L_S(h)\rvert>\epsilon/2\}$. Lấy kì vọng theo $S$ (định lý Fubini, dùng tính độc lập của $S'$ với $S$), ta được $\Pr(W)\ge\mathbb E\big[\mathbb 1_{B_\epsilon}\cdot\tfrac12\big]=\tfrac12\Pr(B_\epsilon)$, tức
$$
\Pr(B_\epsilon)\le2\Pr(W).
$$
Bước này dùng (T1) cho tính độc lập của $S'$ với $S$ và tính bị chặn của hàm lỗi cho cận phương sai.

**Bước C.3 (đổi chỗ).** Cố định $\sigma\in\{-1,1\}^m$. Ánh xạ đổi chỗ $Z_i$ với $Z'_i$ tại các chỉ số có $\sigma_i=-1$ không đổi phân bố của $(S,S')$. Lý do: theo (T1), các cặp $(Z_i,Z'_i)$ độc lập, và mỗi cặp có phân bố $D\otimes D$, đối xứng khi đổi chỗ hai thành phần. Ánh xạ này biến $a_i(h)$ thành $\sigma_ia_i(h)$ đồng thời cho mọi $h$. Do đó
$$
\begin{aligned}
&\Pr(W)\\
&=\Pr\big(\sup_h\lvert\tfrac1m\textstyle\sum_i\sigma_ia_i(h)\rvert>\tfrac\epsilon2\big)
\end{aligned}
$$
với mọi $\sigma$ cố định, nên cũng đúng khi $\sigma_1,\ldots,\sigma_m$ là các dấu ngẫu nhiên độc lập, đều trên $\{-1,1\}$, độc lập với $(S,S')$.

**Bước C.4 (điều kiện theo mẫu gộp).** Cố định giá trị $(s,s')$ của $(S,S')$. Véc-tơ $(a_i(h))_{i\le m}$ chỉ phụ thuộc $h$ qua cách gán nhãn của $h$ trên bộ $2m$ điểm $(x_1,\ldots,x_m,x'_1,\ldots,x'_m)$. Theo (T5), lớp không đổi theo $(s,s')$, nên theo Định nghĩa 03.11, tập các véc-tơ này có nhiều nhất $\Pi_{\mathcal H}(2m)$ phần tử. Với một véc-tơ cố định $a\in[-1,1]^m$, các biến $\sigma_ia_i$ độc lập, có kì vọng $0$ và nằm trong $[-1,1]$. Định lý 02.7(c) với miền dài $2$ cho
$$
\begin{aligned}
&\Pr_\sigma\big(\lvert\tfrac1m\textstyle\sum_i\sigma_ia_i\rvert\ge\tfrac\epsilon2\big)\\
&\quad\le2\exp\big(-2m(\epsilon/2)^2/4\big)\\
&\quad=2e^{-m\epsilon^2/8}.
\end{aligned}
$$
Áp dụng Bổ đề 02.12 cho nhiều nhất $\Pi_{\mathcal H}(2m)$ véc-tơ, ta được xác suất có điều kiện của biến cố ở Bước C.3 không quá $2\Pi_{\mathcal H}(2m)e^{-m\epsilon^2/8}$. Cận này đúng với mọi $(s,s')$, nên lấy kì vọng theo $(S,S')$, ta được
$$
\Pr(W)\le2\,\Pi_{\mathcal H}(2m)\,e^{-m\epsilon^2/8}.
$$

**Bước C.5 (ghép và giải theo $\delta$).** Từ C.2–C.4, khi $m\epsilon^2\ge2$,
$$
\Pr(B_\epsilon)\le4\,\Pi_{\mathcal H}(2m)\,e^{-m\epsilon^2/8}.
$$
Lấy $\epsilon=\rho_m$, vế phải bằng $\delta$. Điều kiện $m\rho_m^2\ge2$ tự thỏa, vì $\Pi_{\mathcal H}(2m)\ge1$ và $\delta<1$ cho $m\rho_m^2=8\ln(4\Pi_{\mathcal H}(2m)/\delta)>8\ln4\approx11{,}09$. Do đó độ lệch đều không quá $\rho_m$ với xác suất ít nhất $1-\delta$; vì độ lệch đều luôn không quá $1$, cận cũng là $\min\{1,\rho_m\}$. Đây là phần (a).

**Bước C.6 (bổ đề Sauer–Shelah và hằng số $4$).** Nếu $1\le d\le m$ thì $d\le2m$, nên Bổ đề 03.12 tại $2m$ điểm cho $\Pi_{\mathcal H}(2m)\le(2em/d)^d$ và
$$
\rho_m\le\sqrt{\tfrac8m\big(d\ln\tfrac{2em}d+\ln\tfrac4\delta\big)}.
$$
Vì $m\ge d$, ta có $\ln(em/d)\ge1$, nên $d\ln(2em/d)=d\ln2+d\ln(em/d)\le(1+\ln2)\,d\ln(em/d)$. Vì $\delta<1$, ta có $\ln(2/\delta)>\ln2$, nên $\ln(4/\delta)=\ln2+\ln(2/\delta)\le2\ln(2/\delta)$. Do $1+\ln2<2$, biểu thức trong căn không quá $16\big(d\ln(em/d)+\ln(2/\delta)\big)/m$, và căn bậc hai cho hằng số $4$. Đây là phần (b).

**Bước C.7 (phần (c)).** Đặt $\kappa=8/\epsilon^2$ và $u_0=4e\kappa$. Hàm $\ln$ lõm nên nằm dưới tiếp tuyến tại $u_0$: $\ln u\le u/u_0+\ln u_0-1$ với mọi $u>0$. Với $u=2em/d$, ta có $u/u_0=m/(2\kappa d)$ và $\ln u_0-1=\ln(4\kappa)$, nên
$$
\kappa d\ln\frac{2em}d\le\frac m2+\kappa d\ln(4\kappa).
$$
Giả sử $m\ge2\kappa\big(d\ln(4\kappa)+\ln(4/\delta)\big)$, tức
$$
m\ge\frac{16}{\epsilon^2}\Big(d\ln\frac{32}{\epsilon^2}+\ln\frac4\delta\Big).
$$
Khi đó $m\ge d$, vì $2\kappa\ln(4\kappa)>1$, và
$$
\begin{aligned}
&\kappa\big(d\ln(2em/d)+\ln(4/\delta)\big)\\
&\quad\le\tfrac m2+\kappa d\ln(4\kappa)\\
&\qquad+\kappa\ln(4/\delta)\le m,
\end{aligned}
$$
tức $8\big(d\ln(2em/d)+\ln(4/\delta)\big)/m\le\epsilon^2$. Theo Bước C.6, $\rho_m\le\epsilon$. Biến cố "độ lệch đều không quá $\epsilon$" chứa biến cố của phần (a), nên có xác suất ít nhất $1-\delta$, và nó đo được theo Bước C.1. Điều này đúng với mọi $D$, nên $\mathcal H$ có tính chất hội tụ đều với $m^{UC}_{\mathcal H}(\epsilon,\delta)$ không quá phần nguyên trên của vế phải.

$\square$ Mọi giả thiết đều được dùng: (T1) ở C.2 và C.3, tính bị chặn của hàm lỗi ở C.2 và C.4, (T5) ở C.4, (M) ở C.1 và C.7, chiều VC hữu hạn ở C.6.
:::

### D. Điều kiện (M) cho lớp khoảng và lớp nửa không gian afin

Nhận xét 03.14 kiểm (M) cho lớp hàm ngưỡng. Hai lớp còn lại được kiểm dưới đây.

**Lớp khoảng.** Lấy $\mathcal H_0$ gồm các $h_{u,v}$ với $u\le v$ hữu tỉ. Với $u\le v$ bất kì, chọn dãy hữu tỉ $u_k\uparrow u$ và $v_k\downarrow v$, nên $u_k\le v_k$. Nếu $x\in[u,v]$ thì $x\in[u_k,v_k]$ với mọi $k$. Nếu $x<u$ thì $x<u_k$ khi $k$ đủ lớn, và nếu $x>v$ thì $x>v_k$ khi $k$ đủ lớn. Do đó $h_{u_k,v_k}(x)\to h_{u,v}(x)$ với mọi $x$.

**Lớp nửa không gian afin.** Lấy $\mathcal H_0$ gồm các $h_{w,b}$ với $w\in\mathbb Q^p$ và $b\in\mathbb Q$. Với $(w,b)$ bất kì, chọn $w_k\in\mathbb Q^p$ với $\lVert w_k-w\rVert\le1/k^2$ và $b_k\in\mathbb Q\cap[b+1/k,b+2/k]$. Đặt $g(x)=\langle w,x\rangle+b$ và $g_k(x)=\langle w_k,x\rangle+b_k$. Theo bất đẳng thức Cauchy–Schwarz,
$$
\begin{aligned}
g_k(x)&\ge g(x)+\frac1k-\frac{\lVert x\rVert}{k^2},\\
g_k(x)&\le g(x)+\frac2k+\frac{\lVert x\rVert}{k^2}.
\end{aligned}
$$

- **Điểm có $g(x)\ge0$, kể cả điểm trên siêu phẳng.** Khi $k\ge\lVert x\rVert$, ta có $\lVert x\rVert/k^2\le1/k$, nên $g_k(x)\ge0$ và $h_{w_k,b_k}(x)=1=h_{w,b}(x)$.
- **Điểm có $g(x)<0$.** Vế phải của bất đẳng thức thứ hai tiến về $g(x)<0$, nên $g_k(x)<0$ và $h_{w_k,b_k}(x)=0$ khi $k$ đủ lớn.

Hệ số tự do $b_k$ được chọn lớn hơn $b$ một chút để các điểm trên siêu phẳng giữ nhãn $1$; chọn $b_k=b$ với $w_k\to w$ có thể đổi nhãn của những điểm đó. Với lớp vô hạn, (M) chỉ bảo đảm độ lệch đều đo được.
