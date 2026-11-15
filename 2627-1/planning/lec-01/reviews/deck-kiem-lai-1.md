# Kiểm lại sau biên tập — deck Bài 01, lượt 1 (2026-11-15)

Vai: kiểm lại sau biên tập (chỉ đọc). Đối tượng: `2627-1/lecture-01-mo-hinh-hoc.html` và `img/lec-01/` sau sửa, so với bản đóng băng trước sửa (thư mục nháp của phiên, `lec-01/frozen/`). Căn cứ: năm báo cáo `reviews/deck-*.md`, quyết định của điều phối viên trong `review-log.md` (hai mục "Năm báo cáo duyệt…" và "Sửa sau năm báo cáo…"), bảng sửa `storyboard.md` mục 15, `materials/lec-01/lecture-note.md`, `exercises.md`. `no-ai-slop` chế độ Detect và "The author's voice" áp cho văn bản mới hoặc đã sửa.

Cách làm: tách deck thành từng trang (mặt trang và ghi chú diễn giả), so từng trang với bản đóng băng (48 trang đổi mặt, 51 trang đổi ghi chú); đọc lại toàn bộ deck sau sửa; tính lại mọi con số trên nội dung đã đổi; đối chiếu phát biểu với các khối của ghi chú (Định nghĩa 01.16–01.28, Mệnh đề 01.7, 01.15, 01.23, 01.31, Hệ quả 01.29, Nhận xét 01.17, 01.19, 01.26, 01.30); đối chiếu bảng `Mục | Bài tập` với đề Bài tập 01.1–01.11; chạy `deck_check.py --shots`, xem bảng ảnh 1600×900 của cả 55 trang và ảnh 390×844 (kể cả ảnh `-end`); dựng bản đóng băng để so bốn trang sát đáy.

## 1. Trạng thái các phát hiện được chấp nhận

### 1a. Nghiêm trọng (2)

| Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|
| TH1 / CG1: 7-02 và ghi chú 1-05 bỏ "khả diễn" ở bảo đảm của $A_{\max}$ | đã sửa | 7-02: "Với mọi phân bố khả diễn trên lớp hàm ngưỡng, $A_{\max}$ là thuật toán học PAC với $M(\epsilon,\delta)=\lceil\ln(1/\delta)/\epsilon\rceil$." Ghi chú 1-05 và 1-04: "trên lớp hàm ngưỡng, với mọi phân bố khả diễn, $A_{\max}$ đạt bảo đảm học PAC khi …". Khớp Mệnh đề 01.31 (giả thiết $(D,\mathcal H)$ khả diễn). Ghi chú 1-05 dòng 2 dùng "khi", không "chỉ khi". |

### 1b. Trung bình (29)

