# Rà lại 4b — Sư phạm và văn phong của bộ bài tập Bài 08 sau vòng sửa 1

Đối tượng: `lec08-ex-r1-frozen.md` (895 dòng, 9 283 tiếng; trùng từng byte với `2627-1/materials/lec-08/exercises.md`, đã kiểm bằng `cmp`). Đầu vào: `lec08-ex-r1.udiff`, `lec-08/reviews/11-quyet-dinh-bai-tap.md`, `lec-08/bai-tap-ghi-chu.md` §8. Số dòng trong mục "Phát hiện mới" theo bản r1. Chế độ `no-ai-slop`: Detect. Phạm vi gồm từng phát hiện cũ (`10-bai-tap-su-pham.md`) và các đoạn đã đổi, mỗi đoạn kèm một đoạn trước và một đoạn sau. Người rà chỉ đọc repo, không sửa, không commit.

**Tổng kết:** 24/24 phát hiện cũ đã được xử lý (24 ✓, 0 ✗, 0 một phần). Có 5 phát hiện mới, đều nhẹ: 0 chặn bàn giao, 0 nghiêm trọng, 0 trung bình, 5 nhẹ. Mục tiêu 2 nay được phủ đủ. Các đề xuất mới bỏ khoảng 20 tiếng.

## Phủ mục tiêu học tập (sau sửa)

| Mục tiêu | Bài đo | Kết quả |
|---|---|---|
| 1 | 08.1(a), (c) | Đạt (không đổi). |
| 2 | 08.3(a) chứng minh trực tiếp; 08.3(b), (c) chỉ chỗ dùng tính lồi | **Đạt.** Ý (a) mới (dòng 262–266) chứng minh $\lvert\Gamma(u)-\Gamma(v)\rvert\le\lvert u-v\rvert$ cho hàm lỗi Huber khi $0\le\eta\le2$, không dùng Bổ đề 08.4. Bước 4 tách vai trò của hai giả thiết: tính lồi cho cận trên, $\eta\le2/\beta$ cho cận dưới. Phản ví dụ $\eta=3$ cho hệ số $2$, khớp cột Huber của Ví dụ 08.3; tôi đã tính lại. Ý này không chép ghi chú: ghi chú chứng minh Bổ đề 08.4(b) qua tính đồng bức, còn bài làm bằng một chặn hai phía. |
| 3 | 08.1, 08.2(b), 08.7 | Đạt. |
| 4 | 08.2(c), 08.8(a)–(c) | Đạt. Sau khi bỏ ý ghép sai đầu ra, (c) vẫn đo phần "điều cận ghép không bảo đảm về lỗi kiểm tra". |
| 5 | 08.3, 08.4, 08.5, 08.6 | Đạt. |

Năm loại bài vẫn đủ; 08.3(a) thêm một ý chứng minh. Về khối lượng: 08.3 nay có năm ý (a)–(e) và là bài dài nhất. Nếu cần giảm tải, có thể ghi (e) là tùy chọn; tôi không ghi điều này thành phát hiện.

## Kiểm từng phát hiện cũ

