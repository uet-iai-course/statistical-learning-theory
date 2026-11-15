# Duyệt deck Bài 04 — Vai 5: mạch truyện và liên kết

Người duyệt: vai `mach-truyen` (chỉ đọc), 2026-11-15. Đối tượng: `2627-1/lecture-04-phan-tich-sai-so.html` (bản đóng băng, 55 trang). Đối chiếu: `materials/lec-04/lecture-note.md`, `materials/lec-04/exercises.md`, `planning/lec-04/storyboard.md` (mục 3, 12, 16), `planning/lec-04/review-log.md` § Bộ trang chiếu (N1, T1–T8), deck Bài 02, Bài 03 và storyboard Bài 03. Bảng kiểm liên tục: phần Outline / Threads / Concept của `quill/references/workflows.md` (không tạo `quill.json`).

## Kiểm tra máy đã chạy

Thư mục nháp: `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-04/rv-mach-truyen/` (`links.py`, `faces.txt`).

- **Trang "Nội dung" (Playwright, 1600×900).** Sáu liên kết `#/2` … `#/7` mở đúng `L04-2-00` … `L04-7-00` (cấu hình `hashOneBasedIndex: true`, 7 chồng ngang, 55 trang); nhấn chuột vào `#/4` từ `L04-1-04` cũng tới `L04-4-00`. Không có lỗi console hay lỗi trang.
- **Liên kết viewer (`L04-7-06`).** `material-viewer.html?doc=materials/lec-04/lecture-note.md&deck=lecture-04-phan-tich-sai-so.html` và bản `exercises.md`: HTTP 200, tiêu đề đúng Bài 04, có liên kết "Bộ trang chiếu" về deck này, 0 `.katex-error`, không yêu cầu thất bại.
- **Bài sau.** `L04-7-07` ghi "Bài 05: Hạ gradient, hạ gradient ngẫu nhiên và cận tối ưu.", đúng tiêu đề `materials/lec-05/lecture-note.md`; không có liên kết vì chưa có deck Bài 05, như deck Bài 02 và Bài 03.
- **`deck_lint.py`.** 1 phát hiện: `L04-7-03`, 76 > 60 âm tiết (ngoại lệ đã ghi ở storyboard mục 16).
- **Tiêu đề trang so với storyboard mục 6.** 55/55 khớp (so bằng script).
- **Từ khóa mạch trên mặt trang nội dung** (không tính trang tiêu đề mạch): mọi từ khóa của mạch 2, 3, 4, 6 có mặt; mạch 5 thiếu "cỡ mẫu theo lớp" và "xác suất thất bại giảm theo cỡ mẫu" (phát hiện 9).
- **Số hiệu dẫn trên mặt trang.** "Ví dụ 04.9" (`L04-4-12`, `L04-7-05`) và "Ví dụ 04.10" (`L04-6-05`) được dẫn nhưng không trang nào gắn hai số hiệu này (phát hiện 6). Mọi số hiệu khác dẫn trên mặt trang đã xuất hiện ở trang trước hoặc thuộc bài trước.

## Bảng chức năng từng trang

