# Storyboard — Bộ trang chiếu Bài 08: Tính ổn định của SGD và tổng quát hóa trong học sâu

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-11-16 bởi tác tử lập storyboard. Nguồn nội dung duy nhất: `materials/lec-08/lecture-note.md` (bản hiện hành); bài tập: `materials/lec-08/exercises.md`. Quy định: `CLAUDE.md` § Slide decks, `common-brief.md` (gồm "Các quy định dễ sót" và các bài học từ duyệt deck 01–05), `brief-storyboard.md`, `../rl-plan/CLAUDE.md` § Deck structure and content, nhật ký yêu cầu 2026-11-13 hàng 1–5, quyết định của điều phối viên trong `lec-0{1,…,6}/review-log.md` § Bộ trang chiếu, ba báo cáo `lec-0{4,5,6}/reviews/deck-storyboard-gate.md`. Khuôn bố cục theo storyboard Bài 06 và Bài 07; deck Bài 06 đã có làm mẫu markup (`<ol>` cho bước chứng minh, tiêu đề trang kỹ thuật là tên kỹ thuật). Mọi mã trang có dạng `L08-k-mm`; trong bảng viết gọn `k-mm`.

Số âm tiết trong tệp này đếm bằng script (mục 15) theo cách của `deck_lint.py`: token cách nhau bởi khoảng trắng có chữ cái hoặc chữ số, số viết trong câu có tính, KaTeX và số trong bảng không tính, mỗi công thức hiển thị tính một dòng. Điều phối viên đếm lại trên deck.

UML: không đọc PDF trong vai này (bản giao việc chỉ cho phép ghi chú và `exercises.md`). Các mục UML và bài báo của Hardt, Recht và Singer (2016) trên trang "Tài liệu tham khảo" lấy từ §13 của ghi chú; số trang PDF lấy từ `outline.md` §7 (UML §13.1–13.2 tr. 171–175, §20.6 tr. 277–278, §31.1 tr. 415–417; bài báo §2 tr. 4–6, §3.1–3.3 tr. 6–9, Phụ lục A tr. 31, §3.5 tr. 12–14, §4 tr. 14–17, §6–§7 tr. 19–28).

## 1. Tên tệp và tiêu đề

- **Tệp deck:** `2627-1/lecture-08-on-dinh-sgd-hoc-sau.html` (slug ASCII từ tên bài: "tính ổn định", "SGD", "học sâu"; theo mẫu `lecture-06-on-dinh-chinh-quy-hoa.html`).
- **Tiêu đề deck (h1 trang bìa):** "Tính ổn định của SGD và tổng quát hóa trong học sâu" (đúng tên bài của ghi chú).
- **`<title>`:** "Bài 08: Tính ổn định của SGD".
- **Chân trang:** "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài 08".
- **Liên kết viewer:** `material-viewer.html?doc=materials/lec-08/lecture-note.md&deck=lecture-08-on-dinh-sgd-hoc-sau.html` và `…exercises.md&deck=…`.
- **Màn hẹp:** chế độ đọc của `lecture-course.css` (`.slides` bọc trong `div.lecture-viewport`, script màn hẹp của `lecture-template.html`); bảng 1-06, 2-10, 7-01, 7-04, 7-06 đặt trong `.table-scroll`.
- **Trang cuối deck Bài 07** (7-07 của storyboard Bài 07) nhận liên kết tới tệp này khi deck Bài 08 xong.

## 2. Khung lý thuyết chung

**Vấn đề trung tâm (hộp "Vấn đề trung tâm", bằng lời, ≤ 30 âm tiết).** "**Câu hỏi:** thuật toán huấn luyện ảnh hưởng tới khoảng cách tổng quát hóa như thế nào?" (câu hỏi trung tâm của ghi chú, đoạn mở đầu dòng 5; `outline.md` §1; 17 âm tiết kể cả nhãn). Câu hỏi thật, không gợi câu trả lời; trang 7-02 trả lời.

**Luận điểm (trang bìa, một câu, có điều kiện, bằng lời).** "Với hàm lỗi lồi, trơn, có gradient bị chặn và độ dài bước không vượt hai lần nghịch đảo hằng số trơn, hai lần chạy hạ gradient ngẫu nhiên trên hai tập huấn luyện khác nhau một quan sát tách xa nhau chậm, nên khoảng cách tổng quát hóa kì vọng không vượt một hằng số nhân tổng các độ dài bước chia cho cỡ mẫu." (Mệnh đề 08.5, Định lý 08.6; §10 đoạn 1. Điều kiện ở vế đầu là (S), (G) và $\eta_t\le2/\beta$; "theo kì vọng" nằm trong tên đại lượng. 66 âm tiết theo script, bìa không tính trần. Bản ngắn ở mục 11, điểm 9.)

**Trọng tâm trực quan của deck.** Năm chỗ, theo yêu cầu của điều phối viên:
1. **Hai quỹ đạo trên hai tập huấn luyện khác một điểm tách xa chậm** (2-04, 2-05, 2-06 với hình F1, 3-01, 3-03): hai lần chạy dùng chung khởi tạo, độ dài bước và dãy chỉ số; khoảng cách $\Delta_t$ chỉ tăng ở bước khác biệt (xác suất $1/m$), mỗi lần không quá $2G\eta_t$, và không tăng ở bước chung. Số: Ví dụ 08.2 ($\Delta$: $0\to1$, $\tfrac34\to\tfrac74$ ở hai bước khác biệt; $1\to\tfrac34$, $\tfrac74\to\tfrac54$ ở bước chung); Ví dụ 08.4 ($\mathbb E\Delta_7\approx0{,}8705$ so với cận $1{,}5$).
2. **Bước gradient co giãn thế nào với hàm lồi, trơn** (2-07, 2-08, 2-09, 2-10, 2-11): một chiều, hệ số góc của $\Gamma(w)=w-\eta f'(w)$ là $1-\eta f''(w)\in[1-\eta\beta,1]$; tính lồi cho cận trên $1$, điều kiện $\eta\le2/\beta$ cho cận dưới $-1$. Bảng của Ví dụ 08.3: bậc hai, Huber, hàm lõm với $\eta\in\{\tfrac12,2,3\}$.
3. **Cái giá khi không lồi** (6-01 với hình F4, 6-02, 6-03, 6-05, 6-07): bước chung nhân khoảng cách với $1+\beta\eta$; hàm lỗi cosin của Ví dụ 08.8 đưa khoảng cách từ $0{,}0010$ tới $\pi$ sau một bước khác biệt; cận $275{,}6$ trên hàm lỗi trong $[0,2]$.
4. **Khoảng cách tổng quát hóa kì vọng theo số bước và độ dài bước** (1-06, 4-01, 4-03, 4-04 với hình F2, 4-05, 5-01, 5-03 với hình F3): cận $\frac{2G^2}m\sum_t\eta_t$ phụ thuộc quỹ đạo chỉ qua ngân sách độ dài bước; thí nghiệm mở đầu có cận $t/200$, bằng số vòng; đại lượng đo được tăng chậm hơn; ghép với cận tối ưu cho số bước tốt nhất $T^*\approx7071$ khi $\eta=0{,}05$.
5. **Giả thiết nào hỏng khi chuyển sang học sâu** (2-02, 6-06, 7-02, 7-03, 7-04): mạng ReLU huấn luyện mọi lớp nơ-ron không trơn, không lồi theo tham số và không có cận gradient đều; định lý áp dụng khi lớp ẩn cố định; ba mức khẳng định (chứng minh được, lý thuyết không lồi bổ sung, phỏng đoán thực nghiệm).

**Đối tượng và kí hiệu chung** (ghi chú §1–§2):
- quan sát $z\in\mathcal Z$, phân bố $D$ chưa biết; mô hình tuyến tính $z=(x,y)$, $x\in\mathcal X\subseteq\mathbb R^p$, $\tilde y=2y-1$, $C_x$; ví dụ một chiều $\mathcal Z=\mathbb R$; tập huấn luyện $S=(Z_1,\ldots,Z_m)\sim D^m$, tập cố định $s=(z_1,\ldots,z_m)$;
- tham số $w\in W\subset\mathbb R^p$ ($W$ khác rỗng, đóng, lồi, có thể là $\mathbb R^p$), $\ell(w,z)\ge0$ khả vi theo $w$, $\nabla\ell(w,z)$, $L_S$, $L_D$; $\beta$, $G$, $R$;
- Thuật toán 08.1: $w_1$, $\eta_t$, $T$, $i_t$, $\xi=(i_1,\ldots,i_T)$, $w_t$, $w_{T+1}$, $\bar w_T$, $A(S;\xi)$; $\operatorname{proj}_W$;
- hai lần chạy ghép cặp: $s^{(i)}$, $i$, $z'$, quan sát kiểm tra $z$, $w'_t$, $\Delta_t=\lVert w_t-w'_t\rVert$, bước chung, bước khác biệt, ngân sách $\sum_t\eta_t$, $\epsilon_{\mathrm{stab}}(m)$;
- bước gradient: $\Gamma$, $\Gamma_{\eta,z}(w)=w-\eta\nabla\ell(w,z)$, hệ số giãn $\kappa$, $g_{uv}$; $q_u$ chỉ ở ghi chú diễn giả;
- đánh đổi: $\tilde w$, $\operatorname{opt}_S$, $\eta^*$, $T^*$, $B(T)$ (Bài tập 08.8); $F$, $F_*$, $\sigma^2$, $g_t$, $\mathcal F_{t-1}$ (Mệnh đề 08.12);
- cục bộ của ví dụ: $\ell_{\mathrm H}$, $s^{(4)}$ (Ví dụ 08.1–08.4, 08.9); $\varphi$, $\zeta$, $\tau$ (Bài tập 08.3(d)); $d$, $\delta$ (Bài tập 08.3(a)); $\psi(T)$, $q$ (Bài tập 08.7); $\theta$, $\Theta_1$, $\Theta_2$, $\chi(x)$ (Ví dụ 08.10, Bài tập 08.5).

**Giả thiết** (ghi chú §2): thống kê (T1) lấy mẫu, (T2) hàm lỗi, (T3) hàm lỗi bị chặn (chỉ Nhận xét 08.11), (X) đặc trưng bị chặn; tối ưu (S) lồi và $\beta$-trơn trên $\mathbb R^p$ với mọi $z$, (S′) chỉ $\beta$-trơn, (G) gradient bị chặn trên $W$ với mọi $z$, độ dài bước tất định $0<\eta_t\le2/\beta$, (I) $\Pr(i_t=i)=1/m$, (R) $\sup_{u\in W}\lVert w_1-u\rVert\le R$. Hệ quả của (G) và $W$ lồi: (L) của Bài 06. Các kết quả cho hàm lỗi lồi không giả sử (T3). Nhãn (X), (S′), (I), (R) là nhãn mới của Bài 08; tên nhãn còn mở cho tác giả (`review-log.md`), deck dùng đúng nhãn của ghi chú.

**Chuỗi định nghĩa → kết quả → phương pháp.**
1. Thí nghiệm hồi quy logistic: cùng mô hình, cùng tập huấn luyện, chỉ số bước thay đổi; khoảng cách $0{,}045\to0{,}919$ (Câu hỏi mở đầu).
2. Thiết lập bảy thành phần (§1), kí hiệu và giả thiết (§2); Ví dụ 08.1 (Huber trên bốn quan sát) và ứng dụng hồi quy logistic nhiều vòng (§3).
3. Thuật toán 08.1 → Định nghĩa 08.2 (hai lần chạy ghép cặp, bước chung, bước khác biệt, $\Delta_t$, ngân sách) → ví dụ một bước ($\tfrac14$ so với $\tfrac38$) → Ví dụ 08.2 (§4).
4. Định nghĩa 08.3 (hệ số giãn, không giãn, đồng bức) → Bổ đề 08.4 (bước gradient không giãn) → Ví dụ 08.3 (ngưỡng $2/\beta$ chặt; hàm lõm giãn) (§5).
5. Mệnh đề 08.5 (bất đẳng thức truy hồi; $\mathbb E\Delta_{T+1}\le\frac{2G}m\sum_t\eta_t$) → Ví dụ 08.4 (§6).
6. Định lý 08.6 (ổn định đều, $\frac{2G^2}m\sum_t\eta_t$) → Ví dụ 08.5 ($0{,}001$; $t/200$), Ví dụ 08.6 (thí nghiệm) → Hệ quả 08.7 (điểm lặp trung bình, $G^2\eta(T-1)/m$) → chương trình của Ví dụ 06.3 ($39{,}975$ so với $0{,}4750$) (§7).
7. Mệnh đề 06.5(b) → Hệ quả 08.8 (cận ghép, $\eta^*$) → Ví dụ 08.7 ($0{,}0866$; $0{,}0708$ so với $0{,}0500$; $T^*\approx7071$) → Định nghĩa 08.9 (dừng sớm, chính quy hóa tường minh, chính quy hóa ngầm) (§8).
8. Ví dụ 08.8 (cosin) → Mệnh đề 08.10 (hệ số giãn $1+\beta\eta$) → Nhận xét 08.11 (đọc thêm) → Mệnh đề 08.12 (đọc thêm; tính dừng) → Ví dụ 08.9 ($\eta>2/\beta$) → Ví dụ 08.10 (không trơn; mạng ReLU) (§9).

**Giới hạn áp dụng** (ghi chú §10): mọi bảo đảm theo kì vọng, không có cận với xác suất cao, không chặn $\mathbb E\lvert L_D-L_S\rvert$; cận tăng tuyến tính theo ngân sách, đại lượng đo được tăng chậm hơn (Ví dụ 08.6); hàm lỗi bản lề và mạng ReLU không thỏa (S) (Ví dụ 08.10); hàm lỗi bình phương cần $W$ bị chặn và dữ liệu bị chặn; Định lý 08.6 không chặn $L_D$, cận số hạng tối ưu chỉ cho $\bar w_T$ (Hệ quả 08.8); với mạng sâu, "huấn luyện nhanh hơn thì tổng quát hóa tốt hơn" và chính quy hóa ngầm là phỏng đoán thực nghiệm. Phụ lục A (tính đồng bức), B (xáo trộn lại, tính đo được), C (chứng minh Hệ quả 08.8), D (Mệnh đề 08.10), E (Mệnh đề 08.12) vào trang ý tưởng chứng minh hoặc ghi chú diễn giả; Phụ lục F (giao thức thí nghiệm) ở ghi chú diễn giả 1-06, 4-04.

## 3. Bảng mạch

Bảy mạch theo đúng thứ tự các mục của ghi chú; mỗi mạch ứng với các mục liên tiếp. Mạch 2 gộp §1–§5: hai lần chạy ghép cặp (§4) và bước gradient không giãn (§5) là hai nửa của câu hỏi "hai quỹ đạo tách nhau ở đâu", và tách §5 khỏi §1–§4 để lại mạch 2 không có bài tập nào trong `exercises.md` chỉ cần §1–§4. Mạch 3 chỉ có §6 vì Mệnh đề 08.5 là bước then chốt của bài, có bài tập riêng (Bài tập 08.1(c)). Bảng đối chiếu trang → khối ghi chú ở mục 12.

| N | Tên mạch | Mục ghi chú | Chức năng | Đầu vào | Đầu ra | `strand-lead` (âm tiết) | Từ khóa | Trang | Phút |
|---|---|---|---|---|---|---|---|---:|---:|
| 1 | Mở đầu | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết | Bìa, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, ví dụ thí nghiệm | Bài 06: Định nghĩa 06.9, Định lý 06.10; Bài 05: SGD, hàm trơn | Câu hỏi: chỉ số bước thay đổi, đại lượng nào quyết định khoảng cách | (không có trang tiêu đề mạch) | — | 6 | 9 |
| 2 | Hai lần chạy ghép cặp và bước gradient không giãn | §1–§5 | Thiết lập, Thuật toán 08.1; giả thiết; Ví dụ 08.1, ứng dụng; Định nghĩa 08.2; trực quan ghép cặp; Ví dụ 08.2 (hình F1); Định nghĩa 08.3; Bổ đề 08.4 và ý tưởng chứng minh; Ví dụ 08.3; Bài tập 08.3(a) | ổn định đều cần so hai kì vọng trên hai mẫu lân cận | Ghép cặp cho phép so từng quỹ đạo; ở bước chung, $\Delta_{t+1}\le\Delta_t$ khi hàm lỗi lồi, trơn và $\eta_t\le2/\beta$ | "Hai lần chạy dùng chung các lần rút; với hàm lỗi lồi, trơn, bước ngắn trên cùng quan sát không đẩy chúng ra xa." (24) | hai lần chạy ghép cặp · bước chung · bước khác biệt · không giãn · tính đồng bức | 12 | 30 |
| 3 | Bất đẳng thức truy hồi | §6 | Mệnh đề 08.5 (trực quan, phát biểu) và ý tưởng chứng minh; Ví dụ 08.4; Bài tập 08.1(c) | Bổ đề 08.4 cho bước chung; bước khác biệt chưa được chặn | $\Delta_{t+1}\le\Delta_t+2G\eta_t\mathbb 1[i_t=i]$ trên từng quỹ đạo; $\mathbb E\Delta_{T+1}\le\frac{2G}m\sum_t\eta_t$ | "Khoảng cách giữa hai lần chạy chỉ tăng ở bước dùng quan sát bị thay, xảy ra với xác suất $1/m$." (20) | bất đẳng thức truy hồi · ngân sách độ dài bước · thừa số $1/m$ | 5 | 13 |
| 4 | Tính ổn định đều của hạ gradient ngẫu nhiên | §7 | Định lý 08.6 (trực quan, phát biểu) và ý tưởng chứng minh; Ví dụ 08.5; Ví dụ 08.6 (hình F2); Hệ quả 08.7 và chương trình của Ví dụ 06.3; Bài tập 08.7(b) | $\mathbb E_\xi\Delta_{T+1}$ của mạch 3; Định nghĩa 06.9, Định lý 06.10 | $\epsilon_{\mathrm{stab}}(m)=\frac{2G^2}m\sum_t\eta_t$ cho $w_{T+1}$, $G^2\eta(T-1)/m$ cho $\bar w_T$; cùng số chặn khoảng cách tổng quát hóa kì vọng | "Với (T1), (T2), (S), (G), $\eta_t\le2/\beta$, khoảng cách tổng quát hóa kì vọng không vượt $2G^2/m$ nhân ngân sách độ dài bước." (20) | ổn định đều · điểm lặp cuối · điểm lặp trung bình · ghép cặp trong thí nghiệm mở đầu | 8 | 20 |
| 5 | Đánh đổi giữa tối ưu và ổn định | §8 | Hệ quả 08.8 (trực quan, phát biểu) và ý tưởng chứng minh; Ví dụ 08.7 (hình F3); Định nghĩa 08.9; Bài tập 08.8(b) | Hệ quả 08.7; Mệnh đề 06.5(b); Định lý 05.14 | Cận ghép $\frac{R^2}{2\eta T}+\frac{\eta G^2}2+\frac{\eta G^2(T-1)}m$; nhiều vòng không cho cận nhỏ hơn một vòng | "Với độ dài bước cố định, thêm bước làm cận tối ưu giảm, cận ổn định tăng; tổng nhỏ nhất ở số bước hữu hạn." (25) | cận ghép · số bước tốt nhất · dừng sớm · chính quy hóa ngầm | 6 | 15 |
| 6 | Khi bỏ tính lồi hoặc tính trơn | §9 | Ví dụ 08.8 (hình F4); Mệnh đề 08.10 và ý tưởng chứng minh (Nhận xét 08.11 một dòng); Mệnh đề 08.12 (đọc thêm); Ví dụ 08.9; Ví dụ 08.10; Bài tập 08.3(d) | bước nào của mạch 2–4 dùng tính lồi, tính trơn | Hệ số giãn $1+\beta\eta$, cận tăng theo hàm mũ; mạng ReLU không thỏa (S), (G) | "Không có tính lồi, bước chung có thể đẩy hai lần chạy ra xa; mạng ReLU huấn luyện mọi lớp không thỏa (S), (S′)." (24) | hệ số giãn · hàm lỗi cosin · điểm dừng xấp xỉ · mạng ReLU | 8 | 21 |
| 7 | Tổng kết | §10–§13 | Bảng kết quả, trả lời vấn đề trung tâm, bài tập tổng hợp (Bài tập 08.5(c), (d)(i)), tự kiểm tra, bài tập về nhà, tài liệu | mọi kết quả | Cầu nối sang Bài 09 | "Tính lồi, tính trơn, (G), điều kiện bước đều có phản ví dụ; mạng ReLU huấn luyện mọi lớp nằm ngoài các kết quả." (24) | — | 10 | 12 |
| | **Tổng** | | | | | | | **55** | **120** |

Số trang của deck cuối: 55 (trần 55; lý do ở mục 16: trang ý tưởng chứng minh Hệ quả 08.7, bảng tổng kết hai trang, bài tập tổng hợp ba trang). Bản lập ban đầu: 52. Sáu kết quả chính có trang phát biểu; năm có trang "Ý tưởng chứng minh" riêng (Bổ đề 08.4, Mệnh đề 08.5, Định lý 08.6, Hệ quả 08.8, Mệnh đề 08.10); Hệ quả 08.7 có lộ trình chứng minh ở ghi chú diễn giả (mục 11, điểm 2). Đã gộp để giữ 52: Thuật toán 08.1 vào trang thiết lập 2-01 (§4 dòng đầu định nghĩa thuật toán, §1 mô tả nó bằng lời); Ví dụ 08.1 và khối ứng dụng §3 chung trang 2-03 (hai thẻ); trực quan và phát biểu chung trang ở Bổ đề 08.4 (2-08), Mệnh đề 08.5 (3-01), Định lý 08.6 (4-01), Hệ quả 08.7 (4-05), Hệ quả 08.8 (5-01), Mệnh đề 08.10 (6-02); Nhận xét 08.11 (đọc thêm) thành một dòng trên trang ý tưởng chứng minh 6-03; Phụ lục A, B, D, E ở trang ý tưởng chứng minh hoặc ghi chú diễn giả.

## 4. Bảng kết quả chính

Số hiệu theo ghi chú. Ánh xạ blueprint → ghi chú theo `outline.md` §2 (không hiện cho người học). Mọi phát biểu rút gọn trên trang dùng "Giả thiết:" và "Bảo đảm:", giữ đủ giả thiết, lượng từ, hằng số và loại bảo đảm của ghi chú (tất định trên từng quỹ đạo; theo kì vọng theo $\xi$ với tập huấn luyện cố định; theo kì vọng theo $(S,\xi)$).

| Kết quả | Loại bảo đảm | (a) Trực quan | (b) Ý tưởng chứng minh | (c) Kỹ thuật | (d) Ví dụ bổ trợ | Trang |
|---|---|---|---|---|---|---|
| **Bổ đề 08.4** (bước gradient không giãn; phác thảo, (a) ở Phụ lục A) | tất định; $f$ lồi, $\beta$-trơn trên toàn $\mathbb R^p$; $0\le\eta\le2/\beta$; $W$ khác rỗng, đóng, lồi | Một chiều, khi $f$ khả vi hai lần: $f''\in[0,\beta]$, nên hệ số góc của $\Gamma$ là $1-\eta f''\in[1-\eta\beta,1]\subset[-1,1]$ khi $\eta\le2/\beta$. Tính lồi cho cận trên $1$; điều kiện độ dài bước cho cận dưới $-1$. Cực biên: hàm bậc hai với $\eta=2$ có hệ số góc $-1$ (Ví dụ 08.3). | Ba bước cho (b), (c): khai triển $\lVert(u-v)-\eta g_{uv}\rVert^2$; (a) chặn số hạng giữa (tính lồi và tính trơn vào ở đây); $\eta\le2/\beta$ cho hệ số $\eta(2/\beta-\eta)\ge0$; hợp với phép chiếu không giãn. (a) theo Phụ lục A: cận trên bậc hai; hàm phụ $q_u$ cực tiểu tại $u$ (dòng duy nhất dùng tính lồi); đổi vai $u$, $v$ rồi cộng. Bỏ tính lồi: $f=-\tfrac12w^2$, $q_u$ không có cực tiểu, hệ số giãn $1+\eta$. | Một dòng "Kỹ thuật." trên 2-09: hàm phụ $q_u=f-\langle\nabla f(u),\cdot\rangle$ có $\nabla q_u(u)=0$. Chỉ dùng ở đây. Nhắc lại phép chiếu không giãn (Bài 05) trên 1-02. | Ví dụ 08.3 (bảng $\tfrac12;1;\tfrac32$ / $1;1;3$ / $2;2;4$); Bài tập 08.3(a) (Huber, cặp $\pm0{,}2$, $0{,}8=2\lvert u-v\rvert$ khi $\eta=3$). | 2-07, 2-08, 2-09, 2-10, 2-11 |
| **Mệnh đề 08.5** (bất đẳng thức truy hồi; chứng minh đầy đủ) | (a) tất định, mọi $\xi$, mọi $t$; (b) kì vọng theo $\xi$, tập huấn luyện, $i$, $z'$ cố định; không phụ thuộc $D$, $p$ | $\Delta$ chỉ tăng ở bước khác biệt, mỗi lần không quá $2G\eta_t$; trong $T$ bước, trung bình có $T/m$ bước khác biệt. Cực biên: cận (a) đạt được trên dãy $(2,3,1,4,4,4)$ của Ví dụ 08.4. | Bốn bước: bước chung, Bổ đề 08.4(c) ((S), $\eta_t\le2/\beta$); bước khác biệt, tam giác và (G) tại $w_t,w'_t\in W$ (không dùng tính lồi hay điều kiện độ dài bước); tổng triệt tiêu từ $\Delta_1=0$; kì vọng bằng tính tuyến tính và (I). Không cần $i_t$ độc lập với $\Delta_t$, vì (a) đúng trên từng quỹ đạo; do đó đúng cả khi xáo trộn lại (Phụ lục B(i)). Bỏ tính lồi: Bước 1 hỏng (Ví dụ 08.8). | **Nhắc lại** tổng triệt tiêu (Bài 05, trang riêng `L05-4-05`) một dòng trên 3-02; tính tuyến tính của kì vọng dùng không nhắc tên. | Ví dụ 08.4 ($\tfrac14$; $\tfrac{29}{64}\approx0{,}4531$; $0{,}8705\le1{,}5$; $\Delta_7=3$); hằng số $2G$ không giảm được ($\tfrac32$ và $\tfrac12$); Bài tập 08.1(c) ($\tfrac12$; $\tfrac{13}{16}$; hụt $\tfrac3{16}$). | 3-01, 3-02, 3-03, 3-04 |
| **Định lý 08.6** (tính ổn định đều của SGD; chứng minh đầy đủ) | (a) kì vọng theo $\xi$, mọi $s,i,z'$, mọi quan sát kiểm tra $z$; (b) ổn định đều; (c) kì vọng theo $(S,\xi)$, trị tuyệt đối; không phụ thuộc $p$, kích thước $W$; cấp thuật toán | Hai đầu ra gần nhau có hàm lỗi gần nhau tại mọi quan sát kiểm tra, vì (L); thừa số $1/m$ là xác suất một bước dùng quan sát bị thay. Đơn vị: gấp đôi ngân sách thì cận gấp đôi, gấp đôi $m$ thì cận giảm một nửa. Cực biên: $\eta_t\to0$ thì đầu ra về $w_1$ cố định. | Bốn bước: (L) từ (G) và $W$ lồi (định lý giá trị trung bình; không dùng tính lồi của hàm lỗi); Mệnh đề 08.5(b) cho (a); ghép cặp không đổi phân bố từng lần chạy, Jensen cho (b); khả tích ($\lVert w_{T+1}-w_1\rVert\le G\sum_t\eta_t$, (T2)) và Định lý 06.10 ((T1), $\xi$ độc lập với $S$) cho (c). | **Nhắc lại** lập luận đổi vai (Bài 06, trang riêng `L06-4-05`) một dòng trên 4-02, là công cụ bên trong Định lý 06.10. Ghép cặp và Jensen ($\lvert\mathbb E a-\mathbb E b\rvert\le\mathbb E\lvert a-b\rvert$) đã trên 2-05. | Ví dụ 08.5 ($0{,}001$; $t/200$; $1$ và $100$); Ví dụ 08.6 (hình F2; tỉ số $11{,}1$ đến $108{,}8$; đổi nhãn $0{,}015\to0{,}034$); câu hỏi cuối buổi (a), (b) ($0{,}8$; $0{,}0113$) ở 7-05. | 4-01, 4-02, 4-03, 4-04 |
| **Hệ quả 08.7** (điểm lặp trung bình; chứng minh đầy đủ) | ổn định đều; kì vọng theo $(S,\xi)$ cho khoảng cách tổng quát hóa của $\bar w_T$ | Các điểm lặp đầu của hai lần chạy còn gần nhau, nên trung bình gần nhau hơn điểm lặp cuối; với bước hằng, hệ số nhỏ hơn một nửa hệ số của $w_{T+1}$. | Lộ trình ở ghi chú diễn giả 4-05: tam giác cho $\lVert\bar w_T-\bar w'_T\rVert\le\frac1T\sum_t\Delta_t$; Mệnh đề 08.5(b) cho từng $t$; đổi thứ tự lấy tổng ($\eta_k$ xuất hiện $T-k$ lần); (L); khả tích và Định lý 06.10. | Đổi thứ tự lấy tổng: một câu ở ghi chú diễn giả 4-05. | Chương trình của Ví dụ 06.3 ($39{,}975$ so với độ rộng $4$; giá trị đúng $0{,}4750$); Bài tập 08.7(b) ($0{,}25$; $4$; $39{,}975$ so với $0{,}0301$; $0{,}2843$; $0{,}4750$; $T\le161$, $T\le80$). | 4-05, 4-06 (ý tưởng chứng minh), 4-07 |
| **Hệ quả 08.8** (rủi ro vượt mức kì vọng của SGD nhiều vòng; chứng minh đầy đủ ở Phụ lục C) | kì vọng theo $(S,\xi)$; rủi ro vượt mức so với $W$; (R); $\eta$ hằng; đầu ra $\bar w_T$; không phụ thuộc $p$ | Khi $T$ tăng, cận tối ưu giảm, cận ổn định tăng; tổng nhỏ nhất ở số bước hữu hạn. Cực biên: $T\to\infty$ với $\eta^*$ cho $RG\sqrt{2/m}$, lớn hơn $RG/\sqrt{m+1}$ của một vòng với quan sát mới khoảng $\sqrt2$ lần. | Bốn bước: Hệ quả 08.7 cho khoảng cách tổng quát hóa; Định lý 05.14 với oracle rút đều trên $s$ cố định ((S) cho (C), (G) cho (G2), (R) cho $\lVert w_1-u\rVert\le R$); Mệnh đề 06.5(b) ((T1)); cân hai số hạng $a/\eta+b\eta$. Ghép cận của $w_{T+1}$ với Định lý 05.14 là sai, vì Định lý 05.14 chỉ chặn $\bar w_T$. | **Nhắc lại** cân hai số hạng (Bài 05, một dòng) trên 5-02. | Ví dụ 08.7 ($0{,}0500$; $\eta^*\approx0{,}0289$, $0{,}0866$; $0{,}0708$; $T^*\approx7071$, $0{,}0958$; hình F3); Bài tập 08.8(b) ($3535{,}5$, $0{,}1208$; $17\,677{,}7$, $0{,}0808$; $\to0{,}0708$). | 5-01, 5-02, 5-03, 5-05 |
| **Mệnh đề 08.10** (bất đẳng thức truy hồi khi bỏ tính lồi; phác thảo, Phụ lục D) | (a) tất định; (b) tất định, mọi $\xi$, $t$; (c) kì vọng theo $\xi$; $\eta_t>0$ bất kì | Không lồi, mỗi bước chung có thể nhân khoảng cách với $1+\beta\eta_t$; $T$ bước chung nhân tới $\prod_t(1+\beta\eta_t)\le e^{\beta\sum_t\eta_t}$, tức hàm mũ của ngân sách. Cực biên: $\eta_t=c/t$ cho thừa số đa thức $(T/t)^{\beta c}$. | Ba bước: tam giác và (S′) cho hệ số giãn $1+\beta\eta$, phép chiếu giữ hệ số; bước chung dùng (a) thay Bổ đề 08.4, bước khác biệt như Mệnh đề 08.5 (không dùng tính lồi); kì vọng, khai triển từ $\Delta_1=0$, $1+x\le e^x$. Hằng số $1+\beta\eta$ không giảm được (cosin, $1+\eta$ tại $w=z$). | Không có kỹ thuật mới (cùng lộ trình với Mệnh đề 08.5). | Ví dụ 08.8 (hình F4; $\Delta_2\approx0{,}0010$; $\Delta_{58}\approx0{,}207>0{,}2$; $\to\pi$); $275{,}6$ với hàm lỗi trong $[0,2]$; Nhận xét 08.11 ($33{,}37>1$); Bài tập 08.3(d) ($68\le\tau\le76$, $\tau=68$). | 6-01, 6-02, 6-03, 6-07 |

**Kết quả phụ và quyết định.**
- Thuật toán 08.1: trang thiết lập 2-01 (phép cập nhật, đầu ra, $A(S;\xi)$); đoạn sau thuật toán (mỗi quan sát dùng trung bình $T/m$ lần; Hệ quả 06.2 không áp dụng khi $T\ge2$) ở ghi chú diễn giả 2-01.
- Định nghĩa 08.2: trang 2-04 (bốn thành phần), trực quan ở 2-05 (ví dụ một bước, Jensen).
- Định nghĩa 08.3: trang 2-07, với hai ví dụ dấu bằng và hàm lõm của ghi chú.
- Định nghĩa 08.9: trang 5-04, với ví dụ chính quy hóa ngầm ở ghi chú diễn giả và dòng so sánh hai hệ số ổn định trên mặt trang.
- Nhận xét 08.11 (đọc thêm): một dòng trên 6-03 (giả thiết thêm, số $33{,}37$); công thức đầy đủ ở ghi chú diễn giả 6-03.
- Mệnh đề 08.12 (đọc thêm; chứng minh ở Phụ lục E): trang 6-04 (Bài 10 dùng lại kết quả này); lộ trình ở ghi chú diễn giả; không có trang ý tưởng chứng minh riêng (mục 11, điểm 3).
- Đoạn "giả thiết đi vào chứng minh" sau Định lý 08.6: ghi chú diễn giả 4-02 và cột "Giả thiết không được bỏ" của 7-01.
- Đoạn "Mạng ReLU huấn luyện mọi lớp nơ-ron không thỏa giả thiết của Định lý 08.6, Mệnh đề 08.10 hay Nhận xét 08.11" sau Ví dụ 08.10: dòng cuối 6-06 và lời giải 7-04.
- Câu ôn nhanh 1–2: ghi chú diễn giả 1-02.
- §10 (ba mức khẳng định, năm giới hạn, so sánh với Hệ quả 07.16): trang 7-02 và ghi chú diễn giả 7-01, 7-02.
- §12 (câu hỏi cuối buổi): câu hỏi tự kiểm tra 3 và 4 ở 7-05 (phần (a), (b) và (c)); phần (d) trùng ý bài tập tổng hợp 7-03, 7-04.
- Phụ lục F: ghi chú diễn giả 1-06 (dữ liệu, ba lần chạy, $20$ hạt giống) và 4-04 ($\Delta$ không ghép cặp $2{,}99$ đến $4{,}00$; $\eta=0{,}25$ cho $0{,}651$ ở cùng ngân sách $5000$).

