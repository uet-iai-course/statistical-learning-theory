# Duyệt deck Bài 06 — Vai 5 `mach-truyen` (mạch truyện, liên kết, thống nhất thứ tự với ghi chú)

Tác tử duyệt độc lập, chỉ đọc. Ngày 2026-11-15. Bản deck đóng băng: `2627-1/lecture-06-on-dinh-chinh-quy-hoa.html` (55 trang). Đối chiếu: `materials/lec-06/lecture-note.md`, `exercises.md`, `planning/lec-06/storyboard.md` (§3, §4, §12, §16), `review-log.md` § Bộ trang chiếu, các deck `lecture-0{1..5}-*.html`. Bảng kiểm liên tục: phần Outline/Threads/Concept của `quill/references/workflows.md` (không tạo `quill.json`). `no-ai-slop` chế độ Detect chỉ dùng cho các câu nối và ghi chú diễn giả có liên quan đến mạch.

## 1. Kiểm bằng máy

| Kiểm | Kết quả |
|---|---|
| Liên kết `#/N` của 1-04 (Playwright, 1600×900) | `#/2`→L06-2-00 … `#/7`→L06-7-00; tên mạch trong danh sách trùng `h2` của sáu trang tiêu đề mạch; bấm `#/4` tới L06-4-00 |
| Liên kết viewer 7-07 | ghi chú và bài tập: HTTP 200, 0 yêu cầu lỗi, 0 `.katex-error`; viewer hiện liên kết "Bộ trang chiếu" về đúng deck |
| Console | 0 lỗi |
| `deck_lint.py` | 0 phát hiện, 55 trang |
| Số hiệu dẫn trên mặt trang (script `rv-mach-truyen/cites.py`) | mọi "Ví dụ/Bài tập/Định lý … 06.k" dẫn trên mặt trang đều có trang nguồn mang số đó ở trước; không trang nào dẫn kết quả của trang sau |
| Bài sau | 7-08: "Bài 07: Mạng nơ-ron, năng lực mô hình và tham số hóa thừa." đúng tên ghi chú Bài 07 (chưa có deck nên chưa có liên kết) |

## 2. Bảng chức năng từng trang và đối chiếu trang → mục ghi chú

