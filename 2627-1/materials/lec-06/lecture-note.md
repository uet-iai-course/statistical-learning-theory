# Bài 06 — Học bằng hạ gradient ngẫu nhiên, chính quy hóa và tính ổn định

Bài 05 chặn độ chênh tối ưu (suboptimality) của một hàm $F$ khi oracle gradient ngẫu nhiên (stochastic gradient oracle) không chệch cho $F$. Trong câu hỏi cuối buổi của Bài 05, chỉ số được rút từ một mẫu $S$ đã lưu; sai số tối ưu thực nghiệm của điểm lặp trung bình khoảng $0{,}0025$, còn sai số ước lượng khoảng $0{,}9025$. Bài 05 kết thúc bằng hai câu hỏi: gradient ngẫu nhiên không chệch cho hàm nào, và khi nào tối thiểu hóa trên $S$ cũng kiểm soát được rủi ro kì vọng (population risk) $L_D$.

Câu hỏi trung tâm của bài là khi nào một thuật toán tối ưu cũng là một thuật toán học, tức có bảo đảm cho rủi ro kì vọng $L_D$ của đầu ra. Hai thuật toán được xét là hạ gradient ngẫu nhiên (stochastic gradient descent, SGD) có chiếu và tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM) có chính quy hóa (regularized ERM). Các công cụ là quan sát mới (fresh observation), khoảng cách tổng quát hóa kì vọng (expected generalization gap), hai mẫu lân cận (neighboring samples) và tính ổn định đều (uniform stability) của thuật toán.

## Câu hỏi mở đầu

Xét lại phân bố $D$ của câu hỏi cuối buổi Bài 05: $X=1$, còn $Y$ nhận $1$ và $-1$ với xác suất $\tfrac12$ mỗi giá trị. Với hàm lỗi bình phương $\ell(w,(x,y))=(wx-y)^2$ trên $W=[-1,1]$, rủi ro kì vọng là $L_D(w)=w^2+1$, nhỏ nhất bằng $1$ tại $w=0$. Hai chương trình chạy SGD có chiếu với $w_1=0$, $T=1600$ bước và $\eta=0{,}00625$, cùng phép cập nhật
$$
w_{t+1}=\operatorname{proj}_W\big(w_t-2\eta(w_t-y_t)\big).
$$
Chúng chỉ khác nhau ở nguồn của nhãn $y_t$.

- **Chương trình thứ nhất.** Ở mỗi bước, $y_t$ là nhãn của một quan sát mới rút từ $D$.
- **Chương trình thứ hai.** Một mẫu $S$ gồm $m=4$ quan sát rút từ $D$ được lưu lại; ở mỗi bước, $y_t$ là nhãn của một quan sát rút đều có hoàn lại từ $S$, tức khoảng $400$ vòng qua dữ liệu.

Hai chương trình có cùng $G=4$, cùng $R=1$ và cùng $T$, và Hệ quả 05.15 cho cận $RG/\sqrt T=0{,}1$.

**Câu hỏi.** Với $\bar w_T$ là điểm lặp trung bình, cận $0{,}1$ có chặn $\mathbb EL_D(\bar w_T)-\min_WL_D$ cho cả hai chương trình không?

Chỉ cho chương trình thứ nhất. Ở chương trình thứ nhất, nhãn mới độc lập với điểm lặp hiện tại, nên gradient ngẫu nhiên không chệch cho $L_D$; theo kì vọng, $L_D(\bar w_T)$ vượt $1$ khoảng $0{,}0006$ (§4). Ở chương trình thứ hai, khi biết $S$, gradient ngẫu nhiên không chệch cho $L_S$, nên cận $0{,}1$ chặn độ chênh tối ưu của $L_S$. Theo kì vọng, độ chênh này khoảng $0{,}001$, trong khi $\mathbb EL_D(\bar w_T)-1\approx0{,}226$ (§5).

Phần chênh nằm ở khoảng cách giữa $L_D$ và $L_S$ tại một điểm chọn theo chính mẫu đó. Với ERM có chính quy hóa, khoảng cách này được chặn bằng tính ổn định của thuật toán (§6–§9).

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Xác định hàm mà gradient ngẫu nhiên không chệch khi dùng quan sát mới và khi rút từ một mẫu đã lưu, rồi suy ra cận rủi ro vượt mức kì vọng khi dùng quan sát mới.
2. Tách rủi ro vượt mức kì vọng của đầu ra một bộ giải thành khoảng cách tổng quát hóa kì vọng và sai số tối ưu thực nghiệm, và chỉ ra bước cần một điểm so sánh không phụ thuộc mẫu.
3. Định nghĩa tính ổn định đều của một thuật toán học và chứng minh rằng nó chặn trị tuyệt đối của khoảng cách tổng quát hóa kì vọng bằng lập luận đổi vai giữa một quan sát huấn luyện và một quan sát mới.
4. Chứng minh cận khoảng cách giữa hai nghiệm của ERM có chính quy hóa trên hai mẫu lân cận, và tính hệ số ổn định cho hồi quy ridge và hồi quy logistic.
5. Chọn hệ số chính quy hóa từ cận đánh đổi khớp–ổn định và tính cỡ mẫu đủ cho một mức rủi ro vượt mức kì vọng; dựng phản ví dụ khi dùng lại mẫu, bỏ chính quy hóa hay bỏ tính bị chặn của dữ liệu.

## Kiến thức tiên quyết

- **Từ Bài 01.** (T1) dạng đầy đủ và dạng yếu, (T2); Định nghĩa 01.4, 01.8, 01.10, 01.12 với hai mức (O1), (O2), 01.14, 01.24; Mệnh đề 01.7, 01.15; Ví dụ 01.8.
- **Từ Bài 02.** Bất đẳng thức Markov (Bổ đề 02.2); hàm lỗi không bị chặn (Nhận xét 02.11); mẫu $\epsilon$-đại diện (Định nghĩa 02.13).
- **Từ Bài 04.** Sai số ước lượng (Định nghĩa 04.1), sai số tối ưu thực nghiệm $\operatorname{opt}_S$ (Định nghĩa 04.2), cận ba thành phần (Mệnh đề 04.3), chọn mô hình bằng mẫu xác thực (Hệ quả 04.17).
- **Từ Bài 05.**
  - **Giải tích lồi:** Định nghĩa 05.1, 05.2, 05.4, 05.6; Mệnh đề 05.3, 05.5; cận $2(BC_x+C_y)C_x$ cho hàm lỗi bình phương trên quả cầu (đoạn sau Định nghĩa 05.4).
  - **SGD:** Định nghĩa 05.10 với (G1), (G2); (C) (đoạn trước Định lý 05.14); Thuật toán 05.11; Định lý 05.14; Hệ quả 05.15, 05.19; Định nghĩa 05.18; Ví dụ 05.9 ($G=1$ cho hàm lỗi logistic).
- **Giải tích và xác suất.** Với $\alpha\in[0,1]$, đẳng thức
  $$
  \begin{aligned}
  &\lVert\alpha a+(1-\alpha)a'\rVert^2\\
  &=\alpha\lVert a\rVert^2+(1-\alpha)\lVert a'\rVert^2\\
  &\quad-\alpha(1-\alpha)\lVert a-a'\rVert^2;
  \end{aligned}
  $$
  bất đẳng thức trung bình cộng–trung bình nhân; định lý Fubini cho hàm không âm (lấy kì vọng theo từng biến độc lập); đổi chỗ hai biến ngẫu nhiên độc lập cùng phân bố không làm đổi phân bố đồng thời.

**Câu hỏi ôn nhanh.**

1. Với $a=1$, $a'=-1$ và $\alpha=\tfrac14$, tính $\alpha a^2+(1-\alpha)a'^2-\big(\alpha a+(1-\alpha)a'\big)^2$ và $\alpha(1-\alpha)(a-a')^2$.
2. Các biến $Y_1,\ldots,Y_4$ độc lập, nhận $\pm1$ với xác suất $\tfrac12$; $\bar Y=\tfrac14\sum_iY_i$ và $\ell(w,y)=(w-y)^2$. Tính $\mathbb E\big[\tfrac14\sum_i\ell(0,Y_i)\big]$ và $\mathbb E\big[\tfrac14\sum_i\ell(\bar Y,Y_i)\big]$, rồi so với $\mathbb E\big[\mathbb E_{Y\sim D}\,\ell(\bar Y,Y)\big]$, trong đó $Y\sim D$ độc lập với $Y_1,\ldots,Y_4$ và có cùng phân bố.
3. Tìm $\lambda>0$ làm nhỏ nhất $0{,}02/\lambda+0{,}5\lambda$ và giá trị nhỏ nhất.

::: solution Lời giải câu hỏi ôn nhanh
1. Ta có $\alpha a+(1-\alpha)a'=\tfrac14-\tfrac34=-\tfrac12$ và $\alpha a^2+(1-\alpha)a'^2=1$, nên hiệu thứ nhất bằng $1-0{,}25=0{,}75$. Biểu thức thứ hai bằng
$$
\tfrac14\cdot\tfrac34\cdot4=0{,}75 .
$$
2. Vì $\ell(0,Y_i)=Y_i^2=1$, kì vọng thứ nhất bằng $1$. Với kì vọng thứ hai, khai triển
$$
\begin{aligned}
&\tfrac14\sum_i(\bar Y-Y_i)^2\\
&=\tfrac14\sum_iY_i^2-\bar Y^2\\
&=1-\bar Y^2 .
\end{aligned}
$$
Các $Y_i$ độc lập, kì vọng $0$, phương sai $1$, nên $\mathbb E\bar Y^2=\tfrac14$ và kì vọng thứ hai bằng $0{,}75$. Với $Y$ độc lập với $\bar Y$, $\mathbb E(\bar Y-Y)^2=\mathbb E\bar Y^2+1=1{,}25$. Với điểm $0$ cố định trước, kì vọng của rủi ro thực nghiệm bằng rủi ro kì vọng (Mệnh đề 01.7); với điểm $\bar Y$ chọn theo mẫu, kì vọng của rủi ro thực nghiệm thấp hơn kì vọng của rủi ro kì vọng $0{,}5$.
3. Theo bất đẳng thức trung bình cộng–trung bình nhân, $0{,}02/\lambda+0{,}5\lambda\ge2\sqrt{0{,}02\cdot0{,}5}=0{,}2$, với dấu bằng khi $0{,}02/\lambda=0{,}5\lambda$, tức
$$
\lambda=\sqrt{0{,}02/0{,}5}=0{,}2 .
$$
Giá trị nhỏ nhất là $0{,}2$.
:::

## 1. Thiết lập bài toán

Bài toán có bảy thành phần. Khác Bài 05, mục tiêu là rủi ro kì vọng của đầu ra, và các quan sát là ngẫu nhiên.

1. **Dữ liệu.** Quan sát $z=(x,y)\in\mathcal Z\subset\mathbb R^p\times\mathcal Y$ từ một phân bố $D$ chưa biết; với hàm lỗi bình phương, thêm $\lVert x\rVert\le C_x$ và $\lvert y\rvert\le C_y$ trên $\mathcal Z$.
2. **Cơ chế lấy mẫu.** Chế độ A: một dòng quan sát mới $Z_1,Z_2,\ldots$ độc lập cùng phân bố $D$, mỗi quan sát dùng một lần. Chế độ B: một mẫu $S\sim D^m$ theo (T1), lưu lại và dùng nhiều lần.
3. **Lớp và hàm lỗi.** Lớp hàm điểm số $\{h_w:w\in W\}$ của Bài 05, với $W\subset\mathbb R^p$ khác rỗng, đóng, lồi; hàm lỗi $\ell(w,z)\ge0$, lồi theo $w$ (bình phương, logistic, bản lề).
4. **Thuật toán.** SGD có chiếu (Thuật toán 05.11) trong hai chế độ; ERM có chính quy hóa (§6).
5. **Mục tiêu.** Rủi ro kì vọng $L_D$ của đầu ra, lấy kì vọng theo mọi nguồn ngẫu nhiên.
6. **Đối tượng so sánh.** Một điểm $u\in W$ cố định, không phụ thuộc mẫu; hoặc $\inf_{w\in W}L_D(w)$; hoặc cận dưới đúng của $L_D$ trên các điểm của $W$ có chuẩn không quá một số cho trước (§9).
7. **Tài nguyên.** Số quan sát ($T-1$ ở chế độ A, $m$ ở chế độ B), số vòng lặp $T$, hệ số chính quy hóa $\lambda$.

Các đại lượng của bài chia theo nguồn ngẫu nhiên như bảng dưới.

| Loại | Đại lượng |
|---|---|
| Cố định | $D$, $W$, $\ell$, $\lambda$, $\eta$, $T$, $w_1$, $u$; các hằng số $G$, $R$, $B$, $C_x$, $C_y$ (§2); $L_D(u)$, $\inf_WL_D$ |
| Ngẫu nhiên theo dữ liệu | dòng $Z_1,Z_2,\ldots$ (chế độ A); mẫu $S$ và hàm $L_S$ (chế độ B); nghiệm của ERM có chính quy hóa (§6) |
| Ngẫu nhiên theo $\xi$ | chỉ số rút từ $S$ ở chế độ B |
| Ngẫu nhiên theo cả hai | điểm lặp và $\bar w_T$ ở chế độ B, cùng $L_D(\bar w_T)$ |

Ở chế độ A, các lần rút chính là các quan sát, không có nguồn ngẫu nhiên riêng. Chứng minh ở §7 thêm một quan sát $Z'\sim D$ độc lập với mẫu và nguồn ngẫu nhiên; quan sát kiểm tra của §7 là một điểm bất kì của $\mathcal Z$, không ngẫu nhiên.

## 2. Kí hiệu và giả thiết

Bảng dưới gồm các kí hiệu dùng từ §3, phần lớn nhắc lại từ Bài 05. Kí hiệu khác được đặt tên tại định nghĩa hay khối dùng nó lần đầu.

| Kí hiệu | Ý nghĩa |
|---|---|
| $w\in W\subset\mathbb R^p$, $h_w(x)=\langle w,x\rangle$ | véc-tơ tham số, tập tham số, hàm điểm số (Bài 05) |
| $\ell(w,z)$, $L_S(w)$, $L_D(w)$ | hàm lỗi và hai rủi ro, viết theo tham số (Bài 05) |
| $B$ | bán kính quả cầu tâm $0$: của $W$ (khi $W$ là quả cầu) hoặc của tập điểm so sánh $W_B$ (§9) |
| $R$; $C_x$, $C_y$ | cận của $\lVert w_1-u\rVert$ (Bài 05); cận của $\lVert x\rVert$, $\lvert y\rvert$ |
| $v(w,z)$ | một dưới gradient của $\ell(\cdot,z)$ tại $w$, chọn đo được theo $(w,z)$ (như Hệ quả 05.19) |
| $\lambda>0$ | hệ số chính quy hóa (regularization parameter) |

Giả thiết thống kê là (T1) và (T2) của Bài 01. Dạng đầy đủ của (T1) được dùng ở §4 (dòng quan sát mới), §7 (đổi vai một quan sát của mẫu với một quan sát mới) và §9; dạng yếu đủ cho §5. Theo (T2), $\ell\ge0$ và $L_D(w)<\infty$ ở mọi điểm được xét. Các kết quả chính của bài không giả sử hàm lỗi bị chặn. Hàm lỗi bình phương và hàm lỗi logistic của mô hình tuyến tính (hàm lỗi log của Nhận xét 02.11) được xét với tính lồi cùng tính Lipschitz trên $W$, hay tính trơn (§8).

Giả thiết tối ưu là (C), (G1), (G2) của Bài 05, dùng ở §4; tính lồi của $\ell(\cdot,z)$; tính Lipschitz của $\ell(\cdot,z)$ trên $W$ (§8); và $\lambda>0$. Ta giả sử ERM có chính quy hóa (§6) được giải đúng, tức mức (O1) của Bài 01 cho mục tiêu có chính quy hóa; nghiệm gần đúng được xét ở cuối §9.

## 3. Ví dụ xuyên suốt

::: example Ví dụ 06.1 (Mẫu bốn quan sát cho hồi quy trên đoạn $[-1,1]$)
**Thiết lập.** Cho $p=1$, $\mathcal Z=[-1,1]\times[-1,1]$, nên $C_x=C_y=1$. Mẫu cố định gồm $m=4$ quan sát
$$
\begin{aligned}
z_1&=(1,1),\quad z_2=(1,0),\\
z_3&=(0{,}5;1),\quad z_4=(-1,-1).
\end{aligned}
$$
Hàm lỗi bình phương $\ell(w,(x,y))=(wx-y)^2$ và $W=[-1,1]$, tức $B=1$. Ví dụ chưa có đại lượng ngẫu nhiên nào.

