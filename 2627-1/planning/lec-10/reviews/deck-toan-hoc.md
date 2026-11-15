# Duyệt deck Bài 10 — Vai 2 `toan-hoc` (độ chính xác toán học, thống nhất với ghi chú)

Người duyệt: tác tử general-purpose, Opus 5.5, effort high (chỉ đọc). Ngày 2026-11-16.

Bản duyệt: `2627-1/lecture-10-gradient-chinh-sach-hoc-lien-tuc.html` (54 trang, bản đóng băng), `img/lec-10/phuong-sai-gia-tri-nen.svg` (F1), `img/lec-10/danh-doi-hai-nhiem-vu.svg` (F2). Đối chiếu: `materials/lec-10/lecture-note.md`, `exercises.md`, `planning/lec-10/storyboard.md` §5 (V1–V24), `review-log.md` § Bộ trang chiếu; các khối được dẫn của Bài 02 (Hệ quả 02.10), Bài 05 (Định nghĩa 05.10), Bài 08 (Mệnh đề 08.12), Bài 09 (Mệnh đề 09.3).

## 1. Tính lại độc lập

Script trong thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-10/rv-toan-hoc/` (`check.py`: phân số chính xác và sai phân hữu hạn; `sim.py`: chạy lại Phụ lục C).

| Mục | Trang | Kết quả tính lại | Khớp |
|---|---|---|---|
| V1 câu hỏi mở đầu | 1-06 | $0{,}2+0{,}6q$: $0{,}5$; $0{,}74$; $L_A(1)=\tfrac12$ | có |
| V2 Ví dụ 10.1 | 2-02 | $\pi=\tfrac34$, $J=\tfrac52$, $J'=\tfrac38$ | có |
| V3 Ví dụ 10.2 | 2-05 | tám quỹ đạo, $p_0$ và $R$ như bảng; $2$, $\tfrac12$; $1{,}7$, $1{,}8$; $J(0)=\tfrac74$ | có |
| V4 Ví dụ 10.3 | 3-02 | $J'=\tfrac12$; $\mathbb E\,\partial\ln p=-1/\theta$; $\mathbb E[A(-1/\theta)]=-\tfrac12$ | có |
| V5 Ví dụ 10.4 | 3-06 | $\pm0{,}75$; $\mathbb E\hat g=\tfrac38$; $\mathbb E$ gradient log $=0$ | có |
| V6 Ví dụ 10.5 | 3-07 | gradient $(-\tfrac1{40};\tfrac14;-\tfrac18)$; sai phân trung tâm $(-0{,}0250;0{,}2500;-0{,}1250)$; $\tfrac14(1{,}7-1{,}8)$ | có |
| V7 Ví dụ 10.6 | 3-08 | đạo hàm đúng $0{,}125$ (sai phân); kì vọng ước lượng $-0{,}25$; $J=1{,}75$ | có |
| V8 Ví dụ 10.7 | 3-10 | $q=0{,}375$, $\theta=\ln0{,}6=-0{,}5108$, $J=0{,}375$, $d^2J/d\theta^2=0{,}17578$; $\sigma(-1)=0{,}2689<0{,}375<\sigma(-0{,}4)=0{,}4013$ nên hai hướng đi lên đúng | có |
| V9 Bài tập 10.1(a)(b) | 3-11 | $\tfrac14$; $1$; $\tfrac34$; giá trị $3$ ($\tfrac14$), $0$ ($\tfrac34$); $\operatorname{Var}=\tfrac{27}{16}$ | có (khớp `exercises.md`) |
| V10, F1 Ví dụ 10.8 | 4-04 | $\operatorname{Var}\hat g_b=(12b^2-36b+27)/64$ (khai triển tay từ Bước 1); $\tfrac{27}{64}$, $\tfrac3{16}$, $0$, $\tfrac{147}{64}$; $147/27=5{,}44$ | có |
| V11 Ví dụ 10.9 | 4-04 | $\tfrac38-\tfrac{3\kappa}{16}$; $0$ tại $\kappa=2$ | có |
| V12 Ví dụ 10.10 | 4-05 | ba hàng phương sai đúng từng phân số; vết $1{,}94625$; $1{,}62125$; $0{,}324375$; tỉ số $6$; Bước 3: $0$ và $1$ | có |
| V13 Ví dụ 10.11 | 4-06 | $0{,}05$; $0{,}1225$; $27{,}6225$; $0{,}06$; mô phỏng: $49/100$ | có |
| V14 Ví dụ 10.12 | 4-07 | $4\sqrt{\ln40/2000}=0{,}171788\le0{,}1718$; $11\,804{,}41\to11\,805$ | có |
| V15 Bài tập 10.2(b)(c) | 4-08 | $0{,}225$; $0{,}425-0{,}2$; kì vọng $0{,}25$, mô-men $0{,}55$, phương sai $0{,}4875$ | có |
| V16 Ví dụ 10.13 | 5-03 | $0{,}81$; $-0{,}11$; $0{,}10$, $0{,}17$, $0{,}135$; $0{,}025$; ma trận hai: $0{,}005$, $0{,}07$, $0$, $-0{,}03$ | có |
| V17 Bài tập 10.4(a)(d) | 5-04 | $0{,}7533$; $-0{,}19$; $0{,}15$, $0{,}28$, $0{,}215$; $0{,}015$; $0{,}60$ so $0{,}86$ | có |
| V18 Mệnh đề 10.13, Ví dụ 10.14 | 6-02, 6-04 | năm hàng $w_\lambda$, $L_A$, $L_B$, tổng, $\alpha$ đúng | có |
| V19 Ví dụ 10.15 | ghi chú 6-04 | $v=\tfrac2{2+\lambda}$; $\tfrac29$, $\tfrac89$ | có |
| V20 Ví dụ 10.16 | 6-05 | $\tfrac58$; $\tfrac1{8M}$; $0{,}125$; $0{,}0125$; $0{,}00125$ | có |
| V21 Ví dụ 10.17 | 6-07 | hạ gradient có chiếu từ $w_1=0$: $\eta=1/\sqrt{1000}$ cho hối tiếc $-116{,}967$, $w_{T+1}=1-1{,}05\cdot10^{-7}$; $\eta_t=1/t$ cho $0{,}1876$, $w_{T+1}=\tfrac12$; $\sqrt{1000}=31{,}623$ | có |
| V22 Bài tập 10.5(c) | 6-08 | $\tfrac15$; $\tfrac12$; $\tfrac15$; $\lambda\Omega=\tfrac{4\alpha}{1-\alpha}$ | có |
| V23 Bài tập 10.7(i) | 7-03 | miền $[0,6]$, tỉ số $1{,}5$ | có |
| V24 §12 | 7-04 | $J'(0)=\tfrac12$; $1$, $0$; $\tfrac45$, $\tfrac8{25}$, $\tfrac1{50}$, $\tfrac15$; $-116{,}97$ | có |
| Phụ lục C, REINFORCE | 4-06 | 100 hạt giống, đúng thứ tự rút: bảng $0{,}969/0{,}011$; $0{,}970/0{,}009$; $0{,}509/0{,}498$, $49$; $0{,}969/0{,}009$ | có, từng chữ số |
| Phụ lục C, phát lại | 6-05 | 20 hạt giống: $w_A=0{,}011$; rủi ro A $0{,}624$; $0{,}331$; $0{,}256$; $0{,}252$; rủi ro B $0{,}126$; $0{,}218$; $0{,}248$; $0{,}255$ | có, từng chữ số |
| F1 (SVG) | 4-04 | trục: $b$ 79,48 px/đơn vị, Var 105,4 px/đơn vị; bốn dấu đúng tọa độ (tam giác lệch tâm $\approx2$ px); đường gấp khúc lệch công thức $\le0{,}0013$ | có |
| F2 (SVG) | 6-04 | trục 563,6 và 520 px/đơn vị; năm chấm đúng $(L_A,L_B)$ của bảng; mọi điểm đường cong thỏa $\sqrt{2L_A}+\sqrt{2L_B}=1$ (sai số làm tròn $\le0{,}01$ chỉ ở hai đầu, do căn bậc hai gần $0$); nét đứt từ $(0;\tfrac14)$ đến $(\tfrac14;0)$, tiếp xúc tại $(\tfrac18;\tfrac18)$ vì $L_A+L_B=(w-\tfrac12)^2+\tfrac14$ | có |

Mọi con số trên mặt trang, trong ghi chú diễn giả và trong hai SVG đều đúng. Các phát hiện dưới đây là về điều kiện bị bỏ, cách đọc trên mặt trang và thống nhất với ghi chú.

## 2. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | L10-6-05 | Dòng mô phỏng đặt cạnh kết quả của Ví dụ 10.16 mà không nói mô hình khác; trên cùng mặt trang, $0{,}252$ nhỏ hơn "$\min L_A=\tfrac12$" vừa nêu, và $0{,}624$ trùng gần $\tfrac58$ của ví dụ, nên người đọc hiểu sai cả hai dòng. Ghi chú nêu rõ mô hình khác và giới hạn $0{,}25$, $0{,}125$. | Deck: "Rủi ro cũ giảm về $\tfrac58$ của điểm thỏa hiệp, không về $\min L_A=\tfrac12$." rồi "Mô phỏng (Phụ lục C): rủi ro kiểm tra trên A $0{,}624$ khi tinh chỉnh; $0{,}331$; $0{,}256$; $0{,}252$ với $M=5;\,50;\,1000$." Ghi chú dòng 791: "Mô hình hồi quy của Phụ lục C có rủi ro tổng thể trên A là $\tfrac12(w^2+0{,}25)$ … tiến về giá trị $0{,}25$ của điểm thỏa hiệp, không về $0{,}125$"; dòng 1024: "Mô hình ở đây khác mô hình của Ví dụ 10.16." | Viết dòng mô phỏng: "Mô phỏng (Phụ lục C, hồi quy $y=wx$, rủi ro trên A $\tfrac12(w^2+0{,}25)$): $0{,}624$ khi tinh chỉnh; $0{,}331$; $0{,}256$; $0{,}252$ với $M=5;50;1000$, về $0{,}25$, không về $0{,}125$." Nếu vượt mật độ, bỏ dòng mô phỏng khỏi mặt trang, giữ trong ghi chú diễn giả. |
| trung bình | L10-4-05 | Ví dụ đổi (Ví dụ 10.10, Bước 3) bỏ điều kiện "xác suất chọn ở $s_0$ không phụ thuộc $\theta$". Thiếu điều kiện này, chính sách bảng vẫn có tọa độ $\theta_{s_0}$; tọa độ đó của (i) là $(-2+r_1)(A_0-\tfrac12)\in\{\pm\tfrac12\}$, phương sai $\tfrac14$, nên "phương sai của (i) là $0$" sai. Điều kiện chỉ có trong ghi chú diễn giả. | Deck: "Đổi ví dụ ($r=-2$ ở $s_0$, luôn tới $s_1$): phương sai của (i) là $0$, của (ii) là $1$." Ghi chú dòng 556: "xác suất chọn ở $s_0$ không phụ thuộc $\theta$ … Gradient chỉ có tọa độ $\theta_{s_1}$." | "Đổi ví dụ ($r=-2$ ở $s_0$, luôn tới $s_1$, chỉ có tham số $\theta_{s_1}$): phương sai của (i) là $0$, của (ii) là $1$." |
| nhẹ | L10-6-05 | "Rủi ro cũ giảm về $\tfrac58$" bỏ chữ "kì vọng": $L_A(w_M)$ ngẫu nhiên; ghi chú nói rủi ro cũ kì vọng. | Ghi chú dòng 789: "Rủi ro cũ kì vọng là $\tfrac58+\tfrac1{8M}$; nó giảm về giá trị $\tfrac58$". | "Rủi ro cũ kì vọng $\tfrac58+\tfrac1{8M}$ giảm về $\tfrac58$ …" (gộp với sửa dòng trên). |
| nhẹ | L10-1-01, L10-3-00, L10-7-00 | Luận điểm bìa và hai dòng dẫn nêu điều kiện đủ "chính sách khả vi và môi trường không phụ thuộc tham số" mà không có tập hữu hạn (hoặc điều kiện hàm trội của Nhận xét 10.5). Ví dụ 10.3 cho thấy với tập vô hạn, hai điều kiện đó chưa đủ. Đây là trang tổng quan, nên chỉ nhẹ. | Bìa: "gradient của mục tiêu ước lượng được không chệch nếu chính sách khả vi và môi trường không phụ thuộc tham số". Ghi chú: Định lý 10.4 dưới (MDP) ($\mathcal S$, $\mathcal A$ hữu hạn), Nhận xét 10.5. | Thêm "trên tập hữu hạn trạng thái và hành động" vào câu bìa nếu vừa một câu; dòng dẫn giữ nguyên hoặc thêm "hữu hạn". |
| nhẹ | L10-7-01 | Cột "Giả thiết không được bỏ" ghi "$\mathcal T$ hữu hạn" cho Định lý 10.4; theo Nhận xét 10.5 giả thiết này thay được bằng mật độ, khả vi liên tục và hàm trội, nên nó không phải giả thiết "không được bỏ" mà là giả thiết "không được bỏ mà không thay". | Ghi chú diễn giả 7-01 đã nói đúng; Nhận xét 10.5. | "$\mathcal T$ hữu hạn (hoặc Nhận xét 10.5)". |
| nhẹ | L10-2-03 | "$\mathbb 1[\theta_s>0]$ không khả vi" bỏ "tại $\theta_s=0$" và tên "chính sách tất định"; hàm này khả vi ở mọi $\theta_s\ne0$. | Ghi chú dòng 165: "*Chính sách tất định* … không khả vi tại $\theta_s=0$". | "chính sách tất định $\mathbb 1[\theta_s>0]$ không khả vi tại $\theta_s=0$". |
| nhẹ | L10-1-02 | Phát biểu rút gọn Hệ quả 02.10(b) bỏ (T2) và $\delta\in(0,1)$. Dạng "$\lvert L_S-L_D\rvert\le\sqrt{\ln(2/\delta)/(2m)}$ với xác suất ít nhất $1-\delta$" tương đương khoảng tin cậy của (b), đúng. | Bài 02, Hệ quả 02.10: "**Hàm lỗi.** $\ell$ thỏa (T2) và (T3)"; "**Tham số.** $\delta\in(0,1)$". | "(T1), (T2), (T3) ($\ell\in[0,1]$), $h$ cố định, $\delta\in(0,1)$". |
| nhẹ | L10-3-05 | Dòng "Kỹ thuật." nêu điều kiện "$\mathcal T$ hữu hạn, cố định, $f$ không chứa $\theta$" nhưng thiếu "$\theta\mapsto p_\theta(\tau)$ khả vi", giả thiết thứ ba của Bổ đề 10.3. | Bổ đề 10.3, Giả thiết "Tính khả vi". | "… khi $\mathcal T$ hữu hạn, cố định, $p_\theta(\tau)$ khả vi theo $\theta$, $f$ không chứa $\theta$." |
| nhẹ | L10-6-04 | "giảm $L_A$ thì tăng $L_B$" đúng dọc đường cong $w\in[0,1]$ (hay khi tăng $\lambda$), không đúng với mọi $w$ (ngoài $[0,1]$ cả hai cùng tăng). | Ghi chú dòng 721: "tăng $\lambda$ làm $L_A$ giảm, $L_B$ tăng". | "tăng $\lambda$: $L_A$ giảm, $L_B$ tăng." |
| nhẹ | L10-4-04 (ghi chú diễn giả) | "bước 2 của chứng minh hỏng" dẫn bước của trang ý tưởng 4-03, trong khi ghi chú nói "Bước 1 của chứng minh Hệ quả 10.8 hỏng"; người học đối chiếu ghi chú sẽ thấy lệch số bước. | Ghi chú dòng 538. | "bước 2 của ý tưởng chứng minh (Bước 1 của chứng minh Hệ quả 10.8) hỏng". |
| nhẹ | L10-2-04 (ghi chú diễn giả) | Câu "đây là quy tắc nhân xác suất của Bài 09 (Mệnh đề 09.3) cho chuỗi trạng thái và hành động" không có trong ghi chú Bài 10. Nội dung đúng: quỹ đạo là một chuỗi mà mỗi thừa số $\mu_0$, $\pi_\theta(a_t\mid s_t)$, $P(s_{t+1}\mid s_t,a_t)$ là xác suất có điều kiện theo tiền tố, nên Mệnh đề 09.3(c) áp dụng. | Ghi chú dòng 183 chỉ nói "Lấy tổng lần lượt theo $a_{H-1}$, $s_{H-1}$, …, $s_0$". | Giữ nếu điều phối viên chấp nhận như một "Nhắc lại" đúng; nếu không, bỏ. |
| nhẹ | L10-7-02 (ghi chú diễn giả) | "$m=1000$ lượt cho bán kính $0{,}1718$" thiếu "với MDP của Ví dụ 10.2" (miền $[0,4]$); bán kính phụ thuộc miền. | Ví dụ 10.12. | "Với chính sách cố định trên MDP của Ví dụ 10.2, …". |
| nhẹ | F2 (`danh-doi-hai-nhiem-vu.svg`) | Nhãn trục viết chữ thường "L_A", "L_B" với dấu gạch dưới, khác kí hiệu $L_A$, $L_B$ của mặt trang và của F1 (dùng "b*", "Var"). | Nhãn: `L_A (nhiệm vụ cũ)`, `L_B (nhiệm vụ mới)`. | Dùng `<tspan>` chỉ số dưới (`L<tspan baseline-shift="sub">A</tspan>`), như tiền lệ hình các bài trước nếu có. |

Không có phát hiện chặn bàn giao.

## 3. Đối chiếu các phát biểu với ghi chú

- **Bổ đề 10.3** (3-01): ba giả thiết ($\mathcal T$ hữu hạn, không phụ thuộc $\theta$; $\Theta$ mở, $p_\theta$ hàm xác suất; khả vi), "đồng nhất thức, mọi $\theta$", (a) cả hai trường hợp trên và ngoài giá, (b): khớp. Dòng chứng minh (b) đúng.
- **Định lý 10.4** (3-03, 3-04): (MDP), (Π); $J$ khả vi; "ước lượng không chệch"; "hiệp phương sai chia cho $m$" cho $m$ lượt độc lập; ba bước ý tưởng gắn đúng giả thiết (hữu hạn ở bước 1, Bổ đề 10.3(a) ở bước 2, $\mu_0$, $P$ không phụ thuộc $\theta$ ở bước 3); dòng "Khi $P$ phụ thuộc $\theta$: bước 3 còn số hạng $\nabla\ln P$" khớp Ví dụ 10.6 ($-0{,}25$ so với $0{,}125$).
- **Luật chuyển không phụ thuộc tham số**: có ở 2-03 ((MDP)), 3-04 bước 3, 3-08, 7-01, 7-02, dòng dẫn 3-00 và bìa.
- **Nhận xét 10.5** (3-05, ghi chú diễn giả): phần thưởng bị chặn; mật độ theo độ đo nền không phụ thuộc $\theta$; khả vi liên tục; hàm trội $\Lambda$ cho $\lvert R\rvert\lVert\nabla p_\theta\rVert$; chính sách Gauss; Ví dụ 10.3 vi phạm điều kiện khả vi: khớp.
- **Mệnh đề 10.7** (4-01): "như Định lý 10.4", đồng nhất thức, (a) với $t'<t$, (b): khớp; "phác thảo" và Phụ lục B nêu trong ghi chú diễn giả.
- **Hệ quả 10.8** (4-02, 4-03): giá trị nền là hàm của lịch sử $\mathcal F_t$, không phụ thuộc $A_t$ hay biến sau; đồng nhất thức: khớp. Điều kiện được giữ ở 7-01 ("$b_t$ là hàm của $\mathcal F_t$") và 7-02 ("Giá trị nền là hàm của lịch sử chỉ đổi phương sai"); phát hiện N1 của cổng duyệt đã được sửa.
- **Phương sai**: 4-04 (bốn giá trị nền, $b^*$, "hơn năm lần" $=5{,}44$), 4-05 (vết, "sáu lần"), 4-06 ("khoảng $225$ lần" ở ghi chú diễn giả, $27{,}6225/0{,}1225=225{,}5$): đúng; xem phát hiện trung bình ở 4-05.
- **(PT)** (4-06): đủ ba vế như §2 của ghi chú.
- **(TK)** (5-01): $S^{(k)}\sim D_k^{m_k}$, độc lập với nhau: khớp.
- **Mệnh đề 10.13** (6-02, 6-03): giả thiết, "tất định", (a)–(d), dấu bằng chỉ ở bất đẳng thức sau: khớp; "Kỹ thuật." $\tfrac\lambda2w^2=\lambda L_A$ đúng điều kiện tâm $w^{(1)}$ và độ cong $1$.
- **Nhận xét 10.14** (ghi chú diễn giả 6-04): EWC dùng đường chéo của ma trận Fisher, "đọc thêm" ngầm qua "Phần đọc thêm": khớp.
- **Nhận xét 10.16** (6-06, 7-01): (C) cho mọi $\ell(\cdot,z)$, $w_1$ tất định, chiếu, $\lVert v_t\rVert\le G$, "tất định, mọi dãy, mọi $u$ với $\lVert w_1-u\rVert\le R$", vế phải và $\eta=R/(G\sqrt T)$: khớp; "phác thảo" trong ghi chú diễn giả.
- **$R$ hai nghĩa**: 6-06 có "($R$: bán kính)"; 7-01 có $\lVert w_1-u\rVert\le R$ ở hàng Nhận xét 10.16. Đạt.
- **Quên và hối tiếc**: 5-02 (độ quên $\ge0$, cực đại tới hàng $K$), 5-03 (quy ước tới hàng $K-1$ cho số âm), 6-07 ("cận hối tiếc tĩnh không chặn độ quên"), 7-02: khớp §9 và Ví dụ 10.17.
- **Mệnh đề 08.12** (3-10, "Nhắc lại:"): ba điều kiện như ghi chú Bài 10 dòng 433–435, "theo kì vọng" như Bài 08; Bài 08 còn cần $W=\mathbb R^p$ (đúng với $\Theta$ là cả không gian ở Thuật toán 10.6) và tính khả tích. Chấp nhận được vì deck theo ghi chú Bài 10.
- **"Cần" so với "đủ"**: 1-02 "Định lý 05.14 cần oracle không chệch và (C)" (cần, đúng); 3-09 "Định lý 05.14 cần $-J$ lồi" (cần, đúng); 7-02 "(C) sai vì $-J$ không lồi" đúng với $\Theta$ là cả không gian và $J$ bị chặn, khác hằng (một hàm lồi bị chặn trên trên cả một đường thẳng thì hằng trên đường đó); "khi" ở 6-01 (xung đột) không đổi thành "chỉ khi"; bìa và dòng dẫn nêu điều kiện đủ, xem phát hiện nhẹ.
- **Bài tập trên mặt trang** (3-11, 4-08, 5-04, 6-08, 7-03): đề, dữ liệu và lời giải khớp `exercises.md` từng số.

## 4. Bảng thống nhất trang → khối ghi chú

| Trang | Khối ghi chú | Kí hiệu, nhãn, số hiệu, dữ liệu | Lệch |
|---|---|---|---|
| 1-01 | đoạn mở, §10 | Định lý 10.4, Mệnh đề 10.13 | luận điểm thiếu "hữu hạn" (nhẹ) |
| 1-02 | Kiến thức tiên quyết, câu ôn nhanh | (T1), (T3), (C), Hệ quả 02.10(b), Định lý 05.14 | thiếu (T2), $\delta$ (nhẹ) |
| 1-03 | Mục tiêu học tập | năm mục tiêu | — |
| 1-04 | §4–§9 | sáu mạch | — |
| 1-05 | câu hỏi trung tâm | — | — |
| 1-06 | Câu hỏi mở đầu | $0{,}2+0{,}6q$, $L_A$, $L_B$ | — |
| 2-01 | §1 | (T1), $K$, $D_k$ | — |
| 2-02 | Ví dụ 10.1 | $r(1)=3$, $r(0)=1$, $\theta=\ln3$ | — |
| 2-03 | §2 (MDP), (Π); Định nghĩa 10.1 | $(\mathcal S,\mathcal A,\mu_0,P,r,H)$ | "tại $\theta_s=0$" (nhẹ) |
| 2-04 | Định nghĩa 10.2 | $\tau$, $\mathcal T$, $p_\theta$, $R(\tau)$, $J$ | Mệnh đề 09.3 trong ghi chú diễn giả (nhẹ) |
| 2-05 | Ví dụ 10.2 | bảng tám quỹ đạo | — |
| 3-01 | §5, Bổ đề 10.3 | gradient log, giá | — |
| 3-02 | Ví dụ 10.3 | đều trên $[0,\theta]$ | — |
| 3-03 | Định lý 10.4 | $\hat g(\tau)$ | — |
| 3-04 | chứng minh Định lý 10.4 | ba bước | — |
| 3-05 | Nhận xét 10.5, Phụ lục A | kỹ thuật | thiếu "khả vi" (nhẹ) |
| 3-06 | Ví dụ 10.4 | $\pm0{,}75$ | — |
| 3-07 | Ví dụ 10.5 | $(-0{,}025;0{,}25;-0{,}125)$ | — |
| 3-08 | Ví dụ 10.6 | $0{,}125$, $-0{,}25$ | — |
| 3-09 | Thuật toán 10.6 và đoạn sau | $\eta_j$, $\theta_j$, $\tau_j$ | — |
| 3-10 | Ví dụ 10.7; Mệnh đề 08.12 | $q=0{,}375$, $\ln0{,}6$ | — |
| 3-11 | Bài tập 10.1(a)(b) | $r(1)=4$, $r(0)=0$, $\theta=-\ln3$ | — |
| 4-01 | §6, Mệnh đề 10.7 | $R_{\ge t}$, $\mathcal F_t$ | — |
| 4-02 | Hệ quả 10.8 | $b_t(\mathcal F_t)$ | — |
| 4-03 | chứng minh Mệnh đề 10.7, Hệ quả 10.8; Phụ lục B | ba bước | — |
| 4-04 | Ví dụ 10.8, 10.9; Nhận xét 10.9 | bảng bốn $b$, F1 | số bước trong ghi chú diễn giả (nhẹ) |
| 4-05 | Ví dụ 10.10 | bảng phương sai, vết | thiếu điều kiện ở ví dụ đổi (trung bình) |
| 4-06 | §2 (PT), khối ứng dụng §3, Ví dụ 10.11, Phụ lục C | $c$, $X$, $49/100$ | — |
| 4-07 | Ví dụ 10.12 | $[0,4]$, $0{,}1718$, $11\,805$ | — |
| 4-08 | Bài tập 10.2(b)(c) | $0{,}225$, $0{,}4875$ | — |
| 5-01 | §7, Định nghĩa 10.10 | $M$, (TK), $w^{(k)}$ | — |
| 5-02 | Định nghĩa 10.11 | $\mathrm{acc}_{k,i}$, $\mathrm{acc}^\circ_i$ | — |
| 5-03 | Ví dụ 10.13 | ma trận ba nhiệm vụ | — |
| 5-04 | Bài tập 10.4(a)(d) | ma trận của bài tập | — |
| 6-01 | §8 đoạn mở, Định nghĩa 10.12 | $\alpha$, $\lambda$, $\Omega$, $L_{\mathrm{buf}}$ | — |
| 6-02 | Mệnh đề 10.13 | $w_\lambda$ | — |
| 6-03 | chứng minh Mệnh đề 10.13 | bốn bước | — |
| 6-04 | Ví dụ 10.14, Nhận xét 10.14, Ví dụ 10.15 | bảng năm $\lambda$, F2 | "giảm $L_A$ thì tăng $L_B$" (nhẹ); nhãn trục F2 (nhẹ) |
| 6-05 | Ví dụ 10.16, Phụ lục C | $\tfrac1{8M}$, mô phỏng | mô hình mô phỏng không nêu (nghiêm trọng); "kì vọng" (nhẹ) |
| 6-06 | §9, Định nghĩa 10.15, Nhận xét 10.16 | $\mathrm{Regret}_T(u)$, $R$, $G$ | — |
| 6-07 | Ví dụ 10.17, Nhận xét 10.17 | $-116{,}97$, $0{,}19$ | — |
| 6-08 | Bài tập 10.5(c) | $L_A=2w^2$ | — |
| 7-01 | §10 | bốn hàng | "$\mathcal T$ hữu hạn" (nhẹ) |
| 7-02 | §10, Phụ lục D | năm dòng | ghi chú diễn giả thiếu MDP (nhẹ) |
| 7-03 | Bài tập 10.7(i) | $[Hr_{\min},Hr_{\max}]$ | — |
| 7-04 | §12 (a), (b), (d), (e) | bốn câu | — |
| 7-05 | §11 | `Mục | Bài tập` | — |
| 7-06 | §13, §12(f) | nguồn | — |

Các trang tiêu đề mạch (2-00 đến 7-00) không có kết quả riêng; ghi chú diễn giả của chúng đúng với §1, §4–§10.

## 5. Đề xuất sửa ghi chú

Không có lỗi toán học trong ghi chú hay `exercises.md` ở các khối deck dùng. Hai điểm cho tác giả, không gấp:

- Ghi chú dòng 418: "Định nghĩa 05.10 và Định lý 05.14 cần $-J$ lồi" đúng theo Bài 05 (Định nghĩa 05.10 giả sử $F$ lồi), nhưng người đọc dễ hiểu là chỉ Định lý 05.14 cần; có thể viết "Định nghĩa 05.10 giả sử hàm mục tiêu lồi, và Định lý 05.14 cần (C)".
- §2 và Nhận xét 10.16 dùng $R$ cho cả tổng phần thưởng và bán kính (cổng duyệt đã ghi đề xuất này).

## Kết luận

**đạt khi sửa** — 0 chặn bàn giao, 1 nghiêm trọng (L10-6-05), 1 trung bình (L10-4-05), 11 nhẹ. Mọi con số, F1, F2 và cả hai bảng Phụ lục C tính lại khớp.