| Trang | Mục / khối ghi chú | Vai trò trong mạch | Kết nối vào | Kết nối ra |
|---|---|---|---|---|
| 1-01 | đoạn mở, §10 | bìa, luận điểm một câu có điều kiện | — | hai chế độ, ổn định đều |
| 1-02 | Tiên quyết, ôn nhanh | nhắc lại Hệ quả 05.15, $\operatorname{opt}_S$, Mệnh đề 01.7, lồi mạnh, $G$ | deck 05 | 1-06, 2-05, 2-08, 3-03 |
| 1-03 | Mục tiêu | năm mục tiêu | — | mạch 2–6 |
| 1-04 | toàn bài, §13 | nội dung, `#/2`–`#/7` | — | mạch 2–7 |
| 1-05 | đoạn mở | một hộp "Câu hỏi:" | — | 7-03 trả lời |
| 1-06 | Câu hỏi mở đầu | ví dụ mở: hai chương trình cùng cận $0{,}1$ | 1-02 (Hệ quả 05.15) | 2-06, 2-11 trả lời bằng số |
| 2-00 | §1–§5 | tiêu đề mạch | 1-06 | 2-01 |
| 2-01 | §1, §2 | thiết lập, hai chế độ, (T1), (T2) | 1-06 | 2-03 (chế độ A), 2-07 (chế độ B) |
| 2-02 | §3 | Ví dụ 06.1, ứng dụng một triệu hồ sơ, câu hỏi thực hành (i) | 2-01 | 2-07 (trả lời (i)), 3-01, 6-04 |
| 2-03 | §4, Bổ đề 06.1 | trực quan + công cụ: dưới gradient không chệch cho $L_D$ | 2-01 chế độ A | 2-04, 2-05 |
| 2-04 | §4, Hệ quả 06.2 | phát biểu kết quả chính 1 | 2-03 | 2-05, 2-06 |
| 2-05 | chứng minh Hệ quả 06.2 | ý tưởng chứng minh; "vòng thứ hai: bước 1 hỏng" | 2-04 | 2-07 |
| 2-06 | Ví dụ 06.2 | kiểm bằng số: $0{,}000578$ so với $0{,}1$ | 1-06, 2-04 | 7-03 (không nối trên mặt trang, xem M4) |
| 2-07 | Nhận xét 06.3; đoạn mở §5; Ví dụ 06.3 Bước 1 | trang chuyển cụm A → B | 2-05, 2-02 | 2-08 |
| 2-08 | §5, Định nghĩa 06.4 | định nghĩa khoảng cách tổng quát hóa kì vọng | 2-07 | 2-09 |
| 2-09 | Mệnh đề 06.5 | trực quan + phát biểu kết quả chính 2 | 2-08 | 2-10, 2-11, 6-01 |
| 2-10 | chứng minh Mệnh đề 06.5 | ý tưởng chứng minh | 2-09 | 2-11 |
| 2-11 | Ví dụ 06.3; đoạn cuối §5 | kiểm bằng số; câu nối "cần một cận theo tính chất của thuật toán" | 1-06, 2-09 | mạch 3 (xem M2), mạch 4 |
| 2-12 | Bài tập 06.1(c), (d) | bài tập giữa cụm | 2-05, 2-07 | — |
| 3-00 | §6 | tiêu đề mạch | 2-11 | 3-01 |
| 3-01 | đoạn mở §6; đoạn sau Định nghĩa 06.6 | vấn đề: một quan sát dịch nghiệm ERM $0{,}6154$; nghiệm không duy nhất | 2-02 (Ví dụ 06.1) | 3-02 |
| 3-02 | Định nghĩa 06.6 | định nghĩa ERM có chính quy hóa | 3-01 | 3-03 |
| 3-03 | Bổ đề 06.7, 06.8 | công cụ: tăng trưởng bậc hai, nghiệm duy nhất | 1-02 (lồi mạnh), 3-02 | 5-02 |
| 3-04 | Ví dụ 06.4, Hình 06.1 | ví dụ: khoảng cách giảm, $L_S$ tăng | 3-01 | 4-01, 5-03, 5-05, 6-01 |
| 3-05 | Bài tập 06.10(a), (c) | bài tập cuối mạch | 3-03 | — |
| 4-00 | §7 | tiêu đề mạch | 2-11 | 4-01 |
| 4-01 | Định nghĩa 06.9 và đoạn sau | vấn đề ($304/169$) + định nghĩa ổn định đều | 3-04 | 4-02, 4-03 |
| 4-02 | đoạn trước Định lý 06.10; thuật toán ghi nhớ | trực quan đổi vai, hình F3 | 4-01 | 4-03 |
| 4-03 | Định lý 06.10 | phát biểu kết quả chính 3 | 4-01, 2-08 | 4-04, 5-01, 6-03 |
| 4-04 | chứng minh Định lý 06.10 | ý tưởng chứng minh; bước 2 hỏng khi bỏ i.i.d. | 4-03 | 4-05 |
| 4-05 | bước 2; đẳng thức sau chứng minh; Phụ lục E | trang "Kỹ thuật." mới: lập luận đổi vai | 4-04, deck 03 (mẫu bóng) | Bài tập 06.2, 06.9 |
| 4-06 | Ví dụ 06.5 | kiểm: ổn định không kéo theo rủi ro thấp | 4-03 | 6-01 (số hạng khớp) |
| 4-07 | Bài tập 06.2(b) | bài tập cuối mạch | 4-05 | — |
| 5-00 | §8 | tiêu đề mạch | 4-03 | 5-01 |
| 5-01 | Mệnh đề 06.11 | trực quan + phát biểu kết quả chính 4 | 3-04, 4-03 (xem M3) | 5-02, 6-02 |
| 5-02 | chứng minh Mệnh đề 06.11; Phụ lục B | ý tưởng chứng minh; dòng "Kỹ thuật." một phía | 3-03 | 5-03, 5-04 |
| 5-03 | Ví dụ 06.6, 06.8 | kiểm bằng số và độ chặt | 3-04, 5-02 | — |
| 5-04 | Ví dụ 06.7, 06.9 | phản ví dụ bỏ $\lambda>0$, bỏ dữ liệu bị chặn | 5-02 | 6-01, 7-02 (ghi chú diễn giả) |
| 5-05 | Bài tập 06.6(a) | bài tập; hai dãy ngược chiều | 3-04 | 6-01 (câu nối có trên mặt trang) |
| 6-00 | §9 | tiêu đề mạch | 5-05 | 6-01 |
| 6-01 | đoạn mở §9; Ví dụ 06.12 | vấn đề, trực quan đánh đổi, cực biên $\lambda$ lớn | 2-09, 5-01, 5-05 | 6-02 |
| 6-02 | Hệ quả 06.13 | phát biểu kết quả chính 5 | 6-01 | 6-03, 6-04 |
| 6-03 | chứng minh Hệ quả 06.13 | ý tưởng chứng minh; "Nhắc lại:" cân hai số hạng | 2-09, 4-03, 5-01 | 6-04 |
| 6-04 | Ví dụ 06.10, 06.11 | kiểm bằng số; so với SGD; trả lời câu hỏi thực hành (ii) | 2-02, 2-04, 2-07 | — |
| 6-05 | Nhận xét 06.14 | giới hạn: kì vọng so với xác suất cao | 6-02 | 7-03 (ghi chú diễn giả) |
| 6-06 | Bài tập 06.4(b) | bài tập cuối mạch | 6-02 | 7-05 (dẫn "phần (b)") |
| 7-00 | §10–§13 | tiêu đề mạch | — | — |
| 7-01, 7-02 | §4–§10 | bảng tổng kết (5 hàng, tách hai trang) | các trang phát biểu | — |
| 7-03 | §10 | trả lời vấn đề trung tâm | 1-05 | — |
| 7-04, 7-05 | Bài tập 06.4(c) | bài tập tổng hợp, "Lời giải:" trên mặt trang | 6-06, 5-01, 6-02 | — |
| 7-06 | Câu hỏi mở đầu, §7, §12 | tự kiểm tra (4 câu) | — | — |
| 7-07 | §11 | `Mục | Bài tập` + viewer | — | `exercises.md` |
| 7-08 | §12, §13 | tài liệu, bài sau | — | Bài 07 |

