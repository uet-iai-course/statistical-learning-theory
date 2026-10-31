# Biên tập vòng 1 — Bài 04, ghi chú

Tệp nội bộ. Người biên tập: tác tử viết ghi chú (cùng phiên). Căn cứ: `reviews/0-quyet-dinh.md` (N1–N5, M1–M23, C, D; M24 bác bỏ) và năm báo cáo `reviews/1-…5-….md`; số dòng trong các báo cáo dẫn theo bản đóng băng `lec04-draft-frozen.md`. Diff của vòng: `scratchpad/lec04-round1.diff` (ngoài repo). Số hiệu khối và ví dụ không đổi.

## Quyết định của điều phối viên

- N1 — đã sửa — Ví dụ 04.8: biến cố hỏng của lớp $k$ là $L_S(h_k)\in\{0,1\}$, xác suất $2^{-9}$; in $1-(1-2^{-9})^{k_{\max}}$: $0{,}858$, $0{,}99994$; giữ câu $0{,}6236$ cho riêng $L_S=0$ (Bài tập 02.4(b)); §9 ghi $0{,}86$.
- N2 — đã sửa — "chia độ tin cậy" → "chia xác suất thất bại" ở đoạn dẫn, mục tiêu 3, §6 (tiêu đề), Ví dụ 04.7, 04.8 (tiêu đề), Hệ quả 04.15 (tiêu đề), §12, Phụ lục B; "xác suất hỏng" → "xác suất thất bại"; không còn chữ "độ tin cậy" chỉ $\delta$ (grep 0).
- N3 — đã sửa — Ví dụ 04.6: câu dẫn nêu cách đọc bị bác; Bước 3 định nghĩa độ chệch/phương sai theo nghĩa phân lớp; Bước 4 bác cách đọc ($0{,}58$ so với $0{,}90$) và câu về độ chệch bình phương ($0{,}25$ so với $0{,}81$); §9 sửa theo.
- N4 — đã sửa — Nhận xét 04.4 "Đẳng thức và cận trong phân tích sai số"; ba nhãn **Đẳng thức.**, **Cận.**, **Hiệu theo rủi ro kì vọng.**; lý do dùng $\operatorname{opt}_S$ ở câu cuối nhãn ba; phép tính tách bốn bước ngắn (Mẫu, Nghiệm ERM, Đầu ra của bộ giải, Hiệu).
- N5 — đã sửa — $k_{\max}$ cho số lớp (§2, §6 câu mở, Ví dụ 04.8, Hệ quả 04.15(b), Phụ lục B); $K$ chỉ còn cho danh sách hữu hạn giả thuyết/ứng viên; Định nghĩa 04.8 dùng $\lvert\mathcal H\rvert$; Ví dụ 04.8 ghi "với $K=k_{\max}$ của bài tập đó".
- M1 — đã sửa — đoạn giải thích "oracle": vế phải là giá trị một người biết $D$ dùng để so các lớp; (b) chỉ nói rủi ro của SRM không vượt giá trị đó cộng $\tau$ với xác suất ít nhất $1-\delta$.
- M2 — đã sửa — câu sau $\square$ của Mệnh đề 04.3: cận có hai số hạng riêng; sai số ước lượng không được tách (khớp Nhận xét 04.4).
- M3 — đã sửa — cuối §3, Ví dụ 04.3, cuối §4: "cận tăng theo lớp", sai số xấp xỉ "không tăng".
- M4 — đã sửa — bỏ đoạn sau Định lý 04.11 và câu thứ hai cuối §6; câu mở §7 nêu phạm vi (bán kính của Định lý 02.14(a), 03.15(a); $\mathrm{pen}_k\to\infty$; "cận không cho cỡ mẫu chung").
- M5 — đã sửa — Ví dụ 04.9 Bước 2 và lời giải câu hỏi cuối buổi (b): "$0{,}3651$ (…$0{,}3751$) là một cận trên tin cậy ở mức $95\%$", dẫn Nhận xét 01.19; §9 dùng "cận".
- M6 — đã sửa — §12: bỏ "cần hàm lỗi trong $[0,1]$" khỏi khác biệt; nêu ví dụ hồi quy đa thức của UML §11.2 không nêu giả thiết bị chặn; mục §5.2 nêu $\min_{\mathcal H}L_D$ (rủi ro tuyệt đối).
- M7 — đã sửa — tiêu đề §4 "… sai số tối ưu thực nghiệm"; cầu nối dùng "độ chênh tối ưu (suboptimality)", câu cuối "Câu hỏi cho Bài 05 là: …".
- M8 — đã sửa — giả thiết **Thuật toán.** của Hệ quả 04.15 và Định lý 04.16(b) thêm điều kiện đo được; Phụ lục A Bước 5 dẫn giả thiết này.
- M9 — đã sửa — Định nghĩa 04.1 chỉ cần (T2) và $L_D<\infty$ trên $\mathcal H$; câu "các kết quả với xác suất cao mới cần (T3)" và $L^*$ chung cho một họ lớp.
- M10 — đã sửa — đoạn sau Mệnh đề 04.6: áp dụng cho hàm cố định (phương sai $0$) cho $\mathbb E(f(x)-Y)^2\ge\sigma^2(x)$; từ đó $\mathbb E\sigma^2(X)$ là rủi ro Bayes của hàm lỗi bình phương; Nhận xét 04.7 dẫn đoạn này.
- M11 — đã sửa — Phụ lục D, Bước 2: lập luận không có bữa trưa miễn phí của Định lý 03.17(a) (UML §5.1, Nhận xét 01.30: "với mỗi thuật toán") không dùng điều kiện đầu ra thuộc $\mathcal H_k$, nên áp dụng cho $A$.
- M12 — đã sửa — Ví dụ 04.9: bảng đủ mười hàng; bỏ câu về hai bộ trọng số; khoảng cách $0{,}0130$; giá $0{,}0058$; cận in $0{,}3651$, $0{,}4350$, $0{,}3593$.
- M13 — đã sửa — đoạn trước Hệ quả 04.15: SRM là họ thuật toán chỉ số theo $\delta$; câu sau $\square$ của Hệ quả 04.15 theo đề xuất.
- M14 — đã sửa — phần đọc bằng số: "đủ", "bỏ $\delta$ khỏi đầu vào", xác suất thất bại $1/m\approx4{,}7\cdot10^{-6}$; Ví dụ 04.12 Bước 4 "là đủ".
- M15 — đã sửa — lời giải (c): $\tau$ do độ chính xác của bộ giải quyết định; cận không có cơ chế làm $\tau$ giảm khi thêm dữ liệu.
- M16 — đã sửa — mục tiêu 5 theo đúng câu chữ của quyết định.
- M17 — đã sửa — "lỗi kiểm tra kì vọng"; "nhãn kiểm tra" (Định nghĩa 04.5, Mệnh đề 04.6, Ví dụ 04.4–04.6; tiêu đề Ví dụ 04.5); "rủi ro kì vọng" thay "rủi ro thật"; "tối thiểu hóa" thay "cực tiểu" (động từ); "Phép kéo theo ngược lại"; $\mathrm{pr}_k$ thay $\pi$; Phụ lục A $v^\star$ thay $V$, Phụ lục B $\varphi$ thay $g$.
- M18 — đã sửa — bỏ "lý do … nằm ở nhận xét cuối mục", "như trong ví dụ thứ hai sau định lý dưới đây", "như ví dụ sau hệ quả dưới đây"; "Bổ đề dưới đây chia $\delta$" viết lại thành nhu cầu. Còn "quy tắc sau", "định lý sau" trỏ khối liền kề (giữ, như Bài 03).
- M19 — đã sửa — Mệnh đề 04.3: điều kiện của (b) chuyển vào **Giả thiết.** (nhãn "Mẫu và lớp, cho phần (b)"); dạng chiều VC có công thức hiển thị, câu dẫn và tiếng Anh.
- M20 — đã sửa — Ví dụ 04.4 Bước 1: bậc $1$ tách hai dòng (hệ số; dự đoán, có phép tính trọng số); hệ phương trình chuẩn đầy đủ ở Phụ lục C (để giữ ngân sách). Thuật toán 04.12: vòng lặp đánh số 1–4, $\hat k\leftarrow1$ ở khởi tạo, đầu vào ghi "danh sách hữu hạn, hoặc $\mathrm{pen}_k\to\infty$"; $\tau'$ gồm cả phép thử dừng.
- M21 — đã sửa — tách các câu dòng 435, 749 (ba câu), 866 (thành khối chứng minh ở Phụ lục D), 944 (viết lại), 950 (danh sách bốn dòng), 308.
- M22 — đã sửa — 262↔273 (một câu, ở cuối §4); câu "kì vọng theo mẫu, không phải xác suất cao" chỉ còn ở Mệnh đề 04.6; bỏ câu cuối §7; cuối §8 còn một câu chung, so sánh SRM–xác thực chỉ ở §9.
- M23 — đã sửa — §9 đoạn đầu: không có cận đều cho lớp đa thức với hàm lỗi bình phương; Ví dụ 04.4; có $\lvert Y\rvert\le B$ và cắt dự đoán thì dùng cận của Nhận xét 04.18.
- M24 — không áp dụng — bác bỏ theo quyết định.
- C — đã sửa — áp dụng các chỗ cắt của R5 và M4, M12, M22. Để bù phần thêm mà không cắt toán: chứng minh đầy đủ Hệ quả 04.15 chuyển sang Phụ lục B (tiêu đề khối ghi "chứng minh đầy đủ ở Phụ lục B", thân bài giữ một câu lộ trình); ý chứng minh Định lý 04.16(a) chuyển thành khối chứng minh ở Phụ lục D; chứng minh $\tau=\epsilon_{\mathrm{opt}}+\tau'$ và cận tinh hơn sau Thuật toán 04.12 chuyển sang Phụ lục E (thân bài giữ phát biểu và công thức cận tinh hơn); lý luận chiều VC $d_k=k+1$ của khối ứng dụng và hệ phương trình chuẩn chuyển sang Phụ lục C.
- D (làm tròn) — đã sửa — cận in sau "$\le$" làm tròn lên: $0{,}3651$, $0{,}3751$, $0{,}4350$, $0{,}3593$; bảng giữ làm tròn gần nhất; Ví dụ 04.3 viết từ $0{,}16443$, $0{,}27992$; hiệu $0{,}0058$, $0{,}0130$.
- D (§11.2 trang 146) — không áp dụng — bác bỏ theo quyết định.
- D (giả thiết thuật toán của Định lý 04.11) — đã sửa — giữ dòng **Thuật toán.**; chứng minh Bước 1 nêu chỗ dùng tính đo được, Bước 2 nêu tính $\tau$-chính xác; thêm câu "bảo đảm áp dụng cho mọi cặp $\tau$-chính xác".
- D (Ví dụ 04.11 so với UML 7.5) — không áp dụng trong ghi chú — chuyển cho người viết bài tập.

