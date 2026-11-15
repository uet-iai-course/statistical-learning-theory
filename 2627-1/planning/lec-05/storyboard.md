# Storyboard — Bộ trang chiếu Bài 05: Hạ gradient, hạ gradient ngẫu nhiên và cận tối ưu

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-11-15 bởi tác tử lập storyboard. Nguồn nội dung duy nhất: `materials/lec-05/lecture-note.md` (bản hiện hành); bài tập: `materials/lec-05/exercises.md`. Quy định: `CLAUDE.md` § Slide decks, `common-brief.md` (gồm "Các quy định dễ sót" và "Bài học từ năm báo cáo duyệt deck 01"), `brief-storyboard.md`, `../rl-plan/CLAUDE.md` § Deck structure and content, nhật ký yêu cầu 2026-11-13 hàng 1–5, quyết định của điều phối viên trong `lec-0{1,2,3,4}/review-log.md` § Bộ trang chiếu. Khuôn bố cục theo storyboard Bài 04. Mọi mã trang có dạng `L05-k-mm`; trong bảng viết gọn `k-mm`.

Số âm tiết trong tệp này đếm bằng script (mục 15) theo cách của `deck_check.py`, cộng thêm số viết ngoài KaTeX (quyết định Bài 01); điều phối viên đếm lại trên deck.

UML đã đọc để đối chiếu (không chép câu chữ): §14.1.1 trang PDF 186 (phân tích GD cho hàm lồi–Lipschitz, bất đẳng thức Jensen cho điểm lặp trung bình, so sánh với mọi $w^\star$); §14.3 trang PDF 192 (Định lý 14.8 của UML: cận $B\rho/\sqrt T$, gradient ngẫu nhiên bị chặn hầu chắc chắn, tính chất tháp theo $v_{1:t-1}$); §14.4.1–14.4.2 trang PDF 194 (bổ đề phép chiếu, bước chiếu giữ bổ đề một bước, độ dài bước $\eta_t\propto1/\sqrt t$). Các mục khác chỉ dẫn theo §14 của ghi chú và `sources/uml-sections.md` (§9.2 trang 123, §12.1 trang 156, §12.2 trang 163, §14.2 trang 188, §14.8 trang 201).

**Điểm toán học #3 còn mở** (`planning/diem-toan-can-doc-2026-11-13.md`, mục 3: câu kết luận của Ví dụ 05.12 lập luận theo $f(w_t)$ trong khi Định lý 05.14 chặn $f(\bar w_T)$). Deck không chép câu kết luận đó: trang 5-03 viết đại lượng được chặn là $f(\bar w_T)$, bằng $0$ khi $T$ chẵn, và $f(w_t)=0{,}1$ bằng số hạng $\eta G^2/2$ (đúng đề xuất của người kiểm).

## 1. Tên tệp và tiêu đề

- **Tệp deck:** `2627-1/lecture-05-ha-gradient-ngau-nhien.html` (slug ASCII từ tên bài).
- **Tiêu đề deck (h1 trang bìa):** "Hạ gradient, hạ gradient ngẫu nhiên và cận tối ưu" (đúng tên bài của ghi chú).
- **`<title>`:** "Bài 05: Hạ gradient ngẫu nhiên".
- **Chân trang:** "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài 05".
- **Liên kết viewer:** `material-viewer.html?doc=materials/lec-05/lecture-note.md&deck=lecture-05-ha-gradient-ngau-nhien.html` và `…exercises.md&deck=…`.
- **Màn hẹp:** chế độ đọc của `lecture-course.css` (`.slides` bọc trong `div.lecture-viewport`, script màn hẹp của `lecture-template.html`); bảng 3-05, 3-08, 6-05, 6-06, 7-02, 7-07 đặt trong `.table-scroll`.
- **Trang cuối deck Bài 04** (7-07 của storyboard Bài 04) nhận liên kết tới tệp này khi deck Bài 05 xong.

## 2. Khung lý thuyết chung

**Vấn đề trung tâm (hộp "Vấn đề trung tâm", bằng lời, ≤ 30 âm tiết).** "**Câu hỏi:** tối ưu ngẫu nhiên làm giảm một hàm mục tiêu nhanh đến mức nào theo số vòng lặp?" (câu hỏi trung tâm ở đoạn mở đầu của ghi chú, thêm "theo số vòng lặp" từ câu hỏi cầu nối của Bài 04; 20 âm tiết kể cả nhãn.)

**Luận điểm (trang bìa, hai câu, bằng lời).** "Sau mỗi bước hạ gradient ngẫu nhiên, bình phương khoảng cách tới một điểm so sánh tăng không quá một số hạng tỉ lệ với độ dài bước, có thể âm, cộng một số hạng tỉ lệ với bình phương độ dài bước. Với độ dài bước chọn theo số vòng lặp, cận của độ chênh tối ưu kì vọng tại trung bình các điểm lặp tỉ lệ nghịch với căn bậc hai của số vòng lặp." (bản sửa theo N1 của cổng duyệt; đoạn đầu §7, Định lý 05.14, Hệ quả 05.15; 52 âm tiết theo script; không kí hiệu, hai câu thay cho một câu có dấu chấm phẩy theo phát hiện L16 của cổng Bài 04.)

**Trọng tâm trực quan của deck.** Bất đẳng thức một bước: bình phương khoảng cách tới điểm so sánh $u$ giảm $2\eta\langle g,w-u\rangle$ và tăng $\eta^2\lVert g\rVert^2$, kể cả khi $g$ là gradient đúng (ghi chú, đoạn mở §7). Ý này đi qua sáu chỗ: 1-06 và 3-05 (một bước SGD làm $L_S$ tăng từ $0{,}0639$ với cả ba lựa chọn, bước GD làm giảm xuống $0{,}0614$; hình F3); 4-01, 4-02 (bước thứ hai của cùng ví dụ: không chiếu thì đẳng thức $1{,}3289$, có chiếu thì $1{,}3289<1{,}5019$); 4-03 đến 4-05 (tổng triệt tiêu: chỉ còn khoảng cách ban đầu, các số hạng $\tfrac\eta2\lVert g_t\rVert^2$ cộng dồn, bất đẳng thức lồi hữu hạn chuyển sang điểm lặp trung bình); 4-06 (vì sao $\eta\propto1/\sqrt T$: hai số hạng cân nhau; hình F4); 5-03 (điểm lặp cuối dao động ở đúng mức $\eta G^2/2$); 7-01 (cận chặn sai số tối ưu thực nghiệm, không chặn $L_D$: $0{,}0025$ so với $0{,}9025$).

**Đối tượng và kí hiệu chung** (ghi chú §1–§2, `ky-hieu.md` dòng 48–68, 75, 127):
- tham số $w\in\mathbb R^p$, tập tham số $W$ (khác rỗng, đóng, lồi), quả cầu bán kính $B$; hàm mục tiêu $F$, trường hợp chính $F=L_S$ với $S=(z_1,\ldots,z_m)$ cố định; $\ell(w,z)$, $L_S(w)$, $L_D(w)$; hàm điểm số $h_w(x)=\langle w,x\rangle$; $\tilde y=2y-1$; $C_x$, $C_y$;
- dưới gradient, dưới vi phân $\partial F(w)$; $G$-Lipschitz; phép chiếu $\operatorname{proj}_W$, $\theta$, $\pi$ (chỉ ở Bổ đề 05.8);
- nguồn ngẫu nhiên $\xi$, $\Xi$, $P_\xi$, $\xi_t$, $i_t$; ánh xạ oracle $\varphi(w,\xi)$, trung bình $\psi(w)$; lịch sử $\mathcal F_t$; $g_t$, $v(w)$, $v_t$;
- $\eta$ (không chỉ số; khác $\eta(x)$ của Bài 01), $T$, $w_t$, $\bar w_T$, $w_{T+1}$, $u$, $w^*$, $R$, $\Delta_t$ (chỉ trong chứng minh), $\eta^*$, $\gamma$ (Ví dụ 05.8);
- $\operatorname{opt}_s$, $\epsilon_{\mathrm{opt}}$, $\delta'$ (theo $\xi$, khác $\delta$ theo $S$), $A(S;\xi)$;
- lô nhỏ: $b$, $\varphi_b$, $\bar\xi$, $\sigma^2$ (khác $\sigma^2(x)$ của Bài 04), $G_F$, $G_b$, $e_j$;
- ví dụ xuyên suốt: hồi quy ba quan sát trong mặt phẳng (Ví dụ 05.1, 05.3, 05.5–05.8; Bài tập 05.3) và hồi quy logistic trên một triệu hồ sơ (Câu hỏi mở đầu, khối ứng dụng §3, Ví dụ 05.9, 05.14).

**Giả thiết** (ghi chú §2): (T1) lấy mẫu (chỉ dùng ở 6-01, 7-01); (C) $F$ lồi trên $\mathbb R^p$, $W$ khác rỗng, đóng, lồi; (G1) $\psi(w)\in\partial F(w)$ với mọi $w\in W$; (G2) $\mathbb E_\xi\lVert\varphi(w,\xi)\rVert^2\le G^2$ với mọi $w\in W$; thêm các lần rút độc lập (Định nghĩa 05.10, dòng 1 của Thuật toán 05.11).

**Chuỗi định nghĩa → kết quả → phương pháp.**
1. Một bước GD trên $L_S$ tốn $m$ gradient; một bước SGD tốn một nhưng có thể làm $L_S$ tăng (Câu hỏi mở đầu) → cần một bảo đảm cho cả quỹ đạo.
2. Tập lồi, hàm lồi, bất đẳng thức lồi hữu hạn (Định nghĩa 05.1) → dưới gradient (Định nghĩa 05.2), ba quy tắc tính (Mệnh đề 05.3, Ví dụ 05.2, 05.3) → Lipschitz và chuẩn của dưới gradient (Định nghĩa 05.4, Mệnh đề 05.5).
3. Phép chiếu Euclid (Định nghĩa 05.7, Ví dụ 05.4) → bất đẳng thức của phép chiếu (Bổ đề 05.8) → oracle (Định nghĩa 05.10, Ví dụ 05.5) → GD và SGD có chiếu (Thuật toán 05.9, 05.11, Ví dụ 05.6) → kì vọng có điều kiện theo lịch sử (Bổ đề 05.12).
4. Bất đẳng thức một bước (Mệnh đề 05.13, Ví dụ 05.7) → cận kì vọng (Định lý 05.14) → độ dài bước theo số vòng lặp (Hệ quả 05.15, Ví dụ 05.8) → GD (Hệ quả 05.16, Ví dụ 05.9).
5. Bỏ một giả thiết (Ví dụ 05.10, 05.11, 05.13) và điểm lặp cuối (Ví dụ 05.12).
6. Thuật toán học có nguồn ngẫu nhiên riêng (Định nghĩa 05.18) → SGD trên rủi ro thực nghiệm, kì vọng và xác suất cao (Hệ quả 05.19, Ví dụ 05.14) → lô nhỏ (Mệnh đề 05.20, Ví dụ 05.15, 05.16) → câu hỏi cuối buổi: $\operatorname{opt}_S$ nhỏ, $L_D$ lớn.

**Giới hạn áp dụng** (ghi chú §8, §9 cuối, §10 cuối, §11): mọi cận chặn độ chênh tối ưu của hàm mà oracle không chệch (với chỉ số rút từ $S$: $L_S$), không chặn $L_D$ hay tỉ lệ lỗi 0–1; chỉ chặn điểm lặp trung bình; cần (C), (G1), (G2) và các lần rút độc lập (cách xáo trộn lại sau mỗi vòng không thỏa Định nghĩa 05.10); bảo đảm với xác suất cao qua bất đẳng thức Markov tốn thừa số $1/\delta'^2$; so sánh GD, SGD, lô nhỏ là so sánh cận trên, không đo thời gian chạy; tính lồi là điều kiện của (G1) và của Bước 5, nên không chuyển sang mạng nơ-ron; Mệnh đề 04.3 không áp dụng trực tiếp cho hàm lỗi logistic hay bình phương. Nhận xét 05.17 (đọc thêm) và Mệnh đề 05.20 (đọc thêm) nói rõ mức đọc thêm ở ghi chú diễn giả. Phụ lục A, B chỉ vào ghi chú diễn giả; Phụ lục C cho số của Nhận xét 05.17; Phụ lục D cho $w^*$ và $\min_WL_S$.

## 3. Bảng mạch

Bảy mạch theo đúng thứ tự các mục của ghi chú; mỗi mạch ứng với các mục liên tiếp (mạch 6 thêm câu hỏi cuối buổi §13, đứng sau §12 nên thứ tự vẫn tăng). Bảng đối chiếu trang → khối ghi chú ở mục 12.

| N | Tên mạch | Mục ghi chú | Chức năng | Đầu vào | Đầu ra | `strand-lead` (âm tiết) | Từ khóa | Trang | Phút |
|---|---|---|---|---|---|---|---|---:|---:|
| 1 | Mở đầu | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết | Bìa, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, ví dụ một triệu hồ sơ và ba quan sát | Bài 04: $\operatorname{opt}_S$ đo bộ giải, chưa có cách tính nghiệm | Câu hỏi: SGD bảo đảm gì sau $T$ bước, khi một bước có thể làm $L_S$ tăng | (không có trang tiêu đề mạch) | — | 6 | 9 |
| 2 | Hàm lồi và dưới gradient | §1–§4 | Thiết lập, Ví dụ 05.1; Định nghĩa 05.1, 05.2; Mệnh đề 05.3, Ví dụ 05.3; Ví dụ 05.2; Định nghĩa 05.4, Mệnh đề 05.5; Bài tập 05.1(d) | cần một hướng đi khi hàm lỗi không khả vi | Dưới gradient của $L_S$ là trung bình dưới gradient của từng quan sát; chuẩn dưới gradient bị chặn bởi hằng số Lipschitz | "Với hàm lồi, thông tin tại một điểm cho một cận dưới trên toàn không gian." (15; L18) | hàm lồi · dưới gradient · dưới vi phân · hằng số Lipschitz | 8 | 22 |
| 3 | Phép chiếu và hạ gradient ngẫu nhiên | §5–§6 | Định nghĩa 05.7, Ví dụ 05.4 (hình F2); Bổ đề 05.8; Định nghĩa 05.10, Ví dụ 05.5; Thuật toán 05.9, 05.11; Ví dụ 05.6 (hình F3); Bổ đề 05.12; kỹ thuật lịch sử; Bài tập 05.3(b) | cận $G$ chỉ đúng trên tập bị chặn; gradient của $L_S$ tốn $m$ | Chiếu không làm tăng khoảng cách tới điểm của $W$; khi biết lịch sử, $g_t$ có trung bình là dưới gradient tại $w_t$ | "Chiếu không làm xa điểm nào của tập tham số; gradient một quan sát rút đều có trung bình là dưới gradient." (22; P5) | phép chiếu · oracle gradient ngẫu nhiên · điểm lặp trung bình · lịch sử | 9 | 22 |
| 4 | Bất đẳng thức một bước và cận kì vọng | §7 | Mệnh đề 05.13 và ý tưởng chứng minh (Ví dụ 05.7); Định lý 05.14 và ý tưởng chứng minh; kỹ thuật tổng triệt tiêu; trực quan độ dài bước (hình F4); Hệ quả 05.15 và ý tưởng chứng minh (Ví dụ 05.8); Hệ quả 05.16, Ví dụ 05.9; Bài tập 05.4(c) | hai bổ đề công cụ của mạch 3 | $\mathbb EF(\bar w_T)-F(u)\le RG/\sqrt T$; $10^4$ bước SGD cho hồi quy logistic | "Phép chiếu, kì vọng theo lịch sử và tính lồi ghép lại cho cận kì vọng tại điểm lặp trung bình." (22; P3) | bất đẳng thức một bước · tổng triệt tiêu · điểm lặp trung bình · độ dài bước | 11 | 30 |
| 5 | Vai trò của từng giả thiết | §8 | Ví dụ 05.10 (hình F5), 05.11, 05.13, 05.12; Bài tập 05.3(c) | ba giả thiết và năm bước của chứng minh | Mỗi giả thiết có một ví dụ một chiều làm kết luận sai; cận không nói về điểm lặp cuối | "Bỏ tính lồi, cận mô-men bậc hai hay tính không chệch, kết luận của cận sai trên một ví dụ một chiều." (22) | tính lồi · mô-men bậc hai · oracle chệch · điểm lặp cuối | 5 | 10 |
| 6 | Hạ gradient ngẫu nhiên trên rủi ro thực nghiệm và lô nhỏ | §9–§10 | Định nghĩa 05.18; Hệ quả 05.19 và ý tưởng chứng minh (Ví dụ 05.14); Mệnh đề 05.20 (đọc thêm); Ví dụ 05.15; Bài tập 05.5(b) | cận kì vọng cho một $F$ bất kì | $\operatorname{opt}_s$ theo kì vọng và với xác suất $1-\delta'$; giá $1/\delta'^2$; lô chỉ chia phần phương sai | "Với hàm lỗi lồi và đủ số bước, SGD có sai số tối ưu thực nghiệm nhỏ theo kì vọng hoặc với xác suất cao." (25) | nguồn ngẫu nhiên riêng · sai số tối ưu thực nghiệm · xác suất cao · lô nhỏ | 7 | 15 |
| 7 | Tổng kết | §11–§14 | Câu hỏi cuối buổi §13 (ví dụ $\operatorname{opt}_S$ nhỏ, $L_D$ lớn), bảng kết quả, trả lời vấn đề trung tâm, bài tập tổng hợp (Bài tập 05.5(d)), tự kiểm tra, bài tập về nhà, tài liệu | mọi kết quả | Cầu nối sang Bài 06 | "Bất đẳng thức một bước, tổng triệt tiêu và điểm lặp trung bình cho mọi cận của bài." (19) | — | 9 | 12 |
| | **Tổng** | | | | | | | **55** | **120** |

Số trang (55) vượt mục tiêu 45–52 ba trang, đúng trần 55. Lý do: bốn kết quả chính có trang phát biểu và trang "Ý tưởng chứng minh" riêng (Mệnh đề 05.13, Định lý 05.14, Hệ quả 05.15, 05.19: 8 trang); hai kỹ thuật dùng lại ở Bài 07, 08, 10 có trang "Kỹ thuật." riêng (3-07, 4-05); năm trang bài tập giữa cụm (mạch 2–6) và một bài tập tổng hợp hai trang (câu chữ của Bài tập 05.5(d) đã chiếm khoảng 60 âm tiết); ba phản ví dụ bỏ giả thiết mà ghi chú §11 liệt kê, cộng ví dụ điểm lặp cuối (mục tiêu 5). Đã gộp để giữ 55: thiết lập §1 và Ví dụ 05.1 chung trang 2-01; khối ứng dụng §3 vào trang dẫn nhập 1-06 (cùng nội dung với Câu hỏi mở đầu); Ví dụ 05.3 thành dòng "Ví dụ." trên 2-04; Định nghĩa 05.7 và Ví dụ 05.4 chung trang 3-01; Ví dụ 05.5 chia giữa dòng "Ví dụ 05.5." trên 3-03 ((G1)) và dòng đầu của 3-05 ((G2), $G=4$); Thuật toán 05.9 và 05.11 chung trang 3-04; Ví dụ 05.7 vào trang ý tưởng chứng minh 4-02; Ví dụ 05.8 chia giữa 4-06 (Bước 3) và 4-08 (Bước 1–2); Hệ quả 05.16 và Ví dụ 05.9 chung trang 4-09; Ví dụ 05.12 và 05.13 chung trang 5-03 (hai thẻ); Ví dụ 05.14 vào trang ý tưởng chứng minh 6-03; Ví dụ 05.16 vào ghi chú diễn giả 6-04; Định nghĩa 05.6, Nhận xét 05.17 (đọc thêm), Phụ lục A–C ở ghi chú diễn giả. Phương án rút còn 53 ở mục 11, điểm 2.

## 4. Bảng kết quả chính

Số hiệu theo ghi chú. Ánh xạ blueprint → ghi chú (theo `outline.md` §2): Lemma 5.1 → Bổ đề 05.8; Prop 5.2 → Mệnh đề 05.13; Theorem 5.3 → Định lý 05.14; Corollary 5.4 → Hệ quả 05.15; Prop 5.5 [O] → Mệnh đề 05.20. Mệnh đề 05.3, 05.5, Bổ đề 05.12, Hệ quả 05.16, 05.19 là kết quả của học phần. Mọi phát biểu rút gọn trên trang dùng "Giả thiết:" và "Bảo đảm:", giữ đủ giả thiết, lượng từ, hằng số và loại bảo đảm của ghi chú.

| Kết quả | Loại bảo đảm | (a) Trực quan | (b) Ý tưởng chứng minh | (c) Kỹ thuật | (d) Ví dụ bổ trợ | Trang |
|---|---|---|---|---|---|---|
| **Mệnh đề 05.13** (bất đẳng thức một bước; chứng minh đầy đủ) | tất định, không dùng tính lồi của $F$ hay xác suất; dấu bằng khi $W=\mathbb R^p$ | Khai triển $\lVert w-\eta g-u\rVert^2$: số hạng $-2\eta\langle g,w-u\rangle$ kéo về phía $u$, số hạng $\eta^2\lVert g\rVert^2$ có mặt cả khi $g$ là gradient đúng; phép chiếu chỉ làm khoảng cách nhỏ thêm. | Hai bước: Bổ đề 05.8(b) với $\theta=w-\eta g$ (chỗ duy nhất dùng phép chiếu, tính lồi, tính đóng của $W$ và $u\in W$); khai triển $\lVert a-a'\rVert^2$, chuyển vế, chia $2\eta$. Bỏ $u\in W$ hoặc tính lồi của $W$: Bước 1 hỏng (Bài tập 05.2(b), ghi chú diễn giả). | Khai triển $\lVert a-a'\rVert^2$ (Kiến thức tiên quyết, nhắc lại ở 1-02); dùng Bổ đề 05.8(b). | Ví dụ 05.7 ($1{,}3289$; $1{,}5019$; không chiếu: đẳng thức). | 4-01, 4-02 |
| **Định lý 05.14** (cận kì vọng cho SGD có chiếu; chứng minh đầy đủ) | kì vọng theo $\xi_1,\ldots,\xi_{T-1}$; mọi $u\in W$ tất định; độ chênh tối ưu của $F$ (hàm mà oracle không chệch) tại $\bar w_T$; phụ thuộc $p$, $m$ chỉ qua $G$, $\lVert w_1-u\rVert$; số hạng $1/T$ và số hạng $\eta G^2/2$ không giảm theo $T$ | Cộng $T$ bất đẳng thức một bước: khoảng cách triệt tiêu, chỉ còn $\lVert w_1-u\rVert^2$; mỗi bước góp $\tfrac\eta2\lVert g_t\rVert^2$; trung bình các $F(w_t)$ chặn $F(\bar w_T)$. | Năm bước: Mệnh đề 05.13 trên từng quỹ đạo ($W$ đóng, lồi, $u\in W$); tổng triệt tiêu, bỏ $-\Delta_{T+1}\le0$; Bổ đề 05.12(c) và bất đẳng thức dưới gradient ((G1)); $\mathbb E\lVert g_t\rVert^2\le G^2$ ((G2)); bất đẳng thức lồi hữu hạn ((C) cho $F$ và $W$). Bỏ (C): Ví dụ 05.10; bỏ (G2): Ví dụ 05.11; bỏ (G1): Ví dụ 05.13; bỏ độc lập: Bài tập 05.3(c). | **Tổng triệt tiêu và trung bình các điểm lặp** (lần đầu, trang riêng 4-05; dùng lại ở Bài 07, 08, 10). **Kì vọng có điều kiện theo lịch sử** (lần đầu, trang riêng 3-07; dùng lại ở Bài 07, 08, 10). | Ví dụ 05.6 (một bước làm $L_S$ tăng); Ví dụ 05.8 Bước 4 ($\eta=0{,}5$: $4{,}000625$, không cho thông tin); Ví dụ 05.10–05.13 (mạch 5). | 4-03, 4-04, 4-05; mạch 5 |
| **Hệ quả 05.15** (độ dài bước theo số vòng lặp; chứng minh đầy đủ) | kì vọng theo $\xi$; (a) mọi $u$ với $\lVert w_1-u\rVert\le R$; (b) so với $F_R$; (c) $T\ge R^2G^2/\epsilon^2$; $T$ cố định trước vì $\eta$ phụ thuộc $T$ | $\eta$ nhỏ: số hạng $R^2/(2\eta T)$ lớn; $\eta$ lớn: số hạng $\eta G^2/2$ lớn; tổng nhỏ nhất khi hai số hạng bằng nhau. Hình F4. | Ba bước: thay $\eta$ (mỗi số hạng bằng $RG/(2\sqrt T)$); vế phải không phụ thuộc $u$, lấy cận trên đúng theo $u$; giải $RG/\sqrt T\le\epsilon$. | Dòng "Kỹ thuật." trên 4-08: cân hai số hạng, $a/\eta+b\eta\ge2\sqrt{ab}$ (Bài tập 05.4(a)); chỉ dùng ở đây. | Ví dụ 05.8 ($400$; $1600$; $6400$; $\eta=0{,}00625$; $0{,}16112$; thừa số $1{,}25$ và $5{,}05$); Bài tập 05.4(c) ($0{,}0625$; $0{,}25$). | 4-06, 4-07, 4-08, 4-10 |
| **Hệ quả 05.16** (cận cho GD có chiếu; chứng minh đầy đủ) | tất định; cùng cận $RG/\sqrt T$ | GD là oracle tất định: không cần kì vọng. | Một dòng ở ghi chú diễn giả 4-09: Bước 1, 2, 5 của Định lý 05.14 trên quỹ đạo duy nhất; Bước 3, 4 thay bằng bất đẳng thức dưới gradient và $\lVert v_t\rVert\le G$. Kết quả phụ, không có trang ý tưởng chứng minh riêng (mục 11, điểm 3). | — | Ví dụ 05.9 ($G=1$, $R=5$, $T=10^4$, $\eta=0{,}05$, $10^{10}$ so với $10^4$ gradient). | 4-09 |
| **Hệ quả 05.19** (SGD trên rủi ro thực nghiệm; chứng minh đầy đủ) | (a) kì vọng theo $\xi$, mọi tập huấn luyện $s$; (b) xác suất $\ge1-\delta'$ theo $\xi$ khi $T\ge R^2G^2/(\delta'^2\epsilon_{\mathrm{opt}}^2)$; đại lượng: $\operatorname{opt}_s(\bar w_T)$ | Rút đều có hoàn lại làm oracle không chệch cho $L_s$; $\operatorname{opt}_s\ge0$ nên bất đẳng thức Markov đổi kì vọng thành xác suất, với giá $1/\delta'$ trong cận, $1/\delta'^2$ trong $T$. | Ba bước: (G1), (G2) cho $L_s$ qua Mệnh đề 05.3(b); Hệ quả 05.15(b) với $R\ge\sup_u\lVert w_1-u\rVert$; Markov (Bổ đề 02.2) cho $\operatorname{opt}_s\ge0$. Cần $W$ bị chặn (để $F_R=\inf_WL_s$). | Nhắc lại bất đẳng thức Markov (Bài 02) ở 1-02. | Ví dụ 05.14 ($640\,000$, $400$ lần; $4\,000\,000$ bằng bốn bước GD); câu hỏi cuối buổi (7-01); Bài tập 05.5(d) (7-04, 7-05). | 6-02, 6-03, 7-01 |
| **Mệnh đề 05.20** (gradient lô nhỏ; đọc thêm) | kì vọng theo $\bar\xi$, mọi $w\in W$; $G_b^2=G_F^2+\sigma^2/b$ | Chỉ phần phương sai chia cho $b$; phần $G_F^2$ là độ lớn gradient thật. | Ghi chú diễn giả 6-04 nêu lộ trình (tuyến tính của kì vọng; số hạng chéo bằng $0$ khi các $e_j$ không tương quan; đẳng thức sau Định nghĩa 05.10). Mức đọc thêm: không có trang ý tưởng chứng minh riêng. | Dòng "Kỹ thuật." trên 6-04: số hạng chéo bằng $0$ cho véc-tơ không tương quan. | Ví dụ 05.15 (bảng); Ví dụ 05.16 (bản sao: phương sai vẫn $\sigma^2$, ghi chú diễn giả); Bài tập 05.5(b) ($b=30$; $150$). | 6-04, 6-05, 6-06 |

**Kết quả phụ và quyết định.**
- Định nghĩa 05.1 và bất đẳng thức lồi hữu hạn: trang 2-02; các ví dụ tập, hàm lồi và không lồi ở ghi chú diễn giả, $(w^2-1)^2$ trên hình F1.
- Định nghĩa 05.2: trang 2-03 với hình F1 ($\lvert w\rvert$ và $(w^2-1)^2$).
- Mệnh đề 05.3 (công cụ tính; chứng minh đầy đủ): phát biểu trên 2-04; lộ trình chứng minh (đoạn thẳng ngắn dần cho (a); cộng bất đẳng thức dưới gradient cho (b); cực đại cho (c)) ở ghi chú diễn giả, không có trang ý tưởng chứng minh (mục 11, điểm 3).
- Mệnh đề 05.5 (chứng minh đầy đủ): phát biểu trên 2-06; lộ trình (Cauchy–Schwarz cho (a), thử theo hướng $v$ cho (b), tính mở dùng ở (b)) ở ghi chú diễn giả.
- Định nghĩa 05.6 (trơn, lồi mạnh): ghi chú diễn giả 2-06 (Bài 06, 08 dẫn; Bài tập 05.8(c), 05.12 dùng); không trên mặt trang vì mật độ (mục 11, điểm 4).
- Bổ đề 05.8 (công cụ; phác thảo): phát biểu và dòng "Trực quan." trên 3-02; lộ trình phác thảo và Phụ lục A ở ghi chú diễn giả 3-02; không có trang ý tưởng chứng minh riêng (mục 11, điểm 3).
- Bổ đề 05.12 (công cụ; phác thảo): phát biểu trên 3-06; cơ chế chứng minh là trang kỹ thuật 3-07 (cùng khuôn với Bổ đề 02.5 trên trang kỹ thuật của deck Bài 02); Phụ lục B (bổ đề đóng băng) ở ghi chú diễn giả 3-07.
- Nhận xét 05.17 (đọc thêm): ghi chú diễn giả 4-08 ($0{,}2281$ so với $0{,}1$, thừa số $\ln T$).
- Định nghĩa 05.18: trang 6-01.
- Cách xáo trộn lại sau mỗi vòng (không thỏa Định nghĩa 05.10): ghi chú diễn giả 3-03 và 5-04.
- Mức sàn sai số (đoạn cuối §8, Bài tập 05.6): ghi chú diễn giả 5-03.
- Câu ôn nhanh 1–3: ghi chú diễn giả 1-02.
- §11 (ý nghĩa, giới hạn): cột "Giả thiết không được bỏ" của 7-02, trang 7-03 và ghi chú diễn giả 7-01.
- §13 (câu hỏi cuối buổi): trang ví dụ 7-01 (dữ liệu, lời giải của ghi chú); không lặp ở câu hỏi tự kiểm tra.
- Phụ lục D ($w^*$, $\min_WL_S=0{,}06112$): số dùng ở 3-05; cách tính ở ghi chú diễn giả 3-05.

## 5. Ví dụ bổ trợ

Ví dụ xuyên suốt: **hồi quy ba quan sát trong mặt phẳng** (Ví dụ 05.1) và **hồi quy logistic trên một triệu hồ sơ** (khối ứng dụng §3). Mỗi lần dùng lại trả lời một câu hỏi mới. Hồi quy ba quan sát: dữ liệu và chi phí một gradient (2-01); gradient đầy đủ là trung bình (2-04); oracle và $G=4$ (3-03, 3-05); ba bước SGD, một bước làm $L_S$ tăng (1-06, 3-05); kì vọng có điều kiện ở bước thứ hai (3-08, 5-04); bất đẳng thức một bước bằng số (4-02); số vòng lặp và độ dài bước (4-06, 4-08). Hồi quy logistic: câu hỏi mở đầu (1-06); số bước SGD và GD (4-09); giá của bảo đảm với xác suất cao (ghi chú diễn giả 6-03); trả lời vấn đề trung tâm (7-03). Bài tập trên mặt trang lấy từ `exercises.md` với cùng số liệu, câu chữ và kết quả: Bài tập 05.1(d) (2-07), 05.3(b) (3-08), 05.4(c) (4-10), 05.3(c) (5-04), 05.5(b) (6-06), 05.5(d) (7-04, 7-05, tổng hợp).