**Thứ tự so với ghi chú.** Mỗi mạch ứng với các mục liên tiếp: mạch 2 = §1–§5, 3 = §6, 4 = §7, 5 = §8, 6 = §9, 7 = §10–§13. Các chỗ đổi thứ tự bên trong một mục đều đã ghi ở storyboard và không làm một trang dùng điều chưa nêu: Ví dụ 06.3 Bước 1 lên 2-07 (trước Định nghĩa 06.4; bước này chỉ cần $L_S'$, $L_D'$); ví dụ nghiệm không duy nhất lên 3-01; Ví dụ 06.8 trước 06.7 (5-03, 5-04); Ví dụ 06.12 lên 6-01 (quyết định 11.5 của điều phối viên). Hành trình khái niệm của năm kết quả chính (vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh riêng → kiểm) giữ đúng thứ tự.

**Bảng `Mục | Bài tập` (7-07).** Đủ 11 bài của `exercises.md`, mỗi bài một lần. Xếp theo mạch cung cấp kiến thức cuối cùng: 06.1 (§4–§5) mạch 2; 06.10 (Bổ đề 06.7) mạch 3; 06.2 (Định lý 06.10, Ví dụ 06.5) mạch 4; 06.3, 06.5, 06.11 (Mệnh đề 06.11) mạch 5; 06.4 (Hệ quả 06.13, Hệ quả 04.17), 06.7 (Nhận xét 06.14), 06.8 và 06.9(b) (Hệ quả 06.13(c)) mạch 6. Bài 06.6 ở mạch 6 dù 5-05 (mạch 5) trình bày phần (a): phần (b) đọc đánh đổi khớp–ổn định trên dữ liệu, khái niệm của §9, nên đúng quy tắc. Các trang bài tập giữa mạch (2-12, 3-05, 4-07, 5-05, 6-06, 7-04/7-05) khớp đề, số liệu và lời giải của `exercises.md`.

