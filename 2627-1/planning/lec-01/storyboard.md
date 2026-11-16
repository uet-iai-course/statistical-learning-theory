# Storyboard — Bộ trang chiếu Bài 01: Mô hình học

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-11-15 bởi tác tử lập storyboard (deck thí điểm của học phần; bố cục dùng làm khuôn cho deck 02–10). Nguồn nội dung duy nhất: `materials/lec-01/lecture-note.md` (bản hiện hành); bài tập: `materials/lec-01/exercises.md`. Quy định: `CLAUDE.md` § Slide decks, `../rl-plan/CLAUDE.md` § Deck structure and content, nhật ký yêu cầu 2026-11-13 hàng 1–6. Mọi mã trang có dạng `L01-k-mm`; trong bảng viết gọn `k-mm`.

Số âm tiết ghi trong tệp này là ước lượng của người lập (đếm theo khoảng trắng, không tính tiêu đề, KaTeX, số trong bảng, nhãn hình, ghi chú); điều phối viên đếm lại trên deck.

## 1. Tên tệp và tiêu đề

- **Tệp deck:** `2627-1/lecture-01-mo-hinh-hoc.html` (slug ASCII từ phần đầu tên bài "Mô hình học"; phần sau dấu hai chấm dài, bỏ khỏi slug).
- **Tiêu đề deck (h1 trang bìa):** "Mô hình học: rủi ro, tối thiểu hóa rủi ro thực nghiệm và học PAC" (đúng tên bài của ghi chú).
- **`<title>`:** "Bài 01: Mô hình học".
- **Chân trang:** "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài 01".
- **Liên kết viewer:** `material-viewer.html?doc=materials/lec-01/lecture-note.md&deck=lecture-01-mo-hinh-hoc.html` và `…exercises.md&deck=…`.

## 2. Khung lý thuyết chung

**Vấn đề trung tâm (hộp "Vấn đề trung tâm", một dòng).** "Câu hỏi: học có nghĩa là gì, tức khi nào một hàm dự đoán chọn từ tập huấn luyện được xem là đã học được?" (theo đoạn mở đầu của ghi chú; xem mục 11, điểm 1).

**Luận điểm (trang bìa, một câu).** "Học là chọn từ tập huấn luyện một hàm dự đoán có rủi ro kì vọng không vượt mức tốt nhất trong lớp giả thuyết cộng $\epsilon$, với xác suất ít nhất $1-\delta$, khi cỡ mẫu vượt một ngưỡng không phụ thuộc phân bố." (ghi chú §7, đoạn cuối; ≈ 38 âm tiết.)

**Đối tượng và kí hiệu chung** (theo `ky-hieu.md` và ghi chú §1–§2):
- $\mathcal X$, $\mathcal Y$, $\mathcal Z=\mathcal X\times\mathcal Y$; quan sát $z=(x,y)$; phân bố liên hợp $D$ trên $\mathcal Z$, phân bố biên $D_{\mathcal X}$, $\eta(x)=\Pr(Y=1\mid X=x)$;
- tập huấn luyện $S=(Z_1,\ldots,Z_m)\sim D^m$, cỡ mẫu $m$;
- lớp giả thuyết $\mathcal H$, hàm lỗi $\ell(h,z)\ge0$ ($\ell_{0\text{-}1}$, $\ell_c$ với $(c_{FP},c_{FN})$);
- thuật toán học $A$, đầu ra $A(S)\in\mathcal H$;
- $L_D(h)$, $L_S(h)$, $\arg\min_{h\in\mathcal H}L_S(h)$, $A_{\min}$, $A_{\max}$, $A_{\mathrm{gn}}$, $\mathcal M_{\mathcal X}$, $L_D^{\mathrm{Bayes}}$, $h_{\mathrm{Bayes}}$, $m_A(\epsilon,\delta)$, $m_{\mathcal H}(\epsilon,\delta)$.

**Giả thiết** (ghi chú §2): (T1) lấy mẫu i.i.d. (dạng yếu: mỗi $Z_i\sim D$); (T2) $\ell\ge0$, $\ell(h,\cdot)$ đo được, $L_D(h)<\infty$ khi $\ell$ không bị chặn; (O1) thuật toán trả về nghiệm ERM chính xác; (O2) thuật toán trả về nghiệm $\epsilon_{\mathrm{opt}}$-ERM; khả diễn: có $h^\star\in\mathcal H$ với $L_D(h^\star)=0$ (hàm lỗi 0–1).

**Chuỗi định nghĩa → kết quả → phương pháp.**
1. Bài toán học thống kê (Định nghĩa 01.1, 01.4, 01.5): mục tiêu $L_D(A(S))-\inf_{h\in\mathcal H}L_D(h)$ nhỏ khi không biết $D$.
2. Đại lượng thay thế tính được: $L_S$ (Định nghĩa 01.6); không chệch với $h$ cố định (Mệnh đề 01.7); hỏng khi $h=A(S)$ (Nhận xét 01.9).
3. Phương pháp: ERM (Định nghĩa 01.8, 01.12, Thuật toán 01.13); quy tắc chọn khi bằng nhau quyết định rủi ro.
4. Phản ví dụ: hàm phân lớp ghi nhớ có $L_S=0$, $L_D=1$ (Mệnh đề 01.15); thiên kiến quy nạp.
5. Bảo đảm học: học PAC khả diễn (Định nghĩa 01.16, 01.18, 01.20); rủi ro Bayes và quy tắc Bayes (Định nghĩa 01.22, Mệnh đề 01.23); rủi ro vượt mức, học PAC bất khả diễn (Định nghĩa 01.24, 01.25).
6. Giới hạn và bảo đảm cụ thể: không có cận tổng quát hóa không tầm thường cho mọi ERM trên $\mathcal M_{\mathcal X}$ (Định nghĩa 01.28, Hệ quả 01.29); $A_{\max}$ trên lớp hàm ngưỡng có cỡ mẫu $\lceil\ln(1/\delta)/\epsilon\rceil$ (Mệnh đề 01.31).

**Giới hạn áp dụng** (ghi chú §4, §7, §9, Phụ lục A): học PAC khả diễn chỉ xét phân lớp nhị phân với hàm lỗi 0–1; thuật toán tất định (thuật toán có $\xi$ cần định nghĩa mở rộng, xác suất lấy theo $S$ và $\xi$); học đúng lớp ($A(S)\in\mathcal H$); hiệu $\inf_{h\in\mathcal H}L_D(h)-L_D^{\mathrm{Bayes}}$ không giảm theo $m$; tính đo được đồng thời theo $(s,z)$ cần cho $L_D(A(S))$ là biến ngẫu nhiên; với lớp vô hạn, $\sup_h\lvert L_S(h)-L_D(h)\rvert$ có thể không đo được. Trên deck chỉ giữ ba giới hạn đầu (ở ghi chú diễn giả các trang 2-01, 5-02, 5-12); tính đo được nằm ở ghi chú.

## 3. Bảng mạch

Bảy mạch theo đúng thứ tự các mục của ghi chú; mỗi mạch ứng với các mục liên tiếp, và trong mỗi mạch các khối theo thứ tự đọc của ghi chú (quy định "Consistency with the note"). Bảng đối chiếu trang → khối ghi chú ở mục 12.

| N | Tên mạch | Mục ghi chú | Chức năng | Đầu vào | Đầu ra | `strand-lead` (âm tiết) | Từ khóa | Trang | Phút |
|---|---|---|---|---|---|---|---|---:|---:|
| 1 | Mở đầu | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết, §2 | Bìa, luận điểm, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, câu hỏi mở đầu $h_3$, $h_4$ | kiến thức xác suất | Hai hàm phân lớp cùng khớp $S_f$, rủi ro $0$ và $0{,}2$ | (không có trang tiêu đề mạch) | — | 6 | 8 |
| 2 | Bài toán học thống kê | §1, §3, §4 | Tám thành phần; ví dụ sàng lọc; rủi ro kì vọng; mục tiêu của bài toán học | câu hỏi mở đầu | $L_D(h_t)$ dưới hai hàm lỗi; mục tiêu $L_D(A(S))-\inf_hL_D(h)$; $L_D$ không tính được | "Chất lượng của một hàm dự đoán là mức sai trung bình của nó trên dữ liệu mới." (sửa 2026-11-15, sau duyệt) | tám thành phần · rủi ro kì vọng · hàm lỗi có trọng số · mục tiêu so với lớp giả thuyết | 6 | 15 |
| 3 | Rủi ro thực nghiệm và tối thiểu hóa rủi ro thực nghiệm | §5, từ Định nghĩa 01.6 đến Thuật toán 01.13 | $L_S$; tính không chệch; ERM và quy tắc chọn khi bằng nhau; chỗ hỏng khi chọn theo tập huấn luyện | $L_D$ không tính được | $\mathbb E_S L_S(h)=L_D(h)$ chỉ với $h$ cố định; tập nghiệm ERM; quy tắc chọn quyết định rủi ro | "Tỉ lệ lỗi trên tập huấn luyện có trung bình bằng mức sai trên dữ liệu mới khi hàm được chọn trước." (sửa 2026-11-15, sau duyệt) | rủi ro thực nghiệm · ước lượng không chệch · khoảng cách tổng quát hóa · quy tắc chọn khi bằng nhau | 8 | 21 |
| 4 | Thuật toán ghi nhớ và thiên kiến quy nạp | §5, từ Định nghĩa 01.14 đến hết mục | Phản ví dụ cực đoan; kỹ thuật bất đẳng thức hợp; thiên kiến quy nạp | quy tắc chọn khi bằng nhau quyết định rủi ro | Nghiệm ERM với $L_S=0$, $L_D=1$; bảo đảm phải nói về $L_D(A(S))$ và cho phép thất bại | "Một hàm khớp mọi quan sát huấn luyện vẫn có thể sai với xác suất 1 trên quan sát mới." (sửa 2026-11-15, sau duyệt) | thuật toán ghi nhớ · nguyên tử · bất đẳng thức hợp · quá khớp · thiên kiến quy nạp | 7 | 15 |
| 5 | Học PAC | §6, §7 | Vai trò $\epsilon$, $\delta$; định nghĩa và thứ tự lượng từ; độ phức tạp mẫu; rủi ro Bayes; học PAC bất khả diễn | bảo đảm phải cho phép thất bại | Hai định nghĩa học PAC; $m_A$, $m_{\mathcal H}$; đối tượng so sánh $\inf_hL_D(h)$ | "Học được nghĩa là rủi ro gần mức tốt nhất với xác suất cao khi đủ dữ liệu." (sửa 2026-11-15, sau duyệt) | xác suất thất bại · thứ tự lượng từ · độ phức tạp mẫu · rủi ro Bayes · rủi ro vượt mức | 13 | 32 |
| 6 | Rủi ro thực nghiệm nhỏ và bảo đảm học | §8, §9 | Hệ quả 01.29; bỏ giả thiết không có nguyên tử (Ví dụ 01.11); Mệnh đề 01.31 với kỹ thuật chặn xác suất bỏ sót | định nghĩa học PAC; phản ví dụ ghi nhớ | $L_S$ nhỏ không đủ; cỡ mẫu $\lceil\ln(1/\delta)/\epsilon\rceil$ chung cho mọi phân bố khả diễn | "Rủi ro thực nghiệm nhỏ không đủ làm bảo đảm học; bảo đảm cần cỡ mẫu chung cho mọi phân bố." (sửa 2026-11-15, sau duyệt) | cận tổng quát hóa · phản ví dụ · nguyên tử · cỡ mẫu không phụ thuộc phân bố | 8 | 16 |
| 7 | Tổng kết | §10, §11, §12 | Bảng kết quả, trả lời vấn đề trung tâm, bài tập tổng hợp, tự kiểm tra, bài tập, tài liệu | mọi kết quả | Cầu nối sang Bài 02 | "Học là chọn hàm có rủi ro gần mức tốt nhất trong lớp với xác suất cao, khi cỡ mẫu vượt ngưỡng chung cho mọi phân bố." (sửa 2026-11-15, lượt 2) | — | 7 | 13 |
| | **Tổng** | | | | | | | **55** | **120** |

**Deck cuối (2026-11-15):** vẫn 55 trang (trần 55): gộp (a) và (b) bớt hai trang, tách Hệ quả 01.29 và thêm bài tập tổng hợp thêm hai trang (quyết định của điều phối viên, `review-log.md`, mục "Bộ trang chiếu"). Thời lượng: mạch 3 và mạch 5 mỗi mạch bớt 1 phút, mạch 7 thêm 2 phút cho bài tập tổng hợp. Đoạn sau là lý do khi lập storyboard. Số trang (55) vượt mức tham khảo 35–50 năm trang. Lý do: năm kết quả của ghi chú đều có hành trình khái niệm đủ bước; ba kỹ thuật dùng lại qua học phần có trang "Kỹ thuật." riêng; người dùng yêu cầu làm rõ riêng vai trò của $\epsilon$, $\delta$ và thứ tự lượng từ; bài tập trên mặt trang phải lấy từ `exercises.md`, và Bài tập 01.5(d) cần hai trang (đề, lời giải) để giữ trần mật độ. Phương án rút còn 51 trang ở mục 11, điểm 2. Mạch 5 chiếm 33 phút; tách thành hai mạch sẽ cho tám mạch, vượt trần 7.

## 4. Bảng kết quả chính

Số hiệu theo ghi chú. Bốn kết quả của blueprint (Prop 1.1, Counterexample 1.2, Prop 1.3, Corollary) là Mệnh đề 01.7, 01.15, 01.23 và Hệ quả 01.29; Mệnh đề 01.31 thêm 2026-11-13. Mọi phát biểu rút gọn trên trang giữ đủ giả thiết, lượng từ, hằng số và loại bảo đảm của ghi chú (cột "Loại bảo đảm").

| Kết quả | Loại bảo đảm | (a) Trực quan dự kiến | (b) Ý tưởng chứng minh | (c) Kỹ thuật | (d) Ví dụ bổ trợ | Trang |
|---|---|---|---|---|---|---|
| **Mệnh đề 01.7** (tính không chệch, chứng minh đầy đủ) | kì vọng; thực nghiệm so với tổng thể; mọi $m\ge1$ | Với $h$ cố định, mỗi số hạng $\ell(h,Z_i)$ là một lần thử $h$ trên dữ liệu mới; trung bình các lần thử có kì vọng $L_D(h)$. Cực biên $Z_1=\cdots=Z_m$: $L_S(h)\in\{0,1\}$ nhưng kì vọng vẫn bằng $L_D(h)$. | Bước 1: $\mathbb E\,\ell(h,Z_i)=L_D(h)$, dùng $h$ không phụ thuộc $S$, $Z_i\sim D$, $L_D(h)<\infty$. Bước 2: tính tuyến tính, không cần độc lập. Bỏ "$h$ không phụ thuộc $S$" thì Bước 1 hỏng (Nhận xét 01.9); phản ví dụ $A_{\max}$ dưới $D_f$, $m=1$: $\mathbb E L_S=0<0{,}36=\mathbb E L_D$. | Tính tuyến tính của kì vọng (lần đầu trong học phần; dòng "Kỹ thuật." trên 3-03 sau khi gộp). | Ví dụ 01.5 ($L_{S_\eta}(h_3)=\tfrac13$ so với $0{,}22$); ví dụ mới một quan sát (3-05). | 3-02, 3-03, 3-05 |
| **Mệnh đề 01.15** (hàm phân lớp ghi nhớ, chứng minh đầy đủ) | tất định, mọi $m\ge1$, mọi tập huấn luyện | Một tập hữu hạn có xác suất $0$ dưới $U[0,1]$; quan sát mới hầu chắc chắn rơi ngoài tập huấn luyện, nơi hàm ghi nhớ báo $0$ còn nhãn luôn là $1$. Hai nghiệm ERM trên cùng $S$: $\mathbb 1_F$ (rủi ro $1$) và $h_{\equiv1}$ (rủi ro $0$). | Bốn bước: thuộc lớp (dùng $\mathcal H=\mathcal M_{\mathcal X}$); nghiệm ERM, $L_S=0$; $\Pr(X\in F)\le\sum_i\Pr(X=x_i)=0$ (dùng không có nguyên tử); $h_{\equiv1}$ cũng là nghiệm ERM. Bỏ "không có nguyên tử": Ví dụ 01.11, $\mathbb E L=0{,}8^m\to0$ (mạch 6, theo thứ tự ghi chú). Bỏ "lớp chứa mọi hàm đo được": lớp hàm ngưỡng loại hàm ghi nhớ trên $\tilde S_f$. | Bất đẳng thức hợp (lần đầu trong học phần, trang riêng 4-04); tập có xác suất $0$. | Ví dụ 01.8 (hình F4); Bài tập 01.4(a) có lời giải (4-05); $\tilde S_f$ (4-06); Ví dụ 01.11 (6-04). | 4-01 đến 4-06, 6-04 |
| **Mệnh đề 01.23** (quy tắc Bayes, đọc thêm) | đại lượng tổng thể, trên mọi hàm phân lớp đo được | Tại mỗi $x$ chỉ có hai lựa chọn; chọn nhãn có rủi ro có điều kiện nhỏ hơn: báo $1$ khi $\eta(x)\ge\tfrac12$; khi bỏ sót đắt gấp bốn, ngưỡng hạ xuống $\tfrac15$. | Ba bước: rủi ro có điều kiện $\eta(x)\mathbb 1[g(x)=0]+(1-\eta(x))\mathbb 1[g(x)=1]$; tối thiểu hóa từng điểm, được $\min\{\eta,1-\eta\}$; lấy kì vọng bằng $\mathbb E[\mathbb E[U\mid X]]=\mathbb E[U]$. Với $\ell_c$: so $c_{FP}(1-\eta)$ với $c_{FN}\eta$. Giả thiết vào: $\eta$ đo được (để $h_{\mathrm{Bayes}}\in\mathcal M_{\mathcal X}$), $g$ đo được. | Tối thiểu hóa từng điểm rồi lấy kì vọng (dòng "Kỹ thuật." trên trang 5-09, không có trang riêng; mục 11, điểm 5). | Ví dụ 01.10: $h_{\mathrm{Bayes}}=\mathbb 1[x\in\{3,5\}]\notin\mathcal H$, $L^{\mathrm{Bayes}}=0{,}18$ (5-07); dưới $\ell_c$: $h_2$, $0{,}32$ (5-10). | 5-07, 5-08, 5-09, 5-10 |
| **Hệ quả 01.29** (rủi ro thực nghiệm nhỏ không đủ, chứng minh đầy đủ) | (a) cận cho mọi $m$, $\delta$; (b) xác suất thành công bằng $0$ với mọi $m$ | Cận phải đúng cho mọi ERM và mọi $D$; một cặp $(A_{\mathrm{gn}},D)$ có khoảng cách tổng quát hóa bằng $1$ trên mọi tập huấn luyện đủ để buộc $\beta\ge1$. | (a) biến cố $\{1\le\beta(m,\delta)\}$ không phụ thuộc $S$, xác suất là $0$ hoặc $1$; vì $1-\delta>0$, cần $\beta\ge1$. (b) $(D,\mathcal M_{\mathcal X})$ khả diễn, $L_D(A_{\mathrm{gn}}(S))=1>\epsilon$ trên mọi $S$, nên $m_{A_{\mathrm{gn}}}=\infty$. Hai giả thiết của Mệnh đề 01.15 vào qua (a) và (b). | Nhắc lại Mệnh đề 01.15 và bất đẳng thức hợp; bác bỏ một khẳng định "với mọi" bằng một phản ví dụ (ghi chú diễn giả). | Câu hỏi của ghi chú §8 (6-01). | 6-01, 6-02, 6-03 |
| **Mệnh đề 01.31** (cỡ mẫu của $A_{\max}$, phác thảo) | xác suất cao; mọi $D$ khả diễn, mọi $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$ | $A_{\max}$ chỉ sai ở các mức từ $t^\star$ đến $\hat t-1$. Thất bại nghĩa là bỏ sót toàn bộ một khối mức đầu có khối lượng lớn hơn $\epsilon$; xác suất bỏ sót giảm mũ theo $m$, không phụ thuộc $K$, $D_{\mathcal X}$. | Ba bước: vùng lỗi $G(\hat t)=D_{\mathcal X}(\{t^\star,\ldots,\hat t-1\})$; tập $C=\{t^\star,\ldots,k\}$ với $D_{\mathcal X}(C)>\epsilon$, có quan sát trong $C$ thì $L_D\le\epsilon$; xác suất thất bại không quá $(1-\epsilon)^m\le e^{-\epsilon m}\le\delta$. Giả thiết vào: khả diễn (nhãn $1$ trên $C$ hầu chắc chắn), (T1) (lũy thừa $m$). | Chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ (lần đầu, trang riêng 6-07). | $\epsilon=0{,}1$, $\delta=0{,}05$ cho $m\ge30$, so với $14$ riêng cho $D_f$ (hình F5b); kiểm tra trên $D_f$: $C=\{3\}$, cận $0{,}8^m$ trùng xác suất đúng. | 6-05, 6-06, 6-07 |

**Kết quả phụ và quyết định.**
- Ví dụ 01.3, Nhận xét 01.2, Định nghĩa 01.3 (hàm lỗi không bị chặn, phân bố có rủi ro hữu hạn): ghi chú diễn giả trang 2-03; Định nghĩa 01.3 nhắc lại một dòng ở 5-12. Lý do: không có trực quan mới cho câu hỏi trung tâm.
- Nhận xét 01.11, Ví dụ 01.7, Định nghĩa 01.12 (tồn tại nghiệm ERM, ERM xấp xỉ): ghi chú diễn giả 3-04. Lý do: (O2) dùng ở các bài sau, nhưng không phục vụ mạch chính của Bài 01.
- Thuật toán 01.13: quy tắc cập nhật trên mặt trang bài tập 3-07 (Bài tập 01.2(a)); lượt chạy trên $S_\eta$ và đặc tả đầy đủ ở ghi chú diễn giả và ghi chú.
- Nhận xét 01.17 (khả diễn là tính chất của cặp): ghi chú diễn giả 5-02.
- Nhận xét 01.19 (độ tin cậy): bài tập 5-06 (Bài tập 01.5(d), câu 4) và câu hỏi tự kiểm tra 3.
- Nhận xét 01.21 (cận trên, cận dưới; thuật toán chẵn lẻ): ý thứ nhất trên 5-04, thuật toán chẵn lẻ ở ghi chú diễn giả.
- Nhận xét 01.26, 01.27 (học ngoài lớp): ghi chú diễn giả 5-12. Nhận xét 01.30 (định lý không có bữa trưa miễn phí): ghi chú diễn giả 6-02.
- Phụ lục A (tính đo được): không đưa lên deck; ghi chú diễn giả 1-02, 4-03 nhắc điều kiện đo được.

## 5. Ví dụ bổ trợ

Ví dụ xuyên suốt: **sàng lọc theo ngưỡng trên năm mức đo** (Ví dụ 01.1), với hai phân bố $D_\eta$, $D_f$ và ba tập huấn luyện $S_\eta$, $S_f$, $\tilde S_f$. Ví dụ thứ hai: **phân bố đều trên $[0,1]$ với nhãn hằng** (Ví dụ 01.8) và bản có nguyên tử của nó (Ví dụ 01.11). Mỗi lần dùng lại trả lời một câu hỏi mới: hai hàm cùng khớp $S_f$ (1-06), rủi ro kì vọng dưới hai hàm lỗi (2-04), mục tiêu của bài toán học (2-05), cùng $L_S$ khác $L_D$ (3-01), kì vọng của $L_S$ với $h$ cố định (3-02), quy tắc chọn khi bằng nhau (3-04), giả thuyết chọn theo tập huấn luyện (3-05), khoảng cách tổng quát hóa âm (3-06), hàm ghi nhớ trên $S_f$ và $\tilde S_f$ (4-01, 4-06), xác suất thất bại và cỡ mẫu (5-01, 5-05, 5-06), không khả diễn dưới $D_\eta$ và rủi ro Bayes (5-07, 5-08), quy tắc Bayes dưới $\ell_c$ (5-10), phân rã rủi ro vượt mức (5-11), cỡ mẫu chung $30$ so với $14$ (6-05, 6-06, 6-07). Ví dụ trên $[0,1]$: 4-01 đến 4-05, 6-01, 6-02; bản có nguyên tử: 6-04. Các bài tập trên mặt trang lấy từ `exercises.md`: Bài tập 01.2(a) (3-07), 01.4(a) (4-05), 01.5(d) câu 4 (5-06), 01.1(d) (7-03, bài tập tổng hợp), với cùng số liệu và kết quả.

Dữ kiện chung: $\mathcal X=\{1,\ldots,5\}$, $D_{\mathcal X}(x)=0{,}2$; $h_t(x)=\mathbb 1[x\ge t]$, $t=1,\ldots,6$; $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$; $f=h_3$, $L_{D_f}(h_t)=0{,}2\lvert t-3\rvert$; $S_\eta=((1,0),(2,0),(2,1),(3,1),(4,0),(5,1))$; $S_f=((1,0),(2,0),(4,1),(5,1))$; $\tilde S_f=((1,0),(3,1),(5,1))$; $(c_{FP},c_{FN})=(1,4)$.

**V1. Câu hỏi mở đầu** (ghi chú, Câu hỏi mở đầu). $h_3$ và $h_4$ cùng khớp $S_f$: $L_{S_f}(h_3)=L_{S_f}(h_4)=0$. Dưới $D_f$, $h_4$ chỉ sai tại $x=3$: $L_{D_f}(h_4)=0{,}2$; $L_{D_f}(h_3)=0$. Tính lại: $h_4(3)=0\ne f(3)=1$; tại các mức khác $h_4=f$. Đúng.

**V2. Rủi ro kì vọng của các hàm ngưỡng** (Ví dụ 01.2, Phụ lục C.1). $L_{D_\eta}(h_t)=0{,}2[a(t)+b(t)]$, $L^c_{D_\eta}(h_t)=0{,}2[4a(t)+b(t)]$, $a(t)=\sum_{x<t}\eta(x)$, $b(t)=\sum_{x\ge t}(1-\eta(x))$.
- $a=(0;\ 0;\ 0{,}25;\ 1;\ 1{,}4;\ 2{,}4)$, $b=(2{,}6;\ 1{,}6;\ 0{,}85;\ 0{,}6;\ 0;\ 0)$ với $t=1,\ldots,6$.
- $t=3$: $0{,}2(0{,}25+0{,}85)=0{,}22$; $0{,}2(1+0{,}85)=0{,}37$.
- Bảng: $L_{D_\eta}=(0{,}52;\ 0{,}32;\ 0{,}22;\ 0{,}32;\ 0{,}28;\ 0{,}48)$; $L^c_{D_\eta}=(0{,}52;\ 0{,}32;\ 0{,}37;\ 0{,}92;\ 1{,}12;\ 1{,}92)$.
- Tính lại lần hai từng cột: $t=2$: $0{,}2\cdot1{,}6=0{,}32$, $0{,}2\cdot1{,}6=0{,}32$; $t=4$: $0{,}2\cdot1{,}6=0{,}32$, $0{,}2(4+0{,}6)=0{,}92$; $t=5$: $0{,}2\cdot1{,}4=0{,}28$, $0{,}2\cdot5{,}6=1{,}12$; $t=6$: $0{,}2\cdot2{,}4=0{,}48$, $0{,}2\cdot9{,}6=1{,}92$; $t=1$: $0{,}2\cdot2{,}6=0{,}52$ cả hai. Đúng.
- Câu hỏi trên trang 2-04 ($L^c_{D_\eta}(h_2)$, số của bảng Ví dụ 01.2): $a(2)=0$, $b(2)=\tfrac34+\tfrac14+\tfrac35+0=1{,}6$, nên $0{,}2(0+1{,}6)=0{,}32$.

**V3. Rủi ro thực nghiệm trên $S_\eta$** (Ví dụ 01.5). Số lỗi của $h_t$, $t=1,\ldots,6$: $(3,2,2,3,2,3)$; $L_{S_\eta}=(\tfrac12,\tfrac13,\tfrac13,\tfrac12,\tfrac13,\tfrac12)$. Tính lại: $h_3$ sai trên $(2,1)$, $(4,0)$; $h_5$ sai trên $(2,1)$, $(3,1)$; $h_2$ sai trên $(2,0)$, $(4,0)$; $h_4$ sai trên $(2,1)$, $(3,1)$, $(4,0)$; $h_1$ sai trên ba nhãn 0; $h_6$ sai trên ba nhãn 1. Đúng.

**V4 (mới). Một quan sát, hai cách chọn giả thuyết** (trang 3-05). Cách dựng: phân bố $D_f$, cỡ mẫu $m=1$, $S=((X_1,f(X_1)))$, $X_1$ đều trên năm mức; so $h_4$ cố định với nghiệm ERM $A_{\max}$ (Định nghĩa của ghi chú §5). Dưới $D_f$, $A_{\max}$ chọn $\hat t=\min\{x_i:y_i=1\}$, hoặc $6$ khi không có nhãn 1 (Ví dụ 01.6).

| $X_1$ | $1$ | $2$ | $3$ | $4$ | $5$ | trung bình |
|---|---|---|---|---|---|---|
| $L_S(h_4)=\mathbb 1[X_1=3]$ | $0$ | $0$ | $1$ | $0$ | $0$ | $0{,}2$ |
| $\hat t$ của $A_{\max}$ | $6$ | $6$ | $3$ | $4$ | $5$ | |
| $L_S(A_{\max}(S))$ | $0$ | $0$ | $0$ | $0$ | $0$ | $0$ |
| $L_{D_f}(A_{\max}(S))=0{,}2(\hat t-3)$ | $0{,}6$ | $0{,}6$ | $0$ | $0{,}2$ | $0{,}4$ | $0{,}36$ |

- Lần tính thứ nhất (theo bảng): $\tfrac15(0{,}6+0{,}6+0+0{,}2+0{,}4)=\tfrac{1{,}8}5=0{,}36$; $\mathbb E L_S(h_4)=\tfrac15=0{,}2=L_{D_f}(h_4)$.
- Lần tính thứ hai (theo công thức của ghi chú Ví dụ 01.9, Phụ lục C.2, $m=1$): $0{,}2(0{,}8+0{,}6+0{,}4)=0{,}2\cdot1{,}8=0{,}36$. Khớp.
- Kiểm tra từng ô $L_S(A_{\max}(S))=0$: $X_1\in\{1,2\}$, nhãn $0$, $h_6\equiv0$ đúng; $X_1=3,4,5$, nhãn $1$, $h_{X_1}(X_1)=1$ đúng.
- Câu đọc trên trang: với $h_4$ cố định, $\mathbb E_S L_S=L_D=0{,}2$; với $A_{\max}$, $\mathbb E_S L_S=0<0{,}36=\mathbb E_S L_D$. Không khẳng định nào ngoài ghi chú: ghi chú đã có $\mathbb E_S[L_{D_f}(A_{\max}(S))]=0{,}2(0{,}8^m+0{,}6^m+0{,}4^m)$ và $\mathbb E_S[L_S(A_{\max}(S))]=0$.

**V5. Khoảng cách tổng quát hóa âm** (sau Định nghĩa 01.10). $A_{\max}(S_\eta)=h_5$: $0{,}28-\tfrac13=\tfrac{21-25}{75}=-\tfrac4{75}\approx-0{,}053$. Đúng.

**V6. Nghiệm ERM** (Ví dụ 01.6). $S_\eta$: tập nghiệm $\{h_2,h_3,h_5\}$; $A_{\min}\to h_2$, $0{,}32$, hiệu $0{,}10$; $A_{\max}\to h_5$, $0{,}28$, hiệu $0{,}06$. $S_f$: điều kiện $2<t\le4$, tập nghiệm $\{h_3,h_4\}$; $A_{\min}\to h_3$ ($0$), $A_{\max}\to h_4$ ($0{,}2$). Đúng.

