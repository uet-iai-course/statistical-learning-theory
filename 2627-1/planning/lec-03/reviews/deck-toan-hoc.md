# Duyệt deck Bài 03 — Vai 2 `toan-hoc` (độ chính xác toán học, thống nhất với ghi chú)

Bản duyệt: `2627-1/lecture-03-chieu-vc.html` (55 trang, bản đóng băng), bảy SVG trong `2627-1/img/lec-03/`. Đối chiếu: `materials/lec-03/lecture-note.md`, `exercises.md` (Bài tập 03.1–03.5, 03.9, 03.11, 03.12), `materials/lec-02/lecture-note.md` (Định lý 02.14, Hệ quả 02.16), `materials/lec-01/lecture-note.md` (Nhận xét 01.26), quyết định "Bộ trang chiếu" cuối `review-log.md`.

Cách kiểm: đọc mã HTML (mặt trang và ghi chú diễn giả) và mã SVG; tính lại bằng Python (`math`, tổng nhị thức chính xác, chia đôi khoảng cho cỡ mẫu) mọi con số trên mặt trang, trong ghi chú diễn giả và trong tọa độ, nhãn SVG. Kịch bản: `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-03/rv-toan-hoc/calc.py`. Chạy `deck_check.py` (không chụp ảnh): console 0, pageerrors 0, failed 0, `katexErrors` 0 trên cả 55 trang.

## 1. Kết quả tính lại

**Mọi con số đều khớp** với ghi chú và tệp bài tập (sai khác chỉ ở chữ số làm tròn cuối). Các nhóm đã kiểm:

