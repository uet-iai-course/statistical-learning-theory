# Quyết định của điều phối viên sau hai lượt rà bài tập — Bài 04 (2026-10-31)

Căn cứ: `9-bai-tap-toan.md` (B1: 0/0/4/13; khoảng 190 con số, sai chỉ ba chỗ làm tròn; không chép bản lời giải) và `10-bai-tap-su-pham.md` (B2: 0/0/7/31; tiêu đề và mục tiêu khớp §10 của ghi chú). Không có lỗi chặn bàn giao hay nghiêm trọng. Điều phối viên đối chiếu với bản đóng băng (`lec04-ex-frozen.md`; dòng dẫn theo bản này) các mục 04.3(d) dòng 338–343 (Bước 2 cần hàm lỗi 0–1: với hàm lỗi tổng quát thỏa (T3), $L_S(h)=1$ không nhất thiết đạt) và 04.6 dòng 586, 589; tính số mới của T4: trong thiết lập Ví dụ 04.8 với $q_k=1/k$, chỉ $k\le3$ có bán kính $\sqrt{\ln(40k)/20}<\tfrac12$, nên xác suất thất bại là $1-(1-2^{-9})^3\approx0{,}0058$.

Mọi mục dưới đây **chấp nhận** trừ khi ghi khác. Giữ ≤ 10 000 tiếng (`wc -w`); bù phần thêm bằng cắt lặp và rút gọn (mục C).

## A. Trung bình

- **T1 — 04.4(a) lặp Ví dụ 04.9** (B2). Ghi chú đã in đủ mười số hạng phạt và tổng. Viết lại (a): dùng bảng của Ví dụ 04.9, chạy Thuật toán 04.12 với quy tắc dừng, xác định các lớp được duyệt, lớp nào làm thuật toán dừng và vì sao các lớp sau không cần giải ERM; lời giải tính một ô không có trong ghi chú (ví dụ $\mathrm{pen}_{11}$ của một lớp giả định thứ mười một, hoặc so $\mathrm{pen}_k$ với giá trị tốt nhất $v$). "Kiểm tra lại" của 04.4 kiểm điều mới (B1).
- **T2 — 04.1(c) lặp Nhận xét 04.4** (B2). Đổi thành một phép tính mới trên mẫu $S_\eta$ như dàn ý dự kiến: so $h_4$ với $h_2$, $h_3$, $h_5$ (dấu của hiệu theo rủi ro kì vọng, sự phụ thuộc vào cách chọn khi bằng nhau), không yêu cầu nêu lại lý do của Nhận xét 04.4.
- **T3 — Mục tiêu 2 chưa đo "độ chệch khác sai số xấp xỉ"** (B2). Thêm một ý ngắn vào 04.2: với ước lượng co $\gamma\bar Y$ và lớp các hàm hằng, sai số xấp xỉ bằng $0$ (hàm hằng $\mu$ thuộc lớp) trong khi độ chệch bằng $(\gamma-1)\mu\ne0$ khi $\gamma\ne1$; kết luận một dòng.
- **T4 — Mục tiêu 5 chưa đo "xác suất thất bại không được chia"** (B2). Thêm một ý vào 04.3: trọng số $q_k=1/k$ có tổng phân kì; chỉ ra bước hỏng trong chứng minh Bổ đề 04.9; trong thiết lập Ví dụ 04.8 ($m=10$, $\delta=0{,}05$, $k_{\max}=1000$) tính xác suất thất bại ($\approx0{,}0058$, chỉ $k\le3$ có bán kính dưới $\tfrac12$) và giải thích vì sao con số nhỏ này không cứu được bảo đảm (bổ đề cần cận cho mọi $D$ và mọi họ; Ví dụ 04.8 với $q_k=1$ cho $0{,}858$).
- **T5 — Kí hiệu** (B1, B2). 04.13: số lớp viết $k_{\max}$; 04.9: $k(h)$ thay $n(h)$ (như ghi chú); 04.10: ngưỡng độ dài không dùng chữ $L$ (chọn chữ không trùng bảng kí hiệu, ví dụ $B$ như dàn ý).
- **T6 — Bước** (B2). Lời giải 04.4(b) tách bước (hai thiết lập, mỗi thiết lập một bảng hoặc dòng `aligned`, rồi kết luận); câu 42 tiếng của đề 04.5(b) thành câu dẫn và danh sách nhãn song song (§3a).
- **T7 — 04.3(d) hàm lỗi 0–1** (B1). Bước 2 thêm giả thiết hàm lỗi 0–1 (hoặc một hàm lỗi đạt giá trị $1$), nói rõ phạm vi của khẳng định "không nhỏ hơn $1$".
- **T8 — 04.11 và UML 7.5** (B1). Tiêu đề ghi các ý dùng; câu đầu của bài nói rõ các ý 1–2 của UML (dẫn ngược định lý) không lấy và ý thử thách gộp ý 3, 5 với thu hẹp về hàm phân lớp đo được. Nếu tiêu đề đổi, sửa dòng §10 tương ứng của ghi chú.
- **T9 — 04.6** (B1). Dòng 586: bỏ "một kết quả khác là lỗi lập trình"; nói quy tắc 1 đạt rủi ro thực nghiệm nhỏ nhất tại bậc $15$ (khi có bằng nhau, phụ thuộc quy tắc chọn). Dòng 589: lý do đúng là Định nghĩa 04.8 và Định lý 04.11 cần hàm lỗi trong $[0,1]$ (T3), không dẫn Bài tập 04.4(d).

## B. Nhẹ

Chấp nhận mọi điểm nhẹ của hai báo cáo, với các ghi chú:

- **Làm tròn** theo quy tắc của ghi chú (số dùng làm cận trên làm tròn lên): $0{,}5399$, hiệu $0{,}1683$, $0{,}0319$.
- **Đổi tên bài 04.3, 04.8, 04.12** (B2 nhẹ): chỉ đổi nếu tên mới rõ hơn; mỗi tên đổi phải đổi cùng dòng §10 của ghi chú.
- 04.7(b): nói rõ cả hai cận tại $m=10^3$ lớn hơn $1$ nên không cho thông tin (B1). 04.13: nói rõ giả thiết $\lvert\mathcal H_i\rvert=2^i$ là học phần thêm (B1).
- Gợi ý của 04.8(a) không được là toàn bộ chứng minh (B2): hai gợi ý tăng dần.

## C. Ngân sách

≤ 10 000 tiếng. Cắt: phần lặp Ví dụ 04.9 ở 04.4(a) (T1), phần lặp Nhận xét 04.4 ở 04.1(c) (T2), câu trên 40 tiếng B2 liệt kê (dòng 3, 5, 7, 353, 470, 479, 540, 589), đoạn mở đầu dòng 3–7 rút gọn (chỉ kí hiệu và thuật ngữ thật sự dùng trong bài tập).

## D. Ghi chú bài giảng

Người soạn bài tập sửa trong `lecture-note.md` (chỉ những dòng này): câu cuối §7 thành "Lớp mọi hàm phân lớp đo được trên một miền vô hạn …" (đề nghị của người soạn, khớp ý thử thách 04.11); các dòng §10 nếu tiêu đề bài tập đổi (T8, B). Sau khi sửa: `forward_refs.py` 0, thân bài ≤ 12 000 tiếng.
