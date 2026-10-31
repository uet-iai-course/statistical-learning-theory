# Biên tập vòng 1 — Bài 05 (2026-10-31)

Tệp nội bộ. Biên tập viên duy nhất của `materials/lec-05/lecture-note.md`, theo `reviews/0-quyet-dinh.md` (QĐ) và năm báo cáo R1–R5. Số dòng "cũ" theo bản đóng băng `lec05-draft-frozen.md`; số dòng "mới" theo ghi chú sau biên tập. Không commit.

**Kết quả kiểm tra:** thân bài $11\,988$ tiếng (`wc -w` trước `## Phụ lục`), phụ lục $1\,182$; `forward_refs.py` báo 0; đồng bộ rồi `--check` OK; 52 khối mở và 52 khối đóng, không lồng nhau; không có chữ có dấu trong `\text{}`; bảng tối đa 3 cột; render `file://` ở 390 px không lỗi KaTeX, không tràn ngang. Không đổi số khối (05.1–05.20) hay số ví dụ (05.1–05.16). Kịch bản: `scratchpad/py/l05_edit_1.py` đến `l05_edit_18.py` (thay chuỗi), `l05_edit_num1.py` (số mới).

## A–B. Quyết định nghiêm trọng và trung bình

| Mục | Trạng thái | Dòng mới | Ghi chú |
|---|---|---|---|
| N1 | áp dụng | 39, 101–104, 143–147, 245, 968–976, 983 | $h_w(x)=\langle w,x\rangle$ là *hàm điểm số* (score function) trong bảng §2; $h_{w,0}=\mathbb 1[h_w\ge0]$ chỉ cho lỗi 0–1; $\ell(w,z)=\ell(h_w,z)$ với dự đoán thực; Ví dụ 05.2 "hàm lỗi bản lề của hàm điểm số $h_w$"; ứng dụng: hồi quy logistic dùng hàm lỗi của $h_w$, thay cho lỗi 0–1 của $h_{w,0}$; đoạn sau Định nghĩa 05.18: lớp hàm điểm số; Hệ quả 05.19: $\operatorname{opt}_s(w)=L_s(w)-\inf_{w'\in W}L_s(w')$ (Định nghĩa 04.2 cho lớp hàm điểm số và hàm lỗi $\ell$); câu hỏi cuối buổi (c) nói lớp hàm điểm số |
| M1 | áp dụng | 15 | "Không nhất thiết, kể cả theo kì vọng." |
| M2 | áp dụng | 83; 993, 1170, 1181, 1184 | Định nghĩa độ chênh tối ưu có công thức ở §1 mục 7; mọi chỗ "sai số tối ưu" trơn đổi thành "sai số tối ưu thực nghiệm $\operatorname{opt}_S$" (kiểm bằng grep: không còn) |
| M3 | áp dụng | 15, 641, 646, 680, 744 | Bỏ "số hạng nhiễu"; mở §7: "chỉ có thêm một số hạng $\eta^2\lVert g\rVert^2$, có mặt cả khi $g$ là gradient đúng"; □ Mệnh đề 05.13: "số hạng bậc hai theo độ dài bước"; □ Định lý 05.14: "mức sàn sai số (error floor) $\eta G^2/2$" (tiếng Anh chuyển lên đây, bỏ ở đoạn cuối §8) |
| M4 | áp dụng | 1111 | "so sánh giữa các cận trên dưới (C), (G2), không phải so sánh thời gian chạy" |
| M5 | áp dụng | (cũ 919) | Câu chương trình rút quan sát mới đã xóa; §13 giữ "hai cách dùng dữ liệu" |
| M6 | áp dụng | 29, 1119–1125, 885–887 | Mục tiêu 5 viết lại đúng chữ của QĐ; §11 danh sách ba giả thiết và một câu riêng về điểm lặp cuối; câu dẫn §8 giữ "hoặc đổi đầu ra" |
| M7 | áp dụng | 587, 610–638 | Tiêu đề "chứng minh cho $\Xi$ hữu hạn"; câu nối về biến cố có xác suất dương và $\mathbb E[\cdot\mid\mathcal F_{t-1}]$; lịch sử $k_{1:t-1}$; tổng ở Bước 3 viết nhiều dòng (vừa 390 px) và ghi "các tổng lấy theo mọi $k_{1:t-1}\in\Xi^{t-1}$" |
| M8 | áp dụng | 735–739, 758, 912–918, 1121, 1127 | Bước 3 "(kì vọng; tính không chệch)", chỉ dùng (G1); tính lồi là điều kiện để (G1) thỏa được, và (G1) trên $W$ buộc $F$ lồi (R2); đoạn sau chứng minh: tính lồi dùng ở Bước 5 và là điều kiện của (G1); Ví dụ 05.10 kết: (G1) hỏng do $f$ không lồi; §11 dòng tính lồi và đoạn cuối. Mục tiêu 1 giữ nguyên chữ |
| M9 | áp dụng | 570–580 | Danh sách ba lựa chọn: $g_3$, điểm trước chiếu và chuẩn ($1{,}2247$; $1{,}2247$; $0{,}9899$), dòng nào chiếu; Bước 4 GD: $(0{,}8330;-0{,}7670)$, chuẩn $1{,}1324$, chiếu thành $(0{,}7356;-0{,}6774)$, $L_S\approx0{,}0614$. Dùng danh sách thay bảng 5 cột để vừa 390 px. Ví dụ 05.6 nay có Bước 1–5 |
| M10 | áp dụng | 950–958 | $W=[-1,1]$, $w_1=0$, $\lvert\varphi\rvert\le4$ nên $G=4$; Bước 3: $L_S=(w-0{,}5)^2+0{,}25$, $\tilde F=(w-0{,}1)^2+0{,}09$, $\mathbb E(\bar w_T-0{,}1)^2\to0$ nên $\mathbb EL_S(\bar w_T)-0{,}25\to0{,}16$; bỏ "với mọi $T$" ở cả §11 |
| M11 | áp dụng | 1199; `outline.md` §7 | UML viết $\arg\min$; $\Pi_W$ là của đề cương (blueprint), trùng $\Pi_{\mathcal H}$ |
| M12 | áp dụng | 344 | Chỉ tính lồi mạnh gắn với UML §14.4.4 |
| M13 | áp dụng | 17, 775, 1029–1031, 1032, 1117, 1100, 1111 | "đủ theo cận"; "với xác suất ít nhất $0{,}95$ theo $\xi$"; "theo cận" cho lô nhỏ; câu mở đầu "$10^4$ bước GD cũng đủ" |
| M14 | áp dụng | 1181 | "sai số ước lượng của $\bar w_{1600}$ (Định nghĩa 04.1)" tách khỏi sai số tối ưu thực nghiệm $0{,}0025$ |
| M15 #2 | áp dụng | 158 | "không khả vi tại các điểm gãy, nơi $\tilde y\langle w,x\rangle=1$" |
| M15 #3 | áp dụng | (cũ 176), 341 | Xóa câu Lipschitz trước định nghĩa; □ Mệnh đề 05.5 thêm "vì bất đẳng thức dưới gradient đòi mọi $u\in\mathbb R^p$" |
| M15 #4 | áp dụng | 306–340, 610–638, 1254–1263 | Tập mở $U$; lịch sử $k_{1:t-1}$; bổ đề đóng băng dùng $\Phi$, $\bar\Phi$ |
| M15 #5 | áp dụng | như M2 | |
| M15 #6 | áp dụng | 113, 179, 445, 642, 883, 1250, 1196–1199 | Bỏ "§9 cho thấy"; "§7 dùng nó" → câu về trung bình; câu không giãn; câu cuối §6 viết lại; cuối §7 viết lại; "Phần này hoàn tất" → "Khi $\Xi$ … cần bổ đề đóng băng …"; §14: "Ở đây …" thay "học phần dùng/mô tả" |
| M15 #7 | áp dụng | 500–504 | Danh sách ba trường hợp, nhãn danh từ song song |
| M15 #8 | áp dụng | 683–697 | Ví dụ 05.7: Bước 1 khoảng cách ($0{,}0034$; $0{,}1764$), Bước 2 hai vế trong `aligned` với $2\eta=1$, $\tfrac\eta2\lVert g\rVert^2=1$, Kết luận |
| M15 #9 | áp dụng | như M9 | |
| M15 #10 | áp dụng một phần | 9–11, 32–36, 112, 500, 968–975, 1005–1008, 1196–1198 | Tách các câu dài ở mở đầu, tiên quyết, §2, đoạn sau Định nghĩa 05.10 (thành danh sách), Định nghĩa 05.18, đoạn sau Hệ quả 05.19, §14. **Không áp dụng** cho Mục tiêu 1 (dòng 25): QĐ M8 ghi "Mục tiêu 1 giữ nguyên" |
| M15 #11 | áp dụng | 207–209, 309–316, 383, 480–481, 590–593, 768–769, 1049–1056 | Mệnh đề 05.3, 05.5, Bổ đề 05.8(b), Định nghĩa 05.10, Bổ đề 05.12, Hệ quả 05.15, Mệnh đề 05.20 có nhãn song song theo đề xuất R4; Định nghĩa 05.18 viết hai câu |
| M15 #12 | áp dụng | 362, 449, 883, (cũ 909, 984), 1111 | Đoạn kết tóm tắt: cuối §4 rút còn một câu; cuối §5 thành giới hạn (tính $\operatorname{proj}_W$ tổng quát là bài toán tối ưu riêng); cuối §7 một câu; cuối §8 và cuối §9 xóa; cuối §10 giữ hai câu giới hạn |
| M15 #13 | áp dụng | 966 (cũ 913), (cũ 829, 711, 904, 1058, 342) | Các câu lặp đã bỏ hoặc viết lại |
| M15 #14 | áp dụng | 1254–1263 | "phát biểu không chứng minh"; bỏ "kết quả chuẩn"; danh sách $\sigma$-đại số / Biến đã biết / Biến độc lập / Hàm; không thêm nguồn |

