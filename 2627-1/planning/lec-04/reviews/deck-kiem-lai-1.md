# Kiểm lại sau biên tập deck Bài 04 — lượt 1 (chỉ đọc)

Ngày: 2026-11-15. Bản kiểm: `2627-1/lecture-04-phan-tich-sai-so.html` (55 trang) và `img/lec-04/` sau sửa. Đối chiếu: bản đóng băng trước sửa (thư mục nháp `master/frozen/`), năm báo cáo `reviews/deck-{hoc-vien,toan-hoc,chuyen-gia,su-pham,mach-truyen}.md`, quyết định của điều phối viên (`review-log.md`, mục "Năm báo cáo duyệt và quyết định của điều phối viên"), bảng sửa `storyboard.md` mục 17, `materials/lec-04/lecture-note.md`, `exercises.md`. Văn bản mới hoặc đã sửa được đọc theo `no-ai-slop` chế độ Detect và mục "The author's voice". Chỉ đọc; không sửa deck, SVG, storyboard, ghi chú.

## Kiểm tra máy (đã chạy)

Thư mục nháp: `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-04/recheck/` (`slides.diff` so từng trang, `check/` ảnh và `report.json`, `nar-01…09.png` ảnh 390 px của mọi trang đổi).

- So từng trang (theo `data-slide-id`): thứ tự 55/55 không đổi; 46 trang có thay đổi. SVG: `phan-tich-sai-so.svg` bị xóa; `can-xac-thuc.svg` thêm một dòng `<text>` "cận (a)"; `srm-danh-doi.svg` không đổi. Không còn tham chiếu nào tới `phan-tich-sai-so.svg` trong deck.
- `deck_lint.py`: 0 phát hiện.
- `footer_check.py` (1600×900): 0 trang.
- `deck_check.py --shots`: console 0, pageerrors 0, failed 0, `.katex-error` 0. OVERFLOW ở 1-02, 4-05, 5-03, 6-01…6-05, 7-01, 7-04: phần tử `path` (đuôi `\sqrt`), báo động giả đã biết. Ở 390 px `docScrollW` = 390 mọi trang; các phần tử rộng hơn màn hình đều nằm trong `span.katex-display` có cuộn ngang tại chỗ (đã kiểm bằng script). SYLL ở 7-01 (72, bảng tổng kết, trần 80); LINE20 ở bìa, 1-05, 3-07, 6-05 như trước sửa.
- Ảnh đã xem: 390×844 (cả `-end`) của 46 trang đổi; 1600×900 của 2-03, 4-08, 5-02, 6-03. Tiêu đề 5-02, 5-03 hiện "$1/m$" chữ thường (KaTeX không bị viết hoa) ở cả hai cỡ. Nhãn "cận (a)" của F3 nằm trên trục tung, không chồng số trục.

## 1. Phát hiện được chấp nhận: trạng thái