## Phát hiện nhẹ — R1 (học viên)

- R1-1 mục tiêu 1 — đã sửa.
- R1-2 câu rối Ví dụ 04.6 Bước 3 — đã sửa.
- R1-3 "Khác biệt duy nhất" — đã sửa (hai khác biệt).
- R1-4 đếm "dòng" trong chứng minh — đã sửa (Mệnh đề 04.3, Định lý 04.11 dùng "bất đẳng thức thứ …"; câu dòng 684 chuyển vào Phụ lục E).
- R1-5 dòng 190 — đã sửa.
- R1-6 lặp 262/273, "giảm" → "không tăng" — đã sửa.
- R1-7 tính trước độ chệch ở dòng 289 — đã sửa (bỏ).
- R1-8 phản ví dụ $0{,}25$ đứng trước Ví dụ 04.2 — đã sửa (chuyển xuống sau).
- R1-9 "(ý này có ở §9 của Bài 02)" — đã sửa.
- R1-10 "cận này không cho cỡ mẫu chung" — đã sửa.
- R1-11 con trỏ vòng vo 602, 778 — đã sửa (bỏ; câu "Phép kéo theo ngược lại" chuyển vào Ví dụ 04.11).
- R1-12 phủ định kép dòng 944 — đã sửa.
- R1-13 dòng 68 — đã sửa.
- R1-14 dòng 15 — đã sửa.
- R1-15 "Dung sai $\tau$ đo độ chính xác của lời giải …" — đã sửa.
- R1-16 "bộ giải (solver)" — đã sửa.
- R1-17 nhãn "Tên gọi" — đã sửa (N4).
- R1-18 "hẳn"; kicker Ví dụ 04.10 — đã sửa.
- R1-19 Ví dụ 04.7 kết luận; Phụ lục C đủ mười tỉ số — đã sửa.
- R1-20 bước giải hệ phương trình chuẩn — đã sửa (Phụ lục C).
- R1-21 §9 lặp; mô-típ "Giá của" — sửa một phần (§9 viết lại; giữ "Giá của việc chia xác suất thất bại" vì N2 chốt tiêu đề, và "giá của việc không biết trước lớp" theo M12).
- R1-22 "sai số tối ưu" ở cầu nối — đã sửa theo M7 ("độ chênh tối ưu"), không theo đề xuất "sai số tối ưu thực nghiệm" của R1.
- R1-23 giải thích "không tiền tố" — đã sửa.
- R1-24 câu về cặp $\tau$-chính xác — đã sửa.
- R1-25 câu hỏi mở đầu trỏ tới §8 — đã sửa.
- R1-26 thiếu $\delta$ ở Nhận xét 04.18 — đã sửa.
- R1-27 câu không động từ dòng 931 — đã sửa.
- R1-28 thiết kế ngẫu nhiên ở dòng 342 — đã sửa.

