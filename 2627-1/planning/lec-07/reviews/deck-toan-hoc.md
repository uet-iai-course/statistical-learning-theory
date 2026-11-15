# Duyệt deck Bài 07 — Vai 2 `toan-hoc` (độ chính xác toán học, thống nhất với ghi chú)

Bản duyệt: `2627-1/lecture-07-mang-no-ron-tham-so-hoa-thua.html` (đóng băng), `img/lec-07/ham-loi-doc.svg`. Đối chiếu: `materials/lec-07/lecture-note.md`, `exercises.md`, `storyboard.md` (V1–V23), `review-log.md` § Bộ trang chiếu; các khối được dẫn của Bài 02–04 (Hệ quả 02.10, Định lý 02.14, Định lý 03.15, Nhận xét 03.10, Mệnh đề 04.3). Chỉ đọc; không sửa deck, ghi chú, storyboard.

## 1. Tính lại độc lập

Hai tệp nháp trong `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-07/rv-toan-hoc/`: `nums.py` (V1–V23) và `exp.py` (thí nghiệm Phụ lục D, mười hạt giống, đúng thứ tự rút của giao thức).

**Thí nghiệm (Phụ lục D), kết quả chạy lại:** hạng $200$ ở cả mười lần; lỗi huấn luyện $0$; lỗi kiểm tra nhãn thật trung bình $0{,}02298$ (độ lệch chuẩn $0{,}0074$, từ $0{,}0140$ đến $0{,}0364$), nhãn hoán vị $0{,}50108$ (độ lệch chuẩn $0{,}0095$, từ $0{,}480$ đến $0{,}512$); $\lVert\hat w\rVert$ trung bình $915{,}67$ ($351{,}5$–$1720{,}8$) và $10\,852{,}6$ ($6791{,}5$–$14\,051{,}9$), tỉ số $11{,}852$ ($10\,853/916=11{,}848$); lề nhỏ nhất $1$; $C_x$ từ $1{,}5176$ đến $1{,}5440$; lề chuẩn hóa $3{,}80\cdot10^{-4}$–$1{,}875\cdot10^{-3}$ và $4{,}64\cdot10^{-5}$–$9{,}64\cdot10^{-5}$; số hạng $2\lVert\hat w\rVert C_x/(\gamma\sqrt{200})$ từ $75{,}43$ đến $371{,}74$ và từ $1467{,}1$ đến $3046{,}7$; chuẩn của $\Theta_2$ trung bình $20{,}47$ và $242{,}67$. Mọi số của 1-06, 6-03, 6-04, 7-03 (0,023/0,501, 0,014–0,036, 0,480–0,512, 916/10 853, 351–1721, 6792–14 052, $C_x$ 1,518–1,544, 75–372, 1467–3047, 11,85, 20,5/242,7, hai khoảng chuẩn không giao nhau) khớp ghi chú và lần chạy lại.

**V1–V23:** khớp toàn bộ.