- **Chiều VC các lớp ví dụ.** $\mathcal H_{\mathrm{thr}}$: $d=1$ (nhân chứng $\{0\}$, $h_0(0)=1$, $h_1(0)=0$; cận trên $x_2<t\le x_1$). $\mathcal H_{\mathrm{int}}$: $d=2$ (bốn khoảng $[0,1],[0,0],[1,1],[2,2]$; cận trên $(1,0,1)$). $\mathcal H^p_{\mathrm{aff}}$: $p+1$; $\mathcal H^p_{\mathrm{hom}}$: $p$; $\mathcal H^{10}_{\mathrm{aff}}$: $11$, $\mathcal H^2_{\mathrm{aff}}$: $3$. Nhận xét 03.10(ii): $k=3$, $y=(1,0,1)$ cho $\theta=\pi(1+4)=5\pi$, $\sin(5\pi/2)=1$, $\sin(5\pi/4)<0$, $\sin(5\pi/8)>0$. (iii): ba hàm, $d=1$. $\mathcal M_{[0,1]}$: $d=\infty$. $\mathcal G_S$: $d=1$. Bài tập 03.2(b): $d=4$.
- **Ví dụ 03.3 (3-02, 3-06).** Công thức $b=2y_0-1$, $w_i=2y_i-1-b$ cho đủ tám cách: $(1,0,1)\to b=1$, $w=(-2,0)$, giá trị $1,-1,1$; $(0,1,1)\to b=-1$, $w=(2,2)$. Hình vuông $14=2+4+4+4$; $(1,1)=\tfrac13(0,0)+\tfrac13(3,0)+\tfrac13(0,3)$.
- **Hàm tăng trưởng.** $\Pi_{\mathcal H_{\mathrm{thr}}}(m)=m+1$, $\Pi_{\mathcal H_{\mathrm{int}}}(m)=\binom{m+1}2+1$, tại $m=5$: $6$, $16=\sum_{j\le2}\binom5j$, $2^5=32$. $\Pi_{\mathcal H^2_{\mathrm{aff}}}(m)=2,4,8,14$ ($m\le4$); tổng nhị thức $d=3$: $2,4,8,15,26$, $1351$ tại $m=20$.
- **Ví dụ tách điểm cuối (4-04).** $\mathcal H_{\mathrm{int}}$ trên $(1,2,3)$: $\mathcal H_C$ bảy cách thiếu $101$; $\mathcal H_{C'}$ bốn cách; $Y_1=\{00,01,11\}$; $7=4+3=(1+2+1)+(1+2)=1+3+3$; $Y_1$ có chiều VC $1$. Ghi chú diễn giả: lớp hàm ngưỡng $\mathcal H_C=\{000,001,011,111\}$, $\mathcal H_{C'}=\{00,01,11\}$, $Y_1=\{00\}$, $4=3+1$. Đúng.
- **Dạng đóng Sauer–Shelah.** Chuỗi bất đẳng thức của 4-05 đúng (gộp hai bước của ghi chú, ghi chú diễn giả nói rõ). $(em/3)^3=20{,}09;\ 47{,}61;\ 92{,}99;\ 5951{,}27$ tại $m=3,4,5,20$; $(e/3)^3\approx0{,}7439<2$. Dạng đóng lớn hơn $2^m$ đúng khi $3\le m\le9$ ($m=9$: $542{,}3>512$; $m=10$: $743{,}9<1024$).
- **Định lý 03.15, Ví dụ 03.7 (5-08).** $\ln80=4{,}3820$; $2em/3=18\,122$; $3\ln18\,122=29{,}415$; $8(29{,}415+4{,}382)/10^4=0{,}027037$; $\sqrt{\cdot}=0{,}1644$. Bảng dạng trực tiếp $0{,}464;0{,}164;0{,}0571$ ($d=3$), $0{,}762;0{,}280;0{,}0993$ ($d=11$); dạng hằng số $4$: $0{,}621;0{,}223;0{,}0779$ và $1{,}014;0{,}379;0{,}136$; tỉ số $1{,}331$–$1{,}366$ ("$1{,}33$ đến $1{,}37$"); giảm $2{,}72$–$2{,}88$ lần ("$2{,}7$ đến $2{,}9$"). $\sqrt{16\ln2}=3{,}330$; $8\ln4=11{,}09$. Kiểm lại $4\Pi e^{-m\rho_m^2/8}=\delta$, hằng số $(1+\ln2)<2$ cho dạng hằng số $4$, và Bước C.7 (tiếp tuyến tại $u_0=4e\kappa$, $\kappa=8/\epsilon^2$) cho đúng $\tfrac{16}{\epsilon^2}(d\ln\tfrac{32}{\epsilon^2}+\ln\tfrac4\delta)$.
- **Ví dụ 03.8 (5-09).** $\ln(2e\cdot1000)=8{,}6009$; $\sqrt{0{,}008\cdot12{,}983}=0{,}3223$. Bài tập 03.5(c): $\sqrt{8\ln80/1000}=0{,}187$. Bài tập 03.4(d) (ghi chú diễn giả 5-03): $\sqrt{\ln(2\cdot2^{1000}/0{,}05)/2000}=0{,}5903$.
- **Ví dụ 03.9 (6-03).** Chia đôi khoảng cho điều kiện $\tfrac{32}m(d\ln\tfrac{2em}d+4{,}382)\le0{,}01$: **$54\,330$**, $132\,992$, **$447\,194$** (cùng kết quả khi dùng $\ln80$ chính xác); vế trái tại $54\,330$ / $54\,329$: $0{,}0099999$ / $0{,}0100001$. Dạng đóng $M(0{,}1;0{,}05)=88\,572$; $209\,624$; $693\,832$ (tỉ số $1{,}55$–$1{,}63$). Dạng hằng số $4$: $103\,939$; $261\,198$; $889\,572$. $447\,194/132\,992=3{,}3626$; $11/3=3{,}667$. Đạo hàm $(d-d\ln\tfrac{2em}d-c)/m^2<0$ đúng.
- **Ví dụ 03.10 (6-04).** $65\ln2+\ln20=48{,}050\to9611$; $705\ln2+\ln20=491{,}664\to98\,333$; tỉ số $5{,}653$ và $4{,}548$; $\sqrt{8\ln480/1000}=0{,}2222$; $\sqrt{\ln240/2000}=0{,}0523$; tỉ số $4{,}245$. Bài tập 03.4(e): $193\ln2+\ln20=136{,}773\to27\,355$; $4{,}86=16\cdot0{,}304$.
- **Định lý 03.17(a).** $(\tfrac14-\tfrac18)/(1-\tfrac18)=\tfrac17$ (ghi chú diễn giả 6-05).
- **Cầu nối (7-06).** $2\cdot0{,}1644=0{,}329$, $2\cdot0{,}2799=0{,}560$. Bài tập 03.4(a) (7-05): $589\,118$ ($d=3$), $1\,999\,657$ ($d=11$).
- **Bài tập 03.1(a) (7-03).** $\Pi(m)=\min\{m+1,6\}$, $\Pi(3)=4$, $\Pi(8)=6$; lời giải hai chiều (nhiều nhất $k+1$, đủ $k+1$ bằng $t=x_i$ và $t=x_k+1\le6$) khớp tệp bài tập.

