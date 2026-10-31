# Rà toán bộ bài tập Bài 08 (người rà 2)

**Đối tượng.** Bản đóng băng `lec08-ex-frozen.md`; số dòng trong bảng phát hiện theo bản này.

**Căn cứ.** Ghi chú đã duyệt `2627-1/materials/lec-08/lecture-note.md`: Phụ lục C chứng minh Hệ quả 08.8, Phụ lục D phác thảo Mệnh đề 08.10, Phụ lục F là giao thức thí nghiệm. Thêm Bài 05 (Nhận xét 05.17) và Bài 06 (Ví dụ 06.3, Phụ lục D, công thức $c_t$ và $\sum c_t$).

**Phép tính lại.** Hai script, đều trong `reviews08/r2/ex/`:
- `ex_check.py` (đầu ra `ex_check_out.txt`): liệt kê đủ trường hợp với phân số chính xác, các tổng, cận và ngưỡng.
- `ex06_paired.py` (đầu ra `ex06_out.txt`): nạp script thí nghiệm, chạy lại cả $\eta=0{,}25$ và $\eta=0{,}5$, rồi tính các hiệu ghép cặp theo từng hạt giống.

Tôi chỉ đọc repo và không commit. Phạm vi là toán học, nên không dùng `no-ai-slop`.

## 1. Tổng kết theo mức

| Mức | Số phát hiện |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 0 |
| nhẹ | 3 |

Tôi tự giải lại được mọi bài và mọi ý. Lượng từ, giả thiết và chiều bất đẳng thức đều đúng. Mọi gợi ý đúng hướng. Mọi số khớp với phép tính lại và với lần chạy lại script, trừ một tỉ số làm tròn sai ở 08.6.

## 2. Từng bài

