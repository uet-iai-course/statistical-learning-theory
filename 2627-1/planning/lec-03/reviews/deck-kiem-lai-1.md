# Kiểm lại sau biên tập — deck Bài 03, lượt 1 (2026-11-15)

Vai: kiểm lại sau biên tập (chỉ đọc). Deck: `2627-1/lecture-03-chieu-vc.html` (55 trang, mã trang không đổi), hình `2627-1/img/lec-03/`. Bản đóng băng trước sửa: `scratchpad/lec-03/master/frozen/`. Đối chiếu: năm báo cáo `reviews/deck-*.md`, quyết định của điều phối viên trong `review-log.md` ("Năm báo cáo duyệt và quyết định của điều phối viên"), bảng sửa `storyboard.md` mục 17, ghi chú `materials/lec-03/lecture-note.md`, `exercises.md`. `no-ai-slop` chế độ Detect trên văn bản mới hoặc đã sửa.

Diff theo trang: 49/55 trang đổi (không đổi: 2-06, 3-01, 3-07, 4-04, 5-02, 7-03); hai SVG đổi (`so-cach-gan-nhan.svg`: nhãn và `desc`; `dinh-ly-co-ban.svg`: viewBox 620×370, chữ nút 20 px, "mọi thuật toán ERM"). Vì gần như mọi trang đổi, mạch truyện được đọc lại trên toàn deck.

## 1. Kiểm tra máy (đã chạy)

| Kiểm tra | Kết quả |
|---|---|
| `deck_lint.py` | 0 phát hiện / 55 trang |
| `footer_check.py` (1600×900) | 0 trang chạm chân trang |
| `deck_check.py --shots` | console 0, page errors 0, failed 0, `.katex-error` 0; OVERFLOW ở 1-02, 5-01, 5-04, 5-09, 6-04, 7-02, cả sáu trang có `\sqrt` (báo động giả đã biết); SYLL ở 1-01 (bìa, miễn), 7-01 (68 ≤ 80); LINE20 ở 1-01 (bìa) và 6-08 (27, xem phát hiện N12) |
| Điều hướng (Playwright) | `#/2`…`#/7` mở đúng 2-00…7-00; bấm liên kết "Nội dung" `#/5` → 5-00; ↓, Space, → đúng; Esc mở overview; không page error |
| Ảnh | 1600×900 cả 55 trang (bảng ghép `recheck/sheet-wide-wide-01…07.png`) và 390×844 cả ảnh `-end` của 20 trang cuộn (`recheck/sheet-nend-narrow-01…02.png`), đã xem: không chồng lấn, không tràn trang; công thức then chốt 5-05 và bảng 5-08 cuộn ngang tại chỗ ở 390 px (đúng quy định) |

## 2. Các phát hiện được chấp nhận → trạng thái

### 2.1. Các điểm điều phối viên nêu riêng

| Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|
| CG1 (nghiêm trọng) 3-04 "Trực quan." gợi $d$ = số tham số | đã sửa | Mặt trang: "Tại $p+1$ đỉnh của đơn hình (simplex), ma trận các hàng $(x_i^\top,1)$ khả nghịch: $g=\langle w,x\rangle+b$ có dấu tùy ý." Ma trận $(p+1)\times(p+1)$ khả nghịch khi và chỉ khi các đỉnh độc lập afin (đúng). Ghi chú diễn giả: "Đẳng thức $d=p+1$ là kết quả riêng của lớp này, không suy ra từ số tham số (Nhận xét 03.10)." |
| TH2/CG6/SP1 (nghiêm trọng) 4-02 "Từ $m>d$, phần lớn các cách gán nhãn bị thiếu" | đã sửa | Câu đã xóa; ghi chú diễn giả mới chỉ dùng số đúng ($1351$ trong $2^{20}=1\,048\,576$). |
| TH1/CG10 5-07 $\delta/\Pi_{\mathcal H}(2m)$ | đã sửa | "ở đây $\delta/(2\Pi_{\mathcal H}(2m))$ mỗi cách"; kiểm: $4\Pi e^{-m\epsilon^2/8}=\delta\Rightarrow2e^{-m\epsilon^2/8}=\delta/(2\Pi)$. Ghi chú diễn giả nêu thừa số $2$ từ bước mẫu bóng. |
| TH3/TH7/CG2/SP14 (M) "không bỏ được"; "các lớp của bài thỏa (M)" | đã sửa | 5-00 ghi chú diễn giả: "(T1), lớp chọn trước (T5) và chiều VC hữu hạn không bỏ được, còn (M) bảo đảm độ lệch đều đo được"; 7-01 cột giả thiết "(T1), (T5), $d<\infty$", ghi chú "(M) cần cho tính đo được, không có phản ví dụ trong bài"; 2-01 ghi chú nêu đúng ba lớp và lớp hữu hạn (Nhận xét 03.14); 5-03 không còn câu về (M). Không còn chuỗi "các lớp của bài" trong deck. |
| CG8 6-08 cận khả diễn | đã sửa | Bỏ "(đọc thêm)" khỏi mặt trang; "Ý nghĩa:" chỉ nói trường hợp bất khả diễn; ghi chú diễn giả dẫn UML Định lý 6.8, §28.3 với cận $(d\ln(1/\epsilon)+\ln(1/\delta))/\epsilon$. Còn hai chỗ ghi chú diễn giả nói "$1/\epsilon^2$ không bỏ được" không kèm "bất khả diễn" (N11). |
| CG4 5-03, 7-04 trở ngại (i)/(ii) | đã sửa | 5-03: "Mẫu bóng … $L_{S'}(h)$ thay $L_D(h)$: sửa (i); dấu ngẫu nhiên khi biết $(S,S')$: sửa (ii)." 7-04 ghi chú câu 2 tương tự; khớp ghi chú §7 và Bước 3. Thuật ngữ mới ở 5-03 dùng trước định nghĩa (N1). |
| HV3, HV4 $\sigma_i$ và bước tam giác | đã sửa | 5-05 bước 2: "$\Pr(\sigma_i=\pm1)=\tfrac12$, độc lập"; 5-06: "$\lvert L_S-L_D\rvert>\epsilon$, $\lvert L_{S'}-L_D\rvert\le\tfrac\epsilon2\Rightarrow\lvert L_{S'}-L_S\rvert>\tfrac\epsilon2$" (bất đẳng thức tam giác, đúng). |
| Lỗi lặp từ deck 02 | đã sửa | Không còn "ERM:", "PAC:" làm nhãn (lint ABBRLABEL 0); không còn câu quy trình ở 1-03, 1-04, 4-05, 7-00, 7-05; "Nhắc lại:" có cho học PAC (1-02), (O1)/(O2) (6-01), đảo cận đuôi (5-05), chia $\delta/K$ (5-07), bước tất định (6-02); khả diễn viết tại chỗ ở 6-05; "đo được" trên mặt trang 6-01 với số Định nghĩa 01.4 ở ghi chú diễn giả. Còn "mọi ERM" ở 6-03 (N15). |
| Mật độ, dòng dẫn | đã sửa | lint SYLL60, LEAD25 đều 0. |

### 2.2. Các phát hiện còn lại (đối chiếu bảng mục 17 với deck)

