# Storyboard — Bộ trang chiếu Bài 04: Phân tích sai số, tối thiểu hóa rủi ro cấu trúc và chọn mô hình

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-11-15 bởi tác tử lập storyboard. Nguồn nội dung duy nhất: `materials/lec-04/lecture-note.md` (bản hiện hành); bài tập: `materials/lec-04/exercises.md`. Quy định: `CLAUDE.md` § Slide decks, `common-brief.md` (gồm "Các quy định dễ sót" và "Bài học từ năm báo cáo duyệt deck 01"), `brief-storyboard.md`, `../rl-plan/CLAUDE.md` § Deck structure and content, nhật ký yêu cầu 2026-11-13 hàng 1–5, quyết định của điều phối viên trong `lec-0{1,2,3}/review-log.md` § Bộ trang chiếu. Khuôn bố cục theo storyboard Bài 03 (đã qua cổng duyệt). Mọi mã trang có dạng `L04-k-mm`; trong bảng viết gọn `k-mm`.

Số âm tiết trong tệp này đếm bằng script (mục 15) theo cách của `deck_check.py`, cộng thêm số viết ngoài KaTeX (quyết định Bài 01); điều phối viên đếm lại trên deck.

UML đã đọc để đối chiếu (không chép câu chữ): §7.1–7.2, trang PDF 85–86 (Định lý 7.3 của UML, hàm trọng số $w(n)$ trên các lớp, ví dụ $w(n)=6/(\pi^2n^2)$). Các mục khác chỉ dẫn theo §12 của ghi chú và `sources/uml-sections.md` (§5.2 trang 64, §7.1 trang 83, §7.2 trang 85, §7.3 trang 89, §11.1 trang 145, §11.2 trang 147).

**Kí hiệu trọng số.** Bản giao việc viết "chia $\delta$ theo trọng số $w_k$". Deck dùng kí hiệu của ghi chú: $q_k$ (`ky-hieu.md` dòng 34: "không dùng $w$ cho trọng số lớp"; $w$ là véc-tơ hệ số của hàm phân lớp tuyến tính trong ứng dụng). Bản giao việc nói "tập kiểm tra/kiểm định"; deck dùng "mẫu xác thực" (validation sample) như ghi chú §8 và `thuat-ngu.md` dòng 254–255; "tập kiểm tra" chỉ xuất hiện ở ghi chú diễn giả về Bài tập 04.6.

## 1. Tên tệp và tiêu đề

- **Tệp deck:** `2627-1/lecture-04-phan-tich-sai-so.html` (slug ASCII từ phần đầu tên bài).
- **Tiêu đề deck (h1 trang bìa):** "Phân tích sai số, tối thiểu hóa rủi ro cấu trúc và chọn mô hình" (đúng tên bài của ghi chú).
- **`<title>`:** "Bài 04: Phân tích sai số".
- **Chân trang:** "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài 04".
- **Liên kết viewer:** `material-viewer.html?doc=materials/lec-04/lecture-note.md&deck=lecture-04-phan-tich-sai-so.html` và `…exercises.md&deck=…`.
- **Màn hẹp:** chế độ đọc của `lecture-course.css` (`.slides` bọc trong `div.lecture-viewport`, script màn hẹp của `lecture-template.html`); bảng rộng (4-07, 3-04, 7-01) đặt trong `.table-scroll`.
- **Trang cuối deck Bài 03** (7-06 của storyboard Bài 03) nhận liên kết tới tệp này khi deck Bài 04 xong.

## 2. Khung lý thuyết chung

**Vấn đề trung tâm (hộp "Vấn đề trung tâm", bằng lời, ≤ 30 âm tiết).** "**Câu hỏi:** với cỡ mẫu cho trước, chọn lớp giả thuyết nào trong một dãy lớp để hàm học được có rủi ro kì vọng nhỏ?" (câu hỏi trung tâm ở đoạn mở đầu của ghi chú, "chọn độ phức tạp của mô hình theo cỡ mẫu", và câu hỏi cầu nối của Bài 03; 26 âm tiết kể cả nhãn.)

**Luận điểm (trang bìa, một câu, bằng lời).** "Rủi ro của hàm học được gồm sai số xấp xỉ, không tăng khi lớp lớn dần, và sai số ước lượng, có cận tăng theo lớp; số hạng phạt rút từ cận đó, hoặc một mẫu xác thực, cho phép chọn lớp theo cỡ mẫu." (đoạn mở đầu, §4 cuối, §6, §8, §9 của ghi chú; 46 âm tiết; không kí hiệu.)

**Trọng tâm trực quan của deck.** Khi lớp lồng nhau lớn dần, sai số xấp xỉ không tăng nhưng không quan sát được, còn số hạng thống kê $2r$ (sau đó $2\,\mathrm{pen}_k$) tăng nhưng tính được (ghi chú, đoạn cuối §4). Ý này xuất hiện ở năm chỗ: 1-06 (lớp lớn nhất luôn có rủi ro thực nghiệm nhỏ nhất; cận tăng từ $0{,}329$ lên $0{,}560$), 2-07 (so hai lớp: hiệu sai số xấp xỉ phải vượt $0{,}2310$), 3-04 (bậc tốt nhất đổi theo mức nhiễu), 4-08 và 4-10 (vế phải của bất đẳng thức oracle; hình F2: $L_S(\hat h_k)$ giảm, $\mathrm{pen}_k$ tăng, tổng nhỏ nhất tại $k=3$), 7-03 (bài tập tổng hợp: SRM giữa hai lớp hình chữ nhật).

