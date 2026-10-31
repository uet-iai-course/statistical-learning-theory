# Dàn ý Bài 08 — Tính ổn định của SGD và tổng quát hóa trong học sâu

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-10-31 bởi tác tử lập dàn ý; chờ điều phối viên duyệt. Dàn ý ràng buộc người viết ghi chú (`materials/lec-08/lecture-note.md`), người viết script thí nghiệm (`../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec08_coupled_sgd.py`) và sau đó người viết bài tập (`materials/lec-08/exercises.md`).

**Căn cứ, theo thứ tự ưu tiên:** 10 quyết định của điều phối viên trong `planning/lec-08/review-log.md`, mục "Phân tích nguồn — quyết định của điều phối viên" (dẫn là "QĐ n"), và danh sách lời hứa ở đầu tệp đó; `sources/blueprint.md` mục A, B, C (Recitation 4, Exam 4), D, E, "Lecture 8" và đầu "Lecture 9"; `CLAUDE.md` của học phần và `../CLAUDE.md`; `planning/lec-08/source-analysis.md` (viết tắt PTN); `planning/course-plan.md`; `planning/van-phong.md` (§3a, §7a, §8, §9a, §11, §12); `planning/thuat-ngu.md` (§9, §10); `planning/ky-hieu.md`; dàn ý Bài 06–07 (mẫu cấu trúc mục 1–13); `lec-06/reviews/0-quyet-dinh.md`, `lec-07/reviews/0-quyet-dinh.md` (lỗi đã bị bắt, tránh từ đầu). Mọi số hiệu Bài 01–07 dẫn dưới đây đã đối chiếu bằng `grep` trên các ghi chú (danh sách ở mục 12). HRS (Hardt, Recht, Singer 2016, `sources/supp/hardt-recht-singer-2016.pdf`) đọc lại: tr. 9 (Thm 3.8 và chứng minh), tr. 12 (Lemma 3.11, Thm 3.12), tr. 19 (Prop 5.4, thảo luận $\sqrt3$, $\sqrt2$; đầu §6), danh mục mục §1–§7 (tr. 1–25).

**Con số mới** (không có trong PTN hoặc khác PTN) đánh dấu †; tất cả đã tính bằng Python trong scratchpad ngoài repo, thư mục `/tmp/claude-1000/-data-tqlong-lectures/15678f46-206f-4a08-81a3-23072a32c4b6/scratchpad/outline08/`: `c1_numbers.py` (mọi con số tính tay, cận, phản ví dụ; kết quả ở `c1_numbers.txt`), `c2_ex.py` (Ví dụ 08.9 và số của bài tập; `c2_ex.txt`), `exp_draft.py` (bản nháp thí nghiệm; kết quả $\eta=0{,}5$ ở `exp_p100_eta05.txt`, $\eta=0{,}25$ ở `exp_p100_eta025.txt`). Mọi số của PTN được dùng lại đã tính lại và khớp. Hai chỗ đổi có chủ ý: cận trên làm tròn lên (PTN ghi $0{,}0957$ cho cận tại $T^*$; giá trị $0{,}095706$ nên ghi $0{,}0958$; giới hạn $0{,}070711$ ghi $0{,}0708$); ví dụ bước quá lớn dùng hàm lỗi Huber thay cho hàm lỗi bình phương để chỉ bỏ đúng một giả thiết (mục 3, §9).

**Nguyên tắc thiết kế (rút từ Bài 01–07):**

1. Đối tượng của ví dụ xuất hiện ở chỗ khái niệm nó minh họa được định nghĩa; §3 chỉ thiết lập ví dụ Huber và khối ứng dụng.
2. Mỗi bảo đảm ghi rõ: tất định trên từng quỹ đạo (mọi giá trị của dãy chỉ số $\xi$), theo kì vọng chỉ theo $\xi$ với mẫu cố định, hay theo kì vọng theo $(S,\xi)$; đại lượng được chặn (khoảng cách giữa hai lần chạy, hệ số ổn định, khoảng cách tổng quát hóa kì vọng, rủi ro vượt mức kì vọng, điểm dừng); cấp thuật toán; phụ thuộc $m$, $T$, $\eta_t$, $G$, $\beta$, $R$; **không** phụ thuộc $p$; không có cận với xác suất cao.
3. Mỗi mục §4–§9 kết bằng một câu văn xuôi nêu hệ quả hay giới hạn (ghi sẵn ở mục 3).
4. Giá trị giả định (cỡ mẫu, bán kính của ứng dụng) luôn ghi "giả định"; số của thí nghiệm luôn ghi là kết quả thí nghiệm của học phần, không phải chứng minh (blueprint §E), và ghi đúng giả thiết nào thỏa trong thí nghiệm (bài học Bài 07).
5. Chứng minh không áp dụng một bước cần tính độc lập cho các biến không độc lập: bất đẳng thức truy hồi được chứng minh **trên từng quỹ đạo** rồi mới lấy kì vọng, chỉ dùng xác suất biên $\Pr(i_t=i)=1/m$ (PTN §2.2). Mọi bước chứng minh ghi giả thiết được dùng.
6. Một chữ một nghĩa: "hồi quy" chỉ dùng cho hồi quy logistic, hồi quy bình phương; recurrence viết "bất đẳng thức truy hồi" (điểm mở 1). "Khoảng cách tổng quát hóa" theo `thuat-ngu.md`, không "độ chênh tổng quát hóa". $\Delta_t$ của bài là khoảng cách giữa hai lần chạy, khác $\Delta_t$ cục bộ trong chứng minh Bài 05 (nói một câu ở lần đầu).
7. Không chuyển kết quả lồi sang mạng nơ-ron hay hàm lỗi không trơn (blueprint 8.4, §E); không ghép cận ổn định của điểm lặp cuối $w_{T+1}$ với cận tối ưu của điểm lặp trung bình $\bar w_T$ (Định lý 05.14 không nói gì về $w_{T+1}$).
8. Quy ước làm tròn: cận trên (vế phải của định lý, hệ quả) làm tròn **lên**; số quan sát được của thí nghiệm làm tròn **gần nhất**; Phụ lục D nêu quy ước một lần (bài học Bài 07).
9. Không câu nào lấy văn bản làm chủ ngữ; không chữ có dấu trong `\text{}`; công thức hiển thị tách dòng bằng `aligned` để vừa 390 px; bảng ≤ 5 cột hẹp.
10. Kí hiệu theo QĐ 1, 10: chỉ số từ $t=1$, $w_1=w'_1$ tất định, điểm lặp cuối $w_{T+1}$, $\xi=(i_1,\ldots,i_T)$ dùng chung, $G$ (không $L$ của HRS), không đặt tên hàm phụ là $\varphi$, $\psi$ (oracle Bài 05) hay $\phi$ (Bài 07).

## 1. Câu hỏi trung tâm, luận điểm, câu hỏi mở đầu, mục tiêu

**Câu hỏi trung tâm** (blueprint mục B: "How does the training algorithm affect generalization?"). Thuật toán huấn luyện ảnh hưởng tới khoảng cách tổng quát hóa như thế nào?

**Luận điểm (một câu).** Với SGD trên một mẫu cố định, hàm lỗi lồi, $\beta$-trơn, có gradient bị chặn bởi $G$ và độ dài bước $\eta_t\le2/\beta$, hai lần chạy ghép cặp trên hai mẫu lân cận cách nhau theo kì vọng không quá $\tfrac{2G}m\sum_{t=1}^T\eta_t$, nên SGD ổn định đều với hệ số $\tfrac{2G^2}m\sum_t\eta_t$ và khoảng cách tổng quát hóa kì vọng của điểm lặp cuối bị chặn bởi cùng số đó (Định lý 08.6) — một bảo đảm cấp thuật toán, phụ thuộc quỹ đạo qua ngân sách độ dài bước, không phụ thuộc số chiều; ghép với cận tối ưu của Bài 05, nó cho một đánh đổi giữa hai cận trên theo số bước (Hệ quả 08.8), không phải bảo đảm rằng dừng sớm làm giảm lỗi kiểm tra; khi bỏ tính lồi, hệ số giãn $1+\beta\eta_t$ làm cận tăng theo hàm mũ (Mệnh đề 08.10), và mạng ReLU không thỏa giả thiết trơn, lồi, gradient bị chặn đều, nên định lý không áp dụng nguyên văn cho chúng.

**Câu hỏi mở đầu** (blueprint 8.1; QĐ 7; viết đúng như sau, có thể sửa chữ nhỏ; đã qua `no-ai-slop` Edit; số lấy từ script cuối cùng, dự kiến như dưới):

> Một mô hình hồi quy logistic với $p=100$ đặc trưng được huấn luyện trên $m=200$ quan sát. Các đặc trưng thỏa $\lVert x\rVert\le1$, và nhãn của khoảng $10\%$ quan sát bị lật ngẫu nhiên. Thuật toán là SGD bắt đầu từ véc-tơ $0$: ở mỗi bước, một quan sát của mẫu được rút đều, có hoàn lại, và véc-tơ tham số đi một bước độ dài $0{,}5$ ngược hướng gradient của hàm lỗi logistic trên quan sát đó. Cùng một lần chạy được đọc ở năm thời điểm, từ nửa vòng đến $100$ vòng qua dữ liệu. Tại mỗi thời điểm, ta đo trung bình hàm lỗi logistic trên mẫu huấn luyện và trên $5000$ quan sát kiểm tra rút độc lập. Bảng ghi trung bình của $20$ lần lặp với $20$ hạt giống; cột cuối là cận mà §7 chứng minh cho khoảng cách tổng quát hóa kì vọng của thuật toán này.
>
> | Số vòng | Huấn luyện | Kiểm tra | Khoảng cách | Cận (§7) |
> |---|---|---|---|---|
> | $0{,}5$ | $0{,}618$ | $0{,}662$ | $0{,}045$ | $0{,}5$ |
> | $1$ | $0{,}561$ | $0{,}640$ | $0{,}079$ | $1$ |
> | $5$ | $0{,}376$ | $0{,}589$ | $0{,}213$ | $5$ |
> | $20$ | $0{,}243$ | $0{,}662$ | $0{,}419$ | $20$ |
> | $100$ | $0{,}135$ | $1{,}053$ | $0{,}919$ | $100$ |
>
> **Câu hỏi.** Mô hình, mẫu và thuật toán giữ nguyên; chỉ số bước thay đổi. Lỗi huấn luyện giảm, còn khoảng cách giữa lỗi kiểm tra và lỗi huấn luyện tăng. Đại lượng nào của quá trình huấn luyện quyết định khoảng cách này?

Số dự kiến (`exp_p100_eta05.txt`, trung bình 20 hạt giống, làm tròn gần nhất ba chữ số): huấn luyện $0{,}6177$; $0{,}5612$; $0{,}3762$; $0{,}2431$; $0{,}1345$; kiểm tra $0{,}6622$; $0{,}6404$; $0{,}5894$; $0{,}6622$; $1{,}0533$; khoảng cách (trung bình của hiệu từng hạt giống) $0{,}0445$; $0{,}0792$; $0{,}2131$; $0{,}4192$; $0{,}9188$. **Lưu ý cho người viết:** cột "Khoảng cách" là trung bình của hiệu, làm tròn riêng, nên có thể lệch một đơn vị ở chữ số cuối so với hiệu của hai cột đã làm tròn (dòng đầu: $0{,}662-0{,}618=0{,}044$ so với $0{,}045$); Phụ lục D ghi một câu về điều này. Cận $t/200$ là số chính xác ($2G^2\eta t/m$ với $G=1$, $\eta=0{,}5$, $m=200$; trong câu hỏi mở đầu không viết công thức).

Đoạn trả lời ngay sau (trả lời thẳng theo `van-phong.md` §9a; câu trả lời hấp dẫn nhưng sai là "khoảng cách tăng vì mô hình có nhiều tham số so với số quan sát", viết thành câu hỏi thẳng rồi trả lời):

> Có phải khoảng cách tăng vì mô hình có $100$ tham số mà chỉ có $200$ quan sát không? Số tham số và lớp hàm như nhau ở mọi dòng của bảng, nên chúng không giải thích sự thay đổi theo số bước. Đại lượng thay đổi là quỹ đạo của thuật toán: sau $t$ bước, tổng các độ dài bước là $0{,}5t$. Với hàm lỗi lồi, trơn và có gradient bị chặn, khoảng cách tổng quát hóa kì vọng của SGD không vượt một hằng số nhân tổng các độ dài bước chia cho cỡ mẫu (§4–§7); cột cuối là cận đó. Các khoảng cách đo được đều nằm dưới cột cuối, nhỏ hơn nó từ khoảng $11$ đến khoảng $109$ lần, và lỗi phân lớp trên mẫu kiểm tra gần như không đổi từ $5$ đến $100$ vòng ($0{,}309$; $0{,}301$; $0{,}312$). Bảng là kết quả của một thí nghiệm, không phải một chứng minh; giao thức ở Phụ lục D.

Số: tỉ số cận/khoảng cách $0{,}5/0{,}0445\approx11{,}2$† và $100/0{,}9188\approx108{,}8$†; lỗi 0–1 kiểm tra $0{,}3089$, $0{,}3009$, $0{,}3118$ ở $5$, $20$, $100$ vòng†. Dẫn "§4–§7", "§7", "Phụ lục D"; không dẫn số khối, không dùng kí hiệu $G$, $\beta$, $\eta_t$, $\Delta_t$ trước §2; "tính ổn định", "ghép cặp" chưa dùng ở đây.

**Mục tiêu học tập** (chỉ chữ, không kí hiệu, không số khối; đã qua `no-ai-slop` Edit):

1. Mô tả hai lần chạy ghép cặp của SGD trên hai mẫu lân cận và tính khoảng cách giữa chúng trên một ví dụ nhỏ.
2. Chứng minh rằng một bước gradient của hàm lồi, trơn không làm tăng khoảng cách giữa hai điểm khi độ dài bước không vượt hai lần nghịch đảo hằng số trơn, và chỉ ra bước chứng minh dùng tính lồi.
3. Chứng minh bất đẳng thức truy hồi cho khoảng cách giữa hai lần chạy, suy ra cận ổn định của SGD và cận cho khoảng cách tổng quát hóa kì vọng, rồi tính các cận đó bằng số.
4. Ghép cận ổn định với cận tối ưu để chọn số bước và độ dài bước, và nêu những điều cận ghép này không bảo đảm về lỗi kiểm tra.
5. Kiểm tra giả thiết của định lý cho một thiết lập huấn luyện cụ thể (hàm lỗi không lồi, độ dài bước lớn, mạng ReLU), và phân biệt kết quả chứng minh được, lý thuyết không lồi bổ sung và giả thuyết thực nghiệm.

Mục tiêu đo bởi: 1 (Bài tập 08.1; Ví dụ 08.2, 08.4); 2 (Bài tập 08.3; Bổ đề 08.4; Ví dụ 08.3, 08.9); 3 (Bài tập 08.1, 08.2, 08.7; Mệnh đề 08.5, Định lý 08.6, Hệ quả 08.7; Ví dụ 08.5); 4 (Bài tập 08.2, 08.8; Hệ quả 08.8; Ví dụ 08.7; Định nghĩa 08.9); 5 (Bài tập 08.3, 08.4, 08.5, 08.6; Ví dụ 08.6, 08.8, 08.10; Mệnh đề 08.10, 08.12; Nhận xét 08.11). Khớp Recitation 4 ("coupled SGD; neural-network assumption audit"): Bài tập 08.1, 08.5; Exam 4 ("identify missing assumptions and distinguish theorem from experiment"): câu hỏi cuối buổi (c), (d), Ví dụ 08.6, Bài tập 08.6.

## 2. Đánh số

Một bộ đếm chung theo thứ tự đọc cho thuật toán, định nghĩa, bổ đề, mệnh đề, định lý, hệ quả, nhận xét; ví dụ và bài tập có bộ đếm riêng. Khối `application` không đánh số. Cột "Blueprint / QĐ" chỉ dùng nội bộ.

| Số | Loại | Tên (cụm danh từ) | Mục | Độ sâu | Blueprint / QĐ |
|---|---|---|---|---|---|
| Thuật toán 08.1 | algorithm | SGD có chiếu trên một mẫu cố định với độ dài bước thay đổi | §4 | — | §8.2 "fixed-sample SGD … with replacement"; QĐ 1, 2 (chỉ số từ $1$, có chiếu) |
| Định nghĩa 08.2 | definition | Hai lần chạy ghép cặp và ngân sách độ dài bước | §4 | — | §8.2 "Couple two runs … same initialization and index sequence. Define $\Delta_t$ … cumulative step-size budget"; QĐ 10 |
| Định nghĩa 08.3 | definition | Hệ số giãn, ánh xạ không giãn và tính đồng bức | §5 | — | §8.3 Lemma 8.1 "nonexpansive", "co-coercivity"; PTN §1 (HRS Def 2.3–2.4) |
| Bổ đề 08.4 | lemma | Bước gradient không giãn | §5 | phác thảo (tính đồng bức chứng minh ở Phụ lục A) | **Lemma 8.1 [S]**; QĐ 4; QĐ 2 (thêm phép chiếu) |
| Mệnh đề 08.5 | proposition | Bất đẳng thức truy hồi cho khoảng cách giữa hai lần chạy ghép cặp | §6 | chứng minh đầy đủ | **Proposition 8.2 [F]**; PTN §2.2 (bất đẳng thức trên từng quỹ đạo) |
| Định lý 08.6 | theorem | Tính ổn định đều của SGD với hàm lỗi lồi và trơn | §7 | chứng minh đầy đủ | **Theorem 8.3 [F]**; QĐ 1, 2, 3; PTN §2.3 |
| Hệ quả 08.7 | corollary | Tính ổn định của điểm lặp trung bình | §7 | chứng minh đầy đủ | QĐ 3 ($G^2\eta(T-1)/m$); PTN §2.4; lời hứa Bài 06 (SGD nhiều vòng của §5 Bài 06 có đầu ra $\bar w_T$) |
| Hệ quả 08.8 | corollary | Rủi ro vượt mức kì vọng của SGD nhiều vòng | §8 | chứng minh đầy đủ (ở Phụ lục C; biên tập vòng 1–2) | **Corollary [F]** (bước hằng, so xu hướng với sai số tối ưu); QĐ 3 (ghép [F], không tốt hơn một vòng); PTN §2.5 |
| Định nghĩa 08.9 | definition | Dừng sớm, chính quy hóa tường minh và chính quy hóa ngầm | §8 | — | §8.4 "early stopping … implicit regularization as selection behavior … distinguish it from explicit regularization and from a proved theorem" |
| Mệnh đề 08.10 | proposition | Bất đẳng thức truy hồi khi bỏ tính lồi | §9 | phác thảo (ở Phụ lục D; biên tập vòng 1–2) | **Nonconvex extension [S]**; QĐ 5; PTN §2.6 |
| Nhận xét 08.11 | remark | Cận ổn định cho hàm lỗi không lồi bị chặn | §9 | đọc thêm | §8.3 "Refer to supplementary results for refined rates"; QĐ 5 (HRS Thm 3.12, đủ giả thiết) |
| Mệnh đề 08.12 | proposition | Điểm dừng xấp xỉ của SGD trên hàm mục tiêu trơn | §9 | đọc thêm (chứng minh ở Phụ lục C) | **Optional optimization appendix [O]**; QĐ 6; PTN §2.7 |

Tiêu đề khối theo mẫu Bài 07: `::: algorithm Thuật toán 08.1 (SGD có chiếu trên một mẫu cố định với độ dài bước thay đổi)`; `::: lemma Bổ đề 08.4 (Bước gradient không giãn) — phác thảo (tính đồng bức chứng minh ở Phụ lục A)`; `::: proposition Mệnh đề 08.5 (Bất đẳng thức truy hồi cho khoảng cách giữa hai lần chạy ghép cặp) — chứng minh đầy đủ`; `::: theorem Định lý 08.6 (Tính ổn định đều của SGD với hàm lỗi lồi và trơn) — chứng minh đầy đủ`; `::: corollary Hệ quả 08.8 (Rủi ro vượt mức kì vọng của SGD nhiều vòng) — chứng minh đầy đủ`; `::: proposition Mệnh đề 08.10 (Bất đẳng thức truy hồi khi bỏ tính lồi) — phác thảo`; `::: remark Nhận xét 08.11 (Cận ổn định cho hàm lỗi không lồi bị chặn) — đọc thêm`; `::: proposition Mệnh đề 08.12 (Điểm dừng xấp xỉ của SGD trên hàm mục tiêu trơn) — đọc thêm (chứng minh ở Phụ lục C)`. Định nghĩa và thuật toán không ghi độ sâu.

**Lý do chọn vai.** Thuật toán 08.1 cần khối riêng vì khác Thuật toán 05.11 ở hai điểm: độ dài bước thay đổi theo $t$ (Nhận xét 05.17 chỉ là đọc thêm) và đầu ra là điểm lặp cuối $w_{T+1}$ (cộng $\bar w_T$ ở Hệ quả 08.7–08.8); gradient thay cho dưới gradient vì hàm lỗi khả vi. Bổ đề 08.4 là công cụ. Mệnh đề 08.5 là sự kiện tập trung về hai quỹ đạo (blueprint §D: "smooth-convex coupled SGD recurrence" trong xương sống chứng minh). Định lý 08.6 là kết quả chính. Hệ quả 08.7 và 08.8 suy ra trực tiếp (thay đầu ra; ghép với Định lý 05.14 và Mệnh đề 06.5). Mệnh đề 08.10 là sự kiện tập trung về trường hợp không lồi, độ sâu [S] như blueprint. Mệnh đề 08.12 [O] đặt phát biểu trong thân bài (§9) và chứng minh ở Phụ lục C, để thân bài dẫn được nó mà không dẫn tới trước (cùng cách Bổ đề 07.10). Không đặt khối riêng cho: tính đồng bức (phần (a) của Bổ đề 08.4); tính không giãn của phép chiếu (đã có, đoạn sau Bổ đề 05.8); xáo trộn lại sau mỗi vòng (một đoạn sau Mệnh đề 08.5, chi tiết Phụ lục B); cận trên bậc hai của hàm trơn (bước 1 của Phụ lục A, dùng lại ở Phụ lục C); cận chuẩn $\lVert w_{T+1}-w_1\rVert\le G\sum_t\eta_t$ (Bước 4 chứng minh Định lý 08.6).

**Ví dụ** (bộ đếm riêng):