| Phát hiện | Trạng thái | Bằng chứng ngắn |
|---|---|---|
| HV5, HV9, TH6, CG12, SP11 nhãn phần | đã sửa | 6-01 có (a), (b), (c); 6-07 "Định lý 03.15(a)"; 7-01 "Định lý 03.15; phần (a)" |
| HV6 4-03 $B$ | đã sửa | "tập điểm $B\subseteq C'$"; ghi chú diễn giả giải nghĩa "$Y_1$ tách trọn vẹn $B$" |
| HV7 3-05 bước 4 | đã sửa | bước 4 (dấu $<0$), bước 5 (phần (b)) |
| HV8, MT N8 "dạng trực tiếp" | đã sửa | 5-08: "vế phải thứ nhất của Định lý 03.15(b)" |
| HV10, TH5 $1\le d\le2m$ | đã sửa | 7-02 dòng 1; 5-07 công thức |
| HV11, MT4 (O1)/(O2) | đã sửa | 6-01 "Nhắc lại:" |
| HV12, MT N3 (M) | đã sửa | 2-01 "(M), điều kiện đo được" |
| HV13, MT N9 6-04 | đã sửa | "Cùng lớp sáu hàm ($K=6$, $\Pi\le6$)…"; "$\rho_m$ gấp hơn bốn lần $r_m$" ($0{,}2222/0{,}0523=4{,}25$) |
| HV14, CG11, SP12 6-05 "kể cả" | đã sửa | "không học được PAC, nên không học được PAC bất khả diễn" |
| HV17 dòng > 20 ở 4-01, 6-01 | đã sửa | deck_check maxLine 18, 17 |
| HV18 dấu chấm đầu dòng | đã sửa | dấu chấm trong KaTeX ở 1-06, 3-03, 5-01; ảnh 1600×900 không còn dấu chấm mồ côi |
| HV19, HV20, HV21, HV22 | đã sửa | 1-06 "trên năm mức đo, chỉ sáu hàm khác nhau"; 3-04 bỏ "hai bao lồi"; 6-03 "$m$ nhỏ nhất tìm bằng chia đôi khoảng (bisection)"; 7-02 có $132\,992$ ($d=3$) |
| TH4 $d\ge1$ ở 1-05, 5-00 | đã sửa | "khi $1\le d\le m$" ở cả hai ghi chú diễn giả |
| TH8, CG7, SP25 5-07 | đã sửa | "bất đẳng thức hợp (Bổ đề 02.12)"; bỏ "hành vi" |
| TH9 7-05 | đã sửa | "$589\,118$ ($d=3$) và $1\,999\,657$ ($d=11$)" (tính lại khớp) |
| TH11 2-07 | đã sửa | ghi chú diễn giả: "cách toàn $0$ dùng hai khoảng $[10,10]$" |
| CG3 bảo đảm theo lớp / thuật toán | đã sửa | 7-02 "bảo đảm cho lớp, mọi $h$ cùng lúc"; ghi chú diễn giả theo §9 |
| CG5 tính bị chặn | đã sửa | 5-05 bước 1 "(hàm lỗi 0–1)", bước 4 "(số hạng trong $[-1,1]$)" |
| CG9, MT N7, SP17 "đối xứng hóa", tên tiếng Anh | đã sửa | 5-06 "Đối xứng hóa (symmetrization)"; ghi chú 5-05 "bước 1–2 là đối xứng hóa"; 3-03 "Radon partition"; 6-00 "fundamental theorem"; 6-08 "sample complexity" |
| CG13 6-01 "Trực quan." | đã sửa | "$\hat h$ thắng mọi $h$ trên mẫu; mẫu lệch tổng thể tối đa $\rho_m$ tại $\hat h$ và tại $h$" |
| CG14 3-04 suy luận về gốc | đã sửa | ghi chú diễn giả: tập $\{0,\mathbf e_1,\ldots,\mathbf e_p\}$ không dùng được cho (b); cận trên qua phụ thuộc tuyến tính (Phụ lục A). Câu mới trên mặt trang xem N6. |
| CG15 σ-đại số | đã sửa | ghi chú diễn giả 2-01 |
| CG16, SP8, MT3 "Trực quan." 4-02, 5-04, 3-04 | đã sửa | 4-02 nêu cơ chế quy nạp; 5-04 hai trường hợp biên $d=0$, $d=\infty$ (số $3{,}33=\sqrt{16\ln2}$ đúng); 3-04 cơ chế ma trận. Độ chính xác của câu 4-02: N5; $\rho_m$ trước định nghĩa ở 5-04: N7 |
| SP2 "lớp giả thuyết", "thuật toán ERM" | đã sửa (một chỗ sót) | 2-01, 6-01, 6-06, SVG đã sửa; 6-03 còn "mọi ERM" (N15) |
| SP3 1-02 | đã sửa | tên đầy đủ trước, chữ viết tắt trong ngoặc; giả thiết Định lý 02.14 viết bằng lời; Hệ quả 02.16 chuyển sang 6-02. Thiếu "đo được" (N4); "(union bound)" chuyển sang 5-03 (N2) |
| SP4 Nhắc lại học PAC, khả diễn, Định nghĩa 01.4 | đã sửa | xem 2.1 |
| SP5, SP6, SP7, MT N13 | đã sửa | 1-03 mục tiêu là câu đủ, ghi chú diễn giả không còn câu quy trình; 1-04 chủ ngữ là đối tượng; 7-00 bỏ "Không có khái niệm mới", 7-05 bỏ câu cách lập bảng |
| SP9, SP15 lặp, dài ghi chú | đã sửa | lint REPEAT, NOTES150 đều 0 |
| SP10 5-08 bảng, "Diễn giải:" | đã sửa | bảng $m\times d$; "khoảng $95$ trong $100$ mẫu cho độ lệch đều $\le0{,}280$" |
| SP13 3-06 "Kết luận:" | đã sửa | "cách thiếu do phân hoạch Radon chỉ ra (Bổ đề 03.8)"; ghi chú diễn giả nêu cận trên $d\le3$ cho mọi bộ bốn điểm |
| SP16 dấu chấm phẩy 4-01, 3-05 | đã sửa | 4-01 tách hai dòng; 3-05 tách bước |
| SP18 "Bảo đảm (…):" | đã sửa | mọi trang dùng "Bảo đảm:" |
| SP19, SP20, SP21, SP22, SP23, SP24, SP26, SP27, SP28, SP29, SP31–SP38 | đã sửa | đối chiếu từng chỗ trong diff: bỏ "(đọc thêm)", "Cách sửa:"; tiêu đề 2-02; gộp "Lưu ý:" 2-04; "Diễn giải:" 4-06 "ba hàng đầu"; 6-03 tên lớp; 4-00 chủ ngữ; 4-05 bỏ câu về ghi chú; 5-05 "nên bước 1 áp dụng được"; 3-06 $z$ là giao hai đường chéo; 3-03 "chia cho $\sum_Ia_i$ được $z$"; 5-09 "Áp dụng … dù (T5) không thỏa"; 3-00 bỏ ẩn dụ; 1-06 bỏ "cần"; 1-01 luận điểm; 5-06 "Dùng khi chặn độ lệch đều trên lớp vô hạn"; 5-01 tên trước kí hiệu; 6-02 "dấu giữa hỏng" |
| SP30 2-07 mảnh câu | sửa chưa đủ | "Thứ hai xét một tập, không cho cận trên; thiếu cận dưới." vẫn là mảnh câu nén (N10) |
| MT T1 6-05 câu nối | đã sửa | "Chiều đủ: Hệ quả 03.16. Chiều cần: …" |
| MT T2, N5 | đã sửa | 3-02 "Lưu ý:"; 2-07 bỏ câu báo trước |
| MT5 6-02 $h_{\mathcal H}$ | đã sửa | "lớp vô hạn có thể không đạt $\min_hL_D(h)$" |
| MT N4 4-06 | đã sửa | ghi chú diễn giả nối $\Pi=14$ với ô vuông cuối của hình |
| MT N6, N10, N11, N12 | đã sửa | 5-05 "Nhắc lại:" đảo cận đuôi; 7-00 dòng dẫn có "đo được"; 7-02 "(T1), (T5)" gắn với độ lệch đều, (M) với định lý cơ bản; 5-05 bước 3 không lặp |

