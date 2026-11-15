# Duyệt deck Bài 05 — Vai 2 `toan-hoc` (độ chính xác toán học, thống nhất với ghi chú)

Bản duyệt: `2627-1/lecture-05-ha-gradient-ngau-nhien.html` (đóng băng, 55 trang) và năm SVG trong `2627-1/img/lec-05/`. Đối chiếu: `materials/lec-05/lecture-note.md`, `exercises.md`, quyết định ở `review-log.md` § "Bộ trang chiếu". Tác tử: general-purpose, Opus 5.5, effort high (do điều phối viên ghi từ lời gọi). Chỉ đọc; không commit.

Mọi con số được tính lại độc lập bằng Python (`/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-05/rv-toan-hoc/check.py`, `poly.py`); tọa độ SVG được đổi ngược về giá trị theo thang của từng hình.

## 1. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L05-2-03, mặt trang | Câu về dưới vi phân bỏ giả thiết lồi ở vế thứ hai, nên mâu thuẫn với chính hình của trang. | Deck: "Dưới vi phân … $\partial F(w)$: tập mọi dưới gradient; khác rỗng khi $F$ lồi, bằng $\{\nabla F(w)\}$ khi $F$ khả vi." Hình bên trái trang là $f(w)=(w^2-1)^2$, khả vi tại $0$ nhưng $\partial f(0)=\varnothing$ (với mọi $v$, $u=\pm1$ cho $0\ge1\pm v$, vô lí). Ghi chú dòng 224: "Với $F$ lồi và hữu hạn trên $\mathbb R^p$, dưới vi phân tại mọi điểm khác rỗng, và $\partial F(w)=\{\nabla F(w)\}$ khi $F$ khả vi tại $w$"; dòng 228: $0\notin\partial f(0)$. | "Với $F$ lồi: $\partial F(w)\ne\varnothing$, và $\partial F(w)=\{\nabla F(w)\}$ khi $F$ khả vi tại $w$." |
| trung bình | L05-4-01, ghi chú diễn giả | Số của bước thứ hai được dùng để nói "một bước có thể không đưa điểm lặp lại gần $w^*$", trong khi chính các số này bảo đảm điểm lặp lại gần. | Ghi chú diễn giả: "$\langle g_2,w_2-w^*\rangle\approx1{,}3289$ và $\tfrac\eta2\lVert g_2\rVert^2=1$: hai số cùng cỡ, nên một bước có thể không đưa điểm lặp lại gần $w^*$." Với $2\eta=1$: $\lVert w_3-w^*\rVert^2\le0{,}5053-1{,}3289+1=0{,}1764<0{,}5053$; thực tế $\lVert w_2-w^*\rVert\approx0{,}7109\to\lVert w_3-w^*\rVert\approx0{,}0586$ (Ví dụ 05.7). Trường hợp ra xa là bước ba với $i_3=1$ (Bài tập 05.2(c)): $\langle g,w-u\rangle\approx0{,}0236<\tfrac\eta2\lVert g\rVert^2\approx0{,}0858$, khoảng cách $0{,}0586\to0{,}1112$. | Thay bằng: "Ở bước thứ hai, $2\eta\langle g_2,w_2-w^*\rangle\approx1{,}3289$ lớn hơn $\eta^2\lVert g_2\rVert^2=1$, nên điểm lặp lại gần $w^*$. Ở bước thứ ba với $i_3=1$, $\langle g_3,w_3-w^*\rangle\approx0{,}0236$ nhỏ hơn $\tfrac\eta2\lVert g_3\rVert^2\approx0{,}0858$, và khoảng cách tăng từ $0{,}0586$ lên $0{,}1112$." |
| trung bình | L05-7-03, dòng 3 | Dòng rút gọn về bảo đảm với xác suất cao bỏ điều kiện: bất đẳng thức Markov chỉ áp dụng cho đại lượng không âm $\operatorname{opt}_s$ (so với $\inf_W$, $W$ bị chặn, $R\ge\sup_{u\in W}\lVert w_1-u\rVert$); đặt ngay sau dòng 2 với $u$ bất kì, dòng 3 đọc như bảo đảm cho $F(\bar w_T)-F(u)$, có thể âm. | Deck: "Mức $\epsilon$ theo kì vọng: $T\ge R^2G^2/\epsilon^2$; với xác suất ít nhất $1-\delta'$ theo $\xi$: thêm thừa số $1/\delta'^2$." Ghi chú, Hệ quả 05.19: giả thiết "$W$ … bị chặn; $R\ge\sup_{u\in W}\lVert w_1-u\rVert$", bảo đảm (b) cho $\operatorname{opt}_s(\bar w_T)$; chứng minh Bước 3: "Vì $\bar w_T\in W$, $\operatorname{opt}_s(\bar w_T)\ge0$". | "Mức $\epsilon$ theo kì vọng: $T\ge R^2G^2/\epsilon^2$; với $\operatorname{opt}_S$ ($W$ bị chặn), mức $\epsilon_{\mathrm{opt}}$ với xác suất ít nhất $1-\delta'$ theo $\xi$: thêm thừa số $1/\delta'^2$." |
| nhẹ | L05-4-03, "Trực quan." | Số hạng thứ nhất bị mô tả sai lũy thừa và hằng số. | Deck: "Khoảng cách ban đầu chia cho tổng độ dài bước $\eta T$, cộng phần $\eta G^2/2$ mỗi bước góp." Công thức trên cùng trang: $\lVert w_1-u\rVert^2/(2\eta T)$. | "Bình phương khoảng cách ban đầu chia cho $2\eta T$, cộng phần $\eta G^2/2$ mỗi bước góp." |
| nhẹ | L05-4-08, ghi chú diễn giả | Giá trị vế phải của Nhận xét 05.17 viết như đẳng thức với số làm tròn lên. | Ghi chú diễn giả: "Nhận xét 05.17 cho vế phải $0{,}2281$". Tính lại: $\sum_t\eta_t\approx19{,}6380$, $\sum_t\eta_t^2\approx0{,}49721$, vế phải $\approx0{,}22801$; ghi chú, Phụ lục C: "$\approx0{,}2280$"; Nhận xét 05.17: "không quá $0{,}2281$". | "cho vế phải không quá $0{,}2281$". |
| nhẹ | L05-7-05, ghi chú diễn giả | Thừa số chi phí của cách chạy nhiều lần bị nêu thiếu thừa số $4$ do chạy mỗi lần tới mức $\epsilon_{\mathrm{opt}}/2$. | Ghi chú diễn giả: "Cách này thay thừa số $1/\delta'^2$ của bất đẳng thức Markov bằng thừa số $\log_2(1/\delta')$ lần chạy." Tổng $32\,000=1600\cdot4\cdot5$, tức thừa số $4\lceil\log_2(1/\delta')\rceil=20$ so với $400$. | "… bằng $\lceil\log_2(1/\delta')\rceil=5$ lần chạy, mỗi lần gấp $4$ số bước: thừa số $20$ thay cho $400$." |
| nhẹ | L05-4-05, ghi chú diễn giả | Cận trên từng quỹ đạo còn phụ thuộc tổng $\tfrac\eta2\lVert g_t\rVert^2$ dọc quỹ đạo; chỉ sau khi lấy kì vọng và dùng (G2) mới còn $G^2$. | Ghi chú diễn giả: "Cận không phụ thuộc quỹ đạo đi qua đâu, chỉ phụ thuộc khoảng cách ban đầu." Ghi chú, chứng minh Định lý 05.14, Bước 2: vế phải $\Delta_1/(2\eta)+\tfrac\eta2\sum_t\lVert g_t\rVert^2$. | "Các khoảng cách giữa triệt tiêu: cận chỉ còn khoảng cách ban đầu và tổng $\tfrac\eta2\lVert g_t\rVert^2$, sau kì vọng không quá $\eta TG^2/2$." |
| nhẹ | L05-7-06, ghi chú diễn giả câu 1 | "còn tăng" đọc như khoảng cách luôn tăng. | "theo bất đẳng thức một bước, khoảng cách tới $u$ còn tăng do số hạng $\eta^2\lVert g\rVert^2$". Mệnh đề 05.13 chỉ cho phép tăng tối đa $\eta^2\lVert g\rVert^2-2\eta\langle g,w-u\rangle$. | "khoảng cách tới $u$ có thể tăng do số hạng $\eta^2\lVert g\rVert^2$". |
| nhẹ | L05-7-02, hàng Hệ quả 05.16 | Cột "Giả thiết không được bỏ" thiếu độ dài bước, trong khi hàng Hệ quả 05.15 có. | Deck: "(C); $\lVert v(w)\rVert\le G$; $\lVert w_1-u\rVert\le R$". Ghi chú, Hệ quả 05.16: "Thuật toán 05.9 với $\eta=R/(G\sqrt T)$, $R>0$". | Thêm "$\eta=R/(G\sqrt T)$". |
| nhẹ | L05-1-01, luận điểm bìa | Câu đầu đúng (không khẳng định mỗi bước giảm khoảng cách: "tăng không quá một số hạng … có thể âm, cộng một số hạng tỉ lệ với bình phương độ dài bước", khớp Mệnh đề 05.13 viết lại). Câu sau nêu tốc độ $1/\sqrt T$ mà không nêu điều kiện. | Ghi chú, Định lý 05.14: giả thiết (C), (G1), (G2). | "Với hàm mục tiêu lồi, gradient ngẫu nhiên không chệch và có mô-men bậc hai bị chặn, cận …" (bằng lời, không kí hiệu). |
| nhẹ | `img/lec-05/do-dai-buoc.svg` (L05-4-06) | Đường tổng đạt $Q(0{,}1)=0{,}803125$ tại $y=66{,}6$, cao hơn vạch trên cùng $0{,}8$ ($y=67{,}8$); storyboard mục 16 ghi trục dọc $[0;0{,}9]$ nhưng hình không có vạch $0{,}9$. Dữ liệu vẫn nằm trong khung vẽ; yêu cầu "trục chứa $0{,}8031$" của cổng duyệt mới đạt một nửa. | Tọa độ: $0$ tại $y=370$, $0{,}2$ tại $y=294{,}4$ (thang $377{,}75$ px/đơn vị); điểm cuối polyline tổng $(720;66{,}6)$. | Thêm vạch và nhãn $1$ (hoặc $0{,}9$), hoặc ghi lại độ lệch storyboard. |
| nhẹ | `img/lec-05/phep-chieu.svg` (L05-3-01) | Nhãn ảnh chiếu trên hình là "proj", trong khi mặt trang và ghi chú diễn giả dùng $\pi=\operatorname{proj}_W(\theta)$ và Bổ đề 05.8 ở trang sau dùng $\pi$. | Mặt trang: "$\pi=\operatorname{proj}_W(\theta)\approx(0{,}7071;-0{,}7071)$". SVG: `<text …>proj</text>`. | Đổi nhãn thành "π". |