Mọi con số dưới đây đã tính lại bằng Python (thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-05/storyboard/num.py`, `fig.py`) và khớp ghi chú, tệp bài tập. Không có ví dụ mới về số trên mặt trang. Dữ liệu vẽ hình mới (không ghi số mới trên nhãn) ở F1, F3, F4 được dựng từ công thức của ghi chú, cách dựng ghi ở mục 8.

**V1. Câu hỏi mở đầu** (1-06). Từ $w_3$ của Ví dụ 05.6, $L_S(w_3)=0{,}063858\approx0{,}0639$; ba lựa chọn $i_3$ cho $0{,}071030$; $0{,}102142$; $0{,}069380$ (trung bình $0{,}080851\approx0{,}0808$); bước GD cho $0{,}061359\approx0{,}0614$. Ứng dụng: $10^4$ bước đủ cho mức kì vọng $0{,}05$ trên quả cầu $\lVert w\rVert\le5$; $10^4/10^6=1\%$.

**V2. Ví dụ 05.1** (2-01). $\lVert x_3\rVert^2=0{,}36+0{,}64=1$; $L_S(0)=\tfrac13(1+1+0)=\tfrac23\approx0{,}6667$.

**V3. Ví dụ 05.3** (2-04). $\nabla_w\ell(0,z_i)=-2y_ix_i$: $(-2,0)$; $(0,2)$; $(0,0)$; $\nabla L_S(0)=\tfrac13(-2,2)=(-\tfrac23,\tfrac23)$.

**V4. Ví dụ 05.2** (2-05). $x=(1,2)$, $\tilde y=1$; $\langle w_0,x\rangle=0{,}5+0{,}5=1$; $u=w_0-0{,}1x=(0{,}4;0{,}05)$, $\langle u,x\rangle=0{,}5$, $\ell(u)=0{,}5$; $\ell(w_0)+\langle v,u-w_0\rangle=(-1{,}2)(-0{,}1)+(-2{,}4)(-0{,}2)=0{,}12+0{,}48=0{,}6>0{,}5$.

**V5. Ví dụ 05.4** (3-01, 3-02, hình F2). $\lVert\theta\rVert=\sqrt2=1{,}4142$; $\pi=(0{,}70711;-0{,}70711)$; $\pi-u=(-0{,}29289;-0{,}70711)$, $\lVert\pi-u\rVert=0{,}76537\approx0{,}7654$; $\lVert\theta-u\rVert=1$; $\langle\theta-\pi,u-\pi\rangle=0{,}08579-0{,}20711=-0{,}12132\approx-0{,}1213$.

**V6. Ví dụ 05.5** (3-03, 3-05). $\lVert\varphi(w,i)\rVert\le2(BC_x+C_y)C_x=2(1+1)=4$; $G=4$; $\varphi((10,0),1)=2\cdot9\cdot(1,0)=(18,0)$ (ghi chú diễn giả).

**V7. Ví dụ 05.6** (3-05, hình F3). $g_1=(-2,0)$, $w_2=(1,0)$, phần dư $0;\ 1;\ 0{,}6$, $L_S(w_2)=1{,}36/3=0{,}45333$; $g_2=(0,2)$, $w_2-\eta g_2=(1,-1)$, chuẩn $1{,}4142$; $w_3=(0{,}70711;-0{,}70711)$, phần dư $-0{,}29289;\ 0{,}29289;\ -0{,}14142$, $L_S(w_3)=0{,}063858$. Bước ba: $i_3=1$: $g_3=(-0{,}58579;0)$, điểm $(1;-0{,}70711)$, chuẩn $1{,}22474$, $w_4=(0{,}81650;-0{,}57735)$, $L_S=0{,}071030$; $i_3=2$: $w_4=(0{,}57735;-0{,}81650)$, $L_S=0{,}102142$; $i_3=3$: $g_3=(-0{,}16971;-0{,}22627)$, điểm $(0{,}79196;-0{,}59397)$, chuẩn $0{,}98995$, $L_S=0{,}069380$. GD: $\nabla L_S(w_3)=(-0{,}25183;0{,}11984)$, điểm $(0{,}83302;-0{,}76703)$, chuẩn $1{,}13237$, sau chiếu $(0{,}73565;-0{,}67737)$, $L_S=0{,}061359$. Phụ lục D: $M=\begin{pmatrix}0{,}4533&0{,}16\\0{,}16&0{,}5467\end{pmatrix}$, $c=(\tfrac13,-\tfrac13)$; nghiệm không ràng buộc $(1{,}06;-0{,}92)$, chuẩn $1{,}40357$, $L_S=0{,}006667$; $\kappa=0{,}134956$, $w^*=(0{,}74733;-0{,}66445)$, $L_S(w^*)=0{,}061117\approx0{,}06112$.

**V8. Ví dụ 05.7** (4-01, 4-02). $\lVert w_2-w^*\rVert^2=0{,}505340$; $\lVert w_3-w^*\rVert=0{,}058628$, bình phương $0{,}003437$; $\lVert(1,-1)-w^*\rVert=0{,}420040$, bình phương $0{,}176434$; vế trái $\langle g_2,w_2-w^*\rangle=2\cdot0{,}664453=1{,}328906$; vế phải $0{,}505340-0{,}003437+1=1{,}501903$; không chiếu $0{,}505340-0{,}176434+1=1{,}328906$ (đẳng thức). Kiểm khai triển: $0{,}505340-2\cdot0{,}5\cdot1{,}328906+0{,}25\cdot4=0{,}176434$.

**V9. Ví dụ 05.8** (4-06, 4-08, hình F4). $T\ge16/\epsilon^2$: $400$; $1600$; $6400$. $T=1600$: $\eta^*=1/(4\cdot40)=0{,}00625$; $0{,}06112+0{,}1=0{,}16112$. $(\gamma+1/\gamma)/2$: $1{,}25$ ($\gamma=2$ hoặc $\tfrac12$), $5{,}05$ ($\gamma=10$); với $RG/\sqrt T=0{,}1$: vế phải $0{,}125$ và $0{,}505$. $\eta=0{,}5$: $1/1600+4=4{,}000625$; hàm lỗi trên $W$ không quá $(BC_x+C_y)^2=4$.

**V10. Ví dụ 05.9** (4-09). $R=5$, $G=1$, $\epsilon=0{,}05$: $T\ge25/0{,}0025=10^4$; $\eta=5/(1\cdot100)=0{,}05$; GD: $10^4\cdot10^6=10^{10}$ gradient trên một quan sát.

**V11. Nhận xét 05.17** (ghi chú diễn giả 4-08; Phụ lục C). $\eta_t=1/(4\sqrt t)$, $T=1600$: $\sum_t\eta_t=19{,}6380$; $\sum_t\eta_t^2=0{,}497205$; vế phải $(1+16\cdot0{,}497205)/(2\cdot19{,}6380)=0{,}228009$ (ghi chú: "không quá $0{,}2281$"; Phụ lục C in $0{,}2280$).

**V12. Ví dụ 05.10** (5-01, hình F5). Hai nhánh bằng nhau tại $w=-0{,}125$; $\lvert f'\rvert$ lớn nhất trên $W$ là $2\lvert-0{,}125-1\rvert=2{,}25$; $R=2{,}5$; $\eta=2{,}5/(2{,}25\cdot40)=0{,}027778$; $RG/\sqrt T=0{,}140625$. Lặp trực tiếp 1600 bước từ $-1{,}5$: các điểm lặp trong $[-1{,}5;-1]$, $\bar w_{1600}=-1{,}005625$, $f(\bar w_{1600})=0{,}500032\approx0{,}5000$. Công thức cấp số nhân: $-0{,}5\cdot(1-(1-2\eta)^{1600})/(2\eta\cdot1600)=-0{,}005625$. $-s^2+4s+0{,}5=0$ tại $s=2-\sqrt{4{,}5}=-0{,}12132$, tức $w=-1{,}12132$; điểm lặp đầu tiên lớn hơn $-1{,}1213$ là $t=26$ ($w_{25}=-1{,}1268$, $w_{26}=-1{,}1198$).

**V13. Ví dụ 05.11** (5-02). GD: $1-10\cdot0{,}15=-0{,}5$; SGD: $1-0{,}3=0{,}7$, $1-2{,}7=-1{,}7$; $\tfrac12(\ln0{,}7+\ln1{,}7)=0{,}086977\approx0{,}087$; $\tfrac12(0{,}49+2{,}89)=1{,}69$; $\tfrac12(4+324)=164$; $\sqrt{164}=12{,}8062\approx12{,}81$.

**V14. Ví dụ 05.12** (5-03). $w_t=0{,}1;-0{,}1;\ldots$, $f(w_t)=0{,}1$; $\eta G^2/2=0{,}1$; $\lVert w_1-u\rVert^2/(2\eta T)=0{,}01/(0{,}4T)=0{,}025/T$; $\bar w_T=0$ khi $T$ chẵn ($\bar w_T=0{,}1/T$ khi $T$ lẻ, vẫn dưới cận; chỉ ở ghi chú diễn giả).

**V15. Ví dụ 05.13** (5-03). $\psi(w)=1{,}8w+0{,}2w-0{,}2=2w-0{,}2$; $\tilde F(w)=(w-0{,}1)^2+0{,}09$; $L_S(0{,}1)-0{,}25=0{,}16$.

**V16. Ví dụ 05.14** (6-03). $16/(0{,}0025\cdot0{,}01)=640\,000$; $640\,000/1600=400=1/0{,}05^2$; ứng dụng: $10^4/0{,}0025=4\,000\,000=4\cdot10^6$.

**V17. Ví dụ 05.15** (6-05). $T(b)=\lceil100(1+15/b)\rceil$: $1600$; $475$; $194$ ($193{,}75$); $124$ ($123{,}44$); $106$ ($105{,}86$); số quan sát $1600$; $1900$; $3104$; $7936$; $27\,136$; GD $100$ bước, $10^6$ quan sát.

**V18. Câu hỏi cuối buổi §13** (7-01). $\eta=0{,}00625$, $1-2\eta=0{,}9875$; $0{,}9875^{1600}=1{,}82\cdot10^{-9}$; $1-\bar w_{1600}=(1-0{,}9875^{1600})/20=0{,}05$; $\bar w_{1600}=0{,}95$; $L_S=0{,}0025$; $L_D=0{,}9025+1=1{,}9025$; $\min_WL_D=1$; sai số ước lượng $0{,}9025$.

**V19. Bài tập 05.1(d)** (2-07; số của `exercises.md`). $(-1,-2)$; $(2,1)$; trung bình $(0{,}5;-0{,}5)$. Kiểm tra (ghi chú diễn giả): tại $u=(1,-1)$, $L_S(u)=2=L_S(0)+\langle(0{,}5;-0{,}5),u\rangle=1+1$.

**V20. Bài tập 05.3(b)** (3-08; số của `exercises.md`). $w_2=(1,0)$; $(0,-1)$; $0$. $\psi(w_2)=(0{,}24;0{,}98667)$; $(-0{,}98667;-0{,}42667)$; $(-\tfrac23,\tfrac23)$. Chín ô (hàng $i_1$, cột $i_2$): $0;\ 1{,}32891;\ 0{,}81980$ / $1{,}49466;\ 0;\ 1{,}14694$ / $1{,}49466;\ 1{,}32891;\ 0$; tổng $7{,}61387$, trung bình $0{,}845985\approx0{,}8460$; trung bình hàng $0{,}71623$; $0{,}88053$; $0{,}94119$, trung bình $0{,}8460$. $\mathbb EL_S(w_2)=(0{,}45333+0{,}54667+0{,}66667)/3=0{,}55556$.

**V21. Bài tập 05.3(c)** (5-04; số của `exercises.md`). $g_2=0$; $0{,}55556-0{,}061117=0{,}494439\approx0{,}4944$.

**V22. Bài tập 05.4(c)** (4-10; số của `exercises.md`). $\hat G=8$: $T=6400$, $\eta=1/640=0{,}0015625$, $Q=0{,}05+0{,}0125=0{,}0625$; $\hat G=2$: $T=400$, $\eta=0{,}025$, $Q=0{,}05+0{,}2=0{,}25$.

**V23. Bài tập 05.5(b)** (6-06; số của `exercises.md`). $T(b)\le110\iff\sigma^2/b\le0{,}1\iff b\ge10\sigma^2$ (với $G_F^2=1$); $\sigma^2=3$: $b=30$, $T(30)=\lceil100\cdot1{,}1\rceil=110$, $3300$ quan sát; $\sigma^2=15$: $b=150$, $T=110$, $16\,500$.

**V24. Bài tập 05.5(d)** (7-04, 7-05; số của `exercises.md`). Markov: $\Pr(X_j\ge0{,}1)\le0{,}05/0{,}1=\tfrac12$; $\log_220=4{,}3219$, $k=5$, $2^{-5}=0{,}03125$, $2^{-4}=0{,}0625>0{,}05$; mỗi lần $16/0{,}05^2=6400$ bước; tổng $32\,000$; $640\,000-32\,000=608\,000=5m$ khi $m=121\,600$.

**V25. Câu ôn nhanh** (ghi chú diễn giả 1-02). (1) $a-a'=(0{,}5;-0{,}5)$, $0{,}5$; $1-1+0{,}5=0{,}5$. (2) $0{,}02/0{,}1=0{,}2$. (3) $\mathbb Eq_I=\tfrac23$, $\mathbb Eq_I^2=\tfrac43$, $\operatorname{Var}=\tfrac89$, $\tfrac49+\tfrac89=\tfrac43$.

**V26. Hình F4** (4-06; dựng từ vế phải của Định lý 05.14 với $R=1$, $G=4$, $T=1600$). $Q(\eta)=1/(3200\eta)+8\eta$: $\eta=0{,}0005$: $0{,}625+0{,}004=0{,}629$; $0{,}001$: $0{,}3205$; $0{,}002$: $0{,}1723$; $0{,}003125$: $0{,}1+0{,}025=0{,}125$; $0{,}00625$: $0{,}05+0{,}05=0{,}1$; $0{,}0125$: $0{,}025+0{,}1=0{,}125$; $0{,}025$: $0{,}2125$; $0{,}05$: $0{,}4063$; $0{,}0625$: $0{,}005+0{,}5=0{,}505$; $0{,}1$: $0{,}8031$. Chỉ các điểm $\eta^*$, $\eta^*/2$, $2\eta^*$, $10\eta^*$ có nhãn số (số của Ví dụ 05.8).

## 6. Danh sách trang

Mỗi mục: ID, tiêu đề, loại, thời lượng; **Mặt trang** (các dòng dự kiến, theo thứ tự; `[f]` là fragment; `$$…$$` là công thức hiển thị, tính một dòng; `{{…}}` là chỉ dẫn bố cục, không lên mặt trang); **Ghi chú diễn giả** (ý chính, 40–150 âm tiết, đến ~250 cho trang ý tưởng chứng minh; viết cho giảng viên và người học; không mã trang, mã ví dụ của storyboard, câu quy trình hay nguồn gốc; luôn kết thúc bằng dòng `note-source`); **Lý do / nối**; **Mục tiêu / nguồn**. Câu trên mặt trang là bản dự kiến đã tự kiểm theo `no-ai-slop` (chế độ Edit) và `eval.md`; người viết deck có thể rút gọn, không thêm khẳng định.

Quy ước chung cho người viết deck:
- Trang kết quả: "Giả thiết:" và "Bảo đảm:" (nhãn của ghi chú), trích số khối của ghi chú một lần.
- Trang tổng quan (bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm") viết bằng lời, không kí hiệu, không tiếng Anh. Lần đầu một thuật ngữ trên trang nội dung có tiếng Anh trong ngoặc (bảng mục 10).
- Mọi kí hiệu trên mặt trang đã có ở trang trước hoặc có dòng "Nhắc lại:"/"Kí hiệu:" (bảng đối chiếu mục 12 ghi chỗ đưa vào).
- Các cụm "Dùng khi …", "Bước 1 …" viết chữ thường hoặc in đậm như tên bước, không thành nhãn mới; chỉ dùng nhãn của danh sách hợp lệ.
- Số thập phân dùng dấu phẩy KaTeX `0{,}2`; dãy số ngăn bằng `;\ `; số từ năm chữ số tách nhóm bằng `\,`; toạ độ có số thập phân viết `(0{,}5;0{,}25)` như ghi chú.
- Mỗi trang ví dụ mở bằng dữ kiện dạng danh sách, không câu dẫn. "Diễn giải:" chỉ dùng số có trên chính trang đó.
- Trang ý tưởng chứng minh: lộ trình 3–5 bước, bất đẳng thức hoặc mẹo then chốt, chỗ giả thiết vào, bỏ giả thiết thì hỏng ở đâu; không chép chứng minh đầy đủ của ghi chú.
- Không `\text{}` chứa tiếng Việt trong KaTeX. Trong ghi chú diễn giả, không ghi "mới", "dựng", "V7", "mục 5", không mở bằng "Trang này", "Mạch này", "Bài này".
- Công thức một dòng khi vừa khung; chỉ ngắt bằng `aligned` khi tràn ở 390 px (đo trong trình duyệt). Ở chế độ đọc hẹp, công thức rộng cuộn ngang tại chỗ.
- Không dùng "tiến bộ", "nhiễu bước" như thuật ngữ trên mặt trang (ghi chú không đặt tên hai số hạng); mặt trang viết đúng hai số hạng $-2\eta\langle g,w-u\rangle$ và $\eta^2\lVert g\rVert^2$.

### Mạch 1. Mở đầu (6 trang, 9 phút)

#### `1-01` Hạ gradient, hạ gradient ngẫu nhiên và cận tối ưu — bìa, điểm vào mạch 1 · 1 phút
- **Mặt trang:** h1 tên bài; h3 "Bài 05"; luận điểm (mục 2, hai câu, bằng lời); "Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1"; "Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN".
- **Ghi chú diễn giả:** Bài 04 đo bộ giải bằng sai số tối ưu thực nghiệm nhưng chưa cho cách tính một nghiệm có sai số đó nhỏ. Bài 05 trả lời cho hạ gradient ngẫu nhiên có chiếu trên một hàm mục tiêu lồi. Câu thứ nhất của luận điểm là bất đẳng thức một bước: bình phương khoảng cách tới một điểm so sánh giảm một lượng tỉ lệ với độ dài bước và tăng một lượng tỉ lệ với bình phương độ dài bước. Câu thứ hai là cận kì vọng: cộng các bước, các khoảng cách triệt tiêu, và với độ dài bước chọn theo số vòng lặp, cận giảm như một chia căn bậc hai của số vòng lặp. Mọi cận của bài chặn độ chênh tối ưu của chính hàm mà thuật toán tối thiểu hóa, ở đây là rủi ro thực nghiệm. Nguồn: ghi chú Bài 05, đoạn mở đầu, §7, §11.
- **Lý do / nối:** luận điểm cả bài → tiên quyết.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu, §11.

#### `1-02` Tiên quyết và quy ước — mở đầu · 1,5 phút
- **Mặt trang:**
  - **Nhắc lại:** sai số tối ưu thực nghiệm $\operatorname{opt}_S(w)=L_S(w)-\inf_{w'\in W}L_S(w')$ (Định nghĩa 04.2); (O2): $\operatorname{opt}_S\le\epsilon_{\mathrm{opt}}$ trên mọi tập huấn luyện.
  - Bất đẳng thức Markov (Bổ đề 02.2): $V\ge0$, $\alpha>0$ thì $\Pr(V\ge\alpha)\le\mathbb EV/\alpha$.
  - Sai số ước lượng $L_D(w)-\inf_{w'\in W}L_D(w')$ (Định nghĩa 04.1); (T1): $S\sim D^m$.
  - **Kí hiệu:** tích vô hướng $\langle\cdot,\cdot\rangle$, chuẩn Euclid $\lVert\cdot\rVert$; $\lVert a-a'\rVert^2=\lVert a\rVert^2-2\langle a,a'\rangle+\lVert a'\rVert^2$.
  - Tính chất tháp (tower property) $\mathbb E\,\mathbb E[V\mid\mathcal G]=\mathbb EV$; lấy ra đại lượng đã biết (taking out what is known).
- **Ghi chú diễn giả:** Mức (O2) của Bài 01 đòi bộ giải đạt độ chính xác $\epsilon_{\mathrm{opt}}$ một cách tất định trên mọi tập huấn luyện; mạch 6 so mức đó với bảo đảm theo kì vọng của một thuật toán ngẫu nhiên. Bất đẳng thức Markov đổi một cận kì vọng của một biến không âm thành một cận xác suất. Quy tắc lấy ra đại lượng đã biết: nếu $V$ đo được theo $\mathcal G$ thì $\mathbb E[VU\mid\mathcal G]=V\,\mathbb E[U\mid\mathcal G]$. Câu ôn nhanh: với $a=(1,0)$, $a'=(0{,}5;0{,}5)$, cả hai cách cho $\lVert a-a'\rVert^2=0{,}5$; với $\mathbb EV\le0{,}02$, $\Pr(V\ge0{,}1)\le0{,}2$; với $q=(0,2,0)$ và chỉ số đều, $\mathbb Eq_I^2=\tfrac43=\tfrac49+\tfrac89$, tức bình phương trung bình cộng phương sai. Đẳng thức cuối trở lại ở oracle và ở lô nhỏ. Nguồn: ghi chú Bài 05, Kiến thức tiên quyết, Câu hỏi ôn nhanh.
- **Lý do / nối:** các kết quả của Bài 01–04 và công cụ xác suất dùng trên mặt trang được nhắc lại ở đây → mục tiêu.
- **Mục tiêu / nguồn:** 1, 2, 3; Kiến thức tiên quyết.

#### `1-03` Mục tiêu — mở đầu · 1 phút
- **Mặt trang (danh sách đánh số, bằng lời, không kí hiệu; trần 80):**
  1. Chứng minh cận kì vọng cho hạ gradient ngẫu nhiên có chiếu, chỉ rõ chỗ dùng giả thiết.
  2. Kiểm tra tính không chệch có điều kiện khi biết lịch sử.
  3. Chọn độ dài bước, số vòng lặp từ cận, kể cả với xác suất cao.
  4. So sánh hạ gradient, bản ngẫu nhiên, lô nhỏ theo số cập nhật, số quan sát.
  5. Dựng phản ví dụ khi bỏ một giả thiết; nêu vì sao cận không chặn điểm lặp cuối.
- **Ghi chú diễn giả:** Mục tiêu 1 xét một hàm mục tiêu lồi. Mục tiêu 2 gồm phát biểu tính không chệch có điều kiện và kiểm tra nó cho cách rút một quan sát ngẫu nhiên có hoàn lại từ tập huấn luyện. Mục tiêu 3 gồm chọn độ dài bước và số vòng lặp cho một độ chênh tối ưu cho trước theo kì vọng, và tính số vòng lặp cần thêm cho bảo đảm với xác suất cao. Mục tiêu 4 so theo hai đơn vị: số lần cập nhật và số quan sát phải xử lý. Ở mục tiêu 5, ba giả thiết là tính lồi, cận mô-men bậc hai và tính không chệch của oracle. Nguồn: ghi chú Bài 05, Mục tiêu học tập, §12.
- **Lý do / nối:** tiêu chí kiểm tra → nội dung.
- **Mục tiêu / nguồn:** tất cả; Mục tiêu học tập.

#### `1-04` Nội dung — mở đầu · 0,5 phút
- **Mặt trang:** `ol start="2"` với liên kết `#/2`…`#/7`: 2. Hàm lồi và dưới gradient; 3. Phép chiếu và hạ gradient ngẫu nhiên; 4. Bất đẳng thức một bước và cận kì vọng; 5. Vai trò của từng giả thiết; 6. Hạ gradient ngẫu nhiên trên rủi ro thực nghiệm và lô nhỏ; 7. Tổng kết. Dòng đọc trước: "Đọc trước: UML §12.1, §14.1."
- **Ghi chú diễn giả:** Mạch 2 cho một hướng đi tại điểm không khả vi và một cận dưới toàn cục từ thông tin tại một điểm. Mạch 3 giữ điểm lặp trong tập tham số và thay gradient đầy đủ bằng gradient trên một quan sát. Mạch 4 là chứng minh chính. Mạch 5 bỏ từng giả thiết. Mạch 6 áp dụng cận cho rủi ro thực nghiệm, thêm bảo đảm với xác suất cao và lô nhỏ, rồi tách sai số tối ưu thực nghiệm khỏi rủi ro kì vọng. Nguồn: ghi chú Bài 05; §14.
- **Lý do / nối:** bản đồ mạch → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §14.

#### `1-05` Vấn đề trung tâm — mở đầu · 1 phút
- **Mặt trang:** một hộp `div.box`: "**Câu hỏi:** tối ưu ngẫu nhiên làm giảm một hàm mục tiêu nhanh đến mức nào theo số vòng lặp?" (20 âm tiết kể cả nhãn, theo script).
- **Ghi chú diễn giả** (câu trả lời theo mạch, không trên mặt trang): (2) với hàm lồi, dưới gradient tại một điểm cho cận dưới trên toàn không gian, và dưới gradient của rủi ro thực nghiệm là trung bình dưới gradient trên từng quan sát; (3) phép chiếu không làm tăng khoảng cách tới điểm của tập tham số, và khi biết các lần rút trước, gradient ngẫu nhiên có trung bình là một dưới gradient; (4) với độ dài bước $R/(G\sqrt T)$, độ chênh tối ưu kì vọng tại điểm lặp trung bình không quá $RG/\sqrt T$; (5) bỏ tính lồi, cận mô-men bậc hai hay tính không chệch, kết luận sai; (6) trên tập huấn luyện, cận chặn sai số tối ưu thực nghiệm, với giá $1/\delta'^2$ cho xác suất cao. Nguồn: ghi chú Bài 05, đoạn mở đầu, §11.
- **Lý do / nối:** một vấn đề cốt lõi → câu hỏi cụ thể.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu.

#### `1-06` Ví dụ: một triệu hồ sơ và ba quan sát — ví dụ dẫn nhập · 4 phút
- **Mặt trang:**
  - $m=10^6$ hồ sơ, hàm lỗi logistic (logistic loss): tối thiểu hóa $L_S(w)$.
  - Hạ gradient (gradient descent, GD): mỗi bước cần $10^6$ gradient.
  - Hạ gradient ngẫu nhiên (stochastic gradient descent, SGD): mỗi bước một quan sát rút đều.
  - Ba quan sát, từ $L_S=0{,}0639$: bước SGD cho $0{,}0694$; $0{,}0710$; $0{,}1021$; bước GD cho $0{,}0614$.
  - **Câu hỏi:** SGD bảo đảm gì cho $L_S$ sau $T$ bước?
- **Ghi chú diễn giả:** Mỗi hồ sơ là một quan sát gồm véc-tơ chỉ số đo và một nhãn; hàm phân lớp là tuyến tính, và $\ell(w,z_i)$ là hàm lỗi trên quan sát thứ $i$. Khi chỉ số $i$ rút đều từ $\{1,\ldots,m\}$, $\mathbb E_i\nabla_w\ell(w,z_i)=\nabla L_S(w)$, nên một bước SGD rẻ hơn $10^6$ lần mà vẫn đi đúng hướng theo trung bình. Bốn số sau lấy từ ví dụ hồi quy ba quan sát của mạch 3, cùng độ dài bước: từ một điểm lặp có $L_S=0{,}0639$, cả ba lựa chọn quan sát đều làm $L_S$ tăng, trung bình lên $0{,}0808$. Bước SGD mang thêm phần nhiễu, và phần nhiễu có thể lớn hơn phần giảm do gradient. Bảo đảm của SGD vì vậy là một cận kì vọng tại trung bình các điểm lặp, không phải sự giảm ở từng bước. Với hồi quy logistic trên $10^6$ hồ sơ và tập tham số $\lVert w\rVert\le5$, $\lVert x\rVert\le1$, câu trả lời của bài là $10^4$ bước cho độ chênh tối ưu kì vọng không quá $0{,}05$. Nguồn: ghi chú Bài 05, Câu hỏi mở đầu và hai đoạn sau; §3, khối ứng dụng.
- **Lý do / nối:** ví dụ dẫn nhập trước mọi định nghĩa; hai ví dụ xuyên suốt của bài → tiêu đề mạch 2.
- **Mục tiêu / nguồn:** 1, 3, 4; Câu hỏi mở đầu, §3.

### Mạch 2. Hàm lồi và dưới gradient (8 trang, 22 phút)

#### `2-00` 2. Hàm lồi và dưới gradient — tiêu đề mạch, điểm vào mạch 2 · 0,5 phút
- **Mặt trang:** "2."; h2 "Hàm lồi và dưới gradient"; `p.strand-lead` (bảng mạch, 24 âm tiết); `p.strand-keys`: "hàm lồi · dưới gradient · dưới vi phân · hằng số Lipschitz".
- **Ghi chú diễn giả:** Hàm lỗi 0–1 của Bài 01–04 không lồi theo $w$, còn hàm lỗi bản lề có điểm gãy. Phương pháp gradient cần hai thứ: một véc-tơ đóng vai gradient ở điểm không khả vi, và một điều kiện để từ thông tin tại một điểm suy ra cận dưới cho hàm mục tiêu trên toàn không gian. Tính lồi và dưới gradient cho cả hai. Hằng số Lipschitz chặn độ dài của dưới gradient, và cận đó trở thành hằng số $G$ trong mọi cận của bài. Nguồn: ghi chú Bài 05, §1–§4.
- **Lý do / nối:** mạch 1 → thiết lập.
- **Mục tiêu / nguồn:** 1; §1–§4.

#### `2-01` Thiết lập và ví dụ hồi quy ba quan sát — định nghĩa (khung), ví dụ xuyên suốt · 3,5 phút
- **Mặt trang** {{`grid2`: thẻ trái thiết lập, thẻ phải Ví dụ 05.1}}:
  - Hàm mục tiêu $F=L_S$, $S$ cố định; tập tham số $W\subset\mathbb R^p$ khác rỗng, đóng, lồi.
  - Ngẫu nhiên chỉ đến từ các lần rút $\xi_1,\xi_2,\ldots$ của thuật toán.
  - Độ chênh tối ưu (suboptimality) của $w\in W$: $F(w)-F(u)$, $u\in W$, hoặc $F(w)-\inf_{w'\in W}F(w')$.
  - **Ví dụ 05.1.** $z_1=((1,0),1)$, $z_2=((0,1),-1)$, $z_3=((0{,}6;0{,}8),0)$; $\ell(w,(x,y))=(\langle w,x\rangle-y)^2$.
  - $L_S(0)=\tfrac23$; gradient của $L_S$ là trung bình ba gradient trên từng quan sát.
- **Ghi chú diễn giả:** Bài toán có tám thành phần: hàm mục tiêu, tập tham số, dữ liệu đã cố định, nguồn ngẫu nhiên riêng của thuật toán, thuật toán với độ dài bước hằng và số vòng lặp chọn trước, đầu ra là trung bình các điểm lặp, đối tượng so sánh, và tài nguyên. Tài nguyên đếm bằng số vòng lặp và số gradient trên một quan sát: một vòng GD trên $L_S$ tốn $m$, một vòng SGD tốn một. Cố định: $S$, $F$, $W$, điểm khởi tạo, độ dài bước, số vòng lặp, mọi $u\in W$. Ngẫu nhiên theo các lần rút: chỉ số rút ở mỗi bước, các điểm lặp từ bước hai, trung bình các điểm lặp. Với GD, không có gì ngẫu nhiên. Khi $S\sim D^m$, các đại lượng cố định thành hàm của $S$, và các cận của bài đúng với mọi giá trị của $S$. Khi $F=L_S$, độ chênh so với cận dưới đúng là $\operatorname{opt}_S(w)$. Trong ví dụ, $\lVert x_i\rVert=1$ và $\lvert y_i\rvert\le1$, nên $C_x=C_y=1$; $W$ sẽ là quả cầu tâm $0$. Nguồn: ghi chú Bài 05, §1 (tám thành phần, bảng nguồn ngẫu nhiên), §3, Ví dụ 05.1.
- **Lý do / nối:** khung chung và ví dụ xuyên suốt trước mọi định nghĩa → hàm lồi.
- **Mục tiêu / nguồn:** 1; §1, §3, Ví dụ 05.1.

#### `2-02` Tập lồi và hàm lồi — vấn đề, trực quan, định nghĩa · 3 phút
- **Mặt trang:**
  - Hàm lỗi 0–1 không lồi theo $w$; hàm lỗi bản lề (hinge loss) có điểm gãy.
  - **Trực quan.** Đồ thị hàm lồi nằm dưới mọi dây cung.
  - **Định nghĩa 05.1.** Tập $W$ lồi (convex set) khi $\alpha w+(1-\alpha)u\in W$ với mọi $w,u\in W$, $\alpha\in[0,1]$; hàm $F$ lồi khi
  - $$F(\alpha w+(1-\alpha)u)\le\alpha F(w)+(1-\alpha)F(u)\quad\forall w,u\in\mathbb R^p,\ \alpha\in[0,1].$$
  - Bất đẳng thức lồi hữu hạn (còn gọi là bất đẳng thức Jensen hữu hạn): $F\big(\sum_t\alpha_tw_t\big)\le\sum_t\alpha_tF(w_t)$, $\alpha_t\ge0$, $\sum_t\alpha_t=1$.
- **Ghi chú diễn giả:** Bất đẳng thức lồi hữu hạn chứng minh bằng quy nạp: viết tổ hợp thành $(1-\alpha_k)\bar v+\alpha_kw_k$ rồi dùng định nghĩa cho cặp $(\bar v,w_k)$. Bất đẳng thức đúng cho từng dãy điểm cố định, nên áp dụng được trên từng quỹ đạo của thuật toán, không cần kì vọng; cùng lập luận cho thấy tổ hợp lồi của các điểm thuộc $W$ thuộc $W$. Ví dụ lồi: quả cầu $\lVert w\rVert\le B$, hàm $\lVert w\rVert^2$, hàm $(\langle w,x\rangle-y)^2$ với $(x,y)$ cố định, cực đại của hai hàm afin. Ví dụ không lồi: tập $\{-1,1\}$, mặt cầu đơn vị, hàm $(w^2-1)^2$ vì $f(0)=1>\tfrac12f(-1)+\tfrac12f(1)=0$, và rủi ro thực nghiệm với hàm lỗi 0–1 xem như hàm của $w$ (Bài tập 05.7). Nguồn: ghi chú Bài 05, §4, Định nghĩa 05.1 và các đoạn sau.
- **Lý do / nối:** vấn đề (hai hàm lỗi quen thuộc không dùng được) → trực quan → định nghĩa → dưới gradient.
- **Mục tiêu / nguồn:** 1, 5; §4, Định nghĩa 05.1.

#### `2-03` Dưới gradient và dưới vi phân — ví dụ, định nghĩa, hình F1 · 3 phút
- **Mặt trang** {{`grid2`: chữ trái, hình F1 phải}}:
  - **Ví dụ.** $f(w)=\lvert w\rvert$: $\lvert u\rvert\ge f(0)+vu$ với mọi $u$ khi $\lvert v\rvert\le1$.
  - **Định nghĩa 05.2.** $v$ là dưới gradient (subgradient) của $F$ tại $w$ khi với mọi $u\in\mathbb R^p$,
  - $$F(u)\ge F(w)+\langle v,u-w\rangle.$$
  - Dưới vi phân (subdifferential) $\partial F(w)$: tập mọi dưới gradient; $F$ lồi thì $\partial F(w)\ne\varnothing$, bằng $\{\nabla F(w)\}$ khi khả vi.
  - $0\in\partial F(w)$ khi và chỉ khi $w$ là điểm cực tiểu toàn cục của $F$.
  - {{hình F1 bên phải}}
- **Ghi chú diễn giả:** Bất đẳng thức trong định nghĩa được gọi là bất đẳng thức dưới gradient (subgradient inequality): đồ thị của $F$ nằm trên siêu phẳng afin qua $(w,F(w))$ với hệ số góc $v$. Với $\lvert w\rvert$, dưới vi phân tại $0$ là đoạn $[-1,1]$, còn tại $w\ne0$ chỉ có dấu của $w$. Đọc hình: bên trái, các đường thẳng qua gốc với hệ số góc trong $[-1,1]$ đều nằm dưới đồ thị; bên phải, hàm không lồi $(w^2-1)^2$ có đạo hàm $0$ tại $0$, nhưng đường nằm ngang qua $(0,1)$ cắt đồ thị, vì $f(\pm1)=0<1$; vậy $0\notin\partial f(0)$ dù $f'(0)=0$. Không có tính lồi, đạo hàm bằng $0$ không cho cực tiểu toàn cục. Khẳng định $\partial F(w)\ne\varnothing$ cho hàm lồi hữu hạn trên $\mathbb R^p$ lấy từ UML §14.2. Nguồn: ghi chú Bài 05, §4, Định nghĩa 05.2 và ba đoạn sau; UML §14.2.
- **Lý do / nối:** ví dụ một chiều trước định nghĩa; hình đặt hàm lồi cạnh hàm không lồi → quy tắc tính.
- **Mục tiêu / nguồn:** 1, 5; Định nghĩa 05.2.

#### `2-04` Ba quy tắc tính dưới gradient — kết quả, ví dụ · 3 phút
- **Mặt trang:**
  - **Mệnh đề 05.3.** **Giả thiết:** $F,F_1,\ldots,F_m:\mathbb R^p\to\mathbb R$, $w\in\mathbb R^p$. **Bảo đảm:** ba khẳng định tất định.
  - (a) $F$ lồi, khả vi tại $w$: $\nabla F(w)\in\partial F(w)$.
  - (b) $v_i\in\partial F_i(w)$, $i=1,\ldots,m$: $\frac1m\sum_iv_i\in\partial\big(\frac1m\sum_iF_i\big)(w)$.
  - (c) $F=\max\{F_1,\ldots,F_m\}$, $F_j(w)=F(w)$, $v\in\partial F_j(w)$: $v\in\partial F(w)$.
  - **Ví dụ.** Ví dụ 05.1 tại $w=0$: $\nabla_w\ell(0,z_i)=-2y_ix_i$ là $(-2,0)$; $(0,2)$; $(0,0)$; theo (a), (b), $\nabla L_S(0)=(-\tfrac23,\tfrac23)$.
  - Rút đều một chỉ số cho một véc-tơ có trung bình $\nabla L_S(0)$.
- **Ghi chú diễn giả:** Lộ trình chứng minh. Phần (a): định nghĩa hàm lồi trên đoạn từ $w$ tới $u$ cho $[F(w+\alpha(u-w))-F(w)]/\alpha\le F(u)-F(w)$; cho $\alpha\downarrow0$, vế trái là đạo hàm theo hướng, bằng $\langle\nabla F(w),u-w\rangle$; tính lồi dùng ở đây. Phần (b): cộng $m$ bất đẳng thức dưới gradient rồi chia cho $m$. Phần (c): $F(u)\ge F_j(u)\ge F_j(w)+\langle v,u-w\rangle=F(w)+\langle v,u-w\rangle$. Trong ví dụ, hàm lỗi bình phương lồi theo $w$ vì $s\mapsto(s-y)^2$ lồi và $w\mapsto\langle w,x\rangle$ tuyến tính, nên $L_S$ lồi; gradient trên một quan sát là $2(\langle w,x\rangle-y)x$ theo quy tắc hàm hợp. Phần (b) là lý do gradient trên một quan sát rút đều có trung bình là một dưới gradient của $L_S$. Nguồn: ghi chú Bài 05, §4, Mệnh đề 05.3 và chứng minh; Ví dụ 05.3.
- **Lý do / nối:** quy tắc tính cần cho hàm lỗi bản lề và cho oracle → ví dụ bản lề.
- **Mục tiêu / nguồn:** 1, 2; Mệnh đề 05.3, Ví dụ 05.3.

#### `2-05` Ví dụ: dưới gradient của hàm lỗi bản lề — ví dụ (Ví dụ 05.2) · 3 phút
- **Mặt trang:**
  - $x=(1,2)$, $y=1$, nên $\tilde y=2y-1=1$; hàm lỗi bản lề là cực đại của hai hàm afin:
  - $$\ell(w)=\max\{0,\,1-\tilde y\langle w,x\rangle\}.$$
  - $w=0$: chỉ nhánh thứ hai đạt cực đại, nên $(-1,-2)\in\partial\ell(0)$ (Mệnh đề 05.3(a), (c)).
  - Điểm gãy $w_0=(0{,}5;0{,}25)$: hai nhánh bằng $0$; $0$, $(-1,-2)$ và $(-\alpha,-2\alpha)$, $\alpha\in[0,1]$, là dưới gradient.
  - $v=(-1{,}2;-2{,}4)$, $u=(0{,}4;0{,}05)$: $\ell(u)=0{,}5<0{,}6=\ell(w_0)+\langle v,u-w_0\rangle$, nên $v\notin\partial\ell(w_0)$.
  - **Kết luận:** $\partial\ell(w_0)$ chứa đoạn nối $0$ và $(-1,-2)$, không chứa $v$.
- **Ghi chú diễn giả:** Nhãn $\tilde y=2y-1\in\{-1,1\}$ ứng với nhãn $y\in\{0,1\}$ của học phần; hàm lỗi bản lề viết cho hàm điểm số $h_w(x)=\langle w,x\rangle$. Hai nhánh có gradient $0$ và $-\tilde yx=(-1,-2)$. Tại điểm gãy, mỗi tổ hợp lồi $(-\alpha,-2\alpha)$ là dưới gradient: nhân bất đẳng thức dưới gradient của $(-1,-2)$ với $\alpha$, của $0$ với $1-\alpha$, rồi cộng. Với $\alpha=1{,}2$, điểm thử $u=w_0-0{,}1x$ có $\langle u,x\rangle=0{,}5$, và vế phải $(-1{,}2)(-0{,}1)+(-2{,}4)(-0{,}2)=0{,}6$ vượt $\ell(u)$. Bài tập 05.1(b) chứng minh dưới vi phân tại điểm gãy bằng đúng đoạn này. Tại $w=(1,1)$, $\langle w,x\rangle=3>1$, hàm lỗi bằng $0$ quanh $w$ và dưới vi phân chỉ có $0$. Nguồn: ghi chú Bài 05, §4, Ví dụ 05.2.
- **Lý do / nối:** kiểm tra Mệnh đề 05.3 trên hàm không khả vi → tính Lipschitz.
- **Mục tiêu / nguồn:** 1; Ví dụ 05.2.

#### `2-06` Hằng số Lipschitz và chuẩn của dưới gradient — định nghĩa, kết quả · 3 phút
- **Mặt trang:**
  - **Định nghĩa 05.4.** $F$ là $G$-Lipschitz trên $C$ khi $\lvert F(w)-F(u)\rvert\le G\lVert w-u\rVert$ với mọi $w,u\in C$.
  - **Mệnh đề 05.5.** **Giả thiết:** $F$ lồi; $U\subset\mathbb R^p$, mở ở phần (b); $G\ge0$. **Bảo đảm:** tất định.
  - (a) Mỗi $u\in U$ có một $v_u\in\partial F(u)$ với $\lVert v_u\rVert\le G$: $F$ là $G$-Lipschitz trên $U$.
  - (b) $F$ là $G$-Lipschitz trên $U$: $\lVert v\rVert\le G$ với mọi $w\in U$, $v\in\partial F(w)$.
  - **Ví dụ.** Hàm lỗi bản lề, logistic: $\lVert x\rVert$-Lipschitz; $w^2$ không Lipschitz trên $\mathbb R$.
- **Ghi chú diễn giả:** Lộ trình chứng minh. Phần (a): bất đẳng thức dưới gradient tại $u$ cho $F(u)-F(w)\le\langle v_u,u-w\rangle\le G\lVert u-w\rVert$ theo Cauchy–Schwarz, rồi đổi vai. Phần (b): thử bất đẳng thức dưới gradient tại $u=w+\alpha v/\lVert v\rVert$, thuộc $U$ khi $\alpha$ đủ nhỏ vì $U$ mở; được $\alpha\lVert v\rVert\le G\alpha$. Theo (b), mỗi bước hạ gradient có độ dài $\eta\lVert v\rVert\le\eta G$. Hàm lỗi bình phương không Lipschitz trên toàn $\mathbb R^p$, vì gradient $2(\langle w,x\rangle-y)x$ tăng theo $\lVert w\rVert$; trên quả cầu bán kính $B$, với $\lVert x\rVert\le C_x$, $\lvert y\rvert\le C_y$, nó là $2(BC_x+C_y)C_x$-Lipschitz theo (a). Định nghĩa 05.6 của ghi chú: $F$ là $\beta$-trơn ($\beta$-smooth) khi gradient là $\beta$-Lipschitz, và $\lambda$-lồi mạnh ($\lambda$-strongly convex) khi $F$ nằm dưới dây cung ít nhất $\tfrac\lambda2\alpha(1-\alpha)\lVert w-u\rVert^2$; trong ví dụ hồi quy, $L_S$ là $\tfrac23$-lồi mạnh và $\tfrac43$-trơn (Bài tập 05.12). Cận nhanh hơn của UML §14.4.4 cần tính lồi mạnh. Nguồn: ghi chú Bài 05, §4, Định nghĩa 05.4, Mệnh đề 05.5 và chứng minh, Định nghĩa 05.6 và đoạn sau.
- **Lý do / nối:** cận chuẩn dưới gradient sẽ là hằng số $G$ → bài tập của cụm.
- **Mục tiêu / nguồn:** 1; Định nghĩa 05.4, Mệnh đề 05.5.

#### `2-07` Bài tập: dưới gradient của rủi ro thực nghiệm với hàm lỗi bản lề — bài tập (Bài tập 05.1(d)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Câu hỏi:** mẫu $S$ gồm hai quan sát $((1,2),1)$ và $((2,1),0)$, với hàm lỗi bản lề.
  - Tìm một dưới gradient của $L_S$ tại $w=0$.
  - `[f]` **Lời giải:** quan sát thứ nhất: $\tilde y_1=1$, $1-\langle0,x_1\rangle=1>0$, gradient $-\tilde y_1x_1=(-1,-2)$.
  - `[f]` Quan sát thứ hai: $\tilde y_2=-1$, $1+\langle0,x_2\rangle=1>0$, gradient $-\tilde y_2x_2=(2,1)$.
  - `[f]` Theo Mệnh đề 05.3(b): $\tfrac12\big[(-1,-2)+(2,1)\big]=(0{,}5;-0{,}5)\in\partial L_S(0)$.
- **Ghi chú diễn giả:** Tại $w=0$ cả hai hàm lỗi ở nhánh afin dương, nên khả vi, và Mệnh đề 05.3(a) cho gradient của từng hàm lỗi. Kiểm tra: tại $u=(1,-1)$, cả hai hàm lỗi bằng $2$, nên $L_S(u)=2=L_S(0)+\langle(0{,}5;-0{,}5),u\rangle=1+1$, bất đẳng thức dưới gradient đúng với dấu bằng. Phần (c) của bài: với $x=(2,1)$, $y=0$, dưới gradient tại $0$ là $(2,1)$, tại $(-1,0)$ là $0$, và dưới vi phân tại điểm gãy $(-0{,}4;-0{,}2)$ là $\{\alpha(2,1):\alpha\in[0,1]\}$. Phần (a), (b) chứng minh tính lồi và dạng của dưới vi phân tại điểm gãy. Nguồn: tệp bài tập, Bài tập 05.1(d), (c), (a), (b).
- **Lý do / nối:** bài tập của cụm hàm lồi, lời giải trên mặt trang; cùng cơ chế với oracle rút một quan sát → mạch 3.
- **Mục tiêu / nguồn:** 1; Bài tập 05.1(d).

### Mạch 3. Phép chiếu và hạ gradient ngẫu nhiên (9 trang, 22 phút)

#### `3-00` 3. Phép chiếu và hạ gradient ngẫu nhiên — tiêu đề mạch, điểm vào mạch 3 · 0,5 phút
- **Mặt trang:** "3."; h2 "Phép chiếu và hạ gradient ngẫu nhiên"; `p.strand-lead` (bảng mạch, 25 âm tiết); `p.strand-keys`: "phép chiếu · oracle gradient ngẫu nhiên · điểm lặp trung bình · lịch sử".
- **Ghi chú diễn giả:** Với hàm lỗi bình phương, gradient lớn dần theo $\lVert w\rVert$, nên một cận cho chuẩn gradient chỉ đúng trên một tập bị chặn; phép chiếu đưa điểm lặp về tập đó mà không làm xa điểm nào của tập. Gradient đầy đủ của $L_S$ tốn $m$ gradient trên một quan sát; oracle thay nó bằng một véc-tơ ngẫu nhiên rẻ, có trung bình đúng. Hai thuật toán của bài dùng chung phép cập nhật. Kết quả cuối của mạch là kì vọng có điều kiện của gradient ngẫu nhiên khi biết các lần rút trước, bước then chốt của chứng minh ở mạch 4. Nguồn: ghi chú Bài 05, §5–§6.
- **Lý do / nối:** mạch 2 (cận $G$ trên tập bị chặn; gradient đầy đủ là trung bình) → phép chiếu.
- **Mục tiêu / nguồn:** 1, 2; §5–§6.

#### `3-01` Phép chiếu lên tập lồi đóng — vấn đề, định nghĩa, ví dụ, hình F2 · 2,5 phút
- **Mặt trang** {{`grid2`: chữ trái, hình F2 phải}}:
  - Gradient $2(\langle w,x\rangle-y)x$ có chuẩn tăng theo $\lVert w\rVert$: cận $G$ chỉ đúng trên tập bị chặn.
  - **Định nghĩa 05.7.** $W$ khác rỗng, đóng, lồi: phép chiếu Euclid (Euclidean projection) $\operatorname{proj}_W(\theta)$ là điểm của $W$ gần $\theta$ nhất.
  - Tồn tại vì $W$ đóng, duy nhất vì $W$ lồi.
  - **Ví dụ.** Quả cầu bán kính $B$: $\operatorname{proj}_W(\theta)=B\theta/\lVert\theta\rVert$ khi $\lVert\theta\rVert>B$; $B=1$, $\theta=(1,-1)$: $\approx(0{,}7071;-0{,}7071)$.
  - Với $u=(1,0)\in W$: $\lVert\theta-u\rVert=1$, khoảng cách sau chiếu $\approx0{,}7654$.
  - {{hình F2 bên phải}}
- **Ghi chú diễn giả:** Khi $\theta\in W$, phép chiếu giữ nguyên $\theta$; với $W=\mathbb R^p$ nó là ánh xạ đồng nhất. Bỏ một trong hai giả thiết thì điểm gần nhất có thể không duy nhất hoặc không tồn tại: với $W=\{-1,1\}$ (không lồi) và $\theta=0$ có hai điểm gần nhất; với quả cầu mở và $\theta$ ở ngoài, không có điểm gần nhất. Đọc hình: điểm $\theta=(1,-1)$ có chuẩn $\sqrt2\approx1{,}4142$, ảnh của nó là $\theta/\sqrt2$ trên đường tròn đơn vị, và khoảng cách tới $u=(1,0)$ giảm từ $1$ xuống $0{,}7654$. Góc tại ảnh giữa hướng về $\theta$ và hướng về $u$ là góc tù. Chiếu lên quả cầu tốn cỡ $p$ phép tính; với một tập lồi đóng tổng quát, tính phép chiếu là một bài toán tối ưu riêng. Nguồn: ghi chú Bài 05, §5, Định nghĩa 05.7 và hai đoạn sau, Ví dụ 05.4, đoạn cuối §5.
- **Lý do / nối:** vấn đề (cận $G$ cần tập bị chặn) → định nghĩa → ví dụ bằng số trước bổ đề → bất đẳng thức của phép chiếu.
- **Mục tiêu / nguồn:** 1; §5, Định nghĩa 05.7, Ví dụ 05.4.

#### `3-02` Bất đẳng thức của phép chiếu — trực quan, kết quả · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Góc giữa $\theta-\pi$ và mọi hướng $u-\pi$ vào $W$ không nhọn.
  - **Bổ đề 05.8.** **Giả thiết:** $W$ khác rỗng, đóng, lồi; $\theta\in\mathbb R^p$; $\pi=\operatorname{proj}_W(\theta)$. **Bảo đảm:** tất định.
  - (a) Bất đẳng thức biến phân (variational inequality): $\langle\theta-\pi,u-\pi\rangle\le0$ với mọi $u\in W$; chỉ $\pi$ có tính chất này.
  - (b) Với mọi $u\in W$: $$\lVert\pi-u\rVert^2\le\lVert\theta-u\rVert^2-\lVert\theta-\pi\rVert^2\le\lVert\theta-u\rVert^2.$$
  - **Ý nghĩa:** chiếu về $W$ không làm tăng khoảng cách tới điểm nào của $W$.
- **Ghi chú diễn giả:** Trong ví dụ quả cầu, $\langle\theta-\pi,u-\pi\rangle\approx0{,}0858-0{,}2071=-0{,}1213\le0$. Lộ trình phác thảo. Phần (b) suy ra từ (a): viết $\theta-u=(\theta-\pi)+(\pi-u)$, khai triển bình phương; số hạng chéo $2\langle\theta-\pi,\pi-u\rangle$ không âm theo (a), bỏ nó được bất đẳng thức thứ nhất. Phần (a): vì $W$ lồi, đoạn từ $\pi$ tới $u$ nằm trong $W$; hàm $\alpha\mapsto\lVert\pi+\alpha(u-\pi)-\theta\rVert^2$ nhỏ nhất tại $\alpha=0$, nên đạo hàm phải tại $0$, bằng $-2\langle\theta-\pi,u-\pi\rangle$, không âm. Tính duy nhất ở (a) và tính không giãn của phép chiếu được chứng minh ở Phụ lục A. Bổ đề là công cụ cho bước một của chứng minh chính: bước chiếu không làm mất phần tiến về phía một điểm so sánh trong $W$. Điều kiện $u\in W$ không bỏ được. Nguồn: ghi chú Bài 05, §5, Bổ đề 05.8, chứng minh phác thảo, đoạn sau; Phụ lục A; UML §14.4.1.
- **Lý do / nối:** công cụ của Mệnh đề 05.13 → oracle.
- **Mục tiêu / nguồn:** 1; Bổ đề 05.8.

#### `3-03` Oracle gradient ngẫu nhiên — định nghĩa, ví dụ · 2,5 phút
- **Mặt trang:**
  - **Định nghĩa 05.10.** Lần rút $\xi_1,\xi_2,\ldots$ độc lập, cùng phân bố $P_\xi$; gradient ngẫu nhiên (stochastic gradient) $\varphi(w,\xi)$ có trung bình $\psi(w)=\mathbb E_\xi\varphi(w,\xi)$.
  - $(\varphi,P_\xi)$ là oracle gradient ngẫu nhiên (stochastic gradient oracle) với hằng số $G$ khi, cho mọi $w\in W$:
  - (G1) oracle không chệch: $\psi(w)\in\partial F(w)$; (G2) mô-men bậc hai bị chặn: $\mathbb E_\xi\lVert\varphi(w,\xi)\rVert^2\le G^2$.
  - **Ví dụ 05.5.** Mẫu của Ví dụ 05.1, $i\in\{1,2,3\}$ rút đều, $\varphi(w,i)=2(\langle w,x_i\rangle-y_i)x_i$: $\psi=\nabla L_S$.
- **Ghi chú diễn giả:** (G1) và (G2) là mệnh đề tất định về từng $w\in W$. Khai triển bình phương như câu ôn nhanh 3, với số hạng chéo có kì vọng $0$, cho $\mathbb E_\xi\lVert\varphi\rVert^2=\lVert\psi\rVert^2+\mathbb E_\xi\lVert\varphi-\psi\rVert^2$, nên (G2) kéo theo $\lVert\psi(w)\rVert\le G$. Trường hợp chính: $F=L_S$, chỉ số rút đều có hoàn lại, $\varphi(w,i)$ là một dưới gradient của hàm lỗi trên quan sát $i$; khi đó $\psi\in\partial L_S$ theo Mệnh đề 05.3(b). Cách xáo trộn lại sau mỗi vòng qua dữ liệu (random reshuffling) không thỏa định nghĩa: chỉ số rút không hoàn lại trong mỗi vòng (epoch), nên các lần rút không độc lập; với $m=2$, lần rút thứ hai của mỗi vòng đã xác định. Cận tổng quát là $2(BC_x+C_y)C_x$ với $C_x$, $C_y$ là cận của $\lVert x\rVert$, $\lvert y\rvert$; ở đây $B=C_x=C_y=1$. Ngoài quả cầu, cận hỏng: tại $w=(10,0)$, $\varphi(w,1)=(18,0)$, chuẩn $18>4$; vì vậy $G=4$ là cận cho trường hợp xấu nhất trên $W$. Nguồn: ghi chú Bài 05, §6, Định nghĩa 05.10 và các đoạn sau, Ví dụ 05.5.
- **Lý do / nối:** đối tượng ngẫu nhiên của bài, ví dụ bằng số ngay trên trang → hai thuật toán.
- **Mục tiêu / nguồn:** 2; Định nghĩa 05.10, Ví dụ 05.5.

#### `3-04` Hạ gradient và hạ gradient ngẫu nhiên có chiếu — thuật toán (Thuật toán 05.9, 05.11) · 2 phút
- **Mặt trang** {{`grid2`: hai thẻ giả mã, tiêu đề thẻ là tên thuật toán}}:
  - **Thuật toán 05.9.** Hạ gradient có chiếu: $v_t=v(w_t)\in\partial F(w_t)$, $w_{t+1}=\operatorname{proj}_W(w_t-\eta v_t)$.
  - **Thuật toán 05.11.** Hạ gradient ngẫu nhiên có chiếu: rút $\xi_t\sim P_\xi$, độc lập với các lần rút trước;
  - $g_t=\varphi(w_t,\xi_t)$, $w_{t+1}=\operatorname{proj}_W(w_t-\eta g_t)$.
  - Chung: $w_1\in W$ tất định, $\eta>0$ hằng, $T$ chọn trước, $t=1,\ldots,T$.
  - Đầu ra: điểm lặp trung bình (averaged iterate) $\bar w_T=\frac1T\sum_{t=1}^Tw_t$, thuộc $W$ vì $W$ lồi.
  - Chi phí trên $L_S$: vòng GD tốn $m$ gradient trên một quan sát, vòng SGD tốn một.
- **Ghi chú diễn giả:** Khi $v_t$ là dưới gradient, Thuật toán 05.9 vẫn gọi là hạ gradient (subgradient descent). Mỗi thuật toán dừng sau đúng $T$ vòng; với SGD, $T$ và $\eta$ chọn trước khi chạy, và $\eta$ được phép phụ thuộc $T$. Điểm lặp $w_t$ chỉ phụ thuộc $\xi_1,\ldots,\xi_{t-1}$, nên $\bar w_T$ phụ thuộc $\xi_1,\ldots,\xi_{T-1}$; đầu ra phụ thuộc cả tập huấn luyện và các lần rút, viết $\bar w_T(S;\xi)$, như $A(S;\xi)$ với lô nhỏ ở Bài 01. Với $W=\mathbb R^p$, phép chiếu biến mất và thuật toán là SGD không chiếu. Với lớp tuyến tính, một gradient trên một quan sát và một phép chiếu lên quả cầu đều tốn cỡ $p$ phép tính. Nguồn: ghi chú Bài 05, §6, Thuật toán 05.9, 05.11 và các đoạn sau.
- **Lý do / nối:** hai thuật toán chung một phép cập nhật; GD là trường hợp oracle tất định → chạy tay ba bước.
- **Mục tiêu / nguồn:** 4; Thuật toán 05.9, 05.11.

#### `3-05` Ví dụ: ba bước hạ gradient ngẫu nhiên có chiếu — ví dụ (Ví dụ 05.6), hình F3 · 3,5 phút
- **Mặt trang** {{`grid2`: chữ trái, hình F3 phải}}:
  - Oracle của Ví dụ 05.5 trên quả cầu đơn vị: $\lVert\varphi(w,i)\rVert\le2(1+1)\cdot1=4$, nên (G2) đúng với $G=4$.
  - $w_1=0$, $\eta=0{,}5$; chỉ số rút được $i_1=1$, $i_2=2$; $w_2=(1,0)$, $L_S(w_2)\approx0{,}4533$.
  - $w_2-\eta g_2=(1,-1)$ chiếu thành $w_3\approx(0{,}7071;-0{,}7071)$, $L_S(w_3)\approx0{,}0639$.
  - Bảng: $i_3$ | $1$ | $2$ | $3$; $L_S(w_4)$ | $0{,}0710$ | $0{,}1021$ | $0{,}0694$.
  - $\mathbb EL_S(w_4)\approx0{,}0808$; bước GD từ $w_3$: $L_S\approx0{,}0614$; $\min_WL_S\approx0{,}06112$ tại $w^*\approx(0{,}7473;-0{,}6645)$.
  - **Diễn giải:** cả ba lựa chọn làm $L_S$ tăng từ $0{,}0639$, nên tăng cả theo kì vọng; bước GD làm $L_S$ giảm.
- **Ghi chú diễn giả:** Bước một: $g_1=\varphi(0,1)=(-2,0)$, $w_1-\eta g_1=(1,0)$ đã nằm trong $W$. Bước hai: $g_2=2(0+1)(0,1)=(0,2)$, điểm $(1,-1)$ có chuẩn $1{,}4142>1$, chiếu theo công thức của quả cầu. Ở bước ba, với $i_3=1$ và $i_3=2$, điểm chưa chiếu có chuẩn $1{,}2247$ nên bị chiếu; với $i_3=3$, điểm có chuẩn $0{,}9899$ và giữ nguyên. Bước GD dùng $\nabla L_S(w_3)\approx(-0{,}2518;0{,}1198)$, điểm chưa chiếu có chuẩn $1{,}1324$. Đọc hình: đường đứt là đường mức $L_S=0{,}0639$ qua $w_3$; ba điểm $w_4$ của SGD nằm ngoài đường mức, điểm của GD nằm trong. Vì $\lVert x_i\rVert=1$ và $\lvert y_i\rvert\le1$, mỗi gradient trên một quan sát có chuẩn không quá $2(\lVert w\rVert+1)\le4$ trên $W$. Nghiệm tối ưu $w^*$ nằm trên biên của $W$, tìm bằng điều kiện $(M+\kappa I)w^*=c$ với $\kappa\approx0{,}1350$ (Phụ lục D); nghiệm bình phương tối thiểu không ràng buộc $(1{,}06;-0{,}92)$ có chuẩn $1{,}404>1$, nên đối tượng so sánh là giá trị nhỏ nhất trên $W$, không phải trên $\mathbb R^2$. Nguồn: ghi chú Bài 05, §6, Ví dụ 05.6; Phụ lục D.
- **Lý do / nối:** chạy tay thuật toán trước mọi cận; trả lời bằng số câu "một bước SGD có thể làm $L_S$ tăng" của trang dẫn nhập → cần trung bình khi biết lịch sử.
- **Mục tiêu / nguồn:** 1, 4; Ví dụ 05.6.

#### `3-06` Tính không chệch có điều kiện — trực quan, kết quả (Bổ đề 05.12) · 2,5 phút
- **Mặt trang:**
  - **Kí hiệu:** lịch sử (history, filtration) $\mathcal F_t=\sigma(\xi_1,\ldots,\xi_t)$; $\mathcal F_0$ tầm thường.
  - **Trực quan.** Biết lịch sử $\mathcal F_{t-1}$: $w_t$ cố định, còn $\xi_t$ vẫn có phân bố $P_\xi$.
  - **Bổ đề 05.12.** **Giả thiết:** $(\varphi,P_\xi)$ thỏa (G1), (G2); $w_t$, $g_t$ của Thuật toán 05.11; $u\in W$ cố định. **Bảo đảm:** với mọi $t\ge1$,
  - (a) $w_t\in W$, đo được theo $(\xi_1,\ldots,\xi_{t-1})$; (b) hầu chắc chắn (almost surely):
  - $$\mathbb E[g_t\mid\mathcal F_{t-1}]=\psi(w_t)\in\partial F(w_t),\qquad\mathbb E\big[\lVert g_t\rVert^2\mid\mathcal F_{t-1}\big]\le G^2;$$
  - (c) $\mathbb E\lVert g_t\rVert^2\le G^2$ và $\mathbb E\langle g_t,w_t-u\rangle=\mathbb E\langle\psi(w_t),w_t-u\rangle$.
- **Ghi chú diễn giả:** Kì vọng có điều kiện theo $\mathcal F_{t-1}$ là trung bình theo lần rút ở bước $t$ khi $t-1$ lần rút đầu đã biết. Phần (a) là quy nạp: $w_1$ tất định, và $w_{t+1}$ là hàm của $w_t$ và $\xi_t$. Phần (b) dùng tính độc lập của $\xi_t$ với các lần rút trước, rồi (G1), (G2) tại điểm cố định $w_t\in W$. Phần (c) là dạng không điều kiện, đúng dạng dùng trong chứng minh định lý chính. Hướng $g_t$ của mỗi bước SGD, tính trung bình khi biết lịch sử, là dưới gradient $\psi(w_t)$, như hướng của GD. Ghi chú chứng minh cho $\Xi$ hữu hạn; trường hợp tổng quát ở Phụ lục B. Nguồn: ghi chú Bài 05, §6, Bổ đề 05.12 và đoạn trước, đoạn sau Định nghĩa 05.10.
- **Lý do / nối:** câu hỏi của trang trước (một bước có thể làm $L_S$ tăng) có câu trả lời theo trung bình có điều kiện → kỹ thuật.
- **Mục tiêu / nguồn:** 2; Bổ đề 05.12.

#### `3-07` Kì vọng có điều kiện theo lịch sử — kỹ thuật (cơ chế chứng minh Bổ đề 05.12(c)) · 2,5 phút
- **Mặt trang:**
  - **Kỹ thuật.** Với $a_t$ đã biết sau $t-1$ lần rút, tức đo được theo $\mathcal F_{t-1}$:
  - $$\mathbb E\langle g_t,a_t\rangle=\mathbb E\big\langle\mathbb E[g_t\mid\mathcal F_{t-1}],a_t\big\rangle=\mathbb E\langle\psi(w_t),a_t\rangle.$$
  - Đẳng thức đầu: tính chất tháp, lấy ra đại lượng đã biết.
  - Đẳng thức sau: $\xi_t$ độc lập với $\mathcal F_{t-1}$, nên trung bình theo $\xi_t$ là $\psi(w_t)$.
  - Dùng khi gradient ngẫu nhiên nhân với một đại lượng đã biết trước bước $t$; ở đây $a_t=w_t-u$.
- **Ghi chú diễn giả:** Với $\Xi$ hữu hạn và $P_\xi(k)>0$, cơ chế là một tổng kép: cố định lịch sử $k_{1:t-1}$, điểm lặp $w_t$ bằng một điểm cố định, tổng theo lần rút mới cho $\psi$ tại điểm đó; rồi lấy trung bình theo lịch sử với trọng số $\Pr(k_{1:t-1})$. Bài tập 05.3(a) viết tổng kép này cho $t=2$. Với $\Xi$ tổng quát, đẳng thức sau là bổ đề đóng băng (freezing lemma), phát biểu ở Phụ lục B; tính hữu hạn của các kì vọng đến từ cận $\mathbb E\lVert w_t-u\rVert^2<\infty$. Khi lần rút mới phụ thuộc lịch sử, đẳng thức sau hỏng; mạch 5 có một ví dụ. Kỹ thuật này trở lại ở các bài về tính ổn định của SGD và về gradient chính sách. Nguồn: ghi chú Bài 05, chứng minh Bổ đề 05.12 (trường hợp $\Xi$ hữu hạn); Phụ lục B; UML §14.3.
- **Lý do / nối:** kỹ thuật dùng lại qua học phần, trang riêng ở nơi dùng lần đầu → bài tập của cụm.
- **Mục tiêu / nguồn:** 2; chứng minh Bổ đề 05.12.

#### `3-08` Bài tập: kì vọng của tích vô hướng ở bước thứ hai — bài tập (Bài tập 05.3(b)), lời giải trên mặt trang · 3,5 phút (1 phút tự làm)
- **Mặt trang:**
  - Thiết lập của Ví dụ 05.6, $u=w^*$; $i_1$, $i_2$ rút đều có hoàn lại trên $\{1,2,3\}$.
  - **Câu hỏi:** tính ba giá trị có thể của $w_2$ và $\psi(w_2)$. Tính $\mathbb E\langle g_2,w_2-u\rangle$ bằng cách liệt kê chín cặp $(i_1,i_2)$ đồng khả năng,
  - và bằng vế phải của Bổ đề 05.12(c). Tính thêm $\mathbb EL_S(w_2)$.
  - `[f]` **Lời giải:** $w_2=(1,0);\ (0,-1);\ 0$, với $\psi(w_2)\approx(0{,}24;0{,}9867);\ (-0{,}9867;-0{,}4267);\ (-\tfrac23,\tfrac23)$.
  - `[f]` Bảng $\langle g_2,w_2-u\rangle$, hàng $i_1$, cột $i_2$: $0;\ 1{,}3289;\ 0{,}8198$ / $1{,}4947;\ 0;\ 1{,}1469$ / $1{,}4947;\ 1{,}3289;\ 0$.
  - `[f]` Trung bình chín ô $\approx0{,}8460$, bằng trung bình ba hàng $0{,}7162;\ 0{,}8805;\ 0{,}9412$; $\mathbb EL_S(w_2)\approx0{,}5556$.
- **Ghi chú diễn giả:** Câu chữ của bài viết "bằng vế phải của (a)"; phần (a) là đẳng thức $\mathbb E\langle g_2,w_2-u\rangle=\mathbb E\langle\psi(w_2),w_2-u\rangle$, tức Bổ đề 05.12(c) với $t=2$. Bước một: $g_1=-2y_{i_1}x_{i_1}$, nên $w_1-\eta g_1=y_{i_1}x_{i_1}$, có chuẩn không quá $1$. Với phần dư $r_i=\langle w_2,x_i\rangle-y_i$, $\psi(w_2)=\tfrac23\sum_ir_ix_i$. Đường chéo bằng $0$: vì $2\eta\lVert x_i\rVert^2=1$, bước thứ nhất đưa phần dư của chính quan sát $i_1$ về $0$. Ô $(1,2)$ là vế trái $1{,}3289$ của bất đẳng thức một bước ở mạch 4. Trung bình theo hàng là $\langle\psi(w_2),w_2-u\rangle$ của từng giá trị $w_2$. Kiểm tra: bất đẳng thức dưới gradient đòi $\mathbb E\langle\psi(w_2),w_2-u\rangle\ge\mathbb EL_S(w_2)-L_S(u)\approx0{,}4944$, và $0{,}8460$ thỏa. Nguồn: tệp bài tập, Bài tập 05.3(a), (b); ghi chú Bài 05, Ví dụ 05.6.
- **Lý do / nối:** bài tập của cụm: kiểm Bổ đề 05.12(c) bằng liệt kê trên dữ liệu thật của ví dụ → mạch 4.
- **Mục tiêu / nguồn:** 2; Bài tập 05.3(b).

### Mạch 4. Bất đẳng thức một bước và cận kì vọng (11 trang, 30 phút)

#### `4-00` 4. Bất đẳng thức một bước và cận kì vọng — tiêu đề mạch, điểm vào mạch 4 · 0,5 phút
- **Mặt trang:** "4."; h2 "Bất đẳng thức một bước và cận kì vọng"; `p.strand-lead` (bảng mạch, 23 âm tiết); `p.strand-keys`: "bất đẳng thức một bước · tổng triệt tiêu · điểm lặp trung bình · độ dài bước".
- **Ghi chú diễn giả:** Bổ đề phép chiếu và bổ đề lịch sử là hai công cụ; chứng minh chính ghép chúng với tính lồi. Bất đẳng thức một bước là một khẳng định tất định về một bước, không dùng xác suất. Cộng theo các bước cho một tổng triệt tiêu, lấy kì vọng đổi gradient ngẫu nhiên thành dưới gradient, và tính lồi chuyển cận sang điểm lặp trung bình. Cận thu được có hai số hạng ngược chiều nhau theo độ dài bước; cân hai số hạng cho độ dài bước tỉ lệ với một chia căn bậc hai của số vòng lặp và trả lời câu hỏi mở đầu bằng số. Nguồn: ghi chú Bài 05, §7.
- **Lý do / nối:** mạch 3 → bất đẳng thức một bước.
- **Mục tiêu / nguồn:** 1, 3; §7.

#### `4-01` Bất đẳng thức một bước — trực quan, kết quả (Mệnh đề 05.13) · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Một bước không chiếu, với $u\in W$:
  - $$\lVert w-\eta g-u\rVert^2=\lVert w-u\rVert^2-2\eta\langle g,w-u\rangle+\eta^2\lVert g\rVert^2.$$
  - Số hạng thứ hai kéo về phía $u$ khi $\langle g,w-u\rangle>0$; số hạng $\eta^2\lVert g\rVert^2$ có mặt cả khi $g$ là gradient đúng.
  - **Mệnh đề 05.13.** **Giả thiết:** $W$ khác rỗng, đóng, lồi; $w,g\in\mathbb R^p$, $\eta>0$, $w^+=\operatorname{proj}_W(w-\eta g)$; $u\in W$.
  - **Bảo đảm:** tất định, không dùng tính lồi của hàm mục tiêu hay xác suất; dấu bằng khi $W=\mathbb R^p$:
  - $$\langle g,w-u\rangle\le\frac{\lVert w-u\rVert^2-\lVert w^+-u\rVert^2}{2\eta}+\frac\eta2\lVert g\rVert^2.$$
- **Ghi chú diễn giả:** Đẳng thức đầu là khai triển $\lVert a-a'\rVert^2$ với $a=w-u$, $a'=\eta g$. Đọc bất đẳng thức: vế trái lớn khi bước đi theo hướng về $u$; khi đó khoảng cách tới $u$ giảm, trừ phần $\tfrac\eta2\lVert g\rVert^2$. Phần này tỉ lệ với $\eta$ sau khi chia cho $2\eta$, nên bước dài làm nó lớn. Ở bước thứ hai của ví dụ ba quan sát, $\langle g_2,w_2-w^*\rangle\approx1{,}3289$ và $\tfrac\eta2\lVert g_2\rVert^2=1$: hai số cùng cỡ, nên một bước có thể không đưa điểm lặp lại gần $w^*$. Mệnh đề không cần $g$ là gradient của hàm nào; nó đúng trên từng quỹ đạo của SGD. Nguồn: ghi chú Bài 05, §7, đoạn mở, Mệnh đề 05.13 và câu sau $\square$.
- **Lý do / nối:** trọng tâm của bài; trực quan bằng khai triển trước phát biểu; ví dụ bằng số là bước thứ hai của 3-05 → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 1; §7, Mệnh đề 05.13.

#### `4-02` Ý tưởng chứng minh: bất đẳng thức một bước — ý tưởng chứng minh, ví dụ (Ví dụ 05.7) · 2,5 phút
- **Mặt trang:**
  - **Bước 1 (phép chiếu).** Bổ đề 05.8(b) với $\theta=w-\eta g$: $\lVert w^+-u\rVert^2\le\lVert w-\eta g-u\rVert^2$; cần $u\in W$.
  - **Bước 2.** Khai triển vế phải, chuyển $2\eta\langle g,w-u\rangle$ sang vế trái, chia cho $2\eta>0$.
  - Bỏ $u\in W$ hoặc tính lồi của $W$: Bước 1 hỏng.
  - **Ví dụ.** Bước thứ hai của Ví dụ 05.6, $u=w^*$: vế trái $\approx1{,}3289$; $\lVert w_2-w^*\rVert^2\approx0{,}5053$; $\tfrac\eta2\lVert g_2\rVert^2=1$.
  - Không chiếu: vế phải $0{,}5053-0{,}1764+1=1{,}3289$; có chiếu: $0{,}5053-0{,}0034+1\approx1{,}5019$.
- **Ghi chú diễn giả** (~170 âm tiết): Bước 1 là chỗ duy nhất dùng phép chiếu, tính đóng và tính lồi của $W$, và điều kiện $u\in W$; Bước 2 là đại số. Khi $W=\mathbb R^p$, $w^+=w-\eta g$ và Bước 1 là đẳng thức, nên cả mệnh đề là đẳng thức. Bài tập 05.2(b) dựng hai trường hợp hỏng trên $\mathbb R$: với tập không lồi $\{-1,1\}$, điểm gần nhất có thể xa $u$ hơn chính điểm chưa chiếu; với $u=3$ ngoài $W=[-1,1]$, chiếu kéo điểm lặp ra xa $u$. Trong cả hai, bất đẳng thức của Bổ đề 05.8(b) sai. Trong ví dụ, phép chiếu đưa khoảng cách bình phương tới $w^*$ từ $0{,}1764$ (điểm chưa chiếu $(1,-1)$, cách $w^*$ khoảng $0{,}42$) xuống $0{,}0034$ ($w_3$, cách $w^*$ khoảng $0{,}0586$), nên bất đẳng thức là nghiêm ngặt: $1{,}3289<1{,}5019$. Bước thứ ba với $i_3=1$ (Bài tập 05.2(c)) đưa điểm lặp ra xa $w^*$, và bất đẳng thức vẫn đúng nhờ số hạng $\tfrac\eta2\lVert g\rVert^2$. Nguồn: ghi chú Bài 05, chứng minh Mệnh đề 05.13; Ví dụ 05.7; tệp bài tập, Bài tập 05.2.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; ví dụ của ghi chú là bước kiểm tra sau phát biểu → định lý chính.
- **Mục tiêu / nguồn:** 1; chứng minh Mệnh đề 05.13, Ví dụ 05.7.

#### `4-03` Cận kì vọng cho hạ gradient ngẫu nhiên có chiếu — trực quan, kết quả (Định lý 05.14) · 3,5 phút
- **Mặt trang:**
  - **Trực quan.** Cộng $T$ bất đẳng thức một bước: khoảng cách triệt tiêu, $\tfrac\eta2\lVert g_t\rVert^2$ cộng dồn.
  - **Định lý 05.14.** **Giả thiết:** (C) $F$ lồi, $W$ khác rỗng, đóng, lồi; $(\varphi,P_\xi)$ thỏa (G1), (G2) với hằng số $G$;
  - Thuật toán 05.11, $w_1\in W$ tất định, $\eta>0$ hằng, $T\ge1$; $u\in W$ tất định, bất kì.
  - **Bảo đảm:** theo kì vọng theo $\xi_1,\ldots,\xi_{T-1}$,
  - $$\mathbb E\big[F(\bar w_T)\big]-F(u)\le\frac{\lVert w_1-u\rVert^2}{2\eta T}+\frac{\eta G^2}{2}.$$
  - Đại lượng được chặn: độ chênh tối ưu của $F$ tại $\bar w_T$.
- **Ghi chú diễn giả:** $F$ là hàm mà oracle không chệch; khi chỉ số rút từ $S$, đó là $L_S$. Cận đúng với mọi $u\in W$, kể cả khi $F$ không đạt giá trị nhỏ nhất trên $W$, và phụ thuộc chiều $p$, cỡ mẫu $m$ chỉ qua $G$ và $\lVert w_1-u\rVert$. Số hạng thứ nhất giảm như $1/T$; số hạng thứ hai tỉ lệ với $\eta$ và không giảm theo $T$. Với $u$ là một nghiệm tối ưu và $\eta$ cố định, cận giảm về mức $\eta G^2/2$; muốn cận về $0$, cần chọn $\eta$ theo $T$. Một bước có thể làm $F$ tăng, như ở ví dụ ba quan sát; định lý chỉ nói về trung bình các điểm lặp, theo kì vọng. Nguồn: ghi chú Bài 05, §7, Định lý 05.14 và đoạn sau, câu sau $\square$.
- **Lý do / nối:** kết quả chính của bài, trực quan trên cùng trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 1; Định lý 05.14.

#### `4-04` Ý tưởng chứng minh: cận kì vọng — ý tưởng chứng minh · 4 phút
- **Mặt trang:**
  - **Bước 1.** Mệnh đề 05.13 tại mỗi $t$, trên từng quỹ đạo; cần $W$ đóng, lồi và $u\in W$.
  - **Bước 2.** Tổng triệt tiêu, $\Delta_t=\lVert w_t-u\rVert^2$: $\sum_t(\Delta_t-\Delta_{t+1})=\Delta_1-\Delta_{T+1}\le\Delta_1$.
  - **Bước 3** ((G1), qua Bổ đề 05.12(c)): $\mathbb E\langle g_t,w_t-u\rangle=\mathbb E\langle\psi(w_t),w_t-u\rangle\ge\mathbb E\big[F(w_t)-F(u)\big]$.
  - **Bước 4** ((G2)): $\mathbb E\lVert g_t\rVert^2\le G^2$, chỉ ở số hạng $\tfrac\eta2\lVert g_t\rVert^2$.
  - **Bước 5** ((C)): bất đẳng thức lồi hữu hạn $F(\bar w_T)\le\frac1T\sum_tF(w_t)$; chia cho $T$.
- **Ghi chú diễn giả** (~200 âm tiết): Lộ trình: một bước, tổng triệt tiêu, kì vọng, tính lồi. Bước 1 và Bước 2 là tất định, đúng với mỗi dãy giá trị cụ thể của các lần rút. Bất đẳng thức then chốt nằm ở Bước 3: theo kì vọng có điều kiện khi biết lịch sử, $g_t$ có thể thay bằng $\psi(w_t)$, và vì $\psi(w_t)$ là dưới gradient tại $w_t$, bất đẳng thức dưới gradient với điểm $u$ cho $\langle\psi(w_t),w_t-u\rangle\ge F(w_t)-F(u)$. Bước này chỉ dùng (G1); tính lồi của $F$ là điều kiện để (G1) thỏa được, vì hàm lồi hữu hạn có dưới vi phân khác rỗng. Lấy kì vọng ở Bước 2 và dùng Bước 3, 4: $\sum_t\mathbb E[F(w_t)-F(u)]\le\Delta_1/(2\eta)+\eta TG^2/2$. Bước 5 dùng tính lồi của $F$ trên từng quỹ đạo và tính lồi của $W$ để $\bar w_T\in W$. Mỗi giả thiết vào đúng một bước, nên bỏ một giả thiết làm hỏng đúng bước đó: tính lồi ở Bước 3 và 5, cận mô-men bậc hai ở Bước 4, tính không chệch ở Bước 3. Nguồn: ghi chú Bài 05, chứng minh Định lý 05.14; UML §14.1.1, §14.3.
- **Lý do / nối:** trang ý tưởng chứng minh riêng, chỗ dùng từng giả thiết → kỹ thuật tổng triệt tiêu.
- **Mục tiêu / nguồn:** 1; chứng minh Định lý 05.14.

#### `4-05` Tổng triệt tiêu và trung bình các điểm lặp — kỹ thuật · 2 phút
- **Mặt trang:**
  - **Kỹ thuật.** Mỗi bước có $c_t\le a_t-a_{t+1}+b_t$ với $a_t\ge0$. Cộng theo $t$:
  - $$\sum_{t=1}^Tc_t\le a_1-a_{T+1}+\sum_{t=1}^Tb_t\le a_1+\sum_{t=1}^Tb_t.$$
  - Các số hạng giữa triệt tiêu; chỉ còn số hạng đầu $a_1$.
  - $F$ lồi và $c_t\ge F(w_t)-F(u)$: chia cho $T$ được $F(\bar w_T)-F(u)\le\frac1T\sum_tc_t$.
  - Dùng khi bất đẳng thức một bước là hiệu của một đại lượng không âm cộng một sai số.
- **Ghi chú diễn giả:** Trong Định lý 05.14, $a_t=\Delta_t/(2\eta)$ là khoảng cách bình phương tới điểm so sánh, $b_t=\tfrac\eta2\lVert g_t\rVert^2$, và $c_t=\langle g_t,w_t-u\rangle$; bất đẳng thức $c_t\ge F(w_t)-F(u)$ chỉ đúng theo kì vọng, qua kỹ thuật kì vọng có điều kiện. Cận không phụ thuộc quỹ đạo đi qua đâu, chỉ phụ thuộc khoảng cách ban đầu. Đầu ra là trung bình các điểm lặp chính vì bất đẳng thức lồi hữu hạn chuyển trung bình các giá trị $F(w_t)$ sang giá trị tại trung bình. Cùng khuôn cho Hệ quả 05.16 (một quỹ đạo, không kì vọng), cho độ dài bước thay đổi ở Nhận xét 05.17 (trọng số $\eta_t$) và cho Bài tập 05.11. Kỹ thuật trở lại ở các bài về tính ổn định của SGD và về hối tiếc. Nguồn: ghi chú Bài 05, chứng minh Định lý 05.14, Bước 2 và 5; Phụ lục C.
- **Lý do / nối:** kỹ thuật dùng lại qua học phần, trang riêng ở nơi dùng lần đầu → chọn độ dài bước.
- **Mục tiêu / nguồn:** 1; chứng minh Định lý 05.14.

#### `4-06` Độ dài bước tối ưu của cận — trực quan, ví dụ, hình F4 · 3 phút
- **Mặt trang** {{`grid2`: chữ trái, hình F4 phải}}:
  - **Trực quan.** Với $\lVert w_1-u\rVert=R$: số hạng $R^2/(2\eta T)$ giảm theo $\eta$, số hạng $\eta G^2/2$ tăng theo $\eta$.
  - Với $\eta$ cố định, vế phải giảm về $\eta G^2/2$ khi $T$ tăng.
  - Tổng nhỏ nhất khi hai số hạng bằng nhau: $\eta^*=R/(G\sqrt T)$, cho $RG/\sqrt T$.
  - **Ví dụ.** $R=1$, $G=4$, $T=1600$: $\eta^*=0{,}00625$, vế phải $0{,}1$; $\eta=2\eta^*$ hoặc $\eta^*/2$: $0{,}125$; $\eta=10\eta^*$: $0{,}505$.
  - **Diễn giải:** lệch hai lần làm vế phải tăng $25\%$; lệch mười lần, gấp $5{,}05$ lần.
  - {{hình F4 bên phải}}
- **Ghi chú diễn giả:** Với $\eta=\gamma\eta^*$, hai số hạng là $RG/(2\gamma\sqrt T)$ và $\gamma RG/(2\sqrt T)$, nên vế phải bằng $\tfrac{RG}{\sqrt T}\cdot\tfrac{\gamma+1/\gamma}2$; thừa số này bằng $1$ tại $\gamma=1$, bằng $1{,}25$ tại $\gamma=2$ hoặc $\tfrac12$, và $5{,}05$ tại $\gamma=10$. Đọc hình: trục ngang là độ dài bước theo thang lôgarit; đường giảm là số hạng khoảng cách, đường tăng là số hạng $\eta G^2/2$, đường cong trên là tổng, đáy tại $\eta^*$. Độ dài bước $0{,}5$ của ví dụ ba quan sát cho vế phải $4{,}000625$ khi $T=1600$, lớn hơn cả cận $4$ của mọi hàm lỗi trên quả cầu, nên không cho thông tin. Số liệu là của oracle rút một quan sát trên quả cầu đơn vị. Nguồn: ghi chú Bài 05, Ví dụ 05.8, Bước 3, 4; đoạn sau Hệ quả 05.15.
- **Lý do / nối:** trực quan và ví dụ bằng số trước phát biểu của hệ quả → Hệ quả 05.15.
- **Mục tiêu / nguồn:** 3; Ví dụ 05.8.

#### `4-07` Độ dài bước theo số vòng lặp — kết quả (Hệ quả 05.15) · 2,5 phút
- **Mặt trang:**
  - **Hệ quả 05.15.** **Giả thiết:** như Định lý 05.14; $G>0$, $R>0$, $\eta=R/(G\sqrt T)$. **Bảo đảm:** theo kì vọng theo $\xi$,
  - (a) với mọi $u\in W$ thỏa $\lVert w_1-u\rVert\le R$: $$\mathbb EF(\bar w_T)-F(u)\le\frac{RG}{\sqrt T};$$
  - (b) cùng cận cho $\mathbb EF(\bar w_T)-F_R$, với $F_R=\inf\{F(u):u\in W,\ \lVert u-w_1\rVert\le R\}$;
  - (c) với $\epsilon>0$, $T\ge R^2G^2/\epsilon^2$ đủ để các vế trái ở (a), (b) không quá $\epsilon$.
  - Vì $\eta$ phụ thuộc $T$, $T$ được cố định trước khi chạy.
- **Ghi chú diễn giả:** Phần (b) có hai trường hợp riêng: nếu $F$ có nghiệm tối ưu $w^*$ trên $W$ với $\lVert w_1-w^*\rVert\le R$ thì cận đúng cho $F(w^*)$; nếu mọi $u\in W$ thỏa $\lVert w_1-u\rVert\le R$, chẳng hạn $W$ là quả cầu bán kính $B$ và $w_1=0$ với $R=B$, thì $F_R=\inf_WF$. Theo (c), muốn giảm cận một nửa, cần gấp bốn lần số vòng lặp. Độ dài bước giảm dần $\eta_t=R/(G\sqrt t)$ không cần biết $T$ trước; Nhận xét 05.17 (đọc thêm) cho cận với trung bình có trọng số, lớn hơn một thừa số cỡ $\ln T$. Nguồn: ghi chú Bài 05, §7, Hệ quả 05.15, câu sau $\square$; Nhận xét 05.17.
- **Lý do / nối:** phát biểu sau trực quan và ví dụ → ý tưởng chứng minh và số vòng lặp.
- **Mục tiêu / nguồn:** 3; Hệ quả 05.15.

#### `4-08` Ý tưởng chứng minh: độ dài bước theo số vòng lặp — ý tưởng chứng minh, ví dụ (Ví dụ 05.8) · 3 phút
- **Mặt trang:**
  - **Bước 1.** Thay $\eta$: mỗi số hạng của Định lý 05.14 không quá $RG/(2\sqrt T)$; cộng được (a).
  - **Bước 2.** Vế phải của (a) không phụ thuộc $u$: lấy cận trên đúng theo $u$ được (b).
  - **Bước 3.** $RG/\sqrt T\le\epsilon$ khi và chỉ khi $T\ge R^2G^2/\epsilon^2$: (c).
  - **Kỹ thuật.** Cân hai số hạng: $a/\eta+b\eta\ge2\sqrt{ab}$, dấu bằng tại $\eta=\sqrt{a/b}$.
  - **Ví dụ.** Oracle của Ví dụ 05.5, $w_1=0$: $R=1$, $G=4$; $\epsilon=0{,}2;\ 0{,}1;\ 0{,}05$ cho $T\ge400;\ 1600;\ 6400$.
  - $T=1600$, $\eta=0{,}00625$: $\mathbb E_\xi L_S(\bar w_{1600})\le\min_WL_S+0{,}1=0{,}16112$.
- **Ghi chú diễn giả** (~150 âm tiết): Ở Bước 1, với $\lVert w_1-u\rVert\le R$, số hạng thứ nhất là $\lVert w_1-u\rVert^2/(2\eta T)\le R^2G\sqrt T/(2RT)=RG/(2\sqrt T)$, và số hạng thứ hai bằng đúng $RG/(2\sqrt T)$. Kỹ thuật cân hai số hạng là bất đẳng thức giữa trung bình cộng và trung bình nhân cho $a/\eta$ và $b\eta$, với $a=R^2/(2T)$, $b=G^2/2$ (Bài tập 05.4(a)); nó chỉ dùng ở đây. Trong ví dụ, mọi $u$ thuộc quả cầu đơn vị có $\lVert w_1-u\rVert\le1$, nên theo (b), đối tượng so sánh là giá trị nhỏ nhất $0{,}06112$ trên $W$. Bảo đảm là theo kì vọng, cho điểm lặp trung bình sau $1600$ bước. Với độ dài bước giảm dần $\eta_t=1/(4\sqrt t)$, Nhận xét 05.17 cho vế phải $0{,}2281$ thay cho $0{,}1$, vì $\sum_t\eta_t^2$ tăng như $\ln T$. Nguồn: ghi chú Bài 05, chứng minh Hệ quả 05.15; Ví dụ 05.8, Bước 1, 2; Nhận xét 05.17; Phụ lục C.
- **Lý do / nối:** trang ý tưởng chứng minh riêng, ví dụ của ghi chú là bước kiểm tra → GD và câu hỏi thực hành.
- **Mục tiêu / nguồn:** 3; chứng minh Hệ quả 05.15, Ví dụ 05.8.

#### `4-09` Hạ gradient có chiếu và hồi quy logistic — kết quả (Hệ quả 05.16), ví dụ (Ví dụ 05.9) · 3,5 phút
- **Mặt trang:**
  - **Hệ quả 05.16.** **Giả thiết:** (C); $v(w)\in\partial F(w)$, $\lVert v(w)\rVert\le G$ trên $W$, $G>0$; Thuật toán 05.9, $\eta=R/(G\sqrt T)$; $\lVert w_1-u\rVert\le R$.
  - **Bảo đảm:** tất định, $F(\bar w_T)-F(u)\le RG/\sqrt T$; $T\ge R^2G^2/\epsilon^2$ đủ cho mức $\epsilon$.
  - **Ví dụ 05.9.** Hồi quy logistic: $m=10^6$, $\lVert x_i\rVert\le1$, $W=\{w:\lVert w\rVert\le5\}$, $w_1=0$, $\epsilon=0{,}05$: $R=5$.
  - $\lVert\nabla_w\ell(w,(x,y))\rVert=\lVert x\rVert/(1+e^{\tilde y\langle w,x\rangle})\le1$: $G=1$; $T\ge25/0{,}0025=10^4$, $\eta=0{,}05$.
  - Chi phí: SGD tính $10^4$ gradient trên một quan sát, bằng $1\%$ một bước GD; GD tính $10^{10}$.
  - **Kết luận:** SGD: $\mathbb E_\xi L_S(\bar w_T)-\min_WL_S\le0{,}05$; GD: cùng cận, tất định.
- **Ghi chú diễn giả:** GD là trường hợp oracle tất định, $g_t=v(w_t)$. Chứng minh lặp lại Bước 1, 2, 5 của Định lý 05.14 trên quỹ đạo duy nhất; Bước 3, 4 không cần kì vọng, vì $\langle v_t,w_t-u\rangle\ge F(w_t)-F(u)$ theo bất đẳng thức dưới gradient và $\lVert v_t\rVert^2\le G^2$ theo giả thiết. Gradient của hàm lỗi logistic là $-\tilde yx/(1+e^{\tilde y\langle w,x\rangle})$, mẫu số lớn hơn $1$; gradient của $L_S$ là trung bình các véc-tơ như vậy, nên cũng có chuẩn không quá $1$. Theo các cận, GD và SGD cần cùng số vòng lặp khi $G$ như nhau, còn mỗi vòng GD trên $L_S$ tốn gấp $m$ lần. Đây là trả lời cho câu hỏi thực hành của trang dẫn nhập; so sánh là giữa hai cận trên, không đo thời gian chạy. Nguồn: ghi chú Bài 05, Hệ quả 05.16 và chứng minh; Ví dụ 05.9; §3, khối ứng dụng; đoạn cuối §10.
- **Lý do / nối:** kết quả phụ chung trang với ví dụ ứng dụng; trả lời câu hỏi mở đầu bằng số → bài tập của cụm.
- **Mục tiêu / nguồn:** 3, 4; Hệ quả 05.16, Ví dụ 05.9.

#### `4-10` Bài tập: ước lượng sai hằng số G — bài tập (Bài tập 05.4(c)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - $$Q(\eta,T)=\frac{R^2}{2\eta T}+\frac{\eta G^2}2\qquad(\lVert w_1-u\rVert=R).$$
  - **Câu hỏi:** chỉ biết một ước lượng $\hat G$ của $G$. Người dùng chọn $T=\lceil R^2\hat G^2/\epsilon^2\rceil$ và $\eta=R/(\hat G\sqrt T)$.
  - Với $R=1$, $G=4$, $\epsilon=0{,}1$, tính $T$, $\eta$ và $Q(\eta,T)$ khi $\hat G=8$ và khi $\hat G=2$. Trường hợp nào giữ được bảo đảm $\epsilon$?
  - `[f]` **Lời giải:** $\hat G=8$: $T=6400$, $\eta=0{,}0015625$, $Q=0{,}05+0{,}0125=0{,}0625\le0{,}1$.
  - `[f]` $\hat G=2$: $T=400$, $\eta=0{,}025$, $Q=0{,}05+0{,}2=0{,}25>0{,}1$.
  - `[f]` **Kết luận:** chỉ $\hat G=8$ giữ bảo đảm, với gấp $4$ lần số vòng lặp.
- **Ghi chú diễn giả:** $Q$ là vế phải của Định lý 05.14 khi $\lVert w_1-u\rVert=R$. Với $\hat G=2$, chỉ riêng số hạng $\eta G^2/2=0{,}2$ đã vượt $\epsilon$. Đánh giá thấp $G$ làm mất bảo đảm; đánh giá cao chỉ làm tăng số vòng lặp, theo thừa số $(\hat G/G)^2$. Kiểm tra: $\eta$ bằng $\eta^*(T)$ nhân $\gamma=G/\hat G$, tức $\gamma=\tfrac12$ hoặc $2$, nên theo trang độ dài bước, $Q=\tfrac{RG}{\sqrt T}\cdot1{,}25$: $\tfrac4{80}\cdot1{,}25=0{,}0625$ và $\tfrac4{20}\cdot1{,}25=0{,}25$. Phần (b) của bài: với $\eta$ cố định không phụ thuộc $T$, có $T$ đủ khi và chỉ khi $\eta<2\epsilon/G^2=0{,}0125$; $\eta=0{,}01$ cần $2500$ vòng, $\eta=0{,}00625$ cho $1600$. Nguồn: tệp bài tập, Bài tập 05.4(c), (b).
- **Lý do / nối:** bài tập của cụm độ dài bước, lời giải trên mặt trang → mạch 5 (bỏ giả thiết).
- **Mục tiêu / nguồn:** 3; Bài tập 05.4(c).

### Mạch 5. Vai trò của từng giả thiết (5 trang, 10 phút)

#### `5-00` 5. Vai trò của từng giả thiết — tiêu đề mạch, điểm vào mạch 5 · 0,5 phút
- **Mặt trang:** "5."; h2 "Vai trò của từng giả thiết"; `p.strand-lead` (bảng mạch, 22 âm tiết); `p.strand-keys`: "tính lồi · mô-men bậc hai · oracle chệch · điểm lặp cuối".
- **Ghi chú diễn giả:** Mỗi ví dụ dưới đây là một bài toán một chiều, giữ các giả thiết còn lại của Định lý 05.14 và bỏ đúng một giả thiết, hoặc đổi đầu ra từ điểm lặp trung bình sang điểm lặp cuối. Trong mỗi ví dụ, kết luận của cận sai, và chỗ hỏng là đúng bước của chứng minh nơi giả thiết đó được dùng. Ví dụ điểm lặp cuối không vi phạm cận: nó cho thấy cận chỉ nói về trung bình. Nguồn: ghi chú Bài 05, §8.
- **Lý do / nối:** mạch 4 (mỗi giả thiết vào một bước) → phản ví dụ.
- **Mục tiêu / nguồn:** 5; §8.

#### `5-01` Ví dụ: hàm mục tiêu không lồi — ví dụ (Ví dụ 05.10), phản ví dụ, hình F5 · 2,5 phút
- **Mặt trang** {{`grid2`: chữ trái, hình F5 phải}}:
  - $f(w)=\min\{(w-1)^2,\,(w+1)^2+0{,}5\}$ trên $W=[-2,2]$: $\min f=f(1)=0$; cực tiểu địa phương (local minimum) $f(-1)=0{,}5$.
  - GD theo đạo hàm của nhánh nhỏ hơn, $w_1=-1{,}5$; $G=2{,}25$, $R=2{,}5$, $T=1600$, $\eta\approx0{,}02778$.
  - Cận của Hệ quả 05.16: $RG/\sqrt T=0{,}140625$.
  - Điểm lặp tiến về $-1$: $\bar w_{1600}\approx-1{,}0056$, $f(\bar w_{1600})-\min f\approx0{,}5>0{,}140625$.
  - Từ $t=26$: $f(1)=0<f(w_t)+f'(w_t)(1-w_t)$, nên $f'(w_t)\notin\partial f(w_t)$: (G1) hỏng, Bước 3 hỏng.
- **Ghi chú diễn giả:** Hai nhánh bằng nhau tại $w=-0{,}125$; nhánh trái nhỏ hơn khi $w<-0{,}125$, và mọi điểm lặp nằm trong $[-1{,}5;-1]$. Hằng số $G=2{,}25$ là giá trị lớn nhất của $\lvert f'\rvert$ trên $W$, đạt tại $-0{,}125$ trên nhánh phải; $R=\lvert w_1-1\rvert$ với $u=1$. Trên nhánh trái, $w_{t+1}+1=(1-2\eta)(w_t+1)$, và trung bình cấp số nhân cho $\bar w_{1600}+1\approx-0{,}0056$. Với $s=w+1$, $f(w)+f'(w)(1-w)=-s^2+4s+0{,}5$, dương khi $w>-1{,}1213$, nên từ vòng $26$ đạo hàm tại điểm lặp không phải dưới gradient. Các giả thiết khác thỏa: $W$ lồi đóng, đạo hàm bị chặn. Đọc hình: đồ thị có hai đáy, $f(-1)=0{,}5$ và $f(1)=0$; các điểm lặp dừng ở đáy trái. Nguồn: ghi chú Bài 05, §8, Ví dụ 05.10.
- **Lý do / nối:** phản ví dụ thứ nhất (tính lồi) → mô-men bậc hai.
- **Mục tiêu / nguồn:** 5; Ví dụ 05.10.

#### `5-02` Ví dụ: mô-men bậc hai không bị chặn — ví dụ (Ví dụ 05.11), phản ví dụ · 2,5 phút
- **Mặt trang:**
  - $S=((1,0),(3,0))$, hàm lỗi bình phương: $F(w)=L_S(w)=5w^2$; $W=\mathbb R$, $\varphi(w,i)=2x_i^2w$, $\eta=0{,}15$, $w_1=1$.
  - GD: $w_{t+1}=-0{,}5\,w_t\to0$. SGD: $w_{t+1}=a_tw_t$, $a_t=0{,}7$ hoặc $-1{,}7$, mỗi giá trị với xác suất $\tfrac12$.
  - $\mathbb E\ln\lvert a_t\rvert\approx0{,}087>0$; theo luật số lớn (law of large numbers), $\lvert w_t\rvert\to\infty$ hầu chắc chắn.
  - $\mathbb E\lVert\varphi(w,\xi)\rVert^2=164w^2$, không bị chặn trên $\mathbb R$: (G2) hỏng, Bước 4 hỏng.
  - Chiếu lên $W=[-1,1]$: $G=\sqrt{164}\approx12{,}81$, Định lý 05.14 áp dụng.
- **Ghi chú diễn giả:** Oracle rút đều có hoàn lại, nên không chệch cho $F$; tính lồi cũng thỏa. GD dùng gradient $10w$ và $1-10\eta=-0{,}5$. Với SGD, thừa số là $1-2\eta x_i^2$, bằng $1-0{,}3=0{,}7$ hoặc $1-2{,}7=-1{,}7$. Theo luật số lớn, $\tfrac1t\ln\lvert w_{t+1}\rvert\to0{,}087$. Ngoài ra $\mathbb Ea_t^2=1{,}69$, nên $\mathbb Ew_{t+1}^2=1{,}69^t$. Cùng độ dài bước, GD hội tụ còn SGD phân kì: phương sai của gradient ngẫu nhiên tăng theo $w^2$. Sau khi chiếu, cận có ích với độ dài bước của Hệ quả 05.15: với $u=0$ và $R=1$, cận là $12{,}81/\sqrt T$. Nguồn: ghi chú Bài 05, §8, Ví dụ 05.11.
- **Lý do / nối:** phản ví dụ thứ hai (cận mô-men bậc hai) → oracle chệch và điểm lặp cuối.
- **Mục tiêu / nguồn:** 5; Ví dụ 05.11.

#### `5-03` Ví dụ: oracle chệch và điểm lặp cuối — ví dụ (Ví dụ 05.13, 05.12), hai thẻ · 2,5 phút
- **Mặt trang** {{`grid2`: thẻ trái Ví dụ 05.13, thẻ phải Ví dụ 05.12}}:
  - **Ví dụ 05.13.** $S=((1,0),(1,1))$, $L_S(w)=(w-0{,}5)^2+0{,}25$, $W=[-1,1]$; chỉ số $1$ với xác suất $0{,}9$.
  - $\psi(w)=2w-0{,}2\ne L_S'(w)=2w-1$; $\psi$ là đạo hàm của $\tilde F(w)=(w-0{,}1)^2+0{,}09$.
  - Độ dài bước của Hệ quả 05.15, $T$ tăng: $\mathbb EL_S(\bar w_T)-0{,}25\to0{,}16$; (G1) cho $L_S$ hỏng, Bước 3 hỏng.
  - **Ví dụ 05.12.** $f(w)=\lvert w\rvert$, $W=[-1,1]$, $G=1$, GD, $\eta=0{,}2$, $w_1=0{,}1$: $w_t=0{,}1;\ -0{,}1;\ 0{,}1;\ \ldots$
  - Điểm lặp cuối (last iterate): $f(w_t)=0{,}1=\eta G^2/2$ với mọi $t$.
  - Định lý 05.14 chặn $f(\bar w_T)$: $\bar w_T=0$ khi $T$ chẵn, và $0\le0{,}025/T+0{,}1$.
- **Ghi chú diễn giả:** Thẻ trái: oracle xác định hàm mục tiêu được tối thiểu hóa. Rút chỉ số theo phân bố không đều cho một oracle không chệch cho $\tilde F$, cực tiểu tại $0{,}1$; Định lý 05.14 áp dụng cho $\tilde F$, và $L_S(0{,}1)-L_S(0{,}5)=0{,}41-0{,}25=0{,}16$. Với $w\in W$, $\lvert\varphi(w,i)\rvert\le4$, nên (G2) vẫn đúng. Thẻ phải: điểm lặp cuối $w_{T+1}$ không hội tụ với độ dài bước hằng, và giá trị $f(w_t)=0{,}1$ đúng bằng số hạng $\eta G^2/2$ của cận; điểm lặp trung bình thỏa cận. Khi $T$ lẻ, $\bar w_T=0{,}1/T$, vẫn dưới cận. Tổng quát hơn, với $F(w)=\tfrac a2w^2$, độ dài bước hằng và nhiễu gradient có phương sai dương, điểm lặp cuối dao động quanh nghiệm ở một mức sàn sai số (error floor) tỉ lệ với $\eta$ khi $\eta$ nhỏ (Bài tập 05.6). Nguồn: ghi chú Bài 05, §8, Ví dụ 05.13, 05.12, đoạn cuối §8.
- **Lý do / nối:** phản ví dụ thứ ba (tính không chệch) và đầu ra khác; hai thẻ cùng trả lời "cận nói về đại lượng nào" → bài tập của cụm.
- **Mục tiêu / nguồn:** 5; Ví dụ 05.13, 05.12.

#### `5-04` Bài tập: lần rút thứ hai phụ thuộc lần thứ nhất — bài tập (Bài tập 05.3(c)), lời giải trên mặt trang · 2 phút
- **Mặt trang:**
  - **Câu hỏi:** trong thiết lập của Bài tập 05.3(b), thay lần rút thứ hai bằng $i_2=i_1$. Tính $\mathbb E\langle g_2,w_2-u\rangle$.
  - Chỉ ra giả thiết bị vi phạm và bước hỏng trong chứng minh Định lý 05.14.
  - `[f]` **Lời giải:** $2\eta\lVert x_i\rVert^2=1$, nên $g_2=0$ và $\mathbb E\langle g_2,w_2-u\rangle=0$.
  - `[f]` $i_2$ không độc lập với $i_1$: $\mathbb E[g_2\mid\mathcal F_1]=\varphi(w_2,i_1)\ne\psi(w_2)$, Bổ đề 05.12(b) hỏng.
  - `[f]` Bước 3 cần vế trái $\ge\mathbb EL_S(w_2)-L_S(u)\approx0{,}5556-0{,}06112\approx0{,}4944$.
- **Ghi chú diễn giả:** Với $i_2=i_1=i$, phép chiếu không tác động ở bước một, và phần dư của quan sát $i$ sau bước một là $(\langle w_1,x_i\rangle-y_i)(1-2\eta\lVert x_i\rVert^2)=0$, nên gradient trên chính quan sát đó bằng $0$. Đây là đường chéo của bảng chín ô. Lần rút thứ hai vẫn có phân bố đều, nhưng không độc lập với lần thứ nhất, trái với Định nghĩa 05.10 và dòng đầu của Thuật toán 05.11. Cách xáo trộn lại sau mỗi vòng qua dữ liệu cũng làm các lần rút phụ thuộc nhau. Nguồn: tệp bài tập, Bài tập 05.3(c); ghi chú Bài 05, §6, đoạn sau Định nghĩa 05.10.
- **Lý do / nối:** bài tập của cụm giả thiết: giả thiết độc lập của các lần rút, ngoài ba giả thiết (C), (G1), (G2) → mạch 6.
- **Mục tiêu / nguồn:** 2, 5; Bài tập 05.3(c).

### Mạch 6. Hạ gradient ngẫu nhiên trên rủi ro thực nghiệm và lô nhỏ (7 trang, 15 phút)

#### `6-00` 6. Hạ gradient ngẫu nhiên trên rủi ro thực nghiệm và lô nhỏ — tiêu đề mạch, điểm vào mạch 6 · 0,5 phút
- **Mặt trang:** "6."; h2 "Hạ gradient ngẫu nhiên trên rủi ro thực nghiệm và lô nhỏ"; `p.strand-lead` (bảng mạch, 25 âm tiết); `p.strand-keys`: "nguồn ngẫu nhiên riêng · sai số tối ưu thực nghiệm · xác suất cao · lô nhỏ".
- **Ghi chú diễn giả:** Hệ quả 05.15 chặn độ chênh tối ưu của một hàm $F$ bất kì theo kì vọng; với $F=L_S$, đó là sai số tối ưu thực nghiệm của Bài 04. SGD là một thuật toán ngẫu nhiên, nên đầu ra là một biến ngẫu nhiên ngay cả khi tập huấn luyện đã cố định; khung của Bài 01 cần thêm nguồn ngẫu nhiên đó. Bất đẳng thức Markov đổi bảo đảm kì vọng thành bảo đảm với xác suất cao, với một giá cụ thể. Lô nhỏ đổi hằng số $G$ của cận. Ví dụ cuối mạch tách sai số tối ưu thực nghiệm khỏi rủi ro kì vọng. Nguồn: ghi chú Bài 05, §9–§10, §13.
- **Lý do / nối:** mạch 4–5 → rủi ro thực nghiệm.
- **Mục tiêu / nguồn:** 3, 4; §9–§10.

#### `6-01` Thuật toán học có nguồn ngẫu nhiên riêng — định nghĩa (Định nghĩa 05.18) · 2 phút
- **Mặt trang:**
  - **Định nghĩa 05.18.** Thuật toán học có nguồn ngẫu nhiên riêng (randomized learning algorithm): ánh xạ $A_m:\mathcal Z^m\times\Xi\to\mathcal H$ vào lớp giả thuyết,
  - với $(s,\xi,z)\mapsto\ell(A_m(s;\xi),z)$ đo được; viết $A(S;\xi)$, $\xi\sim P_\xi$ độc lập với $S$.
  - Bảo đảm theo $\xi$ đúng với mọi $S$ cố định thì đúng theo cặp $(S,\xi)\sim D^m\otimes P_\xi$.
  - **Ví dụ.** SGD có chiếu trên $L_S$: $A(S;\xi)=\bar w_T$, $\xi=(\xi_1,\ldots,\xi_{T-1})$.
  - Lớp hàm điểm số (score function) $\{h_w:w\in W\}$, $h_w(x)=\langle w,x\rangle$, giá trị thực.
- **Ghi chú diễn giả:** Định nghĩa 01.4 là trường hợp $\Xi$ có một điểm. Xác suất trong các định nghĩa PAC của Bài 01 khi đó lấy theo cặp $(S,\xi)$ với phân bố tích $D^m\otimes P_\xi$. Ở SGD, $\xi$ là dãy $T-1$ lần rút theo phân bố của Định nghĩa 05.10, không phụ thuộc $S$; lớp gồm các hàm điểm số nhận giá trị trong $\mathbb R$ thay cho tập nhãn. Đây cũng là cách đọc $A(S;\xi)$ với lô nhỏ mà Bài 01 đã nêu. Nguồn: ghi chú Bài 05, §9, Định nghĩa 05.18 và hai đoạn sau.
- **Lý do / nối:** khung thuật toán ngẫu nhiên trước bảo đảm của SGD trên rủi ro thực nghiệm → Hệ quả 05.19.
- **Mục tiêu / nguồn:** 3; Định nghĩa 05.18.

#### `6-02` Hạ gradient ngẫu nhiên trên rủi ro thực nghiệm — kết quả (Hệ quả 05.19) · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** $\operatorname{opt}_s\ge0$, nên bất đẳng thức Markov đổi cận kì vọng thành cận xác suất.
  - **Hệ quả 05.19.** **Giả thiết:** $s=(z_1,\ldots,z_m)$ cố định; $\ell(\cdot,z)\ge0$ lồi; dưới gradient đo được $v(w,z)$, $\lVert v(w,z_i)\rVert\le G$ trên $W$;
  - $W$ khác rỗng, đóng, lồi, bị chặn; $R\ge\sup_{u\in W}\lVert w_1-u\rVert$; $i_t$ đều, có hoàn lại; $\eta=R/(G\sqrt T)$.
  - **Bảo đảm:** (a) $\mathbb E_\xi\operatorname{opt}_s(\bar w_T)\le RG/\sqrt T$ với mọi tập huấn luyện $s$;
  - (b) với $\epsilon_{\mathrm{opt}}>0$, $\delta'\in(0,1)$ (xác suất thất bại theo $\xi$, khác $\delta$ theo $S$) và $T\ge R^2G^2/(\delta'^2\epsilon_{\mathrm{opt}}^2)$:
  - $$\Pr_\xi\big[\operatorname{opt}_s(\bar w_T)\ge\epsilon_{\mathrm{opt}}\big]\le\delta'.$$