## 3. Đánh giá các mục "không sửa" hoặc "sửa một phần"

| Mục | Lý do của người sửa | Đánh giá |
|---|---|---|
| HV15, HV16 chữ trong hình nhỏ ở 390 px (4-02, 6-07) | cần lớp CSS cho hình toàn bề ngang, ngoài phạm vi ghi | chấp nhận; nhãn đã lớn hơn ở 1600×900. Đề nghị điều phối viên ghi thành việc CSS chung (`lecture-course.css`) cho mọi deck, không chặn Bài 03 |
| HV23 6-02, 4-06 vế quyết định cuộn ngang ở 390 px | cuộn tại chỗ đúng quy định; 6-02 sát trần khung | chấp nhận; ảnh `-end` cho thấy vùng cuộn có dấu hiệu tràn, trang không cuộn ngang |
| TH10 5-05 kí hiệu rút gọn $L_D$, $L_S$ không có $(h)$ | thêm $(h)$ làm công thức vượt bề ngang | chấp nhận; $\sup_h$ ngay trước làm rõ biến; ghi chú có dạng đầy đủ |
| MT N1 1-06 đứng trước §1 | ghi chú đặt Câu hỏi mở đầu trước §1 | chấp nhận; khớp thứ tự ghi chú |
| MT N2 (T4)→(T5) chỉ ở ghi chú diễn giả | trần 60 | chấp nhận; 2-01 có 58 âm tiết |
| SP30 | câu dài hơn vượt trần 60 | chưa chấp nhận trọn: có cách đủ trần, xem N10 |

## 4. Toán trên nội dung đã đổi (tính lại)

