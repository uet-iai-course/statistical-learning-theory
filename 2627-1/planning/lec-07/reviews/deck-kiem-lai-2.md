# Kiểm lại sau biên tập, lượt 2 — deck Bài 07 (2026-11-16)

Vai: kiểm lại, chỉ đọc. Đối chiếu bản trước lượt 2 (`editor/before-round2.html` trong thư mục nháp của phiên) với `2627-1/lecture-07-mang-no-ron-tham-so-hoa-thua.html`; `storyboard.md` mục 17.5; `reviews/deck-kiem-lai-1.md`. Thư mục nháp: `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-07/recheck2/` (`diff.txt`, `shots/`, `sheets/`, `deck_check.txt`).

## 0. Kết luận

**Đạt.** Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 0 trung bình, 5 nhẹ (N1–N5). Không mục nào trong năm mục này chặn việc bàn giao. Sửa chúng xong chỉ cần xem lại ảnh của các trang 2-01, 2-08, 7-03, 1-06, 4-01, 7-06.

Ba trong năm phát hiện nhẹ (N1, N2, N3) sinh ra từ chính các câu đề xuất của báo cáo lượt 1 (K6, mục 6 cắt mật độ cho 2-01, K1). Người sửa đã áp dụng đúng nguyên văn các câu đó.

## 1. Kiểm bằng máy (đã chạy)

| Kiểm | Kết quả |
|---|---|
| `deck_lint.py` | 0 phát hiện / 55 trang |
| `footer_check.py` | 0 trang chạm chân trang |
| `deck_check.py --shots` (20 trang đổi) | console 0, pageerrors 0, failed 0, `.katex-error` 0. OVERFLOW ≤ 5 px chỉ ở các trang có `\sqrt` |
| Ảnh | đã xem 20 ảnh 1600×900 và 31 ảnh 390×844 (có ảnh `-end`), gồm cả 4-03 ở hai cỡ |
| Mật độ | 20 trang đổi đều ≤ 60. Trung vị 42 trang nội dung: 56 → 55 |

4-03 (bước 4 sau lần sửa cuối) ở 1600×900 nằm gọn trong khung, dòng bước 4 kết thúc bằng "với $t=\sqrt{\ln(2/\delta)/(2m)}$.". Ở 390 px, ảnh `-end` hiện đủ bốn bước và không có dấu câu ở đầu dòng.

## 2. K1–K15 → trạng thái

