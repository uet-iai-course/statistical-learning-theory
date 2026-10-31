# Rà lại 5 — Mạch, móc nối và văn phong sau biên tập vòng 1, Bài 06

Người rà: tác tử rà mạch và móc nối, chỉ đọc. Đối tượng: `scratchpad/lec06-r1-frozen.md`, trùng `2627-1/materials/lec-06/lecture-note.md` hiện tại (`diff -q` rỗng), 1301 dòng, thân bài 11 974 tiếng (`wc -w` đến trước `## Phụ lục`). Căn cứ: `lec06-r1.udiff`, `reviews/0-quyet-dinh.md`, `bien-tap-vong-1.md`, `reviews/4-hoc-thuat-van-phong.md`, `reviews/5-mach.md`. Văn phong kiểm theo `no-ai-slop` chế độ Detect và `van-phong.md` §7a, §8, §9, §9a, §12. Số dòng dưới đây là số dòng của `lec06-r1-frozen.md`.

**Tổng kết:** phát hiện cũ: 20/20 của R5 đã xử lý (18 ✓, 1 một phần, 1 ✗ có lý do chấp nhận được); 11/11 phát hiện trung bình của R4 ✓. Phát hiện mới: 0 `chặn bàn giao` · 0 `nghiêm trọng` · 1 `trung bình` · 15 `nhẹ`.

## 1. Define-before-use

`forward_refs.py` chạy từ gốc repo trên bản sao `scratchpad/reviews06/r5b/lec-06/lecture-note.md` (byte-giống bản rà): **0 forward references**.

Kiểm tay các kí hiệu và thuật ngữ mới hay đổi:

| Kí hiệu / thuật ngữ | Lần dùng đầu (thân bài) | Định nghĩa | Kết luận |
|---|---|---|---|
| rủi ro vượt mức kì vọng | 242 (30–34 là mục tiêu, được miễn) | 242, tại chỗ, kèm Định nghĩa 01.24, 04.1 | ✓; dùng nhất quán ở 286, 361, 436, 901, 937, 1064, 1131 |
| cấp thuật toán / cấp lớp | 242 | 242 | ✓; dùng lại 644 |
| lập luận đổi vai (exchange argument) | 626 (32 là mục tiêu; 117 chỉ dùng động từ "đổi vai") | 626, nhắc lại ở lộ trình 648 | ✓ |
| tăng trưởng bậc hai (quadratic growth) | 461 | 461 | ✓ |
| thuật toán hằng (constant algorithm) | 718 | 718 | ✓ |
| bất đẳng thức oracle (oracle inequality) | 903 (tiêu đề Hệ quả 06.13) | 937, kèm câu giải thích mốc | ✓; câu 937 cần sửa văn phong (M9) |
| $W_B$ | 112 (bảng §2, có con trỏ "§9") | 928 | ✓ chấp nhận được; `ky-hieu.md` dòng 71 đã có |
| $B$, $R$ | 97 (bảng §1, có con trỏ "§2") | 112–113 | ✓ |
| $\hat w$, $\hat w'$ | 769 | 769 (chứng minh Mệnh đề 06.11); 815 (Ví dụ 06.6); 1186 (Phụ lục B) | Ví dụ 06.7 dùng lại ở 848 mà không nói hai chữ chỉ gì (M6). Dòng 570 dùng $\hat w$ cho công thức một chiều, cùng nghĩa $\hat w_s$, không xung đột |
| số hạng ổn định / số hạng khớp | 901 ("số hạng khớp" = $\mathbb E[L_S(\hat w_S)-L_S(u)]$) | 937 (= các số hạng của cận) | Hai nghĩa, xem M1 |
| $C_0$ | 891 | 891 | ✓ |

## 2. Phát hiện cũ

### 2a. Của tôi (`5-mach.md`)