- **Ghi chú diễn giả:** Đại lượng được chặn là sai số tối ưu thực nghiệm $\operatorname{opt}_s(\bar w_T)=L_s(\bar w_T)-\inf_{w\in W}L_s(w)$, Định nghĩa 04.2 cho lớp hàm điểm số và hàm lỗi $\ell$; $G>0$, $G$ cận chuẩn dưới gradient trên từng quan sát. Ví dụ về $R$: $R=B$ khi $W$ là quả cầu bán kính $B$ và $w_1=0$. Mức (O2) của Bài 01 đòi $\operatorname{opt}_s\le\epsilon_{\mathrm{opt}}$ trên mọi tập huấn luyện một cách tất định; SGD đạt mức này với xác suất ít nhất $1-\delta'$ theo $\xi$. Đây là bảo đảm cho một thuật toán cụ thể, không phải cho lớp (Nhận xét 01.21). Với $S$ ngẫu nhiên, $\operatorname{opt}_S$ là số hạng của bộ giải trong Mệnh đề 04.3; mệnh đề đó cần hàm lỗi trong $[0,1]$ và một bán kính hội tụ đều, nên không áp dụng trực tiếp cho hàm lỗi logistic hay bình phương. Nguồn: ghi chú Bài 05, §9, Hệ quả 05.19, câu sau $\square$, đoạn cuối §9.
- **Lý do / nối:** áp dụng định lý chính cho rủi ro thực nghiệm, thêm bảo đảm với xác suất cao → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 2, 3; Hệ quả 05.19.