| Phát hiện | Trang | Trạng thái | Bằng chứng |
|---|---|---|---|
| K1 | 7-03 | đã sửa | "Lớp ẩn cố định, $B,\gamma$ chọn trước, xác suất $\ge1-\delta$, $\forall\lVert w\rVert\le B$: $L_D(h_{w,0})\le L^{<\gamma}_S(h_w)+\frac{2BC_x}{\gamma\sqrt m}+3\sqrt{\ln(2/\delta)/(2m)}$, không chứa $p$". Khớp Hệ quả 07.16. Xem N3 |
| K2 | 2-06 | đã sửa | "xấp xỉ đều mọi hàm Lipschitz …, sai số $\epsilon$; cần số nơ-ron mũ theo $p$". Ở 1600×900 không còn dấu phẩy rơi dòng. Tiêu đề cột "Mệnh đề 04.3" (người sửa tự quyết) chấp nhận được: các ô là tên số hạng, và dòng dưới bảng nói "số hạng đầu" |
| K3 | 1-02 | đã sửa | "(M) lớp con đếm được". Giả thiết của Định lý 03.15 còn đủ |
| K4 | 1-06 | đã sửa | "rút ngẫu nhiên rồi cố định". Tiêu đề cột "Lỗi kiểm tra" (tự quyết) chấp nhận được, vì ghi chú diễn giả nói rõ là trung bình qua mười hạt giống. Xem N4 |
| K5 | 2-07 | đã sửa | "$f_\theta(x_i)=\tilde y_i/2$, $i=1,\ldots,4$" |
| K6 | 2-08 | đã sửa; có lỗi mới N1 | "Thước đo đầu tiên cho số hạng $2r$ là số tham số."; "Tham số hóa thừa và nội suy không kéo theo nhau." |
| K7 | 2-09 | đã sửa | "trái với (T5)" |
| K8 | 3-01 | đã sửa | "Lớp hàm giá trị thực cần một đại lượng thay chiều VC; đại lượng này nhỏ đi khi lớp bị chặn theo chuẩn." Dòng tên hai độ phức tạp còn đủ tiếng Anh |
| K9 | 4-05 | đã sửa | "So sánh với Hệ quả 02.10(c). Bước nào làm cận yếu hơn?" |
| K10 | 4-03, 4-01 | 4-03 đã sửa; 4-01 sửa chưa đủ (N5) | 4-03: ổn ở cả hai cỡ. 4-01: ở 390 px, dòng mở bằng ". Đuôi dưới cũng vậy." |
| K11 | 7-06 | đã sửa | "… để chặn rủi ro 0–1?" Xem N5 (ngắt dòng trong "0–1" ở 390 px) |
| K12 | 7-03 | đã sửa | "bị chặn ứng với lớp chọn trước" |
| K13 | 6-06 | đã sửa | "$\bar N$ lớn nhất trong $p$, số nhãn, các $N_j$; $\hat y_\Theta$ nhãn dự đoán"; "… qua $R_\Theta$ và $\ln\bar N$". Ở 1600×900 dòng cuối nằm sát chân trang nhưng `footer_check.py` báo 0 |
| K14 | ghi chú 4-02 | đã sửa | "$3t$ … gồm $t$ cho độ lệch của $\Psi$ và $2t$ cho phép đổi $\mathfrak R_m$ thành $\widehat{\mathfrak R}_S$", khớp bước 4 của 4-03 |
| K15 | 6-03 | đã sửa; phần nhãn: chấp nhận lý do | "hai khoảng chuẩn không giao nhau". Nhãn "Ví dụ 07.k." để trong gạch đầu dòng vì thêm `<p>` sẽ vượt 6 dòng |
| Cắt mật độ | 1-06, 2-01, 2-02, 2-10, 4-01, 4-02, 6-03, 6-04, 7-04 | đã áp dụng | Không mất giả thiết hay số nào. 4-02 bỏ "lớp một phần tử", vì 4-05 xét trường hợp này. 7-04 (c) bỏ "$\delta=0{,}05$", vì (b) ngay trên đã cho. Hai chỗ cắt làm đổi nghĩa: N2 (2-01), N3 (7-03) |

## 3. Toán và mạch truyện trên các trang đổi ±2

- **Toán:** không có số mới. Các công thức đổi khớp ghi chú:
  - 7-03 khớp Hệ quả 07.16.
  - Ghi chú diễn giả 4-02 khớp chứng minh Định lý 07.11 ($\Psi\le2\mathfrak R_m+t\le2\widehat{\mathfrak R}_S+3t$).
  - 6-03: $C_x\in[1{,}518;\,1{,}544]$ khớp dữ liệu cũ.
  - 6-06: $\bar N$ và $\hat y_\Theta$ khớp Nhận xét 07.18 (ghi chú dòng 957).
- **Mạch truyện:**
  - 2-06 → 2-07 → 2-08: nối được ("Thước đo đầu tiên cho số hạng $2r$ …" đứng sau bảng có hàng "năng lực thống kê | $2r$").
  - 2-08 → 7-04: mất mốc "(iii)" (N1).
  - Ranh giới 2→3, 3→4, 6→7 không đổi so với lượt 1.
  - 7-02 → 7-03 → 7-04 liền mạch.

