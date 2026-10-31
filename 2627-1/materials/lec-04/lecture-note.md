# Bài 04 — Phân tích sai số, tối thiểu hóa rủi ro cấu trúc và chọn mô hình

Hệ quả 02.16 và Hệ quả 03.16 chặn rủi ro vượt mức (excess risk) của tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM) so với mức tốt nhất của một lớp giả thuyết (hypothesis class) cố định. Bài 03 kết thúc bằng một câu hỏi khác, đã đặt ra từ đẳng thức sau Định nghĩa 01.24: với cỡ mẫu cho trước, nên chọn lớp nào trong một dãy lớp lồng nhau?

Câu hỏi trung tâm của bài là chọn độ phức tạp của mô hình theo cỡ mẫu. Các công cụ là phân tích sai số (error decomposition), phân tích độ chệch–phương sai (bias–variance decomposition), chia xác suất thất bại (confidence allocation) giữa các lớp, tối thiểu hóa rủi ro cấu trúc (structural risk minimization, SRM) với số hạng phạt (penalty), và mẫu xác thực (validation sample).

## Câu hỏi mở đầu

Cho $16$ quan sát $(x_i,y_i)$ với các $x_i\in\mathbb R$ đôi một khác nhau. Ta khớp đa thức bậc $1$, bậc $3$ và bậc $15$ bằng bình phương tối thiểu (least squares). Lớp đa thức bậc không quá $1$ nằm trong lớp bậc không quá $3$, lớp này nằm trong lớp bậc không quá $15$, nên rủi ro thực nghiệm (empirical risk) của nghiệm bậc $3$ không lớn hơn của nghiệm bậc $1$. Đa thức bậc $15$ đi qua cả $16$ điểm, nên rủi ro thực nghiệm của nó bằng $0$.

**Câu hỏi.** Có nên chọn bậc $15$ vì rủi ro thực nghiệm của nó nhỏ nhất không? Nếu không, quy tắc chọn bậc nào có bảo đảm cho rủi ro kì vọng (population risk)?

Không. Trên một dãy lớp lồng nhau, lớp lớn nhất luôn đạt rủi ro thực nghiệm nhỏ nhất, với mọi cỡ mẫu, nên quy tắc này không dùng đến cỡ mẫu. Cận cho rủi ro vượt mức so với lớp lại tăng theo độ phức tạp của lớp: ở §11 của Bài 03, với $10^4$ quan sát, cận này tăng từ $0{,}329$ lên $0{,}560$ khi chuyển từ hai lên mười chỉ số đo. Quy tắc cần cộng vào rủi ro thực nghiệm một số hạng phạt rút ra từ chính cận đó (§6).

Hàm lỗi bình phương (squared loss) không bị chặn, nên câu trả lời bằng số ở §6 dùng phân lớp với hàm lỗi 0–1 (0–1 loss). Ví dụ ba điểm ở §5 chỉ ra vì sao bậc cao không luôn tốt hơn; với nhãn bị chặn, §8 cho một cận khi chọn bậc bằng mẫu xác thực.

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Viết rủi ro của một hàm dự đoán học được thành sai số xấp xỉ cộng sai số ước lượng, chặn sai số ước lượng bằng một số hạng thống kê cộng sai số tối ưu thực nghiệm, và chỉ ra phần nào là đẳng thức, phần nào chỉ là cận.
2. Chứng minh phân tích độ chệch–phương sai tại một điểm cho hàm lỗi bình phương, chỉ ra chỗ cần nhãn kiểm tra độc lập với mẫu, và giải thích vì sao độ chệch khác sai số xấp xỉ.
3. Chia xác suất thất bại cho một họ đếm được các lớp bằng trọng số, chứng minh bất đẳng thức oracle cho tối thiểu hóa rủi ro cấu trúc, và tính lựa chọn của quy tắc này từ một bảng rủi ro thực nghiệm và số hạng phạt.
4. Định nghĩa học không đều, so sánh với học PAC bất khả tri, và chỉ ra một lớp học được không đều nhưng không học được PAC.
5. Tính cận cho chọn mô hình bằng mẫu xác thực, nêu điều kiện độc lập mà cận cần, và dựng phản ví dụ khi họ lớp hay mẫu xác thực được chọn sau khi xem dữ liệu, hoặc khi xác suất thất bại không được chia.

## Kiến thức tiên quyết

- **Từ Bài 01.**
  - Thuật toán học (Định nghĩa 01.4); ERM, $\epsilon_{\mathrm{opt}}$-ERM và hai mức (O1), (O2) (Định nghĩa 01.6, 01.8, 01.12; Nhận xét 01.9, 01.11; Ví dụ 01.6, 01.7).
  - Hàm lỗi bình phương (Ví dụ 01.3, Nhận xét 01.2); rủi ro Bayes, rủi ro vượt mức và đẳng thức sau Định nghĩa 01.24; học PAC bất khả tri (Định nghĩa 01.25, Nhận xét 01.19, 01.26); ví dụ sàng lọc dưới $D_\eta$ (Ví dụ 01.1, 01.2, 01.10).
- **Từ Bài 02.** Hệ quả 02.10; bất đẳng thức hợp (union bound; Bổ đề 02.12) và dạng đếm được ngay sau nó; mẫu $\epsilon$-đại diện (Định nghĩa 02.13); Định lý 02.14, Hệ quả 02.16, Ví dụ 02.8; Nhận xét 02.11; Bài tập 02.4, 02.6, 02.11; các giả thiết (T1)–(T4).
- **Từ Bài 03.** Giả thiết (T5), điều kiện (M), Nhận xét 03.14; chiều VC (Vapnik–Chervonenkis dimension) của nửa không gian afin (Mệnh đề 03.9); Định lý 03.15 với bán kính VC $\rho_m$; Hệ quả 03.16; Định lý 03.17(a); Ví dụ 03.6, 03.7, 03.8; cầu nối ở §11 của Bài 03.
- **Xác suất và giải tích.** Phương sai, hiệp phương sai; $\mathbb E[UW]=\mathbb EU\,\mathbb EW$ khi $U$, $W$ độc lập; bất đẳng thức Cauchy–Schwarz; $\sum_{k\ge1}1/k^2=\pi^2/6$.

**Câu hỏi ôn nhanh.**

1. Với lớp hữu hạn $K=10$ giả thuyết, $m=1000$ và $\delta=0{,}05$, tính bán kính $r_m$ của Định lý 02.14(a).
2. Cho các biến cố $B_1,B_2,\ldots$ với $\Pr(B_k)\le0{,}05\cdot2^{-k}$. Chặn $\Pr\big(\bigcup_kB_k\big)$.
3. Cho biến ngẫu nhiên $U$ với $\mathbb EU^2<\infty$ và hằng số $c$. Chứng minh $\mathbb E(U-c)^2=\operatorname{Var}(U)+(\mathbb EU-c)^2$.

::: solution Lời giải câu hỏi ôn nhanh
1. Ta có $2K/\delta=400$ và $\ln400\approx5{,}9915$, nên
$$
\begin{aligned}
r_m&=\sqrt{5{,}9915/2000}\\
&\approx0{,}0547.
\end{aligned}
$$
2. Theo dạng đếm được của bất đẳng thức hợp,
$$
\begin{aligned}
\Pr\Big(\bigcup_kB_k\Big)&\le0{,}05\sum_{k\ge1}2^{-k}\\
&=0{,}05.
\end{aligned}
$$
3. Viết $U-c=(U-\mathbb EU)+(\mathbb EU-c)$, bình phương và lấy kì vọng; số hạng chéo $2(\mathbb EU-c)\,\mathbb E[U-\mathbb EU]$ bằng $0$, nên
$$
\begin{aligned}
&\mathbb E(U-c)^2\\
&=\operatorname{Var}(U)\\
&\quad+(\mathbb EU-c)^2 .
\end{aligned}
$$
:::

## 1. Thiết lập bài toán

Bài toán giữ tám thành phần của §1 Bài 01, với hai thay đổi: một họ lớp thay cho một lớp, và độ chính xác của bộ giải (solver), tức thủ tục tối ưu trả về một giả thuyết, được tính vào tài nguyên.

1. **Tập quan sát và phân bố dữ liệu.** $\mathcal Z=\mathcal X\times\mathcal Y$, với $\mathcal Y=\{0,1\}$, trừ §5 và một nhận xét ở §8, nơi $\mathcal Y=\mathbb R$; $D$ cố định nhưng chưa biết.
2. **Mẫu.** $S=(Z_1,\ldots,Z_m)\sim D^m$ theo (T1); thêm một mẫu xác thực độc lập ở §8; đầu vào không ngẫu nhiên ở §5.
3. **Họ lớp giả thuyết.** Một danh sách hữu hạn hoặc đếm được $\mathcal H_1,\mathcal H_2,\ldots$, chọn trước khi lấy mẫu, không nhất thiết lồng nhau.
4. **Hàm lỗi.** Thỏa (T2) và (T3), tức nhận giá trị trong $[0,1]$, như hàm lỗi 0–1; hàm lỗi bình phương ở §5 và, sau khi cắt dự đoán, ở §8.
5. **Quy tắc dùng mẫu.** Một bộ giải bất kì trên một lớp (§4), SRM (§6–§7), chọn theo mẫu xác thực (§8).
6. **Mục tiêu.** Rủi ro kì vọng nhỏ cho hàm được chọn.
7. **Đối tượng so sánh.** Một rủi ro tham chiếu (§4); mức tốt nhất của từng lớp; mức tốt nhất của từng lớp cộng số hạng phạt, lấy nhỏ nhất theo lớp (§6); ứng viên (candidate) tốt nhất (§8).
8. **Tài nguyên.** Cỡ mẫu $m$, cỡ mẫu xác thực và độ chính xác của bộ giải. Thời gian tính chưa được xét (Bài 05).

Các đại lượng của bài chia theo nguồn ngẫu nhiên như bảng dưới.

| Loại | Đại lượng |
|---|---|
| Cố định | $D$, các lớp, trọng số và số hạng phạt của các lớp, $\delta$, mỗi $h$, $L_D(h)$, $\inf_{h\in\mathcal H_k}L_D(h)$, rủi ro tham chiếu |
| Ngẫu nhiên theo $S\sim D^m$ | $L_S(h)$, chỉ số lớp được chọn, hàm được chọn và rủi ro kì vọng của nó, sai số tối ưu thực nghiệm |
| Thêm ở §8 | các ứng viên (ngẫu nhiên qua $S$), rủi ro trên mẫu xác thực, ứng viên được chọn |

## 2. Kí hiệu và giả thiết

Kí hiệu chung theo bảng kí hiệu của học phần. Bảng dưới gồm các kí hiệu dùng từ §3; kí hiệu khác được đặt tên tại định nghĩa.

| Kí hiệu | Ý nghĩa |
|---|---|
| $\mathcal P_j$ | lớp đa thức một biến bậc không quá $j$ |
| $\mathcal H_k$, $k$ | lớp thứ $k$ của một họ lớp; chỉ số lớp |
| $k_{\max}$ | số lớp của một họ lớp hữu hạn |
| $K$ | số phần tử của một danh sách hữu hạn giả thuyết hay ứng viên |
| $d_k$ | chiều VC của $\mathcal H_k$ |
| $p$ | số chiều đặc trưng, $p=10$ trong ứng dụng ở §3 |
| $\epsilon$ | tham số độ chính xác: so với một giả thuyết cho trước ở §7, so với ứng viên tốt nhất ở §8 |

Các giả thiết (T1), (T2), (T3), (T5), (M) được dùng lại; (T6) và (T7) được nêu ở §6 và §8. Giả thiết tối ưu gồm (O1), (O2) và độ chính xác của SRM (§6); giả thiết riêng của §5 nằm trong khối kết quả. Không kết quả nào dùng giả thiết lồi, trơn hay Lipschitz.

## 3. Ví dụ xuyên suốt

::: example Ví dụ 04.1 (Ba bậc đa thức trên ba điểm thiết kế)
**Thiết lập.** Ba hoành độ cố định $x_1=-1$, $x_2=0$, $x_3=1$; đầu vào không ngẫu nhiên, nên đây là một *thiết kế cố định* (fixed design). Nhãn là
$$
Y_i=x_i^2+\zeta_i,\qquad i=1,2,3,
$$
trong đó nhiễu $\zeta_1,\zeta_2,\zeta_3$ độc lập, có kì vọng $0$ và phương sai $\sigma^2>0$. Hàm lỗi bình phương, mẫu $S=((x_i,Y_i))_{i=1}^3$ và
$$
L_S(f)=\tfrac13\textstyle\sum_{i=1}^3\big(f(x_i)-Y_i\big)^2 .
$$
Với $j\in\{0,1,2\}$, $\hat f^{(j)}$ là nghiệm bình phương tối thiểu trên $\mathcal P_j$, tức nghiệm ERM trên lớp đó. Chỉ các nhãn là ngẫu nhiên.

**Bước 1: lớp lồng nhau.** Một đa thức bậc không quá $j$ cũng có bậc không quá $j+1$, nên $\mathcal P_0\subset\mathcal P_1\subset\mathcal P_2$.

**Bước 2: rủi ro thực nghiệm không tăng theo bậc.** Vì $\hat f^{(j)}\in\mathcal P_{j+1}$, ta có $L_S(\hat f^{(j+1)})\le L_S(\hat f^{(j)})$.

**Bước 3: bậc $2$ nội suy ba điểm.** Ba hoành độ đôi một khác nhau, nên ma trận Vandermonde $3\times3$ của chúng khả nghịch. Do đó có đúng một đa thức bậc không quá $2$ đi qua ba điểm $(x_i,Y_i)$, và $L_S(\hat f^{(2)})=0$ trên mọi mẫu.

**Kết luận.** Bậc $2$ đạt rủi ro thực nghiệm nhỏ nhất trên mọi mẫu, với mọi $\sigma^2$. Rủi ro thực nghiệm vì vậy không cho biết bậc nào dự đoán tốt hơn trên một nhãn mới.
:::

::: application Chọn số chỉ số đo cho hàm phân lớp tuyến tính
**Đặc trưng.** Mỗi người được mô tả bởi $p=10$ chỉ số đo, $x\in\mathbb R^{10}$, xếp theo một thứ tự cố định trước khi lấy mẫu.

**Họ lớp.** Với $k=1,\ldots,10$, lớp $\mathcal H_k$ gồm các hàm
$$
\begin{aligned}
x\mapsto\mathbb 1[&w_1x_1+\cdots+w_kx_k\\
&+b\ge0],
\end{aligned}
$$
với $w\in\mathbb R^k$ và $b\in\mathbb R$; hàm phân lớp chỉ dùng $k$ chỉ số đo đầu tiên. Đặt hệ số $w_{k+1}=0$, ta thấy $\mathcal H_k\subset\mathcal H_{k+1}$; lớp $\mathcal H_{10}$ là lớp $\mathcal H^{10}_{\mathrm{aff}}$ của Bài 03.

**Chiều VC và điều kiện đo được.** $d_k=k+1$, theo Mệnh đề 03.9 qua phép chiếu lên $k$ tọa độ đầu, và mỗi $\mathcal H_k$ thỏa (M) với lớp con gồm các tham số hữu tỉ (Phụ lục C).

**Câu hỏi thực hành.** Với $m=10^4$ quan sát và $\delta=0{,}05$, nên dùng bao nhiêu chỉ số đo? Các rủi ro thực nghiệm dùng ở §6 là giá trị giả định.
:::

Trong cả hai ví dụ, các lớp lồng nhau và rủi ro thực nghiệm của nghiệm ERM không tăng theo lớp. Để chọn lớp, chúng ta cần tách rủi ro của hàm học được thành một phần không tăng theo lớp và một phần mà cận của nó tăng theo lớp.

## 4. Sai số xấp xỉ, sai số ước lượng và sai số tối ưu thực nghiệm

Hệ quả 03.16(b) chặn $L_D(A(S))-\inf_{h\in\mathcal H}L_D(h)$ cho một $\epsilon_{\mathrm{opt}}$-ERM trên một lớp cố định. Khi lớp thay đổi, đối tượng so sánh $\inf_{h\in\mathcal H}L_D(h)$ cũng đổi theo, nên chúng ta cần một mức tham chiếu chung cho mọi lớp được so sánh.