## Phát hiện nhẹ — R2 (toán học)

- R2-1 Ví dụ 04.3 $0{,}16443$ — đã sửa.
- R2-2 cận làm tròn xuống — đã sửa (quy tắc D).
- R2-3 $0{,}0131$ ở Bước 5 — đã sửa (M12).
- R2-4 Định nghĩa 04.1 và (T3) — đã sửa (M9).
- R2-5 giả thiết thuật toán của Định lý 04.11 — đã sửa theo D.
- R2-6 Thuật toán 04.12: điều kiện dừng và $\tau'$ của phép thử dừng — đã sửa.
- R2-7 $V$ ở Phụ lục A — đã sửa ($v^\star$).
- R2-8 Định lý 03.17(a) cho thuật toán đầu ra trong $\mathcal H$ — đã sửa (M11, Phụ lục D).
- R2-9 tính đo được của $\operatorname{opt}_S$ — đã sửa.
- R2-10 dòng 776 — đã sửa (không thêm câu về tính liên tục của xác suất, để giữ ngân sách).
- R2-11 Hệ quả 04.17: giả thiết đo được của $K(S)$ và $(s,z)\mapsto\ell(g_j(s),z)$; Bước 3 nói rõ phần phác thảo — đã sửa.

## Phát hiện nhẹ — R3 (chuyên gia, nguồn)

