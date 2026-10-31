# Rà lại 4b — Sư phạm và văn phong của bộ bài tập Bài 09 sau vòng sửa 1

Đối tượng: `lec09-ex-r1-frozen.md` (1027 dòng, 9 985 tiếng; trùng từng byte với `2627-1/materials/lec-09/exercises.md`, đã kiểm bằng `cmp`). Đầu vào: `lec09-ex-r1.udiff`, `planning/lec-09/reviews/11-quyet-dinh-bai-tap.md`, `bai-tap-ghi-chu.md` §8. Vị trí ghi theo số dòng của `lec09-ex-r1-frozen.md`. Chế độ `no-ai-slop`: Detect. Phạm vi: các đoạn đã đổi trong diff, cộng một đoạn trước và một đoạn sau mỗi đoạn. Tôi đã đọc toàn bộ diff (553 dòng). Người rà chỉ đọc, không sửa, không commit.

**Tổng kết:** 24/24 phát hiện cũ đã xử lý: 22 ✓, 2 một phần (có lý do chấp nhận được). Phát hiện mới: 8. Chặn bàn giao: 0. Nghiêm trọng: 0. Trung bình: 1. Nhẹ: 7. Mục tiêu 4 và 5 nay được đo đủ. Các gợi ý 1 mới không lộ lời giải. §11 của ghi chú đã sửa đúng hai dòng (dòng 804: "mục tiêu 4, 5"; dòng 810: "Tùy chọn: bước M cho trọng số hỗn hợp; UML Bài tập 24.3").

## Kiểm từng phát hiện cũ

| Phát hiện | Kết quả | Ghi chú |
|---|---|---|
| T1 (tách tái tạo và KL, mục tiêu 4) | ✓ | Đề 325 thêm yêu cầu; lời giải thêm Bước 5 (tái tạo $-1{,}1439$, KL tới tiên nghiệm $0{,}3681$, hiệu $-1{,}5120$ trùng Bước 4). Có câu dẫn cho từng công thức. |
| T2 (trường hợp bị chệch, mục tiêu 5) | ✓ | Ý (d) ở 329; lời giải ba bước (đạo hàm đúng $1$; ước lượng $\pm2$, kì vọng $0$; (i) của Mệnh đề 09.15 không thỏa). Mức độ, mục tiêu và §11 của ghi chú đã cập nhật. Một chỗ thiếu bước trung gian (M1). |
| T3 ("bằng chứng", "chuỗi hình học", "dừng") | ✓ | Không còn "bằng chứng" theo nghĩa kết quả thí nghiệm; "Tổng của cấp số nhân"; "xác suất kết thúc"; "Điểm dừng" ở 09.5 thay bằng phép tính đạo hàm. |
| N1 (tiếng Anh, KL, ELBO, khe) | ✓ | KL, ELBO có trong danh sách viết tắt; token, bigram model, perplexity, geometric distribution, mixture, random seed, add-one smoothing, *khe* (gap) có ở lần đầu. |
| N2 ($S^2$) | ✓ | $V_s$. |
| N3 ($N$, $\varphi_0$) | ✓ | $\nu_+$, $\rho_0$. |
| N4 (đẳng thức chỉ có trong gợi ý) | ✓ | 09.8(a) Bước 2 tự khai triển; (b) Bước 1 dẫn "(a), Bước 2". |
| N5 (Kiểm tra lại 09.9) | một phần | Đã ghi "Tính bằng máy" và cắt câu thứ hai. Phép kiểm tay không được thêm vì hết chữ; chấp nhận. |
| N6, N8, N13, N14, N17 (cắt) | ✓ | |
| N7 (09.6(a) Bước 5) | ✓ | Gộp với mục toán 3; xem M2 về một số chưa có trong đề. |
| N9 (09.7(c) Bước 3) | ✓ | Hai phép cộng đúng: $(2\mu-2)^2+(2-\mu)^2=5\mu^2-12\mu+8$; $\sigma^2+5\sigma^2+(\sigma^2-2+1/\sigma^2)-2=7\sigma^2+1/\sigma^2-4$. |
| N10 (09.5(a)) | ✓ | Lý do cực tiểu ở Bước 2, đạo hàm ở Bước 3. |
| N11 (gợi ý 09.7(a)) | ✓ | Gợi ý 1 chỉ nói "thác triển $g$ sao cho đạo hàm vẫn không giảm"; cách dựng tiếp tuyến chuyển sang Gợi ý 2. |
| N12 (gợi ý 09.6(b)(i)) | ✓ | Gợi ý 1 nêu hai điều kiện của Ví dụ 09.4; lý do "học trước khi rút mẫu kiểm tra" ở Gợi ý 2. |
| N15 (09.2(b) Bước 5) | ✓ | |
| N16 (dấu hai chấm, ẩn dụ, "mạnh hơn") | ✓ | Câu mới ở 100 mở bằng kí hiệu (M8). |
| N18 (câu dài) | một phần | 538 tách đôi; cột "Hiệu" rút gọn và tách câu. Câu đầu đề 09.6 (giao thức trong ngoặc) giữ nguyên, khoảng 35 tiếng ngoài ngoặc; chấp nhận. |
| N19 (Mức độ 09.2) | ✓ | |
| N20 (Kiểm tra lại 09.2) | ✓ | "quy tắc tra cứu của Ví dụ 09.5". |
| N21 (tên 09.10 ở §11) | ✓ | Ghi chú dòng 810. |