::: definition Định nghĩa 04.1 (Rủi ro tham chiếu, sai số xấp xỉ và sai số ước lượng)
Cho phân bố $D$, lớp $\mathcal H$ và hàm lỗi $\ell$ thỏa (T2), với $L_D(h)<\infty$ cho mọi $h\in\mathcal H$. Ba đại lượng sau được định nghĩa.

- **Rủi ro tham chiếu.** Một số thực $L^*$, chọn trước và không phụ thuộc mẫu, với $L^*\le\inf_{h\in\mathcal H}L_D(h)$, được gọi là *rủi ro tham chiếu* (reference risk). Trong phân lớp thường lấy $L^*=L_D^{\mathrm{Bayes}}$, hoặc lấy $L^*$ là cận dưới đúng của $L_D$ trên một lớp lớn hơn chứa $\mathcal H$.
- **Sai số xấp xỉ.** Số $\inf_{h\in\mathcal H}L_D(h)-L^*\ge0$ được gọi là *sai số xấp xỉ* (approximation error) của $\mathcal H$.
- **Sai số ước lượng.** Với $h\in\mathcal H$, số $L_D(h)-\inf_{h'\in\mathcal H}L_D(h')\ge0$ được gọi là *sai số ước lượng* (estimation error) của $h$; đó là rủi ro vượt mức của $h$ so với $\mathcal H$ (Định nghĩa 01.24).
:::

Với mọi $h\in\mathcal H$, hai số hạng cộng lại đúng bằng rủi ro của $h$ so với mức tham chiếu:
$$
\begin{aligned}
&L_D(h)-L^*\\
&\quad=\Big[\inf_{h'\in\mathcal H}L_D(h')-L^*\Big]\\
&\qquad+\Big[L_D(h)-\inf_{h'\in\mathcal H}L_D(h')\Big].
\end{aligned}
$$
Với $L^*=L_D^{\mathrm{Bayes}}$, đây là đẳng thức sau Định nghĩa 01.24. Sai số xấp xỉ là một số tất định: nó phụ thuộc $D$, $\mathcal H$ và $L^*$, không phụ thuộc mẫu. Với cùng $L^*$, nó không tăng khi lớp lớn hơn, vì cận dưới đúng trên một tập lớn hơn không lớn hơn. Với $h=A(S)$, sai số ước lượng là một biến ngẫu nhiên theo $S$.

Khi so một họ lớp, ta dùng một $L^*$ chung, chẳng hạn rủi ro Bayes. Định nghĩa không cần hàm lỗi bị chặn; các kết quả với xác suất cao dưới đây mới cần (T3).

::: example Ví dụ 04.2 (Hai số hạng trong ví dụ sàng lọc)
**Thiết lập.** Phân bố $D_\eta$ của Ví dụ 01.1, lớp sáu hàm ngưỡng $h_t$, hàm lỗi 0–1 và $L^*=L^{\mathrm{Bayes}}_{D_\eta}=0{,}18$ (Ví dụ 01.10).

**Bước 1: sai số xấp xỉ.** Theo Ví dụ 01.2, $\min_tL_{D_\eta}(h_t)=L_{D_\eta}(h_3)=0{,}22$, nên sai số xấp xỉ của lớp là
$$
0{,}22-0{,}18=0{,}04 .
$$

**Bước 2: sai số ước lượng của $h_2$.** Theo Ví dụ 01.2, $L_{D_\eta}(h_2)=0{,}32$, nên sai số ước lượng của $h_2$ là
$$
0{,}32-0{,}22=0{,}10 .
$$

**Bước 3: tổng.** $0{,}04+0{,}10=0{,}14$, bằng $L_{D_\eta}(h_2)-L^*=0{,}32-0{,}18$.

**Bước 4: lớp lớn hơn.** Trên lớp mọi hàm $\{1,\ldots,5\}\to\{0,1\}$, hàm phân lớp tối ưu Bayes $h_{\mathrm{Bayes}}=\mathbb 1[x\in\{3,5\}]$ thuộc lớp, nên với cùng $L^*$ sai số xấp xỉ bằng $0$.

**Kết luận.** Giới hạn vào lớp hàm ngưỡng làm rủi ro tăng $0{,}04$ so với rủi ro Bayes; chọn $h_2$ thay cho $h_3$ làm rủi ro tăng thêm $0{,}10$.
:::

Với cùng $D_\eta$ và lớp sáu hàm ngưỡng, số $0{,}25$ không phải rủi ro tham chiếu: nó lớn hơn mức tốt nhất $0{,}22$ của lớp, và "sai số xấp xỉ" tương ứng bằng $-0{,}03$.

Sai số ước lượng của $A(S)$ gộp hai nguồn: mẫu hữu hạn và bộ giải không tìm đúng nghiệm ERM. Nguồn thứ hai được đo trên chính mẫu.

::: definition Định nghĩa 04.2 (Sai số tối ưu thực nghiệm)
Cho lớp $\mathcal H$, hàm lỗi $\ell\ge0$, một mẫu $s\in\mathcal Z^m$ và $\tilde h\in\mathcal H$. *Sai số tối ưu thực nghiệm* (empirical optimization error) của $\tilde h$ trên $s$ là
$$
\operatorname{opt}_s(\tilde h)=L_s(\tilde h)-\inf_{h\in\mathcal H}L_s(h).
$$
:::

Vì $\ell\ge0$, $\operatorname{opt}_s(\tilde h)$ xác định và không âm, kể cả khi cận dưới đúng không đạt; $\tilde h$ là đầu ra của một bộ giải bất kì. Với $S\sim D^m$, $\operatorname{opt}_S(A(S))$ là một hàm của mẫu, tính được mà không cần biết $D$, nhưng phân bố của nó phụ thuộc $D$; với lớp vô hạn, tính đo được của nó cần thêm điều kiện như (M). Thuật toán $A$ là một $\epsilon_{\mathrm{opt}}$-ERM (Định nghĩa 01.12) khi và chỉ khi $\operatorname{opt}_S(A(S))\le\epsilon_{\mathrm{opt}}$ trên mọi mẫu.

Trong Ví dụ 01.7, lớp $\mathcal H_+$ trên mẫu $S=((1,0))$ có $\inf_{w>0}L_S(h_w)=0$, nên $\operatorname{opt}_S(h_w)=w^2$.

::: proposition Mệnh đề 04.3 (Cận trên ba thành phần cho rủi ro vượt mức) — chứng minh đầy đủ
**Giả thiết.** Năm thành phần sau.

- **Lớp và hàm lỗi.** $\mathcal H$ bất kì; $\ell$ thỏa (T2) và (T3).
- **Rủi ro tham chiếu.** $L^*$ như ở Định nghĩa 04.1.
- **Đầu ra.** $\tilde h=\tilde h(S)\in\mathcal H$, do một quy tắc đo được bất kì trả về, không cần là ERM.
- **Bán kính.** $r>0$.
- **Mẫu và lớp, cho phần (b).** $S\sim D^m$ theo (T1), $\delta\in(0,1)$, và một trong hai trường hợp: $\mathcal H$ thỏa (T4) với $r=r_m$ của Định lý 02.14(a); hoặc hàm lỗi 0–1, $\mathcal H$ thỏa (T5), (M) với $r=\rho_m$ của Định lý 03.15(a).

**Bảo đảm.** Hai khẳng định.

- **(a) Dạng tất định.** Nếu $S$ là $r$-đại diện đối với $(\mathcal H,\ell,D)$ (Định nghĩa 02.13) thì
  $$
  \begin{aligned}
  &L_D(\tilde h)-L^*\\
  &\le\Big[\inf_{h\in\mathcal H}L_D(h)-L^*\Big]\\
  &\quad+2r+\operatorname{opt}_S(\tilde h).
  \end{aligned}
  $$
- **(b) Dạng xác suất cao.** Với xác suất ít nhất $1-\delta$ theo $S\sim D^m$, bất đẳng thức ở (a) đúng đồng thời cho mọi quy tắc.

Ba số hạng là sai số xấp xỉ (tất định), cận thống kê $2r$ của lớp (phụ thuộc $m$, $\delta$ và $\lvert\mathcal H\rvert$ hoặc hàm tăng trưởng) và đại lượng thực nghiệm $\operatorname{opt}_S(\tilde h)$ của bộ giải.
:::

::: proof Chứng minh Mệnh đề 04.3
**Lộ trình.** Thêm bớt rủi ro thực nghiệm, như Bước 1 của chứng minh Hệ quả 03.16. Bất đẳng thức then chốt là tính đại diện, dùng hai lần.

**Bước 1 (so với một $h$ cố định).** Giả sử $S$ là $r$-đại diện. Với mọi $h\in\mathcal H$,
$$
\begin{aligned}
L_D(\tilde h)&\le L_S(\tilde h)+r\\
&=\inf_{h'\in\mathcal H}L_S(h')\\
&\quad+\operatorname{opt}_S(\tilde h)+r\\
&\le L_S(h)+\operatorname{opt}_S(\tilde h)\\
&\quad+r\\
&\le L_D(h)+2r\\
&\quad+\operatorname{opt}_S(\tilde h).
\end{aligned}
$$
Bất đẳng thức thứ nhất dùng tính đại diện tại $\tilde h$; đây là chỗ cần cận đều, vì $\tilde h$ được chọn theo $S$. Đẳng thức tiếp theo là Định nghĩa 04.2. Bất đẳng thức thứ hai dùng định nghĩa của cận dưới đúng. Bất đẳng thức thứ ba dùng tính đại diện tại $h$.

**Bước 2 (cận dưới đúng).** Vế trái không phụ thuộc $h$. Lấy cận dưới đúng theo $h\in\mathcal H$ ở vế phải rồi trừ $L^*$ ở hai vế, ta được (a). Không bước nào cần $\inf_{h}L_D(h)$ hay $\inf_{h}L_S(h)$ đạt được; điều kiện $L^*\le\inf_hL_D(h)$ chỉ làm số hạng thứ nhất không âm.

**Bước 3 (phần b).** Theo Định lý 02.14(a), hoặc Định lý 03.15(a), biến cố "$S$ là $r$-đại diện" có xác suất ít nhất $1-\delta$. Các giả thiết (T1), (T3) và (T4), hoặc (T1), (T5), (M), chỉ được dùng ở bước này. Biến cố không phụ thuộc quy tắc chọn $\tilde h$, nên (a) đúng đồng thời cho mọi quy tắc.

$\square$ Với $L^*=\inf_{h\in\mathcal H}L_D(h)$ và $\operatorname{opt}_S\le\epsilon_{\mathrm{opt}}$, phần (b) trở về Hệ quả 02.16(b) và 03.16(b). Cận có hai số hạng riêng, $2r$ do mẫu hữu hạn và $\operatorname{opt}_S$ do bộ giải; bản thân sai số ước lượng không được tách thành hai phần.
:::

::: example Ví dụ 04.3 (Cận ba thành phần cho hai lớp của ứng dụng)
**Thiết lập.** Ứng dụng ở §3 với $\mathcal H_2$ ($d_2=3$) và $\mathcal H_{10}$ ($d_{10}=11$); hàm lỗi 0–1, $m=10^4$, $\delta=0{,}05$, $L^*=L_D^{\mathrm{Bayes}}$ chưa biết. Bộ giải là một $\epsilon_{\mathrm{opt}}$-ERM với $\epsilon_{\mathrm{opt}}=0{,}01$, nên $\operatorname{opt}_S\le0{,}01$. Gọi $a_2$, $a_{10}$ là sai số xấp xỉ của hai lớp.

**Bước 1: bán kính.** Theo Định lý 03.15(b) (Ví dụ 03.7), $\rho_m$ không vượt dạng trực tiếp, $\approx0{,}16443$ với $d=3$ và $\approx0{,}27992$ với $d=11$; mẫu $\rho_m$-đại diện cũng đại diện với bán kính lớn hơn.

**Bước 2: hai cận.** Theo Mệnh đề 04.3(b), mỗi bất đẳng thức sau đúng với xác suất ít nhất $0{,}95$:
$$
\begin{aligned}
&L_D(\tilde h_2)-L_D^{\mathrm{Bayes}}\\
&\quad\le a_2+2\rho_m+0{,}01\\
&\quad\approx a_2+2\cdot0{,}16443+0{,}01\\
&\quad\approx a_2+0{,}3389,\\
&L_D(\tilde h_{10})-L_D^{\mathrm{Bayes}}\\
&\quad\le a_{10}+2\rho_m+0{,}01\\
&\quad\approx a_{10}+2\cdot0{,}27992+0{,}01\\
&\quad\approx a_{10}+0{,}5698,
\end{aligned}
$$
trong đó $\tilde h_2$, $\tilde h_{10}$ là đầu ra của bộ giải trên hai lớp.

**Bước 3: sai số xấp xỉ.** Các lớp lồng nhau, nên $a_{10}\le a_2$; cả hai số đều chưa biết.

**Bước 4: so sánh.** Cận của $\mathcal H_{10}$ nhỏ hơn cận của $\mathcal H_2$ khi và chỉ khi
$$
\begin{aligned}
&a_2-a_{10}\\
&\quad>2(0{,}27992-0{,}16443)\\
&\quad\approx0{,}2310 .
\end{aligned}
$$

**Kết luận.** Chỉ phần thống kê của hai cận tính được. Hai cận chưa đúng đồng thời; để chọn lớp theo mẫu, chúng ta cần chia $\delta$ giữa các lớp (§6).
:::

::: remark Nhận xét 04.4 (Đẳng thức và cận trong phân tích sai số)
Ba điểm sau tách đẳng thức, cận và một hiệu mà học phần không dùng.

- **Đẳng thức.** $L_D(\tilde h)-L^*$ bằng đúng sai số xấp xỉ cộng sai số ước lượng (Định nghĩa 04.1).
- **Cận.** Mệnh đề 04.3 chặn sai số ước lượng bởi $2r+\operatorname{opt}_S(\tilde h)$. Sai số ước lượng gộp hiệu ứng thống kê và hiệu ứng tối ưu, và không được tách thành hai phần.
- **Hiệu theo rủi ro kì vọng.** Hiệu $L_D(\tilde h)-L_D(\hat h)$, với $\hat h$ là một nghiệm ERM, phụ thuộc nghiệm ERM được chọn ($0{,}32$ hay $0{,}28$ trên $S_\eta$, Ví dụ 01.6) và có thể âm, như phép tính dưới đây.

**Mẫu.** Dưới $D_\eta$, lấy $S=((1,0),(2,1))$.

**Nghiệm ERM.** Chỉ $h_2$ phân lớp đúng cả hai quan sát, nên $h_2$ là nghiệm ERM duy nhất, với $L_S(h_2)=0$ và $L_{D_\eta}(h_2)=0{,}32$.

**Đầu ra của bộ giải.** Với $\tilde h=h_3$, sai trên $(2,1)$, ta có $\operatorname{opt}_S(h_3)=\tfrac12$ và $L_{D_\eta}(h_3)=0{,}22$.

**Hiệu.** $L_{D_\eta}(h_3)-L_{D_\eta}(h_2)=0{,}22-0{,}32=-0{,}10$.

Vì vậy học phần dùng đại lượng thực nghiệm, không âm, $\operatorname{opt}_S$.
:::

Trong cận của Mệnh đề 04.3, sai số xấp xỉ không tăng khi lớp lớn hơn nhưng không quan sát được, còn số hạng $2r$ tăng theo lớp nhưng tính được. Ở §6, số hạng tính được trở thành một quy tắc chọn lớp. Trước đó, chúng ta xét phân tích độ chệch–phương sai (§5), dễ nhầm với phân tích sai số.

## 5. Độ chệch và phương sai với hàm lỗi bình phương

Ở Ví dụ 04.1, rủi ro thực nghiệm luôn chọn bậc $2$, còn Mệnh đề 04.3 cần hàm lỗi bị chặn. Để so các bậc trên một nhãn mới, chúng ta dùng một đẳng thức khác: kì vọng theo mẫu của lỗi kiểm tra tại một điểm, cho một thuật toán cố định.

