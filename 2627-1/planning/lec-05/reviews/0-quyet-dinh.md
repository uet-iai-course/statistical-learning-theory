# Quyết định của điều phối viên sau năm lượt rà — Bài 05 (2026-10-31)

Căn cứ: `1-hoc-vien.md` (R1: 0/1/5/22), `2-toan-hoc.md` (R2: 0/0/1/10; 206 con số, mọi chứng minh dựng lại đúng), `3-chuyen-gia-nguon.md` (R3: 0/0/6/10; §E 10/12), `4-hoc-thuat-van-phong.md` (R4: 0/0/14/21), `5-mach.md` (R5: 0/0/5/12) — số theo thứ tự chặn bàn giao/nghiêm trọng/trung bình/nhẹ. Không có lỗi chặn bàn giao; không có lỗi trong chứng minh. Điều phối viên đã kiểm lại trên PDF: UML §14.4.1 (tr. 193) viết phép chiếu bằng $\arg\min$, không dùng $\Pi$ (R3 đúng); §12.1 bắt đầu ở tr. 156, §14.2 ở tr. 188 (đã sửa `sources/uml-sections.md`).

Mọi mục dưới đây **chấp nhận** trừ khi ghi khác. Biên tập viên giữ thân bài ≤ 12 000 tiếng (`wc -w`), phụ lục ≤ 3 000; bù phần thêm bằng các chỗ cắt ở mục C. Số dòng theo bản đóng băng `lec05-draft-frozen.md`.

## A. Nghiêm trọng

- **N1 — $h_w$ và $\ell(w,z)$ trong phân lớp** (R1; dòng 88–89, 227, 916–919, 930). Hàm lỗi bản lề và logistic phụ thuộc điểm số $\langle w,x\rangle$, không phụ thuộc nhãn $h_{w,0}(x)\in\{0,1\}$; vì vậy $\ell(h_{w,0},z)$ không xác định. Sửa: trong bài, $h_w(x)=\langle w,x\rangle$ luôn là *hàm điểm số* (score function) $\mathcal X\to\mathbb R$, cho cả hồi quy và phân lớp; hàm phân lớp tương ứng là $h_{w,0}=\mathbb 1[h_w\ge0]$ của Định nghĩa 03.7, chỉ dùng khi nói về lỗi 0–1. $\ell(w,z)$ viết thay cho $\ell(h_w,z)$ với hàm lỗi của dự đoán thực. Định nghĩa 05.18 và Hệ quả 05.19: lớp $\{h_w:w\in W\}$ là lớp hàm điểm số; $\operatorname{opt}_s(w)=L_s(w)-\inf_{w'\in W}L_s(w')$ (Định nghĩa 04.2 áp dụng cho lớp này và hàm lỗi này). Sửa bảng §2, mục "Từ Bài 03" ở Kiến thức tiên quyết, Ví dụ 05.2, khối ứng dụng nếu cần. Điều phối viên sẽ sửa `ky-hieu.md`.

## B. Trung bình