## 5. Ví dụ bổ trợ

Ví dụ xuyên suốt: **hàm lỗi Huber trên bốn quan sát** $s=(0,1,2,3)$ (Ví dụ 08.1, 08.2, 08.3, 08.4, 08.9; Bài tập 08.1(c), 08.3(a)) và **thí nghiệm hồi quy logistic $p=100$, $m=200$** (Câu hỏi mở đầu, Ví dụ 08.5 Bước 3, Ví dụ 08.6, Định nghĩa 08.9 đoạn sau); thêm ứng dụng **hồi quy logistic nhiều vòng trên $10^4$ hồ sơ** (§3, Ví dụ 08.7, Bài tập 08.8). Mỗi lần dùng lại trả lời một câu hỏi mới. Huber: dữ liệu và hằng số (2-03); ghép cặp so với hai dãy độc lập (2-05); hai quỹ đạo, hai loại bước (2-06); hệ số giãn (2-10); chứng minh trực tiếp tính không giãn (2-11); kì vọng của $\Delta$ (3-03); $\eta=1$ (3-04); $\eta>2/\beta$ (6-05). Thí nghiệm: câu hỏi (1-06); cận $t/200$ (4-03); $\Delta$ ghép cặp, đổi nhãn, tỉ số cận trên khoảng cách (4-04); số bước tốt nhất theo hàm lỗi đánh giá (5-04). Hồ sơ: câu hỏi thực hành (2-03); câu trả lời bằng Hệ quả 08.8 (5-03); số bước tốt nhất với hai độ dài bước khác (5-05).

