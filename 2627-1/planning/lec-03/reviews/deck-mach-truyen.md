# Duyệt deck Bài 03 — Vai 5 `mach-truyen` (mạch truyện, liên kết, thống nhất thứ tự với ghi chú)

Bản duyệt: `2627-1/lecture-03-chieu-vc.html` (đóng băng, 55 trang, 7 mạch: 6, 8, 8, 7, 10, 9, 7 trang). Đối chiếu: `materials/lec-03/lecture-note.md`, `exercises.md`, `planning/lec-03/storyboard.md`, `review-log.md` § Bộ trang chiếu, deck 01, 02. Không sửa tệp nào ngoài báo cáo này.

## Kiểm tra máy đã chạy

- `deck_check.py` (không `--shots`) trên `http://localhost:8766/2627-1/lecture-03-chieu-vc.html`: chạy xong, 55 trang; không dùng để kết luận mật độ (ngoài phạm vi vai).
- Playwright (script trong thư mục nháp `rv-mach-truyen/scripts/links.py`): sáu liên kết `#/2`…`#/7` của trang Nội dung (L03-1-04) mở đúng `L03-2-00`…`L03-7-00`, tiêu đề h2 trùng tên trong danh sách; phím →, ↓, Space chuyển trang, Esc mở chế độ tổng quan; số trang theo mạch `[6, 8, 8, 7, 10, 9, 7]`.
- Viewer `material-viewer.html?doc=materials/lec-03/{lecture-note,exercises}.md&deck=lecture-03-chieu-vc.html`: cả hai mở đúng tài liệu Bài 03, có liên kết "Bộ trang chiếu → lecture-03-chieu-vc.html", 0 `.katex-error`, 0 yêu cầu lỗi, 0 lỗi console.
- Không chụp ảnh màn hình; các nhận xét dưới đây dựa trên mã HTML (mặt trang và ghi chú diễn giả).

## 1. Bảng chức năng từng trang và đối chiếu trang → mục ghi chú

