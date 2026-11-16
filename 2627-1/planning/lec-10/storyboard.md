# Storyboard — Bộ trang chiếu Bài 10: Gradient chính sách và học liên tục

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-11-16 bởi tác tử lập storyboard. Nguồn nội dung duy nhất: `materials/lec-10/lecture-note.md` (bản hiện hành); bài tập: `materials/lec-10/exercises.md`. Quy định: `CLAUDE.md` § Slide decks, `common-brief.md` (gồm "Các quy định dễ sót" và các bài học từ duyệt deck 01–07), `brief-storyboard.md`, `../rl-plan/CLAUDE.md` § Deck structure and content, nhật ký yêu cầu 2026-11-13 hàng 1–5, quyết định của điều phối viên trong `lec-0{1,…,9}/review-log.md` § Bộ trang chiếu, ba báo cáo `lec-0{6,7,8}/reviews/deck-storyboard-gate.md`. Khuôn bố cục theo storyboard Bài 08 và Bài 09; deck Bài 05 và Bài 06 làm mẫu markup (`<ol>` cho bước chứng minh, giả thiết trong ngoặc đầu mục; tiêu đề trang kỹ thuật là tên kỹ thuật). Mọi mã trang có dạng `L10-k-mm`; trong bảng viết gọn `k-mm`.

Số âm tiết trong tệp này đếm bằng script (mục 15) theo cách của `deck_lint.py`: token cách nhau bởi khoảng trắng có chữ cái hoặc chữ số; số viết trong câu có tính; chữ trong ô bảng có tính, số trong bảng và KaTeX không tính; mỗi công thức hiển thị là một dòng. Điều phối viên đếm lại trên deck.

Nguồn ngoài ghi chú: không đọc PDF trong vai này (bản giao việc chỉ cho phép ghi chú và `exercises.md`). Các mục của Sutton và Barto (2018), UML và Kirkpatrick và cộng sự (2017) trên trang "Tài liệu tham khảo" lấy từ §13 của ghi chú; số trang PDF lấy từ `outline.md` §7 (Sutton–Barto §13.1–13.3 tr. 343–350, §13.4 tr. 351–352, §2.8 tr. 57–59; UML §21.1–21.3 tr. 288–301; Kirkpatrick và cộng sự, arXiv:1612.00796v2 tr. 1–4).

## 1. Tên tệp và tiêu đề

- **Tệp deck:** `2627-1/lecture-10-gradient-chinh-sach-hoc-lien-tuc.html` (slug ASCII từ tên bài "Gradient chính sách và học liên tục").
- **Tiêu đề deck (h1 trang bìa):** "Gradient chính sách và học liên tục" (đúng tên bài của ghi chú).
- **`<title>`:** "Bài 10: Gradient chính sách và học liên tục".
- **Chân trang:** "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài 10".
- **Liên kết viewer:** `material-viewer.html?doc=materials/lec-10/lecture-note.md&deck=lecture-10-gradient-chinh-sach-hoc-lien-tuc.html` và `…exercises.md&deck=…`.
- **Màn hẹp:** chế độ đọc của `lecture-course.css` (`.slides` bọc trong `div.lecture-viewport`, script màn hẹp của `lecture-template.html`); các bảng (2-05, 4-04, 4-05, 5-03, 5-04, 6-04, 6-07, 7-01, 7-05) cuộn ngang tại chỗ nhờ quy tắc `table` của `lecture-course.css` ở màn hẹp; không có lớp `.table-scroll` (sửa theo cổng duyệt L17 và đối chiếu deck, mục 16).
- **Trang cuối deck Bài 09** (7-06 của storyboard Bài 09) nhận liên kết tới tệp này khi deck Bài 10 xong; dòng chữ "Bài 10: Gradient chính sách và học liên tục" ở đó đổi thành liên kết.

## 2. Khung lý thuyết chung

**Vấn đề trung tâm (hộp "Vấn đề trung tâm", bằng lời, ≤ 30 âm tiết).** "**Câu hỏi:** điều gì thay đổi khi thuật toán học tương tác với môi trường và khi nhiệm vụ thay đổi theo thời gian?" (câu hỏi trung tâm của ghi chú, đoạn mở đầu dòng 5; 24 âm tiết theo script, kể cả nhãn). Câu hỏi thật, không gợi câu trả lời; trang 7-02 trả lời cho cả bài.

**Luận điểm (trang bìa, một câu, có điều kiện, bằng lời, ≤ 50 âm tiết).** "Khi dữ liệu do chính sách sinh ra, gradient của mục tiêu ước lượng được không chệch nếu chính sách khả vi và môi trường không phụ thuộc tham số, còn khi nhiệm vụ thay đổi, cần nêu trước giao thức và ma trận đánh giá." (Định lý 10.4, (MDP), (Π); Định nghĩa 10.10, 10.11; §10 đoạn 1; 46 âm tiết theo script.) Điều kiện nằm ở "nếu chính sách khả vi và môi trường không phụ thuộc tham số" ((Π), (MDP)) và "khi nhiệm vụ thay đổi". Câu không nói gì về hội tụ của REINFORCE (ghi chú không nêu khẳng định hội tụ nào, §13) hay về cận cho độ quên; ghi chú diễn giả 1-01 nêu hai giới hạn này cùng đánh đổi của Mệnh đề 10.13.

**Trọng tâm trực quan của deck.** Năm chỗ, theo bản giao việc của điều phối viên và các mục của ghi chú:
1. **Ước lượng gradient chính sách không chệch nhờ gradient log** (1-06, 3-01, 3-03, 3-04, 3-05, 3-06, 3-07, 3-11): đạo hàm của trung bình các phần thưởng đã thu bằng $0$ (câu hỏi mở đầu), còn $\nabla J=\mathbb E[R(\tau)\sum_t\nabla\ln\pi_\theta(A_t\mid S_t)]$ (Định lý 10.4); chỉ thừa số chính sách phụ thuộc $\theta$, nên không cần $\mu_0$, $P$, $r$. Số: bandit $\pm0{,}75$ có kì vọng $\tfrac38$ (Ví dụ 10.4); MDP hai bước $(-0{,}025;\,0{,}25;\,-0{,}125)$ khớp sai phân hữu hạn (Ví dụ 10.5).
2. **Điều kiện đổi chỗ đạo hàm và kì vọng; bỏ giả thiết thì hỏng** (3-02, 3-05, 3-08): giá phụ thuộc tham số cho $\mathbb E[A\,\partial_\theta\ln p_\theta]=-\tfrac12$ ngược dấu $J'=\tfrac12$ (Ví dụ 10.3); luật chuyển phụ thuộc $\theta$ cho $-0{,}25$ ngược dấu $0{,}125$ (Ví dụ 10.6). Trường hợp vô hạn: "Nhắc lại:" kỹ thuật "Đổi chỗ đạo hàm và kì vọng" của Bài 09 (`L09-6-04`) cùng Nhận xét 10.5.
3. **Phương sai và giá trị nền** (4-01 đến 4-06): cùng kì vọng $\tfrac38$, phương sai $\tfrac{27}{64}$, $\tfrac3{16}$, $0$, $\tfrac{147}{64}$ theo $b$ (Ví dụ 10.8, hình F1); giá trị nền phụ thuộc hành động gây chệch (Ví dụ 10.9); giá trị nền theo trạng thái giảm vết hiệp phương sai sáu lần, còn bỏ phần thưởng trước bước $t$ có thể tăng phương sai từ $0$ lên $1$ (Ví dụ 10.10); dịch phần thưởng $c=10$ nhân phương sai khoảng $225$ lần (Ví dụ 10.11). Thuật ngữ "giá trị nền" theo `thuat-ngu.md` (dòng 465: "đường cơ sở" chỉ dùng cho phương pháp đối chứng trong thực nghiệm).
4. **Dữ liệu i.i.d. và dữ liệu do chính sách sinh ra** (1-06, 2-01, 2-05, 3-09, 4-07, 7-02, 7-03): tham số ở cập nhật $j$ phụ thuộc các lượt trước nên (T1) không đúng (§1); xác suất tới $s_1$ bằng $0{,}2+0{,}6\,\pi_\theta(1\mid s_0)$ (Ví dụ 10.2); với chính sách cố định, các lượt thỏa (T1) và Hoeffding cho bán kính $0{,}1718$ với xác suất ít nhất $0{,}95$ (Ví dụ 10.12); $-J$ không lồi, điểm dừng có thể là cực tiểu (Ví dụ 10.7), nên Định lý 05.14 không áp dụng. Deck không chuyển kết quả lồi hay i.i.d. sang học tăng cường: hai chỗ duy nhất có bảo đảm là Ví dụ 10.12 (chính sách cố định) và điều kiện của Mệnh đề 08.12 nêu ở Ví dụ 10.7, đúng như ghi chú.
5. **Học liên tục: quên, đánh đổi, hối tiếc** (5-01 đến 6-07): ma trận đánh giá và độ quên (Ví dụ 10.13: $0{,}81$; $-0{,}11$; $0{,}135$; độ quên âm khi đổi quy ước); hai nhiệm vụ xung đột buộc $L_A+L_B\ge\tfrac14$ (Mệnh đề 10.13, hình F2); chính quy hóa tham số và phát lại cho cùng điểm cực tiểu khi $\alpha=\lambda/(1+\lambda)$; bộ đệm hữu hạn thêm $\tfrac1{8M}$ (Ví dụ 10.16); hối tiếc $-116{,}97$ đi cùng $L_A\approx\tfrac12$ (Ví dụ 10.17).

