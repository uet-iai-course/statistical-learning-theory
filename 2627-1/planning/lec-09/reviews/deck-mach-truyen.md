# Duyệt deck Bài 09 — Vai 5: mạch truyện và liên kết

Người duyệt: tác tử `mach-truyen` (chỉ đọc), 2026-11-16. Bản duyệt: `2627-1/lecture-09-hoc-chuoi-mo-hinh-sinh.html` (đóng băng, 55 trang). Đối chiếu: `materials/lec-09/lecture-note.md`, `exercises.md`, `planning/lec-09/storyboard.md` (§3, §7, §9, §11, §14, §16), quyết định cuối `review-log.md` § Bộ trang chiếu, decks 02 (`L02-4-04`, Hệ quả 02.10), 04 ((T7)), 05 (Hệ quả 05.15, (C), (G1), (G2)), 08 (trang cuối), 10 (trang bìa). Bảng kiểm liên tục: phần Outline/Threads/Concept của `quill/references/workflows.md` (không tạo `quill.json`). Không đọc UML (vai này không cần). Các điểm đã chốt ở storyboard §11 (Ví dụ 09.1 trên trang Định nghĩa 09.1, Nhận xét 09.5 ở 3-09, "Trực quan." của Mệnh đề 09.15 ở 6-01, 55 trang) không nêu lại thành phát hiện.

Đã chạy (script trong thư mục nháp `lec-09/rv-mach-truyen/`):
- `deck_lint.py`: 0 phát hiện, 55 trang.
- Playwright 1600×900 (`links.py`): sáu liên kết `#/2`…`#/7` của 1-04 mở đúng `L09-2-00`…`L09-7-00`; bấm `#/5` tới `L09-5-00`. Hai liên kết viewer của 7-05 trả 200, tiêu đề đúng Bài 09, trang viewer có liên kết ngược về deck. Không lỗi trang.
- Đếm âm tiết mặt trang (`dens.py`, xấp xỉ cách đếm của `deck_lint.py`) để kiểm biên cho các đề xuất thêm chữ. Tìm thuật ngữ trên mặt trang: "tích phân" chỉ ở 4-03; "SGD" chỉ ở tiêu đề 6-08; "dạng đóng", "rút điểm" không ở mặt trang nào.

## 1. Bảng chức năng từng trang và đối chiếu trang → mục ghi chú

