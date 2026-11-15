# Duyệt deck Bài 02 — vai 5 `mach-truyen` (mạch truyện, liên kết, thống nhất thứ tự với ghi chú)

Ngày: 2026-11-15. Chỉ đọc. Bản đóng băng: `2627-1/lecture-02-bat-dang-thuc-tap-trung.html` (55 trang, 7 mạch).

Đối chiếu: `materials/lec-02/lecture-note.md`, `exercises.md`, `planning/lec-02/storyboard.md`, `review-log.md` § "Bộ trang chiếu", deck `lecture-01-mo-hinh-hoc.html` (đang sửa), `CLAUDE.md` § Slide decks, `common-brief.md`, `brief-reviews.md`.

Kiểm trên trình duyệt (Playwright, `http://localhost:8766/`, 1600×900): sáu liên kết của trang "Nội dung" (`hashOneBasedIndex: true`), cả gõ `#/2`…`#/7` lẫn bấm chuột, đến đúng `L02-2-00`…`L02-7-00`; hai liên kết viewer ở `L02-7-05` mở đúng ghi chú và tệp bài tập, nút "Bộ trang chiếu" của viewer trỏ về `lecture-02-bat-dang-thuc-tap-trung.html`, không lỗi trang. `deck_check.py`: 55 trang, console 0, pageerrors 0, failed 0. Ảnh chụp đã xem: `L02-1-05`, `L02-3-04`, `L02-5-08`, `L02-7-02`, `L02-7-05` (thư mục nháp `…/scratchpad/lec-02/rv-mach-truyen/dc/`).

## 1. Bảng mạch → mục ghi chú

| Mạch | Tiêu đề (h2 = mục "Nội dung") | Liên kết | Mục ghi chú | Liên tiếp, đúng thứ tự |
|---|---|---|---|---|
| 1 | Mở đầu | — | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết; ứng dụng chọn trong $K$ ứng viên (§3) | có |
| 2 | Xác suất đuôi và bất đẳng thức Markov, Chebyshev | `#/2` → `L02-2-00` | §1, §2, §3 (Ví dụ 02.1), §4 | có (xem phát hiện 9 về tiêu đề) |
| 3 | Phương pháp Chernoff và bất đẳng thức Hoeffding | `#/3` → `L02-3-00` | §5: Định nghĩa 02.4 → Nhận xét 02.8, đoạn về $\ell_c$ | có; Ví dụ 02.4 Bước 1–3 kéo lên `3-04` |
| 4 | Cận tin cậy cho một giả thuyết cố định | `#/4` → `L02-4-00` | §5: Định nghĩa 02.9 → Nhận xét 02.11 | có; Ví dụ 02.4 Bước 4 ở `4-04` |
| 5 | Hội tụ đều và rủi ro vượt mức trên lớp hữu hạn | `#/5` → `L02-5-00` | §6, §7 | có |
| 6 | Lớp hữu hạn trong trường hợp khả diễn | `#/6` → `L02-6-00` | §8, §9 | có |
| 7 | Tổng kết | `#/7` → `L02-7-00` | §9–§12 | có |

Bảy mạch (trong khoảng 5–7), mỗi mạch ứng với các mục liên tiếp; thứ tự mạch đúng thứ tự mục của ghi chú.

## 2. Bảng chức năng từng trang và đối chiếu trang → khối ghi chú