- 1-02: dạng Định lý 02.14 có "$\forall D$", xác suất $\ge1-\delta$, $r_m=\sqrt{\ln(2K/\delta)/(2m)}$, đúng Bài 02; ghi chú "(T1)–(T4) của Bài 02" đúng khối Định lý 02.14 Bài 02 (T1, T2, T3, T4). Hoeffding trên $[-1,1]$: $2e^{-2m\epsilon^2/4}=2e^{-m\epsilon^2/2}$, đúng.
- 3-04: ma trận các hàng $(x_i^\top,1)$ cỡ $(p+1)\times(p+1)$, khả nghịch khi đỉnh độc lập afin, cho $g(x_i)=2y_i-1$; đúng. "Bỏ $b$ … đơn hình chứa gốc không còn bị tách trọn vẹn": đúng cả khi gốc là đỉnh (gốc luôn nhãn $1$) lẫn khi gốc nằm trong bao lồi (cách toàn $0$ đòi $\langle w,0\rangle<0$); xem N6 về cách viết.
- 4-02, 4-06: tổng nhị thức $d=3$ tại $m=3,4,5,20$: $8, 15, 26, 1351$; $(em/3)^3$: $20{,}09$; $47{,}61$; $92{,}99$; $5951{,}27$; $1351$ so với $2^{20}$ kém $776$ lần, "gần ba bậc" đúng. 4-05: $(e/3)^3=0{,}7439$.
- 5-03 ghi chú: $\sqrt{(1000\ln2+\ln40)/2000}=0{,}590$.
- 5-04: $\sqrt{16\ln2}=3{,}330$; $d=0$ cho $\sqrt{8\ln(4/\delta)/m}$.
- 5-05: $m\rho_m^2\ge8\ln4=11{,}09\ge2$. 5-06: $|L_{S'}-L_S|\ge|L_S-L_D|-|L_{S'}-L_D|>\epsilon/2$; số mũ $2m(\epsilon/2)^2/2^2=m\epsilon^2/8$.
- 5-07: $\ln(4\Pi_{\mathcal H}(2m)/\delta)\le d\ln(2em/d)+\ln(4/\delta)$ khi $1\le d\le2m$ (Bổ đề 03.12(b) tại $2m$).
- 5-08: $d=3$: $0{,}4638$; $0{,}1644$; $0{,}05706$. $d=11$: $0{,}7622$; $0{,}2799$; $0{,}09931$. Khớp bảng.
- 5-09: $\ln(2e\cdot1000)=8{,}601$, $\ln80=4{,}382$, $\sqrt{0{,}008\cdot12{,}983}=0{,}3223$.
- 6-03 (tìm nhị phân trên điều kiện của mặt trang): $54\,330$; $132\,992$; $447\,194$; dạng đóng $88\,572$; $209\,624$; $693\,832$; tỉ số $3{,}36$. 7-05 ($\epsilon=0{,}05$): $589\,118$; $1\,999\,657$.
- 6-04: $65\ln2+\ln20=48{,}05$, $\lceil200\cdot48{,}05\rceil=9611$, $54\,330/9611=5{,}65$; $705\ln2+\ln20=491{,}66$, cỡ mẫu $98\,333$, tỉ số $4{,}55$; $\sqrt{8\ln480/1000}=0{,}2222$, $\sqrt{\ln240/2000}=0{,}0523$, tỉ số $4{,}25$.
- 6-01, 6-02: hằng số $64/\epsilon^2$, $128/\epsilon^2$ từ Định lý 03.15(c) với $\epsilon/2$; giả thiết khớp Hệ quả 03.16 ($1\le d<\infty$, (O1) đo được hoặc (O2)).
- 6-05, 6-06, 6-08: phát biểu khớp Định lý 03.17(a), (b) và Định lý 03.19 ((a) $1\le d<\infty$, (b) $2\le d<\infty$, "với mọi thuật toán, tồn tại phân bố").
- 7-06 ghi chú: $2\times0{,}1644=0{,}329$, $2\times0{,}2799=0{,}560$.

Không có sai số học nào.

## 4b. Mạch truyện (trang đổi ±2, ranh giới mạch)

- **Hệ quả 02.16 chuyển từ 1-02 sang 6-02:** không mặt trang nào trước 6-02 dẫn Hệ quả 02.16, "bước tất định" hay $2r_m$ (chỉ có ở ghi chú diễn giả 1-06 và dòng từ khóa 6-00). 6-01 nêu cơ chế mà không dẫn kết quả; 6-02 "Nhắc lại:" đứng trước chuỗi bất đẳng thức; 6-04 dẫn "Hệ quả 02.16(c)" sau 6-02; 6-07 "(1)⇒(2): bước tất định" sau 6-02. Đạt.
- Ranh giới 1-06 → 2-00 → 2-01: câu hỏi cỡ mẫu → đo lớp vô hạn → thiết lập; liền. 2-07 → 3-00 → 3-01: thứ tự trên đường thẳng → không có thứ tự trong $\mathbb R^p$; liền. 3-07 → 4-00: "Với $m>d$ điểm, cần đếm số cách gán nhãn" → hàm tăng trưởng; liền. 4-06 → 5-00 → 5-01: đa thức → hội tụ đều; liền. 5-09 → 6-00 → 6-01; 6-08 → 7-00: liền.
- Cụm 5-03 → 5-07: hai trở ngại (5-03) → định lý (5-04) → lộ trình (5-05) → đối xứng hóa (5-06) → hàm tăng trưởng thay $K$ (5-07). Thứ tự hợp lý; điểm yếu duy nhất là thuật ngữ 5-03 dùng trước 5-05 (N1).
- 4-02 → 4-03: "Trực quan." của 4-02 nói "chiều VC của một tập [cách gán nhãn]" trước khi 4-03 giải nghĩa chiều VC của $Y_1$ (N5).

