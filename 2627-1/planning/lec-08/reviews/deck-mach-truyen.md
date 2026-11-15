# Duyệt deck Bài 08 — Vai 5: mạch truyện và liên kết

Người duyệt: tác tử `mach-truyen` (chỉ đọc), 2026-11-16. Bản duyệt: `2627-1/lecture-08-on-dinh-sgd-hoc-sau.html` (đóng băng, 55 trang). Đối chiếu: `materials/lec-08/lecture-note.md`, `exercises.md`, `planning/lec-08/storyboard.md` (§3, §4, §6, §12, §16), quyết định cuối `review-log.md` § Bộ trang chiếu, decks 05, 06, 07 (tên kỹ thuật, Định nghĩa 06.9, Định lý 06.10, trang cuối deck 07). Bảng kiểm liên tục: phần Outline/Threads/Concept của `quill/references/workflows.md` (không tạo `quill.json`). Không đọc UML (vai này không cần).

Đã chạy:
- `deck_lint.py`: 0 phát hiện, 55 trang.
- Playwright 1600×900 (script trong thư mục nháp `lec-08/rv-mach-truyen/links.py`): sáu liên kết `#/2`…`#/7` của trang Nội dung mở đúng `L08-2-00`…`L08-7-00`; bấm `#/5` tới `L08-5-00`. Hai liên kết viewer của `L08-7-08` trả 200, tiêu đề đúng Bài 08, trang viewer có liên kết ngược về deck. Không lỗi trang.
- Từ khóa mạch trên mặt trang nội dung (bỏ trang tiêu đề mạch): đếm bằng script.

## 1. Bảng chức năng từng trang và đối chiếu trang → mục ghi chú