| Trang | Mục ghi chú | Vai trò trong mạch | Kết nối vào | Kết nối ra |
|---|---|---|---|---|
| 1-01 | đoạn mở đầu, §9 | bìa, luận điểm bằng lời | Bài 02 (ghi chú diễn giả) | luận điểm cả bài |
| 1-02 | Kiến thức tiên quyết | nhắc ERM, PAC, union bound, Chebyshev, Hoeffding, 02.14, 02.16 | deck 02 (5-03, 5-09) | $r_m$, $K$ dùng ở 4-01, 5-01, 6-04 |
| 1-03 | Mục tiêu học tập | năm mục tiêu | — | khớp §10 và bảng 7-05 |
| 1-04 | toàn bài | Nội dung, `#/2`–`#/7` đúng | — | các mạch 2–7 |
| 1-05 | đoạn mở đầu | một hộp "Câu hỏi:" (đúng quy định) | câu hỏi cuối deck 02 7-06 ("đại lượng nào thay cho $\ln\lvert\mathcal H\rvert$?") | trả lời ở 7-02 |
| 1-06 | Câu hỏi mở đầu; §3 (khối ứng dụng) | hai câu hỏi cỡ mẫu, dữ kiện dạng danh sách | sáu hàm ngưỡng của Bài 01–02 | trả lời ở 6-03, 7-02 |
| 2-00 | §1–§4 | dòng dẫn mạch | 1-06 | 2-01 |
| 2-01 | §1, §2 | khung bài toán; (T1), (T5), (M) | 1-02 | (T5), (M) dùng ở 5-03, 5-04, 5-09 |
| 2-02 | §3 (Ví dụ 03.1), §4 (Định nghĩa 03.1, Ví dụ 03.2) | đếm véc-tơ thay cho đếm hàm; thu hẹp | 1-06 (sáu hàm) | "Lưu ý:" → trở ngại (ii) ở 5-03 |
| 2-03 | §4 (Định nghĩa 03.2, 03.3) | tách trọn vẹn, chiều VC | 2-02 | 2-04 |
| 2-04 | §4 (Nhận xét 03.4) | Kỹ thuật cận dưới và cận trên | 2-03 | 2-06, 2-07, 3-05, 3-06, 7-04 |
| 2-05 | §4 (Mệnh đề 03.5, 03.6) | trực quan, hình, phát biểu | 2-04 | 2-06 |
| 2-06 | §4 (chứng minh 03.5, 03.6) | ý tưởng chứng minh; "thứ tự trên đường thẳng" | 2-05 | 3-01 dòng 1 (không có thứ tự trong $\mathbb R^p$) |
| 2-07 | tệp bài tập (03.2(b), (c)) | bài tập kiểm tra kỹ thuật | 2-04 | — |
| 3-00 | §5 | dòng dẫn mạch nhắc lại số $11$ của 1-06 | 1-06, 2-06 | 3-04 |
| 3-01 | §5 (Định nghĩa 03.7) | định nghĩa; câu nối trên mặt trang | 2-06 | 3-02 |
| 3-02 | §5 (Ví dụ 03.3 Bước 1–2) | ba điểm: cận dưới; ba điểm thẳng hàng | câu ôn nhanh 2 (1-02 ghi chú) | 3-05 bước 1 (công thức $b$, $w_i$) |
| 3-03 | §5 (Bổ đề 03.8) | công cụ Radon | 3-01 dòng 1 | 3-05 bước 2–3 |
| 3-04 | §5 (Mệnh đề 03.9) | trực quan, phát biểu; $d=11$, $d=3$ | 3-02, 3-03 | 5-08, 6-03 |
| 3-05 | §5 (chứng minh 03.9), Phụ lục A | ý tưởng chứng minh | 3-03, 3-02 | 3-06 |
| 3-06 | §5 (Ví dụ 03.3 Bước 3–4) | kiểm tra cận trên trên hai cấu hình | 3-03 (hình Radon), 3-05 | $14$ ở 4-06 |
| 3-07 | §5 (Nhận xét 03.10) | số tham số; câu nối sang đếm cách gán nhãn | 1-06 (ghi chú: $\mathcal H_{\sin}$) | 4-01 |
| 4-00 | §6 | dòng dẫn mạch | 3-07 | 4-01 |
| 4-01 | §6 (Định nghĩa 03.11, Ví dụ 03.4) | hàm tăng trưởng; câu nối "Định lý 02.14 cộng $K$ biến cố hỏng" | 1-02, 2-02 | 4-02 |
| 4-02 | §6 (Bổ đề 03.12; hình của Ví dụ 03.5) | trực quan, phát biểu | 4-01 | 4-03, 4-05 |
| 4-03 | §6 (chứng minh 03.12 Bước 1–2), Phụ lục B | ý tưởng chứng minh (a) | 4-02 | 4-04 |
| 4-04 | §6 (áp dụng Bước 1–2; ví dụ dựng mới) | ví dụ tính tay | 4-03, 2-05 | — |
| 4-05 | §6 (chứng minh 03.12 Bước 3) | ý tưởng chứng minh (b), phản ví dụ $m<d$ | 4-02 | 5-01 dòng 1 |
| 4-06 | §6 (Ví dụ 03.5) | ba cách đếm, bảng số | 3-06, 4-01 | (không có câu nối trên mặt trang; 5-01 dòng 1 đảm nhận) |
| 5-00 | §7 | dòng dẫn mạch | 4-05 | 5-01 |
| 5-01 | §6 câu cuối, §7 (Định nghĩa 03.13) | câu nối + định nghĩa | 4-05, deck 02 (ε-đại diện) | 5-02, 5-04 (c) |
| 5-02 | §7 (Ví dụ 03.6) | phản ví dụ $d=\infty$ | Bài 01 (Ví dụ 01.8, Mệnh đề 01.15) | 6-07 (Hệ quả 03.18) |
| 5-03 | §7 (đoạn trước Định lý 03.15) | câu hỏi của mạch, hai trở ngại, cách sửa | 2-02 "Lưu ý:", 4-01 | 5-05, 5-06 |
| 5-04 | §7 (Định lý 03.15) | trực quan, phát biểu | 5-01, 5-03 | 5-05, 5-08, 6-01 |
| 5-05 | §7 (lộ trình chứng minh), Phụ lục C | ý tưởng chứng minh năm bước | 5-03, 5-04 | 5-06, 5-07, 5-09 |
| 5-06 | §7 (Bước 1–2), C.2–C.3 | Kỹ thuật đối xứng hóa và mẫu bóng | 5-05 | Bài 07 (storyboard) |
| 5-07 | §7 (Bước 3–5), C.4, C.6 | Kỹ thuật hàm tăng trưởng thay cho số giả thuyết | 5-05, deck 02 5-05 ($\delta/K$) | Bài 04, 07 |
| 5-08 | §7 (Ví dụ 03.7) | cận bằng số | 3-04 ($d=3$, $11$) | 6-03 |
| 5-09 | §7 (Ví dụ 03.8 và đoạn sau) | phản ví dụ bỏ (T5) | 5-02 (cùng $D$), 5-05 bước 3 | 7-01, 7-04 câu 4 |
| 6-00 | §8, §9 | dòng dẫn mạch | 5-04 | 6-01 |
| 6-01 | §8 (Hệ quả 03.16) | trực quan, phát biểu | 5-04, deck 02 5-09 | 6-02, 6-03 |
| 6-02 | §8 (chứng minh 03.16) | ý tưởng chứng minh; "Nhắc lại:" bước tất định | deck 02 5-11 | 6-03 |
| 6-03 | §8 (Ví dụ 03.9) | trả lời câu hỏi 1-06 | 1-06, 5-08 | 7-02 |
| 6-04 | §8 (Ví dụ 03.10), §9 | so với lớp rời rạc hóa | 1-02 ($r_m$), 6-03 | — |
| 6-05 | §8 (Định lý 03.17(a)) | điều kiện cần | (không có câu nối "điều kiện đủ → điều kiện cần" trên mặt trang) | 6-06, 6-07 |
| 6-06 | §8 (Định lý 03.17(b)) | sáu khẳng định | 6-05 | 6-07 |
| 6-07 | §8 (phép kéo theo; Hệ quả 03.18) | ý tưởng chứng minh, sơ đồ | 5-04, 6-02, 6-05, 5-02 | 7-01 |
| 6-08 | §8 (Định lý 03.19), §9 | cận dưới (đọc thêm), giới hạn | 6-01 ($M$) | 7-02 (ghi chú) |
| 7-00 | §9–§12 | dòng dẫn mạch Tổng kết | — | — |
| 7-01 | §4–§9 | bảng tổng kết, sáu hàng | mọi kết quả | — |
| 7-02 | đoạn mở đầu, §9, Ví dụ 03.9 | trả lời hộp 1-05 cho cả bài | 1-05, 1-06 | — |
| 7-03 | tệp bài tập (03.1(a)) | bài tập tổng hợp, "Lời giải:" trên mặt trang | 2-02, 4-01 | — |
| 7-04 | §11, §7, Nhận xét 03.4, 03.10, Ví dụ 03.8 | bốn câu tự kiểm tra | 2-04, 5-03, 3-07, 5-09 | — |
| 7-05 | §10, tệp bài tập | bảng "Mục – Bài tập", liên kết viewer | — | `exercises.md` |
| 7-06 | §11, §12 | tài liệu; tên Bài 04 | — | Bài 04 (câu hỏi cầu nối ở ghi chú diễn giả) |