- R3-1 $V$ ở Phụ lục A — đã sửa.
- R3-2 UML §5.2 dùng $\min_{\mathcal H}L_D$ — đã sửa.
- R3-3 "cần" → "đủ"; "bỏ $\delta$ khỏi đầu vào" — đã sửa.
- R3-4 $\mathcal Y=\mathbb R$ và hàm lỗi bình phương ngoài §5 — đã sửa (§1 mục 1, 4).
- R3-5 Định nghĩa 04.1 với hàm lỗi bình phương — đã sửa (M9).
- R3-6 rủi ro Bayes bình phương — đã sửa (M10).
- R3-7 dòng 190 — đã sửa.
- R3-8 $0{,}0131$ — đã sửa.
- R3-9 tiêu đề §4 — đã sửa.
- R3-10 dòng 435 — đã sửa.
- R3-11 "$A_{\mathrm{SRM}}$ là thuật toán học PAC bất khả tri" ở cuối §7 — đã sửa.
- R3-12 $\tau$ ở lời giải (c) — đã sửa (M15).
- R3-13 chính quy hóa $\lambda\,\Omega(w)$ — đã sửa.
- R3-14 dấu hai chấm khẩu hiệu dòng 745; "không bỏ được" — đã sửa.
- R3 (Ví dụ 04.11 và UML 7.5) — chuyển cho người viết bài tập (D).
- R3 (§11.2 trang 146) — không áp dụng (D bác bỏ).

## Phát hiện trung bình và nhẹ — R4 (học thuật, văn phong)

