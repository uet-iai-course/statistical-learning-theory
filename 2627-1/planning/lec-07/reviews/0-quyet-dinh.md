# Quyết định gộp năm lượt rà — Bài 07 (điều phối viên, 2026-10-31)

Căn cứ: `1-hoc-vien.md` (0/1/8/10), `2-toan-hoc.md` (0/0/1/8), `3-chuyen-gia-nguon.md` (0/0/1/8; §E 12/12), `4-hoc-thuat-van-phong.md` (0/0/7/28), `5-mach.md` (0/0/3/14). Số dòng theo bản đóng băng `lec07-draft-frozen.md` (SHA-256 `90e35e5025ff45db`). Không có lỗi chặn bàn giao; mọi kết quả được người rà toán chứng minh lại đúng; thí nghiệm tái lập khớp (ba người rà chạy lại). Biên tập viên áp dụng mọi mục dưới đây; các phát hiện nhẹ còn lại áp dụng theo đề xuất trừ khi có lý do (ghi vào `bien-tap-vong-1.md`). Thân bài sau sửa ≤ 12 000 tiếng, phụ lục ≤ 3 000.

## Nghiêm trọng

**N1 (R1). Chuẩn trọng số lớp ra (dòng 27 và mọi chỗ dùng 916, 10 853).** Các số là chuẩn của $\hat w$ trên đặc trưng đã chia $\sqrt N$ ($\chi(x)=\operatorname{ReLU}(\cdot)/\sqrt N$); theo mô tả mạng ở câu hỏi mở đầu (nơ-ron tính $\max\{0,\langle v,x\rangle+c\}$, trọng số lớp ra nhân trực tiếp), chuẩn trọng số lớp ra là khoảng $20{,}5$ và $242{,}7$ (điều phối viên kiểm: $916/\sqrt{2000}\approx20{,}48$). Sửa: một quy ước duy nhất xuyên bài. Phương án chọn: giữ đặc trưng chuẩn hóa $\chi$ (cho $C_x$ cỡ $1{,}5$ và các cận của §8–§9), nói rõ ngay ở câu hỏi mở đầu rằng lớp ra nhận đặc trưng chia $\sqrt N$ và đại lượng báo là chuẩn của véc-tơ trọng số trên đặc trưng chuẩn hóa đó; hoặc báo cả hai. Tỉ số $11{,}85$ không đổi. Kiểm lại mọi số phụ thuộc (phần phạt, lề chuẩn hóa) cùng quy ước. Câu hỏi mở đầu cũng nói phép huấn luyện chọn nghiệm nội suy chuẩn nhỏ nhất (R1).

## Trung bình — quyết định cụ thể

