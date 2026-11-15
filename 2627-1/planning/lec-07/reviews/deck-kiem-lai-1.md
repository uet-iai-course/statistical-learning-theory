# Kiểm lại sau biên tập, lượt 1 — deck Bài 07 (2026-11-16)

Vai: kiểm lại độc lập, chỉ đọc. Đối chiếu: bản đóng băng `master/frozen/` (thư mục nháp của phiên) với `2627-1/lecture-07-mang-no-ron-tham-so-hoa-thua.html`; năm báo cáo `reviews/deck-*.md`; quyết định trong `review-log.md` (mục "Năm báo cáo duyệt và quyết định của điều phối viên"); `storyboard.md` mục 17; `materials/lec-07/lecture-note.md` (Nhận xét 07.3 dòng 232, Hệ quả 07.16 dòng 777, Ví dụ 07.10(ii) dòng 924, Nhận xét 07.18 dòng 953, §10 dòng 990–1006); `lec-02/lecture-note.md` (T1)–(T4) dòng 95–98, Định lý 02.14 dòng 670.

Thư mục nháp: `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-07/recheck/` (`diff.txt` so từng trang, `shots/`, `sheets/`, `deck_check.txt`).

## 0. Kết luận

**Đạt khi sửa.** Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 2 trung bình (K1, K2), 13 nhẹ (K3–K15). Hai nhóm nghiêm trọng của năm báo cáo đã sửa đúng. Phạm vi thay đổi: 55 trang, 49 trang đổi (40 đổi mặt trang, 9 chỉ đổi ghi chú diễn giả); một SVG đổi (`ham-loi-doc.svg`, cỡ chữ 22 → 26).

## 1. Kiểm bằng máy (đã chạy)

| Kiểm | Kết quả |
|---|---|
| `deck_lint.py` | 0 phát hiện / 55 trang |
| `footer_check.py` (1600×900) | 0 trang chạm chân trang |
| `deck_check.py --shots` (40 trang đổi mặt trang) | console 0, pageerrors 0, failed 0, `.katex-error` 0. OVERFLOW ≤ 5 px ở các trang có `\sqrt` (báo động giả đã biết). NARROW-H ở 390 px: bảng và công thức hiển thị cuộn tại chỗ, có dấu "↔ cuộn ngang" (cách xử lý chung, CSS 3876170) |
| Ảnh 390×844 | đã xem cả 60 ảnh (40 trang + 20 ảnh `-end`) và 40 ảnh 1600×900 của mọi trang đổi mặt trang. 9 trang chỉ đổi ghi chú diễn giả: mặt trang không đổi, không chụp lại |
| Mật độ (đếm theo quy tắc của `deck_lint.py`) | trung vị 42 trang nội dung: 51 → 56. Có 14 trang ở mức 59–60 (mục 5) |

Ở 390 px không thấy chữ chồng lên nhau, không tràn ngang ngoài vùng cuộn, không mất nội dung ở ảnh `-end`. Các lỗi ngắt dòng nhìn thấy được ghi ở K10.

## 2. Phát hiện được chấp nhận → trạng thái