**Thứ tự so với ghi chú.** Cột "Mục ghi chú" không giảm từ 2-01 đến 7-06; các đổi chỗ trong §5 (Ví dụ 03.3 Bước 1–2 trước Bổ đề 03.8) và trong §6 (ví dụ dựng mới 4-04 giữa hai trang ý tưởng chứng minh) nằm trong cùng mục và đã được điều phối viên chấp nhận. Ngoại lệ duy nhất: 1-06 dùng khối ứng dụng của §3 trước 2-01 (§1–§2), xem phát hiện N1.

**Bảng `Mục | Bài tập` (7-05).** Đủ 12 bài, mỗi bài một lần; tên mục trùng tên mạch 2–6. Kiểm từng bài theo kiến thức cuối cùng bài cần: 03.2, 03.7, 03.9, 03.10 chỉ cần chiều VC (mạch 2); 03.3, 03.12 cần Mệnh đề 03.9 (mạch 3); 03.1, 03.6, 03.8 cần hàm tăng trưởng và Bổ đề 03.12 (mạch 4); 03.5(c) cần Định lý 03.15 (mạch 5); 03.4 cần Hệ quả 03.16, Ví dụ 03.9, 03.10 và 03.11 cần Định lý 03.17 (mạch 6). Khớp. Trang 2-07 khớp đề Bài tập 03.2(c) và lời giải; 7-03 khớp đề và lời giải Bài tập 03.1(a) ($\Pi(3)=4$, $\Pi(8)=6$).