## C. Cắt

| Cắt | Nguồn | Trạng thái | Tiếng (ước) |
|---|---|---|---|
| C1 đoạn tóm tắt cuối §8 | R5 | đã cắt | 46 |
| C2 câu tốc độ GD trơn | R5 | đã cắt | 27 |
| C3 câu đầu sau chứng minh Định lý 05.14 | R5 | viết lại theo M8 (ngắn hơn) | 20 |
| C4 câu xáo trộn cuối §10 | R5 | đã cắt | 14 |
| C5 câu đầu cuối §9 | R5 | đã cắt (cả đoạn) | 26 |
| C6 câu Jensen ở Bước 5 | R5 | đã cắt | 20 |
| C7 sau dấu hai chấm ở □ Bổ đề 05.8 | R5 | đã cắt | 14 |
| C8 câu số vòng lặp/chi phí cuối §7 | R5 | đã cắt (đoạn viết lại) | 14 |
| C9 câu điểm lặp cuối trong Ví dụ 05.12 | R5 | đã cắt | 20 |
| C10 câu "đúng với mọi $s$" sau Hệ quả 05.19 | R5 | đã cắt | 20 |
| C11 câu trơn/lồi mạnh ở §2 | R5 | đã cắt | 15 |
| C12 câu chương trình rút mới | R5 | đã cắt (M5) | 26 |
| Định nghĩa 05.6: hai đoạn đọc gộp thành một | R1 | rút gọn, giữ khối | khoảng 40 |
| §11 ba đoạn đầu gộp còn hai | biên tập viên | rút gọn | khoảng 90 |
| §14 các gạch đầu dòng, tiên quyết, §1 mục 4 và 8, câu dẫn §2, các câu kết của Ví dụ 05.3, 05.8, 05.9, 05.15, 05.16, câu chuyển ý trước Định nghĩa 05.10 | biên tập viên | rút gọn | khoảng 230 |

