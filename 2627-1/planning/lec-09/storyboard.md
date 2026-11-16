# Storyboard — Bộ trang chiếu Bài 09: Học chuỗi và mô hình sinh

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-11-16 bởi tác tử lập storyboard. Nguồn nội dung duy nhất: `materials/lec-09/lecture-note.md` (bản hiện hành); bài tập: `materials/lec-09/exercises.md`. Quy định: `CLAUDE.md` § Slide decks, `common-brief.md` (gồm "Các quy định dễ sót" và các bài học từ duyệt deck 01–06), `brief-storyboard.md`, `../rl-plan/CLAUDE.md` § Deck structure and content, nhật ký yêu cầu 2026-11-13 hàng 1–5, quyết định của điều phối viên trong `lec-0{1,…,8}/review-log.md` § Bộ trang chiếu, ba báo cáo `lec-0{5,6,7}/reviews/deck-storyboard-gate.md`. Khuôn bố cục theo storyboard Bài 08 (`planning/lec-08/storyboard.md`); deck Bài 06 làm mẫu markup (`<ol>` cho bước chứng minh, giả thiết trong ngoặc đầu mục; tiêu đề trang kỹ thuật là tên kỹ thuật). Mọi mã trang có dạng `L09-k-mm`; trong bảng viết gọn `k-mm`.

Số âm tiết trong tệp này đếm bằng script (mục 15) theo cách của `deck_lint.py`: token cách nhau bởi khoảng trắng có chữ cái hoặc chữ số; số viết trong câu có tính; chữ trong ô bảng có tính, số trong bảng và KaTeX không tính; mỗi công thức hiển thị là một dòng. Điều phối viên đếm lại trên deck.

UML: không đọc PDF trong vai này (bản giao việc chỉ cho phép ghi chú và `exercises.md`). Các mục UML và bài báo của Kingma và Welling (2014) trên trang "Tài liệu tham khảo" lấy từ §13 của ghi chú; số trang PDF lấy từ `outline.md` §7 (UML §24.1 tr. 343–347, §24.2 tr. 347, §24.4–24.4.1 tr. 348–352, §24.4.2 tr. 352–353; bài báo §2.1–2.4 tr. 2–5, §3 tr. 5–6, Phụ lục B tr. 10–11).

## 1. Tên tệp và tiêu đề

- **Tệp deck:** `2627-1/lecture-09-hoc-chuoi-mo-hinh-sinh.html` (slug ASCII từ tên bài "Học chuỗi và mô hình sinh").
- **Tiêu đề deck (h1 trang bìa):** "Học chuỗi và mô hình sinh" (đúng tên bài của ghi chú).
- **`<title>`:** "Bài 09: Học chuỗi và mô hình sinh".
- **Chân trang:** "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài 09".
- **Liên kết viewer:** `material-viewer.html?doc=materials/lec-09/lecture-note.md&deck=lecture-09-hoc-chuoi-mo-hinh-sinh.html` và `…exercises.md&deck=…`.
- **Màn hẹp:** chế độ đọc của `lecture-course.css` (`.slides` bọc trong `div.lecture-viewport`, script màn hẹp của `lecture-template.html`); bảng không bọc `.table-scroll` (lớp này không có trong `lecture-course.css`); ở màn hẹp, bảng và công thức rộng cuộn ngang tại chỗ theo quy tắc sẵn có của `lecture-course.css`, như deck 01–08 (mục 16).
- **Trang cuối deck Bài 08** (7-07 của storyboard Bài 08) nhận liên kết tới tệp này khi deck Bài 09 xong.

## 2. Khung lý thuyết chung

**Vấn đề trung tâm (hộp "Vấn đề trung tâm", bằng lời, ≤ 30 âm tiết).** "**Câu hỏi:** học một phân bố xác suất và học một chuỗi như thế nào?" (câu hỏi trung tâm của ghi chú, đoạn mở đầu dòng 5; `outline.md` §1; 16 âm tiết kể cả nhãn). Câu hỏi thật, không gợi câu trả lời; trang 7-02 trả lời cho cả bài.

**Luận điểm (trang bìa, một câu, có điều kiện, bằng lời, ≤ 50 âm tiết).** "Với hàm lỗi log, ước lượng hợp lý cực đại là tối thiểu hóa rủi ro thực nghiệm, ở mức tổng thể chọn mô hình gần phân bố thật nhất theo phân kì Kullback–Leibler, và khi các chuỗi được rút độc lập, cỡ mẫu là số chuỗi." (Định nghĩa 09.2, Hệ quả 09.9, §1 mục 7, §10 đoạn 1; 47 âm tiết theo script.) Điều kiện nằm ở "Với hàm lỗi log", "ở mức tổng thể" (bảo đảm không có tập huấn luyện) và "khi các chuỗi được rút độc lập" (Thiết lập A). Câu không nói gì về cỡ mẫu hữu hạn hay Thiết lập B; ghi chú diễn giả 1-01 nêu hai giới hạn này.

**Trọng tâm trực quan của deck.** Năm chỗ, theo yêu cầu của điều phối viên và các mục của ghi chú:
1. **Dữ liệu chuỗi phá giả thiết độc lập giữa các kí tự, không phá giữa các chuỗi** (1-06, 2-02, 3-04, 3-06, 3-07, 3-08, 7-03): $\Pr(x_3=\mathtt B\mid x_2=\mathtt A)=0{,}7$ khác $\Pr(x_3=\mathtt B\mid x_2=\mathtt B)=0{,}4$ (Ví dụ 09.1); Bài tập 09.1(c) ($0{,}40$ so với $0{,}69$: kí tự cách hai vị trí vẫn phụ thuộc trong mô hình bigram); bán kính Hoeffding theo kí tự $0{,}5754$ với $50$ chuỗi, so với con số sai $0{,}0407$ khi coi $10^4$ kí tự là độc lập (Ví dụ 09.4); cửa sổ chồng lấn chia ngẫu nhiên cho MSE $0{,}2$ dưới rủi ro nhỏ nhất $1$ (Ví dụ 09.5, hình F1); bài tập tổng hợp: $200$ chuỗi kiểm tra, không phải $40\,000$ kí tự (Bài tập 09.6(b)).
2. **Phân rã theo bước** (1-06, 3-01, 3-02, 3-03): hàm lỗi log của chuỗi là tổng các hàm lỗi log có điều kiện, $1{,}784=0{,}511+0{,}357+0{,}916$; đồng nhất thức đúng với mọi phân bố (Mệnh đề 09.3), mỗi số hạng là một bài toán phân lớp kí tự kế tiếp; giả thiết mô hình chỉ vào khi chọn ngữ cảnh.
3. **Hàm lỗi log và hợp lý cực đại cho mô hình sinh** (2-03, 2-04, 2-05, 2-06, 4-02, 4-04, 4-05): ước lượng hợp lý cực đại là ERM với hàm lỗi log; rủi ro kì vọng bằng entropy cộng phân kì KL thuận; rủi ro thực nghiệm có thể xuống dưới entropy ($0{,}6109<0{,}6730$) nhưng rủi ro kì vọng thì không ($0{,}6956$).
4. **Hàm lỗi log không bị chặn: không chuyển kết quả của hàm lỗi bị chặn** (2-03, 2-06, 3-07, 4-06, 4-07, 7-02): cận Hoeffding chỉ áp dụng khi mọi xác suất của mô hình $\ge c>0$ (Ví dụ 09.4); ước lượng hợp lý cực đại không làm trơn có $\mathbb E_SL_D(\hat\theta)=+\infty$ với mọi $m$ (Ví dụ 09.7); với mật độ, $\inf L_s=-\infty$ khi $m=1$ (Bài tập 09.8(c)); lỗi kiểm tra $+\infty$ ở $m=1$ (Ví dụ 09.8). Deck không nêu cận nào cho hàm lỗi log mà ghi chú không có lập luận riêng; hai bảo đảm cho cỡ mẫu hữu hạn duy nhất là Ví dụ 09.4 (mô hình cố định, $c>0$, tập kiểm tra) và Bài tập 09.9 (hai quan sát giả), như §10 của ghi chú.
5. **Khe của cận dưới bằng chứng và điều kiện của tái tham số hóa** (5-02, 5-04 với hình F2, 6-02, 6-05, 6-06): $\ln p_\theta(2)=\operatorname{ELBO}+\text{khe}$, khe bằng KL tới hậu nghiệm ($1{,}1534$ khi $q_\phi$ là tiên nghiệm, $0$ tại hậu nghiệm); gradient theo đường đi không chệch, phương sai $1$ và $6$ so với $29{,}027$ của ước lượng gradient log (Ví dụ 09.11); với hàm chỉ báo, ước lượng theo đường đi bằng $0$ thay cho $0{,}3521$ (Ví dụ 09.12).

**Chuỗi phụ thuộc yếu.** Ghi chú không có bất đẳng thức tập trung nào cho chuỗi phụ thuộc (Thiết lập B); §1 và Ví dụ 09.5 viết "một bảo đảm cần thêm giả thiết về sự phụ thuộc giữa các cửa sổ". Deck nói đúng điều này (2-02, 3-08, 7-02, 7-04 câu 2) và không thêm giả thiết trộn hay cận nào.

**Đối tượng và kí hiệu chung** (ghi chú §1–§2):
- bảng chữ $\mathcal A$, kí tự $\mathtt A,\mathtt B,\ldots$ (chữ đơn cách); chuỗi $x_{1:n}$, kí tự $x_j$, tiền tố $x_{<j}$; độ dài $n$, $n_i$, $n(x)$; độ dài ngữ cảnh $k$, cửa sổ $u_j$; kí tự kết thúc $\mathtt E$;
- tập huấn luyện $S=(X^{(1)},\ldots,X^{(m)})\sim D^m$, tập cố định $s=(x^{(1)},\ldots,x^{(m)})$; tập kiểm tra $V=(V_1,\ldots,V_{m_v})$, $L_V$;
- lớp mô hình $\{p_\theta:\theta\in\Theta\}$, $p_D$; hàm lỗi log $\ell(\theta,x)=-\ln p_\theta(x)$, $\ell_{\mathrm{len}}$; $L_D$, $L_S$, $L_s$, $\hat\theta$; $c$; $\mathrm H$, $\mathrm h$, $\mathrm{KL}$; $\mathrm{Ber}(\theta)$, $m_1$;
- biến ẩn $v\in\mathcal V$, $p_\theta(x,v)$, $p_\theta(v)$, $p_\theta(x\mid v)$, $p_\theta(v\mid x)$; $q_\phi(\cdot\mid x)$, $\phi\in\Phi$, $q$, $q_i$, $\theta_t$; $\operatorname{ELBO}(\theta,\phi;x)$, $\operatorname{ELBO}(\theta,q;x)$;
- nhiễu phụ $\zeta$, $g_\phi$, $\kappa(\phi,\zeta)$, $F(\phi)$, $N_0$, $U$, $M$; $U_0$ (biến đều của Ví dụ 09.12);
- cục bộ của ví dụ và bài tập: $b$ (Ví dụ 09.4); $\pi_0$, $\pi$ (Bài tập 09.1); $p_{\theta_1},p_{\theta_2},p_{\theta_3}$ (Ví dụ 09.13); $W$, $w$, $\varphi$, $G$, $R$, $T$ (Bài tập 09.7, theo Bài 05).

**Giả thiết** (ghi chú §2, danh sách nhãn đậm): (T1) với quan sát là cả chuỗi, kể cả độ dài; (T7) tập kiểm tra độc lập; xác suất bị chặn dưới $p_\theta(x_j\mid x_{<j})\ge c>0$; entropy hữu hạn và khả tích; khả tích của cận dưới bằng chứng; bước M; đổi chỗ đạo hàm và kì vọng. Không kết quả nào giả sử tính lồi. Deck nêu (T1), (T7), $c$ ở trang 2-03; các giả thiết còn lại nêu trên trang kết quả dùng chúng (như ghi chú dẫn nhãn §2 trong các khối).

**Chuỗi định nghĩa → kết quả → phương pháp.**
1. Câu hỏi mở đầu: một nhãn ($-\ln0{,}8\approx0{,}223$) và một chuỗi ($\mathtt{ABB}$: $0{,}168$; $1{,}784=0{,}511+0{,}357+0{,}916$).
2. Thiết lập bảy thành phần (§1) → Định nghĩa 09.1 (Thiết lập A, B) → kí hiệu, ba điểm khác của hàm lỗi log, giả thiết (§2) → Ví dụ 09.1 và ứng dụng chuỗi DNA (§3) → Định nghĩa 09.2 (mô hình xác suất, độ hợp lý, hàm lỗi log, MLE) → Ví dụ 09.2 (Bernoulli) (§4).
3. Mệnh đề 09.3 (quy tắc nhân xác suất) → Định nghĩa 09.4 (mô hình tự hồi quy, ngữ cảnh bậc $k$, độ bối rối, học theo đáp án) → Ví dụ 09.3 ($\mathtt{ABB}$) → Nhận xét 09.5 (kí tự kết thúc) (§5).
4. Quan sát độc lập ở cấp chuỗi → Ví dụ 09.4 (Hoeffding ở cấp chuỗi) → Ví dụ 09.5 (rò rỉ thông tin) → Định nghĩa 09.6 (hàm lỗi tổng, hàm lỗi chuẩn hóa) → Ví dụ 09.6 (§6).
5. Định nghĩa 09.7 (entropy, entropy chéo, KL) → Mệnh đề 09.8 → Hệ quả 09.9 → câu hỏi rủi ro thực nghiệm dưới entropy → Ví dụ 09.7 (rủi ro kì vọng vô hạn; làm trơn cộng một) → Ví dụ 09.8 (bigram DNA) (§7).
6. Định nghĩa 09.10 (biến ẩn) → Ví dụ 09.9 (Gauss tuyến tính) → Định nghĩa 09.11 (ELBO) → Định lý 09.12 → Ví dụ 09.10 → Hệ quả 09.13 (EM) (§8).
7. Định nghĩa 09.14 (tái tham số hóa, hai ước lượng gradient) → Mệnh đề 09.15 → Ví dụ 09.11 (Gauss) → Ví dụ 09.12 (hàm chỉ báo, Bernoulli) → Ví dụ 09.13 (độ hợp lý và dữ liệu sinh ra) (§9).

**Loại bảo đảm của từng kết quả** (§10 đoạn 2 của ghi chú): Mệnh đề 09.3 và Định lý 09.12 là đồng nhất thức tất định; Mệnh đề 09.8 và Hệ quả 09.9 là kết quả tổng thể, kì vọng theo $D$, không có tập huấn luyện; Hệ quả 09.13 tất định trên tập huấn luyện cố định, không chứa $L_D$; Mệnh đề 09.15 là kì vọng theo nhiễu phụ, tất định theo $\phi$. Mức chứng minh: Mệnh đề 09.3, 09.8, Hệ quả 09.9, Định lý 09.12, Hệ quả 09.13 *chứng minh đầy đủ*; Mệnh đề 09.15 *phác thảo* (chi tiết ở Phụ lục B). Ghi chú không có kết quả *đọc thêm*. Ghi chú diễn giả của mỗi trang kết quả nêu mức chứng minh.

**Giới hạn áp dụng** (ghi chú §10): hàm lỗi log không bị chặn, cần cận dưới cho xác suất (Ví dụ 09.4, 09.7); bán kính $0{,}0407$ của phép đếm theo kí tự không được Định lý 02.7 chứng minh; chia ngẫu nhiên cửa sổ cho MSE $0{,}20$ dưới rủi ro nhỏ nhất $1$; hỗn hợp cách giá trị tối ưu không quá $0{,}0059$ nat mỗi tọa độ nhưng $99\%$ điểm rút từ thành phần nhiễu; khe của ELBO bằng KL tới hậu nghiệm ($1{,}1534$ khi $q_\phi$ là tiên nghiệm); với hàm chỉ báo hay biến rời rạc, ước lượng theo đường đi cho $0$ thay cho $0{,}3521$; $-\operatorname{ELBO}$ nói chung không thỏa (C). Phụ lục A (phép tính Gauss) vào ghi chú diễn giả 5-01, 5-04, 6-05; Phụ lục B vào trang 6-03; Phụ lục C (giao thức thí nghiệm) vào ghi chú diễn giả 3-08, 4-07, 7-03; Phụ lục D vào trang 3-02 và 5-05.

## 3. Bảng mạch

Bảy mạch theo đúng thứ tự các mục của ghi chú; mỗi mạch ứng với các mục liên tiếp. Mạch 2 gộp §1–§4 (thiết lập, giả thiết, ví dụ xuyên suốt, hàm lỗi log và ước lượng hợp lý cực đại): bốn mục này cùng trả lời "hàm lỗi nào, quan sát nào". Mạch 3 gộp §5–§6: phân tích tự hồi quy (§5) cho hàm lỗi của chuỗi dạng tổng, §6 nói tổng đó là một quan sát; tách hai mục thành hai mạch làm deck có tám mạch. Mạch 5 (§8) và mạch 6 (§9) tách vì mỗi mạch có một kết quả chính, một trang ý tưởng chứng minh và một bài tập riêng. Bảng đối chiếu trang → khối ghi chú ở mục 12.

| N | Tên mạch | Mục ghi chú | Chức năng | Đầu vào | Đầu ra | `strand-lead` (âm tiết) | Từ khóa | Trang | Phút |
|---|---|---|---|---|---|---|---|---:|---:|
| 1 | Mở đầu | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết | Bìa, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, ví dụ dẫn nhập | Bài 01: rủi ro, ERM, hàm lỗi log (Nhận xét 01.2); Bài 02: Hệ quả 02.10, Nhận xét 02.11 | Câu hỏi: $m$ chuỗi ba kí tự có giống $3m$ quan sát độc lập không | (không có trang tiêu đề mạch) | — | 6 | 9 |
| 2 | Hàm lỗi log và ước lượng hợp lý cực đại | §1–§4 | Thiết lập; Định nghĩa 09.1 (Ví dụ 09.1 trên cùng trang); hàm lỗi log và giả thiết; Định nghĩa 09.2; Ví dụ 09.2 | hàm lỗi log của một nhãn và của một chuỗi (1-06) | Quan sát là cả chuỗi; ước lượng hợp lý cực đại là ERM với hàm lỗi log; hàm lỗi này không bị chặn | "Chọn mô hình gán xác suất lớn nhất cho tập huấn luyện là tối thiểu hóa rủi ro thực nghiệm với hàm lỗi log." (24) | Thiết lập A · Thiết lập B · tập kiểm tra · độ hợp lý · ước lượng hợp lý cực đại | 6 | 15,5 |
| 3 | Phân tích tự hồi quy và quan sát độc lập ở cấp chuỗi | §5–§6 | Mệnh đề 09.3 (trực quan, phát biểu) và ý tưởng chứng minh; Định nghĩa 09.4 với Ví dụ 09.3; Bài tập 09.1(a), (c); quan sát độc lập ở cấp chuỗi và Ví dụ 09.4 (hai trang); Ví dụ 09.5 (hình F1); Nhận xét 09.5, Định nghĩa 09.6, Ví dụ 09.6 | ERM với hàm lỗi log trên các chuỗi; Thiết lập A, B | $\ell(\theta,x_{1:n})=\sum_j-\ln p_\theta(x_j\mid x_{<j})$; cỡ mẫu trong cận là số chuỗi; chia cửa sổ theo thời gian; ghi rõ mục tiêu khi độ dài khác nhau | "Hàm lỗi log của một chuỗi là tổng các hàm lỗi theo từng kí tự, nhưng quan sát độc lập vẫn là cả chuỗi." (24) | phân tích tự hồi quy · độ bối rối · cấp chuỗi · rò rỉ thông tin · hàm lỗi chuẩn hóa theo độ dài | 10 | 22,5 |
| 4 | Entropy và phân kì Kullback–Leibler | §7 | Định nghĩa 09.7; Mệnh đề 09.8 (trực quan, phát biểu) và ý tưởng chứng minh; Hệ quả 09.9; rủi ro thực nghiệm dưới entropy; Ví dụ 09.7; Ví dụ 09.8; Bài tập 09.3(b), (c) | $L_D(\theta)=\mathbb E_D[-\ln p_\theta(X)]$ phụ thuộc $D$ chưa biết | $L_D=\mathrm H(p_D)+\mathrm{KL}(p_D\Vert p_\theta)$; MLE tổng thể làm nhỏ nhất KL thuận; trên tập huấn luyện hữu hạn, $\mathbb E_SL_D(\hat\theta)$ có thể vô hạn | "Với hàm lỗi log, rủi ro kì vọng bằng một số chỉ phụ thuộc phân bố thật cộng một độ lệch không âm." (23) | entropy · phân kì Kullback–Leibler · đặc tả đúng · quá khớp · làm trơn cộng một | 9 | 22 |
| 5 | Mô hình biến ẩn và cận dưới bằng chứng | §8 | Định nghĩa 09.10 với Ví dụ 09.9; Định nghĩa 09.11 và Định lý 09.12 (trực quan, phát biểu); ý tưởng chứng minh; Ví dụ 09.10 (hình F2); Hệ quả 09.13; Bài tập 09.4(b) | Mệnh đề 09.8 cho $p_\theta(x)$; $\mathrm{KL}\ge0$ | $\ln p_\theta(x)=\operatorname{ELBO}+\mathrm{KL}(q\Vert p_\theta(\cdot\mid x))$; EM không làm giảm log độ hợp lý | "Khi có biến không quan sát được, log độ hợp lý bị chặn dưới bởi một đại lượng ước lượng được bằng rút mẫu." (25) | biến ẩn · hậu nghiệm · cận dưới bằng chứng · khe · thuật toán EM | 7 | 18 |
| 6 | Tái tham số hóa và so sánh các mô hình sinh | §9 | Định nghĩa 09.14; Mệnh đề 09.15 (trực quan, phát biểu) và ý tưởng chứng minh; trang kỹ thuật "Đổi chỗ đạo hàm và kì vọng"; Ví dụ 09.11; Ví dụ 09.12; Ví dụ 09.13; Bài tập 09.7(c), (d) | ELBO là một kì vọng theo $q_\phi$; cần gradient theo $\phi$ | $\nabla F(\phi)=\mathbb E\nabla_\phi\kappa(\phi,\zeta)$ dưới (i)–(iii); hàm nhảy làm hỏng; độ hợp lý và dữ liệu sinh ra là hai tiêu chí | "Tái tham số hóa cho gradient không chệch khi hàm khả vi liên tục, khả tích và có gradient bị chặn bởi hàm khả tích." (25) | tái tham số hóa · gradient theo đường đi · gradient log · hàm trội · dữ liệu sinh ra | 9 | 22,5 |
| 7 | Tổng kết | §10–§13 | Bảng kết quả, trả lời vấn đề trung tâm, bài tập tổng hợp (Bài tập 09.6(b)), tự kiểm tra, bài tập về nhà, tài liệu | mọi kết quả | Cầu nối sang Bài 10 | "Mỗi kết quả của bài thuộc một loại bảo đảm: tất định, tổng thể hoặc kì vọng theo nhiễu phụ." (20) | — | 8 | 10,5 |
| | **Tổng** | | | | | | | **55** | **120** |

**Deck cuối: 55 trang** (thêm 3-05, lời giải Bài tập 09.1, mục 16; sau năm báo cáo duyệt: bỏ 2-06, tách 7-03 thành 7-03 và 7-04, mục 17). Bản storyboard trước cổng duyệt: số trang (54) vượt mục tiêu 45–52 và dưới trần 55. Lý do (ghi vào `review-log.md` nếu điều phối viên chấp nhận): sáu kết quả chính có trang phát biểu, bốn có trang "Ý tưởng chứng minh" riêng (Mệnh đề 09.3, 09.8, Định lý 09.12, Mệnh đề 09.15), một kỹ thuật dùng lại ở Bài 10 có trang riêng, mười bốn ví dụ đánh số của ghi chú và bảy trang bài tập (một cho mỗi mạch nội dung, thêm bài tổng hợp). Đã gộp để giữ 54: Ví dụ 09.1 vào trang Định nghĩa 09.1 (2-02); khối ứng dụng §3 vào ghi chú diễn giả 2-01 và trang Ví dụ 09.8 (4-07); Ví dụ 09.3 vào trang Định nghĩa 09.4 (3-03); Ví dụ 09.9 vào trang Định nghĩa 09.10 (5-01); Định nghĩa 09.11 vào trang Định lý 09.12 (5-02); Nhận xét 09.5, Định nghĩa 09.6 và Ví dụ 09.6 chung trang 3-09; Hệ quả 09.9 và Hệ quả 09.13 có dòng "Chứng minh." trên trang phát biểu thay cho trang ý tưởng chứng minh riêng (mục 11, điểm 2); Ví dụ 09.7 Bước 1–2 vào ghi chú diễn giả 4-06. Phương án về 52 trang ở mục 11, điểm 1.

## 4. Bảng kết quả chính

Số hiệu theo ghi chú. Mọi phát biểu rút gọn trên trang dùng "Giả thiết:" và "Bảo đảm:", giữ đủ giả thiết, lượng từ và loại bảo đảm của ghi chú.

| Kết quả | Loại bảo đảm | (a) Trực quan | (b) Ý tưởng chứng minh | (c) Kỹ thuật | (d) Ví dụ bổ trợ | Trang |
|---|---|---|---|---|---|---|
| **Mệnh đề 09.3** (quy tắc nhân xác suất cho chuỗi; chứng minh đầy đủ, Phụ lục D) | tất định, mọi chuỗi; với mọi hàm xác suất $p_1$ trên $\mathcal A^n$ | Mỗi thừa số là một bài toán phân lớp kí tự kế tiếp với ngữ cảnh là tiền tố; (a), (b) đúng với mọi phân bố, giả thiết mô hình chỉ vào khi chọn ngữ cảnh hay kiến trúc. Thay một bảng $\lvert\mathcal A\rvert^n-1$ tham số ($4^{200}-1$) bằng các xác suất có điều kiện. Cực biên: tiền tố có xác suất $0$ cho hai vế bằng $0$. | Bốn bước: định nghĩa xác suất có điều kiện cho $p_1(x_{1:j})=p_1(x_{<j})p_1(x_j\mid x_{<j})$; nhân từ $j=1$ đến $n$, giản ước (tích triệt tiêu), $p_1(x_{<1})=1$; tiền tố xác suất $0$: $p_1(x_{1:n})\le p_1(x_{<j})=0$; (b) lấy $-\ln$; (c) tổng theo kí tự cuối bằng $Q_{j-1}$ vì mỗi hàng có tổng $1$, quy nạp từ $j=n$. Bỏ giả thiết "mỗi hàng có tổng $1$": hàng $(0{,}5;\,0{,}7)$ không xác định mô hình tự hồi quy (đoạn sau Định nghĩa 09.4). | Một dòng "Kỹ thuật." trên 3-02: lấy tổng theo kí tự cuối. Dùng lại ở Bài tập 09.1(d) (trong bài); Bài 10 viết xác suất quỹ đạo là tích các thừa số, không nhắc kỹ thuật này. | Câu hỏi mở đầu ($0{,}168$; $1{,}784=0{,}511+0{,}357+0{,}916$); Ví dụ 09.3 ($1{,}7838$; $0{,}5946$; $1{,}8123$; chuẩn hóa tám chuỗi); Bài tập 09.1(a), (c). | 1-06, 3-01, 3-02, 3-03, 3-04 |
| **Mệnh đề 09.8** (rủi ro với hàm lỗi log bằng entropy cộng phân kì KL; chứng minh đầy đủ) | tổng thể: kì vọng theo $D$, không có tập huấn luyện; $\theta$ cố định | Phần thứ nhất chỉ phụ thuộc phân bố thật và là giá trị tốt nhất; phần thứ hai đo độ lệch của mô hình, bằng $0$ khi mô hình trùng phân bố thật. Cực biên: $p_\theta=0$ tại một điểm có $p_D>0$ cho cả hai vế $+\infty$. Mật độ: entropy vi phân có thể âm. | Bốn bước: $p_\theta=0$ trên giá cho $+\infty$ hai vế; trên giá, tách $-\ln p_\theta=-\ln p_D+\ln(p_D/p_\theta)$, nhân $p_D$, cộng hai tổng nhờ $\mathrm H(p_D)<\infty$; $\ln t\le t-1$ với $t=p_\theta/p_D$ cho $-\mathrm{KL}\le\sum_{p_D>0}p_\theta-1\le0$; dấu bằng ($t=1$ trên giá, $p_\theta=0$ ngoài giá); (c) tích phân thay tổng. Bỏ $\mathrm H(p_D)<\infty$: hai tổng có thể là $\infty-\infty$, phép cộng theo số hạng không hợp lệ. | Một dòng "Kỹ thuật." trên 4-03: $\ln t\le t-1$, dấu bằng chỉ khi $t=1$ (câu ôn nhanh 2). Dùng lại trong bài ở 5-03 bằng "Nhắc lại:"; Bài 10 không dùng (tìm "KL", "t-1" trong ghi chú Bài 10: $0$ kết quả), nên không có trang riêng. | Phân kì KL không đối xứng ($0{,}0226$; $0{,}0216$); rủi ro thực nghiệm dưới entropy ($0{,}6109$; $0{,}6730$; $0{,}6956$); Ví dụ 09.7; Ví dụ 09.8 ($1{,}0904$); Ví dụ 09.13 ($1{,}4189$); Bài tập 09.3(b), (c). | 4-01, 4-02, 4-03, 4-05, 4-08 |
| **Hệ quả 09.9** (ước lượng hợp lý cực đại tổng thể và phân kì KL thuận; chứng minh đầy đủ) | tổng thể | Vì $\mathrm H(p_D)$ không phụ thuộc $\theta$, làm nhỏ nhất $L_D$ là làm nhỏ nhất KL thuận; đặc tả sai để lại phần chênh $\inf_\Theta\mathrm{KL}$ dù có vô hạn dữ liệu. | Một dòng "Chứng minh." trên 4-04: trừ hai đẳng thức của Mệnh đề 09.8(a), hợp lệ vì $\mathrm H(p_D)$ hữu hạn; khi $L_D(\theta)=+\infty$, KL cũng $+\infty$, hai tiêu chí cùng loại $\theta$ đó. | Không có kỹ thuật mới. | Bài tập 09.3(c) (chiều thuận loại mô hình bỏ một điểm của giá). | 4-04, 4-08 |
| **Định lý 09.12** (đồng nhất thức của cận dưới bằng chứng; chứng minh đầy đủ) | tất định, cho từng $x$; (d) trên tập huấn luyện cố định | Bằng chứng không đổi khi đổi $q$; cực đại hóa ELBO theo $\phi$ thu hẹp khe, tức kéo $q$ về hậu nghiệm. Cực biên: $q$ bằng hậu nghiệm cho khe $0$; $q$ đặt khối lượng ở chỗ $p_\theta(x,v)=0$ cho $\operatorname{ELBO}=-\infty$. | Bốn bước: Bayes cho từng $v$ có $p_\theta(x,v)>0$ (dùng $0<p_\theta(x)<\infty$); thêm bớt $\ln q(v)$ (dùng giả thiết về $q$); lấy $\mathbb E_q$, hai ngoặc khả tích (dùng khả tích) cho (a); $\mathrm{KL}\ge0$ như Mệnh đề 09.8 cho (b); tách $\ln p_\theta(x,v)$ cho (c), lấy trung bình cho (d). Bỏ giả thiết về $q$: Phạm vi của định lý, Bài tập 09.4(c). Hậu nghiệm là khối lượng điểm: KL từ mọi mật độ bằng $+\infty$ (đoạn sau Định nghĩa 09.10). | **Nhắc lại** $\ln t\le t-1$ (4-03) một dòng trên 5-03; một dòng "Kỹ thuật." thêm bớt $\ln q(v)$ rồi lấy kì vọng theo $q$ (chỉ dùng ở đây). | Ví dụ 09.9 ($-2{,}2655$; $N(1,\tfrac12)$); Ví dụ 09.10 (bảng, $1{,}1534$; hình F2); Bài tập 09.4(b) ($-1{,}4238$; $0{,}1201$; $0{,}0882$); câu hỏi tự kiểm tra 3 ($0{,}0400$). | 5-02, 5-03, 5-04, 5-06 |
| **Hệ quả 09.13** (thuật toán EM không làm giảm log độ hợp lý; chứng minh đầy đủ, Phụ lục D) | tất định, trên tập huấn luyện cố định; không chứa $L_D$, không nói về cực tiểu toàn cục | Mỗi vòng kẹp tổng log độ hợp lý giữa hai giá trị của ELBO: bước E đặt khe bằng $0$, bước M nâng ELBO. | Dãy ba quan hệ trên mặt trang 5-05 ("Chứng minh."): Định lý 09.12(b) tại $\theta_{t+1}$; bước M, vì $\mathrm H(q_i)$ không phụ thuộc $\theta$; Định lý 09.12(b) với dấu bằng tại $\theta_t$. Bước 1 của Phụ lục D (giả thiết của định lý thỏa tại $\theta_{t+1}$ nhờ giá trị lớn nhất hữu hạn) ở ghi chú diễn giả. | Không có kỹ thuật mới (kẹp giữa hai cận). | Bài tập 09.10 (bước M cho trọng số hỗn hợp; bài về nhà). | 5-05 |
| **Mệnh đề 09.15** (gradient theo đường đi không chệch; phác thảo, chi tiết ở Phụ lục B) | kì vọng theo nhiễu phụ $\zeta$, tất định theo $\phi$ | Sau tái tham số hóa, $\phi$ chỉ nằm trong hàm, không nằm trong phân bố lấy kì vọng; đạo hàm vào trong kì vọng khi mỗi đường nhiễu khả vi và các thương sai phân bị chặn chung bởi một hàm khả tích. Cực biên: hàm nhảy theo $\phi$ có đạo hàm $0$ trên từng đường trong khi gradient thật khác $0$. | Bốn bước: định lý giá trị trung bình trên đoạn $[\phi_0,\phi_0+\Delta e]$ với $\zeta\notin N_0$ (dùng (i)); thương sai phân $\le M(\zeta)$ (dùng (ii)); thương sai phân của $F$ bằng kì vọng thương sai phân của $\kappa$, định lý hội tụ bị chặn khi $\Delta\to0$ (dùng (iii)); hội tụ bị chặn lần nữa cho đạo hàm riêng liên tục, nên $F$ khả vi. Tập ngoại lệ phụ thuộc $\phi$: hợp theo $\phi$ có xác suất dương (Ví dụ 09.12). | **Trang "Kỹ thuật." riêng 6-04** "Đổi chỗ đạo hàm và kì vọng": Bài 10 dùng lại (Nhận xét 10.5, chứng minh ở Phụ lục A của Bài 10: "Như chứng minh Mệnh đề 09.15 ở Phụ lục B của Bài 09", định lý giá trị trung bình, hội tụ bị chặn; sửa theo T6 của cổng duyệt). | Ví dụ 09.11 ($2$; $-1$; phương sai $1$, $6$, $29{,}027$); Ví dụ 09.12 ($0{,}3521$; $2{,}333$); Bài tập 09.7(c), (d) ($G=2\sqrt3$; $0{,}0715$). | 6-02, 6-03, 6-04, 6-05, 6-06, 6-08 |