| Trang | Vai trò trong mạch | Mục ghi chú | Kết nối vào | Kết nối ra |
|---|---|---|---|---|
| 1-01 | bìa, luận điểm một câu có điều kiện | đoạn mở, §10 | deck 08, ghi chú diễn giả trang cuối (câu hỏi cho Bài 09) | 7-00, 7-02 |
| 1-02 | tiên quyết: $L_D$, $L_S$, ERM, (T1)–(T3), Hệ quả 02.10(b), Nhận xét 02.11 | Kiến thức tiên quyết; câu ôn nhanh 1–2 | Bài 01, 02 | 2-03, 3-06, 4-03 |
| 1-03 | mục tiêu 1–5 | Mục tiêu học tập | — | mạch 2–6 |
| 1-04 | nội dung `#/2`…`#/7`, đọc trước | §13 | — | mạch 2–7 |
| 1-05 | vấn đề trung tâm, một hộp "Câu hỏi:" | đoạn mở, dòng 5 | — | 7-02 |
| 1-06 | ví dụ dẫn nhập ($\mathtt{ABB}$), "Câu hỏi:" $m$ chuỗi và $3m$ quan sát | Câu hỏi mở đầu | 1-05 | 2-01, 2-02, 3-01, 3-03, 3-06, 7-04 câu 1 |
| 2-00 | tiêu đề mạch 2 | §1–§4 | 1-06 | 2-01 |
| 2-01 | thiết lập bảy thành phần, cỡ mẫu $m$ | §1; §3 khối ứng dụng (ghi chú diễn giả) | 1-02, 1-06 | 2-02, 2-04, 3-06 |
| 2-02 | Ví dụ 09.1 (Bước 2), Định nghĩa 09.1 | §1 Định nghĩa 09.1 và đoạn sau; §3 Ví dụ 09.1 | 1-06 | 3-06 (A), 3-08 (B), 7-02, 7-04 câu 2 |
| 2-03 | ba điểm khác của hàm lỗi log; (T1) cho cả chuỗi; (T7) | §2 | 1-02 | 2-06, 3-06, 3-08 |
| 2-04 | Định nghĩa 09.2, MLE là ERM | §4 Định nghĩa 09.2 và đoạn sau | 2-01 | 2-05, 4-04 |
| 2-05 | Ví dụ 09.2, trường hợp biên $m_1=0$ | §4 Ví dụ 09.2 | 2-04 | 4-05, 4-06 |
| 2-06 | Bài tập 09.8(c), lời giải | tệp bài tập; §2 | 2-03, 2-04 | 3-00 |
| 3-00 | tiêu đề mạch 3 | §5–§6 | 2-04 | 3-01 |
| 3-01 | vấn đề $\lvert\mathcal A\rvert^n-1$, kí hiệu, trực quan, Mệnh đề 09.3 | §5 đoạn mở, Mệnh đề 09.3 | 1-06 | 3-02, 3-03 |
| 3-02 | ý tưởng chứng minh; "Kỹ thuật." tổng theo kí tự cuối | Phụ lục D | 3-01 | 3-03 |
| 3-03 | Định nghĩa 09.4, bigram, độ bối rối, Ví dụ 09.3 | §5 Định nghĩa 09.4, đoạn sau, Ví dụ 09.3 | 3-01(c), 1-06 | 3-04, 3-06 |
| 3-04 | Bài tập 09.1(a), (c), đề | tệp bài tập | 3-03 | 3-05 |
| 3-05 | lời giải 09.1(a), (c); $x_3$ phụ thuộc $x_1$ | tệp bài tập | 3-04 | 3-06 |
| 3-06 | quan sát độc lập ở cấp chuỗi; Ví dụ 09.4 Bước 1–2 | §6 đoạn mở; Ví dụ 09.4 | 3-05, 1-02, 2-03 | 3-07, 7-02, 7-03 |
| 3-07 | Ví dụ 09.4 Bước 3–5, bảng ba cách đếm; "Nhắc lại:" đảo cận đuôi | Ví dụ 09.4 | 3-06, `L02-4-04` | 7-02, 7-03 |
| 3-08 | Ví dụ 09.5, hình F1 | §6 Ví dụ 09.5; Phụ lục C | 2-02 (B), 2-03 (T7) | 7-02, 7-04 câu 2 |
| 3-09 | Nhận xét 09.5, Định nghĩa 09.6, Ví dụ 09.6 | §5 Nhận xét 09.5; §6 Định nghĩa 09.6, Ví dụ 09.6 | 3-03 | 7-05 (09.1(d), 09.5) |
| 4-00 | tiêu đề mạch 4 | §7 | 2-01 | 4-01 |
| 4-01 | vấn đề ($D$ chưa biết), Định nghĩa 09.7, KL không đối xứng | §7 đoạn mở, Định nghĩa 09.7, hai đoạn sau | 2-01, 2-05 | 4-02, 4-05 |
| 4-02 | trực quan, Mệnh đề 09.8 | §7 Mệnh đề 09.8 | 4-01 | 4-03, 4-04, 4-05, 4-07, 6-07 |
| 4-03 | ý tưởng chứng minh; "Kỹ thuật." $\ln t\le t-1$ | chứng minh Mệnh đề 09.8 | 4-02, 1-02 (ghi chú diễn giả) | 5-03, 7-04 câu 4 |
| 4-04 | Hệ quả 09.9, chứng minh một dòng | Hệ quả 09.9 và chứng minh | 4-02 | 4-05, 4-08(c); 4-07 chỉ ở ghi chú diễn giả |
| 4-05 | "Câu hỏi:" và trả lời bằng số | đoạn sau Hệ quả 09.9 | 2-05, 4-01, 4-02(b) | 4-06 |
| 4-06 | Ví dụ 09.7 Bước 3–4; làm trơn cộng một | Ví dụ 09.7 (Bước 1–2 ở ghi chú diễn giả) | 2-05, 4-05 | 4-07 |
| 4-07 | Ví dụ 09.8, quá khớp | Ví dụ 09.8; §3 khối ứng dụng | 4-06, 4-02(b), 3-06 | 6-07, 7-03 |
| 4-08 | Bài tập 09.3(b), (c), lời giải | tệp bài tập | 4-02, 4-04 | 5-00 |
| 5-00 | tiêu đề mạch 5 | §8 | 4-02 (chỉ ghi chú diễn giả) | 5-01 |
| 5-01 | Định nghĩa 09.10, Ví dụ 09.9 | §8 đoạn mở, Định nghĩa 09.10, Ví dụ 09.9 | 1-02 (câu ôn 3, ghi chú diễn giả) | 5-02, 5-04 |
| 5-02 | Định nghĩa 09.11, trực quan, Định lý 09.12 | §8 | 5-01, 4-01 | 5-03, 5-04, 5-05 |
| 5-03 | ý tưởng chứng minh; "Nhắc lại:" $\ln t\le t-1$; "Kỹ thuật." thêm bớt $\ln q$ | chứng minh Định lý 09.12 | 5-02, 4-03 | 5-04 |
| 5-04 | Ví dụ 09.10, hình F2 | Ví dụ 09.10 | 5-01, 5-02 | 6-05, 6-08, 7-04 câu 3 |
| 5-05 | thuật toán EM, Hệ quả 09.13, chứng minh | §8 cuối, Hệ quả 09.13; Phụ lục D | 5-02(b) | 5-06, 7-01 |
| 5-06 | Bài tập 09.4(b), lời giải | tệp bài tập | 5-02, 5-05 | — |
| 6-00 | tiêu đề mạch 6 | §8 đoạn cuối, §9 | 5-05 (chỉ ghi chú diễn giả) | 6-01 |
| 6-01 | $F(\phi)$, Định nghĩa 09.14, trực quan | §9 đoạn mở, Định nghĩa 09.14, đoạn sau | 5-02 (chỉ ghi chú diễn giả) | 6-02 |
| 6-02 | Mệnh đề 09.15 | §9 Mệnh đề 09.15 | 6-01 | 6-03, 6-04 |
| 6-03 | ý tưởng chứng minh | chứng minh phác thảo; Phụ lục B | 6-02 | 6-04, 6-06 |
| 6-04 | "Kỹ thuật." đổi chỗ đạo hàm và kì vọng | Mệnh đề 09.15; Phụ lục B | 6-03 | 6-05; Bài 10 |
| 6-05 | Ví dụ 09.11 | Ví dụ 09.11 | 5-04, 6-02 | 6-08 |
| 6-06 | Ví dụ 09.12, phản ví dụ bỏ (i) | Ví dụ 09.12 | 6-02 | 7-02 |
| 6-07 | Ví dụ 09.13 | đoạn trước, Ví dụ 09.13, đoạn sau | 4-02(c); 4-07 (ngầm) | 7-00 |
| 6-08 | Bài tập 09.7(c), (d); "Nhắc lại:" Hệ quả 05.15 | tệp bài tập | 6-05, 5-04, `L05-4-07` | — |
| 7-00 | tiêu đề mạch 7 | §10–§13 | — | 7-01 |
| 7-01 | bảng tổng kết, bốn hàng | §10 | 3-01, 4-02, 4-04, 5-02, 5-05, 6-02 | 7-02 |
| 7-02 | vấn đề trung tâm cuối, bốn dòng | §10 đoạn 1 | 1-05 | — |
| 7-03 | Bài tập 09.6(b), bài tổng hợp | tệp bài tập; Phụ lục C | 3-06, 4-06, 4-07 | — |
| 7-04 | bốn câu tự kiểm tra | §12 (a)–(c); chứng minh Mệnh đề 09.8, Bước 2 | 1-06, 3-08, 5-04, 4-03 | — |
| 7-05 | `Mục \| Bài tập`, liên kết viewer | §11 | — | ghi chú, bài tập |
| 7-06 | tài liệu tham khảo, dòng Bài 10 | §12 đoạn cuối, §13 | — | Bài 10 |