Không cắt nội dung toán học, chứng minh hay bước ví dụ.

## D. Phát hiện nhẹ

**R1 (22 mục):** tất cả áp dụng. Kết luận Ví dụ 05.2 "chứa đoạn …; Bài tập 05.1 chứng minh nó đúng bằng đoạn này" (267); bỏ vế "các kết quả vẫn đúng … tập mở" (179); câu cuối mở đầu viết lại (15, không dùng "§7 đo", tránh văn bản làm chủ ngữ); đối tượng so sánh quả cầu bán kính 5 (17); §1 câu mở (75); (T1) có chú giải (111); $B$ khác cận của Bài 04 (108); điểm bị chiếu đổi thành $\theta$ ở §5, Mệnh đề 05.13 và Phụ lục A; hằng số Lipschitz của hàm lỗi bình phương viết luôn phép tính và dẫn phần (a) (304); "Theo (G2) và Cauchy–Schwarz", khai triển như câu ôn nhanh 3 (489); (c) thêm $\langle g_t,w_t-u\rangle$ khả tích (604); "trên từng quỹ đạo (với mỗi dãy giá trị cụ thể của $\xi_1,\ldots,\xi_T$)" (721); Ví dụ 05.7 ba bước; Ví dụ 05.8 Bước 4 rút ra thừa số trong `aligned`; Ví dụ 05.10 đặt tên hai nhánh và công thức trung bình cấp số nhân; Ví dụ 05.11 cận $12{,}81/\sqrt T$ với $\eta$ của Hệ quả 05.15; Ví dụ 05.13 có $W$ (M10); xáo trộn lại chỉ nói ở danh sách §6, bỏ cắt gradient (không định nghĩa được gọn); $\delta'$ có chú giải, $\xi=(\xi_1,\ldots,\xi_{T-1})$ với $P_\xi^{\otimes(T-1)}$; "đủ" thay "cần"; câu hỏi cuối buổi (c) thêm dòng tổng cấp số nhân và $0{,}9875^{1600}\approx1{,}8\cdot10^{-9}$; tiên quyết thêm $\sigma$-đại số.

