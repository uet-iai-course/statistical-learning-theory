# Bài 09 — Rà soát 2: chính xác toán học

Đối tượng: `lec09-draft-frozen.md` (987 dòng). Người rà: rà soát 2 (chính xác toán học), chỉ đọc. Số được tính lại bằng `reviews09/r2/check.py`, `win.py`, `big.py`; script `exp_lec09_bigram.py --part all` chạy lại (1,3 giây), đầu ra ở `reviews09/r2/script_out.txt`.

## Tổng kết theo mức

| Mức | Số phát hiện |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 2 |
| nhẹ | 10 |

Mọi chứng minh đầy đủ (09.3, 09.8, 09.9, 09.12, 09.13, Phụ lục B) đúng với giả thiết đã nêu. Mọi số tính lại khớp ở độ chính xác in ra, trừ hai lỗi làm tròn (F7, F8). Hai lỗi trung bình là: một khẳng định sai trong lời bình sau Hệ quả 09.9 và chỗ Định nghĩa 09.6 với Ví dụ 09.6 không khớp nhau về kí tự kết thúc.

## Danh sách kết quả

| Kết quả | Đánh giá | Ghi chú |
|---|---|---|
| Mệnh đề 09.3(a)(b) | ✓ | Trường hợp tiền tố có xác suất 0 xử lý đúng (biên ≥ xác suất của chuỗi). |
| Mệnh đề 09.3(c) | ✓ | Quy nạp từ $j=n$ xuống: biên của $Q_n$ bằng $Q_j$, tổng bằng 1, xác suất có điều kiện đúng trên tiền tố dương. |
| Nhận xét 09.5 (độ dài thay đổi, kí tự kết thúc) | ✓ | Tổng $1+1+1=3$ đã kiểm bằng cách liệt kê. $\Pr(n)=(1/2)^n$ đúng khi vị trí 1 không rút $\mathtt E$. Điều kiện "dừng với xác suất 1" là đúng và đủ, phần này không có chứng minh. |
| Định nghĩa 09.6 và Ví dụ 09.6 | ✓ cho số, ✗ cho tính nhất quán | $\theta^*=1/6$ và $1/2$, các trọng số $1/2$, $1/4$, $1/20$ đều đúng. Cận dưới khi chuẩn hóa ∝ $p_D/n$ đúng (bất đẳng thức Gibbs với trọng số $p_D/n$). Xem F2. |
| Mệnh đề 09.8(a) | ✓ | Bước 2: chuỗi thứ nhất hội tụ tuyệt đối, chuỗi thứ hai có phần âm khả tổng, nên cộng được trong $(-\infty,\infty]$. Trường hợp giá không chứa cho hai vế $+\infty$. |
| Mệnh đề 09.8(b) | ✓ | Khi KL hữu hạn, các tổng hữu hạn và bất đẳng thức đúng theo từng số hạng, nên dấu bằng xảy ra theo từng số hạng; thêm $\sum_{p_D>0}p_\theta=1$ thì được $p_\theta=p_D$. |
| Mệnh đề 09.8(c) (mật độ) | ✓ | Hai điều kiện khả tích làm $L_D$ và $\mathrm h$ hữu hạn; $\int_{p_D>0}p_\theta\le1$. |
| Hệ quả 09.9(a)(b) | ✓ | Phát biểu và chứng minh đúng. Đoạn sau khối nói rõ đây không phải bảo đảm cho mẫu hữu hạn. **Lời bình sau $\square$ sai** (F1). |
| Định lý 09.12(a)–(d) | ✓ | Ngoặc thứ hai khả tích vì bằng hằng số trừ ngoặc thứ nhất. Dấu bằng hầu khắp nơi (cần $\int_{q>0}p(\cdot\mid x)=1$). Phần (c) cần thêm $\mathbb E_q\lvert\ln p_\theta(v)\rvert<\infty$, đã nêu. Câu ELBO $=-\infty$ đúng (phần dương bị chặn bởi $p_\theta(x)$). |
| Hệ quả 09.13 (EM) | ✓ | Bước 1 đúng: $\mathcal V$ hữu hạn, mỗi số hạng thuộc $[-\infty,\infty)$, tổng hữu hạn nên mọi số hạng hữu hạn. |
| Mệnh đề 09.15 + Phụ lục B | ✓ (hai câu chữ cần sửa, F3, F4) | Bước 1–5 đúng. Bước 6: $\lVert J\rVert\le K(1+\lVert\zeta\rVert)$, $\lVert\nabla f(g)\rVert\le C'(1+\lVert\zeta\rVert^2)$, tích bị chặn bởi $C''(1+\lVert\zeta\rVert^3)$. Điều kiện $\lvert f\rvert\le C(1+\lVert v\rVert^3)$ thừa, vì nó suy ra từ cận của $\nabla f$, nhưng giữ cũng không sai. |
| Phản ví dụ $\mathbb 1[v>0]$ (Ví dụ 09.12) | ✓ | $F'(0{,}5)=0{,}35207$; (i) không thỏa; câu "khả vi hầu khắp nơi tại từng tham số chưa đủ" đúng. |
| Bernoulli $\mathbb 1[u<\phi]$ | ✓ | Ước lượng theo đường đi bằng 0 hầu chắc chắn; $v/\phi$ có kì vọng 1, phương sai $1/\phi-1=2{,}333$. |
| Ví dụ 09.11 (đường đi so với gradient log) | ✓ | Phương sai 1 và 6; $29{,}027$ đúng theo Phụ lục A(iv) (Monte Carlo $4\cdot10^6$ mẫu: $29{,}05$). |
| Ví dụ 09.13 | ✓ | $p_{\theta_3}\ge0{,}01p_{\theta_1}$; các cận làm tròn đúng chiều. |
| Chuẩn blueprint §E/Lecture 9 | ✓ | Hàm lỗi log không bị chặn (§2, Ví dụ 09.4, 09.7); quan sát độc lập là chuỗi (Định nghĩa 09.1, Ví dụ 09.4); cửa sổ phụ thuộc (Ví dụ 09.5, §12(b)); tính không chệch luôn đi kèm điều kiện (Mệnh đề 09.15, Ví dụ 09.12); độ hợp lý và chất lượng mẫu tách riêng (Ví dụ 09.13). |

