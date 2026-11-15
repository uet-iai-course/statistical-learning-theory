# Duyệt deck Bài 10 — Vai 5 `mach-truyen` (mạch truyện, liên kết, thống nhất thứ tự với ghi chú)

Ngày 2026-11-16. Chỉ đọc. Deck đóng băng: `2627-1/lecture-10-gradient-chinh-sach-hoc-lien-tuc.html` (54 trang, 7 mạch). Đối chiếu: `materials/lec-10/lecture-note.md`, `exercises.md`, `planning/lec-10/storyboard.md` (mục 3, 6, 9, 12, 16), `review-log.md` mục "Bộ trang chiếu", decks Bài 01–09.

**Kiểm đã chạy.**

- `deck_lint.py`: 1 phát hiện (7-03, 63 > 60, đã được chấp nhận làm ngoại lệ).
- Playwright (thư mục nháp `rv-mach-truyen/links.py`):
  - cấu trúc 7 chồng dọc (6, 6, 12, 9, 5, 9, 7 trang);
  - `#/2`…`#/7` mở đúng `L10-2-00`…`L10-7-00`, bấm liên kết thứ ba của trang Nội dung tới `L10-4-00`;
  - hai liên kết viewer ở 7-05 trả 200, viewer bài tập có liên kết "Bộ trang chiếu" về đúng deck, 0 `.katex-error`, 0 lỗi console.
- `deck_check.py --shots` cho 1-04, 7-02, 7-05, 7-06; đã xem ảnh 1600×900 của 7-02, 7-06.
- Script kiểm số hiệu: mọi "Ví dụ/Bài tập/Định lý/… 10.k" dẫn trên mặt trang đều có trang nguồn ghi số đó, đứng trước. Riêng "Nhận xét 10.5" (3-05) được phát biểu ngay trên trang đó nhưng không in đậm như nhãn khối. Không có dẫn tới trang sau.
- So tiêu đề storyboard mục 6 với deck: ba chỗ lệch (4-04, 4-05, 6-04), đều đã ghi ở mục 16.

## 1. Bảng đối chiếu mạch → mục ghi chú

| Mạch | Tên | Mục ghi chú | Thứ tự khối trên deck | Khớp thứ tự ghi chú |
|---|---|---|---|---|
| 1 | Mở đầu | đoạn mở, Mục tiêu, Tiên quyết, Câu hỏi mở đầu | bìa, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, câu hỏi mở đầu | có (khuôn deck đặt câu hỏi mở đầu cuối mạch 1, như Bài 01–09) |
| 2 | Quá trình quyết định Markov và mục tiêu của chính sách | §1, §3, §4 (giả thiết §2 phân về nơi dùng) | §1 bảng; Ví dụ 10.1; Định nghĩa 10.1; Định nghĩa 10.2; Ví dụ 10.2 | có (§3 trước §4 như ghi chú) |
| 3 | Gradient chính sách và thuật toán REINFORCE | §5 | Bổ đề 10.3; Ví dụ 10.3; Định lý 10.4; (ý tưởng); Nhận xét 10.5; Ví dụ 10.4, 10.5, 10.6; Thuật toán 10.6; Ví dụ 10.7; Bài tập 10.1 | có |
| 4 | Giá trị nền và phương sai của ước lượng gradient | §6 | Mệnh đề 10.7; Hệ quả 10.8; (ý tưởng); Ví dụ 10.8, 10.9; 10.10; (Nhận xét 10.9 ở ghi chú diễn giả); 10.11; 10.12; Bài tập 10.2 | có |
| 5 | Giao thức học liên tục và ma trận đánh giá | §7 | Định nghĩa 10.10; 10.11; Ví dụ 10.13; Bài tập 10.4 | có |
| 6 | Hai nhiệm vụ xung đột và hối tiếc | §7 câu cuối, §8, §9 | xung đột; Định nghĩa 10.12; Mệnh đề 10.13; (ý tưởng); Ví dụ 10.14 (Nhận xét 10.14, Ví dụ 10.15 ở ghi chú diễn giả); Ví dụ 10.16; Định nghĩa 10.15; Nhận xét 10.16; Ví dụ 10.17 (Nhận xét 10.17 ở ghi chú diễn giả); Bài tập 10.5 | có (Bài tập 10.5(c) thuộc §8 đứng sau §9, xem phát hiện 11) |
| 7 | Tổng kết | §10–§13, Phụ lục D | bảng; vấn đề trung tâm; bài tập tổng hợp; tự kiểm tra; bài tập về nhà; tài liệu | có |