## 5. Phát hiện mới hoặc còn mở

Kí hiệu N là số thứ tự trong báo cáo này. Không có phát hiện chặn bàn giao hay nghiêm trọng.

| # | mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|---|
| N1 | trung bình | L03-5-03 | Câu sửa CG4 dùng "mẫu bóng" và "dấu ngẫu nhiên" trên mặt trang trước khi định nghĩa; tên tiếng Anh và $\Pr(\sigma_i=\pm1)=\tfrac12$ chỉ có ở 5-05. Người học chưa biết "dấu ngẫu nhiên khi biết $(S,S')$" là gì. | 5-03: "Mẫu bóng $S'\sim D^m$ độc lập, $L_{S'}(h)$ thay $L_D(h)$: sửa (i); dấu ngẫu nhiên khi biết $(S,S')$: sửa (ii)." 5-05: "Mẫu bóng (ghost sample) …", "dấu ngẫu nhiên (random signs)". Quy định "Định nghĩa hoặc nhắc lại trước khi dùng" (`common-brief.md`). | Ở 5-03: "Mẫu bóng (ghost sample) $S'\sim D^m$ độc lập thay $L_D(h)$ bằng $L_{S'}(h)$: sửa (i). Đổi chỗ ngẫu nhiên $Z_i\leftrightarrow Z'_i$ khi biết $(S,S')$: sửa (ii)." và bỏ "(ghost sample)" ở 5-05; giữ "(random signs)" ở 5-05. |
| N2 | nhẹ | L03-1-02, L03-5-03 | "bất đẳng thức hợp" xuất hiện lần đầu trên mặt trang ở 1-02 không có tên tiếng Anh; "(union bound)" đã chuyển xuống 5-03. | 1-02: "**Nhắc lại:** bất đẳng thức hợp, Chebyshev, Hoeffding."; 5-03: "bất đẳng thức hợp (union bound)". Bản đóng băng có "(union bound)" ở 1-02. | Trả "(union bound)" về 1-02, bỏ ở 5-03. |
| N3 | nhẹ | L03-2-01 | "lớp con đếm được" mất tên tiếng Anh trên mặt trang (chỉ còn ở ghi chú diễn giả). | "… của dãy trong lớp con đếm được $\mathcal H_0$." / ghi chú diễn giả: "$\mathcal H_0$ là một lớp con đếm được (countable subclass)". | Thêm "(countable subclass)" trên mặt trang (lint 58 → 60, còn trong trần). |
| N4 | nhẹ | L03-1-02 | Phát biểu rút gọn của Định lý 02.14 bỏ điều kiện đo được của hàm lỗi (T2); điều kiện chỉ nằm ở ghi chú diễn giả. | "Định lý 02.14: quan sát độc lập cùng phân bố, hàm lỗi trong $[0,1]$, $K$ hàm chọn trước:" / ghi chú diễn giả: "hàm lỗi còn phải đo được". Quy định: phát biểu rút gọn không bỏ giả thiết. | "… hàm lỗi đo được, trong $[0,1]$, …" (+2 âm tiết, 53 → 55). |
| N5 | nhẹ | L03-4-02 | "Trực quan." nói lỏng: một cách gán nhãn riêng lẻ luôn "thuộc một tập có chiều VC $\le d-1$" (chẳng hạn tập một phần tử); ý đúng là tập các cách được nhân đôi có chiều VC $\le d-1$. "Chiều VC của một tập cách gán nhãn" dùng trước khi 4-03 giải nghĩa. | Mặt trang: "Thêm một điểm chỉ nhân đôi những cách gán nhãn thuộc một tập có chiều VC $\le d-1$." Ghi chú diễn giả: "… chỉ khi nó thuộc một tập có chiều VC không quá $d-1$." | "**Trực quan.** Thêm một điểm, các cách gán nhãn được nhân đôi tạo thành một tập có chiều VC $\le d-1$." Ghi chú diễn giả: "… thành hai cách của $m$ điểm khi và chỉ khi nó thuộc tập $Y_1$, và $Y_1$, coi như một lớp, có chiều VC không quá $d-1$." |
| N6 | nhẹ | L03-3-04 | Tách trọn vẹn là tính chất của một tập điểm; "đơn hình chứa gốc" là một tập lồi, đọc mơ hồ giữa "tập đỉnh có gốc" và "đơn hình chứa gốc bên trong". Khẳng định đúng ở cả hai cách đọc, nhưng lập luận "gốc luôn nhận nhãn $1$" chỉ áp cho cách đọc thứ nhất. | "Bỏ $b$: gốc luôn nhận nhãn $1$, nên đơn hình chứa gốc không còn bị tách trọn vẹn." | "Bỏ $b$: gốc luôn nhận nhãn $1$, nên tập đỉnh có gốc, như $\{0,\mathbf e_1,\ldots,\mathbf e_p\}$, không còn bị tách trọn vẹn." (hoặc "tập điểm chứa gốc") |
| N7 | nhẹ | L03-5-04 | "Trực quan." dùng $\rho_m$ ở dòng đầu, trước khi "Bảo đảm:" của cùng trang định nghĩa nó. | "**Trực quan.** $d=0$: … ; $d=\infty$: $\rho_m\ge3{,}33$, không cho thông tin." rồi mới "… với bán kính VC (VC radius) $\rho_m=\ldots$". | "$d=\infty$: cận $\ge3{,}33$, không cho thông tin." |
| N8 | nhẹ | L03-5-05 | Ba cặp ngoặc chồng nhau làm dòng khó đọc; dấu ngoặc kép "((T1))". | "hệ số $2$ ($m\epsilon^2\ge2$) ((T1), (M))."; "độc lập ((T1))."; "mẫu gộp (combined sample) ((T5))." | "hệ số $2$ khi $m\epsilon^2\ge2$; dùng (T1), (M)."; "…, độc lập; dùng (T1)."; "…; dùng (T5)." |
| N9 | nhẹ | L03-5-06 | Một dòng gói hai ý bằng dấu chấm phẩy, và "miền dài $2$: hằng số $8$" đọc như miền dài $2$ một mình cho hằng số $8$; ghi chú §7: hằng số $8$ đến từ phép chia đôi và miền dài $2$. | "$\lvert L_S-L_D\rvert>\epsilon$, … $\Rightarrow\lvert L_{S'}-L_S\rvert>\tfrac\epsilon2$; miền dài $2$: hằng số $8$ trong $\rho_m$." | Hai dòng: dòng bất đẳng thức; "Chia đôi độ lệch và miền dài $2$ cho hằng số $8$ trong $\rho_m$." (mặt trang 44 âm tiết, còn chỗ). |
| N10 | nhẹ | L03-2-07 | Mảnh câu nén (SP30 sửa chưa đủ). | "Thứ hai xét một tập, không cho cận trên; thiếu cận dưới." | "Thứ hai chỉ xét một tập năm điểm nên không cho cận trên, và thiếu cận dưới."; bù âm tiết bằng cách viết "Thứ nhất:", "Thứ hai:" thay "Lời giải thứ nhất:", "Lời giải thứ hai:" ở hai dòng đề. |
| N11 | nhẹ | L03-6-00, L03-7-02 (ghi chú diễn giả) | Sau quyết định CG8, hai câu còn nói tốc độ $1/\epsilon^2$ không bỏ được mà không giới hạn vào trường hợp bất khả diễn. | 6-00: "cận dưới cho thấy tốc độ $1/\epsilon^2$ không bỏ được"; 7-02: "cận dưới của Định lý 03.19 cho thấy tốc độ theo $1/\epsilon^2$ không bỏ được". Ghi chú: "Theo (a), tốc độ $1/\epsilon^2$ trong trường hợp bất khả diễn là cần thiết." | Thêm "trong trường hợp bất khả diễn" ở cả hai câu. |
| N12 | nhẹ | L03-6-08 | "Ý nghĩa:" dài 27 âm tiết trên một dòng (trần 20; deck_check LINE20) và cấu trúc "với … khi …" vòng. | "**Ý nghĩa:** với độ phức tạp mẫu (sample complexity) khi bất khả diễn, tốc độ $1/\epsilon^2$ là cần thiết; $M(\epsilon,\delta)$ của Hệ quả 03.16(c) dư một thừa số cỡ $\ln(1/\epsilon)$." | Hai câu: "**Ý nghĩa:** khi bất khả diễn, độ phức tạp mẫu (sample complexity) cần tốc độ $1/\epsilon^2$." / "$M(\epsilon,\delta)$ của Hệ quả 03.16(c) dư một thừa số cỡ $\ln(1/\epsilon)$." |
| N13 | trung bình | L03-7-02 | Dòng rút gọn của Định lý 03.15 bỏ (M) và hàm lỗi 0–1 (bản đóng băng có "cần (T1), (T5), hàm lỗi 0–1" ở dòng cuối; bản mới chỉ gắn (M), hàm lỗi 0–1 với định lý cơ bản). Cùng loại với phát hiện trung bình HV10 của lượt duyệt. | "(T1), (T5), mọi $D$, xác suất ít nhất $1-\delta$: độ lệch đều $\le\rho_m$, …" / Định lý 03.15: "$\mathcal H$ thỏa (T5) và (M)", hàm lỗi 0–1. | "(T1), (T5), (M), mọi $D$, xác suất ít nhất $1-\delta$: …"; "hàm lỗi 0–1" đã có ở dòng cuối, có thể chuyển lên dòng này nếu còn trong trần 60 (hiện 56). |
| N14 | nhẹ | L03-7-04 (ghi chú diễn giả, câu 1) | "điểm còn lại $x$" ngụ ý đúng một điểm còn lại; ghi chú §11: "còn ít nhất một điểm $x$ … nhãn $0$ cho mọi điểm còn lại, trong đó có $x$". | "gán $1$ cho các điểm có hoành độ, tung độ nhỏ nhất, lớn nhất, $0$ cho điểm còn lại $x$" | "… $0$ cho các điểm còn lại, trong đó có ít nhất một điểm $x$; …" |
| N15 | nhẹ | L03-6-03 | "ERM" dùng như danh từ (SP2 sót một chỗ). | "mọi ERM, mọi phân bố" | "mọi nghiệm ERM, mọi phân bố" |
| N16 | nhẹ | L03-3-06 (ghi chú diễn giả) | Cụm "là kiểm tra trên số" khó hiểu. | "Hai cấu hình là kiểm tra trên số; cận trên $d\le3$ đến từ Bổ đề 03.8 …" | "Hai cấu hình là hai bộ bốn điểm cụ thể; cận trên $d\le3$ đến từ Bổ đề 03.8 …" |
| N17 | nhẹ | `so-cach-gan-nhan.svg` (L03-4-02) | Nhãn đường cong "(em/3)³: 5951" là một công thức vẽ vào SVG (quy định: công thức là KaTeX); chú giải dạng chữ là đủ. | `<text …>(em/3)³: 5951</text>` | "dạng đóng, d = 3: 5951" (cách đọc công thức đã có ở ghi chú diễn giả). Có thể bỏ qua nếu điều phối viên coi đây là nhãn đường cong. |