| Số | Tên | Mục | Vai trò |
|---|---|---|---|
| Ví dụ 08.1 | Hàm lỗi Huber trên bốn quan sát | §3 | ví dụ tính tay xuyên suốt (QĐ 8): hằng số $\beta=G=1$, một lần chạy SGD; dùng lại ở §4, §5, §6, §9 |
| Ví dụ 08.2 | Hai lần chạy ghép cặp trong ví dụ Huber | §4 | Định nghĩa 08.2 bằng số; bước chung không làm tăng $\Delta_t$, bước khác biệt tăng tối đa $2G\eta$ |
| Ví dụ 08.3 | Hệ số giãn của bước gradient một chiều | §5 | Bổ đề 08.4 bằng số; ngưỡng $2/\beta$ là chặt; hàm lõm có hệ số $1+\eta$ (nhìn tới §9) |
| Ví dụ 08.4 | Kì vọng của khoảng cách trong ví dụ Huber | §6 | Mệnh đề 08.5 bằng số: dấu bằng ở bước đầu, $29/64<1/2$, $0{,}8705\le1{,}5$; quỹ đạo đạt cận |
| Ví dụ 08.5 | Cận ổn định cho hồi quy logistic | §7 | **cận số bắt buộc** (đọc số sau định lý chính, `van-phong.md` §7); ứng dụng $m=10^6$ và thí nghiệm $m=200$ |
| Ví dụ 08.6 | Hai lần chạy ghép cặp trong thí nghiệm mở đầu | §7 | trả lời câu hỏi mở đầu; nêu giả thiết nào thỏa; $\mathbb E\Delta$ đo được so với cận; không ghép cặp; tỉ lệ đổi nhãn |
| Ví dụ 08.7 | Số vòng qua dữ liệu cho hồi quy logistic | §8 | trả lời khối ứng dụng; $\sqrt3$, $\sqrt2$; $T^*$ với $\eta$ cố định |
| Ví dụ 08.8 | Bỏ tính lồi: hàm lỗi cosin | §9 | **phản ví dụ bỏ giả thiết** (PTN (d1)); một quỹ đạo tất định, $\Delta$ nhân $1{,}1$ mỗi bước chung |
| Ví dụ 08.9 | Độ dài bước vượt $2/\beta$ | §9 | phản ví dụ bỏ đúng điều kiện $\eta\le2/\beta$ (Huber, mọi giả thiết khác giữ) |
| Ví dụ 08.10 | Hàm lỗi không trơn và mạng ReLU | §9 | phản ví dụ bỏ tính trơn ($\lvert w-z\rvert$, bản lề); kiểm giả thiết cho mạng ReLU (blueprint 8.4) |

**Ánh xạ blueprint → số cục bộ** (tóm tắt): Lemma 8.1 → Bổ đề 08.4 (thêm phần (c) có chiếu, QĐ 2; định nghĩa ở Định nghĩa 08.3); Proposition 8.2 → Mệnh đề 08.5 (chỉ số từ $1$: $\Delta_1=0$; thêm phần (a) trên từng quỹ đạo); Theorem 8.3 → Định lý 08.6 (tổng $\sum_{t=1}^T\eta_t$ cho $w_{T+1}$, tương đương $\sum_{t=0}^{T-1}$ của blueprint khi đánh số từ $w_0$; thêm dạng ghép cặp (a), có chiếu); Corollary → dòng bước hằng trong Bảo đảm của Định lý 08.6 cùng Hệ quả 08.7, 08.8 và Ví dụ 08.7; Nonconvex extension → Mệnh đề 08.10 và Ví dụ 08.8; "supplementary results for refined rates" → Nhận xét 08.11; Optional optimization appendix → Mệnh đề 08.12 cùng Phụ lục C; §8.2 → Thuật toán 08.1, Định nghĩa 08.2, 08.3; §8.4 → Định nghĩa 08.9, Ví dụ 08.10 và §10; bài gốc §8.5 1–6 → Bài tập 08.1–08.6; hai bài gốc thêm (QĐ 9) → Bài tập 08.7, 08.8.

## 3. Bản đồ các mục và phát biểu hình thức

Quy tắc định nghĩa trước khi dùng thắng thứ tự thành phần của blueprint: thành phần 7–11 nằm xen trong §4–§9; mỗi giả thiết được nêu ngay trước khối dùng nó lần đầu (riêng (S), (G) và điều kiện độ dài bước nêu ở §2 vì §3 dùng chúng); không câu nào trong thân bài dẫn một khối có số đứng sau (viết "mệnh đề ở §6", "bổ đề dưới đây"). Mỗi khối kết quả có **Giả thiết.** và **Bảo đảm.**; từ ba thành phần trở lên thì là danh sách nhãn in đậm song song (`van-phong.md` §3a; mẫu: Định lý 06.10). Cụm chuẩn: "tất định, trên từng quỹ đạo (mọi giá trị của $\xi$)"; "theo kì vọng theo $\xi$, với mẫu cố định"; "theo kì vọng theo $(S,\xi)$".

### `# Bài 08 — Tính ổn định của SGD và tổng quát hóa trong học sâu` và đoạn dẫn

Tên bài theo QĐ 10 (khớp thẻ chỉ mục). Hai đoạn ngắn. Đoạn 1 (nhìn lại Bài 06 và Bài 07): Định lý 06.10 chặn khoảng cách tổng quát hóa kì vọng của một thuật toán ổn định đều, và Mệnh đề 06.11 cho ERM có chính quy hóa một hệ số ổn định $2G^2/(\lambda m)$; SGD chạy nhiều vòng trên một mẫu cố định chưa có cận như vậy (§10 Bài 06). Bài 07 chặn khoảng cách tổng quát hóa đồng thời cho mọi hàm của một lớp chọn trước mẫu, nên không phân biệt hai hàm cùng lớp mà phép huấn luyện chọn khác nhau; Bài 07 kết thúc bằng câu hỏi: với hàm lỗi lồi, trơn và Lipschitz, quỹ đạo của SGD có cho một bảo đảm cho chính hàm SGD trả về không. Đoạn 2: câu hỏi trung tâm viết thành câu khẳng định ("Câu hỏi trung tâm của bài là thuật toán huấn luyện ảnh hưởng tới khoảng cách tổng quát hóa như thế nào."); công cụ, tiếng Anh ở lần đầu: hai lần chạy ghép cặp (coupled runs), ánh xạ không giãn (nonexpansive map), tính đồng bức (co-coercivity), tính ổn định đều của SGD; phạm vi: chứng minh đầy đủ cho hàm lỗi lồi và trơn, rồi xét điều gì hỏng khi bỏ tính lồi, tính trơn, như với mạng nơ-ron ReLU. Không viết "Bài này …".

### `## Câu hỏi mở đầu`, `## Mục tiêu học tập`

Như mục 1. Câu hỏi mở đầu chỉ dẫn "§4–§7", "§7", "Phụ lục D".

### `## Kiến thức tiên quyết`

Danh sách lồng như Bài 06–07, **mỗi số hiệu kèm tên khối** (bài học Bài 07, R1/R4/R5):

- **Từ Bài 01.** (T1), (T2); khoảng cách tổng quát hóa (Định nghĩa 01.10); tính không chệch của rủi ro thực nghiệm với giả thuyết cố định (Mệnh đề 01.7); rủi ro vượt mức (Định nghĩa 01.24).
- **Từ Bài 04.** Sai số tối ưu thực nghiệm $\operatorname{opt}_S$ (Định nghĩa 04.2); mẫu xác thực (chỉ ở Định nghĩa 08.9).
- **Từ Bài 05.** Hàm Lipschitz (Định nghĩa 05.4) và hằng số Lipschitz qua chuẩn của dưới gradient (Mệnh đề 05.5); hàm trơn và hàm lồi mạnh (Định nghĩa 05.6); phép chiếu Euclid (Định nghĩa 05.7) và tính không giãn của nó (đoạn sau Bổ đề 05.8); oracle gradient ngẫu nhiên và lịch sử (Định nghĩa 05.10); SGD có chiếu (Thuật toán 05.11); cận kì vọng cho SGD có chiếu (Định lý 05.14); độ dài bước thay đổi (Nhận xét 05.17); thuật toán học có nguồn ngẫu nhiên riêng (Định nghĩa 05.18); SGD trên rủi ro thực nghiệm (Hệ quả 05.19); phương sai $\sigma^2$ của gradient ngẫu nhiên (Mệnh đề 05.20, chỉ Mệnh đề 08.12); hằng số của hàm lỗi logistic (Bài tập 05.8).
- **Từ Bài 06.** Một vòng qua mẫu theo thứ tự (Nhận xét 06.3); khoảng cách tổng quát hóa kì vọng (Định nghĩa 06.4); phân tích rủi ro của đầu ra tính trên một mẫu cố định (Mệnh đề 06.5); ERM có chính quy hóa (Định nghĩa 06.6); mẫu lân cận và tính ổn định đều (Định nghĩa 06.9); tính ổn định chặn khoảng cách tổng quát hóa kì vọng (Định lý 06.10); tính ổn định của ERM có chính quy hóa (Mệnh đề 06.11); giả thiết (L) (đoạn trước Mệnh đề 06.11).
- **Từ Bài 07.** Mạng nơ-ron lan truyền tới (Định nghĩa 07.1); lớp kiến trúc và mô hình do huấn luyện chọn (Định nghĩa 07.5); cận theo lề, cấp lớp (Hệ quả 07.16); nghiệm nội suy chuẩn nhỏ nhất là giới hạn của hạ gradient khởi tạo tại $0$ (Phụ lục D của Bài 07).
- **Giải tích.** Bất đẳng thức tam giác và Cauchy–Schwarz; khai triển $\lVert a-b\rVert^2$; định lý giá trị trung bình và công thức tích phân của gradient dọc một đoạn thẳng (Phụ lục A); $1+x\le e^x$; $\sum_{s=t+1}^T1/s\le\ln(T/t)$ (§9).

Không đưa vào: Ví dụ 05.10, 06.7 (không dẫn); Định lý 03.15 (không dùng).

**Câu hỏi ôn nhanh** (lời giải ngắn trong một khối `solution`, như Bài 06–07):

1. Cho $g(w)=\ln(1+e^{-w})$ và $f(w)=\tfrac12w^2$ trên $\mathbb R$. Hàm nào là $1$-Lipschitz trên $\mathbb R$? Tìm một hằng số trơn cho mỗi hàm. *Lời giải:* $g'(w)=-1/(1+e^w)\in(-1,0)$, nên $g$ là $1$-Lipschitz (Mệnh đề 05.5(a)); $g''(w)=e^w/(1+e^w)^2\le\tfrac14$ (cực đại tại $w=0$), nên $g'$ là $\tfrac14$-Lipschitz theo định lý giá trị trung bình, tức $g$ là $\tfrac14$-trơn. $f'(w)=w$ không bị chặn, nên $f$ không Lipschitz trên $\mathbb R$, nhưng $f$ là $1$-trơn. (Chuẩn bị (S), (G) ở §2 và Ví dụ 08.5; $\max q(1-q)=0{,}25$ đã kiểm.)
2. Với $W=[-1,1]$, $\theta=3$ và $\theta'=-\tfrac12$, tính $\lvert\operatorname{proj}_W(\theta)-\operatorname{proj}_W(\theta')\rvert$ và so với $\lvert\theta-\theta'\rvert$. *Lời giải:* $\operatorname{proj}_W(3)=1$, $\operatorname{proj}_W(-\tfrac12)=-\tfrac12$, hiệu $1{,}5\le3{,}5$†; phép chiếu không giãn (đoạn sau Bổ đề 05.8). (Chuẩn bị Bổ đề 08.4(c).)
3. Rút $T=6$ chỉ số đều trên $\{1,2,3,4\}$, có hoàn lại. Tính kì vọng của số lần chỉ số $4$ được rút và xác suất chỉ số $4$ được rút ít nhất một lần. *Lời giải:* số lần rút là $\sum_{t=1}^6\mathbb 1[i_t=4]$, kì vọng $6\cdot\tfrac14=1{,}5$† theo tính tuyến tính của kì vọng (không cần tính độc lập); xác suất $1-(3/4)^6=3367/4096\approx0{,}8220$†. (Chuẩn bị Mệnh đề 08.5(b) và Ví dụ 08.4, cùng $m=4$, $T=6$.)

Chú thích trong ngoặc chỉ dành cho người viết.

### `## 1. Thiết lập bài toán`

Câu mở: "Bài toán có bảy thành phần. Khác Bài 07, bảo đảm là cho một thuật toán cụ thể; khác Bài 06, thuật toán là SGD chạy nhiều vòng trên một mẫu cố định." Danh sách nhãn in đậm song song:

1. **Dữ liệu.** Quan sát $z\in\mathcal Z$ rút từ phân bố $D$ chưa biết; với mô hình tuyến tính, $z=(x,y)$ và khi cần, $\lVert x\rVert\le C_x$ trên toàn $\mathcal X$; trong ví dụ tính tay, $\mathcal Z=\mathbb R$.
2. **Cơ chế lấy mẫu.** $S=(Z_1,\ldots,Z_m)\sim D^m$ theo dạng đầy đủ của (T1); mẫu kiểm tra độc lập chỉ dùng trong thí nghiệm (Phụ lục D).
3. **Lớp và hàm lỗi.** Lớp hàm điểm số $\{h_w:w\in W\}$ của Bài 05, $W\subset\mathbb R^p$ khác rỗng, đóng, lồi, có thể là $\mathbb R^p$ (không bị chặn); hàm lỗi $\ell(w,z)\ge0$ khả vi theo $w$; tính lồi và tính trơn nêu ở §2, bỏ ở §9.
4. **Thuật toán.** SGD trên mẫu $S$: chỉ số rút đều có hoàn lại, độ dài bước $\eta_t$ tất định thay đổi theo bước, $T$ bước, có thể nhiều vòng qua dữ liệu (§4); đầu ra là điểm lặp cuối, hoặc điểm lặp trung bình ở §7–§8.
5. **Mục tiêu.** Khoảng cách tổng quát hóa kì vọng của đầu ra (Định nghĩa 06.4), rồi rủi ro vượt mức kì vọng so với $W$ (§8).
6. **Đối tượng so sánh.** Không cần cho cận khoảng cách tổng quát hóa; cận dưới đúng $\inf_WL_D$ ở §8.
7. **Tài nguyên.** Cỡ mẫu $m$, số bước $T$ và các độ dài bước $\eta_1,\ldots,\eta_T$; chúng đi vào cận qua $\tfrac1m\sum_t\eta_t$.

Bảng cố định / ngẫu nhiên (bắt buộc):

| Loại | Đại lượng |
|---|---|
| Cố định | $D$, $W$, $\ell$, $\beta$, $G$, $m$, $T$, $\eta_1,\ldots,\eta_T$, $w_1$ |
| Ngẫu nhiên theo dữ liệu | $S$, $L_S(\cdot)$ |
| Ngẫu nhiên theo $\xi$ | dãy chỉ số $\xi=(i_1,\ldots,i_T)$ |
| Ngẫu nhiên theo cả hai | điểm lặp $w_t$, $w_{T+1}$, $\bar w_T$; $L_D$ và $L_S$ tại đó |
| Chỉ trong định nghĩa và chứng minh | mẫu lân cận $s^{(i)}$, quan sát thay thế $z'$, quan sát kiểm tra $z$, điểm lặp $w'_t$ của lần chạy thứ hai |

Hai câu: trong Định nghĩa 06.9 và §4–§7, mẫu $s$, chỉ số $i$, quan sát thay thế $z'$ và quan sát kiểm tra $z$ là các điểm bất kì, không ngẫu nhiên; chỉ $\xi$ là ngẫu nhiên. Lần chạy thứ hai là công cụ chứng minh, không phải một lần huấn luyện thật.

### `## 2. Kí hiệu và giả thiết`

- Bảng nhỏ, chỉ kí hiệu dùng từ §3 hoặc nhắc lại: $w$, $W$, $h_w$, $\ell(w,z)$, $L_S(w)$, $L_D(w)$, $\operatorname{proj}_W$, $\eta_t$, $T$, $i_t$, $\xi$, $w_t$, $w_{T+1}$, $\bar w_T$, $G$, $\beta$, $R$ (Bài 05); $s^{(i)}$, $z'$, $\epsilon_{\mathrm{stab}}(m)$ (Bài 06). Mọi kí hiệu khác ($w'_t$, $\Delta_t$, $\Gamma$, $\ell_{\mathrm H}$, $\eta^*$, $T^*$, $F_*$) đặt tên tại định nghĩa hay khối dùng nó lần đầu.
- Một đoạn tách hai loại giả thiết. **Giả thiết thống kê:** dạng đầy đủ của (T1) (§7–§8, qua Định lý 06.10); (T2): $\ell\ge0$ đo được và $L_D(w_1)<\infty$. Các kết quả chính không giả sử hàm lỗi bị chặn. **Giả thiết tối ưu**, đặt tên để chứng minh đánh dấu chỗ dùng (QĐ 2; điểm mở 2):
  - **(S)** Với mọi $z\in\mathcal Z$, $\ell(\cdot,z):\mathbb R^p\to\mathbb R$ lồi và $\beta$-trơn (Định nghĩa 05.6) **trên toàn $\mathbb R^p$**.
  - **(G)** Với mọi $z\in\mathcal Z$ và mọi $w\in W$, $\lVert\nabla\ell(w,z)\rVert\le G$.
  - **Độ dài bước.** $\eta_t$ tất định, $0<\eta_t\le2/\beta$.
- Ba câu đọc: (i) lượng từ "với mọi $z\in\mathcal Z$" chạy trên mọi quan sát có thể, không chỉ trên mẫu (PTN §6.3(x)); (ii) (G) kéo theo (L) của Bài 06 theo Mệnh đề 05.5(a) với $U=W$, và kéo theo (G2) cho oracle rút đều (Bước 1 chứng minh Hệ quả 05.19); (iii) (S) được đặt trên toàn $\mathbb R^p$ vì chứng minh tính đồng bức (Phụ lục A) dùng những điểm có thể nằm ngoài $W$. Ví dụ, một câu mỗi loại: hàm lỗi logistic thỏa (S) với $\beta=C_x^2/4$ và (G) với $G=C_x$ trên toàn $\mathbb R^p$ (Bài tập 05.8); hàm lỗi bình phương thỏa (S) với $\beta=2C_x^2$ nhưng (G) chỉ đúng trên $W$ bị chặn, với $G=2(BC_x+C_y)C_x$ (đoạn sau Định nghĩa 05.4); hàm lỗi bản lề và hàm lỗi của mạng ReLU theo trọng số không thỏa (S) (§9).
- Một câu: $\Delta_t$ của bài là khoảng cách giữa hai lần chạy (§4), khác đại lượng $\Delta_t=\lVert w_t-u\rVert^2$ trong chứng minh Định lý 05.14.

### `## 3. Ví dụ xuyên suốt`

- **Ví dụ 08.1 (Hàm lỗi Huber trên bốn quan sát)** (QĐ 8; PTN §3(a); `c1_numbers.txt`). **Thiết lập.** $\mathcal Z=\mathbb R$: mỗi quan sát là một số thực $z$, giả thuyết là một số $w\in W=\mathbb R$ ($p=1$), và hàm lỗi Huber (Huber loss) với ngưỡng $1$:
  $$\ell_{\mathrm H}(w,z)=\begin{cases}\tfrac12(w-z)^2,&\lvert w-z\rvert\le1,\\ \lvert w-z\rvert-\tfrac12,&\lvert w-z\rvert>1.\end{cases}$$
  Mẫu $s=(0,1,2,3)$, $m=4$; chưa có đại lượng ngẫu nhiên ngoài dãy chỉ số. **Bước 1: đạo hàm.** $\partial_w\ell_{\mathrm H}(w,z)$ là $w-z$ cắt vào đoạn $[-1,1]$ (viết $\max\{-1,\min\{1,w-z\}\}$; không đặt tên hàm phụ — `ky-hieu.md`). **Bước 2: ba hằng số.** Đạo hàm không giảm theo $w$ nên $\ell_{\mathrm H}(\cdot,z)$ lồi; phép cắt là $1$-Lipschitz nên $\ell_{\mathrm H}(\cdot,z)$ là $1$-trơn; $\lvert\partial_w\ell_{\mathrm H}\rvert\le1$ nên (G) đúng với $G=1$ **trên toàn $\mathbb R$ và với mọi $z$**, không cần dữ liệu bị chặn (khác hàm lỗi bình phương, đạo hàm $w-z$). Vậy (S), (G) đúng với $\beta=G=1$, và điều kiện độ dài bước là $\eta_t\le2$. **Bước 3: một lần chạy SGD** (phép cập nhật của Thuật toán 05.11 với $W=\mathbb R$, $w_1=0$, $\eta=\tfrac12$) với dãy chỉ số $(1,4,2,3,4,1)$: bảng bốn cột $t$, $i_t$, đạo hàm tại $w_t$, $w_{t+1}$: đạo hàm $0,-1,-\tfrac12,-1,-1,1$; điểm lặp $w_1,\ldots,w_7=0,0,\tfrac12,\tfrac34,\tfrac54,\tfrac74,\tfrac54$. **Kết luận.** Một câu: §4 đặt cạnh lần chạy này một lần chạy trên mẫu thay quan sát thứ tư, với cùng dãy chỉ số.
- **Khối `application`** — tiêu đề đề xuất: **"Huấn luyện nhiều vòng cho hồi quy logistic"**. **Thiết lập.** Hồi quy logistic trên hồ sơ như ứng dụng của Bài 05–06: $\lVert x\rVert\le1$, $W$ là quả cầu bán kính $5$, $w_1=0$ (giá trị giả định của Bài 05), nhưng chỉ có $m=10^4$ hồ sơ (giá trị giả định). **Câu hỏi thực hành.** Một vòng qua dữ liệu, mỗi hồ sơ dùng một lần, cho cận $5/\sqrt{10^4+1}\approx0{,}05$ cho rủi ro vượt mức kì vọng (Nhận xét 06.3). Chạy SGD nhiều vòng trên cùng $10^4$ hồ sơ có cho cận nhỏ hơn không, và với độ dài bước $0{,}05$, nên dừng sau bao nhiêu bước? (Trong ghi chú viết "trả lời ở §8"; nội dung là Ví dụ 08.7. Không dùng thuật ngữ "dừng sớm" ở đây; Định nghĩa 08.9 đứng sau. Không số liệu thật.)

Câu nối sang §4: ví dụ thứ nhất cho một mẫu nhỏ để so hai lần chạy bằng tay; ví dụ thứ hai cần một cận cho khoảng cách tổng quát hóa kì vọng của SGD nhiều vòng, đại lượng mà Bài 06 chưa chặn.

### `## 4. Hai lần chạy ghép cặp` (blueprint 8.6: khối "motivation/coupling 20", phần cuối)

**Câu mở:** "Định nghĩa 06.9 so hai kì vọng theo $\xi$: một cho lần chạy trên $s$, một cho lần chạy trên $s^{(i)}$. Để so hai lần chạy bước theo bước, ta cho chúng dùng chung mọi lựa chọn ngẫu nhiên."