Mỗi mạch ứng với các mục liên tiếp: mạch 2 §1–§4, mạch 3 §5–§6, mạch 4 §7, mạch 5 §8, mạch 6 §9, mạch 7 §10–§13. Trong mạch, thứ tự khái niệm theo ghi chú, trừ hai lệch đã chốt (Ví dụ 09.1 ở 2-02 trước §2; Nhận xét 09.5 ở 3-09).

## 2. Các mạch câu hỏi (threads)

| Mạch câu hỏi | Mở | Đi qua | Đóng trên mặt trang |
|---|---|---|---|
| $m$ chuỗi hay $3m$ quan sát | 1-06 "Câu hỏi:" | 2-01, 2-02, 3-05, 3-06 | 3-07 (bảng ba cách đếm), 7-02 |
| Hàm lỗi log không bị chặn | 1-02 (Nhận xét 02.11) | 2-03, 2-05, 2-06, 3-06 ($c>0$), 4-06 | 4-07, 7-02, 7-03 |
| Chuỗi thời gian, cửa sổ chồng lấn | 2-02 | 2-03 (T7), 3-08 | 7-02, 7-04 câu 2 |
| Tập huấn luyện của Ví dụ 09.2 và $\mathrm{Ber}(0{,}6)$ | 2-05 | 4-01 ($0{,}0226$) | 4-05 |
| Ứng dụng chuỗi DNA và ba câu hỏi thực hành (§3) | ghi chú diễn giả 2-01 | 3-06, 3-07, 4-07 | ghi chú diễn giả 4-07 (xem M4) |
| Bảng $\mathtt{ABB}$ | 1-06 | 2-02, 3-03 | 7-04 câu 1 |
| Mô hình Gauss tại $x=2$ | 5-01 | 5-04, 6-05 | 6-08, 7-04 câu 3 |
| Bằng chứng không tính được → ELBO → bước E không tính được → tái tham số hóa | ghi chú diễn giả 5-00, 6-00 | — | 6-02 (xem M1, M2) |
| Độ hợp lý và dữ liệu sinh ra | ghi chú diễn giả 6-00 | — | 6-07 "Kết luận:" (xem M3) |
| Kỹ thuật $\ln t\le t-1$ | ghi chú diễn giả 1-02 (câu ôn 2) | 4-03 | 5-03 "Nhắc lại:" |