| Phát hiện | Trang | Trạng thái | Bằng chứng |
|---|---|---|---|
| CG1 (nghiêm trọng): hàm lỗi bình phương không bị chặn | 1-06, 3-01 | đã sửa | 1-06: "… bằng bình phương tối thiểu (least squares)", "Hàm lỗi bình phương không bị chặn: cận Bài 02–03 không áp dụng."; 3-01: "Hàm lỗi bình phương không bị chặn, ngoài (T3) của Mệnh đề 04.3: so các bậc qua lỗi trên nhãn mới." |
| HV1/MT19 (nghiêm trọng): số của Ví dụ 04.2 chỉ trong hình | 2-03 | đã sửa (một lỗi mới ở ghi chú diễn giả, phát hiện M4) | Mặt trang: "$L_{D_\eta}(h_3)=0{,}22$, $L_{D_\eta}(h_2)=0{,}32$: sai số xấp xỉ $0{,}04$, sai số ước lượng của $h_2$ là $0{,}10$". 2-04, 2-08 dùng các số này đều có nguồn trên mặt trang trước. |
| SP1/TH4 (nghiêm trọng): "$\hat f$ và $Y$ tương quan dương" | 3-03 (ghi chú diễn giả) | đã sửa | "số hạng chéo bằng $-2\operatorname{Cov}(\hat f,Y)$. Ở Ví dụ 04.5, $\hat f=\bar Y$ … $\operatorname{Cov}(\bar Y,Y_1)=\sigma^2/m>0$". 3-05 "Kết luận:" cũng giới hạn vào $\hat f=\bar Y$; $2\sigma^2/m=0{,}5=1{,}25-0{,}75$ đúng. |
| Định lý 04.16(a) "đếm được", $\mathcal H\ne\varnothing$ (CG6) | 5-04 | đã sửa | "$\mathcal H=\bigcup_{k\in\mathbb N}\mathcal H_k$, chiều VC mỗi $\mathcal H_k$ hữu hạn"; "$\mathcal H\ne\varnothing$"; "(đọc thêm)". Khớp ghi chú dòng 930. |
| "cận trên tin cậy" (TH1, HV3, CG10) | 4-08, 4-10, 7-02 | đã sửa | 4-08 (a) gọi tên lần đầu trên mặt trang; 4-10 "$0{,}3651$ là cận trên tin cậy mức $95\%$ cho $L_D(\hat h_3)$"; 4-10 dòng ERM trên $\mathcal H_{10}$; 7-02 "cận trên tin cậy $95\%$ là $0{,}3651$". Không còn "xác suất $\ge0{,}95$: $L_D(\hat h_3)\le\ldots$". |
| $\mathrm{pen}_k\to\infty$ và điều kiện bán kính (TH2, CG11, MT12) | 5-01 | đã sửa (câu thiếu động từ, phát hiện M7) | "Danh sách vô hạn, bán kính của Định lý 02.14(a), 03.15(a): $\mathrm{pen}_k\to\infty$"; bỏ "cỡ mẫu trong Định lý 04.11(b)". |
| "Nhắc lại:" học PAC bất khả diễn (HV5, SP12, CG5) | 5-01 | đã sửa | "$L_D(A(S))\le\inf_{h'\in\mathcal H}L_D(h')+\epsilon$, xác suất $\ge1-\delta$, khi $m\ge M(\epsilon,\delta)$, mọi $D$" đặt trên công thức Định nghĩa 04.14; hai khác biệt đọc được trên hai công thức. |
| "mốc có phạt" (TH3) | 4-08 | đã sửa | "Mốc có phạt (penalized benchmark): $\inf_k[\cdot]$ ở vế phải, không gồm $\tau$." Không còn mâu thuẫn với 7-01 "$\le$ mốc có phạt $+\tau$". Ghi chú diễn giả: "có rủi ro kì vọng không quá mốc này cộng $\tau$" (TH18). |
| Mục tiêu 4 "bất khả diễn" (TH5, CG7, SP4) | 1-03 | đã sửa | "Định nghĩa học không đều, so với học PAC bất khả diễn qua một phản ví dụ." (mục tiêu 5 có lỗi nhỏ mới, phát hiện M12) |
| Câu nối trên mặt trang: 2-03 (MT1) | 2-01 | đã sửa | "Lớp thay đổi thì $\inf_{h\in\mathcal H}L_D(h)$ đổi theo: cần một mức tham chiếu chung." Đặt ở 2-01, trước định nghĩa ở 2-03; đúng chức năng. |
| Câu nối: 2-07 (MT2) | 2-07 | đã sửa (câu chữ mơ hồ, phát hiện M8) | "$a_{10}\le a_2$ không quan sát được, $2\rho_m+\epsilon_{\mathrm{opt}}$ tính được". Cùng ý có ở 1-05 hộp 1, 2-05 "Trực quan.", 7-02 dòng 1. |
| Câu nối: 3-01 (MT3, SP6) | 3-01 | đã sửa | Như CG1. |
| Câu nối: 3-04 (MT4) | 3-04 | sửa chưa đủ (phát hiện M2) | "$\sigma^2$, $f^*$ chưa biết nên dữ liệu không chọn được bậc." Câu nói mạnh hơn ghi chú và trái 6-04, 7-02. |
| Câu nối: 6-01 (MT5, SP6) | 6-01 | đã sửa (vị trí nhãn, phát hiện M9) | "SRM chọn trên $S$ và trả $\mathrm{pen}_k$." rồi "Mẫu xác thực … chỉ để chọn". |
| Số hiệu Ví dụ 04.9, 04.10 (HV4, MT6) | 4-07, 4-10, 4-11 | đã sửa | "**Ví dụ 04.9.**" đầu 4-07; "Ví dụ 04.9 (tiếp)" ở 4-10; "**Ví dụ 04.10.**" đầu 4-11. Mọi dẫn chiếu 04.9/04.10 ở 4-12, 6-05, 7-05 nay có trang đích. |
| Hệ quả 04.15(b) (MT7, TH11) | 5-03 | đã sửa | Bước 4: "(b) $k_{\max}$ lớp: $A_{\mathrm{SRM}}$ học PAC bất khả diễn, cỡ mẫu $\max\{\lceil1/\delta\rceil,\max_kM_k(\epsilon)\}$." Khớp ghi chú Hệ quả 04.15(b). |
| Quy tắc SRM ở 7-02 (MT10, HV6, SP32) | 7-02 | đã sửa (nhưng mất loại bảo đảm ở hai dòng khác, phát hiện M3) | "SRM làm nhỏ nhất $L_S(h)+\mathrm{pen}_k$: ba chỉ số đo, cận trên tin cậy $95\%$ là $0{,}3651$ ($m=10^4$)." |
| Tiêu đề KaTeX (HV7) | 5-02, 5-03 | đã sửa | `<h2>` chứa `$1/m$`; ảnh 1600 và 390: "1/m" chữ thường. |
| 7-03 mật độ (HV20, SP33) | 7-03, 7-04 | đã sửa | Dòng "Gọi $\hat h_{(2)}$ …" mở 7-04 trước "Lời giải:"; 7-03 58 âm tiết (`deck_check`); "**Nhắc lại:**" thay "Phần (a):"; "$\mathcal R_2$: hai chỉ số đầu" khớp `exercises.md` dòng 663. |
| Các phát hiện trung bình và nhẹ còn lại (bảng mục 17) | — | đã sửa | Đối chiếu từng dòng của bảng mục 17 với `slides.diff`: HV8–HV18, HV21, TH6–TH15, TH17, CG3, CG4, CG8, CG12–CG14, SP2–SP37, MT9, MT11, MT14–MT16 đều có trong diff đúng như ghi. TH6: $0{,}16444$, $a_{10}+0{,}5699$ làm tròn lên đúng ($0{,}1644303$; $0{,}569839$). |

