# Bài 08 — Tính ổn định của SGD và tổng quát hóa trong học sâu

Định lý 06.10 chặn khoảng cách tổng quát hóa kì vọng (expected generalization gap) của một thuật toán ổn định đều (uniform stability). Mệnh đề 06.11 chứng minh rằng tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM) có chính quy hóa ổn định đều với hệ số $2G^2/(\lambda m)$. Hạ gradient ngẫu nhiên (stochastic gradient descent, SGD) chạy nhiều vòng trên một mẫu cố định chưa có cận như vậy (§10 của Bài 06). Bài 07 chặn khoảng cách tổng quát hóa đồng thời cho mọi hàm của một lớp chọn trước mẫu, nên không phân biệt hai hàm cùng lớp mà phép huấn luyện chọn khác nhau. Với hàm lỗi lồi, trơn và Lipschitz, chúng ta cần một bảo đảm cho chính hàm mà SGD trả về, qua số bước và độ dài bước của quỹ đạo.

Câu hỏi trung tâm của bài là thuật toán huấn luyện ảnh hưởng tới khoảng cách tổng quát hóa như thế nào. Các công cụ là hai lần chạy ghép cặp (coupled runs) của SGD trên hai mẫu lân cận, ánh xạ không giãn (nonexpansive map) và tính đồng bức (co-coercivity) của gradient; chúng cho tính ổn định đều của SGD. Chúng ta chứng minh đầy đủ kết quả cho hàm lỗi lồi và trơn, rồi xét bước nào của chứng minh không còn đúng khi bỏ tính lồi hoặc tính trơn, như với mạng nơ-ron ReLU (rectified linear unit).

## Câu hỏi mở đầu

Một mô hình hồi quy logistic (logistic regression) với $p=100$ đặc trưng được huấn luyện trên $m=200$ quan sát. Các đặc trưng thỏa $\lVert x\rVert\le1$, và nhãn của khoảng $10\%$ quan sát bị lật ngẫu nhiên. Thuật toán là SGD bắt đầu từ véc-tơ $0$. Ở mỗi bước, một quan sát của mẫu được rút đều, có hoàn lại, và véc-tơ tham số đi một bước với độ dài bước (step size, còn gọi là tốc độ học) $0{,}5$ ngược hướng gradient của hàm lỗi logistic (logistic loss) trên quan sát đó.

Mỗi lần chạy được đo ở năm thời điểm, từ nửa vòng đến $100$ vòng qua dữ liệu (epoch). Tại mỗi thời điểm, ta đo trung bình hàm lỗi logistic trên mẫu huấn luyện và trên $5000$ quan sát kiểm tra rút độc lập. Bảng ghi trung bình của $20$ lần chạy với $20$ hạt giống ngẫu nhiên (random seed). Cột "Khoảng cách" là trung bình của hiệu giữa lỗi kiểm tra và lỗi huấn luyện. Cận mà §7 chứng minh cho khoảng cách tổng quát hóa kì vọng của thuật toán này bằng đúng số vòng ở cột đầu.

| Số vòng | Huấn luyện | Kiểm tra | Khoảng cách |
|---|---|---|---|
| $0{,}5$ | $0{,}618$ | $0{,}662$ | $0{,}045$ |
| $1$ | $0{,}561$ | $0{,}640$ | $0{,}079$ |
| $5$ | $0{,}376$ | $0{,}589$ | $0{,}213$ |
| $20$ | $0{,}243$ | $0{,}662$ | $0{,}419$ |
| $100$ | $0{,}134$ | $1{,}053$ | $0{,}919$ |

**Câu hỏi.** Mô hình, mẫu và thuật toán giữ nguyên; chỉ có số bước thay đổi. Lỗi huấn luyện giảm, còn khoảng cách giữa lỗi kiểm tra và lỗi huấn luyện tăng. Đại lượng nào của quá trình huấn luyện quyết định khoảng cách này?

Số tham số ($100$) và lớp hàm như nhau ở mọi dòng của bảng, nên tỉ lệ giữa số tham số và cỡ mẫu $200$ không giải thích sự thay đổi theo số bước. Đại lượng thay đổi là quỹ đạo của thuật toán; sau $t$ bước, tổng các độ dài bước là $0{,}5t$. Với hàm lỗi lồi, trơn và có gradient bị chặn, khoảng cách tổng quát hóa kì vọng của SGD không vượt một hằng số nhân tổng các độ dài bước chia cho cỡ mẫu (§4–§7).

Các khoảng cách đo được đều nằm dưới cận (so sánh chi tiết ở §7). Bảng ghi kết quả thí nghiệm; giao thức ở Phụ lục F.

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Mô tả hai lần chạy ghép cặp của SGD trên hai mẫu lân cận và tính khoảng cách giữa chúng trên một ví dụ nhỏ.
2. Chứng minh rằng một bước gradient của hàm lồi, trơn không làm tăng khoảng cách giữa hai điểm khi độ dài bước không vượt hai lần nghịch đảo hằng số trơn, và chỉ ra bước chứng minh dùng tính lồi.
3. Chứng minh bất đẳng thức truy hồi cho khoảng cách giữa hai lần chạy, suy ra cận ổn định của SGD và cận cho khoảng cách tổng quát hóa kì vọng, rồi tính các cận đó bằng số.
4. Ghép cận ổn định với cận tối ưu để chọn số bước và độ dài bước, và nêu những điều cận ghép này không bảo đảm về lỗi kiểm tra.
5. Kiểm tra giả thiết của định lý cho một thiết lập huấn luyện cụ thể (hàm lỗi không lồi, độ dài bước lớn, mạng ReLU), và phân biệt kết quả chứng minh được, lý thuyết không lồi bổ sung và giả thuyết thực nghiệm.

## Kiến thức tiên quyết

- **Từ Bài 01.** (T1), (T2); tính không chệch của rủi ro thực nghiệm với giả thuyết cố định (Mệnh đề 01.7); khoảng cách tổng quát hóa (Định nghĩa 01.10); rủi ro vượt mức (Định nghĩa 01.24).
- **Từ Bài 04.** Sai số tối ưu thực nghiệm $\operatorname{opt}_S$ (Định nghĩa 04.2); mẫu xác thực (§8 của Bài 04).
- **Từ Bài 05.** Hàm Lipschitz (Định nghĩa 05.4); hằng số Lipschitz và chuẩn của dưới gradient (Mệnh đề 05.5); hàm trơn và hàm lồi mạnh (Định nghĩa 05.6); phép chiếu Euclid lên tập lồi đóng (Định nghĩa 05.7) và tính không giãn của nó (đoạn sau Bổ đề 05.8); oracle gradient ngẫu nhiên và lịch sử (Định nghĩa 05.10); hạ gradient ngẫu nhiên có chiếu (Thuật toán 05.11); giả thiết (C) và cận kì vọng cho hạ gradient ngẫu nhiên có chiếu (Định lý 05.14); thuật toán học có nguồn ngẫu nhiên riêng (Định nghĩa 05.18); hạ gradient ngẫu nhiên trên rủi ro thực nghiệm (Hệ quả 05.19); ứng dụng hồi quy logistic (Ví dụ 05.9); điểm lặp cuối với độ dài bước hằng (Ví dụ 05.12); hằng số của hàm lỗi logistic (Bài tập 05.8).
- **Từ Bài 06.** Hạ gradient ngẫu nhiên với quan sát mới (Hệ quả 06.2); một vòng qua mẫu theo thứ tự (Nhận xét 06.3); chương trình chạy nhiều vòng (Ví dụ 06.3); khoảng cách tổng quát hóa kì vọng (Định nghĩa 06.4); phân tích rủi ro của đầu ra tính trên một mẫu cố định (Mệnh đề 06.5); ERM có chính quy hóa (Định nghĩa 06.6); mẫu lân cận và tính ổn định đều (Định nghĩa 06.9); tính ổn định chặn khoảng cách tổng quát hóa kì vọng (Định lý 06.10); tính ổn định của ERM có chính quy hóa (Mệnh đề 06.11) và giả thiết (L) ngay trước nó.
- **Từ Bài 07.** Mạng nơ-ron lan truyền tới (Định nghĩa 07.1); lớp kiến trúc với đặc trưng ngẫu nhiên trong thí nghiệm của Bài 07 (Ví dụ 07.3); hàm mục tiêu không lồi của mạng ReLU (Bài tập 07.5(c)); cận theo lề cho phân lớp tuyến tính bị chặn theo chuẩn (Hệ quả 07.16); nghiệm nội suy chuẩn nhỏ nhất là giới hạn của hạ gradient khởi tạo tại $0$ (Phụ lục D của Bài 07).
- **Giải tích.** Bất đẳng thức tam giác, Cauchy–Schwarz, Jensen, trung bình cộng–trung bình nhân; định lý giá trị trung bình; $1+x\le e^x$; $\sum_{k=t+1}^T1/k\le\ln(T/t)$.

**Câu hỏi ôn nhanh.**

1. Cho $g(w)=\ln(1+e^{-w})$ và $f(w)=\tfrac12w^2$ trên $\mathbb R$. Hàm nào là $1$-Lipschitz trên $\mathbb R$? Tìm một hằng số trơn cho mỗi hàm.
2. Rút $T=6$ chỉ số đều trên $\{1,2,3,4\}$, có hoàn lại. Tính kì vọng của số lần chỉ số $4$ được rút và xác suất chỉ số $4$ được rút ít nhất một lần.

::: solution Lời giải câu hỏi ôn nhanh
1. Đạo hàm của $g$ là $g'(w)=-1/(1+e^w)$, nằm trong $(-1,0)$. Đạo hàm bậc hai là
$$
g''(w)=\frac{e^w}{(1+e^w)^2}\le\frac14,
$$
với dấu bằng tại $w=0$. Vì $g''>0$, $g$ lồi; theo Mệnh đề 05.5(a) và $\lvert g'\rvert<1$, $g$ là $1$-Lipschitz trên $\mathbb R$. Theo định lý giá trị trung bình, $g'$ là $\tfrac14$-Lipschitz, tức $g$ là $\tfrac14$-trơn. Với $f$, đạo hàm $f'(w)=w$ không bị chặn, nên $f$ không Lipschitz trên $\mathbb R$; nhưng $f'$ là $1$-Lipschitz, nên $f$ là $1$-trơn.
2. Số lần rút chỉ số $4$ là $\sum_{t=1}^6\mathbb 1[i_t=4]$. Theo tính tuyến tính của kì vọng, kì vọng của nó là $6\cdot\tfrac14=1{,}5$; bước này không cần các lần rút độc lập. Xác suất không lần nào rút chỉ số $4$ là $(3/4)^6$, nên xác suất cần tìm là
$$
\begin{aligned}
1-\Big(\frac34\Big)^6&=\frac{3367}{4096}\\
&\approx0{,}8220 .
\end{aligned}
$$
:::

## 1. Thiết lập bài toán

Bài toán có bảy thành phần. Khác Bài 07, bảo đảm là cho một thuật toán cụ thể; khác Bài 06, thuật toán là SGD chạy nhiều vòng trên một mẫu cố định.

1. **Dữ liệu.** Quan sát $z\in\mathcal Z$ rút từ một phân bố $D$ chưa biết. Với mô hình tuyến tính, $z=(x,y)$ và khi cần, $\lVert x\rVert\le C_x$ trên toàn $\mathcal X$; trong các ví dụ một chiều, $\mathcal Z=\mathbb R$.
2. **Cơ chế lấy mẫu.** Mẫu huấn luyện $S=(Z_1,\ldots,Z_m)\sim D^m$ theo dạng đầy đủ của (T1); mẫu kiểm tra (test sample) độc lập chỉ dùng trong thí nghiệm.
3. **Lớp và hàm lỗi.** Lớp hàm điểm số $\{h_w:w\in W\}$ của Bài 05, với $W\subset\mathbb R^p$ khác rỗng, đóng, lồi, có thể là $\mathbb R^p$; hàm lỗi $\ell(w,z)\ge0$ khả vi theo $w$. Tính lồi và tính trơn được nêu ở §2 và bỏ ở §9.
4. **Thuật toán.** SGD trên mẫu $S$: chỉ số rút đều có hoàn lại, độ dài bước $\eta_t$ tất định thay đổi theo bước, $T$ bước, có thể nhiều vòng qua dữ liệu (§4). Đầu ra là điểm lặp cuối, hoặc điểm lặp trung bình ở §7–§8.
5. **Mục tiêu.** Khoảng cách tổng quát hóa kì vọng của đầu ra (Định nghĩa 06.4), rồi rủi ro vượt mức kì vọng so với $W$ (§8).
6. **Đối tượng so sánh.** $\inf_WL_D$, chỉ dùng ở §8; cận khoảng cách tổng quát hóa không cần đối tượng so sánh.
7. **Tài nguyên.** Cỡ mẫu $m$, số bước $T$ và các độ dài bước $\eta_1,\ldots,\eta_T$; chúng đi vào cận qua $\tfrac1m\sum_t\eta_t$.

Các đại lượng của bài chia theo nguồn ngẫu nhiên như bảng dưới.

| Loại | Đại lượng |
|---|---|
| Cố định | $D$, $W$, $\ell$, hằng số trơn $\beta$ và cận gradient $G$ (§2), $m$, $T$, $\eta_1,\ldots,\eta_T$, $w_1$ |
| Ngẫu nhiên theo dữ liệu | $S$, $L_S(\cdot)$ |
| Ngẫu nhiên theo nguồn riêng của thuật toán | dãy chỉ số $\xi=(i_1,\ldots,i_T)$ |
| Ngẫu nhiên theo cả hai | điểm lặp $w_t$, $w_{T+1}$, $\bar w_T$; $L_D$ và $L_S$ tại các điểm đó |
| Chỉ trong định nghĩa và chứng minh | mẫu lân cận $s^{(i)}$, quan sát thay thế $z'$, quan sát kiểm tra $z$, điểm lặp của lần chạy thứ hai (§4) |

Trong Định nghĩa 06.9, ở §4–§6 và trong phần (a)–(b) của định lý ở §7, mẫu $s$, chỉ số $i$, quan sát thay thế $z'$ và quan sát kiểm tra $z$ là các điểm bất kì, không ngẫu nhiên; chỉ $\xi$ là ngẫu nhiên.

## 2. Kí hiệu và giả thiết

Bảng dưới gom các kí hiệu dùng từ §3; kí hiệu khác được đặt tên tại chỗ dùng lần đầu.

| Kí hiệu | Ý nghĩa |
|---|---|
| $w\in W$, $h_w$, $\ell(w,z)$ | véc-tơ tham số, hàm điểm số, hàm lỗi (Bài 05) |
| $L_S(w)$, $L_D(w)$ | rủi ro thực nghiệm, rủi ro kì vọng theo tham số (Bài 05) |
| $\eta_t$, $T$, $i_t$ | độ dài bước, số bước, chỉ số rút ở bước $t$ |
| $w_t$, $w_{T+1}$, $\bar w_T$ | điểm lặp, điểm lặp cuối, điểm lặp trung bình |
| $G$, $\beta$, $R$ | cận gradient, hằng số trơn, cận $\lVert w_1-u\rVert$ (Bài 05) |
| $s^{(i)}$, $z'$, $\epsilon_{\mathrm{stab}}(m)$ | mẫu lân cận, quan sát thay thế, hệ số ổn định (Bài 06) |

Giả thiết thống kê là dạng đầy đủ của (T1), dùng ở §7–§8 qua Định lý 06.10, và (T2) ($\ell\ge0$, đo được) cùng điều kiện $L_D(w_1)<\infty$. Các kết quả chính không giả sử hàm lỗi bị chặn. Hai giả thiết tối ưu (S), (G) và một điều kiện độ dài bước được nêu dưới đây để đánh dấu chỗ dùng trong chứng minh.