| Trang | Vai trò trong mạch | Kết nối vào | Kết nối ra |
|---|---|---|---|
| 1-01 | Bìa, luận điểm: rủi ro thực nghiệm chọn lớp lớn nhất; số hạng phạt hoặc mẫu xác thực chọn theo cỡ mẫu | Bài 03 (cận theo một lớp cố định, ghi chú diễn giả) | cả bài |
| 1-02 | Nhắc lại (T1)–(T5), (M), mẫu đại diện, $r_m$, $\rho_m$ | Định lý 02.14(a), 03.15(a) | 2-05, 2-07, 4-01 dùng hai bán kính |
| 1-03 | Năm mục tiêu, ứng với mạch 2–6 | — | mạch 2–6 |
| 1-04 | Nội dung, sáu liên kết `#/N` | — | 2-00 … 7-00 |
| 1-05 | Vấn đề trung tâm: một hộp "Câu hỏi:" chọn lớp theo cỡ mẫu | câu hỏi cầu nối của Bài 03 | 7-02 trả lời |
| 1-06 | Hai câu hỏi dẫn nhập: bậc đa thức; số chỉ số đo, cận $0{,}329\to0{,}560$ | Bài 03, §11 | 2-02 (hai ví dụ xuyên suốt) |
| 2-00 | Tiêu đề mạch: ba nguồn của cận | 1-06 | 2-01 |
| 2-01 | Thiết lập: họ lớp, bộ giải, cố định / ngẫu nhiên | 1-02 | 2-03, 2-04 |
| 2-02 | Hai ví dụ xuyên suốt (Ví dụ 04.1, ứng dụng) | 1-06 | 3-04 (Ví dụ 04.1), 2-07, 4-07 (ứng dụng) |
| 2-03 | Định nghĩa 04.1, Ví dụ 04.2 (hình F1) | 2-01 | 2-05 (sai số xấp xỉ, $L^*$) |
| 2-04 | Định nghĩa 04.2; (O1), (O2); "Lưu ý:" từ Nhận xét 04.4 | 2-03 | 2-05 ($\operatorname{opt}_S$) |
| 2-05 | Trực quan và phát biểu Mệnh đề 04.3 | 2-03, 2-04, 1-02 | 2-06, 2-07 |
| 2-06 | Ý tưởng chứng minh; nhắc lại bước tất định; Kết luận về Hệ quả 02.16(b), 03.16(b) | Bài 02, 2-05 | 4-09 (cùng kỹ thuật) |
| 2-07 | Ví dụ 04.3: so hai cận; Kết luận: cần chia $\delta$ | 2-05, 2-02 | 4-01 |
| 2-08 | Bài tập 04.1(b) | 2-04, 2-05 | — (kết mạch) |
| 3-00 | Tiêu đề mạch | 2-02 (bậc đa thức) | 3-01 |
| 3-01 | Định nghĩa 04.5 | 2-02 | 3-02 |
| 3-02 | Trực quan và phát biểu Mệnh đề 04.6 | 3-01 | 3-03, 3-04 |
| 3-03 | Ý tưởng chứng minh; Kỹ thuật (một dòng) | 3-02 | 3-05 (số hạng chéo) |
| 3-04 | Ví dụ 04.4: bậc tốt nhất theo $\sigma^2$ | 2-02, 3-02 | 7-02; câu nối sang mạch 4 thiếu (phát hiện 4) |
| 3-05 | Ví dụ 04.5: bỏ nhãn kiểm tra độc lập | 3-03 bước 4 | 7-01 |
| 3-06 | Nhận xét 04.7: độ chệch khác sai số xấp xỉ | 2-03, 3-01 | 3-07 |
| 3-07 | Bài tập 04.2(d): chiều ngược của 3-06 | 3-06 | — (kết mạch) |
| 4-00 | Tiêu đề mạch | 2-07 | 4-01 |
| 4-01 | Định nghĩa 04.8; câu mở: cần cận đồng thời cho mọi lớp | 2-07, 1-02 | 4-02 |
| 4-02 | (T6), Trực quan chia $\delta$, Bổ đề 04.9 | 4-01 | 4-03, 4-06 |
| 4-03 | Ý tưởng chứng minh; nhắc lại chia $\delta/K$ | 4-02, Bài 02 | 4-04, 4-05 |
| 4-04 | Kỹ thuật (trang riêng); Ví dụ 04.7 | 4-03 | 4-07 ($\mathrm{pen}_3$), 5-03 |
| 4-05 | Ví dụ 04.8: bỏ $\sum_kq_k\le1$ | 4-03 bước 3 | 7-01, 7-05 |
| 4-06 | Định nghĩa 04.10; câu mở nối với Bổ đề 04.9 | 4-02 | 4-07, 4-08 |
| 4-07 | Ví dụ 04.9 (bảng) và Thuật toán 04.12; SRM chọn $\hat k=3$ | 4-04, 4-06 | 4-10, 4-12, 6-03, 7-05 |
| 4-08 | Trực quan và phát biểu Định lý 04.11 | 4-06, 4-02 | 4-09, 4-10, 5-01 |
| 4-09 | Ý tưởng chứng minh; Kết luận về Hệ quả 03.16(a) | 4-08 | 4-11 (bỏ (T6)) |
| 4-10 | Ví dụ 04.9 Bước 2–5, hình F2: cận $0{,}3651$, so sánh | 4-07, 4-08 | 7-02 |
| 4-11 | Ví dụ 04.10: bỏ (T6) | 4-09 | 6-05 (cùng phân bố), 7-01 |
| 4-12 | Bài tập 04.4(b) | 4-07 | — (kết mạch) |
| 5-00 | Tiêu đề mạch | 4-08 | 5-01 |
| 5-01 | Câu mở: $\mathrm{pen}_k\to\infty$; nhắc lại học PAC bất khả diễn; Định nghĩa 04.14 | 4-08 | 5-02 |
| 5-02 | Trực quan ($\delta=1/m$) và phát biểu Hệ quả 04.15(a) | 5-01, 4-08 | 5-03, 5-04 |
| 5-03 | Ý tưởng chứng minh; Kỹ thuật (một dòng); cỡ mẫu bằng số | 5-02, 4-04 | 7-02 (ghi chú diễn giả) |
| 5-04 | Ví dụ 04.11; Định lý 04.16(a) (đọc thêm) | 5-02 | — (kết mạch) |
| 6-00 | Tiêu đề mạch | (ghi chú diễn giả: SRM trả phạt trên cùng $S$) | 6-01 |
| 6-01 | (T7), Trực quan và phát biểu Hệ quả 04.17 | câu nối sang mạch 6 thiếu trên mặt trang (phát hiện 5) | 6-02, 6-03 |
| 6-02 | Ý tưởng chứng minh; nhắc lại Hệ quả 02.16(a), Định lý 02.14(b) | 6-01, Bài 02 | 6-05 (bước 1 hỏng) |
| 6-03 | Ví dụ 04.12, hình F3 | 4-07 (mười ứng viên), 6-01 | 7-02 |
| 6-04 | Nhận xét 04.18; ví dụ $K=15$ bậc | 6-01, 1-06 (bậc đa thức) | 7-02 |
| 6-05 | Bài tập 04.5(a): bỏ (T7) | 4-11, 6-02 | — (kết mạch) |
| 7-00 | Tiêu đề mạch Tổng kết | mạch 4, 6 | 7-01 |
| 7-01 | Bảng tổng kết, sáu kết quả | 2-05 … 6-01 | 7-02 |
| 7-02 | Vấn đề trung tâm (trả lời) | 1-05 | 7-03 |
| 7-03 | Bài tập 04.7(c), đề | 2-05, 4-02, 4-06 | 7-04 |
| 7-04 | Lời giải Bài tập 04.7(c) | 7-03, 4-08 | — |
| 7-05 | Câu hỏi tự kiểm tra (gồm câu hỏi cuối buổi) | 2-04, 4-06, 3-06, 4-03 | — |
| 7-06 | Bài tập về nhà, bảng Mục–Bài tập, liên kết viewer | `exercises.md` | ghi chú, tệp bài tập |
| 7-07 | Tài liệu tham khảo; dòng Bài 05 | ghi chú §12 | Bài 05 |