**Bước 1: ba tổng.** Ta có
$$
\begin{aligned}
\textstyle\sum_ix_i^2&=1+1+0{,}25+1\\
&=3{,}25,\\
\textstyle\sum_ix_iy_i&=1+0+0{,}5+1\\
&=2{,}5,\\
\textstyle\sum_iy_i^2&=1+0+1+1=3 .
\end{aligned}
$$

**Bước 2: rủi ro thực nghiệm.** Khai triển $(wx_i-y_i)^2=x_i^2w^2-2x_iy_iw+y_i^2$ và lấy trung bình:
$$
L_S(w)=\tfrac14\big(3{,}25w^2-5w+3\big).
$$

**Bước 3: hằng số Lipschitz.** Với $w\in W$ và $z\in\mathcal Z$, đạo hàm theo $w$ là $2(wx-y)x$, và
$$
\begin{aligned}
&\lvert2(wx-y)x\rvert\\
&\le2(BC_x+C_y)C_x\\
&=2(1+1)\cdot1=4 .
\end{aligned}
$$
Theo Mệnh đề 05.5(a), $\ell(\cdot,z)$ là $4$-Lipschitz trên $W$ với mọi $z\in\mathcal Z$, tức $G=4$.

**Bước 4: nghiệm ERM.** Đặt đạo hàm $\tfrac14(6{,}5w-5)$ bằng $0$, ta được
$$
w=\frac{2{,}5}{3{,}25}\approx0{,}7692\in W .
$$
Hàm $L_S$ là đa thức bậc hai có hệ số dẫn dương, nên điểm này là nghiệm ERM trên $W$, với $L_S(0{,}7692)\approx0{,}2692$.

**Kết luận.** Nghiệm ERM nằm trong $W$ và $G=4$. Ở §6, ta thêm một số hạng chính quy hóa và thay quan sát thứ tư để đo nghiệm thay đổi bao nhiêu.
:::

::: application Bảo đảm cho rủi ro kì vọng của hồi quy logistic trên một triệu hồ sơ
**Thiết lập.** Tiếp ứng dụng của Bài 05: $m=10^6$ hồ sơ, $\lVert x\rVert\le1$, nhãn $\tilde y=2y-1$ và hàm lỗi logistic $\ell(w,(x,y))=\ln\big(1+e^{-\tilde y\langle w,x\rangle}\big)$, với $G=1$ (Ví dụ 05.9).

**Kết quả của Bài 05.** Trên quả cầu $\lVert w\rVert\le5$ (giá trị giả định), $10^4$ bước SGD đủ để $\mathbb E_\xi\operatorname{opt}_S\le0{,}05$. Đây là cận cho $L_S$, không cho $L_D$.

**Câu hỏi thực hành.** So với hàm tốt nhất trong quả cầu $\lVert u\rVert\le5$, bảo đảm nào cho $L_D$ đúng với (i) SGD đi đúng một vòng qua $10^6$ hồ sơ, và (ii) ERM có chính quy hóa với hệ số chọn trước khi thấy mẫu? Câu trả lời ở §4 và §9. Ứng dụng không dùng số liệu thật.
:::

## 4. Hạ gradient ngẫu nhiên với quan sát mới

Định lý 05.14 cần một oracle không chệch cho hàm mục tiêu. Với $F=L_D$, một lần rút là một quan sát $Z\sim D$, và gradient ngẫu nhiên là một dưới gradient $v(w,Z)$ của $\ell(\cdot,Z)$. Cần kiểm tra rằng kì vọng của $v(w,Z)$ theo $Z$ là một dưới gradient của $L_D$ tại $w$.

::: lemma Bổ đề 06.1 (Kì vọng của dưới gradient) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Hàm lỗi.** Với mọi $z\in\mathcal Z$, $\ell(\cdot,z):\mathbb R^p\to[0,\infty)$ lồi, và $\ell(w,\cdot)$ đo được với mọi $w$.
- **Khả tích.** $L_D(w)=\mathbb E_{Z\sim D}\,\ell(w,Z)<\infty$ với mọi $w\in\mathbb R^p$.
- **Dưới gradient.** $v:\mathbb R^p\times\mathcal Z\to\mathbb R^p$ đo được, $v(w,z)\in\partial\ell(\cdot,z)(w)$ với mọi $(w,z)$, và $\mathbb E_{Z\sim D}\lVert v(w,Z)\rVert<\infty$ tại điểm $w$ đang xét.

**Bảo đảm.** Hai khẳng định tất định về hàm $L_D$.

- **(a) Tính lồi.** $L_D$ lồi và hữu hạn trên $\mathbb R^p$.
- **(b) Dưới gradient.** $\psi(w)=\mathbb E_{Z\sim D}\,v(w,Z)$ thuộc $\partial L_D(w)$.
:::

::: proof Chứng minh Bổ đề 06.1
**Lộ trình.** Lấy kì vọng theo $Z$ của một bất đẳng thức đúng với từng $z$.

**Bước 1 (phần a).** Với $w,u\in\mathbb R^p$, $\alpha\in[0,1]$ và mọi $z$, Định nghĩa 05.1 cho $\ell(\alpha w+(1-\alpha)u,z)\le\alpha\ell(w,z)+(1-\alpha)\ell(u,z)$. Ba số hạng khả tích theo giả thiết khả tích. Lấy kì vọng theo $Z\sim D$, ta được
$$
\begin{aligned}
&L_D(\alpha w+(1-\alpha)u)\\
&\quad\le\alpha L_D(w)+(1-\alpha)L_D(u).
\end{aligned}
$$

**Bước 2 (phần b).** Với mọi $u\in\mathbb R^p$ và mọi $z$, bất đẳng thức dưới gradient cho
$$
\begin{aligned}
\ell(u,z)&\ge\ell(w,z)\\
&\quad+\langle v(w,z),u-w\rangle .
\end{aligned}
$$
Hai số hạng đầu khả tích theo giả thiết khả tích. Số hạng cuối khả tích vì $\lvert\langle v(w,z),u-w\rangle\rvert\le\lVert v(w,z)\rVert\,\lVert u-w\rVert$ (Cauchy–Schwarz) và $\mathbb E\lVert v(w,Z)\rVert<\infty$. Lấy kì vọng theo $Z$ và dùng tính tuyến tính của kì vọng, ta được $L_D(u)\ge L_D(w)+\langle\psi(w),u-w\rangle$ với mọi $u$, tức $\psi(w)\in\partial L_D(w)$.

$\square$ Với quan sát mới, gradient ngẫu nhiên là một dưới gradient không chệch của chính $L_D$, kể cả với hàm lỗi bản lề không khả vi; không cần đổi chỗ đạo hàm và kì vọng.
:::

Với oracle rút một quan sát mới ($\Xi=\mathcal Z$, $P_\xi=D$, $\varphi=v$), phần (b) của bổ đề là (G1) cho $F=L_D$, và phần (a) cùng tính lồi, đóng của $W$ là (C).

::: corollary Hệ quả 06.2 (Hạ gradient ngẫu nhiên với quan sát mới) — chứng minh đầy đủ
**Giả thiết.** Năm thành phần sau.

- **Dữ liệu.** $Z_1,Z_2,\ldots$ độc lập cùng phân bố $D$ (dạng đầy đủ của (T1) cho một dòng quan sát).
- **Hàm lỗi.** Như Bổ đề 06.1, với quy tắc dưới gradient đo được $v$.
- **Cận gradient.** $G>0$ và $\mathbb E_{Z\sim D}\lVert v(w,Z)\rVert^2\le G^2$ với mọi $w\in W$; điều kiện này thỏa khi $\ell(\cdot,z)$ là $G$-Lipschitz trên một tập mở chứa $W$ với mọi $z$ (Mệnh đề 05.5(b)).
- **Tập tham số.** $W$ khác rỗng, đóng, lồi; $w_1\in W$ tất định; $R>0$.
- **Thuật toán.** Thuật toán 05.11 với $\xi_t=Z_t$, $\varphi(w,z)=v(w,z)$ và $\eta=R/(G\sqrt T)$.

**Bảo đảm.** Theo kì vọng theo $Z_1,\ldots,Z_{T-1}$:

- **(a) Một điểm so sánh.** Với mọi $u\in W$ thỏa $\lVert w_1-u\rVert\le R$,
  $$
  \mathbb EL_D(\bar w_T)-L_D(u)\le\frac{RG}{\sqrt T}.
  $$
- **(b) Cả tập tham số.** Nếu $\lVert w_1-u\rVert\le R$ với mọi $u\in W$ thì
  $$
  \begin{aligned}
  &\mathbb EL_D(\bar w_T)-\inf_{w\in W}L_D(w)\\
  &\quad\le\frac{RG}{\sqrt T}.
  \end{aligned}
  $$
- **(c) Số quan sát.** Với $\epsilon>0$, điều kiện $T\ge R^2G^2/\epsilon^2$ đủ để các vế trái ở (a) và (b) không quá $\epsilon$.

Ta gọi đại lượng ở (b) là *rủi ro vượt mức kì vọng*: kì vọng theo mọi nguồn ngẫu nhiên của rủi ro vượt mức (Định nghĩa 01.24) so với $W$, tức của sai số ước lượng (Định nghĩa 04.1). Đầu ra $\bar w_T$ dùng đúng $T-1$ quan sát, mỗi quan sát một lần (đoạn sau Thuật toán 05.11). Cận là một bảo đảm *cấp thuật toán*, tức cho đầu ra của một thuật toán cụ thể, khác bảo đảm *cấp lớp* đúng đồng thời cho mọi giả thuyết của lớp (Bài 02–04); nó phụ thuộc $p$ chỉ qua $G$ và $R$.
:::

::: proof Chứng minh Hệ quả 06.2
**Lộ trình.** Kiểm ba giả thiết của Định lý 05.14 với $F=L_D$, rồi áp dụng Hệ quả 05.15.

**Bước 1 (oracle; dạng đầy đủ của (T1)).** Các $Z_t$ độc lập cùng phân bố $D$, nên $(v,D)$ có cấu trúc của Định nghĩa 05.10 với các lần rút $\xi_t=Z_t$; tính độc lập được dùng ở đây. Theo bất đẳng thức Cauchy–Schwarz và giả thiết cận gradient, $\mathbb E\lVert v(w,Z)\rVert\le G<\infty$ trên $W$, nên Bổ đề 06.1(b) cho (G1) với $F=L_D$. (G2) là giả thiết cận gradient.

**Bước 2 (tính lồi).** Bổ đề 06.1(a) cho $L_D$ lồi và hữu hạn trên $\mathbb R^p$; cùng với $W$ khác rỗng, đóng, lồi, đó là (C).

**Bước 3 (cận).** Hệ quả 05.15(a), (b), (c) với $F=L_D$ cho ba khẳng định. Kì vọng của Hệ quả 05.15 lấy theo $\xi_1,\ldots,\xi_{T-1}$, tức theo $Z_1,\ldots,Z_{T-1}$.

$\square$ Với quan sát mới, bộ giải của Bài 05 là một thuật toán học, và cỡ mẫu của nó bằng số bước trừ một.
:::

::: example Ví dụ 06.2 (Chương trình dùng quan sát mới)
**Thiết lập.** Phân bố $D$ của câu hỏi mở đầu ($X=1$, $Y=\pm1$ với xác suất $\tfrac12$), hàm lỗi bình phương, $W=[-1,1]$, $w_1=0$, $T=1600$ và $v(w,(x,y))=2(wx-y)x$. Các nhãn $y_1,\ldots,y_{T-1}$ là ngẫu nhiên, độc lập.

**Bước 1: hằng số.** Với $w\in W$, $\lvert v(w,(1,\pm1))\rvert=2\lvert w\mp1\rvert\le4$, nên $G=4$. Mọi $u\in W$ cách $w_1=0$ không quá $1$, nên $R=1$. Độ dài bước là
$$
\eta=\frac{R}{G\sqrt T}=\frac1{4\cdot40}=0{,}00625 .
$$

**Bước 2: cận.** Với $\min_WL_D=L_D(0)=1$, Hệ quả 06.2(b) cho
$$
\mathbb EL_D(\bar w_{1600})-1\le\frac{1\cdot4}{40}=0{,}1,
$$
với $1599$ quan sát mới.

**Bước 3: dạng của điểm lặp trung bình.** Phép cập nhật là $w_{t+1}=(1-2\eta)w_t+2\eta y_t$. Vì $2\eta<1$, đây là tổ hợp lồi của $w_t$ và $y_t\in\{-1,1\}$, nên mọi điểm lặp nằm trong $W$ và phép chiếu không tác động. Do đó
$$
\bar w_T=\sum_{t=1}^{T-1}c_ty_t,
$$
trong đó các hệ số $c_t$ tất định (công thức ở Phụ lục D), với $\sum_tc_t\approx0{,}95$ và $\sum_tc_t^2\approx0{,}000578$. Khi mọi nhãn bằng $1$, $\bar w_T=\sum_tc_t$; đó là giá trị $\bar w_{1600}\approx0{,}95$ trong câu hỏi cuối buổi Bài 05.

**Bước 4: giá trị đúng.** Vì $L_D(w)=w^2+1$, ta có $L_D(\bar w_T)-1=\bar w_T^2$. Các $y_t$ độc lập, kì vọng $0$ và $y_t^2=1$, nên các tích chéo có kì vọng $0$ và
$$
\begin{aligned}
&\mathbb EL_D(\bar w_T)-1\\
&=\mathbb E\bar w_T^2\\
&=\textstyle\sum_tc_t^2\approx0{,}000578 .
\end{aligned}
$$

**Kết luận.** Với chương trình thứ nhất, rủi ro vượt mức kì vọng khoảng $0{,}0006$, nhỏ hơn cận $0{,}1$ khoảng $173$ lần.
:::

::: remark Nhận xét 06.3 (Một vòng qua mẫu theo thứ tự)
Cho $S=(Z_1,\ldots,Z_m)\sim D^m$ theo (T1). SGD xử lý $Z_1,\ldots,Z_m$ đúng một lần theo thứ tự, với $T=m+1$; đầu ra $\bar w_{m+1}$ chỉ dùng $Z_1,\ldots,Z_m$. Đây chính là thuật toán của Hệ quả 06.2, nên với các giả thiết của hệ quả,
$$
\begin{aligned}
&\mathbb E_SL_D(\bar w_{m+1})-\inf_WL_D\\
&\quad\le\frac{RG}{\sqrt{m+1}} .
\end{aligned}
$$
Hai chế độ của §1 khác nhau ở việc dùng lại quan sát; lưu mẫu mà dùng mỗi quan sát một lần vẫn cho cận của Hệ quả 06.2. Với ứng dụng ở §3 ($G=1$, $W$ là quả cầu bán kính $5$ giả định, $w_1=0$, nên $R=5$), một vòng qua $10^6$ hồ sơ cho cận $5/\sqrt{10^6+1}\approx0{,}005$. Từ vòng thứ hai, điểm lặp $w_t$ phụ thuộc quan sát sắp được dùng, nên Bước 1 của chứng minh Hệ quả 06.2 không còn đúng (§5).
:::

Hệ quả 06.2 cần một quan sát mới cho mỗi bước; với $m$ quan sát, chỉ chạy được $m+1$ bước như vậy.

## 5. Tối ưu trên một mẫu cố định

Khi chỉ số được rút đều có hoàn lại từ một mẫu $S$ đã lưu, Hệ quả 05.19 chặn $\mathbb E_\xi\operatorname{opt}_S(\bar w_T)$ với mọi $S$. Đại lượng cần chặn là $L_D(\bar w_T)$, và đầu ra phụ thuộc chính mẫu $S$. Khi biết $S$ và lịch sử, kì vọng có điều kiện của gradient ngẫu nhiên $g_t$ là một dưới gradient của $L_S$ tại $w_t$, không phải của $L_D$.

::: definition Định nghĩa 06.4 (Khoảng cách tổng quát hóa kì vọng)
Cho cỡ mẫu $m$ và ba thành phần sau.