**Tính liên tục với deck 01, 02.** Hộp 1-05 lặp đúng câu hỏi cầu nối cuối deck 02. Định lý 02.14 nhắc lại với cùng $r_m=\sqrt{\ln(2K/\delta)/(2m)}$ và cùng nội dung (a); Hệ quả 02.16 nhắc lại "rủi ro vượt mức của mọi nghiệm ERM $\le2r_m$"; 6-04 dùng đúng dạng (c) của deck 02 ($\lceil2\ln(2K/\delta)/\epsilon^2\rceil$). Tên kỹ thuật của deck 02 được gọi lại: "Chia xác suất thất bại $\delta/K$" (5-07, có "Nhắc lại:"), "Bước tất định trên biến cố đại diện" (6-02, có "Nhắc lại:"), "Đảo cận đuôi" (5-05, không có "Nhắc lại:", xem N6). Ví dụ xuyên suốt sáu hàm ngưỡng của Bài 01–02 xuất hiện ở 1-06, 2-02, 6-04, 7-03.

**Luồng chủ đề mở và đóng (bảng kiểm Threads của `quill`).** Đóng đủ: hộp 1-05 → 7-02; hai câu hỏi 1-06 → 6-03, 7-02; $\mathcal H_{\sin}$ (ghi chú 1-06) → 3-07; "chưa thể thay $K$ bằng $m+1$" (2-02) → 5-03; "dạng trực tiếp" 5-08 → 6-03; ba giả thiết không bỏ được → 5-02, 5-09 (mặt trang), Ví dụ 02.6 (ghi chú diễn giả). Đóng chưa trọn trên mặt trang: ba điểm thẳng hàng ở 3-02 (T2), vai trò của (M) (N3), "điều kiện đủ → điều kiện cần" (T1).