Không có phát hiện chặn bàn giao hoặc nghiêm trọng.

## 2. Các điểm kiểm theo bản giao việc (đều đạt)

- **Luận điểm bìa** không khẳng định mỗi bước giảm khoảng cách (xem dòng nhẹ ở trên về điều kiện của câu sau).
- **Dòng một bước ở L05-7-03** là bất đẳng thức, có $u\in W$: $\lVert w_{t+1}-u\rVert^2\le\lVert w_t-u\rVert^2-2\eta\langle g_t,w_t-u\rangle+\eta^2\lVert g_t\rVert^2$; khớp Bước 1 của chứng minh Mệnh đề 05.13.
- **Mệnh đề 05.13 (4-01, 4-02):** đủ $W$ khác rỗng, đóng, lồi; $u\in W$; $\eta>0$; tất định; dấu bằng khi $W=\mathbb R^p$; Bổ đề 05.8(b) ở bước 1.
- **Định lý 05.14 (4-03, 4-04):** (C), (G1), (G2) với $G$, Thuật toán 05.11, $w_1\in W$ tất định, $\eta>0$ hằng, $T\ge1$, $u\in W$ tất định; kì vọng theo $\xi_1,\ldots,\xi_{T-1}$; đầu ra trung bình các điểm lặp; (G1) vào bước 3, (G2) vào bước 4, (C) vào bước 5, như ghi chú.
- **Hệ quả 05.15 (4-07, 4-08):** $G>0$, $R>0$, $\eta=R/(G\sqrt T)$, (a)–(c), $F_R$, $T$ cố định trước; AM–GM đúng ($a=R^2/(2T)$, $b=G^2/2$).
- **Hệ quả 05.16 (4-09):** (C), $\lVert v(w)\rVert\le G$, $G>0$, $R>0$, $u\in W$, $\lVert w_1-u\rVert\le R$, Thuật toán 05.9; tất định.
- **Hệ quả 05.19 (6-02, 6-03):** đủ năm thành phần (tập huấn luyện cố định, $\ell(\cdot,z)\ge0$ lồi, dưới gradient đo được $\lVert v(w,z_i)\rVert\le G$, $G>0$; $W$ bị chặn, $w_1\in W$, $R\ge\sup$; $\varphi(w,i)=v(w,z_i)$, rút đều có hoàn lại; Thuật toán 05.11 với $\eta=R/(G\sqrt T)$); $\delta'$ theo $\xi$ khác $\delta$ theo $S$; đại lượng là sai số tối ưu, không phải rủi ro.
- **Bổ đề 05.8 (3-02), Bổ đề 05.12 (3-06), Mệnh đề 05.20 (6-04):** giả thiết và bảo đảm khớp; 05.20 ghi "đọc thêm" trong ghi chú diễn giả; (c) của 05.12 có $\mathbb E\lVert g_t\rVert^2\le G^2$, phần khả tích nằm ở ghi chú diễn giả.
- **Kí hiệu:** $\varphi$, $\psi$, $w^*$, $\bar w_T$, $\mathcal F_t$, $\operatorname{opt}_s$/$\operatorname{opt}_S$, $\epsilon_{\mathrm{opt}}$, $\delta'$, $G_F$, $G_b$, $\sigma^2$, $\Delta_t$ đúng như ghi chú; nhãn (C), (G1), (G2), (T1), (O2) đúng.