1. **Nhãn hoán vị và (T1)** (R2, R3): các cặp $(x_i,y_{\pi(i)})$ không độc lập (tổng nhãn cố định). Ở Ví dụ 07.6, 07.10(iii) và §10: các cận của Định lý 07.11, Hệ quả 07.16 và Hệ quả 02.10(b) chỉ được áp cho nhãn thật; với nhãn hoán vị, nói giả thiết không thỏa và chỉ dùng vế phải như một con số so sánh (vế phải > 1 nên không kết luận gì). Một câu ở Phụ lục D. Ví dụ 07.10(iii): "hàm đã chọn độc lập với mẫu kiểm tra" thay "cố định trước khi rút".
2. **Làm tròn cận trên lên** (R2): $0{,}2408$; $0{,}2577$; $0{,}5153$; $0{,}2889$; $0{,}0889$; $0{,}0408$; ôn nhanh 3 $t\approx0{,}0961$; đầu dưới khoảng chuẩn $351$ (R3). Kiểm lại mọi cận trên khác.
3. **Danh sách tiên quyết** (R1, R4, R5): ghi tên khối như Bài 06; thêm Định nghĩa 04.1, 05.18, 06.9, Ví dụ 03.1 (nếu dùng); sửa "Bước 1–2" thành phạm vi thật của Định lý 03.15; bỏ Ví dụ 05.10 nếu không dẫn. Bù chữ bằng các chỗ cắt người rà đề xuất.
4. **Cầu nối sang Bài 08** (R5 F2): không gợi ý Bài 08 bỏ tính lồi; nêu Bài 08 xét quỹ đạo SGD với hàm lỗi lồi, trơn, Lipschitz (blueprint 8); có thể nối qua Phụ lục D (nghiệm chuẩn nhỏ nhất là giới hạn của hạ gradient khởi tạo tại $0$).
5. **Nhận xét 07.18** (R5 F3, R3 F4–F5, R2): đổi $\rho_j$ thành $G_j$; thêm giả thiết $\lVert x_i\rVert\le C_x$; nói phép đổi tỉ lệ giữ độ phức tạp phổ chỉ cho mạng ReLU không hệ số tự do (mạng của Ví dụ 07.2 có hệ số tự do); chỉ số $j$, $k$ không trùng nghĩa.
6. **Ví dụ 07.7** (R1, R4): một thiết lập nhất quán (không đổi $p=1$ sang $p=4$ giữa chừng); cách viết điểm không gây hiểu nhầm.
7. **Ví dụ 07.4 Bước 2–3** (R1, R4): tách theo §7a (bảng hẹp ≤ 4 cột hoặc danh sách).
8. **"Phần phạt" hai nghĩa** (R4): một nghĩa duy nhất (số hạng Rademacher $2\widehat{\mathfrak R}$ hay tổng; chọn và dùng nhất quán).
9. **Cận không cho thông tin** (R4): đặt thuật ngữ (vacuous bound) ở lần dùng đầu (Ví dụ 07.6); bỏ ẩn dụ "chứng nhận rỗng"; ý "bằng chứng, không phải chứng minh" giữ một lần ở câu hỏi mở đầu và một lần ở §10, cắt các lần khác (R1, R4).
10. **Định nghĩa 07.1** (R4): viết đệ quy $a_j=\varsigma(\Theta_ja_{j-1}+b_j)$ để công thức không cắt giữa ngoặc ở 390 px; xem lại thẩm mỹ Mệnh đề 07.2 và 07.9(a) ở 390 px.
11. **Câu hỏi cuối buổi (b)** (R1): đề cho đủ dữ kiện (tỉ lệ vi phạm lề của $\hat w$) hoặc lời giải không dùng số của câu (a).
12. **Lời hứa:** Bài 03 dòng 921: thêm UML §28.1 ở §13 (R3, R5); Bài 05 dòng 1100: thêm một dòng cận cho hàm lỗi logistic (R3 F7 đã dẫn hằng số; người rà toán kiểm ở vòng rà lại) và nối với Mệnh đề 04.3 nếu vừa chữ (R5 F5); dòng 859 không gán hàm lỗi bản lề cho Nhận xét 02.11 (R5 F7).
13. **Ví dụ 07.3 Bước 4, Ví dụ 07.8 Bước 3** (R1, R5): thêm lý do ($2^m$ cách gán nhãn; $d\ge2m$ cho cùng kết luận); câu về hàm ghi nhớ ở dòng 161 viết lại hoặc cắt (R1).

## Nhẹ đáng chú ý (áp dụng)

Ví dụ 07.6 "không cần kiểm (M)" giới hạn vào mẫu mà lớp tách trọn (R2); tính chất (iii) sau Định nghĩa 07.15: chỉ một chiều (R2); một câu về hằng số $2G$ của bản bổ đề co có trị tuyệt đối (R2); Phụ lục A trường hợp suy biến; Phụ lục C(iii) tính đo được của các cận trên (R2); $c$ cho hệ số tự do ở câu mở đầu đổi chữ (R3 F9); Nhận xét 07.3 nói UML phát biểu cho sigmoid (R3 F6); "phân loại" → "phân lớp"; tiếng Anh cho "hàm điểm số", "lớp hàm lỗi", "nhãn hoán vị", ReLU ở lần đầu; $\lvert E\rvert\to P$; "lớp" trơn trong tiêu đề Ví dụ 07.2; câu dẫn trước Bổ đề 07.8, Ví dụ 07.11, Nhận xét 07.18; bảng §2 "$B$ (§8)"; các câu > 45 tiếng, câu kết mục chỉ báo trước, câu lặp (R4). Gợi ý tùy chọn một lần McDiarmid ở Hệ quả 07.16 (R2): không áp dụng (giữ hằng số blueprint).