| Trang | Vai trò trong mạch | Mục ghi chú | Kết nối vào | Kết nối ra |
|---|---|---|---|---|
| 1-01 | bìa, luận điểm | mở đầu, §10 | — | luận điểm có điều kiện, trả lời ở 7-03 |
| 1-02 | tiên quyết: Định nghĩa 06.9, Định lý 06.10, (T1), (T2), tính trơn, phép chiếu | Kiến thức tiên quyết | Bài 05, 06 | 2-04 (mẫu lân cận), 4-01 (Định lý 06.10) |
| 1-03 | mục tiêu 1–5 | Mục tiêu học tập | — | mạch 2–7 |
| 1-04 | nội dung, `#/2`…`#/7` | — | — | mạch 2–7 |
| 1-05 | vấn đề trung tâm, một hộp | mở đầu (dòng 5) | — | 7-03 |
| 1-06 | ví dụ dẫn nhập, "Câu hỏi:" | Câu hỏi mở đầu | 1-05 | 4-03, 4-04 (cận $t/200$), 7-03 |
| 2-00 | tiêu đề mạch 2 | §1–§5 | — | 2-01 |
| 2-01 | thiết lập, Thuật toán 08.1, đại lượng cần chặn | §1; Thuật toán 08.1 ở §4 | 1-06 | 2-02 |
| 2-02 | giả thiết, (L), hằng số logistic | §2 | 2-01 | 2-03, mọi kết quả |
| 2-03 | Ví dụ 08.1; ứng dụng $10^4$ hồ sơ, "Câu hỏi:" | §3 | 2-02 | 2-05 (Huber), 5-03 (câu hỏi) |
| 2-04 | Định nghĩa 08.2 | §4 | 1-02 (Định nghĩa 06.9) | 2-05 |
| 2-05 | trực quan ghép cặp, "Kỹ thuật." Jensen, ví dụ một bước | §4, hai đoạn sau Định nghĩa 08.2 | 2-04 | 2-06, 4-02 bước 3 |
| 2-06 | Ví dụ 08.2, hình F1 | §4 | 2-03, 2-05 | 2-07 (bước chung), 3-01 (bước khác biệt) |
| 2-07 | ánh xạ bước gradient, Định nghĩa 08.3 | §5 đoạn mở, Định nghĩa 08.3 | 2-06 | 2-08 |
| 2-08 | trực quan, Bổ đề 08.4 | §5 | 2-07 | 2-09 |
| 2-09 | ý tưởng chứng minh Bổ đề 08.4 | chứng minh Bổ đề 08.4, Phụ lục A | 2-08 | 2-10 |
| 2-10 | Ví dụ 08.3, ngưỡng chặt; dòng nối sang bước khác biệt | §5, Ví dụ 08.3, đoạn cuối | 2-09 | 3-01, 6-05 |
| 2-11 | Bài tập 08.3(a) | tệp bài tập | 2-10 | — |
| 3-00 | tiêu đề mạch 3 | §6 | 2-10 | 3-01 |
| 3-01 | trực quan, Mệnh đề 08.5 | §6 | 2-06, 2-10 | 3-02, 4-01 |
| 3-02 | ý tưởng chứng minh Mệnh đề 08.5 | chứng minh Mệnh đề 08.5, Phụ lục B(i) | 3-01, Bài 05 (tổng triệt tiêu) | 6-03 |
| 3-03 | Ví dụ 08.4 | §6 | 2-06 | 3-04 |
| 3-04 | Bài tập 08.1(c) | tệp bài tập | 3-03 | — |
| 4-00 | tiêu đề mạch 4 | §7 | 3-01 | 4-01 |
| 4-01 | dòng nối, trực quan, Định lý 08.6 | §7 | 3-01, 2-02 (L), 1-02 | 4-02, 4-03 |
| 4-02 | ý tưởng chứng minh Định lý 08.6 | chứng minh Định lý 08.6 | 4-01, Bài 06 (đổi vai) | 4-03 |
| 4-03 | Ví dụ 08.5 | §7 | 4-01, 1-06 | 4-04 |
| 4-04 | Ví dụ 08.6, hình F2 | §7 | 1-06, 4-03 | 4-05 |
| 4-05 | dòng nối, trực quan, Hệ quả 08.7 | §7 | 4-01 | 4-06, 5-01 |
| 4-06 | ý tưởng chứng minh Hệ quả 08.7 | chứng minh Hệ quả 08.7 | 4-05 | 4-07 |
| 4-07 | Bài tập 08.7(b) | tệp bài tập | 4-05 | — |
| 5-00 | tiêu đề mạch 5 | §8 | 4-05 | 5-01 |
| 5-01 | nhắc lại Mệnh đề 06.5(b), trực quan, Hệ quả 08.8 | §8 | 4-05, Bài 06 | 5-02 |
| 5-02 | ý tưởng chứng minh Hệ quả 08.8 | §8, Phụ lục C | 5-01, Bài 05 (cân hai số hạng) | 5-03 |
| 5-03 | Ví dụ 08.7, hình F3 | §8 | 2-03 (câu hỏi), 5-01 | 5-04, 7-03 |
| 5-04 | Định nghĩa 08.9; so với Mệnh đề 06.11 | §8 | 5-03 | 5-05 |
| 5-05 | Bài tập 08.8(b) | tệp bài tập | 5-03 | — |
| 6-00 | tiêu đề mạch 6 | §9 | 2-08 | 6-01 |
| 6-01 | Ví dụ 08.8, hình F4 | §9 | 2-08, 3-01 | 6-02 |
| 6-02 | trực quan, Mệnh đề 08.10 | §9 | 6-01, 3-01 | 6-03 |
| 6-03 | ý tưởng chứng minh Mệnh đề 08.10 | Phụ lục D, đoạn sau Mệnh đề 08.10 | 6-02 | 6-07 |
| 6-04 | Mệnh đề 08.12 (đọc thêm) | §9, Phụ lục E | Bài 05 (kì vọng có điều kiện), 6-01 | — |
| 6-05 | Ví dụ 08.9 | §9 | 2-10 | 6-06 |
| 6-06 | Ví dụ 08.10, mạng ReLU, "Kết luận:" | §9 | 4-01 | 7-04, 7-06 |
| 6-07 | Bài tập 08.3(d) | tệp bài tập | 6-01, 6-02 | — |
| 7-00 | tiêu đề mạch 7 | §10–§13 | — | 7-01 |
| 7-01, 7-02 | bảng tổng kết, sáu kết quả | §5–§9 | mạch 2–6 | 7-03 |
| 7-03 | vấn đề trung tâm, trả lời | §10 | 1-05, 1-06, 2-03 | 7-04 |
| 7-04–7-06 | bài tập tổng hợp 08.5(c), (d)(i), "Lời giải:" | tệp bài tập | 6-06 | 7-07 |
| 7-07 | câu hỏi tự kiểm tra | §4, §7, §12 | mạch 2, 4 | — |
| 7-08 | bài tập về nhà, viewer | §11 | — | tệp bài tập |
| 7-09 | tài liệu, Bài 09 | §12 đoạn cuối, §13 | — | Bài 09 |