| Bài | Kết quả | Kiểm tra chính |
|---|---|---|
| 08.1(a) lô nhỏ | ✓ | Tách bước thành $\nabla f_t$ cộng $\tfrac{\eta_tn_t}b\nabla\ell(\cdot,z_i)$, kết quả mới đúng. $f_t$ lồi, gradient $\tfrac{b-n_t}b\beta$-Lipschitz nên $\beta$-trơn, $f_t=0$ khi $n_t=b$. Bổ đề 08.4(b) áp dụng vì $\eta_t\le2/\beta$. Bước khác biệt dùng (G) tại $w_t,w'_t\in W$. $\mathbb En_t=b/m$ chỉ cần tuyến tính. Hệ số ổn định $\frac{2G^2}m\sum\eta_t$ không phụ thuộc $b$; với $b=1$ ta được lại Mệnh đề 08.5 |
| 08.1(b) rút không đều | ✓ | Chỉ Bước 4 đổi, thành $\rho_i$; $\epsilon=2G^2\max\rho\sum\eta_t$. Tổng xác suất là $1$; hệ số $0{,}3$ so với $0{,}2$, gấp $1{,}5$ lần. Lập luận "chọn $\rho$ trước khi thấy mẫu" (Định nghĩa 05.18, ghép cặp giữ phân bố) đúng |
| 08.1(c) Huber, $\eta=1$ | ✓ | $\mathbb E\Delta_2=\tfrac12$, đúng bằng cận. $\mathbb E\Delta_3=\tfrac{13}{16}<1$. Nhóm $i_1\ne4$: $w_2\in\{0,1\}$, tổng $6$. Bảng $i_1=4$: $(0,0,0)$, $(1,0,1)$, $(2,0,2)$, $(2,-2,4)$. Liệt kê máy xác nhận đúng hai dãy chặt ngặt $(4,1)$ hụt $2$ và $(4,2)$ hụt $1$; với $\eta=\tfrac12$ lại được $\tfrac{29}{64}$ |
| 08.2 | ✓ | (a) Các bất đẳng thức tích phân đúng. (b) Ngân sách và cận khớp, làm tròn lên. (c) Giả thiết của Nhận xét 05.17 đúng; sáu cận tối ưu khớp. Bước 4: $\le7{,}5/\ln(T+1)$ và $\ge25/(10(1+\ln T))$ |
| 08.3(a) | ✓ | Vế trái $-0{,}2397$ so với $0{,}2298$. $q_0=f$, nên $q_0(0)=2$ là cực đại. Bất đẳng thức then chốt tại $(0,\pi/2)$ cho $-1<\tfrac12$. Bước 1 của Phụ lục A vẫn đúng |
| 08.3(b) | ✓ | Khớp ghi chú: tính lồi của hàm lỗi chỉ đi vào ở bước chung; Bước 2 của 08.5 và Bước 1 của 08.6 chỉ dùng (G) và $W$ lồi. Một ô thiếu "$W$ lồi" (phát hiện 2) |
| 08.3(c) | ✓ | $\varphi'\in[0{,}9;1{,}1]$; $w'_t\in(-\pi,0)$ đúng bằng quy nạp; định lý giá trị trung bình cho $\Delta_{t+1}=\varphi'(\zeta)\Delta_t$. Cận dưới $\tau\ge68$ (vì $65{,}20$); cận trên $\tau\le76$ ($0{,}5051>\tfrac12$, còn với số mũ $73$ chỉ được $0{,}464$). Mô phỏng cho $\tau=68$ |
| 08.3(d) | ✓ | $\le0{,}0149$; dùng tổng tính bằng máy được $0{,}0136$; tích chính xác cho $0{,}01334$, nằm dưới cả hai. Cận lồi $0{,}0104$ và $0{,}2$; $e^{10}$, $e^{0{,}5187}$ đúng |
| 08.4 | ✓ | (a) $\sigma^2=0$, vế phải $40/T$, $\operatorname{opt}_s(0)=2$. (b) Chứng minh đúng; phản ví dụ trên $[-4,4]$ đúng vì $\pi\in W$. (c) Số khớp Phụ lục F. (d) $1{,}0001$; $\eta=0{,}02355\le4$; $0{,}011774\le0{,}0118$; $\sqrt{0{,}0118}=0{,}1086\le0{,}109$ |
| 08.5(a)–(c) | ✓ | Đạo hàm trái $0$, phải $-\tfrac12$; $0{,}6931>0{,}5032$. $\partial_{\theta_1}\ell=-\theta_2/(1+e^{\theta_1\theta_2})$, nên $\lvert\cdot\rvert=\theta_2/(1+e)$ không bị chặn. Bảng giả thiết đúng, kể cả (T2) và "$\eta\le2/\beta$ không xác định" |
| 08.5(d)(i) | ✓ | $0{,}4G^2$, điều kiện $0{,}1\le8/G^2$; với $G=1{,}5$ cận là $0{,}9$ |
| 08.5(d)(ii) | ✓ | Lập luận hợp lệ. Bước 1 của Phụ lục D chỉ dùng $\lVert\nabla\ell(u)-\nabla\ell(v)\rVert\le\beta\lVert u-v\rVert$ tại $u=w_t$, $v=w'_t\in W$, cộng với phép chiếu không giãn. Bước khác biệt dùng (G) trên $W$. Vậy chỉ cần tính trơn trên $W$, khác Phụ lục A, nơi điểm $v^+$ có thể ra ngoài $W$. Với $W$ compact và hàm kích hoạt $C^2$, cả $G$ và $\beta_W$ hữu hạn. $1{,}1^{10^5}=10^{4139{,}27}$. Câu dẫn Nhận xét 08.11 ở cuối cần nói rõ hơn (phát hiện 3) |
| 08.6 | ✓ (một tỉ số làm tròn sai) | Chạy lại: bốn bảng cột $\eta=0{,}25$ khớp đến chữ số thứ ba. Hiệu ghép cặp (trung bình; độ lệch chuẩn) khớp cả tám ô. Sai số chuẩn $0{,}0011$; $0{,}0034$; $0{,}0017$; $0{,}0015$; $0{,}0013$; $0{,}0014$; $0{,}0021$; $0{,}0009$, khớp. Tỉ số $1{,}74$; $6{,}46$; $0{,}63$; $3{,}97$; $1{,}00$; $1{,}03$; $0{,}39$; $1{,}28$: bản nháp ghi $1{,}8$ cho ô đầu (phát hiện 1). Sai số chuẩn khi coi độc lập là $0{,}0263$ (độ lệch chuẩn $0{,}0847$ và $0{,}0817$), gấp khoảng $12{,}5$ lần sai số chuẩn ghép cặp; tương quan theo hạt giống là $0{,}994$. $\alpha=0{,}489$ và $0{,}569$. Tỉ số $0{,}25/0{,}0246=10{,}2$ (bản nháp ghi $10$, theo số đã làm tròn) |
| 08.7 | ✓ | Công thức đóng của $\psi$ khớp Phụ lục D của Bài 06; tổng trực tiếp cho cùng giá trị. $q^T=0{,}8708$; $0{,}1320$; $1{,}8\cdot10^{-9}$. $\psi=0{,}0301$; $0{,}2843$; $0{,}4750$. Cận $0{,}25$; $4$; $39{,}975$. Ngưỡng $T\le161$ và $T\le80$. Các tỉ số $8{,}3$; $14{,}1$; $84{,}2$. $\psi<2/m$ và $\psi$ tăng |
| 08.8 | ✓ | (a) đúng. $\eta=0{,}1$: $T^*=3535{,}5$, $B=0{,}120701\le0{,}1208$. $\eta=0{,}02$: $T^*=17\,677{,}7$, $B=0{,}080709\le0{,}0808$. Độ lệch tại số nguyên kề $T^*$ là $8\cdot10^{-10}$ và $5\cdot10^{-11}$, đều dưới $10^{-8}$. Giới hạn $0{,}0708$. (c) và (d) đúng; khi $\eta=0{,}05$ được lại $0{,}0958$ |

