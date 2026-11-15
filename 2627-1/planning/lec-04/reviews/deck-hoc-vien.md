# Duyệt deck Bài 04 — vai học viên cao học

Bản duyệt: `2627-1/lecture-04-phan-tich-sai-so.html` (bản đóng băng, 55 trang), đọc như người nghe giảng lần đầu đã đọc trước ghi chú. Chỉ đọc; không sửa deck, SVG, storyboard, ghi chú.

## Kiểm tra máy đã chạy (2026-11-15)

- `deck_lint.py`: 1 phát hiện, 7-03 `SYLL60` 76 > 60.
- `footer_check.py` (1600×900): 0 trang chạm chân trang.
- `deck_check.py --shots`: console 0, pageerrors 0, failed 0, `.katex-error` 0; OVERFLOW ở 4-05, 4-11, 5-03, 6-01, 6-02, 6-03, 6-04, 6-05, 7-02, 7-04 đều là đuôi SVG của `\sqrt` (báo động giả đã biết). Ở 390 px `docScrollW` = 390 trên mọi trang.
- Ảnh 1600×900 và 390×844 (kể cả `-end`) của cả 55 trang đã xem, trong thư mục nháp `rv-hoc-vien/shots/`; công thức và bảng rộng cuộn ngang tại chỗ, trang không cuộn ngang.

## Đếm mật độ

Âm tiết mặt trang = token cách nhau bởi khoảng trắng, không tính tiêu đề, KaTeX, bảng, nhãn hình, ghi chú; số viết trong câu có tính. Trần 60 (80 cho Mục tiêu, Nội dung, Bảng tổng kết); bìa và trang tiêu đề mạch tính riêng.

| Trang | Âm tiết | Dòng | CT hiển thị | Trang | Âm tiết | Dòng | CT hiển thị |
|---|---|---|---|---|---|---|---|
| 1-02 | 58 | 5 | 0 | 4-01 | 56 | 4 | 2 |
| 1-03 (trần 80) | 80 | 5 | 0 | 4-02 | 59 | 4 | 1 |
| 1-04 (trần 80) | 39 | 7 mục | 0 | 4-03 | 60 | 5 | 1 |
| 1-05 | 26 | 1 hộp | 0 | 4-04 | 58 | 5 | 0 |
| 1-06 | 58 | 4 | 0 | 4-05 | 52 | 6 | 0 |
| 2-01 | 46 | 3 | 0 | 4-06 | 50 | 4 | 1 |
| 2-02 | 54 | 6 | 0 | 4-07 | 30 (+bảng) | 2 | 0 |
| 2-03 | 47 | 4 | 0 | 4-08 | 57 | 4 | 1 |
| 2-04 | 50 | 4 | 1 | 4-09 | 57 | 5 | 1 |
| 2-05 | 60 | 5 | 1 | 4-10 | 26 | 4 | 0 |
| 2-06 | 59 | 5 | 1 | 4-11 | 57 | 6 | 0 |
| 2-07 | 56 | 5 | 1 | 4-12 | 31 (+bảng) | 4 | 0 |
| 2-08 | 47 (+bảng) | 4 | 0 | 5-01 | 55 | 4 | 1 |
| 3-01 | 57 | 5 | 0 | 5-02 | 60 | 5 | 0 |
| 3-02 | 59 | 4 | 1 | 5-03 | 39 | 6 | 0 |
| 3-03 | 58 | 5 | 0 | 5-04 | 60 | 6 | 0 |
| 3-04 | 24 (+bảng) | 3 | 0 | 6-01 | 59 | 5 | 0 |
| 3-05 | 60 | 5 | 1 | 6-02 | 60 | 6 | 0 |
| 3-06 | 56 | 5 | 0 | 6-03 | 22 | 4 | 0 |
| 3-07 | 59 | 5 | 0 | 6-04 | 58 | 5 | 0 |
| 7-01 (trần 80) | 70 chữ trong bảng | bảng | 0 | 6-05 | 60 | 6 | 0 |
| 7-02 | 59 | 5 | 0 | 7-05 | 59 | 5 | 0 |
| 7-03 | **76** | 5 | 0 | 7-06 | 6 (+bảng) | 1 | 0 |
| 7-04 | 32 | 4 | 1 | 7-07 | 56 | 5 | 0 |

Trang tiêu đề mạch: dòng dẫn 15–23 âm tiết (≤ 25). Bìa 59 (miễn trừ). Không trang nào vượt 20 âm tiết/dòng ngoài hộp 1-05 (26, trang tổng quan) và bìa; không trang nào quá 6 dòng hay 3 công thức hiển thị.