| Trang | Vai trò trong mạch | Kết nối vào | Kết nối ra | Khối ghi chú | Thứ tự |
|---|---|---|---|---|---|
| 1-01 | bìa, luận điểm | Bài 01 (ghi chú diễn giả) | toàn bài | đoạn mở, Định lý 02.14, §9 | — |
| 1-02 | tiên quyết, nhắc lại Bài 01 | Mệnh đề 01.7, Định nghĩa 01.16/18/25 | kí hiệu $K,\epsilon,\delta$ | Kiến thức tiên quyết, §2 | đúng |
| 1-03 | mục tiêu (6, khớp ghi chú) | — | toàn bài | Mục tiêu học tập | đúng |
| 1-04 | nội dung, 6 liên kết | — | mạch 2–7 | — | đúng |
| 1-05 | vấn đề trung tâm, một hộp "Câu hỏi:" | — | trả lời ở 7-02 | đoạn mở (câu hỏi trung tâm) | đúng |
| 1-06 | ví dụ dẫn nhập, hai câu hỏi | 1-05 | Q1 → 4-05, Q2 → 5-08 | Câu hỏi mở đầu; §3 ứng dụng | đúng |
| 2-00 | tiêu đề mạch 2 | 1-06 | 2-06 (cận $\propto1/m$) | §1–§4 | — |
| 2-01 | khung: (T1)–(T4), (O1), bốn đại lượng | 1-06 | mọi kết quả | §1, §2 | đúng |
| 2-02 | ví dụ xuyên suốt $D_\eta$, $h_t$, nhắc $S_\eta$ | Bài 01 | 2-03, 2-06, 3-02, 5-02 | Ví dụ 02.1 | đúng |
| 2-03 | trực quan + định nghĩa xác suất đuôi, giá trị chính xác | 2-02 | 2-06 (so cận với giá trị chính xác) | Định nghĩa 02.1, Ví dụ 02.2 | đúng |
| 2-04 | phát biểu Markov, Chebyshev | 2-03 | 2-05, 2-06 | Bổ đề 02.2, 02.3 | đúng |
| 2-05 | ý tưởng chứng minh | 2-04 | 3-01 (Chernoff = Markov cho hàm mũ) | chứng minh 02.2, 02.3 | đúng |
| 2-06 | ví dụ số, kết luận "chỉ giảm như $1/m$" | 2-03, 2-04 | câu nối sang mạch 3 trên mặt trang | Ví dụ 02.3 | đúng |
| 3-00 | tiêu đề mạch 3 | 2-06 | 3-04 | §5 (đầu) | — |
| 3-01 | định nghĩa hàm sinh mô-men, kỹ thuật Chernoff | 2-05 | 3-02, 3-05 | Định nghĩa 02.4, Bổ đề 02.5 | đúng |
| 3-02 | trực quan, phát biểu, ví dụ bổ đề Hoeffding | 3-01 | 3-03, 3-04 | Bổ đề 02.6 | đúng |
| 3-03 | ý tưởng chứng minh bổ đề Hoeffding | 3-02 | 3-05 | chứng minh 02.6, Phụ lục A | đúng |
| 3-04 | trực quan, phát biểu, cận số | 3-01, 3-02 | 4-02; so với 2-06 chỉ ở ghi chú diễn giả | Định lý 02.7; Ví dụ 02.4 B1–3 | Ví dụ 02.4 lên trước Hệ quả 02.10 (nhẹ, chấp nhận được) |
| 3-05 | ý tưởng chứng minh Hoeffding | 3-01, 3-03 | 4-03 | chứng minh 02.7 | đúng |
| 4-00 | tiêu đề mạch 4 | 3-04 | 4-05 | §5 (Định nghĩa 02.9 trở đi) | — |
| 4-01 | định nghĩa cận/khoảng tin cậy, câu hỏi | 4-00 | 4-02 (cần bán kính: chỉ ở ghi chú diễn giả) | Định nghĩa 02.9 | đúng |
| 4-02 | phát biểu Hệ quả 02.10 | 3-04, 4-01 | 4-03, 4-04, 4-05 | Hệ quả 02.10 | đúng |
| 4-03 | ý tưởng chứng minh; "bỏ $h$ cố định" | 3-04 | mạch 5 | chứng minh 02.10 | đúng |
| 4-04 | kỹ thuật đảo cận đuôi, bảng cỡ mẫu | 2-06, 4-02 | 5-05, 6-05 | chứng minh 02.10 B3–5; Ví dụ 02.4 B4 | đúng |
| 4-05 | trả lời Q1 của 1-06 ($8{,}9\%$) | 1-06, 4-02 | mạch 5 | Ví dụ 02.5 | đúng |
| 4-06 | phản ví dụ bỏ (T1), (T3) | 3-05, 4-03 | 7-01 | Ví dụ 02.6, Nhận xét 02.11 | đúng |
| 5-00 | tiêu đề mạch 5 | 4-03, 4-05 | 5-03, 5-09 | §6, §7 | — |
| 5-01 | vấn đề: thiên lệch do chọn | 1-06 (Q2) | 5-02 (câu nối chỉ ở ghi chú diễn giả) | Ví dụ 02.7 | đúng |
| 5-02 | định nghĩa mẫu đại diện, biến cố hội tụ đều | 5-01 | 5-03, 5-10 | Định nghĩa 02.13 | đúng |
| 5-03 | trực quan, phát biểu | 4-02, 5-02 | 5-04, 5-08, 5-09 | Định lý 02.14 | đúng |
| 5-04 | ý tưởng chứng minh, nhắc bất đẳng thức hợp | Bài 01 (`L01-4-04`), 4-02 | 5-05, 7-04 câu 2 | chứng minh 02.14; Bổ đề 02.12 | Bổ đề 02.12 dạng "Nhắc lại" (đúng chính sách kỹ thuật) |
| 5-05 | kỹ thuật chia $\delta/K$ | 4-04, 5-04 | 6-08 | chứng minh 02.14 B3–4, §9 | đúng |
| 5-06 | bài tập (đề) | 5-03, 5-04 | 5-07 | Bài tập 02.4 | đúng |
| 5-07 | bài tập (lời giải) | 5-06 | 7-01 | lời giải Bài tập 02.4 | đúng |
| 5-08 | ví dụ bán kính theo $K$; trả lời Q2 (chỉ ở ghi chú diễn giả) | 1-06, 4-05, 5-03 | 5-09 (câu nối chỉ ở ghi chú diễn giả) | Ví dụ 02.8, Nhận xét 02.15 | đúng |
| 5-09 | trực quan, phát biểu, ví dụ số | 5-03 | 5-10, 6-05 | Hệ quả 02.16; Ví dụ 02.9, 02.10 | đúng |
| 5-10 | ý tưởng chứng minh | 5-02, 5-03 | 5-11, 5-12 | chứng minh 02.16 | đúng |
| 5-11 | kỹ thuật bước tất định | 5-10 | Bài sau | chứng minh 02.16 B2–3 | đúng |
| 5-12 | bài tập (đề; lời giải ở ghi chú diễn giả) | 5-10 | 6-00 | Bài tập 02.3(a) | đúng |
| 6-00 | tiêu đề mạch 6 | 5-09 ($1/\epsilon^2$) | 6-06 | §8, §9 | — |
| 6-01 | ví dụ $D_f$, định nghĩa, trực quan | Bài 01 ($D_f$, bỏ sót) | 6-02, 6-03 | §8 đầu; Ví dụ 02.11 B4 | ví dụ trước phát biểu (đúng hành trình khái niệm) |
| 6-02 | phát biểu Mệnh đề 02.17 | 6-01 | 6-03, 6-04, 6-05 | Mệnh đề 02.17 | đúng |
| 6-03 | ý tưởng chứng minh | 5-04, 6-01 | 6-04 | chứng minh 02.17 | đúng |
| 6-04 | ví dụ bốn mức cỡ mẫu | 6-02, Bài 01 (Mệnh đề 01.31) | 6-08 | Ví dụ 02.11 | đúng |
| 6-05 | ví dụ bảng cỡ mẫu theo $K$ | 4-04, 5-09, 6-02 | 6-06 | Ví dụ 02.12 | đúng |
| 6-06 | trực quan hai tốc độ | 6-05 | 7-04 câu 3 | Nhận xét 02.18 | đúng |
| 6-07 | bài tập có lời giải | 5-09, 6-02 | 7-01 | Bài tập 02.8(c)(d) | đúng |
| 6-08 | giá của $K$, lớp phụ thuộc dữ liệu | 2-06, 5-05 | 7-02 dòng 5 | §9 | đúng |
| 7-00 | tiêu đề mạch Tổng kết | — | 7-01 | §9–§12 | — |
| 7-01 | bảng `Kết quả | Giả thiết | Ý tưởng chứng minh` | các trang kết quả | 7-02 | §4–§9 | đúng |
| 7-02 | vấn đề trung tâm (trả lời 1-05) | 1-05 | 7-03 | đoạn mở, §9 | đúng |
| 7-03 | bài tập tổng hợp có "Lời giải:" | 3-04, 5-09, Bài 01 ($\ell_c$) | 7-04 | Bài tập 02.11 | đúng |
| 7-04 | câu hỏi tự kiểm tra (3) | 5-03, 5-04, 6-06 | — | §11, Nhận xét 02.18 | đúng |
| 7-05 | bài tập về nhà, viewer | `exercises.md` | ghi chú, tệp bài tập | §10 | đúng |
| 7-06 | tài liệu tham khảo, dòng Bài 03 | §12 | Bài 03 (tên khớp `lec-03/lecture-note.md`) | §12 | đúng |