**V7. Bài tập 01.2(a): tập nghiệm ERM trên tập cỡ 7** (bài tập 3-07; số liệu và kết quả của `exercises.md`). $\mathcal X=\{1,\ldots,6\}$, $\mathcal H=\{h_t:\ t=1,\ldots,7\}$, $S=((1,0),(2,0),(3,1),(4,0),(4,1),(5,0),(6,1))$.
- Số đếm: $c_0=(1,1,0,1,1,0)$, $c_1=(0,0,1,1,0,1)$.
- $E(1)=4$; $E(2)=4-1+0=3$; $E(3)=3-1+0=2$; $E(4)=2-0+1=3$; $E(5)=3-1+1=3$; $E(6)=3-1+0=2$; $E(7)=2-0+1=3$. Khớp bảng $E=(4,3,2,3,3,2,3)$ của lời giải.
- Kiểm tra trực tiếp: $h_3$ sai trên $(4,0)$, $(5,0)$; $h_6$ sai trên $(3,1)$, $(4,1)$; $E(1)$ bằng số nhãn 0 ($4$), $E(7)$ bằng số nhãn 1 ($3$). Đúng.
- Tập nghiệm $\{h_3,h_6\}$; $A_{\min}(S)=h_3$, $A_{\max}(S)=h_6$.
- Số của phần (b) dùng ở dòng "Diễn giải:" (tính lại với $a(x)=D_{\mathcal X}(x)\eta(x)=(0;\ 0{,}04;\ 0{,}08;\ 0{,}12;\ 0{,}18;\ 0{,}07)$, $b(x)=(0{,}1;\ 0{,}16;\ 0{,}12;\ 0{,}08;\ 0{,}02;\ 0{,}03)$): $L_D(h_3)=a(1)+a(2)+b(3)+\cdots+b(6)=0{,}04+0{,}25=0{,}29$; $L_D(h_6)=a(1)+\cdots+a(5)+b(6)=0{,}42+0{,}03=0{,}45$; $L_D(h_4)=0{,}12+0{,}13=0{,}25$, nhỏ nhất. Rủi ro vượt mức $0{,}04$ và $0{,}20$. Khớp lời giải.

**V8. Hàm phân lớp ghi nhớ trên $[0,1]$** (Ví dụ 01.8, Mệnh đề 01.15). Không có phép tính số ngoài $L_S=0$, $L_D=1$, $L_D(h_{\equiv1})=0$. Hình F4 dùng năm điểm minh họa $0{,}12;\ 0{,}31;\ 0{,}47;\ 0{,}68;\ 0{,}90$ (chỉ để vẽ; ghi chú cho $m$ tùy ý; mục 11, điểm 9).

**V9. Hàm phân lớp ghi nhớ khi phân bố có nguyên tử** (Ví dụ 01.11; trang 6-04). $D_1$: $D_{\mathcal X}$ đều trên $\{1,\ldots,5\}$, $Y=1$. $A_{\mathrm{gn}}(S)=\mathbb 1[x\in\{X_1,\ldots,X_m\}]$, sai đúng tại điểm vắng mặt; mỗi điểm vắng mặt với xác suất $0{,}8^m$; $\mathbb E L=5\cdot0{,}2\cdot0{,}8^m=0{,}8^m$. $m=10$: $0{,}8^{10}=0{,}1073741824\approx0{,}107$. Tính lại: $0{,}8^5=0{,}32768$, bình phương $0{,}10737$. Đúng.

**V9b. Bài tập 01.4(a)** (bài tập 4-05; số liệu và kết quả của `exercises.md`). $X\sim U[0,1]$, $f(x)=\mathbb 1[x>0{,}7]$: $L_S(A_{\mathrm{gn}}(S))=0$; $L_D(A_{\mathrm{gn}}(S))=\Pr(f(X)=1)-\Pr(X\in F,f(X)=1)=0{,}3-0=0{,}3$; hàm hằng $0$ có rủi ro $\Pr(X>0{,}7)=0{,}3$; $f$ có rủi ro $0$. Khớp lời giải.

**V10. Thiên kiến quy nạp trên $\tilde S_f$** (ghi chú §5 cuối). $A_{\mathrm{gn}}(\tilde S_f)=\mathbb 1[x\in\{3,5\}]$: tại $x=2$ báo $0=f(2)$, tại $x=4$ báo $0\ne f(4)=1$, nên rủi ro $0{,}2$. Trong lớp hàm ngưỡng: $h_2$ ($0{,}2$), $h_3$ ($0$), cả hai báo $1$ tại $x=4$. Trên $S_f$: $A_{\mathrm{gn}}(S_f)=\mathbb 1[x\in\{4,5\}]=h_4\in\mathcal H$. Đúng.

**V11. Vai trò của $\delta$ và $\epsilon$** (ghi chú §6 đầu). $S$ bỏ sót mức 3 dưới $D_f$ với xác suất $0{,}8^m>0$. Mức có khối lượng $0{,}001$, $m=500$: $0{,}999^{500}=e^{500\ln0{,}999}=e^{-0{,}50025}\approx0{,}606$, ghi chú làm tròn $\approx0{,}61$. Đúng.

**V12. Xác suất thất bại và cỡ mẫu của $A_{\max}$ dưới $D_f$** (Ví dụ 01.9; trang 5-05; Bài tập 01.5(d) ở 5-06 dùng cùng số $14$).
- $L_{D_f}(A_{\max}(S))=0{,}2(\hat t-3)\in\{0;\ 0{,}2;\ 0{,}4;\ 0{,}6\}$; $\Pr[L>0]=0{,}8^m$.
- $\epsilon=0{,}1$: thành công khi và chỉ khi $L=0$; $0{,}8^{13}=0{,}05498>0{,}05$, $0{,}8^{14}=0{,}04398\le0{,}05$, nên $m\ge14$. Tính lại: $0{,}8^{7}=0{,}2097152$, bình phương $0{,}043980$; chia $0{,}8$ được $0{,}054976$. Đúng.
- $\epsilon=0{,}25$: thất bại khi và chỉ khi $\hat t\ge5$, tức vắng cả $3$ và $4$; xác suất $0{,}6^m$; $0{,}6^5=0{,}07776$, $0{,}6^6=0{,}046656$, nên $m\ge6$. Tính lại: $0{,}6^3=0{,}216$, bình phương $0{,}046656$. Đúng.
- Đọc theo các lần lặp: ở $m=14$, khoảng $4{,}4\%$ số tập huấn luyện cho hàm có rủi ro ít nhất $0{,}2$.
- Kì vọng ($m=10$): $0{,}2(0{,}10737+0{,}00605+0{,}00010)=0{,}2\cdot0{,}11353\approx0{,}0227$ (chỉ ở ghi chú diễn giả).

**V13. Không khả diễn và rủi ro Bayes** (Nhận xét 01.17, Ví dụ 01.10; trang 5-07, 5-08, 5-10).
- Tại $x=2$: mọi $g$ sai với xác suất ít nhất $0{,}2\cdot\min\{\tfrac14,\tfrac34\}=0{,}05$.
- $\min\{\eta,1-\eta\}=(0,\tfrac14,\tfrac14,\tfrac25,0)$, tổng $0{,}9$, $L^{\mathrm{Bayes}}_{D_\eta}=0{,}18$; $h_{\mathrm{Bayes}}=\mathbb 1[x\in\{3,5\}]$ ($\eta(3)=\tfrac34$, $\eta(5)=1$ không nhỏ hơn $\tfrac12$; $\eta(4)=\tfrac25<\tfrac12$).
- Dưới $\ell_c$: ngưỡng $\tfrac1{1+4}=\tfrac15$; $\eta(x)\ge\tfrac15$ tại $x=2,3,4,5$; hàm Bayes $h_2$. Rủi ro: $0{,}2(0+\tfrac34+\tfrac14+\tfrac35+0)=0{,}32$. Tính lại theo công thức $\mathbb E\min\{4\eta,1-\eta\}$: $(0;\ \tfrac34;\ \tfrac14;\ 0{,}6;\ 0)$, tổng $1{,}6$, nhân $0{,}2$ được $0{,}32$. Khớp, và bằng $\min_tL^c_{D_\eta}(h_t)$ ở V2.

**V14. Phân rã rủi ro vượt mức** (sau Định nghĩa 01.24; trang 5-11, hình F6). $h=h_2$ dưới $\ell_{0\text{-}1}$: $0{,}32-0{,}22=0{,}10$; $0{,}22-0{,}18=0{,}04$; $0{,}32-0{,}18=0{,}14=0{,}10+0{,}04$. Kiểm tra bằng công thức của Phụ lục B cho $h_3$: $h_3$ khác $h_{\mathrm{Bayes}}$ chỉ tại $x=4$, $0{,}2\lvert2\cdot0{,}4-1\rvert=0{,}04$. Khớp.

**V15. Cỡ mẫu chung của $A_{\max}$** (sau Mệnh đề 01.31; trang 6-05, 6-06, 6-07). $\epsilon=0{,}1$, $\delta=0{,}05$: $\ln20=2{,}995732$, $10\ln20=29{,}957$, trần $30$. Kiểm tra: $e^{-0{,}1\cdot30}=e^{-3}=0{,}0498\le0{,}05$; $e^{-2{,}9}=0{,}0550>0{,}05$. Đúng.

**V16 (không dùng trong deck cuối; câu hỏi tự kiểm tra 4 đã viết lại theo quyết định của điều phối viên, xem trang 7-04). Câu hỏi tự kiểm tra 4 cũ** (trang 7-04). $14\le m_{A_{\max}}(0{,}1;\ 0{,}05)\le30$. Cận dưới: $D_f$ là một phân bố khả diễn mà tại $m=13$ xác suất thất bại $0{,}05498>0{,}05$ (V12), nên mọi $m_0$ trong Định nghĩa 01.20 phải lớn hơn $13$. Cận trên: Mệnh đề 01.31 với $K=5$. Hai cận chỉ dùng ghi chú.

## 6. Danh sách trang

Mỗi mục: ID, tiêu đề, loại, thời lượng; **Mặt trang** (các dòng dự kiến, theo thứ tự; `[f]` là fragment); **Ghi chú diễn giả** (ý chính, 40–150 âm tiết, đến ~250 cho trang ý tưởng chứng minh; luôn kết thúc bằng dòng `note-source`); **Lý do / nối**; **Mục tiêu / nguồn**. Câu trên mặt trang là bản dự kiến đã tự kiểm theo `no-ai-slop` (chế độ Edit) và `eval.md`; người viết deck có thể rút gọn, không thêm khẳng định.

Quy ước chung cho người viết deck:
- Thuật ngữ tiếng Anh trong ngoặc ở lần dùng đầu tiên trên một trang nội dung (từ 1-02 trở đi). Trang bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm" là trang tổng quan, không kèm tiếng Anh (mục 11, điểm 4).
- Số thập phân dùng dấu phẩy KaTeX `0{,}2`; dãy số có dấu phẩy thập phân ngăn bằng `;\ `.
- Mỗi trang ví dụ mở bằng dữ kiện dạng danh sách, không câu dẫn.

### Mạch 1. Mở đầu (6 trang, 8 phút)

#### `1-01` Mô hình học: rủi ro, tối thiểu hóa rủi ro thực nghiệm và học PAC — bìa, điểm vào mạch 1 · 1 phút
- **Mặt trang:** h1 tên bài; h3 "Bài 01"; luận điểm (mục 2); "Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1"; "Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN".
- **Ghi chú diễn giả:** Luận điểm có ba thành phần: ngưỡng $\epsilon$ cho rủi ro kì vọng so với mức tốt nhất trong lớp, xác suất thất bại $\delta$ theo tập huấn luyện, và cỡ mẫu đủ không phụ thuộc phân bố. Rủi ro thực nghiệm nhỏ không có mặt trong yêu cầu này; mạch 4 và 6 chỉ ra vì sao. Nguồn: ghi chú Bài 01, đoạn mở đầu, §7 (đoạn cuối).
- **Lý do / nối:** nêu luận điểm cả bài → tiên quyết.
- **Mục tiêu / nguồn:** tất cả; ghi chú đoạn mở, §7.
- **Bản deck cuối (2026-11-15):** luận điểm trên bìa viết bằng lời, không kí hiệu: "Học là chọn từ tập huấn luyện một hàm dự đoán có rủi ro kì vọng gần mức tốt nhất trong lớp giả thuyết, với xác suất cao, khi cỡ mẫu vượt một ngưỡng không phụ thuộc phân bố." Lý do: quy định trang tổng quan dùng lời, không kí hiệu mới (`CLAUDE.md` § Slide decks). Câu luận điểm 39 âm tiết trong một khối (ngoại lệ dòng 20 âm tiết của trang bìa, xem mục 14).

#### `1-02` Tiên quyết và quy ước — mở đầu · 1,5 phút
- **Mặt trang:**
  - **Nhắc lại:** tính tuyến tính của kì vọng; $\mathbb E[\mathbb E[U\mid X]]=\mathbb E[U]$; cận dưới đúng (infimum) $\inf$; $U[0,1]$; $1-x\le e^{-x}$.
  - Hầu chắc chắn (almost surely): đúng ngoài một biến cố có xác suất $0$.
  - **Ký hiệu:** $\mathcal Z=\mathcal X\times\mathcal Y$, $S=(Z_1,\ldots,Z_m)\sim D^m$, $\eta(x)=\Pr(Y=1\mid X=x)$, $D_{\mathcal X}$ phân bố biên (marginal distribution) của $X$.
  - ERM: tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization).
  - PAC: học xấp xỉ với xác suất cao (probably approximately correct).
  - ≈ 45 âm tiết.
- **Ghi chú diễn giả:** Ba câu ôn nhanh của ghi chú dùng lại trong bài: $\Pr(X\in\{0{,}1;\ 0{,}5;\ 0{,}9\})=0$ dưới $U[0,1]$ (mạch 4); $\mathbb E[(Z_1+Z_2)/2]=\mu$ dù $Z_2=Z_1$ (mạch 3); xác suất $m$ lần rút đều không ra số 3 là $0{,}8^m$ (mạch 5). Hai giả thiết thống kê của bài: (T1) $Z_1,\ldots,Z_m$ i.i.d. theo $D$; (T2) $\ell\ge0$, $\ell(h,\cdot)$ đo được. Định nghĩa thuật toán học của ghi chú có thêm điều kiện đo được theo $(s,z)$ để $L_D(A(S))$ là biến ngẫu nhiên. Nguồn: ghi chú Bài 01, Kiến thức tiên quyết, §2.
- **Lý do / nối:** công cụ và kí hiệu trước mọi định nghĩa; giải nghĩa hai chữ viết tắt trước khi trang "Mục tiêu" dùng → mục tiêu.
- **Mục tiêu / nguồn:** tất cả; Kiến thức tiên quyết, §2.
- **Bản deck cuối (2026-11-15):** sáu dòng: "Nhắc lại:" (tính tuyến tính, kì vọng lặp, $\inf$ (infimum), $U[0,1]$, $1-x\le e^{-x}$); "Ký hiệu:" ($z$, $\mathcal Z$, phân bố biên (marginal distribution) $D_{\mathcal X}$, $\eta$); dòng (T1); dòng (T2); dòng ERM; dòng PAC. Lý do: nhãn (T1), (T2) xuất hiện trên mặt trang 3-02, 6-02, 6-05, 7-01 nên phải được nêu trước (quy định "định nghĩa hoặc nhắc lại trước khi dùng"); "hầu chắc chắn (almost surely)" chuyển sang trang dùng lần đầu (4-02) để giữ trần 60 (60 âm tiết).

#### `1-03` Mục tiêu — mở đầu · 1 phút
- **Mặt trang** (danh sách đánh số, ≈ 72 âm tiết, trần 80):
  1. Phát biểu bài toán học thống kê; tách đại lượng cố định và đại lượng ngẫu nhiên.
  2. Tính $L_D$, $L_S$, tập nghiệm ERM, rủi ro Bayes, rủi ro vượt mức; tìm ngưỡng khi chi phí bất đối xứng.
  3. Chứng minh tính không chệch của $L_S(h)$ với $h$ cố định.
  4. Viết định nghĩa học PAC khả diễn, bất khả diễn; phân biệt $m_A$ với $m_{\mathcal H}$.
  5. Dựng phản ví dụ hàm phân lớp ghi nhớ; giải thích vai trò của thiên kiến quy nạp.
- **Ghi chú diễn giả:** Năm mục tiêu rút gọn từ ghi chú. Mục tiêu 2, 3 kiểm tra ở mạch 2–3 và 5; mục tiêu 4 ở mạch 5; mục tiêu 5 ở mạch 4 và 6. Bài tập 01.1–01.11 ghi mục tiêu tương ứng trong tệp bài tập. Nguồn: ghi chú Bài 01, Mục tiêu học tập, §10.
- **Lý do / nối:** tiêu chí kiểm tra → nội dung.
- **Mục tiêu / nguồn:** tất cả; Mục tiêu học tập.
- **Bản deck cuối (2026-11-15):** năm mục tiêu bằng lời, không kí hiệu (quyết định của điều phối viên, mục 11.14): (1) Phát biểu bài toán học thống kê; tách đại lượng cố định, đại lượng ngẫu nhiên. (2) Tính rủi ro kì vọng, thực nghiệm, Bayes, vượt mức và tập nghiệm ERM. (3) Chứng minh tính không chệch của rủi ro thực nghiệm với giả thuyết cố định. (4) Định nghĩa học PAC khả diễn, bất khả diễn; độ phức tạp mẫu của thuật toán, của lớp. (5) Dựng phản ví dụ hàm phân lớp ghi nhớ; giải thích vai trò thiên kiến quy nạp. 80 âm tiết (trần 80). Phần "tìm ngưỡng khi chi phí bất đối xứng" chuyển sang ghi chú diễn giả.

#### `1-04` Nội dung — mở đầu · 0,5 phút
- **Mặt trang:** `ol start="2"` với liên kết `#/2`…`#/7`: 2. Bài toán học thống kê; 3. Rủi ro thực nghiệm và tối thiểu hóa rủi ro thực nghiệm; 4. Thuật toán ghi nhớ và thiên kiến quy nạp; 5. Học PAC; 6. Rủi ro thực nghiệm nhỏ và bảo đảm học; 7. Tổng kết. Dòng đọc trước: "Đọc trước: UML §§2.1–2.2."
- **Ghi chú diễn giả:** Mạch 2 đặt bài toán, mạch 3 đưa ra đại lượng tính được và quy tắc ERM, mạch 4 cho phản ví dụ, mạch 5 phát biểu bảo đảm học, mạch 6 nối phản ví dụ với bảo đảm. Nguồn: ghi chú Bài 01; §12.
- **Lý do / nối:** bản đồ mạch → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; ghi chú toàn bài, §12.
- **Bản deck cuối (2026-11-15):** bỏ dòng "Đọc trước: UML §§2.1–2.2." khỏi mặt trang ("Đọc trước:" không thuộc danh sách nhãn hợp lệ); tài liệu đọc trước nằm ở ghi chú diễn giả và trang Tài liệu tham khảo.

#### `1-05` Vấn đề trung tâm — mở đầu · 1 phút
- **Mặt trang:** một hộp `div.box`: "Câu hỏi: học có nghĩa là gì, tức khi nào một hàm dự đoán chọn từ tập huấn luyện được xem là đã học được?" (≈ 27 âm tiết).
- **Ghi chú diễn giả** (câu trả lời có điều kiện theo mạch, chuyển khỏi mặt trang theo quyết định 2026-11-14): (2) mục tiêu là $L_D(A(S))-\inf_{h}L_D(h)$ nhỏ khi không biết $D$; (3) $L_S(h)$ ước lượng không chệch $L_D(h)$ chỉ khi $h$ không phụ thuộc $S$; (4) một nghiệm ERM có thể có $L_S=0$ và $L_D=1$; (5) học là bảo đảm $L_D(A(S))\le\inf_hL_D(h)+\epsilon$ với xác suất ít nhất $1-\delta$ khi $m\ge M(\epsilon,\delta)$, $M$ không phụ thuộc $D$; (6) $L_S$ nhỏ không đủ; cấu trúc lớp hàm ngưỡng cho $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$. Nguồn: ghi chú Bài 01, đoạn mở đầu, §7, §8, §9.
- **Lý do / nối:** một vấn đề cốt lõi → câu hỏi mở đầu làm cụ thể vấn đề.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu.
- **Bản deck cuối (2026-11-15):** đúng storyboard. Ghi chú diễn giả liệt kê câu trả lời theo tên phần (không theo số mạch). Hộp 25 âm tiết trong một khối (ngoại lệ dòng 20 âm tiết, xem mục 14).

#### `1-06` Ví dụ: hai hàm phân lớp cùng khớp tập huấn luyện — ví dụ dẫn nhập · 3 phút
- **Mặt trang:**
  - Chỉ số $x\in\{1,\ldots,5\}$, mỗi mức chiếm $20\%$ dân số; có bệnh ($y=1$) khi và chỉ khi $x\ge3$.
  - Tập huấn luyện (training sample) $S_f$: $(1,0)$, $(2,0)$, $(4,1)$, $(5,1)$.
  - Hai hàm phân lớp (classifier): $h_3(x)=\mathbb 1[x\ge3]$, $h_4(x)=\mathbb 1[x\ge4]$.
  - Hình F1 (`img/lec-01/hai-ham-nguong.svg`), cột phải của `grid2`.
  - **Câu hỏi:** hiệu quả của hai hàm phân lớp này như thế nào?
  - `[f]` Cả hai khớp mọi quan sát của $S_f$; trên toàn dân số, $h_4$ sai ở mức 3, tức với xác suất $0{,}2$.
  - ≈ 55 âm tiết.
- **Ghi chú diễn giả:** $\mathbb 1[p]$ là hàm chỉ báo (indicator). Chỉ số dưới của $h$ là ngưỡng báo dương tính. $S_f$ không có người nào ở mức 3, nên tập huấn luyện không phân biệt được $h_3$ với $h_4$; hai hàm chỉ khác nhau tại $x=3$. Câu hỏi mở đầu làm cụ thể vấn đề trung tâm: cùng khớp tập huấn luyện vẫn có thể khác nhau trên quan sát mới. Mạch 3 (quy tắc chọn khi bằng nhau) và mạch 5 (xác suất bỏ sót mức 3 là $0{,}8^m$) trả lời câu hỏi này. Nguồn: ghi chú Bài 01, Câu hỏi mở đầu; §11.
- **Lý do / nối:** ví dụ dẫn nhập trước mọi định nghĩa → tiêu đề mạch 2.
- **Mục tiêu / nguồn:** 1, 5; Câu hỏi mở đầu.
- **Bản deck cuối (2026-11-15):** hai dòng dữ kiện toàn bề rộng (mức, $20\%$, $y=1$ khi $x\ge3$; $S_f$ và $h_3$, $h_4$ chung một dòng), rồi `grid2 wide-right` với "Câu hỏi:" và câu trả lời `[f]` bên trái, hình F1 bên phải. Lý do: bố cục `grid2` hai cột đều làm tràn khung; chữ trong hình đạt 19 px.

### Mạch 2. Bài toán học thống kê (6 trang, 15 phút)

#### `2-00` 2. Bài toán học thống kê — tiêu đề mạch, điểm vào mạch 2 · 0,5 phút
- **Mặt trang:** `span.strand-number` "2."; h2 "Bài toán học thống kê"; `p.strand-lead` (bảng mạch); `p.strand-keys` "tám thành phần · rủi ro kì vọng · hàm lỗi có trọng số · mục tiêu so với lớp giả thuyết".
- **Ghi chú diễn giả:** Kế thừa: câu hỏi mở đầu với hai hàm cùng khớp $S_f$. Nhiệm vụ: viết bài toán thành tám thành phần và đo chất lượng của hàm dự đoán bằng rủi ro kì vọng. Trao cho mạch 3: mục tiêu $L_D(A(S))-\inf_{h\in\mathcal H}L_D(h)$ và việc $L_D$ không tính được vì $D$ chưa biết. Nguồn: ghi chú Bài 01, §1, §3, §4.
- **Lý do / nối:** câu hỏi mở đầu → tám thành phần.
- **Mục tiêu / nguồn:** 1, 2; §1, §3, §4.

#### `2-01` Thành phần của một bài toán học — định nghĩa (khung) · 2,5 phút
- **Mặt trang:**
  - Quan sát (example) $z=(x,y)\in\mathcal Z=\mathcal X\times\mathcal Y$, lấy mẫu từ phân bố $D$ chưa biết.
  - Tập huấn luyện $S\sim D^m$, cỡ mẫu (sample size) $m$.
  - Lớp giả thuyết (hypothesis class) $\mathcal H$ và hàm lỗi (loss function) $\ell\ge0$ chọn trước khi lấy mẫu.
  - Thuật toán học (learning algorithm) $A$ chỉ dùng $S$, trả về $A(S)\in\mathcal H$ có rủi ro kì vọng $L_D(A(S))$ nhỏ.
  - Hộp `div.box`: **Lưu ý:** $D$, $\mathcal H$, $\ell$, $A$ cố định; $S$, $A(S)$, $L_D(A(S))$ ngẫu nhiên theo $S\sim D^m$.
  - ≈ 52 âm tiết.
- **Ghi chú diễn giả:** Đây là tám thành phần của ghi chú §1, gộp thành bốn dòng: tập đầu vào (input space), tập nhãn (label set), phân bố liên hợp (joint distribution) $D$, tập huấn luyện i.i.d., lớp giả thuyết, hàm lỗi, thuật toán học, mục tiêu và tài nguyên $m$. Vì $D$ là phân bố liên hợp, cùng một $x$ có thể đi với hai nhãn; hàm gán nhãn (labeling function, target function) $f$ là trường hợp riêng $D(Y=f(x)\mid X=x)=1$. Một quy tắc cần biết $D$ để chạy không phải là thuật toán học. Khi thuật toán sinh thêm đại lượng ngẫu nhiên $\xi$ (lấy mẫu mini-batch), $A(S;\xi)$ ngẫu nhiên theo cả $S$ và $\xi$. Nguồn: ghi chú Bài 01, §1 (danh sách và bảng nguồn ngẫu nhiên).
- **Lý do / nối:** khung chung cho mọi bài sau → ví dụ sàng lọc điền tám thành phần.
- **Mục tiêu / nguồn:** 1; §1.
- **Bản deck cuối (2026-11-15):** dòng 4 không dùng $L_D$ (chưa định nghĩa): "Thuật toán học (learning algorithm) $A$ chỉ dùng $S$, trả về hàm dự đoán (predictor) $A(S)\in\mathcal H$." Ý "sai ít trên quan sát mới" ở ghi chú diễn giả. Dòng 2 rút còn "Tập huấn luyện $S\sim D^m$, cỡ mẫu (sample size) $m$." Lý do: phát hiện nhẹ của cổng duyệt (2-01) và trần 60 (57 âm tiết).

#### `2-02` Ví dụ: sàng lọc theo ngưỡng trên năm mức đo — ví dụ (ví dụ xuyên suốt) · 2,5 phút
- **Mặt trang:**
  - $\mathcal X=\{1,\ldots,5\}$, $D_{\mathcal X}(x)=0{,}2$; $\mathcal Y=\{0,1\}$, $y=1$ là có bệnh.
  - Lớp hàm ngưỡng $\mathcal H=\{h_t=\mathbb 1[x\ge t]:\ t=1,\ldots,6\}$, với $h_1\equiv1$ và $h_6\equiv0$.
  - Hàm lỗi 0–1 (0–1 loss) $\ell_{0\text{-}1}(h,(x,y))=\mathbb 1[h(x)\ne y]$.
  - Bảng ba hàng: $x$ | $1$ | $2$ | $3$ | $4$ | $5$; $\eta(x)$ | $0$ | $\tfrac14$ | $\tfrac34$ | $\tfrac25$ | $1$; $f(x)$ | $0$ | $0$ | $1$ | $1$ | $1$.
  - Dữ liệu có nhiễu, từ $D_\eta$: $S_\eta=((1,0),(2,0),(2,1),(3,1),(4,0),(5,1))$.
  - Dữ liệu tất định, từ $D_f$ với $f=h_3$: $S_f=((1,0),(2,0),(4,1),(5,1))$.
  - ≈ 40 âm tiết.
- **Ghi chú diễn giả:** Phân bố liên hợp $D(x,y)=D_{\mathcal X}(x)D(y\mid x)$. Bản có nhiễu $D_\eta(y\mid x)=\eta(x)^y(1-\eta(x))^{1-y}$; bản tất định đặt toàn bộ xác suất vào $y=f(x)$. Tại $x=2$, $S_\eta$ có cả nhãn $0$ và nhãn $1$, nên không hàm nào khớp mọi quan sát của $S_\eta$. $S_f$ chính là tập huấn luyện của câu hỏi mở đầu. Ví dụ đủ nhỏ để tính tay mọi đại lượng của bài. Nguồn: ghi chú Bài 01, §3, Ví dụ 01.1.
- **Lý do / nối:** dữ kiện xuyên suốt, nêu ngay dạng danh sách → rủi ro kì vọng.
- **Mục tiêu / nguồn:** 1, 2; Ví dụ 01.1.

#### `2-03` Rủi ro kì vọng và hai loại lỗi — trực quan, định nghĩa · 3 phút
- **Mặt trang:**
  - **Trực quan.** Chất lượng của $h$ đo trên quan sát mới $Z\sim D$, độc lập với $S$.
  - Rủi ro kì vọng (population risk, expected risk) của $h$: display $L_D(h)=\mathbb E_{Z\sim D}\,\ell(h,Z)$.
  - Với $\ell_{0\text{-}1}$: $L_D(h)=\Pr(h(X)\ne Y)$, xác suất lỗi của $h$.
  - Âm tính giả (FN) có chi phí $c_{FN}=4$, dương tính giả (FP) có chi phí $c_{FP}=1$; hàm lỗi có trọng số (cost-weighted loss): display $\ell_c\big(h,(x,y)\big)=c_{FN}\mathbb 1[y=1,\ h(x)=0]+c_{FP}\mathbb 1[y=0,\ h(x)=1]$, rủi ro $L_D^c$.
  - **Câu hỏi:** tại sao không nên đo chất lượng của hàm dự đoán trên tập huấn luyện?
  - ≈ 56 âm tiết; hai công thức hiển thị.
- **Ghi chú diễn giả:** Với $h$ cho trước, $L_D(h)$ là một số, không phải biến ngẫu nhiên, nhưng chưa biết vì chưa biết $D$. Âm tính giả (false negative) là báo âm tính cho người bệnh, dương tính giả (false positive) là báo dương tính cho người khỏe; với $(c_{FP},c_{FN})=(1,4)$, bỏ sót một người bệnh đắt gấp bốn lần đưa một người khỏe đi xét nghiệm thêm. Khi $c_{FP}=c_{FN}=1$, $\ell_c$ là $\ell_{0\text{-}1}$. Cùng khung áp dụng cho hồi quy: hàm lỗi bình phương $(h(x)-y)^2$ với lớp tuyến tính có $L_D(h_w)\le2\lVert w\rVert^2\mathbb E\lVert X\rVert^2+2\mathbb EY^2$, hữu hạn khi tồn tại mô-men bậc 2 (Ví dụ 01.3); với hàm lỗi không bị chặn, bài chỉ xét phân bố có rủi ro hữu hạn trên $\mathcal H$ (Định nghĩa 01.3). Câu hỏi được trả lời ở trang khoảng cách tổng quát hóa của mạch 3. Khối ứng dụng của ghi chú §3 còn đặt câu hỏi thực hành "nên đặt ngưỡng báo dương tính ở đâu khi hai loại lỗi có chi phí khác nhau"; ví dụ quy tắc Bayes dưới $\ell_c$ ở mạch 5 trả lời câu này. Nguồn: ghi chú Bài 01, §3 (khối ứng dụng), §4, Định nghĩa 01.1, 01.3, Ví dụ 01.3.
- **Lý do / nối:** định nghĩa đại lượng mục tiêu, kèm hàm lỗi thứ hai cho ví dụ → tính $L_D(h_t)$.
- **Mục tiêu / nguồn:** 1, 2; §3, Định nghĩa 01.1.
- **Bản deck cuối (2026-11-15):** dòng FN/FP viết đủ tên tiếng Anh: "Chi phí âm tính giả (false negative, FN) $c_{FN}=4$, dương tính giả (false positive, FP) $c_{FP}=1$." (phát hiện nhẹ của cổng duyệt); $L_D^c(h)=\mathbb E_{Z\sim D}\ell_c(h,Z)$ viết bằng công thức; "$L_D(h)=\Pr(h(X)\ne Y)$ với hàm lỗi 0–1" chuyển sang ghi chú diễn giả. 60 âm tiết, 6 dòng.