**Thứ tự.** Các mạch ứng với các mục liên tiếp: 1 → mở đầu; 2 → §1–§5; 3 → §6; 4 → §7; 5 → §8; 6 → §9; 7 → §10–§13. Trong mỗi mục, thứ tự khối trên deck trùng ghi chú (§4: Định nghĩa 08.2 → đoạn Jensen → Ví dụ 08.2; §7: Định lý 08.6 → Ví dụ 08.5 → 08.6 → Hệ quả 08.7; §8: Hệ quả 08.8 → Ví dụ 08.7 → Định nghĩa 08.9; §9: Ví dụ 08.8 → Mệnh đề 08.10 → [Nhận xét 08.11] → Mệnh đề 08.12 → Ví dụ 08.9 → 08.10). Chỉ có một chỗ lệch: Thuật toán 08.1 (§4) lên trang 2-01, trước §2 và §3 (phát hiện M7).

**Số trang mỗi mạch** khớp `storyboard.md` §3: 6, 12, 5, 8, 6, 8, 10 (tổng 55).

## 2. Các mạch câu hỏi (threads)

| Câu hỏi mở | Mở ở | Đóng ở | Nhận xét |
|---|---|---|---|
| Thuật toán huấn luyện ảnh hưởng tới khoảng cách tổng quát hóa như thế nào? | 1-05 | 7-03 dòng 1 | đóng, bằng lời và công thức |
| Đại lượng nào quyết định khoảng cách (thí nghiệm)? | 1-06 | 4-03 ($t/200$), 4-04, 7-03 | đóng; ý "số tham số không giải thích" chỉ ở ghi chú diễn giả (N7) |
| Nhiều vòng trên $10^4$ hồ sơ có cho cận nhỏ hơn không? | 2-03 | 5-03 "Diễn giải:", 7-03 dòng 2 | đóng |
| Ví dụ 08.2 chỉ một dãy; cần với mọi dãy | 2-06 (chỉ ghi chú) | 3-02 bước 3 "trên từng quỹ đạo" | câu mở không có trên mặt (M3) |
| Bước khác biệt chưa được chặn | 2-10 dòng cuối | 3-01 | đóng, câu nối trên mặt |
| Cận tối ưu của Bài 05 dùng $\bar w_T$ | 4-05 dòng đầu | 5-02 | đóng |
| Bổ đề 08.4 hỏng khi không lồi | 6-01 "Diễn giải:" | 6-02, 6-03 | đóng |
| Câu hỏi Bài 07 trao cho Bài 08 (bảo đảm cho chính hàm SGD trả về; lớp chọn trước không phân biệt hai hàm cùng lớp) | deck 07, ghi chú diễn giả trang cuối | không có ở mở đầu deck 08 | M2 |
| Nhận xét 08.11 | không trang nào nêu trên mặt | 7-02 dẫn | M1 |

**Tính liên tục với decks trước.** Tên kỹ thuật nhắc lại khớp: "tổng triệt tiêu" (3-02; deck 05 `L05-4-05`), "cân hai số hạng" (5-02; deck 05), "kì vọng có điều kiện theo lịch sử" (6-04; deck 05 `L05-3-07`), "lập luận đổi vai" (4-02; deck 06 trang "Lập luận đổi vai"). Ghép cặp chưa có ở decks 01–07, nên dòng "Kỹ thuật." ở 2-05 đúng chỗ dùng lần đầu. Định nghĩa 06.9 và Định lý 06.10 ở 1-02 khớp deck 06 (giả thiết và loại bảo đảm). Trang cuối deck 07 ghi "Bài 08: Tính ổn định của SGD và tổng quát hóa trong học sâu.", trùng tiêu đề bìa deck 08; 7-09 ghi "Bài 09: Học chuỗi và mô hình sinh.", trùng tiêu đề ghi chú Bài 09, chữ thường như decks 06, 07.