- R4-1, R4-2 — đã sửa (N4, N5).
- R4-3 $\pi$ hai nghĩa — đã sửa ($\mathrm{pr}_k$).
- R4-4 $V$, $g$ dùng lại — đã sửa ($v^\star$, $\varphi$).
- R4-5 "sai số" → "lỗi" cho giá trị hàm lỗi — đã sửa.
- R4-6 một tên cho $Y$: "nhãn kiểm tra" — đã sửa.
- R4-7 "xác suất hỏng" — đã sửa.
- R4-8 "rủi ro thật" — đã sửa.
- R4-9 "cực tiểu" — đã sửa.
- R4-10 "Chiều ngược lại" — đã sửa.
- R4-11 con trỏ bằng lời; dòng 113 — đã sửa.
- R4-12 Mệnh đề 04.3 giả thiết — đã sửa (M19).
- R4-13 dạng chiều VC có công thức — đã sửa.
- R4-14 Ví dụ 04.4 Bước 1 — đã sửa (M20; hệ phương trình ở Phụ lục C).
- R4-15 Nhận xét 04.4 các bước — đã sửa.
- R4-16 Thuật toán 04.12 danh sách, $\hat k\leftarrow1$ — đã sửa.
- R4-17 dòng 435 — đã sửa.
- R4-18 câu dài 749, 866, 950, 308 — đã sửa.
- R4-19 Định lý 04.16 giả thiết thành danh sách — đã sửa.
- R4-20 lặp giữa các mục — đã sửa (M22).
- R4-21 phủ định vòng dòng 944 — đã sửa.
- R4-22 năm hàng $k=5,\ldots,9$ — đã sửa (bảng mười hàng).
- R4-23 cầu nối: "độ chênh tối ưu", "(stochastic gradient descent, SGD)" — đã sửa.
- R4-24 tiếng Anh ở lần đầu — sửa một phần: thêm (penalty) ở đoạn dẫn, (0–1 loss) ở câu hỏi mở đầu, (solver), (candidate), (adaptive reuse), "chiều VC (Vapnik–Chervonenkis dimension)"; §1 và §2 không dùng "thiết kế cố định", "dung sai" trước định nghĩa; mục tiêu học tập giữ chữ không kèm tiếng Anh (ngoại lệ của quy tắc định nghĩa trước khi dùng); "cận độ lệch đều" không còn ở câu hỏi mở đầu.
- R4-25 thuật ngữ mới cho `thuat-ngu.md` — không áp dụng (ngoài phạm vi ghi; báo điều phối viên).
- R4-26 "hàm phân lớp tối ưu Bayes", "hàm gán nhãn" — đã sửa.
- R4-27 tên của $\epsilon$ — đã sửa.
- R4-28 câu hỏi mở đầu dẫn $0{,}329\to0{,}560$ — đã sửa.
- R4-29 tiêu đề §4 — đã sửa.
- R4-30 bước trung gian — đã sửa ở Ví dụ 04.3 (Bước 2, 4), 04.4 (Bước 5, 6), 04.5 (Bước 2), 04.6 (Bước 1), Nhận xét 04.7 (số hạng chéo), Ví dụ 04.7 (Bước 2: $2\ln3$, $2\ln10$), 04.8 ($\ln40\,000$), 04.12 (Bước 4).
- R4-31 câu kết của Nhận xét 04.7 — đã sửa.
- R4-32 nhãn (a)/(b) song song — đã sửa (Mệnh đề 04.3, Hệ quả 04.15, 04.17).
- R4-33 dòng 159, 178 — đã sửa.
- R4-34 dòng 289 — đã sửa (tách hai đoạn, bỏ phép tính).
- R4-35 mở §5 bằng nhu cầu; câu nguồn chuyển xuống §12 — đã sửa.
- R4-36 "chúng ta" cho kế hoạch; chủ thể trừu tượng — đã sửa (dòng 3, 273, 387, 780, 1001).
- R4-37 danh từ hóa "việc" — sửa một phần (xem R1-21).
- R4-38 kicker dòng 178; "hẳn"; "không phải một hằng số tinh chỉnh" — đã sửa.
- R4-39 chính quy hóa: nêu điểm khác cụ thể, bỏ trỏ sang Bài 06 — đã sửa.
- R4-40 tiên quyết Bài 01 thành gạch con — đã sửa.
- R4-41 "chỉ số đo đầu tiên" — đã sửa.
- R4-42 dòng 776 — đã sửa.
- R4-43 dòng 684 — đã sửa (nội dung chuyển sang Phụ lục E, Bước 3).
- R4-44 dòng 868 — đã sửa.
- R4-45 tiêu đề Ví dụ 04.6 là cụm danh từ — đã sửa.
- R4-46 ba câu chuyển ý cùng khuôn — đã sửa (giữ một ở Ví dụ 04.10; Ví dụ 04.5, 04.8 nêu giả thiết bị bỏ trong **Thiết lập.**).
- R4-47 chứng minh đánh dấu chỗ dùng giả thiết — đã sửa (Mệnh đề 04.3 Bước 2–3, Định lý 04.11 Bước 1, Hệ quả 04.15 Bước 1).
- R4-48 phần đọc bằng số thành danh sách — đã sửa.
- R4-49 Định nghĩa 04.5, 04.8 thành danh sách — đã sửa.
- R4-50 lời giải ôn nhanh 3 — sửa một phần (kết quả là công thức hiển thị; khai triển một dòng trong câu để giữ ngân sách).
- R4-51 `van-phong.md` — không áp dụng (điều phối viên đã sửa).

## Phát hiện trung bình và nhẹ — R5 (mạch)

