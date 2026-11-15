# Storyboard — Bộ trang chiếu Bài 07: Mạng nơ-ron, năng lực mô hình và tham số hóa thừa

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-11-15 bởi tác tử lập storyboard. Nguồn nội dung duy nhất: `materials/lec-07/lecture-note.md` (bản hiện hành); bài tập: `materials/lec-07/exercises.md`. Quy định: `CLAUDE.md` § Slide decks, `common-brief.md` (gồm "Các quy định dễ sót" và các bài học từ duyệt deck 01–04), `brief-storyboard.md`, `../rl-plan/CLAUDE.md` § Deck structure and content, nhật ký yêu cầu 2026-11-13 hàng 1–5, quyết định của điều phối viên trong `lec-0{1,…,6}/review-log.md` § Bộ trang chiếu, ba báo cáo `lec-0{3,4,5}/reviews/deck-storyboard-gate.md`. Khuôn bố cục theo storyboard Bài 06. Mọi mã trang có dạng `L07-k-mm`; trong bảng viết gọn `k-mm`.

Số âm tiết trong tệp này đếm bằng script (mục 15) theo cách của `deck_lint.py`: token cách nhau bởi khoảng trắng có chữ cái hoặc chữ số, số viết trong câu có tính, KaTeX và số trong bảng không tính, mỗi công thức hiển thị tính một dòng. Điều phối viên đếm lại trên deck.

UML: không đọc PDF trong vai này (bản giao việc chỉ cho phép ghi chú và `exercises.md`). Các mục UML trên trang "Tài liệu tham khảo" lấy từ §13 của ghi chú; số trang PDF lấy từ `outline.md` §7 (§20.1–20.3 tr. 269–274, §20.4–20.5 tr. 274–277, §26.1 tr. 375–382, §26.2 tr. 382–383, §26.3 tr. 383–385, §15.2.3 tr. 209–210, Bài tập 20.5 tr. 282–283).

## 1. Tên tệp và tiêu đề

- **Tệp deck:** `2627-1/lecture-07-mang-no-ron-tham-so-hoa-thua.html` (slug ASCII từ tên bài: "mạng nơ-ron", "tham số hóa thừa").
- **Tiêu đề deck (h1 trang bìa):** "Mạng nơ-ron, năng lực mô hình và tham số hóa thừa" (đúng tên bài của ghi chú).
- **`<title>`:** "Bài 07: Mạng nơ-ron và tham số hóa thừa".
- **Chân trang:** "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài 07".
- **Liên kết viewer:** `material-viewer.html?doc=materials/lec-07/lecture-note.md&deck=lecture-07-mang-no-ron-tham-so-hoa-thua.html` và `…exercises.md&deck=…`.
- **Màn hẹp:** chế độ đọc của `lecture-course.css` (`.slides` bọc trong `div.lecture-viewport`, script màn hẹp của `lecture-template.html`); bảng 1-06, 2-06, 3-02, 3-06, 4-04, 6-01, 6-03, 7-01, 7-06 đặt trong `.table-scroll`.
- **Trang cuối deck Bài 06** (7-07 của storyboard Bài 06) nhận liên kết tới tệp này khi deck Bài 07 xong.

## 2. Khung lý thuyết chung

**Vấn đề trung tâm (hộp "Vấn đề trung tâm", bằng lời, ≤ 30 âm tiết).** "**Câu hỏi:** đại lượng nào đo được năng lực thống kê của một lớp mạng nơ-ron khi số tham số vượt cỡ mẫu?" (câu hỏi trung tâm của ghi chú, đoạn mở đầu dòng 5; `outline.md` §1; 23 âm tiết kể cả nhãn).

**Luận điểm (trang bìa, một câu, có điều kiện, bằng lời).** "Với quan sát độc lập cùng phân bố, hàm lỗi bị chặn và lớp chọn trước khi lấy mẫu, độ phức tạp Rademacher chặn khoảng cách tổng quát hóa với xác suất cao; đại lượng này bằng một nửa cho lớp kiến trúc khớp mọi cách gán nhãn, còn trên lớp tuyến tính bị chặn theo chuẩn, cận theo lề không phụ thuộc số chiều." (Định lý 07.11, Mệnh đề 07.9(c) với Ví dụ 07.5, Hệ quả 07.16; §10 đoạn 1–3. Điều kiện ở vế đầu là (T1), (T3), (T5); 65 âm tiết theo script, bìa không tính trần. Bản ngắn 44 âm tiết ở mục 11, điểm 10.)

**Trọng tâm trực quan của deck.** Bốn chỗ, theo yêu cầu của điều phối viên:
1. **Năng lực biểu diễn so với năng lực thống kê** (2-02, 2-04, 2-05 với hình F1, 2-06, 2-11): mạng ReLU hai nơ-ron ẩn phân lớp đúng bốn điểm của phép hoặc loại trừ mà lớp nửa không gian afin sai ít nhất một (sai số xấp xỉ $0$ so với $\tfrac14$); với lớp ẩn cố định, lớp kiến trúc của thí nghiệm có $P=2000$ tham số được huấn luyện, chiều VC $d$ thỏa $m\le d\le N$, và bán kính VC $\rho_m\ge\sqrt{8\ln2}\approx2{,}35>1$.
2. **Vì sao tham số hóa thừa và nội suy không mâu thuẫn tổng quát hóa, đo theo từng đại lượng** (1-06, 2-11, 3-05, 4-04, 6-03, 6-04, 7-03, 7-04): trên cùng kiến trúc và cùng điểm huấn luyện, $P$, $P/m$, chiều VC, độ phức tạp Rademacher của lớp kiến trúc ($\tfrac12$) và lỗi huấn luyện ($0$) như nhau với nhãn thật và nhãn hoán vị; chuẩn $\lVert\hat w\rVert$ (trung bình $916$ so với $10\,853$) và lỗi kiểm tra ($0{,}023$ so với $0{,}501$) khác nhau. Bài tập tổng hợp 07.4(b), (c): $P/m=5000$ vẫn có bán kính $0{,}1095$; $P/m=0{,}005$ cho vế phải $1{,}2881>1$.
3. **Giới hạn của các cận theo đếm tham số và theo lớp kiến trúc** (2-08, 2-11, 3-05, 4-04, 5-07, 6-01): $\mathcal H_{\sin}$ có $P=1$ và độ phức tạp $\tfrac12$; nhúng vào không gian lớn hơn tăng chiều VC nhưng giữ nguyên độ phức tạp của $\mathcal F_B$; với $10^5$ đặc trưng, cận VC có $\rho_m\ge3{,}33$ còn cận theo lề có số hạng phạt $0{,}2408$.
4. **Kết quả chứng minh, kết quả đọc thêm và chỗ không chuyển kết quả lồi sang mạng** (2-01, 2-07, 6-06, 7-01): các cận của bài không dùng tính lồi; hàm mục tiêu bình phương của mạng phép hoặc loại trừ không lồi ($F(\theta_{\mathrm{mid}})=27/16$, Bài tập 07.5(c)), nên các cận của Bài 05–06 không áp dụng; Nhận xét 07.6 và 07.18 là đọc thêm, cột "Ý tưởng chứng minh" của 7-01 ghi độ sâu chứng minh của từng kết quả.

**Đối tượng và kí hiệu chung** (ghi chú §1–§2):
- quan sát $z=(x,y)\in\mathcal Z=\mathcal X\times\{0,1\}$, $\mathcal X\subseteq\mathbb R^p$, phân bố $D$ chưa biết; $\tilde y=2y-1$; tập huấn luyện $S=(Z_1,\ldots,Z_m)\sim D^m$; tập kiểm tra độc lập;
- mạng (Định nghĩa 07.1): $J$, $N_j$, $N$, $\varsigma=\operatorname{ReLU}$, $\theta=(\Theta_1,b_1,\ldots,\Theta_J,b_J)$, $f_\theta$, $h_\theta=\mathbb 1[f_\theta\ge0]$; $P$; $\mathcal H_{J,N}$, $\mathcal F_{J,N}$, $\mathcal H_{J,N}(B)$, $\hat\theta=A(S;\xi)$;
- thí nghiệm: $N=2000$, $v_j$, $b_{1j}$, $\chi(x)$, $w$, $\hat w$, $\mathcal I_S$;
- lớp tuyến tính: $h_w(x)=\langle w,x\rangle$, $h_{w,0}$, $h_{w,b}$, $\mathcal H^p_{\mathrm{aff}}$, $\mathcal H^p_{\mathrm{hom}}$, $d$; $\mathcal F_B$, $B$, $C_x$;
- độ phức tạp Rademacher: $\sigma$, $A$, $\widehat{\mathfrak R}(A)$, $\widehat{\mathfrak R}_S(\mathcal F)$, $\mathfrak R_m(\mathcal F)$; lớp hàm lỗi $\mathcal G$, $g$, $L_D(g)$, $L_S(g)$; nhãn ngẫu nhiên $\tau$, $\operatorname{err}_\tau$; trong chứng minh: $\Psi$, $S'$, $c_i$, $t$;
- lề: $\gamma$, $\phi_\gamma$, $\ell_\gamma$, $L^\gamma_D$, $L^\gamma_S$, $L^{<\gamma}_S$; lưới $\gamma_k$, $q_k$;
- cục bộ của ví dụ: $s=x_1+x_2$ (Mệnh đề 07.2), $c$ (Ví dụ 07.2), $\theta_{\mathrm{swap}}$, $\theta_{\mathrm{mid}}$, $F$ (Bài tập 07.5), $K$ (Ví dụ 07.11).

**Giả thiết** (ghi chú §2): (T1) lấy mẫu; (T3) lớp hàm lỗi bị chặn trong $[0,1]$; (T5) lớp hàm lỗi cố định trước khi lấy mẫu; (M) xấp xỉ được bởi một lớp con đếm được; dữ liệu bị chặn $\lVert x\rVert\le C_x$; bán kính và lề $B$, $\gamma$ cố định trước khi lấy mẫu. Không có giả thiết tối ưu: không tính lồi, tính trơn, sự hội tụ.

**Chuỗi định nghĩa → kết quả → phương pháp.**
1. Thí nghiệm nhãn thật và nhãn hoán vị: cùng kiến trúc, cùng lỗi huấn luyện $0$, lỗi kiểm tra $0{,}023$ so với $0{,}501$ (Câu hỏi mở đầu).
2. Thiết lập tám thành phần (§1), kí hiệu và giả thiết (§2); Ví dụ 07.1 và ứng dụng phân lớp văn bản (§3).
3. Định nghĩa 07.1 → Mệnh đề 07.2 (mạng ReLU cho phép hoặc loại trừ) → Nhận xét 07.3 (xấp xỉ phổ quát; ba năng lực ↔ ba số hạng của Mệnh đề 04.3) (§4).
4. Định nghĩa 07.4 (tham số hóa thừa, nội suy) → Định nghĩa 07.5 (lớp kiến trúc, lớp con, mô hình do huấn luyện chọn) → Ví dụ 07.2 (đổi tỉ lệ) → Ví dụ 07.3 (cận VC không cho thông tin) → Nhận xét 07.6 (đọc thêm) (§5).
5. Định nghĩa 07.7 → Bổ đề 07.8 → Ví dụ 07.4 → Mệnh đề 07.9 → Ví dụ 07.5 (độ phức tạp $\tfrac12$ cho cả hai loại nhãn) (§6).
6. Bổ đề 07.10 (McDiarmid) → Định lý 07.11 → Ví dụ 07.6 (cận $1{,}2881$) → Nhận xét 07.12 (§7).
7. Mệnh đề 07.13 → Ví dụ 07.7 → Bổ đề 07.14 (bổ đề co) → Định nghĩa 07.15 (lề, hàm lỗi dốc) → Hệ quả 07.16 (§8).
8. Ví dụ 07.8 ($0{,}2408$) → Ví dụ 07.9 → Nhận xét 07.17 (lưới) → Ví dụ 07.10 (chuẩn và lề trong thí nghiệm) → Ví dụ 07.11 (lớp điểm số thay cho lớp hàm lỗi) → Nhận xét 07.18 (đọc thêm) (§9).

**Giới hạn áp dụng** (ghi chú §10): lớp chọn trước khi lấy mẫu (chọn $B$, $\gamma$ theo $S$ tốn một bất đẳng thức hợp trên lưới); hàm lỗi bị chặn (lớp điểm số không thay được lớp hàm lỗi); các cận không giải thích vì sao huấn luyện chọn nghiệm có chuẩn nhỏ; cận tuyến tính không chuyển sang mạng sâu (Nhận xét 07.18, đọc thêm); ở $m=200$, số hạng Rademacher của thí nghiệm lớn hơn $75$, cần tập kiểm tra độc lập (bán kính $0{,}0193$); nhãn hoán vị vi phạm (T1). Kết quả lồi của Bài 05–06 không chuyển sang mạng (hàm mục tiêu không lồi: Bài tập 07.5(c)). Phụ lục A, B, C chỉ vào ghi chú diễn giả; Phụ lục D cho giao thức thí nghiệm (ghi chú diễn giả 1-06, 6-03).

## 3. Bảng mạch

Bảy mạch theo đúng thứ tự các mục của ghi chú; mỗi mạch ứng với các mục liên tiếp. Mạch 2 gộp §1–§5 (năng lực biểu diễn ở §4 và giới hạn của số tham số ở §5 là hai vế của một so sánh mà mạch 2 kết thúc: lớp biểu diễn đủ, còn số tham số và chiều VC không phân biệt hai loại nhãn); tách §5 thành mạch riêng thì deck có tám mạch, vượt trần bảy. Bảng đối chiếu trang → khối ghi chú ở mục 12.

| N | Tên mạch | Mục ghi chú | Chức năng | Đầu vào | Đầu ra | `strand-lead` (âm tiết) | Từ khóa | Trang | Phút |
|---|---|---|---|---|---|---|---|---:|---:|
| 1 | Mở đầu | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết | Bìa, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, ví dụ thí nghiệm | Bài 03: cận VC; Bài 06: ổn định cần hàm lỗi lồi | Câu hỏi: vì sao cùng mạng, cùng lỗi huấn luyện $0$, lỗi kiểm tra khác nhau | (không có trang tiêu đề mạch) | — | 6 | 9 |
| 2 | Năng lực biểu diễn và số tham số | §1–§5 | Thiết lập; Ví dụ 07.1, ứng dụng; Định nghĩa 07.1; Mệnh đề 07.2 và ý tưởng chứng minh; Nhận xét 07.3; Bài tập 07.5(c); Định nghĩa 07.4, 07.5; Ví dụ 07.2, 07.3; Nhận xét 07.6 (ghi chú diễn giả) | cận VC và Mệnh đề 04.3 | Mạng nhỏ có sai số xấp xỉ $0$ trên Ví dụ 07.1; $P$, chiều VC, $\rho_m$ của lớp kiến trúc như nhau với hai loại nhãn, $\rho_m>1$ | "Mạng nhỏ khớp được bốn điểm mà hàm afin không khớp được, nhưng số tham số không phân biệt nhãn thật với nhãn hoán vị." (25) | năng lực biểu diễn · tham số hóa thừa · nội suy · lớp kiến trúc · đổi tỉ lệ | 12 | 27 |
| 3 | Độ phức tạp Rademacher | §6 | Định nghĩa 07.7; Ví dụ 07.4 và Bổ đề 07.8; Mệnh đề 07.9 và ý tưởng chứng minh; Ví dụ 07.5; Bài tập 07.2(c) | cần đại lượng cho lớp hàm giá trị thực | $\widehat{\mathfrak R}=\tfrac12-\mathbb E_\tau\min\operatorname{err}_\tau\le\tfrac12$; lớp kiến trúc đạt $\tfrac12$ với cả hai loại nhãn | "Mức một lớp khớp được nhãn ngẫu nhiên đo năng lực thống kê, và bằng một nửa khi lớp khớp mọi cách gán nhãn." (24) | biến Rademacher · độ phức tạp Rademacher thực nghiệm · nhãn ngẫu nhiên · lỗi khớp | 7 | 15 |
| 4 | Cận tổng quát hóa theo độ phức tạp Rademacher | §7 | Bổ đề 07.10; Định lý 07.11 và ý tưởng chứng minh; Ví dụ 07.6; Nhận xét 07.12 (ghi chú diễn giả); Bài tập 07.2(b) | độ phức tạp của mạch 3; mẫu bóng của Bài 03 | Với xác suất ít nhất $1-\delta$: $L_D\le L_S+2\widehat{\mathfrak R}_S+3\sqrt{\ln(2/\delta)/(2m)}$; với lớp kiến trúc, vế phải $1{,}2881$ | "Mức khớp dấu ngẫu nhiên trên tập huấn luyện chặn khoảng cách tổng quát hóa của mọi hàm trong lớp, với xác suất cao." (24) | bất đẳng thức McDiarmid · mẫu bóng · cận phụ thuộc dữ liệu · cận không cho thông tin | 6 | 16 |
| 5 | Lớp tuyến tính bị chặn theo chuẩn và lề | §8 | Mệnh đề 07.13 và ý tưởng chứng minh (với Ví dụ 07.7); Bổ đề 07.14; Định nghĩa 07.15 (hình F2); Hệ quả 07.16 và ý tưởng chứng minh; Bài tập 07.3(d) | cần một lớp có độ phức tạp nhỏ chứa hàm do huấn luyện chọn | $\widehat{\mathfrak R}(\mathcal F_B)\le BC_x/\sqrt m$; cận theo lề với số hạng $2BC_x/(\gamma\sqrt m)$, không phụ thuộc $p$ | "Khi chuẩn trọng số bị chặn, độ phức tạp của lớp tuyến tính và cận cho lỗi phân lớp không phụ thuộc số chiều." (24) | lớp bị chặn theo chuẩn · bổ đề co · lề · hàm lỗi dốc · tỉ lệ vi phạm lề | 8 | 20 |
| 6 | Cận theo chuẩn và lề khi tham số hóa thừa | §9 | Ví dụ 07.8; Nhận xét 07.17; Ví dụ 07.10 (hai trang, hình F3); Ví dụ 07.11; Ví dụ 07.9 (ghi chú diễn giả); Nhận xét 07.18 (đọc thêm) | cận theo lề của mạch 5 | Với $10^5$ đặc trưng: $+0{,}2408$; trong thí nghiệm chuẩn khác $11{,}85$ lần nhưng cận lớn hơn $1$; lớp điểm số không thay được lớp hàm lỗi | "Cận theo chuẩn và lề cho thông tin khi phân lớp văn bản, nhưng lớn hơn một trong thí nghiệm mở đầu." (22) | phân lớp văn bản · lưới lề · lề chuẩn hóa · tập kiểm tra · mạng sâu | 7 | 17 |
| 7 | Tổng kết | §10–§13 | Bảng kết quả, trả lời vấn đề trung tâm, bài tập tổng hợp (Bài tập 07.4(b), (c)), tự kiểm tra, bài tập về nhà, tài liệu | mọi kết quả | Cầu nối sang Bài 08 | "Năng lực thống kê đo trên lớp chứa hàm do huấn luyện chọn; số tham số không quyết định bảo đảm." (21) | — | 9 | 16 |
| | **Tổng** | | | | | | | **55** | **120** |

Số trang (54) vượt mục tiêu 45–52 hai trang, dưới trần 55. Lý do: năm kết quả chính có trang phát biểu và trang "Ý tưởng chứng minh" riêng (Mệnh đề 07.2, Mệnh đề 07.9, Định lý 07.11, Mệnh đề 07.13, Hệ quả 07.16: 10 trang); bốn trang bài tập giữa cụm (mạch 2–5) và một bài tập tổng hợp hai trang; Ví dụ 07.10, câu trả lời của thí nghiệm mở đầu, cần hai trang (bảng chuẩn cùng hình F3; cận và tập kiểm tra). Đã gộp để giữ 54: Ví dụ 07.1 và khối ứng dụng §3 chung trang 2-02 (hai thẻ); bảng ba năng lực vào trang Nhận xét 07.3 (2-06); Nhận xét 07.6 (đọc thêm) vào ghi chú diễn giả 2-11; Bổ đề 07.8 vào trang Ví dụ 07.4 (3-02); Ví dụ 07.7 vào trang ý tưởng chứng minh Mệnh đề 07.13 (5-02); Nhận xét 07.12 và Ví dụ 07.9 vào ghi chú diễn giả (4-04, 6-05); Phụ lục A–D ở ghi chú diễn giả. Phương án rút còn 52 ở mục 11, điểm 2.

## 4. Bảng kết quả chính

Số hiệu theo ghi chú. Ánh xạ blueprint → ghi chú (theo `outline.md` §2): Example/Proposition 7.1 → Mệnh đề 07.2; Theorem 7.2 → Định lý 07.11; Proposition 7.3 → Mệnh đề 07.13; Corollary 7.4 → Hệ quả 07.16; Supplement → Nhận xét 07.18. Mệnh đề 07.9 là sự kiện nối độ phức tạp với thí nghiệm (QĐ 5 của dàn ý). Bổ đề 07.8, 07.10, 07.14 là công cụ. Mọi phát biểu rút gọn trên trang dùng "Giả thiết:" và "Bảo đảm:", giữ đủ giả thiết, lượng từ, hằng số và loại bảo đảm của ghi chú.