#### `2-04` Ví dụ: rủi ro kì vọng của các hàm ngưỡng — ví dụ · 3,5 phút
- **Mặt trang:**
  - $h_t$ sai tại mức $x<t$ khi $Y=1$ và tại mức $x\ge t$ khi $Y=0$, nên
  - display $L_{D_\eta}(h_t)=0{,}2\Big[\sum_{x<t}\eta(x)+\sum_{x\ge t}\big(1-\eta(x)\big)\Big]$.
  - $L_{D_\eta}(h_3)=0{,}2\,(0{,}25+0{,}85)=0{,}22$; $L^c_{D_\eta}(h_3)=0{,}2\,(4\cdot0{,}25+0{,}85)=0{,}37$.
  - **Câu hỏi:** tính $L^c_{D_\eta}(h_2)$.
  - `[f]` **Lời giải:** $0{,}2\,(4\cdot0+1{,}6)=0{,}32$.
  - `[f]` Bảng hai hàng theo $t=1,\ldots,6$: $L_{D_\eta}(h_t)$ = $0{,}52;\ 0{,}32;\ \mathbf{0{,}22};\ 0{,}32;\ 0{,}28;\ 0{,}48$; $L^c_{D_\eta}(h_t)$ = $0{,}52;\ \mathbf{0{,}32};\ 0{,}37;\ 0{,}92;\ 1{,}12;\ 1{,}92$.
  - `[f]` **Diễn giải:** dưới $\ell_{0\text{-}1}$ hàm tốt nhất là $h_3$; dưới $\ell_c$ là $h_2$.
  - ≈ 32 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Tổng thứ nhất là khối lượng nhãn 1 bị bỏ sót, tổng thứ hai là khối lượng nhãn 0 bị báo nhầm; dưới $\ell_c$ tổng thứ nhất nhân $c_{FN}$, tổng thứ hai nhân $c_{FP}$. Tại $t=2$, tổng bỏ sót bằng $0$ và tổng báo nhầm bằng $\tfrac34+\tfrac14+\tfrac35+0=1{,}6$. Khi bỏ sót đắt gấp bốn, báo dương tính thêm cho mức 2 (nơi $\eta(2)=\tfrac14$) làm chi phí giảm từ $0{,}37$ xuống $0{,}32$. Hai hàm lỗi chọn ra hai hàm tốt nhất khác nhau, nên hàm lỗi là một phần của bài toán, không phải của hàm dự đoán. Nguồn: ghi chú Bài 01, Ví dụ 01.2, Phụ lục C.1.
- **Lý do / nối:** con số $0{,}22$ là mức tốt nhất trong lớp, dùng lại ở 2-05, 3-04, 5-08, 5-11 → mục tiêu của bài toán học.
- **Mục tiêu / nguồn:** 2; Ví dụ 01.2.
- **Bản deck cuối (2026-11-15):** công thức $L^c_{D_\eta}(h_3)=0{,}37$ trên mặt trang chỉ ghi kết quả, phép tính đầy đủ ở ghi chú diễn giả; "Diễn giải:" và bảng đặt cạnh nhau (`grid2 wide-right`) để không tràn khung. Ghi chú diễn giả viết dạng khẳng định: "Hàm lỗi chọn hàm tốt nhất: $h_3$ dưới $\ell_{0\text{-}1}$, $h_2$ dưới $\ell_c$" (phát hiện Detect của cổng duyệt).

#### `2-05` Mục tiêu của bài toán học thống kê — định nghĩa, ví dụ · 3 phút
- **Mặt trang:**
  - Thuật toán $A$ chọn trước khi lấy mẫu, không phụ thuộc $D$; cần hiệu sau nhỏ:
  - display $L_D\big(A(S)\big)-\inf_{h\in\mathcal H}L_D(h)$.
  - **Ví dụ.** Dưới $D_\eta$: chọn $\hat t=\hat t(S)$ từ $S$ cỡ $6$ để $L_{D_\eta}(h_{\hat t})-0{,}22$ nhỏ.
  - Dưới $D_f$, trên $S_f$: $h_3$, $h_4$ cùng khớp, với $L_{D_f}(h_3)=0$, $L_{D_f}(h_4)=0{,}2$.
  - **Câu hỏi:** hiệu trên nhỏ đến đâu, với xác suất nào theo $S$, trên họ phân bố nào?
  - ≈ 49 âm tiết.
- **Ghi chú diễn giả:** Đây là bài toán học thống kê (statistical learning problem) của Định nghĩa 01.5. Hiệu không âm vì $A(S)\in\mathcal H$. Tóm lại, mục tiêu là tối thiểu hóa rủi ro kì vọng trên $\mathcal H$ khi không tính được $L_D$. Vì $S$ ngẫu nhiên, $A(S)$ và hiệu cũng ngẫu nhiên: một tập $S$ khác rút từ $D_\eta^6$ có thể cho ngưỡng khác. Ba câu hỏi trên mặt trang là ba câu hỏi chính của Học thống kê; mạch 5 trả lời cả ba bằng $\epsilon$, $\delta$ và họ phân bố. Hiệu không tính được vì $L_D$ là kì vọng theo $D$ chưa biết; mạch 3 thay $L_D$ bằng một đại lượng tính được từ $S$. Nguồn: ghi chú Bài 01, Định nghĩa 01.5, Ví dụ 01.4.
- **Lý do / nối:** đặt mục tiêu và ba câu hỏi → tiêu đề mạch 3 ($L_D$ không tính được).
- **Mục tiêu / nguồn:** 1; Định nghĩa 01.5, Ví dụ 01.4.
- **Bản deck cuối (2026-11-15):** đúng storyboard; ghi chú diễn giả bỏ câu dẫn trước về định nghĩa học PAC.

### Mạch 3. Rủi ro thực nghiệm và tối thiểu hóa rủi ro thực nghiệm (8 trang, 21 phút)

#### `3-00` 3. Rủi ro thực nghiệm và tối thiểu hóa rủi ro thực nghiệm — tiêu đề mạch, điểm vào mạch 3 · 0,5 phút
- **Mặt trang:** "3."; h2 tên mạch; `p.strand-lead` (bảng mạch); `p.strand-keys` "rủi ro thực nghiệm · ước lượng không chệch · khoảng cách tổng quát hóa · quy tắc chọn khi bằng nhau".
- **Ghi chú diễn giả:** Kế thừa: mục tiêu $L_D(A(S))-\inf_hL_D(h)$, không tính được vì $D$ chưa biết. Nhiệm vụ: thay $L_D$ bằng trung bình hàm lỗi trên $S$, xác định khi nào phép thay đúng theo kì vọng, rồi chọn giả thuyết theo đại lượng này. Trao cho mạch 4: khi có nhiều nghiệm ERM, quy tắc chọn khi bằng nhau quyết định rủi ro kì vọng. Nguồn: ghi chú Bài 01, §5.
- **Lý do / nối:** $L_D$ không tính được → định nghĩa $L_S$ trên ví dụ.
- **Mục tiêu / nguồn:** 2, 3; §5.

#### `3-01` Ví dụ: cùng rủi ro thực nghiệm, khác rủi ro kì vọng — định nghĩa, ví dụ · 3 phút
- **Mặt trang:**
  - Rủi ro thực nghiệm (empirical risk) trên $S=(z_1,\ldots,z_m)$: display $L_S(h)=\frac1m\sum_{i=1}^m\ell(h,z_i)$.
  - Trên $S_\eta$: $h_3$ sai trên $(2,1)$ và $(4,0)$, nên $L_{S_\eta}(h_3)=\tfrac26=\tfrac13$.
  - Hình F3 (`img/lec-01/rui-ro-nguong.svg`): $L_{S_\eta}(h_t)$ và $L_{D_\eta}(h_t)$ theo $t$.
  - **Diễn giải:** $h_2$, $h_3$, $h_5$ cùng có $L_{S_\eta}=\tfrac13$, nhưng $L_{D_\eta}$ lần lượt là $0{,}32$, $0{,}22$, $0{,}28$.
  - ≈ 35 âm tiết.
- **Ghi chú diễn giả:** $L_S(h)$ là rủi ro kì vọng dưới phân bố thực nghiệm (empirical distribution), gán xác suất $\tfrac1m$ cho mỗi lần xuất hiện của một quan sát trong $S$; với hàm lỗi 0–1 đó là tỉ lệ lỗi (error rate) trên tập huấn luyện. Số lỗi của $h_1,\ldots,h_6$ trên $S_\eta$ là $3,2,2,3,2,3$. Nếu chỉ dựa vào $L_{S_\eta}$, không phân biệt được hàm tốt nhất $h_3$ với $h_2$, $h_5$. Đọc hình: hai dãy điểm khác ký hiệu (tròn cho $L_S$, vuông cho $L_D$), ba ngưỡng có cùng $L_S$ được đánh dấu. Nguồn: ghi chú Bài 01, Định nghĩa 01.6, Ví dụ 01.5.
- **Lý do / nối:** đại lượng tính được, và ngay một giới hạn của nó trên một tập cụ thể → kì vọng của $L_S$.
- **Mục tiêu / nguồn:** 2; Định nghĩa 01.6, Ví dụ 01.5.
- **Bản deck cuối (2026-11-15):** tiêu đề "Ví dụ: rủi ro thực nghiệm trên $S_\eta$"; dòng đầu là dữ kiện ($S_\eta$, $h_3$ sai trên $(2,1)$ và $(4,0)$), dòng sau gọi tên và viết công thức $L_S$ trong dòng, rồi $L_{S_\eta}(h_3)=\tfrac13$; "Diễn giải:" bên trái, hình F3 bên phải. Lý do: phát hiện nhẹ của cổng duyệt (trang ví dụ nêu dữ kiện trước).

#### `3-02` Tính không chệch với giả thuyết cố định — trực quan, ví dụ, kết quả · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Với $h$ cố định, mỗi số hạng $\ell(h,Z_i)$ là một lần thử $h$ trên dữ liệu mới.
  - **Ví dụ.** Dưới $D_f$, $m=1$: $L_S(h_4)=\mathbb 1[X_1=3]$, kì vọng $0{,}2=L_{D_f}(h_4)$.
  - **Giả thiết:** mỗi $Z_i$ có phân bố $D$, không cần độc lập; $h$ không phụ thuộc $S$; (T2) và $L_D(h)<\infty$.
  - **Kết luận** (Mệnh đề 01.7): với mọi $m\ge1$, display $\mathbb E_S\big[L_S(h)\big]=L_D(h)$.
  - Trên một tập cụ thể vẫn lệch: $L_{S_\eta}(h_3)=\tfrac13$, trong khi $\mathbb E_S[L_S(h_3)]=0{,}22$.
  - ≈ 52 âm tiết.
- **Ghi chú diễn giả:** $L_S(h)$ là ước lượng không chệch (unbiased estimator) của $L_D(h)$. Đây là bảo đảm theo kì vọng, so một đại lượng thực nghiệm với một đại lượng tổng thể (population quantity); nó không nói $L_S(h)$ gần $L_D(h)$ trên một tập cụ thể. Trong ví dụ, $h_4$ và $f=h_3$ chỉ khác nhau tại $x=3$, nên với một quan sát, $L_S(h_4)$ bằng $1$ đúng khi $X_1=3$. Giả thiết "$h$ không phụ thuộc $S$" là giả thiết quyết định; trang ví dụ giả thuyết chọn theo tập huấn luyện cho thấy điều gì xảy ra khi bỏ nó. Nguồn: ghi chú Bài 01, Mệnh đề 01.7 và đoạn sau chứng minh; ví dụ $m=1$ dựng mới theo kí hiệu ghi chú (mục 5, V4).
- **Lý do / nối:** kết quả chính thứ nhất, theo thứ tự trực quan → ví dụ → phát biểu → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 3; Mệnh đề 01.7.
- **Bản deck cuối (2026-11-15):** nhãn "Bảo đảm:" thay "Kết luận" (quy định 2026-11-15: phát biểu dùng "Giả thiết:" và "Bảo đảm:"); ghi chú diễn giả bỏ câu nguồn gốc ví dụ và câu "nó không nói …" (Detect).

#### `3-03` Ý tưởng chứng minh: tính không chệch — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.**
  - 1. $\ell(h,Z_i)$ chỉ phụ thuộc $Z_i$ và $Z_i\sim D$: display $\mathbb E\,\ell(h,Z_i)=\int_{\mathcal Z}\ell(h,z)\,dD(z)=L_D(h)$.
  - 2. Tính tuyến tính: $\mathbb E_S[L_S(h)]=\frac1m\sum_{i=1}^m\mathbb E\,\ell(h,Z_i)=L_D(h)$.
  - Giả thiết vào: $h$ không phụ thuộc $S$, $Z_i\sim D$, $L_D(h)<\infty$ ở bước 1; bước 2 không dùng độc lập.
  - Bỏ "$h$ không phụ thuộc $S$": bước 1 hỏng, vì $\ell(A(S),Z_i)$ phụ thuộc cả $Z_i$.
  - ≈ 40 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả** (~180 âm tiết): Lộ trình hai bước: tính kì vọng của từng số hạng, rồi cộng. Bước 1 là nơi duy nhất dùng giả thiết: vì $h$ cố định và $\ell(h,\cdot)$ đo được, $\ell(h,Z_i)$ là biến ngẫu nhiên không âm chỉ phụ thuộc $Z_i$; phân bố của $Z_i$ là $D$ nên kì vọng là tích phân theo $D$, hữu hạn nhờ $L_D(h)<\infty$. Bước 2 là tính tuyến tính của kì vọng, đúng cả khi các $Z_i$ phụ thuộc nhau. Trường hợp cực biên $Z_1=\cdots=Z_m$ (Bài tập 01.3(a)): $L_S(h_4)$ chỉ nhận $0$ hoặc $1$ nhưng vẫn có kì vọng $0{,}2$; độc lập không làm thay đổi kì vọng mà làm $L_S$ tập trung quanh $L_D$, và Bài 02 dùng độc lập cho việc chặn độ lệch này. Ý nghĩa cho học: để ước lượng rủi ro của một hàm dự đoán, tính rủi ro thực nghiệm trên dữ liệu độc lập với dữ liệu dùng để chọn nó. Nguồn: ghi chú Bài 01, chứng minh Mệnh đề 01.7; §11 (cầu nối); Bài tập 01.3(a).
- **Lý do / nối:** lộ trình, giả thiết vào ở đâu, bỏ giả thiết hỏng ở đâu → kỹ thuật then chốt.
- **Mục tiêu / nguồn:** 3; chứng minh Mệnh đề 01.7.
- **Bản deck cuối (2026-11-15):** gộp trang kỹ thuật cũ 3·04 theo phương án (a) (quyết định của điều phối viên). Mặt trang: bước 1 viết trong dòng "$\mathbb E\,\ell(h,Z_i)=L_D(h)$" (tích phân chuyển sang ghi chú diễn giả, phát hiện nhẹ của cổng duyệt); bước 2 tính tuyến tính; dòng cực biên "$Z_1=\cdots=Z_m$ dưới $D_f$: $L_S(h_4)\in\{0,1\}$, kì vọng vẫn bằng $0{,}2$"; dòng bỏ giả thiết; dòng "**Kỹ thuật.** Tính tuyến tính của kì vọng, với $U_i$ khả tích, không cần độc lập:" cùng công thức hiển thị $\mathbb E[\sum_iU_i]=\sum_i\mathbb EU_i$. Lộ trình có hai bước (đúng hai bước của chứng minh trong ghi chú), dưới mức 3–5 bước của bản giao việc. Bỏ nhãn đứng riêng "Ý tưởng chứng minh." vì tiêu đề đã mang tiền tố (giữ trần 6 dòng). Ghi chú diễn giả dùng $\mathbb EN=\sum_{k=1}^3\Pr(N\ge k)$ chỉ với $k=1,2,3$ như Phụ lục C.2.

#### (trang cũ 3·04 "Tính tuyến tính của kì vọng") — đã gộp vào 3-03
- Gộp theo phương án (a) của mục 11, điểm 2 (quyết định của điều phối viên 2026-11-15). Kỹ thuật là kiến thức nền; một dòng "Kỹ thuật." trên 3-03. Dòng "Đếm bằng hàm chỉ báo" với tổng vô hạn bị bỏ (phát hiện trung bình của cổng duyệt).

#### `3-04` Ví dụ: nghiệm ERM và quy tắc chọn khi bằng nhau — định nghĩa, ví dụ · 2,5 phút
- **Mặt trang:**
  - Thuật toán ERM trả về một phần tử của $\arg\min_{h\in\mathcal H}L_S(h)$ với mọi $S$.
  - Quy tắc chọn khi bằng nhau (tie-breaking): $A_{\min}$ lấy ngưỡng nhỏ nhất, $A_{\max}$ lấy ngưỡng lớn nhất.
  - Bảng: Tập huấn luyện | Tập nghiệm ERM | $A_{\min}$ | $A_{\max}$; hàng $S_\eta$ | $\{h_2,h_3,h_5\}$ | $h_2$, $L_{D_\eta}=0{,}32$ | $h_5$, $L_{D_\eta}=0{,}28$; hàng $S_f$ | $\{h_3,h_4\}$ | $h_3$, $L_{D_f}=0$ | $h_4$, $L_{D_f}=0{,}2$.
  - **Diễn giải:** quy tắc chọn khi bằng nhau quyết định rủi ro kì vọng của hàm trả về.
  - ≈ 41 âm tiết.
- **Ghi chú diễn giả:** Mỗi phần tử của tập nghiệm là một nghiệm ERM. Trên $S_\eta$ chỉ $h_3$ đạt mức $0{,}22$, nhưng cả hai quy tắc đều không chọn $h_3$; so với $0{,}22$, $A_{\min}$ mất $0{,}10$, $A_{\max}$ mất $0{,}06$. Dưới $D_f$, tập nghiệm là $\{h_t:\max\{x_i:y_i=0\}<t\le\min\{x_i:y_i=1\}\}$, nên $A_{\max}$ chọn $\hat t=\min\{x_i:y_i=1\}$ (hoặc $6$) và $A_{\min}$ chọn $\hat t=1+\max\{x_i:y_i=0\}$. Với hàm lỗi 0–1, $L_S$ chỉ nhận giá trị trong $\{0,\tfrac1m,\ldots,1\}$, nên tập nghiệm luôn khác rỗng. Với hàm lỗi khác, tập nghiệm có thể rỗng: lớp $\{x\mapsto wx:\ w>0\}$, hàm lỗi bình phương, $S=((1,0))$ cho $L_S(h_w)=w^2$, cận dưới đúng $0$ không đạt (Ví dụ 01.7). Khi đó dùng ERM xấp xỉ (approximate ERM): $L_S(A(S))\le\inf_hL_S(h)+\epsilon_{\mathrm{opt}}$, giả thiết (O2); thuật toán ERM chính xác là (O1). Nguồn: ghi chú Bài 01, Định nghĩa 01.8, 01.12, Ví dụ 01.6, 01.7, Nhận xét 01.11.
- **Lý do / nối:** phương pháp chọn giả thuyết theo $L_S$ và vai trò của quy tắc chọn → kì vọng của $L_S$ khi giả thuyết được chọn theo tập huấn luyện.
- **Mục tiêu / nguồn:** 2; Định nghĩa 01.8, Ví dụ 01.6.
- **Bản deck cuối (2026-11-15):** tiêu đề "Nghiệm ERM và quy tắc chọn khi bằng nhau" (bỏ tiền tố "Ví dụ:" vì trang mở bằng định nghĩa). Dòng đầu: "Thuật toán ERM trả về một phần tử của tập nghiệm ERM $\arg\min_{h\in\mathcal H}L_S(h)\ne\emptyset$, với mọi $S$" (điều kiện tập nghiệm khác rỗng của Định nghĩa 01.8 viết bằng công thức).

#### `3-05` Ví dụ: giả thuyết chọn theo tập huấn luyện — ví dụ (mới), kiểm tra bỏ giả thiết · 3,5 phút
- **Mặt trang:**
  - **Câu hỏi:** với thuật toán ERM $A$, $\mathbb E_S[L_S(A(S))]$ có bằng $\mathbb E_S[L_D(A(S))]$ không?
  - Dưới $D_f$, $m=1$, $X_1$ đều trên năm mức; so $h_4$ cố định với $A_{\max}$.
  - Bảng V4 (mục 5): cột $X_1=1,\ldots,5$ và cột trung bình; hàng $L_S(h_4)$, $\hat t$, $L_S(A_{\max}(S))$, $L_{D_f}(A_{\max}(S))$.
  - `[f]` **Diễn giải:** với $h_4$: $\mathbb E_S L_S=0{,}2=L_{D_f}(h_4)$; với $A_{\max}$: $\mathbb E_S L_S=0<0{,}36=\mathbb E_S L_{D_f}$.
  - `[f]` $\ell(A(S),Z_1)$ phụ thuộc $Z_1$ qua $A(S)$, nên bước 1 của Mệnh đề 01.7 hỏng.
  - ≈ 42 âm tiết.
- **Ghi chú diễn giả:** Ví dụ dựng mới trên kí hiệu ghi chú, cỡ mẫu nhỏ nhất để liệt kê đủ năm tập huấn luyện đồng khả năng. $A_{\max}$ khớp mọi tập huấn luyện từ $D_f$, nên $L_S(A_{\max}(S))=0$ trên mọi tập; rủi ro kì vọng thì dương khi $X_1\ne3$. Với $m$ tổng quát, ghi chú cho $\mathbb E_S[L_{D_f}(A_{\max}(S))]=0{,}2(0{,}8^m+0{,}6^m+0{,}4^m)\ge0{,}2\cdot0{,}8^m>0$; tại $m=1$ giá trị là $0{,}36$, khớp bảng; tại $m=10$ xấp xỉ $0{,}0227$. Câu trả lời: nói chung không bằng; trên tập dùng để chọn hàm, rủi ro thực nghiệm có thể đánh giá thấp rủi ro kì vọng. Bài tập 01.3 có thêm một thuật toán mà độ lệch theo chiều ngược lại. Nguồn: ghi chú Bài 01, Nhận xét 01.9, Ví dụ 01.9, Phụ lục C.2; Bài tập 01.3; số liệu tính lại ở mục 5, V4.
- **Lý do / nối:** kiểm tra "bỏ giả thiết" của Mệnh đề 01.7 bằng con số tính tay → khoảng cách tổng quát hóa và cách sửa.
- **Mục tiêu / nguồn:** 3; Nhận xét 01.9.
- **Bản deck cuối (2026-11-15):** dữ kiện trước, "Câu hỏi:" sau (phát hiện nhẹ của cổng duyệt). "Diễn giải:" rút thành "với $h_4$, hai kì vọng cùng bằng $0{,}2$; với $A_{\max}$, chúng là $0$ và $0{,}36$"; dòng cuối "Bước 1 của chứng minh Mệnh đề 01.7 hỏng: …". Ghi chú diễn giả bỏ câu nguồn gốc ("dựng mới", "mục 5, V4"); cách dựng ví dụ nằm ở `review-log.md`.

#### `3-06` Khoảng cách tổng quát hóa và tập dữ liệu độc lập — định nghĩa, ý nghĩa · 2,5 phút
- **Mặt trang:**
  - Khoảng cách tổng quát hóa (generalization gap): display $L_D\big(A(S)\big)-L_S\big(A(S)\big)$.
  - Ngẫu nhiên theo $S$ và có thể âm: $A_{\max}(S_\eta)=h_5$ cho $0{,}28-\tfrac13=-\tfrac4{75}$.
  - Kì vọng bằng $0$ với $h$ cố định; với $A_{\max}$ dưới $D_f$, kì vọng ít nhất $0{,}2\cdot0{,}8^m$.
  - **Lưu ý:** ước lượng rủi ro của $A(S)$ bằng $L_{S'}(A(S))$ trên $S'\sim D^{m'}$ độc lập với $S$.
  - `[f]` Do đó trên chính tập huấn luyện dùng để chọn hàm, $L_S$ có thể đánh giá thấp $L_D$.
  - ≈ 54 âm tiết.
- **Ghi chú diễn giả:** Dòng cuối trả lời câu hỏi đặt ra cùng định nghĩa rủi ro kì vọng (vì sao không đo chất lượng trên tập huấn luyện). Cách sửa dùng lại Mệnh đề 01.7: khi lấy điều kiện theo $S$, hàm $A(S)$ cố định đối với $S'$, nên $\mathbb E[L_{S'}(A(S))\mid S]=L_D(A(S))$. Đây là quyết định thực hành thứ ba của ghi chú §9: rủi ro của $\hat h$ phải được ước lượng trên một tập dữ liệu độc lập với tập huấn luyện. Giá trị âm $-\tfrac4{75}$ cho thấy khoảng cách tổng quát hóa là đại lượng có dấu, không phải sai số tuyệt đối. Nguồn: ghi chú Bài 01, Định nghĩa 01.10 và đoạn sau, Nhận xét 01.9, §9.
- **Lý do / nối:** đặt tên cho đại lượng bị lệch, nêu cách sửa → bài tập ERM trên một tập mới.
- **Mục tiêu / nguồn:** 3; Định nghĩa 01.10.
- **Bản deck cuối (2026-11-15):** dòng `[f]` "Do đó trên chính tập huấn luyện …" đứng ngay sau dòng kì vọng $\ge0{,}2\cdot0{,}8^m$, "Lưu ý:" sau cùng (phát hiện nhẹ của cổng duyệt).

#### `3-07` Bài tập: tập nghiệm ERM và hai quy tắc chọn — bài tập (Bài tập 01.2(a)), lời giải trên mặt trang · 3,5 phút (2 phút tự làm)
- **Mặt trang:**
  - Dữ kiện: $\mathcal X=\{1,\ldots,6\}$, $\mathcal H=\{h_t:\ t=1,\ldots,7\}$, $m=7$, $S=((1,0),(2,0),(3,1),(4,0),(4,1),(5,0),(6,1))$.
  - Thuật toán 01.13: $c_y(x)=\#\{i:\ x_i=x,\ y_i=y\}$, $E(1)=\sum_xc_0(x)$, $E(t+1)=E(t)-c_0(t)+c_1(t)$.
  - **Câu hỏi:** tính $L_S(h_t)$, tập nghiệm ERM, $A_{\min}(S)$ và $A_{\max}(S)$.
  - `[f]` **Lời giải:** $c_0=(1,1,0,1,1,0)$, $c_1=(0,0,1,1,0,1)$; $E=(4,3,2,3,3,2,3)$, $L_S(h_t)=E(t)/7$.
  - `[f]` Tập nghiệm ERM $\{h_3,h_6\}$, nên $A_{\min}(S)=h_3$ và $A_{\max}(S)=h_6$.
  - `[f]` **Diễn giải:** với phân bố $D$ của Bài tập 01.2(b), $L_D(h_3)=0{,}29$, $L_D(h_6)=0{,}45$, còn $\min_tL_D(h_t)=0{,}25$.
  - ≈ 45 âm tiết.
- **Ghi chú diễn giả:** Lý do của bước cập nhật: khi ngưỡng tăng từ $t$ lên $t+1$, chỉ dự đoán tại $x=t$ đổi từ $1$ sang $0$; quan sát nhãn 0 tại $t$ hết sai, quan sát nhãn 1 tại $t$ trở thành sai. Chi phí $O(m)$ cho các số đếm và $O(K)$ cho các cập nhật. Kiểm tra: $E(1)$ bằng số nhãn 0 ($4$), $E(7)$ bằng số nhãn 1 ($3$); trên $S_\eta$ của ghi chú, cùng thuật toán cho $E=(3,2,2,3,2,3)$, khớp bảng số lỗi. Rủi ro vượt mức so với $\mathcal H$ là $0{,}04$ cho $A_{\min}(S)$ và $0{,}20$ cho $A_{\max}(S)$: hai nghiệm ERM trên cùng tập huấn luyện, rủi ro chênh nhau $0{,}16$. Phần (b)–(d) của bài tập (rủi ro Bayes, hàm lỗi có trọng số, ngưỡng trên $\mathbb R$) giao về nhà. Đặc tả đầy đủ của thuật toán (đầu vào, đầu ra, điều kiện dừng) ở Thuật toán 01.13. Nguồn: ghi chú Bài 01, Thuật toán 01.13 và lượt chạy trên $S_\eta$; tệp bài tập, Bài tập 01.2(a)(b).
- **Lý do / nối:** bài tập có lời giải trên mặt trang cho cụm ERM, lấy từ `exercises.md` (cùng số liệu, cùng kết quả) → tiêu đề mạch 4.
- **Mục tiêu / nguồn:** 2; Thuật toán 01.13, Bài tập 01.2(a).
- **Bản deck cuối (2026-11-15):** bỏ dòng "Diễn giải:" ($0{,}29$, $0{,}45$, $0{,}25$) khỏi mặt trang, chuyển sang ghi chú diễn giả (quyết định của điều phối viên, mục 11.11). Câu hỏi giữ chữ của Bài tập 01.2(a) ("với $t=1,\ldots,7$").

### Mạch 4. Thuật toán ghi nhớ và thiên kiến quy nạp (7 trang, 15 phút)

#### `4-00` 4. Thuật toán ghi nhớ và thiên kiến quy nạp — tiêu đề mạch, điểm vào mạch 4 · 0,5 phút
- **Mặt trang:** "4."; h2 tên mạch; `p.strand-lead` (bảng mạch); `p.strand-keys` "thuật toán ghi nhớ · nguyên tử · bất đẳng thức hợp · quá khớp · thiên kiến quy nạp".
- **Ghi chú diễn giả:** Kế thừa: trên lớp hàm ngưỡng, quy tắc chọn khi bằng nhau làm rủi ro thay đổi từ $0{,}22$ đến $0{,}32$ trên $S_\eta$. Nhiệm vụ: trên lớp chứa mọi hàm phân lớp đo được, chỉ ra một nghiệm ERM có rủi ro $1$. Trao cho mạch 5: bảo đảm học phải nói trực tiếp về $L_D(A(S))$ và phải cho phép thất bại. Nguồn: ghi chú Bài 01, §5 (cuối).
- **Lý do / nối:** quy tắc chọn quyết định rủi ro → trường hợp cực đoan.
- **Mục tiêu / nguồn:** 5; §5.