## Bảng đối chiếu trang → mục ghi chú

| Mạch | Trang | Mục ghi chú | Khối theo thứ tự của ghi chú | Thứ tự |
|---|---|---|---|---|
| 1 | 1-01 … 1-06 | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết | — | khớp |
| 2 | 2-01 | §1, §2 | tám thành phần, bảng nguồn ngẫu nhiên | khớp |
| 2 | 2-02 | §3 | Ví dụ 04.1, ứng dụng | khớp |
| 2 | 2-03 | §4 | Định nghĩa 04.1, Ví dụ 04.2 | khớp |
| 2 | 2-04 | §4 | Định nghĩa 04.2; Nhận xét 04.4 thành "Lưu ý:" | Nhận xét 04.4 lên trước Mệnh đề 04.3, trong cùng §4 (storyboard mục 3); không phụ thuộc Mệnh đề 04.3 |
| 2 | 2-05, 2-06 | §4 | Mệnh đề 04.3 và chứng minh | khớp |
| 2 | 2-07 | §4 | Ví dụ 04.3 | khớp |
| 2 | 2-08 | §4 (tệp bài tập) | Bài tập 04.1(b) | — |
| 3 | 3-01 … 3-03 | §5 | Định nghĩa 04.5, Mệnh đề 04.6, chứng minh | khớp |
| 3 | 3-04, 3-05 | §5 | Ví dụ 04.4, 04.5 | khớp |
| 3 | 3-06 | §5 | Nhận xét 04.7 (Ví dụ 04.6 ở ghi chú diễn giả) | khớp |
| 3 | 3-07 | §5 (tệp bài tập) | Bài tập 04.2(d) | — |
| 4 | 4-01 … 4-03 | §6 | Định nghĩa 04.8, Bổ đề 04.9, chứng minh | khớp |
| 4 | 4-04, 4-05 | §6 | Ví dụ 04.7, 04.8 | khớp |
| 4 | 4-06 | §6 | Định nghĩa 04.10 | khớp |
| 4 | 4-07 | §6 | Ví dụ 04.9 Bước 1, Thuật toán 04.12 | lên trước Định lý 04.11 theo quyết định T5; trong cùng §6, chỉ cần Định nghĩa 04.10 và $\mathrm{pen}_k$ |
| 4 | 4-08, 4-09 | §6 | Định lý 04.11 và chứng minh | khớp với T5 |
| 4 | 4-10 | §6 | Ví dụ 04.9 Bước 2–5 | khớp với T5 |
| 4 | 4-11 | §6 | Ví dụ 04.10 (Nhận xét 04.13 ở ghi chú diễn giả) | khớp |
| 4 | 4-12 | §6 (tệp bài tập) | Bài tập 04.4(b) | — |
| 5 | 5-01 … 5-03 | §7 | Định nghĩa 04.14, Hệ quả 04.15, phần số sau nó | khớp |
| 5 | 5-04 | §7 | Ví dụ 04.11, Định lý 04.16 | khớp |
| 6 | 6-01, 6-02 | §2 (T7), §8 | Hệ quả 04.17 và chứng minh | khớp |
| 6 | 6-03, 6-04 | §8 | Ví dụ 04.12, Nhận xét 04.18 | khớp |
| 6 | 6-05 | §8 (tệp bài tập) | Bài tập 04.5(a) | — |
| 7 | 7-01 … 7-07 | §9–§12 | bảng tổng kết, §9, Bài tập 04.7(c), §11, §10, §12 | khớp |

Mỗi mạch ứng với các mục liên tiếp của ghi chú (1: phần mở; 2: §1–§4; 3: §5; 4: §6; 5: §7; 6: §8; 7: §9–§12). Hai chỗ đổi thứ tự đều nằm trong một mục và đã có quyết định hoặc ghi ở storyboard.

**Bảng `Mục | Bài tập` (7-06).** Mười ba bài, mỗi bài một lần (1 + 1 + 5 + 2 + 4). Mỗi bài nằm ở mạch cung cấp kiến thức cuối cùng nó cần: 04.7(c) và 04.10 cần SRM (mạch 4); 04.8(b) cần Hệ quả 04.15 (mạch 5); 04.6, 04.12, 04.13 cần mẫu xác thực (mạch 6). Khớp `exercises.md`.

