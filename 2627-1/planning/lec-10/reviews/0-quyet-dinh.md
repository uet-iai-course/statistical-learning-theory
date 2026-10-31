# Quyết định gộp năm lượt rà — Bài 10 (điều phối viên, 2026-11-01)

Căn cứ: `1-hoc-vien.md` (0/2/9/16), `2-toan-hoc.md` (0/1/2/7; mọi kết quả chứng minh lại đúng, kể cả Phụ lục A Bước 6; mọi số khớp; EWC khớp Kirkpatrick tr. 3; cận hối tiếc khớp UML §21.3), `3-chuyen-gia-nguon.md` (0/0/3/10; §E 10/12; không chép nguồn; ba lời hứa được giữ), `4-hoc-thuat-van-phong.md` (0/0/9/20), `5-mach.md` (0/0/5/11; `forward_refs.py` 0; 30 số hiệu đúng). Số dòng theo bản đóng băng `lec10-draft-frozen.md` (SHA-256 `74d96d8878c447a0`). Biên tập viên áp dụng mọi mục và các điểm nhẹ còn lại theo đề xuất trừ khi có lý do (ghi `bien-tap-vong-1.md`). Thân ≤ 12 000 tiếng (đang 11 982: mọi chữ thêm phải bù; chuyển chi tiết sang phụ lục nếu cần, ≤ 3 000).

## Nghiêm trọng

**N1 (R1, R2, R4 T4, R5 T4). Ví dụ 10.16, Kết luận (dòng 749).** Các số $0{,}25$, $0{,}125$, $0{,}624$ là của mô hình hồi quy ở Phụ lục C ($L_A=\tfrac12(w^2+0{,}25)$), không phải của thiết lập trong ví dụ ($L_A=\tfrac12(w^2+1)$, điểm thỏa hiệp cho $L_A(\tfrac12)=0{,}625$). Sửa: một thiết lập nhất quán — hoặc kết luận chỉ dùng số tính được trong mô hình của ví dụ và chuyển số thí nghiệm sang một câu dẫn Phụ lục C có nêu rõ mô hình của thí nghiệm, hoặc đổi thí nghiệm cho khớp ví dụ (chạy lại script, cập nhật Phụ lục C). "$0{,}331$ gần $0{,}25$" sửa (R2).
**N2 (R1, R3 F2, R4 T8). Dòng 768.** "Hối tiếc dưới tuyến tính làm hàm lỗi trung bình tiến tới hàm lỗi của điểm cố định tốt nhất" sai (hối tiếc chỉ cho cận trên; Ví dụ 10.17 có hối tiếc $-116{,}97$). Sửa: hối tiếc tĩnh $o(T)$ nghĩa là hàm lỗi trung bình theo thời gian không vượt hàm lỗi trung bình của điểm cố định tốt nhất quá một lượng tiến về $0$.

## Trung bình — quyết định cụ thể

