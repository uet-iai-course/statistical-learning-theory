# Kiểm lại sau biên tập deck Bài 06 — lượt 2 (chỉ đọc)

Vai: kiểm lại (general-purpose, Opus 5.5), cùng tác tử lượt 1. Ngày 2026-11-16. Đầu vào: deck hiện tại so với trạng thái lượt 1 (bản chép chữ `lec-06/recheck/after.txt` so với `after2.txt`, diff `recheck/r2.diff`), bảng "Lượt 2" ở mục 17 của `storyboard.md`, báo cáo `deck-kiem-lai-1.md`. `no-ai-slop` chế độ Detect cho câu mới.

## 0. Kiểm máy

| Công cụ | Kết quả |
|---|---|
| `deck_lint.py` | **0** phát hiện trên 55 trang |
| `footer_check.py` | 0 trang |
| `deck_check.py --shots` (`recheck/check2/`) | slides=55, console 0, pageerrors 0, failed 0, `.katex-error` 0; tập trang OVERFLOW trùng lượt 1 (chỉ trang có `\sqrt`, báo động giả đã biết); SYLL chỉ ở 1-01 (bìa) và 7-02 (65, trần 80) |
| Mật độ | trung vị 55 (lượt 1: 56); không trang nội dung nào trên 60; 59: 4-02, 7-03; 57–58: 1-02, 1-06, 2-01, 3-02, 4-01, 4-05, 4-07, 5-01, 6-05, 7-04 |
| Ảnh đã xem | 1600×900 và 390×844 (cả `-end`) của 2-08, 2-11, 2-12, 3-01, 3-03, 7-03 (`recheck/s2w-wide-01.png`, `recheck/s2n-narrow-01.png`): không tràn, không chồng chữ; công thức và bảng rộng cuộn tại chỗ ở 390 px |

## 1. K1–K16

| Mã | Trạng thái | Bằng chứng |
|---|---|---|
| K1 7-03 dòng chính quy hóa | đã sửa | "ERM có chính quy hóa, $\ell$ lồi, không âm, (L), (T1), $\lambda^*$ chọn trước: $\mathbb E_SL_D(\hat w_S)-\inf_{W_B}L_D\le2GB/\sqrt m$" — khớp Hệ quả 06.13(c) và hàng 7-02; câu dẫn kết bằng dấu chấm; dòng ví dụ ghi đại lượng $\mathbb EL_D(\bar w_T)-1$ |
| K2 7-03 ghi chú diễn giả | đã sửa | "Ở ví dụ mở đầu, $\mathbb E\operatorname{opt}_S\approx0{,}0011$, còn khoảng cách tổng quát hóa kì vọng bằng $0{,}4750$" |
| K3 3-01 | đã sửa | "dịch $0{,}6154$, khoảng $0{,}31$ lần đường kính $2$ của $W$" |
| K4 2-08 | đã sửa | 5 dòng (Câu hỏi, Định nghĩa, câu định nghĩa, công thức, Ví dụ); `deck_lint` 0; ví dụ $h$ cố định chuyển vào ghi chú diễn giả kèm Mệnh đề 01.7 |
| K5 mật độ | đã sửa (chấp nhận) | trung vị 55, tối đa 59; 2-02 60→≤56, 2-03, 2-12, 4-05, 4-07, 5-02, 6-05 hạ theo bảng đề xuất |
| K6 7-03 dòng cuối | đã sửa | "SGD nhiều vòng: cần hệ số ổn định của chính SGD; mạng nơ-ron: hàm lỗi không lồi." khớp ghi chú §10, §12 |
| K7 7-03 ghi chú diễn giả | đã sửa | điều kiện của cận $RG/\sqrt T$ tách khỏi tính không chệch |
| K8 2-11 cột | đã sửa | tiêu đề cột $\mathbb E[L_D-L_S](\bar w_T)$, hết trùng nghĩa với "khoảng cách" giữa hai nghiệm ở 3-04, 5-03 (cách viết: L2-1) |
| K9 5-02 ghi chú diễn giả | đã sửa | "hằng số Lipschitz $2G/m$ của hiệu hai mục tiêu" |
| K10 4-03 ghi chú diễn giả | đã sửa | "điều kiện trên thuật toán chỉ là tính ổn định đều" |
| K11 2-01 | đã sửa | "(T2): …; hàm lỗi lồi: $\ell(\cdot,z)$ lồi." |
| K12 6-00, 2-00 | đã sửa | 6-00 "cân độ khớp với tính ổn định và xác định cỡ mẫu cho mức rủi ro vượt mức kì vọng"; 2-00 xem §3 |
| K13 3-03 | đã sửa | "(b) có điểm cực tiểu trên $W$; (c) điểm cực tiểu $\hat w_s$ duy nhất, …"; Giả thiết và Bảo đảm tách đoạn |
| K14 4-01 | đã sửa | "$\epsilon_{\mathrm{stab}}(4)\ge1{,}7988$" |
| K15 3-01 | đã sửa | "Tính chất của thuật toán cần đo là độ dịch của nghiệm khi thay một quan sát." |
| K16 4-02, 4-04 | đã sửa | 4-02 "ổn định đều chặn hiệu giữa hai giá trị"; ghi chú diễn giả 4-04 nối Fubini với kỹ thuật Bài 04. "độc lập với $(S,\xi)$" ở "Trực quan." 4-02 chuyển vào ghi chú diễn giả; chú thích hình vẫn nêu điều kiện độc lập cùng phân bố, chấp nhận |