- **(S)** Với mọi $z\in\mathcal Z$, hàm $\ell(\cdot,z):\mathbb R^p\to\mathbb R$ lồi và $\beta$-trơn (Định nghĩa 05.6) trên toàn $\mathbb R^p$.
- **(G)** Với mọi $z\in\mathcal Z$ và mọi $w\in W$, $\lVert\nabla\ell(w,z)\rVert\le G$.
- **Độ dài bước.** Các $\eta_t$ tất định và $0<\eta_t\le2/\beta$.

Lượng từ "với mọi $z\in\mathcal Z$" chạy trên mọi quan sát có thể, không chỉ trên các quan sát của mẫu. Vì $W$ lồi, (G) kéo theo (L) của Bài 06 theo định lý giá trị trung bình dọc đoạn thẳng trong $W$ (§7), không cần tính lồi của hàm lỗi. (G) cũng kéo theo (G2), cận mô-men bậc hai của oracle (Định nghĩa 05.10), cho oracle rút đều một quan sát (Bước 1 của chứng minh Hệ quả 05.19); (G) là một cận tất định, mạnh hơn (G2). Giả thiết (S) được đặt trên toàn $\mathbb R^p$ vì chứng minh ở Phụ lục A dùng những điểm có thể nằm ngoài $W$.

Hàm lỗi logistic thỏa (S) với $\beta=C_x^2/4$ và (G) với $G=C_x$ trên toàn $\mathbb R^p$ (Bài tập 05.8). Hàm lỗi bình phương thỏa (S) với $\beta=2C_x^2$, nhưng (G) chỉ đúng trên $W$ bị chặn: với $W$ là quả cầu bán kính $B$ và $\lvert y\rvert\le C_y$, $G=2(BC_x+C_y)C_x$ (đoạn sau Định nghĩa 05.4). Hàm lỗi bản lề và hàm lỗi của mạng ReLU theo trọng số không thỏa (S) (§9).

Kí hiệu $\Delta_t$ của bài là khoảng cách giữa hai lần chạy (§4), khác đại lượng $\Delta_t=\lVert w_t-u\rVert^2$ trong chứng minh Định lý 05.14.

## 3. Ví dụ xuyên suốt

::: example Ví dụ 08.1 (Hàm lỗi Huber trên bốn quan sát)
**Thiết lập.** Cho $\mathcal Z=\mathbb R$: mỗi quan sát là một số thực $z$, và giả thuyết là một số $w\in W=\mathbb R$ ($p=1$). Hàm lỗi Huber (Huber loss) với ngưỡng $1$ cho bởi hai công thức:

- $\ell_{\mathrm H}(w,z)=\tfrac12(w-z)^2$ khi $\lvert w-z\rvert\le1$;
- $\ell_{\mathrm H}(w,z)=\lvert w-z\rvert-\tfrac12$ khi $\lvert w-z\rvert>1$.

Mẫu là $s=(0,1,2,3)$, $m=4$. Đại lượng ngẫu nhiên duy nhất là dãy chỉ số.

**Bước 1: đạo hàm.** Đạo hàm $\partial_w\ell_{\mathrm H}(w,z)$ là $w-z$ cắt vào đoạn $[-1,1]$, tức $\max\{-1,\min\{1,w-z\}\}$.

**Bước 2: tính lồi, $\beta$ và $G$.** Đạo hàm không giảm theo $w$, nên $\ell_{\mathrm H}(\cdot,z)$ lồi. Phép cắt vào $[-1,1]$ là $1$-Lipschitz, nên đạo hàm là $1$-Lipschitz theo $w$, tức $\ell_{\mathrm H}(\cdot,z)$ là $1$-trơn. Trị tuyệt đối của đạo hàm không quá $1$, nên (G) đúng với $G=1$ trên toàn $\mathbb R$ và với mọi $z$, không cần dữ liệu bị chặn. Vậy (S) và (G) đúng với $\beta=G=1$, và điều kiện độ dài bước là $\eta_t\le2$.

**Bước 3: một lần chạy SGD.** Dùng phép cập nhật của Thuật toán 05.11 với $W=\mathbb R$, $w_1=0$, độ dài bước $\eta=\tfrac12$ và dãy chỉ số $(1,4,2,3,4,1)$. Mỗi dòng của bảng là một bước $w_{t+1}=w_t-\tfrac12\,\partial_w\ell_{\mathrm H}(w_t,z_{i_t})$.

| $t$ | $i_t$ | Đạo hàm tại $w_t$ | $w_{t+1}$ |
|---|---|---|---|
| $1$ | $1$ | $0$ | $0$ |
| $2$ | $4$ | $-1$ | $\tfrac12$ |
| $3$ | $2$ | $-\tfrac12$ | $\tfrac34$ |
| $4$ | $3$ | $-1$ | $\tfrac54$ |
| $5$ | $4$ | $-1$ | $\tfrac74$ |
| $6$ | $1$ | $1$ | $\tfrac54$ |

Chẳng hạn ở bước $2$, $w_2-z_4=0-3=-3$ bị cắt thành $-1$, nên $w_3=0-\tfrac12\cdot(-1)=\tfrac12$.

**Kết luận.** Các điểm lặp là $w_1,\ldots,w_7=0,0,\tfrac12,\tfrac34,\tfrac54,\tfrac74,\tfrac54$. Ở §4, ta đặt cạnh lần chạy này một lần chạy trên mẫu thay quan sát thứ tư, với cùng dãy chỉ số.
:::

::: application Huấn luyện nhiều vòng cho hồi quy logistic
**Thiết lập.** Hồi quy logistic trên hồ sơ như ứng dụng của Bài 05–06: $\lVert x\rVert\le1$, $W$ là quả cầu bán kính $5$, $w_1=0$, nhưng chỉ có $m=10^4$ hồ sơ. Bán kính và cỡ mẫu là giá trị giả định; ứng dụng không dùng số liệu thật.

**Câu hỏi thực hành.** Một vòng qua dữ liệu, mỗi hồ sơ dùng một lần, cho cận $5/\sqrt{10^4+1}\approx0{,}05$ cho rủi ro vượt mức kì vọng (Nhận xét 06.3). Chạy SGD nhiều vòng trên cùng $10^4$ hồ sơ có cho cận nhỏ hơn không? Với độ dài bước $0{,}05$, nên chạy bao nhiêu bước? Câu trả lời ở §8.
:::

## 4. Hai lần chạy ghép cặp

Định nghĩa 06.9 có hai kì vọng theo $\xi$, một cho lần chạy trên $s$ và một cho lần chạy trên $s^{(i)}$. Để so hai lần chạy bước theo bước, ta cho chúng dùng chung mọi lựa chọn ngẫu nhiên.

::: algorithm Thuật toán 08.1 (SGD có chiếu trên một mẫu cố định với độ dài bước thay đổi)
**Đầu vào.** Năm thành phần sau.

- **Mẫu.** $s=(z_1,\ldots,z_m)\in\mathcal Z^m$.
- **Tập tham số.** $W\subset\mathbb R^p$ khác rỗng, đóng, lồi (có thể là $\mathbb R^p$).
- **Độ dài bước.** Một dãy tất định $\eta_1,\ldots,\eta_T>0$.
- **Số bước.** $T\ge1$.
- **Khởi tạo.** $w_1\in W$, tất định.

**Cập nhật.** Với $t=1,\ldots,T$:

1. rút $i_t$ đều trên $\{1,\ldots,m\}$, có hoàn lại, độc lập với các lần rút trước;
2. đặt $w_{t+1}=\operatorname{proj}_W\big(w_t-\eta_t\nabla\ell(w_t,z_{i_t})\big)$.

**Đầu ra.** Điểm lặp cuối $w_{T+1}$; ở §7–§8 xét thêm điểm lặp trung bình $\bar w_T=\frac1T\sum_{t=1}^Tw_t$.

**Điều kiện dừng.** Sau đúng $T$ bước; $T$ và các $\eta_t$ chọn trước khi chạy.

**Chi phí.** $T$ gradient trên một quan sát và $T$ phép chiếu.
:::

Với $\eta_t=\eta$ hằng và đầu ra $\bar w_T$, đây là Thuật toán 05.11 với oracle của Hệ quả 05.19; với $W=\mathbb R^p$, đây là SGD không chiếu của thí nghiệm mở đầu. Theo Định nghĩa 05.18, $A(s;\xi)=w_{T+1}$ với $\xi=(i_1,\ldots,i_T)$; dãy $\xi$ có $m^T$ giá trị đồng khả năng và độc lập với $S$. Chỉ số được rút có hoàn lại, nên một quan sát có thể được dùng lại ngay từ bước thứ hai; khi $T>m$, mỗi quan sát được dùng trung bình $T/m$ lần. Điểm lặp vì vậy phụ thuộc vào quan sát sắp được dùng, và Hệ quả 06.2 không áp dụng khi $T\ge2$; hệ quả này áp dụng cho một vòng theo thứ tự (Nhận xét 06.3).

::: definition Định nghĩa 08.2 (Hai lần chạy ghép cặp và ngân sách độ dài bước)
Cho mẫu $s$, chỉ số $i\in\{1,\ldots,m\}$, quan sát thay thế $z'\in\mathcal Z$ và mẫu lân cận $s^{(i)}$ như Định nghĩa 06.9, cùng các đầu vào khác của Thuật toán 08.1. Định nghĩa gồm bốn thành phần.