## 2. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 6-05 (T1) | Câu nối giữa hai cụm của mạch 6 (điều kiện đủ ở 6-01–6-04, điều kiện cần ở 6-05–6-07) không có trên mặt trang; chỉ ở ghi chú diễn giả 6-06. Quy định "Câu nối giữa hai mạch hoặc hai cụm … phải có trên mặt trang". | 6-05 mở thẳng bằng "**Trực quan.** Mẫu thấy nhiều nhất nửa tập $2m$ điểm …"; ghi chú §8, đoạn trước Định lý 03.17: "Định lý 03.15 và Hệ quả 03.16 cho điều kiện đủ: dưới (M), chiều VC hữu hạn kéo theo học được. Chiều VC hữu hạn cũng là điều kiện cần …" | Thêm một dòng đầu 6-05: "Hệ quả 03.16: dưới (M), $d<\infty$ đủ để học được; phần (a) cho chiều ngược lại." (bù mật độ bằng cách rút "Trực quan." xuống một vế). |
| trung bình | 3-02 (T2) | Dòng "Ba điểm thẳng hàng … cách $(1,0,1)$ không thực hiện được" không có vai trò rõ trên mặt trang: ý cần rút ra (một tập không bị tách trọn vẹn không cho cận trên, đúng lỗi của 2-04 và 2-07) chỉ có ở ghi chú diễn giả. Người học thấy một tập ba điểm không bị tách trọn vẹn ngay trước trang chứng minh $d=p+1\ge3$ mà không có câu nối về kỹ thuật cận dưới và cận trên. | 3-02 mặt trang dòng cuối; ghi chú Ví dụ 03.3 Bước 2: "Tập này không bị tách trọn vẹn, dù $d=3$: theo Nhận xét 03.4, một tập không bị tách trọn vẹn không cho cận trên." | Thêm sau dòng đó: "**Lưu ý:** một tập không bị tách trọn vẹn không cho cận trên (Nhận xét 03.4)." (không cần nêu $d=3$, chưa phát biểu). Khi đó bỏ câu báo trước ở ghi chú diễn giả 2-07 ("Lỗi của lời giải thứ hai cũng xuất hiện ở lớp nửa mặt phẳng …"), xem N5. |
| trung bình | 5-04 | "Trực quan." lặp lại phát biểu (b) và câu nối 5-01, không nêu cơ chế hay trường hợp cực biên (bài học deck 02: "Trực quan." không nhắc lại phát biểu). Cùng phép thay $\ln K\to d\ln(\cdot)\to\sqrt{d\ln m/m}$ xuất hiện ba lần trong bốn trang. | 5-01: "Nếu $d\ln(em/d)$ thay được $\ln K$ trong Định lý 02.14, độ lệch đều có cỡ $\sqrt{d\ln m/m}$."; 5-04: "$\ln K$ thành $\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$, nên độ lệch đều có cỡ $\sqrt{d\ln m/m}$."; 5-07: "$\ln\tfrac{2K}\delta\longrightarrow\ln\tfrac{4\Pi_{\mathcal H}(2m)}\delta\le\ldots$" | Thay "Trực quan." 5-04 bằng hai trường hợp biên đã có trong ghi chú diễn giả (ghi chú, đoạn sau Định lý 03.15): "$d=\infty$: $\Pi_{\mathcal H}(2m)=2^{2m}$, $\rho_m\ge\sqrt{16\ln2}\approx3{,}33$, cận không cho thông tin; $d=0$: $\Pi_{\mathcal H}=1$." |
| trung bình | 6-01 | (O1), (O2) và $\epsilon_{\mathrm{opt}}$-ERM xuất hiện lần đầu trên mặt trang 6-01 mà không có "Nhắc lại:" (quy định định nghĩa hoặc nhắc lại trước khi dùng); 2-01 chỉ liệt kê (T1), (T5), (M), trong khi §2 của ghi chú liệt kê cả (O1), (O2). | 6-01: "ERM (O1) thỏa Định nghĩa 01.4, hoặc $\epsilon_{\mathrm{opt}}$-ERM $A$ (O2)"; nghĩa của hai nhãn chỉ có ở ghi chú diễn giả 6-01. Ghi chú §2: "(O1) … $\hat h\in\arg\min_{h}L_S(h)$. (O2) … $L_S(\hat h)\le\inf_hL_S(h)+\epsilon_{\mathrm{opt}}$." | Thêm vào 2-01 (sau dòng (M)) hoặc đầu 6-01 một dòng "**Nhắc lại:** (O1) $\hat h\in\arg\min_hL_S(h)$; (O2) $L_S(\hat h)\le\inf_hL_S(h)+\epsilon_{\mathrm{opt}}$." |
| trung bình | 6-02 | Điều thay đổi so với Bài 02 (phần tử tốt nhất $h_{\mathcal H}$ có thể không tồn tại, nên chuỗi viết cho mọi $h$ rồi lấy $\inf$) là liên kết "giả thiết nào đổi" giữa deck 02 và deck 03, nhưng lý do chỉ ở ghi chú diễn giả. Đặt cạnh deck 02 5-10 (bước 1: "$h_{\mathcal H}$ tồn tại vì $\mathcal H$ hữu hạn"), người học không thấy vì sao bước 2 khác. | 6-02 bước 2: "Vế trái không phụ thuộc $h$: lấy $\inf_h$."; ghi chú §8 mở đầu: "Với lớp vô hạn, giá trị nhỏ nhất của $L_D$ trên $\mathcal H$ có thể không đạt, nên phép so sánh với phần tử tốt nhất trong lớp ở Hệ quả 02.16 phải viết lại cho mọi $h\in\mathcal H$." | Sửa "Nhắc lại:" 6-02 thành "**Nhắc lại:** bước tất định (Hệ quả 02.16), so với $h_{\mathcal H}$; trên lớp vô hạn $\min_hL_D(h)$ có thể không đạt." |
| nhẹ | 1-06, 2-01 (N1) | Thứ tự mục giảm: 1-06 lấy khối ứng dụng §3, rồi 2-01 quay về §1–§2. Storyboard §12 ghi "các mục không giảm", không ghi ngoại lệ này. Lý do hợp lý (Câu hỏi mở đầu của ghi chú đứng trước §1), nhưng cần ghi. | storyboard §3 bảng mạch: mạch 1 "§3 (khối ứng dụng)", mạch 2 "§1–§4"; §12 "Kiểm tra thứ tự: … các mục không giảm". | Không sửa deck; ghi ngoại lệ vào storyboard §12 và `review-log.md`. |
| nhẹ | 2-01 (N2) | Phép đổi (T4) → (T5) là liên kết giả thiết với Bài 02 nhưng chỉ có ở ghi chú diễn giả; 1-02 viết "(T1)–(T3), $K$ hàm chọn trước" thay cho (T4) của deck 02. | 2-01 mặt trang: "(T5) $\mathcal H$ chọn trước khi lấy mẫu"; ghi chú §2: "Giả thiết (T4) của Bài 02 là (T5) cộng điều kiện $\mathcal H$ hữu hạn." | Viết "(T5) $\mathcal H$ chọn trước khi lấy mẫu, có thể vô hạn ((T4) bỏ điều kiện hữu hạn)". |
| nhẹ | 2-01, 5-03, 5-04 (N3) | Vai trò của (M) (độ lệch đều đo được) không có trên mặt trang nào; (M) được định nghĩa ở 2-01 và chỉ quay lại như một nhãn giả thiết ở 5-04, 5-05. | ghi chú diễn giả 2-01 và 5-03; ghi chú §7: "Điều kiện (M) bảo đảm độ lệch đều đo được." | Thêm vào cuối dòng (M) ở 2-01: "; (M) làm độ lệch đều đo được." |
| nhẹ | 4-02 (N4) | Hình nêu hàm tăng trưởng của lớp nửa mặt phẳng tại $m=4$ bằng $14$ trước khi 4-06 chứng minh $\Pi(4)\le14$; 3-06 chỉ cho hình vuông đạt $14$. | alt hình 4-02: "Bốn ô vuông 2, 4, 8, 14 tại m từ 1 đến 4 là hàm tăng trưởng của lớp nửa mặt phẳng"; ghi chú Ví dụ 03.5 Bước 4. | Chấp nhận được vì hình lấy từ Ví dụ 03.5; nếu sửa, thêm vào 4-06 dòng "$\Pi=14$ là bốn ô vuông của hình ở trang Bổ đề Sauer–Shelah" để nối ngược. |
| nhẹ | 2-07 (N5) | Ghi chú diễn giả báo trước nội dung mạch 3 ("dù chiều VC của lớp lớn hơn hai") trước khi Mệnh đề 03.9 được phát biểu. | ghi chú diễn giả 2-07, câu cuối. | Chuyển ý này thành câu nối ngược ở 3-02 (xem T2) và bỏ ở 2-07. |
| nhẹ | 5-05 (N6) | Kỹ thuật "Đảo cận đuôi thành bán kính và cỡ mẫu" của deck 02 (4-04) được gọi tắt "Đảo cận đuôi" ở bước 5 mà không có "Nhắc lại:" như hai kỹ thuật khác của deck 02 (5-07, 6-02). | 5-05 bước 5: "Đảo cận đuôi: vế phải bằng $\delta$ cho $\epsilon=\rho_m$"; deck 02 4-04: "**Kỹ thuật.** Từ cận đuôi $g(m,r)$: $g(m,r)=\delta$ cho bán kính $r$ …" | "**Nhắc lại:** đảo cận đuôi (Bài 02): vế phải bằng $\delta$ cho $\epsilon=\rho_m$; …" hoặc giữ nguyên và ghi vào storyboard §14 là gọi tên không có nhãn. |
| nhẹ | 5-06 (N7) | Tên kỹ thuật "đối xứng hóa" chỉ có ở tiêu đề; tên tiếng Anh (symmetrization) chỉ ở ghi chú diễn giả. Deck sau sẽ nhắc kỹ thuật bằng tên này (storyboard §14: dùng lại ở Bài 07). | 5-06 dòng "**Kỹ thuật.** Thay $L_D(h)$ bằng $L_{S'}(h)$ …"; ghi chú diễn giả: "Tên chung của bước 1–2 là đối xứng hóa (symmetrization)." | "**Kỹ thuật.** Đối xứng hóa (symmetrization): thay $L_D(h)$ bằng $L_{S'}(h)$ …". |
| nhẹ | 5-08, 6-03 (N8) | "Dạng trực tiếp" là tên do Ví dụ 03.7 đặt cho vế phải thứ nhất của Định lý 03.15(b); deck dùng ở 5-08 và 6-03 mà không nói đó là vế nào. | 5-08: "Dạng trực tiếp của Định lý 03.15(b)."; ghi chú Ví dụ 03.7: "gọi vế phải thứ nhất là dạng trực tiếp, vế phải thứ hai là dạng hằng số $4$". | "Dạng trực tiếp: vế phải thứ nhất của Định lý 03.15(b)." |
| nhẹ | 6-04 (N9) | Dòng hai bán kính của lớp sáu hàm ($0{,}2222$, $0{,}0523$) không được đọc trên mặt trang; "Diễn giải:" chỉ nói về cỡ mẫu. Ý của dòng (thừa số $4$ do hằng số $8$ của mẫu bóng, nối với 5-06) chỉ ở ghi chú diễn giả. | 6-04 dòng 5 và "Diễn giải:"; ghi chú Ví dụ 03.10, đoạn "Tóm lại": "bán kính VC lớn hơn $r_m$ khoảng $4{,}25$ lần, trong đó thừa số $\sqrt{16}=4$ đến từ hằng số $8$ …" | Thêm "(tỉ số $4{,}25$)" vào cuối dòng hai bán kính, hoặc chuyển dòng đó xuống ghi chú diễn giả. |
| nhẹ | 7-00 (N10) | Dòng dẫn mạch Tổng kết liệt kê điều kiện như thể đủ ("khi quan sát độc lập và lớp được chọn trước khi lấy mẫu") nhưng thiếu điều kiện đo được và hàm lỗi 0–1, khác 6-00 và 7-02. | 7-00 `strand-lead`; 7-02 dòng 5: "Dưới (M) … hàm lỗi 0–1". | "… khi quan sát độc lập, lớp chọn trước khi lấy mẫu và thỏa điều kiện đo được." |
| nhẹ | 7-02 (N11) | Dòng 5 ghép (T5) vào định lý cơ bản; Định lý 03.17 không liệt kê (T5), còn bảng 7-01 ghi "(M) cho (b)". Hai trang Tổng kết lệch nhau về giả thiết của cùng kết quả. | 7-02: "Dưới (M), học được khi và chỉ khi $d<\infty$; cần (T1), (T5), hàm lỗi 0–1."; ghi chú Định lý 03.17, Giả thiết; §9 "Ba giả thiết sau không bỏ được" nói về Định lý 03.15. | Chuyển "(T1), (T5)" sang dòng 2 (độ lệch đều $\le\rho_m$); dòng 5 giữ "Dưới (M), hàm lỗi 0–1: học được khi và chỉ khi $d<\infty$." |
| nhẹ | 5-03, 5-05, 5-07 (N12) | Ý "$h$ chỉ vào qua cách gán nhãn trên $2m$ điểm" lặp ba lần trên mặt trang (cách sửa, bước 3, dòng Kỹ thuật). | 5-03 fragment cuối; 5-05 bước 3; 5-07 dòng "**Kỹ thuật.**". | Giữ ở 5-03 và 5-07; bước 3 của 5-05 rút còn "Biết $(S,S')$: nhiều nhất $\Pi_{\mathcal H}(2m)$ cách (giả thiết (T5))". |
| nhẹ | 7-00 (N13) | Ghi chú diễn giả kết bằng câu nói về cấu trúc của deck, không phải nội dung. | ghi chú diễn giả 7-00: "Không có khái niệm mới." | Bỏ câu. |