**R2 (10 mục):** tất cả áp dụng. Bước GD có chiếu (M9); làm tròn lên $4{,}000625$ (in đúng giá trị, không cần làm tròn) và $0{,}2281$; so sánh "$4<4{,}000625$" thay cho "$4-0{,}06112$"; Mệnh đề 05.5 giả thiết theo phần ((a) không cần tập mở); tiêu đề Bổ đề 05.12; Ví dụ 05.2 kết luận; Ví dụ 05.11 (cận có ích với $\eta$ của Hệ quả 05.15; kết luận "Bước 4 của chứng minh cần (G2)"); "đủ"; Mệnh đề 05.20 "**Oracle gốc.** … như Định nghĩa 05.10, thỏa (G1)"; câu dòng 158 bỏ; Phụ lục B thêm tính liên tục của $F$; câu tùy chọn "(G1) trên $W$ buộc $F$ lồi" thêm ở Bước 3.

**R3 (10 mục nhẹ):** tất cả áp dụng. Câu mở đầu nêu đối tượng so sánh; câu "bảo đảm cho một thuật toán cụ thể, không phải cho lớp (Nhận xét 01.21)" ở □ Hệ quả 05.19 (đã kiểm Nhận xét 01.21 nói về độ phức tạp mẫu của thuật toán và của lớp); §14 đối tượng so sánh viết theo R3; Bài tập 05.12 "thêm tính lồi mạnh"; mức sàn sai số chỉ phát biểu cho $F=\tfrac a2w^2$; câu cuối §10; $\xi$ là dãy lần rút; tiêu đề Bổ đề 05.12; Mệnh đề 05.5; tên $\operatorname{opt}_S$.