**Năm trang bài tập** (2-08, 3-07, 4-12, 6-05, 7-03/7-04) lấy đúng câu hỏi và kết quả của `exercises.md` (04.1(b), 04.2(d), 04.4(b), 04.5(a), 04.7(c)); lời giải 7-04 khớp Bước 1–2 của lời giải 04.7(c).

**Liên tục với Bài 02–03.** Nhắc lại Định lý 02.14(a), 03.15(a) ở 1-02; Hệ quả 02.16(a), Định lý 02.14(b) ở 6-02; Hệ quả 02.16(b), 03.16(b) ở Kết luận 2-06; Hệ quả 03.16(a) ở Kết luận 4-09. Tên kỹ thuật: "bước tất định trên biến cố đại diện" (2-06) đúng tiêu đề `L02-5-11`; "chia $\delta/K$ cho từng giả thuyết (Bài 02)" (4-03) đúng câu nhắc lại của deck Bài 03; "đảo cận đuôi thành cỡ mẫu" (6-03) rút gọn tên `L02-4-04` (phát hiện 17). Ví dụ xuyên suốt $D_\eta$, $h_t$, $S_\eta$ ở 2-03, 2-04, 2-08 giữ số liệu Bài 01 ($0{,}18$; $0{,}22$; $0{,}32$; bảng $L_{S_\eta}$). Câu hỏi cho Bài 04 ở cuối deck Bài 03 (`L03-7-06`, ghi chú diễn giả: "nên chọn lớp nào giữa các lớp lồng nhau như vậy?", $0{,}329\to0{,}560$) được nhận đúng ở 1-05, 1-06.

**Mạch chủ đề mở và đóng (Threads).**

| Mạch chủ đề | Mở trên mặt trang | Đóng trên mặt trang |
|---|---|---|
| Chọn số chỉ số đo | 1-06, 2-02 | 4-07, 4-10, 7-02 |
| Chọn bậc đa thức | 1-06 | 3-04 (bậc theo $\sigma^2$), 6-04 ($K=15$), 7-02 |
| Cần chia $\delta$ giữa các lớp | 2-07 | 4-02, 4-03, 4-04 |
| Hàm lỗi bình phương không bị chặn, cận Bài 02–03 không áp dụng | chỉ ở ghi chú diễn giả 1-06, 3-00 | 6-04, 7-02 (phát hiện 3) |
| Sai số xấp xỉ không quan sát được, $2r$ tính được | không có trên mặt trang | không có (phát hiện 2, 10) |
| SRM trả phạt trên cùng tập huấn luyện, xác thực trả bằng dữ liệu giữ lại | chỉ ở ghi chú diễn giả 6-00 | 7-00 ("mỗi cách cần giả thiết riêng") (phát hiện 5) |
| Học được không đều không kéo theo học được PAC | 5-00 (ghi chú diễn giả) | 5-04 ngầm, chỉ ở ghi chú diễn giả (phát hiện 15) |

**Kiểm các quy định mạch.** Trang "Vấn đề trung tâm" mở đầu có một hộp "Câu hỏi:" và trang cuối 7-02 trả lời cho cả bài, không theo từng mạch. Mạch "Tổng kết" không thêm khái niệm trên mặt trang. Không có mặt trang nào xem trước bài sau (chỉ dòng Bài 05 ở 7-07; "Bài 07" chỉ ở ghi chú diễn giả 4-04). Bảy dòng dẫn mạch là câu trần thuật, không lặp một khuôn.

## Phát hiện

Số âm tiết dẫn theo storyboard mục 16 ("Mật độ cuối"); người sửa đếm lại sau khi thêm chữ.