## 3. Số đã tính lại (khớp ghi chú, bài tập, mặt trang, ghi chú diễn giả, SVG)

- **Dưới gradient (F1, 2-03):** khung trái thang ngang $110$ px, dọc $105$ px; bốn đường $v=\pm1,\pm0{,}5$ đúng đầu mút; khung phải: $f(-1{,}6)=2{,}4336$ ↔ $y=38{,}4$; đoạn tô đậm từ $x=469{,}7$, tức $\lvert w\rvert\le\sqrt2$, đúng tập $f\le1$.
- **Hàm lỗi bản lề (2-05, 2-07):** $\langle w_0,x\rangle=1$; $u=(0{,}4;0{,}05)$, $\ell(u)=0{,}5<0{,}6$; Bài tập 05.1(d): $(0{,}5;-0{,}5)$, kiểm tra tại $(1,-1)$: $2=1+1$.
- **Phép chiếu (F2, 3-01, 3-02):** $\lVert\theta\rVert=1{,}4142$; $\pi=(0{,}7071;-0{,}7071)$; $\lVert\pi-u\rVert=0{,}7654$; $\langle\theta-\pi,u-\pi\rangle=-0{,}1213$; tọa độ SVG khớp (tâm $(254{,}1;258{,}9)$, bán kính $172{,}4$); góc tại $\pi$ là $112{,}5^\circ$, cung vẽ đúng phía.
- **Ba bước SGD (3-05, F3):** $w_2=(1,0)$, $L_S=0{,}4533$; $\lVert(1,-1)\rVert=1{,}4142$, $w_3=(0{,}7071;-0{,}7071)$, $L_S=0{,}06386$; $i_3=1,2,3$: chuẩn $1{,}2247$; $1{,}2247$; $0{,}9899$, $L_S(w_4)=0{,}07103$; $0{,}10214$; $0{,}06938$, trung bình $0{,}08085$; GD: gradient $(-0{,}2518;0{,}1198)$, chuẩn $1{,}1324$, $(0{,}7356;-0{,}6774)$, $L_S=0{,}06136$; $M$, $c$, nghiệm không ràng buộc $(1{,}06;-0{,}92)$, chuẩn $1{,}4036$, $L_S=0{,}00667$; $\kappa=0{,}13496$, $w^*=(0{,}74733;-0{,}66445)$, $L_S(w^*)=0{,}061117$. SVG: thang $270$ px (khung chính), $950$ px (khung phóng to, tâm $(0{,}74;-0{,}65)$); mọi điểm $w_1$–$w_4$, GD, $w^*$, nghiệm không ràng buộc đúng tọa độ; elip mức $0{,}0639$ có $y\in[-1{,}2616;-0{,}5784]$, $x\in[0{,}6849;1{,}4351]$, nằm trong khung $[-0{,}1;1{,}5]\times[-1{,}3;0{,}2]$ (polyline $y_{\max}=414{,}6$ ↔ $-1{,}2615$); ba điểm SGD ngoài elip, GD và $w^*$ trong elip, đúng với giá trị $L_S$.
- **Bất đẳng thức một bước (4-02):** $\lVert w_2-w^*\rVert^2=0{,}5053$; $\lVert w_3-w^*\rVert=0{,}05863$ ($0{,}00344$); $\lVert(1,-1)-w^*\rVert=0{,}42004$ ($0{,}17643$); vế trái $1{,}32891$; vế phải có chiếu $1{,}50190$, không chiếu $1{,}32891$; bước ba $i_3=1$: khoảng cách $0{,}0586\to0{,}1112$.
- **Bảng chín ô (3-08, 5-04):** ba $w_2$, ba $\psi(w_2)$; các ô $0$; $1{,}3289$; $0{,}8198$ / $1{,}4947$; $0$; $1{,}1469$ / $1{,}4947$; $1{,}3289$; $0$; hàng $0{,}7162$; $0{,}8805$; $0{,}9412$; trung bình $0{,}84599$; $\mathbb EL_S(w_2)=0{,}5556$; $0{,}5556-0{,}06112=0{,}4944$.
- **Độ dài bước (4-06, 4-08, 4-10, F4):** $16/\epsilon^2$: $400$; $1600$; $6400$; $\eta^*=0{,}00625$, $0{,}16112$; $(\gamma+1/\gamma)/2=1{,}25$; $5{,}05$; $0{,}125$; $0{,}505$; $\eta=0{,}5$: $4{,}000625$; Bài tập 05.4(c): $6400$, $0{,}0015625$, $0{,}0625$; $400$, $0{,}025$, $0{,}25$; (b): $2500$, ngưỡng $0{,}0125$. SVG: vạch lôgarit $0{,}001$; $0{,}003125$; $0{,}00625$; $0{,}0125$; $0{,}0625$ ở đúng vị trí ($278{,}1$ px/thập phân); bốn điểm có nhãn đúng độ cao; $Q(0{,}0005)=0{,}629$, $Q(0{,}1)=0{,}803125$.
- **Hồi quy logistic (4-09, 6-03):** $R=5$, $G=1$, $T=10^4$, $\eta=0{,}05$, $10^{10}$; xác suất cao: $4\,000\,000$ bước, bằng bốn bước GD.
- **Hàm không lồi (5-01, F5):** hai nhánh gặp tại $-0{,}125$, giá trị $1{,}265625$; $G=2{,}25$; $R=2{,}5$; $\eta=0{,}027778$; $RG/\sqrt T=0{,}140625$; $\bar w_{1600}+1=-0{,}005625$, tức $\bar w_{1600}=-1{,}005625$, $f(\bar w_{1600})=0{,}50003$; ngưỡng $-1{,}1213$, từ $t=26$ ($0{,}5\cdot0{,}9444^{t-1}<0{,}1213\iff t-1\ge25$). SVG: thang $165$ px ngang, $212{,}5$ px dọc; $w_1=(-1{,}5;0{,}75)$, hai đáy, điểm gãy đúng tọa độ.
- **Mô-men không bị chặn (5-02):** $\mathbb E\ln\lvert a_t\rvert=0{,}0870$; $\mathbb Ea_t^2=1{,}69$; $164w^2$; $\sqrt{164}=12{,}806$.
- **Điểm lặp cuối, oracle chệch (5-03):** $0{,}1;-0{,}1;\ldots$; $0{,}025/T+0{,}1$; $\psi=2w-0{,}2$; $\tilde F=(w-0{,}1)^2+0{,}09$; $0{,}41-0{,}25=0{,}16$; với $T$ lẻ $\bar w_T=0{,}1/T$ (ghi chú diễn giả, đúng).
- **Lô nhỏ (6-05, 6-06):** $T(b)=1600$; $475$; $194$; $124$; $106$; số quan sát $1600$; $1900$; $3104$; $7936$; $27\,136$; GD $10^6$; Bài tập 05.5(b): $b=30$, $3300$; $b=150$, $16\,500$; (a): $400$; $200$; $119$; $105$; (c): $4{,}75$; $3{,}1667$.
- **Nhiều lần chạy (7-04, 7-05):** $\log_220=4{,}32$, $k=5$, $0{,}03125$; $6400$; $32\,000$; $m<121\,600$.
- **Câu hỏi cuối buổi, Phụ lục D (7-01):** $L_D(w)=w^2+1$; $G=4$, $R=1$, $\eta=0{,}00625$; $0{,}9875^{1600}=1{,}82\cdot10^{-9}$; $\bar w_{1600}=0{,}95$; $L_S=0{,}0025$; $L_D=1{,}9025$; $\min_WL_D=1$; sai số ước lượng $0{,}9025$.
- **Nhận xét 05.17 (4-07, 4-08 ghi chú diễn giả):** $\sum\eta_t=19{,}6380$, $\sum\eta_t^2=0{,}49721$, vế phải $0{,}22801$.