| Mã | Giá trị tính lại | Trang |
|---|---|---|
| V2 | $1{,}5$; $\sqrt3=1{,}7321$; $\sqrt{\ln40/400}=0{,}096032\le0{,}0961$ | 1-02 (ghi chú diễn giả) |
| V3 | vét lưới $61^3$ tham số afin: lỗi ít nhất $1$ điểm; $-\tfrac12,\tfrac12,\tfrac12,\tfrac32$ | 2-02 |
| V4 | $f_\theta=-\tfrac12,\tfrac12,\tfrac12,-\tfrac12$; $f_\theta(\tfrac12,\tfrac12)=\tfrac12$; $9$ tham số | 2-03, 2-04, 2-05 |
| V5 | $F(\theta)=F(\theta_{\mathrm{swap}})=0$; $f_{\theta_{\mathrm{mid}}}=-\tfrac12,-1,-1,-2$; hiệu $0,-\tfrac32,-\tfrac32,-\tfrac32$; $F(\theta_{\mathrm{mid}})=27/16$ | 2-07 |
| V6 | $10{,}25$; $500{,}30$ ($c=10$ và $0{,}1$); $3{,}2016$; $22{,}3674$; $\lVert\Theta_1\rVert_{\mathrm{op}}=2$, $\lVert\Theta_2\rVert=\sqrt5$, tích $4{,}4721$ | 2-10 |
| V7 | $\sqrt{8\ln2}=2{,}3548$ | 2-11 |
| V8 | tổng $0,6,8,12$; $\widehat{\mathfrak R}=0,\tfrac14,\tfrac13,\tfrac12$ (liệt kê đủ 8 bộ dấu) | 3-02 |
| V9 | bảng $h_a$, $h_{a'}$, nhỏ nhất theo 8 giá trị $\tau$ khớp từng ô; tổng $6$; $\tfrac14$ | 3-06 |
| V11 | $0{,}288097$; $0{,}081486\to0{,}0815$; $0{,}040743\to0{,}0408$; $1{,}2881$ | 4-04, 7-05 |
| V12 | $0{,}2881$; $\sqrt{\ln20/400}=0{,}086541\le0{,}0866$; tỉ số $3{,}329$ | 4-05 |
| V13 | $B/2$; $\sqrt2/2=0{,}7071$; $B/\sqrt m$ với $m=4$ | 5-02 |
| V14 | $\tfrac13\mathbb E\lvert\sigma_1+\sigma_2+\sigma_3\rvert=0{,}5$ | 5-03 |
| V15 | lề $\tfrac12$ tại bốn quan sát | 5-04 (ghi chú diễn giả) |
| V16 | $0{,}2$; $0{,}2408$; $\sqrt{16\ln2}=3{,}3302$; $3\sqrt{\ln40/2}=4{,}074305$; $57\,957{,}21\to57\,958$; $231\,828{,}86\to231\,829$; $3689{,}72\to3690$ | 6-01 |
| V17 | $3\sqrt{\ln80/5000}=0{,}088812\le0{,}0889$; $0{,}2889$ | 6-02, 7-06 (ghi chú diễn giả) |
| V18 | $11{,}848$; $20{,}48$; $242{,}68$; $\sqrt{\ln40/10^4}=0{,}019206\le0{,}0193$ | 6-03, 6-04 |
| V19 | $10^{-6}\cdot1/100=10^{-8}$ | 6-05 |
| V20 | $\ln80=4{,}382027$; $0{,}2530+0{,}5617$; $0{,}08+0{,}17762=0{,}25762\le0{,}2577$; $0{,}0253+0{,}0562$; $25{,}7625$; $66\,371$ | 6-05 (ghi chú diễn giả) |
| V21 | $0{,}16$; $0{,}0815$; $0{,}2815$; $2\cdot0{,}04/0{,}5=0{,}16$; $\widehat{\mathfrak R}_S(\mathcal F_2)\le2/50=0{,}04$ | 7-06 |
| V22 | $\sqrt{\ln120/400}=0{,}109402\le0{,}1095$; $\ln120=4{,}7875$; $\sqrt{\ln60/400}=0{,}10117\le0{,}1012$; $5000$; $0{,}005$ | 7-04, 7-05 |
| V23 | không có số; lập luận $(w',0)$ và phép chiếu đúng | 5-07 |
| UML | $4\sqrt{2\ln80/10^4}=0{,}11842\le0{,}1185$ | 7-08 (ghi chú diễn giả) |

**Các phép suy khác đã kiểm:** $\rho_m\ge\sqrt{8\ln2}$ từ $\Pi(2m)\ge2^m$ và $4/\delta>1$; $\Pi(2m)=2^{2m}$ cho $\rho_m\ge\sqrt{16\ln2}$ (6-01); bất biến của Hệ quả 07.16 dưới $(w,\gamma,B)\mapsto(cw,c\gamma,cB)$: $\phi_{c\gamma}(c t)=\phi_\gamma(t)$, $\mathbb 1[ct<c\gamma]=\mathbb 1[t<\gamma]$, số hạng phạt không đổi (5-05); cận logistic sau khi chia cho $K$: $2(1/K)BC_x/\sqrt m$ nhân lại $K$ cho $2BC_x/\sqrt m+3K\sqrt{\cdot}$ (6-05); dạng $C_xR_\Theta\ln\bar N/(\gamma\sqrt m)$ ở 6-06 trội hơn số hạng $\lVert X\rVert_2R_\Theta\ln\bar N/(\gamma m)$ của ghi chú khi $\lVert x_i\rVert\le C_x$, nên bản trên trang là hệ quả đúng của Nhận xét 07.18; $\lVert\chi(x)\rVert\le C_x$ từ $\lvert\operatorname{ReLU}(\langle v_j,x\rangle+b_{1j})\rvert\le1+\lvert b_{1j}\rvert$ (6-03); bộ ba hàm của Nhận xét 03.10(iii) và $r_m=\sqrt{\ln(2K/\delta)/(2m)}$ với $K=3$ của Định lý 02.14(a) (7-05); $q_k=1/(k(k+1))$ có tổng $1$, $\ln(2/(\delta q_1))=\ln80$ (6-02).

**SVG F2 (`ham-loi-doc.svg`):** trục $t$ từ $-\gamma$ ($x=70$) đến $2\gamma$ ($x=570$), $166{,}67$ px mỗi $\gamma$: $0\mapsto236{,}7$, $\gamma\mapsto403{,}3$ đúng; trục tung $0\mapsto320$, $1\mapsto80$ đúng. Hàm dốc đi qua $(-\gamma,1)$, $(0,1)$, $(\gamma,0)$, $(2\gamma,0)$, đúng $\phi_\gamma$. $\mathbb 1[t<\gamma]$: chấm rỗng tại $(\gamma,1)$, chấm đặc tại $(\gamma,0)$; $\mathbb 1[t\le0]$: chấm đặc tại $(0,1)$, chấm rỗng tại $(0,0)$; đúng quy ước mút. Hai đường bậc thang lệch $\pm5$ px để không chồng lên hàm dốc; thứ tự kẹp $\mathbb 1[t\le0]\le\phi_\gamma\le\mathbb 1[t<\gamma]$ thấy được. Nhãn "0–1" cho $\mathbb 1[t\le0]$ theo cách gọi của ghi chú (đoạn sau Định nghĩa 07.15). Đạt.

## 2. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L07-3-02 | "Diễn giải:" nêu một quy luật tổng quát không có trong ghi chú và sai: số véc-tơ không quyết định độ phức tạp. Bổ đề 07.8 trên cùng trang cho phản ví dụ: $0{,}1\cdot\{0,1\}^3$ có $8$ véc-tơ và $\widehat{\mathfrak R}=0{,}05<\tfrac14$ của lớp hai véc-tơ. | Deck: "càng nhiều véc-tơ, càng hợp được nhiều bộ dấu." Ghi chú, Ví dụ 07.4: "Tóm lại, bốn lớp tạo ra $1$, $2$, $4$, $8$ véc-tơ trên ba điểm và có độ phức tạp lần lượt $0$, $\tfrac14$, $\tfrac13$, $\tfrac12$." | "**Diễn giải:** trên bốn lớp này, $1$, $2$, $4$, $8$ véc-tơ cho độ phức tạp $0$, $\tfrac14$, $\tfrac13$, $\tfrac12$." (số có trên trang). |
| trung bình | L07-7-04, L07-7-05 | Định lý 02.14(a), (T4) (và (T2) trong ghi chú diễn giả) xuất hiện trên mặt trang mà chưa có trang nào nhắc lại; 1-02 chỉ nhắc Định lý 03.15, 03.9, 04.3, 02.7, 02.10. Người học không có công thức $r_m$ của lớp hữu hạn để kiểm $\sqrt{\ln(2\cdot3/\delta)/(2m)}$. | 7-04: "tính $r_m$ của Định lý 02.14(a)"; 7-05: "(T4) lớp hữu hạn; $r_m=\sqrt{\ln(2\cdot3/\delta)/(2m)}$". Định lý 02.14: (T1), $\ell$ thỏa (T2), (T3), $\mathcal H$ thỏa (T4); $r_m=\sqrt{\ln(2K/\delta)/(2m)}$, với xác suất ít nhất $1-\delta$, $\sup_h\lvert L_S-L_D\rvert\le r_m$. Quy định "Define or recall before use". | Thêm trên 7-04 một dòng "**Nhắc lại:** Định lý 02.14(a): (T1), hàm lỗi trong $[0,1]$, lớp hữu hạn chọn trước (T4); với xác suất ít nhất $1-\delta$, $\sup_h\lvert L_S(h)-L_D(h)\rvert\le\sqrt{\ln(2\lvert\mathcal H\rvert/\delta)/(2m)}$." (dùng $\lvert\mathcal H\rvert$, tránh $K$ hai nghĩa theo quyết định 11.12), hoặc thêm vào 1-02. |
| trung bình | L07-7-06 (câu 3) | Câu hỏi bỏ hai điều kiện mà lời giải cần: quan sát độc lập cùng phân bố, và $B$, $\gamma$ chọn trước khi lấy mẫu. Không có điều kiện thứ hai, đáp số là $0{,}2889$ (lưới), không phải $0{,}2815$; ghi chú diễn giả nêu cả hai đáp số nên câu hỏi chưa xác định. | Deck: "$m=2500$, $\lVert x\rVert\le1$, $B=2$, $\gamma=0{,}5$, $\delta=0{,}05$, $L^{<\gamma}_S(h_w)=0{,}04$: tính cận của Hệ quả 07.16." Ghi chú §12: "$m=2500$ quan sát độc lập cùng phân bố … Lớp $\mathcal F_B$ với $B=2$ và lề $\gamma=0{,}5$ được chọn trước khi lấy mẫu." | "$m=2500$ quan sát theo (T1), $\lVert x\rVert\le1$, $B=2$, $\gamma=0{,}5$ chọn trước khi lấy mẫu, $\delta=0{,}05$, $L^{<\gamma}_S(h_w)=0{,}04$: tính cận của Hệ quả 07.16." |
| nhẹ | L07-1-05, L07-3-00 (ghi chú diễn giả) | Đồng nhất thức của Mệnh đề 07.9(a) thiếu kì vọng theo $\tau$. 1-05 còn gọi riêng $2BC_x/(\gamma\sqrt m)$ là "số hạng phạt", trong khi ghi chú gọi số hạng phạt là tổng hai số hạng (phụ thuộc $m$, $\delta$, $BC_x/\gamma$; Ví dụ 07.8 Bước 4). | 1-05: "Độ phức tạp Rademacher bằng một nửa trừ lỗi nhỏ nhất khi khớp nhãn ngẫu nhiên"; "số hạng phạt là $2BC_x/(\gamma\sqrt m)$". 3-00: "nó bằng một nửa trừ lỗi nhỏ nhất". Mệnh đề 07.9(a): $\tfrac12-\mathbb E_\tau\min_h\operatorname{err}_\tau(h)$. | "bằng một nửa trừ kì vọng của lỗi nhỏ nhất khi khớp nhãn ngẫu nhiên"; "số hạng Rademacher là $2BC_x/(\gamma\sqrt m)$". |
| nhẹ | L07-1-01, L07-7-03 | Định lý 07.11 dùng độ phức tạp Rademacher thực nghiệm của **lớp hàm lỗi**; "lớp chứa mô hình" là lớp giả thuyết (điểm số). Hai lớp bằng nhau với hàm lỗi 0–1 (Mệnh đề 07.9(b)) và nối nhau qua bổ đề co với hàm lỗi dốc, nhưng không đồng nhất. Trang tổng quan được miễn kí hiệu, không miễn độ chính xác. | 1-01: "độ phức tạp Rademacher của lớp chứa mô hình do huấn luyện chọn chặn khoảng cách tổng quát hóa"; 7-03: "Độ phức tạp Rademacher của lớp chứa mô hình được chọn." Định lý 07.11: "Lớp hàm lỗi. $\mathcal G$ … thỏa (T3), (T5), (M)". | 7-03: "Độ phức tạp Rademacher thực nghiệm của lớp hàm lỗi trên lớp chứa mô hình được chọn." 1-01 có thể giữ nếu điều phối viên coi là lời tổng quan. |
| nhẹ | L07-4-03 | Bước 4 không ghi (T1), dù ghi chú đánh dấu (T1) vào bước này (bất đẳng thức McDiarmid cần các quan sát độc lập); ghi chú diễn giả cũng không nêu. | Deck bước 4: "(Bổ đề 07.10 hai lần, mỗi lần $\delta/2$; bất đẳng thức hợp)". Ghi chú, chứng minh Định lý 07.11: "**Bước 4 (hai lần bất đẳng thức McDiarmid; (T1) cho tính độc lập).**" Bài tập 07.4(d) lời giải cũng nêu Bước 4 dùng (T1). | "((T1); Bổ đề 07.10 hai lần, mỗi lần $\delta/2$; bất đẳng thức hợp)". |
| nhẹ | L07-2-07 | Trên mặt trang, $\theta$ chưa được nói là tham số của Mệnh đề 07.2, và "$F(\theta)=0$" là kết quả của phần (a), chưa có trên trang. | Deck: "kiến trúc của Mệnh đề 07.2 … $\theta_{\mathrm{swap}}$ đổi chỗ hai nơ-ron ẩn của $\theta$"; "$F(\theta_{\mathrm{swap}})=F(\theta)=0$". Bài tập 07.5(c): "từ $\theta$ của Mệnh đề 07.2"; (a): "$F(\theta)=0$ tại tham số $\theta$ của Mệnh đề 07.2". | "… $\theta$ là tham số của Mệnh đề 07.2, $F(\theta)=0$ (phần (a))." |
| nhẹ | L07-3-02 | "Giả thiết: $A$ như trên" nhập nhằng: trên trang, $A$ là bốn tập cụ thể trong $\mathbb R^3$, còn Bổ đề 07.8 phát biểu cho mọi $A\subset\mathbb R^m$ khác rỗng, bị chặn. | Deck: "**Bổ đề 07.8.** **Giả thiết:** $A$ như trên, $c\in\mathbb R$, $\bar a\in\mathbb R^m$." Ghi chú: "**Tập.** $A\subset\mathbb R^m$ khác rỗng, bị chặn." | "**Giả thiết:** $A\subset\mathbb R^m$ khác rỗng, bị chặn; $c\in\mathbb R$, $\bar a\in\mathbb R^m$." |
| nhẹ | L07-5-04, L07-6-02, L07-2-03 | Ba điều kiện nhỏ của định nghĩa bị rút khỏi mặt trang: $\gamma>0$ (Định nghĩa 07.15); chỉ số lưới $k=1,2,\ldots$ (Nhận xét 07.17, cần để $\sum_kq_k=1$); độ rộng $N$ chỉ định nghĩa khi $J\ge2$ (Định nghĩa 07.1). | Ghi chú: "Cho hàm điểm số $f$, …, và $\gamma>0$"; "lưới $\gamma_k=2^{-k}$, $k=1,2,\ldots$"; "khi $J\ge2$, $N=\max_{1\le j\le J-1}N_j$". | Thêm "$\gamma>0$" vào 5-04; "$k\ge1$" vào 6-02; "($J\ge2$)" sau $N$ ở 2-03. |
| nhẹ | L07-2-11 (ghi chú diễn giả) | Nhận xét 07.6 bỏ "kể cả hệ số tự do" khi đếm $P$ trọng số. | Ghi chú: "với $P$ trọng số được huấn luyện (kể cả hệ số tự do)". Deck: "với kích hoạt dấu và $P$ trọng số". | "với kích hoạt dấu và $P$ trọng số được huấn luyện, kể cả hệ số tự do". |
| nhẹ | L07-6-04 | "lỗi $0{,}023$" là trung bình mười lần chạy, còn khoảng tin cậy của Hệ quả 02.10(b) là của từng lần chạy (một hàm cố định trên một tập kiểm tra). Ghép hai số trên một dòng dễ đọc thành khoảng tin cậy cho trung bình. | Ghi chú, câu hỏi mở đầu: "Lỗi kiểm tra trung bình"; Ví dụ 07.10 (ii): "hàm đã chọn … độc lập với $5000$ điểm kiểm tra, nên Hệ quả 02.10(b) cho khoảng tin cậy mức $0{,}95$ với bán kính …". | "lỗi trung bình $0{,}023$; mỗi lần chạy, Hệ quả 02.10(b): bán kính $0{,}0193$, mức $0{,}95$." |
| nhẹ | L07-6-01 | Điều kiện đủ viết với hằng số làm tròn xuống $4{,}0743<3\sqrt{\ln40/2}=4{,}074305$; bảng đúng vì được tính với hằng số đúng (hằng số làm tròn lên $4{,}0744$ cho $231\,831$ ở cột giữa). Giống ghi chú. | Deck: "Số hạng phạt $\le\epsilon$ khi $m\ge\big((2BC_x/\gamma+4{,}0743)/\epsilon\big)^2$". Ghi chú, Ví dụ 07.8 Bước 4, cùng công thức. | Viết hằng số dạng $3\sqrt{\ln40/2}$ trong công thức (giữ $\approx4{,}0743$ ở ghi chú diễn giả). |

Không có phát hiện `chặn bàn giao` hay `nghiêm trọng`. Kiểm riêng các điểm của bản giao việc:

- **Hàm lỗi bị chặn/Lipschitz:** (T3) "hàm lỗi trong $[0,1]$" đúng ở 2-01, 4-02, 7-01, 7-03; hàm lỗi dốc $[0,1]$ và $(1/\gamma)$-Lipschitz (5-04, 5-06); 6-05 tách đúng hàm lỗi bản lề, logistic (không bị chặn trên $\mathbb R^p$) và chia cho $K$; không chỗ nào chuyển kết quả hàm lỗi bị chặn sang hàm lỗi không bị chặn.
- **Chuẩn:** chuẩn Euclid của quả cầu (5-01, 7-02); Frobenius và chuẩn phổ đúng tên (2-10); chuẩn của $w$ so với chuẩn của $\Theta_2$ đúng thừa số $\sqrt N$ (6-03 ghi chú diễn giả); $\lVert\cdot\rVert_{2,1}$ đúng định nghĩa (6-06 ghi chú diễn giả).
- **Lề:** $\tilde yf(x)$, tỉ lệ vi phạm lề với "$<\gamma$", lề chuẩn hóa $\gamma/(\lVert\hat w\rVert C_x)$, lề nhiều lớp với "$\le\gamma$" ở Nhận xét 07.18, đúng ghi chú.
- **Xác suất cao/kì vọng:** Định lý 07.11(a) theo kì vọng với $\mathfrak R_m$, (b) với xác suất ít nhất $1-\delta$ với $\widehat{\mathfrak R}_S$, đồng thời cho mọi $g$ (4-02, 7-01); Mệnh đề 07.9, 07.13, Bổ đề 07.8, 07.14 ghi "tất định", kì vọng chỉ theo $\sigma$ hay $\tau$; Hệ quả 07.16, Nhận xét 07.17, 07.18 "với xác suất ít nhất $1-\delta$, đồng thời cho mọi …".
- **Thực nghiệm so với kì vọng:** 4-03 đặt đúng $\mathbb E\Psi\le2\mathfrak R_m$ rồi đuôi dưới cho $\widehat{\mathfrak R}_S$; 3-01 định nghĩa cả hai; Hệ quả 07.16 dùng $\widehat{\mathfrak R}_S$ (5-06 bước 2).
- **Hằng số 2, 3:** $2$ từ hai cận trên đúng ở bước 2 (đối xứng hóa); $3=1+2$ từ hai lần McDiarmid, mỗi lần $\delta/2$ (4-03, 7-06 câu 2); hằng số $2$ trong số mũ McDiarmid từ độ dài đoạn $c_k$ (4-01 ghi chú diễn giả). Đúng.
- **(T1):** có ở 2-01, 4-03 (bước 1, 2), 5-05, 6-06, 7-01, 7-02, 7-03; nhãn hoán vị vi phạm (T1) đúng lí do (4-04, 6-04). Chỉ thiếu ở bước 4 của 4-03 và câu 3 của 7-06 (xem bảng).
- **"Ngoài thừa số lôgarit":** 6-06 giữ $\ln\bar N$ tường minh, $\tilde O$, và câu "Ngoài thừa số lôgarit, cận không phụ thuộc số tham số" (ghi chú thêm "hay số nhãn"; bản deck yếu hơn, không sai). Quyết định N2 của cổng duyệt đã được áp dụng.
- **Phản ví dụ:** 2-07 (hàm mục tiêu không lồi, $27/16$), 6-05 (lớp điểm số $B=10^{-6}$), 5-03 (định tâm, $0\to0{,}5$), 4-04 (nhãn hoán vị), 7-05 (lớp một tham số, cận $1{,}2881$; lớp $10^6$ tham số, $0{,}1095$): đúng.

## 3. Bảng thống nhất trang → khối ghi chú

`=` khớp; `≈` khớp, rút gọn không bỏ điều kiện; `lệch` xem bảng phát hiện.

| Trang | Khối ghi chú / bài tập | Kí hiệu, nhãn giả thiết, số hiệu | Dữ liệu, kết quả | Ghi chú |
|---|---|---|---|---|
| 1-01 | Đoạn mở đầu, §10 | ≈ | — | lệch nhẹ: "lớp chứa mô hình" |
| 1-02 | Kiến thức tiên quyết; Định lý 03.15, Mệnh đề 03.9, 04.3; câu ôn nhanh | = (04.3 bỏ (T2), (T3) trong dòng nhắc) | = | — |
| 1-03 | Mục tiêu học tập | = | — | — |
| 1-04 | §4–§13 | — | — | — |
| 1-05 | Câu hỏi trung tâm | = | = | lệch nhẹ ghi chú diễn giả (kì vọng; "số hạng phạt") |
| 1-06 | Câu hỏi mở đầu, Phụ lục D | = | = (chạy lại) | — |
| 2-01 | §1, §2 | = (T1), (T3), (T5), (M) | — | — |
| 2-02 | Ví dụ 07.1; khối ứng dụng | = | = | — |
| 2-03 | Định nghĩa 07.1 | ≈ | = ($9$) | nhẹ: $J\ge2$ |
| 2-04 | Mệnh đề 07.2 | = | = | — |
| 2-05 | Chứng minh Mệnh đề 07.2; đoạn sau | = | = | — |
| 2-06 | Nhận xét 07.3; ba năng lực (Mệnh đề 04.3) | = | — | — |
| 2-07 | Bài tập 07.5(c) | = | = ($27/16$) | nhẹ: $\theta$ của Mệnh đề 07.2 |
| 2-08 | Định nghĩa 07.4; Nhận xét 03.10 | = | = | — |
| 2-09 | Định nghĩa 07.5 và đoạn sau | = | — | — |
| 2-10 | Ví dụ 07.2 | = | = | — |
| 2-11 | Ví dụ 07.3; Nhận xét 07.6 | = | = | nhẹ ghi chú diễn giả |
| 3-01 | Định nghĩa 07.7 và ba đoạn sau | ≈ | = | — |
| 3-02 | Ví dụ 07.4; Bổ đề 07.8 | ≈ | = | trung bình: "Diễn giải:"; nhẹ: "$A$ như trên" |
| 3-03 | Mệnh đề 07.9 | = | — | — |
| 3-04 | Chứng minh Mệnh đề 07.9 | = | = | — |
| 3-05 | Ví dụ 07.5 | = | = | — |
| 3-06 | Bài tập 07.2(c) (phần cuối) | = | = (bảng 8 cột) | — |
| 4-01 | Bổ đề 07.10; Phụ lục A | = | — | — |
| 4-02 | Định lý 07.11 | = | — | — |
| 4-03 | Chứng minh Định lý 07.11; Phụ lục C | ≈ | = | nhẹ: (T1) ở bước 4 |
| 4-04 | Ví dụ 07.6; Nhận xét 07.12 | = | = | — |
| 4-05 | Bài tập 07.2(b) | = | = | — |
| 5-01 | §8 mở; Mệnh đề 07.13 | = | — | — |
| 5-02 | Chứng minh Mệnh đề 07.13; Ví dụ 07.7 | = | = | — |
| 5-03 | Bổ đề 07.14 và hai đoạn sau | = | = ($0{,}5$) | — |
| 5-04 | Định nghĩa 07.15, (i)–(iii); SVG F2 | ≈ | = | nhẹ: $\gamma>0$ |
| 5-05 | Hệ quả 07.16 | = | — | — |
| 5-06 | Chứng minh Hệ quả 07.16 | = | — | — |
| 5-07 | Bài tập 07.3(d) | = | = | — |
| 6-01 | Ví dụ 07.8 | = | = | nhẹ: hằng số $4{,}0743$ (như ghi chú) |
| 6-02 | Nhận xét 07.17; câu hỏi cuối buổi (b) | ≈ | = | nhẹ: $k\ge1$ |
| 6-03 | Ví dụ 07.10 Bước 1–2; đoạn sau Định nghĩa 07.15 | = | = (chạy lại) | — |
| 6-04 | Ví dụ 07.10 Bước 3–4; §10 | = | = | nhẹ: trung bình so với từng lần chạy |
| 6-05 | Ví dụ 07.11; Ví dụ 07.9 (ghi chú diễn giả) | = | = | — |
| 6-06 | Nhận xét 07.18 | ≈ (dạng $C_x/\sqrt m$ suy đúng từ $\lVert X\rVert_2/m$) | — | — |
| 7-01 | Mệnh đề 07.2, 07.9, Định lý 07.11 | = | = | — |
| 7-02 | Mệnh đề 07.13, Hệ quả 07.16 | = | = | — |
| 7-03 | §10 | ≈ | = ($11{,}85$) | nhẹ: "lớp chứa mô hình" |
| 7-04 | Bài tập 07.4(b), (c) | = | — | trung bình: Định lý 02.14, (T4) chưa nhắc lại |
| 7-05 | Lời giải Bài tập 07.4(b), (c) | = | = | như trên |
| 7-06 | Mệnh đề 07.9(b), Định lý 07.11, Ví dụ 07.11, §12 | = | = | trung bình: câu 3 thiếu điều kiện |
| 7-07 | §11; `exercises.md` | = (9 bài) | — | — |
| 7-08 | §13; quan hệ với UML | = | = ($0{,}1185$, $0{,}0408$) | — |

## 4. Đề xuất sửa ghi chú

- **Ví dụ 07.8, Bước 4 (nhẹ).** Điều kiện đủ $m\ge\big((2BC_x/\gamma+4{,}0743)/\epsilon\big)^2$ dùng hằng số làm tròn xuống ($3\sqrt{\ln40/2}=4{,}074305$). Các cỡ mẫu $57\,958$, $231\,829$, $3690$ đúng với hằng số đúng. Đề xuất viết $3\sqrt{\ln40/2}$ trong công thức, hoặc "$4{,}0744$" kèm cỡ mẫu tính lại ($57\,958$; $231\,831$; $3690$).
- **Kiến thức tiên quyết (nhắc lại từ cổng duyệt).** Bài tập 07.4(b) dùng Định lý 02.14 và (T4), chưa có trong danh sách tiên quyết; deck kéo theo lỗ hổng ở 7-04.

## 5. Kết luận

**Đạt khi sửa.** Không có phát hiện chặn bàn giao hay nghiêm trọng; 3 trung bình, 9 nhẹ. Mọi con số trên mặt trang, ghi chú diễn giả và SVG khớp ghi chú, `exercises.md` và thí nghiệm chạy lại.