## 3. Bảng số (chọn lọc; đủ ở các tệp đầu ra)

| Vị trí | Bản nháp | Tính lại |
|---|---|---|
| 08.2(b) | $51{,}06$; $995$; $62{,}57$; $3157{,}28$; $48{,}94$; $992{,}72$; $60{,}45$; $3154{,}98$ | $51{,}052$; $995$; $62{,}565$; $3157{,}278$; $48{,}938$; $992{,}723$; $60{,}451$; $3154{,}984$ |
| 08.2(b) bảng | $0{,}0098$; $0{,}0103$; $0{,}0121$; $0{,}0126$; $0{,}1986$; $0{,}199$; $0{,}6310$; $0{,}6315$ | $0{,}009788$; $0{,}010210$; $0{,}012090$; $0{,}012513$; $0{,}198545$; $0{,}199$; $0{,}630997$; $0{,}631456$ |
| 08.2(c) | $0{,}05$; $0{,}6756$; $0{,}1359$; $0{,}0275$; $0{,}5470$; $0{,}0519$ | $0{,}05$; $0{,}675557$; $0{,}135834$; $0{,}0275$; $0{,}546917$; $0{,}051863$ |
| 08.3(c) | $6{,}2146$; $65{,}2$; $1{,}08776$; $0{,}505$; $\tau=68$ | $6{,}21462$; $65{,}204$; $1{,}087758$; $0{,}50511$; $68$ |
| 08.3(d) | $4{,}6904$; $1{,}5849$; $0{,}0149$; $4{,}2780$; $0{,}0136$; $0{,}5187$; $0{,}0104$ | $4{,}690427$; $1{,}584893$; $0{,}014868$; $4{,}278024$; $0{,}013560$; $0{,}518738$; $0{,}010375$ |
| 08.6 bảng ghép cặp, $\eta t=50$ | $0{,}0011$; $1{,}8$ | $0{,}00107$; $1{,}74$ |
| 08.6 độc lập | $0{,}1177/4{,}472\approx0{,}0263$ | $0{,}026313$ |

## 4. Phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | dòng 650 | Tỉ số giữa trị tuyệt đối của trung bình hiệu khoảng cách và sai số chuẩn ở $\eta t=50$ được ghi $1{,}8$; giá trị đúng là $1{,}7$. Kết luận "không vượt hai lần" không đổi. | $0{,}0019/0{,}0011=1{,}73$; tính từ dữ liệu chạy lại được $1{,}74$ (`ex06_out.txt`). | Đổi "$1{,}8$" thành "$1{,}7$". |
| nhẹ | dòng 312 (bảng 08.3(b)) | Ô "Dùng" của "08.5, Bước 1" thiếu "$W$ lồi". Bước này dùng Bổ đề 08.4(c), tức phép chiếu không giãn. | Ghi chú, chứng minh Mệnh đề 08.5 Bước 1: "Theo Bổ đề 08.4(c)"; các dòng 313, 316, 319 của bảng đều ghi "$W$ lồi". | "lồi, trơn, $\eta_t\le2/\beta$, $W$ lồi". |
| nhẹ | dòng 543 (08.5(d)(ii)) | Câu "trừ khi độ dài bước giảm như $c/t$ và hàm lỗi bị chặn (Nhận xét 08.11)" áp Nhận xét 08.11 ra ngoài phát biểu của nó. Nhận xét đó cần SGD không chiếu, tính trơn trên $\mathbb R^p$ và hàm lỗi trong $[0,1]$; thiết lập (ii) có phép chiếu, tính trơn chỉ trên $W$, và hàm lỗi trong $[0,M]$. | Ghi chú, Nhận xét 08.11, các mục Hàm lỗi và Thuật toán. | "… trừ khi độ dài bước giảm như $c/t$ và hàm lỗi bị chặn; Nhận xét 08.11 phát biểu cho SGD không chiếu và hàm lỗi trong $[0,1]$, nên cần chia hàm lỗi cho $M$ và kiểm lại lập luận với phép chiếu." |