## 2. Toán và mạch truyện trên trang đổi ±2

- Toán: 2-02 (câu hỏi với $\inf_{\lVert w\rVert\le5}L_D$, đúng lớp so sánh của Ví dụ 06.11), 2-03 (Trực quan), 2-08 ($0{,}5=1{,}25-0{,}75$), 2-11 (bảng giữ số, tổng $0{,}4750+0{,}0011=0{,}4761$), 2-12 ("Thiết lập của Ví dụ 06.2" cho đúng phân bố, hàm lỗi, $W=[-1,1]$, $w_1=0$; câu hỏi (c), (d) giữ chữ `exercises.md` dòng 35), 4-04 bước 4, 4-07 (b2), 6-05: không sai.
- Mạch: 2-07 → 2-08 → 2-09; 2-11 → 2-12 → 3-00 → 3-01; 3-02 → 3-03 → 3-04; 7-02 → 7-03 → 7-04: liền mạch, không dẫn kết quả trang sau. 6-05 "Các cận của Bài 06" có danh sách kết quả trong ghi chú diễn giả, chấp nhận.

## 3. Bốn dòng dài và dòng dẫn 2-00

- 1-02 (23 âm tiết): hai tên tiếng Anh bắt buộc ở lần dùng đầu (SGD, averaged iterate) — chấp nhận.
- 6-04 (26): dòng dữ liệu Ví dụ 06.10, có từ bản đóng băng, tách sẽ quá 6 dòng — chấp nhận.
- 2-11 (23): đoạn thứ hai của "Diễn giải:" — chấp nhận (sửa câu chữ ở L2-2).
- 7-03 (23): câu dẫn trả lời câu hỏi trung tâm, một ý trọn vẹn — chấp nhận.
- 2-00 "Gradient ngẫu nhiên trên quan sát mới không chệch cho rủi ro kì vọng; trên tập huấn luyện lưu lại, cho rủi ro thực nghiệm.": câu tỉnh lược đúng ngữ pháp, giữ tên chế độ B, ≤ 25 âm tiết, `deck_lint` không báo — chấp nhận.

## 4. Phát hiện còn mở (lượt 2)

| Mã | Mức độ | Trang chiếu | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|---|
| L2-1 | nhẹ | L06-2-11 | Kí hiệu tiêu đề cột không chuẩn: kì vọng đặt trước rồi mới áp vào $\bar w_T$. | "$\mathbb E[L_D-L_S](\bar w_T)$" | "$\mathbb E[(L_D-L_S)(\bar w_T)]$" |
| L2-2 | nhẹ | L06-2-11 | "Diễn giải:" mất từ nối tương phản và giới từ; "qua thuật toán" mơ hồ hơn bản lượt 1. | "$\mathbb E\operatorname{opt}_S\approx0{,}0011$, rủi ro vượt mức kì vọng …"; "Vế phải (b) … cần cận qua thuật toán" | "$\mathbb E\operatorname{opt}_S\approx0{,}0011$, nhưng rủi ro vượt mức kì vọng …"; "Vế phải của (b) … cần cận theo tính chất thuật toán, …" (+3 âm tiết, trang 54) |
| L2-3 | nhẹ | L06-2-08 (ghi chú diễn giả) | Mặt trang còn hai ví dụ, ghi chú diễn giả vẫn gọi "ví dụ thứ ba". | "Ví dụ thứ ba là câu ôn nhanh 2." | "Ví dụ thứ hai là câu ôn nhanh 2." |

Không thấy dấu hiệu `no-ai-slop` khác trong câu mới.

## 5. Kết luận

K1–K16 đã sửa đúng. Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 0 trung bình, 3 nhẹ (L2-1 đến L2-3, mỗi chỗ sửa một cụm từ, không đổi bố cục). **đạt** (ba chỗ nhẹ sửa khi điều phối viên kiểm cuối, không cần lượt kiểm lại thứ ba).