**Vượt trần:** chỉ 7-03 (76 > 60, dưới 1,5 lần trần), có lý do ghi trong `storyboard.md` (mục "Ngoại lệ mật độ"). 30 trang nội dung ở mức 55–60, sát trần và xa mục tiêu 40; không vi phạm nhưng làm tải đọc cao (xem phát hiện về 5-02).

## Bảng phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | 2-03 | Ở 390×844 hình `phan-tich-sai-so.svg` không đọc được: viewBox rộng 1000, chữ 19–21 đơn vị, hình hiển thị khoảng 345 px nên chữ còn khoảng 7 px; thẻ meta `user-scalable=no` chặn phóng to. Các số $0{,}22$ (h3), $0{,}32$ (h2), $0{,}04$, $0{,}10$ của Ví dụ 04.2 chỉ nằm trong hình, không có trên mặt trang, và 2-04 dùng ngay ("$0{,}22-0{,}32=-0{,}10$"). Ở 1600×900 hình đọc được. | Ảnh `narrow-009-L04-2-03-end.png`; mặt trang chỉ có "$L^*=L^{\mathrm{Bayes}}_{D_\eta}=0{,}18$:"; ghi chú Ví dụ 04.2 Bước 1–2. | Ở chế độ màn hẹp cho hình chiếm đủ bề rộng và đặt trong vùng cuộn ngang với bề rộng tối thiểu khoảng 600 px (như bảng), hoặc vẽ lại hình dọc (hai hàng xếp chồng, nhãn ngắn) cho màn hẹp; hoặc thêm một dòng mặt trang "$L_{D_\eta}(h_3)=0{,}22$, $L_{D_\eta}(h_2)=0{,}32$: sai số xấp xỉ $0{,}04$, sai số ước lượng của $h_2$ là $0{,}10$". |
| trung bình | 4-10, 6-03 | Hai đồ thị ở 390 px: nhãn số (0,4423; 0,2871; 0,155; 1199; 4794…) còn khoảng 6–7 px; ở 4-10 hình chỉ rộng khoảng 240 px dù cột đã xếp một. Các số chính có lặp ở mặt trang nên không mất nội dung, nhưng hình không đọc được. | Ảnh `narrow-033-L04-4-10.png`, `narrow-044-L04-6-03.png`; `srm-danh-doi.svg` viewBox 720, chữ 17–19; `can-xac-thuc.svg` viewBox 640, chữ 17–19. | Cùng cách sửa với 2-03 (hình đủ bề rộng, cuộn ngang với bề rộng tối thiểu); kiểm lại ảnh `-end`. |
| trung bình | 4-11, 7-05 (và 4-08, 4-10) | Thuật ngữ "cận trên tin cậy" xuất hiện trên mặt trang 4-11 ("cận trên tin cậy báo $L_D\le0{,}0469$") và 7-05 (câu 1) nhưng chưa được nêu hay nhắc lại trên mặt trang nào trước đó; 4-08 phát biểu (a) mà không gọi tên, 4-10 ghi "Định lý 04.11(a), xác suất $\ge0{,}95$: $L_D(\hat h_3)\le0{,}3651$" cũng không gọi tên. Tên này chỉ có trong ghi chú diễn giả 4-08, 4-10. | Ghi chú §6 Ví dụ 04.9 Bước 2: "$0{,}3651$ là một cận trên tin cậy ở mức $95\%$ … (Nhận xét 01.19)". | 4-08: "(a) cận trên tin cậy $L_D(\hat h)\le L_S(\hat h)+\mathrm{pen}_{\hat k}$"; hoặc 4-10: "cận trên tin cậy (Định lý 04.11(a)), mức $95\%$: $L_D(\hat h_3)\le0{,}3651$". |
| trung bình | 4-12, 6-05, 7-05 (đối chiếu 4-07, 4-11) | Mặt trang dẫn "mười lớp của Ví dụ 04.9", "Phân bố của Ví dụ 04.10", "Ví dụ 04.9 với $\tilde h\in\mathcal H_3$", nhưng số hiệu 04.9 và 04.10 không xuất hiện trên trang ví dụ tương ứng (4-07 "Ví dụ: chọn số chỉ số đo bằng SRM", 4-11 "Ví dụ: họ lớp chọn sau khi xem tập huấn luyện"). Học viên không biết ví dụ nào được dẫn; ngược lại 2-02 có ghi "Ví dụ 04.1." trên mặt trang. | Quét mặt trang: số "Ví dụ 04.x" chỉ có ở 2-02, 3-04 (04.1), 4-12, 7-05 (04.9), 6-05 (04.10). | Đặt "**Ví dụ 04.9.**" ở đầu dòng dữ kiện của 4-07 và "**Ví dụ 04.10.**" ở đầu 4-11 (giữ tiêu đề), hoặc thay dẫn chiếu bằng tên: "mười lớp của ví dụ chọn số chỉ số đo bằng SRM". |
| trung bình | 5-01 | Dòng "**Nhắc lại:** học PAC bất khả diễn (agnostic PAC learning): một $M(\epsilon,\delta)$ cho mọi $D$" không cho thấy đối tượng so sánh $\min_{h'}L_D(h')$, trong khi điểm chính của trang là hai khác biệt (đối tượng so sánh $L_D(h)$ và $M$ phụ thuộc $h$). Hai khác biệt chỉ có trong ghi chú diễn giả; trên mặt trang học viên không đặt được hai định nghĩa cạnh nhau. | Ghi chú diễn giả 5-01: "Hai khác biệt: $M$ được phép phụ thuộc giả thuyết so sánh $h$, và đối tượng so sánh là $L_D(h)$". | Viết dòng nhắc lại bằng công thức: "$\Pr[L_D(A(S))\le\inf_{h'\in\mathcal H}L_D(h')+\epsilon]\ge1-\delta$ khi $m\ge M(\epsilon,\delta)$, mọi $D$ (Định nghĩa 01.25)"; bù chữ bằng cách rút câu mở đầu trang. |
| trung bình | 7-02 | Trang trả lời vấn đề trung tâm có hai dòng khó đọc độc lập: "Bậc tốt nhất phụ thuộc $\sigma^2$, $f^*$; $\lvert Y\rvert\le B$, dự đoán cắt: mẫu xác thực." và "(mười: $0{,}4350$)". Học viên phải đoán quan hệ giữa các vế (điều kiện nào, kết luận nào, $0{,}4350$ là cận của quy tắc nào). | Mặt trang 7-02 dòng 3–4; ghi chú diễn giả 7-02 mới giải thích. | "Bậc đa thức tốt nhất phụ thuộc $\sigma^2$ và $f^*$ chưa biết; khi $\lvert Y\rvert\le B$ và dự đoán được cắt, chọn bậc bằng mẫu xác thực." và "… $L_D\le0{,}3651$ (ERM trên mười chỉ số: $0{,}4350$)". |
| trung bình | 5-02, 5-03 | Tiêu đề "SRM với xác suất thất bại 1/m" bị CSS in hoa thành "… 1/M"; trên cùng trang $M$ là hàm cỡ mẫu $M(\epsilon,\delta,h)$. Học viên đọc tiêu đề thành "1/M", trùng kí hiệu. | Ảnh `wide-038-L04-5-02.png`, `wide-039-L04-5-03.png`: "SRM VỚI XÁC SUẤT THẤT BẠI 1/M". | Viết $1/m$ bằng KaTeX trong tiêu đề và kiểm ảnh (KaTeX có thể vẫn bị `text-transform`), hoặc đổi tiêu đề: "SRM với xác suất thất bại giảm theo cỡ mẫu". |
| nhẹ | 5-02 | Trang dày nhất về khái niệm: một hệ quả với giả thiết ba vế, định nghĩa mới $\mathrm{pen}_k(m)$, hai kí hiệu mới $M_k(\epsilon)$, $k(h)$, rồi bảo đảm; 60 âm tiết. Ở lần nghe đầu, học viên khó giữ cả bốn đối tượng. Trong trần. | Đếm: 60 âm tiết, 5 dòng. | Chuyển dòng "**Kí hiệu:**" lên trước "**Hệ quả 04.15.**" hoặc rút "khi còn lại" thành "nếu không"; không thêm chữ. |
| nhẹ | 1-02 | "(T1), (T3), (T4) cho $S$ $r_m$-đại diện" đặt hai kí hiệu sát nhau, đọc thành "$S\,r_m$"; ở 390 px "$\rho_m$" và "-đại diện" xuống dòng tách nhau. $\rho_m$ dùng trên mặt trang mà công thức chỉ ở ghi chú diễn giả. | Mặt trang 1-02 dòng 4–5; ảnh `narrow-001-L04-1-02.png`. | "… cho $S$ là $r_m$-đại diện"; thêm $\rho_m$ dạng ngắn nếu còn chỗ, hoặc ghi "(bán kính VC, Bài 03)". |
| nhẹ | 2-01 | Dòng 1 giới thiệu họ $\mathcal H_1,\mathcal H_2,\ldots$; dòng 2 viết $\tilde h(S)\in\mathcal H$ mà không nói $\mathcal H$ là một lớp của họ. | Mặt trang 2-01. | "Với một lớp $\mathcal H$ của họ, bộ giải (solver) trả về …". |
| nhẹ | 2-03 | Dẫn "$D_\eta$ (Ví dụ 01.2)", nhưng $D_\eta$ được định nghĩa ở Ví dụ 01.1; Ví dụ 01.2 tính rủi ro các $h_t$. Mặt trang không nói vì sao xét $h_2$. | Ghi chú Bài 04, Ví dụ 04.2: "Phân bố $D_\eta$ của Ví dụ 01.1 … Theo Ví dụ 01.2, …"; ghi chú Bài 01 dòng 121–143. | "$D_\eta$ (Ví dụ 01.1), rủi ro của $h_t$ (Ví dụ 01.2)". |
| nhẹ | 2-05 | "Trực quan." đặt trước phát biểu dùng $h$, $r$, $\operatorname{opt}_S$ chưa giới thiệu trên trang, và là bản rút gọn của chuỗi bất đẳng thức ở 2-06 hơn là cách đọc kết quả. | 2-05 dòng 1; 2-06 chuỗi bất đẳng thức. | Đổi thành cách đọc ba số hạng: "Ba số hạng ba nguồn: lớp (không quan sát được), mẫu ($2r$, tính được), bộ giải ($\operatorname{opt}_S$, tính được trên $S$)." |
| nhẹ | 2-06, 4-09 | "Kết luận:" dẫn "Hệ quả 02.16(b), 03.16(b)" và "Hệ quả 03.16(a)" chỉ bằng số, không nhắc nội dung; học viên không kiểm được tại chỗ. | 2-06, 4-09 dòng "Kết luận:". | Thêm nội dung một vế: "… ERM xấp xỉ có rủi ro vượt mức $\le2r+\epsilon_{\mathrm{opt}}$ (Hệ quả 02.16(b), 03.16(b))". |
| nhẹ | 2-07 | (1) "hai cận chưa đúng đồng thời" khó hiểu: mỗi cận đúng với xác suất $\ge0{,}95$, nên cả hai cùng đúng với xác suất $\ge0{,}90$; điều thiếu là bảo đảm ở mức $0{,}95$ cho cả hai. (2) $\tilde h_2$, $\tilde h_{10}$ chưa định nghĩa trên mặt trang và dễ lẫn với hàm ngưỡng $h_2$ ở 2-03, 2-04. | 2-07 dòng 3 và "Kết luận:"; ghi chú §4 đoạn sau Ví dụ 04.3 dùng cùng câu "Hai cận chưa đúng đồng thời". | (1) "mỗi cận chỉ được bảo đảm cho một lớp chọn trước; chọn lớp theo $S$ cần chia $\delta$ giữa các lớp"; (2) thêm "$\tilde h_k$: đầu ra của bộ giải trên $\mathcal H_k$". Xem đề xuất sửa ghi chú. |
| nhẹ | 3-04 | Dòng 2 nhảy từ $\hat f^{(j)}(x_0)=\sum_iw_iY_i$ sang $\bar f(x_0)=w_1+w_3$ mà không nêu $\mathbb EY_i=x_i^2=(1,0,1)$; lý do chỉ có trong ghi chú diễn giả. | Mặt trang 3-04 dòng 2. | "… $\mathbb EY_i=x_i^2$ nên $\bar f(x_0)=w_1+w_3$". |
| nhẹ | 4-04 | "bán kính tăng từ $1\%$ ($k=1$) đến $3{,}2\%$ ($k=4$)" đọc như bán kính tăng đơn điệu; thực tế mức tăng tương đối là $1{,}0\%$; $2{,}75\%$; $3{,}13\%$; $3{,}17\%$; rồi giảm còn $2{,}57\%$ ở $k=10$ (tính lại). | Tính lại $\mathrm{pen}_k$ theo dạng chiều VC, $q_k=6/(\pi^2k^2)$, $m=10^4$, $\delta=0{,}05$. | "mức tăng tương đối nằm giữa $1\%$ ($k=1$) và $3{,}2\%$ ($k=4$)". |
| nhẹ | 5-04 | Trang tiêu đề "Ví dụ: …" chứa phát biểu Định lý 04.16(a) với "Giả thiết:"/"Bảo đảm:"; học viên không thấy định lý (đọc thêm) thuộc bước nào của mạch. | 5-04 dòng 5–6. | Mở dòng định lý bằng câu nối "Điều kiện cần cho học không đều:" hoặc ghi rõ "(đọc thêm)" trên mặt trang; giữ trong trần. |
| nhẹ | 6-02 | Dòng "Nhắc lại:" viết "$L_D(h)\le L_S(h)+\sqrt{\ln(K/\delta)/(2m)}$ (Định lý 02.14(b))" thiếu lượng từ "đồng thời mọi $h\in\mathcal H$, $\lvert\mathcal H\rvert=K$"; $K$ ở đây là cỡ lớp của Bài 02, trên trang lại là số ứng viên. | Mặt trang 6-02. | "…, đồng thời mọi $h$ của lớp $K$ phần tử". |
| nhẹ | 7-01 | Hàng "Hệ quả 04.17: $L_D(\hat g)-\min_jL_D(g_j)$" không có vế cận, đọc như câu chưa xong. | Bảng 7-01 hàng cuối. | "$L_D(\hat g)-\min_jL_D(g_j)\le2\sqrt{\ln(2K/\delta)/(2m_v)}$" hoặc "… cỡ $\sqrt{\ln K/m_v}$". |
| nhẹ | 7-03 | 76 âm tiết (trần 60, dưới 1,5 lần), có lý do ghi trong storyboard. Ở 1600×900 trang vừa khung và đọc được. Dòng "Gọi $\hat h_{(2)}$, $\hat h_{(5)}$ … là đầu ra của SRM." (13 âm tiết) chỉ cần cho lời giải. | `deck_lint.py`; `storyboard.md` mục "Ngoại lệ mật độ". | Chấp nhận ngoại lệ, hoặc chuyển dòng "Gọi …" sang đầu 7-04 để còn khoảng 63. |
| nhẹ | 3-05, 3-07, 4-05, 6-03, 2-08 | Dấu câu sau KaTeX rơi xuống dòng riêng: "tổng $1{,}25$ / ." (3-05), "sai số xấp xỉ $0$ / ." (3-07), "$h_k(x)=x_k$ / ; hàm lỗi" (4-05), "$\delta=0{,}05$ / ." (6-03), "$0{,}18$ / -đại diện" (2-08). | Ảnh `wide-020`, `wide-022`, `wide-028`, `wide-044`, `wide-014`. | Đưa dấu câu vào trong `$…$` hoặc bọc công thức và dấu câu trong `span` không ngắt dòng (`white-space:nowrap`). |