## Phủ mục tiêu 4 và 5

| Mục tiêu | Bài đo | Kết luận |
|---|---|---|
| 4. Đồng nhất thức và dấu bằng; tách thành số hạng tái tạo và KL trên một mô hình Gauss | 09.4(a) (bất đẳng thức và dấu bằng), (b) Bước 5 (tái tạo và KL trên hỗn hợp Gauss) và Bước 6 (khe bằng KL tới hậu nghiệm), (c); 09.10(a) | Đủ. |
| 5. Gradient theo đường đi; điều kiện đổi chỗ đạo hàm và kì vọng; một trường hợp bị chệch | 09.7(b) (kiểm (i)–(iii) với lân cận cho mọi điểm), 09.4(d) (tái tham số hóa biến rời rạc, ước lượng bị chệch, (i) không thỏa) | Đủ. |

## Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | M2. 09.6(a) Bước 5, dòng 637 | Đề thiếu dữ kiện: lời giải dùng độ lệch chuẩn $0{,}0013$ của hiệu giữa $p_{\mathrm{alt}}$ và mô hình học được, một số không có trong đề và người học không tính được từ các số đã cho. Từ hai độ lệch chuẩn của đề vẫn có một cận trên đủ dùng. | "tính trên cùng các lần chạy, độ lệch chuẩn của hiệu này là $0{,}0013$. Lỗi kiểm tra cũng tách $p_{\mathrm{alt}}$ khỏi mô hình học được." | "Độ lệch chuẩn của một hiệu không quá tổng hai độ lệch chuẩn, nên hiệu này có độ lệch chuẩn không quá $0{,}0012+0{,}00040=0{,}0016$, nhỏ hơn khoảng $24$ lần hiệu. Lỗi kiểm tra cũng tách $p_{\mathrm{alt}}$ khỏi mô hình học được." (±0) |
| nhẹ | M1. 09.4(d) Bước 1, dòng 453 | Bỏ bước trung gian (§7a): người học không thấy hai số hạng $+1$, $-1$ từ đâu ra. | "Lấy đạo hàm; hai số hạng $+1$ và $-1$ triệt tiêu:" | "Đạo hàm của $-(1-\phi)\ln(1-\phi)$ là $\ln(1-\phi)+1$, của $-\phi\ln\phi$ là $-\ln\phi-1$; hai số hạng $+1$ và $-1$ triệt tiêu, nên" (+18; bù bằng M3) |
| nhẹ | M3. 09.6 đề dòng 575; lời giải Bước 4 dòng 635 | Sau khi cắt ở Bước 4, đề còn cho số "$5{,}9\%$" nhưng lời giải không dùng đến. | 575: "…; $5{,}9\%$ số chuỗi có không quá $18$ cặp." | Cắt vế này khỏi đề (−9). Hoặc giữ, và thêm vào Bước 4: "($5{,}9\%$ số chuỗi mô phỏng có không quá $18$ cặp)" (+9). |
| nhẹ | M4. 09.1(b) Bước 1, dòng 78 | Câu cắt để giữ trần chữ là câu trả lời trực tiếp cho câu hỏi đầu của (b) ("So hai độ bối rối ở (a) với độ bối rối của mô hình đều"). Lời giải nay không nêu phép so sánh. | 78: "Mô hình đều gán $\tfrac13$ cho mọi kí tự, nên độ bối rối của nó bằng $3$ trên mọi chuỗi (đoạn sau Định nghĩa 09.4)." | Thêm lại: "Hai độ bối rối ở (a), $2{,}6591$ và $1{,}6719$, đều nhỏ hơn $3$." (+11; bù bằng M3 và M6) |
| nhẹ | M5. 09.6(c) Bước 1, 3 (dòng 658, 662) | Ở 658, chữ "nên" lặp với hai nghĩa ("do đó" và "cần phải"). Bước 3 sau khi rút chỉ còn con số, không nói số đó có nghĩa gì so với dự đoán (§7a). | 658: "…gần $0{,}6$, nên tỉ lệ giữ nguyên nên gần $0{,}6$."; 662: "Một lần chạy cho trung bình $0{,}597$ qua mười hạt giống (từ $0{,}586$ đến $0{,}621$)." | 658: "…gần $0{,}6$, nên dự đoán tỉ lệ giữ nguyên gần $0{,}6$." 662: "…(từ $0{,}586$ đến $0{,}621$), khớp dự đoán." (+3) |
| nhẹ | M6. 09.6(b) Bước 2, dòng 650 | Vế sau thiếu chủ ngữ. | "Cận đúng với mọi phân bố có hàm lỗi trong đoạn đó, nên lỏng với xích Markov này." | "…, nên nó lỏng với xích Markov này." (+1) |
| nhẹ | M7. 09.4 dòng "Mục tiêu" (320); đề (b) dòng 325 | "tách cận" không nói tách thành gì. Ở 325, chuỗi "và … và" làm câu khó đọc. | 320: "tách cận trên một hỗn hợp (mixture) Gauss"; 325: "rồi tính số hạng tái tạo và $\mathrm{KL}$ tới tiên nghiệm và kiểm Định lý 09.12(c)." | 320: "tách cận thành số hạng tái tạo và KL trên một hỗn hợp (mixture) Gauss" (+5). 325: "rồi tính số hạng tái tạo, $\mathrm{KL}$ tới tiên nghiệm, và kiểm Định lý 09.12(c)." (−1) |
| nhẹ | M8. 09.1(c) Bước 2, dòng 100; 09.7 đề (b), dòng 676 | Câu ở 100 mở bằng một kí hiệu toán. Ở 676, sau khi bỏ vế "chọn lân cận …", câu về lân cận của Ví dụ 09.11 thành một nhận xét lơ lửng, không nói người học cần làm gì. | 100: "$x_1$ ảnh hưởng tới $x_3$ qua phân bố của $x_2$."; 676: "Lân cận ở Ví dụ 09.11, Bước 4 không chứa điểm $(2,\tfrac12)$ của $W$." | 100: "Kí tự $x_1$ ảnh hưởng tới $x_3$ qua phân bố của $x_2$." (+2). 676: "Lân cận ở Ví dụ 09.11, Bước 4 không chứa điểm $(2,\tfrac12)$ của $W$, nên cần một lân cận khác." (+4) |

**Ngân sách:** M1 +18, M4 +11, M5 +3, M6 +1, M7 +4, M8 +6; M3 (cắt) −9. Tăng ròng khoảng +34, tệp lên khoảng 10 019 tiếng. Muốn giữ dưới 10 000: rút M1 thành "Đạo hàm của $-(1-\phi)\ln(1-\phi)-\phi\ln\phi$ là $\ln\frac{1-\phi}\phi$, nên" (+8 thay +18), và bỏ phần 676 của M8. Khi đó tăng ròng khoảng +20, tệp còn khoảng 10 005; cắt thêm "(xấp xỉ của một hoán vị ngẫu nhiên khi số cửa sổ lớn)" ở 09.2(b) nếu điều phối viên chấp nhận (−9).

Văn phong ở các đoạn đã cắt câu lặp (09.1(b), 09.2(d), 09.3(b)(c), 09.4(c), 09.5(a), 09.6(b)(c), 09.7(a)(e), 09.8(b)(c), 09.9(a), 09.10(a)): không có câu cụt nghĩa hay mất lý do, trừ M4, M5, M6. Không thấy "hãy", "Đáp án", câu hỏi tu từ, dấu hai chấm "tiết lộ" mới hay thuật ngữ lệch `thuat-ngu.md`.