**Bảng `Mục | Bài tập` (7-08)** khớp `exercises.md` (tám bài, đúng số hiệu). Mỗi bài nằm ở mạch cung cấp kiến thức cuối cùng nó cần: 08.1(a)(b) cần hệ số ổn định điểm lặp cuối (mạch 4); 08.6(b) cần Định lý 08.6 (mạch 4); 08.7 cần Hệ quả 08.7 (mạch 4); 08.2 so cận ổn định với cận tối ưu, 08.8(c) cần Định nghĩa 08.9 (mạch 5); 08.3(e) cần Mệnh đề 08.10, 08.4 cần Mệnh đề 08.12, 08.5 cần Ví dụ 08.10 (mạch 6). Mọi số hiệu Ví dụ/Bài tập dẫn trên mặt trang (08.1–08.10, Bài tập 08.1(c), 08.3(a), 08.3(d), 08.5, 08.7, 08.8) có trên trang nguồn với đúng số hiệu; riêng Nhận xét 08.11 thì không (M1).

**Từ khóa mạch trên mặt trang nội dung.** Có đủ ở mạch 2, 4, 6. Thiếu: "thừa số một phần cỡ mẫu" (mạch 3, không trang nội dung nào), "cận ghép" (mạch 5, chỉ ở 7-03) (N2).