| Phát hiện | Trang | Trạng thái | Bằng chứng |
|---|---|---|---|
| HV1 / TH13 | 2-02 | đã sửa | "$D_\eta$: nhãn $1$ với xác suất $\eta(x)$"; "$D_f$: $y=f(x)$ với hàm gán nhãn … $f=h_3$". |
| HV2 | 2-04 | đã sửa | Công thức hiển thị $L^c_{D_\eta}(h_t)=0{,}2[c_{FN}\sum_{x<t}\eta+c_{FP}\sum_{x\ge t}(1-\eta)]$; câu hỏi $L^c_{D_\eta}(h_2)$ làm được từ mặt trang. Xem mục 5, phát hiện 1 và 2. |
| HV3 / SP29 | 5-11 | đã sửa | Hai rủi ro vượt mức viết tường minh trước đẳng thức. |
| HV4 / SP31 | 6-01 | đã sửa | "Với $\ell_{0\text{-}1}$, $\mathcal Y=\{0,1\}$, $\beta(m,\delta)$ là cận … nếu với mọi thuật toán ERM $\hat A$, mọi $D$, $m$, $\delta$:" — có động từ chính, khớp Định nghĩa 01.28. |
| HV5 | toàn deck | đã sửa | `.lecture-viewport` có, khối script "Màn hẹp" trùng từng dòng với `lecture-template.html` (diff rỗng). Ảnh 390×844: chữ đọc được, công thức và bảng rộng cuộn tại chỗ. |
| TH2 / CG2 | 6-03 | đã sửa | Bước 1: "$L_S=0$ (lớp chứa hàm phân lớp ghi nhớ), $L_D=1$ (không có nguyên tử)"; bước 4 "(cả hai giả thiết)"; ghi chú viết "Mệnh đề 01.15(a)/(b)/(c)". Không mâu thuẫn Hệ quả 01.29. |
| TH3 | 3-02 | đã sửa | "$\mathbb E_{S\sim D_\eta^6}[L_S(h_3)]=0{,}22$". |
| TH4 / CG6 / SP1 | ghi chú 1-05 | đã sửa | "… khi $h$ không phụ thuộc $S$; với $h=A(S)$ thì nói chung không." |
| TH5 | ghi chú 4-03, 7-01 | đã sửa | "$\mathbb E_S[L_{D_1}(A_{\mathrm{gn}}(S))]=0{,}8^m$" ở cả hai trang. |
| TH6 / CG15 | 4-01, 5-07 | đã sửa | 4-01: "$\mathcal M_{\mathcal X}$: mọi hàm phân lớp đo được $\mathcal X\to\{0,1\}$; ở đây $\mathcal X=[0,1]$"; 5-07: "Rủi ro Bayes … dưới $\ell_{0\text{-}1}$". |
| CG3 | 6-06 | đã sửa | "Bỏ khả diễn: bước 1 hỏng; dưới $D_\eta$, $L_D(h_t)\ge0{,}22$ với mọi $t$." Có cơ sở: Nhận xét 01.17. |
| CG4 / SP32 | 6-02 | đã sửa | "Ý nghĩa: (b) nói về $A_{\mathrm{gn}}$, không về lớp; bảo đảm học cần cấu trúc của lớp hoặc thuật toán." Cơ sở: ghi chú dòng 1088. |
| CG5 | 5-03 | đã sửa | Gạch đầu dòng "$D$ chạy trên các phân bố mà $(D,\mathcal H)$ khả diễn." (cùng cách viết với ghi chú sau Định nghĩa 01.18). |
| CG7 | 2-01 | đã sửa | Hộp Lưu ý: "$S$, $A(S)$ và rủi ro của $A(S)$ ngẫu nhiên". |
| CG8 | 3-04, 6-02 | đã sửa theo quyết định | ERM xấp xỉ, $\epsilon_{\mathrm{opt}}$, (O1)/(O2) ở ghi chú diễn giả 3-04; 6-02 "thuật toán ERM chính xác"; (O1) ở ghi chú 6-02. |
| SP2 | 2-02 | đã sửa | Câu "Ví dụ đủ nhỏ để tính tay …" không còn. |
| SP3 | 2-00…7-00 | đã sửa | Không còn nhãn "Kế thừa:/Nhiệm vụ:/Kết quả trao đi:". Xem mục 5, phát hiện 5. |
| SP4 / MT6 | 4-02 | đã sửa | "Ý nghĩa: $A_{\mathrm{gn}}$ quá khớp (overfitting) ở mức cực đoan." |
| SP5 / HV16 | 5-07 | đã sửa | "Chọn như vậy tại mỗi mức cho $\mathbb 1[x\in\{3,5\}]$" — không dùng "hàm Bayes" trước 5-08. |
| SP6 | 4-01, 4-03, 4-06, 6-04, 7-01, 6-01 | đã sửa | `grep "hàm ghi nhớ"` trên deck: 0 kết quả. |
| MT1 | 3-01 | đã sửa | "$L_D(h)$ không tính được vì $D$ chưa biết; $L_S(h)$ tính được từ $S$." |
| MT2 | 5-07 | đã sửa | "…, nên $L_D(A(S))\le\epsilon$ không đạt khi $\epsilon<0{,}05$." |
| MT3 | 5-11, 5-12 | đã sửa | "Câu hỏi: so $L_D(A(S))$ với $\inf_hL_D(h)$ hay với $L_D^{\mathrm{Bayes}}$?" cuối 5-11; ghi chú 5-11 kết bằng câu trả lời. |
| MT4 | 6-02, 6-05 | đã sửa | Ý nghĩa 6-02 (như CG4) và dòng đầu 6-05 "Lớp hàm ngưỡng có cỡ mẫu đủ chung cho mọi phân bố khả diễn." |
| MT5 / TH14 | 7-05 | đã sửa | Kiểm từng bài theo đề trong `exercises.md` (mục 3). |

