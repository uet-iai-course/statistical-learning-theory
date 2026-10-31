# Rà lại 4b — Sư phạm và văn phong của bộ bài tập Bài 07 sau vòng sửa 1

Đối tượng: `lec07-ex-r1-frozen.md` (889 dòng, 9911 tiếng). Tệp này trùng `2627-1/materials/lec-07/exercises.md` (`diff -q` rỗng). Căn cứ: `lec07-ex-r1.udiff`, `reviews/11-quyet-dinh-bai-tap.md`, `bai-tap-ghi-chu.md` §8, bản rà trước `10-bai-tap-su-pham.md`. Chế độ `no-ai-slop`: Detect. Số dòng ở mục 2 là số dòng của `lec07-ex-r1-frozen.md`. Người rà chỉ đọc, không commit.

**Tổng kết:**
- Phát hiện cũ: 25. Đã xử lý 24 (✓). Một mục được giữ nguyên với lý do chấp nhận được (tiêu đề 07.5, ✗). Một mục đã xử lý nhưng theo cách khác đề xuất ($\theta_{\mathrm{II}}$ thay cho $\theta'$, theo quyết định của điều phối viên; tính là ✓).
- Phát hiện mới: 0 chặn bàn giao, 0 nghiêm trọng, 0 trung bình, 3 nhẹ.
- Phủ mục tiêu và loại bài không đổi: năm mục tiêu, năm loại bài, như bảng ở `10-bai-tap-su-pham.md`.
- Ngoài phạm vi tệp bài tập, tôi đã kiểm hai chỗ liên quan. §11 của ghi chú (dòng 932) đã đổi thành "lớp hàm hợp". `thuat-ngu.md` dòng 380 đã có đủ ba thuật ngữ "hàm kích hoạt ngưỡng", "lớp tích", "lớp hàm hợp".

## 1. Phát hiện cũ

| # | Phát hiện (`10-bai-tap-su-pham.md`) | Trạng thái | Bằng chứng trên bản mới |
|---|---|---|---|
| 1 | "lớp hợp" hai nghĩa | ✓ | Đã đổi ở tiêu đề 07.8, đề, gợi ý, lời giải (a) và §11 của ghi chú. Câu ở Bước 3 thành "Lực lượng của hợp các tập $(\mathcal H_2)_u$ không quá tổng lực lượng của chúng". Còn "hợp" ở Gợi ý 1 (c) ("Viết $h_\theta$ thành hợp của …") đúng nghĩa hợp thành hàm, không gây lẫn. |
| 2 | $\tau_{\mathcal H}$ của UML trong 07.8(b) | ✓ | Dòng 764 viết "hàm tăng trưởng theo định nghĩa đó không xác định tại $m=3$". Kí hiệu $\tau_{\mathcal H}$ chỉ còn ở dòng 11, nơi nó được nêu là kí hiệu của UML. |
| 3 | Gợi ý 1 lộ lời giải (07.4(d), 07.7(b)) | ✓ | Gợi ý 1 mới chỉ nêu hướng: 07.4(d) "tìm một đẳng thức hay một cận trong chứng minh sẽ sai khi bỏ giả thiết đó"; 07.7(b) "Với $m=1$, tìm điểm mà tại đó mỗi lớp đạt $\Pi(1)=2$". Câu cũ đã chuyển xuống Gợi ý 2, nên các gợi ý tăng dần. |
| 4 | 07.6(b) Bước 1, câu 88 tiếng | ✓ | Dòng 626 thành một câu dẫn và ba dòng có nhãn song song (Hai loại nhãn, Lỗi kiểm tra, Số hạng Rademacher). |
| 5 | $\vartheta_i$ | ✓ | Thay bằng $\Delta\mu_i$, định nghĩa ngay ở Bước 1 của 07.9(a). |
| 6 | $\mathcal H_{(1)}$, $\mathcal H_{(2)}$ | ✓ | 07.8(c) Bước 1–2 dùng "$\mathcal H_2\circ\mathcal H_1$ của (a)". |
| 7 | $\bar n$ | ✓ | Đã thành $\bar B$ ở đề, gợi ý và bảng lời giải. |
| 8 | $\theta_{\mathrm{abs}}$ lộ kết quả | ✓ (khác đề xuất) | Đã thành $\theta_{\mathrm{II}}$ ("mạng thứ hai"), không còn lộ kết quả. |
| 9 | 07.7(c) câu định nghĩa chen giữa | ✓ | Định nghĩa "hàm kích hoạt ngưỡng" đã thành câu riêng. |
| 10 | Tiếng Anh ở lần đầu | ✓ | Đã thêm ở dòng 5 (rectified linear unit, score function, architecture class), dòng 7 (margin violation rate, minimum-norm interpolant), dòng 386 (permuted labels, đúng lần đầu "nhãn hoán vị" trong tệp) và dòng 538 (random seed, đúng lần đầu "hạt giống"). |
| 11 | 07.4(b) thiếu (T1) | ✓ | Đề và Bước 1 đều đã có (T1). |
| 12 | 07.4(a) câu 68 tiếng | ✓ | Dòng 386 tách thành hai câu, câu đầu 49 tiếng (danh sách sáu đại lượng nằm trong câu này). Có thể chấp nhận. |
| 13 | 07.6(b) "giảm rõ" | ✓ | Đề nêu tiêu chí (hiệu so với sai số chuẩn của hiệu). Gợi ý 2 chỉ còn cách tính sai số chuẩn. |
| 14 | 07.6 Kiểm tra lại dựa vào số không có trong bảng | ✓ | Kiểm bằng $11{,}85$ và $194{,}2\in[75,372]$ (Ví dụ 07.10). |
| 15 | 07.9 Kiểm tra lại dùng số đo bằng máy | ✓ | Đã cắt câu này. |
| 16 | 07.1 Kiểm tra lại có câu nhắc lại | ✓ | Đã cắt câu này. |
| 17 | 07.3(e) Bước 3 bỏ bước trung gian | ✓ | Có `aligned` ba dòng: biểu thức, phép thay số, kết quả. |
| 18 | 07.5(b) đề thiếu động từ | ✓ | Đã thêm "Chạy hạ gradient trên $F$, …". |
| 19 | 07.5(b) bước cơ sở quy nạp | ✓ | Bước cơ sở $t=1$ nay đứng trước bước quy nạp. |
| 20 | 07.9(d) sai đối tượng | ✓ | Đề phát biểu cho mọi hàm liên tục, viết $\tilde f$. Lý do không dùng $g$ ($g$ đã là hàm lỗi ở 07.2(b)) hợp lệ. |
| 21 | 07.9(d) Bước 2 bọc ý trong trích dẫn | ✓ | Đã tách thành hai câu thẳng, không còn trích dẫn. |
| 22 | 07.8(b) dồn hai trường hợp | ✓ | Đã tách thành ba bước. Tham chiếu "Bước 2" trong các bước mới gây mơ hồ (phát hiện mới N1). |
| 23 | "Vẫn vậy" | ✓ | Đã thành "Dù vậy". |
| 24 | In nghiêng "*tốt nhất*" | ✓ | Đã bỏ in nghiêng; câu dùng "giá trị lớn nhất". |
| 25 | Tiêu đề 07.5 | ✗ (chấp nhận) | Giữ nguyên, vì đổi tiêu đề kéo theo đổi §11 của ghi chú, ngoài phạm vi được giao (`bai-tap-ghi-chu.md` §8, mục 2). Đề xuất gốc vốn để điều phối viên quyết. |

## 2. Phát hiện mới (trên các đoạn đã đổi, ±1 đoạn)

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | 07.8(b) Bước 1–2, dòng 764 và 766 | Sau khi (b) có Bước 1–3 riêng, "Bước 2" trơn mơ hồ: ở dòng 766, cụm này nằm ngay trong Bước 2 của (b) nên đọc thành tự tham chiếu. Dòng 764 viết "Bước 2 của (a)" ở câu đầu nhưng chỉ viết "Bước 2" ở cuối câu. Câu của dòng 764 dài 55 tiếng (van-phong §9). | 764: "…, trong khi $\lvert(\mathcal H_2)_u\rvert\ge1$: Bước 2 không còn đúng."; 766: "…, và Bước 2 cần thêm tính không giảm của hàm tăng trưởng theo $m$." | 764: tách tại dấu hai chấm: "… trong khi $\lvert(\mathcal H_2)_u\rvert\ge1$. Do đó bất đẳng thức ở Bước 2 của (a) không còn đúng." 766: "…, và Bước 2 của (a) cần thêm tính không giảm của hàm tăng trưởng theo $m$." (+5) |
| nhẹ | 07.6(b) lời giải Bước 3, dòng 634 | Đoạn 93 tiếng dồn ba phép tính (hai sai số chuẩn của trung bình, sai số chuẩn của hiệu khi coi hai nhóm độc lập, sai số chuẩn ghép cặp) cùng kết luận (§7a). Con số ghép cặp $0{,}0019$ lấy từ các lần chạy riêng lẻ, không có trong ba bảng, nên người học không tính lại được. | "Sai số chuẩn của một trung bình … $\approx0{,}0013$ và … $\approx0{,}0016$. Coi hai nhóm như độc lập, … $\approx0{,}002$. Hai nhóm dùng chung mười hạt giống …; ghép cặp theo hạt giống (từ các lần chạy riêng lẻ) cho sai số chuẩn khoảng $0{,}0019$. Cả hai lớn hơn hiệu …" | Đặt ba phép tính vào một khối `aligned` ($0{,}0040/\sqrt{10}\approx0{,}0013$; $0{,}0050/\sqrt{10}\approx0{,}0016$; $\sqrt{0{,}0013^2+0{,}0016^2}\approx0{,}002$). Giữ câu ghép cặp làm câu riêng, thêm vế "(số này cần dữ liệu từng lần chạy, không có trong bảng)". Câu kết luận thành đoạn riêng. (khoảng +8; bù bằng cắt "Coi hai nhóm như độc lập," vì câu sau đã nói hai nhóm không độc lập, −5) |
| nhẹ | 07.6(b) Bước 1, dòng 630 | Dòng thứ ba của danh sách không có chủ ngữ, nên câu chỉ đúng nghĩa khi đọc liền với nhãn. | "- **Số hạng Rademacher.** Lớn hơn $1$ và tăng theo $m$." | "- **Số hạng Rademacher.** Số hạng này lớn hơn $1$ ở mọi $m$ và tăng theo $m$." (+5) |

Gợi ý 1 mới: tôi đã đọc lại cả chín khối. Không khối nào lộ lời giải; hai khối mới (07.4(d), 07.7(b)) chỉ nêu hướng tiếp cận.

Ngân sách: ba đề xuất mới thêm tổng khoảng +13 tiếng. Tệp sẽ khoảng 9 924 / 10 000.
