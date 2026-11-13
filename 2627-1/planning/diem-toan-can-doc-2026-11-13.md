# Bốn điểm toán học cần tác giả đọc (2026-11-13)

Nguồn: lượt kiểm tuân thủ nguyên tắc ghi chú ngày 2026-11-13 (báo cáo `lec-NN/reviews/kiem-nguyen-tac-2026-11-13.md`). Lượt kiểm đó không dẫn lại toán học; bốn điểm dưới đây được người kiểm ghi nhận khi đọc và **chưa được kiểm**, chưa sửa. Tác giả quyết định (2026-11-13) lưu lại để đọc sau. Số dòng tính theo commit `85c1722`; các thay thế thuật ngữ sau đó ("mẫu kiểm tra" → "tập kiểm tra") không làm đổi số dòng.

## 1. Bài 03 — UML §28.1 được mô tả theo hai cách

- **Vị trí:** `materials/lec-03/lecture-note.md`, §8 sau Định lý 03.19, dòng 861; §12 (Tài liệu đọc), dòng 924.
- **Trích dòng 861:** "bỏ thừa số này cần kỹ thuật xích (chaining), ngoài phạm vi của học phần (UML §28.1)."
- **Trích dòng 924:** "UML Chương 28 (§28.1: cận hội tụ đều qua độ phức tạp Rademacher; §28.2: cận dưới cho trường hợp bất khả diễn; §28.3: cận trên cho trường hợp khả diễn)."
- **Nghi vấn:** dòng 861 đặt kỹ thuật xích ở UML §28.1, dòng 924 nói §28.1 là cận Rademacher. Cần mở UML Chương 28 (trang theo `sources/uml-sections.md`) để xác định §28.1 có trình bày xích hay chỉ dùng cận Rademacher, và cận trên bỏ thừa số $\ln(1/\epsilon)$ có trong UML hay không.
- **Báo cáo gốc:** `lec-03/reviews/kiem-nguyen-tac-2026-11-13.md`, thư trả về của người kiểm (không thành hàng của bảng).

## 2. Bài 04 — dạng phụ thuộc vào $\delta$, $q_k$ sau Bổ đề 04.9

- **Vị trí:** `materials/lec-04/lecture-note.md`, Bổ đề 04.9, câu sau dòng **Bảo đảm.**, dòng 580.
- **Trích:** "nó phụ thuộc $m$ qua $\mathrm{rad}_k$, và $\delta$, $q_k$ qua $\ln(1/\delta)+\ln(1/q_k)$."
- **Nghi vấn:** với bán kính hội tụ đều tổng quát của Định nghĩa 04.8, $\delta$ và $q_k$ đi vào qua $\mathrm{rad}_k(m,\delta q_k)$; dạng $\ln(1/\delta)+\ln(1/q_k)$ chỉ đúng cho hai bán kính cụ thể của Định lý 02.14(a) và 03.15(a) (khi bán kính có dạng $\sqrt{\cdot\,\ln(1/\delta')}$ với $\delta'=\delta q_k$).
- **Đề xuất của người kiểm (chưa kiểm):** "…; nó phụ thuộc $m$, $\delta$ và $q_k$ qua $\mathrm{rad}_k(m,\delta q_k)$, và với các bán kính của Định lý 02.14(a), 03.15(a), $\delta$ và $q_k$ đi vào qua $\ln(1/\delta)+\ln(1/q_k)$."
- **Báo cáo gốc:** `lec-04/reviews/kiem-nguyen-tac-2026-11-13.md`, hàng #47.

## 3. Bài 05 — Ví dụ 05.12 lập luận theo $f(w_t)$, cận chặn $f(\bar w_T)$

- **Vị trí:** `materials/lec-05/lecture-note.md`, Ví dụ 05.12, dòng 1000–1007.
- **Trích dòng 1007:** "Điểm lặp cuối không hội tụ với độ dài bước hằng, nhưng ví dụ không vi phạm cận, vì $f(w_t)$ bằng số hạng $\eta G^2/2=0{,}1$ của cận."
- **Ngữ cảnh:** Bước 1: $f(w_t)=0{,}1$ với mọi $t$; Bước 2: $\bar w_T=0$ khi $T$ chẵn; Bước 3: vế phải của Định lý 05.14 là $0{,}025/T+0{,}1$.
- **Nghi vấn:** Định lý 05.14 chặn $f(\bar w_T)$ (điểm lặp trung bình), nên lý do "không vi phạm cận" phải là $f(\bar w_T)=0\le0{,}025/T+0{,}1$, không phải giá trị $f(w_t)$ của điểm lặp cuối. Cần kiểm lại Định lý 05.14 chặn đại lượng nào và sửa câu kết luận cho đúng đại lượng; trường hợp $T$ lẻ ($\bar w_T\ne0$) cũng cần xem.
- **Đề xuất của người kiểm (chưa kiểm):** "Tóm lại, với độ dài bước hằng, điểm lặp cuối dao động với $f(w_t)=0{,}1$, đúng bằng số hạng $\eta G^2/2$ của cận; điểm lặp trung bình thỏa cận vì $f(\bar w_T)=0$ khi $T$ chẵn."
- **Báo cáo gốc:** `lec-05/reviews/kiem-nguyen-tac-2026-11-13.md`, hàng #58.

## 4. Bài 09 — hai hiệu số ở Ví dụ học chuỗi kí tự (thí nghiệm bigram)

- **Vị trí:** `materials/lec-09/lecture-note.md`, Bước 2 (bảng, dòng 466–474), Bước 4 (dòng 480), dòng kết luận (dòng 482).
- **Bảng (hàm lỗi log trung bình theo kí tự trên tập kiểm tra, trung bình 10 lần chạy):** cột $m$ | MLE | Làm trơn | Mô hình thật; hàng $m=1$: $+\infty$ | $1{,}122$ | $1{,}091$; hàng $m=50$: $1{,}091$ | $1{,}091$ | $1{,}091$. Giá trị tốt nhất ghi trong bài: $1{,}0904$.
- **Trích dòng 480:** "lỗi kiểm tra của nó cao hơn của mô hình thật khoảng $0{,}032$" — bảng cho $1{,}122-1{,}091=0{,}031$.
- **Trích dòng 482:** "lỗi kiểm tra $1{,}091$ cách giá trị tốt nhất khoảng $0{,}0009$" — số trong bài cho $1{,}091-1{,}0904=0{,}0006$.
- **Nghi vấn:** có thể hai hiệu số được tính từ số chưa làm tròn của thí nghiệm, khi đó chữ "khoảng" đúng nhưng người đọc không kiểm lại được từ bảng. Cần chạy lại `tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec09_bigram.py` (ngoài repo) để lấy số chưa làm tròn, rồi chọn: ghi bảng thêm một chữ số, hoặc ghi hiệu số tính từ số trong bảng.
- **Báo cáo gốc:** `lec-09/reviews/kiem-nguyen-tac-2026-11-13.md`, thư trả về của người kiểm (không thành hàng của bảng).
