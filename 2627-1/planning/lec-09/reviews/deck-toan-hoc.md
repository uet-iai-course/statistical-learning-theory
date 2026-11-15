# Duyệt deck Bài 09 — Vai 2 `toan-hoc` (độ chính xác toán học, thống nhất với ghi chú)

Bản duyệt: `2627-1/lecture-09-hoc-chuoi-mo-hinh-sinh.html` (đóng băng, 55 trang), `img/lec-09/cua-so-chong-lan.svg` (F1), `img/lec-09/elbo-theo-mu.svg` (F2). Đối chiếu: `materials/lec-09/lecture-note.md`, `exercises.md`, storyboard V1–V25, `review-log.md` § Bộ trang chiếu; kết quả dẫn từ bài trước kiểm trong ghi chú Bài 01 ((T1), (T2)), Bài 02 ((T3), Hệ quả 02.10, Nhận xét 02.11, đoạn về miền $[a,b]$), Bài 05 ((C), (G1), (G2), $\bar w_T$, Hệ quả 05.15). `deck_lint.py`: 0 phát hiện.

## 1. Tính lại các con số

Mọi số được tính lại bằng Python độc lập (tệp nháp `scratchpad/lec-09/rv-toan-hoc/calc.py`), kèm Monte Carlo $4\cdot10^6$ lần rút cho Ví dụ 09.11.