#### `4-01` Ví dụ: thuật toán ghi nhớ trên đoạn $[0,1]$ — ví dụ, định nghĩa · 3 phút
- **Mặt trang:**
  - $\mathcal X=[0,1]$ với σ-đại số Borel, $X\sim U[0,1]$, $Y=1$ chắc chắn; hàm lỗi $\ell_{0\text{-}1}$.
  - Lớp $\mathcal M_{\mathcal X}$: mọi hàm phân lớp đo được $[0,1]\to\{0,1\}$.
  - Thuật toán ghi nhớ (memorizing algorithm) $A_{\mathrm{gn}}$: tại điểm đã thấy, nhãn đa số (bằng phiếu thì $1$); ở mọi điểm khác, $0$.
  - Trên mỗi $S$: $h_{\equiv1}$ và $\mathbb 1_F$ với $F=\{X_1,\ldots,X_m\}$ cùng khớp mọi quan sát.
  - Hình F4 (`img/lec-01/ghi-nho.svg`), cột phải của `grid2`.
  - ≈ 47 âm tiết.
- **Ghi chú diễn giả:** $A_{\mathrm{gn}}(s)$ là hàm phân lớp ghi nhớ (memorizing classifier). Hàm này không dùng cấu trúc nào của $\mathcal X$: trên $\{1,\ldots,5\}$, $A_{\mathrm{gn}}(S_f)=\mathbb 1[x\in\{4,5\}]=h_4$. Một điểm $x$ với $\Pr(X=x)>0$ là một nguyên tử (atom); $U[0,1]$ không có nguyên tử. Lớp $\mathcal M_{\mathcal X}$ chứa cả hàm hằng $h_{\equiv1}$ (rủi ro $0$) và hàm chỉ báo của mọi tập hữu hạn. Đọc hình: năm điểm huấn luyện minh họa, đường $h_{\equiv1}$ ở mức $1$, hàm ghi nhớ bằng $1$ chỉ tại năm điểm. Nguồn: ghi chú Bài 01, Định nghĩa 01.14, Ví dụ 01.8.
- **Lý do / nối:** dữ kiện của phản ví dụ, nêu ngay dạng danh sách → trực quan và phát biểu.
- **Mục tiêu / nguồn:** 5; Định nghĩa 01.14, Ví dụ 01.8.
- **Bản deck cuối (2026-11-15):** hai dòng thiết lập toàn bề rộng, rồi `grid2` với ba dòng thuật toán ghi nhớ bên trái và hình F4 bên phải. Định nghĩa thuật toán ghi nhớ tách hai dòng (≤ 20 âm tiết mỗi dòng). Hình F4 nêu dữ liệu trong hình: "m = 5, nhãn 1: x = 0,12; 0,31; 0,47; 0,68; 0,90" (quyết định mục 11.9), không chữ "minh họa".

#### `4-02` Hàm phân lớp ghi nhớ có rủi ro kì vọng bằng 1 — trực quan, kết quả · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Một tập hữu hạn có xác suất $0$ dưới $U[0,1]$: quan sát mới hầu chắc chắn rơi ngoài $F$, nơi $A_{\mathrm{gn}}(S)$ báo $0$.
  - **Giả thiết:** $\mathcal X=[0,1]$ (Borel), $D_{\mathcal X}=U[0,1]$ không có nguyên tử (atomless), $Y=1$; $\mathcal H=\mathcal M_{\mathcal X}$; $\ell_{0\text{-}1}$; thuật toán $A_{\mathrm{gn}}$.
  - **Kết luận** (Mệnh đề 01.15), với mọi $m\ge1$ và mọi $S$:
  - (a) $A_{\mathrm{gn}}$ là thuật toán ERM và $L_S(A_{\mathrm{gn}}(S))=0$;
  - (b) $L_D(A_{\mathrm{gn}}(S))=1$;
  - (c) $h_{\equiv1}$ cũng là nghiệm ERM và $L_D(h_{\equiv1})=0$.
  - ≈ 52 âm tiết.
- **Ghi chú diễn giả:** Ba khẳng định đúng tất định, không chỉ với xác suất cao. Khoảng cách tổng quát hóa bằng $1$ với mọi $m$: thêm dữ liệu không giúp $A_{\mathrm{gn}}$. Hai nghiệm ERM trên cùng tập huấn luyện có rủi ro $0$ và $1$, nên quy tắc chọn khi bằng nhau quyết định toàn bộ rủi ro. Phản ví dụ nói về một lựa chọn ERM tồi trong một lớp rất giàu, không nói mọi nghiệm ERM đều tồi dưới phân bố này. Hàm phân lớp ghi nhớ là trường hợp cực đoan của quá khớp (overfitting). Nguồn: ghi chú Bài 01, Mệnh đề 01.15; blueprint mục 1.3 (Counterexample 1.2).
- **Lý do / nối:** kết quả chính thứ hai → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 5; Mệnh đề 01.15.
- **Bản deck cuối (2026-11-15):** nhãn "Bảo đảm:"; dòng "Giả thiết:" ghi nghĩa "không có nguyên tử (atomless): $\Pr(X=x)=0$ với mọi $x$"; "hầu chắc chắn (almost surely)" có tiếng Anh ở đây (lần dùng đầu trên mặt trang); "khoảng cách tổng quát hóa bằng 1" chuyển sang ghi chú diễn giả. 55 âm tiết.

#### `4-03` Ý tưởng chứng minh: hàm phân lớp ghi nhớ — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** (danh sách đánh số)
  - 1. $A_{\mathrm{gn}}(s)=1$ chỉ trên một tập hữu hạn (tập Borel), nên $A_{\mathrm{gn}}(s)\in\mathcal M_{\mathcal X}$.
  - 2. Tại mỗi điểm của $F$, nhãn đa số cho số lỗi nhỏ nhất, nên $A_{\mathrm{gn}}(S)$ là nghiệm ERM và $L_S=0$.
  - 3. $A_{\mathrm{gn}}(S)$ sai khi và chỉ khi $X\notin F$; display $\Pr(X\in F)\le\sum_{i=1}^m\Pr(X=x_i)=0$.
  - 4. $h_{\equiv1}$ đúng trên mọi $(X,1)$, nên $L_S(h_{\equiv1})=L_D(h_{\equiv1})=0$.
  - Giả thiết vào: lớp chứa mọi hàm đo được ở bước 1; không có nguyên tử ở bước 3.
  - ≈ 56 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả** (~190 âm tiết): Lộ trình: thuộc lớp, rủi ro thực nghiệm, rủi ro kì vọng. Tính chất then chốt là một tập hữu hạn có xác suất $0$ dưới $U[0,1]$, chứng minh bằng bất đẳng thức hợp và $\Pr(X=x_i)=0$. Bỏ từng giả thiết thì hỏng ở đâu: nếu lớp chỉ gồm hàm ngưỡng, bước 1 hỏng vì $\mathbb 1_F$ nói chung không là hàm ngưỡng; nếu $D_{\mathcal X}$ có nguyên tử, bước 3 hỏng vì quan sát mới rơi vào $F$ với xác suất dương, và Ví dụ 01.11 cho rủi ro kì vọng $0{,}8^m$ trên năm điểm. Bước 2 không dùng giả thiết nào về $D$: rủi ro thực nghiệm chỉ phụ thuộc giá trị của hàm trên $F$. Tính đo được của $A_{\mathrm{gn}}$ theo $(s,x)$ (để $L_D(A_{\mathrm{gn}}(S))$ là biến ngẫu nhiên) nằm ở Phụ lục A(iii) của ghi chú. Nguồn: ghi chú Bài 01, chứng minh Mệnh đề 01.15, Phụ lục A(iii).
- **Lý do / nối:** lộ trình bốn bước, giả thiết vào ở đâu → kỹ thuật dùng ở bước 3.
- **Mục tiêu / nguồn:** 5; chứng minh Mệnh đề 01.15.
- **Bản deck cuối (2026-11-15):** bốn bước: (1) thuộc lớp (giả thiết $\mathcal H=\mathcal M_{\mathcal X}$); (2) nghiệm ERM; (3) $\Pr(X\in F)\le\sum_i\Pr(X=x_i)=0$ (giả thiết không có nguyên tử); (4) $h_{\equiv1}$. Dòng bỏ giả thiết: "Bỏ 'không có nguyên tử': bước 3 hỏng, $\Pr(X\in F)$ có thể dương." (phát hiện nhẹ của cổng duyệt; con số $0{,}8^m$ của Ví dụ 01.11 ở ghi chú diễn giả vì ví dụ đó thuộc §8, sau trang này).

#### `4-04` Bất đẳng thức hợp — kỹ thuật (lần đầu trong học phần) · 1,5 phút
- **Mặt trang:**
  - **Kỹ thuật.** Bất đẳng thức hợp (union bound): với mọi biến cố $B_1,\ldots,B_m$, display $\Pr\Big(\bigcup_{i=1}^mB_i\Big)\le\sum_{i=1}^m\Pr(B_i)$, không cần độc lập.
  - Ở đây $B_i=\{X=x_i\}$ và $\Pr(B_i)=0$, nên hợp có xác suất $0$.
  - Dạng dùng: chặn xác suất "có ít nhất một chỉ số $i$ xấu" bằng tổng các xác suất "chỉ số $i$ xấu".
  - ≈ 40 âm tiết.
- **Ghi chú diễn giả:** Chứng minh một dòng: $\mathbb 1\big[\bigcup_iB_i\big]\le\sum_i\mathbb 1[B_i]$, rồi lấy kì vọng và dùng tính tuyến tính. Bài 02 dùng lại bất đẳng thức hợp cùng bất đẳng thức Hoeffding để chuyển một cận cho từng giả thuyết cố định thành cận cho nghiệm ERM chọn từ $\lvert\mathcal H\rvert$ ứng viên. Nguồn: ghi chú Bài 01, chứng minh Mệnh đề 01.15 (Bước 3), §11 (cầu nối).
- **Lý do / nối:** kỹ thuật dùng lại qua học phần, đặt ở nơi dùng lần đầu → bài tập dùng cùng hai công cụ.
- **Mục tiêu / nguồn:** 5; Mệnh đề 01.15.
- **Bản deck cuối (2026-11-15):** thêm dòng "Dùng khi …" theo bản giao việc; ghi chú diễn giả thêm giới hạn hợp đếm được (lời giải Bài tập 01.4(b)).

#### `4-05` Bài tập: hàm phân lớp ghi nhớ với nhãn $\mathbb 1[x>0{,}7]$ — bài tập (Bài tập 01.4(a)), lời giải trên mặt trang · 2,5 phút (1 phút tự làm)
- **Mặt trang:**
  - Dữ kiện: $X\sim U[0,1]$, $Y=f(X)$ với $f(x)=\mathbb 1[x>0{,}7]$; $\mathcal H=\mathcal M_{\mathcal X}$; $\ell_{0\text{-}1}$; thuật toán $A_{\mathrm{gn}}$.
  - **Câu hỏi:** tính $L_S(A_{\mathrm{gn}}(S))$ và $L_D(A_{\mathrm{gn}}(S))$, rồi so với rủi ro của $f$ và của hàm hằng $0$.
  - `[f]` **Lời giải:** tại mỗi điểm của $F$, mọi nhãn bằng $f(x)$, nên $A_{\mathrm{gn}}(S)=f$ trên $F$ và $L_S(A_{\mathrm{gn}}(S))=0$.
  - `[f]` Ngoài $F$, $A_{\mathrm{gn}}(S)=0$, sai khi $f(X)=1$; vì $\Pr(X\in F)=0$, $L_D(A_{\mathrm{gn}}(S))=\Pr(X>0{,}7)=0{,}3$.
  - `[f]` **Diễn giải:** rủi ro này bằng rủi ro của hàm hằng $0$; nghiệm ERM $f\in\mathcal H$ có rủi ro $0$.
  - ≈ 58 âm tiết.
- **Ghi chú diễn giả:** Lời giải dùng đúng hai công cụ của chứng minh Mệnh đề 01.15: bất đẳng thức hợp cho $\Pr(X\in F)\le\sum_i\Pr(X=x_i)=0$ và giả thiết không có nguyên tử. Dạng tổng quát của bài tập: với $D_{\mathcal X}$ không có nguyên tử và $Y=f(X)$, $L_D(A_{\mathrm{gn}}(s))=\Pr(f(X)=1)$ với mọi tập huấn luyện $s$; $f\equiv1$ cho lại Mệnh đề 01.15(b), $f\equiv0$ cho rủi ro $0$ vì nhãn mặc định $0$ đúng ở mọi nơi. $F$ là tập cố định khi lấy xác suất theo quan sát mới $X$. Phần (b) (chỗ dùng tính hữu hạn của $F$) và phần (c) (một nguyên tử tại $0$, kì vọng $\tfrac12+\tfrac12\cdot2^{-m}$) giao về nhà. Nguồn: tệp bài tập, Bài tập 01.4(a); ghi chú Bài 01, chứng minh Mệnh đề 01.15.
- **Lý do / nối:** bài tập có lời giải trên mặt trang cho cụm hàm ghi nhớ, lấy từ `exercises.md` → thiên kiến quy nạp.
- **Mục tiêu / nguồn:** 5; Bài tập 01.4(a).

#### `4-06` Thiên kiến quy nạp — khái niệm, ví dụ · 2 phút
- **Mặt trang:**
  - Thiên kiến quy nạp (inductive bias): lớp hàm ngưỡng chọn trước khi có dữ liệu, cam kết dự đoán không giảm theo $x$.
  - **Ví dụ.** $\tilde S_f=((1,0),(3,1),(5,1))$ lấy mẫu từ $D_f$:
  - $A_{\mathrm{gn}}(\tilde S_f)=\mathbb 1[x\in\{3,5\}]\notin\mathcal H$, sai tại $x=4$, rủi ro $0{,}2$;
  - trong lớp hàm ngưỡng chỉ $h_2$ ($0{,}2$) và $h_3$ ($0$) khớp $\tilde S_f$, và cả hai đúng tại $x=4$.
  - Trên $S_f$: $A_{\mathrm{gn}}(S_f)=h_4\in\mathcal H$, nên lớp hàm ngưỡng không loại được nó.
  - ≈ 50 âm tiết.
- **Ghi chú diễn giả:** Lớp $\mathcal M_{\mathcal X}$ không cam kết gì: trên mỗi tập huấn luyện, vô số hàm của lớp khớp mọi quan sát, với rủi ro kì vọng từ $0$ đến $1$. Mọi hàm ngưỡng dương tính tại $x=3$ cũng dương tính tại $x=4$, nên lớp loại được lỗi của hàm ghi nhớ tại $x=4$. Giá của thiên kiến quy nạp là lớp có thể không chứa hàm dự đoán tốt nhất (mạch 5 tính giá này bằng $0{,}04$ dưới $D_\eta$). Vì $h_3$ và $h_4$ cùng có rủi ro thực nghiệm $0$ trên $S_f$, một bảo đảm học phải phát biểu trực tiếp cho $L_D(A(S))$ và phải cho phép thất bại trên những tập như $S_f$; đó là nhiệm vụ của mạch 5. Nguồn: ghi chú Bài 01, §5 (hai đoạn cuối).
- **Lý do / nối:** ý nghĩa của phản ví dụ và yêu cầu đối với bảo đảm học → tiêu đề mạch 5.
- **Mục tiêu / nguồn:** 5; §5.
- **Bản deck cuối (2026-11-15):** ví dụ $\tilde S_f$ đứng đầu, tên khái niệm ở cuối, hai dòng: "Thiên kiến quy nạp (inductive bias) là việc chọn lớp giả thuyết trước khi có dữ liệu." và "Lớp hàm ngưỡng cam kết dự đoán không giảm theo $x$." (phát hiện nhẹ của cổng duyệt, theo ghi chú §5).

### Mạch 5. Học PAC (13 trang, 32 phút)

#### `5-00` 5. Học PAC — tiêu đề mạch, điểm vào mạch 5 · 0,5 phút
- **Mặt trang:** "5."; h2 "Học PAC"; `p.strand-lead` (bảng mạch); `p.strand-keys` "xác suất thất bại · thứ tự lượng từ · độ phức tạp mẫu · rủi ro Bayes · rủi ro vượt mức".
- **Ghi chú diễn giả:** Kế thừa: hai hàm cùng có rủi ro thực nghiệm $0$ trên $S_f$ nhưng khác rủi ro kì vọng, nên bảo đảm học phải nói trực tiếp về $L_D(A(S))$ và cho phép thất bại. Nhiệm vụ: trả lời ba câu hỏi chính của Học thống kê (nhỏ đến đâu, với xác suất nào, trên họ phân bố nào), trước cho cặp khả diễn, sau cho nhãn có nhiễu. Trao cho mạch 6: định nghĩa học PAC và độ phức tạp mẫu. Nguồn: ghi chú Bài 01, §6, §7.
- **Lý do / nối:** yêu cầu đối với bảo đảm → hai tham số.
- **Mục tiêu / nguồn:** 4; §6, §7.

#### `5-01` Xác suất thất bại và độ chính xác — vấn đề, trực quan, ví dụ · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Dưới $D_f$, một tập cỡ $m$ bỏ sót mức 3 với xác suất $0{,}8^m>0$ với mọi $m$.
  - Xác suất thất bại (failure probability) $\delta$: bảo đảm được phép hỏng với xác suất $\delta$ theo $S$.
  - Mức 3 chiếm $0{,}001$ dân số, $m=500$: xác suất bỏ sót $0{,}999^{500}\approx0{,}61$.
  - Tham số độ chính xác (accuracy parameter) $\epsilon$: chỉ đòi $L_D(A(S))-\inf_hL_D(h)\le\epsilon$, bỏ qua vùng có khối lượng nhỏ.
  - ≈ 54 âm tiết.
- **Ghi chú diễn giả:** Hai tham số trả lời hai câu hỏi đầu của trang mục tiêu bài toán học: hiệu nhỏ đến đâu ($\epsilon$) và với xác suất nào theo $S$ ($\delta$). Không thể đòi $\delta=0$: với mọi $m$, tập huấn luyện bỏ sót mức 3 với xác suất dương, và trên những tập đó tập huấn luyện không phân biệt $h_3$ với $h_4$. Không thể đòi $\epsilon=0$ với cỡ mẫu hợp lý: một mức chiếm $0{,}001$ dân số vắng mặt trong $500$ quan sát với xác suất khoảng $0{,}61$. Câu ôn nhanh thứ ba ($0{,}8^m$) xuất hiện lại ở đây. Nguồn: ghi chú Bài 01, §6 (đoạn đầu).
- **Lý do / nối:** vấn đề và trực quan của định nghĩa PAC, có con số → định nghĩa.
- **Mục tiêu / nguồn:** 4; §6.
- **Bản deck cuối (2026-11-15):** thứ tự dòng: Trực quan, $\delta$, $\epsilon$, rồi ví dụ $0{,}999^{500}\approx0{,}61$ (theo thứ tự §6 của ghi chú).

#### `5-02` Học PAC trong trường hợp khả diễn — định nghĩa · 3 phút
- **Mặt trang:**
  - Khả diễn (realizable): có $h^\star\in\mathcal H$ với $L_D(h^\star)=0$; đây là tính chất của cặp $(D,\mathcal H)$.
  - Với hàm lỗi 0–1, $A$ là thuật toán học PAC cho $\mathcal H$ nếu có $M:(0,1)^2\to\mathbb N$ để display $\Pr_{S\sim D^m}\big[L_D(A(S))\le\epsilon\big]\ge1-\delta$
  - với mọi $\epsilon,\delta\in(0,1)$, mọi $D$ mà $(D,\mathcal H)$ khả diễn, mọi $m\ge M(\epsilon,\delta)$.
  - Lớp $\mathcal H$ học được PAC (PAC learnable) nếu có một thuật toán học PAC cho $\mathcal H$.
  - **Ví dụ.** $(D_f,\mathcal H)$ khả diễn với $h^\star=h_3$; $(D_\eta,\mathcal H)$ thì không.
  - ≈ 58 âm tiết.
- **Ghi chú diễn giả:** Bối cảnh: phân lớp nhị phân, $\mathcal Y=\{0,1\}$, với hàm lỗi 0–1. Khi $(D,\mathcal H)$ khả diễn, $Y=h^\star(X)$ hầu chắc chắn, nên mọi nghiệm ERM có rủi ro thực nghiệm $0$ với xác suất $1$, và $\inf_hL_D(h)=0$: bất đẳng thức của định nghĩa chính là mục tiêu của bài toán học với độ chính xác $\epsilon$ và độ tin cậy (confidence) $1-\delta$. Khả diễn thay đổi khi thay một thành phần: $D_f$ với lớp hai hàm hằng $\{h_1,h_6\}$ không khả diễn ($0{,}4$ và $0{,}6$); $D_\eta$ không khả diễn với lớp nào, vì mọi hàm sai ít nhất $0{,}05$ tại $x=2$. Điều kiện $\inf=0$ khác $\min=0$ (Nhận xét 01.17). Với thuật toán có đại lượng ngẫu nhiên $\xi$, xác suất lấy theo cả $S$ và $\xi$. Nguồn: ghi chú Bài 01, Định nghĩa 01.16, 01.18, Nhận xét 01.17.
- **Lý do / nối:** phát biểu → đọc thứ tự lượng từ.
- **Mục tiêu / nguồn:** 4; Định nghĩa 01.16, 01.18.
- **Bản deck cuối (2026-11-15):** dòng lượng từ dạng ngắn "đúng với mọi $\epsilon,\delta\in(0,1)$, mọi $D$ khả diễn và mọi $m\ge M(\epsilon,\delta)$"; $\mathbb N=\{1,2,\ldots\}$ ghi trong dòng; dòng "Lớp $\mathcal H$ học được PAC (PAC learnable) …" giữ ở trang này (54 âm tiết) vì 5-03 sẽ vượt trần nếu nhận thêm dòng.

#### `5-03` Thứ tự lượng từ trong định nghĩa học PAC — trực quan về phát biểu · 3 phút
- **Mặt trang:**
  - **Câu hỏi:** cỡ mẫu đủ có được phép phụ thuộc phân bố $D$ không?
  - display `math-large`: $\exists A\ \exists M\ \forall\epsilon,\delta\in(0,1)\ \forall D\ \forall m\ge M(\epsilon,\delta):\ \Pr_{S\sim D^m}\big[L_D(A(S))\le\epsilon\big]\ge1-\delta$ (ngắt hai dòng bằng `aligned` nếu tràn ở 390 px; đo trên trình duyệt).
  - $\exists M$ trước $\forall D$: cỡ mẫu đủ chỉ phụ thuộc $(\epsilon,\delta)$; bảo đảm không phụ thuộc phân bố (distribution-free).
  - $\exists A$ trước $\forall D$: thuật toán được chọn trước khi biết $D$.
  - $\exists A$ trước $\forall\epsilon,\delta$: thuật toán không nhận $\epsilon$, $\delta$ làm đầu vào.
  - Đổi chỗ thành "$\forall D\ \exists m$": cỡ mẫu được phụ thuộc $D$ chưa biết, một khái niệm yếu hơn.
  - ≈ 57 âm tiết.
- **Ghi chú diễn giả:** $D$ chạy trên các phân bố khả diễn với $\mathcal H$. Xác suất lấy theo $S\sim D^m$, với $D$ cố định bên trong dấu $\Pr$. $\epsilon$ là ngưỡng cho rủi ro kì vọng; $1-\delta$ là độ tin cậy. Câu trả lời cho câu hỏi là không: thuật toán không biết $D$, nên một cỡ mẫu phụ thuộc $D$ không dùng được để quyết định cần thu bao nhiêu dữ liệu. Điều kiện "$\exists A$ trước $\forall D$" là yêu cầu $D$ chưa biết của bài toán học. Bài tập 01.5 yêu cầu viết lại hai định nghĩa với đủ lượng từ. Nguồn: ghi chú Bài 01, §6 (sau Định nghĩa 01.18); blueprint mục 1.2.
- **Lý do / nối:** trọng tâm do người dùng chỉ định; đọc từng cặp lượng từ → tính cỡ mẫu trên ví dụ.
- **Mục tiêu / nguồn:** 4; §6.
- **Bản deck cuối (2026-11-15):** dòng lượng từ ngắt hai dòng bằng `aligned` (một dòng tràn khung 1280 px); ý "$\exists A$ trước $\forall D$" và "$\exists A$ trước $\forall\epsilon,\delta$" gộp một dòng. 50 âm tiết.

#### `5-04` Độ phức tạp mẫu của thuật toán và của lớp — định nghĩa · 2,5 phút
- **Mặt trang:**
  - Độ phức tạp mẫu (sample complexity) $m_A(\epsilon,\delta)$: số $m_0\in\mathbb N$ nhỏ nhất để bảo đảm đúng với mọi $D$ khả diễn và mọi $m\ge m_0$.
  - Của lớp, lấy riêng cho từng cặp $(\epsilon,\delta)$: display $m_{\mathcal H}(\epsilon,\delta)=\min_Am_A(\epsilon,\delta)$.
  - Cận trên cho $m_{\mathcal H}$ chỉ cần một thuật toán tốt; cận dưới phải lập luận cho mọi thuật toán.
  - ≈ 44 âm tiết.
- **Ghi chú diễn giả:** Khi không có $m_0$ nào, $m_A(\epsilon,\delta)=\infty$. Lớp học được PAC khi và chỉ khi có một thuật toán $A$ với $m_A(\epsilon,\delta)<\infty$ cho mọi $(\epsilon,\delta)$; khi đó $A$ cùng $M=m_A$ thỏa định nghĩa. Vì $m_{\mathcal H}$ lấy riêng cho từng cặp, thuật toán đạt nó có thể đổi theo cặp, nên từ $m_{\mathcal H}<\infty$ với mọi cặp chưa suy ra được một thuật toán dùng cho mọi cặp. Điều kiện "mọi $m\ge m_0$" cần thiết vì thành công ở cỡ $m$ không kéo theo thành công ở cỡ $m+1$: dưới phân bố $D_1$ (năm mức đều, $Y=1$ chắc chắn), thuật toán trả $A_{\max}(S)$ khi $m$ chẵn và $h_6\equiv0$ khi $m$ lẻ có $m_A=\infty$. Bài tập 01.7 chứng minh tính đơn điệu của độ phức tạp mẫu. Nguồn: ghi chú Bài 01, Định nghĩa 01.20, Nhận xét 01.21.
- **Lý do / nối:** phân biệt $m_A$ với $m_{\mathcal H}$ (mục tiêu 4), theo thứ tự của ghi chú (Định nghĩa 01.20 trước Ví dụ 01.9) → cỡ mẫu trên ví dụ.
- **Mục tiêu / nguồn:** 4; Định nghĩa 01.20.

#### `5-05` Ví dụ: xác suất thất bại của $A_{\max}$ dưới $D_f$ — ví dụ, cận bằng số · 3 phút
- **Mặt trang:**
  - $L_{D_f}(A_{\max}(S))=0{,}2(\hat t-3)\in\{0;\ 0{,}2;\ 0{,}4;\ 0{,}6\}$, dương khi và chỉ khi $S$ không có quan sát tại $x=3$: display $\Pr_{S\sim D_f^m}\big[L_{D_f}(A_{\max}(S))>0\big]=0{,}8^m$.
  - $\epsilon=0{,}1$, $\delta=0{,}05$: thành công khi và chỉ khi rủi ro bằng $0$; $0{,}8^{13}\approx0{,}0550$, $0{,}8^{14}\approx0{,}0440$, nên $m\ge14$.
  - $\epsilon=0{,}25$, $\delta=0{,}05$: thất bại khi và chỉ khi vắng cả $x=3$ và $x=4$; $0{,}6^5\approx0{,}0778$, $0{,}6^6\approx0{,}0467$, nên $m\ge6$.
  - Hình F5a (`img/lec-01/that-bai-df.svg`), cột phải `grid2`.
  - **Diễn giải:** $14$ và $6$ là cỡ mẫu đủ cho riêng cặp $(A_{\max},D_f)$, tức dạng "$\forall D\ \exists m$".
  - ≈ 55 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Vì $f=h_3$, $h_{\hat t}$ sai đúng tại các mức $3,\ldots,\hat t-1$. $\hat t=3$ khi và chỉ khi $S$ có quan sát tại $x=3$; các quan sát độc lập theo (T1), mỗi quan sát khác $3$ với xác suất $0{,}8$. Vì giá trị dương nhỏ nhất của rủi ro là $0{,}2>0{,}1$, thành công trùng với rủi ro bằng $0$; với $\epsilon=0{,}25$, $0{,}6$ là khối lượng của $\{1,2,5\}$. Nới $\epsilon$ từ $0{,}1$ lên $0{,}25$ làm cỡ mẫu cần giảm từ $14$ xuống $6$. Đọc theo các lần lấy mẫu lặp lại: ở $m=14$, khoảng $4{,}4\%$ số tập huấn luyện cho hàm có rủi ro ít nhất $0{,}2$. Kì vọng $\mathbb E_S[L_{D_f}(A_{\max}(S))]\approx0{,}0227$ tại $m=10$, trong khi rủi ro thực nghiệm luôn bằng $0$. Hai cỡ mẫu đổi khi khối lượng của mức 3 đổi, nên chúng không phải $m_{A_{\max}}$. Đọc hình: đường $0{,}8^m$ và $0{,}6^m$ cắt mức $\delta=0{,}05$ tại $m=14$ và $m=6$. Nguồn: ghi chú Bài 01, Ví dụ 01.9, Phụ lục C.2.
- **Lý do / nối:** con số cụ thể cho $\epsilon$, $\delta$, $m$ → đọc đúng xác suất $1-\delta$.
- **Mục tiêu / nguồn:** 4; Ví dụ 01.9.
- **Bản deck cuối (2026-11-15):** bỏ công thức hiển thị; dòng đầu ghi xác suất $0{,}8^m$ trong dòng; "Diễn giải: $14$ và $6$ chỉ đủ cho riêng $D_f$." (dạng "$\forall D\ \exists m$" ở ghi chú diễn giả). Lý do: hình F5a cần chiều cao, trang tràn khung. Hình F5a có đáy trục log $0{,}001$ (quyết định của điều phối viên).

#### `5-06` Bài tập: đọc một bảo đảm học PAC — bài tập (Bài tập 01.5(d), câu 2 và 4), đề · 2 phút (1 phút tự làm)
- **Mặt trang:**
  - Dữ kiện: $D_f$, lớp hàm ngưỡng, $A_{\max}$; $\Pr_S\big[L_{D_f}(A_{\max}(S))\le0{,}1\big]\ge0{,}95$ khi $m\ge14$; trên $S_f$, $A_{\max}$ trả về $h_4$.
  - **Câu hỏi:** mỗi câu sau đúng hay sai?
  - (2) "Với xác suất ít nhất $0{,}95$ theo tập huấn luyện cỡ $m\ge14$, hàm phân lớp học được có xác suất lỗi không quá $0{,}1$."
  - (4) "Đã có tập huấn luyện $S_f$; xác suất để $L_{D_f}(A_{\max}(S_f))\le0{,}1$ là $0{,}95$."
  - ≈ 55 âm tiết.