**Các mục "không sửa" trong bảng mục 17.**

| Mục | Đánh giá | Lý do |
|---|---|---|
| MT17 (4-12 sau 4-10) | chấp nhận | Người duyệt ghi "không bắt buộc"; 4-11 → 6-05 cùng phân bố, khuôn bài tập kết mạch giữ được. |
| HV2 (hình 4-10, 6-03 ở 390 px) | chấp nhận một phần | Ảnh 390 px: nhãn số trong hai hình vẫn khoảng 6–7 px, nhưng mọi số mà chữ dùng ($0{,}3651$; $0{,}4350$; $0{,}3593$; $0{,}0130$; $0{,}1095$; $1199$; $4794$; $0{,}1871$) có trên mặt trang và trang đã cho phóng to. Cỡ hình màn hẹp là việc của CSS chung; nên ghi thành việc riêng ở `review-log.md`. |
| HV19/TH16 (7-01 hàng 04.17) | chấp nhận | "so với ứng viên tốt nhất, giá cỡ $\sqrt{\ln K/m_v}$" đúng bậc của $2\sqrt{\ln(2K/\delta)/(2m_v)}$ với $\delta$ cố định; vế đầy đủ ở 6-01. |
| CG2 (một thuật toán) | chấp nhận | 3-02 mặt trang "Một thuật toán, một điểm"; 7-01 ghi chú diễn giả "đẳng thức kì vọng cho một thuật toán". |
| CG5 (hai khác biệt ở 5-01) | chấp nhận | Hai công thức đặt liền nhau ($\inf_{h'}L_D(h')$, $M(\epsilon,\delta)$ so với $L_D(h)$, $M(\epsilon,\delta,h)$); trang ở 57 âm tiết. |
| CG9 (giới hạn của bất đẳng thức oracle) | chấp nhận | Câu ở ghi chú diễn giả 4-08, đúng ghi chú dòng 723; mặt trang định nghĩa mốc chính xác. |
| MT10 (vế "rủi ro $\le$ mốc có phạt $+\tau$" ở 7-02) | chấp nhận | Vế này có ở 4-08 và bảng 7-01. Riêng việc dòng 1 và dòng 4 của 7-02 mất đại lượng bị chặn và xác suất là lỗi mới (M3). |