**SVG** (tọa độ tính lại từ dữ liệu):

- `so-cach-gan-nhan.svg`: trục dọc $y=330-\tfrac{300}7\log_{10}v$, trục ngang $x=95+\tfrac{375}{19}(m-1)$. Hai mươi điểm $2^m$, hai mươi điểm tổng nhị thức ($d=3$), mười tám điểm dạng đóng từ $m=3$ và bốn ô vuông $2,4,8,14$ (tâm $y=280{,}9$ tại $m=4$) đều đúng. Nhãn $1\,048\,576$, $5951$, $1351$ đúng. Alt "nằm trên đường hai mũ m khi m từ 3 đến 9" đúng.
- `ban-kinh-vc.svg`: $y=320-362{,}5\,v$, $x=85+237{,}5\log_{10}(m/1000)$; bảy cỡ mẫu $1;2;5;10;20;50;100$ nghìn cho cả hai đường đều đúng đến $0{,}1$ px; sáu nhãn số đúng.
- `khoang-hai-diem.svg`: $115$ px/đơn vị, bốn khoảng và ba điểm đúng vị trí, tô đặc đúng nhãn $1$.
- `nua-mat-phang-ba-diem.svg`: $60$ px/đơn vị, gốc tại $(x_0+30,y_0+90)$ mỗi ô. Sáu đường $x=\tfrac12$, $y=\tfrac12$, $x+y=\tfrac12$ đúng là $\langle w,x\rangle+b=0$ của công thức ($001$, $110$: $y=\tfrac12$; $010$, $101$: $x=\tfrac12$; $011$, $100$: $x+y=\tfrac12$); miền gạch luôn là phía nhãn $1$.
- `radon.svg`: tâm $z=(140;155)$ đúng giao hai đường chéo; tam giác $62{,}53$ px/đơn vị, $(1,1)$ tại $(418{,}8;186{,}2)$ đúng; $I$ tô đặc, $J$ rỗng như chú giải.
- `doi-cho.svg`: $\sigma=(+1,-1,+1,-1)$, đổi chỗ đúng ở cột $2$, $4$; hàng trên sau khi đổi $Z_1,Z'_2,Z_3,Z'_4$.
- `dinh-ly-co-ban.svg`: bảy mũi tên đúng danh sách kéo theo của ghi chú: $(6)\to(1)$, $(1)\to(2)$, $(2)\to(3)$, $(2)\to(5)$, $(3)\to(4)$, $(5)\to(4)$, $(4)\to(6)$ (mũi tên đậm "phần (a)").

## 2. Đối chiếu phát biểu với ghi chú