- R5 trung bình (§9 khép câu hỏi mở đầu) — đã sửa (M23).
- R5-1 đoạn dòng 650 — đã sửa (bỏ).
- R5-2 868↔872 — đã sửa.
- R5-3 938↔948 — đã sửa.
- R5-4 con trỏ 192, 602, 778 — đã sửa.
- R5-5 $2\,\mathrm{pen}_2$ in $0{,}338$, $2\,\mathrm{pen}_{10}$ in $0{,}574$ — đã sửa.
- R5-6 dòng 721 — đã sửa.
- R5-7 mục tiêu 5 — đã sửa (M16).
- R5-8 tiêu đề Nhận xét 04.4 — đã sửa (N4).
- R5-9 thuật ngữ 137, 1001; tên "dạng chiều VC" — đã sửa (công thức hiển thị ở sau Định nghĩa 04.8; Ví dụ 04.3 vẫn gọi vế phải thứ nhất của Định lý 03.15(b) là "dạng trực tiếp", vì đó là cận, chưa cắt ở $1$).
- R5-10 $K$ hai nghĩa — đã sửa (N5).
- R5-11 dòng 159 — đã sửa.
- R5-12 mở §5 bằng nhu cầu — đã sửa.
- R5-13 Bài tập 02.11 trong tiên quyết — đã sửa.
- R5-14 tên $\mathcal G_S$ ở Ví dụ 04.10 — đã sửa.
- R5-15 phân bổ độ dài — đã sửa (bù bằng chuyển chứng minh sang phụ lục; §7 còn khoảng 1 150 tiếng).
- R5-16 "được phụ thuộc", "hẳn" — đã sửa.
- R5-17 cầu nối: thêm "với hàm lỗi lồi theo tham số thay cho hàm lỗi 0–1" — đã sửa.

## Con số mới hoặc đổi

Mọi giá trị tính lại bằng Python trong scratchpad của phiên (`w04/n4.py`, `w04/n5.py`, ngoài repo).

| Vị trí | Trước | Sau | Tính lại |
|---|---|---|---|
| Ví dụ 04.8 Bước 2–3, kết luận | $0{,}6236$; $0{,}9924$ (đẳng thức) | $2^{-9}$; $0{,}858$; $0{,}99994$; giữ $0{,}6236$ cho riêng $L_S=0$ | $1-(1-2^{-9})^{1000}=0{,}858440$; $1-(1-2^{-9})^{5000}=0{,}999943$; $1-(1-2^{-10})^{1000}=0{,}623576$ |
| Ví dụ 04.8, chia đều | $0{,}7279$ | thêm $\ln40\,000\approx10{,}597$ | $10{,}596635$; $\sqrt{10{,}5966/20}=0{,}727895$ |
| §9 | $0{,}62$ | $0{,}86$ | như trên |
| Ví dụ 04.9 Bước 2, §9 | $0{,}3650$ | $0{,}3651$ (chưa làm tròn $0{,}36504$) | $0{,}175+0{,}190044=0{,}365044$ |
| Ví dụ 04.9 Bước 3, §9 | $0{,}4349$ | $0{,}4350$ ($0{,}43492$) | $0{,}155+0{,}279919=0{,}434919$ |
| Ví dụ 04.9 Bước 4 | $0{,}0057$ | $0{,}0058$; cận $0{,}3593$ ($0{,}35928$) | $0{,}365044-0{,}359284=0{,}005759$ |
| Ví dụ 04.9 Bước 5 | $0{,}0131$ | $0{,}0130$ | $0{,}378082-0{,}365044=0{,}013038$ |
| Ví dụ 04.9 bảng, $k=5,\ldots,9$ | (ở bài tập) | $0{,}166+0{,}2241=0{,}3901$; $0{,}163+0{,}2386=0{,}4016$; $0{,}160+0{,}2520=0{,}4120$; $0{,}158+0{,}2644=0{,}4224$; $0{,}156+0{,}2761=0{,}4321$ | $\mathrm{pen}_5,\ldots,\mathrm{pen}_9=0{,}224087$; $0{,}238606$; $0{,}251974$; $0{,}264416$; $0{,}276092$ |
| Ví dụ 04.9 kết luận | $0{,}3379$; $0{,}5742$ | $0{,}338$; $0{,}574$ | $2\cdot0{,}168951=0{,}337902$; $2\cdot0{,}287119=0{,}574237$ |
| Câu hỏi cuối buổi (b) | $0{,}3750$ | $0{,}3751$ ($0{,}37504$) | $0{,}185+0{,}190044=0{,}375044$ |
| Ví dụ 04.3 | $0{,}1644$, $0{,}2799$, "khoảng $0{,}231$" | $0{,}16443$, $0{,}27992$; $0{,}3389$; $0{,}5698$; $2(0{,}27992-0{,}16443)\approx0{,}2310$ | $0{,}338861$; $0{,}569839$; $0{,}230978$ |
| Ví dụ 04.7 Bước 2 | — | $2\ln3\approx2{,}1972$; $2\ln10\approx4{,}6052$ | $2{,}197225$; $4{,}605170$ |
| Phần đọc sau Hệ quả 04.15 | — | $1/m\approx4{,}7\cdot10^{-6}$ | $1/213\,317=4{,}6879\cdot10^{-6}$ |
| Ví dụ 04.12 Bước 4 | — | $2\cdot5{,}9915/0{,}0025\approx4793{,}2$ | $4793{,}17$ |
| Ví dụ 04.6 Bước 4 | — | độ chệch bình phương $0{,}25$ và $0{,}81$ | $(0{,}4-0{,}9)^2$; $(0-0{,}9)^2$ |
| Phụ lục C | năm hàng | mười hàng: $a$ $54{,}67$; $62{,}70$; $70{,}59$; $78{,}36$; $86{,}01$; $b$ $8{,}099$; $8{,}463$; $8{,}772$; $9{,}039$; $9{,}274$; không chia $0{,}2174$; $0{,}2317$; $0{,}2449$; $0{,}2573$; $0{,}2689$; tỉ số $1{,}031$; $1{,}030$; $1{,}029$; $1{,}028$; $1{,}027$ | `w04/n5.py` |

