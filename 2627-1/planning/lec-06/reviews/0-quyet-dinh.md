# Quyết định gộp năm lượt rà — Bài 06 (điều phối viên, 2026-10-31)

Căn cứ: `1-hoc-vien.md` (0/1/7/15), `2-toan-hoc.md` (1/0/2/7), `3-chuyen-gia-nguon.md` (1/1/3/7), `4-hoc-thuat-van-phong.md` (0/1/11/29), `5-mach.md` (0/0/4/16). Số dòng theo bản đóng băng `lec06-draft-frozen.md` (SHA-256 `1a2fd0319e4b55ac`). Biên tập viên áp dụng mọi mục dưới đây; với các phát hiện nhẹ không nêu tên ở đây, áp dụng theo đề xuất của người rà trừ khi có lý do (ghi lý do vào `bien-tap-vong-1.md`). Thân bài sau sửa ≤ 12 000 tiếng (`wc -w`), phụ lục ≤ 3 000.

## Chặn bàn giao

**C1 (R2, R3; R1 xếp nghiêm trọng). Định lý 06.10, Bước 2, dòng 671; câu cuối khối định lý, dòng 650.** Câu "Vế phải bằng $\mathbb EL_D(A(S^{(i)};\xi))$ theo Bước 1 áp dụng cho $S^{(i)}$" sai: $Z'$ là phần tử thứ $i$ của $S^{(i)}$. Điều phối viên kiểm lại: ghép với Bước 3, câu này cho khoảng cách tổng quát hóa kì vọng bằng $0$ với mọi thuật toán, trái Ví dụ 06.3 và $A_{\mathrm{gn}}$. **Sửa:** bỏ câu sai; chứng minh tính hữu hạn bằng tính ổn định: với mọi $i$, theo Định nghĩa 06.9 (quan sát kiểm tra $z_i$) và Bước 2,
$\mathbb E\,\ell(A(S;\xi),Z_i)\le\mathbb E\,\ell(A(S^{(i)};\xi),Z_i)+\epsilon_{\mathrm{stab}}(m)=\mathbb EL_D(A(S;\xi))+\epsilon_{\mathrm{stab}}(m)<\infty$
(kì vọng theo $\xi$ lấy trước bằng Fubini cho hàm không âm). Sửa câu cuối khối định lý: "Giả thiết khả tích và tính ổn định đều kéo theo $\mathbb EL_S(A(S;\xi))<\infty$ (Bước 2)". Đánh dấu chỗ dùng tính ổn định ở Bước 2.

## Nghiêm trọng

**N1 (R1, R4). Dòng 108:** "Quan sát thay thế và quan sát kiểm tra của §7 độc lập với mọi đại lượng khác" sai (quan sát kiểm tra là điểm bất kì; chứng minh dùng $z=z_i$). Sửa: chỉ nói quan sát thay thế $Z'$ trong chứng minh của §7 độc lập với $(S,\xi)$; quan sát kiểm tra là một điểm bất kì của $\mathcal Z$.

**N2 (R3; R2 nhẹ). §13, dòng 1130:** mô tả UML §14.5.1 như chỉ đổi chỗ gradient và kì vọng là sai (UML tr. 197 có lập luận dưới gradient). Sửa: chỉ giữ khác biệt về cách đếm ($T$ so với $T-1$).

## Trung bình — quyết định cụ thể