**Đối tượng và kí hiệu chung** (ghi chú §1–§2):
- Phần A: $\mathcal S$, $\mathcal A$, $H$, $\mu_0$, $P(s'\mid s,a)$, $r(s,a)$, $r_{\min}$, $r_{\max}$; $S_t$, $A_t$, $r_t$; $\theta\in\Theta$, $\pi_\theta(a\mid s)$, $\theta_s$ (chính sách bảng); $\tau$, $\mathcal T$, $p_\theta(\tau)$, $R(\tau)$, $J(\theta)$; $\hat g$, $\hat g_j$, $\eta_j$, $T$; $R_{\ge t}$, $\mathcal F_t$, $b_t(\mathcal F_t)$, $\hat g_b$, $b^*$;
- Phần B: $K$, $D_k$, $L_k=L_{D_k}$, $S^{(k)}$, $m_k$, $M$, $w^{(k)}$, $\mathrm{acc}_{k,i}$, $\mathrm{acc}^\circ_i$; $L_A$, $L_B$, $\lambda$, $\Omega$, $\alpha$, $w_\lambda$, $\mathcal B$, $L_{\mathrm{buf}}$, $\bar Z_M$; $z_t$, $w_t$, $u$, $\mathrm{Regret}_T(u)$, $v_t$, $G$, $R$ (bán kính, như Bài 05);
- cục bộ của ví dụ: $q$ (câu hỏi mở đầu, Ví dụ 10.6, 10.7); $c$, $X$ (Ví dụ 10.11); $\kappa$ (Ví dụ 10.9).

Lưu ý kí hiệu: $R$ có hai nghĩa trong ghi chú, $R(\tau)$ (tổng phần thưởng, Phần A) và $R$ (bán kính, Nhận xét 10.16, Ví dụ 10.17). Hai nghĩa ở hai mạch khác nhau; trang 6-06 viết "$\lVert w_1-u\rVert\le R$" ngay ở dòng giả thiết (mục 11, điểm 12).

**Giả thiết** (ghi chú §2, danh sách nhãn đậm): (MDP) môi trường; (PT) phần thưởng ngẫu nhiên; (Π) chính sách khả vi; (T1), (T2) của Bài 01; (TK) lấy mẫu theo nhiệm vụ; (C) của Bài 05. "Không kết quả nào của Phần A giả sử mục tiêu là hàm lõm." Deck nêu (T1), (T3), (C) bằng "Nhắc lại:" ở 1-02; (MDP), (Π), (PT) ở 2-03 (trang Định nghĩa 10.1, nơi ghi chú viết "Môi trường và họ chính sách của Định nghĩa 10.1 thỏa (MDP) và (Π)"); (TK) ở 5-01; (T2) chỉ ở ghi chú diễn giả 5-01 (mặt trang không dùng nhãn này).

**Chuỗi định nghĩa → kết quả → phương pháp.**
1. Câu hỏi mở đầu: robot (xác suất tới $s_1$ bằng $0{,}2+0{,}6q$: $0{,}5$; $0{,}74$) và mô hình học A rồi B ($L_A$ từ $0$ lên $\tfrac12$).
2. Thiết lập bảy thành phần cho Phần A và Phần B, bảng nguồn ngẫu nhiên (§1) → kí hiệu, giả thiết (§2) → Ví dụ 10.1 (bandit, $J'(\ln3)=\tfrac38$), khối ứng dụng hệ thống đề xuất (§3) → Định nghĩa 10.1 (MDP, chính sách bảng, chính sách tất định) → Định nghĩa 10.2 (quỹ đạo, $p_\theta$, $R$, $J$) → Ví dụ 10.2 (MDP hai bước, $J(0)=1{,}75$) (§4).
3. Gradient log, giá → Bổ đề 10.3 → Ví dụ 10.3 (giá phụ thuộc tham số) → Định lý 10.4 → Nhận xét 10.5 (tập quỹ đạo vô hạn, chính sách Gauss) → Ví dụ 10.4 → Ví dụ 10.5 → Ví dụ 10.6 (luật chuyển phụ thuộc tham số) → Thuật toán 10.6 (REINFORCE) và đoạn oracle → Ví dụ 10.7 (điểm dừng cực tiểu) (§5).
4. $R_{\ge t}$, $\mathcal F_t$ → Mệnh đề 10.7 → Hệ quả 10.8 → Ví dụ 10.8 → Ví dụ 10.9 → Ví dụ 10.10 → Nhận xét 10.9 → Ví dụ 10.11 → Ví dụ 10.12 (§6).
5. Định nghĩa 10.10 (giao thức) → Định nghĩa 10.11 (ma trận đánh giá, bốn độ đo) → Ví dụ 10.13 (§7).
6. Xung đột → Định nghĩa 10.12 (phát lại, chính quy hóa tham số, tinh chỉnh) → Mệnh đề 10.13 → đánh đổi bền vững–mềm dẻo → Ví dụ 10.14 → Nhận xét 10.14 (đọc thêm) → Ví dụ 10.15 → Ví dụ 10.16 (§8) → Định nghĩa 10.15 (học trực tuyến, hối tiếc tĩnh) → Nhận xét 10.16 → Nhận xét 10.17 → Ví dụ 10.17 (§9).

**Loại bảo đảm của từng kết quả** (§10 đoạn 2 của ghi chú): đồng nhất thức: Bổ đề 10.3, Định lý 10.4, Mệnh đề 10.7, Hệ quả 10.8 (và Nhận xét 10.5, 10.9(i)); tất định: Mệnh đề 10.13, Nhận xét 10.16; với xác suất cao: Ví dụ 10.12, cho một chính sách cố định trước khi chạy. Mức chứng minh: Bổ đề 10.3, Định lý 10.4, Hệ quả 10.8, Mệnh đề 10.13, Nhận xét 10.5 *chứng minh đầy đủ*; Mệnh đề 10.7, Nhận xét 10.16 *phác thảo* (chi tiết Mệnh đề 10.7 ở Phụ lục B); Nhận xét 10.14 *đọc thêm*. Ghi chú diễn giả của mỗi trang kết quả nêu mức chứng minh.

**Giới hạn áp dụng** (ghi chú §10): phương sai cao (giá trị nền tùy ý có thể tăng phương sai, Ví dụ 10.8; $c=10$ nhân phương sai khoảng $225$ lần, Ví dụ 10.11); mục tiêu không lõm (Ví dụ 10.7); luật chuyển phụ thuộc tham số làm ước lượng ngược dấu (Ví dụ 10.6); độ quên phụ thuộc quy ước (Ví dụ 10.13); phát lại hữu hạn thêm $\tfrac1{8M}$ (Ví dụ 10.16); hối tiếc âm đi cùng rủi ro cuối $\tfrac12$ (Ví dụ 10.17). Phụ lục A vào trang 3-05 (điều kiện hàm trội, chính sách Gauss ở ghi chú diễn giả); Phụ lục B vào trang 4-03; Phụ lục C vào trang 4-06 và 6-05; Phụ lục D vào trang 7-02 và 7-06.

## 3. Bảng mạch

Bảy mạch theo đúng thứ tự các mục của ghi chú; mỗi mạch ứng với các mục liên tiếp. Mạch 2 gộp §1–§4 (thiết lập, kí hiệu và giả thiết, ví dụ xuyên suốt, MDP và mục tiêu): bốn mục cùng trả lời "dữ liệu nào, mục tiêu nào". Mạch 5 (§7) tách khỏi mạch 6 (§8–§9): §7 định nghĩa bài toán và cách đo; §8–§9 trả lời câu hỏi "tham số nào tốt trên mọi nhiệm vụ cùng lúc", với một kết quả chính và một trang ý tưởng chứng minh. §9 (học trực tuyến) gộp vào mạch 6 vì Ví dụ 10.17 đo độ quên trên chính hai nhiệm vụ A, B của §8; tách thành mạch riêng làm deck có tám mạch. Bảng đối chiếu trang → khối ghi chú ở mục 12.

| N | Tên mạch | Mục ghi chú | Chức năng | Đầu vào | Đầu ra | `strand-lead` (âm tiết) | Từ khóa | Trang | Phút |
|---|---|---|---|---|---|---|---|---:|---:|
| 1 | Mở đầu | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết | Bìa, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, ví dụ dẫn nhập | Bài 01: (T1), rủi ro; Bài 02: Hệ quả 02.10; Bài 05: (C), oracle; Bài 09: gradient log, đổi chỗ đạo hàm và kì vọng | Câu hỏi: dữ liệu của robot và của mô hình học A rồi B khác $S\sim D^m$ ở điểm nào | (không có trang tiêu đề mạch) | — | 6 | 10 |
| 2 | Quá trình quyết định Markov và mục tiêu của chính sách | §1–§4 | Thiết lập hai phần, bảng nguồn ngẫu nhiên; Ví dụ 10.1; Định nghĩa 10.1 với (MDP), (Π), (PT); Định nghĩa 10.2; Ví dụ 10.2 | dữ liệu của robot phụ thuộc $q$ (1-06) | $J(\theta)=\sum_\tau p_\theta(\tau)R(\tau)$; phân bố dữ liệu phụ thuộc $\theta$, $R$ thì không; tác tử không biết $\mu_0$, $P$, $r$ | "Robot chọn hành động theo xác suất đang học, nên phân bố của dữ liệu đổi khi xác suất đó đổi." (cổng duyệt L3) | tác tử · chính sách · quá trình quyết định Markov · quỹ đạo · tổng phần thưởng | 6 | 15 |
| 3 | Gradient chính sách và thuật toán REINFORCE | §5 | Bổ đề 10.3; Ví dụ 10.3; Định lý 10.4 (trực quan, phát biểu) và ý tưởng chứng minh; trang kỹ thuật "Đạo hàm của kì vọng qua gradient log" (gồm Nhận xét 10.5); Ví dụ 10.4, 10.5, 10.6; Thuật toán 10.6; Ví dụ 10.7; Bài tập 10.1(a), (b) | $J$ không tính được bằng công thức (2-05) | $\nabla J=\mathbb E\hat g$ dưới (MDP), (Π); REINFORCE là SGD đi lên với oracle không chệch; thiếu (C) | "Khi môi trường không phụ thuộc tham số, gradient của mục tiêu là kì vọng của một đại lượng tính được trên quỹ đạo." (24; thêm điều kiện, mục 16) | gradient log · gradient chính sách · ước lượng không chệch · REINFORCE · điểm dừng | 12 | 30 |
| 4 | Giá trị nền và phương sai của ước lượng gradient | §6 | Mệnh đề 10.7; Hệ quả 10.8; ý tưởng chứng minh chung; Ví dụ 10.8 (hình F1) và 10.9; Ví dụ 10.10; Ví dụ 10.11; Ví dụ 10.12; Bài tập 10.2(b), (c) | ước lượng $\pm0{,}75$ quanh $\tfrac38$ (3-06) | các ước lượng cùng kì vọng; giá trị nền là hàm của lịch sử; phương sai tăng hay giảm tùy bài toán; cận Hoeffding chỉ cho chính sách cố định | "Trừ một giá trị nền biết trước hành động không đổi kì vọng của ước lượng nhưng đổi phương sai." (cổng duyệt L3) | tổng phần thưởng từ bước $t$ · lịch sử · giá trị nền · phương sai · chính sách cố định | 9 | 24 |
| 5 | Giao thức học liên tục và ma trận đánh giá | §7 | Định nghĩa 10.10 với (TK); Định nghĩa 10.11; Ví dụ 10.13; Bài tập 10.4(a), (d) | mô hình học A rồi B (1-06) | bài toán xác định bởi giao thức; bốn độ đo; độ quên phụ thuộc quy ước | "Một bài toán học liên tục gồm dãy nhiệm vụ, giới hạn bộ nhớ và một ma trận đánh giá." (20) | nhiệm vụ · ngân sách bộ nhớ · ma trận đánh giá · chuyển đổi ngược · độ quên | 5 | 12 |
| 6 | Hai nhiệm vụ xung đột và hối tiếc | §8–§9 | Định nghĩa 10.12; Mệnh đề 10.13 (trực quan, phát biểu) và ý tưởng chứng minh; Ví dụ 10.14 (hình F2); Ví dụ 10.16; Định nghĩa 10.15 và Nhận xét 10.16; Ví dụ 10.17; Bài tập 10.5(c) | ma trận đánh giá không chỉ ra tham số tốt cho mọi nhiệm vụ (5-03) | $L_A+L_B\ge\tfrac14$; $\lambda$, $\alpha$ chọn một điểm trên đánh đổi; bộ đệm thêm $\tfrac1{8M}$; hối tiếc tĩnh không chặn độ quên | "Hai nhiệm vụ không có chung điểm cực tiểu buộc mọi phương pháp chọn một điểm thỏa hiệp." (18) | xung đột · chính quy hóa tham số · phát lại · đánh đổi bền vững–mềm dẻo · hối tiếc tĩnh | 9 | 20 |
| 7 | Tổng kết | §10–§13, Phụ lục D | Bảng kết quả, trả lời vấn đề trung tâm, bài tập tổng hợp (Bài tập 10.7(i)), tự kiểm tra, bài tập về nhà, tài liệu, dòng khép học phần | mọi kết quả | Bốn bài toán của học phần khác nhau ở quá trình sinh dữ liệu và giả thiết cần đổi | "Khi môi trường không phụ thuộc tham số, gradient ước lượng được không chệch; nhiệm vụ thay đổi cần một giao thức nêu trước." (cổng duyệt T2) | — | 7 | 9 |
| | **Tổng** | | | | | | | **54** | **120** |

Số trang (54) vượt mục tiêu 45–52 và dưới trần 55. Lý do (ghi vào `review-log.md` nếu điều phối viên chấp nhận): năm kết quả chính có trang phát biểu (Bổ đề 10.3, Định lý 10.4, Mệnh đề 10.7, Hệ quả 10.8, Mệnh đề 10.13), ba trang "Ý tưởng chứng minh" riêng (Định lý 10.4; Mệnh đề 10.7 cùng Hệ quả 10.8; Mệnh đề 10.13), một trang "Kỹ thuật." riêng, mười bốn trong mười bảy ví dụ đánh số của ghi chú (mười hai ví dụ có trang, Ví dụ 10.1 và 10.9 chung trang với khối khác), sáu trang bài tập (một cho mỗi mạch nội dung trừ mạch 2, thêm bài tổng hợp). Đã gộp để giữ 54: khối ứng dụng §3 vào 2-03 và 4-06; Nhận xét 10.5 vào trang kỹ thuật 3-05; Ví dụ 10.9 vào trang Ví dụ 10.8 (4-04); Nhận xét 10.9 vào ghi chú diễn giả 4-04, 4-05; Hệ quả 10.8 dùng chung trang ý tưởng chứng minh với Mệnh đề 10.7 (4-03); Nhận xét 10.14 (đọc thêm) và Ví dụ 10.15 vào ghi chú diễn giả 6-04; Nhận xét 10.17 vào 6-07; Bổ đề 10.3 có dòng "Chứng minh." trên trang phát biểu thay cho trang ý tưởng chứng minh riêng (mục 11, điểm 2); mạch 2 không có trang bài tập (mục 11, điểm 3). Phương án về 52 trang ở mục 11, điểm 1.

## 4. Bảng kết quả chính

Số hiệu theo ghi chú. Mọi phát biểu rút gọn trên trang dùng "Giả thiết:" và "Bảo đảm:", giữ đủ giả thiết, lượng từ và loại bảo đảm của ghi chú.

| Kết quả | Loại bảo đảm | (a) Trực quan | (b) Ý tưởng chứng minh | (c) Kỹ thuật | (d) Ví dụ bổ trợ | Trang |
|---|---|---|---|---|---|---|
| **Bổ đề 10.3** (đồng nhất thức gradient log; chứng minh đầy đủ) | đồng nhất thức, mọi $\theta\in\Theta$ | Tổng các xác suất luôn bằng $1$, nên tổng các thay đổi bằng $0$; trên giá, thay đổi của $p_\theta$ bằng $p_\theta$ nhân gradient log. Cực biên: ngoài giá, $p_\theta(\tau)=0$ là cực tiểu của hàm không âm, gradient bằng $0$. | Hai bước, dòng "Chứng minh." trên 3-01: (a) quy tắc dây chuyền trên giá; ngoài giá, $\theta$ là điểm trong (dùng $\Theta$ mở) và là điểm cực tiểu của $\theta'\mapsto p_{\theta'}(\tau)\ge0$; (b) đạo hàm từng số hạng của $\sum_\tau p_\theta(\tau)=1$ (dùng $\mathcal T$ hữu hạn, không phụ thuộc $\theta$). Bỏ giả thiết tập giá trị: Ví dụ 10.3 (giá $[0,\theta]$, $\mathbb E\partial_\theta\ln p_\theta=-1/\theta\ne0$). | Trang "Kỹ thuật." riêng 3-05 "Đạo hàm của kì vọng qua gradient log" (lần đầu có trang riêng; Bài 09 dùng ước lượng gradient log ở Định nghĩa 09.14, Ví dụ 09.12 mà không có trang kỹ thuật, theo mục 11 điểm 3 của storyboard Bài 09). | Ví dụ 10.3 ($\tfrac12$; $-1/\theta$; $-\tfrac12$); Ví dụ 10.4, Bước 4 (kì vọng gradient log bằng $0$). | 3-01, 3-02, 3-05 |
| **Định lý 10.4** (gradient của mục tiêu chính sách theo quỹ đạo; chứng minh đầy đủ) | đồng nhất thức, mọi $\theta\in\Theta$; ước lượng một lượt không chệch, trung bình $m$ lượt độc lập chia hiệp phương sai cho $m$ | Trong $p_\theta(\tau)$ chỉ các thừa số chính sách chứa $\theta$; lấy lôgarit biến tích thành tổng, nên gradient log của quỹ đạo là tổng gradient log của chính sách. Tác tử không cần $\mu_0$, $P$, $r$. Đạo hàm của trung bình đã thu bằng $0$ vì thiếu thừa số gradient log, thừa số mang ảnh hưởng của $\theta$ lên phân bố dữ liệu. | Ba bước: đạo hàm tổng hữu hạn $J=\sum_\tau p_\theta R$ (dùng $\mathcal S$, $\mathcal A$, $H$ hữu hạn, (Π)); thay $\nabla p_\theta=p_\theta\nabla\ln p_\theta$ trên giá (Bổ đề 10.3(a)); $\ln p_\theta$ thành tổng, bỏ $\ln\mu_0$, $\ln P$ (dùng (MDP)). Bỏ (MDP): Ví dụ 10.6, ước lượng $-0{,}25$ ngược dấu $0{,}125$. | Dùng trang 3-05; "Nhắc lại:" kỹ thuật "Đổi chỗ đạo hàm và kì vọng" (Bài 09, `L09-6-04`) trên 3-05 cho Nhận xét 10.5. | Ví dụ 10.4 ($\pm0{,}75$, $\tfrac38$); Ví dụ 10.5 ($(-0{,}025;\,0{,}25;\,-0{,}125)$, sai phân hữu hạn); Ví dụ 10.6; Bài tập 10.1(a), (b) ($\tfrac34$; $3$, $0$; $\tfrac{27}{16}$). | 3-03, 3-04, 3-06, 3-07, 3-08, 3-11 |
| **Mệnh đề 10.7** (tổng phần thưởng từ bước $t$; phác thảo, chi tiết ở Phụ lục B) | đồng nhất thức | Hành động ở bước $t$ không ảnh hưởng tới các phần thưởng nhận trước nó, nên các phần thưởng này chỉ thêm nhiễu vào số hạng của hành động đó. | Ba bước, trang chung 4-03: khi biết $\mathcal F_t$, $A_t\sim\pi_\theta(\cdot\mid S_t)$ nên $\mathbb E[\nabla\ln\pi_\theta(A_t\mid S_t)\mid\mathcal F_t]=\sum_a\nabla\pi_\theta(a\mid S_t)=0$ (dùng chính sách chỉ nhìn trạng thái hiện tại, Bổ đề 10.3); $f(\mathcal F_t)$ ra ngoài kì vọng có điều kiện, tính chất tháp; $f=r_{t'}$ với $t'<t$ cho (a), (a) cho (b). | **Nhắc lại** "Kì vọng có điều kiện theo lịch sử" (Bài 05, `L05-3-07`) một dòng trên 4-03; đồng nhất thức $\sum_a\nabla\pi_\theta(a\mid s)=\nabla1=0$ là bước 1 của 4-03, không có dòng "Kỹ thuật." riêng (theo mục 14; cổng duyệt L18). | Ví dụ 10.10 (vết $1{,}94625$ thành $1{,}62125$; trường hợp tăng $0$ lên $1$); Bài tập 10.2(c). | 4-01, 4-03, 4-05, 4-08 |
| **Hệ quả 10.8** (giá trị nền không làm đổi kì vọng của ước lượng; chứng minh đầy đủ) | đồng nhất thức | Giá trị nền là hàm của lịch sử trước $A_t$, nên nhân với một đại lượng có kì vọng có điều kiện $0$. Hệ quả cho phép chọn giá trị nền để giảm phương sai; một giá trị nền tùy ý cũng có thể tăng phương sai. | Trang chung 4-03, bước 3: thay $r_{t'}$ bằng $b_t(\mathcal F_t)$ (dùng giả thiết giá trị nền); trừ khỏi Mệnh đề 10.7(b). Bỏ giả thiết: giá trị nền $\kappa A$ cho kì vọng $\tfrac38-\tfrac{3\kappa}{16}$ (Ví dụ 10.9); $r(A)$ cho ước lượng luôn bằng $0$. | Như Mệnh đề 10.7. | Ví dụ 10.8 (bảng bốn giá trị nền, hình F1); Ví dụ 10.9; Ví dụ 10.11 ($0{,}1225$; $27{,}6225$; $0{,}06$); Bài tập 10.2(b), (c) ($0{,}225$; $0{,}4875$). | 4-02, 4-03, 4-04, 4-06, 4-08 |
| **Mệnh đề 10.13** (hai nhiệm vụ xung đột buộc một đánh đổi; chứng minh đầy đủ) | tất định, với các rủi ro kì vọng cho trước | Hai rủi ro có tâm $0$ và $1$; mọi $w$ cách hai tâm tổng cộng ít nhất $1$, nên không điểm nào làm cả hai bằng $0$; $\lambda$ chỉ trượt $w_\lambda$ trên $(0,1]$. Cực biên: $\lambda=0$ là tinh chỉnh ($L_A=\tfrac12$); $\lambda\to\infty$ giữ $w\to0$. | Bốn bước: bất đẳng thức tam giác cho $\lvert w\rvert+\lvert1-w\rvert\ge1$; hoàn thành bình phương $L_A+L_B=(w-\tfrac12)^2+\tfrac14$; đạo hàm của hàm bậc hai lồi nghiêm ngặt cho (c), (d). Một dòng "Kỹ thuật.": phạt $\tfrac\lambda2w^2=\lambda L_A(w)$ vì $L_A$ bậc hai có tâm $w^{(1)}$, độ cong $1$. Bỏ "độ cong $1$" (Bài tập 10.5(c)): phạt $\Omega=1$ không khớp phát lại. | Một dòng "Kỹ thuật." trên 6-03 (chỉ dùng trong bài). | Câu hỏi mở đầu ($0$ lên $\tfrac12$); Ví dụ 10.14 (bảng năm $\lambda$, hình F2); Bài tập 10.5(c); câu hỏi tự kiểm tra 3 ($\lambda=\tfrac14$). | 1-06, 6-02, 6-03, 6-04, 6-08 |

**Kết quả phụ và quyết định.**
- Thiết lập §1 và bảng nguồn ngẫu nhiên: trang 2-01 (bảng rút gọn hai hàng "Ngẫu nhiên", "Cố định"; hàng "Tất định" ở ghi chú diễn giả).
- Kí hiệu §2: bảng không lên mặt trang; mỗi kí hiệu được đặt tên ở trang đầu tiên dùng nó (mục 12).
- Ví dụ 10.1: trang 2-02. Khối ứng dụng hệ thống đề xuất: dữ liệu ở dòng (PT) của 2-03; câu hỏi (i), (ii) và câu trả lời ở 4-06 (Ví dụ 10.11).
- Định nghĩa 10.1 và đoạn sau (chính sách bảng, chính sách tất định): trang 2-03. Định nghĩa 10.2 và hai câu sau: trang 2-04.
- Nhận xét 10.5 (chứng minh đầy đủ ở Phụ lục A): dòng điều kiện trên trang kỹ thuật 3-05; chính sách Gauss ở ghi chú diễn giả 3-05.
- Đoạn sau Thuật toán 10.6 (oracle, điều kiện không chệch của Bài 05, thiếu (C)): trang 3-09.
- Đoạn sau Ví dụ 10.7 (Mệnh đề 08.12 với ba điều kiện): hai dòng cuối 3-10.
- Nhận xét 10.9 (i) (giá trị nền có tham số, entropy $\ln2$): ghi chú diễn giả 4-04; (ii) (giá trị nền từ chính lượt đang dùng; phần thưởng trước bước $t$; trung bình các lượt trước): ghi chú diễn giả 4-05 và 4-06.
- Định nghĩa 10.10 và đoạn sau: trang 5-01; Định nghĩa 10.11 và đoạn sau: trang 5-02.
- Đánh đổi bền vững–mềm dẻo (đoạn sau Mệnh đề 10.13): hai dòng cuối 6-04.
- Nhận xét 10.14 (đọc thêm) và Ví dụ 10.15: ghi chú diễn giả 6-04 ($v=\tfrac2{2+\lambda}$; $L_B=\tfrac29$, $\tfrac89$).
- Định nghĩa 10.15, đẳng thức sau nó và Nhận xét 10.16: trang 6-06. Nhận xét 10.17: dòng "Kết luận:" của 6-07 và ghi chú diễn giả.
- Câu ôn nhanh 1–2: dòng "Nhắc lại:" và ghi chú diễn giả 1-02.
- §10: trang 7-02 và ghi chú diễn giả 7-01. §12 (câu hỏi cuối buổi (a)–(f)): câu hỏi tự kiểm tra 1–4 ở 7-04 dùng (a), (b), (d), (e); (c) trùng Ví dụ 10.6, ở ghi chú diễn giả 3-08; (f) và Phụ lục D ở trang 7-02 (bảng ba bài toán) và dòng khép học phần ở 7-06.
- Phụ lục C: ghi chú diễn giả 4-06 (bảng REINFORCE) và dòng mô phỏng trên 6-05.

## 5. Ví dụ bổ trợ

Ví dụ xuyên suốt của ghi chú: **bài toán bandit hai hành động với chính sách sigmoid** (Ví dụ 10.1, 10.4, 10.8, 10.9, khối ứng dụng và Ví dụ 10.11, Bài tập 10.1, câu hỏi tự kiểm tra 1–2), **MDP hai bước** (câu hỏi mở đầu, Ví dụ 10.2, 10.5, 10.6, 10.10, 10.12, Bài tập 10.2) và **hai nhiệm vụ bậc hai $L_A=w^2/2$, $L_B=(w-1)^2/2$** (câu hỏi mở đầu, Mệnh đề 10.13, Ví dụ 10.14, 10.16, 10.17, Bài tập 10.5, câu hỏi tự kiểm tra 3–4). Mỗi lần dùng lại trả lời một câu hỏi mới. Bandit: đạo hàm trực tiếp (2-02); ước lượng gradient log không chệch nhưng nhiễu (3-06); phương sai theo giá trị nền (4-04); dịch phần thưởng (4-06). MDP hai bước: phân bố của $S_1$ phụ thuộc $\theta_{s_0}$ (2-05); gradient theo quỹ đạo khớp sai phân hữu hạn (3-07); luật chuyển phụ thuộc tham số (3-08); giá trị nền theo trạng thái (4-05); cận Hoeffding cho chính sách cố định (4-07); bài tập giá trị nền $r_0$ (4-08). Hai nhiệm vụ bậc hai: quên khi tinh chỉnh (1-06); cận dưới và đánh đổi (6-02, 6-04); bộ đệm hữu hạn (6-05); hối tiếc và độ quên (6-07).

Mọi con số dưới đây đã tính lại bằng Python (thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-10/storyboard/num.py`, phân số chính xác bằng `fractions` khi có thể) và khớp ghi chú, tệp bài tập. Số của mô phỏng (Ví dụ 10.11 Bước 4; Ví dụ 10.16 Bước 4) lấy nguyên từ ghi chú và Phụ lục C, không chạy lại. **Không có ví dụ mới mang số mới trên mặt trang.** Hai hình vẽ đồ thị của công thức trong ghi chú: F1 là phương sai của Ví dụ 10.8, Bước 1 theo $b$; F2 là đường $(L_A(w),L_B(w))$, $w\in[0,1]$, của Mệnh đề 10.13 với năm điểm của Ví dụ 10.14 (cách dựng ở mục 8).

| Mã | Nguồn | Trang | Phép tính và kết quả (đã tính lại) |
|---|---|---|---|
| V1 | Câu hỏi mở đầu | 1-06 | Xác suất tới $s_1$: $0{,}8q+0{,}2(1-q)=0{,}2+0{,}6q$; $q=0{,}5$: $0{,}5$; $q=0{,}9$: $0{,}74$. Hai môi trường: $L_A(0)=0$; $L_A(1)=\tfrac12$. |
| V2 | Ví dụ 10.1 | 2-02 | $e^{-\ln3}=\tfrac13$, $\pi_\theta(1)=1/(1+\tfrac13)=\tfrac34$; $J=1+2\cdot\tfrac34=\tfrac52$; $J'=2\cdot\tfrac34\cdot\tfrac14=\tfrac38$. $J<3$, $J\to3$. |
| V3 | Ví dụ 10.2 | 2-05 | Tám quỹ đạo tại $\theta=0$: $(1,s_1,1)$: $\tfrac12\cdot0{,}8\cdot\tfrac12=0{,}2$, $R=3$; $(1,s_1,0)$: $0{,}2$, $1$; $(1,s_2,1)$: $0{,}05$, $0$; $(1,s_2,0)$: $0{,}05$, $1$; $(0,s_1,1)$: $0{,}05$, $4$; $(0,s_1,0)$: $0{,}05$, $2$; $(0,s_2,1)$: $0{,}2$, $1$; $(0,s_2,0)$: $0{,}2$, $2$. Bước cuối: $2$ ở $s_1$, $\tfrac12$ ở $s_2$. Hành động $1$: $0+0{,}8\cdot2+0{,}2\cdot\tfrac12=1{,}7$; hành động $0$: $1+0{,}2\cdot2+0{,}8\cdot\tfrac12=1{,}8$. $J(0)=1{,}75$; tổng bảng $0{,}6+0{,}2+0+0{,}05+0{,}2+0{,}1+0{,}2+0{,}4=1{,}75$. |
| V4 | Ví dụ 10.3 | 3-02 | $J(\theta)=\theta/2$, $J'=\tfrac12$; trên giá $\ln p_\theta=-\ln\theta$, đạo hàm $-1/\theta$; $\mathbb E[A\cdot(-1/\theta)]=-\tfrac12$. |
| V5 | Ví dụ 10.4 | 3-06 | Gradient log $A-\tfrac34$: $\tfrac14$ khi $A=1$, $-\tfrac34$ khi $A=0$. $\hat g=3\cdot\tfrac14=0{,}75$ (xác suất $\tfrac34$), $1\cdot(-\tfrac34)=-0{,}75$ (xác suất $\tfrac14$). $\mathbb E\hat g=0{,}5625-0{,}1875=0{,}375=\tfrac38$. $\mathbb E$ gradient log $=\tfrac3{16}-\tfrac3{16}=0$. |
| V6 | Ví dụ 10.5 | 3-07 | $\partial/\partial\theta_{s_0}$: $\tfrac12(0{,}85)-\tfrac12(0{,}9)=-0{,}025$, với $0{,}85=0{,}6+0{,}2+0+0{,}05$, $0{,}9=0{,}2+0{,}1+0{,}2+0{,}4$. $\theta_{s_1}$: $0{,}3-0{,}1+0{,}1-0{,}05=0{,}25$. $\theta_{s_2}$: $0-0{,}025+0{,}1-0{,}2=-0{,}125$. Sai phân hữu hạn trung tâm ($\epsilon=10^{-6}$): $(-0{,}025;\,0{,}25;\,-0{,}125)$. Diễn giải: $\tfrac14(1{,}7-1{,}8)=-0{,}025$; $(0{,}8-0{,}2)(2-\tfrac12)=0{,}9<1$. |
| V7 | Ví dụ 10.6 | 3-08 | $q=\tfrac12$; bước đầu kì vọng $1-\pi_\theta(1\mid s_0)$, đạo hàm $-\tfrac14$; bước sau $2q+\tfrac12(1-q)$, đạo hàm $\tfrac32q(1-q)=0{,}375$; tổng $0{,}125$. Ước lượng: $\tfrac12\cdot0\cdot\tfrac12+\tfrac12\cdot1\cdot(-\tfrac12)=-0{,}25$. $J=\tfrac12+\tfrac54=1{,}75$. |
| V8 | Ví dụ 10.7 | 3-10 | $J=q^2+0{,}6(1-q)^2$; $dJ/dq=3{,}2q-1{,}2=0$ tại $q=0{,}375$, $\theta=\ln0{,}6\approx-0{,}5108$; $J=0{,}375$; $d^2J/d\theta^2=3{,}2(q(1-q))^2\approx0{,}1758$. Đi lên theo gradient đúng (độ dài bước $0{,}5$, $20\,000$ bước, chỉ để kiểm hướng): từ $\theta=-1$ ($q\approx0{,}2689$), $\theta\to-\infty$, $J\to0{,}6$; từ $\theta=-0{,}4$ ($q\approx0{,}4013$), $\theta\to\infty$, $J\to1$. |
| V9 | Bài tập 10.1(a), (b) | 3-11 | $e^{\ln3}=3$, $\pi=\tfrac14$; $J=1$; $J'=4\cdot\tfrac14\cdot\tfrac34=\tfrac34$. $\hat g=4\cdot\tfrac34=3$ (xác suất $\tfrac14$), $0$ (xác suất $\tfrac34$); $\mathbb E\hat g=\tfrac34$; $\operatorname{Var}=\tfrac14\cdot9-\tfrac9{16}=\tfrac{27}{16}$. |
| V10 | Ví dụ 10.8 | 4-04, F1 | $\hat g_b$: $b=0$: $\tfrac34$, $-\tfrac34$, $\operatorname{Var}=\tfrac{27}{64}$; $b=\tfrac52$: $\tfrac18$, $\tfrac98$, $\tfrac3{256}+\tfrac{81}{256}-\tfrac{36}{256}=\tfrac3{16}$; $b=\tfrac32$: $\tfrac38$, $\tfrac38$, $0$; $b=5$: $-\tfrac12$, $3$, $\tfrac{147}{64}$. $b^*=3\cdot\tfrac14+1\cdot\tfrac34=\tfrac32$. $\tfrac{147}{64}\big/\tfrac{27}{64}\approx5{,}44$ ("hơn năm lần"). Công thức Bước 1 rút gọn thành $(12b^2-36b+27)/64$; F1 vẽ đường này (kiểm bốn điểm). |
| V11 | Ví dụ 10.9 | 4-04 | $\mathbb E[A(A-\tfrac34)]=\tfrac34\cdot\tfrac14=\tfrac3{16}$; kì vọng $\tfrac38-\tfrac{3\kappa}{16}$: $\kappa=1$: $\tfrac3{16}$; $\kappa=2$: $0$. |
| V12 | Ví dụ 10.10 | 4-05 | Phương sai (phân số chính xác): (i) $\tfrac{1619}{1600}$; $\tfrac{11}{16}$; $\tfrac{79}{320}$; (ii) $\tfrac{1619}{1600}$; $\tfrac9{16}$; $\tfrac3{64}$; (iii) $\tfrac{197}{800}$; $\tfrac1{16}$; $\tfrac1{64}$. Vết $1{,}94625$; $1{,}62125$; $0{,}324375$; $1{,}94625/0{,}324375=6$; $1{,}62125/0{,}324375\approx5$. Bước 3: (i) luôn $\tfrac12$, phương sai $0$; (ii) $\tfrac32$ hoặc $-\tfrac12$, phương sai $\tfrac12(\tfrac94+\tfrac14)-\tfrac14=1$; $b^*=3\cdot\tfrac12+1\cdot\tfrac12=2$. |
| V13 | Ví dụ 10.11 | 4-06 | $J'(0)=0{,}2\cdot\tfrac14=0{,}05$; $b=0$: $c=0$: $\tfrac14\cdot\tfrac12-0{,}0025=0{,}1225$; $c=10$: $\tfrac14\cdot110{,}5-0{,}0025=27{,}6225$; tỉ số $\approx225{,}5$ ("khoảng $225$ lần"). $b=c+\tfrac12$: $0{,}0625-0{,}0025=0{,}06$. Mô phỏng (Phụ lục C, không chạy lại): $c=10$, không giá trị nền: $49/100$ lần chạy kết thúc dưới $0{,}5$; có giá trị nền hoặc $c=0$: $0$. |
| V14 | Ví dụ 10.12 | 4-07 | $R\in[0,4]$; $4\sqrt{\ln40/2000}\approx4\cdot0{,}042947=0{,}17179\le0{,}1718$; $m\ge16\ln40/0{,}005\approx11\,804{,}4$, cần $11\,805$ lượt. |
| V15 | Bài tập 10.2(b), (c) | 4-08 | (b) số hạng trừ đi có kì vọng $1\cdot\tfrac14\cdot(-1)=-\tfrac14$; $-0{,}025+0{,}25=0{,}225$ (phân số $\tfrac9{40}$); kiểm trên bảng $0{,}425-0{,}2=0{,}225$. (c) giá trị tọa độ $\theta_{s_1}$: $1{,}5$; $-0{,}5$; $1$; $0$ với xác suất $0{,}2$; $0{,}2$; $0{,}05$; $0{,}05$; kì vọng $0{,}25$; mô-men bậc hai $0{,}55$; phương sai $0{,}4875=\tfrac{39}{80}<\tfrac9{16}=0{,}5625$. |
| V16 | Ví dụ 10.13 | 5-03 | Trung bình cuối $(0{,}80+0{,}75+0{,}88)/3=0{,}81$; chuyển đổi ngược $\tfrac12(-0{,}05-0{,}17)=-0{,}11$; độ quên $0{,}10$; $0{,}17$; trung bình $0{,}135$; chuyển đổi xuôi $\tfrac12(0{,}02+0{,}03)=0{,}025$. Ma trận thứ hai: chuyển đổi ngược $0{,}005$; độ quên $0{,}07$ và $0$; cực đại tới hàng $K-1$: $0{,}92-0{,}95=-0{,}03$. |
| V17 | Bài tập 10.4(a), (d) | 5-04 | Trung bình cuối $2{,}26/3\approx0{,}7533$; chuyển đổi ngược $\tfrac12(-0{,}10-0{,}28)=-0{,}19$; độ quên $0{,}15$; $0{,}28$; trung bình $0{,}215$; chuyển đổi xuôi $0{,}015$. (d) $\min_i\mathrm{acc}_{3,i}=0{,}60$ (nhiệm vụ 2), thấp hơn $\mathrm{acc}^\circ_2=0{,}86$ là $0{,}26$. |
| V18 | Mệnh đề 10.13, Ví dụ 10.14 | 6-02, 6-04, F2 | $\lambda=0;\tfrac13;1;3;9$: $w_\lambda=1;\tfrac34;\tfrac12;\tfrac14;\tfrac1{10}$; $L_A=\tfrac12;\tfrac9{32};\tfrac18;\tfrac1{32};\tfrac1{200}$; $L_B=0;\tfrac1{32};\tfrac18;\tfrac9{32};\tfrac{81}{200}$; tổng $\tfrac12;\tfrac5{16};\tfrac14;\tfrac5{16};\tfrac{41}{100}$; $\alpha=0;\tfrac14;\tfrac12;\tfrac34;\tfrac9{10}$. |
| V19 | Ví dụ 10.15 (ghi chú diễn giả) | 6-04 | $v=\tfrac2{2+\lambda}$: $\lambda=1$: $\tfrac23$, $L_B=2(\tfrac13)^2=\tfrac29\approx0{,}2222$; $\lambda=4$: $\tfrac13$, $L_B=\tfrac89\approx0{,}8889$. |
| V20 | Ví dụ 10.16 | 6-05 | $L_A(\tfrac12)=\tfrac12(\tfrac14+1)=\tfrac58$; $\tfrac12\operatorname{Var}(w_M)=\tfrac12\cdot\tfrac14\cdot\tfrac1M=\tfrac1{8M}$; $M=1;10;100$: $0{,}125$; $0{,}0125$; $0{,}00125$. Mô phỏng (không chạy lại): $0{,}624$; $0{,}331$; $0{,}256$; $0{,}252$; điểm thỏa hiệp $0{,}25$; $\min$ $0{,}125$. |
| V21 | Ví dụ 10.17 | 6-07 | $\sum_t\ell(u,z_t)=250u^2+250(1-u)^2$, nhỏ nhất $125$ tại $u=\tfrac12$. $\sqrt{1000}\approx31{,}623\le31{,}63$. Hạ gradient có chiếu lên $[0,1]$ từ $w_1=0$: $\eta=1/\sqrt{1000}$: hối tiếc $-116{,}967\approx-116{,}97$, $w_{T+1}\approx1-10^{-7}$, $L_A\approx\tfrac12$; $\eta_t=1/t$: hối tiếc $0{,}1876\approx0{,}19$, $w_{T+1}=\tfrac12$, $L_A=\tfrac18$. |
| V22 | Bài tập 10.5(c) | 6-08 | Phát lại: $(1-\alpha)(w-1)+4\alpha w=0$, $w=\frac{1-\alpha}{1+3\alpha}$; $\alpha=\tfrac12$: $\tfrac15$. Phạt: $w=\frac1{1+\lambda\Omega}$; $\Omega=1$, $\lambda=1$: $\tfrac12$; $\Omega=4$, $\lambda=1$: $\tfrac15$. Trùng nhau: $\lambda\Omega=\frac{4\alpha}{1-\alpha}$; $\alpha=\tfrac12$ cho $4$. |
| V23 | Bài tập 10.7(i) | 7-03 | Không có số mới; miền $[Hr_{\min},Hr_{\max}]$, bán kính nhân $H(r_{\max}-r_{\min})$. Kiểm tra lại của tệp bài tập: Ví dụ 10.2 cho $[0,6]$, chứa $[0,4]$ của Ví dụ 10.12. |
| V24 | §12 (a), (b), (d), (e) | 7-04 | (a) $J=2\pi_\theta(1)$, $J'(0)=2\cdot\tfrac14=\tfrac12$; $\hat g=2\cdot\tfrac12=1$ hoặc $0$; kì vọng $\tfrac12$. (b) luôn $0$. (d) $w_\lambda=\tfrac45$; $L_A=\tfrac8{25}$; $L_B=\tfrac1{50}$; $\alpha=\tfrac15$. (e) $-116{,}97$, $L_A\approx\tfrac12$. |

## 6. Danh sách trang

Mỗi mục: ID, tiêu đề, loại, thời lượng; **Mặt trang** (các dòng dự kiến, theo thứ tự; `[f]` là fragment; `$$…$$` là công thức hiển thị, tính một dòng; `Bảng:` là một bảng HTML, ô ngăn bằng `|`, hàng ngăn bằng `;`; `{{…}}` là chỉ dẫn bố cục, không lên mặt trang); **Ghi chú diễn giả** (ý chính, 40–150 âm tiết, đến ~250 cho trang ý tưởng chứng minh và trang bài tập; viết cho giảng viên và người học; không mã trang, mã ví dụ của storyboard, câu quy trình hay nguồn gốc; luôn kết thúc bằng dòng `note-source`); **Lý do / nối**; **Mục tiêu / nguồn**. Câu trên mặt trang là bản dự kiến đã tự kiểm theo `no-ai-slop` (chế độ Edit) và `eval.md`; người viết deck có thể rút gọn, không thêm khẳng định.

Quy ước chung cho người viết deck:
- Trang kết quả: "Giả thiết:" và "Bảo đảm:" (nhãn của ghi chú), trích số khối của ghi chú một lần; "(a)", "(b)" của một kết quả viết thường, không in đậm.
- Trang tổng quan (bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm") viết bằng lời, không kí hiệu, không tiếng Anh. Lần đầu một thuật ngữ trên trang nội dung có tiếng Anh trong ngoặc (bảng mục 10).
- Mọi kí hiệu trên mặt trang đã có ở trang trước hoặc có dòng "Nhắc lại:"/"Kí hiệu:" (bảng đối chiếu mục 12 ghi chỗ đưa vào).
- Bước chứng minh trên trang "Ý tưởng chứng minh" là `<ol>`; giả thiết dùng ở bước ghi trong ngoặc đầu mục, như deck Bài 06 (`L06-4-04`); không nhãn in đậm "Bước k".
- Số thập phân dùng dấu phẩy KaTeX `0{,}5`; dãy số ngăn bằng `;\ `; số từ năm chữ số tách nhóm bằng `\,`.
- Mỗi trang ví dụ mở bằng dữ kiện, không câu dẫn. "Diễn giải:" chỉ dùng số có trên chính trang đó.
- Không `\text{}` chứa tiếng Việt trong KaTeX. Trong ghi chú diễn giả, không ghi câu nguồn gốc, mã "V7", "mục 5", không mở bằng "Trang này", "Mạch này", "Bài này", không lấy mạch làm chủ ngữ.
- Công thức một dòng khi vừa khung; chỉ ngắt bằng `aligned` khi tràn ở 390 px (đo trong trình duyệt). Ở chế độ đọc hẹp, công thức rộng cuộn ngang tại chỗ.
- "Giá trị nền" cho baseline (không "đường cơ sở"); "tổng phần thưởng" cho return; "lượt" cho episode; "gradient log" cho score function; "lôgarit"; "tập huấn luyện", "tập kiểm tra" theo ghi chú. Trên trang bài tập, giữ dữ kiện, câu hỏi và kết quả của `exercises.md`; khi câu chữ rút gọn, câu đầy đủ nằm ở ghi chú diễn giả (mục 11, điểm 7).
- Tiêu đề có công thức viết bằng KaTeX.

### Mạch 1. Mở đầu (6 trang, 10 phút)

#### `1-01` Gradient chính sách và học liên tục — bìa, điểm vào mạch 1 · 1 phút
- **Mặt trang:**
  - Bài 10
  - Khi dữ liệu do chính sách sinh ra, gradient của mục tiêu ước lượng được không chệch nếu chính sách khả vi và môi trường không phụ thuộc tham số, còn khi nhiệm vụ thay đổi, cần nêu trước giao thức và ma trận đánh giá.
  - Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1
  - Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN
- **Ghi chú diễn giả:** Trong Bài 01–09, dữ liệu được rút từ một phân bố $D$ cố định, không phụ thuộc thuật toán học; ở Bài 09, thuật toán chọn phân bố biến phân nhưng dữ liệu vẫn rút từ $D$. Bài 10 xét hai thay đổi. Ở học tăng cường, chính sách mà tác tử đang học quyết định dữ liệu nó quan sát; gradient của tổng phần thưởng kì vọng vẫn là kì vọng của một đại lượng tính được trên quỹ đạo (Định lý 10.4). Ở học liên tục, phân bố thay đổi theo nhiệm vụ; mục tiêu là các độ đo của một ma trận đánh giá, và hai nhiệm vụ xung đột buộc một đánh đổi (Mệnh đề 10.13). Nguồn: ghi chú Bài 10, đoạn mở đầu, §10.
- **Lý do / nối:** luận điểm cả bài → tiên quyết.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu, §10.

#### `1-02` Tiên quyết và quy ước — mở đầu · 1,5 phút
- **Mặt trang:**
  - **Nhắc lại:** (T1): $Z_1,\ldots,Z_m$ độc lập cùng phân bố $D$; $L_D(w)=\mathbb E_{z\sim D}\ell(w,z)$.
  - Hệ quả 02.10(b): (T1), (T3) ($\ell\in[0,1]$), $h$ cố định: với xác suất ít nhất $1-\delta$,
  - $$\lvert L_S(h)-L_D(h)\rvert\le\sqrt{\ln(2/\delta)/(2m)}.$$
  - Bài 05: chiếu $\operatorname{proj}_W$, dưới vi phân $\partial F$; Định lý 05.14 cần oracle không chệch, (C): $W$ khác rỗng, đóng, lồi, $F$ lồi.
  - Bài 09: ước lượng gradient log; đổi chỗ đạo hàm và kì vọng.
  - $s(\theta)=1/(1+e^{-\theta})$: $s'=s(1-s)$, $(\ln s)'=1-s$, $(\ln(1-s))'=-s$.
- **Ghi chú diễn giả:** Hệ quả 02.10 cần dạng đầy đủ của (T1), một hàm lỗi bị chặn và một giả thuyết cố định, không phụ thuộc tập huấn luyện (Nhận xét 01.9); với miền $[a,b]$, bán kính nhân thêm $b-a$ (đoạn sau Nhận xét 02.8). Câu ôn nhanh 1: với $m=500$, $\delta=0{,}05$, bán kính là $\sqrt{\ln40/1000}\le0{,}0608$. Câu ôn nhanh 2: theo quy tắc dây chuyền, $s'(\theta)=e^{-\theta}/(1+e^{-\theta})^2=s(1-s)$; chia cho $s$ được $(\ln s)'=1-s$; vì $1-s$ có đạo hàm $-s(1-s)$, $(\ln(1-s))'=-s$. Ở Bài 05, (C) và oracle không chệch cho cận kì vọng của hạ gradient ngẫu nhiên có chiếu. Nguồn: ghi chú Bài 10, Kiến thức tiên quyết, Câu hỏi ôn nhanh.
- **Lý do / nối:** các kết quả của Bài 01–09 dùng trên mặt trang được nhắc lại ở đây → mục tiêu.
- **Mục tiêu / nguồn:** 2, 5; Kiến thức tiên quyết.

#### `1-03` Mục tiêu — mở đầu · 1 phút
- **Mặt trang (danh sách đánh số, bằng lời, không kí hiệu; trần 80):**
  1. Mô tả tối ưu chính sách: đại lượng nào ngẫu nhiên, theo phân bố nào.
  2. Chứng minh công thức gradient chính sách; nêu điều kiện đổi chỗ đạo hàm, kì vọng.
  3. Chứng minh giá trị nền giữ kì vọng, tính phương sai, chỉ ra trường hợp chệch.
  4. Đặc tả giao thức học liên tục; tính độ quên từ ma trận đánh giá.
  5. Giải thích vì sao cận cho phân bố cố định, mục tiêu lồi, hối tiếc tĩnh không đủ.
- **Ghi chú diễn giả:** Mục tiêu 1 xét quá trình quyết định Markov tầm nhìn hữu hạn. Mục tiêu 2 gồm đồng nhất thức gradient log, công thức gradient chính sách theo quỹ đạo và phép kiểm công thức bằng đạo hàm trực tiếp. Mục tiêu 3 gồm cả tổng phần thưởng từ bước hiện tại; phương sai tính trong trường hợp nhỏ. Ở mục tiêu 4, các độ đo là độ chính xác phân lớp trung bình cuối cùng, chuyển đổi ngược và độ quên. Mục tiêu 5 nói về hai bài toán của bài: các cận cho phân bố cố định, cho mục tiêu lồi và cho hối tiếc tĩnh không trực tiếp giải quyết chúng. Nguồn: ghi chú Bài 10, Mục tiêu học tập.
- **Lý do / nối:** tiêu chí kiểm tra → nội dung.
- **Mục tiêu / nguồn:** tất cả; Mục tiêu học tập.

#### `1-04` Nội dung — mở đầu · 0,5 phút
- **Mặt trang:**
  - `ol start="2"` với liên kết `#/2`…`#/7`: 2. Quá trình quyết định Markov và mục tiêu của chính sách; 3. Gradient chính sách và thuật toán REINFORCE; 4. Giá trị nền và phương sai của ước lượng gradient; 5. Giao thức học liên tục và ma trận đánh giá; 6. Hai nhiệm vụ xung đột và hối tiếc; 7. Tổng kết.
  - Đọc trước: Sutton và Barto (2018), §13.1–13.3.
- **Ghi chú diễn giả:** Phần A: mô hình tương tác và mục tiêu của chính sách; công thức gradient và thuật toán dùng nó; các cách giảm phương sai mà không đổi kì vọng. Phần B: cách đặt bài toán khi nhiệm vụ đến theo thứ tự và cách đo kết quả; đánh đổi giữa nhiệm vụ cũ và mới, và so sánh với hối tiếc của học trực tuyến. Nguồn: ghi chú Bài 10; §13.
- **Lý do / nối:** bản đồ mạch → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §13.

#### `1-05` Vấn đề trung tâm — mở đầu · 1 phút
- **Mặt trang:**
  - {{một hộp `div.box`}} **Câu hỏi:** điều gì thay đổi khi thuật toán học tương tác với môi trường và khi nhiệm vụ thay đổi theo thời gian?
- **Ghi chú diễn giả** (câu trả lời cho cả bài, không trên mặt trang): Khi tác tử tương tác với môi trường, phân bố của dữ liệu phụ thuộc tham số đang học, nên (T1) không đúng; gradient của mục tiêu vẫn ước lượng được không chệch từ một lượt nhờ gradient log của chính sách, khi luật chuyển không phụ thuộc tham số. Mục tiêu không lõm, nên điểm dừng có thể là điểm cực tiểu. Khi nhiệm vụ thay đổi, bài toán chỉ xác định khi có giao thức và ma trận đánh giá; hai nhiệm vụ xung đột buộc một đánh đổi, và hối tiếc tĩnh nhỏ không kéo theo độ quên nhỏ. Nguồn: ghi chú Bài 10, đoạn mở đầu, §10.
- **Lý do / nối:** một vấn đề cốt lõi → hai tình huống cụ thể.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu.

#### `1-06` Ví dụ: robot chọn hành động và mô hình học hai môi trường — ví dụ dẫn nhập (Câu hỏi mở đầu) · 5 phút
- **Mặt trang:**
  - Robot ở $s_0$ chọn $a\in\{0,1\}$, tới $s_1$ với xác suất $0{,}2+0{,}6a$.
  - Chọn $a=1$ với xác suất $q$: tới $s_1$ với xác suất $0{,}2+0{,}6q$ ($0{,}5$ khi $q=0{,}5$; $0{,}74$ khi $q=0{,}9$).
  - Mô hình một tham số: $L_A(w)=w^2/2$ trên A, $L_B(w)=(w-1)^2/2$ trên B.
  - Học A được $w=0$; học tiếp chỉ trên B: $w\to1$, $L_A$ tăng từ $0$ lên $\tfrac12$.
  - **Câu hỏi:** dữ liệu ở mỗi tình huống khác $S\sim D^m$ ở điểm nào?
- **Ghi chú diễn giả:** Các quan sát của robot không tạo thành một tập huấn luyện $S\sim D^m$ như (T1): phân bố của chúng thay đổi theo $q$, và trạng thái ở bước sau phụ thuộc hành động ở bước trước. Khi dữ liệu đã thu, trung bình các phần thưởng là một số cố định, không chứa $q$, nên đạo hàm của nó theo $q$ bằng $0$, dù phần thưởng kì vọng đổi khi $q$ đổi; đạo hàm của phần thưởng kì vọng vẫn ước lượng được từ dữ liệu. Ở tình huống thứ hai, dữ liệu của A không còn khi học B nên không gộp được; nếu giữ được, tập huấn luyện gộp phục vụ rủi ro trung bình của hai môi trường. Không $w$ nào cho cả hai rủi ro bằng $0$, nên cần một điểm thỏa hiệp. Nguồn: ghi chú Bài 10, Câu hỏi mở đầu và đoạn sau.
- **Lý do / nối:** ví dụ dẫn nhập trước mọi định nghĩa; trọng tâm trực quan 1, 4, 5 → tiêu đề mạch 2.
- **Mục tiêu / nguồn:** 1, 5; Câu hỏi mở đầu.

### Mạch 2. Quá trình quyết định Markov và mục tiêu của chính sách (6 trang, 15 phút)

#### `2-00` 2. Quá trình quyết định Markov và mục tiêu của chính sách — tiêu đề mạch, điểm vào mạch 2 · 0,5 phút
- **Mặt trang:**
  - "2."; h2 "Quá trình quyết định Markov và mục tiêu của chính sách"
  - `p.strand-lead`: Dữ liệu của tác tử do chính sách sinh ra, nên phân bố của dữ liệu đổi theo tham số.
  - `p.strand-keys`: tác tử · chính sách · quá trình quyết định Markov · quỹ đạo · tổng phần thưởng
- **Ghi chú diễn giả:** Robot của ví dụ mở đầu là một tác tử: ở mỗi bước nó quan sát trạng thái, chọn hành động theo một phân bố có tham số và nhận phần thưởng. Mục tiêu là tổng phần thưởng kì vọng của một lượt, một hàm của tham số. Mỗi số hạng của mục tiêu chứa xác suất của chính sách và của môi trường; tác tử chỉ biết phần của chính sách, nên không tính được mục tiêu bằng công thức. Nguồn: ghi chú Bài 10, §1, §4.
- **Lý do / nối:** câu hỏi mở đầu → thiết lập.
- **Mục tiêu / nguồn:** 1; §1–§4.

#### `2-01` Thiết lập hai bài toán — thiết lập (§1) · 3 phút
- **Mặt trang:**
  - Học tăng cường (reinforcement learning): tác tử (agent) tương tác với môi trường qua các lượt (episode).
  - Ngẫu nhiên: lượt, tham số, ước lượng gradient; môi trường cố định.
  - Tham số ở cập nhật $j$ phụ thuộc các lượt trước: (T1) không đúng.
  - Học liên tục (continual learning): $K$ nhiệm vụ (task), phân bố $D_1,\ldots,D_K$, đến theo thứ tự.
- **Ghi chú diễn giả:** Mỗi bài toán có bảy thành phần. Phần A: hành động rút theo chính sách hiện tại, trạng thái kế tiếp theo môi trường; các lượt độc lập khi chính sách cố định; mục tiêu là tổng phần thưởng kì vọng của một lượt; tài nguyên là số lượt. Ở Phần A, phân bố của lượt thứ $j$ phụ thuộc các lượt trước qua tham số. Phần B: mỗi tập huấn luyện $S^{(k)}\sim D_k^{m_k}$ thỏa (T1) với phân bố của nó; thuật toán có thể giữ một phần dữ liệu cũ hoặc phạt độ lệch khỏi tham số cũ; mục tiêu là rủi ro $L_{D_k}(w)$ nhỏ với mọi nhiệm vụ đã gặp; ngẫu nhiên là các tập huấn luyện, dữ liệu cũ được giữ và tập kiểm tra. Tại một tham số cố định, mục tiêu và rủi ro từng nhiệm vụ là tất định. Nguồn: ghi chú Bài 10, §1.
- **Lý do / nối:** hai bài toán và chỗ (T1) không đúng (trọng tâm trực quan 4) → ví dụ bandit.
- **Mục tiêu / nguồn:** 1; §1.

#### `2-02` Ví dụ: bài toán bandit hai hành động — ví dụ (Ví dụ 10.1) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 10.1.** Bài toán bandit (multi-armed bandit): một bước, không trạng thái; hành động $A\in\{0,1\}$; phần thưởng $r(1)=3$, $r(0)=1$.
  - Chính sách $\pi_\theta(1)=1/(1+e^{-\theta})$, $\pi_\theta(0)=1-\pi_\theta(1)$, $\theta\in\mathbb R$.
  - $$J(\theta)=\mathbb E_{A\sim\pi_\theta}r(A)=1+2\,\pi_\theta(1),\qquad J'(\theta)=2\,\pi_\theta(1)\big(1-\pi_\theta(1)\big)$$
  - Tại $\theta=\ln3$: $\pi_\theta(1)=\tfrac34$, $J=\tfrac52$, $J'=\tfrac38$.
  - $J<3$ với mọi $\theta$ và $J\to3$ khi $\theta\to\infty$: cận trên đúng $3$ không đạt.
  - **Lưu ý:** $J'$ tính được vì $J$ có dạng đóng chứa $r(0)$, $r(1)$.
- **Ghi chú diễn giả:** Bài toán bandit là bài toán chọn một trong hữu hạn hành động có phần thưởng chưa biết; ở đây một lượt có đúng một bước. $J(\theta)$ là phần thưởng kì vọng của chính sách. Đạo hàm dùng câu ôn nhanh 2: $\frac{d}{d\theta}\pi_\theta(1)=\pi_\theta(1)(1-\pi_\theta(1))$. Tại $\theta=\ln3$, $e^{-\theta}=\tfrac13$, nên $\pi_\theta(1)=\tfrac34$. Tác tử thật không biết $r(0)$, $r(1)$, nên không viết được $J$; số $\tfrac38$ là giá trị để kiểm một ước lượng gradient. Nguồn: ghi chú Bài 10, §3, Ví dụ 10.1.
- **Lý do / nối:** ví dụ xuyên suốt có đạo hàm đúng $\tfrac38$ để kiểm ước lượng → định nghĩa MDP.
- **Mục tiêu / nguồn:** 1, 2; Ví dụ 10.1.

#### `2-03` Quá trình quyết định Markov và chính sách khả vi — định nghĩa (Định nghĩa 10.1) · 3 phút
- **Mặt trang:**
  - **Định nghĩa 10.1.** Quá trình quyết định Markov (Markov decision process, MDP) tầm nhìn hữu hạn (finite horizon) $(\mathcal S,\mathcal A,\mu_0,P,r,H)$; $r$ tất định, trong $[r_{\min},r_{\max}]$.
  - (MDP): $\mathcal S$, $\mathcal A$ hữu hạn; $\mu_0$, $P(\cdot\mid s,a)$ không phụ thuộc $\theta$.
  - (Π): chính sách ngẫu nhiên (stochastic policy) $\pi_\theta(a\mid s)$ khả vi theo $\theta\in\Theta$ mở.
  - (PT): $\mathbb E[r_t\mid S_t=s,A_t=a]=r(s,a)$.
  - Chính sách bảng (tabular policy): $\pi_\theta(1\mid s)=1/(1+e^{-\theta_s})$; $\mathbb 1[\theta_s>0]$ không khả vi.
- **Ghi chú diễn giả:** Tên "Markov" chỉ việc phân bố của trạng thái kế tiếp chỉ phụ thuộc trạng thái và hành động hiện tại. $\mu_0$ là phân bố của trạng thái đầu, $P(s'\mid s,a)$ là xác suất tới $s'$ khi chọn $a$ ở $s$; cả hai cố định, không phụ thuộc tham số của chính sách. Dưới (PT), phân bố của $r_t$ khi biết $(S_t,A_t)$ không phụ thuộc $\theta$ và $r_t$ không ảnh hưởng tới các bước sau; các kết quả về gradient vẫn đúng với $r(s,a)=\mathbb E[r_t\mid S_t=s,A_t=a]$, theo tính chất tháp. Ví dụ 10.1 là chính sách bảng với một trạng thái và $H=1$. Chính sách tất định không khả vi tại $\theta_s=0$, và gradient của $J$ bằng $0$ ở mọi điểm gradient tồn tại. Hệ thống đề xuất hiển thị nội dung $1$ hoặc $0$, phần thưởng bằng $1$ khi người dùng nhấp; mỗi người dùng là một lượt độc lập khi chính sách cố định. Nguồn: ghi chú Bài 10, §2, §3 (khối ứng dụng), §4, Định nghĩa 10.1.
- **Lý do / nối:** câu nối từ ví dụ mở đầu (dòng 1) → định nghĩa; ba nhãn giả thiết của Phần A → quỹ đạo.
- **Mục tiêu / nguồn:** 1; §2, §4, Định nghĩa 10.1.

#### `2-04` Quỹ đạo, tổng phần thưởng và mục tiêu của chính sách — định nghĩa (Định nghĩa 10.2) · 3 phút
- **Mặt trang:**
  - **Định nghĩa 10.2.** Quỹ đạo (trajectory) $\tau=(s_0,a_0,\ldots,s_{H-1},a_{H-1})\in\mathcal T=(\mathcal S\times\mathcal A)^H$: $S_0\sim\mu_0$, $A_t\sim\pi_\theta(\cdot\mid S_t)$, $S_{t+1}\sim P(\cdot\mid S_t,A_t)$.
  - $$p_\theta(\tau)=\mu_0(s_0)\prod_{t=0}^{H-1}\pi_\theta(a_t\mid s_t)\prod_{t=0}^{H-2}P(s_{t+1}\mid s_t,a_t)$$
  - Tổng phần thưởng (return) $R(\tau)=\sum_{t=0}^{H-1}r(s_t,a_t)$; mục tiêu $J(\theta)=\mathbb E_{\tau\sim p_\theta}R(\tau)$; đối tượng so sánh $\sup_{\theta\in\Theta}J(\theta)$.
  - **Lưu ý:** ở Bài 01, $\ell(h,z)$ phụ thuộc $h$, $D$ thì không; ở đây phân bố $p_\theta$ phụ thuộc tham số, $R(\tau)$ thì không.
- **Ghi chú diễn giả:** Bài toán tối ưu chính sách (policy optimization) là tìm $\theta$ làm $J(\theta)$ lớn nhất có thể. $J(\theta)=\sum_{\tau\in\mathcal T}p_\theta(\tau)R(\tau)$ là một tổng hữu hạn. Lấy tổng lần lượt theo $a_{H-1}$, $s_{H-1}$, …, $s_0$ cho tổng bằng $1$, nên $p_\theta$ là một hàm xác suất trên $\mathcal T$; đây là quy tắc nhân xác suất của Bài 09 (Mệnh đề 09.3) cho chuỗi trạng thái và hành động. Trạng thái $s_H$ không xuất hiện vì không có phần thưởng ở bước $H$. $R(\tau)$ thuộc $[Hr_{\min},Hr_{\max}]$, và $r_t=r(S_t,A_t)$ là phần thưởng ngẫu nhiên ở bước $t$. Nguồn: ghi chú Bài 10, §4, Định nghĩa 10.2 và đoạn sau.
- **Lý do / nối:** mục tiêu là kì vọng theo một phân bố phụ thuộc tham số (dòng "Lưu ý:") → ví dụ hai bước.
- **Mục tiêu / nguồn:** 1; Định nghĩa 10.2.

#### `2-05` Ví dụ: quá trình quyết định Markov hai bước — ví dụ (Ví dụ 10.2) · 3 phút
- **Mặt trang:**
  - **Ví dụ 10.2.** $\mathcal S=\{s_0,s_1,s_2\}$, $\mu_0(s_0)=1$, $\mathcal A=\{0,1\}$, $H=2$; từ $s_0$, hành động $1$ tới $s_1$ với xác suất $0{,}8$, hành động $0$ với xác suất $0{,}2$; chính sách bảng.
  - $r(s_0,1)=0$, $r(s_0,0)=1$; $r(s_1,1)=3$, $r(s_1,0)=1$; $r(s_2,1)=0$, $r(s_2,0)=1$.
  - Bảng (tám quỹ đạo tại $\theta=0$, xếp ngang): $a_0$ | $1$ | $1$ | $1$ | $1$ | $0$ | $0$ | $0$ | $0$; $S_1$ | $s_1$ | $s_1$ | $s_2$ | $s_2$ | $s_1$ | $s_1$ | $s_2$ | $s_2$; $a_1$ | $1$ | $0$ | $1$ | $0$ | $1$ | $0$ | $1$ | $0$; $p_0(\tau)$ | $0{,}2$ | $0{,}2$ | $0{,}05$ | $0{,}05$ | $0{,}05$ | $0{,}05$ | $0{,}2$ | $0{,}2$; $R(\tau)$ | $3$ | $1$ | $0$ | $1$ | $4$ | $2$ | $1$ | $2$
  - Bước cuối có kì vọng $2$ ở $s_1$, $\tfrac12$ ở $s_2$; chọn $1$ hay $0$ ở $s_0$ cho $1{,}7$ hay $1{,}8$; $J(0)=1{,}75$.
  - Xác suất tới $s_1$ bằng $0{,}2+0{,}6\,\pi_\theta(1\mid s_0)$: phân bố của dữ liệu ở bước sau phụ thuộc $\theta_{s_0}$.
- **Ghi chú diễn giả:** Tại $\theta=0$ mọi xác suất chọn hành động bằng $\tfrac12$; quỹ đạo $(s_0,1,s_1,1)$ có xác suất $\tfrac12\cdot0{,}8\cdot\tfrac12=0{,}2$ và tổng phần thưởng $0+3=3$. Ở $s_1$, bước cuối có kì vọng $\tfrac12\cdot3+\tfrac12\cdot1=2$; ở $s_2$, $\tfrac12$. Chọn $1$ ở $s_0$: $0+0{,}8\cdot2+0{,}2\cdot\tfrac12=1{,}7$; chọn $0$: $1+0{,}2\cdot2+0{,}8\cdot\tfrac12=1{,}8$. Tổng trên bảng cho cùng $J(0)=1{,}75$. Ở đây $s_1$, $s_2$ là tên trạng thái, còn $S_1$ là trạng thái ngẫu nhiên ở bước $1$. Mỗi số hạng của $J$ chứa xác suất của chính sách và của môi trường; tác tử biết $\pi_\theta$ nhưng không biết $\mu_0$, $P$, $r$, nên không tính được $J$ hay đạo hàm của nó bằng công thức. Nguồn: ghi chú Bài 10, §4, Ví dụ 10.2 và đoạn sau.
- **Lý do / nối:** dòng cuối và ghi chú diễn giả nêu cái còn thiếu (tác tử không tính được $J$) → mạch 3.
- **Mục tiêu / nguồn:** 1; Ví dụ 10.2.

### Mạch 3. Gradient chính sách và thuật toán REINFORCE (12 trang, 30 phút)

#### `3-00` 3. Gradient chính sách và thuật toán REINFORCE — tiêu đề mạch, điểm vào mạch 3 · 0,5 phút
- **Mặt trang:**
  - "3."; h2 "Gradient chính sách và thuật toán REINFORCE"
  - `p.strand-lead`: Gradient của tổng phần thưởng kì vọng là kì vọng của một đại lượng tính được trên quỹ đạo.
  - `p.strand-keys`: gradient log · gradient chính sách · ước lượng không chệch · REINFORCE · điểm dừng
- **Ghi chú diễn giả:** Tác tử không tính được $J$ hay $\nabla J$ bằng công thức, vì mỗi số hạng chứa $\mu_0$, $P$, $r$. Ở câu hỏi mở đầu, đạo hàm theo $q$ của trung bình các phần thưởng đã nhận bằng $0$. Để ước lượng $\nabla J(\theta)$ từ các lượt, cần viết đạo hàm của một kì vọng theo một phân bố phụ thuộc $\theta$ thành kì vọng của một đại lượng tính được trên quỹ đạo. Công cụ là gradient log của phân bố; thuật toán dùng nó là REINFORCE. Nguồn: ghi chú Bài 10, §4 đoạn cuối, §5 đoạn mở.
- **Lý do / nối:** câu nối mạch 2 → 3 trên mặt trang là dòng dẫn và dòng cuối 2-05; cái còn thiếu nêu ở ghi chú diễn giả → bổ đề.
- **Mục tiêu / nguồn:** 2; §5.

#### `3-01` Đồng nhất thức gradient log — kết quả (Bổ đề 10.3) · 3 phút
- **Mặt trang:**
  - Gradient log (score function) $\nabla_\theta\ln p_\theta$; giá (support) của $p_\theta$: các $\tau$ có $p_\theta(\tau)>0$.
  - **Bổ đề 10.3.** **Giả thiết:** $\mathcal T$ hữu hạn, không phụ thuộc $\theta$; với mỗi $\theta\in\Theta$ mở, $p_\theta$ là hàm xác suất trên $\mathcal T$; $\theta\mapsto p_\theta(\tau)$ khả vi.
  - **Bảo đảm:** đồng nhất thức, mọi $\theta\in\Theta$. (a) Trên giá, $\nabla p_\theta=p_\theta\nabla\ln p_\theta$; ngoài giá, $\nabla p_\theta=0$.
  - (b) $\mathbb E_{\tau\sim p_\theta}\nabla_\theta\ln p_\theta(\tau)=0$.
  - **Chứng minh.** (b): $0=\nabla\sum_{\tau\in\mathcal T}p_\theta(\tau)=\sum_{\tau:\,p_\theta(\tau)>0}p_\theta(\tau)\nabla\ln p_\theta(\tau)$, theo (a).
- **Ghi chú diễn giả:** Bổ đề được chứng minh đầy đủ. Phần (a): nếu $p_\theta(\tau)>0$, quy tắc dây chuyền cho $\nabla\ln p_\theta=\nabla p_\theta/p_\theta$; nếu $p_\theta(\tau)=0$, hàm không âm $\theta'\mapsto p_{\theta'}(\tau)$ đạt giá trị nhỏ nhất tại $\theta$, một điểm trong của $\Theta$ vì $\Theta$ mở, nên gradient của nó bằng $0$. Phần (b) dùng giả thiết tập giá trị: tổng bằng $1$ với mọi $\theta$ trên cùng một tập chỉ số hữu hạn, nên đạo hàm được từng số hạng. Hệ quả: tích của gradient log với một hằng số có kì vọng $0$, nên trừ một hằng số khỏi tổng phần thưởng không làm đổi kì vọng của ước lượng gradient. Nguồn: ghi chú Bài 10, §5, Bổ đề 10.3 và chứng minh.
- **Lý do / nối:** công cụ của định lý chính, với chứng minh hai dòng (mục 11, điểm 2) → ví dụ bỏ giả thiết tập giá trị.
- **Mục tiêu / nguồn:** 2; Bổ đề 10.3.

#### `3-02` Ví dụ: giá phụ thuộc tham số — ví dụ, phản ví dụ bỏ giả thiết (Ví dụ 10.3) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 10.3.** $A$ có phân bố đều trên $[0,\theta]$, $\theta>0$: mật độ $p_\theta(a)=\mathbb 1[0\le a\le\theta]/\theta$; phần thưởng $r(a)=a$.
  - Tập giá trị vô hạn; với $a>0$, $\theta\mapsto p_\theta(a)$ nhảy tại $\theta=a$.
  - Đạo hàm đúng: $J(\theta)=\mathbb EA=\theta/2$, $J'(\theta)=\tfrac12$.
  - Trên giá, $\ln p_\theta(a)=-\ln\theta$: kì vọng gradient log bằng $-1/\theta\ne0$, nên (b) sai.
  - $\mathbb E[A\cdot(-1/\theta)]=-\tfrac12$, ngược dấu với $J'(\theta)$.
  - **Diễn giải:** giá nhận thêm khối lượng xác suất ở đầu mút; gradient log bỏ sót phần này.
- **Ghi chú diễn giả:** Ví dụ bỏ cả hai giả thiết về tập giá trị: tập giá trị vô hạn, và giá phụ thuộc $\theta$. Gradient log chỉ đo thay đổi của mật độ bên trong giá; ở đây mật độ trên giá giảm khi $\theta$ tăng, nên gradient log âm, trong khi phần thưởng kì vọng tăng vì khối lượng xác suất dời tới các giá trị lớn hơn ở đầu mút. Ước lượng ngược dấu với đạo hàm. Nguồn: ghi chú Bài 10, §5, Ví dụ 10.3.
- **Lý do / nối:** kiểm tra giả thiết của bổ đề bằng phản ví dụ (bước "bỏ giả thiết" của hành trình) → định lý.
- **Mục tiêu / nguồn:** 2; Ví dụ 10.3.

#### `3-03` Gradient của mục tiêu chính sách theo quỹ đạo — trực quan, kết quả (Định lý 10.4) · 3 phút
- **Mặt trang:**
  - **Trực quan.** Trong $p_\theta(\tau)$ chỉ các thừa số $\pi_\theta(a_t\mid s_t)$ chứa $\theta$; lôgarit biến tích thành tổng.
  - **Định lý 10.4.** **Giả thiết:** (MDP), (Π); $\tau=(S_0,A_0,\ldots,S_{H-1},A_{H-1})\sim p_\theta$ như Định nghĩa 10.2. Đặt
  - $$\hat g(\tau)=R(\tau)\sum_{t=0}^{H-1}\nabla_\theta\ln\pi_\theta(A_t\mid S_t)$$
  - **Bảo đảm:** đồng nhất thức, mọi $\theta\in\Theta$: $J$ khả vi và $\nabla J(\theta)=\mathbb E_{\tau\sim p_\theta}\hat g(\tau)$.
  - Một lượt: không chệch; $m$ lượt độc lập: hiệp phương sai chia cho $m$.
  - Ước lượng không cần $\mu_0$, $P$, $r$.
- **Ghi chú diễn giả:** Định lý được chứng minh đầy đủ. Đại lượng $\nabla_\theta\ln\pi_\theta(A_t\mid S_t)$ xác định với xác suất $1$, vì $A_t$ chỉ nhận các giá trị có $\pi_\theta(A_t\mid S_t)>0$. Ước lượng chỉ cần $R(\tau)$, quan sát được, và gradient log của chính sách, tính được từ $\pi_\theta$. Gradient chính sách (policy gradient) là tên của $\nabla J$ viết theo cách này. Nguồn: ghi chú Bài 10, §5, Định lý 10.4 và đoạn sau.
- **Lý do / nối:** trực quan và phát biểu chung trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 2; Định lý 10.4.

#### `3-04` Ý tưởng chứng minh: gradient theo quỹ đạo — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  1. ($\mathcal S$, $\mathcal A$, $H$ hữu hạn; (Π)) $J=\sum_\tau p_\theta(\tau)R(\tau)$ là tổng hữu hạn hàm khả vi: $\nabla J=\sum_\tau R(\tau)\nabla p_\theta(\tau)$.
  2. (Bổ đề 10.3(a)) Bỏ các $\tau$ ngoài giá, thay $\nabla p_\theta=p_\theta\nabla\ln p_\theta$: $\nabla J=\mathbb E[R(\tau)\nabla\ln p_\theta(\tau)]$.
  3. ((MDP)) $\ln p_\theta(\tau)=\ln\mu_0(s_0)+\sum_t\ln\pi_\theta(a_t\mid s_t)+\sum_t\ln P(s_{t+1}\mid s_t,a_t)$; số hạng đầu và cuối không chứa $\theta$.
  - Bỏ (MDP): bước 3 còn số hạng $\nabla\ln P$.
  - Trung bình phần thưởng đã thu có đạo hàm $0$: thiếu thừa số gradient log.
- **Ghi chú diễn giả:** Đồng nhất thức then chốt là $\nabla p_\theta=p_\theta\nabla\ln p_\theta$ trên giá. Bước 1 dùng tính hữu hạn: mỗi $p_\theta(\tau)$ là tích các hàm khả vi $\pi_\theta(a_t\mid s_t)$ với các hằng số, nên $J$ khả vi và đạo hàm được từng số hạng. Bước 2 dùng Bổ đề 10.3(a): các quỹ đạo ngoài giá có $\nabla p_\theta=0$. Bước 3 dùng (MDP): trên giá, mọi thừa số của $p_\theta(\tau)$ dương và vẫn dương với tham số gần $\theta$ vì chúng liên tục, nên lấy được lôgarit; $\mu_0$ và $P$ không phụ thuộc $\theta$, nên $\nabla\ln p_\theta(\tau)=\sum_t\nabla\ln\pi_\theta(a_t\mid s_t)$. Thừa số gradient log mang ảnh hưởng của $\theta$ lên phân bố dữ liệu; trung bình thực nghiệm của câu hỏi mở đầu bỏ qua ảnh hưởng đó. Nguồn: ghi chú Bài 10, §5, chứng minh Định lý 10.4.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; giả thiết vào ở từng bước; chỗ hỏng khi bỏ (MDP) → kỹ thuật.
- **Mục tiêu / nguồn:** 2; chứng minh Định lý 10.4.

#### `3-05` Đạo hàm của kì vọng qua gradient log — kỹ thuật (trang riêng), nhận xét (Nhận xét 10.5) · 2,5 phút
- **Mặt trang:**
  - **Kỹ thuật.** $\nabla_\theta\mathbb E_{\tau\sim p_\theta}f(\tau)=\mathbb E_{\tau\sim p_\theta}\big[f(\tau)\nabla_\theta\ln p_\theta(\tau)\big]$ khi $f$ không phụ thuộc $\theta$.
  - Dùng khi phân bố phụ thuộc tham số, hàm thì không (Định lý 10.4).
  - Tập vô hạn (Nhận xét 10.5): mật độ theo độ đo nền cố định, khả vi liên tục, hàm trội.
  - **Nhắc lại:** đổi chỗ đạo hàm và kì vọng (Bài 09).
  - Hỏng khi giá di chuyển theo $\theta$ (Ví dụ 10.3).
- **Ghi chú diễn giả:** Với tập hữu hạn không phụ thuộc $\theta$, kỹ thuật là đạo hàm một tổng hữu hạn rồi dùng Bổ đề 10.3(a). Khi trạng thái hay hành động liên tục, tổng thành tích phân, và Nhận xét 10.5 (chứng minh đầy đủ ở Phụ lục A) cần: phần thưởng bị chặn; mật độ $p_\theta(\tau)$ theo một độ đo nền không phụ thuộc $\theta$; $\theta\mapsto p_\theta(\tau)$ khả vi liên tục; quanh mỗi $\theta_0$ một hàm khả tích $\Lambda$ chặn $\lvert R(\tau)\rvert\lVert\nabla_\theta p_\theta(\tau)\rVert$. Chứng minh lặp lại kỹ thuật của Bài 09: định lý giá trị trung bình trên từng $\tau$, hàm trội, hội tụ bị chặn. Chính sách Gauss $A_t\sim N(\mu_\theta(S_t),\omega^2)$ với $\mu_\theta$ khả vi liên tục và $\omega>0$ cố định thỏa ba điều kiện. Ví dụ 10.3 vi phạm điều kiện khả vi. Ở Bài 09, ước lượng gradient log dùng đúng dạng này. Nguồn: ghi chú Bài 10, §5, Nhận xét 10.5; Phụ lục A.
- **Lý do / nối:** kỹ thuật nền tảng của Phần A có trang "Kỹ thuật." riêng, tiêu đề là tên kỹ thuật (mục 11, điểm 4; mục 14) → ví dụ bandit.
- **Mục tiêu / nguồn:** 2; Nhận xét 10.5, Phụ lục A.

#### `3-06` Ví dụ: gradient chính sách trên bài toán bandit — ví dụ (Ví dụ 10.4) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 10.4.** Ví dụ 10.1 tại $\theta=\ln3$: $\pi_\theta(1)=\tfrac34$, $J'=\tfrac38$; một lượt là một hành động $A$, $H=1$.
  - Gradient log: $\tfrac{d}{d\theta}\ln\pi_\theta(1)=\tfrac14$, $\tfrac{d}{d\theta}\ln\pi_\theta(0)=-\tfrac34$; gộp lại: $A-\pi_\theta(1)$.
  - $\hat g=r(A)(A-\tfrac34)$: $0{,}75$ khi $A=1$ (xác suất $\tfrac34$); $-0{,}75$ khi $A=0$ (xác suất $\tfrac14$).
  - $$\mathbb E\hat g=\tfrac34\cdot0{,}75+\tfrac14\cdot(-0{,}75)=0{,}375=\tfrac38$$
  - Kì vọng gradient log: $\tfrac34\cdot\tfrac14+\tfrac14\cdot(-\tfrac34)=0$ (Bổ đề 10.3(b)).
  - **Diễn giải:** mỗi lần rút, $\lvert\hat g\rvert=0{,}75$, gấp đôi $\tfrac38$; với xác suất $\tfrac14$, $\hat g$ ngược dấu với đạo hàm.
- **Ghi chú diễn giả:** Gradient log dùng câu ôn nhanh 2: $\frac{d}{d\theta}\ln\pi_\theta(1)=1-\pi_\theta(1)$ và $\frac{d}{d\theta}\ln\pi_\theta(0)=-\pi_\theta(1)$; gộp hai trường hợp được $A-\pi_\theta(1)$. Kì vọng của ước lượng đúng bằng đạo hàm trực tiếp của Ví dụ 10.1, nhưng một lần rút cho giá trị lớn gấp đôi về độ lớn, và một phần tư số lần rút cho dấu sai. Nguồn: ghi chú Bài 10, §5, Ví dụ 10.4.
- **Lý do / nối:** kiểm định lý bằng đạo hàm trực tiếp (mục tiêu 2); số $\pm0{,}75$ là vấn đề của mạch 4 → ví dụ hai bước.
- **Mục tiêu / nguồn:** 2; Ví dụ 10.4.

#### `3-07` Ví dụ: gradient của quá trình hai bước — ví dụ (Ví dụ 10.5) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 10.5.** Ví dụ 10.2, $\theta=0$; tọa độ $\theta_s$ của gradient log bằng $a-\tfrac12$, các tọa độ khác bằng $0$.
  - Tổng $p_0(\tau)R(\tau)$: $0{,}85$ trên bốn quỹ đạo có $a_0=1$, $0{,}9$ trên bốn quỹ đạo có $a_0=0$.
  - $$\frac{\partial J}{\partial\theta_{s_0}}=\tfrac12\cdot0{,}85-\tfrac12\cdot0{,}9=-0{,}025$$
  - $\theta_{s_1}$: $0{,}3-0{,}1+0{,}1-0{,}05=0{,}25$; $\theta_{s_2}$: $0-0{,}025+0{,}1-0{,}2=-0{,}125$.
  - Sai phân hữu hạn của $J$ cho cùng véc-tơ $(-0{,}025;\,0{,}25;\,-0{,}125)$.
  - **Diễn giải:** hành động $1$ mất $1$ ở bước đầu, chỉ được thêm $(0{,}8-0{,}2)(2-\tfrac12)=0{,}9$ ở bước sau: $\tfrac14(1{,}7-1{,}8)=-0{,}025$.
- **Ghi chú diễn giả:** Theo Định lý 10.4, tọa độ $\theta_{s_0}$ bằng $\sum_\tau p_0(\tau)R(\tau)(a_0-\tfrac12)$, dùng bảng tám quỹ đạo của Ví dụ 10.2. Tọa độ $\theta_{s_1}$ chỉ khác $0$ trên bốn quỹ đạo qua $s_1$, với thừa số $a_1-\tfrac12$; ví dụ, quỹ đạo $(s_0,1,s_1,1)$ góp $0{,}2\cdot3\cdot\tfrac12=0{,}3$. Hành động $1$ dẫn tới $s_1$, nơi có phần thưởng $3$, nhưng tăng $\theta_{s_0}$ làm $J$ giảm, vì khoản mất ở bước đầu lớn hơn khoản được thêm ở bước sau. Phép kiểm bằng sai phân hữu hạn dùng công thức của $J$, mà tác tử không có; ước lượng chỉ dùng các lượt. Nguồn: ghi chú Bài 10, §5, Ví dụ 10.5.
- **Lý do / nối:** kiểm định lý trên MDP nhiều bước; véc-tơ gradient dùng lại ở 4-05 và 4-08 → bỏ giả thiết luật chuyển.
- **Mục tiêu / nguồn:** 2; Ví dụ 10.5.

#### `3-08` Ví dụ: luật chuyển phụ thuộc tham số — ví dụ, phản ví dụ bỏ (MDP) (Ví dụ 10.6) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 10.6.** Như Ví dụ 10.2, nhưng từ $s_0$, với mọi hành động, robot tới $s_1$ với xác suất $q=1/(1+e^{-\theta_{s_0}})$; $\theta=0$, $q=\tfrac12$.
  - Đạo hàm đúng theo $\theta_{s_0}$: bước đầu $-\tfrac14$; bước sau $\tfrac32q(1-q)=0{,}375$; tổng $0{,}125$.
  - Ước lượng của Định lý 10.4: $(r_0+r_1)(A_0-\tfrac12)$; $r_1$ độc lập với $A_0$, nên kì vọng bằng $\mathbb E[r_0(A_0-\tfrac12)]=-0{,}25$.
  - **Kết luận:** ngược dấu đạo hàm thật: thiếu gradient của $\ln P(S_1\mid s_0,A_0)$ (bước 3 của chứng minh).
- **Ghi chú diễn giả:** Tham số $\theta_{s_0}$ điều khiển cả động cơ, nên luật chuyển phụ thuộc tham số, trái (MDP). Tại $\theta=0$, $J=\tfrac12+\tfrac54=1{,}75$. Phần thưởng ở bước đầu có kì vọng $1-\pi_\theta(1\mid s_0)$, đạo hàm $-\tfrac14$; phần thưởng ở bước sau có kì vọng $2q+\tfrac12(1-q)$, đạo hàm $\tfrac32q(1-q)$. Vì $S_1$ không phụ thuộc $A_0$, $r_1$ độc lập với $A_0$ và số hạng của nó có kì vọng $0$; ước lượng chỉ thấy khoản mất ở bước đầu. Đây cũng là câu trả lời cho câu hỏi cuối buổi (c): không dùng được Thuật toán 10.6 mà không sửa. Nguồn: ghi chú Bài 10, §5, Ví dụ 10.6; §12 (c).
- **Lý do / nối:** phản ví dụ khi bỏ (MDP), giả thiết dùng ở bước 3 (bản giao việc: không chuyển kết quả khi không có lập luận mới) → thuật toán.
- **Mục tiêu / nguồn:** 2, 5; Ví dụ 10.6.

#### `3-09` Thuật toán REINFORCE — thuật toán (Thuật toán 10.6) · 2,5 phút
- **Mặt trang:**
  - **Thuật toán 10.6.** Môi trường chưa biết; $\Theta$ là cả không gian tham số; $\eta_1,\ldots,\eta_T>0$ và $\theta_1$ tất định.
  - Với $j=1,\ldots,T$: chạy $\pi_{\theta_j}$ một lượt, được $\tau_j$; tính $\hat g_j=R(\tau_j)\sum_t\nabla\ln\pi_{\theta_j}(A_t\mid S_t)$; đặt $\theta_{j+1}=\theta_j+\eta_j\hat g_j$.
  - Khi biết $\tau_1,\ldots,\tau_{j-1}$: $\theta_j$ cố định và $\tau_j\sim p_{\theta_j}$, nên $\mathbb E[\hat g_j\mid\tau_1,\ldots,\tau_{j-1}]=\nabla J(\theta_j)$.
  - Đây là điều kiện không chệch của Bài 05, dạng đi lên; thiếu (C): Định lý 05.14 cần $-J$ lồi.
- **Ghi chú diễn giả:** REINFORCE dùng ước lượng của Định lý 10.4 với tham số mới sau mỗi lượt; đầu ra là $\theta_{T+1}$, và thuật toán không cần mô hình của môi trường. Chính sách là họ $\pi_\theta$ của Định nghĩa 10.1 với $\Theta$ là cả không gian tham số, như chính sách bảng. Viết mỗi lượt thành hàm của $\theta_j$ và một biến ngẫu nhiên $\xi_j$, với $\xi_1,\xi_2,\ldots$ độc lập cùng phân bố, ta được nguồn ngẫu nhiên và ánh xạ oracle như Định nghĩa 05.10 (Bài tập 10.3). Các lượt không độc lập cùng phân bố: lượt thứ $j$ phụ thuộc các lượt trước qua $\theta_j$. Nguồn: ghi chú Bài 10, §5, Thuật toán 10.6 và đoạn sau.
- **Lý do / nối:** thuật toán và giả thiết còn thiếu (C) → ví dụ mục tiêu không lõm.
- **Mục tiêu / nguồn:** 1, 5; Thuật toán 10.6.

#### `3-10` Ví dụ: điểm dừng là điểm cực tiểu — ví dụ (Ví dụ 10.7) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 10.7.** $H=2$; từ $s_0$, hành động $1$ tới $s_1$, $0$ tới $s_2$; $r(s_1,1)=1$, $r(s_2,0)=0{,}6$, còn lại $0$.
  - Một tham số chung: $\pi_\theta(1\mid s)=q=1/(1+e^{-\theta})$; $J=q^2+0{,}6(1-q)^2$.
  - $dJ/dq=3{,}2q-1{,}2=0$ tại $q=0{,}375$ ($\theta=\ln0{,}6$); $J$ lồi theo $q$: điểm cực tiểu, $J=0{,}375$.
  - Đi lên theo gradient đúng: từ $\theta=-1$, $J\to0{,}6$; từ $\theta=-0{,}4$, $J\to1$.
  - **Nhắc lại:** Mệnh đề 08.12 cho $F=-J$ điểm dừng xấp xỉ khi $J$ $\beta$-trơn, bị chặn trên, phương sai có điều kiện bị chặn, $\eta\le1/\beta$.
- **Ghi chú diễn giả:** Tác tử không phân biệt được các trạng thái, chẳng hạn vì cảm biến cho cùng một số đo, nên dùng một tham số chung. Cận trên đúng $1$ không đạt. Phần thưởng $1$ cần chọn hành động $1$ hai lần, phần thưởng $0{,}6$ cần chọn hành động $0$ hai lần. Vì $dJ/d\theta=(dJ/dq)\,q(1-q)$, đạo hàm theo $\theta$ cũng bằng $0$ tại $\theta\approx-0{,}5108$, và đạo hàm bậc hai theo $\theta$ ở đó bằng $3{,}2(q(1-q))^2\approx0{,}1758>0$. Hàm $-J$ không lồi theo $\theta$, nên Định lý 05.14 không áp dụng, và kết quả phụ thuộc điểm xuất phát. Chứng minh Mệnh đề 08.12 chỉ dùng kì vọng và phương sai có điều kiện theo lịch sử, ở đây là các lượt trước; mệnh đề bảo đảm điểm dừng xấp xỉ, đúng loại điểm của ví dụ này. Nguồn: ghi chú Bài 10, §5, Ví dụ 10.7.
- **Lý do / nối:** giới hạn "mục tiêu không lõm" và chỗ duy nhất có bảo đảm tối ưu (Mệnh đề 08.12) → bài tập.
- **Mục tiêu / nguồn:** 5; Ví dụ 10.7.

#### `3-11` Bài tập: thuật toán REINFORCE cho bài toán bandit — bài tập (Bài tập 10.1(a), (b)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 10.1.** Bandit với chính sách sigmoid, $r(1)=4$, $r(0)=0$, tại $\theta=-\ln3$.
  - (a) Tính $\pi_\theta(1)$, $J(\theta)$ và $J'(\theta)$ bằng đạo hàm trực tiếp.
  - (b) Viết $\hat g$ của Định lý 10.4 cho một lượt; liệt kê giá trị cùng xác suất, kiểm kì vọng bằng $J'(\theta)$, tính phương sai.
  - [f] **Lời giải:** (a) $e^{-\theta}=3$, $\pi_\theta(1)=\tfrac14$; $J=4\cdot\tfrac14=1$; $J'=4\cdot\tfrac14\cdot\tfrac34=\tfrac34$.
  - [f] (b) $\hat g=r(A)(A-\tfrac14)$: $3$ (xác suất $\tfrac14$), $0$ (xác suất $\tfrac34$); $\mathbb E\hat g=\tfrac34=J'$; $\operatorname{Var}\hat g=\tfrac14\cdot9-\tfrac9{16}=\tfrac{27}{16}$.
- **Ghi chú diễn giả:** Câu chữ đầy đủ của đề: "Xét bài toán bandit hai hành động với chính sách sigmoid, phần thưởng tất định $r(1)=4$, $r(0)=0$, tại $\theta=-\ln3$. (a) Tính $\pi_\theta(1)$, $J(\theta)$ và $J'(\theta)$ bằng đạo hàm trực tiếp. (b) Viết ước lượng $\hat g$ của Định lý 10.4 cho một lượt. Liệt kê các giá trị của nó cùng xác suất, kiểm rằng kì vọng bằng $J'(\theta)$, và tính phương sai." Với $H=1$, $R(\tau)=r(A)$ và gradient log bằng $A-\tfrac14$. Khi $A=0$, phần thưởng bằng $0$, nên ước lượng bằng $0$ với xác suất $\tfrac34$: ba phần tư số bước cập nhật không đổi tham số. Phương sai $\tfrac{27}{16}$ lớn gấp ba lần bình phương đạo hàm $\tfrac9{16}$. Các phần (c)–(f) là bài về nhà. Nguồn: tệp bài tập, Bài tập 10.1(a), (b) và lời giải.
- **Lý do / nối:** bài tập của mạch 3, kiểm định lý bằng đạo hàm trực tiếp; mở câu hỏi phương sai → mạch 4.
- **Mục tiêu / nguồn:** 2; Bài tập 10.1(a), (b).

### Mạch 4. Giá trị nền và phương sai của ước lượng gradient (9 trang, 24 phút)

#### `4-00` 4. Giá trị nền và phương sai của ước lượng gradient — tiêu đề mạch, điểm vào mạch 4 · 0,5 phút
- **Mặt trang:**
  - "4."; h2 "Giá trị nền và phương sai của ước lượng gradient"
  - `p.strand-lead`: Trừ một giá trị nền theo lịch sử không đổi kì vọng của ước lượng nhưng đổi phương sai.
  - `p.strand-keys`: tổng phần thưởng từ bước $t$ · lịch sử · giá trị nền · phương sai · chính sách cố định
- **Ghi chú diễn giả:** Ước lượng của Định lý 10.4 không chệch nhưng nhiễu: trong bài toán bandit, đạo hàm bằng $\tfrac38$ còn ước lượng nhận $\pm0{,}75$. Hai cách sửa giữ nguyên kì vọng và có thể giảm phương sai: bỏ các phần thưởng nhận trước một hành động khỏi số hạng của hành động đó, và trừ một giá trị nền. Đánh giá một chính sách cố định là chỗ duy nhất của Phần A có cận với xác suất cao. Nguồn: ghi chú Bài 10, §6 đoạn mở, đoạn trước Ví dụ 10.12.
- **Lý do / nối:** câu nối mạch 3 → 4: dòng đầu 4-01 ($\pm0{,}75$ quanh $\tfrac38$) → mệnh đề.
- **Mục tiêu / nguồn:** 3; §6.

#### `4-01` Tổng phần thưởng từ bước $t$ — định nghĩa, trực quan, kết quả (Mệnh đề 10.7) · 3 phút
- **Mặt trang:**
  - Ví dụ 10.4: $\hat g=\pm0{,}75$ trong khi đạo hàm là $\tfrac38$.
  - Tổng phần thưởng từ bước $t$ (reward-to-go) $R_{\ge t}=\sum_{t'=t}^{H-1}r_{t'}$; lịch sử (history) $\mathcal F_t=(S_0,A_0,\ldots,A_{t-1},S_t)$.
  - **Trực quan.** Hành động ở bước $t$ không ảnh hưởng tới phần thưởng nhận trước nó.
  - **Mệnh đề 10.7.** **Giả thiết:** như Định lý 10.4. **Bảo đảm:** đồng nhất thức, mọi $\theta\in\Theta$. (a) Với $t'<t$, $\mathbb E\big[r_{t'}\nabla\ln\pi_\theta(A_t\mid S_t)\big]=0$. (b)
  - $$\nabla J(\theta)=\mathbb E\sum_{t=0}^{H-1}R_{\ge t}\,\nabla\ln\pi_\theta(A_t\mid S_t)$$
- **Ghi chú diễn giả:** Mệnh đề được trình bày ở mức phác thảo, chi tiết ở Phụ lục B. $R_{\ge0}=R(\tau)$. Lịch sử đến bước $t$ gồm các biến quan sát được trước $A_t$. Chính sách chỉ nhìn trạng thái hiện tại, nên khi biết $\mathcal F_t$, hành động $A_t$ có phân bố $\pi_\theta(\cdot\mid S_t)$. Các phần thưởng nhận trước $A_t$ không chứa thông tin về $A_t$, nên trong số hạng của $A_t$ chúng chỉ thêm nhiễu. Sutton và Barto viết $G_t$ cho tổng phần thưởng từ bước $t$; ở đây viết $R_{\ge t}$ vì $G$ là hằng số Lipschitz từ Bài 05. Nguồn: ghi chú Bài 10, §6, Mệnh đề 10.7; §13.
- **Lý do / nối:** vấn đề (dòng 1) → định nghĩa → trực quan → phát biểu; ý tưởng chứng minh ở trang chung 4-03 (mục 11, điểm 5) → hệ quả.
- **Mục tiêu / nguồn:** 3; §6, Mệnh đề 10.7.

#### `4-02` Giá trị nền không làm đổi kì vọng của ước lượng — kết quả (Hệ quả 10.8) · 2,5 phút
- **Mặt trang:**
  - Giá trị nền (baseline): đại lượng không phụ thuộc hành động đang xét.
  - **Hệ quả 10.8.** **Giả thiết:** như Định lý 10.4; $b_t(\mathcal F_t)$ là hàm của lịch sử, không phụ thuộc $A_t$ hay các biến sau $A_t$.
  - **Bảo đảm:** đồng nhất thức, mọi $\theta\in\Theta$:
  - $$\nabla J(\theta)=\mathbb E\sum_{t=0}^{H-1}\big(R_{\ge t}-b_t(\mathcal F_t)\big)\nabla\ln\pi_\theta(A_t\mid S_t)$$
  - Chọn $b_t$ để giảm phương sai; một $b_t$ tùy ý có thể tăng phương sai.
- **Ghi chú diễn giả:** Hệ quả được chứng minh đầy đủ. Ví dụ thường gặp: $b_t(\mathcal F_t)=b(S_t)$, một hàm của trạng thái hiện tại; hằng số cũng là một giá trị nền. Điều kiện "là hàm của lịch sử trước hành động" là điều kiện cho ước lượng lấy mẫu; giá trị nền dùng hành động hay phần thưởng từ bước $t$ trở đi của chính lượt đang dùng, như $R(\tau)$ hay $r(A_t)$, vi phạm điều kiện này. Phần thưởng nhận trước bước $t$ thì hợp lệ, và trung bình phần thưởng của các lượt trước cũng hợp lệ, vì nó là hằng số khi biết các lượt đó (Nhận xét 10.9(ii)). Nguồn: ghi chú Bài 10, §6, Hệ quả 10.8; Nhận xét 10.9(ii).
- **Lý do / nối:** phát biểu thứ hai trước trang ý tưởng chứng minh chung → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 3; Hệ quả 10.8.

#### `4-03` Ý tưởng chứng minh: tổng phần thưởng từ bước $t$ và giá trị nền — ý tưởng chứng minh (Mệnh đề 10.7, Hệ quả 10.8; Phụ lục B) · 3 phút
- **Mặt trang:**
  - **Nhắc lại:** kì vọng có điều kiện theo lịch sử (Bài 05).
  1. (chính sách chỉ nhìn $S_t$; Bổ đề 10.3) Khi biết $\mathcal F_t$, $A_t\sim\pi_\theta(\cdot\mid S_t)$: $\mathbb E[\nabla\ln\pi_\theta(A_t\mid S_t)\mid\mathcal F_t]=\sum_a\nabla\pi_\theta(a\mid S_t)=0$.
  2. (tính chất tháp) Với $f$ là hàm của $\mathcal F_t$: $\mathbb E\big[f(\mathcal F_t)\nabla\ln\pi_\theta(A_t\mid S_t)\big]=0$.
  3. $f=r_{t'}$, $t'<t$: Mệnh đề 10.7(a); viết $R(\tau)=\sum_{t'<t}r_{t'}+R_{\ge t}$ được (b). $f=b_t$: Hệ quả 10.8.
  - Giá trị nền phụ thuộc $A_t$: bước 2 hỏng.
- **Ghi chú diễn giả:** Đồng nhất thức then chốt là $\sum_a\nabla\pi_\theta(a\mid s)=\nabla1=0$, tức Bổ đề 10.3(b) cho họ $\pi_\theta(\cdot\mid s)$ trên tập hữu hạn $\mathcal A$. Bước 1 dùng giả thiết chính sách chỉ phụ thuộc trạng thái hiện tại: thừa số của $a_t$ trong $p_\theta(\tau)$ là $\pi_\theta(a_t\mid s_t)$, không phụ thuộc phần còn lại của lịch sử, và tổng theo phần sau của quỹ đạo bằng $1$. Bước 2: $f(\mathcal F_t)$ đã biết khi biết lịch sử, nên đưa ra ngoài kì vọng có điều kiện; theo Bước 1, phần còn lại bằng $0$. Bước 3: với $t'<t$, $r_{t'}=r(S_{t'},A_{t'})$ là hàm của $\mathcal F_t$; bỏ các số hạng có kì vọng $0$ khỏi số hạng thứ $t$ của Định lý 10.4. Với giá trị nền, giả thiết "hàm của lịch sử" vào ở Bước 2; một giá trị nền phụ thuộc $A_t$ không đưa ra ngoài được. Chứng minh chỉ dùng việc chính sách chọn $a_t$ theo trạng thái hiện tại và tính hữu hạn của các tập. Nguồn: ghi chú Bài 10, §6, chứng minh Mệnh đề 10.7, Hệ quả 10.8; Phụ lục B.
- **Lý do / nối:** một trang ý tưởng chứng minh cho hai kết quả có chung bước then chốt (Phụ lục B, Bước 4) → ví dụ phương sai.
- **Mục tiêu / nguồn:** 3; Phụ lục B.

#### `4-04` Ví dụ: phương sai theo giá trị nền và giá trị nền gây chệch — ví dụ (Ví dụ 10.8, 10.9), hình F1 · 3 phút
- **Mặt trang:**
  - **Ví dụ 10.8.** Ví dụ 10.4; với hằng số $b$, $\hat g_b=(r(A)-b)(A-\tfrac34)$ có kì vọng $\tfrac38$ (Hệ quả 10.8).
  - {{`grid2`: bảng bên trái, hình F1 bên phải}} Bảng: $b$ | $A=1$ | $A=0$ | $\operatorname{Var}\hat g_b$; $0$ | $\tfrac34$ | $-\tfrac34$ | $\tfrac{27}{64}$; $\tfrac52$ | $\tfrac18$ | $\tfrac98$ | $\tfrac3{16}$; $\tfrac32$ | $\tfrac38$ | $\tfrac38$ | $0$; $5$ | $-\tfrac12$ | $3$ | $\tfrac{147}{64}$
  - Hình F1, chú thích: Phương sai của $\hat g_b$ theo $b$; bốn điểm của bảng.
  - $b^*=\tfrac32$ cho phương sai $0$; $b=J=\tfrac52$ không tốt nhất; $b=5$ tăng phương sai hơn năm lần.
  - **Ví dụ 10.9.** Giá trị nền $\kappa A$ phụ thuộc hành động: kì vọng $\tfrac38-\tfrac{3\kappa}{16}$, bằng $0$ khi $\kappa=2$.
- **Ghi chú diễn giả:** $\hat g_b$ bằng $(3-b)\cdot\tfrac14$ với xác suất $\tfrac34$ và $(1-b)(-\tfrac34)$ với xác suất $\tfrac14$; phương sai là $\tfrac34(\tfrac{3-b}4)^2+\tfrac14(\tfrac{3(1-b)}4)^2-(\tfrac38)^2$, một hàm bậc hai của $b$. Đạo hàm theo $b$ bằng $0$ tại $b^*=r(1)(1-\pi_\theta(1))+r(0)\pi_\theta(1)=\tfrac32$. Ở Ví dụ 10.9, $\mathbb E[A(A-\tfrac34)]=\tfrac3{16}$; với giá trị nền bằng chính $r(A)$, ước lượng luôn bằng $0$. Giá trị nền $\kappa A$ không là hàm của lịch sử trước hành động, nên bước 2 của chứng minh hỏng. Khi giá trị nền có tham số riêng, cố định khi sinh lượt, ước lượng vẫn không chệch; nếu nó dùng chung tham số với chính sách và được lấy đạo hàm cùng, gradient có thêm một số hạng có kì vọng bằng gradient của giá trị nền nhân entropy, $\ln2\approx0{,}6931$ trong bài toán bandit tại $\theta=0$ với $b_\theta=\theta$ (Nhận xét 10.9(i)). Nguồn: ghi chú Bài 10, §6, Ví dụ 10.8, 10.9, Nhận xét 10.9.
- **Lý do / nối:** cùng kì vọng, bốn phương sai (trọng tâm trực quan 3); phản ví dụ bỏ giả thiết của Hệ quả 10.8 → MDP hai bước.
- **Mục tiêu / nguồn:** 3; Ví dụ 10.8, 10.9.

#### `4-05` Ví dụ: tổng phần thưởng từ bước $t$ trên quá trình hai bước — ví dụ (Ví dụ 10.10) · 3 phút
- **Mặt trang:**
  - **Ví dụ 10.10.** Ví dụ 10.2, $\theta=0$: (i) Định lý 10.4; (ii) Mệnh đề 10.7(b); (iii) (ii) trừ $b_t=1{,}75;\,2;\,\tfrac12$ ở $s_0,s_1,s_2$.
  - Cả ba có kì vọng $(-0{,}025;\,0{,}25;\,-0{,}125)$.
  - Bảng (phương sai): | $\theta_{s_0}$ | $\theta_{s_1}$ | $\theta_{s_2}$ | Vết; (i) | $\tfrac{1619}{1600}$ | $\tfrac{11}{16}$ | $\tfrac{79}{320}$ | $1{,}94625$; (ii) | $\tfrac{1619}{1600}$ | $\tfrac9{16}$ | $\tfrac3{64}$ | $1{,}62125$; (iii) | $\tfrac{197}{800}$ | $\tfrac1{16}$ | $\tfrac1{64}$ | $0{,}324375$
  - Giá trị nền theo trạng thái giảm vết sáu lần so với (i).
  - Đổi ví dụ ($r=-2$ ở $s_0$, luôn tới $s_1$): phương sai của (i) là $0$, của (ii) là $1$.
- **Ghi chú diễn giả:** Giá trị nền của (iii) là tổng phần thưởng kì vọng còn lại từ trạng thái hiện tại, lấy từ Ví dụ 10.2. Vết của ma trận hiệp phương sai là tổng ba phương sai. Cột $\theta_{s_0}$ của (i) và (ii) trùng nhau vì $R_{\ge0}=R(\tau)$; so với (ii), giá trị nền giảm vết khoảng năm lần. Trong ví dụ đổi, xác suất chọn ở $s_0$ không phụ thuộc $\theta$, ở $s_1$ phần thưởng là $3$ và $1$; ước lượng (i) bằng $(-2+3)\cdot\tfrac12$ hoặc $(-2+1)(-\tfrac12)$, đều bằng $\tfrac12$. Phần thưởng $-2$ ở bước đầu đóng vai giá trị nền tốt nhất cho bước sau, $b^*=2$ theo công thức của Ví dụ 10.8; bỏ nó, như (ii), làm phương sai tăng. Với cùng một kì vọng, phương sai có thể giảm hoặc tăng tùy bài toán. Nguồn: ghi chú Bài 10, §6, Ví dụ 10.10; Nhận xét 10.9(ii).
- **Lý do / nối:** cả giảm và tăng phương sai trên cùng MDP (mục 11, điểm 6) → dịch phần thưởng.
- **Mục tiêu / nguồn:** 3; Ví dụ 10.10.

#### `4-06` Ví dụ: dịch phần thưởng trong bài toán đề xuất — ví dụ (khối ứng dụng §3, Ví dụ 10.11) · 3 phút
- **Mặt trang:**
  - **Câu hỏi:** cộng $c=10$ vào mỗi phần thưởng thì điều gì thay đổi?
  - **Ví dụ 10.11.** $R(\tau)=c+X$, nhấp $X\in\{0,1\}$; $(R(\tau)-b)(A-\tfrac12)$ không chệch theo Hệ quả 10.8 dưới (PT).
  - $J(\theta)=c+0{,}6\,\pi_\theta(1)+0{,}4\,(1-\pi_\theta(1))$: $J'(0)=0{,}05$ với mọi $c$; chính sách tốt nhất không đổi.
  - Phương sai với $b=0$: $0{,}1225$ ($c=0$), $27{,}6225$ ($c=10$); với $b=J(0)=c+\tfrac12$: $0{,}06$.
  - Thuật toán 10.6, $c=10$, không giá trị nền: $49/100$ lần chạy kết thúc với $\pi_\theta(1)<0{,}5$.
- **Ghi chú diễn giả:** Hệ thống đề xuất hiển thị nội dung $1$ hoặc $0$; người dùng nhấp với xác suất $0{,}6$ hoặc $0{,}4$, và phần thưởng bằng nhấp cộng khoản cố định $c$. Câu (i) của khối ứng dụng hỏi có ước lượng không chệch của đạo hàm từ một lần hiển thị không: có, theo Hệ quả 10.8 dưới (PT). Vì $(A-\tfrac12)^2=\tfrac14$, phương sai khi $b=0$ bằng $\tfrac14\mathbb ER(\tau)^2-0{,}05^2$, với $\mathbb E(c+X)^2=c^2+c+\tfrac12$. Dịch phần thưởng không đổi bài toán nhưng nhân phương sai của ước lượng một lượt khoảng $225$ lần. Mô phỏng theo Phụ lục C: $\theta_1=0$, $\eta_j=0{,}1$, $T=2000$, $100$ hạt giống; giá trị nền là trung bình phần thưởng các lượt trước, hợp lệ theo Nhận xét 10.9(ii); có giá trị nền, hay với $c=0$, không lần chạy nào kết thúc dưới $0{,}5$. Nguồn: ghi chú Bài 10, §3 (khối ứng dụng), §6, Ví dụ 10.11; Phụ lục C.
- **Lý do / nối:** trả lời hai câu hỏi của khối ứng dụng; giới hạn "phương sai cao" của §10 → chính sách cố định.
- **Mục tiêu / nguồn:** 3; Ví dụ 10.11, Phụ lục C.

#### `4-07` Ví dụ: cận Hoeffding cho đánh giá một chính sách cố định — ví dụ, cận số (Ví dụ 10.12) · 3 phút
- **Mặt trang:**
  - **Ví dụ 10.12.** Ví dụ 10.2, $\theta$ cố định trước khi chạy: $m=1000$ lượt thỏa (T1); $\delta=0{,}05$; $R(\tau_j)\in[0,4]$.
  - Hệ quả 02.10(b) cho $R/4$, nhân bán kính với $4$; với xác suất ít nhất $0{,}95$,
  - $$\Big\lvert\tfrac1m\textstyle\sum_jR(\tau_j)-J(\theta)\Big\rvert\le4\sqrt{\ln40/2000}\le0{,}1718$$
  - **Nhắc lại:** đảo cận đuôi thành cỡ mẫu (Bài 02): bán kính $\le0{,}05$ cần $11\,805$ lượt.
  - $\theta$ chọn từ chính các lượt này (Thuật toán 10.6): $\theta$ không cố định, cận không áp dụng.
- **Ghi chú diễn giả:** Các kết quả trước là đồng nhất thức. Với $\theta$ cố định, $R(\tau_1),\ldots,R(\tau_m)$ độc lập cùng phân bố với kì vọng $J(\theta)$. Miền $[0,4]$ đến từ phần thưởng bước đầu trong $\{0,1\}$ và bước sau trong $\{0,1,3\}$; bán kính cho miền $[a,b]$ nhân thêm $b-a$ (đoạn sau Nhận xét 02.8). Cỡ mẫu: $4\sqrt{\ln40/(2m)}\le0{,}05$ khi $m\ge16\ln40/(2\cdot0{,}05^2)\approx11\,804{,}4$. Nếu $\theta$ phụ thuộc các lượt, nó giống một giả thuyết chọn theo tập huấn luyện (Nhận xét 01.9), và Hệ quả 02.10 không còn áp dụng. Đánh giá một chính sách cố định là bài toán ước lượng trung bình như ở Bài 02. Nguồn: ghi chú Bài 10, §6, đoạn trước và Ví dụ 10.12.
- **Lý do / nối:** chỗ duy nhất của Phần A có bảo đảm với xác suất cao (trọng tâm trực quan 4) → bài tập.
- **Mục tiêu / nguồn:** 1, 5; Ví dụ 10.12.

#### `4-08` Bài tập: giá trị nền hợp lệ và giá trị nền gây chệch — bài tập (Bài tập 10.2(b), (c)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 10.2.** Ví dụ 10.2, $\theta=0$, ước lượng của Mệnh đề 10.7(b).
  - (b) Thay $R_{\ge0}$ bằng $R_{\ge0}-r_0$: tính kì vọng tọa độ $\theta_{s_0}$; so với $-0{,}025$.
  - (c) Thay $R_{\ge1}$ bằng $R_{\ge1}-r_0$: hợp lệ không? Kì vọng, phương sai tọa độ $\theta_{s_1}$; so với $\tfrac9{16}$.
  - [f] **Lời giải:** (b) $0{,}225$, ngược dấu với $-0{,}025$: $r_0$ không là hàm của $\mathcal F_0=(S_0)$.
  - [f] (c) Hợp lệ: $r_0$ là hàm của $\mathcal F_1=(S_0,A_0,S_1)$; kì vọng $0{,}25$, phương sai $0{,}4875<0{,}5625$.
- **Ghi chú diễn giả:** Câu chữ đầy đủ của đề: "(b) Trên MDP hai bước của Ví dụ 10.2 tại $\theta=0$, dùng ước lượng của Mệnh đề 10.7(b) và trừ phần thưởng của bước đầu $r_0$ khỏi số hạng $t=0$, tức thay $R_{\ge0}$ bằng $R_{\ge0}-r_0$. Tính kì vọng của tọa độ $\theta_{s_0}$ bằng (a), rồi kiểm lại trên bảng tám quỹ đạo. So với $\partial J/\partial\theta_{s_0}=-0{,}025$ (Ví dụ 10.5). (c) Cũng trên MDP đó, giữ nguyên số hạng $t=0$ và trừ $r_0$ khỏi số hạng $t=1$, tức thay $R_{\ge1}$ bằng $R_{\ge1}-r_0$. Giá trị nền này có hợp lệ theo Hệ quả 10.8 không? Tính kì vọng và phương sai của tọa độ $\theta_{s_1}$, rồi so với phương sai $\tfrac9{16}$ của ước lượng (ii) trong Ví dụ 10.10." Ở (b), số hạng trừ đi có kì vọng $\tfrac14\cdot(r(s_0,1)-r(s_0,0))=-\tfrac14$, nên kì vọng là $-0{,}025+0{,}25$; ước lượng chỉ thấy phần thưởng ở bước sau, nơi hành động $1$ có lợi. Ở (c), tọa độ $\theta_{s_1}$ nhận $1{,}5$; $-0{,}5$; $1$; $0$ trên bốn quỹ đạo qua $s_1$; mô-men bậc hai $0{,}55$. Cùng một đại lượng $r_0$ gây chệch ở (b) và hợp lệ ở (c): Hệ quả 10.8 so giá trị nền với lịch sử của bước mà nó được trừ. Nguồn: tệp bài tập, Bài tập 10.2(b), (c) và lời giải.
- **Lý do / nối:** bài tập của mạch 4 ghép Ví dụ 10.5, 10.10 và giả thiết của Hệ quả 10.8; khép Phần A → mạch 5.
- **Mục tiêu / nguồn:** 3; Bài tập 10.2(b), (c).

### Mạch 5. Giao thức học liên tục và ma trận đánh giá (5 trang, 12 phút)

#### `5-00` 5. Giao thức học liên tục và ma trận đánh giá — tiêu đề mạch, điểm vào mạch 5 · 0,5 phút
- **Mặt trang:**
  - "5."; h2 "Giao thức học liên tục và ma trận đánh giá"
  - `p.strand-lead`: Một bài toán học liên tục gồm dãy nhiệm vụ, giới hạn bộ nhớ và một ma trận đánh giá.
  - `p.strand-keys`: nhiệm vụ · ngân sách bộ nhớ · ma trận đánh giá · chuyển đổi ngược · độ quên
- **Ghi chú diễn giả:** Ở Phần A, chính sách sinh ra dữ liệu; ở Phần B, dữ liệu đến theo nhiệm vụ, mỗi nhiệm vụ có một phân bố riêng. Để so sánh các phương pháp, cần nói rõ thuật toán được phép giữ gì từ các nhiệm vụ trước, và kết quả được đo ở đâu, lúc nào. Hai giao thức chỉ khác ngân sách bộ nhớ hay định danh nhiệm vụ là hai bài toán khác nhau. Nguồn: ghi chú Bài 10, §7 đoạn mở và đoạn sau Định nghĩa 10.10.
- **Lý do / nối:** câu nối Phần A → Phần B: dòng dẫn và dòng đầu 5-01 → định nghĩa giao thức.
- **Mục tiêu / nguồn:** 4; §7.

#### `5-01` Giao thức học liên tục — định nghĩa (Định nghĩa 10.10) · 3 phút
- **Mặt trang:**
  - Môi trường A, B của ví dụ mở đầu là hai nhiệm vụ.
  - **Định nghĩa 10.10.** Nhiệm vụ $k$: phân bố $D_k$ trên $\mathcal Z$, chưa biết, $L_k=L_{D_k}$; (TK): $S^{(k)}\sim D_k^{m_k}$, độc lập.
  - Ngân sách bộ nhớ (memory budget) $M$: học nhiệm vụ $k$ chỉ thấy $S^{(k)}$, $w^{(k-1)}$, $\le M$ quan sát cũ.
  - Định danh nhiệm vụ (task identity): có hay không, chọn trước; tập kiểm tra riêng, độc lập.
- **Ghi chú diễn giả:** Giao thức cho tập quan sát $\mathcal Z$, tập tham số $W$, hàm lỗi $\ell$ thỏa (T2) và số nhiệm vụ $K\ge2$; $w^{(0)}$ là tham số khởi tạo và $w^{(k)}$ là tham số sau nhiệm vụ $k$. Định danh nhiệm vụ là thông tin về nhiệm vụ của quan sát khi dự đoán. Tập kiểm tra độc lập với mọi tập huấn luyện và với bộ nhớ. Các tập huấn luyện, bộ nhớ, nguồn ngẫu nhiên của thuật toán và các tập kiểm tra là ngẫu nhiên. Tình huống thứ hai của câu hỏi mở đầu là một giao thức với $K=2$, $M=0$. Huấn luyện một lần trên mọi dữ liệu có sẵn từ đầu, với các tập huấn luyện cùng cỡ, là tối thiểu hóa rủi ro thực nghiệm cho rủi ro trung bình $\frac1K\sum_kL_k$. Nguồn: ghi chú Bài 10, §7, Định nghĩa 10.10 và đoạn sau.
- **Lý do / nối:** câu nối từ ví dụ mở đầu (dòng 1) → định nghĩa → cách đo.
- **Mục tiêu / nguồn:** 4; Định nghĩa 10.10.

#### `5-02` Ma trận đánh giá và các độ đo — định nghĩa (Định nghĩa 10.11) · 3 phút
- **Mặt trang:**
  - **Định nghĩa 10.11.** Ma trận đánh giá (evaluation matrix) $\mathrm{acc}_{k,i}$: độ chính xác phân lớp (classification accuracy) của $w^{(k)}$ trên nhiệm vụ $i$.
  - Độ chính xác phân lớp trung bình cuối cùng (final average accuracy): $\frac1K\sum_{i=1}^K\mathrm{acc}_{K,i}$.
  - Chuyển đổi ngược (backward transfer): $\frac1{K-1}\sum_{i=1}^{K-1}(\mathrm{acc}_{K,i}-\mathrm{acc}_{i,i})$.
  - Chuyển đổi xuôi (forward transfer), $\mathrm{acc}^\circ_i$ của mô hình chỉ học nhiệm vụ $i$: $\frac1{K-1}\sum_{i=2}^{K}(\mathrm{acc}_{i,i}-\mathrm{acc}^\circ_i)$.
  - Độ quên (forgetting measure) của nhiệm vụ $i<K$: $\max_{i\le k\le K}\mathrm{acc}_{k,i}-\mathrm{acc}_{K,i}\ge0$.
- **Ghi chú diễn giả:** $\mathrm{acc}_{k,i}$ là $1$ trừ rủi ro thực nghiệm với hàm lỗi 0–1 trên tập kiểm tra của nhiệm vụ $i$; mô hình của $\mathrm{acc}^\circ_i$ được huấn luyện từ $w^{(0)}$ chỉ trên nhiệm vụ $i$. Chuyển đổi ngược âm khi các nhiệm vụ sau làm giảm độ chính xác phân lớp trên nhiệm vụ cũ; chuyển đổi xuôi dương khi các nhiệm vụ trước giúp học nhiệm vụ mới. Độ quên trung bình lấy trên $i=1,\ldots,K-1$. Mỗi ô là một ước lượng trên tập kiểm tra độc lập với $w^{(k)}$, nên Hệ quả 02.10 cho một khoảng tin cậy cho từng ô. Với hàm lỗi khác, thay $\mathrm{acc}$ bằng rủi ro kiểm tra và đổi chiều các so sánh. Ma trận và các độ đo là quy ước của học phần; không nguồn nào của học phần định nghĩa chúng. Nguồn: ghi chú Bài 10, §7, Định nghĩa 10.11 và đoạn sau; §13.
- **Lý do / nối:** bốn độ đo trước ví dụ dùng chúng → ví dụ ba nhiệm vụ.
- **Mục tiêu / nguồn:** 4; Định nghĩa 10.11.

#### `5-03` Ví dụ: ma trận đánh giá của ba nhiệm vụ — ví dụ (Ví dụ 10.13) · 3 phút
- **Mặt trang:**
  - **Ví dụ 10.13.** $K=3$; hàng là thời điểm $k$, cột là nhiệm vụ $i$; $\mathrm{acc}^\circ=(0{,}85;\,0{,}90;\,0{,}85)$.
  - Bảng: $k$ | $i=1$ | $i=2$ | $i=3$; $1$ | $0{,}85$ | $0{,}30$ | $0{,}40$; $2$ | $0{,}90$ | $0{,}92$ | $0{,}45$; $3$ | $0{,}80$ | $0{,}75$ | $0{,}88$
  - Trung bình cuối cùng $0{,}81$; chuyển đổi ngược $-0{,}11$; chuyển đổi xuôi $0{,}025$.
  - Độ quên $0{,}10$ và $0{,}17$, trung bình $0{,}135\ne0{,}11$: nhiệm vụ 1 đạt đỉnh ở hàng 2.
  - Hàng 3 thành $(0{,}83;\,0{,}95;\,0{,}88)$, cực đại chỉ tới hàng $K-1$: độ quên âm $-0{,}03$ ở nhiệm vụ 2.
- **Ghi chú diễn giả:** Trung bình cuối cùng là trung bình hàng $3$: $(0{,}80+0{,}75+0{,}88)/3$. Chuyển đổi ngược: $\tfrac12[(0{,}80-0{,}85)+(0{,}75-0{,}92)]$. Độ quên của nhiệm vụ 1 tính từ đỉnh $0{,}90$ ở hàng 2, không từ $0{,}85$ ở hàng 1, nên độ quên trung bình khác đối của chuyển đổi ngược. Chuyển đổi xuôi: $\tfrac12[(0{,}92-0{,}90)+(0{,}88-0{,}85)]$. Với ma trận thứ hai, chuyển đổi ngược thành $0{,}005$, và độ quên, lấy cực đại tới hàng $K$, là $0{,}07$ và $0$; độ quên ở nhiệm vụ 2 bằng $0$ hay $-0{,}03$ tùy hàng cuối của phép lấy cực đại. Ma trận chỉ ghi độ chính xác phân lớp của các tham số mà thuật toán đi qua. Nguồn: ghi chú Bài 10, §7, Ví dụ 10.13 và đoạn sau.
- **Lý do / nối:** giới hạn "phụ thuộc quy ước" của §10 → bài tập.
- **Mục tiêu / nguồn:** 4; Ví dụ 10.13.

#### `5-04` Bài tập: các độ đo từ một ma trận đánh giá — bài tập (Bài tập 10.4(a), (d)), lời giải trên mặt trang · 2,5 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 10.4.** $K=3$, $\mathrm{acc}^\circ=(0{,}85;\,0{,}86;\,0{,}90)$; ma trận đánh giá:
  - Bảng: $k$ | $i=1$ | $i=2$ | $i=3$; $1$ | $0{,}85$ | $0{,}20$ | $0{,}25$; $2$ | $0{,}90$ | $0{,}88$ | $0{,}30$; $3$ | $0{,}75$ | $0{,}60$ | $0{,}91$
  - (a) Tính bốn độ đo của Định nghĩa 10.11. (d) $w^{(3)}$ có phân lớp tốt trên mọi nhiệm vụ không? Vì sao trung bình cuối cùng không đủ?
  - [f] **Lời giải:** (a) $0{,}7533$; $-0{,}19$; độ quên $0{,}15$ và $0{,}28$, trung bình $0{,}215$; $0{,}015$.
  - [f] (d) Không: $\min_i\mathrm{acc}_{3,i}=0{,}60$ ở nhiệm vụ 2, dưới $\mathrm{acc}^\circ_2=0{,}86$; trung bình $0{,}7533$ gộp $0{,}91$ với $0{,}60$.
- **Ghi chú diễn giả:** Câu chữ đầy đủ của đề: "(a) Tính độ chính xác phân lớp trung bình cuối cùng, chuyển đổi ngược, độ quên của từng nhiệm vụ cũ cùng độ quên trung bình, và chuyển đổi xuôi. (d) Mô hình $w^{(3)}$ có phân lớp tốt trên mọi nhiệm vụ không? Con số nào trả lời câu hỏi này, và vì sao độ chính xác phân lớp trung bình cuối cùng không đủ?" Hàng là thời điểm $k$, cột là nhiệm vụ $i$. Ở (a), nhiệm vụ 1 đạt đỉnh $0{,}90$ ở hàng 2, nhiệm vụ 2 đạt đỉnh $0{,}88$ ở hàng 2. Ở (d), con số cần xem là ô nhỏ nhất của hàng cuối; mô hình cuối thấp hơn mô hình chỉ học nhiệm vụ 2 là $0{,}26$. Một ma trận có hàng cuối $(0{,}7533;\,0{,}7533;\,0{,}7533)$ cho cùng trung bình mà không nhiệm vụ nào dưới $0{,}75$. Phần (b) (độ quên trung bình không nhỏ hơn đối của chuyển đổi ngược) và (c) (khoảng tin cậy bằng cận hợp trên bảy ô) là bài về nhà. Nguồn: tệp bài tập, Bài tập 10.4(a), (d) và lời giải.
- **Lý do / nối:** bài tập của mạch 5; câu nối sang mạch 6: ma trận không chỉ ra tham số tốt cho mọi nhiệm vụ cùng lúc (dòng đầu 6-01).
- **Mục tiêu / nguồn:** 4; Bài tập 10.4(a), (d).

### Mạch 6. Hai nhiệm vụ xung đột và hối tiếc (9 trang, 20 phút)

#### `6-00` 6. Hai nhiệm vụ xung đột và hối tiếc — tiêu đề mạch, điểm vào mạch 6 · 0,5 phút
- **Mặt trang:**
  - "6."; h2 "Hai nhiệm vụ xung đột và hối tiếc"
  - `p.strand-lead`: Hai nhiệm vụ không có chung điểm cực tiểu buộc mọi phương pháp chọn một điểm thỏa hiệp.
  - `p.strand-keys`: xung đột · chính quy hóa tham số · phát lại · đánh đổi bền vững–mềm dẻo · hối tiếc tĩnh
- **Ghi chú diễn giả:** Ở câu hỏi mở đầu, huấn luyện tiếp chỉ trên môi trường B đưa rủi ro trên môi trường A từ $0$ lên $\tfrac12$. Hai cách giữ rủi ro trên nhiệm vụ cũ nhỏ là phạt độ lệch khỏi tham số cũ và trộn dữ liệu cũ vào lúc huấn luyện. Trên hai nhiệm vụ bậc hai, cả hai cách chỉ chọn một vị trí trên cùng một đánh đổi. Học trực tuyến đo một dãy quyết định bằng hối tiếc; hối tiếc nhỏ không kéo theo độ quên nhỏ. Nguồn: ghi chú Bài 10, §8 đoạn mở, §9.
- **Lý do / nối:** mạch 5 → định nghĩa phát lại và chính quy hóa.
- **Mục tiêu / nguồn:** 5; §8–§9.

#### `6-01` Phát lại và chính quy hóa tham số — định nghĩa (Định nghĩa 10.12) · 2,5 phút
- **Mặt trang:**
  - Ma trận đánh giá không chỉ ra tham số tốt cho mọi nhiệm vụ.
  - Hai nhiệm vụ $i$, $k$ xung đột khi $\arg\min_WL_i\cap\arg\min_WL_k=\varnothing$.
  - **Định nghĩa 10.12.** Phát lại (replay): bộ đệm phát lại (replay buffer) $\mathcal B$, $\le M$ quan sát cũ; $w^{(k)}$ cực tiểu $(1-\alpha)L_{S^{(k)}}+\alpha L_{\mathrm{buf}}$, $\alpha\in[0,1)$.
  - Chính quy hóa tham số (parameter regularization): $w^{(k)}$ cực tiểu $L_{S^{(k)}}(w)+\tfrac\lambda2(w-w^{(k-1)})^\top\Omega(w-w^{(k-1)})$, $\Omega$ đối xứng nửa xác định dương.
  - Tinh chỉnh (fine-tuning): $\alpha=0$ hoặc $\lambda=0$.
- **Ghi chú diễn giả:** $L_{S^{(k)}}$ là rủi ro thực nghiệm của nhiệm vụ $k$, $L_{\mathrm{buf}}$ là rủi ro thực nghiệm trên bộ đệm; $\alpha$ là tỉ lệ phát lại, chọn trước; điểm cực tiểu có thể đúng hay gần đúng. Với chính quy hóa tham số, $\lambda\ge0$; khi $\Omega$ là ma trận đường chéo, các phần tử đường chéo gọi là trọng số tầm quan trọng (importance weight); $\Omega=I$ cho phạt bình phương khoảng cách. Tinh chỉnh chỉ dùng dữ liệu mới, xuất phát từ $w^{(k-1)}$. Phát lại cần $M>0$; chính quy hóa tham số chỉ cần lưu $w^{(k-1)}$ và $\Omega$. Với $M$ hữu hạn, $L_{\mathrm{buf}}$ chỉ xấp xỉ rủi ro cũ. Nguồn: ghi chú Bài 10, §8, Định nghĩa 10.12 và đoạn sau.
- **Lý do / nối:** câu nối mạch 5 → 6 (dòng 1); hai phương pháp trước mệnh đề so sánh chúng.
- **Mục tiêu / nguồn:** 5; §8 đoạn mở, Định nghĩa 10.12.

#### `6-02` Hai nhiệm vụ xung đột buộc một đánh đổi — trực quan, kết quả (Mệnh đề 10.13) · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** $L_A$, $L_B$ có tâm $0$ và $1$; mỗi $w$ cách hai tâm tổng cộng ít nhất $1$.
  - **Mệnh đề 10.13.** **Giả thiết:** $W=\mathbb R$, $L_A(w)=w^2/2$, $L_B(w)=(w-1)^2/2$; $w^{(1)}=0$; $\lambda\ge0$, $\Omega=1$. **Bảo đảm:** tất định.
  - (a) Với mọi $w$: $\sqrt{2L_A(w)}+\sqrt{2L_B(w)}\ge1$ và $L_A(w)+L_B(w)\ge\tfrac14$, dấu bằng chỉ tại $w=\tfrac12$.
  - (b) Tinh chỉnh: $w=1$, $L_A(1)=\tfrac12$.
  - (c) $w_\lambda=\frac1{1+\lambda}$: $L_A(w_\lambda)=\frac1{2(1+\lambda)^2}$ giảm, $L_B(w_\lambda)=\frac{\lambda^2}{2(1+\lambda)^2}$ tăng theo $\lambda$.
  - (d) Phát lại với rủi ro cũ đầy đủ: cực tiểu $1-\alpha$, trùng $w_\lambda$ khi $\alpha=\frac\lambda{1+\lambda}$.
- **Ghi chú diễn giả:** Mệnh đề được chứng minh đầy đủ. Bảo đảm là tất định, với các rủi ro kì vọng cho trước, không có tập huấn luyện. Phần (a) nói không $w$ nào làm cả hai rủi ro bằng $0$; dấu bằng chỉ tại $w=\tfrac12$ là của bất đẳng thức thứ hai. Ở (c), $w_\lambda$ là điểm cực tiểu duy nhất của $L_B(w)+\frac\lambda2w^2$. Ở (d), "rủi ro cũ đầy đủ" nghĩa là bộ đệm được thay bằng chính $L_A$. Tăng $\lambda$ hay $\alpha$ chỉ dời điểm cực tiểu dọc đoạn $[0,1]$. Nguồn: ghi chú Bài 10, §8, Mệnh đề 10.13.
- **Lý do / nối:** trực quan và phát biểu chung trang; ví dụ dẫn nhập ở 1-06 ((b) là tinh chỉnh) → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 5; Mệnh đề 10.13.

#### `6-03` Ý tưởng chứng minh: hai nhiệm vụ xung đột — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  1. ((a)) $\sqrt{2L_A}=\lvert w\rvert$, $\sqrt{2L_B}=\lvert w-1\rvert$; bất đẳng thức tam giác: $\lvert w\rvert+\lvert1-w\rvert\ge1$.
  2. ((a)) Hoàn thành bình phương: $L_A(w)+L_B(w)=(w-\tfrac12)^2+\tfrac14$.
  3. ((b), (c)) Đạo hàm $(w-1)+\lambda w=0$ tại $w_\lambda$; đạo hàm bậc hai $1+\lambda>0$.
  4. ((d)) $(1-\alpha)(w-1)+\alpha w=0$ tại $w=1-\alpha$.
  - **Kỹ thuật.** Phạt $\tfrac\lambda2w^2=\lambda L_A(w)$, vì $L_A$ bậc hai có tâm $w^{(1)}$ và độ cong $1$: (c) và (d) cho cùng điểm cực tiểu.
- **Ghi chú diễn giả:** Lộ trình: bất đẳng thức tam giác cho phần đầu của (a); hoàn thành bình phương và đạo hàm của hàm bậc hai lồi nghiêm ngặt cho phần còn lại. Ở bước 3, thay $w_\lambda$ và $w_\lambda-1=-\frac\lambda{1+\lambda}$ vào $L_A$, $L_B$ được hai biểu thức của (c). Ở bước 4, $1-\alpha=\frac1{1+\lambda}$ khi $\alpha=\frac\lambda{1+\lambda}$. Với hai nhiệm vụ của mệnh đề, chính quy hóa tham số cho đúng kết quả của phát lại toàn bộ rủi ro cũ mà không cần lưu dữ liệu cũ. Khi rủi ro cũ có độ cong khác $1$, phạt với $\Omega=1$ không còn bằng $\lambda L_A$; Bài tập 10.5(c) tính trường hợp độ cong $4$. Với rủi ro không bậc hai, phạt bậc hai chỉ xấp xỉ rủi ro cũ quanh $w^{(1)}$. Nguồn: ghi chú Bài 10, §8, chứng minh Mệnh đề 10.13; đoạn cuối §8.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; giả thiết "độ cong $1$" vào ở dòng "Kỹ thuật." → ví dụ năm hệ số.
- **Mục tiêu / nguồn:** 5; chứng minh Mệnh đề 10.13.

#### `6-04` Ví dụ: năm hệ số chính quy hóa và đánh đổi bền vững–mềm dẻo — ví dụ (Ví dụ 10.14), hình F2 · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 10.14.** Mệnh đề 10.13(c) với $\lambda\in\{0,\tfrac13,1,3,9\}$.
  - {{`grid2`: bảng bên trái, hình F2 bên phải}} Bảng: $\lambda$ | $w_\lambda$ | $L_A$ | $L_B$ | $L_A+L_B$ | $\alpha$; $0$ | $1$ | $\tfrac12$ | $0$ | $\tfrac12$ | $0$; $\tfrac13$ | $\tfrac34$ | $\tfrac9{32}$ | $\tfrac1{32}$ | $\tfrac5{16}$ | $\tfrac14$; $1$ | $\tfrac12$ | $\tfrac18$ | $\tfrac18$ | $\tfrac14$ | $\tfrac12$; $3$ | $\tfrac14$ | $\tfrac1{32}$ | $\tfrac9{32}$ | $\tfrac5{16}$ | $\tfrac34$; $9$ | $\tfrac1{10}$ | $\tfrac1{200}$ | $\tfrac{81}{200}$ | $\tfrac{41}{100}$ | $\tfrac9{10}$
  - Hình F2, chú thích: Đường $(L_A(w),L_B(w))$ với $w\in[0,1]$, năm điểm của bảng và đường $L_A+L_B=\tfrac14$.
  - Tổng nhỏ nhất $\tfrac14$ tại $\lambda=1$, đúng cận dưới của Mệnh đề 10.13(a).
  - Đánh đổi bền vững–mềm dẻo (stability–plasticity trade-off): tính bền vững (stability) là $L_A$ nhỏ, tính mềm dẻo (plasticity) là $L_B$ nhỏ.
- **Ghi chú diễn giả:** Với $\lambda=\tfrac13$: $w_\lambda=\tfrac34$, $L_A=\tfrac12\cdot\tfrac9{16}=\tfrac9{32}$, $L_B=\tfrac12\cdot\tfrac1{16}=\tfrac1{32}$. Tăng $\lambda$ đổi rủi ro trên nhiệm vụ mới lấy rủi ro trên nhiệm vụ cũ; $\lambda$ hay $\alpha$ chỉ chọn một vị trí trên đánh đổi, và chọn $\lambda$ cần một tiêu chí nêu trước, như các độ đo của Định nghĩa 10.11. "Bền vững" ở đây khác tính ổn định của thuật toán ở Bài 06 và Bài 08. Phần đọc thêm (Nhận xét 10.14): phương pháp củng cố trọng số đàn hồi (elastic weight consolidation, EWC) của Kirkpatrick và cộng sự dùng $\Omega$ là đường chéo của ma trận thông tin Fisher. Ví dụ 10.15 cho thấy bỏ phần ngoài đường chéo có thể làm mất tính mềm dẻo: với $L_A=\tfrac12(w_1+w_2)^2$, $L_B=\tfrac12(w_1-w_2-2)^2$, phạt đầy đủ giữ được điểm $(1,-1)$ làm cả hai rủi ro bằng $0$, còn phạt đường chéo cho $L_B=\tfrac29$ khi $\lambda=1$ và $\tfrac89$ khi $\lambda=4$. Nguồn: ghi chú Bài 10, §8, Ví dụ 10.14, Nhận xét 10.14, Ví dụ 10.15.
- **Lý do / nối:** đánh đổi bằng số và hình (trọng tâm trực quan 5); Nhận xét 10.14 đọc thêm và Ví dụ 10.15 ở ghi chú diễn giả (mục 11, điểm 8) → bộ đệm hữu hạn.
- **Mục tiêu / nguồn:** 5; Ví dụ 10.14, đoạn sau Mệnh đề 10.13.

#### `6-05` Ví dụ: phát lại với bộ đệm hữu hạn — ví dụ (Ví dụ 10.16) · 2 phút
- **Mặt trang:**
  - **Ví dụ 10.16.** Nhiệm vụ A: $Z\sim N(0,1)$, $\ell(w,z)=\tfrac12(w-z)^2$, $L_A(w)=\tfrac12(w^2+1)$; nhiệm vụ B: $L_B(w)=\tfrac12(w-1)^2$; $\alpha=\tfrac12$.
  - Rủi ro cũ đầy đủ: cực tiểu $w=\tfrac12$, $L_A(\tfrac12)=\tfrac58$.
  - Bộ đệm $Z_1,\ldots,Z_M$, trung bình $\bar Z_M$: cực tiểu $w_M=\tfrac12+\tfrac12\bar Z_M$, và
  - $$\mathbb EL_A(w_M)-L_A(\tfrac12)=\tfrac12\operatorname{Var}(w_M)=\tfrac1{8M}$$
  - $M=1;10;100$: $0{,}125$; $0{,}0125$; $0{,}00125$. Rủi ro cũ giảm về $\tfrac58$ của điểm thỏa hiệp, không về $\min L_A=\tfrac12$.
  - Mô phỏng (Phụ lục C): rủi ro kiểm tra trên A $0{,}624$ khi tinh chỉnh; $0{,}331$; $0{,}256$; $0{,}252$ với $M=5;50;1000$.
- **Ghi chú diễn giả:** Với $L_{\mathrm{buf}}(w)=\frac1M\sum_i\tfrac12(w-Z_i)^2$, đạo hàm của $\tfrac12L_B+\tfrac12L_{\mathrm{buf}}$ là $\tfrac12(w-1)+\tfrac12(w-\bar Z_M)$. Vì $\mathbb Ew_M=\tfrac12$ và $\operatorname{Var}\bar Z_M=1/M$, độ lệch theo kì vọng bằng $\tfrac12\operatorname{Var}(w_M)$. Với tỉ lệ $\alpha$ bất kì, $w_M=(1-\alpha)+\alpha\bar Z_M$ và độ lệch là $\alpha^2/(2M)$. Mô hình của mô phỏng là hồi quy $y=wx$, khác mô hình của ví dụ: rủi ro tổng thể trên A là $\tfrac12(w^2+0{,}25)$; rủi ro kiểm tra tiến về giá trị $0{,}25$ của điểm thỏa hiệp $w=\tfrac12$, không về $\min=0{,}125$. Các số mô phỏng là kết quả thí nghiệm cho một thiết lập: $20$ hạt giống, một vòng SGD trên mỗi nhiệm vụ. Nguồn: ghi chú Bài 10, §8, Ví dụ 10.16; Phụ lục C.
- **Lý do / nối:** giới hạn "phát lại hữu hạn" của §10; phát lại không bỏ được đánh đổi → học trực tuyến.
- **Mục tiêu / nguồn:** 5; Ví dụ 10.16, Phụ lục C.

#### `6-06` Học trực tuyến và hối tiếc tĩnh — định nghĩa (Định nghĩa 10.15), nhận xét (Nhận xét 10.16) · 2,5 phút
- **Mặt trang:**
  - **Câu hỏi:** hối tiếc nhỏ có kéo theo độ quên nhỏ không?
  - **Định nghĩa 10.15.** Học trực tuyến (online learning): $z_1,\ldots,z_T$ tùy ý; ở vòng $t$, chọn $w_t\in W$ chỉ từ $z_1,\ldots,z_{t-1}$, rồi chịu $\ell(w_t,z_t)$.
  - Hối tiếc (regret) $\mathrm{Regret}_T(u)=\sum_t\ell(w_t,z_t)-\sum_t\ell(u,z_t)$; hối tiếc tĩnh (static regret): $\sup_{u\in W}\mathrm{Regret}_T(u)$.
  - **Nhận xét 10.16.** **Giả thiết:** (C) cho mọi $\ell(\cdot,z)$; $w_{t+1}=\operatorname{proj}_W(w_t-\eta v_t)$, $v_t\in\partial\ell(w_t,z_t)$, $\lVert v_t\rVert\le G$; $\lVert w_1-u\rVert\le R$.
  - **Bảo đảm:** tất định, với mọi dãy: $\mathrm{Regret}_T(u)\le\frac{R^2}{2\eta}+\frac{\eta G^2T}2$, bằng $RG\sqrt T$ khi $\eta=R/(G\sqrt T)$.
- **Ghi chú diễn giả:** Học trực tuyến (UML Chương 21) cũng xét dữ liệu đến theo thời gian, không có giả thiết thống kê; dãy có thể do một đối thủ (adversary) chọn. Khi hối tiếc tĩnh tăng chậm hơn $T$, hàm lỗi trung bình của thuật toán vượt của điểm so sánh tốt nhất không quá một lượng tiến về $0$. Hối tiếc tĩnh khác rủi ro vượt mức, một kì vọng theo một $D$, và khác độ quên, đo trên dữ liệu cũ sau khi học xong. Nhận xét 10.16 được phác thảo: $w_1\in W$ tất định, $W$ khác rỗng, đóng, lồi; chứng minh cộng bất đẳng thức một bước (Mệnh đề 05.13) theo $t$ như Định lý 05.14, dùng tổng triệt tiêu, nhưng không lấy kì vọng; $\eta=R/(G\sqrt T)$ như Hệ quả 05.15 (UML §21.3, với $w_1=0$). Nguồn: ghi chú Bài 10, §9, Định nghĩa 10.15 và đoạn sau, Nhận xét 10.16.
- **Lý do / nối:** câu hỏi của §9 (dòng 1) → định nghĩa → cận; trả lời ở 6-07.
- **Mục tiêu / nguồn:** 5; Định nghĩa 10.15, Nhận xét 10.16.

#### `6-07` Ví dụ: hối tiếc tĩnh nhỏ và độ quên lớn — ví dụ (Ví dụ 10.17) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 10.17.** $W=[0,1]$, $\ell(w,z)=\tfrac12(w-z)^2$, $T=1000$; $z_t=0$ khi $t\le500$ (nhiệm vụ A), $z_t=1$ khi $t>500$ (nhiệm vụ B); $L_A(w)=\tfrac12w^2$.
  - Điểm so sánh tốt nhất $u=\tfrac12$; Nhận xét 10.16 với $R=G=1$, $\eta=1/\sqrt{1000}$: hối tiếc $\le31{,}63$.
  - Bảng: Độ dài bước | Hối tiếc | $w_{T+1}$ | $L_A(w_{T+1})$; $1/\sqrt T$ | $-116{,}97$ | $\approx1$ | $\approx\tfrac12$; $1/t$ | $0{,}19$ | $\tfrac12$ | $\tfrac18$
  - **Kết luận:** hối tiếc cộng hàm lỗi tại thời điểm của từng vòng, nên cận hối tiếc tĩnh không chặn độ quên.
- **Ghi chú diễn giả:** $\sum_t\ell(u,z_t)=250u^2+250(1-u)^2$ nhỏ nhất tại $u=\tfrac12$, bằng $125$, nên hối tiếc tĩnh bằng hối tiếc so với $u=\tfrac12$. Với $w_1=0$, $\lVert w_1-u\rVert\le1$ và $\lvert w-z\rvert\le1$. Với $\eta=1/\sqrt T$, hối tiếc âm vì thuật toán theo kịp từng nửa dãy, và điểm cuối gần $1$. Với $\eta_t=1/t$, $w_{t+1}$ là trung bình của $z_1,\ldots,z_t$; cận của Nhận xét 10.16 không áp dụng vì độ dài bước thay đổi. Hai thuật toán có hối tiếc dưới $31{,}63$ nhưng rủi ro cuối trên nhiệm vụ A là $\tfrac12$ và $\tfrac18$. Học trực tuyến đo một dãy quyết định bằng hối tiếc so với một điểm cố định; học liên tục đo một dãy nhiệm vụ bằng ma trận đánh giá trên mọi nhiệm vụ đã gặp (Nhận xét 10.17). Nguồn: ghi chú Bài 10, §9, Ví dụ 10.17, Nhận xét 10.17.
- **Lý do / nối:** trả lời câu hỏi của 6-06; giới hạn "hối tiếc và độ quên" của §10 → bài tập.
- **Mục tiêu / nguồn:** 5; Ví dụ 10.17.

#### `6-08` Bài tập: rủi ro cũ có độ cong khác $1$ — bài tập (Bài tập 10.5(c)), lời giải trên mặt trang · 2,5 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 10.5.** Thiết lập của Mệnh đề 10.13, nhưng rủi ro cũ $L_A(w)=2w^2$, vẫn $w^{(1)}=0$.
  - (c) Điểm cực tiểu của: phát lại với rủi ro cũ đầy đủ, $\alpha=\tfrac12$; phạt với $\Omega=1$, $\lambda=1$; phạt với $\Omega=4$, $\lambda=1$. Với $\alpha\in[0,1)$, điều kiện trên $\lambda\Omega$ để hai cách cho cùng điểm cực tiểu?
  - [f] **Lời giải:** phát lại: $(1-\alpha)(w-1)+4\alpha w=0$, $w=\frac{1-\alpha}{1+3\alpha}=\tfrac15$.
  - [f] Phạt: $w=\frac1{1+\lambda\Omega}$, bằng $\tfrac12$ với $\Omega=1$ và $\tfrac15$ với $\Omega=4$; trùng phát lại khi $\lambda\Omega=\frac{4\alpha}{1-\alpha}$.
- **Ghi chú diễn giả:** Câu chữ đầy đủ của đề: "(c) Đổi rủi ro cũ thành $L_A(w)=2w^2$, vẫn với $w^{(1)}=0$. Tính điểm cực tiểu của phát lại với rủi ro cũ đầy đủ, $\alpha=\tfrac12$; của chính quy hóa tham số với $\Omega=1$, $\lambda=1$; và với $\Omega=4$, $\lambda=1$. Với $\alpha\in[0,1)$ tổng quát, tìm điều kiện trên $\lambda\Omega$ để chính quy hóa tham số cho cùng điểm cực tiểu với phát lại." Với $\Omega=4$, điều kiện thành $\lambda=\frac\alpha{1-\alpha}$, đúng quan hệ của Mệnh đề 10.13(d). Phạt $\frac{4\lambda}2w^2$ bằng $\lambda L_A(w)$, vì $\Omega=4$ là đạo hàm bậc hai của $L_A$; với $\Omega=1$, phép phạt chỉ bằng $\tfrac\lambda4L_A$ và đặt nhiệm vụ cũ nhẹ hơn bốn lần. Khi $\lambda\Omega$ bằng đạo hàm bậc hai của rủi ro cũ tại $w^{(1)}$, phạt bậc hai là phần bậc hai của khai triển Taylor quanh $w^{(1)}$ (Nhận xét 10.14(ii), đọc thêm). Các phần (a), (b), (d) là bài về nhà. Nguồn: tệp bài tập, Bài tập 10.5(c) và lời giải.
- **Lý do / nối:** bài tập của mạch 6 kiểm giả thiết "độ cong $1$" của dòng "Kỹ thuật." ở 6-03 → tổng kết.
- **Mục tiêu / nguồn:** 5; Bài tập 10.5(c).

### Mạch 7. Tổng kết (7 trang, 9 phút)

#### `7-00` 7. Tổng kết — tiêu đề mạch, điểm vào mạch 7 · 0,5 phút
- **Mặt trang:**
  - "7."; h2 "Tổng kết"
  - `p.strand-lead`: Dữ liệu do chính sách sinh ra vẫn cho gradient không chệch, còn nhiệm vụ thay đổi đòi một giao thức nêu trước.
- **Ghi chú diễn giả:** Các bảo đảm của bài thuộc ba loại: đồng nhất thức (đồng nhất thức gradient log, gradient theo quỹ đạo, tổng phần thưởng từ bước $t$, giá trị nền); tất định (hai nhiệm vụ xung đột, cận hối tiếc của hạ gradient trực tuyến); với xác suất cao (đánh giá một chính sách cố định trước khi chạy). Rủi ro kì vọng trở thành tổng phần thưởng kì vọng ở Phần A và một ma trận đánh giá ở Phần B; tập huấn luyện cố định trở thành các lượt sinh bởi chính sách hiện tại hay một dãy tập huấn luyện. Nguồn: ghi chú Bài 10, §10.
- **Lý do / nối:** mạch 6 → bảng tổng kết.
- **Mục tiêu / nguồn:** tất cả; §10–§13.

#### `7-01` Bảng tổng kết — tổng kết · 1,5 phút
- **Mặt trang (bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh`, trần 80, chữ trong ô có tính):**
  - Bảng: Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh; Bổ đề 10.3, đồng nhất thức: $\mathbb E\nabla\ln p_\theta=0$ | $\mathcal T$ hữu hạn, không phụ thuộc $\theta$ | đạo hàm $\sum_\tau p_\theta=1$; Định lý 10.4, đồng nhất thức: $\nabla J=\mathbb E\hat g$ | (MDP): $\mu_0$, $P$ không phụ thuộc $\theta$; (Π) | gradient log; bỏ $\ln\mu_0$, $\ln P$; Mệnh đề 10.7, Hệ quả 10.8, đồng nhất thức: $\nabla J=\mathbb E\sum_t(R_{\ge t}-b_t)\nabla\ln\pi_\theta$ | $b_t$ là hàm của $\mathcal F_t$ | tính chất tháp, $\sum_a\nabla\pi_\theta=0$; Mệnh đề 10.13, tất định: $L_A+L_B\ge\tfrac14$, $w_\lambda=\frac1{1+\lambda}$ | hai rủi ro bậc hai xung đột | tam giác; hoàn thành bình phương; Nhận xét 10.16, tất định: $\mathrm{Regret}_T(u)\le RG\sqrt T$ | (C); $\lVert v_t\rVert\le G$; $\eta=R/(G\sqrt T)$ | cộng bất đẳng thức một bước
- **Ghi chú diễn giả:** Bổ đề 10.3 và Định lý 10.4 cần tập quỹ đạo hữu hạn, không phụ thuộc tham số; với tập vô hạn cần thêm mật độ, khả vi liên tục và hàm trội (Nhận xét 10.5). Bỏ (MDP) làm ước lượng ngược dấu (Ví dụ 10.6). Hệ quả 10.8 cần giá trị nền là hàm của lịch sử trước hành động; giá trị nền phụ thuộc hành động gây chệch. Mệnh đề 10.13 là kết quả cho hai rủi ro bậc hai cụ thể; phạt bậc hai chỉ xấp xỉ rủi ro cũ khi rủi ro không bậc hai. Nhận xét 10.16 chặn hối tiếc tĩnh trên mọi dãy, không chặn độ quên. Không kết quả nào của Phần A giả sử mục tiêu lõm; bảo đảm với xác suất cao duy nhất là Ví dụ 10.12, cho chính sách cố định. Nguồn: ghi chú Bài 10, §10.
- **Lý do / nối:** một hàng cho mỗi kết quả chính (Mệnh đề 10.7 và Hệ quả 10.8 chung hàng, như chung trang ý tưởng chứng minh) → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §5–§9.

#### `7-02` Vấn đề trung tâm — tổng kết · 1,5 phút
- **Mặt trang:**
  - Dữ liệu phụ thuộc tham số: (T1) và (C) không còn đúng.
  - Gradient vẫn không chệch khi luật chuyển không phụ thuộc $\theta$; giá trị nền chỉ đổi phương sai.
  - Cận với xác suất ít nhất $1-\delta$: chỉ cho chính sách cố định.
  - Nhiệm vụ thay đổi: cần giao thức nêu trước; xung đột buộc $L_A+L_B\ge\tfrac14$; hối tiếc không chặn độ quên.
- **Ghi chú diễn giả:** Khi tác tử tương tác với môi trường, phân bố $p_\theta$ của dữ liệu phụ thuộc tham số đang học, nhưng gradient của mục tiêu vẫn ước lượng được không chệch từ một lượt nhờ gradient log của chính sách. Với chính sách cố định, $m=1000$ lượt cho bán kính $0{,}1718$ với xác suất ít nhất $0{,}95$. $-J$ không lồi, nên điểm dừng có thể là điểm cực tiểu. Khi nhiệm vụ thay đổi, bài toán chỉ xác định khi có giao thức và ma trận đánh giá, và hai nhiệm vụ xung đột buộc $L_A+L_B\ge\tfrac14$ trong ví dụ bậc hai. Theo Phụ lục D, tối ưu chính sách bỏ (T1), trừ khi đánh giá một chính sách cố định, và bỏ (C); học liên tục thay một $D$ bằng một dãy $D_1,\ldots,D_K$ có giới hạn truy cập. Nguồn: ghi chú Bài 10, §10; Phụ lục D.
- **Lý do / nối:** trả lời vấn đề trung tâm cho cả bài, giữ "với xác suất ít nhất $1-\delta$" và điều kiện luật chuyển (bài học deck 02) → bài tập tổng hợp.
- **Mục tiêu / nguồn:** tất cả; §10.

#### `7-03` Bài tập: năm câu hỏi tổng kết cho đánh giá một chính sách cố định — bài tập tổng hợp (Bài tập 10.7(i)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 10.7.** Dữ liệu, mục tiêu, đối tượng so sánh, đại lượng ngẫu nhiên, giả thiết cần đổi:
  - (i) Đánh giá $\pi_\theta$ bằng $m$ lượt, $\theta$ cố định trước khi chạy.
  - [f] **Lời giải:** $\tau_j$ độc lập cùng phân bố $p_\theta$; mục tiêu $J(\theta)$; so sánh: sai số của trung bình; ngẫu nhiên: các lượt.
  - [f] (T1) đúng cho các lượt; (T3): miền $[Hr_{\min},Hr_{\max}]$; không cần (C).
- **Ghi chú diễn giả:** Câu chữ đầy đủ của đề: "Năm câu hỏi của câu (f) ở §12 là: quá trình sinh dữ liệu; mục tiêu; đối tượng so sánh; các đại lượng ngẫu nhiên; các giả thiết của Bài 01–08 cần thay đổi. Trả lời năm câu hỏi cho hai thiết lập sau. (i) Đánh giá một chính sách $\pi_\theta$ của một MDP tầm nhìn hữu hạn bằng $m$ lượt, với $\theta$ cố định trước khi chạy (như Ví dụ 10.12)." Trong một lượt, các bước phụ thuộc nhau, nhưng quan sát là cả lượt. Mục tiêu là ước lượng $J(\theta)$ bằng $\frac1m\sum_jR(\tau_j)$; không có bước chọn mô hình, không có lớp giả thuyết hay điểm tốt nhất; đại lượng cần đo là sai số $\lvert\frac1m\sum_jR(\tau_j)-J(\theta)\rvert$. $\theta$, $\mu_0$, $P$, $r$ cố định. Với miền $[Hr_{\min},Hr_{\max}]$, bán kính của Hệ quả 02.10 nhân với $H(r_{\max}-r_{\min})$; với MDP của Ví dụ 10.2, miền này là $[0,6]$, chứa miền $[0,4]$ mà Ví dụ 10.12 dùng, và cho bán kính lớn hơn $1{,}5$ lần. Thiết lập (ii), chuỗi thời gian với cửa sổ chồng lấn, là bài về nhà. Nguồn: tệp bài tập, Bài tập 10.7(i) và lời giải.
- **Lý do / nối:** bài tập tổng hợp ghép Phần A (lượt, $p_\theta$), Ví dụ 10.12 và các giả thiết của Bài 01–05 (mục 11, điểm 9) → tự kiểm tra.
- **Mục tiêu / nguồn:** 1, 5; Bài tập 10.7(i).

#### `7-04` Câu hỏi tự kiểm tra — tổng kết · 1,5 phút
- **Mặt trang:**
  1. Bandit, $r(1)=2$, $r(0)=0$, $\theta=0$: tính $J'(0)$, hai giá trị của ước lượng gradient log và kì vọng của nó.
  2. Giá trị nền bằng chính $r(A)$: ước lượng còn không chệch không?
  3. Mệnh đề 10.13 với $\lambda=\tfrac14$: tính $w_\lambda$, $L_A(w_\lambda)$, $L_B(w_\lambda)$ và $\alpha$ cho cùng điểm cực tiểu.
  4. Hối tiếc tĩnh âm trên dãy của Ví dụ 10.17: rủi ro cuối trên A có nhỏ không?
- **Ghi chú diễn giả** (câu trả lời dự kiến, chỉ dùng ghi chú): (1) $\pi_0(1)=\tfrac12$, $J(\theta)=2\pi_\theta(1)$, $J'(0)=2\cdot\tfrac12\cdot\tfrac12=\tfrac12$; ước lượng $r(A)(A-\tfrac12)$ bằng $1$ khi $A=1$, $0$ khi $A=0$; kì vọng $\tfrac12$ (Định lý 10.4). (2) Không: ước lượng luôn bằng $0$, nên kì vọng $0\ne J'$; giá trị nền phụ thuộc hành động vi phạm giả thiết của Hệ quả 10.8 (Ví dụ 10.9). (3) $w_\lambda=\tfrac45$, $L_A=\tfrac8{25}$, $L_B=\tfrac1{50}$, $\alpha=\tfrac15$. (4) Không: thuật toán có hối tiếc $-116{,}97$ kết thúc ở $w\approx1$ với $L_A\approx\tfrac12$, gần giá trị lớn nhất của $L_A$ trên $W$. Câu (c) của ghi chú (luật chuyển phụ thuộc $\theta_{s_0}$) là Ví dụ 10.6. Nguồn: ghi chú Bài 10, §12 và lời giải.
- **Lý do / nối:** bốn câu ngắn trả lời được chỉ bằng ghi chú; là câu hỏi cuối buổi §12 (a), (b), (d), (e) → bài tập về nhà.
- **Mục tiêu / nguồn:** 2, 3, 5; §12.

#### `7-05` Bài tập về nhà — tổng kết · 0,5 phút
- **Mặt trang:**
  - Bảng: Mục | Bài tập; 3. Gradient chính sách và thuật toán REINFORCE | 10.3; 4. Giá trị nền và phương sai của ước lượng gradient | 10.1, 10.2; 5. Giao thức học liên tục và ma trận đánh giá | 10.4; 6. Hai nhiệm vụ xung đột và hối tiếc | 10.5, 10.6, 10.8, 10.9; 7. Tổng kết | 10.7
  - Liên kết "Ghi chú bài giảng · Bài tập" (viewer `&deck=`).
- **Ghi chú diễn giả:** Mỗi bài xếp vào mạch cung cấp kiến thức cuối cùng bài đó cần. Bài tập 10.3 cần Thuật toán 10.6, Định nghĩa 05.10 và Ví dụ 10.7. Bài tập 10.1 cần Định lý 10.4 cho (a), (b), Hệ quả 10.8 cho (c), (d), Nhận xét 10.5 cho (f); 10.2 cần Hệ quả 10.8 và Nhận xét 10.9. Bài tập 10.4 cần Định nghĩa 10.11 và cận hợp. Bài tập 10.5 cần Mệnh đề 10.13; 10.6 cần Định nghĩa 10.12 và thí nghiệm phát lại của Phụ lục C; 10.8 và 10.9 cần hối tiếc và Nhận xét 10.16. Bài tập 10.7 là bài tổng kết. Bảy bài đầu là bài gốc của học phần; 10.8, 10.9 chọn từ UML (Bài tập 21.5, 21.4), 10.9 tùy chọn. Nguồn: ghi chú Bài 10, §11; tệp bài tập.
- **Lý do / nối:** giao bài tập theo mạch (mạch 2 không có bài nào: mọi bài cần ít nhất Định lý 10.4) → tài liệu.
- **Mục tiêu / nguồn:** tất cả; §11.

#### `7-06` Tài liệu tham khảo — tổng kết · 0,5 phút
- **Mặt trang:**
  - Trước buổi học: Sutton, Barto (2018), *Reinforcement Learning: An Introduction*, §13.1–13.3.
  - Sau buổi học: Sutton, Barto, §13.4, §2.8; UML (Shalev-Shwartz, Ben-David, 2014), §21.1–21.3.
  - Mở rộng: Kirkpatrick và cộng sự (2017), *Overcoming catastrophic forgetting in neural networks*, PNAS; Sutton, Barto, §13.5, §13.7.
  - Bốn bài toán của học phần: phân lớp, ước lượng mật độ, tối ưu chính sách, học liên tục.
- **Ghi chú diễn giả:** Sutton và Barto §13.1–13.3: xấp xỉ chính sách, định lý gradient chính sách, REINFORCE; §13.4: REINFORCE có giá trị nền; §2.8: thuật toán gradient cho bài toán bandit; §13.5, §13.7: phương pháp tác nhân–phê bình, hành động liên tục. UML §21.1–21.3: học trực tuyến, hối tiếc, tối ưu lồi trực tuyến. Kirkpatrick và cộng sự: phần đặt vấn đề và phương pháp. Bốn bài toán khác nhau ở quá trình sinh dữ liệu, mục tiêu, đối tượng so sánh, đại lượng ngẫu nhiên và giả thiết cần đổi: phân lớp có giám sát dùng (T1) với một $D$ cố định; ước lượng mật độ bỏ (T3) vì hàm lỗi log không bị chặn; tối ưu chính sách bỏ (T1) và (C); học liên tục thay $D$ bằng một dãy $D_1,\ldots,D_K$. Nguồn: ghi chú Bài 10, §12 (f), §13 và quan hệ với nguồn; Phụ lục D.
- **Lý do / nối:** trang cuối của học phần; dòng khép học phần thay câu nối sang bài sau, lấy từ §12 (f) và Phụ lục D của ghi chú.
- **Mục tiêu / nguồn:** 5; §12 (f), §13.

## 7. Hành trình khái niệm

Thứ tự bước theo quy định: vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh (trang riêng) → kỹ thuật hoặc kiểm tra. Các bước có thể chung trang nhưng không đảo thứ tự trên mặt trang. Theo cổng duyệt Bài 04 (T5), ví dụ đặt trước phát biểu khi số liệu của nó không cần chính kết quả đó; ví dụ của ghi chú dùng kết quả để kiểm tra thì đứng sau, ở cột cuối.

| Kết quả hoặc khái niệm | Vấn đề | Trực quan | Ví dụ | Phát biểu | Ý tưởng chứng minh | Kỹ thuật / kiểm tra | Gộp, `không áp dụng`, lý do |
|---|---|---|---|---|---|---|---|
| Định nghĩa 10.1, 10.2 (MDP, $p_\theta$, $J$) | 1-06 (phân bố tới $s_1$ phụ thuộc $q$), 2-01 dòng 3 ((T1) không đúng) | 2-04 dòng "Lưu ý:" ($p_\theta$ phụ thuộc tham số, $R$ thì không) | 2-02 (Ví dụ 10.1), 2-05 (Ví dụ 10.2) | 2-03, 2-04 | `không áp dụng` (định nghĩa) | 2-05 dòng cuối ($0{,}2+0{,}6\,\pi_\theta(1\mid s_0)$) | Ví dụ 10.1 đứng trước Định nghĩa 10.1 như thứ tự §3 → §4 của ghi chú. |
| Bổ đề 10.3 | 1-06 ghi chú diễn giả, 3-00 (đạo hàm của trung bình đã thu bằng $0$) | ghi chú diễn giả 3-01 (tổng các thay đổi của xác suất bằng $0$) | 3-06 dòng 5 (kì vọng gradient log bằng $0$) | 3-01 | 3-01 dòng "Chứng minh." (mục 11, điểm 2) | 3-02 (Ví dụ 10.3: bỏ giả thiết tập giá trị); 3-05 (trang "Kỹ thuật.") | Bổ đề là công cụ, chứng minh hai dòng. Ví dụ số ở 3-06 đứng sau như ghi chú (Ví dụ 10.4 Bước 4). |
| Định lý 10.4 | 3-00 dòng dẫn và ghi chú diễn giả; 2-05 ghi chú diễn giả (tác tử không tính được $J$) | 3-03 ("Trực quan.": chỉ thừa số chính sách chứa $\theta$) | 2-02 ($J'(\ln3)=\tfrac38$ bằng đạo hàm trực tiếp), 2-05 ($J(0)=1{,}75$) | 3-03 | 3-04 | 3-05 (kỹ thuật, Nhận xét 10.5); 3-06 (Ví dụ 10.4: $\pm0{,}75$, $\tfrac38$); 3-07 (Ví dụ 10.5, sai phân hữu hạn); 3-08 (Ví dụ 10.6: bỏ (MDP)); 3-11 (Bài tập 10.1(a), (b)) | Trực quan và phát biểu chung trang. |
| Thuật toán 10.6 | 3-06 (một lượt cho ước lượng không chệch) | ghi chú diễn giả 3-09 (SGD đi lên với oracle) | 4-06 dòng cuối (mô phỏng $49/100$) | 3-09 | `không áp dụng` (thuật toán; điều kiện không chệch có điều kiện ở dòng 3 của 3-09) | 3-10 (Ví dụ 10.7: $-J$ không lồi, điểm dừng cực tiểu; Mệnh đề 08.12) | Ghi chú không nêu khẳng định hội tụ nào. |
| Mệnh đề 10.7 | 4-01 dòng 1 ($\pm0{,}75$ quanh $\tfrac38$) | 4-01 ("Trực quan.": hành động không ảnh hưởng phần thưởng trước nó) | 4-05 (Ví dụ 10.10, cột $\theta_{s_1}$: $\tfrac{11}{16}$ thành $\tfrac9{16}$) | 4-01 | 4-03 (chung với Hệ quả 10.8) | 4-03 (**Nhắc lại** kì vọng có điều kiện theo lịch sử); 4-05 (trường hợp phương sai tăng); 4-08 (Bài tập 10.2(c)) | Ví dụ 10.10 dùng cả Mệnh đề 10.7 và Hệ quả 10.8, nên đứng sau như ghi chú. |
| Hệ quả 10.8 | 4-02 dòng 1 (giá trị nền) | 4-02 dòng cuối (chọn $b_t$ để giảm phương sai) | 4-04 (Ví dụ 10.8: bốn giá trị nền, hình F1) | 4-02 | 4-03 bước 3 | 4-04 dòng cuối (Ví dụ 10.9: bỏ giả thiết); 4-06 (Ví dụ 10.11); 4-08 (Bài tập 10.2(b): $r_0$ gây chệch) | Ví dụ 10.8 dùng Hệ quả 10.8 cho kì vọng $\tfrac38$, nên đứng sau như ghi chú. |
| Ví dụ 10.12 (chính sách cố định) | 4-07 dòng 1 ($m$ lượt thỏa (T1)) | ghi chú diễn giả 4-07 (ước lượng trung bình như Bài 02) | 4-07 | `không áp dụng` (ví dụ dùng Hệ quả 02.10) | `không áp dụng` | 4-07 dòng "Nhắc lại:" (đảo cận đuôi thành cỡ mẫu, $11\,805$) và dòng cuối ($\theta$ chọn từ chính các lượt); 7-03 (Bài tập 10.7(i)) | Bảo đảm với xác suất cao duy nhất của Phần A. |
| Định nghĩa 10.10, 10.11 | 1-06 (học A rồi B), 5-01 dòng 1 | ghi chú diễn giả 5-00 (giữ gì, đo ở đâu, lúc nào) | 5-03 (Ví dụ 10.13) | 5-01, 5-02 | `không áp dụng` (định nghĩa) | 5-03 dòng cuối (độ quên âm khi đổi quy ước); 5-04 (Bài tập 10.4(a), (d)) | Ví dụ cần các độ đo, nên đứng sau định nghĩa. |
| Mệnh đề 10.13 | 1-06 ($L_A$ từ $0$ lên $\tfrac12$), 6-01 (xung đột) | 6-02 ("Trực quan.": hai tâm $0$, $1$) | 1-06 (tinh chỉnh, chính là (b)) | 6-02 | 6-03 | 6-03 ("Kỹ thuật.": phạt bằng $\lambda L_A$); 6-04 (Ví dụ 10.14, hình F2); 6-08 (Bài tập 10.5(c): độ cong $4$); 7-04 câu 3 | Trực quan và phát biểu chung trang. |
| Ví dụ 10.16 (bộ đệm hữu hạn) | 6-01 ghi chú diễn giả ($L_{\mathrm{buf}}$ chỉ xấp xỉ rủi ro cũ) | ghi chú diễn giả 6-05 (phương sai của $\bar Z_M$) | 6-05 | `không áp dụng` | `không áp dụng` | 6-05 dòng mô phỏng | — |
| Định nghĩa 10.15, Nhận xét 10.16 | 6-06 dòng "Câu hỏi:" | ghi chú diễn giả 6-06 (một điểm so sánh cho cả $T$ vòng) | 6-07 (Ví dụ 10.17) | 6-06 | `không áp dụng` (nhận xét *phác thảo*; chứng minh ở ghi chú diễn giả 6-06 với tên kỹ thuật "tổng triệt tiêu", mục 11, điểm 11) | 6-07 (cận $31{,}63$; hối tiếc $-116{,}97$ đi cùng $L_A\approx\tfrac12$); 7-04 câu 4 | Ví dụ dùng cận của nhận xét, nên đứng sau. |

Thời lượng theo mạch: 10 + 15 + 30 + 24 + 12 + 20 + 9 = 120 phút; 54 trang.

## 8. Hình vẽ

Mọi hình là SVG trong `2627-1/img/lec-10/`, `role="img"`, có `<title>` và alt cụ thể; màu không là tín hiệu duy nhất (kiểu nét, kiểu tô và hình dạng điểm khác nhau; nhãn trực tiếp); chữ trong hình chỉ là nhãn trục, nhãn điểm, số và nhãn ngắn (Unicode), không công thức; công thức và chú thích nằm ở `figcaption` (KaTeX). Chú thích nêu dữ liệu. Mọi số có nhãn trên hình cũng có trong bảng hoặc chữ trên cùng trang. Trục chứa hết dữ liệu.

| Mã | Tệp | Trang | Nội dung và dữ liệu | Alt dự kiến |
|---|---|---|---|---|
| F1 | `phuong-sai-gia-tri-nen.svg` | 4-04 | Trục ngang $b\in[-0{,}5;\,5{,}2]$ (vạch tại $0,1,\ldots,5$, nhãn "b"); trục dọc phương sai $\in[0;\,2{,}6]$ (vạch từng $0{,}5$, nhãn "Var"). Đường cong liền: phương sai của Ví dụ 10.8, Bước 1, $\operatorname{Var}(\hat g_b)=(12b^2-36b+27)/64$, lấy mẫu từng $0{,}05$. Bốn điểm của bảng, hình dạng khác nhau: $(0;\,\tfrac{27}{64}\approx0{,}4219)$ chấm tròn, nhãn "b = 0: 27/64"; $(1{,}5;\,0)$ ô vuông, nhãn "b* = 3/2: 0"; $(2{,}5;\,\tfrac3{16}=0{,}1875)$ tam giác, nhãn "b = J = 5/2: 3/16"; $(5;\,\tfrac{147}{64}\approx2{,}2969)$ hình thoi, nhãn "b = 5: 147/64". Không đường kẻ nào khác. Mọi số có nhãn đều có trong bảng của 4-04. | "Đồ thị phương sai của ước lượng gradient theo giá trị nền b trong bài toán bandit với xác suất 3/4: một parabol có giá trị nhỏ nhất 0 tại b = 3/2. Bốn điểm đánh dấu: b = 0 cho 27/64, b = 3/2 cho 0, b = 5/2 (giá trị của mục tiêu) cho 3/16, b = 5 cho 147/64." |
| F2 | `danh-doi-hai-nhiem-vu.svg` | 6-04 | Trục ngang $L_A\in[0;\,0{,}55]$ (vạch từng $0{,}1$, nhãn "L_A", rủi ro nhiệm vụ cũ); trục dọc $L_B\in[0;\,0{,}55]$ (vạch từng $0{,}1$, nhãn "L_B", rủi ro nhiệm vụ mới); hai trục cùng tỉ lệ. Đường cong liền: $(L_A(w),L_B(w))=(w^2/2,(w-1)^2/2)$ khi $w$ chạy từ $0$ đến $1$, từ $(0;\,0{,}5)$ tới $(0{,}5;\,0)$, lấy mẫu từng $0{,}01$. Đường thẳng nét đứt $L_A+L_B=\tfrac14$ từ $(0;\,0{,}25)$ tới $(0{,}25;\,0)$, chạm đường cong tại $(\tfrac18;\,\tfrac18)$. Năm chấm tròn đặc, nhãn bằng $\lambda$: "λ = 0" tại $(0{,}5;\,0)$; "λ = 1/3" tại $(0{,}28125;\,0{,}03125)$; "λ = 1" tại $(0{,}125;\,0{,}125)$; "λ = 3" tại $(0{,}03125;\,0{,}28125)$; "λ = 9" tại $(0{,}005;\,0{,}405)$. Nhãn đường nét đứt: "L_A + L_B = 1/4". Không ghi nhãn cho đầu mút $w=0$ (xem mục 11, điểm 10). Mọi số có nhãn đều có trong bảng của 6-04. | "Đường cong rủi ro nhiệm vụ mới theo rủi ro nhiệm vụ cũ khi tham số chạy từ 0 đến 1, đi từ điểm (0; 0,5) tới điểm (0,5; 0). Năm điểm ứng với hệ số chính quy hóa 0, 1/3, 1, 3, 9 nằm trên đường cong; tăng hệ số làm rủi ro nhiệm vụ cũ giảm và rủi ro nhiệm vụ mới tăng. Đường thẳng nét đứt có tổng hai rủi ro bằng 1/4 chạm đường cong tại điểm λ = 1, nơi hai rủi ro cùng bằng 1/8; mọi điểm khác của đường cong nằm phía trên đường thẳng này." |

Cách dựng dữ liệu hình (không có số mới trên nhãn): F1 vẽ công thức phương sai của Ví dụ 10.8, Bước 1, rút gọn thành $(12b^2-36b+27)/64$ (tính lại ở `num.py`, khớp bốn hàng của bảng ghi chú); không ghi công thức rút gọn trên hình hay mặt trang, vì dạng $\operatorname{Var}(\hat g_{b^*})+\pi(1-\pi)(b-b^*)^2$ là kết quả của Bài tập 10.1(c), bài về nhà. F2 vẽ hai công thức của Mệnh đề 10.13 theo tham số $w$; năm điểm trùng bảng của Ví dụ 10.14; đường $L_A+L_B=\tfrac14$ là cận dưới của Mệnh đề 10.13(a), chạm tại $w=\tfrac12$. Điều phối viên ghi cách dựng vào `review-log.md`.

## 9. Trang tổng kết

Bản cuối sau năm báo cáo duyệt (mục 17); mạch 7 có tám trang (7-00 đến 7-07). Tóm tắt:
- **Bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh` (7-01):** bốn hàng: Định lý 10.4 cùng Bổ đề 10.3 (đồng nhất thức; "$\mathcal T$ hữu hạn (hoặc Nhận xét 10.5); (MDP); (Π)"); Mệnh đề 10.7 cùng Hệ quả 10.8 (đồng nhất thức; $b_t$ là hàm của $\mathcal F_t$); Mệnh đề 10.13 (tất định); Nhận xét 10.16 (tất định; $\lVert w_1-u\rVert\le R$, $\eta=R/(G\sqrt T)$). Một trang. Phạm vi ở ghi chú diễn giả.
- **Vấn đề trung tâm (7-02):** năm dòng: (T1) sai vì $\theta_j$ phụ thuộc các lượt trước; (C) sai vì $-J$ không lồi (Ví dụ 10.7); dưới (MDP), (Π), ước lượng không chệch và giá trị nền theo lịch sử chỉ đổi phương sai; $\theta$ cố định thì (T1) đúng và với xác suất ít nhất $1-\delta$ sai số đánh giá bị chặn; nhiệm vụ đổi đòi giao thức, ma trận đánh giá, xung đột buộc đánh đổi, hối tiếc tĩnh không chặn độ quên. $L_A+L_B\ge\tfrac14$ trong ví dụ bậc hai và bán kính $0{,}1718$ (MDP của Ví dụ 10.2) ở ghi chú diễn giả.
- **Bài tập tổng hợp (7-03 đề, 7-04 lời giải):** Bài tập 10.7(i), đề theo câu chữ `exercises.md` (bỏ "của câu (f) ở §12", "hai thiết lập"), lời giải là danh sách năm mục theo đúng thứ tự năm câu hỏi.
- **Câu hỏi tự kiểm tra (7-05):** bốn câu §12 (a), (b), (d), (e); câu trả lời ở ghi chú diễn giả.
- **Bài tập về nhà (7-06):** bảng `Mục | Bài tập` như cũ; liên kết viewer.
- **Tài liệu tham khảo (7-07):** Sutton, Barto §13.1–13.3; §13.4, §2.8 và UML §21.1–21.3; Kirkpatrick và cộng sự (2017), Sutton, Barto §13.5, §13.7. Tên sách và tên bài báo ở ghi chú diễn giả.
- **Dòng khép học phần (7-07):** "Bốn bài toán của học phần: phân lớp có giám sát (Bài 01–08), ước lượng mật độ (Bài 09), tối ưu chính sách và học liên tục (Bài 10)." Ghi chú diễn giả nêu các giả thiết cần đổi theo §12 (f) và Phụ lục D, đủ hai vế "(T1) với chuỗi thời gian" và "có giới hạn truy cập".

## 10. Bảng thuật ngữ Việt–Anh của deck

Thuật ngữ xuất hiện trên mặt trang, theo ghi chú và `thuat-ngu.md`; tiếng Anh trong ngoặc ở lần dùng đầu trên một trang nội dung (cột "Trang").

| Tiếng Việt | Tiếng Anh | Trang |
|---|---|---|
| học tăng cường | reinforcement learning | 2-01 |
| tác tử | agent | 2-01 |
| lượt | episode | 2-01 |
| học liên tục | continual learning | 2-01 |
| nhiệm vụ | task | 2-01 |
| bài toán bandit | multi-armed bandit | 2-02 |
| quá trình quyết định Markov | Markov decision process, MDP | 2-03 |
| tầm nhìn hữu hạn | finite horizon | 2-03 |
| chính sách ngẫu nhiên | stochastic policy | 2-03 |
| chính sách bảng | tabular policy | 2-03 |
| quỹ đạo | trajectory | 2-04 |
| tổng phần thưởng | return | 2-04 |
| gradient log | score function | 3-01 |
| giá (của phân bố) | support | 3-01 |
| tổng phần thưởng từ bước $t$ | reward-to-go | 4-01 |
| lịch sử | history | 4-01 |
| giá trị nền | baseline | 4-02 |
| ngân sách bộ nhớ | memory budget | 5-01 |
| định danh nhiệm vụ | task identity | 5-01 |
| ma trận đánh giá | evaluation matrix | 5-02 |
| độ chính xác phân lớp | classification accuracy | 5-02 |
| độ chính xác phân lớp trung bình cuối cùng | final average accuracy | 5-02 |
| chuyển đổi ngược | backward transfer | 5-02 |
| chuyển đổi xuôi | forward transfer | 5-02 |
| độ quên | forgetting measure | 5-02 |
| phát lại | replay | 6-01 |
| bộ đệm phát lại | replay buffer | 6-01 |
| chính quy hóa tham số | parameter regularization | 6-01 |
| tinh chỉnh | fine-tuning | 6-01 |
| đánh đổi bền vững–mềm dẻo | stability–plasticity trade-off | 6-04 |
| tính bền vững | stability | 6-04 |
| tính mềm dẻo | plasticity | 6-04 |
| học trực tuyến | online learning | 6-06 |
| hối tiếc | regret | 6-06 |
| hối tiếc tĩnh | static regret | 6-06 |

Chỉ ở ghi chú diễn giả (tiếng Anh trong ngoặc ở đó): tối ưu chính sách (policy optimization), gradient chính sách (policy gradient), chính sách tất định (deterministic policy), phân bố trạng thái đầu (initial state distribution), luật chuyển trạng thái (transition law), chính sách Gauss (Gaussian policy), trọng số tầm quan trọng (importance weight), củng cố trọng số đàn hồi (elastic weight consolidation, EWC), ma trận thông tin Fisher (Fisher information matrix), đối thủ (adversary). "Chính sách tất định" lên mặt trang 2-03 bằng kí hiệu $\mathbb 1[\theta_s>0]$, không có tên; nếu người viết deck đưa tên lên mặt trang thì kèm "(deterministic policy)". Đã có ở Bài 01–09, không nhắc tiếng Anh: rủi ro kì vọng, rủi ro thực nghiệm, hàm lỗi, dưới vi phân, phép chiếu, hạ gradient ngẫu nhiên (SGD), ước lượng gradient log, đổi chỗ đạo hàm và kì vọng, hạt giống ngẫu nhiên. "REINFORCE" là tên thuật toán, giữ nguyên.

## 11. Rủi ro và điểm cần điều phối viên quyết định

1. **54 trang**, trên mục tiêu 45–52 và dưới trần 55 (lý do ở mục 3). Phương án về 52 trang: (a) bỏ trang 5-04 (Bài tập 10.4(a), (d)); mạch 5 khi đó không có trang bài tập, và ý "trung bình cuối cùng che một nhiệm vụ bị quên" chuyển vào ghi chú diễn giả 5-03; (b) gộp 3-02 (Ví dụ 10.3) vào 3-01 thành một dòng "Bỏ giả thiết tập giá trị: …" (trang gộp ước $62$ âm tiết, phải chuyển dòng định nghĩa gradient log và giá vào ghi chú diễn giả, trái quy tắc định nghĩa trước khi dùng). Khuyến nghị giữ 54: (a) bỏ bài tập duy nhất của cụm §7, (b) làm mất phản ví dụ bỏ giả thiết tập giá trị, chính chỗ 3-05 dẫn lại.
2. **Bổ đề 10.3 không có trang "Ý tưởng chứng minh" riêng.** Ghi chú gọi nó là bổ đề (công cụ chứng minh) và chứng minh gồm hai bước ngắn; mặt trang 3-01 có dòng "**Chứng minh.**" cho (b), ghi chú diễn giả nêu (a) và chỗ dùng $\Theta$ mở, $\mathcal T$ hữu hạn. Ý tưởng chứng minh của Định lý 10.4 (3-04, bước 2) và trang kỹ thuật 3-05 dùng lại đúng đồng nhất thức này. Nếu điều phối viên coi Bổ đề 10.3 là kết quả chính, thêm trang "Ý tưởng chứng minh: đồng nhất thức gradient log" sau 3-01 (hai bước, giả thiết trong ngoặc; bỏ giả thiết: Ví dụ 10.3): 55 trang, cắt bù 0,5 phút ở 3-07 và 3-10.
3. **Mạch 2 không có trang bài tập.** Mọi bài của `exercises.md` cần ít nhất Định lý 10.4 (bài duy nhất chỉ cần §1–§4 là Bài tập 10.1(a), nay ở trang bài tập của mạch 3 cùng (b)). Phương án: tách 3-11 thành 2-06 (Bài tập 10.1(a)) và 3-11 (Bài tập 10.1(b)): 55 trang.
4. **Một trang "Kỹ thuật." riêng (3-05 "Đạo hàm của kì vọng qua gradient log").** Bài 10 là bài cuối; kỹ thuật này đã dùng ở Bài 09 (ước lượng gradient log, Định nghĩa 09.14, Ví dụ 09.12 Bước 4) mà chưa có trang (storyboard Bài 09, mục 11, điểm 3 dành trang này cho deck Bài 10), và là nền của cả Phần A (Bổ đề 10.3, Định lý 10.4, Mệnh đề 10.7, Hệ quả 10.8, Nhận xét 10.14). Trang gộp Nhận xét 10.5 (điều kiện khi tập quỹ đạo vô hạn) và dòng "Nhắc lại:" kỹ thuật "Đổi chỗ đạo hàm và kì vọng" của Bài 09 (`L09-6-04`), đúng như bản giao việc: Bài 10 chỉ nhắc lại trang đó. Tiêu đề là tên kỹ thuật, viết bằng thuật ngữ của `thuat-ngu.md` ("gradient log"); tên "thủ thuật log-đạo hàm" không có trong ghi chú hay bảng thuật ngữ nên không dùng. Phương án tiêu đề khác: "Gradient log của một kì vọng".
5. **Hệ quả 10.8 dùng chung trang ý tưởng chứng minh với Mệnh đề 10.7 (4-03), và phát biểu của hệ quả (4-02) đứng trước trang đó**, trong khi ghi chú đặt chứng minh Mệnh đề 10.7 trước phát biểu Hệ quả 10.8. Lý do: hai chứng minh có chung bước then chốt ($\mathbb E[f(\mathcal F_t)\nabla\ln\pi_\theta(A_t\mid S_t)]=0$ cho mọi hàm $f$ của lịch sử, Phụ lục B Bước 4); một trang riêng cho Hệ quả 10.8 sẽ lặp bước 1–2 của 4-03. Mạch 4 vẫn theo đúng các khối của §6; hành trình khái niệm không đảo thứ tự trên từng kết quả. Phương án khác: trang riêng "Ý tưởng chứng minh: giá trị nền" sau 4-02 (55 trang).
6. **Ví dụ 10.10 chỉ trên một trang (4-05)**, gồm bảng phương sai và trường hợp tăng phương sai; Bước 1 (phép tính phương sai của tọa độ $\theta_{s_1}$) ở ghi chú diễn giả. Trang 54 âm tiết.
7. **Câu chữ bài tập rút gọn trên mặt trang** (giữ đủ dữ kiện, câu hỏi và kết quả; câu đầy đủ ở ghi chú diễn giả, theo tiền lệ Bài 08–09): 3-11 (10.1(a), (b) gộp "Liệt kê … cùng xác suất"); 4-08 (10.2(b) bỏ "bằng (a), rồi kiểm lại trên bảng tám quỹ đạo"; (c) "hợp lệ không?"); 5-04 (10.4(a) viết "bốn độ đo của Định nghĩa 10.11"; (d) bỏ "Con số nào trả lời câu hỏi này"); 6-08 (10.5(c) gộp ba phép tính); 7-03 (10.7: năm câu hỏi viết gọn, bỏ "(như Ví dụ 10.12)" trên mặt trang). Trang 5-04 **không** chép cụm "(giá trị giả định)" của `exercises.md` (cụm bị cấm trên mặt trang; mục 13).
8. **Nhận xét 10.14 (đọc thêm) và Ví dụ 10.15 chỉ ở ghi chú diễn giả 6-04.** Ví dụ 10.15 dẫn từ Nhận xét 10.14 (đọc thêm) và cần hai tham số; trang riêng làm deck 55 trang. Ghi chú diễn giả nêu cả hai giá trị $L_B=\tfrac29$, $\tfrac89$ và ý "bỏ phần ngoài đường chéo có thể làm mất tính mềm dẻo". Phương án: thay 6-05 (Ví dụ 10.16) bằng Ví dụ 10.15 nếu điều phối viên muốn nêu EWC trên mặt trang; khi đó giới hạn "phát lại hữu hạn" của §10 chỉ còn ở ghi chú diễn giả.
9. **Bài tập tổng hợp: Bài tập 10.7(i).** Phương án khác: Bài tập 10.3(d) (vì sao cách làm lồi của Bài 05 không cho bảo đảm cho Thuật toán 10.6; Ví dụ 10.7: (G1) không thỏa tại điểm dừng), gần trọng tâm "không chuyển kết quả lồi sang học tăng cường" hơn, nhưng lời giải cần (c)(i)–(iii) (mở rộng lồi, Hệ quả 05.15) và (G1), chưa có trên mặt trang; hoặc Bài tập 10.8(c) (chuyển từ học trực tuyến sang học theo lô khi phân bố đổi giữa dãy), ghép hối tiếc với độ quên nhưng cần cận số lỗi, khái niệm mới. Khuyến nghị 10.7(i).
10. **Hình F2 và Bài tập 10.5(b).** Bài tập 10.5(b) (về nhà) hỏi tập các điểm tối ưu Pareto ($[0,1]$) và ảnh $\{w_\lambda\}=(0,1]$. F2 vẽ đường cong cho $w\in[0,1]$, là đồ thị tham số của hai công thức trong Mệnh đề 10.13, không nêu "tối ưu Pareto" và không ghi nhãn đầu mút $w=0$ (điểm không ứng với $\lambda$ hữu hạn). Điều phối viên quyết định xem đây có là lộ lời giải không; phương án: chỉ vẽ năm điểm và đường $L_A+L_B=\tfrac14$, không vẽ đường cong.
11. **Nhận xét 10.16 không có dòng chứng minh trên mặt trang** (nhận xét *phác thảo*; trang 6-06 đã $54$ âm tiết). Kỹ thuật "Tổng triệt tiêu và trung bình các điểm lặp" (Bài 05, `L05-4-05`) chỉ được gọi tên ở ghi chú diễn giả 6-06. Nếu điều phối viên muốn "Nhắc lại:" trên mặt trang, thay dòng "Câu hỏi:" bằng câu hỏi ở dòng dẫn 6-00 (đã có ý "thỏa hiệp") và thêm "**Chứng minh.** Cộng bất đẳng thức một bước (Mệnh đề 05.13) theo $t$, không lấy kì vọng; **Nhắc lại:** tổng triệt tiêu (Bài 05)." ($+20$ âm tiết, trang thành $62$; cần cắt thêm).
12. **Kí hiệu $R$ hai nghĩa.** $R(\tau)$ (tổng phần thưởng, mạch 2–4) và $R$ (bán kính, Nhận xét 10.16, Ví dụ 10.17, mạch 6) theo đúng ghi chú. Trên 6-06, $R$ được đặt ở dòng giả thiết "$\lVert w_1-u\rVert\le R$"; 7-01 dùng $RG\sqrt T$ cạnh hàng có $R_{\ge t}$. Đề xuất cho tác giả ở mục 13; deck theo ghi chú.
13. **Các dòng "Nhắc lại:" kết quả của bài trước trên mặt trang:** 1-02 ((T1), (T3), Hệ quả 02.10, phép chiếu, dưới vi phân, (C), Định lý 05.14; Bài 09); 3-05 (đổi chỗ đạo hàm và kì vọng, Bài 09); 3-10 (Mệnh đề 08.12 với ba điều kiện); 4-03 (kì vọng có điều kiện theo lịch sử, Bài 05); 4-07 (đảo cận đuôi thành cỡ mẫu, Bài 02). Mệnh đề 09.3 (quy tắc nhân xác suất) cho $p_\theta(\tau)$ ở ghi chú diễn giả 2-04 (theo storyboard Bài 09, mục 11, điểm 3).
14. **Mật độ** (đếm bằng script, mục 15): không trang nội dung nào vượt $60$; 1-03 $80$/80; 7-01 $77$/80 kể cả chữ trong ô. Trung vị $50$ trên 42 trang nội dung (bỏ tổng quan, tiêu đề mạch, 1-03, 7-01, 7-05). Các trang $57$–$60$ (3-05, 4-07, 5-01, 7-02, 7-03, 7-06) là trang kỹ thuật gộp nhận xét, trang ví dụ có cận số, trang định nghĩa có bốn thành phần, trang tổng kết giữ loại bảo đảm và trang tài liệu; người sửa sau năm báo cáo duyệt còn biên $0$–$3$ âm tiết ở các trang này: mọi bổ sung phải đi kèm một cắt. Ghi chú diễn giả: không trang thường nào vượt $150$; trang ý tưởng chứng minh và trang bài tập $\le187$ (trần $250$).
15. **Công thức cần đo ở 390 px** (ngắt `aligned` chỉ khi tràn): 2-02 (hai đẳng thức trên một dòng), 2-04 ($p_\theta(\tau)$, gần như chắc chắn cần ngắt thành ba dòng như ghi chú), 3-03 ($\hat g$), 3-04 bước 3 (nội dòng dài, nên viết hiển thị nếu tràn), 4-01, 4-02 (tổng có giá trị nền), 4-07, 6-01 (phạt bậc hai, nội dòng dài), 6-05; bảng 2-05 (chín cột, chắc chắn cuộn ngang), 4-04, 4-05, 5-03, 5-04, 6-04 (sáu cột), 6-07, 7-01, 7-05 trong `.table-scroll`.
16. **Trang có hình:** 4-04 (bảng bốn cột cộng F1) và 6-04 (bảng sáu cột cộng F2): người viết deck kiểm 1600×900 với `footer_check.py`; nếu chạm chân trang, chuyển dòng "Ví dụ 10.9" của 4-04 thành trang con (không tăng số trang mạch) hoặc chuyển dòng tổng nhỏ nhất của 6-04 vào ghi chú diễn giả (F2 cho thấy điểm chạm).
17. **"Nhãn" (a), (b), (c), (i)–(iii)** của kết quả và bài tập viết thường, không in đậm; `deck_lint.py` chỉ bắt chuỗi in đậm kết thúc bằng dấu chấm hoặc hai chấm. "REINFORCE" và "MDP" là tên/viết tắt đã nêu đủ ở 2-03 và tiêu đề mạch 3; tiêu đề trang không trộn tiếng Anh ngoài tên thuật toán.
18. **Dòng khép học phần (7-06)** dựa trên §12 (f) và Phụ lục D của ghi chú; ghi chú không có câu "khép học phần" riêng ngoài câu hỏi (f), nên dòng mặt trang chỉ liệt kê bốn bài toán, và ghi chú diễn giả nêu điểm khác nhau theo Phụ lục D. Không có liên kết "bài sau".

## 12. Bảng đối chiếu trang → mục và khối của ghi chú

Cột "Đưa vào" ghi kí hiệu, thuật ngữ hoặc kết quả xuất hiện lần đầu trên mặt trang (định nghĩa hoặc "Nhắc lại:"/"Kí hiệu:"), để kiểm quy tắc định nghĩa trước khi dùng.

| Trang | Mục ghi chú | Khối (số của ghi chú) | Đưa vào |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §10 | — (bằng lời) | — |
| 1-02 | Kiến thức tiên quyết; Câu hỏi ôn nhanh | Hệ quả 02.10(b); Định lý 05.14; (C); Bài 09 | (T1), (T3), $L_D$, $L_S$, $\delta$, $h$ (nhắc lại); $\operatorname{proj}_W$, $\partial F$, (C), $W$, $F$; $s(\theta)$ |
| 1-03 | Mục tiêu học tập | — | — |
| 1-04 | các mục; §13 | — | — |
| 1-05 | đoạn mở đầu | — | — |
| 1-06 | Câu hỏi mở đầu | — | $s_0$, $s_1$, $s_2$, $a$, $q$; $w$, $L_A$, $L_B$; $S\sim D^m$ (nhắc lại) |
| 2-00 | §1–§4 | — | — |
| 2-01 | §1 | bảng nguồn ngẫu nhiên | học tăng cường, tác tử, lượt, học liên tục, nhiệm vụ; $j$; $K$, $D_1,\ldots,D_K$ |
| 2-02 | §3 | Ví dụ 10.1 | bandit, $A$, $r(\cdot)$, $\pi_\theta$, $\theta$, $J$ |
| 2-03 | §2; §4 | Định nghĩa 10.1; (MDP), (Π) | $\mathcal S$, $\mathcal A$, $\mu_0$ (phân bố trạng thái đầu), $P$ (luật chuyển trạng thái), $r$, $H$ (số bước mỗi lượt), $r_{\min}$, $r_{\max}$, $\Theta$, $\pi_\theta(a\mid s)$, $\theta_s$, chính sách bảng; chính sách tất định ở ghi chú diễn giả |
| 2-04 | §4 | Định nghĩa 10.2 | $\tau$, $\mathcal T$, $p_\theta$, $R(\tau)$, $r_t$, $S_t$, $A_t$, $J(\theta)$ (tổng quát), tối ưu chính sách |
| 2-05 | §4 | Ví dụ 10.2 | $p_0(\tau)$, $a_0$, $a_1$, $S_1$ |
| 3-00 | §5 | — | — |
| 3-01 | §5 | Bổ đề 10.3 | gradient log, giá |
| 3-02 | §5 | Ví dụ 10.3 | mật độ $p_\theta(a)$, $\mathbb 1[\cdot]$ (Bài 01) |
| 3-03 | §5 | Định lý 10.4 | $\hat g$, $m$ (số lượt) |
| 3-04 | §5 | chứng minh Định lý 10.4 | — |
| 3-05 | §5; Phụ lục A | Nhận xét 10.5 | $f$ (hàm bất kì); độ đo nền, hàm trội; "Đổi chỗ đạo hàm và kì vọng" (nhắc lại, Bài 09) |
| 3-06 | §5 | Ví dụ 10.4 | — |
| 3-07 | §5 | Ví dụ 10.5 | sai phân hữu hạn |
| 3-08 | §5 | Ví dụ 10.6 | $r_0$, $r_1$, $A_0$ |
| 3-09 | §5 | Thuật toán 10.6 và đoạn sau | $\eta_j$, $T$, $\theta_j$, $\tau_j$, $\hat g_j$; điều kiện không chệch của Bài 05 |
| 3-10 | §5 | Ví dụ 10.7 | $\beta$-trơn, Mệnh đề 08.12 (nhắc lại); $F=-J$ |
| 3-11 | `exercises.md` | Bài tập 10.1(a), (b) | $\operatorname{Var}$ |
| 4-00 | §6 | — | — |
| 4-01 | §6 | Mệnh đề 10.7 | $R_{\ge t}$, $t'$, $\mathcal F_t$, lịch sử |
| 4-02 | §6 | Hệ quả 10.8 | giá trị nền, $b_t(\mathcal F_t)$ |
| 4-03 | §6; Phụ lục B | chứng minh Mệnh đề 10.7, Hệ quả 10.8 | "Kì vọng có điều kiện theo lịch sử" (nhắc lại, Bài 05); $f$ (hàm của lịch sử) |
| 4-04 | §6 | Ví dụ 10.8, 10.9 | $b$, $\hat g_b$, $b^*$, $\kappa$ |
| 4-05 | §6 | Ví dụ 10.10 | vết |
| 4-06 | §2; §3; §6; Phụ lục C | (PT); khối ứng dụng; Ví dụ 10.11 | (PT), $c$, $X$ |
| 4-07 | §6 | Ví dụ 10.12 | "Đảo cận đuôi thành cỡ mẫu" (nhắc lại, Bài 02) |
| 4-08 | `exercises.md` | Bài tập 10.2(c) (phần (b) ở ghi chú diễn giả) | — |
| 5-00 | §7 | — | — |
| 5-01 | §1 (Phần B); §7 | Định nghĩa 10.10; (TK); bảng nguồn ngẫu nhiên | $\mathcal Z$, $L_k$, $S^{(k)}$, $m_k$, $M$, $w^{(k)}$, ngân sách bộ nhớ, định danh nhiệm vụ; cố định, ngẫu nhiên, đối tượng so sánh của Phần B ($w^{(0)}$ ở ghi chú diễn giả) |
| 5-02 | §7 | Định nghĩa 10.11 | $\mathrm{acc}_{k,i}$, $\mathrm{acc}^\circ_i$, bốn độ đo |
| 5-03 | §7 | Ví dụ 10.13 | — |
| 5-04 | `exercises.md` | Bài tập 10.4(a) ((d) ở ghi chú diễn giả) | — |
| 6-00 | §8–§9 | — | — |
| 6-01 | §8 | đoạn mở §8; Định nghĩa 10.12 | xung đột, $\arg\min$, $\mathcal B$, $L_{\mathrm{buf}}$, $\alpha$, $\lambda$, $\Omega$, $L_{S^{(k)}}$, tinh chỉnh |
| 6-02 | §8 | Mệnh đề 10.13 | $w_\lambda$, $w^{(1)}$ |
| 6-03 | §8 | chứng minh Mệnh đề 10.13 | — |
| 6-04 | §8 | Ví dụ 10.14; đoạn sau Mệnh đề 10.13 | tính bền vững, tính mềm dẻo, đánh đổi bền vững–mềm dẻo (mặt trang) |
| 6-05 | §8; Phụ lục C | Ví dụ 10.16 | $Z$, $Z_i$, $\bar Z_M$, $w_M$ |
| 6-06 | `exercises.md` | Bài tập 10.5(c) (chuyển lên sau 6-05, thuộc §8) | — |
| 6-07 | §9 | Định nghĩa 10.15; Nhận xét 10.16 | $z_t$, $w_t$, $u$, $\mathrm{Regret}_T$, $v_t$, $G$, $R$ (bán kính), $\eta$ |
| 6-08 | §9 | Ví dụ 10.17; Nhận xét 10.17 | — |
| 7-00 | §10–§13 | — | — |
| 7-01 | §10 | mọi kết quả | — |
| 7-02 | §10; Phụ lục D | — | — |
| 7-03 | `exercises.md` | Bài tập 10.7(i), đề | — |
| 7-04 | `exercises.md` | Bài tập 10.7(i), lời giải | — |
| 7-05 | §12 | câu hỏi cuối buổi (a), (b), (d), (e) | — |
| 7-06 | §11 | `exercises.md` | — |
| 7-07 | §12 (f), §13; Phụ lục D | — | — |

Kiểm định nghĩa trước khi dùng: (T3) có nghĩa trên mặt trang 1-02 ("$\ell\in[0,1]$") trước 7-03; (C) ở 1-02 trước 3-09, 6-07, 7-01, 7-02, 7-03; $\operatorname{proj}_W$, $\partial F$ ở 1-02 trước 6-06; (MDP), (Π) ở 2-03 trước 3-03; $\mathcal F_t$ ở 4-01 trước 4-02, 4-03, 4-08 và 7-01; $r_0$ ở 3-08 trước 4-08; "Bước 3 của chứng minh" ở 3-08 dẫn trang trước (3-04). Mặt trang 4-07 không dẫn số Nhận xét 01.9 (chỉ "$\theta$ không cố định"; Hệ quả 02.10 ở 1-02 ghi "$h$ cố định"); ghi chú diễn giả dẫn số.

## 13. Đề xuất sửa ghi chú và tệp bài tập (không sửa; chờ điều phối viên và tác giả)

Không thấy lỗi toán học trong các khối deck dùng; mọi con số của ví dụ và sáu bài tập trên mặt trang đã tính lại (mục 5) và khớp ghi chú, tệp bài tập.

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất |
|---|---|---|---|---|
| nhẹ | `exercises.md`, Bài tập 10.4, câu dẫn | "(giá trị giả định)" là cụm rào đón về nguồn gốc số liệu, trái quy tắc văn phong của tác giả ("Disclaimers and hedges", `../CLAUDE.md`) và bị `deck_lint.py` cấm trên mặt trang | `exercises.md` dòng 468: "cho ma trận đánh giá dưới đây (giá trị giả định)" | Bỏ cụm; nguồn gốc số ghi ở `review-log.md`. Deck (5-04) không chép cụm này |
| nhẹ | `exercises.md`, đoạn đầu | "Logarit là logarit tự nhiên" khác chính tả "lôgarit" của ghi chú (§2) và `thuat-ngu.md` | `exercises.md` dòng 8; ghi chú dòng 100 | Viết "Lôgarit là lôgarit tự nhiên" |
| nhẹ | ghi chú §9, Nhận xét 10.16, Ví dụ 10.17 | $R$ vừa là tổng phần thưởng $R(\tau)$ (Phần A) vừa là bán kính $\lVert w_1-u\rVert\le R$ (Phần B); bảng kí hiệu §2 không ghi nghĩa thứ hai | ghi chú dòng 94 (bảng), 821, 837 | Thêm dòng "$R$ (Phần B): bán kính, như Bài 05" vào bảng §2, hoặc đổi tên cục bộ; deck theo ghi chú (mục 11, điểm 12) |
| nhẹ | ghi chú §5, Thuật toán 10.6, Đầu vào | "Chính sách. Họ $\pi_\theta$ của Định nghĩa 10.1, với $\Theta$ là cả không gian tham số (như chính sách bảng)": không nói vì sao cần $\Theta$ là cả không gian (bước $\theta_j+\eta_j\hat g_j$ phải nằm trong $\Theta$); điều kiện này chỉ ngầm hiểu | ghi chú dòng 405 | Không bắt buộc; nếu tác giả muốn, thêm "để bước cập nhật luôn nằm trong $\Theta$". Deck (3-09) chép đúng điều kiện |

## 14. Danh sách kỹ thuật đã giới thiệu đến hết Bài 10

Danh sách của storyboard Bài 09 (mục 14), cột cuối thay bằng cách deck Bài 10 dùng; dòng cuối là kỹ thuật có trang riêng của Bài 10. Bài 10 là bài cuối của học phần, nên danh sách này là danh sách đầy đủ của học phần.

| Kỹ thuật | Bài, trang (lần đầu) | Dạng | Trong deck Bài 10 |
|---|---|---|---|
| Tính tuyến tính của kì vọng | Bài 01, `L01-3-03` | một dòng | dùng không nhắc tên (4-01: tách $R(\tau)=\sum_{t'<t}r_{t'}+R_{\ge t}$) |
| Bất đẳng thức hợp | Bài 01, `L01-4-04` | trang riêng | chỉ ở Bài tập 10.4(c) (bài về nhà; ghi chú diễn giả 5-04) |
| Chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ | Bài 01, `L01-6-07` | trang riêng | không dùng |
| Tối thiểu hóa từng điểm rồi lấy kì vọng | Bài 01, `L01-5-09` | một dòng | không dùng |
| Phương pháp Chernoff | Bài 02, `L02-3-01` | trang riêng | không dùng |
| Dây cung của hàm lồi và Taylor bậc hai tại $0$ | Bài 02, `L02-3-03` | một dòng | không dùng |
| Đảo cận đuôi thành bán kính và cỡ mẫu | Bài 02, `L02-4-04` | trang riêng | **nhắc lại** một dòng ở 4-07 (cỡ mẫu $11\,805$ lượt) |
| Chia xác suất thất bại cho từng giả thuyết | Bài 02, `L02-5-05` | trang riêng | không dùng |
| Bước tất định trên biến cố đại diện | Bài 02, `L02-5-11` | trang riêng | không dùng |
| Cận dưới và cận trên cho chiều VC | Bài 03, `L03-2-04` | trang riêng | không dùng |
| Đối xứng hóa và tập mẫu ảo | Bài 03, `L03-5-06` | trang riêng | không dùng |
| Hàm tăng trưởng thay cho số giả thuyết | Bài 03, `L03-5-07` | trang riêng | không dùng |
| Thêm bớt kì vọng rồi bình phương | Bài 04, `L04-3-03` | một dòng | không dùng |
| Chia xác suất thất bại theo trọng số | Bài 04, `L04-4-04` | trang riêng | không dùng |
| Lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện | Bài 04, `L04-6-02` | một dòng | không dùng trên mặt trang (Bài tập 10.4(c), về nhà) |
| Kì vọng có điều kiện theo lịch sử | Bài 05, `L05-3-07` | trang riêng | **nhắc lại** một dòng ở 4-03 (chứng minh Mệnh đề 10.7, Hệ quả 10.8; ghi chú: "như Bổ đề 05.12"); điều kiện không chệch có điều kiện ở 3-09 |
| Tổng triệt tiêu và trung bình các điểm lặp | Bài 05, `L05-4-05` | trang riêng | gọi tên ở ghi chú diễn giả 6-06 (chứng minh Nhận xét 10.16, phác thảo); mặt trang không có dòng chứng minh (mục 11, điểm 11) |
| Cân hai số hạng, $a/\eta+b\eta\ge2\sqrt{ab}$ | Bài 05, `L05-4-08` | một dòng | dùng ở 6-06 không nhắc tên ($\eta=R/(G\sqrt T)$ cho $RG\sqrt T$) |
| Số hạng chéo bằng $0$ cho véc-tơ không tương quan | Bài 05 | một dòng | không dùng |
| Lập luận đổi vai (thay một điểm) | Bài 06, `L06-4-05` | trang riêng | không dùng |
| Cộng hai bất đẳng thức tăng trưởng bậc hai đối xứng | Bài 06, `L06-5-02` | một dòng | không dùng |
| Điểm trên đoạn thẳng rồi cho dần về đầu mút | Bài 06, ghi chú diễn giả `L06-3-03` | một dòng | không dùng |
| Đưa hàm nhiều biến về một biến bằng các hàng trùng nhau của $\Theta_1$ | Bài 07, 2-05 | một dòng | không dùng |
| Đổi biến giữa dấu và nhãn ngẫu nhiên | Bài 07, 3-04 | một dòng | không dùng |
| Sai phân của một cận trên đúng không quá sai phân lớn nhất | Bài 07, ghi chú diễn giả 4-03 | một dòng | không dùng |
| Thay hàm lỗi 0–1 bằng hàm lỗi bị chặn, Lipschitz rồi dùng bổ đề co | Bài 07, 5-06 | một dòng | không dùng |
| Ghép cặp hai lần chạy rồi Jensen | Bài 08, 2-05 | một dòng | không dùng |
| Hàm phụ $q_u=f-\langle\nabla f(u),\cdot\rangle$ cực tiểu tại $u$ | Bài 08, 2-09 | một dòng "Kỹ thuật." | không dùng |
| Bất đẳng thức trên từng quỹ đạo, rồi kì vọng chỉ qua xác suất biên | Bài 08, 3-02 bước 3–4 | một bước của ý tưởng chứng minh | không dùng |
| Đổi thứ tự lấy tổng | Bài 08, ghi chú diễn giả 4-05 | một câu | không dùng |
| Lấy tổng theo kí tự cuối | Bài 09, 3-02 | một dòng "Kỹ thuật." | dùng không nhắc tên ở ghi chú diễn giả 2-04 ($p_\theta$ là hàm xác suất) và 4-03 (tổng theo phần sau của quỹ đạo bằng $1$) |
| $\ln t\le t-1$, dấu bằng chỉ khi $t=1$ | Bài 09, 4-03 | một dòng "Kỹ thuật." | không dùng |
| Thêm bớt $\ln q(v)$ rồi lấy kì vọng theo $q$ | Bài 09, 5-03 | một dòng "Kỹ thuật." | không dùng |
| Đổi chỗ đạo hàm và kì vọng | Bài 09, 6-04 | trang riêng | **nhắc lại** một dòng ở 3-05 (Nhận xét 10.5, Phụ lục A) |
| **$\sum_a\nabla\pi_\theta(a\mid s)=\nabla1=0$** (gradient của một phân bố trên tập hữu hạn có tổng bằng $0$) | **Bài 10, 4-03 bước 1** | một bước của ý tưởng chứng minh | dùng ở Mệnh đề 10.7, Hệ quả 10.8; là Bổ đề 10.3(b) cho từng trạng thái |
| **Hoàn thành bình phương; phạt bậc hai bằng $\lambda$ lần rủi ro cũ khi rủi ro cũ bậc hai** | **Bài 10, 6-03** | một dòng "Kỹ thuật." | Bài tập 10.5(c) (6-08) |
| **Đạo hàm của kì vọng qua gradient log**, $\nabla\mathbb E_{p_\theta}f=\mathbb E_{p_\theta}[f\nabla\ln p_\theta]$ | **Bài 10, 3-05** | **trang riêng** | Bổ đề 10.3, Định lý 10.4, Mệnh đề 10.7, Hệ quả 10.8, Nhận xét 10.14; Bài 09 đã dùng dưới tên ước lượng gradient log |

Bài 10 có một trang "Kỹ thuật." riêng (3-05): kỹ thuật đã dùng ở Bài 09 mà chưa có trang, và là nền của cả Phần A (mục 11, điểm 4). Các kỹ thuật khác của bài là một dòng hoặc một bước, vì không bài nào sau dùng lại.

## 15. Mật độ mặt trang đo bằng script

Đếm bằng `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-10/storyboard/count.py` trên văn bản dự kiến của mục 6, theo cách của `deck_lint.py`: token cách nhau bởi khoảng trắng, có chữ cái hoặc chữ số; bỏ tiêu đề, công thức `$…$`, chỉ dẫn `{{…}}`, đoạn trong dấu `` ` ``, dấu fragment; số viết trong câu có tính; trong dòng `Bảng:` chỉ token có chữ cái được tính (chữ trong ô có tính, số trong bảng không tính); chữ của chú thích hình (dòng "Hình F…, chú thích:") có tính. Mỗi gạch đầu dòng hoặc mục đánh số là một dòng; mỗi công thức hiển thị là một dòng (số 0 trong cột theo dòng); một bảng là một dòng. Cột cuối là số âm tiết của ghi chú diễn giả theo cùng cách đếm (kể cả dòng nguồn, bỏ chữ "Nguồn:"). Trang tiêu đề mạch: số âm tiết của `strand-lead` ở cột cuối sau dấu "·". Trung vị $50$ trên 42 trang nội dung (bỏ tổng quan, tiêu đề mạch, 1-03, 7-01, 7-05); không trang nội dung nào vượt $60$.

| Trang | Âm tiết mặt trang (kể cả chữ trong bảng) | Dòng | Theo dòng | Ghi chú diễn giả |
|---|---:|---:|---|---:|
| 1-01 | (tổng quan hoặc tiêu đề mạch; 70) | — | — | 126 |
| 1-02 | 52 | 6 | 8; 12; 0; 19; 13; 0 | 95 |
| 1-03 | 80 | 5 | 15; 16; 16; 15; 18 | 122 |
| 1-04 | (tổng quan hoặc tiêu đề mạch; 64) | — | — | 71 |
| 1-05 | (tổng quan hoặc tiêu đề mạch; 24) | — | — | 110 |
| 1-06 | 49 | 5 | 7; 10; 9; 11; 12 | 140 |
| 2-00 | (tổng quan hoặc tiêu đề mạch; 0) | — | — | 87 · lead 20 |
| 2-01 | 56 | 4 | 17; 12; 13; 14 | 146 |
| 2-02 | 38 | 6 | 17; 2; 0; 1; 9; 9 | 70 |
| 2-03 | 47 | 5 | 21; 6; 11; 1; 8 | 149 |
| 2-04 | 35 | 4 | 6; 0; 10; 19 | 87 |
| 2-05 | 44 | 5 | 18; 0; 0; 12; 14 | 89 |
| 3-00 | (tổng quan hoặc tiêu đề mạch; 0) | — | — | 87 · lead 19 |
| 3-01 | 46 | 5 | 9; 20; 11; 1; 5 | 105 |
| 3-02 | 54 | 6 | 12; 8; 3; 10; 3; 18 | 82 |
| 3-03 | 50 | 6 | 13; 12; 0; 9; 12; 4 | 60 |
| 3-04 | 47 | 5 | 10; 8; 8; 7; 14 | 115 |
| 3-05 | 60 | 5 | 6; 14; 20; 11; 9 | 140 |
| 3-06 | 45 | 6 | 13; 4; 6; 0; 7; 15 | 59 |
| 3-07 | 50 | 6 | 17; 11; 0; 0; 8; 14 | 89 |
| 3-08 | 55 | 4 | 18; 9; 13; 15 | 92 |
| 3-09 | 48 | 4 | 16; 7; 6; 19 | 107 |
| 3-10 | 49 | 5 | 10; 4; 6; 7; 22 | 128 |
| 3-11 | 48 | 5 | 9; 8; 23; 3; 5 | 114 |
| 4-00 | (tổng quan hoặc tiêu đề mạch; 0) | — | — | 88 · lead 19 |
| 4-01 | 50 | 5 | 8; 9; 15; 18; 0 | 91 |
| 4-02 | 53 | 5 | 13; 21; 6; 0; 13 | 113 |
| 4-03 | 45 | 5 | 12; 9; 7; 9; 8 | 159 |
| 4-04 | 53 | 5 | 15; 0; 12; 12; 14 | 125 |
| 4-05 | 54 | 5 | 18; 5; 4; 13; 14 | 133 |
| 4-06 | 48 | 5 | 12; 12; 8; 4; 12 | 130 |
| 4-07 | 57 | 5 | 14; 13; 0; 14; 16 | 100 |
| 4-08 | 56 | 5 | 12; 10; 14; 10; 10 | 187 |
| 5-00 | (tổng quan hoặc tiêu đề mạch; 0) | — | — | 88 · lead 20 |
| 5-01 | 57 | 4 | 13; 13; 14; 17 | 137 |
| 5-02 | 56 | 5 | 20; 12; 5; 12; 7 | 142 |
| 5-03 | 49 | 5 | 11; 0; 10; 13; 15 | 106 |
| 5-04 | 53 | 5 | 7; 0; 27; 8; 11 | 177 |
| 6-00 | (tổng quan hoặc tiêu đề mạch; 0) | — | — | 96 · lead 18 |
| 6-01 | 56 | 5 | 14; 6; 17; 15; 4 | 106 |
| 6-02 | 50 | 6 | 13; 9; 8; 3; 4; 13 | 88 |
| 6-03 | 41 | 5 | 6; 5; 9; 2; 19 | 127 |
| 6-04 | 49 | 5 | 7; 0; 12; 11; 19 | 143 |
| 6-05 | 49 | 6 | 9; 7; 7; 0; 11; 15 | 90 |
| 6-06 | 54 | 5 | 12; 17; 8; 8; 9 | 140 |
| 6-07 | 49 | 4 | 11; 11; 5; 22 | 117 |
| 6-08 | 56 | 4 | 14; 29; 4; 9 | 137 |
| 7-00 | (tổng quan hoặc tiêu đề mạch; 0) | — | — | 106 · lead 23 |
| 7-01 | 77 | 1 | 77 | 147 |
| 7-02 | 59 | 4 | 12; 17; 12; 18 | 138 |
| 7-03 | 59 | 4 | 19; 10; 20; 10 | 176 |
| 7-04 | 55 | 4 | 15; 11; 11; 18 | 78 |
| 7-05 | 49 | 2 | 40; 9 | 135 |
| 7-06 | 60 | 4 | 11; 12; 18; 19 | 142 |

## 16. Đối chiếu storyboard với deck (người viết deck, 2026-11-16)

Deck: `2627-1/lecture-10-gradient-chinh-sach-hoc-lien-tuc.html`, 54 trang, mã trang và thứ tự đúng mục 6. Mục 6 giữ bản dự kiến đã qua cổng duyệt; mặt trang cuối cùng nằm trong tệp deck. Bảng dưới ghi mọi chỗ deck lệch mục 6, gồm các sửa theo quyết định của điều phối viên (`review-log.md`, "Quyết định của điều phối viên về storyboard và cổng duyệt") và báo cáo cổng duyệt (mã N1, T1–T11, L1–L18). Kiểm máy lần cuối: `deck_lint.py` 0 phát hiện; `footer_check.py` 0 trang; `deck_check.py` console 0, pageerrors 0, failed 0, `.katex-error` 0.

| Trang | Lệch so với mục 6 | Lý do |
|---|---|---|
| 1-02 | "Hệ quả 02.10(b): (T1), (T3) …, $h$ cố định; với xác suất …" | dấu ";" tách giả thiết khỏi bảo đảm |
| 1-03 | mục 1 rút thành "Mô tả tối ưu chính sách và đại lượng ngẫu nhiên"; mục 2 "… và điều kiện đổi chỗ đạo hàm, kì vọng"; mục 3 thêm "không phụ thuộc hành động", "nêu trường hợp chệch" | L10 (+4 âm tiết) và trần 80 |
| 1-06 | dòng 1 thêm "(state)", "(action)" | tiếng Anh ở lần đầu trên trang nội dung (ghi chú §0) |
| 2-00 | dòng dẫn mới | L3 |
| 2-01 | dòng 1 thêm "chọn hành động theo chính sách (policy)" | tiếng Anh của "chính sách" ở lần đầu |
| 2-02 | "phần thưởng (reward)" | tiếng Anh ở lần đầu |
| 2-03 | bỏ dòng (PT); (MDP) thêm "luật chuyển (transition law)", "$r$ tất định, trong $[r_{\min},r_{\max}]$"; dòng Định nghĩa 10.1 bỏ vế sau | T4 (PT chuyển sang 4-06); L13 (dòng 21 âm tiết); "luật chuyển" dùng ở tiêu đề 3-08 nên phải có tên trên mặt trang trước |
| 2-04 | thêm "$r_t=r(S_t,A_t)$"; tích dùng `\textstyle\prod` | $r_t$ dùng trên mặt 3-08, 4-01; công thức thấp hơn để không chạm chân trang |
| 2-05 | bảng ba hàng ($\tau$ ghi theo $(a_0,S_1,a_1)$; $p_0$; $R$); phần thưởng viết theo cặp $(r(s,1),r(s,0))$; "chính sách bảng, $\theta=0$" vào dòng 1; dòng cuối "phân bố của $S_1$ phụ thuộc $\theta_{s_0}$" | bảng năm hàng chạm chân trang ở 1600×900 |
| 3-00 | dòng dẫn thêm "Khi môi trường không phụ thuộc tham số" | dòng dẫn mất giả thiết là lỗi hay lặp lại; Ví dụ 10.6 là phản ví dụ |
| 3-03 | "Trực quan." theo T6; dòng "Một lượt …" và "Ước lượng không cần …" gộp thành "Trung bình $m$ lượt độc lập: không chệch, hiệp phương sai chia cho $m$; không cần $\mu_0$, $P$, $r$" (L5); "gradient chính sách (policy gradient)" đưa lên mặt ở dòng Bảo đảm; bỏ "như Định nghĩa 10.2" | T6, L5; tiếng Anh ở lần đầu; trần 60 |
| 3-04 | bỏ dòng cuối; dòng bỏ giả thiết viết "Khi $P$ phụ thuộc $\theta$: …"; bước 3 ghi "((MDP): $\mu_0$, $P$ không phụ thuộc $\theta$)" | T6, L4 |
| 3-05 | dòng 1 thêm "$\mathcal T$ hữu hạn, cố định"; dòng 2 "Dùng khi chỉ phân bố chứa tham số (Định lý 10.4)"; "Nhắc lại:" đứng trước dòng Nhận xét 10.5; dòng Nhận xét 10.5 thêm "$R$ bị chặn"; dòng cuối "Giá đổi theo $\theta$: hỏng" | T3, L8, mục 6 cổng duyệt; không dẫn Mệnh đề 10.7 (trang sau) |
| 3-07 | công thức hiển thị thành nội dòng trong dòng 2; "Diễn giải:" thay bằng "Nhắc lại:" $1{,}7$/$1{,}8$ và "Do đó …"; phân tích $0{,}9$ vào ghi chú diễn giả | T9; chạm chân trang |
| 3-08 | "Kết luận:" viết "ngược dấu đạo hàm thật; ước lượng thiếu gradient của …" | tránh hai dấu ":" liên tiếp |
| 3-10 | dòng 3 thêm "$-J$ không lồi"; "Nhắc lại:" Mệnh đề 08.12 hai dòng (thêm "$\eta$ hằng", "Bảo đảm: điểm dừng xấp xỉ, theo kì vọng"); ghi chú diễn giả thêm "(đọc thêm ở Bài 08)" và lập luận vì sao $-J$ không lồi | T5; (C) sai vì $-J$ không lồi được dùng ở 7-02 nên phải có trên mặt trang trước |
| 3-11 | (a) nối vào dòng Bài tập 10.1; (b) tách hai dòng | L13 |
| 4-01 | (a), (b) cùng một dòng, công thức (b) nội dòng; "Trực quan." thêm vế "chỉ thêm nhiễu vào số hạng thứ $t$" | chạm chân trang; "Trực quan." nêu cơ chế (bài học deck 02) |
| 4-02 | dòng 1 rút; thêm "Trực quan." (khi biết lịch sử, gradient log có trung bình $0$; nhân với một số đã biết, trung bình vẫn bằng $0$); dòng cuối chuyển vào ghi chú diễn giả | T7 |
| 4-03 | "Nhắc lại:" thêm "tính chất tháp"; bước 3 ghi "(giả thiết giá trị nền)" trước $f=b_t$; ghi chú diễn giả thêm câu về $\mathcal F_t$ và Bổ đề 05.12 | L9 (giả thiết trong ngoặc), L14 |
| 4-04 | tiêu đề "Ví dụ: phương sai và độ chệch theo giá trị nền"; bảng dùng phân số gạch chéo; dòng $b^*$ viết "$b=J$ không tốt nhất"; F1 vẽ lại (mục 8 dưới) | tiêu đề cũ hai dòng và trang chạm chân trang; chữ trên hình ≥ 16 px |
| 4-05 | tiêu đề "Ví dụ: ba ước lượng trên quá trình hai bước"; cột cuối "Vết (trace)" | tiêu đề cũ hai dòng làm trang chạm chân trang; tiếng Anh ở lần đầu |
| 4-06 | bỏ dòng "Câu hỏi:"; dòng 1 liệt kê dữ kiện; thêm dòng (PT) đủ ba vế; "cộng $c$ chỉ dịch $J$"; dòng mô phỏng rút | T4, T8, L6, mục 6 cổng duyệt |
| 4-08 | (c) "có hợp lệ không? Tính kì vọng, phương sai …" | đề bài không rút thành mảnh câu |
| 5-01 | dòng 1 "Ví dụ mở đầu có hai nhiệm vụ, môi trường A và B"; thêm dòng "$w^{(0)}$: tham số khởi tạo; $w^{(k)}$: sau nhiệm vụ $k$"; dòng bộ nhớ "nhiệm vụ $k$ dùng $S^{(k)}$, $w^{(k-1)}$, $\le M$ điểm cũ" | $w^{(k)}$ dùng trên mặt 5-02 nên phải định nghĩa trước; trần 60 |
| 5-02 | ghi chú diễn giả bỏ câu nguồn gốc | T10 |
| 5-03, 5-04 | bảng và các dòng đặt trong `grid2`; 5-03 dòng 4 theo L11; 5-04 (a), (d) tách hai dòng | chạm chân trang; L11, L13 |
| 6-01 | dòng 1 "không cho biết tham số nào tốt trên mọi nhiệm vụ cùng lúc"; thêm "$\lambda\ge0$" | sát câu ghi chú cuối §7; giả thiết của Định nghĩa 10.12 |
| 6-02 | "Trực quan." theo L7; (c) nêu "$L_B+\tfrac\lambda2w^2$ cực tiểu tại $w_\lambda$"; (a) "dấu bằng ở bất đẳng thức sau chỉ tại $w=\tfrac12$" | L7; $w_\lambda$ phải được định nghĩa trên mặt trang |
| 6-03 | ngoặc đầu mục ghi giả thiết ($L_A$, $L_B$ có tâm $0$, $1$; bậc hai; $w^{(1)}=0$, $\Omega=1$; rủi ro cũ đầy đủ), phần kết quả ở cuối mục | L9 |
| 6-04 | tiêu đề "Ví dụ: năm hệ số chính quy hóa" (tên Ví dụ 10.14 của ghi chú); bảng năm cột không có cột $L_A+L_B$, tổng viết ở dòng riêng; không chú thích hình; dòng đánh đổi rút thành "giảm $L_A$ thì tăng $L_B$", định nghĩa tính bền vững (stability), tính mềm dẻo (plasticity) vào ghi chú diễn giả | trang chạm chân trang; chữ trên hình ≥ 16 px cần hình cao 310 px; "Ví dụ 10.14, Bước 3" ($\alpha$) giữ trong bảng |
| 6-05 | ghi chú diễn giả dùng câu của L16 | L16 |
| 6-06 | Giả thiết thêm "$w_1\in W$ tất định"; Bảo đảm thêm "($R$: bán kính)" | L1, L2 |
| 7-00 | dòng dẫn mới | T2 |
| 7-01 | bốn hàng: hàng Bổ đề 10.3 gộp vào hàng Định lý 10.4; hàng Nhận xét 10.16 thêm $\lVert w_1-u\rVert\le R$ và $\eta=R/(G\sqrt T)$; hàng Mệnh đề 10.13 bỏ $w_\lambda$, ô ý tưởng "tam giác; bình phương" | T11; bảng vừa một trang ở 1600×900 (`footer_check.py` 0), nên không tách hai trang |
| 7-02 | năm dòng theo N1, T1 và mục 6 cổng duyệt: "(T1) sai vì dữ liệu phụ thuộc $\theta$, (C) sai vì $-J$ không lồi"; "Dưới (MDP), (Π): ước lượng một lượt không chệch"; "Giá trị nền là hàm của lịch sử chỉ đổi phương sai"; "Cận với xác suất $\ge1-\delta$: chỉ cho chính sách cố định"; "Nhiệm vụ thay đổi cần giao thức nêu trước; hối tiếc tĩnh không chặn độ quên"; $L_A+L_B\ge\tfrac14$ "trong ví dụ bậc hai" ở ghi chú diễn giả | N1, T1; trần 60 |
| 7-03 | đề: "Nêu quá trình sinh dữ liệu, mục tiêu, đối tượng so sánh, đại lượng ngẫu nhiên và giả thiết cần đổi khi: (i) đánh giá …"; lời giải "(T3) thay bằng miền …" | L12; đề là câu đầy đủ |
| 7-06 | tài liệu viết gọn ("Sutton, Barto"; "UML (Shalev-Shwartz, Ben-David, 2014)"; bỏ "PNAS"); dòng khép học phần "Bốn bài toán: phân lớp có giám sát, …" | L15; trần 60 |

**Hình (thay mục 8 ở các điểm sau).** F1 `phuong-sai-gia-tri-nen.svg`: viewBox 560×380, chữ 26–28, nhãn điểm rút thành "b = 0", "b* = 3/2", "b = J", "b = 5" (giá trị nằm trong bảng của 4-04), vạch trục dọc 0, 1, 2; hiển thị lớp `figure short`. F2 `danh-doi-hai-nhiem-vu.svg`: viewBox 400×380, chữ 24–26, trục ghi "L_A (nhiệm vụ cũ)", "L_B (nhiệm vụ mới)", nhãn đường nét đứt "tổng = 1/4"; hiển thị lớp `figure short-l`, không chú thích (dòng tổng ngay dưới nêu "nét đứt: cận dưới $\tfrac14$ của (a)"). Dữ liệu và cách dựng như mục 8; script dựng: thư mục nháp `lec-10/writer/figs.py` (kiểm bốn điểm của F1 và năm điểm của F2 bằng phân số chính xác).

**Mật độ đo trên deck.** `deck_lint.py` 0 phát hiện. `deck_check.py` (cách đếm khác) báo vượt 60 ở 1-01 (bìa), 1-03 (80/80, trang mục tiêu), 7-01 (61, bảng tổng kết, trần 80) và 7-03 (64; `deck_lint.py` dùng trần 80 vì tiêu đề chứa "tổng kết"; bài tập tổng hợp có lời giải trên mặt trang). Dòng > 20 âm tiết theo `deck_check.py`: 1-05 (hộp câu hỏi), 2-00, 3-00, 4-00, 7-00 (dòng dẫn ≤ 25), 3-03, 3-05, 4-01, 4-02 (dòng Giả thiết hoặc Trực quan mang đủ điều kiện), 6-07, 7-03, 7-06. OVERFLOW 1–2 px ở 1-02, 4-07, 6-02, 6-03, 6-06, 6-07, 7-01 là đuôi SVG của `\sqrt` (báo động giả đã biết).


## 17. Sửa sau năm báo cáo duyệt (biên tập viên, 2026-11-16)

Theo bảng "Năm báo cáo duyệt và quyết định của điều phối viên" ở `review-log.md` và năm báo cáo `reviews/deck-{hoc-vien,toan-hoc,chuyen-gia,su-pham,mach-truyen}.md`. Deck sau sửa: 55 trang (7-03 tách thành đề 7-03 và lời giải 7-04; 7-04→7-05, 7-05→7-06, 7-06→7-07); Bài tập 10.5(c) chuyển lên sau Ví dụ 10.16 (6-06), học trực tuyến thành 6-07, Ví dụ 10.17 thành 6-08, theo thứ tự §8 → §9 của ghi chú (phát hiện nhẹ đã chấp nhận). Kiểm máy: `deck_lint.py` 0 phát hiện (không còn ngoại lệ 7-03); `footer_check.py` 0; `deck_check.py` console 0, pageerrors 0, failed 0, `.katex-error` 0, OVERFLOW 1–2 px chỉ ở các trang có `\sqrt` (1-02, 4-07, 6-02, 6-03, 6-07, 6-08, 7-01; báo động giả đã biết); `#/2`…`#/7` mở đúng L10-2-00…L10-7-00; →, ↓, Space, Esc hoạt động.

| Phát hiện (quyết định) | Trạng thái | Cách sửa hoặc lý do |
|---|---|---|
| 6-05 dòng mô phỏng (nghiêm trọng) | đã sửa | Mặt trang: "Mô phỏng hồi quy $y=wx$ (Phụ lục C), $L_A=\tfrac12(w^2+0{,}25)$: … về $0{,}25$, không về $\min=0{,}125$"; dòng trước "rủi ro cũ kì vọng giảm về $L_A(\tfrac12)=\tfrac58$"; "$L_B$ … biết đủ"; "điểm cực tiểu". Công thức hiển thị bỏ vế $\tfrac12\operatorname{Var}(w_M)$ (ở ghi chú diễn giả). |
| 7-02 dòng 1 và ghi chú diễn giả 1-05 (nghiêm trọng) | đã sửa | "(T1) sai: $\theta_j$ phụ thuộc $\tau_1,\ldots,\tau_{j-1}$"; "(C) sai: $-J$ không lồi (Ví dụ 10.7)"; "$\theta$ cố định: (T1) đúng; …". Ghi chú diễn giả 1-05 viết lại theo §1 của ghi chú và "Mục tiêu nói chung không lõm (Ví dụ 10.7)". |
| 7-02 (trung bình): Mệnh đề 10.13, ma trận đánh giá, đại lượng được chặn, dòng 3 | sửa một phần | Năm dòng (không phải sáu) để giữ trần 60: thêm "với xác suất ít nhất $1-\delta$, $\lvert\frac1m\sum_jR(\tau_j)-J(\theta)\rvert$ bị chặn", "giao thức, ma trận đánh giá", "xung đột buộc đánh đổi", "giá trị nền theo lịch sử chỉ đổi phương sai". Số hiệu "Mệnh đề 10.13" và "$L_A+L_B\ge\tfrac14$" chỉ ở ghi chú diễn giả; ghi chú diễn giả thêm "MDP của Ví dụ 10.2". |
| 1-02, 3-09: (G1), (G2); "điều kiện không chệch của Bài 05" | đã sửa | 1-02: "Định lý 05.14 cần (C), (G1) $\mathbb E_\xi\varphi(w,\xi)\in\partial F(w)$, (G2) …"; Hệ quả 02.10(b) thêm (T2), $\delta\in(0,1)$. 3-09: "Gradient ngẫu nhiên không chệch có điều kiện; (C) và (G1) của Định lý 05.14 cần $-J$ lồi"; ghi chú diễn giả nêu Bài tập 10.3(c). |
| 3-10: Mệnh đề 08.12 đủ đại lượng, điểm lặp | đã sửa | "**Bảo đảm:** theo kì vọng, $\frac1T\sum_j\mathbb E\lVert\nabla J(\theta_j)\rVert^2\le\frac{2(\sup J-J(\theta_1))}{\eta T}+\beta\eta\sigma^2$: điểm dừng xấp xỉ tại $\theta_\tau$, $\tau$ rút đều" ($F=-J$, $F(w_1)-F_*=\sup J-J(\theta_1)$); ghi chú diễn giả: không tại $\theta_{T+1}$, đọc thêm ở Bài 08. Tiêu đề "Ví dụ: một điểm dừng là điểm cực tiểu". |
| 4-01 "chỉ thêm nhiễu" | đã sửa | "chúng thêm vào số hạng thứ $t$ một đại lượng có kì vọng $0$"; ghi chú diễn giả: phương sai có thể tăng hoặc giảm. |
| 4-05: điều kiện, nghĩa giá trị nền, kết luận | đã sửa | "(iii) (ii) trừ phần thưởng kì vọng còn lại: $1{,}75;\,2;\,\tfrac12$"; "Đổi ví dụ ($r=-2$ ở $s_0$, luôn tới $s_1$, chọn ở $s_0$ không phụ thuộc $\theta$): phương sai (i) $0$, (ii) $1$; (ii) tăng phương sai." Cột đầu bảng ghi $\operatorname{Var}$ để giữ trần. |
| 3-03 "Trực quan."; 2-05 câu nối 2→3; 4-07 câu nối | đã sửa | 3-03: "Trung bình phần thưởng đã thu không chứa $\theta$: đạo hàm bằng $0$; gradient log đo ảnh hưởng của $\theta$ lên phân bố quỹ đạo." 2-05: dòng "Tác tử biết $\pi_\theta$, không biết $\mu_0$, $P$, $r$: không tính được $J$, $\nabla J$ bằng công thức." 4-07: dòng mở "$\theta$ cố định: các lượt thỏa (T1), có cận với xác suất cao."; tên kỹ thuật đủ "đảo cận đuôi thành bán kính và cỡ mẫu". |
| 2-03, 2-04: $\mu_0$, $H$, chính sách tất định; Mệnh đề 09.3 | đã sửa | 2-03: "$H$ bước mỗi lượt"; dòng "Phân bố trạng thái đầu (initial state distribution) $\mu_0$; luật chuyển trạng thái (transition law) $P(\cdot\mid s,a)$". Chính sách tất định "không khả vi tại $\theta_s=0$" chuyển vào ghi chú diễn giả kèm tên tiếng Anh (trần 60; người duyệt học viên cho phép). 2-04: bỏ Mệnh đề 09.3 khỏi ghi chú diễn giả; thêm "Tối ưu chính sách (policy optimization)" trên mặt trang. |
| 2-05, 3-07: ví dụ đi nhanh | đã sửa | 2-05: "Tổng phần thưởng kì vọng khi chọn $1$ hay $0$ ở $s_0$: $1{,}7$ hay $1{,}8$". 3-07: "$\theta_{s_1}$ (bốn quỹ đạo qua $s_1$, thừa số $a_1-\tfrac12$)"; "Vì $\tfrac{d}{d\theta}\pi_\theta(1\mid s_0)=\tfrac14$ tại $0$: …"; dãy số của $\theta_{s_2}$ vào ghi chú diễn giả. |
| 6-04: bền vững, mềm dẻo; "dọc đường biên" | đã sửa | Mặt trang: "Tính bền vững (stability): $L_A$ tăng ít; tính mềm dẻo (plasticity): $L_B$ nhỏ." và "… trade-off): tăng $\lambda$, $L_A$ giảm, $L_B$ tăng." Bảng sáu cột (thêm $L_A+L_B$), số viết thường thay KaTeX để bảng thấp hơn; không chú thích hình (giữ chân trang), alt nêu đường nét đứt là cận dưới của Mệnh đề 10.13(a). Nhãn trục SVG dùng chỉ số dưới (`tspan`). |
| 5-02 "trên tập kiểm tra"; 2-01/5-01 Phần B | đã sửa | 5-02: "… của $w^{(k)}$ trên tập kiểm tra của nhiệm vụ $i$"; chuyển đổi xuôi viết công thức trước, $\mathrm{acc}^\circ_i$ sau. 5-01: dòng "Cố định: $D_1,\ldots,D_K$, thứ tự; ngẫu nhiên: $S^{(k)}$, bộ nhớ, tập kiểm tra; so sánh: mô hình học chung hoặc riêng"; "quan sát cũ"; dòng "ví dụ mở đầu" vào ghi chú diễn giả. 2-01: "Tham số $\theta$ cố định: lượt độc lập cùng phân bố; …". |
| Trang bài tập: câu chữ theo `exercises.md`; bỏ khuôn ghi chú diễn giả; 7-03 | đã sửa, giữ ít phần hơn | 3-11: đề và (b) theo câu chữ, (a) vào ghi chú diễn giả (lời giải nêu $\pi_\theta(1)$, $J'$). 4-08: chỉ (c), câu hỏi theo câu chữ ("Giá trị nền này có hợp lệ theo Hệ quả 10.8 không? …"), phần (b) và kết luận so sánh vào ghi chú diễn giả; tiêu đề "Bài tập: giá trị nền trừ ở bước sau". 5-04: chỉ (a), đề theo câu chữ ("hàng: thời điểm $k$, cột: nhiệm vụ $i$" thay cho "hàng là … cột là …"); ý của (d) vào ghi chú diễn giả. 6-06: (c) theo câu chữ, lời giải bốn số. 7-03/7-04: đề theo câu chữ (bỏ "của câu (f) ở §12" và "hai thiết lập", vì deck không có §12 (f) và chỉ xét (i)); lời giải năm mục theo thứ tự năm câu hỏi, có đối tượng so sánh. Năm ghi chú diễn giả bỏ "Câu chữ đầy đủ của đề" và "… là bài về nhà"; "sigmoid" gọi tên ở 2-02. |
| 7-05 (nay 7-06) ghi chú diễn giả; 1-01 ghi chú diễn giả | đã sửa | Bỏ câu quy trình và câu nguồn gốc, thay bằng "Bài tập 10.9 tùy chọn.". 1-01: câu nội dung về REINFORCE và Mệnh đề 08.12 thay câu rào đón. |
| 1-03 mục tiêu 1, 3, 5 | đã sửa | "Mô tả tối ưu chính sách: đại lượng nào ngẫu nhiên"; "Chứng minh tổng phần thưởng từ bước hiện tại và giá trị nền không phụ thuộc hành động giữ kì vọng"; "… không đủ cho hai bài toán". Để giữ trần 80: mục 4 thành "tính độ quên" (ma trận đánh giá ở ghi chú diễn giả), "trường hợp chệch" của mục 3 ở ghi chú diễn giả. |
| 7-06 (nay 7-07) dòng khép học phần | đã sửa | "Bốn bài toán của học phần: phân lớp có giám sát (Bài 01–08), ước lượng mật độ (Bài 09), tối ưu chính sách và học liên tục (Bài 10)." Tên sách và bài báo chuyển vào ghi chú diễn giả; ghi chú diễn giả đủ hai vế của Phụ lục D. |
| 7-01 "$\mathcal T$ hữu hạn" | đã sửa | "$\mathcal T$ hữu hạn (hoặc Nhận xét 10.5); (MDP); (Π)" — ô (MDP) chỉ còn nhãn để bảng vừa một trang. |
| Mật độ ≤ 60 | đã sửa | `deck_lint.py` 0 phát hiện trên 55 trang. |
| Nhẹ: 3-05 "khả vi" | đã sửa | "… $p_\theta(\tau)$ khả vi, $f$ không chứa $\theta$"; "có hàm trội" → "hàm trội" trong danh sách điều kiện; "Giá đổi theo $\theta$: sai". |
| Nhẹ: ghi chú diễn giả 4-04 số bước | đã sửa | "bước 2 của ý tưởng chứng minh (Bước 1 của chứng minh Hệ quả 10.8)"; câu dài tách. |
| Nhẹ: nhãn SVG "L_A" | đã sửa | F2 dùng chỉ số dưới. |
| Nhẹ: "cực tiểu" làm động từ | đã sửa | 6-01 dùng $w^{(k)}\in\arg\min_w[\ldots]$ (hai công thức hiển thị); 6-02, 6-05 "điểm cực tiểu". |
| Nhẹ: tên đủ "độ chính xác phân lớp trung bình cuối cùng" | đã sửa | 5-03, 5-04. |
| Nhẹ: ghi chú diễn giả dẫn phần deck không có ("câu ôn nhanh", "khối ứng dụng", "câu hỏi cuối buổi", "câu (f)") | đã sửa | Thay bằng nội dung; một tên "ví dụ mở đầu" trong ghi chú diễn giả. |
| Nhẹ: năm ghi chú mở bằng độ sâu chứng minh | đã sửa | Câu độ sâu chuyển xuống cuối ở 3-01, 3-03, 4-01, 4-02, 6-02. |
| Nhẹ: 7-00 lặp 3-00 | đã sửa | Dòng dẫn mới: "Mỗi bảo đảm của bài là đồng nhất thức, tất định hoặc với xác suất cao, kèm giả thiết không được bỏ." 2-00, 4-00 đổi theo đề xuất của người duyệt sư phạm. |
| Nhẹ: 4-06 đối chứng $0/100$ | đã sửa | "…; có giá trị nền: $0/100$"; "người dùng nhấp ($X=1$)"; ghi chú diễn giả bỏ cặp tự hỏi tự đáp. |
| Nhẹ: 3-09 dẫn Định lý 10.4 | đã sửa | "(Định lý 10.4)" sau $\hat g_j$. |
| Nhẹ: 1-01 luận điểm thiếu tập hữu hạn | đã sửa | "… môi trường hữu hạn không phụ thuộc tham số …". |
| Nhẹ: 3-02 "Diễn giải:", "(b) sai" | đã sửa | "khi $\theta$ tăng, giá $[0,\theta]$ …"; "Bổ đề 10.3(b) không còn đúng"; ghi chú diễn giả theo Nhận xét 10.5. |
| Nhẹ: 3-03 "cùng $\theta$" | đã sửa | "Trung bình $m$ lượt độc lập cùng $\theta$". |
| Nhẹ: 3-05 ghi chú diễn giả về tái tham số hóa | đã sửa | Thêm một câu. |
| Nhẹ: 4-07 nghĩa dương | đã sửa | Ghi chú diễn giả: đánh giá $\theta_{T+1}$ trên các lượt mới chạy sau huấn luyện. |
| Nhẹ: 5-02 quy ước | đã sửa | Ghi chú diễn giả: "Các độ đo phụ thuộc quy ước …" (không câu nguồn gốc). |
| Nhẹ: 1-06 dấu phẩy, "rủi ro", tiêu đề | đã sửa | Tiêu đề "Ví dụ: robot chọn hành động và mô hình học lần lượt hai môi trường". |
| Nhẹ: dấu câu sau KaTeX xuống dòng | sửa một phần | Sửa ở 3-06, 5-04; các chỗ khác chỉ xuất hiện ở 390 px và phụ thuộc bề rộng, không sửa hàng loạt. |
| Nhẹ: 5-03, 5-04 cột $i=3$ bị che ở 390 px; 2-05 bảng dọc | không sửa | Cần sửa `lecture-course.css` (ngoài phạm vi ghi); bảng cuộn ngang tại chỗ có nhãn "↔ cuộn ngang" như quy định. Bảng 2-05 viết dọc tám hàng làm trang chạm chân trang ở 1600×900. |
| Nhẹ: 4-02 "Lưu ý:" giá trị nền dùng chung tham số; 6-07 "Nhắc lại:" tổng triệt tiêu | sửa một phần | Chỉ ở ghi chú diễn giả (4-04, 6-07): hai trang đã ở trần 60. |
| Nhẹ: F2 thiếu chú thích | không sửa | Thêm chú thích làm 6-04 chạm chân trang; dữ liệu của hình có trong bảng cùng trang và trong alt. |
| Nhẹ: storyboard mục 9, 12 | đã sửa | Mục 9 viết lại; mục 12 sửa các hàng 2-03, 2-04, 4-06, 4-08, 5-01, 5-04, 6-04, 6-06–6-08, 7-03–7-07. |

**Sáu điểm sửa nhỏ của điều phối viên (2026-11-16).** (1) 7-02: cận viết đủ, $\lvert\frac1m\sum_jR(\tau_j)-J(\theta)\rvert\le H(r_{\max}-r_{\min})\sqrt{\ln(2/\delta)/(2m)}$ — đã sửa. (2) 2-01: khôi phục dòng "Ngẫu nhiên: lượt, tham số, ước lượng gradient."; "môi trường cố định" chuyển vào ghi chú diễn giả (trần 60) — đã sửa. (3) 5-01: "tập kiểm tra độc lập" — đã sửa. (4) 7-07: giữ tên sách Sutton, Barto và tên bài báo Kirkpatrick và cộng sự, PNAS trên mặt trang; ba mục Sutton, Barto gộp một dòng, tác giả UML và cụm "(Bài 01–08)", "(Bài 10)" chuyển vào ghi chú diễn giả để giữ trần 60, giữ "ước lượng mật độ (Bài 09)" — đã sửa. (5) 6-04: thử KaTeX trong bảng; bảng cao hơn làm trang chạm chân trang hoặc thu hình F2 xuống dưới 16 px, nên giữ số viết thường — không sửa. (6) 5-04: trang ở trần 60, lời giải giữ dãy số — không sửa.

**Kiểm lại (`reviews/deck-recheck.md`, 2026-11-16).** R1 6-05: "rủi ro trên A $\tfrac12(w^2+0{,}25)$; rủi ro kiểm tra trên A: $0{,}624$ (tinh chỉnh); …"; công thức $\tfrac1{8M}$ chuyển vào dòng (giữ chân trang) — đã sửa. R2, R11 7-07: tên đủ "Shalev-Shwartz và Ben-David (2014), *Understanding Machine Learning: From Theory to Algorithms* (UML)"; "Học phần xét bốn bài toán: …" — đã sửa; **ngoại lệ trần: 7-07 có 70 âm tiết** (tên sách, tên bài báo), điều phối viên cho phép. R3 bỏ câu "Thiết lập (ii) …" — đã sửa. R4 2-01 "Tham số cố định …; tham số ở cập nhật $j$ …: (T1) sai" (bỏ "phân bố" trước $D_1,\ldots,D_K$ để giữ 60) — đã sửa. R5 3-09 — đã sửa. R6 7-02 "giá trị nền là hàm của lịch sử" — đã sửa; "một lượt" không lên mặt trang (vượt 60), có ở ghi chú diễn giả — sửa một phần. R7, R8, R9, R10 (đề 7-03 "Trả lời năm câu hỏi cho (i): …"), R14 — đã sửa. R12 4-07: thêm "Hệ quả 02.10(b) cho $R/4$" làm trang 63 âm tiết; giữ trong ghi chú diễn giả — không sửa trên mặt trang. R13 4-08: "(phương sai của (ii), …)" làm trang 61; giữ như đã chấp nhận — không sửa. R15: §12 "6-06" → "6-07", hàng §17 7-06 viết lại — đã sửa.