| # | Mức độ | Trang chiếu | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|---|
| 1 | trung bình | L04-2-03 (và 2-01) | Câu hỏi của mạch 2 không có trên mặt trang: vì sao cần một rủi ro tham chiếu chung, và mục đích tách rủi ro thành phần không tăng theo lớp và phần có cận tăng theo lớp. Hai câu này chỉ ở ghi chú diễn giả 2-00 và 2-03; 2-01, 2-02, 2-03 vào thẳng định nghĩa. | Ghi chú §4, câu mở: "Khi lớp thay đổi, đối tượng so sánh $\inf_{h\in\mathcal H}L_D(h)$ cũng đổi theo, nên chúng ta cần một mức tham chiếu chung"; §3, câu cuối: "chúng ta cần tách rủi ro của hàm học được thành một phần không tăng theo lớp và một phần mà cận của nó tăng theo lớp". Storyboard mục 16, dòng 2-03: "dòng mở 'Lớp thay đổi thì …' sang ghi chú diễn giả". | Thêm lại một dòng mở trên 2-03 (47 âm tiết, còn chỗ): "Lớp thay đổi thì $\inf_{h\in\mathcal H}L_D(h)$ đổi theo; so nhiều lớp cần một mức tham chiếu chung." |
| 2 | trung bình | L04-2-07 | Ý trọng tâm của deck (sai số xấp xỉ không tăng theo lớp nhưng không quan sát được; $2r$ tăng theo lớp nhưng tính được) không xuất hiện trên mặt trang nào. 2-07 chỉ có "$a_{10}\le a_2$, cả hai chưa biết"; câu "chỉ phần thống kê tính được" nằm ở ghi chú diễn giả 1-05. | Ghi chú, đoạn cuối §4: "sai số xấp xỉ không tăng khi lớp lớn hơn nhưng không quan sát được, còn số hạng $2r$ tăng theo lớp nhưng tính được. Số hạng tính được là cơ sở của một quy tắc chọn lớp."; Ví dụ 04.3, "Tóm lại, chỉ phần thống kê của hai cận tính được". Storyboard mục 2 gọi đây là "trọng tâm trực quan của deck". Tìm "quan sát được", "tính được" trên các mặt trang: 0 kết quả. | Trên 2-07, đổi "$a_{10}\le a_2$, cả hai chưa biết" thành "$a_{10}\le a_2$ không quan sát được, phần $2\rho_m+\epsilon_{\mathrm{opt}}$ tính được" (khoảng +5 âm tiết, 2-07 đang 56; nếu vượt 60, chuyển "$1\le d\le m$" của dòng nhắc lại vào ghi chú diễn giả). Xem thêm phát hiện 10. |
| 3 | trung bình | L04-3-01 (3-00) | Câu nối mạch 2 → 3 thiếu trên mặt trang: lý do chuyển sang một đẳng thức kì vọng (Mệnh đề 04.3 cần (T3), hàm lỗi bình phương không bị chặn; rủi ro thực nghiệm luôn chọn bậc 2). Mặt trang 3-01 chỉ viết "Với hàm lỗi bình phương, so các bậc qua lỗi trên một nhãn mới tại một điểm."; lý do ở ghi chú diễn giả 3-00 và 1-06. Mạch chủ đề "cận của Bài 02–03 không áp dụng cho hàm lỗi bình phương" vì vậy chỉ được đóng (6-04, 7-02) mà chưa được mở trên mặt trang. | Ghi chú §5, câu mở: "Ở Ví dụ 04.1, rủi ro thực nghiệm luôn chọn bậc $2$, còn Mệnh đề 04.3 cần hàm lỗi bị chặn. Để so các bậc trên một nhãn mới, chúng ta dùng một đẳng thức khác …". Common brief: "Câu nối giữa hai mạch … phải có trên mặt trang, không chỉ trong ghi chú diễn giả." | Câu mở 3-01: "Mệnh đề 04.3 cần (T3), hàm lỗi bình phương không bị chặn: so các bậc qua lỗi trên một nhãn mới tại một điểm." 3-01 đang 57 âm tiết và định nghĩa không rút được điều kiện nào; nếu vượt 60, giữ câu mở hiện tại và sửa dòng cuối 3-02 thành "Đúng cả khi hàm lỗi không bị chặn, khác Mệnh đề 04.3." (3-02 đang 59; người sửa đếm lại). |
| 4 | trung bình | L04-3-04 | Câu nối mạch 3 → 4 thiếu trên mặt trang: phân tích độ chệch–phương sai không cho quy tắc chọn bậc từ dữ liệu vì $f^*$, $\sigma^2$ chưa biết. Kết luận 3-04 chỉ nêu bậc tốt nhất theo $\sigma^2$ và "rủi ro thực nghiệm chọn bậc $2$"; câu "hai đại lượng chưa biết" chỉ ở ghi chú diễn giả. Mạch 4 vì vậy mở mà không có lý do từ mạch 3. | Ghi chú, câu cuối §5: "Phân tích độ chệch–phương sai giải thích vì sao bậc cao không luôn tốt hơn, nhưng không cho một quy tắc chọn từ dữ liệu, vì $f^*$ và $\sigma^2$ chưa biết." Storyboard mục 3, mạch 3, cột "Đầu ra": "không cho quy tắc chọn từ dữ liệu". | Kết luận 3-04 (29 âm tiết): "bậc tốt nhất: $0$ ($\sigma^2=1$), $2$ ($\sigma^2=0{,}1$); rủi ro thực nghiệm chọn bậc $2$; $\sigma^2$, $f^*$ chưa biết nên không chọn được bậc từ dữ liệu." |
| 5 | trung bình | L04-6-01 (6-00) | Câu nối sang mạch 6 thiếu trên mặt trang: SRM chọn trên chính tập huấn luyện và trả bằng số hạng phạt; mẫu xác thực trả bằng phần dữ liệu không dùng để huấn luyện. Câu này chỉ ở ghi chú diễn giả 6-00; 6-01 mở bằng "Mẫu xác thực … chỉ để chọn". Bảng tổng kết và 7-02 cũng không nêu giá của mẫu xác thực (dữ liệu giữ lại). | Ghi chú §8, câu mở: "SRM dùng cùng một tập huấn luyện để huấn luyện và để chọn lớp, và trả giá bằng số hạng phạt. Khi có thêm một mẫu xác thực chỉ dùng để chọn …"; §9: "Xác thực trả $2\sqrt{\ln(2K/\delta)/(2m_v)}$ cộng phần dữ liệu không dùng để huấn luyện …, còn SRM trả số hạng phạt trên toàn bộ tập huấn luyện." | Trực quan 6-01: "SRM chọn trên chính $S$, trả $\mathrm{pen}_k$. Mẫu xác thực (validation sample) chỉ để chọn: chọn mô hình (model selection) là ERM trên $K$ ứng viên." 6-01 đang 59: bỏ "ứng viên là hàm của $S$" ở dòng (T7), vì dòng Giả thiết đã có "$g_1,\ldots,g_K$ là hàm đo được của $S$". |
| 6 | trung bình | L04-4-07, L04-4-11 (dẫn ở 4-12, 6-05, 7-05) | Mặt trang 4-12 ("mười lớp của Ví dụ 04.9"), 7-05 ("Ví dụ 04.9 với …") và 6-05 ("Phân bố của Ví dụ 04.10") dẫn hai số hiệu không gắn trên trang nào; tiêu đề 4-07, 4-11 không có số. Người chỉ xem deck không tìm được khối được dẫn. 2-02 làm đúng ("**Ví dụ 04.1.**"). 4-10 tiếp Ví dụ 04.9 mà không ghi là phần tiếp, và dòng "tổng nhỏ nhất tại $k=3$" lặp "SRM chọn $\hat k=3$" của 4-07. | Tìm số hiệu trên mặt trang: "Ví dụ 04.9" chỉ ở 4-12, 7-05; "Ví dụ 04.10" chỉ ở 6-05. Quy định "Define or recall before use … every … result on a slide face is introduced on an earlier slide". Câu chữ của Bài tập 04.4(b), 04.5(a) và §11 dùng hai số hiệu này, nên giữ ở trang bài tập. | Mở dòng đầu 4-07 bằng "**Ví dụ 04.9.**", 4-11 bằng "**Ví dụ 04.10.**" (mỗi chỗ +3 âm tiết; 4-11 đang 57, nên người sửa đếm lại). Trực quan 4-10: "Ví dụ 04.9 (tiếp): $L_S(\hat h_k)$ giảm, $\mathrm{pen}_k$ tăng; tổng nhỏ nhất tại $k=3$." |
| 7 | trung bình | L04-5-03 (5-02) | Phần (b) của Hệ quả 04.15 không được phát biểu trên mặt trang nào: 5-02 chỉ có "Bảo đảm: (a) …"; bước 4 của 5-03 chứng minh "Phần (b), $k_{\max}$ lớp: $M(\epsilon,\delta)=\ldots$" mà không nói (b) khẳng định gì. Trang ý tưởng chứng minh vì vậy chứng minh một khẳng định người đọc chưa thấy; mục tiêu 4 ("so với học PAC") mất nửa so sánh trên mặt trang. | Ghi chú, Hệ quả 04.15(b): "Nếu danh sách có $k_{\max}$ lớp, $A_{\mathrm{SRM}}$ là thuật toán học PAC bất khả diễn cho $\mathcal H$ với $M(\epsilon,\delta)=\ldots$". Quyết định N1: "phần (b) sang bước 4 của 5-03", nên bước 4 phải mang phát biểu. 5-03 đang 39 âm tiết. | Bước 4 của 5-03: "(b) $k_{\max}$ lớp: $A_{\mathrm{SRM}}$ học PAC bất khả diễn với $M(\epsilon,\delta)=\max\{\lceil1/\delta\rceil,\max_kM_k(\epsilon)\}$; lấy $\inf_h$." |
| 8 | trung bình | L04-5-00 | Dòng dẫn mạch "Cỡ mẫu cần thiết được phép phụ thuộc hàm làm mốc so sánh, nhưng không phụ thuộc phân bố." dùng "cần thiết", trái với cách ghi chú và chính ghi chú diễn giả 5-03 phân biệt cỡ mẫu đủ với cỡ mẫu cần; "hàm làm mốc so sánh" lệch thuật ngữ "giả thuyết so sánh" của Định nghĩa 04.14 và từ khóa của mạch. | Định nghĩa 04.14: $M(\epsilon,\delta,h)$ là ngưỡng cỡ mẫu đủ ("mọi $m\ge M(\epsilon,\delta,h)$"); ghi chú §7: "cỡ mẫu đủ theo cận"; ghi chú diễn giả 5-03: "Các số là cỡ mẫu đủ theo một cận trên, không phải cỡ mẫu cần." | "Cỡ mẫu đủ được phép phụ thuộc giả thuyết so sánh, nhưng không phụ thuộc phân bố." |
| 9 | trung bình | L04-5-01, L04-5-02 | Hai từ khóa của mạch 5, "cỡ mẫu theo lớp" và "xác suất thất bại giảm theo cỡ mẫu", không có trên mặt trang nội dung nào (ý có qua công thức $\delta=1/m$, $M_{k(h)}(\epsilon)$). | `strand-keys` của 5-00; tìm hai cụm trên các mặt trang trừ trang tiêu đề mạch: 0 kết quả. Common brief, bài học deck 01: "từ khóa mạch phải xuất hiện trên một mặt trang nội dung." | Trực quan 5-02: "SRM nhận $\delta$; Định nghĩa 04.14 đòi thuật toán cố định trước $\delta$: cho xác suất thất bại giảm theo cỡ mẫu, $\delta=1/m$." (5-02 đang 60, nên cần bù chữ ở chỗ khác trên trang; người sửa đếm lại.) Câu mở 5-01: "… nên cỡ mẫu theo lớp: phụ thuộc lớp chứa $h$." Hoặc đổi `strand-keys` sang cụm đã có trên mặt trang. |
| 10 | trung bình | L04-7-02 | Trang "Vấn đề trung tâm" cuối không nêu quy tắc trả lời câu hỏi của hộp 1-05 ("chọn lớp giả thuyết nào"): dòng 2 chỉ viết "SRM cộng $\mathrm{pen}_k=\ldots$", không nói SRM chọn lớp làm nhỏ nhất $L_S(\hat h_k)+\mathrm{pen}_k$ và rủi ro của nó không quá mốc có phạt; dòng 1 bỏ vế "không quan sát được / tính được", là lý do một quy tắc chọn lớp phải dùng số hạng tính được. | Hộp 1-05: "chọn lớp giả thuyết nào trong một dãy lớp để hàm học được có rủi ro kì vọng nhỏ?"; ghi chú §4 cuối (phát hiện 2); ghi chú §9: "Số hạng phạt của SRM là bán kính hội tụ đều của Bài 02–03 tại xác suất thất bại $\delta q_k$." | Dòng 1: "Sai số xấp xỉ không tăng theo lớp, không quan sát được; cận $2r+\operatorname{opt}_S$ của sai số ước lượng tính được, xác suất $\ge1-\delta$." Dòng 2: "SRM chọn lớp làm nhỏ nhất $L_S(\hat h_k)+\mathrm{pen}_k$, $\mathrm{pen}_k=\mathrm{rad}_k(m,\delta q_k)$; rủi ro $\le$ mốc có phạt $+\tau$." Để giữ ≤ 60: bỏ vế "Lớp lồng nhau: rủi ro thực nghiệm chọn lớp lớn nhất" (đã ở bìa và 1-06). |
| 11 | nhẹ | L04-1-06, L04-2-02 | Câu hỏi "dùng bao nhiêu chỉ số đo" đặt hai lần trên mặt trang (1-06: "Dùng bao nhiêu chỉ số đo?"; 2-02: "Câu hỏi: với $m=10^4$, $\delta=0{,}05$, dùng bao nhiêu chỉ số đo?"). | Ghi chú: Câu hỏi mở đầu chỉ hỏi bậc đa thức; câu hỏi chỉ số đo là "Câu hỏi thực hành" của khối ứng dụng §3. | Ở 1-06 giữ câu hỏi về bậc như ghi chú; dòng thứ ba giữ cận $0{,}329\to0{,}560$ làm lý do. Câu hỏi chỉ số đo đặt một lần ở 2-02. |
| 12 | nhẹ | L04-5-01 | Câu mở "Danh sách vô hạn: $\mathrm{pen}_k\to\infty$, nên cỡ mẫu trong Định lý 04.11(b) phụ thuộc lớp chứa $h$." bỏ điều kiện về bán kính và nói "cỡ mẫu trong Định lý 04.11(b)", trong khi định lý là một cận, không có cỡ mẫu. | Ghi chú §7, câu mở: "Với bán kính của Định lý 02.14(a) hoặc 03.15(a) và một danh sách vô hạn, $\mathrm{pen}_k\to\infty$, nên cỡ mẫu để cận của hiệu này nhỏ hơn $\epsilon$ phụ thuộc lớp chứa $h$". | "Danh sách vô hạn, bán kính của Định lý 02.14(a), 03.15(a): $\mathrm{pen}_k\to\infty$, nên cỡ mẫu để vế phải của Định lý 04.11(b) cách $L_D(h)$ không quá $\epsilon$ phụ thuộc lớp chứa $h$." Gộp với phát hiện 9; đếm lại (đang 55). |
| 13 | nhẹ | L04-5-04 | Mạch 5 không có câu kết trên mặt trang: "học được không đều không kéo theo học được PAC" (mục tiêu 4) chỉ ở ghi chú diễn giả. "Không học được PAC" dựa trên Định lý 03.17(a) và Nhận xét 01.26 mà mặt trang chỉ ghi "(Bài 03)" sau "tách trọn vẹn". | Ví dụ 04.11, "Tóm lại, học được không đều không kéo theo học được PAC"; Bước 2 dẫn Định lý 03.17(a). | Dòng "$\mathcal H_j$ hữu hạn: …" thành "**Kết luận:** $\mathcal H_j$ hữu hạn, nên $A_{\mathrm{SRM}}$ học không đều (Hệ quả 04.15(a)), dù $\mathcal H$ không học được PAC."; dòng trước ghi "$d=\infty$, không học được PAC (Định lý 03.17(a))". 5-04 đang 60; người sửa đếm lại và bù chữ trên cùng trang. |
| 14 | nhẹ | L04-4-09 | Trang dùng lại bước tất định trên biến cố đại diện (đã nhắc ở 2-06) nhưng không gọi tên kỹ thuật; storyboard mục 14 ghi "dùng ở 4-09". | Ghi chú, Lộ trình chứng minh Định lý 04.11: "như Bước 2 của chứng minh Hệ quả 02.16"; ghi chú diễn giả 4-09 có tên kỹ thuật. | Câu mở 4-09: "Bước tất định: $E$ là biến cố của Bổ đề 04.9, …". |
| 15 | nhẹ | L04-6-03 | "Nhắc lại: đảo cận đuôi thành cỡ mẫu (Bài 02)" rút gọn tên kỹ thuật của deck Bài 02. | Tiêu đề `L02-4-04`: "Đảo cận đuôi thành bán kính và cỡ mẫu". | "Nhắc lại: đảo cận đuôi thành bán kính và cỡ mẫu (Bài 02): …". |
| 16 | nhẹ | L04-2-03 | Dòng "Ví dụ." dẫn "$D_\eta$ (Ví dụ 01.2)"; ghi chú dẫn $D_\eta$ ở Ví dụ 01.1, rủi ro của $h_t$ ở Ví dụ 01.2 và $0{,}18$ ở Ví dụ 01.10. | Ví dụ 04.2, Thiết lập: "Phân bố $D_\eta$ của Ví dụ 01.1, … $L^*=L^{\mathrm{Bayes}}_{D_\eta}=0{,}18$ (Ví dụ 01.10)"; Bước 1: "Theo Ví dụ 01.2, …". | "$D_\eta$ (Ví dụ 01.1, 01.2)". |
| 17 | nhẹ | L04-4-12 | Bài tập 04.4(b) dùng bảng của 4-07 nhưng đứng sau Ví dụ 04.10 (4-11), nên người học quay lại bảng sau một phản ví dụ khác chủ đề. Không trái ghi chú (bài tập không thuộc ghi chú; mỗi mạch kết bằng một bài tập theo khuôn chung). | Thứ tự 4-07 → 4-10 → 4-11 → 4-12. | Không bắt buộc: đặt 4-12 ngay sau 4-10, để 4-11 (bỏ (T6)) kết mạch và dẫn sang 6-05, vốn dùng cùng phân bố. Nếu giữ thứ tự, không cần sửa. |
| 18 | nhẹ | storyboard mục 3 | Dòng dẫn mạch 6 trong storyboard ("cho cận chỉ phụ thuộc lôgarit của số ứng viên") khác deck ("cho cận tăng theo lôgarit của số ứng viên"); mục 16 không ghi lệch này. | `storyboard.md` mục 3, hàng 6; `L04-6-00`. | Ghi lệch vào mục 16 hoặc cập nhật mục 3 theo deck. |
| 19 | nhẹ | L04-2-03 → L04-2-08 | Sai số xấp xỉ $0{,}04$ của lớp sáu hàm ngưỡng chỉ có trên hình F1 ở 2-03 (storyboard mục 16: "số $0{,}04$; $0{,}10$ đọc trên hình"), nhưng lời giải 2-08 dùng lại "Ba số hạng $0{,}04$; …". Quy định mới của common brief (duyệt deck 04): con số trên hình mà trang sau dùng đến phải có cả trong chữ trên mặt trang. | 2-03, dòng "Ví dụ."; 2-08, fragment thứ hai; ghi chú, Ví dụ 04.2 Bước 1. | Dòng "Ví dụ." của 2-03 kết bằng "sai số xấp xỉ $0{,}22-0{,}18=0{,}04$". (Ngoài vai: tiêu đề 5-02, 5-03 viết "1/m" bằng chữ thường, quy định mới đòi KaTeX trong tiêu đề.) |