1. **Hệ quả 04.17 cần (T3)** (R5 T1, R2): ở Nhận xét 06.14 ("Tăng độ tin cậy") và §10 (chọn $\lambda$ bằng mẫu xác thực), nêu điều kiện hàm lỗi trong $[0,1]$; với hồi quy logistic, nói việc chọn trên mẫu xác thực dùng một hàm lỗi bị chặn (chẳng hạn hàm lỗi 0–1). Thừa số "cỡ $\ln(1/\delta)$" viết chính xác theo Bài tập 06.7: số khối $k=\lceil\log_2(2/\delta)\rceil$ cộng một mẫu xác thực cỡ $8\ln(4k/\delta)/\epsilon^2$; không nói hơn.
2. **Câu báo trước Bài 08** (R5 T2; dòng 626, 1043, 1117, 1283): nêu điều kiện "hàm lỗi lồi, trơn và Lipschitz" (blueprint Bài 08), không hứa cho SGD nhiều vòng nói chung. "khoảng cách tổng quát hóa bằng chính $L_D$" sửa thành "xấp xỉ $L_D$" (R2, R3, R5).
3. **Hai nghĩa của $B$; $R$** (R1, R5 T3): trong Hệ quả 06.13(c) và Ví dụ 06.10, 06.11, $B$ là cận chuẩn của điểm so sánh và $W_B=\{u\in W:\lVert u\rVert\le B\}$; bảng §2 ghi $B$ là "bán kính quả cầu tâm $0$: của $W$ (khi $W$ là quả cầu) hoặc của tập điểm so sánh $W_B$ (§9)" và thêm $R$ (cận $\lVert w_1-u\rVert$, Bài 05). §1 không dùng $B$ trước §2 (hoặc dẫn "§2"). Điều phối viên sửa `ky-hieu.md`.
4. **"Rủi ro vượt mức kì vọng"** (R1): định nghĩa tại lần dùng đầu trong thân bài: $\mathbb EL_D(\cdot)-\inf_WL_D$, kì vọng của rủi ro vượt mức (Định nghĩa 01.24) so với $W$; dùng nhất quán. "rủi ro thực nghiệm kì vọng" đổi thành "kì vọng của rủi ro thực nghiệm" (R4).
5. **§10 trả lời thẳng câu hỏi trung tâm** (R5 T4): câu mở §10 thay câu siêu ngôn ngữ bằng câu trả lời: tối ưu trở thành học khi oracle không chệch cho $L_D$ (quan sát mới), hoặc khi thuật toán trên mẫu cố định có khoảng cách tổng quát hóa kì vọng nhỏ, chẳng hạn ERM có chính quy hóa nhờ tính ổn định đều.
6. **Kí hiệu $v$ trong chứng minh Mệnh đề 06.11, Ví dụ 06.6, Phụ lục B** (R4): $v$ đã là quy tắc dưới gradient; đổi thành $\hat w=\hat w_s$, $\hat w'=\hat w_{s^{(i)}}$ (hoặc cặp chữ khác không trùng; ghi vào §13 của dàn ý).
7. **Thuật ngữ** (R4): tiếng Anh ở lần đầu cho tăng trưởng bậc hai (quadratic growth), lập luận đổi vai (exchange argument; đặt tên ở lộ trình Định lý 06.10), thuật toán hằng (constant algorithm), bất đẳng thức oracle (oracle inequality, kèm một câu giải thích như Bài 04); "cấp thuật toán"/"cấp lớp" giải thích một lần (bảo đảm cho đầu ra của một thuật toán cụ thể, so với bảo đảm đồng thời cho mọi giả thuyết của lớp); dòng 122 "hàm lỗi log" sửa thành hàm lỗi logistic của mô hình tuyến tính.
8. **Ví dụ từng bước** (R1, R4): Ví dụ 06.3 Bước 3 viết đủ khai triển $\mathbb E\bar w_T^2=\sum_tc_t^2+\sum_{t\ne s}c_tc_s\Pr(i_t=i_s)$; Ví dụ 06.5 dùng một thiết lập nhất quán, báo rõ khi đổi, nêu công thức nhị thức; dòng 628 (thuật toán ghi nhớ trong một câu 58 tiếng) tách thành các bước ngắn; câu cuối dòng 703 viết thẳng.
9. **Phụ lục E(iii)** (R1, R2, R3): thay phản ví dụ bằng cấu trúc của R2 — thuật toán trả về giả thuyết có hàm lỗi $\ell(h_s,z)=\mathbb 1[z\in s]$: vế trái của điều kiện thay một theo trung bình luôn $\le0$ (vì $\ell(h_S,Z_i)=1$), nên điều kiện đúng với $\epsilon=0$ dưới mọi $D$; hệ số ổn định đều bằng $1$. Nêu rõ đây là điều kiện một phía như UML. Sửa tên mục UML §13.2 cho đúng (R3).
10. **Dẫn UML:** dữ liệu không bị chặn là §12.2.1 (Ví dụ 12.9), không phải §12.2.2 (dòng 872, 1123; R2, R3). Số bài tập UML theo quy ước Bài 05: **Bài tập 13.1, 13.2, 13.3, 14.1, 13.4** (không viết "14.8.1"; R3); đồng bộ §11 và `outline.md`.
11. **Ví dụ 06.11 Bước 3** (R5, R1): thay $\lambda=10^{-3}$ bằng $\lambda^*=4\cdot10^{-4}$: $\epsilon_{\mathrm{stab}}=2/(4\cdot10^{-4}\cdot10^6)=0{,}005$, cộng phần khớp $\tfrac{\lambda^*}2B^2=0{,}005$, tổng $0{,}01$ (điều phối viên đã kiểm); kết luận trả lời câu hỏi thực hành của khối ứng dụng §3 ((i) $0{,}005$, (ii) $0{,}01$).
12. **Hình 06.1** (R1, điều phối viên): sửa vị trí nhãn "0,615", "0,178" để không chạm đường cong hay điểm cực tiểu; dẫn hình trong văn bản ("Hình 06.1" ở Ví dụ 06.4). Hai khung dùng thang tung khác nhau: ghi trong chú thích.
13. **Số $1{,}7988$** (R2, R4): viết giá trị chính xác $304/169\approx1{,}7988$, đạt tại $z=(1,-1)$; bỏ "dò trên lưới".

## Nhẹ đáng chú ý (áp dụng)

Dòng 729 (Hệ quả 06.2 chỉ cần cận gradient trên $W$, không cần Lipschitz trên tập mở; R2); dòng 574 (công thức ridge một chiều chỉ là nghiệm trên $W$ khi giá trị thuộc $W$; R2); câu cuối Phụ lục A thêm "tách được bởi một siêu phẳng qua gốc" (R2); dòng 754 "không phụ thuộc trực tiếp" (R3); dòng 1128 thừa số 8 so với 4 đến từ lập luận một phía (R3); dòng 1049 hội tụ đều hỏng khi $p\to\infty$ (R3); trùng $w_1$ ở Phụ lục E (R3); $c_s$ ở Phụ lục D đổi chỉ số (R5); câu kết §3 không hứa §4 dùng Ví dụ 06.1 (R5); phân biệt hai "mẫu bốn quan sát" (R5); tiêu đề Bài tập 06.7 bỏ dạng "Từ … sang …" (R4): đề xuất "Cận với xác suất cao và tăng độ tin cậy cho ERM có chính quy hóa"; ý "không chặn $\mathbb E\lvert L_D-L_S\rvert$" giữ ở Định lý 06.10, Ví dụ 06.5 và §10, cắt các lần lặp khác (R4); các đoạn chỉ đường và lặp R4 nêu (dòng 181, 593, 889, 1043, 1047, 1060/1117, 551/1166) cắt để bù chữ.