**Trang 2-03 sau khi bỏ F1.** Mặt trang đủ cho mục đích của trang: định nghĩa, ba số rủi ro và hai sai số cùng nằm trên một dòng, đọc được ở 1600 và 390 px (ảnh `wide-009`, `narrow-009-…-end`); 2-04, 2-08 dùng lại các số này có nguồn. Phần trực quan mất đi là thứ tự trên một trục ($0{,}18<0{,}22<0{,}32$, hai khoảng liền nhau) và hàng "lớp mọi hàm" có sai số xấp xỉ $0$. Không bắt buộc, nhưng nếu muốn khôi phục thứ tự mà không thêm hình: thay vế cuối dòng "Ví dụ." bằng một chuỗi KaTeX một dòng, ví dụ $0{,}18\xrightarrow{\ \text{xấp xỉ }0{,}04\ }0{,}22\xrightarrow{\ \text{ước lượng }0{,}10\ }0{,}32$ (người sửa đo lại ở 390 px). Ghi chú diễn giả 2-03 còn đọc một hình không còn trên trang (M4).

## 2. Toán trên nội dung đã đổi

Tính lại (đối chiếu bảng số của báo cáo toán học và ghi chú):

- 2-07: $2\cdot0{,}16444+0{,}01=0{,}33888\to0{,}3389$; $2\cdot0{,}27992+0{,}01=0{,}56984\to0{,}5699$; ngưỡng $0{,}5699-0{,}3389=0{,}2310$ nhất quán với số trên trang.
- 3-05: lỗi trên nhãn đã dùng $\sigma^2-\sigma^2/m=0{,}75$; hiệu với $1{,}25$ là $0{,}5=2\sigma^2/m$ ($m=4$, $\sigma^2=1$). Đúng.
- 3-06: Ví dụ 04.6, $0{,}4\cdot0{,}1+0{,}6\cdot0{,}9=0{,}58$; luôn dự đoán $0$: $0{,}9$. Ghi chú diễn giả: cả hai có dự đoán đa số $0$, hàm Bayes dự đoán $1$ tại $\eta=0{,}9$. Đúng.
- 4-09 "Kết luận:": một lớp, $q_1=1$, $\tau=0$: $\inf_k[\cdot]=\inf_hL_D(h)+2\,\mathrm{pen}_1$. Đúng.
- 4-10 ghi chú diễn giả: $0{,}155+0{,}27992=0{,}43492$, làm tròn lên $0{,}4350$. Đúng.
- 5-03 bước 4: khớp $M(\epsilon,\delta)$ của Hệ quả 04.15(b).
- 6-04 ghi chú diễn giả: $8\sqrt{\ln600/2000}=0{,}45244$. Đúng.
- 7-04 ghi chú diễn giả: $0{,}16925-0{,}16831=0{,}00094\approx0{,}001$. Đúng.
- 2-08 ghi chú diễn giả: $2r=0{,}36$. Đúng.

Phát biểu đã đổi: 2-05 bỏ "đồng thời" (M1); 3-04 kết luận quá mạnh (M2); 4-11 "một nhãn $0$" (M5); 4-08 "SRM cân hai phần" (M6). Các phát biểu còn lại (2-06, 4-04, 4-08 Bảo đảm, 5-01, 5-02, 5-04, 6-01, 6-02, 7-01) giữ giả thiết, lượng từ và loại bảo đảm của ghi chú.

## 3. Mạch truyện trên trang đổi ±2 và ranh giới mạch

- 1-05 → 1-06 → 2-00: 1-06 chỉ hỏi về bậc; dòng chỉ số đo làm lý do, câu hỏi chỉ số đo nằm ở 2-02. Liền mạch.
- 2-08 → 3-00 → 3-01: câu nối "hàm lỗi bình phương không bị chặn, ngoài (T3)" mở mạch 3 trên mặt trang. Đạt.
- 3-04 … 3-07 → 4-00 → 4-01: câu kết 3-04 "dữ liệu không chọn được bậc" đứng ngay trước mạch 4 (chọn lớp từ dữ liệu) và trái 6-04 (chọn bậc bằng mẫu xác thực). Đây là chỗ đứt mạch duy nhất do biên tập (M2).
- 4-10 → 4-11 → 4-12 → 5-00 → 5-01: số hiệu ví dụ thống nhất; 5-01 nối từ $\mathrm{pen}_k$ của mạch 4 sang cỡ mẫu theo lớp (câu thiếu động từ, M7).
- 5-04 → 6-00 → 6-01: câu nối SRM / mẫu xác thực có trên mặt trang.
- 7-00 → 7-01 → 7-02 → 7-03 → 7-04: dòng "Gọi …" chuyển sang 7-04 không làm hỏng 7-03, vì câu hỏi 7-03 nói "hai rủi ro thực nghiệm" mà không dùng kí hiệu $\hat h_{(2)}$; 7-04 định nghĩa kí hiệu trước "Lời giải:". 7-02 trả lời 1-05 với quy tắc SRM; xem M3 về loại bảo đảm.

