# Bài 04 — Rà lại toán học sau biên tập vòng 1

Đầu vào: `lec04-round1-frozen.md` (số dòng dẫn theo tệp này, đã đọc toàn bộ 1229 dòng), `lec04-round1.diff`, `reviews/0-quyet-dinh.md`, `bien-tap-vong-1.md`, `reviews/2-toan-hoc.md`. Phạm vi là toán học; không có phát hiện về câu chữ, nên không dùng chế độ Detect của `no-ai-slop`.

**Số phát hiện mới theo mức độ:** chặn bàn giao 0 · nghiêm trọng 0 · trung bình 1 · nhẹ 4.

## 1. Trạng thái các điểm cần sửa

| Điểm | Trạng thái | Dòng | Ghi chú |
|---|---|---|---|
| R2-1 (Ví dụ 04.8, xác suất thất bại) | ✓ | 636–640, 987 | Biến cố hỏng $L_S(h_k)\in\{0,1\}$ với xác suất $2^{-9}$; in $0{,}858$ và $0{,}99994$; giữ $0{,}6236$ cho riêng biến cố $L_S=0$; §9 in $0{,}86$. |
| R2-2 (tính đo được của $A_{\mathrm{SRM}}$) | ✓ | 840, 899, 1080, 1097 | |
| R2-3 (Ví dụ 04.3) | ✓ | 256–278 | Còn một chỗ làm tròn rất nhỏ, xem phát hiện mới 3. |
| R2-4 (cận bị làm tròn xuống) | một phần | 766, 768, 770, 1028 đúng; 792, 796, 986 chưa sửa | Xem phát hiện mới 3. |
| R2-5 ($0{,}0131$) | ✓ | 772 | |
| R2-6 (Định nghĩa 04.1 và (T3)) | ✓ | 151, 168 | |
| R2-7 (giả thiết thuật toán của Định lý 04.11) | ✓ theo quyết định D | 688, 696 | |
| R2-8 (Thuật toán 04.12: điều kiện dừng và $\tau'$) | ✓ | 719, 730, 739, 1216–1222 | |
| R2-9 (kí hiệu $V$ ở Phụ lục A) | ✓ | 1059 ($v^\star$), 1118 ($\varphi$) | |
| R2-10 (Định lý 03.17(a) cho đầu ra ngoài $\mathcal H_k$) | ✓ | 1194 | |
| R2-11 (tính đo được của $\operatorname{opt}_S$) | ✓ | 201 | |
| R2-12 ("khác biệt duy nhất") | ✓ | 827 | |
| R2-13 (giả thiết đo được của Hệ quả 04.17) | ✓ | 918, 945 | |
| N1 | ✓ | 636–640, 987 | |
| N5 ($k_{\max}$ và $K$) | ✓ | 96–97, 512, 625, 853, 1110 | Bảng kí hiệu bị vỡ, xem phát hiện mới 2. |
| M2 | ✓ | 250, 289 | |
| M4 | ✓ | 807 | |
| M5 | ✓ | 766, 1028, 978 | |
| M8 | ✓ | 840, 899, 1080 | |
| M9 | ✓ | 151, 168 | |
| M10 | ✓ | 376–392, 496 | |
| M11 | ✓ | 1194 | |
| M12 | ✓ | 753–772 | |
| M13 | ✓ | 831, 1112 | |
| M14 | ✓ | 866–872 | |
| M15 | ✓ | 1037 | |
| M19 | ✓ | 212, 535–542 | |
| M20 | ✓ | 400–401, 719, 723–730 | |
| Quy tắc làm tròn ở §D | một phần | | Đã áp dụng cho $0{,}3651$, $0{,}3751$, $0{,}4350$, $0{,}3593$, $0{,}0058$, $0{,}0130$. Chưa áp dụng cho $0{,}0468$ (dòng 792, 796, 986) và $\rho_m\le0{,}16443$ (dòng 256). |

**Các đoạn đã sửa: đã chứng minh lại, không có lỗi.**

- **Phụ lục B (chứng minh Hệ quả 04.15).** Các bước 1–4 đúng: $\delta=1/m\in(0,1)$ khi $m\ge2$; $\mathrm{pen}_k(m)\to0$ trong cả ba trường hợp; $M_k(\epsilon)$ hữu hạn; $m\ge\max\{\lceil1/\delta\rceil,M_k\}$ kéo theo $m\ge2$, $1/m\le\delta$ và $2\mathrm{pen}_k\le\epsilon$; phần (b) lấy $\inf$ trên $E_m$. Tính đo được của $A_{\mathrm{SRM}}$ được dẫn đúng chỗ. Câu sau $\square$ đúng.
- **Phụ lục C, chiều VC $d_k=k+1$.** Cận dưới qua phép thêm tọa độ $0$; cận trên qua $\mathrm{pr}_k$ (hai điểm cùng ảnh thì cùng nhãn); điều kiện (M) qua các tham số hữu tỉ.
- **Phụ lục C, hệ phương trình chuẩn.** Ta có $\sum x_iY_i=Y_3-Y_1$, nên $\hat a=\bar Y$ và $\hat b=(Y_3-Y_1)/2$.
- **Phụ lục D.** Các lớp $\mathcal H_k=\{M(\tfrac18,\tfrac18,h)\le k\}$ phủ $\mathcal H$. Phân bố có được từ lập luận không có bữa trưa miễn phí với $m=k$ có $L_D(h)=0$ với $h\in\mathcal H_k$. Từ $m=k\ge M$ suy ra xác suất thất bại không quá $\tfrac18<\tfrac17$, nên $\operatorname{VCdim}(\mathcal H_k)<2k$. Câu cuối cần sửa nhẹ (phát hiện mới 4).
- **Phụ lục E, Bước 1–2.** Đúng, kể cả với sai số so sánh $\tau'$ ở phép thử dừng: $v$ chỉ giảm, và ta có $\mathrm{pen}_{k'}\ge\mathrm{pen}_k\ge v-\tau'$. Bước 3 có một đẳng thức sai (phát hiện mới 1).
- **Ví dụ 04.6.** Lỗi 0–1: $0{,}58$ và $0{,}90$. Đẳng thức của Mệnh đề 04.6 đúng. Dự đoán đa số của cả hai thuật toán là $0$, khác $h_{\mathrm{Bayes}}=1$. Phương sai theo nghĩa phân lớp là $0{,}4$ và $0$. Độ chệch bình phương là $0{,}25$ và $0{,}81$. Kết luận "khi dự đoán đa số sai, tăng phương sai làm giảm lỗi" đúng tại điểm này: lỗi bằng $\eta-P_1(2\eta-1)$ và giảm theo $P_1=\Pr[\hat f=1]<\tfrac12$.
- **Ví dụ 04.8.** Đúng như ở bảng trên.
- **Ví dụ 04.11, Bước 3.** Quy tắc "chọn chỉ số $j$ nhỏ nhất trong các nghiệm" cho một $A_{\mathrm{SRM}}$ đo được. Tập $\{s:j^*(s)=j\}$ là giao đếm được của các bất đẳng thức giữa các hàm đo được $L_s(h_i)+\mathrm{pen}_i$, nên đo được, và $\ell(A(s),z)=\sum_j\mathbb 1[j^*(s)=j]\,\ell(h_j,z)$ đo được.
- **Định nghĩa 04.1 với phạm vi rộng hơn.** Chỉ cần (T2) và $L_D<\infty$. Đẳng thức sai số xấp xỉ cộng sai số ước lượng không cần (T3). Mệnh đề 04.3 vẫn giữ (T3).
- **Câu về rủi ro Bayes của hàm lỗi bình phương (dòng 376–392).** Với $f$ cố định, phương sai bằng $0$ và lỗi bằng $(f-f^*)^2+\sigma^2\ge\sigma^2$. Lấy tích phân theo $X$ cho $L_D(f)\ge\mathbb E\sigma^2(X)$, dấu bằng tại $f^*$; $f^*$ bình phương khả tích vì $\mathbb E f^*(X)^2\le\mathbb EY^2$. Nhận xét 04.7 dẫn đoạn này đúng.
- **Các đoạn khác.** Mệnh đề 04.3 với giả thiết mới; Định nghĩa 04.8 với dạng chiều VC viết thành công thức; Định lý 04.11, Bước 1; Thuật toán 04.12 viết thành danh sách; câu mở §7; Hệ quả 04.17. Không có lỗi mới.