**Liên tục với deck 01–05.** Đúng: "hạ gradient ngẫu nhiên có chiếu", "oracle", (C), (G1), (G2), $\mathcal F_{t-1}=\sigma(\xi_1,\ldots,\xi_{t-1})$ như deck 05 3-06; "Nhắc lại:" cân hai số hạng (deck 05 4-06) trên 6-03; bất đẳng thức Markov (Bổ đề 02.2) trên 6-05; Mệnh đề 04.3 gọi "cận ba thành phần" trên 2-10; tên bài 06 ở trang cuối deck 05 trùng `h1` của deck này. Thiếu: xem M5, M6, N2.

## 3. Kiểm từng mạch

| Mạch | Câu hỏi trung tâm trên mặt trang trước nửa sau | Câu nối vào / ra trên mặt trang | Nhận xét |
|---|---|---|---|
| 1 | 1-05 (một hộp), 1-06 "Câu hỏi:" | ra: 1-06 → mạch 2 | đạt; 1-06 chưa nối với câu hỏi cuối buổi Bài 05 (N2) |
| 2 | cụm A: 1-06, 2-02; cụm B: không có (M1) | A → B: 2-05 "bước 1 hỏng", 2-07 "Từ vòng thứ hai …"; ra: 2-11 "cần một cận theo tính chất của thuật toán" | cụm B thiếu câu hỏi mở cụm |
| 3 | 3-01 (một quan sát dịch nghiệm $0{,}6154$) | vào: không nói vì sao độ nhạy liên quan tới khoảng cách tổng quát hóa (M2); ra: 3-04 "Diễn giải:" | — |
| 4 | 4-01 dòng đầu, 4-02 | vào: strand-lead; ra: 4-06 "Kết luận:" | đạt |
| 5 | 5-01 "Trực quan." | vào: câu "Định lý 06.10 cần một thuật toán có hệ số ổn định nhỏ" và số $0{,}6154\to0{,}1778$ chỉ ở ghi chú diễn giả 5-00 (M3); ra: 5-05 hai dãy ngược chiều | — |
| 6 | 6-01 dòng 1–3 | vào: 6-01 dùng Mệnh đề 06.5(a) và cận $2G^2/(\lambda m)$; ra: 6-05 | đạt |
| 7 | 7-03 | — | không thêm khái niệm mới; 7-03 lặp bảng tổng kết, chưa khép ví dụ mở đầu và mạch SGD nhiều vòng (M4) |

**Các mạch chủ đề (threads).** Mở và đóng trên mặt trang: câu hỏi trung tâm (1-05 → 7-03); hai chương trình (1-06 → 2-06, 2-11); câu hỏi thực hành (2-02 → 2-07 vế (i), 6-04 vế (ii)); "cần một cận theo tính chất của thuật toán" (2-11 → 4-03); "ổn định không kéo theo rủi ro thấp" (4-06 → 6-01); ví dụ bốn quan sát (2-02 → 3-01 → 3-04 → 4-01 → 5-03 → 5-05). Mạch còn mở trên mặt trang: chương trình thứ hai (SGD nhiều vòng, khoảng cách $0{,}4750$) không có bảo đảm trong bài, ghi chú §10 nêu là giới hạn thứ tư; deck không nêu trên trang nào (M4).

**Không xem trước bài sau trên mặt trang:** đạt (chỉ dòng tên Bài 07 ở 7-08; các nhắc tới Bài 08 nằm ở ghi chú diễn giả 4-05).

