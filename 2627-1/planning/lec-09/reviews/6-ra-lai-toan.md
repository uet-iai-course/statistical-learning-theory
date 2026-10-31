# Bài 09 — Rà lại toán học sau biên tập vòng 1 (người rà 2)

Đối tượng: `lec09-r1-frozen.md` (1019 dòng; giống hệt `2627-1/materials/lec-09/lecture-note.md`, đã kiểm bằng `cmp`). Đã đọc: `0-quyet-dinh.md`, toàn văn bản sửa. Số tính lại bằng `reviews09/r2/check2.py` (cùng `check.py`, `big.py`, `win.py` của vòng trước). Chỉ đọc, không commit.

## Tổng kết theo mức

| Mức | Số phát hiện mới |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 0 |
| nhẹ | 4 |

Đã sửa đủ cả 13 phát hiện cũ (2 trung bình, 11 nhẹ). Mọi phần toán đổi mới đúng, mọi số mới tính lại khớp. Bốn ý nhẹ dưới đây chỉ là cách viết hoặc thiếu một giả thiết biên; không có phát hiện nào ảnh hưởng tới kết quả.

## Phát hiện cũ (✓ đã sửa / ✗ chưa)

| Phát hiện cũ | Dòng mới | Đánh giá |
|---|---|---|
| F1 Hệ quả 09.9: "lớp không chứa $p_D$ ⇒ $\inf\mathrm{KL}>0$" | 426 | ✓ "nếu thêm $\inf_\Theta\mathrm{KL}(p_D\Vert p_\theta)>0$, phần chênh này còn lại …" |
| F2 Định nghĩa 09.6 / Ví dụ 09.6 và kí tự kết thúc | 303–306, 312 | ✓ Tổng đến $n(x)+1$ với $x_{n(x)+1}=\mathtt E$. Ví dụ 09.6 cho $\mathtt E$ tham số riêng; số hạng của nó là hằng theo $\theta$ trong cả hai mục tiêu (khi chuẩn hóa, hằng chia cho $n(x)$ vẫn là hằng), nên vẫn được $\tfrac16$ và $\tfrac12$. |
| F3 Phụ lục B Bước 4–5 (tính liên tục) | 941, 943 | ✓ "liên tục tại $\phi_0$; vì $\phi_0$ tùy ý, chúng liên tục trên $\Phi$"; Bước 5 áp dụng trên $\Phi$. |
| F4 Phụ lục B Bước 1 (hợp các tập ngoại lệ) | 931 | ✓ "khoảng đối $\{-\mu:\mu\in I\}$". |
| F5 §9 "không thể đạo hàm bên trong kì vọng" | 656 | ✓ "khác $\mathbb E_{q_\phi}\nabla_\phi f(v)$, vốn bằng $0$" — đúng, vì $f$ không phụ thuộc $\phi$; có nêu hai cách. |
| F6 Gradient ngẫu nhiên của ELBO, số hạng $\ln q_\phi$ | 694–701, 674, 691 | ✓ $\kappa_i=\ln\big(q_\phi(g_\phi(\zeta)\mid x^{(i)})/p_\theta(x^{(i)},g_\phi(\zeta))\big)$ cho $\mathbb E_\zeta\kappa_i=-\operatorname{ELBO}(\theta,\phi;x^{(i)})$ (Monte Carlo tại $x=2$, $q=N(0{,}8;0{,}5)$: $2{,}3052$, so với $2{,}3055$). (i)–(iii) áp cho $(\theta,\phi)$; lấy kì vọng theo $i$ đều được $-\frac1m\sum_i\operatorname{ELBO}$. |
| F7 Ví dụ 09.5 $0{,}246$ | 291 | ✓ $0{,}245$; trung bình ghi $0{,}200$ ($0{,}19950\to0{,}200$, đúng), Phụ lục C dòng 978 giải thích. |
| F8 Ví dụ 09.8 $0{,}031$ | 481 | ✓ "khoảng $0{,}032$". |
| F9 Ví dụ 09.4 đầu mút | 257 | ✓ $[0,\ln20]$, $\ln20\approx2{,}9957$. |
| F10 Ví dụ 09.7 cận $\ln52$ | 448 | ✓ $\ln52<3{,}952$. |
| F11 Kingma–Welling §2.1 cho "probabilistic encoder" | 784 (câu bỏ), 490, 864 | ✓ Đã kiểm thêm: giả thiết "khả vi hầu khắp nơi" nằm ở §2.1 (PDF tr. 2). |
| F12 Ví dụ 09.8(i) | 145, 483 | ✓ Câu hỏi và câu trả lời cùng một đại lượng; $0{,}0009$ và $0{,}0007$ là trung bình 10 lần chạy. |
| F13 §2 "chỉ áp dụng khi" | 118 | ✓ Viết thành điều kiện đủ; với mật độ cần chặn cả trên lẫn dưới. |