#### `6-03` Ý tưởng chứng minh: Hệ quả 05.19 — ý tưởng chứng minh, ví dụ (Ví dụ 05.14) · 2,5 phút
- **Mặt trang:**
  - **Bước 1.** Mệnh đề 05.3(b): $\psi(w)=\frac1m\sum_iv(w,z_i)\in\partial L_s(w)$, tức (G1); $\frac1m\sum_i\lVert v(w,z_i)\rVert^2\le G^2$, tức (G2).
  - **Bước 2.** Mọi $u\in W$ thỏa $\lVert w_1-u\rVert\le R$; Hệ quả 05.15(b) cho (a).
  - **Bước 3.** $\operatorname{opt}_s(\bar w_T)\ge0$ vì $\bar w_T\in W$; Markov và (a): xác suất $\le RG/(\epsilon_{\mathrm{opt}}\sqrt T)\le\delta'$.
  - **Ý nghĩa:** $\delta'=0{,}05$: trong 100 lần chạy độc lập trên cùng $s$, có khoảng 95 lần $\operatorname{opt}_s(\bar w_T)<\epsilon_{\mathrm{opt}}$.
  - **Ví dụ.** $R=1$, $G=4$, $\epsilon_{\mathrm{opt}}=0{,}1$, $\delta'=0{,}05$: $T\ge16/(0{,}0025\cdot0{,}01)=640\,000$, gấp $1/\delta'^2=400$ lần $1600$.