| Phát hiện (báo cáo) | Trang | Trạng thái | Bằng chứng |
|---|---|---|---|
| Nghiêm trọng (HV, MT P1): Định lý 02.14(a), $r_m$, (T4) chưa nhắc lại | 7-04, 7-05 | đã sửa | 7-04: "**Nhắc lại:** Định lý 02.14(a), (T1), (T3), (T4) lớp hữu hạn chọn trước: với xác suất ít nhất $1-\delta$, $\sup_h\lvert L_S(h)-L_D(h)\rvert\le r_m=\sqrt{\ln(2\lvert\mathcal H\rvert/\delta)/(2m)}$" khớp Định lý 02.14 ($K=\lvert\mathcal H\rvert$). Nhắc lại bỏ (T2) (hàm lỗi đo được), giống quy ước của 2-01; không ghi thành phát hiện. 7-05: "(T4) với $\lvert\mathcal H\rvert=3$" |
| Nghiêm trọng (CG): 3-02 "Diễn giải:" khái quát sai | 3-02 | đã sửa | "$1$, $2$, $4$, $8$ véc-tơ cho $0$, $1/4$, $1/3$, $1/2$; $\{0,1\}^3$ khớp mọi bộ dấu." Tính lại: $6/24$, $8/24$, $12/24$ đúng. Phản ví dụ $0{,}1\cdot\{0,1\}^3$ cho $0{,}05$ nằm ở ghi chú diễn giả |
| HV: 3-02 không có tám giá trị lớn nhất, phép chia 24 | 3-02 | đã sửa | Ghi chú diễn giả có hai dãy $-1,0,0,2,1,1,1,2$ (tổng 6) và $0,1,0,2,0,1,1,3$ (tổng 8). Đã liệt kê lại theo thứ tự bộ dấu: đúng |
| CG, TH: "lớp chứa mô hình" thay cho lớp hàm lỗi | 1-01, 7-03 | đã sửa | 1-01: "độ phức tạp Rademacher của lớp hàm lỗi bị chặn ứng với lớp chứa mô hình…". 7-03 viết "bị chặn trên lớp" (xem K12) |
| CG, HV, MT P2, SP: 7-03 thiếu phạm vi, "nó", dòng lớp tuyến tính thiếu xác suất và đại lượng | 7-03 | sửa chưa đủ | Đã có phạm vi, xác suất, công thức đủ và giới hạn $m=200$. Dòng 3 còn thiếu lượng từ "mọi $\lVert w\rVert\le B$" và "$B$, $\gamma$ chọn trước" (K1) |
| CG: 6-06 "không phụ thuộc số tham số" | 6-06 | đã sửa | Đúng câu của quyết định. Ghi chú diễn giả có "$\tilde O$ ẩn thừa số lôgarit". Xem thêm K13 |
| TH: 7-06 câu 3 thiếu (T1), "$B$, $\gamma$ chọn trước" | 7-06 | đã sửa | Đáp số $0{,}04+0{,}16+3\sqrt{\ln40/5000}=0{,}2815$ đúng. Biên tập đồng thời bỏ "để chặn rủi ro 0–1" ở câu 4 (K11) |
| SP, MT P3: số hiệu Ví dụ trên trang nguồn | 2-10, 2-11, 3-02, 3-05, 4-04, 6-01, 6-03, 6-04, 6-05 | đã sửa | Có "Ví dụ 07.2" … "07.11"; 3-06 dẫn "(Ví dụ 07.4)" và 3-02 mang số hiệu đó. Nhãn đặt trong gạch đầu dòng ở 2-10, 2-11, 3-05, 6-01, 6-03…6-05 (K15) |
| MT P4: câu nối 2-07 → 2-08 | 2-08 | sửa chưa đủ | Mặt trang thêm "Số tham số là thước đo đầu tiên của lớp." Vế "số hạng $2r$ đo năng lực thống kê" mà MT đề xuất chỉ nằm ở ghi chú diễn giả (K6) |
| MT P5: câu nối 2 → 3 | 3-01 | đã sửa | "Hàm giá trị thực cần đại lượng thay chiều VC, nhỏ đi khi bị chặn theo chuẩn." Chủ ngữ của "nhỏ đi" chưa rõ (K8) |
| MT P6: 2-01 vì sao cận Bài 06 không dùng được | 2-01 | đã sửa | Mặt trang có "không cần tính lồi, khác Bài 05–06"; lý do (hàm lỗi không lồi theo tham số) ở ghi chú diễn giả |
| SP: 2-06 "ba năng lực" gồm tối ưu | 2-06 | đã sửa | Tiêu đề "Ba câu hỏi về một lớp mạng"; các hàng khớp `thuat-ngu.md`. Nhận xét 07.3 mất "mọi" (K2) |
| SP: 2-09 hệ quả của $B=\lVert\hat\theta\rVert$ | 2-09 | đã sửa | "lấy $B=\lVert\hat\theta\rVert$ thì lớp phụ thuộc $S$, trái (T5)" |
| SP: 3-03 "Trực quan." cơ chế | 3-03 | đã sửa | "Lớp chọn, với mỗi bộ nhãn ngẫu nhiên, hàm sai ít nhất." |
| HV, SP: 5-03 "Lưu ý:" | 5-03 | đã sửa | $\tfrac13\mathbb E\lvert\sigma_1+\sigma_2+\sigma_3\rvert=0{,}5$ đúng |
| SP: 6-03 "Diễn giải:" chiều so sánh | 6-03 | đã sửa | "chuẩn trung bình với nhãn hoán vị gấp $10\,853/916\approx11{,}85$ lần với nhãn thật". $10853/916=11{,}848$ |
| HV: 1-02 kí hiệu; MT P8 $d$ | 1-02 | đã sửa | $\Pi_{\mathcal H}$, $d(\cdot)$, $\tilde h$, $L^*$ có trên mặt trang. Tên của (M) đã bị bỏ khỏi 1-02 (K3) |
| HV: dòng > 20 âm tiết | 2-04, 2-06, 3-06, 4-05 | đã sửa | Đã tách dòng. Dòng 21–23 âm tiết ở 2-01, 7-03, 7-04 được giữ có lý do |
| Bảng ở 390 px | 1-06, 3-02, … | đã xử lý chung | CSS cuộn tại chỗ, có dấu "↔ cuộn ngang" (quyết định của điều phối viên) |
| Phát hiện nhẹ, mục 17.3 (≈ 50 dòng) | nhiều trang | đã sửa, trừ 4 mục dưới | Đã đối chiếu từng trang với `diff.txt` |
| Không sửa: Mục tiêu 5 (SP nhẹ) | 1-03 | chấp nhận lý do | Trang ở mức 79/80; viết đủ ba ý "vì sao" vượt trần. Ba ý có ở ghi chú diễn giả |
| Không sửa: 5-03 "Trực quan." (HV nhẹ) | 5-03 | chấp nhận lý do | 59/60; cơ chế (Phụ lục B) ở ghi chú diễn giả |
| Không sửa: "score function" ở 1-06, "ERM" ở 7-04 (SP nhẹ) | 1-06, 7-04 | chấp nhận lý do | "score function" có ở 2-01; ERM là chữ viết tắt dùng từ Bài 01 |
| Sửa một phần: 6-06 $\mu_\Theta$, $\hat y_\Theta$, $\lVert\cdot\rVert_{2,1}$, $\tilde O$ (HV nhẹ) | 6-06 | sửa chưa đủ | $\mu_\Theta$ có trên mặt trang. $\hat y_\Theta$ bị bỏ khỏi mặt trang và $\lvert\mathcal Y\rvert$ là kí hiệu mới (K13) |