| Mã | Nội dung | Kết quả | Bằng chứng (dòng r1) |
|---|---|---|---|
| T1 | "ghép cặp" hai nghĩa ở 08.6 | ✓ | 648, 677, 688, 695, 717, 730: "sai số chuẩn của hiệu theo hạt giống"; "ghép cặp" chỉ còn cho hai lần chạy (5, 22, tiêu đề 08.6, bảng $\Delta$). Thuật ngữ cho `thuat-ngu.md` được chuyển cho điều phối viên (`bai-tap-ghi-chu.md` §8). |
| T2 | Mục tiêu 2 thiếu phần chứng minh | ✓ | 262–266 (đề), 286, 290 (gợi ý), 294–313 (lời giải bốn bước), 403 (Kiểm tra lại). |
| T3 | 08.8(c) lặp ghi chú | ✓ | 829–837: đã cắt; (d) thành (c); mục tiêu 808 bỏ "nhận ra một cách ghép cận sai"; gợi ý đánh lại. |
| T4 | 08.5 thiếu dữ kiện, câu đầu thiếu động từ | ✓ | 505 "Một báo cáo mô tả việc huấn luyện …" có động từ chính; 513 "đạo hàm cấp một và cấp hai bị chặn"; 558 "$W$ là toàn bộ không gian tham số"; 574 nêu đạo hàm cấp hai bị chặn là giả thiết. |
| N1 | Tiếng Anh ở lần đầu | ✓ | 6 (gradient step map, stability coefficient), 22 (recurrence inequality), 147 (expected generalization gap), 269 (co-coercivity), 339 (còn gọi là bổ đề hạ), 410 (stationarity), 438 (stationary point), 634 (standard deviation). |
| N2 | Dòng "Mục tiêu" dài | ✓ | 17, 134, 258, 410, 502, 581, 808 rút còn 15–25 tiếng. |
| N3 | "chặt ngặt", "$3$ trên $16$ dãy" | ✓ | 30, 122–127. |
| N4 | Câu lặp ở Kiểm tra lại 08.1 | ✓ | 129. |
| N5 | Dấu hai chấm ở 08.1(b) Bước 3 | ✓ | 91 "…, vì nó phải đúng …". |
| N6 | Tám số dồn ở 08.2(b) Bước 2 | ✓ | 205–210: bảng có câu dẫn đứng trước. |
| N7 | 08.2(c) dựa vào gợi ý; "Lưu ý:"; "cận tối ưu" | ✓ | 245 "Như (a), $\sum_t1/t^2\le\ldots=2$"; 158 thành câu thường; 149 gọi tên "độ chênh tối ưu" và đặt tên "*cận tối ưu*" cho vế phải. |
| N8 | Đoạn tóm tắt và chữ "hỏng" ở 08.3 | ✓ | 355: hai câu; grep không còn "hỏng". |
| N9 | "Tính trực tiếp" | ✓ | 370 "Tính bằng máy". |
| N10 | "cái giá phải trả" | ✓ | 403. |
| N11 | Kết luận từ ước lượng ở 08.4(c) | ✓ | 469. |
| N12 | Kiểm tra lại 08.5 | ✓ | 576: hai phép kiểm mới; tôi tính lại $10/(1+e)\approx2{,}69$. |
| N13 | Câu giải thích sau bảng; câu lặp; "Phạm vi"; "che mất" | ✓ | 677 (đã chuyển lên trước bảng, xem M1); 717 đã bỏ câu "Cận cũng …"; 731 đã bỏ "Phạm vi"; 695 bỏ ẩn dụ (xem M2). Bằng chứng/chứng minh vẫn được nói ở (b) Bước 2 (dòng 721), nên yêu cầu của giao thức vẫn giữ. |
| N14 | "Lời hứa của Bài 06"; dấu hai chấm 08.7 | ✓ | 801 đã cắt; 767 đã bỏ dấu hai chấm (xem M3). |
| N15 | "lệch dưới $10^{-8}$"; câu 46 tiếng | ✓ | 880 đã cắt; 882 tách thành hai câu. |
| N16 | Gợi ý 08.4 không tăng dần | ✓ | 430 (Gợi ý 1: "So sánh $\nabla\ell(w,z_j)$ …"), 434 (Gợi ý 2: "… bằng $0$, nên gradient ngẫu nhiên không có nhiễu"). |
| N17 | Câu dài | ✓ | 22, 424, 719 đã tách; 324 đã viết lại (46 tiếng, nhưng không còn mệnh đề phụ chen trước động từ). 147 còn 45 tiếng, xem M5. |
| N18 | Ngoặc ở 08.5(d) Bước 2; phạm vi Nhận xét 08.11 | ✓ | 574: ngoặc đã tách thành câu; phạm vi "SGD không chiếu với hàm lỗi trong $[0,1]$" đã nêu (cũng là mục Toán 3). Đoạn mới quá dài, xem M4. |
| N19 | Câu dẫn cho năm bảng 08.6 | ✓ | 584 "Các bảng dưới đây là số liệu cho phần (a) và (b)." |
| N20 | Nhận xét 05.17 là "đọc thêm"; $R$ | ✓ | 149 "(đọc thêm của Bài 05)", "$R\ge\lVert w_1-u\rVert$". |