- **Ghi chú diễn giả:** Bước 1 kiểm tra hai giả thiết của oracle cho $F=L_s$; tính chất (b) của Mệnh đề 05.3 là chỗ dùng cách rút đều có hoàn lại. Bước 2 cần $W$ bị chặn để cận dưới đúng trên quả cầu bán kính $R$ quanh $w_1$ bằng $\inf_WL_s$. Bước 3 dùng bất đẳng thức Markov, chỉ dựa trên kì vọng, nên tốn thừa số $1/\delta'^2$ trong số vòng lặp. Với hồi quy logistic, $\epsilon_{\mathrm{opt}}=0{,}05$ và $\delta'=0{,}05$, điều kiện đủ là $10^4/0{,}0025=4\,000\,000$ bước, bằng chi phí của bốn bước GD. Bài tập 05.5(d) giảm giá này bằng nhiều lần chạy độc lập. Nguồn: ghi chú Bài 05, chứng minh Hệ quả 05.19, câu sau $\square$; Ví dụ 05.14.
- **Lý do / nối:** trang ý tưởng chứng minh riêng, ví dụ là bước kiểm tra bằng số → lô nhỏ.
- **Mục tiêu / nguồn:** 3; chứng minh Hệ quả 05.19, Ví dụ 05.14.

#### `6-04` Gradient lô nhỏ — kết quả (Mệnh đề 05.20, đọc thêm) · 2,5 phút
- **Mặt trang:**
  - Lô nhỏ (mini-batch) cỡ $b$ (batch size): $\varphi_b(w,\bar\xi)=\frac1b\sum_{j=1}^b\varphi(w,\xi^{(j)})$, $b$ lần rút độc lập theo $P_\xi$.
  - **Mệnh đề 05.20.** **Giả thiết:** (G1); $\mathbb E_\xi\lVert\varphi(w,\xi)-\psi(w)\rVert^2\le\sigma^2$, $\lVert\psi(w)\rVert\le G_F$ trên $W$. **Bảo đảm:** với mọi $w\in W$,
  - $$\mathbb E\varphi_b=\psi(w),\quad\mathbb E\lVert\varphi_b-\psi(w)\rVert^2\le\frac{\sigma^2}b,\quad\mathbb E\lVert\varphi_b\rVert^2\le G_F^2+\frac{\sigma^2}b=:G_b^2.$$
  - Hệ quả 05.15 với $G_b$: $T\ge R^2G_b^2/\epsilon^2$ bước, tức $bT$ lần gọi oracle gốc.
  - **Kỹ thuật.** Các $e_j=\varphi(w,\xi^{(j)})-\psi(w)$ không tương quan, nên số hạng chéo bằng $0$.
- **Ghi chú diễn giả:** Mệnh đề ở mức đọc thêm. Lộ trình: tính tuyến tính của kì vọng cho phần không chệch; khai triển bình phương của một tổng, $\mathbb E\lVert\tfrac1b\sum_je_j\rVert^2=\tfrac1{b^2}\sum_j\mathbb E\lVert e_j\rVert^2+\tfrac1{b^2}\sum_{j\ne k}\mathbb E\langle e_j,e_k\rangle$, với số hạng chéo bằng $0$; phần mô-men bậc hai từ đẳng thức bình phương trung bình cộng phương sai. Chỉ phần phương sai chia cho $b$; phần $G_F^2$ là độ lớn gradient thật và không đổi theo $b$. Khi lô gồm $b$ bản sao của một quan sát rút một lần, số hạng chéo bằng $\sigma^2$, nên phương sai vẫn là $\sigma^2$, không chia cho $b$ (Ví dụ 05.16). Mệnh đề không có trong các mục UML đã dẫn. Nguồn: ghi chú Bài 05, §10, Mệnh đề 05.20 và chứng minh, Ví dụ 05.16; §14, quan hệ với UML.
- **Lý do / nối:** lô nhỏ đổi hằng số $G$ → bảng số bước và số quan sát.
- **Mục tiêu / nguồn:** 4; Mệnh đề 05.20.

#### `6-05` Ví dụ: số bước và số quan sát theo kích thước lô — ví dụ (Ví dụ 05.15) · 2,5 phút
- **Mặt trang:**
  - $G_F^2=1$, $\sigma^2=15$, nên $G^2=16$ khi $b=1$; $R=1$, $\epsilon=0{,}1$, $m=10^4$.
  - $T(b)=\lceil100(1+15/b)\rceil$; số quan sát phải xử lý là $bT(b)$.
  - Bảng: $b$ | $1$ | $4$ | $16$ | $64$ | $256$ | GD; $T(b)$ | $1600$ | $475$ | $194$ | $124$ | $106$ | $100$; Số quan sát | $1600$ | $1900$ | $3104$ | $7936$ | $27\,136$ | $10^6$.
  - **Diễn giải:** $T(b)$ giảm nhanh đến khoảng $b=15$, rồi gần như đứng yên ở mức $100$ của GD; số quan sát tăng theo $b$.
  - **Kết luận:** theo các cận, lô lớn giảm số lần cập nhật nhưng tăng số quan sát phải xử lý.
- **Ghi chú diễn giả:** Với GD, Hệ quả 05.16 với $G=G_F=1$ cho $100$ bước, mỗi bước $m=10^4$ quan sát. Số quan sát $bT(b)\approx R^2(bG_F^2+\sigma^2)/\epsilon^2$ tăng gần tuyến tính theo $b$; ngưỡng $b=\sigma^2/G_F^2=15$ là nơi phần phương sai bằng phần độ lớn gradient. Trường hợp $b=1$ là oracle của ví dụ hồi quy, với $G^2=16$. Đây là so sánh các cận trên, đúng khi (C) và (G2) thỏa; nó không đo thời gian chạy. Nguồn: ghi chú Bài 05, §10, Ví dụ 05.15, đoạn cuối §10.
- **Lý do / nối:** áp dụng Mệnh đề 05.20 bằng số → bài tập của cụm.
- **Mục tiêu / nguồn:** 4; Ví dụ 05.15.

#### `6-06` Bài tập: kích thước lô cho số bước gần bằng hạ gradient — bài tập (Bài tập 05.5(b)), lời giải trên mặt trang · 2,5 phút (1 phút tự làm)
- **Mặt trang:**
  - Thiết lập của Ví dụ 05.15 trừ $\sigma^2$: $T(b)=\big\lceil R^2(G_F^2+\sigma^2/b)/\epsilon^2\big\rceil$; GD cần $R^2G_F^2/\epsilon^2$ bước.
  - **Câu hỏi:** chứng minh $T(b)$ không quá $1{,}1$ lần số bước của GD khi và chỉ khi $b\ge10\,\sigma^2/G_F^2$.
  - Tính $b$ nhỏ nhất và số quan sát khi đó, với $\sigma^2=3$ và với $\sigma^2=15$.
  - `[f]` **Lời giải:** GD cần $100$ bước; $T(b)\le110$ khi và chỉ khi $100(1+\sigma^2/b)\le110$, tức $b\ge10\,\sigma^2$.
  - `[f]` $\sigma^2=3$: $b=30$, $T(30)=110$, $3300$ quan sát; $\sigma^2=15$: $b=150$, $T(150)=110$, $16\,500$ quan sát.
- **Ghi chú diễn giả:** Với $G_F^2=1$, $R=1$, $\epsilon=0{,}1$, ta có $R^2/\epsilon^2=100$, một số nguyên, nên $T(b)\le1{,}1\cdot100$ tương đương bất đẳng thức không làm tròn. Cả hai kích thước lô cho số quan sát nhỏ hơn nhiều so với $10^6$ quan sát của GD. Điều kiện $b\ge10\sigma^2/G_F^2$ nói rằng phần phương sai $\sigma^2/b$ không quá một phần mười phần độ lớn $G_F^2$. Phần (a) của bài lập bảng với $\sigma^2=3$: $T(b)=400;\ 200;\ 119;\ 105$ tại $b=1,3,16,64$; số bước giảm nhanh đến $b=3$. Phần (c) so rút có hoàn lại và không hoàn lại cho một lô cỡ $2$: phương sai $4{,}75$ và $3{,}1667$; lô không hoàn lại vẫn không chệch, và kết luận về phương sai của Mệnh đề 05.20 vẫn đúng dù giả thiết độc lập không thỏa. Nguồn: tệp bài tập, Bài tập 05.5(b), (a), (c).
- **Lý do / nối:** bài tập của cụm lô nhỏ, lời giải trên mặt trang → câu hỏi cuối buổi về đại lượng được chặn.
- **Mục tiêu / nguồn:** 4; Bài tập 05.5(b).

### Mạch 7. Tổng kết (9 trang, 12 phút)

#### `7-00` 7. Tổng kết — tiêu đề mạch, điểm vào mạch 7 · 0,5 phút
- **Mặt trang:** "7."; h2 "Tổng kết"; `p.strand-lead` (bảng mạch, 19 âm tiết); không có dòng từ khóa.
- **Ghi chú diễn giả:** Bài có một bất đẳng thức tất định cho một bước, một cận kì vọng cho cả quỹ đạo và các hệ quả của nó cho độ dài bước, cho GD, cho rủi ro thực nghiệm và cho lô nhỏ. Hai kỹ thuật dùng lại về sau là kì vọng có điều kiện theo lịch sử và tổng triệt tiêu. Mạch cuối gom các giả thiết không được bỏ, trả lời vấn đề trung tâm cho cả bài, làm một bài tập ghép cận kì vọng với bất đẳng thức Markov, rồi tự kiểm tra và giao bài tập. Nguồn: ghi chú Bài 05, §11–§14.
- **Lý do / nối:** mạch 6 → bảng tổng kết.
- **Mục tiêu / nguồn:** tất cả; §11–§14.

#### `7-01` Ví dụ: $\operatorname{opt}_S$ nhỏ, $L_D$ lớn — ví dụ (câu hỏi cuối buổi §13 và lời giải) · 3 phút
- **Mặt trang:**
  - $D$: $X=1$, $Y=\pm1$ với xác suất $\tfrac12$; $S=((1,1))$; $\ell(w,(x,y))=(wx-y)^2$, $W=[-1,1]$, $w_1=0$, $T=1600$.
  - $\psi(w)=2(w-1)=L_S'(w)$; $L_D(w)=w^2+1$, $L_D'(w)=2w$: oracle không chệch cho $L_S$.
  - $G=4$, $R=1$, $\eta=0{,}00625$: Hệ quả 05.15(b) cho $L_S(\bar w_{1600})-\min_WL_S\le0{,}1$.
  - $1-w_t=0{,}9875^{t-1}$, nên $\bar w_{1600}\approx0{,}95$: $L_S\approx0{,}0025$, $L_D\approx1{,}9025$, $\min_WL_D=1$.
  - **Diễn giải:** $\operatorname{opt}_S\approx0{,}0025$, còn sai số ước lượng $L_D(\bar w_{1600})-\min_WL_D\approx0{,}9025$.
  - **Kết luận:** cận chặn $\operatorname{opt}_S$; muốn chặn $L_D$ cần thêm một cận thống kê.
- **Ghi chú diễn giả:** Chỉ có một chỉ số, nên oracle tất định và SGD trùng GD. Trên $W$, $\lvert\psi(w)\rvert=2\lvert w-1\rvert\le4$; mọi $u\in W$ có $\lvert w_1-u\rvert\le1$; $\min_WL_S=L_S(1)=0$. Mọi điểm lặp nằm trong $[0,1]$, nên phép chiếu không tác động, và $1-w_{t+1}=0{,}9875(1-w_t)$; tổng cấp số nhân cho $1-\bar w_{1600}=(1-0{,}9875^{1600})/20\approx0{,}05$, vì $0{,}9875^{1600}\approx1{,}8\cdot10^{-9}$. Với lớp hàm điểm số trên $W$, mức tốt nhất là $L_D(0)=1$. Khi chỉ số được rút từ $S$, oracle không chệch cho $L_S$ và các cận kiểm soát $\operatorname{opt}_S$; với $D$ này, $\operatorname{opt}_S$ nhỏ trong khi $L_D$ còn xa mức tốt nhất. Mọi cận của bài chặn độ chênh tối ưu của hàm mà oracle không chệch; muốn chặn $L_D$, hay tỉ lệ lỗi 0–1 khi tối thiểu hóa hàm lỗi bản lề hoặc logistic, cần một cận thống kê. Nguồn: ghi chú Bài 05, §13, câu hỏi cuối buổi và lời giải, đoạn sau; §11.
- **Lý do / nối:** phân biệt sai số tối ưu thực nghiệm với rủi ro kì vọng trên một ví dụ tính tay; cuối mạch theo thứ tự của ghi chú (§13 sau §12) → tổng kết.
- **Mục tiêu / nguồn:** 3; §13, §11.

