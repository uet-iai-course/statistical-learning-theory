# Bài 07 — Mạng nơ-ron, năng lực mô hình và tham số hóa thừa

Định lý 03.15 chặn độ lệch đều qua chiều VC, và với lớp nửa không gian trong $\mathbb R^p$, chiều VC tăng theo $p$ (Mệnh đề 03.9), nên cận không cho thông tin khi $p$ vượt cỡ mẫu $m$. Bài 06 chặn khoảng cách tổng quát hóa kì vọng bằng tính ổn định, nhưng cần hàm lỗi lồi theo tham số, còn hàm lỗi của mạng nơ-ron theo trọng số nói chung không lồi. Chúng ta cần một đại lượng đo độ phức tạp vẫn cho thông tin khi một mạng lớn khớp được cả nhãn gán ngẫu nhiên (câu hỏi cuối Bài 06).

Câu hỏi trung tâm của bài là đại lượng nào đo được năng lực thống kê (statistical capacity) của một lớp mạng nơ-ron khi số tham số vượt cỡ mẫu. Các công cụ là mạng nơ-ron lan truyền tới (feedforward neural network) cùng năng lực biểu diễn (expressivity) của nó, tham số hóa thừa (overparameterization) so với một mẫu, độ phức tạp Rademacher (Rademacher complexity) và lề (margin).

## Câu hỏi mở đầu

Một mạng nơ-ron phân lớp các điểm $x$ của hình tròn đơn vị trong $\mathbb R^2$. Nó có một lớp nơ-ron ẩn (hidden layer) gồm $N=2000$ nơ-ron ReLU (rectified linear unit), mỗi nơ-ron tính $\max\{0,\langle v,x\rangle+b\}$ với $v$, $b$ riêng, rút ngẫu nhiên một lần rồi giữ cố định. Lớp nơ-ron ra (output layer) nhận các đầu ra này chia cho $\sqrt N$. Chỉ $2000$ trọng số của lớp ra được huấn luyện: trong các bộ trọng số khớp đúng nhãn $\pm1$ tại mọi điểm huấn luyện, phép huấn luyện chọn bộ có chuẩn nhỏ nhất.

Mẫu huấn luyện gồm $m=200$ điểm rút đều trong hình tròn, với nhãn thật $y=\mathbb 1[x_1+0{,}5x_2\ge0]$. Trên cùng các điểm và cùng lớp ẩn, mạng được huấn luyện hai lần.

- **Nhãn thật.** Mỗi điểm giữ nhãn thật của nó.
- **Nhãn hoán vị** (permuted labels). Các nhãn huấn luyện được hoán vị ngẫu nhiên giữa các điểm, nên nhãn không còn liên hệ với vị trí của điểm.

Thí nghiệm lặp lại với mười hạt giống ngẫu nhiên (random seed). Lỗi kiểm tra đo trên $5000$ điểm mới rút độc lập; với nhãn hoán vị, nhãn kiểm tra cũng được hoán vị, độc lập với mẫu huấn luyện.

| Nhãn | Lỗi huấn luyện | Lỗi kiểm tra trung bình | Nhỏ nhất – lớn nhất |
|---|---|---|---|
| Thật | $0$ | $0{,}023$ | $0{,}014$ – $0{,}036$ |
| Hoán vị | $0$ | $0{,}501$ | $0{,}480$ – $0{,}512$ |

**Câu hỏi.** Hai trường hợp có cùng kiến trúc, cùng số tham số, cùng điểm huấn luyện và cùng lỗi huấn luyện $0$. Vì sao lỗi kiểm tra khác nhau?

Có phải mạng quá khớp (overfitting) vì có nhiều tham số hơn số quan sát không? Với nhãn thật, cùng mạng đó có lỗi kiểm tra khoảng $2\%$, nên số tham số không giải thích được sự khác nhau. Năng lực của cả lớp hàm mà kiến trúc biểu diễn được cũng không giải thích được. Lớp này thực hiện được mọi cách gán nhãn của $200$ điểm huấn luyện. Do đó độ phức tạp Rademacher của nó (§6), đo mức khớp nhãn ngẫu nhiên trên các điểm đó, như nhau trong hai trường hợp.

Hai trường hợp khác nhau ở hàm mà phép huấn luyện chọn. Chuẩn của véc-tơ trọng số lớp ra, trên các đầu ra ẩn đã chia $\sqrt N$, trung bình khoảng $916$ với nhãn thật và khoảng $10\,853$ với nhãn hoán vị (§9); cận theo chuẩn và lề ở §8 dùng đúng đại lượng này. Bảng trên là bằng chứng thí nghiệm, không phải chứng minh; giao thức ở Phụ lục D.

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Phân biệt năng lực biểu diễn, năng lực thống kê và khả năng tối ưu của một lớp mạng nơ-ron; kiểm tra một mạng ReLU nhỏ biểu diễn đúng một hàm Boole cho trước.
2. Tính độ phức tạp Rademacher thực nghiệm của một lớp nhỏ bằng cách liệt kê bộ dấu, và nối nó với lỗi nhỏ nhất khi khớp nhãn ngẫu nhiên.
3. Phát biểu cận tổng quát hóa theo độ phức tạp Rademacher, trình bày các bước chứng minh và chỉ ra chỗ dùng mẫu độc lập cùng phân bố, hàm lỗi bị chặn, lớp cố định trước mẫu.
4. Chứng minh cận độ phức tạp Rademacher cho lớp hàm tuyến tính bị chặn theo chuẩn, rồi suy ra và tính bằng số cận theo lề cho phân lớp tuyến tính.
5. Giải thích bằng ví dụ vì sao số tham số không quyết định lỗi kiểm tra, vì sao chuẩn và lề cho thêm thông tin, và vì sao một cận lớn hơn một không cho biết gì về chất lượng của mô hình.

## Kiến thức tiên quyết

- **Từ Bài 01.** (T1), (T2); rủi ro, khoảng cách tổng quát hóa (Định nghĩa 01.1, 01.6, 01.10); tính không chệch (Mệnh đề 01.7).
- **Từ Bài 02.** Phương pháp Chernoff, bổ đề Hoeffding, bất đẳng thức hợp (Bổ đề 02.5, 02.6, 02.12); bất đẳng thức Hoeffding (Định lý 02.7) và (T3) (đoạn sau Nhận xét 02.8); cận tin cậy (Hệ quả 02.10); mẫu $\epsilon$-đại diện (Định nghĩa 02.13).
- **Từ Bài 03.** Lớp hàm ngưỡng (Ví dụ 03.1); tách trọn, chiều VC (Định nghĩa 03.2, 03.3); nửa không gian (Định nghĩa 03.7, Mệnh đề 03.9, Ví dụ 03.3); số tham số và chiều VC (Nhận xét 03.10); hàm tăng trưởng (Định nghĩa 03.11); hội tụ đều (Định nghĩa 03.13); (M), (T5) (trước Nhận xét 03.14, trước Định lý 03.15); Định lý 03.15 với Bước 1–4 của chứng minh; Ví dụ 03.8; Hệ quả 03.16.
- **Từ Bài 04.** Sai số xấp xỉ (Định nghĩa 04.1); cận ba thành phần (Mệnh đề 04.3); kiểm soát đồng thời trên một họ lớp (Bổ đề 04.9, Ví dụ 04.10).
- **Từ Bài 05–06.** $h_w$, $h_{w,0}$, $\tilde y$, $C_x$ (§2 của Bài 05); hàm Lipschitz (Định nghĩa 05.4, Mệnh đề 05.5); thuật toán có nguồn ngẫu nhiên riêng (Định nghĩa 05.18); mẫu lân cận (Định nghĩa 06.9); bỏ chính quy hóa (Ví dụ 06.7).
- **Giải tích và xác suất.** Bất đẳng thức Cauchy–Schwarz (dấu bằng khi hai véc-tơ cùng hướng); bất đẳng thức Jensen cho hàm lõm $t\mapsto\sqrt t$ và $\sup\mathbb E\le\mathbb E\sup$; kì vọng có điều kiện và tính chất tháp (Phụ lục A).

**Câu hỏi ôn nhanh.**

1. Các biến $\sigma_1,\sigma_2,\sigma_3$ độc lập, nhận $\pm1$ với xác suất $\tfrac12$. Tính $\mathbb E\lvert\sigma_1+\sigma_2+\sigma_3\rvert$ và $\sqrt{\mathbb E(\sigma_1+\sigma_2+\sigma_3)^2}$.
2. Cho số nguyên $N\ge1$ và $m\le N$ véc-tơ độc lập tuyến tính $x_1,\ldots,x_m\in\mathbb R^N$. Lớp nửa không gian thuần nhất $\mathcal H^N_{\mathrm{hom}}$ có tách trọn bộ $(x_1,\ldots,x_m)$ không? Chiều VC của lớp bằng bao nhiêu?
3. Cho $V_1,\ldots,V_{200}$ độc lập, nhận giá trị trong $[0,1]$, với trung bình $\bar V$. Tìm $t$ để Định lý 02.7(a) cho $\Pr(\bar V-\mathbb E\bar V\ge t)\le0{,}025$.

::: solution Lời giải câu hỏi ôn nhanh
1. Tổng bằng $\pm3$ khi ba dấu bằng nhau (xác suất $\tfrac18$ cho mỗi dấu) và bằng $\pm1$ trong sáu trường hợp còn lại (xác suất $\tfrac38$ cho mỗi dấu). Do đó
$$
\begin{aligned}
&\mathbb E\lvert\sigma_1+\sigma_2+\sigma_3\rvert\\
&=\frac{2\cdot3+6\cdot1}8=1{,}5 .
\end{aligned}
$$
Khai triển bình phương: $\mathbb E\sigma_i^2=1$, và với $i\ne j$, $\mathbb E[\sigma_i\sigma_j]=\mathbb E\sigma_i\,\mathbb E\sigma_j=0$ do tính độc lập. Do đó $\mathbb E(\sigma_1+\sigma_2+\sigma_3)^2=3$, và căn bậc hai bằng $\sqrt3\approx1{,}7321$.
2. Có. Với một cách gán nhãn $(y_1,\ldots,y_m)\in\{0,1\}^m$, ma trận có các hàng $x_i^\top$ có hạng $m$, nên hệ $\langle w,x_i\rangle=2y_i-1$, $i=1,\ldots,m$, có nghiệm $w$. Khi đó $h_{w,0}(x_i)=y_i$, nên lớp tách trọn bộ điểm; chiều VC bằng $N$ (Mệnh đề 03.9(b)).
3. Định lý 02.7(a) với $b-a=1$ cho cận $e^{-2\cdot200\,t^2}$. Đặt cận này bằng $0{,}025$:
$$
\begin{aligned}
400\,t^2&=\ln40\approx3{,}6889,\\
t&=\sqrt{\ln40/400}\\
&\approx0{,}0961 .
\end{aligned}
$$
Giá trị được làm tròn lên, để cận vẫn không quá $0{,}025$.
:::

## 1. Thiết lập bài toán

Bài toán có tám thành phần. Khác Bài 05–06, lớp hàm có thể không lồi theo tham số, và các bảo đảm đúng đồng thời cho mọi hàm của một lớp chọn trước mẫu.

1. **Dữ liệu.** Quan sát $z=(x,y)\in\mathcal Z=\mathcal X\times\{0,1\}$, $\mathcal X\subseteq\mathbb R^p$, từ một phân bố $D$ chưa biết; $\tilde y=2y-1$.
2. **Cơ chế lấy mẫu.** Mẫu huấn luyện $S=(Z_1,\ldots,Z_m)\sim D^m$ theo (T1); *mẫu kiểm tra* (test sample) độc lập, chỉ dùng trong thí nghiệm.
3. **Lớp hàm.** *Hàm điểm số* (score function) của một kiến trúc mạng hay của một lớp con chọn trước mẫu (§4–§5); hàm phân lớp tương ứng là $\mathbb 1[f\ge0]$, với $f$ là hàm điểm số.
4. **Hàm lỗi.** Hàm lỗi 0–1; ở §8 thêm hàm lỗi dốc, ở §9 hàm lỗi bình phương chia cho một hằng số, cả hai nhận giá trị trong $[0,1]$.
5. **Thuật toán.** Bất kì (ERM, SGD trên hàm mục tiêu không lồi, phép nội suy); các kết quả chỉ cần đầu ra nằm trong lớp đã chọn trước.
6. **Mục tiêu.** Rủi ro kì vọng 0–1 của đầu ra, chặn bằng một đại lượng thực nghiệm cộng một số hạng phạt.
7. **Đối tượng so sánh.** Không cần cho cận khoảng cách tổng quát hóa; cận dưới đúng của $L_D$ trên lớp khi xét rủi ro vượt mức của ERM (§9).
8. **Tài nguyên.** Cỡ mẫu $m$ và độ tin cậy $\delta$; từ §8, bán kính $B$ và lề $\gamma$, chọn trước mẫu.

Các đại lượng của bài chia theo nguồn ngẫu nhiên như bảng dưới.

| Loại | Đại lượng |
|---|---|
| Cố định | $D$, $p$; kiến trúc (độ sâu, các độ rộng, hàm kích hoạt); lớp hàm; $B$, $C_x$, $\gamma$, $\delta$ |
| Ngẫu nhiên theo dữ liệu | $S$; rủi ro thực nghiệm; độ phức tạp Rademacher thực nghiệm (§6); tham số do huấn luyện chọn |
| Ngẫu nhiên theo nguồn riêng của thuật toán | khởi tạo và chỉ số của SGD; trong thí nghiệm, trọng số lớp ẩn |
| Chỉ trong định nghĩa và chứng minh | biến Rademacher (§6), mẫu bóng (Bài 03) |

Trong thí nghiệm, trọng số lớp ẩn được rút độc lập với $S$. Khi cố định lớp ẩn, các hàm của lớp ra lập thành một lớp chọn trước mẫu, và các kết quả cấp lớp áp dụng có điều kiện theo lớp ẩn.

## 2. Kí hiệu và giả thiết

Bảng dưới gom các kí hiệu dùng từ §3; kí hiệu khác được đặt tên tại chỗ dùng lần đầu.

| Kí hiệu | Ý nghĩa |
|---|---|
| $L_D(h)$, $L_S(h)$ | rủi ro kì vọng, rủi ro thực nghiệm (Bài 01) |
| $h_w(x)=\langle w,x\rangle$, $h_{w,0}=\mathbb 1[h_w\ge0]$ | hàm điểm số tuyến tính, hàm phân lớp tương ứng (Bài 05) |
| $h_{w,b}$, $\mathcal H^p_{\mathrm{aff}}$, $\mathcal H^p_{\mathrm{hom}}$, $d$ | nửa không gian afin, hai lớp nửa không gian, chiều VC (Bài 03) |
| $B$, $C_x$ | cận chuẩn của véc-tơ trọng số (§5, §8); cận của $\lVert x\rVert$ (Bài 05) |
| $\operatorname{ReLU}(t)=\max\{0,t\}$ | hàm ReLU |

Giả thiết thống kê là (T1) dạng đầy đủ, dùng ở §7–§9. Định lý chính ở §7 cần thêm ba điều kiện cho lớp hàm lỗi (loss class): giá trị trong $[0,1]$ như (T3), lớp cố định trước mẫu như (T5), và điều kiện đo được (M) cho hàm giá trị thực. Bài 02–03 phát biểu chúng cho lớp giả thuyết, nên ta viết lại chúng trong giả thiết của định lý. Từ §8, ta thêm $\lVert x\rVert\le C_x$ trên giá của $D$. Không có giả thiết tối ưu: các kết quả không dùng tính lồi, tính trơn hay sự hội tụ của thuật toán.

## 3. Ví dụ xuyên suốt

::: example Ví dụ 07.1 (Mẫu bốn điểm của phép hoặc loại trừ)
**Thiết lập.** Cho $p=2$, $\mathcal X=\{0,1\}^2$ và nhãn $y=x_1\oplus x_2$, phép *hoặc loại trừ* (exclusive or, XOR): $y=1$ khi đúng một tọa độ của $x$ bằng $1$. Phân bố $D$ đều trên bốn quan sát, mẫu $S$ gồm đúng bốn quan sát này ($m=4$), hàm lỗi 0–1; không có đại lượng ngẫu nhiên.

**Bước 1: nhãn.** Tại $(0,0)$, $(1,0)$, $(0,1)$, $(1,1)$, nhãn lần lượt là $y=0,1,1,0$, tức $\tilde y=-1,1,1,-1$.