::: definition Định nghĩa 04.5 (Hàm hồi quy, độ chệch và phương sai tại một điểm)
Cho ba đối tượng sau.

- **Điểm.** $x\in\mathcal X$ cố định.
- **Nhãn kiểm tra.** Một biến ngẫu nhiên $Y\in\mathbb R$ có phân bố của nhãn khi $X=x$, với $\mathbb EY^2<\infty$.
- **Ước lượng.** $\hat f_S(x)\in\mathbb R$, tính từ mẫu ngẫu nhiên $S$, với $\mathbb E_S\hat f_S(x)^2<\infty$.

Năm đại lượng sau được định nghĩa.

- **Hàm hồi quy.** $f^*(x)=\mathbb E[Y\mid X=x]$, giá trị tại $x$ của *hàm hồi quy* (regression function).
- **Phương sai nhiễu.** $\sigma^2(x)=\operatorname{Var}(Y\mid X=x)$, *phương sai nhiễu* (noise variance) tại $x$.
- **Dự đoán trung bình.** $\bar f(x)=\mathbb E_S\hat f_S(x)$, *dự đoán trung bình* (average prediction) tại $x$.
- **Độ chệch.** $\bar f(x)-f^*(x)$, *độ chệch* (bias) của ước lượng tại $x$.
- **Phương sai.** $\operatorname{Var}_S(\hat f_S(x))=\mathbb E_S\big(\hat f_S(x)-\bar f(x)\big)^2$, *phương sai* (variance) của ước lượng tại $x$.
:::

Kì vọng trong $\bar f(x)$ và $\operatorname{Var}_S$ lấy theo mẫu huấn luyện, với $x$ cố định. Số $\sigma^2(x)$ là phương sai của một nhãn mới tại $x$, khác các dấu ngẫu nhiên $\sigma_i$ của Bài 03.

Trong thiết kế cố định của Ví dụ 04.1, $f^*(x)=x^2$ và $\sigma^2(x)=\sigma^2$. Một hàm dự đoán đã huấn luyện xong rồi giữ cố định có phương sai $0$: phương sai là tính chất của thuật toán cùng phân bố của mẫu, không phải của một hàm.

::: proposition Mệnh đề 04.6 (Phân tích độ chệch–phương sai tại một điểm) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Điểm.** $x\in\mathcal X$ cố định.
- **Ước lượng.** $\hat f_S(x)$ như ở Định nghĩa 04.5; mẫu $S$ có phân bố bất kì, không cần độc lập cùng phân bố.
- **Nhãn kiểm tra.** $Y$ với $\mathbb EY=f^*(x)$ và $\operatorname{Var}(Y)=\sigma^2(x)<\infty$, độc lập với $S$.

**Bảo đảm.** *Lỗi kiểm tra kì vọng* (expected test error) tại $x$ là
$$
\begin{aligned}
&\mathbb E_{S,Y}\big(\hat f_S(x)-Y\big)^2\\
&\quad=\big(\bar f(x)-f^*(x)\big)^2\\
&\qquad+\operatorname{Var}_S\big(\hat f_S(x)\big)+\sigma^2(x).
\end{aligned}
$$
Đây là một đẳng thức chính xác theo kì vọng trên $(S,Y)$, cho một thuật toán tại một điểm. Nó không phải cận với xác suất cao hay bảo đảm cho lớp; hàm lỗi không cần bị chặn, và $m$ chỉ đi vào qua phân bố của $\hat f_S(x)$.
:::

::: proof Chứng minh Mệnh đề 04.6
**Lộ trình.** Tách $\hat f_S(x)-Y$ quanh hai kì vọng $\bar f(x)$ và $f^*(x)$, bình phương, rồi chứng minh ba số hạng chéo có kì vọng $0$. Tính độc lập chỉ được dùng ở một số hạng chéo.

**Bước 1 (tách).** Viết tắt $\hat f=\hat f_S(x)$, $\bar f=\bar f(x)$, $f^*=f^*(x)$. Ta có
$$
\begin{aligned}
\hat f-Y&=(\hat f-\bar f)+(\bar f-f^*)\\
&\quad+(f^*-Y).
\end{aligned}
$$
Bình phương vế phải cho ba bình phương và ba số hạng chéo, mỗi số hạng chéo có hệ số $2$.

**Bước 2 (khả tích).** Vì $\mathbb E\hat f^2<\infty$ và $\mathbb EY^2<\infty$, ba số hạng của Bước 1 có mô-men bậc hai hữu hạn, nên theo bất đẳng thức Cauchy–Schwarz mọi tích của chúng khả tích.

**Bước 3 (ba bình phương).** $\mathbb E(\hat f-\bar f)^2=\operatorname{Var}_S(\hat f)$; $(\bar f-f^*)^2$ là hằng số; $\mathbb E(f^*-Y)^2=\sigma^2(x)$ vì $\mathbb EY=f^*$.

**Bước 4 (hai số hạng chéo có một hằng số).** $2(\bar f-f^*)\,\mathbb E[\hat f-\bar f]=0$ vì $\mathbb E\hat f=\bar f$, và $2(\bar f-f^*)\,\mathbb E[f^*-Y]=0$ vì $\mathbb EY=f^*$.

**Bước 5 (số hạng chéo cần độc lập).** Vì $Y$ độc lập với $S$,
$$
\begin{aligned}
&2\,\mathbb E\big[(\hat f-\bar f)(f^*-Y)\big]\\
&\quad=2\,\mathbb E[\hat f-\bar f]\;\mathbb E[f^*-Y]\\
&\quad=0.
\end{aligned}
$$
Đây là chỗ duy nhất dùng giả thiết nhãn kiểm tra độc lập; chỉ cần $\hat f$ và $Y$ không tương quan.

$\square$ Lỗi kiểm tra kì vọng tại $x$ bằng hai đại lượng của thuật toán, độ chệch bình phương và phương sai, cộng phần nhiễu $\sigma^2(x)$ mà không thuật toán nào giảm được.
:::

Với một hàm $f$ cố định, tức $\hat f_S(x)=f(x)$ với mọi $S$, phương sai bằng $0$ và Mệnh đề 04.6 cho
$$
\begin{aligned}
&\mathbb E\big(f(x)-Y\big)^2\\
&\quad=\big(f(x)-f^*(x)\big)^2+\sigma^2(x)\\
&\quad\ge\sigma^2(x),
\end{aligned}
$$
dấu bằng khi $f(x)=f^*(x)$. Với *thiết kế ngẫu nhiên* (random design), tức đầu vào $X\sim D_{\mathcal X}$ và $(X,Y)$ độc lập với $S$, lấy thêm kì vọng theo $X$ (định lý Fubini, giả sử các hàm đo được) cho
$$
\begin{aligned}
&\mathbb E_S\big[L_D(\hat f_S)\big]\\
&\quad=\mathbb E_X\Big[\big(\bar f(X)-f^*(X)\big)^2\\
&\qquad+\operatorname{Var}_S\big(\hat f_S(X)\big)+\sigma^2(X)\Big].
\end{aligned}
$$
Theo bất đẳng thức trên, $\mathbb E\,\sigma^2(X)$ là giá trị nhỏ nhất của $L_D$ trên các hàm đo được, tức rủi ro Bayes của hàm lỗi bình phương, đạt tại $f^*$ (Bài tập 04.2).

::: example Ví dụ 04.4 (Độ chệch và phương sai của ba bậc đa thức)
**Thiết lập.** Như Ví dụ 04.1, với điểm kiểm tra $x_0=0{,}5$, $f^*(x_0)=0{,}25$ và nhãn kiểm tra $Y=0{,}25+\zeta$, độc lập với mẫu, có phương sai $\sigma^2$. Ngẫu nhiên chỉ đến từ nhiễu.

**Bước 1: dạng tuyến tính.** Mỗi dự đoán $\hat f^{(j)}(x_0)$ có dạng $\sum_iw_iY_i$ với trọng số cố định.

- **Bậc $0$.** Nghiệm là $\bar Y$, trọng số $(\tfrac13,\tfrac13,\tfrac13)$.
- **Bậc $1$, hệ số.** Nghiệm $\hat a+\hat bx$ giải hệ phương trình chuẩn (normal equations); vì $\sum_ix_i=0$ và $\sum_ix_i^2=2$, ta được $\hat a=\bar Y$ và $\hat b=(Y_3-Y_1)/2$ (Phụ lục C).
- **Bậc $1$, dự đoán.** $\hat f^{(1)}(0{,}5)=\hat a+0{,}5\,\hat b=\bar Y+\tfrac14(Y_3-Y_1)$, nên trọng số là $(\tfrac13-\tfrac14,\tfrac13,\tfrac13+\tfrac14)=(\tfrac1{12},\tfrac13,\tfrac7{12})$.
- **Bậc $2$.** Nghiệm là đa thức nội suy Lagrange; ba đa thức cơ sở tại $x_0$ có giá trị $(-\tfrac18,\tfrac34,\tfrac38)$ (Phụ lục C).

**Bước 2: dự đoán trung bình.** Vì $\mathbb EY_i=x_i^2$ và $(x_1^2,x_2^2,x_3^2)=(1,0,1)$, ta có $\bar f(x_0)=w_1+w_3$:
$$
\begin{aligned}
j=0:&\quad\tfrac13+\tfrac13=\tfrac23,\\
j=1:&\quad\tfrac1{12}+\tfrac7{12}=\tfrac23,\\
j=2:&\quad-\tfrac18+\tfrac38=\tfrac14.
\end{aligned}
$$

**Bước 3: độ chệch bình phương.** Với bậc $0$ và $1$, $(\tfrac23-\tfrac14)^2=(\tfrac5{12})^2=\tfrac{25}{144}\approx0{,}1736$. Với bậc $2$, độ chệch bằng $0$, vì $x^2\in\mathcal P_2$ được nội suy đúng.

**Bước 4: phương sai.** Các nhiễu độc lập, cùng phương sai $\sigma^2$, nên phương sai bằng $\sigma^2\sum_iw_i^2$:
$$
\begin{aligned}
j=0:&\quad\tfrac39\sigma^2\approx0{,}3333\,\sigma^2,\\
j=1:&\quad\tfrac{1+16+49}{144}\sigma^2\\
&\quad\approx0{,}4583\,\sigma^2,\\
j=2:&\quad\tfrac{1+36+9}{64}\sigma^2\\
&\quad=0{,}71875\,\sigma^2.
\end{aligned}
$$

**Bước 5: $\sigma^2=1$.** Độ chệch bình phương cộng phương sai là $0{,}1736+0{,}3333=0{,}5069$; $0{,}1736+0{,}4583=0{,}6319$; $0+0{,}7188=0{,}7188$. Bậc $0$ tốt nhất; lỗi kiểm tra kì vọng cộng thêm $\sigma^2=1$ cho cả ba bậc.

**Bước 6: $\sigma^2=0{,}1$.** Phương sai chia cho $10$: $0{,}1736+0{,}0333=0{,}2069$; $0{,}1736+0{,}0458=0{,}2194$; $0+0{,}0719=0{,}0719$. Bậc $2$ tốt nhất.

**Kết luận.** Bậc tốt nhất phụ thuộc mức nhiễu $\sigma^2$ và hàm hồi quy $f^*$, hai đại lượng chưa biết. Quy tắc chọn theo rủi ro thực nghiệm luôn chọn bậc $2$ (Ví dụ 04.1).
:::

Mệnh đề 04.6 cần nhãn kiểm tra độc lập với mẫu.

::: example Ví dụ 04.5 (Nhãn kiểm tra nằm trong mẫu)
**Thiết lập.** Không có đầu vào: $Y_1,\ldots,Y_m$ độc lập cùng phân bố, kì vọng $\mu$, phương sai $\sigma^2$; ước lượng $\hat f=\bar Y$; $m=4$, $\sigma^2=1$. Nhãn kiểm tra là $Y_1$, nằm trong mẫu, nên giả thiết độc lập của Mệnh đề 04.6 bị bỏ.

**Bước 1: giá trị nếu áp dụng Mệnh đề 04.6.** Độ chệch $0$, phương sai $\sigma^2/m=0{,}25$, nhiễu $\sigma^2=1$; tổng $1{,}25$.

**Bước 2: giá trị đúng.** Ta viết
$$
\begin{aligned}
\bar Y-Y_1&=-\tfrac{m-1}m(Y_1-\mu)\\
&\quad+\tfrac1m\textstyle\sum_{i\ge2}(Y_i-\mu).
\end{aligned}
$$
Các số hạng độc lập và có kì vọng $0$, nên
$$
\begin{aligned}
&\mathbb E(\bar Y-Y_1)^2\\
&\quad=\sigma^2\Big[\big(\tfrac{m-1}m\big)^2+\tfrac{m-1}{m^2}\Big]\\
&\quad=\sigma^2\,\tfrac{(m-1)(m-1+1)}{m^2}\\
&\quad=\sigma^2\,\tfrac{m-1}m=0{,}75 .
\end{aligned}
$$

**Bước 3: nguồn chênh lệch.** Hiệu $1{,}25-0{,}75=0{,}5=2\sigma^2/m$ đến từ số hạng chéo ở Bước 5 của chứng minh: $2\,\mathbb E[(\bar Y-\mu)(\mu-Y_1)]=-2\operatorname{Cov}(\bar Y,Y_1)=-2\sigma^2/m$.

**Kết luận.** Lỗi trên một nhãn đã dùng để huấn luyện thấp hơn lỗi trên một nhãn mới.
:::

Với nhãn trong $\{0,1\}$, đẳng thức vẫn đúng, nhưng cách đọc "cùng độ chệch thì phương sai nhỏ hơn tốt hơn" không còn đúng.

::: example Ví dụ 04.6 (Phân tích độ chệch–phương sai cho hàm phân lớp)
**Thiết lập.** Một điểm $x$ với $\eta(x)=0{,}9$, nhãn kiểm tra $Y\in\{0,1\}$ tại $x$, độc lập với mẫu, nên $f^*(x)=0{,}9$ và $\sigma^2(x)=0{,}09$. Khi dự đoán và nhãn thuộc $\{0,1\}$, $(\hat f-Y)^2=\mathbb 1[\hat f\ne Y]$. Thuật toán $A$ cho $\hat f_S(x)=1$ với xác suất $0{,}4$ theo $S$ và $0$ với xác suất $0{,}6$; thuật toán $B$ luôn cho $0$.

**Bước 1: lỗi 0–1.** Với $A$, dự đoán $1$ sai khi $Y=0$, dự đoán $0$ sai khi $Y=1$, nên lỗi là $0{,}4\cdot0{,}1+0{,}6\cdot0{,}9=0{,}58$. Với $B$, lỗi là $0{,}9$.

**Bước 2: đẳng thức vẫn đúng.** Với $A$, $\bar f(x)=0{,}4$, độ chệch bình phương $(0{,}4-0{,}9)^2=0{,}25$ và phương sai $0{,}4\cdot0{,}6=0{,}24$:
$$
\begin{aligned}
A:&\quad(0{,}4-0{,}9)^2+0{,}24\\
&\qquad+0{,}09=0{,}58,\\
B:&\quad0{,}81+0+0{,}09\\
&\qquad=0{,}90.
\end{aligned}
$$
Số $0{,}4$ là xác suất dự đoán nhãn $1$, không phải một nhãn.

**Bước 3: cách đọc cho hàm phân lớp.** *Độ chệch theo nghĩa phân lớp* là việc dự đoán đa số theo $S$ có khác hàm phân lớp tối ưu Bayes hay không. *Phương sai theo nghĩa phân lớp* là xác suất dự đoán khác dự đoán đa số. Cả $A$ và $B$ dự đoán đa số $0$, trong khi $h_{\mathrm{Bayes}}$ dự đoán $1$ tại $x$, nên hai thuật toán có cùng độ chệch theo nghĩa phân lớp; phương sai theo nghĩa phân lớp là $0{,}4$ với $A$ và $0$ với $B$.