| Nhóm | Trang | Kết quả tính lại | Kết luận |
|---|---|---|---|
| V1 | 1-06 | $-\ln0{,}8=0{,}22314$; $0{,}168$; $1{,}78379=0{,}51083+0{,}35667+0{,}91629$ | khớp |
| V2 | 2-02 | $0{,}58$; $0{,}7\ne0{,}4$ | khớp |
| V3 | 2-03 | $\ln(0{,}1\sqrt{2\pi})=-1{,}38365$ | khớp |
| V4 | 2-05 | $0{,}6931$; $0{,}6325$; $0{,}6109$; $0{,}6390$; $0{,}7\cdot0{,}3567+0{,}3\cdot1{,}2040$ | khớp |
| V5 | 2-06 | $L_s=\tfrac12\ln(2\pi\sigma^2)\to-\infty$ | khớp |
| V6 | 3-03 | $0{,}59460$; $0{,}168^{-1/3}=1{,}81230$ | khớp |
| V7 | 3-05 | $\ln50=3{,}91202$, $0{,}97801$, $2{,}65915$; $2{,}05573$, $0{,}51393$, $1{,}67185$; $0{,}40$; $0{,}69$ | khớp |
| V8 | 3-06, 3-07 | $b=599{,}146$; $0{,}192065$; $115{,}075\le115{,}08$; $0{,}575374\le0{,}5754$; $0{,}040685$; $6621{,}10\to6622$; kiểm thêm $m_v=6622$ cho $0{,}049997\le0{,}05$ | khớp |
| V9 | 3-08 | $0{,}2^{10}=1{,}024\cdot10^{-7}$; $0{,}8\cdot0+0{,}2\cdot1$ | khớp |
| V10 | 3-09 | cực tiểu $\tfrac16$ và $\tfrac12$; trọng số $\tfrac14$, $\tfrac1{20}$ | khớp |
| V11 | 4-01 | $0{,}022582$; $0{,}021601$ | khớp |
| V12 | 4-05 | $0{,}673012$; $0{,}695594$; $0{,}610864$; $0{,}084730$ | khớp |
| V13 | 4-06 (+ ghi chú diễn giả) | $1{,}2040$; $3{,}4544$; $6{,}9078$; $\ln2{,}5$; $\ln1{,}25$; $0{,}99^m$: $0{,}90438$, $0{,}60501$, $0{,}36603$; $0{,}99^{68}=0{,}50489$, $0{,}99^{69}=0{,}49984$; $0{,}058736$; $0{,}056002$ | khớp |
| V14 | 4-07 | $1{,}088900$; $1{,}090387$; $e^{1{,}0904}=2{,}9754$ | khớp |
| V15 | 4-08 | $1{,}03972$; $\ln3=1{,}09861$; $0{,}05889$; $0{,}05663$; $\tfrac12\ln2=0{,}34657$ | khớp |
| V16 | 5-01 | $-\tfrac12\ln(4\pi)-1=-2{,}265512$; hậu nghiệm $N(1,\tfrac12)$; câu ôn 3: $0{,}4$, $0{,}75$ | khớp |
| V17 | 5-04 | bốn dòng tái tạo/KL/ELBO/khe: $-3{,}4189/0/-3{,}4189/1{,}1534$; $-1{,}9189/0{,}5/-2{,}4189/0{,}1534$; $-1{,}8889/0{,}4166/-2{,}3055/0{,}0400$; $-1{,}6689/0{,}5966/-2{,}2655/0$; khe tính độc lập bằng $\mathrm{KL}(q_\phi\Vert N(1,\tfrac12))$ trùng cả bốn dòng | khớp |
| V18 | 5-06 | $\rho_0(1{,}5)=0{,}129518$, $\rho_0(0{,}5)=0{,}352065$; $0{,}240791$; $-1{,}423824$; $0{,}731059$; ELBO $-1{,}543939$/$-1{,}512003$; khe $0{,}120115$/$0{,}088179$ = KL tới hậu nghiệm; tái tạo $-1{,}143939$; KL tiên nghiệm $0{,}368064$ | khớp |
| V19 | 6-05 | $(2-\zeta,\,2\zeta-\zeta^2)$; $(1{,}5;0{,}75)$, $(3;-3)$; phương sai $1$, $6$; gradient log $29{,}0270$ (Monte Carlo: kì vọng $2{,}0002$, phương sai $29{,}09$; thành phần $\sigma$: $6{,}004$) | khớp |
| V20 | 6-06 | $e^{-1/8}/\sqrt{2\pi}=0{,}352065$; $1/0{,}3-1=2{,}3333$ | khớp |
| V21 | 6-07 | $\ln100=4{,}60517$; $1{,}418939$; $1{,}424812\le1{,}4249$; $\tfrac12\ln(50\pi)+\tfrac1{50}=2{,}548376$; $50\cdot\tfrac14\cdot0{,}6^{199}=8{,}892\cdot10^{-44}$ | khớp |
| V22 | 6-08 | $\mathbb E\lVert\varphi\rVert^2$ tại bốn góc: $12$; $8$; $9{,}75$; $5{,}75$ (hai ngoặc lồi, nên cực đại ở góc); $G=3{,}46410$; $R=2{,}06155$; $\eta=0{,}005951$; $\sqrt{51}/100=0{,}071414\le0{,}0715$ | khớp |
| V23 | 7-03 | $2{,}441847$; $0{,}096032$; $0{,}234496\le0{,}2345$; $57{,}2$ | khớp |
| V24 | 7-04 | $0{,}096$; $2{,}34341$; $0{,}78114$; $2{,}18395$; $0{,}0400$ | khớp |
| V25 | 1-02 | $0{,}192065\le0{,}1921$ | khớp |
| F1 | 3-08 | 12 ô $j-10,\ldots,j+1$; ngoặc trên phủ $j-10..j-1$ (x 43–637), đích $j$; ngoặc dưới phủ $j-9..j$ (x 103–697), đích $j+1$; 9 ô tô nền $j-9..j-1$ $=k-1$; ô $j$ gạch chéo | đúng với Định nghĩa 09.1, Ví dụ 09.5, Bước 1 |
| F2 | 5-04 | Trục: $y=24+127{,}16(-2-\mathrm{ELBO})$, $x=92+179{,}33(\mu+0{,}5)$. Đường ngang $y=57{,}8\leftrightarrow-2{,}2655$; đầu mút hai parabol tại $\mu=-0{,}5$: $-4{,}5155\to343{,}9$ (vẽ $343{,}8$), $-4{,}6689\to363{,}4$ (vẽ $363{,}3$); bốn điểm $(0;-3{,}4189)\to204{,}4$, $(1;-2{,}4189)\to77{,}3$, $(0{,}8;-2{,}3055)\to62{,}8$, $(1;-2{,}2655)\to57{,}8$; hai parabol cách nhau $0{,}5-\tfrac12\ln2=0{,}1534$ tại mọi $\mu$; mũi tên tại $\mu=0$ từ điểm vuông tới đường ngang $=1{,}1534$ | đúng |