- **Hai lần chạy ghép cặp.** Hai lần chạy của Thuật toán 08.1, một trên $s$ (điểm lặp $w_t$) và một trên $s^{(i)}$ (điểm lặp $w'_t$), là *hai lần chạy ghép cặp* (coupled runs) nếu chúng dùng chung khởi tạo $w_1=w'_1$, các $\eta_t$ và dãy chỉ số $\xi=(i_1,\ldots,i_T)$.
- **Bước chung và bước khác biệt.** Bước $t$ là *bước chung* (shared step) nếu $i_t\ne i$, khi đó hai lần chạy dùng cùng quan sát $z_{i_t}$; bước $t$ là *bước khác biệt* (differing step) nếu $i_t=i$, khi đó lần chạy thứ nhất dùng $z_i$ và lần chạy thứ hai dùng $z'$.
- **Khoảng cách giữa hai lần chạy.** $\Delta_t=\lVert w_t-w'_t\rVert$ với $t=1,\ldots,T+1$; $\Delta_1=0$.
- **Ngân sách độ dài bước.** Tổng $\sum_{t=1}^T\eta_t$, gọi là *ngân sách độ dài bước* (cumulative step-size budget); nó bằng $\eta T$ khi độ dài bước hằng.
:::

Mỗi bước là bước khác biệt với xác suất $1/m$. Lần chạy thứ hai chỉ dùng trong chứng minh. Ghép cặp đặt hai lần chạy trên cùng không gian xác suất của $\xi$; mỗi lần chạy riêng vẫn có đúng phân bố của Thuật toán 08.1, nên hai kì vọng trong Định nghĩa 06.9 không đổi. Với hai biến $a$, $b$ trên cùng không gian, theo bất đẳng thức Jensen với hàm trị tuyệt đối, $\lvert\mathbb E_\xi a-\mathbb E_\xi b\rvert\le\mathbb E_\xi\lvert a-b\rvert$, nên ta chặn được hiệu hai kì vọng qua từng quỹ đạo; Bài 06 đã nêu dạng này ngay sau Định nghĩa 06.9.

Xét một bước trên mẫu $s=(0,1,2,3)$ của Ví dụ 08.1 và mẫu lân cận $s^{(4)}=(0,1,2,-3)$, với $w_1=0$, $\eta=\tfrac12$.

- **Hai kì vọng.** Bốn giá trị có thể của $w_2$ là $0,\tfrac12,\tfrac12,\tfrac12$ trên $s$ và $0,\tfrac12,\tfrac12,-\tfrac12$ trên $s^{(4)}$, nên $\mathbb E_\xi w_2=\tfrac38$, $\mathbb E_\xi w'_2=\tfrac18$, hiệu bằng $\tfrac14$.
- **Ghép cặp.** Hai lần chạy chỉ khác nhau khi $i_1=4$, và khi đó $\lvert w_2-w'_2\rvert=1$, nên $\mathbb E_\xi\lvert w_2-w'_2\rvert=\tfrac14$, đúng bằng hiệu.
- **Hai dãy chỉ số độc lập.** Liệt kê $16$ cặp chỉ số cho $\mathbb E\lvert w_2-w'_2\rvert=\tfrac38$, lớn hơn hiệu. Khoảng cách này gồm cả hiệu $\tfrac14$ do thay quan sát và phần do tính ngẫu nhiên của thuật toán.

::: example Ví dụ 08.2 (Hai lần chạy ghép cặp trong ví dụ Huber)
**Thiết lập.** Ví dụ 08.1 với $i=4$, $z'=-3$, nên $s^{(4)}=(0,1,2,-3)$; $\eta=\tfrac12$, $w_1=w'_1=0$ và dãy chỉ số $(1,4,2,3,4,1)$. Các bước $t=2$ và $t=5$ là bước khác biệt; bốn bước còn lại là bước chung.

**Bước 1: lần chạy trên $s^{(4)}$.** Ở bước $2$, $w'_2-z'=0+3=3$ bị cắt thành $1$, nên $w'_3=-\tfrac12$. Tính như Ví dụ 08.1, đạo hàm tại $w'_t$ ở sáu bước lần lượt là $0;1;-1;-1;1;0$, và $w'_{t+1}$ bằng $w'_t$ trừ nửa đạo hàm.

**Bước 2: khoảng cách.** Bảng ghép cột $w_{t+1}$ của Ví dụ 08.1 với lần chạy trên $s^{(4)}$.

| $t$ | $i_t$ | $w_{t+1}$ | $w'_{t+1}$ | $\Delta_{t+1}$ |
|---|---|---|---|---|
| $1$ | $1$ | $0$ | $0$ | $0$ |
| $2$ | $4$ | $\tfrac12$ | $-\tfrac12$ | $1$ |
| $3$ | $2$ | $\tfrac34$ | $0$ | $\tfrac34$ |
| $4$ | $3$ | $\tfrac54$ | $\tfrac12$ | $\tfrac34$ |
| $5$ | $4$ | $\tfrac74$ | $0$ | $\tfrac74$ |
| $6$ | $1$ | $\tfrac54$ | $0$ | $\tfrac54$ |

**Bước 3: hai loại bước.** Ở bước khác biệt $t=2$, khoảng cách tăng từ $0$ lên $1$; ở bước khác biệt $t=5$, từ $\tfrac34$ lên $\tfrac74$. Mỗi lần tăng đúng $1=2G\eta$. Ở các bước chung, khoảng cách không tăng: $0\to0$ ở bước $1$, $1\to\tfrac34$ ở bước $3$, $\tfrac34\to\tfrac34$ ở bước $4$, $\tfrac74\to\tfrac54$ ở bước $6$.

**Bước 4: tổng các phần tăng.** Dãy có hai bước khác biệt, nên tổng các phần tăng ở Bước 3 là $2\cdot2G\eta=2$, và $\Delta_7=\tfrac54\le2$.

**Kết luận.** Khoảng cách chỉ tăng ở các bước dùng quan sát khác biệt, mỗi lần không quá $2G\eta$; ở các bước chung nó không tăng.
:::

Ví dụ 08.2 chỉ xét một dãy chỉ số; Định nghĩa 06.9 cần kì vọng theo $\xi$, nên hai sự kiện ở Bước 3 phải được chứng minh cho mọi dãy.

## 5. Bước gradient không giãn

Ở một bước chung, hai lần chạy áp dụng cùng một ánh xạ $w\mapsto\operatorname{proj}_W\big(w-\eta_t\nabla\ell(w,z_{i_t})\big)$ cho hai điểm $w_t$ và $w'_t$. Cần biết ánh xạ này kéo hai điểm lại gần hay đẩy chúng ra xa.

::: definition Định nghĩa 08.3 (Hệ số giãn, ánh xạ không giãn và tính đồng bức)
Cho ánh xạ $\Gamma:\mathbb R^p\to\mathbb R^p$, hàm khả vi $f:\mathbb R^p\to\mathbb R$, số $\kappa\ge0$ và $\beta>0$. Định nghĩa gồm ba thành phần.

- **Hệ số giãn.** $\Gamma$ có *hệ số giãn* $\kappa$ (expansion factor) nếu $\lVert\Gamma(u)-\Gamma(v)\rVert\le\kappa\lVert u-v\rVert$ với mọi $u,v\in\mathbb R^p$.
- **Ánh xạ không giãn.** $\Gamma$ là *ánh xạ không giãn* (nonexpansive map) nếu nó có hệ số giãn $1$.
- **Tính đồng bức.** Gradient $\nabla f$ là *$\tfrac1\beta$-đồng bức* ($\tfrac1\beta$-co-coercive) nếu với mọi $u,v\in\mathbb R^p$,
  $$
  \begin{aligned}
  &\langle\nabla f(u)-\nabla f(v),u-v\rangle\\
  &\ge\tfrac1\beta\lVert\nabla f(u)-\nabla f(v)\rVert^2 .
  \end{aligned}
  $$
:::

Ta gọi $\Gamma_{\eta,z}(w)=w-\eta\nabla\ell(w,z)$ là *ánh xạ bước gradient* (gradient step map). Hợp của hai ánh xạ có hệ số giãn $\kappa_1$ và $\kappa_2$ có hệ số giãn $\kappa_1\kappa_2$, và phép chiếu $\operatorname{proj}_W$ không giãn (Bài 05). Nếu $\nabla f$ là $\tfrac1\beta$-đồng bức thì, theo bất đẳng thức Cauchy–Schwarz, $\tfrac1\beta\lVert\nabla f(u)-\nabla f(v)\rVert^2\le\lVert\nabla f(u)-\nabla f(v)\rVert\,\lVert u-v\rVert$, nên $\nabla f$ là $\beta$-Lipschitz, tức $f$ là $\beta$-trơn. Bổ đề dưới đây cho chiều ngược lại khi $f$ lồi.

Với $f(w)=\tfrac\beta2\lVert w\rVert^2$, ta có $\nabla f(w)=\beta w$; vế trái của bất đẳng thức đồng bức bằng $\beta\lVert u-v\rVert^2$, vế phải bằng $\tfrac1\beta\beta^2\lVert u-v\rVert^2=\beta\lVert u-v\rVert^2$, nên dấu bằng xảy ra. Hàm $f(w)=-\tfrac12w^2$ trên $\mathbb R$ là $1$-trơn, nhưng vế trái bằng $-(u-v)^2<0$ khi $u\ne v$, nên $\nabla f$ không đồng bức với hằng số nào.

::: lemma Bổ đề 08.4 (Bước gradient không giãn) — phác thảo (tính đồng bức chứng minh ở Phụ lục A)
**Giả thiết.** Ba thành phần sau.

- **Hàm.** $f:\mathbb R^p\to\mathbb R$ lồi và $\beta$-trơn trên toàn $\mathbb R^p$.
- **Độ dài bước.** $0\le\eta\le2/\beta$.
- **Tập.** $W\subset\mathbb R^p$ khác rỗng, đóng, lồi.

**Bảo đảm.** Ba khẳng định tất định.

- **(a) Tính đồng bức.** $\nabla f$ là $\tfrac1\beta$-đồng bức.
- **(b) Bước gradient không giãn.** Với $\Gamma(w)=w-\eta\nabla f(w)$, mọi $u,v\in\mathbb R^p$ và $g_{uv}=\nabla f(u)-\nabla f(v)$,
  $$
  \begin{aligned}
  &\lVert\Gamma(u)-\Gamma(v)\rVert^2\\
  &\le\lVert u-v\rVert^2\\
  &\quad-\eta\big(\tfrac2\beta-\eta\big)\lVert g_{uv}\rVert^2\\
  &\le\lVert u-v\rVert^2 .
  \end{aligned}
  $$
- **(c) Bước có chiếu.** Ánh xạ $w\mapsto\operatorname{proj}_W(\Gamma(w))$ không giãn.
:::

::: proof Chứng minh Bổ đề 08.4 (phác thảo)
**Lộ trình.** Phần (a) chứng minh ở Phụ lục A. Phần (b) khai triển bình phương rồi dùng (a). Phần (c) là hợp của hai ánh xạ không giãn. Bất đẳng thức then chốt là tính đồng bức (a).

**Bước 1 (phần b; tính lồi và tính trơn qua (a)).** Khai triển bình phương:
$$
\begin{aligned}
&\lVert\Gamma(u)-\Gamma(v)\rVert^2\\
&=\lVert(u-v)-\eta g_{uv}\rVert^2\\
&=\lVert u-v\rVert^2-2\eta\langle g_{uv},u-v\rangle\\
&\quad+\eta^2\lVert g_{uv}\rVert^2 .
\end{aligned}
$$
Theo (a), $\langle g_{uv},u-v\rangle\ge\tfrac1\beta\lVert g_{uv}\rVert^2$, nên số hạng giữa không quá $-\tfrac{2\eta}\beta\lVert g_{uv}\rVert^2$; tính lồi và tính trơn của $f$ được dùng ở đây, qua (a). Gộp hai số hạng chứa $\lVert g_{uv}\rVert^2$, ta được bất đẳng thức thứ nhất của (b).

**Bước 2 (phần b; điều kiện độ dài bước).** Vì $0\le\eta\le2/\beta$, hệ số $\eta(2/\beta-\eta)$ không âm, nên bỏ số hạng đó ta được bất đẳng thức thứ hai. Điều kiện $\eta\le2/\beta$ được dùng ở đây.

**Bước 3 (phần c).** Phép chiếu lên $W$ đóng, lồi là không giãn (đoạn sau Bổ đề 05.8), và $\Gamma$ không giãn theo (b); hợp của hai ánh xạ không giãn là không giãn.

$\square$ Một bước SGD trên hàm lỗi lồi, trơn, với $\eta_t\le2/\beta$, không làm tăng khoảng cách giữa hai điểm bất kì; do đó ở mỗi bước chung, $\Delta_{t+1}\le\Delta_t$.
:::

::: example Ví dụ 08.3 (Hệ số giãn của bước gradient một chiều)
**Thiết lập.** Cho $p=1$, $W=\mathbb R$, ba hàm $\beta$-trơn với $\beta=1$ và ba độ dài bước $\eta\in\{\tfrac12,2,3\}$. Với mỗi ánh xạ bước, ta tìm số $\kappa$ nhỏ nhất thỏa Định nghĩa 08.3, gọi là hệ số giãn nhỏ nhất; với một ánh xạ tuyến tính từng khúc và liên tục trên $\mathbb R$, số đó là trị tuyệt đối lớn nhất của hệ số góc.

**Bước 1: hàm bậc hai.** Với $f(w)=\tfrac12w^2$, $\Gamma(w)=(1-\eta)w$, nên hệ số giãn nhỏ nhất là $\lvert1-\eta\rvert$.

**Bước 2: hàm lỗi Huber của Ví dụ 08.1.** $\Gamma$ có hệ số góc $1-\eta$ khi $\lvert w-z\rvert<1$ và $1$ khi $\lvert w-z\rvert>1$ (đạo hàm là hằng $\pm1$ ở đó). Hệ số giãn nhỏ nhất là $\max\{\lvert1-\eta\rvert,1\}$.

**Bước 3: hàm lõm.** Với $f(w)=-\tfrac12w^2$ ($1$-trơn, không lồi), $\Gamma(w)=(1+\eta)w$, nên hệ số giãn nhỏ nhất là $1+\eta>1$ với mọi $\eta>0$.

**Bước 4: thay số.** Bảng ghi hệ số giãn nhỏ nhất.

| $\eta$ | Bậc hai | Huber | Lõm |
|---|---|---|---|
| $\tfrac12$ | $\tfrac12$ | $1$ | $\tfrac32$ |
| $2$ | $1$ | $1$ | $3$ |
| $3$ | $2$ | $2$ | $4$ |

**Kết luận.** Ngưỡng $2/\beta$ là chặt: với hàm bậc hai và $\eta=2$, hệ số giãn nhỏ nhất bằng đúng $1$, còn với $\eta=3$ nó bằng $2$. Không có tính lồi, bước gradient có thể giãn với mọi độ dài bước dương, như hàm lõm ở Bước 3 (§9).
:::

Ở bước khác biệt, hai lần chạy áp dụng hai ánh xạ khác nhau, $\Gamma_{\eta_t,z_i}$ và $\Gamma_{\eta_t,z'}$, nên Bổ đề 08.4 không chặn được $\Delta_{t+1}$.

## 6. Bất đẳng thức truy hồi cho khoảng cách giữa hai lần chạy

Cận gradient (G) giới hạn phần tăng của khoảng cách ở bước khác biệt. Ghép trường hợp này với bước chung (Bổ đề 08.4), ta được một *bất đẳng thức truy hồi* (recurrence inequality) cho $\Delta_t$.

::: proposition Mệnh đề 08.5 (Bất đẳng thức truy hồi cho khoảng cách giữa hai lần chạy ghép cặp) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau.

- **Hàm lỗi.** (S) với hằng số $\beta$; (G) với hằng số $G$.
- **Mẫu.** $s$, $i$, $z'$ bất kì, cố định; $s^{(i)}$ như Định nghĩa 06.9.
- **Thuật toán.** Hai lần chạy ghép cặp theo phép cập nhật của Thuật toán 08.1 (Định nghĩa 08.2), với $0<\eta_t\le2/\beta$.
- **Chỉ số.** Một quy tắc rút chỉ số với $\Pr(i_t=i)=1/m$ cho mọi $t$, chẳng hạn rút đều có hoàn lại.

**Bảo đảm.** Hai khẳng định.

- **(a) Trên từng quỹ đạo.** Tất định, với mọi giá trị của $\xi$ và mọi $t$,
  $$
  \begin{aligned}
  \Delta_{t+1}&\le\Delta_t\\
  &\quad+2G\eta_t\,\mathbb 1[i_t=i],
  \end{aligned}
  $$
  nên $\Delta_{T+1}\le2G\sum_{t=1}^T\eta_t\,\mathbb 1[i_t=i]$.
- **(b) Theo kì vọng theo $\xi$, với mẫu cố định.** Với mọi $t$, $\mathbb E\Delta_{t+1}\le\mathbb E\Delta_t+2G\eta_t/m$, và
  $$
  \mathbb E\Delta_{T+1}\le\frac{2G}m\sum_{t=1}^T\eta_t .
  $$

Cận đúng với mọi mẫu và mọi cách thay một quan sát; nó không dùng phân bố $D$ và không phụ thuộc $p$.
:::

::: proof Chứng minh Mệnh đề 08.5
**Lộ trình.** So một bước trên hai quỹ đạo theo hai trường hợp (bước chung, bước khác biệt), cộng dọc quỹ đạo, rồi lấy kì vọng bằng tính tuyến tính. Bất đẳng thức then chốt là (a), chứng minh trên từng quỹ đạo.

**Bước 1 (bước chung; (S) và $\eta_t\le2/\beta$ qua Bổ đề 08.4(c)).** Nếu $i_t\ne i$, cả hai lần chạy áp dụng cùng ánh xạ $\operatorname{proj}_W\circ\Gamma_{\eta_t,z_{i_t}}$ cho $w_t$ và $w'_t$. Theo Bổ đề 08.4(c) với $f=\ell(\cdot,z_{i_t})$, ánh xạ này không giãn, nên $\Delta_{t+1}\le\Delta_t$.

**Bước 2 (bước khác biệt; (G) và tính không giãn của phép chiếu).** Nếu $i_t=i$, lần chạy thứ nhất dùng $z_i$ và lần chạy thứ hai dùng $z'$. Đặt $g_t=\nabla\ell(w_t,z_i)$ và $g'_t=\nabla\ell(w'_t,z')$. Phép chiếu lên $W$ đóng, lồi là không giãn; theo bất đẳng thức tam giác,
$$
\begin{aligned}
&\Delta_{t+1}\\
&\le\lVert(w_t-w'_t)-\eta_t(g_t-g'_t)\rVert\\
&\le\Delta_t+\eta_t\lVert g_t\rVert+\eta_t\lVert g'_t\rVert\\
&\le\Delta_t+2G\eta_t .
\end{aligned}
$$
Bất đẳng thức cuối dùng (G) hai lần, tại $w_t$ và $w'_t$; hai điểm này thuộc $W$ vì $w_1=w'_1\in W$ và mỗi điểm lặp sau là một phép chiếu lên $W$. Bước này không dùng tính lồi của hàm lỗi hay điều kiện độ dài bước.

**Bước 3 (tổng triệt tiêu).** Gộp hai trường hợp, ta được bất đẳng thức đầu của (a). Cộng nó từ $t=1$ đến $T$, các số hạng $\Delta_2,\ldots,\Delta_T$ triệt tiêu, và $\Delta_1=0$ vì $w_1=w'_1$; ta được bất đẳng thức sau của (a).

**Bước 4 (kì vọng; giả thiết về chỉ số).** Dãy $\xi$ có hữu hạn giá trị, nên mọi kì vọng dưới đây là trung bình hữu hạn. Lấy kì vọng hai vế của (a) và dùng $\mathbb E\,\mathbb 1[i_t=i]=\Pr(i_t=i)=1/m$:
$$
\begin{aligned}
\mathbb E\Delta_{T+1}&\le2G\sum_{t=1}^T\eta_t\,\Pr(i_t=i)\\
&=\frac{2G}m\sum_{t=1}^T\eta_t ;
\end{aligned}
$$
bất đẳng thức một bước của (b) có cùng lý do. Bước này chỉ dùng tính tuyến tính của kì vọng và xác suất biên của $i_t$. Không cần $i_t$ độc lập với $\Delta_t$, vì (a) đúng trên từng quỹ đạo.

$\square$ Thừa số $1/m$ là xác suất một bước dùng quan sát khác biệt; mỗi lần như vậy, khoảng cách giữa hai lần chạy tăng không quá $2G\eta_t$.
:::

Hằng số $2G$ không giảm được. Với hàm lỗi Huber của Ví dụ 08.1, $w_t=w'_t=1$, $z_i=3$, $z'=-3$ và $\eta=\tfrac12$, hai bước cho $1+\tfrac12=\tfrac32$ và $1-\tfrac12=\tfrac12$, cách nhau đúng $1=2G\eta$. Mệnh đề cũng giữ nguyên khi *xáo trộn lại sau mỗi vòng qua dữ liệu* (random reshuffling): mỗi vòng là một hoán vị đều của $\{1,\ldots,m\}$, nên vẫn có $\Pr(i_t=i)=1/m$, dù các $i_t$ không độc lập (Phụ lục B).

::: example Ví dụ 08.4 (Kì vọng của khoảng cách trong ví dụ Huber)
**Thiết lập.** Ví dụ 08.2 ($s=(0,1,2,3)$, $s^{(4)}=(0,1,2,-3)$, $\eta=\tfrac12$, $w_1=w'_1=0$), nhưng dãy chỉ số ngẫu nhiên, đều trên $\{1,2,3,4\}^T$. Ta có $G=1$, $m=4$, nên cận (b) là $\tfrac{2G\eta T}m=\tfrac T4$.

**Bước 1: $T=1$.** Ta có $\Delta_2=1$ nếu $i_1=4$ và $\Delta_2=0$ nếu không, nên $\mathbb E\Delta_2=\tfrac14$. Đây là dấu bằng trong (b).

**Bước 2: $T=2$.** Liệt kê $16$ dãy $(i_1,i_2)$ theo hai nhóm.

- **Nhóm $i_1\ne4$** ($12$ dãy). Bước đầu là bước chung, nên $w_2=w'_2\in\{0,\tfrac12\}$. Nếu $i_2\ne4$, bước thứ hai cũng là bước chung và $\Delta_3=0$. Nếu $i_2=4$, ta có $w_2-3<-1$ và $w_2+3>1$, nên hai đạo hàm là $-1$ và $1$, và $\Delta_3=\tfrac12\cdot2=1$. Tổng của nhóm là $3\cdot1=3$.
- **Nhóm $i_1=4$** ($4$ dãy). Ta có $w_2=\tfrac12$ và $w'_2=-\tfrac12$. Bảng dưới tính bước thứ hai theo $i_2$ như Ví dụ 08.2; tổng của nhóm là $\tfrac12+\tfrac34+1+2=\tfrac{17}4$.

| $i_2$ | $w_3$ | $w'_3$ | $\Delta_3$ |
|---|---|---|---|
| $1$ | $\tfrac14$ | $-\tfrac14$ | $\tfrac12$ |
| $2$ | $\tfrac34$ | $0$ | $\tfrac34$ |
| $3$ | $1$ | $0$ | $1$ |
| $4$ | $1$ | $-1$ | $2$ |

Do đó
$$
\begin{aligned}
\mathbb E\Delta_3&=\frac{3+17/4}{16}=\frac{29}{64}\\
&\approx0{,}4531<\frac12 .
\end{aligned}
$$

**Bước 3: $T=6$.** Liệt kê $4^6=4096$ dãy bằng máy tính cho
$$
\begin{aligned}
\mathbb E\Delta_7&=\frac{228\,203}{262\,144}\approx0{,}8705\\
&\le\frac64=1{,}5 .
\end{aligned}
$$

**Bước 4: một quỹ đạo đạt cận (a).** Với dãy $(2,3,1,4,4,4)$, hai lần chạy trùng nhau đến hết bước $3$ ($w_4=w'_4=\tfrac12$), rồi ba bước khác biệt liên tiếp cho $w_7=2$, $w'_7=-1$ và $\Delta_7=3=2G\eta\cdot3$.

**Kết luận.** Cận (b) đạt dấu bằng ở bước đầu. Sau đó các bước chung kéo hai lần chạy lại gần nhau (nhóm $i_1=4$, $i_2=1$: $\Delta$ giảm từ $1$ xuống $\tfrac12$), nên kì vọng tăng chậm hơn cận.
:::

Cận của Mệnh đề 08.5 chỉ dùng xác suất $1/m$ của bước khác biệt và bỏ qua việc các bước chung có thể kéo hai lần chạy lại gần nhau.

## 7. Tính ổn định đều của SGD

Theo (G) và tính lồi của $W$, hàm lỗi tại một quan sát kiểm tra bất kì thay đổi không quá $G$ nhân khoảng cách giữa hai điểm lặp. Ghép điều này với Mệnh đề 08.5 cho tính ổn định đều theo Định nghĩa 06.9, rồi Định lý 06.10 cho cận khoảng cách tổng quát hóa.

::: theorem Định lý 08.6 (Tính ổn định đều của SGD với hàm lỗi lồi và trơn) — chứng minh đầy đủ
**Giả thiết.** Bốn thành phần sau.

- **Mẫu.** $S\sim D^m$ theo dạng đầy đủ của (T1); chỉ dùng cho (c).
- **Hàm lỗi.** (T2); (S) với hằng số $\beta$; (G) với hằng số $G$.
- **Tập tham số.** $W$ khác rỗng, đóng, lồi (có thể là $\mathbb R^p$); $w_1\in W$ tất định.
- **Thuật toán.** Thuật toán 08.1 với $0<\eta_t\le2/\beta$ tất định; $\xi=(i_1,\ldots,i_T)$ độc lập với $S$; đầu ra $A(S;\xi)=w_{T+1}$.

**Bảo đảm.** Ba khẳng định.

**(a) Dạng ghép cặp.** Theo kì vọng theo $\xi$, với mọi $s$, $i$, $z'$ và mọi quan sát kiểm tra $z\in\mathcal Z$,
$$
\begin{aligned}
&\mathbb E_\xi\big\lvert\ell(w_{T+1},z)-\ell(w'_{T+1},z)\big\rvert\\
&\le\frac{2G^2}m\sum_{t=1}^T\eta_t,
\end{aligned}
$$
trong đó $w'_{T+1}$ là điểm lặp cuối của lần chạy ghép cặp trên $s^{(i)}$.

**(b) Ổn định đều.** Thuật toán ổn định đều (Định nghĩa 06.9) với
$$
\epsilon_{\mathrm{stab}}(m)=\frac{2G^2}m\sum_{t=1}^T\eta_t .
$$

**(c) Khoảng cách tổng quát hóa kì vọng.** Theo kì vọng theo $(S,\xi)$,
$$
\begin{aligned}
&\big\lvert\mathbb E_{S,\xi}[L_D(w_{T+1})-L_S(w_{T+1})]\big\rvert\\
&\le\frac{2G^2}m\sum_{t=1}^T\eta_t .
\end{aligned}
$$

Với độ dài bước hằng, vế phải là $2G^2\eta T/m$. Cận không phụ thuộc $p$ hay kích thước của $W$, phụ thuộc quỹ đạo chỉ qua ngân sách độ dài bước, và chỉ đúng theo kì vọng; nó chặn khoảng cách tổng quát hóa kì vọng, chứ không chặn $\mathbb E\lvert L_D-L_S\rvert$ hay $L_D$. Bảo đảm chỉ áp dụng cho Thuật toán 08.1 với quy tắc rút chỉ số đã nêu.
:::

::: proof Chứng minh Định lý 08.6
**Lộ trình.** Tính Lipschitz của hàm lỗi tại quan sát kiểm tra đưa hiệu hàm lỗi về $\Delta_{T+1}$; Mệnh đề 08.5 chặn $\mathbb E_\xi\Delta_{T+1}$; hiệu hai kì vọng không quá kì vọng của trị tuyệt đối; kiểm tra tính khả tích; cuối cùng áp dụng Định lý 06.10. Bất đẳng thức then chốt là Mệnh đề 08.5(b).

**Bước 1 (tính Lipschitz; (G) và tính lồi của $W$).** Cho $z\in\mathcal Z$ và $u,v\in W$. Vì $W$ lồi, đoạn thẳng nối $v$ với $u$ nằm trong $W$. Hàm $r\mapsto\ell(v+r(u-v),z)$ khả vi trên $[0,1]$, nên theo định lý giá trị trung bình, có $r\in(0,1)$ với $\ell(u,z)-\ell(v,z)=\langle\nabla\ell(v+r(u-v),z),u-v\rangle$. Theo bất đẳng thức Cauchy–Schwarz và (G) tại điểm $v+r(u-v)\in W$,
$$
\lvert\ell(u,z)-\ell(v,z)\rvert\le G\lVert u-v\rVert .
$$
Bước này không dùng tính lồi của hàm lỗi.

**Bước 2 (phần a; Mệnh đề 08.5(b)).** Hai điểm $w_{T+1}$ và $w'_{T+1}$ thuộc $W$. Theo Bước 1 rồi Mệnh đề 08.5(b),
$$
\begin{aligned}
&\mathbb E_\xi\big\lvert\ell(w_{T+1},z)-\ell(w'_{T+1},z)\big\rvert\\
&\le G\,\mathbb E_\xi\Delta_{T+1}\\
&\le\frac{2G^2}m\sum_{t=1}^T\eta_t .
\end{aligned}
$$

**Bước 3 (phần b; hiệu hai kì vọng).** Dãy $\xi$ có hữu hạn giá trị, nên $\mathbb E_\xi\ell(w_{T+1},z)$ và $\mathbb E_\xi\ell(w'_{T+1},z)$ hữu hạn. Ghép cặp không đổi phân bố của từng lần chạy, nên hai kì vọng này đúng là hai kì vọng trong Định nghĩa 06.9. Do đó
$$
\begin{aligned}
&\big\lvert\mathbb E_\xi\ell(w_{T+1},z)-\mathbb E_\xi\ell(w'_{T+1},z)\big\rvert\\
&\le\mathbb E_\xi\big\lvert\ell(w_{T+1},z)-\ell(w'_{T+1},z)\big\rvert,
\end{aligned}
$$
và theo phần (a), điều kiện của Định nghĩa 06.9 đúng với hệ số đã nêu.

**Bước 4 (tính khả tích; (G) và (T2)).** Theo (G), gradient $g_t=\nabla\ell(w_t,z_{i_t})$ có chuẩn không quá $G$, và $w_1=\operatorname{proj}_W(w_1)$ vì $w_1\in W$. Phép chiếu không giãn, nên
$$
\begin{aligned}
&\lVert w_{t+1}-w_1\rVert\\
&\le\lVert(w_t-w_1)-\eta_tg_t\rVert\\
&\le\lVert w_t-w_1\rVert+\eta_tG .
\end{aligned}
$$
Cộng theo $t$, ta được $\lVert w_{T+1}-w_1\rVert\le G\sum_t\eta_t$. Theo Bước 1, $\ell(w_{T+1},z)\le\ell(w_1,z)+G^2\sum_t\eta_t$ với mọi $z$. Áp dụng với $z=Z_j$ rồi lấy trung bình theo $j$ và kì vọng, $\mathbb EL_S(w_{T+1})\le L_D(w_1)+G^2\sum_t\eta_t$ (Mệnh đề 01.7 cho $w_1$ cố định). Lấy kì vọng theo $z\sim D$ rồi theo $(S,\xi)$,
$$
\begin{aligned}
\mathbb E_{S,\xi}L_D(w_{T+1})&\le L_D(w_1)\\
&\quad+G^2\sum_{t=1}^T\eta_t,
\end{aligned}
$$
và vế phải hữu hạn theo (T2). Tính đo được của $(s,\xi,z)\mapsto\ell(w_{T+1},z)$ ở Phụ lục B.

**Bước 5 (phần c; Định lý 06.10 và (T1)).** Thuật toán $A(S;\xi)=w_{T+1}$ thỏa mọi giả thiết của Định lý 06.10: (T1) dạng đầy đủ, $\xi$ độc lập với $S$, ổn định đều theo (b), (T2), và khả tích theo Bước 4. Định lý 06.10 cho (c).

$\square$ Với hàm lỗi lồi, trơn, có gradient bị chặn, SGD trên một mẫu cố định có khoảng cách tổng quát hóa kì vọng nhỏ khi ngân sách độ dài bước nhỏ so với cỡ mẫu, bất kể số chiều.
:::

Giả thiết (G) được dùng ở bước khác biệt, cho tính Lipschitz tại mọi quan sát kiểm tra, và cho tính khả tích ở Bước 4. Hằng số $\beta$ chỉ đi vào qua điều kiện $\eta_t\le2/\beta$. Tính lồi của hàm lỗi chỉ đi vào qua Bổ đề 08.4(a), ở các bước chung. Tính lồi của $W$ cho tính không giãn của phép chiếu ở mọi bước và tính Lipschitz ở Bước 1.

::: example Ví dụ 08.5 (Cận ổn định cho hồi quy logistic)
**Thiết lập.** Hồi quy logistic với hàm lỗi $\ell(w,(x,y))=\ln\big(1+e^{-\tilde y\langle w,x\rangle}\big)$, $\tilde y=2y-1$, và $\lVert x\rVert\le1$ trên toàn $\mathcal X$; $W=\mathbb R^p$ hoặc quả cầu bán kính $5$.

**Bước 1: hằng số.** Theo Bài tập 05.8, (S) đúng với $\beta=\tfrac14$ và (G) đúng với $G=1$ trên toàn $\mathbb R^p$. Điều kiện độ dài bước là $\eta_t\le2/\beta=8$. Ta có $\ell\ge0$ và $L_D(0)=\ln2$, nên (T2) đúng với $w_1=0$.

**Bước 2: ứng dụng của Bài 05.** Với $m=10^6$, $\eta=0{,}05$ và $T=10^4$ (Ví dụ 05.9), cận của Định lý 08.6 cho điểm lặp cuối là
$$
\frac{2\cdot1\cdot0{,}05\cdot10^4}{10^6}=0{,}001 .
$$

**Bước 3: thí nghiệm mở đầu.** Với $m=200$ và $\eta=0{,}5$, sau $t$ bước cận là
$$
\frac{2\cdot1\cdot0{,}5\cdot t}{200}=\frac t{200}.
$$
Cận bằng $1$ sau một vòng ($t=200$) và bằng $100$ sau $100$ vòng ($t=20\,000$).

**Kết luận.** Cận tăng tuyến tính theo số bước. Nó nhỏ khi $T\eta$ nhỏ so với $m$; với $200$ quan sát, nó vượt $1$ ngay từ vòng thứ hai.
:::

::: example Ví dụ 08.6 (Hai lần chạy ghép cặp trong thí nghiệm mở đầu)
**Thiết lập.** Giao thức ở Phụ lục F. Với mỗi hạt giống, ta tạo một mẫu lân cận bằng cách thay quan sát có chỉ số rút đều bằng một quan sát mới từ $D$, rồi chạy hai lần chạy ghép cặp.

**Bước 1: kiểm tra giả thiết.** Mọi giả thiết của Định lý 08.6 đều thỏa.

- **(T1).** Mẫu huấn luyện và mẫu kiểm tra gồm các quan sát độc lập cùng phân bố; nhãn được lật độc lập giữa các quan sát.
- **(T2).** Hàm lỗi logistic không âm và $L_D(0)=\ln2$.
- **(S) và (G).** Với $\beta=\tfrac14$ và $G=1$, vì mọi đặc trưng có thể có đều thỏa $\lVert x\rVert\le1$ do cách sinh dữ liệu, không chỉ các đặc trưng trên mẫu.
- **Thuật toán.** $W=\mathbb R^p$, $\eta=0{,}5\le8$, chỉ số rút đều có hoàn lại.

Mệnh đề 08.5(b) chặn $\mathbb E_\xi\Delta_{t+1}$ cho từng cặp mẫu lân cận, nên cũng chặn trung bình theo các cặp. Với $G=1$, cận của $\mathbb E\Delta_{t+1}$ và cận của khoảng cách tổng quát hóa cùng bằng $t/200$.

**Bước 2: bảng.** Bảng ghi trung bình của $20$ hạt giống. Cột giữa là $\Delta_{t+1}$ của hai lần chạy ghép cặp; cột cuối là *tỉ lệ đổi nhãn dự đoán* (prediction flip rate), tức tỉ lệ quan sát kiểm tra mà hai lần chạy ghép cặp dự đoán nhãn khác nhau.

| Vòng | $\Delta$ ghép cặp | Đổi nhãn |
|---|---|---|
| $0{,}5$ | $0{,}142$ | $0{,}015$ |
| $1$ | $0{,}233$ | $0{,}016$ |
| $5$ | $0{,}873$ | $0{,}022$ |
| $20$ | $2{,}219$ | $0{,}026$ |
| $100$ | $5{,}458$ | $0{,}034$ |

Ở $100$ vòng, $\Delta$ ghép cặp của các hạt giống nằm trong khoảng $1{,}31$–$15{,}08$.

**Bước 3: khoảng cách tổng quát hóa.** Cột "Khoảng cách" của câu hỏi mở đầu ước lượng $\mathbb E[L_D-L_S]$, với $L_D$ thay bằng trung bình trên $5000$ quan sát kiểm tra. Cận lớn hơn khoảng cách đó từ khoảng $11$ lần (nửa vòng: $0{,}5/0{,}045\approx11{,}1$) đến khoảng $109$ lần ($100$ vòng: $100/0{,}919\approx108{,}8$). Ở $100$ vòng, khoảng cách của các hạt giống nằm trong khoảng $0{,}693$–$1{,}149$.

**Bước 4: đọc bảng.** $\Delta$ ghép cặp tăng chậm hơn tuyến tính và luôn nằm dưới cận. Định lý không chặn tỉ lệ đổi nhãn, vì hàm lỗi 0–1 không Lipschitz theo $w$.

**Kết luận.** Trong thí nghiệm, $\Delta$ ghép cặp và khoảng cách tổng quát hóa đều nằm dưới cận $t/200$ và tăng chậm hơn tuyến tính; cận không cho hình dạng của các đường cong này.
:::

Định lý 08.6 nói về điểm lặp cuối. Thuật toán 05.11 và các cận tối ưu của Bài 05 dùng điểm lặp trung bình, nên ta cần cùng loại cận cho $\bar w_T$.

::: corollary Hệ quả 08.7 (Tính ổn định của điểm lặp trung bình) — chứng minh đầy đủ
**Giả thiết.** Như Định lý 08.6, với đầu ra $A(S;\xi)=\bar w_T=\frac1T\sum_{t=1}^Tw_t$.

**Bảo đảm.** Thuật toán ổn định đều với
$$
\epsilon_{\mathrm{stab}}(m)=\frac{2G^2}m\sum_{t=1}^{T-1}\frac{T-t}T\,\eta_t,
$$
bằng $G^2\eta(T-1)/m$ khi độ dài bước hằng. Cùng số đó chặn trị tuyệt đối của khoảng cách tổng quát hóa kì vọng của $\bar w_T$, theo kì vọng theo $(S,\xi)$.
:::

::: proof Chứng minh Hệ quả 08.7
**Lộ trình.** Chặn khoảng cách giữa hai điểm lặp trung bình bằng trung bình của các $\Delta_t$, dùng Mệnh đề 08.5(b) cho từng $t$, rồi đổi thứ tự lấy tổng. Bất đẳng thức then chốt là Mệnh đề 08.5(b), áp dụng cho từng $t$.

**Bước 1 (khoảng cách giữa hai trung bình).** Vì $W$ lồi, $\bar w_T\in W$ và $\bar w'_T=\frac1T\sum_tw'_t\in W$. Theo bất đẳng thức tam giác,
$$
\lVert\bar w_T-\bar w'_T\rVert\le\frac1T\sum_{t=1}^T\Delta_t .
$$

**Bước 2 (Mệnh đề 08.5(b) đến bước $t-1$).** Áp dụng Mệnh đề 08.5(b) cho $t-1$ bước đầu, ta có $\mathbb E\Delta_t\le\frac{2G}m\sum_{k=1}^{t-1}\eta_k$; với $t=1$, tổng rỗng và $\Delta_1=0$.

**Bước 3 (đổi thứ tự lấy tổng).** Mỗi $\eta_k$ xuất hiện trong các tổng ứng với $t=k+1,\ldots,T$, tức $T-k$ lần, nên
$$
\begin{aligned}
\sum_{t=1}^T\sum_{k=1}^{t-1}\eta_k&=\sum_{k=1}^{T-1}(T-k)\,\eta_k .
\end{aligned}
$$
Với $\eta_k=\eta$ hằng, $\sum_{k=1}^{T-1}(T-k)=T(T-1)/2$.

**Bước 4 (hệ số ổn định; Bước 1 của chứng minh Định lý 08.6).** Theo Bước 1 của chứng minh Định lý 08.6, $\mathbb E_\xi\lvert\ell(\bar w_T,z)-\ell(\bar w'_T,z)\rvert\le G\,\mathbb E_\xi\lVert\bar w_T-\bar w'_T\rVert$. Ghép với Bước 1–3, ta được hệ số ổn định đã nêu; với bước hằng, nó bằng $\frac{2G^2}m\cdot\frac\eta T\cdot\frac{T(T-1)}2=\frac{G^2\eta(T-1)}m$.

**Bước 5 (tính khả tích và Định lý 06.10).** Ta có $\lVert\bar w_T-w_1\rVert\le\frac1T\sum_t\lVert w_t-w_1\rVert\le G\sum_t\eta_t$, nên $\mathbb EL_D(\bar w_T)<\infty$ như Bước 4 của chứng minh Định lý 08.6. Định lý 06.10 cho cận khoảng cách tổng quát hóa.

$\square$ Với độ dài bước hằng, cận của điểm lặp trung bình nhỏ hơn một nửa cận $2G^2\eta T/m$ của điểm lặp cuối, vì các điểm lặp đầu của hai lần chạy còn gần nhau.
:::

Hệ quả 08.7 áp dụng cho chương trình chạy nhiều vòng của Bài 06 (Ví dụ 06.3): hàm lỗi $(w-y)^2$ với $\lvert y\rvert\le1$, $W=[-1,1]$, $m=4$, $\eta=0{,}00625$ và $T=1600$. Hàm lỗi thỏa (S) với $\beta=2$ và (G) với $G=2(1+1)=4$ trên $W$, và $\eta\le1=2/\beta$. Cận là
$$
\begin{aligned}
\frac{G^2\eta(T-1)}m&=\frac{16\cdot0{,}00625\cdot1599}4\\
&=39{,}975 .
\end{aligned}
$$
Trên $W$, hàm lỗi nhận giá trị trong $[0,4]$, nên mọi khoảng cách tổng quát hóa không quá $4$; cận $39{,}975$ vượt mức này nên không cho thông tin. Khoảng cách tổng quát hóa kì vọng thật là $0{,}4750$ (Ví dụ 06.3, Bước 5).

## 8. Đánh đổi giữa tối ưu và ổn định

Theo Mệnh đề 06.5(b), rủi ro vượt mức kì vọng không quá khoảng cách tổng quát hóa kì vọng cộng kì vọng của sai số tối ưu thực nghiệm. Với SGD có chiếu, cận của số hạng thứ hai giảm khi $T$ tăng (Định lý 05.14), còn cận của số hạng thứ nhất tăng (Hệ quả 08.7).

::: corollary Hệ quả 08.8 (Rủi ro vượt mức kì vọng của SGD nhiều vòng) — chứng minh đầy đủ (ở Phụ lục C)
**Giả thiết.** Bốn thành phần sau.

- **Mẫu.** $S\sim D^m$ theo dạng đầy đủ của (T1).
- **Hàm lỗi.** (T2), (S) và (G).
- **Tập tham số.** $W$ khác rỗng, đóng, lồi, bị chặn; $w_1\in W$; $R\ge\sup_{u\in W}\lVert w_1-u\rVert$.
- **Thuật toán.** Thuật toán 08.1 với độ dài bước hằng $0<\eta\le2/\beta$; đầu ra $\bar w_T$.

**Bảo đảm.** Theo kì vọng theo $(S,\xi)$, hai khẳng định.

**(a) Cận ghép.**
$$
\begin{aligned}
&\mathbb E_{S,\xi}L_D(\bar w_T)-\inf_WL_D\\
&\le\frac{R^2}{2\eta T}+\frac{\eta G^2}2+\frac{\eta G^2(T-1)}m .
\end{aligned}
$$

**(b) Độ dài bước tốt nhất với $T$ cho trước.** Đặt
$$
\eta^*=\frac R{G\sqrt{T+2T(T-1)/m}} .
$$
Nếu $\eta^*\le2/\beta$, vế phải của (a) tại $\eta=\eta^*$ bằng
$$
RG\sqrt{\frac{1+2(T-1)/m}T}.
$$
Giá trị này không quá $RG\sqrt{3/m}$ khi $T=m$, tiến về $RG\sqrt{2/m}$ khi $T\to\infty$, và giảm theo $T$ khi $m>2$.

Vế trái là rủi ro vượt mức kì vọng so với $W$, và cận không phụ thuộc $p$. Cận ở (b) luôn lớn hơn cận $RG/\sqrt{m+1}$ của một vòng qua dữ liệu với quan sát mới (Nhận xét 06.3): khoảng $\sqrt3$ lần khi $T=m$ và khoảng $\sqrt2$ lần khi $T\to\infty$.
:::

Ở Phụ lục C, ta cộng hai cận theo Mệnh đề 06.5(b): Hệ quả 08.7 chặn khoảng cách tổng quát hóa, Định lý 05.14 chặn sai số tối ưu; rồi ta chọn $\eta$ bằng bất đẳng thức trung bình cộng–trung bình nhân.

Ghép cận ổn định của điểm lặp cuối $w_{T+1}$ (Định lý 08.6) với Định lý 05.14 là sai, vì Định lý 05.14 chỉ chặn độ chênh tối ưu của $\bar w_T$. Với hàm không trơn của Ví dụ 05.12, điểm lặp cuối không hội tụ.

::: example Ví dụ 08.7 (Số vòng qua dữ liệu cho hồi quy logistic)
**Thiết lập.** Khối ứng dụng ở §3: $m=10^4$ (giả định), $G=1$, $\beta=\tfrac14$ (Ví dụ 08.5), $W$ là quả cầu bán kính $5$, $w_1=0$, nên $R=5$.

**Bước 1: một vòng.** Theo Nhận xét 06.3, cận là
$$
\frac{RG}{\sqrt{m+1}}=\frac5{\sqrt{10\,001}}\le0{,}0500 .
$$

**Bước 2: nhiều vòng với $\eta^*$.** Xét $T=10^4$ bước rút có hoàn lại; số bước bằng một vòng, nhưng thuật toán khác thuật toán theo thứ tự của Bước 1. Ta có $1+2\cdot9999/10^4=2{,}9998$, nên theo Hệ quả 08.8(b),
$$
\begin{aligned}
\eta^*&=\tfrac5{100}\cdot2{,}9998^{-1/2}\\
&\approx0{,}0289\le8,
\end{aligned}
$$
và cận là
$$
5\sqrt{2{,}9998/10^4}\le0{,}0866 .
$$
Cùng công thức cho $0{,}0791$ khi $T=2\cdot10^4$ và $0{,}0725$ khi $T=10^5$ (làm tròn lên). Khi $T\to\infty$, cận giảm về $5\sqrt{2\cdot10^{-4}}\le0{,}0708$.

**Bước 3: độ dài bước cố định $\eta=0{,}05$.** Vế phải của Hệ quả 08.8(a) là hàm của $T$:
$$
\frac{250}T+0{,}025+\frac{0{,}05(T-1)}{10^4}.
$$
Số hạng thứ nhất giảm, số hạng thứ ba tăng. Đạo hàm theo $T$ bằng $0$ khi $250/T^2=5\cdot10^{-6}$, tức $T^2=5\cdot10^7$ và $T^*=\frac{R\sqrt{m/2}}{\eta G}\approx7071$. Bảng ghi cận (làm tròn lên) tại một số giá trị của $T$.

| $T$ | Cận |
|---|---|
| $5000$ | $0{,}1000$ |
| $7071$ | $0{,}0958$ |
| $10^4$ | $0{,}1000$ |
| $2\cdot10^4$ | $0{,}1375$ |
| $5\cdot10^4$ | $0{,}2800$ |

**Kết luận.** Theo các cận này, chạy nhiều vòng trên $10^4$ hồ sơ không cho cận nhỏ hơn một vòng ($0{,}0708$ so với $0{,}0500$). Với $\eta=0{,}05$, cận nhỏ nhất ở khoảng $7071<m$ bước, tức trước khi hết một vòng. Số bước $T^*$ làm nhỏ nhất tổng hai cận trên; nó không chứng minh rằng lỗi kiểm tra nhỏ nhất ở đó.
:::

Ở Ví dụ 08.7, số bước được chọn theo một cận. Chọn số bước, thêm số hạng phạt và để quá trình huấn luyện tự chọn nghiệm là ba cách khác nhau điều khiển đầu ra của một thuật toán huấn luyện.

::: definition Định nghĩa 08.9 (Dừng sớm, chính quy hóa tường minh và chính quy hóa ngầm)
Cho một thuật toán huấn luyện lặp, chẳng hạn Thuật toán 08.1, trên mẫu $s$. Định nghĩa gồm ba thành phần.

- **Dừng sớm.** *Dừng sớm* (early stopping) là chọn số bước $T$ nhỏ hơn số bước cần để đưa sai số tối ưu thực nghiệm về gần $0$. Số bước được chọn trước khi chạy, hoặc chọn bằng một mẫu xác thực độc lập với $s$; đầu ra là điểm lặp tại bước dừng.
- **Chính quy hóa tường minh.** *Chính quy hóa tường minh* (explicit regularization) là thêm một số hạng phạt vào hàm mục tiêu, như $\tfrac\lambda2\lVert w\rVert^2$ trong Định nghĩa 06.6.
- **Chính quy hóa ngầm.** *Chính quy hóa ngầm* (implicit regularization) là việc các lựa chọn của quá trình huấn luyện (khởi tạo, độ dài bước, số bước, cách rút chỉ số) quyết định điểm được trả về khi nhiều điểm của $W$ có rủi ro thực nghiệm nhỏ như nhau, không qua một số hạng phạt.
:::

Học phần có một lập luận cho một trường hợp: hạ gradient trên hàm lỗi bình phương, khởi tạo tại $0$, với độ dài bước đủ nhỏ, hội tụ tới nghiệm nội suy chuẩn nhỏ nhất khi nghiệm nội suy tồn tại (Phụ lục D của Bài 07). Trong Định lý 08.6, ngân sách độ dài bước đóng vai của $1/\lambda$ trong Mệnh đề 06.11; đây chỉ là một gợi ý về dạng công thức.

Trong các thời điểm đo của thí nghiệm mở đầu, hàm lỗi logistic trên mẫu kiểm tra nhỏ nhất ở $5$ vòng ($0{,}589$; ở $10$ vòng là $0{,}603$, Phụ lục F). Lỗi phân lớp trên mẫu kiểm tra gần như không đổi từ $5$ đến $100$ vòng ($0{,}309$; $0{,}301$; $0{,}312$ ở $5$, $20$, $100$ vòng). Số bước tốt nhất vì vậy phụ thuộc vào hàm lỗi dùng để chọn.

Số bước và độ dài bước đi vào cận rủi ro qua hai số hạng ngược chiều. Chọn chúng để làm nhỏ nhất tổng là làm nhỏ nhất một cận trên, và mọi kết luận về số bước ở trên cần hàm lỗi lồi, trơn.

## 9. Khi bỏ tính lồi hoặc tính trơn

Trong chứng minh Định lý 08.6, tính lồi của hàm lỗi, tính trơn và điều kiện $\eta_t\le2/\beta$ chỉ đi vào qua Bổ đề 08.4, tức qua các bước chung. Ba ví dụ dưới đây lần lượt bỏ tính lồi, điều kiện độ dài bước và tính trơn, và giữ các giả thiết còn lại; ví dụ cuối cũng xét mạng ReLU, nơi tính lồi, tính trơn và (G) đều không thỏa.

::: example Ví dụ 08.8 (Bỏ tính lồi: hàm lỗi cosin)
**Thiết lập.** Cho $\mathcal Z=\mathbb R$, $W=\mathbb R$ và $\ell(w,z)=1+\cos(w-z)$, nhận giá trị trong $[0,2]$. Mẫu có $m=100$ quan sát, mọi $z_j=0$; quan sát thay thế là $z'=0{,}01$ ở một chỉ số $i$. Lấy $w_1=w'_1=0$, $\eta=0{,}1$, và một dãy chỉ số với $i_1=i$ và $i_t\ne i$ với mọi $t\ge2$; quỹ đạo là tất định.

**Bước 1: tính lồi, $\beta$ và $G$.** Đạo hàm theo $w$ là $-\sin(w-z)$, có trị tuyệt đối không quá $1$, nên (G) đúng với $G=1$. Đạo hàm bậc hai là $-\cos(w-z)\in[-1,1]$, nên hàm lỗi $1$-trơn. Đạo hàm bậc hai âm gần $w=z$, nên hàm lỗi không lồi.

**Bước 2: lần chạy trên $s$.** Đạo hàm tại $w=0$ với $z=0$ bằng $0$, nên $w_t=0$ với mọi $t$. Điểm $w=0$ là một điểm dừng (stationary point) của $L_s$, và là điểm cực đại của nó, với $L_s(0)=2$.

**Bước 3: bước khác biệt.** Lần chạy thứ hai dùng $z'$ ở bước $1$:
$$
\begin{aligned}
w'_2&=0+0{,}1\sin(0-0{,}01)\\
&\approx-0{,}0010,
\end{aligned}
$$
nên $\Delta_2\approx0{,}0010\le2G\eta=0{,}2$.

**Bước 4: các bước chung.** Từ bước $2$, $w'_{t+1}=w'_t+0{,}1\sin w'_t$. Khi $w'_t$ gần $0$, $\sin w'_t\approx w'_t$, nên khoảng cách nhân khoảng $1+\beta\eta=1{,}1$ sau mỗi bước; tính trực tiếp, $\Delta_3/\Delta_2\approx1{,}1000$. Tiếp tục, ta có $\Delta_{21}\approx0{,}0061$, $\Delta_{41}\approx0{,}0411$, $\Delta_{61}\approx0{,}2753$, $\Delta_{81}\approx1{,}529$ và $\Delta_{101}\approx2{,}879$. Giá trị đầu tiên vượt $0{,}2$ là $\Delta_{58}\approx0{,}207$. Sau đó $w'_t\to-\pi$, điểm cực tiểu của $L_s$, nên $\Delta_t\to\pi$.

**Bước 5: so với cận lồi.** Quỹ đạo chỉ có một bước khác biệt. Nếu phần (a) của Mệnh đề 08.5 đúng ở đây, nó cho $\Delta_t\le0{,}2$ với mọi $t$. Với $T$ lớn, tại quan sát kiểm tra $z=0$, hàm lỗi của hai đầu ra là $2$ và gần $0$; hiệu gần $2$, bằng độ rộng của miền giá trị.

**Kết luận.** Khi bỏ tính lồi, các bước chung đẩy hai lần chạy ra xa, và hai lần chạy hội tụ tới hai điểm khác nhau, $0$ và $-\pi$. Bổ đề 08.4 là bước không còn đúng.
:::

::: proposition Mệnh đề 08.10 (Bất đẳng thức truy hồi khi bỏ tính lồi) — phác thảo (ở Phụ lục D)
**Giả thiết.** Như Mệnh đề 08.5, với hai thay đổi.

- **Hàm lỗi.** Với mọi $z$, $\ell(\cdot,z)$ là $\beta$-trơn trên $\mathbb R^p$, không cần lồi; (G) với hằng số $G$.
- **Độ dài bước.** $\eta_t>0$ bất kì, tất định.

**Bảo đảm.** Ba khẳng định.

**(a) Hệ số giãn.** Ánh xạ $\operatorname{proj}_W\circ\Gamma_{\eta,z}$ có hệ số giãn $1+\beta\eta$. Hằng số này không giảm được, kể cả khi (G) đúng: với hàm lỗi cosin của Ví dụ 08.8 ($\beta=1$, $W=\mathbb R$), đạo hàm của ánh xạ bước $w\mapsto w+\eta\sin(w-z)$ là $1+\eta\cos(w-z)$, bằng $1+\eta$ tại $w=z$.

**(b) Trên từng quỹ đạo.** Với mọi giá trị của $\xi$ và mọi $t$,
$$
\begin{aligned}
\Delta_{t+1}&\le(1+\beta\eta_t)\Delta_t\\
&\quad+2G\eta_t\,\mathbb 1[i_t=i].
\end{aligned}
$$

**(c) Theo kì vọng theo $\xi$.**
$$
\begin{aligned}
&\mathbb E\Delta_{T+1}\\
&\le\frac{2G}m\sum_{t=1}^T\eta_t\prod_{k=t+1}^T(1+\beta\eta_k)\\
&\le\frac{2G}m\sum_{t=1}^T\eta_t\,e^{\beta\sum_{k=t+1}^T\eta_k}.
\end{aligned}
$$
Với độ dài bước hằng, vế phải thứ nhất bằng $\frac{2G}{m\beta}\big((1+\beta\eta)^T-1\big)$.
:::

Ta chứng minh mệnh đề (phác thảo ở Phụ lục D) bằng cách dùng (a) thay cho Bổ đề 08.4 ở bước chung, giữ Bước 2 của chứng minh Mệnh đề 08.5 ở bước khác biệt vì bước đó không dùng tính lồi, rồi lấy kì vọng và khai triển bất đẳng thức truy hồi.

Thừa số $\prod_k(1+\beta\eta_k)$ trong (c) tăng theo hàm mũ khi độ dài bước hằng. Với $\beta=1$, $\eta=0{,}1$, $T=100$ và $m=100$, ta có $(1{,}1)^{100}\approx1{,}378\cdot10^4$, nên vế phải của (c) là $\tfrac2{100}\big((1{,}1)^{100}-1\big)\approx275{,}6$. Nhân với $G=1$, cận cho hiệu hàm lỗi tại một quan sát kiểm tra cũng là khoảng $275{,}6$, trong khi hàm lỗi cosin chỉ nhận giá trị trong $[0,2]$. Với $\eta_t=c/t$, trong đó $c>0$ là một hằng số,
$$
\begin{aligned}
\prod_{k=t+1}^T\Big(1+\frac{\beta c}k\Big)&\le e^{\beta c\sum_{k=t+1}^T1/k}\\
&\le\Big(\frac Tt\Big)^{\beta c},
\end{aligned}
$$
tăng theo đa thức của $T$; vì vậy các kết quả không lồi dùng độ dài bước giảm.

::: remark Nhận xét 08.11 (Cận ổn định cho hàm lỗi không lồi bị chặn) — đọc thêm
Hardt, Recht và Singer (2016, Định lý 3.12) chứng minh cận sau, viết theo kí hiệu của học phần.

**Giả thiết.** Ba thành phần sau.

- **Hàm lỗi.** Với mọi $z$, $\ell(\cdot,z)$ nhận giá trị trong $[0,1]$, là $G$-Lipschitz và $\beta$-trơn trên $\mathbb R^p$.
- **Độ dài bước.** $\eta_t$ không tăng và $\eta_t\le c/t$, với một hằng số $c>0$.
- **Thuật toán.** SGD không chiếu, $T$ bước, chỉ số rút đều có hoàn lại.

**Bảo đảm.** Thuật toán ổn định đều với
$$
\begin{aligned}
\epsilon_{\mathrm{stab}}(m)&\le T^{\frac{\beta c}{\beta c+1}}(2cG^2)^{\frac1{\beta c+1}}\\
&\quad\times\frac{1+1/(\beta c)}{m-1} .
\end{aligned}
$$
So với Định lý 08.6, cận cần thêm hai giả thiết: hàm lỗi bị chặn và độ dài bước giảm như $c/t$. Chứng minh dùng một *giai đoạn đầu* (burn-in) gồm $t_0$ bước; trong giai đoạn này, quan sát khác biệt được dùng với xác suất không quá $t_0/m$. Với $\beta=10$, $c=1$, $G=1$, $m=10^4$ và $T=10^6$, vế phải không quá $33{,}37$, lớn hơn $1$, nên không cho thông tin với hàm lỗi trong $[0,1]$.
:::

Không có tính lồi, SGD vẫn có một bảo đảm tối ưu, nhưng cho một đại lượng yếu hơn sai số tối ưu thực nghiệm.

::: proposition Mệnh đề 08.12 (Điểm dừng xấp xỉ của SGD trên hàm mục tiêu trơn) — đọc thêm (chứng minh ở Phụ lục E)
**Giả thiết.** Bốn thành phần sau.

- **Hàm mục tiêu.** $F:\mathbb R^p\to\mathbb R$ là $\beta$-trơn, không cần lồi, với $F_*=\inf F>-\infty$.
- **Gradient ngẫu nhiên.** Với lịch sử $\mathcal F_{t-1}$ như Định nghĩa 05.10, $\mathbb E[g_t\mid\mathcal F_{t-1}]=\nabla F(w_t)$ và $\mathbb E\big[\lVert g_t-\nabla F(w_t)\rVert^2\mid\mathcal F_{t-1}\big]\le\sigma^2$.
- **Thuật toán.** $w_{t+1}=w_t-\eta g_t$ với $W=\mathbb R^p$, $w_1$ tất định và $0<\eta\le1/\beta$.
- **Khả tích.** $\mathbb E\lvert F(w_t)\rvert<\infty$ với mọi $t$; điều này đúng khi nguồn ngẫu nhiên có hữu hạn giá trị, như khi rút chỉ số từ một mẫu.

**Bảo đảm.** Theo kì vọng theo nguồn ngẫu nhiên của các gradient,
$$
\begin{aligned}
&\frac1T\sum_{t=1}^T\mathbb E\lVert\nabla F(w_t)\rVert^2\\
&\le\frac{2(F(w_1)-F_*)}{\eta T}+\beta\eta\sigma^2 .
\end{aligned}
$$
Vế trái bằng $\mathbb E\lVert\nabla F(w_\tau)\rVert^2$ với $\tau$ rút đều trên $\{1,\ldots,T\}$, độc lập với các gradient. Mệnh đề chặn *tính dừng* (stationarity), tức độ lớn của gradient. Điểm $w_\tau$ là một *điểm dừng xấp xỉ* (approximate stationary point) theo nghĩa $\mathbb E\lVert\nabla F(w_\tau)\rVert^2$ không quá vế phải. Mệnh đề không chặn sai số tối ưu, rủi ro vượt mức hay khoảng cách tổng quát hóa, và không nói về $w_{T+1}$.
:::

Với hồi quy logistic, $F=L_s$ và $W=\mathbb R^p$, ta có $\beta=\tfrac14$, $F(0)-F_*\le\ln2$ vì $F\ge0$, và $\sigma^2\le1$ vì $\mathbb E\lVert g-\nabla F\rVert^2\le\mathbb E\lVert g\rVert^2\le G^2=1$. Với $w_1=0$, $\eta=0{,}05$ và $T=10^4$, vế phải là $\frac{2\ln2}{500}+0{,}0125\le0{,}0153$. Trong Ví dụ 08.8, $w=0$ là điểm dừng với $L_s(0)=2$, giá trị lớn nhất; khi hàm không lồi, gradient nhỏ không kéo theo rủi ro thực nghiệm nhỏ.

Hai ví dụ cuối trở lại hàm lỗi lồi và bỏ điều kiện độ dài bước hoặc tính trơn.

::: example Ví dụ 08.9 (Độ dài bước vượt $2/\beta$)
**Thiết lập.** Hàm lỗi Huber của Ví dụ 08.1 ($\beta=G=1$, lồi), $W=\mathbb R$, mẫu $s=(0,0,0,\tfrac1{100})$ và mẫu lân cận $s^{(4)}=(0,0,0,-\tfrac1{100})$. Lấy $w_1=w'_1=0$ và dãy chỉ số $i_1=4$, rồi $i_t=1$ với $t\ge2$; quỹ đạo là tất định.

**Bước 1: $\eta=1$.** Bước khác biệt cho $w_2=0{,}01$ và $w'_2=-0{,}01$, nên $\Delta_2=0{,}02$. Bước chung với $z=0$ là $w\mapsto w-1\cdot w=0$, nên $\Delta_t=0$ từ $t=3$.

**Bước 2: $\eta=2=2/\beta$.** Ta có $\Delta_2=0{,}04$. Bước chung là $w\mapsto-w$, nên $w_t$ đổi dấu ($\pm\tfrac1{50}$) và $\Delta_t=0{,}04$ không đổi.

**Bước 3: $\eta=3$.** Ta có $\Delta_2=0{,}06$. Khi $\lvert w\rvert\le1$, bước chung là $w\mapsto w-3w=-2w$, nên
$$
\begin{aligned}
&\Delta_2,\ldots,\Delta_8\\
&=0{,}06;\,0{,}12;\,0{,}24;\,0{,}48;\\
&\quad\ 0{,}96;\,1{,}92;\,3{,}84 .
\end{aligned}
$$
Sau đó $\lvert w_t\rvert>1$ và điểm lặp ra khỏi vùng bậc hai của hàm lỗi.

**Kết luận.** Mọi giả thiết khác của Mệnh đề 08.5 vẫn đúng; chỉ điều kiện $\eta\le2/\beta$ bị bỏ. Khi đó các bước chung nhân khoảng cách với $\lvert1-\eta\beta\rvert=2$, đúng hệ số giãn nhỏ nhất ở Ví dụ 08.3.
:::

::: example Ví dụ 08.10 (Hàm lỗi không trơn và mạng ReLU)
**Thiết lập.** Ba trường hợp không trơn: hai hàm lỗi lồi một chiều với $W=\mathbb R$, rồi hàm lỗi của một mạng ReLU.

**Bước 1: giá trị tuyệt đối.** Hàm $\ell(w,z)=\lvert w-z\rvert$ lồi, $1$-Lipschitz và không khả vi tại $w=z$. Xét hai điểm $\pm0{,}01$ và một bước chung với $z=0$, $\eta=\tfrac12$. Đạo hàm là $\pm1$ tại hai điểm, nên $0{,}01\mapsto-0{,}49$ và $-0{,}01\mapsto0{,}49$; khoảng cách tăng từ $0{,}02$ lên $0{,}98$. Mỗi bước chung có thể tăng khoảng cách gần $2G\eta$, nên Mệnh đề 08.5 không còn thừa số $1/m$.

**Bước 2: hàm lỗi bản lề.** Với $\ell(w,(x,y))=\max\{0,1-\tilde y\,wx\}$, $x=\tilde y=1$ và $\eta=\tfrac12$, một bước chung đưa $0{,}99$ tới $1{,}49$ và giữ nguyên $1{,}01$, nên khoảng cách tăng từ $0{,}02$ lên $0{,}48$.

**Bước 3: mạng ReLU.** Xét mạng của Định nghĩa 07.1 với hàm kích hoạt ReLU và mọi trọng số được huấn luyện, hàm lỗi logistic theo véc-tơ tham số $\theta$.

- **Tính trơn.** Hàm lỗi không khả vi theo $\theta$ tại các tham số có một tiền kích hoạt (pre-activation), tức một tọa độ của $\Theta_1x+b_1$, bằng $0$ và trọng số ra tương ứng khác $0$; do đó nó không $\beta$-trơn.
- **Tính lồi.** Đổi chỗ hai nơ-ron ẩn cho cùng một hàm, còn trung điểm của hai tham số có thể cho hàm mục tiêu lớn hơn; Bài tập 07.5(c) chỉ ra điều này với hàm mục tiêu bình phương. Hàm mục tiêu của mạng ReLU vì vậy nói chung không lồi theo $\theta$.
- **Cận gradient.** Gradient theo ma trận trọng số lớp ẩn $\Theta_1$ tỉ lệ với độ lớn của ma trận lớp ra $\Theta_2$ và ngược lại (Định nghĩa 07.1), nên không có $G$ đều trên toàn không gian tham số khi trọng số không bị chặn.

**Kết luận.** Áp dụng Định lý 08.6 nguyên văn cho mạng ReLU huấn luyện mọi lớp nơ-ron là sai. Định lý áp dụng khi lớp ẩn cố định và chỉ lớp ra được huấn luyện bằng SGD trên hàm lỗi logistic, như mạng của Ví dụ 07.3. Khi đó hàm lỗi lồi và trơn theo trọng số lớp ra, với $G=\sup_x\lVert\chi(x)\rVert$ (hữu hạn với véc-tơ đặc trưng ngẫu nhiên $\chi(x)$ của Ví dụ 07.3) và $\beta=G^2/4$.
:::

Mạng ReLU huấn luyện mọi lớp nơ-ron không thỏa giả thiết của Định lý 08.6, Mệnh đề 08.10 hay Nhận xét 08.11, vì hàm lỗi không trơn. Với các mạng này, học phần không có cận ổn định.

## 10. Ý nghĩa, tác động và giới hạn

Với hàm lỗi lồi, trơn, có gradient bị chặn, thuật toán ảnh hưởng tới khoảng cách tổng quát hóa qua ngân sách độ dài bước: SGD ổn định đều với hệ số $\frac{2G^2}m\sum_t\eta_t$ (Định lý 08.6). Trong thí nghiệm mở đầu, cận này là $t/200$, còn khoảng cách đo được tăng từ $0{,}045$ lên $0{,}919$ (câu hỏi mở đầu).

Độ dài bước và số bước đi vào cận qua cùng một tổng, và điểm lặp trung bình giảm số hạng ổn định hơn một nửa (Hệ quả 08.7). Với $10^4$ hồ sơ, theo các cận, chạy nhiều vòng không cho cận nhỏ hơn một vòng ($0{,}0708$ so với $0{,}0500$, Ví dụ 08.7); dừng sớm theo Hệ quả 08.8 chỉ làm nhỏ nhất một tổng hai cận trên.

Các khẳng định của bài thuộc ba mức.

- **Chứng minh được.** Định lý 08.6, Hệ quả 08.7 và 08.8 cho hàm lỗi lồi, trơn, gồm hồi quy logistic và lớp ra của mạng với lớp ẩn cố định.
- **Lý thuyết không lồi bổ sung.** Mệnh đề 08.10 (tăng theo hàm mũ với độ dài bước hằng), Nhận xét 08.11 (cần hàm lỗi bị chặn và $\eta_t\le c/t$), Mệnh đề 08.12 (chỉ tính dừng).
- **Giả thuyết thực nghiệm.** Hardt, Recht và Singer (2016, §6) thấy khoảng cách giữa hai lần chạy và khoảng cách tổng quát hóa của mạng sâu tăng theo thời gian huấn luyện. Tiêu đề bài báo, "huấn luyện nhanh hơn thì tổng quát hóa tốt hơn", chưa có chứng minh cho mạng sâu; chính quy hóa ngầm trong mạng sâu cũng là giả thuyết.

Các kết quả của bài có năm giới hạn.

- **Theo kì vọng.** Không có cận với xác suất cao, và không chặn $\mathbb E\lvert L_D-L_S\rvert$.
- **Độ chặt.** Cận tăng tuyến tính theo ngân sách độ dài bước, còn các đại lượng đo được trong thí nghiệm tăng chậm hơn (Ví dụ 08.6).
- **Tính trơn và tính lồi.** Hàm lỗi bản lề và mạng ReLU không thỏa (Ví dụ 08.10).
- **Cận gradient đều.** Hàm lỗi bình phương cần $W$ bị chặn và dữ liệu bị chặn.
- **Rủi ro kì vọng.** Định lý 08.6 không chặn $L_D$; cần thêm số hạng tối ưu, và trong học phần số hạng này chỉ có cho điểm lặp trung bình (Định lý 05.14, Hệ quả 08.8).

Hệ quả 07.16 đúng với xác suất ít nhất $1-\delta$ cho mọi hàm của một lớp chọn trước mẫu và không cần tính lồi. Định lý 08.6 đúng theo kì vọng cho một thuật toán, cần tính lồi và tính trơn, nhưng không cần $W$ bị chặn và không phụ thuộc $p$.

## 11. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 08](material-viewer.html?doc=materials/lec-08/exercises.md); cả tám bài là bài gốc. Không có bài từ UML: các bài phù hợp của chương 12–14 đã dùng ở Bài 05–06, và các bài tập ở §20.9 không có bài về SGD hay tính ổn định.

1. **Bài tập 08.1** (Bất đẳng thức truy hồi và thừa số $1/m$): mục tiêu 1, 3.
2. **Bài tập 08.2** (Ngân sách độ dài bước của ba lịch độ dài bước): mục tiêu 3, 4.
3. **Bài tập 08.3** (Bước chứng minh không còn đúng khi bỏ tính lồi): mục tiêu 2, 5.
4. **Bài tập 08.4** (Gradient nhỏ, rủi ro thực nghiệm nhỏ và rủi ro kì vọng nhỏ): mục tiêu 5.
5. **Bài tập 08.5** (Kiểm tra giả thiết cho một thiết lập huấn luyện mạng ReLU): mục tiêu 5.
6. **Bài tập 08.6** (Thực nghiệm tùy chọn: hai lần chạy ghép cặp theo thời gian): mục tiêu 5.
7. **Bài tập 08.7** (SGD có chiếu nhiều vòng cho hồi quy bình phương): mục tiêu 3.
8. **Bài tập 08.8** (Số bước tốt nhất với độ dài bước cố định): mục tiêu 4.

## 12. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Xét hồi quy logistic với $\lVert x\rVert\le1$ trên toàn $\mathcal X$, $W=\mathbb R^p$ và $m=5000$ quan sát độc lập cùng phân bố. SGD theo Thuật toán 08.1 chạy $T=20\,000$ bước, tức bốn vòng qua dữ liệu, từ $w_1=0$.

(a) Với $\eta_t=0{,}1$ cho mọi $t$, tính cận của Định lý 08.6 cho khoảng cách tổng quát hóa kì vọng của điểm lặp cuối.

(b) Với $\eta_t=0{,}1/\sqrt t$, dùng $\sum_{t=1}^Tt^{-1/2}\le2\sqrt T-1$ để tính lại cận.

(c) Cận ở (a) có chặn hiệu giữa tỉ lệ lỗi phân lớp trên mẫu kiểm tra và trên mẫu huấn luyện không?

(d) Thay hàm lỗi logistic bằng hàm lỗi bản lề, hoặc thay mô hình tuyến tính bằng một mạng ReLU hai lớp nơ-ron với mọi trọng số được huấn luyện. Cận ở (a) còn có căn cứ không? Chỉ ra giả thiết không thỏa.

::: solution Lời giải câu hỏi cuối buổi
**(a)** Theo Ví dụ 08.5, $G=1$ và $\beta=\tfrac14$; điều kiện $\eta_t=0{,}1\le8$ thỏa. Ngân sách độ dài bước là $0{,}1\cdot20\,000=2000$, nên cận là
$$
\frac{2\cdot1\cdot2000}{5000}=0{,}8 .
$$

**(b)** Ngân sách độ dài bước thỏa
$$
\begin{aligned}
\sum_{t=1}^T\eta_t&\le0{,}1\big(2\sqrt{20\,000}-1\big)\\
&\le28{,}19 .
\end{aligned}
$$
Điều kiện $\eta_t\le0{,}1\le8$ vẫn thỏa. Cận là
$$
\frac{2\cdot1\cdot28{,}19}{5000}\le0{,}0113 .
$$

**(c)** Không. Định lý chặn khoảng cách tổng quát hóa kì vọng của hàm lỗi logistic, theo kì vọng theo $(S,\xi)$. Hàm lỗi 0–1 không Lipschitz theo $w$, nên cận không chuyển sang tỉ lệ lỗi phân lớp; và định lý không cho cận với xác suất cao.

**(d)** Không. Hàm lỗi bản lề không khả vi tại lề $1$, nên không thỏa (S); một bước chung có thể làm tăng khoảng cách (Ví dụ 08.10, Bước 2). Mạng ReLU huấn luyện mọi lớp nơ-ron không thỏa (S), vì hàm lỗi không trơn và không lồi theo tham số, và không có $G$ đều (Ví dụ 08.10, Bước 3). Định lý không áp dụng, nên con số $0{,}8$ không có căn cứ; điều đó không có nghĩa là khoảng cách thật lớn.
:::

Hàm lỗi logistic bằng $-\ln$ của xác suất mà mô hình gán cho nhãn quan sát được, tức là hàm lỗi log của một mô hình xác suất có điều kiện (đoạn sau Nhận xét 02.11). Các kết quả của bài giả sử các quan sát độc lập, mỗi quan sát là một điểm $z$ (với hồi quy logistic, một cặp $(x,y)$), và hàm lỗi lồi, trơn, có gradient bị chặn theo tham số. Câu hỏi cho Bài 09 là: khi mỗi quan sát là một chuỗi có các phần tử phụ thuộc nhau và hàm lỗi là $-\ln$ độ hợp lý (likelihood) của cả chuỗi, rủi ro kì vọng, rủi ro thực nghiệm và giả thiết độc lập được viết lại như thế nào?

## 13. Tài liệu đọc

- **Trước buổi học:** UML §13.1–13.2 (ERM có chính quy hóa; quy tắc ổn định không quá khớp), đã dùng ở Bài 06; UML §20.6 (SGD và lan truyền ngược; mỗi bước dùng một quan sát mới từ $D$; không có định lý ổn định).
- **Sau buổi học:** M. Hardt, B. Recht, Y. Singer (2016), *Train faster, generalize better: Stability of stochastic gradient descent*, ICML: §2 (định nghĩa ổn định, quy tắc cập nhật), §3.1–3.3 (hàm trơn và lồi, Định lý 3.8), Phụ lục A (chứng minh Bổ đề 3.7 từ tính đồng bức); phần thảo luận ở §1 và §5.
- **Mở rộng:** cùng bài báo, §3.5 (phân tích không lồi, Định lý 3.12), §4 (suy giảm trọng số, cắt gradient, dropout), §6 (thí nghiệm trên mạng sâu, là quan sát thực nghiệm), §7 (câu hỏi mở); Mệnh đề 08.12 và Phụ lục E; UML §31.1 (cận PAC-Bayes), một hướng khác để chặn khoảng cách tổng quát hóa.

**Quan hệ với nguồn.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục, bài báo của Hardt, Recht và Singer theo mục và số định lý của bài báo. Các khác biệt chính:

- **Kí hiệu và chỉ số.** Bài báo viết $n$, $L$, $\alpha_t$, $\delta_t$ cho cỡ mẫu, hằng số Lipschitz, độ dài bước và khoảng cách giữa hai lần chạy; học phần viết $m$, $G$, $\eta_t$, $\Delta_t$, vì $L$ là rủi ro và $\delta$ là xác suất thất bại. Bài báo bắt đầu từ $w_0$ và gọi điểm lặp sau $T$ bước là $w_T$; học phần đánh số từ $w_1$ như Bài 05, nên $T$ bước cho $w_{T+1}$. Cận của Định lý 3.8 và của Định lý 08.6 cùng dạng $\frac{2G^2}m\sum_{t=1}^T\eta_t$.
- **Phép chiếu.** Định lý 3.8 của bài báo xét SGD không chiếu; học phần thêm phép chiếu lên $W$ đóng, lồi để dùng cùng thuật toán với Bài 05–06.
- **Lập luận truy hồi.** Bài báo chia hai trường hợp theo quan sát được chọn rồi dùng tính tuyến tính của kì vọng, và nêu kết quả cho cả rút đều lẫn hoán vị ngẫu nhiên. Học phần viết bất đẳng thức trên từng quỹ đạo trước (Mệnh đề 08.5(a)), nên chỉ cần $\Pr(i_t=i)=1/m$ (Phụ lục B).
- **Tính đồng bức.** Bài báo dẫn tài liệu tối ưu; học phần chứng minh ở Phụ lục A.
- **Ghép với sai số tối ưu.** §5 của bài báo so với kì vọng của cực tiểu rủi ro thực nghiệm; Hệ quả 08.8 so với $\inf_WL_D$ qua Mệnh đề 06.5 và Hệ quả 08.7. Hai cách cho cùng hai thừa số $\sqrt3$ và $\sqrt2$ so với cận một vòng; bài báo đọc chúng như mức chênh tối đa.

## Phụ lục

### A. Tính đồng bức và tính không giãn

Chứng minh phần (a) của Bổ đề 08.4 dựa trên *cận trên bậc hai* (còn gọi là bổ đề hạ; quadratic upper bound, descent lemma) của một hàm trơn.

::: proof Chứng minh Bổ đề 08.4(a)
**Lộ trình.** Chứng minh cận trên bậc hai của hàm trơn, áp dụng nó cho một hàm phụ đạt cực tiểu toàn cục, rồi đổi vai hai điểm và cộng lại. Bất đẳng thức then chốt là
$$
\begin{aligned}
&f(v)-f(u)\\
&\ge\langle\nabla f(u),v-u\rangle\\
&\quad+\tfrac1{2\beta}\lVert\nabla f(v)-\nabla f(u)\rVert^2 .
\end{aligned}
$$

**Bước 1 (cận trên bậc hai; tính trơn).** Gradient của $f$ là $\beta$-Lipschitz nên liên tục, và hàm $r\mapsto f(u+r(v-u))$ khả vi liên tục trên $[0,1]$. Đặt $g_r=\nabla f(u+r(v-u))-\nabla f(u)$; theo tính trơn, $\lVert g_r\rVert\le\beta r\lVert v-u\rVert$. Theo công thức tích phân dọc đoạn thẳng từ $u$ tới $v$ và bất đẳng thức Cauchy–Schwarz,
$$
\begin{aligned}
&f(v)-f(u)-\langle\nabla f(u),v-u\rangle\\
&=\int_0^1\langle g_r,v-u\rangle\,dr\\
&\le\int_0^1\beta r\lVert v-u\rVert^2\,dr\\
&=\tfrac\beta2\lVert v-u\rVert^2 .
\end{aligned}
$$
Bất đẳng thức này đúng với mọi hàm $\beta$-trơn, không cần lồi.

**Bước 2 (hàm phụ; tính lồi được dùng ở đây).** Cố định $u$ và đặt $q_u(v)=f(v)-\langle\nabla f(u),v\rangle$. Hàm $q_u$ lồi (hàm lồi trừ một hàm tuyến tính), $\beta$-trơn (gradient $\nabla f(v)-\nabla f(u)$ là $\beta$-Lipschitz theo $v$), và $\nabla q_u(u)=0$. Vì $q_u$ lồi và khả vi, bất đẳng thức dưới gradient tại $u$ cho $q_u(v)\ge q_u(u)+\langle\nabla q_u(u),v-u\rangle=q_u(u)$ với mọi $v$, nên $u$ là điểm cực tiểu toàn cục của $q_u$ trên $\mathbb R^p$. Đây là dòng duy nhất của chứng minh dùng tính lồi của $f$. Với $f(w)=-\tfrac12w^2$, hàm $q_u(v)=-\tfrac12v^2+uv$ không có cực tiểu (Bài tập 08.3).

**Bước 3 (áp dụng Bước 1 cho $q_u$).** Đặt $v^+=v-\tfrac1\beta\nabla q_u(v)$. Theo Bước 2 rồi Bước 1 cho $q_u$ tại hai điểm $v$ và $v^+$,
$$
\begin{aligned}
q_u(u)&\le q_u(v^+)\\
&\le q_u(v)-\tfrac1\beta\lVert\nabla q_u(v)\rVert^2\\
&\quad+\tfrac\beta2\cdot\tfrac1{\beta^2}\lVert\nabla q_u(v)\rVert^2\\
&=q_u(v)-\tfrac1{2\beta}\lVert\nabla q_u(v)\rVert^2 .
\end{aligned}
$$
Điểm $v^+$ có thể nằm ngoài $W$, nên (S) cần đúng trên toàn $\mathbb R^p$. Thay $q_u(u)=f(u)-\langle\nabla f(u),u\rangle$, $q_u(v)=f(v)-\langle\nabla f(u),v\rangle$ và $\nabla q_u(v)=\nabla f(v)-\nabla f(u)$, ta được bất đẳng thức then chốt.

**Bước 4 (đổi vai).** Đổi vai $u$ và $v$ trong bất đẳng thức then chốt:
$$
\begin{aligned}
&f(u)-f(v)\\
&\ge\langle\nabla f(v),u-v\rangle\\
&\quad+\tfrac1{2\beta}\lVert\nabla f(u)-\nabla f(v)\rVert^2 .
\end{aligned}
$$
Cộng hai bất đẳng thức, các giá trị $f(u)$, $f(v)$ triệt tiêu, và
$$
\begin{aligned}
&\langle\nabla f(u)-\nabla f(v),u-v\rangle\\
&\ge\tfrac1\beta\lVert\nabla f(u)-\nabla f(v)\rVert^2 .
\end{aligned}
$$

$\square$ Với hàm lồi, tính $\beta$-trơn và tính $\tfrac1\beta$-đồng bức tương đương; chiều kia ở đoạn sau Định nghĩa 08.3.
:::

### B. Chi tiết cho bất đẳng thức truy hồi

**(i) Xáo trộn lại sau mỗi vòng qua dữ liệu.** Giả sử $m$ chia hết $T$, và mỗi vòng $(i_{km+1},\ldots,i_{(k+1)m})$, $k=0,\ldots,T/m-1$, là một hoán vị đều của $\{1,\ldots,m\}$, độc lập giữa các vòng. Với bước $t$ ở vị trí thứ $j$ của một vòng, $i_t$ là phần tử thứ $j$ của một hoán vị đều; theo tính đối xứng, $\Pr(i_t=i)=1/m$. Mệnh đề 08.5(a) đúng trên từng quỹ đạo và không dùng phân bố của $\xi$; phần (b) chỉ dùng xác suất biên. Cùng lập luận đối xứng áp dụng khi một hoán vị đều được rút một lần rồi dùng lại ở mọi vòng. Do đó cả hai phần đúng, và Định lý 08.6 đúng với cùng cận, vì Định nghĩa 05.18 cho phép $\xi$ là một dãy ngẫu nhiên bất kì độc lập với $S$. Định nghĩa 05.10 đòi các lần rút độc lập, nên Định lý 05.14 không áp dụng nguyên văn cho xáo trộn lại; Hệ quả 08.8 chỉ được phát biểu cho rút có hoàn lại.

**(ii) Tính đo được.** Giả sử $(w,z)\mapsto\nabla\ell(w,z)$ đo được. Như Bước 1 của Phụ lục B trong Bài 05, quy nạp theo $t$ cho $w_{t+1}$ là hàm đo được của $(s,\xi)$: $w_t$ đo được, $\nabla\ell(w_t,z_{i_t})$ là hợp của các hàm đo được, và phép chiếu liên tục. Hàm $\ell(\cdot,z)$ liên tục theo $w$ và $\ell(w,\cdot)$ đo được theo $z$, nên $(s,\xi,z)\mapsto\ell(w_{T+1},z)$ đo được theo bộ ba, như Định nghĩa 05.18 đòi. Cùng lập luận áp dụng cho $\bar w_T$.

### C. Chứng minh Hệ quả 08.8

::: proof Chứng minh Hệ quả 08.8
**Lộ trình.** Dùng Mệnh đề 06.5(b), chặn riêng hai số hạng, rồi chọn $\eta$. Bất đẳng thức then chốt là Mệnh đề 06.5(b).

**Bước 1 (khoảng cách tổng quát hóa; Hệ quả 08.7).** Với độ dài bước hằng, Hệ quả 08.7 cho
$$
\begin{aligned}
&\mathbb E\big[L_D(\bar w_T)-L_S(\bar w_T)\big]\\
&\le\frac{\eta G^2(T-1)}m .
\end{aligned}
$$
Các kì vọng $\mathbb EL_D(\bar w_T)$ và $\mathbb EL_S(\bar w_T)$ hữu hạn như Bước 4 của chứng minh Định lý 08.6. Với mọi $w\in W$, $L_D(w)\le L_D(w_1)+GR<\infty$ theo Bước 1 của chứng minh Định lý 08.6 và (T2); đó là giả thiết hàm lỗi của Mệnh đề 06.5.

**Bước 2 (sai số tối ưu; Định lý 05.14).** Cố định mẫu $s$. Oracle rút đều một quan sát, $\varphi(w,i)=\nabla\ell(w,z_i)$, thỏa (G1) với $F=L_s$ vì $\frac1m\sum_i\nabla\ell(w,z_i)=\nabla L_s(w)$, và thỏa (G2) với hằng số $G$ theo (G), như Bước 1 của chứng minh Hệ quả 05.19. Hàm $L_s$ lồi theo (S) và $W$ đóng, lồi, nên (C) đúng. Định lý 05.14 cho, với mọi $u\in W$,
$$
\begin{aligned}
&\mathbb E_\xi L_s(\bar w_T)-L_s(u)\\
&\le\frac{\lVert w_1-u\rVert^2}{2\eta T}+\frac{\eta G^2}2\\
&\le\frac{R^2}{2\eta T}+\frac{\eta G^2}2 .
\end{aligned}
$$
Lấy cận trên đúng theo $u\in W$, ta được $\mathbb E_\xi\operatorname{opt}_s(\bar w_T)\le\frac{R^2}{2\eta T}+\frac{\eta G^2}2$ với mọi $s$, rồi lấy kì vọng theo $S$.

**Bước 3 (Mệnh đề 06.5(b) và (T1)).** Cộng hai bước theo Mệnh đề 06.5(b), ta được (a).

**Bước 4 (chọn $\eta$).** Vế phải của (a) có dạng $a/\eta+b\eta$ với
$$
\begin{aligned}
a&=\frac{R^2}{2T},\\
b&=G^2\Big(\frac12+\frac{T-1}m\Big).
\end{aligned}
$$
Theo bất đẳng thức trung bình cộng–trung bình nhân, $a/\eta+b\eta\ge2\sqrt{ab}$, với dấu bằng tại $\eta^*=\sqrt{a/b}$. Tính trực tiếp, $\sqrt{a/b}$ bằng $\eta^*$ đã nêu và $2\sqrt{ab}=RG\sqrt{(1+2(T-1)/m)/T}$. Điều kiện $\eta^*\le2/\beta$ cần cho (a). Thay $T=m$, ta được $RG\sqrt{(3-2/m)/m}\le RG\sqrt{3/m}$. Ngoài ra $\frac{1+2(T-1)/m}T=\frac2m+\frac{1-2/m}T$, giảm theo $T$ khi $m>2$ và tiến về $\frac2m$.

$\square$ SGD chạy nhiều vòng có một cận rủi ro, nhưng theo các cận này, nó không tốt hơn một vòng qua dữ liệu với quan sát mới.
:::

### D. Phác thảo chứng minh Mệnh đề 08.10

::: proof Chứng minh Mệnh đề 08.10 (phác thảo)
**Lộ trình.** Thay Bổ đề 08.4 bằng một cận hệ số giãn chỉ dùng tính trơn, lặp lại chứng minh Mệnh đề 08.5, rồi khai triển bất đẳng thức truy hồi.

**Bước 1 (phần a; tính trơn).** Với $\Gamma=\Gamma_{\eta,z}$, theo bất đẳng thức tam giác và tính $\beta$-trơn,
$$
\begin{aligned}
&\lVert\Gamma(u)-\Gamma(v)\rVert\\
&\le\lVert u-v\rVert\\
&\quad+\eta\lVert\nabla\ell(u,z)-\nabla\ell(v,z)\rVert\\
&\le(1+\beta\eta)\lVert u-v\rVert .
\end{aligned}
$$
Phép chiếu không giãn, nên $\operatorname{proj}_W\circ\Gamma$ có cùng hệ số giãn.

**Bước 2 (phần b).** Ở bước chung, (a) thay cho Bổ đề 08.4. Ở bước khác biệt, Bước 2 của chứng minh Mệnh đề 08.5 không dùng tính lồi, nên vẫn cho $\Delta_{t+1}\le\Delta_t+2G\eta_t$, không quá vế phải của (b).

**Bước 3 (phần c).** Lấy kì vọng hai vế của (b) bằng tính tuyến tính, với $\Pr(i_t=i)=1/m$: $\mathbb E\Delta_{t+1}\le(1+\beta\eta_t)\mathbb E\Delta_t+2G\eta_t/m$. Khai triển từ $\Delta_1=0$ cho vế phải thứ nhất; $1+x\le e^x$ cho vế phải thứ hai. Với bước hằng, tổng hình học $\sum_{t=1}^T\eta(1+\beta\eta)^{T-t}=\big((1+\beta\eta)^T-1\big)/\beta$.

$\square$ Thừa số $1+\beta\eta_k$ xuất hiện vì các bước chung, chỗ duy nhất mà tính lồi của hàm lỗi từng được dùng; để lấy kì vọng mà không cần tính độc lập, (b) nhân thừa số này ở mọi bước.
:::

### E. Điểm dừng xấp xỉ

::: proof Chứng minh Mệnh đề 08.12
**Lộ trình.** Áp dụng cận trên bậc hai (Phụ lục A, Bước 1) cho hai điểm lặp liên tiếp, lấy kì vọng có điều kiện theo lịch sử, rồi cộng thành một tổng triệt tiêu. Bất đẳng thức then chốt là bất đẳng thức một bước ở Bước 2.

**Bước 1 (cận trên bậc hai; tính trơn).** Với $v=w_{t+1}=w_t-\eta g_t$ và $u=w_t$,
$$
\begin{aligned}
F(w_{t+1})&\le F(w_t)\\
&\quad-\eta\langle\nabla F(w_t),g_t\rangle\\
&\quad+\tfrac{\beta\eta^2}2\lVert g_t\rVert^2 .
\end{aligned}
$$

**Bước 2 (kì vọng có điều kiện; tính không chệch và cận phương sai).** Điểm lặp $w_t$ được xác định bởi lịch sử $\mathcal F_{t-1}$. Theo tính không chệch, $\mathbb E[\langle\nabla F(w_t),g_t\rangle\mid\mathcal F_{t-1}]=\lVert\nabla F(w_t)\rVert^2$. Khai triển bình phương như đẳng thức sau Định nghĩa 05.10, bản có điều kiện, số hạng chéo có kì vọng có điều kiện bằng $0$, nên
$$
\begin{aligned}
&\mathbb E\big[\lVert g_t\rVert^2\mid\mathcal F_{t-1}\big]\\
&=\lVert\nabla F(w_t)\rVert^2\\
&\quad+\mathbb E\big[\lVert g_t-\nabla F(w_t)\rVert^2\mid\mathcal F_{t-1}\big]\\
&\le\lVert\nabla F(w_t)\rVert^2+\sigma^2 .
\end{aligned}
$$
Thay vào Bước 1:
$$
\begin{aligned}
&\mathbb E\big[F(w_{t+1})\mid\mathcal F_{t-1}\big]\\
&\le F(w_t)\\
&\quad-\eta\big(1-\tfrac{\beta\eta}2\big)\lVert\nabla F(w_t)\rVert^2\\
&\quad+\tfrac{\beta\eta^2\sigma^2}2 .
\end{aligned}
$$

**Bước 3 (điều kiện $\eta\le1/\beta$).** Khi $\eta\le1/\beta$, $1-\tfrac{\beta\eta}2\ge\tfrac12$, nên hệ số của $\lVert\nabla F(w_t)\rVert^2$ không lớn hơn $-\tfrac\eta2$.

**Bước 4 (tính chất tháp, tổng triệt tiêu, $F\ge F_*$; giả thiết khả tích).** Các kì vọng $\mathbb EF(w_t)$ hữu hạn theo giả thiết khả tích. Lấy kì vọng (tính chất tháp) và chuyển vế:
$$
\begin{aligned}
&\tfrac\eta2\,\mathbb E\lVert\nabla F(w_t)\rVert^2\\
&\le\mathbb EF(w_t)-\mathbb EF(w_{t+1})\\
&\quad+\tfrac{\beta\eta^2\sigma^2}2 .
\end{aligned}
$$
Cộng theo $t=1,\ldots,T$, tổng triệt tiêu cho $F(w_1)-\mathbb EF(w_{T+1})\le F(w_1)-F_*$. Chia hai vế cho $\eta T/2$, ta được bảo đảm.

$\square$ Cận chặn trung bình của bình phương chuẩn gradient dọc quỹ đạo, không chặn $F(w_{T+1})-F_*$.
:::

### F. Giao thức thí nghiệm

Giao thức dưới đây đủ để tái lập bảng của câu hỏi mở đầu và các số của Ví dụ 08.6; chỉ cần thư viện NumPy.

- **Dữ liệu.** Với $p=100$, rút $g\sim N(0,I_p/p)$ và đặt $x=g/\max\{1,\lVert g\rVert\}$, nên $\lVert x\rVert\le1$ với mọi đặc trưng có thể có. Véc-tơ $w^\star$ đều trên mặt cầu đơn vị (một véc-tơ $N(0,I_p)$ chia cho chuẩn của nó), rút một lần cho mỗi hạt giống; vì vậy mỗi hạt giống cho một phân bố $D$ riêng. Cận của Định lý 08.6 đúng với mọi $D$, nên cũng đúng cho trung bình qua các hạt giống. Nhãn $y=\mathbb 1[\langle w^\star,x\rangle\ge0]$, lật với xác suất $0{,}1$, độc lập giữa các quan sát. Mẫu huấn luyện có $m=200$ quan sát; mẫu kiểm tra có $5000$ quan sát độc lập.
- **Mẫu lân cận.** Một chỉ số $i$ rút đều trên $\{1,\ldots,m\}$; quan sát thứ $i$ được thay bằng một quan sát mới rút từ $D$.
- **Thuật toán.** Thuật toán 08.1 với $W=\mathbb R^p$ (không chiếu), $w_1=0$, $\eta_t=0{,}5$, $T=20\,000$ bước, tức $100$ vòng qua dữ liệu; chỉ số rút đều có hoàn lại; hàm lỗi logistic với nhãn $\tilde y=2y-1$; đầu ra là điểm lặp cuối.
- **Ba lần chạy.** Lần thứ nhất trên $S$; lần thứ hai trên mẫu lân cận với cùng dãy chỉ số (ghép cặp); lần thứ ba trên $S$ với một dãy chỉ số độc lập (không ghép cặp).
- **Đại lượng đo.** Tại các bước $100$, $200$, $1000$, $2000$, $4000$, $10\,000$ và $20\,000$: trung bình hàm lỗi logistic trên mẫu huấn luyện và trên mẫu kiểm tra cùng hiệu của chúng; lỗi phân lớp trên hai mẫu; $\Delta$ ghép cặp và không ghép cặp; tỉ lệ đổi nhãn dự đoán trên mẫu kiểm tra; chuẩn gradient của $L_S$; cận $2G^2\eta t/m=t/200$ với $G=1$.
- **Lặp lại.** Hai mươi hạt giống $0,1,\ldots,19$, mỗi hạt giống khởi tạo bộ sinh số ngẫu nhiên `numpy.random.default_rng`. Thứ tự rút cố định: $w^\star$, mẫu huấn luyện, mẫu kiểm tra, chỉ số $i$, quan sát thay thế, dãy chỉ số ghép cặp, dãy chỉ số độc lập. Báo trung bình và khoảng nhỏ nhất – lớn nhất qua các hạt giống.
- **Giả thiết.** Mọi giả thiết của Định lý 08.6 thỏa (Ví dụ 08.6, Bước 1).
- **Chi phí.** Khoảng $15$–$25$ giây trên một máy nhiều nhân.

Các số đo được làm tròn đến giá trị gần nhất, ba chữ số thập phân; chỉ cận trên của các định lý được làm tròn lên. Cột "Khoảng cách" của câu hỏi mở đầu là trung bình của hiệu từng hạt giống, làm tròn riêng, nên có thể lệch một đơn vị ở chữ số cuối so với hiệu của hai cột đã làm tròn: ở nửa vòng, $0{,}662-0{,}618=0{,}044$, còn trung bình của hiệu là $0{,}0445$, ghi $0{,}045$.

Ngoài các số đã dùng, lần chạy cho các kết quả sau. Ở $10$ và $50$ vòng, hàm lỗi logistic trên mẫu kiểm tra là $0{,}603$ và $0{,}827$, khoảng cách là $0{,}298$ và $0{,}650$. Lỗi phân lớp trên mẫu kiểm tra là $0{,}383$ ở nửa vòng và nằm giữa $0{,}301$ và $0{,}312$ từ $5$ đến $100$ vòng. Chuẩn gradient của $L_S$ giảm từ $0{,}039$ ở nửa vòng xuống $0{,}004$ ở $100$ vòng. $\Delta$ giữa lần chạy thứ nhất và lần chạy thứ ba (không ghép cặp) là $2{,}99$; $3{,}83$; $4{,}90$; $4{,}93$; $4{,}82$; $4{,}34$; $4{,}00$ ở $0{,}5$; $1$; $5$; $10$; $20$; $50$; $100$ vòng: nó đã lớn từ nửa vòng đầu, rồi giảm sau $10$ vòng; các định lý của bài không nói gì về đại lượng này. Chạy lại với $\eta=0{,}25$ cho khoảng cách $0{,}651$ sau $100$ vòng, gần giá trị $0{,}650$ của $\eta=0{,}5$ sau $50$ vòng, với cùng ngân sách độ dài bước $5000$.