## 2. Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | Phụ lục E, Bước 3 (dòng 1226) | Câu "dòng cuối của Bước 1 bằng $\inf_{h\in\mathcal H_k}L_S(h)+\operatorname{opt}_S(\hat h_k)+\mathrm{pen}_k+\tau'$" sai. Dòng cuối của Bước 1 là $\inf L_S+\mathrm{pen}_k+\epsilon_{\mathrm{opt}}+\tau'$, và nó $\ge$ giá trị trên. Đẳng thức đúng cho dòng giữa, $L_S(\hat h_k)+\mathrm{pen}_k+\tau'$. Bản đóng băng trước viết "dòng thứ hai"; lỗi xuất hiện khi chuyển đoạn này sang phụ lục. Ngoài ra "với số hạng này thay cho $\tau$" không nói rõ số hạng nào. | Dòng 1208–1213 so với 1226. | "…vế phải của bất đẳng thức thứ nhất ở Bước 1, $L_S(\hat h_k)+\mathrm{pen}_k+\tau'$, bằng $\inf_{h\in\mathcal H_k}L_S(h)+\operatorname{opt}_S(\hat h_k)+\mathrm{pen}_k+\tau'$… chuỗi bất đẳng thức của Định lý 04.11, với $\operatorname{opt}_S(\hat h_k)+\tau'$ thay cho $\tau$, cho cận tinh hơn." |
| nhẹ | §2, bảng kí hiệu (dòng 99–101) | Dòng trống ở dòng 100 cắt bảng, nên hàng $\epsilon$ không còn thuộc bảng mà hiện thành một đoạn văn có dấu `|`. Hàng $\ln$ của bản trước cũng đã bị xóa; chỉ cần kiểm lại xem việc xóa này có chủ ý không. | Dòng 99–101. | Xóa dòng 100. |
| nhẹ | Ví dụ 04.10 (dòng 792, 796), §9 (dòng 986); Ví dụ 04.3 (dòng 256) | Quy tắc làm tròn ở §D chưa áp dụng hết. Cận báo "$L_D\le0{,}0468$", trong khi giá trị đúng là $0{,}046808$, nên làm tròn lên phải là $0{,}0469$. "$\rho_m\le0{,}16443$" thấp hơn dạng trực tiếp $0{,}1644303$ ở chữ số thứ bảy. | Python. | Ghi $0{,}0469$ ở ba chỗ. Ở dòng 256, viết "$\rho_m\le0{,}16444$", hoặc "dạng trực tiếp $\approx0{,}16443$". |
| nhẹ | Phụ lục D, câu sau $\square$ (dòng 1198) | Câu "mỗi lớp học được không đều là hợp đếm được của các lớp học được PAC" cần (M): theo Định lý 03.17(b), chiều VC hữu hạn chỉ cho học được PAC dưới (M). Phần (a) chỉ cho các lớp có chiều VC hữu hạn. | Lec-03, Định lý 03.17(b) "dưới (M)". | "…là hợp đếm được của các lớp có chiều VC hữu hạn (học được PAC khi thêm (M), Định lý 03.17(b))…" |
| nhẹ | Ví dụ 04.6, Bước 2–3 (dòng 469, 480) | Chữ "phương sai" chỉ hai đại lượng khác nhau cho cùng thuật toán $A$: $0{,}24$ theo Định nghĩa 04.5 và $0{,}4$ theo nghĩa phân lớp. Phép tính không sai, nhưng hai số cùng tên dễ gây nhầm. | Dòng 469 so với 480. | Ở Bước 3, viết "*phương sai theo nghĩa phân lớp* là $0{,}4$ với $A$ (khác phương sai $0{,}24$ của Định nghĩa 04.5)". |