## Kiểm tra đã chạy

- `python3 ../tools/courses/statistical-learning-theory/scripts/forward_refs.py 2627-1/materials/lec-04/lecture-note.md`: `0 forward references`.
- `wc -w`: thân bài $11\,997$ tiếng (đến trước `## Phụ lục`), phụ lục $1\,853$ tiếng.
- Sync `material-local-data.js` và `--check`: OK (7 tệp).
- Playwright (Chromium, máy chủ `reloadserver` cổng 8781, đã tắt sau khi kiểm), 1600×900 và 390×844, mở mọi khối thu gọn (11 khối `details`): 0 `.katex-error`; 0 yêu cầu thất bại; không công thức hay bảng nào rộng hơn khung (lần chạy đầu có 5 công thức tràn ở 390 px, đã ngắt dòng); không tràn ngang trang. Một lỗi console "inline script violates CSP" xuất hiện trên mọi trang, kể cả Bài 03, nên không do ghi chú. Ảnh chụp Ví dụ 04.6, 04.8, Nhận xét 04.4, Thuật toán 04.12, Định nghĩa 04.8 đã xem, trong scratchpad `w04/shots/`.
- Quét chữ: không còn "độ tin cậy" theo nghĩa $\delta$, "xác suất hỏng", "rủi ro thật", "cực tiểu" (động từ), "Chiều ngược lại", "phản hồi", "quan sát kiểm tra"; không có `\text{}` chứa chữ có dấu.

## Vòng 2

Căn cứ: `reviews/6-ra-lai-toan.md` (R6) và `reviews/7-ra-lai-mach.md` (R7), số dòng theo `lec04-round1-frozen.md`; quyết định của điều phối viên cho Ví dụ 04.6. Diff: `scratchpad/lec04-round2.diff`.