## 3. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 7-02 (M1) | Mạch Tổng kết dẫn một kết quả chưa từng có trên mặt trang. Nhận xét 08.11 chỉ có ở ghi chú diễn giả 6-03. Đồng thời (T3) được thêm vào 2-02 nhưng không mặt trang nào dùng. Lý do cổng duyệt chuyển dòng Nhận xét 08.11 vào ghi chú ("(T3) chưa định nghĩa") không còn đúng, vì 2-02 nay đã định nghĩa (T3). | 7-02: "Đọc thêm: Nhận xét 08.11, Mệnh đề 08.12."; 2-02: "(T3) $\ell(w,z)\in[0,1]$"; review-log: "6-03 dòng Nhận xét 08.11 dùng (T3) chưa định nghĩa … chuyển vào ghi chú diễn giả" | Chọn một trong hai cách: (a) thêm lại một dòng trên 6-03, ví dụ "Nhận xét 08.11 (đọc thêm): thêm (T3), $\eta_t\le c/t$ cho cận đa thức theo $T$; $\beta=10$, $c=1$, $G=1$, $m=10^4$, $T=10^6$: $\le33{,}37>1$."; (b) bỏ "Nhận xét 08.11" khỏi 7-02 và bỏ (T3) khỏi 2-02. Cách (a) giữ được tham chiếu của 7-03 trong ghi chú diễn giả. |
| trung bình | 1-01, 1-05 (M2) | Mở đầu deck 08 không nhận câu hỏi mà deck 07 trao lại. Ghi chú mở đầu nói rõ vì sao cần cận cấp thuật toán: cận của Bài 07 đúng cho mọi hàm của một lớp chọn trước, nên không phân biệt hai hàm mà phép huấn luyện chọn. Trên deck 08, so sánh với Bài 07 chỉ xuất hiện ở ghi chú diễn giả 7-03. | Deck 07, ghi chú trang cuối: "Câu hỏi cho Bài 08: … quỹ đạo của hạ gradient ngẫu nhiên có cho một bảo đảm cho chính hàm nó trả về không?"; ghi chú Bài 08, dòng 3: "Bài 07 chặn khoảng cách tổng quát hóa đồng thời cho mọi hàm của một lớp chọn trước …"; ghi chú diễn giả 1-01 và 1-05 chỉ nhắc Bài 06 | Thêm vào ghi chú diễn giả 1-05 (trang tổng quan, mặt trang giữ nguyên): "Bài 07 chặn khoảng cách tổng quát hóa cho mọi hàm của một lớp chọn trước, nên không phân biệt hai hàm cùng lớp mà phép huấn luyện chọn khác nhau; bài này tìm bảo đảm cho chính hàm mà SGD trả về." |
| trung bình | 2-06 → 2-07 (M3) | Câu nối giữa ví dụ (một quỹ đạo) và bổ đề (mọi dãy) chỉ có trong ghi chú diễn giả. Trên 2-07, câu hỏi "ánh xạ này kéo hai điểm lại gần hay đẩy ra xa" cũng không có trên mặt, nên trang mở bằng một khẳng định và đi thẳng vào định nghĩa. Bài học deck 01: câu nối giữa hai cụm phải có trên mặt trang. | Ghi chú diễn giả 2-06: "Ví dụ chỉ xét một dãy chỉ số; Định nghĩa 06.9 cần kì vọng theo $\xi$, nên hai sự kiện … phải được chứng minh cho mọi dãy."; ghi chú §5 dòng 240: "Cần biết ánh xạ này kéo hai điểm lại gần hay đẩy chúng ra xa." | Thêm vào 2-06 (30 âm tiết, còn chỗ): "Đây là một dãy chỉ số; Định nghĩa 06.9 cần hai sự kiện trên với mọi dãy." Có thể thêm vào 2-07, sau dòng đầu: "**Câu hỏi:** ánh xạ này kéo hai điểm lại gần hay đẩy ra xa?" (2-07 hiện có 46 âm tiết). |
| trung bình | 4-00, 7-00 (M4) | Dòng dẫn mạch 4 và mạch 7 gần trùng nhau, và cũng lặp luận điểm bìa. Cả hai bỏ điều kiện độ dài bước; dòng dẫn mạch 4 bỏ thêm (G). Bài học deck 01 yêu cầu dòng dẫn không lặp một khuôn giữa các mạch và phát biểu rút gọn giữ đủ giả thiết. | 4-00: "Với hàm lỗi lồi, trơn, khoảng cách tổng quát hóa kì vọng tăng không nhanh hơn ngân sách độ dài bước chia cho cỡ mẫu."; 7-00: "Với hàm lỗi lồi, trơn, có gradient bị chặn, ngân sách độ dài bước chặn khoảng cách tổng quát hóa kì vọng." | 4-00: "Với hàm lỗi lồi, trơn, có gradient bị chặn và bước không quá $2/\beta$, …" (hoặc nói cơ chế: "Hàm lỗi Lipschitz đổi khoảng cách giữa hai lần chạy thành hệ số ổn định, chia cho cỡ mẫu."). 7-00: nêu ý tổng kết khác, ví dụ "Mỗi giả thiết của định lý có một phản ví dụ; với mạng ReLU huấn luyện mọi lớp, định lý không áp dụng." (≤ 25 âm tiết). |
| trung bình | 6-04 (M5) | $g_t$ trên mặt 6-04 không được gọi tên, và trong cùng deck mang hai nghĩa: ở 3-02 là $\nabla\ell(w_t,z_i)$ của lần chạy thứ nhất, ở 6-04 là gradient ngẫu nhiên của $F$. Dòng "Nhắc lại:" chỉ nhắc lịch sử. Ghi chú cũng có lỗi này, đã ghi trong đề xuất cho tác giả. | 3-02 bước 2: "$g_t=\nabla\ell(w_t,z_i)$"; 6-04: "$\mathbb E[g_t\mid\mathcal F_{t-1}]=\nabla F(w_t)$"; review-log: "$g_t$ ba nghĩa" | Trên 6-04, gọi tên ngay trong giả thiết: "gradient ngẫu nhiên $g_t$: $\mathbb E[g_t\mid\mathcal F_{t-1}]=\nabla F(w_t)$, …". Khi tác giả chốt kí hiệu trong ghi chú, đổi theo ở 3-02. |
| nhẹ | 6-03 → 6-04 (N1) | Không có câu nối trên mặt cho lý do Mệnh đề 08.12 có mặt: không có tính lồi, SGD vẫn có bảo đảm tối ưu, nhưng cho một đại lượng yếu hơn. Câu này của ghi chú chỉ ở ghi chú diễn giả 6-00. | ghi chú §9 dòng 822: "Không có tính lồi, SGD vẫn có một bảo đảm tối ưu, nhưng cho một đại lượng yếu hơn sai số tối ưu thực nghiệm." | Nếu còn chỗ (6-04 có 50 âm tiết), mở trang bằng câu này. Nếu không, đổi dòng cuối thành "Ví dụ 08.8: $w=0$ là điểm dừng, $L_s(0)=2$ lớn nhất; tính dừng yếu hơn sai số tối ưu." |
| nhẹ | 3-00, 5-00 (N2) | Từ khóa mạch không có trên mặt trang nội dung của chính mạch: "thừa số một phần cỡ mẫu" không ở trang nào; "cận ghép" chỉ ở 7-03. | kết quả đếm bằng script (mục 2) | Đổi từ khóa theo chữ có trên mặt ("thừa số $1/m$", "rủi ro vượt mức sau nhiều vòng"), hoặc dùng chữ đó ở 3-01 "Trực quan." / 5-01 "Trực quan." |
| nhẹ | 2-09, 4-02 (N3) | "Đổi vai $u$, $v$" ở 2-09 dùng lại tên của kỹ thuật "lập luận đổi vai" (Bài 06), mà 4-02 nhắc lại ba trang sau. Hai thao tác khác nhau. Deck theo ghi chú (Phụ lục A, Bước 4). | 2-09 bước 4: "đổi vai $u$, $v$ rồi cộng"; 4-02: "**Nhắc lại:** Định lý 06.10 dựa trên lập luận đổi vai (Bài 06)." | Chờ tác giả (xem đề xuất ghi chú 2); nếu tác giả đồng ý, đổi 2-09 thành "hoán đổi $u$, $v$ rồi cộng". |
| nhẹ | 2-00 (N4) | Ba trang đầu mạch 2 (2-01–2-03: thiết lập, giả thiết, ví dụ xuyên suốt) không thuộc chủ đề mà tiêu đề và dòng dẫn mạch nêu. Ghi chú diễn giả 2-00 cũng không nói mạch mở bằng phần thiết lập. | 2-00 ghi chú diễn giả bắt đầu từ Định nghĩa 06.9; `storyboard.md` §3 giải thích lý do gộp §1–§5 | Thêm vào ghi chú diễn giả 2-00 câu đầu: "Mạch mở bằng thiết lập, giả thiết và hai ví dụ xuyên suốt; sau đó …". Giữ nguyên số mạch (bảy). |
| nhẹ | 5-01 (N5) | Lý do cần mạch 5 (Định lý 08.6 chặn khoảng cách tổng quát hóa, không chặn rủi ro kì vọng) chỉ có ở ghi chú diễn giả 5-00. Mặt trang chỉ có dòng "Nhắc lại:" của Mệnh đề 06.5(b). | ghi chú diễn giả 5-00: "Định lý 08.6 chặn khoảng cách tổng quát hóa, không chặn rủi ro kì vọng; cần thêm số hạng tối ưu." | Nếu trần 60 cho phép, mở 5-01 bằng "Định lý 08.6 chặn khoảng cách tổng quát hóa; rủi ro vượt mức cần thêm số hạng tối ưu." Nếu không, nối vào dòng "Nhắc lại:". |
| nhẹ | 4-04, 1-06, 6-02 (N6) | Chữ "khoảng cách" trơ được dùng cho hai đại lượng: khoảng cách tổng quát hóa và khoảng cách $\Delta$ giữa hai lần chạy. 4-04 đặt hai nghĩa cạnh nhau. Ghi chú cũng dùng như vậy. | 4-04: "$\Delta\approx5{,}458$, khoảng cách $0{,}919$"; 1-06: "đại lượng nào quyết định khoảng cách?"; 6-02: "nhân khoảng cách với $1+\beta\eta_t$" | 4-04: "khoảng cách tổng quát hóa $0{,}919$". Ở các trang khác, khi nghĩa là $\Delta_t$, viết "$\Delta$" hoặc "khoảng cách giữa hai lần chạy". |
| nhẹ | 7-03 (N7) | Câu trả lời cuối không đóng ý chính của câu hỏi mở đầu: số tham số và lớp hàm như nhau ở mọi dòng của bảng, nên không giải thích sự thay đổi. Ý này chỉ có ở ghi chú diễn giả 1-06 và 7-03. | ghi chú diễn giả 7-03: "… chia cho cỡ mẫu, không qua số tham số" | Dòng 1 của 7-03: "Thuật toán tác động qua ngân sách độ dài bước, không qua số tham số: …" (7-03 đang ở 60/60; bỏ "(T1), (T2)" sẽ làm mất giả thiết, nên cắt chữ ở dòng 2 thay vì ở dòng 1). |
| nhẹ | 2-01 (M7) | Thuật toán 08.1 thuộc §4 nhưng đứng trên trang thiết lập của §1, trước §2 và Ví dụ 08.1. `storyboard.md` §3 có ghi lý do, nhưng `review-log.md` chưa ghi quyết định. Nguồn trong ghi chú diễn giả chỉ ghi §1. | 2-01: "**Thuật toán 08.1.** …"; nguồn: "Nguồn: ghi chú Bài 08, §1, Thuật toán 08.1 và hai đoạn sau." | Điều phối viên ghi chấp nhận lệch vào `review-log.md`. Sửa dòng nguồn: "Nguồn: ghi chú Bài 08, §1; §4, Thuật toán 08.1 và hai đoạn sau." |
| nhẹ | 7-01 (N8) | Ô "Giả thiết không được bỏ" của Định lý 08.6 viết "như trên", nên kéo theo "ghép cặp" của Mệnh đề 08.5 (là công cụ chứng minh, không phải giả thiết của định lý), và thiếu "$\xi$ độc lập với $S$" mà 4-01 có. | 7-01: "như trên; (T1), (T2); $W$ lồi"; 4-01: "$\xi$ độc lập với $S$" | "(S), (G), $\eta_t\le2/\beta$; (T1), (T2); $\xi$ độc lập với $S$; $W$ lồi". |
| nhẹ | 4-05, 4-07 (N9) | Ghi chú diễn giả 4-05 tính sẵn cận $39{,}975$ và giá trị đúng $0{,}4750$, tức chính đáp số của Bài tập 08.7(b) ở 4-07, hai trang sau. | ghi chú diễn giả 4-05: "… cận là $39{,}975$ … khoảng cách thật là $0{,}4750$"; 4-07 lời giải: "$39{,}975$ … $0{,}4750$" | Ở 4-05, chỉ giữ phần dẫn ("Chương trình của Ví dụ 06.3 thỏa (S) với $\beta=2$, (G) với $G=4$ trên $W$; bài tập sau tính cận.") và bỏ hai con số. |
| nhẹ | 1-04 (N10) | Dòng nguồn khó đọc. | "Nguồn: ghi chú Bài 08; §13." | "Nguồn: ghi chú Bài 08, đoạn mở đầu, §13." |
| nhẹ | `storyboard.md` (N11) | Các mục §4, §6, §12 còn dùng số trang cũ và mô tả cũ: Hệ quả 08.7 "lộ trình ở ghi chú diễn giả 4-05", bài tập 08.7 ở "4-06", "7-02 Vấn đề trung tâm". Chỗ đúng chỉ ghi ở §16. Điều kiện "Done" yêu cầu storyboard khớp deck. | `storyboard.md` §4 hàng Hệ quả 08.7; §6 tiêu đề `4-06`, `7-02`; §3 dòng dẫn mạch 4, 6, 7 | Sau vòng sửa, người sửa cập nhật §3, §4, §12 theo ID của deck, hoặc ghi ở đầu §6 và §12 rằng §16 thay thế. |