#### `7-02` Bảng tổng kết — tổng kết · 1,5 phút
- **Mặt trang (bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh`, trần 80):**
  | Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh |
  |---|---|---|
  | $\langle g,w-u\rangle\le\frac{\lVert w-u\rVert^2-\lVert w^+-u\rVert^2}{2\eta}+\frac\eta2\lVert g\rVert^2$, tất định (Mệnh đề 05.13) | $W$ đóng, lồi; $u\in W$ | phép chiếu, khai triển |
  | $\mathbb EF(\bar w_T)-F(u)\le\frac{\lVert w_1-u\rVert^2}{2\eta T}+\frac{\eta G^2}2$, kì vọng (Định lý 05.14) | (C), (G1), (G2), rút độc lập | tổng triệt tiêu, lịch sử, lồi hữu hạn |
  | $\mathbb EF(\bar w_T)-F(u)\le RG/\sqrt T$ khi $\lVert w_1-u\rVert\le R$, kì vọng (Hệ quả 05.15) | $\eta=R/(G\sqrt T)$, $T$ chọn trước | cân hai số hạng |
  | $F(\bar w_T)-F(u)\le RG/\sqrt T$, tất định (Hệ quả 05.16) | (C), $\lVert v(w)\rVert\le G$ | một quỹ đạo |
  | $\mathbb E_\xi\operatorname{opt}_s\le RG/\sqrt T$; $\Pr_\xi[\operatorname{opt}_s\ge\epsilon_{\mathrm{opt}}]\le\delta'$, kì vọng; xác suất $\ge1-\delta'$ (Hệ quả 05.19) | rút có hoàn lại; $W$ bị chặn | Mệnh đề 05.3(b), Markov |
- **Ghi chú diễn giả:** Mỗi giả thiết của Định lý 05.14 có một phản ví dụ ở mạch 5: bỏ tính lồi, độ chênh $0{,}5$ so với cận $0{,}140625$; bỏ cận mô-men bậc hai, SGD phân kì trong khi GD hội tụ; bỏ tính không chệch, độ chênh của $L_S$ tiến tới $0{,}16$; bỏ tính độc lập của các lần rút, Bước 3 hỏng. Hàng Hệ quả 05.15 giữ mọi giả thiết của Định lý 05.14. Hàng Hệ quả 05.19 giữ mọi giả thiết về hàm lỗi lồi, không âm và dưới gradient bị chặn. Bổ đề 05.8 và 05.12 là công cụ, không có hàng riêng. Mệnh đề 05.20 (đọc thêm) không có hàng: gradient lô nhỏ có mô-men bậc hai $G_F^2+\sigma^2/b$ khi các phần tử của lô không tương quan, chứng minh bằng số hạng chéo bằng $0$. Nguồn: ghi chú Bài 05, §7–§11.
- **Lý do / nối:** một hàng cho mỗi kết quả chính, giữ loại bảo đảm → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §7–§10.

#### `7-03` Vấn đề trung tâm — tổng kết · 1,5 phút
- **Mặt trang:**
  - Mỗi bước: $\lVert w_t-u\rVert^2$ giảm $2\eta\langle g_t,w_t-u\rangle$, tăng $\eta^2\lVert g_t\rVert^2$; $L_S$ có thể tăng.
  - Theo kì vọng, khi (C), (G1), (G2) thỏa, $\eta=R/(G\sqrt T)$, $\lVert w_1-u\rVert\le R$: $\mathbb EF(\bar w_T)-F(u)\le RG/\sqrt T$.
  - Mức $\epsilon$ theo kì vọng: $T\ge R^2G^2/\epsilon^2$; với xác suất ít nhất $1-\delta'$ theo $\xi$: thêm thừa số $1/\delta'^2$.
  - $10^6$ hồ sơ: $10^4$ bước SGD cho mức kì vọng $0{,}05$, bằng $1\%$ một bước GD.
  - Đại lượng được chặn: $\operatorname{opt}_S$, không phải $L_D$.
- **Ghi chú diễn giả:** Trả lời cho câu hỏi "tối ưu ngẫu nhiên làm giảm hàm mục tiêu nhanh đến mức nào": độ chênh tối ưu kì vọng tại điểm lặp trung bình giảm như $RG/\sqrt T$, nên muốn giảm một nửa cần gấp bốn lần số vòng lặp. Một bước SGD có thể làm $L_S$ tăng (ví dụ ba quan sát), nhưng bảo đảm là cho trung bình. Độ dài bước được rút ra từ cận; lệch mười lần làm cận tăng $5{,}05$ lần. Với lô nhỏ, theo cận, chỉ phần phương sai giảm theo kích thước lô. Mọi cận chặn độ chênh tối ưu của hàm mà oracle không chệch; với chỉ số rút từ $S$, đó là $L_S$; tính lồi là điều kiện của (G1) và của Bước 5, nên các cận không chuyển sang mạng nơ-ron mà không có lập luận mới. Nguồn: ghi chú Bài 05, §11.
- **Lý do / nối:** trả lời vấn đề trung tâm cho cả bài, giữ loại bảo đảm và đại lượng được chặn → bài tập tổng hợp.
- **Mục tiêu / nguồn:** tất cả; §11.

#### `7-04` Bài tập: nhiều lần chạy độc lập — bài tập tổng hợp (Bài tập 05.5(d)), đề · 1,5 phút
- **Mặt trang:**
  - Lấy $R=1$, $G=4$, $\epsilon_{\mathrm{opt}}=0{,}1$, $\delta'=0{,}05$ như Ví dụ 05.14.
  - **Câu hỏi:** chạy SGD có chiếu $k$ lần độc lập trên cùng mẫu $S$, mỗi lần với số bước đủ cho $\mathbb E_\xi\operatorname{opt}_S\le\epsilon_{\mathrm{opt}}/2$,
  - rồi giữ đầu ra có $L_S$ nhỏ nhất ($L_S$ tính chính xác, $m$ lần tính hàm lỗi mỗi đầu ra).
  - Chứng minh xác suất để đầu ra được giữ có $\operatorname{opt}_S\ge\epsilon_{\mathrm{opt}}$ không quá $2^{-k}$.
  - Tìm $k$ nhỏ nhất, tổng số bước SGD, và so với $640\,000$ bước của Ví dụ 05.14.
- **Ghi chú diễn giả:** Bài ghép bốn ý của bài: cận kì vọng với độ dài bước theo số vòng lặp, tính không âm của sai số tối ưu thực nghiệm, bất đẳng thức Markov, và tính độc lập giữa các lần chạy, rồi so chi phí với cận của Hệ quả 05.19(b). Gợi ý: áp dụng bất đẳng thức Markov cho từng lần chạy; mọi đầu ra có cùng số trừ $\inf_WL_S$, nên đầu ra có $L_S$ nhỏ nhất cũng có $\operatorname{opt}_S$ nhỏ nhất. Nguồn: tệp bài tập, Bài tập 05.5(d) và hai gợi ý.
- **Lý do / nối:** bài tập tổng hợp từ `exercises.md`, đề trên một trang vì câu chữ dài → lời giải.
- **Mục tiêu / nguồn:** 3, 4; Bài tập 05.5(d).

#### `7-05` Bài tập: nhiều lần chạy độc lập (tiếp) — bài tập tổng hợp (Bài tập 05.5(d)), lời giải · 2 phút
- **Mặt trang:**
  - **Lời giải:** $X_j=\operatorname{opt}_S$ của lần chạy $j$: $X_j\ge0$, $\mathbb EX_j\le\epsilon_{\mathrm{opt}}/2$; Markov: $\Pr(X_j\ge\epsilon_{\mathrm{opt}})\le\tfrac12$.
  - Đầu ra được giữ có $\operatorname{opt}_S=\min_jX_j$; các lần chạy độc lập: xác suất $\le2^{-k}$.
  - $2^{-k}\le0{,}05$ khi $k\ge\log_220\approx4{,}32$: $k=5$, $2^{-5}=0{,}03125$.
  - Mỗi lần $16/0{,}0025=6400$ bước; tổng $32\,000$ bước, cộng $5m$ lần tính hàm lỗi.
  - **Kết luận:** ít hơn $640\,000$ khi $32\,000+5m<640\,000$, tức $m<121\,600$.
- **Ghi chú diễn giả:** Biến cố "đầu ra được giữ có $\operatorname{opt}_S\ge\epsilon_{\mathrm{opt}}$" là giao của $k$ biến cố $X_j\ge\epsilon_{\mathrm{opt}}$, độc lập vì các lần chạy dùng các lần rút độc lập. Với $k=4$, $2^{-4}=0{,}0625>0{,}05$, nên $k=5$ là nhỏ nhất. Mỗi lần chạy cần $R^2G^2/(\epsilon_{\mathrm{opt}}/2)^2$ bước theo Hệ quả 05.15(c). So sánh ở dòng kết luận giả sử một lần tính hàm lỗi tốn ngang một gradient trên một quan sát. Cách này thay thừa số $1/\delta'^2$ của bất đẳng thức Markov bằng thừa số $\log_2(1/\delta')$ lần chạy. Nguồn: tệp bài tập, lời giải Bài tập 05.5(d).
- **Lý do / nối:** lời giải trên mặt trang, mỗi dòng một bước → tự kiểm tra.
- **Mục tiêu / nguồn:** 3, 4; Bài tập 05.5(d).

#### `7-06` Câu hỏi tự kiểm tra — tổng kết · 1 phút
- **Mặt trang:**
  - 1. Vì sao Định lý 05.14 vẫn đúng khi một bước SGD làm $L_S$ tăng?
  - 2. Với $\eta$ cố định, vế phải của Định lý 05.14 tiến tới đâu khi $T$ tăng?
  - 3. Bước nào của chứng minh dùng (G1), bước nào dùng (G2)?
  - 4. Vì sao cách xáo trộn lại sau mỗi vòng không thỏa Định nghĩa 05.10?
- **Ghi chú diễn giả** (câu trả lời dự kiến, chỉ dùng ghi chú): (1) Định lý chặn trung bình theo kì vọng tại điểm lặp trung bình, không chặn từng bước; theo bất đẳng thức một bước, khoảng cách tới $u$ còn tăng do số hạng $\eta^2\lVert g\rVert^2$, và trong ví dụ ba quan sát cả ba lựa chọn đều làm $L_S$ tăng từ $0{,}0639$. (2) Tới $\eta G^2/2$, vì số hạng $\lVert w_1-u\rVert^2/(2\eta T)$ giảm như $1/T$; muốn cận về $0$ phải chọn $\eta$ theo $T$ (Hệ quả 05.15). (3) (G1) ở Bước 3, qua Bổ đề 05.12(c) và bất đẳng thức dưới gradient; (G2) chỉ ở Bước 4, cho số hạng $\tfrac\eta2\lVert g_t\rVert^2$. (4) Chỉ số rút không hoàn lại trong mỗi vòng, nên các lần rút không độc lập; với $m=2$, lần rút thứ hai của mỗi vòng đã xác định. Nguồn: ghi chú Bài 05, Ví dụ 05.6, Định lý 05.14 và đoạn sau, chứng minh Định lý 05.14, đoạn sau Định nghĩa 05.10.
- **Lý do / nối:** 2–4 câu hỏi ngắn trả lời được chỉ bằng ghi chú → bài tập về nhà.
- **Mục tiêu / nguồn:** 1, 2, 5; §6, §7.

#### `7-07` Bài tập về nhà — tổng kết · 0,5 phút
- **Mặt trang:**
  | Mục | Bài tập |
  |---|---|
  | 2. Hàm lồi và dưới gradient | 05.1, 05.7, 05.9, 05.12 |
  | 4. Bất đẳng thức một bước và cận kì vọng | 05.2, 05.4, 05.8, 05.10, 05.11 |
  | 5. Vai trò của từng giả thiết | 05.3, 05.6 |
  | 6. Hạ gradient ngẫu nhiên trên rủi ro thực nghiệm và lô nhỏ | 05.5 |
  - Liên kết "Ghi chú bài giảng · Bài tập" (viewer `&deck=`).
- **Ghi chú diễn giả:** Mỗi bài xếp vào mạch cung cấp kiến thức cuối cùng bài đó cần. Bài tập 05.8 cần hằng số $G$ của ví dụ hồi quy logistic; 05.10 cần Thuật toán 05.9 và Hệ quả 05.16; 05.11 cần độ dài bước thay đổi và Ví dụ 05.8; 05.2 cần Mệnh đề 05.13 và Ví dụ 05.6; 05.3 cần chỗ dùng tính độc lập trong chứng minh; 05.6 cần mức sàn sai số và Định lý 05.14. Mạch 3 không có bài riêng: các bài về phép chiếu và oracle đều cần thêm bất đẳng thức một bước hoặc chứng minh định lý chính. Sáu bài đầu là bài gốc của học phần, sáu bài sau chọn từ UML §9.6, §12.6, §14.8; Bài tập 05.6(f) là thực nghiệm tùy chọn, Bài tập 05.12 là phần mở rộng. Nguồn: ghi chú Bài 05, §12; tệp bài tập.
- **Lý do / nối:** giao bài tập theo mạch → tài liệu.
- **Mục tiêu / nguồn:** tất cả; §12.

#### `7-08` Tài liệu tham khảo — tổng kết · 0,5 phút
- **Mặt trang:**
  - Trước buổi học: UML §12.1, §14.1.
  - Sau buổi học: UML §14.2, §14.3, §14.4.1, §9.2, §12.2.
  - Mở rộng: UML §14.4.2–14.4.4, §12.3.
  - Shalev-Shwartz, S. và Ben-David, S. (2014). *Understanding Machine Learning: From Theory to Algorithms*. Cambridge University Press.
  - Bài 06: Học bằng hạ gradient ngẫu nhiên, chính quy hóa và tính ổn định.
- **Ghi chú diễn giả:** UML §12.1 trình bày tính lồi, tính Lipschitz, tính trơn; §14.1 hạ gradient; §14.2 dưới gradient; §14.3 hạ gradient ngẫu nhiên; §14.4.1 bước chiếu; §9.2 hồi quy tuyến tính; §12.2 bài toán học lồi; §14.4.2–14.4.4 độ dài bước thay đổi, các cách lấy trung bình khác, hàm lồi mạnh; §12.3 hàm lỗi thay thế (surrogate loss). Khác biệt chính với UML: UML §14.3 xét điểm khởi tạo $0$, không chiếu, gradient ngẫu nhiên bị chặn hầu chắc chắn; ở đây có phép chiếu, điểm khởi tạo bất kì trong $W$, cận mô-men bậc hai và mọi điểm so sánh $u\in W$. UML đặt điều kiện lên kì vọng có điều kiện của véc-tơ cập nhật; ở đây điều kiện đó là Bổ đề 05.12. UML viết $\rho$ cho hằng số Lipschitz; UML §12.3 gọi hiệu giữa hai giá trị nhỏ nhất là optimization error, khác $\operatorname{opt}_S$. Bài 06 so hai cách dùng dữ liệu có cùng phép cập nhật: rút một quan sát mới từ $D$ ở mỗi bước, hoặc chạy nhiều vòng trên cùng $S$, và hỏi khi nào tối thiểu hóa trên $S$ cũng kiểm soát được $L_D$. Nguồn: ghi chú Bài 05, §14 và quan hệ với UML; §13, đoạn cuối.
- **Lý do / nối:** trang cuối; dòng chữ Bài 06 (không liên kết cho đến khi deck Bài 06 có tên tệp).
- **Mục tiêu / nguồn:** —; §14.

## 7. Hành trình khái niệm

Thứ tự bước theo quy định: vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh (trang riêng) → kỹ thuật hoặc kiểm tra. Các bước có thể chung trang nhưng không đảo thứ tự trên mặt trang. Theo cổng duyệt Bài 04 (T5), ví dụ đặt trước phát biểu khi số liệu của nó không cần chính kết quả đó; ví dụ của ghi chú dùng kết quả để kiểm tra thì đứng sau, ở cột cuối.

| Kết quả hoặc khái niệm | Vấn đề | Trực quan | Ví dụ | Phát biểu | Ý tưởng chứng minh | Kỹ thuật / kiểm tra | Gộp, `không áp dụng`, lý do |
|---|---|---|---|---|---|---|---|
| Hàm lồi (Định nghĩa 05.1) | 2-02 (dòng mở: hàm lỗi 0–1 không lồi, hàm lỗi bản lề có điểm gãy) | 2-02 ("Trực quan.": dưới dây cung) | 2-03 (hình F1, $(w^2-1)^2$ không lồi) | 2-02 | `không áp dụng` (định nghĩa) | 2-02 (bất đẳng thức lồi hữu hạn, dùng lại ở 4-04 Bước 5) | Ví dụ lồi/không lồi ở ghi chú diễn giả vì mật độ. |
| Dưới gradient (Định nghĩa 05.2) và Mệnh đề 05.3 | 2-00, 2-02 | 2-03 (hình F1: siêu phẳng tựa) | 2-03 ($\lvert w\rvert$: mọi $\lvert v\rvert\le1$ cho cận dưới tại $0$) | 2-03, 2-04 | `không áp dụng`: Mệnh đề 05.3 là công cụ tính, chứng minh ba dòng ở ghi chú diễn giả 2-04 (mục 11, điểm 3) | 2-04 (Ví dụ 05.3), 2-05 (Ví dụ 05.2), 2-07 (Bài tập 05.1(d)) | Ví dụ 05.2, 05.3 dùng Mệnh đề 05.3 nên đứng sau, theo ghi chú. |
| Lipschitz (Định nghĩa 05.4) và Mệnh đề 05.5 | 2-05 (dưới gradient của hàm lỗi bản lề có chuẩn $\lVert x\rVert$) | ghi chú diễn giả 2-06 (mỗi bước dài không quá $\eta G$) | 2-06 dòng "Ví dụ." | 2-06 | `không áp dụng`: công cụ, lộ trình ở ghi chú diễn giả 2-06 | 3-05 ($G=4$ từ $2(BC_x+C_y)C_x$ với $B=C_x=C_y=1$) | Trực quan gộp vào ghi chú diễn giả vì mật độ (2-06 ở 48). |
| Phép chiếu (Định nghĩa 05.7) và Bổ đề 05.8 | 3-01 (dòng mở: cận $G$ cần tập bị chặn) | 3-02 ("Trực quan.": góc không nhọn); hình F2 | 3-01 (Ví dụ 05.4 bằng số, hình F2) | 3-01, 3-02 | `không áp dụng`: công cụ, phác thảo ở ghi chú diễn giả 3-02 | 4-02 Bước 1 (dùng Bổ đề 05.8(b)) | Ví dụ 05.4 Bước 3 không cần bổ đề nên đặt trước; Bước 2 (kiểm bằng bổ đề) ở ghi chú diễn giả. |
| Oracle (Định nghĩa 05.10) và Bổ đề 05.12 | 1-06, 2-04 (rút đều cho trung bình $\nabla L_S(0)$) | 3-06 ("Trực quan.": biết lịch sử, $w_t$ cố định) | 3-03 dòng "Ví dụ 05.5."; 3-05 (Ví dụ 05.5 Bước 2, Ví dụ 05.6) | 3-03, 3-06 | 3-07 (trang "Kỹ thuật.", cơ chế chứng minh phần (c)) | 3-08 (Bài tập 05.3(b): $0{,}8460$ hai cách); 5-04 (Bài tập 05.3(c): bỏ độc lập) | Bổ đề 05.12 là công cụ (phác thảo); trang kỹ thuật thay trang ý tưởng chứng minh, như Bổ đề 02.5 của deck Bài 02. |
| Mệnh đề 05.13 | 1-06, 3-05 (một bước SGD làm $L_S$ tăng) | 4-01 ("Trực quan.": khai triển $\lVert w-\eta g-u\rVert^2$) | 3-05 (bước thứ hai: $w_2$, $g_2$, $(1,-1)$, $w_3$) | 4-01 | 4-02 | 4-02 (Ví dụ 05.7: $1{,}3289$, $1{,}5019$; Bài tập 05.2 ở ghi chú diễn giả) | Ví dụ 05.7 dùng dạng của mệnh đề nên là bước kiểm tra trên trang ý tưởng chứng minh. |
| Định lý 05.14 | 1-05, 1-06; 3-05 (cần bảo đảm cho trung bình) | 4-03 ("Trực quan.": khoảng cách triệt tiêu) | 3-05, 3-08 (cùng ví dụ, các bước đầu) | 4-03 | 4-04 | 4-05 (trang "Kỹ thuật."); 5-01 đến 5-04 (bỏ từng giả thiết) | — |
| Hệ quả 05.15 | 4-06 (dòng: với $\eta$ cố định, vế phải giảm về $\eta G^2/2$) | 4-06 ("Trực quan.", hình F4) | 4-06 dòng "Ví dụ." (Ví dụ 05.8 Bước 3) | 4-07 | 4-08 | 4-08 (Ví dụ 05.8 Bước 1–2); 4-09 (Ví dụ 05.9); 4-10 (Bài tập 05.4(c)) | Ví dụ 05.8 chia: Bước 3 (không cần hệ quả) trước, Bước 1–2 (dùng (c)) sau. |
| Hệ quả 05.16 | 4-08 (GD và SGD cùng số vòng lặp?) | ghi chú diễn giả 4-09 (oracle tất định) | 4-09 (Ví dụ 05.9) | 4-09 | `không áp dụng`: kết quả phụ, một dòng ở ghi chú diễn giả 4-09 (mục 11, điểm 3) | 4-09 dòng "Kết luận:"; 5-01 (Ví dụ 05.10 dùng cận của Hệ quả 05.16) | Phát biểu và ví dụ chung trang. |
| Định nghĩa 05.18 và Hệ quả 05.19 | 6-01 (đầu ra ngẫu nhiên khi $S$ cố định); 1-02 ((O2) tất định) | 6-02 ("Trực quan.": $\operatorname{opt}_s\ge0$, Markov) | 4-08 (Ví dụ 05.8: $\mathbb E_\xi L_S(\bar w_{1600})\le0{,}16112$, phần (a) trên dữ liệu thật) | 6-01, 6-02 | 6-03 | 6-03 (Ví dụ 05.14: $640\,000$); 7-01 (câu hỏi cuối buổi); 7-04, 7-05 (Bài tập 05.5(d)) | — |
| Mệnh đề 05.20 (đọc thêm) | 4-09, 6-04 dòng mở (hai đầu mút: một quan sát, cả tập) | 6-04 dòng "Kỹ thuật." (chỉ phương sai chia cho $b$) | 6-05 (Ví dụ 05.15) | 6-04 | `không áp dụng`: mức đọc thêm, lộ trình ở ghi chú diễn giả 6-04 | 6-05, 6-06 (Bài tập 05.5(b)); Ví dụ 05.16 ở ghi chú diễn giả 6-04 | Ví dụ 05.15 đứng sau phát biểu theo ghi chú (cần $G_b$). |

Thời lượng theo mạch: 9 + 22 + 22 + 30 + 10 + 18 + 9 = 120 phút; 55 trang.

## 8. Hình vẽ

Mọi hình là SVG trong `2627-1/img/lec-05/`, `role="img"`, có `<title>` và alt cụ thể; màu không là tín hiệu duy nhất (kiểu nét và hình dạng điểm khác nhau cho từng dãy); chữ trong hình chỉ là nhãn trục, nhãn điểm, số và nhãn ngắn (Unicode), không công thức; công thức và chú thích nằm ở `figcaption` (KaTeX). Chú thích nêu dữ liệu. Dữ liệu chính xác lấy từ mục 5.

| Mã | Tệp | Trang | Nội dung và dữ liệu | Alt dự kiến |
|---|---|---|---|---|
| F1 | `duoi-gradient.svg` | 2-03 | Hai khung cạnh nhau. Khung trái: $f(w)=\lvert w\rvert$ trên $[-1{,}5;1{,}5]$, trục dọc $[-1{,}5;1{,}5]$; bốn đường thẳng nét đứt qua gốc với hệ số góc $-1$; $-0{,}5$; $0{,}5$; $1$ (nhãn ở đầu mút), đều nằm dưới hoặc chạm đồ thị; nhãn "hệ số góc trong [−1, 1]". Khung phải: $f(w)=(w^2-1)^2$ trên $[-1{,}6;1{,}6]$, trục dọc $[0;2{,}5]$; chấm tại $(0,1)$ nhãn "f′(0) = 0", đường nằm ngang nét chấm $y=1$; chấm tại $(-1,0)$ và $(1,0)$; đoạn đồ thị dưới đường ngang tô đậm. `figcaption`: "Trái: $f(w)=\lvert w\rvert$ và các đường $vw$ với $v\in\{-1;-0{,}5;0{,}5;1\}$, nằm dưới đồ thị. Phải: $f(w)=(w^2-1)^2$; đường nằm ngang qua $(0,1)$ cắt đồ thị vì $f(\pm1)=0$." | "Hai đồ thị. Bên trái là hàm trị tuyệt đối, hình chữ V; bốn đường thẳng qua gốc với hệ số góc từ âm 1 đến 1 đều nằm dưới chữ V. Bên phải là hàm (w bình phương trừ 1) bình phương, có hai đáy tại âm 1 và 1 với giá trị 0 và một đỉnh tại 0 với giá trị 1; đường nằm ngang qua đỉnh cắt đồ thị và nằm trên hai đáy." |
| F2 | `phep-chieu.svg` | 3-01 | Hình tròn đơn vị tô nhạt (nhãn "W"), trục $[-1{,}3;1{,}6]\times[-1{,}4;1{,}3]$. Điểm $\theta=(1,-1)$ (chấm rỗng, nhãn "θ"), $\pi=(0{,}7071;-0{,}7071)$ (chấm đặc, nhãn "proj"), $u=(1,0)$ (ô vuông, nhãn "u"). Đoạn $\theta$–$\pi$ (nét liền, nằm trên đường thẳng qua gốc), đoạn $\pi$–$u$ (nét đứt), đoạn $\theta$–$u$ (nét chấm, nhãn "1"), nhãn "0,7654" cạnh đoạn $\pi$–$u$; cung đánh dấu góc tại $\pi$ giữa hai đoạn đầu (góc tù). `figcaption`: "Quả cầu đơn vị, $\theta=(1,-1)$, $\operatorname{proj}_W(\theta)\approx(0{,}7071;-0{,}7071)$, $u=(1,0)$: $\lVert\theta-u\rVert=1$, $\lVert\operatorname{proj}_W(\theta)-u\rVert\approx0{,}7654$, $\langle\theta-\pi,u-\pi\rangle\approx-0{,}1213$." | "Hình tròn đơn vị. Điểm theta (1, âm 1) nằm ngoài, ảnh chiếu của nó nằm trên đường tròn tại (0,7071; âm 0,7071). Điểm u (1, 0) nằm trên đường tròn. Khoảng cách từ theta tới u là 1, từ ảnh chiếu tới u là 0,7654. Góc tại ảnh chiếu giữa hướng về theta và hướng về u là góc tù." |
| F3 | `ba-buoc-sgd.svg` | 3-05 | Mặt phẳng, trục $[-0{,}1;1{,}5]\times[-1{,}1;0{,}2]$ (tỉ lệ bằng nhau); cung đường tròn đơn vị (nét liền mảnh, nhãn "‖w‖ = 1"). Điểm: $w_1=0$; $w_2=(1,0)$; điểm chưa chiếu $(1,-1)$ (chấm rỗng); $w_3=(0{,}7071;-0{,}7071)$; mũi tên $w_1\to w_2\to(1,-1)\to w_3$. Ba điểm $w_4$ (tam giác, nhãn "1: 0,0710", "2: 0,1021", "3: 0,0694"): $(0{,}8165;-0{,}5774)$, $(0{,}5774;-0{,}8165)$, $(0{,}7920;-0{,}5940)$. Điểm GD $(0{,}7356;-0{,}6774)$ (ô vuông, nhãn "GD: 0,0614"); $w^*=(0{,}7473;-0{,}6645)$ (ngôi sao, nhãn "w*: 0,06112"); nghiệm không ràng buộc $(1{,}06;-0{,}92)$ (hình thoi rỗng, nhãn "1,06; −0,92"). Đường mức $L_S=0{,}0639$ nét đứt: elip tâm $(1{,}06;-0{,}92)$, bán trục $0{,}4142$ theo hướng $(-0{,}8;0{,}6)$ và $0{,}2929$ theo hướng $(0{,}6;0{,}8)$ (từ dạng bậc hai của Phụ lục D, trị riêng của $M$ là $\tfrac13$, $\tfrac23$); nhãn "L_S = 0,0639". Cụm điểm quanh $w_3$ có thể phóng to trong một khung nhỏ. `figcaption`: "Ví dụ 05.6: $w_1=0$, $\eta=0{,}5$, $i_1=1$, $i_2=2$; ba lựa chọn $i_3$ cho $L_S(w_4)$ bằng $0{,}0710$; $0{,}1021$; $0{,}0694$, bước GD cho $0{,}0614$; đường đứt là đường mức $L_S=0{,}0639$ qua $w_3$." | "Quỹ đạo SGD trong mặt phẳng: từ gốc tới (1, 0), rồi tới (1, âm 1) bên ngoài đường tròn đơn vị và được chiếu về (0,7071; âm 0,7071). Một elip nét đứt là đường mức của rủi ro thực nghiệm tại giá trị 0,0639 đi qua điểm này. Ba điểm của bước thứ ba nằm ngoài elip, với rủi ro 0,0710, 0,1021 và 0,0694. Điểm của bước hạ gradient nằm trong elip, rủi ro 0,0614, gần nghiệm tối ưu trên đường tròn có rủi ro 0,06112." |
| F4 | `do-dai-buoc.svg` | 4-06 | Trục ngang $\eta$ thang lôgarit từ $0{,}0005$ đến $0{,}1$ (vạch $0{,}001$; $0{,}003125$; $0{,}00625$; $0{,}0125$; $0{,}0625$); trục dọc tuyến tính $[0;0{,}8]$ (vạch $0$; $0{,}2$; $0{,}4$; $0{,}6$; $0{,}8$). Ba đường từ công thức $Q(\eta)=1/(3200\eta)+8\eta$ (vế phải của Định lý 05.14 với $R=1$, $G=4$, $T=1600$; số liệu mục 5, V26): số hạng $1/(3200\eta)$ (nét đứt, giảm), số hạng $8\eta$ (nét chấm, tăng), tổng (nét liền đậm). Bốn chấm trên đường tổng có nhãn: "η*/2: 0,125", "η*: 0,1", "2η*: 0,125", "10η*: 0,505". Nhãn trực tiếp cuối đường: "khoảng cách", "nhiễu", "tổng". `figcaption`: "Vế phải của Định lý 05.14 với $R=1$, $G=4$, $T=1600$ theo $\eta$: số hạng $R^2/(2\eta T)$, số hạng $\eta G^2/2$ và tổng; nhỏ nhất $0{,}1$ tại $\eta^*=0{,}00625$." | "Đồ thị theo độ dài bước trên trục lôgarit. Một đường giảm, một đường tăng, và tổng của chúng có dạng chữ U với đáy 0,1 tại độ dài bước 0,00625. Tại một nửa và gấp đôi độ dài bước đó, tổng là 0,125; tại gấp mười, tổng là 0,505." |
| F5 | `khong-loi.svg` | 5-01 | Trục ngang $[-2;2]$ (vạch từng $0{,}5$), trục dọc $[0;1{,}6]$. Đồ thị $f(w)=\min\{(w-1)^2,(w+1)^2+0{,}5\}$ (nét liền), điểm gãy tại $(-0{,}125;1{,}2656)$. Chấm tại $(1,0)$ nhãn "cực tiểu toàn cục 0", tại $(-1;0{,}5)$ nhãn "cực tiểu địa phương 0,5". Điểm khởi tạo $(-1{,}5;0{,}75)$ (chấm rỗng, nhãn "w₁"); mũi tên dọc đồ thị từ $-1{,}5$ tới $-1$; nhãn "w̄ ≈ −1,0056" tại đáy trái. `figcaption`: "Ví dụ 05.10: $f(w)=\min\{(w-1)^2,(w+1)^2+0{,}5\}$ trên $[-2,2]$, GD từ $w_1=-1{,}5$ với $\eta\approx0{,}02778$, $T=1600$: $\bar w_{1600}\approx-1{,}0056$, $f(\bar w_{1600})\approx0{,}5$." | "Đồ thị có hai đáy: đáy trái tại âm 1 với giá trị 0,5, đáy phải tại 1 với giá trị 0. Hai nhánh gặp nhau tại một điểm gãy gần âm 0,125. Các điểm lặp hạ gradient xuất phát tại âm 1,5 và đi xuống đáy trái, trung bình các điểm lặp ở âm 1,0056 với giá trị 0,5." |

Cách dựng dữ liệu hình không có số mới trên nhãn: F1 dùng bốn hệ số góc trong $[-1,1]$ (khẳng định của ghi chú: mọi $v$ với $\lvert v\rvert\le1$); F3 dùng đường mức tính từ dạng bậc hai của Phụ lục D, chỉ ghi nhãn $0{,}0639$ (số của ghi chú); F4 vẽ đường cong từ công thức của Định lý 05.14, chỉ bốn điểm có nhãn (số của Ví dụ 05.8). Điều phối viên ghi cách dựng vào `review-log.md`.

## 9. Trang tổng kết

Chi tiết từng trang ở mục 6 (7-02 đến 7-08). Tóm tắt:
- **Bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh` (7-02):** năm hàng: Mệnh đề 05.13 (tất định), Định lý 05.14 (kì vọng), Hệ quả 05.15 (kì vọng), Hệ quả 05.16 (tất định), Hệ quả 05.19 (kì vọng; xác suất $\ge1-\delta'$). Mệnh đề 05.20 (đọc thêm) và hai bổ đề công cụ ở ghi chú diễn giả. Phản ví dụ của từng giả thiết ở ghi chú diễn giả.
- **Vấn đề trung tâm (7-03):** năm câu trả lời cho cả bài: một bước; cận kì vọng với độ dài bước theo $T$; số vòng lặp theo kì vọng và với xác suất ít nhất $1-\delta'$; câu hỏi thực hành ($10^4$ bước, $1\%$ một bước GD); đại lượng được chặn là $\operatorname{opt}_S$, không phải $L_D$.
- **Bài tập tổng hợp (7-04, 7-05):** Bài tập 05.5(d), hai trang (đề; lời giải trên mặt trang). Lý do chọn: ghép Hệ quả 05.15(c), tính không âm của $\operatorname{opt}_S$, bất đẳng thức Markov, tính độc lập giữa các lần chạy, và so với Ví dụ 05.14 (Hệ quả 05.19(b)).
- **Câu hỏi tự kiểm tra (7-06):** bốn câu, câu trả lời dự kiến ở ghi chú diễn giả: (1) định lý chặn trung bình theo kì vọng, không chặn từng bước; số hạng $\eta^2\lVert g\rVert^2$; ví dụ $0{,}0639$; (2) tới $\eta G^2/2$; (3) (G1) ở Bước 3, (G2) ở Bước 4; (4) rút không hoàn lại trong mỗi vòng, các lần rút không độc lập.
- **Bài tập về nhà (7-07):** bảng `Mục | Bài tập` ánh xạ mười hai bài vào mạch 2, 4, 5, 6 (mạch 3 không có bài mà kiến thức cuối cùng cần đến nằm ở mạch 3); liên kết viewer.
- **Tài liệu tham khảo (7-08):** UML §12.1, §14.1 (trước buổi học); §14.2, §14.3, §14.4.1, §9.2, §12.2 (sau buổi học); §14.4.2–14.4.4, §12.3 (mở rộng); dòng chữ "Bài 06: Học bằng hạ gradient ngẫu nhiên, chính quy hóa và tính ổn định".
- **Câu nối sang bài sau** (ghi chú diễn giả 7-08): Bài 06 so hai cách dùng dữ liệu có cùng phép cập nhật và hỏi khi nào tối thiểu hóa trên $S$ cũng kiểm soát $L_D$.

## 10. Bảng thuật ngữ Việt–Anh của deck

Theo ghi chú và `thuat-ngu.md`; tiếng Anh trong ngoặc ở lần dùng đầu trên trang nội dung (trang ghi ở cột cuối).

| Tiếng Việt | Tiếng Anh | Lần đầu trên mặt trang |
|---|---|---|
| tính chất tháp | tower property | 1-02 |
| lấy ra đại lượng đã biết | taking out what is known | 1-02 |
| hàm lỗi logistic | logistic loss | 1-06 |
| hạ gradient (GD) | gradient descent | 1-06 |
| hạ gradient ngẫu nhiên (SGD) | stochastic gradient descent | 1-06 |
| độ chênh tối ưu | suboptimality | 2-01 |
| hàm lỗi bản lề | hinge loss | 2-02 |
| tập lồi | convex set | 2-02 |
| bất đẳng thức lồi hữu hạn (còn gọi là bất đẳng thức Jensen hữu hạn) | finite Jensen inequality | 2-02 (tên tiếng Việt thứ hai thay cho tiếng Anh, như ghi chú) |
| dưới gradient | subgradient | 2-03 |
| dưới vi phân | subdifferential | 2-03 |
| phép chiếu Euclid | Euclidean projection | 3-01 |
| bất đẳng thức biến phân | variational inequality | 3-02 |
| gradient ngẫu nhiên | stochastic gradient | 3-03 |
| oracle gradient ngẫu nhiên | stochastic gradient oracle | 3-03 |
| điểm lặp trung bình | averaged iterate | 3-04 |
| lịch sử | history, filtration | 3-06 |
| hầu chắc chắn | almost surely | 3-06 |
| cực tiểu địa phương | local minimum | 5-01 |
| luật số lớn | law of large numbers | 5-02 |
| điểm lặp cuối | last iterate | 5-03 |
| thuật toán học có nguồn ngẫu nhiên riêng | randomized learning algorithm | 6-01 |
| hàm điểm số | score function | 6-01 |
| lô nhỏ | mini-batch | 6-04 |
| kích thước lô | batch size | 6-04 |

Chỉ ở ghi chú diễn giả (tiếng Anh trong ngoặc ở đó): bất đẳng thức dưới gradient (subgradient inequality), hạ gradient dùng dưới gradient (subgradient descent), xáo trộn lại sau mỗi vòng (random reshuffling), vòng qua dữ liệu (epoch), bổ đề đóng băng (freezing lemma), mức sàn sai số (error floor), hàm trơn ($\beta$-smooth), lồi mạnh ($\lambda$-strongly convex), bình phương tối thiểu (least squares), hàm lỗi thay thế (surrogate loss). Đã có ở Bài 01–04, không nhắc tiếng Anh: rủi ro thực nghiệm, sai số tối ưu thực nghiệm, sai số ước lượng, hàm lỗi bình phương, rủi ro kì vọng (population risk, expected risk; ghi chú diễn giả 7-01 nhắc lại nếu cần).

## 11. Rủi ro và điểm cần điều phối viên quyết định

1. **Bài tập 05.5(b) thay cho 05.5(a) ở 6-06.** Phần (a) có cụm nguồn gốc "(giá trị giả định, khác $\sigma^2=15$ của Ví dụ 05.15)" mà mặt trang không được chép ("giá trị giả định" bị cấm) và câu chữ của (a) cộng bảng vượt trần 60. Phần (b) ngắn hơn (51 âm tiết), dùng cả $\sigma^2=3$ và $\sigma^2=15$, nối thẳng với Ví dụ 05.15. Đề xuất sửa `exercises.md` ở mục 13.
2. **Số trang 55, đúng trần** (lý do ở mục 3). Phương án rút còn 53, không bỏ bước nào của hành trình khái niệm: (a) gộp 7-04 và 7-05 thành một trang khoảng $103$ âm tiết: vượt $1{,}5$ lần trần, không khuyến nghị; (b) bỏ 5-04 (Bài tập 05.3(c)) và đưa lời giải vào ghi chú diễn giả 5-03: cụm giả thiết mất bài tập trên mặt trang, và giả thiết độc lập của các lần rút chỉ còn ở ghi chú diễn giả; (c) bỏ 3-08 (Bài tập 05.3(b)): mạch 3 mất bài tập. Khuyến nghị giữ 55.
3. **Kết quả không có trang ý tưởng chứng minh riêng:** Mệnh đề 05.3, 05.5 (sự kiện tập trung, chứng minh một đến ba dòng, lộ trình ở ghi chú diễn giả 2-04, 2-06); Bổ đề 05.8 (công cụ, phác thảo; lộ trình ở ghi chú diễn giả 3-02); Bổ đề 05.12 (công cụ, phác thảo; cơ chế ở trang kỹ thuật 3-07, như Bổ đề 02.5 trên trang kỹ thuật của deck Bài 02); Hệ quả 05.16 (hệ quả trực tiếp, một dòng ở ghi chú diễn giả 4-09, như Hệ quả 03.18); Mệnh đề 05.20 (đọc thêm). Bốn kết quả chính có trang riêng: Mệnh đề 05.13 (4-02), Định lý 05.14 (4-04), Hệ quả 05.15 (4-08), Hệ quả 05.19 (6-03). Nếu điều phối viên muốn Bổ đề 05.8 có trang ý tưởng chứng minh (blueprint Lemma 5.1 [S]), deck lên 56: cần một phương án của điểm 2.
4. **Định nghĩa 05.6 (trơn, lồi mạnh) chỉ ở ghi chú diễn giả 2-06.** Ghi chú giữ nó ở §4 vì Bài 06, 08 dẫn (#29 của `lec-05/review-log.md`); deck Bài 05 không dùng nó trên mặt trang nào, và thêm một dòng đưa 2-06 lên khoảng 70. Deck Bài 06, 08 nhắc lại khi dùng. Bảng bài tập về nhà có Bài tập 05.8(c), 05.12 dùng định nghĩa này; ghi chú bài giảng có đủ.
5. **Thứ tự trong §6:** Thuật toán 05.9 (GD) đứng trước Định nghĩa 05.10 trong ghi chú; deck đặt hai thuật toán chung trang 3-04, sau Định nghĩa 05.10 và Ví dụ 05.5, vì giả mã SGD cần oracle. Cùng mục §6; không trang nào trước 3-04 dùng Thuật toán 05.9. Đề nghị chấp nhận và ghi vào `review-log.md`.
6. **Câu hỏi cuối buổi §13 thành trang ví dụ 7-01** (cuối mạch 6, sau bài tập §12 nên thứ tự mục vẫn tăng), không thành câu hỏi tự kiểm tra như deck Bài 04. Lý do: bản giao việc đặt trọng tâm "phân biệt sai số tối ưu hóa với rủi ro"; ví dụ là phép tính tay duy nhất của ghi chú cho thấy $\operatorname{opt}_S\approx0{,}0025$ trong khi sai số ước lượng $\approx0{,}9025$. Tiêu đề "Ví dụ: …" theo quy định (trường hợp đã giải của ghi chú là trang ví dụ).
7. **Khối ứng dụng §3 gộp vào trang dẫn nhập 1-06**, cùng nội dung với Câu hỏi mở đầu; thông số $\lVert w\rVert\le5$, $\lVert x\rVert\le1$ chỉ trên 4-09 (và ghi chú diễn giả 1-06). Ví dụ 05.1 chung trang với thiết lập §1 (2-01).
8. **Mục tiêu (1-03)** giữ đủ năm mục tiêu của ghi chú theo thứ tự, rút câu chữ trong trần $80$ (đếm $79$): mục tiêu 2 bỏ "phát biểu" và "cho cách rút một quan sát ngẫu nhiên có hoàn lại"; mục tiêu 3 viết "kể cả với xác suất cao"; mục tiêu 4 viết "bản ngẫu nhiên" cho hạ gradient ngẫu nhiên; mục tiêu 5 không liệt kê ba giả thiết. Ghi chú diễn giả nêu đủ các ý đã rút.
9. **Bài tập tổng hợp 7-04: 68 âm tiết, vượt trần 60** (ngoại lệ có lý do: câu chữ của Bài tập 05.5(d) và dòng dữ kiện "như Ví dụ 05.14"; dưới $1{,}5$ lần trần; tiền lệ $73$ của deck Bài 01). Phương án khác: Bài tập 05.4(b) làm bài tổng hợp (khoảng 45 âm tiết đề, ghép Định lý 05.14 với mức sàn của độ dài bước cố định), nhưng chỉ dùng kiến thức mạch 4.
10. **Điểm toán học #3 còn mở** (Ví dụ 05.12): 5-03 theo đề xuất của người kiểm, không chép câu kết luận của ghi chú (xem đầu tệp).
11. **Công thức cần đo ở 390 px** (ngắt `aligned` chỉ khi tràn): 1-02 (khai triển bình phương), 2-02 (định nghĩa hàm lồi với lượng từ), 3-02 (chuỗi hai bất đẳng thức), 3-06 (hai kì vọng có điều kiện trên một dòng; có thể tách hai dòng), 3-07, 4-01 (hai công thức), 4-03, 4-05, 6-04 (ba đẳng thức trên một dòng; gần như chắc chắn cần ngắt); bảng 3-05, 6-05, 7-02, 7-07 đặt trong `.table-scroll`; bảng chín ô 3-08 viết bằng bảng HTML $3\times3$ hoặc `array` KaTeX.
12. **Trang sát trần** (đếm bằng script, mục 15): 3-08 (57, câu chữ bài tập), 4-03 (57, định lý chính), 1-02, 3-04, 6-02, 7-06 (56), 4-08 (55); 1-03 ($79$/80), 7-02 ($79$/80); 7-04 ($68$, ngoại lệ ở điểm 9). Người viết deck không thêm chữ trên các trang này; điều phối viên đếm lại trên deck. 36 trong 46 trang có mặt trang được đếm ở 31–54 âm tiết, trung vị khoảng 49.
13. **Ghi chú diễn giả dẫn kết quả về sau hoặc bài sau** ở 1-01, 1-05 (câu trả lời theo mạch), 3-07, 4-05 (kỹ thuật trở lại ở các bài sau, không nêu số bài), 7-08 (Bài 06): chỉ trong ghi chú diễn giả, không trên mặt trang.
14. **Liên kết hai chiều:** trang 7-07 của deck Bài 04 nhận liên kết tới `lecture-05-ha-gradient-ngau-nhien.html`; trang 7-08 ở đây là dòng chữ không liên kết cho đến khi deck Bài 06 có tên tệp.
15. **"Tiến bộ" và "nhiễu bước"** (từ của bản giao việc) không phải thuật ngữ của ghi chú; mặt trang viết hai số hạng bằng công thức, ghi chú diễn giả dùng "phần giảm do gradient" và "phần nhiễu" như Câu hỏi mở đầu của ghi chú.
16. **Trang 2-03 dẫn UML §14.2** cho khẳng định $\partial F(w)\ne\varnothing$ (ghi chú cũng dẫn như vậy); mặt trang không có dẫn nguồn, chỉ ghi chú diễn giả.

17. **Câu chữ Bài tập 05.3(b) trên 3-08:** cụm "bằng vế phải của (a)" viết thành "bằng vế phải của Bổ đề 05.12(c)", vì phần (a) (chứng minh tổng kép) không lên mặt trang; vế phải của (a) và của Bổ đề 05.12(c) với $t=2$ là cùng một đại lượng $\mathbb E\langle\psi(w_2),w_2-u\rangle$; ghi chú diễn giả 3-08 nói rõ. Dòng dữ kiện "Thiết lập của Ví dụ 05.6, $u=w^*$" thay bốn gạch đầu dòng thiết lập của bài (các số đã có trên 3-05). Tương tự, 5-04 mở bằng "trong thiết lập của Bài tập 05.3(b)" và 6-06 bằng dòng thiết lập của Ví dụ 05.15. Đề nghị điều phối viên chấp nhận.

## 12. Bảng đối chiếu trang → mục và khối của ghi chú

Cột "Đưa vào" ghi kí hiệu, thuật ngữ hoặc kết quả xuất hiện lần đầu trên mặt trang (định nghĩa hoặc "Nhắc lại:"/"Kí hiệu:"), để kiểm quy tắc định nghĩa trước khi dùng.

| Trang | Mục ghi chú | Khối (số của ghi chú) | Đưa vào |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §7; §11 | — (bằng lời) | — |
| 1-02 | Kiến thức tiên quyết; Câu hỏi ôn nhanh | Định nghĩa 04.1, 04.2; (O2); Bổ đề 02.2; (T1) (nhắc lại) | $\operatorname{opt}_S$, $L_S$, $L_D$, $W$, $\epsilon_{\mathrm{opt}}$, (O2), Markov, sai số ước lượng, (T1), $D$, $m$, $\langle\cdot,\cdot\rangle$, $\lVert\cdot\rVert$, khai triển bình phương, tính chất tháp, lấy ra đại lượng đã biết |
| 1-03 | Mục tiêu học tập | — | — |
| 1-04 | toàn bài; §14 | — | — |
| 1-05 | đoạn mở đầu | — | — |
| 1-06 | Câu hỏi mở đầu và hai đoạn sau; §3 khối ứng dụng | — | GD, SGD, hàm lỗi logistic, $T$ |
| 2-00 | §1–§4 | — | — |
| 2-01 | §1, §3 | tám thành phần; Ví dụ 05.1 | $F$, $S$ cố định, $\mathbb R^p$, $\xi_t$, độ chênh tối ưu, $u$, $z_i$, $\ell(w,z)$, $x$, $y$ |
| 2-02 | §4 | Định nghĩa 05.1; bất đẳng thức lồi hữu hạn | tập lồi, hàm lồi, $\alpha$, bất đẳng thức lồi hữu hạn, hàm lỗi bản lề |
| 2-03 | §4 | Định nghĩa 05.2; ba đoạn sau | dưới gradient, $\partial F(w)$, dưới vi phân, cực tiểu toàn cục |
| 2-04 | §4 | Mệnh đề 05.3; Ví dụ 05.3 | Mệnh đề 05.3 |
| 2-05 | §4 | Ví dụ 05.2 | $\tilde y$, điểm gãy, $w_0$ |
| 2-06 | §4 | Định nghĩa 05.4; Mệnh đề 05.5; ví dụ sau Định nghĩa 05.4 | $G$-Lipschitz, $G$, $U$ |
| 2-07 | §4 | Bài tập 05.1(d) | — |
| 3-00 | §5–§6 | — | — |
| 3-01 | §5 | Định nghĩa 05.7; Ví dụ 05.4 | $\operatorname{proj}_W$, $\theta$, $B$, quả cầu |
| 3-02 | §5 | Bổ đề 05.8 | $\pi$, bất đẳng thức biến phân |
| 3-03 | §6 | Định nghĩa 05.10; Ví dụ 05.5 Bước 1 | $\xi$, $P_\xi$, $\varphi$, $\psi$, (G1), (G2), oracle gradient ngẫu nhiên |
| 3-04 | §6 | Thuật toán 05.9, 05.11 | $v(w)$, $v_t$, $g_t$, $\eta$, $w_t$, $\bar w_T$, điểm lặp trung bình |
| 3-05 | §6; Phụ lục D | Ví dụ 05.6; Ví dụ 05.5 Bước 2 | $G=4$ (cận viết bằng số; $C_x$, $C_y$ chỉ ở ghi chú diễn giả), $i_t$, $w^*$, $\min_WL_S$ |
| 3-06 | §6 | Bổ đề 05.12; Định nghĩa 05.10 (lịch sử) | $\mathcal F_t$, lịch sử, hầu chắc chắn |
| 3-07 | §6; Phụ lục B | chứng minh Bổ đề 05.12 | $a_t$ |
| 3-08 | §6 | Bài tập 05.3(b) | — |
| 4-00 | §7 | — | — |
| 4-01 | §7 | Mệnh đề 05.13 và đoạn trước | $w^+$, Mệnh đề 05.13 |
| 4-02 | §7 | chứng minh Mệnh đề 05.13; Ví dụ 05.7 | — |
| 4-03 | §2 (C), §7 | Định lý 05.14 | (C), Định lý 05.14 |
| 4-04 | §7 | chứng minh Định lý 05.14 | $\Delta_t$ |
| 4-05 | §7 | chứng minh Định lý 05.14 (Bước 2, 5) | $a_t$, $b_t$, $c_t$ (cục bộ trên trang) |
| 4-06 | §7 | Ví dụ 05.8 Bước 3; đoạn sau Hệ quả 05.15 | $R$, $\eta^*$ |
| 4-07 | §7 | Hệ quả 05.15 | $F_R$, $\epsilon$ |
| 4-08 | §7 | chứng minh Hệ quả 05.15; Ví dụ 05.8 Bước 1–2 | — |
| 4-09 | §7; §3 | Hệ quả 05.16; Ví dụ 05.9 | Hệ quả 05.16 |
| 4-10 | §7 | Bài tập 05.4(c) | $Q(\eta,T)$, $\hat G$ |
| 5-00 | §8 | — | — |
| 5-01 | §8 | Ví dụ 05.10 | cực tiểu địa phương |
| 5-02 | §8 | Ví dụ 05.11 | $a_t$ (thừa số của ví dụ) |
| 5-03 | §8 | Ví dụ 05.13, 05.12; đoạn cuối §8 (ghi chú diễn giả) | $\tilde F$, điểm lặp cuối |
| 5-04 | §6, §7 | Bài tập 05.3(c) | — |
| 6-00 | §9–§10 | — | — |
| 6-01 | §9 | Định nghĩa 05.18 và hai đoạn sau | $A_m$, $A(S;\xi)$, $\mathcal Z$, $\mathcal H$, hàm điểm số, $h_w$ |
| 6-02 | §9 | Hệ quả 05.19 | $s$, $v(w,z)$, $\delta'$, $\operatorname{opt}_s$ |
| 6-03 | §9 | chứng minh Hệ quả 05.19; Ví dụ 05.14 | — |
| 6-04 | §10 | Mệnh đề 05.20; Ví dụ 05.16 (ghi chú diễn giả) | lô nhỏ, $b$, $\bar\xi$, $\varphi_b$, $\sigma^2$, $G_F$, $G_b$, $e_j$ |
| 6-05 | §10 | Ví dụ 05.15 | $T(b)$ |
| 6-06 | §10 | Bài tập 05.5(b) | — |
| 7-00 | §11–§14 | — | — |
| 7-01 | §13 | câu hỏi cuối buổi và lời giải; đoạn sau | — |
| 7-02 | §7–§10 | Mệnh đề 05.13, Định lý 05.14, Hệ quả 05.15, 05.16, 05.19 | — |
| 7-03 | §11 | — | — |
| 7-04 | Bài tập 05.5 | Bài tập 05.5(d) (đề) | $k$ |
| 7-05 | Bài tập 05.5 | Bài tập 05.5(d) (lời giải) | $X_j$ |
| 7-06 | §6, §7 | — | — |
| 7-07 | §12 | `exercises.md` | — |
| 7-08 | §13, §14 | — | — |

## 13. Đề xuất sửa ghi chú và tệp bài tập (không sửa; chờ điều phối viên và tác giả)

Không thấy lỗi toán học trong các khối deck dùng; mọi con số của ví dụ và sáu bài tập trên mặt trang đã tính lại (mục 5) và khớp ghi chú, tệp bài tập.

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất |
|---|---|---|---|---|
| nhẹ | `exercises.md`, Bài tập 05.5(a), dòng 446 | Cụm nguồn gốc "(giá trị giả định, khác $\sigma^2=15$ của Ví dụ 05.15)" trái quy tắc không ghi câu nguồn gốc (cùng loại với đề xuất số 6 của Bài 01) | "Lấy $\sigma^2=3$ (giá trị giả định, khác $\sigma^2=15$ của Ví dụ 05.15)." | "Lấy $\sigma^2=3$ (thay cho $\sigma^2=15$ của Ví dụ 05.15)." Deck không dùng phần (a) trên mặt trang (mục 11, điểm 1). |
| nhẹ | ghi chú, Ví dụ 05.12, dòng 1030 | Điểm toán học #3 (còn mở cho tác giả): câu kết luận lập luận theo $f(w_t)$ trong khi Định lý 05.14 chặn $f(\bar w_T)$ | `planning/diem-toan-can-doc-2026-11-13.md`, mục 3 | Như đề xuất đã ghi; deck theo đề xuất đó ở 5-03. |
| nhẹ | ghi chú, Nhận xét 05.17 (dòng 960) và Phụ lục C (dòng 1405) | Hai cách ghi một số: "không quá $0{,}2281$" và "$\approx0{,}2280$"; giá trị $0{,}228009$ | `num.py` | Không cần sửa (hai cách ghi nhất quán); deck dùng "$0{,}2281$" của Nhận xét 05.17 ở ghi chú diễn giả. |

## 14. Danh sách kỹ thuật đã giới thiệu đến hết Bài 05

| Kỹ thuật | Bài, trang (lần đầu) | Dạng | Trong deck Bài 05 |
|---|---|---|---|
| Tính tuyến tính của kì vọng | Bài 01, `L01-3-03` | một dòng | ghi chú diễn giả 6-04 (phần không chệch của gradient lô) |
| Bất đẳng thức hợp | Bài 01, `L01-4-04` | trang riêng | không dùng |
| Chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ | Bài 01, `L01-6-07` | trang riêng | không dùng |
| Tối thiểu hóa từng điểm rồi lấy kì vọng | Bài 01 | một dòng | không dùng |
| Phương pháp Chernoff | Bài 02, `L02-3-01` | trang riêng | không dùng (chỉ bất đẳng thức Markov, nhắc lại ở 1-02) |
| Dây cung của hàm lồi và Taylor bậc hai tại $0$ | Bài 02 | một dòng | không dùng |
| Đảo cận đuôi thành bán kính và cỡ mẫu | Bài 02, `L02-4-04` | trang riêng | không dùng (đảo $RG/\sqrt T\le\epsilon$ thành số vòng lặp ở 4-08 là phép tính một dòng) |
| Chia xác suất thất bại $\delta/K$ cho từng giả thuyết | Bài 02, `L02-5-05` | trang riêng | không dùng |
| Bước tất định trên biến cố đại diện | Bài 02, `L02-5-11` | trang riêng | không dùng |
| Cận dưới và cận trên cho chiều VC | Bài 03, `L03-2-04` | trang riêng | không dùng |
| Thứ tự trên đường thẳng cho cận trên | Bài 03 | một dòng | không dùng |
| Hàm afin giữ tổ hợp lồi (với phân hoạch Radon) | Bài 03 | một dòng | không dùng |
| Tách theo nhãn của điểm cuối rồi quy nạp | Bài 03 | một dòng | không dùng |
| Đối xứng hóa và mẫu bóng | Bài 03, `L03-5-06` | trang riêng | không dùng |
| Hàm tăng trưởng thay cho số giả thuyết | Bài 03, `L03-5-07` | trang riêng | không dùng |
| Bất đẳng thức tiếp tuyến $\ln u\le u/u_0+\ln u_0-1$ để giải cỡ mẫu | Bài 03 | một dòng (ghi chú diễn giả) | không dùng |
| Thêm bớt kì vọng rồi bình phương; mỗi số hạng chéo một lý do | Bài 04, 3-03 | một dòng | gần với đẳng thức $\mathbb E\lVert\varphi\rVert^2=\lVert\psi\rVert^2+\mathbb E\lVert\varphi-\psi\rVert^2$ (ghi chú diễn giả 3-03, 6-04), không nhắc tên |
| Chia xác suất thất bại theo trọng số | Bài 04, 4-04 | trang riêng | không dùng |
| Chọn $\delta=1/m$ để bỏ $\delta$ khỏi đầu vào | Bài 04, 5-03 | một dòng | không dùng |
| Lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện | Bài 04, 6-02 | một dòng | không dùng (6-01 nói bảo đảm theo $\xi$ với mọi $S$ cố định đúng theo cặp $(S,\xi)$, một câu của Định nghĩa 05.18) |
| **Kì vọng có điều kiện theo lịch sử** (tính chất tháp, lấy ra đại lượng đã biết, lần rút mới độc lập) | Bài 05, 3-07 | trang riêng | dùng ở 3-06, 3-08, 4-04 Bước 3, 5-04; dùng lại ở Bài 07, 08, 10 |
| **Tổng triệt tiêu và trung bình các điểm lặp** | Bài 05, 4-05 | trang riêng | dùng ở 4-04, 4-09; dùng lại ở Bài 07, 08, 10 (theo ghi chú các bài đó: "tổng triệt tiêu", "bất đẳng thức một bước", Định lý 05.14) |
| Cân hai số hạng, $a/\eta+b\eta\ge2\sqrt{ab}$ | Bài 05, 4-08 | một dòng | — |
| Số hạng chéo bằng $0$ cho véc-tơ không tương quan | Bài 05, 6-04 | một dòng | — |

Mã trang của Bài 01–04 lấy theo mục 14 của storyboard Bài 04; nếu deck đổi mã, người viết deck Bài 05 không cần mã (deck nhắc kỹ thuật bằng tên). Deck Bài 06 trở đi nhắc lại "kì vọng có điều kiện theo lịch sử" và "tổng triệt tiêu và trung bình các điểm lặp" bằng tên, một dòng "Nhắc lại:".

## 15. Mật độ mặt trang đo bằng script

Đếm bằng `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-05/storyboard/count.py` (bản sao script của storyboard Bài 04) trên văn bản dự kiến của mục 6, theo cách của `deck_check.py`: token cách nhau bởi khoảng trắng, có chữ cái hoặc chữ số; bỏ tiêu đề, công thức `$…$`, chỉ dẫn `{{…}}`, dấu fragment; nhãn "(G1)", "(C)", "(a)", số khối như "05.14" và tiếng Anh trong ngoặc được đếm (quyết định Bài 01: số viết trong câu có tính). Ô bảng chỉ chứa số hoặc công thức không đếm; dòng "Bảng: …" viết tắt trong mục 6 (3-05, 6-05) chỉ chứa số và nhãn cột, đếm là một dòng. Mỗi gạch đầu dòng là một dòng; mỗi công thức hiển thị là thêm một dòng (số 0 trong cột theo dòng); một bảng là một dòng. Token có gạch nối như "mô-men" đếm là một, nên số thật cao hơn một ở các trang có từ này (3-03, 5-02, 7-06). Trang tổng quan và trang tiêu đề mạch không đếm (bìa: luận điểm 52 âm tiết; hộp Vấn đề trung tâm 20; câu dẫn mạch 19–25). Kết quả đầy đủ: `counts.txt` cùng thư mục.

| Trang | Tổng | Dòng | Theo dòng | Trang | Tổng | Dòng | Theo dòng |
|---|---:|---:|---|---|---:|---:|---|
| 1-02 | 56 | 5 | 17; 8; 8; 7; 16 | 4-06 | 49 | 5 | 11; 9; 10; 5; 14 |
| 1-03 | 79 | 5 | 18; 12; 15; 16; 18 | 4-07 | 45 | 6 | 15; 4; 0; 5; 12; 9 |
| 1-06 | 53 | 5 | 10; 9; 15; 10; 9 | 4-08 | 55 | 6 | 15; 16; 7; 9; 8; 0 |
| 2-01 | 44 | 5 | 12; 11; 7; 3; 11 | 4-09 | 46 | 6 | 10; 7; 6; 0; 15; 8 |
| 2-02 | 54 | 5 | 15; 11; 13; 0; 15 | 4-10 | 39 | 6 | 0; 12; 13; 2; 0; 12 |
| 2-03 | 42 | 5 | 5; 12; 0; 14; 11 | 5-01 | 31 | 5 | 7; 8; 5; 4; 7 |
| 2-04 | 40 | 6 | 12; 5; 1; 1; 10; 11 | 5-02 | 40 | 5 | 4; 9; 11; 9; 7 |
| 2-05 | 42 | 6 | 12; 0; 12; 9; 1; 8 | 5-03 | 44 | 6 | 8; 4; 14; 4; 7; 7 |
| 2-06 | 48 | 5 | 9; 14; 8; 6; 11 | 5-04 | 49 | 5 | 16; 16; 4; 8; 5 |
| 2-07 | 35 | 5 | 13; 6; 7; 5; 4 | 6-01 | 54 | 5 | 20; 7; 12; 6; 9 |
| 3-01 | 49 | 5 | 12; 17; 8; 7; 5 | 6-02 | 56 | 6 | 15; 13; 10; 8; 10; 0 |
| 3-02 | 54 | 6 | 10; 13; 15; 3; 0; 13 | 6-03 | 44 | 5 | 9; 9; 8; 14; 4 |
| 3-03 | 52 | 4 | 18; 14; 10; 10 | 6-04 | 43 | 5 | 11; 11; 0; 10; 11 |
| 3-04 | 56 | 6 | 7; 17; 0; 6; 11; 15 | 6-05 | 49 | 5 | 2; 7; 20; 20 |
| 3-05 | 43 | 6 | 14; 4; 2; 4; 19 | 6-06 | 51 | 5 | 10; 15; 12; 10; 4 |
| 3-06 | 50 | 6 | 8; 12; 18; 10; 0; 2 | 7-01 | 31 | 6 | 3; 4; 4; 1; 7; 12 |
| 3-07 | 51 | 5 | 12; 0; 12; 11; 16 | 7-02 | 79 | 1 | (bảng 79) |
| 3-08 | 57 | 6 | 12; 20; 10; 3; 3; 9 | 7-03 | 46 | 5 | 7; 8; 13; 12; 6 |
| 4-01 | 51 | 6 | 7; 0; 17; 9; 18; 0 | 7-04 | 68 | 5 | 5; 19; 17; 12; 15 |
| 4-02 | 46 | 5 | 9; 12; 8; 11; 6 | 7-05 | 35 | 5 | 6; 12; 1; 10; 6 |
| 4-03 | 57 | 6 | 14; 17; 10; 6; 0; 10 | 7-06 | 56 | 4 | 14; 15; 12; 15 |
| 4-04 | 45 | 5 | 15; 5; 7; 7; 11 | 7-07 | 49 | 2 | 10 (bảng 39) |
| 4-05 | 43 | 5 | 8; 0; 11; 5; 19 | 7-08 | 51 | 5 | 6; 9; 5; 16; 15 |

Trần: 60 cho trang nội dung, 80 cho 1-03, 7-02, 7-07; mọi dòng ≤ 20; mọi trang ≤ 6 dòng. Kết quả: một trang vượt trần, 7-04 ($68$; ngoại lệ có lý do ở mục 11, điểm 9: câu chữ của Bài tập 05.5(d), dưới $1{,}5$ lần trần); không dòng nào vượt 20; không trang nào quá 6 dòng. Trung vị $49$; 36 trong 46 trang được đếm ở 31–54 âm tiết, còn biên cho các sửa của cổng duyệt. Trang bài tập giữ câu chữ của `exercises.md` (2-07, 3-08, 4-10, 5-04, 6-06, 7-04).

## 16. Đối chiếu với deck đã viết (người viết deck, 2026-11-15)

Deck: `2627-1/lecture-05-ha-gradient-ngau-nhien.html`, 55 trang, hình `img/lec-05/{duoi-gradient,phep-chieu,ba-buoc-sgd,do-dai-buoc,khong-loi}.svg` (dựng bằng script nháp `…/scratchpad/lec-05/writer/figs.py` từ công thức của ghi chú; mọi số trên nhãn khớp mục 5). Mặt trang và ghi chú diễn giả của deck là bản cuối; câu dự kiến ở mục 6 chỉ còn giá trị tham chiếu. Số âm tiết mục 15 là số trước khi viết; số cuối ở cuối mục này.

**Đánh số lại theo quyết định của điều phối viên (T13).** Trang câu hỏi cuối buổi §13 (cũ `6-07`) thành `7-01`, trang nội dung đầu của mạch Tổng kết; các trang Tổng kết cũ `7-01…7-07` thành `7-02…7-08`. Mạch 6 ứng với §9–§10 (7 trang), mạch 7 với §11–§14 (9 trang). Mọi mã trang trong tệp này đã đổi theo (trừ mã của deck Bài 01, 04).

**Áp dụng quyết định của cổng duyệt.**
- N1, L1: luận điểm bìa và ghi chú diễn giả 1-01 viết theo bất đẳng thức một bước (tăng không quá một số hạng tỉ lệ với $\eta$, có thể âm, cộng một số hạng tỉ lệ với $\eta^2$), không còn "kéo về phía điểm so sánh".
- T1, T2, L11, L22: F4 trục dọc $[0;0{,}9]$, nhãn đường "số hạng thứ nhất", "số hạng thứ hai", "tổng" (không đặt tên "khoảng cách", "nhiễu"); F3 trục $y\in[-1{,}3;0{,}2]$ chứa cả elip, khung phóng to bắt buộc ($x\in[0{,}54;0{,}94]$, $y\in[-0{,}85;-0{,}45]$), nhãn số chỉ trong khung.
- T3: 2-02 có dòng "**Ví dụ.** $f(w)=(w^2-1)^2$ …, đồ thị nằm trên dây cung" trước Định nghĩa 05.1.
- T4: câu nối trên mặt trang ở 3-03 (oracle thay $\nabla L_S$), 3-06 (cần trung bình của $g_t$ khi biết lịch sử), 4-09 (GD là oracle tất định), 6-04 (Ví dụ 05.9 so một quan sát với cả tập).
- T5: "Trực quan." 4-03 đọc vế phải (khoảng cách ban đầu chia cho tổng độ dài bước $\eta T$, cộng phần $\eta G^2/2$ mỗi bước góp); 6-02 bằng lời, trước dòng giả thiết ("một đại lượng không âm có trung bình nhỏ thì lớn với xác suất nhỏ"). Dòng "Bảo đảm:" 4-03 nêu đại lượng được chặn và "hàm mà oracle không chệch".
- T6, L5: Hệ quả 05.19 trên 6-02 có $G>0$, $w_1\in W$, Thuật toán 05.11, $\varphi(w,i)=v(w,z_i)$; Hệ quả 05.16 trên 4-09 có $R>0$, $u\in W$.
- T7, L6: bảng 7-02 giữ (C), (G1), (G2) ở hàng Hệ quả 05.15, $\ell\ge0$ lồi, $\lVert v\rVert\le G$ ở hàng Hệ quả 05.19, "kì vọng theo $\xi$" và "xác suất $\ge1-\delta'$". T12, L6: 7-03 viết bất đẳng thức một bước với "$\le$" và $u\in W$.
- T8: 7-05 dòng kết luận giữ điều kiện "nếu một lần tính hàm lỗi tốn ngang một gradient trên một quan sát". L10: tiêu đề "Bài tập: nhiều lần chạy độc lập, lời giải".
- T9: Bài tập 05.7 ở hàng mạch 5 của bảng 7-07. T11: ghi chú diễn giả 4-04 viết lại chỗ dùng giả thiết theo đề xuất.
- L2: $\pi=\operatorname{proj}_W(\theta)$ đặt trên 3-01. L4: dòng chi phí ở đầu 3-04. L7: 5-03 đổi thứ tự thẻ (Ví dụ 05.12 trái, 05.13 phải) theo thứ tự ghi chú; tiêu đề "Ví dụ: điểm lặp cuối và oracle chệch". L8: 3-08 ghi $u=w^*\approx(0{,}7473;-0{,}6645)$ và nói rõ cột trung bình theo hàng. L9: 5-04 thêm "mà vế trái bằng $0$". L12: câu hỏi 4 của 7-06 tả cách rút ("Rút không hoàn lại trong mỗi vòng qua dữ liệu (random reshuffling) …"). L13: mục tiêu giữ "trên hàm lồi" và "cho cách rút có hoàn lại" (80 âm tiết). L14: câu hỏi 1-06 có vế "và cần bao nhiêu bước". L15: 6-06 ghi "(Hệ quả 05.16)". L16: ghi chú diễn giả 2-01, 7-08 và các trang tiêu đề mạch đã rút (deck_lint: mọi trang ≤ 150, trang tiêu đề mạch ≤ 100 theo deck_check). L17: bảng mục 7 hàng "Dưới gradient" đọc là "2-03 ($\lvert w\rvert$: mọi $\lvert v\rvert\le1$ cho cận dưới tại $0$)". L18: dòng dẫn mạch 2, 4 theo đề xuất. L19: ghi chú 1-04, 1-06, 7-00 bỏ tương phản và mạch làm chủ ngữ. L20: ghi chú 3-07 nối với kỹ thuật lấy điều kiện rồi bỏ điều kiện của Bài 04. L21: 2-06 thêm "**Ý nghĩa:** theo (b), $G$ chặn độ dài của mọi dưới gradient trên $U$"; 3-06 viết (a) là "$w_t\in W$ là hàm đo được của $\xi_1,\ldots,\xi_{t-1}$"; 6-01 giữ điều kiện đo được.
- Khung (tin nhắn điều phối viên): thẻ meta viewport `width=device-width,initial-scale=1`; mọi số trên hình mà mặt trang dùng đều có trong chữ trên mặt trang (3-01, 3-05, 4-06, 5-01); tiêu đề có kí hiệu viết bằng KaTeX ("Bài tập: ước lượng sai hằng số $G$", "Ví dụ: $\operatorname{opt}_S$ nhỏ, $L_D$ lớn").

**Lệch storyboard và lý do (ngoài các điểm trên).**
- Mật độ thực tế (chữ và KaTeX cỡ deck) làm 10 trang chạm chân trang ở bản đầu; sửa bằng rút chữ, không bỏ ý của ghi chú. Các ý chuyển xuống ghi chú diễn giả: 1-02 khai triển $\lVert a-a'\rVert^2$ (công thức có trên 4-01, ghi chú diễn giả 4-01 nêu tên); 2-03 dòng "$0\in\partial F(w)$ khi và chỉ khi …" (ghi chú diễn giả 2-03; hình F1 bên phải đọc đúng ý này); 3-04 "$\bar w_T\in W$ vì $W$ lồi" thành "$\bar w_T\in W$" trên mặt trang; 3-05 công thức $\varphi(w,i)$ và cận $2(1+1)\cdot1=4$ (mặt trang ghi "(G2) đúng với $G=4$"; công thức $\varphi(w,i)=\nabla_w\ell(w,z_i)$ có trên 3-03); 4-06 dòng "Diễn giải:" (thừa số $1{,}25$, $5{,}05$ ở ghi chú diễn giả; các số $0{,}1$; $0{,}125$; $0{,}505$ trên mặt trang); 5-01 độ dài bước $\eta\approx0{,}02778$, quy tắc "đạo hàm của nhánh nhỏ hơn" và bất đẳng thức $f(1)<f(w_t)+f'(w_t)(1-w_t)$ (ghi chú diễn giả); 7-01 đạo hàm $L_D'(w)=2w$; 7-02 công thức của Mệnh đề 05.13 và Định lý 05.14 trong cột kết quả (ghi chú diễn giả 7-02 ghi đủ).
- 3-08: thiết lập gộp vào câu "Câu hỏi:"; lời giải là một bảng ($i_1$, $w_2$, $\psi(w_2)$, chín ô, trung bình hàng) và một dòng "chín ô và cột hàng cùng có trung bình $0{,}8460$; $\mathbb EL_S(w_2)\approx0{,}5556$". Lý do: chân trang.
- 3-03: dòng Ví dụ 05.5 viết $\varphi(w,i)=\nabla_w\ell(w,z_i)$ thay cho công thức khai triển (gate T4 chuyển công thức sang 3-05; mặt trang 3-05 không đủ chỗ, nên công thức khai triển ở ghi chú diễn giả 3-05).
- 4-01: khai triển ở dòng "Trực quan." viết trong dòng, không hiển thị riêng (chân trang).
- Bước chứng minh trên các trang "Ý tưởng chứng minh" là danh sách đánh số, giả thiết ghi "(giả thiết …)" trong bước, không nhãn "Bước k" in đậm (nhãn ngoài danh sách hợp lệ).
- Bảng: không dùng lớp `.table-scroll` (không có trong `lecture-course.css`); bảng rộng cuộn ngang tại chỗ ở 390 px theo quy tắc sẵn có. Hình: không có chú thích `figcaption`; dữ liệu nằm trong `alt`, `<title>`/`<desc>` của SVG và trên mặt trang (theo khuôn deck 01–04).
- 6-04: dòng "**Kỹ thuật.**" giữ như mục 4 (một dòng, chỉ dùng ở đây). Kỹ thuật một dòng gần nó của Bài 04 ("thêm bớt kì vọng rồi bình phương") không có trang riêng ở Bài 04, nên không thêm "Nhắc lại:".
- 7-04: 66 âm tiết theo deck_check (68 theo deck_lint), vượt trần 60; ngoại lệ đã được điều phối viên chấp nhận (mục 11, điểm 9): câu chữ của Bài tập 05.5(d).
- 3-01: dòng Định nghĩa 05.7 dài 27 âm tiết, vượt mức 20 âm tiết/dòng; ngoại lệ (kiểm lại lượt 1 chấp nhận): tách dòng làm trang chạm chân trang, và câu giữ đủ "tồn tại vì $W$ đóng, duy nhất vì $W$ lồi".

**Kiểm tra máy (bản cuối).** `deck_lint.py`: 1 phát hiện, `L05-7-04 | SYLL60 | 68 > 60` (ngoại lệ trên). `footer_check.py`: 0 trang. `deck_check.py`: console 0, pageerrors 0, failed 0, không `.katex-error`; OVERFLOW 1–4 px ở 4-06, 4-07, 4-08, 4-09, 4-10, 5-02, 6-02, 6-03, 7-02, 7-03 đều là phần đuôi SVG của `\sqrt` (báo động giả đã biết). Liên kết `#/2`…`#/7` của 1-04 mở đúng trang tiêu đề mạch; →, ↓, Space chuyển trang.

**Âm tiết mặt trang cuối (deck_check).** 1-01 98 (bìa, không tính trần); 1-02 54; 1-03 80; 1-04 44; 1-05 20; 1-06 58; 2-00 26; 2-01 52; 2-02 58; 2-03 32; 2-04 39; 2-05 42; 2-06 56; 2-07 35; 3-00 37; 3-01 45; 3-02 51; 3-03 57; 3-04 54; 3-05 26; 3-06 57; 3-07 51; 3-08 52; 4-00 39; 4-01 48; 4-02 43; 4-03 57; 4-04 45; 4-05 43; 4-06 31; 4-07 40; 4-08 49; 4-09 49; 4-10 39; 5-00 32; 5-01 18; 5-02 43; 5-03 31; 5-04 51; 6-00 38; 6-01 54; 6-02 56; 6-03 47; 6-04 52; 6-05 58; 6-06 52; 7-00 19; 7-01 28; 7-02 74 (trần 80); 7-03 52; 7-04 66; 7-05 52; 7-06 56; 7-07 40; 7-08 36.

## 17. Sửa sau năm báo cáo duyệt (người sửa deck, 2026-11-15)

Đầu vào: `reviews/deck-{hoc-vien,toan-hoc,chuyen-gia,su-pham,mach-truyen}.md` và quyết định của điều phối viên ("chấp nhận mọi phát hiện", bảng quyết định thắng báo cáo) trong `review-log.md`. Mã: HV (học viên, theo thứ tự trong bảng), TH (toán học), CG (chuyên gia), SP (sư phạm), MT (mạch truyện, P1–P15). Deck vẫn 55 trang. Kiểm tra sau sửa: `deck_lint.py` 1 phát hiện (7-04, 68 âm tiết, ngoại lệ đã chấp nhận); `footer_check.py` 0 trang; `deck_check.py --shots` (thư mục nháp `…/lec-05/editor/chk`): console 0, pageerrors 0, failed 0, không `.katex-error`, OVERFLOW còn lại đều là đuôi SVG của `\sqrt`; `#/2`…`#/7`, →, ↓, Space, Esc chạy đúng; đã xem ảnh 1600×900 và 390×844 (cả `-end`) của mọi trang.

| Mã | Trang | Phát hiện (tóm tắt) | Kết quả |
|---|---|---|---|
| CG1, SP1, TH1 (nghiêm trọng) | 2-03 | $\partial F=\{\nabla F\}$ bỏ giả thiết lồi | đã sửa: "Với $F$ lồi, hữu hạn trên $\mathbb R^p$: $\partial F(w)\ne\varnothing$, và $\partial F(w)=\{\nabla F(w)\}$ khi $F$ khả vi tại $w$." |
| HV1, SP2, MT P1, TH10, CG11 | 1-01 | luận điểm hai câu, thiếu điều kiện | đã sửa: một câu, có hàm lồi, oracle không chệch, mô-men bậc hai bị chặn, độ dài bước theo $T$; ghi chú diễn giả viết lại, bỏ câu nói về chính luận điểm |
| HV2 | 1-06 | dòng ba quan sát không nêu ý, thứ tự số | đã sửa: "mọi bước SGD làm $L_S$ tăng ($0{,}0710$; $0{,}1021$; $0{,}0694$), GD làm giảm ($0{,}0614$)" |
| HV3 | 4-02 | $0{,}1764$, $0{,}0034$ không gọi tên | đã sửa: thêm dòng $\lVert(1,-1)-w^*\rVert^2\approx0{,}1764$, $\lVert w_3-w^*\rVert^2\approx0{,}0034$ |
| HV4 | 4-04 | thiếu bất đẳng thức tổng trước bước 5 | đã sửa: bước 4 có $\sum_t\mathbb E[F(w_t)-F(u)]\le\Delta_1/(2\eta)+\eta TG^2/2$ (trong dòng, vì chân trang) |
| HV5 | 4-09 | thiếu công thức hàm lỗi logistic | đã sửa: $\ell=\ln(1+e^{-\tilde y\langle w,x\rangle})$ ở dòng Ví dụ 05.9 |
| HV6, SP (5-01 so sánh) | 5-01 | (G1) hỏng không có lý do; thiếu "$>0{,}140625$" | đã sửa: dòng $f(1)=0<f(w_t)+f'(w_t)(1-w_t)$ và "$0{,}5>0{,}140625$"; "bước 3 của chứng minh" |
| HV7, TH4, CG7, SP4 | 4-03 | "Trực quan." sai lũy thừa, chỉ đọc lại phát biểu; dòng "Bảo đảm:" khó theo | đã sửa: "Theo kì vọng, mỗi bước tiến về phía $u$ ít nhất $F(w_t)-F(u)$ và trả thêm $\eta G^2/2$; tổng phần tiến bị chặn bởi $\lVert w_1-u\rVert^2/(2\eta)$"; "Bảo đảm: theo kì vọng theo $\xi_1,\ldots,\xi_{T-1}$, với $F$ là hàm mà oracle không chệch" |
| HV8, CG2 | 4-05 | $c_t\ge F(w_t)-F(u)$ như trên từng quỹ đạo | đã sửa: "(với SGD: theo kì vọng)" |
| HV9 | 3-05 | $w^*$ chưa gọi tên | đã sửa: "$\min_WL_S\approx0{,}06112$ tại $w^*\approx(0{,}7473;-0{,}6645)$" (dòng Diễn giải) |
| HV10 | 3-05 | "GD:" không nói từ $w_3$ | đã sửa: "bước GD từ $w_3$ cho $0{,}0614$" |
| HV11 | 3-08 | cột "hàng" khó hiểu | đã sửa: cột "trung bình hàng"; ghi chú diễn giả nói cột này là $\langle\psi(w_2),w_2-u\rangle$ |
| HV12 | 3-03/4-09 | hai nghĩa của $G$ không nối | đã sửa ở 4-09 (không đủ chỗ ở 3-03): "GD là oracle tất định …; (G2) thành $\lVert v(w)\rVert\le G$ (Mệnh đề 05.5)"; ghi chú diễn giả 4-09 nói hằng số Lipschitz đóng vai $G$ |
| HV13, CG13, MT P7 | 6-04, 3-07 | kỹ thuật Bài 04 không nhắc lại | đã sửa: 6-04 "**Nhắc lại:** thêm bớt kì vọng rồi bình phương (Bài 04) …" (quyết định); 3-07 dòng "Đẳng thức đầu" nhắc "lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện (Bài 04)" bằng tên, trang "Kỹ thuật." giữ (quyết định) |
| HV14 | 3-06 | 7 dòng | đã sửa: câu nối gộp vào "Trực quan."; 6 dòng |
| HV15 | 6-04 | công thức ba kết luận cuộn ở 390 px | đã sửa: ba kết luận viết trong dòng "Bảo đảm:" |
| HV16 | 2-05 | dòng điểm gãy vấp | đã sửa: "hai nhánh cùng bằng $0$; các véc-tơ …" |
| HV17 | 1-02, 6-01 | $p$, $\Xi$, $\mathcal Z$, $\mathcal H$ chưa nêu | đã sửa: "Kí hiệu: $w\in\mathbb R^p$" ở 1-02; 6-01 "($\mathcal Z$, $\mathcal H$ như Định nghĩa 01.4, $\xi\in\Xi$)" |
| HV18 | 6-02 | $s$ so với $S$ | đã sửa: "tập huấn luyện $s=(z_1,\ldots,z_m)$ cố định" |
| HV19 | 4-06/4-08 | cân hai số hạng lặp | đã sửa: 4-06 chỉ nêu "Tổng nhỏ nhất tại $\eta^*=R/(G\sqrt T)$, nơi hai số hạng bằng nhau"; bất đẳng thức ở dòng "Kỹ thuật." 4-08 |
| HV20, TH9 | 7-02 | hàng 05.16 thiếu $\eta$ | đã sửa |
| HV21, SP3 | 1-03 | "bản ngẫu nhiên", mảnh câu | đã sửa: "theo kì vọng và xác suất cao"; "hạ gradient, hạ gradient ngẫu nhiên, lô nhỏ" (80 âm tiết, trần) |
| HV22, SP6 | 6-05 | Diễn giải giảm nhẹ, không nêu ngưỡng | đã sửa: số cụ thể ($1600\to194$, $27\,136$) và "ngưỡng $b=\sigma^2/G_F^2=15$" |
| HV23 | 5-03 | thiếu $u=0$ | đã sửa |
| HV24, SP7 | 3-08 (ghi chú) | câu về câu chữ của đề | đã sửa: bỏ; giữ ý vế phải của Bổ đề 05.12(c) |
| HV25 | nhiều trang | 12 trang 55–60 âm tiết | đã sửa một phần: các ý phụ chuyển xuống ghi chú diễn giả khi sửa; trang dày nhất còn 60 (1-06) theo deck_check |
| TH2, CG14, SP10 | 4-01 (ghi chú) | dùng số bước hai cho "một bước có thể ra xa" | đã sửa: bước hai lại gần ($1{,}3289>1$), bước ba với $i_3=1$ ra xa ($0{,}0236<0{,}0858$, $0{,}0586\to0{,}1112$); câu đọc bất đẳng thức viết lại |
| TH3 | 7-03 | $1/\delta'^2$ ngoài phạm vi | đã sửa: "cho $\operatorname{opt}_S$ ($W$ bị chặn) với xác suất $\ge1-\delta'$ theo $\xi$" |
| TH5 | 4-08 (ghi chú) | $0{,}2281$ như đẳng thức | đã sửa: "không quá $0{,}2281$" |
| TH6 | 7-05 (ghi chú) | thiếu thừa số $4$ | đã sửa: "$5$ lần chạy, mỗi lần gấp $4$ số bước: thừa số $20$" thay $400$ |
| TH7, CG15 | 4-05 (ghi chú) | bỏ phần $\sum b_t$ | đã sửa |
| TH8 | 7-06 (ghi chú) | "còn tăng" | đã sửa: "có thể tăng" |
| TH11 | F4 | trục chưa có vạch trên $0{,}8031$ | đã sửa: trục dọc $[0;1]$, vạch $0$; $0{,}2$; …; $1$ |
| TH12 | F2 | nhãn "proj" | đã sửa: nhãn "π" |
| CG3 | 6-03 | gán "rút có hoàn lại" cho (G1) | đã sửa: bước 1 "(rút đều) … (G1); … (G2); rút có hoàn lại: các $\xi_t$ độc lập"; ghi chú diễn giả sửa theo |
| CG4 | 6-02 | không nói bảo đảm cho thuật toán, không chặn $L_D$; "Trực quan." là bước Markov | đã sửa: "Trực quan. Với $F=L_s$, Hệ quả 05.15 chặn $\operatorname{opt}_s$ của SGD trên $s$ cố định, không chặn $L_D$"; "không cho lớp" ở ghi chú diễn giả (chân trang) |
| CG5 | 5-01 | giới hạn mạng nơ-ron chỉ ở ghi chú | đã sửa: dòng "Kết luận:" |
| CG6, SP (7-03 "1%") | 4-09, 7-03 | thiếu "theo cận" | đã sửa |
| CG8 | 4-03 | ý nghĩa phụ thuộc $p$, $m$ | đã sửa ở 4-07 ("**Ý nghĩa:** cận phụ thuộc chiều $p$, cỡ mẫu $m$ chỉ qua $G$ và $R$"), 4-03 hết chỗ |
| CG9 | 3-07 | thiếu điều kiện đo được, khả tích | đã sửa |
| CG10 | 7-02 | "theo $\xi$"; $\bar w_T$ | đã sửa |
| CG12 | 6-00 | dòng dẫn thiếu điều kiện | đã sửa: "Với hàm lỗi lồi và đủ số bước, …" (25 âm tiết) |
| SP5 | 5-03 | kết luận điểm lặp cuối chỉ ở ghi chú | đã sửa: "…với mọi $t$, không hội tụ" |
| SP8 | 7-07 (ghi chú) | câu quy tắc xếp bảng | đã sửa: bỏ |
| SP9 | 3-04 | nhãn "Chung:", "Đầu ra:" | đã sửa: một câu "Cả hai dùng …, trả về điểm lặp trung bình …" |
| SP11, MT P3, P4 | 4-01, 5-01, 6-01 | câu nối mạch chỉ ở ghi chú | đã sửa: mạch 4 qua dòng dẫn 4-00 (P3, trang tiêu đề mạch là mặt trang); mạch 5 qua dòng dẫn 5-00 có sẵn ("Bỏ tính lồi, … kết luận của cận sai") và câu "Mỗi ví dụ … bỏ đúng một giả thiết" ở ghi chú diễn giả 5-01 (mặt trang 5-01 hết chỗ); 6-01 dòng mở "Với $F=L_S$, Hệ quả 05.15 chặn sai số tối ưu thực nghiệm; đầu ra $\bar w_T$ ngẫu nhiên cả khi $S$ cố định", 6-03 "**Ý nghĩa:** SGD đạt (O2) … với xác suất $\ge1-\delta'$, không tất định" |
| SP12, MT P15 | nhiều trang | tiếng Anh thiếu | đã sửa: convex function (2-02), subgradient inequality (2-03), squared loss (2-04), affine function (2-05), step size, learning rate (3-04; "tốc độ học" ở ghi chú diễn giả), conditional expectation (3-06), telescoping sum (4-04), logistic regression (4-09) |
| SP13 | 4-05, 7-00, 1-01 | "trung bình các điểm lặp" và "điểm lặp trung bình" | đã sửa: dùng "điểm lặp trung bình" ở mọi nơi trừ tên kỹ thuật "Tổng triệt tiêu và trung bình các điểm lặp" (không sửa: tên này đã được storyboard Bài 06 dẫn để nhắc lại) |
| SP14 | 4-05 | "Dùng khi …" không chính xác | đã sửa: "hiệu hai giá trị liên tiếp của đại lượng không âm …; ở Định lý 05.14, $a_t=\lVert w_t-u\rVert^2/(2\eta)$" |
| SP15 | 2-06 | "Ý nghĩa:" nhắc lại (b) | đã sửa: "$G$ chặn mọi dưới gradient; đó là hằng số $G$ của các cận sau" |
| SP16 | 3-05 | hai bước dồn một dòng | đã sửa: danh sách hai dòng |
| SP17 | 6-01 | định nghĩa tách hai đoạn | đã sửa: một đoạn; dòng cuối thành phần của "Ví dụ." |
| SP18 | 6-04, 6-06 | câu mơ hồ | đã sửa: "giữa hai đầu mút của Ví dụ 05.9"; "với $\sigma^2$ thay đổi" |
| SP19 | 7-02 | tiêu đề cột, ô cụt, ghi chú nói về bảng | đã sửa: tiêu đề cột đúng khuôn; ô "Bổ đề 05.8(b)", "một quỹ đạo, không kì vọng", "Markov" (ý tưởng đầy đủ ở ghi chú diễn giả, vì chân trang); câu "không có hàng" thay bằng nội dung |
| SP20 | 3-06, 4-06, 6-06 | tiêu đề | đã sửa: "Tính không chệch có điều kiện", "Độ dài bước tối ưu của cận", "Bài tập: kích thước lô cho số bước gần bằng hạ gradient" |
| SP21 | 1-02 | quy tắc lấy ra đại lượng không có công thức; "với" | đã sửa |
| SP22 | 1-06 (ghi chú) | "Vì vậy" sai quan hệ | đã sửa |
| SP23 | 2-06, 3-03, 3-06, 2-03 (ghi chú) | văn bản làm chủ ngữ, câu chỉ đường, câu bên lề | đã sửa: bỏ câu Định nghĩa 05.6; "Khai triển bình phương, …"; "Chứng minh cho $\Xi$ tổng quát dùng bổ đề đóng băng (Phụ lục B)"; "Chứng minh $\partial F(w)\ne\varnothing$ …: UML §14.2" |
| SP24 | 4-04 (ghi chú) | lặp mặt trang | đã sửa |
| SP25 | 4-09, 6-05, 6-06 (ghi chú) | câu phạm vi lặp, "nhỏ hơn nhiều" | đã sửa: giữ ở 6-05; 6-06 ghi số |
| SP26 | 3-03 | định nghĩa thành mảnh câu | đã sửa: "Các lần rút … có trung bình $\psi(w)$" |
| SP27 | F3, F5 (alt, desc) | "rủi ro", "gần âm 0,125" | đã sửa |
| SP28 | 7-05 | tiêu đề hai phần | đã sửa: "Bài tập: nhiều lần chạy độc lập (tiếp)" |
| MT P2 | 3-05, 6-03, 6-05, 3-08 | số Ví dụ/Bài tập không có ở trang nguồn | đã sửa: "**Ví dụ 05.6.**", "**Ví dụ 05.14.**", "**Ví dụ 05.15.**", "(Bài tập 05.3(b))" |
| MT P5 | 3-00 | dòng dẫn thiếu phép chiếu | đã sửa |
| MT P6 | 3-07, 4-05 | tiêu đề "Kỹ thuật: …" | đã sửa: tên kỹ thuật |
| MT P8 | 2-04/2-05, 3-03/3-04 | thứ tự khối lệch ghi chú | không sửa: Ví dụ 05.3 dùng Mệnh đề 05.3(a), (b) ngay trên trang phát biểu; Thuật toán 05.11 cần Định nghĩa 05.10 nên hai thuật toán chung trang sau định nghĩa (mục 11, điểm 5 đã được chấp nhận); thứ tự mục giữ đúng |
| MT P9 | 2-06, 5-01, 6-02 | từ khóa mạch không trên mặt trang | đã sửa: tiêu đề "Hằng số Lipschitz …"; "tính lồi" ở dòng Kết luận 5-01; "(b) với xác suất cao" ở 6-02 |
| MT P10 | 7-01, 7-03 | kết luận trùng | đã sửa: bỏ "Kết luận:" của 7-01 (ý chuyển xuống ghi chú diễn giả); 7-03 dòng cuối có số $0{,}0025$ và $0{,}9025$ |
| MT P11 | 7-01, 6-03 | nhắc lại xa nơi dùng | đã sửa: 7-01 "sai số ước lượng $L_D-\min_WL_D$ (Định nghĩa 04.1)" (bỏ khỏi 1-02); 6-03 "bất đẳng thức Markov (Bổ đề 02.2)" |
| MT P12 | 1-02 | (O2) thiếu đầu ra | đã sửa: "$\operatorname{opt}_S(A(S))\le\epsilon_{\mathrm{opt}}$ với mọi $S$ (Bài 01)" |
| MT P13 | 4-09 | không nối câu hỏi mở đầu | đã sửa: "với $10^6$ hồ sơ của ví dụ mở đầu" |
| MT P14 | 6-04 | dòng nối không nói lô nhỏ đem gì | đã sửa |
| HV (dòng > 20 âm tiết) | 3-01 | dòng Định nghĩa 05.7 27 âm tiết | không sửa: tách dòng làm trang chạm chân trang; câu giữ đủ "tồn tại vì $W$ đóng, duy nhất vì $W$ lồi" |

Đề xuất sửa ghi chú: không có mới (điều phối viên đã ghi các đề xuất của báo cáo cho tác giả).

### Lượt 2 (theo `reviews/deck-kiem-lai-1.md`, 12 mục nhẹ)

| # | Trang | Phát hiện | Kết quả |
|---|---|---|---|
| 1 | 1-01 | chủ ngữ dài xa động từ | đã sửa: "…, hạ gradient ngẫu nhiên có chiếu có cận của độ chênh tối ưu kì vọng tại điểm lặp trung bình tỉ lệ nghịch với căn bậc hai của số vòng lặp." |
| 2 | 1-06 | "mọi bước SGD làm $L_S$ tăng" sai với hai bước đầu | đã sửa: "Ba quan sát, $L_S=0{,}0639$: mọi lựa chọn của bước SGD sau làm tăng (…), GD giảm ($0{,}0614$)." |
| 3 | 4-03 | "phần tiến" chưa có đơn vị | đã sửa ở ghi chú diễn giả: phần tiến $(\Delta_t-\Delta_{t+1})/(2\eta)$, theo kì vọng ít nhất $F(w_t)-F(u)-\eta G^2/2$, tổng không quá $\Delta_1/(2\eta)$ (mặt trang hết chỗ) |
| 4 | 4-03, 7-00, 7-03 | thiếu "cho" | đã sửa: "hàm mà oracle không chệch cho" |
| 5 | 4-05 | kết luận thiếu $\mathbb E$ | đã sửa: "…; với SGD, lấy kì vọng: $\mathbb EF(\bar w_T)-F(u)\le\frac1T\sum_t\mathbb Ec_t$." |
| 6 | 4-09 | trích Mệnh đề 05.5 đặt sai chỗ | đã sửa: bỏ trích dẫn trên mặt trang ("Với GD, oracle tất định $g_t=v(w_t)$: (G2) thành $\lVert v\rVert\le G$."); quan hệ với hằng số Lipschitz ở ghi chú diễn giả |
| 7 | 6-01/6-02 | lặp ý; $S$/$s$ | đã sửa: 6-01 viết $F=L_s$, "$s$ cố định"; "Trực quan." 6-02 chỉ giữ phần mới: "Bảo đảm cho một thuật toán, trên $s$ cố định; chặn $\operatorname{opt}_s$, không chặn $L_D$." |
| 8 | 6-02 | "$\delta'\in(0,1)$ theo $\xi$" vô nghĩa | đã sửa: bỏ "theo $\xi$" ($\Pr_\xi$ đã nêu); "xác suất thất bại theo $\xi$, khác $\delta$ theo $S$" ở ghi chú diễn giả |
| 9 | 6-03 | "đạt (O2) với xác suất" tự mâu thuẫn; mất nghĩa thao tác | đã sửa: "SGD đạt mức (O2) với xác suất $\ge1-\delta'$: khi $\delta'=0{,}05$, khoảng 95/100 lần chạy độc lập trên cùng $s$ cho $\operatorname{opt}_s<\epsilon_{\mathrm{opt}}$." |
| 10 | 6-04 | "Nhắc lại:" sau phát biểu dùng nó | đã sửa: chuyển lên trước "Mệnh đề 05.20." |
| 11 | 7-03 | đối lập nhị phân | đã sửa: "Cận chặn $\operatorname{opt}_S\approx0{,}0025$; sai số ước lượng vẫn $\approx0{,}9025$." |
| 12 | 4-02, 4-09, 7-01 (390 px) | dấu câu rơi dòng | đã sửa: dấu chấm, dấu phẩy đưa vào trong KaTeX ($1{,}5019.$; $10^4,$ $\eta=0{,}05.$; $\min_WL_D=1.$) |

Kiểm tra sau lượt 2: `deck_lint.py` 1 phát hiện (7-04, ngoại lệ); `footer_check.py` 0 trang; `deck_check.py --shots` các trang đổi (1-01, 1-06, 4-02, 4-03, 4-05, 4-09, 6-01, 6-02, 6-03, 6-04, 7-01, 7-03; thư mục nháp `…/lec-05/editor/chk2`, `chk3`): console 0, pageerrors 0, failed 0, không `.katex-error`, OVERFLOW chỉ ở đuôi `\sqrt`; đã xem ảnh 1600×900 và 390×844 (cả `-end`).

### Lượt 3 (theo `reviews/deck-kiem-lai-2.md`)

| # | Trang | Phát hiện | Kết quả |
|---|---|---|---|
| A | 1-06 | "làm tăng" thiếu tân ngữ, không rõ "sau" điểm nào; câu hỏi thiếu "và" | đã sửa: "Ba quan sát, từ $L_S=0{,}0639$: mọi lựa chọn của bước SGD tiếp theo làm $L_S$ tăng: $(0{,}0710;\ 0{,}1021;\ 0{,}0694)$; GD giảm: $(0{,}0614)$."; "…sau $T$ bước, và cần bao nhiêu bước?"; dòng đầu bỏ "tối thiểu hóa $L_S(w)$" để giữ trần 60 ($L_S$ đã nhắc ở 1-02); số trong ngoặc đưa vào KaTeX để dấu ngoặc không rơi dòng |
| B | 6-02 | "Trực quan." không chủ ngữ | đã sửa: "Hệ quả 05.19 bảo đảm cho một thuật toán trên $s$ cố định: nó chặn $\operatorname{opt}_s$, không chặn $L_D$." |

Kiểm tra: `deck_lint.py` chỉ 7-04 (ngoại lệ); `footer_check.py` 0; `deck_check.py --ids L05-1-06,L05-6-02 --shots`: console 0, pageerrors 0, failed 0, không `.katex-error` (OVERFLOW 6-02 là đuôi `\sqrt`); 1-06 60 âm tiết; đã xem ảnh 1600×900 và 390×844.