## 4. Phát hiện mới hoặc còn mở

| # | mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|---|
| M1 | trung bình | L04-2-05 | Phần (b) mất lượng từ "đồng thời" (và "theo $S\sim D^m$") khi viết lại. Đây là điểm phân biệt bảo đảm theo lớp với bảo đảm theo thuật toán, cần cho 2-07 và mạch 4. | Mới: "mọi $D$, xác suất $\ge1-\delta$, (a) đúng cho mọi quy tắc." Trước sửa: "(a) đúng đồng thời cho mọi quy tắc". Ghi chú dòng 252: "bất đẳng thức ở (a) đúng đồng thời cho mọi quy tắc". | "mọi $D$, xác suất $\ge1-\delta$ theo $S\sim D^m$: (a) đúng đồng thời cho mọi quy tắc." (+3 âm tiết; 2-05 đang 56). |
| M2 | trung bình | L04-3-04 | "Kết luận:" nói mạnh hơn ghi chú và trái 6-04, 7-02 (dữ liệu xác thực chọn được bậc); đặt ngay trước mạch 4, nơi lớp được chọn từ dữ liệu. | "$\sigma^2$, $f^*$ chưa biết nên dữ liệu không chọn được bậc." Ghi chú dòng 550: "không cho một quy tắc chọn từ dữ liệu, vì $f^*$ và $\sigma^2$ chưa biết." | "… $\sigma^2$, $f^*$ chưa biết nên phân tích này không cho quy tắc chọn bậc từ dữ liệu." |
| M3 | trung bình | L04-7-02 | Hai dòng rút gọn mất đại lượng bị chặn hoặc loại bảo đảm (bài học deck 02 trong `common-brief.md`). Dòng 1 không còn "sai số ước lượng" và "xác suất $\ge1-\delta$"; dòng 4 còn "xác suất $\ge1-\delta$" nhưng đã mất đại lượng được chặn ($2\sqrt{\ln(2K/\delta)/(2m_v)}$). | Dòng 1: "… cận $2r+\operatorname{opt}_S$ tính được."; dòng 4: "mẫu xác thực cần (T7), giữ $m_v$ quan sát; xác suất $\ge1-\delta$." Trước sửa: "sai số ước lượng $\le2r+\operatorname{opt}_S$, xác suất $\ge1-\delta$"; "giá $2\sqrt{\ln(2K/\delta)/(2m_v)}$, xác suất $\ge1-\delta$". | Dòng 1: "… cận $2r+\operatorname{opt}_S$ của sai số ước lượng (xác suất $\ge1-\delta$) tính được." Dòng 4: "… giữ $m_v$ quan sát; so với ứng viên tốt nhất, giá $2\sqrt{\ln(2K/\delta)/(2m_v)}$, xác suất $\ge1-\delta$." Trang đang 60 âm tiết: bù bằng cách bỏ "($m=10^4$)" ở dòng 2 hoặc rút "Cùng $L^*$, lớp lồng nhau:" thành "Lớp lồng nhau, cùng $L^*$:" và bỏ "không quan sát được" (đã có ở 2-07, 2-05). Người sửa đếm lại. |
| M4 | trung bình | L04-2-03 (ghi chú diễn giả) | Ghi chú diễn giả còn "Đọc hình: …" cho hình F1 đã bỏ, kể cả hàng "lớp mọi hàm" không còn ở đâu trên trang. Câu thêm "Các số $0{,}22$; $0{,}32$ là rủi ro của $h_3$, $h_2$ ở Ví dụ 01.2; $D_\eta$ là phân bố của Ví dụ 01.1." lặp dẫn chiếu đã có trên mặt trang; ghi chú diễn giả 158 token (`deck_check`), quá 150. | `lecture-04-phan-tich-sai-so.html` dòng 153: "Đọc hình: ở lớp sáu hàm ngưỡng, khoảng từ $0{,}18$ đến $0{,}22$ … ở lớp mọi hàm, hàm phân lớp tối ưu Bayes $\mathbb 1[x\in\{3,5\}]$ thuộc lớp." | Đổi "Đọc hình:" thành câu về số: "Ở lớp sáu hàm ngưỡng, $0{,}04$ là cái giá của việc giới hạn vào hàm ngưỡng, $0{,}10$ là cái giá của việc chọn $h_2$ thay cho $h_3$; lớp mọi hàm trên năm mức đo chứa hàm phân lớp tối ưu Bayes $\mathbb 1[x\in\{3,5\}]$, nên sai số xấp xỉ của nó bằng $0$." Bỏ câu "Các số $0{,}22$; $0{,}32$ …". |
| M5 | nhẹ | L04-4-11 | "có một nhãn $0$" đọc được là đúng một nhãn; xác suất $1-0{,}8^{1000}$ ứng với ít nhất một. | "SRM chọn $\mathbb 1_{F_+}$ khi $S$ có một nhãn $0$"; ghi chú dòng 824: "có ít nhất một nhãn $0$". | "… khi $S$ có ít nhất một nhãn $0$" (+2 âm tiết; 4-11 đang 53). |
| M6 | nhẹ | L04-4-08 | "SRM cân hai phần": SRM không thấy $\inf_{h\in\mathcal H_k}L_D(h)$; vế phải của (b) mới cân hai phần, SRM đạt mức đó cộng $\tau$. | "**Trực quan.** … $\inf_{h\in\mathcal H_k}L_D(h)$ không tăng, $2\,\mathrm{pen}_k$ tăng; SRM cân hai phần." Ghi chú diễn giả cùng trang: "SRM không biết số hạng thứ nhất". | "…; vế phải của (b) cân hai phần." |
| M7 | nhẹ | L04-5-01 | Vế sau thiếu động từ, đọc như cụm từ khóa dán vào câu. | "…: $\mathrm{pen}_k\to\infty$, nên cỡ mẫu theo lớp chứa $h$." | "…, nên cỡ mẫu phụ thuộc lớp chứa $h$: cỡ mẫu theo lớp." hoặc "…, nên cần cỡ mẫu theo lớp chứa $h$." |
| M8 | nhẹ | L04-2-07 | (1) "$a_{10}\le a_2$ không quan sát được" đọc như bất đẳng thức không quan sát được; ý là hai số $a_2$, $a_{10}$ không quan sát được. (2) "Nhắc lại:" của Định lý 03.15(b) bỏ điều kiện $1\le d\le m$ có ở bản trước. | Mặt trang dòng 5; bản đóng băng: "$\rho_m^2\le\ldots$, $1\le d\le m$ (Định lý 03.15(b))". | (1) "$a_{10}\le a_2$, cả hai không quan sát được; $2\rho_m+\epsilon_{\mathrm{opt}}$ tính được; …". (2) Trả lại "$1\le d\le m$" nếu còn chỗ (trang đang 50). |
| M9 | nhẹ | L04-6-01, L04-4-10 | Nhãn "Trực quan." gắn sai câu. 6-01: nhãn đứng trước câu nối về SRM, còn trực quan của Hệ quả 04.17 ở dòng sau. 4-10: "**Trực quan.** Ví dụ 04.9 (tiếp): …" đặt nhãn ví dụ bên trong nhãn trực quan. | 6-01 dòng 1–2; 4-10 dòng 1. | 6-01: "SRM chọn trên $S$ và trả $\mathrm{pen}_k$. **Trực quan.** Mẫu xác thực … chỉ để chọn: …". 4-10: "**Ví dụ 04.9 (tiếp).** **Trực quan.** $L_S(\hat h_k)$ …" hoặc bỏ "Trực quan." vì dòng là cách đọc hình của ví dụ. |
| M10 | nhẹ | L04-3-06 | Dòng "Lưu ý:" có hai dấu hai chấm nối tiếp và vế không chủ ngữ ("dao động nhiều hơn: lỗi …"); không nói thuật toán nào. | "… $\Pr(Y=1\mid x)=0{,}9$: dao động nhiều hơn: lỗi $0{,}58$; luôn dự đoán $0$: lỗi $0{,}90$ (Ví dụ 04.6)." | "**Lưu ý:** nhãn $\{0,1\}$, $\Pr(Y=1\mid X=x)=0{,}9$: thuật toán dao động nhiều hơn có lỗi $0{,}58$, thuật toán luôn dự đoán $0$ có lỗi $0{,}90$ (Ví dụ 04.6)." |
| M11 | nhẹ | L04-3-05 | "nhãn đã huấn luyện" sai nghĩa (nhãn không huấn luyện); ghi chú viết "nhãn đã dùng để huấn luyện". | "**Kết luận:** với $\hat f=\bar Y$, lỗi trên nhãn đã huấn luyện thấp hơn trên nhãn mới $2\sigma^2/m$." | "… lỗi trên nhãn đã dùng để huấn luyện thấp hơn lỗi trên nhãn mới $2\sigma^2/m$." |
| M12 | nhẹ | L04-1-03 | Mục tiêu 5 "Tính cận xác thực": cụm không có trong ghi chú hay `thuat-ngu.md`; ghi chú: "Tính cận cho chọn mô hình bằng mẫu xác thực". | 1-03 mục 5. | "Tính cận của mẫu xác thực; …" (như bản trước). |
| M13 | nhẹ | L04-1-06 | "cận Bài 02–03" thiếu "các … của"; dòng cận $0{,}329$, $0{,}560$ mất nguồn "(Bài 03)". | 1-06 dòng 3–4. | "… các cận của Bài 02–03 không áp dụng."; "cận rủi ro vượt mức (Bài 03), xác suất $\ge0{,}95$: …". Đếm lại (trang đang 59). |
| M14 | nhẹ | L04-2-05, L04-2-02 | Dấu câu sau KaTeX rơi xuống dòng riêng ở 390 px: 2-05 dấu ":" sau "$\delta\in(0,1)$" (mới); 2-02 dấu "," trước "dùng bao nhiêu chỉ số đo?" (có từ trước, ngoài danh sách HV21). | Ảnh `narrow-011-L04-2-05`, `narrow-008-L04-2-02-end`. | Đưa dấu câu vào trong `$…$` như các chỗ đã sửa theo HV21. |
| M15 | nhẹ | L04-7-01 | Tiêu đề cột bỏ "mọi $D$" khi rút gọn loại bảo đảm. | Trước: "Kết quả (xác suất $\ge1-\delta$, mọi $D$; trừ 04.6)"; sau: "Kết quả (xác suất $\ge1-\delta$, trừ 04.6)". | Trả lại "mọi $D$" nếu bảng vẫn vừa khung ở 1600×900. |