## 3. Bảng kiểm mạch truyện

| Mục kiểm | Kết quả |
|---|---|
| "Vấn đề trung tâm" mở đầu: một hộp, một "Câu hỏi:" | đạt (`1-05`; câu trả lời từng mạch nằm trong ghi chú diễn giả) |
| "Vấn đề trung tâm" cuối trả lời cho cả bài | đạt (`7-02` trả lời hộp `1-05`: $h$ chọn trước, $\hat h$ chọn theo $S$, ERM, khả diễn, giả thiết); câu hỏi của ví dụ dẫn nhập `1-06` không được nhắc lại trên mặt trang (phát hiện 3) |
| Câu hỏi trung tâm của mạch trên mặt trang trước nửa sau | đạt: dòng dẫn mạch ở cả sáu trang tiêu đề mạch nêu ý cốt lõi; mạch 5 có thêm ví dụ vấn đề `5-01` |
| Câu nối giữa mạch và giữa cụm trên mặt trang | 2→3 đạt (`2-06` dòng cuối); 3→4 thiếu so sánh với Chebyshev (phát hiện 4); 4→5 đạt một phần (`4-03`, `4-05`); trong mạch 5 thiếu hai câu nối then chốt (phát hiện 1, 2); 5→6 đạt qua dòng dẫn `6-00` |
| Không xem trước bài sau trên mặt trang | đạt (Bài 03 chỉ ở `7-06`, Bernstein chỉ ở ghi chú diễn giả) |
| Không dẫn kết quả của trang sau | đạt (mọi "dùng ở …" trên mặt trang trỏ về trang trước) |
| Mạch Tổng kết không thêm khái niệm mới | đạt ($\ell_c$ có "Nhắc lại:" từ Bài 01; phần (a) của Bài tập 02.11 là đề bài) |
| Trang "Nội dung" ↔ `#/N` ↔ h2 | đạt (kiểm trên trình duyệt) |
| Bảng `Mục | Bài tập` ↔ `exercises.md` | đủ 11 bài, không trùng; một chỗ xếp mạch (phát hiện 12) |
| Liên kết viewer, bài sau | đạt |
| Từ khóa mạch và thuật ngữ in nghiêng của ghi chú có trên mặt trang | đạt (cận đuôi, cận trên tin cậy, khoảng tin cậy, cận một/hai phía, bán kính tin cậy, thiên lệch do chọn, biến cố hội tụ đều, nhất quán với tập huấn luyện, giả thuyết xấu, ngưỡng xấu, dùng lại thích nghi, lớp phụ thuộc dữ liệu, dây cung, hai tốc độ) |
| Trùng lặp | nhẹ (phát hiện 7, 16) |
| Liên tục với deck 01 | đạt: cùng (T1), (T2), (O1), (O2); "ví dụ sàng lọc", $D_\eta$, $D_f$, $S_\eta$, $h_t$, $A_{\max}$, $\ell_c$ với $(c_{FP},c_{FN})=(1,4)$; bảng $L_{D_\eta}(h_t)$ trùng `L01-2-04`; bất đẳng thức hợp và "chặn xác suất bỏ sót" là trang "Kỹ thuật." ở `L01-4-04`, `L01-6-07` và được nhắc bằng tên ở `5-04`, `6-01`, `7-01`; tiêu đề trang cuối deck 01 trùng h1 deck 02. Ba chỗ nhỏ ở phát hiện 10, 11, 15 |