Mọi phát biểu kết quả đã đối chiếu từng giả thiết với khối ghi chú (bảng ở mục 3). Các điểm brief nêu: quy ước tích bằng $0$ (3-01, đúng), $p_1(x_{<j})>0$ (3-01 Kí hiệu, đúng), hàm lỗi log không bị chặn (2-03, 3-07 ghi chú diễn giả, 4-06, đúng), $c>0$ cho cận hữu hạn mẫu (3-06, 7-02, 7-03, đúng), "mô hình cố định, trên tập kiểm tra" (3-06, 7-02 dòng 3, 7-03, đúng; N1 của cổng đã sửa), quan sát độc lập ở cấp chuỗi (2-02, 3-06, 3-07, đúng), KL và ELBO (4-01, 5-02, đúng), tái tham số hóa (6-01, đúng), đổi chỗ đạo hàm và kì vọng (6-02 đúng; 6-04 có lỗi "cần/đủ", phát hiện 3).

## 2. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | L09-4-03 (ghi chú diễn giả) | Khẳng định sai về chỗ giả thiết $\mathrm H(p_D)<\infty$ hỏng. Khi $\mathrm H(p_D)=\infty$, không có dạng $\infty-\infty$: tổng thứ nhất có số hạng không âm, phần âm của các số hạng KL có tổng không quá $\sum p_\theta\le1$ (chính 4-01 ghi chú diễn giả nói KL xác định trong $(-\infty,\infty]$), nên (a) vẫn đúng với hai vế $+\infty$. Chỗ giả thiết thật sự cần là vế sau của (b) ("$L_D\ge\mathrm H$, dấu bằng khi và chỉ khi"): khi $\mathrm H=\infty$, mọi mô hình có $L_D=+\infty=\mathrm H$, nên "chỉ khi" hỏng; và phép trừ của Hệ quả 09.9. "Chỗ duy nhất" cũng trái ghi chú, Bước 3 viết "Vế sau của (b) suy ra từ (a), vì $\mathrm H(p_D)$ hữu hạn". | Deck: "Bước 2 là chỗ duy nhất dùng $\mathrm H(p_D)<\infty$ … Bỏ giả thiết này, hai tổng có thể có dạng $\infty-\infty$." Ghi chú §7, chứng minh Mệnh đề 09.8, Bước 2 ("ta cộng được hai tổng … giả thiết entropy hữu hạn dùng ở đây") và Bước 3 ("Vế sau của (b) suy ra từ (a), vì $\mathrm H(p_D)$ hữu hạn"); đoạn sau Định nghĩa 09.7. | Thay hai câu bằng: "Bước 2 dùng $\mathrm H(p_D)<\infty$ để cộng hai tổng theo từng số hạng; vế sau của (b) dùng lại nó qua (a). Bỏ giả thiết này, mọi mô hình có $L_D=+\infty=\mathrm H(p_D)$, nên điều kiện dấu bằng của (b) và phép trừ ở Hệ quả 09.9 mất nghĩa." |
| trung bình | L09-7-04 (câu 4 và lời giải trong ghi chú diễn giả) | Lời giải chưa đủ theo ghi chú: ghi chú dùng $\mathrm H(p_D)<\infty$ ở Bước 2 và ở vế sau của (b), Bước 3. Câu hỏi tự kiểm tra phải trả lời được chỉ bằng ghi chú; người đọc ghi chú sẽ đưa ra hai chỗ. | Deck: "Bước 2, cộng hai tổng theo từng số hạng: tổng $\sum p_D(-\ln p_D)$ hữu hạn nên phép cộng hợp lệ." Ghi chú, chứng minh Mệnh đề 09.8, Bước 3, câu cuối. | Lời giải: "Bước 2 (cộng hai tổng theo từng số hạng) và vế sau của (b) ở Bước 3, suy từ (a) vì $\mathrm H(p_D)$ hữu hạn." |
| trung bình | L09-6-04 (mặt trang, dòng "Kỹ thuật.") | Điều kiện cần/đủ: dòng kỹ thuật viết đẳng thức đổi chỗ đúng "khi phân bố của $\zeta$ không phụ thuộc $\phi$", như thể một điều kiện này đủ. Ví dụ 09.12 trên chính deck là phản ví dụ (phân bố của $\zeta$ không phụ thuộc $\mu$, đẳng thức sai). Dòng sau mới nêu "Điều kiện đủ". | Deck: "$\nabla_\phi\mathbb E\kappa(\phi,\zeta)=\mathbb E\nabla_\phi\kappa(\phi,\zeta)$ khi phân bố của $\zeta$ không phụ thuộc $\phi$." Ghi chú Mệnh đề 09.15: sáu giả thiết, trong đó (i)–(iii). | "… với $\zeta$ có phân bố không phụ thuộc $\phi$, khi ba điều kiện sau thỏa:" rồi giữ dòng điều kiện; hoặc gộp hai dòng. |
| trung bình | L09-6-04 (ghi chú diễn giả) | Khái quát không có cơ sở và sai: một hàm có bước nhảy theo $\phi$ không nhất thiết có đạo hàm bằng $0$ trên từng đường, và đạo hàm của kì vọng không nhất thiết khác $0$ (ví dụ $\kappa=\phi+\mathbb 1[\phi+\zeta>0]$ có đạo hàm $1$ hầu chắc chắn). Ghi chú chỉ nói điều này cho hàm chỉ báo của Ví dụ 09.12. | Deck: "Với một hàm có bước nhảy theo $\phi$, đạo hàm trên từng đường bằng $0$ hầu chắc chắn trong khi đạo hàm của kì vọng khác $0$." Ghi chú Ví dụ 09.12, Bước 2–4. | "Với hàm chỉ báo $\mathbb 1[\mu+\zeta>0]$ và biến Bernoulli của Ví dụ 09.12, đạo hàm trên từng đường bằng $0$ hầu chắc chắn, trong khi đạo hàm của kì vọng bằng $0{,}3521$ và $1$." |
| trung bình | L09-6-03 (ghi chú diễn giả, câu cuối) | Bỏ giả thiết: phát biểu gradient một lần rút là gradient ngẫu nhiên không chệch của $-\frac1m\sum_i\operatorname{ELBO}$ mà không có điều kiện của ghi chú. | Deck: "Với $\xi=(i,\zeta)$, $i$ rút đều, gradient một lần rút là gradient ngẫu nhiên không chệch của $-\frac1m\sum_i\operatorname{ELBO}(\theta,\phi;x^{(i)})$". Ghi chú §9, đoạn sau chứng minh Mệnh đề 09.15: "Nếu với mỗi $i$, $\kappa_i$ thỏa (i)–(iii) của Mệnh đề 09.15 với $(\theta,\phi)$ ở chỗ của $\phi$, thì …". | Thêm "khi mỗi $\kappa_i$ thỏa (i)–(iii) theo $(\theta,\phi)$" vào câu. |
| nhẹ | L09-2-03 (mặt trang dòng 3; ghi chú diễn giả) | Xác suất có điều kiện $\ge c$ cho $\ell\le n\ln(1/c)$ chỉ khi độ dài bị chặn; với độ dài thay đổi (Định nghĩa 09.6) hàm lỗi vẫn không bị chặn. Deck theo đúng ghi chú, nhưng câu "cận … áp dụng khi mọi xác suất … $\ge c>0$" thiếu điều kiện này. | Ghi chú §2: "Với mô hình rời rạc, điều này đúng khi các xác suất bị chặn dưới bởi $c>0$"; Ví dụ 09.4, Bước 1 dùng $n=200$ cố định. | Thêm "độ dài cố định" vào dòng 3; xem đề xuất sửa ghi chú 1. |
| nhẹ | L09-2-02 | Thứ tự: "Ví dụ 09.1" (ghi chú §3) đứng trước "Định nghĩa 09.1" (§1) trên cùng trang. Không sai toán; dữ liệu đã có ở 1-06. Thiết lập B thiếu chỉ số $j=k+1,\ldots,n$ và "nói chung" của câu "các cửa sổ nói chung phụ thuộc nhau". | Ghi chú §1, Định nghĩa 09.1 và đoạn sau; §3. | Giữ, hoặc đưa dòng Ví dụ 09.1 xuống sau Định nghĩa 09.1; thêm "$j=k+1,\ldots,n$". |
| nhẹ | L09-3-08 (mặt trang dòng 2) | "$0{,}8\cdot0+0{,}2\cdot1=0{,}2$" viết là đẳng thức cho MSE; ghi chú viết "xấp xỉ" (xác suất $u_{j+1}$ thuộc tập huấn luyện là khoảng $0{,}8$; cửa sổ cuối không có $u_{j+1}$). | Ghi chú Ví dụ 09.5, Bước 2: "MSE … xấp xỉ $0{,}8\cdot0+0{,}2\cdot1=0{,}2$". | "MSE $\approx0{,}8\cdot0+0{,}2\cdot1=0{,}2$". |
| nhẹ | L09-3-09 (ghi chú diễn giả) | Trọng số lẫn hai mức: "trọng số $1/n$: $\tfrac14$ với chuỗi ngắn" — $1/n$ với $n=2$ là $\tfrac12$; $\tfrac14=\tfrac12\cdot\tfrac12$ đã nhân xác suất $D(\mathtt{11})$. Ngoài ra, ví dụ bỏ số hạng của $\mathtt E$ (có tham số riêng) mà deck không nói, trong khi Định nghĩa 09.6 trên cùng trang có số hạng đó. | Ghi chú §6 đoạn sau Định nghĩa 09.6 ("trọng số $1/n$"); Ví dụ 09.6, Thiết lập và Bước 3 ("$\tfrac12\cdot\tfrac12=\tfrac14$"). | "… mỗi kí tự có trọng số $D(x)/n(x)$: $\tfrac12\cdot\tfrac12=\tfrac14$ với chuỗi ngắn, $\tfrac12\cdot\tfrac1{10}=\tfrac1{20}$ với chuỗi dài"; thêm "Xác suất của $\mathtt E$ có tham số riêng, nên số hạng của nó là hằng theo $\theta$ và được bỏ." |
| nhẹ | L09-4-02 (mặt trang, dòng (c)) | "như trên với $\mathrm h(p_D)$" có thể đọc là cả "trong $[0,\infty]$" của (a) và "$L_D\ge\mathrm h\ge0$"; với mật độ, $L_D$ và $\mathrm h(p_D)$ có thể âm (chỉ có trong ghi chú diễn giả). | Ghi chú Mệnh đề 09.8(c): "$\mathrm{KL}\ge0$ và dấu bằng khi và chỉ khi $p_\theta=p_D$ hầu khắp nơi; $\mathrm h(p_D)$ có thể âm". | "(c) Mật độ, …: $L_D=\mathrm h(p_D)+\mathrm{KL}$, $\mathrm{KL}\ge0$, bằng $0$ khi và chỉ khi $p_\theta=p_D$ hầu khắp nơi; $\mathrm h(p_D)$ có thể âm." |
| nhẹ | L09-4-07 | Công thức trên mặt trang có $\ln4$ mà mặt trang không nói kí tự đầu rút đều. Ghi chú diễn giả "cách giá trị tốt nhất khoảng $0{,}0009$" không suy ra được từ số trên trang ($1{,}091-1{,}0904=0{,}0006$); số $0{,}0009$ đúng với giá trị chưa làm tròn (khoảng $1{,}0913$), ghi chú cũng vậy. | Ghi chú Ví dụ 09.8, Thiết lập ("kí tự đầu rút đều") và (i). | Thêm "kí tự đầu đều" vào dòng Ví dụ 09.8; trong ghi chú diễn giả viết "khoảng $0{,}0009$ (theo trung bình chưa làm tròn)" hoặc bỏ số; xem đề xuất sửa ghi chú 2. |
| nhẹ | L09-5-03 (ghi chú diễn giả) | "Khi bỏ giả thiết về $q$: với $x=v\sim N(0,1)$ …": ví dụ khối lượng điểm làm hỏng trước hết giả thiết "Mô hình: $p_\theta(x,v)$ là mật độ"; ghi chú đặt nó sau Định nghĩa 09.10, không gắn với giả thiết về $q$. | Ghi chú §8, đoạn sau Định nghĩa 09.10; Định lý 09.12, Giả thiết "Mô hình". | "Khi mô hình không có mật độ liên hợp: với $x=v$ …, hậu nghiệm là khối lượng điểm …". |
| nhẹ | L09-5-04 (bảng) | Cột "KL" cạnh cột "Khe" (cũng là một KL, tới hậu nghiệm) dễ nhầm; ghi chú ghi rõ "Cột KL … là KL tới tiên nghiệm". | Ghi chú Ví dụ 09.10, Bước 2. | Tiêu đề cột "KL tới tiên nghiệm" (hoặc "KL tiên nghiệm"). |
| nhẹ | L09-5-04 (F2, `elbo-theo-mu.svg`) | Nhãn "ln p(2) ≈ −2,2655" bỏ chỉ số $\theta$; chú thích dưới hình và ghi chú viết $\ln p_\theta(2)$. Số và tọa độ đúng (mục 1). | Ghi chú Ví dụ 09.9–09.10. | Nhãn "ln p<sub>θ</sub>(2) ≈ −2,2655". |
| nhẹ | L09-5-05 | Mặt trang dùng $\operatorname{ELBO}(\theta_{t+1},q_i;x^{(i)})$, nhưng kí hiệu $\operatorname{ELBO}(\theta,q;x)$ (đối số thứ hai là hàm xác suất $q$, không phải $\phi$) chỉ định nghĩa trong ghi chú diễn giả. | Ghi chú §8, đoạn trước Hệ quả 09.13. | Thêm vào dòng 1: "viết $\operatorname{ELBO}(\theta,q;x)$ với $q$ cho trước". |
| nhẹ | L09-6-00 (dòng dẫn) | "đạo hàm vào được trong kì vọng khi hàm khả vi, khả tích": hàm chỉ báo của Ví dụ 09.12 khả vi tại từng $\mu$ hầu chắc chắn mà đẳng thức vẫn sai; điều kiện là khả vi liên tục trên từng đường nhiễu với tập ngoại lệ chung, cộng hàm trội. | Ghi chú Ví dụ 09.12, Bước 3 ("khả vi tại từng $\mu$ hầu chắc chắn chưa đủ"). | "… khi hàm khả vi trên từng đường nhiễu và bị chặn bởi một hàm khả tích." |
| nhẹ | L09-7-01 (hàng 2) | "Giả thiết không được bỏ: $\mathcal X$ đếm được": bản mật độ (c) thay điều kiện này bằng hai điều kiện khả tích, nên nó không phải giả thiết "không được bỏ". | Ghi chú Mệnh đề 09.8(c). | "$\mathrm H(p_D)<\infty$ (mật độ: hai điều kiện khả tích)". |