Không phát hiện chặn bàn giao. Các ví dụ tính tay (2-08, 3-04, 3-05, 3-06, 4-05, 4-11, 6-03, 6-04, 6-05, 7-04) đi đủ chậm để theo; các số đã tính lại khớp: $\rho_m$ $0{,}16443$, $0{,}27992$, ngưỡng $0{,}2310$; bảng $\mathrm{pen}_k$ và tổng 4-07; 4-12; cỡ mẫu $172\,279$, $181\,575$, $213\,317$; $0{,}1095$, $0{,}1871$, $1199$, $4794$; $0{,}4524$; $0{,}1103$; $0{,}858$, $0{,}99994$, $0{,}7279$; $0{,}1858$, $0{,}2699$, $0{,}3716$, $0{,}5399$.

## Đề xuất sửa ghi chú

| vị trí | vấn đề | đề xuất |
|---|---|---|
| Ghi chú Bài 04, §4, đoạn "Tóm lại" sau Ví dụ 04.3 (dòng 310: "Hai cận chưa đúng đồng thời; …") | Câu dễ hiểu sai: hai cận vẫn có thể cùng đúng (theo bất đẳng thức hợp, với xác suất ít nhất $0{,}90$); điều thiếu là bảo đảm ở mức $0{,}95$ cho cả hai và cho mọi lớp có thể được chọn. Câu cũng nói về trạng thái chưa đạt thay vì nêu điều kiện. | Thay bằng: "Mỗi cận chỉ được bảo đảm cho một lớp chọn trước; để chọn lớp theo tập huấn luyện, chúng ta cần chia $\delta$ giữa các lớp." (chờ tác giả duyệt). |

## Kết luận

**đạt khi sửa** — 0 chặn bàn giao, 1 nghiêm trọng (2-03, hình không đọc được ở 390 px), 6 trung bình, 14 nhẹ.