**Gợi ý 1 mới không lộ lời giải:** 08.3 Gợi ý 1 (a) (dòng 286) chỉ yêu cầu viết hiệu hai ảnh theo $u-v$ và $d(u)-d(v)$; chặn $0\le\delta\le u-v$ chỉ có ở Gợi ý 2. Gợi ý 1 của 08.4 (dòng 430) chỉ yêu cầu so sánh các gradient. Cả hai đạt.

## Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | M1. 08.6 lời giải Bước 3, dòng 677 | Sau khi chuyển câu lên trước bảng, đoạn nói hai lần cùng một ý (`no-ai-slop`: lặp). | "rồi so trị tuyệt đối của trung bình hiệu với sai số chuẩn. Mỗi ô ghi sai số chuẩn, rồi tỉ số giữa trị tuyệt đối của trung bình hiệu và sai số chuẩn." | "**Bước 3: sai số chuẩn của hiệu theo hạt giống.** Sai số chuẩn bằng độ lệch chuẩn của các hiệu chia cho $\sqrt{20}$. Mỗi ô ghi sai số chuẩn, rồi tỉ số giữa trị tuyệt đối của trung bình hiệu và sai số chuẩn." (−10) |
| nhẹ | M2. 08.6 lời giải Bước 4, dòng 695 | "khoảng $12$ lần" xuất hiện hai lần trong cùng một đoạn. | "lớn hơn sai số chuẩn của hiệu theo hạt giống ($0{,}0021$) khoảng $12$ lần. … công thức độc lập bỏ qua tương quan này, nên cho sai số chuẩn lớn gấp khoảng $12$ lần." | Kết câu cuối ở "…; công thức độc lập bỏ qua tương quan này." (−7) |
| nhẹ | M3. 08.7(a) lời giải Bước 1, dòng 767 | Bản sửa bỏ dấu hai chấm nhưng tạo một câu có hai lần "nên". | "…, nên $\ell(\cdot,(x,y))$ lồi và đạo hàm của nó $2$-Lipschitz trên $\mathbb R$, nên (S) đúng với $\beta=2$." | "…, nên $\ell(\cdot,(x,y))$ lồi và đạo hàm của nó là $2$-Lipschitz trên $\mathbb R$; do đó (S) đúng với $\beta=2$." (±0) |
| nhẹ | M4. 08.5(d) lời giải Bước 2, dòng 574 | Đoạn dài 159 tiếng với năm ý (hằng số trên $W$, tính không lồi, thừa số hàm mũ, kết luận, phạm vi Nhận xét 08.11), dồn vào một bước (§7a); hai câu dài 42 và 48 tiếng (§9). | "**Bước 2: hàm kích hoạt trơn và phép chiếu.** Trên $W$ lồi, bị chặn, … Cận không cho thông tin. Nhận xét 08.11 dùng độ dài bước giảm như $c/t$, nhưng nó được phát biểu cho SGD không chiếu với hàm lỗi trong $[0,1]$; áp dụng cho thiết lập (ii) cần chia hàm lỗi …" | Tách thành "**Bước 2: hằng số trên $W$.**" (ba câu đầu, đến "Ví dụ 08.10, Bước 3") và "**Bước 3: cận không lồi.**" (từ "Bước 1 của Phụ lục D …"). Câu cuối: "Nhận xét 08.11 dùng độ dài bước giảm như $c/t$, nhưng được phát biểu cho SGD không chiếu với hàm lỗi trong $[0,1]$. Để áp dụng cho (ii), cần chia hàm lỗi cho cận trên của nó và kiểm lại lập luận khi có phép chiếu." (+3) |
| nhẹ | M5. 08.2(b) đề, dòng 147 | Câu 45 tiếng (thêm tiếng Anh làm câu dài hơn); dấu hai chấm nối hai yêu cầu. | "tính ngân sách độ dài bước và cận của Định lý 08.6 cho khoảng cách tổng quát hóa kì vọng (expected generalization gap) của $w_{T+1}$: trước hết dùng (a), rồi dùng các giá trị tính bằng máy …" | "… của $w_{T+1}$. Tính trước hết bằng (a), rồi bằng các giá trị tính bằng máy …" (±0) |