`no-ai-slop` (Detect) trên văn bản mới: các mẫu thấy được là chuỗi dấu hai chấm/chấm phẩy nén (N1, N9, N10, N12) và ngoặc chồng (N8); không thấy câu rào đón về trạng thái văn bản, câu khẩu hiệu, câu hỏi tu từ, chủ ngữ là văn bản hay câu quy trình. Con trỏ điều hướng duy nhất trong ghi chú diễn giả ("ô vuông cuối của hình ở trang bổ đề Sauer–Shelah", 4-06) là theo yêu cầu MT N4 và cần để đọc số $14$; giữ.

## 6. Kết luận

Hai phát hiện nghiêm trọng (CG1 3-04; TH2/CG6/SP1 4-02) và mọi phát hiện trung bình của năm báo cáo đã sửa đúng; các điểm điều phối viên nêu riêng (5-07, (M), 6-08, trở ngại (i)/(ii), $\sigma_i$ và bước tam giác, lỗi lặp từ deck 02) đạt; nhắc lại Hệ quả 02.16 chỉ xuất hiện từ 6-02. Toán trên mọi nội dung đã đổi tính lại khớp. `deck_lint.py` 0, `footer_check.py` 0, `deck_check.py` sạch (chỉ báo động giả `\sqrt`).

Còn mở: chặn bàn giao 0, nghiêm trọng 0, trung bình 2 (N1, N13), nhẹ 15 (N2–N12, N14–N17).

**Kết luận: đạt khi sửa** (N1 và N13; các mục nhẹ sửa cùng lượt, mỗi mục một dòng, rồi kiểm lại 5-03 ±2 và 7-02 ±2 bằng `deck_lint.py`, `footer_check.py`).

Tệp nháp: `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-03/recheck/` (`slidediff.txt`, `faces.txt`, `lint.txt`, `footer.txt`, `deck_check.txt`, `check/` ảnh, `sheet-*.png`, `scripts/`).