**Bước 4: cách đọc bị bác bỏ.** Cách đọc "cùng độ chệch thì phương sai nhỏ hơn tốt hơn" sai ở đây: $A$ có phương sai theo nghĩa phân lớp lớn hơn và lỗi nhỏ hơn ($0{,}58$ so với $0{,}90$). Độ chệch bình phương của Mệnh đề 04.6 lại khác nhau ($0{,}25$ so với $0{,}81$), nên nó không đo độ chệch theo nghĩa phân lớp.

**Kết luận.** Với hàm phân lớp, đẳng thức đúng về số nhưng không cho đánh đổi độ chệch–phương sai: khi dự đoán đa số sai, tăng phương sai theo nghĩa phân lớp làm giảm lỗi.
:::

::: remark Nhận xét 04.7 (Độ chệch và sai số xấp xỉ)
Dự đoán trung bình $\bar f$ không nhất thiết thuộc lớp; độ chệch là tính chất của thuật toán, còn sai số xấp xỉ là tính chất của lớp. Ví dụ sau có độ chệch $0$ và sai số xấp xỉ $1$.

**Thiết lập.** Không có đầu vào; $Y=\pm1$, mỗi giá trị xác suất $\tfrac12$, nên $f^*=0$ và $\sigma^2=1$. Lớp gồm hai hàm hằng $+1$ và $-1$, hàm lỗi bình phương, mẫu $Y_1,\ldots,Y_m$ độc lập cùng phân bố với $m$ lẻ.

**Nghiệm ERM.** Với $c=\pm1$, $(c-Y_i)^2$ bằng $0$ khi $Y_i=c$ và $4$ khi $Y_i\ne c$, nên nghiệm ERM là dấu chiếm đa số $\operatorname{sign}(\bar Y)$, không có trường hợp bằng nhau vì $m$ lẻ. Do đối xứng, nó nhận $\pm1$ với xác suất $\tfrac12$ mỗi giá trị.

**Độ chệch và phương sai.** $\bar f=0=f^*$, nên độ chệch bằng $0$; phương sai bằng $1$.

**Sai số xấp xỉ.** Lấy $L^*=\sigma^2=1$, rủi ro Bayes của hàm lỗi bình phương (đoạn sau Mệnh đề 04.6). Với $c=\pm1$,
$$
\begin{aligned}
\mathbb E(c-Y)^2&=c^2-2c\,\mathbb EY+\mathbb EY^2\\
&=1-0+1=2,
\end{aligned}
$$
nên sai số xấp xỉ của lớp bằng $2-1=1$.

**Kết luận.** Độ chệch bằng $0$, nhưng mọi hàm của lớp có rủi ro lớn hơn rủi ro Bayes $1$.
:::

Phân tích độ chệch–phương sai giải thích vì sao bậc cao không luôn tốt hơn, nhưng không cho một quy tắc chọn từ dữ liệu, vì $f^*$ và $\sigma^2$ chưa biết. Quy tắc như vậy được dựng ở §6 từ số hạng thống kê của Mệnh đề 04.3, với hàm lỗi bị chặn.

## 6. Chia xác suất thất bại và tối thiểu hóa rủi ro cấu trúc

Ví dụ 04.3 so hai cận, mỗi cận đúng với xác suất $0{,}95$ cho một lớp chọn trước. Một quy tắc chọn lớp theo mẫu cần các cận đúng đồng thời cho mọi lớp có thể được chọn, như Định lý 02.14 cần cận đồng thời cho mọi giả thuyết. Chỉ số lớp $k$ chạy trên $\{1,\ldots,k_{\max}\}$ hoặc $\mathbb N$.

::: definition Định nghĩa 04.8 (Bán kính hội tụ đều của một lớp)
Cho lớp $\mathcal H$ và hàm lỗi $\ell$ thỏa (T2), (T3). Một hàm $\mathrm{rad}_{\mathcal H}:\mathbb N\times(0,1)\to[0,\infty)$ được gọi là *bán kính hội tụ đều* (uniform convergence radius) của $\mathcal H$ nếu nó có ba tính chất sau.