## 3. Số mới hoặc đã đổi

| vị trí | số in | tính lại | |
|---|---|---|---|
| Dòng 13 | $0{,}329\to0{,}560$ | $0{,}32886$; $0{,}55984$ | ✓ |
| Ví dụ 04.3 | $0{,}16443$; $0{,}27992$ | $0{,}1644303$; $0{,}2799193$ | ~ (xem phát hiện mới 3) |
| Ví dụ 04.3 | $\approx a_2+0{,}3389$; $\approx a_{10}+0{,}5698$ | $0{,}338861$; $0{,}569839$ | ✓ |
| Ví dụ 04.3 B4 | $2(0{,}27992-0{,}16443)\approx0{,}2310$ | $0{,}23098$ | ✓ |
| Ví dụ 04.4 B5–6 | $0{,}1736+0{,}3333=0{,}5069$; $0{,}6319$; $0{,}7188$; $0{,}0333$; $0{,}0458$; $0{,}2069$; $0{,}2194$; $0{,}0719$ | như in | ✓ |
| Ví dụ 04.5 | $\sigma^2(m-1)m/m^2=0{,}75$ | $0{,}75$ | ✓ |
| Ví dụ 04.6 | $0{,}58$; $0{,}90$; $0{,}24$; $0{,}4$ / $0$; $0{,}25$ / $0{,}81$ | như in | ✓ |
| Nhận xét 04.7 | $1-0+1=2$; $2-1=1$ | như in | ✓ |
| Ví dụ 04.7 B2 | $2{,}1972+0{,}4977\approx2{,}695$; $4{,}6052+0{,}4977\approx5{,}103$ | $2{,}19722$; $4{,}60517$; $2{,}69492$; $5{,}10287$ | ✓ |
| Ví dụ 04.8 | $2^{-9}$; $0{,}858$; $0{,}99994$; $0{,}6236$; $\sqrt{\ln40\,000/20}\approx0{,}7279$ | $0{,}858440$; $0{,}999943$; $0{,}623576$; $0{,}727895$ | ✓ |
| Ví dụ 04.9, bảng mười hàng | $\mathrm{pen}$ $0{,}2241$; $0{,}2386$; $0{,}2520$; $0{,}2644$; $0{,}2761$; tổng $0{,}3901$; $0{,}4016$; $0{,}4120$; $0{,}4224$; $0{,}4321$ | $0{,}224087$; $0{,}238606$; $0{,}251974$; $0{,}264416$; $0{,}276092$; tổng $0{,}39009$; $0{,}40161$; $0{,}41197$; $0{,}42242$; $0{,}43209$ | ✓ |
| Ví dụ 04.9 B2 | $0{,}3651$ (chưa làm tròn $0{,}36504$) | $0{,}365044$ | ✓ |
| Ví dụ 04.9 B3 | $0{,}155+0{,}27992=0{,}43492\to0{,}4350$ | $0{,}434919$ | ✓ |
| Ví dụ 04.9 B4 | $0{,}35928\to0{,}3593$; hiệu $0{,}0058$ | $0{,}359284$; $0{,}005759$ | ✓ |
| Ví dụ 04.9 B5 | $0{,}0130$ | $0{,}013038$ | ✓ |
| Ví dụ 04.9 KL | $2\mathrm{pen}$: $0{,}338$; $0{,}574$ | $0{,}337902$; $0{,}574237$ | ✓ |
| Ví dụ 04.10 | $\le0{,}0468$ | $0{,}046808$ | ~ (làm tròn lên thành $0{,}0469$) |
| Dòng 872 | $1/m\approx4{,}7\cdot10^{-6}$ | $4{,}688\cdot10^{-6}$ | ✓ |
| Phụ lục C, cột $a$, $k=5..9$ | $54{,}67$; $62{,}70$; $70{,}59$; $78{,}36$; $86{,}01$ | $54{,}6704$; $62{,}7030$; $70{,}5924$; $78{,}3564$; $86{,}0090$ | ✓ |
| Phụ lục C, cột $b$, $k=5..9$ | $8{,}099$; $8{,}463$; $8{,}772$; $9{,}039$; $9{,}274$ | $8{,}09860$; $8{,}46325$; $8{,}77155$; $9{,}03861$; $9{,}27418$ | ✓ |
| Phụ lục C, cột "không chia", $k=5..9$ | $0{,}2174$; $0{,}2317$; $0{,}2449$; $0{,}2573$; $0{,}2689$ | $0{,}217352$; $0{,}231664$; $0{,}244907$; $0{,}257276$; $0{,}268910$ | ✓ |
| Phụ lục C, tỉ số, $k=5..9$ | $1{,}031$; $1{,}030$; $1{,}029$; $1{,}028$; $1{,}027$ | $1{,}03099$; $1{,}02997$; $1{,}02886$; $1{,}02776$; $1{,}02670$ | ✓ |
| Phụ lục C, tỉ số nhỏ nhất và lớn nhất | $1{,}010$ ($k=1$); $1{,}032$ ($k=4$) | $1{,}00998$; $1{,}03165$ | ✓ |
| Phụ lục B | $172\,279$; $181\,575$; $213\,317$; $16{,}35$ | không đổi so với bản trước, đã kiểm ở `2-toan-hoc.md` | ✓ |
| Câu hỏi cuối buổi (b) | $0{,}3751$ (chưa làm tròn $0{,}37504$) | $0{,}375044$ | ✓ |
| §9 | $0{,}3651$ / $0{,}4350$; $0{,}86$; $3{,}2\%$; $17{,}5\%$; $0{,}0468$ / $0{,}8$; $0{,}75$ / $1{,}25$ | như trên | ✓ (riêng $0{,}0468$ là ~) |

Các số không đổi so với bản đóng băng trước đã được kiểm ở `2-toan-hoc.md` và không bị diff động đến.

## 4. Kết luận

**Giao được** sau khi sửa phát hiện mức trung bình ở Phụ lục E, Bước 3. Đó là đẳng thức "dòng cuối" sai; chỉ cần sửa câu, không phải sửa lập luận. Bốn phát hiện nhẹ (bảng kí hiệu bị vỡ, $0{,}0468\to0{,}0469$, câu cuối Phụ lục D, chữ "phương sai" hai nghĩa ở Ví dụ 04.6) có thể sửa trong cùng lượt. Mọi điểm của vòng trước đều đã sửa, trừ hai chỗ làm tròn còn sót.