1. **Thuật toán 08.1 (SGD có chiếu trên một mẫu cố định với độ dài bước thay đổi)** (QĐ 1, 2). Dạng như Thuật toán 05.11. **Đầu vào** (danh sách): **Mẫu.** $s=(z_1,\ldots,z_m)$. **Tập tham số.** $W$ khác rỗng, đóng, lồi (có thể là $\mathbb R^p$). **Độ dài bước.** Dãy tất định $\eta_1,\ldots,\eta_T>0$. **Số bước.** $T\ge1$. **Khởi tạo.** $w_1\in W$, tất định. **Cập nhật.** Với $t=1,\ldots,T$: rút $i_t$ đều trên $\{1,\ldots,m\}$, có hoàn lại, độc lập với các lần rút trước; đặt $w_{t+1}=\operatorname{proj}_W\big(w_t-\eta_t\nabla\ell(w_t,z_{i_t})\big)$. **Đầu ra.** Điểm lặp cuối $w_{T+1}$; ở §7–§8 cũng xét điểm lặp trung bình $\bar w_T=\tfrac1T\sum_{t=1}^Tw_t$. **Điều kiện dừng.** Sau đúng $T$ bước, $T$ và các $\eta_t$ chọn trước khi chạy. **Chi phí.** $T$ gradient trên một quan sát và $T$ phép chiếu.

   Đoạn đọc sau (ba câu): với $\eta_t=\eta$ hằng và đầu ra $\bar w_T$, đây là Thuật toán 05.11 với oracle của Hệ quả 05.19; với $W=\mathbb R^p$, đây là SGD không chiếu của HRS và của thí nghiệm mở đầu. Theo Định nghĩa 05.18, $A(s;\xi)=w_{T+1}$ với $\xi=(i_1,\ldots,i_T)$, có $m^T$ giá trị đồng khả năng, độc lập với $S$. Khi $T>m$, mỗi quan sát được dùng trung bình $T/m$ lần, nên điểm lặp phụ thuộc quan sát sắp dùng; Hệ quả 06.2 không áp dụng (Nhận xét 06.3).