## 3. Bảng thống nhất trang → khối ghi chú

"Khớp" nghĩa là kí hiệu, nhãn giả thiết, số hiệu, dữ liệu và kết quả trùng ghi chú; lệch ghi ở cột cuối (số phát hiện ở mục 2).

| Trang | Khối ghi chú / bài tập | Thống nhất |
|---|---|---|
| 1-01 | đoạn mở đầu, §10 | khớp |
| 1-02 | Kiến thức tiên quyết; (T1), (T2) Bài 01; (T3), Hệ quả 02.10(b), Nhận xét 02.11, đoạn miền $[a,b]$ Bài 02; câu ôn nhanh 1–2 | khớp (dạng "với xác suất ít nhất $1-\delta$" tương đương 02.10(a)–(b)) |
| 1-03 | Mục tiêu học tập 1–5 | khớp |
| 1-04, 1-05 | đoạn mở đầu, §13 | khớp |
| 1-06 | Câu hỏi mở đầu | khớp |
| 2-01 | §1, bảy thành phần; khối ứng dụng §3 | khớp |
| 2-02 | Định nghĩa 09.1, đoạn sau; Ví dụ 09.1 | khớp; thứ tự §3 trước §1 (nhẹ) |
| 2-03 | §2: ba điểm của hàm lỗi log, (T1), (T7) | khớp; điều kiện độ dài (nhẹ, theo ghi chú) |
| 2-04 | Định nghĩa 09.2 và ba đoạn sau | khớp |
| 2-05 | Ví dụ 09.2 | khớp |
| 2-06 | Bài tập 09.8(c) | khớp đề và lời giải |
| 3-01 | Mệnh đề 09.3 | khớp (quy ước tích $0$, $p_1(x_{<j})>0$, (c) với $Q_n$) |
| 3-02 | Phụ lục D, chứng minh Mệnh đề 09.3; Ví dụ 09.3, Bước 5 | khớp |
| 3-03 | Định nghĩa 09.4, đoạn sau; Ví dụ 09.3 | khớp |
| 3-04, 3-05 | Bài tập 09.1(a), (c) | khớp đề, bảng và lời giải |
| 3-06 | §6 đoạn mở; Ví dụ 09.4, Bước 1–2 | khớp ("cố định, không phụ thuộc $V$", $c=0{,}05$, xác suất theo tập kiểm tra) |
| 3-07 | Ví dụ 09.4, Bước 3–5 | khớp |
| 3-08 | Ví dụ 09.5; Phụ lục C | khớp; "$=0{,}2$" thay "xấp xỉ" (nhẹ) |
| 3-09 | Nhận xét 09.5; Định nghĩa 09.6; Ví dụ 09.6 | khớp mặt trang; ghi chú diễn giả về trọng số (nhẹ) |
| 4-01 | Định nghĩa 09.7 và ba đoạn sau | khớp |
| 4-02 | Mệnh đề 09.8 | khớp (a), (b); (c) mơ hồ (nhẹ) |
| 4-03 | chứng minh Mệnh đề 09.8 | các bước khớp; ghi chú diễn giả sai về $\mathrm H<\infty$ (nghiêm trọng) |
| 4-04 | Hệ quả 09.9 và chứng minh | khớp |
| 4-05 | câu hỏi và đoạn sau Hệ quả 09.9 | khớp |
| 4-06 | Ví dụ 09.7 | khớp |
| 4-07 | Ví dụ 09.8; khối ứng dụng §3; Phụ lục C | khớp số; $\ln4$, $0{,}0009$ (nhẹ) |
| 4-08 | Bài tập 09.3(b), (c) | khớp đề và lời giải |
| 5-01 | Định nghĩa 09.10; Ví dụ 09.9; Phụ lục A(ii) | khớp |
| 5-02 | Định nghĩa 09.11; Định lý 09.12 | khớp (bốn giả thiết, "tất định", (a)–(c); (d) và Phạm vi ở ghi chú diễn giả) |
| 5-03 | chứng minh Định lý 09.12 | khớp; gán nhãn ví dụ khối lượng điểm (nhẹ) |
| 5-04 | Ví dụ 09.10; Phụ lục A(iii) | khớp; tiêu đề cột KL, nhãn F2 (nhẹ) |
| 5-05 | Hệ quả 09.13; Phụ lục D | khớp; kí hiệu $\operatorname{ELBO}(\theta,q;x)$ (nhẹ) |
| 5-06 | Bài tập 09.4(b) | khớp đề và lời giải |
| 6-01 | §9 đoạn mở; Định nghĩa 09.14 và đoạn sau | khớp |
| 6-02 | Mệnh đề 09.15 | khớp (sáu giả thiết, bảo đảm theo kì vọng theo $\zeta$, điều kiện đủ ở ghi chú diễn giả) |
| 6-03 | chứng minh Mệnh đề 09.15; Phụ lục B; đoạn sau | các bước khớp; câu ELBO thiếu điều kiện (trung bình) |
| 6-04 | Mệnh đề 09.15; Phụ lục B | "khi" chỉ một điều kiện (trung bình); khái quát hàm nhảy (trung bình) |
| 6-05 | Ví dụ 09.11; Phụ lục A(iv) | khớp |
| 6-06 | Ví dụ 09.12; §12 câu (d) | khớp |
| 6-07 | Ví dụ 09.13 và đoạn sau | khớp |
| 6-08 | Bài tập 09.7(c), (d); Hệ quả 05.15(a)–(b); (C), (G1), (G2) Bài 05 | khớp; "Nhắc lại:" đủ (C), (G1), (G2), $\lVert w_1-u\rVert\le R$ trên $W$ |
| 7-01 | §10 | khớp; "$\mathcal X$ đếm được" (nhẹ) |
| 7-02 | §10 | khớp (giữ "mô hình cố định", "$c>0$", "trên $m_v$ chuỗi kiểm tra", "xác suất $\ge1-\delta$") |
| 7-03 | Bài tập 09.6(b) | khớp đề và lời giải |
| 7-04 | §12 câu (a)–(c); chứng minh Mệnh đề 09.8 | câu 1–3 khớp; câu 4 thiếu Bước 3 (trung bình) |
| 7-05 | §11; `exercises.md` | khớp; mỗi bài ở mạch cung cấp kiến thức cuối cùng (09.4, 09.7 ở mạch 6 vì cần Mệnh đề 09.15) |
| 7-06 | §12 đoạn cuối, §13 | khớp |