- **M1 — Câu trả lời mở đầu** (R5; dòng 13): "Không nhất thiết, kể cả theo kì vọng."
- **M2 — "Độ chênh tối ưu" có công thức** (R5, R4 #5, R3; dòng 3, 15, 136, 673, 930, 938, 1118, 1130). Định nghĩa bằng một câu có công thức ở lần dùng đầu trong thân (§1, mục **Đối tượng so sánh**): $F(w)-F(u)$, hoặc $F(w)-\inf_{w'\in W}F(w')$. Khi $F=L_S$ và so với $\inf_W L_S$, đại lượng này là sai số tối ưu thực nghiệm $\operatorname{opt}_S$ (Định nghĩa 04.2) và từ đó gọi đúng tên này; không bao giờ viết "sai số tối ưu" trơn.
- **M3 — Số hạng $\tfrac\eta2\lVert g\rVert^2$** (R5; dòng 609, 613, 647, 713): không gọi là "số hạng nhiễu" (GD cũng có); gọi là "số hạng bậc hai theo độ dài bước" hoặc nêu thẳng công thức, và mức sàn $\eta G^2/2$ đặt tên một lần.
- **M4 — "Mô hình Lipschitz"** (R5; dòng 1058): thay bằng "so sánh giữa các cận trên dưới (C), (G2), không phải so sánh thời gian chạy".
- **M5 — Câu về chương trình rút quan sát mới** (R1, R3, R5; dòng 919): **xóa** câu cuối; §13 (cầu nối) giữ nội dung về Bài 06, không phát biểu dạng thuật toán.
- **M6 — Điểm lặp cuối không phải giả thiết bị bỏ** (R1, R4 #1; dòng 27, 1068–1073): §11 liệt kê ba giả thiết (tính lồi, mô-men bậc hai, oracle không chệch) và một câu riêng: định lý không nói gì về điểm lặp cuối; trong Ví dụ 05.12 điểm lặp cuối dao động ở mức $f=0{,}1$. Mục tiêu 5: "Dựng phản ví dụ khi bỏ tính lồi, cận mô-men bậc hai hay tính không chệch của oracle, và giải thích vì sao cận không nói gì về điểm lặp cuối." Câu dẫn §8 giữ "hoặc đổi đầu ra".
- **M7 — Chứng minh rời rạc của Bổ đề 05.12** (R1, R2; dòng 564–604): một câu nối: khi $\Xi$ hữu hạn và $P_\xi(k)>0$, mỗi biến cố $\{(\xi_1,\ldots,\xi_{t-1})=k_{1:t-1}\}$ có xác suất dương và $\mathbb E[\cdot\mid\mathcal F_{t-1}]$ bằng kì vọng có điều kiện theo biến cố đó trên biến cố đó; đổi kí hiệu lịch sử $h$ thành $k_{1:t-1}$; tiêu đề "chứng minh cho $\Xi$ hữu hạn".
- **M8 — Chỗ dùng tính lồi** (R1; dòng 693–697, 716, Mục tiêu 1): sửa quyết định 4 của điều phối viên về dàn ý. Bước 3 dùng (G1): bất đẳng thức dưới gradient là định nghĩa của dưới gradient, áp dụng cho $\psi(w_t)\in\partial F(w_t)$. Tính lồi của $F$ dùng ở Bước 5 (bất đẳng thức lồi hữu hạn) và là điều kiện để (G1) thỏa được ($\partial F(w)\ne\varnothing$, Định nghĩa 05.2). Viết đúng như vậy ở tiêu đề các bước, đoạn sau chứng minh, §8 (Ví dụ 05.10 hỏng vì đạo hàm không là dưới gradient, tức (G1) hỏng, do $F$ không lồi) và §11. Mục tiêu 1 giữ nguyên.
- **M9 — Ví dụ 05.6 Bước 3 từng bước** (R1, R4 #9; R2 nhẹ): thêm $g_3$, điểm trước chiếu và chuẩn của nó (số trong R4 #9), nói dòng nào bị chiếu; bước GD ghi điểm $(0{,}8330;-0{,}7670)$, chuẩn $1{,}1324$, rồi chiếu. Biên tập viên tính lại.
- **M10 — Ví dụ 05.13** (R2, R3; dòng 896–902, 1072): thêm $W=[-1,1]$, $w_1=0$ (để (G2) thỏa); "khi $T$ tăng với độ dài bước của Hệ quả 05.15, $\bar w_T$ tiến tới cực tiểu $0{,}1$ của $\tilde F$ theo kì vọng, nên độ chênh của $L_S$ tiến tới $0{,}16$, không về $0$". Không viết "với mọi $T$".
- **M11 — Quan hệ với UML** (R3; dòng 1143 và `outline.md` §7): UML viết phép chiếu bằng $\arg\min$; $\Pi$ là kí hiệu của blueprint và trùng hàm tăng trưởng $\Pi_{\mathcal H}$ của học phần. Không nói UML dùng $\Pi$.
- **M12 — Tính trơn và UML §14.4.4** (R3; dòng 322): §14.4.4 chỉ xét hàm lồi mạnh; không gán tính trơn cho mục này.
- **M13 — Đủ, không phải cần; lượng từ** (R3; dòng 733, 1066, và mọi câu tương tự): "số vòng lặp đủ theo cận", "với xác suất ít nhất $0{,}95$ theo $\xi$", "theo cận" cho so sánh lô nhỏ.
- **M14 — Tên của $L_D(\bar w)-\min_WL_D$ trong câu hỏi cuối buổi** (R3; dòng 1127, 1130): đây là sai số ước lượng đối với lớp $\{h_w:w\in W\}$ (Định nghĩa 04.1), không phải độ chênh tối ưu; viết đúng tên, một câu tách hai đại lượng.
- **M15 — Mười bốn mục trung bình của R4** (#2–#14): chấp nhận tất cả. Riêng #4: tập mở trong Mệnh đề 05.5 viết $U$; lịch sử $k_{1:t-1}$ (M7); bổ đề đóng băng dùng $\Phi$, $\bar\Phi$. #14: bổ đề đóng băng ghi "phát biểu không chứng minh", bỏ "kết quả chuẩn"; không thêm nguồn. #11: nhãn song song theo đề xuất của R4. #6: văn bản không làm chủ ngữ ("Phần này hoàn tất…", "§7 tìm", "§8 xét", "học phần dùng…").

## C. Cắt để giữ ngân sách

Theo R5 (12 chỗ, khoảng 269 tiếng: dòng 909, câu đầu 716, 807, 919 câu cuối…), R4 #12, #13 (đoạn kết tóm tắt ở 427, 840, 909, 984; câu lặp 913, 829, 711, 904, 1058, 342), R1 (Định nghĩa 06 dòng 322–340 rút gọn nếu cần). Không cắt nội dung toán học, chứng minh hay bước ví dụ.

## D. Nhẹ

Chấp nhận mọi điểm nhẹ của năm báo cáo, trừ:

- **Làm tròn** (R2): số in sau "$\le$" như một cận được làm tròn lên: $4{,}0007$ (giá trị $4{,}000625$), $0{,}2281$ ($0{,}2280087$); sửa phép so sánh "$4-0{,}06112$" ở dòng 783 theo R2. Số trong bảng giữ làm tròn gần nhất.
- **Mệnh đề 05.5** (R2): giả thiết tách theo phần; (a) không cần tập mở (dòng 286 áp dụng (a) cho quả cầu đóng).
- **Liên kết `exercises.md` ở §12** (R5): giữ; bài tập được soạn ngay sau ghi chú, như Bài 04.
- **Lời hứa Bài 01 dòng 846** (R5): một câu ở §11 nói bảo đảm thống kê cho hàm lỗi Lipschitz thuộc Bài 06–07 (đã có ở dòng 964; không thêm câu mới nếu đã đủ).
- **Ngoài bản thảo, điều phối viên tự sửa:** `sources/uml-sections.md` (§12.1 tr. 156, §14.2 tr. 188); `thuat-ngu.md` hai dòng "internal randomness" (R3); `ky-hieu.md` theo N1 và M15 #4.