## 3. Các điểm đạt (không cần sửa)

- Trang "Vấn đề trung tâm" mở đầu: đúng một hộp "Câu hỏi:", câu trả lời theo mạch nằm ở ghi chú diễn giả; trang "Vấn đề trung tâm" cuối (7-02) trả lời đúng câu hỏi của hộp bằng dòng 1 ($\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$ thay cho $\ln\lvert\mathcal H\rvert$), giữ "với xác suất ít nhất $1-\delta$" và đại lượng được chặn.
- Câu nối giữa các mạch có trên mặt trang ở 3-01 (không có thứ tự trong $\mathbb R^p$), 3-07 ("Với $m>d$ điểm, cần đếm số cách gán nhãn"), 4-01 ("Định lý 02.14 cộng $K$ biến cố hỏng"), 5-01 (dòng đầu), 6-01 ("Trực quan." hai sai số $\rho_m$); câu hỏi trung tâm của mạch 5 nằm ở 5-03, trước nửa sau của mạch.
- Từ khóa của mọi mạch xuất hiện trên một mặt trang nội dung; dòng dẫn mạch là câu trần thuật về nội dung, không lặp một khuôn; ghi chú diễn giả trang tiêu đề mạch viết bằng câu thường.
- Mạch Tổng kết không đưa khái niệm mới trên mặt trang; lớp hình chữ nhật ở 7-04 có dẫn Bài tập 02.7.
- Không có trang nào xem trước Bài 04 trên mặt trang; câu hỏi cầu nối sang Bài 04 nằm ở ghi chú diễn giả 7-06, tên Bài 04 khớp tiêu đề ghi chú Bài 04.

## Đề xuất sửa ghi chú

Không có đề xuất mới. Đề xuất đã ghi ở `review-log.md` (Ví dụ 03.5 Bước 7, "$3\le m\le5$" → "$3\le m\le9$") không ảnh hưởng mạch truyện; deck theo ghi chú ở 4-06.

## Kết luận

**đạt khi sửa** — 0 chặn bàn giao, 0 nghiêm trọng, 5 trung bình, 13 nhẹ.