- **Ghi chú diễn giả:** Bài tập 01.5(d) có bốn câu; trang giữ câu 2 và câu 4 vì hai câu này tách đúng hai loại xác suất: theo tập huấn luyện (trước khi lấy mẫu) và sau khi đã có một tập cụ thể. Câu 1 ("dự đoán sai với xác suất không quá $0{,}05$") và câu 3 ("ít nhất $95\%$ số người nhận kết quả đúng") để trong lời giải của tệp bài tập: câu 1 nhầm vai trò của $\epsilon$ và $\delta$; câu 3 chỉ có cơ sở $1-L_D(A(S))\ge0{,}9$ trên biến cố thành công. Giữ nguyên chữ của hai câu như trong tệp bài tập. Nguồn: tệp bài tập, Bài tập 01.5(d); ghi chú Bài 01, Nhận xét 01.19, Ví dụ 01.9.
- **Lý do / nối:** bài tập về vai trò của $\delta$, trọng tâm do người dùng chỉ định; đề và lời giải tách hai trang vì gộp sẽ vượt trần 60 âm tiết (khoảng 90) → lời giải.
- **Mục tiêu / nguồn:** 4; Bài tập 01.5(d).
- **Bản deck cuối (2026-11-15):** gộp đề và lời giải theo phương án (b) (quyết định của điều phối viên): một trang chỉ với câu (4) của Bài tập 01.5(d). Mặt trang: dữ kiện; "Câu hỏi: câu sau đúng hay sai? 'Đã có tập huấn luyện $S_f$; xác suất để $L_{D_f}(A_{\max}(S_f))\le0{,}1$ là $0{,}95$.'"; `[f]` "Lời giải: sai. Sau khi có $S_f$, $L_{D_f}(h_4)=0{,}2>0{,}1$ đã cố định; không còn xác suất nào để gán."; `[f]` "Ngoài ra $m=4$ chưa đạt ngưỡng $14$."; `[f]` cách hiểu 100 lần huấn luyện (Nhận xét 01.19). 59 âm tiết. Câu (2) đúng nằm ở ghi chú diễn giả; câu (1), (3) làm ở nhà.

#### (trang cũ 5·07 "Bài tập: đọc một bảo đảm học PAC, lời giải") — đã gộp vào 5-06
- Gộp theo phương án (b) của mục 11, điểm 2 (quyết định của điều phối viên 2026-11-15).

#### `5-07` Rủi ro Bayes — vấn đề, trực quan, ví dụ · 2,5 phút
- **Mặt trang:**
  - Dưới $D_\eta$, tại $x=2$ mọi hàm phân lớp sai với xác suất ít nhất $0{,}2\cdot\tfrac14=0{,}05$, nên không đạt được $L_D(A(S))\le\epsilon$ khi $\epsilon<0{,}05$.
  - Rủi ro Bayes (Bayes risk): display $L_D^{\mathrm{Bayes}}=\inf_{g\in\mathcal M_{\mathcal X}}L_D(g)$, chỉ phụ thuộc $D$.
  - **Trực quan.** Tại mỗi $x$, chọn nhãn sai ít hơn: báo $1$ khi $\eta(x)\ge1-\eta(x)$.
  - **Ví dụ.** $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$ cho hàm $\mathbb 1[x\in\{3,5\}]$, rủi ro $0{,}2\,(0+\tfrac14+\tfrac14+\tfrac25+0)=0{,}18$.
  - Hình F2a (`img/lec-01/eta-nguong.svg`), cột phải `grid2`.
  - ≈ 52 âm tiết.
- **Ghi chú diễn giả:** Mức rủi ro dùng để so với $L_D(A(S))$ gọi là đối tượng so sánh (comparator): trong trường hợp khả diễn nó bằng $0$; dưới $D_\eta$ nó phải là một mức dương. Rủi ro Bayes là mức thấp nhất trên mọi hàm phân lớp đo được, không phụ thuộc lớp giả thuyết hay tập huấn luyện. Trong ví dụ, tại $x=4$, $\eta=\tfrac25<\tfrac12$, nên hàm Bayes báo âm tính dù mức 3 bên dưới báo dương tính; hàm này không đơn điệu, không thuộc lớp hàm ngưỡng. Đọc hình: năm cột $\eta(x)$, đường ngang $\tfrac12$, các cột vượt đường được đánh dấu. Nguồn: ghi chú Bài 01, §7 (đoạn đầu), Định nghĩa 01.22, Nhận xét 01.17, Ví dụ 01.10.
- **Lý do / nối:** vấn đề (không khả diễn) → trực quan → ví dụ, trước phát biểu.
- **Mục tiêu / nguồn:** 2; Định nghĩa 01.22, Ví dụ 01.10.
- **Bản deck cuối (2026-11-15):** dòng đầu toàn bề rộng, rồi `grid2` (định nghĩa rủi ro Bayes với công thức hiển thị và "Trực quan." bên trái, hình F2a bên phải), "Ví dụ." ở cuối: "Hàm Bayes là $\mathbb 1[x\in\{3,5\}]$, với rủi ro $0{,}2\,(0+\tfrac14+\tfrac14+\tfrac25+0)=0{,}18$" ($\eta$ có trong hình). Tại $x=2$ ghi $0{,}2\cdot\min\{\tfrac14,\tfrac34\}$ như Nhận xét 01.17.

#### `5-08` Quy tắc Bayes — kết quả · 2 phút
- **Mặt trang:**
  - **Giả thiết:** $\eta$ đo được và $\eta(X)=\Pr(Y=1\mid X)$ hầu chắc chắn; xét mọi $g\in\mathcal M_{\mathcal X}$, không giới hạn trong $\mathcal H$.
  - **Kết luận** (Mệnh đề 01.23):
  - (a) $h_{\mathrm{Bayes}}(x)=\mathbb 1[\eta(x)\ge\tfrac12]$ đạt display $L_D^{\mathrm{Bayes}}=\mathbb E\min\{\eta(X),1-\eta(X)\}$;
  - (b) dưới $\ell_c$ với $c_{FP},c_{FN}>0$, hàm $\mathbb 1\big[\eta(x)\ge c_{FP}/(c_{FP}+c_{FN})\big]$ có rủi ro nhỏ nhất trên $\mathcal M_{\mathcal X}$, bằng $\mathbb E\min\{c_{FN}\eta(X),\ c_{FP}(1-\eta(X))\}$.
  - **Ý nghĩa:** dưới $D_\eta$, $h_{\mathrm{Bayes}}\notin\mathcal H$ và $\min_tL_{D_\eta}(h_t)=0{,}22>0{,}18$.
  - ≈ 33 âm tiết.
- **Ghi chú diễn giả:** $h_{\mathrm{Bayes}}$ là hàm phân lớp tối ưu Bayes (Bayes optimal classifier). Hàm tối ưu không duy nhất nói chung; khi $\eta(X)$ bằng ngưỡng với xác suất $0$, nó duy nhất nếu bỏ qua một tập có xác suất $0$; dưới $D_\eta$ điều kiện này thỏa cho cả hai ngưỡng $\tfrac12$ và $\tfrac15$. Rủi ro Bayes bằng $0$ khi và chỉ khi $\eta(X)\in\{0,1\}$ hầu chắc chắn, tức nhãn là hàm tất định của đầu vào; với $D_\eta$ thì không, nên không lớp nào khả diễn. Ghi chú xếp mệnh đề ở mức đọc thêm; chứng minh đầy đủ ở Phụ lục B. Nguồn: ghi chú Bài 01, Mệnh đề 01.23, Phụ lục B.
- **Lý do / nối:** kết quả chính thứ ba → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 2; Mệnh đề 01.23.
- **Bản deck cuối (2026-11-15):** "Giả thiết:" thêm "$D$ trên $\mathcal X\times\{0,1\}$; $\ell_{0\text{-}1}$ ở (a), $\ell_c$ với $c_{FP},c_{FN}>0$ ở (b)" (phát hiện nhẹ của cổng duyệt); nhãn "Bảo đảm:"; tên tiếng Anh "Bayes optimal classifier" trên mặt trang. Ghi chú diễn giả nói kết quả ở mức đọc thêm (quyết định mục 11.10).

#### `5-09` Ý tưởng chứng minh: quy tắc Bayes — ý tưởng chứng minh, kỹ thuật · 2,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** (danh sách đánh số)
  - 1. Rủi ro có điều kiện (conditional risk): display $\Pr(g(X)\ne Y\mid X=x)=\eta(x)\,\mathbb 1[g(x)=0]+\big(1-\eta(x)\big)\mathbb 1[g(x)=1]$.
  - 2. Tại mỗi $x$, vế phải không nhỏ hơn $\min\{\eta(x),1-\eta(x)\}$; dấu bằng khi $g=h_{\mathrm{Bayes}}$.
  - 3. Lấy kì vọng: $L_D(g)=\mathbb E\big[\mathbb E[\mathbb 1[g(X)\ne Y]\mid X]\big]\ge\mathbb E\min\{\eta(X),1-\eta(X)\}$.
  - Với $\ell_c$: báo $1$ khi $c_{FP}(1-\eta(x))\le c_{FN}\,\eta(x)$, tức $\eta(x)\ge c_{FP}/(c_{FP}+c_{FN})$.
  - **Kỹ thuật.** Tối thiểu hóa từng điểm, rồi lấy kì vọng theo $X$.
  - ≈ 30 âm tiết.
- **Ghi chú diễn giả** (~200 âm tiết): Lộ trình ba bước: tính rủi ro có điều kiện tại $X=x$, so hai lựa chọn $0$ và $1$ tại từng điểm, rồi lấy kì vọng theo $D_{\mathcal X}$ bằng $\mathbb E[\mathbb E[U\mid X]]=\mathbb E[U]$. Giả thiết vào: $g$ đo được để đưa $\mathbb 1[g(X)=\cdot]$ ra ngoài kì vọng có điều kiện (bước 1); $\eta$ đo được để tập $\{\eta\ge\tfrac12\}$ đo được, tức $h_{\mathrm{Bayes}}\in\mathcal M_{\mathcal X}$ (bước 2). Từ bước 2 còn có $L_D(g)-L_D(h_{\mathrm{Bayes}})=\mathbb E\big[\lvert2\eta(X)-1\rvert\,\mathbb 1[g(X)\ne h_{\mathrm{Bayes}}(X)]\big]$; dưới $D_\eta$, $h_3$ khác $h_{\mathrm{Bayes}}$ chỉ tại $x=4$, nên hiệu là $0{,}2\cdot\lvert2\cdot0{,}4-1\rvert=0{,}04$, khớp $0{,}22-0{,}18$. Phép tương đương ở dòng $\ell_c$ dùng $c_{FP}+c_{FN}>0$. Kỹ thuật tối thiểu hóa từng điểm chỉ dùng trong chứng minh này của Bài 01, nên được nêu bằng một dòng, không có trang riêng. Nguồn: ghi chú Bài 01, Mệnh đề 01.23 (đoạn ý tưởng), Phụ lục B.
- **Lý do / nối:** lộ trình và chỗ giả thiết vào → áp dụng phần (b) cho ví dụ sàng lọc.
- **Mục tiêu / nguồn:** 2; Phụ lục B.
- **Bản deck cuối (2026-11-15):** đúng storyboard; ghi chú diễn giả bỏ câu "nên được nêu bằng một dòng, không có trang riêng".

#### `5-10` Ví dụ: quy tắc Bayes dưới hàm lỗi có trọng số — ví dụ (Ví dụ 01.10), kiểm tra · 2,5 phút
- **Mặt trang:**
  - $D_\eta$ với $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$, $(c_{FP},c_{FN})=(1,4)$, lớp hàm ngưỡng.
  - **Câu hỏi:** nên đặt ngưỡng báo dương tính ở đâu khi bỏ sót đắt gấp bốn?
  - `[f]` Ngưỡng $\tfrac{c_{FP}}{c_{FP}+c_{FN}}=\tfrac1{1+4}=\tfrac15$; $\eta(x)\ge\tfrac15$ tại $x=2,3,4,5$, nên hàm Bayes dưới $\ell_c$ là $h_2\in\mathcal H$.
  - `[f]` Rủi ro: $L^c_{D_\eta}(h_2)=0{,}2\,(0+\tfrac34+\tfrac14+\tfrac35+0)=0{,}32=\min_tL^c_{D_\eta}(h_t)$.
  - `[f]` Hình F2b (`img/lec-01/eta-hai-nguong.svg`).
  - `[f]` **Diễn giải:** lớp hàm ngưỡng chứa hàm Bayes dưới $\ell_c$ nhưng không chứa hàm Bayes dưới $\ell_{0\text{-}1}$.
  - ≈ 50 âm tiết.
- **Ghi chú diễn giả:** Trang trả lời câu hỏi thực hành của ví dụ sàng lọc (ghi chú §3): ngưỡng trên $\eta(x)$ là $c_{FP}/(c_{FP}+c_{FN})$, bằng $\tfrac12$ chỉ khi $c_{FP}=c_{FN}$. $h_2$ báo âm tính tại $x=1$, nơi $\eta(1)=0$, nên không bỏ sót người bệnh nào; nó báo nhầm tại các mức 2 đến 5 với xác suất có điều kiện $1-\eta(x)$. Giá trị $0{,}32$ khớp bảng $L^c_{D_\eta}$ của Ví dụ 01.2. Trang là ví dụ của ghi chú với một "Câu hỏi:", không phải trang "Bài tập:", vì `exercises.md` không có bài này; Bài tập 01.1(d) và 01.2(c) áp cùng công thức với chi phí khác (giao về nhà). Nguồn: ghi chú Bài 01, Ví dụ 01.10, §3 (khối ứng dụng), Mệnh đề 01.23(b).
- **Lý do / nối:** kiểm tra của hành trình Mệnh đề 01.23, khép câu hỏi thực hành của mạch 2 → hai đối tượng so sánh.
- **Mục tiêu / nguồn:** 2; Ví dụ 01.10.
- **Bản deck cuối (2026-11-15):** hình F2b hiện cùng fragment đầu, đặt cạnh "Câu hỏi:"; ghi chú diễn giả mở thẳng bằng nội dung ("Ngưỡng báo dương tính trên $\eta(x)$ là …"), bỏ câu về loại trang (phát hiện trung bình của cổng duyệt).

#### `5-11` Rủi ro vượt mức — định nghĩa, ví dụ · 2,5 phút
- **Mặt trang:**
  - Rủi ro vượt mức (excess risk) của $h$ so với $\mathcal H$: $L_D(h)-\inf_{h'\in\mathcal H}L_D(h')$; so với rủi ro Bayes: $L_D(h)-L_D^{\mathrm{Bayes}}$.
  - display (dùng `aligned` nếu tràn) $L_D(h)-L_D^{\mathrm{Bayes}}=\Big[L_D(h)-\inf_{h'\in\mathcal H}L_D(h')\Big]+\Big[\inf_{h'\in\mathcal H}L_D(h')-L_D^{\mathrm{Bayes}}\Big]$.
  - **Ví dụ.** $h=h_2$ dưới $D_\eta$, $\ell_{0\text{-}1}$: $0{,}32-0{,}18=0{,}14=0{,}10+0{,}04$.
  - Hình F6 (`img/lec-01/rui-ro-vuot-muc.svg`).
  - **Diễn giải:** $0{,}04$ chỉ phụ thuộc lớp và không giảm khi $m$ tăng; $0{,}10$ là phần mất do chọn $h_2$ thay $h_3$.
  - ≈ 44 âm tiết.
- **Ghi chú diễn giả:** Khi nói rủi ro vượt mức phải nêu đối tượng so sánh. Số hạng thứ hai chỉ phụ thuộc lớp đã chọn, không phụ thuộc $h$; nó là giá của thiên kiến quy nạp. Câu hỏi của ghi chú: nên so $L_D(A(S))$ với $\inf_hL_D(h)$ hay với $L_D^{\mathrm{Bayes}}$; định nghĩa học PAC bất khả diễn chọn $\inf_hL_D(h)$, với hai lý do nêu cùng định nghĩa. Đọc hình: trục rủi ro với ba mốc $0{,}18$, $0{,}22$, $0{,}32$ và hai đoạn $0{,}04$, $0{,}10$. Nguồn: ghi chú Bài 01, Định nghĩa 01.24 và đoạn sau.
- **Lý do / nối:** chuẩn bị đối tượng so sánh của định nghĩa bất khả diễn → định nghĩa.
- **Mục tiêu / nguồn:** 2; Định nghĩa 01.24.
- **Bản deck cuối (2026-11-15):** dòng định nghĩa rút: "Rủi ro vượt mức (excess risk) của $h$: so với rủi ro Bayes ở vế trái, so với $\mathcal H$ ở ngoặc đầu." (hai hiệu đọc trực tiếp trên đẳng thức hiển thị); hình F6 dưới dòng "Ví dụ.", "Diễn giải:" ở cuối. Lý do: trang tràn khung khi có cả hai công thức trong dòng.

#### `5-12` Học PAC bất khả diễn — định nghĩa, so sánh · 3 phút
- **Mặt trang:**
  - Học PAC bất khả diễn (agnostic PAC learning): cùng thứ tự lượng từ, với bất đẳng thức display $\Pr_{S\sim D^m}\Big[L_D(A(S))\le\inf_{h\in\mathcal H}L_D(h)+\epsilon\Big]\ge1-\delta$ (dùng `aligned` nếu tràn).
  - So với trường hợp khả diễn:
  - hàm lỗi $\ell\ge0$ bất kì trên $\mathcal Z$, thay cho $\ell_{0\text{-}1}$;
  - biến cố là rủi ro vượt mức so với $\mathcal H$ không quá $\epsilon$;
  - mọi $D$ có rủi ro hữu hạn trên $\mathcal H$, kể cả nhãn ngẫu nhiên như $D_\eta$.
  - **Lưu ý:** đối tượng so sánh là $\inf_hL_D(h)$, vì $A(S)\in\mathcal H$ không xuống dưới mức này.
  - ≈ 54 âm tiết.
- **Ghi chú diễn giả:** Lớp học được PAC bất khả diễn (agnostic PAC learnable) nếu có một thuật toán như vậy. Hai lý do chọn $\inf_hL_D(h)$ thay cho rủi ro Bayes: (i) thuật toán học đúng lớp (proper learning) có $L_D(A(S))\ge\inf_hL_D(h)$, và hiệu $0{,}04$ không giảm theo $m$; (ii) khi $\mathcal X$ vô hạn, không thuật toán nào bảo đảm $L_D(A(S))\le L_D^{\mathrm{Bayes}}+\epsilon$ cho mọi $D$ với cỡ mẫu không phụ thuộc $D$ (UML §5.1). Phân bố có rủi ro hữu hạn: $L_D(h)<\infty$ với mọi $h\in\mathcal H$; mọi phân bố đều thỏa khi hàm lỗi bị chặn. Với hàm lỗi 0–1 và cặp khả diễn, hai biến cố trùng nhau, nên mọi thuật toán học PAC bất khả diễn cũng là thuật toán học PAC khả diễn với cùng $M$ (Bài tập 01.10). Học ngoài lớp (improper learning) cho phép $A(S)$ ra ngoài $\mathcal H$ và có thể xuống dưới đối tượng so sánh: $\mathbb 1[x\in\{3,5\}]$ có rủi ro $0{,}18<0{,}22$. Tóm lại câu trả lời của ghi chú cho "học có nghĩa là gì": chọn $A(S)$ thỏa bất đẳng thức trên với xác suất ít nhất $1-\delta$ khi $m$ vượt một ngưỡng không phụ thuộc phân bố; rủi ro thực nghiệm không có mặt trong yêu cầu này. Nguồn: ghi chú Bài 01, Định nghĩa 01.25 và đoạn sau, Định nghĩa 01.3, Nhận xét 01.26, 01.27; UML §3.2, §5.1.
- **Lý do / nối:** định nghĩa thứ hai của học, khép mạch 5 → tiêu đề mạch 6.
- **Mục tiêu / nguồn:** 4; Định nghĩa 01.25.
- **Bản deck cuối (2026-11-15):** bỏ dòng dẫn "So với trường hợp khả diễn:" (ba gạch đầu dòng tự nêu "thay cho …") để giữ 6 dòng; họ phân bố viết bằng công thức "$L_D(h)<\infty$ với mọi $h\in\mathcal H$"; "đối tượng so sánh (comparator)" có tiếng Anh ở lần dùng đầu trên mặt trang.

### Mạch 6. Rủi ro thực nghiệm nhỏ và bảo đảm học (8 trang, 16 phút)

#### `6-00` 6. Rủi ro thực nghiệm nhỏ và bảo đảm học — tiêu đề mạch, điểm vào mạch 6 · 0,5 phút
- **Mặt trang:** "6."; h2 tên mạch; `p.strand-lead` (bảng mạch); `p.strand-keys` "cận tổng quát hóa · phản ví dụ · nguyên tử · cỡ mẫu không phụ thuộc phân bố".
- **Ghi chú diễn giả:** Kế thừa: định nghĩa học PAC và phản ví dụ ghi nhớ. Nhiệm vụ: phát biểu phản ví dụ bằng ngôn ngữ học PAC, chỉ ra giả thiết không có nguyên tử là cần thiết, rồi cho một bảo đảm học thật sự trên một lớp có cấu trúc. Trao cho Tổng kết và Bài 02: một bảo đảm cho ERM cần chặn độ lệch $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$ khi $D$ chưa biết. Nguồn: ghi chú Bài 01, §8, §9.
- **Lý do / nối:** hai định nghĩa học → giới hạn của $L_S$.
- **Mục tiêu / nguồn:** 4, 5; §8, §9.

#### `6-01` Cận tổng quát hóa cho mọi thuật toán ERM — định nghĩa, câu hỏi · 2 phút
- **Mặt trang:**
  - Cận tổng quát hóa cho mọi thuật toán ERM: hàm $\beta(m,\delta)$ sao cho với mọi ERM $\hat A$, mọi $D$, $m$, $\delta$:
  - display $\Pr_{S\sim D^m}\Big[L_D\big(\hat A(S)\big)-L_S\big(\hat A(S)\big)\le\beta(m,\delta)\Big]\ge1-\delta$.
  - Cận tầm thường $\beta\equiv1$ luôn đúng, vì $L_D\le1$ với $\ell_{0\text{-}1}$.
  - **Câu hỏi:** trên $\mathcal M_{\mathcal X}$ với $\mathcal X=[0,1]$, có cận nào nhỏ hơn $\beta\equiv1$?
  - `[f]` **Trực quan.** Với cặp $(A_{\mathrm{gn}},D)$, khoảng cách tổng quát hóa bằng $1$ trên mọi tập huấn luyện, nên không có.
  - ≈ 54 âm tiết.
- **Ghi chú diễn giả:** Định nghĩa đặt tên cho loại cận mà phản ví dụ ghi nhớ bác bỏ: một cận cho khoảng cách tổng quát hóa, đúng cho mọi quy tắc chọn khi bằng nhau (thỏa điều kiện đo được) và mọi phân bố trên $\mathcal X\times\{0,1\}$. "Với mọi ERM" là điều kiện mạnh: để bác bỏ, chỉ cần một thuật toán ERM và một phân bố. Nguồn: ghi chú Bài 01, §8, Định nghĩa 01.28.
- **Lý do / nối:** vấn đề và trực quan của Hệ quả 01.29; ví dụ là phản ví dụ ghi nhớ của mạch 4 → phát biểu.
- **Mục tiêu / nguồn:** 5; Định nghĩa 01.28.

#### `6-02` Rủi ro thực nghiệm nhỏ không đủ làm bảo đảm học — kết quả · 1,5 phút
- **Mặt trang:**
  - **Giả thiết:** như Mệnh đề 01.15 ($\mathcal X=[0,1]$, $X\sim U[0,1]$, $Y=1$, $\mathcal H=\mathcal M_{\mathcal X}$, $\ell_{0\text{-}1}$); $S\sim D^m$ theo (T1); thuật toán ERM.
  - **Bảo đảm:** (Hệ quả 01.29)
  - (a) mọi cận tổng quát hóa cho mọi thuật toán ERM trên $\mathcal M_{\mathcal X}$ thỏa $\beta(m,\delta)\ge1$ với mọi $m$, $\delta$;
  - (b) $\Pr_S[L_D(A_{\mathrm{gn}}(S))\le\epsilon]=0$ với mọi $\epsilon\in(0,1)$ và mọi $m$, nên $A_{\mathrm{gn}}$ không là thuật toán học PAC cho $\mathcal M_{\mathcal X}$.
  - **Ý nghĩa:** với mỗi $\delta$, $\beta(m,\delta)$ không tiến về $0$ khi $m\to\infty$; chỉ biết $L_S$ nhỏ thì chưa đủ để bảo đảm học.
  - 60 âm tiết.
- **Ghi chú diễn giả:** thuật toán của phần (a) và (b); $D$ khả diễn với $h_{\equiv1}$; theo Nhận xét 01.26, $A_{\mathrm{gn}}$ cũng không là thuật toán học PAC bất khả diễn; câu cuối của Hệ quả 01.29 viết dạng khẳng định: "Lớp $\mathcal M_{\mathcal X}$ với $\mathcal X=[0,1]$ không học được PAC; chứng minh cần một lập luận cho mọi thuật toán, dựa trên định lý không có bữa trưa miễn phí (no-free-lunch theorem, UML §5.1)"; Nhận xét 01.30. Nguồn: ghi chú Bài 01, Hệ quả 01.29, Nhận xét 01.26, 01.30; UML §5.1.
- **Lý do / nối:** kết quả chính thứ tư; tách khỏi ý tưởng chứng minh theo quyết định của điều phối viên (mục 11, điểm 7: "yêu cầu sửa: tách phát biểu và ý tưởng chứng minh thành hai trang") → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 5; Hệ quả 01.29.

#### `6-03` Ý tưởng chứng minh: rủi ro thực nghiệm nhỏ không đủ — ý tưởng chứng minh · 1,5 phút
- **Mặt trang** (danh sách đánh số, bốn bước):
  1. (a) Lấy $\hat A=A_{\mathrm{gn}}$, $D$ của Mệnh đề 01.15: khoảng cách tổng quát hóa bằng $1$ trên mọi $S$ (giả thiết lớp chứa hàm ghi nhớ).
  2. Biến cố trong định nghĩa thành $\{1\le\beta(m,\delta)\}$, không phụ thuộc $S$: display $\Pr_{S\sim D^m}[1\le\beta(m,\delta)]=\mathbb 1[\beta(m,\delta)\ge1]$.
  3. Vì $1-\delta>0$, xác suất này ít nhất bằng $1-\delta$ chỉ khi $\beta(m,\delta)\ge1$.
  4. (b) $(D,\mathcal M_{\mathcal X})$ khả diễn với $h_{\equiv1}$ nhưng $L_D(A_{\mathrm{gn}}(S))=1>\epsilon$ trên mọi $S$ (giả thiết không có nguyên tử): $m_{A_{\mathrm{gn}}}(\epsilon,\delta)=\infty$.
  - 55 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả** (~150 âm tiết): lộ trình; $A_{\mathrm{gn}}$ là thuật toán ERM đo được (Phụ lục A(iii)); biến cố không phụ thuộc $S$ có xác suất $0$ hoặc $1$; hai giả thiết của Mệnh đề 01.15 vào qua (a) và (b) đúng như ghi chú; kỹ thuật lập luận "bác bỏ một khẳng định 'với mọi' bằng một cặp $(\hat A,D)$" ở ghi chú diễn giả, không có dòng "Kỹ thuật." trên mặt trang (giữ trần mật độ). Nguồn: ghi chú Bài 01, chứng minh Hệ quả 01.29, Phụ lục A(iii).
- **Lý do / nối:** trang ý tưởng chứng minh riêng theo quy định "own slide" → bỏ giả thiết không có nguyên tử.
- **Mục tiêu / nguồn:** 5; chứng minh Hệ quả 01.29.

#### `6-04` Ví dụ: hàm phân lớp ghi nhớ khi phân bố có nguyên tử — ví dụ (Ví dụ 01.11; bỏ giả thiết của Mệnh đề 01.15(b)) · 2,5 phút
- **Mặt trang:**
  - $\mathcal X=\{1,\ldots,5\}$; $D_1$: $D_{\mathcal X}$ đều, $Y=1$ chắc chắn; lớp $\mathcal M_{\mathcal X}$ gồm cả $32$ hàm $\mathcal X\to\{0,1\}$; $\ell_{0\text{-}1}$; $S\sim D_1^m$; $A_{\mathrm{gn}}$.
  - Mỗi điểm là một nguyên tử có xác suất $0{,}2$.
  - $A_{\mathrm{gn}}(S)=\mathbb 1[x\in\{X_1,\ldots,X_m\}]$ sai đúng tại các điểm vắng mặt; mỗi điểm vắng mặt với xác suất $0{,}8^m$.
  - Theo tính tuyến tính: display $\mathbb E_S\big[L_{D_1}(A_{\mathrm{gn}}(S))\big]=5\cdot0{,}2\cdot0{,}8^m=0{,}8^m$.
  - **Diễn giải:** $m=10$ cho $0{,}8^{10}\approx0{,}107$, và $0{,}8^m\to0$; kết luận $L_D(A_{\mathrm{gn}}(S))=1$ của Mệnh đề 01.15(b) cần giả thiết không có nguyên tử.
  - ≈ 58 âm tiết.
- **Ghi chú diễn giả:** So với ví dụ trên $[0,1]$, chỉ giả thiết không có nguyên tử bị bỏ; nhãn hằng và thuật toán ghi nhớ giữ nguyên. Hàm ghi nhớ vẫn là nghiệm ERM; điều thay đổi là quan sát mới có thể trùng một điểm đã thấy. Rủi ro bằng $0{,}2\sum_x\mathbb 1[x\notin\{X_1,\ldots,X_m\}]$; tính tuyến tính của kì vọng cho kết quả mà không cần phân bố của số điểm vắng mặt. Phân bố $D_1$ là phân bố của Nhận xét 01.21. Định lý không có bữa trưa miễn phí (no-free-lunch theorem, UML §5.1) nói về mọi thuật toán khi cỡ mẫu nhỏ so với $\lvert\mathcal X\rvert$; ví dụ này chỉ xét một thuật toán và một phân bố. Nguồn: ghi chú Bài 01, Ví dụ 01.11, Nhận xét 01.21, 01.30.
- **Lý do / nối:** kiểm tra "bỏ giả thiết" của Mệnh đề 01.15, đúng vị trí của ghi chú (§8, sau Hệ quả 01.29) → một bảo đảm học thật sự trên lớp hàm ngưỡng.
- **Mục tiêu / nguồn:** 5; Ví dụ 01.11.
- **Bản deck cuối (2026-11-15):** đúng storyboard; dòng "Mỗi điểm là một nguyên tử, xác suất $0{,}2$" gộp vào dòng dữ kiện (giữ 6 dòng). Ghi chú diễn giả bỏ câu "ví dụ này chỉ xét một thuật toán và một phân bố" (Detect).

#### `6-05` Cỡ mẫu của $A_{\max}$ trên lớp hàm ngưỡng — trực quan, kết quả, cận bằng số · 3 phút
- **Mặt trang:**
  - **Trực quan.** $A_{\max}$ chỉ sai ở các mức từ $t^\star$ đến $\hat t-1$; thất bại đòi bỏ sót cả một khối mức có khối lượng lớn hơn $\epsilon$.
  - **Giả thiết:** $\mathcal X=\{1,\ldots,K\}$, lớp hàm ngưỡng $\{h_t:\ t=1,\ldots,K+1\}$, $\ell_{0\text{-}1}$, $(D,\mathcal H)$ khả diễn với $h^\star=h_{t^\star}$; (T1).
  - **Kết luận** (Mệnh đề 01.31): với mọi $\epsilon,\delta\in(0,1)$, mọi $D$ như trên và mọi $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$, display $\Pr_{S\sim D^m}\big[L_D(A_{\max}(S))\le\epsilon\big]\ge1-\delta$.
  - **Ý nghĩa:** $\epsilon=0{,}1$, $\delta=0{,}05$ cho $m\ge\lceil10\ln20\rceil=30$ với mọi phân bố khả diễn; $14$ chỉ đủ cho $D_f$.
  - Hình F5b (`img/lec-01/can-co-mau.svg`), cột phải `grid2` hoặc dưới.
  - ≈ 52 âm tiết.