**Bước 2: lớp nửa không gian afin.** Hai điểm nhãn $0$ nằm trên một đường chéo của hình vuông, hai điểm nhãn $1$ trên đường chéo kia, và hai đường chéo cắt nhau tại $(\tfrac12,\tfrac12)$. Theo Ví dụ 03.3, Bước 3, không hàm nào của $\mathcal H^2_{\mathrm{aff}}$ thực hiện cách gán nhãn này (xem thêm Bài tập 07.1).

**Bước 3: hàm afin tốt nhất.** Với $w=(1,1)$ và $b=-\tfrac12$, giá trị $\langle w,x\rangle+b$ tại bốn điểm trên lần lượt là $-\tfrac12$, $\tfrac12$, $\tfrac12$, $\tfrac32$. Hàm $h_{w,b}$ chỉ sai tại $(1,1)$: $L_S(h_{w,b})=\tfrac14$.

**Bước 4: rủi ro nhỏ nhất.** Theo Bước 2, mọi hàm của lớp sai ít nhất một quan sát, nên $\min_{h\in\mathcal H^2_{\mathrm{aff}}}L_S(h)=\tfrac14$; vì $D$ đều trên bốn quan sát của mẫu, $L_D=L_S$.

**Kết luận.** Lớp nửa không gian afin có rủi ro nhỏ nhất $\tfrac14$; ở §4, một mạng với hai nơ-ron ẩn phân lớp đúng cả bốn quan sát.
:::

::: application Phân lớp văn bản với một trăm nghìn đặc trưng
**Thiết lập.** Mỗi văn bản được biểu diễn bằng véc-tơ tần suất từ (bag of words) đã chuẩn hóa, gồm $p=10^5$ tọa độ, với $\lVert x\rVert\le C_x=1$. Có $m=10^4$ văn bản có nhãn $y\in\{0,1\}$. Hàm phân lớp $h_{w,0}$ thuộc lớp $\mathcal H^p_{\mathrm{hom}}$ có chiều VC $d=p>2m$ (Mệnh đề 03.9(b)), nên Định lý 03.15 không cho thông tin.

**Câu hỏi thực hành.** Một bộ giải trả về $w$ với $\lVert w\rVert\le B$, đa số văn bản có lề $\tilde y\langle w,x\rangle$ ít nhất $\gamma$ (§8), và $BC_x/\gamma=10$, với $B$, $\gamma$ chọn trước mẫu. Có bảo đảm nào cho tỉ lệ lỗi của $h_{w,0}$ không? Câu trả lời ở §9. Các giá trị $p$ và $BC_x/\gamma$ là giả định; ứng dụng không dùng số liệu thật.
:::

Để phân lớp đúng Ví dụ 07.1, chúng ta cần một lớp lớn hơn lớp nửa không gian afin; với lớp rất lớn của ứng dụng, chúng ta cần một đại lượng đo năng lực khác chiều VC.

## 4. Mạng nơ-ron lan truyền tới và năng lực biểu diễn

Một mạng nơ-ron ghép nhiều hàm afin, xen giữa bởi một hàm phi tuyến.

::: definition Định nghĩa 07.1 (Mạng nơ-ron lan truyền tới)
Cho số chiều đầu vào $p$ và một hàm $\varsigma:\mathbb R\to\mathbb R$. Mạng gồm năm thành phần.

- **Kiến trúc.** Số nguyên $J\ge1$, gọi là *độ sâu* (depth), và các số nguyên dương $N_0=p,N_1,\ldots,N_{J-1}$, $N_J=1$; $N_j$ là số nơ-ron của *lớp nơ-ron* (layer) thứ $j$, và khi $J\ge2$, $N=\max_{1\le j\le J-1}N_j$ là *độ rộng* (width) của mạng.
- **Hàm kích hoạt.** $\varsigma$, *hàm kích hoạt* (activation function), áp dụng cho từng tọa độ của một véc-tơ; trong bài chủ yếu là $\operatorname{ReLU}$.
- **Tham số.** $\theta=(\Theta_1,b_1,\ldots,\Theta_J,b_J)$, gồm các *ma trận trọng số* $\Theta_j\in\mathbb R^{N_j\times N_{j-1}}$ và các *hệ số tự do* $b_j\in\mathbb R^{N_j}$; kiến trúc có $\sum_{j=1}^JN_j(N_{j-1}+1)$ tham số.
- **Hàm điểm số.** Hàm $f_\theta:\mathbb R^p\to\mathbb R$ cho bởi $a_0=x$ và, với $j=1,\ldots,J-1$,
  $$
  \begin{aligned}
  a_j&=\varsigma(\Theta_ja_{j-1}+b_j),\\
  f_\theta(x)&=\Theta_Ja_{J-1}+b_J .
  \end{aligned}
  $$
- **Hàm phân lớp.** $h_\theta(x)=\mathbb 1[f_\theta(x)\ge0]$.

Bộ này được gọi là một *mạng nơ-ron lan truyền tới*; với $J=2$, $f_\theta(x)=\Theta_2\,\varsigma(\Theta_1x+b_1)+b_2$.
:::

Các lớp nơ-ron $1,\ldots,J-1$ là lớp ẩn, lớp thứ $J$ là lớp ra; lớp ra không có hàm kích hoạt, nên $f_\theta(x)$ là một số thực. Ta viết "lớp nơ-ron" để phân biệt với lớp giả thuyết, và viết $\varsigma$ thay cho chữ $\sigma$ của UML vì $\sigma$ dành cho biến Rademacher (§6).

Với $J=1$, $h_\theta=h_{w,b}$ với $w=\Theta_1^\top$, $b=b_1$: lớp nửa không gian afin là lớp mạng độ sâu $1$. Với $p=2$, $J=2$, $N_1=2$, kiến trúc có $2\cdot3+1\cdot3=9$ tham số. Ngược lại, hàm phân lớp $\mathbb 1[x\in\mathbb Q]$ trên $\mathbb R$ không thuộc lớp mạng ReLU nào: $f_\theta$ liên tục nên $\{f_\theta\ge0\}$ là tập đóng, còn $\mathbb Q$ thì không.

::: proposition Mệnh đề 07.2 (Biểu diễn phép hoặc loại trừ bằng mạng ReLU) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Kiến trúc.** $p=2$, $J=2$, $N_1=2$, hàm kích hoạt $\operatorname{ReLU}$.
- **Tham số.** $\Theta_1$ có hai hàng bằng $(1,1)$, $b_1=(0,-1)^\top$, $\Theta_2=(1,\,-2)$ và $b_2=-\tfrac12$.
- **Đầu vào.** $x\in\{0,1\}^2$, bốn điểm của Ví dụ 07.1.

**Bảo đảm.** Tất định, chỉ về bốn điểm của $\{0,1\}^2$: với $s=x_1+x_2$, hàm điểm số $f_\theta(x)=\operatorname{ReLU}(s)-2\operatorname{ReLU}(s-1)-\tfrac12$ nhận các giá trị $-\tfrac12$, $\tfrac12$, $\tfrac12$, $-\tfrac12$ tại $(0,0)$, $(1,0)$, $(0,1)$, $(1,1)$, nên $h_\theta(x)=x_1\oplus x_2$ với mọi $x\in\{0,1\}^2$.
:::

::: proof Chứng minh Mệnh đề 07.2
**Lộ trình.** Hàm $f_\theta$ chỉ phụ thuộc $x$ qua tổng $s$; ta tính ba giá trị của nó.

**Bước 1 (lớp ẩn).** Hai hàng của $\Theta_1$ đều bằng $(1,1)$, nên $\Theta_1x+b_1=(s,\ s-1)^\top$, và
$$
\begin{aligned}
f_\theta(x)={}&\operatorname{ReLU}(s)\\
&-2\operatorname{ReLU}(s-1)-\tfrac12 .
\end{aligned}
$$

**Bước 2 (ba giá trị của $s$).** Trên $\{0,1\}^2$, $s\in\{0,1,2\}$, và
$$
\begin{aligned}
s=0:&\quad0-0-\tfrac12=-\tfrac12,\\
s=1:&\quad1-0-\tfrac12=\tfrac12,\\
s=2:&\quad2-2-\tfrac12=-\tfrac12 .
\end{aligned}
$$

**Bước 3 (so với nhãn).** $s=1$ khi và chỉ khi $x_1\oplus x_2=1$, nên $f_\theta(x)\ge0$ khi và chỉ khi $x_1\oplus x_2=1$.

$\square$ Với rủi ro tham chiếu $L^*=0$ (nhãn là hàm tất định của $x$), sai số xấp xỉ (Định nghĩa 04.1) trên Ví dụ 07.1 của lớp mạng độ sâu $2$ với hai nơ-ron ẩn bằng $0$, của lớp nửa không gian afin bằng $\tfrac14$.
:::

Mạng cũng gán nhãn cho các điểm ngoài mẫu: tại $x=(\tfrac12,\tfrac12)$, $s=1$ và $f_\theta(x)=\tfrac12$, nên $h_\theta(x)=1$. Bài tập 07.1 mô tả cả miền $\{x:f_\theta(x)\ge0\}$.

::: remark Nhận xét 07.3 (Xấp xỉ phổ quát và sai số xấp xỉ)
Với hàm kích hoạt dấu (sign), mọi hàm Boole trên $\{\pm1\}^p$ được biểu diễn bởi một mạng độ sâu $2$, nhưng số nơ-ron cần thiết tăng theo hàm mũ của $p$ (UML §20.3). Mạng sigmoid có tính *xấp xỉ phổ quát* (universal approximation): mọi hàm Lipschitz từ $[-1,1]^p$ vào $[-1,1]$ được xấp xỉ đều tới sai số $\epsilon>0$, với số nơ-ron tăng theo hàm mũ của $p$ (UML §20.3; Bài tập 07.9 cho ReLU và $p=1$).

Theo các kết quả này, lớp chứa một hàm tốt (sai số xấp xỉ nhỏ); chúng không cho biết cần bao nhiêu quan sát (sai số ước lượng) hay thuật toán nào tìm được hàm đó (sai số tối ưu). Với hàm kích hoạt dấu và ba nơ-ron ẩn cùng một nơ-ron hằng, tìm nghiệm ERM đã là bài toán NP-khó (NP-hard) (UML §20.5).
:::

Về một lớp mạng, chúng ta có ba câu hỏi, ứng với ba số hạng của Mệnh đề 04.3. Năng lực biểu diễn ứng với sai số xấp xỉ; năng lực thống kê ứng với số hạng $2r$ khi $S$ là $r$-đại diện (Định nghĩa 02.13); khả năng tối ưu ứng với sai số tối ưu thực nghiệm. Từ §5, chúng ta xét năng lực thống kê.

## 5. Số tham số, tham số hóa thừa và năng lực thống kê

Để học từ mẫu, chúng ta cần biết lớp mạng lớn tới mức nào. Nếu lớp phân lớp đúng mọi cách gán nhãn của mẫu, lỗi huấn luyện bằng $0$ không phân biệt nhãn mang thông tin với nhãn không mang thông tin. Đại lượng đầu tiên để đo kích thước của lớp là số tham số.

::: definition Định nghĩa 07.4 (Tham số hóa thừa so với một mẫu)
Cho một kiến trúc (Định nghĩa 07.1), trong đó một phần tham số có thể được rút trước mẫu rồi giữ cố định, và một bộ điểm $x_1,\ldots,x_m\in\mathcal X$.

- **Số tham số.** $P$, số tham số được chọn theo dữ liệu; các tham số rút trước mẫu và giữ cố định không được đếm.
- **Tham số hóa thừa.** Kiến trúc được gọi là *tham số hóa thừa* so với cỡ mẫu $m$ nếu $P>m$.
- **Nội suy.** Với nhãn $y_1,\ldots,y_m$, kiến trúc *nội suy* (interpolates) mẫu nếu có tham số $\theta$ với $h_\theta(x_i)=y_i$ cho mọi $i$, tức lỗi huấn luyện 0–1 bằng $0$.
- **Nội suy mọi cách gán nhãn.** Kiến trúc nội suy mọi cách gán nhãn của bộ điểm nếu lớp $\{h_\theta\}$ tách trọn bộ $(x_1,\ldots,x_m)$ (Định nghĩa 03.2).
:::

Tham số hóa thừa là một phép đếm, không phụ thuộc các điểm hay nhãn nhưng phụ thuộc $m$: cùng kiến trúc là tham số hóa thừa với $m=200$, không với $m=10^5$. Nội suy và nội suy mọi cách gán nhãn là tính chất của lớp trên một bộ điểm. Mạng của câu hỏi mở đầu có $P=2000>m=200$ và nội suy mọi cách gán nhãn của mẫu (ví dụ cuối mục).

Hai lớp của Nhận xét 03.10 tách hai khái niệm: $\mathcal H_{\sin}$ có $P=1$ nhưng tách trọn những bộ điểm lớn tùy ý; lớp ở (iii) có $P=p$ tùy ý lớn nhưng chỉ gồm ba hàm, cho các nhãn $(0,1)$, $(1,0)$, $(1,1)$ trên hai điểm $x_1<0<x_2$ mà không cho $(0,0)$. Tham số hóa thừa không kéo theo nội suy, và nội suy không cần tham số hóa thừa.

Một bảo đảm học có thể nói về một lớp hay về riêng hàm mà phép huấn luyện chọn.

::: definition Định nghĩa 07.5 (Lớp kiến trúc, lớp con bị chặn theo chuẩn và mô hình do huấn luyện chọn)
Cho một kiến trúc với độ sâu $J$ và độ rộng $N$; $\theta\in\mathbb R^P$ gồm các tham số được chọn theo dữ liệu, còn tham số cố định trước mẫu giữ nguyên giá trị. Cho thêm một chuẩn $\lVert\cdot\rVert$ trên $\mathbb R^P$, một số $B>0$ và một thuật toán học $A$ có nguồn ngẫu nhiên riêng $\xi$ (Định nghĩa 05.18).

- **Lớp kiến trúc.** $\mathcal H_{J,N}=\{h_\theta:\theta\in\mathbb R^P\}$ và $\mathcal F_{J,N}=\{f_\theta:\theta\in\mathbb R^P\}$, *lớp kiến trúc* (architecture class) của hàm phân lớp và của hàm điểm số; cố định trước mẫu.
- **Lớp con bị chặn theo chuẩn.** $\mathcal H_{J,N}(B)=\{h_\theta:\lVert\theta\rVert\le B\}$, một *lớp con bị chặn theo chuẩn* (norm-bounded class); cố định trước mẫu khi $B$ được chọn trước mẫu.
- **Mô hình do huấn luyện chọn.** $\hat\theta=A(S;\xi)$ và hàm $h_{\hat\theta}$, *mô hình do huấn luyện chọn* (model selected by training); ngẫu nhiên, phụ thuộc $S$.
:::

Bảo đảm cấp lớp (Bài 02–03, §7) đúng đồng thời cho mọi hàm của một lớp cố định trước mẫu, nên đúng cho $h_{\hat\theta}$ mỗi khi $h_{\hat\theta}$ thuộc lớp (với lớp con: khi $\lVert\hat\theta\rVert\le B$), bất kể thuật toán. Bảo đảm này không nói thuật toán chọn hàm nào; đó là việc của bảo đảm cấp thuật toán, như ở Bài 06.

Lớp $\{h_\theta:\lVert\theta\rVert\le\lVert\hat\theta\rVert\}$ có bán kính phụ thuộc $S$; dùng nó như một lớp chọn trước mẫu lặp lại lỗi của Ví dụ 03.8 và Ví dụ 04.10 (cách xử lý đúng ở §9). Một hàm có thể có nhiều véc-tơ tham số với chuẩn khác nhau, như ví dụ sau.

::: example Ví dụ 07.2 (Đổi tỉ lệ hai lớp nơ-ron kề nhau của mạng biểu diễn phép hoặc loại trừ)
**Thiết lập.** Mạng của Mệnh đề 07.2. Với $c>0$, thay $\Theta_1$, $b_1$ bằng $c\Theta_1$, $cb_1$ và $\Theta_2$ bằng $\Theta_2/c$, giữ $b_2=-\tfrac12$; đây là phép *đổi tỉ lệ* (rescaling) hai lớp nơ-ron kề nhau.

**Bước 1: tính thuần nhất dương.** Với $c>0$, $\operatorname{ReLU}(ct)=c\operatorname{ReLU}(t)$; đây là *tính thuần nhất dương* (positive homogeneity).

**Bước 2: hàm không đổi.** Áp dụng Bước 1 cho từng tọa độ, với mọi $x\in\mathbb R^2$,
$$
\begin{aligned}
&\tfrac1c\Theta_2\operatorname{ReLU}(c\Theta_1x+cb_1)\\
&=\tfrac1c\Theta_2\,c\operatorname{ReLU}(\Theta_1x+b_1)\\
&=\Theta_2\operatorname{ReLU}(\Theta_1x+b_1).
\end{aligned}
$$
Cộng $b_2$, mạng mới có cùng hàm điểm số trên $\mathbb R^2$.