| Mã | Phát hiện | Trạng thái | Bằng chứng trên bản mới |
|---|---|---|---|
| T1 | Hệ quả 04.17 cần (T3) | ✓ | 1051: "Khi hàm lỗi nhận giá trị trong $[0,1]$ (giả thiết (T3) của Hệ quả 04.17) …; Với hồi quy logistic, việc chọn … dùng một hàm lỗi bị chặn"; 1068: "Khi $B$ chưa biết và hàm lỗi bị chặn" |
| T2 | Báo trước Bài 08 thiếu điều kiện | ✓ | 620, 1134, 1299: "với hàm lỗi lồi, trơn và Lipschitz"; 1075 chỉ nói "chưa được chặn trong bài" |
| T3 | Hai nghĩa của $B$; thiếu $R$ | ✓ | 90 không còn $B$; 112–113; 972 "$W_B=W$ với $B=1$" |
| T4 | §10 không trả lời câu hỏi trung tâm | ✓ | 1064, hai câu đầu |
| N1 | Câu kết §3 | ✓ (đã cắt) | §3 kết bằng khối ứng dụng; §4 mở bằng vấn đề (178) |
| N2 | Hai "mẫu bốn quan sát" | ✓ | 390 "khác mẫu cố định của Ví dụ 06.1" |
| N3 | "Quan sát kiểm tra" ngẫu nhiên ở §1 | ✓ | 102 |
| N4 | $\bar w_T$, $g_t$ chưa gọi tên | ✓ | 20, 304 |
| N5 | "(§4)" mơ hồ; (O1) cho $F_{S,\lambda}$; Phụ lục A | một phần | 119 ✓. Phụ lục A giữ "§4 của Bài 05" với lý do Mệnh đề 05.3(a) chỉ cho trường hợp khả vi; lý do hợp lệ |
| N6 | Tiếng Anh ở lần đầu | ✓ | 461, 626, 718, 937 |
| N7 | "Mọi lập luận còn lại" | ✓ | 461 |
| N8 | Câu kết §6 | ✓ (đã cắt) | xem M5 |
| N9 | Chỉ số $\mathbb E_S$ | ✓ | 955–957, 1009 |
| N10 | Ví dụ 06.11 Bước 3 | ✓ | 1011–1018; 1022 trả lời câu hỏi thực hành của §3 |
| N11 | Hình 06.1 chưa được dẫn | ✓ | 580 "(Hình 06.1)" |
| N12 | $c_s$ ở Phụ lục D | ✓ | 1257–1273 |
| N13 | Cầu nối lặp §10; "bằng chính $L_D$" | ✓ | 1134 |
| N14 | Lời hứa "nhãn hiếm" của Nhận xét 02.11 | ✗ | không áp dụng vì hết ngân sách; đề xuất vốn là tùy chọn, chấp nhận |
| N15 | Thuật toán hằng nêu hai lần | ✓ | câu ở 618–624 đã bỏ |
| N16 | $W_B$ trong `ky-hieu.md` | ✓ | `ky-hieu.md` dòng 71 |

### 2b. Phát hiện trung bình của R4 (`4-hoc-thuat-van-phong.md`)

| R4 | Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|---|
| 1 | Tiếng Anh cho bốn thuật ngữ; câu giải thích "bất đẳng thức oracle" | ✓ | 461, 626, 718, 937 |
| 2 | Đặt tên "lập luận đổi vai" | ✓ | 626, 648 |
| 3 | "Cấp thuật toán" chưa định nghĩa | ✓ | 242 |
| 4 | Trùng $v$ | ✓ | 769–796, 815–831, Phụ lục B |
| 5 | Tiêu đề Bài tập 06.7 dạng "Từ … sang …" | ✓ | 1089; phạm vi tiêu đề mới hẹp hơn nội dung (M10) |
| 6 | "Rủi ro thực nghiệm kì vọng" | ✓ | 73 "kì vọng của rủi ro thực nghiệm" |
| 7 | Ví dụ thuật toán ghi nhớ trong một câu 58 tiếng | ✓ | 622, ba câu |
| 8 | Câu cuối dòng 703 lắt léo | ✓ | 715 |
| 9 | Ví dụ 06.5 hai thiết lập | ✓ | 718–731, một thiết lập, công thức nhị thức, lý do $1/\sqrt{2\pi m}$ |
| 10 | Ví dụ 06.3 Bước 3 bỏ bước | ✓ | 403–412; câu dẫn sang Bước 4 cần sửa nhẹ (M11) |
| 11 | Dòng 122 "hàm lỗi log" | ✓ | 117 |

## 3. Mạch sau 13 chỗ cắt