Không có phát hiện `chặn bàn giao` hay `nghiêm trọng`. Các mục đạt:
- trang "Vấn đề trung tâm" mở đầu chỉ có một hộp, câu hỏi mở;
- trang "Vấn đề trung tâm" cuối trả lời cho cả bài, có lời;
- mạch Tổng kết đủ thành phần và đúng thứ tự;
- `#/N` khớp;
- không mặt trang nào xem trước bài sau;
- hành trình khái niệm đúng thứ tự cho sáu kết quả chính.

## 4. Đề xuất sửa ghi chú (cho điều phối viên và tác giả)

1. **$g_t$ nhiều nghĩa** (đã có trong `review-log.md`). Trong chứng minh Mệnh đề 08.5, $g_t$ là gradient của lần chạy thứ nhất; trong Mệnh đề 08.12, $g_t$ là gradient ngẫu nhiên. Đề xuất đổi kí hiệu trong chứng minh Mệnh đề 08.5 (ví dụ $a_t$, $a'_t$), hoặc đặt tên $g_t$ ngay trong Mệnh đề 08.12.
2. **"Đổi vai" ở Phụ lục A, Bước 4** trùng tên "lập luận đổi vai" (exchange argument) của Bài 06. Đề xuất viết "hoán đổi $u$ và $v$" ở dòng 983 (Lộ trình) và dòng 1016 (Bước 4).
3. **"Khoảng cách" trơ.** Ghi chú dùng chữ này cho cả khoảng cách tổng quát hóa và $\Delta_t$, ví dụ "Bảng của Ví dụ 08.6" và §10 ("khoảng cách đo được"). Đề xuất luôn viết đủ tên khi hai đại lượng đứng gần nhau.
4. Không thấy lỗi thứ tự hay tham chiếu tới khối sau trong các mục mà deck dùng.

## 5. Kết luận

**đạt khi sửa** — 0 chặn bàn giao, 0 nghiêm trọng, 5 trung bình (M1–M5), 12 nhẹ (N1–N11, M7).