### 1c. Nhẹ (79) và các điểm không sửa

- Đối chiếu từng dòng của `storyboard.md` mục 15 với deck: mọi mục ghi "đã sửa" đều thấy trên deck, gồm HV6–HV12, HV14–HV23, TH7–TH12, CG9–CG18, SP7–SP41, MT7–MT9, MT11–MT13.
- **Sửa chưa đủ (2, nhẹ):** CG17(a) — hàng Hệ quả 01.29 của 7-01 chưa ghi loại bảo đảm (mục 5, phát hiện 3); HV (nhẹ, 7-01 sát chân trang) — bảng thấp hơn nhưng đáy hàng cuối vẫn chạm dòng chân trang (mục 5, phát hiện 1).
- HV13 / MT10 (thứ tự trang ý tưởng chứng minh → "Kỹ thuật."): điều phối viên bác bỏ; deck giữ thứ tự, nhất quán ở 4-03/4-04 và 6-06/6-07.
- SP42 ("mini-batch"): không sửa theo quyết định; ghi chú diễn giả 2-01 vẫn theo ghi chú.
- SP21 (3-04 "Diễn giải:"): đã sửa đúng theo đề xuất của báo cáo; câu mới nhắc lại bốn số của bảng ngay trên, nhưng có nội dung so sánh hai quy tắc, nên không mở phát hiện.

## 2. Toán trên nội dung đã đổi (tính lại)

| Trang | Đại lượng | Kết quả kiểm |
|---|---|---|
| 2-04 | $L_{D_\eta}(h_t)$, $t=1..6$: $0{,}52;0{,}32;0{,}22;0{,}32;0{,}28;0{,}48$; $L^c$ với $(c_{FP},c_{FN})=(1,4)$: $0{,}52;0{,}32;0{,}37;0{,}92;1{,}12;1{,}92$; $0{,}2(4\cdot0+1{,}6)=0{,}32$ | đúng |
| 3-01 | số lỗi trên $S_\eta$ của $h_1..h_6$: $3,2,2,3,2,3$; $L_{S_\eta}(h_3)=2/6$ | đúng |
| 3-02 | $\mathbb E_{S\sim D_\eta^6}L_S(h_3)=L_{D_\eta}(h_3)=0{,}22$; $m=1$ dưới $D_f$: $\mathbb E\,\mathbb 1[X_1=3]=0{,}2$ | đúng |
| 3-04 | tập nghiệm $\{h_2,h_3,h_5\}$ / $\{h_3,h_4\}$; mất $0{,}10$, $0{,}06$ | đúng |
| 3-05 | $\hat t=6,6,3,4,5$; $L_{D_f}=0{,}6;0{,}6;0;0{,}2;0{,}4$, trung bình $0{,}36$; $\Pr(N\ge k)=(1-0{,}2k)^m$; $m=10$: $0{,}2(0{,}10737+0{,}00605+0{,}00010)=0{,}0227$ | đúng |
| 3-06 | $0{,}28-\tfrac13=-\tfrac4{75}$; kì vọng khoảng cách $\ge0{,}2\cdot0{,}8^m$ | đúng |
| 4-06 | $A_{\mathrm{gn}}(\tilde S_f)$ sai tại $x=4$, rủi ro $0{,}2$; $h_t$ khớp $\tilde S_f$ khi $1<t\le3$ | đúng |
| 5-01 | $0{,}999^{500}=e^{-0{,}50025}\approx0{,}606$ | đúng |
| 5-05 | $0{,}8^{13}=0{,}0550$, $0{,}8^{14}=0{,}0440$, $0{,}6^5=0{,}0778$, $0{,}6^6=0{,}0467$ | đúng |
| 5-06 | $1-0{,}8^{14}=0{,}956$ | đúng |
| 5-07 | $0{,}2\cdot\min\{\tfrac14,\tfrac34\}=0{,}05$; $0{,}2(\tfrac14+\tfrac14+\tfrac25)=0{,}18$ | đúng |
| 5-08, 5-09 | ngưỡng $\tfrac{c_{FP}}{c_{FP}+c_{FN}}$; rủi ro (b) $\mathbb E\min\{c_{FN}\eta,c_{FP}(1-\eta)\}$; $0{,}2\lvert2\cdot0{,}4-1\rvert=0{,}04$ | đúng |
| 5-10 | ngưỡng $\tfrac15$, đạt tại $x=2..5$; $0{,}2(\tfrac34+\tfrac14+\tfrac35)=0{,}32$ | đúng |
| 5-11 | $0{,}32-0{,}18=0{,}10+0{,}04$ | đúng |
| 6-04 | $5\cdot0{,}2\cdot0{,}8^m=0{,}8^m$; $0{,}8^{10}=0{,}107$ | đúng |
| 6-05, 6-07 | $10\ln20=29{,}96\to30$; $e^{-3}=0{,}0498$, $e^{-2{,}9}=0{,}0550$ | đúng |
| 6-06 | bước 3: $L_D(h_{\hat t})=G(\hat t)\le G(k)=D_{\mathcal X}(\{t^\star,\ldots,k-1\})\le\epsilon$; chuỗi $(1-D_{\mathcal X}(C))^m\le(1-\epsilon)^m\le e^{-\epsilon m}$ | đúng, khớp chứng minh phác thảo của Mệnh đề 01.31 |
| 7-03 | $(c_{FP},c_{FN})=(4,1)$, ngưỡng $\tfrac45$ | đúng, khớp lời giải Bài tập 01.1(d) |