- **Ghi chú diễn giả:** Do đó $m_{A_{\max}}(\epsilon,\delta)\le\lceil\ln(1/\delta)/\epsilon\rceil$: một cỡ mẫu chung cho mọi phân bố khả diễn, đúng dạng "$\exists M\ \forall D$" của định nghĩa. Cận không phụ thuộc $K$ hay $D_{\mathcal X}$. Đây là một bảo đảm cho một thuật toán cụ thể trên một lớp có cấu trúc, khác với phản ví dụ ghi nhớ trên lớp không cam kết gì. Đọc hình: ba đường $0{,}8^m$ (xác suất thất bại đúng dưới $D_f$, $\epsilon=0{,}1$), $0{,}6^m$ ($\epsilon=0{,}25$) và $e^{-0{,}1m}$ (cận của mệnh đề), cắt mức $\delta=0{,}05$ lần lượt tại $m=14$, $6$, $30$. Mệnh đề ở mức phác thảo trong ghi chú; Bài tập 01.9(c) có lời giải đầy đủ cho cùng lớp. Nguồn: ghi chú Bài 01, §9, Mệnh đề 01.31 và đoạn sau.
- **Lý do / nối:** kết quả chính thứ năm; con số so với Ví dụ 01.9 → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 4; Mệnh đề 01.31.
- **Bản deck cuối (2026-11-15):** không có hình F5b (hình chuyển sang trang kỹ thuật chặn xác suất bỏ sót, nơi nó minh chứng $e^{-\epsilon m}$ so với xác suất đúng); công thức hiển thị gồm bất đẳng thức và "$m_{A_{\max}}(\epsilon,\delta)\le\lceil\ln(1/\delta)/\epsilon\rceil$" (phần thứ hai của "Bảo đảm." trong ghi chú). Lý do: trang có Trực quan, Giả thiết, Bảo đảm, Ý nghĩa không còn chỗ cho hình ở chiều cao 720 px. Ghi chú diễn giả bỏ câu "khác với phản ví dụ ghi nhớ …" (Detect).

#### `6-06` Ý tưởng chứng minh: cỡ mẫu của $A_{\max}$ — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** (danh sách đánh số)
  - 1. Vì khả diễn, $\hat t$ là mức nhỏ nhất có nhãn $1$ trong $S$ (hoặc $K+1$), và $L_D(h_{\hat t})=D_{\mathcal X}(\{t^\star,\ldots,\hat t-1\})$.
  - 2. Lấy khối đầu ngắn nhất $C=\{t^\star,\ldots,k\}$ có $D_{\mathcal X}(C)>\epsilon$.
  - 3. Có quan sát với $x_i\in C$ thì $\hat t\le k$ và $L_D\le\epsilon$; thất bại kéo theo không quan sát nào nằm trong $C$.
  - display $\Pr_S\big[L_D(h_{\hat t})>\epsilon\big]\le\big(1-D_{\mathcal X}(C)\big)^m\le(1-\epsilon)^m\le e^{-\epsilon m}$.
  - Giả thiết vào: khả diễn ở bước 1 và 3; (T1) ở lũy thừa $m$.
  - Hình F7 (`img/lec-01/vung-loi.svg`).
  - ≈ 47 âm tiết.
- **Ghi chú diễn giả** (~200 âm tiết): Đặt $G(t)=D_{\mathcal X}(\{t^\star,\ldots,t-1\})$, không giảm theo $t$, $G(t^\star)=0$. Nếu $G(K+1)\le\epsilon$ thì thuật toán không bao giờ thất bại. Nếu không, $k$ là mức lớn nhất trong $\{t^\star,\ldots,K\}$ có $G(k)\le\epsilon$, và $D_{\mathcal X}(C)=G(k+1)>\epsilon$. Một quan sát rơi vào $C$ có nhãn $1$ hầu chắc chắn (khả diễn), nên $\hat t\le k$ và $L_D(h_{\hat t})=G(\hat t)\le G(k)\le\epsilon$. Các quan sát độc lập (T1), nên xác suất không quan sát nào rơi vào $C$ là $(1-D_{\mathcal X}(C))^m$; bất đẳng thức $1-x\le e^{-x}$ cho bước cuối. Kiểm tra trên $D_f$ với $\epsilon=0{,}1$: $t^\star=3$, $G(3)=0$, $G(4)=0{,}2>0{,}1$, nên $k=3$, $C=\{3\}$, và cận $(1-0{,}2)^m=0{,}8^m$ trùng xác suất thất bại đúng của Ví dụ 01.9. Đọc hình: dãy mức $1,\ldots,K$, mốc $t^\star$, khối $C$ tô đậm với khối lượng lớn hơn $\epsilon$, và vị trí có thể của $\hat t$. Nguồn: ghi chú Bài 01, chứng minh Mệnh đề 01.31 (phác thảo), Ví dụ 01.9.
- **Lý do / nối:** lộ trình ba bước, giả thiết vào ở đâu → kỹ thuật ở bước cuối.
- **Mục tiêu / nguồn:** 4; chứng minh Mệnh đề 01.31.
- **Bản deck cuối (2026-11-15):** bố cục `grid2`: ba bước bên trái, hình F7 bên phải; dòng "Thất bại kéo theo không quan sát nào nằm trong $C$; theo (T1)," và công thức hiển thị chuỗi bất đẳng thức ở dưới. Giả thiết ghi trong bước ("Khả diễn: …", "(khả diễn: nhãn 1 trên $C$)", "theo (T1)"); không có dòng "Giả thiết vào:" (nhãn không hợp lệ).

#### `6-07` Chặn xác suất bỏ sót — kỹ thuật (lần đầu trong học phần) · 2 phút
- **Mặt trang:**
  - **Kỹ thuật.** Nếu $D_{\mathcal X}(C)>\epsilon$, xác suất $m$ quan sát i.i.d. đều nằm ngoài $C$ thỏa display $\big(1-D_{\mathcal X}(C)\big)^m\le(1-\epsilon)^m\le e^{-\epsilon m}$.
  - $e^{-\epsilon m}\le\delta$ khi và chỉ khi $m\ge\ln(1/\delta)/\epsilon$.
  - $\epsilon=0{,}1$, $\delta=0{,}05$: $e^{-3}\approx0{,}0498\le0{,}05$ tại $m=30$; $e^{-2{,}9}\approx0{,}0550$ tại $m=29$.
  - ≈ 30 âm tiết.
- **Ghi chú diễn giả:** Kỹ thuật biến một xác suất bỏ sót thành một cỡ mẫu tuyến tính theo $1/\epsilon$ và lôgarit theo $1/\delta$. Nó dùng hai điều: tính độc lập của các quan sát (lũy thừa $m$) và bất đẳng thức $1-x\le e^{-x}$ của phần tiên quyết. Bài 02 dùng lại kỹ thuật này, cùng bất đẳng thức hợp, cho lớp hữu hạn trong trường hợp khả diễn. Nguồn: ghi chú Bài 01, chứng minh Mệnh đề 01.31, Kiến thức tiên quyết; ghi chú Bài 02 (trường hợp khả diễn).
- **Lý do / nối:** kỹ thuật dùng lại qua học phần → tiêu đề mạch Tổng kết.
- **Mục tiêu / nguồn:** 4; Mệnh đề 01.31.
- **Bản deck cuối (2026-11-15):** `grid2`: kỹ thuật, điều kiện $m\ge\ln(1/\delta)/\epsilon$, con số $e^{-3}$, $e^{-2{,}9}$ và dòng "Dùng khi thất bại kéo theo một tập có khối lượng lớn hơn $\epsilon$ vắng mặt trong $S$." bên trái; hình F5b bên phải (đáy trục log $0{,}001$, các đường cắt ở mép trục, ghi rõ trong alt và ghi chú diễn giả).

### Mạch 7. Tổng kết (7 trang, 13 phút)

#### `7-00` 7. Tổng kết — tiêu đề mạch, điểm vào mạch 7 · 0,5 phút
- **Mặt trang:** "7."; h2 "Tổng kết"; `p.strand-lead` (bảng mạch); không có dòng từ khóa.
- **Ghi chú diễn giả:** Kế thừa: năm kết quả và hai định nghĩa học PAC. Nhiệm vụ: gom giả thiết của từng kết quả, trả lời vấn đề trung tâm, tự kiểm tra, giao bài tập. Không có khái niệm mới. Nguồn: ghi chú Bài 01, §9–§12.
- **Lý do / nối:** mạch 6 → bảng tổng kết.
- **Mục tiêu / nguồn:** tất cả; §9–§12.

#### `7-01` Bảng tổng kết — tổng kết · 2,5 phút
- **Mặt trang:** bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh` (≈ 75 âm tiết, trần 80):

| Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh |
|---|---|---|
| $\mathbb E_S[L_S(h)]=L_D(h)$ (Mệnh đề 01.7) | $h$ không phụ thuộc $S$; mỗi $Z_i\sim D$ | tính tuyến tính của kì vọng |
| $L_S(A_{\mathrm{gn}}(S))=0$, $L_D(A_{\mathrm{gn}}(S))=1$ (Mệnh đề 01.15) | $D_{\mathcal X}$ không có nguyên tử; $\mathcal H=\mathcal M_{\mathcal X}$ | tập hữu hạn có xác suất $0$, bất đẳng thức hợp |
| $h_{\mathrm{Bayes}}=\mathbb 1[\eta\ge\tfrac12]$; ngưỡng $\tfrac{c_{FP}}{c_{FP}+c_{FN}}$ (Mệnh đề 01.23) | $\eta$ đo được; xét mọi hàm đo được | tối thiểu hóa từng điểm, rồi lấy kì vọng |
| $\beta(m,\delta)\ge1$ trên $\mathcal M_{\mathcal X}$ (Hệ quả 01.29) | như Mệnh đề 01.15 | một cặp $(A_{\mathrm{gn}},D)$ làm phản ví dụ |
| $m_{A_{\max}}\le\lceil\ln(1/\delta)/\epsilon\rceil$ (Mệnh đề 01.31) | khả diễn; (T1) | thất bại kéo theo bỏ sót tập $C$ có khối lượng lớn hơn $\epsilon$; $(1-\epsilon)^m\le e^{-\epsilon m}$ |

- **Ghi chú diễn giả:** Cột giữa là giả thiết mà bỏ đi thì kết luận sai, kèm phản ví dụ của bài: $A_{\max}$ dưới $D_f$ với $m=1$ ($\mathbb E L_S=0<0{,}36$); hàm ghi nhớ trên năm điểm ($\mathbb E L=0{,}8^m$); dưới $D_\eta$ hàm Bayes nằm ngoài lớp hàm ngưỡng. Bảo đảm theo kì vọng (Mệnh đề 01.7) khác bảo đảm với xác suất cao (Mệnh đề 01.31); bảo đảm cho lớp ("học được PAC") khác bảo đảm cho một thuật toán ("$A$ là thuật toán học PAC"). Nguồn: ghi chú Bài 01, §5–§9.
- **Lý do / nối:** một hàng cho mỗi kết quả chính → trả lời vấn đề trung tâm.
- **Mục tiêu / nguồn:** 2–5; §5–§9.
- **Bản deck cuối (2026-11-15):** cột "Kết quả" mở bằng số hiệu ("Mệnh đề 01.7: …") và rút gọn công thức để mỗi hàng không quá hai dòng (bảng cũ tràn khung); 65 âm tiết (trần 80 cho bảng tổng kết).

#### `7-02` Vấn đề trung tâm — tổng kết · 2 phút
- **Mặt trang:** danh sách câu trả lời cho cả bài (≈ 75 âm tiết):
  - Học là chọn $A(S)$ với $L_D(A(S))\le\inf_{h\in\mathcal H}L_D(h)+\epsilon$, với xác suất ít nhất $1-\delta$ theo $S\sim D^m$.
  - Cỡ mẫu đủ $M(\epsilon,\delta)$ không phụ thuộc $D$; thuật toán được chọn trước khi biết $D$.
  - $L_S(h)$ ước lượng không chệch $L_D(h)$ khi $h$ không phụ thuộc $S$; với $h=A(S)$ thì nói chung không.
  - $L_S$ nhỏ không đủ: trên $\mathcal M_{\mathcal X}$, một nghiệm ERM có $L_S=0$ và $L_D=1$.
  - Trên lớp hàm ngưỡng, $A_{\max}$ đạt bảo đảm khi $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$.
- **Ghi chú diễn giả:** Các câu trả lời theo thứ tự lập luận của bài, không theo mạch. Câu hỏi mở đầu được trả lời trọn: $h_3$ và $h_4$ chỉ khác nhau tại $x=3$, $S_f$ không chứa $x=3$; $S_f$ cũng có thể đến từ phân bố có hàm gán nhãn $h_4$, nên trên $S_f$ không thuật toán nào trả về được một hàm có rủi ro $0$ dưới cả hai phân bố. Học PAC chỉ đòi xác suất gặp những tập như $S_f$ đủ nhỏ, với một ngưỡng cỡ mẫu chung cho mọi phân bố. Nguồn: ghi chú Bài 01, §7 (đoạn cuối), §11.
- **Lý do / nối:** trả lời vấn đề của trang 1-05 cho cả bài → tự kiểm tra.
- **Mục tiêu / nguồn:** tất cả; §7, §11.
- **Bản deck cuối (2026-11-15):** đúng storyboard (53 âm tiết).

#### `7-03` Bài tập: ngưỡng chặn thư rác — bài tập tổng hợp (Bài tập 01.1(d)), lời giải trên mặt trang · 2 phút
- **Mặt trang:**
  - Lọc thư rác (spam filtering): $y=1$ là thư rác; chặn nhầm thư thường tốn $4$, để lọt thư rác tốn $1$.
  - **Câu hỏi:** tìm ngưỡng trên $\eta(x)$ của quy tắc Bayes dưới $\ell_c$; vì sao không nên giả sử $(D,\mathcal H)$ khả diễn?
  - `[f]` **Lời giải:** chặn nhầm là dương tính giả, nên $(c_{FP},c_{FN})=(4,1)$, ngưỡng $\tfrac{c_{FP}}{c_{FP}+c_{FN}}=\tfrac45$.
  - `[f]` Hai thư cùng tập từ có thể khác nhãn, nên có thể $\eta(x)\in(0,1)$ trên một tập có xác suất dương.
  - `[f]` Khi đó $L_D^{\mathrm{Bayes}}=\mathbb E\min\{\eta(X),1-\eta(X)\}>0$, nên không lớp nào khả diễn.
  - 73 âm tiết (ngoại lệ, xem mục 14).
- **Ghi chú diễn giả:** mô hình phù hợp là học PAC bất khả diễn; ba kết quả dùng (Mệnh đề 01.23(b), 01.23(a), định nghĩa khả diễn); mô tả véc-tơ từ $x\in\{0,1\}^p$; so ngưỡng $\tfrac15$ của ứng dụng sàng lọc với $\tfrac45$; lỗi thường gặp (đưa $\eta$ vào thuật toán). Nguồn: tệp bài tập, Bài tập 01.1(d) và lời giải; ghi chú Bài 01, Mệnh đề 01.23, Phụ lục B.
- **Lý do / nối:** bài tập tổng hợp của mạch Tổng kết theo quy định `CLAUDE.md` § Slide decks và quyết định của điều phối viên (mục 11, điểm 8). Chọn Bài tập 01.1(d) vì nó nối hàm lỗi có trọng số (mạch 2), quy tắc Bayes và rủi ro Bayes, tính khả diễn và học PAC bất khả diễn (mạch 5) trên một bài toán mới, lời giải ba dòng; Bài tập 01.9(c) chỉ lặp con số $30$ so với $14$ đã có ở mạch 6. Số liệu và kết quả giữ đúng `exercises.md` ($(c_{FP},c_{FN})=(4,1)$, ngưỡng $\tfrac45$). → câu hỏi tự kiểm tra.
- **Mục tiêu / nguồn:** 2, 4; Bài tập 01.1(d).

#### `7-04` Câu hỏi tự kiểm tra — tổng kết · 3,5 phút
- **Mặt trang:** "Câu hỏi: trả lời và nêu kết quả đã dùng." rồi bốn câu (≈ 70 âm tiết):
  1. Trong $L_D(A(S))$, $D$ cố định. Đại lượng nào ngẫu nhiên, theo phân bố nào?
  2. Trên $S_\eta$, nghiệm ERM trên lớp hàm ngưỡng có rủi ro kì vọng dưới $D_\eta$ bằng bao nhiêu?
  3. Với $\delta=0{,}05$, có thể nói hàm phân lớp vừa học đúng với xác suất $95\%$ không?
  4. Cỡ $14$ của ví dụ $A_{\max}$ dưới $D_f$ có phải là $m_{A_{\max}}(0{,}1;\ 0{,}05)$ không?
- **Ghi chú diễn giả** (đáp án dự kiến): (1) $A(S)$ ngẫu nhiên vì là hàm của $S\sim D^m$, nên $L_D(A(S))$ là biến ngẫu nhiên theo $D^m$; khi thuật toán sinh thêm $\xi$, theo cả $S$ và $\xi$ (bảng nguồn ngẫu nhiên §1). (2) Tùy quy tắc chọn khi bằng nhau, vì tập nghiệm là $\{h_2,h_3,h_5\}$: $0{,}32$, $0{,}22$ hoặc $0{,}28$ (Ví dụ 01.6). (3) Không: $0{,}95$ là xác suất theo các lần lấy tập huấn luyện lặp lại; trong 100 lần huấn luyện có khoảng 95 lần hàm học được có rủi ro không quá $\epsilon$ (Nhận xét 01.19). (4) Không nhất thiết: $14$ chỉ đủ cho $D_f$, còn $m_{A_{\max}}$ phải đúng với mọi phân bố khả diễn; vì $D_f$ khả diễn và thất bại ở $m=13$, $14\le m_{A_{\max}}(0{,}1;\ 0{,}05)\le30$ (Ví dụ 01.9, Mệnh đề 01.31; storyboard mục 5, V16). Nguồn: ghi chú Bài 01, §11, Ví dụ 01.6, 01.9, Nhận xét 01.19, Mệnh đề 01.31.
- **Lý do / nối:** câu hỏi cuối buổi của ghi chú (1–3) và một câu về độ phức tạp mẫu (4) → bài tập về nhà.
- **Mục tiêu / nguồn:** 1, 2, 4; §11.
- **Bản deck cuối (2026-11-15):** câu 4 viết lại theo quyết định của điều phối viên: "Cỡ $14$ của Ví dụ 01.9 và cỡ $30$ của Mệnh đề 01.31 ứng với thứ tự lượng từ nào?"; lời giải (ghi chú diễn giả): $14$ là cỡ mẫu đủ cho riêng cặp $(A_{\max},D_f)$, dạng "$\forall D\ \exists m$" (Ví dụ 01.9, đoạn cuối); $30=\lceil10\ln20\rceil$ đúng cho mọi phân bố khả diễn, dạng "$\exists M\ \forall D$" (Mệnh đề 01.31). Bỏ đáp án "Không nhất thiết" và cận $14\le m_{A_{\max}}\le30$. Câu 1, 2 rút chữ (câu 1 bỏ "$D$ cố định", câu 2 viết $L_{D_\eta}$) để giữ trần 60; dòng dẫn "Câu hỏi: trả lời, nêu kết quả đã dùng." 60 âm tiết.

#### `7-05` Bài tập về nhà — tổng kết · 1,5 phút
- **Mặt trang:** bảng `Mục | Bài tập`:

| Mục | Bài tập |
|---|---|
| Bài toán học thống kê | 01.1 |
| Rủi ro thực nghiệm và tối thiểu hóa rủi ro thực nghiệm | 01.2, 01.3 |
| Thuật toán ghi nhớ và thiên kiến quy nạp | 01.4, 01.6 |
| Học PAC | 01.5, 01.7, 01.8, 01.10, 01.11 |
| Rủi ro thực nghiệm nhỏ và bảo đảm học | 01.9 |

  - Dòng liên kết: "Ghi chú bài giảng · Bài tập" (viewer, kèm `&deck=lecture-01-mo-hinh-hoc.html`).
- **Ghi chú diễn giả:** Năm bài đầu là bài gốc, sáu bài sau chọn từ UML (§2.4, §3.5). Bài tập 01.2 còn dùng quy tắc Bayes và rủi ro vượt mức của mạch Học PAC; Bài tập 01.11 (thử thách) chứng minh tính tối ưu của quy tắc Bayes. Bài tập 01.3 mở rộng ví dụ một quan sát của mạch 3 sang hai thuật toán có độ lệch ngược chiều. Bài tập 01.9 so lớp hình tròn đồng tâm với lớp hàm ngưỡng, cùng kỹ thuật chặn xác suất bỏ sót. Nguồn: ghi chú Bài 01, §10; tệp bài tập Bài 01.
- **Lý do / nối:** ánh xạ bài tập vào mạch → tài liệu.
- **Mục tiêu / nguồn:** tất cả; §10, `exercises.md`.
- **Bản deck cuối (2026-11-15):** đúng storyboard; dòng liên kết "Ghi chú bài giảng · Bài tập" dùng `&deck=lecture-01-mo-hinh-hoc.html`.

#### `7-06` Tài liệu tham khảo — tổng kết · 1 phút
- **Mặt trang:**
  - Shalev-Shwartz và Ben-David (2014), *Understanding Machine Learning: From Theory to Algorithms*: §§2.1–2.3 (mô hình học, ERM, quá khớp, thiên kiến quy nạp); §§3.1–3.2 (học PAC, học PAC bất khả diễn); §5.1 (định lý không có bữa trưa miễn phí).
  - Dòng nối: "Bài 02: Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn." (liên kết thêm khi deck Bài 02 có tên tệp).
- **Ghi chú diễn giả:** Trước buổi học: UML §§2.1–2.2; sau buổi học: §2.3, §§3.1–3.2 và bài tập §2.4, §3.5; mở rộng: §5.1. Khác biệt so với UML: $D$ là phân bố liên hợp ngay từ đầu; mức tốt nhất trong lớp viết $\inf$; có ERM xấp xỉ; họ phân bố của học PAC bất khả diễn là các phân bố có rủi ro hữu hạn; tính đo được đòi đồng thời theo tập huấn luyện và quan sát. Cầu nối: Ví dụ 01.9 tính được xác suất thất bại vì đã biết $D_f$; khi $D$ chưa biết, cần chặn $\Pr(\lvert L_S(h)-L_D(h)\rvert>\epsilon)$ cho từng $h$ cố định, với giả thiết quan sát độc lập và hàm lỗi bị chặn, rồi cho nghiệm ERM chọn từ $\lvert\mathcal H\rvert$ ứng viên; công cụ là bất đẳng thức Hoeffding và bất đẳng thức hợp. Nguồn: ghi chú Bài 01, §11, §12.
- **Lý do / nối:** trang cuối theo quy định → (hết).
- **Mục tiêu / nguồn:** —; §12.
- **Bản deck cuối (2026-11-15):** bốn gạch đầu dòng (sách, §§2.1–2.3, §§3.1–3.2, §5.1) và dòng "Bài 02: Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn." (chưa liên kết).

## 7. Hành trình khái niệm

Thứ tự bước theo quy định: vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh → kỹ thuật hoặc kiểm tra. Các bước có thể chung trang nhưng không đảo thứ tự, trừ ví dụ dẫn nhập đứng cùng vấn đề (ghi rõ ở cột cuối).

| Kết quả hoặc khái niệm | Vấn đề | Trực quan | Ví dụ | Phát biểu | Ý tưởng chứng minh | Kỹ thuật / kiểm tra | Gộp, `không áp dụng`, lý do |
|---|---|---|---|---|---|---|---|
| Rủi ro kì vọng và bài toán học (Định nghĩa 01.1, 01.5) | 1-06 | 2-03 | 2-02, 2-04 | 2-03, 2-05 | `không áp dụng` (định nghĩa) | 2-04 (Câu hỏi: $L^c_{D_\eta}(h_2)$) | Ví dụ dẫn nhập 1-06 làm cụ thể vấn đề "cùng khớp tập huấn luyện, khác trên dữ liệu mới". |
| Mệnh đề 01.7 | 2-03 (Câu hỏi về đo trên tập huấn luyện), 3-01 ($\tfrac13$ so với $0{,}22$) | 3-02 | 3-01, 3-02 (dòng "Ví dụ.") | 3-02 | 3-03 | 3-03 (kỹ thuật); 3-05 (bỏ giả thiết: $0<0{,}36$); 3-06 (cách sửa) | Trực quan, ví dụ một dòng và phát biểu chung trang 3-02, theo đúng thứ tự trên mặt trang. ERM (3-04) đứng giữa 3-03 và 3-05 vì ghi chú định nghĩa ERM trước Nhận xét 01.9, và phản ví dụ 3-05 cần $A_{\max}$. |
| ERM và quy tắc chọn khi bằng nhau (Định nghĩa 01.8, Thuật toán 01.13) | 3-01 (ba hàm cùng $L_S$) | 3-04 (dòng "Diễn giải:") | 3-04 | 3-04 | `không áp dụng` | 3-07 (Bài tập 01.2(a)) | Định nghĩa và ví dụ chung trang. |
| Mệnh đề 01.15 | 3-04, 4-00 (quy tắc chọn quyết định rủi ro) | 4-02 | 4-01 | 4-02 | 4-03 | 4-04 (kỹ thuật); 4-05 (Bài tập 01.4(a)); 4-06 (bỏ "lớp chứa mọi hàm đo được"); 6-04 (bỏ "không có nguyên tử", vị trí §8 của ghi chú) | 4-01 là ví dụ dẫn nhập của phản ví dụ (liệt kê dữ kiện), đứng trước trực quan; nó làm cụ thể vấn đề "hai nghiệm ERM trên cùng $S$". |
| Học PAC khả diễn (Định nghĩa 01.16, 01.18, 01.20) | 4-06 (bảo đảm phải cho phép thất bại), 5-01 | 5-01 | 5-01 ($0{,}8^m$, $0{,}999^{500}$) | 5-02, 5-03, 5-04 | `không áp dụng` (định nghĩa) | 5-05 (Ví dụ 01.9); 5-06 (Bài tập 01.5(d), câu 4) | Thứ tự lượng từ có trang riêng (5-03) theo yêu cầu của người dùng. |
| Mệnh đề 01.23 | 5-07 (mọi hàm sai ít nhất $0{,}05$); câu hỏi thực hành của ghi chú §3 (ghi chú diễn giả 2-03) | 5-07 | 5-07 | 5-08 | 5-09 | 5-09 (dòng "Kỹ thuật."); 5-10 (Ví dụ 01.10 dưới $\ell_c$) | Vấn đề, trực quan, ví dụ chung trang 5-07. |
| Rủi ro vượt mức, học PAC bất khả diễn (Định nghĩa 01.24, 01.25) | 5-07 (đối tượng so sánh phải dương) | 5-11 (hình F6) | 5-11 | 5-11, 5-12 | `không áp dụng` (định nghĩa) | 5-12 (dòng "Lưu ý:"; hai lý do ở ghi chú diễn giả) | — |
| Hệ quả 01.29 | 6-01 (Câu hỏi) | 6-01 (`[f]` "Trực quan.") | 4-01, 4-02 (cặp $(A_{\mathrm{gn}},D)$, nhắc tên ở 6-01) | 6-02 | 6-03 | 6-04 (bỏ giả thiết không có nguyên tử) | Không có trang ví dụ mới: ví dụ là phản ví dụ của mạch 4. Deck cuối: phát biểu (6-02) và ý tưởng chứng minh (6-03) tách hai trang theo quyết định của điều phối viên (mục 11, điểm 7). |
| Mệnh đề 01.31 | 5-05, 5-04 ($14$ chỉ cho $D_f$; $m_A$ phải đúng cho mọi $D$) | 6-05 | 5-05 (Ví dụ 01.9, trường hợp $D_f$) | 6-05 | 6-06 | 6-07 (kỹ thuật); 6-05 ("Ý nghĩa:" $30$ so với $14$); 6-06 (ghi chú diễn giả: $C=\{3\}$ dưới $D_f$); 7-04 câu 4 | Ví dụ đứng ở mạch 5 vì Ví dụ 01.9 thuộc §6 của ghi chú. |

Thời lượng theo mạch (deck cuối): 8 + 15 + 21 + 15 + 32 + 16 + 13 = 120 phút; 6 + 6 + 8 + 7 + 13 + 8 + 7 = 55 trang.

## 8. Hình vẽ

Mọi hình là SVG trong `2627-1/img/lec-01/`, `role="img"`, có `<title>` và alt cụ thể; màu không là tín hiệu duy nhất (dùng hình dạng điểm, kiểu nét, mẫu gạch); chữ trong hình bằng Unicode (không KaTeX), cỡ chữ đọc được ở 390 px. Dữ liệu chính xác lấy từ mục 5.

| Mã | Tệp | Trang | Nội dung và dữ liệu | Alt dự kiến |
|---|---|---|---|---|
| F1 | `hai-ham-nguong.svg` | 1-06 | Trục năm mức $1,\ldots,5$, ghi "mỗi mức 20%". Hàng 1: nhãn thật $y=\mathbb 1[x\ge3]$. Hàng 2: bốn quan sát của $S_f$, nhãn 0 vẽ ô vuông rỗng tại 1, 2, nhãn 1 vẽ chấm tròn đặc tại 4, 5; mức 3 khung nét đứt "không có quan sát". Hàng 3, 4: giá trị của $h_3$ và $h_4$ tại từng mức (0 hoặc 1). Cột $x=3$ gạch chéo, chú thích "h₄ sai". | "Năm mức đo từ 1 đến 5, mỗi mức 20% dân số. Tập huấn luyện có nhãn 0 tại mức 1 và 2, nhãn 1 tại mức 4 và 5, không có quan sát ở mức 3. Hàm h3 báo dương tính từ mức 3, hàm h4 từ mức 4; hai hàm chỉ khác nhau ở mức 3, nơi nhãn thật là 1." |
| F2a | `eta-nguong.svg` | 5-07 | Năm cột $\eta(x)$ cao $0;\ 0{,}25;\ 0{,}75;\ 0{,}4;\ 1$ với nhãn số "0", "1/4", "3/4", "2/5", "1"; đường ngang nét đứt tại $\tfrac12$; cột không thấp hơn $\tfrac12$ ($x=3$, $5$) có mẫu gạch và chữ "báo 1". | "Xác suất có điều kiện của nhãn 1 tại năm mức: 0, 1/4, 3/4, 2/5 và 1. Đường ngang tại 1/2. Chỉ mức 3 và mức 5 đạt hoặc vượt 1/2, nên hàm Bayes dưới hàm lỗi 0–1 báo dương tính đúng tại hai mức này." |
| F2b | `eta-hai-nguong.svg` | 5-10 | Như F2a, thêm đường chấm tại $\tfrac15$ (kiểu nét khác đường $\tfrac12$); các cột không thấp hơn $\tfrac15$ ($x=2,\ldots,5$) có dấu tam giác phía trên, chú thích "báo 1 dưới ℓc". | "Năm cột xác suất có điều kiện như hình trước, với hai đường ngang tại 1/2 và 1/5. Dưới hàm lỗi có trọng số với chi phí bỏ sót gấp bốn, ngưỡng là 1/5, nên hàm Bayes báo dương tính tại các mức 2 đến 5; đó là hàm ngưỡng h2." |
| F3 | `rui-ro-nguong.svg` | 3-01 | Trục ngang $t=1,\ldots,6$, trục dọc $0$ đến $0{,}6$. Chấm tròn nối nét liền: $L_{S_\eta}(h_t)=0{,}5;\ 0{,}333;\ 0{,}333;\ 0{,}5;\ 0{,}333;\ 0{,}5$. Ô vuông nối nét đứt: $L_{D_\eta}(h_t)=0{,}52;\ 0{,}32;\ 0{,}22;\ 0{,}32;\ 0{,}28;\ 0{,}48$. Ghi nhãn trực tiếp ở cuối mỗi đường; ngoặc nhóm $t=2,3,5$ "cùng L_S = 1/3"; ghi "0,22" tại $t=3$. | "Rủi ro thực nghiệm trên tập huấn luyện cỡ 6 và rủi ro kì vọng của sáu hàm ngưỡng. Ba ngưỡng 2, 3 và 5 cùng có rủi ro thực nghiệm 1/3, nhưng rủi ro kì vọng lần lượt là 0,32, 0,22 và 0,28; chỉ ngưỡng 3 đạt mức nhỏ nhất 0,22." |
| F4 | `ghi-nho.svg` | 4-01 | Trục $[0,1]$ với vạch $0$, $0{,}5$, $1$. Năm điểm huấn luyện (tam giác trên trục) tại $0{,}12;\ 0{,}31;\ 0{,}47;\ 0{,}68;\ 0{,}90$, mọi nhãn bằng 1; deck cuối ghi dữ liệu trong hình "m = 5, nhãn 1: x = 0,12; 0,31; 0,47; 0,68; 0,90" (quyết định mục 11.9: chú thích nêu dữ liệu, không chữ "minh họa"). Hàng trên: $h_{\equiv1}$, đường liền ở mức 1, "rủi ro 0". Hàng dưới: $\mathbb 1_F$, đường ở mức 0 và năm chấm đặc ở mức 1 tại năm điểm, "rủi ro 1". | "Trên đoạn từ 0 đến 1 có năm điểm huấn luyện, tất cả mang nhãn 1. Hàm hằng 1 đúng ở mọi điểm, rủi ro 0. Hàm phân lớp ghi nhớ chỉ bằng 1 tại năm điểm đã thấy và bằng 0 ở mọi nơi khác, nên sai với mọi quan sát mới không trùng năm điểm đó, rủi ro 1." |
| F5a | `that-bai-df.svg` | 5-05 | Trục ngang $m=0,\ldots,20$ (điểm rời tại số nguyên), trục dọc logarit $0{,}001$ đến $1$ (vạch $1$, $0{,}1$, $0{,}01$, $0{,}001$; đường chấm $\delta=0{,}05$). Deck cuối: đáy trục $0{,}001$ theo quyết định của điều phối viên; $0{,}6^m$ vẽ đến $m=13$ ($0{,}6^{13}\approx0{,}0013$, $0{,}6^{14}\approx0{,}00078<0{,}001$), chú giải ghi "dưới 0,001 từ m = 14". Chấm tròn nét liền $0{,}8^m$; tam giác nét đứt $0{,}6^m$; đường ngang chấm $\delta=0{,}05$; vạch đứng tại $m=6$ và $m=14$. Kiểm tra: $0{,}8^{13}=0{,}0550$, $0{,}8^{14}=0{,}0440$, $0{,}6^5=0{,}0778$, $0{,}6^6=0{,}0467$. | "Xác suất thất bại của thuật toán chọn ngưỡng lớn nhất dưới phân bố tất định, theo cỡ mẫu, trên thang logarit. Với độ chính xác 0,1, xác suất là 0,8 mũ m và xuống dưới 0,05 từ m bằng 14; với độ chính xác 0,25, xác suất là 0,6 mũ m và xuống dưới 0,05 từ m bằng 6." |
| F5b | `can-co-mau.svg` | 6-07 (deck cuối; storyboard đặt ở trang phát biểu Mệnh đề 01.31, trang đó không đủ chiều cao) | Như F5a với $m=0,\ldots,32$, thêm đường gạch chấm $e^{-0{,}1m}$; vạch đứng tại $6$, $14$, $30$; đáy trục $0{,}001$, các đường cắt ở mép trục ($0{,}8^{31}\approx0{,}00099$), ghi trong alt và ghi chú diễn giả. Kiểm tra: $e^{-2{,}9}=0{,}0550$, $e^{-3}=0{,}0498$. | "Ba đường theo cỡ mẫu trên thang logarit: 0,8 mũ m và 0,6 mũ m là xác suất thất bại đúng dưới phân bố tất định, e mũ trừ 0,1m là cận của Mệnh đề 01.31 cho mọi phân bố khả diễn. Ba đường xuống dưới mức 0,05 lần lượt tại m bằng 14, 6 và 30." |
| F6 | `rui-ro-vuot-muc.svg` | 5-11 | Trục rủi ro từ $0{,}15$ đến $0{,}35$; ba mốc $0{,}18$ ("rủi ro Bayes"), $0{,}22$ ("tốt nhất trong lớp, h₃"), $0{,}32$ ("h₂"); ngoặc $0{,}04$ "phụ thuộc lớp", ngoặc $0{,}10$ "do chọn h₂", ngoặc dưới $0{,}14$ "so với rủi ro Bayes". | "Trục rủi ro với ba mốc: rủi ro Bayes 0,18, rủi ro nhỏ nhất trong lớp hàm ngưỡng 0,22 và rủi ro của h2 là 0,32. Rủi ro vượt mức của h2 so với rủi ro Bayes, 0,14, tách thành 0,04 do lớp giả thuyết và 0,10 do chọn h2 thay cho h3." |
| F7 | `vung-loi.svg` | 6-06 | Sơ đồ (không số liệu): dãy ô mức $1,\ldots,K$; các ô trước $t^\star$ ghi "nhãn 0", từ $t^\star$ ghi "nhãn 1"; khối $C=\{t^\star,\ldots,k\}$ gạch chéo, chú thích "khối lượng > ε"; mũi tên "có quan sát trong C ⇒ t̂ ≤ k ⇒ rủi ro ≤ ε"; ngoặc "vùng lỗi t*, …, t̂−1". | "Các mức từ 1 đến K, nhãn 0 trước mức t* và nhãn 1 từ mức t*. Khối C gồm các mức từ t* đến k có tổng khối lượng lớn hơn epsilon. Nếu tập huấn luyện có một quan sát trong C, ngưỡng chọn được không vượt k và rủi ro không quá epsilon; thất bại đòi mọi quan sát nằm ngoài C." |

## 9. Trang tổng kết

Chi tiết từng trang ở mục 6 (7-01 đến 7-06). Tóm tắt:
- **Bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh`:** năm hàng, cho Mệnh đề 01.7, 01.15, 01.23, Hệ quả 01.29, Mệnh đề 01.31 (7-01).
- **Vấn đề trung tâm:** năm câu trả lời cho cả bài (7-02), không theo mạch.
- **Bài tập tổng hợp:** Bài tập 01.1(d), ngưỡng chặn thư rác và vì sao không giả sử khả diễn, "Lời giải:" trên mặt trang (7-03; thêm theo quyết định của điều phối viên).
- **Câu hỏi tự kiểm tra:** bốn câu; ba câu đầu là câu hỏi cuối buổi của ghi chú §11, câu 4 (viết lại theo quyết định của điều phối viên) hỏi cỡ $14$ của Ví dụ 01.9 và cỡ $30$ của Mệnh đề 01.31 ứng với thứ tự lượng từ nào; lời giải chỉ dùng ghi chú (7-04).
- **Bảng `Mục | Bài tập`:** khớp `exercises.md` (01.1–01.11), mỗi bài một mạch (7-05); liên kết "Ghi chú bài giảng · Bài tập".
- **Tài liệu tham khảo:** UML §§2.1–2.3, §§3.1–3.2, §5.1 (7-06).
- **Câu nối sang Bài 02:** "Bài 02: Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn." (7-06); nội dung cầu nối (chặn $\Pr(\lvert L_S(h)-L_D(h)\rvert>\epsilon)$ khi $D$ chưa biết, bằng bất đẳng thức Hoeffding và bất đẳng thức hợp) ở ghi chú diễn giả.