**R4 (21 mục nhẹ, #15–#35):** áp dụng #15 (dòng dẫn "Theo kì vọng theo $\xi_1,\ldots,\xi_{T-1}$" trước công thức; Nhận xét 05.17 có **Giả thiết.**/**Bảo đảm.**), #16 (tiếng Anh lần đầu: empirical risk, population risk, squared loss, logistic regression, 0–1 loss, $\sigma$-algebra, least squares, almost surely, law of large numbers, parallelogram law; câu điểm dừng), #17 (tối thiểu hóa, giá trị nhỏ nhất), #18 ($s$ là mẫu cố định), #19 (khai triển $\lVert a-a'\rVert^2$; $\gamma$ ở Ví dụ 05.8; câu ôn nhanh 3 dùng $q_i$; điểm bị chiếu $\theta$), #20 ("cách dùng dữ liệu"; "quỹ đạo" có chú giải; "quan sát" trong phép đếm chi phí), #21, #22 (tách đoạn mở đầu, đoạn phản ví dụ phép chiếu, cầu nối), #23 (bỏ "Ta có" mở bước ở Ví dụ 05.2, 05.6; "Cần tìm"), #24 (câu dẫn Định nghĩa 05.1, 05.6, 05.10), #25 (kết luận Ví dụ 05.1, 05.8; Ví dụ 05.10 có **Kết luận.**; nhãn "**Bước k: tên.**" thống nhất ở Ví dụ 05.6, 05.12, 05.16), #26 (câu 322 viết lại; câu 807 cắt theo C2), #27 (mức sàn; câu song song; □ Phụ lục C), #28 (thêm bước trung gian ở câu ôn nhanh 3, Ví dụ 05.2, 05.4, 05.8, 05.9, 05.10, 05.11, 05.13, 05.15, câu hỏi cuối buổi), #29 (câu đọc nghĩa sau Định nghĩa 05.4 và 05.6), #30 (tiêu đề §8 "Vai trò của từng giả thiết"), #31 (mục tiêu 2 mở bằng "Phát biểu"; ghi chú cho người viết bài tập ở `outline.md` §13), #32 (như M10), #33 (câu sau Thuật toán 05.11), #34 ("Lấy kì vọng theo $\xi$:"), #35 (640.000 và 27.136 ngoài công thức; $6{,}4\cdot10^{5}$ trong công thức). Câu dài (#10): như M15 #10.

**R5 (12 mục nhẹ):** tất cả áp dụng. Ví dụ 05.1 trỏ §6; C1; Ví dụ 05.13 có $W$; Ví dụ 05.15 ghi $m$ là giả định, khác §3; §11 ghi ngữ cảnh ví dụ hồi quy; "(error floor)" chuyển lên □ Định lý 05.14; câu Lipschitz ở đoạn sau Hệ quả 05.19 ("hàm lỗi lồi và Lipschitz", không thêm câu mới, theo QĐ D); tiên quyết thay Nhận xét 01.2 bằng (T1); §1 câu mở; câu mở §9; giữ các nhắc Bài 06 ở chú thích $\lambda$ và phạm vi; giữ liên kết `exercises.md` (QĐ D).

## Số mới hoặc đổi (tính lại trong `l05_edit_num1.py`)

| Số | Chỗ | Giá trị máy |
|---|---|---|
| $g_3$: $(-0{,}5858;0)$, $(0;0{,}5858)$, $(-0{,}1697;-0{,}2263)$; chuẩn trước chiếu $1{,}2247$, $1{,}2247$, $0{,}9899$ | Ví dụ 05.6 Bước 3 | khớp R1, R2 |
| $(0{,}8330;-0{,}7670)$, chuẩn $1{,}1324$, chiếu $(0{,}7356;-0{,}6774)$, $L_S=0{,}06136$ | Ví dụ 05.6 Bước 4 | khớp R2 |
| $0{,}0034$; $0{,}1764$; $\tfrac\eta2\lVert g\rVert^2=1$ | Ví dụ 05.7 | $0{,}003437$; $0{,}176434$ |
| $4{,}000625$ (thay $4{,}0006$); $0{,}2281$ (thay $0{,}2280$/$0{,}228$ khi là cận) | Ví dụ 05.8, Nhận xét 05.17, §11 | $4{,}000625$; $0{,}2280087$ làm tròn lên |
| $-0{,}0056=\bar w_{1600}+1$; $-s^2+4s+0{,}5$ | Ví dụ 05.10 | $-0{,}005625$ |
| $0{,}7=1-0{,}3$; $-1{,}7=1-2{,}7$; $\mathbb Ea_t^2=1{,}69$; $12{,}81/\sqrt T$ | Ví dụ 05.11 | $\sqrt{164}=12{,}806$ |
| $G=4$ trên $[-1,1]$; $(w-0{,}5)^2+0{,}25$; $(w-0{,}1)^2+0{,}09$ | Ví dụ 05.13 | khớp R2 |
| $T(4)=\lceil100\cdot4{,}75\rceil=475$ | Ví dụ 05.15 | 475 |
| $0{,}9875^{1600}\approx1{,}8\cdot10^{-9}$ | câu hỏi cuối buổi | $1{,}817\cdot10^{-9}$ |
| $\pi-u\approx(-0{,}2929;-0{,}7071)$, $0{,}0858+0{,}5$; $0{,}0858-0{,}2071$ | Ví dụ 05.4 | khớp |
| $\operatorname{Var}=\tfrac13(\tfrac49+\tfrac{16}9+\tfrac49)=\tfrac89$ | câu ôn nhanh 3 | khớp |

## Không áp dụng

- **Mục tiêu 1 tách hai câu (R4 #10, #23):** QĐ M8 giữ nguyên Mục tiêu 1.
- **Cắt gradient (gradient clipping):** bỏ khỏi ghi chú thay vì định nghĩa (R1 cho phép một trong hai); thuật ngữ vẫn ở `thuat-ngu.md`.
- **Đánh số riêng cho bất đẳng thức lồi hữu hạn (R4 #15, phần cuối):** giữ văn xuôi để không đổi số khối, như R4 chấp nhận.
- **Thêm nguồn cho bổ đề đóng băng (R4 #14):** không thêm, theo QĐ M15.

## Cho người rà lại

Xem trước: Ví dụ 05.6 Bước 3–4 (dòng 570–580); Bổ đề 05.12, câu nối và Bước 3 viết lại (610–638); Định lý 05.14, Bước 3 và đoạn sau chứng minh (735–760); Ví dụ 05.10 Bước 5 và Kết luận (912–918); Ví dụ 05.13 (950–958); §11 (1113–1127); N1 ở §2 (101–104), Định nghĩa 05.18 và Hệ quả 05.19 (968–990). Đổi kí hiệu cần điều phối viên ghi vào `ky-hieu.md`: $\theta$ (điểm bị chiếu, §5), $U$ (tập ở Mệnh đề 05.5), $k_{1:t-1}$, $\Phi$, $\bar\Phi$ (Phụ lục B), $\gamma$ (Ví dụ 05.8), $q_i$ (câu ôn nhanh 3), $a'$ (khai triển).

## Vòng 2 (2026-10-31): sửa theo `reviews/6-ra-lai-toan.md` và `reviews/7-ra-lai-mach.md`

**Kết quả kiểm tra:** thân bài $11\,973$ tiếng, phụ lục $1\,182$; `forward_refs.py` báo 0 (một tham chiếu tới trước mới, "Ví dụ 05.3" ở dòng 154, đã sửa thành "kiểm ở §4 và Bài tập 05.8"); đồng bộ rồi `--check` OK; 52/52 khối; không chữ có dấu trong `\text{}`; render `file://` 390 px không lỗi KaTeX, không tràn. Kịch bản: `scratchpad/py/l05_edit_r2.py`, `l05_edit_r2b.py`, `l05_edit_r2c.py`. Không có số mới cần tính; $0{,}140625$ in đúng giá trị.

**Quy ước "mức sàn sai số":** tên này (kèm "error floor") chỉ dùng cho mức dao động thật của điểm lặp cuối (dòng 962, Bài tập 05.6). Số hạng $\eta G^2/2$ của cận gọi là "mức sàn $\eta G^2/2$ của cận" (dòng 755) hoặc "số hạng $\eta G^2/2$ của cận" (Ví dụ 05.12, dòng 947).

| Phát hiện | Nguồn | Trạng thái | Dòng mới |
|---|---|---|---|
| Câu cuối §6 khẳng định không điều kiện | R6 trung bình, R7 trung bình, QĐ 1 | áp dụng: "Theo kì vọng có điều kiện, bình phương khoảng cách tới một điểm $u\in W$ giảm ít nhất $2\eta(F(w_t)-F(u))$, trừ số hạng $\eta^2G^2$ (§7)." | 642 |
| Câu cuối §4 lệch M8 | R7 trung bình, QĐ 2 | áp dụng: dưới gradient cho cận dưới toàn cục theo định nghĩa; tính lồi bảo đảm tồn tại và gradient là một dưới gradient (Mệnh đề 05.3(a)) | 362 |
| □ Mệnh đề 05.13 "bậc hai theo độ dài bước" | R7 nhẹ, QĐ 3 | áp dụng: "trừ số hạng $\tfrac\eta2\lVert g\rVert^2$" | 680 |
| "Mức sàn sai số" hai nghĩa | R6 nhẹ, QĐ 3 | áp dụng theo quy ước trên | 755, 947, 962 |
| $0{,}1406$ làm tròn xuống | R6 nhẹ, QĐ 4 | áp dụng: in $0{,}140625$ ở Ví dụ 05.10 (Bước 2, Bước 4) và §11 | 896, 900, 1121 |
| (G1) buộc $F$ lồi không có lý do | R6 nhẹ | áp dụng: nửa câu về hai bất đẳng thức dưới gradient tại $\alpha w+(1-\alpha)w'$ | 739 |
| §9 câu đầu: $\operatorname{opt}_S$ là độ chênh, không phải $F(\bar w_T)$ | R6 nhẹ | áp dụng | 966 |
| Định nghĩa 05.18: $s$ cố định so với đo được theo bộ ba | R6 nhẹ | áp dụng: "đo được theo bộ ba, với $s$ chạy trên $\mathcal Z^m$" | 969 |
| $P_\xi$ hai nghĩa ở dòng 974 | R6 nhẹ | áp dụng: giữ $P_\xi$ của Định nghĩa 05.18 cho toàn bộ $\xi$; ở đoạn sau viết "phân bố tích của $T-1$ lần rút theo phân bố của Định nghĩa 05.10" | 974 |
| Lớp hàm điểm số nhận giá trị trong $\mathbb R$ | R7 nhẹ | áp dụng | 974 |
| (C) đi vào "một bước" | R7 nhẹ | áp dụng: "đi vào những bước đã ghi trong chứng minh" | 883 |
| §9 không kết bằng văn xuôi | R7 nhẹ | áp dụng: đoạn "Mức (O2) …" chuyển xuống sau Ví dụ 05.14 | 1037 |
| §3 dùng "hàm lồi" trước §4 | R7 nhẹ | áp dụng: "theo nghĩa của §4 (kiểm ở §4 và Bài tập 05.8)" (không dẫn Ví dụ 05.3 để giữ `forward_refs` = 0) | 154 |
| Lý do $\lambda$ trùng kí hiệu | R7 nhẹ | áp dụng | 360 |
| Định nghĩa 04.1 vào tiên quyết | R7 nhẹ | áp dụng | 40 |
| Nhãn danh sách sau Định nghĩa 05.10 | R7 nhẹ | áp dụng: "Phân bố rút không đều"; dòng ba thêm "nên $g_t$ không có dạng $\varphi(w_t,\xi_t)$" | 502–504 |
| Câu dài 17, 304, 962 | R7 nhẹ | áp dụng: tách cả ba | 17, 304, 962 |
| "Chặt ngặt" | R7 nhẹ | áp dụng: "ngặt: $1{,}3289<1{,}5019$" | 695 |
| Số lớn trong bảng Ví dụ 05.15 và §11 | R7 nhẹ | áp dụng: $2{,}7136\cdot10^4$ trong bảng; $1600$ và $6{,}4\cdot10^5$ trong công thức ở §11 | 1093, 1117 |
| Cắt K1–K7 | R7 §6 | áp dụng cả bảy (khoảng 107 tiếng); §10 kết bằng câu giới hạn | 775, 843, 870, 179, 474, 1098, 1111 |

Không có phát hiện nào không áp dụng.

## Vòng 3 (2026-10-31): `reviews/8-ra-lai-vong-2.md`, cách in số lớn, công thức tràn ở 390 px

**Kết quả kiểm tra:** thân bài $11\,984$ tiếng, phụ lục $1\,189$; `forward_refs.py` báo 0; đồng bộ rồi `--check` OK; 52/52 khối. Đầu dò `final05/probe.py` ở 390×844 (mở mọi khối thu gọn): **0** phần tử tràn (trước: 43 công thức). Ở 1600×900: 0 công thức có cuộn ngang, 0 lỗi KaTeX, 0 lỗi console; ảnh `final05/wide1600.png` bình thường. Kịch bản: `final05/probe_tex.py` (lấy mã TeX của công thức tràn), `final05/new_tex.txt` và `final05/apply_tex.py` (thay 43 công thức), `py/l05_edit_r3.py`, `l05_edit_r3b.py`, `l05_edit_r3c.py`.

| Phát hiện | Trạng thái | Dòng mới |
|---|---|---|
| Dòng 642: "giảm ít nhất $2\eta(F(w_t)-F(u))-\eta^2G^2$ (§7)" | áp dụng | 681 |
| Dòng 755: "về số hạng $\eta G^2/2$ của cận"; "mức sàn" chỉ còn ở mức dao động thật (cuối §8) và §12 | áp dụng | 802 |
| Dòng 966: "(khi $\lVert w_1-u\rVert\le R$ với mọi $u\in W$)" | áp dụng | 1026 |
| Dòng 154: "§4" lặp | áp dụng: "(định nghĩa và kiểm tra ở §4 và Bài tập 05.8)" | 158 |
| Câu dài 739, 974 | áp dụng: tách trước "Ngược lại"; tách "Đầu ra là $A(S;\xi)=\bar w_T$, …" | 786, 1034 |
| Cách in số lớn | áp dụng: $640\,000$ (Ví dụ 05.14 và §11), $4\,000\,000$ (Ví dụ 05.14, hai chỗ), $27\,136$ (bảng Ví dụ 05.15); giữ $10^4$, $10^6$, $10^{10}$ (lũy thừa tự nhiên) và $1{,}8\cdot10^{-9}$ (số thập phân nhỏ) | 1090, 1095, 1157, 1181 |
| 43 công thức tràn ở 390 px | áp dụng: viết lại theo kiểu Bài 04 (`aligned` nhiều dòng, dòng tiếp mở bằng `&\quad=`/`&\quad\le`/`&\qquad+`; hai công thức độc lập ghép bằng dấu phẩy thành hai dòng của một `aligned`); không đổi nội dung toán học | toàn bài |

**Cắt để giữ ngân sách** (các dòng `aligned` thêm khoảng 60 tiếng theo `wc -w`): đoạn (O1)/(O2) ở cuối §2 (ý đã có ở câu mở §9), một nửa lộ trình chứng minh Mệnh đề 05.5, vế "$\mathcal F_t$ luôn có chỉ số …" sau Định nghĩa 05.10, câu dẫn Bước 3 của Ví dụ 05.6 viết ngắn, câu cuối Ví dụ 05.12 ("một bước theo dưới gradient …"; trỏ §8 của nó đã bị cắt ở vòng 2). Không có phát hiện nào không áp dụng.