Trang Nội dung: sáu mục đánh số 2–7, tên trùng tiêu đề sáu mạch, liên kết `#/2`…`#/7` đúng.

## 2. Bảng chức năng từng trang (kèm trang → mục ghi chú)

| Trang | Mục ghi chú | Vai trò trong mạch | Kết nối vào | Kết nối ra |
|---|---|---|---|---|
| 1-01 | đoạn mở, §10 | bìa, luận điểm một câu có điều kiện | deck 09 (câu nối "Bài 10 hỏi …") | 1-05, toàn bài |
| 1-02 | Tiên quyết, câu ôn nhanh | nhắc lại (T1), Hệ quả 02.10(b), (C), Định lý 05.14, Bài 09, đạo hàm sigmoid | Bài 01–09 | 2-01 ((T1)), 2-02 ($s'$), 3-09 ((C)), 4-07 (02.10), 7-03 ((T3)) |
| 1-03 | Mục tiêu học tập | năm mục tiêu, đủ năm mục tiêu của ghi chú | — | mạch 2–6 |
| 1-04 | các mục, §13 | danh sách mạch, đọc trước | — | 2-00…7-00 |
| 1-05 | đoạn mở | một hộp "Câu hỏi:", câu hỏi thật, không gợi lời giải | câu nối cuối deck 09 (cùng ý) | 7-02 |
| 1-06 | Câu hỏi mở đầu | hai tình huống; "Câu hỏi:" khác $S\sim D^m$ ở đâu | 1-05 | 2-01, 2-05 (dòng cuối), 5-01, 6-02(b) |
| 2-00 | §1–§4 | dòng dẫn: phân bố dữ liệu đổi theo xác suất đang học | 1-06 | 2-01 |
| 2-01 | §1 | thiết lập hai bài toán; "(T1) không đúng" trả lời một nửa câu hỏi 1-06 | 1-06 | 2-03 (Phần A), 5-01 (Phần B) |
| 2-02 | §3, Ví dụ 10.1 | ví dụ xuyên suốt; $J'=\tfrac38$ bằng dạng đóng; "Lưu ý:" vì sao tính được | 1-02 | 3-06, 4-04 |
| 2-03 | §2, §4, Định nghĩa 10.1 | (MDP), (Π), chính sách bảng | 2-01, 2-02 | 2-04, 3-03, 3-04 |
| 2-04 | §4, Định nghĩa 10.2 | $\tau$, $p_\theta$, $R$, $J$; "Lưu ý:" đối chiếu Bài 01 | 2-03 | 2-05, 3-01 |
| 2-05 | §4, Ví dụ 10.2 | tám quỹ đạo, $J(0)=1{,}75$; phân bố $S_1$ phụ thuộc $\theta_{s_0}$ | 2-04, 1-06 | 3-07, 3-08, 4-05, 4-07; câu "tác tử không biết $\mu_0$, $P$, $r$" chỉ ở ghi chú diễn giả (phát hiện 2) |
| 3-00 | §5 | dòng dẫn nêu điều kiện và kết quả của mạch | ghi chú diễn giả (đạo hàm của trung bình đã thu bằng $0$) | 3-01 |
| 3-01 | §5, Bổ đề 10.3 | công cụ; chứng minh hai dòng | 2-04 | 3-02, 3-04 bước 2, 3-06 dòng 5 |
| 3-02 | §5, Ví dụ 10.3 | phản ví dụ khi bỏ giả thiết tập giá trị | 3-01 | 3-05 dòng cuối |
| 3-03 | §5, Định lý 10.4 | trực quan, phát biểu, "không cần $\mu_0$, $P$, $r$" | 3-01, 2-05 | 3-04, 3-06, 3-07, 3-09 |
| 3-04 | §5, chứng minh | ba bước, chỗ (MDP) vào, bỏ giả thiết hỏng ở bước 3 | 3-03 | 3-08 ("bước 3 của chứng minh") |
| 3-05 | §5, Nhận xét 10.5, Phụ lục A | "Kỹ thuật." của Phần A; nhắc kỹ thuật Bài 09 | 3-02, 3-03, deck 09 (6-04) | 4-03 |
| 3-06 | §5, Ví dụ 10.4 | kiểm định lý trên bandit; "Diễn giải:" $\pm0{,}75$ | 2-02, 3-03 | 3-11, 4-01 (câu nối mạch 3 → 4) |
| 3-07 | §5, Ví dụ 10.5 | kiểm định lý trên MDP hai bước | 2-05, 3-03 | 4-05 |
| 3-08 | §5, Ví dụ 10.6 | phản ví dụ bỏ (MDP) | 3-04 bước 3 | 7-01 (giả thiết không được bỏ) |
| 3-09 | §5, Thuật toán 10.6 và đoạn sau | thuật toán; không chệch có điều kiện; thiếu (C) | 3-03, 1-02 | 3-10 |
| 3-10 | §5, Ví dụ 10.7 | điểm dừng là cực tiểu; nhắc Mệnh đề 08.12 | 3-09 | 7-02 dòng 1 |
| 3-11 | Bài tập 10.1(a), (b) | luyện Định lý 10.4; phương sai $\tfrac{27}{16}$ | 3-06 | 4-01 |
| 4-00 | §6 | dòng dẫn: giá trị nền giữ kì vọng, đổi phương sai | 3-06 | 4-01 |
| 4-01 | §6, Mệnh đề 10.7 | câu nối $\pm0{,}75$; $R_{\ge t}$, $\mathcal F_t$; trực quan; phát biểu | 3-06 | 4-02, 4-03 |
| 4-02 | §6, Hệ quả 10.8 | giá trị nền; trực quan; phát biểu | 4-01 | 4-03, 4-04 |
| 4-03 | §6, Phụ lục B | ý tưởng chứng minh chung; nhắc kỹ thuật Bài 05 | 4-01, 4-02, deck 05 | 4-04 (Ví dụ 10.9), 4-08 |
| 4-04 | §6, Ví dụ 10.8, 10.9 | phương sai theo $b$ (F1); giá trị nền gây chệch | 3-06, 4-02 | 4-05 ($b^*$), 7-04 câu 2 |
| 4-05 | §6, Ví dụ 10.10 | ba ước lượng cùng kì vọng; phương sai giảm hay tăng | 2-05, 3-07, 4-01, 4-02 | 4-08 ($\tfrac9{16}$) |
| 4-06 | §2 (PT), §3 ứng dụng, §6, Phụ lục C | dịch phần thưởng; phương sai; mô phỏng | 4-02, 3-09 | — |
| 4-07 | §6, Ví dụ 10.12 | cận với xác suất cao duy nhất của Phần A | 1-02, 2-05; chưa có câu nối trên mặt trang (phát hiện 3) | 7-02 dòng 4, 7-03 |
| 4-08 | Bài tập 10.2(b), (c) | luyện Hệ quả 10.8 | 4-03, 4-05 | — |
| 5-00 | §7 | dòng dẫn: thành phần của bài toán học liên tục | (chuyển sang Phần B) | 5-01 |
| 5-01 | §7, Định nghĩa 10.10 | giao thức | 1-06, 2-01 dòng 4 | 5-02 |
| 5-02 | §7, Định nghĩa 10.11 | ma trận đánh giá, bốn độ đo | 5-01 | 5-03 |
| 5-03 | §7, Ví dụ 10.13 | tính độ đo; độ quên âm khi đổi quy ước | 5-02 | 5-04, 6-01 |
| 5-04 | Bài tập 10.4(a), (d) | luyện; trung bình cuối cùng không đủ | 5-03 | 6-01 |
| 6-00 | §8–§9 | dòng dẫn: xung đột buộc thỏa hiệp | 1-06 | 6-01 |
| 6-01 | §7 câu cuối, §8, Định nghĩa 10.12 | câu nối từ ma trận đánh giá; xung đột; hai phương pháp | 5-03, 5-04 | 6-02 |
| 6-02 | §8, Mệnh đề 10.13 | trực quan, phát biểu | 6-01, 1-06 | 6-03, 6-04, 6-05 |
| 6-03 | §8, chứng minh | bốn bước; "Kỹ thuật." một dòng | 6-02 | 6-08 |
| 6-04 | §8, Ví dụ 10.14 | năm $\lambda$ (F2); đánh đổi bền vững–mềm dẻo | 6-02 | 6-05 |
| 6-05 | §8, Ví dụ 10.16, Phụ lục C | bộ đệm hữu hạn so với rủi ro cũ đầy đủ | 6-02(d) | 6-06 |
| 6-06 | §9, Định nghĩa 10.15, Nhận xét 10.16 | "Câu hỏi:" hối tiếc nhỏ và độ quên | 1-02, 5-02 | 6-07 |
| 6-07 | §9, Ví dụ 10.17 | "Kết luận:" trả lời câu hỏi của 6-06 | 6-06 | 7-02 dòng 5, 7-04 câu 4 |
| 6-08 | Bài tập 10.5(c) | luyện Mệnh đề 10.13 với độ cong $4$ | 6-03 | — |
| 7-00 | §10 | dòng dẫn tổng kết | toàn bài | 7-01 |
| 7-01 | §10 | bảng bốn hàng | 3-03, 4-01, 4-02, 6-02, 6-06 | 7-02 |
| 7-02 | §10, Phụ lục D | trả lời vấn đề trung tâm | 1-05 | — |
| 7-03 | Bài tập 10.7(i) | bài tập tổng hợp có lời giải | 4-07, 1-02 | 7-06 dòng khép |
| 7-04 | §12 (a), (b), (d), (e) | bốn câu tự kiểm tra | 2-02, 4-04, 6-02, 6-07 | — |
| 7-05 | §11 | bảng `Mục \| Bài tập`, liên kết viewer | — | ghi chú, `exercises.md` |
| 7-06 | §12 (f), §13, Phụ lục D | tài liệu; dòng khép học phần | 1-04 | (khép học phần) |

## 3. Kiểm theo bảng kiểm của Vai 5

- **Câu hỏi trung tâm của từng mạch** xuất hiện trên mặt trang trước nửa sau của mạch: đạt.
  - Dòng dẫn của sáu mạch nội dung nêu ý cốt lõi. Các dòng dẫn không lặp khuôn, trừ 7-00 trùng mở đầu với 3-00 (phát hiện 10).
  - Mạch 6 có thêm "Câu hỏi:" ở 6-06 cho nhánh hối tiếc.
- **Câu nối giữa các mạch trên mặt trang.**
  - 3 → 4: 3-06 "Diễn giải:" và 4-01 dòng 1 ($\pm0{,}75$ so với $\tfrac38$). Đạt.
  - 5 → 6: 6-01 dòng 1. Đạt.
  - 3-09 → 3-10: "thiếu (C)". Đạt.
  - 2 → 3: thiếu câu "tác tử không biết $\mu_0$, $P$, $r$" (phát hiện 2).
  - Trong mạch 4, chuyển từ đồng nhất thức sang cận với xác suất cao (4-07) chưa có câu nối (phát hiện 3).
  - 4 → 5: chuyển phần, có câu nối về câu hỏi mở đầu ở 5-01. Đạt.
- **Xem trước bài sau:** không có. Bài cuối; trang 7-06 không có liên kết bài sau, có dòng khép học phần (phát hiện 4).
- **Trùng lặp:** chỉ có các câu nhắc lại có chủ đích (2-02/3-06; 3-06/4-01; 1-06/6-02(b)). Không có trang thừa.
- **Trang "Vấn đề trung tâm".**
  - Mở đầu (1-05): một hộp, đạt.
  - Cuối (7-02): trả lời phần tương tác với môi trường, nhưng bỏ kết quả chính của Phần B (phát hiện 1).
- **Mạch "Tổng kết":** không có khái niệm mới, trừ tên "ước lượng mật độ" ở 7-06. Tên này chưa xuất hiện trên mặt trang của deck nào (phát hiện 4).
- **Bảng `Mục | Bài tập` (7-05):** khớp `exercises.md` §11 của ghi chú. Mỗi bài nằm ở mạch cung cấp kiến thức cuối cùng nó cần:
  - 10.1(c), (d) cần Hệ quả 10.8, nên ở mạch 4;
  - 10.3 cần Thuật toán 10.6 và Ví dụ 10.7, nên ở mạch 3;
  - 10.6 cần Định nghĩa 10.12 và thí nghiệm Phụ lục C (6-05), nên ở mạch 6;
  - 10.7 cần câu (f) §12, nên ở mạch 7.

  Các trang bài tập lấy đúng phần: 10.1(a), (b); 10.2(b), (c); 10.4(a), (d); 10.5(c); 10.7(i).
- **Liên kết viewer:** đúng, có `&deck=`.
- **Liên tục với Bài 01–09.**
  - "Đổi chỗ đạo hàm và kì vọng": tên trùng tiêu đề L09-6-04, nhắc lại một dòng ở 3-05, có ở 1-02.
  - "Kì vọng có điều kiện theo lịch sử" (L05-3-07): nhắc lại ở 4-03, kèm "tính chất tháp".
  - Mệnh đề 08.12: nhắc lại ở 3-10 với "theo kì vọng", khớp L08-6-04 ("tính dừng, theo kì vọng").
  - Câu nối cuối deck 09 ("Bài 10 hỏi điều gì thay đổi khi hành động của một tác tử quyết định quan sát tiếp theo, và khi phân bố dữ liệu thay đổi theo thời gian"): cùng ý với hộp 1-05.
  - Trang cuối deck 09 ghi "Bài 10: Gradient chính sách và học liên tục", trùng tiêu đề bìa 1-01.
  - Lệch nhỏ: tên kỹ thuật Bài 02 ở 4-07 (phát hiện 9).
- **Luồng khái niệm (outline, threads, concepts).** Mọi câu hỏi mở trên mặt trang đều được đóng:
  - 1-06 đóng ở 2-01 và 2-05;
  - "Lưu ý:" 2-02 đóng ở 3-03;
  - "thiếu (C)" ở 3-09 đóng ở 3-10;
  - "Câu hỏi:" 6-06 đóng ở 6-07;
  - 1-05 đóng ở 7-02, nhưng chỉ một phần (phát hiện 1).

  Riêng mô phỏng $49/100$ (4-06) không có đối chứng trên mặt trang (phát hiện 6). Thuật ngữ dùng nhất quán trong deck.

## 4. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L10-7-02 | Trang trả lời vấn đề trung tâm bỏ kết quả chính của Phần B: hai nhiệm vụ xung đột buộc một đánh đổi (Mệnh đề 10.13). Trang cũng bỏ "ma trận đánh giá". Câu hỏi 1-05 hỏi cả "khi nhiệm vụ thay đổi theo thời gian", nhưng phần học liên tục chỉ còn "cần giao thức nêu trước; hối tiếc tĩnh không chặn độ quên". Bìa và dòng dẫn 6-00 đều nêu ý xung đột. | Mặt 7-02 dòng 5: "Nhiệm vụ thay đổi cần giao thức nêu trước; hối tiếc tĩnh không chặn độ quên." Ghi chú §10 đoạn 1: "Khi nhiệm vụ thay đổi, bài toán chỉ xác định khi có giao thức và ma trận đánh giá (Định nghĩa 10.10, 10.11), và hai nhiệm vụ xung đột buộc $L_A+L_B\ge\tfrac14$ trong ví dụ bậc hai (Mệnh đề 10.13)." Bìa 1-01: "… cần nêu trước giao thức và ma trận đánh giá". | Sáu dòng, giữ nguyên điều kiện N1 ở dòng 3; đếm theo cách của `deck_lint.py` được 60 âm tiết, bằng trần (hiện tại 59). (1) "(T1), (C) không đúng: dữ liệu phụ thuộc $\theta$, $-J$ không lồi."; (2) "(MDP), (Π): ước lượng một lượt không chệch."; (3) giữ nguyên; (4) "Xác suất $\ge1-\delta$: chỉ cho chính sách cố định."; (5) "Nhiệm vụ đổi: cần giao thức, ma trận đánh giá."; (6) "Xung đột buộc đánh đổi; hối tiếc tĩnh không chặn độ quên." Dòng (1) đổi "sai" thành "không đúng" như 2-01 và ghi chú §1. |
| trung bình | L10-2-05 (hoặc L10-2-02), câu nối mạch 2 → 3 | Mặt trang không có câu nêu cái còn thiếu sau mạch 2: tác tử biết $\pi_\theta$ nhưng không biết $\mu_0$, $P$, $r$, nên không tính được $J$ hay $\nabla J$ bằng công thức. Câu này chỉ có ở ghi chú diễn giả 2-00, 2-05, 3-00. Vì vậy 3-03 "không cần $\mu_0$, $P$, $r$" trả lời một khó khăn chưa được nêu trên mặt trang. "Lưu ý:" 2-02 chỉ nói $J'$ tính được nhờ dạng đóng. | Ghi chú cuối §4: "Tác tử biết $\pi_\theta$ nhưng không biết $\mu_0$, $P$, $r$, nên không tính được $J$ hay đạo hàm của nó bằng công thức." Mặt 2-02: "**Lưu ý:** $J'$ tính được vì $J$ có dạng đóng chứa $r(0)$, $r(1)$." Mặt 2-05 (44 âm tiết, còn chỗ) không có câu này. | Thêm vào 2-05 một dòng: "Tác tử biết $\pi_\theta$, không biết $\mu_0$, $P$, $r$: không tính được $J$, $\nabla J$ bằng công thức." Tùy chọn: nối vào "Lưu ý:" 2-02 vế "; tác tử không biết $r$." |
| trung bình | L10-4-07 | Mạch 4 chuyển từ các đồng nhất thức (4-01–4-06) sang một cận với xác suất cao mà mặt trang không có câu nối. Trang mở ngay bằng dữ kiện. Lý do Ví dụ 10.12 đứng ở đây (chính sách cố định thì các lượt thỏa (T1)) chỉ có ở ghi chú diễn giả ("Các kết quả trước là đồng nhất thức."). | Ghi chú §6, ngay trước Ví dụ 10.12: "Các kết quả trên là đồng nhất thức. Khi chính sách cố định, các lượt thỏa (T1), và bất đẳng thức Hoeffding cho một cận với xác suất cao." Mặt 4-07 dòng 1: "**Ví dụ 10.12.** Ví dụ 10.2, $\theta$ cố định trước khi chạy: $m=1000$ lượt thỏa (T1); …" | Mở trang bằng một dòng nối, ví dụ "Các kết quả trước là đồng nhất thức; với $\theta$ cố định, các lượt thỏa (T1) và có cận với xác suất cao." Gọn dòng cuối để giữ ≤ 60 âm tiết (57 hiện tại): "$\theta$ do Thuật toán 10.6 chọn từ chính các lượt: cận không áp dụng." |
| trung bình | L10-7-06 | Dòng khép học phần "Bốn bài toán: phân lớp có giám sát, ước lượng mật độ, tối ưu chính sách, học liên tục." có ba điểm yếu. (i) Thiếu "của học phần" (storyboard mục 9 dự kiến "Bốn bài toán của học phần: …"), nên người đọc không biết danh sách nói về điều gì. (ii) Không gắn với các bài. (iii) "ước lượng mật độ" chưa xuất hiện trên mặt trang của deck nào (0 lần trong decks 01–09) và cả ghi chú Bài 09. Deck 09 gọi bài toán đó là "học một phân bố xác suất". Đây là trang khép cả học phần. | Mặt 7-06 dòng cuối. Storyboard mục 9: "Bốn bài toán của học phần: phân lớp, …". Ghi chú §12 (f), Phụ lục D: "*Phân lớp có giám sát (Bài 01–08).* … *Ước lượng mật độ (Bài 09).* … *Tối ưu chính sách (Phần A).* … *Học liên tục (Phần B).*" Hộp 1-05 deck 09: "học một phân bố xác suất và học một chuỗi như thế nào?" | "Bốn bài toán của học phần: phân lớp có giám sát (Bài 01–08), ước lượng mật độ (Bài 09), tối ưu chính sách và học liên tục (Bài 10)." Để giữ ≤ 60 âm tiết (59 hiện tại), bỏ tên bài báo in nghiêng của Kirkpatrick và cộng sự trên mặt trang và giữ tên đó ở ghi chú diễn giả. |
| nhẹ | L10-4-05 | Dòng cuối "Đổi ví dụ (…): phương sai của (i) là $0$, của (ii) là $1$." không nói kết luận: bỏ phần thưởng trước bước $t$ có thể làm phương sai tăng. Đây là ý mà dòng dẫn mạch 4 ("đổi phương sai") cần, và hiện chỉ có ở ghi chú diễn giả. | Ghi chú Ví dụ 10.10: "Tóm lại, với cùng một kì vọng, phương sai có thể giảm (Bước 2) hoặc tăng (Bước 3) tùy bài toán." | "… phương sai của (i) là $0$, của (ii) là $1$: (ii) làm phương sai tăng." |
| nhẹ | L10-4-06 | Kết quả mô phỏng $49/100$ (không giá trị nền) không có đối chứng trên mặt trang. Đối chứng (có giá trị nền hoặc $c=0$: $0/100$) chỉ ở ghi chú diễn giả, nên số $49/100$ đứng một mình. | Ghi chú Ví dụ 10.11, Bước 4: "có giá trị nền, hay với $c=0$, không lần nào." | Nối vào dòng mô phỏng "; có giá trị nền: $0/100$" và gọn chỗ khác để giữ ≤ 60 (58 hiện tại). |
| nhẹ | L10-3-09 | Câu nối từ Định lý 10.4 sang thuật toán chỉ có ở ghi chú diễn giả. Mặt trang viết $\hat g_j$ mà không dẫn định lý. | Ghi chú §5: "Dùng ước lượng của Định lý 10.4 với tham số mới sau mỗi lượt, ta được thuật toán dưới đây." | Thêm "(Định lý 10.4)" sau công thức $\hat g_j$ ở dòng 2. |
| nhẹ | L10-3-09 → L10-4-03 | Kì vọng có điều kiện theo lịch sử dùng trên mặt 3-09 ($\mathbb E[\hat g_j\mid\tau_1,\ldots,\tau_{j-1}]$), nhưng dòng "Nhắc lại:" kỹ thuật Bài 05 đến 4-03 mới có. 3-09 chỉ dẫn "điều kiện không chệch của Bài 05". | Mặt 3-09 dòng 3–4; mặt 4-03 dòng 1 "**Nhắc lại:** kì vọng có điều kiện theo lịch sử, tính chất tháp (Bài 05)." | Chấp nhận được vì 3-09 đã gọi tên điều kiện của Bài 05. Nếu sửa, thêm "(kì vọng có điều kiện theo lịch sử, Bài 05)" vào 3-09 và giữ 4-03. |
| nhẹ | L10-4-07 | Tên kỹ thuật lệch: "đảo cận đuôi thành cỡ mẫu". Tiêu đề L02-4-04 là "Đảo cận đuôi thành bán kính và cỡ mẫu", và decks 04, 09 nhắc lại đúng tên đầy đủ. | Mặt 4-07: "**Nhắc lại:** đảo cận đuôi thành cỡ mẫu (Bài 02)". Deck 09: "**Nhắc lại:** đảo cận đuôi thành bán kính và cỡ mẫu (Bài 02)." | Dùng tên đầy đủ; tính chung với phát hiện 3 khi gọn trang. |
| nhẹ | L10-7-00 | Dòng dẫn tổng kết lặp gần nguyên dòng dẫn 3-00 ("Khi môi trường không phụ thuộc tham số, gradient …"), trái bài học deck 01 "không lặp một khuôn qua các mạch". | 3-00: "Khi môi trường không phụ thuộc tham số, gradient của mục tiêu là kì vọng …"; 7-00: "Khi môi trường không phụ thuộc tham số, gradient ước lượng được không chệch; …" | Dòng dẫn nêu cái mạch tổng kết đem lại, theo ghi chú diễn giả 7-00 và §10: "Mỗi bảo đảm của bài là đồng nhất thức, tất định hoặc với xác suất cao, kèm giả thiết không được bỏ." |
| nhẹ | L10-6-08 | Bài tập 10.5(c) thuộc §8 (Mệnh đề 10.13) nhưng đứng sau hai trang §9 (6-06, 6-07). Mạch quay lại phát lại và phạt sau khi đã kết luận về hối tiếc. | Thứ tự ghi chú: Mệnh đề 10.13 … Ví dụ 10.16 (§8), rồi §9. Storyboard mục 3 gộp §9 vào mạch 6. | Tùy chọn: chuyển 6-08 lên sau 6-05 (đổi số trang), hoặc giữ vì khuôn đặt bài tập cuối mạch. Điều phối viên quyết định. |
| nhẹ | L10-3-08 (ghi chú diễn giả) | "(câu hỏi cuối buổi (c))" dẫn một câu của ghi chú mà deck không có: 7-04 chỉ gồm (a), (b), (d), (e). | Ghi chú diễn giả 3-08; mặt 7-04. | Viết "(ghi chú, §12, câu (c))" hoặc bỏ ngoặc. |
| nhẹ | L10-1-01 (ghi chú diễn giả) | Câu nói về trạng thái của chính văn bản (quy tắc tác giả 2026-11-04): "Bài không nêu khẳng định hội tụ nào cho thuật toán REINFORCE và không có cận cho độ quên." Thuộc phạm vi Vai 4, ghi ở đây vì nó nằm ở điểm vào của mạch truyện. | Ghi chú diễn giả 1-01, câu cuối. `../CLAUDE.md` "No hedging about the text's own status". | Bỏ câu. Các giới hạn đã có ở 3-10 (điểm dừng là cực tiểu) và 6-07 (hối tiếc không chặn độ quên). |
| nhẹ | storyboard mục 9, 12 | Storyboard chưa khớp deck cuối ở bảng trang → khối, trong khi điều kiện "done" yêu cầu `storyboard.md` khớp deck (bảng trang → khối). Mục 16 có ghi các chỗ lệch. | Mục 12 ghi 2-03 "(MDP), (Π), (PT)" (deck: (PT) ở 4-06); 6-04 "tính bền vững, tính mềm dẻo" trên mặt (deck: ở ghi chú diễn giả); 2-04 thiếu $r_t$; 5-01 thiếu $w^{(0)}$. Mục 9 ghi bảng 7-01 năm hàng (deck: bốn) và dòng khép "phân lớp". | Biên tập viên cập nhật mục 12 (các hàng 2-03, 2-04, 4-06, 5-01, 6-04) và mục 9 theo deck sau sửa. |

**Số phát hiện:** chặn bàn giao 0; nghiêm trọng 0; trung bình 4; nhẹ 9.

## 5. Đề xuất sửa ghi chú

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất |
|---|---|---|---|---|
| nhẹ | ghi chú Bài 10, §12 (f) và Phụ lục D | Tên bài toán của Bài 09 là "ước lượng mật độ", nhưng ghi chú Bài 09 không dùng tên này: nó gọi bài toán là "học một phân bố xác suất", và mô hình có thể là hàm xác suất rời rạc. | `grep` "ước lượng mật độ" trong `materials/lec-09/lecture-note.md`: 0 lần. Bài 09, đoạn mở: "học một phân bố xác suất và học một chuỗi". | Nếu tác giả đồng ý: "ước lượng mật độ (học một phân bố xác suất, Bài 09)" ở lần dùng đầu trong §12 (f). Deck theo ghi chú. |

## Kết luận

**đạt khi sửa.** Thứ tự mạch và khối khớp ghi chú. Các liên kết `#/N`, liên kết viewer và bảng bài tập đúng, và deck nối liền với các deck 01–09. Cần sửa bốn phát hiện trung bình trước khi bàn giao:

- 7-02 thiếu kết quả xung đột và ma trận đánh giá;
- câu nối mạch 2 → 3 thiếu trên mặt trang;
- 4-07 thiếu câu nối;
- dòng khép học phần ở 7-06.