| Kết quả | Trang | Giả thiết | Lượng từ | Loại bảo đảm, hằng số | Kết luận |
|---|---|---|---|---|---|
| Định nghĩa 03.1–03.3, Nhận xét 03.4 | 2-02, 2-03, 2-04 | đủ (bỏ chữ "$k\ge1$", "khác rỗng" ở 03.3 — chấp nhận được) | — | — | khớp |
| Mệnh đề 03.5, 03.6 | 2-05, 2-06 | đủ hai trường hợp (a), (b) của 03.5 | — | tất định | khớp |
| Bổ đề 03.8 | 3-03 | $p\ge1$, $p+2$ điểm | tồn tại $I,J$ khác rỗng, rời nhau, phủ | tất định | khớp |
| Mệnh đề 03.9 | 3-04, 3-05 | $p\ge1$, hai lớp | — | tất định, theo $p$ | khớp; quy ước $\ge0$ và $J\ne\varnothing$ vào đúng bước |
| Định nghĩa 03.11 | 4-01 | bộ có điểm lặp | — | — | khớp |
| Bổ đề 03.12 | 4-02, 4-03, 4-05 | $\mathcal H\ne\varnothing$, $d<\infty$, $m\ge1$; (b) $1\le d\le m$ | — | tất định | khớp |
| Định nghĩa 03.13 | 5-01 | đo được | $\exists M\ \forall\epsilon,\delta\ \forall D\ \forall m\ge M$ | xác suất cao | khớp |
| Định lý 03.15 | 5-04, 5-05 | (T1), $m\ge1$, 0–1, (T5), (M), $\delta\in(0,1)$; (b) $1\le d\le m$; (c) $1\le d<\infty$ | mọi $D$, đồng thời mọi $h$ | xác suất $\ge1-\delta$; $8$, $4$, $16$, $32$ đúng | khớp |
| Hệ quả 03.16 | 6-01, 6-02 | (T1), 0–1, (T5), (M), $1\le d<\infty$, ERM thỏa Định nghĩa 01.4 hoặc (O2) | mọi $D$, đồng thời mọi nghiệm ERM | xác suất $\ge1-\delta$; $2\rho_m$, $+\epsilon_{\mathrm{opt}}$, $64$, $128$ đúng | khớp |
| Định lý 03.17(a) | 6-05 | 0–1, (T1), $\mathcal H\ne\varnothing$, $A$ theo Định nghĩa 01.4; không dùng (M) | $\forall A\ \exists D$ khả diễn | $>1/8$, $\ge1/7$ | khớp |
| Định lý 03.17(b) | 6-06, 6-07 | thêm (M) và **có một thuật toán ERM thỏa Định nghĩa 01.4** (phát hiện cổng duyệt đã sửa) | — | tương đương sáu khẳng định | khớp; năm nhóm kéo theo đúng nguồn |
| Hệ quả 03.18 | 6-07 (Kết luận) | $\mathcal M_{[0,1]}$ | mọi thuật toán | — | khớp |
| Định lý 03.19 | 6-08 | 0–1, (T1), chiều VC $d$; (a) $1\le d<\infty$; (b) $2\le d<\infty$ | $\exists c,\epsilon_0,\delta_0\ \forall\epsilon,\delta,A,m\ \exists D$ | $>\delta$; $1/\epsilon^2$, $1/\epsilon$ | khớp; "đọc thêm" ghi ở mặt trang và ghi chú diễn giả |

**Lộ trình đối xứng hóa và mẫu bóng** (5-03, 5-05, 5-06, 5-07) khớp ghi chú: hai trở ngại (i), (ii) và cách sửa; Bước 1 mẫu bóng với Chebyshev, $\operatorname{Var}\le\tfrac14$, điều kiện $m\epsilon^2\ge2$, hệ số $2$, chỗ dùng (T1), (M); Bước 2 đổi chỗ, dấu ngẫu nhiên, (T1); Bước 3 đếm trên mẫu gộp, (T5); Bước 4 Hoeffding miền dài $2$, $2e^{-m\epsilon^2/8}$, bất đẳng thức hợp; Bước 5 giải theo $\delta$, Sauer–Shelah tại $2m$ điểm, tiếp tuyến cho (c). Bất đẳng thức then chốt đúng hướng, đúng hằng số. Bước tất định của Hệ quả 03.16 đúng ba dấu $\le$ và chỗ dùng (O1). Phản ví dụ Ví dụ 03.6, 03.8, Bài tập 03.5(c) đúng.