## 3. Toán trên nội dung đã đổi (đã tính lại)

- 3-04 bước 1–2: với $\sigma_i=2\tau_i-1$ và $h_i\in\{0,1\}$, $\sigma_ih_i=\tau_i-\mathbb 1[h_i\ne\tau_i]$ đúng ở cả bốn trường hợp. Do đó $\sup_h\frac1m\sum_i\sigma_ih_i=\frac1m\sum_i\tau_i-\min_h\operatorname{err}_\tau(h)$, khớp dòng mới.
- 4-03 bước 2: $\mathbb E\Psi\le\mathbb E\sup_g\frac1m\sum_i\sigma_i(g(Z'_i)-g(Z_i))\le2\mathfrak R_m(\mathcal G)$ đúng. Bước 4: $t=\sqrt{\ln(2/\delta)/(2m)}$ ứng với $\delta/2$ và $c_i=1/m$; $\Psi\le2\mathfrak R_m+t\le2\widehat{\mathfrak R}_S+3t$ đúng.
- 4-05: $3\sqrt{\ln40/400}=0{,}28810\le0{,}2881$; $\sqrt{\ln20/400}=0{,}08654\le0{,}0866$; tỉ số $3{,}33$. Đúng.
- 5-02: $p=1$, $m=2$, $x_1=x_2=1$ cho $\widehat{\mathfrak R}=B/2$ và cận $B/\sqrt2=0{,}7071B$. Đúng.
- 6-01: $3\sqrt{\ln40/2}=4{,}0743$; $m$ ứng với ba cột là $57\,958$, $231\,829$, $3690$; $3\sqrt{\ln40/(2\cdot10^4)}=0{,}04074\le0{,}0408$. Đúng.
- 6-04: Hệ quả 02.10(b) với $n=5000$ cho $\sqrt{\ln40/10^4}=0{,}01921\le0{,}0193$, khớp ghi chú dòng 924.
- 7-03 dòng 3: công thức khớp Hệ quả 07.16 (ghi chú dòng 790), nhưng thiếu lượng từ (K1).
- 7-05: $\sqrt{\ln120/400}=0{,}1094\le0{,}1095$; $P/m=5000$ và $0{,}005$. Đúng.
- 7-06 câu 3: $0{,}2815$ đúng.
- 2-06 Nhận xét 07.3: ghi chú viết "**mọi** hàm Lipschitz … được xấp xỉ đều …, **với** số nơ-ron tăng theo hàm mũ". Deck viết "xấp xỉ đều hàm Lipschitz …, **cần** số nơ-ron mũ theo $p$". Chữ "cần" theo đề xuất của CG và đề xuất sửa ghi chú (UML Định lý 20.5 là cận dưới), điều phối viên đã ghi cho tác giả. Việc bỏ "mọi" là lỗi mới (K2).
- 4-02, ghi chú diễn giả: "(b) đổi sang độ phức tạp thực nghiệm … với giá thêm số hạng $2\sqrt{\ln(2/\delta)/(2m)}$". Câu này so (b) với mốc trung gian $2\mathfrak R_m+t$ chứ không so với (a), vì (a) là phát biểu theo kì vọng (K14).

## 4. Mạch truyện: các trang đổi ±2 và ranh giới mạch

- 1-01 → 1-06: luận điểm bìa vẫn một câu, có điều kiện. 1-05 (chỉ đổi ghi chú diễn giả) thêm "kì vọng của lỗi nhỏ nhất", khớp Mệnh đề 07.9(a).
- Mạch 2: 2-00 → 2-01 → 2-02 liền mạch. Ở 2-05 → 2-06 → 2-07, tiêu đề "Ba câu hỏi" khớp mục tiêu 1 ở 1-03. Ranh giới hai cụm 2-07 → 2-08 còn yếu (K6).
- Ranh giới 2 → 3 (2-11 → 3-00 → 3-01) đạt; xem K8. Ranh giới 3 → 4: dòng dẫn 4-00 đủ "bị chặn, chọn trước". Ranh giới 4 → 5 không đổi.
- Ranh giới 5 → 6: 6-00 (ghi chú) và 6-01 "Bảo đảm cho câu hỏi phân lớp văn bản" nối ngược về 2-02 trên mặt trang. 6-05 có "Kết luận:" và dẫn Bổ đề 07.8.
- Ranh giới 6 → 7: 7-02 "Đọc thêm" chỉ còn Nhận xét 07.18. 7-03 trả lời câu hỏi trung tâm; dòng 1 vẫn là cụm danh từ và dòng 2 chỉ về nó bằng "đại lượng này", đọc được. 7-04 → 7-05 có "Nhắc lại:" trước công thức dùng nó. 7-06 xem K11.

## 5. Phát hiện mới hoặc còn mở

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L07-7-03 | K1. Dòng rút gọn của Hệ quả 07.16 bỏ lượng từ cấp lớp "mọi $\lVert w\rVert\le B$" và giả thiết "$B$, $\gamma$ chọn trước", là hai điều kiện mà 6-02 và 6-04 cho thấy là thiết yếu. Ngoài ra $L^{<\gamma}_S$ thiếu đối số $(h_w)$. Quy định: phát biểu rút gọn không bỏ lượng từ, giả thiết | 7-03: "Lớp tuyến tính, lớp ẩn cố định, xác suất $\ge1-\delta$: $L_D(h_{w,0})\le L^{<\gamma}_S+\dots$". Ghi chú dòng 789: "đồng thời cho mọi $w$ với $\lVert w\rVert\le B$"; 7-02 viết đủ | "Lớp ẩn cố định, $B,\gamma$ chọn trước, xác suất $\ge1-\delta$, $\forall\lVert w\rVert\le B$: $L_D(h_{w,0})\le L^{<\gamma}_S(h_w)+\dots$, không chứa $p$." (bỏ "Lớp tuyến tính,", vì lớp ẩn cố định đã xác định lớp). Dòng 4: "…; không giải thích chuẩn nhỏ" (bỏ chữ "cận" thứ hai). Mật độ 59 → 57 |
| trung bình | L07-2-06 | K2. Nhận xét 07.3 mất lượng từ "mọi". Câu chỉ còn vế cận dưới, mất phát biểu xấp xỉ phổ quát mà dòng cuối ("chỉ chặn số hạng đầu") dùng. Ở 1600×900, dấu phẩy sau $\epsilon$ rơi xuống đầu dòng sau | "Mạng sigmoid xấp xỉ đều hàm Lipschitz $[-1,1]^p\to[-1,1]$ tới sai số $\epsilon$, cần số nơ-ron mũ theo $p$." Ghi chú dòng 234: "mọi hàm Lipschitz … được xấp xỉ đều tới sai số $\epsilon>0$" | "Mạng sigmoid xấp xỉ đều mọi hàm Lipschitz $[-1,1]^p\to[-1,1]$ tới sai số $\epsilon$; số nơ-ron cần thiết mũ theo $p$." Để giữ 60: dòng cuối viết "Kết quả này chỉ chặn số hạng đầu." và chuyển "(universal approximation)" lên tiêu đề khối "Nhận xét 07.3 (xấp xỉ phổ quát, universal approximation)." Đếm lại |
| nhẹ | L07-1-02 | K3. (M) mất tên trên mặt trang. 1-02 đứng trước 2-01, nơi (M) được đặt tên, nên kí hiệu xuất hiện trước khi được giải nghĩa. Bản đóng băng có tên này | Đóng băng: "(M) lớp con đếm được"; bản sửa: "(T5), (M): với xác suất…" | Ghi lại "(M) lớp con đếm được"; bù bằng "Định lý 03.15, (T1), …" (bỏ "với") và "Mệnh đề 04.3, $S$ $r$-đại diện:" (bỏ "khi", "là"). Mật độ ≈ 60 |
| nhẹ | L07-1-06 | K4. "rút ngẫu nhiên" thay "cố định": mặt trang không còn nói lớp ẩn giữ cố định, không huấn luyện. Điều này là phạm vi của 7-03 ("lớp ẩn cố định") | "$N=2000$ ReLU (rectified linear unit) $\psi_j$ rút ngẫu nhiên." | "$N=2000$ nơ-ron ReLU (rectified linear unit) $\psi_j$ rút ngẫu nhiên rồi cố định." Nếu vượt 60, rút dòng nhãn hoán vị thành "Nhãn hoán vị (permuted labels) của tập huấn luyện." |
| nhẹ | L07-2-07 | K5. Kí hiệu thiếu đối số trong lời giải mới | "…$=0$ vì $f_\theta=\tilde y_i/2$ tại bốn điểm." | "vì $f_\theta(x_i)=\tilde y_i/2$, $i=1,\ldots,4$." |
| nhẹ | L07-2-08 | K6. Câu nối MT P4 mới có một vế. "Hai khái niệm" ở dòng cuối không có tiền ngữ gần | "Số tham số là thước đo đầu tiên của lớp."; "Hai khái niệm không kéo theo nhau." | "Thước đo đầu tiên cho số hạng $2r$ là số tham số." (+2, tức 60); dòng cuối: "Tham số hóa thừa và nội suy không kéo theo nhau." (bù bằng cách bỏ "(iii)": "lớp $p$ tham số, ba hàm") |
| nhẹ | L07-2-09 | K7. Thiếu giới từ | "trái (T5)" | "trái với (T5)" |
| nhẹ | L07-3-01 | K8. Chủ ngữ của "nhỏ đi" và đối tượng "bị chặn" chưa rõ (no-ai-slop Detect: chủ ngữ mờ) | "Hàm giá trị thực cần đại lượng thay chiều VC, nhỏ đi khi bị chặn theo chuẩn." | "Lớp hàm giá trị thực cần một đại lượng thay chiều VC; đại lượng này nhỏ đi khi lớp bị chặn theo chuẩn." (+5, tức 63). Bù bằng "Trực quan. Mỗi bộ dấu: chọn hàm tương quan nhất, rồi lấy trung bình." (−1) và bỏ "là độ phức tạp" ở một trong hai vế định nghĩa, viết "($\widehat{\mathfrak R}_S$ thực nghiệm, empirical; $\mathfrak R_m$ tổng thể, population)" |
| nhẹ | L07-4-05 | K9. Câu hỏi tách thành mảnh câu mở bằng giới từ, có dấu chấm phẩy | "So với Hệ quả 02.10(c); bước nào làm cận yếu hơn?" | "So sánh với Hệ quả 02.10(c). Bước nào làm cận yếu hơn?" |
| nhẹ | L07-4-03, L07-2-06, L07-4-01 | K10. Dấu câu rơi xuống đầu dòng khi công thức ngắt dòng. 4-03 do gộp công thức hiển thị vào bước 4. Ở 4-01, 2-01, lỗi này có từ trước | 4-03 (1600×900 và 390 px): dòng mở bằng ":Ψ ≤ 2ℜ_m + t …"; 2-06: ", cần số nơ-ron…"; 4-01: ";đuôi dưới cũng vậy." | 4-03: "… $t=\sqrt{\ln(2/\delta)/(2m)}$, nên $\Psi\le2\mathfrak R_m+t\le2\widehat{\mathfrak R}_S+3t$." (chữ "nên" ngắt dòng gọn hơn dấu hai chấm). 4-01: "…$\big)$. Đuôi dưới cũng vậy." 2-06: xem K2 |
| nhẹ | L07-7-06 | K11. Câu 4 bỏ "để chặn rủi ro 0–1". 6-05 cho thấy Định lý 07.11 áp dụng được cho lớp điểm số dịch $\tfrac12$ để chặn trung bình điểm số, nên câu hỏi mất trọng tâm. Trang hiện ở mức 52 | "vì sao không đặt $2\cdot0{,}04$ vào Định lý 07.11?" | Khôi phục: "… vào Định lý 07.11 để chặn rủi ro 0–1?" (57) |
| nhẹ | L07-7-03 | K12. "bị chặn trên lớp" đọc thành "bị chặn trên" (bounded above). 1-01 viết "ứng với lớp" | "Độ phức tạp Rademacher của lớp hàm lỗi bị chặn trên lớp chọn trước chứa mô hình…" | "… của lớp hàm lỗi bị chặn ứng với lớp chọn trước chứa …" (+1; bù bằng đề xuất ở K1) |
| nhẹ | L07-6-06 | K13. Mặt trang dùng $\hat y_\Theta$ và $\lvert\mathcal Y\rvert$ chưa giải nghĩa. $\lvert\mathcal Y\rvert$ là mới; bản đóng băng viết "số nhãn". Câu cuối nói độ rộng vào cận qua $R_\Theta$, trong khi độ rộng còn vào trực tiếp qua $\ln\bar N$ | "$\bar N=\max\{p,\lvert\mathcal Y\rvert,N_j\}$"; "$\Pr[\hat y_\Theta(x)\ne y]$"; ghi chú dòng 957 định nghĩa $\hat y_\Theta$, $\lvert\mathcal Y\rvert$ | "Kí hiệu: … $\bar N$ lớn nhất trong $p$, số nhãn, các $N_j$; $\hat y_\Theta$ nhãn dự đoán." Trang đang 44, còn chỗ cho số âm tiết; chạy lại `footer_check.py` vì ảnh 1600×900 đã sát chân trang. Câu cuối: "…; độ sâu, độ rộng vào cận qua $R_\Theta$ và $\ln\bar N$." |
| nhẹ | L07-4-02 (ghi chú diễn giả) | K14. So sánh (a) với (b) không chính xác: (a) là phát biểu theo kì vọng; $2t$ là giá của việc đổi $\mathfrak R_m$ thành $\widehat{\mathfrak R}_S$ tính từ mốc $2\mathfrak R_m+t$ | "(b) đổi sang độ phức tạp thực nghiệm, tính được từ tập huấn luyện, với giá thêm số hạng $2\sqrt{\ln(2/\delta)/(2m)}$." | "(b) là bảo đảm xác suất cao với độ phức tạp thực nghiệm, tính được từ tập huấn luyện; số hạng tin cậy $3t$ gồm $t$ cho độ lệch của $\Psi$ và $2t$ cho phép đổi $\mathfrak R_m$ thành $\widehat{\mathfrak R}_S$." |
| nhẹ | L07-2-10, L07-2-11, L07-3-05, L07-6-01, L07-6-03, L07-6-04, L07-6-05 | K15. Nhãn "**Ví dụ 07.k.**" nằm trong gạch đầu dòng thứ nhất, nên đọc như một ý của danh sách. Các trang khác (3-02, 4-04, 5-02) đặt nhãn ở đầu đoạn. Ở 6-03, "hai khoảng không giao nhau" không nói khoảng nào, vì bảng có hai cột khoảng | 2-10: "• **Ví dụ 07.2.** Mạng của Mệnh đề 07.2; …"; 6-03: "…; hai khoảng không giao nhau." | Đặt nhãn thành một `<p>` trước `<ul>`, hoặc giữ nguyên nếu bố cục chung của Bài 06 cũng làm vậy. 6-03: "hai khoảng chuẩn không giao nhau" (+1) |

Kiểm `no-ai-slop` (chế độ Detect) trên văn bản mới, cả mặt trang và ghi chú diễn giả: không có từ cấm, không có câu hỏi tu từ, không có câu khẩu hiệu. Có ba mẫu ở mức nhẹ, đã ghi ở K8 và K6 (chủ ngữ hoặc tiền ngữ mờ), và một mẫu tương phản nhị phân ở 6-05 "Kết luận: Định lý 07.11 cần lớp hàm lỗi trong $[0,1]$, không phải lớp điểm số". Mẫu sau chấp nhận được vì phủ định ở đây là nội dung toán học: lớp điểm số vi phạm (T3). Ghi chú diễn giả mới (4-02 "95 trên 100 lần", 6-06, 7-08) đi thẳng vào ý, không có câu nguồn gốc. Ở 7-07, "Bài tập 07.7–07.9 lấy từ UML §20.9" là dẫn nguồn của bài tập; giữ.

## 6. Mật độ: đề xuất cắt cho các trang 59–60

Trung vị 56 (đóng băng 51). Phần tăng đến chủ yếu từ các sửa bắt buộc: thêm Ví dụ số hiệu, nhắc lại và phạm vi. Đề xuất bên dưới không bỏ kết quả, giả thiết hay số nào.

| Trang | Hiện | Đề xuất cắt cụ thể | Sau |
|---|---:|---|---:|
| 1-02 | 59 | xem K3 (thêm tên (M), bỏ "với", "khi", "là") | ≈ 60 |
| 1-06 | 60 | "Nhãn hoán vị (permuted labels): hoán vị nhãn huấn luyện." → "Nhãn hoán vị (permuted labels) của tập huấn luyện." | 59 |
| 2-01 | 59 | "Cần chặn $\sup\ldots$ và rủi ro của đầu ra $A(S;\xi)$ của thuật toán bất kì." → "Cần chặn $\sup\ldots$ cho đầu ra $A(S;\xi)$ của mọi thuật toán." | 56 |
| 2-02 | 60 | "Tỉ lệ lỗi của $h_{w,0}$ có bảo đảm nào?" → "Bảo đảm nào cho $L_D(h_{w,0})$?" | 56 |
| 2-06 | 60 | xem K2 | ≈ 60 |
| 2-10 | 60 | "Diễn giải:" → "chuẩn tham số $\sqrt{10{,}25}\approx3{,}20$ hay $\sqrt{500{,}30}\approx22{,}37$ cho cùng một hàm, nên không xác định từ hàm; tích chuẩn phổ không đổi." | 57 |
| 3-03 | 60 | Không cắt được mà không mất (b) hoặc "Trực quan." mới. Giữ; mức này đã có trước khi sửa | 60 |
| 4-01 | 59 | "…không là trung bình: bất đẳng thức Hoeffding không áp dụng." → "…không là trung bình, nên Hoeffding không áp dụng." | 57 |
| 4-02 | 59 | Bỏ "; lớp một phần tử: $\widehat{\mathfrak R}_S=0$" khỏi "Trực quan." (4-05 xét đúng trường hợp này) | 55 |
| 5-03 | 59 | Giữ. "Lưu ý:" vừa được viết đủ theo HV, SP | 59 |
| 6-03 | 60 | "$C_x$ từ $1{,}518$ đến $1{,}544$" → "$C_x\in[1{,}518;\,1{,}544]$" | 58 |
| 6-04 | 60 | "$B$ chọn theo $S$ nên cần lưới $B_k=2^k\ge\lVert\hat w\rVert$ (Nhận xét 07.17), số hạng còn lớn hơn." → "Chọn $B$ theo $S$ cần lưới $B_k=2^k\ge\lVert\hat w\rVert$ (Nhận xét 07.17): số hạng còn lớn hơn." | 58 |
| 7-03 | 59 | xem K1, K12 | ≈ 58 |
| 7-04 | 60 | (c): bỏ "với $\delta=0{,}05$" vì (b) đã cho $\delta$: "vế phải Định lý 07.11(b) cho nghiệm ERM, nhãn bất kì" | 59 |

Áp dụng hết các đề xuất này đưa trung vị về khoảng 55. Muốn về gần 52 phải chuyển một dòng ở các trang 57–58 (2-08, 2-09, 3-01, 6-05, 7-05) sang ghi chú diễn giả. Việc này do điều phối viên quyết.