## 4. Phát hiện

| # | mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|---|
| 1 | trung bình | L02-5-01 → L02-5-02 | Câu nối then chốt của bài (cận cho $h$ cố định không chuyển sang $\hat h$, nên cần một biến cố đúng đồng thời cho mọi ứng viên) chỉ có trong ghi chú diễn giả. Mặt trang `5-01` kết thúc ở "Diễn giải: … thiên lệch do chọn", `5-02` mở ngay bằng định nghĩa mẫu đại diện. Vi phạm bài học deck 01 "Câu nối … phải có trên mặt trang". | Ghi chú diễn giả `5-01`: "Xác suất của một biến cố tính cho $h$ cố định không chuyển sang $\hat h$; cần một biến cố đúng cho mọi ứng viên cùng lúc." Ghi chú §6 dòng 594 ("nên chúng ta cần một cận đúng đồng thời cho mọi $h\in\mathcal H$") và dòng 621–624. | Thêm dòng đầu `5-02` (41 âm tiết, 4 dòng, còn chỗ): "Ứng viên được chọn theo $S$, nên cần một biến cố đúng đồng thời cho mọi $h\in\mathcal H$." |
| 2 | trung bình | L02-5-08 → L02-5-09 | Câu nối §7 (Định lý 02.14 mới chặn $L_D(\hat h)$ bằng $L_S(\hat h)$ cộng bán kính; rủi ro vượt mức cần so với mức tốt nhất trong lớp, nhờ (O1)) chỉ ở ghi chú diễn giả `5-09`. Trên mặt trang, `5-09` chuyển sang rủi ro vượt mức mà không nói vì sao kết quả vừa có chưa đủ. | Ghi chú diễn giả `5-09`: "Định lý 02.14 chặn $L_D(\hat h)$ bằng $L_S(\hat h)$ cộng một bán kính, nhưng chưa so $L_D(\hat h)$ với mức tốt nhất trong lớp". Ghi chú §7 dòng 762: "Bước còn lại là chuyển cận đồng thời của Định lý 02.14 thành cận cho rủi ro vượt mức … dùng giả thiết tối ưu (O1) hoặc (O2)." | `5-09` đã 56 âm tiết, 6 dòng; đặt câu ở cuối `5-08` (37 âm tiết): "Rủi ro vượt mức so $L_D(\hat h)$ với $\min_{h\in\mathcal H}L_D(h)$, không với $L_S(\hat h)$." Có thể bỏ vế "gấp năm lần $K$ thêm khoảng $0{,}005$" của Diễn giải để giữ mật độ (vế này mang số làm tròn còn chờ tác giả, xem mục 5). |
| 3 | trung bình | L02-5-08 (và L02-7-02) | Câu hỏi thứ hai của ví dụ dẫn nhập `1-06` ("khi $h$ được chọn trong $1000$ ứng viên") không được trả lời bằng lời trên mặt trang. `4-05` trả lời câu thứ nhất rõ ràng ("rủi ro kì vọng không quá khoảng $8{,}9\%$"), còn `5-08` chỉ ghi "cận trên $0{,}1204$" và Diễn giải nói về bán kính; `7-02` không nhắc ví dụ dẫn nhập. Vòng mở–đóng của ví dụ dẫn nhập chỉ khép trong ghi chú diễn giả. | Ghi chú diễn giả `5-08`: "Đây là câu trả lời cho câu hỏi thứ hai về tỉ lệ lỗi $5\%$ … khoảng $12\%$ cho hàm chọn trong $1000$ ứng viên". Storyboard `5-08`: "ví dụ, trả lời câu hỏi mở đầu". Ghi chú Ví dụ 02.8. | Diễn giải `5-08` (chỉ dùng số trên trang): "Diễn giải: với độ tin cậy $95\%$, hàm chọn trong $1000$ ứng viên có rủi ro kì vọng không quá $0{,}1204$; bán kính tăng từ $0{,}0387$ ($K=1$) lên $0{,}0704$ ($K=1000$)." |
| 4 | trung bình | L02-3-04 (nối mạch 2 → 3 → 4) | Trang so ba cận (Ví dụ 02.4 Bước 2–3) đã bị bỏ, phần so sánh chỉ còn trong ghi chú diễn giả `3-04`. Mặt trang `2-06` kết thúc "cần dùng thêm tính bị chặn" và dòng dẫn `3-00` hứa cận "giảm theo hàm mũ", nhưng con số đầu tiên của Hoeffding trên mặt trang ($0{,}2707$ ở $m=100$) lớn hơn hai cận Chebyshev $0{,}1716$, $0{,}25$ của `2-06`, và không trang nào nói điều đó. Người nghe thấy kết quả mạch 3 có vẻ trái với lời hứa của chính mạch 3; mục tiêu 2 ("So sánh xác suất đuôi với các cận") không có trang nào đặt ba cận cạnh nhau. Lợi ích chỉ hiện ra ở bảng cỡ mẫu `4-04`. | `2-06`: Chebyshev $0{,}1716$; $0{,}25$ ở $m=100$. `3-04`: "$2e^{-2}\approx0{,}2707$ ở $m=100$; $2e^{-4}\approx0{,}0366$ ở $m=200$". Ghi chú Ví dụ 02.4 Bước 3: "Ở $m=100$, cả hai cận Chebyshev nhỏ hơn cận Hoeffding. Ở $m=200$, cận Hoeffding nhỏ nhất." `review-log.md`: "bỏ trang so ba cận cũ 4-04 (nội dung chuyển vào ghi chú diễn giả 3-04)". | Trên `3-04`, thay dòng "Ví dụ." bằng một bảng nhỏ (số trong bảng không tính âm tiết): hàng "chính xác", "Chebyshev $25/m$", "Hoeffding" × cột $m=100$, $m=200$, rồi một dòng "Diễn giải: ở $m=100$ cận Hoeffding lớn hơn cận Chebyshev; ở $m=200$ nhỏ hơn." Nếu không đủ chỗ, đặt hai dòng này ở `4-04` trên bảng cỡ mẫu. |
| 5 | trung bình | L02-7-01 | Hàng Markov, Chebyshev ghi "Giả thiết không được bỏ: $V\ge0$; độc lập", trong khi `2-05` nói trên mặt trang "chỉ cần các $V_i$ không tương quan từng đôi". Hai trang của cùng deck nói ngược nhau về một giả thiết; Bài tập 02.1(b) đúng là điểm này. | `2-05`: "Độc lập chỉ dùng ở bước 3; chỉ cần các $V_i$ không tương quan từng đôi". Storyboard `7-01` dự kiến: "$V\ge0$; độc lập hoặc không tương quan cho trung bình". | Sửa ô thành "$V\ge0$; không tương quan từng đôi". |
| 6 | nhẹ | L02-4-01 → L02-4-02 | Kết luận của câu hỏi `4-01` ($L_S(h)$ không phải cận trên tin cậy) dẫn sang bán kính chỉ trong ghi chú diễn giả; mặt trang `4-02` mở bằng "Bán kính tin cậy giảm như $1/\sqrt m$" mà không nói bán kính dùng để làm gì. | Ghi chú diễn giả `4-01`: "muốn có cận trên tin cậy, cần cộng thêm một bán kính". | Dòng "Trực quan." của `4-02`: "Cộng vào $L_S(h)$ một bán kính tin cậy (confidence radius); bán kính giảm như $1/\sqrt m$." |
| 7 | nhẹ | L02-4-05, L02-4-06 | Điều kiện "$h$ cố định trước khi xem $S$" xuất hiện hai lần trên `4-05` (dòng đầu và dòng cuối) và một lần trên `4-03`, nhưng ranh giới mạch 4 → 5 nằm sau `4-06` (phản ví dụ (T1), (T3)), nên câu nối sang mạch 5 không đứng ở cuối mạch. | `4-05` dòng 1: "$h$ cố định trước khi xem mẫu xác thực $S$"; dòng 5: "Bảo đảm cần $h$ cố định trước khi xem $S$." | Bỏ dòng cuối `4-05`; nếu mật độ `4-06` cho phép, khép mạch bằng "Hệ quả 02.10 cần (T1), (T3) và $h$ cố định trước khi xem $S$." Nếu không, giữ như hiện tại: dòng dẫn `5-00` và ví dụ `5-01` đủ nối. |
| 8 | nhẹ | L02-2-03 → L02-2-04 | Lý do chuyển từ xác suất đuôi chính xác sang cận đuôi (các số chỉ tính được vì biết $D_\eta$) chỉ ở ghi chú diễn giả. | Ghi chú diễn giả `2-03`: "Các số này tính được vì đã biết $D_\eta$. Một cận đuôi có ích khi nó nhỏ hơn $1$ và tính được mà không cần biết phân bố." | `2-03` có 30 âm tiết; thêm "Các số trên dùng $D_\eta$; cận đuôi phải tính được khi chưa biết $D$." |
| 9 | nhẹ | L02-2-00, L02-2-01, L02-2-02 | Mạch 2 chứa khung chung của cả bài (§1–§3: giả thiết, bốn đại lượng, ví dụ xuyên suốt), nhưng tiêu đề, dòng dẫn và từ khóa mạch chỉ nói về §4. Hai trang đầu mạch phục vụ toàn bài, không phục vụ câu hỏi của mạch. | `2-00` từ khóa: "xác suất đuôi · cận đuôi · bất đẳng thức Markov · bất đẳng thức Chebyshev"; storyboard mục 3: mạch 2 ↔ §1–§4. | Chấp nhận được. Nếu sửa: chuyển `2-01`, `2-02` về cuối mạch 1 (deck 01 đặt (T1), (T2) ở trang "Tiên quyết và quy ước"), hoặc thêm "giả thiết (T1)–(T4)" vào dòng từ khóa mạch 2. |
| 10 | nhẹ | L02-6-01 | Dòng "Nhắc lại: chặn xác suất bỏ sót … (Bài 01)" đứng cuối trang, sau công thức đã dùng nó; $D_f$ được nhắc kèm định nghĩa trong ngoặc mà không có nhãn "Nhắc lại:" (khác `2-02` nhắc $S_\eta$ bằng nhãn). | Thứ tự trên `6-01`: Ví dụ → định nghĩa → Trực quan + công thức $(1-\epsilon)^m\le e^{-\epsilon m}$ → Nhắc lại. | Đưa dòng "Nhắc lại:" lên đầu trang và gộp: "Nhắc lại: $D_f$ ($D_{\mathcal X}$ đều, $Y=h_3(X)$); chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ (Bài 01)." |
| 11 | nhẹ | L02-6-04 | Hàng "$30=\lceil\ln20/0{,}1\rceil$ · $A_{\max}$ · hàm ngưỡng · mọi" là Mệnh đề 01.31 của Bài 01 (deck 01 `L01-6-05`: "cỡ chung $30$"), nhưng không ghi nguồn; người học không thấy đây là số đã gặp. | Deck 01 `L01-6-05`, `L01-7-01`: "Mệnh đề 01.31 … $m_{A_{\max}}\le\lceil\ln(1/\delta)/\epsilon\rceil$". | Ghi "$30$ (Mệnh đề 01.31)" trong ô cỡ mẫu. |
| 12 | nhẹ | L02-7-05 | Bài tập 02.6 xếp vào hàng "Lớp hữu hạn trong trường hợp khả diễn", nhưng bài chỉ cần Hệ quả 02.10, Định lý 02.14 và cấu trúc Bài tập 02.4 (mạch 5); họ đếm được có trọng số là nội dung bài chứng minh, không phải kiến thức bài cần. Ghi chú diễn giả `5-05` cũng nói "Bài tập 02.6 làm chi tiết" ở mạch 5. Trái với chính câu "Mỗi bài xếp vào phần cung cấp kiến thức cuối cùng mà bài cần" trong ghi chú diễn giả `7-05`. | `exercises.md` Bài tập 02.6: dùng (T1)–(T3), Định lý 02.14(a), Bài tập 02.4; không dùng khả diễn. | Chuyển 02.6 sang hàng "Hội tụ đều và rủi ro vượt mức trên lớp hữu hạn" (02.3, 02.4, 02.5, 02.6, 02.11). Nếu điều phối viên coi `6-08` là nơi cung cấp ý tưởng họ đếm được, giữ nguyên và sửa ghi chú diễn giả `5-05` cho khớp. |
| 13 | nhẹ | L02-7-00 (ghi chú diễn giả) | Ghi chú diễn giả trang tiêu đề mạch nói về chính các trang ("Các trang cuối gom …", "Không có khái niệm mới.") thay cho nội dung. | `7-00` ghi chú diễn giả. Bài học deck 01: ghi chú diễn giả trang tiêu đề mạch viết bằng câu thường về nội dung. | Ví dụ: "Sáu kết quả của bài dựa trên ba giả thiết: quan sát độc lập, hàm lỗi bị chặn, lớp giả thuyết chọn trước khi lấy mẫu. Số ứng viên vào cỡ mẫu qua $\ln K$, độ chính xác qua $1/\epsilon$ hoặc $1/\epsilon^2$." |
| 14 | nhẹ | L02-1-03 | Mục tiêu 6 "hoặc hệ số số ứng viên" đọc như lỗi gõ và mất ý "hệ số đếm số ứng viên trong bất đẳng thức hợp" của ghi chú; mục tiêu 6 là căn cứ của phản ví dụ `5-06`/`5-07`. | Ghi chú, Mục tiêu học tập 6: "… hoặc hệ số đếm số ứng viên trong bất đẳng thức hợp." Trang đang 79/80 âm tiết. | "Dựng phản ví dụ khi bỏ độc lập, bị chặn hoặc hệ số đếm ứng viên." (cùng số âm tiết). |
| 15 | nhẹ | Liên tục với deck 01 (`L01-7-06`, ghi chú diễn giả) | Deck 01 dẫn sang Bài 02 bằng "$\Pr(\lvert L_S(h)-L_D(h)\rvert>\epsilon)$", còn ghi chú và deck 02 dùng "$\ge\epsilon$" (Định nghĩa 02.1, Hệ quả 02.10(a), `2-03`, `4-02`). | `L01-7-06` ghi chú diễn giả; `2-03`: "$\Pr(\lvert V-\mathbb EV\rvert\ge\epsilon)$". | Báo người sửa deck 01: đổi thành "$\ge\epsilon$". |
| 16 | nhẹ | L02-3-01, L02-3-03 (ghi chú diễn giả) | Phản ví dụ đuôi nặng $\Pr(V=j)=c/j^3$ lặp ở ghi chú diễn giả `3-01` và `3-03`, cộng dòng mặt trang `3-03`. | Hai ghi chú diễn giả cùng câu "$\mathbb Ee^{\tau V}=\infty$ với mọi $\tau>0$". | Giữ ở `3-03` (nơi có dòng "Bỏ tính bị chặn"), bỏ ở `3-01`. |
| 17 | nhẹ | L02-7-03 ↔ L02-5-09 | `7-03` (câu chữ Bài tập 02.11) so với "cỡ mẫu $1097$ của Ví dụ 02.9", nhưng trên mặt trang `5-09` số $1097$ đứng sau nhãn "Ví dụ." không số hiệu, nên người học không nối được hai trang. | `5-09`: "Ví dụ. Sáu hàm ngưỡng, $\epsilon=0{,}1$, $\delta=0{,}05$: $M=\lceil1096{,}1\rceil=1097$". | Trên `5-09` ghi "(Ví dụ 02.9)" sau dòng ví dụ; câu chữ `7-03` giữ nguyên theo `exercises.md`. |