Liên tục với các deck trước: tên "Đảo cận đuôi thành bán kính và cỡ mẫu" ở 3-07 trùng `L02-4-04`; Hệ quả 02.10(b) ở 1-02 trùng `L02` (giả thiết (T1)–(T3), $h$ cố định); "Nhắc lại:" Hệ quả 05.15 ở 6-08 trùng `L05-4-07` (phần (a) với mọi $u\in W$ cách $w_1$ không quá $R$, kì vọng). Câu hỏi cuối deck 08 (ghi chú diễn giả `L08-7-09`: rủi ro, rủi ro thực nghiệm và giả thiết độc lập viết lại thế nào khi quan sát là chuỗi) được nhận ở ghi chú diễn giả 1-01 và trả lời trên mặt 2-01, 2-03. Ghi chú diễn giả 7-06 trao câu hỏi cho Bài 10, và bìa deck 10 nhận lại ("ở Bài 09, thuật toán chọn phân bố biến phân nhưng dữ liệu vẫn rút từ $D$"). Từ khóa mạch 2–6 đều có trên mặt trang nội dung của chính mạch.

## 3. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 5-00 → 5-01, 5-02 (M1) | Câu nối từ mạch 4 sang mạch 5 không có trên mặt trang. Lý do cần cận dưới bằng chứng là bằng chứng là một tích phân nói chung không tính được. Kết quả kế thừa là Mệnh đề 09.8 và Hệ quả 09.9 áp dụng cho $p_\theta(x)$. Cả hai chỉ có ở ghi chú diễn giả 5-00. Bước "vấn đề" của Định lý 09.12 vì thế không có mặt trang nào. Storyboard §7 cũng ghi bước này ở "5-00 ghi chú diễn giả". Trên mặt trang, "tích phân" chỉ xuất hiện ở 4-03. | ghi chú §8, dòng 534: "Khi mô hình quan sát là một mạng nơ-ron, tích phân này nói chung không tính được"; dòng 574: "Khi tích phân của bằng chứng không tính được, chúng ta làm việc với một đại lượng chỉ cần giá trị của $p_\theta(x,v)$."; 5-01 dòng 1: "Rút một biến không quan sát được, rồi rút quan sát." | 5-01 dòng 1: "Rút một biến không quan sát được, rồi rút quan sát; độ hợp lý là một tích phân theo biến đó, nói chung không tính được." Mật độ $45\to$ khoảng $56$, số dòng giữ $6$. Câu "Mệnh đề 09.8 áp dụng cho $p_\theta(x)$" để ở ghi chú diễn giả. |
| trung bình | 6-00 → 6-01 (M2) | Câu nối từ EM sang tái tham số hóa không có trên mặt trang. Khi hậu nghiệm không có dạng đóng, bước E không tính được, nên ELBO được cực đại hóa bằng SGD và cần gradient theo $\phi$. 6-01 mở bằng $F(\phi)=\mathbb E_{v\sim q_\phi}f(v)$ nhưng không nói $F$ là ELBO hay vì sao cần $\nabla F$. Câu này chỉ có ở ghi chú diễn giả 6-00. | ghi chú §8, dòng 695: "Khi hậu nghiệm không có dạng đóng, bước E không tính được … cực đại hóa ELBO theo $(\theta,\phi)$ bằng SGD"; §9, dòng 699: "Để cực đại hóa ELBO bằng SGD, chúng ta cần gradient của $\phi\mapsto\mathbb E_{v\sim q_\phi}f(v)$."; 6-01 dòng 1: "$F(\phi)=\ldots$: $\nabla F$ nói chung khác …" | Cách (a): 6-01 dòng 1 thành "Hậu nghiệm không có dạng đóng: cực đại hóa ELBO bằng hạ gradient ngẫu nhiên (SGD) cần $\nabla F$, $F(\phi)=\mathbb E_{v\sim q_\phi}f(v)$; nói chung $\nabla F\ne\mathbb E\nabla_\phi f(v)=0$ vì phân bố phụ thuộc $\phi$." 6-01 đang ở khoảng $52$ âm tiết và $6$ dòng, nên cần cắt bù khoảng $5$ âm tiết, chẳng hạn chuyển "Gauss: …" của dòng 3 vào ghi chú diễn giả. Cách (b): đổi dòng dẫn 6-00 (≤ 25), ví dụ "Khi hậu nghiệm không có dạng đóng, ELBO được tối ưu bằng gradient, cần đổi chỗ đạo hàm và kì vọng." Cách (a) cũng sửa N4 cho "SGD". |
| trung bình | 6-07 (M3) | Ví dụ 09.13 đổi chủ đề, từ gradient sang so sánh các mô hình sinh, mà mặt trang không có câu nối. Dòng dẫn 6-00 chỉ nói về tái tham số hóa. Trang này còn chen giữa hai ví dụ gradient (6-05, 6-06) và bài tập gradient 6-08, nên mạch gradient bị ngắt một trang. "$50$ chuỗi DNA" không nói là thiết lập của Ví dụ 09.8. | ghi chú §9, dòng 801: "Một mô hình sinh còn được dùng để rút điểm mới từ $p_\theta$; mức giống dữ liệu thật của các điểm sinh ra là một tiêu chí khác hàm lỗi log."; câu này chỉ ở ghi chú diễn giả 6-07 và 6-00; storyboard §7, hàng Ví dụ 09.13: vấn đề ở "6-00 ghi chú diễn giả"; Ví dụ 09.13, Bước 4: "Thiết lập của Ví dụ 09.8 với $50$ chuỗi huấn luyện" | Mở 6-07 bằng "Mô hình sinh còn dùng để rút điểm mới; mức giống dữ liệu thật là tiêu chí khác hàm lỗi log." Viết "$50$ chuỗi của Ví dụ 09.8". 6-07 đang ở khoảng $59$ âm tiết, nên cắt bù: chuyển "so với $2{,}5484$ của $p_{\theta_2}$" vào ghi chú diễn giả và gộp hai dòng mô hình ghi nhớ thành một. Tùy chọn: đổi chỗ 6-07 và 6-08, để bài tập SGD đứng ngay sau Ví dụ 09.11, 09.12 và "Kết luận:" của 6-07 đóng mạch 6. Khi đó cập nhật mã trang. |
| trung bình | 4-07 (M4) | Mạch "ví dụ xuyên suốt" chuỗi DNA (§3) không có trên mặt trang. Ba câu hỏi thực hành chỉ ở ghi chú diễn giả 2-01. Câu trả lời (i) (cách giá trị tốt nhất khoảng $0{,}0009$ ở $m=50$) và (iii) (khoảng tin cậy dùng số chuỗi kiểm tra) chỉ ở ghi chú diễn giả 4-07. Storyboard §11.5 ghi rằng 4-07 trả lời ba câu hỏi trên mặt trang. Mối nối với Hệ quả 09.9(b) ("đặc tả đúng") cũng chỉ ở ghi chú diễn giả, dù 4-04 vừa nêu từ khóa này. | ghi chú §3, dòng 178–182 (ba câu hỏi); Ví dụ 09.8, dòng 525–529: "Tóm lại, ba câu hỏi thực hành có câu trả lời sau: (i) … $0{,}0009$ … (iii) … dùng số chuỗi kiểm tra làm cỡ mẫu (Ví dụ 09.4)"; dòng 498: "lớp mô hình bigram chứa mô hình thật" | 4-07 còn chỗ (khoảng $38$ âm tiết, $4$ dòng). Thêm một dòng: "$m=50$: cách giá trị tốt nhất $\approx0{,}0009$; khoảng tin cậy dùng số chuỗi kiểm tra (Ví dụ 09.4)." Dòng thiết lập thêm "lớp bigram chứa mô hình thật (đặc tả đúng)". Tổng khoảng $57$ âm tiết. |
| trung bình | 7-02 (M5) | Trang "Vấn đề trung tâm" cuối chưa trả lời trọn câu hỏi "như thế nào". Dòng 4 nêu tính chất của khe nhưng không nói học mô hình biến ẩn bằng cách nào: cực đại hóa ELBO, tức tối thiểu hóa một cận trên của rủi ro thực nghiệm, bằng EM hoặc gradient theo đường đi. Dòng 3 bỏ đại lượng được chặn. Bài học deck 02 yêu cầu dòng rút gọn giữ "với xác suất ít nhất $1-\delta$" cùng đại lượng được chặn. | 7-02 dòng 3: "Cận Hoeffding (xác suất $\ge1-\delta$): mô hình cố định, mọi xác suất $\ge c>0$, trên $m_v$ chuỗi kiểm tra."; dòng 4: "Biến ẩn: khe $=\mathrm{KL}$ tới hậu nghiệm; …"; Định lý 09.12, câu sau $\square$: "Tối thiểu hóa $-\frac1m\sum_i\operatorname{ELBO}$ … là tối thiểu hóa một cận trên của rủi ro thực nghiệm"; `common-brief.md`, bài học deck 02 | Giữ trần $60$: dòng 3 "Với xác suất $\ge1-\delta$: $\lvert L_V(\theta)-L_D(\theta)\rvert\le b\sqrt{\ln(2/\delta)/(2m_v)}$, $\theta$ cố định, mọi xác suất $\ge c>0$." (ngắn hơn bản hiện tại khoảng $5$ âm tiết); dòng 4 "Biến ẩn: cực đại hóa ELBO, khe $=\mathrm{KL}$ tới hậu nghiệm; gradient theo đường đi không chệch dưới (i)–(iii)." ($+3$). Dòng 2: bỏ "thêm" nếu cần. |
| nhẹ | 6-08 (N1) | (C) và (G1) được gọi tên trên mặt trang mà không có nội dung. (G2) có nội dung ($\mathbb E\lVert\varphi\rVert^2\le G^2$). Điều phối viên đã giao người duyệt đánh giá điểm này. 6-08 còn chỗ (khoảng $46$ âm tiết). | 6-08: "dưới (C), (G1), (G2) $\mathbb E\lVert\varphi\rVert^2\le G^2$"; `L05`: "(C) $F$ lồi, $W$ khác rỗng, đóng, lồi"; "(G1) không chệch: $\psi(w)\in\partial F(w)$" | "dưới (C) $F$ lồi, $W$ đóng, lồi; (G1) oracle không chệch; (G2) $\mathbb E\lVert\varphi\rVert^2\le G^2$; …" (khoảng $+9$). |
| nhẹ | 1-02, 6-08 (N2) | Hai chữ viết tắt xuất hiện trên mặt trang trước tên đầy đủ. "ERM" ở 1-02 đứng trước 2-04, nơi lần đầu có "tối thiểu hóa rủi ro thực nghiệm (ERM)". "SGD" chỉ có ở tiêu đề 6-08, và không mặt trang nào có "hạ gradient ngẫu nhiên". | 1-02: "ERM làm nhỏ nhất $L_S$"; 2-04: "tức tối thiểu hóa rủi ro thực nghiệm (ERM)"; tìm "SGD" trên mặt trang: chỉ tiêu đề 6-08 | 1-02: "tối thiểu hóa rủi ro thực nghiệm (ERM) làm nhỏ nhất $L_S$" ($51\to56$). "SGD": theo M2 cách (a), hoặc dòng "Nhắc lại:" của 6-08 viết "Hệ quả 05.15 (hạ gradient ngẫu nhiên có chiếu)". |
| nhẹ | 1-02, 2-03 (N3) | (T7) là giả thiết của Bài 04 ("mẫu xác thực độc lập"). Trên 2-03 nó hiện ra như giả thiết mới, dưới tên "tập kiểm tra", không có "Nhắc lại:" hay "Bài 04". Ghi chú liệt kê (T7) trong Kiến thức tiên quyết, còn 1-02 thì không. | ghi chú, Kiến thức tiên quyết: "Từ Bài 04. Giả thiết (T7), mẫu độc lập với tập huấn luyện"; `L04`: "(T7): $V=(V_1,\ldots,V_{m_v})\sim D^{m_v}$ độc lập với $S$, cỡ mẫu xác thực …" | 1-02 thêm "(T7) (Bài 04): mẫu $V$ độc lập với $S$." ($51\to$ khoảng $59$; nếu làm cùng N2 thì gộp hai dòng (T…) để giữ trần). 2-03 giữ nguyên. |
| nhẹ | 3-03 (N4) | "$<2$" trên mặt trang không có mốc so sánh. Số $2$ là độ bối rối của mô hình đều, nhưng mặt trang không nói. | 3-03: "độ bối rối $0{,}168^{-1/3}\approx1{,}8123<2$"; Ví dụ 09.3, Bước 4: "nhỏ hơn $2$ của mô hình đều" | "…$\approx1{,}8123$, nhỏ hơn $2$ của mô hình đều." 3-03 đang ở khoảng $58$, nên cắt bù $2$ âm tiết ở dòng 1. |
| nhẹ | 4-05 (N5) | "Khoảng cách tổng quát hóa" (Định nghĩa 01.10) trên mặt trang không được nhắc lại. | 4-05: "Khoảng cách tổng quát hóa $0{,}6956-0{,}6109=0{,}0847$." | Viết bằng công thức, không thêm chữ: "Khoảng cách tổng quát hóa $L_D(0{,}7)-L_s(0{,}7)=0{,}0847$." |
| nhẹ | 4-08 (N6) | Nhãn "(c)" xuất hiện hai lần trên mặt trang, như hai câu khác nhau. | 4-08 dòng 2: "…; (c) $p_\theta=(\tfrac12,\tfrac12,0)$."; dòng 3: "(c) MLE tổng thể làm nhỏ nhất chiều nào; …" | Dòng 3 mở bằng "Ở (c): MLE tổng thể …". |
| nhẹ | 3-07 (N7) | Trang tiếp nối Ví dụ 09.4 nhưng mặt trang không ghi số hiệu. Người đọc chỉ thấy "Ví dụ 09.4." ở 3-06. | tiêu đề 3-07: "Ví dụ: bán kính theo kí tự và phép đếm sai"; ghi chú diễn giả 7-03: "dùng cách của Ví dụ 09.4" | Dòng 2: "Ví dụ 09.4, theo kí tự: chia cho $n=200$ …" ($52\to55$). |
| nhẹ | 3-09 (N8) | Mạch 3 kết thúc bằng hai số mà không có câu kết luận trên mặt trang. Lý do hai điểm cực tiểu khác nhau, và yêu cầu ghi rõ mục tiêu, chỉ ở ghi chú diễn giả. | 3-09: "Điểm cực tiểu: $\tfrac16$ (tổng), $\tfrac12$ (chuẩn hóa)."; ghi chú dòng 368: "ta cần ghi rõ mục tiêu nào được tối thiểu hóa, vì hai mục tiêu có điểm cực tiểu khác nhau" | Nếu trần cho phép (3-09 khoảng $49$): "Điểm cực tiểu $\tfrac16$ (tổng), $\tfrac12$ (chuẩn hóa): ghi rõ mục tiêu khi độ dài khác nhau." |
| nhẹ | 7-00 (N9) | Dòng dẫn mạch Tổng kết gần trùng luận điểm bìa và ý của dòng dẫn 2-00. Mạch 5–6 không có trong dòng dẫn. | 1-01: "Với hàm lỗi log, ước lượng hợp lý cực đại là tối thiểu hóa rủi ro thực nghiệm, và khi các chuỗi được rút độc lập, cỡ mẫu là số chuỗi."; 7-00: "Học một phân bố là tối thiểu hóa rủi ro thực nghiệm với hàm lỗi log; với chuỗi, cỡ mẫu là số chuỗi độc lập." | Ví dụ (≤ 25): "Bốn kết quả của bài: phân tích tự hồi quy, rủi ro bằng entropy cộng KL, cận dưới bằng chứng, gradient theo đường đi." |
| nhẹ | 7-06 (N10) | Dòng bài sau là chữ thường, không liên kết. Deck 03–05 liên kết tới deck sau. Tệp `lecture-10-gradient-chinh-sach-hoc-lien-tuc.html` đã có trong repo, chưa qua duyệt. | 7-06: "Bài 10: Gradient chính sách và học liên tục."; `L05` trang cuối: `<a href="lecture-06-on-dinh-chinh-quy-hoa.html">Bài 06</a>` | Khi deck 10 qua duyệt, đổi thành `<a href="lecture-10-gradient-chinh-sach-hoc-lien-tuc.html">Bài 10</a>: …`. Tên bài đã khớp `<title>` của deck 10. |
| nhẹ | `storyboard.md` (N11) | Vài mục còn mô tả bản trước. §3 còn dòng dẫn mạch 6 cũ. §9 ghi 7-01 "năm hàng", 7-02 "năm câu trả lời", trong khi deck có bốn. Chỉ §16 ghi bản cuối. | `storyboard.md` §3 hàng 6: "Viết lần rút thành hàm của một nhiễu cố định đưa đạo hàm vào trong kì vọng, …"; §9: "năm hàng", "năm câu trả lời"; deck 6-00, 7-01, 7-02 | Sau vòng sửa, cập nhật §3, §9 theo deck, hoặc ghi ở đầu §3, §6, §9 rằng §16 thay thế. |