- **Câu kết các mục.** §4 (300), §5 (439), §7 (736) giữ câu kết dẫn sang mục sau. §3 kết bằng khối ứng dụng, §6 bằng chú thích Hình 06.1, §8 bằng Nhận xét 06.12, đều do cắt theo R4 (điều phối viên chấp nhận). Câu mở của §4 (178), §7 (591) và §9 (901) nêu lại vấn đề, nên mạch không đứt; mục 3 nguyên tắc (iii) của `outline.md` cần ghi nhận thay đổi này (M5). §9 kết bằng một câu đứng riêng (1060) lặp ý Nhận xét 06.15 và mục "Nghiệm chính xác" của §10 (M4).
- **Câu mở §7 (591).** Sau khi câu đối chiếu với Bài 02–04 bị cắt, "Ở đây, ta chỉ dùng …" không còn vế để so sánh (M3).
- **Câu hỏi mở đầu và §10.** §10 mở bằng câu trả lời câu hỏi trung tâm (1064), rồi số của câu hỏi mở đầu. Con số $0{,}0011$ (sai số tối ưu thực nghiệm), vốn là nửa còn lại của câu trả lời ở dòng 22, không còn trong §10; "chủ yếu do khoảng cách tổng quát hóa kì vọng" không đúng về độ lớn, vì $0{,}4750>0{,}2261$ (M2).
- **Lời hứa và cầu nối.** Bài 01 dòng 913 → 715; Bài 02 dòng 574 → 896, 1022; Bài 05 dòng 1100, 1254 → §4–§9, 1064. Cầu nối Bài 07 (1134) khớp blueprint 6.6 và 7.1; câu báo trước Bài 08 khớp blueprint 8.1–8.2. 1077 viết "không lồi", còn 1134 viết "nói chung không lồi" và dẫn §10 (M8).
- **Các chỗ cắt khác** (tiên quyết chỉ còn số hiệu, câu sau Định nghĩa 06.4, Mệnh đề 06.5, Bổ đề 06.7, các câu thiết lập của Ví dụ 06.9–06.11, §13 mục "Tập tham số"): không mất câu dẫn, không có tham chiếu treo. Riêng "Bước 1–3 là các đẳng thức" (713, 1295) không còn đúng hẳn, vì Bước 2 nay có thêm một chuỗi bất đẳng thức chứng minh tính hữu hạn (M7).

## 4. Số bài tập UML

§11 (1089–1093) và `outline.md` (343–347) nhất quán: UML Bài tập 13.1, 13.2, 13.3, 14.1, 13.4 (ý 1–3). §13 (1139) dẫn "các bài tập UML §13.7, §14.8", khớp. Không còn "14.8.1" trong ghi chú. Tiêu đề mới của Bài tập 06.7 hẹp hơn nội dung dự kiến (M10). Tiêu đề Bài tập 06.9 viết "Ổn định theo trung bình", khác thuật ngữ đã chốt (M10).

## 5. Phát hiện mới