## 4. Phát hiện

| Mức độ | Trang chiếu | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|
| trung bình | M1 · 2-07, 2-08 | Cụm B của mạch 2 (§5) mở mà không có câu hỏi trên mặt trang. Ghi chú §5 có câu hỏi in đậm và câu "đại lượng cần chặn là $L_D(\bar w_T)$, và đầu ra phụ thuộc chính tập huấn luyện $S$"; deck đưa cả hai vào ghi chú diễn giả 2-07. Strand-lead 2-00 chỉ nói về tính không chệch, không về phân tích rủi ro của nửa sau. | ghi chú dòng 359–361: "**Câu hỏi.** Tại sao cận của Hệ quả 05.19 không chặn $\mathbb EL_D(\bar w_T)$ khi chỉ số được rút từ tập huấn luyện?"; 2-07 ghi chú diễn giả: "Ở chế độ B, khi biết $S$, Hệ quả 05.19 chặn …" | Trên 2-08, thay dòng "Nhắc lại: $\mathbb E_SL_S(h)=L_D(h)$ khi $h$ cố định (Mệnh đề 01.7); …" (đã nhắc ở 1-02) bằng "**Câu hỏi:** tại sao cận cho $\operatorname{opt}_S$ của Bài 05 không chặn $\mathbb EL_D(\bar w_T)$ khi chỉ số rút từ $S$?" và giữ vế "đầu ra $A(S;\xi)$ được tính từ chính $S$" làm dòng trả lời; mật độ gần như không đổi (2-08 đang 58) |
| trung bình | M2 · 3-01 | Câu nối mạch 2 → 3 thiếu một khâu trên mặt trang: 2-11 kết thúc bằng "cần một cận theo tính chất của thuật toán", 3-01 mở bằng độ nhạy của nghiệm ERM, nhưng không trang nào nói tính chất được xét là độ nhạy khi thay một quan sát. Câu "Mệnh đề 06.5 cần một thuật toán có khoảng cách tổng quát hóa kì vọng nhỏ" chỉ ở ghi chú diễn giả 3-00. | 2-11 "Diễn giải: … cần một cận theo tính chất của thuật toán"; 3-01 dòng cuối "Thêm một số hạng phạt chuẩn vào $L_S$ làm nghiệm ít nhạy hơn." | Thêm một dòng đầu 3-01: "Tính chất của thuật toán xét ở đây: nghiệm đổi bao nhiêu khi thay một quan sát." (lấy từ câu mở §7 của ghi chú, không dẫn kết quả nào); bỏ phần "$\sum_ix_i^2=3{,}25$ giữ nguyên" ở dòng 2 để giữ mật độ (đang 50) |
| trung bình | M3 · 5-01 (ranh giới 4 → 5) | Câu nối "Để dùng Định lý 06.10, cần một thuật toán có hệ số ổn định nhỏ" và lời nhắc Ví dụ 06.4 ($0{,}6154\to0{,}1778$) chỉ ở ghi chú diễn giả 5-00; mạch 4 kết thúc bằng 4-06 "tính ổn định không kéo theo rủi ro thấp" rồi 4-07 bài tập, nên mặt trang không nói vì sao mạch 5 cần. | ghi chú dòng 803, 807; 5-00 ghi chú diễn giả "Định lý 06.10 cần một thuật toán có hệ số ổn định nhỏ. Trong ví dụ hồi quy ridge, khoảng cách …" | Trên 5-01, gộp dòng "Tức ERM có chính quy hóa ổn định đều …" vào cuối Bảo đảm (b) và dùng chỗ trống cho dòng đầu: "Định lý 06.10 cần hệ số ổn định nhỏ; ở Ví dụ 06.4, khoảng cách giữa hai nghiệm giảm từ $0{,}6154$ ($\lambda=0$) xuống $0{,}1778$ ($\lambda=4$)." Đếm lại mật độ (5-01 đang 57); nếu vượt trần, đặt vế thứ nhất vào "Kết luận:" của 4-06 |
| trung bình | M4 · 7-03 | Trang "Vấn đề trung tâm" cuối (a) lặp gần nguyên các công thức của 7-01, 7-02 (Hệ quả 06.2, Mệnh đề 06.5(b), Định lý 06.10, $\epsilon_{\mathrm{stab}}$, Hệ quả 06.13(c)), thành một dòng cho mỗi kết quả; (b) không khép ví dụ mở đầu trên mặt trang ($0{,}0006$ so với $0{,}2261$, đoạn 1 §10 của ghi chú; con số chỉ có ở ghi chú diễn giả); (c) bỏ giới hạn SGD nhiều vòng (§10, giới hạn thứ tư), tức chương trình thứ hai của 1-06 được giải thích nhưng không được nói là chưa có bảo đảm. Thêm: dòng đầu kết thúc bằng dấu hai chấm nhưng là một mục cùng cấp với các mục nó dẫn. | 7-03 dòng 2–4; ghi chú dòng 1165 "Trong câu hỏi mở đầu, rủi ro vượt mức kì vọng là $0{,}0006$ … và $0{,}2261$ …"; dòng 1176 "Với SGD dùng lại tập huấn luyện, khoảng cách … $0{,}4750$ … Định lý 06.10 cần một hệ số ổn định cho chính SGD" | Viết lại 7-03 thành các câu trả lời, không chép bảng: một đoạn mở "Tối ưu là học khi gradient không chệch cho $L_D$, hoặc khi khoảng cách tổng quát hóa kì vọng của bộ giải nhỏ; mọi bảo đảm theo kì vọng."; rồi danh sách: "Câu hỏi mở đầu: $0{,}0006$ với quan sát mới, $0{,}2261$ khi dùng lại bốn quan sát; phần chênh là khoảng cách $0{,}4750$."; "Hàm lỗi lồi, Lipschitz, $\lambda>0$ chọn trước: ERM có chính quy hóa ổn định đều, và với $\lambda^*$ rủi ro vượt mức kì vọng không quá $2GB/\sqrt m$."; "SGD nhiều vòng: khoảng cách không giảm khi chạy thêm; Định lý 06.10 cần hệ số ổn định của chính SGD."; "Các cận cần hàm lỗi lồi theo tham số; mạng nơ-ron cần lập luận mới." Đếm lại theo trần 60 |
| trung bình | M5 · 1-02, 1-06, 2-04 | Tính liên tục với deck 05: điểm lặp trung bình $\bar w_T$ và SGD có chiếu không được nhắc lại. $\bar w_T$ xuất hiện từ 1-02 (trong dòng "Nhắc lại:" Hệ quả 05.15) và 1-06 mà không giải nghĩa; thuật ngữ "điểm lặp trung bình (averaged iterate)" không có ở đâu trong deck (cả ghi chú diễn giả), dù là từ khóa mạch 3 của deck 05 và ghi chú Bài 06 nêu ngay ở câu hỏi mở đầu; 2-04 chỉ dẫn "Thuật toán 05.11" bằng số. | ghi chú dòng 25 "Với $\bar w_T$ là điểm lặp trung bình (averaged iterate)"; deck 05 3-04: "trả về điểm lặp trung bình (averaged iterate) $\bar w_T=\frac1T\sum_{t=1}^Tw_t\in W$"; script đếm: 0 lần "điểm lặp trung bình" trong deck 06 | Thêm vào 1-02 một dòng "**Nhắc lại:** SGD có chiếu (Thuật toán 05.11) trả về điểm lặp trung bình (averaged iterate) $\bar w_T=\frac1T\sum_{t=1}^Tw_t$." (1-02 đang 49); hoặc viết "điểm lặp trung bình $\bar w_T$" trong câu hỏi của 1-06 |
| trung bình | M6 · 2-03, 4-04, 4-05 | Kỹ thuật của bài trước dùng lại mà không nhắc tên trên mặt trang, trái quy định "later decks recall it by name with 'Nhắc lại:' in one line": (a) 2-03 "Nhắc lại:" chỉ nêu kí hiệu lịch sử, không nêu tên kỹ thuật "kì vọng có điều kiện theo lịch sử" (deck 05 3-07), dù storyboard §4 và §12 ghi dòng này; (b) 4-04 bước 4 dùng kỹ thuật "lấy điều kiện theo $S$, rồi bỏ điều kiện" của deck 04 nhưng tên chỉ ở ghi chú diễn giả ("như ở Bài 04"); (c) 4-05 "Nhắc lại: mẫu bóng (Bài 03)", trong khi trang kỹ thuật deck 03 tên "Đối xứng hóa và mẫu bóng". | 2-03 dòng 1; 4-04 ghi chú diễn giả "ta lấy điều kiện theo tập huấn luyện như ở Bài 04"; deck 04 "Kỹ thuật. Lấy điều kiện theo $S$, rồi bỏ điều kiện."; deck 03 trang "Đối xứng hóa và mẫu bóng" | (a) 2-03: "**Nhắc lại:** kì vọng có điều kiện theo lịch sử (Bài 05): khi biết $\mathcal F_{t-1}=\sigma(\xi_1,\ldots,\xi_{t-1})$, $w_t$ cố định; chế độ A: $\xi_t=Z_t$."; (b) 4-04 bước 4: "(ổn định đều; lấy điều kiện theo $(S,Z')$ rồi bỏ điều kiện, Bài 04) …"; (c) 4-05: "**Nhắc lại:** đối xứng hóa và mẫu bóng (Bài 03) thêm $m$ quan sát." |
| nhẹ | N1 · 2-06, 2-11 | Hai ví dụ của ghi chú không mang số trên mặt trang, trong khi mọi ví dụ khác của ghi chú đều có nhãn ("Ví dụ 06.1.", "Ví dụ 06.4." … "Ví dụ 06.12."); người học không đối chiếu được với Ví dụ 06.2, 06.3 của ghi chú. | 2-06 `<h2>Ví dụ: chương trình dùng quan sát mới</h2>`, danh sách không có nhãn; 2-11 tương tự; script: 0 lần "Ví dụ 06.2"/"Ví dụ 06.3" trên mặt trang | Thêm "**Ví dụ 06.2.**" đầu mục 1 của 2-06 và "**Ví dụ 06.3.**" đầu mục 1 của 2-11 |
| nhẹ | N2 · 1-06 | Ghi chú mở câu hỏi bằng "Xét lại phân bố $D$ của câu hỏi cuối buổi Bài 05"; deck 05 kết thúc (7-01, 7-03) bằng chính phân bố này ($\operatorname{opt}_S\approx0{,}0025$, sai số ước lượng $\approx0{,}9025$). 1-06 không nối với nó trên mặt trang. | ghi chú dòng 14; deck 05 L05-7-01 | Mục 1 của 1-06: "Phân bố của câu hỏi cuối buổi Bài 05: $X=1$, $Y=\pm1$ …" |
| nhẹ | N3 · 4-01 | Dòng đầu ($304/169\approx1{,}7988$) đứng trước định nghĩa nhưng sau định nghĩa không có câu nói đó là cận dưới của hệ số ổn định của ERM khi $\lambda=0$; ý nối này chỉ ở ghi chú diễn giả. | 4-01 ghi chú diễn giả "nên hệ số ổn định của ERM ở đây ít nhất $1{,}7988$" | Dòng cuối 4-01: "Mọi $s\in\mathcal Z^m$, kể cả tập có xác suất $0$; ERM ở dòng đầu có hệ số ít nhất $1{,}7988$." (4-01 đang 60: bớt chữ ở dòng đầu, ví dụ bỏ "Bốn quan sát,") |
| nhẹ | N4 · 2-04, 2-11 | "Cấp thuật toán (algorithm-level)" trên 2-04 và "cần một cận theo tính chất của thuật toán" trên 2-11 thiếu vế đối chiếu trên mặt trang: "cấp lớp (class-level)" và "hội tụ đều (uniform convergence)" chỉ ở ghi chú diễn giả; đối chiếu chỉ hiện ở 6-05. | ghi chú dòng 292, 507 | 2-11 "Diễn giải:" kết thúc bằng "…, cần một cận theo tính chất của thuật toán, không qua hội tụ đều của cả lớp." |
| nhẹ | N5 · ghi chú diễn giả 2-02, 7-01, 7-02 | Câu nói về chính văn bản hoặc bố cục trang (`no-ai-slop` Detect; quy định T9/L12 của cổng duyệt): "Câu hỏi thực hành của ghi chú có thêm vế thứ hai …"; "Bổ đề 06.1 là công cụ của Hệ quả 06.2, không có hàng riêng."; "Bổ đề 06.7, 06.8 là công cụ, không có hàng riêng". | trích nguyên văn ở cột trái | 2-02: "Câu hỏi thực hành còn vế thứ hai, cho ERM có chính quy hóa với hệ số chọn trước; vế này cần hệ số ổn định của quy tắc đó."; 7-01: "Bổ đề 06.1 là công cụ của Hệ quả 06.2."; 7-02: "Bổ đề 06.7, 06.8 là công cụ của Mệnh đề 06.11." |
| nhẹ | N6 · deck 05 7-08 (ngoài tệp đóng băng) | Dòng bài sau của deck 05 vẫn là chữ thường "Bài 06: …"; các deck 01–04 dùng `<a href="lecture-0N-…">Bài 0N</a>: …`. Storyboard §1 đã ghi việc này cho bước xuất bản. | `lecture-05-ha-gradient-ngau-nhien.html` dòng 830 | Khi xuất bản deck 06: `<p><a href="lecture-06-on-dinh-chinh-quy-hoa.html">Bài 06</a>: Học bằng hạ gradient ngẫu nhiên, chính quy hóa và tính ổn định.</p>` |
| nhẹ | N7 · storyboard §12 | Bảng trang → khối chưa khớp deck ở hai chỗ: 4-05 ghi "$\phi$" (deck dùng $\Phi$, đã ghi ở §16); 2-03 ghi "kì vọng có điều kiện theo lịch sử (nhắc lại)" nhưng mặt trang không có tên này (M6). "Done means" đòi storyboard khớp deck. | storyboard dòng tương ứng ở §12 | Cập nhật §12 sau khi người biên tập sửa M6 |