## Phần toán đã đổi (dựng lại)

| Mục | Dòng | Đánh giá |
|---|---|---|
| N1 GAN và mô hình khuếch tán | 797 | ✓ Không còn khẳng định toán học nào sai. |
| N2 câu cầu nối | 851 | ✓ (có kèm ghi chú, xem P1). Trong $L_S$, $L_D$ và $-\frac1m\sum\operatorname{ELBO}$, kì vọng lấy theo $D$ hoặc $S$ (cố định) và theo $q_\phi$; $p_\theta$ chỉ nằm trong hàm lấy kì vọng. |
| N3 bảng §1 | 97–101 | ✓ $L_D(\theta)$ tất định với mỗi $\theta$; $\hat\theta$, $L_S$ ngẫu nhiên theo dữ liệu. |
| Hệ quả 09.9 | 410–427 | ✓ |
| Định nghĩa 09.6, Ví dụ 09.6 | 302–335 | ✓ Bước 2 ($-\tfrac12\ln\theta-\tfrac12\ln(1-\theta)$; đạo hàm $-\tfrac1{2\theta}+\tfrac1{2(1-\theta)}$) đúng. Xem P2 về $n(x)\ge1$. |
| Đoạn mở §9 | 656 | ✓ |
| Mệnh đề 09.15, mục "Hàm" | 674 | ✓ "$\phi$ gồm mọi tham số cần lấy gradient". |
| $\kappa_i$, đoạn 694–701 | 694–701 | ✓ |
| Câu sau $\square$ (phác thảo) và dòng 780 | 691, 780 | ✓ Với $\Phi$ liên thông, một phép tái tham số hóa rời rạc không tầm thường luôn nhảy theo $\phi$, nên (i) không thỏa. Câu "điều không xảy ra với biến ẩn rời rạc" đúng. |
| Phụ lục B Bước 1, 4, 5 | 931, 941, 943 | ✓ |
| Phụ lục D, chứng minh Mệnh đề 09.3 | 982–1000 | ✓ Chuyển nguyên văn từ bản cũ, đã kiểm ở vòng trước; câu sau $\square$ đúng. |
| Phụ lục D, chứng minh Hệ quả 09.13 | 1002–1019 | ✓ Xem P3 về câu sau $\square$. |
| Định lý 09.12 Bước 4 dẫn Mệnh đề 09.8(c) | 585 | ✓ $\mathbb E_q\lvert\ln p_\theta(v\mid x)\rvert\le\mathbb E_q\lvert\ln p_\theta(x,v)\rvert+\lvert\ln p_\theta(x)\rvert<\infty$, nên hai điều kiện khả tích của 09.8(c) thỏa khi $q$ ở chỗ của $p_D$. |
| Dòng 504 (hậu nghiệm là khối lượng điểm) | 504 | ✓ $q$ không liên tục tuyệt đối theo $\delta_x$, nên KL $=+\infty$. |
| Dòng 161 ($c\,p_\theta$) | 161 | ✓ |
| Dòng 215 (học theo đáp án) | 215 | ✓ "có thể khác … khi $p_\theta\ne p_D$". |

## Bảng số mới