| Kết quả | Loại bảo đảm | (a) Trực quan | (b) Ý tưởng chứng minh | (c) Kỹ thuật | (d) Ví dụ bổ trợ | Trang |
|---|---|---|---|---|---|---|
| **Mệnh đề 07.2** (biểu diễn phép hoặc loại trừ bằng mạng ReLU; chứng minh đầy đủ) | tất định, chỉ về bốn điểm của $\{0,1\}^2$ | Hai nơ-ron ẩn cùng đọc tổng $s=x_1+x_2$; nơ-ron thứ hai chỉ bật khi $s>1$ và trừ đi gấp đôi, nên điểm số tăng ở $s=1$ rồi quay về âm ở $s=2$. Hình F1: miền $f_\theta\ge0$ là một dải, không phải nửa mặt phẳng. | Ba bước: hai hàng của $\Theta_1$ bằng nhau nên $f_\theta$ chỉ phụ thuộc $s$; ba giá trị tại $s=0,1,2$; $s=1$ khi và chỉ khi $x_1\oplus x_2=1$. Bỏ hàm kích hoạt phi tuyến: không có trong ghi chú, không đưa lên mặt trang; đối chiếu là lớp nửa không gian afin (Ví dụ 07.1, sai ít nhất một quan sát). | Dòng "Kỹ thuật." trên 2-05: đưa hàm hai biến về một biến bằng các hàng trùng nhau của $\Theta_1$. Chỉ dùng ở đây (và Bài tập 07.1(d)). | Ví dụ 07.1 ($\min L_S=\tfrac14$ cho lớp afin); $(\tfrac12,\tfrac12)$ được gán nhãn $1$; Bài tập 07.5(c) ($27/16$). | 2-02, 2-04, 2-05, 2-06, 2-07 |
| **Mệnh đề 07.9** (độ phức tạp Rademacher và lỗi khớp nhãn ngẫu nhiên; chứng minh đầy đủ) | tất định; kì vọng chỉ theo $\tau$ hay $\sigma$; bộ điểm cố định, cho phép lặp | Dấu $\sigma_i=+1$ ứng với nhãn ngẫu nhiên $\tau_i=1$; một lớp tương quan nhiều với dấu khi nó khớp được nhãn ngẫu nhiên. Cực biên: lớp một phần tử cho $0$; lớp tách trọn vẹn cho $\tfrac12$. | Bốn bước: $\sigma_ih_i=\tau_i-\mathbb 1[h_i\ne\tau_i]$ (kiểm bốn trường hợp); trung bình theo $i$, số hạng đầu không phụ thuộc $h$, lỗi nhỏ nhất đạt được vì $\mathcal H\circ x_{1:m}$ hữu hạn; (b) $\mathbb 1[h\ne y]=h+y-2hy$ và $\sigma_i(1-2y_i)$ là biến Rademacher; (c) mỗi $\tau$ có xác suất $2^{-m}>0$. | Dòng "Kỹ thuật." trên 3-04: đổi biến $\sigma_i=2\tau_i-1$ giữa dấu và nhãn ngẫu nhiên. Chỉ dùng ở đây. | Ví dụ 07.4 ($0$; $\tfrac14$; $\tfrac13$; $\tfrac12$); Ví dụ 07.5 ($\mathcal H_{2,2000}$ và $\mathcal H_{\sin}$: $\tfrac12$); Bài tập 07.2(c) ($\mathbb E_\tau\min\operatorname{err}_\tau=\tfrac14$). | 3-03, 3-04, 3-05, 3-06 |
| **Định lý 07.11** (cận tổng quát hóa theo độ phức tạp Rademacher thực nghiệm; phác thảo, McDiarmid ở Phụ lục A) | (a) kì vọng theo $S$; (b) xác suất ít nhất $1-\delta$ theo $S$, đồng thời cho mọi $g\in\mathcal G$; cấp lớp; phụ thuộc $\delta$ qua $\ln(2/\delta)$; không chứa $p$; cận phụ thuộc dữ liệu | Đơn vị: $\widehat{\mathfrak R}_S$ đo bằng đơn vị của hàm lỗi; cực biên $\widehat{\mathfrak R}_S=\tfrac12$ cho $2\widehat{\mathfrak R}_S=1$, đã bằng giá trị lớn nhất của rủi ro 0–1; lớp một phần tử cho $0$. | Bốn bước (cộng Bước 0 cho (M)): mẫu bóng ((T1), (T5)) và $\sup\mathbb E\le\mathbb E\sup$; đổi chỗ với biến Rademacher ((T1)), tách hai cận trên đúng: $\mathbb E\Psi\le2\mathfrak R_m$; sai phân $1/m$ ((T3)); McDiarmid hai lần với $\delta/2$ và bất đẳng thức hợp. Bỏ (T1): nhãn hoán vị (Ví dụ 07.6, Bước 3); bỏ (T3): lớp điểm số (Ví dụ 07.11); bỏ (T5): chọn $B$, $\gamma$ theo $S$ (Nhận xét 07.17). | **Nhắc lại** đối xứng hóa và mẫu bóng (Bài 03, trang riêng `L03-5-06`) một dòng trên 4-03; bất đẳng thức hợp (Bài 01); ghi chú diễn giả 4-03: sai phân của một cận trên đúng không quá sai phân lớn nhất (Phụ lục C(ii)); mặt trang nêu ý này trong Bước 3. | Ví dụ 07.6 ($0{,}2881$; $0{,}0815$; $0{,}0408$; $1{,}2881$); Bài tập 07.2(b) ($0{,}2881$ so với $0{,}0866$, khoảng $3{,}33$ lần); Ví dụ 07.8. | 4-01, 4-02, 4-03, 4-04, 4-05 |
| **Mệnh đề 07.13** (độ phức tạp của lớp tuyến tính bị chặn theo chuẩn; chứng minh đầy đủ) | tất định, kì vọng chỉ theo $\sigma$; bộ điểm cố định; không phụ thuộc $p$, giảm như $1/\sqrt m$, tỉ lệ với $B$ | Tổng có dấu $v_\sigma=\sum_i\sigma_ix_i$ có bình phương độ dài trung bình $\sum_i\lVert x_i\rVert^2$, không phụ thuộc số chiều; véc-tơ $w$ tốt nhất cùng hướng $v_\sigma$. | Bốn bước: Cauchy–Schwarz trên quả cầu Euclid (đẳng thức); Jensen cho $\sqrt t$ lõm (bất đẳng thức duy nhất); số hạng chéo bằng $0$ (tính độc lập, kì vọng $0$); cận $C_x$. Dấu bằng khi các điểm trực chuẩn; lỏng $\sqrt2$ lần khi hai điểm trùng nhau (Ví dụ 07.7). | Nhắc lại "số hạng chéo bằng $0$ cho véc-tơ không tương quan" (Bài 05, một dòng) trên 5-02, dùng không cần dòng riêng. | Ví dụ 07.7 ($B/2$ so với $0{,}7071B$; $B/2=B/\sqrt m$); Bài tập 07.3(d) (nhúng vào $\mathbb R^{p'}$). | 5-01, 5-02, 5-07 |
| **Hệ quả 07.16** (cận theo lề cho phân lớp tuyến tính bị chặn theo chuẩn; phác thảo) | xác suất ít nhất $1-\delta$ theo $S$, đồng thời cho mọi $\lVert w\rVert\le B$; cấp lớp, đúng cho đầu ra của mọi thuật toán có chuẩn không quá $B$; phụ thuộc $m$, $\delta$, $BC_x/\gamma$, không phụ thuộc $p$ | Thay $(w,\gamma,B)$ bằng $(cw,c\gamma,cB)$ không đổi hàm phân lớp, tỉ lệ vi phạm lề và số hạng phạt: năng lực đo bằng tỉ số $BC_x/\gamma$. | Bốn bước: Định lý 07.11(b) cho lớp hàm lỗi dốc ($B$, $\gamma$ chọn trước; giá trị trong $[0,1]$; (M) với $w$ hữu tỉ); bổ đề co với $\phi_i(a)=\phi_\gamma(\tilde y_ia)$, $(1/\gamma)$-Lipschitz; Mệnh đề 07.13; tính chất kẹp (iii). Bỏ "chọn trước": $\gamma$ bằng lề nhỏ nhất trên $S$ làm Bước 1 hỏng (Nhận xét 07.17). | Dòng "Kỹ thuật." trên 5-06: chặn hàm lỗi 0–1 bằng một hàm lỗi bị chặn, Lipschitz nằm trên nó, rồi dùng bổ đề co. Nhắc lại "chia xác suất thất bại theo trọng số" (Bài 04, trang riêng `L04-4-04`) trên 6-02. | Ví dụ 07.8 ($0{,}2$; $0{,}2408$; cỡ mẫu $57\,958$, $231\,829$, $3690$); Ví dụ 07.10; câu hỏi cuối buổi ($0{,}2815$; $0{,}2889$). | 5-04, 5-05, 5-06, 6-01, 6-02, 6-03, 6-04, 7-05 |

**Kết quả phụ và quyết định.**
- Bổ đề 07.8 (công cụ; chứng minh đầy đủ): một dòng phát biểu trên 3-02; lộ trình (tách số hạng dịch có kì vọng $0$; $c\ge0$ giữ thứ tự; $-\sigma$ cùng phân bố với $\sigma$) ở ghi chú diễn giả 3-02. Dùng lại ở Nhận xét 07.12 (ghi chú diễn giả 4-04), Ví dụ 07.11 Bước 3 (6-05), Phụ lục B (ghi chú diễn giả 5-03).
- Bổ đề 07.10 (công cụ; phác thảo, Phụ lục A): trang 4-01 với "Trực quan." và trường hợp riêng Hoeffding; lộ trình Phụ lục A (martingale Doob, bổ đề Hoeffding có điều kiện cho từng bước tăng, phương pháp Chernoff; hằng số $2$ từ độ dài đoạn $c_k$) ở ghi chú diễn giả 4-01. Không có trang ý tưởng chứng minh riêng (mục 11, điểm 3).
- Bổ đề 07.14 (công cụ; phác thảo, Phụ lục B): trang 5-03, cùng quy ước định tâm và phản ví dụ $A=\{0\}$; lộ trình Phụ lục B ở ghi chú diễn giả 5-03.
- Nhận xét 07.3: trang 2-06 cùng bảng ba năng lực của §4.
- Nhận xét 07.6 (đọc thêm): ghi chú diễn giả 2-11.
- Nhận xét 07.12: ghi chú diễn giả 4-04 (dùng ở Ví dụ 07.9).
- Nhận xét 07.17: trang 6-02.
- Nhận xét 07.18 (đọc thêm): trang 6-06; mặt trang ghi "Chứng minh nằm ngoài phạm vi học phần" với nguồn (quy tắc tác giả: câu này không phải lời rào đón).
- Ví dụ 07.9: ghi chú diễn giả 6-05 (mục 11, điểm 4).
- Câu ôn nhanh 1–3: ghi chú diễn giả 1-02.
- §10 (ý nghĩa, giới hạn): cột "Giả thiết không được bỏ" của 7-01, trang 7-02, ghi chú diễn giả 7-02.
- §12 (câu hỏi cuối buổi): câu hỏi tự kiểm tra 3 và 4 ở 7-05 (phần (a) và (c)); phần (b) ở ghi chú diễn giả 6-02 và 7-05.
- Phụ lục D: ghi chú diễn giả 1-06 (giao thức), 6-03 ($C_x$, hạng $200$); giới hạn hạ gradient khởi tạo tại $0$ ở ghi chú diễn giả 7-07 (câu nối Bài 08).

## 5. Ví dụ bổ trợ

Ví dụ xuyên suốt: **thí nghiệm nhãn thật và nhãn hoán vị** (câu hỏi mở đầu, Ví dụ 07.3, 07.5, 07.6, 07.10; Bài tập 07.4) và **bốn điểm của phép hoặc loại trừ** (Ví dụ 07.1, Mệnh đề 07.2, Ví dụ 07.2, lề ở §8; Bài tập 07.5); thêm ứng dụng **phân lớp văn bản với $10^5$ đặc trưng** (§3, Ví dụ 07.8). Mỗi lần dùng lại trả lời một câu hỏi mới. Thí nghiệm: câu hỏi (1-06); số tham số, chiều VC, bán kính VC (2-11); độ phức tạp của lớp kiến trúc (3-05); cận của Định lý 07.11 (4-04); chuẩn, lề chuẩn hóa và tập kiểm tra (6-03, 6-04); tổng hợp (7-02). Phép hoặc loại trừ: lớp afin sai ít nhất một quan sát (2-02); mạng hai nơ-ron ẩn (2-04, 2-05); ba năng lực (2-06); hàm mục tiêu không lồi (2-07); đổi tỉ lệ (2-10); lề $\tfrac12$ (5-04). Văn bản: câu hỏi (2-02); cận theo lề và cỡ mẫu (6-01). Bài tập trên mặt trang lấy từ `exercises.md` với cùng số liệu, câu chữ và kết quả: Bài tập 07.5(c) (2-07), 07.2(c) phần cuối (3-06), 07.2(b) (4-05), 07.3(d) (5-07), 07.4(b), (c) (7-03, 7-04, tổng hợp).

Mọi con số dưới đây đã tính lại bằng Python (thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-07/storyboard/num.py`, kết quả `num.txt`) và khớp ghi chú, tệp bài tập. Số của thí nghiệm (lỗi kiểm tra, chuẩn, $C_x$, lề chuẩn hóa, khoảng của số hạng Rademacher) là số đo của Phụ lục D trong ghi chú; script chỉ kiểm chúng nhất quán với các cận suy từ khoảng đã cho. **Không có ví dụ mới mang số mới trên mặt trang.** Hình F1 vẽ miền suy từ công thức $f_\theta$ của chứng minh Mệnh đề 07.2, Bước 1 (đúng trên $\mathbb R^2$), cũng là kết quả của Lời giải Bài tập 07.1(c); hình F2 vẽ ba hàm của Định nghĩa 07.15 và tính chất (iii); hình F3 vẽ các khoảng chuẩn của Ví dụ 07.10, Bước 2.

**V1. Câu hỏi mở đầu** (1-06). $P=2000$, $m=200$, $P/m=10$; lỗi kiểm tra trung bình $0{,}023$ ($0{,}014$–$0{,}036$) và $0{,}501$ ($0{,}480$–$0{,}512$); chuẩn trung bình $916$ và $10\,853$, tỉ số $10\,853/916=11{,}848\approx11{,}85$.

**V2. Câu ôn nhanh** (ghi chú diễn giả 1-02). (1) $\mathbb E\lvert\sigma_1+\sigma_2+\sigma_3\rvert=(2\cdot3+6\cdot1)/8=1{,}5$; $\sqrt3=1{,}7321$. (2) chiều VC của $\mathcal H^N_{\mathrm{hom}}$ bằng $N$. (3) $t=\sqrt{\ln40/400}=0{,}096032$, làm tròn lên $0{,}0961$; $\ln40=3{,}688879$.

**V3. Ví dụ 07.1** (2-02). Với $w=(1,1)$, $b=-\tfrac12$: $\langle w,x\rangle+b=-\tfrac12;\ \tfrac12;\ \tfrac12;\ \tfrac32$ tại $(0,0),(1,0),(0,1),(1,1)$; sai tại $(1,1)$: $L_S=\tfrac14=\min_{\mathcal H^2_{\mathrm{aff}}}L_S$; $L_D=L_S$.

**V4. Mệnh đề 07.2** (2-04, 2-05). $f_\theta=\operatorname{ReLU}(s)-2\operatorname{ReLU}(s-1)-\tfrac12$: $s=0$: $-\tfrac12$; $s=1$: $\tfrac12$; $s=2$: $2-2-\tfrac12=-\tfrac12$; $(\tfrac12,\tfrac12)$: $s=1$, $f_\theta=\tfrac12$. Trên $\mathbb R^2$: $f_\theta=-\tfrac12$ khi $s\le0$, $s-\tfrac12$ khi $0\le s\le1$, $\tfrac32-s$ khi $s\ge1$, nên $f_\theta\ge0\iff\tfrac12\le s\le\tfrac32$ (Lời giải Bài tập 07.1(c)). Số tham số của kiến trúc $p=2$, $J=2$, $N_1=2$: $2\cdot3+1\cdot3=9$. Sai số xấp xỉ: $0$ và $\tfrac14$.

**V5. Bài tập 07.5(c)** (2-07; số của `exercises.md`). $\theta_{\mathrm{swap}}$: $b_1=(-1,0)^\top$, $\Theta_2=(-2,1)$, $F=0$ (kiểm bằng script). $\theta_{\mathrm{mid}}$: $b_1=(-\tfrac12,-\tfrac12)^\top$, $\Theta_2=(-\tfrac12,-\tfrac12)$, $f=-\operatorname{ReLU}(s-\tfrac12)-\tfrac12$: $-\tfrac12;\ -1;\ -1;\ -2$; hiệu với $\tilde y_i/2$: $0;\ -\tfrac32;\ -\tfrac32;\ -\tfrac32$; $F(\theta_{\mathrm{mid}})=\tfrac14\cdot3\cdot\tfrac94=27/16=1{,}6875$ (script: $1{,}6875$).

**V6. Ví dụ 07.2** (2-10). $\lVert c\Theta_1\rVert_F^2+\lVert cb_1\rVert^2=5c^2$; $\lVert\Theta_2/c\rVert^2=5/c^2$; $b_2^2=\tfrac14$; tổng $10{,}25$ ($c=1$), $500{,}30$ ($c=10$ và $c=0{,}1$); $\sqrt{10{,}25}=3{,}2016\approx3{,}20$; $\sqrt{500{,}30}=22{,}3674\approx22{,}37$. Chuẩn phổ (numpy): $\lVert\Theta_1\rVert_{\mathrm{op}}=2$, $\lVert\Theta_2\rVert_{\mathrm{op}}=\sqrt5$; tích $2\sqrt5=4{,}4721$.

**V7. Ví dụ 07.3** (2-11). $6000=2000\cdot(2+1)$ tham số lớp ẩn; $P/m=10$; $\rho_m\ge\sqrt{8\ln2}=2{,}3548\approx2{,}35$.

**V8. Ví dụ 07.4** (3-02). Giá trị lớn nhất theo tám bộ dấu (thứ tự của ghi chú): hai hàm $-1,0,0,2,1,1,1,2$, tổng $6$, $\widehat{\mathfrak R}=6/24=\tfrac14$; lớp hàm ngưỡng $0,1,0,2,0,1,1,3$, tổng $8$, $\tfrac13$; $\{0,1\}^3$: tổng số dấu dương $12$, $\tfrac12$; lớp một phần tử $0$ (script khớp cả bốn).

**V9. Bài tập 07.2(c), phần cuối** (3-06; số của `exercises.md`). Số điểm sai theo $\tau=(0,0,0),\ldots,(1,1,1)$: $h_a$: $1,2,2,3,0,1,1,2$; $h_{a'}$: $2,1,1,0,3,2,2,1$; nhỏ nhất: $1,1,1,0,0,1,1,1$, tổng $6$; $\mathbb E_\tau\min\operatorname{err}_\tau=6/24=\tfrac14$; $\tfrac12-\tfrac14=\tfrac14$ (script khớp).

**V10. Ví dụ 07.5** (3-05). $\widehat{\mathfrak R}=\tfrac12$ cho $\mathcal H_{2,2000}$ trên $200$ điểm và cho $\mathcal H_{\sin}$ ($P=1$) trên $\{2^{-1},\ldots,2^{-m}\}$.

**V11. Ví dụ 07.6** (4-04). $3\sqrt{\ln40/(2m)}$: $m=200$: $0{,}288097\approx0{,}2881$; $m=2500$: $0{,}081486$, làm tròn lên $0{,}0815$; $m=10^4$: $0{,}040743$, làm tròn lên $0{,}0408$. Vế phải $0+2\cdot\tfrac12+0{,}2881=1{,}2881$.

**V12. Bài tập 07.2(b)** (4-05; số của `exercises.md`). $3\sqrt{\ln40/400}\le0{,}2881$; $\sqrt{\ln20/400}=0{,}086541\le0{,}0866$, $\ln20=2{,}995732$; tỉ số $3{,}329\approx3{,}33$.

**V13. Ví dụ 07.7** (5-02). Hai điểm trùng nhau: $\mathbb E\lvert\sigma_1+\sigma_2\rvert=1$, $\widehat{\mathfrak R}=B/2$; cận $B\sqrt2/2=0{,}7071B$. Bộ trực chuẩn, $m=4$: $\lVert v_\sigma\rVert=2$, $\widehat{\mathfrak R}=\tfrac B4\cdot2=B/2=B/\sqrt m$.

**V14. Quy ước định tâm** (5-03). $A=\{0\}\subset\mathbb R^3$, $\phi_i\equiv1$: bản có trị tuyệt đối $\tfrac13\cdot1{,}5=0{,}5$ sau phép biến đổi (script: $\tfrac12$).

**V15. Lề của mạng phép hoặc loại trừ** (5-04). Tại $(0,0)$: $\tilde yf_\theta=(-1)(-\tfrac12)=\tfrac12$; tại ba điểm còn lại cũng bằng $\tfrac12$ (V4); $\gamma=\tfrac12$: $L^\gamma_S=L^{<\gamma}_S=0$.

**V16. Ví dụ 07.8** (6-01). $2\cdot10/100=0{,}2$; $0{,}2+0{,}0408=0{,}2408$; $\rho_m\ge\sqrt{16\ln2}=3{,}3302\approx3{,}33$; $3\sqrt{\ln40/2}=4{,}074305$; $(24{,}0743/0{,}1)^2=57\,957{,}21\to57\,958$; $(24{,}0743/0{,}05)^2=231\,828{,}86\to231\,829$; $(6{,}0743/0{,}1)^2=3689{,}72\to3690$.

**V17. Nhận xét 07.17 và câu hỏi cuối buổi (b)** (ghi chú diễn giả 6-02, 7-05). $\gamma=0{,}5=\gamma_1$, $q_1=\tfrac12$, $\delta q_1=0{,}025$; $3\sqrt{\ln80/5000}=0{,}088812\le0{,}0889$; cận $0{,}04+0{,}16+0{,}0889=0{,}2889$.

**V18. Ví dụ 07.10** (6-03, 6-04). Tỉ số chuẩn $11{,}85$; chuẩn của $\Theta_2$: $916/\sqrt{2000}=20{,}48\approx20{,}5$, $10\,853/\sqrt{2000}=242{,}68\approx242{,}7$. Kiểm nhất quán với $C_x\in[1{,}518;1{,}544]$: số hạng $2\lVert\hat w\rVert C_x/\sqrt{200}$ nằm trong $[75{,}35;375{,}79]$ (nhãn thật) và $[1458{,}1;3068{,}3]$ (nhãn hoán vị), chứa các khoảng $75$–$372$ và $1467$–$3047$ của ghi chú; lề chuẩn hóa nằm trong $[3{,}76\cdot10^{-4};1{,}877\cdot10^{-3}]$ và $[4{,}61\cdot10^{-5};9{,}70\cdot10^{-5}]$, chứa các khoảng của ghi chú. Bán kính tập kiểm tra $\sqrt{\ln40/10^4}=0{,}019206\le0{,}0193$. Lỗi kiểm tra so với số hạng: $75>1$.

**V19. Ví dụ 07.11** (6-05). $B=10^{-6}$, $\sqrt m=100$: $BC_x/\sqrt m=10^{-8}$; $K=\ln(1+e^{BC_x})$.

**V20. Ví dụ 07.9** (ghi chú diễn giả 6-05). $\ln80=4{,}382027$; $m=10^3$: $0{,}2530+0{,}5617=0{,}8147$; $m=10^4$: $0{,}08+0{,}1776=0{,}2576\le0{,}2577$; $m=10^5$: $0{,}0253+0{,}0562=0{,}0815$; $8+12\sqrt{\ln80/2}=25{,}7625$, $\lceil(25{,}7625/0{,}1)^2\rceil=66\,371$; $2\cdot0{,}25762=0{,}5153$.

**V21. Câu hỏi cuối buổi (a)** (7-05). $2\cdot2\cdot1/(0{,}5\cdot50)=0{,}16$; $3\sqrt{\ln40/5000}=0{,}081486\le0{,}0815$; $0{,}04+0{,}16+0{,}0815=0{,}2815$. (c): $2\cdot0{,}04/0{,}5=0{,}16$.

**V22. Bài tập 07.4(b), (c)** (7-03, 7-04; số của `exercises.md`). $r_m=\sqrt{\ln120/400}=0{,}109402\le0{,}1095$, $\ln120=4{,}787492$; $P/m=10^6/200=5000$; một phía $\sqrt{\ln60/400}=0{,}1012$ (ghi chú diễn giả). (c) $\mathbb E_\tau\min\operatorname{err}_\tau=0$; vế phải $1{,}2881$; $P/m=1/200=0{,}005$.

**V23. Bài tập 07.3(d)** (5-07): không có số.

## 6. Danh sách trang

Mỗi mục: ID, tiêu đề, loại, thời lượng; **Mặt trang** (các dòng dự kiến, theo thứ tự; `[f]` là fragment; `$$…$$` là công thức hiển thị, tính một dòng; `{{…}}` là chỉ dẫn bố cục, không lên mặt trang); **Ghi chú diễn giả** (ý chính, 40–150 âm tiết, đến ~250 cho trang ý tưởng chứng minh và trang bài tập; viết cho giảng viên và người học; không mã trang, mã ví dụ của storyboard, câu quy trình hay nguồn gốc; luôn kết thúc bằng dòng `note-source`); **Lý do / nối**; **Mục tiêu / nguồn**. Câu trên mặt trang là bản dự kiến đã tự kiểm theo `no-ai-slop` (chế độ Edit) và `eval.md`; người viết deck có thể rút gọn, không thêm khẳng định.

Quy ước chung cho người viết deck:
- Trang kết quả: "Giả thiết:" và "Bảo đảm:" (nhãn của ghi chú), trích số khối của ghi chú một lần.
- Trang tổng quan (bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm" ở mạch 1) viết bằng lời, không kí hiệu, không tiếng Anh. Lần đầu một thuật ngữ trên trang nội dung có tiếng Anh trong ngoặc (bảng mục 10).
- Mọi kí hiệu trên mặt trang đã có ở trang trước hoặc có dòng "Nhắc lại:"/"Kí hiệu:" (bảng đối chiếu mục 12 ghi chỗ đưa vào).
- "Bước 1 …", "(a)", "(b)" viết in đậm như tên bước, không thành nhãn mới; chỉ dùng nhãn của danh sách hợp lệ. "Ví dụ 07.1", "Phân lớp văn bản" ở 2-02 là tiêu đề thẻ h3, không phải nhãn.
- "Lớp nơ-ron", "lớp ẩn", "lớp ra" cho lớp của mạng; "lớp" trơn chỉ cho lớp giả thuyết, lớp hàm (`thuat-ngu.md` §10).
- Số thập phân dùng dấu phẩy KaTeX `0{,}2`; dãy số ngăn bằng `;\ `; số từ năm chữ số tách nhóm bằng `\,`; toạ độ có số thập phân viết `(0{,}3;0{,}7;0{,}2)` như ghi chú.
- Mỗi trang ví dụ mở bằng dữ kiện dạng danh sách, không câu dẫn. "Diễn giải:" chỉ dùng số có trên chính trang đó.
- Trang ý tưởng chứng minh: lộ trình 3–5 bước, bất đẳng thức hoặc mẹo then chốt, chỗ giả thiết vào, bỏ giả thiết thì hỏng ở đâu; không chép chứng minh đầy đủ của ghi chú.
- `figcaption` được `deck_lint.py` đếm: chú thích hình viết chủ yếu bằng KaTeX, dữ liệu chính đã có trong chữ của trang.
- Không `\text{}` chứa tiếng Việt trong KaTeX. Không "cận vô nghĩa" (dùng "cận không cho thông tin", `thuat-ngu.md`). Trong ghi chú diễn giả, không ghi câu nguồn gốc, mã "V7", "mục 5", không mở bằng "Trang này", "Mạch này", "Bài này".

### Mạch 1. Mở đầu (6 trang, 9 phút)

#### `1-01` Mạng nơ-ron, năng lực mô hình và tham số hóa thừa — bìa, điểm vào mạch 1 · 1 phút
- **Mặt trang:** h1 tên bài; h3 "Bài 07"; luận điểm (mục 2, một câu, bằng lời); "Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1"; "Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN".
- **Ghi chú diễn giả:** Với lớp nửa không gian afin trong $\mathbb R^p$, chiều VC bằng $p+1$, nên cận của Định lý 03.15 không cho thông tin khi số chiều vượt cỡ mẫu. Cận ổn định của Bài 06 cần hàm lỗi lồi theo tham số, còn hàm lỗi của mạng nơ-ron theo trọng số nói chung không lồi. Bài 07 đo năng lực bằng độ phức tạp Rademacher: mức một lớp hàm lỗi khớp được dấu ngẫu nhiên trên chính tập huấn luyện. Luận điểm gồm ba kết quả: cận của Định lý 07.11, giá trị một nửa của lớp kiến trúc khớp mọi cách gán nhãn, và cận theo lề của Hệ quả 07.16. Cả ba là bảo đảm cấp lớp và không dùng tính lồi. Nguồn: ghi chú Bài 07, đoạn mở đầu, §10.
- **Lý do / nối:** luận điểm cả bài → tiên quyết.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu, §10.

#### `1-02` Tiên quyết và quy ước — mở đầu · 2 phút
- **Mặt trang:**
  - **Nhắc lại:** Định lý 03.15: (T1), hàm lỗi 0–1, (T5), (M); với xác suất ít nhất $1-\delta$: $\sup_h\lvert L_S(h)-L_D(h)\rvert\le\rho_m=\sqrt{8\ln(4\Pi_{\mathcal H}(2m)/\delta)/m}$.
  - Mệnh đề 03.9: chiều VC của $\mathcal H^p_{\mathrm{aff}}$ là $p+1$, của $\mathcal H^p_{\mathrm{hom}}$ là $p$.
  - Mệnh đề 04.3: $S$ là $r$-đại diện thì $L_D(\tilde h)-L^*\le$ sai số xấp xỉ $+\,2r+\operatorname{opt}_S(\tilde h)$.
  - Bất đẳng thức hợp; bất đẳng thức Hoeffding (Định lý 02.7); cận tin cậy (Hệ quả 02.10).
  - **Kí hiệu:** $h_w(x)=\langle w,x\rangle$, $h_{w,0}=\mathbb 1[h_w\ge0]$, $\tilde y=2y-1$, $\lVert x\rVert\le C_x$; $G$-Lipschitz (Định nghĩa 05.4).
- **Ghi chú diễn giả:** Bất đẳng thức Hoeffding: với $V_1,\ldots,V_m$ độc lập trong $[a,b]$, xác suất trung bình vượt kì vọng ít nhất $t$ không quá $e^{-2mt^2/(b-a)^2}$. Hệ quả 02.10 đảo cận này thành cận tin cậy cho rủi ro của một hàm cố định trên một tập kiểm tra độc lập. Câu ôn nhanh: $\mathbb E\lvert\sigma_1+\sigma_2+\sigma_3\rvert=1{,}5$, nhỏ hơn $\sqrt3\approx1{,}7321$ theo bất đẳng thức Jensen; $m\le N$ véc-tơ độc lập tuyến tính bị lớp nửa không gian thuần nhất tách trọn vẹn, và lớp có chiều VC $N$; với $m=200$, $t=\sqrt{\ln40/400}\approx0{,}0961$ cho xác suất $0{,}025$. Mệnh đề 04.3 gồm sai số xấp xỉ, cận thống kê $2r$ và sai số tối ưu thực nghiệm; ba số hạng này trở lại ở trang ba năng lực. Nguồn: ghi chú Bài 07, Kiến thức tiên quyết, Câu hỏi ôn nhanh.
- **Lý do / nối:** nhắc lại đúng những kết quả deck dùng trên mặt trang → mục tiêu.
- **Mục tiêu / nguồn:** tất cả; Kiến thức tiên quyết.

#### `1-03` Mục tiêu — mở đầu · 1 phút
- **Mặt trang:** `ol`, năm mục tiêu của ghi chú theo thứ tự, rút gọn câu chữ:
  1. Phân biệt năng lực biểu diễn, thống kê, khả năng tối ưu; kiểm mạng ReLU cho hàm Boole.
  2. Tính độ phức tạp Rademacher bằng liệt kê bộ dấu, nối với lỗi khớp nhãn ngẫu nhiên.
  3. Phát biểu, trình bày chứng minh cận theo độ phức tạp Rademacher.
  4. Chứng minh cận cho lớp tuyến tính bị chặn theo chuẩn; tính cận theo lề.
  5. Giải thích bằng ví dụ vai trò của số tham số, chuẩn, lề, cận lớn hơn một.
- **Ghi chú diễn giả:** Mục tiêu 1 nói về một mạng ReLU nhỏ biểu diễn đúng một hàm Boole cho trước. Mục tiêu 2 là độ phức tạp Rademacher thực nghiệm của một lớp nhỏ, và đồng nhất thức nối nó với lỗi nhỏ nhất khi khớp nhãn ngẫu nhiên. Mục tiêu 3 là cận tổng quát hóa với xác suất cao. Mục tiêu 4 gồm chứng minh đầy đủ cho lớp tuyến tính, rồi suy ra cận theo lề và tính nó bằng số. Mục tiêu 5 có ba ý: số tham số không quyết định lỗi kiểm tra; chuẩn và lề cho thêm thông tin; một cận lớn hơn một không cho biết mô hình tốt hay kém. Nguồn: ghi chú Bài 07, Mục tiêu học tập.
- **Lý do / nối:** mục tiêu → bản đồ mạch.
- **Mục tiêu / nguồn:** tất cả; Mục tiêu học tập.

#### `1-04` Nội dung — mở đầu · 0,5 phút
- **Mặt trang:** `ol start="2"` với liên kết `#/2`…`#/7`: 2. Năng lực biểu diễn và số tham số; 3. Độ phức tạp Rademacher; 4. Cận tổng quát hóa theo độ phức tạp Rademacher; 5. Lớp tuyến tính bị chặn theo chuẩn và lề; 6. Cận theo chuẩn và lề khi tham số hóa thừa; 7. Tổng kết. Dòng đọc trước: "Đọc trước: UML §20.1–20.3, §26.1."
- **Ghi chú diễn giả:** Mạch 2 so năng lực biểu diễn của một mạng nhỏ với những gì số tham số và chiều VC nói về lớp mạng. Mạch 3 định nghĩa độ phức tạp Rademacher và nối nó với việc khớp nhãn ngẫu nhiên. Mạch 4 chứng minh cận tổng quát hóa theo đại lượng đó. Mạch 5 tính đại lượng đó cho lớp tuyến tính bị chặn theo chuẩn và suy ra cận theo lề. Mạch 6 áp dụng cận vào phân lớp văn bản và vào thí nghiệm mở đầu, rồi nêu các giới hạn. Nguồn: ghi chú Bài 07; §13.
- **Lý do / nối:** bản đồ mạch → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §13.

#### `1-05` Vấn đề trung tâm — mở đầu · 1 phút
- **Mặt trang:** một hộp `div.box`: "**Câu hỏi:** đại lượng nào đo được năng lực thống kê của một lớp mạng nơ-ron khi số tham số vượt cỡ mẫu?" (23 âm tiết kể cả nhãn).
- **Ghi chú diễn giả** (câu trả lời theo mạch, không trên mặt trang): (2) một mạng hai nơ-ron ẩn biểu diễn được phép hoặc loại trừ; số tham số, chiều VC và bán kính VC của lớp kiến trúc trong thí nghiệm như nhau với hai loại nhãn, và bán kính VC lớn hơn $1$; (3) độ phức tạp Rademacher bằng một nửa trừ lỗi nhỏ nhất khi khớp nhãn ngẫu nhiên, và bằng một nửa cho lớp khớp mọi cách gán nhãn; (4) với quan sát độc lập, hàm lỗi trong $[0,1]$ và lớp chọn trước, nó chặn khoảng cách tổng quát hóa với xác suất cao; (5) với chuẩn trọng số bị chặn, số hạng phạt là $2BC_x/(\gamma\sqrt m)$, không phụ thuộc số chiều; (6) cận này cho thông tin với $10^5$ đặc trưng nhưng lớn hơn $1$ trong thí nghiệm hai trăm điểm. Nguồn: ghi chú Bài 07, đoạn mở đầu, §10.
- **Lý do / nối:** một vấn đề cốt lõi → thí nghiệm cụ thể.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu.

#### `1-06` Ví dụ: nhãn thật và nhãn hoán vị — ví dụ dẫn nhập (Câu hỏi mở đầu) · 3,5 phút
- **Mặt trang:**
  - $m=200$ điểm đều trong hình tròn đơn vị; nhãn thật $y=\mathbb 1[x_1+0{,}5x_2\ge0]$.
  - Lớp nơ-ron ẩn (hidden layer): $N=2000$ nơ-ron ReLU (rectified linear unit), rút một lần rồi cố định.
  - Lớp nơ-ron ra (output layer): $w\in\mathbb R^{2000}$ có $\lVert w\rVert$ nhỏ nhất với $f(x_i)=2y_i-1$.
  - Nhãn hoán vị (permuted labels): hoán vị nhãn huấn luyện.
  - Bảng (`caption`: "Mười hạt giống ngẫu nhiên; $5000$ điểm kiểm tra"): `Nhãn | Lỗi huấn luyện | Lỗi kiểm tra trung bình | Nhỏ nhất – lớn nhất`; `Thật | 0 | 0,023 | 0,014 – 0,036`; `Hoán vị | 0 | 0,501 | 0,480 – 0,512`.
  - **Câu hỏi:** cùng mạng, cùng lỗi huấn luyện $0$; vì sao lỗi kiểm tra khác nhau?
- **Ghi chú diễn giả:** Hàm điểm số là $f(x)=\frac1{\sqrt N}\sum_jw_j\operatorname{ReLU}(\langle v_j,x\rangle+b_{1j})$, với $v_j$ đều trên đường tròn đơn vị và $b_{1j}$ đều trên $[-1,1]$; chỉ $2000$ trọng số của lớp ra được huấn luyện. Với nhãn hoán vị, nhãn không còn liên hệ với vị trí của điểm, và nhãn kiểm tra cũng được hoán vị, độc lập với tập huấn luyện. Số tham số lớn hơn số quan sát không giải thích được bảng: với nhãn thật, cùng mạng đó có lỗi kiểm tra $0{,}023$. Phép huấn luyện là bình phương tối thiểu chuẩn nhỏ nhất bằng NumPy; giao thức đầy đủ ở Phụ lục D của ghi chú. Bảng là kết quả của một thí nghiệm, không phải một định lý. Nguồn: ghi chú Bài 07, Câu hỏi mở đầu và hai đoạn sau; Phụ lục D.
- **Lý do / nối:** ví dụ dẫn nhập trước mọi định nghĩa; ví dụ xuyên suốt của bài → tiêu đề mạch 2.
- **Mục tiêu / nguồn:** 5; Câu hỏi mở đầu.

### Mạch 2. Năng lực biểu diễn và số tham số (12 trang, 27 phút)

#### `2-00` 2. Năng lực biểu diễn và số tham số — tiêu đề mạch, điểm vào mạch 2 · 0,5 phút
- **Mặt trang:** "2."; h2 "Năng lực biểu diễn và số tham số"; `p.strand-lead` (bảng mạch, 25 âm tiết); `p.strand-keys`: "năng lực biểu diễn · tham số hóa thừa · nội suy · lớp kiến trúc · đổi tỉ lệ".
- **Ghi chú diễn giả:** Lớp nửa không gian afin sai ít nhất một trong bốn điểm của phép hoặc loại trừ; một mạng ReLU với hai nơ-ron ẩn phân lớp đúng cả bốn. Mạch tách ba câu hỏi về một lớp mạng: lớp có chứa hàm tốt không, cần bao nhiêu quan sát, và thuật toán có tìm được hàm đó không. Phần sau của mạch đếm tham số của lớp mạng trong thí nghiệm: số tham số, chiều VC và bán kính VC như nhau với nhãn thật và nhãn hoán vị. Nguồn: ghi chú Bài 07, §1–§5.
- **Lý do / nối:** mạch 1 → thiết lập.
- **Mục tiêu / nguồn:** 1, 5; §1–§5.

#### `2-01` Thiết lập bài toán — thiết lập (§1, §2) · 2,5 phút
- **Mặt trang:**
  - $z=(x,y)\in\mathcal X\times\{0,1\}$, $\mathcal X\subseteq\mathbb R^p$; $S\sim D^m$ theo (T1); tập kiểm tra (test set) độc lập.
  - Lớp hàm điểm số (score function) $f$ chọn trước khi lấy mẫu; $h=\mathbb 1[f\ge0]$; hàm lỗi 0–1.
  - Thuật toán $A(S;\xi)$ bất kì (ERM, SGD, phép nội suy), đầu ra thuộc lớp.
  - Cần chặn $\sup_{h\in\mathcal H}\big(L_D(h)-L_S(h)\big)$ và $L_D(h_{\hat\theta})$, $\hat\theta=A(S;\xi)$.
  - **Giả thiết:** (T1); (T3) hàm lỗi trong $[0,1]$; (T5) lớp chọn trước; (M); không cần tính lồi.
- **Ghi chú diễn giả:** Các đại lượng chia theo nguồn ngẫu nhiên. Cố định: $D$, $p$, kiến trúc, lớp hàm, $B$, $C_x$, $\gamma$, $\delta$. Ngẫu nhiên theo dữ liệu: $S$, rủi ro thực nghiệm, độ phức tạp Rademacher thực nghiệm, tham số do huấn luyện chọn. Ngẫu nhiên theo nguồn riêng của thuật toán: khởi tạo và chỉ số của SGD; trong thí nghiệm, trọng số lớp ẩn. Chỉ trong chứng minh: biến Rademacher, mẫu bóng. Khi cố định lớp ẩn, các hàm điểm số của lớp ra lập thành một lớp chọn trước khi lấy mẫu, và kết quả cấp lớp áp dụng có điều kiện theo lớp ẩn. Giả thiết (M): một lớp con đếm được xấp xỉ mọi hàm của lớp hàm lỗi theo từng điểm. Các kết quả không dùng tính lồi, tính trơn hay sự hội tụ của thuật toán; khác Bài 05–06, hàm lỗi có thể không lồi theo tham số. Nguồn: ghi chú Bài 07, §1, §2.
- **Lý do / nối:** khung chung trước mọi kết quả → ví dụ xuyên suốt.
- **Mục tiêu / nguồn:** 3; §1, §2.

#### `2-02` Ví dụ: phép hoặc loại trừ và phân lớp văn bản — ví dụ xuyên suốt (Ví dụ 07.1, khối ứng dụng §3), hai thẻ · 2,5 phút
- **Mặt trang** {{hai thẻ `grid2`}}:
  - {{thẻ trái, tiêu đề thẻ h3 "Ví dụ 07.1"}} $\mathcal X=\{0,1\}^2$, $y=x_1\oplus x_2$, phép hoặc loại trừ (exclusive or, XOR); $D$ đều trên bốn quan sát:
  - $((0,0),0)$, $((1,0),1)$, $((0,1),1)$, $((1,1),0)$.
  - Hai đường chéo cắt nhau: mọi hàm của $\mathcal H^2_{\mathrm{aff}}$ sai ít nhất một quan sát; $w=(1,1)$, $b=-\tfrac12$ chỉ sai tại $(1,1)$: $\min L_S=\tfrac14$.
  - {{thẻ phải, tiêu đề thẻ h3 "Phân lớp văn bản"}} $p=10^5$ tần suất từ, $\lVert x\rVert\le C_x=1$, $m=10^4$; $d=p>2m$: Định lý 03.15 không cho thông tin.
  - **Câu hỏi:** $\lVert w\rVert\le B$, đa số văn bản có lề $\tilde y\langle w,x\rangle\ge\gamma$, $BC_x/\gamma=10$; tỉ lệ lỗi của $h_{w,0}$ có bảo đảm nào?
- **Ghi chú diễn giả:** Hai điểm nhãn $0$ nằm trên một đường chéo của hình vuông, hai điểm nhãn $1$ trên đường chéo kia; theo Ví dụ 03.3, Bước 3, không nửa mặt phẳng nào tách hai cặp này. Vì $D$ đều trên bốn quan sát của tập huấn luyện, $L_D=L_S$, nên giá trị $\tfrac14$ cũng là rủi ro kì vọng nhỏ nhất của lớp afin. Văn bản được biểu diễn bằng véc-tơ tần suất từ (bag of words) đã chuẩn hóa; $h_{w,0}$ thuộc $\mathcal H^p_{\mathrm{hom}}$ với chiều VC $p$ (Mệnh đề 03.9(b)). Trong câu hỏi, $B$ và $\gamma$ được chọn trước khi lấy mẫu; câu trả lời nằm ở mạch 6. Nguồn: ghi chú Bài 07, §3, Ví dụ 07.1 và khối ứng dụng.
- **Lý do / nối:** đối tượng xuyên suốt đặt ở mục của ghi chú (§3) → mạng nơ-ron.
- **Mục tiêu / nguồn:** 1, 4; §3.

#### `2-03` Mạng nơ-ron lan truyền tới — định nghĩa (Định nghĩa 07.1) · 2,5 phút
- **Mặt trang:**
  - Một mạng nơ-ron ghép nhiều hàm afin, xen giữa bởi một hàm phi tuyến.
  - **Định nghĩa 07.1.** Độ sâu (depth) $J$; $N_0=p,N_1,\ldots,N_J=1$ nơ-ron; độ rộng (width) $N=\max_{1\le j\le J-1}N_j$; hàm kích hoạt (activation function) $\varsigma$, ở đây ReLU.
  - $\theta=(\Theta_1,b_1,\ldots,\Theta_J,b_J)$, $\Theta_j\in\mathbb R^{N_j\times N_{j-1}}$, $b_j\in\mathbb R^{N_j}$: $\sum_jN_j(N_{j-1}+1)$ tham số.
  - $$a_0=x,\quad a_j=\varsigma(\Theta_ja_{j-1}+b_j)\ (j<J),\quad f_\theta(x)=\Theta_Ja_{J-1}+b_J,\quad h_\theta=\mathbb 1[f_\theta\ge0].$$
  - Ví dụ: $J=1$ cho lớp $\mathcal H^p_{\mathrm{aff}}$; $p=2$, $J=2$, $N_1=2$ có $9$ tham số; $\mathbb 1[x\in\mathbb Q]$ không thuộc lớp mạng ReLU nào.
- **Ghi chú diễn giả:** Tên đầy đủ là mạng nơ-ron lan truyền tới (feedforward neural network). Các lớp nơ-ron $1,\ldots,J-1$ là lớp ẩn, lớp $J$ là lớp ra; lớp ra không có hàm kích hoạt, nên $f_\theta(x)$ là một số thực. Với $J=1$, lớp nửa không gian afin là lớp mạng độ sâu $1$. Với $J=2$, $f_\theta(x)=\Theta_2\,\varsigma(\Theta_1x+b_1)+b_2$; ví dụ thứ hai đếm $2\cdot3+1\cdot3=9$ tham số. Ví dụ thứ ba: $f_\theta$ liên tục nên $\{f_\theta\ge0\}$ là tập đóng, còn tập số hữu tỉ thì không. Nguồn: ghi chú Bài 07, §4, Định nghĩa 07.1 và hai đoạn sau.
- **Lý do / nối:** đối tượng của mạch → mạng cho phép hoặc loại trừ.
- **Mục tiêu / nguồn:** 1; Định nghĩa 07.1.

#### `2-04` Mạng ReLU cho phép hoặc loại trừ — trực quan, kết quả (Mệnh đề 07.2) · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Hai nơ-ron ẩn cùng đọc $s=x_1+x_2$; nơ-ron thứ hai bật khi $s>1$ và kéo điểm số xuống.
  - **Mệnh đề 07.2.** **Giả thiết:** $p=2$, $J=2$, $N_1=2$, ReLU; $\Theta_1$ có hai hàng $(1,1)$, $b_1=(0,-1)^\top$, $\Theta_2=(1,-2)$, $b_2=-\tfrac12$; $x\in\{0,1\}^2$.
  - **Bảo đảm:** tất định, chỉ về bốn điểm của $\{0,1\}^2$:
  - $$f_\theta(x)=\operatorname{ReLU}(s)-2\operatorname{ReLU}(s-1)-\tfrac12$$
  - nhận $-\tfrac12$, $\tfrac12$, $\tfrac12$, $-\tfrac12$ tại $(0,0)$, $(1,0)$, $(0,1)$, $(1,1)$; do đó $h_\theta(x)=x_1\oplus x_2$.
- **Ghi chú diễn giả:** Hai hàng của $\Theta_1$ bằng nhau, nên hai nơ-ron ẩn nhận cùng đầu vào $s$ và chỉ khác hệ số tự do: nơ-ron thứ nhất cho $\operatorname{ReLU}(s)$, nơ-ron thứ hai cho $\operatorname{ReLU}(s-1)$, nhân với $-2$ ở lớp ra. Hệ số tự do $-\tfrac12$ của lớp ra đặt ngưỡng của quy ước $f_\theta\ge0$ giữa hai giá trị $-\tfrac12$ và $\tfrac12$. Bảo đảm chỉ nói về bốn điểm; mạng cũng gán nhãn cho mọi điểm khác của mặt phẳng, và trang sau vẽ miền đó. Nguồn: ghi chú Bài 07, §4, Mệnh đề 07.2.
- **Lý do / nối:** trực quan và phát biểu chung trang; ý tưởng chứng minh ở trang riêng.
- **Mục tiêu / nguồn:** 1; Mệnh đề 07.2.

#### `2-05` Ý tưởng chứng minh: mạng ReLU cho phép hoặc loại trừ — ý tưởng chứng minh, hình F1 · 2 phút
- **Mặt trang** {{`grid2`: chữ trái, hình F1 phải}}:
  - **Bước 1.** Hai hàng của $\Theta_1$ bằng nhau: $\Theta_1x+b_1=(s,\ s-1)^\top$, nên $f_\theta$ chỉ phụ thuộc $s$.
  - **Bước 2.** Trên $\{0,1\}^2$, $s\in\{0,1,2\}$, với $f_\theta=-\tfrac12;\ \tfrac12;\ 2-2-\tfrac12=-\tfrac12$.
  - **Bước 3.** $s=1$ khi và chỉ khi $x_1\oplus x_2=1$.
  - Trên $\mathbb R^2$: $f_\theta\ge0$ khi và chỉ khi $\tfrac12\le x_1+x_2\le\tfrac32$; tại $(\tfrac12,\tfrac12)$, $f_\theta=\tfrac12$, $h_\theta=1$.
  - **Kỹ thuật.** Các hàng trùng nhau của $\Theta_1$ đưa hàm hai biến về hàm một biến $s$.
  - {{hình F1 `vung-hoac-loai-tru.svg`; `figcaption` ở mục 8}}
- **Ghi chú diễn giả:** Lộ trình gồm ba phép tính, không cần bất đẳng thức. Ở Bước 2, với $s=2$ cả hai nơ-ron bật: $\operatorname{ReLU}(2)=2$ và $2\operatorname{ReLU}(1)=2$ triệt tiêu nhau, còn lại $-\tfrac12$. Với $s\le0$, $f_\theta=-\tfrac12$; với $0\le s\le1$, $f_\theta=s-\tfrac12$; với $s\ge1$, $f_\theta=\tfrac32-s$. Miền $f_\theta\ge0$ là dải đóng giữa hai đường thẳng song song, nên hai nơ-ron ẩn cho hai biên tuyến tính, còn một hàm phân lớp afin chỉ có một biên. Điểm $(\tfrac12,\tfrac12)$ không có trong tập huấn luyện nhưng được gán nhãn $1$: phân lớp đúng bốn điểm chỉ xác định hàm phân lớp trên bốn điểm đó. Nguồn: ghi chú Bài 07, chứng minh Mệnh đề 07.2 và đoạn sau; Lời giải Bài tập 07.1(c).
- **Lý do / nối:** trang ý tưởng chứng minh riêng; hình miền → so sánh ba năng lực.
- **Mục tiêu / nguồn:** 1; chứng minh Mệnh đề 07.2.

#### `2-06` Ba năng lực của một lớp mạng — kết quả (Nhận xét 07.3), so sánh (§4 cuối) · 2,5 phút
- **Mặt trang:**
  - **Nhận xét 07.3.** Xấp xỉ phổ quát (universal approximation): mạng sigmoid xấp xỉ đều mọi hàm Lipschitz
  - trên $[-1,1]^p$ tới sai số $\epsilon$, với số nơ-ron tăng theo hàm mũ của $p$.
  - Bảng: `Năng lực | Số hạng của Mệnh đề 04.3 | Ví dụ 07.1`; `biểu diễn (expressivity) | sai số xấp xỉ | 0 và 1/4`; `thống kê (statistical capacity) | 2r | —`; `tối ưu | sai số tối ưu thực nghiệm | —`.
  - Xấp xỉ phổ quát chỉ chặn số hạng đầu.
- **Ghi chú diễn giả:** Trên Ví dụ 07.1, rủi ro tham chiếu $L^*=0$ vì nhãn là hàm tất định của $x$; lớp mạng độ sâu $2$ với hai nơ-ron ẩn có sai số xấp xỉ $0$, còn lớp afin có $\tfrac14$: hai số ở cột cuối của bảng. Với kích hoạt dấu, mọi hàm Boole trên $\{\pm1\}^p$ có một mạng độ sâu $2$, cũng với số nơ-ron tăng theo hàm mũ của $p$ (UML §20.3). Các kết quả này không cho biết cần bao nhiêu quan sát hay thuật toán nào tìm được hàm tốt. Với kích hoạt dấu, ba nơ-ron ẩn và một nơ-ron hằng, tìm nghiệm ERM đã là bài toán NP-khó (NP-hard) (UML §20.5): đó là số hạng thứ ba. Các mạch sau đo số hạng thứ hai, khi $S$ là $r$-đại diện. Nguồn: ghi chú Bài 07, Nhận xét 07.3 và đoạn sau; UML §20.3, §20.5.
- **Lý do / nối:** ba câu hỏi khác nhau → bài tập về khả năng tối ưu → số tham số.
- **Mục tiêu / nguồn:** 1; Nhận xét 07.3, §4 cuối.

#### `2-07` Bài tập: hàm mục tiêu không lồi của mạng phép hoặc loại trừ — bài tập (Bài tập 07.5(c)) · 2,5 phút
- **Mặt trang:**
  - Bốn quan sát của Ví dụ 07.1, $\tilde y\in\{\pm1\}$, kiến trúc của Mệnh đề 07.2: $F(\theta)=\tfrac14\sum_{i=1}^4\big(f_\theta(x_i)-\tilde y_i/2\big)^2$.
  - **Câu hỏi:** $\theta_{\mathrm{swap}}$ đổi chỗ hai nơ-ron ẩn của $\theta$. Chứng minh $F(\theta_{\mathrm{swap}})=0$,
  - tính $F(\theta_{\mathrm{mid}})$, $\theta_{\mathrm{mid}}=\tfrac12(\theta+\theta_{\mathrm{swap}})$; kết luận về tính lồi của $F$.
  - **Lời giải:** [f] đổi thứ tự hai số hạng: $f_{\theta_{\mathrm{swap}}}=f_\theta=\tilde y_i/2$ tại bốn điểm, $F(\theta_{\mathrm{swap}})=0$.
  - [f] $b_1=(-\tfrac12,-\tfrac12)^\top$, $\Theta_2=(-\tfrac12,-\tfrac12)$: $f_{\theta_{\mathrm{mid}}}=-\operatorname{ReLU}(s-\tfrac12)-\tfrac12$; hiệu với $\tilde y_i/2$: $0;\ -\tfrac32;\ -\tfrac32;\ -\tfrac32$.
  - [f] $F(\theta_{\mathrm{mid}})=27/16>0=\tfrac12F(\theta)+\tfrac12F(\theta_{\mathrm{swap}})$: $F$ không lồi.
- **Ghi chú diễn giả** (~200 âm tiết): Đổi chỗ hai nơ-ron ẩn nghĩa là đổi hai hàng của $\Theta_1$, hai tọa độ của $b_1$ và hai tọa độ của $\Theta_2$. Hai hàng của $\Theta_1$ đều bằng $(1,1)$, nên $\theta_{\mathrm{swap}}$ có $b_1=(-1,0)^\top$, $\Theta_2=(-2,1)$, $b_2=-\tfrac12$. Tại trung điểm, hai nơ-ron ẩn cùng tính $\operatorname{ReLU}(s-\tfrac12)$, và hàm điểm số nhận $-\tfrac12$, $-1$, $-1$, $-2$ tại bốn điểm; trung điểm của hai nghiệm khớp đúng sai hai trong bốn quan sát. Với hàm lồi, giá trị tại trung điểm không vượt trung bình giá trị ở hai đầu, ở đây bằng $0$. Các bảo đảm hội tụ của Bài 05 cho hàm lồi không áp dụng cho hàm mục tiêu này, như Ví dụ 05.10. Phần (b) của bài tập cho thêm một hiện tượng: hạ gradient khởi tạo tại $0$ giữ $\Theta_1$, $b_1$, $\Theta_2$ bằng $0$ ở mọi bước, và hàm trả về sai một nửa số quan sát, dù lớp chứa nghiệm khớp đúng. Nguồn: `exercises.md`, Bài tập 07.5(b), (c); ghi chú Bài 07, Nhận xét 07.3.
- **Lý do / nối:** bài tập của cụm năng lực biểu diễn (khả năng tối ưu, hàm mục tiêu không lồi) → số tham số.
- **Mục tiêu / nguồn:** 1; Bài tập 07.5(c).

#### `2-08` Tham số hóa thừa và nội suy — định nghĩa (Định nghĩa 07.4) · 2,5 phút
- **Mặt trang:**
  - **Nhắc lại:** Nhận xét 03.10: $\mathcal H_{\sin}$ có một tham số, chiều VC vô hạn; lớp $\{\mathbb 1[(w_1+\cdots+w_p)x\ge0]\}$ có $p$ tham số, ba hàm.
  - **Định nghĩa 07.4.** $P$: số tham số chọn theo dữ liệu; tham số hóa thừa (overparameterization): $P>m$.
  - Nội suy (interpolation): $h_\theta(x_i)=y_i\ \forall i$ với một $\theta$; nội suy mọi cách gán nhãn: $\{h_\theta\}$ tách trọn vẹn $(x_1,\ldots,x_m)$.
  - Tham số hóa thừa không kéo theo nội suy, và ngược lại.
- **Ghi chú diễn giả:** Nếu lớp phân lớp đúng mọi cách gán nhãn của tập huấn luyện, lỗi huấn luyện bằng $0$ không phân biệt nhãn mang thông tin với nhãn không mang thông tin; số tham số là đại lượng đầu tiên để đo kích thước của lớp. Tham số rút trước khi lấy mẫu rồi giữ cố định không được đếm. Tham số hóa thừa là một phép đếm, phụ thuộc $m$: mạng của thí nghiệm có $P=2000>m=200$, nhưng không tham số hóa thừa với $m=10^5$. Nội suy là tính chất của lớp trên một bộ điểm. Lớp một tham số $\mathcal H_{\sin}$ tách trọn vẹn những bộ điểm lớn tùy ý; lớp $p$ tham số chỉ gồm ba hàm và không cho nhãn $(0,0)$ trên hai điểm $x_1<0<x_2$. Nguồn: ghi chú Bài 07, §5, Định nghĩa 07.4 và hai đoạn sau.
- **Lý do / nối:** phản ví dụ của Bài 03 mở khái niệm → ba đối tượng của một bảo đảm.
- **Mục tiêu / nguồn:** 5; Định nghĩa 07.4.

#### `2-09` Lớp kiến trúc và mô hình do huấn luyện chọn — định nghĩa (Định nghĩa 07.5) · 2,5 phút
- **Mặt trang:**
  - **Định nghĩa 07.5.** Lớp kiến trúc (architecture class) $\mathcal H_{J,N}=\{h_\theta:\theta\in\mathbb R^P\}$: cố định trước khi lấy mẫu.
  - Lớp con bị chặn theo chuẩn (norm-bounded class) $\mathcal H_{J,N}(B)$: $\lVert\theta\rVert\le B$, $B$ chọn trước.
  - Mô hình do huấn luyện chọn (model selected by training) $h_{\hat\theta}$, $\hat\theta=A(S;\xi)$: phụ thuộc $S$.
  - Bảo đảm cấp lớp (class-level) đúng cho $h_{\hat\theta}$ khi $\lVert\hat\theta\rVert\le B$, với mọi thuật toán.
  - Với $B=\lVert\hat\theta\rVert$, lớp phụ thuộc $S$ (lỗi của Ví dụ 03.8).
- **Ghi chú diễn giả:** Một bảo đảm học có thể nói về một lớp hay về riêng hàm mà phép huấn luyện chọn. Lớp kiến trúc gồm mọi hàm mà kiến trúc biểu diễn được; lớp hàm điểm số tương ứng là $\mathcal F_{J,N}$. Bảo đảm cấp lớp của Bài 02–03 đúng đồng thời cho mọi hàm của một lớp cố định trước khi lấy mẫu, nên đúng cho hàm do huấn luyện chọn mỗi khi hàm đó thuộc lớp, bất kể thuật toán. Bảo đảm này không nói thuật toán chọn hàm nào; đó là việc của bảo đảm cấp thuật toán, như ở Bài 06. Ví dụ 03.8 lập một lớp sau khi xem tập huấn luyện rồi dùng cận cho lớp cố định; cùng lỗi xảy ra khi coi quả cầu bán kính $\lVert\hat\theta\rVert$ là lớp chọn trước. Nguồn: ghi chú Bài 07, §5, Định nghĩa 07.5 và hai đoạn sau.
- **Lý do / nối:** tách lớp khỏi hàm được chọn → một hàm có nhiều chuẩn tham số.
- **Mục tiêu / nguồn:** 5; Định nghĩa 07.5.

#### `2-10` Ví dụ: đổi tỉ lệ hai lớp nơ-ron kề nhau — ví dụ (Ví dụ 07.2) · 2 phút
- **Mặt trang:**
  - Mạng của Mệnh đề 07.2; $c>0$: thay $\Theta_1$, $b_1$ bằng $c\Theta_1$, $cb_1$ và $\Theta_2$ bằng $\Theta_2/c$.
  - Tính thuần nhất dương (positive homogeneity) $\operatorname{ReLU}(ct)=c\operatorname{ReLU}(t)$: cùng hàm điểm số trên $\mathbb R^2$.
  - Tổng bình phương các tham số $5c^2+5/c^2+\tfrac14$: $10{,}25$ tại $c=1$; $500{,}30$ tại $c=10$ hay $c=0{,}1$.
  - Chuẩn phổ (spectral norm): $\lVert c\Theta_1\rVert_{\mathrm{op}}=2c$, $\lVert\Theta_2/c\rVert_{\mathrm{op}}=\sqrt5/c$; tích $2\sqrt5\approx4{,}4721$ với mọi $c$.
  - **Diễn giải:** cùng một hàm, chuẩn tham số $\sqrt{10{,}25}\approx3{,}20$ hay $\sqrt{500{,}30}\approx22{,}37$; tích hai chuẩn phổ không đổi.
- **Ghi chú diễn giả:** Phép đổi tỉ lệ (rescaling) giữ $b_2=-\tfrac12$. Tổng bình phương dùng chuẩn Frobenius: $\lVert c\Theta_1\rVert_F^2+\lVert cb_1\rVert^2=c^2(4+1)$ và $\lVert\Theta_2/c\rVert^2=5/c^2$; giá trị nhỏ nhất $10{,}25$ tại $c=1$ theo bất đẳng thức trung bình cộng–trung bình nhân. Chuẩn phổ là $\max_{\lVert u\rVert=1}\lVert\Theta u\rVert$; theo Cauchy–Schwarz, dấu bằng khi $u$ cùng hướng $(1,1)$ hay $(1,-2)$. Ba chuẩn $\sqrt{10{,}25}\approx3{,}20$ và $\sqrt{500{,}30}\approx22{,}37$ thuộc cùng một hàm, nên chuẩn của toàn bộ véc-tơ tham số không xác định được từ hàm. Một đại lượng gắn với hàm phải bất biến khi đổi tỉ lệ, như tích các chuẩn phổ. Nguồn: ghi chú Bài 07, §5, Ví dụ 07.2.
- **Lý do / nối:** phản ví dụ "chuẩn tham số là đại lượng của hàm" → lớp kiến trúc của thí nghiệm.
- **Mục tiêu / nguồn:** 5; Ví dụ 07.2.

#### `2-11` Ví dụ: lớp kiến trúc của thí nghiệm mở đầu — ví dụ (Ví dụ 07.3; Nhận xét 07.6 ở ghi chú diễn giả) · 2,5 phút
- **Mặt trang:**
  - $v_j$ đều trên đường tròn đơn vị, $b_{1j}$ đều trên $[-1,1]$, độc lập với $S$.
  - Đặc trưng ngẫu nhiên (random features) $\chi(x)=\operatorname{ReLU}(\Theta_1x+b_1)/\sqrt N$; $f_\theta=\langle w,\chi\rangle$; $P=2000$, $P/m=10$.
  - Nghiệm nội suy chuẩn nhỏ nhất (minimum-norm interpolant) $\hat w=\arg\min\{\lVert w\rVert:\langle w,\chi(x_i)\rangle=\tilde y_i\ \forall i\}$.
  - Ma trận các hàng $\chi(x_i)^\top$ có hạng $200$: lớp tách trọn vẹn $200$ điểm, $m\le d\le N$.
  - Lặp mỗi điểm hai lần: $\Pi(2m)\ge2^m$, $\rho_m\ge\sqrt{8\ln2}\approx2{,}35>1$.
  - **Diễn giải:** $P$, $d$, $\rho_m$ như nhau với hai loại nhãn.
- **Ghi chú diễn giả:** Có $6000$ tham số lớp ẩn cố định và $b_2=0$; chỉ $w$ được chọn theo dữ liệu, nên $P=N$. Với lớp ẩn cố định, lớp kiến trúc $\mathcal H_{2,2000}$ là lớp nửa không gian thuần nhất trên $\chi(x)$, và $d\le N$ theo Mệnh đề 03.9(b). Hạng $200$ cho nghiệm của mọi hệ $\langle w,\chi(x_i)\rangle=\tilde y_i$, như câu ôn nhanh 2. Hai bản sao của một điểm nhận cùng nhãn, nên trên bộ $2m$ điểm lớp thực hiện đúng $2^m$ cách gán nhãn; vì $4/\delta>1$, bán kính VC ít nhất $\sqrt{8\ln2}$. Nhận xét 07.6 (đọc thêm, UML §20.4): với kích hoạt dấu và $P$ trọng số, hàm tăng trưởng không quá $(em)^P$, chiều VC là $O(P\ln P)$; cận chỉ phụ thuộc đồ thị của mạng, nên cũng không phân biệt hai loại nhãn. Nguồn: ghi chú Bài 07, §5, Ví dụ 07.3, Nhận xét 07.6; Phụ lục D.
- **Lý do / nối:** cận VC không cho thông tin cho cả hai loại nhãn → cần đại lượng cho lớp hàm giá trị thực (tiêu đề mạch 3).
- **Mục tiêu / nguồn:** 5; Ví dụ 07.3.

### Mạch 3. Độ phức tạp Rademacher (7 trang, 15 phút)

#### `3-00` 3. Độ phức tạp Rademacher — tiêu đề mạch, điểm vào mạch 3 · 0,5 phút
- **Mặt trang:** "3."; h2 "Độ phức tạp Rademacher"; `p.strand-lead` (bảng mạch, 24 âm tiết); `p.strand-keys`: "biến Rademacher · độ phức tạp Rademacher thực nghiệm · nhãn ngẫu nhiên · lỗi khớp".
- **Ghi chú diễn giả:** Chiều VC chỉ xác định cho lớp hàm phân lớp, và với lớp kiến trúc của thí nghiệm nó không phân biệt hai loại nhãn. Cần một đại lượng xác định cho cả lớp hàm giá trị thực, như lớp hàm điểm số và lớp hàm lỗi, và nhỏ đi khi lớp bị chặn theo chuẩn. Mạch định nghĩa độ phức tạp Rademacher, tính nó trên ba điểm, rồi chứng minh nó bằng một nửa trừ lỗi nhỏ nhất khi khớp nhãn ngẫu nhiên. Kết quả trao cho mạch sau: lớp kiến trúc của thí nghiệm có độ phức tạp một nửa với cả hai loại nhãn. Nguồn: ghi chú Bài 07, §5 cuối, §6.
- **Lý do / nối:** mạch 2 → định nghĩa.
- **Mục tiêu / nguồn:** 2; §6.

#### `3-01` Độ phức tạp Rademacher — định nghĩa (Định nghĩa 07.7) · 2,5 phút
- **Mặt trang:**
  - **Nhắc lại:** Định lý 03.15 dùng dấu ngẫu nhiên $\sigma_i$ rồi đếm cách gán nhãn trên mẫu gộp.
  - **Trực quan.** Với mỗi bộ dấu, chọn hàm tương quan nhiều nhất với dấu, rồi lấy trung bình.
  - **Định nghĩa 07.7.** Biến Rademacher (Rademacher variables) $\sigma_i$ độc lập, nhận $\pm1$ với xác suất $\tfrac12$; $A\subset\mathbb R^m$ khác rỗng, bị chặn:
  - $$\widehat{\mathfrak R}(A)=\mathbb E_\sigma\Big[\sup_{a\in A}\tfrac1m\textstyle\sum_{i=1}^m\sigma_ia_i\Big].$$
  - Thực nghiệm (empirical): $\widehat{\mathfrak R}_S(\mathcal F)=\widehat{\mathfrak R}(\mathcal F\circ S)$; tổng thể (population): $\mathfrak R_m(\mathcal F)=\mathbb E_S\widehat{\mathfrak R}_S(\mathcal F)$.
  - $0\le\widehat{\mathfrak R}(A)\le\sup_{a\in A}\max_i\lvert a_i\rvert$.
- **Ghi chú diễn giả:** Bước 2 của chứng minh Định lý 03.15 đưa vào các dấu ngẫu nhiên, Bước 3 đếm các cách gán nhãn trên mẫu gộp; với lớp hàm giá trị thực không còn phép đếm như vậy. $\mathcal F\circ S$ là tập véc-tơ giá trị $(f(\omega_1),\ldots,f(\omega_m))$ trên tập huấn luyện; với lớp hàm điểm số, các điểm là $X_1,\ldots,X_m$, nên độ phức tạp thực nghiệm không phụ thuộc nhãn. Vế trái của cận đơn giản đúng vì cận trên đúng không nhỏ hơn giá trị tại một véc-tơ cố định, có kì vọng $0$. Định nghĩa không có trị tuyệt đối, như UML. Dấu ngẫu nhiên đứng thay cho nhãn thật vì đại lượng $\sup_f\frac1m\sum_i\tilde y_if(x_i)$ đo mức lớp khớp nhãn của bài toán, còn $\sigma_i$ độc lập với dữ liệu, nên độ phức tạp đo khả năng khớp của riêng lớp. Nguồn: ghi chú Bài 07, §6, Định nghĩa 07.7 và ba đoạn sau.
- **Lý do / nối:** khái niệm mở bằng nhắc lại và trực quan, rồi định nghĩa → tính trên ba điểm.
- **Mục tiêu / nguồn:** 2; Định nghĩa 07.7.

#### `3-02` Ví dụ: độ phức tạp Rademacher của bốn lớp trên ba điểm — ví dụ (Ví dụ 07.4), kết quả (Bổ đề 07.8) · 2,5 phút
- **Mặt trang:**
  - $m=3$; mỗi lớp là tập $A\subset\mathbb R^3$ các véc-tơ giá trị trên ba điểm; $8$ bộ dấu đồng khả năng.
  - Bảng: `Lớp | Véc-tơ | Tổng | R̂`; `một phần tử (0,3; 0,7; 0,2) | 1 | 0 | 0`; `hai hàm (1,0,0), (0,1,1) | 2 | 6 | 1/4`; `hàm ngưỡng, x₁<x₂<x₃ | 4 | 8 | 1/3`; `mọi cách gán nhãn {0,1}³ | 8 | 12 | 1/2` {{công thức trong ô viết KaTeX; cột "Tổng" là tổng tám giá trị lớn nhất}}.
  - **Diễn giải:** $1$, $2$, $4$, $8$ véc-tơ cho $0$, $\tfrac14$, $\tfrac13$, $\tfrac12$.
  - **Bổ đề 07.8.** Tất định: $\widehat{\mathfrak R}(cA+\bar a)=\lvert c\rvert\,\widehat{\mathfrak R}(A)$ với $c\in\mathbb R$, $\bar a\in\mathbb R^m$.
- **Ghi chú diễn giả:** Công thức tính: $\widehat{\mathfrak R}(A)=\frac18\sum_\sigma\max_{a\in A}\frac13\sum_i\sigma_ia_i$, nên độ phức tạp bằng tổng tám giá trị lớn nhất chia $24$. Với hai hàm, tổng có dấu là $\sigma_1$ và $\sigma_2+\sigma_3$; chẳng hạn với $(-,-,-)$ hai tổng là $-1$ và $-2$. Lớp hàm ngưỡng tạo bốn véc-tơ $(0,0,0)$, $(0,0,1)$, $(0,1,1)$, $(1,1,1)$. Với $\{0,1\}^3$, véc-tơ tốt nhất đặt $a_i=1$ đúng tại các dấu dương, nên giá trị lớn nhất bằng số dấu dương, có kì vọng $\tfrac32$. Lớp một phần tử không có phép chọn, nên tổng có dấu có kì vọng $0$. Bổ đề 07.8: cộng hằng số vào hàm lỗi hay đổi dấu nó không đổi độ phức tạp, nhân với $c$ nhân độ phức tạp với $\lvert c\rvert$; chứng minh tách số hạng dịch, có kì vọng $0$, rồi dùng $-\sigma$ cùng phân bố với $\sigma$ khi $c<0$. Nguồn: ghi chú Bài 07, §6, Bổ đề 07.8, Ví dụ 07.4.
- **Lý do / nối:** kiểm định nghĩa bằng số; dãy $0<\tfrac14<\tfrac13<\tfrac12$ theo số véc-tơ → giá trị lớn nhất $\tfrac12$.
- **Mục tiêu / nguồn:** 2; Ví dụ 07.4, Bổ đề 07.8.

#### `3-03` Độ phức tạp Rademacher và lỗi khớp nhãn ngẫu nhiên — trực quan, kết quả (Mệnh đề 07.9) · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Hàm cố định sai trung bình nửa số nhãn ngẫu nhiên.
  - **Mệnh đề 07.9.** **Giả thiết:** $x_1,\ldots,x_m$ cố định; $\mathcal H\ne\varnothing$, hàm $\mathcal X\to\{0,1\}$;
  - nhãn ngẫu nhiên (random labels) $\tau_i$ độc lập, đều trên $\{0,1\}$; $\operatorname{err}_\tau(h)=\tfrac1m\sum_i\mathbb 1[h(x_i)\ne\tau_i]$.
  - **Bảo đảm:** tất định; (a) $\widehat{\mathfrak R}_{x_{1:m}}(\mathcal H)=\tfrac12-\mathbb E_\tau\min_h\operatorname{err}_\tau(h)$;
  - (b) lớp hàm lỗi (loss class) 0–1: cùng giá trị, mọi nhãn cố định;
  - (c) $\widehat{\mathfrak R}_{x_{1:m}}(\mathcal H)\le\tfrac12$, bằng $\tfrac12$ khi và chỉ khi $\mathcal H$ tách trọn vẹn bộ điểm.
- **Ghi chú diễn giả:** Một lớp gồm nhiều hàm chọn, với mỗi bộ nhãn ngẫu nhiên, hàm sai ít nhất; lỗi nhỏ nhất càng dưới một nửa thì độ phức tạp càng lớn. Bảo đảm là tất định; kì vọng chỉ lấy theo $\tau$ hay $\sigma$, và bộ điểm được phép có điểm lặp. Ở (b), lớp hàm lỗi là $\mathcal G=\{(x,y)\mapsto\mathbb 1[h(x)\ne y]:h\in\mathcal H\}$, xét trên $z_i=(x_i,y_i)$ với nhãn $y_i$ cố định; độ phức tạp của nó bằng độ phức tạp của $\mathcal H$ trên các $x_i$, không phụ thuộc nhãn. Cực biên: lớp một phần tử cho $0$; lớp tách trọn vẹn bộ điểm khớp đúng mọi bộ nhãn ngẫu nhiên và đạt $\tfrac12$. Nguồn: ghi chú Bài 07, §6, Mệnh đề 07.9.
- **Lý do / nối:** phát biểu sau ví dụ; ý tưởng chứng minh ở trang riêng.
- **Mục tiêu / nguồn:** 2; Mệnh đề 07.9.

#### `3-04` Ý tưởng chứng minh: độ phức tạp Rademacher và lỗi khớp nhãn ngẫu nhiên — ý tưởng chứng minh · 2 phút
- **Mặt trang:**
  - **Bước 1.** $\tau_i=(1+\sigma_i)/2$; với $h_i\in\{0,1\}$, $\sigma_ih_i=\tau_i-\mathbb 1[h_i\ne\tau_i]$ (bốn trường hợp).
  - **Bước 2 (a).** Trung bình theo $i$: $\tfrac1m\sum_i\tau_i$ không phụ thuộc $h$; cận trên đúng thành lỗi nhỏ nhất; $\mathbb E\tau_i=\tfrac12$.
  - **Bước 3 (b).** $\mathbb 1[h\ne y]=h+y-2hy$; $\sigma_i(1-2y_i)$ lại là biến Rademacher.
  - **Bước 4 (c).** Lỗi nhỏ nhất $\ge0$; mỗi $\tau$ có xác suất $2^{-m}>0$.
  - **Kỹ thuật.** Đổi biến giữa dấu và nhãn ngẫu nhiên, $\sigma_i=2\tau_i-1$.
- **Ghi chú diễn giả** (~180 âm tiết): Bốn trường hợp của Bước 1: với $(\tau_i,h_i)$ bằng $(1,1)$, $(1,0)$, $(0,1)$, $(0,0)$, hai vế lần lượt bằng $1$, $0$, $-1$, $0$. Ở Bước 2, cận trên đúng theo $h$ bằng $\tfrac1m\sum_i\tau_i$ trừ lỗi nhỏ nhất, và lỗi nhỏ nhất đạt được vì $\mathcal H$ chỉ tạo hữu hạn véc-tơ trên $m$ điểm. Ở Bước 3, số hạng $\sigma_iy_i$ không phụ thuộc $h$ và có kì vọng $0$; vì $1-2y_i\in\{\pm1\}$ cố định, nhân $\sigma_i$ với nó cho lại các biến Rademacher, nên nhãn biến mất khỏi độ phức tạp. Ở Bước 4, dấu bằng cần lỗi nhỏ nhất bằng $0$ với mọi $\tau$, vì mỗi $\tau$ có xác suất dương, tức lớp thực hiện mọi cách gán nhãn. Ý nghĩa cho học: độ phức tạp của lớp hàm lỗi 0–1 đo mức lớp khớp được nhãn không mang thông tin trên chính các điểm của tập huấn luyện. Nguồn: ghi chú Bài 07, chứng minh Mệnh đề 07.9.
- **Lý do / nối:** trang ý tưởng chứng minh riêng → áp dụng cho thí nghiệm.
- **Mục tiêu / nguồn:** 2; chứng minh Mệnh đề 07.9.

#### `3-05` Ví dụ: lớp khớp mọi cách gán nhãn — ví dụ (Ví dụ 07.5) · 2,5 phút
- **Mặt trang:**
  - Lớp kiến trúc $\mathcal H_{2,2000}$ tách trọn vẹn $200$ điểm huấn luyện: $\widehat{\mathfrak R}=\tfrac12$ (Mệnh đề 07.9(c)).
  - Theo (b): lớp hàm lỗi 0–1 có độ phức tạp $\tfrac12$ với nhãn thật và với nhãn hoán vị.
  - $\mathcal H_{\sin}$: $P=1$, tách trọn vẹn $\{2^{-1},\ldots,2^{-m}\}$ với mọi $m$: $\widehat{\mathfrak R}=\tfrac12$.
  - **Diễn giải:** $P=1$ và $P=2000$ cho cùng độ phức tạp $\tfrac12$: số tham số không xác định độ phức tạp.
- **Ghi chú diễn giả:** Lớp kiến trúc tách trọn vẹn tập huấn luyện trong cả mười lần chạy, vì ma trận đặc trưng có hạng $200$. Theo (b), giá trị $\tfrac12$ của lớp hàm lỗi không đổi khi thay nhãn thật bằng nhãn hoán vị: đại lượng của lớp không thấy nhãn. Lớp $\mathcal H_{\sin}$ của Nhận xét 03.10(ii) có một tham số nhưng cũng đạt mức lớn nhất trên các điểm $2^{-1},\ldots,2^{-m}$, như số tham số không xác định chiều VC. Nguồn: ghi chú Bài 07, §6, Ví dụ 07.5.
- **Lý do / nối:** độ phức tạp của lớp kiến trúc không phân biệt hai loại nhãn → bài tập → cận ở mạch 4.
- **Mục tiêu / nguồn:** 2, 5; Ví dụ 07.5.

#### `3-06` Bài tập: hai hàm phân lớp và nhãn ngẫu nhiên — bài tập (Bài tập 07.2(c), phần cuối) · 2,5 phút
- **Mặt trang:**
  - $a=(1,0,0)$, $a'=(0,1,1)$: giá trị của hai hàm phân lớp $h_a$, $h_{a'}$ trên ba điểm.
  - **Câu hỏi:** tính $\mathbb E_\tau\min\operatorname{err}_\tau$ bằng cách liệt kê tám giá trị của $\tau$, và kiểm Mệnh đề 07.9(a).
  - **Lời giải:** [f] số điểm sai theo $\tau$: {{bảng ngang bốn hàng × chín cột: hàng $\tau$: $(0,0,0)$, $(0,0,1)$, $(0,1,0)$, $(0,1,1)$, $(1,0,0)$, $(1,0,1)$, $(1,1,0)$, $(1,1,1)$; hàng $h_a$: $1,2,2,3,0,1,1,2$; hàng $h_{a'}$: $2,1,1,0,3,2,2,1$; hàng "nhỏ nhất": $1,1,1,0,0,1,1,1$}}
  - [f] Tổng hàng cuối $6$: $\mathbb E_\tau\min\operatorname{err}_\tau=6/24=\tfrac14$; $\tfrac12-\tfrac14=\tfrac14$, khớp Ví dụ 07.4.
  - [f] Hai hàm sai trung bình $\tfrac14$, một hàm cố định sai $\tfrac12$; phần chênh bằng độ phức tạp.
- **Ghi chú diễn giả** (~150 âm tiết): Câu hỏi là phần cuối của Bài tập 07.2(c); hai phần đầu chứng minh công thức $\widehat{\mathfrak R}(\{a,a'\})=\frac1{2m}\mathbb E\lvert\sum_i\sigma_i(a_i-a'_i)\rvert$ và áp dụng nó: với $a-a'=(1,-1,-1)$, kì vọng của trị tuyệt đối bằng $1{,}5$ theo câu ôn nhanh 1, nên độ phức tạp bằng $1{,}5/6=\tfrac14$. Mỗi ô của bảng là số điểm sai của một hàm với một bộ nhãn; cột cuối lấy hàm sai ít hơn. Hai bộ nhãn $(0,1,1)$ và $(1,0,0)$ được khớp đúng, vì đó là chính hai véc-tơ của lớp. Nguồn: `exercises.md`, Bài tập 07.2(c); ghi chú Bài 07, Mệnh đề 07.9, Ví dụ 07.4.
- **Lý do / nối:** bài tập của cụm độ phức tạp, trên đúng số liệu của Ví dụ 07.4 → tiêu đề mạch 4.
- **Mục tiêu / nguồn:** 2; Bài tập 07.2(c).

### Mạch 4. Cận tổng quát hóa theo độ phức tạp Rademacher (6 trang, 16 phút)

#### `4-00` 4. Cận tổng quát hóa theo độ phức tạp Rademacher — tiêu đề mạch, điểm vào mạch 4 · 0,5 phút
- **Mặt trang:** "4."; h2 "Cận tổng quát hóa theo độ phức tạp Rademacher"; `p.strand-lead` (bảng mạch, 24 âm tiết); `p.strand-keys`: "bất đẳng thức McDiarmid · mẫu bóng · cận phụ thuộc dữ liệu · cận không cho thông tin".
- **Ghi chú diễn giả:** Mạch chứng minh rằng độ phức tạp Rademacher chặn khoảng cách tổng quát hóa của mọi hàm trong một lớp hàm lỗi chọn trước khi lấy mẫu. Chứng minh dùng lại mẫu bóng của Bài 03 và thay bất đẳng thức Hoeffding bằng một bất đẳng thức tập trung cho chính cận trên đúng theo lớp. Áp dụng vào lớp kiến trúc của thí nghiệm, độ phức tạp một nửa cho một cận lớn hơn một. Nguồn: ghi chú Bài 07, §7.
- **Lý do / nối:** mạch 3 → công cụ tập trung.
- **Mục tiêu / nguồn:** 3; §7.

#### `4-01` Bất đẳng thức McDiarmid — vấn đề, trực quan, kết quả (Bổ đề 07.10) · 3 phút
- **Mặt trang:**
  - **Kí hiệu:** $L_D(g)=\mathbb E_{Z\sim D}g(Z)$, $L_S(g)=\tfrac1m\sum_ig(Z_i)$; $\Psi(S)=\sup_{g\in\mathcal G}\big(L_D(g)-L_S(g)\big)$.
  - $\Psi$ không là trung bình của biến độc lập: bất đẳng thức Hoeffding không áp dụng trực tiếp.
  - **Trực quan.** Không biến nào đổi $Q$ quá $c_i$; trung bình trong $[a,b]$ có $c_i=(b-a)/m$: Định lý 02.7.
  - **Bổ đề 07.10.** **Giả thiết:** $V_1,\ldots,V_m$ độc lập, $V_i\in\mathcal V_i$; $Q$ đo được; $\lvert Q(v)-Q(v')\rvert\le c_i$ khi $v$, $v'$ chỉ khác tọa độ $i$.
  - **Bảo đảm:** với mọi $t>0$, $\Pr\big(Q-\mathbb EQ\ge t\big)\le\exp\big(-2t^2/\sum_ic_i^2\big)$; cùng cận cho đuôi dưới.
- **Ghi chú diễn giả** (~170 âm tiết): Bổ đề là bất đẳng thức McDiarmid (McDiarmid's inequality), còn gọi là bất đẳng thức sai phân bị chặn (bounded differences inequality); giả thiết thứ ba là điều kiện sai phân bị chặn. Các $V_i$ không cần cùng phân bố. Với $Q$ là trung bình của $m$ biến trong $[a,b]$, đổi một biến làm $Q$ đổi không quá $(b-a)/m$, và bổ đề cho đúng Định lý 02.7(a), (b); ở đây $Q$ có thể là một cận trên đúng theo lớp. Chứng minh ở Phụ lục A: viết $Q-\mathbb EQ$ thành tổng các bước tăng của martingale Doob khi lần lượt biết $V_1,V_2,\ldots$; mỗi bước tăng có kì vọng có điều kiện $0$ và nằm trong một đoạn dài không quá $c_k$; bổ đề Hoeffding chặn hàm sinh mô-men của từng bước, nhân các cận lại rồi dùng phương pháp Chernoff. Hằng số $2$ trong số mũ đến từ độ dài $c_k$ của đoạn; chỉ dùng $\lvert U_k\rvert\le c_k$ thì số mũ yếu hơn bốn lần. Nguồn: ghi chú Bài 07, §7, Bổ đề 07.10 và đoạn sau; Phụ lục A.
- **Lý do / nối:** công cụ tập trung cho cận trên đúng → định lý chính.
- **Mục tiêu / nguồn:** 3; Bổ đề 07.10.

#### `4-02` Cận tổng quát hóa theo độ phức tạp Rademacher thực nghiệm — trực quan, kết quả (Định lý 07.11) · 3 phút
- **Mặt trang:**
  - **Trực quan.** $\widehat{\mathfrak R}_S=\tfrac12$ cho $2\widehat{\mathfrak R}_S=1$, bằng rủi ro 0–1 lớn nhất; $\widehat{\mathfrak R}_S=0$ chỉ còn số hạng tin cậy.
  - **Định lý 07.11.** **Giả thiết:** $S\sim D^m$ theo (T1); lớp hàm lỗi $\mathcal G$ đo được, thỏa (T3), (T5), (M); $\delta\in(0,1)$.
  - **Bảo đảm:** (a) theo kì vọng: $\mathbb E_S\sup_{g\in\mathcal G}\big(L_D(g)-L_S(g)\big)\le2\,\mathfrak R_m(\mathcal G)$.
  - (b) với xác suất ít nhất $1-\delta$, đồng thời cho mọi $g\in\mathcal G$:
  - $$L_D(g)\le L_S(g)+2\widehat{\mathfrak R}_S(\mathcal G)+3\sqrt{\frac{\ln(2/\delta)}{2m}}.$$
  - Cận phụ thuộc dữ liệu (data-dependent bound), cấp lớp, không chứa $p$.
- **Ghi chú diễn giả:** Vế phải của (b) tính được từ chính tập huấn luyện, nên (b) là một cận phụ thuộc dữ liệu. Bảo đảm là cấp lớp: đúng cho mọi hàm của lớp, kể cả hàm chọn theo tập huấn luyện. Cận phụ thuộc $\delta$ qua $\ln(2/\delta)$, và vế phải không chứa số chiều $p$. Câu trực quan đọc hai cực biên: khi lớp khớp mọi cách gán nhãn, riêng số hạng Rademacher đã bằng rủi ro 0–1 lớn nhất; khi lớp có một phần tử, cận chỉ còn số hạng tin cậy. Nguồn: ghi chú Bài 07, §7, Định lý 07.11.
- **Lý do / nối:** phát biểu; ý tưởng chứng minh ở trang riêng.
- **Mục tiêu / nguồn:** 3; Định lý 07.11.

#### `4-03` Ý tưởng chứng minh: cận theo độ phức tạp Rademacher — ý tưởng chứng minh · 3,5 phút
- **Mặt trang:**
  - **Nhắc lại:** đối xứng hóa và mẫu bóng (Bài 03).
  - **Bước 1 ((T1), (T5)).** Mẫu bóng $S'\sim D^m$: $L_D(g)=\mathbb E_{S'}L_{S'}(g)$; $\sup\mathbb E\le\mathbb E\sup$.
  - **Bước 2 ((T1)).** Đổi chỗ $Z_i\leftrightarrow Z'_i$ tại $\sigma_i=-1$; tách hai cận trên đúng: $\mathbb E\Psi\le2\,\mathfrak R_m(\mathcal G)$.
  - **Bước 3 ((T3)).** Mỗi hàm đổi không quá $1/m$ khi thay một quan sát, nên $\Psi$, $\widehat{\mathfrak R}_S$ cũng vậy: $c_i=1/m$.
  - **Bước 4.** Bổ đề 07.10 hai lần, mỗi lần $\delta/2$, $t=\sqrt{\ln(2/\delta)/(2m)}$; bất đẳng thức hợp: $\Psi\le2\mathfrak R_m+t\le2\widehat{\mathfrak R}_S+3t$.
- **Ghi chú diễn giả** (~220 âm tiết): Lộ trình: chặn $\mathbb E\Psi$ bằng mẫu bóng và biến Rademacher, chứng minh $\Psi$ và độ phức tạp thực nghiệm có sai phân bị chặn $1/m$, rồi dùng bất đẳng thức McDiarmid hai lần. Bất đẳng thức then chốt là $\mathbb E\Psi\le2\mathfrak R_m(\mathcal G)$. Bước 0, dùng (M): cận trên đúng theo lớp bằng cận trên đúng theo một lớp con đếm được, nên $\Psi$ và độ phức tạp thực nghiệm đo được. Bước 1 dùng tính không chệch $L_D(g)=\mathbb E_{S'}L_{S'}(g)$ cho từng $g$ cố định, nên cần lớp chọn trước. Bước 2 dùng phân bố tích $D^{2m}$ không đổi khi hoán vị tọa độ; $-\sigma$ cùng phân bố với $\sigma$, $S'$ cùng phân bố với $S$. Ở Bước 3, kỹ thuật là: nếu hai họ giá trị lệch nhau không quá $c$ tại mỗi hàm, hai cận trên đúng cũng lệch không quá $c$ (Phụ lục C(ii)). Ở Bước 4, đuôi trên áp dụng cho $\Psi$, đuôi dưới cho độ phức tạp thực nghiệm; hằng số $3$ đến từ hai lần dùng, mỗi lần với xác suất thất bại $\delta/2$. Bỏ (T1): nhãn hoán vị làm các cặp không độc lập. Bỏ (T3): lớp điểm số không bị chặn trong $[0,1]$. Bỏ (T5): chọn bán kính hay lề sau khi xem tập huấn luyện. Nguồn: ghi chú Bài 07, chứng minh Định lý 07.11 và đoạn sau; Phụ lục C.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; nhắc lại kỹ thuật của Bài 03 → cận bằng số.
- **Mục tiêu / nguồn:** 3; chứng minh Định lý 07.11.

#### `4-04` Ví dụ: cận của Định lý 07.11 bằng số — ví dụ (Ví dụ 07.6) · 3 phút
- **Mặt trang:**
  - $\delta=0{,}05$, $\ln(2/\delta)=\ln40\approx3{,}6889$; số hạng tin cậy $3\sqrt{\ln40/(2m)}$:
  - Bảng: `m | 200 | 2500 | 10⁴`; `Số hạng tin cậy | 0,2881 | 0,0815 | 0,0408`.
  - Lớp hàm lỗi 0–1 của $\mathcal H_{2,2000}$, nhãn thật: $L_S=0$, $\widehat{\mathfrak R}_S=\tfrac12$; vế phải $0+1+0{,}2881=1{,}2881$.
  - Cận không cho thông tin (vacuous bound): lớn hơn rủi ro 0–1 lớn nhất.
  - Nhãn hoán vị: tổng nhãn huấn luyện không đổi, các cặp $(x_i,y_i)$ không độc lập; (T1) không thỏa.
- **Ghi chú diễn giả:** Số hạng tin cậy với $m=200$ là $3\sqrt{\ln40/400}$, ba lần giá trị của câu ôn nhanh 3; với $m=2500$ và $10^4$, giá trị được làm tròn lên. Lớp ẩn cố định trước khi lấy mẫu, nên Định lý 07.11 áp dụng cho lớp hàm lỗi 0–1 của lớp ra với nhãn thật. Với nhãn hoán vị, tổng các nhãn hoán vị bằng tổng các nhãn thật, nên các cặp không độc lập và định lý không áp dụng. Nhận xét 07.12: áp dụng định lý cho $\mathcal G$ và cho $1-\mathcal G$, mỗi lần với $\delta/2$, và dùng Bổ đề 07.8 với $c=-1$, được cận hai phía $\lvert L_D(g)-L_S(g)\rvert\le2\widehat{\mathfrak R}_S(\mathcal G)+3\sqrt{\ln(4/\delta)/(2m)}$. Cần một lớp nhỏ hơn mà vẫn chứa hàm do huấn luyện chọn. Nguồn: ghi chú Bài 07, §7, Ví dụ 07.6, Nhận xét 07.12.
- **Lý do / nối:** cận số cho lớp kiến trúc; câu nối "cần lớp nhỏ hơn" ở ghi chú diễn giả và ở câu dẫn mạch 5 → bài tập.
- **Mục tiêu / nguồn:** 3, 5; Ví dụ 07.6.

#### `4-05` Bài tập: lớp một phần tử trong Định lý 07.11 — bài tập (Bài tập 07.2(b)) · 3 phút
- **Mặt trang:**
  - **Câu hỏi:** $g:\mathcal Z\to[0,1]$ cố định trước mẫu. Chứng minh $\mathfrak R_m(\{g\})=0$ với mọi $D$.
  - Viết Định lý 07.11(b) cho $\{g\}$; tính số hạng tin cậy với $m=200$, $\delta=0{,}05$, so với Hệ quả 02.10(c).
  - Chỉ ra bước làm cận yếu hơn với lớp một phần tử.
  - **Lời giải:** [f] $\mathbb E\sigma_i=0$: $\widehat{\mathfrak R}_S(\{g\})=0$; $L_D(g)\le L_S(g)+3\sqrt{\ln40/400}$.
  - [f] $3\sqrt{\ln40/400}\le0{,}2881$, $\sqrt{\ln20/400}\le0{,}0866$: lớn hơn khoảng $3{,}33$ lần.
  - [f] Bước 4: lần McDiarmid thứ hai thừa; một lần với $\delta$ cho đúng Hệ quả 02.10(c).
- **Ghi chú diễn giả** (~150 âm tiết): Trên mỗi mẫu, $\widehat{\mathfrak R}_S(\{g\})$ là độ phức tạp của một tập một véc-tơ, bằng $0$, nên $\mathfrak R_m(\{g\})=0$. Lớp $\{g\}$ cố định trước mẫu, nhận giá trị trong $[0,1]$ và thỏa (M). Cận trên tin cậy một phía của Hệ quả 02.10(c) là $\sqrt{\ln(1/\delta)/(2m)}$, với $\ln20\approx2{,}9957$. Với lớp một phần tử, độ phức tạp thực nghiệm và tổng thể đều bằng $0$, nên lần dùng thứ hai của bất đẳng thức McDiarmid, thêm $2t$, không cần; còn $\Psi=L_D(g)-L_S(g)$ có kì vọng $0$ và một lần với xác suất thất bại $\delta$ cho đúng Hệ quả 02.10(c). Thừa số $3$ và $\ln(2/\delta)$ là giá của một cận phụ thuộc dữ liệu đúng cho mọi lớp. Nguồn: `exercises.md`, Bài tập 07.2(b); ghi chú Bài 07, Định lý 07.11 và chứng minh.
- **Lý do / nối:** bài tập của cụm cận Rademacher: đọc lại chứng minh để thấy giá của hằng số → mạch 5.
- **Mục tiêu / nguồn:** 3; Bài tập 07.2(b).

### Mạch 5. Lớp tuyến tính bị chặn theo chuẩn và lề (8 trang, 20 phút)

#### `5-00` 5. Lớp tuyến tính bị chặn theo chuẩn và lề — tiêu đề mạch, điểm vào mạch 5 · 0,5 phút
- **Mặt trang:** "5."; h2 "Lớp tuyến tính bị chặn theo chuẩn và lề"; `p.strand-lead` (bảng mạch, 24 âm tiết); `p.strand-keys`: "lớp bị chặn theo chuẩn · bổ đề co · lề · hàm lỗi dốc · tỉ lệ vi phạm lề".
- **Ghi chú diễn giả:** Với lớp kiến trúc, cận của Định lý 07.11 lớn hơn một; cần một lớp nhỏ hơn mà vẫn chứa hàm do huấn luyện chọn. Với lớp ẩn cố định, hàm điểm số của mạng trong thí nghiệm tuyến tính theo trọng số lớp ra, nên lớp tuyến tính với trọng số trong một quả cầu là ứng viên. Mạch tính độ phức tạp của lớp đó bằng bất đẳng thức Cauchy–Schwarz, chuyển nó sang lớp hàm lỗi bằng bổ đề co, rồi ghép với Định lý 07.11 thành cận theo lề. Nguồn: ghi chú Bài 07, §8.
- **Lý do / nối:** câu nối "cần lớp nhỏ hơn" của mạch 4 → lớp tuyến tính.
- **Mục tiêu / nguồn:** 4; §8.

#### `5-01` Độ phức tạp của lớp tuyến tính bị chặn theo chuẩn — vấn đề, trực quan, kết quả (Mệnh đề 07.13) · 2,5 phút
- **Mặt trang:**
  - Lớp ẩn cố định: $\langle w,\chi(x)\rangle$ tuyến tính theo $w$; cần lớp tuyến tính có độ phức tạp nhỏ.
  - **Trực quan.** $v_\sigma=\sum_i\sigma_ix_i$ có $\mathbb E\lVert v_\sigma\rVert^2=\sum_i\lVert x_i\rVert^2$, không phụ thuộc $p$; $w$ tốt nhất cùng hướng $v_\sigma$.
  - **Mệnh đề 07.13.** **Giả thiết:** $\mathcal F_B=\{h_w:\lVert w\rVert\le B\}$, chuẩn Euclid, $B>0$; $x_1,\ldots,x_m$ cố định, $\lVert x_i\rVert\le C_x$.
  - **Bảo đảm:** tất định, kì vọng chỉ theo $\sigma$:
  - $$\widehat{\mathfrak R}_{x_{1:m}}(\mathcal F_B)\le\frac Bm\sqrt{\textstyle\sum_i\lVert x_i\rVert^2}\le\frac{BC_x}{\sqrt m}.$$
  - Không phụ thuộc $p$, giảm như $1/\sqrt m$, tỉ lệ với $B$.
- **Ghi chú diễn giả:** Lớp $\mathcal F_B$ gồm các hàm điểm số tuyến tính $h_w(x)=\langle w,x\rangle$ với $w\in\mathbb R^p$. Câu trực quan đọc cơ chế: với mỗi bộ dấu, véc-tơ tốt nhất trong quả cầu nằm cùng hướng với tổng có dấu của các điểm, và độ dài bình phương trung bình của tổng đó là tổng các $\lVert x_i\rVert^2$, không phụ thuộc số tọa độ. Nhân bán kính với $2$ thì cận nhân $2$; nhân cỡ mẫu với $4$ thì cận chia $2$. Năng lực của lớp đo bằng tích $BC_x$, không bằng số chiều $p$. Nguồn: ghi chú Bài 07, §8, đoạn mở và Mệnh đề 07.13.
- **Lý do / nối:** trực quan và phát biểu chung trang; ý tưởng chứng minh ở trang riêng.
- **Mục tiêu / nguồn:** 4; Mệnh đề 07.13.

#### `5-02` Ý tưởng chứng minh: lớp tuyến tính bị chặn theo chuẩn — ý tưởng chứng minh, ví dụ (Ví dụ 07.7) · 3 phút
- **Mặt trang:**
  - **Bước 1 (Cauchy–Schwarz; quả cầu Euclid).** $\sup_{\lVert w\rVert\le B}\tfrac1m\langle w,v_\sigma\rangle=\tfrac Bm\lVert v_\sigma\rVert$, tại $w=Bv_\sigma/\lVert v_\sigma\rVert$.
  - **Bước 2 (Jensen).** $\mathbb E\lVert v_\sigma\rVert\le\sqrt{\mathbb E\lVert v_\sigma\rVert^2}$; bất đẳng thức duy nhất.
  - **Bước 3 (độc lập, kì vọng $0$).** $\mathbb E[\sigma_i\sigma_j]=0$ khi $i\ne j$: $\mathbb E\lVert v_\sigma\rVert^2=\sum_i\lVert x_i\rVert^2$.
  - **Bước 4.** $\lVert x_i\rVert\le C_x$ cho $BC_x/\sqrt m$.
  - **Ví dụ 07.7.** $x_1=x_2=1$: $\widehat{\mathfrak R}=B/2<0{,}7071B$; $x_i=\mathbf e_i$, $m=4$: Bước 2 là đẳng thức, $\widehat{\mathfrak R}=B/\sqrt m$.
- **Ghi chú diễn giả** (~190 âm tiết): Lộ trình: tính cận trên đúng theo $w$ bằng bất đẳng thức Cauchy–Schwarz, đưa kì vọng vào trong căn bằng bất đẳng thức Jensen cho hàm lõm $t\mapsto\sqrt t$, rồi khai triển bình phương. Bước 1 là đẳng thức nhờ quả cầu Euclid: dấu bằng của Cauchy–Schwarz đạt được trong quả cầu khi $v_\sigma\ne0$. Bước 3 dùng tính độc lập và kì vọng $0$ của các biến Rademacher: số hạng chéo bằng $0$, như số hạng chéo của véc-tơ không tương quan ở Bài 05. Ví dụ 07.7 kiểm Bước 2. Với hai điểm trùng nhau ($p=1$, $m=2$), $v_\sigma=\sigma_1+\sigma_2$ nhận $2,0,0,-2$, nên $\mathbb E\lvert v_\sigma\rvert=1$ và giá trị đúng $B/2$ nhỏ hơn cận $B\sqrt2/2$. Với bốn véc-tơ đơn vị ($p=m=4$), $v_\sigma$ có chuẩn $2$ với mọi $\sigma$, nên Bước 2 là đẳng thức và cận đạt với $C_x=1$. Tóm lại, cận chặt khi các điểm trực chuẩn và lỏng $\sqrt2$ lần khi hai điểm trùng nhau. Nguồn: ghi chú Bài 07, chứng minh Mệnh đề 07.13, Ví dụ 07.7.
- **Lý do / nối:** trang ý tưởng chứng minh riêng, kèm kiểm tra bằng số → chuyển sang lớp hàm lỗi.
- **Mục tiêu / nguồn:** 4; chứng minh Mệnh đề 07.13, Ví dụ 07.7.

#### `5-03` Bổ đề co — vấn đề, kết quả (Bổ đề 07.14) · 3 phút
- **Mặt trang:**
  - Hàm lỗi là hàm Lipschitz của điểm số thì độ phức tạp chuyển về lớp điểm số.
  - **Bổ đề 07.14.** **Giả thiết:** $A\subset\mathbb R^m$ khác rỗng, bị chặn; $\phi_i$ là $G$-Lipschitz trên một tập chứa $\{a_i:a\in A\}$.
  - **Bảo đảm:** tất định: $\widehat{\mathfrak R}(\phi\circ A)\le G\,\widehat{\mathfrak R}(A)$, với $\phi(a)=(\phi_1(a_1),\ldots,\phi_m(a_m))$.
  - Bổ đề co (contraction lemma); $\phi_i$ được phép phụ thuộc $i$, chứa nhãn $\tilde y_i$.
  - **Lưu ý:** không cần $\phi_i(0)=0$; với $\mathbb E\sup\lvert\cdot\rvert$, $A=\{0\}\subset\mathbb R^3$, $\phi_i\equiv1$ cho $0$ trước, $0{,}5$ sau.
- **Ghi chú diễn giả** (~160 âm tiết): Định lý 07.11 cần một lớp hàm lỗi; bổ đề co chuyển độ phức tạp của lớp hàm lỗi về lớp điểm số khi hàm lỗi là hàm Lipschitz của điểm số. Vì Định nghĩa 07.7 không có trị tuyệt đối, bổ đề không cần điều kiện định tâm $\phi_i(0)=0$; với định nghĩa dùng $\mathbb E\sup\lvert\cdot\rvert$, cần thêm điều kiện đó. Trong ví dụ, $\phi_i\equiv1$ là $0$-Lipschitz; bản có trị tuyệt đối cho $\tfrac13\mathbb E\lvert\sigma_1+\sigma_2+\sigma_3\rvert=0{,}5$ sau phép biến đổi (câu ôn nhanh 1). Chứng minh ở Phụ lục B: với $G=1$, thay tọa độ thứ nhất $a_1$ bằng $\phi_1(a_1)$ không làm tăng độ phức tạp, vì $\phi_1(a_1)-\phi_1(a'_1)\le\lvert a_1-a'_1\rvert$ và đổi vai $a$, $a'$ bỏ được trị tuyệt đối; lặp cho từng tọa độ; trường hợp $G>0$ bất kì đưa về $G=1$ bằng Bổ đề 07.8. Nguồn: ghi chú Bài 07, §8, Bổ đề 07.14 và hai đoạn sau; Phụ lục B.
- **Lý do / nối:** công cụ nối lớp hàm lỗi với lớp điểm số → hàm lỗi Lipschitz cho phân lớp.
- **Mục tiêu / nguồn:** 4; Bổ đề 07.14.

#### `5-04` Lề và hàm lỗi dốc — định nghĩa (Định nghĩa 07.15), hình F2 · 3 phút
- **Mặt trang** {{`grid2`: chữ trái, hình F2 phải}}:
  - Hàm lỗi 0–1 không Lipschitz theo điểm số; thay bằng hàm bị chặn, Lipschitz, nằm trên nó.
  - **Định nghĩa 07.15.** Lề (margin) $\tilde yf(x)$; $\phi_\gamma(t)=\min\{1,\max\{0,1-t/\gamma\}\}$; hàm lỗi dốc (ramp loss) $\ell_\gamma(f,z)=\phi_\gamma(\tilde yf(x))$.
  - Tỉ lệ vi phạm lề (margin violation rate) $L^{<\gamma}_S(f)=\tfrac1m\sum_i\mathbb 1[\tilde y_if(x_i)<\gamma]$.
  - (i) $\ell_\gamma\in[0,1]$; (ii) $\phi_\gamma$ là $(1/\gamma)$-Lipschitz; (iii) $\mathbb 1[t\le0]\le\phi_\gamma(t)\le\mathbb 1[t<\gamma]$.
  - Lề chuẩn hóa (normalized margin) $\tilde y\langle w,x\rangle/(\lVert w\rVert C_x)$: nhân $f$ với $c>0$ nhân lề với $c$.
  - {{hình F2 `ham-loi-doc.svg`; `figcaption` ở mục 8}}
- **Ghi chú diễn giả:** Hàm dốc bằng $1$ khi $t\le0$, bằng $1-t/\gamma$ khi $0\le t\le\gamma$ và bằng $0$ khi $t\ge\gamma$; $L^\gamma_D$, $L^\gamma_S$ là rủi ro kì vọng và thực nghiệm của hàm lỗi dốc. Hàm phân lớp $\mathbb 1[f\ge0]$ sai tại $z$ thì $\tilde yf(x)\le0$, nên hàm lỗi 0–1 không quá hàm lỗi dốc, và $L^\gamma_S\le L^{<\gamma}_S$. Mạng của Mệnh đề 07.2 có lề $\tfrac12$ tại cả bốn quan sát, nên với $\gamma=\tfrac12$ tỉ lệ vi phạm lề bằng $0$; nhân lớp ra với $2$ cho lề $1$ và cùng hàm phân lớp, nên chỉ lề chuẩn hóa so sánh được hai hàm điểm số. Hàm lỗi bản lề (hinge loss) $\max\{0,1-t\}$ là $1$-Lipschitz nhưng không bị chặn; hàm lỗi 0–1 bị chặn nhưng không Lipschitz; hàm dốc có cả hai tính chất. Nguồn: ghi chú Bài 07, §8, Định nghĩa 07.15 và ba đoạn sau.
- **Lý do / nối:** hàm lỗi cho bổ đề co → cận theo lề.
- **Mục tiêu / nguồn:** 4; Định nghĩa 07.15.

#### `5-05` Cận theo lề cho phân lớp tuyến tính bị chặn theo chuẩn — trực quan, kết quả (Hệ quả 07.16) · 3 phút
- **Mặt trang:**
  - **Trực quan.** Thay $(w,\gamma,B)$ bằng $(cw,c\gamma,cB)$ không đổi hai vế: năng lực đo bằng $BC_x/\gamma$.
  - **Hệ quả 07.16.** **Giả thiết:** $S\sim D^m$ theo (T1); $\lVert x\rVert\le C_x$; lớp $\mathcal F_B$; $B$, $\gamma>0$ chọn trước khi lấy mẫu; $\delta\in(0,1)$.
  - **Bảo đảm:** với xác suất ít nhất $1-\delta$, đồng thời cho mọi $\lVert w\rVert\le B$:
  - $$L_D(h_{w,0})\le L^\gamma_D(h_w)\le L^{<\gamma}_S(h_w)+\frac{2BC_x}{\gamma\sqrt m}+3\sqrt{\frac{\ln(2/\delta)}{2m}}.$$
  - Không phụ thuộc $p$; cấp lớp: đúng cho đầu ra của mọi thuật toán có chuẩn không quá $B$.
- **Ghi chú diễn giả:** $L_D(h_{w,0})$ là rủi ro kì vọng 0–1 của hàm phân lớp $h_{w,0}$, với $y\in\{0,1\}$. Số hạng phạt phụ thuộc $m$, $\delta$ và tỉ số $BC_x/\gamma$, không phụ thuộc số chiều $p$; nhân $w$, $\gamma$, $B$ với cùng một số dương không đổi hàm phân lớp, tỉ lệ vi phạm lề hay số hạng phạt, nên chỉ tỉ số giữa chuẩn và lề đo năng lực. Bảo đảm đúng cho đầu ra của mọi thuật toán có chuẩn không quá $B$, kể cả hạ gradient ngẫu nhiên trên hàm lỗi logistic (logistic loss), và không dùng tính lồi. Nguồn: ghi chú Bài 07, §8, Hệ quả 07.16.
- **Lý do / nối:** phát biểu; ý tưởng chứng minh ở trang riêng.
- **Mục tiêu / nguồn:** 4; Hệ quả 07.16.

#### `5-06` Ý tưởng chứng minh: cận theo lề — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  - **Bước 1 ($B$, $\gamma$ chọn trước; giá trị trong $[0,1]$).** Định lý 07.11(b) cho $\mathcal G_\gamma=\{\phi_\gamma(\tilde y\langle w,x\rangle):\lVert w\rVert\le B\}$.
  - **Bước 2 (bổ đề co).** $\phi_i(a)=\phi_\gamma(\tilde y_ia)$ là $(1/\gamma)$-Lipschitz: $\widehat{\mathfrak R}_S(\mathcal G_\gamma)\le\tfrac1\gamma\widehat{\mathfrak R}(\mathcal F_B)$.
  - **Bước 3 (Mệnh đề 07.13).** $2\widehat{\mathfrak R}_S(\mathcal G_\gamma)\le2BC_x/(\gamma\sqrt m)$.
  - **Bước 4 (kẹp).** (iii) cho $L_D(h_{w,0})\le L^\gamma_D(h_w)$ và $L^\gamma_S(h_w)\le L^{<\gamma}_S(h_w)$.
  - **Kỹ thuật.** Thay hàm lỗi 0–1 bằng hàm lỗi bị chặn, Lipschitz nằm trên nó; dùng bổ đề co.
  - Chọn $\gamma$ theo $S$: lớp phụ thuộc $S$, Bước 1 hỏng.
- **Ghi chú diễn giả** (~170 âm tiết): Lộ trình: áp dụng Định lý 07.11 cho lớp hàm lỗi dốc, chuyển độ phức tạp của nó về lớp điểm số bằng bổ đề co, rồi dùng Mệnh đề 07.13. Ở Bước 1, lớp hàm lỗi dốc nhận giá trị trong $[0,1]$, cố định trước khi lấy mẫu vì $B$ và $\gamma$ chọn trước, và thỏa (M) với các $w$ hữu tỉ vì liên tục theo $w$. Ở Bước 2, $\lvert\tilde y_i\rvert=1$ nên $\phi_i$ có cùng hằng số Lipschitz $1/\gamma$; nhãn nằm trong $\phi_i$, đúng chỗ bổ đề co cho phép $\phi_i$ phụ thuộc $i$. Ở Bước 3, các $X_i$ nằm trong giá của $D$, nên $\lVert X_i\rVert\le C_x$. Bước 4 là tính chất kẹp, đổi rủi ro dốc thành rủi ro 0–1 ở vế trái và thành tỉ lệ vi phạm lề ở vế phải. Ý nghĩa cho học: cận đo năng lực bằng tỉ số giữa chuẩn và lề, không bằng số tham số, nên cho bảo đảm cả khi $p$ lớn hơn nhiều so với $m$. Nguồn: ghi chú Bài 07, chứng minh Hệ quả 07.16.
- **Lý do / nối:** trang ý tưởng chứng minh riêng → bài tập về số chiều.
- **Mục tiêu / nguồn:** 4; chứng minh Hệ quả 07.16.

#### `5-07` Bài tập: nhúng vào không gian nhiều chiều hơn — bài tập (Bài tập 07.3(d)) · 2,5 phút
- **Mặt trang:**
  - Nhúng $x_1,\ldots,x_m\in\mathbb R^p$ vào $\mathbb R^{p'}$, $p'>p$, bằng $p'-p$ tọa độ $0$.
  - **Câu hỏi:** chứng minh độ phức tạp của $\mathcal F_B$ trên các điểm mới bằng trên các điểm cũ,
  - và so với chiều VC của $\mathcal H^p_{\mathrm{hom}}$ và $\mathcal H^{p'}_{\mathrm{hom}}$.
  - **Lời giải:** [f] $\hat x_i=(x_i,0)$, $w=(w',w'')$: $\langle w,\hat x_i\rangle=\langle w',x_i\rangle$; $\lVert w\rVert\le B\Rightarrow\lVert w'\rVert\le B$; $(w',0)$ cho chiều ngược lại.
  - [f] Hai tập véc-tơ giá trị trùng nhau, nên hai độ phức tạp bằng nhau.
  - [f] Chiều VC $p$ và $p'$ (Mệnh đề 03.9(b)) tăng theo số chiều.
- **Ghi chú diễn giả:** Mỗi $w'$ với $\lVert w'\rVert\le B$ cho $w=(w',0)$ với cùng chuẩn và cùng giá trị trên các điểm mới; ngược lại, bỏ các tọa độ sau của $w$ không làm tăng chuẩn. Chiều VC của lớp nửa không gian thuần nhất tăng theo số chiều của không gian, còn độ phức tạp của $\mathcal F_B$ trên các điểm cho trước và cận $BC_x/\sqrt m$ không đổi. Thêm tọa độ, tức thêm tham số, không làm lớp bị chặn theo chuẩn khớp nhãn ngẫu nhiên tốt hơn. Nguồn: `exercises.md`, Bài tập 07.3(d); ghi chú Bài 07, Mệnh đề 07.13.
- **Lý do / nối:** bài tập của cụm lớp tuyến tính: số chiều không vào độ phức tạp → áp dụng ở mạch 6.
- **Mục tiêu / nguồn:** 4, 5; Bài tập 07.3(d).

### Mạch 6. Cận theo chuẩn và lề khi tham số hóa thừa (7 trang, 17 phút)

#### `6-00` 6. Cận theo chuẩn và lề khi tham số hóa thừa — tiêu đề mạch, điểm vào mạch 6 · 0,5 phút
- **Mặt trang:** "6."; h2 "Cận theo chuẩn và lề khi tham số hóa thừa"; `p.strand-lead` (bảng mạch, 22 âm tiết); `p.strand-keys`: "phân lớp văn bản · lưới lề · lề chuẩn hóa · tập kiểm tra · mạng sâu".
- **Ghi chú diễn giả:** Hệ quả 07.16 không chứa số chiều, nên cho bảo đảm cả khi số chiều lớn hơn nhiều so với cỡ mẫu, nơi Định lý 03.15 không cho thông tin. Mạch trả lời câu hỏi thực hành về phân lớp văn bản, xử lý trường hợp lề được chọn sau khi xem tập huấn luyện, rồi đo chuẩn và lề trong thí nghiệm mở đầu. Hai trang cuối nêu hai giới hạn: lớp điểm số không thay được lớp hàm lỗi, và cận tuyến tính không chuyển sang mạng sâu. Nguồn: ghi chú Bài 07, §9.
- **Lý do / nối:** mạch 5 → áp dụng.
- **Mục tiêu / nguồn:** 4, 5; §9.

#### `6-01` Ví dụ: phân lớp văn bản với một trăm nghìn đặc trưng — ví dụ (Ví dụ 07.8) · 3 phút
- **Mặt trang:**
  - $p=10^5$, $C_x=1$, $m=10^4$, $\delta=0{,}05$, $BC_x/\gamma=10$; $B$, $\gamma$ chọn trước khi lấy mẫu.
  - Số hạng Rademacher $2BC_x/(\gamma\sqrt m)=2\cdot10/100=0{,}2$; số hạng tin cậy $\le0{,}0408$.
  - Hệ quả 07.16: với xác suất ít nhất $0{,}95$, mọi $\lVert w\rVert\le B$: $L_D(h_{w,0})\le L^{<\gamma}_S(h_w)+0{,}2408$.
  - Định lý 03.15: $d=p>2m$, $\Pi(2m)=2^{2m}$, $\rho_m\ge\sqrt{16\ln2}\approx3{,}33>1$.
  - Cỡ mẫu cho số hạng phạt $\le\epsilon$: $m\ge\big((2BC_x/\gamma+4{,}0743)/\epsilon\big)^2$.
  - Bảng: `BC_x/γ | ε | m`; `10 | 0,1 | 57 958`; `10 | 0,05 | 231 829`; `1 | 0,1 | 3690`.
- **Ghi chú diễn giả:** Câu trả lời cho câu hỏi thực hành: với xác suất ít nhất $0{,}95$, tỉ lệ lỗi của $h_{w,0}$ không quá tỉ lệ văn bản có lề nhỏ hơn $\gamma$ cộng $0{,}2408$, bất kể $10^5$ đặc trưng. Cái giá là vế phải tính tỉ lệ vi phạm lề, không chỉ tỉ lệ lỗi. Cận VC dùng cùng dữ liệu cho bán kính lớn hơn $3{,}33$, nên không cho thông tin. Cỡ mẫu đến từ việc viết số hạng phạt thành $\big(2BC_x/\gamma+3\sqrt{\ln(2/\delta)/2}\big)/\sqrt m$ với $3\sqrt{\ln40/2}\approx4{,}0743$, rồi đảo cận thành cỡ mẫu như kỹ thuật của Bài 02; các giá trị được làm tròn lên. Nguồn: ghi chú Bài 07, §9, Ví dụ 07.8.
- **Lý do / nối:** cận số bắt buộc, so với cận VC trên cùng số liệu → khi lề chọn theo tập huấn luyện.
- **Mục tiêu / nguồn:** 4; Ví dụ 07.8.

#### `6-02` Chọn lề sau khi xem tập huấn luyện — vấn đề, kết quả (Nhận xét 07.17) · 2,5 phút
- **Mặt trang:**
  - Chọn $\gamma$ hay $B$ sau khi xem $S$: vi phạm Hệ quả 07.16.
  - **Nhắc lại:** chia xác suất thất bại theo trọng số (Bài 04).
  - **Nhận xét 07.17.** **Giả thiết:** như Hệ quả 07.16 trừ lề: $\gamma_k=2^{-k}$, $q_k=1/(k(k+1))$ cố định trước; $k$ chọn theo $S$.
  - **Bảo đảm:** với xác suất ít nhất $1-\delta$, đồng thời cho mọi $k$ và mọi $\lVert w\rVert\le B$:
  - $$L_D(h_{w,0})\le L^{<\gamma_k}_S(h_w)+\frac{2BC_x}{\gamma_k\sqrt m}+3\sqrt{\frac{\ln(2/(\delta q_k))}{2m}}.$$
  - Thêm $\ln(k(k+1))$ dưới dấu căn so với Hệ quả 07.16.
- **Ghi chú diễn giả:** Lấy $\gamma$ bằng lề nhỏ nhất trên tập huấn luyện, hay $B=\lVert\hat w\rVert$ sau khi huấn luyện, làm lớp hàm lỗi phụ thuộc mẫu. Cách sửa giống Bổ đề 04.9: áp dụng Hệ quả 07.16 với $\gamma_k$ và xác suất thất bại $\delta q_k$ cho mỗi $k$, rồi dùng bất đẳng thức hợp; các $q_k$ có tổng $1$. Lưới $B_k=2^k$ cho bán kính được xử lý cùng cách. Ví dụ: $\gamma=0{,}5$ ứng với $k=1$, $q_1=\tfrac12$, $\delta q_1=0{,}025$; với $m=2500$, số hạng tin cậy tăng từ $0{,}0815$ lên $3\sqrt{\ln80/5000}\le0{,}0889$. Nguồn: ghi chú Bài 07, §9, Nhận xét 07.17; câu hỏi cuối buổi (b).
- **Lý do / nối:** điều kiện "chọn trước" của mạch 5 → thí nghiệm, nơi bán kính chỉ biết sau huấn luyện.
- **Mục tiêu / nguồn:** 4, 5; Nhận xét 07.17.

#### `6-03` Ví dụ: chuẩn và lề trong thí nghiệm mở đầu — ví dụ (Ví dụ 07.10, Bước 1–2), hình F3 · 3 phút
- **Mặt trang** {{`grid2`: bảng trái, hình F3 phải}}:
  - Lớp của thí nghiệm, $m=200$, mười lần chạy; $\lVert\chi(x)\rVert\le C_x$, $C_x$ từ $1{,}518$ đến $1{,}544$.
  - $\langle\hat w,\chi(x_i)\rangle=\tilde y_i$: mọi lề bằng $1$; $\gamma=1$, $L^{<\gamma}_S=0$.
  - Bảng: `Nhãn | ‖ŵ‖ trung bình | nhỏ nhất – lớn nhất | lề chuẩn hóa`; `Thật | 916 | 351 – 1721 | 3,8·10⁻⁴ – 1,87·10⁻³`; `Hoán vị | 10 853 | 6792 – 14 052 | 4,6·10⁻⁵ – 9,6·10⁻⁵` {{số trong ô viết KaTeX}}.
  - **Diễn giải:** tỉ số chuẩn trung bình $10\,853/916\approx11{,}85$; hai khoảng chuẩn không giao nhau.
  - {{hình F3 `chuan-hai-loai-nhan.svg`; `figcaption` ở mục 8}}
- **Ghi chú diễn giả:** Vì $\lVert x\rVert\le1$ và $\lVert v_j\rVert=1$, tọa độ thứ $j$ của $\chi(x)$ có trị tuyệt đối không quá $(1+\lvert b_{1j}\rvert)/\sqrt N$, nên $C_x^2=\frac1N\sum_j(1+\lvert b_{1j}\rvert)^2$. Nghiệm nội suy cho điểm số đúng bằng $\tilde y_i$, nên mọi lề bằng $\tilde y_i^2=1$. Lề chuẩn hóa là $\gamma/(\lVert\hat w\rVert C_x)$. Chuẩn của ma trận lớp ra $\Theta_2=\hat w^\top/\sqrt N$ trung bình $20{,}5$ và $242{,}7$, cùng tỉ số. Hạng của ma trận đặc trưng bằng $200$ trong mọi lần chạy. Các số là số đo của thí nghiệm, giao thức ở Phụ lục D. Nguồn: ghi chú Bài 07, §9, Ví dụ 07.10, Bước 1–2; Phụ lục D.
- **Lý do / nối:** đại lượng phân biệt hai loại nhãn → cận và tập kiểm tra.
- **Mục tiêu / nguồn:** 5; Ví dụ 07.10.

#### `6-04` Ví dụ: cận theo chuẩn và tập kiểm tra trong thí nghiệm — ví dụ (Ví dụ 07.10, Bước 3–4) · 3 phút
- **Mặt trang:**
  - Số hạng $2\lVert\hat w\rVert C_x/(\gamma\sqrt{200})$: $75$–$372$ (nhãn thật), $1467$–$3047$ (nhãn hoán vị, (T1) không thỏa).
  - Cận hợp lệ cần lưới $B_k=2^k\ge\lVert\hat w\rVert$ (Nhận xét 07.17): số hạng còn lớn hơn.
  - Tập kiểm tra $5000$ điểm, độc lập với hàm đã chọn: lỗi $0{,}023$; Hệ quả 02.10(b) cho bán kính $0{,}0193$, mức $0{,}95$.
  - **Diễn giải:** cận theo chuẩn lớn hơn $1$; tập kiểm tra cho bảo đảm dùng được.
- **Ghi chú diễn giả:** Với nhãn thật, hàm đã chọn chỉ phụ thuộc tập huấn luyện và lớp ẩn, độc lập với $5000$ điểm kiểm tra, nên Hệ quả 02.10(b) cho khoảng tin cậy mức $0{,}95$ với bán kính $\sqrt{\ln40/10^4}\le0{,}0193$. Với nhãn hoán vị, Hệ quả 07.16 không áp dụng vì (T1) không thỏa. Một cận lớn hơn một không cho biết mô hình tốt hay kém: ở đây mô hình có lỗi kiểm tra $0{,}023$. Trong thí nghiệm, chuẩn và lề chuẩn hóa phân biệt hai loại nhãn, còn số tham số và độ phức tạp Rademacher của lớp kiến trúc thì không. Nguồn: ghi chú Bài 07, §9, Ví dụ 07.10, Bước 3–4; §10.
- **Lý do / nối:** trả lời câu hỏi mở đầu bằng số → giới hạn: lớp điểm số.
- **Mục tiêu / nguồn:** 5; Ví dụ 07.10.

#### `6-05` Ví dụ: lớp điểm số thay cho lớp hàm lỗi — phản ví dụ bỏ giả thiết (Ví dụ 07.11) · 2,5 phút
- **Mặt trang:**
  - $\mathcal F_B$ trên $\mathbb R^p$, $\lVert x\rVert\le1$, $m=10^4$, $B=10^{-6}$: $\widehat{\mathfrak R}_S(\mathcal F_B)\le10^{-8}$.
  - $h_{w,0}$ không đổi khi nhân $w$ với $c>0$: $\{h_{w,0}:\lVert w\rVert\le10^{-6}\}=\mathcal H^p_{\mathrm{hom}}$, chiều VC $p$.
  - $\{\tfrac12+\langle w,x\rangle\}$ trong $[0,1]$, độ phức tạp $\le10^{-8}$ (Bổ đề 07.8): Định lý 07.11 chỉ chặn trung bình điểm số.
  - Hàm lỗi dốc nối hai lớp với giá $1/\gamma$; thu nhỏ $B$ buộc thu nhỏ $\gamma$ cùng tỉ lệ.
  - Hàm lỗi logistic, $\lVert w\rVert\le B$: trong $[0,K]$, $K=\ln(1+e^{BC_x})$; chia cho $K$ rồi dùng bổ đề co.
- **Ghi chú diễn giả** (~200 âm tiết): Giả thiết "lớp hàm lỗi trong $[0,1]$" của Định lý 07.11 bị thay bằng một lớp điểm số. Hàm lỗi 0–1 không phải hàm Lipschitz của điểm số, nên bổ đề co không nối hai lớp; lớp điểm số rất nhỏ nhưng lớp hàm phân lớp không nhỏ đi. Hàm lỗi bản lề và hàm lỗi logistic không bị chặn khi $w$ chạy trên $\mathbb R^p$; với $B$ chọn trước, hàm lỗi logistic là $1$-Lipschitz theo điểm số, và với xác suất ít nhất $1-\delta$, đồng thời cho mọi $\lVert w\rVert\le B$, rủi ro logistic thỏa $L_D(w)\le L_S(w)+2BC_x/\sqrt m+3K\sqrt{\ln(2/\delta)/(2m)}$. Cùng cách chia cho cận hàm lỗi áp dụng cho hồi quy bình phương trên $[-1,1]$ (Ví dụ 07.9): hàm lỗi chia cho $4$ là $1$-Lipschitz, và Nhận xét 07.12 cho độ lệch đều không quá $8/\sqrt m+12\sqrt{\ln(4/\delta)/(2m)}$, tức $0{,}2577$ khi $m=10^4$. Lớp đó không ổn định đều với hệ số giảm theo $m$ (Ví dụ 06.7) nhưng vẫn hội tụ đều. Nguồn: ghi chú Bài 07, §9, Ví dụ 07.11, Ví dụ 07.9.
- **Lý do / nối:** phản ví dụ bỏ giả thiết "lớp hàm lỗi bị chặn" → giới hạn thứ hai: mạng sâu.
- **Mục tiêu / nguồn:** 3, 5; Ví dụ 07.11.

#### `6-06` Cận theo chuẩn phổ cho mạng sâu — kết quả đọc thêm (Nhận xét 07.18) · 2,5 phút
- **Mặt trang:**
  - **Nhận xét 07.18** (Bartlett, Foster, Telgarsky 2017). Không hệ số tự do; $\varsigma_j$ là $G_j$-Lipschitz, $\varsigma_j(0)=0$.
  - Nhãn dự đoán $\hat y_\Theta$; lề nhiều lớp (multiclass margin) $\mu_\Theta$; độ phức tạp phổ (spectral complexity) $R_\Theta=\big(\prod_jG_j\lVert\Theta_j\rVert_{\mathrm{op}}\big)\big(\sum_jr_j^{2/3}\big)^{3/2}$.
  - Với xác suất ít nhất $1-\delta$, đồng thời cho mọi $\gamma>0$ và $\Theta$, khi $\lVert x_i\rVert\le C_x$:
  - $$\Pr_{(x,y)\sim D}[\hat y_\Theta(x)\ne y]\le\tfrac1m\textstyle\sum_i\mathbb 1[\mu_\Theta(x_i,y_i)\le\gamma]+\tilde O\Big(\frac{C_xR_\Theta}{\gamma\sqrt m}+\sqrt{\frac{\ln(1/\delta)}m}\Big).$$
  - $\tilde O$ ẩn thừa số lôgarit; $R_\Theta$ đóng vai $B$; cận không chứa số tham số.
  - Chứng minh nằm ngoài phạm vi học phần.
- **Ghi chú diễn giả:** Nhận xét này là phần đọc thêm, cho trường hợp mọi lớp nơ-ron được huấn luyện. Mạng là $f_\Theta(x)=\varsigma_J(\Theta_J\varsigma_{J-1}(\cdots\varsigma_1(\Theta_1x)\cdots))$; ReLU có $G_j=1$. Đầu ra có một tọa độ cho mỗi nhãn; lề nhiều lớp là tọa độ của nhãn đúng trừ tọa độ lớn nhất còn lại. $r_j$ là chuẩn nhóm của $\Theta_j-M_j$ chia chuẩn phổ của $\Theta_j$, với ma trận tham chiếu $M_j$ cố định trước; $\lVert X\rVert_2=(\sum_i\lVert x_i\rVert^2)^{1/2}$; $\bar N$ là số lớn nhất trong $p$, số nhãn và các độ rộng. Dạng của ghi chú là $\tilde O(\varepsilon_\Theta)$ với $\varepsilon_\Theta=\lVert X\rVert_2R_\Theta\ln\bar N/(\gamma m)+\sqrt{\ln(1/\delta)/m}$; khi $\lVert x_i\rVert\le C_x$, $\lVert X\rVert_2/m\le C_x/\sqrt m$, và $\tilde O$ ẩn thêm thừa số $\ln\bar N$, cho dạng trên mặt trang. Với $M_j=0$, $R_\Theta$ không đổi khi đổi tỉ lệ hai lớp nơ-ron kề nhau, như tích các chuẩn phổ ở ví dụ đổi tỉ lệ. Hệ quả 07.16 không thay được $R_\Theta$. Nguồn: ghi chú Bài 07, §9, Nhận xét 07.18; Bartlett, Foster, Telgarsky (2017), Định lý 1.1.
- **Lý do / nối:** phân biệt kết quả chứng minh với kết quả đọc thêm; giới hạn cuối của bài → tiêu đề mạch 7.
- **Mục tiêu / nguồn:** 5; Nhận xét 07.18.

### Mạch 7. Tổng kết (8 trang, 16 phút)

#### `7-00` 7. Tổng kết — tiêu đề mạch, điểm vào mạch 7 · 0,5 phút
- **Mặt trang:** "7."; h2 "Tổng kết"; `p.strand-lead` (bảng mạch, 21 âm tiết); không có `p.strand-keys`.
- **Ghi chú diễn giả:** Mạch tổng kết năm kết quả chính cùng giả thiết không được bỏ của từng kết quả, trả lời câu hỏi trung tâm cho cả bài, rồi giải một bài tập tổng hợp về số tham số và bảo đảm. Câu hỏi tự kiểm tra và bảng bài tập về nhà dẫn về ghi chú và tệp bài tập. Nguồn: ghi chú Bài 07, §10–§13.
- **Lý do / nối:** mạch 6 → bảng tổng kết.
- **Mục tiêu / nguồn:** tất cả; §10–§13.

#### `7-01` Bảng tổng kết — tổng kết · 3 phút
- **Mặt trang:**
  {{bảng năm hàng; công thức trong ô viết KaTeX; đặt trong `.table-scroll`}}
  | Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh |
  |---|---|---|
  | Mệnh đề 07.2: $h_\theta=x_1\oplus x_2$ trên $\{0,1\}^2$ | hai nơ-ron ẩn, ReLU | $f_\theta$ chỉ phụ thuộc $s$ (đầy đủ) |
  | Mệnh đề 07.9: $\widehat{\mathfrak R}=\tfrac12-\mathbb E_\tau\min\operatorname{err}_\tau\le\tfrac12$ | hàm vào $\{0,1\}$ | $\sigma_i=2\tau_i-1$ (đầy đủ) |
  | Định lý 07.11: với xác suất ít nhất $1-\delta$, mọi $g$: $L_D\le L_S+2\widehat{\mathfrak R}_S+3\sqrt{\ln(2/\delta)/(2m)}$ | (T1), (T3), (T5), (M) | mẫu bóng, McDiarmid hai lần (phác thảo) |
  | Mệnh đề 07.13: $\widehat{\mathfrak R}(\mathcal F_B)\le BC_x/\sqrt m$ | quả cầu Euclid, $\lVert x_i\rVert\le C_x$ | Cauchy–Schwarz, Jensen (đầy đủ) |
  | Hệ quả 07.16: với xác suất ít nhất $1-\delta$, mọi $\lVert w\rVert\le B$: $L_D(h_{w,0})\le L^{<\gamma}_S+\frac{2BC_x}{\gamma\sqrt m}+3\sqrt{\ln(2/\delta)/(2m)}$ | (T1), $\lVert x\rVert\le C_x$, $B$, $\gamma$ chọn trước | hàm lỗi dốc, bổ đề co (phác thảo) |
  - Đọc thêm: Nhận xét 07.6, 07.18.
- **Ghi chú diễn giả:** Cột cuối ghi độ sâu chứng minh trong ghi chú: đầy đủ hay phác thảo; bất đẳng thức McDiarmid và bổ đề co có chứng minh ở Phụ lục A, B. Mỗi giả thiết của Định lý 07.11 có một phản ví dụ trong bài: bỏ (T1) với nhãn hoán vị; bỏ hàm lỗi trong $[0,1]$ với lớp điểm số; bỏ lớp chọn trước khi lấy bán kính hay lề sau khi xem tập huấn luyện, sửa bằng lưới của Nhận xét 07.17. Không kết quả nào dùng tính lồi; các cận lồi của Bài 05–06 không áp dụng cho hàm mục tiêu không lồi của mạng. Nhận xét 07.6 và 07.18 là đọc thêm, không chứng minh trong học phần. Nguồn: ghi chú Bài 07, §4–§10.
- **Lý do / nối:** bảng một hàng mỗi kết quả chính → câu trả lời cho cả bài.
- **Mục tiêu / nguồn:** tất cả; §4–§10.

#### `7-02` Vấn đề trung tâm — trả lời cho cả bài (§10) · 3 phút
- **Mặt trang:**
  - $P$, chiều VC và độ phức tạp của lớp kiến trúc như nhau với hai loại nhãn.
  - Với (T1), (T3), (T5), (M), với xác suất ít nhất $1-\delta$: $\widehat{\mathfrak R}_S$ chặn khoảng cách tổng quát hóa của mọi hàm.
  - Chuẩn bị chặn, $B$, $\gamma$ chọn trước: số hạng $2BC_x/(\gamma\sqrt m)$ không phụ thuộc $p$.
  - Thí nghiệm: chuẩn gấp $11{,}85$ lần nhưng cận lớn hơn $1$; báo lỗi trên tập kiểm tra.
- **Ghi chú diễn giả:** Đại lượng đo được năng lực thống kê khi số tham số vượt cỡ mẫu là độ phức tạp Rademacher của một lớp chứa hàm do huấn luyện chọn, không phải số tham số; với lớp kiến trúc, đại lượng này bằng một nửa với cả hai loại nhãn. Với $10^5$ đặc trưng, số hạng phạt của Hệ quả 07.16 là $0{,}2408$. Cùng một hàm có tổng bình phương tham số $10{,}25$ hay $500{,}30$, nên chỉ đại lượng bất biến khi đổi tỉ lệ, như lề chuẩn hóa, mới so sánh được các mô hình. Các cận không dùng tính lồi, nên đúng cho mạng huấn luyện bằng hạ gradient ngẫu nhiên trên hàm mục tiêu không lồi, miễn đầu ra thuộc lớp chọn trước. Chúng không giải thích vì sao phép huấn luyện chọn nghiệm chuẩn nhỏ với nhãn thật. Nguồn: ghi chú Bài 07, §10.
- **Lý do / nối:** trả lời câu hỏi của 1-05 → bài tập tổng hợp.
- **Mục tiêu / nguồn:** tất cả; §10.

#### `7-03` Bài tập: số tham số và bảo đảm — bài tập tổng hợp, đề (Bài tập 07.4(b), (c)) · 2,5 phút
- **Mặt trang:**
  - **(b)** Lớp của Nhận xét 03.10(iii) với $p=10^6$ tham số; $S\sim D^m$ theo (T1), $m=200$, $\delta=0{,}05$, hàm lỗi 0–1.
  - Kiểm giả thiết của Định lý 02.14, tính $r_m$ của phần (a). Có tham số hóa thừa so với $m=200$ không?
  - **(c)** $\mathcal H_{\sin}$ có $P=1$; với $200$ đầu vào $2^{-1},\ldots,2^{-200}$, tính $\mathbb E_\tau\min_{h}\operatorname{err}_\tau(h)$
  - và vế phải của Định lý 07.11(b) với $\delta=0{,}05$ cho một nghiệm ERM, với nhãn bất kì.
- **Ghi chú diễn giả** (~150 âm tiết): Bài ghép bốn mạch: định nghĩa tham số hóa thừa (mạch 2), bán kính của Định lý 02.14 cho lớp hữu hạn, Mệnh đề 07.9 và Ví dụ 07.5 (mạch 3), số hạng tin cậy của Ví dụ 07.6 (mạch 4). Hai phần xét hai lớp ở hai đầu: rất nhiều tham số nhưng ba hàm, và một tham số nhưng khớp mọi cách gán nhãn. Định lý 02.14 cần quan sát độc lập cùng phân bố, hàm lỗi đo được trong $[0,1]$ và một lớp hữu hạn chọn trước, giả thiết (T4) của Bài 02. Phần (a) của bài tập, so sáu đại lượng của hai lượt huấn luyện, đã có trên trang trả lời vấn đề trung tâm và ở các ví dụ về thí nghiệm. Nguồn: `exercises.md`, Bài tập 07.4.
- **Lý do / nối:** bài tập tổng hợp, chọn vì trả lời trực tiếp câu hỏi trung tâm bằng hai lớp cực biên (mục 11, điểm 6) → lời giải.
- **Mục tiêu / nguồn:** 3, 5; Bài tập 07.4(b), (c).

#### `7-04` Bài tập: số tham số và bảo đảm, lời giải — bài tập tổng hợp, lời giải · 3 phút
- **Mặt trang:**
  - **Lời giải:** **(b)** [f] Ba hàm $\mathbb 1[x\ge0]$, $\mathbb 1[x\le0]$, hằng $1$: (T4) lớp hữu hạn chọn trước, $K=3$; $r_m=\sqrt{\ln(2K/\delta)/(2m)}=\sqrt{\ln120/400}\le0{,}1095$.
  - [f] $P/m=5000$: tham số hóa thừa; với xác suất ít nhất $0{,}95$, mọi hàm có $\lvert L_S-L_D\rvert\le0{,}1095$.
  - **(c)** [f] Lớp tách trọn vẹn bộ điểm: $\mathbb E_\tau\min\operatorname{err}_\tau=0$, độ phức tạp $\tfrac12$ (Mệnh đề 07.9).
  - [f] ERM có $L_S=0$: vế phải $0+2\cdot\tfrac12+0{,}2881=1{,}2881>1$, dù $P/m=0{,}005$.
  - **Kết luận:** [f] $P/m$ lớn không ngăn một bảo đảm, $P/m$ nhỏ không đủ cho một bảo đảm.
- **Ghi chú diễn giả** (~150 âm tiết): Ở (b), lớp chỉ gồm ba hàm theo dấu của $w_1+\cdots+w_p$, cố định trước mẫu, nên thỏa (T4) với số hàm $K=3$; hàm lỗi 0–1 thỏa (T2), (T3); $\ln120\approx4{,}7875$. Cận một phía của Định lý 02.14(b) là $\sqrt{\ln60/400}\le0{,}1012$, nhỏ hơn vì không chia $\delta$ cho hai phía. Ở (c), Mệnh đề 07.9(a) cho độ phức tạp $\tfrac12-0$ trên các điểm, và theo (b) của mệnh đề, lớp hàm lỗi 0–1 có cùng giá trị với mọi nhãn; vế phải lớn hơn $1$ với mọi nhãn, kể cả nhãn hoàn toàn ngẫu nhiên. Đại lượng cần đo là năng lực của lớp chứa hàm được chọn. Nguồn: `exercises.md`, Lời giải Bài tập 07.4(b), (c).
- **Lý do / nối:** lời giải trên mặt trang, mỗi bước một dòng → tự kiểm tra.
- **Mục tiêu / nguồn:** 3, 5; Bài tập 07.4(b), (c).

#### `7-05` Câu hỏi tự kiểm tra — tổng kết · 2,5 phút
- **Mặt trang:** `ol`:
  1. Vì sao độ phức tạp của lớp hàm lỗi 0–1 không phân biệt nhãn thật với nhãn hoán vị?
  2. Hằng số $3$ trong Định lý 07.11(b) đến từ đâu?
  3. $m=2500$, $\lVert x\rVert\le1$, $B=2$, $\gamma=0{,}5$, $\delta=0{,}05$, $L^{<\gamma}_S(h_w)=0{,}04$: tính cận của Hệ quả 07.16.
  4. Mệnh đề 07.13 cho $\widehat{\mathfrak R}_S(\mathcal F_2)\le0{,}04$; vì sao không đặt $2\cdot0{,}04$ vào Định lý 07.11 để chặn rủi ro 0–1?
- **Ghi chú diễn giả** (câu trả lời dự kiến, chỉ dùng ghi chú): (1) Mệnh đề 07.9(b): với mọi nhãn cố định, độ phức tạp của lớp hàm lỗi 0–1 bằng độ phức tạp của lớp trên các đầu vào, vì $\sigma_i(1-2y_i)$ lại là biến Rademacher. (2) Hai lần bất đẳng thức McDiarmid một phía, mỗi lần với xác suất thất bại $\delta/2$: một lần cho $\Psi$, một lần để thay độ phức tạp tổng thể bằng độ phức tạp thực nghiệm. (3) $2\cdot2\cdot1/(0{,}5\cdot50)=0{,}16$; $3\sqrt{\ln40/5000}\approx0{,}0815$; cận $0{,}2815$; nếu $\gamma=0{,}5$ chọn sau khi xem lề, lưới cho $0{,}2889$. (4) Định lý 07.11 cần lớp hàm lỗi trong $[0,1]$; hàm lỗi 0–1 không là hàm Lipschitz của điểm số, và lớp hàm phân lớp không đổi khi thu nhỏ $w$; hàm lỗi dốc nối hai lớp với giá $1/\gamma$: $2\cdot0{,}04/0{,}5=0{,}16$. Nguồn: ghi chú Bài 07, Mệnh đề 07.9, Định lý 07.11, Ví dụ 07.11, §12.
- **Lý do / nối:** kiểm bốn ý chính, câu 3 và 4 là câu hỏi cuối buổi của ghi chú → bài tập về nhà.
- **Mục tiêu / nguồn:** 2, 3, 4; §12.

#### `7-06` Bài tập về nhà — tổng kết · 1 phút
- **Mặt trang:**
  - Bảng `Mục | Bài tập`: `Năng lực biểu diễn và số tham số | 07.1, 07.5, 07.7, 07.8, 07.9`; `Cận tổng quát hóa theo độ phức tạp Rademacher | 07.2`; `Cận theo chuẩn và lề khi tham số hóa thừa | 07.3, 07.4, 07.6`.
  - Liên kết "Ghi chú bài giảng · Bài tập" (viewer với `&deck=`).
- **Ghi chú diễn giả:** Sáu bài đầu là bài gốc, ba bài sau chọn từ UML §20.9; Bài tập 07.9 là bài tùy chọn với phát biểu đã sửa (ReLU, một biến). Mỗi bài xếp vào mạch cung cấp kiến thức cuối cùng bài đó cần: Bài tập 07.2(b) đọc lại chứng minh Định lý 07.11; Bài tập 07.3(e) dùng cận cho hàm lỗi logistic của Ví dụ 07.11; Bài tập 07.4(a), (d) dùng Ví dụ 07.10, 07.11 và Nhận xét 07.17; Bài tập 07.6 dùng số hạng Rademacher của thí nghiệm và lưới của Nhận xét 07.17. Bài tập 07.7, 07.8 chặn hàm tăng trưởng của lớp mạng ngưỡng, gần Nhận xét 07.6. Bài tập 07.6(c) là thí nghiệm tùy chọn chỉ dùng NumPy. Nguồn: ghi chú Bài 07, §11; `exercises.md`.
- **Lý do / nối:** dẫn tới tệp bài tập → tài liệu.
- **Mục tiêu / nguồn:** tất cả; §11.

#### `7-07` Tài liệu tham khảo — tổng kết · 0,5 phút
- **Mặt trang:**
  - Shalev-Shwartz và Ben-David (2014), *Understanding Machine Learning: From Theory to Algorithms* (UML).
  - UML §20.1–20.3, §26.1 (trước buổi học); §26.2, §20.4–20.5 (sau buổi học).
  - Mở rộng: UML §26.3, §28.1, §15.2.3, Bài tập 20.5; Bartlett, Foster, Telgarsky (2017), *Spectrally-normalized margin bounds for neural networks*.
  - Bài 08: Tính ổn định của SGD và tổng quát hóa trong học sâu. {{liên kết tới deck Bài 08 khi có; trước đó chữ thường}}
- **Ghi chú diễn giả:** Khác UML: cận Rademacher của học phần dùng hàm lỗi trong $[0,1]$ và hai lần bất đẳng thức McDiarmid một phía, được số hạng $3\sqrt{\ln(2/\delta)/(2m)}$, so với $4c\sqrt{2\ln(4/\delta)/m}$ của UML §26.1; với $c=1$, $m=10^4$, $\delta=0{,}05$, hai số hạng là $0{,}1185$ và $0{,}0408$. Học phần giữ $B$, $\gamma$ riêng và dùng độ phức tạp thực nghiệm; mạng viết ở dạng ma trận với ReLU, $J$ và $\varsigma$. Cầu nối: Hệ quả 07.16 đúng cho mọi $w$ trong quả cầu, nên không giải thích vì sao cùng một quy tắc huấn luyện chọn nghiệm có chuẩn trung bình $916$ với nhãn thật và $10\,853$ với nhãn hoán vị. Nghiệm nội suy chuẩn nhỏ nhất cũng là giới hạn của hạ gradient khởi tạo tại $0$ (Phụ lục D), nên chuẩn của nó do quỹ đạo tối ưu quyết định. Bài 08 hỏi: với hàm lỗi lồi, trơn và Lipschitz, quỹ đạo của hạ gradient ngẫu nhiên có cho một bảo đảm cho chính hàm nó trả về không? Nguồn: ghi chú Bài 07, §12 (đoạn cuối), §13.
- **Lý do / nối:** trang cuối; câu nối sang Bài 08 một dòng trên mặt trang.
- **Mục tiêu / nguồn:** —; §12, §13.

## 7. Hành trình khái niệm

Thứ tự bước theo quy định: vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh (trang riêng) → kỹ thuật hoặc kiểm tra. Các bước có thể chung trang nhưng không đảo thứ tự trên mặt trang. Theo cổng duyệt Bài 04 (T5), ví dụ đặt trước phát biểu khi số liệu của nó không cần chính kết quả đó; ví dụ của ghi chú dùng kết quả để kiểm tra thì đứng sau, ở cột cuối.

| Kết quả hoặc khái niệm | Vấn đề | Trực quan | Ví dụ | Phát biểu | Ý tưởng chứng minh | Kỹ thuật / kiểm tra | Gộp, `không áp dụng`, lý do |
|---|---|---|---|---|---|---|---|
| Định nghĩa 07.1 | 2-02 (lớp afin sai ít nhất một quan sát) | 2-03 dòng mở ("ghép nhiều hàm afin, xen giữa bởi hàm phi tuyến") | 2-03 dòng "Ví dụ:" ($J=1$; $9$ tham số; $\mathbb 1[x\in\mathbb Q]$) | 2-03 | `không áp dụng` (định nghĩa) | 2-04 | Ví dụ ngắn chung trang với định nghĩa, sau phát biểu, như ghi chú (ba ví dụ dùng chính kí hiệu của định nghĩa). |
| Mệnh đề 07.2 | 2-02 (Ví dụ 07.1) | 2-04 ("Trực quan.": hai nơ-ron cùng đọc $s$) | 2-02 (bốn quan sát) | 2-04 | 2-05 | 2-05 hình F1, $(\tfrac12,\tfrac12)$; 2-06 (sai số xấp xỉ $0$ so với $\tfrac14$); 2-07 (Bài tập 07.5(c)) | Trực quan và phát biểu chung trang. |
| Nhận xét 07.3, ba năng lực | 1-06, 2-05 (mạng gán nhãn ngoài tập huấn luyện) | 2-06 (bảng ba năng lực ↔ ba số hạng) | 2-06 cột "Ví dụ 07.1" | 2-06 | `không áp dụng` (nhận xét, dẫn UML) | 2-07 (hàm mục tiêu không lồi) | — |
| Định nghĩa 07.4 | 2-08 dòng "Nhắc lại:" (Nhận xét 03.10: hai phản ví dụ) | ghi chú diễn giả 2-08 (lỗi huấn luyện $0$ không mang thông tin) | 2-08 dòng đầu (hai lớp của Nhận xét 03.10) | 2-08 | `không áp dụng` (định nghĩa) | 2-11 ($P/m=10$) | Hai phản ví dụ của Bài 03 đứng trước định nghĩa vì không cần định nghĩa để đọc. |
| Định nghĩa 07.5 | 2-08 dòng cuối | ghi chú diễn giả 2-09 | 2-10, 2-11 | 2-09 | `không áp dụng` (định nghĩa) | 2-10 (chuẩn không là đại lượng của hàm); 2-11 | Ví dụ sau định nghĩa vì dùng ba đối tượng của nó; trang 2-09 mở bằng định nghĩa ngay sau câu kết của 2-08 (mục 11, điểm 12). |
| Định nghĩa 07.7 | 2-11 (cận VC không cho thông tin; cần đại lượng cho hàm giá trị thực), 3-00 | 3-01 ("Trực quan.": chọn hàm sau khi thấy dấu) | 3-02 (Ví dụ 07.4) | 3-01 | `không áp dụng` (định nghĩa) | 3-02 ($0$; $\tfrac14$; $\tfrac13$; $\tfrac12$) | Ví dụ 07.4 dùng công thức của định nghĩa nên đứng sau; trang mở bằng "Nhắc lại:" và "Trực quan.", không mở bằng định nghĩa. |
| Mệnh đề 07.9 | 3-02 (dãy tăng tới $\tfrac12$) | 3-03 ("Trực quan.": hàm cố định sai nửa số nhãn) | 3-02 (Ví dụ 07.4) | 3-03 | 3-04 | 3-05 (Ví dụ 07.5); 3-06 (Bài tập 07.2(c)) | Trực quan và phát biểu chung trang. |
| Bổ đề 07.10 | 4-01 dòng 2 ($\Psi$ không là trung bình) | 4-01 ("Trực quan.": không biến nào đổi $Q$ quá $c_i$) | 4-01 (trung bình trong $[a,b]$ cho Định lý 02.7) | 4-01 | `không áp dụng`: công cụ, phác thảo; lộ trình Phụ lục A ở ghi chú diễn giả 4-01 (mục 11, điểm 3) | 4-03 Bước 4 | Bốn bước chung trang. |
| Định lý 07.11 | 3-05 (độ phức tạp $\tfrac12$ với hai loại nhãn), 4-00, 4-01 | 4-02 ("Trực quan.": hai cực biên $\tfrac12$ và $0$) | 3-05 (lớp kiến trúc) | 4-02 | 4-03 | 4-04 (Ví dụ 07.6: $1{,}2881$; nhãn hoán vị vi phạm (T1)); 4-05 (Bài tập 07.2(b)) | Nhắc lại đối xứng hóa và mẫu bóng trên 4-03. |
| Mệnh đề 07.13 | 4-04 (cần lớp nhỏ hơn), 5-00, 5-01 dòng 1 | 5-01 ("Trực quan.": $\mathbb E\lVert v_\sigma\rVert^2$ không phụ thuộc $p$) | 3-02 (lớp trên ba điểm; ghi chú diễn giả 5-01 đọc đơn vị) | 5-01 | 5-02 | 5-02 (Ví dụ 07.7: đẳng thức và độ lỏng $\sqrt2$); 5-07 (Bài tập 07.3(d)) | Ví dụ 07.7 dùng $v_\sigma$ của chứng minh nên chung trang ý tưởng chứng minh, sau các bước. |
| Bổ đề 07.14 | 5-03 dòng 1 | ghi chú diễn giả 5-03 | 5-03 dòng "Lưu ý:" ($A=\{0\}$, $0$ so với $0{,}5$) | 5-03 | `không áp dụng`: công cụ, phác thảo; lộ trình Phụ lục B ở ghi chú diễn giả 5-03 | 5-06 Bước 2 | Phản ví dụ quy ước định tâm đứng sau phát biểu vì nó kiểm điều kiện của chính bổ đề. |
| Định nghĩa 07.15 | 5-04 dòng 1 (0–1 không Lipschitz) | hình F2 | ghi chú diễn giả 5-04 (lề $\tfrac12$ của mạng phép hoặc loại trừ) | 5-04 | `không áp dụng` (định nghĩa) | 5-04 (i)–(iii) | — |
| Hệ quả 07.16 | 2-02 (câu hỏi phân lớp văn bản), 5-04 | 5-05 ("Trực quan.": bất biến khi nhân $(w,\gamma,B)$ với $c$) | 2-02 (dữ liệu văn bản) | 5-05 | 5-06 | 6-01 (Ví dụ 07.8: $0{,}2408$; so cận VC $3{,}33$); 6-02 (bỏ "chọn trước": lưới); 6-04; 7-05 câu 3 | Trực quan và phát biểu chung trang. |
| Nhận xét 07.17 | 5-06 dòng cuối, 6-02 dòng 1 | ghi chú diễn giả 6-02 | ghi chú diễn giả 6-02 ($\gamma=0{,}5$: $0{,}0815\to0{,}0889$) | 6-02 | ghi chú diễn giả 6-02 (Hệ quả 07.16 với $\delta q_k$, bất đẳng thức hợp) | 6-04 dòng 2 | Nhắc lại kỹ thuật của Bài 04. |
| Nhận xét 07.18 (đọc thêm) | 6-05 (lớp điểm số), ghi chú diễn giả 6-06 | ghi chú diễn giả 6-06 (bất biến khi đổi tỉ lệ) | 2-10 (Ví dụ 07.2) | 6-06 | `không áp dụng`: đọc thêm, chứng minh ngoài học phần | 7-01 dòng "Đọc thêm" | — |

Thời lượng theo mạch: 9 + 27 + 15 + 16 + 20 + 17 + 16 = 120 phút; 54 trang.

## 8. Hình vẽ

Mọi hình là SVG trong `2627-1/img/lec-07/`, `role="img"`, có `<title>` và alt cụ thể; màu không là tín hiệu duy nhất (kiểu nét và hình dạng điểm khác nhau); chữ trong hình chỉ là nhãn trục, nhãn điểm, số và nhãn ngắn (Unicode), không công thức; công thức và chú thích nằm ở `figcaption` (KaTeX). Chú thích nêu dữ liệu. Mọi số trên hình có trong chữ của cùng trang. Trục chứa hết dữ liệu.

| Mã | Tệp | Trang | Nội dung và dữ liệu | Alt dự kiến |
|---|---|---|---|---|
| F1 (bỏ, mục 16) | `vung-hoac-loai-tru.svg` (khoảng 360×360) | 2-05 | Mặt phẳng $[-0{,}25;1{,}5]^2$, trục $x_1$, $x_2$ (vạch $0$; $0{,}5$; $1$). Dải đóng $\tfrac12\le x_1+x_2\le\tfrac32$ tô nền nhạt có gạch chéo, giới hạn bởi hai đường liền $x_1+x_2=\tfrac12$ (qua $(0{,}5;0)$, $(0;0{,}5)$) và $x_1+x_2=\tfrac32$ (qua $(1{,}5;0)$, $(0;1{,}5)$; đoạn vẽ được cắt ở khung); nhãn ngắn trong dải "f ≥ 0". Bốn điểm: $(1,0)$, $(0,1)$ tròn đặc, nhãn "1"; $(0,0)$, $(1,1)$ vuông rỗng, nhãn "0"; điểm $(\tfrac12,\tfrac12)$ là dấu chữ thập, nhãn "(½, ½)". `figcaption`: "Miền $f_\theta\ge0$ của mạng ở Mệnh đề 07.2: dải $\tfrac12\le x_1+x_2\le\tfrac32$; $(1,0)$, $(0,1)$ nằm trong dải, $(0,0)$, $(1,1)$ nằm ngoài; $(\tfrac12,\tfrac12)$ nằm trong dải." | "Mặt phẳng với bốn đỉnh của hình vuông đơn vị. Một dải chéo giữa hai đường thẳng song song x một cộng x hai bằng một phần hai và bằng ba phần hai chứa hai điểm nhãn 1 là (1, 0) và (0, 1), cùng điểm (½, ½). Hai điểm nhãn 0 là (0, 0) và (1, 1) nằm ngoài dải, mỗi điểm ở một phía." |
| F2 | `ham-loi-doc.svg` (khoảng 420×260) | 5-04 | Trục ngang $t$ từ $-\gamma$ đến $2\gamma$ (vạch "−γ", "0", "γ", "2γ"); trục dọc $[0;1{,}25]$ (vạch $0$, $1$). Ba đường: $\mathbb 1[t\le0]$ nét đứt (bằng $1$ trên $[-\gamma,0]$, chấm đặc tại $(0,1)$, chấm rỗng tại $(0,0)$, bằng $0$ trên $(0,2\gamma]$); $\phi_\gamma$ nét liền đậm (bằng $1$ trên $[-\gamma,0]$, đoạn thẳng từ $(0,1)$ xuống $(\gamma,0)$, bằng $0$ sau đó); $\mathbb 1[t<\gamma]$ nét chấm (bằng $1$ trên $[-\gamma,\gamma)$, chấm rỗng tại $(\gamma,1)$, chấm đặc tại $(\gamma,0)$). Các đoạn trùng nhau vẽ lệch $2$ px để thấy cả ba kiểu nét. Nhãn trực tiếp: "0–1", "dốc", "cận trên". `figcaption`: "$\mathbb 1[t\le0]\le\phi_\gamma(t)\le\mathbb 1[t<\gamma]$ trên $[-\gamma,2\gamma]$; $\phi_\gamma$ có độ dốc $-1/\gamma$ trên $[0,\gamma]$." | "Ba hàm bậc thang và hàm dốc theo lề t từ âm gamma đến hai gamma. Hàm lỗi 0–1 bằng 1 khi t không dương rồi rơi xuống 0. Hàm dốc bằng 1 khi t không dương, giảm tuyến tính về 0 tại t bằng gamma. Hàm cận trên bằng 1 cho tới gamma rồi rơi xuống 0. Hàm dốc nằm giữa hai hàm bậc thang." |
| F3 (bỏ, mục 16) | `chuan-hai-loai-nhan.svg` (khoảng 420×180) | 6-03 | Trục ngang thang lôgarit từ $100$ đến $20\,000$ (vạch $100$; $1000$; $10\,000$), nhãn "‖ŵ‖". Hai đoạn ngang: hàng trên "nhãn thật" từ $351$ đến $1721$, dấu tròn đặc tại trung bình $916$; hàng dưới "nhãn hoán vị" từ $6792$ đến $14\,052$, dấu vuông đặc tại trung bình $10\,853$. Hai hàng khác nhau ở hình dạng dấu và nhãn chữ, không chỉ màu. Nhãn số ở hai đầu và tại trung bình. `figcaption`: "Chuẩn $\lVert\hat w\rVert$ qua mười lần chạy, $m=200$: nhãn thật $351$–$1721$, trung bình $916$; nhãn hoán vị $6792$–$14\,052$, trung bình $10\,853$." | "Hai đoạn ngang trên trục lôgarit của chuẩn véc-tơ trọng số. Đoạn nhãn thật từ 351 đến 1721 với trung bình 916. Đoạn nhãn hoán vị từ 6792 đến 14 052 với trung bình 10 853. Hai đoạn không giao nhau." |

Cách dựng dữ liệu hình, không có số mới: F1 vẽ miền suy từ công thức $f_\theta=\operatorname{ReLU}(s)-2\operatorname{ReLU}(s-1)-\tfrac12$ (chứng minh Mệnh đề 07.2, Bước 1, đúng trên $\mathbb R^2$), trùng Lời giải Bài tập 07.1(c); F2 vẽ ba hàm của Định nghĩa 07.15 và tính chất (iii); F3 vẽ các số của Ví dụ 07.10, Bước 2. Điều phối viên ghi cách dựng vào `review-log.md`. Chú thích hình được `deck_lint.py` đếm (mục 6, quy ước chung): chữ và số ngoài KaTeX của ba chú thích lần lượt khoảng $16$, $5$, $18$ âm tiết (đếm bằng script); tổng trang 2-05 là $42+16=58$, 5-04 là $50+5=55$, 6-03 là $25+18=43$ chưa kể bảng ($70$ khi tính chữ trong bảng). Người viết deck rút chú thích nếu trang vượt $60$.

## 9. Trang tổng kết

Chi tiết từng trang ở mục 6 (7-01 đến 7-07). Tóm tắt:
- **Bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh` (7-01):** năm hàng: Mệnh đề 07.2 (tất định), Mệnh đề 07.9 (tất định), Định lý 07.11 (xác suất ít nhất $1-\delta$, mọi $g$), Mệnh đề 07.13 (tất định), Hệ quả 07.16 (xác suất ít nhất $1-\delta$, mọi $\lVert w\rVert\le B$). Cột cuối ghi độ sâu chứng minh của ghi chú (đầy đủ, phác thảo); dòng "Đọc thêm: Nhận xét 07.6, 07.18." Ba bổ đề công cụ và phản ví dụ của từng giả thiết ở ghi chú diễn giả.
- **Vấn đề trung tâm (7-02):** bốn câu trả lời cho cả bài: các đại lượng của lớp kiến trúc như nhau với hai loại nhãn; độ phức tạp Rademacher chặn khoảng cách tổng quát hóa với xác suất ít nhất $1-\delta$ dưới (T1), (T3), (T5), (M); số hạng phạt theo chuẩn và lề không phụ thuộc $p$; trong thí nghiệm, chuẩn phân biệt hai loại nhãn nhưng cận lớn hơn $1$, nên báo lỗi trên tập kiểm tra. Giới hạn (không lồi; không giải thích việc chọn chuẩn nhỏ; mạng sâu) ở ghi chú diễn giả và ở 7-01.
- **Bài tập tổng hợp (7-03, 7-04):** Bài tập 07.4(b), (c), hai trang (đề; lời giải trên mặt trang). Lý do chọn: ghép định nghĩa tham số hóa thừa (mạch 2), Định lý 02.14, Mệnh đề 07.9 và Ví dụ 07.5 (mạch 3), số hạng tin cậy của Ví dụ 07.6 (mạch 4); hai lớp ở hai đầu ($P/m=5000$ có bảo đảm $0{,}1095$; $P/m=0{,}005$ không có bảo đảm) trả lời trực tiếp câu hỏi trung tâm. Phần (a) trùng nội dung 7-02 và 6-04; phần (d) dùng Nhận xét 07.17 và Ví dụ 07.11, để ở bài tập về nhà.
- **Câu hỏi tự kiểm tra (7-05):** bốn câu, câu trả lời dự kiến ở ghi chú diễn giả: (1) Mệnh đề 07.9(b); (2) hằng số $3$; (3) câu hỏi cuối buổi (a): $0{,}2815$ (và $0{,}2889$ với lưới); (4) câu hỏi cuối buổi (c).
- **Bài tập về nhà (7-06):** bảng `Mục | Bài tập` ánh xạ chín bài vào ba mạch theo mạch cung cấp kiến thức cuối cùng (mục 11, điểm 7); liên kết viewer.
- **Tài liệu tham khảo (7-07):** UML §20.1–20.3, §26.1 (trước buổi học); §26.2, §20.4–20.5 (sau buổi học); §26.3, §28.1, §15.2.3, Bài tập 20.5 và Bartlett, Foster, Telgarsky (2017) (mở rộng); dòng "Bài 08: Tính ổn định của SGD và tổng quát hóa trong học sâu".
- **Câu nối sang bài sau** (mặt trang 7-07 một dòng; ghi chú diễn giả 7-07): cận cấp lớp không giải thích vì sao huấn luyện chọn nghiệm chuẩn nhỏ; Bài 08 hỏi quỹ đạo của hạ gradient ngẫu nhiên có cho bảo đảm cho chính hàm nó trả về không.

## 10. Bảng thuật ngữ Việt–Anh của deck

Theo ghi chú và `thuat-ngu.md` §10; tiếng Anh trong ngoặc ở lần dùng đầu trên trang nội dung (trang ghi ở cột cuối).

| Tiếng Việt | Tiếng Anh | Lần đầu trên mặt trang |
|---|---|---|
| lớp nơ-ron ẩn, lớp nơ-ron ra (gọn: lớp ẩn, lớp ra) | hidden layer, output layer | 1-06 |
| ReLU | rectified linear unit | 1-06 |
| nhãn hoán vị | permuted labels | 1-06 |
| tập kiểm tra | test set | 2-01 |
| hàm điểm số | score function | 2-01 |
| phép hoặc loại trừ | exclusive or, XOR | 2-02 |
| độ sâu, độ rộng, hàm kích hoạt | depth, width, activation function | 2-03 |
| mạng nơ-ron lan truyền tới | feedforward neural network | ghi chú diễn giả 2-03 (tiêu đề trang mang tên tiếng Việt; người viết deck thêm vào dòng mở của 2-03 nếu mật độ cho phép, trang đang ở 47) |
| xấp xỉ phổ quát | universal approximation | 2-06 |
| năng lực biểu diễn, năng lực thống kê | expressivity, statistical capacity | 2-06 |
| tham số hóa thừa, nội suy | overparameterization, interpolation | 2-08 |
| lớp kiến trúc, lớp con bị chặn theo chuẩn, mô hình do huấn luyện chọn | architecture class, norm-bounded class, model selected by training | 2-09 |
| bảo đảm cấp lớp | class-level guarantee | 2-09 |
| tính thuần nhất dương, chuẩn phổ | positive homogeneity, spectral norm | 2-10 |
| đổi tỉ lệ | rescaling | ghi chú diễn giả 2-10 (từ khóa mạch 2) |
| đặc trưng ngẫu nhiên, nghiệm nội suy chuẩn nhỏ nhất | random features, minimum-norm interpolant | 2-11 |
| biến Rademacher | Rademacher variables | 3-01 |
| độ phức tạp Rademacher thực nghiệm, tổng thể | empirical, population (Rademacher complexity) | 3-01 |
| nhãn ngẫu nhiên | random labels | 3-03 |
| lớp hàm lỗi | loss class | 3-03 |
| bất đẳng thức McDiarmid, bất đẳng thức sai phân bị chặn | McDiarmid's inequality, bounded differences inequality | ghi chú diễn giả 4-01 (tiêu đề trang 4-01 là tên bổ đề; mục 11, điểm 9) |
| cận phụ thuộc dữ liệu | data-dependent bound | 4-02 |
| cận không cho thông tin | vacuous bound | 4-04 |
| bổ đề co | contraction lemma | 5-03 |
| lề, hàm lỗi dốc, tỉ lệ vi phạm lề, lề chuẩn hóa | margin, ramp loss, margin violation rate, normalized margin | 5-04 |
| hàm lỗi logistic | logistic loss | ghi chú diễn giả 5-05 |
| lề nhiều lớp, độ phức tạp phổ | multiclass margin, spectral complexity | 6-06 |

Chỉ ở ghi chú diễn giả (tiếng Anh trong ngoặc ở đó): véc-tơ tần suất từ (bag of words), hàm lỗi bản lề (hinge loss), NP-khó (NP-hard), martingale Doob (Doob martingale), chuẩn nhóm (group norm), ma trận tham chiếu (reference matrices), hạt giống ngẫu nhiên (random seed). Đã có ở Bài 01–06, không nhắc tiếng Anh: tối thiểu hóa rủi ro thực nghiệm (ERM), hạ gradient ngẫu nhiên (SGD), chiều VC, tách trọn vẹn, hàm tăng trưởng, mẫu bóng, đối xứng hóa, sai số xấp xỉ, sai số tối ưu thực nghiệm, khoảng cách tổng quát hóa, bất đẳng thức hợp, cận tin cậy.

## 11. Rủi ro và điểm cần điều phối viên quyết định

1. **Mạch 2 gộp §1–§5** (12 trang, 27 phút). Tách §5 thành mạch riêng thì deck có tám mạch, vượt trần bảy. Hai nửa của mạch là một so sánh: §4 cho thấy mạng nhỏ đủ năng lực biểu diễn, §5 cho thấy số tham số và chiều VC không đo được năng lực thống kê trong thí nghiệm; câu dẫn mạch nói cả hai vế. Phương án khác: gộp §5 với §6 thành mạch "Số tham số và độ phức tạp Rademacher" (12 trang) và để §1–§4 thành mạch 2 (8 trang); khi đó mạch 2 kết thúc ở bài tập 2-07 và mạch 3 mở bằng Định nghĩa 07.4. Khuyến nghị giữ.
2. **Số trang 54**, vượt mục tiêu 45–52 hai trang, dưới trần 55 (lý do ở mục 3). Phương án rút còn 52, không bỏ bước nào của hành trình khái niệm: (a) gộp 6-03 và 6-04 thành một trang Ví dụ 07.10 và bỏ hình F3 (bảng chuẩn giữ, các số của Bước 3–4 vào hai dòng; trang sẽ ở khoảng $60$); (b) chuyển Nhận xét 07.18 (6-06) vào ghi chú diễn giả 6-05 và dòng "Đọc thêm" của 7-01: mất trang phân biệt kết quả đọc thêm với kết quả chứng minh mà bản giao việc nêu. Khuyến nghị giữ 54, hoặc chỉ (a) nếu cần 53.
3. **Kết quả không có trang ý tưởng chứng minh riêng:** Bổ đề 07.8 (công cụ, chứng minh ba bước; lộ trình ở ghi chú diễn giả 3-02); Bổ đề 07.10 (công cụ, phác thảo; Phụ lục A ở ghi chú diễn giả 4-01); Bổ đề 07.14 (công cụ, phác thảo; Phụ lục B ở ghi chú diễn giả 5-03); Nhận xét 07.12 (hai lần Định lý 07.11 và bất đẳng thức hợp, ghi chú diễn giả 4-04); Nhận xét 07.17 (Hệ quả 07.16 với $\delta q_k$, ghi chú diễn giả 6-02); Nhận xét 07.3, 07.6, 07.18 (dẫn UML hoặc đọc thêm). Năm kết quả chính có trang riêng: Mệnh đề 07.2 (2-05), Mệnh đề 07.9 (3-04), Định lý 07.11 (4-03), Mệnh đề 07.13 (5-02), Hệ quả 07.16 (5-06). Nếu điều phối viên coi bất đẳng thức McDiarmid là kết quả chính, trang 55 là "Ý tưởng chứng minh: bất đẳng thức McDiarmid" sau 4-01 (lộ trình đã có ở ghi chú diễn giả 4-01).
4. **Ví dụ 07.9 (hồi quy bình phương) chỉ ở ghi chú diễn giả 6-05.** Ví dụ giữ lời hứa của Bài 06 (lớp không ổn định đều nhưng hội tụ đều) và dùng Nhận xét 07.12; một trang riêng làm deck 55 trang. Ghi chú diễn giả 6-05 nêu cận $0{,}2577$ tại $m=10^4$ và câu kết của ví dụ.
5. **Không có trang "Kỹ thuật." riêng trong Bài 07.** Quy định chỉ cho trang riêng khi kỹ thuật dùng lại qua các bài; `grep` trên ghi chú Bài 08–10 không thấy McDiarmid, độ phức tạp Rademacher, bổ đề co hay Mệnh đề 07.13 (Bài 08 chỉ dẫn Hệ quả 07.16 hai lần như một kết quả, Bài 09 dẫn Ví dụ 07.11, Bước 4; Bài 10 dẫn Định lý 07.11 như một thiết lập). Các mẹo một chứng minh là một dòng "Kỹ thuật." trên trang ý tưởng chứng minh (2-05, 3-04, 5-06) hoặc ở ghi chú diễn giả (4-03: sai phân của cận trên đúng). Nhắc lại bằng tên: đối xứng hóa và mẫu bóng (4-03), chia xác suất thất bại theo trọng số (6-02). Nếu điều phối viên muốn trang "Kỹ thuật." cho bổ đề co (dùng ba lần trong bài: 5-06, 6-05, Bài tập 07.3(e)), trang đó thay dòng "Kỹ thuật." của 5-06 và làm deck 55 trang.
6. **Bài tập tổng hợp: Bài tập 07.4(b), (c)** (7-03, 7-04). Phương án khác: Bài tập 07.4(a) (sáu đại lượng của hai lượt huấn luyện), gần thí nghiệm hơn nhưng trùng 7-02 và 6-04; Bài tập 07.6(a) (ba bảng, số mũ $\alpha\approx1{,}23$), cần ba bảng số trên mặt trang. Đề nghị chấp nhận (b), (c). Câu chữ đề rút gọn hai chỗ: "kiểm các giả thiết của Định lý 02.14 và tính bán kính $r_m$ của phần (a)" thành "Kiểm giả thiết của Định lý 02.14, tính $r_m$ của phần (a)"; "Trên một mẫu có $200$ đầu vào" thành "với $200$ đầu vào". Lời giải 7-04 viết công thức $r_m$ của Định lý 02.14(a) tại chỗ dùng, thay cho một dòng "Nhắc lại:" trên 7-03.
7. **Bảng `Mục | Bài tập` (7-06)** chỉ có ba hàng: mạch 3 và mạch 5 không có bài nào theo quy tắc "mạch cung cấp kiến thức cuối cùng": Bài tập 07.2(b) cần Định lý 07.11 (mạch 4); Bài tập 07.3(e) cần Bước 4 của Ví dụ 07.11 (mạch 6). Phương án: xếp theo phần (07.2(a), (c), (d) ở mạch 3; 07.3(a)–(d) ở mạch 5), như bài tập trên mặt trang 3-06 và 5-07. Khuyến nghị giữ quy tắc của bài học deck 01 (cả bài vào một mạch).
8. **Chọn bài tập giữa cụm.** Mạch 2: Bài tập 07.5(c) (hàm mục tiêu không lồi) thay cho 07.1(a), (c), vì nó cho thấy trên mặt trang chỗ không chuyển kết quả lồi sang mạng mà bản giao việc yêu cầu; kết quả 07.1(c) (miền dải và điểm $(\tfrac12,\tfrac12)$) đã nằm ở 2-05 và hình F1. Mạch 3: phần cuối của 07.2(c) (bảng tám giá trị của $\tau$, cùng số liệu Ví dụ 07.4). Mạch 4: 07.2(b). Mạch 5: 07.3(d) (số chiều không vào độ phức tạp). Mạch 6: không có trang bài tập riêng; bài tổng hợp 7-03 dùng thí nghiệm và hai lớp cực biên. Câu chữ rút gọn: 2-07 bỏ ngoặc "(hai hàng của $\Theta_1$, hai tọa độ của $b_1$, hai tọa độ của $\Theta_2$)" khỏi đề, đưa vào ghi chú diễn giả; 4-05 viết "so với Hệ quả 02.10(c)" cho "so với cận trên tin cậy của Hệ quả 02.10(c)" và "Chỉ ra bước làm cận yếu hơn với lớp một phần tử" cho "Chỉ ra bước của chứng minh Định lý 07.11 làm cận yếu hơn với lớp một phần tử". Đề nghị chấp nhận.
9. **Tiếng Anh ở lần dùng đầu khi tên nằm trong tiêu đề trang.** "Mạng nơ-ron lan truyền tới (feedforward neural network)" (2-03) và "bất đẳng thức McDiarmid (McDiarmid's inequality)" (4-01) có tên tiếng Việt ở tiêu đề trang; tiếng Anh nằm ở ghi chú diễn giả vì mật độ (4-01 ở $56$). Phương án: thêm tiếng Anh vào dòng mở của 2-03 (+3 âm tiết, trang thành $50$) và vào dòng **Bổ đề 07.10.** (+2, thành $58$). Khuyến nghị thêm cho 2-03; điều phối viên chọn cho 4-01.
10. **Luận điểm bìa** $65$ âm tiết theo script (Bài 06: $57$; Bài 01: $63$, ngoại lệ đã ghi). Bản ngắn, giữ điều kiện và "với xác suất cao", mất ý "bằng một nửa cho lớp kiến trúc": "Với quan sát độc lập, hàm lỗi bị chặn và lớp chọn trước, độ phức tạp Rademacher chặn khoảng cách tổng quát hóa với xác suất cao; trên lớp tuyến tính bị chặn theo chuẩn, cận theo lề không phụ thuộc số chiều." (44). Điều phối viên chọn.
11. **Mục tiêu (1-03)** giữ đủ năm mục tiêu theo thứ tự, rút câu chữ trong trần 80 (đếm $79$): mục tiêu 2 bỏ "thực nghiệm" và "của một lớp nhỏ"; mục tiêu 3 bỏ "các bước"; mục tiêu 4 bỏ "suy ra" và "bằng số"; mục tiêu 5 không viết thành ba vế "vì sao". Ghi chú diễn giả nêu đủ các ý đã rút.
12. **Trang 2-09 mở bằng định nghĩa.** Câu mở của §5 ("Một bảo đảm học có thể nói về một lớp hay về riêng hàm mà phép huấn luyện chọn") nằm ở ghi chú diễn giả; mặt trang 2-08 kết bằng câu "Tham số hóa thừa không kéo theo nội suy, và ngược lại", và dòng cuối của 2-09 nêu vấn đề (bán kính phụ thuộc $S$). Nếu cổng duyệt yêu cầu câu mở trên mặt trang (bài học "mở khái niệm bằng định nghĩa"), người viết deck thêm câu đó ($14$ âm tiết) và chuyển dòng "Bảo đảm cấp lớp …" vào ghi chú diễn giả để giữ trang dưới $60$.
13. **Trang bảng vượt trần khi tính chữ trong bảng.** `deck_lint.py` bỏ toàn bộ bảng khi đếm; mục 15 đếm cả chữ trong ô (cách của storyboard Bài 06). Theo cách thứ hai: 1-06 ($59+34$), 2-06 ($38+35$), 3-02 ($26+35$), 6-03 ($25+27$, cộng chú thích hình $18$), 7-01 ($6+81$, trần $80$). Chữ trong bảng chủ yếu là nhãn hàng và cột (tên lớp, tên nhãn, tên năng lực); số trong ô không tính. Đề nghị chấp nhận theo cách đếm của `deck_lint.py` (mặt chữ ngoài bảng $\le60$); nếu không, 7-01 bỏ "(đầy đủ)/(phác thảo)" khỏi cột cuối và đưa độ sâu chứng minh vào ghi chú diễn giả ($-10$).
14. **Câu nối giữa mạch trên mặt trang.** Mạch 2→3: dòng "**Diễn giải:** $P$, $d$, $\rho_m$ như nhau với hai loại nhãn" (2-11) và câu dẫn mạch 3. Mạch 3→4: "**Diễn giải:** … số tham số không xác định độ phức tạp" (3-05) và câu dẫn mạch 4. Mạch 4→5: dòng "Cận không cho thông tin" (4-04) và dòng mở 5-01 "cần lớp tuyến tính có độ phức tạp nhỏ". Mạch 5→6: dòng "Không phụ thuộc $p$" (5-01, 5-05) và câu dẫn mạch 6. Mạch 6→7: dòng cuối 6-06. Cổng duyệt kiểm các câu này.
15. **Công thức cần đo ở 390 px** (ngắt `aligned` chỉ khi tràn): 1-02 (bán kính VC), 2-03 (bốn đẳng thức của định nghĩa; gần như chắc chắn cần ngắt), 2-04, 2-07 (hàm $F$), 2-11 ($\hat w$), 3-01, 4-01 (bảo đảm), 4-02 (b), 4-03 Bước 4, 5-01, 5-05 (gần như chắc chắn cần ngắt), 5-06 Bước 1, 6-02, 6-06 (gần như chắc chắn cần ngắt), 7-01 (các ô công thức); bảng 1-06, 2-06, 3-02, 3-06, 4-04, 6-01, 6-03, 7-01, 7-06 đặt trong `.table-scroll`.
16. **Trang sát trần** (đếm bằng script, mục 15, chữ ngoài bảng): 2-08, 3-03, 6-02, 7-02 ($60$); 1-02, 1-06, 4-05, 5-07, 6-06 ($59$); 3-01, 4-02 ($58$); 2-09, 7-04 ($57$). Người viết deck không thêm chữ trên các trang này. Trung vị $55$ trên 45 trang nội dung theo chữ ngoài bảng ($56$ khi tính cả chữ trong bảng); 15 trang $\le50$ theo chữ ngoài bảng (9 khi tính cả bảng): không đạt mục tiêu trung vị 45–50 của bản giao việc. Lý do: các trang kết quả giữ đủ giả thiết của ghi chú, tiếng Anh ở lần dùng đầu (ba thuật ngữ trên 2-09, bốn trên 5-04, ba trên 6-06), số viết trong câu có tính, và bài này có nhiều thuật ngữ mới hơn Bài 06. Khi cổng duyệt yêu cầu thêm chữ, cắt bù trên cùng trang hoặc chuyển dòng "Diễn giải:" vào ghi chú diễn giả.
17. **Ghi chú diễn giả dẫn bài sau** chỉ ở 7-07 (Bài 08), không trên mặt trang trừ dòng tên Bài 08 của trang tài liệu.
18. **"Thí nghiệm" và "kết quả thí nghiệm".** Bảng 1-06, các số của 2-11, 6-03, 6-04 là số đo của thí nghiệm học phần (Phụ lục D); ghi chú diễn giả 1-06 và 6-03 nói rõ đó là kết quả thí nghiệm, không phải định lý (blueprint §E). Mặt trang không thêm câu rào đón.
19. **Kí hiệu $\Psi$** được đặt ở 4-01 (trước định lý, khác ghi chú đặt trong chứng minh) để nêu vấn đề "cận trên đúng không là trung bình" trên mặt trang. Kí hiệu khớp ghi chú.
20. **Nhận xét 07.18 trên mặt trang (6-06)** dùng dạng $C_xR_\Theta/(\gamma\sqrt m)$ thay cho $\lVert X\rVert_2R_\Theta\ln\bar N/(\gamma m)$ của ghi chú, kèm điều kiện "khi $\lVert x_i\rVert\le C_x$" và "$\tilde O$ ẩn thừa số lôgarit"; đây là bước chính ghi chú viết ngay sau phát biểu, nên không thêm khẳng định. $r_j$ và $M_j$ chỉ giải nghĩa ở ghi chú diễn giả (trang ở $59$). Nếu cổng duyệt đòi dạng nguyên văn, mặt trang thêm dòng "**Kí hiệu:** $\lVert X\rVert_2$, $\bar N$, $r_j$" và bỏ dòng "Chứng minh nằm ngoài phạm vi học phần" sang ghi chú diễn giả (quy tắc tác giả cho phép câu này nhưng không bắt buộc trên mặt trang).
21. **Kí hiệu $K$ hai nghĩa**: $K=\ln(1+e^{BC_x})$ ở 6-05 (Ví dụ 07.11) và $K=3$ số hàm của lớp hữu hạn ở 7-04 (Định lý 02.14, Bài tập 07.4(b)). Cả hai là kí hiệu của ghi chú và tệp bài tập; deck giữ nguyên, ghi chú diễn giả 7-04 nói "số hàm của lớp" ngay khi dùng. Đề xuất cho tác giả ở mục 13.

## 12. Bảng đối chiếu trang → mục và khối của ghi chú

Cột "Đưa vào" ghi kí hiệu, thuật ngữ hoặc kết quả xuất hiện lần đầu trên mặt trang (định nghĩa hoặc "Nhắc lại:"/"Kí hiệu:"), để kiểm quy tắc định nghĩa trước khi dùng.

| Trang | Mục ghi chú | Khối (số của ghi chú) | Đưa vào |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §10 | — (bằng lời) | — |
| 1-02 | Kiến thức tiên quyết; Câu hỏi ôn nhanh | Định lý 03.15, Mệnh đề 03.9, Mệnh đề 04.3, Định lý 02.7, Hệ quả 02.10, Định nghĩa 05.4 (nhắc lại) | (T1), (T5), (M), $\rho_m$, $\Pi_{\mathcal H}$, $\delta$, $L_S$, $L_D$, $\mathcal H^p_{\mathrm{aff}}$, $\mathcal H^p_{\mathrm{hom}}$, $p$, $r$-đại diện, $L^*$, $\tilde h$, $\operatorname{opt}_S$, sai số xấp xỉ, $h_w$, $h_{w,0}$, $\tilde y$, $C_x$, $G$-Lipschitz, bất đẳng thức hợp |
| 1-03 | Mục tiêu học tập | — | — |
| 1-04 | toàn bài; §13 | — | — |
| 1-05 | đoạn mở đầu | — | — |
| 1-06 | Câu hỏi mở đầu và hai đoạn sau | — | $m$, $N$, $w$, $f$, lớp nơ-ron ẩn, lớp nơ-ron ra, ReLU, nhãn hoán vị, nhãn thật |
| 2-00 | §1–§5 | — | — |
| 2-01 | §1, §2 | tám thành phần; (T3) | $z$, $\mathcal X$, $S$, $D$, tập kiểm tra, hàm điểm số, $A(S;\xi)$, $\hat\theta$, $h_{\hat\theta}$, $\mathcal H$, ERM, SGD, (T3) |
| 2-02 | §3 | Ví dụ 07.1; khối ứng dụng | $x_1\oplus x_2$, phép hoặc loại trừ, $h_{w,b}$, $d$, $B$, $\gamma$, lề (theo công thức $\tilde y\langle w,x\rangle$) |
| 2-03 | §4 | Định nghĩa 07.1 và hai đoạn sau | $J$, $N_j$, $N$, $\varsigma$, $\theta$, $\Theta_j$, $b_j$, $a_j$, $f_\theta$, $h_\theta$ |
| 2-04 | §4 | Mệnh đề 07.2 | $s$ |
| 2-05 | §4 | chứng minh Mệnh đề 07.2; đoạn sau | — |
| 2-06 | §4 | Nhận xét 07.3; đoạn ba năng lực | xấp xỉ phổ quát, năng lực biểu diễn, năng lực thống kê, khả năng tối ưu |
| 2-07 | Bài tập 07.5 | Bài tập 07.5(c) | $F$, $\theta_{\mathrm{swap}}$, $\theta_{\mathrm{mid}}$ |
| 2-08 | §5 | Định nghĩa 07.4; đoạn Nhận xét 03.10 | $P$, $\mathcal H_{\sin}$, tham số hóa thừa, nội suy |
| 2-09 | §5 | Định nghĩa 07.5 và hai đoạn sau | $\mathcal H_{J,N}$, $\mathcal H_{J,N}(B)$, lớp kiến trúc, lớp con, mô hình do huấn luyện chọn, cấp lớp; Ví dụ 03.8 (tên) |
| 2-10 | §5 | Ví dụ 07.2 | $c$, $\lVert\cdot\rVert_{\mathrm{op}}$, tính thuần nhất dương |
| 2-11 | §5; Phụ lục D | Ví dụ 07.3; Nhận xét 07.6 (ghi chú diễn giả) | $v_j$, $b_{1j}$, $\chi$, $\hat w$, $\mathcal H_{2,2000}$ (dùng ở 3-05; ghi chú diễn giả 2-11 gọi tên) |
| 3-00 | §6 | — | — |
| 3-01 | §6 | Định nghĩa 07.7 và ba đoạn sau | $\sigma_i$, $A$, $\widehat{\mathfrak R}(A)$, $\widehat{\mathfrak R}_S(\mathcal F)$, $\mathfrak R_m(\mathcal F)$, $\mathcal F\circ S$ |
| 3-02 | §6 | Bổ đề 07.8; Ví dụ 07.4 | $c$, $\bar a$ |
| 3-03 | §6 | Mệnh đề 07.9 | $\tau_i$, $\operatorname{err}_\tau$, $x_{1:m}$, lớp hàm lỗi |
| 3-04 | §6 | chứng minh Mệnh đề 07.9 | $h_i$, $y$ |
| 3-05 | §6 | Ví dụ 07.5 | — |
| 3-06 | Bài tập 07.2 | Bài tập 07.2(c), phần cuối | $a$, $a'$, $h_a$, $h_{a'}$ |
| 4-00 | §7 | — | — |
| 4-01 | §7; Phụ lục A | Bổ đề 07.10 và đoạn sau | $g$, $\mathcal G$, $L_D(g)$, $L_S(g)$, $\Psi$, $V_i$, $\mathcal V_i$, $Q$, $c_i$, $t$ |
| 4-02 | §7 | Định lý 07.11 | cận phụ thuộc dữ liệu |
| 4-03 | §7; Phụ lục C | chứng minh Định lý 07.11 | $S'$, $Z_i'$, mẫu bóng, đối xứng hóa (nhắc lại) |
| 4-04 | §7 | Ví dụ 07.6; Nhận xét 07.12 (ghi chú diễn giả) | cận không cho thông tin |
| 4-05 | Bài tập 07.2 | Bài tập 07.2(b) | — |
| 5-00 | §8 | — | — |
| 5-01 | §8 | đoạn mở §8; Mệnh đề 07.13 | $\mathcal F_B$, $v_\sigma$ |
| 5-02 | §8 | chứng minh Mệnh đề 07.13; Ví dụ 07.7 | $\mathbf e_i$ |
| 5-03 | §8; Phụ lục B | Bổ đề 07.14 và hai đoạn sau | $\phi_i$, $\phi\circ A$, bổ đề co |
| 5-04 | §8 | Định nghĩa 07.15 và ba đoạn sau | $\phi_\gamma$, $\ell_\gamma$, $L^{<\gamma}_S$, lề, hàm lỗi dốc, tỉ lệ vi phạm lề, lề chuẩn hóa ($L^\gamma_D$, $L^\gamma_S$ ở ghi chú diễn giả 5-04; dùng trên mặt trang 5-05) |
| 5-05 | §8 | Hệ quả 07.16 | $L^\gamma_D$ (theo $\ell_\gamma$ của 5-04) |
| 5-06 | §8 | chứng minh Hệ quả 07.16 | $\mathcal G_\gamma$ |
| 5-07 | Bài tập 07.3 | Bài tập 07.3(d) | $p'$, $\hat x_i$, $w'$, $w''$ |
| 6-00 | §9 | — | — |
| 6-01 | §9 | Ví dụ 07.8 | $\epsilon$ |
| 6-02 | §9 | Nhận xét 07.17 | $\gamma_k$, $q_k$, $k$; chia xác suất thất bại theo trọng số (nhắc lại) |
| 6-03 | §9; Phụ lục D | Ví dụ 07.10, Bước 1–2 | — |
| 6-04 | §9 | Ví dụ 07.10, Bước 3–4 | $B_k$ |
| 6-05 | §9 | Ví dụ 07.11; Ví dụ 07.9 (ghi chú diễn giả) | $K$, hàm lỗi logistic |
| 6-06 | §9 | Nhận xét 07.18 | $\Theta$, $\varsigma_j$, $G_j$, $\hat y_\Theta$, $\mu_\Theta$, $R_\Theta$, $\tilde O$; $r_j$ ($r_j$, $M_j$ giải nghĩa ở ghi chú diễn giả) |
| 7-00 | §10–§13 | — | — |
| 7-01 | §4, §6, §7, §10 | Mệnh đề 07.2, 07.9, Định lý 07.11 | — |
| 7-02 | §8–§10 | Mệnh đề 07.13, Hệ quả 07.16 | — |
| 7-03 | §10 | — | — |
| 7-04 | Bài tập 07.4 | Bài tập 07.4(b), (c) (đề) | Định lý 02.14 (tên), $r_m$ |
| 7-05 | Bài tập 07.4 | Bài tập 07.4(b), (c) (lời giải) | (T4); số hàm $3$ viết thẳng, không đặt $K$ |
| 7-06 | §12 | câu hỏi cuối buổi (a), (c) | — |
| 7-07 | §11 | `exercises.md` | — |
| 7-08 | §12, §13 | — | — |

## 13. Đề xuất sửa ghi chú và tệp bài tập (không sửa; chờ điều phối viên và tác giả)

Không thấy lỗi toán học trong các khối deck dùng; mọi con số của ví dụ và năm bài tập trên mặt trang đã tính lại (mục 5) và khớp ghi chú, tệp bài tập. Số đo của thí nghiệm (Phụ lục D) nhất quán với các khoảng suy từ $C_x\in[1{,}518;1{,}544]$ (V18).

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất |
|---|---|---|---|---|
| nhẹ | ghi chú, Nhận xét 07.18, câu "Cận của Hệ quả 07.16 không thay được $R_\Theta$." | Câu khó đọc: không rõ "thay" theo chiều nào (Hệ quả 07.16 thay cho cận của Bartlett–Foster–Telgarsky, hay $B$ thay cho $R_\Theta$) | ghi chú §9, đoạn cuối Nhận xét 07.18 (dòng "Ngoài thừa số logarit, …") | "Hệ quả 07.16 không cho cận này: nó chỉ áp dụng cho lớp tuyến tính, tức mạng có lớp ẩn cố định." |
| nhẹ | ghi chú, Ví dụ 07.11, Bước 4; `exercises.md`, Lời giải 07.4(b) | $K$ hai nghĩa trong cùng bài: $K=\ln(1+e^{BC_x})$ và $K=3$ số hàm của lớp hữu hạn (kí hiệu của Bài 02) | ghi chú dòng "$K=\ln(1+e^{BC_x})$"; `exercises.md` "(T4) với $K=3$" | Đổi kí hiệu của Ví dụ 07.11, chẳng hạn $K_{\log}$, hoặc giữ và nêu trong §2; deck giữ nguyên (mục 11, điểm 21) |
| nhẹ | ghi chú, "Kiến thức tiên quyết", dòng "Từ Bài 02" | Bài tập 07.4(b) dùng Định lý 02.14 và (T4), không có trong danh sách tiên quyết | `exercises.md` Bài tập 07.4(b) "kiểm các giả thiết của Định lý 02.14"; dòng "Từ Bài 02" chỉ có Bổ đề 02.5, 02.6, 02.12, Định lý 02.7, Hệ quả 02.10, Định nghĩa 02.13 | Thêm "Định lý 02.14, (T4)" vào dòng "Từ Bài 02"; deck viết công thức $r_m$ và nghĩa của (T4) tại chỗ dùng (7-04) |

## 14. Danh sách kỹ thuật đã giới thiệu đến hết Bài 07

| Kỹ thuật | Bài, trang (lần đầu) | Dạng | Trong deck Bài 07 |
|---|---|---|---|
| Tính tuyến tính của kì vọng | Bài 01, `L01-3-03` | một dòng | dùng không nhắc tên (3-02, 3-04) |
| Bất đẳng thức hợp | Bài 01, `L01-4-04` | trang riêng | nhắc tên trên 1-02; dùng ở 4-03 Bước 4, ghi chú diễn giả 4-04, 6-02 |
| Chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ | Bài 01, `L01-6-07` | trang riêng | không dùng |
| Tối thiểu hóa từng điểm rồi lấy kì vọng | Bài 01, `L01-5-09` | một dòng | không dùng |
| Phương pháp Chernoff | Bài 02, `L02-3-01` | trang riêng | ghi chú diễn giả 4-01 (Phụ lục A) |
| Dây cung của hàm lồi và Taylor bậc hai tại $0$ (bổ đề Hoeffding) | Bài 02, `L02-3-03` | một dòng | bổ đề Hoeffding nêu tên ở ghi chú diễn giả 4-01 |
| Đảo cận đuôi thành bán kính và cỡ mẫu | Bài 02, `L02-4-04` | trang riêng | ghi chú diễn giả 6-01 (cỡ mẫu $57\,958$, $231\,829$, $3690$) |
| Chia xác suất thất bại cho từng giả thuyết | Bài 02, `L02-5-05` | trang riêng | $\delta/2$ cho hai biến cố ở 4-03 Bước 4, không nhắc tên |
| Bước tất định trên biến cố đại diện | Bài 02, `L02-5-11` | trang riêng | không nhắc tên (4-03 Bước 4: trên giao hai biến cố) |
| Cận dưới và cận trên cho chiều VC | Bài 03, `L03-2-04` | trang riêng | 2-11 ($m\le d\le N$), không nhắc tên |
| Đối xứng hóa và mẫu bóng | Bài 03, `L03-5-06` | trang riêng | **nhắc lại một dòng ở 4-03**; dùng ở 4-03 Bước 1–2 |
| Hàm tăng trưởng thay cho số giả thuyết | Bài 03, `L03-5-07` | trang riêng | 2-11 ($\Pi(2m)\ge2^m$ trong bán kính VC), không nhắc tên |
| Thêm bớt kì vọng rồi bình phương; mỗi số hạng chéo một lý do | Bài 04, `L04-3-03` | một dòng | gần với Bước 3 của 5-02, không nhắc tên |
| Chia xác suất thất bại theo trọng số | Bài 04, `L04-4-04` | trang riêng | **nhắc lại một dòng ở 6-02** (Nhận xét 07.17) |
| Lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện | Bài 04, `L04-6-02` | một dòng | ghi chú diễn giả 2-01, 6-04 (có điều kiện theo lớp ẩn; tập kiểm tra độc lập) |
| Kì vọng có điều kiện theo lịch sử | Bài 05, `L05-3-07` | trang riêng | ghi chú diễn giả 4-01 (bước tăng của martingale Doob), không nhắc tên |
| Tổng triệt tiêu và trung bình các điểm lặp | Bài 05, `L05-4-05` | trang riêng | tổng triệt tiêu của các bước tăng ở ghi chú diễn giả 4-01 |
| Cân hai số hạng | Bài 05, `L05-4-08` | một dòng | không dùng |
| Số hạng chéo bằng $0$ cho véc-tơ không tương quan | Bài 05 | một dòng | 5-02 Bước 3; ghi chú diễn giả 5-02 nhắc tên |
| Lập luận đổi vai (thay một điểm) | Bài 06, 4-05 (storyboard Bài 06) | trang riêng | không dùng (Bài 07 là bảo đảm cấp lớp); sai phân bị chặn của Bước 3 ở 4-03 là cùng phép thay một quan sát, ghi chú diễn giả 4-03 không nhắc tên |
| Cộng hai bất đẳng thức tăng trưởng bậc hai đối xứng | Bài 06, 5-02 | một dòng | không dùng |
| Điểm trên đoạn thẳng rồi cho dần về đầu mút | Bài 06, 3-03 | một dòng | không dùng |
| Đưa hàm nhiều biến về một biến bằng các hàng trùng nhau của $\Theta_1$ | **Bài 07, 2-05** | một dòng | — |
| Đổi biến giữa dấu và nhãn ngẫu nhiên, $\sigma_i=2\tau_i-1$ | **Bài 07, 3-04** | một dòng | — |
| Sai phân của một cận trên đúng không quá sai phân lớn nhất | **Bài 07, ghi chú diễn giả 4-03** (Phụ lục C(ii)) | một dòng | — |
| Thay hàm lỗi 0–1 bằng hàm lỗi bị chặn, Lipschitz nằm trên nó, rồi dùng bổ đề co | **Bài 07, 5-06** | một dòng | dùng lại ở 6-05 (hàm lỗi logistic chia cho $K$) |

Bài 07 không có trang "Kỹ thuật." riêng (mục 11, điểm 5): ghi chú Bài 08–10 không dùng lại các kỹ thuật mới của bài. Deck Bài 08 nhắc lại "lập luận đổi vai" (Bài 06) và "kì vọng có điều kiện theo lịch sử" (Bài 05) bằng tên.

## 15. Mật độ mặt trang đo bằng script

Đếm bằng `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-07/storyboard/count.py` (bản của storyboard Bài 06, thêm cột chữ ngoài bảng) trên văn bản dự kiến của mục 6: token cách nhau bởi khoảng trắng, có chữ cái hoặc chữ số; bỏ tiêu đề, công thức `$…$`, chỉ dẫn `{{…}}`, dấu fragment; nhãn "(T1)", "(a)", số khối như "07.11" và tiếng Anh trong ngoặc được đếm (số viết trong câu có tính). Cột "Chữ ngoài bảng" là cách đếm của `deck_lint.py` (bỏ bảng); cột "Kể cả chữ trong bảng" cộng các ô có chữ (cách của storyboard Bài 06). Mỗi gạch đầu dòng là một dòng; mỗi công thức hiển thị là thêm một dòng (số 0 trong cột theo dòng). Chú thích hình chưa cộng (mục 8: 2-05 $+16$, 5-04 $+5$, 6-03 $+18$). Trang tổng quan và trang tiêu đề mạch không đếm theo trần: bìa (luận điểm $65$), hộp vấn đề trung tâm $23$, câu dẫn mạch $21$–$25$ (bảng mạch), trang "Nội dung" $63$ (trần $80$). Kết quả đầy đủ: `counts.txt` cùng thư mục.

| Trang | Chữ ngoài bảng | Kể cả chữ trong bảng | Dòng | Theo dòng | Ghi chú diễn giả |
|---|---:|---:|---:|---|---:|
| 1-02 | 59 | 59 | 5 | 16; 9; 11; 17; 6 | 107 |
| 1-03 | 79 | 79 | 5 | 18; 17; 12; 15; 17 | 116 |
| 1-06 | 59 | 93 | 6 | 9; 16; 9; 10; 15 | 111 |
| 2-01 | 55 | 55 | 5 | 9; 14; 13; 3; 16 | 146 |
| 2-02 | 55 | 55 | 5 | 12; 0; 17; 10; 16 | 97 |
| 2-03 | 47 | 47 | 5 | 14; 18; 2; 0; 13 | 70 |
| 2-04 | 39 | 39 | 5 | 17; 9; 9; 0; 4 | 74 |
| 2-05 | 42 | 42 | 5 | 11; 4; 6; 6; 15 | 83 |
| 2-06 | 38 | 73 | 4 | 17; 12; 9 | 123 |
| 2-07 | 45 | 45 | 6 | 13; 10; 7; 11; 2; 2 | 135 |
| 2-08 | 60 | 60 | 4 | 19; 15; 14; 12 | 118 |
| 2-09 | 57 | 57 | 5 | 14; 10; 12; 12; 9 | 134 |
| 2-10 | 51 | 51 | 5 | 9; 11; 9; 7; 15 | 77 |
| 2-11 | 49 | 49 | 6 | 11; 6; 8; 11; 5; 8 | 111 |
| 3-01 | 58 | 58 | 6 | 17; 18; 17; 0; 6; 0 | 138 |
| 3-02 | 26 | 61 | 4 | 16; 4; 6 | 114 |
| 3-03 | 60 | 60 | 6 | 13; 8; 9; 5; 14; 11 | 98 |
| 3-04 | 49 | 49 | 5 | 6; 16; 7; 10; 10 | 126 |
| 3-05 | 52 | 52 | 4 | 12; 18; 5; 17 | 73 |
| 3-06 | 55 | 55 | 5 | 10; 16; 6; 7; 16 | 75 |
| 4-01 | 56 | 56 | 5 | 2; 17; 14; 14; 9 | 148 |
| 4-02 | 58 | 58 | 6 | 15; 16; 6; 10; 0; 11 | 88 |
| 4-03 | 56 | 56 | 5 | 10; 6; 11; 16; 13 | 192 |
| 4-04 | 44 | 56 | 5 | 4; 9; 14; 17 | 110 |
| 4-05 | 59 | 59 | 6 | 10; 16; 12; 2; 4; 15 | 99 |
| 5-01 | 51 | 51 | 6 | 16; 10; 9; 8; 0; 8 | 79 |
| 5-02 | 33 | 33 | 5 | 7; 8; 7; 3; 8 | 135 |
| 5-03 | 56 | 56 | 5 | 17; 15; 5; 11; 8 | 120 |
| 5-04 | 50 | 50 | 5 | 17; 10; 8; 5; 10 | 107 |
| 5-05 | 53 | 53 | 5 | 12; 13; 11; 0; 17 | 86 |
| 5-06 | 56 | 56 | 6 | 11; 7; 5; 6; 19; 8 | 151 |
| 5-07 | 59 | 59 | 6 | 5; 17; 7; 6; 14; 10 | 76 |
| 6-01 | 30 | 45 | 6 | 5; 7; 9; 3; 6 | 94 |
| 6-02 | 60 | 60 | 6 | 10; 12; 16; 13; 0; 9 | 70 |
| 6-03 | 25 | 52 | 4 | 9; 3; 13 | 66 |
| 6-04 | 56 | 56 | 4 | 10; 13; 18; 15 | 96 |
| 6-05 | 51 | 51 | 5 | 1; 7; 16; 16; 11 | 142 |
| 6-06 | 59 | 59 | 6 | 14; 14; 11; 0; 12; 8 | 118 |
| 7-01 | 6 | 87 | 2 | 6 | 120 |
| 7-02 | 60 | 60 | 4 | 16; 19; 10; 15 | 137 |
| 7-03 | 55 | 55 | 4 | 14; 19; 6; 16 | 127 |
| 7-04 | 57 | 57 | 5 | 12; 12; 13; 5; 15 | 98 |
| 7-05 | 51 | 51 | 4 | 19; 9; 6; 17 | 113 |
| 7-06 | 11 | 51 | 2 | 11 | 121 |
| 7-07 | 56 | 56 | 4 | 12; 11; 19; 14 | 150 |

Trần: 60 cho trang nội dung, 80 cho 1-03, 7-01, 7-06; mọi dòng ≤ 20; mọi trang ≤ 6 dòng; ≤ 3 công thức hiển thị. Kết quả theo chữ ngoài bảng (`deck_lint.py`): không trang nào vượt trần (lớn nhất $60$ ở 2-08, 3-03, 6-02, 7-02; 1-03 $79$/80); không dòng nào vượt 20; không trang nào quá 6 dòng. Khi tính cả chữ trong bảng, năm trang vượt: 1-06 ($93$), 2-06 ($73$), 3-02 ($61$), 7-01 ($87$/80), 6-03 ($52$, thành $70$ khi cộng chú thích hình); quyết định ở mục 11, điểm 13. Trung vị $55$ (chữ ngoài bảng) và $56$ (kể cả bảng) trên 45 trang nội dung. Trang bài tập giữ câu chữ của `exercises.md`, trừ các rút gọn ghi ở mục 11, điểm 6 và 8 (2-07, 3-06, 4-05, 5-07, 7-03). Ghi chú diễn giả đếm cùng script (bỏ dòng nguồn): mọi trang ≤ 150 trừ trang ý tưởng chứng minh 4-03 ($192$) và 5-06 ($151$), trần 250.

## 16. Đối chiếu với deck cuối (người viết deck, 2026-11-16)

Tệp: `2627-1/lecture-07-mang-no-ron-tham-so-hoa-thua.html`; hình: `2627-1/img/lec-07/ham-loi-doc.svg` (F2). Deck áp dụng quyết định của điều phối viên trong `review-log.md` (mục "Quyết định của điều phối viên về storyboard và cổng duyệt") và các cắt ở mục 5 của `reviews/deck-storyboard-gate.md`; những chỗ đó thắng mục 1–15 ở trên. Các mục 6, 12, 15 phía trên giữ bản storyboard; bảng dưới ghi mọi chỗ deck lệch và lý do.

### 16.1 Số trang và mã trang

- **55 trang** (trần 55), không phải 54: bảng tổng kết năm hàng vượt khung 16:9 khoảng 330 px ở 1600×900 (`footer_check.py`), nên tách thành `7-01` "Bảng tổng kết" (Mệnh đề 07.2, 07.9, Định lý 07.11) và `7-02` "Bảng tổng kết (tiếp)" (Mệnh đề 07.13, Hệ quả 07.16, dòng "Đọc thêm"), như deck Bài 06. Các trang sau dời một số: vấn đề trung tâm `7-03`, bài tập tổng hợp `7-04` (đề) và `7-05` (lời giải), câu hỏi tự kiểm tra `7-06`, bài tập về nhà `7-07`, tài liệu tham khảo `7-08`. Mạch 7 có 9 trang; bảng mạch (mục 3) và mục 12 đã sửa theo.
- Mật độ (đếm theo `deck_lint.py`, chữ trong ô bảng có tính): mọi trang nội dung $\le60$ (Mục tiêu $79/80$; bảng tổng kết $47$ và $43$); **trung vị $51$** trên 46 trang nội dung (không tính bìa, Nội dung, Vấn đề trung tâm mở đầu, tiêu đề mạch). `deck_lint.py`: 0 phát hiện; `footer_check.py`: 0 trang; `deck_check.py`: console 0, page errors 0, failed 0, không `.katex-error`; các cờ OVERFLOW còn lại 1–4 px đều ở trang có $\sqrt{\ }$ (báo động giả đã biết).

### 16.2 Lệch theo quyết định của điều phối viên và cổng duyệt

| Trang | Lệch so với mục 6 | Lý do |
|---|---|---|
| 1-01 | Luận điểm bìa là bản một câu 47 âm tiết của cổng duyệt (mục 4, điểm 10) | quyết định điều phối viên |
| 1-02 | "(M) lớp con đếm được"; gộp dòng bất đẳng thức hợp, Hoeffding, Hệ quả 02.10 | L13; cắt mục 5 |
| 1-06 | Bỏ `caption` (mười hạt giống, $5000$ điểm vào ghi chú diễn giả); cột "$L_S$" và "$\min$ – $\max$"; gộp dòng lớp ra; câu hỏi rút gọn; "$f$" gọi tên "hàm điểm số" trên mặt trang | N1, L12 |
| 2-00 | Câu dẫn mạch "Mạng nhỏ biểu diễn được hàm mà hàm afin sai, …" | L16 |
| 2-01 | Bỏ dòng "Thuật toán … (ERM, SGD, phép nội suy)", ghép vào dòng mục tiêu; ví dụ thuật toán ở ghi chú diễn giả | T2 (giảm chép ghi chú) |
| 2-03 | Bỏ ví dụ $\mathbb 1[x\in\mathbb Q]$ và ví dụ $J=1$ khỏi mặt trang (vào ghi chú diễn giả); "$9$ khi $p=J=N_1=2$" ghép vào dòng tham số; "(feedforward neural network)" ở dòng mở | T2; mục 11, điểm 9; chống chạm chân trang |
| 2-04 | "Trực quan." nêu cơ chế (nơ-ron thứ hai trừ gấp đôi phần vượt, kéo $s=2$ về mức $s=0$); công thức $f_\theta$ ngắt hai dòng (tràn ở 390 px) | bài học deck 02 |
| 2-05 | **Bỏ dòng miền $\tfrac12\le x_1+x_2\le\tfrac32$ và hình F1**; giữ điểm $(\tfrac12,\tfrac12)$ (đoạn sau Mệnh đề 07.2 của ghi chú); thêm dòng "Với $J=1$, $h_\theta=h_{w,b}$ sai ít nhất một quan sát (Ví dụ 07.1)" (chỗ hỏng khi bỏ lớp ẩn, có trong ghi chú); bước chứng minh dùng `<ol>` | quyết định điều phối viên: không lộ lời giải Bài tập 07.1(c); T8 |
| 2-06 | Bỏ cột "Ví dụ 07.1" (hai số $0$, $\tfrac14$ vào ghi chú diễn giả); miền $[-1,1]^p\to[-1,1]$; "Xấp xỉ phổ quát chỉ chặn số hạng đầu (Mệnh đề 04.3)" | N1, L1 |
| 2-07 | Tiêu đề rút thành "Bài tập: hàm mục tiêu không lồi"; nhãn "Bài tập 07.5(c)." trên mặt trang; ghi chú diễn giả "Ở phần (b) …" | chống chạm chân trang; bài học "số Bài tập trên trang nguồn"; L18 |
| 2-08 | "Nhắc lại:" rút gọn; "và ngược lại" thay vế sau | cắt mục 5 |
| 2-09 | Mở bằng "Bảo đảm nói về một lớp, hoặc về riêng hàm do huấn luyện chọn."; dòng cấp lớp gộp "$B=\lVert\hat\theta\rVert$ phụ thuộc $S$"; "Ví dụ 03.8" vào ghi chú diễn giả | T10 |
| 2-10 | "đổi tỉ lệ (rescaling)" trên mặt trang (từ khóa mạch) | bài học deck 01 |
| 3-00 | Ghi chú diễn giả bỏ "Mạch …", "Kết quả trao cho mạch sau" | L17(d), (e) |
| 3-01 | Dòng đầu là câu nối mạch 2→3: "Chiều VC đếm cách gán nhãn; hàm điểm số, hàm lỗi cần đại lượng cho giá trị thực."; "Nhắc lại" Định lý 03.15 vào ghi chú diễn giả; $\Pr(\sigma_i=\pm1)=\tfrac12$ | T6 |
| 3-02 | Tiêu đề "Ví dụ: bốn lớp trên ba điểm"; công thức tính vào ghi chú diễn giả; Bổ đề 07.8 có "Giả thiết:"/"Bảo đảm:", đặt cuối trang vì ví dụ chỉ dùng định nghĩa ở trang trước còn bổ đề là công cụ cho mạch 4–5 | chống tràn; L6 |
| 3-03 | "Trực quan." chỉ còn mức tham chiếu (hàm cố định sai trung bình nửa số nhãn); cơ chế chọn hàm ở ghi chú diễn giả; (b), (c) rút gọn | T2, trần 60 |
| 3-04 | `<ol>`; bước 1 ghi giả thiết "$h$ nhận giá trị trong $\{0,1\}$"; bỏ "Ý nghĩa cho học:" | T8, L18 |
| 3-06 | Nhãn "Bài tập 07.2(c)."; bảng ngang; câu "phần chênh là độ phức tạp" vào ghi chú diễn giả (theo L14 câu cũ dễ hiểu sai) | chống chạm chân trang; L14 |
| 4-00 | Câu dẫn mạch "Với lớp hàm lỗi chọn trước, độ phức tạp Rademacher thực nghiệm chặn khoảng cách tổng quát hóa với xác suất cao." (21) | L15 |
| 4-01 | "Trực quan." nêu cơ chế (biết thêm từng biến, kì vọng có điều kiện dịch ít; bổ đề Hoeffding chặn từng bước); tên tiếng Anh trong dòng bổ đề; $\Psi$ chuyển sang 4-03, $L_D(g)$, $L_S(g)$ sang 4-02 | T3; mục 11, điểm 9; trần 60 |
| 4-02 | Tiêu đề "Cận theo độ phức tạp Rademacher thực nghiệm" (một dòng); "Kí hiệu:" $L_D(g)$, $L_S(g)$ trong dòng giả thiết | chống chạm chân trang; trần 6 dòng |
| 4-03 | `<ol>`; $\Psi$ định nghĩa ở dòng "Kí hiệu:"; bất đẳng thức cuối là công thức hiển thị; ghi chú diễn giả thêm L3 (bỏ (T3) hỏng bước 3) và L4 (mẫu lân cận của Bài 06) | T8, L3, L4 |
| 4-04 | Câu nối mạch 4→5 trên mặt trang: "**Diễn giải:** … cần lớp nhỏ hơn vẫn chứa hàm do huấn luyện chọn" | bài học deck 01 |
| 4-05 | Nhãn "Bài tập 07.2(b)."; câu hỏi gộp một dòng | trần 60 |
| 5-01 | Dòng "Không phụ thuộc $p$, giảm như $1/\sqrt m$, tỉ lệ với $B$" vào ghi chú diễn giả ("không phụ thuộc $p$" còn ở "Trực quan.") | trung vị |
| 5-02 | `<ol>`; "bất đẳng thức duy nhất của cận thứ nhất" vào ghi chú diễn giả | T8, L5 |
| 5-03 | Tên tiếng Anh ở dòng bổ đề; "Lưu ý:" rút gọn | trần 60 |
| 5-04 | **Dòng lề chuẩn hóa chuyển sang 6-03**; lưới `grid2` 3:2 (kiểu nội tuyến; màn hẹp vẫn một cột nhờ `!important` của `lecture-course.css`); nhãn hình "1[t < γ]" thay "cận trên" | T2; chống chạm chân trang |
| 5-05 | Dòng cuối "đúng cho đầu ra $\lVert\hat w\rVert\le B$ của mọi thuật toán" | trung vị |
| 5-06 | `<ol>`; $\widehat{\mathfrak R}_S(\mathcal F_B)$ | T8, L7 |
| 6-00 | Ghi chú diễn giả bỏ "Hai trang cuối …" | L17(c) |
| 6-01 | Tiêu đề "Ví dụ: phân lớp văn bản"; bảng cỡ mẫu xoay ngang; cận VC thành dòng "Diễn giải:" cuối trang | chống tràn khung |
| 6-02 | "trái giả thiết của Hệ quả 07.16"; "lưới", "trọng số" trên mặt trang; dòng "Thêm $\ln(k(k+1))$" vào ghi chú diễn giả | L9, L10, cắt mục 5 |
| 6-03 | **Bỏ hình F3**: ba dòng dữ kiện, bảng bốn cột (trung bình, $\min$ – $\max$, lề chuẩn hóa) và "Diễn giải:" đã chiếm hết khung; với hình, trang tràn $\approx150$ px ở 1600×900, còn hình thu nhỏ có chữ dưới $12$ px; mọi số của hình nằm trong bảng; trang thêm dòng lề chuẩn hóa từ 5-04 | chống tràn; trần 55 trang không cho trang thêm |
| 6-04 | Khoảng số hạng viết "$75$–$372$"; "$B$ chọn theo $S$: cần lưới …"; "Diễn giải:" nêu bán kính $0{,}0193$ | trung vị |
| 6-05 | Bước 1 của Ví dụ 07.11 gộp vào dòng dữ kiện; "$\lVert x\rVert\le C_x$" ở dòng hàm lỗi logistic; Bổ đề 07.8 nêu ở ghi chú diễn giả | T2, L11 |
| 6-06 | Theo N2: "Với (T1)" (nhãn của giả thiết quan sát độc lập cùng phân bố, đặt ở 2-01), giữ $\ln\bar N$ trong $\tilde O(\cdot)$, dòng "**Kí hiệu:**" định nghĩa $r_j$, $M_j$, $\bar N$, $\hat y_\Theta$; dòng cuối "Ngoài thừa số lôgarit, cận không phụ thuộc số tham số." (câu nối 6→7); "Chứng minh nằm ngoài phạm vi học phần" và "$R_\Theta$ đóng vai $B$" vào ghi chú diễn giả; $b_j=0$ thay "không hệ số tự do" | N2; trần 60 |
| 7-01, 7-02 | Bỏ "(đầy đủ)/(phác thảo)" khỏi cột cuối (vào ghi chú diễn giả); hàng Mệnh đề 07.2 theo giả thiết của ghi chú ("$J=2$, $N_1=2$, ReLU, tham số cho trước; chỉ $x\in\{0,1\}^2$"); tách hai trang (mục 16.1) | N1, T5 |
| 7-03 | Dòng đầu trả lời thẳng câu hỏi trung tâm; bốn dòng; "báo lỗi trên tập kiểm tra" ở ghi chú diễn giả | T7, trần 60 |
| 7-04 | "Kiểm giả thiết, tính $r_m$ của Định lý 02.14(a)" | trần 60 |
| 7-05 | "ba hàm", $r_m=\sqrt{\ln(2\cdot3/\delta)/(2m)}$, không đặt $K$ | quyết định điều phối viên (mục 11.21) |
| 7-07 | Liên kết "Ghi chú bài giảng · Bài tập" ở trang bài tập về nhà (như deck Bài 06) | thống nhất deck 06 |
| 7-08 | Dòng Bài 08 là chữ thường, chưa liên kết | bản giao việc |

### 16.3 Công thức rộng ở 390 px

Đã ngắt `aligned`: 2-03 (hai dòng), 2-04. Còn cuộn ngang tại chỗ ở 390 px (chế độ đọc màn hẹp cho phép): 4-02 (b), 5-01, 5-05, 6-02, 6-06; ngắt các công thức này làm trang 1600×900 chạm chân trang (đã thử: 5-01 tới $954$ px, 5-05 tới $964$ px, 6-02 tới $878$ px so với chân trang $863$ px). Bảng 1-06, 3-02, 3-06, 6-03, 7-01, 7-02 cuộn ngang tại chỗ.

### 16.4 Kỹ thuật (mục 14) trong deck cuối

Không đổi so với mục 14: "Kỹ thuật." một dòng ở 2-05, 3-04, 5-06; "Nhắc lại:" đối xứng hóa và mẫu bóng ở 4-03, chia xác suất thất bại theo trọng số ở 6-02; sai phân của cận trên đúng ở ghi chú diễn giả 4-03.

### 16.5 Mật độ mặt trang và ghi chú diễn giả của deck cuối (đếm theo `deck_lint.py`)

| Trang | Mặt trang | Ghi chú diễn giả |
|---|---:|---:|
| 1-01 | 72 | 138 |
| 1-02 | 57 | 115 |
| 1-03 | 79 | 124 |
| 1-04 | 47 | 91 |
| 1-05 | 23 | 130 |
| 1-06 | 59 | 147 |
| 2-00 | 23 | 87 |
| 2-01 | 52 | 125 |
| 2-02 | 60 | 102 |
| 2-03 | 43 | 81 |
| 2-04 | 47 | 76 |
| 2-05 | 46 | 125 |
| 2-06 | 60 | 134 |
| 2-07 | 48 | 148 |
| 2-08 | 57 | 130 |
| 2-09 | 57 | 126 |
| 2-10 | 51 | 79 |
| 2-11 | 51 | 125 |
| 3-00 | 24 | 113 |
| 3-01 | 53 | 141 |
| 3-02 | 49 | 114 |
| 3-03 | 60 | 97 |
| 3-04 | 45 | 141 |
| 3-05 | 52 | 81 |
| 3-06 | 45 | 108 |
| 4-00 | 22 | 79 |
| 4-01 | 60 | 149 |
| 4-02 | 55 | 97 |
| 4-03 | 51 | 225 |
| 4-04 | 48 | 114 |
| 4-05 | 56 | 118 |
| 5-00 | 24 | 81 |
| 5-01 | 43 | 94 |
| 5-02 | 21 | 151 |
| 5-03 | 56 | 133 |
| 5-04 | 45 | 96 |
| 5-05 | 49 | 94 |
| 5-06 | 45 | 156 |
| 5-07 | 57 | 92 |
| 6-00 | 22 | 112 |
| 6-01 | 28 | 102 |
| 6-02 | 54 | 95 |
| 6-03 | 46 | 110 |
| 6-04 | 51 | 107 |
| 6-05 | 47 | 145 |
| 6-06 | 56 | 150 |
| 7-00 | 21 | 91 |
| 7-01 | 47 | 127 |
| 7-02 | 43 | 105 |
| 7-03 | 58 | 148 |
| 7-04 | 55 | 143 |
| 7-05 | 60 | 115 |
| 7-06 | 51 | 130 |
| 7-07 | 36 | 114 |
| 7-08 | 57 | 149 |

## 17. Sửa sau năm báo cáo duyệt (người sửa, 2026-11-16)

Đầu vào: `reviews/deck-{hoc-vien,toan-hoc,chuyen-gia,su-pham,mach-truyen}.md`; quyết định của điều phối viên trong `review-log.md` (mục "Năm báo cáo duyệt và quyết định của điều phối viên"). Bản đóng băng trước khi sửa lưu ở thư mục nháp `editor/frozen-before-edit.html`. Viết tắt người duyệt: HV học viên, TH toán học, CG chuyên gia, SP sư phạm, MT mạch truyện. Mã trang và số trang (55) không đổi. Kiểm tra sau sửa: `deck_lint.py` 0, `footer_check.py` 0, `deck_check.py` console 0, pageerrors 0, failed 0, không `.katex-error`, OVERFLOW còn lại $\le5$ px ở trang có $\sqrt{\ }$; phím →, ↓, Space, Esc và `#/2`…`#/7` đúng.

### 17.1 Phát hiện nghiêm trọng

| Phát hiện | Trang | Xử lý |
|---|---|---|
| HV, MT P1 (TH, SP trung bình; CG nhẹ): Định lý 02.14(a), $r_m$, (T4) chưa nhắc lại | 7-04, 7-05 | đã sửa: 7-04 mở bằng "**Nhắc lại:** Định lý 02.14(a), (T1), (T3), (T4) lớp hữu hạn chọn trước: với xác suất ít nhất $1-\delta$, $\sup_h\lvert L_S-L_D\rvert\le r_m=\sqrt{\ln(2\lvert\mathcal H\rvert/\delta)/(2m)}$"; 7-05 viết "(T4) với $\lvert\mathcal H\rvert=3$"; đề 7-04 rút gọn để giữ trần 60 |
| CG (TH, HV, SP trung bình/nhẹ): "Diễn giải:" 3-02 khái quát sai | 3-02 | đã sửa: "$1$, $2$, $4$, $8$ véc-tơ cho $0$, $1/4$, $1/3$, $1/2$; $\{0,1\}^3$ khớp mọi bộ dấu"; phản ví dụ $0{,}1\cdot\{0,1\}^3$ ($0{,}05$) ở ghi chú diễn giả |

### 17.2 Phát hiện trung bình

| Phát hiện | Trang | Xử lý |
|---|---|---|
| HV: 3-02 không cho tám giá trị lớn nhất, không ghi chia $24$ | 3-02 | đã sửa: "$\widehat{\mathfrak R}(A)={}$tổng$/24$" trên mặt trang; hai dãy $-1,0,0,2,1,1,1,2$ và $0,1,0,2,0,1,1,3$ ở ghi chú diễn giả |
| HV: bảng ở 390 px cắt ô số | 1-06, 3-02, 4-04, 6-01, 6-03, 7-01, 7-02 | không sửa trong deck: điều phối viên xử lý bằng CSS chung (commit 3876170) |
| HV, CG, MT P2, SP: 7-03 thiếu phạm vi, "nó", dòng lớp tuyến tính thiếu xác suất và đại lượng; CG, TH: "lớp chứa mô hình" | 7-03 | đã sửa: bốn dòng — độ phức tạp của lớp hàm lỗi bị chặn trên lớp chọn trước chứa mô hình do huấn luyện chọn; với (T1), xác suất $\ge1-\delta$, đại lượng này chặn khoảng cách tổng quát hóa; lớp tuyến tính, lớp ẩn cố định, xác suất $\ge1-\delta$, công thức đủ của Hệ quả 07.16, không chứa $p$; ở $m=200$ cận $>1$, lỗi báo trên tập kiểm tra, cận không giải thích chuẩn nhỏ. Viết "$\ge1-\delta$" bằng công thức và bỏ "mọi hàm", "$11{,}85$" để giữ trần 60; lề chuẩn hóa và giới hạn mạng sâu ở ghi chú diễn giả |
| CG, TH: bìa "lớp chứa mô hình" | 1-01 | đã sửa: "độ phức tạp Rademacher của lớp hàm lỗi bị chặn ứng với lớp chứa mô hình do huấn luyện chọn, với xác suất cao, chặn …" (một câu; SP nhẹ về hai động từ liền nhau cũng được sửa bằng dấu phẩy) |
| HV, SP: 5-03 "Lưu ý:" khó đọc | 5-03 | đã sửa: "không cần $\phi_i(0)=0$. Với định nghĩa có trị tuyệt đối $\mathbb E\sup\lvert\cdot\rvert$, bổ đề cần điều kiện này: $A=\{0\}$, $\phi_i\equiv1$ đổi $0$ thành $0{,}5$." |
| HV: 1-02 kí hiệu chưa giải nghĩa; MT P8: $d$ | 1-02 | đã sửa: "$\Pi_{\mathcal H}$ hàm tăng trưởng", "$d(\mathcal H^p_{\mathrm{aff}})=p+1$", "$\tilde h$ hàm trả về, $L^*$ rủi ro tham chiếu"; $\operatorname{opt}_S$ và (M) giải nghĩa ở ghi chú diễn giả; (M) có tên "lớp con đếm được" ở 2-01; "$G$-Lipschitz (Định nghĩa 05.4)" chuyển xuống 5-03, nơi dùng |
| HV: dòng > 20 âm tiết | 2-04, 2-06, 3-06, 4-05 | đã sửa: 2-04 tách "Trực quan." hai dòng; 2-06 Nhận xét 07.3 rút còn 18; 3-06 và 4-05 tách "Câu hỏi:"; còn dòng 21–23 ở 2-01, 7-03, 7-04 (gộp để giữ $\le6$ dòng) |
| TH: 7-06 câu 3 thiếu (T1) và "$B$, $\gamma$ chọn trước" | 7-06 | đã sửa; câu 4 bỏ "để chặn rủi ro 0–1" để giữ trần 60 |
| CG: 6-06 "không phụ thuộc số tham số" mạnh hơn nguồn | 6-06 | đã sửa theo câu của quyết định: "Số tham số không xuất hiện trực tiếp; độ sâu, độ rộng vào cận qua $R_\Theta$"; ghi chú diễn giả thêm "$\tilde O$ ẩn thừa số lôgarit", độ sâu qua tích và tổng theo $j$, cận không cho biết vì sao huấn luyện chọn $R_\Theta$ nhỏ. Đề xuất sửa ghi chú do điều phối viên ghi |
| SP: 2-06 "ba năng lực" gồm tối ưu, cột "Số hạng" | 2-06 | đã sửa: tiêu đề "Ba câu hỏi về một lớp mạng"; cột "Câu hỏi \| Số hạng (Mệnh đề 04.3)"; hàng "năng lực biểu diễn", "năng lực thống kê", "khả năng tối ưu"; CG nhẹ "cần số nơ-ron mũ theo $p$" |
| SP: 2-09 hệ quả của $B=\lVert\hat\theta\rVert$ | 2-09 | đã sửa: "lấy $B=\lVert\hat\theta\rVert$ thì lớp phụ thuộc $S$, trái (T5)" |
| SP, MT P3: số hiệu Ví dụ trên trang nguồn | 2-10, 2-11, 3-02, 3-05, 4-04, 6-01, 6-03, 6-04, 6-05 | đã sửa: nhãn "**Ví dụ 07.2.**", "07.3", "07.4", "07.5", "07.6", "07.8", "07.10", "07.10 (tiếp)", "07.11" |
| SP: 3-03 "Trực quan." chưa nêu cơ chế | 3-03 | đã sửa: "Lớp chọn, với mỗi bộ nhãn ngẫu nhiên, hàm sai ít nhất."; mức tham chiếu một hàm cố định và "phần lỗi dưới $\tfrac12$ là độ phức tạp" ở ghi chú diễn giả (trần 60) |
| SP: 6-03 "Diễn giải:" thiếu chiều so sánh | 6-03 | đã sửa: "chuẩn trung bình với nhãn hoán vị gấp … lần với nhãn thật" |
| SP: 7-04 không nhắc lại Định lý 02.14 | 7-04 | đã sửa (xem 17.1) |
| MT P4: câu nối 2-07→2-08 | 2-08 | đã sửa: dòng mở "Số tham số là thước đo đầu tiên của lớp."; câu "số hạng $2r$ đo năng lực thống kê" ở ghi chú diễn giả (trần 60) |
| MT P5: câu nối 2→3 thiếu vế "nhỏ đi khi bị chặn theo chuẩn" | 3-01 | đã sửa: "Hàm giá trị thực cần đại lượng thay chiều VC, nhỏ đi khi bị chặn theo chuẩn." |
| MT P6: 2-01 lý do cận Bài 06 không dùng được | 2-01 | đã sửa: "không cần tính lồi, khác Bài 05–06"; lý do ở ghi chú diễn giả |

### 17.3 Phát hiện nhẹ

| Phát hiện | Trang | Xử lý |
|---|---|---|
| HV: mật độ, trung vị 51 | toàn deck | không sửa: các phát hiện yêu cầu thêm chữ; mọi trang $\le60$, trung vị nay $56$ |
| HV, TH: 4-03 bước 2 thiếu biểu thức; (T1) ở bước 4 | 4-03 | đã sửa; bất đẳng thức cuối đưa vào bước 4 (bỏ công thức hiển thị) để trang không tràn |
| HV, SP: 5-02 Ví dụ 07.7 thiếu $p$, $m$, tên cận; câu cuối ghi chú lặp | 5-02 | đã sửa |
| HV: 4-05 thiếu công thức Hệ quả 02.10(c) | 4-05 | đã sửa: "Hệ quả 02.10(c): $\sqrt{\ln(1/\delta)/(2m)}=\sqrt{\ln20/400}\le0{,}0866$"; "một lần với $\delta$ cho đúng Hệ quả 02.10(c)" chuyển vào ghi chú diễn giả (trần 60) |
| HV: 6-05 thiếu kết luận | 6-05 | đã sửa: "**Kết luận:** Định lý 07.11 cần lớp hàm lỗi trong $[0,1]$, không phải lớp điểm số."; cận logistic (với $K$) chuyển vào ghi chú diễn giả |
| HV: 1-06 quan hệ $f$, $w$; lớp ẩn rút ngẫu nhiên | 1-06 | đã sửa: "$\psi_j$ rút ngẫu nhiên", "$f=\frac1{\sqrt N}\sum_jw_j\psi_j$" |
| HV, TH: 3-02 "$A$ như trên"; bổ đề dùng ở đâu | 3-02 | đã sửa: "$A\subset\mathbb R^m$ khác rỗng, bị chặn"; nơi dùng ở ghi chú diễn giả |
| HV: 3-05 "Theo (b)" | 3-05 | đã sửa: "Theo Mệnh đề 07.9(b)" |
| HV, SP: 4-01 "dịch ít", đối tượng | 4-01 | đã sửa: "Cận trên đúng theo lớp hàm lỗi …"; "Biết thêm $V_i$, kì vọng có điều kiện của $Q$ dịch $\le c_i$" |
| HV: 5-03 thiếu "Trực quan." | 5-03 | không sửa: trang ở trần 60 sau khi sửa "Lưu ý:"; cơ chế (Phụ lục B) ở ghi chú diễn giả |
| HV: 6-06 $\mu_\Theta$, $\lVert\cdot\rVert_{2,1}$, $\tilde O$ | 6-06 | đã sửa một phần: $r_j$, $M_j$, $\bar N$ ở "Kí hiệu:" trên mặt trang; $\mu_\Theta$, $\hat y_\Theta$, $\lVert\cdot\rVert_{2,1}$, $\tilde O$ ở ghi chú diễn giả (thêm chữ làm trang tràn khung) |
| HV, TH: 2-07 $F(\theta)=0$, $\theta$ của Mệnh đề 07.2 | 2-07 | đã sửa |
| HV: 5-04 nhãn SVG nhỏ | 5-04, `ham-loi-doc.svg` | đã sửa: chữ SVG $22\to26$; chú thích nêu kiểu nét của từng đường |
| HV, SP: 7-04 câu (c) tách đôi, thiếu "Câu hỏi:" | 7-04 | đã sửa |
| TH: 1-05, 3-00 thiếu kì vọng; "số hạng phạt" | ghi chú 1-05, 3-00 | đã sửa |
| TH, SP: $\gamma>0$, $k\ge1$, $J\ge2$ | 5-04, 6-02, 2-03 | đã sửa |
| TH: Nhận xét 07.6 "kể cả hệ số tự do" | ghi chú 2-11 | đã sửa |
| TH, CG: 6-04 trung bình so với từng lần chạy | 6-04 | đã sửa: "lỗi trung bình $0{,}023$; mỗi lần chạy, Hệ quả 02.10(b) cho bán kính …" |
| TH, SP: 6-01 hằng số $4{,}0743$ | 6-01 | đã sửa: công thức viết $3\sqrt{\ln40/2}$, kèm $\approx4{,}0743$ |
| CG: 2-01 đối tượng so sánh | ghi chú 2-01 | đã sửa |
| CG, SP: 2-10 kết luận đổi tỉ lệ | 2-10 | đã sửa: "nên chuẩn tham số không xác định từ hàm" |
| CG: 2-06 cận dưới số nơ-ron | 2-06 | đã sửa: "cần số nơ-ron mũ theo $p$" |
| CG: 4-03 khác Bài 03 (Chebyshev) | ghi chú 4-03 | đã sửa |
| CG: 3-01 $\widehat{\mathfrak R}_S$ ngẫu nhiên theo $S$ | ghi chú 3-01 | đã sửa |
| CG: 4-00 dòng dẫn bỏ "bị chặn" | 4-00 | đã sửa (23 âm tiết) |
| CG: 1-05, 7-08 ghi chú đọc rộng hơn ghi chú | ghi chú 1-05, 7-08 | đã sửa: "lớp tuyến tính bị chặn theo chuẩn (mạng có lớp ẩn cố định)"; "với lớp ẩn cố định, … hạ gradient trên hàm bình phương theo $w$" |
| SP: hai dấu hai chấm liền | 1-02, 2-08, 4-04, 6-02 | đã sửa |
| SP: Mục tiêu 5 chuỗi danh từ | 1-03 | không sửa: viết đủ ba ý "vì sao" làm trang vượt trần 80 (đếm $\approx94$); ba ý ở ghi chú diễn giả |
| SP: tiếng Anh ở lần đầu ("score function" ở 1-06; "Thực nghiệm (empirical):"; ERM) | 1-06, 3-01, 2-01, 7-04 | đã sửa 3-01 (không còn dạng nhãn) và ghi chú 2-01 (tên đầy đủ ERM, SGD); không sửa 1-06 ("score function" ở 2-01; 1-06 ở trần 60) và "ERM" trên mặt trang 7-04 (chữ viết tắt dùng từ Bài 01, mục 10 của storyboard) |
| SP: 1-06 cột "trung bình", "$\min$ – $\max$" | 1-06, 6-03 | đã sửa: "Lỗi kiểm tra trung bình" (1-06); "Nhỏ nhất – lớn nhất" (6-03); 1-06 giữ "$\min$ – $\max$" vì trần 60, nghĩa giải ở ghi chú diễn giả |
| SP: 2-00 dòng dẫn | 2-00 | đã sửa: "Mạng ReLU nhỏ biểu diễn được phép hoặc loại trừ, lớp afin thì không; số tham số không phân biệt hai loại nhãn." |
| SP: 2-02 "Câu hỏi:" thiếu chủ ngữ | 2-02 | đã sửa: "$w$ của bộ giải, …"; "Định lý 03.15" thành "cận VC" để giữ trần |
| SP: ghi chú 2-05, 2-06 dấu hai chấm, lặp, thứ tự số hạng | ghi chú 2-05, 2-06 | đã sửa |
| SP: ghi chú 2-08 hai ý một câu | ghi chú 2-08 | đã sửa |
| SP: 3-02 "Diễn giải:", "hợp" | 3-02 | đã sửa (17.1) |
| SP: 3-03 (b) cụt | 3-03 | đã sửa: "với mọi nhãn cố định, lớp hàm lỗi 0–1 có cùng giá trị" |
| SP: 3-04 bước 2 | 3-04 | đã sửa |
| SP: 4-02 ghi chú lặp mặt trang; nghĩa vận hành | 4-02 | đã sửa: ghi chú nêu "95 trên 100 lần", khác biệt (a)/(b); "Trực quan." nói hệ quả (cận không cho thông tin); "không chứa $p$" chuyển vào ghi chú diễn giả (trần 60) |
| SP: ghi chú 4-04 thiếu mắt xích | ghi chú 4-04 | đã sửa |
| SP: ghi chú 5-01, 5-05, 5-06, 6-00 lặp ý | ghi chú 5-06, 6-00 | đã sửa (bỏ câu cuối 5-06; 6-00 mở bằng phân lớp văn bản) |
| SP: 6-01 hằng số, nhãn "Diễn giải:" | 6-01 | đã sửa: dòng so cận VC không nhãn |
| SP: 6-04 "Diễn giải:" lặp số | 6-04 | đã sửa |
| SP: ghi chú 7-00, 7-04 lặp câu | ghi chú 7-00 | đã sửa |
| SP: "câu ôn nhanh 1/2/3" không đánh số | ghi chú 1-02, 2-11, 3-06, 4-04, 5-03 | đã sửa: đánh số (1)–(3) ở 1-02 |
| SP: chủ ngữ văn bản, câu nguồn gốc | ghi chú 1-03, 6-03, 6-06, 7-07, 7-08 | đã sửa |
| MT P7: "Đọc thêm" nêu Nhận xét 07.6 | 7-02 | đã sửa: chỉ còn Nhận xét 07.18 |
| MT P9: 6-05 không dẫn Bổ đề 07.8 | 6-05 | đã sửa |
| MT P10: 6-01 không nói trả lời câu hỏi văn bản | 6-01 | đã sửa: "Bảo đảm cho câu hỏi phân lớp văn bản (Hệ quả 07.16)" |
| MT P11: bổ đề Hoeffding chưa nhắc | 1-02 | đã sửa: "Hoeffding (Bổ đề 02.6, Định lý 02.7)" |
| MT P12: 2-10 hệ quả | 2-10 | đã sửa |
| MT P13: ghi chú 7-08 thiếu câu Bài 06 | ghi chú 7-08 | đã sửa |
| CG: 7-04, 7-05 Định lý 02.14 | 7-04 | đã sửa (17.1) |

### 17.4 Mật độ sau sửa (đếm theo `deck_lint.py`)

| Trang | Mặt trang | Ghi chú diễn giả |
|---|---:|---:|
| 1-01 | 75 | 138 |
| 1-02 | 59 | 133 |
| 1-03 | 79 | 122 |
| 1-04 | 47 | 91 |
| 1-05 | 23 | 141 |
| 1-06 | 60 | 145 |
| 2-00 | 23 | 87 |
| 2-01 | 59 | 143 |
| 2-02 | 60 | 98 |
| 2-03 | 43 | 81 |
| 2-04 | 48 | 76 |
| 2-05 | 46 | 98 |
| 2-06 | 60 | 137 |
| 2-07 | 55 | 148 |
| 2-08 | 58 | 142 |
| 2-09 | 58 | 126 |
| 2-10 | 60 | 79 |
| 2-11 | 54 | 138 |
| 3-00 | 24 | 116 |
| 3-01 | 58 | 150 |
| 3-02 | 46 | 138 |
| 3-03 | 60 | 103 |
| 3-04 | 44 | 141 |
| 3-05 | 57 | 81 |
| 3-06 | 43 | 108 |
| 4-00 | 24 | 79 |
| 4-01 | 59 | 149 |
| 4-02 | 59 | 87 |
| 4-03 | 46 | 246 |
| 4-04 | 52 | 121 |
| 4-05 | 52 | 118 |
| 5-00 | 24 | 81 |
| 5-01 | 43 | 94 |
| 5-02 | 22 | 136 |
| 5-03 | 59 | 144 |
| 5-04 | 48 | 96 |
| 5-05 | 49 | 94 |
| 5-06 | 45 | 129 |
| 5-07 | 57 | 92 |
| 6-00 | 22 | 95 |
| 6-01 | 38 | 102 |
| 6-02 | 54 | 95 |
| 6-03 | 60 | 96 |
| 6-04 | 60 | 107 |
| 6-05 | 58 | 149 |
| 6-06 | 44 | 146 |
| 7-00 | 21 | 79 |
| 7-01 | 47 | 127 |
| 7-02 | 42 | 105 |
| 7-03 | 59 | 150 |
| 7-04 | 60 | 143 |
| 7-05 | 58 | 115 |
| 7-06 | 52 | 130 |
| 7-07 | 36 | 102 |
| 7-08 | 57 | 150 |

### 17.5 Lượt 2 (theo `reviews/deck-kiem-lai-1.md`, 2026-11-16)

| Phát hiện | Trang | Xử lý |
|---|---|---|
| K1 | 7-03 | đã sửa: "Lớp ẩn cố định, $B,\gamma$ chọn trước, xác suất $\ge1-\delta$, $\forall\lVert w\rVert\le B$: $L_D(h_{w,0})\le L^{<\gamma}_S(h_w)+\dots$, không chứa $p$"; dòng 4 bỏ chữ "cận" thứ hai |
| K2 | 2-06 | đã sửa: "Nhận xét 07.3 (xấp xỉ phổ quát, universal approximation). Mạng sigmoid xấp xỉ đều mọi hàm Lipschitz …, sai số $\epsilon$; cần số nơ-ron mũ theo $p$."; dòng cuối "Kết quả chỉ chặn số hạng đầu."; cột "Mệnh đề 04.3" thay "Số hạng (Mệnh đề 04.3)" để giữ trần 60; không còn dấu phẩy rơi dòng ở 1600×900 |
| K3 | 1-02 | đã sửa: "(M) lớp con đếm được"; bù bằng "Định lý 03.15, (T1), …" và "Mệnh đề 04.3, $S$ $r$-đại diện:" |
| K4 | 1-06 | đã sửa: "rút ngẫu nhiên rồi cố định"; bù: "Nhãn hoán vị (permuted labels) của tập huấn luyện", tiêu đề cột "Lỗi kiểm tra" (chữ "trung bình" chuyển vào ghi chú diễn giả, ngược sửa nhẹ SP ở lượt 1, vì trần 60) |
| K5 | 2-07 | đã sửa: "$f_\theta(x_i)=\tilde y_i/2$, $i=1,\ldots,4$" |
| K6 | 2-08 | đã sửa: "Thước đo đầu tiên cho số hạng $2r$ là số tham số."; dòng cuối "Tham số hóa thừa và nội suy không kéo theo nhau."; bù: "$\mathcal H_{\sin}$ có $P=1$, $d=\infty$; lớp $p$ tham số, ba hàm" |
| K7 | 2-09 | đã sửa: "trái với (T5)" |
| K8 | 3-01 | đã sửa: "Lớp hàm giá trị thực cần một đại lượng thay chiều VC; đại lượng này nhỏ đi khi lớp bị chặn theo chuẩn."; bù ở "Trực quan." và dòng tên hai độ phức tạp |
| K9 | 4-05 | đã sửa: "So sánh với Hệ quả 02.10(c). Bước nào làm cận yếu hơn?" |
| K10 | 4-03, 4-01 | đã sửa: 4-03 bước 4 đặt bất đẳng thức trước, "với $t=\dots$" ở cuối; 4-01 "… $\big)$. Đuôi dưới cũng vậy." |
| K11 | 7-06 | đã sửa: khôi phục "để chặn rủi ro 0–1" |
| K12 | 7-03 | đã sửa: "bị chặn ứng với lớp chọn trước" |
| K13 | 6-06 | đã sửa: "Kí hiệu:" thêm "$\bar N$ lớn nhất trong $p$, số nhãn, các $N_j$; $\hat y_\Theta$ nhãn dự đoán"; dòng cuối "… vào cận qua $R_\Theta$ và $\ln\bar N$" |
| K14 | ghi chú 4-02 | đã sửa theo câu đề xuất ($3t$ gồm $t$ và $2t$) |
| K15 | 6-03 | đã sửa: "hai khoảng chuẩn không giao nhau"; nhãn "Ví dụ 07.k." trong gạch đầu dòng giữ nguyên (đặt `<p>` riêng thêm một dòng trên các trang đã ở 5–6 dòng) |
| Mục 6, cắt mật độ | 1-06, 2-01, 2-02, 2-10, 4-01, 4-02, 6-03, 6-04, 7-04 | đã áp dụng đúng câu đề xuất; 1-02, 2-06, 7-03 theo K3, K2, K1; 3-03, 5-03 giữ |

Kiểm tra lượt 2: `deck_lint.py` 0; `footer_check.py` 0; `deck_check.py --shots` trên 20 trang đổi: console 0, pageerrors 0, failed 0, không `.katex-error`, không OVERFLOW > 5 px; đã xem ảnh 1600×900 và 390×844 (cả `-end`) của 20 trang; phím và `#/N` đúng. Trung vị trang nội dung: 55.

| Trang đổi | Mặt trang | Ghi chú diễn giả |
|---|---:|---:|
| 1-02 | 60 | 133 |
| 1-06 | 60 | 145 |
| 2-01 | 55 | 143 |
| 2-02 | 56 | 98 |
| 2-06 | 60 | 137 |
| 2-07 | 52 | 148 |
| 2-08 | 60 | 142 |
| 2-09 | 59 | 126 |
| 2-10 | 57 | 79 |
| 3-01 | 59 | 150 |
| 4-01 | 57 | 149 |
| 4-02 | 55 | 101 |
| 4-03 | 47 | 246 |
| 4-05 | 53 | 118 |
| 6-03 | 59 | 96 |
| 6-04 | 59 | 107 |
| 6-06 | 54 | 146 |
| 7-03 | 58 | 150 |
| 7-04 | 59 | 143 |
| 7-06 | 57 | 130 |

### 17.6 Lượt 3 (theo `reviews/deck-kiem-lai-2.md`, 2026-11-16)

| Phát hiện | Trang | Xử lý |
|---|---|---|
| N1 | 2-08 | đã sửa: dòng "Nhắc lại:" chuyển xuống sau Định nghĩa 07.4 (dùng $P$ sau khi định nghĩa), ghi lại "lớp (iii) $p$ tham số, ba hàm"; câu mở "Thước đo đầu tiên cho số hạng $2r$: số tham số." (60) |
| N2 | 2-01 | đã sửa: "Cần chặn $\sup_{h\in\mathcal H}(L_D(h)-L_S(h))$; cận này chặn cả rủi ro đầu ra $A(S;\xi)$ của mọi thuật toán." (bỏ "của" để giữ 60) |
| N3 | 7-03 | đã sửa: "…; cận không giải thích chuẩn nhỏ." (59) |
| N4 | 1-06 | đã sửa: "$\lVert w\rVert$ nhỏ nhất thỏa $f(x_i)=2y_i-1$"; bù "$\psi_j$ rút ngẫu nhiên, cố định" (60) |
| N5 | 4-01, 7-06 | đã sửa: 4-01 dấu chấm đưa vào KaTeX ("…\big).$ Đuôi dưới cũng vậy."); 7-06 bọc "0–1?" trong `white-space:nowrap` |

Kiểm tra lượt 3: `deck_lint.py` 0; `footer_check.py` 0; `deck_check.py --ids L07-1-06,L07-2-01,L07-2-08,L07-4-01,L07-7-03,L07-7-06 --shots`: console 0, pageerrors 0, failed 0, không `.katex-error`, OVERFLOW ≤ 2 px (đuôi √); đã xem ảnh 1600×900 và 390×844 (cả `-end`) của sáu trang.