**Bước 3: tổng bình phương các tham số.** Với *chuẩn Frobenius* $\lVert\Theta\rVert_F$ (căn của tổng bình phương các phần tử),
$$
\begin{aligned}
&\lVert c\Theta_1\rVert_F^2+\lVert cb_1\rVert^2\\
&=c^2(4+1)=5c^2,\\
&\lVert\Theta_2/c\rVert^2=(1+4)/c^2=5/c^2,
\end{aligned}
$$
và $b_2^2=\tfrac14$. Tổng $5c^2+5/c^2+\tfrac14$ bằng $10{,}25$ tại $c=1$ (nhỏ nhất, theo bất đẳng thức trung bình cộng–trung bình nhân) và $500{,}30$ tại $c=10$ hay $c=0{,}1$.

**Bước 4: tích các chuẩn phổ.** *Chuẩn phổ* (spectral norm) của ma trận $\Theta$ là $\lVert\Theta\rVert_{\mathrm{op}}=\max_{\lVert u\rVert=1}\lVert\Theta u\rVert$. Theo Cauchy–Schwarz, với $\lVert u\rVert=1$, $\lVert\Theta_1u\rVert=\sqrt2\,\lvert u_1+u_2\rvert\le2$ và $\lVert\Theta_2u\rVert=\lvert u_1-2u_2\rvert\le\sqrt5$, với dấu bằng khi $u$ cùng hướng $(1,1)$ hay $(1,-2)$. Do đó
$$
\begin{aligned}
\lVert c\Theta_1\rVert_{\mathrm{op}}&=2c,\\
\lVert\Theta_2/c\rVert_{\mathrm{op}}&=\sqrt5/c,
\end{aligned}
$$
nên tích hai chuẩn phổ bằng $2\sqrt5\approx4{,}4721$ với mọi $c>0$.

**Kết luận.** Cùng một hàm có véc-tơ tham số với chuẩn Euclid $\sqrt{10{,}25}\approx3{,}20$ và với chuẩn $\sqrt{500{,}30}\approx22{,}37$, nên chuẩn của toàn bộ véc-tơ tham số không xác định được từ hàm. Một đại lượng gắn với hàm phải bất biến khi đổi tỉ lệ, như tích các chuẩn phổ.
:::

::: example Ví dụ 07.3 (Lớp kiến trúc của thí nghiệm mở đầu)
**Thiết lập.** Cho $p=2$, $\mathcal X=\{x:\lVert x\rVert\le1\}$, $J=2$, $N=2000$, ReLU. Hàng thứ $j$ của $\Theta_1$ là $v_j^\top$, với $v_j$ đều trên đường tròn đơn vị, và tọa độ $b_{1j}$ của $b_1$ đều trên $[-1,1]$; lớp ẩn rút độc lập với $S$ rồi cố định. Đặt
$$
\chi(x)=\frac{\operatorname{ReLU}(\Theta_1x+b_1)}{\sqrt N},
$$
véc-tơ *đặc trưng ngẫu nhiên* (random features) của $x$ trong $\mathbb R^N$. Lớp ra có $\Theta_2=w^\top/\sqrt N$, $w\in\mathbb R^N$, $b_2=0$, nên $f_\theta(x)=\langle w,\chi(x)\rangle$ và $\lVert\Theta_2\rVert=\lVert w\rVert/\sqrt N$; chuẩn được báo trong bài là $\lVert w\rVert$. Mẫu $S$ là mẫu của câu hỏi mở đầu, $m=200$.

**Bước 1: ba đối tượng của Định nghĩa 07.5.** Tham số được chọn là $w$, nên $P=N$. Với lớp ẩn cố định, lớp kiến trúc $\mathcal H_{2,2000}$ là lớp nửa không gian thuần nhất $x\mapsto\mathbb 1[\langle w,\chi(x)\rangle\ge0]$; lớp con ứng với $\lVert w\rVert\le B$. Mô hình do huấn luyện chọn là *nghiệm nội suy chuẩn nhỏ nhất* (minimum-norm interpolant) $\hat w$, có chuẩn nhỏ nhất trong các $w$ thỏa $\langle w,\chi(x_i)\rangle=\tilde y_i$ với mọi $i$ (Phụ lục D).

**Bước 2: đếm.** Có $P=2000$ tham số được huấn luyện; $6000$ tham số lớp ẩn và $b_2=0$ cố định. Tỉ số $P/m=10$: kiến trúc tham số hóa thừa.

**Bước 3: nội suy mọi cách gán nhãn.** Trong cả mười lần chạy, ma trận $200\times2000$ với các hàng $\chi(x_i)^\top$ có hạng $200$ (Phụ lục D), nên theo lập luận của câu ôn nhanh 2, lớp tách trọn $200$ điểm huấn luyện. Chiều VC thỏa $d\ge m$, và $d\le N$ theo Mệnh đề 03.9(b).

**Bước 4: cận VC.** Lặp mỗi điểm huấn luyện hai lần cho một bộ $2m$ điểm. Hai bản sao của một điểm nhận cùng nhãn, nên trên bộ này lớp thực hiện đúng $2^m$ cách gán nhãn và $\Pi_{\mathcal H_{2,2000}}(2m)\ge2^m$. Thay vào bán kính VC của Định lý 03.15, vì $4/\delta>1$,
$$
\begin{aligned}
\rho_m&=\sqrt{8\ln\big(4\Pi(2m)/\delta\big)/m}\\
&\ge\sqrt{8\ln2}\approx2{,}35>1,
\end{aligned}
$$
nên định lý không cho thông tin.

**Kết luận.** Số tham số, chiều VC và bán kính VC như nhau cho nhãn thật và nhãn hoán vị.
:::

::: remark Nhận xét 07.6 (Chiều VC của lớp mạng ngưỡng) — đọc thêm
Với hàm kích hoạt dấu và $P$ trọng số được huấn luyện (kể cả hệ số tự do), hàm tăng trưởng của lớp mạng không quá $(em)^P$, nên chiều VC là $O(P\ln P)$ (UML §20.4; Bài tập 07.7, 07.8). Cận chỉ phụ thuộc đồ thị của mạng, nên không phân biệt nhãn thật với nhãn hoán vị.
:::

Chúng ta cần một đại lượng xác định cho cả lớp hàm giá trị thực, như lớp hàm điểm số và lớp hàm lỗi, và nhỏ đi khi lớp bị chặn theo chuẩn.

## 6. Độ phức tạp Rademacher

Bước 2 của chứng minh Định lý 03.15 đưa vào các dấu ngẫu nhiên $\sigma_i$, và Bước 3 đếm các cách gán nhãn trên mẫu gộp. Với lớp hàm giá trị thực, không còn phép đếm như vậy; ta đo mức tương quan lớn nhất mà lớp đạt được với một bộ dấu ngẫu nhiên. Từ đây, các dấu ngẫu nhiên của Bài 03 được gọi là biến Rademacher.

::: definition Định nghĩa 07.7 (Độ phức tạp Rademacher)
Cho $m\ge1$, một tập $\Omega$ và một lớp $\mathcal F$ các hàm $\Omega\to\mathbb R$; $\Omega$ là $\mathcal X$ khi $\mathcal F$ là lớp hàm điểm số, và là $\mathcal Z$ khi $\mathcal F$ là lớp hàm lỗi. Định nghĩa gồm bốn thành phần.

- **Biến Rademacher.** $\sigma=(\sigma_1,\ldots,\sigma_m)$, các *biến Rademacher* (Rademacher variables): độc lập với nhau và với mọi đại lượng khác, nhận $\pm1$ với xác suất $\tfrac12$.
- **Tập véc-tơ.** Với $A\subset\mathbb R^m$ khác rỗng, bị chặn,
  $$
  \begin{aligned}
  &\widehat{\mathfrak R}(A)\\
  &=\mathbb E_\sigma\Big[\sup_{a\in A}\tfrac1m\textstyle\sum_{i=1}^m\sigma_ia_i\Big].
  \end{aligned}
  $$
- **Độ phức tạp thực nghiệm.** Với bộ điểm cố định $\omega_{1:m}=(\omega_1,\ldots,\omega_m)\in\Omega^m$, đặt $\mathcal F\circ\omega_{1:m}=\{(f(\omega_1),\ldots,f(\omega_m)):f\in\mathcal F\}$. Khi tập này bị chặn,
  $$
  \begin{aligned}
  &\widehat{\mathfrak R}_{\omega_{1:m}}(\mathcal F)\\
  &=\widehat{\mathfrak R}(\mathcal F\circ\omega_{1:m})\\
  &=\mathbb E_\sigma\Big[\sup_{f\in\mathcal F}\tfrac1m\textstyle\sum_i\sigma_if(\omega_i)\Big]
  \end{aligned}
  $$
  là *độ phức tạp Rademacher thực nghiệm* (empirical Rademacher complexity) của $\mathcal F$ trên bộ điểm. Khi bộ điểm là mẫu $S$ (với lớp hàm điểm số: các đầu vào $X_1,\ldots,X_m$), ta viết $\widehat{\mathfrak R}_S(\mathcal F)$.
- **Độ phức tạp tổng thể.** $\mathfrak R_m(\mathcal F)=\mathbb E_{S\sim D^m}\widehat{\mathfrak R}_S(\mathcal F)$, *độ phức tạp Rademacher tổng thể* (population Rademacher complexity), khi $\widehat{\mathfrak R}_S(\mathcal F)$ là một biến ngẫu nhiên đo được (§7).
:::

Độ phức tạp thực nghiệm còn ngẫu nhiên theo $S$; với lớp hàm điểm số, nó không phụ thuộc nhãn. Với mỗi bộ dấu, ta chọn hàm tương quan nhiều nhất với các dấu, rồi mới lấy kì vọng theo $\sigma$. Hai cận đơn giản là
$$
0\le\widehat{\mathfrak R}(A)\le\sup_{a\in A}\max_i\lvert a_i\rvert .
$$
Vế trái đúng vì cận trên đúng không nhỏ hơn giá trị tại một $a\in A$ cố định, có kì vọng $0$; vế phải vì $\frac1m\sum_i\sigma_ia_i\le\max_i\lvert a_i\rvert$. Định nghĩa không có trị tuyệt đối, như UML; quy ước dùng $\mathbb E\sup\lvert\cdot\rvert$ cho kết quả khác ở lớp một phần tử (Bài tập 07.2).

Đại lượng $\sup_{f\in\mathcal F}\frac1m\sum_i\tilde y_if(x_i)$, với nhãn thật $\tilde y_i$, đo mức lớp khớp với nhãn của bài toán, nên không phải độ phức tạp Rademacher; độ phức tạp này dùng dấu độc lập với dữ liệu và đo riêng khả năng khớp của lớp.

Bổ đề sau, dùng ở §7–§8, cho biết độ phức tạp đổi thế nào khi cộng hằng số, đổi dấu hay nhân với một số.

::: lemma Bổ đề 07.8 (Độ phức tạp Rademacher qua một phép biến đổi afin) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Tập.** $A\subset\mathbb R^m$ khác rỗng, bị chặn.
- **Hệ số.** $c\in\mathbb R$.
- **Véc-tơ dịch.** $\bar a=(\bar a_1,\ldots,\bar a_m)\in\mathbb R^m$.

**Bảo đảm.** Tất định: với $cA+\bar a=\{ca+\bar a:a\in A\}$,
$$
\widehat{\mathfrak R}(cA+\bar a)=\lvert c\rvert\,\widehat{\mathfrak R}(A).
$$
:::

::: proof Chứng minh Bổ đề 07.8
**Lộ trình.** Tách số hạng dịch ra khỏi cận trên đúng, rồi xét dấu của $c$.

**Bước 1 (số hạng dịch).** Với mỗi $\sigma$,
$$
\begin{aligned}
&\sup_{a\in A}\tfrac1m\textstyle\sum_i\sigma_i(ca_i+\bar a_i)\\
&=\sup_{a\in A}\tfrac1m\textstyle\sum_i\sigma_ica_i+\tfrac1m\textstyle\sum_i\sigma_i\bar a_i .
\end{aligned}
$$
Số hạng cuối không phụ thuộc $a$ và có kì vọng $0$. Lấy kì vọng theo $\sigma$, ta được $\widehat{\mathfrak R}(cA+\bar a)=\widehat{\mathfrak R}(cA)$.

**Bước 2 ($c\ge0$).** Nhân với một số không âm giữ nguyên thứ tự, nên $\sup_a c(\cdot)=c\sup_a(\cdot)$, và $\widehat{\mathfrak R}(cA)=c\,\widehat{\mathfrak R}(A)$.

**Bước 3 ($c<0$).** Viết $\sigma_ica_i=\lvert c\rvert(-\sigma_i)a_i$. Véc-tơ $-\sigma$ có cùng phân bố với $\sigma$, nên theo Bước 2,
$$
\begin{aligned}
&\widehat{\mathfrak R}(cA)\\
&=\lvert c\rvert\,\mathbb E\sup_a\tfrac1m\textstyle\sum_i(-\sigma_i)a_i\\
&=\lvert c\rvert\,\widehat{\mathfrak R}(A).
\end{aligned}
$$

$\square$ Cộng hằng số vào hàm lỗi hay đổi dấu nó không đổi độ phức tạp; nhân với $c$ nhân độ phức tạp với $\lvert c\rvert$.
:::

::: example Ví dụ 07.4 (Độ phức tạp Rademacher của bốn lớp trên ba điểm)
**Thiết lập.** Cho $m=3$ và ba điểm phân biệt cố định; mỗi lớp được mô tả bằng tập $A\subset\mathbb R^3$ các véc-tơ giá trị của nó trên ba điểm. Có $8$ bộ dấu đồng khả năng, nên
$$
\begin{aligned}
&\widehat{\mathfrak R}(A)\\
&=\frac18\sum_{\sigma\in\{\pm1\}^3}\max_{a\in A}\frac13\sum_{i=1}^3\sigma_ia_i .
\end{aligned}
$$

**Bước 1: lớp một phần tử.** Với $A=\{(0{,}3;0{,}7;0{,}2)\}$, không có phép chọn, và tổng có dấu có kì vọng $0$, nên $\widehat{\mathfrak R}(A)=0$.

**Bước 2: hai hàm.** Với $A=\{(1,0,0),(0,1,1)\}$, tổng có dấu của hai véc-tơ là $\sigma_1$ và $\sigma_2+\sigma_3$. Cột "Bước 2" của bảng dưới ghi giá trị lớn nhất của hai tổng này theo từng bộ dấu; chẳng hạn với $(-,-,-)$, hai tổng là $-1$ và $-2$.

| $(\sigma_1,\sigma_2,\sigma_3)$ | Bước 2 | Bước 3 |
|---|---|---|
| $(-,-,-)$ | $-1$ | $0$ |
| $(-,-,+)$ | $0$ | $1$ |
| $(-,+,-)$ | $0$ | $0$ |
| $(-,+,+)$ | $2$ | $2$ |
| $(+,-,-)$ | $1$ | $0$ |
| $(+,-,+)$ | $1$ | $1$ |
| $(+,+,-)$ | $1$ | $1$ |
| $(+,+,+)$ | $2$ | $3$ |
| Tổng | $6$ | $8$ |

Tổng cột "Bước 2" bằng $6$, nên $\widehat{\mathfrak R}(A)=6/(8\cdot3)=\tfrac14$.

**Bước 3: lớp hàm ngưỡng.** Trên ba điểm $x_1<x_2<x_3$, lớp hàm ngưỡng của Ví dụ 03.1 tạo ra bốn véc-tơ $(0,0,0)$, $(0,0,1)$, $(0,1,1)$, $(1,1,1)$, với các tổng có dấu $0$, $\sigma_3$, $\sigma_2+\sigma_3$, $\sigma_1+\sigma_2+\sigma_3$. Giá trị lớn nhất của bốn tổng ở cột "Bước 3"; tổng cột bằng $8$, nên $\widehat{\mathfrak R}(A)=8/24=\tfrac13$.

**Bước 4: mọi cách gán nhãn.** Với $A=\{0,1\}^3$, véc-tơ tốt nhất đặt $a_i=1$ đúng tại các $i$ có $\sigma_i=1$, nên giá trị lớn nhất bằng số dấu dương, có kì vọng $\tfrac32$; do đó $\widehat{\mathfrak R}(A)=\tfrac12$.