## 10. Bảng thuật ngữ Việt–Anh của deck

Thuật ngữ xuất hiện trên mặt trang, theo ghi chú và `thuat-ngu.md`; cột cuối là trang có tiếng Anh trong ngoặc (lần dùng đầu trên trang nội dung).

| Tiếng Việt | Tiếng Anh | Trang |
|---|---|---|
| cận dưới đúng | infimum | 1-02 |
| hầu chắc chắn | almost surely | 4-02 (deck cuối; chuyển khỏi 1-02 để giữ trần) |
| hàm chỉ báo | indicator | 1-06 (ghi chú diễn giả) |
| độc lập cùng phân bố (i.i.d.) | independent and identically distributed | 1-02 (mặt trang ghi viết tắt; tên đầy đủ ở ghi chú diễn giả) |
| phân bố biên | marginal distribution | 1-02 |
| tối thiểu hóa rủi ro thực nghiệm (ERM) | empirical risk minimization | 1-02 |
| học xấp xỉ với xác suất cao (PAC) | probably approximately correct | 1-02 |
| tập huấn luyện | training sample | 1-06 |
| hàm phân lớp | classifier | 1-06 |
| hàm dự đoán | predictor | 2-01 |
| quan sát | example | 2-01 |
| cỡ mẫu | sample size | 2-01 |
| lớp giả thuyết | hypothesis class | 2-01 |
| hàm lỗi | loss function | 2-01 |
| thuật toán học | learning algorithm | 2-01 |
| hàm lỗi 0–1 | 0–1 loss | 2-02 |
| rủi ro kì vọng | population risk, expected risk | 2-03 |
| âm tính giả (FN), dương tính giả (FP) | false negative, false positive | 2-03 |
| hàm lỗi có trọng số | cost-weighted loss | 2-03 |
| rủi ro thực nghiệm | empirical risk | 3-01 |
| ước lượng không chệch | unbiased estimator | 3-02 (ghi chú diễn giả; mặt trang dùng "tính không chệch") |
| quy tắc chọn khi bằng nhau | tie-breaking | 3-04 |
| khoảng cách tổng quát hóa | generalization gap | 3-06 |
| thuật toán ghi nhớ, hàm phân lớp ghi nhớ | memorizing algorithm, memorizing classifier | 4-01 |
| không có nguyên tử, nguyên tử | atomless, atom | 4-02 |
| bất đẳng thức hợp | union bound | 4-04 |
| thiên kiến quy nạp | inductive bias | 4-06 |
| quá khớp | overfitting | 4-02 (ghi chú diễn giả) |
| xác suất thất bại | failure probability | 5-01 |
| tham số độ chính xác | accuracy parameter | 5-01 |
| khả diễn | realizable | 5-02 |
| học được PAC | PAC learnable | 5-02 |
| không phụ thuộc phân bố | distribution-free | 5-03 |
| độ tin cậy | confidence | 5-02 (ghi chú diễn giả) |
| độ phức tạp mẫu | sample complexity | 5-04 |
| rủi ro Bayes | Bayes risk | 5-07 |
| hàm phân lớp tối ưu Bayes | Bayes optimal classifier | 5-08 (deck cuối: mặt trang) |
| đối tượng so sánh | comparator | 5-07 (ghi chú diễn giả), 5-12 (mặt trang) |
| khối lượng xác suất | probability mass | 5-01 (ghi chú diễn giả) |
| rủi ro có điều kiện | conditional risk | 5-09 |
| rủi ro vượt mức | excess risk | 5-11 |
| học PAC bất khả diễn | agnostic PAC learning | 5-12 |
| học đúng lớp, học ngoài lớp | proper learning, improper learning | 5-12 (ghi chú diễn giả) |
| cận tổng quát hóa cho mọi thuật toán ERM | (không có tên tiếng Anh trong ghi chú) | 6-01 |
| định lý không có bữa trưa miễn phí | no-free-lunch theorem | 6-02 (ghi chú diễn giả) |
| lọc thư rác | spam filtering | 7-03 |

## 11. Rủi ro và điểm cần điều phối viên quyết định

Các điểm dưới đây giữ nội dung lúc lập storyboard (mã trang đã đổi theo deck cuối). Quyết định của điều phối viên ở `review-log.md`, mục "Bộ trang chiếu (2026-11-15)"; cách deck cuối áp dụng ở mục 14.

1. **Hộp "Vấn đề trung tâm" (1-05) là một câu hỏi** có nhãn "Câu hỏi:", lấy từ đoạn mở đầu của ghi chú ("học có nghĩa là gì"). Phương án khác, dạng trần thuật: "Xác định khi nào một hàm dự đoán chọn từ tập huấn luyện được xem là đã học được." Cách chọn ở đây sẽ thành khuôn cho deck 02–10.
2. **Số trang 55, vượt mức tham khảo 35–50.** Phương án rút còn 51, không bỏ bước nào của hành trình khái niệm: (a) gộp trang kỹ thuật tính tuyến tính (cũ 3·04) thành dòng "Kỹ thuật." trên 3-03; (b) gộp hai trang Bài tập 01.5(d) (cũ 5-06, 5·07) thành một trang chỉ với câu (4) của Bài tập 01.5(d); (c) gộp 6-01 vào 6-02; (d) gộp 5-04 vào 5-05. Mỗi phương án bớt khoảng 1–1,5 phút; thời gian dư chuyển cho mạch 5.
3. **Ví dụ mới duy nhất: V4 (3-05), một quan sát dưới $D_f$.** Dùng kí hiệu ghi chú; $0{,}36$ khớp công thức $0{,}2(0{,}8^m+0{,}6^m+0{,}4^m)$ của ghi chú tại $m=1$; không mâu thuẫn con số nào của ghi chú. Cần ghi cách dựng vào `review-log.md` khi duyệt. Câu trả lời 7-04 câu 4 ($14\le m_{A_{\max}}\le30$) là suy luận một dòng từ Ví dụ 01.9 và Mệnh đề 01.31, không có câu tương ứng trong ghi chú (xem mục 13, điểm 2).
4. **Tiếng Anh trong ngoặc:** không đặt trên trang bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm" (trang tổng quan, giống ngoại lệ của tiêu đề và danh sách mục tiêu trong quy tắc "define before use" của ghi chú); lần đầu trên trang nội dung có tiếng Anh. Tiêu đề bài trên bìa chứa "PAC" trước khi 1-02 giải nghĩa chữ viết tắt (tiêu đề giữ đúng tên bài của ghi chú).
5. **Chính sách trang "Kỹ thuật." (khuôn cho deck 02–10):** kỹ thuật dùng lại qua học phần có trang riêng tại nơi dùng lần đầu (Bài 01: tính tuyến tính của kì vọng 3-03, bất đẳng thức hợp 4-04, chặn xác suất bỏ sót 6-07); kỹ thuật chỉ dùng trong một chứng minh là một dòng "Kỹ thuật." trên trang ý tưởng chứng minh (tối thiểu hóa từng điểm, 5-09). Deck sau nhắc lại theo tên, một dòng.
6. **Mạch 5 dài** (14 trang, 33 phút) vì §6 và §7 của ghi chú là hai mục liên tiếp có cùng chủ đề; tách thành hai mạch sẽ cho tám mạch.
7. **6-02: phát biểu và ý tưởng chứng minh của Hệ quả 01.29 chung một trang**, trong khi quy định ghi "Ý tưởng chứng minh … own slide". Lý do: chứng minh hai bước, mỗi bước một dòng, dựa trên Mệnh đề 01.15 vừa chứng minh. Nếu điều phối viên đòi trang riêng: tách thành 6-02 (phát biểu) và 6-03 (ý tưởng chứng minh), thêm 1 trang, lấy 1 phút từ 6-01.
8. **Trang bài tập chỉ lấy từ `exercises.md`:** 3-07 (Bài tập 01.2(a)), 4-05 (Bài tập 01.4(a)), 5-06 (Bài tập 01.5(d), câu 4, giữ nguyên chữ; sau khi gộp). Ví dụ của ghi chú có "Câu hỏi:" và lời giải `[f]` là trang "Ví dụ:" (2-04, 5-10), không phải "Bài tập:". Mạch 2 và mạch 6 không có trang "Bài tập:"; kiểm tra của hai mạch là "Câu hỏi:" ở 2-04, 6-01 và Ví dụ 01.11 ở 6-04.
9. **Hình F4 dùng năm vị trí điểm minh họa** ($0{,}12;\ldots;0{,}90$) không có trong ghi chú (ghi chú cho $m$ tùy ý); hình ghi rõ "một tập huấn luyện minh họa". Không có kết luận nào phụ thuộc vị trí các điểm.
10. **Mệnh đề 01.23 ở mức đọc thêm trong ghi chú nhưng có trang ý tưởng chứng minh (5-09):** blueprint xếp nó là một trong bốn kết quả chính, và bài toán sàng lọc với chi phí bất đối xứng cần phần (b).
11. **Dòng "Diễn giải:" của 3-07 dẫn số của Bài tập 01.2(b)** ($0{,}29$, $0{,}45$, $0{,}25$) mà bảng phân bố $D$ không có trên mặt trang. Phương án khác: bỏ dòng này khỏi mặt trang, để ở ghi chú diễn giả.
12. **Công thức cần đo ở 390 px:** 2-03 ($\ell_c$), 2-04, 3-03, 5-03 (dòng lượng từ), 5-11 (phân rã), 5-12, 6-01, 6-06. Ngắt bằng `aligned` chỉ khi tràn (quy tắc của tác giả).
13. **Liên kết sang Bài 02** ở 7-06 là dòng chữ không có liên kết cho đến khi deck Bài 02 có tên tệp.
14. **Mục tiêu (1-03) rút gọn** từ năm mục tiêu của ghi chú để vừa trần 80 âm tiết; không thêm năng lực nào ngoài ghi chú. Mục tiêu 4 của ghi chú có thêm "độ phức tạp mẫu của một thuật toán với độ phức tạp mẫu của một lớp", trên trang viết bằng kí hiệu $m_A$, $m_{\mathcal H}$.

## 12. Bảng đối chiếu trang → mục và khối của ghi chú

Bảng theo deck cuối (55 trang, 2026-11-15). Cột "Mặt trang" ghi các mục và khối mà mặt trang dùng; cột "Ghi chú diễn giả" ghi các khối chỉ được dẫn trong ghi chú diễn giả.

| Trang | Mục ghi chú (mặt trang) | Khối (mặt trang) | Ghi chú diễn giả dẫn thêm |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §7 đoạn cuối | — | — |
| 1-02 | Kiến thức tiên quyết; §2 | (T1), (T2) | câu ôn nhanh 1–3; Định nghĩa 01.4 (điều kiện đo được) |
| 1-03 | Mục tiêu học tập | — | §10 |
| 1-04 | toàn bài | — | §12 |
| 1-05 | đoạn mở đầu | — | §7, §8, §9 (câu trả lời theo phần) |
| 1-06 | Câu hỏi mở đầu | — | — |
| 2-00 | §1, §3, §4 | — | — |
| 2-01 | §1 | danh sách thành phần | bảng nguồn ngẫu nhiên §1; Định nghĩa 01.4 |
| 2-02 | §3 | Ví dụ 01.1 | — |
| 2-03 | §3 (ứng dụng sàng lọc), §4 | Định nghĩa 01.1 | Ví dụ 01.3, Nhận xét 01.2, Định nghĩa 01.3 |
| 2-04 | §4 | Ví dụ 01.2 | Phụ lục C.1 |
| 2-05 | §4 | Định nghĩa 01.5, Ví dụ 01.4 | — |
| 3-00 | §5 | — | — |
| 3-01 | §5 | Định nghĩa 01.6, Ví dụ 01.5 | — |
| 3-02 | §5 | Mệnh đề 01.7 | — |
| 3-03 | §5; Kiến thức tiên quyết | chứng minh Mệnh đề 01.7 (gộp dòng kỹ thuật) | Phụ lục C.2 (§6); Bài tập 01.3(a) |
| 3-04 | §5 | Định nghĩa 01.8, Ví dụ 01.6 | Nhận xét 01.11, Ví dụ 01.7, Định nghĩa 01.12; §2 (O1), (O2) |
| 3-05 | §5 | Nhận xét 01.9; ví dụ $m=1$ (cách dựng ở `review-log.md`) | Ví dụ 01.9, Phụ lục C.2 (§6); Bài tập 01.3 |
| 3-06 | §5 | Định nghĩa 01.10 và đoạn sau, Nhận xét 01.9 | — |
| 3-07 | §5; tệp bài tập | Thuật toán 01.13; Bài tập 01.2(a) | Bài tập 01.2(b) |
| 4-00 | §5 | — | — |
| 4-01 | §5 | Định nghĩa 01.14, Ví dụ 01.8 | — |
| 4-02 | §5 | Mệnh đề 01.15 | — |
| 4-03 | §5 | chứng minh Mệnh đề 01.15 | Ví dụ 01.11 (§8); Phụ lục A(iii) |
| 4-04 | §5 | chứng minh Mệnh đề 01.15 (Bước 3) | §11; Bài tập 01.4(b) |
| 4-05 | tệp bài tập | Bài tập 01.4(a) | — |
| 4-06 | §5 (các đoạn sau chứng minh Mệnh đề 01.15) | — | — |
| 5-00 | §6, §7 | — | — |
| 5-01 | §6 (đoạn đầu) | — | — |
| 5-02 | §6 | Định nghĩa 01.16, 01.18 | Nhận xét 01.17 |
| 5-03 | §6 | đoạn thứ tự lượng từ sau Định nghĩa 01.18 | Bài tập 01.5(a)(b) |
| 5-04 | §6 | Định nghĩa 01.20, Nhận xét 01.21 | Bài tập 01.7 |
| 5-05 | §6 | Ví dụ 01.9 | Phụ lục C.2 |
| 5-06 | tệp bài tập; §6 | Bài tập 01.5(d) câu 4 và lời giải; Nhận xét 01.19 | Bài tập 01.5(d) câu 2, 01.5(e) |
| 5-07 | §7 (đoạn đầu) | Định nghĩa 01.22, Nhận xét 01.17, Ví dụ 01.10 (phần hàm lỗi 0–1) | — |
| 5-08 | §7 | Mệnh đề 01.23 | Phụ lục B |
| 5-09 | §7; Phụ lục B | đoạn ý tưởng sau Mệnh đề 01.23; chứng minh Mệnh đề 01.23 | — |
| 5-10 | §7 | Ví dụ 01.10 (phần $\ell_c$), Mệnh đề 01.23(b) | §3 (câu hỏi thực hành); Bài tập 01.1(d), 01.2(c) |
| 5-11 | §7 | Định nghĩa 01.24 và đoạn sau | — |
| 5-12 | §7 | Định nghĩa 01.25 và đoạn sau | Định nghĩa 01.3, Nhận xét 01.26, 01.27, đoạn cuối §7; Bài tập 01.10 |
| 6-00 | §8, §9 | — | — |
| 6-01 | §8 | Định nghĩa 01.28 và câu hỏi sau | — |
| 6-02 | §8 | Hệ quả 01.29 | Nhận xét 01.26, 01.30 |
| 6-03 | §8 | chứng minh Hệ quả 01.29 | Phụ lục A(iii) |
| 6-04 | §8 | Ví dụ 01.11 | Nhận xét 01.21 (phân bố $D_1$) |
| 6-05 | §9 | Mệnh đề 01.31 và đoạn sau | Bài tập 01.9(c) |
| 6-06 | §9 | chứng minh Mệnh đề 01.31 (phác thảo) | Ví dụ 01.9 |
| 6-07 | §9; Kiến thức tiên quyết | chứng minh Mệnh đề 01.31 (bước cuối) | Ví dụ 01.9 |
| 7-00 | §9–§12 | — | — |
| 7-01 | §5–§9 | Mệnh đề 01.7, 01.15, 01.23, Hệ quả 01.29, Mệnh đề 01.31 | Nhận xét 01.9, Ví dụ 01.10, 01.11; §9 |
| 7-02 | §7 (đoạn cuối), §11 | — | — |
| 7-03 | tệp bài tập | Bài tập 01.1(d); Mệnh đề 01.23 | Phụ lục B (đoạn "Rủi ro Bayes") |
| 7-04 | §11; §6 | Ví dụ 01.6, 01.9, Nhận xét 01.19, Mệnh đề 01.31 (trong lời giải ở ghi chú diễn giả) | — |
| 7-05 | §10; tệp bài tập | Bài tập 01.1–01.11 | — |
| 7-06 | §11, §12 | — | — |

Kiểm tra thứ tự: đọc cột "Mục ghi chú (mặt trang)" từ trên xuống, các mục không giảm (Kiến thức tiên quyết và tệp bài tập là nguồn phụ). Ghi chú diễn giả dẫn về phía sau ở 1-05, 2-03 (câu hỏi thực hành), 3-03 và 3-05 (Phụ lục C.2, Ví dụ 01.9), 4-03 (Ví dụ 01.11), 5-03 và 5-04 (bài tập về nhà) để nối sang phần sau; mặt trang không dẫn kết quả của trang sau. Trang 7-04 dùng §6 cho câu 4 (thứ tự lượng từ), là trang tổng kết nhìn lại.

## 13. Đề xuất sửa ghi chú và tệp bài tập (không sửa; chờ điều phối viên và tác giả)

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất |
|---|---|---|---|---|
| nhẹ | `exercises.md` dòng 73, Bài tập 01.2 | Câu nguồn gốc số liệu "(giá trị dựng để luyện tập)", thuộc loại câu rào đón về nguồn gốc mà `../CLAUDE.md` § The author's voice yêu cầu bỏ ("… là số liệu sư phạm tự xây dựng"; nguồn gốc ghi ở `review-log.md`) | "Cho $\mathcal X=\{1,\ldots,6\}$, $\mathcal Y=\{0,1\}$ và phân bố $D$ cho bởi bảng sau (giá trị dựng để luyện tập):" | Bỏ cụm trong ngoặc. Deck không chép cụm này. |
| nhẹ | ghi chú Ví dụ 01.9, đoạn "Cỡ mẫu cho riêng $D_f$" | Khoảng trống nhỏ: ghi chú nói $14$ chỉ đủ riêng cho $D_f$ nhưng không nêu quan hệ của $14$ với $m_{A_{\max}}(0{,}1;\ 0{,}05)$; từ Ví dụ 01.9 và Mệnh đề 01.31 suy ra ngay $14\le m_{A_{\max}}(0{,}1;\ 0{,}05)\le30$ | "Cỡ mẫu $m_0$ trong Định nghĩa 01.20 phải đúng cho mọi phân bố khả diễn, còn các con số này thay đổi khi khối lượng xác suất của điểm $x=3$ thay đổi." và "Cỡ $14$ của Ví dụ 01.9 chỉ đủ riêng cho $D_f$." (sau Mệnh đề 01.31) | Không bắt buộc. Nếu tác giả muốn, thêm một câu sau Mệnh đề 01.31: "Do đó $14\le m_{A_{\max}}(0{,}1;\ 0{,}05)\le30$." Deck chỉ dùng kết luận này ở ghi chú diễn giả câu hỏi tự kiểm tra 4. |

Không thấy lỗi toán học trong ghi chú ở các khối deck dùng; mọi con số của ví dụ đã tính lại (mục 5).

## 14. Bản deck cuối và các chỗ lệch storyboard (2026-11-15)

Tệp: `2627-1/lecture-01-mo-hinh-hoc.html`, 55 trang, mã `L01-k-mm`. Hình: chín SVG trong `2627-1/img/lec-01/` (F1–F7 như mục 8). Mỗi trang ở mục 6 có dòng "Bản deck cuối (2026-11-15)" khi mặt trang lệch bản dự kiến; mục này gom các chỗ lệch theo loại.

**Ánh xạ mã trang** (storyboard lúc lập → deck cuối): 3-04 gộp vào 3-03; 3-05→3-04, 3-06→3-05, 3-07→3-06, 3-08→3-07; 5-07 gộp vào 5-06; 5-08→5-07, 5-09→5-08, 5-10→5-09, 5-11→5-10, 5-12→5-11, 5-13→5-12; 6-02 tách thành 6-02 (phát biểu) và 6-03 (ý tưởng chứng minh); 6-03→6-04, 6-04→6-05, 6-05→6-06, 6-06→6-07; thêm 7-03 (bài tập tổng hợp); 7-03→7-04, 7-04→7-05, 7-05→7-06. Mọi mã trong tệp này đã đổi theo deck cuối.

**Áp dụng quyết định của điều phối viên** (`review-log.md`, mục "Bộ trang chiếu (2026-11-15)"):

| Quyết định | Deck cuối |
|---|---|
| Gộp (a): kỹ thuật tính tuyến tính thành dòng "Kỹ thuật." | 3-03 (dòng "Kỹ thuật." và công thức hiển thị); bỏ tổng đuôi vô hạn |
| Gộp (b): Bài tập 01.5(d) một trang, chỉ câu 4 | 5-06 |
| Tách Hệ quả 01.29 | 6-02 (Giả thiết, Bảo đảm, Ý nghĩa), 6-03 (bốn bước) |
| Bài tập tổng hợp ở mạch 7 | 7-03, Bài tập 01.1(d) (lý do chọn ở mục 6, trang 7-03) |
| Câu hỏi tự kiểm tra 4 viết lại | 7-04: "Cỡ $14$ của Ví dụ 01.9 và cỡ $30$ của Mệnh đề 01.31 ứng với thứ tự lượng từ nào?" |
| Mục tiêu bằng lời | 1-03 |
| "Diễn giải:" của bài tập ERM chuyển sang ghi chú diễn giả | 3-07 |
| Đáy trục log $0{,}001$ | F5a (5-05), F5b (6-07) |
| Chú thích F4 nêu dữ liệu | F4 ghi "m = 5, nhãn 1: x = 0,12; 0,31; 0,47; 0,68; 0,90" trong hình |
| Ghi chú diễn giả không có mã nội bộ, câu quy trình, câu nguồn gốc | đã kiểm bằng tìm chuỗi ("mạch N", "V4", "mục 5", "storyboard", "dựng mới", "Trang này") và đọc lại; nguồn gốc ví dụ $m=1$ chỉ ở `review-log.md` |
| 14 phát hiện nhẹ của cổng duyệt | 2-01, 2-03, 3-01, 3-05, 3-06, 4-03, 4-06, 5-02/5-03, 5-08 áp dụng như dòng "Bản deck cuối" của từng trang; ghi chú diễn giả viết dạng khẳng định ở 2-04, 3-02, 3-06, 4-02, 6-02, 6-04, 6-05; mục 12 viết lại đủ khối và câu kiểm tra thứ tự; bài tập tổng hợp ở 7-03 |

**Lệch khác so với storyboard, kèm lý do.**
- Nhãn "Bảo đảm:" thay "Kết luận" ở mọi trang phát biểu kết quả (3-02, 4-02, 5-08, 6-02, 6-05): quy định 2026-11-15.
- Nhãn (T1), (T2) nêu trên mặt trang 1-02 vì 3-02, 6-02, 6-05, 7-01 dùng chúng trên mặt trang; (O1), (O2) chỉ ở ghi chú diễn giả, mặt trang viết "thuật toán ERM".
- 1-04 bỏ dòng "Đọc trước:" (nhãn không hợp lệ). 6-03 không có dòng "Kỹ thuật." trên mặt trang (giữ trần; ý bác bỏ "với mọi" bằng một cặp phản ví dụ ở ghi chú diễn giả). Các trang ý tưởng chứng minh ghi giả thiết trong bước, không dùng nhãn "Giả thiết vào:" (không hợp lệ).
- Bố cục: 1-06, 3-01, 4-01, 5-05, 5-07, 5-10, 5-11, 6-06, 6-07 dùng `grid2` hoặc hình dưới chữ để không tràn khung và giữ chữ trong hình từ 16 px; F5b chuyển từ 6-05 sang 6-07. Hình F3, F5a, F2a, F2b vẽ thấp hơn bản đặc tả để chữ trong hình đạt 17–19 px ở kích thước hiển thị (đo trên trình duyệt: F1 19,0; F3 17,3; F4 19,0; F5a 17,1; F2a 18,9; F2b 17,1; F6 16,5; F7 17,9; F5b 17,7 px).
- 3-01 đổi tiêu đề thành "Ví dụ: rủi ro thực nghiệm trên $S_\eta$"; 3-04 bỏ tiền tố "Ví dụ:" (trang mở bằng định nghĩa ERM).