2. **Định nghĩa 08.2 (Hai lần chạy ghép cặp và ngân sách độ dài bước)** (blueprint 8.2; QĐ 10). Câu dẫn "Cho mẫu $s$, chỉ số $i\in\{1,\ldots,m\}$, quan sát thay thế $z'\in\mathcal Z$ và mẫu lân cận $s^{(i)}$ như Định nghĩa 06.9, cùng các đầu vào khác của Thuật toán 08.1." Danh sách nhãn:
   - **Hai lần chạy ghép cặp.** Hai lần chạy của Thuật toán 08.1, một trên $s$ với điểm lặp $w_t$, một trên $s^{(i)}$ với điểm lặp $w'_t$, dùng chung $w_1=w'_1$, chung các $\eta_t$ và chung dãy chỉ số $\xi=(i_1,\ldots,i_T)$ (coupled runs).
   - **Bước chung và bước khác biệt.** Bước $t$ là *bước chung* nếu $i_t\ne i$ (hai lần chạy dùng cùng quan sát $z_{i_t}$) và là *bước khác biệt* nếu $i_t=i$ (lần chạy thứ nhất dùng $z_i$, lần chạy thứ hai dùng $z'$).
   - **Khoảng cách.** $\Delta_t=\lVert w_t-w'_t\rVert$ với $t=1,\ldots,T+1$; $\Delta_1=0$.
   - **Ngân sách độ dài bước.** Tổng $\sum_{t=1}^T\eta_t$ (cumulative step-size budget); bằng $\eta T$ khi độ dài bước hằng.

   Đoạn đọc sau: hai lần chạy chỉ khác nhau ở các bước khác biệt, và mỗi bước là bước khác biệt với xác suất $1/m$. Ghép cặp là một cách đặt hai lần chạy trên cùng không gian xác suất của $\xi$; mỗi lần chạy riêng vẫn có đúng phân bố của Thuật toán 08.1, nên hai kì vọng của Định nghĩa 06.9 không đổi, và $\lvert\mathbb E_\xi a-\mathbb E_\xi b\rvert\le\mathbb E_\xi\lvert a-b\rvert$ cho phép chặn hiệu hai kì vọng qua quỹ đạo (lời hứa Bài 06, đoạn sau Định nghĩa 06.9). **Ví dụ:** ví dụ Huber ngay dưới (viết "ví dụ dưới đây"). **Không-ví dụ** (tất định, PTN (d5) bản tính tay†): hai lần chạy trên **cùng** mẫu $s$ của Ví dụ 08.1 với hai dãy chỉ số khác nhau, $i_1=1$ và $i'_1=4$: sau một bước, $w_2=0$ và $w'_2=\tfrac12$, nên khoảng cách $\tfrac12>0$ dù hai mẫu như nhau. Khoảng cách của hai lần chạy không ghép cặp đo tính ngẫu nhiên của thuật toán, không đo độ nhạy theo một quan sát của mẫu; số của thí nghiệm ở §7.
3. **Ví dụ 08.2 (Hai lần chạy ghép cặp trong ví dụ Huber)** (PTN §3(a); `c1_numbers.txt`). **Thiết lập.** Ví dụ 08.1 với $i=4$, $z'=-3$, $s^{(4)}=(0,1,2,-3)$, $\eta=\tfrac12$, dãy chỉ số $(1,4,2,3,4,1)$. **Bước 1: lần chạy trên $s^{(4)}$.** $w'_1,\ldots,w'_7=0,0,-\tfrac12,0,\tfrac12,0,0$ (bảng như Ví dụ 08.1). **Bước 2: khoảng cách.** $\Delta_1,\ldots,\Delta_7=0,0,1,\tfrac34,\tfrac34,\tfrac74,\tfrac54$. **Bước 3: hai loại bước.** Ở bước khác biệt $t=2$ và $t=5$, $\Delta$ tăng đúng $1=2G\eta$ ($0\to1$, $\tfrac34\to\tfrac74$); ở các bước chung, $\Delta$ không tăng ($1\to\tfrac34$, $\tfrac34\to\tfrac34$, $\tfrac74\to\tfrac54$; bước $t=1$: $0\to0$). **Bước 4: ngân sách.** $\sum_{t=1}^6\eta_t=3$; dãy có hai bước khác biệt, nên tổng các phần tăng ở Bước 3 là $2\cdot2G\eta=2$, và $\Delta_7=\tfrac54\le2$. **Kết luận.** Khoảng cách chỉ tăng ở các bước dùng quan sát khác biệt, mỗi lần không quá $2G\eta$; ở các bước chung nó không tăng.

**Câu kết §4:** cận cho $\mathbb E_\xi\Delta_{T+1}$ cần hai sự kiện: một bước chung không làm tăng khoảng cách, và một bước khác biệt làm tăng nó không quá $2G\eta_t$.

### `## 5. Bước gradient không giãn` (khối "nonexpansiveness 20")

**Câu mở:** "Ở một bước chung, hai lần chạy áp dụng cùng một ánh xạ $w\mapsto\operatorname{proj}_W(w-\eta_t\nabla\ell(w,z_{i_t}))$ cho hai điểm $w_t$ và $w'_t$. Cần biết ánh xạ này kéo hai điểm lại gần hay đẩy chúng ra xa."

1. **Định nghĩa 08.3 (Hệ số giãn, ánh xạ không giãn và tính đồng bức)** (PTN §1, HRS Def 2.3–2.4, Def 3.6; `thuat-ngu.md` §10). Câu dẫn "Cho ánh xạ $\Gamma:\mathbb R^p\to\mathbb R^p$, hàm khả vi $f:\mathbb R^p\to\mathbb R$, $c\ge0$ và $\beta>0$." Danh sách nhãn:
   - **Hệ số giãn.** $\Gamma$ có *hệ số giãn* $c$ (expansion factor) nếu $\lVert\Gamma(u)-\Gamma(v)\rVert\le c\lVert u-v\rVert$ với mọi $u,v$.
   - **Không giãn.** $\Gamma$ *không giãn* (nonexpansive) nếu có hệ số giãn $1$.
   - **Tính đồng bức.** Gradient $\nabla f$ là *$\tfrac1\beta$-đồng bức* (co-coercive) nếu $\langle\nabla f(u)-\nabla f(v),u-v\rangle\ge\tfrac1\beta\lVert\nabla f(u)-\nabla f(v)\rVert^2$ với mọi $u,v$ (hiển thị bằng `aligned`, hai dòng).

   Đoạn đọc sau: *ánh xạ bước gradient* (gradient step map) $\Gamma_{\eta,z}(w)=w-\eta\nabla\ell(w,z)$; hợp của hai ánh xạ có hệ số giãn $c_1$, $c_2$ có hệ số giãn $c_1c_2$; phép chiếu $\operatorname{proj}_W$ không giãn (Bài 05). Theo Cauchy–Schwarz, tính $\tfrac1\beta$-đồng bức kéo theo $\nabla f$ là $\beta$-Lipschitz, tức $f$ là $\beta$-trơn; bổ đề dưới đây cho chiều ngược lại khi $f$ lồi. **Ví dụ:** $f(w)=\tfrac\beta2\lVert w\rVert^2$: vế trái bằng $\beta\lVert u-v\rVert^2$, vế phải bằng $\beta\lVert u-v\rVert^2$, dấu bằng. **Không-ví dụ:** $f(w)=-\tfrac12w^2$ trên $\mathbb R$ là $1$-trơn nhưng vế trái bằng $-(u-v)^2<0$ khi $u\ne v$, nên $\nabla f$ không đồng bức với hằng số nào.
2. **Bổ đề 08.4 (Bước gradient không giãn) — phác thảo (tính đồng bức chứng minh ở Phụ lục A)** (blueprint Lemma 8.1 [S]; QĐ 2, 4; PTN §2.1). **Giả thiết.** $f:\mathbb R^p\to\mathbb R$ lồi và $\beta$-trơn trên toàn $\mathbb R^p$; $0\le\eta\le2/\beta$; $W$ khác rỗng, đóng, lồi. (Ba thành phần: viết thành danh sách **Hàm.** / **Độ dài bước.** / **Tập.**) **Bảo đảm** (tất định), danh sách:
   - **(a) Tính đồng bức.** $\nabla f$ là $\tfrac1\beta$-đồng bức.
   - **(b) Bước gradient không giãn.** Với $\Gamma(w)=w-\eta\nabla f(w)$ và mọi $u,v$:
     $$\begin{aligned}&\lVert\Gamma(u)-\Gamma(v)\rVert^2\\&\le\lVert u-v\rVert^2\\&\quad-\eta\big(\tfrac2\beta-\eta\big)\lVert\nabla f(u)-\nabla f(v)\rVert^2\\&\le\lVert u-v\rVert^2 .\end{aligned}$$
   - **(c) Bước có chiếu.** $w\mapsto\operatorname{proj}_W(\Gamma(w))$ không giãn.

   **Chứng minh** (khoảng 180 tiếng). Lộ trình: (a) ở Phụ lục A; (b) khai triển bình phương rồi dùng (a); (c) hợp hai ánh xạ không giãn. Bước (b): $\lVert\Gamma(u)-\Gamma(v)\rVert^2=\lVert u-v\rVert^2-2\eta\langle\nabla f(u)-\nabla f(v),u-v\rangle+\eta^2\lVert\nabla f(u)-\nabla f(v)\rVert^2$ (`aligned`, ba dòng); (a) thay số hạng giữa bằng $-\tfrac{2\eta}\beta\lVert\cdot\rVert^2$ — **tính lồi và tính trơn dùng ở đây, qua (a)**; $\eta\le2/\beta$ cho hệ số $\eta(2/\beta-\eta)\ge0$ — **điều kiện độ dài bước dùng ở đây**. Bước (c): tính không giãn của $\operatorname{proj}_W$ (đoạn sau Bổ đề 05.8). Câu sau $\square$: một bước SGD trên một hàm lỗi lồi, trơn, với $\eta_t\le2/\beta$, không làm tăng khoảng cách giữa hai điểm bất kì, nên ở bước chung $\Delta_{t+1}\le\Delta_t$.
3. Một đoạn ngắn (trực giác một chiều, PTN §2.1): khi $p=1$ và $f$ hai lần khả vi, đạo hàm của ánh xạ bước là $1-\eta f''(w)$, với $0\le f''\le\beta$ (lồi và trơn), nên nằm trong $[1-\eta\beta,1]\subset[-1,1]$ khi $\eta\le2/\beta$.
4. **Ví dụ 08.3 (Hệ số giãn của bước gradient một chiều)** (`c1_numbers.txt`). **Thiết lập.** $p=1$, ba hàm, độ dài bước $\eta\in\{\tfrac12,2,3\}$. **Bước 1: hàm bậc hai** $f(w)=\tfrac12w^2$, $\beta=1$: $\Gamma(w)=(1-\eta)w$, hệ số giãn $\lvert1-\eta\rvert$: $\tfrac12$; $1$; $2$. **Bước 2: hàm lỗi Huber** của Ví dụ 08.1: $\Gamma$ có hệ số góc $1-\eta$ khi $\lvert w-z\rvert<1$ và $1$ khi $\lvert w-z\rvert>1$, nên hệ số giãn $\max\{\lvert1-\eta\rvert,1\}$: $1$; $1$; $2$. **Bước 3: hàm lõm** $f(w)=-\tfrac12w^2$ ($1$-trơn, không lồi): $\Gamma(w)=(1+\eta)w$, hệ số giãn $1+\eta>1$ với mọi $\eta>0$: $1{,}5$; $3$; $4$. **Kết luận.** Ngưỡng $2/\beta$ là chặt (hàm bậc hai với $\eta=2$ có hệ số giãn đúng bằng $1$); bỏ tính lồi thì bước gradient giãn với mọi độ dài bước (§9).

**Câu kết §5:** tính lồi, tính trơn và điều kiện $\eta_t\le2/\beta$ chỉ đi vào chứng minh qua bổ đề này, tức qua các bước chung.

### `## 6. Bất đẳng thức truy hồi cho khoảng cách giữa hai lần chạy` (khối "recurrence 30")

**Câu mở:** "Bổ đề 08.4 xử lý bước chung. Ở bước khác biệt, hai lần chạy dùng hai quan sát khác nhau, và cận gradient (G) giới hạn khoảng cách mà bước đó tạo ra."

1. **Mệnh đề 08.5 (Bất đẳng thức truy hồi cho khoảng cách giữa hai lần chạy ghép cặp) — chứng minh đầy đủ** (blueprint Proposition 8.2 [F]; PTN §2.2). **Giả thiết** (danh sách): **Hàm lỗi.** (S) với hằng số $\beta$; (G) với hằng số $G$. **Mẫu.** $s$, $i$, $z'$ bất kì, cố định; $s^{(i)}$ như Định nghĩa 06.9. **Thuật toán.** Hai lần chạy ghép cặp của Thuật toán 08.1 (Định nghĩa 08.2), với $0<\eta_t\le2/\beta$. **Chỉ số.** Với mọi $t$, $\Pr(i_t=i)=1/m$ (đúng khi rút đều có hoàn lại). **Bảo đảm**, danh sách:
   - **(a) Trên từng quỹ đạo** (tất định, mọi giá trị của $\xi$): với mọi $t$,
     $$\Delta_{t+1}\le\Delta_t+2G\eta_t\,\mathbb 1[i_t=i],$$
     nên $\Delta_{T+1}\le2G\sum_{t=1}^T\eta_t\mathbb 1[i_t=i]$.
   - **(b) Theo kì vọng theo $\xi$** (mẫu cố định): $\mathbb E\Delta_{t+1}\le\mathbb E\Delta_t+\tfrac{2G\eta_t}m$ và
     $$\mathbb E\Delta_{T+1}\le\frac{2G}m\sum_{t=1}^T\eta_t .$$

   Dòng diễn giải: cận đúng với mọi mẫu và mọi cách thay một quan sát, không dùng $D$, không phụ thuộc $p$.

   **Chứng minh** (khoảng 350 tiếng; `aligned`). Lộ trình: so một bước trên hai quỹ đạo theo hai trường hợp, cộng dọc quỹ đạo, rồi lấy kì vọng bằng tính tuyến tính. **Bước 1 (bước chung; (S) và $\eta_t\le2/\beta$ qua Bổ đề 08.4(c)).** Nếu $i_t\ne i$, cả hai lần chạy áp dụng cùng ánh xạ $\operatorname{proj}_W\circ\Gamma_{\eta_t,z_{i_t}}$, nên $\Delta_{t+1}\le\Delta_t$. **Bước 2 (bước khác biệt; (G) tại $z_i$ và $z'$).** Nếu $i_t=i$: phép chiếu không giãn; thêm bớt điểm trung gian $w'_t-\eta_t\nabla\ell(w'_t,z_i)$; bất đẳng thức tam giác:
   $$\begin{aligned}\Delta_{t+1}&\le\lVert\Gamma_{\eta_t,z_i}(w_t)-\Gamma_{\eta_t,z_i}(w'_t)\rVert\\&\quad+\eta_t\lVert\nabla\ell(w'_t,z_i)-\nabla\ell(w'_t,z')\rVert\\&\le\Delta_t+2G\eta_t .\end{aligned}$$
   Số hạng đầu dùng Bổ đề 08.4(b); số hạng sau dùng (G) hai lần tại $w'_t\in W$ (vì $w'_1\in W$ và mỗi điểm lặp sau là một phép chiếu lên $W$) — **$2G$ vì hai gradient tại hai quan sát khác nhau, mỗi gradient có chuẩn không quá $G$, có thể ngược hướng**. **Bước 3 (tổng triệt tiêu).** Gộp hai trường hợp được (a); cộng từ $t=1$ đến $T$, dùng $\Delta_1=0$. **Bước 4 (kì vọng; giả thiết về chỉ số dùng ở đây).** $\xi$ có hữu hạn giá trị, nên mọi kì vọng là trung bình hữu hạn; lấy kì vọng hai vế của (a), dùng $\mathbb E\,\mathbb 1[i_t=i]=\Pr(i_t=i)=1/m$. Một câu bắt buộc: bước này chỉ dùng tính tuyến tính của kì vọng và xác suất biên của $i_t$; không cần $i_t$ độc lập với $\Delta_t$, vì (a) đúng trên từng quỹ đạo. Câu sau $\square$: thừa số $1/m$ là xác suất một bước dùng quan sát khác biệt; mỗi lần như vậy khoảng cách tăng không quá $2G\eta_t$.
2. Đoạn ngắn sau mệnh đề (hai ý, khoảng 90 tiếng): (i) **hằng số $2G$ là chặt** (PTN §2.2): với hàm lỗi Huber, $w'_t=1$, $z_i=3$, $z'=-3$, $\eta=\tfrac12$, hai bước cho $\tfrac32$ và $\tfrac12$, khác nhau đúng $1=2G\eta$; (ii) **xáo trộn lại sau mỗi vòng qua dữ liệu** (Định nghĩa 05.10, đoạn sau): mỗi vòng là một hoán vị đều của $\{1,\ldots,m\}$, nên vẫn có $\Pr(i_t=i)=1/m$ và (a), (b) giữ nguyên (Phụ lục B).
3. **Ví dụ 08.4 (Kì vọng của khoảng cách trong ví dụ Huber)** (PTN §3(a); `c1_numbers.txt`). **Thiết lập.** Ví dụ 08.2, nhưng dãy chỉ số ngẫu nhiên, đều trên $\{1,2,3,4\}^T$; cận (b) là $\tfrac{2G\eta T}m=\tfrac T4$. **Bước 1: $T=1$.** $\Delta_2=1$ nếu $i_1=4$ và $0$ nếu không, nên $\mathbb E\Delta_2=\tfrac14$: dấu bằng trong (b). **Bước 2: $T=2$, liệt kê $16$ dãy theo hai nhóm** (danh sách, mỗi nhóm một dòng): $i_1\ne4$ ($12$ dãy, hai lần chạy cùng điểm $w_2$): $\Delta_3=1$ khi $i_2=4$, đóng góp $3$; $i_1=4$ ($4$ dãy, $w_2=\tfrac12$, $w'_2=-\tfrac12$): $\Delta_3=\tfrac12,\tfrac34,1,2$ với $i_2=1,2,3,4$, đóng góp $\tfrac{17}4$. Vậy $\mathbb E\Delta_3=\tfrac{3+17/4}{16}=\tfrac{29}{64}\approx0{,}4531<\tfrac12$. **Bước 3: $T=6$** (liệt kê $4^6=4096$ dãy bằng máy): $\mathbb E\Delta_7=\tfrac{228\,203}{262\,144}\approx0{,}8705\le\tfrac64=1{,}5$†. **Bước 4: quỹ đạo đạt cận (a).** Dãy $(2,3,1,4,4,4)$: $\Delta_7=3=2G\eta\cdot3$. **Kết luận.** Cận đạt dấu bằng ở bước đầu; sau đó các bước chung kéo hai lần chạy lại gần (Bước 2: $1\to\tfrac12$), nên kì vọng tăng chậm hơn cận.

   Ghi chú cho người viết: PTN ghi $T=5$ ($0{,}8053\le1{,}25$); dàn ý chọn $T=6$ để khớp Ví dụ 08.1–08.2 và câu ôn nhanh 3. Phân số $228\,203/262\,144$ đã kiểm bằng phân số chính xác.

**Câu kết §6:** theo kì vọng, khoảng cách giữa hai lần chạy không vượt $\tfrac{2G}m$ nhân ngân sách độ dài bước, với mọi mẫu và mọi cách thay một quan sát; cận không dùng phân bố $D$.

*(Nghỉ 10 phút trước §7.)*

### `## 7. Tính ổn định đều của SGD` (khối "stability theorem/interpretation 30", phần đầu)

**Câu mở:** "Theo (G), hàm lỗi tại một quan sát kiểm tra bất kì thay đổi không quá $G$ nhân khoảng cách giữa hai điểm lặp. Ghép điều này với Mệnh đề 08.5 cho tính ổn định đều theo Định nghĩa 06.9, rồi Định lý 06.10 cho cận khoảng cách tổng quát hóa."

1. **Định lý 08.6 (Tính ổn định đều của SGD với hàm lỗi lồi và trơn) — chứng minh đầy đủ** (blueprint Theorem 8.3 [F]; QĐ 1, 2, 3; HRS Thm 3.8 tr. 9; PTN §2.3). **Giả thiết** (danh sách, mẫu Định lý 06.10): **Mẫu.** $S\sim D^m$ theo dạng đầy đủ của (T1) (chỉ cho (c)). **Hàm lỗi.** (T2); (S) với $\beta$; (G) với $G$. **Tập tham số.** $W$ khác rỗng, đóng, lồi (có thể là $\mathbb R^p$); $w_1\in W$ tất định. **Thuật toán.** Thuật toán 08.1 với $0<\eta_t\le2/\beta$ tất định; $\xi=(i_1,\ldots,i_T)$ độc lập với $S$; đầu ra $A(S;\xi)=w_{T+1}$. **Bảo đảm**, danh sách; đặt $\epsilon_T=\tfrac{2G^2}m\sum_{t=1}^T\eta_t$ (hoặc viết thẳng vế phải mỗi lần; điểm mở 4):
   - **(a) Dạng ghép cặp** (theo kì vọng theo $\xi$, với mọi $s$, $i$, $z'$ và mọi quan sát kiểm tra $z\in\mathcal Z$): $\mathbb E_\xi\lvert\ell(w_{T+1},z)-\ell(w'_{T+1},z)\rvert\le\frac{2G^2}m\sum_{t=1}^T\eta_t$, với $w'_{T+1}$ là điểm lặp cuối của lần chạy ghép cặp trên $s^{(i)}$.
   - **(b) Ổn định đều.** Thuật toán ổn định đều (Định nghĩa 06.9) với $\epsilon_{\mathrm{stab}}(m)=\frac{2G^2}m\sum_{t=1}^T\eta_t$.
   - **(c) Khoảng cách tổng quát hóa kì vọng** (theo kì vọng theo $(S,\xi)$): $\big\lvert\mathbb E_{S,\xi}[L_D(w_{T+1})-L_S(w_{T+1})]\big\rvert\le\frac{2G^2}m\sum_{t=1}^T\eta_t$.

   Đoạn trong khối: với độ dài bước hằng, vế phải là $2G^2\eta T/m$. Cận không phụ thuộc $p$ hay kích thước của $W$, phụ thuộc quỹ đạo chỉ qua ngân sách độ dài bước, chỉ theo kì vọng; đại lượng được chặn là khoảng cách tổng quát hóa kì vọng, không phải $\mathbb E\lvert L_D-L_S\rvert$ và không phải $L_D$. Đây là bảo đảm cho một thuật toán với quy tắc rút chỉ số đã nêu, không cho mọi thuật toán tối ưu (blueprint 8.3).

   **Chứng minh** (khoảng 330 tiếng). Lộ trình: Lipschitz của hàm lỗi kiểm tra, Mệnh đề 08.5, hiệu hai kì vọng, tính khả tích, Định lý 06.10. **Bước 1 ((G) và Mệnh đề 05.5(a) với $U=W$).** Với mọi $z\in\mathcal Z$ và $u,v\in W$: $\lvert\ell(u,z)-\ell(v,z)\rvert\le G\lVert u-v\rVert$ — **(G) dùng lần thứ hai, tại mọi quan sát kiểm tra**. **Bước 2 (Mệnh đề 08.5(b)).** Vì $w_{T+1},w'_{T+1}\in W$: $\mathbb E_\xi\lvert\ell(w_{T+1},z)-\ell(w'_{T+1},z)\rvert\le G\,\mathbb E_\xi\Delta_{T+1}\le\tfrac{2G^2}m\sum_t\eta_t$, tức (a). **Bước 3 (hiệu hai kì vọng).** Ghép cặp không đổi phân bố của từng lần chạy, nên $\lvert\mathbb E_\xi\ell(w_{T+1},z)-\mathbb E_\xi\ell(w'_{T+1},z)\rvert\le\mathbb E_\xi\lvert\cdot\rvert$, và mọi kì vọng hữu hạn ($\xi$ có hữu hạn giá trị); đó là điều kiện của Định nghĩa 06.9, tức (b). **Bước 4 (khả tích; (G), (T2)).** Phép chiếu không giãn và $w_1\in W$ cho $\lVert w_{t+1}-w_1\rVert\le\lVert w_t-w_1\rVert+\eta_tG$, nên $\lVert w_{T+1}-w_1\rVert\le G\sum_t\eta_t$; theo Bước 1, $\ell(w_{T+1},z)\le\ell(w_1,z)+G^2\sum_t\eta_t$; lấy kì vọng, $\mathbb EL_D(w_{T+1})\le L_D(w_1)+G^2\sum_t\eta_t<\infty$ theo (T2). Tính đo được: Phụ lục B. **Bước 5 (Định lý 06.10; (T1)).** Áp dụng cho $A(S;\xi)=w_{T+1}$, được (c). Câu sau $\square$: với hàm lỗi lồi, trơn, có gradient bị chặn, SGD trên một mẫu cố định có khoảng cách tổng quát hóa kì vọng nhỏ khi ngân sách độ dài bước nhỏ so với cỡ mẫu, bất kể số chiều.
2. Đoạn sau định lý (khoảng 120 tiếng; PTN §2.3, §4): ba giả thiết vào ba chỗ khác nhau — (G) hai lần với hai vai trò (gradient tại quan sát huấn luyện và quan sát thay thế ở bước khác biệt; tính Lipschitz của hàm lỗi tại mọi quan sát kiểm tra), $\beta$ chỉ qua điều kiện $\eta_t\le2/\beta$, tính lồi chỉ qua Bổ đề 08.4(a). So với Mệnh đề 06.11 ($2G^2/(\lambda m)$): cùng dạng $2G^2(\cdot)/m$ với $1/\lambda$ thay bằng $\sum_t\eta_t$; đây là so sánh hình thức, không phải một định lý.
3. **Ví dụ 08.5 (Cận ổn định cho hồi quy logistic)** (PTN §3(b); `c1_numbers.txt`). **Thiết lập.** Hồi quy logistic với $\lVert x\rVert\le1$ trên toàn $\mathcal X$, $W=\mathbb R^p$ hoặc quả cầu bán kính $5$. **Bước 1: hằng số** (Bài tập 05.8): (S) với $\beta=\tfrac14$, (G) với $G=1$ trên toàn $\mathbb R^p$; điều kiện độ dài bước $\eta_t\le8$; $\ell\ge0$ và $L_D(0)=\ln2$, nên (T2) đúng với $w_1=0$. **Bước 2: ứng dụng của Bài 05** ($m=10^6$, $\eta=0{,}05$, $T=10^4$ của Ví dụ 05.9): $\tfrac{2\cdot1\cdot0{,}05\cdot10^4}{10^6}=0{,}001$; số bước chỉ bằng $1\%$ của một vòng. **Bước 3: thí nghiệm mở đầu** ($m=200$, $\eta=0{,}5$): sau $t$ bước, cận $\tfrac{2\cdot0{,}5\,t}{200}=\tfrac t{200}$: $1$ sau một vòng, $100$ sau $100$ vòng. **Kết luận.** Cận tăng tuyến tính theo số bước; nó nhỏ khi $T\eta\ll m$, và với $200$ quan sát nó vượt $1$ ngay từ vòng thứ hai.
4. **Ví dụ 08.6 (Hai lần chạy ghép cặp trong thí nghiệm mở đầu)** (QĐ 7; PTN §3(e); `exp_p100_eta05.txt`). **Thiết lập.** Giao thức ở Phụ lục D; với mỗi hạt giống, một mẫu lân cận: thay quan sát có chỉ số rút đều bằng một quan sát mới từ $D$; hai lần chạy ghép cặp; thêm một lần chạy thứ ba trên **cùng** mẫu với dãy chỉ số độc lập (không ghép cặp). **Bước 1: giả thiết nào thỏa** (danh sách ngắn, bắt buộc): (T1) cho mẫu huấn luyện và mẫu kiểm tra; (T2); (S) với $\beta=\tfrac14$; (G) với $G=1$, vì **mọi** đặc trưng có thể có đều thỏa $\lVert x\rVert\le1$ (do cách sinh dữ liệu, không chỉ trên mẫu); $\eta=0{,}5\le8$; $W=\mathbb R^p$; chỉ số đều có hoàn lại. Vậy Định lý 08.6 áp dụng, và (a) chặn $\mathbb E_\xi\Delta$ của từng cặp mẫu lân cận, nên chặn cả trung bình theo các cặp. **Bước 2: bảng** (năm cột):

   | Số vòng | $\Delta$ ghép cặp | Cận $t/200$ | $\Delta$ không ghép cặp | Tỉ lệ đổi nhãn |
   |---|---|---|---|---|
   | $0{,}5$ | $0{,}142$ | $0{,}5$ | $2{,}99$ | $0{,}015$ |
   | $1$ | $0{,}233$ | $1$ | $3{,}83$ | $0{,}016$ |
   | $5$ | $0{,}873$ | $5$ | $4{,}90$ | $0{,}022$ |
   | $20$ | $2{,}219$ | $20$ | $4{,}82$ | $0{,}026$ |
   | $100$ | $5{,}458$ | $100$ | $4{,}00$ | $0{,}034$ |

   (trung bình $20$ hạt giống; "tỉ lệ đổi nhãn" là tỉ lệ điểm kiểm tra mà hai lần chạy ghép cặp dự đoán nhãn khác nhau; số dự kiến: $0{,}1417$; $0{,}2332$; $0{,}8732$; $2{,}2185$; $5{,}4583$ / $2{,}9942$; $3{,}8273$; $4{,}9029$; $4{,}8228$; $4{,}0015$ / $0{,}0152$; $0{,}0159$; $0{,}0218$; $0{,}0262$; $0{,}0339$; khoảng giữa các hạt giống của $\Delta$ ghép cặp ở $100$ vòng: $1{,}31$–$15{,}08$†.) **Bước 3: khoảng cách tổng quát hóa.** Cột "Khoảng cách" của câu hỏi mở đầu ước lượng $\mathbb E[L_D-L_S]$ (thay $L_D$ bằng trung bình trên $5000$ quan sát kiểm tra); cận lớn hơn nó từ khoảng $11$ đến khoảng $109$ lần; khoảng giữa các hạt giống ở $100$ vòng: $0{,}693$–$1{,}149$†. **Bước 4: đọc.** $\Delta$ ghép cặp tăng chậm hơn tuyến tính và luôn dưới cận; $\Delta$ không ghép cặp đã cỡ $3$–$5$ từ nửa vòng đầu (ngẫu nhiên của thuật toán, không phải độ nhạy theo mẫu); tỉ lệ đổi nhãn không được định lý chặn, vì hàm lỗi 0–1 không Lipschitz theo $w$. **Kết luận.** Thí nghiệm khớp với định lý ở chỗ định lý khẳng định (các đại lượng nằm dưới cận), nhưng cận tăng tuyến tính còn đại lượng đo được tăng chậm hơn; đường cong thí nghiệm không phải là cận và cận không dự đoán được chúng (blueprint 8.5 bài 6).
5. **Hệ quả 08.7 (Tính ổn định của điểm lặp trung bình) — chứng minh đầy đủ** (QĐ 3; PTN §2.4). **Giả thiết.** Như Định lý 08.6, với đầu ra $A(S;\xi)=\bar w_T=\tfrac1T\sum_{t=1}^Tw_t$. **Bảo đảm.** Ổn định đều với
   $$\epsilon_{\mathrm{stab}}(m)=\frac{2G^2}m\sum_{t=1}^{T-1}\frac{T-t}T\,\eta_t,$$
   bằng $\frac{G^2\eta(T-1)}m$ khi độ dài bước hằng; cùng số đó chặn trị tuyệt đối của khoảng cách tổng quát hóa kì vọng của $\bar w_T$. **Chứng minh** (khoảng 160 tiếng): $\bar w_T\in W$ vì $W$ lồi; bất đẳng thức tam giác cho $\lVert\bar w_T-\bar w'_T\rVert\le\tfrac1T\sum_{t=1}^T\Delta_t$; Mệnh đề 08.5(b) áp dụng tới bước $t-1$: $\mathbb E\Delta_t\le\tfrac{2G}m\sum_{s=1}^{t-1}\eta_s$; đổi thứ tự lấy tổng, $\sum_{t=1}^T\sum_{s=1}^{t-1}\eta_s=\sum_{s=1}^{T-1}(T-s)\eta_s$ (`aligned`); với $\eta$ hằng, $\sum_{s=1}^{T-1}(T-s)=T(T-1)/2$; các Bước 1, 3, 4, 5 như Định lý 08.6. Câu sau $\square$: với độ dài bước hằng, cận của điểm lặp trung bình nhỏ hơn một nửa cận của điểm lặp cuối, vì các điểm lặp đầu chưa kịp tách.
6. Đoạn ngắn sau hệ quả (lời hứa Bài 06; khoảng 70 tiếng): SGD có chiếu nhiều vòng ở §5 Bài 06 (Ví dụ 06.3: hàm lỗi $(w-y)^2$ trên $W=[-1,1]$, $m=4$, $\eta=0{,}00625$, $T=1600$) thỏa (S) với $\beta=2$ và (G) với $G=4$ trên $W$, $\eta\le1=2/\beta$; Hệ quả 08.7 cho $16\cdot0{,}00625\cdot1599/4=39{,}975$, tức không quá $39{,}98$, đúng nhưng không cho thông tin so với khoảng cách thật $0{,}4750$ (Bài tập 08.7).

**Câu kết §7:** cận ổn định không phụ thuộc số chiều và tăng theo ngân sách độ dài bước; muốn chặn chính rủi ro kì vọng, cần cộng thêm sai số tối ưu, đại lượng giảm khi số bước tăng.

### `## 8. Đánh đổi giữa tối ưu và ổn định` (khối "stability theorem/interpretation 30", phần cuối)

**Câu mở:** "Theo Mệnh đề 06.5(b), rủi ro vượt mức kì vọng không quá khoảng cách tổng quát hóa kì vọng cộng kì vọng của sai số tối ưu thực nghiệm. Với SGD có chiếu, số hạng thứ hai giảm khi $T$ tăng (Định lý 05.14), còn số hạng thứ nhất tăng (Hệ quả 08.7)."

1. **Hệ quả 08.8 (Rủi ro vượt mức kì vọng của SGD nhiều vòng) — chứng minh đầy đủ** (blueprint Corollary [F]; QĐ 3; PTN §2.5; HRS Prop 5.4 tr. 19). **Giả thiết** (danh sách): **Mẫu.** $S\sim D^m$ theo (T1). **Hàm lỗi.** (T2), (S), (G). **Tập tham số.** $W$ khác rỗng, đóng, lồi, **bị chặn**; $w_1\in W$; $R\ge\sup_{u\in W}\lVert w_1-u\rVert$. **Thuật toán.** Thuật toán 08.1 với độ dài bước hằng $0<\eta\le2/\beta$; đầu ra $\bar w_T$. **Bảo đảm** (theo kì vọng theo $(S,\xi)$), danh sách:
   - **(a) Cận ghép.** $\mathbb E_{S,\xi}L_D(\bar w_T)-\inf_WL_D\le\frac{R^2}{2\eta T}+\frac{\eta G^2}2+\frac{\eta G^2(T-1)}m$ (`aligned`, ba dòng).
   - **(b) Độ dài bước tốt nhất với $T$ cho trước.** Với $\eta^*=\frac R{G\sqrt{T(1+2(T-1)/m)}}$, nếu $\eta^*\le2/\beta$, vế phải của (a) bằng $RG\sqrt{\frac{1+2(T-1)/m}T}$; giá trị này không quá $RG\sqrt{3/m}$ khi $T=m$ và giảm về $RG\sqrt{2/m}$ khi $T\to\infty$.

   Đoạn trong khối: vế trái là rủi ro vượt mức kì vọng so với $W$; cận không phụ thuộc $p$; (b) luôn lớn hơn cận $RG/\sqrt{m+1}$ của một vòng qua dữ liệu với quan sát mới (Nhận xét 06.3): khoảng $\sqrt3$ lần khi $T=m$, khoảng $\sqrt2$ lần khi $T\to\infty$. (Cho người viết và người rà toán: $\tfrac{1+2(T-1)/m}T=\tfrac2m+\tfrac{1-2/m}T$ giảm theo $T$ khi $m>2$; và $\tfrac{1+2(T-1)/m}T\ge\tfrac1{m+1}$ tương đương $(m-2)(m+1)+T(m+2)\ge0$, đúng với mọi $m\ge1$, $T\ge1$. Tỉ số với cận một vòng ở $T=m=10^4$: $1{,}7321$†.)

   **Chứng minh** (khoảng 280 tiếng). Lộ trình: Mệnh đề 06.5(b), rồi chặn riêng hai số hạng, rồi chọn $\eta$. **Bước 1 (khoảng cách tổng quát hóa; Hệ quả 08.7).** $\mathbb E[L_D(\bar w_T)-L_S(\bar w_T)]\le\tfrac{\eta G^2(T-1)}m$; các kì vọng hữu hạn như Bước 4 của Định lý 08.6. **Bước 2 (sai số tối ưu; Định lý 05.14).** Với mỗi mẫu $s$, oracle rút đều thỏa (G1), (G2) với hằng số $G$ (Bước 1 chứng minh Hệ quả 05.19, dùng (G)), và $L_s$ lồi trên $W$ lồi (dùng (S)), tức (C); Định lý 05.14 với mọi $u\in W$ và $\lVert w_1-u\rVert\le R$ cho $\mathbb E_\xi\operatorname{opt}_s(\bar w_T)\le\tfrac{R^2}{2\eta T}+\tfrac{\eta G^2}2$; lấy kì vọng theo $S$. **Bước 3 (Mệnh đề 06.5(b)).** Cộng hai bước, được (a). **Bước 4 (chọn $\eta$).** Vế phải có dạng $a/\eta+b\eta$ với $a=\tfrac{R^2}{2T}$, $b=G^2\big(\tfrac12+\tfrac{T-1}m\big)$; cực tiểu tại $\eta^*=\sqrt{a/b}$, giá trị $2\sqrt{ab}$ (bất đẳng thức trung bình cộng–trung bình nhân); thay $T=m$ được $RG\sqrt{(3-2/m)/m}\le RG\sqrt{3/m}$. Câu sau $\square$: SGD chạy nhiều vòng có một cận rủi ro, nhưng theo các cận này, nó không tốt hơn một vòng qua dữ liệu với quan sát mới.
2. Một câu cảnh báo ngay sau (bắt buộc, nguyên tắc 7): ghép cận ổn định của điểm lặp cuối $w_{T+1}$ (Định lý 08.6) với Định lý 05.14 là sai, vì Định lý 05.14 chỉ chặn sai số tối ưu của $\bar w_T$ (Ví dụ 05.12: điểm lặp cuối có thể không hội tụ).
3. **Ví dụ 08.7 (Số vòng qua dữ liệu cho hồi quy logistic)** (trả lời khối ứng dụng; PTN §3(b); `c1_numbers.txt`). **Thiết lập.** Khối ứng dụng: $m=10^4$ (giả định), $G=1$, $\beta=\tfrac14$, $W$ quả cầu bán kính $5$, $w_1=0$, $R=5$. **Bước 1: một vòng** (Nhận xét 06.3): $5/\sqrt{10\,001}\le0{,}0500$. **Bước 2: nhiều vòng với $\eta^*$** (Hệ quả 08.8(b); $\eta^*\le0{,}029\le8$): $T=10^4$ (một vòng): $0{,}0866$; $T=2\cdot10^4$: $0{,}0791$; $T=10^5$: $0{,}0725$; giới hạn $5\sqrt{2\cdot10^{-4}}\le0{,}0708$†. **Bước 3: độ dài bước cố định $\eta=0{,}05$.** Hàm $T\mapsto\tfrac{R^2}{2\eta T}+\tfrac{\eta G^2(T-1)}m$ nhỏ nhất gần $T^*=\tfrac{R\sqrt{m/2}}{\eta G}\approx7071$; cận $\le0{,}0958$† tại $T=7071$; $0{,}1000$ tại $T=5000$ và $T=10^4$; $0{,}1375$† tại $T=2\cdot10^4$; $0{,}2800$ tại $T=5\cdot10^4$. **Bước 4: nhiều dữ liệu** (ứng dụng của Bài 05, $m=10^6$, $T=10^4$, $\eta=0{,}05$): sai số tối ưu $0{,}05$ cộng số hạng ổn định $\le0{,}0005$, tổng $\le0{,}0505$. **Kết luận.** Trả lời câu hỏi thực hành: theo các cận này, chạy nhiều vòng trên $10^4$ hồ sơ không cho cận nhỏ hơn một vòng ($0{,}0708$ so với $0{,}0500$); với $\eta=0{,}05$, cận nhỏ nhất ở khoảng $7071$ bước. Số bước $T^*$ làm nhỏ nhất tổng hai **cận trên**; nó không chứng minh lỗi kiểm tra nhỏ nhất ở đó. (Bước 4 là phần cắt thứ ba nếu vượt ngân sách.)
4. **Định nghĩa 08.9 (Dừng sớm, chính quy hóa tường minh và chính quy hóa ngầm)** (blueprint 8.4; PTN §4). Câu dẫn "Cho một thuật toán huấn luyện lặp, chẳng hạn Thuật toán 08.1, trên mẫu $s$." Danh sách nhãn:
   - **Dừng sớm.** Chọn số bước $T$ nhỏ hơn số bước cần để đưa sai số tối ưu thực nghiệm về gần $0$, trước khi chạy hoặc bằng một mẫu xác thực độc lập với $s$ (Bài 04); đầu ra là điểm lặp tại bước dừng (early stopping).
   - **Chính quy hóa tường minh.** Thêm một số hạng phạt vào hàm mục tiêu, như $\tfrac\lambda2\lVert w\rVert^2$ của Định nghĩa 06.6 (explicit regularization).
   - **Chính quy hóa ngầm.** Khi nhiều điểm của $W$ có rủi ro thực nghiệm nhỏ như nhau, các lựa chọn của quá trình huấn luyện (khởi tạo, độ dài bước, số bước, cách rút chỉ số) quyết định điểm nào được trả về, không qua một số hạng phạt (implicit regularization).

   Đoạn đọc sau (khoảng 150 tiếng): dòng thứ ba mô tả một hành vi chọn lựa, không phải một định lý. Hai trường hợp có chứng minh trong học phần: hạ gradient trên hàm lỗi bình phương, khởi tạo tại $0$, hội tụ tới nghiệm nội suy chuẩn nhỏ nhất (Phụ lục D của Bài 07); Định lý 08.6, trong đó ngân sách độ dài bước giới hạn tính ổn định như $1/\lambda$ trong Mệnh đề 06.11. **Ví dụ** (thí nghiệm mở đầu, số dự kiến): hàm lỗi logistic trên mẫu kiểm tra nhỏ nhất ở khoảng $5$–$10$ vòng ($0{,}589$; $0{,}603$), còn lỗi phân lớp trên mẫu kiểm tra gần như không đổi từ $5$ đến $100$ vòng ($0{,}309$; $0{,}301$; $0{,}312$), nên số bước tốt nhất phụ thuộc vào hàm lỗi dùng để chọn. **Không-ví dụ:** câu "chính quy hóa ngầm làm mạng sâu tổng quát hóa tốt" là một giả thuyết thực nghiệm; học phần không có định lý cho nó (§10).

**Câu kết §8:** số bước và độ dài bước đi vào cận rủi ro qua hai số hạng ngược chiều; chọn chúng để cực tiểu tổng là cực tiểu một cận trên, và mọi kết luận ở đây cần hàm lỗi lồi, trơn.

### `## 9. Khi bỏ tính lồi hoặc tính trơn` (khối "nonconvex limitations 25")

**Câu mở:** "Tính lồi, tính trơn và điều kiện $\eta_t\le2/\beta$ chỉ đi vào chứng minh qua Bổ đề 08.4, tức qua các bước chung. Mỗi ví dụ dưới đây bỏ một trong ba điều kiện và giữ các giả thiết còn lại." (Blueprint 8.4: hàm lỗi của mạng ReLU theo trọng số vừa không trơn vừa không lồi.)

1. **Ví dụ 08.8 (Bỏ tính lồi: hàm lỗi cosin)** (PTN (d1); `c1_numbers.txt`; blueprint bài 3). **Thiết lập.** $\mathcal Z=\mathbb R$, $W=\mathbb R$, $\ell(w,z)=1+\cos(w-z)\in[0,2]$; $m=100$, mọi $z_j=0$; quan sát thay thế $z'=0{,}01$ ở một chỉ số $i$; $w_1=0$; $\eta=0{,}1$; dãy chỉ số có $i_1=i$ và $i_t\ne i$ với mọi $t\ge2$ (một quỹ đạo tất định). **Bước 1: ba hằng số.** Đạo hàm $-\sin(w-z)$ có trị tuyệt đối $\le1$ nên (G) đúng với $G=1$; đạo hàm bậc hai $-\cos(w-z)\in[-1,1]$ nên hàm lỗi $1$-trơn; đạo hàm bậc hai âm gần $w=z$ nên hàm lỗi **không lồi**. **Bước 2: lần chạy trên $s$.** Đạo hàm tại $w=0$ với $z=0$ bằng $0$, nên $w_t=0$ với mọi $t$; $w=0$ là một điểm dừng, và là điểm cực đại của $L_s$ (giá trị $2$). **Bước 3: bước khác biệt.** $w'_2=-0{,}1\sin(0{,}01)\approx-0{,}0010$, nên $\Delta_2\approx0{,}0010\le2G\eta=0{,}2$. **Bước 4: các bước chung.** $w'_{t+1}=w'_t+0{,}1\sin w'_t$, nên khi $w'_t$ gần $0$, khoảng cách nhân khoảng $1+\beta\eta=1{,}1$ mỗi bước ($\Delta_3/\Delta_2=1{,}1000$†): $\Delta_{21}\approx0{,}0061$, $\Delta_{41}\approx0{,}0411$, $\Delta_{61}\approx0{,}2753$ ($\Delta_{58}\approx0{,}207$ là giá trị đầu tiên vượt $0{,}2$†), $\Delta_{81}\approx1{,}529$, $\Delta_{101}\approx2{,}879$, rồi $\Delta_t\to\pi$ ($w'_t\to-\pi$, điểm cực tiểu)†. **Bước 5: so với cận lồi.** Quỹ đạo chỉ có một bước khác biệt, nên phần (a) của Mệnh đề 08.5, nếu đúng, cho $\Delta_t\le0{,}2$ với mọi $t$. Tại quan sát kiểm tra $z=0$, hàm lỗi của hai đầu ra là $2$ và gần $0$, hiệu $2$, bằng độ rộng của miền giá trị. **Bước 6 (tùy chọn, phần cắt đầu tiên): kì vọng theo $\xi$** (Monte Carlo, $4000$ lần lặp, chỉ số đều): $\mathbb E\Delta_{101}\approx0{,}59$, $\mathbb E\Delta_{201}\approx2{,}20$, $\mathbb E\Delta_{401}\approx3{,}03$, so với $2G\eta t/m=0{,}2$; $0{,}4$; $0{,}8$. **Kết luận.** Bỏ tính lồi, các bước chung đẩy hai lần chạy ra xa, và hai lần chạy dừng ở hai điểm khác nhau ($0$ và $-\pi$); Bổ đề 08.4 là bước hỏng.
2. **Mệnh đề 08.10 (Bất đẳng thức truy hồi khi bỏ tính lồi) — phác thảo** (blueprint Nonconvex extension [S]; QĐ 5; PTN §2.6). **Giả thiết** (danh sách): như Mệnh đề 08.5, nhưng (S) thay bằng: với mọi $z$, $\ell(\cdot,z)$ là $\beta$-trơn trên $\mathbb R^p$ (không cần lồi); $\eta_t>0$ bất kì. **Bảo đảm**, danh sách:
   - **(a) Hệ số giãn.** Ánh xạ $\operatorname{proj}_W\circ\Gamma_{\eta,z}$ có hệ số giãn $1+\beta\eta$; hằng số này chặt (hàm $-\tfrac\beta2\lVert w\rVert^2$ với $W=\mathbb R^p$).
   - **(b) Trên từng quỹ đạo.** $\Delta_{t+1}\le(1+\beta\eta_t)\Delta_t+2G\eta_t\mathbb 1[i_t=i]$.
   - **(c) Theo kì vọng theo $\xi$.**
     $$\begin{aligned}\mathbb E\Delta_{T+1}&\le\frac{2G}m\sum_{t=1}^T\eta_t\prod_{s=t+1}^T(1+\beta\eta_s)\\&\le\frac{2G}m\sum_{t=1}^T\eta_t\,e^{\beta\sum_{s=t+1}^T\eta_s};\end{aligned}$$
     với độ dài bước hằng, vế phải thứ nhất bằng $\frac{2G}{m\beta}\big((1+\beta\eta)^T-1\big)$.

   **Chứng minh** (phác thảo, khoảng 150 tiếng). (a) Bất đẳng thức tam giác và tính trơn: $\lVert\Gamma(u)-\Gamma(v)\rVert\le\lVert u-v\rVert+\eta\lVert\nabla\ell(u,z)-\nabla\ell(v,z)\rVert\le(1+\beta\eta)\lVert u-v\rVert$; phép chiếu không giãn. (b) Như Bước 1–2 chứng minh Mệnh đề 08.5, với (a) thay Bổ đề 08.4. (c) Lấy kì vọng (tính tuyến tính), khai triển truy hồi từ $\Delta_1=0$, dùng $1+x\le e^x$; tổng hình học cho dạng bước hằng. Câu sau $\square$: thừa số $\prod_s(1+\beta\eta_s)$ thay cho $1$ là chỗ duy nhất tính lồi từng được dùng.
3. Đoạn sau mệnh đề (khoảng 120 tiếng; PTN §2.6): với $\beta=1$, $\eta=0{,}1$, $T=100$: $(1{,}1)^{100}\approx1{,}378\cdot10^4$†, nên với $m=100$ vế phải bằng $\tfrac2{100}\big((1{,}1)^{100}-1\big)\approx275{,}6$†, trong khi hàm lỗi cosin nhận giá trị trong $[0,2]$; với $\eta=0{,}05$, $T=1000$: $(1{,}05)^{1000}\approx1{,}5\cdot10^{21}$. Với $\eta_t=c/t$: $\prod_{s=t+1}^T(1+\beta c/s)\le e^{\beta c\sum_{s=t+1}^T1/s}\le(T/t)^{\beta c}$, tăng theo đa thức của $T$; đây là lý do các kết quả không lồi cần độ dài bước giảm. Công thức $\tfrac{2G^2}m\sum_t\eta_t$ của trường hợp lồi không được dùng lại.
4. **Nhận xét 08.11 (Cận ổn định cho hàm lỗi không lồi bị chặn) — đọc thêm** (QĐ 5; HRS Thm 3.12 tr. 12–14, Lemma 3.11 tr. 12; PTN §1, §2.6; khoảng 160 tiếng). Phát biểu theo kí hiệu học phần, dẫn nguồn đầy đủ (Hardt, Recht, Singer 2016, Định lý 3.12): nếu với mọi $z$, $\ell(\cdot,z)$ nhận giá trị trong $[0,1]$, là $G$-Lipschitz và $\beta$-trơn, SGD không chiếu chạy $T$ bước với $\eta_t$ không tăng và $\eta_t\le c/t$, chỉ số đều có hoàn lại (hoặc hoán vị ngẫu nhiên), thì
   $$\epsilon_{\mathrm{stab}}(m)\le\frac{1+1/(\beta c)}{m-1}\,(2cG^2)^{\frac1{\beta c+1}}\,T^{\frac{\beta c}{\beta c+1}} .$$
   Ba giả thiết thêm so với Định lý 08.6: hàm lỗi bị chặn, độ dài bước giảm như $c/t$, và lập luận về giai đoạn đầu khi quan sát khác biệt chưa được dùng (xác suất không quá $t_0/m$ trước bước $t_0$; burn-in). Số: $\beta=10$, $c=1$, $G=1$, $m=10^4$, $T=10^6$: $\le33{,}37$†, lớn hơn $1$ nên không cho thông tin với hàm lỗi trong $[0,1]$; $\beta=1$, $c=0{,}1$: $\le0{,}0009$, với bước rất nhỏ. Không chứng minh; chỉ ở mục Tài liệu đọc thêm.
5. **Ví dụ 08.9 (Độ dài bước vượt $2/\beta$)** (thay PTN (d2) bằng bản Huber để chỉ bỏ một điều kiện; `c2_ex.txt`†). **Thiết lập.** Hàm lỗi Huber của Ví dụ 08.1 ($\beta=G=1$, lồi), mẫu $s=(0,0,0,\tfrac1{100})$, $s^{(4)}=(0,0,0,-\tfrac1{100})$, $w_1=0$, dãy chỉ số $i_1=4$ rồi $i_t=1$ với $t\ge2$. **Bước 1: $\eta=1$.** $\Delta_2=0{,}02$, rồi $\Delta_t=0$ từ $t=3$ (bước chung đưa cả hai về $0$). **Bước 2: $\eta=2=2/\beta$.** $w_t$ đổi dấu ($\pm\tfrac1{50}$), $\Delta_t=0{,}04$ không đổi. **Bước 3: $\eta=3$.** Khi $\lvert w\rvert\le1$, bước chung là $w\mapsto-2w$, nên $\Delta_2,\ldots,\Delta_8=0{,}06;\,0{,}12;\,0{,}24;\,0{,}48;\,0{,}96;\,1{,}92;\,3{,}84$; sau đó điểm lặp ra khỏi vùng bậc hai. **Kết luận.** Mọi giả thiết khác của Mệnh đề 08.5 vẫn đúng; chỉ điều kiện $\eta\le2/\beta$ bị bỏ, và các bước chung nhân khoảng cách với $\lvert1-\eta\beta\rvert=2$, đúng hệ số giãn của Ví dụ 08.3.
6. **Ví dụ 08.10 (Hàm lỗi không trơn và mạng ReLU)** (PTN (d4); blueprint 8.4, bài 5). **Bước 1: giá trị tuyệt đối.** $\ell(w,z)=\lvert w-z\rvert$ (lồi, $1$-Lipschitz, không khả vi tại $w=z$; mọi cách chọn dưới gradient): hai điểm $\pm0{,}01$, một bước chung với $z=0$, $\eta=\tfrac12$: $0{,}01\mapsto-0{,}49$, $-0{,}01\mapsto0{,}49$, khoảng cách từ $0{,}02$ thành $0{,}98$. Mỗi bước chung có thể tăng khoảng cách tới $2G\eta$, nên thừa số $1/m$ mất. **Bước 2: hàm lỗi bản lề** (phần cắt thứ hai): $x=1$, $\tilde y=1$, $w=0{,}99$, $w'=1{,}01$, $\eta=\tfrac12$: khoảng cách từ $0{,}02$ thành $0{,}48$†. **Bước 3: mạng ReLU** (Định nghĩa 07.1, mọi trọng số được huấn luyện; ba ý, mỗi ý một dòng): (i) hàm lỗi không khả vi theo $\theta$ tại các tham số có một tiền kích hoạt bằng $0$, nên không $\beta$-trơn; (ii) không lồi theo $\theta$: đổi chỗ hai nơ-ron ẩn cho cùng hàm, và trung điểm của hai tham số có thể tệ hơn (Bài tập 07.5(c)); (iii) gradient theo $\Theta_1$ tỉ lệ với độ lớn của $\Theta_2$ và ngược lại, nên không có $G$ đều trên $\mathbb R^P$ khi trọng số không bị chặn. **Kết luận.** Áp dụng Định lý 08.6 nguyên văn cho mạng ReLU huấn luyện mọi lớp nơ-ron là sai. Trường hợp riêng chặt chẽ: lớp ẩn cố định, chỉ lớp ra được huấn luyện bằng SGD trên hàm lỗi logistic (mạng đặc trưng ngẫu nhiên của Bài 07); khi đó hàm lỗi lồi, trơn theo trọng số lớp ra, với $G=\sup_x\lVert\chi(x)\rVert$, $\beta=G^2/4$, và định lý áp dụng. Một câu: hàm lỗi bình phương không có $G$ hữu hạn trên $\mathbb R^p$ (Ví dụ 06.9 cho hiện tượng tương tự ở ERM có chính quy hóa).
7. **Mệnh đề 08.12 (Điểm dừng xấp xỉ của SGD trên hàm mục tiêu trơn) — đọc thêm (chứng minh ở Phụ lục C)** (blueprint Optional optimization appendix [O]; QĐ 6; PTN §2.7). Câu dẫn: "Không có tính lồi, SGD vẫn có một bảo đảm tối ưu, nhưng cho một đại lượng yếu hơn sai số tối ưu." **Giả thiết** (danh sách): **Hàm mục tiêu.** $F:\mathbb R^p\to\mathbb R$ $\beta$-trơn, $F_*=\inf F>-\infty$, không cần lồi. **Gradient ngẫu nhiên.** $\mathbb E[g_t\mid\mathcal F_{t-1}]=\nabla F(w_t)$ và $\mathbb E[\lVert g_t-\nabla F(w_t)\rVert^2\mid\mathcal F_{t-1}]\le\sigma^2$ ($\sigma^2$ như Mệnh đề 05.20; $\mathcal F_t$ như Định nghĩa 05.10). **Thuật toán.** $w_{t+1}=w_t-\eta g_t$, $W=\mathbb R^p$, $w_1$ tất định, $0<\eta\le1/\beta$. **Bảo đảm** (theo kì vọng theo $\xi$):
   $$\begin{aligned}&\frac1T\sum_{t=1}^T\mathbb E\lVert\nabla F(w_t)\rVert^2\\&\le\frac{2(F(w_1)-F_*)}{\eta T}+\beta\eta\sigma^2 .\end{aligned}$$
   Dòng diễn giải: vế trái bằng $\mathbb E\lVert\nabla F(w_\tau)\rVert^2$ với $\tau$ rút đều trên $\{1,\ldots,T\}$, độc lập; mệnh đề chặn **tính dừng** (gradient nhỏ), không chặn sai số tối ưu, rủi ro vượt mức hay khoảng cách tổng quát hóa; không nói về $w_{T+1}$. Đoạn ngắn sau (khoảng 100 tiếng): (i) hồi quy logistic với $F=L_s$, $\beta=\tfrac14$, $\sigma^2\le1$ (vì $\mathbb E\lVert g-\nabla F\rVert^2\le\mathbb E\lVert g\rVert^2\le G^2$), $F(w_1)-F_*\le\ln2$ khi $w_1=0$: với $\eta=0{,}05$, $T=10^4$, vế phải $\le0{,}0153$; (ii) trong Ví dụ 08.8, $w=0$ là điểm dừng với $L_s=2$, giá trị lớn nhất: gradient nhỏ không kéo theo rủi ro thực nghiệm nhỏ khi hàm không lồi.

**Câu kết §9:** khi bỏ tính lồi, cận ổn định tăng theo tích các hệ số giãn và tối ưu chỉ còn bảo đảm tính dừng; với mạng ReLU huấn luyện mọi lớp nơ-ron, các giả thiết của Định lý 08.6 không thỏa.

### `## 10. Ý nghĩa, tác động và giới hạn`, `## 11. Bài tập`, `## 12. Câu hỏi cuối buổi và cầu nối`, `## 13. Tài liệu đọc`

Nội dung ở mục 4–7 dưới. Bốn mục này nhìn lại, nên được dẫn mọi số khối.

### `## Phụ lục`

Nội dung ở mục 8.

## 4. Kế hoạch bài tập (`exercises.md`, viết sau khi ghi chú qua rà soát)

Danh sách ở §11 của ghi chú: một dòng mỗi bài (tên, mục tiêu đo), như Bài 07. Đề, gợi ý tăng dần (mỗi gợi ý một khối `hint`), lời giải đầy đủ theo `van-phong.md` §7a trong `exercises.md`. **Không có bài UML** (QĐ 9; PTN §5): chương 13–14 đã dùng ở Bài 05–06 (13.1–13.4, 14.1, 14.3, 14.4), Bài tập 14.2 thuộc mạch quan sát mới của Bài 06 và cần bổ đề tự chặn chưa có; §20.9 không có bài về SGD hay tính ổn định (20.1, 20.3, 20.4 đã dùng ở Bài 07); Ch. 31 là một hướng khác. Ghi lý do này một câu ở §11 và một câu ở §13 của ghi chú. Mức: KN khái niệm, TT tính toán, CM chứng minh, GT kiểm tra giả thiết, TN thực nghiệm tùy chọn. Tổng 8 bài: 6 bài gốc blueprint 8.5 và 2 bài gốc thêm (QĐ 9). Số trong ngoặc là số dự kiến (`c1_numbers.txt`, `c2_ex.txt`, `exp_p100_eta05.txt`, `exp_p100_eta025.txt`).

**Bài gốc (blueprint 8.5).**

1. **Bài tập 08.1 (Bất đẳng thức truy hồi và thừa số $1/m$)** — mục tiêu 1, 3; CM+TT; vừa. Blueprint bài 1. (a) Viết đầy đủ chứng minh Mệnh đề 08.5(a), ghi giả thiết dùng ở mỗi dòng. (b) Chứng minh $\mathbb E\sum_{t=1}^T\eta_t\mathbb 1[i_t=i]=\tfrac1m\sum_t\eta_t$ và suy ra (b); chỉ ra rằng thừa số $1/m$ chỉ đến từ $\Pr(i_t=i)$. (c) Xáo trộn lại sau mỗi vòng qua dữ liệu với $m$ chia hết $T$: chứng minh $\Pr(i_t=i)=1/m$ và (b) vẫn đúng, dù các $i_t$ không độc lập. (d) Ví dụ Huber ($m=4$, $\eta=\tfrac12$): kiểm $\mathbb E\Delta_2=\tfrac14$ (dấu bằng) và $\mathbb E\Delta_3=\tfrac{29}{64}<\tfrac12$; chỉ ra bước chung nào làm bất đẳng thức chặt ngặt. Kết quả mong đợi: thừa số $1/m$ là xác suất biên, không cần tính độc lập giữa $i_t$ và $\Delta_t$. Liên hệ: Mệnh đề 08.5, Ví dụ 08.4, Phụ lục B.
2. **Bài tập 08.2 (Ngân sách độ dài bước của ba lịch độ dài bước)** — mục tiêu 3, 4; TT+CM; dễ–vừa. Blueprint bài 2. (a) Chứng minh $\ln(T+1)\le\sum_{t=1}^T\tfrac1t\le1+\ln T$ và $\sum_{t=1}^Tt^{-1/2}\le2\sqrt T-1$ bằng so sánh với tích phân. (b) So ngân sách của $\eta_t=0{,}05$, $\eta_t=5/t$, $\eta_t=5/\sqrt t$ với $T=10^4$: $500$; $48{,}94$ (vì $\sum1/t\approx9{,}7876$)†; $992{,}72$†; cận của Định lý 08.6 cho hồi quy logistic ($G=1$, $m=10^4$; điều kiện $\eta_t\le8$ thỏa): $0{,}1000$; $0{,}0098$†; $0{,}1986$†. (c) Với Nhận xét 05.17 ($R=5$, $G=1$; đầu ra là trung bình có trọng số $\tilde w_T$), cận tối ưu của ba lịch ở $T=10^4$: $0{,}0500$; $0{,}6756$†; $0{,}1359$†; ở $T=10^5$: $0{,}0275$; $0{,}5470$†; $0{,}0519$† (cận trên, làm tròn lên; `c3_more.txt`). Giải thích vì sao lịch $1/t$ có cận ổn định nhỏ nhưng cận tối ưu chỉ giảm như $1/\ln T$. Lưu ý trong đề: không cộng hai cận ở (b) và (c), vì chúng nói về hai đầu ra khác nhau ($w_{T+1}$ và $\tilde w_T$). Kết quả mong đợi: ngân sách nhỏ giữ số hạng ổn định nhỏ và làm số hạng tối ưu giảm chậm. Liên hệ: Định lý 08.6, Nhận xét 05.17, Hệ quả 08.8.
3. **Bài tập 08.3 (Bước chứng minh không còn đúng khi bỏ tính lồi)** — mục tiêu 2, 5; CM+GT; vừa. Blueprint bài 3. (a) Trong chứng minh tính đồng bức (Phụ lục A), chỉ ra đúng dòng dùng tính lồi (hàm phụ $q_u$ đạt cực tiểu toàn cục tại $u$ vì $\nabla q_u(u)=0$) và cho một hàm $\beta$-trơn không lồi mà dòng đó sai ($-\tfrac12w^2$). (b) Suy ra bước nào của Mệnh đề 08.5 hỏng (Bước 1, bước chung) và bước nào còn đúng (Bước 2, nhờ (G)). (c) Ví dụ 08.8: kiểm $\Delta_3/\Delta_2=1{,}1$ và giải thích bằng đạo hàm $1+\eta\cos w$ của ánh xạ bước tại $w$ gần $0$. (d) Dùng Mệnh đề 08.10 với $\beta=1$, $\eta=0{,}1$, $m=100$, $T=100$: vế phải $\approx275{,}6$†; so với miền giá trị $[0,2]$ của hàm lỗi. Kết quả mong đợi: tính lồi chỉ đi vào qua tính đồng bức; không có nó, mỗi bước chung có thể nhân khoảng cách với $1+\beta\eta$. Liên hệ: Bổ đề 08.4, Phụ lục A, Ví dụ 08.3, 08.8, Mệnh đề 08.10.
4. **Bài tập 08.4 (Gradient nhỏ, rủi ro thực nghiệm nhỏ và rủi ro kì vọng nhỏ)** — mục tiêu 5; KN+TT; vừa. Blueprint bài 4. (a) Ví dụ 08.8: $w=0$ có $\nabla L_s(0)=0$ và $L_s(0)=2$ là giá trị lớn nhất. (b) Với $L_s$ lồi, khả vi trên $\mathbb R^p$ và $W$ bị chặn: chứng minh $\operatorname{opt}_s(w)\le\lVert\nabla L_s(w)\rVert\operatorname{diam}(W)$ với mọi $w\in W$ (bất đẳng thức dưới gradient tại $w$ và Cauchy–Schwarz), nên với hàm lồi gradient nhỏ kéo theo sai số tối ưu nhỏ. (c) Thí nghiệm mở đầu sau $100$ vòng: $\lVert\nabla L_S(w)\rVert\approx0{,}004$†, $L_S\approx0{,}135$, ước lượng $L_D\approx1{,}053$: rủi ro thực nghiệm nhỏ không kéo theo rủi ro kì vọng nhỏ. (d) Mệnh đề 08.12 cho hồi quy logistic ($\eta=0{,}05$, $T=10^4$): $0{,}0153$; với $\eta=4=1/\beta$: $1{,}0001$† (độ dài bước lớn làm số hạng $\beta\eta\sigma^2$ chiếm ưu thế). Kết quả mong đợi: ba đại lượng (tính dừng, sai số tối ưu, rủi ro kì vọng) cần ba loại bảo đảm khác nhau; chỉ với hàm lồi, gradient nhỏ chặn sai số tối ưu. Liên hệ: Mệnh đề 08.12, Ví dụ 08.8, Hệ quả 08.8.
5. **Bài tập 08.5 (Kiểm tra giả thiết cho một thiết lập huấn luyện mạng ReLU)** — mục tiêu 5; GT+KN; vừa. Blueprint bài 5. Thiết lập cho trong đề: mạng ReLU hai lớp nơ-ron $f_\theta(x)=\Theta_2\operatorname{ReLU}(\Theta_1x)$, hàm lỗi logistic, $\lVert x\rVert\le1$, SGD không chiếu, $\eta=0{,}1$, $T=10^5$, $m=5\cdot10^4$; một báo cáo khẳng định "Định lý 08.6 cho khoảng cách tổng quát hóa kì vọng không quá $2\cdot1^2\cdot0{,}1\cdot10^5/(5\cdot10^4)=0{,}4$". (a) Với một nơ-ron, $x=1$, $\tilde y=1$, $\ell(\theta)=\ln(1+e^{-\operatorname{ReLU}(\theta)})$: tính đạo hàm trái ($0$) và phải ($-\tfrac12$) tại $0$; kết luận không khả vi, không $\beta$-trơn; và $\ell(0)=\ln2\approx0{,}6931>\tfrac12(\ell(-1)+\ell(1))\approx0{,}5032$†, nên không lồi. (b) Mạng hai lớp: gradient theo $\Theta_1$ chứa $\Theta_2$, nên không có $G$ đều. (c) Liệt kê từng giả thiết của Định lý 08.6: (T1) ✓, (T2) ✓, (S) ✗, (G) ✗, $\eta\le2/\beta$ không xác định. (d) Hai cách sửa và cái giá: cố định lớp ẩn, chỉ huấn luyện lớp ra (định lý áp dụng với $G=\sup\lVert\operatorname{ReLU}(\Theta_1x)\rVert$); thay ReLU bằng hàm kích hoạt trơn và chiếu lên $W$ bị chặn (trơn trên $W$ nhưng không lồi, chỉ còn Mệnh đề 08.10). Kết quả mong đợi: con số $0{,}4$ không có căn cứ; kết luận đúng chỉ cho trường hợp riêng. Liên hệ: Ví dụ 08.10, Mệnh đề 08.10, Bài tập 07.5.
6. **Bài tập 08.6 (Thực nghiệm tùy chọn: hai lần chạy ghép cặp theo thời gian)** — mục tiêu 5; TN; vừa. Blueprint bài 6. Chỉ mô tả giao thức (Phụ lục D), không notebook. Yêu cầu: với $\eta\in\{0{,}25;0{,}5\}$, báo theo số vòng $\{0{,}5;1;5;10;20;50;100\}$: $\Delta$ ghép cặp, tỉ lệ đổi nhãn, lỗi phân lớp kiểm tra, khoảng cách tổng quát hóa ước lượng và cận $2G^2\eta t/m$; không đồng nhất đường cong nào với cận. Số dự kiến (bản nháp, 20 hạt giống): với $\eta=0{,}25$, khoảng cách $0{,}025$; $0{,}046$; $0{,}147$; $0{,}212$; $0{,}299$; $0{,}461$; $0{,}651$†, $\Delta$ ghép cặp $0{,}073$; $0{,}124$; $0{,}523$; $0{,}931$; $1{,}447$; $2{,}531$; $3{,}745$†; với cùng ngân sách $\eta t$, hai độ dài bước cho khoảng cách gần nhau: $\eta t=500$: $0{,}212$ và $0{,}213$; $\eta t=1000$: $0{,}299$ và $0{,}298$; $\eta t=5000$: $0{,}651$ và $0{,}650$† ($\eta=0{,}25$ so với $\eta=0{,}5$). Kết quả mong đợi: trong thí nghiệm này, khoảng cách đo được gần như chỉ phụ thuộc ngân sách $\eta t$, cùng biến mà cận dùng, nhưng tăng chậm hơn tuyến tính; quan sát này là bằng chứng cho một thiết lập, không phải định lý (blueprint §E). Liên hệ: Ví dụ 08.6, Định nghĩa 08.9.

**Bài gốc thêm** (QĐ 9, gắn với khối của ghi chú).

7. **Bài tập 08.7 (SGD có chiếu nhiều vòng cho hồi quy bình phương)** — mục tiêu 3; GT+TT; dễ–vừa. Lời hứa Bài 06 (§5, §10). (a) Với hàm lỗi $(wx-y)^2$, $\lvert x\rvert\le1$, $\lvert y\rvert\le1$, $W=[-1,1]$: kiểm (S) trên $\mathbb R$ với $\beta=2$, (G) trên $W$ với $G=4$, và giải thích vì sao (G) sai trên $\mathbb R$. (b) Chương trình thứ hai của câu hỏi mở đầu Bài 06 ($m=4$, $\eta=0{,}00625$, $T=1600$, đầu ra $\bar w_T$): kiểm $\eta\le2/\beta=1$, tính cận của Hệ quả 08.7: $39{,}975$, ghi $\le39{,}98$; cận của Định lý 08.6 cho điểm lặp cuối: $80$. (c) So với khoảng cách tổng quát hóa kì vọng thật $0{,}4750$ (Ví dụ 06.3) và giải thích vì sao cận đúng nhưng không cho thông tin ($\eta T/m=2{,}5$, tức $400$ vòng). Kết quả mong đợi: lời hứa của Bài 06 được giữ ở dạng đúng; cận có ích khi $\eta T\ll m$. Liên hệ: Hệ quả 08.7, Định lý 08.6, Ví dụ 06.3.
8. **Bài tập 08.8 (Số bước tốt nhất với độ dài bước cố định)** — mục tiêu 4; CM+TT; vừa. (a) Với $\eta$ cố định, tìm $T^*$ làm nhỏ nhất vế phải của Hệ quả 08.8(a) theo $T$ liên tục: $T^*=\tfrac{R\sqrt{m/2}}{\eta G}$, giá trị $RG\sqrt{2/m}+\tfrac{\eta G^2}2-\tfrac{\eta G^2}m$. (b) Số cho ứng dụng $m=10^4$, $R=5$, $G=1$, $\eta=0{,}05$: $T^*\approx7071$, cận $\le0{,}0958$†. (c) Một bạn ghép cận ổn định của điểm lặp cuối $2G^2\eta T/m$ với cận tối ưu của Định lý 05.14 để được một cận cho $L_D(w_{T+1})$; chỉ ra bước sai (Định lý 05.14 nói về $\bar w_T$; Ví dụ 05.12). (d) Giải thích vì sao $T^*$ không chứng minh rằng lỗi kiểm tra nhỏ nhất ở $T^*$; dùng bảng của câu hỏi mở đầu (hàm lỗi logistic kiểm tra nhỏ nhất ở khoảng $5$ vòng, lỗi phân lớp gần như không đổi). Kết quả mong đợi: đánh đổi giữa hai cận trên, không phải giữa hai đại lượng thật. Liên hệ: Hệ quả 08.8, Ví dụ 08.7, Định nghĩa 08.9.

Mục tiêu được đo: 1 (08.1); 2 (08.3); 3 (08.1, 08.2, 08.7); 4 (08.2, 08.8); 5 (08.3, 08.4, 08.5, 08.6).

## 5. Ý nghĩa, tác động và giới hạn (§10 của ghi chú)

Thứ tự đoạn, mỗi đoạn kết bằng một đại lượng cụ thể (`van-phong.md` §8); khoảng 480 tiếng. Câu mở trả lời thẳng câu hỏi trung tâm (bài học Bài 06 R5 T4), không câu siêu ngôn ngữ.

1. **Câu trả lời cho câu hỏi trung tâm và câu hỏi mở đầu.** Với hàm lỗi lồi, trơn, có gradient bị chặn, thuật toán ảnh hưởng tới khoảng cách tổng quát hóa qua ngân sách độ dài bước: hệ số ổn định $\tfrac{2G^2}m\sum_t\eta_t$ (Định lý 08.6). Trong thí nghiệm mở đầu, cận là $t/200$ và khoảng cách đo được tăng từ $0{,}045$ lên $0{,}919$ (Ví dụ 08.6).
2. **Cấp thuật toán và cấp lớp.** Hệ quả 07.16 đúng với xác suất ít nhất $1-\delta$ cho mọi hàm của một lớp chọn trước mẫu, không cần tính lồi; Định lý 08.6 đúng theo kì vọng cho một thuật toán, cần tính lồi và tính trơn, nhưng không cần $W$ bị chặn và không phụ thuộc $p$. Một bảo đảm không thay được bảo đảm kia.
3. **Quyết định thực hành.** Độ dài bước và số bước đi vào cận qua cùng một tổng; điểm lặp trung bình giảm số hạng ổn định khoảng một nửa (Hệ quả 08.7); với $10^4$ hồ sơ, các cận không ủng hộ nhiều vòng hơn một vòng ($0{,}0708$ so với $0{,}0500$, Ví dụ 08.7); dừng sớm cực tiểu một tổng hai cận trên (Định nghĩa 08.9, Hệ quả 08.8).
4. **Ba mức khẳng định** (blueprint 8.4; danh sách nhãn): **Chứng minh được.** Định lý 08.6, Hệ quả 08.7, 08.8 cho hàm lỗi lồi, trơn, gồm hồi quy logistic và lớp ra của mạng với lớp ẩn cố định. **Lý thuyết không lồi bổ sung.** Mệnh đề 08.10 (tăng theo hàm mũ với bước hằng), Nhận xét 08.11 (cần hàm lỗi bị chặn, $\eta_t\le c/t$), Mệnh đề 08.12 (chỉ tính dừng). **Giả thuyết thực nghiệm.** HRS §6 đo khoảng cách tham số và khoảng cách tổng quát hóa của mạng sâu và thấy chúng tăng theo thời gian huấn luyện; câu "huấn luyện nhanh hơn thì tổng quát hóa tốt hơn" (tiêu đề của HRS) là cách đọc các cận trên, không phải định lý cho mạng sâu; chính quy hóa ngầm trong mạng sâu là giả thuyết (PTN §1 dòng 8.4).
5. **Giới hạn** (danh sách nhãn, như Bài 06–07): **Theo kì vọng.** Không có cận với xác suất cao; không chặn $\mathbb E\lvert L_D-L_S\rvert$. **Cận trên.** Lớn hơn khoảng cách đo được từ khoảng $11$ đến khoảng $109$ lần trong thí nghiệm (Ví dụ 08.6). **Tính trơn và tính lồi.** Hàm lỗi bản lề, mạng ReLU (Ví dụ 08.10). **Cận gradient đều.** Hàm lỗi bình phương cần $W$ bị chặn và dữ liệu bị chặn (Bài tập 08.7). **Không chặn $L_D$.** Cần thêm số hạng tối ưu, chỉ có cho điểm lặp trung bình (Hệ quả 08.8).

## 6. Câu hỏi cuối buổi và cầu nối

**Câu hỏi** (chẩn đoán ngắn, tính được; trọng tâm Recitation 4 "coupled SGD; neural-network assumption audit" và Exam 4 "Identify missing assumptions and distinguish theorem from experiment"; viết đúng như sau, có thể sửa chữ nhỏ; đã qua `no-ai-slop` Edit):

> Hồi quy logistic với $\lVert x\rVert\le1$ trên toàn $\mathcal X$, $W=\mathbb R^p$ và $m=5000$ quan sát độc lập cùng phân bố. SGD theo Thuật toán 08.1 chạy $T=20\,000$ bước (bốn vòng qua dữ liệu) từ $w_1=0$.
>
> (a) Với $\eta_t=0{,}1$ cho mọi $t$, tính cận của Định lý 08.6 cho khoảng cách tổng quát hóa kì vọng của điểm lặp cuối.
>
> (b) Với $\eta_t=0{,}1/\sqrt t$, dùng $\sum_{t=1}^Tt^{-1/2}\le2\sqrt T-1$ để tính lại cận.
>
> (c) Cận ở (a) có chặn hiệu giữa tỉ lệ lỗi phân lớp trên mẫu kiểm tra và trên mẫu huấn luyện không?
>
> (d) Thay hàm lỗi logistic bằng hàm lỗi bản lề, hoặc thay mô hình tuyến tính bằng một mạng ReLU hai lớp nơ-ron với mọi trọng số được huấn luyện. Cận ở (a) còn có căn cứ không? Chỉ ra giả thiết không thỏa.

*Lời giải (khối `solution`, từng bước theo §7a).* **(a)** Hằng số: $G=1$, $\beta=\tfrac14$ (Ví dụ 08.5); $\eta_t=0{,}1\le8$. Cận $\tfrac{2\cdot1\cdot0{,}1\cdot20\,000}{5000}=0{,}8$. **(b)** $\sum_t\eta_t\le0{,}1(2\sqrt{20\,000}-1)\le28{,}19$† (giá trị $28{,}184$; tổng thật $28{,}139$†); cận $\le\tfrac{2\cdot28{,}19}{5000}\le0{,}0113$†; $\eta_t\le0{,}1\le8$. **(c)** Không: định lý chặn khoảng cách tổng quát hóa kì vọng của hàm lỗi logistic, theo kì vọng theo $(S,\xi)$; hàm lỗi 0–1 không Lipschitz theo $w$, và không có cận với xác suất cao. **(d)** Hàm lỗi bản lề không khả vi tại lề $1$, nên không thỏa (S); một bước chung có thể tăng khoảng cách (Ví dụ 08.10, Bước 2). Mạng ReLU huấn luyện mọi lớp nơ-ron không thỏa (S) (không trơn, không lồi) và không có $G$ đều (Ví dụ 08.10, Bước 3). Định lý không áp dụng, nên con số $0{,}8$ không có căn cứ; điều đó không có nghĩa khoảng cách thật lớn.

**Cầu nối sang Bài 09** (một đoạn; blueprint 8.6 bridge "The same risk language can describe probability models. What changes when an example is a sequence or the loss is log-likelihood?"; **không phát biểu kết quả của Bài 09**): Hàm lỗi logistic là $-\ln$ của xác suất mà mô hình gán cho nhãn quan sát được, tức hàm lỗi log của một mô hình xác suất có điều kiện (Nhận xét 02.11 nhắc hàm lỗi log). Các kết quả của bài dùng mỗi quan sát là một cặp $(x,y)$, các quan sát độc lập, và hàm lỗi lồi, trơn, có gradient bị chặn theo tham số. Câu hỏi cho Bài 09: khi mỗi quan sát là một chuỗi mà các phần tử phụ thuộc nhau, và hàm lỗi là $-\ln$ độ hợp lý của cả chuỗi, rủi ro kì vọng, rủi ro thực nghiệm và giả thiết độc lập được viết lại như thế nào? (Không khẳng định gì về tính lồi hay Lipschitz của mô hình chuỗi.)

## 7. Tài liệu đọc (theo mục UML và mục HRS; trang là trang PDF, chỉ ghi trong dàn ý)

- **Trước buổi học:** UML Ch. 13, §13.1–13.2 (ERM có chính quy hóa, quy tắc ổn định không quá khớp; tr. 171–175) làm nền, đã dùng ở Bài 06; UML §20.6 (SGD và lan truyền ngược cho mạng nơ-ron; tr. 277–278) làm nền về thuật toán thực tế. Một câu: §20.6 dùng quan sát mới ở mỗi bước và không có định lý ổn định.
- **Sau buổi học:** Hardt, Recht, Singer (2016), *Train faster, generalize better: Stability of stochastic gradient descent*, ICML — §2 (định nghĩa ổn định, quy tắc cập nhật; tr. 4–6), §3.1–3.3 (lập luận trơn–lồi, Định lý 3.8; tr. 6–9), Phụ lục A (tính đồng bức; tr. 31); phần thảo luận chọn lọc §1 (tr. 1–3) và §5 (so sánh với cận một vòng; tr. 17–19).
- **Mở rộng:** HRS §3.5 (phân tích không lồi, Định lý 3.12; tr. 12–14), §4 (suy giảm trọng số, cắt gradient, dropout; tr. 14–17), §6–§7 (thí nghiệm trên mạng sâu, câu hỏi mở; tr. 19–28, là quan sát thực nghiệm của bài báo); Mệnh đề 08.12 và Phụ lục C (tính dừng); UML Ch. 31, §31.1 (cận PAC-Bayes; tr. 415–417), một hướng khác để chặn khoảng cách tổng quát hóa, không thuộc các chứng minh bắt buộc của bài.

**Quan hệ với nguồn** (danh sách; câu mở: "Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục, bài báo của Hardt, Recht và Singer được dẫn theo mục và số định lý của bài báo." Chỉ khác biệt thật, nói trung tính):

- **Kí hiệu và chỉ số.** Bài báo viết $n$, $L$, $\alpha_t$, $\delta_t$ cho cỡ mẫu, hằng số Lipschitz, độ dài bước và khoảng cách giữa hai lần chạy; học phần viết $m$, $G$, $\eta_t$, $\Delta_t$, vì $L$ là rủi ro và $\delta$ là xác suất thất bại. Học phần đánh số điểm lặp từ $w_1$ như Bài 05, nên $T$ bước cho điểm lặp cuối $w_{T+1}$ và tổng $\sum_{t=1}^T\eta_t$.
- **Phép chiếu.** Định lý 3.8 của bài báo xét SGD không chiếu; học phần thêm phép chiếu lên $W$ đóng, lồi, nhờ tính không giãn của phép chiếu, để dùng cùng thuật toán với Bài 05–06.
- **Lập luận truy hồi.** Bài báo chia hai trường hợp theo việc quan sát được chọn có phải quan sát khác biệt không, rồi dùng tính tuyến tính của kì vọng; học phần viết bất đẳng thức trên từng quỹ đạo trước (Mệnh đề 08.5(a)), nên chỉ cần $\Pr(i_t=i)=1/m$, và kết quả cũng đúng khi xáo trộn lại sau mỗi vòng.
- **Tính đồng bức.** Bài báo phát biểu và dẫn tài liệu tối ưu; học phần chứng minh ở Phụ lục A.
- **Ghép với sai số tối ưu.** §5 của bài báo dùng cận ổn định cho điểm lặp trung bình và so với kì vọng của cực tiểu rủi ro thực nghiệm; Hệ quả 08.8 so với $\inf_WL_D$ qua Mệnh đề 06.5, với cận ổn định $G^2\eta(T-1)/m$ của Hệ quả 08.7 theo cách đếm của Bài 05; hai cách cho cùng kết luận: thua cận một vòng khoảng $\sqrt3$ lần khi $T=m$ và khoảng $\sqrt2$ lần khi $T\to\infty$.
- **Bài tập.** Không có bài UML: các bài phù hợp của chương 12–14 đã dùng ở Bài 05–06, và §20.9 không có bài về SGD hay tính ổn định.

Ghi chú cho người viết (không đưa vào ghi chú): PTN §1 ghi lệch một chỉ số trong Lemma 2.5 và trong khai triển (3.4) của HRS, và Thm 4.7 phát biểu $\alpha TL^2/n$ trong khi chứng minh cho $\alpha(T+1)L^2/n$; ghi chú **không** nêu các điểm này như lỗi của bài báo, chỉ dùng cách đánh số của học phần (QĐ 1: "trung tính").

## 8. Phụ lục (≤ 3 000 tiếng; dự kiến khoảng 2 500)

- **A. Tính đồng bức và tính không giãn** (khoảng 750 tiếng; QĐ 4). `::: proof Chứng minh Bổ đề 08.4(a)`. Lộ trình: cận trên bậc hai của hàm trơn, một hàm phụ đạt cực tiểu toàn cục, rồi đổi vai hai điểm. **Bước 1 (cận trên bậc hai; tính trơn).** Với $f$ $\beta$-trơn, $f(v)\le f(u)+\langle\nabla f(u),v-u\rangle+\tfrac\beta2\lVert v-u\rVert^2$: viết $f(v)-f(u)-\langle\nabla f(u),v-u\rangle=\int_0^1\langle\nabla f(u+r(v-u))-\nabla f(u),v-u\rangle\,dr$ (gradient liên tục vì Lipschitz), Cauchy–Schwarz, tính trơn, $\int_0^1r\,dr=\tfrac12$ (`aligned`). Đặt tên "cận trên bậc hai" (quadratic upper bound; còn gọi là descent lemma) — điểm mở 5. **Bước 2 (hàm phụ; tính lồi dùng ở đây).** Cố định $u$, đặt $q_u(v)=f(v)-\langle\nabla f(u),v\rangle$ (không dùng $\varphi$, $\psi$, $\phi$): $q_u$ lồi, $\beta$-trơn, $\nabla q_u(u)=0$; vì $q_u$ lồi, $u$ là điểm cực tiểu toàn cục của $q_u$ trên $\mathbb R^p$ (bất đẳng thức dưới gradient tại $u$). Câu bắt buộc: đây là dòng duy nhất dùng tính lồi; với $f(w)=-\tfrac12w^2$, $q_u$ không có cực tiểu (Bài tập 08.3). **Bước 3 (áp dụng Bước 1 cho $q_u$).** Tại điểm $v-\tfrac1\beta\nabla q_u(v)$, Bước 1 cho $q_u(u)\le q_u\big(v-\tfrac1\beta\nabla q_u(v)\big)\le q_u(v)-\tfrac1{2\beta}\lVert\nabla q_u(v)\rVert^2$; điểm này có thể nằm ngoài $W$, nên (S) cần trên toàn $\mathbb R^p$. Viết lại: $f(v)\ge f(u)+\langle\nabla f(u),v-u\rangle+\tfrac1{2\beta}\lVert\nabla f(v)-\nabla f(u)\rVert^2$. **Bước 4 (đổi vai).** Đổi $u$, $v$ và cộng hai bất đẳng thức, được (a). Câu sau $\square$: với hàm lồi, tính trơn và tính đồng bức tương đương (chiều kia ở đoạn sau Định nghĩa 08.3).
- **B. Chi tiết cho bất đẳng thức truy hồi** (khoảng 450 tiếng; cách hiểu "chi tiết hồi quy" của lời giao việc, điểm mở 6). (i) **Xáo trộn lại sau mỗi vòng.** Khi $m$ chia hết $T$ và mỗi vòng $(i_{km+1},\ldots,i_{(k+1)m})$ là một hoán vị đều, độc lập giữa các vòng: $\Pr(i_t=i)=1/m$ với mọi $t$ (đối xứng); Mệnh đề 08.5(a) không dùng phân bố của $\xi$, (b) chỉ dùng xác suất biên, nên cả hai đúng; Định lý 08.6 đúng với cùng cận, $\xi$ là dãy hoán vị (Định nghĩa 05.18 cho phép $\xi$ là một dãy bất kì độc lập với $S$). Một câu: Định nghĩa 05.10 đòi các lần rút độc lập, nên Định lý 05.14 không áp dụng nguyên văn cho xáo trộn lại; Hệ quả 08.8 chỉ phát biểu cho rút có hoàn lại. (ii) **Tính đo được.** Giả sử $(w,z)\mapsto\nabla\ell(w,z)$ đo được; khi đó $w_{t+1}$ là hàm đo được của $(s,\xi)$ (hợp của các hàm đo được, phép chiếu liên tục), nên $(s,\xi,z)\mapsto\ell(w_{T+1},z)$ đo được như Định nghĩa 05.18 đòi; như Phụ lục B của Bài 05. (iii) **Cận chuẩn của điểm lặp** (Bước 4 của Định lý 08.6): $\lVert w_{t+1}-w_1\rVert=\lVert\operatorname{proj}_W(w_t-\eta_tg_t)-\operatorname{proj}_W(w_1)\rVert\le\lVert w_t-w_1\rVert+\eta_tG$ (`aligned`), dùng $w_1\in W$. (iv) **Đổi thứ tự lấy tổng** của Hệ quả 08.7, viết đủ một lần.
- **C. Điểm dừng xấp xỉ** (khoảng 650 tiếng; QĐ 6; PTN §2.7). `::: proof Chứng minh Mệnh đề 08.12`. Lộ trình: cận trên bậc hai tại hai điểm lặp liên tiếp, kì vọng có điều kiện theo lịch sử, tổng triệt tiêu. **Bước 1 (cận trên bậc hai; tính trơn).** $F(w_{t+1})\le F(w_t)-\eta\langle\nabla F(w_t),g_t\rangle+\tfrac{\beta\eta^2}2\lVert g_t\rVert^2$. **Bước 2 (kì vọng có điều kiện; tính không chệch và cận phương sai).** $\mathbb E[\lVert g_t\rVert^2\mid\mathcal F_{t-1}]=\lVert\nabla F(w_t)\rVert^2+\mathbb E[\lVert g_t-\nabla F(w_t)\rVert^2\mid\mathcal F_{t-1}]$ (bản có điều kiện của đẳng thức sau Định nghĩa 05.10), nên $\mathbb E[F(w_{t+1})\mid\mathcal F_{t-1}]\le F(w_t)-\eta\big(1-\tfrac{\beta\eta}2\big)\lVert\nabla F(w_t)\rVert^2+\tfrac{\beta\eta^2\sigma^2}2$. **Bước 3 ($\eta\le1/\beta$).** $1-\tfrac{\beta\eta}2\ge\tfrac12$. **Bước 4 (tính chất tháp, tổng triệt tiêu, $F\ge F_*$).** Lấy kì vọng, cộng $t=1,\ldots,T$, dùng $\mathbb EF(w_{T+1})\ge F_*$, chia cho $\eta T/2$. Một câu về tính khả tích: giả sử $\mathbb E\lvert F(w_t)\rvert<\infty$ với mọi $t$ (đúng khi nguồn ngẫu nhiên có hữu hạn giá trị, như rút chỉ số từ $s$). Câu sau $\square$: cận chặn trung bình của bình phương chuẩn gradient, không chặn $F(w_{T+1})-F_*$.
- **D. Giao thức thí nghiệm** (khoảng 600 tiếng; QĐ 7; blueprint §E "held-out protocol and multiple runs"). Danh sách nhãn: **Dữ liệu** ($p=100$; $g\sim N(0,I_p/p)$, $x=g/\max\{1,\lVert g\rVert\}$, nên $\lVert x\rVert\le1$ với mọi đặc trưng có thể có; $w^\star$ đều trên mặt cầu đơn vị, rút một lần mỗi hạt giống; $y=\mathbb 1[\langle w^\star,x\rangle\ge0]$, lật với xác suất $0{,}1$, độc lập; $m=200$; mẫu kiểm tra $5000$ quan sát độc lập); **Mẫu lân cận** (một chỉ số $i$ rút đều trên $\{1,\ldots,m\}$; quan sát thứ $i$ thay bằng một quan sát mới rút từ $D$); **Thuật toán** (Thuật toán 08.1 với $W=\mathbb R^p$, không chiếu, $w_1=0$, $\eta_t=0{,}5$, $T=20\,000$ bước, tức $100$ vòng; chỉ số đều có hoàn lại; hàm lỗi logistic với nhãn $\tilde y=2y-1$); **Ba lần chạy** (trên $S$; trên mẫu lân cận với cùng dãy chỉ số; trên $S$ với một dãy chỉ số độc lập); **Đại lượng** (tại các bước $100$, $200$, $1000$, $2000$, $4000$, $10\,000$, $20\,000$: trung bình hàm lỗi logistic trên mẫu huấn luyện và trên mẫu kiểm tra, hiệu của chúng, lỗi phân lớp hai mẫu, $\Delta$ ghép cặp và không ghép cặp, tỉ lệ đổi nhãn dự đoán trên mẫu kiểm tra, chuẩn gradient của $L_S$, cận $2G^2\eta t/m$ với $G=1$); **Lặp lại** ($20$ hạt giống $0,\ldots,19$; báo trung bình, khoảng nhỏ nhất – lớn nhất); **Giả thiết** (một câu: mọi giả thiết của Định lý 08.6 thỏa, Ví dụ 08.6 Bước 1); **Làm tròn** (số đo làm tròn gần nhất, ba chữ số thập phân; cận trên làm tròn lên; cột khoảng cách là trung bình của hiệu nên có thể lệch một đơn vị ở chữ số cuối so với hiệu của hai cột đã làm tròn); **Chi phí** (khoảng $15$ giây trên một máy nhiều nhân với `numpy`). Không nêu đường dẫn script trong ghi chú (công cụ nằm ngoài repo).

**Yêu cầu cho script** `../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec08_coupled_sgd.py` (người viết ghi chú tạo từ `outline08/exp_draft.py`): chỉ `numpy`; tham số dòng lệnh `--p` ($100$), `--m` ($200$), `--eta` ($0{,}5$), `--seeds` ($20$), `--ntest` ($5000$); thứ tự rút ngẫu nhiên cố định trong mỗi hạt giống (`numpy.random.default_rng(seed)`): $w^\star$, mẫu huấn luyện, mẫu kiểm tra, chỉ số $i$, quan sát thay thế, dãy chỉ số ghép cặp, dãy chỉ số độc lập; in hai bảng (câu hỏi mở đầu; Ví dụ 08.6) đúng các cột đã nêu, cộng lỗi 0–1, khoảng giữa các hạt giống và chuẩn gradient (Bài tập 08.4, 08.6); chạy lại với `--eta 0.25` cho Bài tập 08.6. Bản nháp tái lập đúng số của PTN §3(e).

## 9. Thuật ngữ mới (đối chiếu `thuat-ngu.md`; điều phối viên sửa §10 trước khi viết)

`thuat-ngu.md` đã có và bài dùng đúng: hai lần chạy ghép cặp, không giãn, tính đồng bức, dừng sớm (§10); điểm dừng, khoảng cách tổng quát hóa kì vọng, hai mẫu lân cận, hệ số ổn định, quan sát thay thế, quan sát kiểm tra, tính ổn định đều, độ dài bước, vòng qua dữ liệu, xáo trộn lại sau mỗi vòng qua dữ liệu, điểm lặp cuối, trung bình có trọng số, rút có hoàn lại, phương sai của gradient ngẫu nhiên, hàm lỗi logistic, lịch sử, tính chất tháp, tổng triệt tiêu (§9); mẫu kiểm tra, cận không cho thông tin, lớp nơ-ron ẩn, lớp nơ-ron ra, đặc trưng ngẫu nhiên (§10). Không dùng "độ chênh tổng quát hóa" (lời giao việc); "độ chênh tối ưu" là suboptimality (PTN §6.2).

Đề xuất thêm vào §10:

| English | Đề xuất | Ghi chú |
|---|---|---|
| recurrence (inequality) | bất đẳng thức truy hồi | không dùng "hồi quy" (trùng regression: hồi quy logistic); điểm mở 1 |
| expansion factor; expansive | hệ số giãn; giãn | $\lVert\Gamma(u)-\Gamma(v)\rVert\le c\lVert u-v\rVert$; $1+\beta\eta$ khi không lồi |
| gradient step map | ánh xạ bước gradient | $\Gamma_{\eta,z}(w)=w-\eta\nabla\ell(w,z)$ |
| shared step; differing step | bước chung; bước khác biệt | $i_t\ne i$; $i_t=i$ (Định nghĩa 08.2) |
| cumulative step-size budget | ngân sách độ dài bước | $\sum_{t=1}^T\eta_t$ |
| step-size schedule | lịch độ dài bước | $\eta_t=\eta_0/t$, $\eta_0/\sqrt t$ (Bài tập 08.2) |
| quadratic upper bound (descent lemma) | cận trên bậc hai (còn gọi là bổ đề hạ) | điểm mở 5; chỉ Phụ lục A, C |
| explicit regularization; implicit regularization | chính quy hóa tường minh; chính quy hóa ngầm | Định nghĩa 08.9; ngầm = hành vi chọn lựa, không phải định lý |
| Huber loss | hàm lỗi Huber | $\ell_{\mathrm H}$, ngưỡng $1$ |
| prediction flip rate (prediction sensitivity) | tỉ lệ đổi nhãn dự đoán | thí nghiệm; không được định lý chặn |
| parameter distance | khoảng cách tham số | chỉ khi nói về HRS §6; trong bài là $\Delta_t$ "khoảng cách giữa hai lần chạy" |
| burn-in | giai đoạn đầu (trước khi quan sát khác biệt được dùng) | chỉ Nhận xét 08.11 [O] |
| approximate stationary point; stationarity | điểm dừng xấp xỉ; tính dừng | Mệnh đề 08.12 |
| weight decay; gradient clipping; backpropagation | suy giảm trọng số; cắt gradient (đã có §9); lan truyền ngược | chỉ mục Tài liệu đọc |

Sửa một dòng §10: "coupled runs" — ghi chú thêm "cùng khởi tạo, cùng độ dài bước, cùng dãy chỉ số; trên hai mẫu lân cận".

## 10. Kí hiệu mới (đề xuất bổ sung `ky-hieu.md`, QĐ 10; không tự sửa)

| Kí hiệu | Ý nghĩa | Ghi chú |
|---|---|---|
| $w'_t$, $w'_{T+1}$, $\bar w'_T$ | Điểm lặp của lần chạy ghép cặp trên mẫu lân cận $s^{(i)}$ | Bài 08; dấu phẩy như $z'$ (Bài 06), không phải mẫu bóng |
| $\Delta_t=\lVert w_t-w'_t\rVert$ | Khoảng cách giữa hai lần chạy ghép cặp; $\Delta_1=0$ | Bài 08; khác $\Delta_t=\lVert w_t-u\rVert^2$ chỉ trong chứng minh Bài 05; không dùng $\delta_t$ của HRS |
| $\xi=(i_1,\ldots,i_T)$ | Dãy chỉ số dùng chung của hai lần chạy | Bài 05, 08; cho điểm lặp cuối $w_{T+1}$ (Bài 05 dùng $\xi_{1:T-1}$ cho $\bar w_T$) |
| (S), (G) | Hàm lỗi lồi và $\beta$-trơn trên $\mathbb R^p$ với mọi $z$; $\lVert\nabla\ell(w,z)\rVert\le G$ với mọi $w\in W$, $z\in\mathcal Z$ | Bài 08; khác (C), (G1), (G2), (L), (T1)–(T7); điểm mở 2 |
| $\Gamma$, $\Gamma_{\eta,z}$ | Ánh xạ $\mathbb R^p\to\mathbb R^p$; ánh xạ bước gradient $w\mapsto w-\eta\nabla\ell(w,z)$ | Bài 08 |
| $q_u$ | Hàm phụ $f-\langle\nabla f(u),\cdot\rangle$ | Bài 08, chỉ Phụ lục A |
| $\ell_{\mathrm H}$ | Hàm lỗi Huber ngưỡng $1$ | Bài 08; không dùng $h$ (giả thuyết) |
| $\eta^*$, $T^*$ | Độ dài bước hằng tốt nhất với $T$ cho trước; số bước tốt nhất với $\eta$ cho trước, của cận ghép | Bài 08; khác $\lambda^*$ (Bài 06) |
| $c$, $t_0$ | Hằng số trong $\eta_t\le c/t$; bước kết thúc giai đoạn đầu | Bài 08, chỉ Nhận xét 08.11 |
| $F_*$ | $\inf F$ | Bài 08, chỉ Mệnh đề 08.12 và Phụ lục C; khác $L^*$ (Bài 04), $w^*$ (Bài 05) |
| $\tau$ | Chỉ số rút đều trên $\{1,\ldots,T\}$ | Bài 08, chỉ dòng diễn giải của Mệnh đề 08.12; $\tau$ ở Bài 04, 07 là nghĩa cục bộ khác (khác bài) |

Dòng sửa: $\epsilon_{\mathrm{stab}}(m)$ — thêm "với SGD phụ thuộc thêm $T$ và $\eta_t$ (Bài 08)"; $T$, $\eta_t$ — "Bài 05–08" đã có.

## 11. Phân bổ thời gian và ngân sách độ dài

### 11.1 Phân bổ thời gian 140 phút (chỉ trong dàn ý, blueprint 8.6)

| Khối blueprint | Phút | Nội dung ghi chú |
|---|---|---|
| motivation/coupling | 20 | câu hỏi mở đầu, §1–§3 lướt (Ví dụ 08.1), §4 (Thuật toán 08.1, Định nghĩa 08.2, Ví dụ 08.2) |
| nonexpansiveness | 20 | §5 (Định nghĩa 08.3, Bổ đề 08.4, Ví dụ 08.3); Phụ lục A chỉ nêu lộ trình |
| recurrence | 30 | §6 (Mệnh đề 08.5 chứng minh đầy đủ, Ví dụ 08.4) |
| nghỉ | 10 | — |
| stability theorem/interpretation | 30 | §7 (Định lý 08.6, Ví dụ 08.5, 08.6, Hệ quả 08.7) 18 phút; §8 (Hệ quả 08.8, Ví dụ 08.7, Định nghĩa 08.9) 12 phút |
| nonconvex limitations | 25 | §9 (Ví dụ 08.8, Mệnh đề 08.10, Ví dụ 08.9, 08.10; Nhận xét 08.11 và Mệnh đề 08.12 chỉ nêu phát biểu) |
| exit | 15 | §10 lướt, câu hỏi cuối buổi (a)–(d), cầu nối |

Nếu 150 phút không kể giờ nghỉ (blueprint §A "Timing"): thêm 10 phút cho Bài tập 08.1(d) hoặc câu hỏi cuối buổi (b).

### 11.2 Ngân sách độ dài

Trần: thân bài ≤ 12 000 tiếng, phụ lục ≤ 3 000 (QĐ 10; đếm `wc -w`, như Bài 06–07).

| Phần | Dự kiến (tiếng) |
|---|---|
| Đoạn dẫn, câu hỏi mở đầu, mục tiêu, tiên quyết, ôn nhanh | 1 450 |
| §1–§3 (thiết lập, kí hiệu và giả thiết, Ví dụ 08.1, khối ứng dụng) | 1 250 |
| §4 (Thuật toán 08.1, Định nghĩa 08.2, Ví dụ 08.2) | 900 |
| §5 (Định nghĩa 08.3, Bổ đề 08.4, Ví dụ 08.3) | 850 |
| §6 (Mệnh đề 08.5, đoạn sau, Ví dụ 08.4) | 1 100 |
| §7 (Định lý 08.6, Ví dụ 08.5, 08.6, Hệ quả 08.7, đoạn lời hứa) | 1 750 |
| §8 (Hệ quả 08.8, Ví dụ 08.7, Định nghĩa 08.9) | 1 300 |
| §9 (Ví dụ 08.8–08.10, Mệnh đề 08.10, Nhận xét 08.11, Mệnh đề 08.12) | 1 750 |
| §10–§13 | 1 400 |
| **Thân bài** | **11 750** |
| Phụ lục A–D | 2 450 |

Thứ tự cắt nếu vượt (mỗi mục bỏ được mà không hỏng mạch): (1) Ví dụ 08.8 Bước 6 (Monte Carlo); (2) Ví dụ 08.10 Bước 2 (bản lề; giữ một câu); (3) Ví dụ 08.7 Bước 4 ($m=10^6$); (4) trực giác một chiều sau Bổ đề 08.4; (5) số $(1{,}05)^{1000}$ sau Mệnh đề 08.10; (6) câu ôn nhanh 2; (7) rút §10 đoạn 4 còn ba câu. Không cắt: chứng minh Mệnh đề 08.5, Định lý 08.6, Hệ quả 08.8; Bước 1 của Ví dụ 08.6 (giả thiết nào thỏa); câu cảnh báo sau Hệ quả 08.8; Ví dụ 08.9.

### 11.3 Giai đoạn viết (mỗi đợt khoảng 150 dòng; người viết chạy `forward_refs.py` sau mỗi đợt)

0. **Script.** Tạo `exp_lec08_coupled_sgd.py` từ `outline08/exp_draft.py` theo yêu cầu ở mục 8; chạy với $\eta=0{,}5$ và $0{,}25$; chép số vào §13 của dàn ý; số trong ghi chú lấy từ lần chạy này.
1. Đầu bài đến hết §3.
2. §4–§5.
3. §6 và §7 đến hết Ví dụ 08.6.
4. Hệ quả 08.7 đến hết §8.
5. §9.
6. §10–§13.
7. Phụ lục A–D; đếm chữ; `forward_refs.py` 0; `sync-local-materials.py --check`; không "Mục này", "rõ ràng", "dễ thấy", "Đáp án", "hãy", "vô nghĩa", "hồi quy" theo nghĩa recurrence; không chữ có dấu trong `\text{}`; ghi sai khác vào mục 13.

## 12. Rủi ro, điểm mở và danh sách con số

### 12.1 Rủi ro (đã xử lý trong dàn ý)

1. **Biến không độc lập trong chứng minh truy hồi** (bài học Bài 06–07). Đã xử lý: Mệnh đề 08.5(a) trên từng quỹ đạo, (b) chỉ dùng xác suất biên; câu bắt buộc ở Bước 4.
2. **Ghép sai đầu ra** ($w_{T+1}$ với Định lý 05.14). Đã xử lý: Hệ quả 08.8 dùng $\bar w_T$; câu cảnh báo; Bài tập 08.8(c).
3. **Dừng sớm như định lý.** Đã xử lý: Hệ quả 08.8 đoạn kết, Ví dụ 08.7 kết luận, Định nghĩa 08.9 đọc sau, §10 đoạn 4.
4. **Chuyển kết quả lồi sang mạng ReLU.** Đã xử lý: Ví dụ 08.10, Bài tập 08.5, câu hỏi cuối buổi (d), §10.
5. **Thí nghiệm như bằng chứng cho định lý.** Đã xử lý: Ví dụ 08.6 Bước 1 nêu đúng giả thiết thỏa; kết luận "đường cong không phải là cận"; một câu ở câu hỏi mở đầu, một câu ở §10.
6. **Lượng từ của (G)**: $G$ chặn gradient tại **mọi** quan sát có thể (PTN §6.3(x)); nêu ở §2 và Ví dụ 08.6 Bước 1.
7. **Cầu nối nói trước kết quả Bài 09.** Đã xử lý: chỉ đặt câu hỏi; không khẳng định về mô hình chuỗi.
8. **Danh sách tiên quyết thiếu tên khối** (Bài 07). Đã xử lý ở mục 3.
9. **Làm tròn.** Mọi cận trên trong dàn ý đã làm tròn lên; số đo làm tròn gần nhất (nguyên tắc 8).

### 12.2 Điểm mở cho điều phối viên

1. **"Bất đẳng thức truy hồi"** cho recurrence (tránh "hồi quy" hai nghĩa). Phương án khác: "hệ thức truy hồi".
2. **Nhãn giả thiết (S), (G).** (G) gần chữ với (G1), (G2) của Bài 05 nhưng nghĩa khớp (cận gradient $G$; kéo theo (G2) cho oracle rút đều). Phương án khác: không đặt nhãn, gọi tên trong danh sách giả thiết ("tính lồi và tính trơn", "cận gradient").
3. **Định lý 08.6 có phép chiếu** (QĐ 2) — đã theo; thí nghiệm và ví dụ đều dùng $W=\mathbb R^p$ (trường hợp riêng).
4. **Kí hiệu $\epsilon_T$** cho $\tfrac{2G^2}m\sum_t\eta_t$ (gọn công thức ở 390 px) hay viết thẳng; dàn ý nghiêng về viết thẳng (tránh thêm kí hiệu).
5. **Tên "cận trên bậc hai"** (quadratic upper bound, còn gọi là descent lemma) — chỉ dùng ở Phụ lục A, C; "bổ đề hạ" là dịch sát, có thể bỏ phần "còn gọi là".
6. **Phụ lục B** hiểu "chi tiết hồi quy" của lời giao việc là chi tiết cho bất đẳng thức truy hồi (xáo trộn lại, đo được, cận chuẩn, đổi thứ tự tổng). Nếu ý là chi tiết hồi quy logistic: hằng số đã ở Bài tập 05.8, Ví dụ 08.5 Bước 1; có thể thêm một đoạn nhỏ vào Phụ lục D.
7. **Ví dụ 08.4 dùng $T=6$** (PTN dùng $T=5$) để khớp Ví dụ 08.1–08.2 và câu ôn nhanh 3.
8. **Ví dụ 08.9 dùng Huber** thay hàm lỗi bình phương của PTN (d2) để chỉ bỏ điều kiện độ dài bước; PTN (d3) (hàm lỗi bình phương không Lipschitz, $\mathbb E\Delta_{21}$ tăng tuyến tính theo $M$) chỉ còn một câu dẫn Ví dụ 06.9.
9. **Hai bài gốc thêm** (QĐ 9): 08.7 (giữ lời hứa Bài 06 bằng số) và 08.8 ($T^*$ và lỗi ghép đầu ra) thay cho hai gợi ý của QĐ 9 (điểm lặp trung bình đã thành Hệ quả 08.7 [F]; hằng số logistic đã là Bài tập 05.8).
10. **Biến thể mạng đặc trưng ngẫu nhiên của Bài 07** (PTN §3(e), `l08e`): không đưa số vào ghi chú; chỉ nêu là trường hợp riêng chặt chẽ ở Ví dụ 08.10 và §10.

### 12.3 Danh sách con số mới († trong dàn ý; đều trong `outline08/*.txt`)

Câu hỏi mở đầu: bảng năm dòng (huấn luyện, kiểm tra, khoảng cách) như PTN; tỉ số $11{,}2$, $108{,}8$; lỗi 0–1 kiểm tra $0{,}309$, $0{,}301$, $0{,}312$. Ôn nhanh: $1{,}5$; $3367/4096\approx0{,}8220$; $1{,}5\le3{,}5$. Ví dụ 08.1: đạo hàm $0,-1,-\tfrac12,-1,-1,1$. Ví dụ 08.2: không-ví dụ $\Delta=\tfrac12$ trên cùng mẫu. Ví dụ 08.3: $\tfrac12;1;2$ / $1;1;2$ / $1{,}5;3;4$. Ví dụ 08.4: nhóm $3$ và $\tfrac{17}4$; $\mathbb E\Delta_7=228\,203/262\,144\approx0{,}8705$. Ví dụ 08.6: bảng năm dòng; khoảng $1{,}31$–$15{,}08$ và $0{,}693$–$1{,}149$. Hệ quả 08.8: tỉ số $1{,}7321$. Ví dụ 08.7: $0{,}0708$ (giới hạn, làm tròn lên); $0{,}0958$; $0{,}1375$. Ví dụ 08.8: $\Delta_3/\Delta_2=1{,}1000$; bước $58$; $\Delta_{101}\approx2{,}879$; $\Delta\to\pi$. Sau Mệnh đề 08.10: $1{,}378\cdot10^4$; $275{,}6$. Nhận xét 08.11: $33{,}37$. Ví dụ 08.9: dãy $0{,}06,\ldots,3{,}84$; $0{,}04$; $0{,}02$. Ví dụ 08.10: $0{,}48$ (bản lề). Câu hỏi cuối buổi: $28{,}19$; $28{,}139$; $0{,}0113$. Bài tập 08.2: $48{,}94$; $992{,}72$; $0{,}0098$; $0{,}1986$; $0{,}6756$; $0{,}1359$; $0{,}5470$; $0{,}0519$. Bài tập 08.3: $275{,}6$. Bài tập 08.4: $0{,}004$; $1{,}0001$. Bài tập 08.5: $0{,}5032$. Bài tập 08.6: hai dãy $\eta=0{,}25$; $0{,}212$ và $0{,}213$. Bài tập 08.8: $0{,}0958$.

Các số của PTN dùng lại, đã tính lại và khớp: Ví dụ 08.1–08.2 (điểm lặp, $\Delta$), $\mathbb E\Delta_2=\tfrac14$, $\tfrac{29}{64}$, dãy $(2,3,1,4,4,4)$; $0{,}001$, $0{,}0005$, $0{,}0505$; $0{,}0500$, $0{,}0866$, $0{,}0791$, $0{,}0725$; $T^*\approx7071$, $0{,}1000$, $0{,}2800$; $0{,}0153$; $(1{,}05)^{1000}\approx1{,}5\cdot10^{21}$; $0{,}0009$; Monte Carlo cosin $0{,}592$, $2{,}204$, $3{,}030$; mọi số thí nghiệm $\eta=0{,}5$; $39{,}98$; $0{,}4750$.

### 12.4 Số hiệu đã grep (Bài 01–07)

Bài 01: Mệnh đề 01.7 (Tính không chệch của rủi ro thực nghiệm với giả thuyết cố định), Định nghĩa 01.10 (Khoảng cách tổng quát hóa), Định nghĩa 01.24 (Rủi ro vượt mức), (T1), (T2) (dòng 83). Bài 02: Nhận xét 02.11 (Hàm lỗi không bị chặn; hàm lỗi log ở đoạn sau). Bài 04: Định nghĩa 04.2 (Sai số tối ưu thực nghiệm). Bài 05: Định nghĩa 05.4, Mệnh đề 05.5, Định nghĩa 05.6, 05.7, Bổ đề 05.8 (và đoạn "không giãn" sau nó), Định nghĩa 05.10, Thuật toán 05.11, Định lý 05.14, Nhận xét 05.17, Định nghĩa 05.18, Hệ quả 05.19, Mệnh đề 05.20, Ví dụ 05.9, 05.12; Bài tập 05.8 (`exercises.md`, UML 12.2). Bài 06: Nhận xét 06.3, Định nghĩa 06.4, Mệnh đề 06.5, Định nghĩa 06.6, 06.9, Định lý 06.10, Mệnh đề 06.11, Ví dụ 06.3, 06.9; (L) (đoạn trước Mệnh đề 06.11); lời hứa: đoạn sau Định nghĩa 06.9 (dạng $\mathbb E_\xi\lvert\cdot\rvert$), §10 "SGD nhiều vòng", cầu nối cuối §12, Phụ lục E "Lý do chọn ổn định đều". Bài 07: Định nghĩa 07.1, 07.5, Hệ quả 07.16, Phụ lục D (giới hạn của hạ gradient), cầu nối §12 (dòng 960), Bài tập 07.5(c).

### 12.5 Kiểm tham chiếu tới trước trên giấy

Câu hỏi mở đầu: chỉ "§4–§7", "§7", "Phụ lục D". Mục tiêu: chỉ chữ. §3 khối ứng dụng: "§8", không "dừng sớm". §4: Định nghĩa 08.2 dẫn Thuật toán 08.1 (trước), "§6" cho mệnh đề sau. §5: "bổ đề dưới đây"; Ví dụ 08.3 nhắc "§9". §6: dẫn Bổ đề 08.4 (trước), "Phụ lục B". §7: dẫn Mệnh đề 08.5 (trước), Định lý 06.10; đoạn lời hứa dẫn "Bài tập 08.7" (bài tập nằm ở tệp khác; Bài 06–07 dẫn bài tập trong thân bài như vậy — người viết kiểm `forward_refs.py` có báo không; nếu báo, viết "§11"). §8: Hệ quả 08.8 dẫn Hệ quả 08.7 (trước); Định nghĩa 08.9 đứng sau Hệ quả 08.8 và Ví dụ 08.7, nên hai khối này và câu kết của chúng không dùng "dừng sớm", "chính quy hóa ngầm" như thuật ngữ (viết "số bước", "dừng sau $T^*$ bước"). §9: Ví dụ 08.8 trước Mệnh đề 08.10, nên Ví dụ 08.8 Bước 5 dẫn "Mệnh đề 08.5" (trước), không dẫn 08.10; Mệnh đề 08.12 dẫn Ví dụ 08.8 (trước). §10–§13 nhìn lại.

## 13. Sai khác khi viết

Người viết ghi chú, 2026-10-31. Ghi chú: 1 084 dòng; thân bài 11 950 tiếng, phụ lục 1 488 tiếng (`wc -w`); 12 khối 08.1–08.12, Ví dụ 08.1–08.10, một khối `application`; `forward_refs.py` 0.

### 13.1 Thí nghiệm (giai đoạn 0)

Script `../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec08_coupled_sgd.py` (ngoài repo, chỉ NumPy, `argparse`: `--p 100 --m 200 --eta 0.5 --seeds 20 --ntest 5000 --rho 0.1`), viết lại từ `outline08/exp_draft.py` với cùng thứ tự rút ($w^\star$, mẫu huấn luyện, mẫu kiểm tra, $i$, quan sát thay thế, dãy ghép cặp, dãy độc lập), nên tái lập đúng số của bản nháp (so từng dòng: trùng). Chạy bằng `/data/tqlong/lectures/.venv/bin/python`, khoảng 14 giây. In bảng câu hỏi mở đầu, bảng Ví dụ 08.6 (bảy thời điểm: $0{,}5$; $1$; $5$; $10$; $20$; $50$; $100$ vòng) và bảng đầy đủ (trung bình, nhỏ nhất, lớn nhất; lỗi 0–1; chuẩn gradient của $L_S$; tỉ số cận/khoảng cách). Đầu ra lưu ở scratchpad `writer08/exp_eta05_final.txt`, `writer08/exp_eta025.txt`.

Kết quả $\eta=0{,}5$ (trung bình 20 hạt giống, bốn chữ số):

| Vòng | Huấn luyện | Kiểm tra | Khoảng cách [min, max] | 0–1 kiểm tra | $\Delta$ ghép cặp [min, max] | $\Delta$ không ghép cặp | Đổi nhãn | $\lVert\nabla L_S\rVert$ |
|---|---|---|---|---|---|---|---|---|
| 0,5 | 0,6177 | 0,6622 | 0,0445 [0,0300; 0,0619] | 0,3827 | 0,1417 [0; 0,3815] | 2,9942 | 0,0152 | 0,0387 |
| 1 | 0,5612 | 0,6404 | 0,0792 [0,0525; 0,1070] | 0,3562 | 0,2332 [0; 0,8845] | 3,8273 | 0,0160 | 0,0335 |
| 5 | 0,3762 | 0,5894 | 0,2131 [0,1717; 0,2709] | 0,3089 | 0,8732 [0,1851; 1,7716] | 4,9029 | 0,0218 | 0,0171 |
| 10 | 0,3049 | 0,6027 | 0,2977 [0,2375; 0,3629] | 0,3011 | 1,4719 | 4,9252 | 0,0257 | 0,0122 |
| 20 | 0,2431 | 0,6622 | 0,4192 [0,3431; 0,5343] | 0,3009 | 2,2185 [0,7314; 5,0654] | 4,8228 | 0,0262 | 0,0086 |
| 50 | 0,1767 | 0,8269 | 0,6503 | 0,3043 | 3,7320 | 4,3442 | 0,0310 | 0,0057 |
| 100 | 0,1345 (chính xác 0,134477) | 1,0533 | 0,9188 [0,6930; 1,1494] | 0,3118 | 5,4583 [1,3096; 15,0812] | 4,0015 | 0,0339 | 0,0042 |

Tỉ số cận/khoảng cách: 11,24 (nửa vòng) đến 108,84 (100 vòng). $\eta=0{,}25$: khoảng cách 0,0246; 0,0464; 0,1470; 0,2121; 0,2991; 0,4613; 0,6511; $\Delta$ ghép cặp 0,0727; 0,1244; 0,5229; 0,9306; 1,4469; 2,5308; 3,7448 (khớp dàn ý mục 4, Bài tập 08.6).

**Sai khác số liệu với dàn ý:** lỗi huấn luyện ở 100 vòng là $0{,}134477$, làm tròn gần nhất thành $0{,}134$, không phải $0{,}135$ như mục 1 của dàn ý; ghi chú dùng $0{,}134$ (khoảng cách $0{,}919$ không đổi, $1{,}053-0{,}134=0{,}919$). Mọi số khác của mục 1, mục 3 (Ví dụ 08.6, Định nghĩa 08.9) khớp lần chạy.

### 13.2 Sai khác khi viết ghi chú (kèm lý do)

1. **Bảng câu hỏi mở đầu bỏ cột "Cận (§7)"**: cận $t/200$ bằng đúng số vòng, nên ghi một câu "cận … bằng đúng số vòng ở cột đầu"; với năm cột, bảng tràn ở 390 px. Câu trả lời viết "ở đây cận đó bằng số vòng", "nằm dưới cận" thay cho "cột cuối". Đoạn trả lời chia hai đoạn.
2. **Bảng Ví dụ 08.6 còn ba cột** (Vòng, Ghép cặp, Không ghép cặp): bản bốn và năm cột tràn ở 390 px trong khối ví dụ (bề rộng 271 px). Cột cận bỏ vì bằng số vòng; tỉ lệ đổi nhãn (thuật ngữ in nghiêng, tiếng Anh) chuyển thành một câu liệt kê năm giá trị.
3. **Hàm lỗi Huber** định nghĩa bằng danh sách hai dòng thay cho `cases` (tràn ở 390 px).
4. **Cắt theo thứ tự cắt của dàn ý** (thân bài lúc đầu 12 301 tiếng): Ví dụ 08.8 Bước 6 (Monte Carlo); Ví dụ 08.10 Bước 2 rút còn một câu; Ví dụ 08.7 Bước 4 ($m=10^6$); trực giác một chiều sau Bổ đề 08.4; số $(1{,}05)^{1000}$. Thêm: bỏ số $0{,}0009$ ($\beta=1$, $c=0{,}1$) ở Nhận xét 08.11; bỏ câu "số bước bằng $1\%$ một vòng" ở Ví dụ 08.5; bỏ câu về hàm lỗi bình phương và Ví dụ 06.9 ở kết luận Ví dụ 08.10 (giới hạn "Cận gradient đều" ở §10 vẫn nêu); rút §13 (tài liệu đọc, quan hệ với nguồn).
5. **Danh sách tiên quyết** khớp các khối thật sự được dẫn: bỏ Mệnh đề 01.7, Nhận xét 05.17, Mệnh đề 05.20, Định nghĩa 07.5 (không dẫn trong thân bài; Nhận xét 05.17 chỉ dùng ở Bài tập 08.2); thêm Ví dụ 05.9, 05.12, Hệ quả 06.2, Ví dụ 06.3, 06.9, Ví dụ 07.3, Bài tập 07.5 (đều được dẫn); "mẫu xác thực (§8 của Bài 04)" vì Bài 04 không có khối định nghĩa riêng. Mục "Giải tích" rút gọn; công thức tích phân dọc đoạn thẳng được nêu tại chỗ ở Phụ lục A.
6. **Mệnh đề 08.12**: không dẫn Mệnh đề 05.20; $\sigma^2$ đặt tên tại giả thiết của mệnh đề.
7. **Hệ quả 08.7, đoạn lời hứa Bài 06**: ghi $39{,}975$ (giá trị chính xác) thay cho "không quá $39{,}98$".
8. **Câu kết §5** đổi thành "Bổ đề không nói gì về bước khác biệt…" để không lặp câu mở §9 (cùng ý "tính lồi, tính trơn chỉ đi vào qua bổ đề"). **Câu kết §6** đổi thành một giới hạn có số ($0{,}8705$ so với $1{,}5$) thay vì nhắc lại phát biểu của Mệnh đề 08.5. Câu kết §7 chỉ giữ câu về sai số tối ưu (câu "không phụ thuộc số chiều" đã có trong khối định lý).
9. **Nhận xét 08.11** viết thành **Giả thiết.** (ba dòng) / **Bảo đảm.**, theo yêu cầu mọi phát biểu hình thức có hai nhãn này; chỉ nêu quy tắc rút có hoàn lại (Định lý 3.12 của HRS phát biểu cho SGM; Bổ đề 3.11 xét cả hoán vị).
10. **Kí hiệu cục bộ để vừa 390 px**: chứng minh Mệnh đề 08.5 Bước 2 viết gọn $\Gamma=\Gamma_{\eta_t,z_i}$; Định lý 08.6 Bước 4 đặt $g_t=\nabla\ell(w_t,z_{i_t})$; Bổ đề 08.4 chứng minh đặt $d=\nabla f(u)-\nabla f(v)$; Phụ lục A đặt $v^+=v-\tfrac1\beta\nabla q_u(v)$. Hệ quả 08.8(b) viết $\eta^*=\frac R{G\sqrt T}\big(1+\tfrac{2(T-1)}m\big)^{-1/2}$ (cùng giá trị).
11. **Phụ lục B** chỉ còn (i) xáo trộn lại và (ii) tính đo được: (iii) cận chuẩn điểm lặp và (iv) đổi thứ tự tổng đã viết đủ trong thân bài (Định lý 08.6 Bước 4, Hệ quả 08.7 Bước 3).
12. **Phụ lục D** thêm một đoạn kết quả ngoài các số đã dùng (10 và 50 vòng; lỗi 0–1 kiểm tra; chuẩn gradient $0{,}039\to0{,}004$; $\eta=0{,}25$ cho khoảng cách $0{,}651$ ở 100 vòng, gần $0{,}650$ của $\eta=0{,}5$ ở 50 vòng, cùng ngân sách $5000$). Không nêu đường dẫn script.
13. **Câu hỏi cuối buổi (b)**: lời giải không nêu tổng thật $28{,}139$ (không cần cho cận); bỏ câu so sánh tỉ lệ ngân sách ($\approx71$ lần) chưa được kiểm.
14. **§11** dẫn tệp bài tập như Bài 07 (`exercises.md` chưa có; liên kết sẽ đúng khi bài tập được viết). **§13** không ghi trang PDF (trang chỉ trong dàn ý).
15. **Script**: in bảy thời điểm (thêm 10, 50 vòng) và bảng có cột "Cận", là tập cha của hai bảng trong ghi chú.
16. Các thuật ngữ "chính quy hóa ngầm", "chính quy hóa tường minh", "dừng sớm" chỉ dùng từ Định nghĩa 08.9 trở đi; §10 dùng "dừng sớm theo Hệ quả 08.8" (nhìn lại).

### 13.3 Kiểm tra đã chạy

`sync-local-materials.py` và `--check` (OK); `forward_refs.py` 0; `git diff --check` sạch; 33 khối mở, 33 khối đóng; viewer qua HTTP (cổng 8783, đã tắt) và `file://` ở 1600×900 và 390×844 với mọi `details` mở: 1 350 công thức KaTeX, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức hay bảng tràn (đo `scrollWidth`), không tràn ngang trang; bản in 45 trang. Console HTTP có một cảnh báo CSP về script nội tuyến do `reloadserver` chèn, cũng xuất hiện với Bài 07; `file://` không có cảnh báo. Ảnh chụp ở scratchpad `writer08/shots/`.

### 13.4 Biên tập vòng 1 (2026-10-31)

Theo `reviews/0-quyet-dinh.md`; bảng từng phát hiện ở `bien-tap-vong-1.md`. Sai khác mới so với dàn ý:

1. **Chỗ dùng tính lồi (N1).** Bước khác biệt của Mệnh đề 08.5 nay chỉ dùng (G), bất đẳng thức tam giác và tính không giãn của phép chiếu: $\Delta_{t+1}\le\lVert(w_t-w'_t)-\eta_t(g-g')\rVert\le\Delta_t+2G\eta_t$, không qua điểm trung gian $\Gamma(w'_t)$ của blueprint 8.3 (quyết định của điều phối viên). Bước 1 của Định lý 08.6 lấy tính Lipschitz trên $W$ từ (G) bằng định lý giá trị trung bình (tính lồi của $W$), không qua Mệnh đề 05.5(a). Tính lồi của hàm lỗi chỉ còn ở Bổ đề 08.4(a), tại bước chung; câu tổng kết §7, §9, $\square$ Mệnh đề 08.10 và Phụ lục A nói đúng điều này. Mệnh đề 08.10, Bước 2: bước khác biệt dùng lại Bước 2 của 08.5.
2. **Chuyển chứng minh ra phụ lục để giữ trần 12 000 tiếng:** chứng minh Hệ quả 08.8 thành Phụ lục E (tiêu đề khối "chứng minh đầy đủ (ở Phụ lục E)", thân bài giữ một câu lộ trình); phác thảo chứng minh Mệnh đề 08.10 thành Phụ lục F (thân bài giữ một câu lộ trình). Thứ tự số khối không đổi.
3. **§9 sắp lại:** Ví dụ 08.8 → Mệnh đề 08.10 → Nhận xét 08.11 → Mệnh đề 08.12 (cùng đoạn sau nó) → câu chuyển → Ví dụ 08.9 → Ví dụ 08.10 → câu kết (giới hạn: mạng ReLU không có cận ổn định trong học phần). Số khối vẫn tăng (08.10, 08.11, 08.12; ví dụ đếm riêng), không đánh số lại.
4. **Bỏ câu ôn nhanh 2** (phép chiếu, thứ tự cắt 6 của mục 11.2); câu 3 cũ thành câu 2.
5. **Ví dụ 08.6:** bỏ lần chạy không ghép cặp khỏi thân bài (số ở Phụ lục D, kèm câu "các định lý không nói gì về đại lượng này"); bảng ba cột Vòng / $\Delta$ ghép cặp / Đổi nhãn (vừa 390 px); tỉ số dùng số trong bảng ($0{,}5/0{,}045\approx11{,}1$, $100/0{,}919\approx108{,}8$).
6. **§4:** thêm phép tính một bước cho ghép cặp ($\tfrac38$, $\tfrac18$, hiệu $\tfrac14$; ghép cặp $\tfrac14$; độc lập $\tfrac38$; người viết kiểm bằng liệt kê 4 và 16 trường hợp); thay không-ví dụ cũ (cùng mẫu, hai dãy chỉ số). Ví dụ 08.2 bỏ câu ngân sách $3$ (bước 4 đổi tên "tổng các phần tăng").
7. **Kí hiệu:** hệ số giãn $\kappa$ (không dùng $c$, giữ $c$ cho $\eta_t\le c/t$); chỉ số cộng $k$ thay $s$ (Hệ quả 08.7, Mệnh đề 08.10, đoạn $c/t$, tiên quyết); $g_{uv}=\nabla f(u)-\nabla f(v)$ thay $d$ (Bổ đề 08.4); $g_r$ trong Phụ lục A; $g$, $g'$ cục bộ ở Bước 2 Mệnh đề 08.5.
8. **Bảo đảm của Định lý 08.6, Hệ quả 08.8, Mệnh đề 08.10** viết thành đoạn có nhãn in đậm thay cho danh sách, để công thức có 271 px thay vì 230 px; $\eta^*=R/(G\sqrt{T+2T(T-1)/m})$.
9. **Mệnh đề 08.12** có thêm giả thiết **Khả tích**; Phụ lục C Bước 4 dẫn giả thiết đó.
10. **Mệnh đề 08.5** phát biểu cho mọi quy tắc rút với $\Pr(i_t=i)=1/m$ (phủ xáo trộn lại); Phụ lục B(i) thêm trường hợp một hoán vị dùng lại.
11. **Định lý 08.6 Bước 4** thêm cận $\mathbb EL_S(w_{T+1})\le L_D(w_1)+G^2\sum_t\eta_t$ (Mệnh đề 01.7 trở lại danh sách tiên quyết).
12. **§10** kết bằng đoạn văn xuôi (cấp lớp và cấp thuật toán); gạch đầu dòng "Cận trên" thành "Độ chặt" với nội dung mới (tăng tuyến tính so với đo được), số "11–109 lần" chỉ còn ở Ví dụ 08.6.
13. **§13:** bỏ gạch đầu dòng "Bài tập" (lý do đã ở §11); HRS §6 / §7 tách; HRS đánh số từ $w_0$; cách đọc $\sqrt3$, $\sqrt2$ của bài báo; UML §20.6 dùng quan sát mới.
14. **Tiêu đề Bài tập 08.3** đổi thành "Bước chứng minh không còn đúng khi bỏ tính lồi" (mục 4 ở trên đã sửa); đáp án mong đợi của (a)–(b) khớp chứng minh mới (tính lồi chỉ ở Bổ đề 08.4(a), bước khác biệt chỉ cần (G)).
15. Script thí nghiệm không đổi (đã in sẵn $\Delta$ không ghép cặp ở bảy thời điểm).

Số tiếng sau biên tập: thân bài 11 982 (trước 11 946), phụ lục 2 106 (trước 1 488); 1 111 dòng.

### 13.5 Biên tập vòng 2 (2026-10-31)

Theo `reviews/6-ra-lai-toan.md`, `reviews/7-ra-lai-mach.md` (chi tiết ở `bien-tap-vong-1.md`, mục "Vòng 2"). Sai khác mới: **chữ phụ lục đánh lại theo thứ tự đọc** — A tính đồng bức, B chi tiết bất đẳng thức truy hồi, C chứng minh Hệ quả 08.8 (mục 13.4 gọi là E), D phác thảo Mệnh đề 08.10 (13.4 gọi là F), E điểm dừng xấp xỉ (mục 8 của dàn ý gọi là C), F giao thức thí nghiệm (mục 8 gọi là D). Bảng số ở mục 2: Hệ quả 08.8 "chứng minh đầy đủ (ở Phụ lục C)", Mệnh đề 08.10 "phác thảo (ở Phụ lục D)", Mệnh đề 08.12 "đọc thêm (chứng minh ở Phụ lục E)". Cầu nối có lại câu "Câu hỏi cho Bài 09 là: …". Kí hiệu cục bộ $g_t$, $g'_t$ ở bước khác biệt (Mệnh đề 08.5). Thân bài 11 995 tiếng, phụ lục 2 131.