**Ngoài phạm vi deck Bài 04 (để điều phối viên quyết định).** Deck Bài 03 (`L03-7-06`) ghi "Bài 04: Phân tích sai số, …" bằng chữ thường; deck Bài 01 liên kết Bài 02. Khi deck Bài 04 được công bố, dòng này có thể thành liên kết `lecture-04-phan-tich-sai-so.html` để các deck nhất quán.

## Đề xuất sửa ghi chú

Không có đề xuất mới. Thứ tự mục, khối và câu nối của ghi chú đủ cho mọi câu nối đề xuất ở trên; các phát hiện 1–5 chỉ đưa câu đã có trong ghi chú lên mặt trang. Điểm toán #47 (dạng phụ thuộc "$\ln(1/\delta)+\ln(1/q_k)$" sau Bổ đề 04.9) vẫn mở cho tác giả; deck không khẳng định dạng chung này trên mặt trang (chỉ ở ghi chú diễn giả 4-02 với điều kiện "với hai bán kính của Bài 02–03").

## Kết luận

**Đạt khi sửa.** 0 chặn bàn giao, 0 nghiêm trọng, 10 trung bình, 9 nhẹ. Bảy mạch ứng đúng các mục liên tiếp của ghi chú; hai chỗ đổi thứ tự (Nhận xét 04.4 thành "Lưu ý:" ở 2-04; Ví dụ 04.9 và Thuật toán 04.12 trước Định lý 04.11 theo T5) nằm trong một mục và có căn cứ. Liên kết `#/N`, viewer và dòng Bài 05 đúng; bảng Mục–Bài tập và năm trang bài tập khớp `exercises.md`; nhắc lại kết quả và kỹ thuật của Bài 02–03 thống nhất. Các phát hiện trung bình đều thuộc một loại: câu nối giữa mạch hoặc ý trọng tâm có trong ghi chú và ghi chú diễn giả nhưng chưa có trên mặt trang (1–5, 10), số hiệu được dẫn mà chưa gắn (6), một phần kết quả được chứng minh mà chưa phát biểu (7), và dòng dẫn, từ khóa của mạch 5 (8, 9).