## 4. Kiểm ý tưởng chứng minh

- 3-02: bốn bước đúng; trường hợp tiền tố xác suất $0$ ở bước riêng; "mỗi hàng có tổng $1$" vào đúng bước (c).
- 4-03: bốn bước đúng; $\ln t\le t-1$ đúng tên và đúng chỗ; điều kiện dấu bằng đúng. Chỉ sai ở ghi chú diễn giả (phát hiện nghiêm trọng).
- 5-03: bốn bước đúng; khả tích vào ở Bước 3; (b) dùng lại lập luận của Mệnh đề 09.8(b), (c).
- 5-05: dãy bất đẳng thức khớp Phụ lục D; điều kiện của Định lý 09.12 tại $\theta_{t+1}$ được nêu ở ghi chú diễn giả.
- 6-03: định lý giá trị trung bình dùng (i), hàm trội dùng (ii), hội tụ bị chặn dùng (iii), liên tục của đạo hàm riêng kéo theo khả vi; vai trò tập ngoại lệ chung đúng.
- Phản ví dụ: Bài tập 09.8(c) (mật độ không bị chặn dưới), Ví dụ 09.7 (bỏ $c>0$), phép đếm theo kí tự (bỏ độc lập), Ví dụ 09.5 (bỏ (T7)), Ví dụ 09.12 (bỏ (i)): đều đúng.