| Vị trí | Bản sửa | Tính lại | |
|---|---|---|---|
| Ví dụ 09.2, dòng 174 | $0{,}7\cdot0{,}3567+0{,}3\cdot1{,}2040=0{,}6109$ | $0{,}249672+0{,}361192=0{,}610864$ | ✓ |
| Ví dụ 09.3, dòng 229 | $0{,}5108$; $0{,}3567$; $0{,}9163$ | $0{,}510826$; $0{,}356675$; $0{,}916291$ | ✓ |
| Ví dụ 09.1, dòng 135 | $1-0{,}58=0{,}42$ | $0{,}42$ | ✓ |
| Ví dụ 09.4, dòng 257, 271 | $\ln20\approx2{,}9957$; $\ln20\sqrt{\ln40/(2\cdot10^4)}\approx0{,}0407$ | $2{,}995732$; $0{,}040685$ | ✓ |
| Sau Hệ quả 09.9, dòng 429 | $0{,}6956-0{,}6109=0{,}0847$ | $0{,}084730$ | ✓ |
| Ví dụ 09.7, dòng 434 | $L_D(0{,}1)=0{,}0527+1{,}1513=1{,}2040$ | $0{,}052680+1{,}151293$ | ✓ |
| Ví dụ 09.7, dòng 450 | $0{,}0192+0{,}0395=0{,}0587$ | $0{,}019224+0{,}039512=0{,}058736$ | ✓ |
| Ví dụ 09.8, dòng 462 | $1{,}3863+216{,}69=218{,}08$ | $199\cdot1{,}088900=216{,}6911$; $\mathrm H=218{,}0774$ | ✓ |
| Ví dụ 09.8, dòng 483 | $0{,}0009$; $0{,}0007$ | $1{,}091300-1{,}090387=0{,}000913$; $1{,}091300-1{,}090569=0{,}000731$ | ✓ |
| Ví dụ 09.8, dòng 481 | $0{,}032$ | $0{,}031566$ | ✓ |
| Ví dụ 09.5, dòng 291, 293 | $0{,}200$ ($0{,}137$–$0{,}245$); $0{,}994$ ($0{,}915$–$1{,}066$) | $0{,}199502$ [$0{,}136720$; $0{,}245465$]; $0{,}994415$ [$0{,}915396$; $1{,}066030$] | ✓ |
| Ví dụ 09.11, dòng 727–731 | $\operatorname{Var}(2\zeta-\zeta^2)=4+2-0=6$ | hệ số chéo $2\cdot2\cdot(-1)=-4$, đúng; Monte Carlo $5{,}994$ | ✓ |
| Ví dụ 09.13, dòng 775 | $\tfrac14\cdot0{,}6^{199}$; $50\cdot\tfrac14\cdot0{,}6^{199}\approx8{,}9\cdot10^{-44}$ | $1{,}778\cdot10^{-45}$; $8{,}892\cdot10^{-44}$ | ✓ |

## Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | dòng 851 (N2) | Với thuật toán EM (§8), phân bố lấy kì vọng là $q_i=p_{\theta_t}(\cdot\mid x^{(i)})$, cũng phụ thuộc tham số (giá trị hiện tại $\theta_t$). Câu "là $q_\phi$" không bao trường hợp này. Câu vẫn đúng nếu hiểu $q_i$ là một phân bố biến phân do thuật toán chọn. | "phân bố lấy kì vọng duy nhất phụ thuộc tham số đang tối ưu là $q_\phi$, và thuật toán học chọn nó"; dòng 643–644. | "…là phân bố biến phân ($q_\phi$, hoặc $q_i$ ở bước E của EM), và thuật toán học chọn nó." |
| nhẹ | Định nghĩa 09.6, dòng 303, 306 | $\ell_{\mathrm{len}}=\ell/n(x)$ chưa xác định khi $n(x)=0$ (chuỗi rút ngay $\mathtt E$). Định nghĩa không loại trường hợp này. Mệnh đề "tỉ lệ với $p_D(x)/n(x)$" ở dòng 309 cũng cần nó. | "chuỗi $x$ có $n(x)$ kí tự trước $\mathtt E$"; ví dụ của Nhận xét 09.5 có $n\ge1$. | Thêm "$n(x)\ge1$" (vị trí $1$ không rút $\mathtt E$), như ví dụ của Nhận xét 09.5. |
| nhẹ | Phụ lục D, câu sau $\square$ của Hệ quả 09.13, dòng 1018 | "Bước M chỉ cần làm tăng" hẹp hơn điều cần: chỉ cần *không làm giảm* tổng. Khi bỏ cực đại hóa, Bước 1 cũng không còn dựa được vào "giá trị lớn nhất hữu hạn". Tính hữu hạn khi đó đến từ bất đẳng thức: tổng tại $\theta_{t+1}$ $\ge$ tổng tại $\theta_t>-\infty$, mỗi số hạng $<+\infty$ vì $\mathcal V$ hữu hạn. | Dòng 1005 dùng "Giá trị lớn nhất ở bước M hữu hạn". | "Bước M chỉ cần $\sum_i\mathbb E_{q_i}\ln p_{\theta_{t+1}}(x^{(i)},v)\ge\sum_i\mathbb E_{q_i}\ln p_{\theta_t}(x^{(i)},v)$; vế phải hữu hạn, nên Bước 1 vẫn đúng và dòng thứ hai của dãy bất đẳng thức vẫn đúng." |
| nhẹ | Ví dụ 09.8 Bước 1, dòng 458 | "số hạng thứ $j$ có kì vọng bằng entropy của hàng ứng với $x_{j-1}$" thật ra là kì vọng có điều kiện theo $x_{j-1}$. Kì vọng không điều kiện bằng $1{,}0889$ vì mọi hàng có cùng entropy. Kết quả không đổi. | Dòng 458. | "…có kì vọng có điều kiện, khi biết $x_{j-1}$, bằng entropy của hàng ứng với $x_{j-1}$; mọi hàng có cùng entropy …, nên kì vọng bằng $1{,}0889$." |