- **Tính tất định.** $\mathrm{rad}_{\mathcal H}$ được chọn trước khi lấy mẫu và không phụ thuộc $S$, $h$ hay $D$.
- **Tính đo được.** Với mọi $D$, $m\ge1$ và $\delta'\in(0,1)$, biến cố trong công thức dưới đây đo được.
- **Cận đều.** Với mọi phân bố $D$ trên $\mathcal Z$, mọi $m\ge1$ và mọi $\delta'\in(0,1)$,
  $$
  \begin{aligned}
  &\Pr_{S\sim D^m}\Big[\sup_{h\in\mathcal H}\lvert L_S(h)\\
  &\qquad-L_D(h)\rvert\\
  &\qquad\le\mathrm{rad}_{\mathcal H}(m,\delta')\Big]\\
  &\quad\ge1-\delta'.
  \end{aligned}
  $$
:::

Hai ví dụ từ Bài 02–03:

- **Lớp hữu hạn.** Lớp hữu hạn $\mathcal H$ thỏa (T4) có bán kính $\sqrt{\ln(2\lvert\mathcal H\rvert/\delta')/(2m)}$ (Định lý 02.14(a)).
- **Lớp có chiều VC hữu hạn.** Với hàm lỗi 0–1, lớp thỏa (T5), (M) có bán kính $\rho_m$ tính tại $\delta'$ (Định lý 03.15(a)).

Một hàm lớn hơn một bán kính cũng là bán kính, và độ lệch đều không vượt quá $1$. Do đó, với chiều VC $d\ge1$, theo Định lý 03.15(b), hàm
$$
\begin{aligned}
\mathrm{rad}(m,\delta')^2&=\tfrac8m\Big(d\ln\tfrac{2em}d\\
&\qquad+\ln\tfrac4{\delta'}\Big)
\end{aligned}
$$
khi $m\ge d$, và $\mathrm{rad}(m,\delta')=1$ khi $m<d$, cũng là một bán kính hội tụ đều. Ta gọi nó là *dạng chiều VC* (VC-dimension form) của bán kính.

Lớp $\mathcal M_{[0,1]}$ của Ví dụ 03.6 có độ lệch đều bằng $1$ trên mọi mẫu dưới phân bố của ví dụ đó, nên mọi bán kính hội tụ đều của nó không nhỏ hơn $1$ và không cho thông tin.

Để chia $\delta$ cho các lớp theo trọng số, chúng ta cần giả thiết sau (ý này có ở §9 của Bài 02).

- **(T6) Họ lớp cố định trước mẫu.** Danh sách $\mathcal H_1,\mathcal H_2,\ldots$ (hữu hạn hoặc đếm được), các bán kính hội tụ đều $\mathrm{rad}_k=\mathrm{rad}_{\mathcal H_k}$ và các trọng số $q_k>0$ với $\sum_kq_k\le1$ được chọn trước và không phụ thuộc $S$. Danh sách chứa mọi lớp có thể được xét sau này.

Giả thiết (T5) là (T6) với một lớp và $q_1=1$.

::: lemma Bổ đề 04.9 (Kiểm soát đồng thời trên một họ lớp) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau.

- **Mẫu.** $S\sim D^m$ theo (T1), $m\ge1$.
- **Hàm lỗi.** $\ell$ thỏa (T2) và (T3).
- **Họ lớp.** Các lớp, bán kính và trọng số thỏa (T6).
- **Tham số.** $\delta\in(0,1)$.

**Bảo đảm.** Đặt *số hạng phạt* của lớp $k$ là
$$
\mathrm{pen}_k=\mathrm{rad}_k(m,\delta q_k).
$$
Với xác suất ít nhất $1-\delta$ theo $S\sim D^m$, đồng thời cho mọi $k$ và mọi $h\in\mathcal H_k$,
$$
\lvert L_S(h)-L_D(h)\rvert\le\mathrm{pen}_k .
$$
Đây là bảo đảm với xác suất cao cho cả họ lớp, giữa đại lượng thực nghiệm và tổng thể; nó phụ thuộc $m$ qua $\mathrm{rad}_k$, và $\delta$, $q_k$ qua $\ln(1/\delta)+\ln(1/q_k)$.
:::

::: proof Chứng minh Bổ đề 04.9
**Lộ trình.** Áp dụng bất đẳng thức hợp trên các lớp, như Định lý 02.14 áp dụng nó trên các giả thuyết.

**Bước 1 (biến cố hỏng).** Với mỗi $k$, đặt
$$
\begin{aligned}
B_k=\Big\{&\sup_{h\in\mathcal H_k}\lvert L_S(h)-L_D(h)\rvert\\
&>\mathrm{pen}_k\Big\},
\end{aligned}
$$
đo được theo Định nghĩa 04.8. Biến cố của bổ đề là phần bù của $\bigcup_kB_k$.

**Bước 2 (từng lớp).** Vì $0<q_k\le\sum_jq_j\le1$, ta có $\delta q_k\in(0,1)$. Theo (T6), $\mathrm{rad}_k$ và $q_k$ không phụ thuộc $S$, nên Định nghĩa 04.8 với $\delta'=\delta q_k$ cho $\Pr(B_k)\le\delta q_k$. Các giả thiết (T1), (T3) đi vào qua bán kính.

**Bước 3 (hợp đếm được).** Theo dạng đếm được của bất đẳng thức hợp (sau Bổ đề 02.12),
$$
\begin{aligned}
\Pr\Big(\bigcup_kB_k\Big)&\le\sum_k\delta q_k\\
&\le\delta .
\end{aligned}
$$
Giả thiết $\sum_kq_k\le1$ của (T6) được dùng ở bất đẳng thức thứ hai.

$\square$ Tính đồng thời trên các lớp chỉ đòi thay $\delta$ bằng $\delta q_k$ trong bán kính của lớp $k$; Bài tập 02.6 là trường hợp mỗi lớp có một phần tử.
:::

::: example Ví dụ 04.7 (Giá của việc chia xác suất thất bại)
**Thiết lập.** Trọng số $q_k=6/(\pi^2k^2)$, $k\ge1$; ứng dụng ở §3 với dạng chiều VC của bán kính, $m=10^4$, $\delta=0{,}05$.

**Bước 1: tổng trọng số.** $\sum_k6/(\pi^2k^2)=\tfrac6{\pi^2}\cdot\tfrac{\pi^2}6=1$, đúng như (T6) đòi.

**Bước 2: số hạng của trọng số.** $\ln(1/q_k)=2\ln k+\ln(\pi^2/6)$, với $\ln(\pi^2/6)\approx0{,}4977$. Với $k=3$, giá trị là $2{,}1972+0{,}4977\approx2{,}695$; với $k=10$, là $4{,}6052+0{,}4977\approx5{,}103$.

**Bước 3: một ô đầy đủ, $k=3$, $d_3=4$.** Với $\ln80\approx4{,}382$,
$$
\begin{aligned}
&2em/d_3=2e\cdot10^4/4\approx13\,591,\\
&4\ln13\,591\approx38{,}069,\\
&\ln\tfrac4{0{,}05\,q_3}\approx4{,}382+2{,}695\\
&\quad=7{,}077,\\
&8(38{,}069+7{,}077)/10^4\\
&\quad\approx0{,}036117,
\end{aligned}
$$
nên $\mathrm{pen}_3\approx\sqrt{0{,}036117}\approx0{,}1900$. Không chia xác suất thất bại ($q=1$), cùng phép tính cho $0{,}1843$.

**Bước 4: hai lớp khác.** Với $k=2$ ($d=3$), bán kính tăng từ $0{,}1644$ lên $0{,}1690$; với $k=10$ ($d=11$), từ $0{,}2799$ lên $0{,}2871$.

**Kết luận.** Trên $k=1,\ldots,10$, chia xác suất thất bại làm bán kính tăng từ khoảng $1\%$ ($k=1$) đến khoảng $3{,}2\%$ ($k=4$) (Phụ lục C). Giá đó là số hạng $\ln(1/q_k)$ cộng thêm trong căn.
:::

Bổ đề 04.9 cần $\sum_kq_k\le1$.

::: example Ví dụ 04.8 (Xác suất thất bại không được chia)
**Thiết lập.** $\mathcal X=\{0,1\}^{k_{\max}}$, các tọa độ của $X$ độc lập, có phân bố $\mathrm{Bernoulli}(\tfrac12)$; nhãn $Y=0$ chắc chắn. Mỗi lớp có một phần tử, $\mathcal H_k=\{h_k\}$ với $h_k(x)=x_k$, $k=1,\ldots,k_{\max}$; hàm lỗi 0–1, $m=10$, $\delta=0{,}05$. Mọi $q_k=1$, nên $\sum_kq_k=k_{\max}>1$: ví dụ bỏ điều kiện tổng trọng số của (T6). Cấu trúc là của Bài tập 02.4, với $K=k_{\max}$ của bài tập đó.

**Bước 1: bán kính.** $L_D(h_k)=\tfrac12$. Bán kính của một lớp một phần tử tại $\delta$ (Hệ quả 02.10(b)) là
$$
\begin{aligned}
\sqrt{\tfrac{\ln(2/\delta)}{2m}}&=\sqrt{\tfrac{\ln40}{20}}\\
&\approx0{,}4295,
\end{aligned}
$$
nhỏ hơn $\tfrac12$.

**Bước 2: biến cố hỏng của một lớp.** $L_S(h_k)$ nhận giá trị trong $\{0;0{,}1;\ldots;1\}$, nên độ lệch $\lvert L_S(h_k)-\tfrac12\rvert$ vượt $0{,}4295$ khi và chỉ khi $L_S(h_k)\in\{0,1\}$. Mỗi giá trị có xác suất $2^{-10}$, nên biến cố hỏng của lớp $k$ có xác suất $2\cdot2^{-10}=2^{-9}$.

**Bước 3: xác suất thất bại.** Các biến cố hỏng độc lập theo $k$, nên kết luận của Bổ đề 04.9 sai với xác suất $1-(1-2^{-9})^{k_{\max}}$: $0{,}858$ khi $k_{\max}=1000$ và $0{,}99994$ khi $k_{\max}=5000$. Riêng biến cố có $k$ với $L_S(h_k)=0$ đã có xác suất $0{,}6236$ khi $k_{\max}=1000$ (Bài tập 02.4(b)).

**Bước 4: khi chia đều.** Với $q_k=1/k_{\max}$ và $k_{\max}=1000$, bán kính thành $\sqrt{\ln40\,000/20}\approx0{,}7279>\tfrac12$, nên bổ đề đúng trên mọi mẫu.

**Kết luận.** Bỏ điều kiện $\sum_kq_k\le1$, kết luận của Bổ đề 04.9 sai với xác suất $0{,}858$ thay vì không quá $0{,}05$, và xác suất này tiến về $1$ khi $k_{\max}\to\infty$.
:::

Trên biến cố của Bổ đề 04.9, $L_S(h)+\mathrm{pen}_k$ là một cận trên cho $L_D(h)$, đúng đồng thời cho mọi lớp. Quy tắc sau tối thiểu hóa cận trên đó.

::: definition Định nghĩa 04.10 (Tối thiểu hóa rủi ro cấu trúc)
Cho họ lớp, bán kính và trọng số thỏa (T6), $\delta\in(0,1)$, một mẫu $S$ cỡ $m$ và $\mathrm{pen}_k=\mathrm{rad}_k(m,\delta q_k)$ như ở Bổ đề 04.9. Ba thành phần sau được định nghĩa.

- **Mục tiêu có phạt.** Hàm $(k,h)\mapsto L_S(h)+\mathrm{pen}_k$ trên các cặp với $h\in\mathcal H_k$ được gọi là *mục tiêu có phạt* (penalized objective).
- **Dung sai.** Một số $\tau\ge0$ được gọi là *dung sai* (tolerance).
- **Nghiệm $\tau$-chính xác.** Một cặp $(\hat k,\hat h)$ với $\hat h\in\mathcal H_{\hat k}$ và
  $$
  \begin{aligned}
  &L_S(\hat h)+\mathrm{pen}_{\hat k}\\
  &\le\inf_k\inf_{h\in\mathcal H_k}\big[L_S(h)\\
  &\qquad+\mathrm{pen}_k\big]+\tau
  \end{aligned}
  $$
  được gọi là một *nghiệm $\tau$-chính xác* ($\tau$-accurate solution).

Một thuật toán học trả về một nghiệm $\tau$-chính xác trên mọi mẫu được gọi là *thuật toán SRM với dung sai $\tau$*; với $\tau=0$, ta gọi là SRM chính xác.
:::

Dung sai $\tau$ đo độ chính xác của lời giải bài toán có phạt trên cả họ, còn $\epsilon_{\mathrm{opt}}$ của Bài 01 đo bài toán trên một lớp. Một $h$ thuộc nhiều lớp có thể đi cùng bất kì lớp nào chứa nó; các lớp không cần lồng nhau; $\delta$ là một đầu vào của quy tắc. Với một lớp, SRM là ERM.

Nghiệm $\tau$-chính xác với $\tau>0$ luôn tồn tại, vì mục tiêu không âm. Với hàm lỗi 0–1, nghiệm chính xác tồn tại khi danh sách hữu hạn, hoặc khi $\mathrm{pen}_k\to\infty$, điều mà bán kính của Định lý 02.14(a) và $\rho_m$ thỏa (Phụ lục A).

::: theorem Định lý 04.11 (Bất đẳng thức oracle cho tối thiểu hóa rủi ro cấu trúc) — chứng minh đầy đủ
**Giả thiết.** Năm thành phần sau.

- **Mẫu.** $S\sim D^m$ theo (T1), $m\ge1$.
- **Hàm lỗi.** $\ell$ thỏa (T2) và (T3).
- **Họ lớp.** Các lớp, bán kính và trọng số thỏa (T6); $\mathrm{pen}_k$ như ở Bổ đề 04.9.
- **Thuật toán.** Một thuật toán SRM với dung sai $\tau\ge0$, thỏa điều kiện đo được của Định nghĩa 01.4.
- **Tham số.** $\delta\in(0,1)$.

**Bảo đảm.** Với xác suất ít nhất $1-\delta$ theo $S\sim D^m$, đồng thời cho mọi nghiệm $\tau$-chính xác $(\hat k,\hat h)$:

- **(a) Cận trên tin cậy.** $L_D(\hat h)\le L_S(\hat h)+\mathrm{pen}_{\hat k}$.
- **(b) Bất đẳng thức oracle.**
  $$
  \begin{aligned}
  &L_D(\hat h)\\
  &\le\inf_k\Big[\inf_{h\in\mathcal H_k}L_D(h)\\
  &\qquad+2\,\mathrm{pen}_k\Big]+\tau .
  \end{aligned}
  $$

Phần (b) chặn rủi ro so với một *mốc có phạt* (penalized benchmark), tức cận dưới đúng ở vế phải, không phải rủi ro vượt mức so với hợp các lớp. Dung sai $\tau$ cộng với hệ số $1$; cận phụ thuộc $m$, $\delta$, $q_k$ và độ phức tạp của lớp qua $\mathrm{pen}_k$; bảo đảm áp dụng cho mọi cặp $\tau$-chính xác, kể cả cặp không do một thuật toán cố định trả về.
:::

Tên *bất đẳng thức oracle* (oracle inequality) chỉ mốc so sánh: vế phải của (b) là giá trị mà một người biết $D$ (một "oracle") có thể dùng để so các lớp, tức mức tốt nhất $\inf_{h\in\mathcal H_k}L_D(h)$ của lớp $k$ cộng giá thống kê $2\,\mathrm{pen}_k$. Với xác suất ít nhất $1-\delta$, rủi ro của SRM không vượt giá trị đó cộng $\tau$.

::: proof Chứng minh Định lý 04.11
**Lộ trình.** Ba bất đẳng thức trên biến cố của Bổ đề 04.9, như Bước 2 của chứng minh Hệ quả 02.16.

**Bước 1 (biến cố).** Gọi $E$ là biến cố của Bổ đề 04.9; $\Pr(E)\ge1-\delta$, và $E$ không phụ thuộc thuật toán. Các giả thiết (T1)–(T3), (T6) chỉ đi vào qua bổ đề này; tính đo được của thuật toán làm $L_D(\hat h)$ là biến ngẫu nhiên.

**Bước 2 (chuỗi bất đẳng thức).** Trên $E$, với mọi $k$ và mọi $h\in\mathcal H_k$,
$$
\begin{aligned}
L_D(\hat h)&\le L_S(\hat h)+\mathrm{pen}_{\hat k}\\
&\le L_S(h)+\mathrm{pen}_k+\tau\\
&\le L_D(h)+2\,\mathrm{pen}_k+\tau .
\end{aligned}
$$
Bất đẳng thức thứ nhất dùng $E$ tại cặp $(\hat k,\hat h)$; đây là chỗ cần tính đồng thời theo $k$, vì $\hat k$ được chọn theo $S$, và nó là phần (a). Bất đẳng thức thứ hai dùng tính $\tau$-chính xác, vì cận dưới đúng của mục tiêu không vượt quá giá trị tại $(k,h)$. Bất đẳng thức thứ ba dùng $E$ tại $(k,h)$.

**Bước 3 (cận dưới đúng).** Vế trái không phụ thuộc $(k,h)$. Lấy cận dưới đúng theo $h\in\mathcal H_k$ rồi theo $k$, ta được (b).

$\square$ SRM cạnh tranh đồng thời với mọi lớp, và với lớp $k$ nó trả giá $2\,\mathrm{pen}_k$. Với một lớp, $q_1=1$ và $\tau=0$, phần (b) có dạng của Hệ quả 03.16(a).
:::

Một cách tính nghiệm SRM là giải ERM trên từng lớp rồi so các tổng.

::: algorithm Thuật toán 04.12 (SRM qua ERM trên từng lớp)
**Đầu vào.** Bốn thành phần sau.

- **Mẫu.** $S$ cỡ $m$.
- **Họ lớp.** Các lớp, bán kính và trọng số thỏa (T6), với $\mathrm{pen}_k$ không giảm theo $k$; danh sách hữu hạn, hoặc $\mathrm{pen}_k\to\infty$.
- **Tham số.** $\delta\in(0,1)$.
- **Bộ giải.** Với mỗi $k$, một $\epsilon_{\mathrm{opt}}$-ERM trên $\mathcal H_k$, cùng $\epsilon_{\mathrm{opt}}$.

**Khởi tạo.** $v\leftarrow+\infty$ (giá trị tốt nhất đã có), $\hat k\leftarrow1$, $k\leftarrow1$.

**Vòng lặp theo $k$.**

1. Tính $\mathrm{pen}_k=\mathrm{rad}_k(m,\delta q_k)$.
2. Nếu $\mathrm{pen}_k\ge v$, dừng.
3. Gọi bộ giải trên $\mathcal H_k$, được $\hat h_k$.
4. Nếu $L_S(\hat h_k)+\mathrm{pen}_k<v$, đặt $v\leftarrow L_S(\hat h_k)+\mathrm{pen}_k$ và $\hat k\leftarrow k$. Nếu còn lớp, tăng $k$ lên $1$ và trở lại bước 1; nếu hết danh sách, dừng.

**Điều kiện dừng.** Hết danh sách, hoặc $\mathrm{pen}_k\ge v$; điều kiện thứ hai hợp lệ vì $L_S\ge0$ và $\mathrm{pen}$ không giảm, nên mọi lớp chưa duyệt có mục tiêu không nhỏ hơn $v$.

**Đầu ra.** Cặp $(\hat k,\hat h_{\hat k})$.

**Chi phí.** Một lần gọi bộ giải ERM cho mỗi lớp được duyệt; với điều kiện ở đầu vào, số lớp được duyệt hữu hạn.
:::

Đầu ra của Thuật toán 04.12 là một nghiệm $\tau$-chính xác với $\tau=\epsilon_{\mathrm{opt}}+\tau'$, trong đó $\tau'\ge0$ là sai số của các phép so sánh ở bước 2 và 4. Khi mọi lớp được duyệt, trên cùng biến cố với Định lý 04.11 còn có cận tinh hơn (cả hai khẳng định được chứng minh ở Phụ lục E):
$$
\begin{aligned}
L_D(\hat h_{\hat k})\le\inf_k\Big[&\inf_{h\in\mathcal H_k}L_D(h)+2\,\mathrm{pen}_k\\
&+\operatorname{opt}_S(\hat h_k)\Big]+\tau'.
\end{aligned}
$$
Sai số tối ưu thực nghiệm xuất hiện ở lớp so sánh, không phải ở lớp được chọn.

::: example Ví dụ 04.9 (Chọn số chỉ số đo bằng tối thiểu hóa rủi ro cấu trúc)
**Thiết lập.** Ứng dụng ở §3 với $m=10^4$, $\delta=0{,}05$, $q_k=6/(\pi^2k^2)$ và dạng chiều VC của bán kính, với $d=d_k=k+1$ và $\delta'=\delta q_k$. Thuật toán là Thuật toán 04.12 với nghiệm ERM chính xác $\hat h_k$ trên mỗi $\mathcal H_k$ (Nhận xét 01.11). Các giá trị $L_S(\hat h_k)$ dưới đây là giả định để minh họa, không phải số liệu đo được; chúng không tăng theo $k$ vì các lớp lồng nhau.

**Bước 1: bảng.** Các số hạng phạt tính như ở Ví dụ 04.7 (Phụ lục C); các tổng làm tròn đến bốn chữ số.

| $k$ | $L_S(\hat h_k)$ giả định $+\ \mathrm{pen}_k$ | tổng |
|---|---|---|
| $1$ | $0{,}300+0{,}1423$ | $0{,}4423$ |
| $2$ | $0{,}210+0{,}1690$ | $0{,}3790$ |
| $3$ | $0{,}175+0{,}1900$ | $\mathbf{0{,}3650}$ |
| $4$ | $0{,}170+0{,}2081$ | $0{,}3781$ |
| $5$ | $0{,}166+0{,}2241$ | $0{,}3901$ |
| $6$ | $0{,}163+0{,}2386$ | $0{,}4016$ |
| $7$ | $0{,}160+0{,}2520$ | $0{,}4120$ |
| $8$ | $0{,}158+0{,}2644$ | $0{,}4224$ |
| $9$ | $0{,}156+0{,}2761$ | $0{,}4321$ |
| $10$ | $0{,}155+0{,}2871$ | $0{,}4421$ |

**Bước 2: lựa chọn và cận.** SRM chọn $\hat k=3$. Theo Định lý 04.11(a), $0{,}3651$ là một cận trên tin cậy ở mức $95\%$ cho $L_D(\hat h_3)$ (giá trị chưa làm tròn $0{,}36504$): thủ tục tính cận này đúng với xác suất ít nhất $0{,}95$ theo $S$ (Nhận xét 01.19).

**Bước 3: so với tối thiểu hóa rủi ro thực nghiệm.** Tối thiểu hóa rủi ro thực nghiệm trên cả họ luôn chọn một hàm của lớp lớn nhất $\mathcal H_{10}$. Lớp này cố định trước mẫu, nên Định lý 03.15 áp dụng cho riêng $\mathcal H_{10}$ với $\delta$ không chia: cận là $0{,}155+0{,}27992=0{,}43492$, làm tròn lên $0{,}4350$.

**Bước 4: nếu biết trước lớp.** Nếu $k=3$ được cố định trước mẫu, cận là $0{,}175+0{,}18428=0{,}35928$, làm tròn lên $0{,}3593$. Hiệu $0{,}36504-0{,}35928\approx0{,}0058$ là giá của việc không biết trước lớp.

**Bước 5: độ nhạy.** Tổng tại $k=4$ lớn hơn tổng tại $k=3$ khoảng $0{,}0130$, nên lựa chọn nhạy với các giá trị giả định.

**Kết luận.** Với $10^4$ quan sát, SRM dùng ba chỉ số đo và cho cận trên tin cậy $0{,}3651$, so với $0{,}4350$ khi dùng cả mười. Trong bất đẳng thức oracle, số hạng $2\,\mathrm{pen}_k$ bằng $0{,}338$ tại $k=2$ và $0{,}574$ tại $k=10$, so với $0{,}329$ và $0{,}560$ khi mỗi lớp được xét riêng (§11 của Bài 03).
:::

Ví dụ sau bỏ (T6): lớp thứ hai được dựng sau khi xem mẫu.

::: example Ví dụ 04.10 (Họ lớp chọn sau khi xem mẫu)
**Thiết lập.** $X\sim U[0,1]$, $Y\sim\mathrm{Bernoulli}(0{,}8)$ độc lập với $X$; hàm lỗi 0–1, $m=1000$, $\delta=0{,}05$. Lớp thứ nhất là $\mathcal H_1=\{h\equiv1\}$, với $L_D(h\equiv1)=0{,}2$. Sau khi xem $S$, gọi $F_+$ là tập các đầu vào có nhãn $1$ trong mẫu, và đặt lớp thứ hai là $\mathcal G_S=\{\mathbb 1_{F_+}\}$, dùng lại tên $\mathcal G_S$ của Ví dụ 03.8 cho một lớp dựng từ mẫu.

**Bước 1: hai rủi ro.** Các đầu vào trong mẫu đôi một khác nhau với xác suất $1$, nên $L_S(\mathbb 1_{F_+})=0$. Một đầu vào mới nằm ngoài tập hữu hạn $F_+$ với xác suất $1$ và được dự đoán $0$, nên $L_D(\mathbb 1_{F_+})=0{,}8$.

**Bước 2: bán kính nếu coi hai lớp là cố định.** Với $q=\tfrac12$ cho mỗi lớp và bán kính của lớp một phần tử (Hệ quả 02.10(b)),
$$
\begin{aligned}
\sqrt{\tfrac{\ln(2/(\delta/2))}{2m}}&=\sqrt{\tfrac{\ln80}{2000}}\\
&\approx0{,}04681 .
\end{aligned}
$$

**Bước 3: lựa chọn.** Hai lớp có cùng số hạng phạt, nên SRM chọn $\mathbb 1_{F_+}$ khi mẫu có ít nhất một nhãn $0$ (xác suất $1-0{,}8^{1000}$), và cận trên tin cậy báo $L_D\le0{,}0469$.

**Bước 4: chỗ hỏng.** Lớp $\mathcal G_S$ phụ thuộc $S$, nên bước $\Pr(B_2)\le\delta/2$ trong chứng minh Bổ đề 04.9 không còn đúng. Ở đây độ lệch của $\mathbb 1_{F_+}$ luôn bằng $0{,}8$, nên $B_2$ xảy ra chắc chắn.

**Kết luận.** Rủi ro kì vọng là $0{,}8$, còn cận báo $0{,}0469$, vì (T6) không thỏa.
:::

::: remark Nhận xét 04.13 (Số hạng phạt theo độ dài mô tả) — đọc thêm
Coi mỗi giả thuyết là một lớp một phần tử, mô tả bằng một chuỗi bit dài $\lvert h\rvert$, gọi là *độ dài mô tả* (description length), trong một ngôn ngữ *không tiền tố* (prefix-free) cố định trước mẫu: không mô tả nào là đoạn đầu của mô tả khác. Bất đẳng thức Kraft (Kraft inequality) $\sum_h2^{-\lvert h\rvert}\le1$ cho trọng số $q_h=2^{-\lvert h\rvert}$ và số hạng phạt $\sqrt{(\lvert h\rvert\ln2+\ln(2/\delta))/(2m)}$ (UML §7.3; Bài tập 04.10).
:::

SRM thay câu hỏi chọn lớp bằng một bài toán tối ưu có phạt, và Định lý 04.11 so đầu ra của nó với mốc có phạt; số hạng phạt trong cận này còn phụ thuộc $\delta$, một đầu vào của quy tắc.

## 7. Học không đều

Theo Định lý 04.11, với $h\in\mathcal H_k$ ta có $L_D(\hat h)\le L_D(h)+2\,\mathrm{pen}_k+\tau$. Với bán kính của Định lý 02.14(a) hoặc 03.15(a) và một danh sách vô hạn, $\mathrm{pen}_k\to\infty$ (Phụ lục A), nên cỡ mẫu để cận của hiệu này nhỏ hơn $\epsilon$ phụ thuộc lớp chứa $h$; cận không cho một cỡ mẫu chung cho mọi $h$ như Định nghĩa 01.25 đòi.

::: definition Định nghĩa 04.14 (Học không đều)
Cho tập quan sát $\mathcal Z$, lớp $\mathcal H$ và hàm lỗi $\ell$ thỏa (T2), (T3). Một thuật toán học $A$ được gọi là *thuật toán học không đều* (nonuniform learner) cho $\mathcal H$ nếu tồn tại hàm $M:(0,1)^2\times\mathcal H\to\mathbb N$ sao cho bất đẳng thức dưới đây đúng với mọi lựa chọn của bốn thành phần sau.

- **Tham số.** $\epsilon,\delta\in(0,1)$.
- **Giả thuyết so sánh.** $h\in\mathcal H$, gọi là *giả thuyết so sánh* (comparator hypothesis).
- **Phân bố dữ liệu.** $D$ trên $\mathcal Z$.
- **Cỡ mẫu.** $m\ge M(\epsilon,\delta,h)$.

Bất đẳng thức đó là
$$
\begin{aligned}
&\Pr_{S\sim D^m}\big[L_D(A(S))\\
&\quad\le L_D(h)+\epsilon\big]\ge1-\delta .
\end{aligned}
$$
Lớp $\mathcal H$ được gọi là *học được không đều* (nonuniformly learnable) nếu tồn tại một thuật toán học không đều cho $\mathcal H$.
:::

Thứ tự lượng từ giống Định nghĩa 01.25: $A$ cố định trước $\epsilon$, $\delta$, và $M$ có trước $D$. Có hai khác biệt: $M$ có thể phụ thuộc giả thuyết so sánh $h$, nhưng không phụ thuộc $D$; và đối tượng so sánh là $L_D(h)$ thay cho $\inf_{h'}L_D(h')$, với xác suất lấy cho từng $h$.

Với hàm lỗi bị chặn, mọi thuật toán học PAC bất khả tri là thuật toán học không đều với $M(\epsilon,\delta,h)=M(\epsilon,\delta)$, vì $L_D(A(S))\le\inf_{h'}L_D(h')+\epsilon\le L_D(h)+\epsilon$. Một quy tắc có cỡ mẫu phụ thuộc $D$, chẳng hạn qua sai số xấp xỉ, không thỏa định nghĩa.

Số hạng phạt của SRM ở §6, nên cả quy tắc, phụ thuộc $\delta$: SRM là một họ thuật toán chỉ số theo $\delta$, còn Định nghĩa 04.14 đòi một thuật toán cố định trước $\epsilon$, $\delta$. Chúng ta cho $\delta$ giảm theo cỡ mẫu.

::: corollary Hệ quả 04.15 (Tối thiểu hóa rủi ro cấu trúc với xác suất thất bại $1/m$) — chứng minh đầy đủ ở Phụ lục B
**Giả thiết.** Năm thành phần sau.

- **Bài toán.** Phân lớp nhị phân, hàm lỗi 0–1, $S\sim D^m$ theo (T1).
- **Họ lớp.** Một danh sách đếm được $\mathcal H_1,\mathcal H_2,\ldots$ cố định trước mẫu; mỗi $\mathcal H_k$ hữu hạn, hoặc thỏa (M) và có chiều VC $d_k<\infty$.
- **Trọng số.** $q_k>0$, $\sum_kq_k\le1$, chọn trước mẫu.
- **Số hạng phạt.** $\mathrm{pen}_k(m)=\mathrm{rad}_k(m,q_k/m)$, với $\mathrm{rad}_k$ là bán kính của Định lý 02.14(a) khi $\mathcal H_k$ hữu hạn và của Định lý 03.15(a) trong trường hợp còn lại.
- **Thuật toán.** $A_{\mathrm{SRM}}$: với $m\ge2$, trả về một nghiệm SRM chính xác với các số hạng phạt này (tồn tại theo Phụ lục A), chọn sao cho $A_{\mathrm{SRM}}$ thỏa điều kiện đo được của Định nghĩa 01.4; với $m=1$, trả về một phần tử cố định của $\mathcal H_1$.

Đặt $M_k(\epsilon)$ là số $m_0\ge2$ nhỏ nhất sao cho $2\,\mathrm{pen}_k(m)\le\epsilon$ với mọi $m\ge m_0$, và với $h\in\mathcal H=\bigcup_k\mathcal H_k$, gọi $k(h)$ là chỉ số nhỏ nhất có $h\in\mathcal H_k$.

**Bảo đảm.** Hai khẳng định.

- **(a) Danh sách đếm được.** $M_k(\epsilon)<\infty$ với mọi $k$ và $\epsilon$, và $A_{\mathrm{SRM}}$ là thuật toán học không đều cho $\mathcal H$ với
  $$
  \begin{aligned}
  &M(\epsilon,\delta,h)=\max\big\{\lceil1/\delta\rceil,\\
  &\qquad M_{k(h)}(\epsilon)\big\}.
  \end{aligned}
  $$
- **(b) Danh sách hữu hạn.** Nếu danh sách có $k_{\max}$ lớp, $A_{\mathrm{SRM}}$ là thuật toán học PAC bất khả tri cho $\mathcal H$ với
  $$
  \begin{aligned}
  &M(\epsilon,\delta)=\max\big\{\lceil1/\delta\rceil,\\
  &\qquad\max_{k\le k_{\max}}M_k(\epsilon)\big\}.
  \end{aligned}
  $$

Thuật toán không nhận $\epsilon$, $\delta$; cỡ mẫu phụ thuộc $h$ qua chỉ số lớp, không phụ thuộc $D$.
:::

Chứng minh dùng Định lý 04.11 với $\delta=1/m$ và $\tau=0$, rồi cho $m\to\infty$ trong số hạng phạt; chi tiết ở Phụ lục B.

Với $k=3$ ($d_3=4$), $\epsilon=0{,}1$ và dạng chiều VC của bán kính, cỡ mẫu đủ theo cận để $2\,\mathrm{pen}\le0{,}1$ như sau (Phụ lục B).

- **ERM chỉ trên $\mathcal H_3$, $\delta=0{,}05$.** $172\,279$ quan sát.
- **SRM với $\delta=0{,}05$ chia theo $q_3$.** $181\,575$ quan sát.
- **$A_{\mathrm{SRM}}$.** $213\,317$ quan sát; điều kiện $m\ge\lceil1/\delta\rceil=20$ không ràng buộc.

Không biết trước lớp làm cỡ mẫu đủ tăng khoảng $5{,}4\%$; bỏ $\delta$ khỏi đầu vào làm nó tăng thêm khoảng $17{,}5\%$, nhưng ở cỡ mẫu đó $A_{\mathrm{SRM}}$ có xác suất thất bại không quá $1/m\approx4{,}7\cdot10^{-6}$, nhỏ hơn nhiều so với $0{,}05$.

::: example Ví dụ 04.11 (Một lớp đếm được có chiều VC vô hạn)
**Thiết lập.** $\mathcal X=[0,1]$ với σ-đại số Borel, hàm lỗi 0–1. Lớp $\mathcal H$ gồm các hàm $\mathbb 1_F$, với $F$ là một tập con hữu hạn của tập các số hữu tỉ trong $[0,1]$.

**Bước 1: lớp đếm được.** Tập các tập con hữu hạn của một tập đếm được là đếm được, nên ta liệt kê $\mathcal H=\{h_1,h_2,\ldots\}$. Đặt $\mathcal H_j=\{h_j\}$, lớp một phần tử, với trọng số $q_j=6/(\pi^2j^2)$.

**Bước 2: chiều VC vô hạn.** Mọi tập hữu hạn các số hữu tỉ trong $[0,1]$ bị tách trọn (lấy $F$ là tập các điểm nhãn $1$), nên $d=\infty$. Theo Định lý 03.17(a), $\mathcal H$ không học được PAC, và theo Nhận xét 01.26 cũng không học được PAC bất khả tri.

**Bước 3: học được không đều.** Mỗi $\mathcal H_j$ hữu hạn, nên Hệ quả 04.15(a) áp dụng được; chọn chỉ số $j$ nhỏ nhất trong các nghiệm cho một $A_{\mathrm{SRM}}$ đo được.

**Kết luận.** Phép kéo theo ngược lại của đoạn sau Định nghĩa 04.14 sai: lớp này học được không đều nhưng không học được PAC. Cỡ mẫu tăng theo $\ln(1/q_j)=2\ln j+\ln(\pi^2/6)$, tức theo vị trí của giả thuyết so sánh trong danh sách.
:::

Định lý sau thêm điều kiện cần, theo UML §7.1.

::: theorem Định lý 04.16 (Đặc trưng của học không đều cho phân lớp nhị phân) — đọc thêm
**Giả thiết.** Năm thành phần sau.

- **Bài toán.** $\mathcal X$ có σ-đại số, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1.
- **Mẫu.** $S\sim D^m$ theo (T1).
- **Lớp.** $\mathcal H$ khác rỗng.
- **Họ lớp, cho phần (b).** Một danh sách đếm được $\mathcal H_1,\mathcal H_2,\ldots$ với $\mathcal H=\bigcup_k\mathcal H_k$, mỗi lớp có chiều VC hữu hạn và thỏa (M), cùng các trọng số $q_k>0$, $\sum_kq_k\le1$.
- **Thuật toán.** Thuật toán học theo Định nghĩa 01.4; ở phần (b), có một cách chọn nghiệm SRM chính xác cho họ lớp trên làm $A_{\mathrm{SRM}}$ của Hệ quả 04.15 thỏa Định nghĩa 01.4.

**Bảo đảm.** Hai khẳng định định tính về lớp.

- **(a) Điều kiện cần.** Nếu $\mathcal H$ học được không đều thì $\mathcal H=\bigcup_{k\in\mathbb N}\mathcal H_k$, với mọi $\mathcal H_k$ có chiều VC hữu hạn.
- **(b) Điều kiện đủ.** Dưới các giả thiết cho phần (b), $\mathcal H$ học được không đều (Hệ quả 04.15).
:::

Phần (a) được phác thảo ở Phụ lục D.

Theo Ví dụ 04.11, một lớp đếm được có chiều VC vô hạn vẫn học được không đều. Lớp mọi hàm trên một miền vô hạn được xét ở ý thử thách của Bài tập 04.11.

## 8. Chọn mô hình bằng mẫu xác thực

SRM dùng cùng một mẫu để huấn luyện và để chọn lớp, và trả giá bằng số hạng phạt. Khi có thêm một mẫu chỉ dùng để chọn, phép chọn mô hình (model selection) là ERM trên một lớp hữu hạn các ứng viên (§3 của Bài 02), dưới giả thiết sau.

- **(T7) Mẫu xác thực độc lập.** Mẫu xác thực $V=(V_1,\ldots,V_{m_v})\sim D^{m_v}$ độc lập với mẫu huấn luyện $S$ và với mọi nguồn đã sinh ra các ứng viên. Số ứng viên $K$ và các ứng viên $g_1,\ldots,g_K$ là hàm của $S$, không phụ thuộc $V$.

Ta kí hiệu $L_V(g)=\frac1{m_v}\sum_{i=1}^{m_v}\ell(g,V_i)$ và gọi $m_v$ là *cỡ mẫu xác thực* (validation sample size); khác Ví dụ 02.8, $S$ ở đây là mẫu huấn luyện.

::: corollary Hệ quả 04.17 (Chọn mô hình bằng mẫu xác thực) — phác thảo
**Giả thiết.** Sáu thành phần sau.

- **Dữ liệu huấn luyện.** $S$ có phân bố bất kì.
- **Ứng viên.** $g_1,\ldots,g_K$ là hàm của $S$; $K\ge1$ có thể phụ thuộc $S$; $K(S)$ và $(s,z)\mapsto\ell(g_j(s),z)$ đo được.
- **Mẫu xác thực.** $V$ thỏa (T7).
- **Hàm lỗi.** $\ell$ thỏa (T2) và (T3).
- **Quy tắc chọn.** $\hat g$ là một ứng viên bất kì làm $L_V$ nhỏ nhất trong $K$ ứng viên.
- **Tham số.** $\delta\in(0,1)$.

**Bảo đảm.** Xác suất lấy theo $(S,V)$; mỗi khẳng định đúng với xác suất ít nhất $1-\delta$.

- **(a) Cận so với ứng viên tốt nhất.**
  $$
  \begin{aligned}
  &L_D(\hat g)\le\min_{j\le K}L_D(g_j)\\
  &\quad+2\sqrt{\tfrac{\ln(2K/\delta)}{2m_v}}.
  \end{aligned}
  $$
- **(b) Cận trên tin cậy.** $L_D(\hat g)\le L_V(\hat g)+\sqrt{\ln(K/\delta)/(2m_v)}$.

Đối tượng so sánh là ứng viên tốt nhất, ngẫu nhiên qua $S$; cận phụ thuộc $m_v$, $\ln K$, $\delta$, không phụ thuộc độ phức tạp của các lớp sinh ra ứng viên hay $m$.
:::

::: proof Chứng minh Hệ quả 04.17 (phác thảo)
**Lộ trình.** Lấy điều kiện theo $S$, như Bước 1 của Ví dụ 02.8, rồi áp dụng các kết quả của Bài 02 cho mẫu $V$.

**Bước 1 (lấy điều kiện).** Khi biết $S$, $K$ ứng viên là một lớp hữu hạn cố định. Theo (T7), mẫu $V$ vẫn có phân bố $D^{m_v}$ khi biết $S$ (Nhận xét 01.9), nên (T1) và (T4) thỏa với mẫu $V$ và lớp $\{g_1,\ldots,g_K\}$.

**Bước 2 (hai phần).** Hệ quả 02.16(a), với giá trị nhỏ nhất $\min_jL_D(g_j)$ đạt vì lớp hữu hạn, cho (a) với xác suất có điều kiện ít nhất $1-\delta$. Định lý 02.14(b) cho (b). Hai phần dùng hai biến cố khác nhau; nếu cần cả hai đồng thời, dùng $\delta/2$ cho mỗi phần.

**Bước 3 (bỏ điều kiện).** Lấy kì vọng theo $S$ của xác suất có điều kiện (định lý Fubini, dùng tính đo được trong giả thiết). Bước lấy điều kiện chỉ được phác thảo theo Ví dụ 02.8, nên chứng minh là phác thảo.

Hệ số $2$ trong $\ln(2K/\delta)$ đến từ hai phía của bất đẳng thức Hoeffding; hệ số $2$ ngoài căn đến từ hai phép so sánh.

$\square$ Chọn trong $K$ ứng viên tốn một lượng tỉ lệ với $\sqrt{\ln K/m_v}$.
:::

::: example Ví dụ 04.12 (Chọn trong mười ứng viên bằng mẫu xác thực)
**Thiết lập.** Ứng dụng ở §3: ứng viên $g_k=\hat h_k$ là nghiệm ERM trên $\mathcal H_k$ tính từ $S$ ($m=10^4$), $K=10$; một mẫu xác thực mới $V$ với $m_v=1000$; hàm lỗi 0–1; $\delta=0{,}05$.

**Bước 1: số hạng lôgarit.** $\ln(2K/\delta)=\ln400\approx5{,}9915$.

**Bước 2: cận (a).** $\sqrt{5{,}9915/2000}\approx0{,}0547$, nên ứng viên được chọn có rủi ro vượt ứng viên tốt nhất không quá $2\cdot0{,}0547\approx0{,}1095$.

**Bước 3: theo cỡ mẫu xác thực.** Cùng công thức với $m_v=200$, $500$, $2000$, $5000$ cho $0{,}2448$; $0{,}1548$; $0{,}0774$; $0{,}0490$.

**Bước 4: cỡ mẫu xác thực đủ.** Cận (a) không quá $\epsilon$ khi $m_v\ge2\ln400/\epsilon^2$. Với $\epsilon=0{,}1$, $2\cdot5{,}9915/0{,}01\approx1198{,}3$, nên $1199$ quan sát là đủ; với $\epsilon=0{,}05$, $2\cdot5{,}9915/0{,}0025\approx4793{,}2$, nên $4794$ là đủ.

**Kết luận.** Với $m_v=1000$, nhân số ứng viên lên $10^5$ lần ($K=10^6$) chỉ làm cận tăng từ $0{,}1095$ lên $0{,}1871$. Đổi lại, cận chỉ so với ứng viên tốt nhất, nên không so trực tiếp được với cận của Ví dụ 04.9.
:::

::: remark Nhận xét 04.18 (Phạm vi của bảo đảm xác thực)
Hệ quả 04.17 có ba giới hạn sau.

- **Dùng lại thích nghi.** Nếu ứng viên hoặc $K$ được thiết kế sau khi xem $L_V$ (dùng lại thích nghi, adaptive reuse; §9 của Bài 02), (T7) không còn thỏa; danh sách thực tế gồm mọi ứng viên có thể được tạo ra (Bài tập 04.5).
- **Kiểm tra chéo.** Trong kiểm tra chéo (cross-validation), mỗi phần dữ liệu vừa huấn luyện vừa xác thực, nên các số hạng phụ thuộc nhau và Hệ quả 04.17 không áp dụng (Bài tập 04.12).
- **Hàm lỗi bình phương.** Với hồi quy, cần $\lvert Y\rvert\le B$ và cắt dự đoán vào $[-B,B]$; hàm lỗi khi đó nằm trong $[0,4B^2]$ và cận nhân thêm $4B^2$ (Bài tập 02.11). Chọn trong $K=15$ bậc đa thức với $m_v=1000$, $B=1$ và $\delta=0{,}05$ cho cận $4\cdot2\sqrt{\ln600/2000}\approx0{,}4524$.
:::

Cả SRM lẫn xác thực cần mọi lựa chọn (họ lớp, trọng số, danh sách ứng viên) cố định trước khi dùng mẫu đánh giá.

## 9. Ý nghĩa, tác động và giới hạn

Số hạng phạt của SRM là bán kính hội tụ đều của Bài 02–03 tại xác suất thất bại $\delta q_k$. Với câu hỏi cầu nối của Bài 03, SRM chọn ba chỉ số đo (cận $0{,}3651$, so với $0{,}4350$ cho mười chỉ số đo; Ví dụ 04.9). Với câu hỏi mở đầu, bài không có cận đều cho lớp đa thức với hàm lỗi bình phương; bậc tốt nhất phụ thuộc mức nhiễu và $f^*$ (Ví dụ 04.4). Khi $\lvert Y\rvert\le B$ và dự đoán được cắt vào $[-B,B]$, chọn bậc bằng mẫu xác thực có cận của Nhận xét 04.18.

Chia xác suất thất bại làm bán kính tăng không quá khoảng $3{,}2\%$ (Ví dụ 04.7); bỏ $\delta$ khỏi đầu vào làm cỡ mẫu đủ tăng thêm khoảng $17{,}5\%$ (Hệ quả 04.15). Xác thực trả $2\sqrt{\ln(2K/\delta)/(2m_v)}$ cộng phần dữ liệu không dùng để huấn luyện (Bài tập 04.13), còn SRM trả số hạng phạt trên toàn bộ mẫu.

Mệnh đề 04.3 là cận với xác suất cao cho hàm lỗi bị chặn; Mệnh đề 04.6 là đẳng thức kì vọng cho một thuật toán với hàm lỗi bình phương. Độ chệch không phải sai số xấp xỉ (Nhận xét 04.7), và với hàm phân lớp, khi dự đoán đa số sai, phương sai theo nghĩa phân lớp lớn hơn có thể cho lỗi nhỏ hơn (Ví dụ 04.6).

Bỏ một trong bốn giả thiết sau, bảo đảm có thể hỏng.

- **Họ lớp cố định.** Cận báo $0{,}0469$ trong khi rủi ro kì vọng là $0{,}8$ (Ví dụ 04.10).
- **Tổng trọng số không quá $1$.** Xác suất thất bại $0{,}86$ thay vì không quá $0{,}05$ (Ví dụ 04.8).
- **Nhãn kiểm tra độc lập.** Lỗi $0{,}75$ thay vì $1{,}25$ (Ví dụ 04.5).
- **Mẫu xác thực dùng một lần.** Dùng lại thích nghi làm hỏng (T7) (Nhận xét 04.18).

Chính quy hóa (regularization) cộng vào rủi ro thực nghiệm một số hạng $\lambda\,\Omega(w)$, thường là $\lambda\lVert w\rVert^2$, với $\lambda$ chọn theo dữ liệu; khi $\lambda$ được chọn trên chính mẫu huấn luyện, Định lý 04.11 không áp dụng. Các cận của bài cần hàm lỗi trong $[0,1]$ và không chuyển sang hàm lỗi bình phương hay hàm lỗi log mà không có giả thiết bị chặn (Nhận xét 02.11).

## 10. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 04](material-viewer.html?doc=materials/lec-04/exercises.md). Sáu bài đầu là bài gốc, bảy bài sau chọn từ UML; mỗi dòng ghi mục tiêu mà bài kiểm tra.

1. **Bài tập 04.1** (Cận ba thành phần cho ERM xấp xỉ): mục tiêu 1.
2. **Bài tập 04.2** (Phân tích độ chệch–phương sai lấy trung bình theo đầu vào): mục tiêu 2.
3. **Bài tập 04.3** (Trọng số $q_k=6/(\pi^2k^2)$ và số hạng tin cậy của từng lớp): mục tiêu 3.
4. **Bài tập 04.4** (Chọn lớp bằng SRM từ một bảng): mục tiêu 3.
5. **Bài tập 04.5** (Dùng lại thích nghi một mẫu xác thực): mục tiêu 5.
6. **Bài tập 04.6** (Chọn bậc đa thức bằng ba quy tắc, thực nghiệm tùy chọn): mục tiêu 2, 5.
7. **Bài tập 04.7** (Hai lớp hình chữ nhật trên hai và năm đặc trưng; UML Bài tập 5.2): mục tiêu 1, 3.
8. **Bài tập 04.8** (Không có trọng số không giảm có tổng hữu hạn; UML Bài tập 7.2): mục tiêu 3.
9. **Bài tập 04.9** (Trọng số từ chỉ số lớp và số phần tử; UML Bài tập 7.3): mục tiêu 3.
10. **Bài tập 04.10** (Bất đẳng thức oracle cho độ dài mô tả; UML Bài tập 7.4): mục tiêu 3.
11. **Bài tập 04.11** (Hợp các lớp nhiều khoảng: học được không đều nhưng không học được PAC; UML Bài tập 7.5): mục tiêu 4.
12. **Bài tập 04.12** (Kiểm tra chéo để lại một quan sát thất bại; UML Bài tập 11.1): mục tiêu 5.
13. **Bài tập 04.13** (ERM trên hợp các lớp so với chia huấn luyện–xác thực; UML Bài tập 11.2): mục tiêu 3, 5.

## 11. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Trong Ví dụ 04.9, thay nghiệm ERM chính xác trên $\mathcal H_3$ bằng đầu ra $\tilde h\in\mathcal H_3$ của một bộ giải gần đúng, với $L_S(\tilde h)=0{,}185$, trong khi $\inf_{h\in\mathcal H_3}L_S(h)=0{,}175$. Phần còn lại giữ nguyên.

(a) Tính $\operatorname{opt}_S(\tilde h)$ và dung sai $\tau$ của cặp $(3,\tilde h)$ đối với bài toán có phạt.

(b) Viết cận trên cho $L_D(\tilde h)$ mà Định lý 04.11 cho, ở dạng cận trên tin cậy và ở dạng oracle.

(c) Trong cận dạng oracle, số hạng nào giảm khi cỡ mẫu $m$ tăng, số hạng nào không đổi theo $m$, và số hạng nào chỉ giảm khi bài toán tối ưu được giải tốt hơn?

::: solution Lời giải câu hỏi cuối buổi
**(a)** Theo Định nghĩa 04.2, $\operatorname{opt}_S(\tilde h)=0{,}185-0{,}175=0{,}010$. Mục tiêu có phạt tại $(3,\tilde h)$ bằng
$$
0{,}185+0{,}1900=0{,}3750 .
$$
Giá trị nhỏ nhất của mục tiêu trên cả họ là $0{,}3650$, đạt trên $\mathcal H_3$ (Ví dụ 04.9), nên $\tau=0{,}3750-0{,}3650=0{,}010$. Hai số bằng nhau vì giá trị nhỏ nhất của mục tiêu đạt trên $\mathcal H_3$; nói chung chúng khác nhau.

**(b)** Theo Định lý 04.11(a), $0{,}3751$ (giá trị chưa làm tròn $0{,}37504$) là một cận trên tin cậy ở mức $95\%$ cho $L_D(\tilde h)$. Trên cùng biến cố, Định lý 04.11(b) cho
$$
\begin{aligned}
&L_D(\tilde h)\\
&\le\inf_k\Big[\inf_{h\in\mathcal H_k}L_D(h)\\
&\qquad+2\,\mathrm{pen}_k\Big]+0{,}010 .
\end{aligned}
$$

**(c)** Số hạng $2\,\mathrm{pen}_k$ giảm khi $m$ tăng, cỡ $\sqrt{\ln m/m}$. Số hạng $\inf_{h\in\mathcal H_k}L_D(h)$ không phụ thuộc $m$; trừ đi $L^*$, nó là sai số xấp xỉ. Dung sai $\tau$ do độ chính xác của bộ giải quyết định; cận không có cơ chế nào làm $\tau$ giảm khi thêm dữ liệu.
:::

Trong bài này, bộ giải chỉ được đo bằng $\operatorname{opt}_S$ hoặc $\tau$, và $\tau$ cộng thẳng vào bất đẳng thức oracle. ERM và SRM là các nguyên tắc thống kê, chưa cho cách tính nghiệm. Bài 05 xét các mục tiêu lồi, với hàm lỗi lồi theo tham số thay cho hàm lỗi 0–1, và thuật toán hạ gradient ngẫu nhiên (stochastic gradient descent, SGD) có chiếu. Câu hỏi cho Bài 05 là: sau $T$ vòng lặp, độ chênh tối ưu (suboptimality) của mục tiêu còn bao nhiêu, và mỗi vòng tốn bao nhiêu phép tính?

## 12. Tài liệu đọc

- **Trước buổi học:** UML §5.2 (phân tích sai số thành sai số xấp xỉ và sai số ước lượng), §7.1 (học không đều).
- **Sau buổi học:** UML §7.2 (tối thiểu hóa rủi ro cấu trúc), §11.1 (chọn mô hình bằng SRM), §11.2 (xác thực); các bài tập UML §5.5, §7.8, §11.5 đã chọn ở §10.
- **Mở rộng:** UML §7.3 (độ dài mô tả tối thiểu và dao cạo Occam; Nhận xét 04.13).

**Quan hệ với giáo trình UML.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục. Các khác biệt chính:

- **Phân tích sai số.** UML §5.2 gọi chính $\min_{h\in\mathcal H}L_D(h)$ (rủi ro tuyệt đối) là sai số xấp xỉ và chỉ xét nghiệm ERM; học phần dùng cận dưới đúng, $L^*$ và $\operatorname{opt}_S$. Phân tích ở §5 là phần bổ sung của học phần.
- **Kiểm soát từng lớp.** UML §7.2 định nghĩa bán kính qua hàm cỡ mẫu hội tụ đều, với trọng số $w$; học phần dùng các bán kính tường minh của Bài 02–03 và kí hiệu $q_k$.
- **SRM và học không đều.** UML so đầu ra với từng giả thuyết cố định và cho quy tắc SRM nhận $\delta$; học phần phát biểu bất đẳng thức oracle cho nghiệm có dung sai $\tau$, và Hệ quả 04.15 dùng xác suất thất bại $1/m$ để có một thuật toán không nhận $\delta$.
- **Xác thực.** UML §11.2 chặn độ lệch đều trên các ứng viên, với hàm lỗi trong $[0,1]$; Hệ quả 04.17 so với ứng viên tốt nhất, sau bước lấy điều kiện theo dữ liệu huấn luyện. Ví dụ hồi quy đa thức của UML §11.2 không nêu giả thiết bị chặn; học phần thêm $\lvert Y\rvert\le B$ và cắt dự đoán (Nhận xét 04.18).

## Phụ lục

### A. Sự tồn tại và tính đo được của nghiệm SRM

Các khẳng định về sự tồn tại sau Định nghĩa 04.10 và trong Hệ quả 04.15 được chứng minh dưới đây. Cố định một mẫu $S$ cỡ $m$ và đặt $v^\star=\inf_k\inf_{h\in\mathcal H_k}\big[L_S(h)+\mathrm{pen}_k\big]$.

::: proof Chứng minh các khẳng định về sự tồn tại
**Lộ trình.** Với $\tau>0$ chỉ cần $v^\star$ hữu hạn. Với $\tau=0$, ta đưa cận dưới đúng về một giá trị nhỏ nhất trên hữu hạn lớp, rồi dùng tính hữu hạn của tập giá trị của $L_S$ với hàm lỗi 0–1.

**Bước 1 ($\tau>0$).** Mục tiêu có phạt không âm, nên $0\le v^\star<\infty$. Theo định nghĩa của cận dưới đúng, có một cặp $(k,h)$ với $L_S(h)+\mathrm{pen}_k\le v^\star+\tau$.

**Bước 2 (hàm lỗi 0–1, giá trị tại lớp thứ nhất).** Với hàm lỗi 0–1, $L_S$ chỉ nhận giá trị trong $\{0,\tfrac1m,\ldots,1\}$, nên trên mỗi lớp khác rỗng, $\min_{h\in\mathcal H_k}L_S(h)$ đạt được (Nhận xét 01.11). Đặt $v_1=\min_{h\in\mathcal H_1}L_S(h)+\mathrm{pen}_1$.

**Bước 3 (chỉ hữu hạn lớp cần xét).** Giả sử danh sách hữu hạn, hoặc $\mathrm{pen}_k\to\infty$. Khi đó tập $J=\{k:\mathrm{pen}_k<v_1\}\cup\{1\}$ hữu hạn. Với $k\notin J$ và $h\in\mathcal H_k$, ta có $L_S(h)+\mathrm{pen}_k\ge\mathrm{pen}_k\ge v_1$, vì $L_S\ge0$. Do đó
$$
v^\star=\min_{k\in J}\Big[\min_{h\in\mathcal H_k}L_S(h)+\mathrm{pen}_k\Big],
$$
giá trị nhỏ nhất của hữu hạn số, và một cặp đạt giá trị đó là nghiệm SRM chính xác.

**Bước 4 ($\mathrm{pen}_k\to\infty$ cho hai bán kính).** Vì $\sum_kq_k\le1$, ta có $q_k\to0$, nên $\ln(1/(\delta q_k))\to\infty$. Với bán kính của Định lý 02.14(a), $\lvert\mathcal H_k\rvert\ge1$, nên
$$
\mathrm{pen}_k\ge\sqrt{\tfrac1{2m}\ln\tfrac2{\delta q_k}}\to\infty .
$$
Với bán kính $\rho_m$ của Định lý 03.15(a), $\Pi_{\mathcal H_k}(2m)\ge1$, nên $\mathrm{pen}_k\ge\sqrt{8\ln(4/(\delta q_k))/m}\to\infty$. Trong Hệ quả 04.15, $\delta=1/m$ cố định khi $m$ cố định, nên lập luận không đổi. Dạng chiều VC có cắt ở $1$ không thỏa điều kiện này khi $d_k\to\infty$; các ví dụ của bài chỉ dùng nó trên danh sách hữu hạn.

**Bước 5 (tính đo được).** Biến cố của Bổ đề 04.9 là giao đếm được của các biến cố đo được $B_k^c$, nên đo được. Quy tắc chọn giữa các cặp có cùng giá trị mục tiêu được giả sử đo được: đó là giả thiết **Thuật toán.** của Hệ quả 04.15 và Định lý 04.16(b), theo Định nghĩa 01.4 (Phụ lục A của Bài 01).

$\square$ Với hàm lỗi 0–1, SRM chính xác luôn xác định trên danh sách hữu hạn, và trên danh sách đếm được khi số hạng phạt tăng vô hạn theo chỉ số lớp.
:::

### B. Chứng minh và cỡ mẫu của Hệ quả 04.15

::: proof Chứng minh Hệ quả 04.15
**Lộ trình.** Áp dụng Định lý 04.11 với $\delta=1/m$ và $\tau=0$, rồi cho $m\to\infty$ trong số hạng phạt.

**Bước 1 (Định lý 04.11 tại $\delta=1/m$).** Với $m\ge2$, ta có $1/m\in(0,1)$, và $\mathrm{pen}_k(m)$ là số hạng phạt của Bổ đề 04.9 tại $\delta=1/m$. Định lý 04.11(b) cho một biến cố $E_m$, với $\Pr(E_m)\ge1-1/m$, trên đó
$$
\begin{aligned}
&L_D(A_{\mathrm{SRM}}(S))\\
&\quad\le L_D(h)+2\,\mathrm{pen}_k(m)
\end{aligned}
$$
với mọi $k$ và mọi $h\in\mathcal H_k$. Giả thiết (T1), hàm lỗi 0–1 và điều kiện trọng số đi vào qua Định lý 04.11; tính đo được của $A_{\mathrm{SRM}}$ làm các biến cố dưới đây có xác suất.

**Bước 2 ($\mathrm{pen}_k(m)\to0$).** Lớp hữu hạn có $\mathrm{pen}_k(m)=\sqrt{\ln(2\lvert\mathcal H_k\rvert m/q_k)/(2m)}$; lớp có $1\le d_k\le m$ có, theo Định lý 03.15(b),
$$
\begin{aligned}
\mathrm{pen}_k(m)^2&\le\tfrac8m\Big(d_k\ln\tfrac{2em}{d_k}\\
&\qquad+\ln\tfrac{4m}{q_k}\Big).
\end{aligned}
$$
Với $d_k=0$, hàm tăng trưởng bằng $1$ và $\mathrm{pen}_k(m)=\sqrt{8\ln(4m/q_k)/m}$. Cả ba vế phải có dạng $\sqrt{(a+b\ln m)/m}$ với $a$, $b$ không phụ thuộc $m$, nên tiến về $0$, và $M_k(\epsilon)$ hữu hạn.

**Bước 3 (phần a).** Cố định $\epsilon$, $\delta$, $h$, $D$, đặt $k=k(h)$ và lấy $m\ge\max\{\lceil1/\delta\rceil,M_k(\epsilon)\}$. Khi đó $m\ge2$, $1/m\le\delta$ và $2\,\mathrm{pen}_k(m)\le\epsilon$. Trên $E_m$, Bước 1 cho $L_D(A_{\mathrm{SRM}}(S))\le L_D(h)+\epsilon$, nên biến cố của Định nghĩa 04.14 có xác suất ít nhất $1-1/m\ge1-\delta$.

**Bước 4 (phần b).** Với $k_{\max}$ lớp và $m\ge\max\{\lceil1/\delta\rceil,\max_kM_k(\epsilon)\}$, trên $E_m$ bất đẳng thức $L_D(A_{\mathrm{SRM}}(S))\le L_D(h)+\epsilon$ đúng đồng thời cho mọi $h\in\mathcal H$. Lấy cận dưới đúng theo $h$, ta được biến cố của Định nghĩa 01.25; mọi $D$ có rủi ro hữu hạn vì hàm lỗi bị chặn.

$\square$ Chọn $\delta=1/m$ cho một thuật toán duy nhất, không nhận $\delta$, đạt mọi mức $\delta$ khi $m\ge\lceil1/\delta\rceil$, như Định nghĩa 04.14 đòi. Giá phải trả là $\ln m$ thay cho $\ln(1/\delta)$ trong số hạng phạt.
:::

**Cỡ mẫu trong phần đọc bằng số.** Với $d_3=4$ và dạng chiều VC của bán kính tại xác suất thất bại $\delta'$, điều kiện $2\,\mathrm{pen}\le0{,}1$ tương đương với
$$
\begin{aligned}
&\varphi(m)=\tfrac{32}m\Big(4\ln\tfrac{em}2+c(m)\Big)\\
&\qquad\le0{,}01,
\end{aligned}
$$
với $c(m)=\ln(4/\delta')$. Ba trường hợp là:

- **ERM chỉ trên $\mathcal H_3$.** $\delta'=0{,}05$, $c=\ln80\approx4{,}382$.
- **SRM tại $\delta=0{,}05$.** $\delta'=0{,}05\,q_3$, $c=\ln80+\ln(1/q_3)\approx7{,}077$.
- **$A_{\mathrm{SRM}}$.** $\delta'=q_3/m$, $c(m)=\ln(4m)+\ln(1/q_3)$, phụ thuộc $m$.

**Tính đơn điệu.** Trong hai trường hợp đầu, đạo hàm của $(4\ln\tfrac{em}2+c)/m$ theo $m$ bằng $(4-4\ln\tfrac{em}2-c)/m^2<0$ khi $m\ge4$, vì $\ln\tfrac{em}2>1$, như Bước 1 của Ví dụ 03.9. Trong trường hợp thứ ba, tử số là $5\ln m+c_0$ với $c_0=4\ln\tfrac e2+\ln4+\ln(1/q_3)>0$, và đạo hàm của $(5\ln m+c_0)/m$ bằng $(5-5\ln m-c_0)/m^2<0$ khi $m\ge3$. Do đó cỡ mẫu nhỏ nhất thỏa điều kiện cũng thỏa nó với mọi cỡ mẫu lớn hơn. Vì $\rho_m$ không vượt quá dạng chiều VC, cỡ mẫu này là một cận trên của $M_3(0{,}1)$ trong Hệ quả 04.15.

**Giải số.** Chia đôi khoảng tìm cỡ mẫu nhỏ nhất, ta được $172\,279$; $181\,575$; $213\,317$. Kiểm tra: $\varphi$ bằng khoảng $0{,}0099999$ tại các giá trị này và lớn hơn $0{,}01$ tại các giá trị nhỏ hơn một đơn vị. Trong trường hợp thứ ba, $c(213\,317)\approx16{,}35$. Các con số là cỡ mẫu nhỏ nhất của một cận trên, nên chỉ là cỡ mẫu đủ.

### C. Tính toán chi tiết cho các ví dụ

**Bảng của Ví dụ 04.9 và Ví dụ 04.7.** Với $m=10^4$, $\delta=0{,}05$ và $q_k=6/(\pi^2k^2)$, hai số hạng trong căn và số hạng phạt là:

| $k$ | $a=d_k\ln\tfrac{2em}{d_k}$ | $b=\ln\tfrac4{\delta q_k}$ | $\mathrm{pen}_k$ |
|---|---|---|---|
| $1$ | $20{,}42$ | $4{,}880$ | $0{,}1423$ |
| $2$ | $29{,}41$ | $6{,}266$ | $0{,}1690$ |
| $3$ | $38{,}07$ | $7{,}077$ | $0{,}1900$ |
| $4$ | $46{,}47$ | $7{,}652$ | $0{,}2081$ |
| $5$ | $54{,}67$ | $8{,}099$ | $0{,}2241$ |
| $6$ | $62{,}70$ | $8{,}463$ | $0{,}2386$ |
| $7$ | $70{,}59$ | $8{,}772$ | $0{,}2520$ |
| $8$ | $78{,}36$ | $9{,}039$ | $0{,}2644$ |
| $9$ | $86{,}01$ | $9{,}274$ | $0{,}2761$ |
| $10$ | $93{,}56$ | $9{,}485$ | $0{,}2871$ |

Mỗi số hạng phạt bằng $\sqrt{8(a+b)/10^4}$. Không chia xác suất thất bại, $b=\ln80\approx4{,}382$ với mọi $k$. Bảng sau so hai bán kính.

| $k$ | không chia | tỉ số |
|---|---|---|
| $1$ | $0{,}1409$ | $1{,}010$ |
| $2$ | $0{,}1644$ | $1{,}027$ |
| $3$ | $0{,}1843$ | $1{,}031$ |
| $4$ | $0{,}2017$ | $1{,}032$ |
| $5$ | $0{,}2174$ | $1{,}031$ |
| $6$ | $0{,}2317$ | $1{,}030$ |
| $7$ | $0{,}2449$ | $1{,}029$ |
| $8$ | $0{,}2573$ | $1{,}028$ |
| $9$ | $0{,}2689$ | $1{,}027$ |
| $10$ | $0{,}2799$ | $1{,}026$ |

Tỉ số nhỏ nhất là $1{,}010$ tại $k=1$ và lớn nhất là $1{,}032$ tại $k=4$, nên mức tăng ở Ví dụ 04.7 nằm giữa khoảng $1\%$ và $3{,}2\%$.

**Chiều VC của các lớp trong ứng dụng ở §3.** Lớp $\mathcal H_k$ là $\mathcal H^k_{\mathrm{aff}}$ ghép với phép chiếu $\mathrm{pr}_k$ lên $k$ tọa độ đầu. Cận dưới: thêm các tọa độ $0$ vào một tập $k+1$ điểm bị $\mathcal H^k_{\mathrm{aff}}$ tách trọn (Mệnh đề 03.9). Cận trên: nếu $\mathcal H_k$ tách trọn một tập $C$ có ít nhất hai điểm, các ảnh $\mathrm{pr}_k(x)$, $x\in C$, đôi một khác nhau, vì hai điểm cùng ảnh luôn cùng nhãn, và tập ảnh bị $\mathcal H^k_{\mathrm{aff}}$ tách trọn; do đó $\lvert C\rvert\le k+1$. Điều kiện (M) thỏa với lớp con gồm các tham số hữu tỉ, như $\mathcal H^k_{\mathrm{aff}}$ ở Nhận xét 03.14.

**Hệ phương trình chuẩn của Ví dụ 04.4.** Nghiệm bậc $1$ thỏa
$$
\begin{aligned}
3\hat a+\hat b\textstyle\sum_ix_i&=\textstyle\sum_iY_i,\\
\hat a\textstyle\sum_ix_i+\hat b\textstyle\sum_ix_i^2&=\textstyle\sum_ix_iY_i .
\end{aligned}
$$
Với $\sum_ix_i=0$, $\sum_ix_i^2=2$ và $\sum_ix_iY_i=Y_3-Y_1$, hệ cho $\hat a=\bar Y$ và $\hat b=(Y_3-Y_1)/2$.

**Trọng số Lagrange của Ví dụ 04.4.** Với $x_1=-1$, $x_2=0$, $x_3=1$, ba đa thức cơ sở $u_1$, $u_2$, $u_3$ là
$$
\begin{aligned}
u_1(x)&=\tfrac12x(x-1),\\
u_2(x)&=1-x^2,\\
u_3(x)&=\tfrac12x(x+1).
\end{aligned}
$$
Tại $x_0=\tfrac12$, chúng bằng $\tfrac12\cdot\tfrac12\cdot(-\tfrac12)=-\tfrac18$; $1-\tfrac14=\tfrac34$; $\tfrac12\cdot\tfrac12\cdot\tfrac32=\tfrac38$. Tổng bằng $1$, đúng với việc đa thức hằng $1$ được nội suy chính xác.

### D. Ý chứng minh điều kiện cần của Định lý 04.16

::: proof Ý chứng minh Định lý 04.16(a)
**Lộ trình.** Phủ $\mathcal H$ bằng các lớp có cỡ mẫu nhỏ, rồi dùng định lý không có bữa trưa miễn phí để chặn chiều VC của mỗi lớp. Bất đẳng thức then chốt là cận dưới của Định lý 03.17(a).

**Bước 1 (phủ lớp).** Gọi $A$ là một thuật toán học không đều cho $\mathcal H$, với hàm cỡ mẫu $M$. Đặt $\mathcal H_k=\{h\in\mathcal H:M(\tfrac18,\tfrac18,h)\le k\}$. Các lớp này phủ $\mathcal H$ vì $M$ nhận giá trị hữu hạn.

**Bước 2 (giả sử tách trọn).** Giả sử $\mathcal H_k$ tách trọn một tập $2k$ phần tử. Theo Định lý 03.17(a) với $m=k$, có một phân bố $D$ khả thực đối với $\mathcal H_k$, với hàm gán nhãn $h\in\mathcal H_k$ và $L_D(h)=0$, dưới đó $\Pr[L_D(A(S))>\tfrac18]\ge\tfrac17$. Lập luận không có bữa trưa miễn phí của Định lý 03.17(a) (UML §5.1) không dùng điều kiện đầu ra thuộc $\mathcal H_k$, nên áp dụng được cho $A$, có đầu ra trong $\mathcal H$.

**Bước 3 (mâu thuẫn).** Vì $k\ge M(\tfrac18,\tfrac18,h)$, Định nghĩa 04.14 cho $\Pr[L_D(A(S))\le\tfrac18]\ge\tfrac78$, tức xác suất thất bại không quá $\tfrac18<\tfrac17$. Mâu thuẫn này cho chiều VC của $\mathcal H_k$ nhỏ hơn $2k$.

$\square$ Mỗi lớp học được không đều là hợp đếm được của các lớp có chiều VC hữu hạn, tức các lớp học được PAC khi thêm (M) (Định lý 03.17(b)).
:::

### E. Chứng minh cho Thuật toán 04.12

::: proof Chứng minh các khẳng định sau Thuật toán 04.12
**Lộ trình.** So mục tiêu có phạt tại đầu ra với mục tiêu tại từng lớp, tách lớp đã duyệt khỏi lớp chưa duyệt; rồi lặp lại chuỗi bất đẳng thức của Định lý 04.11.

**Bước 1 (lớp đã duyệt).** Với mỗi lớp $k$ đã duyệt, bước 4 và tính $\epsilon_{\mathrm{opt}}$-ERM của bộ giải cho
$$
\begin{aligned}
&L_S(\hat h_{\hat k})+\mathrm{pen}_{\hat k}\\
&\quad\le L_S(\hat h_k)+\mathrm{pen}_k+\tau'\\
&\quad\le\inf_{h\in\mathcal H_k}L_S(h)+\mathrm{pen}_k\\
&\qquad+\epsilon_{\mathrm{opt}}+\tau'.
\end{aligned}
$$

**Bước 2 (lớp chưa duyệt).** Thuật toán dừng ở lớp $k$ khi $\mathrm{pen}_k\ge v$ (sai khác $\tau'$), và $\mathrm{pen}$ không giảm, nên với mọi lớp $k'$ chưa duyệt và mọi $h\in\mathcal H_{k'}$,
$$
\begin{aligned}
&L_S(\hat h_{\hat k})+\mathrm{pen}_{\hat k}\\
&\quad=v\le\mathrm{pen}_{k'}+\tau'\\
&\quad\le L_S(h)+\mathrm{pen}_{k'}+\tau'.
\end{aligned}
$$
Hai bước cho tính $\tau$-chính xác với $\tau=\epsilon_{\mathrm{opt}}+\tau'$.

**Bước 3 (cận tinh hơn).** Khi mọi lớp được duyệt, vế phải của bất đẳng thức thứ nhất ở Bước 1, $L_S(\hat h_k)+\mathrm{pen}_k+\tau'$, bằng $\inf_{h\in\mathcal H_k}L_S(h)+\operatorname{opt}_S(\hat h_k)+\mathrm{pen}_k+\tau'$, với $\operatorname{opt}_S$ tính trên $\mathcal H_k$. Trên biến cố của Bổ đề 04.9, chuỗi bất đẳng thức của Định lý 04.11, với $\operatorname{opt}_S(\hat h_k)+\tau'$ thay cho $\tau$ ở lớp $k$, cho cận tinh hơn.

$\square$ Trong cận tinh hơn, sai số tối ưu thực nghiệm chỉ đi vào qua lớp so sánh; sai số của bộ giải ở các lớp khác không xuất hiện.
:::