**Ngoại lệ mật độ** (số âm tiết do `deck_check.py` đếm):
- 1-01 (bìa): câu luận điểm 39 âm tiết trong một khối, vượt "≤ 20 âm tiết/dòng"; đây là luận điểm một câu theo quy định trang bìa, tổng trang 60.
- 1-05: hộp "Câu hỏi:" 25 âm tiết trong một khối; câu hỏi trung tâm lấy nguyên ý đoạn mở đầu của ghi chú, trang chỉ có một hộp.
- 7-01: 65 âm tiết, dưới trần 80 của bảng tổng kết (công cụ báo vì trần mặc định 60).
- 7-03: 73 âm tiết, trên trần 60, dưới 1,5 lần trần. Lý do: bài tập tổng hợp phải có "Lời giải:" trên mặt trang và deck đã ở trần 55 trang, nên không tách được đề và lời giải. Bản trước khi rút là 81 âm tiết; đã chuyển "mô hình phù hợp là học PAC bất khả diễn" và mô tả véc-tơ từ sang ghi chú diễn giả.

**Kiểm tra máy** (`deck_check.py`, `--shots`, 1600×900 và 390×844): slides=55, console=0, pageerrors=0, failed=0, `.katex-error`=0, không trang tràn khung, không trang tràn ngang ở 390 px, không trang quá 6 dòng hay 3 công thức hiển thị; liên kết `#/2`…`#/7` của trang "Nội dung" mở đúng 2-00…7-00; phím →, ↓, Space, Esc hoạt động. Người viết đã xem ảnh chụp mọi trang ở hai cỡ.

**UML:** không đọc thêm trang UML khi viết deck; các mục UML trên deck (§§2.1–2.3, §§3.1–3.2, §5.1) lấy từ §12 của ghi chú.

## 15. Sửa sau năm báo cáo duyệt (2026-11-15)

Người sửa: tác tử viết deck, theo quyết định ở `review-log.md`, mục "Năm báo cáo duyệt và quyết định của điều phối viên". Số trang giữ 55, không thêm, không bớt trang; mã trang không đổi. Mỗi phát hiện ghi theo thứ tự trong báo cáo; mã phát hiện: HV (`deck-hoc-vien.md`, 23), TH (`deck-toan-hoc.md`, 14, theo số của báo cáo), CG (`deck-chuyen-gia.md`, 18, theo số của báo cáo), SP (`deck-su-pham.md`, 42, theo thứ tự dòng), MT (`deck-mach-truyen.md`, 13, theo thứ tự dòng).

**Thay đổi chung.**
- Chế độ màn hẹp: `.slides` bọc trong `div.lecture-viewport`, chép khối script "Màn hẹp (≤ 760 px)" của `lecture-template.html`. Ở 390×844, trang không cuộn ngang (`documentElement.scrollWidth` = 390 ở mọi trang); công thức hiển thị và bảng rộng cuộn ngang tại chỗ. Công thức trong dòng không còn nhóm `{…}` (nhóm làm công thức không xuống dòng và bị cắt ở màn hẹp); các bộ dữ liệu $S_\eta$, $S_f$, $S$ viết thành từng cặp $(x,y)$ riêng. Ba công thức hiển thị nằm trong danh sách đánh số (4-03, 5-09, 6-03) được đưa ra ngoài `ol` (danh sách tiếp tục bằng `ol start`).
- Dòng dẫn sáu trang tiêu đề mạch viết lại thành câu trần thuật về ý cốt lõi, không mở bằng "Người học" (mục 3); ghi chú diễn giả các trang này bỏ nhãn "Kế thừa:/Nhiệm vụ:/Kết quả trao đi:".
- Nhãn "Kí hiệu:"; "kí hiệu", "lôgarit" trong ghi chú diễn giả, alt và `<desc>` của SVG.
- "Tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM)" chuyển xuống 3-04, "Học xấp xỉ với xác suất cao (probably approximately correct, PAC)" chuyển xuống 5-02 (nơi dùng lần đầu trên trang nội dung), để 1-02 dưới trần 60 sau khi thêm (T2) đầy đủ, tên đầy đủ của i.i.d. và tên của $\mathcal X$, $\mathcal Y$, $D$.
- Mật độ đếm lại với số trong câu có tính (quy ước của điều phối viên). Mọi trang ≤ 60 âm tiết, trừ: 1-01 (bìa, 63, gồm hai dòng đơn vị bắt buộc; câu luận điểm 39 âm tiết trong một khối) và 7-03 (65, bài tập tổng hợp có lời giải trên mặt trang; bản trước 73). 1-03 (80) và 7-01 (69) dưới trần 80. Trung bình 48 âm tiết/trang; mục tiêu ≤ 40 không đạt được ở các trang phát biểu kết quả mà không bỏ giả thiết, nên chưa đạt ở 34 trang.
- SVG: F6 (`rui-ro-vuot-muc.svg`) và F7 (`vung-loi.svg`) vẽ thấp hơn để trang không tràn khung; số liệu không đổi.

| Phát hiện | Trang | Kết quả |
|---|---|---|
| HV1 (TB) | 2-02 | đã sửa: "$D_\eta$: nhãn $1$ với xác suất $\eta(x)$", "$D_f$: $y=f(x)$ với hàm gán nhãn …" |
| HV2 (TB) | 2-04 | đã sửa: công thức hiển thị là $L^c_{D_\eta}(h_t)$ với $c_{FN}$, $c_{FP}$; $L_{D_\eta}$ là trường hợp $c_{FN}=c_{FP}=1$ |
| HV3 (TB) | 5-11 | đã sửa: hai rủi ro vượt mức viết tường minh, rồi đẳng thức |
| HV4 (TB) | 6-01 | đã sửa: "Với $\ell_{0\text{-}1}$, $\mathcal Y=\{0,1\}$, $\beta(m,\delta)$ là cận … nếu với mọi thuật toán ERM …" |
| HV5 (TB) | toàn deck | đã sửa: chế độ màn hẹp (thay đổi chung) |
| HV6 | 1-02 | đã sửa: "$\mathcal X$ tập đầu vào, $\mathcal Y$ tập nhãn, $D$ phân bố dữ liệu" |
| HV7 | 1-06 | đã sửa: "với hàm chỉ báo (indicator) $\mathbb 1[\cdot]$" |
| HV8 | 3-04 | đã sửa: "Khi tập nghiệm ERM … $\ne\emptyset$ với mọi $S$, thuật toán ERM trả về …" |
| HV9 | 3-05 | đã sửa: ghi chú diễn giả nêu quy tắc $\hat t=X_1$ hoặc $6$ |
| HV10 | 3-07 | đã sửa: "Thuật toán 01.13 tính số lỗi $E(t)$ của $h_t$" |
| HV11 | 4-01 | đã sửa: "σ-đại số (σ-algebra)"; "$A_{\mathrm{gn}}(S)=\mathbb 1_F$ …; $h_{\equiv1}$ cũng khớp" |
| HV12 | 4-03 | đã sửa: "Với $s$ cố định"; ghi chú diễn giả phân biệt $s$ và $S$, $F$ |
| HV13 | 4-03/4-04, 6-06/6-07 | không sửa, đề xuất bác bỏ: thứ tự "ý tưởng chứng minh → kỹ thuật" là thứ tự của quy định "Concept journey"; mạch truyện (MT10) chấp nhận khi nhất quán; công thức hiển thị ở bước 3 của 4-03 là dạng riêng của bất đẳng thức hợp, chuỗi bất đẳng thức ở 6-06 tự đủ. Bản thử thêm công thức chung vào bước 3 làm trang tràn khung |
| HV14 | 5-01 | đã sửa: "…; sai ở đó chỉ tốn $0{,}001$"; ghi chú diễn giả nối với $\epsilon$ |
| HV15 | 5-04 | đã sửa: hai câu trọn ý ("… nhỏ nhất đủ cho mọi $D$ khả diễn." / "Đủ nghĩa là …") |
| HV16 | 5-07 | đã sửa: "Chọn như vậy tại mỗi mức cho $\mathbb 1[x\in\{3,5\}]$" |
| HV17 | 5-10 | đã sửa: câu hỏi và dòng đáp nói "ngưỡng … của $\eta(x)$"; ghi chú diễn giả phân biệt với ngưỡng $t$ |
| HV18 | 6-01 | đã sửa: bỏ nhãn "Trực quan." ở câu đáp |
| HV19 | 6-05 | đã sửa: Trực quan nói bằng lời, không dùng $t^\star$, $K$; "khối lượng xác suất (probability mass)" |
| HV20 | 6-06 | đã sửa: bước 3 ghi chặn trung gian $\le D_{\mathcal X}(\{t^\star,\ldots,k-1\})\le\epsilon$; lý do "$C$ ngắn nhất, nên $G(k)\le\epsilon$" ở ghi chú diễn giả (thêm vào mặt trang làm tràn khung) |
| HV21 | 6-07 | đã sửa: điều kiện cỡ mẫu nằm trong công thức hiển thị |
| HV22 | 7-01 | đã sửa: các ô rút gọn, bảng thấp hơn |
| HV23 | 7-03 | đã sửa: "$x$ là tập từ"; "Lọc thư rác (spam filtering)" ở ghi chú diễn giả, mặt trang "Thư rác (spam)" |
| TH1 (NT) | 7-02, 1-05 | đã sửa: "Với mọi phân bố khả diễn trên lớp hàm ngưỡng, $A_{\max}$ là thuật toán học PAC với $M(\epsilon,\delta)=\lceil\ln(1/\delta)/\epsilon\rceil$"; ghi chú diễn giả 1-05, 1-04 thêm "khả diễn" và "$A_{\max}$" |
| TH2 (TB) | 6-03 | đã sửa: bước 1 nêu cả hai giả thiết ($L_S=0$ do lớp, $L_D=1$ do không có nguyên tử), bước 4 "(cả hai giả thiết)"; ghi chú diễn giả viết "Mệnh đề 01.15(a)/(b)/(c)" |
| TH3 (TB) | 3-02 | đã sửa: "$\mathbb E_{S\sim D_\eta^6}[L_S(h_3)]=0{,}22$" |
| TH4 (TB) | 1-05 | đã sửa: "khi …; với $h=A(S)$ thì nói chung không" |
| TH5 (TB) | 4-03, 7-01 | đã sửa: ghi chú diễn giả viết $\mathbb E_S[L_{D_1}(A_{\mathrm{gn}}(S))]=0{,}8^m$ |
| TH6 (TB) | 4-01, 5-07 | đã sửa: $\mathcal M_{\mathcal X}$ định nghĩa cho $\mathcal X$ tổng quát ("ở đây $\mathcal X=[0,1]$"); "Rủi ro Bayes … dưới $\ell_{0\text{-}1}$" |
| TH7 | 7-02 | đã sửa: "Trên $\mathcal M_{\mathcal X}$, $X\sim U[0,1]$, …" |
| TH8 | 1-02 | đã sửa: (T2) có vế "$\ell$ không bị chặn thì cần rủi ro kì vọng hữu hạn" ($L_D$ chưa định nghĩa ở 1-02, nên viết bằng lời; ghi chú diễn giả ghi $L_D(h)<\infty$) |
| TH9 | 6-02 | đã sửa: "thuật toán ERM chính xác"; (b) "dưới $D$ khả diễn"; nhãn (O1) ở ghi chú diễn giả 3-04, 6-02 (quyết định về (O1)/(O2)) |
| TH10 | 5-11 | đã sửa: "so với rủi ro Bayes (phân lớp)"; điều kiện $L_D(h)<\infty$ ở ghi chú diễn giả |
| TH11 | 7-03 | đã sửa: lời giải "chặn là báo $h(x)=1$, nên chặn nhầm là dương tính giả" |
| TH12 | 3-06 | đã sửa: ghi chú diễn giả trích nội dung, bỏ "dòng thứ tư" |
| TH13 | 2-02 | đã sửa (cùng HV1) |
| TH14 | 7-05 | đã sửa (cùng MT5) |
| CG1 (NT) | 7-02, 1-05 | đã sửa (cùng TH1) |
| CG2 (TB) | 6-03 | đã sửa (cùng TH2) |
| CG3 (TB) | 6-06 | đã sửa: dòng "Bỏ khả diễn: bước 1 hỏng; dưới $D_\eta$, $L_D(h_t)\ge0{,}22$ với mọi $t$"; hệ quả "biến cố rỗng khi $\epsilon<0{,}22$" ở ghi chú diễn giả. Phần tùy chọn (bỏ độc lập, $Z_1=\cdots=Z_m$) không thêm vì là ví dụ mới cần ghi cách dựng vào `review-log.md` |
| CG4 (TB) | 6-02 | đã sửa: "Ý nghĩa: (b) nói về $A_{\mathrm{gn}}$, không về lớp; bảo đảm học cần cấu trúc của lớp hoặc thuật toán"; câu về định lý không có bữa trưa miễn phí ở ghi chú diễn giả |
| CG5 (TB) | 5-03 | đã sửa: gạch đầu dòng "$D$ chạy trên các phân bố mà $(D,\mathcal H)$ khả diễn" |
| CG6 (TB) | 1-05 | đã sửa (cùng TH4) |
| CG7 (TB) | 2-01 | đã sửa: "…; $S$, $A(S)$ và rủi ro của $A(S)$ ngẫu nhiên" (bằng lời vì $L_D$ định nghĩa ở 2-03); ghi chú diễn giả nêu $L_D(A(S))$ là biến ngẫu nhiên |
| CG8 (TB) | 3-04, 6-02 | đã sửa theo quyết định: ERM xấp xỉ, sai số tối ưu $\epsilon_{\mathrm{opt}}$, (O1)/(O2) ở ghi chú diễn giả 3-04 (mặt trang 3-04 ở 57 âm tiết, thêm một dòng sẽ vượt trần); 6-02 "thuật toán ERM chính xác" |
| CG9 | 1-02 | đã sửa (cùng TH8) |
| CG10 | 5-01 | đã sửa: "hỏng với xác suất $\le\delta$" |
| CG11 | 5-06 | đã sửa: "trong $100$ lần huấn luyện với tập mới, ít nhất khoảng $95$ lần …"; ghi chú diễn giả nêu $0{,}956$ tại $m=14$ |
| CG12 | 5-11 | đã sửa: "$0{,}04$ do $(D,\mathcal H)$, không do $h$; không giảm khi $m$ tăng" |
| CG13 | 6-00 | đã sửa: "một cách đủ để có bảo đảm cho mọi nghiệm ERM là chặn sup" |
| CG14 | 6-05 | đã sửa: ghi chú diễn giả "lớp hàm ngưỡng học được PAC, $m_{\mathcal H}\le\lceil\ln(1/\delta)/\epsilon\rceil$" |
| CG15 | 4-01, 5-07 | đã sửa (cùng TH6) |
| CG16 | 3-02 | đã sửa: "mỗi $\ell(h,Z_i)$ có cùng phân bố với lỗi của $h$ trên một quan sát mới" |
| CG17 | 7-01 | đã sửa: loại bảo đảm sau số hiệu (kì vọng, tất định, tổng thể, xác suất cao); hàng 01.23 "hàm lỗi; so trên mọi $g\in\mathcal M_{\mathcal X}$" |
| CG18 | 5-09 | đã sửa: ghi chú diễn giả nêu thu hẹp tập so sánh về lớp hàm ngưỡng ($0{,}18$ lên $0{,}22$) |
| SP1 (TB) | 1-05 | đã sửa (cùng TH4) |
| SP2 (TB) | 2-02 | đã sửa: bỏ câu "Ví dụ đủ nhỏ để tính tay …" |
| SP3 (TB) | 2-00…7-00 | đã sửa: ghi chú diễn giả viết thành câu thường, không nhãn |
| SP4 (TB) | 4-02 | đã sửa: "Ý nghĩa: $A_{\mathrm{gn}}$ quá khớp (overfitting) ở mức cực đoan" |
| SP5 (TB) | 5-07 | đã sửa (cùng HV16) |
| SP6 (TB) | 4-01, 4-03, 4-06, 6-04, 7-01, 6-01 | đã sửa: "hàm phân lớp ghi nhớ", "phản ví dụ hàm phân lớp ghi nhớ" |
| SP7 | ghi chú 1-01, 1-04, 2-01, 2-03, 5-09, 5-11, 6-01 | đã sửa: nêu thẳng nội dung; bỏ câu ở 5-09 |
| SP8 | 1-02 | đã sửa: "cận dưới đúng (infimum) $\inf$; phân bố đều $U[0,1]$" |
| SP9 | 1-02 | đã sửa: "độc lập cùng phân bố (independent and identically distributed, i.i.d.)"; ERM và PAC viết đúng dạng ở 3-04 và 5-02 |
| SP10 | ghi chú 1-03, 7-05 | đã sửa |
| SP11 | 1-05 | đã sửa: hộp "Câu hỏi: học có nghĩa là gì?" (câu in đậm của ghi chú); ghi chú diễn giả mở bằng nội dung cụ thể hóa câu hỏi |
| SP12 | ghi chú 1-04, 1-05 | đã sửa: bảo đảm cho $A_{\max}$, khả diễn |
| SP13 | 1-06 | đã sửa (cùng HV7) |
| SP14 | dòng dẫn mạch | đã sửa theo quyết định (thay đổi chung) |
| SP15 | 3-00 | đã sửa: dòng dẫn mới không có "nó" |
| SP16 | ghi chú 2-03 | đã sửa: bỏ câu hồi quy và cận bình phương |
| SP17 | ghi chú 2-04 | đã sửa: "Hàm tốt nhất trong lớp đổi theo hàm lỗi, nên hàm lỗi là một thành phần của bài toán" |
| SP18 | ghi chú 2-05 | đã sửa: bỏ câu "Tóm lại"; "Ba câu hỏi này …" |
| SP19 | ghi chú 3-02 | đã sửa: "trên $S_\eta$, độ lệch là $\tfrac13-0{,}22$" |
| SP20 | 3-03 | đã sửa: "Trường hợp cực biên …"; câu về $N$ chuyển sang ghi chú 3-05 |
| SP21 | 3-04 | đã sửa phần "Diễn giải:" (nêu bốn con số); (O1)/(O2) giữ ở ghi chú diễn giả theo quyết định về CG8 |
| SP22 | ghi chú 3-06 | đã sửa |
| SP23 | ghi chú 3-07 | đã sửa: "$K=\lvert\mathcal X\rvert=6$" |
| SP24 | ghi chú 4-01 | đã sửa: bỏ câu về σ-đại số chứa tập một điểm |
| SP25 | ghi chú 4-02 | đã sửa: bỏ câu nhắc lại "tất định" |
| SP26 | 4-06 | đã sửa: "Chọn lớp giả thuyết trước khi có tập huấn luyện là một thiên kiến quy nạp (inductive bias)." |
| SP27 | ghi chú 5-01 | đã sửa |
| SP28 | 5-06 | đã sửa: tiêu đề "Bài tập: cách đọc một bảo đảm học PAC"; ghi chú bỏ "điều này" |
| SP29 | 5-11 | đã sửa (cùng HV3) |
| SP30 | 5-12 | đã sửa: "$A$ là thuật toán học PAC bất khả diễn … nếu, cùng thứ tự lượng từ,"; ba dòng song song "… thay cho …"; ghi chú bỏ câu "Tóm lại" (ghi chú 185 âm tiết) |
| SP31 | 6-01 | đã sửa (cùng HV4, HV18) |
| SP32 | 6-02 | đã sửa (cùng CG4) |
| SP33 | 6-04 | đã sửa: dữ kiện thành danh sách; $0{,}8^{10}\approx0{,}107$ trong công thức hiển thị; ghi chú bỏ câu chẻ |
| SP34 | 6-05, 6-06 | đã sửa: "thất bại chỉ khi …", "dãy ngắn nhất" |
| SP35 | ghi chú 7-00, 7-02 | đã sửa |
| SP36 | 7-02 | đã sửa: năm dòng là điều kiện của "học được" (học, cỡ mẫu không phụ thuộc $D$, $L_S$ với $h=A(S)$, phản ví dụ, bảo đảm của $A_{\max}$) |
| SP37 | ghi chú 7-03 | đã sửa: "Thuật toán không biết $\eta$; nó chỉ thấy $S$." |
| SP38 | 7-04 | đã sửa: "hàm vừa học có rủi ro không quá $\epsilon$ với xác suất $95\%$ không?" |
| SP39 | 7-01 | đã sửa (cùng CG17) |
| SP40 | ghi chú 3-01, 4-01, 5-07, 5-11, 6-06 | đã sửa: câu đọc hình nói điều cần nhìn, không chép alt |
| SP41 | ghi chú 3-01, 6-07 | đã sửa: "kí hiệu", "lôgarit" |
| SP42 | ghi chú 2-01 | không sửa: deck theo ghi chú ("mini-batch"); đề xuất sửa ghi chú số 5 của điều phối viên |
| MT1 (TB) | 3-01 | đã sửa: dòng "$L_D(h)$ không tính được vì $D$ chưa biết; $L_S(h)$ tính được từ $S$." |
| MT2 (TB) | 5-07 | đã sửa: "…, nên $L_D(A(S))\le\epsilon$ không đạt khi $\epsilon<0{,}05$" |
| MT3 (TB) | 5-11, 5-12 | đã sửa: "Câu hỏi: so $L_D(A(S))$ với $\inf_hL_D(h)$ hay với $L_D^{\mathrm{Bayes}}$?" cuối 5-11; ghi chú bỏ "Câu hỏi của ghi chú:" |
| MT4 (TB) | 6-02, 6-05 | đã sửa: Ý nghĩa của 6-02 và dòng đầu 6-05 "Lớp hàm ngưỡng có cỡ mẫu đủ chung cho mọi phân bố khả diễn." |
| MT5 (TB) | 7-05 | đã sửa theo quyết định: 01.3 (mạch 3); 01.6 (mạch 4); 01.1, 01.2, 01.5, 01.7, 01.11 (mạch 5); 01.4, 01.8, 01.9, 01.10 (mạch 6). Mạch 2 không còn bài nào, nên bỏ hàng. Ghi chú diễn giả nói phần nào của bài nhiều phần dùng kiến thức nào |
| MT6 (TB) | 4-02 | đã sửa (cùng SP4) |
| MT7 | 4-06 | đã sửa: dòng cuối "Trên $S_f$, $A_{\mathrm{gn}}(S_f)=h_4\in\mathcal H$: bảo đảm học phải cho phép thất bại trên những tập như $S_f$"; vế "phát biểu trực tiếp cho $L_D(A(S))$" ở ghi chú diễn giả 4-06 (trang ở 60 âm tiết) |
| MT8 | 7-04 | đã sửa: "Cỡ $14$ dưới $D_f$ …" |
| MT9 | ghi chú 3-03 | đã sửa: câu về $N=\hat t-3$ chuyển sang 3-05 |
| MT10 | 4-03/4-04, 6-06/6-07 | không sửa: báo cáo chấp nhận thứ tự hiện tại khi nhất quán (cùng HV13) |
| MT11 | 6-06, 6-07 | đã sửa: 6-07 nêu dạng chung "xác suất không quá $e^{-\epsilon m}$" và $e^{-\epsilon m}\le\delta\iff m\ge\ln(1/\delta)/\epsilon$; chuỗi đầy đủ chỉ ở 6-06 |
| MT12 | 2-02 | đã sửa: "hàm gán nhãn (labeling function, target function)" |
| MT13 | ghi chú 7-02 | đã sửa: "Hai dòng đầu trả lời trực tiếp câu hỏi; ba dòng sau là các kết quả đỡ cho câu trả lời." |

**Tổng:** 110 phát hiện; đã sửa 107, không sửa 3 (HV13 và MT10 đề xuất bác bỏ vì thứ tự theo quy định; SP42 vì deck theo ghi chú). Các mục trong bảng quyết định của điều phối viên (dòng dẫn mạch, ghi chú trang tiêu đề mạch, bảng 7-05, "Kí hiệu:", "lôgarit", quy ước đếm âm tiết, 6-03, ERM xấp xỉ) đã áp dụng như trên.

**Kiểm tra máy** (`deck_check.py --shots`, thư mục nháp `lec-01/editor/`): slides=55, console=0, pageerrors=0, failed=0, `.katex-error`=0, không trang tràn khung 1600×900. Cờ NARROW-H của công cụ còn ở các trang có công thức hiển thị hoặc bảng rộng: đó là các phần tử bên trong vùng cuộn ngang tại chỗ; trang không cuộn ngang ở mọi trang (390 px). Liên kết `#/2`…`#/7` và phím →, ↓, Space, Esc đã thử.

### Lượt 2 (2026-11-15, theo `reviews/deck-kiem-lai-1.md`)

| Phát hiện | Trang | Xử lý |
|---|---|---|
| trung bình: nội dung chạm đáy khung ở 1600×900 | 6-03, 2-04, 7-01, 6-05 và năm trang `footer_check.py` báo thêm (1-06, 3-01, 4-01, 5-07, 6-06) | đã sửa; `footer_check.py` báo 0 trang. 1-06: bỏ "hàm chỉ báo (indicator)" khỏi mặt trang, đưa vào đầu ghi chú. 2-04: bỏ ngoặc $c_{FN}=c_{FP}=1$ (ghi chú đã có). 3-01: câu "$L_D(h)$ không tính được …" vào cột trái của lưới; bỏ "trên $S=(z_1,\ldots,z_m)$". 4-01: bỏ "chắc chắn" và "ở đây $\mathcal X=[0,1]$" (lặp dòng trên). 5-07: phép tính $0{,}2\cdot\min\{\tfrac14,\tfrac34\}=0{,}05$ chuyển vào ghi chú; bỏ "tại mỗi mức". 6-03: bước (a) dẫn Mệnh đề 01.15 thay hai ngoặc giả thiết (ghi chú nêu đủ); bỏ "trên mọi $S$ (cả hai giả thiết)" ở (b) vì bước 2 đã nêu. 6-05: "lớn hơn $\epsilon$" thành "$>\epsilon$", bớt hai chữ "mọi". 6-06: bước 3 dẫn "(bước 2)" thay $D_{\mathcal X}(\{t^\star,\ldots,k-1\})$ (ghi chú có $G(k)\le\epsilon$); hình F7 bớt lề, viewBox 640×182. 7-01: tiêu đề cột "Giả thiết không được bỏ" (ghi chú giải thích nghĩa); $c_{FP}/(c_{FP}+c_{FN})$ viết một dòng; bỏ nhóm ngoặc làm cột 1 quá rộng; "trên $\mathcal M_{\mathcal X}$" của Hệ quả 01.29 bỏ vì cột giữa "như Mệnh đề 01.15" đã gồm $\mathcal H=\mathcal M_{\mathcal X}$. Không giảm cỡ chữ; chữ trong hình ≥ 17,1 px ở 1600×900. |
| nhẹ: ngoặc chen giữa câu và công thức | 2-04 | đã sửa: "… khi $Y=0$, nên" + công thức |
| nhẹ: Hệ quả 01.29 chưa ghi loại bảo đảm | 7-01 | đã sửa: "Hệ quả 01.29 (tất định)" |
| nhẹ: dòng dẫn 7-00 nói về bài | 7-00 | đã sửa: câu nội dung theo cuối §7 của ghi chú (xem §3) |
| nhẹ: "Phần này" làm chủ ngữ | ghi chú 3-00, 5-00, 6-00 | đã sửa: chủ ngữ là rủi ro thực nghiệm, hai định nghĩa học PAC, phản ví dụ |
| nhẹ: "khoảng 95 lần" lệch 5-06 | ghi chú 7-04 | đã sửa: "có ít nhất khoảng 95 lần" |
| nhẹ: "không ước lượng không chệch" dùng như động từ | 7-02 | đã sửa: "không là ước lượng không chệch của $L_D(h)$" |
| nhẹ: (T2) thiếu chủ ngữ; ghi chú chỉ dẫn "định nghĩa ở phần sau" | 1-02 | đã sửa: "khi $\ell$ không bị chặn, rủi ro kì vọng phải hữu hạn"; ghi chú "$L_D(h)=\mathbb E_{Z\sim D}\,\ell(h,Z)<\infty$" |
| nhẹ: so 14, 6 với 30 trộn hai $\epsilon$ | ghi chú 6-07, alt và `<desc>` của `can-co-mau.svg` | đã sửa: $14$ so với cận $30$ ở cùng $\epsilon=0{,}1$; $6$ ứng với $\epsilon=0{,}25$, cận chung tại $\epsilon=0{,}25$ là $\lceil4\ln20\rceil=12$ |
| nhẹ: dấu câu rơi xuống dòng riêng ở 390 px | 6-03 bước 3 và (b), 5-12 hai gạch đầu dòng, 5-05, 7-01 hai ô | đã sửa: dấu câu đưa vào trong `$…$` |
| bổ sung (người duyệt mạch Bài 02): 7-06 viết "$>\epsilon$", Bài 02 viết "$\ge\epsilon$" | 7-06 | không sửa: ghi chú Bài 01 ở đúng ngữ cảnh (dòng 1250) viết $\Pr(\lvert L_S(h)-L_D(h)\rvert>\epsilon)$; deck theo ghi chú. Chênh lệch giữa hai bài thuộc về ghi chú, chuyển điều phối viên |

**Kiểm tra máy lượt 2:** `footer_check.py` 0 trang; `deck_check.py --shots`: slides=55, console=0, pageerrors=0, failed=0, `.katex-error`=0, không tràn khung; mật độ trung bình 47,7, mọi trang ≤ 60 trừ 1-01 và 7-03 (ngoại lệ đã ghi). Đã xem ảnh 1600×900 và 390×844 (kể cả `-end`) của các trang đổi.

### Lượt 3 (2026-11-15, theo `reviews/deck-kiem-lai-2.md`)

| Phát hiện | Trang | Xử lý |
|---|---|---|
| trung bình: tiêu đề cột "Giả thiết then chốt" lệch quy định `REPO/CLAUDE.md` § Slide decks | 7-01, ghi chú 7-00 và 7-01, storyboard | đã sửa: trả về "Giả thiết không được bỏ" ở mặt trang, hai ghi chú và storyboard (thay quyết định "then chốt" ghi ở Lượt 2). Bù dòng tiêu đề bằng `<colgroup>` với thuộc tính HTML `width` 41% / 31% / 28% (không dùng CSS), tiêu đề cột giữa nằm trên một dòng; `footer_check.py` 0 trang |
| nhẹ: hàm chỉ báo không còn giới thiệu trên mặt trang sau khi rút 1-06 | 1-02 | đã sửa: dòng "Kí hiệu:" thêm "hàm chỉ báo (indicator function) $\mathbb 1[\cdot]$"; ghi chú 1-06 bỏ tên tiếng Anh lặp lại |
| nhẹ: "(bước 2)" không nêu lý do | 6-06 | đã sửa: "($C$ ngắn nhất)" |
| nhẹ: $z_i$ ở 3-01 chưa có chỗ giới thiệu | 2-01 | đã sửa: "$S=(z_1,\ldots,z_m)\sim D^m$" |
| bảng 7-01 ở 390 px | 7-01 | điều phối viên đã sửa CSS (commit 56b2226); không sửa deck |

**Kiểm tra máy lượt 3:** `footer_check.py` 0 trang; `deck_check.py --shots`: slides=55, console=0, pageerrors=0, failed=0, `.katex-error`=0, không tràn khung; mật độ trung bình 47,9. Đã xem ảnh 1600×900 và 390×844 (kể cả `-end`) của 1-02, 2-01, 6-06, 7-01.