## 5. Đề xuất sửa ghi chú

1. **§2, giả thiết "Xác suất bị chặn dưới" và đoạn trước nó (nhẹ).** $p_\theta(x_j\mid x_{<j})\ge c$ cho $\ell\in[0,n\ln(1/c)]$ chỉ khi độ dài $n$ cố định (hoặc bị chặn); với độ dài thay đổi (Định nghĩa 09.6) hàm lỗi vẫn không bị chặn. Đề xuất: "Với mô hình rời rạc và độ dài cố định $n$, điều này đúng khi …".
2. **Ví dụ 09.8, câu (i) (nhẹ).** "lỗi kiểm tra $1{,}091$ cách giá trị tốt nhất khoảng $0{,}0009$": từ số in trong bảng ($1{,}091$) và $1{,}0904$ chỉ tính được $0{,}0006$. Đề xuất ghi trung bình chưa làm tròn (bốn chữ số) hoặc viết "khoảng $0{,}001$". (Bổ sung cho đề xuất đã có về "khoảng $0{,}032$" ở Bước 4.)
3. **Chứng minh Mệnh đề 09.8, Bước 2 (nhẹ, tùy chọn).** Phép cộng theo từng số hạng vẫn hợp lệ khi $\mathrm H(p_D)=\infty$ (phần âm của các số hạng KL có tổng hữu hạn), nên (a) đúng với hai vế $+\infty$. Giả thiết $\mathrm H(p_D)<\infty$ cần cho điều kiện dấu bằng ở vế sau của (b) và phép trừ của Hệ quả 09.9. Có thể thêm một câu như vậy để người đọc không suy ra (như deck đã suy ra) rằng bỏ giả thiết sẽ gây dạng $\infty-\infty$.

## 6. Kết luận

0 chặn bàn giao, 1 nghiêm trọng, 4 trung bình, 12 nhẹ. Mọi con số trên mặt trang, ghi chú diễn giả và hai SVG tính lại đều khớp ghi chú và `exercises.md`. Các lỗi nằm ở phát biểu "cần/đủ" và ở ghi chú diễn giả.

**Kết luận: đạt khi sửa.**