- **Thuật toán.** $A$ có nguồn ngẫu nhiên riêng (Định nghĩa 05.18), đầu ra trong $\mathcal H$ (trong bài: $A(S;\xi)\in W$, viết theo tham số).
- **Mẫu và nguồn ngẫu nhiên.** $S\sim D^m$ và $\xi\sim P_\xi$ độc lập với $S$.
- **Hàm lỗi.** $\ell$ thỏa (T2), với $\mathbb E_{S,\xi}L_D(A(S;\xi))<\infty$ và $\mathbb E_{S,\xi}L_S(A(S;\xi))<\infty$.

*Khoảng cách tổng quát hóa kì vọng* của $A$ với cỡ mẫu $m$ là số thực
$$
\begin{aligned}
&\mathbb E_{S,\xi}\big[L_D(A(S;\xi))\\
&\quad-L_S(A(S;\xi))\big].
\end{aligned}
$$
:::

Khoảng cách tổng quát hóa kì vọng là một số có dấu, phụ thuộc $D$, $m$ và $A$. Khi $A$ tất định, nó là kì vọng theo $S$ của khoảng cách tổng quát hóa ở Định nghĩa 01.10.

Ba ví dụ. Với $A$ trả về một $h$ cố định, khoảng cách tổng quát hóa kì vọng bằng $0$ (Mệnh đề 01.7). Với $A_{\mathrm{gn}}$ dưới phân bố của Ví dụ 01.8, nó bằng $1$ với mọi $m$ (Mệnh đề 01.15(b)). Với thuật toán trả về $\bar Y$ trong câu hỏi ôn nhanh 2, nó bằng $1{,}25-0{,}75=0{,}5$.

Đại lượng $\mathbb E_{S,\xi}\lvert L_D(A(S;\xi))-L_S(A(S;\xi))\rvert$ không phải khoảng cách tổng quát hóa kì vọng: nó có thể dương khi khoảng cách tổng quát hóa kì vọng bằng $0$ (§7).

Mệnh đề sau là bản kì vọng của Mệnh đề 04.3 cho một thuật toán.

::: proposition Mệnh đề 06.5 (Phân tích rủi ro của đầu ra tính trên một mẫu cố định) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau.

- **Mẫu.** $S=(Z_1,\ldots,Z_m)$, mỗi $Z_i$ có phân bố $D$ (dạng yếu của (T1) đủ).
- **Thuật toán.** $A$ có nguồn ngẫu nhiên riêng, $\xi$ độc lập với $S$; đầu ra $\tilde w=A(S;\xi)\in W$, với $\mathbb EL_D(\tilde w)<\infty$ và $\mathbb EL_S(\tilde w)<\infty$.
- **Hàm lỗi.** $\ell\ge0$ đo được, $L_D(w)<\infty$ với mọi $w\in W$.
- **Điểm so sánh.** $u\in W$ cố định, không phụ thuộc $S$ và $\xi$.

Kí hiệu $\operatorname{opt}_S(w)=L_S(w)-\inf_{w'\in W}L_S(w')$ (Định nghĩa 04.2 cho lớp $\{h_w:w\in W\}$).

**Bảo đảm.** Hai khẳng định.

- **(a) Đẳng thức trên từng mẫu.** Với mọi giá trị của $(S,\xi)$,
  $$
  \begin{aligned}
  &L_D(\tilde w)-L_D(u)\\
  &=\big[L_D(\tilde w)-L_S(\tilde w)\big]\\
  &\quad+\big[L_S(\tilde w)-L_S(u)\big]\\
  &\quad+\big[L_S(u)-L_D(u)\big],
  \end{aligned}
  $$
  trong đó số hạng giữa không quá $\operatorname{opt}_S(\tilde w)$ và số hạng cuối có kì vọng $0$ theo $S$.
- **(b) Cận theo kì vọng.** Theo kì vọng theo $(S,\xi)$,
  $$
  \begin{aligned}
  &\mathbb EL_D(\tilde w)-\inf_{w\in W}L_D(w)\\
  &\le\mathbb E\big[L_D(\tilde w)-L_S(\tilde w)\big]\\
  &\quad+\mathbb E\operatorname{opt}_S(\tilde w).
  \end{aligned}
  $$

Vế trái của (b) là rủi ro vượt mức kì vọng so với $W$; vế phải là khoảng cách tổng quát hóa kì vọng của chính thuật toán (Định nghĩa 06.4) cộng kì vọng của sai số tối ưu thực nghiệm. So với Mệnh đề 04.3, số hạng $2r$ của lớp được thay bằng khoảng cách tổng quát hóa kì vọng của thuật toán, và không có sai số xấp xỉ vì đối tượng so sánh nằm trong $W$.
:::

::: proof Chứng minh Mệnh đề 06.5
**Lộ trình.** Thêm bớt rủi ro thực nghiệm như Bước 1 của chứng minh Mệnh đề 04.3, rồi lấy kì vọng thay vì dùng tính đại diện của mẫu.

**Bước 1 (đẳng thức).** Cộng và trừ $L_S(\tilde w)$ và $L_S(u)$; các số hạng đều hữu hạn trên từng mẫu vì $\ell$ nhận giá trị thực và $L_D<\infty$ trên $W$.

**Bước 2 (số hạng giữa; $u\in W$).** Vì $u\in W$, ta có $L_S(u)\ge\inf_{w'\in W}L_S(w')$, nên
$$
L_S(\tilde w)-L_S(u)\le\operatorname{opt}_S(\tilde w).
$$

**Bước 3 (số hạng cuối; $u$ không phụ thuộc mẫu).** Vì $u$ cố định và mỗi $Z_i$ có phân bố $D$, Mệnh đề 01.7 cho $\mathbb E_SL_S(u)=L_D(u)$. Nếu $u$ được chọn theo $S$, chẳng hạn $u=\tilde w$, bước này không còn đúng.

**Bước 4 (kì vọng).** Các số hạng ở (a) khả tích: $\mathbb EL_S(u)=L_D(u)<\infty$, còn $\mathbb EL_D(\tilde w)$ và $\mathbb EL_S(\tilde w)$ hữu hạn theo giả thiết. Lấy kì vọng ở (a) và dùng Bước 2, Bước 3:
$$
\begin{aligned}
&\mathbb EL_D(\tilde w)-L_D(u)\\
&\le\mathbb E\big[L_D(\tilde w)-L_S(\tilde w)\big]\\
&\quad+\mathbb E\operatorname{opt}_S(\tilde w).
\end{aligned}
$$
Vế phải không phụ thuộc $u$. Lấy cận dưới đúng của $L_D(u)$ theo $u\in W$ ở vế trái, ta được (b).

$\square$ Muốn đánh giá $L_D(\tilde w)$, cần một cận cho khoảng cách tổng quát hóa kì vọng của thuật toán, hoặc một mẫu kiểm tra độc lập với $S$ (Mệnh đề 01.7); Hệ quả 05.19 chỉ chặn số hạng thứ hai.
:::

::: example Ví dụ 06.3 (Chương trình chạy nhiều vòng qua một mẫu)
**Thiết lập.** Phân bố $D$, $W$, $w_1$, $T=1600$ và $\eta=0{,}00625$ như Ví dụ 06.2. Mẫu $S=((1,Y_1),\ldots,(1,Y_4))\sim D^4$ là ngẫu nhiên, khác mẫu cố định của Ví dụ 06.1; chỉ số $i_t$ đều trên $\{1,2,3,4\}$, rút có hoàn lại, độc lập với $S$. Kí hiệu $\bar Y=\tfrac14\sum_iY_i$. Đây là chương trình thứ hai của câu hỏi mở đầu.

**Bước 1: hàm mà oracle không chệch.** Khi biết $S$ và lịch sử, kì vọng của $g_t=2(w_t-Y_{i_t})$ theo $i_t$ là
$$
\begin{aligned}
\mathbb E[g_t\mid\cdot]&=2(w_t-\bar Y)\\
&=L_S'(w_t),
\end{aligned}
$$
còn $L_D'(w_t)=2w_t$. Hiệu $-2\bar Y$ khác $0$ trừ khi $\bar Y=0$, biến cố có xác suất $\tfrac6{16}=0{,}375$.

**Bước 2: dạng của điểm lặp trung bình.** Như Ví dụ 06.2, phép chiếu không tác động, và $\bar w_T=\sum_tc_tY_{i_t}$ với cùng các hệ số $c_t$.

**Bước 3: hai mô-men.** Với $t=s$, $\mathbb E[Y_{i_t}Y_{i_s}]=1$. Với $t\ne s$, $\Pr(i_t=i_s)=\tfrac14$; khi $i_t=i_s$, tích bằng $1$, còn khi $i_t\ne i_s$, tích có kì vọng $0$. Do đó $\mathbb E[Y_{i_t}Y_{i_s}]=\Pr(i_t=i_s)$ với $t\ne s$. Khai triển bình phương và dùng $\sum_{t\ne s}c_tc_s=(\sum_tc_t)^2-\sum_tc_t^2$, với $m=4$:
$$
\begin{aligned}
\mathbb E\bar w_T^2&=\textstyle\sum_tc_t^2+\tfrac1m\sum_{t\ne s}c_tc_s\\
&=\tfrac1m\big(\textstyle\sum_tc_t\big)^2\\
&\quad+\big(1-\tfrac1m\big)\textstyle\sum_tc_t^2\\
&\approx\tfrac{0{,}9025}{4}+0{,}75\cdot0{,}000578\\
&\approx0{,}2261 .
\end{aligned}
$$
Ở Bước 4, ta cần thêm mô-men chéo. Vì $\mathbb E[Y_j\bar Y]=\tfrac14$ với mọi $j$, ta có $\mathbb E[\bar w_T\bar Y]=\tfrac14\sum_tc_t\approx0{,}2375$.

**Bước 4: ba đại lượng.** Rủi ro kì vọng là $L_D(w)=w^2+1$, rủi ro thực nghiệm là $L_S(w)=w^2-2w\bar Y+1$, và $\inf_WL_S=L_S(\bar Y)=1-\bar Y^2$. Theo Bước 3,
$$
\begin{aligned}
&\mathbb EL_D(\bar w_T)\approx1{,}2261,\\
&\mathbb EL_S(\bar w_T)\\
&\quad\approx0{,}2261-0{,}4750+1\\
&\quad=0{,}7511,\\
&\mathbb E\inf_WL_S=1-\tfrac14=0{,}75 .
\end{aligned}
$$
Do đó $\mathbb E\operatorname{opt}_S(\bar w_T)\approx0{,}0011$, đúng với cận $0{,}1$ của Hệ quả 05.19.

**Bước 5: phân tích theo Mệnh đề 06.5 với $u=0$.** Vì $y^2=1$, $L_S(0)=L_D(0)=1$ trên mọi mẫu, nên số hạng cuối bằng $0$. Khoảng cách tổng quát hóa kì vọng là
$$
\begin{aligned}
1{,}2261-0{,}7511&=0{,}4750\\
&=\tfrac2m\textstyle\sum_tc_t .
\end{aligned}
$$
Số hạng giữa có kì vọng $0{,}7511-1=-0{,}2489$, và tổng $0{,}4750-0{,}2489=0{,}2261$. Cận (b) của Mệnh đề 06.5 cho $0{,}4750+0{,}0011=0{,}4761\ge0{,}2261$.

**Kết luận.** Sai số tối ưu thực nghiệm nhỏ ($0{,}0011$), nhưng rủi ro vượt mức kì vọng $0{,}2261$ lớn hơn cận $0{,}1$. Toàn bộ phần chênh nằm ở khoảng cách tổng quát hóa kì vọng; chạy thêm vòng lặp không làm nó giảm (Phụ lục D).
:::

Chúng ta cần một cách chặn khoảng cách tổng quát hóa kì vọng theo tính chất của thuật toán, không qua hội tụ đều của cả lớp (Bài 02–04, Định nghĩa 02.13). Thuật toán là ERM có chính quy hóa (§6); công cụ là tính ổn định (§7).

## 6. ERM có chính quy hóa

Trên mẫu của Ví dụ 06.1, nghiệm ERM là $0{,}7692$. Thay quan sát thứ tư $(-1,-1)$ bằng $(1,-1)$, tổng $\sum_ix_iy_i$ giảm từ $2{,}5$ xuống $0{,}5$, còn $\sum_ix_i^2$ giữ nguyên, nên theo Bước 4 của Ví dụ 06.1 nghiệm ERM trở thành $0{,}5/3{,}25\approx0{,}1538$. Một quan sát trong bốn làm nghiệm dịch $0{,}6154$, gần một phần ba đường kính của $W$. Thêm vào $L_S$ một số hạng phạt chuẩn của $w$ làm nghiệm ít nhạy hơn.

::: definition Định nghĩa 06.6 (ERM có chính quy hóa)
Cho $W\subset\mathbb R^p$ khác rỗng, đóng, lồi, hàm lỗi $\ell(w,z)$ và một mẫu $s\in\mathcal Z^m$. Quy tắc gồm ba thành phần.

- **Hệ số chính quy hóa.** Một số $\lambda>0$, chọn trước khi thấy mẫu.
- **Mục tiêu có chính quy hóa.** Hàm $F_{s,\lambda}(w)=L_s(w)+\tfrac\lambda2\lVert w\rVert^2$ trên $\mathbb R^p$, gọi là *mục tiêu có chính quy hóa* (regularized objective).
- **Đầu ra.** Một điểm $\hat w_s\in W$ đạt giá trị nhỏ nhất của $F_{s,\lambda}$ trên $W$; khi cần ghi $\lambda$, viết $\hat w_{s,\lambda}$, và với mẫu ngẫu nhiên, $F_{S,\lambda}$ và $\hat w_S$.

Quy tắc $s\mapsto\hat w_s$ được gọi là *ERM có chính quy hóa* (còn gọi là chính quy hóa Tikhonov, Tikhonov regularization). Với hàm lỗi bình phương, nó được gọi là *hồi quy ridge* (ridge regression).
:::

Số hạng $\tfrac\lambda2\lVert w\rVert^2$ phạt các điểm có chuẩn lớn. Hệ số $\lambda$ cố định; $\hat w_S$ ngẫu nhiên theo $S$. Khi $\ell(\cdot,z)$ lồi với mọi $z$, điểm đạt giá trị nhỏ nhất tồn tại và duy nhất, như chứng minh dưới đây; khi đó $\hat w_s$ xác định.

Với $\lambda=0$, quy tắc là ERM trên $W$ (Định nghĩa 01.8), và nghiệm có thể không duy nhất. Chẳng hạn, với $p=2$, một quan sát $x=(1,0)$, $y=1$, hàm lỗi bình phương và $W=\mathbb R^2$, mọi điểm $w=(1,t)$ đều có $L_S(w)=0$.

Tối thiểu hóa $L_S$ trên quả cầu $\{w:\lVert w\rVert\le r\}$ không thuộc định nghĩa: quy tắc đó dùng ràng buộc thay cho số hạng phạt.

Các lập luận về ERM có chính quy hóa ở §8–§9 dùng hai tính chất của $F_{s,\lambda}$: nó lồi mạnh (strongly convex), và một hàm lồi mạnh tăng ít nhất bậc hai khi rời điểm cực tiểu, gọi là *tăng trưởng bậc hai* (quadratic growth). Bổ đề sau phát biểu tính chất thứ hai cho một hàm lồi mạnh bất kì trên một tập lồi.

::: lemma Bổ đề 06.7 (Tăng trưởng bậc hai quanh điểm cực tiểu của hàm lồi mạnh) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Hàm.** $f:\mathbb R^p\to\mathbb R$ là $\lambda$-lồi mạnh (Định nghĩa 05.6), với $\lambda>0$.
- **Tập.** $W\subset\mathbb R^p$ khác rỗng, lồi.
- **Điểm cực tiểu.** $u\in W$ với $f(u)=\min_{w\in W}f(w)$.

**Bảo đảm.** Tất định: với mọi $w\in W$,
$$
f(w)-f(u)\ge\tfrac\lambda2\lVert w-u\rVert^2 .
$$
:::

::: proof Chứng minh Bổ đề 06.7
**Lộ trình.** So $f(u)$ với giá trị của $f$ tại một điểm trên đoạn thẳng từ $u$ đến $w$, rồi cho điểm đó dần về $u$.