**Đối tượng và kí hiệu chung** (ghi chú §1–§3, `ky-hieu.md`):
- $\mathcal Z=\mathcal X\times\mathcal Y$, $\mathcal Y=\{0,1\}$ (phân lớp) hoặc $\mathbb R$ (hàm lỗi bình phương); $D$ cố định, chưa biết; $S=(Z_1,\ldots,Z_m)\sim D^m$;
- họ lớp $\mathcal H_1,\mathcal H_2,\ldots$ (hữu hạn hoặc đếm được, chọn trước, không nhất thiết lồng nhau), $k$, $k_{\max}$, $d_k$, $q_k$; bán kính hội tụ đều $\mathrm{rad}_{\mathcal H}(m,\delta')$, $\mathrm{rad}_k$; số hạng phạt $\mathrm{pen}_k=\mathrm{rad}_k(m,\delta q_k)$; dung sai $\tau$; nghiệm SRM $(\hat k,\hat h)$; $\hat h_k$;
- rủi ro tham chiếu $L^*$; đầu ra của bộ giải $\tilde h=\tilde h(S)$; sai số tối ưu thực nghiệm $\operatorname{opt}_S(\tilde h)$; $\epsilon_{\mathrm{opt}}$;
- hàm lỗi bình phương: $f^*$, $\sigma^2(x)$, $\hat f_S$, $\bar f$, $\zeta_i$, $\mathcal P_j$, $\hat f^{(j)}$, $x_0$;
- học không đều: $M(\epsilon,\delta,h)$, $k(h)$, $M_k(\epsilon)$, $A_{\mathrm{SRM}}$;
- mẫu xác thực $V=(V_1,\ldots,V_{m_v})$, $m_v$, $L_V$; ứng viên $g_1,\ldots,g_K$, $\hat g$;
- ví dụ xuyên suốt: ba bậc đa thức trên ba điểm thiết kế (Ví dụ 04.1, 04.4) và hàm phân lớp tuyến tính trên $k$ chỉ số đo đầu tiên, $k=1,\ldots,10$ (khối ứng dụng §3; Ví dụ 04.3, 04.7, 04.9, 04.12); ví dụ sàng lọc dưới $D_\eta$ của Bài 01 (Ví dụ 04.2, Nhận xét 04.4, Bài tập 04.1).

**Giả thiết** (ghi chú §2): (T1) độc lập cùng phân bố; (T2) $\ell\ge0$, đo được; (T3) $\ell\in[0,1]$; (T4) lớp hữu hạn chọn trước; (T5) lớp chọn trước; (M) lớp con đếm được xấp xỉ theo từng điểm; (T6) họ lớp, bán kính, trọng số $q_k>0$, $\sum_kq_k\le1$ cố định trước khi lấy mẫu; (T7) mẫu xác thực độc lập với $S$, ứng viên là hàm của $S$; (O1), (O2).

**Chuỗi định nghĩa → kết quả → phương pháp.**
1. Lớp lớn nhất luôn có rủi ro thực nghiệm nhỏ nhất (Câu hỏi mở đầu, Ví dụ 04.1) → cần tách rủi ro thành phần không tăng theo lớp và phần có cận tăng theo lớp.
2. Rủi ro tham chiếu, sai số xấp xỉ, sai số ước lượng (Định nghĩa 04.1, Ví dụ 04.2); sai số tối ưu thực nghiệm (Định nghĩa 04.2, Nhận xét 04.4) → cận ba thành phần (Mệnh đề 04.3, Ví dụ 04.3).
3. Hàm lỗi bình phương: hàm hồi quy, độ chệch, phương sai (Định nghĩa 04.5) → đẳng thức độ chệch–phương sai (Mệnh đề 04.6, Ví dụ 04.4); bỏ độc lập (Ví dụ 04.5); hàm phân lớp (Ví dụ 04.6); độ chệch khác sai số xấp xỉ (Nhận xét 04.7).
4. Bán kính hội tụ đều (Định nghĩa 04.8) → chia xác suất thất bại (Bổ đề 04.9, Ví dụ 04.7, 04.8) → SRM (Định nghĩa 04.10) → bất đẳng thức oracle (Định lý 04.11) → Thuật toán 04.12, Ví dụ 04.9; bỏ (T6) (Ví dụ 04.10); độ dài mô tả (Nhận xét 04.13, đọc thêm).
5. Học không đều (Định nghĩa 04.14) → SRM với $\delta=1/m$ (Hệ quả 04.15) → lớp đếm được có chiều VC vô hạn (Ví dụ 04.11); đặc trưng (Định lý 04.16, đọc thêm).
6. Mẫu xác thực (T7) → Hệ quả 04.17, Ví dụ 04.12; phạm vi (Nhận xét 04.18).

**Giới hạn áp dụng** (ghi chú §9): các cận của Mệnh đề 04.3, Bổ đề 04.9, Định lý 04.11, Hệ quả 04.17 cần hàm lỗi trong $[0,1]$, không chuyển sang hàm lỗi bình phương hay log mà không có giả thiết bị chặn (Nhận xét 02.11); Mệnh đề 04.6 là đẳng thức kì vọng cho một thuật toán, không cho quy tắc chọn từ dữ liệu; với hàm phân lớp, đẳng thức đúng về số nhưng không cho đánh đổi (Ví dụ 04.6); bốn giả thiết có phản ví dụ khi bỏ: họ lớp cố định (Ví dụ 04.10), tổng trọng số không quá $1$ (Ví dụ 04.8), nhãn kiểm tra độc lập (Ví dụ 04.5), mẫu xác thực dùng một lần (Nhận xét 04.18, Bài tập 04.5); chính quy hóa với $\lambda$ chọn trên chính tập huấn luyện nằm ngoài Định lý 04.11. Phụ lục A, D, E chỉ vào ghi chú diễn giả; Phụ lục B, C cho số liệu.

## 3. Bảng mạch

Bảy mạch theo đúng thứ tự các mục của ghi chú; mỗi mạch ứng với các mục liên tiếp. Bảng đối chiếu trang → khối ghi chú ở mục 12.

| N | Tên mạch | Mục ghi chú | Chức năng | Đầu vào | Đầu ra | `strand-lead` (âm tiết) | Từ khóa | Trang | Phút |
|---|---|---|---|---|---|---|---|---:|---:|
| 1 | Mở đầu | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết, §3 (khối ứng dụng, câu hỏi cầu nối Bài 03) | Bìa, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, câu hỏi chọn bậc và chọn số chỉ số đo | Bài 03: cận rủi ro vượt mức so với một lớp cố định | Hai câu hỏi chọn lớp; cận tăng $0{,}329\to0{,}560$ | (không có trang tiêu đề mạch) | — | 6 | 8 |
| 2 | Phân tích sai số | §1–§4 | Thiết lập họ lớp; hai ví dụ xuyên suốt; Định nghĩa 04.1, 04.2; Mệnh đề 04.3 và ý tưởng chứng minh; Ví dụ 04.3; Bài tập 04.1(b) | lớp lớn nhất luôn thắng theo rủi ro thực nghiệm | Cận ba thành phần; chỉ phần thống kê tính được; cần chia $\delta$ giữa các lớp | "Cận cho rủi ro có ba phần: do lớp giả thuyết, do cỡ mẫu hữu hạn và do tối ưu không chính xác." (23) | rủi ro tham chiếu · sai số xấp xỉ · sai số ước lượng · sai số tối ưu thực nghiệm | 9 | 22 |
| 3 | Độ chệch và phương sai | §5 | Định nghĩa 04.5; Mệnh đề 04.6 và ý tưởng chứng minh; Ví dụ 04.4; Ví dụ 04.5 (bỏ độc lập); Nhận xét 04.7 (Ví dụ 04.6 ở ghi chú diễn giả); Bài tập 04.2(d) | hàm lỗi bình phương không bị chặn; Mệnh đề 04.3 không áp dụng | Bậc tốt nhất phụ thuộc $\sigma^2$, $f^*$; không cho quy tắc chọn từ dữ liệu | "Lỗi bình phương trên một nhãn mới tách thành phần do thuật toán và phần nhiễu không thuật toán nào giảm được." (22) | hàm hồi quy · dự đoán trung bình · độ chệch · phương sai · nhãn kiểm tra độc lập | 8 | 19 |
| 4 | Chia xác suất thất bại và tối thiểu hóa rủi ro cấu trúc | §6 | Định nghĩa 04.8; (T6); Bổ đề 04.9, ý tưởng chứng minh, kỹ thuật chia theo trọng số (Ví dụ 04.7); Ví dụ 04.8; Định nghĩa 04.10; Định lý 04.11, ý tưởng chứng minh; Ví dụ 04.9 (Thuật toán 04.12), hình F2; Ví dụ 04.10; Bài tập 04.4(b) | cận đúng riêng cho từng lớp chọn trước | $\mathrm{pen}_k=\mathrm{rad}_k(m,\delta q_k)$; bất đẳng thức oracle; SRM chọn $k=3$, cận $0{,}3651$ | "Khi cận đúng đồng thời cho mọi lớp, chọn lớp theo tập huấn luyện vẫn giữ được bảo đảm cho rủi ro." (22) | bán kính hội tụ đều · trọng số · số hạng phạt · bất đẳng thức oracle · dung sai | 13 | 34 |
| 5 | Học không đều | §7 | Định nghĩa 04.14; Hệ quả 04.15 và ý tưởng chứng minh (cỡ mẫu $172\,279$; $181\,575$; $213\,317$); Ví dụ 04.11; Định lý 04.16 (đọc thêm) | $\mathrm{pen}_k\to\infty$: cỡ mẫu phụ thuộc lớp chứa giả thuyết so sánh | Một thuật toán không nhận $\delta$; học được không đều không kéo theo học được PAC | "Cỡ mẫu đủ được phép phụ thuộc giả thuyết so sánh, nhưng không phụ thuộc phân bố." (17) | giả thuyết so sánh · cỡ mẫu theo lớp · xác suất thất bại giảm theo cỡ mẫu | 5 | 12 |
| 6 | Chọn mô hình bằng mẫu xác thực | §8 | (T7); Hệ quả 04.17 và ý tưởng chứng minh; Ví dụ 04.12 (hình F3); Nhận xét 04.18; Bài tập 04.5(a) | SRM trả số hạng phạt trên cùng tập huấn luyện | Giá $2\sqrt{\ln(2K/\delta)/(2m_v)}$; cần danh sách ứng viên cố định trước khi dùng $V$ | "Một mẫu dữ liệu mới, chỉ dùng để chọn, cho cận tăng theo căn bậc hai của lôgarit số ứng viên." (21) | mẫu xác thực · ứng viên · lấy điều kiện · dùng lại thích nghi · kiểm tra chéo | 6 | 14 |
| 7 | Tổng kết | §9–§12 | Bảng kết quả, trả lời vấn đề trung tâm, bài tập tổng hợp (Bài tập 04.7(c)), tự kiểm tra (gồm câu hỏi cuối buổi), bài tập về nhà, tài liệu | mọi kết quả | Cầu nối sang Bài 05 | "Số hạng phạt và mẫu xác thực là hai cách chọn lớp phù hợp với cỡ mẫu, mỗi cách cần giả thiết riêng." (23) | — | 8 | 11 |
| | **Tổng** | | | | | | | **55** | **120** |

Số trang (55) vượt mục tiêu 45–52 ba trang, đúng trần 55. Lý do: sáu kết quả chính (Mệnh đề 04.3, 04.6, Bổ đề 04.9, Định lý 04.11, Hệ quả 04.15, 04.17), mỗi kết quả có trang phát biểu và trang "Ý tưởng chứng minh" riêng (12 trang); một kỹ thuật mới dùng lại ở Bài 07 có trang "Kỹ thuật." riêng (4-04); bốn trang bài tập giữa cụm (mạch 2, 3, 4, 6) và một bài tập tổng hợp hai trang (đề và lời giải: câu chữ của Bài tập 04.7(c) đã chiếm 47 âm tiết, một trang vượt trần 60), theo khuôn chung; bốn phản ví dụ bỏ giả thiết mà ghi chú §9 liệt kê (3-05, 4-05, 4-11, 6-05). Đã gộp để giữ 55: câu hỏi mở đầu và câu hỏi cầu nối Bài 03 chung trang 1-06; hai ví dụ xuyên suốt chung trang 2-02; Định nghĩa 04.1 và Ví dụ 04.2 chung trang 2-03 (hình F1); Nhận xét 04.4 thành dòng "Lưu ý:" trên 2-04; Ví dụ 04.7 thành dòng "Ví dụ." trên trang kỹ thuật 4-04; Thuật toán 04.12 thành một dòng trên 4-07 (đầy đủ ở ghi chú diễn giả); Ví dụ 04.6 ở ghi chú diễn giả 3-06; phần số của Hệ quả 04.15 thành dòng "Ví dụ." trên 5-03; Định lý 04.16 (đọc thêm) chung trang với Ví dụ 04.11. Phương án rút còn 53 ở mục 11, điểm 2.

## 4. Bảng kết quả chính

Số hiệu theo ghi chú. Ánh xạ blueprint → ghi chú (theo `outline.md` §2): Proposition 4.1 → Mệnh đề 04.3; Proposition 4.2 → Mệnh đề 04.6; Lemma 4.3 → Bổ đề 04.9; Theorem 4.4 → Định lý 04.11; Corollary (validation) → Hệ quả 04.17. Hệ quả 04.15 là kết quả của học phần (ghi chú §12, "Quan hệ với giáo trình UML"). Mọi phát biểu rút gọn trên trang dùng "Giả thiết:" và "Bảo đảm:", giữ đủ giả thiết, lượng từ, hằng số và loại bảo đảm của ghi chú.

| Kết quả | Loại bảo đảm | (a) Trực quan | (b) Ý tưởng chứng minh | (c) Kỹ thuật | (d) Ví dụ bổ trợ | Trang |
|---|---|---|---|---|---|---|
| **Mệnh đề 04.3** (cận trên ba thành phần; chứng minh đầy đủ) | (a) tất định trên biến cố đại diện; (b) xác suất cao theo $S$, đồng thời mọi quy tắc, mọi $D$; phụ thuộc $m$, $\delta$, $\lvert\mathcal H\rvert$ hoặc hàm tăng trưởng qua $r$ | Ba số hạng ba nguồn: sai số xấp xỉ (tất định, không quan sát được), $2r$ (do cỡ mẫu, tính được), $\operatorname{opt}_S$ (do bộ giải, tính được trên $S$). Hình F1 cho phần đẳng thức. | Ba bước: thêm bớt $L_S$ (chuỗi bốn quan hệ); tính đại diện tại $\tilde h$ (cần cận đều vì $\tilde h$ chọn theo $S$), định nghĩa $\operatorname{opt}_S$, cận dưới đúng, tính đại diện tại $h$; lấy $\inf_h$, trừ $L^*$; phần (b): (T1), (T3), (T4) hoặc (T1), (T5), (M) chỉ vào xác suất của biến cố đại diện. Bỏ cận đều: bất đẳng thức đầu không có cơ sở. | Nhắc lại **bước tất định trên biến cố đại diện** (Bài 02). | Ví dụ 04.2 (F1: $0{,}04$, $0{,}10$); Nhận xét 04.4 ($-0{,}10$); Ví dụ 04.3 ($a_2+0{,}3389$, $a_{10}+0{,}5698$, ngưỡng $0{,}2310$); Bài tập 04.1(b) ($0{,}5667$ so với $0{,}14$). | 2-03 đến 2-08 |
| **Mệnh đề 04.6** (độ chệch–phương sai tại một điểm; chứng minh đầy đủ) | đẳng thức kì vọng trên $(S,Y)$, một thuật toán, một điểm; đúng cả khi hàm lỗi không bị chặn; $m$ vào qua phân bố của $\hat f_S(x)$ | Dự đoán lệch nhãn mới vì ba lẽ: dao động quanh $\bar f(x)$, $\bar f(x)$ lệch $f^*(x)$, nhiễu của $Y$. Hàm cố định: phương sai $0$, lỗi $\ge\sigma^2(x)$. | Bốn bước: tách quanh $\bar f$ và $f^*$; Cauchy–Schwarz cho khả tích; ba bình phương; hai số hạng chéo có hằng số bằng $0$ nhờ $\mathbb E\hat f=\bar f$, $\mathbb EY=f^*$; số hạng chéo thứ ba bằng $0$ chỉ nhờ $Y$ độc lập với $S$. Bỏ độc lập: Ví dụ 04.5 ($0{,}75$ thay vì $1{,}25$). | Dòng "Kỹ thuật." trên 3-03: thêm bớt hai kì vọng rồi bình phương; mỗi số hạng chéo một lý do (chỉ dùng ở đây và Bài tập 04.2). | Ví dụ 04.4 (bảng, $\sigma^2=1$: bậc $0$; $\sigma^2=0{,}1$: bậc $2$); Ví dụ 04.5; Nhận xét 04.7; Ví dụ 04.6 (ghi chú diễn giả); Bài tập 04.2(d). | 3-01 đến 3-07 |
| **Bổ đề 04.9** (kiểm soát đồng thời trên một họ lớp; chứng minh đầy đủ) | xác suất cao theo $S$, đồng thời mọi $k$, mọi $h\in\mathcal H_k$; thực nghiệm so với tổng thể; $m$ qua $\mathrm{rad}_k$, $\delta$ và $q_k$ qua $\delta q_k$ | Lớp $k$ nhận phần $\delta q_k$ của xác suất thất bại; các phần cộng lại không quá $\delta$; lớp có trọng số nhỏ trả bán kính lớn hơn. | Ba bước: biến cố hỏng $B_k$ (đo được theo Định nghĩa 04.8); $\Pr(B_k)\le\delta q_k$ vì $\mathrm{rad}_k$, $q_k$ không phụ thuộc $S$ ((T6); (T1), (T3) vào qua bán kính); dạng đếm được của bất đẳng thức hợp, $\sum_kq_k\le1$ ở bất đẳng thức thứ hai. Bỏ $\sum_kq_k\le1$: Ví dụ 04.8 ($0{,}858$). Bỏ "chọn trước": Ví dụ 04.10. | **Chia xác suất thất bại theo trọng số** (lần đầu, trang riêng 4-04; dùng lại ở Hệ quả 04.15 và Bài 07). Nhắc lại bất đẳng thức hợp (Bài 01) và chia $\delta/K$ (Bài 02). | Ví dụ 04.7 ($\mathrm{pen}_3\approx0{,}1900$ so với $0{,}1843$; tăng $1\%$ đến $3{,}2\%$); Ví dụ 04.8. | 4-01 đến 4-05 |
| **Định lý 04.11** (bất đẳng thức oracle cho SRM; chứng minh đầy đủ) | xác suất cao theo $S$; đồng thời mọi nghiệm $\tau$-chính xác; (a) cận trên tin cậy thực nghiệm, (b) so với mốc có phạt; $m$, $\delta$, $q_k$, độ phức tạp qua $\mathrm{pen}_k$ | Vế phải của (b): $\inf_{h\in\mathcal H_k}L_D(h)$ không tăng khi lớp lồng nhau lớn dần, $2\,\mathrm{pen}_k$ tăng; SRM cân hai phần qua $L_S(h)+\mathrm{pen}_k$ mà không biết phần thứ nhất. Hình F2. | Ba bất đẳng thức trên biến cố $E$ của Bổ đề 04.9: $E$ tại $(\hat k,\hat h)$ (cần đồng thời theo $k$ vì $\hat k$ chọn theo $S$; đây là (a)); tính $\tau$-chính xác; $E$ tại $(k,h)$ cố định; lấy cận dưới đúng theo $h$, rồi theo $k$. Bỏ (T6): Ví dụ 04.10 ($0{,}0469$ so với $0{,}8$). | Nhắc lại bước tất định (Bài 02); chia xác suất thất bại theo trọng số (4-04). | Ví dụ 04.9 (bảng mười lớp; $0{,}3651$; $0{,}4350$; $0{,}3593$; $0{,}0058$; $0{,}0130$); Bài tập 04.4(b); Bài tập 04.7(c) (7-03). | 4-06 đến 4-12 |
| **Hệ quả 04.15** (SRM với xác suất thất bại $1/m$; chứng minh đầy đủ ở Phụ lục B) | (a) học không đều, $M(\epsilon,\delta,h)$ phụ thuộc $h$ qua $k(h)$, không phụ thuộc $D$; (b) danh sách hữu hạn: học PAC bất khả diễn | SRM nhận $\delta$, còn Định nghĩa 04.14 đòi một thuật toán cố định trước $\epsilon$, $\delta$; chọn $\delta=1/m$ giảm theo cỡ mẫu. | Bốn bước: Định lý 04.11(b) tại $\delta=1/m$, $\tau=0$; $\mathrm{pen}_k(m)=\sqrt{(a+b\ln m)/m}\to0$, nên $M_k(\epsilon)<\infty$; $m\ge\max\{\lceil1/\delta\rceil,M_{k(h)}(\epsilon)\}$ cho $1/m\le\delta$ và $2\,\mathrm{pen}\le\epsilon$; hữu hạn lớp: $\max_k M_k$, lấy $\inf_h$. Giá: $\ln m$ thay cho $\ln(1/\delta)$. | Dòng "Kỹ thuật." trên 5-03: chọn $\delta=1/m$ để bỏ $\delta$ khỏi đầu vào (chỉ dùng ở đây). Nhắc lại chia xác suất thất bại theo trọng số. | Cỡ mẫu đủ $172\,279$; $181\,575$; $213\,317$ ($+5{,}4\%$, $+17{,}5\%$); Ví dụ 04.11. | 5-01 đến 5-04 |
| **Hệ quả 04.17** (chọn mô hình bằng mẫu xác thực; phác thảo) | theo $(S,V)$, mỗi phần xác suất $\ge1-\delta$; (a) so với ứng viên tốt nhất (ngẫu nhiên qua $S$), (b) cận trên tin cậy; phụ thuộc $m_v$, $\ln K$, $\delta$, không phụ thuộc độ phức tạp của lớp hay $m$ | Mẫu xác thực chỉ dùng để chọn, nên chọn mô hình là ERM trên một lớp hữu hạn $K$ ứng viên; giá như lớp hữu hạn của Bài 02 với $m_v$ thay cho $m$. | Ba bước: lấy điều kiện theo $S$ (ứng viên thành lớp hữu hạn cố định; theo (T7), $V\sim D^{m_v}$ khi biết $S$); Hệ quả 02.16(a) cho (a), Định lý 02.14(b) cho (b); bỏ điều kiện bằng định lý Fubini. Hệ số $2$ trong $\ln(2K/\delta)$: hai phía của Hoeffding; hệ số $2$ ngoài căn: hai phép so sánh. Bỏ (T7): Bài tập 04.5(a) ($\ge0{,}6$ so với $0{,}1103$). | Dòng "Kỹ thuật." trên 6-02: lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện (dùng ở Ví dụ 02.8 Bước 1). Nhắc lại đảo cận đuôi thành bán kính và cỡ mẫu (Bài 02) ở 6-03. | Ví dụ 04.12 ($0{,}1095$; bảng theo $m_v$; $1199$, $4794$; $K=10^6$: $0{,}1871$); Nhận xét 04.18 ($0{,}4524$). | 6-01 đến 6-05 |

**Kết quả phụ và quyết định.**
- Định nghĩa 04.1 và Ví dụ 04.2: một trang (2-03) với hình F1; đoạn "số $0{,}25$ không phải rủi ro tham chiếu" ở ghi chú diễn giả 2-03.
- Định nghĩa 04.2 và Nhận xét 04.4: trang 2-04; Nhận xét 04.4 thành dòng "Lưu ý:" với phép tính $-0{,}10$; câu Ví dụ 01.7 ($\operatorname{opt}_S(h_w)=w^2$) ở ghi chú diễn giả.
- Phân tích độ chệch–phương sai theo thiết kế ngẫu nhiên (đoạn sau Mệnh đề 04.6) và rủi ro Bayes $\mathbb E\,\sigma^2(X)$ của hàm lỗi bình phương: ghi chú diễn giả 3-02 (Nhận xét 04.7 và 3-07 dùng $L^*=\sigma^2$).
- Ví dụ 04.6 (hàm phân lớp, $0{,}58$ so với $0{,}90$): ghi chú diễn giả 3-06, không có trang riêng (mục 11, điểm 2); §9 của ghi chú chỉ nêu nó như một giới hạn.
- Định nghĩa 04.8 có trang riêng 4-01, cùng hai bán kính của Bài 02–03 và dạng chiều VC; câu về lớp $\mathcal M_{[0,1]}$ ở ghi chú diễn giả.
- Thuật toán 04.12 và cận tinh hơn (Phụ lục E): một dòng trên 4-07, đầy đủ ở ghi chú diễn giả 4-07; Bài tập 04.4(a) chạy thuật toán.
- Nhận xét 04.13 (độ dài mô tả, đọc thêm): ghi chú diễn giả 4-11, nói rõ mức đọc thêm; Bài tập 04.10 ở bảng bài tập về nhà.
- Định lý 04.16 (đọc thêm; phác thảo (a) ở Phụ lục D): phát biểu rút gọn một dòng trên 5-04; không có trang ý tưởng chứng minh (ghi chú diễn giả nêu lộ trình phủ lớp và định lý không có bữa trưa miễn phí ở mức đọc thêm).
- Phụ lục A (tồn tại, đo được của nghiệm SRM): ghi chú diễn giả 4-06; Phụ lục B: 5-03; Phụ lục C: số liệu của 3-04, 4-04, 4-07; Phụ lục D: ghi chú diễn giả 5-04; Phụ lục E: ghi chú diễn giả 4-07.
- Câu ôn nhanh 1–3: ghi chú diễn giả 1-02 (câu 1: $r_m\approx0{,}0547$, dùng lại ở 6-03), 4-03 (câu 2: $0{,}05\sum_k2^{-k}=0{,}05$), 3-03 (câu 3: $\mathbb E(U-c)^2=\operatorname{Var}(U)+(\mathbb EU-c)^2$).
- §9 (ý nghĩa, giới hạn): cột "Giả thiết không được bỏ" của 7-01, trang 7-02 và ghi chú diễn giả 6-04; chính quy hóa ở ghi chú diễn giả 7-02.
- §11 (câu hỏi cuối buổi): câu 1 của 7-04.

## 5. Ví dụ bổ trợ

Ví dụ xuyên suốt: **ba bậc đa thức trên ba điểm thiết kế** (Ví dụ 04.1; câu hỏi mở đầu là bản 16 quan sát của nó) và **hàm phân lớp tuyến tính trên $k$ chỉ số đo đầu tiên** (khối ứng dụng §3). Mỗi lần dùng lại trả lời một câu hỏi mới. Ba bậc đa thức: rủi ro thực nghiệm luôn chọn bậc cao nhất (1-06, 2-02); độ chệch, phương sai và bậc tốt nhất theo mức nhiễu (3-04); chọn bậc bằng mẫu xác thực với $\lvert Y\rvert\le B$ (6-04, $0{,}4524$); trả lời câu hỏi mở đầu (7-02). Số chỉ số đo: cận tăng $0{,}329\to0{,}560$ (1-06); định nghĩa họ lớp, $d_k=k+1$ (2-02); cận ba thành phần cho $\mathcal H_2$, $\mathcal H_{10}$, ngưỡng $0{,}2310$ (2-07); giá của việc chia xác suất thất bại (4-04); SRM chọn $k=3$ (4-07, 4-10); chọn trong mười ứng viên bằng mẫu xác thực (6-03); cầu nối Bài 05 qua câu hỏi cuối buổi (7-04). Bài tập trên mặt trang lấy từ `exercises.md` với cùng số liệu, câu chữ và kết quả: Bài tập 04.1(b) (2-08), 04.2(d) (3-07), 04.4(b) (4-12), 04.5(a) (6-05), 04.7(c) (7-03, tổng hợp).

Mọi con số dưới đây đã tính lại bằng Python (thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-04/storyboard/num.py`) và khớp ghi chú, tệp bài tập. Không có ví dụ mới về số: mọi số trên mặt trang và trong hình lấy từ ghi chú hoặc `exercises.md`.

**V1. Câu hỏi mở đầu và cầu nối Bài 03** (1-06). $16$ quan sát, $x_i$ đôi một khác nhau; bậc $15$ nội suy: $L_S=0$. $2\rho_m$ với $m=10^4$, $\delta=0{,}05$: $d=3$: $2\cdot0{,}164430=0{,}32886\approx0{,}329$; $d=11$: $2\cdot0{,}279919=0{,}55984\approx0{,}560$.

**V2. Ví dụ 04.2** (2-03, hình F1). $L^*=0{,}18$; $\min_tL_{D_\eta}(h_t)=L_{D_\eta}(h_3)=0{,}22$; $L_{D_\eta}(h_2)=0{,}32$. Sai số xấp xỉ $0{,}04$; sai số ước lượng của $h_2$: $0{,}10$; tổng $0{,}14=0{,}32-0{,}18$. Lớp mọi hàm $\{1,\ldots,5\}\to\{0,1\}$ chứa $h_{\mathrm{Bayes}}=\mathbb 1[x\in\{3,5\}]$: sai số xấp xỉ $0$. Số $0{,}25$ cho "sai số xấp xỉ" $-0{,}03$.

**V3. Nhận xét 04.4** (2-04). $S=((1,0),(2,1))$ dưới $D_\eta$: $h_2$ là nghiệm ERM duy nhất, $L_S(h_2)=0$, $L_{D_\eta}(h_2)=0{,}32$; $\tilde h=h_3$: $\operatorname{opt}_S(h_3)=\tfrac12$, $L_{D_\eta}(h_3)=0{,}22$; hiệu $-0{,}10$.

**V4. Ví dụ 04.3** (2-07). $\rho_m\le0{,}16443$ ($d=3$), $\le0{,}27992$ ($d=11$); $2\cdot0{,}16443+0{,}01=0{,}33886\approx0{,}3389$; $2\cdot0{,}27992+0{,}01=0{,}56984\approx0{,}5698$; ngưỡng $2(0{,}27992-0{,}16443)=0{,}23098\approx0{,}2310$.

**V5. Ví dụ 04.4** (3-04). Trọng số tại $x_0=0{,}5$: bậc $0$: $(\tfrac13,\tfrac13,\tfrac13)$; bậc $1$: $(\tfrac1{12},\tfrac13,\tfrac7{12})$; bậc $2$: $(-\tfrac18,\tfrac34,\tfrac38)$ (tổng $1$). $\bar f(x_0)=w_1+w_3$: $\tfrac23$; $\tfrac23$; $\tfrac14$. Độ chệch bình phương $\tfrac{25}{144}\approx0{,}1736$; $0{,}1736$; $0$. Phương sai $\sigma^2\sum_iw_i^2$: $\tfrac13\sigma^2\approx0{,}3333\sigma^2$; $\tfrac{66}{144}\sigma^2=\tfrac{11}{24}\sigma^2\approx0{,}4583\sigma^2$; $\tfrac{46}{64}\sigma^2=0{,}71875\sigma^2$. Tổng (không kể $\sigma^2$): $\sigma^2=1$: $0{,}5069$; $0{,}6319$; $0{,}7188$ (bậc $0$ tốt nhất); $\sigma^2=0{,}1$: $0{,}2069$; $0{,}2194$; $0{,}0719$ (bậc $2$ tốt nhất).

**V6. Ví dụ 04.5** (3-05). $m=4$, $\sigma^2=1$: áp dụng sai $0+0{,}25+1=1{,}25$; đúng $\sigma^2(m-1)/m=0{,}75$; hiệu $0{,}5=2\sigma^2/m$.

**V7. Ví dụ 04.6** (ghi chú diễn giả 3-06). $\eta(x)=0{,}9$, $\sigma^2(x)=0{,}09$. $A$: lỗi $0{,}4\cdot0{,}1+0{,}6\cdot0{,}9=0{,}58=0{,}25+0{,}24+0{,}09$; $B$: $0{,}81+0+0{,}09=0{,}90$.

**V8. Nhận xét 04.7** (3-06). $Y=\pm1$, $f^*=0$, $\sigma^2=1$; nghiệm ERM $\operatorname{sign}(\bar Y)$, $\bar f=0$, phương sai $1$; $\mathbb E(c-Y)^2=1-0+1=2$; sai số xấp xỉ $2-1=1$.

**V9. Bài tập 04.2(d)** (3-07; số của `exercises.md`). $m=4$, $\mu=1$, $\sigma^2=1$; sai số xấp xỉ của lớp hàm hằng $\sigma^2-\sigma^2=0$; độ chệch của $0{,}8\bar Y$: $(0{,}8-1)\mu=-0{,}2$. Phần (b) (ghi chú diễn giả): lỗi $1{,}25$; $1{,}20$; $1{,}3125$; $2{,}00$ tại $\gamma=1;\ 0{,}8;\ 0{,}5;\ 0$; $\gamma^*=1/(1+0{,}25)=0{,}8$.

**V10. Bảng số hạng phạt** (Ví dụ 04.7, 04.9; Phụ lục C; 4-04, 4-07, hình F2). $m=10^4$, $\delta=0{,}05$, $q_k=6/(\pi^2k^2)$, $d_k=k+1$; $\ln(\pi^2/6)=0{,}4977$; $\ln(1/q_3)=2{,}695$; $\ln(1/q_{10})=5{,}103$.

| $k$ | $L_S(\hat h_k)$ | $\mathrm{pen}_k$ | tổng | không chia | tỉ số |
|---|---|---|---|---|---|
| $1$ | $0{,}300$ | $0{,}1423$ | $0{,}4423$ | $0{,}1409$ | $1{,}010$ |
| $2$ | $0{,}210$ | $0{,}1690$ | $0{,}3790$ | $0{,}1644$ | $1{,}027$ |
| $3$ | $0{,}175$ | $0{,}1900$ | $0{,}3650$ | $0{,}1843$ | $1{,}031$ |
| $4$ | $0{,}170$ | $0{,}2081$ | $0{,}3781$ | $0{,}2017$ | $1{,}032$ |
| $5$ | $0{,}166$ | $0{,}2241$ | $0{,}3901$ | $0{,}2174$ | $1{,}031$ |
| $6$ | $0{,}163$ | $0{,}2386$ | $0{,}4016$ | $0{,}2317$ | $1{,}030$ |
| $7$ | $0{,}160$ | $0{,}2520$ | $0{,}4120$ | $0{,}2449$ | $1{,}029$ |
| $8$ | $0{,}158$ | $0{,}2644$ | $0{,}4224$ | $0{,}2573$ | $1{,}028$ |
| $9$ | $0{,}156$ | $0{,}2761$ | $0{,}4321$ | $0{,}2689$ | $1{,}027$ |
| $10$ | $0{,}155$ | $0{,}2871$ | $0{,}4421$ | $0{,}2799$ | $1{,}026$ |

Tổng chưa làm tròn tại $k=3$: $0{,}365044$ (ghi chú: $0{,}36504$, làm tròn lên $0{,}3651$ cho cận trên tin cậy). ERM trên $\mathcal H_{10}$: $0{,}155+0{,}279919=0{,}434919$ (ghi chú: $0{,}43492$, làm tròn lên $0{,}4350$). Biết trước $k=3$: $0{,}175+0{,}184284=0{,}359284$ ($0{,}3593$); hiệu $0{,}36504-0{,}35928=0{,}00576\approx0{,}0058$. Tổng $k=4$ trừ $k=3$: $0{,}01304\approx0{,}0130$. $2\,\mathrm{pen}_2=0{,}3379\approx0{,}338$, $2\,\mathrm{pen}_{10}=0{,}5742\approx0{,}574$, so với $0{,}329$, $0{,}560$.

**V11. Ví dụ 04.8** (4-05). $\sqrt{\ln40/20}=0{,}42947$; biến cố hỏng một lớp $2\cdot2^{-10}=2^{-9}$; $1-(1-2^{-9})^{1000}=0{,}85844$; $1-(1-2^{-9})^{5000}=0{,}99994$; $1-(1-2^{-10})^{1000}=0{,}62358$; chia đều: $\sqrt{\ln40\,000/20}=0{,}72790>\tfrac12$.

**V12. Ví dụ 04.10** (4-11). $\sqrt{\ln80/2000}=0{,}046808\approx0{,}04681$; làm tròn lên $0{,}0469$.

**V13. Bài tập 04.4(b)** (4-12; số của `exercises.md`). $q_k=1/10$: $\ln800=6{,}685$; tổng tại $k=1,\ldots,5$: $0{,}4473$; $0{,}3799$; $0{,}3642$; $0{,}3762$; $0{,}3875$ (với $k\ge5$ tăng). $q_k=2^{-k}$: $0{,}4428$; $0{,}3778$; $0{,}3637$; $0{,}3771$; $0{,}3896$. Cả hai chọn $k=3$.

**V14. Hệ quả 04.15, phần đọc bằng số** (5-03; Phụ lục B). Chia đôi khoảng trên $\varphi(m)=\tfrac{32}m(4\ln\tfrac{em}2+c(m))\le0{,}01$: $172\,279$ ($c=\ln80$); $181\,575$ ($c=\ln80+\ln(1/q_3)$); $213\,317$ ($c=\ln(4m)+\ln(1/q_3)$, $c\approx16{,}35$). Tỉ lệ $181\,575/172\,279-1=5{,}40\%$; $213\,317/181\,575-1=17{,}48\%$; $1/213\,317=4{,}69\cdot10^{-6}$.

**V15. Ví dụ 04.12** (6-03, hình F3). $\ln400=5{,}9915$; $\sqrt{5{,}9915/2000}=0{,}05473$; cận $0{,}10947\approx0{,}1095$. $m_v=200;\ 500;\ 1000;\ 2000;\ 5000$: $0{,}2448;\ 0{,}1548;\ 0{,}1095;\ 0{,}0774;\ 0{,}0490$. Đủ: $1198{,}29\to1199$ ($\epsilon=0{,}1$); $4793{,}17\to4794$ ($\epsilon=0{,}05$). $K=10^6$: $2\sqrt{\ln(4\cdot10^7)/2000}=0{,}18711\approx0{,}1871$.

**V16. Nhận xét 04.18** (6-04). $K=15$, $m_v=1000$, $B=1$: $4\cdot2\sqrt{\ln600/2000}=0{,}45244\approx0{,}4524$.

**V17. Bài tập 04.5(a)** (6-05; số của `exercises.md`). $L_V(g_{11})=0$, $L_D(g_{11})=0{,}8$, $L_D(g_1)=0{,}2$: hiệu $\ge0{,}6$; $2\sqrt{\ln440/2000}=0{,}11033\approx0{,}1103$.

**V18. Bài tập 04.7(c)** (7-03; số của `exercises.md`). $\delta'=0{,}025$, $\ln160=5{,}075$; $d=4$: $\sqrt{8(38{,}069+5{,}075)/10^4}=0{,}18578\approx0{,}1858$; $d=10$: $0{,}26994\approx0{,}2699$; ngưỡng $0{,}2699-0{,}1858=0{,}0841$; $2\,\mathrm{pen}$: $0{,}3716$, $0{,}5399$.

**V19. Câu hỏi cuối buổi §11** (7-04). $\operatorname{opt}_S(\tilde h)=0{,}185-0{,}175=0{,}010$; mục tiêu tại $(3,\tilde h)$: $0{,}185+0{,}1900=0{,}3750$ (chưa làm tròn $0{,}37504$); $\tau=0{,}3750-0{,}3650=0{,}010$.

**V20. Câu ôn nhanh** (ghi chú diễn giả 1-02, 3-03, 4-03). $K=10$, $m=1000$, $\delta=0{,}05$: $r_m=\sqrt{\ln400/2000}=0{,}05473$; $0{,}05\sum_{k\ge1}2^{-k}=0{,}05$.

## 6. Danh sách trang

Mỗi mục: ID, tiêu đề, loại, thời lượng; **Mặt trang** (các dòng dự kiến, theo thứ tự; `[f]` là fragment; `$$…$$` là công thức hiển thị, tính một dòng); **Ghi chú diễn giả** (ý chính, 40–150 âm tiết, đến ~250 cho trang ý tưởng chứng minh; viết cho giảng viên và người học; không mã trang, mã ví dụ của storyboard, câu quy trình hay nguồn gốc; luôn kết thúc bằng dòng `note-source`); **Lý do / nối**; **Mục tiêu / nguồn**. Câu trên mặt trang là bản dự kiến đã tự kiểm theo `no-ai-slop` (chế độ Edit) và `eval.md`; người viết deck có thể rút gọn, không thêm khẳng định.

Quy ước chung cho người viết deck:
- Trang kết quả: "Giả thiết:" và "Bảo đảm:" (nhãn của ghi chú), trích số khối của ghi chú một lần.
- Trang tổng quan (bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm") viết bằng lời, không kí hiệu, không tiếng Anh. Lần đầu một thuật ngữ trên trang nội dung có tiếng Anh trong ngoặc (bảng mục 10).
- Mọi kí hiệu trên mặt trang đã có ở trang trước hoặc có dòng "Nhắc lại:" (bảng đối chiếu mục 12 ghi chỗ đưa vào).
- Các cụm "Dùng khi …", "Bỏ …", "Giá …" viết chữ thường, không in đậm như nhãn; chỉ dùng nhãn của danh sách hợp lệ.
- Số thập phân dùng dấu phẩy KaTeX `0{,}2`; dãy số ngăn bằng `;\ `; số từ năm chữ số tách nhóm bằng `\,`.
- Mỗi trang ví dụ mở bằng dữ kiện dạng danh sách, không câu dẫn. "Diễn giải:" chỉ dùng số có trên chính trang đó.
- Trang ý tưởng chứng minh: lộ trình 3–5 bước, bất đẳng thức hoặc mẹo then chốt, chỗ giả thiết vào, bỏ giả thiết thì hỏng ở đâu; không chép chứng minh đầy đủ của ghi chú.
- Không `\text{}` chứa tiếng Việt trong KaTeX. Trong ghi chú diễn giả, không ghi "mới", "dựng", "V6", "mục 5".
- Công thức một dòng khi vừa khung; chỉ ngắt bằng `aligned` khi tràn ở 390 px (đo trong trình duyệt). Ở chế độ đọc hẹp, công thức rộng cuộn ngang tại chỗ.

### Mạch 1. Mở đầu (6 trang, 8 phút)

#### `1-01` Phân tích sai số, tối thiểu hóa rủi ro cấu trúc và chọn mô hình — bìa, điểm vào mạch 1 · 1 phút
- **Mặt trang:** h1 tên bài; h3 "Bài 04"; luận điểm (mục 2, bằng lời); "Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1"; "Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN".
- **Ghi chú diễn giả:** Bài 02 và Bài 03 chặn rủi ro vượt mức của ERM so với mức tốt nhất của một lớp cố định. Bài này đổi câu hỏi: với một cỡ mẫu cho trước, chọn lớp nào trong một dãy lớp. Luận điểm có ba phần. Rủi ro của hàm học được so với một mức tham chiếu bằng sai số xấp xỉ cộng sai số ước lượng; phần thứ nhất không tăng khi lớp lớn dần nhưng không quan sát được, phần thứ hai có cận tăng theo lớp và tính được. Chia xác suất thất bại cho các lớp biến cận đó thành số hạng phạt cộng vào rủi ro thực nghiệm. Một mẫu xác thực độc lập cho cách chọn thứ hai, với giá theo lôgarit của số ứng viên. Nguồn: ghi chú Bài 04, đoạn mở đầu, §4, §6, §8, §9.
- **Lý do / nối:** luận điểm cả bài → tiên quyết.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu, §9.

#### `1-02` Tiên quyết và quy ước — mở đầu · 1,5 phút
- **Mặt trang:**
  - **Nhắc lại:** (T1) độc lập cùng phân bố; (T2) $\ell\ge0$ đo được; (T3) $\ell\in[0,1]$.
  - (T4), (T5) lớp hữu hạn, lớp bất kì chọn trước; (M) lớp con đếm được xấp xỉ theo từng điểm.
  - $\epsilon$-đại diện: $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\le\epsilon$.
  - Mọi $D$, xác suất $\ge1-\delta$: $S$ là $r_m$-đại diện khi (T1), (T3), (T4) (Định lý 02.14(a));
  - $\rho_m$-đại diện khi hàm lỗi 0–1, (T1), (T5), (M) (Định lý 03.15(a)).
- **Ghi chú diễn giả:** Hai bán kính: $r_m=\sqrt{\ln(2\lvert\mathcal H\rvert/\delta)/(2m)}$ cho lớp hữu hạn, và bán kính VC $\rho_m=\sqrt{8\ln(4\Pi_{\mathcal H}(2m)/\delta)/m}$, với $\rho_m^2\le\tfrac8m\big(d\ln\tfrac{2em}d+\ln\tfrac4\delta\big)$ khi $1\le d\le m$ (Định lý 03.15(b)). Hai bất đẳng thức cùng một dạng: xác suất để tập huấn luyện đại diện ít nhất $1-\delta$ cho mọi phân bố. Từ Bài 01 bài dùng hai mức chính xác của bộ giải (O1), (O2), rủi ro Bayes của ví dụ sàng lọc và học PAC bất khả diễn; từ Bài 02, bất đẳng thức hợp dạng đếm được. Câu ôn nhanh 1: với $K=10$, $m=1000$, $\delta=0{,}05$, $r_m=\sqrt{\ln400/2000}\approx0{,}0547$; số này trở lại ở phần mẫu xác thực. Nguồn: ghi chú Bài 04, Kiến thức tiên quyết, Câu hỏi ôn nhanh; §2.
- **Lý do / nối:** các giả thiết và hai kết quả của Bài 02–03 dùng trên mặt trang được nhắc lại ở đây → mục tiêu.
- **Mục tiêu / nguồn:** 1, 3; Kiến thức tiên quyết, §2.

#### `1-03` Mục tiêu — mở đầu · 1 phút
- **Mặt trang (danh sách đánh số, bằng lời, không kí hiệu; trần 80):**
  1. Viết rủi ro thành sai số xấp xỉ cộng sai số ước lượng; chặn bằng ba số hạng.
  2. Chứng minh phân tích độ chệch–phương sai; phân biệt độ chệch với sai số xấp xỉ.
  3. Chia xác suất thất bại, chứng minh bất đẳng thức oracle, chọn lớp từ một bảng.
  4. Định nghĩa học không đều; nêu lớp học được không đều mà không học được PAC.
  5. Tính cận của mẫu xác thực; dựng phản ví dụ khi bỏ giả thiết.
- **Ghi chú diễn giả:** Ở mục tiêu 1, ba số hạng là sai số xấp xỉ, một số hạng thống kê theo cỡ mẫu và sai số tối ưu thực nghiệm của bộ giải. Ở mục tiêu 4, lớp đó học được không đều nhưng không học được PAC bất khả diễn, và mọi lớp học được PAC bất khả diễn với hàm lỗi bị chặn cũng học được không đều. Nguồn: ghi chú Bài 04, Mục tiêu học tập, §10.
- **Lý do / nối:** tiêu chí kiểm tra → nội dung.
- **Mục tiêu / nguồn:** tất cả; Mục tiêu học tập.

#### `1-04` Nội dung — mở đầu · 0,5 phút
- **Mặt trang:** `ol start="2"` với liên kết `#/2`…`#/7`: 2. Phân tích sai số; 3. Độ chệch và phương sai; 4. Chia xác suất thất bại và tối thiểu hóa rủi ro cấu trúc; 5. Học không đều; 6. Chọn mô hình bằng mẫu xác thực; 7. Tổng kết. Dòng đọc trước: "Đọc trước: UML §5.2, §7.1."
- **Ghi chú diễn giả:** Mạch 2 tách rủi ro theo nguồn và chặn nó bằng ba số hạng; mạch 3 xét hàm lỗi bình phương, nơi lỗi trên nhãn mới là một đẳng thức theo kì vọng; mạch 4 biến cận đều của từng lớp thành một quy tắc chọn lớp có bảo đảm; mạch 5 dùng quy tắc đó cho một lớp hợp đếm được; mạch 6 chọn bằng một mẫu dữ liệu mới. Nguồn: ghi chú Bài 04; §12.
- **Lý do / nối:** bản đồ mạch → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §12.

#### `1-05` Vấn đề trung tâm — mở đầu · 1 phút
- **Mặt trang:** một hộp `div.box`: "**Câu hỏi:** với cỡ mẫu cho trước, chọn lớp giả thuyết nào trong một dãy lớp để hàm học được có rủi ro kì vọng nhỏ?" (26 âm tiết kể cả nhãn).
- **Ghi chú diễn giả** (câu trả lời theo mạch, không trên mặt trang): (2) rủi ro của hàm học được bằng sai số xấp xỉ cộng sai số ước lượng, và sai số ước lượng bị chặn bởi $2r$ cộng sai số tối ưu thực nghiệm; chỉ phần thống kê tính được; (3) với hàm lỗi bình phương, lỗi trên nhãn mới là độ chệch bình phương cộng phương sai cộng nhiễu, và bậc tốt nhất phụ thuộc mức nhiễu chưa biết; (4) chia xác suất thất bại theo trọng số cho số hạng phạt, và SRM có bất đẳng thức oracle; trong ví dụ, SRM chọn ba chỉ số đo; (5) chọn xác suất thất bại $1/m$ cho một thuật toán học không đều; (6) một mẫu xác thực độc lập chọn trong $K$ ứng viên với giá theo $\sqrt{\ln K/m_v}$. Nguồn: ghi chú Bài 04, đoạn mở đầu, §4–§9.
- **Lý do / nối:** một vấn đề cốt lõi → hai câu hỏi cụ thể.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu.

#### `1-06` Ví dụ: chọn bậc đa thức và chọn số chỉ số đo — ví dụ dẫn nhập · 3 phút
- **Mặt trang:**
  - $16$ quan sát $(x_i,y_i)$, các $x_i\in\mathbb R$ đôi một khác nhau; khớp đa thức bậc $1$, $3$, $15$.
  - Lớp bậc thấp nằm trong lớp bậc cao; bậc $15$ qua cả $16$ điểm: rủi ro thực nghiệm bằng $0$.
  - Bài 03, $m=10^4$, hàm phân lớp tuyến tính trên $k$ chỉ số đo: cận rủi ro vượt mức $0{,}329$ ($k=2$), $0{,}560$ ($k=10$).
  - **Câu hỏi:** bậc nào dự đoán tốt trên nhãn mới? Dùng bao nhiêu chỉ số đo?
- **Ghi chú diễn giả:** Vì lớp bậc thấp nằm trong lớp bậc cao, rủi ro thực nghiệm không tăng theo bậc. Trên một dãy lớp lồng nhau, lớp lớn nhất luôn đạt rủi ro thực nghiệm nhỏ nhất, với mọi cỡ mẫu, nên quy tắc chọn theo rủi ro thực nghiệm không dùng đến cỡ mẫu. Cận cho rủi ro vượt mức so với lớp lại tăng theo độ phức tạp của lớp: hai số $0{,}329$ và $0{,}560$ là $2\rho_m$ với chiều VC $3$ và $11$, $\delta=0{,}05$. Quy tắc cần cộng vào rủi ro thực nghiệm một số hạng phạt rút ra từ chính cận đó. Với bậc đa thức có một khó khăn riêng: hàm lỗi bình phương không bị chặn, nên các cận của Bài 02–03, viết cho hàm lỗi trong $[0,1]$, không áp dụng trực tiếp. Nguồn: ghi chú Bài 04, Câu hỏi mở đầu và hai đoạn sau; §11 của Bài 03.
- **Lý do / nối:** ví dụ dẫn nhập trước mọi định nghĩa; hai ví dụ xuyên suốt của bài → tiêu đề mạch 2.
- **Mục tiêu / nguồn:** 1, 3, 5; Câu hỏi mở đầu.

### Mạch 2. Phân tích sai số (9 trang, 22 phút)

#### `2-00` 2. Phân tích sai số — tiêu đề mạch, điểm vào mạch 2 · 0,5 phút
- **Mặt trang:** "2."; h2 "Phân tích sai số"; `p.strand-lead` (bảng mạch, 23 âm tiết); `p.strand-keys`: "rủi ro tham chiếu · sai số xấp xỉ · sai số ước lượng · sai số tối ưu thực nghiệm".
- **Ghi chú diễn giả:** Hệ quả 02.16 và 03.16 so rủi ro của ERM với mức tốt nhất của một lớp cố định. Khi lớp thay đổi, mức đó thay đổi theo, nên mạch này đặt một mức tham chiếu chung, tách rủi ro thành phần do lớp và phần do mẫu, rồi tách tiếp phần do mẫu thành số hạng thống kê và sai số của bộ giải. Kết quả là một cận ba thành phần, và phép so hai lớp trên cận đó cho thấy vì sao cần chia xác suất thất bại giữa các lớp. Nguồn: ghi chú Bài 04, §1–§4.
- **Lý do / nối:** mạch 1 → thiết lập.
- **Mục tiêu / nguồn:** 1; §1–§4.

#### `2-01` Họ lớp và đầu ra của bộ giải — định nghĩa (khung) · 2 phút
- **Mặt trang:**
  - Họ lớp $\mathcal H_1,\mathcal H_2,\ldots$ hữu hạn hoặc đếm được, chọn trước, không nhất thiết lồng nhau.
  - Bộ giải (solver) trả về $\tilde h=\tilde h(S)\in\mathcal H$, có thể khác nghiệm tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM).
  - Mục tiêu: $L_D(\tilde h)$ nhỏ, so với $\inf_{h\in\mathcal H}L_D(h)$ hoặc một mức chung cho mọi lớp.
  - Cố định: $D$, các lớp, $\delta$, $L_D(h)$. Ngẫu nhiên theo $S$: $L_S(h)$, lớp và hàm được chọn.
- **Ghi chú diễn giả:** Bài toán giữ tám thành phần của Bài 01 với hai thay đổi: một họ lớp thay cho một lớp, và độ chính xác của bộ giải được tính vào tài nguyên, cùng cỡ mẫu $m$ và cỡ mẫu xác thực. Bộ giải là thủ tục tối ưu trả về một giả thuyết. Có bốn mức so sánh: rủi ro tham chiếu chọn trước, mức tốt nhất của từng lớp, mức tốt nhất có phạt, và ứng viên tốt nhất khi chọn bằng mẫu xác thực. Bài dùng ba loại hàm lỗi: hàm lỗi trong $[0,1]$ như hàm lỗi 0–1, hàm lỗi bình phương khi phân tích độ chệch–phương sai, và hàm lỗi bình phương với nhãn và dự đoán bị chặn khi chọn mô hình bằng mẫu xác thực. Trọng số và số hạng phạt của các lớp cũng cố định; các ứng viên và rủi ro trên mẫu xác thực là ngẫu nhiên. Nguồn: ghi chú Bài 04, §1 (tám thành phần, bảng nguồn ngẫu nhiên), §2.
- **Lý do / nối:** khung chung trước mọi kết quả; phân biệt cố định và ngẫu nhiên → hai ví dụ xuyên suốt.
- **Mục tiêu / nguồn:** 1; §1, §2.

#### `2-02` Ví dụ: ba bậc đa thức và số chỉ số đo — ví dụ (hai ví dụ xuyên suốt) · 2,5 phút
- **Mặt trang** (`grid2`, hai thẻ `card`):
  - Thẻ trái, **Ví dụ 04.1.** $x_1=-1$, $x_2=0$, $x_3=1$ cố định: thiết kế cố định (fixed design); $Y_i=x_i^2+\zeta_i$, nhiễu độc lập, kì vọng $0$, phương sai $\sigma^2$.
  - $\hat f^{(j)}$: nghiệm ERM trên $\mathcal P_j$ với hàm lỗi bình phương (squared loss), $j=0,1,2$; $\mathcal P_0\subset\mathcal P_1\subset\mathcal P_2$.
  - Bậc $2$ nội suy ba điểm: $L_S(\hat f^{(2)})=0$ trên mọi tập huấn luyện.
  - Thẻ phải, **Ứng dụng.** $x\in\mathbb R^{10}$; $\mathcal H_k$ gồm $x\mapsto\mathbb 1[w_1x_1+\cdots+w_kx_k+b\ge0]$, $k=1,\ldots,10$.
  - $\mathcal H_k\subset\mathcal H_{k+1}$; chiều VC $d_k=k+1$; mỗi $\mathcal H_k$ thỏa (M).
  - **Câu hỏi:** với $m=10^4$ và $\delta=0{,}05$, dùng bao nhiêu chỉ số đo?
- **Ghi chú diễn giả:** Ví dụ thứ nhất là bản thu nhỏ của câu hỏi mở đầu: chỉ các nhãn là ngẫu nhiên, và $\mathcal P_j$ là lớp đa thức một biến bậc không quá $j$. Vì $\hat f^{(j)}\in\mathcal P_{j+1}$, rủi ro thực nghiệm không tăng theo bậc; ma trận Vandermonde $3\times3$ của ba hoành độ khả nghịch, nên bậc $2$ nội suy và rủi ro thực nghiệm chọn bậc $2$ với mọi $\sigma^2$. Ở ví dụ thứ hai, các chỉ số đo xếp theo một thứ tự cố định trước khi lấy mẫu; đặt $w_{k+1}=0$ cho bao hàm $\mathcal H_k\subset\mathcal H_{k+1}$, và $\mathcal H_{10}$ là lớp $\mathcal H^{10}_{\mathrm{aff}}$ của Bài 03. Chiều VC $d_k=k+1$ theo Mệnh đề 03.9 qua phép chiếu lên $k$ tọa độ đầu, chứng minh bằng kỹ thuật cận dưới và cận trên của Bài 03; điều kiện (M) thỏa với lớp con gồm các tham số hữu tỉ. Nguồn: ghi chú Bài 04, §3 (Ví dụ 04.1, khối ứng dụng); Phụ lục C (chiều VC).
- **Lý do / nối:** hai ví dụ xuyên suốt xuất hiện cùng lúc, cả hai có lớp lồng nhau và rủi ro thực nghiệm không tăng → cần tách rủi ro theo nguồn.
- **Mục tiêu / nguồn:** 1, 2, 3; Ví dụ 04.1, §3.

#### `2-03` Rủi ro tham chiếu, sai số xấp xỉ và sai số ước lượng — định nghĩa, ví dụ · 3 phút
- **Mặt trang** (`grid2`: chữ bên trái, hình F1 bên phải):
  - Lớp thay đổi thì $\inf_{h\in\mathcal H}L_D(h)$ đổi theo; cần một mức chung cho mọi lớp.
  - **Định nghĩa 04.1.** $\ell$ thỏa (T2), $L_D(h)<\infty$ trên $\mathcal H$. Rủi ro tham chiếu (reference risk): số $L^*\le\inf_{h\in\mathcal H}L_D(h)$ chọn trước, không phụ thuộc $S$.
  - Sai số xấp xỉ (approximation error) $\inf_{h\in\mathcal H}L_D(h)-L^*$ và sai số ước lượng (estimation error) $L_D(h)-\inf_{h'\in\mathcal H}L_D(h')$ cộng lại:
  - $$L_D(h)-L^*=\Big[\inf_{h'\in\mathcal H}L_D(h')-L^*\Big]+\Big[L_D(h)-\inf_{h'\in\mathcal H}L_D(h')\Big]$$
  - **Ví dụ.** Sàng lọc, $L^*=0{,}18$: sai số xấp xỉ $0{,}22-0{,}18=0{,}04$; sai số ước lượng của $h_2$: $0{,}32-0{,}22=0{,}10$.
  - {{hình F1 bên phải}}
- **Ghi chú diễn giả:** Ví dụ về rủi ro tham chiếu: rủi ro Bayes trong phân lớp, hoặc cận dưới đúng của $L_D$ trên một lớp lớn hơn chứa $\mathcal H$. Với $L^*$ là rủi ro Bayes, đẳng thức là đẳng thức sau Định nghĩa 01.24. Sai số xấp xỉ là một số tất định, phụ thuộc $D$, $\mathcal H$ và $L^*$; với cùng $L^*$ nó giảm hoặc giữ nguyên khi lớp lớn hơn, vì cận dưới đúng trên một tập lớn hơn không lớn hơn cận dưới đúng trên tập con. Với $h=A(S)$, sai số ước lượng là một biến ngẫu nhiên theo $S$; nó là rủi ro vượt mức so với lớp. Đọc hình: trên lớp sáu hàm ngưỡng, rủi ro tham chiếu $0{,}18$ là rủi ro Bayes, mức tốt nhất của lớp $0{,}22$ đạt tại $h_3$, và $h_2$ có rủi ro $0{,}32$; trên lớp mọi hàm của năm mức đo, hàm phân lớp tối ưu Bayes $\mathbb 1[x\in\{3,5\}]$ thuộc lớp và sai số xấp xỉ bằng $0$. Số $0{,}25$ không phải một rủi ro tham chiếu cho lớp sáu hàm ngưỡng: nó lớn hơn $0{,}22$ và cho "sai số xấp xỉ" $-0{,}03$. Định nghĩa chỉ dùng (T2) và $L_D<\infty$, nên áp dụng được cho hàm lỗi bình phương. Nguồn: ghi chú Bài 04, §4, Định nghĩa 04.1 và đoạn sau, Ví dụ 04.2.
- **Lý do / nối:** định nghĩa then chốt của mạch, mở bằng câu nêu nhu cầu so sánh nhiều lớp, ví dụ số ngay trên trang → nguồn thứ hai của sai số ước lượng.
- **Mục tiêu / nguồn:** 1; Định nghĩa 04.1, Ví dụ 04.2.

#### `2-04` Sai số tối ưu thực nghiệm — định nghĩa, lưu ý · 2,5 phút
- **Mặt trang:**
  - Sai số ước lượng của $\tilde h$ gộp hai nguồn: cỡ mẫu hữu hạn và bộ giải không tìm đúng nghiệm ERM.
  - **Định nghĩa 04.2.** Với $\ell\ge0$, tập huấn luyện $s$, $\tilde h\in\mathcal H$, sai số tối ưu thực nghiệm (empirical optimization error) là
  - $$\operatorname{opt}_s(\tilde h)=L_s(\tilde h)-\inf_{h\in\mathcal H}L_s(h)\ge0.$$
  - **Nhắc lại:** (O2) $\epsilon_{\mathrm{opt}}$-ERM: $L_S(\hat h)\le\inf_{h\in\mathcal H}L_S(h)+\epsilon_{\mathrm{opt}}$, tức $\operatorname{opt}_S\le\epsilon_{\mathrm{opt}}$ trên mọi tập huấn luyện.
  - **Lưu ý:** $L_D(\tilde h)-L_D(\hat h)$ có thể âm: $S=((1,0),(2,1))$, nghiệm ERM duy nhất $h_2$, $\tilde h=h_3$: $0{,}22-0{,}32=-0{,}10$, còn $\operatorname{opt}_S(h_3)=\tfrac12$.
- **Ghi chú diễn giả:** Đại lượng $\operatorname{opt}_S(\tilde h)$ tính được từ tập huấn luyện mà không cần biết $D$, nhưng phân bố của nó theo $S$ phụ thuộc $D$; nó không âm kể cả khi cận dưới đúng không đạt. Ví dụ: lớp $\mathcal H_+$ của Ví dụ 01.7 trên $S=((1,0))$ có cận dưới đúng $0$ không đạt, và $\operatorname{opt}_S(h_w)=w^2$. Ở dòng lưu ý, dưới $D_\eta$, chỉ $h_2$ phân lớp đúng cả hai quan sát; $h_3$ sai trên $(2,1)$. Hiệu theo rủi ro kì vọng còn phụ thuộc nghiệm ERM được chọn làm mốc: trên $S_\eta$ của Ví dụ 01.6 có nghiệm ERM với rủi ro $0{,}32$ và nghiệm khác với $0{,}28$. Vì vậy sai số của bộ giải được đo bằng $\operatorname{opt}_S$, một đại lượng thực nghiệm và không âm. Nguồn: ghi chú Bài 04, §4, Định nghĩa 04.2 và đoạn sau, Nhận xét 04.4.
- **Lý do / nối:** nguồn sai số thứ ba trước cận → cận ba thành phần.
- **Mục tiêu / nguồn:** 1; Định nghĩa 04.2, Nhận xét 04.4.

#### `2-05` Cận ba thành phần — trực quan, kết quả · 3 phút
- **Mặt trang:**
  - **Trực quan.** Sai số xấp xỉ: tất định, không quan sát được; $2r$: cỡ mẫu; $\operatorname{opt}_S(\tilde h)$: bộ giải.
  - **Mệnh đề 04.3.** **Giả thiết:** (T2), (T3); $L^*$ như Định nghĩa 04.1; $\tilde h=\tilde h(S)\in\mathcal H$ đo được, bất kì; $r>0$.
  - **Bảo đảm:** (a) nếu $S$ là $r$-đại diện,
  - $$L_D(\tilde h)-L^*\le\Big[\inf_{h\in\mathcal H}L_D(h)-L^*\Big]+2r+\operatorname{opt}_S(\tilde h).$$
  - (b) Mọi $D$, xác suất $\ge1-\delta$ theo $S\sim D^m$: (a) đồng thời cho mọi quy tắc khi
  - (T1), (T4), $r=r_m$; hoặc hàm lỗi 0–1, (T1), (T5), (M), $r=\rho_m$.
- **Ghi chú diễn giả:** Đầu ra $\tilde h$ không cần là nghiệm ERM; mọi quy tắc đo được đều được phép. Ba số hạng là sai số xấp xỉ (tất định), cận thống kê $2r$ của lớp và đại lượng thực nghiệm $\operatorname{opt}_S(\tilde h)$ của bộ giải. Cận $2r$ phụ thuộc $m$, $\delta$ và số phần tử của lớp hoặc hàm tăng trưởng. Phần (a) là một khẳng định tất định trên biến cố đại diện; phần (b) là bảo đảm với xác suất cao, và vì biến cố không phụ thuộc quy tắc, cận đúng đồng thời cho mọi quy tắc trên cùng một tập huấn luyện. Sai số ước lượng gộp hiệu ứng thống kê và hiệu ứng tối ưu, và đẳng thức của Định nghĩa 04.1 không tách được nó thành hai phần; chỉ cận tách được. Nguồn: ghi chú Bài 04, §4, Mệnh đề 04.3, Nhận xét 04.4.
- **Lý do / nối:** kết quả chính đầu tiên, trực quan trên cùng trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 1; Mệnh đề 04.3.

#### `2-06` Ý tưởng chứng minh: cận ba thành phần — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  - **Nhắc lại:** bước tất định trên biến cố đại diện (Bài 02).
  - Khi $S$ là $r$-đại diện, với mọi $h\in\mathcal H$:
  - $$L_D(\tilde h)\le L_S(\tilde h)+r=\inf_{h'}L_S(h')+\operatorname{opt}_S(\tilde h)+r\le L_S(h)+\operatorname{opt}_S(\tilde h)+r\le L_D(h)+2r+\operatorname{opt}_S(\tilde h)$$
  - Thứ nhất: đại diện tại $\tilde h$, cần cận đều vì $\tilde h$ chọn theo $S$; cuối: đại diện tại $h$ cố định.
  - Lấy $\inf_h$, trừ $L^*$: (a). Phần (b): giả thiết thống kê chỉ vào xác suất của biến cố đại diện.
  - **Kết luận:** $L^*=\inf_{h\in\mathcal H}L_D(h)$, $\operatorname{opt}_S\le\epsilon_{\mathrm{opt}}$: Hệ quả 02.16(b), 03.16(b).
- **Ghi chú diễn giả** (~180 âm tiết): Lộ trình giống Bước 1 của chứng minh Hệ quả 03.16, với một số hạng mới. Đọc chuỗi từ trái sang: bất đẳng thức thứ nhất dùng tính đại diện tại $\tilde h$; đẳng thức là Định nghĩa 04.2; bất đẳng thức thứ hai dùng định nghĩa của cận dưới đúng, $\inf_{h'}L_S(h')\le L_S(h)$; bất đẳng thức thứ ba dùng tính đại diện tại $h$. Vế trái không phụ thuộc $h$, nên lấy được cận dưới đúng theo $h\in\mathcal H$ ở vế phải. Bất đẳng thức then chốt là tính đại diện, dùng hai lần; ở lần đầu nó phải đúng cho một hàm được chọn sau khi xem tập huấn luyện, nên một cận cho từng $h$ cố định là không đủ. Các giả thiết thống kê không xuất hiện ở phần (a); chúng chỉ cho xác suất của biến cố "$S$ là $r$-đại diện", qua Định lý 02.14(a) hoặc 03.15(a). Cận có hai số hạng riêng: $2r$ do cỡ mẫu hữu hạn và $\operatorname{opt}_S$ do bộ giải; khi bộ giải chính xác, số hạng thứ hai bằng $0$. Nguồn: ghi chú Bài 04, chứng minh Mệnh đề 04.3.
- **Lý do / nối:** trang ý tưởng chứng minh riêng → áp dụng bằng số cho hai lớp của ứng dụng.
- **Mục tiêu / nguồn:** 1; chứng minh Mệnh đề 04.3.

#### `2-07` Ví dụ: cận ba thành phần cho hai lớp — ví dụ (Ví dụ 04.3), cận bằng số · 3 phút
- **Mặt trang:**
  - $\mathcal H_2$ ($d_2=3$), $\mathcal H_{10}$ ($d_{10}=11$); hàm lỗi 0–1; $m=10^4$, $\delta=0{,}05$; $L^*=L_D^{\mathrm{Bayes}}$ chưa biết.
  - Bộ giải thỏa (O2) với $\epsilon_{\mathrm{opt}}=0{,}01$; $a_2$, $a_{10}$ là sai số xấp xỉ của hai lớp.
  - Định lý 03.15(b): $\rho_m\le0{,}16443$ ($d=3$), $\rho_m\le0{,}27992$ ($d=11$). Mỗi cận đúng với xác suất $\ge0{,}95$:
  - $$L_D(\tilde h_2)-L_D^{\mathrm{Bayes}}\le a_2+0{,}3389,\qquad L_D(\tilde h_{10})-L_D^{\mathrm{Bayes}}\le a_{10}+0{,}5698$$
  - $a_{10}\le a_2$, cả hai chưa biết; cận của $\mathcal H_{10}$ nhỏ hơn khi và chỉ khi $a_2-a_{10}>0{,}2310$.
  - **Kết luận:** hai cận chưa đúng đồng thời; chọn lớp theo $S$ cần chia $\delta$ giữa các lớp.
- **Ghi chú diễn giả:** Vế phải của Định lý 03.15(b) bằng $\sqrt{\tfrac8m\big(d\ln\tfrac{2em}d+\ln\tfrac4\delta\big)}$; một mẫu $\rho_m$-đại diện cũng đại diện với mọi bán kính lớn hơn, nên dùng được vế phải này làm $r$. Hai số cuối là $2\cdot0{,}16443+0{,}01$ và $2\cdot0{,}27992+0{,}01$, đúng cho đầu ra $\tilde h_2$, $\tilde h_{10}$ của bộ giải trên hai lớp. Chỉ phần thống kê của hai cận tính được. Ngưỡng $0{,}2310$ bằng hai lần hiệu hai bán kính. Mười chỉ số đo chỉ cho cận tốt hơn khi tám chỉ số thêm làm sai số xấp xỉ giảm hơn $0{,}23$, một điều kiện không kiểm tra được từ dữ liệu. Mỗi cận đúng với xác suất $0{,}95$ cho một lớp chọn trước; một quy tắc chọn lớp theo tập huấn luyện cần hai cận đúng cùng lúc. Nguồn: ghi chú Bài 04, Ví dụ 04.3.
- **Lý do / nối:** áp dụng mệnh đề vào ví dụ xuyên suốt; giới hạn của phép so hai cận tạo nhu cầu cho mạch 4 → bài tập của cụm.
- **Mục tiêu / nguồn:** 1, 3; Ví dụ 04.3.

#### `2-08` Bài tập: ba số hạng trên tập huấn luyện sàng lọc — bài tập (Bài tập 04.1(b)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Nhắc lại:** $S_\eta=((1,0),(2,0),(2,1),(3,1),(4,0),(5,1))$, lớp sáu hàm ngưỡng $h_t$, hàm lỗi 0–1 (Ví dụ 01.5):
  - Bảng ba hàng: $t$ | $1$ … $6$; $L_{S_\eta}(h_t)$ | $\tfrac12;\ \tfrac13;\ \tfrac13;\ \tfrac12;\ \tfrac13;\ \tfrac12$; $L_{D_\eta}(h_t)$ | $0{,}52;\ 0{,}32;\ 0{,}22;\ 0{,}32;\ 0{,}28;\ 0{,}48$.
  - **Câu hỏi:** tính $\operatorname{opt}_{S_\eta}(h_t)$ với $t=1,\ldots,6$. Với đầu ra $\tilde h=h_4$, $L^*=0{,}18$ và $r=0{,}18$,
  - tính ba số hạng của Mệnh đề 04.3(a), vế phải của cận, và so với $L_{D_\eta}(h_4)-L^*$.
  - `[f]` **Lời giải:** $\min_tL_{S_\eta}(h_t)=\tfrac13$: $\operatorname{opt}=\tfrac16;\ 0;\ 0;\ \tfrac16;\ 0;\ \tfrac16$. Độ lệch lớn nhất $\tfrac12-0{,}32=0{,}18$ (tại $h_4$): $S_\eta$ là $0{,}18$-đại diện.
  - `[f]` Ba số hạng: $0{,}22-0{,}18=0{,}04$; $2r=0{,}36$; $\tfrac16$. Vế phải $\approx0{,}5667$, so với $0{,}32-0{,}18=0{,}14$.
- **Ghi chú diễn giả:** Theo §6 của Bài 02, $S_\eta$ là $\epsilon$-đại diện khi và chỉ khi $\epsilon\ge0{,}18$, nên Mệnh đề 04.3(a) áp dụng được với $r=0{,}18$. Cận lớn hơn giá trị thật khoảng $0{,}43$, chủ yếu do $2r$. Kiểm tra: $\tfrac13+\tfrac16=\tfrac12=L_{S_\eta}(h_4)$. Phần (c) của bài: với $\tilde h=h_5$, một nghiệm ERM chính xác, hiệu $L_{D_\eta}(\tilde h)-L_{D_\eta}(\hat h)$ âm khi mốc là $h_2$ và dương khi mốc là $h_3$, còn $\operatorname{opt}_{S_\eta}(h_5)=0$. Phần (a) chứng minh dạng cho ERM xấp xỉ và trường hợp bộ giải chỉ đúng với xác suất cao. Nguồn: tệp bài tập, Bài tập 04.1(b), (c), (a); ghi chú Bài 01, Ví dụ 01.5.
- **Lý do / nối:** bài tập của cụm phân tích sai số, lời giải trên mặt trang; ba số hạng tính được trên dữ liệu thật của Bài 01 → mạch 3.
- **Mục tiêu / nguồn:** 1; Bài tập 04.1(b).

### Mạch 3. Độ chệch và phương sai (8 trang, 19 phút)

#### `3-00` 3. Độ chệch và phương sai — tiêu đề mạch, điểm vào mạch 3 · 0,5 phút
- **Mặt trang:** "3."; h2 "Độ chệch và phương sai"; `p.strand-lead` (bảng mạch, 22 âm tiết); `p.strand-keys`: "hàm hồi quy · dự đoán trung bình · độ chệch · phương sai · nhãn kiểm tra độc lập".
- **Ghi chú diễn giả:** Mệnh đề 04.3 cần hàm lỗi trong $[0,1]$, còn ví dụ ba bậc đa thức dùng hàm lỗi bình phương, không bị chặn. Mạch này dùng một công cụ khác: kì vọng theo tập huấn luyện của lỗi bình phương trên một nhãn mới, tại một điểm cố định, cho một thuật toán cố định. Đẳng thức thu được giải thích vì sao bậc cao không luôn tốt hơn, nhưng các thành phần của nó phụ thuộc hàm hồi quy và mức nhiễu chưa biết. Mạch cũng tách độ chệch, một tính chất của thuật toán, khỏi sai số xấp xỉ, một tính chất của lớp. Nguồn: ghi chú Bài 04, §5.
- **Lý do / nối:** mạch 2 (hàm lỗi bị chặn) → hàm lỗi bình phương.
- **Mục tiêu / nguồn:** 2; §5.

#### `3-01` Độ chệch và phương sai của một ước lượng tại một điểm — định nghĩa · 2 phút
- **Mặt trang:**
  - Với hàm lỗi bình phương, so các bậc qua lỗi trên một nhãn mới tại một điểm.
  - **Định nghĩa 04.5.** Điểm $x$ cố định; nhãn kiểm tra (test label) $Y$ có phân bố của nhãn khi $X=x$, $\mathbb EY^2<\infty$; $\hat f_S(x)$ tính từ $S$, $\mathbb E_S\hat f_S(x)^2<\infty$.
  - Hàm hồi quy (regression function) $f^*(x)=\mathbb E[Y\mid X=x]$; phương sai nhiễu (noise variance) $\sigma^2(x)=\operatorname{Var}(Y\mid X=x)$.
  - Dự đoán trung bình (average prediction) $\bar f(x)=\mathbb E_S\hat f_S(x)$; độ chệch (bias) $\bar f(x)-f^*(x)$.
  - Phương sai (variance) $\operatorname{Var}_S(\hat f_S(x))=\mathbb E_S\big(\hat f_S(x)-\bar f(x)\big)^2$.
- **Ghi chú diễn giả:** Kì vọng trong $\bar f(x)$ và $\operatorname{Var}_S$ lấy theo tập huấn luyện, với $x$ cố định; $\sigma^2(x)$ là phương sai của một nhãn mới tại $x$. Phương sai là tính chất của thuật toán cùng phân bố của tập huấn luyện. Trong thiết kế cố định của ví dụ ba bậc đa thức, $f^*(x)=x^2$ và $\sigma^2(x)=\sigma^2$. Thuật ngữ "độ chệch" khác "độ lệch" của Bài 02–03: độ lệch là $\lvert L_S(h)-L_D(h)\rvert$, còn độ chệch là hiệu giữa dự đoán trung bình và hàm hồi quy. Nguồn: ghi chú Bài 04, §5, Định nghĩa 04.5 và hai đoạn sau.
- **Lý do / nối:** câu mở nêu đại lượng cần so, rồi năm đại lượng của định nghĩa → phát biểu.
- **Mục tiêu / nguồn:** 2; Định nghĩa 04.5.

#### `3-02` Phân tích độ chệch–phương sai tại một điểm — trực quan, kết quả · 3 phút
- **Mặt trang:**
  - **Trực quan.** Ba lẽ: dự đoán dao động quanh $\bar f(x)$; $\bar f(x)$ lệch $f^*(x)$; nhãn $Y$ có nhiễu.
  - **Mệnh đề 04.6.** **Giả thiết:** $x$ cố định; $\hat f_S(x)$ như Định nghĩa 04.5, $S$ bất kì; $Y$ có $\mathbb EY=f^*(x)$, $\operatorname{Var}(Y)=\sigma^2(x)<\infty$, độc lập với $S$.
  - **Bảo đảm** (đẳng thức kì vọng theo $(S,Y)$): lỗi kiểm tra kì vọng (expected test error) tại $x$ là
  - $$\mathbb E_{S,Y}\big(\hat f_S(x)-Y\big)^2=\big(\bar f(x)-f^*(x)\big)^2+\operatorname{Var}_S\big(\hat f_S(x)\big)+\sigma^2(x).$$
  - Đúng cả khi hàm lỗi không bị chặn. Hàm $f$ cố định: phương sai $0$, $\mathbb E(f(x)-Y)^2\ge\sigma^2(x)$.
- **Ghi chú diễn giả:** Đẳng thức là cho một thuật toán tại một điểm. Với hàm $f$ cố định, dấu bằng ở dòng cuối xảy ra khi $f(x)=f^*(x)$. Tập huấn luyện không cần độc lập cùng phân bố; cỡ mẫu $m$ đi vào qua phân bố của $\hat f_S(x)$. Hai số hạng đầu là đại lượng của thuật toán, số hạng cuối là phần nhiễu mà không thuật toán nào giảm được. Với thiết kế ngẫu nhiên (random design), tức đầu vào $X\sim D_{\mathcal X}$ và $(X,Y)$ độc lập với $S$, lấy thêm kì vọng theo $X$ cho $\mathbb E_S[L_D(\hat f_S)]=\mathbb E_X[(\bar f(X)-f^*(X))^2+\operatorname{Var}_S(\hat f_S(X))+\sigma^2(X)]$, giả sử các hàm đo được. Theo dòng cuối, $\mathbb E\,\sigma^2(X)$ là giá trị nhỏ nhất của $L_D$ trên các hàm đo được, tức rủi ro Bayes của hàm lỗi bình phương, đạt tại $f^*$. Nguồn: ghi chú Bài 04, §5, Mệnh đề 04.6 và hai đoạn sau; tệp bài tập, Bài tập 04.2(a).
- **Lý do / nối:** kết quả chính của mạch, trực quan trên cùng trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 2; Mệnh đề 04.6.

#### `3-03` Ý tưởng chứng minh: phân tích độ chệch–phương sai — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  1. Viết tắt $\hat f=\hat f_S(x)$, $\bar f=\bar f(x)$, $f^*=f^*(x)$; tách quanh hai kì vọng:
  - $$\hat f-Y=(\hat f-\bar f)+(\bar f-f^*)+(f^*-Y)$$
  2. Ba bình phương: phương sai, độ chệch bình phương, $\sigma^2(x)$; tích khả tích (Cauchy–Schwarz).
  3. Hai số hạng chéo chứa hằng $\bar f-f^*$ có kì vọng $0$, vì $\mathbb E\hat f=\bar f$ và $\mathbb EY=f^*$.
  4. Số hạng chéo $2\,\mathbb E[(\hat f-\bar f)(f^*-Y)]$ bằng $0$ chỉ nhờ $Y$ độc lập với $S$.
  - **Kỹ thuật.** Thêm bớt kì vọng rồi bình phương; mỗi số hạng chéo một lý do để bằng $0$.
- **Ghi chú diễn giả** (~150 âm tiết): Bình phương vế phải của bước 1 cho ba bình phương và ba số hạng chéo, mỗi số hạng chéo có hệ số $2$. Vì $\mathbb E\hat f^2<\infty$ và $\mathbb EY^2<\infty$, ba số hạng có mô-men bậc hai hữu hạn, nên mọi tích của chúng khả tích. Ở bước 4, tính độc lập cho $\mathbb E[(\hat f-\bar f)(f^*-Y)]=\mathbb E[\hat f-\bar f]\,\mathbb E[f^*-Y]=0$; đây là chỗ duy nhất dùng giả thiết nhãn kiểm tra độc lập. Khi nhãn kiểm tra nằm trong tập huấn luyện, số hạng này bằng $-2\operatorname{Cov}(\hat f,Y)$ và đẳng thức hỏng. Câu ôn nhanh 3 là trường hợp riêng không có $S$: $\mathbb E(U-c)^2=\operatorname{Var}(U)+(\mathbb EU-c)^2$. Nguồn: ghi chú Bài 04, chứng minh Mệnh đề 04.6; Câu hỏi ôn nhanh 3.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; bước 4 đặt câu hỏi về giả thiết độc lập → ví dụ số.
- **Mục tiêu / nguồn:** 2; chứng minh Mệnh đề 04.6.

#### `3-04` Ví dụ: độ chệch và phương sai của ba bậc đa thức — ví dụ (Ví dụ 04.4), chọn bậc · 3,5 phút
- **Mặt trang:**
  - Ví dụ 04.1; $x_0=0{,}5$, $f^*(x_0)=0{,}25$; nhãn kiểm tra $Y=0{,}25+\zeta_0$ độc lập với $S$.
  - $\hat f^{(j)}(x_0)=\sum_iw_iY_i$: dự đoán trung bình $\bar f(x_0)=w_1+w_3$, phương sai $\sigma^2\sum_iw_i^2$.
  | $j$ | $(w_1,w_2,w_3)$ | $\bar f(x_0)$ | độ chệch bình phương | phương sai | tổng, $\sigma^2=1$ | tổng, $\sigma^2=0{,}1$ |
  |---|---|---|---|---|---|---|
  | $0$ | $(\tfrac13,\tfrac13,\tfrac13)$ | $\tfrac23$ | $0{,}1736$ | $0{,}3333\,\sigma^2$ | $0{,}5069$ | $0{,}2069$ |
  | $1$ | $(\tfrac1{12},\tfrac13,\tfrac7{12})$ | $\tfrac23$ | $0{,}1736$ | $0{,}4583\,\sigma^2$ | $0{,}6319$ | $0{,}2194$ |
  | $2$ | $(-\tfrac18,\tfrac34,\tfrac38)$ | $\tfrac14$ | $0$ | $0{,}71875\,\sigma^2$ | $0{,}7188$ | $0{,}0719$ |
  - $\sigma^2=1$: bậc $0$ tốt nhất; $\sigma^2=0{,}1$: bậc $2$; lỗi kiểm tra kì vọng cộng thêm $\sigma^2$.
  - **Kết luận:** bậc tốt nhất phụ thuộc $\sigma^2$, $f^*$ chưa biết; rủi ro thực nghiệm luôn chọn bậc $2$.
- **Ghi chú diễn giả:** Bậc $0$ cho $\bar Y$. Bậc $1$ giải hệ phương trình chuẩn (normal equations); vì $\sum_ix_i=0$ và $\sum_ix_i^2=2$, nghiệm là $\hat a=\bar Y$, $\hat b=(Y_3-Y_1)/2$, nên $\hat f^{(1)}(0{,}5)=\bar Y+\tfrac14(Y_3-Y_1)$. Bậc $2$ là đa thức nội suy Lagrange; ba đa thức cơ sở tại $x_0$ bằng $-\tfrac18$, $\tfrac34$, $\tfrac38$, tổng bằng $1$. Vì $\mathbb EY_i=x_i^2$ và $(x_1^2,x_2^2,x_3^2)=(1,0,1)$, dự đoán trung bình là $w_1+w_3$. Bậc $0$ và $1$ có cùng độ chệch bình phương $(\tfrac23-\tfrac14)^2=\tfrac{25}{144}$; bậc $2$ không chệch vì $x^2\in\mathcal P_2$ được nội suy đúng, nhưng có phương sai lớn nhất. Khi nhiễu chia cho $10$, phương sai chia cho $10$ và độ chệch giữ nguyên, nên thứ tự đảo lại. Nguồn: ghi chú Bài 04, Ví dụ 04.4; Phụ lục C (hệ phương trình chuẩn, trọng số Lagrange).
- **Lý do / nối:** ví dụ số tính tay cho câu hỏi chọn bậc; đánh đổi độ chệch–phương sai trên một bảng → bỏ giả thiết độc lập.
- **Mục tiêu / nguồn:** 2; Ví dụ 04.4.

#### `3-05` Ví dụ: nhãn kiểm tra nằm trong tập huấn luyện — ví dụ (Ví dụ 04.5), bỏ giả thiết · 2,5 phút
- **Mặt trang:**
  - Không có đầu vào; $Y_1,\ldots,Y_m$ độc lập cùng phân bố, kì vọng $\mu$, phương sai $\sigma^2$; $\hat f=\bar Y$; $m=4$, $\sigma^2=1$.
  - Nhãn kiểm tra $Y_1$ nằm trong tập huấn luyện: bỏ giả thiết độc lập.
  - Nếu áp dụng Mệnh đề 04.6: độ chệch $0$, phương sai $\sigma^2/m=0{,}25$, nhiễu $1$; tổng $1{,}25$.
  - $$\mathbb E(\bar Y-Y_1)^2=\sigma^2\Big[\big(\tfrac{m-1}m\big)^2+\tfrac{m-1}{m^2}\Big]=\sigma^2\,\tfrac{m-1}m=0{,}75$$
  - Hiệu $1{,}25-0{,}75=0{,}5=2\sigma^2/m$ là số hạng chéo $-2\operatorname{Cov}(\bar Y,Y_1)$.
  - **Kết luận:** lỗi trên nhãn đã dùng để huấn luyện thấp hơn lỗi trên nhãn mới.
- **Ghi chú diễn giả:** Công thức đúng đến từ cách viết $\bar Y-Y_1=-\tfrac{m-1}m(Y_1-\mu)+\tfrac1m\sum_{i\ge2}(Y_i-\mu)$; các số hạng độc lập và có kì vọng $0$, nên kì vọng của bình phương là tổng các phương sai. Số hạng chéo ở bước 4 của chứng minh bằng $2\,\mathbb E[(\bar Y-\mu)(\mu-Y_1)]=-2\operatorname{Cov}(\bar Y,Y_1)=-2\sigma^2/m$. Đây là lý do không đo chất lượng của hàm dự đoán trên chính các nhãn đã dùng để chọn nó. Nguồn: ghi chú Bài 04, Ví dụ 04.5.
- **Lý do / nối:** phản ví dụ bỏ giả thiết của Mệnh đề 04.6 → so độ chệch với sai số xấp xỉ của mạch 2.
- **Mục tiêu / nguồn:** 2, 5; Ví dụ 04.5.

#### `3-06` Độ chệch và sai số xấp xỉ — nhận xét, phản ví dụ · 2,5 phút
- **Mặt trang:**
  - **Nhận xét 04.7.** Độ chệch: tính chất của thuật toán; sai số xấp xỉ: tính chất của lớp.
  - Không có đầu vào; $Y=\pm1$, mỗi giá trị xác suất $\tfrac12$: $f^*=0$, $\sigma^2=1$.
  - Lớp hai hàm hằng $+1$, $-1$, hàm lỗi bình phương, $m$ lẻ: nghiệm ERM $\operatorname{sign}(\bar Y)$ nhận $\pm1$ với xác suất $\tfrac12$.
  - $\bar f=0=f^*$, không thuộc lớp: độ chệch $0$; phương sai $1$.
  - $L^*=\sigma^2=1$; $\mathbb E(c-Y)^2=2$ với $c=\pm1$: sai số xấp xỉ $1$.
- **Ghi chú diễn giả:** Với $c=\pm1$, $(c-Y_i)^2$ bằng $0$ khi $Y_i=c$ và $4$ khi $Y_i\ne c$, nên nghiệm ERM là dấu chiếm đa số, không có trường hợp bằng nhau vì $m$ lẻ, và do đối xứng nó nhận mỗi dấu với xác suất $\tfrac12$. Rủi ro tham chiếu $\sigma^2=1$ là rủi ro Bayes của hàm lỗi bình phương. Tóm lại, độ chệch bằng $0$, nhưng mọi hàm của lớp có rủi ro lớn hơn rủi ro Bayes $1$. Với nhãn trong $\{0,1\}$, đẳng thức của Mệnh đề 04.6 vẫn đúng nhưng không cho đánh đổi độ chệch–phương sai (bias–variance tradeoff): tại một điểm với $\eta(x)=0{,}9$, thuật toán dự đoán $1$ với xác suất $0{,}4$ có lỗi $0{,}25+0{,}24+0{,}09=0{,}58$, còn thuật toán luôn dự đoán $0$ có lỗi $0{,}81+0+0{,}09=0{,}90$; cả hai có cùng dự đoán đa số sai, và thuật toán có phương sai theo nghĩa phân lớp lớn hơn lại có lỗi nhỏ hơn. Nguồn: ghi chú Bài 04, Nhận xét 04.7, Ví dụ 04.6.
- **Lý do / nối:** phân biệt hai khái niệm dễ nhầm (mục tiêu 2) → bài tập của cụm.
- **Mục tiêu / nguồn:** 2; Nhận xét 04.7, Ví dụ 04.6.

#### `3-07` Bài tập: độ chệch của ước lượng co và sai số xấp xỉ — bài tập (Bài tập 04.2(d)), lời giải trên mặt trang · 2,5 phút (1 phút tự làm)
- **Mặt trang:**
  - $Y_1,\ldots,Y_m$, $Y$ độc lập cùng phân bố, kì vọng $\mu$, phương sai $\sigma^2$.
  - Ước lượng co (shrinkage estimator) $\gamma\bar Y$, $\gamma\in[0,1]$; $m=4$, $\mu=1$, $\sigma^2=1$.
  - **Câu hỏi:** xét lớp các hàm hằng và $L^*=\sigma^2$. Tính sai số xấp xỉ của lớp và độ chệch của $\gamma\bar Y$ tại $\gamma=0{,}8$,
  - với các số trên, và giải thích vì sao hai số khác nhau.
  - `[f]` **Lời giải:** $c=\mu$ thuộc lớp, làm $\mathbb E(c-Y)^2=(c-\mu)^2+\sigma^2$ nhỏ nhất: sai số xấp xỉ $0$.
  - `[f]` $\mathbb E[0{,}8\bar Y]=0{,}8\mu\ne\mu$: độ chệch $(0{,}8-1)\mu=-0{,}2$.
- **Ghi chú diễn giả:** Sai số xấp xỉ là tính chất của lớp, chứa hàm tốt nhất $\mu$; độ chệch là tính chất của thuật toán, có dự đoán trung bình $0{,}8\mu$, khác $\mu$ khi $\mu\ne0$. Bài này và nhận xét vừa xét cho hai chiều ngược nhau: độ chệch $0$ với sai số xấp xỉ $1$, và sai số xấp xỉ $0$ với độ chệch $-0{,}2$. Phần (b) của bài: lỗi kiểm tra kì vọng $(1-\gamma)^2\mu^2+\gamma^2\sigma^2/m+\sigma^2$ bằng $1{,}25$; $1{,}20$; $1{,}3125$; $2{,}00$ tại $\gamma=1;\ 0{,}8;\ 0{,}5;\ 0$, và $\gamma^*=\mu^2/(\mu^2+\sigma^2/m)=0{,}8$ phụ thuộc $\mu$, $\sigma^2$ chưa biết. Phần (c): chọn $\gamma$ theo lỗi trên nhãn đã dùng để huấn luyện cho $\gamma=1$. Nguồn: tệp bài tập, Bài tập 04.2(b)–(d).
- **Lý do / nối:** bài tập của cụm độ chệch–phương sai, lời giải trên mặt trang → mạch 4 (quay về hàm lỗi bị chặn để có quy tắc chọn từ dữ liệu).
- **Mục tiêu / nguồn:** 2; Bài tập 04.2(d).

### Mạch 4. Chia xác suất thất bại và tối thiểu hóa rủi ro cấu trúc (13 trang, 34 phút)

#### `4-00` 4. Chia xác suất thất bại và tối thiểu hóa rủi ro cấu trúc — tiêu đề mạch, điểm vào mạch 4 · 0,5 phút
- **Mặt trang:** "4."; h2 "Chia xác suất thất bại và tối thiểu hóa rủi ro cấu trúc"; `p.strand-lead` (bảng mạch, 22 âm tiết); `p.strand-keys`: "bán kính hội tụ đều · trọng số · số hạng phạt · bất đẳng thức oracle · dung sai".
- **Ghi chú diễn giả:** Mạch 2 cho mỗi lớp chọn trước một cận đúng với xác suất $0{,}95$, và phép so hai cận cần một hiệu sai số xấp xỉ không biết được. Mạch này cho các cận đúng đồng thời trên cả họ lớp bằng cách chia xác suất thất bại theo trọng số. Trên biến cố chung đó, rủi ro thực nghiệm cộng số hạng phạt là một cận trên cho rủi ro kì vọng, và quy tắc tối thiểu hóa cận này có một bất đẳng thức oracle. Ví dụ chọn số chỉ số đo nhận câu trả lời bằng số. Nguồn: ghi chú Bài 04, §6.
- **Lý do / nối:** mạch 2, kết luận của Ví dụ 04.3 → bán kính của một lớp.
- **Mục tiêu / nguồn:** 3; §6.

#### `4-01` Bán kính hội tụ đều của một lớp — định nghĩa · 2,5 phút
- **Mặt trang:**
  - Chọn lớp theo $S$ cần cận đồng thời cho mọi lớp.
  - **Định nghĩa 04.8.** (T2), (T3). $\mathrm{rad}_{\mathcal H}(m,\delta')$ chọn trước, không phụ thuộc $S$, $h$, $D$, là bán kính hội tụ đều (uniform convergence radius) nếu
  - $$\Pr_{S\sim D^m}\Big[\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\le\mathrm{rad}_{\mathcal H}(m,\delta')\Big]\ge1-\delta'$$
  - với mọi $D$, $m\ge1$, $\delta'\in(0,1)$, và biến cố trong ngoặc đo được.
  - Lớp hữu hạn, (T4): $\sqrt{\ln(2\lvert\mathcal H\rvert/\delta')/(2m)}$; hàm lỗi 0–1, (T5), (M): $\rho_m$ tại $\delta'$.
  - Dạng chiều VC (VC-dimension form): $\mathrm{rad}(m,\delta')^2=\tfrac8m\big(d\ln\tfrac{2em}d+\ln\tfrac4{\delta'}\big)$ khi $m\ge d\ge1$; bằng $1$ khi $m<d$.
- **Ghi chú diễn giả:** Câu mở lặp lại yêu cầu của Định lý 02.14: cận đồng thời cho mọi giả thuyết vì giả thuyết được chọn theo mẫu; ở đây là cận đồng thời cho mọi lớp vì lớp được chọn theo mẫu. Hai bán kính ở dòng thứ năm là của Định lý 02.14(a) và Định lý 03.15(a). Một hàm lớn hơn một bán kính cũng là bán kính, và độ lệch đều không vượt quá $1$; vì vậy vế phải thứ nhất của Định lý 03.15(b), cắt ở $1$ khi $m<d$, cũng là một bán kính. Lớp $\mathcal M_{[0,1]}$ của Ví dụ 03.6 có độ lệch đều bằng $1$ trên mọi tập huấn luyện dưới phân bố của ví dụ đó, nên mọi bán kính của nó không nhỏ hơn $1$ và không cho thông tin. Nguồn: ghi chú Bài 04, §6, Định nghĩa 04.8 và ba đoạn sau.
- **Lý do / nối:** đại lượng mà số hạng phạt sẽ dùng → giả thiết (T6) và bổ đề.
- **Mục tiêu / nguồn:** 3; Định nghĩa 04.8.

#### `4-02` Kiểm soát đồng thời trên một họ lớp — trực quan, kết quả · 3 phút
- **Mặt trang:**
  - **Giả thiết:** (T6) các lớp $\mathcal H_1,\mathcal H_2,\ldots$, bán kính $\mathrm{rad}_k=\mathrm{rad}_{\mathcal H_k}$ và trọng số $q_k>0$, $\sum_kq_k\le1$ chọn trước, không phụ thuộc $S$.
  - **Trực quan.** Lớp $k$ nhận phần $\delta q_k$ của xác suất thất bại; các phần cộng lại không quá $\delta$.
  - **Bổ đề 04.9.** **Giả thiết:** (T1), $m\ge1$; $\ell$ thỏa (T2), (T3); (T6); $\delta\in(0,1)$.
  - **Bảo đảm:** số hạng phạt (penalty) $\mathrm{pen}_k=\mathrm{rad}_k(m,\delta q_k)$; với xác suất $\ge1-\delta$, đồng thời mọi $k$, mọi $h\in\mathcal H_k$:
  - $$\lvert L_S(h)-L_D(h)\rvert\le\mathrm{pen}_k$$
- **Ghi chú diễn giả:** Giả thiết (T5) của Bài 03 là (T6) với một lớp và $q_1=1$. Bảo đảm là với xác suất cao cho cả họ lớp, giữa đại lượng thực nghiệm và tổng thể; nó phụ thuộc $m$ qua $\mathrm{rad}_k$, và $\delta$, $q_k$ qua tích $\delta q_k$ trong bán kính. Với hai bán kính của Bài 02–03, tích này vào dưới dạng $\ln(1/\delta)+\ln(1/q_k)$ trong căn. Lớp có trọng số nhỏ nhận bán kính lớn hơn; trọng số giảm theo chỉ số lớp nghĩa là các lớp đầu danh sách được ưu tiên. Nguồn: ghi chú Bài 04, §2 (T6), §6, Bổ đề 04.9.
- **Lý do / nối:** kết quả chính, trực quan trên cùng trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 3; Bổ đề 04.9, (T6).

#### `4-03` Ý tưởng chứng minh: kiểm soát đồng thời — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  1. Biến cố hỏng $B_k=\{\sup_{h\in\mathcal H_k}\lvert L_S(h)-L_D(h)\rvert>\mathrm{pen}_k\}$, đo được theo Định nghĩa 04.8.
  2. $\delta q_k\in(0,1)$; $\mathrm{rad}_k$, $q_k$ không phụ thuộc $S$ (T6), nên $\Pr(B_k)\le\delta q_k$; (T1), (T3) vào qua bán kính.
  3. Dạng đếm được của bất đẳng thức hợp:
  - $$\Pr\Big(\bigcup_kB_k\Big)\le\sum_k\delta q_k\le\delta$$
  - $\sum_kq_k\le1$ dùng ở bất đẳng thức thứ hai; $q_k=1/K$ là phép chia $\delta/K$ của Bài 02.
  - Bỏ "chọn trước": lớp dựng sau khi xem $S$ làm bước 2 hỏng.
- **Ghi chú diễn giả** (~130 âm tiết): Lộ trình là bất đẳng thức hợp trên các lớp, như Định lý 02.14 dùng nó trên các giả thuyết. Biến cố của bổ đề là phần bù của $\bigcup_kB_k$. Ở bước 2, $0<q_k\le\sum_jq_j\le1$ nên $\delta q_k$ nằm trong miền của bán kính; vì $\mathrm{rad}_k$ và $q_k$ cố định trước khi lấy mẫu, Định nghĩa 04.8 áp dụng với $\delta'=\delta q_k$. Câu ôn nhanh 2 là bước 3 với $q_k=2^{-k}$: $0{,}05\sum_{k\ge1}2^{-k}=0{,}05$. Tính đồng thời trên các lớp chỉ đòi thay $\delta$ bằng $\delta q_k$ trong bán kính của lớp $k$. Khi một lớp phụ thuộc $S$, bán kính của nó không còn chặn xác suất của biến cố hỏng; khi tổng trọng số vượt $1$, bất đẳng thức thứ hai hỏng. Nguồn: ghi chú Bài 04, chứng minh Bổ đề 04.9; Câu hỏi ôn nhanh 2.
- **Lý do / nối:** trang ý tưởng chứng minh riêng → kỹ thuật dùng lại.
- **Mục tiêu / nguồn:** 3; chứng minh Bổ đề 04.9.

#### `4-04` Chia xác suất thất bại theo trọng số — kỹ thuật (lần đầu trong học phần) · 2,5 phút
- **Mặt trang:**
  - **Kỹ thuật.** Cận đúng với xác suất $\ge1-\delta'$ cho từng thành phần $k$ của một danh sách đếm được: đặt $\delta'=\delta q_k$,
  - $q_k>0$, $\sum_kq_k\le1$ chọn trước; bất đẳng thức hợp cho mọi $k$ đồng thời với xác suất $\ge1-\delta$.
  - Dùng khi thành phần (lớp, giả thuyết, cỡ mẫu) được chọn theo dữ liệu.
  - **Ví dụ.** $q_k=6/(\pi^2k^2)$: $\sum_kq_k=1$, $\ln(1/q_k)=2\ln k+\ln(\pi^2/6)$; $k=3$: $\mathrm{pen}_3\approx0{,}1900$, không chia: $0{,}1843$.
  - Trên $k=1,\ldots,10$, chia làm bán kính tăng từ khoảng $1\%$ ($k=1$) đến $3{,}2\%$ ($k=4$).
- **Ghi chú diễn giả:** Dạng tổng quát là Bổ đề 04.9 với mọi họ biến cố có cận riêng; giá phải trả là bán kính của thành phần $k$ tính tại $\delta q_k$ thay cho $\delta$. Ví dụ dùng ứng dụng chọn số chỉ số đo, dạng chiều VC của bán kính, $m=10^4$, $\delta=0{,}05$, $d_3=4$: $\ln(4/(0{,}05\,q_3))\approx4{,}382+2{,}695=7{,}077$, $8(38{,}069+7{,}077)/10^4\approx0{,}036117$, căn bằng $0{,}1900$. Với $k=2$, bán kính tăng từ $0{,}1644$ lên $0{,}1690$; với $k=10$, từ $0{,}2799$ lên $0{,}2871$. Giá của phép chia là số hạng $\ln(1/q_k)$ cộng thêm trong căn, nhỏ so với $d_k\ln(2em/d_k)$. Trường hợp $q_k=1/K$ trên $K$ giả thuyết là phép chia $\delta/K$ của Bài 02; trong bài, kỹ thuật dùng lại khi chọn xác suất thất bại theo cỡ mẫu, và Bài 07 dùng lại nó. Nguồn: ghi chú Bài 04, Bổ đề 04.9, Ví dụ 04.7; Phụ lục C (bảng).
- **Lý do / nối:** kỹ thuật dùng lại qua học phần, trang riêng tại nơi dùng lần đầu; giá bằng số → điều kiện tổng trọng số không bỏ được.
- **Mục tiêu / nguồn:** 3, 5; Bổ đề 04.9, Ví dụ 04.7.

#### `4-05` Ví dụ: xác suất thất bại không được chia — ví dụ (Ví dụ 04.8), bỏ giả thiết · 3 phút
- **Mặt trang:**
  - $\mathcal X=\{0,1\}^{k_{\max}}$, tọa độ độc lập $\mathrm{Bernoulli}(\tfrac12)$, $Y=0$; $\mathcal H_k=\{h_k\}$, $h_k(x)=x_k$; hàm lỗi 0–1; $m=10$, $\delta=0{,}05$.
  - Mọi $q_k=1$: $\sum_kq_k=k_{\max}>1$, bỏ điều kiện tổng trọng số của (T6).
  - $L_D(h_k)=\tfrac12$; bán kính một phần tử $\sqrt{\ln40/20}\approx0{,}4295<\tfrac12$.
  - Lớp $k$ hỏng khi $L_S(h_k)\in\{0,1\}$: xác suất $2^{-9}$; các biến cố hỏng độc lập.
  - $k_{\max}=1000$: kết luận của Bổ đề 04.9 sai với xác suất $1-(1-2^{-9})^{1000}\approx0{,}858$; $k_{\max}=5000$: $0{,}99994$.
  - Chia đều, $q_k=1/1000$: bán kính $\approx0{,}7279>\tfrac12$, bổ đề đúng trên mọi tập huấn luyện.
- **Ghi chú diễn giả:** Bán kính một phần tử là $\sqrt{\ln(2/\delta)/(2m)}$ của Hệ quả 02.10(b). $L_S(h_k)$ nhận giá trị trong $\{0;\ 0{,}1;\ \ldots;\ 1\}$, nên độ lệch $\lvert L_S(h_k)-\tfrac12\rvert$ vượt $0{,}4295$ khi và chỉ khi $L_S(h_k)\in\{0,1\}$; mỗi giá trị có xác suất $2^{-10}$. Riêng biến cố có một $k$ với $L_S(h_k)=0$ đã có xác suất $0{,}6236$ khi $k_{\max}=1000$, con số của Bài tập 02.4(b). Bỏ điều kiện $\sum_kq_k\le1$, xác suất thất bại là $0{,}858$ thay vì không quá $0{,}05$, và tiến về $1$ khi $k_{\max}\to\infty$. Nguồn: ghi chú Bài 04, Ví dụ 04.8.
- **Lý do / nối:** phản ví dụ bỏ giả thiết của bổ đề → quy tắc dùng cận đồng thời.
- **Mục tiêu / nguồn:** 3, 5; Ví dụ 04.8.

#### `4-06` Tối thiểu hóa rủi ro cấu trúc — định nghĩa · 2,5 phút
- **Mặt trang:**
  - Trên biến cố của Bổ đề 04.9, $L_S(h)+\mathrm{pen}_k$ là cận trên cho $L_D(h)$, đồng thời mọi lớp.
  - **Định nghĩa 04.10.** Mục tiêu có phạt (penalized objective) $(k,h)\mapsto L_S(h)+\mathrm{pen}_k$, $h\in\mathcal H_k$; dung sai (tolerance) $\tau\ge0$.
  - Nghiệm $\tau$-chính xác ($\tau$-accurate solution): $(\hat k,\hat h)$, $\hat h\in\mathcal H_{\hat k}$, với
  - $$L_S(\hat h)+\mathrm{pen}_{\hat k}\le\inf_k\inf_{h\in\mathcal H_k}\big[L_S(h)+\mathrm{pen}_k\big]+\tau$$
  - Thuật toán trả về nghiệm $\tau$-chính xác trên mọi tập huấn luyện:
  - thuật toán tối thiểu hóa rủi ro cấu trúc (structural risk minimization, SRM), dung sai $\tau$.
- **Ghi chú diễn giả:** Với $\tau=0$ ta gọi là SRM chính xác. Dung sai $\tau$ đo độ chính xác của lời giải bài toán có phạt trên cả họ, còn $\epsilon_{\mathrm{opt}}$ đo bài toán trên một lớp. Một $h$ thuộc nhiều lớp tạo một cặp $(k,h)$ với mỗi lớp chứa nó; $\delta$ là một đầu vào của quy tắc, nên mỗi giá trị $\delta$ cho một quy tắc SRM khác nhau; với một lớp, SRM là ERM. Nghiệm $\tau$-chính xác với $\tau>0$ luôn tồn tại vì mục tiêu không âm; với hàm lỗi 0–1, nghiệm chính xác tồn tại khi danh sách hữu hạn hoặc khi $\mathrm{pen}_k\to\infty$, tính chất mà hai bán kính của Bài 02–03 có (Phụ lục A). Nguồn: ghi chú Bài 04, §6, Định nghĩa 04.10 và hai đoạn sau; đoạn cuối §6; Phụ lục A.
- **Lý do / nối:** câu mở nêu cận trên đồng thời, quy tắc tối thiểu hóa cận đó → bảo đảm.
- **Mục tiêu / nguồn:** 3; Định nghĩa 04.10.

#### `4-07` Ví dụ: chọn số chỉ số đo bằng SRM — ví dụ (Ví dụ 04.9), bảng · 3 phút
- **Mặt trang:**
  - $m=10^4$, $\delta=0{,}05$, $q_k=6/(\pi^2k^2)$, dạng chiều VC với $d_k=k+1$, $\delta'=\delta q_k$; nghiệm ERM chính xác $\hat h_k$ (O1).
  - Thuật toán 04.12: ERM trên từng lớp, so các tổng; dừng khi $\mathrm{pen}_k\ge v$, tổng tốt nhất đã có.
  | $k$ | $L_S(\hat h_k)$ | $\mathrm{pen}_k$ | tổng |
  |---|---|---|---|
  | $1$ | $0{,}300$ | $0{,}1423$ | $0{,}4423$ |
  | $2$ | $0{,}210$ | $0{,}1690$ | $0{,}3790$ |
  | $3$ | $0{,}175$ | $0{,}1900$ | $\mathbf{0{,}3650}$ |
  | $4$ | $0{,}170$ | $0{,}2081$ | $0{,}3781$ |
  | $5$ | $0{,}166$ | $0{,}2241$ | $0{,}3901$ |
  | $6$ | $0{,}163$ | $0{,}2386$ | $0{,}4016$ |
  | $7$ | $0{,}160$ | $0{,}2520$ | $0{,}4120$ |
  | $8$ | $0{,}158$ | $0{,}2644$ | $0{,}4224$ |
  | $9$ | $0{,}156$ | $0{,}2761$ | $0{,}4321$ |
  | $10$ | $0{,}155$ | $0{,}2871$ | $0{,}4421$ |
  - Giả sử $L_S(\hat h_k)$ như bảng, không tăng theo $k$ vì các lớp lồng nhau. SRM chọn $\hat k=3$.
- **Ghi chú diễn giả:** Các số hạng phạt tính như ở trang kỹ thuật, với $\mathrm{pen}_k=\sqrt{8(a_k+b_k)/10^4}$, $a_k=d_k\ln(2em/d_k)$, $b_k=\ln(4/(\delta q_k))$; các tổng làm tròn đến bốn chữ số. Thuật toán 04.12 đầy đủ: đầu vào là tập huấn luyện, họ lớp thỏa (T6) với $\mathrm{pen}_k$ không giảm theo $k$ (danh sách hữu hạn hoặc $\mathrm{pen}_k\to\infty$), $\delta$, và một $\epsilon_{\mathrm{opt}}$-ERM trên mỗi lớp; khởi tạo $v\leftarrow+\infty$, $\hat k\leftarrow1$; ở lớp $k$, tính $\mathrm{pen}_k$, dừng nếu $\mathrm{pen}_k\ge v$, nếu không thì gọi bộ giải được $\hat h_k$ và cập nhật $v$, $\hat k$ khi $L_S(\hat h_k)+\mathrm{pen}_k<v$. Điều kiện dừng hợp lệ vì $L_S\ge0$ và $\mathrm{pen}$ không giảm. Đầu ra là một nghiệm $\tau$-chính xác với $\tau=\epsilon_{\mathrm{opt}}+\tau'$, $\tau'$ là sai số của các phép so sánh; khi mọi lớp được duyệt, sai số tối ưu thực nghiệm chỉ xuất hiện ở lớp so sánh (Phụ lục E). Ở ví dụ này $\epsilon_{\mathrm{opt}}=0$. Nguồn: ghi chú Bài 04, Ví dụ 04.9 Bước 1, Thuật toán 04.12 và đoạn sau; Phụ lục C, E.
- **Lý do / nối:** trả lời câu hỏi thực hành bằng một bảng (mục tiêu 3) → đọc bảng trên hình và so với các cách khác.
- **Mục tiêu / nguồn:** 3; Ví dụ 04.9, Thuật toán 04.12.

#### `4-08` Bất đẳng thức oracle cho SRM — trực quan, kết quả · 3 phút
- **Mặt trang:**
  - **Trực quan.** SRM chọn cặp có $L_S(h)+\mathrm{pen}_k$ nhỏ nhất; so với lớp $k$, giá là $2\,\mathrm{pen}_k$.
  - **Định lý 04.11.** **Giả thiết:** (T1), $m\ge1$; (T2), (T3); (T6); SRM dung sai $\tau\ge0$, đo được; $\delta\in(0,1)$.
  - **Bảo đảm:** với xác suất $\ge1-\delta$, đồng thời mọi nghiệm $\tau$-chính xác: (a) $L_D(\hat h)\le L_S(\hat h)+\mathrm{pen}_{\hat k}$;
  - (b) bất đẳng thức oracle (oracle inequality):
  - $$L_D(\hat h)\le\inf_k\Big[\inf_{h\in\mathcal H_k}L_D(h)+2\,\mathrm{pen}_k\Big]+\tau$$
  - Mốc có phạt (penalized benchmark): $\inf_{h\in\mathcal H_k}L_D(h)$ không tăng khi lớp lồng nhau lớn dần, $2\,\mathrm{pen}_k$ tăng.
- **Ghi chú diễn giả:** Vế phải của (b) là một mốc có phạt; nó chặn rủi ro so với mốc này, còn rủi ro vượt mức so với hợp các lớp thì định lý không chặn. Số hạng phạt là bán kính của Bổ đề 04.9, với các lớp, bán kính, trọng số thỏa (T6). Tên "oracle" chỉ mốc so sánh: vế phải của (b) là giá trị một người biết $D$ có thể dùng để so các lớp, tức mức tốt nhất của lớp $k$ cộng giá thống kê $2\,\mathrm{pen}_k$. SRM không biết số hạng thứ nhất; nó tối thiểu hóa cận trên $L_S(h)+\mathrm{pen}_k$, và định lý nói rằng làm vậy đạt mốc oracle trên biến cố có xác suất ít nhất $1-\delta$. Thuật toán cần thỏa điều kiện đo được của Định nghĩa 01.4. Cận phụ thuộc $m$, $\delta$, $q_k$ và độ phức tạp của lớp qua $\mathrm{pen}_k$; bảo đảm áp dụng cho mọi cặp $\tau$-chính xác, kể cả cặp không do một thuật toán cố định trả về. Phần (a) là một cận trên tin cậy tính được từ dữ liệu. Nguồn: ghi chú Bài 04, §6, Định lý 04.11 và đoạn sau; đoạn cuối §4.
- **Lý do / nối:** kết quả chính của bài, trực quan về hai số hạng trên cùng trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 3; Định lý 04.11.

#### `4-09` Ý tưởng chứng minh: bất đẳng thức oracle — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - Gọi $E$ là biến cố của Bổ đề 04.9: $\Pr(E)\ge1-\delta$, $E$ không phụ thuộc thuật toán. Trên $E$, với mọi $k$, $h\in\mathcal H_k$:
  - $$L_D(\hat h)\le L_S(\hat h)+\mathrm{pen}_{\hat k}\le L_S(h)+\mathrm{pen}_k+\tau\le L_D(h)+2\,\mathrm{pen}_k+\tau$$
  1. Thứ nhất: $E$ tại $(\hat k,\hat h)$, cần đồng thời theo $k$ vì $\hat k$ chọn theo $S$; đây là (a).
  2. Thứ hai: tính $\tau$-chính xác. Thứ ba: $E$ tại $(k,h)$ cố định.
  3. Lấy cận dưới đúng theo $h\in\mathcal H_k$, rồi theo $k$: (b).
  - **Kết luận:** một lớp, $q_1=1$, $\tau=0$: (b) có dạng của Hệ quả 03.16(a).
- **Ghi chú diễn giả** (~170 âm tiết): Lộ trình là ba bất đẳng thức trên biến cố của Bổ đề 04.9, như Bước 2 của chứng minh Hệ quả 02.16. Bất đẳng thức then chốt là cận đồng thời của bổ đề, dùng tại cặp được chọn và tại một cặp so sánh cố định. Bất đẳng thức thứ hai đúng vì cận dưới đúng của mục tiêu không vượt quá giá trị của nó tại $(k,h)$. Các giả thiết (T1)–(T3), (T6) chỉ đi vào qua bổ đề; tính đo được của thuật toán làm $L_D(\hat h)$ là một biến ngẫu nhiên. Nếu bỏ (T6), chẳng hạn một lớp được dựng sau khi xem tập huấn luyện, bất đẳng thức thứ nhất mất cơ sở dù hai bất đẳng thức sau vẫn đúng. Ý nghĩa: SRM cạnh tranh đồng thời với mọi lớp, và với lớp $k$ nó trả giá $2\,\mathrm{pen}_k$. Nguồn: ghi chú Bài 04, chứng minh Định lý 04.11.
- **Lý do / nối:** trang ý tưởng chứng minh riêng → áp dụng bằng số trên ví dụ xuyên suốt.
- **Mục tiêu / nguồn:** 3; chứng minh Định lý 04.11.

#### `4-10` Đánh đổi giữa rủi ro thực nghiệm và số hạng phạt — trực quan, so sánh (Ví dụ 04.9, Bước 2–5) · 3 phút
- **Mặt trang** (`grid2`: hình F2 bên trái, chữ bên phải):
  - **Trực quan.** $L_S(\hat h_k)$ giảm theo $k$, $\mathrm{pen}_k$ tăng; tổng nhỏ nhất tại $k=3$.
  - Định lý 04.11(a): $0{,}3651$ là cận trên tin cậy mức $95\%$ cho $L_D(\hat h_3)$.
  - ERM trên cả họ chọn một hàm của $\mathcal H_{10}$; Định lý 03.15 riêng cho $\mathcal H_{10}$: $0{,}155+0{,}27992\approx0{,}4350$.
  - Biết trước $k=3$: $0{,}175+0{,}18428\approx0{,}3593$; hiệu $\approx0{,}0058$ là giá của việc không biết trước lớp.
  - Tổng tại $k=4$ lớn hơn tại $k=3$ khoảng $0{,}0130$: lựa chọn nhạy với $L_S(\hat h_k)$.
  - {{hình F2 bên trái}}
- **Ghi chú diễn giả:** Cận trên tin cậy $0{,}3651$ là tổng chưa làm tròn $0{,}36504$ làm tròn lên; theo Nhận xét 01.19, thủ tục tính cận này đúng với xác suất ít nhất $0{,}95$ theo tập huấn luyện. Lớp $\mathcal H_{10}$ cố định trước khi lấy mẫu, nên Định lý 03.15 áp dụng cho riêng nó với $\delta$ không chia. Trong bất đẳng thức oracle, số hạng $2\,\mathrm{pen}_k$ bằng $0{,}338$ tại $k=2$ và $0{,}574$ tại $k=10$, so với $0{,}329$ và $0{,}560$ khi mỗi lớp được xét riêng. Đọc hình: rủi ro thực nghiệm (tròn) giảm nhanh từ $k=1$ đến $k=3$ rồi gần như phẳng, số hạng phạt (tam giác) tăng đều, tổng (vuông) có đáy tại $k=3$; với $10^4$ quan sát, SRM dùng ba chỉ số đo. Nguồn: ghi chú Bài 04, Ví dụ 04.9, Bước 2–5 và câu tóm lại.
- **Lý do / nối:** trọng tâm trực quan của bài trên số liệu của ví dụ xuyên suốt; so SRM với ERM trên lớp lớn nhất và với lớp biết trước → bỏ (T6).
- **Mục tiêu / nguồn:** 3; Ví dụ 04.9.

#### `4-11` Ví dụ: họ lớp chọn sau khi xem tập huấn luyện — ví dụ (Ví dụ 04.10), bỏ giả thiết · 3 phút
- **Mặt trang:**
  - $X\sim U[0,1]$, $Y\sim\mathrm{Bernoulli}(0{,}8)$ độc lập với $X$; hàm lỗi 0–1; $m=1000$, $\delta=0{,}05$.
  - $\mathcal H_1=\{h\equiv1\}$, $L_D(h\equiv1)=0{,}2$; sau khi xem $S$: $\mathcal G_S=\{\mathbb 1_{F_+}\}$, $F_+$ là các đầu vào nhãn $1$ của $S$.
  - Với xác suất $1$: $L_S(\mathbb 1_{F_+})=0$, $L_D(\mathbb 1_{F_+})=0{,}8$.
  - Coi hai lớp là cố định, $q=\tfrac12$: bán kính $\sqrt{\ln80/2000}\approx0{,}04681$ cho cả hai.
  - SRM chọn $\mathbb 1_{F_+}$ khi $S$ có ít nhất một nhãn $0$ (xác suất $1-0{,}8^{1000}$); cận trên tin cậy báo $L_D\le0{,}0469$.
  - **Kết luận:** $\mathcal G_S$ phụ thuộc $S$, nên $\Pr(B_2)\le\delta/2$ hỏng; $B_2$ xảy ra chắc chắn, (T6) không thỏa.
- **Ghi chú diễn giả:** Các đầu vào trong tập huấn luyện đôi một khác nhau với xác suất $1$, nên $\mathbb 1_{F_+}$ đúng trên mọi quan sát huấn luyện. Một đầu vào mới nằm ngoài tập hữu hạn $F_+$ với xác suất $1$ và được dự đoán $0$, nên rủi ro kì vọng là $\Pr(Y=1)=0{,}8$. Bán kính là của lớp một phần tử (Hệ quả 02.10(b)) tại $\delta/2$. Hai lớp có cùng số hạng phạt, nên SRM chọn $\mathbb 1_{F_+}$ khi tập huấn luyện có ít nhất một nhãn $0$. Độ lệch của $\mathbb 1_{F_+}$ luôn bằng $0{,}8$: rủi ro kì vọng là $0{,}8$, còn cận báo $0{,}0469$. Đọc thêm: coi mỗi giả thuyết là một lớp một phần tử mô tả bằng một chuỗi bit trong một ngôn ngữ không tiền tố (prefix-free) cố định trước, bất đẳng thức Kraft (Kraft inequality) cho trọng số $q_h=2^{-\lvert h\rvert}$ và số hạng phạt theo độ dài mô tả (description length) $\sqrt{(\lvert h\rvert\ln2+\ln(2/\delta))/(2m)}$ (Nhận xét 04.13, UML §7.3). Nguồn: ghi chú Bài 04, Ví dụ 04.10, Nhận xét 04.13.
- **Lý do / nối:** phản ví dụ bỏ (T6) của Bổ đề 04.9 và Định lý 04.11 → bài tập của cụm.
- **Mục tiêu / nguồn:** 3, 5; Ví dụ 04.10.

#### `4-12` Bài tập: chọn lớp với hai dãy trọng số khác — bài tập (Bài tập 04.4(b)), lời giải trên mặt trang · 2,5 phút (1 phút tự làm)
- **Mặt trang:**
  - **Câu hỏi:** với mười lớp của Ví dụ 04.9, thay $q_k$ bằng $1/10$, rồi bằng $2^{-k}$.
  - Tính các tổng tại $k=2,3,4$ và kiểm tra lựa chọn.
  - `[f]` **Lời giải:** $q_k=1/10$: $\ln(4/(\delta q_k))=\ln800\approx6{,}685$ với mọi $k$; $q_k=2^{-k}$: $\ln80+k\ln2$.
  | $k$ | $q_k=1/10$ | $q_k=2^{-k}$ |
  |---|---|---|
  | $2$ | $0{,}210+0{,}1699=0{,}3799$ | $0{,}210+0{,}1678=0{,}3778$ |
  | $3$ | $0{,}175+0{,}1892=\mathbf{0{,}3642}$ | $0{,}175+0{,}1887=\mathbf{0{,}3637}$ |
  | $4$ | $0{,}170+0{,}2062=0{,}3762$ | $0{,}170+0{,}2071=0{,}3771$ |
  - `[f]` Các lớp còn lại: $k=1$: $0{,}4473$; $0{,}4428$. Với $k\ge5$, nhỏ nhất tại $k=5$: $0{,}3875$; $0{,}3896$.
  - `[f]` Cả hai dãy chọn $k=3$; trọng số chỉ vào qua $\ln(1/q_k)$, nhỏ so với $d_k\ln(2em/d_k)$.
- **Ghi chú diễn giả:** Cột rủi ro thực nghiệm là của Ví dụ 04.9. Với $q_k=1/10$ tại $k=3$: $a_3\approx38{,}069$, $\mathrm{pen}_3=\sqrt{8\cdot44{,}753/10^4}\approx0{,}1892$. Với $q_k=2^{-k}$: $b_3\approx6{,}461$, $\mathrm{pen}_3\approx0{,}1887$. Trọng số đều $1/10$ chỉ dùng được cho danh sách hữu hạn; trên danh sách vô hạn, $\sum_kq_k\le1$ buộc $q_k\to0$. Phần (a) của bài chạy Thuật toán 04.12 trên $25$ lớp: thuật toán dừng ở lớp $19$, vì $\mathrm{pen}_{19}\approx0{,}3676\ge0{,}3650$, sau $18$ lần gọi bộ giải. Phần (c): với $m=10^5$, SRM vẫn chọn $k=3$, nhưng sát $k=4$; đổi riêng $L_S(\hat h_4)$ thành $0{,}166$ thì SRM chọn $k=4$. Nguồn: tệp bài tập, Bài tập 04.4(a)–(c).
- **Lý do / nối:** bài tập của cụm SRM, lời giải trên mặt trang (bảng hiện cùng fragment của dòng lời giải đầu) → mạch 5 (khi danh sách vô hạn, cỡ mẫu phụ thuộc lớp).
- **Mục tiêu / nguồn:** 3; Bài tập 04.4(b).

### Mạch 5. Học không đều (5 trang, 12 phút)

#### `5-00` 5. Học không đều — tiêu đề mạch, điểm vào mạch 5 · 0,5 phút
- **Mặt trang:** "5."; h2 "Học không đều"; `p.strand-lead` (bảng mạch, 19 âm tiết); `p.strand-keys`: "giả thuyết so sánh · cỡ mẫu theo lớp · xác suất thất bại giảm theo cỡ mẫu".
- **Ghi chú diễn giả:** Bất đẳng thức oracle so với mọi lớp cùng lúc, nhưng với một danh sách vô hạn, số hạng phạt tăng vô hạn theo chỉ số lớp, nên cỡ mẫu đủ phụ thuộc lớp chứa hàm làm mốc. Mạch này định nghĩa kiểu bảo đảm tương ứng, học không đều, rồi cho xác suất thất bại giảm theo cỡ mẫu để SRM thành một thuật toán duy nhất có bảo đảm đó. Một lớp đếm được có chiều VC vô hạn cho thấy kiểu học này yếu hơn hẳn học PAC. Nguồn: ghi chú Bài 04, §7.
- **Lý do / nối:** mạch 4 → định nghĩa.
- **Mục tiêu / nguồn:** 4; §7.

#### `5-01` Thuật toán học không đều — định nghĩa · 2,5 phút
- **Mặt trang:**
  - Định lý 04.11: $L_D(\hat h)\le L_D(h)+2\,\mathrm{pen}_k+\tau$, $h\in\mathcal H_k$; $\mathrm{pen}_k\to\infty$: cỡ mẫu theo lớp chứa $h$.
  - **Nhắc lại:** học xấp xỉ với xác suất cao (probably approximately correct, PAC) bất khả diễn: $M(\epsilon,\delta)$ chung, so với $\inf_{h'}L_D(h')$.
  - **Định nghĩa 04.14.** $A$ là thuật toán học không đều (nonuniform learner) cho $\mathcal H$ nếu có $M:(0,1)^2\times\mathcal H\to\mathbb N$ sao cho
  - $$\Pr_{S\sim D^m}\big[L_D(A(S))\le L_D(h)+\epsilon\big]\ge1-\delta$$
  - với mọi giả thuyết so sánh (comparator hypothesis) $h\in\mathcal H$, mọi $\epsilon,\delta\in(0,1)$, mọi $D$, mọi $m\ge M(\epsilon,\delta,h)$.
  - $M$ phụ thuộc $h$, không phụ thuộc $D$.
- **Ghi chú diễn giả:** Học PAC bất khả diễn là Định nghĩa 01.25. Trên danh sách vô hạn, $\mathrm{pen}_k\to\infty$ với bán kính của Định lý 02.14(a) hoặc 03.15(a), nên cận không cho một cỡ mẫu chung cho mọi $h$. Thứ tự lượng từ giống Định nghĩa 01.25: $A$ cố định trước $\epsilon$, $\delta$, và $M$ có trước $D$. Hai khác biệt: $M$ được phép phụ thuộc giả thuyết so sánh $h$, và đối tượng so sánh là $L_D(h)$ thay cho $\inf_{h'}L_D(h')$, với xác suất lấy cho từng $h$. Lớp $\mathcal H$ học được không đều (nonuniformly learnable) nếu có một thuật toán học không đều cho nó. Với hàm lỗi bị chặn, một thuật toán học PAC bất khả diễn có $M(\epsilon,\delta,h)=M(\epsilon,\delta)$, vì $L_D(A(S))\le\inf_{h'}L_D(h')+\epsilon\le L_D(h)+\epsilon$. Một quy tắc có cỡ mẫu phụ thuộc $D$, chẳng hạn qua sai số xấp xỉ, không thỏa định nghĩa. Nguồn: ghi chú Bài 04, §7, đoạn mở, Định nghĩa 04.14 và hai đoạn sau.
- **Lý do / nối:** câu mở nêu nhu cầu từ Định lý 04.11, nhắc lại học PAC trước khi so → SRM như một thuật toán học không đều.
- **Mục tiêu / nguồn:** 4; Định nghĩa 04.14.

#### `5-02` SRM với xác suất thất bại 1/m — trực quan, kết quả · 3 phút
- **Mặt trang:**
  - **Trực quan.** SRM nhận $\delta$; Định nghĩa 04.14 đòi thuật toán cố định trước $\epsilon$, $\delta$: cho $\delta=1/m$.
  - **Hệ quả 04.15.** **Giả thiết:** hàm lỗi 0–1, (T1); họ lớp đếm được chọn trước; mỗi $\mathcal H_k$ hữu hạn hoặc (M), $d_k<\infty$;
  - $q_k>0$, $\sum_kq_k\le1$; $\mathrm{pen}_k(m)=\mathrm{rad}_k(m,q_k/m)$; $A_{\mathrm{SRM}}$: nghiệm SRM chính xác, đo được, khi $m\ge2$.
  - **Bảo đảm:** (a) $A_{\mathrm{SRM}}$ học không đều cho $\mathcal H=\bigcup_k\mathcal H_k$ với
  - $$M(\epsilon,\delta,h)=\max\big\{\lceil1/\delta\rceil,\ M_{k(h)}(\epsilon)\big\}$$
  - (b) Danh sách $k_{\max}$ lớp: học PAC bất khả diễn với $M(\epsilon,\delta)=\max\{\lceil1/\delta\rceil,\max_{k\le k_{\max}}M_k(\epsilon)\}$.
- **Ghi chú diễn giả:** Bán kính $\mathrm{rad}_k$ là của Định lý 02.14(a) khi $\mathcal H_k$ hữu hạn và của Định lý 03.15(a) trong trường hợp còn lại; với $m=1$, thuật toán trả về một phần tử cố định của $\mathcal H_1$. $M_k(\epsilon)$ là cỡ mẫu $m_0\ge2$ nhỏ nhất sao cho $2\,\mathrm{pen}_k(m)\le\epsilon$ với mọi $m\ge m_0$, và $k(h)$ là chỉ số nhỏ nhất của lớp chứa $h$. Thuật toán không nhận $\epsilon$, $\delta$; cỡ mẫu phụ thuộc $h$ qua chỉ số lớp, không phụ thuộc $D$. Nghiệm SRM chính xác tồn tại vì $\mathrm{pen}_k\to\infty$ theo $k$ khi $m$ cố định (Phụ lục A). Nguồn: ghi chú Bài 04, §7, Hệ quả 04.15; Phụ lục A.
- **Lý do / nối:** kết quả chính của mạch, trực quan trên cùng trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 4; Hệ quả 04.15.

#### `5-03` Ý tưởng chứng minh: xác suất thất bại 1/m — ý tưởng chứng minh, cỡ mẫu bằng số · 3 phút
- **Mặt trang:**
  1. Định lý 04.11(b) tại $\delta=1/m$, $\tau=0$: trên $E_m$, $\Pr(E_m)\ge1-1/m$, $L_D(A_{\mathrm{SRM}}(S))\le L_D(h)+2\,\mathrm{pen}_k(m)$ với mọi $k$, $h\in\mathcal H_k$.
  2. $\mathrm{pen}_k(m)$ có dạng $\sqrt{(a+b\ln m)/m}\to0$, nên $M_k(\epsilon)<\infty$.
  3. $m\ge\max\{\lceil1/\delta\rceil,M_{k(h)}(\epsilon)\}$ cho $1/m\le\delta$ và $2\,\mathrm{pen}_{k(h)}(m)\le\epsilon$: phần (a).
  4. Hữu hạn lớp: lấy $\max_kM_k(\epsilon)$, rồi $\inf_h$: phần (b).
  - **Kỹ thuật.** Chọn $\delta=1/m$: một thuật toán không nhận $\delta$ đạt mọi mức $\delta$ khi $m\ge\lceil1/\delta\rceil$; giá là $\ln m$ thay cho $\ln(1/\delta)$.
  - **Ví dụ.** $k=3$, $\epsilon=0{,}1$: $172\,279$ (ERM trên $\mathcal H_3$), $181\,575$ (SRM, $\delta=0{,}05$), $213\,317$ ($A_{\mathrm{SRM}}$) quan sát.
- **Ghi chú diễn giả** (~190 âm tiết): Giả thiết (T1), hàm lỗi 0–1 và điều kiện trọng số đi vào qua Định lý 04.11; tính đo được của $A_{\mathrm{SRM}}$ làm các biến cố có xác suất. Ở bước 2, lớp hữu hạn có $\mathrm{pen}_k(m)=\sqrt{\ln(2\lvert\mathcal H_k\rvert m/q_k)/(2m)}$, lớp có $1\le d_k\le m$ có $\mathrm{pen}_k(m)^2\le\tfrac8m\big(d_k\ln\tfrac{2em}{d_k}+\ln\tfrac{4m}{q_k}\big)$, và $d_k=0$ cho $\sqrt{8\ln(4m/q_k)/m}$; cả ba có dạng $\sqrt{(a+b\ln m)/m}$. Ở bước 4, mọi phân bố có rủi ro hữu hạn vì hàm lỗi bị chặn. Ba cỡ mẫu đủ là nghiệm nhỏ nhất của điều kiện $2\,\mathrm{pen}\le0{,}1$ với dạng chiều VC, $d_3=4$, tìm bằng chia đôi khoảng: không biết trước lớp làm cỡ mẫu tăng khoảng $5{,}4\%$, bỏ $\delta$ khỏi đầu vào tăng thêm khoảng $17{,}5\%$; đổi lại, ở cỡ mẫu $213\,317$, $A_{\mathrm{SRM}}$ có xác suất thất bại không quá $1/m\approx4{,}7\cdot10^{-6}$. Điều kiện $m\ge\lceil1/\delta\rceil=20$ không ràng buộc. Các số là cỡ mẫu nhỏ nhất của một cận trên, nên chỉ là cỡ mẫu đủ. Nguồn: ghi chú Bài 04, §7 (đoạn sau Hệ quả 04.15); Phụ lục B.
- **Lý do / nối:** trang ý tưởng chứng minh riêng, kèm kiểm tra bằng số → một lớp học được không đều mà không học được PAC.
- **Mục tiêu / nguồn:** 4; Hệ quả 04.15, Phụ lục B.

#### `5-04` Ví dụ: một lớp đếm được có chiều VC vô hạn — ví dụ (Ví dụ 04.11), kết quả đọc thêm (Định lý 04.16) · 3 phút
- **Mặt trang:**
  - $\mathcal X=[0,1]$, hàm lỗi 0–1; $\mathcal H$: các $\mathbb 1_F$, $F$ hữu hạn, gồm các số hữu tỉ.
  - $\mathcal H$ đếm được: $\mathcal H=\{h_1,h_2,\ldots\}$; $\mathcal H_j=\{h_j\}$, trọng số $q_j=6/(\pi^2j^2)$.
  - Mọi tập hữu hạn số hữu tỉ bị tách trọn vẹn: $d=\infty$, không học được PAC.
  - Mỗi $\mathcal H_j$ hữu hạn: học được không đều (Hệ quả 04.15(a)).
  - **Định lý 04.16.** Phân lớp nhị phân: học được không đều thì $\mathcal H=\bigcup_k\mathcal H_k$, mỗi $\mathcal H_k$ có chiều VC hữu hạn.
- **Ghi chú diễn giả:** Tập các tập con hữu hạn của một tập đếm được là đếm được, nên lớp liệt kê được thành $h_1,h_2,\ldots$. Không học được PAC là theo Định lý 03.17(a). Tóm lại, học được không đều không kéo theo học được PAC. Lấy $F$ là tập các điểm nhãn $1$ cho thấy mọi tập hữu hạn số hữu tỉ bị tách trọn vẹn; theo Nhận xét 01.26, lớp cũng không học được PAC bất khả diễn. Để $A_{\mathrm{SRM}}$ đo được, chọn chỉ số $j$ nhỏ nhất trong các nghiệm. Cỡ mẫu tăng theo $\ln(1/q_j)=2\ln j+\ln(\pi^2/6)$, tức theo vị trí của giả thuyết so sánh trong danh sách. Định lý 04.16 ở mức đọc thêm, cho phân lớp nhị phân với hàm lỗi 0–1: phần (a) là điều kiện cần, chứng minh phác thảo ở Phụ lục D bằng cách phủ lớp bởi các tập $\{h:M(\tfrac18,\tfrac18,h)\le k\}$ rồi dùng định lý không có bữa trưa miễn phí (no-free-lunch theorem); phần (b), điều kiện đủ khi các lớp có chiều VC hữu hạn và thỏa (M), là Hệ quả 04.15. Lớp của ví dụ có đúng dạng của phần (a): hợp đếm được của các lớp một phần tử, chiều VC $0$. Nguồn: ghi chú Bài 04, Ví dụ 04.11, Định lý 04.16 và đoạn sau; Phụ lục D; UML §7.1.
- **Lý do / nối:** ví dụ tách hai khái niệm (mục tiêu 4), đặc trưng đọc thêm cùng trang → mạch 6 (một cách chọn không cần số hạng phạt).
- **Mục tiêu / nguồn:** 4; Ví dụ 04.11, Định lý 04.16.

### Mạch 6. Chọn mô hình bằng mẫu xác thực (6 trang, 14 phút)

#### `6-00` 6. Chọn mô hình bằng mẫu xác thực — tiêu đề mạch, điểm vào mạch 6 · 0,5 phút
- **Mặt trang:** "6."; h2 "Chọn mô hình bằng mẫu xác thực"; `p.strand-lead` (bảng mạch, 19 âm tiết); `p.strand-keys`: "mẫu xác thực · ứng viên · lấy điều kiện · dùng lại thích nghi · kiểm tra chéo".
- **Ghi chú diễn giả:** SRM dùng cùng một tập huấn luyện để huấn luyện và để chọn lớp, và trả giá bằng số hạng phạt. Khi có thêm một mẫu dữ liệu chỉ dùng để chọn, phép chọn trở thành ERM trên một danh sách hữu hạn ứng viên, và cận của Bài 02 cho lớp hữu hạn áp dụng được sau một bước lấy điều kiện. Giá của cách này là phần dữ liệu không dùng để huấn luyện và giả thiết danh sách ứng viên cố định trước khi dùng mẫu xác thực. Nguồn: ghi chú Bài 04, §8, đoạn mở.
- **Lý do / nối:** mạch 4–5 → giả thiết (T7).
- **Mục tiêu / nguồn:** 5; §8.

#### `6-01` Chọn ứng viên bằng mẫu xác thực — trực quan, kết quả · 3 phút
- **Mặt trang:**
  - **Trực quan.** Mẫu xác thực (validation sample) chỉ để chọn: chọn mô hình (model selection) là ERM trên $K$ ứng viên.
  - **Giả thiết:** (T7) $V=(V_1,\ldots,V_{m_v})\sim D^{m_v}$ độc lập với $S$; ứng viên là hàm của $S$. $L_V(g)=\tfrac1{m_v}\sum_i\ell(g,V_i)$.
  - **Hệ quả 04.17.** **Giả thiết:** $S$ bất kì; $g_1,\ldots,g_K$ là hàm đo được của $S$; (T7); (T2), (T3); $\hat g\in\arg\min_jL_V(g_j)$.
  - **Bảo đảm:** theo $(S,V)$, mỗi phần với xác suất $\ge1-\delta$: (a)
  - $$L_D(\hat g)\le\min_{j\le K}L_D(g_j)+2\sqrt{\tfrac{\ln(2K/\delta)}{2m_v}}$$
  - (b) cận trên tin cậy $L_D(\hat g)\le L_V(\hat g)+\sqrt{\ln(K/\delta)/(2m_v)}$.
- **Ghi chú diễn giả:** $m_v$ là cỡ mẫu xác thực (validation sample size). Số ứng viên $K\ge1$ có thể phụ thuộc $S$; $K(S)$ và hàm lỗi của từng ứng viên cần đo được. Đối tượng so sánh là ứng viên tốt nhất, ngẫu nhiên qua $S$. Cận phụ thuộc $m_v$, $\ln K$ và $\delta$, không phụ thuộc độ phức tạp của các lớp sinh ra ứng viên hay cỡ mẫu huấn luyện $m$. Nguồn: ghi chú Bài 04, §8, (T7), Hệ quả 04.17.
- **Lý do / nối:** giả thiết mới và kết quả chính của mạch, trực quan trên cùng trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 5; (T7), Hệ quả 04.17.

#### `6-02` Ý tưởng chứng minh: chọn mô hình bằng mẫu xác thực — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  1. Lấy điều kiện theo $S$: ứng viên thành lớp hữu hạn cố định; $V\sim D^{m_v}$ (T7).
  2. (a): Hệ quả 02.16(a), ERM trên lớp hữu hạn, cho $V$; (b): Định lý 02.14(b).
  3. Bỏ điều kiện bằng định lý Fubini.
  - **Kỹ thuật.** Lấy điều kiện theo tập huấn luyện, áp dụng Bài 02, bỏ điều kiện.
  - Bỏ (T7): ứng viên dựng từ $V$ làm bước 1 hỏng.
- **Ghi chú diễn giả** (~150 âm tiết): Bước 1 giống Bước 1 của Ví dụ 02.8: khi biết $S$, các ứng viên không còn ngẫu nhiên, và mẫu xác thực độc lập vẫn có phân bố $D^{m_v}$ (Nhận xét 01.9). Ở bước 2, Hệ quả 02.16(a) cho ERM trên lớp hữu hạn cận $2r_m$ với $m_v$ thay cho $m$, và Định lý 02.14(b) là cận một phía $\sqrt{\ln(K/\delta)/(2m_v)}$; giá trị nhỏ nhất $\min_jL_D(g_j)$ đạt vì lớp hữu hạn. Hai phần dùng hai biến cố khác nhau; nếu cần cả hai cùng lúc, dùng $\delta/2$ cho mỗi phần. Bước 3 lấy kì vọng theo $S$ của xác suất có điều kiện; tính đo được trong giả thiết cho phép bước này. Hệ số $2$ trong $\ln(2K/\delta)$ đến từ hai phía của bất đẳng thức Hoeffding; hệ số $2$ ngoài căn đến từ hai phép so sánh. Ý nghĩa: chọn trong $K$ ứng viên tốn một lượng tỉ lệ với $\sqrt{\ln K/m_v}$. Nguồn: ghi chú Bài 04, chứng minh Hệ quả 04.17 (phác thảo).
- **Lý do / nối:** trang ý tưởng chứng minh riêng → số liệu trên ví dụ xuyên suốt.
- **Mục tiêu / nguồn:** 5; chứng minh Hệ quả 04.17.

#### `6-03` Ví dụ: mười ứng viên và mẫu xác thực — ví dụ (Ví dụ 04.12), cận bằng số · 2,5 phút
- **Mặt trang** (`grid2`: chữ bên trái, hình F3 bên phải):
  - $g_k=\hat h_k$, nghiệm ERM trên $\mathcal H_k$ từ $S$ ($m=10^4$), $K=10$; $V$ mới, $m_v=1000$; hàm lỗi 0–1; $\delta=0{,}05$.
  - $\ln(2K/\delta)=\ln400\approx5{,}9915$; cận (a): $2\sqrt{5{,}9915/2000}\approx0{,}1095$.
  - Theo $m_v$: $0{,}2448$ ($200$); $0{,}1548$ ($500$); $0{,}0774$ ($2000$); $0{,}0490$ ($5000$).
  - **Nhắc lại:** đảo cận đuôi thành bán kính và cỡ mẫu (Bài 02): $m_v\ge2\ln400/\epsilon^2$; $1199$ ($\epsilon=0{,}1$), $4794$ ($\epsilon=0{,}05$).
  - $K=10^6$: cận tăng từ $0{,}1095$ lên $0{,}1871$.
  - {{hình F3 bên phải}}
- **Ghi chú diễn giả:** Số $0{,}0547$ là bán kính của câu ôn nhanh 1, với $m_v$ thay cho $m$. Với $\epsilon=0{,}1$, $2\cdot5{,}9915/0{,}01\approx1198{,}3$, nên $1199$ quan sát xác thực là đủ; với $\epsilon=0{,}05$, $4793{,}2$ cho $4794$. Nhân số ứng viên lên $10^5$ lần chỉ làm cận tăng từ $0{,}1095$ lên $0{,}1871$, vì $K$ vào qua lôgarit. Đổi lại, cận chỉ so với ứng viên tốt nhất, nên không so trực tiếp được với cận trên tin cậy $0{,}3651$ của SRM. Đọc hình: cận (a) theo cỡ mẫu xác thực trên trục lôgarit, giảm theo $1/\sqrt{m_v}$. Nguồn: ghi chú Bài 04, Ví dụ 04.12.
- **Lý do / nối:** ví dụ số của hệ quả trên ví dụ xuyên suốt → các giới hạn.
- **Mục tiêu / nguồn:** 5; Ví dụ 04.12.

#### `6-04` Phạm vi của bảo đảm xác thực — nhận xét, ví dụ chọn bậc · 2,5 phút
- **Mặt trang:**
  - **Nhận xét 04.18.** Giới hạn của Hệ quả 04.17:
  - Dùng lại thích nghi (adaptive reuse): ứng viên, $K$ chọn sau khi xem $L_V$ làm hỏng (T7).
  - Kiểm tra chéo (cross-validation): mỗi phần vừa huấn luyện vừa xác thực.
  - Hàm lỗi bình phương: cần $\lvert Y\rvert\le B$, cắt dự đoán vào $[-B,B]$; cận nhân $4B^2$.
  - **Ví dụ.** Chọn trong $K=15$ bậc đa thức, $m_v=1000$, $B=1$, $\delta=0{,}05$: cận $4\cdot2\sqrt{\ln600/2000}\approx0{,}4524$.
- **Ghi chú diễn giả:** Khi dùng lại thích nghi, danh sách thực tế gồm mọi ứng viên có thể được tạo ra, không chỉ những ứng viên được thử. Trong kiểm tra chéo, các số hạng phụ thuộc nhau và Hệ quả 04.17 không áp dụng. Với hàm lỗi bình phương sau khi cắt, hàm lỗi nằm trong $[0,4B^2]$. Dòng ví dụ trả lời một phần câu hỏi mở đầu: với nhãn bị chặn và dự đoán được cắt, chọn bậc bằng mẫu xác thực có bảo đảm, còn các cận đều của Bài 02–03 không áp dụng cho lớp đa thức với hàm lỗi bình phương. SRM cần họ lớp, bán kính và trọng số cố định trước khi lấy mẫu (T6); chọn mô hình bằng mẫu xác thực cần danh sách ứng viên cố định trước khi dùng mẫu xác thực (T7). Nguồn: ghi chú Bài 04, Nhận xét 04.18 và đoạn sau; §9.
- **Lý do / nối:** giới hạn của kết quả và câu trả lời bằng số cho bài toán chọn bậc → bài tập về dùng lại thích nghi.
- **Mục tiêu / nguồn:** 5; Nhận xét 04.18.

#### `6-05` Bài tập: dùng lại thích nghi một mẫu xác thực — bài tập (Bài tập 04.5(a)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - Phân bố của Ví dụ 04.10, hàm lỗi 0–1, $m_v=1000$; $g_1,\ldots,g_{10}$ hàm của $S$, $g_1\equiv1$, (T7) thỏa.
  - Sau khi xem $V$: thêm $g_{11}=\mathbb 1_{F_+(V)}$ (đầu vào nhãn $1$ trong $V$); $\hat g$ làm $L_V$ nhỏ nhất trong $11$ ứng viên.
  - **Câu hỏi:** chặn dưới $L_D(\hat g)-\min_{j\le11}L_D(g_j)$ khi $\hat g=g_{11}$, so với vế phải của Hệ quả 04.17(a) với $K=11$,
  - và chỉ ra giả thiết bị vi phạm.
  - `[f]` **Lời giải:** $L_V(g_{11})=0$, $L_D(g_{11})=0{,}8$, $L_D(g_1)=0{,}2$: hiệu $\ge0{,}6$; vế phải $2\sqrt{\ln440/2000}\approx0{,}1103$.
  - `[f]` $g_{11}$ dùng chính $V$: (T7) bị vi phạm.
- **Ghi chú diễn giả:** Như Ví dụ 04.10 với $V$ thay cho $S$: các đầu vào của $V$ đôi một khác nhau với xác suất $1$, nên $L_V(g_{11})=0$, còn một đầu vào mới nằm ngoài tập hữu hạn $F_+(V)$ và được dự đoán $0$. Vì $L_V\ge0$, $g_{11}$ luôn làm $L_V$ nhỏ nhất, nên quy tắc chọn được phép trả về nó. (T7) đòi ứng viên là hàm của $S$; bước lấy điều kiện của chứng minh không áp dụng. Phần (b) của bài: với $K_0$ phép sửa định sẵn qua $J$ vòng, danh sách thực tế có $K_0^J$ mô hình, và $K_0=10$, $J=5$ cho $2\sqrt{\ln(4\cdot10^6)/2000}\approx0{,}1744$; phần (c): khi phép sửa nghĩ ra sau khi xem kết quả, cần một mẫu mới để đánh giá. Nguồn: tệp bài tập, Bài tập 04.5(a)–(c).
- **Lý do / nối:** bài tập của cụm mẫu xác thực, kiểm giả thiết (T7) → mạch Tổng kết.
- **Mục tiêu / nguồn:** 5; Bài tập 04.5(a).

### Mạch 7. Tổng kết (8 trang, 11 phút)

#### `7-00` 7. Tổng kết — tiêu đề mạch, điểm vào mạch 7 · 0,5 phút
- **Mặt trang:** "7."; h2 "Tổng kết"; `p.strand-lead` (bảng mạch, 21 âm tiết); không có dòng từ khóa.
- **Ghi chú diễn giả:** Bài có sáu kết quả chính và một kỹ thuật mới, chia xác suất thất bại theo trọng số. Mạch cuối gom các giả thiết không được bỏ của từng kết quả, trả lời vấn đề trung tâm cho cả bài, làm một bài tập ghép phân tích sai số, chiều VC và SRM, rồi tự kiểm tra và giao bài tập. Không có khái niệm mới. Nguồn: ghi chú Bài 04, §9–§12.
- **Lý do / nối:** mạch 6 → bảng tổng kết.
- **Mục tiêu / nguồn:** tất cả; §9–§12.

#### `7-01` Bảng tổng kết — tổng kết · 2 phút
- **Mặt trang (bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh`, trần 80):**
  | Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh |
  |---|---|---|
  | $L_D(\tilde h)-L^*\le$ xấp xỉ $+2r+\operatorname{opt}_S$, xác suất $\ge1-\delta$ (Mệnh đề 04.3) | (T3), cận đều | thêm bớt $L_S$ |
  | độ chệch–phương sai, kì vọng (Mệnh đề 04.6) | $Y$ độc lập với $S$ | tách quanh kì vọng |
  | $\sup_{\mathcal H_k}\lvert L_S-L_D\rvert\le\mathrm{pen}_k$ mọi $k$, xác suất $\ge1-\delta$ (Bổ đề 04.9) | (T6), $\sum_kq_k\le1$ | bất đẳng thức hợp |
  | $L_D(\hat h)\le\inf_k[\inf_{\mathcal H_k}L_D+2\,\mathrm{pen}_k]+\tau$, xác suất $\ge1-\delta$ (Định lý 04.11) | (T3), (T6) | ba bất đẳng thức |
  | $A_{\mathrm{SRM}}$ học không đều (Hệ quả 04.15) | hữu hạn hoặc (M), $d_k<\infty$ | $\delta=1/m$ |
  | $L_D(\hat g)\le\min_jL_D(g_j)+2\sqrt{\ln(2K/\delta)/(2m_v)}$, xác suất $\ge1-\delta$ (Hệ quả 04.17) | (T7), (T3) | lấy điều kiện |
- **Ghi chú diễn giả:** Hàng thứ hai là một đẳng thức kì vọng cho hàm lỗi bình phương; các hàng khác là bảo đảm với xác suất cao cho hàm lỗi trong $[0,1]$, với mọi phân bố. Hàng thứ nhất cần cận đều vì đầu ra được chọn theo tập huấn luyện; cận đều có được dưới (T1), (T4), hoặc dưới hàm lỗi 0–1, (T1), (T5), (M). Bốn giả thiết có phản ví dụ khi bỏ: họ lớp cố định (cận báo $0{,}0469$ trong khi rủi ro kì vọng là $0{,}8$), tổng trọng số không quá $1$ (xác suất thất bại $0{,}86$ thay vì không quá $0{,}05$), nhãn kiểm tra độc lập (lỗi $0{,}75$ thay vì $1{,}25$), mẫu xác thực dùng một lần (dùng lại thích nghi làm hỏng (T7)). Hàng Hệ quả 04.15 còn cần hàm lỗi 0–1 và (T1); với danh sách hữu hạn, thuật toán học PAC bất khả diễn. Nguồn: ghi chú Bài 04, §4–§9.
- **Lý do / nối:** bảng tổng kết theo quy định → trả lời vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §4–§9.

#### `7-02` Vấn đề trung tâm — tổng kết · 1,5 phút
- **Mặt trang:** danh sách câu trả lời cho cả bài:
  - Sai số xấp xỉ không tăng khi lớp lớn hơn; sai số ước lượng bị chặn bởi $2r+\operatorname{opt}_S$.
  - Rủi ro thực nghiệm luôn chọn lớp lớn nhất; SRM chọn theo $m$ nhờ $\mathrm{pen}_k=\mathrm{rad}_k(m,\delta q_k)$.
  - Mười chỉ số đo, $m=10^4$: SRM chọn ba; cận $0{,}3651$, so với $0{,}4350$.
  - Bậc đa thức tốt nhất phụ thuộc $\sigma^2$, $f^*$; với $\lvert Y\rvert\le B$: mẫu xác thực.
  - SRM cần (T6); mẫu xác thực cần (T7), giá $2\sqrt{\ln(2K/\delta)/(2m_v)}$.
- **Ghi chú diễn giả:** Các câu trả lời theo thứ tự lập luận của bài. Câu hỏi thực hành của Bài 03 được trả lời trọn: với $10^4$ quan sát và xác suất ít nhất $0{,}95$, SRM dùng ba chỉ số đo, so với cận $0{,}4350$ khi dùng cả mười. Câu hỏi mở đầu chỉ được trả lời một phần: hàm lỗi bình phương không bị chặn, nên các cận đều của Bài 02–03 không áp dụng cho lớp đa thức; khi nhãn bị chặn và dự đoán được cắt, chọn bậc bằng mẫu xác thực có cận của Nhận xét 04.18. Chia xác suất thất bại làm bán kính tăng không quá khoảng $3{,}2\%$; bỏ $\delta$ khỏi đầu vào làm cỡ mẫu đủ tăng thêm khoảng $17{,}5\%$. Xác thực trả giá theo lôgarit của số ứng viên cộng phần dữ liệu không dùng để huấn luyện, còn SRM trả số hạng phạt trên toàn bộ tập huấn luyện. Chính quy hóa (regularization) cộng vào rủi ro thực nghiệm một số hạng nhân với hệ số $\lambda\ge0$; khi $\lambda$ được chọn trên chính tập huấn luyện, Định lý 04.11 không áp dụng. Nguồn: ghi chú Bài 04, §9.
- **Lý do / nối:** trả lời vấn đề của trang mở đầu cho cả bài → bài tập tổng hợp.
- **Mục tiêu / nguồn:** tất cả; §9.

#### `7-03` Bài tập: tối thiểu hóa rủi ro cấu trúc trên hai lớp hình chữ nhật — bài tập tổng hợp (Bài tập 04.7(c)), đề · 1,5 phút (1 phút tự làm)
- **Mặt trang:**
  - Phần (a): $\mathcal R_2\subseteq\mathcal R_5$ trên hai và năm chỉ số đo, $d=4$, $10$; $a_2$, $a_5$: sai số xấp xỉ.
  - **Câu hỏi:** khi không biết $a_2-a_5$, dùng SRM trên họ $(\mathcal R_2,\mathcal R_5)$ với $q_1=q_2=\tfrac12$ và dạng chiều VC của bán kính.
  - Gọi $\hat h_{(2)}$, $\hat h_{(5)}$ là nghiệm ERM trên hai lớp và $\hat h$ là đầu ra của SRM.
  - Tính hai số hạng phạt tại $m=10^4$, và viết quy tắc chọn theo hai rủi ro thực nghiệm.
- **Ghi chú diễn giả:** Hai lớp gồm các hình chữ nhật song song với trục; sai số xấp xỉ tính với cùng $L^*$. Bài toán dự đoán một biến cố tim mạch từ năm chỉ số: huyết áp, chỉ số khối cơ thể, tuổi, mức vận động, thu nhập; $\mathcal R_2$ chỉ dùng huyết áp và chỉ số khối cơ thể. Hàm lỗi 0–1, $\delta=0{,}05$, và hai lớp thỏa (M). Phần (a) cho bao hàm $\mathcal R_2\subseteq\mathcal R_5$, nên $a_5\le a_2$, và chiều VC $4$, $10$ (lớp hình chữ nhật trên $p$ đặc trưng có chiều VC $2p$, Bài tập 03.9; phép chiếu như ở ứng dụng chọn số chỉ số đo). Bài tập ghép ba phần của bài: phân tích sai số (mạch 2), chiều VC qua dạng chiều VC của bán kính, và SRM với bất đẳng thức oracle (mạch 4). Nguồn: tệp bài tập, Bài tập 04.7.
- **Lý do / nối:** bài tập tổng hợp của mạch Tổng kết, đúng câu chữ của `exercises.md` → lời giải.
- **Mục tiêu / nguồn:** 1, 3; Bài tập 04.7(c).

#### `7-04` Bài tập: tối thiểu hóa rủi ro cấu trúc trên hai lớp hình chữ nhật, lời giải — bài tập tổng hợp, lời giải trên mặt trang · 2 phút
- **Mặt trang:**
  - **Lời giải:** mỗi lớp nhận $\delta'=\delta/2=0{,}025$, nên $\ln(4/\delta')=\ln160\approx5{,}075$.
  - `[f]` $d=4$: $\mathrm{pen}_1=\sqrt{8(38{,}069+5{,}075)/10^4}\approx0{,}1858$; $d=10$: $\mathrm{pen}_2\approx0{,}2699$.
  - `[f]` SRM chọn $\mathcal R_5$ khi và chỉ khi $L_S(\hat h_{(5)})+0{,}2699<L_S(\hat h_{(2)})+0{,}1858$,
  - `[f]` tức khi rủi ro thực nghiệm giảm hơn $0{,}0841$ nhờ ba chỉ số thêm. Theo Định lý 04.11(b), xác suất $\ge0{,}95$:
  - `[f]` $$L_D(\hat h)-L^*\le\min\{a_2+0{,}3716,\ a_5+0{,}5399\}$$
- **Ghi chú diễn giả:** Với $d=4$, $4\ln(2e\cdot10^4/4)\approx38{,}069$; cộng $5{,}075$ và nhân $8\cdot10^{-4}$ được $0{,}03452$. Hai số trong vế phải là $2\,\mathrm{pen}_1$ và $2\,\mathrm{pen}_2$. Hiệu $0{,}5399-0{,}3716=0{,}1683$ gần ngưỡng $0{,}1693$ mà phần (b) tìm được khi so hai cận của từng lớp riêng tại $m=10^4$: SRM trả thêm một lượng nhỏ để chọn lớp từ dữ liệu. Phần (b) của bài còn cho thấy với $10^3$ quan sát, cả hai cận lớn hơn $1$ và không cho thông tin. Nguồn: tệp bài tập, Bài tập 04.7(b), (c).
- **Lý do / nối:** lời giải trên mặt trang, một bước một dòng → tự kiểm tra.
- **Mục tiêu / nguồn:** 1, 3; Bài tập 04.7(c).

#### `7-05` Câu hỏi tự kiểm tra — tổng kết · 2 phút
- **Mặt trang:**
  - **Câu hỏi:** trả lời và nêu kết quả đã dùng.
  1. Ví dụ 04.9 với $\tilde h\in\mathcal H_3$, $L_S(\tilde h)=0{,}185$, $\inf_{h\in\mathcal H_3}L_S(h)=0{,}175$: tính $\operatorname{opt}_S(\tilde h)$, dung sai $\tau$ và cận trên tin cậy.
  2. Bất đẳng thức oracle: số hạng nào giảm theo $m$, số hạng nào chỉ giảm nhờ bộ giải?
  3. Độ chệch bằng $0$ có kéo theo sai số xấp xỉ bằng $0$?
  4. Bỏ $\sum_kq_k\le1$: bước nào của chứng minh Bổ đề 04.9 hỏng?
- **Ghi chú diễn giả** (câu trả lời, mỗi câu trả lời được chỉ bằng ghi chú): (1) $\operatorname{opt}_S(\tilde h)=0{,}010$; mục tiêu có phạt tại $(3,\tilde h)$ là $0{,}185+0{,}1900=0{,}3750$, giá trị nhỏ nhất trên cả họ là $0{,}3650$, nên $\tau=0{,}010$; hai số bằng nhau vì giá trị nhỏ nhất đạt trên $\mathcal H_3$. Định lý 04.11(a) cho cận trên tin cậy $0{,}3751$ (chưa làm tròn $0{,}37504$), và (b) cho cận oracle cộng thêm $0{,}010$. (2) $2\,\mathrm{pen}_k$ giảm cỡ $\sqrt{\ln m/m}$; $\inf_{h\in\mathcal H_k}L_D(h)$ không phụ thuộc $m$, và trừ đi $L^*$ là sai số xấp xỉ; $\tau$ do bộ giải quyết định, cận không có cơ chế làm $\tau$ giảm khi thêm dữ liệu. (3) Không: ở Nhận xét 04.7, độ chệch bằng $0$ còn sai số xấp xỉ bằng $1$; độ chệch là tính chất của thuật toán, sai số xấp xỉ là tính chất của lớp. (4) Bất đẳng thức thứ hai ở bước hợp đếm được, $\sum_k\delta q_k\le\delta$; Ví dụ 04.8 cho xác suất thất bại $0{,}858$. Nguồn: ghi chú Bài 04, §11 và lời giải; Nhận xét 04.7; Bổ đề 04.9; Ví dụ 04.8.
- **Lý do / nối:** câu hỏi cuối buổi (1, 2) và hai điểm dễ nhầm (3, 4) → bài tập về nhà.
- **Mục tiêu / nguồn:** 1, 2, 3; §11.

#### `7-06` Bài tập về nhà — tổng kết · 1 phút
- **Mặt trang:** bảng `Mục | Bài tập`:

  | Mục | Bài tập |
  |---|---|
  | Phân tích sai số | 04.1 |
  | Độ chệch và phương sai | 04.2 |
  | Chia xác suất thất bại và tối thiểu hóa rủi ro cấu trúc | 04.3, 04.4, 04.7, 04.9, 04.10 |
  | Học không đều | 04.8, 04.11 |
  | Chọn mô hình bằng mẫu xác thực | 04.5, 04.6, 04.12, 04.13 |

  - Dòng liên kết: "Ghi chú bài giảng · Bài tập" (viewer, kèm `&deck=lecture-04-phan-tich-sai-so.html`).
- **Ghi chú diễn giả:** Sáu bài đầu là bài gốc, bảy bài sau chọn từ UML (§5.5, §7.8, §11.5). Mỗi bài xếp vào mạch cung cấp kiến thức cuối cùng nó cần: Bài tập 04.8 dùng Hệ quả 04.15; Bài tập 04.6 so ba quy tắc chọn bậc, trong đó có mẫu xác thực, và là bài thực nghiệm tùy chọn với một tập kiểm tra (test set) sinh riêng; Bài tập 04.13 so ERM trên hợp các lớp với chia huấn luyện–xác thực, và cách thứ hai cho cận nhỏ hơn từ $k_{\max}=119$ khi giả thuyết tốt nhất nằm trong lớp đầu. Bài tập 04.10 là bất đẳng thức oracle cho độ dài mô tả (Nhận xét 04.13). Nguồn: ghi chú Bài 04, §10; tệp bài tập Bài 04.
- **Lý do / nối:** ánh xạ bài tập vào mạch, mỗi bài một mạch → tài liệu.
- **Mục tiêu / nguồn:** tất cả; §10, `exercises.md`.

#### `7-07` Tài liệu tham khảo — tổng kết · 0,5 phút
- **Mặt trang:**
  - Shalev-Shwartz và Ben-David (2014), *Understanding Machine Learning: From Theory to Algorithms* (UML).
  - UML §5.2: phân tích sai số; §7.1–7.2: học không đều, SRM.
  - UML §11.1–11.2: chọn mô hình bằng SRM, xác thực.
  - Đọc thêm: UML §7.3, độ dài mô tả tối thiểu.
  - Bài 05: Hạ gradient, hạ gradient ngẫu nhiên và cận tối ưu. {{chữ, liên kết thêm khi deck Bài 05 có tên tệp}}
- **Ghi chú diễn giả:** Trước buổi học: UML §5.2, §7.1; sau buổi học: §7.2, §11.1, §11.2 và các bài tập §5.5, §7.8, §11.5. Khác biệt so với UML: UML gọi chính mức tốt nhất của lớp là sai số xấp xỉ và chỉ xét nghiệm ERM, còn học phần dùng rủi ro tham chiếu $L^*$, cận dưới đúng và $\operatorname{opt}_S$; phân tích độ chệch–phương sai là phần bổ sung của học phần; UML viết trọng số là $w$ và định nghĩa bán kính qua hàm cỡ mẫu hội tụ đều, học phần dùng $q_k$ và các bán kính tường minh của Bài 02–03; bất đẳng thức oracle phát biểu cho nghiệm có dung sai $\tau$, và Hệ quả 04.15 dùng xác suất thất bại $1/m$; Hệ quả 04.17 so với ứng viên tốt nhất sau bước lấy điều kiện. Cầu nối: ERM và SRM là các nguyên tắc thống kê, chưa cho cách tính nghiệm; bộ giải được đo bằng $\operatorname{opt}_S$ hoặc $\tau$, và $\tau$ cộng thẳng vào bất đẳng thức oracle. Bài 05 xét mục tiêu lồi, với hàm lỗi lồi theo tham số, và thuật toán hạ gradient ngẫu nhiên (stochastic gradient descent, SGD) có chiếu; câu hỏi là sau $T$ vòng lặp, độ chênh tối ưu (suboptimality) còn bao nhiêu và mỗi vòng tốn bao nhiêu phép tính. Nguồn: ghi chú Bài 04, §11, §12.
- **Lý do / nối:** trang cuối theo quy định → (hết).
- **Mục tiêu / nguồn:** —; §12.

## 7. Hành trình khái niệm

Thứ tự bước theo quy định: vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh (trang riêng) → kỹ thuật hoặc kiểm tra. Các bước có thể chung trang nhưng không đảo thứ tự trên mặt trang. Ví dụ đứng sau phát biểu chỉ khi ghi chú đặt nó sau phát biểu; khi đó nó là bước kiểm tra và được ghi ở cột cuối.

| Kết quả hoặc khái niệm | Vấn đề | Trực quan | Ví dụ | Phát biểu | Ý tưởng chứng minh | Kỹ thuật / kiểm tra | Gộp, `không áp dụng`, lý do |
|---|---|---|---|---|---|---|---|
| Rủi ro tham chiếu, sai số xấp xỉ, sai số ước lượng (Định nghĩa 04.1) | 1-06, 2-02 (lớp lớn nhất luôn thắng theo rủi ro thực nghiệm) | 2-03 (dòng mở; hình F1) | 2-03 (Ví dụ 04.2, F1) | 2-03 | `không áp dụng` (định nghĩa) | 2-03 dòng "Ví dụ." | Định nghĩa và ví dụ chung trang; hình F1 đặt ví dụ cạnh định nghĩa. |
| Sai số tối ưu thực nghiệm (Định nghĩa 04.2) | 2-04 (dòng mở: hai nguồn của sai số ước lượng) | 2-04 | 2-04 dòng "Lưu ý:" (Nhận xét 04.4, $-0{,}10$) | 2-04 | `không áp dụng` (định nghĩa) | 2-04 | Một trang; ví dụ là bước kiểm tra vì sao không dùng hiệu theo rủi ro kì vọng. |
| Mệnh đề 04.3 | 2-02, 2-04 | 2-05 (dòng "Trực quan.") | 2-03 (F1: phần đẳng thức trên số) | 2-05 | 2-06 | 2-07 (Ví dụ 04.3, ngưỡng $0{,}2310$); 2-08 (Bài tập 04.1(b)) | Ví dụ 04.3 là bước kiểm tra sau phát biểu, theo thứ tự ghi chú. |
| Định nghĩa 04.5 và Mệnh đề 04.6 | 3-01 (dòng mở), 2-02 (Ví dụ 04.1: rủi ro thực nghiệm chọn bậc $2$) | 3-02 (dòng "Trực quan."; hàm cố định) | 2-02 (Ví dụ 04.1) | 3-01, 3-02 | 3-03 | 3-04 (Ví dụ 04.4, bảng); 3-05 (bỏ độc lập: $0{,}75$ so với $1{,}25$); 3-06 (Nhận xét 04.7; Ví dụ 04.6 ở ghi chú diễn giả); 3-07 (Bài tập 04.2(d)) | Ví dụ 04.4 là bước kiểm tra sau phát biểu, theo thứ tự ghi chú. |
| Định nghĩa 04.8 và Bổ đề 04.9 | 2-07 (kết luận: hai cận chưa đồng thời), 4-01 (dòng mở) | 4-02 (dòng "Trực quan.") | 4-04 (Ví dụ 04.7, dòng "Ví dụ.") | 4-02 | 4-03 | 4-04 (kỹ thuật chia theo trọng số); 4-05 (Ví dụ 04.8: $0{,}858$) | Ví dụ 04.7 đứng sau phát biểu theo thứ tự ghi chú; gộp vào trang kỹ thuật. |
| Định nghĩa 04.10 và Định lý 04.11 | 4-06 (dòng mở: cận trên đồng thời) | 4-08 (dòng "Trực quan." và dòng mốc có phạt) | 4-07, 4-10 (Ví dụ 04.9, hình F2) | 4-06, 4-08 | 4-09 | 4-10 (so ERM trên $\mathcal H_{10}$, lớp biết trước); 4-11 (bỏ (T6): $0{,}0469$ so với $0{,}8$); 4-12 (Bài tập 04.4(b)); 7-03, 7-04 | Ví dụ 04.9 đứng sau phát biểu theo thứ tự ghi chú (cần Thuật toán 04.12); là bước kiểm tra bằng số. |
| Định nghĩa 04.14 và Hệ quả 04.15 | 5-01 (dòng mở: $\mathrm{pen}_k\to\infty$) | 5-02 (dòng "Trực quan.": $\delta=1/m$) | 5-03 dòng "Ví dụ." (cỡ mẫu $172\,279$; $181\,575$; $213\,317$) | 5-01, 5-02 | 5-03 | 5-04 (Ví dụ 04.11; Định lý 04.16, đọc thêm) | Phần số đứng sau hệ quả theo thứ tự ghi chú; gộp vào trang ý tưởng chứng minh làm bước kiểm tra. |
| (T7) và Hệ quả 04.17 | 6-01 (dòng "Trực quan.": SRM dùng cùng tập huấn luyện để chọn) | 6-01 | 6-03 (Ví dụ 04.12, hình F3) | 6-01 | 6-02 | 6-04 (Nhận xét 04.18: ba giới hạn, chọn bậc $0{,}4524$); 6-05 (Bài tập 04.5(a): $\ge0{,}6$ so với $0{,}1103$) | Ví dụ 04.12 là bước kiểm tra sau phát biểu, theo thứ tự ghi chú. |

Thời lượng theo mạch: 8 + 22 + 19 + 34 + 12 + 14 + 11 = 120 phút; 55 trang.

## 8. Hình vẽ

Mọi hình là SVG trong `2627-1/img/lec-04/`, `role="img"`, có `<title>` và alt cụ thể; màu không là tín hiệu duy nhất (kiểu nét và hình dạng điểm khác nhau cho từng dãy); chữ trong hình chỉ là nhãn trục, nhãn điểm, số và nhãn ngắn (Unicode), không công thức; công thức và chú thích nằm ở `figcaption` (KaTeX). Chú thích nêu dữ liệu. Dữ liệu chính xác lấy từ mục 5.

| Mã | Tệp | Trang | Nội dung và dữ liệu | Alt dự kiến |
|---|---|---|---|---|
| F1 (đã bỏ sau năm báo cáo duyệt, xem mục 17) | `phan-tich-sai-so.svg` | 2-03 | Trục dọc rủi ro kì vọng từ $0{,}15$ đến $0{,}35$ (vạch $0{,}15$; $0{,}20$; $0{,}25$; $0{,}30$; $0{,}35$). Cột trái "sáu hàm ngưỡng": vạch ngang nét đứt tại $0{,}18$ (nhãn "rủi ro Bayes 0,18"), nét liền tại $0{,}22$ (nhãn "h3: 0,22"), nét chấm tại $0{,}32$ (nhãn "h2: 0,32"); ngoặc từ $0{,}18$ đến $0{,}22$ nhãn "xấp xỉ 0,04", ngoặc từ $0{,}22$ đến $0{,}32$ nhãn "ước lượng 0,10". Cột phải "mọi hàm trên năm mức đo": vạch tại $0{,}18$ (nhãn "hàm Bayes 0,18"), nhãn "xấp xỉ 0". `figcaption`: "Ví dụ sàng lọc dưới $D_\eta$, $L^*=0{,}18$: lớp sáu hàm ngưỡng có $\min_tL_{D_\eta}(h_t)=0{,}22$ và $L_{D_\eta}(h_2)=0{,}32$; lớp mọi hàm $\{1,\ldots,5\}\to\{0,1\}$ chứa $\mathbb 1[x\in\{3,5\}]$." | "Hai cột trên cùng một trục rủi ro. Cột trái, lớp sáu hàm ngưỡng: rủi ro Bayes 0,18, mức tốt nhất 0,22 của h3, rủi ro 0,32 của h2; khoảng từ 0,18 đến 0,22 là sai số xấp xỉ 0,04, khoảng từ 0,22 đến 0,32 là sai số ước lượng 0,10. Cột phải, lớp mọi hàm: hàm Bayes thuộc lớp, sai số xấp xỉ bằng 0." |
| F2 | `srm-danh-doi.svg` | 4-10 | Trục ngang $k=1,\ldots,10$ (vạch từng số); trục dọc tuyến tính $[0;\ 0{,}5]$ (vạch $0$; $0{,}1$; …; $0{,}5$). Ba dãy, dữ liệu V10: $L_S(\hat h_k)$ (chấm tròn, nét liền) $0{,}300;\ 0{,}210;\ 0{,}175;\ 0{,}170;\ 0{,}166;\ 0{,}163;\ 0{,}160;\ 0{,}158;\ 0{,}156;\ 0{,}155$; $\mathrm{pen}_k$ (tam giác, nét đứt) $0{,}1423;\ \ldots;\ 0{,}2871$; tổng (ô vuông, nét đậm) $0{,}4423;\ \ldots;\ 0{,}4421$. Ô vuông tại $k=3$ tô đặc, nhãn "k = 3: 0,3650". Nhãn trực tiếp cuối dãy: "rủi ro thực nghiệm", "số hạng phạt", "tổng"; nhãn số tại $k=1$ và $k=10$. `figcaption`: "Ví dụ 04.9: $L_S(\hat h_k)$ của bảng, $\mathrm{pen}_k$ với $m=10^4$, $\delta=0{,}05$, $q_k=6/(\pi^2k^2)$, và tổng $L_S(\hat h_k)+\mathrm{pen}_k$; tổng nhỏ nhất $0{,}3650$ tại $k=3$." | "Đồ thị theo số chỉ số đo k từ 1 đến 10. Rủi ro thực nghiệm giảm từ 0,300 xuống 0,155, giảm nhanh đến k bằng 3 rồi gần như phẳng. Số hạng phạt tăng đều từ 0,142 lên 0,287. Tổng giảm từ 0,442, đạt nhỏ nhất 0,365 tại k bằng 3, rồi tăng lại đến 0,442 tại k bằng 10." |
| F3 | `can-xac-thuc.svg` | 6-03 | Trục ngang $m_v$ thang lôgarit từ $100$ đến $10^4$ (vạch $200$; $500$; $1000$; $2000$; $5000$); trục dọc tuyến tính $[0;\ 0{,}3]$ (vạch $0$; $0{,}1$; $0{,}2$; $0{,}3$). Đường liền $2\sqrt{\ln400/(2m_v)}$ trên $[150;\ 8000]$; năm chấm tròn có nhãn: $(200;\ 0{,}2448)$, $(500;\ 0{,}1548)$, $(1000;\ 0{,}1095)$, $(2000;\ 0{,}0774)$, $(5000;\ 0{,}0490)$. Hai đường ngang nét đứt tại $0{,}1$ và $0{,}05$, cắt đường cong tại $m_v\approx1198$ và $4793$, nhãn "1199" và "4794". `figcaption`: "Cận (a) của Hệ quả 04.17 với $K=10$, $\delta=0{,}05$ theo cỡ mẫu xác thực $m_v$ (Ví dụ 04.12)." | "Đường cong giảm theo cỡ mẫu xác thực trên trục lôgarit. Cận bằng 0,245 tại 200 quan sát, 0,155 tại 500, 0,109 tại 1000, 0,077 tại 2000 và 0,049 tại 5000. Cận xuống dưới 0,1 từ 1199 quan sát và dưới 0,05 từ 4794 quan sát." |

Mọi điểm có nhãn số của F1–F3 là số của ghi chú. Đường cong của F3 vẽ từ công thức của Ví dụ 04.12 (không có số mới trên nhãn).

## 9. Trang tổng kết

Chi tiết từng trang ở mục 6 (7-01 đến 7-07). Tóm tắt:
- **Bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh`:** sáu hàng: Mệnh đề 04.3, Mệnh đề 04.6, Bổ đề 04.9, Định lý 04.11, Hệ quả 04.15, Hệ quả 04.17 (7-01); bốn hàng xác suất giữ "xác suất $\ge1-\delta$", hàng Bổ đề 04.9 giữ "mọi $k$", hàng Mệnh đề 04.6 ghi "kì vọng". Phản ví dụ của bốn giả thiết ở ghi chú diễn giả.
- **Vấn đề trung tâm (7-02):** năm câu trả lời cho cả bài: phân tích sai số; rủi ro thực nghiệm so với SRM; câu hỏi thực hành ($k=3$, $0{,}3651$ so với $0{,}4350$); câu hỏi mở đầu (bậc phụ thuộc $\sigma^2$, $f^*$; mẫu xác thực khi $\lvert Y\rvert\le B$); giả thiết (T6), (T7) và giá của mẫu xác thực.
- **Bài tập tổng hợp (7-03, 7-04):** Bài tập 04.7(c), hai trang (đề; lời giải trên mặt trang).
- **Câu hỏi tự kiểm tra (7-05):** bốn câu, câu trả lời dự kiến ở ghi chú diễn giả: (1) $\operatorname{opt}_S=0{,}010$, $\tau=0{,}010$, cận trên tin cậy $0{,}3751$; (2) $2\,\mathrm{pen}_k$ giảm cỡ $\sqrt{\ln m/m}$, $\inf_{\mathcal H_k}L_D$ không đổi theo $m$, $\tau$ chỉ giảm nhờ bộ giải; (3) không, Nhận xét 04.7 (độ chệch $0$, sai số xấp xỉ $1$); (4) bất đẳng thức $\sum_k\delta q_k\le\delta$, Ví dụ 04.8 ($0{,}858$).
- **Bài tập về nhà (7-06):** bảng `Mục | Bài tập` ánh xạ mười ba bài vào mạch 2–6 (mục 6, 7-06); liên kết viewer.
- **Tài liệu tham khảo (7-07):** UML §5.2, §7.1–7.2, §11.1–11.2; đọc thêm §7.3; dòng chữ "Bài 05: Hạ gradient, hạ gradient ngẫu nhiên và cận tối ưu".
- **Câu nối sang bài sau** (ghi chú diễn giả 7-07): ERM và SRM là nguyên tắc thống kê, chưa cho cách tính nghiệm; $\tau$ cộng thẳng vào bất đẳng thức oracle; Bài 05 hỏi độ chênh tối ưu sau $T$ vòng lặp của hạ gradient ngẫu nhiên có chiếu.

## 10. Bảng thuật ngữ Việt–Anh của deck

Thuật ngữ xuất hiện trên mặt trang, theo ghi chú và `thuat-ngu.md` §8; tiếng Anh trong ngoặc ở lần dùng đầu trên một trang nội dung (cột "Trang đầu").

| Tiếng Việt | Tiếng Anh | Trang đầu |
|---|---|---|
| tối thiểu hóa rủi ro thực nghiệm | empirical risk minimization, ERM | 2-01 |
| bộ giải | solver | 2-01 |
| thiết kế cố định | fixed design | 2-02 |
| hàm lỗi bình phương | squared loss | 2-02 |
| rủi ro tham chiếu | reference risk | 2-03 |
| sai số xấp xỉ | approximation error | 2-03 |
| sai số ước lượng | estimation error | 2-03 |
| sai số tối ưu thực nghiệm | empirical optimization error | 2-04 |
| nhãn kiểm tra | test label | 3-01 |
| hàm hồi quy | regression function | 3-01 |
| phương sai nhiễu | noise variance | 3-01 |
| dự đoán trung bình | average prediction | 3-01 |
| độ chệch | bias | 3-01 |
| phương sai | variance | 3-01 |
| lỗi kiểm tra kì vọng | expected test error | 3-02 |
| ước lượng co | shrinkage estimator | 3-07 |
| bán kính hội tụ đều | uniform convergence radius | 4-01 |
| dạng chiều VC (của bán kính) | VC-dimension form | 4-01 |
| số hạng phạt | penalty | 4-02 |
| mục tiêu có phạt | penalized objective | 4-06 |
| dung sai | tolerance | 4-06 |
| nghiệm $\tau$-chính xác | $\tau$-accurate solution | 4-06 |
| tối thiểu hóa rủi ro cấu trúc | structural risk minimization, SRM | 4-06 |
| bất đẳng thức oracle | oracle inequality | 4-08 |
| mốc có phạt | penalized benchmark | 4-08 |
| học xấp xỉ với xác suất cao | probably approximately correct, PAC | 5-01 |
| thuật toán học không đều | nonuniform learner | 5-01 |
| giả thuyết so sánh | comparator hypothesis | 5-01 |
| mẫu xác thực | validation sample | 6-01 |
| chọn mô hình | model selection | 6-01 |
| dùng lại thích nghi | adaptive reuse | 6-04 |
| kiểm tra chéo | cross-validation | 6-04 |

Chỉ ở ghi chú diễn giả (tiếng Anh trong ngoặc ở đó): bình phương tối thiểu (least squares), hệ phương trình chuẩn (normal equations), thiết kế ngẫu nhiên (random design), đánh đổi độ chệch–phương sai (bias–variance tradeoff), học được không đều (nonuniformly learnable), cỡ mẫu xác thực (validation sample size), định lý không có bữa trưa miễn phí (no-free-lunch theorem), không tiền tố (prefix-free), bất đẳng thức Kraft (Kraft inequality), độ dài mô tả (description length), tập kiểm tra (test set), chính quy hóa (regularization), hạ gradient ngẫu nhiên (stochastic gradient descent, SGD), độ chênh tối ưu (suboptimality). Đã có ở Bài 01–03, không nhắc tiếng Anh: tách trọn vẹn, chiều VC, đại diện ($\epsilon$-representative có tiếng Anh ở Bài 02), bất đẳng thức hợp.

## 11. Rủi ro và điểm cần điều phối viên quyết định

1. **Kí hiệu và thuật ngữ của bản giao việc.** Bản giao việc viết "trọng số $w_k$" và "tập kiểm tra/kiểm định". Storyboard dùng $q_k$ (ghi chú, `ky-hieu.md` dòng 34) và "mẫu xác thực" (ghi chú §8, `thuat-ngu.md` dòng 254–255); "tập kiểm tra" chỉ ở ghi chú diễn giả 7-06 (Bài tập 04.6). Đề nghị điều phối viên xác nhận và sửa bản giao việc cho người viết deck.
2. **Số trang 55, đúng trần** (lý do ở mục 3). Phương án rút còn 53, không bỏ bước nào của hành trình khái niệm: (a) bỏ trang 3-07 (Bài tập 04.2(d)) và đưa lời giải vào ghi chú diễn giả 3-06; cụm độ chệch–phương sai khi đó không có bài tập trên mặt trang; (b) gộp 7-03 và 7-04 thành một trang khoảng $90$ âm tiết, ngoại lệ trần $60$ có lý do (câu chữ của bài tập), như trang bài tập tổng hợp $73$ âm tiết của deck Bài 01. Khuyến nghị giữ 55. Không khuyến nghị bỏ 4-05 hay 4-11: ghi chú §9 liệt kê hai phản ví dụ này trong bốn giả thiết không được bỏ.
3. **(T6), (T7) xuất hiện trên mặt trang ở nơi dùng lần đầu** (4-02, 6-01), không ở trang thiết lập 2-01, dù ghi chú đặt chúng ở §2. Lý do: (T6) nói về bán kính hội tụ đều $\mathrm{rad}_k$, chỉ được định nghĩa ở §6 (Định nghĩa 04.8, trang 4-01); đặt (T6) ở 2-01 sẽ dùng một thuật ngữ chưa định nghĩa trên mặt trang. (T7) đặt cạnh Hệ quả 04.17 cho cân đối. Thứ tự các khối của §4–§8 không đổi. Điều phối viên ghi quyết định này vào `review-log.md`.
4. **Ví dụ 04.1 chung trang với khối ứng dụng** (2-02), cả hai thuộc §3; câu hỏi mở đầu ($16$ quan sát) và câu hỏi cầu nối Bài 03 ($0{,}329\to0{,}560$) chung trang 1-06. Ví dụ 04.4 ở 3-04 dẫn "Ví dụ 04.1" bằng số khối thay cho nhắc lại dữ liệu.
5. **Kết quả và khối không có trang riêng:** Ví dụ 04.6 (ghi chú diễn giả 3-06); Nhận xét 04.4 (dòng "Lưu ý:" 2-04); Ví dụ 04.7 (dòng "Ví dụ." 4-04); Thuật toán 04.12 (một dòng 4-07, đầy đủ ở ghi chú diễn giả); Nhận xét 04.13, đọc thêm (ghi chú diễn giả 4-11); Định lý 04.16, đọc thêm (một dòng 5-04, không có trang ý tưởng chứng minh; phác thảo của Phụ lục D ở ghi chú diễn giả); Phụ lục A, E (ghi chú diễn giả). Nếu điều phối viên muốn Thuật toán 04.12 có trang riêng (mục tiêu 3 nói "tính lựa chọn ... từ một bảng", Bài tập 04.4(a) chạy thuật toán), deck lên 56: cần bỏ một trang theo điểm 2.
6. **Chính sách kỹ thuật.** Một trang "Kỹ thuật." mới: chia xác suất thất bại theo trọng số (4-04; dùng lại ở Hệ quả 04.15 và trong ghi chú Bài 07, nơi dẫn Bổ đề 04.9). Ba dòng "Kỹ thuật." chỉ dùng trong một chứng minh: thêm bớt kì vọng (3-03), chọn $\delta=1/m$ (5-03), lấy điều kiện theo tập huấn luyện (6-02). Dòng cuối có thể được Bài 06 dùng lại khi chọn mô hình bằng mẫu xác thực; ghi chú Bài 06 chỉ dẫn Hệ quả 04.17, không dẫn kỹ thuật, nên storyboard giữ một dòng. Nhắc lại bằng tên: bước tất định trên biến cố đại diện (2-06), chia $\delta/K$ (4-03), đảo cận đuôi thành bán kính và cỡ mẫu (6-03), cận dưới và cận trên cho chiều VC (ghi chú diễn giả 2-02). Bất đẳng thức hợp được dùng ở 4-03 (dạng đếm được) và nhắc lại ở 1-02 qua Định lý 02.14; không có dòng "Nhắc lại:" riêng cho tên kỹ thuật này trên mặt trang (mật độ 1-02); đề nghị chấp nhận vì 4-03 viết "Dạng đếm được của bất đẳng thức hợp".
7. **Bài tập trên mặt trang**, giữ dữ kiện, câu chữ và kết quả của `exercises.md`: 04.1(b) (2-08, kèm nhắc lại $S_\eta$ và bảng rủi ro của Ví dụ 01.5); 04.2(d) (3-07, với dữ kiện của phần (b): câu "Trong thiết lập của (b)" thành hai dòng dữ kiện và "với các số của (b)" thành "với các số trên"); 04.4(b) (4-12); 04.5(a) (6-05); 04.7(c) (7-03, 7-04, tổng hợp; dữ kiện của phần (a) thành một dòng). Lý do chọn 04.7(c) làm bài tổng hợp: ghép phân tích sai số ($a_2$, $a_5$), chiều VC và SRM với bất đẳng thức oracle, đúng câu hỏi trung tâm (chọn giữa hai lớp lồng nhau theo cỡ mẫu). Phương án khác: Bài tập 04.13(c) (ERM trên hợp so với chia huấn luyện–xác thực, ghép mạch 4 và 6), cần hai trang vì hai cận của (a), (b) và bảng ba dòng.
8. **Mục tiêu (1-03)** giữ đủ năm mục tiêu của ghi chú theo thứ tự, rút câu chữ trong trần $80$ (đếm $80$): mục tiêu 1 viết "chặn bằng ba số hạng" thay cho "chặn sai số ước lượng bằng một số hạng thống kê cộng sai số tối ưu thực nghiệm" (ghi chú diễn giả nêu ba số hạng); mục tiêu 3 bỏ "cho một họ đếm được các lớp bằng trọng số"; mục tiêu 4 bỏ vế "so sánh với học PAC bất khả diễn" (ghi chú diễn giả nêu); mục tiêu 5 viết "cận của mẫu xác thực". Nếu điều phối viên muốn giữ vế so sánh của mục tiêu 4, cần rút mục tiêu 3 còn "Chứng minh bất đẳng thức oracle; chọn lớp từ một bảng" (bỏ ý chia xác suất thất bại, vốn có ở từ khóa mạch 4).
9. **Thứ tự trong §5:** Ví dụ 04.6 (hàm phân lớp) đứng trước Nhận xét 04.7 trong ghi chú; deck đưa nó vào ghi chú diễn giả của trang Nhận xét 04.7 (3-06). Không đổi thứ tự trên mặt trang.
10. **Điểm toán học còn mở #47** (`planning/diem-toan-can-doc-2026-11-13.md`, mục 2): câu sau Bổ đề 04.9 nói $\delta$, $q_k$ vào "qua $\ln(1/\delta)+\ln(1/q_k)$", chỉ đúng cho hai bán kính cụ thể. Deck không viết khẳng định này cho bán kính tổng quát: mặt trang 4-02 không có nó; ghi chú diễn giả 4-02 và dòng "Ví dụ." 4-04 chỉ nói cho hai bán kính của Bài 02–03.
11. **Công thức cần đo ở 390 px** (ngắt `aligned` chỉ khi tràn): 2-03 (đẳng thức hai ngoặc), 2-05 (cận ba thành phần), 2-06 (chuỗi bốn quan hệ, gần như chắc chắn cần ngắt), 2-07 (hai cận trên một dòng; có thể tách hai dòng), 3-02, 3-05, 4-01, 4-06, 4-08, 4-09 (chuỗi ba bất đẳng thức), 5-01, 5-02, 6-01, 7-04; bảng 3-04 (bảy cột), 4-07, 4-12, 7-01 đặt trong `.table-scroll`.
12. **Trang sát trần** (đếm bằng script, mục 15): 1-02, 1-06, 2-01, 2-02, 2-03, 2-05, 2-06, 3-01, 3-02, 3-03, 3-05, 3-07, 4-04, 4-06, 4-08, 4-09, 5-01, 5-02, 5-04, 6-01, 6-02, 6-05, 7-02, 7-03, 7-05 (từ $58$ đến $60$); 1-03, 7-01 đúng $80$. Người viết deck không thêm chữ trên các trang này; điều phối viên đếm lại trên deck.
13. **Ghi chú diễn giả dẫn kết quả về sau hoặc bài sau** ở 1-01, 1-05 (câu trả lời theo mạch), 4-04 (Hệ quả 04.15, Bài 07), 7-07 (Bài 05): chỉ trong ghi chú diễn giả, không trên mặt trang.
14. **Liên kết hai chiều:** trang 7-06 của deck Bài 03 nhận liên kết tới `lecture-04-phan-tich-sai-so.html`; trang 7-07 ở đây là dòng chữ không liên kết cho đến khi deck Bài 05 có tên tệp.
15. **Hình F2 dùng rủi ro thực nghiệm "giả sử" của Ví dụ 04.9.** Ghi chú viết "Giả sử các nghiệm ERM có rủi ro thực nghiệm … như … bảng"; chú thích hình nêu đúng nguồn dữ liệu ("$L_S(\hat h_k)$ của bảng") và không dùng chữ "giả định" hay "minh họa". Dòng cuối 4-07 giữ chữ "Giả sử" như một giả thiết toán học của ví dụ.

## 12. Bảng đối chiếu trang → mục và khối của ghi chú

Cột "Đưa vào" ghi kí hiệu, thuật ngữ hoặc kết quả xuất hiện lần đầu trên mặt trang (định nghĩa hoặc "Nhắc lại:"), để kiểm quy tắc định nghĩa trước khi dùng.

| Trang | Mục ghi chú | Khối (số của ghi chú) | Đưa vào |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §9 | — (bằng lời) | — |
| 1-02 | Kiến thức tiên quyết; §2 | (T1)–(T5), (M); Định nghĩa 02.13; Định lý 02.14(a), 03.15(a) (nhắc lại) | (T1)–(T5), (M), $\ell$, $\epsilon$-đại diện, $L_S$, $L_D$, $D$, $\delta$, $r_m$, $\rho_m$ |
| 1-03 | Mục tiêu học tập | — | — |
| 1-04 | toàn bài; §12 | — | — |
| 1-05 | đoạn mở đầu | — | — |
| 1-06 | Câu hỏi mở đầu và hai đoạn sau | — | $(x_i,y_i)$, rủi ro thực nghiệm, $k$, rủi ro vượt mức |
| 2-00 | §1–§4 | — | — |
| 2-01 | §1, §2 | tám thành phần; bảng nguồn ngẫu nhiên | họ lớp $\mathcal H_1,\mathcal H_2,\ldots$, bộ giải, $\tilde h$, ERM, cố định / ngẫu nhiên |
| 2-02 | §3 | Ví dụ 04.1; khối ứng dụng | thiết kế cố định, $\zeta_i$, $\sigma^2$, $\mathcal P_j$, $\hat f^{(j)}$, hàm lỗi bình phương, $\mathcal H_k$, $d_k$, $m$ |
| 2-03 | §4 | Định nghĩa 04.1; đẳng thức sau nó; Ví dụ 04.2 | $L^*$, (T2), sai số xấp xỉ, sai số ước lượng, $h_2$, $h_3$ của ví dụ sàng lọc |
| 2-04 | §4 | Định nghĩa 04.2; (O2); Nhận xét 04.4 | $\operatorname{opt}_S$, $\epsilon_{\mathrm{opt}}$, (O2), $\hat h$ |
| 2-05 | §4 | Mệnh đề 04.3 | $r$, Mệnh đề 04.3 |
| 2-06 | §4 | chứng minh Mệnh đề 04.3 | — (nhắc lại bước tất định) |
| 2-07 | §4 | Ví dụ 04.3 | $a_2$, $a_{10}$, $\tilde h_2$, $\tilde h_{10}$, $L_D^{\mathrm{Bayes}}$ |
| 2-08 | §4; Bài 01 | Bài tập 04.1(b); Ví dụ 01.5 (nhắc lại) | $S_\eta$, $h_t$, $L_{D_\eta}$ |
| 3-00 | §5 | — | — |
| 3-01 | §5 | Định nghĩa 04.5 | $x$, $Y$, nhãn kiểm tra, $\hat f_S$, $f^*$, $\sigma^2(x)$, $\bar f$, độ chệch, phương sai |
| 3-02 | §5 | Mệnh đề 04.6; hai đoạn sau | lỗi kiểm tra kì vọng |
| 3-03 | §5 | chứng minh Mệnh đề 04.6 | — |
| 3-04 | §5 | Ví dụ 04.4 | $x_0$, $\zeta_0$, $w_i$ |
| 3-05 | §5 | Ví dụ 04.5 | $\mu$, $\bar Y$ |
| 3-06 | §5 | Nhận xét 04.7; Ví dụ 04.6 (ghi chú diễn giả) | — |
| 3-07 | §5 | Bài tập 04.2(d) | ước lượng co, $\gamma$ |
| 4-00 | §6 | — | — |
| 4-01 | §6 | Định nghĩa 04.8 và ba đoạn sau | $\mathrm{rad}_{\mathcal H}$, $\delta'$, bán kính hội tụ đều, dạng chiều VC |
| 4-02 | §2 (T6), §6 | Bổ đề 04.9 | (T6), $q_k$, $\mathrm{rad}_k$, $\mathrm{pen}_k$, số hạng phạt |
| 4-03 | §6 | chứng minh Bổ đề 04.9 | $B_k$, $K$ |
| 4-04 | §6 | Bổ đề 04.9 (kỹ thuật); Ví dụ 04.7 | — |
| 4-05 | §6 | Ví dụ 04.8 | $k_{\max}$, $h_k$ |
| 4-06 | §6 | Định nghĩa 04.10 và đoạn sau | mục tiêu có phạt, $\tau$, $(\hat k,\hat h)$, SRM |
| 4-07 | §6 | Ví dụ 04.9 Bước 1; Thuật toán 04.12 (một dòng) | $\hat h_k$, $v$, (O1) |
| 4-08 | §6 | Định lý 04.11 và đoạn sau | bất đẳng thức oracle, mốc có phạt |
| 4-09 | §6 | chứng minh Định lý 04.11 | $E$ |
| 4-10 | §6 | Ví dụ 04.9 Bước 2–5 | — |
| 4-11 | §6 | Ví dụ 04.10; Nhận xét 04.13 (ghi chú diễn giả) | $F_+$, $\mathcal G_S$, $\mathbb 1_{F_+}$, $B_2$ |
| 4-12 | §6 | Bài tập 04.4(b) | — |
| 5-00 | §7 | — | — |
| 5-01 | §7 | Định nghĩa 04.14 và hai đoạn sau; Định nghĩa 01.25 (nhắc lại) | PAC, học PAC bất khả diễn, $M$, thuật toán học không đều, giả thuyết so sánh |
| 5-02 | §7 | Hệ quả 04.15 | $\mathrm{pen}_k(m)$, $A_{\mathrm{SRM}}$, $M_k(\epsilon)$, $k(h)$ |
| 5-03 | §7; Phụ lục B | chứng minh Hệ quả 04.15; phần đọc bằng số | $E_m$ |
| 5-04 | §7 | Ví dụ 04.11; Định lý 04.16 (đọc thêm) | $\mathbb 1_F$, $\mathcal H_j$, $q_j$ |
| 6-00 | §8 | — | — |
| 6-01 | §2 (T7), §8 | Hệ quả 04.17 | (T7), $V$, $m_v$, $L_V$, $g_j$, $K$, $\hat g$, mẫu xác thực, chọn mô hình |
| 6-02 | §8 | chứng minh Hệ quả 04.17 | — |
| 6-03 | §8 | Ví dụ 04.12 | — |
| 6-04 | §8 | Nhận xét 04.18 và đoạn sau | $B$, dùng lại thích nghi, kiểm tra chéo |
| 6-05 | §8 | Bài tập 04.5(a) | $g_{11}$, $F_+(V)$ |
| 7-00 | §9–§12 | — | — |
| 7-01 | §4–§9 | Mệnh đề 04.3, 04.6, Bổ đề 04.9, Định lý 04.11, Hệ quả 04.15, 04.17 | — |
| 7-02 | §9 | — | — |
| 7-03 | Bài tập 04.7 | Bài tập 04.7(c) (đề), (a) (dữ kiện) | $\mathcal R_2$, $\mathcal R_5$, $a_2$, $a_5$, $\hat h_{(2)}$, $\hat h_{(5)}$ |
| 7-04 | Bài tập 04.7 | Bài tập 04.7(c) (lời giải) | — |
| 7-05 | §11 | câu hỏi cuối buổi và lời giải | — |
| 7-06 | §10 | `exercises.md` | — |
| 7-07 | §11, §12 | — | — |

## 13. Đề xuất sửa ghi chú và tệp bài tập (không sửa; chờ điều phối viên và tác giả)

Không thấy lỗi toán học trong các khối deck dùng; mọi con số của ví dụ và năm bài tập trên mặt trang đã tính lại (mục 5) và khớp ghi chú, tệp bài tập. Không có đề xuất sửa ghi chú mới. Hai điểm đã mở từ trước, deck không phụ thuộc vào chúng:

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất |
|---|---|---|---|---|
| nhẹ | ghi chú, câu sau **Bảo đảm.** của Bổ đề 04.9 | Dạng phụ thuộc "$\ln(1/\delta)+\ln(1/q_k)$" chỉ đúng cho hai bán kính cụ thể (điểm toán học #47, còn mở cho tác giả) | `planning/diem-toan-can-doc-2026-11-13.md`, mục 2 | Như đề xuất đã ghi; deck tránh khẳng định này (mục 11, điểm 10). |
| nhẹ | `ky-hieu.md` | Chưa có $\bar y(x)$ (Ví dụ 04.6) và $\zeta_0$ (Ví dụ 04.4) | `lec-04/review-log.md`, "Còn mở cho tác giả" | Thêm hai dòng; deck chỉ dùng $\zeta_0$ trên mặt trang 3-04. |

## 14. Danh sách kỹ thuật đã giới thiệu đến hết Bài 04

| Kỹ thuật | Bài, trang (lần đầu) | Dạng | Trong deck Bài 04 |
|---|---|---|---|
| Tính tuyến tính của kì vọng | Bài 01, `L01-3-03` | một dòng | không dùng |
| Bất đẳng thức hợp | Bài 01, `L01-4-04` | trang riêng | dạng đếm được ở 4-03, 4-04 |
| Chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ | Bài 01, `L01-6-07` | trang riêng | không dùng |
| Tối thiểu hóa từng điểm rồi lấy kì vọng | Bài 01 | một dòng | không dùng |
| Phương pháp Chernoff | Bài 02, `L02-3-01` | trang riêng | không dùng trực tiếp (qua Hoeffding ở 6-02) |
| Dây cung của hàm lồi và Taylor bậc hai tại $0$ | Bài 02 | một dòng | không dùng |
| Đảo cận đuôi thành bán kính và cỡ mẫu | Bài 02, `L02-4-04` | trang riêng | "Nhắc lại:" ở 6-03 |
| Chia xác suất thất bại $\delta/K$ cho từng giả thuyết | Bài 02, `L02-5-05` | trang riêng | nhắc tên ở 4-03 (trường hợp $q_k=1/K$) |
| Bước tất định trên biến cố đại diện | Bài 02, `L02-5-11` | trang riêng | "Nhắc lại:" ở 2-06; dùng ở 4-09 |
| Cận dưới và cận trên cho chiều VC | Bài 03, `L03-2-04` | trang riêng | ghi chú diễn giả 2-02 ($d_k=k+1$) |
| Thứ tự trên đường thẳng cho cận trên | Bài 03 | một dòng | không dùng |
| Hàm afin giữ tổ hợp lồi (với phân hoạch Radon) | Bài 03 | một dòng | không dùng |
| Tách theo nhãn của điểm cuối rồi quy nạp | Bài 03 | một dòng | không dùng |
| Đối xứng hóa và mẫu bóng | Bài 03, `L03-5-06` | trang riêng | không dùng |
| Hàm tăng trưởng thay cho số giả thuyết | Bài 03, `L03-5-07` | trang riêng | qua $\rho_m$ và dạng chiều VC (1-02, 4-01) |
| Bất đẳng thức tiếp tuyến $\ln u\le u/u_0+\ln u_0-1$ để giải cỡ mẫu | Bài 03 | một dòng (ghi chú diễn giả) | không dùng |
| Thêm bớt kì vọng rồi bình phương; mỗi số hạng chéo một lý do | Bài 04, 3-03 | một dòng | — |
| **Chia xác suất thất bại theo trọng số** | Bài 04, 4-04 | trang riêng | dùng ở 4-02 đến 4-05, 5-03; dùng lại ở Bài 07 |
| Chọn $\delta=1/m$ để bỏ $\delta$ khỏi đầu vào | Bài 04, 5-03 | một dòng | — |
| Lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện | Bài 04, 6-02 | một dòng | — |

Mã trang của Bài 02, 03 lấy theo storyboard đã duyệt; nếu deck Bài 02, 03 đổi mã, người viết deck Bài 04 không cần mã (deck nhắc kỹ thuật bằng tên). Deck Bài 05 trở đi nhắc lại "chia xác suất thất bại theo trọng số" bằng tên, một dòng "Nhắc lại:".

## 15. Mật độ mặt trang đo bằng script

Đếm bằng `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-04/storyboard/count.py` trên văn bản dự kiến của mục 6, theo cách của `deck_check.py`: token cách nhau bởi khoảng trắng, có chữ cái hoặc chữ số; bỏ tiêu đề, công thức `$…$`, ghi chú `{{…}}` của người lập, dấu fragment; nhãn "(T1)", "(M)", "(a)", số khối như "04.11" và tiếng Anh trong ngoặc được đếm (quyết định Bài 01: số viết trong câu có tính). Ô bảng chỉ chứa số hoặc công thức không đếm. Mỗi gạch đầu dòng là một dòng; mỗi công thức hiển thị là thêm một dòng (số 0 trong cột theo dòng); một bảng là một dòng. Các chữ chỉ dẫn bố cục "Thẻ trái,", "Thẻ phải," của 2-02 được đếm nên số thật của trang này thấp hơn bốn. Trang tổng quan và trang tiêu đề mạch không đếm (bìa 46 âm tiết luận điểm; hộp Vấn đề trung tâm 26; câu dẫn mạch 19–23).

| Trang | Tổng | Dòng | Theo dòng | Trang | Tổng | Dòng | Theo dòng |
|---|---:|---:|---|---|---:|---:|---|
| 1-02 | 59 | 5 | 12; 20; 2; 13; 12 | 4-06 | 60 | 6 | 15; 12; 6; 0; 12; 15 |
| 1-03 | 80 | 5 | 18; 16; 16; 16; 14 | 4-08 | 60 | 6 | 13; 14; 12; 7; 0; 14 |
| 1-06 | 60 | 4 | 11; 17; 16; 16 | 4-09 | 58 | 6 | 16; 0; 13; 10; 8; 11 |
| 2-01 | 58 | 4 | 14; 20; 12; 12 | 4-07 | 41 | 4 | 9; 17; 14 (bảng 1) |
| 2-02 | 60 | 6 | 20; 10; 10; 5; 5; 10 | 4-10 | 53 | 5 | 9; 10; 13; 11; 10 |
| 2-03 | 59 | 5 | 13; 18; 15; 0; 13 | 4-11 | 57 | 6 | 6; 9; 3; 11; 15; 13 |
| 2-04 | 57 | 5 | 20; 17; 0; 10; 10 | 4-12 | 46 | 6 | 13; 9; 4; 8; 12 |
| 2-05 | 60 | 6 | 16; 15; 7; 0; 13; 9 | 5-01 | 59 | 6 | 8; 19; 16; 0; 11; 5 |
| 2-06 | 59 | 6 | 12; 6; 0; 17; 18; 6 | 5-02 | 59 | 6 | 14; 20; 7; 8; 0; 10 |
| 2-07 | 55 | 6 | 5; 13; 9; 0; 12; 16 | 5-03 | 44 | 6 | 7; 3; 4; 7; 16; 7 |
| 2-08 | 52 | 6 | 12; 8; 15; 10; 7 | 5-04 | 58 | 5 | 11; 4; 15; 10; 18 |
| 3-01 | 58 | 5 | 17; 19; 10; 9; 3 | 6-01 | 60 | 6 | 20; 11; 15; 9; 0; 5 |
| 3-02 | 60 | 5 | 13; 17; 17; 0; 13 | 6-02 | 60 | 5 | 13; 14; 7; 16; 10 |
| 3-03 | 58 | 6 | 7; 0; 13; 11; 9; 18 | 6-03 | 28 | 5 | 8; 2; 1; 13; 4 |
| 3-04 | 50 | 5 | 9; 6; 11; 16 (bảng 8) | 6-04 | 55 | 5 | 9; 15; 12; 11; 8 |
| 3-05 | 59 | 6 | 13; 13; 12; 0; 5; 16 | 6-05 | 60 | 6 | 13; 14; 14; 8; 5; 6 |
| 3-06 | 54 | 5 | 18; 9; 15; 7; 5 | 7-01 | 80 | 1 | — (bảng 80) |
| 3-07 | 60 | 6 | 9; 5; 20; 13; 11; 2 | 7-02 | 60 | 5 | 17; 13; 10; 11; 9 |
| 4-01 | 57 | 6 | 10; 20; 0; 9; 10; 8 | 7-03 | 60 | 4 | 13; 17; 13; 17 |
| 4-02 | 54 | 5 | 15; 16; 10; 13; 0 | 7-04 | 31 | 5 | 6; 0; 6; 19; 0 |
| 4-03 | 53 | 6 | 9; 11; 8; 0; 13; 12 | 7-05 | 60 | 5 | 10; 12; 17; 11; 10 |
| 4-04 | 58 | 5 | 18; 13; 14; 4; 9 | 7-06 | 47 | 2 | 12 (bảng 35) |
| 4-05 | 54 | 6 | 7; 9; 5; 11; 10; 12 | 7-07 | 54 | 5 | 12; 11; 9; 10; 12 |

Trần: 60 cho trang nội dung, 80 cho 1-03, 7-01, 7-06; mọi dòng ≤ 20; mọi trang ≤ 6 dòng. Kết quả: không trang nào vượt. Ngoại lệ: không có. Trang bài tập giữ câu chữ của `exercises.md` nhờ tách đề và lời giải của bài tổng hợp thành hai trang (7-03, 7-04).

## 16. Đối chiếu với deck cuối (người viết deck, 2026-11-15)

Deck: `2627-1/lecture-04-phan-tich-sai-so.html`, 55 trang, mã trang theo mục 6 sau khi đổi số ở mạch 4. Hình: `img/lec-04/phan-tich-sai-so.svg` (F1), `srm-danh-doi.svg` (F2), `can-xac-thuc.svg` (F3), sinh bằng script trong thư mục nháp của người viết (`…/scratchpad/lec-04/writer/make_svg.py`, tính lại $\mathrm{pen}_k$, tổng nhỏ nhất $0{,}365044$, cận xác thực và hai giao điểm $1198{,}3$; $4793{,}2$). Các quyết định của điều phối viên (N1, T1–T8, 19 phát hiện nhẹ) đã áp dụng như dưới.

**Lệch storyboard và lý do.**

| Trang | Lệch | Lý do |
|---|---|---|
| 4-07, 4-08, 4-09 | Ví dụ 04.9 (trước là 4-09) đặt ngay sau 4-06; Định lý 04.11 thành 4-08, ý tưởng chứng minh thành 4-09; mã trang trong toàn tệp này đã đổi theo | T5: ví dụ trước phát biểu, 4-07 chỉ cần Định nghĩa 04.10 và $\mathrm{pen}_k$ |
| 2-01, 2-02, 4-07, 4-08, 5-02, 6-01, 6-03 | Tiêu đề rút gọn (xem tiêu đề mục 6) | tiêu đề dài chiếm hai dòng làm tràn khung 1600×900; "SRM" đã có tiếng Anh ở 4-06 |
| 2-01 | Bỏ dòng "Mục tiêu: …" | T6; ý đã ở 2-03 |
| 2-02 | Bỏ nhãn "Ứng dụng."; thẻ phải mở bằng "**Ví dụ.**"; "chiều VC (Bài 03)" | L4; nhắc lại khái niệm bài trước |
| 2-03 | Không có công thức hiển thị: sai số xấp xỉ và sai số ước lượng định nghĩa trong danh sách, "Phân tích sai số (error decomposition): $L_D(h)-L^*$ bằng tổng hai sai số"; dòng "Ví dụ." chỉ nêu thiết lập ($D_\eta$, Ví dụ 01.2, $h_t=\mathbb 1[x\ge t]$, $L^{\mathrm{Bayes}}_{D_\eta}=0{,}18$), số $0{,}04$; $0{,}10$ đọc trên hình; dòng mở "Lớp thay đổi thì …" sang ghi chú diễn giả | T2, L13; định nghĩa, công thức hiển thị và hình F1 dọc không vừa một khung |
| F1 | Vẽ lại dạng ngang (hai hàng trên một trục rủi ro, $1000\times192$), hiển thị `figure short-s` | chữ trong hình ≥ 17 px ở 1600×900; hình dọc không vừa trang |
| 1-02 | Thêm công thức $r_m$ trên mặt trang; (M) viết "xấp xỉ từng điểm bởi lớp con đếm được" | L14; trần mật độ |
| 1-03 | Mục tiêu 1, 4 theo câu chữ cổng duyệt đề xuất (rút "một", "mà") | quyết định 11.5, trần 80 |
| 2-05 | "Trực quan." nêu cơ chế ($L_D\to L_S$ tại $\tilde h$, ngược lại tại $h$: $2r$; bộ giải: $\operatorname{opt}_S$); phần (b) tách hai dòng | L12; dòng ≤ 20 âm tiết |
| 2-06, 4-09 | Chuỗi bất đẳng thức của 2-06 ngắt bằng `aligned` (hai dòng) | tràn ở 1600×900 khi một dòng |
| 2-07 | Thêm "Nhắc lại:" dạng chiều VC của Định lý 03.15(b) | định nghĩa trước khi dùng |
| 2-08 | Dòng nhắc lại không chép $S_\eta$ (đưa vào ghi chú diễn giả); bảng giữ $L_{S_\eta}$, $L_{D_\eta}$ | vừa khung |
| 3-04 | Cột "độ chệch bình phương" viết "(độ chệch)$^2$"; dòng 2 nêu "tổng: (độ chệch)$^2$ + phương sai" | vừa khung |
| 3-05 | Câu số hạng chéo sửa dấu | T1 |
| 3-07 | Gộp dữ kiện một dòng; "với các số trên" bỏ (dữ kiện đã là các số của (b)); lời giải hai fragment, fragment hai nêu lý do hai số khác nhau | L9, trần 60 |
| 4-01 | Hai bán kính viết "$r_m$ khi (T4); $\rho_m$ tại $\delta'$ khi …"; dạng chiều VC là công thức hiển thị | T6 |
| 4-02, 6-01 | (T6), (T7) viết "Họ lớp cố định trước khi lấy mẫu (T6): …", "Mẫu xác thực độc lập (T7): …", không in đậm | L3; `deck_lint.py` coi nhãn in đậm "(T6) …." là nhãn ngoài danh sách |
| 4-02 | "Trực quan." thêm ví dụ $q_k=2^{-k}$ ($0{,}025$; $0{,}0125$; … tổng $0{,}05$) và tên tiếng Anh confidence allocation | T5, L13 |
| 4-03 | Thêm "Nhắc lại:" chia $\delta/K$ (Bài 02) là trường hợp $q_k=1/K$ | mục 14 |
| 4-04 | "Dùng khi lớp hoặc giả thuyết được chọn theo dữ liệu."; dòng "Ví dụ." nêu thiết lập | L1, L2 |
| 4-06 | Hai dòng cuối gộp thành một | T6 |
| 4-07 | Bảng hai nhóm cột ($k=1$–$5$ và $6$–$10$), số viết chữ thường thay KaTeX; dòng Thuật toán 04.12 thêm "($\mathrm{pen}_k$ không giảm)" và "SRM chọn $\hat k=3$"; "không tăng vì lồng nhau" sang ghi chú diễn giả | L10; bảng mười dòng không vừa khung |
| 4-08 | "Trực quan." nêu nguồn của $2\,\mathrm{pen}_k$; dòng mốc có phạt: "vế phải của (b)"; "không tăng khi lớp lồng nhau lớn dần" sang ghi chú diễn giả | L5; trần 60 |
| 4-10 | Phép cộng $0{,}155+0{,}27992$, $0{,}175+0{,}18428$ và hiệu $0{,}0058$ sang ghi chú diễn giả; mặt trang giữ $0{,}3651$, $0{,}4350$, $0{,}3593$, $0{,}0130$ | vừa cột chữ cạnh F2 |
| 4-11 | Kết luận: "(T6) không thỏa; biến cố hỏng $B_2$ xảy ra chắc chắn"; $\Pr(B_2)\le\delta/2$ sang ghi chú diễn giả | vừa khung |
| 4-12 | Câu hỏi tách hai dòng; hai fragment cuối gộp; câu "trọng số chỉ vào qua $\ln(1/q_k)$" sang ghi chú diễn giả | dòng ≤ 20, vừa khung |
| 5-01 | Dòng mở theo L6; "Nhắc lại:" học PAC bất khả diễn (agnostic PAC learning) theo tên của ghi chú; bỏ dòng "$M$ phụ thuộc $h$ …" | L6, T6 |
| 5-02, 5-03 | N1: dòng bán kính (Định lý 02.14(a) khi hữu hạn, 03.15(a) khi còn lại), trọng số "chọn trước", dòng "Kí hiệu:" $M_k(\epsilon)$, $k(h)$ bằng công thức; phần (b) chuyển sang bước 4 của 5-03 (phát biểu đủ ở ghi chú diễn giả 5-02); bước 2 viết "$\mathrm{pen}_k(m)\le\sqrt{(a+b\ln m)/m}$" | N1, L7 |
| 5-04 | Định lý 04.16(a) với "Giả thiết:"/"Bảo đảm:", phát biểu bằng "có thuật toán học không đều cho $\mathcal H$" (mặt trang chưa định nghĩa từ "học được không đều"); "(Bài 03)" sau "tách trọn vẹn"; đoạn Phụ lục D rút trong ghi chú diễn giả | L8, T8 |
| 6-01 | Hai phần (a), (b) viết trong dòng, không công thức hiển thị | vừa khung |
| 6-02 | Dòng "Nhắc lại:" nội dung của Hệ quả 02.16(a) và Định lý 02.14(b) với (T1), (T3), (T4) | T4 |
| 6-03 | Các giá trị theo $m_v$ chỉ trên F3 (và ghi chú diễn giả) | vừa cột chữ cạnh F3 |
| 7-01 | Loại bảo đảm ghi ở tiêu đề cột "Kết quả (xác suất $\ge1-\delta$, mọi $D$; trừ 04.6)"; cột kết quả nêu đại lượng được chặn dạng ngắn; Định lý 04.11: "cận đồng thời"; Hệ quả 04.15: "(T6), $d_k<\infty$" | L11, vừa khung |
| 7-02 | Ba dòng giữ "xác suất $\ge1-\delta$", "lớp lồng nhau", "dự đoán cắt" | T7 |
| 7-03 | Dòng $\mathcal R_5$, $\mathcal R_2$ và dòng dữ kiện phần (a), (b); (M) và "cùng $L^*$" sang ghi chú diễn giả | T3 |
| 7-06 | Liên kết viewer có `&deck=` | — |
| 7-07 | Dòng chữ "Bài 05: Hạ gradient, hạ gradient ngẫu nhiên và cận tối ưu." không liên kết | chưa có deck Bài 05 |
| mọi bảng | Không dùng `.table-scroll` | lớp này không có trong `lecture-course.css`; chế độ đọc màn hẹp đã cho bảng cuộn ngang tại chỗ |
| ghi chú diễn giả | Viết lại theo T8, L17, L18, L19 (không "Mạch này", không câu quy trình), ≤ 150 âm tiết (≤ 250 ở trang chứng minh) | T8 |

**Ngoại lệ mật độ:** 7-03, 76 âm tiết (`deck_lint.py`, có tính số trong câu): câu chữ của Bài tập 04.7(c) chiếm 47 âm tiết, cộng dòng mô tả $\mathcal R_5$, $\mathcal R_2$ và dữ kiện phần (a), (b) mà T3 yêu cầu trên mặt trang. 7-01 là bảng tổng kết, 71 (trần 80; `deck_check.py` báo SYLL vì tiêu đề "Bảng tổng kết" không nằm trong danh sách tiêu đề trần 80 của script).

**Mật độ cuối** (âm tiết, có tính số viết ngoài KaTeX / số dòng / âm tiết ghi chú diễn giả không kể KaTeX): 1-01 61/4/127 (bìa); 1-02 58/5/83; 1-03 80/5/86; 1-04 39/7/84 (Nội dung); 1-05 26/1/132; 1-06 58/4/105; 2-01 46/3/90; 2-02 54/6/97; 2-03 47/4/113; 2-04 50/5/88; 2-05 60/6/106; 2-06 59/6/154; 2-07 56/6/101; 2-08 47/5/70; 3-01 57/5/76; 3-02 59/5/91; 3-03 58/5/112; 3-04 29/4/98; 3-05 60/6/63; 3-06 56/5/85; 3-07 59/5/82; 4-01 56/6/126; 4-02 59/5/83; 4-03 60/6/105; 4-04 58/5/68; 4-05 52/6/62; 4-06 50/5/93; 4-07 32/3/93; 4-08 57/5/119; 4-09 57/6/148; 4-10 26/4/113; 4-11 57/6/122; 4-12 31/5/82; 5-01 55/5/102; 5-02 60/5/81; 5-03 39/6/139; 5-04 60/6/104; 6-01 59/5/75; 6-02 60/6/134; 6-03 22/4/97; 6-04 58/5/107; 6-05 60/6/102; 7-01 71/1/142; 7-02 59/5/123; 7-03 76/5/104; 7-04 32/5/70; 7-05 59/5/116; 7-06 40/2/85; 7-07 56/5/121. Mục 15 giữ số của bản dự kiến.

**Kiểm tra máy:** `deck_check.py`: console 0, pageerrors 0, failed 0, `.katex-error` 0; OVERFLOW chỉ ở đuôi SVG của `\sqrt` (báo động giả đã biết); ở 390 px `docScrollW` = 390 trên mọi trang. `footer_check.py`: 0 trang. `deck_lint.py`: chỉ 7-03 (ngoại lệ trên).

## 17. Sửa sau năm báo cáo duyệt (người sửa, 2026-11-15)

Đầu vào: `reviews/deck-{hoc-vien,toan-hoc,chuyen-gia,su-pham,mach-truyen}.md` và quyết định của điều phối viên trong `review-log.md` (chấp nhận mọi phát hiện). Kí hiệu nguồn: HV (học viên, theo thứ tự hàng), TH (toán học, số hiệu của báo cáo), CG (chuyên gia, theo thứ tự hàng), SP (sư phạm, theo thứ tự hàng), MT (mạch truyện, số hiệu của báo cáo). Mặt trang và ghi chú diễn giả trong mục 6 được thay bằng bản deck ở những trang ghi dưới đây; mục 16 giữ lịch sử của bản viết.

**Thay đổi chung.**
- Hình F1 (`phan-tich-sai-so.svg`) bỏ khỏi deck và xóa khỏi `img/lec-04/`: mọi số của Ví dụ 04.2 ($0{,}18$; $0{,}22$; $0{,}32$; $0{,}04$; $0{,}10$) nay ở dòng "Ví dụ." của 2-03 (HV nghiêm trọng, MT19). Đặt cả hình và dòng số trên một trang thì tràn khung 1600×900; ở 390 px chữ trong hình còn khoảng 7 px.
- F3 thêm nhãn trục tung "cận (a)" (SP49).
- Tiêu đề 5-02, 5-03 viết $1/m$ bằng KaTeX.
- Thẻ meta viewport giữ như điều phối viên đã sửa; không đặt lại `user-scalable=no`.
- Mạch 5, 6, 7: dòng dẫn đổi theo SP và TH (mục 3 đã cập nhật).

| Phát hiện | Trang | Sửa | Trạng thái |
|---|---|---|---|
| HV1 (nghiêm trọng) | 2-03 | Số của Ví dụ 04.2 lên chữ; bỏ F1 | đã sửa |
| HV2 | 4-10, 6-03 | Các số dùng trên trang đã có trong chữ (4-10: $0{,}3651$; $0{,}4350$; $0{,}3593$; $0{,}0130$; 6-03: $0{,}1095$; $1199$; $4794$; $0{,}1871$); cỡ hình ở 390 px do CSS chung quyết định | đã sửa một phần: cỡ hình ở màn hẹp cần đổi CSS, ngoài phạm vi ghi |
| HV3 | 4-08, 4-10, 4-11, 7-05 | 4-08 (a) gọi tên "cận trên tin cậy"; 4-10 "cận trên tin cậy mức $95\%$" | đã sửa |
| HV4 | 4-07, 4-11 | "**Ví dụ 04.9.**", "**Ví dụ 04.10.**" ở đầu trang | đã sửa |
| HV5 | 5-01 | "Nhắc lại:" học PAC bất khả diễn bằng công thức với $\inf_{h'}L_D(h')$, $M(\epsilon,\delta)$ | đã sửa |
| HV6 | 7-02 | Viết lại bốn dòng thành câu đủ vế | đã sửa |
| HV7 | 5-02, 5-03 | Tiêu đề KaTeX $1/m$ | đã sửa |
| HV8 | 5-02 | Rút "khi còn lại" thành "nếu không thì"; Trực quan rút còn một dòng | đã sửa (giữ thứ tự Hệ quả rồi Kí hiệu: "Kí hiệu:" định nghĩa $M_k$ qua $\mathrm{pen}_k(m)$ của dòng trên) |
| HV9 | 1-02 | "cho $S$ là $r_m$-đại diện"; hai dòng thành hai câu | đã sửa ($\rho_m$ đầy đủ ở ghi chú diễn giả) |
| HV10 | 2-01 | "Bộ giải (solver) trên một lớp $\mathcal H$ của họ" | đã sửa |
| HV11 | 2-03 | "$D_\eta$ (Ví dụ 01.1, 01.2)"; rủi ro $h_3$, $h_2$ trên mặt trang | đã sửa |
| HV12 | 2-05 | Trực quan: cách đọc ba số hạng | đã sửa |
| HV13 | 2-06, 4-09 | "Kết luận:" nêu nội dung cận | đã sửa |
| HV14 | 2-07 | Kết luận viết lại; định nghĩa $\tilde h_k$ | đã sửa |
| HV15 | 3-04 | "$\mathbb EY_i=x_i^2$ nên $\bar f(x_0)=w_1+w_3$" | đã sửa |
| HV16 | 4-04 | "mức tăng nằm giữa $1\%$ ($k=1$) và $3{,}2\%$ ($k=4$)" | đã sửa |
| HV17 | 5-04 | "(đọc thêm)" trên mặt trang; "Kết luận:" trước định lý | đã sửa |
| HV18 | 6-02 | "mọi $h$", "lớp $K$ phần tử" | đã sửa |
| HV19 | 7-01 | Hàng Hệ quả 04.17: "so với ứng viên tốt nhất, giá cỡ $\sqrt{\ln K/m_v}$" | đã sửa (dạng "cỡ", phương án thứ hai của người duyệt; vế cận đầy đủ làm bảng tràn khung) |
| HV20 | 7-03 | Dòng "Gọi $\hat h_{(2)}$ …" chuyển sang đầu 7-04 | đã sửa; 7-03 còn 60 âm tiết, `deck_lint` 0 |
| HV21 | 2-08, 3-05, 3-07, 4-05, 6-03 | Dấu câu vào trong KaTeX; 2-08 "đại diện với bán kính $0{,}18$" | đã sửa |
| TH1 | 4-10, 7-02 | "cận trên tin cậy mức $95\%$" | đã sửa |
| TH2 | 5-01 | Điều kiện bán kính của Định lý 02.14(a), 03.15(a) | đã sửa |
| TH3 | 4-08 | "Mốc có phạt: $\inf_k[\cdot]$ ở vế phải, không gồm $\tau$" | đã sửa |
| TH4 | 3-03 (ghi chú diễn giả) | Giới hạn vào Ví dụ 04.5, $\operatorname{Cov}(\bar Y,Y_1)=\sigma^2/m$ | đã sửa |
| TH5 | 1-03 | Mục tiêu 4 có "bất khả diễn" | đã sửa |
| TH6 | 2-07 | Làm tròn lên: $\rho_m\le0{,}16444$; $a_{10}+0{,}5699$ | đã sửa |
| TH7 | 4-10 (ghi chú diễn giả) | "$=0{,}43492$, làm tròn lên $0{,}4350$" | đã sửa |
| TH8 | 1-06 (ghi chú diễn giả) | "hai lần vế phải của Định lý 03.15(b)" | đã sửa |
| TH9 | 2-02, 2-03 | "Mệnh đề 03.9, phép chiếu"; "Ví dụ 01.1, 01.2" | đã sửa |
| TH10 | 1-02, 2-05, 6-01, 6-02 | "(T1)–(T4)"; "$\delta\in(0,1)$" | đã sửa |
| TH11 | 5-03 | Bước 4 nêu "học PAC bất khả diễn" | đã sửa |
| TH12 | 4-05 | "kết luận của Bổ đề 04.9 sai" | đã sửa |
| TH13 | 5-04 (ghi chú diễn giả) | Câu về chỉ số $j$ nhỏ nhất cho $A_{\mathrm{SRM}}$ đo được | đã sửa |
| TH14 | 6-00, 1-01 | Dòng dẫn "căn bậc hai của lôgarit"; câu ở ghi chú 1-01 bỏ | đã sửa |
| TH15 | 6-02 | "mọi $h$" | đã sửa |
| TH16 | 7-01 | Như HV19 | đã sửa (dạng "cỡ") |
| TH17 | 7-02 | "Cùng $L^*$, lớp lồng nhau" | đã sửa |
| TH18 | 4-08 (ghi chú diễn giả) | "không quá mốc này cộng $\tau$" | đã sửa |
| CG1 (nghiêm trọng) | 1-06, 3-01 | 1-06: "bình phương tối thiểu (least squares)" và dòng "Hàm lỗi bình phương không bị chặn: cận Bài 02–03 không áp dụng"; 3-01 dòng mở | đã sửa (3-00 giữ dòng dẫn; câu nối nằm ở 3-01) |
| CG2 | 3-02, 7-01 | 3-02 "Một thuật toán, một điểm"; 7-01 hàng 04.6 "kì vọng, hàm lỗi bình phương" | đã sửa ("một thuật toán" ở ghi chú diễn giả 7-01: thêm vào ô làm bảng tràn khung) |
| CG3 | 3-06 | Dòng "**Lưu ý:**" Ví dụ 04.6 | đã sửa |
| CG4 | 4-08, 4-10 | 4-08 Trực quan: đánh đổi ở mức tổng thể; 4-10 "(giả sử) không tăng" | đã sửa |
| CG5 | 5-01 | Nhắc lại bằng công thức; hai khác biệt đọc được trên hai công thức đặt cạnh nhau ($\inf_{h'}$, $M(\epsilon,\delta)$ so với $L_D(h)$, $M(\epsilon,\delta,h)$) | đã sửa (dòng "Khác biệt: …" và chiều kéo theo ở ghi chú diễn giả: trang ở trần 60) |
| CG6 | 5-04 | $\mathcal H\ne\varnothing$, $\bigcup_{k\in\mathbb N}$ | đã sửa |
| CG7 | 1-03, 5-04 | "bất khả diễn"; "kể cả bất khả diễn" | đã sửa |
| CG8 | 1-06 | "xác suất $\ge0{,}95$" | đã sửa |
| CG9 | 4-08 | "không phải rủi ro vượt mức so với hợp các lớp" | đã sửa ở ghi chú diễn giả (mặt trang ở trần 60) |
| CG10 | 4-10 | "Cận trên tin cậy: ERM trên $\mathcal H_{10}$ cho $0{,}4350$" | đã sửa |
| CG11 | 5-01 | Như TH2 | đã sửa |
| CG12 | 6-02 | Bước 2 "Hoeffding, bất đẳng thức hợp trên $K$ ứng viên" | đã sửa |
| CG13 | 6-00, 7-02 | 7-02 "giữ $m_v$ quan sát" | đã sửa |
| CG14 | 7-02 | Như TH17 | đã sửa |
| SP1 (nghiêm trọng) | 3-03 | Như TH4; bỏ vế "đó là lý do …" | đã sửa |
| SP2 | 1-05 (ghi chú diễn giả) | "Sai số xấp xỉ không quan sát được; $2r$ và sai số tối ưu thực nghiệm tính được." | đã sửa |
| SP3 | 2-01 (ghi chú diễn giả) | Bỏ "thường" | đã sửa |
| SP4 | 1-03 | Mục tiêu 1, 3, 4 viết đủ (trần 80: mục tiêu 3 "chọn lớp từ một bảng số", mục tiêu 4 "qua một phản ví dụ") | đã sửa |
| SP5 | 2-05, 4-08 | Trực quan nêu cách đọc (2-05) và cơ chế đánh đổi (4-08), không chép bước chứng minh | đã sửa (4-08 dùng đánh đổi theo CG4 thay cho trường hợp một lớp; trường hợp một lớp ở "Kết luận:" 4-09) |
| SP6 | 3-01, 6-01 | Câu nối trên mặt trang | đã sửa |
| SP7 | 1-01, 1-04 (ghi chú diễn giả) | 1-01 rút; 1-04 nêu lý do thứ tự mạch | đã sửa |
| SP8 | 6-04, 7-02 (ghi chú diễn giả) | Nêu thẳng nội dung | đã sửa |
| SP9 | 2-07 | Kết luận; tách dòng | đã sửa |
| SP10 | 4-04 | Như HV16; "so với $0{,}1843$ khi không chia" | đã sửa |
| SP11 | 3-06 (ghi chú diễn giả) | Ví dụ 04.6 tách câu, nêu kết luận | đã sửa |
| SP12 | 5-01 | Như HV5 | đã sửa |
| SP13 | 5-04 | "**Kết luận:**" trên mặt trang | đã sửa |
| SP14 | 5-00 | Dòng dẫn "Cỡ mẫu đủ … giả thuyết so sánh" | đã sửa |
| SP15 | 1-01 | Luận điểm một câu, "lớp phù hợp với cỡ mẫu"; 7-00 tương tự | đã sửa |
| SP16 | 1-02 (ghi chú diễn giả) | "Từ Bài 01 cần …"; bỏ câu chỉ đường | đã sửa |
| SP17 | 1-02, 2-05, 3-07, 4-04, 6-05 | Câu bị tách: gộp (3-07, 6-05) hoặc viết thành hai câu trọn (1-02, 2-05, 4-04) | đã sửa (3-07, 6-05 mỗi dòng câu hỏi trên 20 âm tiết: câu chữ của `exercises.md`) |
| SP18 | 2-01 | "Họ lớp giả thuyết" | đã sửa |
| SP19 | 2-03 (ghi chú diễn giả) | "Ví dụ về rủi ro tham chiếu: …" | đã sửa |
| SP20 | 2-06 | Dòng cuối tách hai câu | đã sửa |
| SP21 | 2-08 (ghi chú diễn giả) | "riêng $2r$ đã là $0{,}36$" | đã sửa |
| SP22 | 3-02 | "**Bảo đảm:** lỗi kiểm tra kì vọng (expected test error) theo $(S,Y)$" | đã sửa |
| SP23 | 3-03 (ghi chú diễn giả) | Bỏ vế bình kỹ thuật | đã sửa |
| SP24 | 3-00, 3-07 (ghi chú diễn giả) | Bỏ câu lặp | đã sửa |
| SP25 | 4-01 (ghi chú diễn giả) | "Lý do giống …"; "không cho thông tin" | đã sửa |
| SP26 | 4-07 | "với $v$ là tổng nhỏ nhất đã có" | đã sửa |
| SP27 | 4-11 | "$q_1=q_2=\tfrac12$"; bỏ câu Nhận xét 04.13 ở ghi chú diễn giả | đã sửa |
| SP28 | 5-02 | Trực quan viết lại | đã sửa |
| SP29 | 5-03 (ghi chú diễn giả) | "Ba số là cỡ mẫu đủ suy từ một cận trên"; bỏ câu bước 4 | đã sửa |
| SP30 | 6-01 | "cỡ mẫu xác thực (validation sample size) $m_v$" trên mặt trang | đã sửa |
| SP31 | 7-00 (ghi chú diễn giả) | "bốn giả thiết"; bỏ câu cuối | đã sửa |
| SP32 | 7-02, 4-10 | Như HV6, CG10 | đã sửa |
| SP33 | 7-03 | "**Nhắc lại:**" thay "Phần (a):"; "Gọi …" sang 7-04 | đã sửa |
| SP34 | 7-04 (ghi chú diễn giả) | Nêu chênh lệch $0{,}001$ | đã sửa |
| SP35 | 7-05 | Bỏ nhãn "Câu hỏi:" ở dòng chỉ dẫn | đã sửa |
| SP36 | F1 | "hàm phân lớp tối ưu Bayes", tên đủ hai sai số | đã sửa trong ghi chú diễn giả; F1 bỏ khỏi deck |
| SP37 | F3 | Nhãn trục tung | đã sửa |
| MT1 | 2-01 | Dòng "Lớp thay đổi thì … cần một mức tham chiếu chung" | đã sửa (đặt ở 2-01, trang thiết lập, vì 2-03 hết chỗ) |
| MT2 | 2-05, 2-07, 7-02 | "không quan sát được / tính được" trên mặt trang | đã sửa |
| MT3 | 3-01 | Như CG1 | đã sửa |
| MT4 | 3-04 | "$\sigma^2$, $f^*$ chưa biết nên dữ liệu không chọn được bậc" | đã sửa |
| MT5 | 6-01 | "SRM chọn trên $S$ và trả $\mathrm{pen}_k$" | đã sửa |
| MT6 | 4-07, 4-11, 4-10 | Số hiệu ví dụ; "Ví dụ 04.9 (tiếp)" | đã sửa |
| MT7 | 5-03 | Như TH11 | đã sửa |
| MT8 | 5-00 | Như SP14 | đã sửa |
| MT9 | 5-01, 5-02 | "cỡ mẫu theo lớp", "xác suất thất bại giảm theo cỡ mẫu" trên mặt trang | đã sửa |
| MT10 | 7-02 | "SRM làm nhỏ nhất $L_S(h)+\mathrm{pen}_k$"; "không quan sát được / tính được" | đã sửa (vế "rủi ro $\le$ mốc có phạt $+\tau$" ở 4-08 và bảng 7-01; 7-02 ở trần 60) |
| MT11 | 1-06 | Câu hỏi ở 1-06 chỉ về bậc | đã sửa |
| MT12 | 5-01 | Như TH2 | đã sửa |
| MT13 | 5-04 | Như SP13 | đã sửa |
| MT14 | 4-09 | "Bước tất định:" mở trang | đã sửa |
| MT15 | 6-03 | "đảo cận đuôi thành bán kính và cỡ mẫu" | đã sửa |
| MT16 | 2-03 | Như TH9 | đã sửa |
| MT17 | 4-12 | Đặt 4-12 sau 4-10 | không sửa: người duyệt ghi không bắt buộc; 4-12 dùng bảng 4-07, còn 4-11 nối sang 6-05 qua cùng phân bố, nên giữ khuôn "bài tập kết mạch" |
| MT18 | mục 3 | Dòng dẫn mạch 6 cập nhật theo deck | đã sửa |
| MT19 | 2-03 | Như HV1 | đã sửa |

**Kiểm tra máy sau khi sửa:**
- `deck_lint.py`: 0 phát hiện; 7-03 hết ngoại lệ.
- `footer_check.py`: 0 trang.
- `deck_check.py`: console 0, pageerrors 0, failed 0, `.katex-error` 0. OVERFLOW chỉ ở đuôi `\sqrt`; ở 390 px `docScrollW` = 390 mọi trang. LINE20 ở 3-07, 6-05: một câu của `exercises.md`. LINE20 ở bìa, 1-05: trang tổng quan. SYLL ở 7-01: tiêu đề "Bảng tổng kết" nằm ngoài danh sách trần 80 của script.
- Phím: →, ↓, Space, Esc chạy đúng; liên kết `#/2`…`#/7` của 1-04 mở đúng `L04-2-00`…`L04-7-00`.
- 55 trang.

### Lượt 2 (theo `reviews/deck-kiem-lai-1.md`)

| Phát hiện | Trang | Sửa | Trạng thái |
|---|---|---|---|
| M1 | 2-05 | (b): "Mọi $D$, xác suất $\ge1-\delta$ theo $S\sim D^m$: (a) đúng đồng thời cho mọi quy tắc." Trực quan rút gọn để bù mật độ | đã sửa |
| M2 | 3-04 | "…; $\sigma^2$, $f^*$ chưa biết nên phân tích này không cho quy tắc chọn bậc từ dữ liệu." (ghi chú dòng 550) | đã sửa |
| M3 | 7-02 | Dòng 1 "sai số ước lượng $\le2r+\operatorname{opt}_S$, xác suất $\ge1-\delta$"; dòng 4 "giá $2\sqrt{\ln(2K/\delta)/(2m_v)}$, xác suất $\ge1-\delta$". Để giữ trần 60: bỏ "không quan sát được" ở dòng 1, "($m=10^4$)" ở dòng 2, rút dòng 3 | đã sửa |
| M4 | 2-03 (ghi chú diễn giả) | Bỏ "Đọc hình:" và câu lặp dẫn chiếu; thay bằng câu về $0{,}04$, $0{,}10$ và lớp mọi hàm | đã sửa |
| M5 | 4-11 | "có ít nhất một nhãn $0$" | đã sửa |
| M6 | 4-08 | "vế phải của (b) cân hai phần"; bỏ "ở vế phải" trong dòng mốc có phạt để bù mật độ | đã sửa |
| M7 | 5-01 | "nên cần cỡ mẫu theo lớp chứa $h$" | đã sửa |
| M8 | 2-07 | "$a_{10}\le a_2$, cả hai không quan sát được"; trả lại "$1\le d\le m$" | đã sửa |
| M9 | 6-01, 4-10 | 6-01: câu nối SRM không nhãn, rồi "**Trực quan.** Mẫu xác thực …"; 4-10: "**Ví dụ 04.9 (tiếp).**" thay nhãn trực quan | đã sửa |
| M10 | 3-06 | "thuật toán dao động nhiều hơn có lỗi $0{,}58$, thuật toán hằng $0$ có lỗi $0{,}90$"; bù mật độ: "Độ chệch thuộc thuật toán, sai số xấp xỉ thuộc lớp", "không đầu vào" | đã sửa |
| M11 | 3-05 | "nhãn đã dùng để huấn luyện"; dòng áp dụng sai rút thành "(độ chệch, phương sai, nhiễu): $0+\sigma^2/m+\sigma^2=1{,}25$" để vừa khung | đã sửa |
| M12 | 1-03 | "Tính cận của mẫu xác thực"; bù trần 80: mục tiêu 3 "chọn lớp từ bảng" | đã sửa |
| M13 | 1-06 | "các cận của Bài 02–03"; "(Bài 03)" ở dòng cận; bù: dòng 1 "$16$ điểm, …, bình phương tối thiểu (least squares)", dòng 4 "Phân lớp, $k$ chỉ số đo" | đã sửa |
| M14 | 2-05, 2-02, 3-06 | Dấu câu vào trong KaTeX ($\delta\in(0,1).$, $\delta=0{,}05,$, $1.$) | đã sửa |
| M15 | 7-01 | Tiêu đề cột trả lại "mọi $D$" | đã sửa |
| Chuỗi $0{,}18<0{,}22<0{,}32$ (tùy chọn) | 2-03 | Bản thử `\underbrace` làm trang chạm chân trang; dòng "Ví dụ." đã có đủ ba số theo thứ tự | không thêm |

Kiểm tra máy lượt 2: `deck_lint.py` 0; `footer_check.py` 0. `deck_check.py --shots` trên 16 trang đổi: console 0, pageerrors 0, failed 0, `.katex-error` 0; ở 390 px `docScrollW` = 390. Đã xem ảnh 1600×900 và 390×844 (có `-end`) của các trang đổi.

### Lượt 3 (theo `reviews/deck-kiem-lai-2.md`)

| Phát hiện | Trang | Sửa | Trạng thái |
|---|---|---|---|
| N1 | 7-02 | Dòng 1: "Cùng $L^*$: sai số xấp xỉ không tăng, không quan sát được; sai số ước lượng $\le2r+\operatorname{opt}_S$, xác suất $\ge1-\delta$; cận tính được." (bỏ "Lớp lồng nhau," như đề xuất) | đã sửa |
| N2 | 1-03 | Mục tiêu 3 "chọn lớp từ bảng rủi ro thực nghiệm và số hạng phạt"; bù trần 80: mục tiêu 1 "Phân tích sai số: tách rủi ro, chặn sai số ước lượng bằng hai số hạng", mục tiêu 4 bỏ "qua một phản ví dụ" (mục tiêu 5 vẫn có phản ví dụ) | đã sửa (mục tiêu 3 có 23 âm tiết một dòng; trang tổng quan, trần 80 giữ) |
| N3 | 3-04 | "Kết luận:" tách hai dòng (11 và 14 âm tiết) | đã sửa |
| N4 | 7-02 | Dòng 3: "Bậc tốt nhất phụ thuộc $\sigma^2$, $f^*$ chưa biết; …"; bù trần 60: dòng 4 "giữ riêng $V$", dòng 3 bỏ "khi" | đã sửa |
| N1 (bổ sung, điều phối viên) | 7-02 | Khôi phục "Lớp lồng nhau, cùng $L^*$:" ở dòng 1 (điều kiện của "sai số xấp xỉ không tăng", cổng duyệt T7); bù bằng bỏ "không quan sát được" (ý này có trên 2-05 "Trực quan." và 2-07 "cả hai không quan sát được"); trang 59 âm tiết | đã sửa |

Kiểm tra máy lượt 3: `deck_lint.py` 0; `footer_check.py` 0; `deck_check.py --shots --ids L04-1-03,L04-3-04,L04-7-02`: console 0, pageerrors 0, failed 0, `.katex-error` 0, ở 390 px không cuộn ngang (OVERFLOW ở 7-02 là đuôi `\sqrt`). Đã xem ảnh 1600×900 và 390×844 (có `-end` của 3-04).