Phát biểu: 3-02 (Mệnh đề 01.7: bốn giả thiết, "với mọi $m\ge1$, theo kì vọng"), 4-02 (Mệnh đề 01.15 (a)(b)(c), "tất định, với mọi $m\ge1$ và mọi $S$"), 5-02 (Định nghĩa 01.16, 01.18, $M:(0,1)^2\to\mathbb N$), 5-04 (Định nghĩa 01.20), 5-12 (Định nghĩa 01.25), 6-01 (Định nghĩa 01.28), 6-02 (Hệ quả 01.29: (O1), (T1), "dưới $D$ khả diễn" với $D$ của Mệnh đề 01.15), 6-05 (Mệnh đề 01.31): khớp ghi chú, không bỏ giả thiết, lượng từ hay loại bảo đảm. SVG đổi (F5a, F6, F7, F8): chỉ đổi chiều cao khung, tọa độ dọc và "logarit" → "lôgarit" trong `<desc>`; số liệu không đổi.

## 3. Mạch truyện (trang đổi ±2 và ranh giới mạch)

- **Dòng dẫn mạch mới.** 2-00 "Chất lượng của một hàm dự đoán là mức sai trung bình của nó trên dữ liệu mới."; 3-00 "Tỉ lệ lỗi trên tập huấn luyện có trung bình bằng mức sai trên dữ liệu mới khi hàm được chọn trước."; 4-00 "Một hàm khớp mọi quan sát huấn luyện vẫn có thể sai với xác suất 1 trên quan sát mới."; 5-00 "Học được nghĩa là rủi ro gần mức tốt nhất với xác suất cao khi đủ dữ liệu."; 6-00 "Rủi ro thực nghiệm nhỏ không đủ làm bảo đảm học; bảo đảm cần cỡ mẫu chung cho mọi phân bố." Năm câu trần thuật về nội dung, không mở bằng "Người học", không lặp khuôn, mỗi câu khớp nội dung mạch. Riêng 7-00 nói về bài chứ không nêu nội dung (mục 5, phát hiện 4).
- **Ranh giới.** 2-05 → 3-00 → 3-01: câu hỏi cuối 2-05 và dòng "$L_D(h)$ không tính được …; $L_S(h)$ tính được từ $S$" ở 3-01 nối trên mặt trang. 3-07 → 4-00 → 4-01: dòng dẫn 4-00 nêu đúng kết quả của mạch 4. 4-06 → 5-00 → 5-01: dòng cuối 4-06 ("bảo đảm học phải cho phép thất bại …") dẫn sang $\delta$ ở 5-01. 5-12 → 6-00 → 6-01: thứ tự định nghĩa → phản ví dụ → bảo đảm dương liền mạch; 6-02 Ý nghĩa và 6-05 dòng đầu nối hai nửa mạch 6 (MT4). 6-07 → 7-00 → 7-01: không khái niệm mới.
- **Trong mạch 5:** 5-06 → 5-07 (giới hạn khả diễn dưới $D_\eta$ trên mặt trang) → 5-08 → 5-09 → 5-10 → 5-11 (câu hỏi so sánh) → 5-12 (trả lời bằng đối tượng so sánh): mạch không đứt.
- **Thứ tự định nghĩa trước khi dùng** trên các trang đổi: $L_D$ ở 2-01 viết bằng lời ("rủi ro của $A(S)$"), $L_D$ định nghĩa ở 2-03; "ERM", "PAC" chuyển xuống 3-04, 5-02 (nơi dùng lần đầu trên trang nội dung); $\mathcal M_{\mathcal X}$ tổng quát ở 4-01 trước 5-07, 6-04. Không thấy kí hiệu dùng trước khi định nghĩa trên mặt trang.
- **Bảng `Mục | Bài tập` (7-05).** Kiểm theo đề: 01.3 (tính không chệch, thuật toán chọn theo $Z_1$) → mạch 3; 01.6 (ghi nhớ trên lớp đa thức, thiên kiến quy nạp) → mạch 4; 01.1(d) (quy tắc Bayes dưới $\ell_c$), 01.2(b)(c) (rủi ro vượt mức), 01.5 (lượng từ, $A_{\mathrm{gn}}$ trên $\mathbb N$, đọc bảo đảm), 01.7 (đơn điệu của độ phức tạp mẫu), 01.11 (tối ưu Bayes) → mạch 5; 01.4(c) (so với Ví dụ 01.11 ở 6-04), 01.8(b) và 01.9 (cận $\lceil\ln(1/\delta)/\epsilon\rceil$), 01.10(b) ($A'$ học PAC khả diễn) → mạch 6. Đúng quy tắc "mạch cung cấp kiến thức cuối cùng". Ghi chú diễn giả 7-05 nêu phần nào dùng kiến thức nào, khớp đề. Liên kết viewer có `&deck=`.

## 4. Kiểm tra máy

`deck_check.py --shots` (http://localhost:8766): slides=55, console=0, pageerrors=0, failed=0, `.katex-error`=0, cột overflow=0 ở mọi trang. Mật độ theo công cụ: mọi trang nội dung ≤ 60, trừ 1-03 (80, trần 80), 7-01 (69, bảng tổng kết, trần 80), 7-03 (65, ngoại lệ đã ghi). Cờ NARROW-H ở 2-03, 2-04, 3-05, 4-03, 5-03, 5-08, 5-09, 5-11, 5-12, 6-01, 6-03…6-06, 7-01: ảnh 390×844 cho thấy đó là công thức hoặc bảng cuộn ngang tại chỗ (có viền gợi ý), trang không cuộn ngang. Ghi chú diễn giả: theo cách đếm của tôi (bỏ KaTeX), chỉ 4-03 (161), 5-12 (152), 6-03 (152) vượt 150; 4-03, 6-03 là trang chứng minh (trần ≈ 250), 5-12 vượt 2 âm tiết.

## 5. Phát hiện mới hoặc còn mở

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L01-6-03, L01-2-04 (mới do biên tập); L01-7-01, L01-6-05 (đã có trước) | Ở 1600×900 nội dung chạm đáy khung: chỉ số dưới đè lên dòng chân trang hoặc nằm dưới nút điều hướng. 6-03: dòng "thiết): $m_{A_{\mathrm{gn}}}=\infty$." có chỉ số "gn" đè lên chữ "2026" của chân trang; bản đóng băng kết thúc cách chân trang ≈ 40 px. 2-04: câu đầu thành hai dòng nên hàng $L^c_{D_\eta}(h_t)$ của bảng xuống sát đáy, nút ⌃⌄ đè lên mép ô. 7-01: $m_{A_{\max}}$ chạm chân trang (đã có trước; phát hiện nhẹ của học viên "sửa chưa đủ"). 6-05: dòng "Ý nghĩa:" nằm dưới nút điều hướng. `deck_check` không báo vì phần tử vẫn trong khung. | `recheck/check/wide-043-L01-6-03.png`, `wide-010-L01-2-04.png`, `wide-049-L01-7-01.png`, `wide-045-L01-6-05.png`; so với `recheck/frozen-check/wide-*.png` | 6-03: bỏ "(cả hai giả thiết)" ở bước 4 hoặc gộp bước 2 với công thức để bớt một dòng (ghi chú diễn giả đã nêu đủ). 2-04: xem phát hiện 2. 7-01: cho công thức cột "Ý tưởng chứng minh" hàng cuối gọn một dòng ("bỏ sót $C$; $e^{-\epsilon m}$"), hoặc rút ô 01.23. 6-05: bỏ dòng đầu hoặc rút "Trực quan." một dòng. Chụp lại 1600×900. |
| nhẹ | L01-2-04 | Ngoặc chen giữa câu và công thức: "… khi $Y=0$, nên ($c_{FN}=c_{FP}=1$ cho $L_{D_\eta}$)" rồi mới đến công thức $L^c$; câu khó đọc và tốn thêm một dòng. | mặt trang 2-04, dòng 1 | "… khi $Y=0$, nên" + công thức; thêm sau công thức "$L_{D_\eta}$ ứng với $c_{FN}=c_{FP}=1$." hoặc để câu này ở ghi chú diễn giả (ghi chú đã có). |
| nhẹ | L01-7-01 | CG17(a) sửa chưa đủ: bốn hàng ghi loại bảo đảm (kì vọng, tất định, tổng thể, xác suất cao), hàng Hệ quả 01.29 không ghi. | "Hệ quả 01.29: $\beta\ge1$ trên $\mathcal M_{\mathcal X}$" | "Hệ quả 01.29 (tất định): …" — khoảng cách tổng quát hóa bằng $1$ trên mọi $S$. |
| nhẹ | L01-7-00 | Dòng dẫn nói về bài, không nêu ý cốt lõi (metadiscourse), trái mẫu của tác giả và năm dòng dẫn còn lại. | "Các kết quả của bài trả lời câu hỏi học có nghĩa là gì." | Một câu nội dung, ví dụ câu của ghi chú (cuối §7): "Học là chọn hàm có rủi ro gần mức tốt nhất trong lớp với xác suất cao, khi cỡ mẫu vượt một ngưỡng không phụ thuộc phân bố." |
| nhẹ | ghi chú L01-3-00, L01-5-00, L01-6-00 | Văn bản làm chủ ngữ ("Phần này …"), trái quy định văn phong của khóa ("the document is never the subject"). | "Phần này thay $L_D$ bằng …"; "Phần này trả lời ba câu hỏi chính …"; "phần này phát biểu phản ví dụ …" | Đặt chủ ngữ là đối tượng: "Rủi ro thực nghiệm thay $L_D$ bằng trung bình hàm lỗi trên $S$; …"; "Hai định nghĩa học PAC trả lời ba câu hỏi chính …"; "Phản ví dụ được phát biểu bằng ngôn ngữ học PAC, …". |
| nhẹ | ghi chú L01-7-04 (câu 3) | Lệch với 5-06 sau CG11: 5-06 viết "ít nhất khoảng $95$ lần", ghi chú 7-04 vẫn "khoảng 95 lần". | 7-04: "trong 100 lần huấn luyện có khoảng 95 lần …" | Thống nhất một cách viết trong deck (theo 5-06), chờ tác giả quyết đề xuất sửa ghi chú số 4. |
| nhẹ | L01-7-02 (dòng 3) | "ước lượng không chệch" dùng như động từ, câu đọc vấp. | "Với $h=A(S)$, $L_S(h)$ nói chung không ước lượng không chệch $L_D(h)$." | "Với $h=A(S)$, $L_S(h)$ nói chung không là ước lượng không chệch của $L_D(h)$." |
| nhẹ | L01-1-02 (mặt trang, ghi chú) | (T2) mới: câu thiếu chủ ngữ; ghi chú có chỉ dẫn phía trước ("định nghĩa ở phần sau"). | "$\ell$ không bị chặn thì cần rủi ro kì vọng hữu hạn."; ghi chú: "với rủi ro kì vọng $L_D$ định nghĩa ở phần sau" | Mặt trang: "khi $\ell$ không bị chặn, rủi ro kì vọng phải hữu hạn." Ghi chú: "điều kiện hữu hạn là $L_D(h)=\mathbb E_{Z\sim D}\ell(h,Z)<\infty$." |
| nhẹ | ghi chú L01-6-07; alt và `<desc>` của `can-co-mau.svg` (có từ bản đóng băng, không do biên tập) | So "$m=14$ và $6$ so với $30$" trộn hai $\epsilon$: $6$ ứng với $\epsilon=0{,}25$, còn $30$ là cận tại $\epsilon=0{,}1$; cận chung tại $\epsilon=0{,}25$ là $\lceil4\ln20\rceil=12$ ($4\ln20=11{,}98$). Câu "vì cận phải đúng cho mọi phân bố khả diễn" gán cả khoảng cách $6$–$30$ cho tính không phụ thuộc phân bố. | ghi chú 6-07: "cắt mức $\delta=0{,}05$ sớm hơn ($m=14$ và $6$ so với $30$), vì cận phải đúng cho mọi phân bố khả diễn" | Ghi chú: "đường $0{,}8^m$ cắt mức $0{,}05$ tại $m=14$, sớm hơn cận $30$ ở cùng $\epsilon=0{,}1$, vì cận phải đúng cho mọi phân bố khả diễn." Alt giữ ba số, có thể thêm "(cận cho $\epsilon=0{,}1$)". |
| nhẹ | L01-6-03 (bước 3), L01-5-12 (gạch đầu dòng 1) ở 390 px | Dấu câu sau công thức trong dòng rơi xuống một dòng riêng (".", ";"). | `recheck/check/narrow-043-L01-6-03*.png`, `narrow-039-L01-5-12.png` | Đưa dấu câu vào trong `$…$` ở hai chỗ này. |

Không thấy từ hoặc mẫu cấm của `no-ai-slop` (câu khẩu hiệu, câu hỏi tu từ, rào đón, "Đáp án", "minh họa", "Ký hiệu", "logarit", "Người học", "Trang này", nhãn ngoài danh sách) trong văn bản mới; các nhãn dùng đều thuộc danh sách hợp lệ.

## 6. Kết luận

Hai phát hiện nghiêm trọng và 29 phát hiện trung bình của năm báo cáo đã sửa đúng; 77/79 phát hiện nhẹ đã sửa, 2 sửa chưa đủ (mục 5, phát hiện 1 và 3); các điểm bác bỏ hoặc giữ nguyên theo quyết định của điều phối viên được tôn trọng. Mọi con số trên nội dung đổi tính lại đúng; phát biểu khớp ghi chú. Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 1 trung bình (nội dung chạm đáy khung ở 6-03, 2-04, 7-01, 6-05), 9 nhẹ.

**Kết luận: đạt khi sửa** (sửa phát hiện trung bình về bố cục đáy khung, chụp lại 1600×900 bốn trang; các phát hiện nhẹ tùy điều phối viên).