- R6 trung bình (Phụ lục E, Bước 3) — đã sửa — đẳng thức gắn vào vế phải của bất đẳng thức thứ nhất, $L_S(\hat h_k)+\mathrm{pen}_k+\tau'$; nói rõ $\operatorname{opt}_S(\hat h_k)+\tau'$ thay cho $\tau$ ở lớp $k$; bỏ cách đếm "dòng" (cũng là R7-10).
- R6/R7 bảng kí hiệu §2 bị cắt — đã sửa — xóa dòng trống; Playwright đếm 5 bảng và không còn dòng nào bắt đầu bằng "|" trong văn bản hiển thị. Hàng $\ln$ đã xóa có chủ ý ở vòng 1 (kí hiệu chuẩn) để giữ ngân sách.
- R6 làm tròn — đã sửa — cận $0{,}0469$ ở Ví dụ 04.10 (Bước 3, Kết luận) và §9; phép tính in $\approx0{,}04681$; Ví dụ 04.3 Bước 1 viết "$\rho_m$ không vượt dạng trực tiếp, $\approx0{,}16443$ … $\approx0{,}27992$".
- R6 Phụ lục D câu sau $\square$ — đã sửa — "hợp đếm được của các lớp có chiều VC hữu hạn, tức các lớp học được PAC khi thêm (M) (Định lý 03.17(b))".
- R6/R7 Ví dụ 04.6, hai nghĩa — đã sửa theo quyết định — Bước 2 nêu "độ chệch bình phương $0{,}25$" và "phương sai $0{,}24$" (Định nghĩa 04.5); Bước 3 định nghĩa *độ chệch theo nghĩa phân lớp* và *phương sai theo nghĩa phân lớp* ($0{,}4$ với $A$); Bước 4 và kết luận chỉ dùng các tên này; câu dẫn và Bước 4 trích cùng một câu "cùng độ chệch thì phương sai nhỏ hơn tốt hơn".
- R7-1 (203/290) — đã sửa — bỏ câu "Hiệu tổng thể … là một đại lượng khác"; chỉ còn tên "hiệu theo rủi ro kì vọng" ở Nhận xét 04.4.
- R7-3 Ví dụ 04.8 — đã sửa — phép tính chia đều tách thành **Bước 4: khi chia đều.** trước Kết luận.
- R7-4 câu dài 480, 768, 899, 941 — đã sửa — 480 tách thành hai câu định nghĩa; 768 tách sau "$\mathcal H_{10}$" ("Lớp này cố định trước mẫu, …"); 899: điều kiện đo được chuyển vào nhãn **Thuật toán.** của **Giả thiết.** ("ở phần (b), …"); 941 tách sau "cố định".
- R7-5 (768, chủ ngữ của "cố định trước mẫu") — đã sửa cùng R7-4.
- R7-6 Nhận xét 04.4 — đã sửa — câu lý do chuyển xuống sau bước **Hiệu.**
- R7-7 cuối §7 — đã sửa — chỉ giữ câu về ý thử thách của Bài tập 04.11.
- R7-8 "thiết kế ngẫu nhiên" — đã sửa — *thiết kế ngẫu nhiên* (random design) ở lần đầu.
- R7-11 câu kết §6 — đã sửa — thêm "; cận đó còn phụ thuộc $\delta$, một đầu vào của quy tắc".

**Con số đổi:** $0{,}0468\to0{,}0469$ cho cận (tính lại $\sqrt{\ln80/2000}=0{,}046808$); $0{,}04681$ in trong phép tính. Không số nào khác đổi.

**Kiểm tra đã chạy:** `forward_refs.py` 0; `wc -w` thân bài $11\,978$, phụ lục $1\,862$; sync và `--check` OK; Playwright 1600×900 và 390×844 (11 khối `details` mở): 0 `.katex-error`, 0 yêu cầu thất bại, không công thức hay bảng tràn, không tràn trang, 5 bảng, không dòng nào trong `document.body.innerText` bắt đầu bằng "|" hay ":::" hoặc chứa "$$"; lỗi CSP inline có sẵn như ở Bài 03. Máy chủ cổng 8781 đã tắt.

## Vòng 3

Căn cứ: `reviews/8-ra-lai-vong-2.md`, số dòng theo `lec04-round2-frozen.md`. Chỉ đổi câu chữ, không đổi con số. Diff: `scratchpad/lec04-round3.diff`.

- Câu kết §7 (dòng 907) — đã sửa — thêm câu "Theo Ví dụ 04.11, một lớp đếm được có chiều VC vô hạn vẫn học được không đều." trước câu về ý thử thách của Bài tập 04.11.
- Định lý 04.16 (dòng 897) — đã sửa — thêm nhãn **Họ lớp, cho phần (b).** (danh sách đếm được, chiều VC hữu hạn, (M), trọng số $q_k$) trước nhãn **Thuật toán.**; phần (b) dẫn lại Hệ quả 04.15.
- "cận đó" (dòng 806) — đã sửa — "số hạng phạt trong cận này còn phụ thuộc $\delta$".
- Câu lý do lặp (299 so với 289) — đã sửa — câu cuối Nhận xét 04.4 còn "Vì vậy học phần dùng đại lượng thực nghiệm, không âm, $\operatorname{opt}_S$."
- §9 (dòng 985) — đã sửa — "phương sai theo nghĩa phân lớp lớn hơn".
- Ví dụ 04.3 Bước 2 — đã sửa — "$\le a+2\rho_m+0{,}01$", rồi "$\approx$" với $0{,}16443$, $0{,}27992$.
- Bù ngân sách: rút câu cuối Hệ quả 04.15, câu sau Định nghĩa 04.14 và kết luận Ví dụ 04.12 (giữ ý).

**Kiểm tra đã chạy:** `forward_refs.py` 0; thân bài $11\,999$ tiếng; sync và `--check` OK; Playwright 1600×900 và 390×844: 0 `.katex-error`, 0 yêu cầu thất bại, không tràn, 5 bảng, không dòng "|", ":::" hay "$$" trong văn bản hiển thị. Máy chủ đã tắt.