1. **Nhận xét 10.9(ii)** (R2): giá trị nền tính từ phần thưởng nhận trước bước $t$ là hàm của $\mathcal F_t$ nên hợp lệ khi $H\ge2$; sửa phát biểu (Ví dụ 10.10 Bước 2 dùng đúng điều đó).
2. **Định nghĩa 05.10 và Mệnh đề 08.12** (R1 dòng 397, 410; R3 F1; R2 nhẹ): câu "khác Định nghĩa 05.10" viết đúng: viết lượt qua các biến độc lập thì đưa được về 05.10; trở ngại thật là (C). Ví dụ 10.7 áp dụng Mệnh đề 08.12 có câu nối và giả thiết bước hằng $\eta\le1/\beta$.
3. **$\mathcal F_t$** (R5 T3): nói rõ ở Bài 10 $\mathcal F_t$ là bộ biến quan sát được trước $A_t$ (khác kiểu và lệch chỉ số so với σ-đại số $\mathcal F_{t-1}$ của Định nghĩa 05.10); bỏ câu "cùng vai". Điều phối viên sửa dòng `ky-hieu.md`.
4. **Kí hiệu một nghĩa** (R5 T1, T2; R2; R1; R3): hàm trội $M\to\Lambda$ (giữ $M$ cho ngân sách bộ nhớ); $K$ hằng số ở Phụ lục A đổi chữ (giữ $K$ cho số nhiệm vụ, giới thiệu trước khi dùng); Nhận xét 10.16, Ví dụ 10.17 dùng $R$ cho $\lVert w_1-u\rVert$ như Bài 05; $L_{\mathcal B}$ trùng $L_B$ đổi; tên trạng thái $s_1,s_2$ không trùng chỉ số bước; $h$ một nghĩa.
5. **"Người học"** (R1, R3, R4 T3, R5): trong văn bản cho học viên chỉ dùng "tác tử" (agent) hoặc "thuật toán học"; không dùng "người học" cho thuật toán (theo `thuat-ngu.md`).
6. **"Độ chính xác"** (R1, R4): dùng "độ chính xác phân lớp" $=1-$ lỗi 0–1, định nghĩa tại chỗ, nối với hàm lỗi; "chính xác", "nghiệm" mỗi chữ một nghĩa (R4). Điều phối viên đã sửa `thuat-ngu.md`.
7. **Quy ước độ đo** (R4 T6): bỏ khẳng định không có cơ sở "các bài báo dùng những quy ước khác nhau" (dòng 607) hoặc diễn đạt chỉ dựa trên ví dụ của bài (hai quy ước cho giá trị khác dấu, Ví dụ 10.14); khớp với dòng 908.
8. **Sutton–Barto** (R3 F3): §13 nói REINFORCE trong Sutton–Barto (bài đọc trước buổi) dùng tổng phần thưởng từ bước $t$, tức ước lượng của Mệnh đề 10.7(b), còn Thuật toán 10.6 dùng $R(\tau)$.
9. **Câu hỏi mở đầu** (R1): trả lời việc gộp mẫu ở tình huống 2.
10. **Ví dụ từng bước và thiết lập nhất quán** (R1, R4 T4–T5): Ví dụ 10.6 Bước 2; Ví dụ 10.10 Bước 1 (cho đủ phép tính, không chỉ ba tổng) và Bước 2; Ví dụ 10.13 Bước 5; các dòng 523, 571, 724, 744, 795–797; Ví dụ 10.15 thêm câu nối Fisher với Hesse (R1, R3) và $\Omega$ không chéo ngoài Định nghĩa 10.12 (R2) nói rõ; EWC chỉ đúng nguyên văn với hai nhiệm vụ (R3).
11. **§10 và §12(f)** (R2, R5 T5): "$225$ lần" và "$\alpha^2/(2M)$" nói là của Ví dụ 10.11, 10.16; §12(f) nhìn lại đủ Bài 01–09 (không bỏ Bài 05, 06, 08; nêu Thiết lập B của Bài 09 vi phạm (T1)); §10 đoạn 2 không chỉ nói Phần A.
12. **Văn phong** (R4 T1, T2, T7, T9): câu kết mục ở 413, 578, 631, 752, 802 viết văn xuôi không tóm tắt, không châm ngôn; ý "chỉ giữ kì vọng, không nói gì về phương sai" giữ một lần; đoạn mở không bọc "Câu hỏi cuối Bài 09 là …", không lặp câu hỏi trung tâm; tách các câu dài ở 146, 531, 682, 712, 808.
13. **Phụ lục C** (R1): nêu cách rút hành động và cách cập nhật đủ để tái lập phần REINFORCE.

## Nhẹ đáng chú ý (áp dụng)

Nhận xét 10.5 và 10.16 có dòng Giả thiết/Bảo đảm; bảng Ví dụ 10.8 vừa 271 px theo bản sửa N13 của R4; danh sách tiên quyết bỏ khối thừa, thêm khối thiếu (R5); mục tiêu 5 giữ vế ví dụ hai nhiệm vụ bậc hai; Ví dụ 10.12 có câu dẫn; câu "học có giám sát với phân bố $\frac1K\sum_kD_k$" nói đúng về mẫu phân tầng (R2); "chính sách tốt nhất" ở Ví dụ 10.11 nói rõ trong họ nào (R2); câu hai nghĩa ở dòng 840; dấu hai chấm "tiết lộ", văn bản làm chủ ngữ (R4).