## 4. Bảng thống nhất trang → khối ghi chú

"Khớp" nghĩa là kí hiệu, giả thiết, số hiệu, dữ liệu và kết quả trùng ghi chú hoặc `exercises.md`.

| Trang | Khối ghi chú / bài tập | Thống nhất |
|---|---|---|
| 1-01 | đoạn mở đầu, §7, §11 | khớp; câu sau của luận điểm thiếu điều kiện (nhẹ) |
| 1-02 | Kiến thức tiên quyết; Định nghĩa 04.1, 04.2; (O2); (T1); Bổ đề 02.2; câu ôn nhanh | khớp |
| 1-03 | Mục tiêu học tập 1–5 | khớp (rút gọn) |
| 1-04 | §4–§13 theo mạch; §14 | khớp |
| 1-05 | đoạn mở đầu (câu hỏi trung tâm) | khớp |
| 1-06 | Câu hỏi mở đầu; Ví dụ 05.6 (bốn số); khối ứng dụng §3 | khớp |
| 2-00 | §4 đoạn mở | khớp |
| 2-01 | §1 (tám thành phần, độ chênh tối ưu, bảng nguồn ngẫu nhiên); Ví dụ 05.1 | khớp |
| 2-02 | Định nghĩa 05.1; bất đẳng thức lồi hữu hạn; ví dụ không lồi | khớp |
| 2-03 | Định nghĩa 05.2; ba đoạn sau; ví dụ $\lvert w\rvert$, $(w^2-1)^2$ | lệch: bỏ "lồi" ở câu $\partial F=\{\nabla F\}$ (trung bình) |
| 2-04 | Mệnh đề 05.3; Ví dụ 05.3 | khớp |
| 2-05 | Ví dụ 05.2 | khớp |
| 2-06 | Định nghĩa 05.4; Mệnh đề 05.5; ví dụ Lipschitz; Định nghĩa 05.6 (ghi chú diễn giả) | khớp |
| 2-07 | Bài tập 05.1(d), (c) | khớp |
| 3-00 | §5, §6 đoạn mở | khớp |
| 3-01 | Định nghĩa 05.7; Ví dụ 05.4 | khớp; nhãn SVG "proj" (nhẹ) |
| 3-02 | Bổ đề 05.8 (phác thảo), Phụ lục A | khớp |
| 3-03 | Định nghĩa 05.10, (G1), (G2), đoạn sau; Ví dụ 05.5 | khớp |
| 3-04 | Thuật toán 05.9, 05.11; đoạn sau | khớp |
| 3-05 | Ví dụ 05.5, 05.6; Phụ lục D | khớp |
| 3-06 | Bổ đề 05.12 | khớp |
| 3-07 | chứng minh Bổ đề 05.12 ($\Xi$ hữu hạn), Phụ lục B | khớp |
| 3-08 | Bài tập 05.3(b) | khớp ("vế phải của (a)" thay bằng Bổ đề 05.12(c) với $t=2$, cùng nội dung) |
| 4-00 | §7 | khớp |
| 4-01 | đoạn mở §7; Mệnh đề 05.13 | khớp; ghi chú diễn giả dùng sai số của bước hai (trung bình) |
| 4-02 | chứng minh Mệnh đề 05.13; Ví dụ 05.7; Bài tập 05.2(b), (c) | khớp |
| 4-03 | Định lý 05.14 và đoạn sau | khớp; "Trực quan." thiếu bình phương và thừa số 2 (nhẹ) |
| 4-04 | chứng minh Định lý 05.14, Bước 1–5 | khớp |
| 4-05 | chứng minh Định lý 05.14, Bước 2, 5; Phụ lục C | khớp |
| 4-06 | Ví dụ 05.8, Bước 3, 4; đoạn sau Hệ quả 05.15 | khớp |
| 4-07 | Hệ quả 05.15; Nhận xét 05.17 (ghi chú diễn giả) | khớp |
| 4-08 | chứng minh Hệ quả 05.15; Ví dụ 05.8, Bước 1, 2; Bài tập 05.4(a) | khớp; $0{,}2281$ viết như đẳng thức (nhẹ) |
| 4-09 | Hệ quả 05.16 và chứng minh; Ví dụ 05.9 | khớp |
| 4-10 | Bài tập 05.4(c), (b) | khớp |
| 5-00 | §8 đoạn mở | khớp |
| 5-01 | Ví dụ 05.10 | khớp |
| 5-02 | Ví dụ 05.11 | khớp |
| 5-03 | Ví dụ 05.12, 05.13; đoạn cuối §8 | khớp (theo cách đọc §11 đã chốt) |
| 5-04 | Bài tập 05.3(c) | khớp |
| 6-00 | §9 đoạn mở, §10 đoạn mở | khớp |
| 6-01 | Định nghĩa 05.18 và hai đoạn sau | khớp |
| 6-02 | Hệ quả 05.19; câu sau $\square$; đoạn cuối §9 | khớp |
| 6-03 | chứng minh Hệ quả 05.19; Ví dụ 05.14 | khớp |
| 6-04 | Mệnh đề 05.20 và chứng minh; Ví dụ 05.16 | khớp |
| 6-05 | Ví dụ 05.15; đoạn cuối §10 | khớp |
| 6-06 | Bài tập 05.5(b), (a), (c) | khớp |
| 7-00 | §11–§14 | khớp |
| 7-01 | §13 câu hỏi cuối buổi và lời giải; đoạn sau | khớp |
| 7-02 | Mệnh đề 05.13, Định lý 05.14, Hệ quả 05.15, 05.16, 05.19 | khớp; hàng 05.16 thiếu $\eta$ (nhẹ) |
| 7-03 | §11 | lệch: dòng 3 bỏ điều kiện của Hệ quả 05.19(b) (trung bình) |
| 7-04 | Bài tập 05.5(d) và hai gợi ý | khớp |
| 7-05 | lời giải Bài tập 05.5(d) | khớp; thừa số chi phí trong ghi chú diễn giả (nhẹ) |
| 7-06 | Ví dụ 05.6; Định lý 05.14 và chứng minh; đoạn sau Định nghĩa 05.10 | khớp |
| 7-07 | §12; `exercises.md` (12 bài) | khớp số hiệu |
| 7-08 | §14 và quan hệ với UML; §13 đoạn cuối; tiêu đề Bài 06 | khớp |

## 5. Kết luận

**đạt khi sửa** — 0 chặn bàn giao, 0 nghiêm trọng, 3 trung bình (2-03, ghi chú diễn giả 4-01, 7-03), 9 nhẹ.

## Đề xuất sửa ghi chú

- **nhẹ | Nhận xét 05.17 và §11 so với Phụ lục C.** Nhận xét 05.17 ghi "không quá $0{,}2281$", §11 ghi "cận $0{,}2281$", Phụ lục C Bước 4 ghi "$\approx0{,}2280$"; giá trị đúng $0{,}22801$. Đề xuất thống nhất: §11 viết "cận không quá $0{,}2281$" hoặc dùng $0{,}2280$ ở cả ba chỗ.
- Hai đề xuất đã có trong `review-log.md` (Bài tập 05.5(a) "giá trị giả định"; câu kết dòng 1030 của Ví dụ 05.12) vẫn còn nguyên; không có phát hiện mới về toán trong ghi chú.