| Mã | mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|---|
| M1 | trung bình | 901, 937, 1036 | "Số hạng khớp" và "số hạng ổn định" mang hai nghĩa: ở 901, "số hạng khớp" là đại lượng thật $\mathbb E[L_S(\hat w_S)-L_S(u)]$; ở 937, hai tên chỉ hai số hạng của cận, $2G^2/(\lambda m)$ và $\tfrac\lambda2\lVert u\rVert^2$. Câu kết Ví dụ 06.12 vì thế phát biểu sai: $W=\mathbb R$ với hàm lỗi bình phương không có $G$ hữu hạn, nên "số hạng ổn định" theo nghĩa 937 không xác định; đại lượng bằng $0$ là khoảng cách tổng quát hóa. | 901: "cộng số hạng khớp $\mathbb E[L_S(\hat w_S)-L_S(u)]$"; 937: "Hai số hạng là *số hạng ổn định* $2G^2/(\lambda m)$ và *số hạng khớp* $\tfrac\lambda2\lVert u\rVert^2$"; 1036: "Rủi ro tăng theo $\lambda$ trong khi số hạng ổn định đã bằng $0$." | 901: "… là khoảng cách tổng quát hóa kì vọng cộng $\mathbb E[L_S(\hat w_S)-L_S(u)]$." (−2 tiếng). 1036: "Rủi ro tăng theo $\lambda$ trong khi khoảng cách tổng quát hóa bằng $0$." (+1). Giữ hai tên cho các số hạng của cận như 937, 1011, 1253. |
| M2 | nhẹ | §10, 1064 câu cuối | "chủ yếu do khoảng cách tổng quát hóa kì vọng" không đúng về độ lớn: khoảng cách $0{,}4750$ lớn hơn rủi ro vượt mức $0{,}2261$, vì số hạng giữa âm. Câu cũng bỏ mất con số $0{,}0011$, nửa còn lại của câu trả lời ở dòng 22 (cận $0{,}1$ chỉ chặn sai số tối ưu thực nghiệm). | "… và $0{,}2261$ khi dùng lại bốn quan sát, chủ yếu do khoảng cách tổng quát hóa kì vọng (Ví dụ 06.3)." | "… và $0{,}2261$ khi dùng lại bốn quan sát, dù kì vọng của sai số tối ưu thực nghiệm chỉ là $0{,}0011$ (Ví dụ 06.3)." (+4) |
| M3 | nhẹ | §7, 591 | Sau khi câu đối chiếu với Bài 02–04 bị cắt, "Ở đây, ta chỉ dùng" không còn vế để so sánh (no-ai-slop: câu chuyển ý thiếu căn cứ). | "Mệnh đề 06.5 cần một cận … Ở đây, ta chỉ dùng một tính chất của chính thuật toán: …" | "Cận dưới đây không dùng cấu trúc của lớp, chỉ dùng một tính chất của chính thuật toán: …" (+3) |
| M4 | nhẹ | §9, 1060 | Câu đứng riêng cuối §9 lặp ý Nhận xét 06.15 (ngay trên) và mục "Nghiệm chính xác" của §10 (1073); không dẫn sang §10. | "Cận $2GB/\sqrt m$ dành cho nghiệm chính xác của ERM có chính quy hóa." | Cắt (−11). §10 mở bằng câu trả lời câu hỏi trung tâm nên không cần câu dẫn. |
| M5 | nhẹ | §3, §6, §8 (kết mục); `outline.md` §3 | Ba mục nay kết bằng khối hay chú thích hình, không bằng câu văn xuôi (`van-phong.md` §8; nguyên tắc (iii) của dàn ý). Câu mở của mục sau gánh phần dẫn, nên mạch vẫn liền. | Cuối §6: chú thích Hình 06.1 (587); cuối §8: Nhận xét 06.12 (897). | Không sửa ghi chú. Ghi vào `outline.md` §13 rằng câu kết §3, §6, §8 được cắt theo R4 và phần dẫn chuyển sang câu mở §4, §7, §9. |
| M6 | nhẹ | Ví dụ 06.7 Bước 3, 845–849 | $\hat w$, $\hat w'$ là kí hiệu cục bộ của chứng minh Mệnh đề 06.11 ($\lambda>0$). Ví dụ 06.7 ($\lambda=0$) dùng lại mà không nói chúng chỉ gì. | "Cộng hai bất đẳng thức … rồi dùng (L) như Bước 2–3: $\tfrac2m\lvert\hat w-\hat w'\rvert^2\le…$" | "Với $\hat w$, $\hat w'$ là hai nghiệm ERM, cộng hai bất đẳng thức …" (+7) |
| M7 | nhẹ | 713; Phụ lục E 1295 | Sau sửa C1, Bước 2 có thêm một chuỗi bất đẳng thức (chứng minh tính hữu hạn), nên "Bước 1–3 là các đẳng thức" không còn đúng nguyên văn. | 713: "Bước 1–3 là các đẳng thức, nên …"; 1295 cùng câu. | "Các đẳng thức ở Bước 1–3 cho thấy …" (+2 ở 713; phụ lục ngoài trần). |
| M8 | nhẹ | §10, 1077 | Lệch với cầu nối 1134, vốn dẫn chính §10: một bên viết "không lồi", bên kia "nói chung không lồi". | 1077: "hàm lỗi của mạng nơ-ron theo trọng số không lồi"; 1134: "nói chung không lồi (§10)". | 1077: "… theo trọng số nói chung không lồi, …" (+2) |
| M9 | nhẹ | Hệ quả 06.13, 937 | Câu thiếu động từ chính, dựng theo kiểu "nhãn: tiết lộ" (no-ai-slop: colon reveal; `van-phong.md` §9a). | "Tên *bất đẳng thức oracle* (oracle inequality) theo Bài 04: phần (b) so đầu ra với mốc …, mốc chỉ tính được khi biết $D$." | "Theo cách gọi của Bài 04, phần (b) là một *bất đẳng thức oracle* (oracle inequality): nó so đầu ra với mốc $\inf_u[\ldots]$, và mốc này chỉ tính được khi biết $D$." (+6) |
| M10 | nhẹ | §11, 1089, 1091; `outline.md` 343, 345 | (i) Tiêu đề Bài tập 06.7 nói "cho ERM có chính quy hóa", nhưng bài (dàn ý 343(a)–(b)) phát biểu cho một thuật toán bất kì có cận kì vọng trên $\mathcal H$. (ii) Tiêu đề Bài tập 06.9 viết "Ổn định theo trung bình", khác thuật ngữ đã chốt "ổn định thay một theo trung bình" (`thuat-ngu.md` dòng 338; Phụ lục E 1287). | 1089: "(Cận với xác suất cao và tăng độ tin cậy cho ERM có chính quy hóa; …)"; 1091: "(Ổn định theo trung bình và gần đúng ERM …)". | (i) "Cận với xác suất cao và tăng độ tin cậy từ một cận kì vọng", hoặc giữ tiêu đề nếu người viết bài tập đặt bài cho ERM có chính quy hóa (±0). (ii) "Ổn định thay một theo trung bình và gần đúng ERM theo kì vọng đủ cho học" (+2). Đồng bộ `outline.md`. |
| M11 | nhẹ | Ví dụ 06.3, 413 | Chủ thể trừu tượng làm việc của người (`van-phong.md` §9a). | "Bước 4 cần thêm mô-men chéo." | "Ở Bước 4, ta cần thêm mô-men chéo." (+2) |
| M12 | nhẹ | Nhận xét 06.14, 1051 | Câu đầu khoảng 50 tiếng, nhiều mệnh đề phụ, thiếu chủ ngữ ("có thể chia") (`van-phong.md` §9). | "Khi hàm lỗi nhận giá trị trong $[0,1]$ (…), có thể chia mẫu thành $k=…$ khối độc lập, mỗi khối đủ cho mức kì vọng $\epsilon/4$, rồi chọn đầu ra bằng một mẫu xác thực cỡ … (Hệ quả 04.17, Bài tập 06.7)." | Tách: "Khi hàm lỗi nhận giá trị trong $[0,1]$ ((T3) của Hệ quả 04.17), ta chia mẫu thành $k=\lceil\log_2(2/\delta)\rceil$ khối độc lập, mỗi khối đủ cho mức kì vọng $\epsilon/4$. Ta chọn đầu ra bằng một mẫu xác thực cỡ $8\ln(4k/\delta)/\epsilon^2$ (Bài tập 06.7)." (−2) |
| M13 | nhẹ | §2, 117 | Câu cuối khoảng 45 tiếng, hai vế ghép bằng dấu chấm phẩy (`van-phong.md` §9). | "Các kết quả chính của bài không giả sử hàm lỗi bị chặn; hàm lỗi bình phương và hàm lỗi logistic … hay tính trơn (§8)." | Thay dấu chấm phẩy bằng dấu chấm: "… không giả sử hàm lỗi bị chặn. Hàm lỗi bình phương và …" (±0) |
| M14 | nhẹ | Ví dụ 06.9 Bước 4, 882 | "chọn $M=m$ làm nghiệm … dần về $0$" đọc được thành "chọn $M=m$ làm nghiệm". | "còn chọn $M=m$ làm nghiệm trên mẫu lân cận dần về $0$" | "còn với $M=m$, nghiệm trên mẫu lân cận dần về $0$ khi $m$ tăng" (+2) |
| M15 | nhẹ | Ví dụ 06.7 Kết luận, 854 | Một khẳng định ("lớp này vẫn có tính hội tụ đều") được dẫn tới bài sau làm căn cứ. | "Lớp này vẫn có tính hội tụ đều, vì dữ liệu và $W$ bị chặn (Bài 07)" | "(chứng minh ở Bài 07)" (+2), hoặc giữ nguyên nếu điều phối viên coi là lời báo trước. |
| M16 | nhẹ | Nhận xét 06.12, 896; §13, 1140 | 896: dấu hai chấm dựng "tiết lộ" (no-ai-slop). 1140: "§12.2.2: bài toán …" lệch định dạng ngoặc của các mục khác trong cùng danh sách. | 896: "cận là $192C_x^2C_y^2/(\lambda m)$: đây là giả thiết khác mà Nhận xét 02.11 hứa …"; 1140: "§12.2.2: bài toán lồi–Lipschitz–bị chặn (convex-Lipschitz-bounded problem)". | 896: "… cận là $192C_x^2C_y^2/(\lambda m)$. Dữ liệu bị chặn và tính trơn là giả thiết khác mà Nhận xét 02.11 hứa …" (+5). 1140: "§12.2.2 (bài toán lồi–Lipschitz–bị chặn, convex-Lipschitz-bounded problem)" (±0). |

## 6. Ngân sách (thân bài 11 974 / 12 000)

Các đề xuất thêm tổng khoảng +38 tiếng (M2 +4, M3 +3, M6 +7, M7 +2, M8 +2, M9 +6, M10 +2, M11 +2, M14 +2, M15 +2, M16 +5, M1 −1, M12 −2). Cắt M4 −11, nên tăng ròng khoảng +27 và vượt trần một ít. Chỗ cắt dự phòng: câu cuối Kết luận Ví dụ 06.4 (582), "Độ nhạy được chặn bằng $2G/(\lambda m)$ ở §8, và hai phía được cân ở §9." (−15), vì câu mở §8 (740) và §9 (901) đã nêu đúng hai ý này. Với cả hai chỗ cắt, thân bài khoảng 11 986 tiếng. Ưu tiên: M1, rồi M2, M3, M7, M10; các mục văn phong (M9, M11–M16) làm khi còn chỗ.