**Kết quả phụ và quyết định.**
- Định nghĩa 09.1: trang 2-02, mở bằng hai xác suất có điều kiện của câu hỏi mở đầu và Ví dụ 09.1 ($0{,}58$); không có trang ví dụ riêng.
- §2 (ba điểm khác của hàm lỗi log, giả thiết): trang 2-03.
- Định nghĩa 09.2 và câu "điều kiện tổng bằng $1$ là cần thiết": trang 2-04.
- Định nghĩa 09.4: trang 3-03 cùng Ví dụ 09.3; Bước 5 (chuẩn hóa) ở ghi chú diễn giả 3-02.
- Nhận xét 09.5: dòng đầu 3-09, nơi Định nghĩa 09.6 dùng kí tự kết thúc (mục 11, điểm 4).
- Đoạn §6 "quan sát độc lập ở cấp chuỗi" (Mệnh đề 01.7, Định lý 02.7): trang 3-06.
- Định nghĩa 09.6 và Ví dụ 09.6: trang 3-09; câu "kì vọng của $\ell_{\mathrm{len}}$ nhỏ nhất tại phân bố tỉ lệ với $p_D(x)/n(x)$" chỉ ở ghi chú diễn giả, vì đó là kết quả của Bài tập 09.5(c), bài về nhà.
- Định nghĩa 09.7 và hai đoạn sau (KL xác định trong $(-\infty,\infty]$, KL hai Gauss, entropy vi phân âm): trang 4-01; công thức KL hai Gauss lên mặt trang ở 5-04, nơi dùng ("công thức sau Định nghĩa 09.7").
- "**Câu hỏi.** Một mô hình có rủi ro thực nghiệm nhỏ hơn $\mathrm H(p_D)$ …" và bốn số: trang 4-05.
- Định nghĩa 09.10: trang 5-01; Định nghĩa 09.11: dòng đầu 5-02; Định nghĩa 09.14: trang 6-01.
- Đoạn §9 về gradient ngẫu nhiên của $-\frac1m\sum_i\operatorname{ELBO}$ với $\xi=(i,\zeta)$ và (C): ghi chú diễn giả 6-03 và trang bài tập 6-08.
- Câu ôn nhanh 1–3: ghi chú diễn giả 1-02 (câu 1, 2) và 5-01 (câu 3).
- §10: trang 7-02 và ghi chú diễn giả 7-01.
- §12 (câu hỏi cuối buổi (a)–(d)): câu hỏi tự kiểm tra 1–3 ở 7-04 dùng (a), (b), (c); (d) trùng Ví dụ 09.12 Bước 4, ở ghi chú diễn giả 6-06.
- Phụ lục C: ghi chú diễn giả 3-08 (cửa sổ chồng lấn), 4-07 (dữ liệu bigram, mười hạt giống), 7-03 (độ lệch chuẩn qua hạt giống).

## 5. Ví dụ bổ trợ

Ví dụ xuyên suốt: **mô hình hai kí tự sinh chuỗi độ dài ba** (câu hỏi mở đầu, Ví dụ 09.1, 09.3, Nhận xét 09.5, câu hỏi cuối buổi (a)) và **mô hình Gauss tuyến tính một chiều tại $x=2$** (Ví dụ 09.9, 09.10, 09.11, Bài tập 09.7, câu hỏi cuối buổi (c)); thêm **chuỗi DNA độ dài $200$** (ứng dụng §3, Ví dụ 09.4, 09.8, 09.13 Bước 4, Bài tập 09.6). Mỗi lần dùng lại trả lời một câu hỏi mới. Hai kí tự: hàm lỗi log là tổng (1-06); kí tự phụ thuộc nhau (2-02); độ bối rối (3-03); tổng $3$ khi độ dài thay đổi (3-09); chuỗi $\mathtt{BBA}$ (7-04). Gauss: bằng chứng và hậu nghiệm dạng đóng (5-01); khe bằng KL tới hậu nghiệm (5-04, hình F2); gradient theo đường đi (6-05); SGD với gradient đó (6-08). DNA: câu hỏi thực hành (ghi chú diễn giả 2-01); cỡ mẫu là số chuỗi (3-06, 3-07); MLE, làm trơn, quá khớp (4-07); mô hình ghi nhớ (6-07); bài tập tổng hợp (7-03).