Mọi con số dưới đây đã tính lại bằng Python (phân số chính xác cho ví dụ Huber; thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-08/storyboard/num.py`, `num2.py`) và khớp ghi chú, tệp bài tập. **Không có ví dụ mới mang số mới trên mặt trang.** Bốn hình dùng số của ghi chú: F1 vẽ hai quỹ đạo của Ví dụ 08.2; F2 vẽ các cột của câu hỏi mở đầu và Ví dụ 08.6 cùng cận $t/200$; F3 vẽ vế phải của Hệ quả 08.8(a) với số của Ví dụ 08.7, Bước 3; F4 vẽ quỹ đạo tất định của Ví dụ 08.8, lặp đúng phép cập nhật của ghi chú (chỉ các giá trị của bảng ghi chú có nhãn số).

**V1. Câu hỏi mở đầu** (1-06). Bảng năm dòng của ghi chú. Cận $2G^2\eta t/m=2\cdot0{,}5\,t/200=t/200$, bằng số vòng; sau $t$ bước, ngân sách $0{,}5t$. Tỉ số cận trên khoảng cách: $0{,}5/0{,}045=11{,}11$; $100/0{,}919=108{,}81$ (ghi chú: $11{,}1$, $108{,}8$).

**V2. Ví dụ 08.1** (2-03). $\partial_w\ell_{\mathrm H}=\max\{-1,\min\{1,w-z\}\}$; $\beta=G=1$; $\eta_t\le2$. Lần chạy $w_1=0$, $\eta=\tfrac12$, dãy $(1,4,2,3,4,1)$: đạo hàm $0;-1;-\tfrac12;-1;-1;1$; $w_2,\ldots,w_7=0;\tfrac12;\tfrac34;\tfrac54;\tfrac74;\tfrac54$. Ứng dụng: $5/\sqrt{10\,001}=0{,}0499975\approx0{,}05$.

**V3. Một bước ghép cặp** (2-05; đoạn sau Định nghĩa 08.2). $w_2$ trên $s$: $0;\tfrac12;\tfrac12;\tfrac12$ (theo $i_1=1,\ldots,4$); trên $s^{(4)}$: $0;\tfrac12;\tfrac12;-\tfrac12$. $\mathbb E_\xi w_2=\tfrac38$, $\mathbb E_\xi w'_2=\tfrac18$, hiệu $\tfrac14$. Ghép cặp: chỉ $i_1=4$ cho $\lvert w_2-w'_2\rvert=1$, kì vọng $\tfrac14$. Hai dãy độc lập: $16$ cặp, $7$ cặp cho $0$, $6$ cặp cho $\tfrac12$, $3$ cặp cho $1$; $(6\cdot\tfrac12+3)/16=\tfrac38$.

**V4. Ví dụ 08.2** (2-06; hình F1). $w_1,\ldots,w_7=0;0;\tfrac12;\tfrac34;\tfrac54;\tfrac74;\tfrac54$; $w'_1,\ldots,w'_7=0;0;-\tfrac12;0;\tfrac12;0;0$; $\Delta_1,\ldots,\Delta_7=0;0;1;\tfrac34;\tfrac34;\tfrac74;\tfrac54$. Bước khác biệt $t=2$ ($0\to1$), $t=5$ ($\tfrac34\to\tfrac74$), mỗi lần $+1=2G\eta$; bước chung $0\to0$, $1\to\tfrac34$, $\tfrac34\to\tfrac34$, $\tfrac74\to\tfrac54$; $\Delta_7=\tfrac54\le2$.

**V5. Định nghĩa 08.3, hai ví dụ** (2-07). $f=\tfrac\beta2\lVert w\rVert^2$: hai vế bằng $\beta\lVert u-v\rVert^2$. $f=-\tfrac12w^2$: vế trái $-(u-v)^2<0$.

**V6. Ví dụ 08.3** (2-10). Hệ số giãn nhỏ nhất: bậc hai $\lvert1-\eta\rvert$: $\tfrac12;1;2$; Huber $\max\{\lvert1-\eta\rvert,1\}$: $1;1;2$; lõm $1+\eta$: $\tfrac32;3;4$, với $\eta=\tfrac12;2;3$.

**V7. Bài tập 08.3(a)** (2-11; số của `exercises.md`). $\eta=3$, $z=0$, $u=0{,}2$, $v=-0{,}2$: $\Gamma(w)=-2w$ trên $[-1,1]$, $\Gamma(u)-\Gamma(v)=-0{,}4-0{,}4=-0{,}8$, $\lvert\cdot\rvert=0{,}8=2\cdot0{,}4$.

**V8. Hằng số $2G$** (ghi chú diễn giả 3-02; đoạn sau chứng minh Mệnh đề 08.5). $w_t=w'_t=1$, $z_i=3$, $z'=-3$, $\eta=\tfrac12$: $1-\tfrac12(-1)=\tfrac32$, $1-\tfrac12\cdot1=\tfrac12$, cách nhau $1=2G\eta$.

**V9. Ví dụ 08.4** (3-03). Liệt kê chính xác: $\mathbb E\Delta_2=\tfrac14$; $\mathbb E\Delta_3=\tfrac{29}{64}=0{,}453125$ (nhóm $i_1\ne4$: $3$; nhóm $i_1=4$: $\tfrac12+\tfrac34+1+2=\tfrac{17}4$; $(3+\tfrac{17}4)/16$); $\mathbb E\Delta_7=\tfrac{228\,203}{262\,144}=0{,}870525$; cận $T/4$: $\tfrac14$; $\tfrac12$; $1{,}5$. Dãy $(2,3,1,4,4,4)$: $w_7=2$, $w'_7=-1$, $\Delta_7=3$.

**V10. Bài tập 08.1(c)** (3-04; số của `exercises.md`). $\eta=1$: cận $T/2$. $\mathbb E\Delta_2=\tfrac24=\tfrac12$; $\mathbb E\Delta_3=(6+7)/16=\tfrac{13}{16}=0{,}8125<1$; nhóm $i_1=4$: $\Delta_3=0;1;2;4$ theo $i_2=1,\ldots,4$; dãy có phần hụt (liệt kê $16$ dãy): $(4,1)$ ($\Delta_3=0$, cận $2$), $(4,2)$ ($\Delta_3=1$, cận $2$); tổng phần hụt $3$, $\tfrac3{16}=1-\tfrac{13}{16}$.

**V11. Ví dụ 08.5** (4-03). $2\cdot1\cdot0{,}05\cdot10^4/10^6=0{,}001$; $2\cdot0{,}5\,t/200=t/200$: $t=200$ cho $1$, $t=20\,000$ cho $100$.

**V12. Ví dụ 08.6** (4-04; hình F2). Bảng ghi chú: $\Delta$ ghép cặp $0{,}142;0{,}233;0{,}873;2{,}219;5{,}458$; đổi nhãn $0{,}015;0{,}016;0{,}022;0{,}026;0{,}034$ ở $0{,}5;1;5;20;100$ vòng; khoảng $1{,}31$–$15{,}08$ của $\Delta$ và $0{,}693$–$1{,}149$ của khoảng cách ở $100$ vòng; tỉ số $11{,}1$ và $108{,}8$.

**V13. Hệ quả 08.7 và Ví dụ 06.3** (4-05). $\beta=2$, $G=2(1+1)=4$, $\eta=0{,}00625\le1$; $G^2\eta(T-1)/m=16\cdot0{,}00625\cdot1599/4=39{,}975$; độ rộng miền giá trị $4$; giá trị đúng $0{,}4750$. Bước hằng: $\frac{2G^2}m\cdot\frac\eta T\cdot\frac{T(T-1)}2=\frac{G^2\eta(T-1)}m$.

**V14. Bài tập 08.7(b)** (4-06; số của `exercises.md`). $0{,}025(T-1)$: $0{,}25$; $4$; $39{,}975$. $q=0{,}9875$; $\psi(11)=0{,}030107$; $\psi(161)=0{,}284340$; $\psi(1600)=0{,}475000$. $0{,}025(T-1)\le4\iff T\le161$; $0{,}05T\le4\iff T\le80$.

**V15. Ví dụ 08.7** (5-03; hình F3). $5/\sqrt{10\,001}=0{,}049998\le0{,}0500$; $T=10^4$: $1+2\cdot9999/10^4=2{,}9998$, $\eta^*=0{,}028868\approx0{,}0289$, cận $0{,}086600\le0{,}0866$; $T=2\cdot10^4$: $0{,}079055\le0{,}0791$; $T=10^5$: $0{,}072457\le0{,}0725$; $T\to\infty$: $0{,}070711\le0{,}0708$. $\eta=0{,}05$: $B(T)=250/T+0{,}025+0{,}05(T-1)/10^4$; $T^*=R\sqrt{m/2}/(\eta G)=7071{,}07$; $B(5000)=0{,}099995$; $B(7071)=0{,}095706$; $B(10^4)=0{,}099995$; $B(2\cdot10^4)=0{,}137495$; $B(5\cdot10^4)=0{,}279995$ (ghi chú làm tròn lên: $0{,}1000$; $0{,}0958$; $0{,}1000$; $0{,}1375$; $0{,}2800$). Tỉ số với một vòng tại $T=m$: $1{,}7321\approx\sqrt3$.

**V16. Bài tập 08.8(b)** (5-05; số của `exercises.md`). $RG\sqrt{2/m}=0{,}070711$; $R\sqrt{m/2}/G=353{,}55$. $\eta=0{,}1$: $T^*=3535{,}53$, $B(T^*)=0{,}070711+0{,}05-0{,}00001=0{,}120701\le0{,}1208$. $\eta=0{,}02$: $T^*=17\,677{,}67$, $B(T^*)=0{,}070711+0{,}01-0{,}000002=0{,}080709\le0{,}0808$.

**V17. Định nghĩa 08.9, đoạn sau** (5-04). Thí nghiệm: hàm lỗi logistic kiểm tra $0{,}589$ ở $5$ vòng, $0{,}603$ ở $10$ vòng; lỗi phân lớp $0{,}309$; $0{,}301$; $0{,}312$ ở $5$, $20$, $100$ vòng.

**V18. Ví dụ 08.8** (6-01; hình F4). $w'_2=0{,}1\sin(-0{,}01)=-0{,}00099998$; $\Delta_3/\Delta_2=1{,}0999999\approx1{,}1000$; lặp $w'_{t+1}=w'_t+0{,}1\sin w'_t$: $\Delta_{21}=0{,}006116$; $\Delta_{41}=0{,}041139$; $\Delta_{58}=0{,}207316$ (giá trị đầu tiên vượt $0{,}2$); $\Delta_{61}=0{,}275281$; $\Delta_{81}=1{,}529034$; $\Delta_{101}=2{,}879307$; $\Delta_{200}=3{,}141585\to\pi$. Khớp bảng ghi chú ($0{,}0061$; $0{,}0411$; $0{,}207$; $0{,}2753$; $1{,}529$; $2{,}879$).

**V19. Mệnh đề 08.10, đoạn sau** (6-03). $(1{,}1)^{100}=13\,780{,}6\approx1{,}378\cdot10^4$; $\tfrac2{100}\big((1{,}1)^{100}-1\big)=275{,}59\approx275{,}6$. Nhận xét 08.11: $\beta=10$, $c=1$, $G=1$, $m=10^4$, $T=10^6$: $T^{10/11}\cdot2^{1/11}\cdot1{,}1/9999=33{,}369\le33{,}37$.

**V20. Mệnh đề 08.12, đoạn sau** (6-04). $2\ln2/500+0{,}0125=0{,}0027726+0{,}0125=0{,}0152726\le0{,}0153$.

**V21. Ví dụ 08.9** (6-05). $\eta=1$: $\Delta_2=0{,}02$, rồi $0$. $\eta=2$: $\Delta_t=0{,}04$. $\eta=3$: $\Delta_2,\ldots,\Delta_8=0{,}06;0{,}12;0{,}24;0{,}48;0{,}96;1{,}92;3{,}84$; $\lvert1-\eta\beta\rvert=2$.

**V22. Ví dụ 08.10** (6-06). $\lvert w\rvert$, $\eta=\tfrac12$: $0{,}01-\tfrac12=-0{,}49$, $-0{,}01+\tfrac12=0{,}49$; $0{,}02\to0{,}98$. Bản lề $\max\{0,1-w\}$: $0{,}99\mapsto0{,}99+\tfrac12=1{,}49$; $1{,}01\mapsto1{,}01$; $0{,}02\to0{,}48$. Bài tập 07.5(c): $0$ tại hai tham số, $\tfrac{27}{16}$ tại trung điểm.

**V23. Bài tập 08.3(d)** (6-07; số của `exercises.md`). $\Delta_2=0{,}1\sin0{,}01=0{,}00099998$; $\ln(0{,}5/\Delta_2)=6{,}2146$; $1+0{,}1\cos\tfrac12=1{,}087758$; $6{,}2146/\ln1{,}1=65{,}20$, nên $\tau\ge68$; $1{,}087758^{74}\Delta_2=0{,}5051>\tfrac12$, nên $\tau\le76$; lặp trực tiếp: $\tau=68$ (khớp V18: $\Delta_{68}$ là giá trị đầu tiên vượt $0{,}5$).

**V24. Bài tập 08.5(c), (d)(i)** (7-03, 7-04; số của `exercises.md`). Báo cáo: $2\cdot0{,}1\cdot10^5/(5\cdot10^4)=0{,}4$. (a): đạo hàm trái $0$, phải $-\tfrac12$; $\ell(0)=0{,}6931$, $\tfrac12(\ell(-1)+\ell(1))=0{,}5032$. (b): $\theta_1=1/\theta_2$: $\theta_2/(1+e)$; $\theta_2=10$: $2{,}69$. (d)(i): $0{,}4G^2$, điều kiện $0{,}1\le8/G^2$; $G=1{,}5$: $0{,}9$. (d)(ii) chỉ ở ghi chú diễn giả: $1{,}1^{10^5}>10^{4139}$ ($10^5\log_{10}1{,}1=4139{,}27$).

**V25. Câu hỏi cuối buổi §12** (7-05). (a) ngân sách $0{,}1\cdot20\,000=2000$, cận $2\cdot2000/5000=0{,}8$. (b) $0{,}1(2\sqrt{20\,000}-1)=28{,}184\le28{,}19$, cận $2\cdot28{,}19/5000=0{,}011276\le0{,}0113$.

**V26. Câu ôn nhanh** (ghi chú diễn giả 1-02). (1) $g'(w)=-1/(1+e^w)\in(-1,0)$, $g''\le\tfrac14$: $g$ là $1$-Lipschitz, $\tfrac14$-trơn; $f=\tfrac12w^2$: không Lipschitz, $1$-trơn. (2) $6\cdot\tfrac14=1{,}5$; $1-(\tfrac34)^6=\tfrac{3367}{4096}=0{,}8220$.

## 6. Danh sách trang

> Bản lập trước khi viết deck. ID trang dưới đây đã đổi theo deck cuối (thêm `4-06` ý tưởng chứng minh Hệ quả 08.7, `7-02` bảng tổng kết tiếp, bài tập tổng hợp ba trang `7-04`–`7-06`); câu chữ trên mặt trang của deck cuối và lý do lệch ở mục 16 và mục 17.

Mỗi mục: ID, tiêu đề, loại, thời lượng; **Mặt trang** (các dòng dự kiến, theo thứ tự; `[f]` là fragment; `$$…$$` là công thức hiển thị, tính một dòng; `{{…}}` là chỉ dẫn bố cục, không lên mặt trang); **Ghi chú diễn giả** (ý chính, 40–150 âm tiết, đến ~250 cho trang ý tưởng chứng minh và trang bài tập; viết cho giảng viên và người học; không mã trang, mã ví dụ của storyboard, câu quy trình hay nguồn gốc; luôn kết thúc bằng dòng `note-source`); **Lý do / nối**; **Mục tiêu / nguồn**. Câu trên mặt trang là bản dự kiến đã tự kiểm theo `no-ai-slop` (chế độ Edit) và `eval.md`; người viết deck có thể rút gọn, không thêm khẳng định.

Quy ước chung cho người viết deck:
- Trang kết quả: "Giả thiết:" và "Bảo đảm:" (nhãn của ghi chú), trích số khối của ghi chú một lần.
- Trang tổng quan (bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm") viết bằng lời, không kí hiệu, không tiếng Anh. Lần đầu một thuật ngữ trên trang nội dung có tiếng Anh trong ngoặc (bảng mục 10).
- Mọi kí hiệu trên mặt trang đã có ở trang trước hoặc có dòng "Nhắc lại:"/"Kí hiệu:" (bảng đối chiếu mục 12 ghi chỗ đưa vào).
- Bước chứng minh trên trang "Ý tưởng chứng minh" là `<ol>`; giả thiết dùng ở bước ghi trong ngoặc đầu mục, như deck Bài 06 (`L06-4-04`); không nhãn in đậm "Bước k". "(a)", "(b)", "(c)" của một kết quả viết thường, không thành nhãn trong `<strong>`.
- Số thập phân dùng dấu phẩy KaTeX `0{,}5`; dãy số ngăn bằng `;\ `; số từ năm chữ số tách nhóm bằng `\,`.
- Mỗi trang ví dụ mở bằng dữ kiện dạng danh sách, không câu dẫn. "Diễn giải:" chỉ dùng số có trên chính trang đó.
- Không `\text{}` chứa tiếng Việt trong KaTeX. Trong ghi chú diễn giả, không ghi câu nguồn gốc, mã "V7", "mục 5", không mở bằng "Trang này", "Mạch này", "Bài này", không lấy mạch làm chủ ngữ.
- Công thức một dòng khi vừa khung; chỉ ngắt bằng `aligned` khi tràn ở 390 px (đo trong trình duyệt). Ở chế độ đọc hẹp, công thức rộng cuộn ngang tại chỗ.
- "Tập huấn luyện" theo ghi chú; "mẫu lân cận" giữ nguyên (thuật ngữ của Định nghĩa 06.9). Trên trang bài tập, giữ câu chữ của `exercises.md`, kể cả "mẫu" ở Bài tập 08.5 ("mẫu gồm $m=5\cdot10^4$ quan sát").
- Tiêu đề có công thức viết bằng KaTeX (6-05: "Ví dụ: độ dài bước vượt $2/\beta$").

### Mạch 1. Mở đầu (6 trang, 9 phút)

#### `1-01` Tính ổn định của SGD và tổng quát hóa trong học sâu — bìa, điểm vào mạch 1 · 1 phút
- **Mặt trang:** h1 tên bài; h3 "Bài 08"; luận điểm (mục 2, một câu, bằng lời); "Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1"; "Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN".
- **Ghi chú diễn giả:** Bài 06 chặn khoảng cách tổng quát hóa kì vọng của một thuật toán ổn định đều, và tối thiểu hóa rủi ro thực nghiệm có chính quy hóa là một thuật toán như vậy. Bài 08 cho cùng loại bảo đảm cho hạ gradient ngẫu nhiên chạy nhiều vòng trên một tập huấn luyện cố định. Luận điểm gồm Mệnh đề 08.5 (hai lần chạy ghép cặp cách nhau theo kì vọng không quá $\tfrac{2G}m\sum_t\eta_t$) và Định lý 08.6 (hệ số ổn định $\tfrac{2G^2}m\sum_t\eta_t$). Bảo đảm là theo kì vọng, cho một thuật toán cụ thể, và không phụ thuộc số chiều. Khi bỏ tính lồi hoặc tính trơn, như với mạng ReLU, chứng minh không còn đúng. Nguồn: ghi chú Bài 08, đoạn mở đầu, §10.
- **Lý do / nối:** luận điểm cả bài → tiên quyết.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu, §10.

#### `1-02` Tiên quyết và quy ước — mở đầu · 1,5 phút
- **Mặt trang:**
  - **Nhắc lại:** mẫu lân cận $s^{(i)}$: $s$ với $z_i$ thay bằng $z'$; $A$ ổn định đều: với mọi $s,i,z'$, mọi quan sát kiểm tra (test observation) $z$,
  - $$\big\lvert\mathbb E_\xi\ell(A(s;\xi),z)-\mathbb E_\xi\ell(A(s^{(i)};\xi),z)\big\rvert\le\epsilon_{\mathrm{stab}}(m).$$
  - Định lý 06.10: (T1), (T2), $\xi$ độc lập với $S$, ổn định đều, khả tích: $\lvert\mathbb E_{S,\xi}[L_D(A(S;\xi))-L_S(A(S;\xi))]\rvert\le\epsilon_{\mathrm{stab}}(m)$.
  - (T1): $Z_1,\ldots,Z_m$ độc lập cùng phân bố $D$; (T2): $\ell\ge0$, $\ell(w,\cdot)$ đo được, $L_D(w_1)<\infty$.
  - $f$ là $\beta$-trơn: $\lVert\nabla f(u)-\nabla f(v)\rVert\le\beta\lVert u-v\rVert$ (Định nghĩa 05.6); $\operatorname{proj}_W$ không giãn (Bài 05).
- **Ghi chú diễn giả:** Định nghĩa 06.9 đòi bất đẳng thức với mọi tập huấn luyện, mọi chỉ số, mọi quan sát thay thế và mọi quan sát kiểm tra; chỉ $\xi$ là ngẫu nhiên. Định lý 06.10 chuyển hệ số ổn định thành cận cho trị tuyệt đối của khoảng cách tổng quát hóa kì vọng, theo kì vọng theo cả tập huấn luyện và nguồn ngẫu nhiên riêng. Câu ôn nhanh 1: $\ln(1+e^{-w})$ là $1$-Lipschitz và $\tfrac14$-trơn; $\tfrac12w^2$ không Lipschitz trên $\mathbb R$ nhưng $1$-trơn. Câu ôn nhanh 2: rút sáu chỉ số đều trên bốn chỉ số, chỉ số $4$ được rút trung bình $1{,}5$ lần, và ít nhất một lần với xác suất $3367/4096\approx0{,}8220$. Nguồn: ghi chú Bài 08, Kiến thức tiên quyết, Câu hỏi ôn nhanh.
- **Lý do / nối:** các kết quả của Bài 05–06 dùng trên mặt trang được nhắc lại ở đây → mục tiêu.
- **Mục tiêu / nguồn:** 1–5; Kiến thức tiên quyết.

#### `1-03` Mục tiêu — mở đầu · 1 phút
- **Mặt trang (danh sách đánh số, bằng lời, không kí hiệu; trần 80):**
  1. Mô tả hai lần chạy ghép cặp và tính khoảng cách giữa chúng.
  2. Chứng minh bước gradient không giãn với hàm lồi, trơn và độ dài bước nhỏ.
  3. Chứng minh bất đẳng thức truy hồi; suy ra cận ổn định, cận khoảng cách tổng quát hóa kì vọng.
  4. Ghép cận ổn định với cận tối ưu để chọn số bước, độ dài bước.
  5. Kiểm tra giả thiết; phân biệt kết quả chứng minh được với phỏng đoán thực nghiệm.
- **Ghi chú diễn giả:** Mục tiêu 1 là cho hạ gradient ngẫu nhiên trên hai mẫu lân cận, tức hai tập huấn luyện khác nhau một quan sát, và khoảng cách được tính trên một ví dụ nhỏ. Ở mục tiêu 2, "không giãn" nghĩa là bước gradient không làm tăng khoảng cách giữa hai điểm, và "độ dài bước nhỏ" là độ dài bước không vượt hai lần nghịch đảo hằng số trơn. Mục tiêu 3 gồm cận ổn định của điểm lặp cuối và của điểm lặp trung bình, cùng cận cho khoảng cách tổng quát hóa kì vọng, tính bằng số. Ở mục tiêu 5, giả thiết của định lý được kiểm trên một thiết lập huấn luyện cụ thể: hàm lỗi không lồi, độ dài bước lớn, mạng ReLU. Nguồn: ghi chú Bài 08, Mục tiêu học tập.
- **Lý do / nối:** tiêu chí kiểm tra → nội dung.
- **Mục tiêu / nguồn:** tất cả; Mục tiêu học tập.

#### `1-04` Nội dung — mở đầu · 0,5 phút
- **Mặt trang:** `ol start="2"` với liên kết `#/2`…`#/7`: 2. Hai lần chạy ghép cặp và bước gradient không giãn; 3. Bất đẳng thức truy hồi; 4. Tính ổn định đều của hạ gradient ngẫu nhiên; 5. Đánh đổi giữa tối ưu và ổn định; 6. Khi bỏ tính lồi hoặc tính trơn; 7. Tổng kết. Dòng đọc trước: "Đọc trước: UML §13.1–13.2, §20.6."
- **Ghi chú diễn giả:** Hai lần chạy ghép cặp dùng chung mọi lần rút, nên khoảng cách giữa chúng chỉ đến từ quan sát bị thay. Bước gradient không giãn và bất đẳng thức truy hồi chặn khoảng cách đó theo số bước và độ dài bước. Tính Lipschitz đổi khoảng cách thành hệ số ổn định, rồi ghép với cận tối ưu của Bài 05 cho một đánh đổi theo số bước. Cuối cùng, các phản ví dụ cho thấy bước nào hỏng khi hàm lỗi không lồi hoặc không trơn. Nguồn: ghi chú Bài 08; §13.
- **Lý do / nối:** bản đồ mạch → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §13.

#### `1-05` Vấn đề trung tâm — mở đầu · 1 phút
- **Mặt trang:** một hộp `div.box`: "**Câu hỏi:** thuật toán huấn luyện ảnh hưởng tới khoảng cách tổng quát hóa như thế nào?" (17 âm tiết kể cả nhãn).
- **Ghi chú diễn giả** (câu trả lời cho cả bài, không trên mặt trang): Với hàm lỗi lồi, trơn, có gradient bị chặn và $\eta_t\le2/\beta$, thuật toán ảnh hưởng qua ngân sách độ dài bước: hạ gradient ngẫu nhiên ổn định đều với hệ số $\tfrac{2G^2}m\sum_t\eta_t$, và cùng số đó chặn khoảng cách tổng quát hóa kì vọng của điểm lặp cuối. Với điểm lặp trung bình, hệ số nhỏ hơn một nửa. Ghép với cận tối ưu, tổng hai cận nhỏ nhất ở một số bước hữu hạn. Khi bỏ tính lồi, cận tăng theo hàm mũ của ngân sách; với mạng ReLU huấn luyện mọi lớp nơ-ron, định lý không áp dụng. Nguồn: ghi chú Bài 08, đoạn mở đầu, §10.
- **Lý do / nối:** một vấn đề cốt lõi → câu hỏi cụ thể.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu.

#### `1-06` Ví dụ: khoảng cách tổng quát hóa theo số vòng qua dữ liệu — ví dụ dẫn nhập (Câu hỏi mở đầu) · 4 phút
- **Mặt trang:**
  - Hồi quy logistic, $p=100$, $m=200$, $\lVert x\rVert\le1$; mỗi nhãn bị lật với xác suất $0{,}1$.
  - Hạ gradient ngẫu nhiên (SGD) từ $0$, rút đều có hoàn lại, độ dài bước (step size) $0{,}5$.
  - Trung bình $20$ hạt giống (random seed); lỗi kiểm tra trên $5000$ quan sát độc lập.
  - Bảng: Số vòng | Huấn luyện | Kiểm tra | Khoảng cách; $0{,}5$ | $0{,}618$ | $0{,}662$ | $0{,}045$; $1$ | $0{,}561$ | $0{,}640$ | $0{,}079$; $5$ | $0{,}376$ | $0{,}589$ | $0{,}213$; $20$ | $0{,}243$ | $0{,}662$ | $0{,}419$; $100$ | $0{,}134$ | $1{,}053$ | $0{,}919$.
  - **Câu hỏi:** chỉ số bước thay đổi; đại lượng nào quyết định khoảng cách?
- **Ghi chú diễn giả:** Mô hình, tập huấn luyện và thuật toán giữ nguyên ở mọi dòng; lỗi huấn luyện giảm, còn khoảng cách giữa lỗi kiểm tra và lỗi huấn luyện tăng. Số tham số $100$ và lớp hàm như nhau ở mọi dòng, nên tỉ lệ giữa số tham số và cỡ mẫu không giải thích sự thay đổi. Đại lượng thay đổi là quỹ đạo: sau $t$ bước, tổng các độ dài bước là $0{,}5t$. Với hàm lỗi lồi, trơn, có gradient bị chặn và độ dài bước không vượt hai lần nghịch đảo hằng số trơn, khoảng cách tổng quát hóa kì vọng không vượt $c\cdot\tfrac1m\sum_t\eta_t$; ở đây $c=2$, nên cận sau $t$ bước là $t/200$, bằng số vòng. Mỗi lần chạy là $20\,000$ bước, từ véc-tơ $0$, nhãn sinh từ một véc-tơ ngẫu nhiên trên mặt cầu đơn vị. Nguồn: ghi chú Bài 08, Câu hỏi mở đầu và đoạn sau; Phụ lục F.
- **Lý do / nối:** ví dụ dẫn nhập trước mọi định nghĩa; câu trả lời bằng số ở mạch 4 → tiêu đề mạch 2.
- **Mục tiêu / nguồn:** 3, 5; Câu hỏi mở đầu.

### Mạch 2. Hai lần chạy ghép cặp và bước gradient không giãn (12 trang, 30 phút)

#### `2-00` 2. Hai lần chạy ghép cặp và bước gradient không giãn — tiêu đề mạch, điểm vào mạch 2 · 0,5 phút
- **Mặt trang:** "2."; h2 "Hai lần chạy ghép cặp và bước gradient không giãn"; `p.strand-lead` (bảng mạch, 24 âm tiết); `p.strand-keys`: "hai lần chạy ghép cặp · bước chung · bước khác biệt · không giãn · tính đồng bức".
- **Ghi chú diễn giả:** Định nghĩa 06.9 so hai kì vọng theo nguồn ngẫu nhiên riêng của thuật toán, một trên tập huấn luyện và một trên mẫu lân cận. Khi hai lần chạy dùng chung khởi tạo, độ dài bước và dãy chỉ số, ta so được chúng bước theo bước. Ở một bước dùng cùng quan sát, hai lần chạy áp dụng cùng một ánh xạ cho hai điểm; với hàm lỗi lồi, trơn và độ dài bước không vượt $2/\beta$, ánh xạ đó không làm tăng khoảng cách. Nguồn: ghi chú Bài 08, §1–§5.
- **Lý do / nối:** mạch 1 → thiết lập.
- **Mục tiêu / nguồn:** 1, 2; §1–§5.

#### `2-01` Thiết lập bài toán — thiết lập (§1; Thuật toán 08.1 ở §4) · 2,5 phút
- **Mặt trang:**
  - Quan sát $z\in\mathcal Z$ từ $D$ chưa biết; tập huấn luyện $S=(Z_1,\ldots,Z_m)\sim D^m$ theo (T1).
  - $W\subset\mathbb R^p$ khác rỗng, đóng, lồi; hàm lỗi $\ell(w,z)\ge0$ khả vi theo $w$.
  - **Thuật toán 08.1.** Với $t=1,\ldots,T$: rút $i_t$ đều trên $\{1,\ldots,m\}$, có hoàn lại; $\eta_t>0$ tất định, chọn trước;
  - $$w_{t+1}=\operatorname{proj}_W\big(w_t-\eta_t\nabla\ell(w_t,z_{i_t})\big).$$
  - Đầu ra $A(S;\xi)=w_{T+1}$ (điểm lặp cuối, last iterate) hoặc $\bar w_T$; $\xi=(i_1,\ldots,i_T)$ độc lập với $S$.
  - Mục tiêu: chặn $\mathbb E_{S,\xi}[L_D(A(S;\xi))-L_S(A(S;\xi))]$ theo $m$, $T$ và $\eta_1,\ldots,\eta_T$.
- **Ghi chú diễn giả:** Cố định: $D$, $W$, $\ell$, các hằng số, $m$, $T$, các $\eta_t$, $w_1$. Ngẫu nhiên theo dữ liệu: $S$ và $L_S$; theo nguồn riêng của thuật toán: dãy chỉ số $\xi$, có $m^T$ giá trị đồng khả năng; điểm lặp ngẫu nhiên theo cả hai. Với $\eta_t$ hằng và đầu ra $\bar w_T$, đây là Thuật toán 05.11 với oracle rút đều của Hệ quả 05.19; với $W=\mathbb R^p$, đây là thuật toán của thí nghiệm mở đầu. Rút có hoàn lại, mỗi quan sát được dùng trung bình $T/m$ lần, nên điểm lặp phụ thuộc quan sát sắp dùng và Hệ quả 06.2 không áp dụng khi $T\ge2$. Mục tiêu thứ hai là rủi ro vượt mức kì vọng so với $\inf_WL_D$. Nguồn: ghi chú Bài 08, §1, Thuật toán 08.1 và hai đoạn sau.
- **Lý do / nối:** khung chung và thuật toán trước mọi kết quả → giả thiết.
- **Mục tiêu / nguồn:** 1, 3; §1, §4.

#### `2-02` Giả thiết — thiết lập (§2) · 2,5 phút
- **Mặt trang:**
  - Với mọi $z\in\mathcal Z$: (S) $\ell(\cdot,z)$ lồi và $\beta$-trơn trên toàn $\mathbb R^p$; (S′) chỉ $\beta$-trơn.
  - (G) $\lVert\nabla\ell(w,z)\rVert\le G$ với mọi $w\in W$; $W$ lồi nên (L): $\lvert\ell(u,z)-\ell(v,z)\rvert\le G\lVert u-v\rVert$.
  - Độ dài bước $0<\eta_t\le2/\beta$ tất định; (I) $\Pr(i_t=i)=1/m$ với mọi $t$, $i$.
  - (R) $\sup_{u\in W}\lVert w_1-u\rVert\le R<\infty$; (X) $\lVert x\rVert\le C_x$ với mô hình tuyến tính.
  - Dưới (X), hàm lỗi logistic $\ln\big(1+e^{-\tilde y\langle w,x\rangle}\big)$, $\tilde y=2y-1$, thỏa (S) với $\beta=C_x^2/4$, (G) với $G=C_x$ trên $\mathbb R^p$.
- **Ghi chú diễn giả:** Lượng từ "với mọi $z\in\mathcal Z$" chạy trên mọi quan sát, kể cả quan sát ngoài tập huấn luyện; quan sát kiểm tra cần điều này. (S) đòi tính trơn trên toàn $\mathbb R^p$, không chỉ trên $W$, vì chứng minh tính đồng bức dùng điểm có thể nằm ngoài $W$. (L) suy từ (G) theo định lý giá trị trung bình dọc đoạn thẳng trong $W$ lồi. Hàm lỗi bình phương thỏa (S) với $\beta=2C_x^2$, nhưng (G) chỉ đúng khi $W$ bị chặn: với quả cầu bán kính $B$ và $\lvert y\rvert\le C_y$, $G=2(BC_x+C_y)C_x$. Hàm lỗi bản lề (hinge loss) và hàm lỗi của mạng ReLU theo trọng số không thỏa (S). Các kết quả cho hàm lỗi lồi không cần hàm lỗi bị chặn (T3). Nguồn: ghi chú Bài 08, §2.
- **Lý do / nối:** mọi giả thiết của bài ở một chỗ, như §2 của ghi chú → ví dụ xuyên suốt.
- **Mục tiêu / nguồn:** 2, 5; §2.

#### `2-03` Ví dụ: hàm lỗi Huber và hồi quy logistic nhiều vòng — ví dụ xuyên suốt (Ví dụ 08.1, khối ứng dụng §3), hai thẻ · 2,5 phút
- **Mặt trang** {{hai thẻ `grid2`}}:
  - {{thẻ trái}} **Ví dụ 08.1.** $\mathcal Z=W=\mathbb R$; tập huấn luyện $z_1=0$, $z_2=1$, $z_3=2$, $z_4=3$, $m=4$.
  - Hàm lỗi Huber (Huber loss): $\ell_{\mathrm H}(w,z)=\tfrac12(w-z)^2$ khi $\lvert w-z\rvert\le1$, $\lvert w-z\rvert-\tfrac12$ khi $\lvert w-z\rvert>1$.
  - Đạo hàm là $w-z$ cắt vào $[-1,1]$: lồi, $1$-trơn, $G=1$; điều kiện $\eta_t\le2$.
  - {{thẻ phải, tiêu đề thẻ h3 "Hồi quy logistic nhiều vòng"}} $\lVert x\rVert\le1$, $W$ quả cầu bán kính $5$, $w_1=0$, $m=10^4$.
  - Một vòng, mỗi hồ sơ một lần: cận $5/\sqrt{10^4+1}\approx0{,}05$ (Nhận xét 06.3).
  - **Câu hỏi:** chạy nhiều vòng trên cùng $10^4$ hồ sơ có cho cận nhỏ hơn không?
- **Ghi chú diễn giả:** Đạo hàm của hàm lỗi Huber là $\max\{-1,\min\{1,w-z\}\}$. Nó không giảm theo $w$, nên hàm lỗi lồi; nó $1$-Lipschitz, nên hàm lỗi $1$-trơn; trị tuyệt đối không quá $1$, nên (G) đúng với $G=1$ trên toàn $\mathbb R$, không cần dữ liệu bị chặn. Với $w_1=0$, $\eta=\tfrac12$ và dãy chỉ số $(1,4,2,3,4,1)$, sáu bước cho $w_2,\ldots,w_7$ bằng $0$; $\tfrac12$; $\tfrac34$; $\tfrac54$; $\tfrac74$; $\tfrac54$; ở bước $2$, $w_2-z_4=-3$ bị cắt thành $-1$. Cận một vòng của ứng dụng là cận rủi ro vượt mức kì vọng của Bài 06; câu hỏi thực hành của ghi chú có thêm vế "với độ dài bước $0{,}05$, nên chạy bao nhiêu bước". Nguồn: ghi chú Bài 08, §3, Ví dụ 08.1 và khối ứng dụng.
- **Lý do / nối:** hai đối tượng xuyên suốt đặt ở mục của ghi chú (§3) → định nghĩa ghép cặp.
- **Mục tiêu / nguồn:** 1, 4; §3.

#### `2-04` Hai lần chạy ghép cặp — định nghĩa (Định nghĩa 08.2) · 2,5 phút
- **Mặt trang:**
  - **Định nghĩa 08.2.** Hai lần chạy ghép cặp (coupled runs): Thuật toán 08.1 trên $s$ ($w_t$) và trên $s^{(i)}$ ($w'_t$),
  - dùng chung $w_1=w'_1$, các $\eta_t$ và dãy chỉ số $\xi$.
  - Bước chung (shared step), $i_t\ne i$: hai lần chạy dùng cùng $z_{i_t}$.
  - Bước khác biệt (differing step), $i_t=i$: $z_i$ ở lần thứ nhất, $z'$ ở lần thứ hai.
  - $\Delta_t=\lVert w_t-w'_t\rVert$, $\Delta_1=0$; ngân sách độ dài bước (cumulative step-size budget) $\sum_{t=1}^T\eta_t$.
- **Ghi chú diễn giả:** Tập huấn luyện $s$, chỉ số $i$, quan sát thay thế $z'$ và mẫu lân cận $s^{(i)}$ là các điểm cố định bất kì như Định nghĩa 06.9; chỉ $\xi$ là ngẫu nhiên. Với độ dài bước hằng, ngân sách bằng $\eta T$. Kí hiệu $\Delta_t$ ở bài này là khoảng cách giữa hai lần chạy, khác $\lVert w_t-u\rVert^2$ trong chứng minh Định lý 05.14. Với rút đều có hoàn lại, mỗi bước là bước khác biệt với xác suất $1/m$, nên trong $T$ bước có trung bình $T/m$ bước khác biệt. Nguồn: ghi chú Bài 08, §4, Định nghĩa 08.2 và đoạn sau.
- **Lý do / nối:** định nghĩa sau thiết lập; trực quan và ví dụ ngay sau.
- **Mục tiêu / nguồn:** 1; Định nghĩa 08.2.

#### `2-05` Ghép cặp và hiệu hai kì vọng — trực quan, ví dụ (đoạn sau Định nghĩa 08.2) · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Từng lần chạy giữ phân bố cũ, nên hai kì vọng của Định nghĩa 06.9 không đổi.
  - Hai lần chạy trên cùng không gian của $\xi$; theo bất đẳng thức Jensen: $\lvert\mathbb E_\xi a-\mathbb E_\xi b\rvert\le\mathbb E_\xi\lvert a-b\rvert$.
  - **Ví dụ.** Một bước, $s=(0,1,2,3)$, $s^{(4)}=(0,1,2,-3)$, $w_1=0$, $\eta=\tfrac12$.
  - Theo $i_1=1,\ldots,4$: $w_2=0;\tfrac12;\tfrac12;\tfrac12$ và $w'_2=0;\tfrac12;\tfrac12;-\tfrac12$, nên $\mathbb E_\xi w_2-\mathbb E_\xi w'_2=\tfrac38-\tfrac18=\tfrac14$.
  - Ghép cặp: $\mathbb E_\xi\lvert w_2-w'_2\rvert=\tfrac14$, đúng bằng hiệu; hai dãy chỉ số độc lập: $\tfrac38$, lớn hơn hiệu.
- **Ghi chú diễn giả:** Hai lần chạy chỉ khác nhau khi $i_1=4$, và khi đó $\lvert w_2-w'_2\rvert=1$, nên kì vọng theo $\xi$ bằng $\tfrac14$. Với hai dãy chỉ số độc lập, trong $16$ cặp chỉ số có $6$ cặp cho khoảng cách $\tfrac12$, $3$ cặp cho $1$ và $7$ cặp cho $0$, nên kì vọng là $(6\cdot\tfrac12+3)/16=\tfrac38$. Khoảng cách này gồm cả hiệu $\tfrac14$ do thay quan sát và phần do tính ngẫu nhiên của thuật toán. Ghép cặp bỏ phần thứ hai, nên chặn được hiệu hai kì vọng qua từng quỹ đạo. Nguồn: ghi chú Bài 08, §4, hai đoạn sau Định nghĩa 08.2.
- **Lý do / nối:** trọng tâm trực quan 1; vì sao chỉ cần chặn $\mathbb E_\xi\Delta$ → hai quỹ đạo của ví dụ Huber.
- **Mục tiêu / nguồn:** 1; §4.

#### `2-06` Ví dụ: hai lần chạy ghép cặp trong ví dụ Huber — ví dụ (Ví dụ 08.2), hình F1 · 3 phút
- **Mặt trang:**
  - **Ví dụ 08.2.** Ví dụ 08.1 với $i=4$, $z'=-3$; $w_1=w'_1=0$, $\eta=\tfrac12$, $\xi=(1,4,2,3,4,1)$.
  - {{hình F1 `hai-lan-chay-huber.svg`, figcaption: "Ví dụ 08.2: điểm lặp $w_t$ trên $s=(0,1,2,3)$ và $w'_t$ trên $s^{(4)}=(0,1,2,-3)$, $t=1,\ldots,7$; bước khác biệt ở $t=2$ và $t=5$."}}
  - Bước khác biệt $t=2$: $\Delta$ từ $0$ lên $1$; $t=5$: từ $\tfrac34$ lên $\tfrac74$; mỗi lần tăng $1=2G\eta$.
  - Bước chung: $0\to0$, $1\to\tfrac34$, $\tfrac34\to\tfrac34$, $\tfrac74\to\tfrac54$; khoảng cách không tăng.
  - $\Delta_7=\tfrac54\le2\cdot2G\eta=2$.
- **Ghi chú diễn giả:** Ở bước $2$, $w'_2-z'=3$ bị cắt thành $1$, nên $w'_3=-\tfrac12$, còn $w_3=\tfrac12$. Đạo hàm tại $w'_t$ ở sáu bước lần lượt là $0;1;-1;-1;1;0$. Hai quỹ đạo tách nhau đúng ở hai bước dùng quan sát thứ tư, và giữa hai bước đó, các bước chung giữ hoặc giảm khoảng cách. Ví dụ chỉ xét một dãy chỉ số; Định nghĩa 06.9 cần kì vọng theo $\xi$, nên hai sự kiện "bước khác biệt tăng không quá $2G\eta$" và "bước chung không làm tăng" phải được chứng minh cho mọi dãy. Nguồn: ghi chú Bài 08, §4, Ví dụ 08.2 và đoạn sau.
- **Lý do / nối:** trọng tâm trực quan 1 (hai quỹ đạo tách xa chậm); câu hỏi cho bước chung → ánh xạ bước gradient.
- **Mục tiêu / nguồn:** 1; Ví dụ 08.2.

#### `2-07` Ánh xạ bước gradient và tính đồng bức — vấn đề, định nghĩa (đoạn mở §5, Định nghĩa 08.3) · 2,5 phút
- **Mặt trang:**
  - Ở bước chung, hai lần chạy áp dụng cùng ánh xạ $w\mapsto\operatorname{proj}_W\big(\Gamma_{\eta_t,z_{i_t}}(w)\big)$ cho $w_t$ và $w'_t$.
  - Ánh xạ bước gradient (gradient step map): $\Gamma_{\eta,z}(w)=w-\eta\nabla\ell(w,z)$.
  - **Định nghĩa 08.3.** $\Gamma$ có hệ số giãn (expansion factor) $\kappa$ nếu $\lVert\Gamma(u)-\Gamma(v)\rVert\le\kappa\lVert u-v\rVert$ với mọi $u,v$; không giãn (nonexpansive) khi $\kappa=1$.
  - $\nabla f$ là $\tfrac1\beta$-đồng bức (co-coercive) nếu với mọi $u,v$:
  - $$\langle\nabla f(u)-\nabla f(v),u-v\rangle\ge\tfrac1\beta\lVert\nabla f(u)-\nabla f(v)\rVert^2.$$
  - $f=\tfrac\beta2\lVert w\rVert^2$: dấu bằng; $f=-\tfrac12w^2$, $1$-trơn: vế trái âm khi $u\ne v$, không đồng bức.
- **Ghi chú diễn giả:** Câu hỏi của mục là ánh xạ này kéo hai điểm lại gần hay đẩy chúng ra xa. Hai tính chất dùng ngay: hợp của hai ánh xạ có hệ số giãn $\kappa_1$, $\kappa_2$ có hệ số giãn $\kappa_1\kappa_2$; phép chiếu lên tập đóng, lồi không giãn. Nếu $\nabla f$ là $\tfrac1\beta$-đồng bức thì theo bất đẳng thức Cauchy–Schwarz, $\nabla f$ là $\beta$-Lipschitz, tức $f$ là $\beta$-trơn; chiều ngược lại cần tính lồi. Với $f=\tfrac\beta2\lVert w\rVert^2$, hai vế cùng bằng $\beta\lVert u-v\rVert^2$; với $f=-\tfrac12w^2$, vế trái là $-(u-v)^2$. Nguồn: ghi chú Bài 08, §5, Định nghĩa 08.3 và ba đoạn sau.
- **Lý do / nối:** vấn đề của bước chung trên mặt trang (câu nối từ ví dụ) → bổ đề.
- **Mục tiêu / nguồn:** 2; §5.

#### `2-08` Bước gradient không giãn — trực quan, kết quả (Bổ đề 08.4) · 3 phút
- **Mặt trang:**
  - **Trực quan.** Một chiều, $f''\in[0,\beta]$: hệ số góc của $\Gamma(w)=w-\eta f'(w)$ là $1-\eta f''\in[1-\eta\beta,1]$; tính lồi cho cận trên $1$, $\eta\le2/\beta$ cho cận dưới $-1$.
  - **Bổ đề 08.4.** **Giả thiết:** $f$ lồi, $\beta$-trơn trên toàn $\mathbb R^p$; $0\le\eta\le2/\beta$; $W$ khác rỗng, đóng, lồi.
  - **Bảo đảm:** tất định, với $\Gamma(w)=w-\eta\nabla f(w)$, $g_{uv}=\nabla f(u)-\nabla f(v)$: (a) $\nabla f$ là $\tfrac1\beta$-đồng bức;
  - (b) $$\lVert\Gamma(u)-\Gamma(v)\rVert^2\le\lVert u-v\rVert^2-\eta\big(\tfrac2\beta-\eta\big)\lVert g_{uv}\rVert^2\le\lVert u-v\rVert^2;$$
  - (c) $w\mapsto\operatorname{proj}_W(\Gamma(w))$ không giãn.
- **Ghi chú diễn giả:** Câu trực quan đọc bổ đề trong trường hợp một chiều: hệ số góc của ánh xạ bước nằm giữa $-1$ và $1$, nên khoảng cách không tăng. Hàm lồi có đạo hàm bậc hai không âm, nên bước gradient không đẩy hai điểm xa hơn; độ dài bước không quá $2/\beta$ giữ cho bước không vượt quá xa sang phía bên kia. Bổ đề không cần $f$ khả vi hai lần. Phần (a) là phát biểu then chốt; với hàm lồi, tính $\beta$-trơn và tính $\tfrac1\beta$-đồng bức tương đương. Áp dụng với $f=\ell(\cdot,z_{i_t})$: ở mỗi bước chung, $\Delta_{t+1}\le\Delta_t$. Nguồn: ghi chú Bài 08, §5, Bổ đề 08.4 (phác thảo).
- **Lý do / nối:** trọng tâm trực quan 2; trực quan trước phát biểu trên cùng trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 2; Bổ đề 08.4.

#### `2-09` Ý tưởng chứng minh: bước gradient không giãn — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  1. Khai triển $\lVert(u-v)-\eta g_{uv}\rVert^2=\lVert u-v\rVert^2-2\eta\langle g_{uv},u-v\rangle+\eta^2\lVert g_{uv}\rVert^2$.
  2. (tính lồi, tính trơn qua (a)) Số hạng giữa $\le-\tfrac{2\eta}\beta\lVert g_{uv}\rVert^2$: bất đẳng thức đầu của (b).
  3. ($\eta\le2/\beta$) $\eta(2/\beta-\eta)\ge0$, bỏ số hạng: (b); hợp với phép chiếu không giãn: (c).
  4. (a): cận trên bậc hai (quadratic upper bound); $q_u$ cực tiểu tại $u$ nhờ tính lồi; đổi vai, cộng.
  - **Kỹ thuật.** $q_u=f-\langle\nabla f(u),\cdot\rangle$ lồi, $\beta$-trơn, $\nabla q_u(u)=0$; với $f=-\tfrac12w^2$, $q_u$ không có cực tiểu.
- **Ghi chú diễn giả** (~180 âm tiết): Bất đẳng thức then chốt là tính đồng bức (a). Bước 1 là đại số. Bước 2 dùng (a) cho số hạng tích vô hướng, nên tính lồi và tính trơn của $f$ vào ở đây. Bước 3 là chỗ duy nhất dùng $\eta\le2/\beta$; với $\eta>2/\beta$ hệ số âm và bất đẳng thức thứ hai hỏng (hàm bậc hai với $\eta=3$ cho hệ số giãn $2$). Phần (a) chứng minh ở Phụ lục A theo bốn dòng: cận trên bậc hai $f(v)\le f(u)+\langle\nabla f(u),v-u\rangle+\tfrac\beta2\lVert v-u\rVert^2$ chỉ cần tính trơn; hàm phụ $q_u$ đạt cực tiểu toàn cục tại $u$ vì nó lồi và có gradient bằng $0$ tại đó, đây là dòng duy nhất dùng tính lồi; áp dụng cận trên bậc hai cho $q_u$ tại điểm $v-\tfrac1\beta\nabla q_u(v)$, điểm này có thể nằm ngoài $W$, nên (S) cần đúng trên toàn $\mathbb R^p$; đổi vai $u$, $v$ rồi cộng hai bất đẳng thức, các giá trị $f(u)$, $f(v)$ triệt tiêu. Nguồn: ghi chú Bài 08, chứng minh Bổ đề 08.4; Phụ lục A.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; chỗ dùng tính lồi và điều kiện độ dài bước → ví dụ kiểm hai điều kiện.
- **Mục tiêu / nguồn:** 2; chứng minh Bổ đề 08.4, Phụ lục A.

#### `2-10` Ví dụ: hệ số giãn của bước gradient một chiều — ví dụ (Ví dụ 08.3), kiểm tra · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 08.3.** $p=1$, $W=\mathbb R$, $\beta=1$; hệ số giãn nhỏ nhất: trị tuyệt đối lớn nhất của hệ số góc của $\Gamma$.
  - Bậc hai $\tfrac12w^2$: $\lvert1-\eta\rvert$; Huber: $\max\{\lvert1-\eta\rvert,1\}$; lõm $-\tfrac12w^2$: $1+\eta$.
  - Bảng: $\eta$ | Bậc hai | Huber | Lõm; $\tfrac12$ | $\tfrac12$ | $1$ | $\tfrac32$; $2$ | $1$ | $1$ | $3$; $3$ | $2$ | $2$ | $4$.
  - Ngưỡng $2/\beta$ chặt: hàm bậc hai cho $1$ khi $\eta=2$, $2$ khi $\eta=3$; hàm lõm giãn với mọi $\eta>0$.
  - Ở bước khác biệt, hai ánh xạ $\Gamma_{\eta_t,z_i}$ và $\Gamma_{\eta_t,z'}$ khác nhau, nên Bổ đề 08.4 không chặn $\Delta_{t+1}$.
- **Ghi chú diễn giả:** Với hàm bậc hai, $\Gamma(w)=(1-\eta)w$. Với hàm lỗi Huber, $\Gamma$ có hệ số góc $1-\eta$ khi $\lvert w-z\rvert<1$ và $1$ khi $\lvert w-z\rvert>1$, vì ở đó đạo hàm là hằng $\pm1$. Với hàm lõm, $\Gamma(w)=(1+\eta)w$. Ánh xạ tuyến tính từng khúc và liên tục trên $\mathbb R$ có hệ số giãn nhỏ nhất bằng trị tuyệt đối lớn nhất của hệ số góc. Cột "Lõm" cho thấy không có tính lồi thì bước gradient giãn với mọi độ dài bước dương, dù hàm vẫn $1$-trơn. Dòng cuối nêu chỗ còn thiếu: ở bước khác biệt, hai lần chạy không dùng cùng một ánh xạ. Nguồn: ghi chú Bài 08, §5, Ví dụ 08.3 và đoạn cuối §5.
- **Lý do / nối:** kiểm cả hai điều kiện của bổ đề bằng số; câu nối sang mạch 3 trên mặt trang (dòng cuối) → bài tập.
- **Mục tiêu / nguồn:** 2, 5; Ví dụ 08.3.

#### `2-11` Bài tập: bước gradient của hàm lỗi Huber — bài tập (Bài tập 08.3(a)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 08.3(a).** $\ell_{\mathrm H}$ ($\beta=1$), $z$ cố định, $d(w)=\partial_w\ell_{\mathrm H}(w,z)$. Không dùng Bổ đề 08.4, chứng minh trực tiếp
  - với $0\le\eta\le2$, mọi $u,v\in\mathbb R$: $\lvert\Gamma_{\eta,z}(u)-\Gamma_{\eta,z}(v)\rvert\le\lvert u-v\rvert$, chỉ dùng: $d$ không giảm và $1$-Lipschitz.
  - Tính chất nào đến từ tính lồi? Nêu một cặp $u,v$ cho thấy kết luận sai khi $\eta=3$.
  - **Lời giải:** $u>v$, $\delta=d(u)-d(v)\in[0,u-v]$: $(1-\eta)(u-v)\le\Gamma(u)-\Gamma(v)=(u-v)-\eta\delta\le u-v$.
  - Tính không giảm (từ tính lồi) cho cận trên; $\eta\le2$ cho cận dưới, vì $\lvert1-\eta\rvert\le1$.
  - $\eta=3$, $z=0$, $u=0{,}2$, $v=-0{,}2$: $\Gamma(w)=-2w$ trên $[-1,1]$, $\lvert\Gamma(u)-\Gamma(v)\rvert=0{,}8=2\lvert u-v\rvert$.
- **Ghi chú diễn giả:** Gợi ý của tệp bài tập: viết $\Gamma(u)-\Gamma(v)$ theo $u-v$ và $d(u)-d(v)$. Tính không giảm của $d$ đến từ tính lồi của hàm lỗi Huber, tính $1$-Lipschitz đến từ tính $1$-trơn. Khi $u=v$ hai vế bằng $0$, nên chỉ cần xét $u>v$. Nếu $\delta$ có thể âm, như với hàm lõm, hiệu có thể vượt $u-v$; nếu $\eta>2$, cận dưới $(1-\eta)(u-v)$ nhỏ hơn $-(u-v)$. Hệ số $2$ khi $\eta=3$ khớp cột Huber của Ví dụ 08.3. Nguồn: tệp bài tập, Bài tập 08.3(a), gợi ý và lời giải.
- **Lý do / nối:** bài tập của cụm bước gradient không giãn, từ `exercises.md`, cùng dữ liệu Huber → tiêu đề mạch 3.
- **Mục tiêu / nguồn:** 2, 5; Bài tập 08.3(a).

### Mạch 3. Bất đẳng thức truy hồi (5 trang, 13 phút)

#### `3-00` 3. Bất đẳng thức truy hồi — tiêu đề mạch, điểm vào mạch 3 · 0,5 phút
- **Mặt trang:** "3."; h2 "Bất đẳng thức truy hồi"; `p.strand-lead` (bảng mạch, 24 âm tiết); `p.strand-keys`: "bất đẳng thức truy hồi · ngân sách độ dài bước · thừa số $1/m$".
- **Ghi chú diễn giả:** Ở bước chung, Bổ đề 08.4 cho $\Delta_{t+1}\le\Delta_t$. Ở bước khác biệt, cận gradient (G) giới hạn phần tăng. Ghép hai trường hợp, ta được một bất đẳng thức truy hồi cho $\Delta_t$ trên từng quỹ đạo, rồi lấy kì vọng theo dãy chỉ số. Thừa số $1/m$ của mọi cận về sau xuất hiện ở bước lấy kì vọng này. Nguồn: ghi chú Bài 08, §6, đoạn mở.
- **Lý do / nối:** câu nối của 2-10 → mệnh đề.
- **Mục tiêu / nguồn:** 3; §6.

#### `3-01` Bất đẳng thức truy hồi cho hai lần chạy ghép cặp — trực quan, kết quả (Mệnh đề 08.5) · 3 phút
- **Mặt trang:**
  - **Trực quan.** $\Delta$ chỉ tăng ở bước khác biệt, mỗi lần $\le2G\eta_t$; trung bình có $T/m$ bước như vậy.
  - **Mệnh đề 08.5.** **Giả thiết:** (S), (G); $s,i,z'$ cố định; hai lần chạy ghép cặp, $0<\eta_t\le2/\beta$; (I).
  - **Bảo đảm:** (a) bất đẳng thức truy hồi (recurrence inequality), tất định, mọi $\xi$, $t$: $\Delta_{t+1}\le\Delta_t+2G\eta_t\mathbb 1[i_t=i]$, nên $\Delta_{T+1}\le2G\sum_t\eta_t\mathbb 1[i_t=i]$;
  - (b) kì vọng theo $\xi$, với tập huấn luyện cố định:
  - $$\mathbb E\Delta_{T+1}\le\frac{2G}m\sum_{t=1}^T\eta_t.$$
- **Ghi chú diễn giả:** Cận không phụ thuộc phân bố $D$ và số chiều $p$. Phần (a) là khẳng định trên từng quỹ đạo: với mọi dãy chỉ số, khoảng cách cuối không quá $2G$ nhân tổng độ dài bước của các bước khác biệt. Phần (b) cũng có dạng một bước: $\mathbb E\Delta_{t+1}\le\mathbb E\Delta_t+2G\eta_t/m$. Thừa số $1/m$ là xác suất một bước dùng quan sát khác biệt. Khi xáo trộn lại sau mỗi vòng qua dữ liệu (random reshuffling), mỗi vòng là một hoán vị đều của $\{1,\ldots,m\}$; các $i_t$ không độc lập nhưng (I) vẫn đúng, nên mệnh đề giữ nguyên. Hằng số $2G$ không giảm được: với hàm lỗi Huber, $w_t=w'_t=1$, $z_i=3$, $z'=-3$, $\eta=\tfrac12$, hai bước cho $\tfrac32$ và $\tfrac12$. Nguồn: ghi chú Bài 08, §6, Mệnh đề 08.5 và hai đoạn sau; Phụ lục B(i).
- **Lý do / nối:** vấn đề ở 2-10, ví dụ ở 2-06; trực quan và phát biểu chung trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 3; Mệnh đề 08.5.

#### `3-02` Ý tưởng chứng minh: bất đẳng thức truy hồi — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - **Nhắc lại:** tổng triệt tiêu (Bài 05): cộng các bất đẳng thức một bước.
  1. ((S), $\eta_t\le2/\beta$) Bước chung: cùng ánh xạ $\operatorname{proj}_W\circ\Gamma_{\eta_t,z_{i_t}}$, Bổ đề 08.4(c) cho $\Delta_{t+1}\le\Delta_t$.
  2. ((G), phép chiếu không giãn) Bước khác biệt, $g_t=\nabla\ell(w_t,z_i)$, $g'_t=\nabla\ell(w'_t,z')$: $\Delta_{t+1}\le\Delta_t+\eta_t\lVert g_t\rVert+\eta_t\lVert g'_t\rVert\le\Delta_t+2G\eta_t$.
  3. Tổng triệt tiêu từ $\Delta_1=0$: (a), trên từng quỹ đạo.
  4. ((I)) Lấy kì vọng, $\mathbb E\,\mathbb 1[i_t=i]=1/m$: (b); không cần $i_t$ độc lập với $\Delta_t$.
- **Ghi chú diễn giả** (~170 âm tiết): Bất đẳng thức then chốt là (a), chứng minh trên từng quỹ đạo. Ở bước 2, $g_t=\nabla\ell(w_t,z_i)$ và $g'_t=\nabla\ell(w'_t,z')$; (G) dùng hai lần, tại $w_t$ và $w'_t$, hai điểm thuộc $W$ vì $w_1\in W$ và mỗi điểm lặp sau là một phép chiếu lên $W$. Bước này không dùng tính lồi của hàm lỗi hay điều kiện độ dài bước. Tính lồi và điều kiện độ dài bước chỉ vào ở bước 1, qua Bổ đề 08.4. Ở bước 4, dãy $\xi$ có hữu hạn giá trị, nên mọi kì vọng là trung bình hữu hạn; bước này chỉ dùng tính tuyến tính của kì vọng và xác suất biên của $i_t$. Vì (a) đúng với mọi dãy, không cần biết $i_t$ phụ thuộc lịch sử thế nào; đó là lý do kết quả đúng cả với xáo trộn lại. Bỏ tính lồi, bước 1 hỏng: hàm lỗi cosin là phản ví dụ. Nguồn: ghi chú Bài 08, chứng minh Mệnh đề 08.5; Phụ lục B(i).
- **Lý do / nối:** trang ý tưởng chứng minh riêng; giả thiết theo từng bước → kiểm bằng số.
- **Mục tiêu / nguồn:** 3; chứng minh Mệnh đề 08.5.

#### `3-03` Ví dụ: kì vọng của khoảng cách trong ví dụ Huber — ví dụ (Ví dụ 08.4), kiểm tra · 3 phút
- **Mặt trang:**
  - **Ví dụ 08.4.** Ví dụ 08.2 với $\xi$ đều trên $\{1,2,3,4\}^T$; $G=1$, $m=4$, $\eta=\tfrac12$: cận (b) là $T/4$.
  - $T=1$: $\Delta_2=1$ khi $i_1=4$, nên $\mathbb E\Delta_2=\tfrac14$, dấu bằng.
  - $T=2$, liệt kê $16$ dãy: $\mathbb E\Delta_3=\tfrac{29}{64}\approx0{,}4531<\tfrac12$.
  - $T=6$, liệt kê $4096$ dãy: $\mathbb E\Delta_7\approx0{,}8705\le1{,}5$.
  - Dãy $(2,3,1,4,4,4)$: $w_7=2$, $w'_7=-1$, $\Delta_7=3=2G\eta\cdot3$, đạt cận (a).
  - **Diễn giải:** bước chung kéo hai lần chạy lại gần ($i_1=4$, $i_2=1$: $\Delta$ từ $1$ xuống $\tfrac12$), nên kì vọng tăng chậm hơn cận.
- **Ghi chú diễn giả:** Với $T=2$, nhóm $i_1\ne4$ gồm $12$ dãy: bước đầu là bước chung, nên $w_2=w'_2$; nếu $i_2=4$, hai đạo hàm là $-1$ và $1$, và $\Delta_3=1$; tổng của nhóm là $3$. Nhóm $i_1=4$ gồm $4$ dãy, với $\Delta_3$ lần lượt $\tfrac12$; $\tfrac34$; $1$; $2$ theo $i_2=1,\ldots,4$, tổng $\tfrac{17}4$. Do đó $\mathbb E\Delta_3=(3+\tfrac{17}4)/16=\tfrac{29}{64}$. Giá trị với $T=6$ là $228\,203/262\,144$, tính bằng máy. Trên dãy $(2,3,1,4,4,4)$, hai lần chạy trùng nhau đến hết bước $3$, rồi ba bước khác biệt liên tiếp mỗi bước thêm đúng $1$. Nguồn: ghi chú Bài 08, §6, Ví dụ 08.4.
- **Lý do / nối:** cận đạt dấu bằng ở bước đầu và trên một quỹ đạo, lỏng theo kì vọng → bài tập.
- **Mục tiêu / nguồn:** 1, 3; Ví dụ 08.4.

#### `3-04` Bài tập: ví dụ Huber với độ dài bước 1 — bài tập (Bài tập 08.1(c)), lời giải trên mặt trang · 3,5 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 08.1(c).** Ví dụ 08.2 ($s=(0,1,2,3)$, $s^{(4)}=(0,1,2,-3)$, $w_1=w'_1=0$), rút đều có hoàn lại, $\eta=1$.
  - Tính $\mathbb E\Delta_2$, $\mathbb E\Delta_3$ bằng liệt kê, so với cận của Mệnh đề 08.5(b);
  - chỉ ra các dãy $(i_1,i_2)$ có $\Delta_3$ nhỏ hơn ngặt cận của Mệnh đề 08.5(a) trên dãy đó.
  - **Lời giải:** $\eta=1\le2/\beta$, cận (b) là $T/2$; $\mathbb E\Delta_2=\tfrac24=\tfrac12$, bằng cận.
  - $T=2$: nhóm $i_1\ne4$ tổng $6$, nhóm $i_1=4$ tổng $0+1+2+4=7$; $\mathbb E\Delta_3=\tfrac{13}{16}<1$.
  - Hụt so với cận (a): $(4,1)$ hụt $2$, $(4,2)$ hụt $1$; $\tfrac3{16}=1-\tfrac{13}{16}$.
- **Ghi chú diễn giả** (~150 âm tiết): Gợi ý của tệp bài tập: kiểm điều kiện độ dài bước, rồi nhóm $16$ dãy theo $i_1$ như Ví dụ 08.4; với $\eta=1$, bước chung với $z=0$ đưa mọi $w\in[-1,1]$ về $0$. Ở bước đầu với $i_1=4$: $w_2=0-(-1)=1$, $w'_2=0-1=-1$. Trong nhóm $i_1\ne4$, nếu $i_2=4$ thì hai đạo hàm là $-1$ và $1$, nên $\Delta_3=2$; ba dãy như vậy cho tổng $6$. Với $(4,2)$: $w_2-1=0$ giữ $w_3=1$, còn $w'_2-1=-2$ bị cắt thành $-1$, nên $w'_3=0$. Mọi bước khác biệt trong liệt kê làm $\Delta$ tăng đúng $2G\eta=2$; phần hụt so với cận chỉ đến từ bước chung, khớp hệ số giãn $\lvert1-\eta\rvert=0$ của Ví dụ 08.3. Kiểm tra: cùng phép liệt kê với $\eta=\tfrac12$ cho lại $\tfrac{29}{64}$. Nguồn: tệp bài tập, Bài tập 08.1(c), gợi ý và lời giải.
- **Lý do / nối:** bài tập của cụm bất đẳng thức truy hồi, từ `exercises.md`; câu nối sang mạch 4 trên 4-01 → tiêu đề mạch 4.
- **Mục tiêu / nguồn:** 1, 3; Bài tập 08.1(c).

### Mạch 4. Tính ổn định đều của hạ gradient ngẫu nhiên (7 trang, 20 phút)

#### `4-00` 4. Tính ổn định đều của hạ gradient ngẫu nhiên — tiêu đề mạch, điểm vào mạch 4 · 0,5 phút
- **Mặt trang:** "4."; h2 "Tính ổn định đều của hạ gradient ngẫu nhiên"; `p.strand-lead` (bảng mạch, 23 âm tiết); `p.strand-keys`: "ổn định đều · điểm lặp cuối · điểm lặp trung bình · thí nghiệm ghép cặp".
- **Ghi chú diễn giả:** Mệnh đề 08.5 chặn khoảng cách giữa hai tham số; Định nghĩa 06.9 cần hiệu hàm lỗi tại mọi quan sát kiểm tra. Tính Lipschitz của hàm lỗi nối hai đại lượng này, và Định lý 06.10 chuyển hệ số ổn định thành cận khoảng cách tổng quát hóa kì vọng. Với thí nghiệm mở đầu, cận là $t/200$, và các khoảng cách đo được nằm dưới cận. Nguồn: ghi chú Bài 08, §7, đoạn mở.
- **Lý do / nối:** mạch 3 → định lý.
- **Mục tiêu / nguồn:** 3; §7.

#### `4-01` Tính ổn định đều của SGD — trực quan, kết quả (Định lý 08.6) · 3,5 phút
- **Mặt trang:**
  - **Trực quan.** Hai lần chạy gần nhau thì, theo (L), hàm lỗi gần nhau tại mọi $z$.
  - **Định lý 08.6.** **Giả thiết:** (T1), (T2), (S), (G); $W$ khác rỗng, đóng, lồi, $w_1\in W$ tất định;
  - Thuật toán 08.1, $0<\eta_t\le2/\beta$ tất định, $\xi$ độc lập với $S$, đầu ra $w_{T+1}$.
  - **Bảo đảm:** (a) mọi $s,i,z',z$: $\mathbb E_\xi\lvert\ell(w_{T+1},z)-\ell(w'_{T+1},z)\rvert\le\frac{2G^2}m\sum_t\eta_t$; (b) ổn định đều, $\epsilon_{\mathrm{stab}}(m)$ bằng số đó;
  - (c) kì vọng theo $(S,\xi)$:
  - $$\big\lvert\mathbb E_{S,\xi}[L_D(w_{T+1})-L_S(w_{T+1})]\big\rvert\le\frac{2G^2}m\sum_{t=1}^T\eta_t.$$
- **Ghi chú diễn giả:** Mệnh đề 08.5 chặn khoảng cách giữa hai đầu ra; Định nghĩa 06.9 đòi hiệu hàm lỗi tại mọi quan sát kiểm tra, kể cả quan sát ngoài tập huấn luyện, và (L) nối hai đại lượng. Cận không phụ thuộc số chiều $p$ hay kích thước của $W$, và phụ thuộc quỹ đạo chỉ qua ngân sách độ dài bước. Đơn vị của cận: gấp đôi ngân sách độ dài bước thì cận gấp đôi; gấp đôi cỡ mẫu thì cận giảm một nửa. Với độ dài bước hằng, vế phải là $2G^2\eta T/m$. Đây là bảo đảm cấp thuật toán, theo kì vọng: không có cận với xác suất cao, và cận chặn trị tuyệt đối của kì vọng, không chặn kì vọng của trị tuyệt đối. Nguồn: ghi chú Bài 08, §7, đoạn mở, Định lý 08.6.
- **Lý do / nối:** trọng tâm trực quan 4; trực quan và phát biểu chung trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 3; Định lý 08.6.

#### `4-02` Ý tưởng chứng minh: tính ổn định đều của SGD — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - **Nhắc lại:** Định lý 06.10 dựa trên lập luận đổi vai (Bài 06).
  1. ((G), $W$ lồi) Định lý giá trị trung bình: (L), không cần tính lồi của hàm lỗi.
  2. (Mệnh đề 08.5(b)) $\mathbb E_\xi\lvert\ell(w_{T+1},z)-\ell(w'_{T+1},z)\rvert\le G\,\mathbb E_\xi\Delta_{T+1}\le\frac{2G^2}m\sum_t\eta_t$: (a).
  3. (ghép cặp, Jensen) Hiệu hai kì vọng $\le$ kì vọng của trị tuyệt đối: (b).
  4. ((G), (T2)) $\lVert w_{T+1}-w_1\rVert\le G\sum_t\eta_t$, nên $\mathbb EL_D(w_{T+1})<\infty$; Định lý 06.10, (T1): (c).
- **Ghi chú diễn giả** (~160 âm tiết): Bất đẳng thức then chốt là Mệnh đề 08.5(b). Ở bước 1, hàm $r\mapsto\ell(v+r(u-v),z)$ khả vi trên $[0,1]$; định lý giá trị trung bình và Cauchy–Schwarz cho $\lvert\ell(u,z)-\ell(v,z)\rvert\le G\lVert u-v\rVert$, với (G) tại một điểm của đoạn thẳng, thuộc $W$ vì $W$ lồi. Ở bước 3, ghép cặp không đổi phân bố của từng lần chạy, nên hai kì vọng theo $\xi$ đúng là hai kì vọng của Định nghĩa 06.9. Ở bước 4, phép chiếu không giãn và $w_1=\operatorname{proj}_W(w_1)$ cho $\lVert w_{t+1}-w_1\rVert\le\lVert w_t-w_1\rVert+\eta_tG$; khi đó $\mathbb E_{S,\xi}L_D(w_{T+1})\le L_D(w_1)+G^2\sum_t\eta_t$, hữu hạn theo (T2). Tính đo được ở Phụ lục B(ii). Định lý 06.10 dùng (T1), $\xi$ độc lập với $S$, tính ổn định đều, (T2) và tính khả tích. Hằng số $\beta$ chỉ vào qua điều kiện $\eta_t\le2/\beta$; tính lồi của hàm lỗi chỉ vào qua Bổ đề 08.4(a), ở các bước chung; tính lồi của $W$ cho tính không giãn của phép chiếu và tính Lipschitz. Nguồn: ghi chú Bài 08, chứng minh Định lý 08.6 và danh sách giả thiết sau chứng minh; Phụ lục B(ii).
- **Lý do / nối:** trang ý tưởng chứng minh riêng; nhắc lại kỹ thuật của Bài 06 bằng tên → ví dụ bằng số.
- **Mục tiêu / nguồn:** 3; chứng minh Định lý 08.6.

#### `4-03` Ví dụ: cận ổn định cho hồi quy logistic — ví dụ (Ví dụ 08.5) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 08.5.** Hàm lỗi logistic, $\lVert x\rVert\le1$ trên $\mathcal X$; $W=\mathbb R^p$ hoặc quả cầu bán kính $5$; $w_1=0$.
  - (S) với $\beta=\tfrac14$, (G) với $G=1$ (Bài tập 05.8); $\eta_t\le8$; $L_D(0)=\ln2$, nên (T2) đúng.
  - $m=10^6$, $\eta=0{,}05$, $T=10^4$ (Ví dụ 05.9): cận $\frac{2\cdot1\cdot0{,}05\cdot10^4}{10^6}=0{,}001$.
  - Thí nghiệm mở đầu, $m=200$, $\eta=0{,}5$: cận $\frac{2\cdot0{,}5\cdot t}{200}=\frac t{200}$, tức $1$ sau một vòng, $100$ sau $100$ vòng.
  - **Diễn giải:** cận tăng tuyến tính theo số bước và vượt $1$ ngay từ vòng thứ hai.
- **Ghi chú diễn giả:** Hằng số của hàm lỗi logistic với $\lVert x\rVert\le1$ là của Bài tập 05.8: đạo hàm theo điểm số nằm trong $(-1,0)$ và đạo hàm bậc hai không quá $\tfrac14$. Cận $0{,}001$ là cho điểm lặp cuối của ứng dụng một triệu hồ sơ của Bài 05, với ngân sách $500$. Cận nhỏ khi $T\eta$ nhỏ so với $m$. Trong thí nghiệm mở đầu, ngân sách sau $t$ bước là $0{,}5t$, nên cận đúng bằng số vòng ở cột đầu của bảng; điều kiện $\eta=0{,}5\le8$ thỏa. Nguồn: ghi chú Bài 08, §7, Ví dụ 08.5.
- **Lý do / nối:** áp dụng định lý cho hai thiết lập của bài; câu hỏi mở đầu nhận cận → đo trong thí nghiệm.
- **Mục tiêu / nguồn:** 3; Ví dụ 08.5.

#### `4-04` Ví dụ: hai lần chạy ghép cặp trong thí nghiệm mở đầu — ví dụ (Ví dụ 08.6), hình F2 · 4 phút
- **Mặt trang:**
  - **Ví dụ 08.6.** Thí nghiệm mở đầu; mẫu lân cận: quan sát rút đều thay bằng quan sát mới từ $D$.
  - Định lý 08.6 áp dụng; cận của $\mathbb E\Delta_{t+1}$ và của khoảng cách đều là $t/200$.
  - {{hình F2 `thi-nghiem-ghep-cap.svg`, figcaption: "Thí nghiệm mở đầu, trung bình $20$ hạt giống ở $0{,}5$; $1$; $5$; $20$; $100$ vòng: khoảng cách giữa lỗi kiểm tra và lỗi huấn luyện, $\Delta$ của hai lần chạy ghép cặp, và cận $t/200$; hai trục theo thang lôgarit."}}
  - Tỉ lệ đổi nhãn dự đoán (prediction flip rate) tăng từ $0{,}015$ lên $0{,}034$.
  - **Diễn giải:** ở $100$ vòng, $\Delta\approx5{,}458$, khoảng cách $0{,}919$, cận $100$; cả hai tăng chậm hơn tuyến tính.
- **Ghi chú diễn giả:** Cận lớn hơn khoảng cách đo được từ khoảng $11$ lần ở nửa vòng ($0{,}5/0{,}045$) đến khoảng $109$ lần ở $100$ vòng ($100/0{,}919$). Tỉ lệ đổi nhãn dự đoán là tỉ lệ quan sát kiểm tra mà hai lần chạy ghép cặp dự đoán nhãn khác nhau. Định lý 08.6 không chặn nó vì hàm lỗi 0–1 không Lipschitz theo $w$. Mệnh đề 08.5(b) chặn $\mathbb E_\xi\Delta_{t+1}$ cho từng cặp mẫu lân cận, nên cũng chặn trung bình theo các cặp. Ở $100$ vòng, $\Delta$ của các hạt giống nằm trong khoảng $1{,}31$–$15{,}08$, và khoảng cách trong khoảng $0{,}693$–$1{,}149$. Khoảng cách giữa lần chạy trên $S$ và một lần chạy với dãy chỉ số độc lập là $2{,}99$ ở nửa vòng và $4{,}00$ ở $100$ vòng: ghép cặp bỏ phần do tính ngẫu nhiên của thuật toán. Chạy lại với $\eta=0{,}25$ cho khoảng cách $0{,}651$ sau $100$ vòng, gần giá trị $0{,}650$ của $\eta=0{,}5$ sau $50$ vòng, cùng ngân sách $5000$. Nguồn: ghi chú Bài 08, §7, Ví dụ 08.6; Phụ lục F.
- **Lý do / nối:** câu trả lời bằng số cho câu hỏi mở đầu; trọng tâm trực quan 4 (hình) → điểm lặp trung bình.
- **Mục tiêu / nguồn:** 3, 5; Ví dụ 08.6.

#### `4-05` Tính ổn định của điểm lặp trung bình — trực quan, kết quả (Hệ quả 08.7), ví dụ · 3 phút
- **Mặt trang:**
  - Cận tối ưu của Bài 05 dùng $\bar w_T$, không dùng $w_{T+1}$.
  - **Trực quan.** Điểm lặp đầu của hai lần chạy còn gần nhau; hai trung bình gần nhau hơn.
  - **Hệ quả 08.7.** **Giả thiết:** như Định lý 08.6, đầu ra $\bar w_T=\frac1T\sum_{t=1}^Tw_t$. **Bảo đảm:** ổn định đều với
  - $$\epsilon_{\mathrm{stab}}(m)=\frac{2G^2}m\sum_{t=1}^{T-1}\frac{T-t}T\eta_t,$$
  - bằng $G^2\eta(T-1)/m$ khi bước hằng; cùng số chặn khoảng cách tổng quát hóa kì vọng của $\bar w_T$.
- **Ghi chú diễn giả:** Áp dụng cho chương trình chạy nhiều vòng của Ví dụ 06.3: hàm lỗi $(w-y)^2$ với $\lvert y\rvert\le1$, $W=[-1,1]$, $m=4$, $\eta=0{,}00625$, $T=1600$; (S) với $\beta=2$, (G) với $G=4$, nên cận là $39{,}975$, trong khi khoảng cách thật là $0{,}4750$. Lộ trình chứng minh: theo bất đẳng thức tam giác, $\lVert\bar w_T-\bar w'_T\rVert\le\frac1T\sum_t\Delta_t$; Mệnh đề 08.5(b) cho $t-1$ bước đầu chặn $\mathbb E\Delta_t$ bằng $\frac{2G}m\sum_{k<t}\eta_k$; đổi thứ tự lấy tổng, mỗi $\eta_k$ xuất hiện $T-k$ lần; rồi (L), tính khả tích và Định lý 06.10. Với bước hằng, $\sum_{k=1}^{T-1}(T-k)=T(T-1)/2$, nên hệ số nhỏ hơn một nửa hệ số $2G^2\eta T/m$ của điểm lặp cuối. Hàm lỗi trên $W$ nằm trong $[0,4]$, nên cận $39{,}975$ đúng nhưng không cho thông tin. Nguồn: ghi chú Bài 08, §7, Hệ quả 08.7, chứng minh và đoạn sau.
- **Lý do / nối:** đầu ra cần cho cận tối ưu; chương trình của Ví dụ 06.3 đi lên mặt trang ở bài tập ngay sau → bài tập theo số bước.
- **Mục tiêu / nguồn:** 3; Hệ quả 08.7.

#### `4-07` Bài tập: SGD có chiếu nhiều vòng cho hồi quy bình phương — bài tập (Bài tập 08.7(b)), lời giải trên mặt trang · 3,5 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 08.7.** Chương trình của Ví dụ 06.3: $(wx-y)^2$, $x=1$, $y=\pm1$, $W=[-1,1]$, $m=4$, $\eta=0{,}00625$, đầu ra $\bar w_T$; khoảng cách tổng quát hóa kì vọng đúng:
  - $$\psi(T)=\frac2m\Big(1-\frac{1-q^T}{2\eta T}\Big),\quad q=1-2\eta.$$
  - (b) Với $T\in\{11;161;1600\}$, tính cận của Hệ quả 08.7 và $\psi(T)$.
  - $T$ lớn nhất để cận không vượt độ rộng miền giá trị của hàm lỗi trên $W$, cho $\bar w_T$, $w_{T+1}$ (Định lý 08.6)?
  - **Lời giải:** $G=4$; cận $\frac{16\cdot0{,}00625}4(T-1)=0{,}025(T-1)$: $0{,}25;\ 4;\ 39{,}975$; $\psi(T)\approx0{,}0301;\ 0{,}2843;\ 0{,}4750$.
  - Hàm lỗi trong $[0,4]$: $T\le161$ cho $\bar w_T$; $0{,}05T\le4$, tức $T\le80$, cho $w_{T+1}$.
- **Ghi chú diễn giả** (~150 âm tiết): Gợi ý của tệp bài tập: Hệ quả 08.7 với độ dài bước hằng cho $G^2\eta(T-1)/m$, và trên $W$, $\lvert wx-y\rvert\le2$. Phần (a) của bài kiểm (S) với $\beta=2$, (G) với $G=4$ trên $W$, và chỉ ra (G) không đúng trên $\mathbb R$: với $x=1$, $y=0$, đạo hàm $2w$ không bị chặn. Với $q=0{,}9875$: $q^{11}\approx0{,}8708$, $q^{161}\approx0{,}1320$, $q^{1600}\approx1{,}8\cdot10^{-9}$. Cận có thông tin đến $T=161$, khoảng $40$ vòng qua bốn quan sát; cận của điểm lặp cuối $2G^2\eta T/m=0{,}05T$ chỉ đến $T=80$, tức $20$ vòng. Phần (c) chứng minh $\psi(T)<2/m=0{,}5$ với mọi $T$: cận tăng tuyến tính, còn giá trị đúng bị chặn. Nguồn: tệp bài tập, Bài tập 08.7, gợi ý và lời giải.
- **Lý do / nối:** bài tập của cụm tính ổn định đều, từ `exercises.md`; khoảng cách tổng quát hóa theo số bước → tiêu đề mạch 5.
- **Mục tiêu / nguồn:** 3; Bài tập 08.7(b).

### Mạch 5. Đánh đổi giữa tối ưu và ổn định (6 trang, 15 phút)

#### `5-00` 5. Đánh đổi giữa tối ưu và ổn định — tiêu đề mạch, điểm vào mạch 5 · 0,5 phút
- **Mặt trang:** "5."; h2 "Đánh đổi giữa tối ưu và ổn định"; `p.strand-lead` (bảng mạch, 25 âm tiết); `p.strand-keys`: "cận ghép · số bước tốt nhất · dừng sớm · chính quy hóa ngầm".
- **Ghi chú diễn giả:** Định lý 08.6 không chặn rủi ro kì vọng; cần thêm số hạng tối ưu. Mệnh đề 06.5(b) tách rủi ro vượt mức kì vọng của một đầu ra thành khoảng cách tổng quát hóa kì vọng và sai số tối ưu thực nghiệm kì vọng. Với hạ gradient ngẫu nhiên có chiếu, cận của số hạng thứ hai giảm khi số bước tăng, còn cận của số hạng thứ nhất tăng. Với $10^4$ hồ sơ, cận ghép cho biết chạy nhiều vòng có lợi hay không. Nguồn: ghi chú Bài 08, §8, đoạn mở.
- **Lý do / nối:** mạch 4 → hệ quả.
- **Mục tiêu / nguồn:** 4; §8.

#### `5-01` Rủi ro vượt mức kì vọng của SGD nhiều vòng — trực quan, kết quả (Hệ quả 08.8) · 3 phút
- **Mặt trang:**
  - **Nhắc lại:** Mệnh đề 06.5(b): $\mathbb EL_D(\tilde w)-\inf_WL_D\le\mathbb E[L_D(\tilde w)-L_S(\tilde w)]+\mathbb E\operatorname{opt}_S(\tilde w)$.
  - **Trực quan.** Khi $T$ tăng, cận tối ưu (Định lý 05.14) giảm, cận ổn định (Hệ quả 08.7) tăng.
  - **Hệ quả 08.8.** **Giả thiết:** (T1), (T2), (S), (G); $W$ khác rỗng, đóng, lồi, $w_1\in W$, (R); Thuật toán 08.1, $\eta$ hằng, $0<\eta\le2/\beta$, đầu ra $\bar w_T$.
  - **Bảo đảm:** kì vọng theo $(S,\xi)$; (a) $$\mathbb E_{S,\xi}L_D(\bar w_T)-\inf_WL_D\le\frac{R^2}{2\eta T}+\frac{\eta G^2}2+\frac{\eta G^2(T-1)}m;$$
  - (b) với $\eta^*=R/\big(G\sqrt{T+2T(T-1)/m}\big)\le2/\beta$: vế phải $RG\sqrt{(1+2(T-1)/m)/T}$, không quá $RG\sqrt{3/m}$ khi $T=m$, về $RG\sqrt{2/m}$ khi $T\to\infty$.
- **Ghi chú diễn giả:** Vế trái là rủi ro vượt mức kì vọng so với $W$, và cận không phụ thuộc $p$. Ở (b), giá trị giảm theo $T$ khi $m>2$. Cận ở (b) luôn lớn hơn cận $RG/\sqrt{m+1}$ của một vòng qua dữ liệu với quan sát mới (Nhận xét 06.3): khoảng $\sqrt3$ lần khi $T=m$ và khoảng $\sqrt2$ lần khi $T\to\infty$. Hệ quả chỉ phát biểu cho rút có hoàn lại, vì Định lý 05.14 đòi các lần rút độc lập; với xáo trộn lại, Định lý 08.6 vẫn đúng nhưng Định lý 05.14 không áp dụng nguyên văn. Nguồn: ghi chú Bài 08, §8, đoạn mở, Hệ quả 08.8; Phụ lục B(i).
- **Lý do / nối:** trực quan đánh đổi và phát biểu chung trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 4; Hệ quả 08.8.

#### `5-02` Ý tưởng chứng minh: rủi ro vượt mức kì vọng của SGD nhiều vòng — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - **Nhắc lại:** cân hai số hạng (Bài 05): $a/\eta+b\eta\ge2\sqrt{ab}$, dấu bằng tại $\eta=\sqrt{a/b}$.
  1. (Hệ quả 08.7) Khoảng cách tổng quát hóa kì vọng $\le\eta G^2(T-1)/m$.
  2. (Định lý 05.14; (S), $W$ lồi, (R)) Rút đều trên $s$ không chệch cho $\nabla L_s$: $\mathbb E_\xi\operatorname{opt}_s(\bar w_T)\le\frac{R^2}{2\eta T}+\frac{\eta G^2}2$.
  3. (Mệnh đề 06.5(b), (T1)) Cộng hai cận: (a).
  4. $a=\frac{R^2}{2T}$, $b=G^2\big(\frac12+\frac{T-1}m\big)$: $\eta^*$ và giá trị $2\sqrt{ab}$ của (b).
  - Ghép cận của $w_{T+1}$ là sai: Định lý 05.14 chỉ chặn $\bar w_T$.
- **Ghi chú diễn giả** (~160 âm tiết): Bất đẳng thức then chốt là Mệnh đề 06.5(b). Ở bước 2, oracle $\varphi(w,i)=\nabla\ell(w,z_i)$ thỏa (G1) với $F=L_s$ vì trung bình theo $i$ của nó bằng $\nabla L_s(w)$, và thỏa (G2) với hằng số $G$ theo (G); $L_s$ lồi theo (S) và $W$ đóng, lồi, nên (C) đúng. Định lý 05.14 cho cận với mọi $u\in W$; (R) cho $\lVert w_1-u\rVert\le R$, rồi lấy cận trên đúng theo $u$ và kì vọng theo $S$. Ở bước 1, các kì vọng hữu hạn như bước khả tích của Định lý 08.6, và $L_D(w)\le L_D(w_1)+GR$ trên $W$ là giả thiết hàm lỗi của Mệnh đề 06.5. Điều kiện $\eta^*\le2/\beta$ cần cho (a). Với hàm không trơn của Ví dụ 05.12, điểm lặp cuối không hội tụ. Nguồn: ghi chú Bài 08, §8, đoạn sau Hệ quả 08.8; Phụ lục C.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; giả thiết từng bước, cách ghép sai → ví dụ bằng số.
- **Mục tiêu / nguồn:** 4; chứng minh Hệ quả 08.8 (Phụ lục C).

#### `5-03` Ví dụ: số vòng qua dữ liệu cho hồi quy logistic — ví dụ (Ví dụ 08.7), hình F3 · 3 phút
- **Mặt trang:**
  - **Ví dụ 08.7.** Ứng dụng $10^4$ hồ sơ: $G=1$, $\beta=\tfrac14$, $W$ quả cầu bán kính $5$, $w_1=0$, $R=5$.
  - Một vòng, quan sát mới: $5/\sqrt{10\,001}\le0{,}0500$; $T=10^4$ với $\eta^*\approx0{,}0289$: $\le0{,}0866$; $T\to\infty$: $\le0{,}0708$.
  - $\eta=0{,}05$: vế phải $\frac{250}T+0{,}025+\frac{0{,}05(T-1)}{10^4}$, nhỏ nhất $0{,}0958$ tại $T^*\approx7071<m$.
  - {{hình F3 `danh-doi-so-buoc.svg`, figcaption: "Vế phải của Hệ quả 08.8(a) với $R=5$, $G=1$, $m=10^4$, $\eta=0{,}05$: số hạng tối ưu $250/T$, số hạng ổn định $0{,}05(T-1)/10^4$ và tổng (cộng hằng $0{,}025$); nhỏ nhất $0{,}0958$ tại $T^*\approx7071$; đường ngang $0{,}05$ là cận một vòng."}}
  - **Diễn giải:** theo các cận, nhiều vòng không cho cận nhỏ hơn một vòng: $0{,}0708$ so với $0{,}0500$.
- **Ghi chú diễn giả:** Bước $T=10^4$ rút có hoàn lại có cùng số bước với một vòng, nhưng là một thuật toán khác thuật toán theo thứ tự của Nhận xét 06.3. Theo Hệ quả 08.8(b), cận là $0{,}0791$ khi $T=2\cdot10^4$ và $0{,}0725$ khi $T=10^5$, rồi giảm về $5\sqrt{2\cdot10^{-4}}\le0{,}0708$. Với $\eta=0{,}05$, số hạng thứ nhất giảm, số hạng thứ ba tăng; đạo hàm theo $T$ bằng $0$ khi $T^2=5\cdot10^7$, tức $T^*=R\sqrt{m/2}/(\eta G)\approx7071$. Bảng của ghi chú: $0{,}1000$ tại $T=5000$ và $T=10^4$, $0{,}1375$ tại $2\cdot10^4$, $0{,}2800$ tại $5\cdot10^4$. $T^*$ làm nhỏ nhất vế phải, tức một tổng hai cận trên. Nguồn: ghi chú Bài 08, §8, Ví dụ 08.7.
- **Lý do / nối:** câu trả lời cho câu hỏi thực hành của 2-03; trọng tâm trực quan 4 (hình) → ba cách điều khiển đầu ra.
- **Mục tiêu / nguồn:** 4; Ví dụ 08.7.

#### `5-04` Dừng sớm, chính quy hóa tường minh và chính quy hóa ngầm — định nghĩa (Định nghĩa 08.9) · 2,5 phút
- **Mặt trang:**
  - **Định nghĩa 08.9.** Dừng sớm (early stopping): $T$ nhỏ hơn số bước đưa $\operatorname{opt}_s$ về gần $0$;
  - chọn trước khi chạy hoặc bằng mẫu xác thực độc lập.
  - Chính quy hóa tường minh (explicit regularization): số hạng phạt, như $\tfrac\lambda2\lVert w\rVert^2$.
  - Chính quy hóa ngầm (implicit regularization): huấn luyện tự chọn nghiệm, không qua số hạng phạt.
  - Hai hệ số ổn định $\frac{2G^2}m\sum_t\eta_t$, $\frac{2G^2}{\lambda m}$: ngân sách thay $1/\lambda$.
- **Ghi chú diễn giả:** Mẫu xác thực phải độc lập với tập huấn luyện $s$; đầu ra là điểm lặp tại bước dừng. Chính quy hóa ngầm xảy ra khi nhiều điểm của $W$ có rủi ro thực nghiệm nhỏ như nhau, và khởi tạo, độ dài bước, số bước, cách rút chỉ số quyết định điểm được trả về. Ví dụ về chính quy hóa ngầm: với hàm lỗi bình phương, hạ gradient khởi tạo tại $0$ với độ dài bước hằng $0<\eta<2/\lambda_{\max}(\Phi^\top\Phi)$ hội tụ tới nghiệm nội suy chuẩn nhỏ nhất khi nghiệm nội suy tồn tại; $\Phi$ là ma trận đặc trưng (Phụ lục D của Bài 07). Trong thí nghiệm mở đầu, hàm lỗi logistic trên tập kiểm tra nhỏ nhất ở $5$ vòng ($0{,}589$; ở $10$ vòng là $0{,}603$), còn lỗi phân lớp gần như không đổi từ $5$ đến $100$ vòng ($0{,}309$; $0{,}301$; $0{,}312$), nên số bước tốt nhất phụ thuộc vào hàm lỗi dùng để chọn. Nguồn: ghi chú Bài 08, §8, Định nghĩa 08.9 và hai đoạn sau.
- **Lý do / nối:** khái niệm của §8 sau ví dụ chọn số bước; liên hệ với Bài 06 → bài tập.
- **Mục tiêu / nguồn:** 4, 5; Định nghĩa 08.9.

#### `5-05` Bài tập: số bước tốt nhất với độ dài bước cố định — bài tập (Bài tập 08.8(b)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 08.8.** $B(T)$ là vế phải của Hệ quả 08.8(a); phần (a) cho $T^*=\frac{R\sqrt{m/2}}{\eta G}$, $B(T^*)=RG\sqrt{\frac2m}+\frac{\eta G^2}2-\frac{\eta G^2}m$.
  - (b) Thiết lập của Ví dụ 08.7 ($m=10^4$, $R=5$, $G=1$, $\beta=\tfrac14$): tính $T^*$ và $B(T^*)$ cho $\eta=0{,}1$ và $\eta=0{,}02$.
  - Khi $\eta\to0$, $B(T^*)$ tiến về đâu? So với Hệ quả 08.8(b).
  - **Lời giải:** $\eta\le8$; $\eta=0{,}1$: $T^*\approx3535{,}5$, $B(T^*)\le0{,}1208$; $\eta=0{,}02$: $T^*\approx17\,677{,}7$, $B(T^*)\le0{,}0808$.
  - $\eta\to0$: $T^*\to\infty$, $B(T^*)\to RG\sqrt{2/m}\le0{,}0708$, giới hạn của Hệ quả 08.8(b); vẫn lớn hơn $0{,}0500$ của một vòng.
- **Ghi chú diễn giả** (~140 âm tiết): Gợi ý của tệp bài tập: $B$ có dạng $a/T+bT+c$ với $a=R^2/(2\eta)$, $b=\eta G^2/m$; giá trị nhỏ nhất của $a/T+bT$ là $2\sqrt{ab}$ tại $T=\sqrt{a/b}$. Hai số dùng chung: $RG\sqrt{2/m}\approx0{,}070711$ và $R\sqrt{m/2}/G\approx353{,}55$. Với $\eta=0{,}1$: $0{,}070711+0{,}05-0{,}00001$; với $\eta=0{,}02$: $0{,}070711+0{,}01-0{,}000002$. Độ dài bước nhỏ cần nhiều bước hơn và cho cận nhỏ hơn, nhưng cận không xuống dưới $0{,}0708$. Phần (c) của bài hỏi $T^*$ có làm lỗi kiểm tra nhỏ nhất không: thí nghiệm mở đầu dùng $W=\mathbb R^p$ và $w_{T+1}$, nên Hệ quả 08.8 không áp dụng; $T^*$ làm nhỏ nhất một tổng hai cận trên, và số bước hợp lệ được chọn trước khi chạy hoặc bằng mẫu xác thực độc lập. Nguồn: tệp bài tập, Bài tập 08.8, gợi ý và lời giải.
- **Lý do / nối:** bài tập của cụm đánh đổi, từ `exercises.md` → tiêu đề mạch 6.
- **Mục tiêu / nguồn:** 4; Bài tập 08.8(b).

### Mạch 6. Khi bỏ tính lồi hoặc tính trơn (8 trang, 21 phút)

#### `6-00` 6. Khi bỏ tính lồi hoặc tính trơn — tiêu đề mạch, điểm vào mạch 6 · 0,5 phút
- **Mặt trang:** "6."; h2 "Khi bỏ tính lồi hoặc tính trơn"; `p.strand-lead` (bảng mạch, 24 âm tiết); `p.strand-keys`: "hệ số giãn · hàm lỗi cosin · điểm dừng xấp xỉ · mạng ReLU".
- **Ghi chú diễn giả:** Các ví dụ lần lượt bỏ tính lồi, điều kiện độ dài bước và tính trơn, và giữ các giả thiết còn lại; ví dụ cuối xét mạng ReLU, nơi tính lồi, tính trơn và (G) đều không thỏa. Mỗi lần, câu hỏi là bước nào của chứng minh Mệnh đề 08.5 hoặc Định lý 08.6 không còn đúng. Không có tính lồi, SGD vẫn có một bảo đảm tối ưu, nhưng cho một đại lượng yếu hơn sai số tối ưu thực nghiệm. Nguồn: ghi chú Bài 08, §9, đoạn mở.
- **Lý do / nối:** mạch 5 → phản ví dụ đầu tiên.
- **Mục tiêu / nguồn:** 5; §9.

#### `6-01` Ví dụ: bỏ tính lồi với hàm lỗi cosin — ví dụ, phản ví dụ bỏ giả thiết (Ví dụ 08.8), hình F4 · 3 phút
- **Mặt trang:**
  - **Ví dụ 08.8.** $\ell(w,z)=1+\cos(w-z)\in[0,2]$, $W=\mathbb R$; $m=100$, mọi $z_j=0$, $z'=0{,}01$; $\eta=0{,}1$, $w_1=w'_1=0$.
  - Chỉ $i_1=i$; $G=1$, $1$-trơn, không lồi gần $w=z$; lần chạy trên $s$ đứng yên ở $w=0$, cực đại của $L_s$.
  - Bước khác biệt: $\Delta_2\approx0{,}0010\le2G\eta=0{,}2$; bước chung: $w'_{t+1}=w'_t+0{,}1\sin w'_t$, nhân khoảng $1{,}1$.
  - {{hình F4 `ham-loi-cosin.svg`, figcaption: "Ví dụ 08.8: $\Delta_t$ theo $t=2,\ldots,101$, trục dọc thang lôgarit; đường ngang $0{,}2$ là cận của Mệnh đề 08.5(a) với một bước khác biệt, đường chấm là $\pi$."}}
  - $\Delta_{58}\approx0{,}207>0{,}2$; $w'_t\to-\pi$, cực tiểu của $L_s$, nên $\Delta_t\to\pi$.
  - **Diễn giải:** tại $z=0$, hàm lỗi của hai đầu ra là $2$ và gần $0$; Bổ đề 08.4 là bước hỏng.
- **Ghi chú diễn giả:** Đạo hàm theo $w$ là $-\sin(w-z)$, trị tuyệt đối không quá $1$, nên (G) đúng với $G=1$; đạo hàm bậc hai $-\cos(w-z)\in[-1,1]$, nên hàm lỗi $1$-trơn, và âm gần $w=z$, nên không lồi. Dãy chỉ số có $i_1=i$ và $i_t\ne i$ với mọi $t\ge2$, nên quỹ đạo tất định và chỉ có một bước khác biệt. Điểm $w=0$ là một điểm dừng của $L_s$ với $L_s(0)=2$. Tính trực tiếp, $\Delta_3/\Delta_2\approx1{,}1000$; bảng của ghi chú: $\Delta_{21}\approx0{,}0061$, $\Delta_{41}\approx0{,}0411$, $\Delta_{61}\approx0{,}2753$, $\Delta_{81}\approx1{,}529$, $\Delta_{101}\approx2{,}879$. Nếu phần (a) của Mệnh đề 08.5 đúng ở đây, nó cho $\Delta_t\le0{,}2$ với mọi $t$. Hai lần chạy hội tụ tới hai điểm khác nhau, $0$ và $-\pi$; hiệu hàm lỗi gần $2$, bằng độ rộng của miền giá trị. Nguồn: ghi chú Bài 08, §9, Ví dụ 08.8.
- **Lý do / nối:** trọng tâm trực quan 3 (cái giá khi không lồi); phản ví dụ trước phát biểu → mệnh đề.
- **Mục tiêu / nguồn:** 5; Ví dụ 08.8.

#### `6-02` Bất đẳng thức truy hồi khi bỏ tính lồi — trực quan, kết quả (Mệnh đề 08.10) · 3 phút
- **Mặt trang:**
  - **Trực quan.** Không có tính lồi, mỗi bước chung có thể nhân khoảng cách với $1+\beta\eta_t$.
  - **Mệnh đề 08.10.** **Giả thiết:** như Mệnh đề 08.5, nhưng (S′) thay (S), và $\eta_t>0$ bất kì, tất định.
  - **Bảo đảm:** (a) $\operatorname{proj}_W\circ\Gamma_{\eta,z}$ có hệ số giãn $1+\beta\eta$; (b) mọi $\xi$, $t$: $\Delta_{t+1}\le(1+\beta\eta_t)\Delta_t+2G\eta_t\mathbb 1[i_t=i]$;
  - (c) kì vọng theo $\xi$:
  - $$\mathbb E\Delta_{T+1}\le\frac{2G}m\sum_{t=1}^T\eta_t\prod_{k=t+1}^T(1+\beta\eta_k)\le\frac{2G}m\sum_{t=1}^T\eta_t\,e^{\beta\sum_{k=t+1}^T\eta_k}.$$
  - Bước hằng: vế phải thứ nhất bằng $\frac{2G}{m\beta}\big((1+\beta\eta)^T-1\big)$.
- **Ghi chú diễn giả:** Sau $T$ bước chung, khoảng cách có thể nhân tới $\prod_t(1+\beta\eta_t)$. So với Mệnh đề 08.5, hệ số của $\Delta_t$ là $1+\beta\eta_t$ thay cho $1$, và điều kiện độ dài bước không cần nữa. Hằng số $1+\beta\eta$ ở (a) không giảm được, kể cả khi (G) đúng: với hàm lỗi cosin, $\beta=1$, đạo hàm của ánh xạ bước $w\mapsto w+\eta\sin(w-z)$ là $1+\eta\cos(w-z)$, bằng $1+\eta$ tại $w=z$. Thừa số tích tăng theo hàm mũ khi độ dài bước hằng, tức theo hàm mũ của ngân sách độ dài bước. Nguồn: ghi chú Bài 08, §9, Mệnh đề 08.10 và đoạn sau.
- **Lý do / nối:** trực quan và phát biểu chung trang → ý tưởng chứng minh và con số.
- **Mục tiêu / nguồn:** 5; Mệnh đề 08.10.

#### `6-03` Ý tưởng chứng minh: bất đẳng thức truy hồi khi bỏ tính lồi — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  1. ((S′)) Tam giác: $\lVert\Gamma(u)-\Gamma(v)\rVert\le\lVert u-v\rVert+\eta\beta\lVert u-v\rVert$; phép chiếu giữ hệ số: (a).
  2. Bước chung dùng (a) thay Bổ đề 08.4; bước khác biệt như Mệnh đề 08.5, không dùng tính lồi: (b).
  3. ((I)) Lấy kì vọng, khai triển từ $\Delta_1=0$; $1+x\le e^x$: (c).
  - $\beta=1$, $\eta=0{,}1$, $T=m=100$: $(1{,}1)^{100}\approx1{,}378\cdot10^4$, vế phải $\approx275{,}6$, hàm lỗi cosin trong $[0,2]$.
  - $\eta_t=c/t$: $\prod_{k=t+1}^T(1+\beta c/k)\le(T/t)^{\beta c}$, tăng theo đa thức của $T$.
  - Nhận xét 08.11 (đọc thêm): thêm (T3) và $\eta_t\le c/t$; với $\beta=10$, $c=1$, $m=10^4$, $T=10^6$: $\le33{,}37>1$.
- **Ghi chú diễn giả** (~200 âm tiết): Bất đẳng thức then chốt là hệ số giãn $1+\beta\eta$ ở bước 1, chỉ dùng tính trơn. Ở bước 2, chứng minh bước khác biệt của Mệnh đề 08.5 không dùng tính lồi, nên vẫn cho $\Delta_{t+1}\le\Delta_t+2G\eta_t$. Ở bước 3, $\mathbb E\Delta_{t+1}\le(1+\beta\eta_t)\mathbb E\Delta_t+2G\eta_t/m$; với bước hằng, tổng hình học cho $\big((1+\beta\eta)^T-1\big)/\beta$. Nhân với $G=1$, cận cho hiệu hàm lỗi tại một quan sát kiểm tra cũng khoảng $275{,}6$. Với $\eta_t=c/t$, thừa số tích không quá $e^{\beta c\sum_{k>t}1/k}\le(T/t)^{\beta c}$; vì vậy cận cho hàm lỗi không lồi của Hardt, Recht và Singer (2016, Định lý 3.12) dùng $\eta_t\le c/t$. Nhận xét 08.11 ở mức đọc thêm: với (T3), (S′), hàm lỗi $G$-Lipschitz trên $\mathbb R^p$, $\eta_t$ không tăng, $\eta_t\le c/t$ và SGD không chiếu, hệ số ổn định không quá $T^{\beta c/(\beta c+1)}(2cG^2)^{1/(\beta c+1)}\frac{1+1/(\beta c)}{m-1}$; con số $33{,}37$ với $G=1$ không cho thông tin với hàm lỗi trong $[0,1]$. Nguồn: ghi chú Bài 08, Phụ lục D; đoạn sau Mệnh đề 08.10; Nhận xét 08.11.
- **Lý do / nối:** trang ý tưởng chứng minh riêng, cùng con số cho cái giá → bảo đảm tối ưu không lồi.
- **Mục tiêu / nguồn:** 5; Phụ lục D, Nhận xét 08.11.

#### `6-04` Điểm dừng xấp xỉ của SGD trên hàm mục tiêu trơn — kết quả đọc thêm (Mệnh đề 08.12) · 2,5 phút
- **Mặt trang:**
  - **Nhắc lại:** lịch sử $\mathcal F_{t-1}$ và kì vọng có điều kiện theo lịch sử (Bài 05).
  - **Mệnh đề 08.12.** **Giả thiết:** $F$ $\beta$-trơn, không cần lồi, $F_*=\inf F>-\infty$; $\mathbb E[g_t\mid\mathcal F_{t-1}]=\nabla F(w_t)$, $\mathbb E[\lVert g_t-\nabla F(w_t)\rVert^2\mid\mathcal F_{t-1}]\le\sigma^2$;
  - $w_{t+1}=w_t-\eta g_t$, $0<\eta\le1/\beta$, $w_1$ tất định; $\mathbb E\lvert F(w_t)\rvert<\infty$. **Bảo đảm:** theo kì vọng,
  - $$\frac1T\sum_{t=1}^T\mathbb E\lVert\nabla F(w_t)\rVert^2\le\frac{2(F(w_1)-F_*)}{\eta T}+\beta\eta\sigma^2.$$
  - Tính dừng (stationarity); hồi quy logistic, $\eta=0{,}05$, $T=10^4$: vế phải $\le0{,}0153$.
  - Ví dụ 08.8: $w=0$ là điểm dừng (stationary point), $L_s(0)=2$ lớn nhất; gradient nhỏ không kéo theo $L_s$ nhỏ.
- **Ghi chú diễn giả:** Kết quả ở mức đọc thêm; chứng minh ở Phụ lục E: cận trên bậc hai tại hai điểm lặp liên tiếp, kì vọng có điều kiện theo lịch sử dùng tính không chệch và cận phương sai, điều kiện $\eta\le1/\beta$ cho hệ số $-\tfrac\eta2$, rồi tính chất tháp và tổng triệt tiêu. Vế trái bằng $\mathbb E\lVert\nabla F(w_\tau)\rVert^2$ với $\tau$ rút đều trên $\{1,\ldots,T\}$; $w_\tau$ là một điểm dừng xấp xỉ (approximate stationary point). Với hồi quy logistic, $F=L_s$, $W=\mathbb R^p$, $w_1=0$: $\beta=\tfrac14$, $F(0)-F_*\le\ln2$, $\sigma^2\le G^2=1$, và vế phải là $\tfrac{2\ln2}{500}+0{,}0125$. Cận chặn trung bình của bình phương chuẩn gradient, không chặn $F(w_{T+1})-F_*$. Nguồn: ghi chú Bài 08, §9, Mệnh đề 08.12 và đoạn sau; Phụ lục E.
- **Lý do / nối:** bảo đảm còn lại khi không lồi, đặt trước hai ví dụ cuối như ghi chú; Bài 10 dùng lại kết quả này → trở lại hàm lỗi lồi.
- **Mục tiêu / nguồn:** 5; Mệnh đề 08.12.

#### `6-05` Ví dụ: độ dài bước vượt $2/\beta$ — ví dụ, phản ví dụ bỏ giả thiết (Ví dụ 08.9) · 2,5 phút
- **Mặt trang:**
  - **Ví dụ 08.9.** Huber ($\beta=G=1$, lồi), $s=(0,0,0,\tfrac1{100})$, $s^{(4)}=(0,0,0,-\tfrac1{100})$, $w_1=w'_1=0$; $i_1=4$, rồi $i_t=1$.
  - Chỉ bỏ điều kiện $\eta\le2/\beta$; quỹ đạo tất định.
  - $\eta=1$: $\Delta_2=0{,}02$; bước chung $w\mapsto0$, nên $\Delta_t=0$ từ $t=3$.
  - $\eta=2$: $\Delta_2=0{,}04$; bước chung $w\mapsto-w$, nên $\Delta_t=0{,}04$.
  - $\eta=3$: bước chung $w\mapsto-2w$ khi $\lvert w\rvert\le1$: $\Delta_2,\ldots,\Delta_8=0{,}06;\ 0{,}12;\ 0{,}24;\ 0{,}48;\ 0{,}96;\ 1{,}92;\ 3{,}84$.
  - **Diễn giải:** với $\eta=3$, bước chung nhân khoảng cách với $\lvert1-\eta\beta\rvert=2$, đúng hệ số giãn của Ví dụ 08.3.
- **Ghi chú diễn giả:** Mọi giả thiết khác của Mệnh đề 08.5 vẫn đúng. Bước khác biệt cho $w_2=\pm0{,}01\eta$, vì $w_1-z=\mp0{,}01$ nằm trong vùng bậc hai. Bước chung với $z=0$ trên $[-1,1]$ là $w\mapsto(1-\eta)w$. Với $\eta=2=2/\beta$, $w_t$ đổi dấu ($\pm\tfrac1{50}$) và khoảng cách giữ nguyên: đây là biên của điều kiện. Sau $\Delta_8$, $\lvert w_t\rvert>1$ và điểm lặp ra khỏi vùng bậc hai của hàm lỗi. Nguồn: ghi chú Bài 08, §9, Ví dụ 08.9.
- **Lý do / nối:** bỏ giả thiết thứ hai (độ dài bước), với hàm lồi → bỏ tính trơn.
- **Mục tiêu / nguồn:** 2, 5; Ví dụ 08.9.

#### `6-06` Ví dụ: hàm lỗi không trơn và mạng ReLU — ví dụ, phản ví dụ bỏ giả thiết (Ví dụ 08.10) · 3,5 phút
- **Mặt trang:**
  - **Ví dụ 08.10.** Một bước chung, $\eta=\tfrac12$: $\lvert w\rvert$ đưa khoảng cách $0{,}02\to0{,}98$; bản lề ($x=\tilde y=1$): $0{,}02\to0{,}48$.
  - Mạng ReLU, mọi trọng số huấn luyện, hàm lỗi logistic theo $\theta$:
  - không trơn tại tiền kích hoạt (pre-activation) bằng $0$; không lồi (Bài tập 07.5(c));
  - không có $G$ đều: gradient theo $\Theta_1$ tỉ lệ với $\Theta_2$.
  - **Kết luận:** Định lý 08.6 không áp dụng nguyên văn; áp dụng khi lớp ẩn cố định.
- **Ghi chú diễn giả:** Với $\ell(w,z)=\lvert w-z\rvert$ (lồi, $1$-Lipschitz, không khả vi tại $w=z$), $z=0$ và hai điểm $\pm0{,}01$, đạo hàm là $\pm1$, nên $0{,}01\mapsto-0{,}49$ và $-0{,}01\mapsto0{,}49$; mỗi bước chung có thể tăng khoảng cách gần $2G\eta$, và Mệnh đề 08.5 không còn thừa số $1/m$. Với hàm lỗi bản lề, $0{,}99\mapsto1{,}49$ và $1{,}01$ giữ nguyên. Mạng là mạng của Định nghĩa 07.1; hàm lỗi không khả vi tại tham số có một tọa độ của $\Theta_1x+b_1$ bằng $0$ và trọng số ra tương ứng khác $0$. Đổi chỗ hai nơ-ron ẩn cho cùng một hàm; Bài tập 07.5(c) cho hàm mục tiêu bình phương bằng $0$ tại hai tham số và $\tfrac{27}{16}$ tại trung điểm. Với lớp ẩn cố định như mạng của Ví dụ 07.3, hàm lỗi logistic lồi và trơn theo trọng số lớp ra, với $G=\sup_x\lVert\chi(x)\rVert$ và $\beta=G^2/4$. Mạng ReLU huấn luyện mọi lớp nơ-ron cũng không thỏa giả thiết của Mệnh đề 08.10 hay Nhận xét 08.11, vì hàm lỗi không trơn. Nguồn: ghi chú Bài 08, §9, Ví dụ 08.10 và đoạn sau.
- **Lý do / nối:** trọng tâm trực quan 5 (giả thiết nào hỏng khi chuyển sang học sâu) → bài tập.
- **Mục tiêu / nguồn:** 5; Ví dụ 08.10.

#### `6-07` Bài tập: khoảng cách tăng theo hàm mũ với hàm lỗi cosin — bài tập (Bài tập 08.3(d)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Bài tập 08.3(d).** Ví dụ 08.8: $w_t=0$ với mọi $t$, nên $\Delta_t=\lvert w'_t\rvert$, và $\Delta_2=0{,}1\sin0{,}01$. Chứng minh: nếu $\Delta_t\le\tfrac12$ thì
  - $$1+0{,}1\cos\tfrac12\le\frac{\Delta_{t+1}}{\Delta_t}\le1{,}1.$$
  - Suy ra chỉ số $t$ đầu tiên có $\Delta_t>\tfrac12$ nằm trong một khoảng, và tính khoảng đó.
  - **Lời giải:** $\varphi(w)=w+0{,}1\sin w$, $\varphi(0)=0$; định lý giá trị trung bình: $\Delta_{t+1}=\varphi'(\zeta)\Delta_t$, $\varphi'=1+0{,}1\cos\zeta\le1{,}1$, và $\ge1{,}08776$ khi $\lvert\zeta\rvert\le\tfrac12$.
  - $\ln(0{,}5/\Delta_2)\approx6{,}2146$: $\tau-2>65{,}2$, nên $\tau\ge68$; $1{,}08776^{74}\Delta_2\approx0{,}505>\tfrac12$, nên $\tau\le76$.
  - Tính bằng máy: $\tau=68$.
- **Ghi chú diễn giả** (~150 âm tiết): Gợi ý của tệp bài tập: ánh xạ bước ở các bước chung là $\varphi(w)=w+0{,}1\sin w$; với $w\in[-\tfrac12,0)$, $\varphi(w)=\varphi'(\zeta)w$ với $\zeta\in(w,0)$. Mọi $w'_t$ với $t\ge2$ nằm trong $(-\pi,0)$, vì $\varphi$ tăng, $\varphi(-\pi)=-\pi$ và $\varphi(w)<w$ trên $(-\pi,0)$; do đó $\Delta_t=-w'_t$. Kí hiệu $\tau$ là chỉ số đầu tiên có $\Delta_\tau>\tfrac12$. Cận trên $1{,}1$ đúng ở mọi bước, nên $\Delta_t\le1{,}1^{t-2}\Delta_2$; cận dưới chỉ đúng khi $\Delta_t\le\tfrac12$, và nếu $\Delta_t\le\tfrac12$ đến $t=76$ thì $\Delta_{76}>\tfrac12$, mâu thuẫn. Mệnh đề 08.10(a) cho hệ số giãn trên $1{,}1$; trên quỹ đạo này, khoảng cách tăng ít nhất theo cơ số $1{,}0878$ mỗi bước, nên tốc độ hàm mũ của mệnh đề xảy ra thật. Giá trị $\Delta_{58}\approx0{,}207$ của Ví dụ 08.8 nhỏ hơn $\tfrac12$, phù hợp với $\tau=68$. Nguồn: tệp bài tập, Bài tập 08.3(d), gợi ý và lời giải.
- **Lý do / nối:** bài tập của cụm không lồi, từ `exercises.md` → tiêu đề mạch 7.
- **Mục tiêu / nguồn:** 5; Bài tập 08.3(d).

### Mạch 7. Tổng kết (8 trang, 12 phút)

#### `7-00` 7. Tổng kết — tiêu đề mạch, điểm vào mạch 7 · 0,5 phút
- **Mặt trang:** "7."; h2 "Tổng kết"; `p.strand-lead` (bảng mạch, 24 âm tiết); không có dòng từ khóa.
- **Ghi chú diễn giả:** Bài có một bổ đề về bước gradient không giãn, một bất đẳng thức truy hồi cho hai lần chạy ghép cặp, một định lý ổn định cho điểm lặp cuối, một hệ quả cho điểm lặp trung bình, một cận ghép với sai số tối ưu và một bất đẳng thức truy hồi khi bỏ tính lồi. Bảng tổng kết gom các giả thiết không được bỏ; sau đó là câu trả lời cho vấn đề trung tâm, một bài tập kiểm giả thiết cho mạng ReLU, câu hỏi tự kiểm tra và bài tập về nhà. Nguồn: ghi chú Bài 08, §10–§13.
- **Lý do / nối:** mạch 6 → bảng tổng kết.
- **Mục tiêu / nguồn:** tất cả; §10–§13.

#### `7-01`, `7-02` Bảng tổng kết — tổng kết · 2 phút
- **Mặt trang (bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh`, trần 80):**
  | Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh |
  |---|---|---|
  | Bổ đề 08.4, tất định: $\operatorname{proj}_W\circ\Gamma$ không giãn | $f$ lồi, $\beta$-trơn trên $\mathbb R^p$; $\eta\le2/\beta$; $W$ đóng, lồi | tính đồng bức |
  | Mệnh đề 08.5, kì vọng theo $\xi$: $\mathbb E\Delta_{T+1}\le\frac{2G}m\sum_t\eta_t$ | (S), (G), $\eta_t\le2/\beta$, (I); ghép cặp | hai loại bước, tổng triệt tiêu |
  | Định lý 08.6, kì vọng theo $(S,\xi)$: $\lvert\mathbb E[L_D-L_S](w_{T+1})\rvert\le\frac{2G^2}m\sum_t\eta_t$ | như trên; (T1), (T2); $W$ lồi | (L); Định lý 06.10 |
  | Hệ quả 08.7: $\epsilon_{\mathrm{stab}}=G^2\eta(T-1)/m$ cho $\bar w_T$, bước hằng | như Định lý 08.6 | trung bình các $\Delta_t$ |
  | Hệ quả 08.8, kì vọng theo $(S,\xi)$: $\mathbb EL_D(\bar w_T)-\inf_WL_D\le\frac{R^2}{2\eta T}+\frac{\eta G^2}2+\frac{\eta G^2(T-1)}m$ | như trên; (R); $\eta$ hằng; đầu ra $\bar w_T$ | Mệnh đề 06.5(b); Định lý 05.14 |
  | Mệnh đề 08.10, kì vọng theo $\xi$: $\mathbb E\Delta_{T+1}\le\frac{2G}m\sum_t\eta_t\prod_{k>t}(1+\beta\eta_k)$ | (S′), (G), (I); ghép cặp | hệ số giãn $1+\beta\eta$ |
- **Ghi chú diễn giả:** Mỗi giả thiết có một phản ví dụ hoặc một bước hỏng trong bài: bỏ tính lồi, hàm lỗi cosin đưa khoảng cách từ $0{,}0010$ tới $\pi$ sau một bước khác biệt; bỏ $\eta\le2/\beta$, bước chung nhân khoảng cách với $2$ khi $\eta=3$; bỏ tính trơn, giá trị tuyệt đối và hàm lỗi bản lề tăng khoảng cách ở bước chung; bỏ (G), hàm lỗi bình phương trên $\mathbb R$ và mạng ReLU không có cận gradient đều; ghép cận của điểm lặp cuối với Định lý 05.14 là sai. Mệnh đề 08.12 và Nhận xét 08.11 ở mức đọc thêm. Với hàm lỗi lồi, mọi cận không phụ thuộc $p$; các kết quả của bài không có cận với xác suất cao. Nguồn: ghi chú Bài 08, §5–§10.
- **Lý do / nối:** một hàng cho mỗi kết quả chính, giữ loại bảo đảm và giả thiết đầy đủ khi đặt cạnh nhau → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §5–§9.

#### `7-03` Vấn đề trung tâm — tổng kết · 2,5 phút
- **Mặt trang:**
  - (T1), (T2), (S), (G), $\eta_t\le2/\beta$: khoảng cách tổng quát hóa kì vọng ($w_{T+1}$) $\le\frac{2G^2}m\sum_t\eta_t$.
  - Thêm cận tối ưu: nhiều vòng không cho cận nhỏ hơn một vòng ($0{,}0708$ so với $0{,}0500$).
  - Không lồi: cận tăng theo hàm mũ; mạng ReLU (mọi lớp huấn luyện) không thỏa (S), (G).
  - Mạng sâu: "huấn luyện nhanh hơn thì tổng quát hóa tốt hơn" là phỏng đoán (conjecture).
- **Ghi chú diễn giả:** Trả lời cho câu hỏi "thuật toán huấn luyện ảnh hưởng tới khoảng cách tổng quát hóa như thế nào": với hàm lỗi lồi, trơn, có gradient bị chặn, qua tổng các độ dài bước chia cho cỡ mẫu, không qua số tham số. Cận không phụ thuộc $p$; trong thí nghiệm mở đầu, cận là $t/200$ còn khoảng cách đo được tăng từ $0{,}045$ lên $0{,}919$. Các khẳng định thuộc ba mức: chứng minh được (Định lý 08.6, Hệ quả 08.7, 08.8); lý thuyết không lồi bổ sung (Mệnh đề 08.10, Nhận xét 08.11, Mệnh đề 08.12); phỏng đoán thực nghiệm, gồm cả chính quy hóa ngầm trong mạng sâu. So với Hệ quả 07.16 (xác suất ít nhất $1-\delta$, mọi hàm của một lớp chọn trước, không cần tính lồi), Định lý 08.6 đúng theo kì vọng cho một thuật toán, cần tính lồi và tính trơn, nhưng không cần $W$ bị chặn. Nguồn: ghi chú Bài 08, §10.
- **Lý do / nối:** trả lời vấn đề trung tâm cho cả bài, giữ điều kiện và loại bảo đảm → bài tập tổng hợp.
- **Mục tiêu / nguồn:** tất cả; §10.

#### `7-04` Bài tập: kiểm tra giả thiết cho một thiết lập huấn luyện mạng ReLU — bài tập tổng hợp (Bài tập 08.5(c)), đề · 2 phút
- **Mặt trang:**
  - **Bài tập 08.5.** Mạng ReLU, $J=2$, huấn luyện mọi trọng số, hàm lỗi logistic, $\lVert x\rVert\le1$;
  - $m=5\cdot10^4$ quan sát độc lập cùng phân bố; SGD không chiếu, $\eta=0{,}1$, $T=10^5$.
  - Báo cáo: "Theo Định lý 08.6 với $G=1$, khoảng cách tổng quát hóa kì vọng không quá $2\cdot1^2\cdot0{,}1\cdot10^5/(5\cdot10^4)=0{,}4$."
  - (c) Lập bảng các giả thiết của định lý: thỏa, không thỏa, hay không xác định; $0{,}4$ có căn cứ không?
- **Ghi chú diễn giả:** Bài ghép phát biểu đầy đủ của Định lý 08.6 với ba phản ví dụ của Ví dụ 08.10: hàm lỗi không trơn, không lồi và không có cận gradient đều. Mạng là mạng của Định nghĩa 07.1 với $N$ nơ-ron ẩn; mẫu gồm $m=5\cdot10^4$ quan sát. Hai phần đầu của bài cho hai sự kiện dùng ở (c). Phần (a) xét trường hợp nhỏ nhất $p=1$, $N=1$, $x=1$, $\tilde y=1$, trọng số ra bằng $1$, chỉ trọng số ẩn $\theta$ được huấn luyện: hai đạo hàm một phía khác nhau nên hàm không khả vi tại $0$, và đạo hàm phải nhỏ hơn đạo hàm trái nên hàm không lồi. Phần (b): với $\theta_1=1/\theta_2$, $\lvert\partial\ell/\partial\theta_1\rvert=\theta_2/(1+e)$, vượt mọi $G$ khi $\theta_2$ lớn. Hai sự kiện này là Bước 3 của Ví dụ 08.10 trên trường hợp nhỏ nhất. Nguồn: tệp bài tập, Bài tập 08.5 và gợi ý.
- **Lý do / nối:** bài tập tổng hợp từ `exercises.md`; đề trên một trang vì câu chữ dài; phần (d)(i) ở trang sau → lời giải.
- **Mục tiêu / nguồn:** 5; Bài tập 08.5.

#### `7-05`, `7-06` Lời giải: kiểm tra giả thiết cho một thiết lập huấn luyện mạng ReLU — bài tập tổng hợp (Bài tập 08.5(c), (d)(i)), lời giải · 2 phút
- **Mặt trang:**
  - **Lời giải:** (c)
  - Bảng: Giả thiết | Kết luận; (T1) | thỏa; (T2) | thỏa; $W$ lồi | thỏa ($W$ là toàn bộ không gian tham số); (S): lồi | không thỏa; (S): trơn | không thỏa; (G) | không thỏa; $\eta_t\le2/\beta$ | không xác định.
  - Ba giả thiết tối ưu không thỏa (Ví dụ 08.10), nên $0{,}4$ không có căn cứ.
  - (d)(i) Cố định lớp ẩn, chỉ huấn luyện lớp ra (Ví dụ 07.3): cận ổn định và cái giá?
  - (S), $\beta=G^2/4$; (G), $G=\sup_x\lVert\chi(x)\rVert$: cận $\frac{2G^2\cdot0{,}1\cdot10^5}{5\cdot10^4}=0{,}4G^2$ khi $0{,}1\le8/G^2$; $G=1{,}5$ cho $0{,}9$.
  - Cái giá: lớp ẩn không học; mô hình tuyến tính trên đặc trưng cố định.
- **Ghi chú diễn giả:** Định lý 08.6, Mệnh đề 08.10 và Nhận xét 08.11 đều không áp dụng cho thiết lập của báo cáo. Phần (d)(i) của tệp bài tập: "Nêu hai cách sửa thiết lập để có một cận ổn định, và cái giá của mỗi cách: (i) cố định lớp ẩn trước khi thấy mẫu, chỉ huấn luyện lớp ra như mạng của Ví dụ 07.3"; gợi ý: với lớp ẩn cố định, hàm lỗi là hàm lỗi logistic của một mô hình tuyến tính trên đặc trưng $\chi(x)$. Với (T2): $\ell\ge0$, và tại tham số khởi tạo cố định, $f_\theta$ liên tục nên bị chặn trên quả cầu đơn vị, do đó $L_D$ hữu hạn. Điều kiện độ dài bước không xác định vì không có $\beta$. Cách sửa (ii) của bài (hàm kích hoạt trơn, chiếu lên $W$ lồi, bị chặn) vẫn không có tính lồi; lập luận của Mệnh đề 08.10 cho thừa số $1{,}1^{10^5}>10^{4139}$ với $\beta_W=1$, nên cận không cho thông tin. Nguồn: tệp bài tập, lời giải Bài tập 08.5.
- **Lý do / nối:** lời giải trên mặt trang, bảng giả thiết → tự kiểm tra.
- **Mục tiêu / nguồn:** 5; Bài tập 08.5.

#### `7-07` Câu hỏi tự kiểm tra — tổng kết · 2 phút
- **Mặt trang:**
  - 1. Vì sao hai lần chạy cần dùng chung dãy chỉ số?
  - 2. Bước nào của chứng minh Định lý 08.6 dùng tính lồi của hàm lỗi?
  - 3. Hồi quy logistic, $\lVert x\rVert\le1$, $W=\mathbb R^p$, $m=5000$, $T=20\,000$: cận của Định lý 08.6 với $\eta_t=0{,}1$ và với $\eta_t=0{,}1/\sqrt t$?
  - 4. Cận ở câu 3 có chặn hiệu lỗi phân lớp giữa tập kiểm tra và tập huấn luyện không?
- **Ghi chú diễn giả** (câu trả lời dự kiến, chỉ dùng ghi chú): (1) Ghép cặp giữ phân bố của từng lần chạy và đặt hai lần chạy trên cùng không gian, nên hiệu hai kì vọng không quá kì vọng của trị tuyệt đối; với hai dãy độc lập, khoảng cách gồm cả phần do tính ngẫu nhiên của thuật toán ($\tfrac38$ so với $\tfrac14$ trong ví dụ một bước). (2) Chỉ Bổ đề 08.4(a), ở các bước chung của Mệnh đề 08.5. (3) $G=1$, $\beta=\tfrac14$; ngân sách $2000$ cho $2\cdot2000/5000=0{,}8$; với $\sum_tt^{-1/2}\le2\sqrt T-1$, ngân sách không quá $28{,}19$ và cận không quá $0{,}0113$. (4) Không: định lý chặn khoảng cách tổng quát hóa kì vọng của hàm lỗi logistic, theo kì vọng theo $(S,\xi)$; hàm lỗi 0–1 không Lipschitz theo $w$, và không có cận với xác suất cao. Nguồn: ghi chú Bài 08, §4, §7, §12 và lời giải.
- **Lý do / nối:** bốn câu ngắn trả lời được chỉ bằng ghi chú; câu 3, 4 là câu hỏi cuối buổi §12 (a)–(c) → bài tập về nhà.
- **Mục tiêu / nguồn:** 1, 3, 5; §4, §7, §12.

#### `7-08` Bài tập về nhà — tổng kết · 0,5 phút
- **Mặt trang:**
  - Bảng: Mục | Bài tập; 4. Tính ổn định đều của hạ gradient ngẫu nhiên | 08.1, 08.6, 08.7; 5. Đánh đổi giữa tối ưu và ổn định | 08.2, 08.8; 6. Khi bỏ tính lồi hoặc tính trơn | 08.3, 08.4, 08.5.
  - Liên kết "Ghi chú bài giảng · Bài tập" (viewer `&deck=`).
- **Ghi chú diễn giả:** Mỗi bài xếp vào mạch cung cấp kiến thức cuối cùng bài đó cần. Bài tập 08.1 cần hệ số ổn định của điểm lặp cuối (phần (a), (b)); 08.6 đọc số đo của thí nghiệm ghép cặp và phân biệt bằng chứng thí nghiệm với chứng minh; 08.7 cần Hệ quả 08.7. Bài tập 08.2 so cận ổn định với cận tối ưu của ba lịch độ dài bước (step-size schedule); 08.8 cần Hệ quả 08.8 và cách chọn số bước hợp lệ. Bài tập 08.3 cần hàm lỗi cosin và Mệnh đề 08.10; 08.4 cần Mệnh đề 08.12; 08.5 là bài tổng hợp vừa làm. Cả tám bài là bài gốc của học phần; phần thực nghiệm của Bài tập 08.6 là tùy chọn. Nguồn: ghi chú Bài 08, §11; tệp bài tập.
- **Lý do / nối:** giao bài tập theo mạch → tài liệu.
- **Mục tiêu / nguồn:** tất cả; §11.

#### `7-09` Tài liệu tham khảo — tổng kết · 0,5 phút
- **Mặt trang:**
  - Trước buổi học: UML §13.1–13.2, §20.6.
  - Sau buổi học: Hardt, Recht và Singer (2016), §2, §3.1–3.3, Phụ lục A, §1, §5.
  - Shalev-Shwartz và Ben-David (2014). *Understanding Machine Learning: From Theory to Algorithms*. Cambridge University Press.
  - Hardt, Recht và Singer (2016). *Train faster, generalize better: Stability of stochastic gradient descent*. ICML.
  - Bài 09: Học chuỗi và mô hình sinh.
- **Ghi chú diễn giả:** UML §13.1–13.2: chính quy hóa và quy tắc ổn định không quá khớp; §20.6: SGD và lan truyền ngược, một quan sát mới ở mỗi bước. Bài báo: §3.1–3.3 cho hàm trơn và lồi (Định lý 3.8), Phụ lục A cho tính đồng bức. Đọc mở rộng: §3.5 (không lồi, Định lý 3.12), §4 (suy giảm trọng số, cắt gradient, dropout), §6 (thí nghiệm trên mạng sâu, quan sát thực nghiệm), §7 (câu hỏi mở) của bài báo; UML §31.1 (cận PAC-Bayes). Bài 09 hỏi: khi mỗi quan sát là một chuỗi có các phần tử phụ thuộc nhau và hàm lỗi là $-\ln$ độ hợp lý của cả chuỗi, rủi ro kì vọng, rủi ro thực nghiệm và giả thiết độc lập được viết lại thế nào. Nguồn: ghi chú Bài 08, §12 đoạn cuối, §13 và quan hệ với nguồn.
- **Lý do / nối:** trang cuối; dòng chữ Bài 09 (không liên kết cho đến khi deck Bài 09 có tên tệp).
- **Mục tiêu / nguồn:** —; §13.

## 7. Hành trình khái niệm

Thứ tự bước theo quy định: vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh (trang riêng) → kỹ thuật hoặc kiểm tra. Các bước có thể chung trang nhưng không đảo thứ tự trên mặt trang. Theo cổng duyệt Bài 04 (T5), ví dụ đặt trước phát biểu khi số liệu của nó không cần chính kết quả đó; ví dụ của ghi chú dùng kết quả để kiểm tra thì đứng sau, ở cột cuối.

| Kết quả hoặc khái niệm | Vấn đề | Trực quan | Ví dụ | Phát biểu | Ý tưởng chứng minh | Kỹ thuật / kiểm tra | Gộp, `không áp dụng`, lý do |
|---|---|---|---|---|---|---|---|
| Định nghĩa 08.2 (ghép cặp) | 1-02 (Định nghĩa 06.9 so hai kì vọng), 2-00 | 2-05 ("Trực quan.": phân bố từng lần chạy giữ nguyên; Jensen) | 2-05 (một bước: $\tfrac14$ so với $\tfrac38$), 2-06 (Ví dụ 08.2, hình F1) | 2-04 | `không áp dụng` (định nghĩa) | 2-06 (hai loại bước trên một quỹ đạo) | Ví dụ một bước của ghi chú đứng sau định nghĩa như trong ghi chú, vì nó dùng thuật ngữ ghép cặp. |
| Bổ đề 08.4 | 2-06 (dòng "bước chung: khoảng cách không tăng"), 2-07 (dòng đầu: cùng ánh xạ cho hai điểm) | 2-08 ("Trực quan.": hệ số góc $1-\eta f''\in[1-\eta\beta,1]$) | 2-07 (dấu bằng với hàm bậc hai; hàm lõm không đồng bức) | 2-08 | 2-09 | 2-10 (Ví dụ 08.3: ngưỡng chặt, hàm lõm giãn); 2-11 (Bài tập 08.3(a)) | Trực quan và phát biểu chung trang. |
| Mệnh đề 08.5 | 2-10 (dòng cuối: bước khác biệt chưa được chặn) | 3-01 ("Trực quan.": chỉ tăng ở bước khác biệt, trung bình $T/m$ bước) | 2-06 (Ví dụ 08.2: $+1=2G\eta$ ở hai bước khác biệt) | 3-01 | 3-02 | 3-03 (Ví dụ 08.4: $\tfrac14$; $\tfrac{29}{64}$; $0{,}8705$; dãy đạt cận); 3-04 (Bài tập 08.1(c)) | Trực quan và phát biểu chung trang. |
| Định lý 08.6 | 1-06 (câu hỏi mở đầu), 4-00 | 4-01 ("Trực quan.": hai lần chạy gần nhau, theo (L) hàm lỗi gần nhau) | 1-06 (bảng thí nghiệm) | 4-01 | 4-02 | 4-03 (Ví dụ 08.5: $0{,}001$; $t/200$); 4-04 (Ví dụ 08.6, hình F2); 7-05 câu 3–4 | Trực quan và phát biểu chung trang. Câu nối "Mệnh đề 08.5 chặn khoảng cách tham số, Định nghĩa 06.9 cần hiệu hàm lỗi" nằm trong dòng "Trực quan." và ghi chú diễn giả (mục 11, điểm 6). |
| Hệ quả 08.7 | 4-05 (dòng đầu: cận tối ưu dùng $\bar w_T$) | 4-05 ("Trực quan.": điểm lặp đầu còn gần nhau) | 4-06 (chương trình của Ví dụ 06.3, trên mặt trang bài tập) | 4-05 | ghi chú diễn giả 4-05 (lộ trình bốn bước) | 4-06 (Bài tập 08.7(b): $39{,}975$ so với $0{,}4750$; $T\le161$) | Không có trang ý tưởng chứng minh riêng (mục 11, điểm 2). Chương trình của Ví dụ 06.3 (đoạn sau Hệ quả 08.7) đứng trên trang bài tập ngay sau, cùng số liệu. |
| Hệ quả 08.8 | 5-00 (ghi chú diễn giả), 2-03 (câu hỏi thực hành) | 5-01 ("Trực quan.": hai cận ngược chiều theo $T$) | 2-03 (một vòng: $0{,}05$) | 5-01 | 5-02 | 5-03 (Ví dụ 08.7, hình F3); 5-05 (Bài tập 08.8(b)) | Trực quan và phát biểu chung trang; ví dụ của ghi chú cần $\eta^*$, nên đứng sau. |
| Định nghĩa 08.9 | 5-03 (số bước chọn theo một cận) | ghi chú diễn giả 5-04 (ba cách điều khiển đầu ra) | ghi chú diễn giả 5-04 (nghiệm nội suy chuẩn nhỏ nhất; thí nghiệm: $0{,}589$ ở $5$ vòng) | 5-04 | `không áp dụng` (định nghĩa) | 5-04 dòng cuối (hai hệ số ổn định cùng dạng) | Ví dụ ở ghi chú diễn giả vì trang định nghĩa đã ở trần 60. |
| Mệnh đề 08.10 | 6-00, 6-01 (khoảng cách $0{,}0010\to\pi$) | 6-02 ("Trực quan.": nhân $1+\beta\eta_t$ mỗi bước chung) | 6-01 (Ví dụ 08.8, hình F4) | 6-02 | 6-03 | 6-03 ($275{,}6$; $\eta_t=c/t$; Nhận xét 08.11); 6-07 (Bài tập 08.3(d)) | Ví dụ 08.8 đứng trước phát biểu như ghi chú (số liệu không cần mệnh đề). |
| Mệnh đề 08.12 (đọc thêm) | 6-00 (ghi chú diễn giả: bảo đảm yếu hơn khi không lồi) | ghi chú diễn giả 6-04 | 6-01 ($w=0$ là cực đại) | 6-04 | ghi chú diễn giả 6-04 (Phụ lục E) | 6-04 ($0{,}0153$; điểm dừng là cực đại) | Kết quả đọc thêm: một trang, lộ trình ở ghi chú diễn giả (mục 11, điểm 3). |
| Giả thiết khi chuyển sang học sâu | 2-02 (giả thiết (S), (G)), 6-00 | 6-06 (ba giả thiết hỏng) | 6-05 (Ví dụ 08.9), 6-06 (Ví dụ 08.10) | 6-06 dòng "Kết luận:" | `không áp dụng` | 7-03, 7-04 (Bài tập 08.5(c), (d)(i)); 7-02 | — |

Thời lượng theo mạch: 9 + 30 + 13 + 20 + 15 + 21 + 12 = 120 phút; 52 trang.

## 8. Hình vẽ

Mọi hình là SVG trong `2627-1/img/lec-08/`, `role="img"`, có `<title>` và alt cụ thể; màu không là tín hiệu duy nhất (kiểu nét và hình dạng điểm khác nhau cho từng dãy, nhãn trực tiếp cuối đường); chữ trong hình chỉ là nhãn trục, nhãn điểm, số và nhãn ngắn (Unicode), không công thức; công thức và chú thích nằm ở `figcaption` (KaTeX). Chú thích nêu dữ liệu. Mọi số có nhãn trên hình cũng có trong chữ trên cùng trang. Trục chứa hết dữ liệu.

| Mã | Tệp | Trang | Nội dung và dữ liệu | Alt dự kiến |
|---|---|---|---|---|
| F1 | `hai-lan-chay-huber.svg` | 2-06 | Trục ngang $t=1,\ldots,7$ (vạch nguyên); trục dọc $w\in[-1;2]$ (vạch từng $0{,}5$). Dãy $w_t$ (nét liền, chấm tròn đặc): $0;0;\tfrac12;\tfrac34;\tfrac54;\tfrac74;\tfrac54$. Dãy $w'_t$ (nét đứt, ô vuông rỗng): $0;0;-\tfrac12;0;\tfrac12;0;0$. Hai dải nền nhạt có viền chấm giữa $t=2$ và $3$, giữa $t=5$ và $6$, nhãn "bước khác biệt". Mũi tên hai đầu dọc tại $t=3$, $6$, $7$ với nhãn "1", "7/4", "5/4" (khoảng cách $\Delta_3$, $\Delta_6$, $\Delta_7$). Nhãn trực tiếp cuối đường: "tập huấn luyện s", "mẫu lân cận s⁽⁴⁾". Số $1$, $\tfrac74$, $\tfrac54$ có trên mặt trang. | "Hai đường gấp khúc theo bước t từ 1 đến 7. Đường liền là điểm lặp trên tập huấn luyện (0, 1, 2, 3), đi từ 0 lên 7/4 rồi về 5/4. Đường đứt là điểm lặp trên mẫu lân cận thay 3 bằng −3, dao động giữa −1/2 và 1/2. Hai đường tách nhau ở bước 2 và bước 5, hai bước dùng quan sát thứ tư; khoảng cách bằng 1 sau bước 2, 7/4 sau bước 5 và 5/4 ở cuối." |
| F2 | `thi-nghiem-ghep-cap.svg` | 4-04 | Hai trục thang lôgarit. Trục ngang: số vòng $0{,}5$ đến $100$ (vạch $0{,}5$; $1$; $5$; $20$; $100$). Trục dọc: $0{,}01$ đến $200$ (vạch $0{,}01$; $0{,}1$; $1$; $10$; $100$). Đường cận $t/200$, tức bằng số vòng (nét liền đậm, từ $0{,}5$ đến $100$). Khoảng cách đo được (chấm tròn, nét đứt): $0{,}045$; $0{,}079$; $0{,}213$; $0{,}419$; $0{,}919$. $\Delta$ ghép cặp (ô vuông, nét chấm): $0{,}142$; $0{,}233$; $0{,}873$; $2{,}219$; $5{,}458$. Nhãn trực tiếp: "cận", "Δ ghép cặp", "khoảng cách"; nhãn số chỉ ở $100$ vòng: "100", "5,458", "0,919". | "Đồ thị lôgarit hai trục theo số vòng từ 0,5 đến 100. Đường cận đi thẳng từ 0,5 lên 100. Khoảng cách giữa lỗi kiểm tra và lỗi huấn luyện tăng từ 0,045 lên 0,919, và khoảng cách giữa hai lần chạy ghép cặp tăng từ 0,142 lên 5,458; cả hai nằm dưới đường cận và dốc ít hơn nó." |
| F3 | `danh-doi-so-buoc.svg` | 5-03 | Trục ngang $T$ thang lôgarit $1000$ đến $50\,000$ (vạch $1000$; $2000$; $5000$; $10^4$; $2\cdot10^4$; $5\cdot10^4$); trục dọc tuyến tính $[0;0{,}30]$ (vạch từng $0{,}05$). Ba đường từ vế phải của Hệ quả 08.8(a) với $R=5$, $G=1$, $m=10^4$, $\eta=0{,}05$: số hạng tối ưu $250/T$ (nét đứt, $0{,}25\to0{,}005$), số hạng ổn định $0{,}05(T-1)/10^4$ (nét chấm, $0{,}005\to0{,}25$), tổng $B(T)$ gồm cả hằng $0{,}025$ (nét liền đậm; $0{,}28$ ở hai đầu mút; $0{,}1000$ tại $5000$ và $10^4$). Chấm đặc tại $(7071;0{,}0958)$ nhãn "T* ≈ 7071: 0,0958". Đường ngang mảnh $0{,}05$ nhãn "một vòng: 0,05". Nhãn trực tiếp cuối đường: "tối ưu", "ổn định", "tổng". Số $0{,}0958$, $7071$, $0{,}05$ có trên mặt trang. | "Đồ thị theo số bước trên trục lôgarit từ 1000 đến 50 000. Đường nét đứt giảm, đường nét chấm tăng, và đường tổng có dạng chữ U với đáy 0,0958 tại khoảng 7071 bước. Đường ngang 0,05 của một vòng qua dữ liệu nằm dưới toàn bộ đường tổng." |
| F4 | `ham-loi-cosin.svg` | 6-01 | Trục ngang $t=2$ đến $101$ (vạch $2$; $21$; $41$; $58$; $81$; $101$); trục dọc thang lôgarit $[0{,}0005;5]$ (vạch $0{,}001$; $0{,}01$; $0{,}1$; $1$). Đường $\Delta_t$ của Ví dụ 08.8 (nét liền), lặp $w'_{t+1}=w'_t+0{,}1\sin w'_t$ từ $w'_2=-0{,}1\sin0{,}01$: $\Delta_2\approx0{,}0010$, $\Delta_{21}\approx0{,}0061$, $\Delta_{41}\approx0{,}0411$, $\Delta_{58}\approx0{,}207$, $\Delta_{81}\approx1{,}529$, $\Delta_{101}\approx2{,}879$. Đường ngang nét đứt $0{,}2$ nhãn "0,2"; đường ngang nét chấm $\pi$ nhãn "π". Chấm đặc tại $t=58$ nhãn "Δ₅₈ ≈ 0,207". Số $0{,}0010$, $0{,}2$, $0{,}207$ và $\pi$ có trên mặt trang. | "Đồ thị lôgarit của khoảng cách giữa hai lần chạy theo bước t từ 2 đến 101, với hàm lỗi cosin. Khoảng cách bắt đầu ở 0,001, tăng gần như thẳng trên trục lôgarit, vượt đường ngang 0,2 tại bước 58 và tiến dần tới đường π." |

Cách dựng dữ liệu hình (không có số mới trên nhãn): F1 là hai cột của bảng Ví dụ 08.2; F2 là các cột của câu hỏi mở đầu và bảng Ví dụ 08.6 cùng công thức cận $t/200$ của Ví dụ 08.5; F3 vẽ công thức của Ví dụ 08.7, Bước 3, nhãn số là số của ghi chú; F4 lặp đúng phép cập nhật của Ví dụ 08.8 (V18), nhãn số là số của bảng ghi chú. Điều phối viên ghi cách dựng vào `review-log.md`.

## 9. Trang tổng kết

Chi tiết từng trang ở mục 6 (7-01 đến 7-07). Tóm tắt:
- **Bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh` (7-01):** sáu hàng: Bổ đề 08.4 (tất định), Mệnh đề 08.5 (kì vọng theo $\xi$), Định lý 08.6 (kì vọng theo $(S,\xi)$, trị tuyệt đối), Hệ quả 08.7 (ổn định đều, bước hằng), Hệ quả 08.8 (kì vọng theo $(S,\xi)$, rủi ro vượt mức so với $W$), Mệnh đề 08.10 (kì vọng theo $\xi$). Nhận xét 08.11 và Mệnh đề 08.12 (đọc thêm) ở ghi chú diễn giả; phản ví dụ của từng giả thiết ở ghi chú diễn giả.
- **Vấn đề trung tâm (7-02):** bốn câu trả lời cho cả bài: thuật toán tác động qua ngân sách độ dài bước (với (S), (G), $\eta_t\le2/\beta$); thêm cận tối ưu, theo các cận nhiều vòng không tốt hơn một vòng; không lồi thì cận tăng theo hàm mũ, mạng ReLU không thỏa (S), (G); với mạng sâu, "huấn luyện nhanh hơn thì tổng quát hóa tốt hơn" là phỏng đoán thực nghiệm. Ghi chú diễn giả: ba mức khẳng định và so sánh với Hệ quả 07.16.
- **Bài tập tổng hợp (7-03, 7-04):** Bài tập 08.5(c), (d)(i), hai trang (đề; lời giải trên mặt trang). Lý do chọn: ghép phát biểu đầy đủ của Định lý 08.6 (bảng bảy giả thiết), ba phản ví dụ của mạch 6 (không trơn, không lồi, không có $G$ đều), Mệnh đề 08.10 và Nhận xét 08.11 (không áp dụng), và lớp ẩn cố định của Ví dụ 07.3 với cận $0{,}4G^2$; đây là câu hỏi "giả thiết nào hỏng khi chuyển sang học sâu" của bài.
- **Câu hỏi tự kiểm tra (7-05):** bốn câu, câu trả lời dự kiến ở ghi chú diễn giả: (1) vì sao dùng chung dãy chỉ số ($\tfrac14$ so với $\tfrac38$); (2) tính lồi chỉ vào qua Bổ đề 08.4(a); (3) $0{,}8$ và $\le0{,}0113$ (câu hỏi cuối buổi (a), (b)); (4) không chặn lỗi phân lớp (câu hỏi cuối buổi (c)).
- **Bài tập về nhà (7-06):** bảng `Mục | Bài tập` ánh xạ tám bài vào mạch 4–6 theo mạch cung cấp kiến thức cuối cùng (mạch 2, 3 không có hàng; mục 11, điểm 10); liên kết viewer.
- **Tài liệu tham khảo (7-07):** UML §13.1–13.2, §20.6 (trước buổi học); Hardt, Recht và Singer (2016) §2, §3.1–3.3, Phụ lục A, §1, §5 (sau buổi học); đọc mở rộng ở ghi chú diễn giả; dòng chữ "Bài 09: Học chuỗi và mô hình sinh".
- **Câu nối sang bài sau** (ghi chú diễn giả 7-07): Bài 09 hỏi rủi ro kì vọng, rủi ro thực nghiệm và giả thiết độc lập được viết lại thế nào khi mỗi quan sát là một chuỗi và hàm lỗi là $-\ln$ độ hợp lý của cả chuỗi.

## 10. Bảng thuật ngữ Việt–Anh của deck

Theo ghi chú và `thuat-ngu.md` (§10, các dòng "điều phối viên chốt (Bài 08)"); tiếng Anh trong ngoặc ở lần dùng đầu trên trang nội dung (trang ghi ở cột cuối).

| Tiếng Việt | Tiếng Anh | Lần đầu trên mặt trang |
|---|---|---|
| quan sát kiểm tra | test observation | 1-02 |
| hạ gradient ngẫu nhiên (SGD) | stochastic gradient descent | 1-06 (chữ viết tắt; tiếng Anh đã có ở Bài 05) |
| độ dài bước | step size | 1-06 |
| hạt giống ngẫu nhiên | random seed | 1-06 |
| điểm lặp cuối | last iterate | 2-01 |
| hàm lỗi Huber | Huber loss | 2-03 |
| hai lần chạy ghép cặp | coupled runs | 2-04 |
| bước chung | shared step | 2-04 |
| bước khác biệt | differing step | 2-04 |
| ngân sách độ dài bước | cumulative step-size budget | 2-04 |
| ánh xạ bước gradient | gradient step map | 2-07 |
| hệ số giãn | expansion factor | 2-07 |
| không giãn | nonexpansive | 2-07 |
| đồng bức | co-coercive (co-coercivity) | 2-07 |
| cận trên bậc hai | quadratic upper bound | 2-09 |
| bất đẳng thức truy hồi | recurrence inequality | 3-01 |
| tỉ lệ đổi nhãn dự đoán | prediction flip rate | 4-04 |
| dừng sớm | early stopping | 5-04 |
| chính quy hóa tường minh | explicit regularization | 5-04 |
| chính quy hóa ngầm | implicit regularization | 5-04 |
| tiền kích hoạt | pre-activation | 6-06 |
| điểm dừng | stationary point | 6-04 |
| tính dừng | stationarity | 6-04 |
| phỏng đoán (phỏng đoán thực nghiệm) | conjecture | 7-02 |

Chỉ ở ghi chú diễn giả (tiếng Anh trong ngoặc ở đó): xáo trộn lại sau mỗi vòng qua dữ liệu (random reshuffling), điểm dừng xấp xỉ (approximate stationary point), lịch độ dài bước (step-size schedule), cận trên bậc hai còn gọi là bổ đề hạ (descent lemma) nếu người viết dùng tên này. Đã có ở Bài 01–07, không nhắc tiếng Anh: rủi ro kì vọng, rủi ro thực nghiệm, khoảng cách tổng quát hóa kì vọng, mẫu lân cận, quan sát thay thế, ổn định đều, hệ số ổn định, điểm lặp trung bình, hàm lỗi logistic, hàm lỗi bản lề, sai số tối ưu thực nghiệm, mẫu xác thực, vòng qua dữ liệu.

## 11. Rủi ro và điểm cần điều phối viên quyết định

1. **Mạch 2 gộp §1–§5** (12 trang, 30 phút). Tách §5 thành mạch riêng thì §1–§4 không có bài tập nào trong `exercises.md` chỉ cần các mục đó (Bài tập 08.1 cần Mệnh đề 08.5; 08.3(a) cần §5), và deck có tám mạch nếu giữ mạch 3 riêng. Câu nối giữa hai nửa nằm trên mặt trang 2-06 (dòng "bước chung: khoảng cách không tăng") và 2-07 (dòng đầu). Khuyến nghị giữ.
2. **Hệ quả 08.7 không có trang "Ý tưởng chứng minh" riêng.** Ghi chú gọi nó là hệ quả, chứng minh gồm tam giác, Mệnh đề 08.5(b) cho từng $t$ và đổi thứ tự lấy tổng; lộ trình ở ghi chú diễn giả 4-05. Nếu điều phối viên coi đây là kết quả chính (nó có hàng riêng ở 7-01 và là đầu vào của Hệ quả 08.8), thêm trang `4-06` "Ý tưởng chứng minh: tính ổn định của điểm lặp trung bình" (bốn bước như mục 4) và đánh số lại 4-06 thành 4-07: 53 trang, 121 phút; cắt bù 1 phút ở 6-04.
3. **Mệnh đề 08.12 và Nhận xét 08.11 (đọc thêm) không có trang ý tưởng chứng minh.** Mệnh đề 08.12 có trang phát biểu 6-04 (Bài 10 dẫn lại nó), lộ trình Phụ lục E ở ghi chú diễn giả; Nhận xét 08.11 là một dòng trên 6-03, công thức đầy đủ ở ghi chú diễn giả. Ghi chú diễn giả nói rõ mức đọc thêm.
4. **Không có trang "Kỹ thuật." riêng.** Kỹ thuật mới của bài (ghép cặp hai lần chạy rồi Jensen; hàm phụ $q_u$ trong chứng minh tính đồng bức; bất đẳng thức trên từng quỹ đạo rồi lấy kì vọng bằng xác suất biên; đổi thứ tự lấy tổng) không được ghi chú Bài 09–10 dùng lại (tìm "ghép cặp", "không giãn", "đồng bức", "truy hồi", "cận trên bậc hai", "hệ số giãn" trong hai ghi chú đó: $0$ kết quả; Bài 10 chỉ dẫn Mệnh đề 08.12). Theo chính sách kỹ thuật, chúng là dòng "Kỹ thuật." (2-09) hoặc một bước của trang ý tưởng chứng minh. Hai kỹ thuật có trang riêng ở bài trước được nhắc lại bằng tên: lập luận đổi vai (Bài 06) ở 4-02, kì vọng có điều kiện theo lịch sử (Bài 05) ở 6-04; thêm tổng triệt tiêu (Bài 05) ở 3-02 và cân hai số hạng (Bài 05) ở 5-02. Nếu điều phối viên muốn trang "Kỹ thuật." cho ghép cặp, trang 2-05 đổi tiêu đề thành "Ghép cặp" và thêm nhãn "**Kỹ thuật.**" ở dòng Jensen, không thêm trang.
5. **Câu chữ bài tập rút gọn trên mặt trang** (giữ đủ dữ kiện, câu hỏi và kết quả; câu đầy đủ ở ghi chú diễn giả khi bị rút): 2-11 (Bài tập 08.3(a): "chỉ dùng hai tính chất của $d$" thành "chỉ dùng: $d$ không giảm và $1$-Lipschitz"); 4-06 (Bài tập 08.7: thiết lập của Ví dụ 06.3 viết bằng kí hiệu; câu "Tìm $T$ lớn nhất … làm tương tự với cận của Định lý 08.6 cho điểm lặp cuối" thành một câu hỏi với "cho $\bar w_T$, $w_{T+1}$ (Định lý 08.6)"); 7-03 (Bài tập 08.5: bỏ câu dẫn "Một báo cáo mô tả việc huấn luyện …", "$N$ nơ-ron ẩn" và "mẫu gồm" chuyển vào ghi chú diễn giả; phần (a), (b) không lên mặt trang, kết luận của chúng dẫn qua Ví dụ 08.10 ở 7-04); 7-04 (phần (d)(i) viết thành câu hỏi ngắn, câu đầy đủ ở ghi chú diễn giả). Đề nghị chấp nhận, như quyết định Bài 06 mục 11.5.
6. **Câu nối vào mạch 4** nằm trong dòng "Trực quan." của 4-01 ("Hai lần chạy gần nhau thì, theo (L), hàm lỗi gần nhau tại mọi $z$") và ghi chú diễn giả 4-01 (Mệnh đề 08.5 chặn khoảng cách tham số; Định nghĩa 06.9 cần hiệu hàm lỗi). Một dòng câu nối riêng làm 4-01 vượt 60 âm tiết và 6 dòng. Câu nối mạch 2 → 3 ở dòng cuối 2-10; mạch 3 → 4 ở 4-01; mạch 4 → 5 ở dòng đầu 4-05 và dòng "Nhắc lại:" của 5-01; mạch 5 → 6 ở 6-01 (phản ví dụ mở mạch); mạch 6 → 7 ở dòng "Kết luận:" của 6-06.
7. **Bài tập tổng hợp: Bài tập 08.5(c), (d)(i).** Phương án khác: Bài tập 08.2(b) (ba lịch độ dài bước, cận $0{,}1$; $0{,}0098$; $0{,}1986$ khi $T=10^4$), gần trọng tâm "theo số bước và độ dài bước" hơn nhưng chỉ ghép Định lý 08.6 với một phép so sánh tổng–tích phân. Khuyến nghị 08.5, vì nó kiểm cả bảy giả thiết và nối với mạch 6.
8. **Mục tiêu (1-03)** giữ đủ năm mục tiêu theo thứ tự trong trần 80 (đếm $79$); câu chữ rút: mục tiêu 1 bỏ "trên một ví dụ nhỏ", mục tiêu 2 viết "độ dài bước nhỏ" cho "độ dài bước không vượt hai lần nghịch đảo hằng số trơn", mục tiêu 3 bỏ "rồi tính các cận đó bằng số", mục tiêu 5 bỏ "cho một thiết lập huấn luyện cụ thể (…)". Ghi chú diễn giả nêu đủ các ý đã rút. Nếu điều phối viên muốn giữ điều kiện độ dài bước ở mục tiêu 2 (quyết định Bài 05 giữ "hàm lồi" ở mục tiêu 1), câu thay thế: "Chứng minh bước gradient không giãn khi hàm lồi, trơn và độ dài bước tới hai lần nghịch đảo hằng số trơn." ($22$ âm tiết, vượt trần dòng $2$; tổng $86$, cần cắt mục tiêu 3 thành "Chứng minh bất đẳng thức truy hồi; suy ra cận ổn định." ($11$)).
9. **Luận điểm bìa** $66$ âm tiết (Bài 07: $65$; Bài 06: $57$). Bản ngắn, $43$ âm tiết, mất câu về hai quỹ đạo: "Với hàm lỗi lồi, trơn, có gradient bị chặn và độ dài bước đủ nhỏ, khoảng cách tổng quát hóa kì vọng của hạ gradient ngẫu nhiên không vượt một hằng số nhân tổng các độ dài bước chia cho cỡ mẫu." Khuyến nghị bản dài: câu "hai lần chạy … tách xa nhau chậm" là cơ chế mà điều phối viên yêu cầu làm trọng tâm.
10. **Bảng `Mục | Bài tập` (7-06)** chỉ có ba hàng (mạch 4, 5, 6): theo quy tắc mạch cung cấp kiến thức cuối cùng, không bài nào chỉ cần mạch 2 hoặc 3 (Bài tập 08.1(a), (b) cần hệ số ổn định của Định lý 08.6; 08.3(b)–(e) cần hàm lỗi cosin và Mệnh đề 08.10). Hai trang bài tập 2-11, 3-04 dùng phần (a) của 08.3 và phần (c) của 08.1. Bài tập 08.2 xếp vào mạch 5 vì phần (c) so cận ổn định với cận tối ưu và câu cuối của đề cần hiểu vì sao hai cận cho hai đầu ra khác nhau không cộng được (§8); xếp vào mạch 4 nếu điều phối viên chỉ xét phần (b). Bài tập 08.6 xếp vào mạch 4 (Ví dụ 08.6, Phụ lục F).
11. **Hàm lỗi bản lề và mạng ReLU ở §2** chỉ vào ghi chú diễn giả 2-02 (mặt trang đã $43$ âm tiết sau khi bỏ dòng này); chúng lên mặt trang ở 6-06 và 7-04. Nếu cổng duyệt muốn giữ ý "giả thiết nào hỏng" ngay từ §2, thêm lại dòng "Không thỏa (S): hàm lỗi bản lề, hàm lỗi mạng ReLU theo trọng số." ($14$ âm tiết, trang thành $57$).
12. **Công thức cần đo ở 390 px** (ngắt `aligned` chỉ khi tràn): 1-02 (định nghĩa ổn định đều), 2-07 (tính đồng bức), 2-08 (b) (hai bất đẳng thức), 3-01 (b), 4-01 (c), 4-05 ($\epsilon_{\mathrm{stab}}$ của điểm lặp trung bình), 4-06 ($\psi(T)$), 5-01 (a) và dòng (b) (công thức $\eta^*$ trong dòng), 6-02 (c) (gần như chắc chắn cần ngắt: hai vế phải), 6-04, 6-07; bảng 1-06, 2-10, 7-01, 7-04, 7-06 đặt trong `.table-scroll`.
13. **Mật độ** (đếm bằng script, mục 15): không trang nội dung nào vượt $60$; 1-03 $79$/80. Trung vị $54$ trên 40 trang nội dung (bỏ 1-03, 7-01, 7-06), 10 trang ≤ 50, 19 trang 51–56, 11 trang 57–60 (4-04, 4-05, 5-01, 5-04, 6-03, 6-06, 7-02, 7-03, 7-04, 7-05, 7-07): không đạt mục tiêu trung vị 45–50. Lý do: sáu trang kết quả giữ đủ giả thiết của ghi chú (Định lý 08.6 bốn thành phần, Hệ quả 08.8 bốn thành phần, Mệnh đề 08.12 bốn thành phần), tiếng Anh ở lần dùng đầu (24 thuật ngữ), số viết trong câu có tính, và năm trang bài tập giữ câu hỏi của `exercises.md`. Biên sửa còn $0$–$3$ âm tiết ở 11 trang; người viết deck không thêm chữ trên các trang này, và khi cổng duyệt yêu cầu thêm chữ, cắt bù trên cùng trang hoặc chuyển dòng "Diễn giải:" vào ghi chú diễn giả.
14. **Tiêu đề deck có "SGD"** (trộn ngôn ngữ) vì đúng tên bài của ghi chú. Trên các trang tổng quan và tiêu đề mạch, deck viết "hạ gradient ngẫu nhiên"; trên trang nội dung, "SGD" sau lần dùng đầu ở 1-06 ("Hạ gradient ngẫu nhiên (SGD)"). Tiêu đề 4-01, 4-02 dùng "SGD" theo tên Định lý 08.6 của ghi chú.
15. **Hình F2 trên 4-04** (4 dòng chữ, $59$ âm tiết, cộng hình) và **F4 trên 6-01** (5 dòng, $47$ âm tiết): người viết deck kiểm 1600×900 với `footer_check.py`; nếu chạm chân trang, chuyển dòng tỉ lệ đổi nhãn (4-04) hoặc dòng cuối (6-01) vào ghi chú diễn giả. F1 (2-06, $23$ âm tiết) và F3 (5-03, $38$) có chỗ.
16. **Thứ tự trong §9:** Mệnh đề 08.12 (6-04) đứng trước Ví dụ 08.9 và 08.10 như ghi chú; mạch 6 vẫn là các mục liên tiếp. Ví dụ 08.8 (6-01) đứng trước Mệnh đề 08.10 như ghi chú.
17. **Kí hiệu $\mathcal F_{t-1}$** ở 6-04 là lịch sử các gradient ngẫu nhiên của Định nghĩa 05.10 (nhắc lại một dòng); kí hiệu $\Delta_t$ khác nghĩa ở chứng minh Định lý 05.14 (ghi chú diễn giả 2-04).
18. **"Nhãn" (a), (b), (c)** của kết quả và "(d)(i)" của bài tập viết thường, không in đậm; `deck_lint.py` chỉ bắt chuỗi in đậm kết thúc bằng dấu chấm hoặc hai chấm.

## 12. Bảng đối chiếu trang → mục và khối của ghi chú

Cột "Đưa vào" ghi kí hiệu, thuật ngữ hoặc kết quả xuất hiện lần đầu trên mặt trang (định nghĩa hoặc "Nhắc lại:"/"Kí hiệu:"), để kiểm quy tắc định nghĩa trước khi dùng.

| Trang | Mục ghi chú | Khối (số của ghi chú) | Đưa vào |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §10 | — (bằng lời) | — |
| 1-02 | Kiến thức tiên quyết; Câu hỏi ôn nhanh | Định nghĩa 06.9, Định lý 06.10, Định nghĩa 05.6 (nhắc lại); (T1), (T2) | $s$, $s^{(i)}$, $z_i$, $z'$, $z$, quan sát kiểm tra, $A(s;\xi)$, $\xi$, $\epsilon_{\mathrm{stab}}(m)$, $S$, $L_D$, $L_S$, $\mathbb E_{S,\xi}$, (T1), (T2), $w_1$, $\beta$-trơn, $\operatorname{proj}_W$, không giãn (của phép chiếu) |
| 1-03 | Mục tiêu học tập | — | — |
| 1-04 | toàn bài; §13 | — | — |
| 1-05 | đoạn mở đầu | — | — |
| 1-06 | Câu hỏi mở đầu và đoạn sau | — | $p$, $m$, $x$, SGD, độ dài bước, hạt giống, vòng, khoảng cách (đo được) |
| 2-00 | §1–§5 | — | — |
| 2-01 | §1; §4 | Thuật toán 08.1 | $\mathcal Z$, $D$, $Z_i$, $W$, $\ell$, $i_t$, $\eta_t$, $T$, $w_t$, $\nabla\ell$, $w_{T+1}$, $\bar w_T$, điểm lặp cuối, Thuật toán 08.1 |
| 2-02 | §2 | (S), (S′), (G), độ dài bước, (I), (R), (X); (L) (Bài 06) | $\beta$, $G$, $R$, $C_x$, (L), (S), (S′), (G), (I), (R), (X) |
| 2-03 | §3 | Ví dụ 08.1; khối ứng dụng | $z_1,\ldots,z_4$, $\ell_{\mathrm H}$, hàm lỗi Huber, Nhận xét 06.3 (tên) |
| 2-04 | §4 | Định nghĩa 08.2 | $w'_t$, hai lần chạy ghép cặp, bước chung, bước khác biệt, $\Delta_t$, ngân sách độ dài bước |
| 2-05 | §4 | hai đoạn sau Định nghĩa 08.2 | bất đẳng thức Jensen cho trị tuyệt đối, $a$, $b$ (cục bộ), $s^{(4)}$ |
| 2-06 | §4 | Ví dụ 08.2 | — |
| 2-07 | §5 | đoạn mở §5; Định nghĩa 08.3 và ba đoạn sau | $\Gamma_{\eta,z}$, ánh xạ bước gradient, $\Gamma$, $\kappa$, hệ số giãn, không giãn, $f$, tính đồng bức |
| 2-08 | §5 | Bổ đề 08.4 | $g_{uv}$, $\eta$ |
| 2-09 | §5; Phụ lục A | chứng minh Bổ đề 08.4 | cận trên bậc hai, $q_u$ |
| 2-10 | §5 | Ví dụ 08.3; đoạn cuối §5 | hệ số giãn nhỏ nhất |
| 2-11 | Bài tập 08.3 | Bài tập 08.3(a) | $d$, $\delta$ (cục bộ) |
| 3-00 | §6 | — | — |
| 3-01 | §6 | Mệnh đề 08.5 | bất đẳng thức truy hồi, $\mathbb 1[i_t=i]$ |
| 3-02 | §6; Phụ lục B(i) | chứng minh Mệnh đề 08.5 | tổng triệt tiêu (nhắc lại), $g_t$, $g'_t$ |
| 3-03 | §6 | Ví dụ 08.4 | — |
| 3-04 | Bài tập 08.1 | Bài tập 08.1(c) | — |
| 4-00 | §7 | — | — |
| 4-01 | §7 | đoạn mở §7; Định lý 08.6 | — (mọi kí hiệu đã có) |
| 4-02 | §7; Phụ lục B(ii) | chứng minh Định lý 08.6; danh sách giả thiết sau chứng minh | lập luận đổi vai (nhắc lại), định lý giá trị trung bình |
| 4-03 | §7 | Ví dụ 08.5 | hàm lỗi logistic (Bài 05), Bài tập 05.8, Ví dụ 05.9 (tên) |
| 4-04 | §7; Phụ lục F | Ví dụ 08.6 | tỉ lệ đổi nhãn dự đoán |
| 4-05 | §7 | Hệ quả 08.7; đoạn sau (Ví dụ 06.3) | — |
| 4-06 | §7 | chứng minh Hệ quả 08.7 | đổi thứ tự lấy tổng, $\bar w'_T$ |
| 4-07 | Bài tập 08.7 | Bài tập 08.7(b) | $\psi(T)$, $q$ |
| 5-00 | §8 | — | — |
| 5-01 | §8 | đoạn mở §8 (Mệnh đề 06.5(b), nhắc lại); Hệ quả 08.8 | $\tilde w$, $\operatorname{opt}_S$, $\inf_WL_D$, $\eta^*$, Định lý 05.14 (tên) |
| 5-02 | §8; Phụ lục C | chứng minh Hệ quả 08.8; đoạn sau | cân hai số hạng (nhắc lại), $a$, $b$, $\operatorname{opt}_s$, $L_s$ |
| 5-03 | §8 | Ví dụ 08.7 | $T^*$ |
| 5-04 | §8 | Định nghĩa 08.9; hai đoạn sau | dừng sớm, chính quy hóa tường minh, chính quy hóa ngầm, $\lambda$ (Bài 06) |
| 5-05 | Bài tập 08.8 | Bài tập 08.8(b) | $B(T)$ |
| 6-00 | §9 | — | — |
| 6-01 | §9 | Ví dụ 08.8 | hàm lỗi cosin, $z_j$ |
| 6-02 | §9 | Mệnh đề 08.10; đoạn sau | — |
| 6-03 | §9; Phụ lục D | chứng minh Mệnh đề 08.10; đoạn sau; Nhận xét 08.11 | $c$, (T3) (tên; định nghĩa ở ghi chú diễn giả) |
| 6-04 | §9; Phụ lục E | Mệnh đề 08.12; đoạn sau | $\mathcal F_{t-1}$ (nhắc lại), $F$, $F_*$, $g_t$ (gradient ngẫu nhiên), $\sigma^2$, tính dừng, điểm dừng |
| 6-05 | §9 | Ví dụ 08.9 | — |
| 6-06 | §9 | Ví dụ 08.10; đoạn sau | $\theta$, $\Theta_1$, $\Theta_2$, $\tilde y$, tiền kích hoạt, mạng ReLU (Bài 07) |
| 6-07 | Bài tập 08.3 | Bài tập 08.3(d) | $\varphi$, $\zeta$, $\tau$ |
| 7-00 | §10–§13 | — | — |
| 7-01 | §5–§7, §10 | Bổ đề 08.4, Mệnh đề 08.5, Định lý 08.6 | — |
| 7-02 | §7–§9 | Hệ quả 08.7, 08.8, Mệnh đề 08.10 | — |
| 7-03 | §10 | — | phỏng đoán thực nghiệm |
| 7-04 | Bài tập 08.5 | Bài tập 08.5(c) (đề) | — |
| 7-05 | Bài tập 08.5 | Bài tập 08.5(c) (lời giải) | — |
| 7-06 | Bài tập 08.5 | Bài tập 08.5(d)(i) (đề, lời giải) | $\chi(x)$ (Ví dụ 07.3) |
| 7-07 | §4, §7, §12 | câu hỏi cuối buổi (a)–(c) | — |
| 7-08 | §11 | `exercises.md` | — |
| 7-09 | §12, §13 | — | — |

Kiểm định nghĩa trước khi dùng: 2-02 dùng (L) của Bài 06 với công thức đầy đủ trên cùng dòng; 6-03 nêu tên (T3) mà ghi chú diễn giả định nghĩa (hàm lỗi trong $[0,1]$); nếu cổng duyệt muốn (T3) trên mặt trang, thay "(T3)" bằng "hàm lỗi trong $[0,1]$" (cùng số âm tiết). $\tilde y=2y-1$ dùng ở 6-06 được đặt ở dòng hàm lỗi logistic của 2-02.

## 13. Đề xuất sửa ghi chú và tệp bài tập (không sửa; chờ điều phối viên và tác giả)

Không thấy lỗi toán học trong các khối deck dùng; mọi con số của ví dụ và bảy bài tập trên mặt trang đã tính lại (mục 5) và khớp ghi chú, tệp bài tập.

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất |
|---|---|---|---|---|
| nhẹ | ghi chú, đoạn sau Câu hỏi mở đầu (dòng 23) | Câu "Với hàm lỗi lồi, trơn và có gradient bị chặn, khoảng cách tổng quát hóa kì vọng của SGD sau $T$ bước … không vượt $c\cdot\frac1m\sum_t\eta_t$" bỏ điều kiện độ dài bước $\eta_t\le2/\beta$ của Định lý 08.6 | Định lý 08.6, giả thiết "Thuật toán": "$0<\eta_t\le2/\beta$"; Ví dụ 08.9 cho thấy bỏ điều kiện này thì khoảng cách nhân đôi mỗi bước chung | Thêm "và độ dài bước không vượt hai lần nghịch đảo hằng số trơn" vào câu (bằng lời, vì kí hiệu $\beta$ chưa được đặt trước §2); ghi chú diễn giả 1-06 của deck đã nêu điều kiện này |
| nhẹ | ghi chú, Định nghĩa 08.9 | "gần $0$" chưa có ngưỡng (điểm #63 đang mở cho tác giả) | `review-log.md` lec-08, "Còn mở cho tác giả: #63" | Deck theo ghi chú ("về gần $0$"); chờ tác giả |
| nhẹ | ghi chú §2 | Nhãn mới (X), (S′), (I), (R) chờ tác giả duyệt tên | `review-log.md` lec-08, cùng dòng | Deck dùng đúng nhãn hiện hành; nếu đổi tên, sửa 2-02, 3-01, 5-01, 5-02, 6-02, 6-03, 7-01 |

## 14. Danh sách kỹ thuật đã giới thiệu đến hết Bài 08

| Kỹ thuật | Bài, trang (lần đầu) | Dạng | Trong deck Bài 08 |
|---|---|---|---|
| Tính tuyến tính của kì vọng | Bài 01, `L01-3-03` | một dòng | dùng không nhắc tên (3-02 bước 4) |
| Bất đẳng thức hợp | Bài 01, `L01-4-04` | trang riêng | không dùng |
| Chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ | Bài 01, `L01-6-07` | trang riêng | không dùng |
| Tối thiểu hóa từng điểm rồi lấy kì vọng | Bài 01, `L01-5-09` | một dòng | không dùng |
| Phương pháp Chernoff | Bài 02, `L02-3-01` | trang riêng | không dùng |
| Dây cung của hàm lồi và Taylor bậc hai tại $0$ | Bài 02, `L02-3-03` | một dòng | không dùng |
| Đảo cận đuôi thành bán kính và cỡ mẫu | Bài 02, `L02-4-04` | trang riêng | không dùng |
| Chia xác suất thất bại cho từng giả thuyết | Bài 02, `L02-5-05` | trang riêng | không dùng |
| Bước tất định trên biến cố đại diện | Bài 02, `L02-5-11` | trang riêng | gần với Mệnh đề 08.5(a) (bất đẳng thức trên mọi quỹ đạo, rồi lấy kì vọng), không nhắc tên |
| Cận dưới và cận trên cho chiều VC | Bài 03, `L03-2-04` | trang riêng | không dùng |
| Đối xứng hóa và mẫu bóng | Bài 03, `L03-5-06` | trang riêng | không dùng |
| Hàm tăng trưởng thay cho số giả thuyết | Bài 03, `L03-5-07` | trang riêng | không dùng |
| Thêm bớt kì vọng rồi bình phương | Bài 04, `L04-3-03` | một dòng | gần với khai triển bình phương ở 2-09 bước 1, không nhắc tên |
| Chia xác suất thất bại theo trọng số | Bài 04, `L04-4-04` | trang riêng | không dùng |
| Lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện | Bài 04, `L04-6-02` | một dòng | Mệnh đề 08.5(b) với tập huấn luyện cố định rồi Định lý 08.6(c) theo $(S,\xi)$; ghi chú diễn giả 4-02, không nhắc tên |
| Kì vọng có điều kiện theo lịch sử | Bài 05, `L05-3-07` | trang riêng | **nhắc lại một dòng ở 6-04** (Mệnh đề 08.12) |
| Tổng triệt tiêu và trung bình các điểm lặp | Bài 05, `L05-4-05` | trang riêng | **nhắc lại một dòng ở 3-02**; dùng ở 6-03, ghi chú diễn giả 6-04 |
| Cân hai số hạng, $a/\eta+b\eta\ge2\sqrt{ab}$ | Bài 05, `L05-4-08` | một dòng | **nhắc lại một dòng ở 5-02**; dùng ở 5-05 |
| Số hạng chéo bằng $0$ cho véc-tơ không tương quan | Bài 05 | một dòng | ghi chú diễn giả 6-04 (Phụ lục E, không nhắc tên) |
| Lập luận đổi vai (thay một điểm) | Bài 06, `L06-4-05` | trang riêng | **nhắc lại một dòng ở 4-02** (công cụ bên trong Định lý 06.10) |
| Cộng hai bất đẳng thức tăng trưởng bậc hai đối xứng | Bài 06, `L06-5-02` | một dòng | không dùng (bước "đổi vai $u$, $v$ rồi cộng" ở 2-09 bước 4 cùng dạng, không nhắc tên) |
| Điểm trên đoạn thẳng rồi cho dần về đầu mút | Bài 06, ghi chú diễn giả `L06-3-03` | một dòng | không dùng (định lý giá trị trung bình dọc đoạn thẳng ở 4-02 bước 1 là công cụ giải tích của ghi chú) |
| Đưa hàm nhiều biến về một biến bằng các hàng trùng nhau của $\Theta_1$ | Bài 07, 2-05 | một dòng | không dùng |
| Đổi biến giữa dấu và nhãn ngẫu nhiên | Bài 07, 3-04 | một dòng | không dùng |
| Sai phân của một cận trên đúng không quá sai phân lớn nhất | Bài 07, ghi chú diễn giả 4-03 | một dòng | không dùng |
| Thay hàm lỗi 0–1 bằng hàm lỗi bị chặn, Lipschitz rồi dùng bổ đề co | Bài 07, 5-06 | một dòng | không dùng (4-04: hàm lỗi 0–1 không Lipschitz, nên Định lý 08.6 không chặn tỉ lệ đổi nhãn) |
| **Ghép cặp hai lần chạy rồi Jensen**, $\lvert\mathbb E_\xi a-\mathbb E_\xi b\rvert\le\mathbb E_\xi\lvert a-b\rvert$ | **Bài 08, 2-05** | một dòng ("Trực quan.") | dùng ở 4-02 bước 3 |
| **Hàm phụ $q_u=f-\langle\nabla f(u),\cdot\rangle$** cực tiểu tại $u$ (tính đồng bức từ tính lồi và tính trơn) | **Bài 08, 2-09** | một dòng "Kỹ thuật." | — |
| **Bất đẳng thức trên từng quỹ đạo, rồi kì vọng chỉ qua xác suất biên $\Pr(i_t=i)$** | **Bài 08, 3-02 bước 3–4** | một bước của ý tưởng chứng minh | dùng lại ở 6-03 bước 3; cho phép xáo trộn lại (ghi chú diễn giả 3-01) |
| **Đổi thứ tự lấy tổng** ($\eta_k$ xuất hiện $T-k$ lần) | **Bài 08, ghi chú diễn giả 4-05** | một câu | — |

Bài 08 không có trang "Kỹ thuật." riêng (mục 11, điểm 4): ghi chú Bài 09–10 không dùng lại các kỹ thuật mới của bài. Deck Bài 10 nhắc lại Mệnh đề 08.12 (kết quả, không phải kỹ thuật) nếu dùng.

## 15. Mật độ mặt trang đo bằng script

> Bảng dưới là số đo của bản lập. Số đo của deck cuối: mục 16 (trước năm báo cáo duyệt) và mục 17 (sau khi sửa).

Đếm bằng `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-08/storyboard/count.py` (bản của storyboard Bài 07) trên văn bản dự kiến của mục 6: token cách nhau bởi khoảng trắng, có chữ cái hoặc chữ số; bỏ tiêu đề, công thức `$…$`, chỉ dẫn `{{…}}`, dấu fragment; nhãn "(T1)", "(a)", số khối như "08.6" và tiếng Anh trong ngoặc được đếm (số viết trong câu có tính). Cột "Chữ ngoài bảng" là cách đếm của `deck_lint.py` (bỏ bảng); cột "Kể cả chữ trong bảng" cộng các ô có chữ. Mỗi gạch đầu dòng hoặc mục đánh số là một dòng; mỗi công thức hiển thị thêm một dòng (số 0 trong cột theo dòng); một bảng là một dòng. Tiêu đề thẻ h3 "Hồi quy logistic nhiều vòng" ở 2-03 thêm $5$ âm tiết trên deck ($57$). Trang tổng quan và trang tiêu đề mạch không tính trần (bìa: luận điểm $66$ âm tiết; hộp Vấn đề trung tâm $17$; câu dẫn mạch $23$–$25$). Ghi chú diễn giả đếm cùng script, bỏ dòng nguồn. Kết quả đầy đủ: `counts.txt` cùng thư mục.

| Trang | Chữ ngoài bảng | Kể cả chữ trong bảng | Dòng | Theo dòng | Ghi chú diễn giả |
|---|---:|---:|---:|---|---:|
| 1-01 | (tổng quan hoặc tiêu đề mạch; 36) | — | — | — | 117 |
| 1-02 | 51 | 51 | 5 | 20; 0; 13; 9; 9 | 106 |
| 1-03 | 79 | 79 | 5 | 13; 15; 20; 15; 16 | 129 |
| 1-04 | (tổng quan hoặc tiêu đề mạch; 62) | — | — | — | 88 |
| 1-05 | (tổng quan hoặc tiêu đề mạch; 26) | — | — | — | 98 |
| 1-06 | 54 | 63 | 5 | 10; 16; 14; 14; bảng 9 | 131 |
| 2-00 | (tổng quan hoặc tiêu đề mạch; 34) | — | — | — | 86 |
| 2-01 | 49 | 49 | 6 | 10; 9; 14; 0; 11; 5 | 104 |
| 2-02 | 43 | 43 | 5 | 11; 6; 8; 7; 11 | 113 |
| 2-03 | 52 | 52 | 6 | 6; 7; 9; 4; 11; 15 | 88 |
| 2-04 | 53 | 53 | 5 | 16; 7; 9; 13; 8 | 79 |
| 2-05 | 53 | 53 | 5 | 19; 13; 4; 3; 14 | 76 |
| 2-06 | 23 | 23 | 4 | 7; 10; 6; 0 | 81 |
| 2-07 | 53 | 53 | 6 | 13; 7; 16; 7; 0; 10 | 74 |
| 2-08 | 43 | 43 | 6 | 17; 13; 9; 1; 0; 3 | 93 |
| 2-09 | 54 | 54 | 5 | 2; 15; 11; 17; 9 | 139 |
| 2-10 | 51 | 56 | 5 | 18; 4; 13; 16; bảng 5 | 92 |
| 2-11 | 54 | 54 | 6 | 14; 8; 16; 2; 13; 1 | 62 |
| 3-00 | (tổng quan hoặc tiêu đề mạch; 30) | — | — | — | 58 |
| 3-01 | 55 | 55 | 5 | 16; 15; 14; 10; 0 | 103 |
| 3-02 | 51 | 51 | 5 | 14; 10; 8; 9; 10 | 142 |
| 3-03 | 45 | 45 | 6 | 12; 4; 3; 3; 4; 19 | 59 |
| 3-04 | 56 | 56 | 6 | 11; 11; 16; 7; 4; 7 | 91 |
| 4-00 | (tổng quan hoặc tiêu đề mạch; 32) | — | — | — | 67 |
| 4-01 | 56 | 56 | 6 | 16; 15; 10; 11; 4; 0 | 125 |
| 4-02 | 55 | 55 | 5 | 13; 16; 4; 14; 8 | 137 |
| 4-03 | 53 | 53 | 5 | 12; 10; 4; 11; 16 | 75 |
| 4-04 | 59 | 59 | 4 | 20; 13; 12; 14 | 138 |
| 4-05 | 59 | 59 | 5 | 9; 18; 17; 0; 15 | 93 |
| 4-06 | 56 | 56 | 6 | 19; 0; 9; 19; 3; 6 | 77 |
| 5-00 | (tổng quan hoặc tiêu đề mạch; 29) | — | — | — | 86 |
| 5-01 | 58 | 58 | 6 | 5; 18; 20; 6; 0; 9 | 88 |
| 5-02 | 56 | 56 | 6 | 11; 10; 12; 8; 5; 10 | 105 |
| 5-03 | 38 | 38 | 4 | 11; 6; 5; 16 | 75 |
| 5-04 | 60 | 60 | 5 | 14; 11; 11; 16; 8 | 145 |
| 5-05 | 47 | 47 | 5 | 13; 11; 9; 2; 12 | 92 |
| 6-00 | (tổng quan hoặc tiêu đề mạch; 28) | — | — | — | 84 |
| 6-01 | 47 | 47 | 5 | 4; 14; 7; 4; 18 | 96 |
| 6-02 | 53 | 53 | 6 | 15; 18; 9; 4; 0; 7 | 76 |
| 6-03 | 57 | 57 | 6 | 9; 20; 8; 6; 5; 9 | 121 |
| 6-04 | 55 | 55 | 6 | 15; 9; 7; 0; 8; 16 | 86 |
| 6-05 | 41 | 41 | 6 | 6; 8; 4; 3; 3; 17 | 51 |
| 6-06 | 60 | 60 | 5 | 11; 11; 13; 8; 17 | 144 |
| 6-07 | 44 | 44 | 6 | 14; 0; 15; 10; 2; 3 | 96 |
| 7-00 | (tổng quan hoặc tiêu đề mạch; 15) | — | — | — | 98 |
| 7-01 | 0 | 103 | 1 | ; bảng 103 | 115 |
| 7-02 | 59 | 59 | 4 | 11; 15; 17; 16 | 149 |
| 7-03 | 59 | 59 | 4 | 13; 10; 16; 20 | 124 |
| 7-04 | 57 | 89 | 6 | 3; 15; 19; 5; 15; bảng 32 | 156 |
| 7-05 | 59 | 59 | 4 | 12; 15; 12; 20 | 116 |
| 7-06 | 10 | 49 | 2 | 10; bảng 39 | 126 |
| 7-07 | 58 | 58 | 5 | 6; 15; 14; 15; 8 | 127 |

Trần: 60 cho trang nội dung, 80 cho 1-03, 7-01, 7-06; mọi dòng ≤ 20; mọi trang ≤ 6 dòng; ≤ 3 công thức hiển thị. Kết quả theo chữ ngoài bảng (`deck_lint.py`): không trang nào vượt trần (lớn nhất $60$ ở 5-04, 6-06, 7-02; 1-03 $79$/80); không dòng nào vượt 20; không trang nào quá 6 dòng. Khi tính cả chữ trong bảng: 1-06 $63$, 2-10 $56$, 7-01 $103$/80, 7-04 $89$, 7-06 $49$; bảng 7-01 vượt trần 80 khi tính chữ trong bảng (câu "Bài 07 đã chấp nhận 87" ở bản lập là sai: cổng duyệt Bài 07 xếp 7-01 82/80 là nghiêm trọng; deck cuối tách bảng thành hai trang, mục 16); phương án cắt: bỏ cột loại bảo đảm khỏi ô "Kết quả" và nêu nó ở ghi chú diễn giả, nhưng bài học deck 02 yêu cầu giữ loại bảo đảm trong bảng tổng kết, nên khuyến nghị giữ. Trung vị $54$ trên 40 trang nội dung (bỏ 1-03, 7-01, 7-06); 10 trang ≤ 50, 19 trang 51–56, 11 trang 57–60 (mục 11, điểm 13). Trang bài tập giữ câu hỏi của `exercises.md` (2-11, 3-04, 4-06, 5-05, 6-07, 7-03, 7-04; câu rút gọn ở mục 11, điểm 5). Ghi chú diễn giả: mọi trang ≤ 150 trừ trang ý tưởng chứng minh và bài tập (trần 250; lớn nhất 7-04 $156$).

## 16. Đối chiếu với deck cuối (người viết deck, 2026-11-16)

Deck: `2627-1/lecture-08-on-dinh-sgd-hoc-sau.html`, 55 trang; hình `img/lec-08/{hai-lan-chay-huber,thi-nghiem-ghep-cap,danh-doi-so-buoc,ham-loi-cosin}.svg` (sinh bằng script trong thư mục nháp `lec-08/writer/make_svg.py`, dữ liệu như mục 8; F4 lặp đúng phép cập nhật của Ví dụ 08.8, kiểm $\Delta_{58}=0{,}207316$ là giá trị đầu tiên vượt $0{,}2$). Mục 6 giữ nguyên làm bản lập; khi lệch, mục này và deck thắng. Các quyết định của điều phối viên (cuối `review-log.md`) và phát hiện của cổng duyệt đã áp dụng như dưới.

**Đánh số lại.** Thêm `4-06` "Ý tưởng chứng minh: tính ổn định của điểm lặp trung bình" (T6; bốn bước của chứng minh ghi chú, dòng "Kỹ thuật." đổi thứ tự lấy tổng); bài tập 08.7 thành `4-07`. Mạch 7: `7-01` Bảng tổng kết (Bổ đề 08.4, Mệnh đề 08.5, Định lý 08.6), `7-02` Bảng tổng kết (tiếp) (Hệ quả 08.7, 08.8, Mệnh đề 08.10; dòng "Đọc thêm: Nhận xét 08.11, Mệnh đề 08.12"), `7-03` Vấn đề trung tâm, `7-04` Bài tập 08.5 (đề, phần (c)), `7-05` lời giải (c), `7-06` Bài tập 08.5(d)(i) (câu hỏi và lời giải), `7-07` Câu hỏi tự kiểm tra, `7-08` Bài tập về nhà, `7-09` Tài liệu tham khảo. Tổng 55 = trần. Lý do: N1 (bảng sáu hàng giữ chữ "kì vọng theo $\xi$/$(S,\xi)$" có $\approx87$ chữ > 80, tách hai trang như Bài 06–07); L11 (câu hỏi (d)(i) không đứng trên trang lời giải (c); đề (c) và (d)(i) chung một trang là $\approx77$ âm tiết, lời giải (c) và (d)(i) chung một trang $\approx69$).

**Lệch so với mục 6 và lý do (ngoài các sửa theo cổng duyệt đã nêu trong báo cáo cổng).**

| Trang | Lệch | Lý do |
|---|---|---|
| 1-02 | Thêm "$\xi$ là nguồn ngẫu nhiên riêng của $A$", "tại khởi tạo $w_1$" (L2); bỏ "(Bài 05)" sau phép chiếu | định nghĩa trước khi dùng; trần 60 |
| 1-03 | Mục tiêu 2 giữ điều kiện đầy đủ (23 âm tiết một dòng, vượt 20/dòng); mục tiêu 1, 3, 4, 5 rút để tổng $80$ | quyết định của điều phối viên (T10) |
| 1-06 | Danh sách và bảng đặt hai cột (`grid2`); câu hỏi "đại lượng nào quyết định khoảng cách?", "chỉ số bước thay đổi" vào ghi chú diễn giả | chạm chân trang; cắt N1 |
| 2-01 | "Mục tiêu:" thành "Cần chặn …"; thêm "$w_1\in W$ tất định" vào Thuật toán 08.1, "điểm lặp trung bình" (L3) | đầu vào của thuật toán; tránh từ "Mục tiêu" trên trang nội dung |
| 2-02 | Thêm "(T3) $\ell(w,z)\in[0,1]$" | T8 (đủ danh sách §2) |
| 2-03 | Bỏ tiêu đề thẻ h3; "Một vòng theo thứ tự: cận rủi ro vượt mức kì vọng $\le0{,}0500$" | T2; "theo thứ tự" là thuật toán của Nhận xét 06.3 |
| 2-04 | Mở bằng câu ghép cặp (theo câu §4 của ghi chú); gộp bước chung/khác biệt một dòng; giữ $\sum_{t=1}^T\eta_t$ (KaTeX, không tính âm tiết) | T1; định nghĩa cần đối tượng |
| 2-05 | Dòng Jensen thành "Kỹ thuật." + dòng "Dùng khi …"; chỗ dùng lại ở ghi chú diễn giả | T3 (không dẫn trang sau trên mặt) |
| 2-06, 4-04, 5-03, 6-01 | Hình trong `grid2`, chú thích là `figcaption`, lớp `short-l` khi cần | `footer_check.py`; F4 đổi tỉ lệ khung 760×370 để chữ hình $\ge16$ px ở 1600 |
| 2-07 | Câu "vế trái âm khi $u\ne v$" thành công thức $-(u-v)^2<0$ | hạ trung vị (N1) |
| 2-08 | "Trực quan." một dòng (hệ số góc trong $[1-\eta\beta,1]\subset[-1,1]$, khi $f$ khả vi hai lần); phần "tính lồi cho cận trên …" vào ghi chú diễn giả | T4, L4 |
| 2-09 | "Kỹ thuật." bỏ vế "$q_u$ không có cực tiểu khi $f=-\tfrac12w^2$" (vào ghi chú) | cắt N1 |
| 2-10 | Dòng ngưỡng thành "Diễn giải:"; định nghĩa hệ số giãn nhỏ nhất viết $\max\lvert\Gamma'\rvert$ (lời đầy đủ ở ghi chú) | trang ví dụ kết thúc bằng "Diễn giải:"; chạm chân trang |
| 2-11 | Bỏ "$\Gamma(w)=-2w$ trên $[-1,1]$" khỏi lời giải (vào ghi chú) | chạm chân trang |
| 3-04 | Lời giải dòng cuối "tổng $\tfrac3{16}=1-\tfrac{13}{16}$" | rõ nghĩa |
| 4-01 | Dòng nối không nhãn (Mệnh đề 08.5, (L)); "Trực quan." theo đơn vị; bỏ "$W$ khác rỗng, đóng, lồi" vì là đầu vào của Thuật toán 08.1 (nêu ở ghi chú diễn giả); (c) công thức trong dòng | T5; trần 60 và chân trang |
| 4-02 | Giữ dòng "Nhắc lại: Định lý 06.10 dựa trên lập luận đổi vai (Bài 06)" (lệch L5) | tin nhắn giao việc của điều phối viên liệt kê lập luận đổi vai trong các kỹ thuật chỉ nhắc lại; tiêu đề bỏ "SGD" (L15) |
| 4-03 | Giữ "Diễn giải:" nhưng viết lại theo câu "Tóm lại" của ghi chú ($\eta T\ll m$; vượt $1$ từ vòng thứ hai) | trang ví dụ kết thúc bằng "Diễn giải:"; không trùng dòng trên (gate mục 6) |
| 4-04 | Tiêu đề "Ví dụ: ghép cặp trong thí nghiệm mở đầu"; tỉ lệ đổi nhãn, $2{,}99$ (dãy độc lập) vào ghi chú diễn giả | gate mục 6; tiêu đề một dòng |
| 4-05 | Dòng đầu "Cận tối ưu của Bài 05 dùng $\bar w_T$"; vế cuối viết bằng công thức $\lvert\mathbb E_{S,\xi}[L_D(\bar w_T)-L_S(\bar w_T)]\rvert$; lộ trình chứng minh chuyển sang 4-06 | trần 60; T6 |
| 4-07 | Tiêu đề "Bài tập: hồi quy bình phương nhiều vòng"; $\psi(T)$ trong dòng; thêm "$y=\pm1$ đồng khả năng" | tiêu đề một dòng; chân trang; dữ kiện của đề |
| 5-01 | Tiêu đề "Rủi ro vượt mức kì vọng sau nhiều vòng" (L15); "Nhắc lại:" có $\operatorname{opt}_S$ và $\tilde w$ (T9; Định nghĩa 04.2 ở ghi chú); (a) trong dòng; (b) bỏ biểu thức giá trị tại $\eta^*$ (vào ghi chú) | chân trang |
| 5-02 | Bước 2 thêm (G) (L6); tiêu đề rút | L6, L15 |
| 5-03 | "nhỏ nhất $\le0{,}0958$" (L7); công thức $B(T)$ chuyển vào ghi chú; chấm F3 ở $0{,}0957$, nhãn "≤ 0,0958" | L7; chân trang |
| 5-04 | Theo T13: "Định nghĩa 08.9. Ba cách điều khiển đầu ra:" và ba mục; dừng sớm viết "dừng trước khi $\operatorname{opt}_s$ về gần $0$" | trần 60 |
| 6-01 | L8; bước chung "nhân khoảng $1{,}1$"; phép cập nhật $w'_{t+1}=w'_t+0{,}1\sin w'_t$ và "hàm lỗi $2$ và gần $0$" vào ghi chú; "Diễn giải:" nêu $w_t=0$ cực đại, $-\pi$ cực tiểu | chân trang ở 1600×900 |
| 6-02 | Bỏ dòng "Bước hằng" (lên 6-03) | gate mục 6 |
| 6-03 | Dòng Nhận xét 08.11 vào ghi chú diễn giả (đủ giả thiết, $G=1$); dòng $275{,}6$ ghi $\beta=G=1$ và công thức bước hằng | T8 |
| 6-04 | $0{,}0153$ vào ghi chú; "$W=\mathbb R^p$" thêm vào giả thiết; tiêu đề rút | gate mục 6; L9 nghĩa $g_t$ ở ghi chú |
| 6-05 | Dãy $\Delta_2,\ldots,\Delta_8$ tách hai đoạn KaTeX | màn 390 px không cắt chữ |
| 6-06 | "Kết luận:" giữ "lớp ẩn cố định, chỉ lớp ra được huấn luyện"; $\Theta_1$ (lớp ẩn), $\Theta_2$ (lớp ra); Bài tập 07.5(c) vào ghi chú | L10; trần 60 |
| 6-07 | $\tau$ định nghĩa trong đề (T7); bất đẳng thức của đề trong dòng | chân trang |
| 7-00 | Dòng dẫn "Với hàm lỗi lồi, trơn, có gradient bị chặn, ngân sách độ dài bước chặn khoảng cách tổng quát hóa kì vọng." (22) | L12; vế "mạng sâu là phỏng đoán" làm dòng dẫn vượt 25, nên đặt ở 7-03 |
| 4-00 | Dòng dẫn "Với hàm lỗi lồi, trơn, khoảng cách tổng quát hóa kì vọng tăng không nhanh hơn ngân sách độ dài bước chia cho cỡ mẫu." (25) | L12 |
| 6-00 | Dòng dẫn "… bước chung có thể đẩy hai lần chạy ra xa; …" (23) | `deck_lint` LEAD25 |
| 7-03 | Bốn dòng: tác động qua ngân sách (điều kiện, công thức cho $w_{T+1}$); $10^4$ hồ sơ; không lồi: hàm mũ của ngân sách độ dài bước; mạng ReLU huấn luyện mọi lớp không thỏa (S), (G), với mạng sâu là phỏng đoán (conjecture). Câu "huấn luyện nhanh hơn thì tổng quát hóa tốt hơn" ở ghi chú | T12; trần 60 |
| 7-04–7-06 | Đề (c) trên 7-04; câu hỏi (d)(i) rút gọn trên 7-06 cùng lời giải ở fragment; câu đầy đủ (d) ở ghi chú; "Định lý 08.6, Mệnh đề 08.10 và Nhận xét 08.11 đều không áp dụng" ở ghi chú 7-05 | L11; trần 60 |
| 7-07 | Câu 4 "Cận ở câu 3 có chặn hiệu lỗi phân lớp không?" | gate mục 6 |
| 7-09 | Gộp tài liệu và mục đọc; mục mở rộng ở ghi chú; "Bài 09: Học chuỗi và mô hình sinh." là chữ, chưa liên kết | gate mục 6; bản giao việc |

**Không đổi theo cổng.** Không thêm trang "Kỹ thuật." riêng; nhãn (X), (S′), (I), (R) theo ghi chú; "SGD" chỉ còn ở tiêu đề 1-01 và 4-01 (tên bài, tên Định lý 08.6).

**Kiểm tra máy (deck cuối).** `deck_lint.py`: 0 phát hiện. `footer_check.py`: 0 trang. `deck_check.py`: 55 trang, console 0, pageerrors 0, failed 0, không `.katex-error`; OVERFLOW 1–3 px ở 2-03, 5-01, 5-02, 5-05, 7-07 là đuôi SVG của `\sqrt` (báo động giả đã biết). Đã xem ảnh 1600×900 và 390×844 (kể cả ảnh `-end`) của mọi trang; ở 390 px, công thức hiển thị và bảng rộng cuộn ngang tại chỗ.

**Mật độ (cách đếm của `deck_lint.py`, chữ trong ô bảng có tính).** 41 trang nội dung (bỏ bìa, tiêu đề mạch, Mục tiêu, Nội dung, Vấn đề trung tâm mở đầu, hai bảng tổng kết, Bài tập về nhà, Tài liệu): trung vị $50$, $21$ trang $\le50$, lớn nhất $60$ (2-04, 4-01, 5-04, 6-06, 7-03, 7-04). 1-03: $80/80$; 7-02: $66/80$; 7-01: $54/80$. Không trang nào quá 6 dòng (1-04 Nội dung 7 dòng, được miễn). Ghi chú diễn giả $\le150$ (trang thường) và $\le250$ (ý tưởng chứng minh, bài tập).

| Trang | Tiêu đề | Âm tiết | Dòng | Ghi chú diễn giả |
|---|---|---:|---:|---:|
| 1-01 | Tính ổn định của SGD và tổng quát hóa trong học sâu | bìa (luận điểm 60) | 3 | 126 |
| 1-02 | Tiên quyết và quy ước | 59 | 6 | 133 |
| 1-03 | Mục tiêu | 80 | 5 | 130 |
| 1-04 | Nội dung | 46 | 7 | 94 |
| 1-05 | Vấn đề trung tâm | 17 | 1 | 109 |
| 1-06 | Ví dụ: khoảng cách tổng quát hóa theo số vòng qua dữ liệu | 54 | 5 | 120 |
| 2-00 | Hai lần chạy ghép cặp và bước gradient không giãn | 24 | — | 91 |
| 2-01 | Thiết lập bài toán | 56 | 6 | 118 |
| 2-02 | Giả thiết | 44 | 5 | 123 |
| 2-03 | Ví dụ: hàm lỗi Huber và hồi quy logistic nhiều vòng | 58 | 6 | 98 |
| 2-04 | Hai lần chạy ghép cặp | 60 | 5 | 102 |
| 2-05 | Ghép cặp và hiệu hai kì vọng | 59 | 6 | 121 |
| 2-06 | Ví dụ: hai lần chạy ghép cặp trong ví dụ Huber | 30 | 4 | 91 |
| 2-07 | Ánh xạ bước gradient và tính đồng bức | 46 | 6 | 90 |
| 2-08 | Bước gradient không giãn | 40 | 6 | 88 |
| 2-09 | Ý tưởng chứng minh: bước gradient không giãn | 50 | 5 | 156 |
| 2-10 | Ví dụ: hệ số giãn của bước gradient một chiều | 41 | 5 | 96 |
| 2-11 | Bài tập: bước gradient của hàm lỗi Huber | 52 | 6 | 89 |
| 3-00 | Bất đẳng thức truy hồi | 24 | — | 65 |
| 3-01 | Bất đẳng thức truy hồi cho hai lần chạy ghép cặp | 55 | 5 | 118 |
| 3-02 | Ý tưởng chứng minh: bất đẳng thức truy hồi | 50 | 5 | 152 |
| 3-03 | Ví dụ: kì vọng của khoảng cách trong ví dụ Huber | 45 | 6 | 67 |
| 3-04 | Bài tập: ví dụ Huber với độ dài bước 1 | 57 | 6 | 108 |
| 4-00 | Tính ổn định đều của hạ gradient ngẫu nhiên | 25 | — | 74 |
| 4-01 | Tính ổn định đều của SGD | 60 | 5 | 113 |
| 4-02 | Ý tưởng chứng minh: tính ổn định đều | 55 | 5 | 168 |
| 4-03 | Ví dụ: cận ổn định cho hồi quy logistic | 49 | 5 | 84 |
| 4-04 | Ví dụ: ghép cặp trong thí nghiệm mở đầu | 59 | 3 | 136 |
| 4-05 | Tính ổn định của điểm lặp trung bình | 49 | 5 | 89 |
| 4-06 | Ý tưởng chứng minh: tính ổn định của điểm lặp trung bình | 48 | 5 | 95 |
| 4-07 | Bài tập: hồi quy bình phương nhiều vòng | 59 | 6 | 124 |
| 5-00 | Đánh đổi giữa tối ưu và ổn định | 25 | — | 99 |
| 5-01 | Rủi ro vượt mức kì vọng sau nhiều vòng | 53 | 5 | 135 |
| 5-02 | Ý tưởng chứng minh: rủi ro vượt mức sau nhiều vòng | 57 | 6 | 147 |
| 5-03 | Ví dụ: số vòng qua dữ liệu cho hồi quy logistic | 45 | 4 | 94 |
| 5-04 | Dừng sớm, chính quy hóa tường minh và chính quy hóa ngầm | 60 | 5 | 150 |
| 5-05 | Bài tập: số bước tốt nhất với độ dài bước cố định | 47 | 5 | 99 |
| 6-00 | Khi bỏ tính lồi hoặc tính trơn | 23 | — | 94 |
| 6-01 | Ví dụ: bỏ tính lồi với hàm lỗi cosin | 33 | 4 | 106 |
| 6-02 | Bất đẳng thức truy hồi khi bỏ tính lồi | 46 | 5 | 88 |
| 6-03 | Ý tưởng chứng minh: bất đẳng thức truy hồi khi bỏ tính lồi | 49 | 5 | 149 |
| 6-04 | Điểm dừng xấp xỉ trên hàm mục tiêu trơn | 50 | 5 | 107 |
| 6-05 | Ví dụ: độ dài bước vượt $2/\beta$ | 41 | 6 | 59 |
| 6-06 | Ví dụ: hàm lỗi không trơn và mạng ReLU | 60 | 5 | 148 |
| 6-07 | Bài tập: khoảng cách tăng theo hàm mũ với hàm lỗi cosin | 44 | 5 | 95 |
| 7-00 | Tổng kết | 22 | — | 102 |
| 7-01 | Bảng tổng kết | 54 | 1 | 125 |
| 7-02 | Bảng tổng kết (tiếp) | 66 | 2 | 118 |
| 7-03 | Vấn đề trung tâm | 60 | 4 | 134 |
| 7-04 | Bài tập: kiểm tra giả thiết cho mạng ReLU | 60 | 4 | 136 |
| 7-05 | Bài tập: kiểm tra giả thiết cho mạng ReLU, lời giải | 42 | 3 | 123 |
| 7-06 | Bài tập: cố định lớp ẩn của mạng ReLU | 58 | 4 | 149 |
| 7-07 | Câu hỏi tự kiểm tra | 48 | 4 | 127 |
| 7-08 | Bài tập về nhà | 33 | 2 | 130 |
| 7-09 | Tài liệu tham khảo | 50 | 3 | 140 |

**Bảng đối chiếu trang → khối ghi chú (bổ sung mục 12).** 4-06: chứng minh Hệ quả 08.7 (đưa vào: đổi thứ tự lấy tổng, $\bar w'_T$). 4-07 = 4-06 cũ (Bài tập 08.7). 7-01, 7-02 = 7-01 cũ; 7-03 = 7-02 cũ; 7-04 = 7-03 cũ (Bài tập 08.5(c)); 7-05, 7-06 = 7-04 cũ (lời giải (c); (d)(i), đưa vào $\chi(x)$); 7-07, 7-08, 7-09 = 7-05, 7-06, 7-07 cũ. Kí hiệu mới trên mặt trang so với mục 12: (T3) ở 2-02; $\operatorname{opt}_S$, $\tilde w$ ở 5-01 (Nhắc lại); $\tau$ ở 6-07 (trong đề); $\Theta_1$, $\Theta_2$ kèm tên lớp ở 6-06; $\max\lvert\Gamma'\rvert$ ở 2-10.

## 17. Sửa sau năm báo cáo duyệt (người sửa, 2026-11-16)

Đầu vào: `reviews/deck-{hoc-vien,toan-hoc,chuyen-gia,su-pham,mach-truyen}.md` và quyết định của điều phối viên ở cuối `review-log.md` (chấp nhận mọi phát hiện; bảng quyết định thắng báo cáo). Mục này thay mục 16 ở mọi chỗ lệch. Số trang giữ 55. Bản deck trước khi sửa: thư mục nháp `lec-08/editor/frozen.html`.

**Kiểm máy sau khi sửa.** `deck_lint.py` 0; `footer_check.py` 0; `deck_check.py --shots`: 55 trang, console 0, pageerrors 0, failed 0, không `.katex-error`; OVERFLOW 1–5 px ở 2-03, 5-01, 5-02, 5-05, 7-07 là đuôi `\sqrt` (báo động giả đã biết). Đã xem ảnh 1600×900 và 390×844 (kể cả `-end`) của mọi trang. Phím →, ↓, Space, Esc (overview) và `#/2`…`#/7` của trang Nội dung đúng (mở đúng 2-00…7-00). Mật độ (cách đếm `deck_lint`): 41 trang nội dung, trung vị $50$, $21$ trang $\le50$, lớn nhất $60$; 1-03 $80/80$, 7-01 $77/80$, 7-02 $64/80$.

**Mã phát hiện.** HV = học viên (theo thứ tự bảng, HV1 là nghiêm trọng), TH = toán học (số của báo cáo), CG = chuyên gia (CG1 nghiêm trọng, rồi theo thứ tự bảng), SP = sư phạm (theo thứ tự bảng), MT = mạch truyện (mã M/N của báo cáo).

| Mã | Trang | Phát hiện (tóm tắt) | Kết quả |
|---|---|---|---|
| HV1 (ng.tr.) | 2-05 | hiệu $\tfrac38-\tfrac18$ không gọi tên; $\tfrac38$ hai nghĩa; "phân bố cũ" | đã sửa: $\mathbb E_\xi w_2-\mathbb E_\xi w'_2=\tfrac38-\tfrac18=\tfrac14$; $\mathbb E\lvert w_2-w'_2\rvert=\tfrac38>\tfrac14$; "Trực quan." nói phân bố của Thuật toán 08.1 |
| HV2 | 1-02 | $W$, $\operatorname{proj}_W$, "không giãn", (T1)/(T2) dùng trước | đã sửa: (T1), (T2) lên trước Định lý 06.10; tính trơn chuyển vào (S) ở 2-02 (công thức, Định nghĩa 05.6); phép chiếu không giãn nhắc ở 2-08(c) "Bài 05" |
| HV3 | 6-04 | $g_t$, $F$ không gọi tên | đã sửa: "hàm mục tiêu $F$", "gradient ngẫu nhiên $g_t$" |
| HV4 | 6-06 | thiếu dữ liệu ví dụ; $\Theta_1$, $\Theta_2$ không nhắc lại | đã sửa: $\pm0{,}01\mapsto\mp0{,}49$, $z=0$; $0{,}99\mapsto1{,}49$, $1{,}01\mapsto1{,}01$; dòng "Nhắc lại:" mạng ReLU, $\Theta_1$ (lớp ẩn), $\Theta_2$ (lớp ra); "Kết luận:" chuyển: điều kiện áp dụng (lớp ẩn cố định trước khi thấy mẫu, chỉ lớp ra, $G=\sup\lVert\chi\rVert$) ở 7-06 và ghi chú diễn giả 6-06 (trần 60, giữ 55 trang) |
| HV5 | 5-01 | (b) viết điều kiện thành khẳng định | đã sửa: "nếu $\eta^*\le2/\beta$, vế phải tại $\eta^*$ …" |
| HV6 | 5-01, 5-02, 5-04 | $\operatorname{opt}_S$ chỉ gọi tên; $s$, $L_s$ chữ thường | đã sửa: công thức $\operatorname{opt}_S(w)=L_S(w)-\inf_WL_S$ trong "Nhắc lại:"; 5-02 "tập huấn luyện cố định $s$" |
| HV7 | toàn deck | mật độ ở trần | đã sửa một phần: trung vị về $50$ (cắt 2-02, 2-07, 3-01, 4-02, 6-03; chữ chuyển vào ghi chú diễn giả); cách đếm số trong KaTeX không áp dụng theo quyết định |
| HV8 | 2-07 | $\Gamma_{\eta_t,z_{i_t}}$ dùng trước định nghĩa | đã sửa: đổi thứ tự hai dòng |
| HV9 | 2-09 | (a) dùng ở bước 2, chứng minh ở bước 4 | đã sửa: chứng minh (a) thành bước 1; ghi chú đánh số lại |
| HV10 | 4-02, 4-06 | bước khả tích thiếu (L) | đã sửa: $L_D(w_{T+1})\le L_D(w_1)+G^2\sum_t\eta_t$, tương tự cho $\bar w_T$ |
| HV11 | 3-04 | "tổng $6$" không nói tổng gì | đã sửa: "tổng $\Delta_3$ trên nhóm …" |
| HV12 | 4-03 | mốc $1$ không có nghĩa | đã sửa: "lớn hơn mọi khoảng cách đo được ở bảng mở đầu" (đề xuất sửa ghi chú dòng 550 đã có ở review-log) |
| HV13 | 6-03 | thiếu nhân $G=1$; $c$ chưa nêu | đã sửa: "nhân $G$: cận hiệu hàm lỗi $\gg2$"; "$c>0$" |
| HV14 | 7-05 | "giả thiết tối ưu" chưa định nghĩa | đã sửa: "Tính lồi, tính trơn và (G) không thỏa" |
| HV15 | 7-06 | ý "$0{,}4$ chỉ khi $G\le1$" chỉ ở ghi chú; dòng đề dài | đã sửa: "bằng $0{,}4$ chỉ khi $G\le1$; với $G=1{,}5$ là $0{,}9$"; dòng đề theo câu của `exercises.md` (xem SP6) |
| HV16 | 7-07 | câu 3 thiếu bất đẳng thức tổng | đã sửa: "(dùng $\sum_tt^{-1/2}\le2\sqrt T-1$)" |
| HV17 | 7-04 | $J$ không nhắc lại | đã sửa: "Mạng ReLU hai lớp" |
| HV18 | 7-09 | thiếu nhãn thảo luận | đã sửa: "Phụ lục A; thảo luận: §1, §5" |
| HV19 | 3-01, 7-03, 2-02, 2-06, 2-07 | dấu câu mồ côi | đã sửa ở 3-01 (đổi thứ tự giả thiết, dấu chấm trong KaTeX), 7-03 (viết lại), 2-02 (dấu chấm trong KaTeX); 2-06, 2-07 ở 390 px: không sửa (ngắt dòng của KaTeX ở màn hẹp, không mất chữ) |
| HV20 | 2-08 | "(b)" một mình trên công thức | đã sửa: công thức (b) trong dòng |
| HV21 | 2-06, 4-04, 5-03, 6-01 | chữ SVG nhỏ ở 390 px | không sửa: không bắt buộc theo báo cáo; số dùng đều có trên mặt trang |
| HV22 | 7-01, 7-02 | bảng cuộn ngang ở 390 px | không sửa: đúng quy định (cuộn tại chỗ, có nhãn) |
| CG1 (ng.tr.) | 7-03, 6-06 | mạng ReLU cũng không thỏa (S′) | đã sửa: 7-03 "không thỏa (S), (S′), (G): Định lý 08.6, Mệnh đề 08.10, Nhận xét 08.11 không áp dụng"; 6-00 dòng dẫn "(S), (S′)"; 6-06 "không khả vi …: không $\beta$-trơn" |
| CG2 | 4-00 | "tăng không nhanh hơn"; thiếu (G), điều kiện bước | đã sửa: dòng dẫn mới có (T1), (T2), (S), (G), $\eta_t\le2/\beta$, "không vượt $2G^2/m$ nhân ngân sách" |
| CG3 | 4-01/7-03 | ba đặc điểm (thuật toán, kì vọng, không phụ thuộc $p$) | đã sửa: dòng dưới bảng 7-01 "Mọi bảo đảm theo kì vọng, cho một thuật toán, không phụ thuộc $p$; không có cận với xác suất cao"; 7-03 "không qua số tham số"; so với Hệ quả 07.16 ở ghi chú diễn giả 7-03 |
| CG4 | 2-01/2-03 | lý do cần ổn định cho nhiều vòng | đã sửa: 2-03 "Nhiều vòng: mỗi hồ sơ dùng lại, nên Hệ quả 06.2 không áp dụng" (2-01 ở trần 60); $T/m$ và điểm lặp phụ thuộc quan sát sắp dùng ở ghi chú diễn giả 2-03 |
| CG5 | 7-03 | "cận tăng theo hàm mũ" thiếu "bước hằng" | đã sửa: dòng bỏ khỏi 7-03 (trần 60, thêm (S′) và phỏng đoán); khẳng định có điều kiện ở 6-03 (bước hằng; $\eta_t=c/t$ cho đa thức) và ghi chú diễn giả 7-03, 1-05 |
| CG6 | 6-06 | (G) thiếu "khi trọng số không bị chặn" | đã sửa: "không có $G$ đều trên toàn không gian tham số" (theo quyết định) |
| CG7 | 5-01 | điều kiện $\eta^*$ | đã sửa (như HV5) |
| CG8 | 5-04 | "ngân sách thay $1/\lambda$" mạnh hơn ghi chú; chính quy hóa ngầm mất điều kiện; phỏng đoán | đã sửa: định nghĩa đủ điều kiện ("nhiều điểm có $L_s$ nhỏ như nhau, khởi tạo, độ dài bước quyết định điểm trả về, không qua số hạng phạt"); so sánh hai hệ số "cùng dạng, ngân sách ở vị trí của $1/\lambda$" chuyển vào ghi chú diễn giả; "chính quy hóa ngầm là phỏng đoán thực nghiệm" ở 7-03 |
| CG9 | 6-06 | "trọng số ra khác 0" | đã sửa theo câu ngắn của người duyệt toán học (quyết định) |
| CG10 | 6-06 | "Kết luận:" thiếu điều kiện | đã sửa: dòng chuyển; điều kiện đủ ở 7-06 và ghi chú diễn giả 6-06 |
| CG11 | 7-00 | dòng dẫn thiếu cỡ mẫu | đã sửa: dòng dẫn mới (tính lồi, tính trơn, (G), điều kiện bước đều có phản ví dụ; mạng ReLU nằm ngoài các kết quả), không còn câu về ngân sách (MT M4) |
| CG12 | 2-01 | $T$ chọn trước | đã sửa: "$T$, $\eta_t>0$ tất định, chọn trước" |
| CG13 | 2-09 | tên "bổ đề hạ", descent lemma | đã sửa |
| CG14 | 6-01 | "Bổ đề 08.4 hỏng" | đã sửa: "bước chung làm $\Delta$ tăng, trái kết luận của Bổ đề 08.4" |
| CG15 | 4-01 | "Trực quan." chỉ đọc tuyến tính | đã sửa: trường hợp cực biên $\eta_t\to0$ và cơ chế "mỗi bước khác biệt thêm không quá $2G\eta_t$" |
| TH1, TH2 | 6-06 | điều kiện khả vi; (G) | đã sửa (như CG9, CG6) |
| TH3 | 5-00, 1-05 | "nhỏ nhất ở số bước hữu hạn" cần bước cố định | đã sửa cả hai |
| TH4 | 5-04 | chính quy hóa ngầm mất điều kiện | đã sửa (như CG8) |
| TH5 | 1-05 (ghi chú) | "nhỏ hơn một nửa" thiếu bước hằng | đã sửa |
| TH6 | 5-01 | "nếu" | đã sửa |
| TH7 | 4-00 | dòng dẫn | đã sửa (như CG2) |
| TH8 | 4-03 (ghi chú) | đạo hàm theo lề | đã sửa |
| TH9 | 4-04 (ghi chú) | $2{,}99$ là hai lần chạy trên cùng $S$ | đã sửa |
| TH10 | 6-06 | "Kết luận:" thiếu điều kiện | đã sửa (như CG10) |
| TH11 | 6-04 | $g_t$ đổi nghĩa | đã sửa (như HV3) |
| TH12 | 4-07 | thiếu $w_1=0$ | đã sửa |
| TH13 | 7-03 | dòng không lồi không nêu đại lượng | đã sửa (như CG5) |
| TH14 | 2-02 | (T3) thiếu lượng từ theo $w$ | đã sửa: "với mọi $w\in\mathbb R^p$" |
| TH15 | 2-07 | thiếu "khi $u\ne v$" | đã sửa |
| TH16 | 1-02 | thiếu "kì vọng hữu hạn" | đã sửa: "hai kì vọng hữu hạn và" |
| TH17 | 2-09 (ghi chú) | "bốn dòng" | đã sửa: "bốn bước" |
| TH18 | 2-09 | descent lemma | đã sửa |
| SP1 | 1-02, 1-06, 2-01, 2-02, 2-09, 6-06, 7-03 | tên tiếng Anh | đã sửa: uniform stability, neighboring samples (1-02); logistic regression, stochastic gradient descent, epoch (1-06); averaged iterate, expected generalization gap (2-01); logistic loss (2-02); descent lemma (2-09); hinge loss, rectified linear unit (6-06); "phỏng đoán thực nghiệm (conjecture)" (7-03). "còn gọi là tốc độ học" ở ghi chú diễn giả 1-06 (trần 60) |
| SP2 | 4-04 | "khoảng cách" hai nghĩa | đã sửa: "khoảng cách tổng quát hóa (kì vọng)" ở dòng 2, "Diễn giải:", chú thích |
| SP3 | 4-00 | dòng dẫn; từ khóa | đã sửa: dòng dẫn (như CG2); từ khóa "ghép cặp trong thí nghiệm mở đầu" |
| SP4 | 5-01 | "nếu" | đã sửa |
| SP5 | 5-04 | chủ thể trừu tượng; điều kiện | đã sửa (như CG8) |
| SP6 | 4-07, 7-06 | đề rút thành mảnh câu | đã sửa: 4-07 "Tìm $T$ lớn nhất để cận của Hệ quả 08.7 không vượt …; làm tương tự với Định lý 08.6 cho $w_{T+1}$"; 7-06 "Nêu cách sửa thiết lập để có cận ổn định, và cái giá: cố định lớp ẩn trước khi thấy mẫu, chỉ huấn luyện lớp ra như mạng của Ví dụ 07.3"; bỏ câu "Đề đầy đủ …" khỏi ghi chú |
| SP7 | 7-08 (ghi chú) | câu quy trình, câu nguồn gốc | đã sửa: bỏ hai câu |
| SP8 | 2-05 | đối tượng không gọi tên | đã sửa (như HV1) |
| SP9 | 3-00 | "một phần cỡ mẫu" | đã sửa: "xác suất $1/m$", từ khóa "thừa số $1/m$" |
| SP10 | 1-02 | dùng trước định nghĩa | đã sửa (như HV2) |
| SP11 | 1-02 (ghi chú) | câu ôn nhanh chỉ đáp số | đã sửa: viết thành câu khẳng định |
| SP12 | 2-07 | thứ tự dòng | đã sửa |
| SP13 | 1-06 (ghi chú) | "chỉ số bước" | đã sửa: "chỉ có số bước thay đổi" |
| SP14 | 1-06, 4-04 | "trung bình 20 hạt giống" | đã sửa: 1-06 "trung bình $20$ lần chạy (hạt giống ngẫu nhiên, random seed)"; 4-04 bỏ khỏi chú thích (đã ở 1-06) |
| SP15 | 1-03 | mục tiêu 4 mơ hồ; ghi chú máy móc | đã sửa: "Ghép cận ổn định với cận tối ưu để chọn số bước, độ dài bước"; ghi chú viết lại (giữ $80/80$: rút mục tiêu 3, 5) |
| SP16 | 2-09 | "đổi vai" trùng tên kỹ thuật | đã sửa: "hoán đổi $u$, $v$" (mặt trang, ghi chú) |
| SP17 | 3-01 (ghi chú) | câu Huber khó theo | đã sửa |
| SP18 | 4-01 | "Trực quan." | đã sửa (như CG15) |
| SP19 | 5-01 | "Trực quan." lặp dòng dẫn | đã sửa: "Tối ưu: $\sim1/T$; ổn định: $\sim T/m$" |
| SP20 | 5-02 | dòng cuối không rõ đối tượng | đã sửa: "Định lý 05.14 chặn sai số tối ưu của $\bar w_T$, không của $w_{T+1}$" |
| SP21 | 6-01 | "Bổ đề hỏng"; "nhân khoảng 1,1" | đã sửa (như CG14); "bước chung nhân $\Delta$ với khoảng $1{,}1$" |
| SP22 | 6-03 | dòng $275{,}6$ khó theo | đã sửa (như HV13); số của Ví dụ 08.8 ghi ở ghi chú diễn giả |
| SP23 | 6-06 | tên hàm lỗi cụt; "được" | đã sửa: $\ell=\lvert w-z\rvert$, "hàm lỗi bản lề (hinge loss)"; câu theo người duyệt toán học |
| SP24 | 7-03 | "tác động này"; "phỏng đoán thực nghiệm"; hai dấu hai chấm | đã sửa: viết lại 7-03 (ba dòng, mỗi dòng một chủ ngữ rõ) |
| SP25 | 7-04 | "Báo cáo:" như nhãn | đã sửa: "Một báo cáo viết:" |
| SP26 | 7-05 | "giả thiết tối ưu" | đã sửa (như HV14) |
| SP27 | 6-00 | "định lý" không nói định lý nào | đã sửa: "(S), (S′)" thay cho "giả thiết của định lý" |
| SP28 | 2-02 | bỏ (T3) khỏi mặt trang; ghi chú | không sửa phần bỏ (T3): quyết định của điều phối viên giữ (T3) cho dòng Nhận xét 08.11 ở 6-03; ghi chú diễn giả đã viết lại câu "quan sát kiểm tra cần điều này" |
| SP29 | 2-03, 2-11 (ghi chú) | câu nói về ghi chú/đề bài | đã sửa: 2-03 "Câu hỏi còn một vế …"; 2-11 mặt trang theo lời đề, bỏ câu ở ghi chú |
| SP30 | ghi chú các trang chứng minh; 4-01, 5-01 | khuôn mở lặp; câu nhắc Thuật toán 08.1 lặp | đã sửa: đổi câu mở ở 3-02, 4-02, 4-06, 5-02, 6-03, 2-09; bỏ câu nhắc Thuật toán 08.1 và câu đầu ở 4-01, 5-01 |
| MT M1 | 7-02, 6-03 | Nhận xét 08.11 không có trên mặt trang | đã sửa: một dòng trên 6-03 ((T3), $\eta_t\le c/t$ không tăng, $W=\mathbb R^p$; $\beta=10$, $c=G=1$, $m=10^4$, $T=10^6$: $\epsilon_{\mathrm{stab}}\le33{,}37>1$) |
| MT M2 | 1-05 (ghi chú) | câu hỏi Bài 07 trao lại | đã sửa |
| MT M3 | 2-06, 2-07 | câu nối một dãy → mọi dãy | đã sửa ở 2-06 ("Đây là một dãy chỉ số; Định nghĩa 06.9 cần hai sự kiện trên với mọi dãy"); "Câu hỏi:" trên 2-07 không thêm (báo cáo ghi "có thể"; trần 60) |
| MT M4 | 4-00, 7-00 | dòng dẫn trùng khuôn, thiếu điều kiện | đã sửa: hai dòng dẫn khác ý, đủ điều kiện |
| MT M5 | 6-04 | $g_t$ | đã sửa (như HV3) |
| MT N1 | 6-04 | câu nối tính dừng | đã sửa: "tính dừng yếu hơn sai số tối ưu" |
| MT N2 | 3-00, 5-00 | từ khóa không có trên mặt trang | đã sửa: "thừa số $1/m$" (3-00, có ở 3-01 "Trực quan."); "cận ghép" trên 5-03 "Diễn giải:" |
| MT N3 | 2-09 | "đổi vai" | đã sửa (như SP16) |
| MT N4 | 2-00 (ghi chú) | mạch mở bằng thiết lập | đã sửa |
| MT N5 | 5-01 | lý do mạch 5 | đã sửa một phần: "Nhắc lại:" nêu $\operatorname{opt}_S$ và Mệnh đề 06.5(b); câu "Định lý 08.6 không chặn rủi ro kì vọng" ở ghi chú diễn giả 5-01 (chỗ trên mặt trang dành cho điều kiện "nếu" của (b)) |
| MT N6 | 4-04, 1-06, 6-02 | "khoảng cách" hai nghĩa | đã sửa ở 4-04, 6-02 ("nhân $\Delta$"), 6-01; 1-06 giữ "khoảng cách" theo cột bảng và câu hỏi của ghi chú |
| MT N7 | 7-03 | "không qua số tham số" | đã sửa |
| MT N8 | 7-01 | "như trên" kéo theo "ghép cặp"; thiếu $\xi$ độc lập | đã sửa |
| MT N9 | 4-05 (ghi chú) | lộ đáp số Bài tập 08.7 | đã sửa |
| MT N10 | 1-04 | dòng nguồn | đã sửa |
| MT N11 | storyboard | số trang cũ ở §3, §4, §6, §12 | đã sửa: §3 dòng dẫn và từ khóa mới, §4 hàng Hệ quả 08.7, §6 tiêu đề ID mới (có ghi chú đầu mục), §12 hàng 4-06, 4-07, 7-01–7-09; §15 ghi là số của bản lập |
| MT M7 | 2-01 (ghi chú) | dòng nguồn §4 | đã sửa: "§1; §4, Thuật toán 08.1 …" |

**Lệch khác so với mục 16.** 1-06 tiêu đề "Ví dụ: khoảng cách tổng quát hóa theo số vòng" (tiêu đề một dòng, chân trang); 5-03 bỏ "(Nhận xét 06.3)" khỏi mặt trang (ở ghi chú diễn giả) và rút chú thích hình; 6-03 tiêu đề "Ý tưởng chứng minh: truy hồi khi bỏ tính lồi"; 6-04 bảo đảm viết trong dòng; 7-02 bỏ dòng "Bỏ tính lồi …" (chạm chân trang; nội dung ở 6-03 và ghi chú 7-03).

**Mật độ từng trang sau khi sửa** (trang: âm tiết/dòng/ghi chú diễn giả): 1-01 bìa (luận điểm 60)/3/126; 1-02 60/5/129; 1-03 80/5/101; 1-04 46/7/97; 1-05 17/1/149; 1-06 57/6/137; 2-00 24/–/104; 2-01 60/5/90; 2-02 46/5/124; 2-03 58/6/132; 2-04 60/5/102; 2-05 60/6/121; 2-06 47/4/79; 2-07 47/6/90; 2-08 46/5/88; 2-09 58/5/148; 2-10 41/5/96; 2-11 57/6/74; 3-00 20/–/65; 3-01 48/5/115; 3-02 50/5/153; 3-03 45/6/67; 3-04 60/6/108; 4-00 20/–/74; 4-01 57/5/117; 4-02 49/5/180; 4-03 60/5/83; 4-04 59/3/137; 4-05 49/5/77; 4-06 49/5/88; 4-07 59/6/124; 5-00 25/–/99; 5-01 48/5/150; 5-02 59/6/146; 5-03 34/4/102; 5-04 58/4/125; 5-05 47/5/99; 6-00 24/–/94; 6-01 39/3/106; 6-02 44/5/88; 6-03 50/5/140; 6-04 58/5/107; 6-05 41/6/59; 6-06 60/4/128; 6-07 44/5/95; 7-00 25/–/102; 7-01 77/2/125; 7-02 64/2/118; 7-03 60/3/148; 7-04 59/4/136; 7-05 43/3/123; 7-06 57/4/121; 7-07 49/4/127; 7-08 33/2/107; 7-09 52/3/140.

### Lượt 2 (theo `reviews/deck-kiem-lai-1.md`)

| Phát hiện | Trang | Kết quả |
|---|---|---|
| T1 | 5-01 | đã sửa: "nếu $\eta^*\le2/\beta$, vế phải (a) tại $\eta=\eta^*$ không vượt $RG\sqrt{3/m}$ khi $T=m$, $\to RG\sqrt{2/m}$ khi $T\to\infty$"; cắt bù và chân trang: "Nhắc lại:" viết $\operatorname{opt}_S(w)=\ldots$ (sai số tối ưu thực nghiệm), $\tilde w=A(S;\xi)$, công thức Mệnh đề 06.5(b) gọn; giả thiết "$\eta\in(0,2/\beta]$ hằng"; (a) viết $\mathbb EL_D(\bar w_T)$ (loại kì vọng ghi ở "kì vọng theo $(S,\xi)$") |
| N2 | 4-01 | đã sửa: "hiệu hàm lỗi tại mọi $z$ không quá $G\Delta_{T+1}$" |
| T2 | 5-04 | đã sửa: "khi nhiều điểm có $L_s$ nhỏ như nhau, khởi tạo, độ dài bước, số bước và cách rút chỉ số quyết định điểm trả về, không qua số hạng phạt"; cắt bù: "$\operatorname{opt}_s\approx0$", "phạt $\tfrac\lambda2\lVert w\rVert^2$", "mẫu xác thực" (chữ "độc lập" ở ghi chú diễn giả); 60/60 |
| N1 | 2-06 | đã sửa: "… $=2$ trên một dãy chỉ số; Định nghĩa 06.9 lấy kì vọng theo $\xi$, nên cần hai sự kiện trên với mọi dãy"; chú thích hình rút để không chạm chân trang |
| N3 | 2-03 | đã sửa: "hồ sơ được dùng lại" |
| N4 | 7-01 | đã sửa: "Các cận ổn định theo kì vọng, …" |
| N6 | 7-04 | đã sửa: "(c) Lập bảng giả thiết của Định lý 08.6: …"; cắt bù: "quan sát theo (T1)", "mọi trọng số huấn luyện", "Báo cáo viết:" |
| N7 | 6-06 | đã sửa: "$0{,}99\mapsto1{,}49$; $1{,}01\mapsto1{,}01$" |
| N8 | 5-02, 1-06, 3-01, 5-03 | đã sửa: 5-02 đổi thứ tự câu ("không chặn … của $w_{T+1}$, chỉ của $\bar w_T$"); 1-06, 3-01, 5-03 dấu câu vào trong KaTeX |
| N9, N10, N11 | ghi chú 1-02, 4-07, 7-03 | đã sửa: cắt câu điều hướng (1-02), cắt câu lặp đề (4-07), thêm vế "Định lý 08.6 đúng theo kì vọng, cho một thuật toán" (7-03; câu khác trong ghi chú 7-03 rút để giữ ≤ 150) |

Kiểm máy lượt 2: `deck_lint.py` 0; `footer_check.py` 0; `deck_check.py --shots` các trang đổi: console 0, pageerrors 0, failed 0, không `.katex-error`; đã xem ảnh 1600×900 và 390×844 (cả `-end`) của 1-02, 1-06, 2-03, 2-06, 3-01, 4-01, 4-07, 5-01, 5-02, 5-03, 5-04, 6-06, 7-01, 7-03, 7-04; phím →, ↓, Space, Esc và `#/2`…`#/7` đúng. Mật độ sau lượt 2: 4-01 59, 5-01 49, 5-04 60, 7-04 58; trung vị 41 trang nội dung vẫn $50$ (21 trang $\le50$), lớn nhất $60$.

### Lượt 3 (theo `reviews/deck-kiem-lai-2.md`)

| Phát hiện | Trang | Kết quả |
|---|---|---|
| T3 | 5-04 | đã sửa: "mẫu xác thực độc lập"; bù: "không qua phạt"; 60/60 |
| N12 | 5-03 | đã sửa: dấu hai chấm trong KaTeX viết `{:}` ("$\eta^*\approx0{,}0289{:}\ \le0{,}0866$", "$T\to\infty{:}\ \le0{,}0708$") |
| N13 | 5-01 | đã sửa: $\mathbb E[L_D(\tilde w)-L_S(\tilde w)]$; để không chạm chân trang và giữ trung vị 50: "đầu ra $\tilde w$" trong dòng "Nhắc lại:", giả thiết viết "$\tilde w=\bar w_T$" (bỏ chữ "đầu ra" ở đó); 49 âm tiết |

Kiểm máy lượt 3: `deck_lint.py` 0; `footer_check.py` 0; `deck_check.py --ids L08-5-01,L08-5-03,L08-5-04 --shots`: console 0, pageerrors 0, failed 0, không `.katex-error`; đã xem ảnh 1600×900 và 390×844 (cả `-end`) của ba trang. Trung vị 41 trang nội dung $50$, lớn nhất $60$.