**Văn phong (`no-ai-slop` Detect, "The author's voice").** Văn bản mới không có từ rào đón ("thường", "chủ yếu", "vài" đã thay bằng số), không câu về trạng thái văn bản ("trả lời một phần" đã bỏ ở 6-04, 7-02), không câu chỉ đường, không lời bình kỹ thuật (3-03, 5-03 đã cắt). Mẫu còn gặp: chuỗi dấu hai chấm (M10), câu cụt thiếu động từ (M7), nhãn đặt sai chỗ (M9). Câu "Mốc có phạt không phải rủi ro vượt mức so với hợp các lớp." ở ghi chú diễn giả 4-08 là phủ định toán học lấy từ ghi chú dòng 723, giữ.

## Kết luận

Ba phát hiện nghiêm trọng và mọi phát hiện được chấp nhận trong bảng quyết định đã sửa; một mục sửa chưa đủ (câu nối 3-04). Bảy mục "không sửa" đều chấp nhận được (HV2 chấp nhận một phần, cần việc CSS riêng). Máy: `deck_lint.py` 0, `footer_check.py` 0, `deck_check.py` sạch (chỉ báo động giả đã biết). Biên tập sinh lỗi mới: 0 chặn bàn giao, 0 nghiêm trọng, **4 trung bình** (M1–M4), **11 nhẹ** (M5–M15). Mỗi chỗ sửa là một cụm từ trên một trang, không cần thêm trang.

**Kết luận: đạt khi sửa.** Sau khi sửa M1–M4, kiểm lại 2-03 (ghi chú diễn giả), 2-05, 3-04, 7-02 bằng `deck_lint.py`, `footer_check.py` và ảnh 390 px `-end`.

## Đề xuất sửa ghi chú

Không có đề xuất mới.