Không có phát hiện `chặn bàn giao` hay `nghiêm trọng`. Các mục đạt:
- trang "Vấn đề trung tâm" mở đầu (1-05) có đúng một hộp, câu hỏi của ghi chú, câu trả lời ở ghi chú diễn giả;
- số mạch (bảy), tiêu đề mạch, trang "Nội dung" và bảng `Mục | Bài tập` khớp nhau; `#/2`…`#/7` mở đúng trang tiêu đề mạch;
- mỗi mạch ứng với các mục liên tiếp của ghi chú; hai lệch thứ tự trong mạch đã chốt ở storyboard §11;
- mỗi số hiệu Ví dụ, Bài tập, kết quả dẫn trên mặt trang đều có trên trang nguồn trước đó (Ví dụ 09.1–09.13, Bài tập 09.1, 09.3, 09.4, 09.6, 09.7, 09.8; Định nghĩa, Mệnh đề, Định lý, Hệ quả 09.1–09.15); không mặt trang nào dẫn kết quả của trang sau hay bài sau;
- bảng `Mục | Bài tập` có đủ mười bài của `exercises.md`, xếp theo mạch cung cấp kiến thức cuối cùng (09.1(d) cần kí tự kết thúc ở 3-09; 09.4(d) cần Mệnh đề 09.15; 09.10 cần bước M; 09.5(c), 09.6(a)(ii), 09.9(c) cần mạch 4); liên kết viewer có `&deck=` đúng;
- mạch Tổng kết đủ thành phần, đúng thứ tự, không thêm khái niệm mới; bài tổng hợp 09.6(b) có "Lời giải:" trên mặt trang; bốn câu tự kiểm tra trả lời được từ ghi chú;
- câu hỏi trên mặt trang (1-06, 4-05) được trả lời trên mặt trang (2-01, 3-07; dòng cuối 4-05);
- tên kỹ thuật và cách nhắc lại khớp deck 02, 05; câu hỏi cuối deck 08 được nhận, câu hỏi cho Bài 10 được trao.

## 4. Đề xuất sửa ghi chú (cho điều phối viên và tác giả)

1. **Tên của (T7).** Bài 04 gọi (T7) là "mẫu xác thực độc lập", còn §2 Bài 09 gọi cùng nhãn là "tập kiểm tra độc lập". Kí hiệu $V$, $m_v$ giữ nguyên. Đề xuất: §2 Bài 09 ghi "(T7) của Bài 04, áp dụng cho tập kiểm tra", để người đọc nhận ra cùng một giả thiết.
2. Không thấy lỗi thứ tự hay tham chiếu tới khối sau trong các mục mà deck dùng. Các đề xuất đã có trong `review-log.md` (Ví dụ 09.8, Bước 4, "khoảng $0{,}032$"; Hệ quả 05.15 trong tiên quyết; $\rho_0$ ở Bài tập 09.4) không nêu lại.

## 5. Kết luận

**đạt khi sửa**: 0 chặn bàn giao, 0 nghiêm trọng, 5 trung bình (M1–M5), 11 nhẹ (N1–N11).