## 3. Bảng phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L03-5-07 (mặt trang) | Hằng số sai trong dòng so sánh: phần $\delta$ dành cho mỗi cách gán nhãn không phải $\delta/\Pi_{\mathcal H}(2m)$. | Mặt trang: "**Nhắc lại:** chia $\delta/K$ cho từng giả thuyết (Bài 02); ở đây $\delta/\Pi_{\mathcal H}(2m)$ cho từng cách." Với $\epsilon=\rho_m$, mỗi cách có xác suất có điều kiện $2e^{-m\epsilon^2/8}=\delta/(2\Pi_{\mathcal H}(2m))$ (ghi chú, Phụ lục C.4–C.5: $\Pr(B_\epsilon)\le2\Pr(W)\le4\Pi e^{-m\epsilon^2/8}=\delta$). Ở Bài 02, $2e^{-2mr_m^2}=\delta/K$. | Viết "ở đây $\delta/(2\Pi_{\mathcal H}(2m))$ cho từng cách; thừa số $2$ còn lại đến từ mẫu bóng", hoặc bỏ dòng "Nhắc lại:" và giữ công thức $\ln\tfrac{2K}\delta\to\ln\tfrac{4\Pi_{\mathcal H}(2m)}\delta$. |
| trung bình | L03-4-02 (ghi chú diễn giả) | Khẳng định toán học sai. | "Từ $m&gt;d$, phần lớn các cách gán nhãn bị thiếu." Tại $m=d+1$, tổng nhị thức bằng $2^{d+1}-1$; với $\mathcal H^2_{\mathrm{aff}}$, $m=4$: $14$ trong $16$ cách thực hiện được (Ví dụ 03.5, Bước 4). Ghi chú không có câu này. | "Từ $m&gt;d$, mỗi tập $m$ điểm thiếu ít nhất một cách gán nhãn; khi $m$ lớn hơn nhiều so với $d$, phần lớn bị thiếu: tại $m=20$, $d=3$, nhiều nhất $1351$ trong $2^{20}$ cách." |
| trung bình | L03-2-01, L03-5-03 (ghi chú diễn giả) | Khẳng định quá rộng về điều kiện (M), không có cơ sở trong ghi chú; sai với $\mathcal M_{[0,1]}$. | 2-01: "các lớp của bài đều thỏa (M) với lớp con có tham số hữu tỉ"; 5-03: "Các lớp của bài thỏa (M) với tham số hữu tỉ". Nhận xét 03.14 chỉ nêu lớp hàm ngưỡng, lớp khoảng, lớp nửa không gian afin (và lớp hữu hạn). $\mathcal M_{[0,1]}$ (Ví dụ 03.6) là lớp của bài, không có tham số, và giới hạn theo từng điểm của dãy trong một lớp con đếm được cố định không cho mọi hàm Borel (lớp Baire bị chặn); Định lý 03.17(a) được phát biểu "không dùng (M)" chính vì lớp này. | "Lớp hàm ngưỡng, lớp khoảng và lớp nửa không gian afin thỏa (M) với lớp con có tham số hữu tỉ (Nhận xét 03.14); lớp hữu hạn thỏa (M) với $\mathcal H_0=\mathcal H$." |
| nhẹ | L03-1-05, L03-5-00 (ghi chú diễn giả) | Thiếu điều kiện $d\ge1$ của Bổ đề 03.12(b); với $d=0$ biểu thức $(em/d)^d$ không xác định. | 1-05: "Trên $m\ge d$ điểm, lớp có chiều VC $d$ cho nhiều nhất $(em/d)^d$ cách gán nhãn."; 5-00: "… $(em/d)^d$ cách gán nhãn khi $d\le m$." Ghi chú: "Nếu $1\le d\le m$". | Viết "khi $1\le d\le m$". |
| nhẹ | L03-5-04 (Trực quan.), L03-7-02 (gạch đầu dòng 1) | Bất đẳng thức $\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$ thiếu điều kiện $1\le d\le2m$; 5-07 có điều kiện này. | 5-04: "$\ln K$ thành $\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$"; 7-02: "$\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$ thay cho $\ln\lvert\mathcal H\rvert$." Ghi chú §9 dòng 890 cũng viết không điều kiện (xem mục 4). | Thêm "($1\le d\le m$)" hoặc "khi $d\ge1$", như 5-07. |
| nhẹ | L03-6-07 (mặt trang) | "(a)" có hai nghĩa trên cùng trang: dòng 1 là Định lý 03.15(a), dòng 4 là Định lý 03.17(a). | "(6)⇒(1): Định lý 03.15(c) khi $d\ge1$; (a) với $\Pi_{\mathcal H}=1$ khi $d=0$." và "(4)⇒(6): phần (a), …". Ghi chú dòng 845: "Định lý 03.15(a) với $\Pi_{\mathcal H}=1$ khi $d=0$". | Dòng 1: "Định lý 03.15(a) với $\Pi_{\mathcal H}=1$ khi $d=0$". |
| nhẹ | L03-7-01 (bảng và ghi chú diễn giả) | Cột "Giả thiết không được bỏ" của Định lý 03.15 lệch danh sách của ghi chú §9; ghi chú diễn giả gọi chiều VC hữu hạn là giả thiết của Định lý 03.15. | Bảng: "(T1), (T5), (M)"; ghi chú diễn giả: "Ba giả thiết của Định lý 03.15 có phản ví dụ khi bỏ: (T5) …, (T1) …, chiều VC hữu hạn ở Ví dụ 03.6." Ghi chú §9: "Ba giả thiết sau không bỏ được: (T5), (T1), chiều VC hữu hạn"; (M) không có phản ví dụ; Định lý 03.15(a) đúng cả khi $d=\infty$, chỉ (b), (c) cần $1\le d$. | Bảng: "(T1), (T5); $d<\infty$ cho (b), (c)" và để (M) trong ghi chú diễn giả ("cần cho tính đo được"); ghi chú diễn giả: "Ba giả thiết không bỏ được (§9): …". |
| nhẹ | L03-5-07 (ghi chú diễn giả) | Dẫn sai bài của bất đẳng thức hợp. | "Kỹ thuật ghép ba công cụ: bất đẳng thức hợp của Bài 01, …". Ghi chú Bài 03, Kiến thức tiên quyết: "Từ Bài 02. … bất đẳng thức hợp (union bound; Bổ đề 02.12)"; 1-02 cũng dẫn Bổ đề 02.12. | "bất đẳng thức hợp (Bổ đề 02.12)". |
| nhẹ | L03-7-05 (ghi chú diễn giả) | Hai cỡ mẫu không ghi chiều VC; người đọc dễ hiểu là $d=1$ và $d=11$ như 7-02. | "tại $\epsilon=0{,}05$ được $589\,118$ và $1\,999\,657$". Tệp bài tập, Bài tập 03.4(a) Bước 2: "$589\,118$ với $d=3$ và $1\,999\,657$ với $d=11$". | "… được $589\,118$ ($d=3$) và $1\,999\,657$ ($d=11$)". |
| nhẹ | L03-5-05, L03-4-06 (mặt trang) | Kí hiệu rút gọn lệch ghi chú: bỏ đối số $h$ và chỉ số lớp. | 5-05: "$\sup_h\lvert L_D-L_S\rvert$", "$\sup_h\lvert L_{S'}-L_S\rvert$"; ghi chú dòng 591: "$\sup_h\lvert L_D(h)-L_S(h)\rvert$". 4-06: "$\Pi=14&lt;15$", "tổng nhị thức bằng $\Pi$"; ghi chú: $\Pi_{\mathcal H^2_{\mathrm{aff}}}(4)\le14$. | Viết $L_D(h)$, $L_S(h)$, $L_{S'}(h)$ nếu vừa dòng; 4-06: "$\Pi_{\mathcal H^2_{\mathrm{aff}}}(4)=14&lt;15$". |
| nhẹ | L03-2-07 (ghi chú diễn giả) | Lời giải cận dưới Bài tập 03.2(b) thiếu cách xử lý khoảng không dùng và cách toàn $0$ (khoảng đóng $u\le v$ luôn khác rỗng). | "mỗi khối $\{i,\ldots,i'\}$ được thực hiện bởi khoảng $[i,i']$." Tệp bài tập, Lời giải 03.2(b) Bước 2: "Khoảng không dùng đến được đặt là $[10,10]$, và cách toàn $0$ dùng hai khoảng $[10,10]$." | Thêm mệnh đề đó. |

## 4. Bảng thống nhất trang → khối ghi chú

Kí hiệu: ✓ khớp (kí hiệu, nhãn giả thiết, số hiệu, dữ liệu, thuật ngữ); ⚠ có phát hiện ở mục 3.

| Trang | Khối ghi chú | Trạng thái |
|---|---|---|
| 1-01 | đoạn mở đầu; Bổ đề 03.12; Định lý 03.15, 03.17 | ✓ |
| 1-02 | Kiến thức tiên quyết; Câu hỏi ôn nhanh; Định lý 02.14, Hệ quả 02.16 | ✓ (02.14 ghi "(T1)–(T3), $K$ hàm chọn trước" tương đương (T1)–(T4)) |
| 1-03 | Mục tiêu học tập 1–5 | ✓ |
| 1-04 | §4–§9 | ✓ |
| 1-05 | Câu hỏi trung tâm (đoạn mở đầu) | ⚠ ghi chú diễn giả thiếu $d\ge1$ |
| 1-06 | Câu hỏi mở đầu; khối ứng dụng §3 | ✓ |
| 2-00 | §1–§4 | ✓ |
| 2-01 | §1 (tám thành phần), §2 (T1), (T5), (M) | ⚠ ghi chú diễn giả "(M) cho mọi lớp" |
| 2-02 | Ví dụ 03.1, Định nghĩa 03.1, Ví dụ 03.2 | ✓ |
| 2-03 | Định nghĩa 03.2, 03.3 và các đoạn sau | ✓ |
| 2-04 | Nhận xét 03.4 | ✓ |
| 2-05 | Mệnh đề 03.5, 03.6 | ✓ |
| 2-06 | chứng minh Mệnh đề 03.5, 03.6 | ✓ |
| 2-07 | Bài tập 03.2(b), (c) | ⚠ ghi chú diễn giả thiếu cách toàn $0$ |
| 3-00 | §5 | ✓ |
| 3-01 | Định nghĩa 03.7 và hai đoạn sau | ✓ |
| 3-02 | Ví dụ 03.3, Bước 1–2; câu ôn nhanh 2 | ✓ |
| 3-03 | Bổ đề 03.8, chứng minh, Phụ lục A | ✓ |
| 3-04 | Mệnh đề 03.9 | ✓ |
| 3-05 | chứng minh Mệnh đề 03.9; Phụ lục A | ✓ |
| 3-06 | Ví dụ 03.3, Bước 3–4 | ✓ |
| 3-07 | Nhận xét 03.10; Bài tập 03.5(a) | ✓ |
| 4-00 | §6 | ✓ |
| 4-01 | Định nghĩa 03.11, đoạn sau, Ví dụ 03.4 | ✓ |
| 4-02 | Bổ đề 03.12; Ví dụ 03.5 (hình) | ⚠ ghi chú diễn giả "phần lớn bị thiếu" |
| 4-03 | chứng minh Bổ đề 03.12(a), Phụ lục B | ✓ |
| 4-04 | ví dụ dựng mới bằng kí hiệu ghi chú (Bước 1–2 chứng minh 03.12, Mệnh đề 03.6, Ví dụ 03.4) | ✓ không mâu thuẫn số nào của ghi chú ($\Pi_{\mathcal H_{\mathrm{int}}}(3)=7$) |
| 4-05 | chứng minh Bổ đề 03.12(b) | ✓ |
| 4-06 | Ví dụ 03.5 | ⚠ kí hiệu $\Pi$ rút gọn |
| 5-00 | §7 | ⚠ ghi chú diễn giả thiếu $d\ge1$ |
| 5-01 | Định nghĩa 03.13 và hai đoạn sau | ✓ |
| 5-02 | Ví dụ 03.6 | ✓ |
| 5-03 | đoạn trước Định lý 03.15, Nhận xét 03.14; Bài tập 03.4(d) | ⚠ ghi chú diễn giả "(M) cho mọi lớp" |
| 5-04 | Định lý 03.15 và đoạn sau | ⚠ Trực quan. thiếu điều kiện |
| 5-05 | chứng minh Định lý 03.15 (lộ trình) | ⚠ kí hiệu bỏ $(h)$ |
| 5-06 | Bước 1–2 chứng minh; Phụ lục C.2–C.3; Bài tập 03.4(c) | ✓ ("đối xứng hóa" có trong `thuat-ngu.md`, ghi chú không dùng từ này) |
| 5-07 | Bước 3–5 chứng minh; Phụ lục C.4, C.6 | ⚠ $\delta/\Pi_{\mathcal H}(2m)$; "Bài 01" |
| 5-08 | Ví dụ 03.7 | ✓ |
| 5-09 | Ví dụ 03.8 và đoạn sau; Bài tập 03.5(c) | ✓ |
| 6-00 | §8, §9 | ✓ |
| 6-01 | Hệ quả 03.16 và đoạn sau | ✓ |
| 6-02 | chứng minh Hệ quả 03.16 | ✓ |
| 6-03 | Ví dụ 03.9 | ✓ |
| 6-04 | Ví dụ 03.10; Bài tập 03.4(e) | ✓ |
| 6-05 | Định lý 03.17(a) và đoạn sau | ✓ |
| 6-06 | Định lý 03.17(b) | ✓ (giả thiết ERM đo được có trên mặt trang) |
| 6-07 | danh sách kéo theo; Hệ quả 03.18 | ⚠ "(a)" hai nghĩa |
| 6-08 | Định lý 03.19 và đoạn sau; §9 | ✓ |
| 7-00 | §9–§12 | ✓ |
| 7-01 | §4–§9 | ⚠ cột "không được bỏ" |
| 7-02 | đoạn mở đầu, Ví dụ 03.9, §9 | ⚠ thiếu điều kiện |
| 7-03 | Bài tập 03.1(a), (b) | ✓ |
| 7-04 | §11 và lời giải; §7; Nhận xét 03.4, 03.10; Ví dụ 03.8 | ✓ |
| 7-05 | §10; tệp bài tập | ⚠ thiếu $d$ cho hai cỡ mẫu |
| 7-06 | §11, §12 | ✓ (tiêu đề Bài 04 khớp tệp ghi chú Bài 04) |

Thứ tự khái niệm theo thứ tự mục của ghi chú: mạch 2 ↔ §1–§4, mạch 3 ↔ §5, mạch 4 ↔ §6, mạch 5 ↔ §7, mạch 6 ↔ §8–§9; đổi chỗ trong §5 ở 3-02 đã được điều phối viên chấp nhận.

## 5. Đề xuất sửa ghi chú

- **§9, dòng 890:** "$\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$" thiếu điều kiện $1\le d\le2m$ của Bổ đề 03.12(b) (đúng như Phụ lục C.6 đã viết "Nếu $1\le d\le m$ thì $d\le2m$"). Đề xuất: "… $\le d\ln(2em/d)$ khi $1\le d\le m$".
- **Ví dụ 03.5, Bước 7:** đồng ý đề xuất đã ghi ở `review-log.md` ("$3\le m\le5$" → "$3\le m\le9$"): dạng đóng $(em/3)^3$ lớn hơn $2^m$ đúng với $m=3,\ldots,9$ và nhỏ hơn từ $m=10$ ($743{,}9<1024$). Câu hiện tại đúng nhưng chưa đủ.

Không phát hiện lỗi toán học nào khác trong ghi chú ở các khối deck dùng; mọi hằng số của Định lý 03.15, Hệ quả 03.16 và Phụ lục C đã tính lại khớp.

## 6. Kết luận

Số phát hiện: 0 chặn bàn giao, 0 nghiêm trọng, 3 trung bình, 8 nhẹ. Mọi con số trên mặt trang, ghi chú diễn giả và SVG khớp; mọi phát biểu giữ đủ giả thiết, lượng từ, hằng số và loại bảo đảm của ghi chú; lộ trình mẫu bóng khớp ghi chú.

**Kết luận: đạt khi sửa.**