Tổng: 0 chặn bàn giao, 0 nghiêm trọng, 5 trung bình, 12 nhẹ.

## 5. Đề xuất sửa ghi chú

Không có đề xuất mới. Đề xuất đã ghi ở `review-log.md` vẫn ảnh hưởng tới deck: Ví dụ 02.8 ghi "khoảng $0{,}005$" cho phần bán kính tăng khi gấp năm lần $K$, giá trị là $0{,}0759-0{,}0704=0{,}0055$; Diễn giải `5-08` chép số này. Đề xuất ở phát hiện 2–3 (viết lại Diễn giải `5-08`) bỏ vế đó, nên deck không còn phụ thuộc vào số chờ tác giả.

## Kết luận

**đạt khi sửa.** Bảy mạch khớp thứ tự và nhóm mục của ghi chú; liên kết "Nội dung", viewer và bài sau đúng; hai trang "Vấn đề trung tâm" đúng khuôn; mạch Tổng kết không thêm khái niệm; liên tục với deck 01 tốt. Cần sửa năm chỗ trung bình: ba câu nối chỉ nằm trong ghi chú diễn giả (`5-01`→`5-02`, `5-08`→`5-09`, so sánh Hoeffding với Chebyshev ở `3-04`), câu trả lời trên mặt trang cho câu hỏi thứ hai của ví dụ dẫn nhập (`5-08`), và ô "độc lập" của `7-01` mâu thuẫn với `2-05`.