## Bảng số (tính lại)

| Vị trí | Bản nháp | Tính lại | Kết luận |
|---|---|---|---|
| Mở đầu, Ví dụ 09.3 | $21/125=0{,}168$; $1{,}7838=0{,}5108+0{,}3567+0{,}9163$; $0{,}5946$; $1{,}8123$ | $1{,}783791$; $0{,}594597$; $1{,}812301$ | ✓ |
| Ví dụ 09.1 | $\Pr(x_2=\mathtt B)=0{,}58$ | $0{,}58$ | ✓ |
| Câu ôn nhanh 1 | $\sqrt{0{,}036889}\le0{,}1921$ | $0{,}192065$ | ✓ (làm tròn lên) |
| Câu ôn nhanh 3 | $0{,}4$; $0{,}75$ | $0{,}4$; $0{,}75$ | ✓ |
| Ví dụ 09.2 | $0{,}6931$; $0{,}6325$; $0{,}6109$; $0{,}6390$ | $0{,}693147$; $0{,}632465$; $0{,}610864$; $0{,}639032$ | ✓ |
| §2 | $\ln(0{,}1\sqrt{2\pi})\approx-1{,}3836$ | $-1{,}383647$ | ✓ |
| Nhận xét 09.5 | tổng theo độ dài 1, 2, 3 bằng $1$ mỗi độ dài | $1$; $1$; $1$ | ✓ |
| Ví dụ 09.4 | $\ln20=2{,}9957$; $b\approx599{,}15$; $\le115{,}08$; $0{,}5754$; $0{,}0407$; $6621{,}1\Rightarrow6622$ | $2{,}995732$; $599{,}1465$; $115{,}0748$; $0{,}575374$; $0{,}040685$; $6621{,}105$ | ✓ (về "$=[0;2{,}9957]$" xem F9) |
| Ví dụ 09.5 | $4990$; $998$; $0{,}2^{10}\approx10^{-7}$ | $4990$; $998$; $1{,}024\cdot10^{-7}$ | ✓ |
| Ví dụ 09.5 (thí nghiệm) | ngẫu nhiên $0{,}1995$ (từ $0{,}137$ đến $0{,}246$); theo thời gian $0{,}9944$ ($0{,}915$–$1{,}066$) | $0{,}199502$ [$0{,}136720$; $0{,}245465$]; $0{,}994415$ [$0{,}915396$; $1{,}066030$] | **$0{,}246$ sai, đúng là $0{,}245$** (F7) |
| Ví dụ 09.6 | $\theta^*=1/6$; $1/2$ | $0{,}166667$; $0{,}5$ | ✓ |
| Sau Định nghĩa 09.7 | KL Bernoulli $0{,}0226$; $0{,}0216$; $\mathrm h=-0{,}6931$ | $0{,}022582$; $0{,}021601$; $-0{,}693147$ | ✓ |
| Sau Hệ quả 09.9 | $\mathrm H=0{,}6730$; $L_D(0{,}7)=0{,}6956$; khoảng cách $0{,}0847$ | $0{,}673012$; $0{,}695594$; $0{,}084730$ | ✓ |
| Ví dụ 09.7 | $1{,}2040$; $3{,}4544$; $6{,}9078$; $\ln2{,}5=0{,}9163$; $\ln1{,}25=0{,}2231$ | $1{,}203973$; $3{,}454378$; $6{,}907756$; $0{,}916291$; $0{,}223144$ | ✓ |
| Ví dụ 09.7 | $0{,}99^m$: $0{,}9044$; $0{,}6050$; $0{,}3660$; $m\le68$ ($0{,}5049$; $0{,}4998$) | $0{,}904382$; $0{,}605006$; $0{,}366032$; $68$ ($0{,}504886$; $0{,}499837$) | ✓ |
| Ví dụ 09.7 | $1/52=0{,}0192$; $L_D=0{,}0587$; $\mathrm H=0{,}0560$; $\ln52\approx3{,}95$ | $0{,}019231$; $0{,}058736$; $0{,}056002$; $3{,}951244$ | ✓ (về cận $3{,}95$ xem F10) |
| Ví dụ 09.8 | entropy mỗi hàng $1{,}0889$; $\mathrm H/200=1{,}0904$; độ bối rối $2{,}975$ | $1{,}088900$; $1{,}090387$; $2{,}975425$ | ✓ |
| Ví dụ 09.8 bảng | MLE/cộng một/thật: $m=1$: $+\infty$/$1{,}122$/$1{,}091$; $m=5$: $+\infty$/$1{,}097$/$1{,}090$; $m=50$: $1{,}091$/$1{,}091$/$1{,}091$; $m=500$: $1{,}088$/$1{,}088$/$1{,}088$; huấn luyện $1{,}070$; $1{,}080$; $1{,}090$; $1{,}090$ | $1{,}122273$/$1{,}090707$; $1{,}097123$/$1{,}090414$; $1{,}091300$/$1{,}091281$/$1{,}090569$; $1{,}088246$/$1{,}088246$/$1{,}088164$; $1{,}069855$; $1{,}079882$; $1{,}089713$; $1{,}090279$; $+\infty$ ở $10/10$, $5/10$ lần chạy | ✓ |
| Ví dụ 09.8 Bước 3–4 | 12 kí tự `AAGGAAAACCCC`, $10/16$ ô; chi phí $0{,}031$ | 6 cặp đã gặp, đúng $10/16$; $1{,}122273-1{,}090707=0{,}031566$ | **$0{,}032$ khi làm tròn từ số chưa làm tròn** (F8) |
| Phụ lục C | khoảng cộng một và thật; huấn luyện $1{,}077$; …; mẫu sinh; $18/39$ | [$1{,}104395$; $1{,}147280$], [$1{,}088743$; $1{,}109283$], [$1{,}084901$; $1{,}098933$], [$1{,}082795$; $1{,}092213$]; thật [$1{,}082308$; $1{,}098284$]; $1{,}076508$; chuỗi sinh trùng; $0{,}4615$ | ✓ |
| Ví dụ 09.9 | $\ln p_\theta(2)=-2{,}2655$; hậu nghiệm $N(1,\tfrac12)$ | $-2{,}265512$ | ✓ |
| Ví dụ 09.10 (hai bảng) | tái tạo $-3{,}4189$, $-1{,}9189$, $-1{,}8889$, $-1{,}6689$; KL $0$, $0{,}5$, $0{,}4166$, $0{,}5966$; ELBO $-3{,}4189$, $-2{,}4189$, $-2{,}3055$, $-2{,}2655$; khe $1{,}1534$, $0{,}1534$, $0{,}0400$, $0$ | khớp đến $10^{-6}$; KL tới hậu nghiệm $N(1,\tfrac12)$ tính trực tiếp: $1{,}153426$; $0{,}153426$; $0{,}04$; $0$ (bằng khe chính xác); Monte Carlo ELBO $(0{,}8;0{,}5)$: $-2{,}3053$ | ✓ |
| Phụ lục A(iii) | Hesse $\operatorname{diag}(2,2+1/\sigma^2)$; giá trị lớn nhất $=\ln p_\theta(2)$ | đúng | ✓ |
| Ví dụ 09.11 | $(1{,}5;0{,}75)$; $(3;-3)$; kì vọng $(2,-1)$; phương sai $1$, $6$; $29{,}027$ | đúng; Monte Carlo $(1{,}9994;1{,}0004)$, $(-0{,}9992;6{,}0023)$; gradient log: kì vọng $1{,}9985$, phương sai $29{,}053$; dạng đóng $29{,}027018$ | ✓ |
| Ví dụ 09.12 | $0{,}3521$; $2{,}333$ | $0{,}352065$; $2{,}333333$ | ✓ |
| Ví dụ 09.13 | $\ln100\to4{,}6052$; $1{,}4189$; $\le1{,}4249$; $2{,}5484$; $8{,}9\cdot10^{-44}$; $0{,}0059$ | $4{,}605170$; $1{,}418939$; $1{,}424812$; $2{,}548376$; $8{,}892\cdot10^{-44}$; $0{,}005874$ | ✓ (cận làm tròn đúng chiều) |
| §12 câu hỏi cuối buổi | $12/125=0{,}096$; $2{,}3434$; $0{,}7811$; $2{,}184$; KL $0{,}0400$ | $2{,}343407$; $0{,}781136$; $2{,}183951$; $0{,}040000$ | ✓ |

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | Hệ quả 09.9, câu sau $\square$ (dòng 439) | Khẳng định "khi lớp không chứa $p_D$, phần chênh $\inf_\Theta\mathrm{KL}(p_D\Vert p_\theta)>0$" sai trong trường hợp tổng quát. Cận dưới đúng có thể bằng 0 mà không đạt được. | "Khi lớp không chứa $p_D$ (*đặc tả sai*, misspecification), phần chênh $\inf_\Theta\mathrm{KL}(p_D\Vert p_\theta)>0$ còn lại ngay cả khi có vô hạn dữ liệu." Phản ví dụ: $D=\mathrm{Ber}(0{,}6)$, $\Theta=(0,1)\setminus\{0{,}6\}$. Lớp không chứa $p_D$ nhưng $\inf\mathrm{KL}=0$. | Viết "Khi lớp không chứa $p_D$ (đặc tả sai) và $\inf_\Theta\mathrm{KL}(p_D\Vert p_\theta)>0$, phần chênh này còn lại ngay cả khi có vô hạn dữ liệu", hoặc "phần chênh $\inf_\Theta\mathrm{KL}\ge0$, nói chung dương, còn lại …". |
| trung bình | Định nghĩa 09.6 (dòng 324–327) và Ví dụ 09.6 (dòng 333) | Định nghĩa 09.6 đặt mô hình có kí tự kết thúc. Nhưng tổng chỉ chạy đến $n(x)$ mà không nói $n(x)$ có tính $\mathtt E$ không, nên "tức hàm lỗi log của chuỗi" chỉ đúng khi số hạng của $\mathtt E$ có mặt (Nhận xét 09.5 nói "gồm cả số hạng của $\mathtt E$"). Ví dụ 09.6 lại dùng mô hình không có $\mathtt E$, với "độ dài coi như cho trước", nên không phải một trường hợp của Định nghĩa 09.6. Kết luận vẫn đúng, nhưng chưa có lý do được viết ra. | Dòng 326: $\sum_{j=1}^{n(x)}$; dòng 266: "gồm cả số hạng của $\mathtt E$"; dòng 333: "độ dài coi như cho trước". | (1) Định nghĩa 09.6: ghi rõ "$n(x)$ là số kí tự trước $\mathtt E$; $\ell$ gồm cả số hạng $-\ln p_\theta(\mathtt E\mid x_{1:n(x)})$" (tổng đến $n(x)+1$). Một cách khác là định nghĩa $\ell$ là hàm lỗi có điều kiện theo độ dài. (2) Ví dụ 09.6, Thiết lập: thêm "phân bố độ dài (hoặc xác suất của $\mathtt E$) có tham số riêng, không phụ thuộc $\theta$; số hạng của nó là hằng theo $\theta$ trong cả hai mục tiêu, nên không đổi $\theta^*$". |
| nhẹ | Phụ lục B, Bước 4 (dòng 950) | Lập luận dãy $\phi_k\to\phi_0$ chỉ cho tính liên tục tại $\phi_0$, nhưng câu kết lại nói "liên tục trên $U$". Bước 5 cần tính liên tục trên một tập mở. | "…nên các đạo hàm riêng của $F$ liên tục trên $U$." | "…liên tục tại $\phi_0$; vì $\phi_0$ tùy ý, chúng liên tục trên $\Phi$." Bước 5: "Áp dụng trên $\Phi$". |
| nhẹ | Phụ lục B, Bước 1 (dòng 940) | Hợp các tập ngoại lệ $\{-\mu\}$ theo $\mu\in I$ là $-I$, không phải $I$. | "hợp theo $\mu$ trong một khoảng là chính khoảng đó" | "…là khoảng đối $\{-\mu:\mu\in I\}$, có xác suất dương". |
| nhẹ | §9, câu thứ hai (dòng 673) | "không thể đạo hàm trực tiếp bên trong kì vọng" thiếu chính xác. Ước lượng gradient log chính là đạo hàm dưới dấu tích phân (lấy đạo hàm mật độ). Điều không được làm là đưa $\nabla_\phi$ vào trong $\mathbb E_{q_\phi}$ như thể phân bố cố định. | Dòng 673; Định nghĩa 09.14, khoản gradient log. | "…nên $\nabla F(\phi)$ không bằng $\mathbb E_{q_\phi}\nabla_\phi f(v)$ (bằng $0$); cần lấy đạo hàm mật độ (ước lượng gradient log) hoặc chuyển sự phụ thuộc vào hàm (tái tham số hóa)." |
| nhẹ | Đoạn sau Ví dụ 09.11 (dòng 711–718) | Nói gradient một mẫu của $-\frac1m\sum\operatorname{ELBO}$ không chệch "dưới các điều kiện trên". Nhưng $\kappa$ ở đây có thêm $\ln q_\phi(g_\phi(\zeta)\mid x_i)$, phụ thuộc $\phi$ trực tiếp, và còn phụ thuộc $\theta$. Trường hợp đủ (Gauss, dạng $f\circ g_\phi$) không áp dụng nguyên văn. | Dòng 698 (trường hợp đủ chỉ cho $f(g_\phi(\zeta))$); dòng 714–715. | "…dưới các điều kiện (i)–(iii) của Mệnh đề 09.15 cho $\kappa((\theta,\phi),\zeta)$ ở trên, với mỗi $i$". |
| nhẹ | Ví dụ 09.8, Kết luận (i) (dòng 485) và câu hỏi thực hành (i) (dòng 149) | Câu hỏi hỏi khoảng cách tới **giá trị tốt nhất**, câu trả lời so với **mô hình thật** trên mẫu kiểm tra. "Dưới $0{,}001$" đúng cho trung bình 10 lần chạy ($0{,}00073$) nhưng không đúng cho từng lần (tối đa $0{,}0016$). | Tính lại: trung bình MLE $1{,}091300$, thật $1{,}090569$, $\mathrm H/200=1{,}090387$; chênh lệch lớn nhất theo lần chạy $0{,}00159$. | "trung bình qua 10 lần chạy, hàm lỗi kiểm tra cách mô hình thật $0{,}0007$ và cách giá trị tốt nhất $0{,}0009$". |
| nhẹ | Ví dụ 09.5, Bước 2 (dòng 312) | Làm tròn sai: giá trị lớn nhất $0{,}245465$ được ghi $0{,}246$, có lẽ do làm tròn hai lần từ $0{,}2455$. | `win.py`: max $=0{,}24546533$. | "từ $0{,}137$ đến $0{,}245$". |
| nhẹ | Ví dụ 09.8, Bước 4 (dòng 483) | Hiệu được lấy từ hai số đã làm tròn: $1{,}122-1{,}091=0{,}031$. Tính từ số chưa làm tròn thì $0{,}031566\to0{,}032$. | `big.py`: $1{,}122273-1{,}090707$. | "với giá khoảng $0{,}032$" (hoặc giữ phép trừ và ghi "khoảng $0{,}03$"). |
| nhẹ | Ví dụ 09.4, Bước 1 (dòng 278) | Dấu "=" đứng trước một đầu mút đã làm tròn xuống ($\ln20=2{,}99573>2{,}9957$), trong khi nó là cận trên của miền giá trị. | "$[0,\ln(1/c)]=[0;\,2{,}9957]$" | "$\approx[0;\,2{,}9957]$", hoặc "$\subseteq[0;\,2{,}9958]$". |
| nhẹ | Ví dụ 09.7, Bước 4 (dòng 453) | Một cận trên được ghi bằng giá trị làm tròn xuống: $\ln52=3{,}9512>3{,}95$. Quy ước của học phần là làm tròn cận trên lên. | "$\ell\le\ln52\approx3{,}95$" | "$\ell\le\ln52<3{,}952$". |
| nhẹ | §10 (dòng 793) | Dẫn sai mục: cụm "probabilistic encoder" nằm ở §2.1 của Kingma–Welling, không ở §2.2. | PDF trang 3: cụm từ ở vị trí 4048, còn tiêu đề §2.2 bắt đầu ở vị trí 4399. | "Kingma và Welling (§2.1)". |
| nhẹ | §2, cuối đoạn 3 (dòng 122) | "chỉ áp dụng khi xác suất … bị chặn dưới" đọc như một điều kiện cần. Với mật độ, còn cần cận trên của mật độ, vì không có nó thì $\ell$ không bị chặn dưới. | "Các cận của Bài 02–04 và Bài 07 chỉ áp dụng khi xác suất của mô hình bị chặn dưới" | "…áp dụng trực tiếp khi hàm lỗi bị chặn, chẳng hạn khi xác suất của mô hình rời rạc bị chặn dưới bởi $c>0$ (với mật độ: bị chặn trên và dưới)…". |

Ghi chú (không phải phát hiện): Định nghĩa 05.10 đặt $F$ lồi, nên khi gọi (G1) "cho một hàm mục tiêu khả vi" không lồi (Phụ lục B, câu sau $\square$) là đang dùng rộng định nghĩa. Bài đã nói rõ rằng Định lý 05.14 không áp dụng.