Mọi con số dưới đây đã tính lại bằng Python (thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-09/storyboard/num.py`) và khớp ghi chú, tệp bài tập. Số của thí nghiệm (Ví dụ 09.5, 09.8, Bài tập 09.6) lấy nguyên từ ghi chú và tệp bài tập, không chạy lại. **Không có ví dụ mới mang số mới trên mặt trang.** Hai hình dùng số của ghi chú: F1 là sơ đồ hai cửa sổ của Ví dụ 09.5 (không có số đo); F2 vẽ ELBO của Ví dụ 09.10 theo $\mu$ với $\sigma^2=1$ và $\sigma^2=\tfrac12$, đi qua bốn dòng của bảng ghi chú (cách dựng ở mục 8).

**V1. Câu hỏi mở đầu** (1-06). $-\ln0{,}8=0{,}2231$. $\tfrac35\cdot\tfrac7{10}\cdot\tfrac25=\tfrac{21}{125}=0{,}168$; $-\ln0{,}168=1{,}78379$; $-\ln\tfrac35=0{,}51083$, $-\ln\tfrac7{10}=0{,}35667$, $-\ln\tfrac25=0{,}91629$; tổng $1{,}78379$.

**V2. Ví dụ 09.1** (2-02). $\Pr(x_2=\mathtt B)=\tfrac35\cdot\tfrac7{10}+\tfrac25\cdot\tfrac25=0{,}42+0{,}16=0{,}58$; $\Pr(x_2=\mathtt A)=0{,}42$. $\Pr(x_3=\mathtt B\mid x_2=\mathtt A)=0{,}7\ne0{,}4=\Pr(x_3=\mathtt B\mid x_2=\mathtt B)$.

**V3. §2, mật độ** (2-03). $N(0;\,0{,}01)$ tại $0$: $\ell=\ln(0{,}1\sqrt{2\pi})=-1{,}38365$.

**V4. Ví dụ 09.2** (2-05). $L_s(\theta)=-0{,}7\ln\theta-0{,}3\ln(1-\theta)$: $0{,}6931$; $0{,}6325$; $0{,}6109$; $0{,}6390$ tại $0{,}5$; $0{,}6$; $0{,}7$; $0{,}8$. $L_s'=0$ tại $\theta=0{,}7$; $\hat\theta=m_1/m$. $m_1=0$: $\hat\theta=0$, $\ell(\hat\theta,1)=+\infty$.

**V5. Bài tập 09.8(c)** (2-06; số của `exercises.md`). $\ell=\tfrac12\ln(2\pi\sigma^2)+(x-\mu)^2/(2\sigma^2)$; $m=1$, $\mu=x^{(1)}$: $L_s=\tfrac12\ln(2\pi\sigma^2)\to-\infty$ khi $\sigma^2\to0$.

**V6. Ví dụ 09.3** (3-03). $\ell=1{,}78379$; $/3=0{,}59460$; $e^{0{,}5946}=0{,}168^{-1/3}=1{,}81230<2$. Chuẩn hóa (Bước 5): tổng theo $x_3$, $x_2$, $x_1$ mỗi lần bằng $1$; tám chuỗi có tổng $1$. Nhận xét 09.5: $1+1+1=3$; với xác suất kết thúc $\tfrac12$ sau mỗi kí tự, độ dài $n$ có xác suất $(\tfrac12)^n$, tổng $1$.

**V7. Bài tập 09.1(a), (c)** (3-04; số của `exercises.md`). $\mathtt{ABBC}$: $0{,}5\cdot0{,}5\cdot0{,}4\cdot0{,}2=0{,}02$; $\ell=\ln50=3{,}91202$; $/4=0{,}97801$; $50^{1/4}=2{,}65915$. $\mathtt{CCCC}$: $0{,}25\cdot0{,}8^3=0{,}128$; $\ell=\ln4+3\ln1{,}25=2{,}0557$; $0{,}5139$; $1{,}6719$. (c) $0{,}2\cdot0{,}3+0{,}5\cdot0{,}2+0{,}3\cdot0{,}8=0{,}40$; $0{,}1\cdot0{,}3+0{,}1\cdot0{,}2+0{,}8\cdot0{,}8=0{,}69$.

**V8. Ví dụ 09.4** (3-06, 3-07). $\ln20=2{,}99573$; $b=200\ln20=599{,}146$; $\sqrt{\ln40/100}=0{,}192065$; $b\cdot0{,}192065=115{,}075\le115{,}08$; $/200=0{,}575374\le0{,}5754$. Phép đếm sai: $\ln20\sqrt{\ln40/(2\cdot10^4)}=0{,}040685\approx0{,}0407$. Cỡ mẫu: $(\ln20)^2\ln40/(2\cdot0{,}05^2)=6621{,}10$, nên $6622$ chuỗi.

**V9. Ví dụ 09.5** (3-08; số của ghi chú). $4990$ cửa sổ, $998=20\%$; $0{,}8\cdot0+0{,}2\cdot1=0{,}2$; đo được $0{,}200$ ($0{,}137$ đến $0{,}245$); chia theo thời gian $0{,}994$ ($0{,}915$ đến $1{,}066$); $1-0{,}2^{10}=1-1{,}024\cdot10^{-7}$.

**V10. Ví dụ 09.6** (3-09). Hàm lỗi tổng: $-\ln\theta-5\ln(1-\theta)$, đạo hàm $0$ tại $\theta=\tfrac16=\tfrac2{12}$. Chuẩn hóa: $-\tfrac12\ln\theta-\tfrac12\ln(1-\theta)$, $\theta=\tfrac12$. Trọng số: $\tfrac12$ (tổng); $\tfrac14$ và $\tfrac1{20}$ (chuẩn hóa).

**V11. Định nghĩa 09.7, đoạn sau** (4-01). $\mathrm{KL}(\mathrm{Ber}(0{,}6)\Vert\mathrm{Ber}(0{,}7))=0{,}022582$; chiều ngược $0{,}021601$. Đều trên $[0,\tfrac12]$: $\mathrm h=-\ln2=-0{,}6931$.

**V12. Câu hỏi sau Hệ quả 09.9** (4-05). $\mathrm H(\mathrm{Ber}(0{,}6))=0{,}673012$; $L_D(0{,}7)=0{,}673012+0{,}022582=0{,}695594$; $L_s(0{,}7)=0{,}610864$; hiệu $0{,}084730$.

**V13. Ví dụ 09.7** (4-06). Bước 1: $L_D(\theta)=1{,}2040$; $3{,}4544$; $6{,}9078$ tại $10^{-1}$; $10^{-3}$; $10^{-6}$. Bước 2: $\ln2{,}5=0{,}9163$, $\ln1{,}25=0{,}2231$. Bước 3: $0{,}99^m=0{,}9044$; $0{,}6050$; $0{,}3660$ tại $m=10$; $50$; $100$; $0{,}99^{68}=0{,}5049$, $0{,}99^{69}=0{,}4998$. Bước 4: $1/52=0{,}019231$; $\ln52=3{,}95124<3{,}952$; $L_D=-0{,}99\ln\tfrac{51}{52}-0{,}01\ln\tfrac1{52}=0{,}058736\approx0{,}0587$; $\mathrm H(\mathrm{Ber}(0{,}01))=0{,}056002\approx0{,}0560$.

**V14. Ví dụ 09.8** (4-07). Entropy mỗi hàng $-(0{,}6\ln0{,}6+0{,}2\ln0{,}2+2\cdot0{,}1\ln0{,}1)=1{,}088900$; $\ln4+199\cdot1{,}0889=218{,}077$; $/200=1{,}090387\approx1{,}0904$; $e^{1{,}0904}=2{,}9754$. Bảng và số $+\infty$ ($10/10$, $5/10$), lỗi huấn luyện $1{,}070$; $1{,}080$; $1{,}090$; $1{,}090$ lấy từ ghi chú.

**V15. Bài tập 09.3(b), (c)** (4-08; số của `exercises.md`). $\mathrm H(p_D)=\tfrac32\ln2=1{,}03972$; $\ln3=1{,}09861$; $\mathrm{KL}(p_D\Vert p_\theta)=0{,}05889$; $1{,}0397+0{,}0589=1{,}0986$; $\mathrm{KL}(p_\theta\Vert p_D)=0{,}05663\approx0{,}0566$. (c) $L_D=\mathrm{KL}=+\infty$; $\mathrm{KL}(p_\theta\Vert p_D)=\tfrac12\ln2=0{,}34657$.

**V16. Ví dụ 09.9** (5-01). $\ln p_\theta(2)=-\tfrac12\ln(4\pi)-1=-2{,}265512$; hậu nghiệm $N(1,\tfrac12)$. Câu ôn nhanh 3 (ghi chú diễn giả): $\Pr(x)=\tfrac12\cdot0{,}2+\tfrac12\cdot0{,}6=0{,}4$; $\Pr(v=2\mid x)=0{,}3/0{,}4=0{,}75$.

**V17. Ví dụ 09.10** (5-04; hình F2). Tái tạo $-\tfrac12\ln(2\pi)-\tfrac12((2-\mu)^2+\sigma^2)$, $-\tfrac12\ln(2\pi)=-0{,}918939$; KL tới tiên nghiệm $\tfrac12(\mu^2+\sigma^2-1-\ln\sigma^2)$. Bốn dòng ($\mu;\sigma^2$ → tái tạo; KL; ELBO; khe): $0;1$ → $-3{,}4189$; $0$; $-3{,}4189$; $1{,}1534$. $1;1$ → $-1{,}9189$; $0{,}5$; $-2{,}4189$; $0{,}1534$. $0{,}8;0{,}5$ → $-1{,}8889$; $0{,}4166$; $-2{,}3055$; $0{,}0400$. $1;0{,}5$ → $-1{,}6689$; $0{,}5966$; $-2{,}2655$; $0$. Kiểm khe dòng đầu: $\ln\sqrt{0{,}5}+\tfrac{1+1}{2\cdot0{,}5}-\tfrac12=1{,}153426$. Cực đại: $\partial_\mu=2-2\mu=0$ tại $\mu=1$, $\partial_\sigma=-2\sigma+1/\sigma=0$ tại $\sigma^2=\tfrac12$.

**V18. Bài tập 09.4(b)** (5-06; số của `exercises.md`). $\rho_0(1{,}5)=0{,}129518$, $\rho_0(0{,}5)=0{,}352065$; $p_\theta(0{,}5)=0{,}240791\approx0{,}2408$; $\ln=-1{,}423824\approx-1{,}4238$; $\Pr(v=2\mid x)=1/(1+e^{-1})=0{,}731059$. $q(2)=0{,}5$: ELBO $-1{,}543939$, khe $0{,}120115\approx0{,}1201$. $q(2)=0{,}9$: ELBO $-1{,}512003$, khe $0{,}088179\approx0{,}0882$; KL tới hậu nghiệm $0{,}088179$; tái tạo $-1{,}143939$; KL tới tiên nghiệm $0{,}368064$; hiệu $-1{,}512003$.

**V19. Ví dụ 09.11** (6-05). Tại $(0,1)$: gradient đúng $(2,-1)$; ước lượng $(2-\zeta,\ 2\zeta-\zeta^2)$; $\zeta=0{,}5$: $(1{,}5;\,0{,}75)$; $\zeta=-1$: $(3;\,-3)$. Phương sai $1$; $4+2-0=6$. Ước lượng gradient log: với $a=\tfrac12\ln(2\pi)$, $(a+2)(a+5)+11{,}75=29{,}0270$.

**V20. Ví dụ 09.12** (6-06). $F'(0{,}5)=e^{-1/8}/\sqrt{2\pi}=0{,}352065\approx0{,}3521$; Bernoulli: phương sai $1/\phi-1=2{,}3333$ tại $\phi=0{,}3$.

**V21. Ví dụ 09.13** (6-07). $\ln100=4{,}60517$; $\tfrac12\ln(2\pi e)=1{,}418939$; $1{,}418939+4{,}60517/784=1{,}424813\le1{,}4249$; $\tfrac12\ln(50\pi)+\tfrac1{50}=2{,}548376\approx2{,}5484$; $50\cdot\tfrac14\cdot0{,}6^{199}=8{,}892\cdot10^{-44}\approx8{,}9\cdot10^{-44}$; $4{,}60517/784=0{,}005874\le0{,}0059$.

**V22. Bài tập 09.7(c), (d)** (6-08; số của `exercises.md`). $\mathbb E\lVert\varphi\rVert^2=(5\mu^2-12\mu+8)+(7\sigma^2+1/\sigma^2-4)$: $12$ tại $(0,1)$; $8$ tại $(2,1)$; $9{,}75$ tại $(0,\tfrac12)$; $5{,}75$ tại $(2,\tfrac12)$; lớn nhất $12$, $G=\sqrt{12}=3{,}46410$. $R=\sqrt{4{,}25}=2{,}06155$; $\eta=R/(G\cdot100)=0{,}005951$; $RG/100=\sqrt{51}/100=0{,}071414\le0{,}0715$. Kiểm tra: $1+6+\lVert(-2,1)\rVert^2=12$.

**V23. Bài tập 09.6(b)** (7-03; số của `exercises.md`). $\ln(1/0{,}087)=2{,}441847$; $\sqrt{\ln40/400}=0{,}096032$; tích $0{,}234496\le0{,}2345$; $0{,}2345/0{,}0041=57{,}2$. Hiệu với mô hình thật $0{,}0316$ ($m=1$) xuống $0{,}00008$ ($m=500$).

**V24. Câu hỏi cuối buổi §12** (7-04). (a) $\mathtt{BBA}$: $\tfrac25\cdot\tfrac25\cdot\tfrac35=0{,}096$; $-\ln0{,}096=2{,}34341$; $/3=0{,}78114$; $e^{0{,}7811}=2{,}18395\approx2{,}184$. (c) $-2{,}2655+2{,}3055=0{,}0400$.

**V25. Câu ôn nhanh** (ghi chú diễn giả 1-02). (1) $\sqrt{\ln40/100}=0{,}192065\le0{,}1921$; Ví dụ 02.6 bỏ tính độc lập. (2) $g(t)=t-1-\ln t$, $g'=1-1/t$, cực tiểu duy nhất $g(1)=0$.

## 6. Danh sách trang

Mỗi mục: ID, tiêu đề, loại, thời lượng; **Mặt trang** (các dòng dự kiến, theo thứ tự; `[f]` là fragment; `$$…$$` là công thức hiển thị, tính một dòng; `Bảng:` là một bảng HTML, ô ngăn bằng `|`, hàng ngăn bằng `;`; `{{…}}` là chỉ dẫn bố cục, không lên mặt trang); **Ghi chú diễn giả** (ý chính, 40–150 âm tiết, đến ~250 cho trang ý tưởng chứng minh và trang bài tập; viết cho giảng viên và người học; không mã trang, mã ví dụ của storyboard, câu quy trình hay nguồn gốc; luôn kết thúc bằng dòng `note-source`); **Lý do / nối**; **Mục tiêu / nguồn**. Câu trên mặt trang là bản dự kiến đã tự kiểm theo `no-ai-slop` (chế độ Edit) và `eval.md`; người viết deck có thể rút gọn, không thêm khẳng định.

Quy ước chung cho người viết deck:
- Trang kết quả: "Giả thiết:" và "Bảo đảm:" (nhãn của ghi chú), trích số khối của ghi chú một lần; "(a)", "(b)", "(c)" của một kết quả viết thường, không in đậm.
- Trang tổng quan (bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm") viết bằng lời, không kí hiệu, không tiếng Anh. Lần đầu một thuật ngữ trên trang nội dung có tiếng Anh trong ngoặc (bảng mục 10).
- Mọi kí hiệu trên mặt trang đã có ở trang trước hoặc có dòng "Nhắc lại:"/"Kí hiệu:" (bảng đối chiếu mục 12 ghi chỗ đưa vào).
- Bước chứng minh trên trang "Ý tưởng chứng minh" là `<ol>`; giả thiết dùng ở bước ghi trong ngoặc đầu mục, như deck Bài 06 (`L06-4-04`); không nhãn in đậm "Bước k".
- Số thập phân dùng dấu phẩy KaTeX `0{,}5`; dãy số ngăn bằng `;\ `; số từ năm chữ số tách nhóm bằng `\,`. Kí tự viết `\mathtt{A}`.
- Mỗi trang ví dụ mở bằng dữ kiện, không câu dẫn. "Diễn giải:" chỉ dùng số có trên chính trang đó.
- Không `\text{}` chứa tiếng Việt trong KaTeX. Trong ghi chú diễn giả, không ghi câu nguồn gốc, mã "V7", "mục 5", không mở bằng "Trang này", "Mạch này", "Bài này", không lấy mạch làm chủ ngữ, không nhắc Bài 10 (trừ câu nối ở ghi chú diễn giả 7-06).
- Công thức một dòng khi vừa khung; chỉ ngắt bằng `aligned` khi tràn ở 390 px (đo trong trình duyệt). Ở chế độ đọc hẹp, công thức rộng cuộn ngang tại chỗ.
- "Tập huấn luyện", "tập kiểm tra" theo ghi chú (quyết định của tác giả 2026-11-13); "lôgarit"; "hàm chỉ báo"; "mật độ liên hợp"; "kí tự" cho token. Trên trang bài tập, giữ dữ kiện, câu hỏi và kết quả của `exercises.md`; khi câu chữ rút gọn, câu đầy đủ nằm ở ghi chú diễn giả (mục 11, điểm 6); giữ "mẫu" ở Bài tập 09.8 như tệp bài tập (trước 2026-11-16; nay "tập huấn luyện").
- Tiêu đề có công thức viết bằng KaTeX.

### Mạch 1. Mở đầu (6 trang, 9 phút)

#### `1-01` Học chuỗi và mô hình sinh — bìa, điểm vào mạch 1 · 1 phút
- **Mặt trang:**
  - Bài 09
  - Với hàm lỗi log, ước lượng hợp lý cực đại là tối thiểu hóa rủi ro thực nghiệm, ở mức tổng thể chọn mô hình gần phân bố thật nhất theo phân kì Kullback–Leibler, và khi các chuỗi được rút độc lập, cỡ mẫu là số chuỗi.
  - Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1
  - Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN
- **Ghi chú diễn giả:** Ở Bài 01–08, mỗi quan sát là một điểm $z$ và hàm lỗi logistic là hàm lỗi log của một mô hình xác suất cho nhãn. Bài 09 xét quan sát là cả một chuỗi có các kí tự phụ thuộc nhau, và hàm lỗi là $-\ln$ của xác suất mà mô hình gán cho cả chuỗi. Luận điểm gồm ba kết quả: ước lượng hợp lý cực đại là ERM với hàm lỗi log (Định nghĩa 09.2); rủi ro kì vọng bằng entropy cộng phân kì KL thuận (Mệnh đề 09.8, Hệ quả 09.9); trong Thiết lập A, cỡ mẫu là số chuỗi $m$. Hai bảo đảm tổng thể không cho cận cho cỡ mẫu hữu hạn; với một chuỗi thời gian chia thành cửa sổ chồng lấn, cần thêm giả thiết về sự phụ thuộc. Nguồn: ghi chú Bài 09, đoạn mở đầu, §10.
- **Lý do / nối:** luận điểm cả bài → tiên quyết.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu, §10.

#### `1-02` Tiên quyết và quy ước — mở đầu · 1,5 phút
- **Mặt trang:**
  - **Nhắc lại:** rủi ro kì vọng $L_D=\mathbb E_{z\sim D}\ell(\cdot,z)$, rủi ro thực nghiệm $L_S=\frac1m\sum_i\ell(\cdot,z_i)$, ERM làm nhỏ nhất $L_S$.
  - Hệ quả 02.10(b): (T1), hàm lỗi trong $[0,1]$, $h$ cố định: với xác suất ít nhất $1-\delta$,
  - $$\lvert L_S(h)-L_D(h)\rvert\le\sqrt{\ln(2/\delta)/(2m)}.$$
  - Nhận xét 02.11: với hàm lỗi không bị chặn, Định lý 02.7 không áp dụng.
- **Ghi chú diễn giả:** Hệ quả 02.10 cần dạng đầy đủ của (T1), một hàm lỗi bị chặn và một giả thuyết cố định, không phụ thuộc $S$. Với miền $[a,b]$, bán kính nhân thêm $b-a$ (đoạn sau Nhận xét 02.8). Câu ôn nhanh 1: với $\delta=0{,}05$ và $m=50$, bán kính là $\sqrt{\ln40/100}\le0{,}1921$; Ví dụ 02.6 chép một quan sát $m$ lần, giữ dạng yếu của (T1) nhưng bỏ tính độc lập, nên Hệ quả 02.10 không áp dụng. Câu ôn nhanh 2: $g(t)=t-1-\ln t$ có $g'(t)=1-1/t$, giảm nghiêm ngặt rồi tăng nghiêm ngặt, giá trị nhỏ nhất duy nhất $g(1)=0$, nên $\ln t\le t-1$, dấu bằng chỉ khi $t=1$. Nguồn: ghi chú Bài 09, Kiến thức tiên quyết, Câu hỏi ôn nhanh.
- **Lý do / nối:** các kết quả của Bài 01–02 dùng trên mặt trang được nhắc lại ở đây → mục tiêu.
- **Mục tiêu / nguồn:** 1–3; Kiến thức tiên quyết.

#### `1-03` Mục tiêu — mở đầu · 1 phút
- **Mặt trang (danh sách đánh số, bằng lời, không kí hiệu; trần 80):**
  1. Phân tích xác suất chuỗi theo xác suất có điều kiện; tính độ bối rối.
  2. Viết ước lượng hợp lý cực đại thành ERM; chứng minh rủi ro bằng entropy cộng phân kì.
  3. Phân biệt độc lập giữa các chuỗi với phụ thuộc trong chuỗi; chỉ ra rò rỉ.
  4. Chứng minh đồng nhất thức cận dưới bằng chứng; tách thành tái tạo và phân kì.
  5. Dẫn ra gradient theo đường đi; kiểm điều kiện không chệch, nêu trường hợp chệch.
- **Ghi chú diễn giả:** Mục tiêu 1 gồm cả độ hợp lý và hàm lỗi log trung bình theo kí tự, tính từ một bảng xác suất. Ở mục tiêu 2, "phân kì" là phân kì Kullback–Leibler, và rủi ro là rủi ro kì vọng với hàm lỗi log. Mục tiêu 3 gồm ba ý: tính độc lập giữa các chuỗi khác sự phụ thuộc giữa các kí tự trong một chuỗi; chia ngẫu nhiên các cửa sổ chồng lấn làm rò rỉ thông tin; hàm lỗi tổng và hàm lỗi chuẩn hóa theo độ dài cho hai điểm cực tiểu khác nhau. Mục tiêu 4 tách cận trên một mô hình Gauss. Ở mục tiêu 5, điều kiện không chệch là điều kiện cho phép đổi chỗ đạo hàm và kì vọng. Nguồn: ghi chú Bài 09, Mục tiêu học tập.
- **Lý do / nối:** tiêu chí kiểm tra → nội dung.
- **Mục tiêu / nguồn:** tất cả; Mục tiêu học tập.

#### `1-04` Nội dung — mở đầu · 0,5 phút
- **Mặt trang:**
  - `ol start="2"` với liên kết `#/2`…`#/7`: 2. Hàm lỗi log và ước lượng hợp lý cực đại; 3. Phân tích tự hồi quy và quan sát độc lập ở cấp chuỗi; 4. Entropy và phân kì Kullback–Leibler; 5. Mô hình biến ẩn và cận dưới bằng chứng; 6. Tái tham số hóa và so sánh các mô hình sinh; 7. Tổng kết.
  - Đọc trước: UML §24.1.
- **Ghi chú diễn giả:** Hàm lỗi log biến việc học một phân bố thành ERM. Với chuỗi, quy tắc nhân xác suất tách hàm lỗi theo từng kí tự, còn đơn vị độc lập là cả chuỗi. Entropy và phân kì Kullback–Leibler cho giá trị tốt nhất và phần vượt của rủi ro kì vọng. Khi có biến không quan sát được, ta tối ưu một cận dưới của log độ hợp lý, và tái tham số hóa cho gradient của cận đó. Nguồn: ghi chú Bài 09; §13.
- **Lý do / nối:** bản đồ mạch → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §13.

#### `1-05` Vấn đề trung tâm — mở đầu · 1 phút
- **Mặt trang:**
  - {{một hộp `div.box`}} **Câu hỏi:** học một phân bố xác suất và học một chuỗi như thế nào?
- **Ghi chú diễn giả** (câu trả lời cho cả bài, không trên mặt trang): Học một phân bố là ERM với hàm lỗi log, tức ước lượng hợp lý cực đại; ở mức tổng thể, giá trị tốt nhất là entropy của phân bố thật và phần vượt là phân kì KL thuận. Học một chuỗi dùng quy tắc nhân xác suất: hàm lỗi của chuỗi là tổng các hàm lỗi có điều kiện, nhưng quan sát độc lập là cả chuỗi, nên các cận dùng số chuỗi, và chỉ khi xác suất của mô hình bị chặn dưới. Với mô hình biến ẩn, ta tối ưu cận dưới bằng chứng; khe bằng phân kì KL tới hậu nghiệm, và gradient tái tham số hóa không chệch dưới các điều kiện khả vi, khả tích. Nguồn: ghi chú Bài 09, đoạn mở đầu, §10.
- **Lý do / nối:** một vấn đề cốt lõi → câu hỏi cụ thể.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu.

#### `1-06` Ví dụ: hàm lỗi log của một nhãn và của một chuỗi — ví dụ dẫn nhập (Câu hỏi mở đầu) · 4 phút
- **Mặt trang:**
  - Phân lớp: $-\ln0{,}8\approx0{,}223$ cho nhãn $1$ dự đoán với xác suất $0{,}8$.
  - Mô hình sinh (generative model) trên $\mathtt A$, $\mathtt B$: rút kí tự (token) đầu, rồi mỗi kí tự theo kí tự trước.
  - Bảng: Kí tự đứng trước | Rút $\mathtt A$ | Rút $\mathtt B$; (đầu chuỗi) | $3/5$ | $2/5$; $\mathtt A$ | $3/10$ | $7/10$; $\mathtt B$ | $3/5$ | $2/5$
  - $$\Pr(\mathtt{ABB})=\tfrac35\cdot\tfrac7{10}\cdot\tfrac25=0{,}168,\quad-\ln0{,}168\approx1{,}784=0{,}511+0{,}357+0{,}916$$
  - **Câu hỏi:** huấn luyện trên $m$ chuỗi ba kí tự có giống trên $3m$ quan sát độc lập không?
- **Ghi chú diễn giả:** Mỗi số hạng của tổng ứng với một lần dự đoán kí tự kế tiếp từ các kí tự đứng trước, tức một bài toán phân lớp với hàm lỗi log. Đẳng thức "$-\ln$ của xác suất của chuỗi bằng tổng các hàm lỗi log theo từng kí tự" đúng với mọi phân bố. Tuy nhiên, theo bảng, $\Pr(x_3=\mathtt B\mid x_2=\mathtt A)=0{,}7$ và $\Pr(x_3=\mathtt B\mid x_2=\mathtt B)=0{,}4$, mà $x_2$ là ngẫu nhiên, nên ba số hạng không độc lập. Quan sát độc lập là cả chuỗi. Rủi ro kì vọng cần làm nhỏ là kì vọng của $-\ln$ xác suất mà mô hình gán cho cả chuỗi; nó bằng một đại lượng chỉ phụ thuộc phân bố thật cộng một số không âm. Nguồn: ghi chú Bài 09, Câu hỏi mở đầu và hai đoạn sau.
- **Lý do / nối:** ví dụ dẫn nhập trước mọi định nghĩa; trọng tâm trực quan 1 và 2 → tiêu đề mạch 2.
- **Mục tiêu / nguồn:** 1, 3; Câu hỏi mở đầu.

### Mạch 2. Hàm lỗi log và ước lượng hợp lý cực đại (7 trang, 15,5 phút)

#### `2-00` 2. Hàm lỗi log và ước lượng hợp lý cực đại — tiêu đề mạch, điểm vào mạch 2 · 0,5 phút
- **Mặt trang:**
  - "2."; h2 "Hàm lỗi log và ước lượng hợp lý cực đại"
  - Chọn mô hình gán xác suất lớn nhất cho tập huấn luyện là tối thiểu hóa rủi ro thực nghiệm với hàm lỗi log.
  - Thiết lập A · Thiết lập B · tập kiểm tra · độ hợp lý · ước lượng hợp lý cực đại
- **Ghi chú diễn giả:** Câu hỏi mở đầu cho thấy hàm lỗi log đánh giá một phân bố trên một quan sát, cả khi quan sát là một nhãn lẫn khi nó là một chuỗi. Trước hết cần nói rõ quan sát độc lập là gì khi dữ liệu là chuỗi, và hàm lỗi log khác hàm lỗi của các bài trước ở đâu. Sau đó, ước lượng hợp lý cực đại được viết thành ERM của Bài 01 với hàm lỗi này. Nguồn: ghi chú Bài 09, §1–§4.
- **Lý do / nối:** mạch 1 → thiết lập.
- **Mục tiêu / nguồn:** 2, 3; §1–§4.

#### `2-01` Thiết lập bài toán — thiết lập (§1) · 2,5 phút
- **Mặt trang:**
  - Quan sát (không nhãn): chuỗi $x_{1:n}=(x_1,\ldots,x_n)\in\mathcal A^n$, bảng chữ (alphabet) $\mathcal A$ hữu hạn.
  - Tập huấn luyện $S=(X^{(1)},\ldots,X^{(m)})\sim D^m$: $m$ chuỗi độc lập cùng phân bố, kể cả độ dài $n_i$.
  - Lớp mô hình $\{p_\theta:\theta\in\Theta\}$: hàm xác suất (hoặc mật độ) trên $\mathcal X$; hàm lỗi log $\ell(\theta,x)=-\ln p_\theta(x)$.
  - $$L_D(\theta)=\mathbb E_{X\sim D}\,\ell(\theta,X),\qquad L_S(\theta)=\tfrac1m\textstyle\sum_{i=1}^m\ell(\theta,X^{(i)})$$
  - Đối tượng so sánh $\inf_{\theta\in\Theta}L_D(\theta)$; cỡ mẫu là số chuỗi $m$.
- **Ghi chú diễn giả:** Bài toán có bảy thành phần; khác Bài 01–08, quan sát không có nhãn, $\mathcal Z=\mathcal X$, và mô hình trả về một phân bố thay cho một nhãn. Tổng số kí tự $\sum_in_i$ không thay được $m$ trong các cận. Tập quan sát là $\mathcal A^n$ khi độ dài cố định, hoặc tập mọi chuỗi hữu hạn; cả hai đều đếm được. Với chuỗi độ dài cố định $n$, ta báo cáo thêm rủi ro theo kí tự $\tfrac1nL_D(\theta)$. Ví dụ thực hành: chuỗi DNA độ dài $200$ trên $\{\mathtt A,\mathtt C,\mathtt G,\mathtt T\}$, $m$ từ $1$ đến $500$ chuỗi rút độc lập, lớp mô hình bigram có $3+12=15$ tham số tự do. Ba câu hỏi: với $m=50$, hàm lỗi log theo kí tự trên chuỗi mới cách giá trị tốt nhất bao xa; vì sao với $m$ nhỏ, ước lượng hợp lý cực đại cho hàm lỗi $+\infty$; khoảng tin cậy dùng cỡ mẫu nào. Nguồn: ghi chú Bài 09, §1; §3, khối ứng dụng.
- **Lý do / nối:** đặt quan sát, hàm lỗi, rủi ro trước định nghĩa → hai thiết lập lấy mẫu.
- **Mục tiêu / nguồn:** 2, 3; §1.

#### `2-02` Hai thiết lập lấy mẫu cho dữ liệu chuỗi — định nghĩa (Định nghĩa 09.1), ví dụ (Ví dụ 09.1) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 09.1.** $\Pr(x_3=\mathtt B\mid x_2=\mathtt A)=0{,}7\ne0{,}4=\Pr(x_3=\mathtt B\mid x_2=\mathtt B)$: kí tự trong chuỗi phụ thuộc nhau.
  - **Định nghĩa 09.1.** Thiết lập A (các chuỗi độc lập): quan sát là cả chuỗi, $S\sim D^m$.
  - Thiết lập B (chuỗi thời gian, time series): $x_1,\ldots,x_n$; cửa sổ $u_j=\big((x_{j-k},\ldots,x_{j-1}),x_j\big)$, độ dài ngữ cảnh (context length) $k$.
  - Với B, (T1) không áp dụng; cần giả thiết về sự phụ thuộc.
- **Ghi chú diễn giả:** Bảng có ba tham số tự do: $\tfrac35$, $\tfrac7{10}$, $\tfrac25$. Theo công thức xác suất toàn phần, $\Pr(x_2=\mathtt B)=\tfrac35\cdot\tfrac7{10}+\tfrac25\cdot\tfrac25=0{,}58$. Hai xác suất có điều kiện của $x_3$ khác nhau, nên $x_2$ và $x_3$ không độc lập; mỗi kí tự là một phần của một quan sát. Các chuỗi ba kí tự của câu hỏi mở đầu, rút độc lập, thuộc Thiết lập A. Phản ví dụ là các cửa sổ chồng lấn của một chuỗi đo hằng ngày, coi như các quan sát độc lập: chúng thuộc Thiết lập B và nói chung phụ thuộc nhau, vì hai cửa sổ liền nhau chung $k-1$ giá trị. Trong Thiết lập A, các cận của Bài 02–08 áp dụng với $m$ chuỗi khi hàm lỗi thỏa giả thiết của chúng. Câu trả lời cho câu hỏi mở đầu: $m$ chuỗi là $m$ quan sát độc lập, không phải $3m$. Nguồn: ghi chú Bài 09, §1, Định nghĩa 09.1 và đoạn sau; §3, Ví dụ 09.1.
- **Lý do / nối:** trọng tâm trực quan 1; Ví dụ 09.1 mở trang trước định nghĩa (không mở khái niệm bằng định nghĩa) → hàm lỗi log và giả thiết.
- **Mục tiêu / nguồn:** 3; Định nghĩa 09.1, Ví dụ 09.1.

#### `2-03` Hàm lỗi log và giả thiết của bài — thiết lập (§2) · 2,5 phút
- **Mặt trang:**
  - Hàm xác suất: $\ell\in[0,\infty]$, bằng $+\infty$ khi $p_\theta(x)=0$.
  - Mật độ: $\ell$ có thể âm, trái (T2): $N(0;\,0{,}01)$ tại $0$ cho $\ell=\ln(0{,}1\sqrt{2\pi})\approx-1{,}3836$.
  - Không bị chặn: không thỏa (T3); cận Bài 02–04, 07 cần mọi xác suất của mô hình $\ge c>0$.
  - **Giả thiết:** (T1) với quan sát là cả chuỗi $X^{(i)}$, kể cả độ dài $n_i$.
  - (T7) tập kiểm tra (test set) $V=(V_1,\ldots,V_{m_v})\sim D^{m_v}$ độc lập với $S$; $\hat\theta=\hat\theta(S)$ không phụ thuộc $V$.
- **Ghi chú diễn giả:** Ba điểm khác của hàm lỗi log so với các bài trước: giá trị $+\infty$ nằm ngoài Định nghĩa 01.1 (giá trị trong $[0,\infty)$), giá trị âm với mật độ, và không bị chặn. Với mô hình rời rạc, hàm lỗi bị chặn khi mọi xác suất có điều kiện của mô hình không nhỏ hơn $c>0$, như Ví dụ 07.11, Bước 4 làm với hàm lỗi logistic; với mật độ, cần chặn cả trên lẫn dưới. Dạng yếu của (T1) chỉ đòi mỗi chuỗi có phân bố $D$. Các giả thiết còn lại của §2 (entropy hữu hạn, khả tích của cận dưới bằng chứng, bước M, đổi chỗ đạo hàm và kì vọng) được nêu tại kết quả dùng chúng. Không kết quả nào của bài giả sử tính lồi. Nguồn: ghi chú Bài 09, §2.
- **Lý do / nối:** trọng tâm trực quan 4 (hàm lỗi không bị chặn) đặt trước mọi cận → định nghĩa mô hình xác suất.
- **Mục tiêu / nguồn:** 2, 3; §2.

#### `2-04` Mô hình xác suất và ước lượng hợp lý cực đại — định nghĩa (Định nghĩa 09.2) · 2,5 phút
- **Mặt trang:**
  - Mô hình trả về một phân bố thay cho một nhãn.
  - **Định nghĩa 09.2.** $p_\theta(x)\ge0$, $\sum_{x\in\mathcal X}p_\theta(x)=1$; độ hợp lý (likelihood) tại tập huấn luyện $s=(x^{(1)},\ldots,x^{(m)})$ là $\prod_ip_\theta(x^{(i)})$; lôgarit: log độ hợp lý (log-likelihood).
  - Ước lượng hợp lý cực đại (maximum likelihood estimation, MLE): $\hat\theta$ làm lớn nhất độ hợp lý,
  - $$\hat\theta\in\arg\min_{\theta\in\Theta}L_s(\theta),\qquad L_s(\theta)=\tfrac1m\textstyle\sum_{i=1}^m-\ln p_\theta(x^{(i)})$$
  - tức ERM với hàm lỗi log.
- **Ghi chú diễn giả:** Tập huấn luyện $s$ viết thường là một tập cố định; $L_s$ là rủi ro thực nghiệm trên nó. Với mật độ trên $\mathbb R^p$, tổng thay bằng tích phân. Phân bố thật $p_D$ chưa biết và không nhất thiết thuộc lớp mô hình. Quy ước $-\ln0=+\infty$ cho hàm lỗi log giá trị trong $[0,\infty]$; hàm lỗi này còn gọi là đối của log độ hợp lý (negative log-likelihood). Hai cách mô tả $\hat\theta$ tương đương vì $t\mapsto-\frac1m\ln t$ giảm nghiêm ngặt. Điều kiện tổng bằng $1$ không bỏ được: thay $p_\theta$ bằng $a\,p_\theta$ với $a>1$ thì $L_s$ giảm $\ln a$ và tiến tới $-\infty$ khi $a\to\infty$. Nguồn: ghi chú Bài 09, §4, Định nghĩa 09.2 và ba đoạn sau.
- **Lý do / nối:** trọng tâm trực quan 3; định nghĩa mở bằng câu khẳng định → ví dụ Bernoulli.
- **Mục tiêu / nguồn:** 2; Định nghĩa 09.2.

#### `2-05` Ví dụ: ước lượng hợp lý cực đại cho phân bố Bernoulli — ví dụ (Ví dụ 09.2) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 09.2.** $\mathrm{Ber}(\theta)$: $p_\theta(1)=\theta$, $p_\theta(0)=1-\theta$, $\Theta=[0,1]$; $s=(1,1,1,1,1,1,1,0,0,0)$, $m=10$, $m_1=7$.
  - $$L_s(\theta)=-0{,}7\ln\theta-0{,}3\ln(1-\theta)$$
  - Bảng: $\theta$ | $0{,}5$ | $0{,}6$ | $0{,}7$ | $0{,}8$; $L_s(\theta)$ | $0{,}6931$ | $0{,}6325$ | $0{,}6109$ | $0{,}6390$
  - $L_s'(\theta)=-0{,}7/\theta+0{,}3/(1-\theta)=0$ tại $\theta=0{,}7$; tổng quát, $\hat\theta=m_1/m$.
  - $m_1=0$: $\hat\theta=0$, nên $\ell(\hat\theta,1)=+\infty$.
- **Ghi chú diễn giả:** Bảy quan sát bằng $1$ góp $-\ln\theta$, ba quan sát bằng $0$ góp $-\ln(1-\theta)$. Chẳng hạn $L_s(0{,}7)=0{,}7\cdot0{,}3567+0{,}3\cdot1{,}2040=0{,}6109$. Đạo hàm bậc hai dương trên $(0,1)$, nên $\theta=0{,}7$ là điểm cực tiểu duy nhất, bằng tần suất của số $1$. Dòng cuối là trường hợp biên: khi tập huấn luyện không có số $1$ nào, mô hình học được gán xác suất $0$ cho quan sát $1$, và hàm lỗi trên quan sát đó là $+\infty$. Nguồn: ghi chú Bài 09, §4, Ví dụ 09.2.
- **Lý do / nối:** ví dụ tính tay của định nghĩa; trường hợp biên chuẩn bị cho rủi ro vô hạn ở mạch 4 → bài tập.
- **Mục tiêu / nguồn:** 2; Ví dụ 09.2.

#### `2-06` (bỏ sau năm báo cáo duyệt, mục 17; nội dung vào ghi chú diễn giả 2-05) Bài tập: ước lượng hợp lý cực đại Gauss từ một quan sát — bài tập (Bài tập 09.8(c)), lời giải trên mặt trang · 2,5 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 09.8.** Họ mật độ $N(\mu,\sigma^2)$, $(\mu,\sigma^2)\in\mathbb R\times(0,\infty)$; $\ell=\tfrac12\ln(2\pi\sigma^2)+(x-\mu)^2/(2\sigma^2)$.
  - (c) Với $m=1$, chứng minh $\inf L_s=-\infty$, nên không có ước lượng hợp lý cực đại.
  - Nối với hàm lỗi log của mật độ (§2 của ghi chú).
  - [f] **Lời giải:** với $\mu=x^{(1)}$, $L_s=\tfrac12\ln(2\pi\sigma^2)\to-\infty$ khi $\sigma^2\to0$; không có điểm cực tiểu.
  - [f] Với mật độ, hàm lỗi log không bị chặn dưới.
- **Ghi chú diễn giả:** Câu cuối của đề: "Nối kết quả này với tính chất của hàm lỗi log cho mật độ ở §2 của ghi chú." Tập huấn luyện gồm $x^{(1)},\ldots,x^{(m)}$ độc lập cùng phân bố $N(\mu,\sigma^2)$, cả $\mu$ và $\sigma^2$ chưa biết. Bài tập ghép hai điểm của mạch: ước lượng hợp lý cực đại là ERM với hàm lỗi log, và với mật độ, hàm lỗi log có thể âm. Mật độ Gauss tại tâm bằng $1/\sqrt{2\pi\sigma^2}$, tăng không giới hạn khi $\sigma^2\to0$, nên hàm lỗi log giảm không giới hạn. Khi mọi quan sát bằng nhau, lập luận không đổi. Phần (a), (b) của bài (ước lượng $\bar x$ và $\tfrac1m\sum_i(x^{(i)}-\bar x)^2$, độ chệch $\tfrac{m-1}m\sigma^2$) để về nhà. Nguồn: tệp bài tập, Bài tập 09.8 và lời giải.
- **Lý do / nối:** bài tập của mạch 2 từ `exercises.md`, lời giải trên mặt trang; câu nối sang mạch 3 ở tiêu đề mạch (hàm lỗi của chuỗi) → tiêu đề mạch 3.
- **Mục tiêu / nguồn:** 2; Bài tập 09.8(c).

### Mạch 3. Phân tích tự hồi quy và quan sát độc lập ở cấp chuỗi (10 trang, 22,5 phút)

#### `3-00` 3. Phân tích tự hồi quy và quan sát độc lập ở cấp chuỗi — tiêu đề mạch, điểm vào mạch 3 · 0,5 phút
- **Mặt trang:**
  - "3."; h2 "Phân tích tự hồi quy và quan sát độc lập ở cấp chuỗi"
  - Hàm lỗi log của một chuỗi là tổng các hàm lỗi theo từng kí tự, nhưng quan sát độc lập vẫn là cả chuỗi.
  - phân tích tự hồi quy · độ bối rối · cấp chuỗi · rò rỉ thông tin · hàm lỗi chuẩn hóa theo độ dài
- **Ghi chú diễn giả:** Mạch trước cho ERM với hàm lỗi log, trong đó mỗi quan sát là cả chuỗi. Một bảng liệt kê xác suất của từng chuỗi có quá nhiều tham số; quy tắc nhân xác suất thay nó bằng các xác suất có điều kiện của kí tự kế tiếp. Hàm lỗi khi đó là một tổng theo vị trí, nhưng các số hạng phụ thuộc nhau, nên mọi cận tập trung vẫn đếm số chuỗi. Với một chuỗi thời gian cắt thành cửa sổ chồng lấn, cách chia tập kiểm tra quyết định lỗi kiểm tra có ước lượng được rủi ro hay không. Nguồn: ghi chú Bài 09, §5–§6.
- **Lý do / nối:** mạch 2 → quy tắc nhân xác suất.
- **Mục tiêu / nguồn:** 1, 3; §5–§6.

#### `3-01` Quy tắc nhân xác suất cho chuỗi — trực quan, kết quả (Mệnh đề 09.3) · 3 phút
- **Mặt trang:**
  - Bảng cho từng chuỗi: $\lvert\mathcal A\rvert^n-1$ tham số ($4^{200}-1$ với DNA).
  - **Kí hiệu:** $x_{<j}=x_{1:j-1}$; $p_1(x_j\mid x_{<j})=p_1(x_{1:j})/p_1(x_{<j})$.
  - **Trực quan.** Mỗi thừa số: phân lớp kí tự kế tiếp.
  - **Mệnh đề 09.3.** **Giả thiết:** $n\ge1$ cố định; $p_1$ là một hàm xác suất trên $\mathcal A^n$.
  - **Bảo đảm:** tất định, với mọi $x_{1:n}$: (a) phân tích tự hồi quy (autoregressive factorization) $p_1(x_{1:n})=\prod_{j=1}^np_1(x_j\mid x_{<j})$; (b) $-\ln p_1(x_{1:n})=\sum_{j=1}^n-\ln p_1(x_j\mid x_{<j})$.
  - (c) Mọi họ $p_\theta(\cdot\mid x_{<j})$ trên $\mathcal A$ cho tích là hàm xác suất trên $\mathcal A^n$.
- **Ghi chú diễn giả:** Tiền tố $x_{<j}$ rỗng khi $j=1$, và xác suất có điều kiện xác định khi $p_1(x_{<j})>0$. Dòng "Trực quan." đọc mệnh đề theo câu hỏi mở đầu: $0{,}511$, $0{,}357$, $0{,}916$ là ba lần phân lớp kí tự kế tiếp với ngữ cảnh là tiền tố; ở (c), mỗi $p_\theta(\cdot\mid x_{<j})$ là một hàm xác suất bất kì. Phần (a), (b) đúng với mọi phân bố trên $\mathcal A^n$, kể cả $p_D$; giả thiết mô hình chỉ xuất hiện khi giới hạn độ dài ngữ cảnh hay chọn một kiến trúc. Khi một tiền tố có xác suất $0$, tích được quy ước bằng $0$. Theo (c), mọi mô hình định nghĩa bằng các xác suất có điều kiện là hàm xác suất, không cần chuẩn hóa thêm. Mệnh đề được chứng minh đầy đủ ở Phụ lục D. Nguồn: ghi chú Bài 09, §5, Mệnh đề 09.3 và đoạn sau.
- **Lý do / nối:** trọng tâm trực quan 2 (phân rã theo bước); vấn đề (số tham số) → trực quan → phát biểu trên cùng trang; ví dụ dẫn nhập ở 1-06 → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 1; Mệnh đề 09.3.

#### `3-02` Ý tưởng chứng minh: quy tắc nhân xác suất cho chuỗi — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  1. (định nghĩa xác suất có điều kiện) $p_1(x_{1:j})=p_1(x_{<j})\,p_1(x_j\mid x_{<j})$; nhân từ $j=1$ đến $n$, giản ước: (a).
  2. (tiền tố có xác suất $0$) $p_1(x_{1:n})\le p_1(x_{<j})=0$: hai vế bằng $0$.
  3. Lấy $-\ln$ hai vế, với $-\ln0=+\infty$: (b).
  4. (mỗi hàng có tổng $1$) Tổng theo kí tự cuối giảm tích đi một thừa số; quy nạp từ $j=n$: (c).
  - **Kỹ thuật.** Lấy tổng theo kí tự cuối: $\sum_{x_j\in\mathcal A}Q_j(x_{1:j})=Q_{j-1}(x_{<j})$, với $Q_j=\prod_{i\le j}p_\theta(x_i\mid x_{<i})$.
- **Ghi chú diễn giả** (~180 âm tiết): Bước 1 nhân $n$ đẳng thức của định nghĩa, các biên $p_1(x_{1:j})$ chung giản ước lần lượt, còn lại $p_1(x_{<1})=1$ và tích các xác suất có điều kiện. Bước 2 dùng tính đơn điệu của biên: biên của một tiền tố là tổng các số không âm, có chứa $p_1(x_{1:n})$. Bước 4 là chỗ duy nhất dùng giả thiết "mỗi hàng có tổng $1$": $\sum_{x_j}p_\theta(x_j\mid x_{<j})=1$ cho đẳng thức của dòng "Kỹ thuật.", rồi quy nạp cho tổng trên $\mathcal A^n$ bằng $1$ và biên của $Q_n$ trên $x_{1:j}$ bằng $Q_j$. Bỏ giả thiết này, một bảng có hàng $\mathtt A$ là $(0{,}5;\,0{,}7)$ không xác định một mô hình tự hồi quy. Với bảng của câu hỏi mở đầu, lấy tổng lần lượt theo $x_3$, $x_2$, $x_1$, mỗi lần được $1$, nên tám chuỗi trong $\{\mathtt A,\mathtt B\}^3$ có tổng xác suất $1$ (Ví dụ 09.3, Bước 5). Do đó huấn luyện một mô hình tự hồi quy là ERM với hàm lỗi log trên các chuỗi. Nguồn: ghi chú Bài 09, Phụ lục D, chứng minh Mệnh đề 09.3; Ví dụ 09.3, Bước 5.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; chỗ dùng giả thiết của (c) và phản ví dụ → định nghĩa mô hình tự hồi quy.
- **Mục tiêu / nguồn:** 1; Phụ lục D.

#### `3-03` Mô hình tự hồi quy và độ bối rối — định nghĩa (Định nghĩa 09.4), ví dụ (Ví dụ 09.3) · 3 phút
- **Mặt trang:**
  - **Định nghĩa 09.4.** Mô hình tự hồi quy: $p_\theta(x_{1:n})=\prod_jp_\theta(x_j\mid x_{<j})$.
  - Ngữ cảnh bậc $k$: chỉ phụ thuộc $k$ kí tự cuối; bậc $1$ là mô hình bigram (bigram model).
  - Độ bối rối (perplexity) $\exp\big(\tfrac1n\ell(\theta,x_{1:n})\big)$; $\tfrac1n\ell$: hàm lỗi log trung bình theo kí tự.
  - Học theo đáp án (teacher forcing): dùng tiền tố thật $x_{<j}$.
  - **Ví dụ 09.3.** $\mathtt{ABB}$: $\ell=1{,}7838$, theo kí tự $0{,}5946$, độ bối rối $0{,}168^{-1/3}\approx1{,}8123<2$.
- **Ghi chú diễn giả:** Theo Mệnh đề 09.3(c), mô hình tự hồi quy là một hàm xác suất. Thừa số thứ $j$ là độ hợp lý có điều kiện (conditional likelihood) của vị trí $j$; học theo đáp án không dùng tiền tố do mô hình sinh ra. Mô hình tự hồi quy dùng phân tích tự hồi quy của Mệnh đề 09.3(a) làm định nghĩa. Mô hình đều gán $1/\lvert\mathcal A\rvert$ cho mọi kí tự, nên có độ bối rối $\lvert\mathcal A\rvert$; độ bối rối là nghịch đảo của trung bình nhân các xác suất có điều kiện. Mô hình của câu hỏi mở đầu là một mô hình bigram. Ở vị trí $3$ của $\mathtt{ABB}$, học theo đáp án dùng tiền tố thật $\mathtt{AB}$, nhưng với ngữ cảnh bậc $1$ chỉ kí tự $\mathtt B$ ở vị trí $2$ được dùng: $p_\theta(\mathtt B\mid\mathtt{AB})=\tfrac25$. Nguồn: ghi chú Bài 09, §5, Định nghĩa 09.4, đoạn sau, Ví dụ 09.3.
- **Lý do / nối:** định nghĩa dựa trên (c) vừa chứng minh; ví dụ dùng lại chuỗi của 1-06 cho câu hỏi mới (độ bối rối) → bài tập.
- **Mục tiêu / nguồn:** 1; Định nghĩa 09.4, Ví dụ 09.3.

#### `3-04` Bài tập: độ hợp lý và độ bối rối từ một bảng — bài tập (Bài tập 09.1(a), (c)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 09.1.** Mô hình bigram trên $\{\mathtt A,\mathtt B,\mathtt C\}$:
  - Bảng: Trước | $\mathtt A$ | $\mathtt B$ | $\mathtt C$; (đầu chuỗi) | $0{,}5$ | $0{,}25$ | $0{,}25$; $\mathtt A$ | $0{,}2$ | $0{,}5$ | $0{,}3$; $\mathtt B$ | $0{,}4$ | $0{,}4$ | $0{,}2$; $\mathtt C$ | $0{,}1$ | $0{,}1$ | $0{,}8$
  - (a) $n=4$: độ hợp lý, hàm lỗi log, theo kí tự, độ bối rối của $\mathtt{ABBC}$, $\mathtt{CCCC}$.
  - (c) Tính $\Pr(x_3=\mathtt C\mid x_1=\mathtt A)$, $\Pr(x_3=\mathtt C\mid x_1=\mathtt C)$; $x_3$ có độc lập với $x_1$ không?
  - [f] **Lời giải:** Bảng: Chuỗi | Độ hợp lý | $\ell$ | Theo kí tự | Độ bối rối; $\mathtt{ABBC}$ | $0{,}02$ | $\ln50\approx3{,}9120$ | $0{,}9780$ | $2{,}6591$; $\mathtt{CCCC}$ | $0{,}128$ | $2{,}0557$ | $0{,}5139$ | $1{,}6719$
  - [f] (c) $0{,}2\cdot0{,}3+0{,}5\cdot0{,}2+0{,}3\cdot0{,}8=0{,}40\ne0{,}69$: không độc lập; $x_1$ tác động qua $x_2$.
- **Ghi chú diễn giả:** Câu (a) của đề: "Với độ dài cố định $n=4$, tính độ hợp lý, hàm lỗi log, hàm lỗi log trung bình theo kí tự và độ bối rối (perplexity) của hai chuỗi"; hàng "(đầu chuỗi)" là $\pi_0$, hàng $a$ là $\pi(a,\cdot)$, cột "Trước" là kí tự đứng trước. Bốn thừa số của $\mathtt{ABBC}$ là $\pi_0(\mathtt A)=0{,}5$, $\pi(\mathtt A,\mathtt B)=0{,}5$, $\pi(\mathtt B,\mathtt B)=0{,}4$, $\pi(\mathtt B,\mathtt C)=0{,}2$; hàm lỗi là $\ln2+\ln2+\ln2{,}5+\ln5=\ln50$. Với $\mathtt{CCCC}$: $0{,}25\cdot0{,}8^3=0{,}128$. Cả hai độ bối rối nhỏ hơn $3$ của mô hình đều trên ba kí tự. Ở (c), lấy tổng theo $x_2$: $\Pr(x_3=\mathtt C\mid x_1=\mathtt C)=0{,}1\cdot0{,}3+0{,}1\cdot0{,}2+0{,}8\cdot0{,}8=0{,}69$. Ngữ cảnh bậc $1$ chỉ nói rằng xác suất có điều kiện của $x_3$ khi biết $x_{<3}$ chỉ phụ thuộc $x_2$; kí tự $x_1$ vẫn ảnh hưởng tới $x_3$ qua phân bố của $x_2$. Phần (b) và (d) (kí tự kết thúc, phân bố hình học của độ dài) để về nhà. Nguồn: tệp bài tập, Bài tập 09.1 và lời giải.
- **Lý do / nối:** bài tập của cụm §5 từ `exercises.md`; (c) cho trọng tâm trực quan 1 trong một mô hình bigram; câu nối sang §6 ở trang sau (dòng đầu 3-06) → quan sát độc lập ở cấp chuỗi.
- **Mục tiêu / nguồn:** 1, 3; Bài tập 09.1(a), (c).

#### `3-05` Bài tập: độ hợp lý và độ bối rối từ một bảng, lời giải — lời giải Bài tập 09.1(a), (c) · (tách từ 3-04 khi viết deck)
- **Mặt trang:**
  - **Lời giải:** (a) theo bảng; (c) lấy tổng theo $x_2$.
  - Bảng: Chuỗi | Độ hợp lý | $\ell$ | Theo kí tự | Độ bối rối; $\mathtt{ABBC}$ | $0{,}5\cdot0{,}5\cdot0{,}4\cdot0{,}2=0{,}02$ | $\ln50\approx3{,}9120$ | $0{,}9780$ | $2{,}6591$; $\mathtt{CCCC}$ | $0{,}25\cdot0{,}8^3=0{,}128$ | $2{,}0557$ | $0{,}5139$ | $1{,}6719$
  - $$\Pr(x_3=\mathtt C\mid x_1=\mathtt A)=\ldots=0{,}40,\quad\Pr(x_3=\mathtt C\mid x_1=\mathtt C)=\ldots=0{,}69$$ (aligned, hai dòng)
  - $0{,}40\ne0{,}69$: $x_3$ không độc lập với $x_1$; $x_1$ tác động lên $x_3$ qua $x_2$.
- **Ghi chú diễn giả:** bốn thừa số và $\ln50$, $\ln4+3\ln1{,}25$; so với $3$ của mô hình đều; ngữ cảnh bậc $1$ và phụ thuộc qua $x_2$. Phần câu chữ đầy đủ của đề ở ghi chú diễn giả 3-04.
- **Lý do / nối:** hai bảng (đề và lời giải) không vừa một khung 16:9 (`footer_check.py`: 1021 px > 863 px ở mọi cách sắp xếp đã thử); tiền lệ `L08-7-04`/`L08-7-05` → quan sát độc lập ở cấp chuỗi.
- **Mục tiêu / nguồn:** 1, 3; Bài tập 09.1(a), (c), lời giải.

#### `3-06` Quan sát độc lập ở cấp chuỗi — trực quan, ví dụ (§6 đoạn mở; Ví dụ 09.4, Bước 1–2) · 2,5 phút
- **Mặt trang:**
  - Hàm lỗi của chuỗi: tổng $n$ số hạng phụ thuộc nhau; $L_S(\theta)$: trung bình $m$ biến độc lập.
  - Định lý 02.7 cần số hạng độc lập, bị chặn: dùng ở cấp chuỗi.
  - **Ví dụ 09.4.** DNA, $n=200$; bigram $p_\theta$ cố định, mọi xác suất $\ge c=0{,}05$; $m_v=50$ chuỗi kiểm tra; $\delta=0{,}05$.
  - $\ell\in[0,b]$, $b=200\ln20\approx599{,}15$; với xác suất ít nhất $1-\delta$ theo tập kiểm tra,
  - $$\lvert L_V(\theta)-L_D(\theta)\rvert\le b\sqrt{\ln(2/\delta)/(2m_v)}\le115{,}08,\qquad L_V(\theta)=\tfrac1{m_v}\textstyle\sum_{i=1}^{m_v}\ell(\theta,V_i)$$
- **Ghi chú diễn giả:** Mỗi số hạng $-\ln p_\theta(x_j\mid x_{<j})$ nằm trong $[0,\ln(1/c)]=[0,\ln20]$, $\ln20\approx2{,}9957$. Với $\theta$ cố định, không phụ thuộc $S$, Mệnh đề 01.7 cho $\mathbb E_SL_S(\theta)=L_D(\theta)$ khi $L_D(\theta)<\infty$, chỉ cần dạng yếu của (T1). Cận dùng Hệ quả 02.10(b) cho hàm lỗi $\ell/b\in[0,1]$ rồi nhân bán kính với $b$; mô hình cố định, không phụ thuộc tập kiểm tra, nên (T7) thỏa. Xác suất lấy theo tập kiểm tra. Nghĩa là: trong $100$ lần lấy tập kiểm tra $50$ chuỗi, có khoảng $95$ lần $\lvert L_V(\theta)-L_D(\theta)\rvert\le115{,}08$. Nguồn: ghi chú Bài 09, §6 đoạn mở, Ví dụ 09.4, Bước 1–2.
- **Lý do / nối:** câu nối từ §5 (hàm lỗi là tổng phụ thuộc) sang §6 trên mặt trang (dòng đầu); trọng tâm trực quan 1 → bán kính theo kí tự.
- **Mục tiêu / nguồn:** 3; §6, Ví dụ 09.4.

#### `3-07` Ví dụ: bán kính theo kí tự và phép đếm sai — ví dụ (Ví dụ 09.4, Bước 3–5), so sánh cận · 2,5 phút
- **Mặt trang:**
  - Theo kí tự: chia cho $n=200$; bán kính $\ln(1/c)\sqrt{\ln(2/\delta)/(2m_v)}$ nat, không giảm khi $n$ tăng.
  - Bảng: Đếm | Cỡ mẫu | Bán kính; chuỗi | $50$ | $0{,}5754$; chuỗi | $6622$ | $\le0{,}05$; kí tự, coi như độc lập | $10^4$ | $0{,}0407$
  - $0{,}0407$ dùng Định lý 02.7 cho kí tự phụ thuộc nhau: không được chứng minh.
  - Cần $c>0$: không có cận dưới cho xác suất, hàm lỗi không bị chặn.
- **Ghi chú diễn giả:** Nat là đơn vị của hàm lỗi log khi dùng lôgarit tự nhiên. Bán kính theo kí tự bằng $599{,}15\cdot0{,}19207/200\le0{,}5754$; độ dài $n$ xuất hiện ở cả $b$ và phép chia, nên triệt tiêu. Phép đếm sai coi $m_vn=10^4$ kí tự là $10^4$ quan sát độc lập với miền $[0,\ln20]$: $\ln20\sqrt{\ln40/(2\cdot10^4)}\approx0{,}0407$. Để bán kính theo kí tự không quá $0{,}05$, cần $m_v\ge(\ln20)^2\ln40/(2\cdot0{,}05^2)\approx6621{,}1$, tức ít nhất $6622$ chuỗi. Một cận dùng số kí tự cần thêm giả thiết về sự phụ thuộc giữa các kí tự. Khi các xác suất không bị chặn dưới, Nhận xét 02.11 áp dụng: không có cận Hoeffding. Nguồn: ghi chú Bài 09, §6, Ví dụ 09.4, Bước 3–5.
- **Lý do / nối:** bảng nhỏ so ba cách đếm trên cùng số liệu (bài học deck 04); trọng tâm trực quan 1 và 4 → Thiết lập B.
- **Mục tiêu / nguồn:** 3; Ví dụ 09.4.

#### `3-08` Ví dụ: rò rỉ thông tin khi chia ngẫu nhiên cửa sổ chồng lấn — ví dụ (Ví dụ 09.5), hình F1 · 3 phút
- **Mặt trang:**
  - **Ví dụ 09.5.** Thiết lập B: $x_1,\ldots,x_{5000}$ độc lập $N(0,1)$; $k=10$; $4990$ cửa sổ, $998$ để kiểm tra; lỗi bình phương.
  - Cửa sổ liền nhau chung $k-1=9$ giá trị: cửa sổ chồng lấn (overlapping windows).
  - Tra $u_{j+1}$, chứa đích $x_j$: chia ngẫu nhiên cho MSE (mean squared error) $0{,}8\cdot0+0{,}2\cdot1=0{,}2$; theo thời gian, $0{,}994$.
  - Rủi ro nhỏ nhất là $1$; (T7) không thỏa: rò rỉ thông tin (leakage).
  - {{Hình F1 `cua-so-chong-lan.svg`, cạnh dòng 2}}
- **Ghi chú diễn giả:** Các giá trị độc lập, trung bình $0$, nên với mọi hàm $f$ của ngữ cảnh, $\mathbb E(x_j-f)^2\ge\operatorname{Var}(x_j)=1$. Hàm dự đoán (theo cách của Định nghĩa 01.14) tìm cửa sổ huấn luyện có chín giá trị đầu của ngữ cảnh bằng $(x_{j-9},\ldots,x_{j-1})$; đó là $u_{j+1}$, với giá trị cuối của ngữ cảnh là $x_j$. Cửa sổ này thuộc tập huấn luyện với xác suất khoảng $0{,}8$; thí nghiệm với $10$ chuỗi cho $0{,}200$ (từ $0{,}137$ đến $0{,}245$), chia theo thời gian cho $0{,}994$ (từ $0{,}915$ đến $1{,}066$), bằng MSE của dự đoán $0$. Đích còn nằm trong ngữ cảnh của mười cửa sổ $u_{j+1},\ldots,u_{j+10}$, nên rò rỉ xảy ra với xác suất xấp xỉ $1-0{,}2^{10}$. Khi phần kiểm tra nằm giữa chuỗi, bỏ thêm $k$ cửa sổ ở mỗi biên; các cửa sổ kiểm tra vẫn phụ thuộc nhau, nên Hệ quả 02.10 không cho khoảng tin cậy nếu không có giả thiết thêm. Nguồn: ghi chú Bài 09, §6, Ví dụ 09.5; Phụ lục C.
- **Lý do / nối:** trọng tâm trực quan 1 cho Thiết lập B; "lỗi bình phương trung bình (MSE)" có tiếng Anh ở dòng 3 → độ dài thay đổi.
- **Mục tiêu / nguồn:** 3; Ví dụ 09.5.

#### `3-09` Hàm lỗi tổng và hàm lỗi chuẩn hóa theo độ dài — nhận xét (Nhận xét 09.5), định nghĩa (Định nghĩa 09.6), ví dụ (Ví dụ 09.6) · 2,5 phút
- **Mặt trang:**
  - Độ dài thay đổi: thêm kí tự kết thúc (end-of-sequence token) $\mathtt E$ (Nhận xét 09.5).
  - **Định nghĩa 09.6.** Hàm lỗi tổng (total sequence loss) $\ell(\theta,x)=\sum_{j=1}^{n(x)+1}-\ln p_\theta(x_j\mid x_{<j})$, $x_{n(x)+1}=\mathtt E$.
  - Hàm lỗi chuẩn hóa theo độ dài (length-normalized loss) $\ell_{\mathrm{len}}=\ell/n(x)$.
  - **Ví dụ 09.6.** $D(\mathtt{11})=D(\mathtt{0000000000})=\tfrac12$; kí tự độc lập, là $\mathtt 1$ với xác suất $\theta$.
  - Hàm lỗi tổng cho $\theta=\tfrac16$; hàm lỗi chuẩn hóa cho $\theta=\tfrac12$.
- **Ghi chú diễn giả:** Dùng bảng của câu hỏi mở đầu cho mọi độ dài, tổng các tích trên độ dài $1$ đến $3$ là $1+1+1=3$, nên chúng không là một hàm xác suất. Chuỗi dừng ở lần đầu rút $\mathtt E$; nếu sau mỗi kí tự mô hình rút $\mathtt E$ với xác suất $\tfrac12$, độ dài $n$ có xác suất $(\tfrac12)^n$, tổng $1$. Trong ví dụ, rủi ro với hàm lỗi tổng là $-\ln\theta-5\ln(1-\theta)$, cực tiểu tại $\tfrac16=\tfrac2{12}$; với hàm lỗi chuẩn hóa là $-\tfrac12\ln\theta-\tfrac12\ln(1-\theta)$, cực tiểu tại $\tfrac12$, trung bình của tần suất trong từng chuỗi. Hàm lỗi chuẩn hóa cho mỗi kí tự của chuỗi độ dài $n$ trọng số $1/n$, ở đây $\tfrac14$ với chuỗi ngắn và $\tfrac1{20}$ với chuỗi dài. Khi mọi chuỗi cùng độ dài, hai mục tiêu cùng điểm cực tiểu; khi độ dài khác nhau, cần ghi rõ mục tiêu nào được tối thiểu hóa. Nguồn: ghi chú Bài 09, §5, Nhận xét 09.5; §6, Định nghĩa 09.6, Ví dụ 09.6.
- **Lý do / nối:** Nhận xét 09.5 đặt ở chỗ dùng đầu tiên (mục 11, điểm 4); hai mục tiêu cho hai điểm cực tiểu; câu nối sang mạch 4 ở tiêu đề mạch 4 → tiêu đề mạch 4.
- **Mục tiêu / nguồn:** 3; Nhận xét 09.5, Định nghĩa 09.6, Ví dụ 09.6.

### Mạch 4. Entropy và phân kì Kullback–Leibler (9 trang, 22 phút)

#### `4-00` 4. Entropy và phân kì Kullback–Leibler — tiêu đề mạch, điểm vào mạch 4 · 0,5 phút
- **Mặt trang:**
  - "4."; h2 "Entropy và phân kì Kullback–Leibler"
  - Với hàm lỗi log, rủi ro kì vọng bằng một số chỉ phụ thuộc phân bố thật cộng một độ lệch không âm.
  - entropy · phân kì Kullback–Leibler · đặc tả đúng · quá khớp · làm trơn cộng một
- **Ghi chú diễn giả:** Mạch 3 cho hàm lỗi của một chuỗi và cỡ mẫu trong cận, nhưng chưa cho biết rủi ro kì vọng nhỏ nhất bằng bao nhiêu và một mô hình cách mức đó bao xa. Rủi ro kì vọng phụ thuộc phân bố thật chưa biết. Tách nó thành một phần chỉ phụ thuộc phân bố thật, là giá trị tốt nhất, và một phần đo độ lệch của mô hình, ta biết ước lượng hợp lý cực đại tổng thể nhắm tới mô hình nào, và vì sao trên tập huấn luyện hữu hạn rủi ro thực nghiệm có thể xuống dưới giá trị tốt nhất. Nguồn: ghi chú Bài 09, §7.
- **Lý do / nối:** câu nối từ mạch 3 (cận của Ví dụ 09.4 cần $c>0$, giá trị tốt nhất chưa biết) → định nghĩa.
- **Mục tiêu / nguồn:** 2; §7.

#### `4-01` Entropy, entropy chéo và phân kì Kullback–Leibler — định nghĩa (Định nghĩa 09.7) · 2,5 phút
- **Mặt trang:**
  - Rủi ro kì vọng phụ thuộc phân bố thật chưa biết.
  - **Định nghĩa 09.7.** Entropy $\mathrm H(p_1)=-\sum_xp_1(x)\ln p_1(x)\in[0,\infty]$; entropy chéo (cross-entropy) $\mathbb E_{X\sim p_1}[-\ln p_2(X)]$, bằng $L_D(\theta)$ khi $p_1=p_D$ (hàm xác suất của $D$), $p_2=p_\theta$.
  - Phân kì Kullback–Leibler (Kullback–Leibler divergence, KL), tổng trên giá (support) $\{x:p_1(x)>0\}$:
  - $$\mathrm{KL}(p_1\Vert p_2)=\sum_{x:\,p_1(x)>0}p_1(x)\ln\frac{p_1(x)}{p_2(x)}$$
  - Mật độ: entropy vi phân (differential entropy) $\mathrm h(p_1)=-\int p_1\ln p_1$, có thể âm: đều trên $[0,\tfrac12]$ cho $-\ln2$.
  - Không đối xứng: $\mathrm{KL}(\mathrm{Ber}(0{,}6)\Vert\mathrm{Ber}(0{,}7))\approx0{,}0226$, chiều ngược $\approx0{,}0216$.
- **Ghi chú diễn giả:** Hai hàm xác suất $p_1$, $p_2$ trên một tập đếm được, với quy ước $0\ln0=0$ và $a\ln(a/0)=+\infty$ khi $a>0$. Phân kì KL còn gọi là entropy tương đối (relative entropy), tên dùng trong UML. Tổng trong định nghĩa KL luôn xác định trong $(-\infty,\infty]$: với $t=p_2(x)/p_1(x)$, bất đẳng thức $\ln t\le t-1$ cho mỗi số hạng $\ge-p_2(x)$, và $\sum_xp_2(x)=1$. Với mật độ, $\mathrm{KL}(p_1\Vert p_2)=\int_{p_1>0}p_1\ln(p_1/p_2)$ khi tích phân xác định. Kí hiệu $\mathrm H$, $\mathrm h$ in đứng, khác lớp giả thuyết $\mathcal H$ và giả thuyết $h$. Nguồn: ghi chú Bài 09, §7, Định nghĩa 09.7 và ba đoạn sau.
- **Lý do / nối:** dòng đầu là vấn đề; định nghĩa đặt các đại lượng của mệnh đề → mệnh đề.
- **Mục tiêu / nguồn:** 2; Định nghĩa 09.7.

#### `4-02` Rủi ro bằng entropy cộng phân kì Kullback–Leibler — trực quan, kết quả (Mệnh đề 09.8) · 3 phút
- **Mặt trang:**
  - **Trực quan.** Ở mỗi $x$, mô hình trả thêm $\ln\frac{p_D(x)}{p_\theta(x)}$; vô hạn khi $p_\theta(x)=0<p_D(x)$.
  - **Mệnh đề 09.8.** **Giả thiết:** $\mathcal X$ đếm được; $\mathrm H(p_D)<\infty$; $p_\theta$ là hàm xác suất, $\theta$ cố định.
  - **Bảo đảm:** tổng thể, kì vọng theo $D$: (a) $L_D(\theta)=\mathrm H(p_D)+\mathrm{KL}(p_D\Vert p_\theta)$ trong $[0,\infty]$.
  - (b) $\mathrm{KL}(p_D\Vert p_\theta)\ge0$, dấu bằng khi và chỉ khi $p_\theta=p_D$; do đó $L_D(\theta)\ge\mathrm H(p_D)$.
  - (c) Mật độ có $\int p_D\lvert\ln p_D\rvert,\int p_D\lvert\ln p_\theta\rvert<\infty$: như trên với $\mathrm h(p_D)$, hầu khắp nơi.
- **Ghi chú diễn giả:** Dòng "Trực quan." đọc phần vượt của rủi ro: so với phân bố thật, mô hình chịu thêm $\ln(p_D/p_\theta)$ tại mỗi quan sát, và kì vọng của lượng này theo $D$ là phân kì KL. Phần $\mathrm H(p_D)$ không phụ thuộc mô hình, nên là giá trị tốt nhất. Ở (a), nếu có $x$ với $p_D(x)>0=p_\theta(x)$, hai vế bằng $+\infty$. Bảo đảm là tổng thể: kì vọng theo $D$, không có tập huấn luyện, nên không nói gì về một ước lượng tính từ $m$ quan sát. Với mật độ, $\mathrm h(p_D)$ có thể âm. Khi lớp mô hình chứa $p_D$, phần vượt là rủi ro vượt mức (Định nghĩa 01.24). Mệnh đề được chứng minh đầy đủ trong ghi chú. Nguồn: ghi chú Bài 09, §7, Mệnh đề 09.8 và câu sau chứng minh.
- **Lý do / nối:** trọng tâm trực quan 3; trực quan (cơ chế, cực biên) trước phát biểu → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 2; Mệnh đề 09.8.

#### `4-03` Ý tưởng chứng minh: rủi ro bằng entropy cộng phân kì Kullback–Leibler — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  1. ($p_\theta(x_0)=0<p_D(x_0)$) $L_D=+\infty$; số hạng $x_0$ của KL bằng $+\infty$, phần âm có tổng hữu hạn.
  2. ($\mathrm H(p_D)<\infty$) Trên giá, $-\ln p_\theta=-\ln p_D+\ln(p_D/p_\theta)$; nhân $p_D$, lấy tổng, cộng được hai tổng: (a).
  3. ($\ln t\le t-1$, $t=p_\theta/p_D$) $-\mathrm{KL}\le\sum_{p_D>0}(p_\theta-p_D)=\sum_{p_D>0}p_\theta-1\le0$: (b).
  4. Dấu bằng: $t=1$ trên giá và $p_\theta=0$ ngoài giá; (c): tích phân thay tổng.
  - **Kỹ thuật.** $\ln t\le t-1$ với $t>0$, dấu bằng chỉ khi $t=1$; cho $\mathrm{KL}\ge0$.
- **Ghi chú diễn giả** (~200 âm tiết): Bất đẳng thức then chốt là $\ln t\le t-1$ (câu ôn nhanh 2). Bước 1 xử lý trường hợp mô hình bằng $0$ tại một điểm của giá: quan sát đó xảy ra với xác suất dương nên rủi ro là $+\infty$, và phần âm của các số hạng khác của KL có tổng hữu hạn theo đoạn sau Định nghĩa 09.7. Bước 2 là chỗ duy nhất dùng $\mathrm H(p_D)<\infty$: tổng thứ nhất có số hạng không âm và hữu hạn, tổng thứ hai xác định trong $(-\infty,\infty]$, nên ta cộng được theo từng số hạng. Bỏ giả thiết này, hai tổng có thể có dạng $\infty-\infty$. Bước 3 áp dụng $\ln t\le t-1$ cho từng số hạng; vế phải không quá $0$ vì $p_\theta$ có tổng $1$ trên cả $\mathcal X$. Dấu bằng cần $t=1$ tại mọi điểm của giá và $\sum_{p_D>0}p_\theta=1$, hai điều này nghĩa là $p_\theta=p_D$. Ở (c), hai điều kiện khả tích thay cho entropy hữu hạn, và $\int_{p_D>0}p_\theta\le1$ thay cho tổng. Nguồn: ghi chú Bài 09, chứng minh Mệnh đề 09.8.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; chỗ dùng giả thiết entropy hữu hạn → hệ quả.
- **Mục tiêu / nguồn:** 2; chứng minh Mệnh đề 09.8.

#### `4-04` Ước lượng hợp lý cực đại tổng thể và phân kì KL thuận — kết quả (Hệ quả 09.9), chứng minh một dòng · 2,5 phút
- **Mặt trang:**
  - **Hệ quả 09.9.** **Giả thiết:** như Mệnh đề 09.8; mọi $p_\theta$, $\theta\in\Theta$, là hàm xác suất.
  - **Bảo đảm:** tổng thể. (a) Với $L_D(\theta),L_D(\theta')<\infty$: $L_D(\theta)-L_D(\theta')=\mathrm{KL}(p_D\Vert p_\theta)-\mathrm{KL}(p_D\Vert p_{\theta'})$.
  - $L_D$ và KL thuận (forward KL) có cùng điểm cực tiểu; $\inf_\Theta L_D=\mathrm H(p_D)+\inf_\Theta\mathrm{KL}(p_D\Vert p_\theta)$.
  - (b) Đặc tả đúng (well-specified), $p_D=p_{\theta^\star}$: $\theta^\star$ làm nhỏ nhất $L_D$; mọi điểm cực tiểu có $p_\theta=p_D$.
  - **Chứng minh.** Trừ hai đẳng thức của Mệnh đề 09.8(a).
- **Ghi chú diễn giả:** Phép trừ hợp lệ vì $\mathrm H(p_D)$ hữu hạn; khi $L_D(\theta)=+\infty$, cả $\mathrm{KL}(p_D\Vert p_\theta)=+\infty$, nên hai tiêu chí cùng loại $\theta$ đó. Phần (b) dùng Mệnh đề 09.8(b): $\mathrm{KL}=0$ là giá trị nhỏ nhất, và chỉ đạt khi $p_\theta=p_D$. Ước lượng hợp lý cực đại tổng thể nhắm tới mô hình gần $p_D$ nhất theo $\mathrm{KL}(p_D\Vert\cdot)$. Khi lớp mô hình không chứa $p_D$, mô hình bị đặc tả sai (misspecification); nếu thêm $\inf_\Theta\mathrm{KL}(p_D\Vert p_\theta)>0$, phần chênh này còn lại ngay cả khi có vô hạn dữ liệu. Hệ quả có chứng minh đầy đủ trong ghi chú, gồm hai bước trên. Nguồn: ghi chú Bài 09, §7, Hệ quả 09.9 và chứng minh.
- **Lý do / nối:** hệ quả trực tiếp, chứng minh một dòng trên mặt trang (mục 11, điểm 2); kết quả tổng thể dẫn tới câu hỏi về tập huấn luyện hữu hạn → câu hỏi.
- **Mục tiêu / nguồn:** 2; Hệ quả 09.9.

#### `4-05` Rủi ro thực nghiệm và entropy của phân bố thật — câu hỏi, ví dụ (đoạn sau Hệ quả 09.9) · 2,5 phút
- **Mặt trang:**
  - **Câu hỏi:** mô hình có rủi ro thực nghiệm nhỏ hơn $\mathrm H(p_D)$ có tốt hơn phân bố thật không?
  - $D=\mathrm{Ber}(0{,}6)$; tập huấn luyện của Ví dụ 09.2, $\hat\theta=0{,}7$.
  - Bảng: Đại lượng | Giá trị; $L_s(0{,}7)$ | $0{,}6109$; $\mathrm H(p_D)$ | $0{,}6730$; $L_D(0{,}7)=\mathrm H(p_D)+\mathrm{KL}$ | $0{,}6730+0{,}0226=0{,}6956$
  - Rủi ro thực nghiệm xuống dưới $\mathrm H(p_D)$; rủi ro kì vọng thì không (Mệnh đề 09.8(b)).
  - Khoảng cách tổng quát hóa $0{,}6956-0{,}6109=0{,}0847$.
- **Ghi chú diễn giả:** Hệ quả 09.9 nói về điểm cực tiểu của rủi ro kì vọng, không về rủi ro thực nghiệm trên một tập huấn luyện hữu hạn. Với mười quan sát của Ví dụ 09.2, ước lượng hợp lý cực đại khớp tần suất $0{,}7$ của tập huấn luyện, nên rủi ro thực nghiệm $0{,}6109$ thấp hơn entropy $0{,}6730$ của phân bố thật $\mathrm{Ber}(0{,}6)$. Rủi ro kì vọng của cùng mô hình là $0{,}6956$, vẫn lớn hơn entropy. Câu trả lời cho câu hỏi là không: mô hình chỉ khớp tập huấn luyện. Khoảng cách tổng quát hóa là Định nghĩa 01.10. Nguồn: ghi chú Bài 09, §7, câu hỏi và đoạn sau Hệ quả 09.9.
- **Lý do / nối:** "Câu hỏi." của ghi chú, trả lời trên mặt trang (dòng 4); dùng lại Ví dụ 09.2 → rủi ro kì vọng vô hạn.
- **Mục tiêu / nguồn:** 2; đoạn sau Hệ quả 09.9.

#### `4-06` Ví dụ: rủi ro kì vọng vô hạn của ước lượng hợp lý cực đại — ví dụ, phản ví dụ hàm lỗi không bị chặn (Ví dụ 09.7, Bước 3–4) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 09.7.** $D=\mathrm{Ber}(\theta^\star)$, $\theta^\star=0{,}01$; $S\sim D^m$; $\hat\theta=m_1/m$ của Ví dụ 09.2.
  - Tập huấn luyện toàn số $0$ có xác suất $0{,}99^m$:
  - Bảng: $m$ | $10$ | $50$ | $100$; $0{,}99^m$ | $0{,}9044$ | $0{,}6050$ | $0{,}3660$
  - Trên biến cố đó, $\hat\theta=0$ và $L_D(\hat\theta)=0{,}01\cdot(-\ln0)=+\infty$; nên $\mathbb E_SL_D(\hat\theta)=+\infty$ với mọi $m$.
  - Làm trơn cộng một (add-one smoothing): $\hat\theta=(1+m_1)/(m+2)$, nên $\ell(\hat\theta,x)\le\ln(m+2)$.
  - $m=50$, $m_1=0$: $\hat\theta=\tfrac1{52}$, $L_D(\hat\theta)\approx0{,}0587$, gần $\mathrm H(p_D)\approx0{,}0560$.
- **Ghi chú diễn giả:** Biến cố toàn số $0$ có xác suất dương với mọi $m$, nên kì vọng theo $S$ của rủi ro là vô hạn với mọi cỡ mẫu; xác suất của nó ít nhất $\tfrac12$ khi và chỉ khi $m\le68$. Hàm lỗi log là một hàm lỗi không bị chặn như ở Nhận xét 02.11, nên các bảo đảm cho hàm lỗi bị chặn không chuyển sang được. Làm trơn cộng một giữ $\hat\theta$ trong $[\tfrac1{m+2},\tfrac{m+1}{m+2}]$; đó là ước lượng hợp lý cực đại sau khi thêm hai quan sát giả. Phần đầu của ví dụ: với $p_D=(\tfrac12,\tfrac12,0)$ và mô hình $(1-\theta,\theta,0)$, $L_D$ bằng $1{,}2040$; $3{,}4544$; $6{,}9078$ khi $\theta=10^{-1}$; $10^{-3}$; $10^{-6}$, và $+\infty$ khi $\theta=0$; mô hình $(0{,}4;\,0{,}4;\,0{,}2)$ đặt khối lượng ngoài giá vẫn có $L_D=\ln2{,}5$ hữu hạn. Nguồn: ghi chú Bài 09, §7, Ví dụ 09.7.
- **Lý do / nối:** trọng tâm trực quan 4: phản ví dụ khi bỏ cận dưới cho xác suất → thí nghiệm DNA.
- **Mục tiêu / nguồn:** 2; Ví dụ 09.7.

#### `4-07` Ví dụ: mô hình bigram trên chuỗi DNA tổng hợp — ví dụ (Ví dụ 09.8), trả lời câu hỏi thực hành · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 09.8.** Xích Markov (Markov chain), mỗi hàng $0{,}6$ (giữ nguyên), $0{,}2$, $0{,}1$, $0{,}1$; $n=200$; $200$ chuỗi kiểm tra; $10$ lần chạy.
  - Giá trị tốt nhất $\mathrm H(p_D)/200=(\ln4+199\cdot1{,}0889)/200\approx1{,}0904$ (Mệnh đề 09.8(b)).
  - Bảng: $m$ | MLE | Làm trơn | Mô hình thật; $1$ | $+\infty$ | $1{,}122$ | $1{,}091$; $5$ | $+\infty$ | $1{,}097$ | $1{,}090$; $50$ | $1{,}091$ | $1{,}091$ | $1{,}091$; $500$ | $1{,}088$ | $1{,}088$ | $1{,}088$
  - $m=1$: lỗi huấn luyện $1{,}070<1{,}0904$, lỗi kiểm tra $+\infty$: quá khớp (overfitting).
  - $m=500$: $1{,}088<1{,}0904$, như mô hình thật trên cùng tập kiểm tra: dao động của tập kiểm tra.
- **Ghi chú diễn giả:** Bảng ghi hàm lỗi log trung bình theo kí tự trên tập kiểm tra, trung bình của $10$ lần chạy; lớp bigram chứa mô hình thật, nên đây là trường hợp đặc tả đúng. Giá trị tốt nhất: kí tự đầu có entropy $\ln4$, mỗi chuyển tiếp có entropy của một hàng, $1{,}0889$. Ba câu hỏi thực hành: (i) với $m=50$, lỗi kiểm tra $1{,}091$ cách giá trị tốt nhất khoảng $0{,}0009$ và cách mô hình thật trên cùng tập kiểm tra khoảng $0{,}0007$; (ii) $+\infty$ đến từ các xác suất bằng $0$ của ước lượng hợp lý cực đại (kí tự đầu chưa gặp: $10/10$ lần chạy với $m=1$, $5/10$ với $m=5$), và làm trơn bỏ được chúng; (iii) với mô hình làm trơn, xác suất bị chặn dưới, nên khoảng tin cậy dùng số chuỗi kiểm tra làm cỡ mẫu. Nguồn: ghi chú Bài 09, §7, Ví dụ 09.8; §3, khối ứng dụng; Phụ lục C.
- **Lý do / nối:** ý in đậm của ghi chú ("quá khớp") trên mặt trang; thí nghiệm nối Mệnh đề 09.8 với cỡ mẫu hữu hạn → bài tập.
- **Mục tiêu / nguồn:** 2, 3; Ví dụ 09.8.

#### `4-08` Bài tập: entropy chéo, entropy và phân kì KL — bài tập (Bài tập 09.3(b), (c)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 09.3.** $\mathcal X=\{1,2,3\}$, $p_D=(\tfrac12,\tfrac14,\tfrac14)$.
  - (b) $p_\theta$ đều; (c) $p_\theta=(\tfrac12,\tfrac12,0)$: tính $\mathrm H(p_D)$, $L_D(\theta)$, hai chiều KL; kiểm Mệnh đề 09.8(a).
  - (c) MLE tổng thể làm nhỏ nhất chiều nào?
  - Mô hình gán xác suất $0$ cho quan sát có thể xảy ra bị đánh giá thế nào?
  - [f] **Lời giải:** Bảng: Đại lượng | (b) | (c); $\mathrm H(p_D)$ | $1{,}0397$ | $1{,}0397$; $L_D(\theta)$ | $\ln3\approx1{,}0986$ | $+\infty$; $\mathrm{KL}(p_D\Vert p_\theta)$ | $0{,}0589$ | $+\infty$; $\mathrm{KL}(p_\theta\Vert p_D)$ | $0{,}0566$ | $\tfrac12\ln2\approx0{,}3466$
  - [f] Chiều thuận: mô hình bỏ một điểm của giá có rủi ro $+\infty$.
- **Ghi chú diễn giả:** Câu chữ đầy đủ của đề: "(b) Với $p_\theta$ đều trên $\mathcal X$, tính $\mathrm H(p_D)$, entropy chéo $L_D(\theta)$ và $\mathrm{KL}(p_D\Vert p_\theta)$, kiểm Mệnh đề 09.8(a), rồi tính $\mathrm{KL}(p_\theta\Vert p_D)$. (c) Với $p_\theta=(\tfrac12,\tfrac12,0)$, tính $L_D(\theta)$, $\mathrm{KL}(p_D\Vert p_\theta)$ và $\mathrm{KL}(p_\theta\Vert p_D)$. Ước lượng hợp lý cực đại tổng thể làm nhỏ nhất chiều nào (Hệ quả 09.9)? Với chiều đó, một mô hình gán xác suất $0$ cho một quan sát có thể xảy ra bị đánh giá thế nào?" Ở (b), $\mathrm H(p_D)=\tfrac32\ln2$, hai chiều KL khác nhau (KL không đối xứng), và $1{,}0397+0{,}0589=1{,}0986$, đúng Mệnh đề 09.8(a). Ở (c), $p_D(3)=\tfrac14>0=p_\theta(3)$, nên chiều thuận, chiều mà Hệ quả 09.9 làm nhỏ nhất, là $+\infty$; chiều ngược chỉ đo trên giá của $p_\theta$ và cho $\tfrac12\ln2$. Phần (a) (chứng minh bằng bất đẳng thức Jensen) và (d) (rời rạc hóa entropy vi phân) để về nhà. Nguồn: tệp bài tập, Bài tập 09.3 và lời giải.
- **Lý do / nối:** bài tập của mạch 4 từ `exercises.md`, câu chữ rút gọn trên mặt trang (đủ dữ kiện, câu hỏi, kết quả; câu đầy đủ ở ghi chú diễn giả); câu nối sang mạch 5 ở tiêu đề mạch 5 → tiêu đề mạch 5.
- **Mục tiêu / nguồn:** 2; Bài tập 09.3(b), (c).

### Mạch 5. Mô hình biến ẩn và cận dưới bằng chứng (7 trang, 18 phút)

#### `5-00` 5. Mô hình biến ẩn và cận dưới bằng chứng — tiêu đề mạch, điểm vào mạch 5 · 0,5 phút
- **Mặt trang:**
  - "5."; h2 "Mô hình biến ẩn và cận dưới bằng chứng"
  - Khi có biến không quan sát được, log độ hợp lý bị chặn dưới bởi một đại lượng ước lượng được bằng rút mẫu.
  - biến ẩn · hậu nghiệm · cận dưới bằng chứng · khe · thuật toán EM
- **Ghi chú diễn giả:** Hàm lỗi vẫn là $-\ln p_\theta(x)$, nên Mệnh đề 09.8 và Hệ quả 09.9 áp dụng cho $p_\theta(x)$. Khó khăn mới nằm ở chỗ tính $p_\theta(x)$: với một biến không quan sát được, độ hợp lý là một tổng hay một tích phân theo biến đó, và khi mô hình quan sát là một mạng nơ-ron, tích phân này nói chung không tính được (Kingma và Welling, §2.1). Ta thay nó bằng một cận dưới chỉ cần giá trị của mật độ liên hợp, và đo khoảng cách giữa cận và log độ hợp lý bằng phân kì KL của mạch trước. Nguồn: ghi chú Bài 09, §8.
- **Lý do / nối:** câu nối từ mạch 4 (KL) sang mạch 5 → định nghĩa.
- **Mục tiêu / nguồn:** 4; §8.

#### `5-01` Mô hình biến ẩn — định nghĩa (Định nghĩa 09.10), ví dụ (Ví dụ 09.9) · 3 phút
- **Mặt trang:**
  - Rút một biến không quan sát được, rồi rút quan sát.
  - **Định nghĩa 09.10.** Biến ẩn (latent variable) $v\in\mathcal V$; $p_\theta(x,v)=p_\theta(v)\,p_\theta(x\mid v)$: tiên nghiệm (prior), mô hình quan sát.
  - Bằng chứng (evidence) $\ln p_\theta(x)$, $p_\theta(x)=\int_{\mathcal V}p_\theta(x,v)\,dv$; hậu nghiệm (posterior) $p_\theta(v\mid x)=p_\theta(x,v)/p_\theta(x)$.
  - Phân bố biến phân (variational distribution) $q_\phi(\cdot\mid x)$, $\phi\in\Phi$, xấp xỉ $p_\theta(\cdot\mid x)$.
  - **Ví dụ 09.9.** $v\sim N(0,1)$, $x\mid v\sim N(v,1)$, $x=2$: $x\sim N(0,2)$, $\ln p_\theta(2)=-\tfrac12\ln(4\pi)-1\approx-2{,}2655$.
  - Hậu nghiệm $N(\tfrac x2,\tfrac12)=N(1,\tfrac12)$: trung bình nằm giữa $0$ của tiên nghiệm và quan sát $2$.
- **Ghi chú diễn giả:** Câu ôn nhanh 3 là một mô hình biến ẩn với $\mathcal V=\{1,2\}$: $\Pr(x)=\tfrac12\cdot0{,}2+\tfrac12\cdot0{,}6=0{,}4$ và $\Pr(v=2\mid x)=0{,}3/0{,}4=0{,}75$. Mật độ liên hợp (joint density) gồm tiên nghiệm và mô hình quan sát; khi $\mathcal V$ hữu hạn, tích phân là tổng. Hậu nghiệm xác định khi $0<p_\theta(x)<\infty$; $\phi$ có thể dùng chung cho mọi $x$. Trong ví dụ, $x$ là tổng của $v$ và một biến $N(0,1)$ độc lập với $v$, nên $x\sim N(0,2)$; hoàn thành bình phương (Phụ lục A) cho hậu nghiệm tỉ lệ với $\exp(-(v-\tfrac x2)^2)$. Phương sai giảm từ $1$ xuống $\tfrac12$. Bằng chứng và hậu nghiệm có dạng đóng, nên đo được sai số của mọi phân bố biến phân. Nguồn: ghi chú Bài 09, §8, Định nghĩa 09.10, Ví dụ 09.9; Phụ lục A(ii).
- **Lý do / nối:** mở bằng câu khẳng định; ví dụ có dạng đóng trên cùng trang → cận dưới.
- **Mục tiêu / nguồn:** 4; Định nghĩa 09.10, Ví dụ 09.9.

#### `5-02` Đồng nhất thức của cận dưới bằng chứng — định nghĩa (Định nghĩa 09.11), trực quan, kết quả (Định lý 09.12) · 3 phút
- **Mặt trang:**
  - **Định nghĩa 09.11.** Cận dưới bằng chứng (evidence lower bound, ELBO):
  - $$\operatorname{ELBO}(\theta,\phi;x)=\mathbb E_{v\sim q_\phi(\cdot\mid x)}\ln\frac{p_\theta(x,v)}{q_\phi(v\mid x)}$$
  - **Trực quan.** Đổi $q$ không đổi bằng chứng; ELBO lớn nhất khi $q$ là hậu nghiệm.
  - **Định lý 09.12.** **Giả thiết:** $q=q_\phi(\cdot\mid x)$; $0<p_\theta(x)<\infty$; $p_\theta(x,v)>0$ cho $q$-hầu hết $v$; $\ln p_\theta(x,v)$, $\ln q$ khả tích theo $q$.
  - **Bảo đảm:** tất định: (a) $\ln p_\theta(x)=\operatorname{ELBO}+\mathrm{KL}(q\Vert p_\theta(\cdot\mid x))$; (b) $\operatorname{ELBO}\le\ln p_\theta(x)$, dấu bằng khi và chỉ khi $q=p_\theta(\cdot\mid x)$ hầu khắp nơi.
  - (c) Thêm $\mathbb E_q\lvert\ln p_\theta(v)\rvert<\infty$: $\operatorname{ELBO}=\mathbb E_q\ln p_\theta(x\mid v)-\mathrm{KL}(q\Vert p_\theta(\cdot))$ (số hạng tái tạo, reconstruction term).
- **Ghi chú diễn giả:** Cận dưới bằng chứng còn gọi là cận dưới biến phân (variational lower bound); kì vọng lấy theo $q_\phi$, nên ELBO ước lượng được bằng cách rút $v$ từ $q_\phi$. Dòng "Trực quan." đọc (a): bằng chứng chỉ phụ thuộc mô hình và $x$, nên cực đại hóa ELBO theo $\phi$ thu hẹp khe (gap) $\ln p_\theta(x)-\operatorname{ELBO}$, tức phân kì KL tới hậu nghiệm, mà không đổi $\ln p_\theta(x)$. Giả thiết thứ hai nói $q$ không đặt khối lượng ở chỗ hậu nghiệm bằng $0$; nếu $q$ đặt khối lượng dương ở đó và $\mathbb E_q\lvert\ln q\rvert<\infty$, thì $\operatorname{ELBO}=-\infty$ và (b) vẫn đúng (Phạm vi). Phần (d): với tập huấn luyện thỏa giả thiết tại mỗi $x^{(i)}$, $L_s(\theta)\le-\frac1m\sum_i\operatorname{ELBO}(\theta,\phi;x^{(i)})$, nên tối thiểu hóa vế phải là tối thiểu hóa một cận trên của rủi ro thực nghiệm. Định lý được chứng minh đầy đủ trong ghi chú. Nguồn: ghi chú Bài 09, §8, Định nghĩa 09.11, Định lý 09.12 và câu sau chứng minh.
- **Lý do / nối:** trọng tâm trực quan 5; định nghĩa, trực quan, phát biểu cùng trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 4; Định nghĩa 09.11, Định lý 09.12.

#### `5-03` Ý tưởng chứng minh: đồng nhất thức của cận dưới bằng chứng — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  1. ($0<p_\theta(x)<\infty$) Bayes với $p_\theta(x,v)>0$: $\ln p_\theta(x)=\ln p_\theta(x,v)-\ln p_\theta(v\mid x)$.
  2. (giả thiết về $q$) Thêm bớt $\ln q(v)$, với $q$-hầu hết $v$: $\ln p_\theta(x)=\big[\ln p_\theta(x,v)-\ln q(v)\big]+\big[\ln q(v)-\ln p_\theta(v\mid x)\big]$.
  3. (khả tích) Lấy $\mathbb E_q$: ngoặc đầu cho ELBO, ngoặc sau cho $\mathrm{KL}(q\Vert p_\theta(\cdot\mid x))$: (a).
  4. **Nhắc lại:** $\ln t\le t-1$ cho $\mathrm{KL}\ge0$ (Mệnh đề 09.8(b)): (b). Tách $\ln p_\theta(x,v)=\ln p_\theta(x\mid v)+\ln p_\theta(v)$: (c).
  - **Kỹ thuật.** Thêm bớt $\ln q(v)$ rồi lấy kì vọng theo $q$, phân bố do ta chọn.
- **Ghi chú diễn giả** (~180 âm tiết): Bất đẳng thức then chốt là $\mathrm{KL}\ge0$. Bước 1 dùng $0<p_\theta(x)<\infty$ để hậu nghiệm xác định và dương tại mọi $v$ có $p_\theta(x,v)>0$. Bước 2 dùng giả thiết về $q$: với $q$-hầu hết $v$, Bước 1 áp dụng được. Ở Bước 3, ngoặc thứ nhất khả tích theo giả thiết; ngoặc thứ hai bằng hằng số $\ln p_\theta(x)$ trừ ngoặc thứ nhất, nên cũng khả tích. Bước 4 áp dụng lập luận của chứng minh Mệnh đề 09.8 cho hai mật độ $q$ và $p_\theta(\cdot\mid x)$ trên $\mathcal V$. Khi bỏ giả thiết về $q$: với $x=v\sim N(0,1)$ không có nhiễu, hậu nghiệm là khối lượng điểm (point mass) tại $v=x$, không có mật độ, và KL từ một mật độ bất kì tới nó bằng $+\infty$. Phần (d) là (b) tại mỗi $x^{(i)}$, đổi dấu rồi lấy trung bình. Nguồn: ghi chú Bài 09, chứng minh Định lý 09.12; đoạn sau Định nghĩa 09.10.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; nhắc lại kỹ thuật của 4-03 → ví dụ Gauss.
- **Mục tiêu / nguồn:** 4; chứng minh Định lý 09.12.

#### `5-04` Ví dụ: số hạng tái tạo, phân kì KL và khe của cận — ví dụ (Ví dụ 09.10), hình F2 · 3 phút
- **Mặt trang:**
  - **Ví dụ 09.10.** Ví dụ 09.9 tại $x=2$; $q_\phi=N(\mu,\sigma^2)$, $\phi=(\mu,\sigma)$.
  - Tái tạo $-\tfrac12\ln(2\pi)-\tfrac12\big((2-\mu)^2+\sigma^2\big)$; KL tới tiên nghiệm $\tfrac12(\mu^2+\sigma^2-1-\ln\sigma^2)$.
  - Bảng: $\mu;\sigma^2$ | Tái tạo | KL | ELBO | Khe; $0;1$ | $-3{,}4189$ | $0$ | $-3{,}4189$ | $1{,}1534$; $1;1$ | $-1{,}9189$ | $0{,}5$ | $-2{,}4189$ | $0{,}1534$; $0{,}8;0{,}5$ | $-1{,}8889$ | $0{,}4166$ | $-2{,}3055$ | $0{,}0400$; $1;0{,}5$ | $-1{,}6689$ | $0{,}5966$ | $-2{,}2655$ | $0$
  - Khe (gap) $\ln p_\theta(2)-\operatorname{ELBO}=\mathrm{KL}(q_\phi\Vert N(1,\tfrac12))$; dòng đầu: $1{,}1534$, đúng Định lý 09.12(a).
  - Cực đại tại $\mu=1$, $\sigma^2=\tfrac12$, tức hậu nghiệm: khe $0$.
  - {{Hình F2 `elbo-theo-mu.svg`, cột phải; bảng cột trái}}
- **Ghi chú diễn giả:** Công thức KL tới tiên nghiệm $N(0,1)$ là công thức sau Định nghĩa 09.7 với $\mu_2=0$, $\sigma_2=1$. Dòng đầu, với $q_\phi$ bằng tiên nghiệm, có KL tới tiên nghiệm bằng $0$ nhưng số hạng tái tạo thấp. Dòng cuối có KL tới tiên nghiệm $0{,}5966$ nhưng số hạng tái tạo cao hơn, vì $q_\phi$ đặt $v$ gần quan sát, và khe bằng $0$. Kiểm khe dòng đầu: $\mathrm{KL}(N(0,1)\Vert N(1,\tfrac12))=\ln\sqrt{0{,}5}+2-0{,}5\approx1{,}1534$; ba dòng còn lại trùng đến bốn chữ số. Đạo hàm $\partial_\mu\operatorname{ELBO}=2-2\mu$ và $\partial_\sigma\operatorname{ELBO}=-2\sigma+1/\sigma$; $-\operatorname{ELBO}$ lồi nghiêm ngặt theo $(\mu,\sigma)$ trên $\sigma>0$ (Phụ lục A(iii)). Hình vẽ ELBO theo $\mu$ với hai giá trị của $\sigma^2$; khoảng cách dọc tới đường $-2{,}2655$ là khe. Nguồn: ghi chú Bài 09, §8, Ví dụ 09.10; Phụ lục A(iii).
- **Lý do / nối:** trọng tâm trực quan 5 bằng số và hình → thuật toán EM.
- **Mục tiêu / nguồn:** 4; Ví dụ 09.10.

#### `5-05` Thuật toán EM không làm giảm log độ hợp lý — kết quả (Hệ quả 09.13), chứng minh một dòng · 2,5 phút
- **Mặt trang:**
  - $\mathcal V$ hữu hạn: thuật toán EM (Expectation–Maximization) cực đại hóa ELBO luân phiên theo $q$ và $\theta$.
  - **Hệ quả 09.13.** **Giả thiết:** $s$ cố định, $p_{\theta_t}(x^{(i)})>0$; bước E: $q_i=p_{\theta_t}(\cdot\mid x^{(i)})$;
  - bước M: $\theta_{t+1}$ làm lớn nhất $\sum_i\mathbb E_{v\sim q_i}\ln p_\theta(x^{(i)},v)$ trên $\Theta$, giá trị lớn nhất hữu hạn.
  - **Bảo đảm:** tất định: $L_s(\theta_{t+1})\le L_s(\theta_t)$; không chứa $L_D$, không nói về cực tiểu toàn cục.
  - **Chứng minh.** Định lý 09.12(b); bước M; dấu bằng tại hậu nghiệm:
  - $$\textstyle\sum_i\ln p_{\theta_{t+1}}(x^{(i)})\ge\sum_i\operatorname{ELBO}(\theta_{t+1},q_i;x^{(i)})\ge\sum_i\operatorname{ELBO}(\theta_t,q_i;x^{(i)})=\sum_i\ln p_{\theta_t}(x^{(i)})$$
- **Ghi chú diễn giả:** Ta viết $\operatorname{ELBO}(\theta,q;x)$ khi phân bố biến phân là một hàm xác suất $q$ cho trước trên $\mathcal V$; chỉ số $t$ đếm vòng lặp. Bước E đặt khe bằng $0$ tại $\theta_t$; bước M nâng ELBO. Dòng thứ hai của dãy dùng $\operatorname{ELBO}(\theta,q_i;x^{(i)})=\mathbb E_{q_i}\ln p_\theta(x^{(i)},v)+\mathrm H(q_i)$, với $\mathrm H(q_i)$ không phụ thuộc $\theta$. Trước dòng đầu, cần kiểm giả thiết của Định lý 09.12 tại $\theta_{t+1}$: giá trị lớn nhất của bước M hữu hạn và $\mathcal V$ hữu hạn, nên $p_{\theta_{t+1}}(x^{(i)},v)>0$ trên giá của $q_i$. Nhân với $-\frac1m$ được bảo đảm. Mọi $\theta_{t+1}$ không làm giảm tổng ở bước M đều cho cùng kết luận. Hệ quả được chứng minh đầy đủ ở Phụ lục D. Nguồn: ghi chú Bài 09, §8, Hệ quả 09.13; Phụ lục D; UML §24.4.1.
- **Lý do / nối:** hệ quả có dãy chứng minh ba quan hệ trên mặt trang (mục 11, điểm 2) → bài tập.
- **Mục tiêu / nguồn:** 4; Hệ quả 09.13.

#### `5-06` Bài tập: cận dưới bằng chứng cho một hỗn hợp hai Gauss — bài tập (Bài tập 09.4(b)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 09.4.** (b) $v\in\{1,2\}$, $\Pr(v=1)=\Pr(v=2)=\tfrac12$; $x\mid v=1\sim N(-1,1)$, $x\mid v=2\sim N(1,1)$; $x=0{,}5$.
  - Tính $p_\theta(x)$, $\Pr(v=2\mid x)$; ELBO và khe với $q(2)=0{,}5$, $0{,}9$; với $q(2)=0{,}9$, kiểm khe bằng KL tới hậu nghiệm và Định lý 09.12(c).
  - [f] **Lời giải:** $p_\theta(0{,}5)\approx0{,}2408$, $\ln p_\theta(0{,}5)\approx-1{,}4238$; $\Pr(v=2\mid x)=1/(1+e^{-1})\approx0{,}7311$.
  - [f] Bảng: $q(2)$ | ELBO | Khe; $0{,}5$ | $-1{,}5439$ | $0{,}1201$; $0{,}9$ | $-1{,}5120$ | $0{,}0882$
  - [f] $q(2)=0{,}9$: KL tới hậu nghiệm $0{,}0882$; tái tạo $-1{,}1439$ trừ KL tới tiên nghiệm $0{,}3681$ bằng $-1{,}5120$.
- **Ghi chú diễn giả:** Câu chữ đầy đủ của đề: "Tính $p_\theta(x)$, $\ln p_\theta(x)$ và hậu nghiệm $\Pr(v=2\mid x)$. Với $q(2)=0{,}5$ và $q(2)=0{,}9$, tính ELBO và khe $\ln p_\theta(x)-\operatorname{ELBO}$. Với $q(2)=0{,}9$, kiểm khe bằng $\mathrm{KL}(q\Vert p_\theta(\cdot\mid x))$, rồi tính số hạng tái tạo, KL tới tiên nghiệm, và kiểm Định lý 09.12(c)." Gọi $\rho_0$ là mật độ của $N(0,1)$; hai mật độ có điều kiện tại $x=0{,}5$ là $\rho_0(1{,}5)\approx0{,}1295$ và $\rho_0(0{,}5)\approx0{,}3521$, tỉ số $e^{-1}$. Hậu nghiệm là $(0{,}2689;\,0{,}7311)$; $q(2)=0{,}9$ gần hậu nghiệm hơn $q(2)=0{,}5$, và khe nhỏ hơn. Phần (a) (chứng minh trực tiếp bằng $\ln t\le t-1$), (c) (giá của $q$) và (d) (biến ẩn rời rạc) để về nhà. Nguồn: tệp bài tập, Bài tập 09.4 và lời giải.
- **Lý do / nối:** bài tập của mạch 5 từ `exercises.md`; khe bằng KL trên một hỗn hợp; câu nối sang mạch 6 ở tiêu đề mạch 6 → tiêu đề mạch 6.
- **Mục tiêu / nguồn:** 4; Bài tập 09.4(b).

### Mạch 6. Tái tham số hóa và so sánh các mô hình sinh (9 trang, 22,5 phút)

#### `6-00` 6. Tái tham số hóa và so sánh các mô hình sinh — tiêu đề mạch, điểm vào mạch 6 · 0,5 phút
- **Mặt trang:**
  - "6."; h2 "Tái tham số hóa và so sánh các mô hình sinh"
  - Viết lần rút thành hàm của một nhiễu cố định đưa đạo hàm vào trong kì vọng, dưới điều kiện khả vi và khả tích.
  - tái tham số hóa · gradient theo đường đi · gradient log · hàm trội · dữ liệu sinh ra
- **Ghi chú diễn giả:** Khi hậu nghiệm không có dạng đóng, bước E không tính được. Kingma và Welling (§2.1–§2.3) thay nó bằng một phân bố biến phân dùng chung cho mọi quan sát và cực đại hóa ELBO theo cả $\theta$ lẫn $\phi$ bằng SGD. ELBO là một kì vọng theo $q_\phi$, nên gradient theo $\phi$ cần đạo hàm của một kì vọng theo một phân bố phụ thuộc chính $\phi$. Cuối mạch, một mô hình sinh được đánh giá theo hai tiêu chí: hàm lỗi log và mức giống dữ liệu thật của dữ liệu sinh ra. Nguồn: ghi chú Bài 09, §8 đoạn cuối, §9.
- **Lý do / nối:** câu nối từ mạch 5 (bước E không tính được) → định nghĩa.
- **Mục tiêu / nguồn:** 5; §9.

#### `6-01` Tái tham số hóa và hai ước lượng gradient — vấn đề, định nghĩa (Định nghĩa 09.14), trực quan · 2,5 phút
- **Mặt trang:**
  - SGD trên ELBO cần $\nabla F$, $F(\phi)=\mathbb E_{v\sim q_\phi}f(v)$; phân bố phụ thuộc $\phi$, nên $\nabla F$ nói chung khác $\mathbb E_{v\sim q_\phi}\nabla_\phi f(v)=0$.
  - **Định nghĩa 09.14.** Nhiễu phụ (auxiliary noise) $\zeta$: phân bố không phụ thuộc $\phi$.
  - Tái tham số hóa (reparameterization): $g_\phi(\zeta)$ có phân bố $q_\phi$; Gauss: $\zeta\sim N(0,I_r)$, $g_\phi(\zeta)=\mu_\phi+\sigma_\phi\odot\zeta$.
  - Ước lượng gradient theo đường đi (pathwise gradient estimator): $\nabla_\phi\big[f(g_\phi(\zeta))\big]$.
  - Ước lượng gradient log (score-function estimator): $f(v)\,\nabla_\phi\ln q_\phi(v)$, $v\sim q_\phi$.
  - **Trực quan.** $F(\phi)=\mathbb E_\zeta f(g_\phi(\zeta))$: $\phi$ chỉ còn trong hàm dưới kì vọng.
- **Ghi chú diễn giả:** Gradient $\mathbb E_{v\sim q_\phi}\nabla_\phi f(v)$ bằng $0$ vì $f$ không phụ thuộc $\phi$; sự phụ thuộc nằm ở phân bố lấy kì vọng. Có hai cách: lấy đạo hàm của mật độ (ước lượng gradient log), hoặc chuyển sự phụ thuộc vào hàm lấy kì vọng (tái tham số hóa). Với họ Gauss, $\mu_\phi,\sigma_\phi\in\mathbb R^r$ có thể phụ thuộc $x$, và $\odot$ là tích từng thành phần. Mỗi ước lượng dùng một lần rút: $\zeta$ cho ước lượng theo đường đi, $v\sim q_\phi$ cho ước lượng gradient log. Vì $g_\phi(\zeta)$ có phân bố $q_\phi$, ta có $F(\phi)=\mathbb E_\zeta f(g_\phi(\zeta))$ (Kingma và Welling, §2.4); câu hỏi còn lại là khi nào gradient của vế phải bằng kì vọng của gradient. Với ELBO, khi KL tới tiên nghiệm có dạng đóng (Định lý 09.12(c)), chỉ số hạng tái tạo cần rút mẫu. Nguồn: ghi chú Bài 09, §9, đoạn mở, Định nghĩa 09.14 và đoạn sau.
- **Lý do / nối:** vấn đề → định nghĩa → trực quan của Mệnh đề 09.15 (dòng cuối) → mệnh đề.
- **Mục tiêu / nguồn:** 5; Định nghĩa 09.14.

#### `6-02` Gradient theo đường đi không chệch — kết quả (Mệnh đề 09.15) · 3 phút
- **Mặt trang:**
  - **Mệnh đề 09.15.** **Giả thiết:** $\zeta$ là nhiễu phụ; $\Phi$ mở; $\kappa(\phi,\zeta)$ đo được, như $f(g_\phi(\zeta))$.
  - (i) Có $N_0$ xác suất $0$, không phụ thuộc $\phi$: với $\zeta\notin N_0$, $\kappa(\cdot,\zeta)$ khả vi liên tục trên $\Phi$.
  - (ii) Hàm trội (dominating function): mỗi $\phi_0$ có lân cận $U$, $M\ge0$, $\mathbb EM(\zeta)<\infty$, $\lVert\nabla_\phi\kappa(\phi,\zeta)\rVert\le M(\zeta)$ trên $U$.
  - (iii) $\mathbb E\lvert\kappa(\phi,\zeta)\rvert<\infty$ với mọi $\phi$.
  - **Bảo đảm:** kì vọng theo $\zeta$: $F$ khả vi, $\nabla F(\phi)=\mathbb E\nabla_\phi\kappa(\phi,\zeta)$; một lần rút cho ước lượng không chệch.
- **Ghi chú diễn giả:** Bảo đảm là theo kì vọng theo nhiễu phụ, tất định theo $\phi$; với $\kappa=f\circ g_\phi$, ước lượng theo đường đi là ước lượng không chệch của $\nabla F(\phi)$. Điều kiện (i) đòi một tập ngoại lệ chung cho mọi $\phi$, không chỉ khả vi tại từng $\phi$ cho hầu hết $\zeta$. Một điều kiện đủ (Phụ lục B, Bước 6): $\zeta\sim N(0,I_r)$, $g_\phi(\zeta)=\mu_\phi+\sigma_\phi\odot\zeta$ với $\mu_\phi$, $\sigma_\phi$ khả vi liên tục, $f$ khả vi liên tục với $\lVert\nabla f(v)\rVert\le C(1+\lVert v\rVert^2)$ và $\lvert f(v)\rvert\le C(1+\lVert v\rVert^3)$. Mệnh đề được phát biểu ở mức phác thảo trong thân bài, chứng minh chi tiết ở Phụ lục B. Phương sai của ước lượng cần một cận riêng, như (G2) của Bài 05. Nguồn: ghi chú Bài 09, §9, Mệnh đề 09.15.
- **Lý do / nối:** trực quan ở dòng cuối 6-01, ví dụ ở 6-05 sau phát biểu vì ví dụ kiểm điều kiện của mệnh đề (mục 7) → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 5; Mệnh đề 09.15.

#### `6-03` Ý tưởng chứng minh: gradient theo đường đi không chệch — ý tưởng chứng minh (Phụ lục B) · 3 phút
- **Mặt trang:**
  1. ((i)) Giá trị trung bình (mean value theorem) trên đoạn $[\phi_0,\phi_0+\Delta e]$, cùng $\zeta\notin N_0$.
  2. ((ii)) Thương sai phân bị chặn bởi $M(\zeta)$, khả tích.
  3. ((iii)) $F$ hữu hạn; hội tụ bị chặn (dominated convergence) khi $\Delta\to0$: $\partial_eF(\phi_0)=\mathbb E\langle\nabla_\phi\kappa(\phi_0,\zeta),e\rangle$.
  4. Hội tụ bị chặn: đạo hàm riêng liên tục, nên $F$ khả vi.
  - Tập ngoại lệ phụ thuộc $\phi$: hợp theo $\phi$ có thể có xác suất dương.
- **Ghi chú diễn giả** (~200 âm tiết): Bất đẳng thức then chốt là cận $M(\zeta)$ cho trị tuyệt đối của thương sai phân. Bước 1 cố định $\phi_0$, một hướng đơn vị $e$ và $\lvert\Delta\rvert$ đủ nhỏ để đoạn nằm trong $U$; theo định lý giá trị trung bình, thương sai phân $(\kappa(\phi_0+\Delta e,\zeta)-\kappa(\phi_0,\zeta))/\Delta$ bằng đạo hàm theo hướng $e$ tại một điểm của đoạn. Bước này cần $\kappa(\cdot,\zeta)$ khả vi tại mọi điểm của đoạn với cùng một $\zeta$. Dòng cuối nêu chỗ hỏng: nếu tập ngoại lệ phụ thuộc $\phi$, hợp các tập ngoại lệ trên đoạn có thể có xác suất dương; với hàm chỉ báo, tập ngoại lệ tại $\mu$ là $\{-\mu\}$, và hợp theo $\mu$ trong một khoảng là một khoảng. Bước 3 dùng (iii) để thương sai phân của $F$ bằng kì vọng của thương sai phân của $\kappa$, rồi định lý hội tụ bị chặn. Bước 4 dùng tính liên tục của $\nabla_\phi\kappa$ và cùng hàm trội; một hàm có mọi đạo hàm riêng liên tục trên tập mở thì khả vi. Với $\xi=(i,\zeta)$, $i$ rút đều, $\nabla_{\theta,\phi}\kappa_i$ là gradient ngẫu nhiên không chệch của $-\frac1m\sum_i\operatorname{ELBO}(\theta,\phi;x^{(i)})$; Định lý 05.14 còn cần (C), mà $-\operatorname{ELBO}$ nói chung không lồi. Nguồn: ghi chú Bài 09, chứng minh Mệnh đề 09.15; Phụ lục B; đoạn sau chứng minh.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; chỗ hỏng khi bỏ (i) → kỹ thuật.
- **Mục tiêu / nguồn:** 5; Phụ lục B.

#### `6-04` Đổi chỗ đạo hàm và kì vọng — kỹ thuật (trang riêng) · 2,5 phút
- **Mặt trang:**
  - **Kỹ thuật.** $\nabla_\phi\mathbb E\kappa(\phi,\zeta)=\mathbb E\nabla_\phi\kappa(\phi,\zeta)$ khi phân bố của $\zeta$ không phụ thuộc $\phi$.
  - Cần: khả vi trên mọi đường ngoài một tập xác suất $0$ chung; hàm trội khả tích.
  - Dùng khi cần gradient không chệch của một kì vọng, như SGD trên ELBO.
  - Không dùng được khi hàm nhảy theo $\phi$: hàm chỉ báo, biến rời rạc.
- **Ghi chú diễn giả:** Dạng tổng quát gồm ba bước của trang trước: định lý giá trị trung bình trên từng đường nhiễu, hàm trội chặn các thương sai phân, định lý hội tụ bị chặn đưa giới hạn vào trong kì vọng. Ước lượng dùng một lần rút nhiễu. Kỹ thuật dùng ở Mệnh đề 09.15 và để kiểm điều kiện của gradient theo đường đi trong mô hình Gauss. Điều kiện khả tích (iii) bảo đảm vế trái xác định. Với một hàm có bước nhảy theo $\phi$, đạo hàm trên từng đường bằng $0$ hầu chắc chắn trong khi đạo hàm của kì vọng khác $0$. Nguồn: ghi chú Bài 09, §9, Mệnh đề 09.15; Phụ lục B.
- **Lý do / nối:** kỹ thuật dùng lại ở bài sau (mục 14) có trang "Kỹ thuật." riêng, tiêu đề là tên kỹ thuật → ví dụ Gauss.
- **Mục tiêu / nguồn:** 5; Phụ lục B.

#### `6-05` Ví dụ: gradient theo đường đi trong mô hình Gauss — ví dụ (Ví dụ 09.11) · 3 phút
- **Mặt trang:**
  - **Ví dụ 09.11.** Ví dụ 09.10, $x=2$; chỉ rút mẫu số hạng tái tạo:
  - $$\kappa(\mu,\sigma,\zeta)=-\tfrac12\ln(2\pi)-\tfrac12(2-\mu-\sigma\zeta)^2-\tfrac12(\mu^2+\sigma^2-1-\ln\sigma^2)$$
  - Gradient đúng tại $(0,1)$: $(2-2\mu,\,-2\sigma+1/\sigma)=(2,-1)$.
  - Một lần rút: $(2-\zeta,\ 2\zeta-\zeta^2)$; $\zeta=0{,}5$ cho $(1{,}5;\,0{,}75)$, $\zeta=-1$ cho $(3;\,-3)$.
  - Kì vọng $(2,-1)$: không chệch; phương sai $1$ và $4+2-0=6$.
  - Ước lượng gradient log cho $\partial_\mu$: kì vọng $2$, phương sai $29{,}027$, gấp khoảng $29$ lần.
- **Ghi chú diễn giả:** $\Phi=\mathbb R\times(0,\infty)$ mở; KL tới tiên nghiệm có dạng đóng. Phương sai thành phần thứ hai dùng $\operatorname{Var}\zeta^2=3-1=2$ và $\operatorname{Cov}(\zeta,\zeta^2)=\mathbb E\zeta^3=0$, nên $4\operatorname{Var}\zeta+\operatorname{Var}\zeta^2-4\operatorname{Cov}=6$. Kiểm điều kiện: $\kappa$ khả vi liên tục với mọi $\zeta$, nên $N_0=\varnothing$; trên $U=\{\lvert\mu\rvert\le1,\ \sigma\in[\tfrac12,2]\}$, hai đạo hàm bị chặn bởi $C(1+\zeta^2)$, khả tích; $\kappa$ là đa thức bậc hai theo $\zeta$, nên (iii) thỏa. Với $f(v)=-\tfrac12\ln(2\pi)-\tfrac12(2-v)^2$, ước lượng gradient log tại $(0,1)$ là $f(\zeta)\zeta$; phương sai $29{,}027$ tính từ $\mathbb E\zeta^4=3$, $\mathbb E\zeta^6=15$ (Phụ lục A(iv)). Kingma và Welling (§2.2) ghi nhận ước lượng gradient log có phương sai rất cao. Nguồn: ghi chú Bài 09, §9, Ví dụ 09.11; Phụ lục A(iv).
- **Lý do / nối:** trọng tâm trực quan 5: kiểm mệnh đề bằng số, so hai ước lượng trên cùng số liệu → phản ví dụ.
- **Mục tiêu / nguồn:** 5; Ví dụ 09.11.

#### `6-06` Ví dụ: hàm chỉ báo và biến Bernoulli — ví dụ, phản ví dụ bỏ điều kiện (i) (Ví dụ 09.12) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 09.12.** $q_\mu=N(\mu,1)$, $v=\mu+\zeta$, $f(v)=\mathbb 1[v>0]$: $F(\mu)=\Pr(\zeta>-\mu)$, $F'(0{,}5)\approx0{,}3521$.
  - Theo đường đi: $\partial_\mu\mathbb 1[\mu+\zeta>0]=0$ với mọi $\zeta\ne-\mu$; ước lượng bằng $0$ hầu chắc chắn, bị chệch.
  - (i) không thỏa: với $\zeta$ cố định, $\kappa$ nhảy tại $\mu=-\zeta\in\Phi$; không có tập ngoại lệ chung.
  - Khả vi tại từng $\mu$ cho hầu hết $\zeta$ chưa đủ.
  - Bernoulli: $q_\phi=\mathrm{Ber}(\phi)$, $v=\mathbb 1[U_0<\phi]$, $U_0$ đều trên $[0,1]$, $f(v)=v$: $F'=1$, theo đường đi $0$.
  - Gradient log $v/\phi$: kì vọng $1$, không chệch; phương sai $1/\phi-1\approx2{,}333$ tại $\phi=0{,}3$.
- **Ghi chú diễn giả:** Đạo hàm đúng là mật độ chuẩn tắc tại $\mu$, $e^{-\mu^2/2}/\sqrt{2\pi}$. Với mỗi $\mu$ cố định, $\kappa(\cdot,\zeta)$ vẫn khả vi tại $\mu$ cho hầu hết $\zeta$, nhưng tập ngoại lệ $\{-\mu\}$ thay đổi theo $\mu$, nên điều kiện (i) hỏng. Với biến Bernoulli, $F(\phi)=\phi$; ước lượng gradient log $f(v)\,\partial_\phi\ln q_\phi(v)=v/\phi$ có kì vọng $\phi\cdot\tfrac1\phi=1$. Câu hỏi cuối buổi (d) của ghi chú là phần Bernoulli này: ước lượng theo đường đi không cho ước lượng không chệch, còn ước lượng gradient log thì cho. Tái tham số hóa cần $f\circ g_\phi$ khả vi theo $\phi$ dọc từng đường nhiễu; với biến ẩn rời rạc, điều kiện này không thỏa. Nguồn: ghi chú Bài 09, §9, Ví dụ 09.12; §12, câu (d).
- **Lý do / nối:** phản ví dụ khi bỏ giả thiết (i), cùng chỗ hỏng của 6-03 → tiêu chí thứ hai cho mô hình sinh.
- **Mục tiêu / nguồn:** 5; Ví dụ 09.12.

#### `6-07` Ví dụ: độ hợp lý và chất lượng dữ liệu sinh ra — ví dụ (Ví dụ 09.13) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 09.13.** $D=N(0,I_p)$, $p=784$; $p_{\theta_1}=D$, $p_{\theta_2}=N(0,25I_p)$, hỗn hợp (mixture) $p_{\theta_3}=0{,}01\,p_{\theta_1}+0{,}99\,p_{\theta_2}$.
  - Theo $p_{\theta_3}\ge0{,}01\,p_{\theta_1}$: $1{,}4189\le L_D(\theta_3)/p\le1{,}4249$, so với $2{,}5484$ của $p_{\theta_2}$; $99\%$ dữ liệu sinh ra đến từ thành phần nhiễu.
  - Mô hình ghi nhớ (memorizing model), $50$ chuỗi DNA: mọi chuỗi sinh ra là chuỗi thật,
  - nhưng chuỗi kiểm tra mới có hàm lỗi log $+\infty$ với xác suất $\ge1-8{,}9\cdot10^{-44}$.
  - **Kết luận:** báo cáo riêng hai tiêu chí.
- **Ghi chú diễn giả:** Một mô hình sinh còn được dùng để rút điểm mới; mức giống dữ liệu thật của các điểm sinh ra là một tiêu chí khác hàm lỗi log. Bước 1: $-\ln p_{\theta_3}(x)\le-\ln p_{\theta_1}(x)+\ln100$ với mọi $x$, nên $L_D(\theta_3)\le L_D(\theta_1)+4{,}6052$. Giá trị $1{,}4189=\tfrac12\ln(2\pi e)$ là entropy vi phân của $D$ chia cho $p$, cũng là cận dưới của Mệnh đề 09.8(c). Điểm nhiễu có độ lệch chuẩn $5$ ở mỗi tọa độ thay vì $1$. Mô hình ghi nhớ đặt xác suất $\tfrac1{50}$ lên mỗi chuỗi huấn luyện của thí nghiệm DNA; một chuỗi có xác suất lớn nhất $\tfrac14\cdot0{,}6^{199}$, nên chuỗi mới trùng một chuỗi huấn luyện với xác suất không quá $8{,}9\cdot10^{-44}$. Tóm lại, hàm lỗi log gần tối ưu không bảo đảm dữ liệu sinh ra giống dữ liệu thật, và ngược lại; hai tiêu chí có thể xếp các mô hình theo hai thứ tự ngược nhau. Nguồn: ghi chú Bài 09, §9, Ví dụ 09.13 và đoạn sau.
- **Lý do / nối:** giới hạn của độ hợp lý như tiêu chí duy nhất (§10) → bài tập.
- **Mục tiêu / nguồn:** 2, 5; Ví dụ 09.13.

#### `6-08` Bài tập: SGD với gradient theo đường đi cho một mục tiêu lồi — bài tập (Bài tập 09.7(c), (d)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Nhắc lại:** (G2) $\mathbb E\lVert\varphi(w,\zeta)\rVert^2\le G^2$ trên $W$; Hệ quả 05.15: $\eta=R/(G\sqrt T)$ cho $\mathbb EF(\bar w_T)-\min_WF\le RG/\sqrt T$ khi mọi $u\in W$ có $\lVert w_1-u\rVert\le R$.
  - **Bài tập 09.7.** $F=-\operatorname{ELBO}$ của Ví dụ 09.10 theo $w=(\mu,\sigma)$; $W=[0,2]\times[\tfrac12,1]$, $w_1=(0,1)$; $\varphi=-\nabla_{\mu,\sigma}\kappa$.
  - (c) Tính $\mathbb E\lVert\varphi(w,\zeta)\rVert^2$ và giá trị lớn nhất trên $W$; suy ra $G$.
  - (d) $T=10^4$: tính $R$, độ dài bước, cận; cận này là kì vọng của KL nào?
  - [f] **Lời giải:** $\mathbb E\lVert\varphi\rVert^2=(5\mu^2-12\mu+8)+(7\sigma^2+1/\sigma^2-4)$, lớn nhất $12$ tại $(0,1)$: $G=2\sqrt3$.
  - [f] $R=\sqrt{4{,}25}\approx2{,}0616$, $\eta\approx0{,}00595$, cận $\sqrt{51}/100\le0{,}0715$ cho $\mathbb E\,\mathrm{KL}(q_{\bar w_T}\Vert p_\theta(\cdot\mid2))$; mô phỏng: $0{,}00014$.
- **Ghi chú diễn giả** (~200 âm tiết): Câu chữ đầy đủ của đề: "(c) Kiểm (G2): tính $\mathbb E\lVert\varphi(w,\zeta)\rVert^2$ và giá trị lớn nhất của nó trên $W$, rồi suy ra $G$. (d) Với $T=10^4$, tính $R$, độ dài bước và cận của Hệ quả 05.15 cho $\mathbb EF(\bar w_T)-\min_\Phi F$. Đại lượng này bằng kì vọng của phân kì KL nào? Một mô phỏng (Thuật toán 05.11 với độ dài bước trên, $20$ hạt giống) cho trung bình $0{,}00014$ của đại lượng này; so với cận." Ánh xạ oracle $\varphi$ dùng $\kappa$ của Ví dụ 09.11, nguồn ngẫu nhiên $\zeta\sim N(0,1)$, $\theta$ cố định. Hai ngoặc của $\mathbb E\lVert\varphi\rVert^2$ lồi, nên lớn nhất tại đầu mút: ngoặc đầu $8$ tại $\mu=0$, ngoặc sau $4$ tại $\sigma=1$. Kiểm tra: tại $(0,1)$, tổng các phương sai $1+6$ của Ví dụ 09.11 cộng $\lVert(-2,1)\rVert^2=5$ cho $12$. Điểm xa $w_1$ nhất là $(2,\tfrac12)$. Điểm cực tiểu $(1,1/\sqrt2)$ thuộc $W$, nên $\min_WF=\min_\Phi F=-\ln p_\theta(2)$, và $F(w)-\min F=\mathrm{KL}(q_w\Vert p_\theta(\cdot\mid2))$ theo Định lý 09.12(a). Mô phỏng nhỏ hơn cận khoảng $500$ lần; cận đúng cho mọi hàm lồi có cùng $R$, $G$. Phần (a), (b), (e) để về nhà; (e) cho thấy $G\to\infty$ khi $\sigma_0\to0$, và kết luận không chuyển sang việc học đồng thời $\theta$ và $\phi$ với mạng nơ-ron. Nguồn: tệp bài tập, Bài tập 09.7 và lời giải.
- **Lý do / nối:** bài tập của mạch 6 từ `exercises.md`, nối gradient theo đường đi với (G2) của Bài 05; câu nối sang mạch 7 ở tiêu đề mạch 7 → tiêu đề mạch 7.
- **Mục tiêu / nguồn:** 5; Bài tập 09.7(c), (d).

### Mạch 7. Tổng kết (7 trang, 10,5 phút)

#### `7-00` 7. Tổng kết — tiêu đề mạch, điểm vào mạch 7 · 0,5 phút
- **Mặt trang:**
  - "7."; h2 "Tổng kết"
  - Học một phân bố là tối thiểu hóa rủi ro thực nghiệm với hàm lỗi log; với chuỗi, cỡ mẫu là số chuỗi độc lập.
- **Ghi chú diễn giả:** Bài có hai đồng nhất thức tất định (quy tắc nhân xác suất, đồng nhất thức của cận dưới bằng chứng), hai kết quả tổng thể (rủi ro bằng entropy cộng phân kì KL, ước lượng hợp lý cực đại tổng thể và KL thuận), một kết quả trên tập huấn luyện cố định (thuật toán EM) và một kết quả theo kì vọng theo nhiễu phụ (gradient theo đường đi). Bảng tổng kết gom các giả thiết không được bỏ; sau đó là câu trả lời cho vấn đề trung tâm, một bài tập tổng hợp về cỡ mẫu và cận dưới cho xác suất, câu hỏi tự kiểm tra và bài tập về nhà. Nguồn: ghi chú Bài 09, §10–§13.
- **Lý do / nối:** mạch 6 → bảng tổng kết.
- **Mục tiêu / nguồn:** tất cả; §10–§13.

#### `7-01` Bảng tổng kết — tổng kết · 2 phút
- **Mặt trang (bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh`, trần 80, chữ trong ô có tính):**
  - Bảng: Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh; Mệnh đề 09.3, tất định: $p_1(x_{1:n})=\prod_jp_1(x_j\mid x_{<j})$ | (c): hàng tổng $1$ | giản ước; Mệnh đề 09.8, Hệ quả 09.9, tổng thể: $L_D=\mathrm H(p_D)+\mathrm{KL}(p_D\Vert p_\theta)$ | đếm được; $\mathrm H(p_D)<\infty$ | $\ln t\le t-1$; trừ hai đẳng thức; Định lý 09.12, tất định: $\ln p_\theta(x)=\operatorname{ELBO}+\mathrm{KL}(q\Vert p_\theta(\cdot\mid x))$ | $0<p_\theta(x)<\infty$; $p_\theta(x,v)>0$ $q$-hầu khắp nơi; khả tích | thêm bớt $\ln q$; Hệ quả 09.13, tất định: $L_s(\theta_{t+1})\le L_s(\theta_t)$ | $\mathcal V$ hữu hạn; $q_i$ hậu nghiệm; bước M hữu hạn | kẹp hai ELBO; Mệnh đề 09.15, kì vọng theo $\zeta$: $\nabla F=\mathbb E\nabla_\phi\kappa$ | (i) $N_0$ chung; hàm trội; khả tích | hội tụ bị chặn
- **Ghi chú diễn giả:** Mệnh đề 09.3 đúng với mọi phân bố trên $\mathcal A^n$; phần (c) cần mỗi hàng của bảng xác suất có điều kiện có tổng $1$. Mệnh đề 09.8 và Hệ quả 09.9 là kết quả tổng thể, kì vọng theo $D$, không có tập huấn luyện; Hệ quả 09.9 cho $\arg\min_\Theta L_D=\arg\min_\Theta\mathrm{KL}(p_D\Vert p_\theta)$. Định lý 09.12 là đồng nhất thức cho từng $x$. Hệ quả 09.13 không chứa $L_D$ và không nói về cực tiểu toàn cục. Mệnh đề 09.15 cho gradient không chệch, không cho cận phương sai; $-\operatorname{ELBO}$ nói chung không thỏa (C). Không kết quả nào giả sử tính lồi. Hai bảo đảm cho cỡ mẫu hữu hạn của bài nằm ngoài bảng: Ví dụ 09.4 (mô hình cố định có $c>0$, trên tập kiểm tra) và Bài tập 09.9 (ước lượng có hai quan sát giả). Nguồn: ghi chú Bài 09, §10.
- **Lý do / nối:** một hàng cho mỗi kết quả chính (Hệ quả 09.9 gộp với Mệnh đề 09.8 để giữ trần 80) → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §5–§9.

#### `7-02` Vấn đề trung tâm — tổng kết · 2 phút
- **Mặt trang:**
  - Học một phân bố: ERM với hàm lỗi log, $L_D=\mathrm H(p_D)+\mathrm{KL}(p_D\Vert p_\theta)$.
  - Học một chuỗi: tổng theo kí tự; cỡ mẫu là số chuỗi.
  - Cỡ mẫu hữu hạn: cận Hoeffding (xác suất $\ge1-\delta$) cần mọi xác suất $\ge c>0$.
  - Biến ẩn: khe ELBO bằng KL tới hậu nghiệm; gradient theo đường đi cần (i)–(iii).
  - Chuỗi thời gian: cần thêm giả thiết về sự phụ thuộc.
- **Ghi chú diễn giả:** Trả lời cho câu hỏi "học một phân bố xác suất và học một chuỗi như thế nào". Học một phân bố là ERM với hàm lỗi log, tức ước lượng hợp lý cực đại; ở mức tổng thể, giá trị tốt nhất là entropy và phần vượt là phân kì KL thuận, khi $\mathrm H(p_D)<\infty$. Với chuỗi, hàm lỗi là tổng các hàm lỗi có điều kiện, nhưng quan sát độc lập là cả chuỗi: với $50$ chuỗi, bán kính Hoeffding theo kí tự là $0{,}5754$, với xác suất ít nhất $1-\delta$ theo tập kiểm tra, cho $\lvert L_V(\theta)-L_D(\theta)\rvert/n$. Ước lượng hợp lý cực đại không chính quy hóa có $\mathbb E_SL_D(\hat\theta)=+\infty$ với mọi $m$ trong Ví dụ 09.7. Với cửa sổ chồng lấn, chia ngẫu nhiên cho MSE $0{,}20$ dưới rủi ro nhỏ nhất $1$. Nguồn: ghi chú Bài 09, §10.
- **Lý do / nối:** trả lời vấn đề trung tâm cho cả bài, giữ "xác suất $\ge1-\delta$" và điều kiện $c>0$ (bài học deck 02) → bài tập tổng hợp.
- **Mục tiêu / nguồn:** tất cả; §10.

#### `7-03` Bài tập: phạm vi kết luận của lỗi kiểm tra theo kí tự — bài tập tổng hợp (Bài tập 09.6(b)), lời giải trên mặt trang · 3 phút (1 phút tự làm) — sau duyệt tách thành 7-03 (đề) và 7-04 (lời giải), mục 17
- **Mặt trang:**
  - **Bài tập 09.6.** Làm trơn, $m=50$ (Ví dụ 09.8), mọi xác suất $\ge0{,}087$; $200$ chuỗi kiểm tra, $n=200$.
  - (b) $\delta=0{,}05$: bán kính Hoeffding, cỡ mẫu (Ví dụ 09.4); kết luận được phép?
  - [f] **Lời giải:** mô hình cố định với tập kiểm tra; cỡ mẫu $200$ chuỗi, không phải $40\,000$ kí tự:
  - [f] $$\ln(1/0{,}087)\sqrt{\ln(2/\delta)/(2\cdot200)}\approx2{,}4418\cdot0{,}09603\le0{,}2345$$
  - [f] Chỉ cho thiết lập này; không cho phân bố khác, mạng nơ-ron, Thiết lập B.
- **Ghi chú diễn giả** (~200 âm tiết): Câu chữ đầy đủ của đề: "(b)(i) Với $\delta=0{,}05$, dùng cách của Ví dụ 09.4 để tính bán kính tin cậy Hoeffding cho lỗi kiểm tra của một mô hình làm trơn học với $m=50$. Cỡ mẫu trong cận là bao nhiêu? So bán kính với độ lệch chuẩn qua hạt giống. (ii) Nêu những kết luận các số trên cho phép và những kết luận chúng không cho phép." Lỗi kiểm tra là hàm lỗi log trung bình theo kí tự trên tập kiểm tra. Mô hình được học trước khi rút tập kiểm tra. Mỗi số hạng thuộc $[0,\ln(1/c)]$ với $c=0{,}087$, $\ln(1/0{,}087)\approx2{,}4418$. Bán kính $0{,}2345$ lớn hơn khoảng $57$ lần độ lệch chuẩn (standard deviation) $0{,}0041$ qua mười hạt giống; cận đúng với mọi phân bố có hàm lỗi trong đoạn đó, nên nó lỏng với xích Markov này. Kết luận được phép: trong thiết lập của Phụ lục C, lỗi kiểm tra của mô hình làm trơn tiến về giá trị tốt nhất $1{,}0904$ khi $m$ tăng, và hiệu với mô hình thật giảm từ $0{,}0316$ ở $m=1$ xuống $0{,}00008$ ở $m=500$. Không được phép: các số là kết quả thí nghiệm cho một thiết lập, không phải chứng minh; chúng không cho tốc độ giảm với phân bố khác, với lớp mô hình không chứa phân bố thật, với mạng nơ-ron hay với Thiết lập B. Nguồn: tệp bài tập, Bài tập 09.6(b) và lời giải; ghi chú Bài 09, Phụ lục C.
- **Lý do / nối:** bài tập tổng hợp từ `exercises.md` ghép mạch 3 (cỡ mẫu), mạch 4 (làm trơn, giá trị tốt nhất) và giới hạn của §10; câu chữ rút gọn (mục 11, điểm 6) → tự kiểm tra.
- **Mục tiêu / nguồn:** 3; Bài tập 09.6(b).

#### `7-05` Câu hỏi tự kiểm tra — tổng kết · 2 phút
- **Mặt trang:**
  - 1. Tính độ hợp lý, hàm lỗi log và độ bối rối của $\mathtt{BBA}$ (bảng câu hỏi mở đầu).
  - 2. Chuỗi $10^4$ ngày, cửa sổ $30$ ngày, chia ngẫu nhiên $80\%/20\%$: Hệ quả 02.10 có cho khoảng tin cậy không?
  - 3. $q_\phi=N(0{,}8;\,0{,}5)$ tại $x=2$, $\operatorname{ELBO}=-2{,}3055$: tính KL tới hậu nghiệm; đổi $q_\phi$ có đổi $\ln p_\theta(2)$ không?
  - 4. Bước nào của chứng minh Mệnh đề 09.8 dùng $\mathrm H(p_D)<\infty$?
- **Ghi chú diễn giả** (câu trả lời dự kiến, chỉ dùng ghi chú): (1) Chuỗi đo hằng ngày; câu hỏi gốc hỏi thêm hàm lỗi log trung bình theo kí tự. Theo Mệnh đề 09.3, $\tfrac25\cdot\tfrac25\cdot\tfrac35=0{,}096$; hàm lỗi log $0{,}9163+0{,}9163+0{,}5108=2{,}3434$; chia cho $3$ được $0{,}7811$; độ bối rối $e^{0{,}7811}\approx2{,}184$. (2) Không: đích của một cửa sổ kiểm tra nằm trong ngữ cảnh của các cửa sổ huấn luyện kề nó, nên (T7) không thỏa (Ví dụ 09.5); chia theo thời gian bỏ được rò rỉ, nhưng các cửa sổ kiểm tra vẫn phụ thuộc nhau (Thiết lập B), nên cần thêm giả thiết về sự phụ thuộc. (3) Theo Định lý 09.12(a), $\mathrm{KL}=-2{,}2655+2{,}3055=0{,}0400$; $\ln p_\theta(2)$ chỉ phụ thuộc mô hình và $x$, nên đổi $q_\phi$ chỉ đổi khe. (4) Bước cộng hai tổng theo từng số hạng: tổng $\sum p_D(-\ln p_D)$ hữu hạn nên phép cộng hợp lệ. Nguồn: ghi chú Bài 09, §12 và lời giải; chứng minh Mệnh đề 09.8, Bước 2.
- **Lý do / nối:** bốn câu ngắn trả lời được chỉ bằng ghi chú; câu 1–3 là câu hỏi cuối buổi §12 (a)–(c) → bài tập về nhà.
- **Mục tiêu / nguồn:** 1–4; §12.

#### `7-06` Bài tập về nhà — tổng kết · 0,5 phút
- **Mặt trang:**
  - Bảng: Mục | Bài tập; 2. Hàm lỗi log và ước lượng hợp lý cực đại | 09.8; 3. Phân tích tự hồi quy và quan sát độc lập ở cấp chuỗi | 09.1, 09.2; 4. Entropy và phân kì Kullback–Leibler | 09.3, 09.5, 09.6, 09.9; 5. Mô hình biến ẩn và cận dưới bằng chứng | 09.10; 6. Tái tham số hóa và so sánh các mô hình sinh | 09.4, 09.7
  - Liên kết "Ghi chú bài giảng · Bài tập" (viewer `&deck=`).
- **Ghi chú diễn giả:** Mỗi bài xếp vào mạch cung cấp kiến thức cuối cùng bài đó cần. Bài tập 09.8 cần Định nghĩa 09.2 và hàm lỗi log của mật độ. Bài tập 09.1 cần Định nghĩa 09.4 và kí tự kết thúc; 09.2 cần Ví dụ 09.5 và Hệ quả 02.10. Bài tập 09.3 cần Mệnh đề 09.8 và Hệ quả 09.9; 09.5(c) cần Mệnh đề 09.8; 09.6(a)(ii) cần Mệnh đề 09.8(a) cho từng hàng; 09.9(c) cần Mệnh đề 09.8(a) và $\ln t\le t-1$. Bài tập 09.10 cần bước M của Hệ quả 09.13. Bài tập 09.4(d) và 09.7 cần Mệnh đề 09.15. Bảy bài đầu là bài gốc của học phần; 09.8, 09.9, 09.10 chọn từ UML (Bài tập 24.1–24.3), 09.10 tùy chọn; phần thực nghiệm của 09.6 là tùy chọn. Nguồn: ghi chú Bài 09, §11; tệp bài tập.
- **Lý do / nối:** giao bài tập theo mạch → tài liệu.
- **Mục tiêu / nguồn:** tất cả; §11.

#### `7-07` Tài liệu tham khảo — tổng kết · 0,5 phút
- **Mặt trang:**
  - Trước buổi học: UML §24.1, §24.1.2, §24.1.3.
  - Sau buổi học: UML §24.4, §24.4.1; Kingma và Welling (2014), §2.1–2.4, §3, Phụ lục B.
  - Mở rộng: UML §24.4.2, §24.2.
  - Shalev-Shwartz và Ben-David (2014). *Understanding Machine Learning: From Theory to Algorithms*. Cambridge University Press.
  - Kingma và Welling (2014). *Auto-Encoding Variational Bayes*. ICLR.
  - Bài 10: Gradient chính sách và học liên tục.
- **Ghi chú diễn giả:** UML §24.1: ước lượng hợp lý cực đại, §24.1.2 ước lượng hợp lý cực đại và ERM, §24.1.3 phân tích tổng quát hóa. Kingma và Welling: §2.1–2.4 cho cận biến phân và tái tham số hóa, Phụ lục B cho KL Gauss dạng đóng. UML viết $\log$ và cực đại hóa log độ hợp lý; ở đây viết $\ln$ và tối thiểu hóa hàm lỗi log. Trong cả bài, dữ liệu đến từ một phân bố $D$ cố định; phân bố lấy kì vọng duy nhất phụ thuộc tham số là phân bố biến phân, do thuật toán chọn. Bài 10 hỏi điều gì thay đổi khi hành động của một tác tử quyết định quan sát tiếp theo, và khi phân bố dữ liệu thay đổi theo thời gian. Nguồn: ghi chú Bài 09, §12 đoạn cuối, §13 và quan hệ với nguồn.
- **Lý do / nối:** trang cuối; dòng chữ Bài 10 (không liên kết cho đến khi deck Bài 10 có tên tệp).
- **Mục tiêu / nguồn:** —; §13.

## 7. Hành trình khái niệm

Thứ tự bước theo quy định: vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh (trang riêng) → kỹ thuật hoặc kiểm tra. Các bước có thể chung trang nhưng không đảo thứ tự trên mặt trang. Theo cổng duyệt Bài 04 (T5), ví dụ đặt trước phát biểu khi số liệu của nó không cần chính kết quả đó; ví dụ của ghi chú dùng kết quả để kiểm tra thì đứng sau, ở cột cuối.

| Kết quả hoặc khái niệm | Vấn đề | Trực quan | Ví dụ | Phát biểu | Ý tưởng chứng minh | Kỹ thuật / kiểm tra | Gộp, `không áp dụng`, lý do |
|---|---|---|---|---|---|---|---|
| Định nghĩa 09.1 (hai thiết lập lấy mẫu) | 1-06 (câu hỏi $m$ chuỗi và $3m$ quan sát) | 2-02 dòng 1 (kí tự phụ thuộc: $0{,}7\ne0{,}4$) | 2-02 (Ví dụ 09.1) | 2-02 | `không áp dụng` (định nghĩa) | 3-06, 3-07 (cỡ mẫu là số chuỗi), 3-08 (Thiết lập B) | Ví dụ 09.1 (§3) đứng trên trang Định nghĩa 09.1 (§1), dòng đầu, để không mở khái niệm bằng định nghĩa (mục 11, điểm 5). |
| Định nghĩa 09.2 (MLE là ERM) | 1-06 (hàm lỗi log của nhãn và của chuỗi), 2-04 dòng 1 | ghi chú diễn giả 2-04 (điều kiện tổng bằng $1$) | 2-05 (Ví dụ 09.2) | 2-04 | `không áp dụng` | 2-05 dòng cuối ($m_1=0$, $+\infty$); 2-06 (Bài tập 09.8(c)) | Ví dụ 09.2 dùng thuật ngữ MLE, nên đứng sau định nghĩa như ghi chú. |
| Mệnh đề 09.3 | 3-01 dòng 1 ($4^{200}-1$ tham số) | 3-01 ("Trực quan.": phân lớp kí tự kế tiếp) | 1-06 ($\mathtt{ABB}$: $1{,}784=0{,}511+0{,}357+0{,}916$) | 3-01 | 3-02 | 3-02 ("Kỹ thuật.": tổng theo kí tự cuối; hàng $(0{,}5;\,0{,}7)$ ở ghi chú diễn giả); 3-03 (Ví dụ 09.3); 3-04 (Bài tập 09.1) | Vấn đề, trực quan, phát biểu chung trang; ví dụ dẫn nhập ở 1-06. |
| Định nghĩa 09.4 (mô hình tự hồi quy, độ bối rối) | 3-02 bước 4 (mọi họ xác suất có điều kiện cho một hàm xác suất) | ghi chú diễn giả 3-03 (nghịch đảo trung bình nhân) | 3-03 (Ví dụ 09.3: $1{,}8123<2$) | 3-03 | `không áp dụng` | 3-04 (Bài tập 09.1(a): $2{,}6591$; $1{,}6719$) | Ví dụ 09.3 cần độ bối rối, nên đứng sau định nghĩa trên cùng trang. |
| Quan sát độc lập ở cấp chuỗi (§6, Ví dụ 09.4) | 3-04 (c) ($x_3$ phụ thuộc $x_1$) | 3-06 dòng 1–2 (tổng phụ thuộc; Định lý 02.7 chỉ ở cấp chuỗi) | 3-06, 3-07 (Ví dụ 09.4) | `không áp dụng` (đoạn văn, không khối kết quả) | `không áp dụng` | 3-07 (bảng ba cách đếm: $0{,}5754$; $\le0{,}05$ với $6622$; $0{,}0407$); 7-03 (Bài tập 09.6(b)) | Ghi chú không đánh số đoạn này; ví dụ mang kết luận. |
| Ví dụ 09.5 (rò rỉ thông tin) | 2-02 (Thiết lập B) | 3-08 dòng 2 và hình F1 (cửa sổ chung $9$ giá trị) | 3-08 | `không áp dụng` | `không áp dụng` | 3-08 dòng cuối ((T7) không thỏa); 7-04 câu 2 | — |
| Định nghĩa 09.6 | 3-09 dòng 1 (độ dài thay đổi, Nhận xét 09.5) | ghi chú diễn giả 3-09 (trọng số $1/n$ mỗi kí tự) | 3-09 (Ví dụ 09.6: $\tfrac16$ và $\tfrac12$) | 3-09 | `không áp dụng` | Bài tập 09.5 (về nhà) | Ví dụ dùng hai hàm lỗi, nên đứng sau định nghĩa trên cùng trang. |
| Mệnh đề 09.8 | 4-01 dòng 1 ($L_D$ phụ thuộc $D$ chưa biết), 1-06 ghi chú diễn giả | 4-02 ("Trực quan.": trả thêm $\ln(p_D/p_\theta)$; vô hạn khi bỏ sót điểm của giá) | 4-01 (KL không đối xứng: $0{,}0226$; $0{,}0216$) | 4-02 | 4-03 | 4-03 ("Kỹ thuật.": $\ln t\le t-1$); 4-05 ($0{,}6109<0{,}6730<0{,}6956$); 4-08 (Bài tập 09.3) | Trực quan và phát biểu chung trang. |
| Hệ quả 09.9 | 4-02 (Bảo đảm (b): $L_D\ge\mathrm H(p_D)$) | ghi chú diễn giả 4-04 (nhắm tới mô hình gần $p_D$ nhất) | 4-07 (đặc tả đúng: lớp bigram chứa mô hình thật) | 4-04 | 4-04 dòng "Chứng minh." (một dòng; mục 11, điểm 2) | 4-08 (c) (chiều thuận loại mô hình bỏ một điểm của giá) | Hệ quả trực tiếp; không có trang ý tưởng chứng minh riêng. |
| Ví dụ 09.7 (rủi ro vô hạn) | 2-05 dòng cuối ($\ell(\hat\theta,1)=+\infty$), 4-05 | 4-06 (biến cố toàn số $0$ có xác suất dương với mọi $m$) | 4-06 | `không áp dụng` | `không áp dụng` | 4-07 ($+\infty$ ở $m=1$, $m=5$); 7-02 dòng 3 | Phản ví dụ khi bỏ cận dưới cho xác suất. |
| Định lý 09.12 | 5-00 ghi chú diễn giả (tích phân không tính được), 5-01 | 5-02 ("Trực quan.": đổi $q$ không đổi bằng chứng) | 5-01 (Ví dụ 09.9: bằng chứng, hậu nghiệm dạng đóng) | 5-02 | 5-03 | 5-03 (**Nhắc lại** $\ln t\le t-1$; "Kỹ thuật." thêm bớt $\ln q$); 5-04 (Ví dụ 09.10, hình F2); 5-06 (Bài tập 09.4(b)); 7-04 câu 3 | Định nghĩa 09.11, trực quan và phát biểu chung trang. |
| Hệ quả 09.13 (EM) | 5-05 dòng 1 (luân phiên theo $q$ và $\theta$) | ghi chú diễn giả 5-05 (bước E đặt khe bằng $0$, bước M nâng ELBO) | `không áp dụng` (ghi chú không có ví dụ số; Bài tập 09.10 về nhà) | 5-05 | 5-05 dòng "Chứng minh." và dãy ba quan hệ (mục 11, điểm 2) | — | Hệ quả của Định lý 09.12(b). |
| Mệnh đề 09.15 | 6-01 dòng 1 ($\nabla F\ne\mathbb E\nabla_\phi f=0$) | 6-01 dòng cuối ("Trực quan.": $\phi$ chỉ còn trong hàm dưới kì vọng) | 6-05 (Ví dụ 09.11, kiểm điều kiện) | 6-02 | 6-03 | 6-04 (trang "Kỹ thuật." riêng); 6-05 (phương sai $1$, $6$, $29{,}027$); 6-06 (Ví dụ 09.12, phản ví dụ bỏ (i)); 6-08 (Bài tập 09.7) | Ví dụ 09.11 dùng Mệnh đề 09.15 để kiểm điều kiện, nên đứng sau như ghi chú; trực quan ở trang định nghĩa liền trước. |
| Ví dụ 09.13 (hai tiêu chí) | 6-00 ghi chú diễn giả | ghi chú diễn giả 6-07 | 6-07 | `không áp dụng` | `không áp dụng` | 6-07 dòng "Kết luận:" | — |

Thời lượng theo mạch: 9 + 15,5 + 22,5 + 22 + 18 + 22,5 + 10,5 = 120 phút; 55 trang (deck cuối, mục 16).

## 8. Hình vẽ

Mọi hình là SVG trong `2627-1/img/lec-09/`, `role="img"`, có `<title>` và alt cụ thể; màu không là tín hiệu duy nhất (kiểu nét, kiểu tô và hình dạng điểm khác nhau; nhãn trực tiếp); chữ trong hình chỉ là nhãn trục, nhãn ô, số và nhãn ngắn (Unicode), không công thức; công thức và chú thích nằm ở `figcaption` (KaTeX). Chú thích nêu dữ liệu. Mọi số có nhãn trên hình cũng có trong chữ trên cùng trang. Trục chứa hết dữ liệu.

| Mã | Tệp | Trang | Nội dung và dữ liệu | Alt dự kiến |
|---|---|---|---|---|
| F1 | `cua-so-chong-lan.svg` | 3-08 | Một hàng $12$ ô cho $x_{j-10},\ldots,x_{j+1}$ (nhãn dưới ô: "j−10", …, "j", "j+1"). Ngoặc trên: cửa sổ $u_j$ = ngữ cảnh $x_{j-10},\ldots,x_{j-1}$ (khung liền) và đích $x_j$ (ô tô gạch chéo), nhãn "uⱼ: tập kiểm tra". Ngoặc dưới: cửa sổ $u_{j+1}$ = ngữ cảnh $x_{j-9},\ldots,x_j$ (khung đứt) và đích $x_{j+1}$, nhãn "uⱼ₊₁: tập huấn luyện". Dải chung $x_{j-9},\ldots,x_{j-1}$ có ngoặc nhãn "9 giá trị chung". Ô $x_j$ (gạch chéo) nằm ở cả đích của $u_j$ và cuối ngữ cảnh của $u_{j+1}$, nhãn "đích xⱼ". Số $9$ và $k=10$ có trên mặt trang (dòng 1–2). | "Một dãy mười hai giá trị liên tiếp của chuỗi, từ vị trí j−10 đến j+1. Cửa sổ kiểm tra u_j gồm mười giá trị ngữ cảnh và đích x_j. Cửa sổ huấn luyện u_{j+1} gồm mười giá trị ngữ cảnh kết thúc bằng x_j. Hai cửa sổ chung chín giá trị, và đích của cửa sổ kiểm tra là giá trị cuối trong ngữ cảnh của cửa sổ huấn luyện." |
| F2 | `elbo-theo-mu.svg` | 5-04 | Trục ngang $\mu\in[-0{,}5;\,2{,}5]$ (vạch từng $0{,}5$); trục dọc ELBO $\in[-4{,}8;\,-2{,}0]$ (vạch từng $0{,}5$). Đường ngang nét đứt tại $\ln p_\theta(2)=-2{,}2655$, nhãn "ln p(2) ≈ −2,2655". Hai parabol: $\sigma^2=\tfrac12$ (nét liền), $\operatorname{ELBO}=-2{,}2655-(\mu-1)^2$, chạm đường ngang tại $\mu=1$; $\sigma^2=1$ (nét chấm), $\operatorname{ELBO}=-2{,}4189-(\mu-1)^2$. Bốn điểm của bảng: $(0;\,-3{,}4189)$ và $(1;\,-2{,}4189)$ trên đường chấm (ô vuông rỗng), $(0{,}8;\,-2{,}3055)$ và $(1;\,-2{,}2655)$ trên đường liền (chấm tròn đặc). Mũi tên dọc hai đầu tại $\mu=0$ từ $-3{,}4189$ lên $-2{,}2655$, nhãn "khe 1,1534". Nhãn trực tiếp: "σ² = 1/2", "σ² = 1". Mọi số có nhãn đều có trong bảng hoặc dòng 4 của 5-04. | "Hai parabol úp của cận dưới bằng chứng theo trung bình μ của phân bố biến phân, với phương sai 1/2 (nét liền) và 1 (nét chấm), cùng đỉnh tại μ = 1. Đường ngang nét đứt là log bằng chứng −2,2655. Parabol phương sai 1/2 chạm đường ngang tại μ = 1, nơi phân bố biến phân bằng hậu nghiệm; parabol phương sai 1 luôn thấp hơn ít nhất 0,1534. Tại μ = 0 với phương sai 1, khoảng cách tới đường ngang là 1,1534." |

Cách dựng dữ liệu hình (không có số mới trên nhãn): F1 là sơ đồ của Ví dụ 09.5, Bước 1 với $k=10$, không có số đo. F2 vẽ công thức ELBO dạng đóng của Phụ lục A(iii) với $\sigma^2$ cố định: $\operatorname{ELBO}(\mu,\sigma)=-\tfrac12\ln(2\pi)-\tfrac12(2-\mu)^2-\tfrac12\mu^2-\sigma^2+\tfrac12+\ln\sigma$, rút gọn thành $-2{,}2655-(\mu-1)^2$ khi $\sigma^2=\tfrac12$ và $-2{,}4189-(\mu-1)^2$ khi $\sigma^2=1$ (khe $(\mu-1)^2$ và $0{,}1534+(\mu-1)^2$); bốn điểm có nhãn trùng bảng của Ví dụ 09.10 (tính lại ở `num.py`: tám giá trị của $\mu\in\{-0{,}5;0;0{,}5;0{,}8;1;1{,}5;2;2{,}5\}$ với $\sigma^2=\tfrac12$, khe đúng bằng $(\mu-1)^2$). Điều phối viên ghi cách dựng vào `review-log.md`.

## 9. Trang tổng kết

Chi tiết từng trang ở mục 6 (7-01 đến 7-06). Tóm tắt:
- **Bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh` (7-01):** năm hàng: Mệnh đề 09.3 (tất định); Mệnh đề 09.8 cùng Hệ quả 09.9 (tổng thể); Định lý 09.12 (tất định, từng $x$); Hệ quả 09.13 (tất định, tập huấn luyện cố định); Mệnh đề 09.15 (kì vọng theo $\zeta$). Phạm vi (không chứa $L_D$; không cận phương sai; $-\operatorname{ELBO}$ không lồi) và hai bảo đảm cho cỡ mẫu hữu hạn ở ghi chú diễn giả.
- **Vấn đề trung tâm (7-02):** năm câu trả lời cho cả bài: học một phân bố là ERM với hàm lỗi log, $L_D=\mathrm H+\mathrm{KL}$; học một chuỗi: tổng theo kí tự, cỡ mẫu là số chuỗi; cỡ mẫu hữu hạn: cận Hoeffding với xác suất ít nhất $1-\delta$ cần mọi xác suất $\ge c>0$; biến ẩn: khe bằng KL tới hậu nghiệm, gradient theo đường đi cần (i)–(iii); chuỗi thời gian cần thêm giả thiết về sự phụ thuộc.
- **Bài tập tổng hợp (7-03):** Bài tập 09.6(b), một trang, lời giải ở fragment. Lý do chọn: ghép cỡ mẫu ở cấp chuỗi (mạch 3), cận dưới cho xác suất của mô hình làm trơn (mạch 4), cách của Ví dụ 09.4 và giới hạn "thí nghiệm không phải chứng minh" của §10; đây là trọng tâm "vì sao dữ liệu chuỗi phá giả thiết độc lập" và "không chuyển kết quả hàm lỗi bị chặn" trên cùng một số liệu.
- **Câu hỏi tự kiểm tra (7-04):** bốn câu, câu trả lời dự kiến ở ghi chú diễn giả: (1) $\mathtt{BBA}$: $0{,}096$; $2{,}3434$; $0{,}7811$; $2{,}184$; (2) không, (T7) không thỏa, cần giả thiết về sự phụ thuộc; (3) $0{,}0400$, không đổi; (4) Bước 2 (cộng hai tổng).
- **Bài tập về nhà (7-05):** bảng `Mục | Bài tập` ánh xạ mười bài vào mạch 2–6 theo mạch cung cấp kiến thức cuối cùng: mạch 2: 09.8; mạch 3: 09.1, 09.2; mạch 4: 09.3, 09.5, 09.6, 09.9; mạch 5: 09.10; mạch 6: 09.4, 09.7; liên kết viewer.
- **Tài liệu tham khảo (7-06):** UML §24.1 (§24.1.2, §24.1.3) trước buổi học; UML §24.4, §24.4.1 và Kingma, Welling (2014) §2.1–2.4, §3, Phụ lục B sau buổi học; UML §24.4.2, §24.2 mở rộng; dòng chữ "Bài 10: Gradient chính sách và học liên tục".
- **Câu nối sang bài sau** (ghi chú diễn giả 7-06): dữ liệu của cả bài đến từ một $D$ cố định; Bài 10 hỏi điều gì thay đổi khi hành động của tác tử quyết định quan sát tiếp theo, và khi $D$ thay đổi theo thời gian.

## 10. Bảng thuật ngữ Việt–Anh của deck

Theo ghi chú và `thuat-ngu.md` (§11 "Bài 09"); tiếng Anh trong ngoặc ở lần dùng đầu trên trang nội dung (trang ghi ở cột cuối).

| Tiếng Việt | Tiếng Anh | Lần đầu trên mặt trang |
|---|---|---|
| mô hình sinh | generative model | 1-06 |
| kí tự | token | 1-06 |
| bảng chữ | alphabet | 2-01 |
| chuỗi thời gian | time series | 2-02 |
| độ dài ngữ cảnh | context length | 2-02 |
| tập kiểm tra | test set | 2-03 |
| độ hợp lý; log độ hợp lý | likelihood; log-likelihood | 2-04 |
| ước lượng hợp lý cực đại (MLE) | maximum likelihood estimation | 2-04 |
| phân tích tự hồi quy | autoregressive factorization | 3-01 |
| mô hình bigram | bigram model | 3-03 |
| độ bối rối | perplexity | 3-03 |
| học theo đáp án | teacher forcing | 3-03 |
| cửa sổ chồng lấn | overlapping windows | 3-08 |
| lỗi bình phương trung bình (MSE) | mean squared error | 3-08 |
| rò rỉ thông tin | leakage | 3-08 |
| kí tự kết thúc | end-of-sequence token | 3-09 |
| hàm lỗi tổng | total sequence loss | 3-09 |
| hàm lỗi chuẩn hóa theo độ dài | length-normalized loss | 3-09 |
| entropy chéo | cross-entropy | 4-01 |
| phân kì Kullback–Leibler (KL) | Kullback–Leibler divergence | 4-01 |
| giá | support | 4-01 |
| entropy vi phân | differential entropy | 4-01 |
| phân kì KL thuận | forward KL | 4-04 |
| đặc tả đúng | well-specified | 4-04 |
| làm trơn cộng một | add-one smoothing | 4-06 |
| xích Markov | Markov chain | 4-07 |
| quá khớp | overfitting | 4-07 |
| biến ẩn | latent variable | 5-01 |
| tiên nghiệm; hậu nghiệm | prior; posterior | 5-01 |
| bằng chứng | evidence | 5-01 |
| phân bố biến phân | variational distribution | 5-01 |
| cận dưới bằng chứng (ELBO) | evidence lower bound | 5-02 |
| số hạng tái tạo | reconstruction term | 5-02 |
| khe | gap | 5-04 |
| thuật toán EM | Expectation–Maximization | 5-05 |
| nhiễu phụ | auxiliary noise | 6-01 |
| tái tham số hóa | reparameterization | 6-01 |
| ước lượng gradient theo đường đi | pathwise gradient estimator | 6-01 |
| ước lượng gradient log | score-function estimator | 6-01 |
| hàm trội | dominating function | 6-02 |
| định lý giá trị trung bình | mean value theorem | 6-03 |
| định lý hội tụ bị chặn | dominated convergence theorem | 6-03 (mặt trang viết "(dominated convergence)"; người viết deck có thể viết đủ nếu dòng vừa 20 âm tiết) |
| hỗn hợp | mixture | 6-07 |
| mô hình ghi nhớ | memorizing model | 6-07 |

Chỉ ở ghi chú diễn giả (tiếng Anh trong ngoặc ở đó): độ hợp lý có điều kiện (conditional likelihood), mật độ liên hợp (joint density), entropy tương đối (relative entropy), đặc tả sai (misspecification), khối lượng điểm (point mass), cận dưới biến phân (variational lower bound), đối của log độ hợp lý (negative log-likelihood), độ lệch chuẩn (standard deviation). Đã có ở Bài 01–08, không nhắc tiếng Anh: rủi ro kì vọng, rủi ro thực nghiệm, hàm lỗi log, tối thiểu hóa rủi ro thực nghiệm (ERM), khoảng cách tổng quát hóa, rủi ro vượt mức, hạ gradient ngẫu nhiên (SGD), hạt giống ngẫu nhiên.

## 11. Rủi ro và điểm cần điều phối viên quyết định

1. **54 trang**, trên mục tiêu 45–52 và dưới trần 55 (lý do ở mục 3). Phương án về 52 trang: (a) bỏ trang 2-06 (Bài tập 09.8(c)); mạch 2 khi đó không có trang bài tập, và ý "với mật độ, $\inf L_s=-\infty$" chuyển vào ghi chú diễn giả 2-03; (b) gộp 3-06 và 3-07 thành một trang Ví dụ 09.4, bỏ dòng nguyên lý (dòng 1–2 của 3-06) vào ghi chú diễn giả; trang gộp ước khoảng $65$ âm tiết, phải cắt thêm dòng "Cần $c>0$". Khuyến nghị giữ 54: cả hai phương án làm mất ý trọng tâm (hàm lỗi log không bị chặn; quan sát độc lập ở cấp chuỗi).
2. **Hệ quả 09.9 và Hệ quả 09.13 không có trang "Ý tưởng chứng minh" riêng.** Ghi chú gọi cả hai là hệ quả; chứng minh của 09.9 là phép trừ hai đẳng thức, của 09.13 là dãy ba quan hệ dùng Định lý 09.12(b) hai lần. Mặt trang 4-04 và 5-05 có dòng "**Chứng minh.**" (nhãn hợp lệ), ghi chú diễn giả nêu chỗ dùng giả thiết. Nếu điều phối viên coi Hệ quả 09.13 là kết quả chính (UML §24.4.1 đặt EM ở trung tâm), thêm trang `5-06` "Ý tưởng chứng minh: thuật toán EM không làm giảm log độ hợp lý" (bốn bước: kiểm giả thiết tại $\theta_{t+1}$; Định lý 09.12(b); bước M và $\mathrm H(q_i)$; dấu bằng tại hậu nghiệm), đánh số lại 5-06 thành 5-07: 55 trang, cắt bù 2 phút ở 5-04 và 6-07.
3. **Một trang "Kỹ thuật." riêng (6-04 "Đổi chỗ đạo hàm và kì vọng").** Kiểm Bài 10 (sửa theo T6): Phụ lục A của Bài 10, chứng minh khẳng định của Nhận xét 10.5, viết "Như chứng minh Mệnh đề 09.15 ở Phụ lục B của Bài 09", với định lý giá trị trung bình và hội tụ bị chặn; tiên quyết của Bài 10 dẫn Mệnh đề 09.15. Các kỹ thuật khác chỉ là một dòng: $\ln t\le t-1$ (4-03, nhắc lại ở 5-03; Bài 10 không dùng KL, tìm "KL" trong ghi chú Bài 10: $0$ kết quả); tổng theo kí tự cuối (3-02); thêm bớt $\ln q$ (5-03). Ước lượng gradient log: Bài 10 dùng (Ví dụ 09.12, Bước 4) nhưng tự chứng minh đồng nhất thức gradient log (Bổ đề 10.3), nên trang kỹ thuật cho nó thuộc deck Bài 10; Bài 09 chỉ có định nghĩa (6-01). Quy tắc nhân xác suất: Bài 10 viết xác suất quỹ đạo là tích các thừa số; đây là Mệnh đề 09.3 (một kết quả có trang riêng), deck Bài 10 nhắc lại kết quả.
4. **Nhận xét 09.5 ở dòng đầu 3-09** (đầu §6), không ở cuối §5 như ghi chú. Lý do: trang 3-03 đã $55$ âm tiết; Định nghĩa 09.6 là chỗ đầu tiên dùng $\mathtt E$, và chính ghi chú dẫn "(Nhận xét 09.5)" trong định nghĩa đó. Mạch 3 vẫn là các mục liên tiếp §5–§6. Phương án khác: tách một trang Nhận xét 09.5 sau 3-03 (55 trang).
5. **Ví dụ 09.1 (§3) đứng trên trang Định nghĩa 09.1 (§1)**, dòng đầu, để không mở khái niệm bằng định nghĩa; số $0{,}7$, $0{,}4$ là của bảng câu hỏi mở đầu, và $0{,}58$ ở ghi chú diễn giả. Khối ứng dụng chuỗi DNA (§3) ở ghi chú diễn giả 2-01 và trên mặt trang 4-07 (Ví dụ 09.8 trả lời ba câu hỏi thực hành).
6. **Câu chữ bài tập rút gọn trên mặt trang** (giữ đủ dữ kiện, câu hỏi và kết quả; câu đầy đủ ở ghi chú diễn giả, theo tiền lệ Bài 08): 2-06 (câu cuối của 09.8(c) viết "Nối với hàm lỗi log của mật độ (§2 của ghi chú)"); 3-04 (09.1(a): "tính … hàm lỗi log trung bình theo kí tự" thành "theo kí tự"; tiêu đề cột "Trước"); 4-08 (09.3(b), (c) gộp thành một dòng tính; "Ước lượng hợp lý cực đại tổng thể" thành "MLE tổng thể"); 5-06 (09.4(b) gộp ba câu); 6-08 (09.7(c), (d): bỏ "Kiểm (G2):", câu so với mô phỏng chuyển vào lời giải); 7-03 (09.6(b)(i), (ii) gộp một câu; câu "So bán kính với độ lệch chuẩn qua hạt giống" chỉ ở ghi chú diễn giả, mặt trang đã $59$).
7. **Bài tập tổng hợp: Bài tập 09.6(b).** Phương án khác: Bài tập 09.9(c) (cận $B_m$ với xác suất ít nhất $1-\delta$ cho rủi ro vượt mức với hàm lỗi log của ước lượng có hai quan sát giả: $1{,}279$; $0{,}4815$; $0{,}1810$), là bảo đảm cho cỡ mẫu hữu hạn thứ hai của §10 và là một lập luận mới cho hàm lỗi không bị chặn; nhưng lời giải dài sáu bước, không vừa một trang. Khuyến nghị 09.6(b).
8. **Trang bài tập mạch 6 cần nhắc lại Bài 05** ((G2), Hệ quả 05.15 trên mặt trang 6-08, dòng "Nhắc lại:"). Ghi chú không liệt kê Hệ quả 05.15 trong Kiến thức tiên quyết (mục 13). Phương án khác: Bài tập 09.4(d) (biến ẩn rời rạc, kì vọng của ước lượng theo đường đi $0\ne1$), ngắn hơn nhưng trùng ý Ví dụ 09.12, Bước 4.
9. **Mật độ** (đếm bằng script, mục 15): không trang nội dung nào vượt $60$; 1-03 $80$/80; 7-01 $73$/80 kể cả chữ trong ô; 7-05 $61$/80. Trung vị $53$ trên 42 trang nội dung (bỏ tổng quan, tiêu đề mạch, 1-03, 7-01, 7-05): trên mục tiêu $50$, dưới $54$–$55$ của Bài 06–08. Các trang $57$–$60$ (3-01, 4-08, 5-02, 5-05, 6-01, 7-02, 7-03, 7-04, 7-06) là trang kết quả giữ đủ giả thiết của ghi chú (Mệnh đề 09.3 ba phần, Định lý 09.12 bốn thành phần, Hệ quả 09.13 ba thành phần), trang bài tập giữ đủ dữ kiện, và trang tổng kết giữ loại bảo đảm. Văn xuôi giải thích đã chuyển vào ghi chú diễn giả. Người sửa sau năm báo cáo duyệt còn biên $0$–$3$ âm tiết ở các trang này: mọi bổ sung phải đi kèm một cắt.
10. **Kỹ thuật "Đảo cận đuôi thành bán kính và cỡ mẫu" (Bài 02, `L02-4-04`)** dùng ở 3-07 (cỡ mẫu $6622$ chuỗi) mà không có dòng "Nhắc lại:" trên mặt trang (3-07 đã $52$, dòng này thêm $10$); ghi chú diễn giả 3-07 nêu phép đảo. Nếu điều phối viên muốn nhắc tên trên mặt trang, thay dòng 1 của 3-07 bằng "**Nhắc lại:** đảo cận đuôi thành cỡ mẫu (Bài 02); bán kính theo kí tự không giảm khi $n$ tăng." và chuyển công thức bán kính vào bảng.
11. **Chuỗi phụ thuộc yếu.** Ghi chú không có cận tập trung cho Thiết lập B; deck không thêm giả thiết trộn, hệ số phụ thuộc hay cận nào. Mọi chỗ (2-02, 3-08, 7-02, 7-04 câu 2) viết đúng câu của ghi chú: "cần thêm giả thiết về sự phụ thuộc".
12. **Công thức cần đo ở 390 px** (ngắt `aligned` chỉ khi tràn): 1-06 (dòng hiển thị gồm hai đẳng thức, gần như chắc chắn cần ngắt), 2-01, 2-04, 3-06 (hai vế và định nghĩa $L_V$), 4-01, 5-02, 5-05 (dãy bốn vế, chắc chắn cần ngắt, một quan hệ mỗi dòng), 6-05 ($\kappa$), 7-03; bảng 1-06, 2-05, 3-04 (hai bảng), 3-07, 4-05, 4-06, 4-07, 4-08, 5-04, 5-06, 7-01, 7-05 trong `.table-scroll`.
13. **Trang có hình:** 3-08 (4 dòng, $56$ âm tiết, F1) và 5-04 (bảng năm cột cộng F2): người viết deck kiểm 1600×900 với `footer_check.py`; nếu chạm chân trang ở 5-04, đặt bảng và F2 trong `grid2`, hoặc chuyển dòng "Cực đại tại …" vào ghi chú diễn giả (F2 cho thấy điểm cực đại).
14. **Hai trang có "Trực quan." ở trang trước phát biểu:** Mệnh đề 09.15 có dòng "Trực quan." ở cuối 6-01 (trang định nghĩa liền trước), vì 6-02 đã $53$ với đủ ba điều kiện; hành trình không đảo thứ tự. Định lý 09.12 có "Trực quan." trên cùng trang 5-02.
15. **Câu hỏi tự kiểm tra 1–3** là câu hỏi cuối buổi §12 (a)–(c) của ghi chú; câu (d) là phần Bernoulli của Ví dụ 09.12, nằm ở ghi chú diễn giả 6-06. Câu 4 hỏi chỗ dùng giả thiết entropy hữu hạn (chứng minh Mệnh đề 09.8, Bước 2).
16. **"MLE"** dùng trên mặt trang 4-07 (tiêu đề cột) và 4-08 sau khi định nghĩa ở 2-04 ("ước lượng hợp lý cực đại (maximum likelihood estimation, MLE)"); tiêu đề và trang tổng quan viết đủ tên.
17. **"Nhãn" (a), (b), (c), (i)–(iii)** của kết quả và bài tập viết thường, không in đậm; `deck_lint.py` chỉ bắt chuỗi in đậm kết thúc bằng dấu chấm hoặc hai chấm.

## 12. Bảng đối chiếu trang → mục và khối của ghi chú

Cột "Đưa vào" ghi kí hiệu, thuật ngữ hoặc kết quả xuất hiện lần đầu trên mặt trang (định nghĩa hoặc "Nhắc lại:"/"Kí hiệu:"), để kiểm quy tắc định nghĩa trước khi dùng.

| Trang | Mục ghi chú | Khối (số của ghi chú) | Đưa vào |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §10 | — (bằng lời) | — |
| 1-02 | Kiến thức tiên quyết | Hệ quả 02.10(b), Nhận xét 02.11, Định lý 02.7 (Bài 02) | $L_D$, $L_S$, ERM (nhắc lại); $\delta$; (T1) (nhắc lại tên) |
| 1-03 | Mục tiêu học tập | — | — |
| 1-04 | các mục; §13 | — | — |
| 1-05 | đoạn mở đầu | — | — |
| 1-06 | Câu hỏi mở đầu | bảng câu hỏi mở đầu | kí tự $\mathtt A,\mathtt B$; mô hình sinh |
| 2-00 | §1–§4 | — | — |
| 2-01 | §1 | — | $\mathcal A$, $x_{1:n}$, $S$, $X^{(i)}$, $n_i$, $p_\theta$, $\Theta$, $\ell(\theta,x)$, $L_D(\theta)$, $L_S(\theta)$ |
| 2-02 | §1; §3 | Định nghĩa 09.1; Ví dụ 09.1 | Thiết lập A, B; $u_j$, $k$; chuỗi thời gian |
| 2-03 | §2 | danh sách giả thiết | (T2), (T3) (tên, đã có ở Bài 01–02), $c$, (T7), $V$, $m_v$, $\hat\theta$ |
| 2-04 | §4 | Định nghĩa 09.2 | $s$, $x^{(i)}$, $L_s$, độ hợp lý, MLE |
| 2-05 | §4 | Ví dụ 09.2 | $\mathrm{Ber}(\theta)$, $m_1$ |
| 3-00 | §5–§6 | — | — |
| 3-01 | §5 | Mệnh đề 09.3 | $x_{<j}$, $p_1$, $p_1(x_j\mid x_{<j})$ |
| 3-02 | Phụ lục D | chứng minh Mệnh đề 09.3 | $Q_j$ |
| 3-03 | §5 | Định nghĩa 09.4, Ví dụ 09.3 | ngữ cảnh bậc $k$, mô hình bigram, độ bối rối, học theo đáp án |
| 3-04 | `exercises.md` | Bài tập 09.1(a), (c) (đề) | $\pi_0$, $\pi$ (ghi chú diễn giả) |
| 3-05 | `exercises.md` | lời giải Bài tập 09.1(a), (c) | — |
| 3-06 | §6 | đoạn mở §6; Ví dụ 09.4, Bước 1–2 | $b$, $L_V$ |
| 3-07 | §6 | Ví dụ 09.4, Bước 3–5 | nat |
| 3-08 | §6; Phụ lục C | Ví dụ 09.5 | cửa sổ chồng lấn, MSE, rò rỉ thông tin |
| 3-09 | §5; §6 | Nhận xét 09.5; Định nghĩa 09.6; Ví dụ 09.6 | $\mathtt E$, $n(x)$, $\ell_{\mathrm{len}}$ |
| 4-00 | §7 | — | — |
| 4-01 | §7 | Định nghĩa 09.7 và đoạn sau | $\mathrm H$, $\mathrm h$, $\mathrm{KL}$, $p_1$, $p_2$, giá, $p_D$ |
| 4-02 | §7 | Mệnh đề 09.8 | — |
| 4-03 | §7 | chứng minh Mệnh đề 09.8 | — |
| 4-04 | §7 | Hệ quả 09.9 | $\theta^\star$, KL thuận, đặc tả đúng |
| 4-05 | §7 | câu hỏi và đoạn sau Hệ quả 09.9 | — |
| 4-06 | §7 | Ví dụ 09.7, Bước 3–4 | làm trơn cộng một |
| 4-07 | §7; §3; Phụ lục C | Ví dụ 09.8 | xích Markov, quá khớp |
| 4-08 | `exercises.md` | Bài tập 09.3(b), (c) | — |
| 5-00 | §8 | — | — |
| 5-01 | §8; Phụ lục A(ii) | Định nghĩa 09.10, Ví dụ 09.9 | $v$, $\mathcal V$, $p_\theta(x,v)$, tiên nghiệm, bằng chứng, hậu nghiệm, $q_\phi$, $\phi$, $\Phi$ |
| 5-02 | §8 | Định nghĩa 09.11, Định lý 09.12 | ELBO, $q$, số hạng tái tạo |
| 5-03 | §8 | chứng minh Định lý 09.12 | — |
| 5-04 | §8; Phụ lục A(iii) | Ví dụ 09.10 | khe |
| 5-05 | §8; Phụ lục D | Hệ quả 09.13 | EM, $q_i$, $\theta_t$, $\operatorname{ELBO}(\theta,q;x)$ (ghi chú diễn giả; mặt trang dùng trong dãy), $\mathrm H(q_i)$ |
| 5-06 | `exercises.md` | Bài tập 09.4(b) | — |
| 6-00 | §9 | — | — |
| 6-01 | §9 | Định nghĩa 09.14 | $F$, $f$, $\zeta$, $g_\phi$, $\mu_\phi$, $\sigma_\phi$, $\odot$, $I_r$ |
| 6-02 | §9 | Mệnh đề 09.15 | $\kappa$, $N_0$, $U$, $M$, (i)–(iii) |
| 6-03 | Phụ lục B | chứng minh Mệnh đề 09.15 | $e$, $\Delta$, $\partial_e$ |
| 6-04 | §9; Phụ lục B | — | — |
| 6-05 | §9; Phụ lục A(iv) | Ví dụ 09.11 | — |
| 6-06 | §9 | Ví dụ 09.12 | $U_0$, $\mathbb 1[\cdot]$ (đã có ở Bài 01) |
| 6-07 | §9 | Ví dụ 09.13 | $p_{\theta_1},p_{\theta_2},p_{\theta_3}$, hỗn hợp, mô hình ghi nhớ |
| 6-08 | `exercises.md`; Bài 05 | Bài tập 09.7(c), (d); Hệ quả 05.15 (nhắc lại) | $W$, $w$, $w_1$, $\varphi$, $G$, $R$, $T$, $\eta$, $\bar w_T$ |
| 7-00 | §10–§13 | — | — |
| 7-01 | §10 | mọi kết quả | — |
| 7-02 | §10 | — | — |
| 7-03 | `exercises.md`; Phụ lục C | Bài tập 09.6(b), đề | — |
| 7-04 | `exercises.md`; Phụ lục C | lời giải Bài tập 09.6(b) | — |
| 7-05 | §12 | câu hỏi cuối buổi (a)–(c) | — |
| 7-06 | §11 | `exercises.md` | — |
| 7-07 | §12 đoạn cuối, §13 | — | — |

Kiểm định nghĩa trước khi dùng: $p_D$ lên mặt trang lần đầu ở 4-01, với "(hàm xác suất của $D$)". (G2), Thuật toán 05.11 và (C) của Bài 05: (G2) nhắc lại ở 6-08; (C) chỉ ở ghi chú diễn giả 6-03. $\operatorname{ELBO}(\theta,q;x)$ dùng trong dãy của 5-05 với $q_i$ ở dòng bước E.

## 13. Đề xuất sửa ghi chú và tệp bài tập (không sửa; chờ điều phối viên và tác giả)

Không thấy lỗi toán học trong các khối deck dùng; mọi con số của ví dụ và bảy bài tập trên mặt trang đã tính lại (mục 5) và khớp ghi chú, tệp bài tập.

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất |
|---|---|---|---|---|
| nhẹ | ghi chú, Ví dụ 09.8, Bước 4 | "lỗi kiểm tra của nó cao hơn của mô hình thật khoảng $0{,}032$" không đọc được từ bảng của Bước 2 ($1{,}122-1{,}091=0{,}031$); con số $0{,}032$ đến từ trung bình hiệu theo hạt giống $0{,}0316$ của Bài tập 09.6 | ghi chú dòng 523; bảng dòng 514; `exercises.md` Bài tập 09.6, bảng hàng $m=1$; lời giải 09.6, "Kiểm tra lại" | Viết "khoảng $0{,}031$" (từ bảng) hoặc "khoảng $0{,}032$ khi lấy hiệu theo từng lần chạy"; deck (ghi chú diễn giả 4-07) không nêu con số này |
| nhẹ | ghi chú, Kiến thức tiên quyết, "Từ Bài 05" | Bài tập 09.7(d) dùng Hệ quả 05.15 và Thuật toán 05.11; danh sách chỉ nêu Định nghĩa 05.10, (G1), (G2), (C), Định lý 05.14 | ghi chú dòng 62; `exercises.md` Bài tập 09.7(d) | Thêm "độ dài bước theo số vòng lặp (Hệ quả 05.15)"; deck nhắc lại ở 6-08 |
| nhẹ | `exercises.md`, lời giải Bài tập 09.4(b) | $\rho_0$ chỉ được đặt tên ở Gợi ý 2; lời giải (mở mặc định độc lập với gợi ý) dùng $\rho_0$ không định nghĩa | `exercises.md` dòng 337 (Gợi ý 2) và 366 (lời giải, Bước 1) | Thêm "Gọi $\rho_0$ là mật độ của $N(0,1)$." vào đầu Bước 1 của lời giải (b); deck nêu ở ghi chú diễn giả 5-06 |

## 14. Danh sách kỹ thuật đã giới thiệu đến hết Bài 09

Danh sách của storyboard Bài 08 (mục 14), cột cuối thay bằng cách deck Bài 09 dùng; bốn dòng cuối là kỹ thuật mới của Bài 09.

| Kỹ thuật | Bài, trang (lần đầu) | Dạng | Trong deck Bài 09 |
|---|---|---|---|
| Tính tuyến tính của kì vọng | Bài 01, `L01-3-03` | một dòng | dùng không nhắc tên (ghi chú diễn giả 4-07: kì vọng hai vế của Mệnh đề 09.3(b)) |
| Bất đẳng thức hợp | Bài 01, `L01-4-04` | trang riêng | không dùng |
| Chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ | Bài 01, `L01-6-07` | trang riêng | không dùng |
| Tối thiểu hóa từng điểm rồi lấy kì vọng | Bài 01, `L01-5-09` | một dòng | không dùng |
| Phương pháp Chernoff | Bài 02, `L02-3-01` | trang riêng | không dùng |
| Dây cung của hàm lồi và Taylor bậc hai tại $0$ | Bài 02, `L02-3-03` | một dòng | không dùng |
| Đảo cận đuôi thành bán kính và cỡ mẫu | Bài 02, `L02-4-04` | trang riêng | dùng ở 3-07 (cỡ mẫu $6622$ chuỗi); ghi chú diễn giả 3-07 nêu phép đảo; dòng "Nhắc lại:" trên mặt trang là điểm mở (mục 11, điểm 10) |
| Chia xác suất thất bại cho từng giả thuyết | Bài 02, `L02-5-05` | trang riêng | không dùng |
| Bước tất định trên biến cố đại diện | Bài 02, `L02-5-11` | trang riêng | không dùng |
| Cận dưới và cận trên cho chiều VC | Bài 03, `L03-2-04` | trang riêng | không dùng |
| Đối xứng hóa và tập mẫu ảo | Bài 03, `L03-5-06` | trang riêng | không dùng |
| Hàm tăng trưởng thay cho số giả thuyết | Bài 03, `L03-5-07` | trang riêng | không dùng |
| Thêm bớt kì vọng rồi bình phương | Bài 04, `L04-3-03` | một dòng | không dùng |
| Chia xác suất thất bại theo trọng số | Bài 04, `L04-4-04` | trang riêng | không dùng |
| Lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện | Bài 04, `L04-6-02` | một dòng | không dùng |
| Kì vọng có điều kiện theo lịch sử | Bài 05, `L05-3-07` | trang riêng | không dùng ($\mathcal F_{t-1}$ không xuất hiện) |
| Tổng triệt tiêu và trung bình các điểm lặp | Bài 05, `L05-4-05` | trang riêng | gần với tích triệt tiêu ở 3-02 bước 1 (giản ước các biên), không nhắc tên |
| Cân hai số hạng, $a/\eta+b\eta\ge2\sqrt{ab}$ | Bài 05, `L05-4-08` | một dòng | không dùng |
| Số hạng chéo bằng $0$ cho véc-tơ không tương quan | Bài 05 | một dòng | không dùng |
| Lập luận đổi vai (thay một điểm) | Bài 06, `L06-4-05` | trang riêng | không dùng |
| Cộng hai bất đẳng thức tăng trưởng bậc hai đối xứng | Bài 06, `L06-5-02` | một dòng | không dùng |
| Điểm trên đoạn thẳng rồi cho dần về đầu mút | Bài 06, ghi chú diễn giả `L06-3-03` | một dòng | không dùng |
| Đưa hàm nhiều biến về một biến bằng các hàng trùng nhau của $\Theta_1$ | Bài 07, 2-05 | một dòng | không dùng |
| Đổi biến giữa dấu và nhãn ngẫu nhiên | Bài 07, 3-04 | một dòng | không dùng |
| Sai phân của một cận trên đúng không quá sai phân lớn nhất | Bài 07, ghi chú diễn giả 4-03 | một dòng | không dùng |
| Thay hàm lỗi 0–1 bằng hàm lỗi bị chặn, Lipschitz rồi dùng bổ đề co | Bài 07, 5-06 | một dòng | không dùng |
| Ghép cặp hai lần chạy rồi Jensen, $\lvert\mathbb E_\xi a-\mathbb E_\xi b\rvert\le\mathbb E_\xi\lvert a-b\rvert$ | Bài 08, 2-05 | một dòng ("Trực quan.") | không dùng |
| Hàm phụ $q_u=f-\langle\nabla f(u),\cdot\rangle$ cực tiểu tại $u$ (tính đồng bức từ tính lồi và tính trơn) | Bài 08, 2-09 | một dòng "Kỹ thuật." | không dùng |
| Bất đẳng thức trên từng quỹ đạo, rồi kì vọng chỉ qua xác suất biên $\Pr(i_t=i)$ | Bài 08, 3-02 bước 3–4 | một bước của ý tưởng chứng minh | không dùng |
| Đổi thứ tự lấy tổng ($\eta_k$ xuất hiện $T-k$ lần) | Bài 08, ghi chú diễn giả 4-05 | một câu | không dùng |
| **Lấy tổng theo kí tự cuối**, $\sum_{x_j}Q_j(x_{1:j})=Q_{j-1}(x_{<j})$ | **Bài 09, 3-02** | một dòng "Kỹ thuật." | dùng lại trong bài ở Bài tập 09.1(d) (về nhà) |
| **$\ln t\le t-1$, dấu bằng chỉ khi $t=1$** (tính không âm của phân kì KL) | **Bài 09, 4-03** | một dòng "Kỹ thuật." | nhắc lại một dòng ở 5-03; Bài tập 09.3(a), 09.4(a), 09.9(c), 09.10(b); Bài 10 không dùng |
| **Thêm bớt $\ln q(v)$ rồi lấy kì vọng theo $q$** | **Bài 09, 5-03** | một dòng "Kỹ thuật." | — |
| **Đổi chỗ đạo hàm và kì vọng** (định lý giá trị trung bình trên từng đường, hàm trội, hội tụ bị chặn) | **Bài 09, 6-04** | **trang riêng** | Bài 10 dùng lại (Nhận xét 10.5, Phụ lục A của Bài 10) |

Bài 09 có một trang "Kỹ thuật." riêng (6-04), vì ghi chú Bài 10 dùng lại lập luận của Phụ lục B. Ước lượng gradient log (Định nghĩa 09.14) là một định nghĩa; Bài 10 chứng minh đồng nhất thức gradient log (Bổ đề 10.3), nên trang kỹ thuật cho nó, nếu có, thuộc deck Bài 10 (mục 11, điểm 3).

## 15. Mật độ mặt trang đo bằng script

Đếm bằng `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-09/storyboard/count.py` trên văn bản dự kiến của mục 6, theo cách của `deck_lint.py`: token cách nhau bởi khoảng trắng, có chữ cái hoặc chữ số; bỏ tiêu đề, công thức `$…$`, chỉ dẫn `{{…}}`, dấu fragment; số viết trong câu có tính; trong dòng `Bảng:` chỉ token có chữ cái được tính (chữ trong ô có tính, số trong bảng không tính). Mỗi gạch đầu dòng hoặc mục đánh số là một dòng; mỗi công thức hiển thị là một dòng (số 0 trong cột theo dòng); một bảng là một dòng. Cột cuối là số âm tiết của ghi chú diễn giả theo cùng cách đếm.

**Số đo trên deck sau khi sửa** (2026-11-16, `deck_lint.py` và bản sao đếm theo trang của nó):

| Trang | Âm tiết mặt trang (kể cả chữ trong bảng) | Dòng | Ghi chú diễn giả |
|---|---:|---:|---:|
| 1-01 | 55 | 3 | 136 |
| 1-02 | 49 | 5 | 124 |
| 1-03 | 79 | 5 | 129 |
| 1-04 | 54 | 7 | 90 |
| 1-05 | 15 | 1 | 148 |
| 1-06 | 55 | 6 | 122 |
| 2-00 | (bìa hoặc tiêu đề mạch) | — | 92 |
| 2-01 | 52 | 5 | 140 |
| 2-02 | 60 | 4 | 133 |
| 2-03 | 60 | 5 | 142 |
| 2-04 | 57 | 6 | 97 |
| 2-05 | 7 | 5 | 109 |
| 3-00 | (bìa hoặc tiêu đề mạch) | — | 104 |
| 3-01 | 60 | 6 | 123 |
| 3-02 | 49 | 5 | 164 |
| 3-03 | 58 | 4 | 122 |
| 3-04 | 59 | 4 | 100 |
| 3-05 | 27 | 4 | 69 |
| 3-06 | 57 | 5 | 80 |
| 3-07 | 60 | 4 | 93 |
| 3-08 | 60 | 5 | 144 |
| 3-09 | 59 | 5 | 149 |
| 4-00 | (bìa hoặc tiêu đề mạch) | — | 107 |
| 4-01 | 47 | 5 | 91 |
| 4-02 | 60 | 5 | 108 |
| 4-03 | 42 | 5 | 169 |
| 4-04 | 53 | 5 | 87 |
| 4-05 | 52 | 5 | 98 |
| 4-06 | 32 | 5 | 134 |
| 4-07 | 55 | 6 | 145 |
| 4-08 | 59 | 5 | 60 |
| 5-00 | (bìa hoặc tiêu đề mạch) | — | 101 |
| 5-01 | 55 | 6 | 127 |
| 5-02 | 55 | 5 | 138 |
| 5-03 | 48 | 5 | 142 |
| 5-04 | 41 | 4 | 120 |
| 5-05 | 60 | 6 | 103 |
| 5-06 | 42 | 5 | 93 |
| 6-00 | (bìa hoặc tiêu đề mạch) | — | 101 |
| 6-01 | 60 | 6 | 140 |
| 6-02 | 59 | 5 | 88 |
| 6-03 | 59 | 5 | 181 |
| 6-04 | 55 | 4 | 128 |
| 6-05 | 40 | 6 | 82 |
| 6-06 | 45 | 5 | 105 |
| 6-07 | 60 | 6 | 117 |
| 6-08 | 56 | 5 | 155 |
| 7-00 | (bìa hoặc tiêu đề mạch) | — | 105 |
| 7-01 | 78 | 1 | 138 |
| 7-02 | 60 | 5 | 131 |
| 7-03 | 60 | 3 | 129 |
| 7-04 | 58 | 5 | 139 |
| 7-05 | 59 | 4 | 138 |
| 7-06 | 57 | 2 | 112 |
| 7-07 | 48 | 3 | 139 |

Kết quả: `deck_lint.py` 0 phát hiện; không trang nội dung nào vượt $60$ (1-03 $79$/80, 7-01 $78$/80); không trang nào quá $6$ dòng trừ 1-04 "Nội dung" (được miễn). Trên 43 trang nội dung (bỏ bìa, 1-03, 1-04, 1-05, tiêu đề mạch, 7-01, 7-06): trung vị $56$; 13 trang $\le50$, 9 trang $51$–$56$, 21 trang $57$–$60$. Ghi chú diễn giả trong trần ($150$; $250$ cho trang ý tưởng chứng minh, bài tập, lời giải); lớn nhất 6-03 $181$.

## 16. Deck cuối: các chỗ lệch storyboard và lý do (người viết deck, 2026-11-16)

Tệp `2627-1/lecture-09-hoc-chuoi-mo-hinh-sinh.html`, 55 trang; hình `img/lec-09/cua-so-chong-lan.svg` (F1, trang 3-08) và `img/lec-09/elbo-theo-mu.svg` (F2, trang 5-04), sinh bằng script trong thư mục nháp của người viết (`writer/gen_figs.py`; F2 vẽ từ công thức ELBO dạng đóng, có `assert` kiểm $-2{,}2655$, $-3{,}4189$, $-2{,}3055$). Mục 6, 12, 15 đã cập nhật mã trang; mặt trang cuối cùng là mặt trang trong deck, các mục 6 khác ở câu chữ theo bảng dưới. Mọi "yêu cầu sửa" và mười lăm phát hiện nhẹ của cổng duyệt (quyết định của điều phối viên trong `review-log.md`) đã áp dụng.

**Thay đổi chung.**
- **55 trang** (trần): thêm `3-05` (lời giải Bài tập 09.1); mã cũ 3-05…3-08 thành 3-06…3-09. Lý do: bảng đề ($5$ hàng) và bảng lời giải không vừa một khung 16:9 (`footer_check.py` báo 1021, 944, 913 px > 863 px với ba cách sắp xếp); tiền lệ `L08-7-04`/`L08-7-05`.
- Không dùng `.table-scroll` (lớp không có trong CSS); bảng rộng cuộn ngang tại chỗ ở màn hẹp theo `lecture-course.css`.
- Thuộc tính `style` tại chỗ: `colgroup` của 7-01 ($44/30/26\%$, để tiêu đề cột nằm một dòng, như `L08-7-01`) và `white-space:nowrap` ở năm chỗ (4-02, 4-07, 5-06, 7-01, 7-02) để tránh dấu câu hay "(iii)" rơi đầu dòng.
- Bốn trang "Bài tập" cuối mạch giữ lời giải trên mặt trang bằng `fragment`; mặt trang rút gọn câu chữ đề, câu đầy đủ ở ghi chú diễn giả (mục 11, điểm 6).

**Theo trang** (mã của deck cuối; "N1", "T…", "L…" là mã phát hiện của cổng duyệt).

| Trang | Lệch so với mục 6 | Lý do |
|---|---|---|
| 1-01 | Luận điểm: "Với hàm lỗi log, ước lượng hợp lý cực đại là tối thiểu hóa rủi ro thực nghiệm, và khi các chuỗi được rút độc lập, cỡ mẫu là số chuỗi."; ý KL ở ghi chú diễn giả | L14 |
| 1-02 | Thêm dòng (T1), (T2), (T3); Hệ quả 02.10(b) dẫn "(T1)–(T3)" | L2 |
| 1-03 | Mục 2 không dùng "ERM"; mục 5 "Dẫn ra gradient theo đường đi, điều kiện không chệch và một trường hợp chệch"; câu chữ các mục rút để giữ $80$ | L8 |
| 1-05 | Ghi chú: "cần xác suất của mô hình bị chặn dưới", cận cho mô hình cố định trên tập kiểm tra | L1, N1 |
| 1-06 | Bảng và hai công thức đặt cạnh nhau (`grid2`); câu hỏi rút gọn | chạm chân trang (922 px) |
| 2-00 | Ghi chú bỏ câu lộ trình "Trước hết … Sau đó" | L10 |
| 2-01 | Dòng 1 nêu $\mathcal X$: "$\mathcal A^n$ hoặc mọi chuỗi hữu hạn"; bỏ "(không nhãn)" ra ghi chú | L3; mật độ |
| 2-02 | Bỏ câu dẫn "Với bảng của ví dụ mở đầu"; dòng cuối giữ câu của ghi chú "cần thêm giả thiết về sự phụ thuộc" | mật độ ($75\to56$) |
| 2-03 | "Không bị chặn, trái (T3); cận Bài 02–04, 07 áp dụng khi mọi xác suất của mô hình rời rạc $\ge c>0$"; (T7) "mô hình được đánh giá $\hat\theta=\hat\theta(S)$" | L1, L2 |
| 2-04 | Tách "Log độ hợp lý (log-likelihood)" thành một dòng | dòng > 20 âm tiết |
| 3-00 | Ghi chú mở bằng nội dung, không "Mạch trước" | T10 |
| 3-01 | Thêm điều kiện $p_1(x_{<j})>0$, quy ước tích $=0$, vế sau của (c) viết bằng $Q_n$; "Trực quan." rút thành "Thừa số thứ $j$: phân lớp kí tự $j$"; $4^{200}-1$ ra ghi chú | T1 và cắt bù của T1 |
| 3-02 | Bước 4 rút gọn; ghi chú không chỉ vào "dòng Kỹ thuật." | cắt mục 6 cổng duyệt; T11 |
| 3-03 | Mở bằng "Theo Mệnh đề 09.3(c), mọi họ xác suất có điều kiện cho một mô hình."; dòng học theo đáp án ra ghi chú diễn giả (có "(teacher forcing)") | L11; cắt mục 6 |
| 3-04, 3-05 | Tách đề và lời giải; (c) lời giải viết đủ hai tổng trong một khối `aligned` | xem trên; T7 không liên quan |
| 3-06 | "DNA trên $\{\mathtt A,\mathtt C,\mathtt G,\mathtt T\}$"; "không phụ thuộc $V$" trên mặt trang; định nghĩa $L_V$ chuyển vào dòng chữ trước công thức | L11; N1; công thức tràn ngang 1600 px |
| 3-07 | Dòng 1 "**Nhắc lại:** đảo cận đuôi thành bán kính và cỡ mẫu (Bài 02)."; dòng "Cần $c>0$" ra ghi chú; cột cỡ mẫu ghi $m_v$, $m_vn$ | T5 |
| 3-08 | F1 trong `grid2` cạnh hai dòng; "lỗi bình phương trung bình (mean squared error, MSE)" | chạm chân trang; tên tiếng Việt trước chữ viết tắt |
| 3-09 | Dòng cuối "Điểm cực tiểu: $\tfrac16$ (tổng), $\tfrac12$ (chuẩn hóa)." | cắt mục 6 |
| 4-00 | Ghi chú bỏ câu "Mạch 3 … chưa cho biết" | T10 |
| 4-01 | KL viết trong dòng chữ (không công thức hiển thị); "có thể âm, $-\ln2$" ra ghi chú | cắt mục 6; chạm chân trang |
| 4-02 | "**Trực quan.** Xác suất nhỏ ở điểm hay xảy ra: hàm lỗi lớn; bỏ sót điểm của giá: rủi ro $+\infty$."; ghi chú nêu số hạng có thể âm, kì vọng là KL | T2; T11 |
| 4-06 | Bảng $0{,}99^m$ thành một dòng chữ | chạm chân trang |
| 4-07 | Dòng $m=500$ ra ghi chú; bảng và hai dòng trong `grid2` | cắt mục 6; chạm chân trang |
| 4-08 | Đề và bảng lời giải trong `grid2`; dòng "MLE tổng thể … thế nào?" gộp hai câu hỏi | chạm chân trang; mật độ |
| 5-01 | Dòng hậu nghiệm rút gọn | cắt mục 6 |
| 5-02 | ELBO trong dòng chữ; "**Trực quan.** $\ln p_\theta(x)$ không phụ thuộc $q$: tăng ELBO theo $q$ thu hẹp khoảng cách tới nó."; (c) viết "ELBO $=$ số hạng tái tạo … $-\mathrm{KL}$" | L4; mật độ ($68\to56$) |
| 5-03 | Bước 4 dẫn "(lập luận của Mệnh đề 09.8(b), (c))" | L5 |
| 5-04 | Dòng khe đặt trước bảng; công thức tái tạo và KL tới tiên nghiệm ra ghi chú; F2 lớp `short`, chú thích một dòng | L6; chạm chân trang |
| 5-05 | Dòng mở "Thuật toán EM (Expectation–Maximization), $\mathcal V$ hữu hạn: …"; Bảo đảm "không nói về $L_D$ hay cực tiểu toàn cục"; dãy ba quan hệ trong `aligned` hai dòng, `\sum\nolimits`; ghi chú "Bất đẳng thức thứ hai" | công thức tràn ngang; chạm chân trang; T11 |
| 5-06 | Tiêu đề "Bài tập: cận dưới bằng chứng của hỗn hợp Gauss"; dữ kiện "$v$ đều trên $\{1,2\}$" (cùng dữ liệu); lời giải trong `grid2` | tiêu đề hai dòng; chạm chân trang |
| 6-00 | Dòng dẫn "Viết lần rút thành hàm của nhiễu có phân bố cố định, đạo hàm vào được trong kì vọng khi hàm khả vi, khả tích." (24); ghi chú bỏ "Cuối mạch" | L7; LEAD25; L10 |
| 6-01 | Dòng 1 "$F(\phi)=\ldots$: $\nabla F$ nói chung khác $\ldots=0$: phân bố phụ thuộc $\phi$." | cắt mục 6 (giữ định nghĩa $F$) |
| 6-02 | (ii) có "$\zeta\notin N_0$" | L12 |
| 6-03 | Dòng cuối "Tập ngoại lệ phụ thuộc $\phi$: hợp theo $\phi$ có thể có xác suất dương."; ghi chú không "Dòng cuối" | T11; mật độ |
| 6-04 | "Điều kiện đủ: khả vi liên tục theo $\phi$ ngoài một tập $N_0$ chung; hàm trội khả tích; $\mathbb E\lvert\kappa\rvert<\infty$"; "Dùng khi … (Mệnh đề 09.15)" | T3 |
| 6-06 | Bỏ dòng "Khả vi tại từng $\mu$ … chưa đủ" (ở ghi chú) | cắt mục 6 |
| 6-07 | "Mệnh đề 09.8(c) và $p_{\theta_3}\ge0{,}01\,p_{\theta_1}$: …"; "**Kết luận:** báo cáo riêng độ hợp lý và chất lượng dữ liệu sinh ra." | T13; mật độ |
| 6-08 | Tiêu đề "Bài tập: SGD với gradient theo đường đi" (một dòng); "**Nhắc lại:** Hệ quả 05.15: dưới (C), (G1), (G2) $\mathbb E\lVert\varphi\rVert^2\le G^2$ và $\lVert w_1-u\rVert\le R$ trên $W$, …, $\bar w_T$ trung bình $T$ điểm lặp."; đề thêm "(C), (G1) thỏa theo (a), (b)"; (d) hỏi "$\mathbb EF(\bar w_T)-\min_\Phi F$ là kì vọng của KL nào?"; số mô phỏng $0{,}00014$ và $R\approx2{,}0616$ ra ghi chú | N2, L15, T14; chạm chân trang |
| 7-00 | Ghi chú chỉ giữ câu phân loại kết quả | L10 |
| 7-01 | Hàng "Định lý 09.12, tất định: …; Hệ quả 09.13: $L_s(\theta_{t+1})\le L_s(\theta_t)$" (một hàng), giả thiết EM "$\mathcal V$, bước M hữu hạn"; bốn hàng | T4 (gộp hàng) |
| 7-02 | Bốn dòng: "Phân bố: ERM với hàm lỗi log; $L_D=\ldots$ khi $\mathrm H(p_D)<\infty$"; "Chuỗi: … cỡ mẫu: số chuỗi; chuỗi thời gian cần thêm giả thiết về sự phụ thuộc"; "Cận Hoeffding (xác suất $\ge1-\delta$): mô hình cố định, mọi xác suất $\ge c>0$, trên $m_v$ chuỗi kiểm tra"; "Biến ẩn: khe $=\mathrm{KL}$ tới hậu nghiệm; gradient theo đường đi không chệch dưới (i)–(iii)" | N1, T12, T3; trần 60 |
| 7-03 | Lời giải: "cỡ mẫu $m_v=200$ chuỗi, mô hình cố định"; dòng cuối "Bán kính $\approx57$ lần độ lệch chuẩn; được phép: hiệu với mô hình thật giảm khi $m$ tăng, chỉ trong thiết lập này."; độ lệch chuẩn $0{,}0041$ trên dòng dữ kiện; phần "không được phép" (phân bố, lớp mô hình khác, mạng nơ-ron, Thiết lập B) và câu "200 chuỗi, không phải 40 000 kí tự" ở ghi chú diễn giả | T7; trần 60 (bản đủ câu là $97$) |
| 7-04 | Ghi chú câu 1 mở bằng "Theo Mệnh đề 09.3" | L9 |
| 7-05 | Giữ năm hàng, tên mạch đủ: $57$ âm tiết theo `deck_lint.py` | T9 đạt trần 60 không cần gộp hàng |
| 7-06 | "Mở rộng: UML §24.4.2, §24.2" chuyển vào ghi chú diễn giả | mật độ |
| mọi trang | Dòng `note-source` thêm mục UML ở mạch 2, 4, 5 | L13 |

**Kiểm tra máy trên deck cuối.** `deck_check.py`: console $0$, pageerrors $0$, failed $0$, không `.katex-error`; OVERFLOW còn ở 1-02, 2-03, 3-06, 3-07, 6-08, 7-03, đều là đuôi SVG của `\sqrt` (phần tử `path`, báo động giả đã biết); màn hẹp: `scrollWidth` của trang $390$ ở mọi trang (công thức, bảng cuộn tại chỗ). `footer_check.py`: $0$ trang. `deck_lint.py`: $0$ phát hiện. Bàn phím: →, ↓, Space, Esc (tổng quan) và liên kết `#/2`…`#/7` của trang "Nội dung" tới đúng trang tiêu đề mạch. Ảnh chụp 1600×900 và 390×844 (cả ảnh `-end`) đã xem.

**Còn để điều phối viên xem.** (1) Ở 390 px, chữ trên F1 và F2 nhỏ (hình co theo bề rộng cột); mọi số trên hai hình có trong chữ hoặc bảng cùng trang, như bài học deck 04. (2) 7-03: phần "kết luận không được phép" chỉ ở ghi chú diễn giả vì trần $60$; mặt trang nêu nghĩa dương có giới hạn "chỉ trong thiết lập này". (3) 6-08: (C), (G1) chỉ được gọi tên trên mặt trang, định nghĩa ở ghi chú diễn giả.

## 17. Sửa sau năm báo cáo duyệt (người sửa, 2026-11-16)

Đầu vào: `reviews/deck-{hoc-vien,toan-hoc,chuyen-gia,su-pham,mach-truyen}.md` và quyết định của điều phối viên trong `review-log.md` ("Năm báo cáo duyệt và quyết định của điều phối viên": chấp nhận mọi phát hiện). Mã trang dưới đây là mã của deck sau khi sửa. Mục 15 đã thay bằng số đo mới; mục 16 giữ lịch sử bản viết đầu.

**Thay đổi cấu trúc (55 trang, giữ trần).**
- **Bỏ trang 2-06** (Bài tập 09.8(c)), phương án (a) của mục 11, điểm 1. Lý do: bài tập tổng hợp 7-03 phải theo câu chữ `exercises.md` và có đủ hai vế của câu (ii); đề cộng lời giải là khoảng $80$ âm tiết, không vừa trần $60$, nên tách thành 7-03 (đề) và 7-04 (lời giải). Không còn trang nào gộp được mà không trái quy định. Nội dung của 2-06 ($\inf L_s=-\infty$ với mật độ Gauss và một quan sát) chuyển vào ghi chú diễn giả 2-05; Bài tập 09.8 vẫn ở bảng bài tập về nhà (mạch 2). Mạch 2 vì thế không có trang bài tập trên lớp: điểm để điều phối viên quyết định.
- **Tách 7-03** thành 7-03 (đề, câu chữ rút gọn thành câu đầy đủ theo đề xuất của người duyệt sư phạm) và 7-04 (lời giải, có cả kết luận được phép và không được phép). Mã cũ 7-04, 7-05, 7-06 thành 7-05, 7-06, 7-07.
- Mạch 2: 6 trang (2-00…2-05); mạch 3: 10 trang; mạch 7: 8 trang (7-00…7-07).

**Bảng xử lý từng phát hiện.**

| Báo cáo | Trang | Phát hiện | Xử lý |
|---|---|---|---|
| chuyên gia (nghiêm trọng) | 2-03 | cận Bài 02–04, 07 "khi mọi xác suất $\ge c$" quá rộng | đã sửa: "Với độ dài $n$ cố định, mọi xác suất có điều kiện $\ge c>0$ ($c$ chung cho lớp): $\ell\le n\ln(1/c)$. Khi đó cận Bài 02, 04, 07 cho hàm lỗi bị chặn áp dụng."; bỏ Bài 03; ghi chú: Định lý 03.15 chỉ cho hàm lỗi 0–1, độ dài thay đổi vẫn không bị chặn, cận cho mô hình cố định chỉ cần $c$ của nó |
| chuyên gia (nghiêm trọng) | 6-08 | tiêu đề bỏ "mục tiêu lồi"; thiếu $\theta$ cố định, một quan sát, độ chênh tối ưu, $-\operatorname{ELBO}$ không lồi | đã sửa: tiêu đề "Bài tập: SGD cho một mục tiêu lồi"; đề nêu "$\theta$ cố định, một quan sát $x=2$"; lời giải "độ chênh tối ưu, không phải $L_D$" và "Theo $(\theta,\phi)$, $-\operatorname{ELBO}$ nói chung không lồi" |
| toán học (nghiêm trọng) | 4-03 ghi chú | "chỗ duy nhất … dạng $\infty-\infty$" sai | đã sửa: Bước 2 dùng $\mathrm H<\infty$ để cộng theo số hạng; vế sau của (b) suy từ (a) vì $\mathrm H$ hữu hạn; bỏ giả thiết thì mọi mô hình có $L_D=+\infty=\mathrm H$, dấu bằng của (b) và phép trừ ở Hệ quả 09.9 mất nghĩa |
| toán học | 7-05 câu 4 | thiếu Bước 3 | đã sửa (ghi chú diễn giả: Bước 2 và vế sau của (b) ở Bước 3) |
| toán học | 6-04 | "khi phân bố không phụ thuộc $\phi$" như điều kiện đủ | đã sửa: "Với $\zeta$ có phân bố không phụ thuộc $\phi$: … khi:" (i), (ii), (iii) |
| toán học | 6-04 ghi chú | khái quát về hàm nhảy | đã sửa: chỉ nói cho hàm chỉ báo và biến Bernoulli của Ví dụ 09.12 ($0{,}3521$ và $1$) |
| toán học | 6-03 ghi chú | gradient ELBO thiếu điều kiện | đã sửa: "nếu mỗi $\kappa_i$ thỏa (i)–(iii) theo $(\theta,\phi)$" |
| toán học | 2-03 | thiếu độ dài cố định | đã sửa (cùng phát hiện nghiêm trọng) |
| toán học | 2-02 | thiếu $j=k+1,\ldots,n$, "nói chung"; thứ tự Ví dụ 09.1 | đã sửa hai ý đầu; thứ tự: không sửa (đã chốt ở mục 11, điểm 5) |
| toán học | 3-08 | "$=0{,}2$" thay "xấp xỉ" | đã sửa ($\approx$) |
| toán học | 3-09 ghi chú | trọng số $1/n$ và $D(x)/n(x)$; số hạng $\mathtt E$ | đã sửa |
| toán học | 4-02 (c) | "như trên" mơ hồ | đã sửa: $L_D=\mathrm h(p_D)+\mathrm{KL}$, $\mathrm{KL}\ge0$, $=0$ khi và chỉ khi … |
| toán học | 4-07 | $\ln4$ không giải thích; $0{,}0009$ | đã sửa: "kí tự đầu đều" trên mặt trang; công thức và nghĩa của $\ln4$, $1{,}0889$ ở ghi chú; $0{,}0009$ "tính từ trung bình chưa làm tròn" |
| toán học | 5-03 ghi chú | khối lượng điểm gán sai giả thiết | đã sửa: "khi mô hình liên hợp không có mật độ" |
| toán học | 5-04 | cột "KL" dễ nhầm | đã sửa: "KL tiên nghiệm" |
| toán học | F2 | nhãn $\ln p(2)$ | đã sửa: "ln pθ(2)" (SVG sinh lại) |
| toán học | 5-05 | kí hiệu $\operatorname{ELBO}(\theta,q;x)$ chỉ ở ghi chú | đã sửa: dòng 1 nêu $\operatorname{ELBO}(\theta,q;x)$, $q$ là hàm xác suất |
| toán học | 6-00 dòng dẫn | "khả vi, khả tích" chưa đủ | đã sửa: "khả vi liên tục trên từng đường nhiễu, có hàm trội và khả tích" |
| toán học | 7-01 | "$\mathcal X$ đếm được" không phải giả thiết không bỏ được | đã sửa: "$p_\theta$ tổng $1$; $\mathrm H(p_D)<\infty$ (mật độ: khả tích)" |
| chuyên gia | 7-02 | dòng Hoeffding thiếu $n$ cố định, đại lượng | đã sửa: "Với xác suất $\ge1-\delta$: $\lvert L_V(\theta)-L_D(\theta)\rvert\le n\ln(1/c)\sqrt{\ldots}$, $\theta$ cố định, $n$ cố định, mọi xác suất $\ge c>0$" |
| chuyên gia | 6-08 | (C), (G1) chỉ có tên; (C) cho thác triển | đã sửa: "Nhắc lại:" viết (C), (G1), (G2); đề "(C) cho thác triển lồi của $F$; (G1) thỏa"; ghi chú nêu $\tilde F$ |
| chuyên gia | 2-01 | cố định và ngẫu nhiên | đã sửa (ghi chú diễn giả, ba nhóm của §1) |
| chuyên gia | 3-01, 3-03 | đồng nhất thức và giả thiết mô hình | đã sửa: 3-03 "Ngữ cảnh bậc $k$ (giả thiết mô hình)"; ghi chú 3-01 |
| chuyên gia | 3-08 | chia theo thời gian không cho khoảng tin cậy | đã sửa: "Chia theo thời gian: $0{,}994$; cửa sổ kiểm tra vẫn phụ thuộc nhau"; câu Hệ quả 02.10 ở ghi chú (trần $60$) |
| chuyên gia | 3-09 | cực tiểu của $\ell_{\mathrm{len}}$ trên mọi phân bố | đã sửa (ghi chú diễn giả) |
| chuyên gia | 4-07 | $1{,}088<1{,}0904$ | đã sửa: dòng "$m=500$: mô hình thật cũng $1{,}088$: dao động của tập kiểm tra" |
| chuyên gia | 6-00 | dòng dẫn | đã sửa (như trên) |
| chuyên gia | 5-03 | khối lượng điểm | đã sửa (như trên) |
| chuyên gia | 6-04 | dạng tổng quát; tên tiếng Anh; hội tụ bị chặn | đã sửa: "(differentiation under the integral sign)", "(định lý hội tụ bị chặn)" |
| chuyên gia | 3-06 | $L_S(\theta)$ với $\theta$ cố định | đã sửa |
| chuyên gia | 7-01 | $p_\theta$ tổng $1$ | đã sửa |
| chuyên gia | 3-03 | học theo đáp án trên mặt trang | không sửa: trang ở trần ($58$ âm tiết, 4 dòng); định nghĩa ở ghi chú diễn giả |
| chuyên gia | 6-08 | $\min_WF=\min_\Phi F$ | đã sửa ở ghi chú diễn giả; mặt trang không thêm (6-08 sát chân trang) |
| chuyên gia | 4-06 | bảo đảm theo thuật toán (Bài tập 09.9) | đã sửa (ghi chú diễn giả 4-06 và 7-06) |
| học viên | 3-08 | cơ chế rò rỉ không đọc được | đã sửa: "Hàm dự đoán ghi nhớ tra $u_{j+1}$: đích $x_j$ ở cuối ngữ cảnh"; "rủi ro nhỏ nhất" thành "$<\operatorname{Var}(x_j)=1$" |
| học viên | 3-09 | hai điểm cực tiểu không có lý do | đã sửa: hai dòng với hai rủi ro, cực tiểu và trọng số |
| học viên | 4-07 | $\ln4$, $1{,}0889$, thiết lập | đã sửa (như trên; ngắt công thức hết vì công thức chuyển vào ghi chú) |
| học viên | 6-08 | (C), (G1); $u$; $\varphi$ và $\phi$ | đã sửa; ghi chú phân biệt $\varphi$ và $\phi$ |
| học viên | toàn deck | mật độ sát trần | một phần: không trang nào vượt $60$; trung vị tăng lên $56$ vì các bổ sung bắt buộc (xem điểm còn mở) |
| học viên | 4-08 | "(c)" hai lần; số trong bảng | đã sửa: trang chỉ còn câu (c) theo câu chữ đề, không còn bảng; câu (b) ở ghi chú diễn giả |
| học viên | 1-02, 2-04 | ERM trước tên đầy đủ | đã sửa: 1-02 "Tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM)" |
| học viên | 2-04 | $s$ cố định | đã sửa: "tập huấn luyện cố định $s$" |
| học viên | 3-07 | "nat" | đã sửa: "nat (đơn vị của $\ln$)" |
| học viên | 3-08 | tên tiếng Anh lỗi bình phương; chú thích hình | đã sửa: "(squared loss)"; chú thích "Chung $9$ giá trị ($k=10$)" |
| học viên | 4-05 | khoảng cách tổng quát hóa | đã sửa: $L_D(0{,}7)-L_s(0{,}7)$ |
| học viên | 5-05 | kí hiệu ELBO | đã sửa |
| học viên | 6-01 | hai dấu hai chấm | đã sửa |
| học viên | 6-03 | thương sai phân chưa nêu | đã sửa (bước 1) |
| học viên | 6-05 | $4+2-0$ | đã sửa: $4\operatorname{Var}\zeta+\operatorname{Var}\zeta^2=6$ ($\mathbb E\zeta^3=0$) |
| học viên | 6-07 ghi chú | thiếu thừa số $50$ | đã sửa |
| học viên | 7-03 | "hạt giống" thiếu tiếng Anh; thiếu vế không được phép | đã sửa (7-03, 7-04) |
| học viên | nhiều trang | dòng > 20 âm tiết | một phần: còn 3-04 ($29$), 7-03 ($26$), 4-08, 6-07, 7-05 ($22$–$23$): câu chữ của đề hoặc một ý trọn vẹn |
| học viên | nhiều trang | mảnh mồ côi sau KaTeX | đã sửa bằng `white-space:nowrap` ở 1-06, 3-09, 5-02, 6-02, 7-02, 7-04 và viết lại 4-07, 5-05, 6-08 |
| học viên | 5-04, 7-01, 3-05 (390 px) | hình nhỏ, bảng cuộn | không sửa: người duyệt ghi "không bắt buộc"; số đều có trong chữ hoặc bảng |
| sư phạm | 4-08, 7-03 | đề rút thành mảnh câu; vế "không được phép" | đã sửa: 4-08 câu (c) đủ câu chữ đề; 7-03/7-04 câu đầy đủ, lời giải có hai vế |
| sư phạm | 7-06 ghi chú | câu quy trình, câu nguồn gốc | đã sửa |
| sư phạm | 1-02, 2-01, 2-04, 4-05, 6-08, 7-03 | tên tiếng Anh, tên đầy đủ | đã sửa: rủi ro kì vọng, rủi ro thực nghiệm, ERM, log loss, generalization gap, SGD (6-01), random seed |
| sư phạm | 3-08 | "Tra" không chủ thể | đã sửa |
| sư phạm | 6-01 | cấu trúc khó theo | đã sửa |
| sư phạm | 6-08 | (C), (G1) | đã sửa |
| sư phạm | 1-03 | mục tiêu viết tắt | đã sửa ("Phân biệt …", "giải thích rò rỉ", "tách số hạng tái tạo", "kiểm điều kiện"); ghi chú viết theo nội dung |
| sư phạm | 1-02, 5-01, 6-06 ghi chú | "Câu ôn nhanh", "Câu hỏi cuối buổi (d)" | đã sửa |
| sư phạm | 1-06 | hai dấu hai chấm; "rút" | đã sửa |
| sư phạm | ghi chú | "câu hỏi mở đầu" và "ví dụ mở đầu" | đã sửa: "ví dụ mở đầu" (dòng nguồn giữ tên mục của ghi chú) |
| sư phạm | 2-03 | mảnh câu, "trái với" | đã sửa |
| sư phạm | 2-06 | tiêu đề | không còn áp dụng (trang bỏ) |
| sư phạm | 3-01 | "Trực quan." quá ngắn | đã sửa một phần: "Thừa số thứ $j$: phân lớp kí tự $j$ theo tiền tố $x_{<j}$" (trang ở trần $60$) |
| sư phạm | 3-03 | "$<2$" | đã sửa: "$<2$ (mô hình đều)" |
| sư phạm | 3-05 ghi chú | chủ thể trừu tượng; câu lặp | đã sửa |
| sư phạm | 3-06, 3-07 | mảnh câu, số làm chủ ngữ, nat | đã sửa |
| sư phạm | 4-00 ghi chú | cấu trúc | đã sửa |
| sư phạm | 4-05 | trả lời "Không" trên mặt trang; ghi chú đọc lại số | đã sửa |
| sư phạm | 4-07 | "lỗi huấn luyện"; dãy số | đã sửa: "rủi ro thực nghiệm"; dãy $0{,}2$; $0{,}1$; $0{,}1$ chuyển vào ghi chú |
| sư phạm | 5-06 | "$0{,}5$, $0{,}9$" | đã sửa |
| sư phạm | 4-07 ghi chú | câu dồn | đã sửa |
| sư phạm | 5-02, 5-00 | "khoảng cách" thay "khe"/"hiệu" | đã sửa |
| sư phạm | 5-02 ghi chú | phủ định lồng | đã sửa |
| sư phạm | 5-04, 5-06 | "tái tạo" thay "số hạng tái tạo" | đã sửa trong câu; tiêu đề cột giữ "Tái tạo" |
| sư phạm | 3-01, 4-02, 4-04, 5-02, 5-05, 6-02 ghi chú | câu "được chứng minh đầy đủ" | đã sửa: bỏ năm câu [F]; 6-02 "Ghi chú phác thảo chứng minh; chi tiết ở Phụ lục B." |
| sư phạm | 4-03, 5-03, 6-03 ghi chú | khuôn "Bất đẳng thức then chốt là" | đã sửa: ghép vào câu về bước dùng |
| sư phạm | 6-00 | dòng dẫn mệnh lệnh; thiếu ý thứ hai | đã sửa ý đầu (chủ ngữ "Tái tham số hóa"); ý thứ hai không thêm (trần $25$) |
| sư phạm | 6-03 | "((i))"; dòng cuối | đã sửa: "(dùng (i))"; "**Lưu ý:** (i) cần $N_0$ chung cho mọi $\phi$" |
| sư phạm | 6-05 | $4+2-0$ | đã sửa |
| sư phạm | 6-07 | dòng dồn ba ý | đã sửa (tách dòng) |
| sư phạm | 7-00, 7-01 ghi chú | dòng dẫn lặp luận điểm; "nằm ngoài bảng" | đã sửa: dòng dẫn "Mỗi kết quả của bài thuộc một loại bảo đảm: tất định, tổng thể hoặc kì vọng theo nhiễu phụ." |
| mạch truyện M1 | 5-01 | câu nối 4→5 | đã sửa: "Độ hợp lý của mô hình có biến không quan sát được là một tích phân, nói chung không tính được." |
| mạch truyện M2 | 6-01 | câu nối 5→6 | đã sửa: "Cực đại hóa ELBO bằng hạ gradient ngẫu nhiên (…, SGD) cần $\nabla F$"; "hậu nghiệm không dạng đóng" ở ghi chú; Gauss ra ghi chú |
| mạch truyện M3 | 6-07 | câu nối, $50$ chuỗi của Ví dụ 09.8 | đã sửa; không đổi chỗ 6-07, 6-08 (tùy chọn) |
| mạch truyện M4 | 4-07 | câu hỏi thực hành trên mặt trang | một phần: (i) "$m=50$: cách tốt nhất $\approx0{,}0009$" và $m=1$, $m=500$ trên mặt trang; (iii) và "đặc tả đúng" ở ghi chú (trần, $6$ dòng) |
| mạch truyện M5 | 7-02 | cách học mô hình biến ẩn; đại lượng được chặn | đã sửa |
| mạch truyện N1 | 6-08 | (C), (G1) | đã sửa |
| mạch truyện N2 | 1-02, 6-08 | ERM, SGD | đã sửa |
| mạch truyện N3 | 2-03 | (T7) của Bài 04 | đã sửa: "(T7) (Bài 04)" trên 2-03; 1-02 không thêm (trần) |
| mạch truyện N4 | 3-03 | mốc $2$ | đã sửa |
| mạch truyện N5 | 4-05 | khoảng cách tổng quát hóa | đã sửa |
| mạch truyện N6 | 4-08 | "(c)" hai lần | đã sửa |
| mạch truyện N7 | 3-07 | số hiệu Ví dụ 09.4 | đã sửa |
| mạch truyện N8 | 3-09 | câu kết luận | không sửa trên mặt trang (trần $60$); câu ở ghi chú diễn giả |
| mạch truyện N9 | 7-00 | dòng dẫn | đã sửa |
| mạch truyện N10 | 7-07 | liên kết Bài 10 | không sửa: deck Bài 10 chưa qua duyệt |
| mạch truyện N11 | storyboard | §3, §9 cũ | đã sửa: §3 cập nhật số trang; mục này và mục 15 thay các mô tả cũ |

**Còn mở cho điều phối viên.** (1) Bỏ 2-06: mạch 2 không còn bài tập trên lớp. (2) Trung vị mật độ $56$ trên 43 trang nội dung (trước sửa $51$): mọi trang $\le60$, nhưng các bổ sung bắt buộc (giả thiết đầy đủ, tên tiếng Anh, câu nối, câu chữ đề) đẩy nhiều trang lên $57$–$60$. (3) 4-08 chỉ còn câu (c) của Bài tập 09.3; câu (b) ở ghi chú diễn giả. (4) Hình F1 ở 3-08 và F2 ở 5-04 thu nhỏ để vừa khung; số trên hình có trong chữ.

**Bổ sung theo điều phối viên (2026-11-16).** Khôi phục hai giả thiết: 7-01 hàng Mệnh đề 09.8/Hệ quả 09.9 ghi "$\mathcal X$ đếm được; $p_\theta$ tổng $1$; $\mathrm H(p_D)<\infty$"; 1-02 "(T2) $\ell\ge0$, đo được". Để 7-01 không chạm chân trang, phần "(mật độ: khả tích)" chuyển vào ghi chú diễn giả 7-01 (hàng này phát biểu bản rời rạc với $\mathrm H(p_D)$), ô giả thiết của hàng Định lý 09.12 viết gọn "$p_\theta(x)\in(0,\infty)$; $p_\theta(x,v)>0$ trên giá $q$; khả tích; EM: $\mathcal V$ và bước M hữu hạn", cột $42/32/26\%$. Mật độ: 1-02 $51$, 7-01 $76$/80.

**Sửa sau kiểm lại (`reviews/deck-recheck.md`).** R2: 4-07 ghi đủ dữ liệu xích Markov ($0{,}6$; $0{,}2$; $0{,}1$; $0{,}1$; trung bình $10$ lần chạy) trên mặt trang; dòng $m=500$ chuyển xuống ghi chú diễn giả. R3: 2-02 ghi chú diễn giả đặt "(T1) không áp dụng cho các cửa sổ" sau câu về cửa sổ chồng lấn. Nhẹ: 6-01 "phân bố không phụ thuộc $\phi$", dòng "Trực quan." nêu $\phi$ chỉ nằm trong $f(g_\phi(\zeta))$; 6-08 lời giải nêu $\max_W\mathbb E\lVert\varphi\rVert^2=12$; 6-00 dòng dẫn không dùng "hàm trội", "đường nhiễu"; 1-02, 6-08, 6-01, 4-07, 2-02 thêm `white-space:nowrap` cho dấu câu mồ côi ở 390 px; 4-05 ghi chú diễn giả gọi tên chủ ngữ; mục 3 cập nhật mạch 2, dòng dẫn mạch 6, 7. R1 (7-03), **ngoại lệ mật độ** (điều phối viên chọn phương án (a), 2026-11-16; tiền lệ Bài 01, 05): 7-03 là bài tập tổng hợp, mặt trang ghi đủ giả thiết của Bài tập 09.6(b) ($n=200$, $200$ chuỗi kiểm tra, mô hình làm trơn với $m=50$, cận $0{,}087$, độ lệch chuẩn $0{,}0041$ qua mười hạt giống, cách của Ví dụ 09.4) và thuật ngữ "hạt giống (random seed)" với $76$ âm tiết, vượt trần $60$; `deck_lint` chỉ báo trang này. Ghi chú diễn giả bỏ câu "Câu đầy đủ của (i): …", giữ phần giải thích lỗi kiểm tra, mười hạt giống và gợi ý. Kiểm lại lượt 2: 4-07 có lại dòng "$m=500$: mô hình thật cũng $1{,}088$: dao động của tập kiểm tra" (bù bằng cách viết gọn dòng xích Markov và chuyển trích dẫn Mệnh đề 09.8(b) xuống ghi chú diễn giả; giữ đủ dữ kiện, $60$ âm tiết).