**Bước 1 (một điểm trên đoạn; tính lồi của $W$).** Cố định $w\in W$ và $\alpha\in(0,1]$. Điểm $u+\alpha(w-u)=\alpha w+(1-\alpha)u$ thuộc $W$ vì $W$ lồi; tính lồi của $W$ được dùng ở đây. Do đó
$$
\begin{aligned}
f(u)&\le f(u+\alpha(w-u))\\
&\le\alpha f(w)+(1-\alpha)f(u)\\
&\quad-\tfrac\lambda2\alpha(1-\alpha)\lVert w-u\rVert^2 .
\end{aligned}
$$
Bất đẳng thức thứ nhất do $u$ là điểm cực tiểu trên $W$; bất đẳng thức thứ hai là định nghĩa lồi mạnh với cặp $(w,u)$ và trọng số $\alpha$.

**Bước 2 (chia và lấy giới hạn).** Chuyển $(1-\alpha)f(u)$ sang vế trái và chia cho $\alpha>0$:
$$
\begin{aligned}
&f(w)-f(u)\\
&\quad\ge\tfrac\lambda2(1-\alpha)\lVert w-u\rVert^2 .
\end{aligned}
$$
Cho $\alpha\to0^+$, ta được bảo đảm.

$\square$ Chứng minh không dùng đạo hàm hay điều kiện tối ưu bậc nhất, nên bất đẳng thức đúng cả khi $u$ nằm trên biên của $W$ và $f$ không khả vi.
:::

Với $f=F_{s,\lambda}$, Bổ đề 06.7 cho tính duy nhất của nghiệm; sự tồn tại cần thêm một lập luận compact.

::: lemma Bổ đề 06.8 (Tính lồi mạnh, sự tồn tại và tính duy nhất của nghiệm có chính quy hóa) — phác thảo (sự tồn tại chứng minh ở Phụ lục A)
**Giả thiết.** Ba thành phần sau.

- **Tập tham số.** $W\subset\mathbb R^p$ khác rỗng, đóng, lồi.
- **Hàm lỗi.** Với mọi $z$, $\ell(\cdot,z):\mathbb R^p\to\mathbb R$ lồi (không cần $\ell\ge0$).
- **Chính quy hóa.** $\lambda>0$; mẫu $s\in\mathcal Z^m$ cố định.

**Bảo đảm.** Ba khẳng định tất định, đúng với mọi mẫu.

- **(a) Lồi mạnh.** $F_{s,\lambda}$ là $\lambda$-lồi mạnh.
- **(b) Tồn tại.** $F_{s,\lambda}$ đạt giá trị nhỏ nhất trên $W$.
- **(c) Duy nhất và tăng trưởng bậc hai.** Điểm đạt giá trị nhỏ nhất là duy nhất, kí hiệu $\hat w_s$, và với mọi $w\in W$,
  $$
  \begin{aligned}
  &F_{s,\lambda}(w)-F_{s,\lambda}(\hat w_s)\\
  &\quad\ge\tfrac\lambda2\lVert w-\hat w_s\rVert^2 .
  \end{aligned}
  $$
:::

::: proof Chứng minh Bổ đề 06.8 (phác thảo)
**Lộ trình.** Phần (a) cộng một bất đẳng thức lồi với một đẳng thức của chuẩn; phần (b) dùng tính compact (chi tiết ở Phụ lục A); phần (c) là Bổ đề 06.7.

**Bước 1 (phần a).** Theo đẳng thức của mục Giải tích và xác suất, với mọi $w,u$ và $\alpha\in[0,1]$,
$$
\begin{aligned}
&\tfrac\lambda2\lVert\alpha w+(1-\alpha)u\rVert^2\\
&=\alpha\tfrac\lambda2\lVert w\rVert^2+(1-\alpha)\tfrac\lambda2\lVert u\rVert^2\\
&\quad-\tfrac\lambda2\alpha(1-\alpha)\lVert w-u\rVert^2 .
\end{aligned}
$$
Vậy $\tfrac\lambda2\lVert\cdot\rVert^2$ thỏa Định nghĩa 05.6 với dấu bằng. Hàm $L_s$ lồi vì là trung bình của các hàm lồi $\ell(\cdot,z_i)$. Cộng bất đẳng thức lồi của $L_s$ với đẳng thức trên, ta được bất đẳng thức lồi mạnh cho $F_{s,\lambda}$.

**Bước 2 (phần b).** Hàm $F_{s,\lambda}$ lồi và hữu hạn nên liên tục, và tiến ra vô cùng khi $\lVert w\rVert\to\infty$, vì $L_s$ bị chặn dưới bởi một hàm afin còn $\tfrac\lambda2\lVert w\rVert^2$ tăng bậc hai. Do đó nó đạt giá trị nhỏ nhất trên tập đóng $W$ (Phụ lục A).