**Kết luận.** Bốn lớp cho các giá trị $0$, $\tfrac14$, $\tfrac13$, $\tfrac12$.
:::

Giá trị $\tfrac12$ ở Bước 4 là lớn nhất với mọi lớp hàm phân lớp; mệnh đề sau chứng minh điều đó và nối độ phức tạp với lỗi nhỏ nhất khi khớp nhãn ngẫu nhiên.

::: proposition Mệnh đề 07.9 (Độ phức tạp Rademacher và lỗi khớp nhãn ngẫu nhiên) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Điểm.** $x_1,\ldots,x_m\in\mathcal X$ cố định, cho phép lặp.
- **Lớp.** $\mathcal H$ khác rỗng, gồm các hàm $\mathcal X\to\{0,1\}$.
- **Nhãn ngẫu nhiên.** $\tau=(\tau_1,\ldots,\tau_m)$, các *nhãn ngẫu nhiên* (random labels): độc lập, mỗi $\tau_i$ đều trên $\{0,1\}$; lỗi khớp của $h$ là $\operatorname{err}_\tau(h)=\frac1m\sum_i\mathbb 1[h(x_i)\ne\tau_i]$.

**Bảo đảm.** Ba khẳng định tất định; kì vọng chỉ lấy theo $\tau$ hay $\sigma$.

- **(a) Đồng nhất thức.** Lỗi nhỏ nhất dưới đây đạt được, và
  $$
  \begin{aligned}
  &\widehat{\mathfrak R}_{x_{1:m}}(\mathcal H)\\
  &=\tfrac12-\mathbb E_\tau\min_{h\in\mathcal H}\operatorname{err}_\tau(h).
  \end{aligned}
  $$
- **(b) Lớp hàm lỗi.** Với mọi nhãn cố định $y_1,\ldots,y_m\in\{0,1\}$ và $z_i=(x_i,y_i)$, lớp hàm lỗi 0–1 $\mathcal G=\{(x,y)\mapsto\mathbb 1[h(x)\ne y]:h\in\mathcal H\}$ thỏa $\widehat{\mathfrak R}_{z_{1:m}}(\mathcal G)=\widehat{\mathfrak R}_{x_{1:m}}(\mathcal H)$, không phụ thuộc nhãn.
- **(c) Giá trị lớn nhất.** $\widehat{\mathfrak R}_{x_{1:m}}(\mathcal H)\le\tfrac12$, với dấu bằng khi và chỉ khi $\mathcal H$ tách trọn bộ $(x_1,\ldots,x_m)$.
:::

::: proof Chứng minh Mệnh đề 07.9
**Lộ trình.** Viết mỗi dấu qua một nhãn ngẫu nhiên, rồi đổi cận trên đúng thành giá trị nhỏ nhất của lỗi.

**Bước 1 (đổi biến).** Đặt $\tau_i=(1+\sigma_i)/2$; các $\tau_i$ độc lập, đều trên $\{0,1\}$. Với $h_i\in\{0,1\}$,
$$
\sigma_ih_i=\tau_i-\mathbb 1[h_i\ne\tau_i].
$$
Bốn trường hợp kiểm trực tiếp: với $(\tau_i,h_i)=(1,1),(1,0),(0,1),(0,0)$, hai vế lần lượt bằng $1$, $0$, $-1$, $0$.

**Bước 2 (phần a).** Lấy $h_i=h(x_i)$ và trung bình theo $i$:
$$
\begin{aligned}
&\tfrac1m\textstyle\sum_i\sigma_ih(x_i)\\
&=\tfrac1m\textstyle\sum_i\tau_i\\
&\quad-\tfrac1m\textstyle\sum_i\mathbb 1[h(x_i)\ne\tau_i].
\end{aligned}
$$
Số hạng đầu không phụ thuộc $h$, nên cận trên đúng theo $h$ bằng $\tfrac1m\sum_i\tau_i$ trừ lỗi nhỏ nhất, đạt được vì $\mathcal H\circ x_{1:m}\subseteq\{0,1\}^m$ hữu hạn. Lấy kì vọng và dùng $\mathbb E\tau_i=\tfrac12$, ta được (a).

**Bước 3 (phần b).** Với $h(x),y\in\{0,1\}$, $\mathbb 1[h(x)\ne y]=h(x)+y-2h(x)y$. Do đó
$$
\begin{aligned}
&\sigma_i\mathbb 1[h(x_i)\ne y_i]\\
&=\sigma_iy_i+\sigma_i(1-2y_i)h(x_i).
\end{aligned}
$$
Số hạng $\sigma_iy_i$ không phụ thuộc $h$ và có kì vọng $0$. Vì $1-2y_i\in\{\pm1\}$ cố định, $\sigma'_i=\sigma_i(1-2y_i)$ lại là các biến Rademacher, nên $\widehat{\mathfrak R}_{z_{1:m}}(\mathcal G)=\mathbb E\sup_h\frac1m\sum_i\sigma'_ih(x_i)=\widehat{\mathfrak R}_{x_{1:m}}(\mathcal H)$.

**Bước 4 (phần c).** Lỗi nhỏ nhất không âm, nên theo (a), $\widehat{\mathfrak R}_{x_{1:m}}(\mathcal H)\le\tfrac12$. Mỗi giá trị của $\tau$ có xác suất $2^{-m}>0$, nên dấu bằng xảy ra khi và chỉ khi lỗi nhỏ nhất bằng $0$ với mọi $\tau\in\{0,1\}^m$, tức lớp thực hiện mọi cách gán nhãn của bộ điểm.

Với lớp các hàm nhận giá trị $\pm1$, bốn trường hợp tương tự cho $\sigma_ih_i=1-2\cdot\mathbb 1[h_i\ne\sigma_i]$, nên trong (a), hằng số $\tfrac12$ thành $1$, hệ số của lỗi thành $2$, và nhãn ngẫu nhiên là $\sigma_i$.

$\square$ Độ phức tạp Rademacher của lớp hàm lỗi 0–1 đo mức lớp khớp được những nhãn không mang thông tin trên chính các điểm của mẫu.
:::

::: example Ví dụ 07.5 (Lớp khớp mọi cách gán nhãn)
**Thiết lập.** Hai lớp hàm phân lớp trên các bộ điểm cố định; chỉ nhãn ngẫu nhiên $\tau$ là ngẫu nhiên.

**Bước 1: lớp kiến trúc của thí nghiệm.** Theo Ví dụ 07.3, lớp $\mathcal H_{2,2000}$ tách trọn $200$ điểm huấn luyện, nên theo Mệnh đề 07.9(c), độ phức tạp Rademacher thực nghiệm của nó trên các điểm này bằng $\tfrac12$. Theo (b), lớp hàm lỗi 0–1 có cùng giá trị với nhãn thật và với nhãn hoán vị.

**Bước 2: một tham số.** Lớp $\mathcal H_{\sin}$ của Nhận xét 03.10(ii) có $P=1$ và tách trọn $\{2^{-1},\ldots,2^{-m}\}$ với mọi $m$, nên theo Mệnh đề 07.9(c), độ phức tạp của nó trên các điểm này bằng $\tfrac12$.

**Kết luận.** Số tham số không chặn trên, cũng không chặn dưới, độ phức tạp Rademacher (như Nhận xét 03.10 cho chiều VC); ở §8, một lớp với $10^5$ tham số nhưng chuẩn bị chặn có độ phức tạp nhỏ.
:::

## 7. Cận tổng quát hóa theo độ phức tạp Rademacher

Chúng ta cần chứng minh rằng độ phức tạp Rademacher chặn khoảng cách tổng quát hóa của mọi hàm trong một lớp hàm lỗi chọn trước mẫu. Bước 1 của chứng minh Định lý 03.15 dùng bất đẳng thức Chebyshev để đưa vào mẫu bóng, và Bước 4 dùng bất đẳng thức Hoeffding cho từng cách gán nhãn. Với lớp hàm lỗi giá trị thực, ta lấy kì vọng thay cho xác suất ở Bước 1, rồi cần một bất đẳng thức tập trung cho chính cận trên đúng theo lớp. Cận trên đúng này không phải trung bình của các biến độc lập, nên bất đẳng thức Hoeffding không áp dụng trực tiếp.

::: lemma Bổ đề 07.10 (Bất đẳng thức McDiarmid) — phác thảo (chứng minh ở Phụ lục A)
**Giả thiết.** Ba thành phần sau.

- **Biến.** $V_1,\ldots,V_m$ độc lập, $V_i$ nhận giá trị trong một tập $\mathcal V_i$, không cần cùng phân bố.
- **Hàm.** $Q:\mathcal V_1\times\cdots\times\mathcal V_m\to\mathbb R$ đo được.
- **Sai phân bị chặn.** Có $c_1,\ldots,c_m\ge0$ sao cho $\lvert Q(v)-Q(v')\rvert\le c_i$ khi hai bộ $v$, $v'$ chỉ khác nhau ở tọa độ thứ $i$.

**Bảo đảm.** Với xác suất lấy theo $V=(V_1,\ldots,V_m)$ và mọi $t>0$,
$$
\begin{aligned}
&\Pr\big(Q(V)-\mathbb EQ(V)\ge t\big)\\
&\quad\le\exp\big(-2t^2/\textstyle\sum_ic_i^2\big),
\end{aligned}
$$
và cùng cận đúng cho $\Pr\big(Q(V)-\mathbb EQ(V)\le-t\big)$.
:::

Bổ đề được gọi là *bất đẳng thức McDiarmid* (McDiarmid's inequality, còn gọi là bất đẳng thức sai phân bị chặn); giả thiết thứ ba là *điều kiện sai phân bị chặn* (bounded differences condition). Với $Q$ là trung bình của $m$ biến trong $[a,b]$, $c_i=(b-a)/m$ và bổ đề cho đúng Định lý 02.7(a), (b); ở đây $Q$ có thể là một cận trên đúng theo một lớp. Chứng minh (Phụ lục A) dùng bổ đề Hoeffding có điều kiện cho từng bước tăng của $Q-\mathbb EQ$.

Với một hàm $g:\mathcal Z\to[0,1]$, ta viết $L_D(g)=\mathbb E_{Z\sim D}\,g(Z)$ và $L_S(g)=\frac1m\sum_{i=1}^mg(Z_i)$; khi $g=\ell(h,\cdot)$, đây là $L_D(h)$ và $L_S(h)$.

::: theorem Định lý 07.11 (Cận tổng quát hóa theo độ phức tạp Rademacher thực nghiệm) — phác thảo (bất đẳng thức McDiarmid chứng minh ở Phụ lục A)
**Giả thiết.** Ba thành phần sau.

- **Mẫu.** $S=(Z_1,\ldots,Z_m)\sim D^m$ theo (T1).
- **Lớp hàm lỗi.** $\mathcal G$ gồm các hàm đo được $g:\mathcal Z\to[0,1]$, cố định trước mẫu, và thỏa (M): có một lớp con đếm được $\mathcal G_0\subseteq\mathcal G$ sao cho mỗi $g\in\mathcal G$ là giới hạn theo từng điểm của một dãy trong $\mathcal G_0$.
- **Tham số.** $\delta\in(0,1)$.

**Bảo đảm.** Xác suất và kì vọng lấy theo $S\sim D^m$.

- **(a) Theo kì vọng.**
  $$
  \begin{aligned}
  &\mathbb E_S\sup_{g\in\mathcal G}\big(L_D(g)-L_S(g)\big)\\
  &\le2\,\mathfrak R_m(\mathcal G).
  \end{aligned}
  $$
- **(b) Với xác suất cao.** Với xác suất ít nhất $1-\delta$, đồng thời cho mọi $g\in\mathcal G$,
  $$
  \begin{aligned}
  L_D(g)\le{}&L_S(g)+2\widehat{\mathfrak R}_S(\mathcal G)\\
  &+3\sqrt{\frac{\ln(2/\delta)}{2m}} .
  \end{aligned}
  $$

Vế phải của (b) tính được từ chính mẫu, nên (b) là một *cận phụ thuộc dữ liệu* (data-dependent bound). Bảo đảm là cấp lớp; cận phụ thuộc $\delta$ qua $\ln(2/\delta)$, không phụ thuộc trực tiếp vào $p$.
:::

::: proof Chứng minh Định lý 07.11
**Lộ trình.** Đặt $\Psi(S)=\sup_{g\in\mathcal G}\big(L_D(g)-L_S(g)\big)$. Ta chặn $\mathbb E\Psi$ bằng mẫu bóng và biến Rademacher, chứng minh $\Psi$ và $\widehat{\mathfrak R}_S(\mathcal G)$ có sai phân bị chặn $1/m$, rồi dùng bất đẳng thức McDiarmid hai lần. Bất đẳng thức then chốt là $\mathbb E\Psi\le2\,\mathfrak R_m(\mathcal G)$.

**Bước 0 (tính đo được; (M)).** Như đoạn trước Nhận xét 03.14, (M) và định lý hội tụ bị chặn cho phép thay cận trên đúng theo $\mathcal G$ bằng cận trên đúng theo $\mathcal G_0$ đếm được (Phụ lục C). Do đó $\Psi(S)\in[-1,1]$ và $\widehat{\mathfrak R}_S(\mathcal G)\in[0,1]$ là các biến ngẫu nhiên đo được.

**Bước 1 (mẫu bóng; (T1) và lớp cố định trước mẫu).** Lấy mẫu bóng $S'=(Z'_1,\ldots,Z'_m)\sim D^m$ độc lập với $S$. Vì $\mathcal G$ không phụ thuộc $S$, Mệnh đề 01.7 cho $L_D(g)=\mathbb E_{S'}L_{S'}(g)$ với mỗi $g$. Cận trên đúng của kì vọng không quá kì vọng của cận trên đúng, nên
$$
\begin{aligned}
&\Psi(S)\\
&=\sup_g\mathbb E_{S'}\big[L_{S'}(g)-L_S(g)\big]\\
&\le\mathbb E_{S'}\sup_g\big(L_{S'}(g)-L_S(g)\big).
\end{aligned}
$$
Lấy kì vọng theo $S$ (định lý Fubini), $\mathbb E\Psi$ không quá kì vọng theo $(S,S')$ của $\sup_g\frac1m\sum_i\big(g(Z'_i)-g(Z_i)\big)$.