## 4. Phát hiện còn mở

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | L07-2-08 | N1. Câu bù mật độ bỏ nhãn "(iii)". Nhãn này là mốc cho "Nhận xét 03.10(iii)" ở 7-04 (bài tập tổng hợp), nên 7-04 mất chỗ dựa trên mặt trang. Ngoài ra "$\mathcal H_{\sin}$ có $P=1$" dùng $P$ trước Định nghĩa 07.4 ở dòng dưới. Lỗi xuất phát từ đề xuất K6 của báo cáo lượt 1 | "Nhắc lại: Nhận xét 03.10, $\mathcal H_{\sin}$ có $P=1$, $d=\infty$; lớp $p$ tham số, ba hàm."; 7-04: "(b) Nhận xét 03.10(iii), $p=10^6$ tham số" | Đưa dòng "Nhắc lại:" xuống sau Định nghĩa 07.4 (khi đó $P$ đã được định nghĩa) và ghi lại "lớp (iii) $p$ tham số, ba hàm". Bù 1 âm tiết bằng câu mở "Thước đo đầu tiên cho số hạng $2r$: số tham số." (bỏ "là"). Mật độ 60 |
| nhẹ | L07-2-01 | N2. Câu đã cắt gán cận trên đúng theo lớp cho "đầu ra", sai quan hệ: $\sup_h$ chặn cho mọi $h$, rồi suy ra cận cho đầu ra. Câu xuất phát từ đề xuất cắt mật độ ở báo cáo lượt 1 | "Cần chặn $\sup_{h\in\mathcal H}\big(L_D(h)-L_S(h)\big)$ cho đầu ra $A(S;\xi)$ của mọi thuật toán." | "Cần chặn $\sup_{h\in\mathcal H}\big(L_D(h)-L_S(h)\big)$; cận này chặn cả rủi ro của đầu ra $A(S;\xi)$ của mọi thuật toán." (55 → khoảng 60) |
| nhẹ | L07-7-03 | N3. Bỏ chữ "cận" thứ hai (đề xuất K1) khiến vế sau mất chủ ngữ | "Ở $m=200$ cận $>1$, lỗi báo trên tập kiểm tra; không giải thích chuẩn nhỏ." | Ghi lại "…; cận không giải thích chuẩn nhỏ." (58 → 59) |
| nhẹ | L07-1-06 | N4. Dấu phẩy thay "với" làm mất quan hệ ràng buộc: nghiệm là chuẩn nhỏ nhất *trong số các $w$ thỏa* $f(x_i)=2y_i-1$ | "$\lVert w\rVert$ nhỏ nhất, $f(x_i)=2y_i-1$." | "$\lVert w\rVert$ nhỏ nhất thỏa $f(x_i)=2y_i-1$"; bù bằng "$\psi_j$ rút ngẫu nhiên, cố định" (bỏ "rồi"). Mật độ 60 |
| nhẹ | L07-4-01, L07-7-06 | N5. Ở 390 px, dấu câu đứng đầu dòng và "0–1" bị ngắt giữa | 4-01 (390 px): ". Đuôi dưới cũng vậy."; 7-06 câu 4: "rủi ro 0–" / "1?" | 4-01: đưa dấu chấm vào KaTeX (`…\big).$`) hoặc viết "…$\big)$; đuôi dưới cũng vậy" trong cùng mệnh đề. 7-06: viết "0‑1" với dấu nối không ngắt (U+2011), hoặc bọc "0–1" trong `<span style="white-space:nowrap">`, theo cách deck đang dùng cho "0–1" ở trang khác |

Kiểm `no-ai-slop` (chế độ Detect) trên văn bản đổi ở lượt 2: không có từ cấm, câu hỏi tu từ hay câu khẩu hiệu. Chủ ngữ mờ ghi ở N3. Câu "Kết quả chỉ chặn số hạng đầu." ở 2-06 có tiền ngữ là Nhận xét 07.3 ở ngay trên bảng; giữ.