**Bước 3 (phần c).** Nếu $u$ và $u'$ cùng đạt giá trị nhỏ nhất, Bổ đề 06.7 với $f=F_{s,\lambda}$ cho
$$
\begin{aligned}
0&=F_{s,\lambda}(u')-F_{s,\lambda}(u)\\
&\ge\tfrac\lambda2\lVert u'-u\rVert^2,
\end{aligned}
$$
nên $u'=u$. Bất đẳng thức của (c) là Bổ đề 06.7 với $u=\hat w_s$.

$\square$ Với $\lambda>0$ và hàm lỗi lồi, ERM có chính quy hóa luôn có đúng một nghiệm, nên $\hat w_S$ là đầu ra xác định của một thuật toán học (tính đo được giả sử như cuối Phụ lục A).
:::

::: example Ví dụ 06.4 (Hồi quy ridge trên mẫu bốn quan sát)
**Thiết lập.** Mẫu $S$, hàm lỗi bình phương và $W=[-1,1]$ của Ví dụ 06.1, với $\lambda\in\{0,1,4\}$. Mẫu $S^{(4)}$ thu được từ $S$ khi thay quan sát thứ tư $z_4=(-1,-1)$ bằng $z'=(1,-1)$. Không có đại lượng ngẫu nhiên.

**Bước 1: hai mục tiêu.** Với $S^{(4)}$, $\sum_ix_i^2=3{,}25$ không đổi vì $1^2=(-1)^2$, $\sum_ix_iy_i=0{,}5$ và $\sum_iy_i^2=3$. Theo Bước 2 của Ví dụ 06.1,
$$
\begin{aligned}
&F_{S,\lambda}(w)=\tfrac\lambda2w^2\\
&\quad+\tfrac14\big(3{,}25w^2-5w+3\big),\\
&F_{S^{(4)},\lambda}(w)=\tfrac\lambda2w^2\\
&\quad+\tfrac14\big(3{,}25w^2-w+3\big).
\end{aligned}
$$

**Bước 2: nghiệm.** Đạo hàm của $F_{S,\lambda}$ là $\tfrac14(6{,}5w-5)+\lambda w$; đặt bằng $0$, ta được
$$
\begin{aligned}
\hat w_S&=\frac{2{,}5}{3{,}25+2\lambda},\\
\hat w_{S^{(4)}}&=\frac{0{,}5}{3{,}25+2\lambda}.
\end{aligned}
$$
Mỗi mục tiêu là đa thức bậc hai có hệ số dẫn dương, và cả hai điểm thuộc $W$, nên chúng là các nghiệm trên $W$ (duy nhất khi $\lambda>0$, theo Bổ đề 06.8(c)). Công thức chung trong một chiều là $\hat w=\sum_ix_iy_i\big/\big(\sum_ix_i^2+\lambda m/2\big)$, khi giá trị này thuộc $W$ (luôn đúng với $W=\mathbb R$).

**Bước 3: ba giá trị của $\lambda$.** Thay $\lambda=0,1,4$ vào hai công thức trên và vào $L_S$ của Ví dụ 06.1:

- **$\lambda=0$.** $\hat w_S\approx0{,}7692$, $\hat w_{S^{(4)}}\approx0{,}1538$, khoảng cách $0{,}6154$, $L_S(\hat w_S)\approx0{,}2692$.
- **$\lambda=1$.** $\hat w_S=10/21\approx0{,}4762$, $\hat w_{S^{(4)}}=2/21\approx0{,}0952$, khoảng cách $8/21\approx0{,}3810$, $L_S(\hat w_S)\approx0{,}3390$.
- **$\lambda=4$.** $\hat w_S=2/9\approx0{,}2222$, $\hat w_{S^{(4)}}=2/45\approx0{,}0444$, khoảng cách $0{,}1778$, $L_S(\hat w_S)\approx0{,}5123$.

Khoảng cách ở đây là $\lvert\hat w_S-\hat w_{S^{(4)}}\rvert$.

**Bước 4: so sánh.** Khi $\lambda$ tăng từ $0$ lên $4$, khoảng cách giữa hai nghiệm giảm từ $0{,}6154$ xuống $0{,}1778$, còn $L_S(\hat w_S)$ tăng từ $0{,}2692$ lên $0{,}5123$ (Hình 06.1).

**Kết luận.** Chính quy hóa đổi độ khớp trên mẫu lấy độ nhạy thấp khi thay một quan sát.
:::

![Hai đồ thị của mục tiêu có chính quy hóa theo w trên đoạn từ −0,25 đến 1. Mỗi đồ thị có một đường liền cho mẫu S và một đường đứt cho mẫu thay quan sát thứ tư. Với λ = 0, hai điểm cực tiểu là 0,769 và 0,154, cách nhau 0,615. Với λ = 4, hai điểm cực tiểu là 0,222 và 0,044, cách nhau 0,178.](img/lec-06/ridge-thay-mot-quan-sat.svg)

*Hình 06.1. Mục tiêu có chính quy hóa của mẫu $S$ (nét liền, điểm cực tiểu tròn đặc) và của mẫu $S^{(4)}$ (nét đứt, điểm cực tiểu vuông rỗng) trong Ví dụ 06.4, với $\lambda=0$ (trái) và $\lambda=4$ (phải): thay một quan sát dịch điểm cực tiểu $0{,}615$ khi không chính quy hóa và $0{,}178$ khi $\lambda=4$; hai khung dùng thang tung khác nhau.*

## 7. Tính ổn định và khoảng cách tổng quát hóa kì vọng

Mệnh đề 06.5 cần một cận cho khoảng cách tổng quát hóa kì vọng của một thuật toán. Cận dưới đây không dùng cấu trúc của lớp, chỉ dùng một tính chất của chính thuật toán: khi thay một quan sát của mẫu, hàm lỗi của đầu ra tại mọi điểm thay đổi ít.

::: definition Định nghĩa 06.9 (Mẫu lân cận và tính ổn định đều)
Cho thuật toán học $A$ có nguồn ngẫu nhiên riêng (Định nghĩa 05.18), hàm lỗi $\ell$ và cỡ mẫu $m$. Định nghĩa gồm bốn thành phần.

- **Mẫu lân cận.** Với $s=(z_1,\ldots,z_m)\in\mathcal Z^m$, $i\in\{1,\ldots,m\}$ và $z'\in\mathcal Z$, đặt
  $$
  \begin{aligned}
  s^{(i)}=(&z_1,\ldots,z_{i-1},z',\\
  &z_{i+1},\ldots,z_m).
  \end{aligned}
  $$
  Hai mẫu $s$ và $s^{(i)}$ là *hai mẫu lân cận*; $z'$ là *quan sát thay thế* (replacement observation).
- **Quan sát kiểm tra.** Một điểm $z\in\mathcal Z$ bất kì, gọi là *quan sát kiểm tra* (test observation).
- **Hệ số ổn định.** Một số $\epsilon_{\mathrm{stab}}(m)\ge0$, gọi là *hệ số ổn định* (stability coefficient).
- **Điều kiện.** Với mọi $s$, $i$, $z'$ và $z$, các kì vọng sau hữu hạn và
  $$
  \begin{aligned}
  \Big\lvert\,&\mathbb E_\xi\,\ell(A(s;\xi),z)\\
  &-\mathbb E_\xi\,\ell(A(s^{(i)};\xi),z)\Big\rvert\\
  &\le\epsilon_{\mathrm{stab}}(m).
  \end{aligned}
  $$

Khi điều kiện đúng, $A$ được gọi là *ổn định đều* với hệ số ổn định $\epsilon_{\mathrm{stab}}(m)$.
:::

Lượng từ "với mọi" chạy trên mọi mẫu, kể cả mẫu có xác suất $0$ dưới $D$. Hai kì vọng lấy theo cùng $P_\xi$, cho hai lần chạy riêng; với $A$ tất định, bỏ $\mathbb E_\xi$. Với mẫu ngẫu nhiên, ta viết $S^{(i)}$ và $Z'$.

Nếu thay hiệu hai kì vọng bằng $\mathbb E_\xi\lvert\ell(A(s;\xi),z)-\ell(A(s^{(i)};\xi),z)\rvert$, với hai lần chạy dùng chung $\xi$, ta được một điều kiện mạnh hơn; Bài 08 dùng dạng này cho SGD với hàm lỗi lồi, trơn và Lipschitz. UML dùng một dạng yếu hơn, lấy trung bình theo mẫu (Phụ lục E).

Thuật toán ghi nhớ $A_{\mathrm{gn}}$ với hàm lỗi 0–1 có hệ số ổn định nhỏ nhất bằng $1$ với mọi $m$. Lấy một mẫu có $z_i=(x_i,1)$, với $x_i$ xuất hiện đúng một lần, rồi thay $z_i$ bằng một quan sát tại điểm khác. Dự đoán tại $x_i$ đổi từ $1$ sang $0$, nên hàm lỗi tại quan sát kiểm tra $z=(x_i,1)$ đổi từ $0$ sang $1$.

Ngược lại, ERM trên $W$ trong Ví dụ 06.4 ($\lambda=0$) không có hệ số ổn định nhỏ: thay quan sát thứ tư làm hàm lỗi tại quan sát kiểm tra $z=(1,-1)$ đổi $304/169\approx1{,}7988$, giá trị lớn nhất trên $\mathcal Z$; với $\lambda=0$, hệ số không giảm theo $m$ (§8).

Chứng minh của định lý dưới đây dùng *lập luận đổi vai* (exchange argument): thêm một quan sát $Z'\sim D$ độc lập với $(S,\xi)$ rồi đổi vai nó với $Z_i$. Quan sát này không phải mẫu bóng $S'$ của Bài 03.

::: theorem Định lý 06.10 (Tính ổn định chặn khoảng cách tổng quát hóa kì vọng) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau.

- **Mẫu.** $S=(Z_1,\ldots,Z_m)\sim D^m$ theo (T1), dạng đầy đủ.
- **Thuật toán.** $A$ có nguồn ngẫu nhiên riêng (Định nghĩa 05.18), $\xi\sim P_\xi$ độc lập với $S$, ổn định đều với hệ số $\epsilon_{\mathrm{stab}}(m)$ (Định nghĩa 06.9).
- **Hàm lỗi.** $\ell$ thỏa (T2); không cần bị chặn.
- **Khả tích.** $\mathbb E_{S,\xi}L_D(A(S;\xi))<\infty$.

**Bảo đảm.** Theo kì vọng theo $(S,\xi)$,
$$
\begin{aligned}
\Big\lvert\,&\mathbb E_{S,\xi}\big[L_D(A(S;\xi))\\
&-L_S(A(S;\xi))\big]\Big\rvert\le\epsilon_{\mathrm{stab}}(m).
\end{aligned}
$$

Đại lượng được chặn là trị tuyệt đối của khoảng cách tổng quát hóa kì vọng (Định nghĩa 06.4), không phải $\mathbb E\lvert L_D-L_S\rvert$; không có cận với xác suất cao. Bảo đảm là cấp thuật toán, không dùng chiều VC hay $p$, và phụ thuộc $m$ chỉ qua $\epsilon_{\mathrm{stab}}(m)$. Giả thiết khả tích và tính ổn định đều kéo theo $\mathbb EL_S(A(S;\xi))<\infty$ (Bước 2 của chứng minh).
:::

::: proof Chứng minh Định lý 06.10
**Lộ trình.** Lập luận đổi vai: thêm một quan sát mới $Z'$, đổi vai $Z'$ với $Z_i$, so hai đầu ra trên hai mẫu lân cận, rồi lấy trung bình theo $i$. Đặt $Z'\sim D$ độc lập với $(S,\xi)$, và $S^{(i)}$ là $S$ với $Z_i$ thay bằng $Z'$. Mọi kì vọng không có chỉ số lấy theo $(S,Z',\xi)$.

**Bước 1 (rủi ro kì vọng là hàm lỗi trên một quan sát mới; tính độc lập của $Z'$ và (T2)).** Hàm $(s,\xi,z)\mapsto\ell(A(s;\xi),z)$ đo được và không âm (Định nghĩa 05.18, (T2)). Vì $Z'$ độc lập với $(S,\xi)$, định lý Fubini cho phép lấy kì vọng theo $Z'$ trước:
$$
\begin{aligned}
&\mathbb E\,\ell(A(S;\xi),Z')\\
&\quad=\mathbb EL_D(A(S;\xi)).
\end{aligned}
$$

**Bước 2 (đổi vai; (T1) và tính độc lập của $\xi$).** Các thành phần của bộ $(Z_1,\ldots,Z_m,Z',\xi)$ độc lập, và $Z_1,\ldots,Z_m,Z'$ cùng phân bố $D$; dạng đầy đủ của (T1) được dùng ở đây. Đổi chỗ $Z_i$ và $Z'$ không làm đổi phân bố đồng thời của bộ này. Phép đổi chỗ biến cặp $(S,Z')$ thành $(S^{(i)},Z_i)$, nên với mọi $i$,
$$
\begin{aligned}
&\mathbb E\,\ell(A(S;\xi),Z')\\
&\quad=\mathbb E\,\ell(A(S^{(i)};\xi),Z_i).
\end{aligned}
$$
Theo Bước 1, cả hai vế bằng $\mathbb EL_D(A(S;\xi))<\infty$. Còn cần $\mathbb E\,\ell(A(S;\xi),Z_i)<\infty$; tính ổn định đều được dùng ở đây. Với $(s,z')$ cố định, Định nghĩa 06.9 với quan sát kiểm tra $z_i$ cho
$$
\begin{aligned}
&\mathbb E_\xi\,\ell(A(s;\xi),z_i)\\
&\le\mathbb E_\xi\,\ell(A(s^{(i)};\xi),z_i)\\
&\quad+\epsilon_{\mathrm{stab}}(m).
\end{aligned}
$$
Lấy kì vọng theo $(S,Z')$ (định lý Fubini cho hàm không âm) và dùng đẳng thức vừa chứng minh:
$$
\begin{aligned}
&\mathbb E\,\ell(A(S;\xi),Z_i)\\
&\le\mathbb E\,\ell(A(S^{(i)};\xi),Z_i)\\
&\quad+\epsilon_{\mathrm{stab}}(m)\\
&=\mathbb EL_D(A(S;\xi))\\
&\quad+\epsilon_{\mathrm{stab}}(m)<\infty .
\end{aligned}
$$
Vậy mọi số hạng dưới đây hữu hạn.

**Bước 3 (rủi ro thực nghiệm).** Theo định nghĩa của $L_S$ và tính tuyến tính của kì vọng,
$$
\begin{aligned}
&\mathbb EL_S(A(S;\xi))\\
&\quad=\frac1m\sum_{i=1}^m\mathbb E\,\ell(A(S;\xi),Z_i).
\end{aligned}
$$

**Bước 4 (hiệu; tính ổn định).** Lấy trung bình theo $i$ của Bước 1–2 rồi trừ Bước 3:
$$
\begin{aligned}
&\mathbb E\big[L_D(A(S;\xi))-L_S(A(S;\xi))\big]\\
&=\frac1m\sum_{i=1}^m\mathbb E\big[\ell(A(S^{(i)};\xi),Z_i)\\
&\qquad-\ell(A(S;\xi),Z_i)\big].
\end{aligned}
$$
Trong số hạng thứ $i$, lấy kì vọng theo $\xi$ trước, với $(S,Z')$ cố định; điều này hợp lệ theo định lý Fubini vì $\xi$ độc lập với $(S,Z')$. Với $S=s$ và $Z'=z'$, ta được
$$
\begin{aligned}
&\mathbb E_\xi\,\ell(A(s^{(i)};\xi),z_i)\\
&\quad-\mathbb E_\xi\,\ell(A(s;\xi),z_i).
\end{aligned}
$$
Theo Định nghĩa 06.9 với quan sát kiểm tra $z=z_i$, trị tuyệt đối của hiệu này không quá $\epsilon_{\mathrm{stab}}(m)$; tính ổn định đều được dùng ở đây. Lấy kì vọng theo $(S,Z')$ và dùng bất đẳng thức tam giác cho trung bình theo $i$, ta được bảo đảm.

$\square$ Với thuật toán ổn định đều, khoảng cách tổng quát hóa kì vọng không vượt $\epsilon_{\mathrm{stab}}(m)$, bất kể kích thước của lớp giả thuyết. Định lý chỉ nói về hiệu $L_D-L_S$, không nói gì về $L_D$ của đầu ra.
:::

Các đẳng thức ở Bước 1–3 cho thấy khoảng cách tổng quát hóa kì vọng bằng đúng trung bình ở vế phải của Bước 4. Đẳng thức này được dùng lại ở §8 và ở Phụ lục E.

Với thuật toán ghi nhớ dưới phân bố của Ví dụ 01.8, cả hai vế của Định lý 06.10 bằng $1$ (Mệnh đề 01.15(b)): cận đạt được nhưng không cho thông tin. Câu cuối của chứng minh Hệ quả 01.29 nói một bảo đảm học có thể dựa trên tính chất của một thuật toán cụ thể; Định lý 06.10 là một bảo đảm như vậy.

::: example Ví dụ 06.5 (Thuật toán hằng)
**Thiết lập.** *Thuật toán hằng* (constant algorithm) trả về cùng một hàm phân lớp $h_0\equiv0$ với mọi mẫu. Cho $X\sim U[0,1]$, nhãn $Y=\mathbb 1[X>\tfrac12]$, hàm lỗi 0–1 và $S\sim D^m$.

**Bước 1: hệ số ổn định.** Đầu ra không phụ thuộc mẫu, nên hệ số ổn định bằng $0$. Theo Định lý 06.10, khoảng cách tổng quát hóa kì vọng bằng $0$.

**Bước 2: rủi ro.** Hàm lỗi $\ell(h_0,Z)=Y$ có phân bố Bernoulli với tham số $\tfrac12$, nên $L_D(h_0)=\tfrac12$, trong khi hàm phân lớp $\mathbb 1[x>\tfrac12]$ có rủi ro $0$.

**Bước 3: kì vọng của trị tuyệt đối.** Số $mL_S(h_0)$ có phân bố nhị thức với tham số $(m,\tfrac12)$, nên
$$
\begin{aligned}
&\mathbb E\big\lvert L_S(h_0)-\tfrac12\big\rvert\\
&=2^{-m}\sum_{k=0}^m\binom mk\Big\lvert\frac km-\frac12\Big\rvert .
\end{aligned}
$$
Tổng này bằng $0{,}1230$; $0{,}0398$; $0{,}0126$ với $m=10$; $100$; $1000$. Các số gần $1/\sqrt{2\pi m}$, vì $L_S(h_0)$ xấp xỉ chuẩn với độ lệch chuẩn $\sigma=1/(2\sqrt m)$ và $\mathbb E\lvert N(0,\sigma^2)\rvert=\sigma\sqrt{2/\pi}$.

**Kết luận.** Tính ổn định không kéo theo rủi ro thấp. Ở đây $\lvert\mathbb E[L_D-L_S]\rvert=0$, còn $\mathbb E\lvert L_D-L_S\rvert>0$ với mọi $m$: Định lý 06.10 chỉ chặn đại lượng thứ nhất.
:::

Để dùng Định lý 06.10, cần một thuật toán có hệ số ổn định nhỏ. Ở §8, ta chứng minh ERM có chính quy hóa là một thuật toán như vậy.

## 8. Tính ổn định của ERM có chính quy hóa

Trong Ví dụ 06.4, khoảng cách giữa hai nghiệm giảm từ $0{,}6154$ xuống $0{,}1778$ khi $\lambda$ tăng từ $0$ lên $4$. Mệnh đề dưới đây chặn khoảng cách này cho mọi mẫu, mọi cách thay một quan sát và mọi hàm lỗi lồi, Lipschitz trên $W$. Ta gọi giả thiết sau là (L): với mọi $z\in\mathcal Z$, $\ell(\cdot,z)$ là $G$-Lipschitz trên $W$ (Định nghĩa 05.4). Đây là điều kiện trên giá trị của hàm lỗi tại các điểm của $W$; chứng minh dưới đây chỉ so giá trị tại hai điểm của $W$, nên không cần một tập mở chứa $W$.

::: proposition Mệnh đề 06.11 (Tính ổn định của ERM có chính quy hóa) — phác thảo (chi tiết ở Phụ lục B)
**Giả thiết.** Bốn thành phần sau.

- **Tập tham số.** $W\subset\mathbb R^p$ khác rỗng, đóng, lồi (có thể là $\mathbb R^p$).
- **Hàm lỗi.** Với mọi $z\in\mathcal Z$, $\ell(\cdot,z):\mathbb R^p\to\mathbb R$ lồi và không âm trên $W$; (L) đúng với hằng số $G$.
- **Chính quy hóa.** $\lambda>0$; $\hat w_s$ như Định nghĩa 06.6, xác định nhờ Bổ đề 06.8.
- **Mẫu.** $s\in\mathcal Z^m$, $i\in\{1,\ldots,m\}$ và $z'\in\mathcal Z$ bất kì; $s^{(i)}$ như Định nghĩa 06.9.

**Bảo đảm.** Hai khẳng định tất định, đúng với mọi mẫu và không cần $D$.

- **(a) Khoảng cách giữa hai nghiệm.**
  $$
  \lVert\hat w_s-\hat w_{s^{(i)}}\rVert\le\frac{2G}{\lambda m}.
  $$
- **(b) Ổn định đều.** Với mọi $z\in\mathcal Z$,
  $$
  \begin{aligned}
  &\big\lvert\ell(\hat w_s,z)-\ell(\hat w_{s^{(i)}},z)\big\rvert\\
  &\quad\le\frac{2G^2}{\lambda m},
  \end{aligned}
  $$
  tức ERM có chính quy hóa ổn định đều với $\epsilon_{\mathrm{stab}}(m)=2G^2/(\lambda m)$.

Hệ số ổn định phụ thuộc $G$, $\lambda$ và $m$; nó không phụ thuộc trực tiếp vào $p$, $D$ hay bán kính của $W$; với hàm lỗi bình phương, $G$ phụ thuộc bán kính. Thuật toán tất định, nên không có $\mathbb E_\xi$.
:::

::: proof Chứng minh Mệnh đề 06.11 (phác thảo)
**Lộ trình.** Viết bất đẳng thức tăng trưởng bậc hai cho hai mục tiêu, cộng lại, triệt tiêu các số hạng chung, rồi dùng tính Lipschitz hai lần. Bất đẳng thức then chốt là tổng của hai bất đẳng thức tăng trưởng bậc hai. Đặt $\hat w=\hat w_s$ và $\hat w'=\hat w_{s^{(i)}}$; cả hai thuộc $W$.

**Bước 1 (hai bất đẳng thức; tính lồi của $\ell$ và của $W$, $\lambda>0$).** Bổ đề 06.8(c) cho $F_{s,\lambda}$ tại $w=\hat w'$ và cho $F_{s^{(i)},\lambda}$ tại $w=\hat w$:
$$
\begin{aligned}
&F_{s,\lambda}(\hat w')-F_{s,\lambda}(\hat w)\\
&\quad\ge\tfrac\lambda2\lVert \hat w-\hat w'\rVert^2,\\
&F_{s^{(i)},\lambda}(\hat w)-F_{s^{(i)},\lambda}(\hat w')\\
&\quad\ge\tfrac\lambda2\lVert \hat w-\hat w'\rVert^2 .
\end{aligned}
$$

**Bước 2 (cộng và triệt tiêu).** Hai mục tiêu chỉ khác nhau ở quan sát thứ $i$, nên $F_{s,\lambda}-F_{s^{(i)},\lambda}=\tfrac1m\big[\ell(\cdot,z_i)-\ell(\cdot,z')\big]$; số hạng chính quy hóa và $m-1$ số hạng chung triệt tiêu (Phụ lục B). Cộng hai bất đẳng thức của Bước 1, ta được
$$
\begin{aligned}
&\lambda\lVert \hat w-\hat w'\rVert^2\\
&\le\tfrac1m\big[\ell(\hat w',z_i)-\ell(\hat w,z_i)\big]\\
&\quad+\tfrac1m\big[\ell(\hat w,z')-\ell(\hat w',z')\big].
\end{aligned}
$$

**Bước 3 (Lipschitz hai lần; (L) với $z_i$ và $z'$).** Vì $\hat w,\hat w'\in W$, (L) cho mỗi ngoặc vuông không quá $G\lVert \hat w-\hat w'\rVert$, nên vế phải không quá $2G\lVert \hat w-\hat w'\rVert/m$. Nếu $\hat w\ne \hat w'$, chia hai vế cho $\lambda\lVert \hat w-\hat w'\rVert$, ta được (a); nếu $\hat w=\hat w'$, vế trái của (a) bằng $0$.

**Bước 4 (phần b; (L) với $z$).** Với mọi $z\in\mathcal Z$,
$$
\begin{aligned}
&\lvert\ell(\hat w,z)-\ell(\hat w',z)\rvert\\
&\le G\lVert \hat w-\hat w'\rVert\le\frac{2G^2}{\lambda m}.
\end{aligned}
$$

$\square$ Hệ số ổn định của ERM có chính quy hóa giảm như $1/(\lambda m)$: mỗi quan sát chỉ chiếm trọng số $1/m$ trong mục tiêu, còn số hạng chính quy hóa giữ độ cong $\lambda$ cố định.
:::

::: example Ví dụ 06.6 (Hệ số ổn định của hồi quy ridge)
**Thiết lập.** Tiếp Ví dụ 06.4: $G=4$ và $m=4$ (Ví dụ 06.1), $W=[-1,1]$, $\lambda\in\{1,4\}$, thay $z_4=(-1,-1)$ bằng $z'=(1,-1)$.

**Bước 1: hai cận.** Theo Mệnh đề 06.11,
$$
\begin{aligned}
\frac{2G}{\lambda m}&=\frac{2\cdot4}{4\lambda}=\frac2\lambda,\\
\frac{2G^2}{\lambda m}&=\frac{2\cdot16}{4\lambda}=\frac8\lambda .
\end{aligned}
$$
Với $\lambda=1$, hai cận là $2$ và $8$; với $\lambda=4$, chúng là $0{,}5$ và $2$.

**Bước 2: kiểm Bước 2–3 của chứng minh tại $\lambda=1$.** Ở đây $\hat w=10/21$ và $\hat w'=2/21$. Hai hiệu hàm lỗi là
$$
\begin{aligned}
&\ell(\hat w',z_4)-\ell(\hat w,z_4)\\
&\quad=\big(\tfrac{19}{21}\big)^2-\big(\tfrac{11}{21}\big)^2\\
&\quad=\tfrac{240}{441}\approx0{,}5442,\\
&\ell(\hat w,z')-\ell(\hat w',z')\\
&\quad=\big(\tfrac{31}{21}\big)^2-\big(\tfrac{23}{21}\big)^2\\
&\quad=\tfrac{432}{441}\approx0{,}9796 .
\end{aligned}
$$
Vế phải của Bước 2 là $\tfrac14(0{,}5442+0{,}9796)\approx0{,}3810$, và chuỗi bất đẳng thức là
$$
\begin{aligned}
&\lambda\lVert \hat w-\hat w'\rVert^2\approx0{,}1451\\
&\le0{,}3810\\
&\le2G\lVert \hat w-\hat w'\rVert/m\approx0{,}7619 .
\end{aligned}
$$

**Kết luận.** Theo Ví dụ 06.4, Bước 3, khoảng cách thật là $0{,}3810\le2$ khi $\lambda=1$ và $0{,}1778\le0{,}5$ khi $\lambda=4$: cận đúng nhưng lỏng khoảng $5$ lần ở $\lambda=1$.
:::

::: example Ví dụ 06.7 (Bỏ chính quy hóa)
**Thiết lập.** Mẫu gồm $m-1$ bản sao của $(0,0)$ và $z_m=(1,1)$; mẫu lân cận thay $z_m$ bằng $(1,-1)$. Hàm lỗi bình phương, $W=[-1,1]$ và $G=4$; giả thiết $\lambda>0$ bị bỏ.

**Bước 1: $\lambda=0$.** Các quan sát $(0,0)$ có hàm lỗi $0$, nên $L_S(w)=\tfrac1m(w\mp1)^2$ trên hai mẫu. ERM trên $W$ cho hai nghiệm $1$ và $-1$, cách nhau bằng đường kính $2$ của $W$; hàm lỗi tại $(1,1)$ đổi từ $0$ lên $4$, với mọi $m$.

**Bước 2: $\lambda=0{,}1$.** Trên hai mẫu, $\sum_ix_iy_i=\pm1$ và $\sum_ix_i^2=1$, nên theo công thức một chiều của Ví dụ 06.4, hai nghiệm là $\pm1/(1+\lambda m/2)=\pm2/(2+\lambda m)$. Khoảng cách $4/(2+0{,}1m)$ bằng $1{,}3333$; $0{,}3333$; $0{,}0392$ với $m=10$; $100$; $1000$. Cận $8/(\lambda m)$ tương ứng là $8$; $0{,}8$; $0{,}08$; khi $m$ lớn, cận chỉ lỏng khoảng hai lần.

**Bước 3: chỗ chứng minh hỏng.** Không có $\lambda>0$, Bước 1 của chứng minh Mệnh đề 06.11 chỉ còn hệ số lồi mạnh của chính $L_S$. Ở đây $L_S(w)=\tfrac1m(w-1)^2$ có đạo hàm bậc hai $2/m$, nên nó là $(2/m)$-lồi mạnh. Với $\hat w$, $\hat w'$ là hai nghiệm ERM, cộng hai bất đẳng thức tăng trưởng bậc hai với hệ số $2/m$ thay cho $\lambda$, rồi dùng (L) như Bước 2–3:
$$
\begin{aligned}
\tfrac2m\lvert\hat w-\hat w'\rvert^2&\le\tfrac{2G}m\lvert\hat w-\hat w'\rvert,\\
\lvert\hat w-\hat w'\rvert&\le G=4,
\end{aligned}
$$
lớn hơn đường kính $2$ của $W$ và không giảm theo $m$.

**Kết luận.** Không có chính quy hóa, ERM ở đây không ổn định đều với một hệ số giảm theo $m$. Lớp này vẫn có tính hội tụ đều, vì dữ liệu và $W$ bị chặn (chứng minh ở Bài 07); ví dụ cho thấy công cụ ổn định cần chính quy hóa, không cho thấy ERM quá khớp.
:::

::: example Ví dụ 06.8 (Hàm lỗi tuyến tính đạt cận khoảng cách giữa hai nghiệm)
**Thiết lập.** Cho $p=1$, $\mathcal Z=\{-1,1\}$ với $D$ đều, $\lambda=0{,}1$, $m=100$, $W=[-10,10]$ và hàm lỗi tuyến tính $\ell(w,z)=10-zw$. Hàm lỗi không âm trên $W$ và $1$-Lipschitz, nên $G=1$.

**Bước 1: nghiệm.** Với $\bar z=\tfrac1m\sum_iz_i$, mục tiêu là $F_{S,\lambda}(w)=10-\bar zw+\tfrac\lambda2w^2$, nên $\hat w_S=\bar z/\lambda\in W$.

**Bước 2: cận (a) đạt được.** Thay một $z_i=1$ bằng $z'=-1$ làm $\bar z$ giảm $2/m$, nên hai nghiệm cách nhau đúng $2/(\lambda m)=0{,}2$.

**Bước 3: khoảng cách tổng quát hóa kì vọng.** Vì $\mathbb EZ=0$, $L_D(w)=10$ với mọi $w$. Thay $\hat w_S$, $L_S(\hat w_S)=10-\bar z^2/\lambda$, nên $L_D(\hat w_S)-L_S(\hat w_S)=\bar z^2/\lambda$. Biến $\bar z$ là trung bình của $m$ biến độc lập có kì vọng $0$ và phương sai $1$, nên $\mathbb E\bar z^2=1/m$, và khoảng cách tổng quát hóa kì vọng bằng $1/(\lambda m)=0{,}1$, so với cận $0{,}2$.

**Kết luận.** Cận (a) của Mệnh đề 06.11 không cải thiện được; cận cho khoảng cách tổng quát hóa kì vọng lỏng hai lần.
:::

::: example Ví dụ 06.9 (Dữ liệu không bị chặn)
**Thiết lập.** Hồi quy ridge một chiều với $W=\mathbb R$, $\lambda=1$ và $m=100$. Mẫu $S$ gồm $100$ bản sao của $(1,1)$; mẫu $S^{(100)}$ thay quan sát cuối bằng $z'=(M,0)$, với $M>0$.

**Bước 1: nghiệm trên $S$.** Theo công thức một chiều của Ví dụ 06.4, $\hat w_S=100/(100+50)\approx0{,}6667$.

**Bước 2: nghiệm trên mẫu lân cận.** Với $\sum_ix_iy_i=99$ và $\sum_ix_i^2=99+M^2$,
$$
\hat w_{S^{(100)}}=\frac{99}{99+M^2+50},
$$
bằng $0{,}6600$; $0{,}3976$; $0{,}0098$ với $M=1$; $10$; $100$.

**Bước 3: thay đổi hàm lỗi.** Tại quan sát kiểm tra $(1,1)$, hàm lỗi $(w-1)^2$ đổi $0{,}0045$; $0{,}2518$; $0{,}8695$ với $M=1$; $10$; $100$.

**Bước 4: chỗ chứng minh hỏng.** Khi $x$ không bị chặn, đạo hàm $2(wx-y)x$ không bị chặn quanh $\hat w_S$, nên không có $G$ hữu hạn và Bước 3 của chứng minh Mệnh đề 06.11 không dùng được. Với $m$ bản sao bất kì, $\hat w_S=2/3$, còn với $M=m$, nghiệm trên mẫu lân cận dần về $0$ khi $m$ tăng, nên thay đổi của hàm lỗi không giảm theo $m$.

**Kết luận.** Với hàm lỗi bình phương, cận ổn định cần dữ liệu bị chặn; khi $x$ không bị chặn, không thuật toán nào học được bài toán này (UML §12.2.1, Ví dụ 12.9). Trường hợp dữ liệu bị chặn nhưng $W=\mathbb R^p$ là Bài tập 06.5.
:::

::: remark Nhận xét 06.12 (Hàm lỗi trơn và không âm) — đọc thêm
**Giả thiết.**

- **Mẫu và tập tham số.** $S\sim D^m$ theo (T1); $W=\mathbb R^p$.
- **Hàm lỗi.** $\ell(\cdot,z)$ lồi, không âm, $\beta$-trơn (Định nghĩa 05.6), $\ell(0,z)\le C_0$.
- **Chính quy hóa.** $\lambda\ge4\beta/m$.

**Bảo đảm.** Theo UML §13.3.2 (viết lại với $\lambda_{\mathrm{UML}}=\lambda/2$), khoảng cách tổng quát hóa kì vọng của ERM có chính quy hóa không quá $96\beta C_0/(\lambda m)$. Đây là cận một phía, qua đẳng thức sau chứng minh Định lý 06.10 và một dạng ổn định yếu hơn ổn định đều (Phụ lục E).

Hàm lỗi bình phương với $\lVert x\rVert\le C_x$, $\lvert y\rvert\le C_y$ không thỏa (L) trên $W=\mathbb R^p$, nhưng là $2C_x^2$-trơn với $\ell(0,z)=y^2\le C_y^2$. Khi $\lambda\ge8C_x^2/m$, cận là $192C_x^2C_y^2/(\lambda m)$. Dữ liệu bị chặn và tính trơn là giả thiết khác mà Nhận xét 02.11 hứa cho hàm lỗi bình phương.
:::

## 9. Đánh đổi khớp–ổn định

Theo Mệnh đề 06.5(a) với một điểm so sánh $u$ cố định, rủi ro vượt mức kì vọng của $\hat w_S$ so với $u$ là khoảng cách tổng quát hóa kì vọng cộng $\mathbb E[L_S(\hat w_S)-L_S(u)]$. Khi $\lambda$ tăng, số hạng thứ nhất giảm (§8), còn số hạng thứ hai có thể tăng (Ví dụ 06.4). Ta gọi đây là *đánh đổi khớp–ổn định* (fitting–stability trade-off).

::: corollary Hệ quả 06.13 (Bất đẳng thức oracle cho ERM có chính quy hóa) — phác thảo (chi tiết ở Phụ lục C)
**Giả thiết.** Bốn thành phần sau.

- **Mẫu.** $S\sim D^m$ theo (T1).
- **Hàm lỗi và tập tham số.** Như Mệnh đề 06.11, với $\ell(w,\cdot)$ đo được; thêm $L_D(w_0)<\infty$ cho một $w_0\in W$, nên theo (L), $L_D$ hữu hạn trên $W$.
- **Chính quy hóa.** $\lambda>0$, chọn trước khi thấy mẫu.
- **Điểm so sánh.** $u\in W$ cố định.

**Bảo đảm.** Theo kì vọng theo $S\sim D^m$:

- **(a) Một điểm so sánh.**
  $$
  \begin{aligned}
  &\mathbb E_SL_D(\hat w_S)-L_D(u)\\
  &\quad\le\frac{2G^2}{\lambda m}+\frac\lambda2\lVert u\rVert^2 .
  \end{aligned}
  $$
- **(b) Dạng cận dưới đúng.**
  $$
  \begin{aligned}
  &\mathbb E_SL_D(\hat w_S)\\
  &\le\inf_{u\in W}\big[L_D(u)+\tfrac\lambda2\lVert u\rVert^2\big]\\
  &\quad+\frac{2G^2}{\lambda m}.
  \end{aligned}
  $$
- **(c) Hệ số chọn theo cận.** Cho $B>0$ với $W_B=\{u\in W:\lVert u\rVert\le B\}$ khác rỗng, và $\lambda^*=2G/(B\sqrt m)$. Với $\lambda=\lambda^*$,
  $$
  \begin{aligned}
  &\mathbb E_SL_D(\hat w_S)-\inf_{u\in W_B}L_D(u)\\
  &\quad\le\frac{2GB}{\sqrt m},
  \end{aligned}
  $$
  và cỡ mẫu $m\ge4G^2B^2/\epsilon^2$ đủ để vế trái không quá $\epsilon$.

Đại lượng được chặn là rủi ro vượt mức kì vọng so với một điểm so sánh cố định, hay so với $W_B$. Hai số hạng là *số hạng ổn định* $2G^2/(\lambda m)$ và *số hạng khớp* $\tfrac\lambda2\lVert u\rVert^2$. Theo cách gọi của Bài 04, phần (b) là một *bất đẳng thức oracle* (oracle inequality): nó so đầu ra với mốc $\inf_u[L_D(u)+\tfrac\lambda2\lVert u\rVert^2]$, và mốc này chỉ tính được khi biết $D$. Hệ số $\lambda^*$ phụ thuộc $G$, $B$, $m$ và được chọn trước khi thấy mẫu; cận không phụ thuộc trực tiếp vào $p$.
:::

::: proof Chứng minh Hệ quả 06.13 (phác thảo)
**Lộ trình.** Dùng tính tối ưu của $\hat w_S$ cho $F_{S,\lambda}$, Mệnh đề 06.5(a), rồi Định lý 06.10 với Mệnh đề 06.11.

**Bước 1 (tính tối ưu; $u\in W$).** Vì $\hat w_S$ là điểm nhỏ nhất của $F_{S,\lambda}$ trên $W$ và $u\in W$,
$$
\begin{aligned}
L_S(\hat w_S)&\le F_{S,\lambda}(\hat w_S)\\
&\le F_{S,\lambda}(u)\\
&=L_S(u)+\tfrac\lambda2\lVert u\rVert^2 .
\end{aligned}
$$

**Bước 2 (phân tích; $u$ cố định).** Các kì vọng hữu hạn (Phụ lục C). Lấy kì vọng ở Mệnh đề 06.5(a); số hạng cuối có kì vọng $0$ vì $u$ không phụ thuộc $S$, nên
$$
\begin{aligned}
&\mathbb E_SL_D(\hat w_S)-L_D(u)\\
&=\mathbb E_S\big[L_D(\hat w_S)-L_S(\hat w_S)\big]\\
&\quad+\mathbb E_S\big[L_S(\hat w_S)-L_S(u)\big].
\end{aligned}
$$
Theo Bước 1, số hạng thứ hai không quá $\tfrac\lambda2\lVert u\rVert^2$.

**Bước 3 (ổn định; (T1) qua Định lý 06.10).** Mệnh đề 06.11(b) cho $\epsilon_{\mathrm{stab}}(m)=2G^2/(\lambda m)$. Định lý 06.10 chặn số hạng thứ nhất bởi $2G^2/(\lambda m)$; chỉ cần một phía của trị tuyệt đối. Ta được (a).

**Bước 4 (phần b).** Vế trái của (a) cộng $L_D(u)$ không phụ thuộc $u$; lấy cận dưới đúng theo $u\in W$.

**Bước 5 (phần c).** Với $u\in W_B$, vế phải của (a) không quá $a/\lambda+b\lambda$, với $a=2G^2/m$ và $b=B^2/2$. Theo bất đẳng thức trung bình cộng–trung bình nhân (như câu ôn nhanh 3), giá trị nhỏ nhất theo $\lambda$ đạt tại $\lambda^*=\sqrt{a/b}=2G/(B\sqrt m)$ và bằng $2\sqrt{ab}=2GB/\sqrt m$. Lấy cận dưới đúng theo $u\in W_B$ ở vế trái. Cuối cùng, $2GB/\sqrt m\le\epsilon$ khi và chỉ khi $m\ge4G^2B^2/\epsilon^2$.

$\square$ Chính quy hóa không làm rủi ro giảm đơn điệu theo $\lambda$; nó cân hai số hạng, và giá trị cân bằng phụ thuộc chuẩn của điểm so sánh.
:::

::: example Ví dụ 06.10 (Cỡ mẫu cho ERM có chính quy hóa và cho quan sát mới)
**Thiết lập.** Hồi quy ridge với $\lVert x\rVert\le1$, $\lvert y\rvert\le1$ và $W=\{w:\lVert w\rVert\le1\}$, nên $G=4$ (cận của Bài 05 với $B=C_x=C_y=1$) và $W_B=W$ với $B=1$.

**Bước 1: hồi quy ridge.** Theo Hệ quả 06.13(c), với $m=1600$,
$$
\begin{aligned}
\lambda^*&=\frac{2\cdot4}{1\cdot40}=0{,}2,\\
\frac{2GB}{\sqrt m}&=\frac{2\cdot4\cdot1}{40}=0{,}2 .
\end{aligned}
$$
Với $\epsilon=0{,}1$, điều kiện đủ là $m\ge4\cdot16\cdot1/0{,}01=6400$, và khi đó $\lambda^*=0{,}1$.

**Bước 2: SGD với quan sát mới cho cùng bài toán.** Với $w_1=0$ và $R=1$, Hệ quả 06.2(c) cho $T\ge16/0{,}01=1600$, tức $1599$ quan sát.

**Bước 3: hồi quy logistic.** Với $G=1$, $B=5$ và $\epsilon=0{,}05$, ERM có chính quy hóa cần
$$
m\ge\frac{4\cdot1\cdot25}{0{,}0025}=40\,000 .
$$
SGD với quan sát mới và $R=5$ cần
$$
T\ge\frac{25}{0{,}0025}=10^4 .
$$

**Kết luận.** Hai cận cùng bậc $GB/\sqrt m$; theo các cận, ERM có chính quy hóa cần khoảng bốn lần số quan sát, do hằng số $2$ trong $2GB/\sqrt m$. Đây là so sánh giữa hai cận, không phải giữa hai thuật toán, và ERM có chính quy hóa còn cần giải đúng $F_{S,\lambda}$ (nhận xét cuối mục).
:::

::: example Ví dụ 06.11 (Hồi quy logistic có chính quy hóa trên một triệu hồ sơ)
**Thiết lập.** Ứng dụng ở §3: $m=10^6$, $\lVert x\rVert\le1$, hàm lỗi logistic; cần một bảo đảm cho $L_D$ so với hàm tốt nhất trong quả cầu $\lVert u\rVert\le5$ (bán kính giả định).

**Bước 1: hằng số.** Gradient $\nabla_w\ell=-\tilde y\,x/(1+e^{\tilde y\langle w,x\rangle})$ có chuẩn không quá $\lVert x\rVert\le1$ trên toàn $\mathbb R^p$ (Ví dụ 05.9). Theo Mệnh đề 05.5(a), (L) đúng với $G=1$ và $W=\mathbb R^p$; nghiệm tồn tại theo Bổ đề 06.8.

**Bước 2: hệ số và cận.** Với $B=5$, Hệ quả 06.13(c) cho
$$
\begin{aligned}
\lambda^*&=\frac{2\cdot1}{5\cdot1000}=4\cdot10^{-4},\\
\frac{2GB}{\sqrt m}&=\frac{10}{1000}=0{,}01,
\end{aligned}
$$
tức $\mathbb E_SL_D(\hat w_S)-\min_{\lVert u\rVert\le5}L_D(u)\le0{,}01$.

**Bước 3: hai số hạng tại $\lambda^*$.** Mệnh đề 06.11 cho số hạng ổn định, và số hạng khớp tính với $\lVert u\rVert\le B=5$:
$$
\begin{aligned}
\epsilon_{\mathrm{stab}}&=\frac{2\cdot1}{4\cdot10^{-4}\cdot10^6}=0{,}005,\\
\tfrac{\lambda^*}2B^2&=2\cdot10^{-4}\cdot25=0{,}005 .
\end{aligned}
$$
Tổng là $0{,}01$, đúng cận ở Bước 2.

**Bước 4: một vòng SGD.** Theo Nhận xét 06.3 với $R=5$, cận là $5/\sqrt{10^6+1}\approx0{,}005$.

**Kết luận.** Câu hỏi thực hành của §3 có hai câu trả lời: một vòng SGD bảo đảm mức $0{,}005$, còn ERM có chính quy hóa với $\lambda^*$ bảo đảm mức $0{,}01$. Hàm lỗi logistic không bị chặn nhưng Lipschitz; đây là giả thiết khác mà Nhận xét 02.11 hứa cho hàm lỗi log, áp dụng cho mô hình logistic tuyến tính $h_w$. Kết luận không chuyển sang hàm lỗi log của một mô hình bất kì, vì hàm lỗi đó có thể không lồi hay không Lipschitz theo tham số.
:::

::: example Ví dụ 06.12 (Chính quy hóa quá mạnh)
**Thiết lập.** Phân bố $D$: $X=1$ và $Y=1$ chắc chắn; hàm lỗi bình phương, $W=\mathbb R$, $\lambda>0$.

**Bước 1: khoảng cách tổng quát hóa.** Mọi quan sát bằng $(1,1)$, nên $L_S(w)=L_D(w)=(w-1)^2$ trên mọi mẫu, và khoảng cách tổng quát hóa bằng $0$.

**Bước 2: rủi ro.** Đạo hàm của $(w-1)^2+\tfrac\lambda2w^2$ bằng $0$ tại $\hat w_S=1/(1+\lambda/2)$, nên
$$
L_D(\hat w_S)=\Big(\frac{\lambda}{2+\lambda}\Big)^2,
$$
bằng $0{,}0083$; $0{,}25$; $0{,}8264$ với $\lambda=0{,}2$; $2$; $20$.

**Kết luận.** Số hạng phạt kéo $\hat w_S=1/(1+\lambda/2)$ ra xa điểm tốt nhất $1$, nên $L_D(\hat w_S)$ tăng theo $\lambda$ dù khoảng cách tổng quát hóa bằng $0$.
:::

::: remark Nhận xét 06.14 (Bảo đảm theo kì vọng và bảo đảm với xác suất cao)
- **Loại cận.** Hệ quả 06.2, Định lý 06.10 và Hệ quả 06.13 chặn kì vọng theo mẫu của một đại lượng gắn với một thuật toán. Bài 02–04 cho cận với xác suất ít nhất $1-\delta$ theo $S$, đồng thời cho mọi giả thuyết của lớp.
- **Bất đẳng thức Markov.** Với $W$ là quả cầu bán kính $B$, $L_D(\hat w_S)-\inf_WL_D\ge0$, nên Bổ đề 02.2 và Hệ quả 06.13(c) cho
  $$
  \begin{aligned}
  &\Pr_S\big[L_D(\hat w_S)-\inf_WL_D\ge\epsilon\big]\\
  &\quad\le\frac{2GB}{\epsilon\sqrt m}.
  \end{aligned}
  $$
  Với $G=4$, $B=1$, $\epsilon=0{,}1$ và $\delta=0{,}05$, điều kiện đủ để xác suất này không quá $\delta$ là $m\ge4G^2B^2/(\epsilon\delta)^2=2\,560\,000$, so với $6400$ cho mức kì vọng: thừa số $1/\delta^2=400$.
- **Chia khối và xác thực.** Khi hàm lỗi nhận giá trị trong $[0,1]$, tức (T3) của Hệ quả 04.17, ta chia mẫu thành $k=\lceil\log_2(2/\delta)\rceil$ khối độc lập, mỗi khối đủ cho mức kì vọng $\epsilon/4$. Ta chọn đầu ra bằng một mẫu xác thực cỡ $8\ln(4k/\delta)/\epsilon^2$ (Bài tập 06.7). Khi đó, với xác suất ít nhất $1-\delta$ theo mẫu, đầu ra được chọn có rủi ro vượt mức không quá $\epsilon$; số khối tăng theo $\log_2(2/\delta)$, thay cho thừa số $1/\delta^2$ của bất đẳng thức Markov. Với hàm lỗi không bị chặn như hàm lỗi logistic, cách này cần thêm một cận cho hàm lỗi trên các ứng viên, ngoài phạm vi bài.
:::

::: remark Nhận xét 06.15 (Nghiệm gần đúng của bài toán có chính quy hóa) — đọc thêm
**Giả thiết.** Như Hệ quả 06.13, với đầu ra $\tilde w\in W$ thỏa $F_{S,\lambda}(\tilde w)-F_{S,\lambda}(\hat w_S)\le\epsilon_{\mathrm{opt}}$ trên mọi mẫu, tức mức (O2) của Bài 01 cho $F_{S,\lambda}$.

**Bảo đảm.** Bổ đề 06.8(c) cho $\lVert\tilde w-\hat w_S\rVert\le\sqrt{2\epsilon_{\mathrm{opt}}/\lambda}$, nên theo (L), $L_D(\tilde w)\le L_D(\hat w_S)+G\sqrt{2\epsilon_{\mathrm{opt}}/\lambda}$. Với $G=4$, $\lambda=0{,}2$ và $\epsilon_{\mathrm{opt}}=10^{-4}$, số hạng thêm là $4\sqrt{10^{-3}}\approx0{,}1265$; khi $\lambda$ nhỏ, cần giải $F_{S,\lambda}$ rất chính xác.
:::

## 10. Ý nghĩa, tác động và giới hạn

Một bộ giải tối ưu là một thuật toán học khi gradient ngẫu nhiên không chệch cho $L_D$, tức mỗi bước dùng một quan sát mới (Hệ quả 06.2), hoặc khi thuật toán chạy trên một mẫu cố định có khoảng cách tổng quát hóa kì vọng nhỏ. ERM có chính quy hóa với hàm lỗi lồi, Lipschitz là một thuật toán như vậy nhờ tính ổn định đều (Định lý 06.10, Mệnh đề 06.11). Trong câu hỏi mở đầu, rủi ro vượt mức kì vọng là $0{,}0006$ với quan sát mới (Ví dụ 06.2) và $0{,}2261$ khi dùng lại bốn quan sát, dù kì vọng của sai số tối ưu thực nghiệm chỉ là $0{,}0011$; khoảng cách tổng quát hóa kì vọng ở đó là $0{,}4750$ (Ví dụ 06.3).

Hai cách cho cận cùng bậc $GB/\sqrt m$; với hồi quy ridge trên quả cầu đơn vị, theo các cận, SGD cần $1599$ và ERM có chính quy hóa cần $6400$ quan sát cho mức $0{,}1$ (Ví dụ 06.10). Bài tập 06.8 cho một bài toán mà cận của ERM có chính quy hóa không phụ thuộc số chiều $p$, còn cỡ mẫu cho hội tụ đều tăng theo $p$.

Hệ số $\lambda^*=2G/(B\sqrt m)$ cân hai số hạng của Hệ quả 06.13. Không có chính quy hóa, cận ổn định không giảm theo $m$ (Ví dụ 06.7); chính quy hóa quá mạnh làm rủi ro tăng tới $0{,}8264$ khi $\lambda=20$ (Ví dụ 06.12). Khi $B$ chưa biết và hàm lỗi bị chặn, $\lambda$ được chọn bằng mẫu xác thực (Hệ quả 04.17).

Bốn giới hạn còn lại.

- **Theo kì vọng.** Bất đẳng thức Markov tốn thừa số $400$ về cỡ mẫu (Nhận xét 06.14); không cận nào chặn $\mathbb E\lvert L_D-L_S\rvert$ (Ví dụ 06.5).
- **Nghiệm chính xác.** Nghiệm gần đúng thêm $G\sqrt{2\epsilon_{\mathrm{opt}}/\lambda}$ vào cận (Nhận xét 06.15).
- **Dữ liệu bị chặn.** Với hàm lỗi bình phương, cận ổn định cần dữ liệu bị chặn (Ví dụ 06.9).
- **SGD nhiều vòng.** Khoảng cách tổng quát hóa kì vọng của SGD dùng lại mẫu chưa được chặn trong bài.

Các kết quả cần hàm lỗi lồi theo tham số; hàm lỗi của mạng nơ-ron theo trọng số nói chung không lồi, nên các cận không chuyển sang mạng nơ-ron mà không có lập luận mới.

## 11. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 06](material-viewer.html?doc=materials/lec-06/exercises.md). Sáu bài đầu là bài gốc, năm bài sau chọn từ UML.

1. **Bài tập 06.1** (Hàm mà gradient ngẫu nhiên không chệch trong hai chế độ lấy mẫu): mục tiêu 1.
2. **Bài tập 06.2** (Lập luận đổi vai cho khoảng cách tổng quát hóa kì vọng): mục tiêu 3.
3. **Bài tập 06.3** (Cận khoảng cách giữa hai nghiệm của ERM có chính quy hóa): mục tiêu 4.
4. **Bài tập 06.4** (Chọn hệ số chính quy hóa khi biết cận chuẩn của điểm so sánh): mục tiêu 5.
5. **Bài tập 06.5** (Hồi quy ridge khi dữ liệu không bị chặn hoặc tập tham số không bị chặn): mục tiêu 5.
6. **Bài tập 06.6** (Thay một quan sát và đo độ nhạy, thực nghiệm tùy chọn): mục tiêu 5.
7. **Bài tập 06.7** (Cận với xác suất cao và tăng độ tin cậy từ một cận kì vọng; UML Bài tập 13.1, phát biểu đã chỉnh hằng số): mục tiêu 5.
8. **Bài tập 06.8** (Học được mà không có hội tụ đều; UML Bài tập 13.2): mục tiêu 3, 4, 5.
9. **Bài tập 06.9** (Ổn định thay một theo trung bình và gần đúng ERM theo kì vọng đủ cho học; UML Bài tập 13.3): mục tiêu 2, 3.
10. **Bài tập 06.10** (Dạng bậc nhất của tính lồi mạnh; UML Bài tập 14.1): mục tiêu 4.
11. **Bài tập 06.11** (Tùy chọn: lồi mạnh theo chuẩn bất kì; UML Bài tập 13.4, ý 1–3): phần mở rộng của §6 và §8.

## 12. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Hồi quy ridge với $\lVert x\rVert\le1$, $\lvert y\rvert\le1$, $W=\{w\in\mathbb R^p:\lVert w\rVert\le1\}$ và $m=400$ quan sát độc lập cùng phân bố.

(a) Tính hằng số $G$ của hàm lỗi trên $W$, hệ số ổn định của ERM có chính quy hóa với $\lambda=0{,}4$, và cận cho khoảng cách tổng quát hóa kì vọng.

(b) Tính $\lambda^*$ và cận cho $\mathbb E_SL_D(\hat w_S)-\inf_WL_D$.

(c) Cận ở (a) có chặn $\mathbb E_S\lvert L_D(\hat w_S)-L_S(\hat w_S)\rvert$ không? Cận ở (b) cho biết gì về $\Pr_S\big[L_D(\hat w_S)-\inf_WL_D\ge0{,}8\big]$?

::: solution Lời giải câu hỏi cuối buổi
**(a)** Theo cận của Bài 05 (đoạn sau Định nghĩa 05.4) với $B=C_x=C_y=1$, $G=2(1+1)\cdot1=4$. Theo Mệnh đề 06.11,
$$
\begin{aligned}
\epsilon_{\mathrm{stab}}(400)&=\frac{2\cdot16}{0{,}4\cdot400}\\
&=\frac{32}{160}=0{,}2 .
\end{aligned}
$$
Theo Định lý 06.10, $\big\lvert\mathbb E_S[L_D(\hat w_S)-L_S(\hat w_S)]\big\rvert\le0{,}2$.

**(b)** Với $B=1$, Hệ quả 06.13(c) cho
$$
\begin{aligned}
\lambda^*&=\frac{2\cdot4}{1\cdot20}=0{,}4,\\
\frac{2GB}{\sqrt m}&=\frac{8}{20}=0{,}4 .
\end{aligned}
$$
Hệ số $\lambda$ của (a) chính là $\lambda^*$, và cận $0{,}4=0{,}2+\tfrac{0{,}4}2\cdot1$ gồm hai số hạng bằng nhau.

**(c)** Không: Định lý 06.10 chặn trị tuyệt đối của kì vọng, không chặn kì vọng của trị tuyệt đối (Ví dụ 06.5). Vì $\hat w_S\in W$, $L_D(\hat w_S)-\inf_WL_D\ge0$, nên theo Bổ đề 02.2,
$$
\begin{aligned}
&\Pr_S\big[L_D(\hat w_S)-\inf_WL_D\ge0{,}8\big]\\
&\quad\le\frac{0{,}4}{0{,}8}=0{,}5 .
\end{aligned}
$$
Đại lượng ở (a) là khoảng cách tổng quát hóa kì vọng; đại lượng ở (b) là rủi ro vượt mức kì vọng theo $S$.
:::

Mệnh đề 06.11 cần hàm lỗi lồi theo tham số, và hàm lỗi của mạng nơ-ron theo trọng số nói chung không lồi (§10). Một mạng nơ-ron lớn có thể khớp cả nhãn gán ngẫu nhiên; khi đó $L_S\approx0$ và khoảng cách tổng quát hóa xấp xỉ $L_D$, còn số tham số không phân biệt được nhãn thật với nhãn ngẫu nhiên. Câu hỏi cho Bài 07 là: đại lượng đo độ phức tạp nào của lớp mạng nơ-ron còn cho thông tin trong tình huống này? Với hàm lỗi lồi, trơn và Lipschitz, khoảng cách tổng quát hóa kì vọng của SGD nhiều vòng (§5) được chặn ở Bài 08 bằng tính ổn định của hai lần chạy ghép cặp.

## 13. Tài liệu đọc

- **Trước buổi học:** UML §14.5 (học bằng SGD; §14.5.1 cho thiết lập quan sát mới), §13.1 (ERM có chính quy hóa, hồi quy ridge).
- **Sau buổi học:** UML §13.2 (quy tắc ổn định không quá khớp), §13.3 (chính quy hóa Tikhonov như một cơ chế ổn định); các bài tập UML §13.7, §14.8 đã chọn ở §11.
- **Mở rộng:** UML §13.4 (đánh đổi khớp–ổn định, bất đẳng thức oracle), §13.3.2 (hàm lỗi trơn và không âm), §12.2.1 (Ví dụ 12.9: dữ liệu không bị chặn), §12.2.2 (bài toán lồi–Lipschitz–bị chặn, convex-Lipschitz-bounded problem).

**Quan hệ với giáo trình UML.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục. Các khác biệt chính:

- **Định nghĩa ổn định.** UML §13.2 dùng ổn định thay một theo trung bình (on-average-replace-one stability), một phía, cho thuật toán tất định, và chứng minh một đẳng thức. Học phần dùng ổn định đều, hai phía, cho thuật toán có nguồn ngẫu nhiên riêng, để nối sang Bài 08 (Phụ lục E).
- **Chuẩn hóa và hằng số.** UML dùng $\lambda\lVert w\rVert^2$, hằng số Lipschitz $\rho$ và lập luận một phía (§13.3); học phần dùng $\tfrac\lambda2\lVert w\rVert^2$, $G$ và lập luận đối xứng. Cỡ mẫu tương ứng là $4G^2B^2/\epsilon^2$ ở đây và $8\rho^2B^2/\epsilon^2$ ở UML §13.4; khác biệt này đến từ lập luận đối xứng, không từ chuẩn hóa.
- **Số quan sát của SGD.** UML §14.5.1 đếm $T$ quan sát; học phần đếm $T-1$ theo Thuật toán 05.11.

## Phụ lục

### A. Sự tồn tại nghiệm của bài toán có chính quy hóa

Phần (b) của Bổ đề 06.8 được chứng minh dưới đây. Cố định $W$ khác rỗng, đóng, lồi, một mẫu $s$ và $\lambda>0$; với mọi $z$, $\ell(\cdot,z):\mathbb R^p\to\mathbb R$ lồi. Viết $F=F_{s,\lambda}$.

::: proof Chứng minh Bổ đề 06.8(b)
**Lộ trình.** Chặn $F$ từ dưới bằng một hàm tiến ra vô cùng, thu hẹp bài toán về một tập compact, rồi dùng tính liên tục.

**Bước 1 (cận dưới afin của $L_s$).** Lấy $w_0\in W$. Hàm $L_s$ lồi và hữu hạn trên $\mathbb R^p$, nên dưới vi phân của nó tại $w_0$ khác rỗng (§4 của Bài 05); lấy $v_0\in\partial L_s(w_0)$. Theo bất đẳng thức dưới gradient và Cauchy–Schwarz, với mọi $w$,
$$
\begin{aligned}
L_s(w)&\ge L_s(w_0)+\langle v_0,w-w_0\rangle\\
&\ge L_s(w_0)\\
&\quad-\lVert v_0\rVert\,\lVert w-w_0\rVert .
\end{aligned}
$$

**Bước 2 ($F$ tiến ra vô cùng).** Cộng $\tfrac\lambda2\lVert w\rVert^2$ vào hai vế và dùng $\lVert w-w_0\rVert\le\lVert w\rVert+\lVert w_0\rVert$:
$$
\begin{aligned}
F(w)&\ge L_s(w_0)-\lVert v_0\rVert\,\lVert w_0\rVert\\
&\quad-\lVert v_0\rVert\,\lVert w\rVert+\tfrac\lambda2\lVert w\rVert^2 .
\end{aligned}
$$
Vế phải là một đa thức bậc hai theo $\lVert w\rVert$ với hệ số dẫn $\tfrac\lambda2>0$, nên $F(w)\to\infty$ khi $\lVert w\rVert\to\infty$; giả thiết $\lambda>0$ được dùng ở đây.

**Bước 3 (tập compact).** Đặt $K=\{w\in W:F(w)\le F(w_0)\}$. Tập $K$ chứa $w_0$. Hàm $F$ lồi và hữu hạn trên $\mathbb R^p$ nên liên tục; do đó $K$ là giao của tập đóng $W$ với một tập đóng, nên đóng; tính đóng của $W$ được dùng ở đây. Theo Bước 2, $K$ bị chặn. Vậy $K$ compact.

**Bước 4 (giá trị nhỏ nhất).** Hàm liên tục $F$ đạt giá trị nhỏ nhất trên $K$ tại một điểm $\hat w$. Mọi $w\in W\setminus K$ có $F(w)>F(w_0)\ge F(\hat w)$, nên $\hat w$ là điểm nhỏ nhất của $F$ trên $W$.

$\square$ Chứng minh không dùng $\ell\ge0$. Với $\lambda=0$, Bước 2 không còn đúng, và giá trị nhỏ nhất có thể không đạt, như hàm lỗi logistic với $W=\mathbb R^p$ trên một mẫu có $w$ thỏa $\tilde y_i\langle w,x_i\rangle>0$ cho mọi $i$ (tách được bởi một siêu phẳng qua gốc).
:::

Tính đo được của $s\mapsto\hat w_s$ không được chứng minh ở đây; nó được giả sử như điều kiện đo được chung của học phần.

### B. Chi tiết cho Mệnh đề 06.11

Kí hiệu như chứng minh Mệnh đề 06.11: $\hat w=\hat w_s$, $\hat w'=\hat w_{s^{(i)}}$.

::: proof Chi tiết của chứng minh Mệnh đề 06.11
**Lộ trình.** Viết đầy đủ phép triệt tiêu ở Bước 2, so với lập luận chỉ dùng một bất đẳng thức tăng trưởng bậc hai, và ghi chỗ cần (L).

**Bước 1 (phép triệt tiêu).** Hai mẫu $s$ và $s^{(i)}$ chung $m-1$ quan sát và cùng số hạng chính quy hóa, nên với mọi $w$,
$$
\begin{aligned}
&F_{s,\lambda}(w)-F_{s^{(i)},\lambda}(w)\\
&\quad=\tfrac1m\big[\ell(w,z_i)-\ell(w,z')\big].
\end{aligned}
$$
Tổng hai vế trái của Bước 1 trong chứng minh Mệnh đề 06.11 là
$$
\begin{aligned}
&\big[F_{s,\lambda}-F_{s^{(i)},\lambda}\big](\hat w')\\
&\quad-\big[F_{s,\lambda}-F_{s^{(i)},\lambda}\big](\hat w)\\
&=\tfrac1m\big[\ell(\hat w',z_i)-\ell(\hat w',z')\big]\\
&\quad-\tfrac1m\big[\ell(\hat w,z_i)-\ell(\hat w,z')\big],
\end{aligned}
$$
và sắp xếp lại các số hạng cho vế phải của Bước 2.

**Bước 2 (lập luận một phía).** Chỉ dùng tăng trưởng bậc hai của $F_{s,\lambda}$ tại $\hat w$ và tính tối ưu của $\hat w'$ cho $F_{s^{(i)},\lambda}$, tức $F_{s^{(i)},\lambda}(\hat w')\le F_{s^{(i)},\lambda}(\hat w)$:
$$
\begin{aligned}
&\tfrac\lambda2\lVert \hat w-\hat w'\rVert^2\\
&\le F_{s,\lambda}(\hat w')-F_{s,\lambda}(\hat w)\\
&=F_{s^{(i)},\lambda}(\hat w')-F_{s^{(i)},\lambda}(\hat w)\\
&\quad+\tfrac1m\big[\ell(\hat w',z_i)-\ell(\hat w,z_i)\big]\\
&\quad+\tfrac1m\big[\ell(\hat w,z')-\ell(\hat w',z')\big]\\
&\le0+\frac{2G\lVert \hat w-\hat w'\rVert}{m}.
\end{aligned}
$$
Do đó $\lVert \hat w-\hat w'\rVert\le4G/(\lambda m)$, gấp đôi cận đối xứng. Thừa số $2$ mất đi vì chỉ một trong hai bất đẳng thức tăng trưởng bậc hai được dùng.

**Bước 3 (chỗ cần (L)).** (L) chỉ được dùng tại $\hat w$, $\hat w'\in W$ với các quan sát $z_i$, $z'$ và quan sát kiểm tra $z$. Khi $W=\mathbb R^p$, cần $\ell(\cdot,z)$ Lipschitz trên $\mathbb R^p$, như hàm lỗi logistic hay bản lề; với hàm lỗi bình phương, cần thêm một cận cho chuẩn của nghiệm (Bài tập 06.5).

$\square$ Lập luận đối xứng cho hằng số $2G/(\lambda m)$, lập luận một phía cho $4G/(\lambda m)$; cả hai giảm như $1/(\lambda m)$.
:::

### C. Chi tiết cho Hệ quả 06.13

::: proof Chi tiết của chứng minh Hệ quả 06.13
**Lộ trình.** Kiểm các kì vọng hữu hạn để Mệnh đề 06.5 và Định lý 06.10 áp dụng được, rồi viết phép thay $\lambda^*$.

**Bước 1 (rủi ro thực nghiệm khả tích).** Theo Bước 1 của chứng minh Hệ quả 06.13, $0\le L_S(\hat w_S)\le L_S(u)+\tfrac\lambda2\lVert u\rVert^2$, và $\mathbb EL_S(u)=L_D(u)<\infty$; do đó $\mathbb EL_S(\hat w_S)<\infty$.

**Bước 2 (chuẩn của nghiệm).** Vì $L_S\ge0$ trên $W$, cùng chuỗi bất đẳng thức cho $\tfrac\lambda2\lVert\hat w_S\rVert^2\le L_S(u)+\tfrac\lambda2\lVert u\rVert^2$. Lấy kì vọng,
$$
\begin{aligned}
&\mathbb E\lVert\hat w_S\rVert^2\\
&\quad\le\lVert u\rVert^2+\frac{2L_D(u)}{\lambda}<\infty .
\end{aligned}
$$

**Bước 3 (rủi ro kì vọng khả tích).** Với mỗi $z$, (L) cho $\ell(\hat w_S,z)\le\ell(u,z)+G\lVert\hat w_S-u\rVert$; lấy kì vọng theo $Z$ với $S$ cố định, $L_D(\hat w_S)\le L_D(u)+G\lVert\hat w_S-u\rVert$. Theo Bước 2 và Cauchy–Schwarz, $\mathbb E\lVert\hat w_S-u\rVert\le\lVert u\rVert+(\mathbb E\lVert\hat w_S\rVert^2)^{1/2}<\infty$, nên $\mathbb EL_D(\hat w_S)<\infty$. Giả thiết khả tích của Định lý 06.10 và của Mệnh đề 06.5 được thỏa.

**Bước 4 (phép thay $\lambda^*$).** Với $\lambda^*=2G/(B\sqrt m)$,
$$
\begin{aligned}
\frac{2G^2}{\lambda^*m}&=\frac{2G^2B\sqrt m}{2Gm}=\frac{GB}{\sqrt m},\\
\frac{\lambda^*}2B^2&=\frac{GB^2}{B\sqrt m}=\frac{GB}{\sqrt m}.
\end{aligned}
$$
Hai số hạng bằng nhau, và tổng của chúng là $2GB/\sqrt m$.

$\square$ Các bất đẳng thức của Hệ quả 06.13 so sánh các số hữu hạn; tại $\lambda^*$, số hạng ổn định bằng số hạng khớp.
:::

### D. Hai chương trình của câu hỏi mở đầu

Đặt $q=1-2\eta$. Trong cả hai chương trình, phép chiếu không tác động (Ví dụ 06.2, Bước 3), nên $w_{t+1}=qw_t+2\eta y_t$ với $w_1=0$. Quy nạp theo $k$ cho
$$
w_k=2\eta\sum_{t=1}^{k-1}q^{\,k-1-t}y_t .
$$
Lấy trung bình $w_1,\ldots,w_T$ và đổi thứ tự lấy tổng, hệ số của $y_t$ là $\tfrac{2\eta}T\sum_{k=t+1}^{T}q^{\,k-1-t}$. Tổng cấp số nhân với $1-q=2\eta$ cho
$$
\bar w_T=\sum_{t=1}^{T-1}c_ty_t,\qquad c_t=\frac{1-q^{\,T-t}}{T}.
$$
Cộng các hệ số, lại theo tổng cấp số nhân,
$$
\sum_{t=1}^{T-1}c_t=1-\frac{1-q^{T}}{2\eta T}.
$$
Với $T=1600$ và $\eta=0{,}00625$, ta có $q=0{,}9875$, $\sum_tc_t=0{,}95$ (khớp $\bar w_{1600}\approx0{,}95$ khi mọi nhãn bằng $1$, như câu hỏi cuối buổi Bài 05) và, tính trực tiếp, $\sum_tc_t^2\approx0{,}000578$.

Hai công thức mô-men là $\mathbb E\bar w_T^2=\sum_tc_t^2$ với quan sát mới (Ví dụ 06.2) và
$$
\begin{aligned}
\mathbb E\bar w_T^2&=\tfrac1m\Big(\sum_tc_t\Big)^2\\
&\quad+\Big(1-\tfrac1m\Big)\sum_tc_t^2
\end{aligned}
$$
khi rút từ một mẫu $m$ quan sát (Ví dụ 06.3). Khoảng cách tổng quát hóa kì vọng của chương trình thứ hai bằng $\tfrac2m\sum_tc_t$.

Chạy lâu hơn với $\eta=1/(4\sqrt T)$, ta có $2\eta T=\sqrt T/2\to\infty$ và $q^T\to0$, nên $\sum_tc_t\to1$; vì $0\le c_t\le1/T$, $\sum_tc_t^2\le1/T\to0$. Do đó $\mathbb EL_D(\bar w_T)\to1+\tfrac1m$, bằng $1{,}25$ với $m=4$. Với $T=25\,600$: $\sum_tc_t=0{,}9875$, $\sum_tc_t^2\approx3{,}83\cdot10^{-5}$, $\mathbb EL_D(\bar w_T)\approx1{,}2438$ với $m=4$ và $1{,}9752$ với $m=1$; khoảng cách tổng quát hóa kì vọng với $m=4$ tăng từ $0{,}4750$ lên $0{,}4938$.

### E. Hai quy ước về tính ổn định

Định nghĩa 06.9 là quy ước của học phần. UML §13.2 dùng một quy ước khác; phụ lục này so hai quy ước.

**Ổn định thay một theo trung bình.** Cho thuật toán tất định $A$ và một hàm không tăng $\epsilon(m)$. Với $S\sim D^m$, $Z'\sim D$ độc lập và $S^{(i)}$ như chứng minh Định lý 06.10, $A$ là *ổn định thay một theo trung bình* (on-average-replace-one stable) với tốc độ $\epsilon(m)$ nếu với mọi phân bố $D$,
$$
\begin{aligned}
&\frac1m\sum_{i=1}^m\mathbb E\big[\ell(A(S^{(i)}),Z_i)\\
&\qquad-\ell(A(S),Z_i)\big]\le\epsilon(m).
\end{aligned}
$$

**Đẳng thức.** Khi $\mathbb EL_D(A(S))<\infty$, các đẳng thức ở Bước 1–3 của chứng minh Định lý 06.10 cho thấy khoảng cách tổng quát hóa kì vọng bằng đúng vế trái trên. Do đó điều kiện trên tương đương với cận một phía $\mathbb E[L_D(A(S))-L_S(A(S))]\le\epsilon(m)$ cho mọi $D$. UML trình bày kết quả này ở §13.2, mục có tên "quy tắc ổn định không quá khớp" (Stable Rules Do Not Overfit).

**So với ổn định đều.** Ổn định đều với hệ số $\epsilon_{\mathrm{stab}}(m)$ kéo theo điều kiện trên với $\epsilon(m)=\epsilon_{\mathrm{stab}}(m)$, cho cả hai phía và mọi $D$: mỗi hiệu trong tổng có trị tuyệt đối không quá $\epsilon_{\mathrm{stab}}(m)$. Điều ngược lại sai. Lấy lớp giả thuyết gồm các hàm chỉ thị $h_C=\mathbb 1_C$ của các tập hữu hạn $C\subset\mathcal Z$, hàm lỗi $\ell(h,z)=h(z)$, và thuật toán $A(s)=h_{\{z_1,\ldots,z_m\}}$, nên $\ell(A(s),z)=\mathbb 1[z\in\{z_1,\ldots,z_m\}]$. Vì $\ell(A(S),Z_i)=1$, mỗi hiệu trong vế trái không dương, nên điều kiện một phía đúng với $\epsilon(m)=0$ dưới mọi $D$. Nhưng với một mẫu có $z_i$ xuất hiện đúng một lần và $z'\ne z_i$, hàm lỗi tại quan sát kiểm tra $z=z_i$ đổi từ $1$ sang $0$, nên hệ số ổn định đều nhỏ nhất bằng $1$.

**Lý do chọn ổn định đều.** Ổn định đều lấy cận trên theo mọi mẫu, nên không phụ thuộc $D$; nó có kì vọng theo $\xi$ bên trong, nên áp dụng cho thuật toán có nguồn ngẫu nhiên riêng. Dạng $\mathbb E_\xi\lvert\ell(A(s;\xi),z)-\ell(A(s^{(i)};\xi),z)\rvert$, với hai lần chạy dùng chung $\xi$, là dạng mà Bài 08 chặn cho SGD với hàm lỗi lồi, trơn và Lipschitz.

**Hằng số.** UML dùng số hạng chính quy hóa $\lambda_{\mathrm{UML}}\lVert w\rVert^2=\tfrac\lambda2\lVert w\rVert^2$ và lập luận một phía, cho tốc độ $2\rho^2/(\lambda_{\mathrm{UML}}m)=4\rho^2/(\lambda m)$ với hằng số Lipschitz $\rho$. Lập luận đối xứng của Mệnh đề 06.11 cho $2G^2/(\lambda m)$; lập luận một phía ở Phụ lục B cho cùng hằng số $4$ như UML.