**Bước 2 (đổi chỗ với biến Rademacher; (T1)).** Với mỗi bộ dấu cố định, đổi chỗ $Z_i\leftrightarrow Z'_i$ tại các $i$ có $\sigma_i=-1$ không làm đổi phân bố của $(S,S')$ (Phụ lục C). Do đó kì vọng ở cuối Bước 1 bằng kì vọng của $\sup_g\frac1m\sum_i\sigma_i\big(g(Z'_i)-g(Z_i)\big)$, với $\sigma$ độc lập với $(S,S')$. Tách cận trên đúng của một tổng thành tổng hai cận trên đúng:
$$
\begin{aligned}
\mathbb E\Psi&\le\mathbb E\sup_g\tfrac1m\textstyle\sum_i\sigma_i\big(g(Z'_i)\\
&\qquad-g(Z_i)\big)\\
&\le\mathbb E\sup_g\tfrac1m\textstyle\sum_i\sigma_ig(Z'_i)\\
&\quad+\mathbb E\sup_g\tfrac1m\textstyle\sum_i(-\sigma_i)g(Z_i)\\
&=2\,\mathfrak R_m(\mathcal G),
\end{aligned}
$$
vì $-\sigma$ có cùng phân bố với $\sigma$ và $S'$ có cùng phân bố với $S$. Đây là phần (a); khác Bài 03, không cần bất đẳng thức Chebyshev hay phép đếm.

**Bước 3 (sai phân bị chặn; giá trị trong $[0,1]$).** Coi $\Psi$ và $\widehat{\mathfrak R}$ là hàm của mẫu $s$, và gọi $s^{(i)}$ là mẫu thu được khi thay $z_i$ bằng $z'$ (như Bài 06). Vì $g$ nhận giá trị trong $[0,1]$, mỗi $L_s(g)$ và mỗi tổng $\frac1m\sum_i\sigma_ig(z_i)$ đổi không quá $1/m$. Cận trên đúng của một họ hàm, mỗi hàm đổi không quá $1/m$, cũng đổi không quá $1/m$ (Phụ lục C), nên $\Psi$ và $\widehat{\mathfrak R}_s(\mathcal G)$ có sai phân không quá $1/m$: $c_i=1/m$ và $\sum_ic_i^2=1/m$.

**Bước 4 (hai lần bất đẳng thức McDiarmid; (T1) cho tính độc lập).** Đặt $t=\sqrt{\ln(2/\delta)/(2m)}$; khi đó $\exp\big(-2t^2/\sum_ic_i^2\big)=e^{-2mt^2}=\delta/2$. Theo đuôi trên của Bổ đề 07.10 cho $\Psi$, với xác suất ít nhất $1-\delta/2$, $\Psi\le\mathbb E\Psi+t$. Theo đuôi dưới cho $\widehat{\mathfrak R}_S(\mathcal G)$, có kì vọng $\mathfrak R_m(\mathcal G)$, với xác suất ít nhất $1-\delta/2$, $\mathfrak R_m(\mathcal G)\le\widehat{\mathfrak R}_S(\mathcal G)+t$. Theo bất đẳng thức hợp (Bổ đề 02.12), cả hai đúng với xác suất ít nhất $1-\delta$, và khi đó, theo Bước 2,
$$
\begin{aligned}
\Psi&\le2\,\mathfrak R_m(\mathcal G)+t\\
&\le2\widehat{\mathfrak R}_S(\mathcal G)+3t .
\end{aligned}
$$
Với mọi $g\in\mathcal G$, $L_D(g)-L_S(g)\le\Psi$, nên ta được (b).

$\square$ Khoảng cách tổng quát hóa của mọi hàm trong lớp, kể cả hàm chọn theo mẫu, được chặn bởi mức lớp tương quan với dấu ngẫu nhiên trên chính mẫu đó.
:::

Hằng số $3$ đến từ hai lần dùng bất đẳng thức McDiarmid một phía, mỗi lần với xác suất thất bại $\delta/2$: một lần cho $\Psi$, một lần để thay độ phức tạp tổng thể bằng độ phức tạp thực nghiệm. Hằng số của UML §26.1 khác (§13).

::: example Ví dụ 07.6 (Cận của Định lý 07.11 bằng số)
**Thiết lập.** Cho $\delta=0{,}05$, nên $\ln(2/\delta)=\ln40\approx3{,}6889$.

**Bước 1: số hạng tin cậy.** Với $m=200$, $3\sqrt{\ln40/(2m)}=3\sqrt{\ln40/400}\approx0{,}2881$ (câu ôn nhanh 3). Cùng cách tính, làm tròn lên, cho $0{,}0815$ và $0{,}0408$ khi $m=2500$ và $m=10^4$.

**Bước 2: lớp kiến trúc của thí nghiệm, nhãn thật.** Lấy $\mathcal G$ là lớp hàm lỗi 0–1 của $\mathcal H_{2,2000}$, với lớp ẩn cố định trước mẫu. Trên mỗi mẫu mà lớp tách trọn các điểm huấn luyện (cả mười lần chạy), nghiệm nội suy có $L_S=0$ và $\widehat{\mathfrak R}_S(\mathcal G)=\tfrac12$ (Ví dụ 07.5, Bước 1), nên vế phải của Định lý 07.11(b) là
$$
0+2\cdot\tfrac12+0{,}2881=1{,}2881 .
$$
Vế phải lớn hơn $1$, giá trị lớn nhất của rủi ro 0–1, nên đây là một *cận không cho thông tin* (vacuous bound), đúng tầm thường trên các mẫu đó mà không cần kiểm (M).

**Bước 3: nhãn hoán vị.** Các cặp $(x_i,y_i)$ của mẫu hoán vị không độc lập (tổng các nhãn hoán vị bằng tổng các nhãn thật), nên (T1) không thỏa và định lý không áp dụng; vế phải $1{,}2881$ chỉ để so sánh.

**Kết luận.** Với lớp kiến trúc, cận không cho thông tin; chúng ta cần một lớp nhỏ hơn mà vẫn chứa hàm do huấn luyện chọn.
:::

::: remark Nhận xét 07.12 (Cận hai phía)
Lớp $1-\mathcal G=\{1-g:g\in\mathcal G\}$ cũng thỏa các giả thiết của Định lý 07.11. Theo Bổ đề 07.8 với $c=-1$ và $\bar a=(1,\ldots,1)$, $\widehat{\mathfrak R}_S(1-\mathcal G)=\widehat{\mathfrak R}_S(\mathcal G)$. Áp dụng Định lý 07.11(b) cho $\mathcal G$ và cho $1-\mathcal G$, mỗi lần với $\delta/2$, rồi dùng bất đẳng thức hợp: với xác suất ít nhất $1-\delta$, đồng thời cho mọi $g\in\mathcal G$,
$$
\begin{aligned}
&\lvert L_D(g)-L_S(g)\rvert\\
&\le2\widehat{\mathfrak R}_S(\mathcal G)+3\sqrt{\frac{\ln(4/\delta)}{2m}} .
\end{aligned}
$$
:::

Định lý 07.11 đưa câu hỏi về khoảng cách tổng quát hóa của một lớp về độ phức tạp Rademacher của lớp hàm lỗi.

## 8. Lớp tuyến tính bị chặn theo chuẩn và lề phân lớp

Theo Ví dụ 07.6, chúng ta cần một lớp có độ phức tạp Rademacher nhỏ. Lớp hàm điểm số tuyến tính với véc-tơ trọng số trong một quả cầu là một lớp tính được đại lượng này bằng bất đẳng thức Cauchy–Schwarz; với lớp ẩn cố định, lớp ra của mạng trong thí nghiệm là một lớp như vậy trên véc-tơ đặc trưng.

::: proposition Mệnh đề 07.13 (Độ phức tạp Rademacher của lớp tuyến tính bị chặn theo chuẩn) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Lớp.** $\mathcal F_B=\{h_w:w\in\mathbb R^p,\ \lVert w\rVert\le B\}$, với $h_w(x)=\langle w,x\rangle$, chuẩn Euclid và $B>0$.
- **Điểm.** $x_1,\ldots,x_m\in\mathbb R^p$ cố định.
- **Cận dữ liệu.** $\lVert x_i\rVert\le C_x$ với mọi $i$; chỉ dùng cho bất đẳng thức thứ hai.

**Bảo đảm.** Tất định; kì vọng chỉ lấy theo $\sigma$:
$$
\begin{aligned}
&\widehat{\mathfrak R}_{x_{1:m}}(\mathcal F_B)\\
&\le\frac Bm\sqrt{\textstyle\sum_{i=1}^m\lVert x_i\rVert^2}\\
&\le\frac{BC_x}{\sqrt m}.
\end{aligned}
$$
Cận không phụ thuộc $p$, giảm như $1/\sqrt m$ và tỉ lệ với $B$.
:::

::: proof Chứng minh Mệnh đề 07.13
**Lộ trình.** Tính cận trên đúng theo $w$ bằng bất đẳng thức Cauchy–Schwarz, đưa kì vọng vào trong căn bằng bất đẳng thức Jensen, rồi khai triển bình phương. Đặt $v_\sigma=\sum_{i=1}^m\sigma_ix_i\in\mathbb R^p$.

**Bước 1 (Cauchy–Schwarz; quả cầu Euclid).** Với mỗi $\sigma$, $\frac1m\sum_i\sigma_i\langle w,x_i\rangle=\frac1m\langle w,v_\sigma\rangle\le\frac Bm\lVert v_\sigma\rVert$ khi $\lVert w\rVert\le B$, với dấu bằng tại $w=Bv_\sigma/\lVert v_\sigma\rVert$ khi $v_\sigma\ne0$. Do đó
$$
\widehat{\mathfrak R}_{x_{1:m}}(\mathcal F_B)=\frac Bm\,\mathbb E\lVert v_\sigma\rVert .
$$

**Bước 2 (Jensen).** Hàm $t\mapsto\sqrt t$ lõm, nên $\mathbb E\lVert v_\sigma\rVert=\mathbb E\sqrt{\lVert v_\sigma\rVert^2}\le\sqrt{\mathbb E\lVert v_\sigma\rVert^2}$.

**Bước 3 (số hạng chéo; tính độc lập và kì vọng $0$ của $\sigma$).** Vì $\mathbb E[\sigma_i\sigma_j]=0$ với $i\ne j$ và $\sigma_i^2=1$,
$$
\begin{aligned}
\mathbb E\lVert v_\sigma\rVert^2&=\textstyle\sum_{i,j}\mathbb E[\sigma_i\sigma_j]\langle x_i,x_j\rangle\\
&=\textstyle\sum_i\lVert x_i\rVert^2 .
\end{aligned}
$$

**Bước 4 (cận dữ liệu).** Ghép ba bước và dùng $\lVert x_i\rVert\le C_x$:
$$
\begin{aligned}
&\widehat{\mathfrak R}_{x_{1:m}}(\mathcal F_B)\\
&\le\frac Bm\sqrt{\textstyle\sum_i\lVert x_i\rVert^2}\\
&\le\frac Bm\sqrt{mC_x^2}=\frac{BC_x}{\sqrt m}.
\end{aligned}
$$

$\square$ Năng lực của lớp đo bằng tích $BC_x$, không bằng số chiều $p$.
:::

::: example Ví dụ 07.7 (Lớp tuyến tính trên hai điểm trùng nhau và trên bộ điểm trực chuẩn)
**Thiết lập.** Lớp $\mathcal F_B$ của Mệnh đề 07.13 trên hai bộ điểm cố định: $p=1$, $m=2$, $x_1=x_2=1$ (Bước 1); $p=m=4$, $x_i=\mathbf e_i$ là véc-tơ đơn vị thứ $i$ (Bước 2). Theo Bước 1 của chứng minh trên, $\widehat{\mathfrak R}=\frac Bm\,\mathbb E\lVert v_\sigma\rVert$.

**Bước 1: hai điểm $x_1=x_2=1$.** Ở đây $v_\sigma=\sigma_1+\sigma_2$ nhận $2,0,0,-2$ với xác suất bằng nhau, nên $\mathbb E\lvert v_\sigma\rvert=1$ và $\widehat{\mathfrak R}=B/2$, so với cận $B\sqrt2/2\approx0{,}7071B$.

**Bước 2: bộ điểm trực chuẩn.** Ở đây $v_\sigma=(\sigma_1,\ldots,\sigma_4)$ có chuẩn $2$ với mọi $\sigma$, nên Bước 2 của chứng minh là đẳng thức, và
$$
\widehat{\mathfrak R}=\frac B4\cdot2=\frac B2=\frac{B}{\sqrt m},
$$
đúng bằng cận với $C_x=1$.

**Kết luận.** Cận đạt dấu bằng khi các điểm trực chuẩn và lớn hơn giá trị đúng $\sqrt2$ lần với hai điểm trùng nhau.
:::

Để dùng Định lý 07.11 cho phân lớp, cần chuyển độ phức tạp của lớp hàm lỗi về lớp điểm số khi hàm lỗi là hàm Lipschitz của điểm số.

::: lemma Bổ đề 07.14 (Bổ đề co) — phác thảo (chứng minh ở Phụ lục B)
**Giả thiết.** Ba thành phần sau.

- **Tập.** $A\subset\mathbb R^m$ khác rỗng, bị chặn.
- **Hàm.** $\phi_1,\ldots,\phi_m:\mathbb R\to\mathbb R$; mỗi $\phi_i$ là $G$-Lipschitz (Định nghĩa 05.4) trên một tập chứa $\{a_i:a\in A\}$.
- **Ánh xạ theo tọa độ.** $\phi(a)=(\phi_1(a_1),\ldots,\phi_m(a_m))$ và $\phi\circ A=\{\phi(a):a\in A\}$.

**Bảo đảm.** Tất định:
$$
\widehat{\mathfrak R}(\phi\circ A)\le G\,\widehat{\mathfrak R}(A).
$$
:::

Bổ đề được gọi là *bổ đề co* (contraction lemma). Các $\phi_i$ được phép khác nhau theo $i$, nên nhãn của quan sát thứ $i$ có thể nằm trong $\phi_i$. Vì Định nghĩa 07.7 không có trị tuyệt đối, bổ đề không cần *điều kiện định tâm* $\phi_i(0)=0$; với định nghĩa dùng $\mathbb E\sup\lvert\cdot\rvert$, cần thêm điều kiện đó, và dạng này thường được phát biểu với hằng số $2G$ thay cho $G$. Chẳng hạn, với $A=\{0\}\subset\mathbb R^3$ và $\phi_i\equiv1$ ($0$-Lipschitz), Định nghĩa 07.7 cho $0$ trước và sau phép biến đổi, còn bản có trị tuyệt đối cho $0$ trước và $\tfrac13\mathbb E\lvert\sigma_1+\sigma_2+\sigma_3\rvert=0{,}5$ sau (câu ôn nhanh 1).

Chứng minh (Phụ lục B) xử lý từng tọa độ. Hàm lỗi 0–1 không phải hàm Lipschitz của điểm số, nên ta thay nó bằng một hàm lỗi bị chặn, Lipschitz và nằm trên nó.

::: definition Định nghĩa 07.15 (Lề và hàm lỗi dốc)
Cho hàm điểm số $f:\mathcal X\to\mathbb R$, quan sát $z=(x,y)$ với $\tilde y=2y-1$, và $\gamma>0$. Định nghĩa gồm bốn thành phần.

- **Lề.** $\tilde y\,f(x)$, *lề* của $f$ tại $z$.
- **Hàm dốc.** $\phi_\gamma(t)=\min\{1,\max\{0,1-t/\gamma\}\}$, với $t\in\mathbb R$.
- **Hàm lỗi dốc.** $\ell_\gamma(f,z)=\phi_\gamma(\tilde y\,f(x))$, *hàm lỗi dốc* (ramp loss); $L^\gamma_D(f)$ và $L^\gamma_S(f)$ là rủi ro kì vọng và rủi ro thực nghiệm tương ứng.
- **Tỉ lệ vi phạm lề.** $L^{<\gamma}_S(f)=\frac1m\sum_i\mathbb 1[\tilde y_if(x_i)<\gamma]$, *tỉ lệ vi phạm lề* (margin violation rate) trên mẫu.
:::

Hàm dốc bằng $1$ khi $t\le0$, $1-t/\gamma$ khi $0\le t\le\gamma$ và $0$ khi $t\ge\gamma$, nên:

- **(i) Bị chặn.** $\ell_\gamma$ nhận giá trị trong $[0,1]$.
- **(ii) Lipschitz.** $\phi_\gamma$ liên tục, tuyến tính từng khúc với độ dốc $0$, $-1/\gamma$, $0$, nên là $(1/\gamma)$-Lipschitz trên $\mathbb R$.
- **(iii) Kẹp.** $\mathbb 1[t\le0]\le\phi_\gamma(t)\le\mathbb 1[t<\gamma]$. Hàm phân lớp $\mathbb 1[f\ge0]$ sai tại $z$ khi $y=1$, $f(x)<0$ hoặc $y=0$, $f(x)\ge0$; trong cả hai trường hợp $\tilde yf(x)\le0$, nên hàm lỗi 0–1 của nó không quá $\ell_\gamma(f,z)$, và $L^\gamma_S(f)\le L^{<\gamma}_S(f)$.

Mạng của Mệnh đề 07.2 có lề $\tfrac12$ tại cả bốn quan sát của Ví dụ 07.1 (tại $(0,0)$, $\tilde yf_\theta=(-1)(-\tfrac12)$), nên với $\gamma=\tfrac12$, $L^\gamma_S=L^{<\gamma}_S=0$. Nhân $\Theta_2$ và $b_2$ với $2$ cho lề $1$ và cùng hàm phân lớp; tổng quát, nhân $f$ với $c>0$ nhân mọi lề với $c$, nên chỉ *lề chuẩn hóa* (normalized margin), tức lề chia cho một chuẩn của $f$, mới so sánh được giữa hai hàm điểm số.

Hàm lỗi bản lề $\max\{0,1-t\}$ là $1$-Lipschitz nhưng không bị chặn trên; hàm lỗi 0–1 $\mathbb 1[t\le0]$ bị chặn nhưng không Lipschitz. Hàm dốc, tức hàm lỗi bản lề của $t/\gamma$ cắt ở mức $1$, có cả hai tính chất.

::: corollary Hệ quả 07.16 (Cận theo lề cho phân lớp tuyến tính bị chặn theo chuẩn) — phác thảo
**Giả thiết.** Năm thành phần sau.

- **Mẫu.** $S\sim D^m$ theo (T1).
- **Dữ liệu.** $y\in\{0,1\}$ và $\lVert x\rVert\le C_x$ trên giá của $D$.
- **Lớp.** $\mathcal F_B$ của Mệnh đề 07.13, với $B>0$ cố định trước mẫu.
- **Lề.** $\gamma>0$ cố định trước mẫu.
- **Tham số.** $\delta\in(0,1)$.

**Bảo đảm.** Với xác suất ít nhất $1-\delta$ theo $S\sim D^m$, đồng thời cho mọi $w$ với $\lVert w\rVert\le B$,
$$
\begin{aligned}
L_D(h_{w,0})&\le L^\gamma_D(h_w)\\
&\le L^{<\gamma}_S(h_w)+\frac{2BC_x}{\gamma\sqrt m}\\
&\quad+3\sqrt{\frac{\ln(2/\delta)}{2m}},
\end{aligned}
$$
trong đó $L_D(h_{w,0})$ là rủi ro kì vọng 0–1 của hàm phân lớp $h_{w,0}$.

Số hạng phạt phụ thuộc $m$, $\delta$ và $BC_x/\gamma$, không phụ thuộc $p$, và không đổi khi thay $(w,\gamma,B)$ bằng $(cw,c\gamma,cB)$. Bảo đảm là cấp lớp: nó đúng cho đầu ra của mọi thuật toán, kể cả SGD trên hàm lỗi logistic, có chuẩn không quá $B$.
:::

::: proof Chứng minh Hệ quả 07.16 (phác thảo)
**Lộ trình.** Áp dụng Định lý 07.11 cho lớp hàm lỗi dốc, chuyển độ phức tạp của nó về lớp điểm số bằng bổ đề co, rồi dùng Mệnh đề 07.13.

**Bước 1 (lớp hàm lỗi; $B$, $\gamma$ cố định trước mẫu, giá trị trong $[0,1]$).** Lớp
$$
\begin{aligned}
\mathcal G_\gamma=\{&z\mapsto\phi_\gamma(\tilde y\langle w,x\rangle):\\
&\lVert w\rVert\le B\}
\end{aligned}
$$
nhận giá trị trong $[0,1]$, cố định trước mẫu, và thỏa (M) với các $w$ hữu tỉ (liên tục theo $w$). Theo Định lý 07.11(b), với xác suất ít nhất $1-\delta$, đồng thời cho mọi $\lVert w\rVert\le B$,
$$
\begin{aligned}
&L^\gamma_D(h_w)\le L^\gamma_S(h_w)\\
&\quad+2\widehat{\mathfrak R}_S(\mathcal G_\gamma)\\
&\quad+3\sqrt{\ln(2/\delta)/(2m)} .
\end{aligned}
$$

**Bước 2 (bổ đề co).** Trên mẫu, $\mathcal G_\gamma\circ z_{1:m}=\phi\circ(\mathcal F_B\circ x_{1:m})$ với $\phi_i(a)=\phi_\gamma(\tilde y_ia)$, là $(1/\gamma)$-Lipschitz theo tính chất (ii) vì $\lvert\tilde y_i\rvert=1$. Bổ đề 07.14 cho $\widehat{\mathfrak R}_S(\mathcal G_\gamma)\le\frac1\gamma\widehat{\mathfrak R}_{x_{1:m}}(\mathcal F_B)$.

**Bước 3 (Mệnh đề 07.13; $\lVert x\rVert\le C_x$).** Các $X_i$ nằm trong giá của $D$, nên Mệnh đề 07.13 cho $2\widehat{\mathfrak R}_S(\mathcal G_\gamma)\le2BC_x/(\gamma\sqrt m)$.

**Bước 4 (kẹp).** Theo tính chất (iii), $L_D(h_{w,0})\le L^\gamma_D(h_w)$ và $L^\gamma_S(h_w)\le L^{<\gamma}_S(h_w)$. Thay vào Bước 1, ta được bảo đảm.

$\square$ Cận đo năng lực bằng tỉ số giữa chuẩn và lề, không bằng số tham số, nên có bảo đảm cả khi $p\gg m$.
:::

Tỉ số $BC_x/\gamma$ là đại lượng mà câu hỏi mở đầu cần.

## 9. Cận theo chuẩn và lề khi tham số hóa thừa

Hệ quả 07.16 không chứa $p$. Ta so nó với cận VC, dùng cùng công cụ cho hàm lỗi bình phương của Bài 06, đọc lại thí nghiệm, rồi xét giả thiết hàm lỗi bị chặn và mạng sâu.

::: example Ví dụ 07.8 (Phân lớp văn bản với một trăm nghìn đặc trưng)
**Thiết lập.** Như khối ứng dụng ở §3: $p=10^5$, $C_x=1$, $m=10^4$, $\delta=0{,}05$ và $BC_x/\gamma=10$ (giá trị giả định), với $B$, $\gamma$ chọn trước mẫu.

**Bước 1: số hạng Rademacher.** $2BC_x/(\gamma\sqrt m)=2\cdot10/100=0{,}2$.

**Bước 2: số hạng tin cậy.** Theo Ví dụ 07.6, $3\sqrt{\ln40/(2\cdot10^4)}\le0{,}0408$.

**Bước 3: cận.** Theo Hệ quả 07.16, với xác suất ít nhất $0{,}95$, mọi $w$ với $\lVert w\rVert\le B$ thỏa
$$
L_D(h_{w,0})\le L^{<\gamma}_S(h_w)+0{,}2408 .
$$
Với $d=p>2m$, một bộ $2m$ điểm bị tách trọn, nên $\Pi(2m)=2^{2m}$ và Định lý 03.15 chỉ cho $\rho_m\ge\sqrt{16\ln2}\approx3{,}33$, như đoạn sau Định lý 03.15.

**Bước 4: cỡ mẫu.** Số hạng phạt bằng $\big(2BC_x/\gamma+3\sqrt{\ln(2/\delta)/2}\big)/\sqrt m$, với $3\sqrt{\ln40/2}\approx4{,}0743$. Nó không quá $\epsilon$ khi
$$
m\ge\Big(\frac{2BC_x/\gamma+4{,}0743}{\epsilon}\Big)^2 .
$$
Với $BC_x/\gamma=10$, $\epsilon=0{,}1$: $(24{,}0743/0{,}1)^2\approx57\,957{,}2$, làm tròn lên $m\ge57\,958$. Tương tự, $m\ge231\,829$ với $\epsilon=0{,}05$, và $m\ge3690$ với $BC_x/\gamma=1$, $\epsilon=0{,}1$.

**Kết luận.** Với xác suất ít nhất $0{,}95$, tỉ lệ lỗi của $h_{w,0}$ không quá tỉ lệ văn bản có lề nhỏ hơn $\gamma$ cộng $0{,}2408$, bất kể $10^5$ đặc trưng; đó là câu trả lời cho câu hỏi thực hành của §3. Cái giá là vế phải tính tỉ lệ vi phạm lề, không chỉ tỉ lệ lỗi.
:::

::: example Ví dụ 07.9 (Hội tụ đều cho hồi quy bình phương trên đoạn $[-1,1]$)
**Thiết lập.** Cho $\mathcal Z=[-1,1]^2$, $\ell(w,(x,y))=(wx-y)^2\in[0,4]$, $W=[-1,1]$, $D$ bất kì trên $\mathcal Z$ và $\delta=0{,}05$: lớp của Ví dụ 06.7.

**Bước 1: chuẩn hóa.** Đặt $g_w=\ell(w,\cdot)/4\in[0,1]$ và $\mathcal G=\{g_w:\lvert w\rvert\le1\}$. Lớp cố định trước mẫu và thỏa (M) với các $w$ hữu tỉ, vì $g_w$ liên tục theo $w$.

**Bước 2: bổ đề co.** Ta có $g_w(z_i)=\phi_i(wx_i)$ với $\phi_i(a)=(a-y_i)^2/4$ và $\lvert wx_i\rvert\le1$. Trên $[-1,1]$, $\lvert\phi_i'(a)\rvert=\lvert a-y_i\rvert/2\le1$, nên $\phi_i$ là $1$-Lipschitz trên đó (Mệnh đề 05.5(a), $\phi_i$ lồi). Bổ đề 07.14 và Mệnh đề 07.13 với $p=1$, $B=C_x=1$ cho $\widehat{\mathfrak R}_S(\mathcal G)\le\frac1m\sqrt{\sum_ix_i^2}\le1/\sqrt m$.

**Bước 3: hai phía.** Theo Nhận xét 07.12 rồi nhân với $4$: với xác suất ít nhất $1-\delta$,
$$
\begin{aligned}
&\sup_{\lvert w\rvert\le1}\lvert L_D(w)-L_S(w)\rvert\\
&\le\frac8{\sqrt m}+12\sqrt{\frac{\ln(4/\delta)}{2m}} .
\end{aligned}
$$

**Bước 4: số.** Với $\ln80\approx4{,}3820$, vế phải không quá $0{,}8147$; $0{,}2577$; $0{,}0815$ khi $m=10^3$; $10^4$; $10^5$. Vì $8+12\sqrt{\ln80/2}\approx25{,}7625$, vế phải không quá $0{,}1$ khi $m\ge\lceil(25{,}7625/0{,}1)^2\rceil=66\,371$.

**Bước 5: hệ quả.** Với mọi $D$ trên $\mathcal Z$, $S$ là $\epsilon$-đại diện (Định nghĩa 02.13) với xác suất ít nhất $1-\delta$ khi $m$ đủ lớn: lớp hội tụ đều (Định nghĩa 03.13, viết cho hàm lỗi bình phương). Theo lập luận của Hệ quả 03.16, mọi nghiệm ERM trên $W$ có rủi ro vượt mức không quá $2\epsilon\le0{,}5153$ khi $m=10^4$. Với hàm lỗi $\ell/4\in[0,1]$, vế phải chia $4$ là bán kính $r$ mà Mệnh đề 04.3 cần.

**Kết luận.** ERM trên lớp này không ổn định đều với hệ số giảm theo $m$ (Ví dụ 06.7), nhưng lớp vẫn hội tụ đều. Bổ đề co cho một cận cấp lớp ở chỗ công cụ cấp thuật toán của Bài 06 không cho kết quả.
:::

Trong thí nghiệm, bán kính chỉ được biết sau khi huấn luyện, nên cần chọn $B$ hay $\gamma$ theo mẫu.

::: remark Nhận xét 07.17 (Chọn bán kính và lề sau khi xem mẫu)
Lấy $\gamma$ bằng lề nhỏ nhất trên mẫu, hay $B=\lVert\hat w\rVert$ sau khi huấn luyện, vi phạm giả thiết chọn trước mẫu của Hệ quả 07.16. Cách sửa giống Bổ đề 04.9: ta cố định trước lưới $\gamma_k=2^{-k}$, $k=1,2,\ldots$, với trọng số $q_k=1/(k(k+1))$, có tổng bằng $1$, áp dụng Hệ quả 07.16 với $\gamma_k$ và xác suất thất bại $\delta q_k$ cho mỗi $k$, rồi dùng bất đẳng thức hợp. Với xác suất ít nhất $1-\delta$, đồng thời cho mọi $k$ và mọi $\lVert w\rVert\le B$,
$$
\begin{aligned}
L_D(h_{w,0})\le{}&L^{<\gamma_k}_S(h_w)+\frac{2BC_x}{\gamma_k\sqrt m}\\
&+3\sqrt{\frac{\ln(2/(\delta q_k))}{2m}} .
\end{aligned}
$$
Chọn $k$ sau khi xem mẫu chỉ tốn thêm $\ln(k(k+1))$ dưới dấu căn; lưới $B_k=2^k$ cho bán kính được xử lý cùng cách.
:::

::: example Ví dụ 07.10 (Chuẩn và lề trong thí nghiệm mở đầu)
**Thiết lập.** Lớp của Ví dụ 07.3, $m=200$, mười lần chạy (Phụ lục D). Vì $\lVert x\rVert\le1$ và $\lVert v_j\rVert=1$, tọa độ thứ $j$ của $\chi(x)$ có trị tuyệt đối không quá $(1+\lvert b_{1j}\rvert)/\sqrt N$, nên
$$
\begin{aligned}
\lVert\chi(x)\rVert&\le C_x,\\
C_x^2&=\tfrac1N\textstyle\sum_{j=1}^N(1+\lvert b_{1j}\rvert)^2,
\end{aligned}
$$
với $C_x$ từ $1{,}518$ đến $1{,}544$ tùy lần chạy.

**Bước 1: lề.** Vì $\langle\hat w,\chi(x_i)\rangle=\tilde y_i$, mọi lề bằng $\tilde y_i^2=1$; với $\gamma=1$, tỉ lệ vi phạm lề bằng $0$.

**Bước 2: chuẩn và lề chuẩn hóa.** Mười lần chạy cho:

- **Nhãn thật.** $\lVert\hat w\rVert$ trung bình $916$ (từ $351$ đến $1721$); lề chuẩn hóa $\gamma/(\lVert\hat w\rVert C_x)$ từ $3{,}8\cdot10^{-4}$ đến $1{,}87\cdot10^{-3}$.
- **Nhãn hoán vị.** $\lVert\hat w\rVert$ trung bình $10\,853$ (từ $6792$ đến $14\,052$); lề chuẩn hóa từ $4{,}6\cdot10^{-5}$ đến $9{,}6\cdot10^{-5}$.

Tỉ số hai chuẩn trung bình là $11{,}85$. Chuẩn của $\Theta_2=\hat w^\top/\sqrt N$ trung bình $20{,}5$ và $242{,}7$, cùng tỉ số.

**Bước 3: số hạng Rademacher.** Với $B=\lVert\hat w\rVert$, số hạng $2BC_x/(\gamma\sqrt{200})$ nằm trong khoảng $75$–$372$ với nhãn thật và $1467$–$3047$ với nhãn hoán vị (chỉ để so sánh, vì (T1) không thỏa). Bán kính được chọn sau khi xem mẫu, nên cận hợp lệ dùng lưới $B_k=2^k\ge\lVert\hat w\rVert$ của Nhận xét 07.17, với số hạng còn lớn hơn.

**Bước 4: đọc kết quả.**

- **(i) Cận.** Ở $m=200$, cận theo chuẩn lớn hơn $1$ trong khi lỗi kiểm tra với nhãn thật là $0{,}023$; cận không cho thông tin.
- **(ii) Mẫu kiểm tra.** Với nhãn thật, hàm đã chọn chỉ phụ thuộc mẫu huấn luyện và lớp ẩn, độc lập với $5000$ điểm kiểm tra, nên Hệ quả 02.10(b) cho khoảng tin cậy mức $0{,}95$ với bán kính $\sqrt{\ln40/10^4}\le0{,}0193$.

**Kết luận.** Trong thí nghiệm, chuẩn và lề chuẩn hóa phân biệt hai trường hợp, còn số tham số và độ phức tạp Rademacher của lớp kiến trúc thì không.
:::

Đặt thẳng một lớp điểm số nhỏ vào Định lý 07.11, thay cho lớp hàm lỗi, dẫn tới kết luận sai về rủi ro 0–1.

::: example Ví dụ 07.11 (Lớp điểm số thay cho lớp hàm lỗi)
**Thiết lập.** Lớp $\mathcal F_B$ trên $\mathbb R^p$, $\lVert x\rVert\le1$, $m=10^4$; giả thiết "lớp hàm lỗi" của Định lý 07.11 bị thay bằng một lớp điểm số.

**Bước 1: lớp điểm số rất nhỏ.** Với $B=10^{-6}$, Mệnh đề 07.13 cho $\widehat{\mathfrak R}_S(\mathcal F_B)\le10^{-8}$.

**Bước 2: lớp hàm phân lớp không nhỏ đi.** Hàm $h_{w,0}$ không đổi khi nhân $w$ với $c>0$, nên $\{h_{w,0}:\lVert w\rVert\le10^{-6}\}=\mathcal H^p_{\mathrm{hom}}$, có chiều VC $p$ (Mệnh đề 03.9(b)).

**Bước 3: chỗ lập luận hỏng.** Lớp $\{x\mapsto\tfrac12+\langle w,x\rangle:\lVert w\rVert\le10^{-6}\}$ nhận giá trị trong $[0,1]$ và có độ phức tạp không quá $10^{-8}$ (Bổ đề 07.8). Định lý 07.11 áp dụng cho nó, nhưng chỉ chặn độ lệch của trung bình điểm số. Hàm lỗi 0–1 không phải hàm Lipschitz của điểm số, nên bổ đề co không nối hai lớp; hàm lỗi dốc nối chúng với giá $1/\gamma$, và thu nhỏ $B$ buộc thu nhỏ $\gamma$ theo cùng tỉ lệ.

**Bước 4: hàm lỗi không bị chặn.** Hàm lỗi bản lề và logistic không bị chặn khi $w$ chạy trên $\mathbb R^p$. Với $B$ chọn trước mẫu, $\lVert w\rVert\le B$ và $\lVert x\rVert\le C_x$, hàm lỗi logistic nằm trong $[0,K]$, $K=\ln(1+e^{BC_x})$, và là $1$-Lipschitz theo điểm số. Chia cho $K$ rồi dùng bổ đề co và Mệnh đề 07.13: với xác suất ít nhất $1-\delta$, đồng thời cho mọi $\lVert w\rVert\le B$, rủi ro logistic kì vọng $L_D(w)$ và thực nghiệm $L_S(w)$ thỏa
$$
\begin{aligned}
L_D(w)\le{}&L_S(w)+\frac{2BC_x}{\sqrt m}\\
&+3K\sqrt{\frac{\ln(2/\delta)}{2m}} .
\end{aligned}
$$

**Kết luận.** Định lý 07.11 áp dụng cho lớp hàm lỗi bị chặn, không tự động cho điểm số của mạng; hàm lỗi logistic dùng được sau khi chia cho $K$.
:::

Các cận trên dùng cho lớp tuyến tính; với mạng, đó là lớp ra khi lớp ẩn cố định. Khi mọi lớp nơ-ron đều được huấn luyện, cần một đại lượng khác.

::: remark Nhận xét 07.18 (Cận theo chuẩn phổ cho mạng sâu) — đọc thêm
Bartlett, Foster và Telgarsky (2017) chứng minh cận theo lề sau cho mạng sâu, viết theo kí hiệu của bài.

- **Mạng.** $F_\Theta(x)=\varsigma_J(\Theta_J\varsigma_{J-1}(\cdots\varsigma_1(\Theta_1x)\cdots))$, không có hệ số tự do; mỗi $\varsigma_j$ là $G_j$-Lipschitz với $\varsigma_j(0)=0$ (ReLU: $G_j=1$). Đầu ra có $k$ tọa độ, ứng với $k$ nhãn; nhãn dự đoán là $\arg\max_{y'}F_\Theta(x)_{y'}$, và *lề nhiều lớp* (multiclass margin) là $F_\Theta(x)_y-\max_{y'\ne y}F_\Theta(x)_{y'}$.
- **Độ phức tạp phổ.** Với các *ma trận tham chiếu* (reference matrices) $M_j$ cố định trước,
  $$
  \begin{aligned}
  R_\Theta={}&\Big(\textstyle\prod_jG_j\lVert\Theta_j\rVert_{\mathrm{op}}\Big)\\
  &\cdot\Big(\textstyle\sum_jr_j^{2/3}\Big)^{3/2}
  \end{aligned}
  $$
  là *độ phức tạp phổ* (spectral complexity), với $r_j=\lVert\Theta_j^\top-M_j^\top\rVert_{2,1}/\lVert\Theta_j\rVert_{\mathrm{op}}$; *chuẩn nhóm* (group norm) $\lVert\Theta_j^\top-M_j^\top\rVert_{2,1}$ là tổng các chuẩn Euclid của các hàng của $\Theta_j-M_j$.
- **Cận.** Với quan sát độc lập cùng phân bố, với xác suất ít nhất $1-\delta$, đồng thời cho mọi $\gamma>0$ và mọi $\Theta$, xác suất phân lớp sai không quá tỉ lệ quan sát của mẫu có lề nhiều lớp không quá $\gamma$ cộng
  $$
  \begin{aligned}
  \tilde O\Big(&\frac{\lVert X\rVert_2R_\Theta\ln\bar N}{\gamma m}\\
  &+\sqrt{\tfrac{\ln(1/\delta)}m}\Big),
  \end{aligned}
  $$
  với $\lVert X\rVert_2=(\sum_i\lVert x_i\rVert^2)^{1/2}$, $\bar N$ là số lớn nhất trong $p$, $k$ và các độ rộng, và $\tilde O$ ẩn các thừa số logarit.

Khi $\lVert x_i\rVert\le C_x$, ta có $\lVert X\rVert_2/m\le C_x/\sqrt m$, nên số hạng đầu có dạng $C_xR_\Theta\ln\bar N/(\gamma\sqrt m)$: $R_\Theta$ đóng vai $B$ của Hệ quả 07.16. Ngoài thừa số logarit, cận không phụ thuộc số tham số hay số nhãn. Chứng minh dùng *số phủ* (covering number), không dùng bổ đề co cho từng lớp nơ-ron. Với $M_j=0$, $R_\Theta$ không đổi khi nhân $\Theta_j$ với một số dương và chia $\Theta_{j+1}$ cho số đó; với ReLU, hàm $F_\Theta$ cũng không đổi, như Bước 2 của Ví dụ 07.2 (mạng ở đây không có hệ số tự do). Cận tuyến tính của Hệ quả 07.16 không thay được số hạng này.
:::

Mọi cận ở đây là cận cấp lớp, đúng với hàm do huấn luyện chọn khi hàm đó nằm trong lớp chọn trước.

## 10. Ý nghĩa, tác động và giới hạn

Trong thí nghiệm mở đầu, lớp kiến trúc có độ phức tạp Rademacher $\tfrac12$ với cả hai loại nhãn, và cận $1{,}2881$ với nhãn thật (Ví dụ 07.5, 07.6). Hai trường hợp khác nhau ở mô hình do huấn luyện chọn, với chuẩn khác nhau gần $12$ lần (Ví dụ 07.10). Đây là bằng chứng thí nghiệm, không phải chứng minh.

Về biểu diễn, trên Ví dụ 07.1 mạng hai nơ-ron ẩn có sai số xấp xỉ $0$, lớp afin có $\tfrac14$. Năng lực thống kê được đo bằng độ phức tạp Rademacher (Định lý 07.11). Khả năng tối ưu cần lập luận riêng, vì Bài 05 dùng tính lồi.

Hệ quả 07.16 cho cận $0{,}2408$ với $10^5$ đặc trưng (Ví dụ 07.8). Cùng một hàm có tổng bình phương tham số $10{,}25$ hay $500{,}30$ (Ví dụ 07.2), nên chỉ đại lượng bất biến khi đổi tỉ lệ, như lề chuẩn hóa, mới so sánh được các mô hình. Các cận không dùng tính lồi hay sự hội tụ, nên đúng cho mạng huấn luyện bằng SGD trên hàm mục tiêu không lồi, miễn là đầu ra thuộc lớp chọn trước.

Các kết quả của bài có năm giới hạn.

- **Lớp chọn trước mẫu.** Chọn $B$, $\gamma$ theo mẫu tốn một bất đẳng thức hợp trên lưới (Nhận xét 07.17).
- **Hàm lỗi bị chặn.** Lớp điểm số không thay được lớp hàm lỗi trong $[0,1]$ (Ví dụ 07.11).
- **Thuật toán.** Các cận không giải thích vì sao phép huấn luyện chọn nghiệm có chuẩn nhỏ với nhãn thật (Ví dụ 07.10).
- **Mạng sâu.** Cận tuyến tính không chuyển sang mạng sâu (Nhận xét 07.18).
- **Cận không cho thông tin.** Ở $m=200$, số hạng Rademacher của thí nghiệm lớn hơn $75$, còn lỗi kiểm tra với nhãn thật có bán kính tin cậy $0{,}0193$ (Ví dụ 07.10).

Khi cận lớn hơn $1$, cần báo lỗi trên một mẫu kiểm tra độc lập. Khi so hai mô hình cùng kiến trúc, đại lượng xuất hiện trong cận là lề chuẩn hóa, còn số tham số thì không.

## 11. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 07](material-viewer.html?doc=materials/lec-07/exercises.md); sáu bài đầu là bài gốc, ba bài sau chọn từ UML.

1. **Bài tập 07.1** (Phép hoặc loại trừ bằng mạng ReLU và bằng hàm phân lớp afin): mục tiêu 1.
2. **Bài tập 07.2** (Độ phức tạp Rademacher của lớp một phần tử và lớp hai phần tử): mục tiêu 2.
3. **Bài tập 07.3** (Cận độ phức tạp Rademacher cho lớp tuyến tính bị chặn theo chuẩn): mục tiêu 4.
4. **Bài tập 07.4** (Số tham số, cỡ mẫu và lỗi kiểm tra): mục tiêu 3, 5.
5. **Bài tập 07.5** (Xấp xỉ phổ quát và việc tìm một mạng tốt bằng SGD): mục tiêu 1.
6. **Bài tập 07.6** (Nhãn thật và nhãn hoán vị, thực nghiệm tùy chọn): mục tiêu 5.
7. **Bài tập 07.7** (Hàm tăng trưởng của lớp tích; UML Bài tập 20.3): mục tiêu 5.
8. **Bài tập 07.8** (Hàm tăng trưởng của lớp hàm hợp; UML Bài tập 20.4): mục tiêu 5.
9. **Bài tập 07.9** (Tùy chọn: xấp xỉ đều hàm Lipschitz một biến bằng mạng một lớp ẩn; UML Bài tập 20.1, phát biểu đã sửa: hàm kích hoạt ReLU, một biến): mục tiêu 1.

## 12. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Xét bài toán phân lớp tuyến tính với $\lVert x\rVert\le1$, $m=2500$ quan sát độc lập cùng phân bố và $\delta=0{,}05$. Lớp $\mathcal F_B$ với $B=2$ và lề $\gamma=0{,}5$ được chọn trước khi lấy mẫu.

(a) Một véc-tơ $w$ với $\lVert w\rVert\le2$ có tỉ lệ vi phạm lề $L^{<\gamma}_S(h_w)=0{,}04$. Tính cận của Hệ quả 07.16 cho rủi ro 0–1 của $h_{w,0}$.

(b) SGD trên hàm lỗi logistic trả về $\hat w$ với $\lVert\hat w\rVert=1{,}6$ và $L^{<\gamma}_S(h_{\hat w})=0{,}04$. Cận ở (a) có áp dụng cho $\hat w$ không? Nếu $\gamma=0{,}5$ được chọn sau khi xem các lề trên mẫu, dùng lưới của Nhận xét 07.17 và tính lại số hạng tin cậy.

(c) Mệnh đề 07.13 cho $\widehat{\mathfrak R}_S(\mathcal F_2)\le0{,}04$. Vì sao không được đặt $2\cdot0{,}04$ vào Định lý 07.11 để chặn rủi ro 0–1?

::: solution Lời giải câu hỏi cuối buổi
**(a)** Với $B=2$, $C_x=1$, $\gamma=0{,}5$ và $\sqrt{2500}=50$, số hạng Rademacher là
$$
\frac{2BC_x}{\gamma\sqrt m}=\frac{2\cdot2\cdot1}{0{,}5\cdot50}=0{,}16 .
$$
Số hạng tin cậy là $3\sqrt{\ln40/5000}\approx0{,}0815$. Cận là
$$
0{,}04+0{,}16+0{,}0815=0{,}2815 .
$$

**(b)** Có: $\lVert\hat w\rVert\le2$, $B$ và $\gamma$ cố định trước mẫu, và cận đúng đồng thời cho mọi $w$ của lớp; với $L^{<\gamma}_S(h_{\hat w})=0{,}04$, cận vẫn là $0{,}2815$. Với lưới $\gamma_k=2^{-k}$, giá trị $\gamma=0{,}5$ ứng với $k=1$, $q_1=\tfrac12$ và $\delta q_1=0{,}025$. Số hạng tin cậy thành $3\sqrt{\ln80/5000}\le0{,}0889$, và cận thành $0{,}04+0{,}16+0{,}0889=0{,}2889$.

**(c)** Định lý 07.11 cần một lớp hàm lỗi nhận giá trị trong $[0,1]$. Độ phức tạp của lớp điểm số không chặn rủi ro 0–1: hàm lỗi 0–1 không phải hàm Lipschitz của điểm số, và lớp hàm phân lớp không đổi khi thu nhỏ $w$ (Ví dụ 07.11). Hàm lỗi dốc nối hai lớp với giá $1/\gamma$: $2\cdot0{,}04/0{,}5=0{,}16$, đúng số hạng ở (a).
:::

Hệ quả 07.16 đúng cho mọi $w$ trong quả cầu, nên không giải thích vì sao cùng một quy tắc huấn luyện chọn nghiệm có chuẩn khoảng $916$ với nhãn thật và $10\,853$ với nhãn hoán vị. Trong thí nghiệm, nghiệm nội suy chuẩn nhỏ nhất cũng là giới hạn của hạ gradient khởi tạo tại $0$ (Phụ lục D), nên chuẩn của nó do quỹ đạo tối ưu quyết định. Bài 06 chặn khoảng cách tổng quát hóa qua tính ổn định đều, một tính chất của thuật toán chứ không của lớp. Câu hỏi cho Bài 08 là: với hàm lỗi lồi, trơn và Lipschitz, quỹ đạo của SGD, qua số bước và độ dài bước, có cho một bảo đảm cho chính hàm mà SGD trả về không?

## 13. Tài liệu đọc

- **Trước buổi học:** UML §20.1–20.3 (mạng lan truyền tới, năng lực biểu diễn), §26.1 (độ phức tạp Rademacher).
- **Sau buổi học:** UML §26.2 (lớp tuyến tính), §20.4–20.5 (độ phức tạp mẫu và thời gian chạy khi học mạng nơ-ron); các bài tập UML §20.9 đã chọn ở §11.
- **Mở rộng:** UML §26.3 (cận cho SVM và lề), §28.1 (cận trên cho học bất khả tri với chiều VC hữu hạn, qua cận Rademacher), §15.2.3 (hàm lỗi dốc), Bài tập 20.5 (chiều VC của mạng sigmoid); P. L. Bartlett, D. J. Foster, M. Telgarsky (2017), *Spectrally-normalized margin bounds for neural networks*, NeurIPS, Định lý 1.1 và phần thảo luận (§1–§3). Thí nghiệm nhãn ngẫu nhiên của bài báo dùng dữ liệu ảnh.

**Quan hệ với giáo trình UML.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục. Các khác biệt chính:

- **Hằng số của cận Rademacher.** UML §26.1 phát biểu cận phụ thuộc dữ liệu cho hàm lỗi có $\lvert\ell\rvert\le c$, với số hạng tin cậy $4c\sqrt{2\ln(4/\delta)/m}$ và bất đẳng thức McDiarmid hai phía không chứng minh. Học phần dùng hàm lỗi trong $[0,1]$ và hai lần dạng một phía, được $3\sqrt{\ln(2/\delta)/(2m)}$; với $c=1$, $m=10^4$, $\delta=0{,}05$, hai số hạng là $0{,}1185$ và $0{,}0408$.
- **Lớp tuyến tính và lề.** UML §26.2 chuẩn hóa $B=1$; UML §26.3 cố định lề bằng $1$ và dùng kì vọng của độ phức tạp. Học phần giữ $B$, $\gamma$ riêng, dùng độ phức tạp thực nghiệm, và viết hằng số Lipschitz của bổ đề co là $G$ thay cho $\rho$.
- **Mạng nơ-ron.** UML §20.1 mô tả mạng bằng đồ thị có hướng, hàm kích hoạt dấu hay sigmoid, độ sâu $T$, kí hiệu $\sigma$; học phần dùng dạng ma trận, ReLU, $J$ và $\varsigma$.

## Phụ lục

### A. Bất đẳng thức McDiarmid

Kí hiệu $V_{1:k}=(V_1,\ldots,V_k)$ và $v_{1:k}=(v_1,\ldots,v_k)$. Tham số của phương pháp Chernoff viết $\kappa$, để khỏi lẫn với nhãn ngẫu nhiên $\tau_i$ của Mệnh đề 07.9.

::: proof Chứng minh Bổ đề 07.10
**Lộ trình.** Viết $Q(V)-\mathbb EQ(V)$ thành tổng của $m$ bước tăng khi lần lượt biết $V_1,V_2,\ldots$; mỗi bước tăng, khi các biến trước nó cố định, có kì vọng $0$ và nằm trong một đoạn độ dài $c_k$; bổ đề Hoeffding chặn hàm sinh mô-men của từng bước; nhân các cận lại rồi dùng phương pháp Chernoff. Bất đẳng thức then chốt là $\mathbb Ee^{\kappa(Q-\mathbb EQ)}\le e^{\kappa^2\sum_kc_k^2/8}$.

**Bước 1 (các hàm trung bình; tính độc lập).** Theo điều kiện sai phân bị chặn, $\lvert Q(v)-Q(v')\rvert\le\sum_ic_i$ với mọi $v$, $v'$, nên $Q$ bị chặn và mọi kì vọng dưới đây hữu hạn. Với $k=0,1,\ldots,m$, đặt
$$
g_k(v_{1:k})=\mathbb E\,Q(v_{1:k},V_{k+1:m}),
$$
kì vọng chỉ lấy theo các biến còn lại. Vì $V_1,\ldots,V_m$ độc lập, định lý Fubini cho $g_{k-1}(v_{1:k-1})=\mathbb E\,g_k(v_{1:k-1},V_k)$; tính độc lập được dùng ở đây. Ta có $g_0=\mathbb EQ(V)$ và $g_m=Q$. Biến $E_k=g_k(V_{1:k})$ là kì vọng có điều kiện $\mathbb E[Q(V)\mid V_{1:k}]$; dãy $E_0,\ldots,E_m$ gọi là *martingale Doob* (Doob martingale).

**Bước 2 (phân tích thành bước tăng).** Đặt $D_k=E_k-E_{k-1}$. Tổng triệt tiêu cho
$$
Q(V)-\mathbb EQ(V)=\sum_{k=1}^mD_k .
$$

**Bước 3 (một bước tăng; sai phân bị chặn).** Cố định $v_{1:k-1}$ và đặt $\tilde D_k(x)=g_k(v_{1:k-1},x)-g_{k-1}(v_{1:k-1})$, nên $D_k=\tilde D_k(V_k)$ khi $V_{1:k-1}=v_{1:k-1}$. Theo Bước 1, $\mathbb E\tilde D_k(V_k)=0$. Với hai giá trị $x$, $x'$ của tọa độ thứ $k$, điều kiện sai phân bị chặn đúng bên trong kì vọng, nên
$$
\begin{aligned}
&\lvert\tilde D_k(x)-\tilde D_k(x')\rvert\\
&\le\mathbb E\big\lvert Q(v_{1:k-1},x,V_{k+1:m})\\
&\qquad-Q(v_{1:k-1},x',V_{k+1:m})\big\rvert\\
&\le c_k .
\end{aligned}
$$
Do đó $\tilde D_k(V_k)$ nằm trong đoạn $[\inf\tilde D_k,\sup\tilde D_k]$, có độ dài không quá $c_k$; điều kiện sai phân bị chặn được dùng ở đây.

**Bước 4 (bổ đề Hoeffding).** Áp dụng Bổ đề 02.6 cho biến $\tilde D_k(V_k)$, có kì vọng $0$, với mọi $\kappa\in\mathbb R$:
$$
\mathbb Ee^{\kappa\tilde D_k(V_k)}\le e^{\kappa^2c_k^2/8}.
$$
Cận này đúng với mọi giá trị cố định $v_{1:k-1}$; khi $\tilde D_k$ hằng, $\tilde D_k(V_k)=0$ và cận đúng tầm thường.

**Bước 5 (nhân các cận; tính chất tháp).** Vì $V_m$ độc lập với $V_{1:m-1}$, lấy kì vọng theo $V_m$ trước (định lý Fubini, ở đây đóng vai tính chất tháp) và dùng Bước 4 với $k=m$:
$$
\begin{aligned}
&\mathbb Ee^{\kappa\sum_{k\le m}D_k}\\
&=\mathbb E\Big[e^{\kappa\sum_{k<m}D_k}\,\mathbb E_{V_m}e^{\kappa D_m}\Big]\\
&\le e^{\kappa^2c_m^2/8}\,\mathbb Ee^{\kappa\sum_{k<m}D_k}.
\end{aligned}
$$
Lặp lại cho $k=m-1,\ldots,1$, ta được $\mathbb Ee^{\kappa(Q-\mathbb EQ)}\le e^{\kappa^2\sum_kc_k^2/8}$.

**Bước 6 (phương pháp Chernoff).** Theo Bổ đề 02.5(a), với $\kappa>0$,
$$
\begin{aligned}
&\Pr(Q-\mathbb EQ\ge t)\\
&\le e^{-\kappa t}\,\mathbb Ee^{\kappa(Q-\mathbb EQ)}\\
&\le\exp\big(-\kappa t+\kappa^2\textstyle\sum_kc_k^2/8\big).
\end{aligned}
$$
Nếu mọi $c_k=0$ thì $Q$ hằng và hai xác suất bằng $0$. Nếu không, chọn $\kappa=4t/\sum_kc_k^2$: số mũ bằng $-4t^2/\sum_kc_k^2+2t^2/\sum_kc_k^2=-2t^2/\sum_kc_k^2$, tức đuôi trên. Hàm $-Q$ thỏa điều kiện sai phân bị chặn với cùng $c_k$, nên đuôi dưới suy từ đuôi trên áp dụng cho $-Q$.

$\square$ Điểm quyết định là độ dài $c_k$ của đoạn chứa mỗi bước tăng. Nếu chỉ dùng $\lvert D_k\rvert\le c_k$, tức đoạn $[-c_k,c_k]$ dài $2c_k$, cùng lập luận cho $\exp\big(-t^2/(2\sum_kc_k^2)\big)$, yếu hơn bốn lần trong số mũ, và hằng số $3$ của Định lý 07.11 sẽ lớn gấp đôi.
:::

### B. Bổ đề co

Mọi tập véc-tơ dưới đây khác rỗng, bị chặn, nên mọi cận trên đúng hữu hạn; không cần giả sử chúng đạt được.

::: proof Chứng minh Bổ đề 07.14
**Lộ trình.** Xét trường hợp $G=1$ và chứng minh rằng thay tọa độ thứ nhất $a_1$ bằng $\phi_1(a_1)$ không làm tăng độ phức tạp; lặp lại cho từng tọa độ; cuối cùng đưa trường hợp $G$ bất kì về $G=1$. Bất đẳng thức then chốt là $\phi_1(a_1)-\phi_1(a'_1)\le\lvert a_1-a'_1\rvert$.

**Bước 1 (một tọa độ).** Giả sử $\phi_1$ là $1$-Lipschitz trên một tập chứa $\{a_1:a\in A\}$, và đặt $A_1=\{(\phi_1(a_1),a_2,\ldots,a_m):a\in A\}$. Cố định $\sigma_2,\ldots,\sigma_m$ và đặt $r(a)=\sum_{i\ge2}\sigma_ia_i$. Kì vọng theo $\sigma_1$ là trung bình của hai giá trị $\sigma_1=\pm1$:
$$
\begin{aligned}
&\mathbb E_{\sigma_1}\sup_a\big(\sigma_1\phi_1(a_1)+r(a)\big)\\
&=\tfrac12\sup_a\big(\phi_1(a_1)+r(a)\big)\\
&\quad+\tfrac12\sup_{a'}\big(r(a')-\phi_1(a'_1)\big)\\
&=\tfrac12\sup_{a,a'}\big(\phi_1(a_1)-\phi_1(a'_1)\\
&\qquad+r(a)+r(a')\big)\\
&\le\tfrac12\sup_{a,a'}\big(\lvert a_1-a'_1\rvert\\
&\qquad+r(a)+r(a')\big).
\end{aligned}
$$
Đẳng thức thứ hai đúng vì hai cận trên đúng lấy theo hai biến chạy riêng $a$, $a'$. Bất đẳng thức là tính Lipschitz của $\phi_1$ tại $a_1$, $a'_1$; giả thiết Lipschitz được dùng ở đây.

**Bước 2 (bỏ trị tuyệt đối).** Đổi vai $a$ và $a'$ không đổi $r(a)+r(a')$ và đổi dấu $a_1-a'_1$. Do đó cận trên đúng của $\lvert a_1-a'_1\rvert+r(a)+r(a')$ bằng cận trên đúng của $a_1-a'_1+r(a)+r(a')$, và
$$
\begin{aligned}
&\tfrac12\sup_{a,a'}\big(a_1-a'_1+r(a)+r(a')\big)\\
&=\tfrac12\sup_a\big(a_1+r(a)\big)\\
&\quad+\tfrac12\sup_{a'}\big(r(a')-a'_1\big)\\
&=\mathbb E_{\sigma_1}\sup_a\big(\sigma_1a_1+r(a)\big).
\end{aligned}
$$

**Bước 3 (lấy kì vọng và lặp).** Ghép Bước 1, 2, lấy kì vọng theo $\sigma_2,\ldots,\sigma_m$ và chia cho $m$, ta được $\widehat{\mathfrak R}(A_1)\le\widehat{\mathfrak R}(A)$. Áp dụng cùng lập luận cho tọa độ thứ hai của $A_1$ với $\phi_2$ (tọa độ này của $A_1$ vẫn là $a_2$, nằm trong tập mà $\phi_2$ Lipschitz), rồi lần lượt cho các tọa độ còn lại, ta được $\widehat{\mathfrak R}(\phi\circ A)\le\widehat{\mathfrak R}(A)$ khi $G=1$.

**Bước 4 (hằng số $G$ bất kì).** Nếu $G=0$, mỗi $\phi_i$ hằng trên tập chứa $\{a_i:a\in A\}$, nên $\phi\circ A$ chỉ có một phần tử và $\widehat{\mathfrak R}(\phi\circ A)=0$. Nếu $G>0$, các hàm $\phi_i/G$ là $1$-Lipschitz, và theo Bổ đề 07.8 với hệ số $G$,
$$
\begin{aligned}
\widehat{\mathfrak R}(\phi\circ A)&=G\,\widehat{\mathfrak R}\big((\phi/G)\circ A\big)\\
&\le G\,\widehat{\mathfrak R}(A).
\end{aligned}
$$

$\square$ Chứng minh không cần $\phi_i(0)=0$: trong Bước 1, mọi hằng số cộng vào $\phi_1$ xuất hiện trong hai cận trên đúng với dấu ngược nhau và triệt tiêu. Với định nghĩa có trị tuyệt đối, phép triệt tiêu này không còn, và cần thêm điều kiện định tâm (§8).
:::

### C. Chi tiết cho Định lý 07.11

Ba chi tiết dùng trong chứng minh Định lý 07.11.

**(i) Phép đổi chỗ ở Bước 2.** Theo (T1), $2m$ quan sát của $(S,S')$ độc lập cùng phân bố $D$, nên phân bố đồng thời của chúng là tích $D^{2m}$ và không đổi khi hoán vị các tọa độ. Với $\sigma$ cố định, phép đổi chỗ $Z_i\leftrightarrow Z'_i$ tại các $i$ có $\sigma_i=-1$ là một hoán vị như vậy, và nó biến $\sum_i\big(g(Z'_i)-g(Z_i)\big)$ thành $\sum_i\sigma_i\big(g(Z'_i)-g(Z_i)\big)$ đồng thời cho mọi $g$. Do đó hai cận trên đúng theo $g$ có cùng phân bố và cùng kì vọng. Lấy trung bình theo $\sigma$, độc lập với $(S,S')$ (định lý Fubini), ta được đẳng thức ở Bước 2.

**(ii) Sai phân của một cận trên đúng.** Cho hai hàm $u$, $u'$ trên $\mathcal G$ với $\lvert u(g)-u'(g)\rvert\le c$ cho mọi $g$. Khi đó với mọi $g$,
$$
u(g)\le u'(g)+c\le\sup_{\mathcal G}u'+c,
$$
nên $\sup u\le\sup u'+c$; đổi vai $u$ và $u'$ cho $\lvert\sup u-\sup u'\rvert\le c$. Áp dụng với $u(g)=L_D(g)-L_s(g)$, $u'(g)=L_D(g)-L_{s^{(i)}}(g)$ và $c=1/m$ cho sai phân của $\Psi$. Áp dụng với $u(g)=\frac1m\sum_j\sigma_jg(z_j)$ và hàm tương ứng trên $s^{(i)}$, rồi lấy kì vọng theo $\sigma$, cho sai phân của $\widehat{\mathfrak R}_s(\mathcal G)$.

**(iii) Tính đo được dưới (M).** Lấy $g\in\mathcal G$ và dãy $g_k\in\mathcal G_0$ hội tụ theo từng điểm về $g$. Trên mỗi mẫu $s$, $L_s(g_k)\to L_s(g)$ vì $L_s$ là tổng hữu hạn, và $L_D(g_k)\to L_D(g)$ theo định lý hội tụ bị chặn, vì $0\le g_k\le1$. Do đó giá trị của $L_D-L_s$ tại $g$ là giới hạn của các giá trị tại $g_k$, nên cận trên đúng theo $\mathcal G$ bằng cận trên đúng theo $\mathcal G_0$. Cận trên đúng của một họ đếm được hàm đo được của $s$ là đo được, nên $\Psi$ đo được. Cùng lập luận với mỗi trong $2^m$ bộ dấu cho tính đo được của $\widehat{\mathfrak R}_s(\mathcal G)$, và với các cận trên đúng theo $(S,S',\sigma)$ ở Bước 1–2.

### D. Giao thức thí nghiệm của câu hỏi mở đầu

Giao thức dưới đây đủ để tái lập bảng của câu hỏi mở đầu và các số của Ví dụ 07.3, 07.10; chỉ cần thư viện NumPy.

- **Dữ liệu.** Mỗi điểm $x$ rút đều trên hình tròn đơn vị của $\mathbb R^2$: hướng là một véc-tơ chuẩn tắc hai chiều đã chuẩn hóa, bán kính là căn bậc hai của một biến đều trên $[0,1]$ (rút một mảng $n\times2$ chuẩn tắc rồi một mảng $n$ đều). Nhãn thật $y=\mathbb 1[x_1+0{,}5x_2\ge0]$. Mẫu huấn luyện có $m=200$ điểm, mẫu kiểm tra có $5000$ điểm độc lập.
- **Nhãn hoán vị.** Một hoán vị đều của $200$ nhãn huấn luyện, và một hoán vị đều độc lập của $5000$ nhãn kiểm tra; hai lượt huấn luyện dùng chung điểm và lớp ẩn. Các cặp $(x_i,y_i)$ của mẫu hoán vị không độc lập (tổng các nhãn hoán vị bằng tổng các nhãn thật), nên (T1) không thỏa; các số của trường hợp này chỉ để so sánh. Nhãn ngẫu nhiên độc lập với $x$, như $\tau_i$ của Mệnh đề 07.9, thỏa (T1).
- **Mạng.** $N=2000$ nơ-ron ẩn; $v_j$ là véc-tơ chuẩn tắc hai chiều đã chuẩn hóa, tức đều trên đường tròn đơn vị; $b_{1j}$ đều trên $[-1,1]$; $\chi(x)=\operatorname{ReLU}(\Theta_1x+b_1)/\sqrt N$, với các hàng $v_j^\top$ của $\Theta_1$.
- **Huấn luyện.** Nghiệm nội suy chuẩn nhỏ nhất $\hat w$: véc-tơ có chuẩn nhỏ nhất trong các $w$ thỏa $\langle w,\chi(x_i)\rangle=\tilde y_i$ với mọi $i$, tính bằng bình phương tối thiểu (hàm `numpy.linalg.lstsq`). Nghiệm tồn tại vì ma trận đặc trưng $200\times2000$ có hạng $200$. Đây cũng là giới hạn của hạ gradient trên $\frac12\sum_i(\langle w,\chi(x_i)\rangle-\tilde y_i)^2$ khởi tạo tại $0$ với độ dài bước đủ nhỏ: mọi điểm lặp nằm trong không gian hàng của ma trận đặc trưng, và trong không gian đó chỉ có một nghiệm nội suy.
- **Lặp lại.** Mười hạt giống $0,1,\ldots,9$, mỗi hạt giống khởi tạo bộ sinh số ngẫu nhiên `numpy.random.default_rng`; thứ tự rút cố định: điểm huấn luyện, điểm kiểm tra, lớp ẩn ($v_j$ rồi $b_{1j}$), hoán vị huấn luyện, hoán vị kiểm tra.
- **Đại lượng đo.** Lỗi huấn luyện và lỗi kiểm tra 0–1; $\lVert\hat w\rVert$; lề nhỏ nhất $\gamma=\min_i\tilde y_i\langle\hat w,\chi(x_i)\rangle$; $C_x$ của Ví dụ 07.10; lề chuẩn hóa $\gamma/(\lVert\hat w\rVert C_x)$; số hạng Rademacher $2\lVert\hat w\rVert C_x/(\gamma\sqrt m)$; chuẩn $\lVert\hat w\rVert/\sqrt N$ của $\Theta_2$; hạng của ma trận đặc trưng.

Kết quả của mười lần chạy: lỗi huấn luyện bằng $0$ trong mọi lần chạy; lỗi kiểm tra trung bình $0{,}023$ (độ lệch chuẩn $0{,}0074$) với nhãn thật và $0{,}501$ (độ lệch chuẩn $0{,}0095$) với nhãn hoán vị; lề nhỏ nhất bằng $1$; hạng bằng $200$ trong mọi lần chạy; $C_x$ từ $1{,}518$ đến $1{,}544$. Các khoảng quan sát được làm tròn đến giá trị gần nhất; chỉ cận trên của các định lý được làm tròn lên.