## 5. Đề xuất sửa ghi chú (cho tác giả; deck vẫn theo ghi chú)

| Mức độ | Vị trí | Vấn đề | Đề xuất |
|---|---|---|---|
| nhẹ | §6, đoạn mở (dòng 511) | §5 kết thúc bằng nhu cầu "một cách chặn khoảng cách tổng quát hóa kì vọng theo tính chất của thuật toán"; §6 mở ngay bằng độ nhạy của nghiệm ERM, còn lý do độ nhạy là tính chất cần xét chỉ đến ở câu mở §7. Cùng khoảng trống như M2 của deck. | Tùy tác giả: thêm một mệnh đề ở câu mở §6, ví dụ "Một tính chất như vậy là độ nhạy của đầu ra khi thay một quan sát." |

## 6. Kết luận

0 chặn bàn giao, 0 nghiêm trọng, 6 trung bình (M1–M6), 7 nhẹ (N1–N7). Cấu trúc mạch, thứ tự khái niệm, bảng `Mục | Bài tập`, liên kết `#/N` và liên kết viewer đạt; các phát hiện trung bình là câu nối giữa cụm/mạch còn nằm ở ghi chú diễn giả, trang "Vấn đề trung tâm" cuối lặp bảng tổng kết và chưa khép ví dụ mở đầu, và cách nhắc lại kỹ thuật, kí hiệu của bài trước.

**Kết luận: đạt khi sửa.**
