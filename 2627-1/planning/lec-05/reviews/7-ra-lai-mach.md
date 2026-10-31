# Bài 05 — Rà lại mạch, móc nối và văn phong sau biên tập vòng 1

Số phát hiện: chặn bàn giao 0 · nghiêm trọng 0 · trung bình 2 · nhẹ 11.

Đầu vào: `2627-1/materials/lec-05/lecture-note.md` (1341 dòng, bản hiện tại; số dòng dưới đây là của bản này); `scratchpad/lec05-round1.diff`; `planning/lec-05/reviews/0-quyet-dinh.md`; `planning/lec-05/bien-tap-vong-1.md`; báo cáo `5-mach.md` của vòng trước; `van-phong.md` §2, §3a, §7a, §8, §9a, §12; ghi chú Bài 01, 03, 04 (grep). Văn bản rà theo `no-ai-slop` chế độ Detect: trích câu, đề xuất sửa, không viết lại cả đoạn.

**Kiểm tra đã chạy.** `python3 ../tools/courses/statistical-learning-theory/scripts/forward_refs.py 2627-1/materials/lec-05/lecture-note.md` → **`0 forward references`**. Thân bài `wc -w` trước `## Phụ lục`: **11 988**. Câu dài hơn 40 tiếng (đếm bằng `split()`, script `scratchpad/py/r05_mach_long.py`, đối chiếu với bản đóng băng để tách câu mới): dòng 17, 151, 304, 962 là câu mới hoặc câu đã sửa; dòng 25 (Mục tiêu 1) giữ theo QĐ M8.

## 1. Đối chiếu 17 phát hiện của vòng trước

| # | phát hiện vòng trước | trạng thái | dòng hiện tại |
|---|---|---|---|
| T1 | "Không" ở câu trả lời mở đầu | ✓ | 15: "Không nhất thiết, kể cả theo kì vọng." |
| T2 | "Độ chênh tối ưu" không có công thức; nhiều tên cho $\operatorname{opt}_S$ | ✓ | 83 (định nghĩa có công thức, liên hệ $\operatorname{opt}_S$); grep: không còn "sai số tối ưu" thiếu "thực nghiệm" (993, 1170, 1181, 1184) |
| T3 | "Số hạng nhiễu" | một phần | 642, 646 đúng; 680 gọi $\tfrac\eta2\lVert g\rVert^2$ là "số hạng bậc hai theo độ dài bước", xem bảng mục 3 |
| T4 | "Mô hình Lipschitz" | ✓ | 1111 |
| T5 | Câu chương trình rút quan sát mới ở §9 | ✓ | đã xóa; §13 (1186) giữ nội dung |
| N1 | Con trỏ "§5" cho ràng buộc $\lVert w\rVert\le1$ | ✓ | 137: "§6" |
| N2 | Đoạn tóm tắt cuối §8 | ✓ | §8 kết bằng dòng 962 (mức sàn, một giới hạn) |
| N3 | Ví dụ 05.13 thiếu $W$ | ✓ | 951: $W=[-1,1]$, $w_1=0$, $G=4$ |
| N4 | $m=10^4$ ở Ví dụ 05.15 | ✓ | 1081 |
| N5 | Ngữ cảnh cho $1600$, $640\,000$ ở §11 | ✓ | 1117: "Trong ví dụ hồi quy, theo các cận, …" |
| N6 | "Mức sàn" dùng trước khi đặt tên | ✓ | 755 "mức sàn sai số (error floor)"; 947, 962 dùng sau |
| N7 | Lời hứa Lipschitz của Bài 01 dòng 846 | ✓ | 1019: "cận thống kê cho hàm lỗi lồi và Lipschitz thuộc Bài 06–07" (QĐ D: không thêm câu) |
| N8 | Tiên quyết: Nhận xét 01.2 thừa, thiếu (T1) | ✓ | 36–38 (đổi sang Bài 02, nơi (T1) cũng được nêu lại; chấp nhận) |
| N9 | "Giữ tám thành phần" | ✓ | 75 |
| N10 | Câu mở §9 lặp dòng 3 | ✓ | 966 |
| N11 | Nhắc Bài 06 ngoài §13 | giữ theo QĐ | 360, 1019 |
| N12 | Liên kết `exercises.md` chưa có tệp | giữ theo QĐ D | 1131 |

**Danh sách cắt C1–C12:** cả 12 chỗ đã áp dụng (đã kiểm từng chỗ trên bản hiện tại): C1 (cuối §8), C2 (không còn câu tốc độ GD trơn trước Ví dụ 05.9), C3 (758, viết lại theo M8, ngắn hơn), C4 (1111), C5 (cả đoạn cuối §9), C6 (753 không còn câu Jensen), C7 (417), C8 (883, viết lại), C9 (947), C10 (993), C11 (113), C12 (§9). Hệ quả của C5 xem phát hiện về cuối §9.

## 2. Ranh giới các mục

| Mục | Câu mở (nhu cầu) | Câu kết (hệ quả/giới hạn) |
|---|---|---|
| Mở đầu, câu hỏi (3–19) | nêu câu hỏi của Bài 04 | 19: phạm vi $L_S$, hẹn §13 ✓ |
| §1 | 75 ✓ | 93 ✓ |
| §2 | 97 (câu dẫn bảng) ✓ | 113 ✓ |
| §3 | ví dụ | 154: dùng "hàm lồi" trước §4 (nhẹ, xem bảng) |
| §4 | 158 ✓ (0–1 không lồi, bản lề không khả vi) | 362: lệch QĐ M8 (trung bình, xem bảng) |
| §5 | 366 ✓ | 449 ✓ giới hạn: tính $\operatorname{proj}_W$ tổng quát là bài toán riêng |
| §6 | 453 ✓ | 642: khẳng định không điều kiện (trung bình, xem bảng) |
| §7 | 646 ✓ | 883 ✓ giới hạn, nối §8 (một chữ cần sửa, xem bảng) |
| §8 "Vai trò của từng giả thiết" | 887 ✓ (nhu cầu ở 883); tiêu đề là cụm danh từ, khớp nội dung (ba giả thiết bị bỏ, một đầu ra khác) | 962 ✓ giới hạn (mức sàn tỉ lệ với $\eta$), không còn đoạn tóm tắt |
| §9 | 966 ✓ (kì vọng so với hai mức tất định) | **không có câu kết văn xuôi**: mục kết bằng khối Ví dụ 05.14 (nhẹ, xem bảng) |
| §10 | 1041 ✓ | 1111 ✓ giới hạn; câu đầu lặp 1098 (cắt) |
| §11 | 1115 trả lời câu hỏi mở đầu ✓ | 1119–1123 đúng ba giả thiết; 1125 câu riêng về điểm lặp cuối ✓; 1127 giới hạn ✓, khớp M8 ("điều kiện của (G1) và của Bước 5") |
| §13 | câu hỏi không đổi; lời giải (c) tách sai số ước lượng (Định nghĩa 04.1) và sai số tối ưu thực nghiệm ✓ | 1184–1186: nêu câu hỏi cho Bài 06, chỉ gọi tên hai công cụ, không phát biểu kết quả nào của Bài 06 ✓ |

## 3. Phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | §4 cuối, dòng 362; so với QĐ M8 và dòng 735–739, 758, 1127 | Câu kết §4 vẫn mang cách đọc mà QĐ M8 đã sửa: một dưới gradient **theo định nghĩa** đã cho cận dưới toàn cục (Định nghĩa 05.2, dòng 191); tính lồi chỉ bảo đảm dưới gradient tồn tại và gradient là một dưới gradient. Dòng 739 nói đúng ("Bước này chỉ dùng (G1). Tính lồi của $F$ là điều kiện để (G1) thỏa được"), nên §4 và §7 nói hai điều khác nhau về vai của tính lồi, đúng chỗ Mục tiêu 1 kiểm tra. | "Tính lồi biến một dưới gradient tại $w$ thành một cận dưới toàn cục của $F$; cận $G$ trên chuẩn của dưới gradient chặn độ dài mỗi bước." | "Với $F$ lồi, gradient tại một điểm là một dưới gradient (Mệnh đề 05.3(a)), và mỗi dưới gradient cho một cận dưới toàn cục của $F$; cận $G$ trên chuẩn của dưới gradient chặn độ dài mỗi bước." (thêm khoảng 8 tiếng) |
| trung bình | §6 cuối, dòng 642 | Câu chuyển sang §7 khẳng định không điều kiện rằng bình phương khoảng cách tới **mọi** $u\in W$ giảm theo trung bình. Điều này chỉ đúng khi $F(w_t)>F(u)$ và cần thêm bất đẳng thức dưới gradient: theo Bước 1–3 của chứng minh, $\mathbb E\Delta_{t+1}\le\mathbb E\Delta_t-2\eta\,\mathbb E[F(w_t)-F(u)]+\eta^2G^2$. Với $u$ có $F(u)>F(w_t)$, khoảng cách có thể tăng theo kì vọng. Câu cũ (“§7 tìm một đại lượng…”) là lời hẹn; câu mới là một khẳng định sai ở dạng tổng quát. | "Gradient ngẫu nhiên không chệch khi biết lịch sử, nên bình phương khoảng cách tới một điểm $u\in W$ giảm theo trung bình, trừ một số hạng tỉ lệ với $\eta^2\lVert g_t\rVert^2$." | "…nên bình phương khoảng cách tới một điểm $u\in W$ giảm theo trung bình khi $F(w_t)>F(u)$, trừ một số hạng tỉ lệ với $\eta^2\lVert g_t\rVert^2$." (thêm 3 tiếng) |
| nhẹ | □ Mệnh đề 05.13, dòng 680 | Sau khi chia cho $2\eta$, số hạng $\tfrac\eta2\lVert g\rVert^2$ là bậc **một** theo $\eta$; bậc hai là $\eta^2\lVert g\rVert^2$ trước khi chia (dòng 646, 673). Tên gọi lệch với công thức đứng cạnh và với $\eta G^2/2$ "tỉ lệ với $\eta$" ở dòng 715. | "trừ số hạng bậc hai theo độ dài bước $\tfrac\eta2\lVert g\rVert^2$." | "trừ số hạng $\tfrac\eta2\lVert g\rVert^2$." (bớt 5 tiếng) |
| nhẹ | §7 cuối, dòng 883 | "(C) … đi vào một bước": theo chính chứng minh, (C) đi vào Bước 1 (tính lồi, tính đóng của $W$, dòng 725) và Bước 5 (tính lồi của $F$, $W$, dòng 749), và là điều kiện của (G1) (dòng 739). | "Mỗi giả thiết (C), (G1), (G2) của Định lý 05.14 đi vào một bước của chứng minh" | "…đi vào những bước đã ghi trong chứng minh" hoặc "ít nhất một bước". |
| nhẹ | §9, ranh giới với §10 (sau dòng 1036) | Sau cắt C5, §9 kết bằng khối Ví dụ 05.14, không có câu văn xuôi nêu hệ quả hay giới hạn (`van-phong.md` §8). Đoạn giới hạn của mục (dòng 1019: (O2) chỉ đạt với xác suất cao; Mệnh đề 04.3 không ghép trực tiếp được) đang đứng giữa Hệ quả 05.19 và Ví dụ 05.14. | §9 kết ở dòng 1036: "Bài tập 05.5(d) giảm giá này bằng nhiều lần chạy độc lập." (trong khối) | Chuyển nguyên đoạn 1019 xuống sau Ví dụ 05.14 (0 tiếng). Ví dụ 05.14 vẫn đứng ngay sau Hệ quả 05.19, nên mạch không đổi. |
| nhẹ | §3 cuối, dòng 154 | Câu kết §3 khẳng định tính lồi trước khi tính lồi được định nghĩa (§4) và trước khi được kiểm (Ví dụ 05.3; Bài tập 05.8). Bản trước có câu nối "chúng ta cần định nghĩa tính lồi…", nay đã bỏ. | "Trong cả hai ví dụ, hàm lỗi trên từng quan sát là một hàm lồi của $w$." | "…là một hàm lồi của $w$ theo nghĩa của §4 (Ví dụ 05.3, Bài tập 05.8)." (thêm khoảng 7 tiếng) |
| nhẹ | Đoạn sau Định nghĩa 05.6, dòng 360 | Câu rút gọn bỏ mất lý do, nên "trùng" đọc như một xung đột kí hiệu trái quy tắc một kí hiệu một nghĩa; bản trước nói rõ sự trùng là cố ý. | "$\lambda$ trùng hệ số chính quy hóa của Bài 06." | "$\lambda$ trùng hệ số chính quy hóa của Bài 06, vì $\tfrac\lambda2\lVert w\rVert^2$ là $\lambda$-lồi mạnh." (thêm 6 tiếng) |
| nhẹ | Định nghĩa 05.18 (969) và dòng 974; §2 dòng 102 | Theo N1, $\mathcal H=\{h_w:w\in W\}$ là lớp hàm điểm số $\mathcal X\to\mathbb R$; Định nghĩa 05.18 lấy "$\mathcal H$ … như Định nghĩa 01.4", mà ở Bài 01 (§1 mục 4) lớp giả thuyết gồm các hàm $\mathcal X\to\mathcal Y$, với $\mathcal Y=\{0,1\}$ trong phân lớp. Với hồi quy logistic, lớp ở dòng 974 không là lớp giả thuyết theo nghĩa của Bài 01. Cách đặt nhất quán với §2 và Định nghĩa 03.7 ($h_{w,0}=\mathbb 1[h_w\ge0]$, dòng 103); chỉ thiếu một mệnh đề nói rõ sự mở rộng. | "Lớp $\mathcal H=\{h_w:w\in W\}$ là lớp hàm điểm số" | Dòng 974: "…là lớp hàm điểm số, nhận giá trị trong $\mathbb R$ thay cho $\mathcal Y$" (thêm khoảng 7 tiếng). |
| nhẹ | Kiến thức tiên quyết, dòng 40; lời giải câu hỏi cuối buổi, dòng 1181 | Lời giải (c) dùng Định nghĩa 04.1 (sai số ước lượng, theo QĐ M14), nhưng danh sách tiên quyết từ Bài 04 chỉ có Định nghĩa 04.2 và Mệnh đề 04.3. Định nghĩa 04.1 có đúng nội dung được dùng (Bài 04 dòng 149–155: $L_D(h)-\inf_{h'}L_D(h')$, cần (T2) và $L_D<\infty$, thỏa với hàm lỗi bình phương ở đây). | "**Từ Bài 04.** Sai số tối ưu thực nghiệm (Định nghĩa 04.2), Mệnh đề 04.3." | "**Từ Bài 04.** Sai số ước lượng (Định nghĩa 04.1), sai số tối ưu thực nghiệm (Định nghĩa 04.2), Mệnh đề 04.3." (thêm 4 tiếng) |
| nhẹ | Danh sách sau Định nghĩa 05.10, dòng 500–504 | Nhãn chưa song song theo `van-phong.md` §3a: hai nhãn đầu là cụm động từ ("Rút không đều", "Xáo trộn lại …"), nhãn ba là danh từ. Khuôn nội dung cũng lệch: dòng 502, 503 nêu hệ quả (oracle của hàm khác; các $\xi_t$ không độc lập), dòng 504 chỉ mô tả mà không nói vì sao nằm ngoài định nghĩa. | "- **Rút không đều.** …" / "- **Oracle phụ thuộc thời điểm.** $\varphi$ phụ thuộc thêm vào $t$ hay vào các điểm lặp trước." | Nhãn danh từ: "**Phân bố rút không đều.**", "**Xáo trộn lại sau mỗi vòng qua dữ liệu (random reshuffling).**", "**Oracle phụ thuộc thời điểm.**"; dòng 504 thêm hệ quả: "…, nên $g_t$ không có dạng $\varphi(w_t,\xi_t)$." (thêm khoảng 8 tiếng) |
| nhẹ | Câu dài, `van-phong.md` §9a: dòng 17 (44 tiếng), 304 (50), 962 (42) | Ba câu mới hoặc vừa sửa vượt 40 tiếng; dòng 304 dồn ba ý (không Lipschitz trên $\mathbb R^p$, cận gradient trên quả cầu, kết luận theo phần (a)). | Dòng 304: "Tương tự, hàm lỗi bình phương không Lipschitz trên toàn $\mathbb R^p$; trên quả cầu bán kính $B$, … nên theo phần (a) của mệnh đề dưới đây, hàm lỗi là $2(BC_x+C_y)C_x$-Lipschitz trên quả cầu." | Tách tại dấu chấm phẩy (304) và trước "số gradient phải tính" (17): "…trên quả cầu $\lVert w\rVert\le5$. Số gradient phải tính bằng $1\%$…". Dòng 962: tách "…dao động quanh nó. Mức dao động là một mức sàn sai số tỉ lệ với $\eta$ khi $\eta$ nhỏ." |
| nhẹ | Ví dụ 05.7, Kết luận, dòng 695 | "Chặt ngặt" ghép hai từ khác nghĩa ("chặt" thường dùng cho cận đạt được, nghĩa ngược lại). | "…nên bất đẳng thức là chặt ngặt." | "…nên bất đẳng thức là ngặt: $1{,}3289<1{,}5019$." |
| nhẹ | Bảng Ví dụ 05.15 (1093) và §11 (1117) | Theo R4 #35, số lớn ngoài công thức viết "27.136", "640.000" (đúng `van-phong.md` §12). Nhưng trong cùng bảng các ô khác là công thức ($1600$, $7936$, $10^6$), và dòng 1117 viết "1600" thường trong khi mọi chỗ khác là $1600$. | "\| $256$ \| $106$ \| 27.136 \|"; "1600 bước đủ … 640.000 bước đủ" | Trong bảng: "$2{,}7136\cdot10^4$" hoặc để cả cột ở dạng văn bản; dòng 1117: "$1600$ bước … $6{,}4\cdot10^5$ bước" như dòng 1029. |

## 4. Định nghĩa trước khi dùng và kí hiệu mới

- `forward_refs.py`: 0. Các con trỏ mới tới phía sau đều là "§n" hoặc lời: 83 "(Định nghĩa 04.2, §9)", 137 "§6", 304 "mệnh đề dưới đây", 474 "(§8)", 502 "(§8)", 552 "(§9)".
- **$U$** (Mệnh đề 05.5, 310): đặt trong khối, cục bộ; không trùng kí hiệu Bài 01–04. ✓
- **$\theta$** (Định nghĩa 05.7, 369; Mệnh đề 05.13 Bước 1, 668; Phụ lục A): đặt tại định nghĩa. Bài 02 (bổ đề Hoeffding) và Bài 03 (lớp $\sin(\theta x)$) dùng $\theta$ cục bộ trong một chứng minh hay ví dụ; không xung đột. ✓
- **$k_{1:t-1}$** (613): định nghĩa tại chỗ dùng đầu, trước Bước 1. ✓
- **$\Phi$, $\bar\Phi$, $V$** (Phụ lục B, 1259–1263): đặt trong danh sách thành phần của bổ đề đóng băng; Bài 01–04 không dùng $\Phi$. ✓
- **$\gamma$** (Ví dụ 05.8 Bước 4, 812): đặt tại chỗ ("$\gamma>0$"). Bài 01–04 không dùng; blueprint Bài 07 dùng $\gamma$ cho lề (margin), nhưng đây là kí hiệu cục bộ của ví dụ. ✓
- **$q_i$** (câu ôn nhanh 3, 48) và **$a'$** (41, 46, 676): đặt tại chỗ; $a'$ ở dòng 676 dùng đúng khai triển của dòng 41. ✓
- **N1:** §2 (102–104) đặt $h_w(x)=\langle w,x\rangle$ là hàm điểm số, $h_{w,0}=\mathbb 1[h_w\ge0]$ khớp Định nghĩa 03.7 ($h_{w,b}(x)=\mathbb 1[\langle w,x\rangle+b\ge0]$) và khớp Ví dụ 01.3 ($h_w:x\mapsto\langle w,x\rangle$). Mọi chỗ dùng sau đều theo: 39 (tiên quyết), 126 (Ví dụ 05.1), 143–147 (ứng dụng: hàm lỗi logistic của $h_w$, lỗi 0–1 của $h_{w,0}$), 245 (Ví dụ 05.2), 974, 985 (Hệ quả 05.19), 1181 (lời giải (c)). Câu hỏi mở đầu (9) nói "hàm phân lớp tuyến tính", hợp lý vì đầu ra cuối là $h_{w,0}$. Chỉ còn điểm nhẹ ở Định nghĩa 05.18 (bảng mục 3).

## 5. Văn phong trên phần đã sửa (`no-ai-slop`, Detect)

- **§3a nhãn song song:** Mệnh đề 05.3 ("Hàm.", "Điểm."), Mệnh đề 05.5 ("Hàm.", "Tập.", "Hằng số."), Bổ đề 05.8(b), Định nghĩa 05.10, Bổ đề 05.12, Hệ quả 05.15 ("Hằng số.", "Độ dài bước."; (a)–(c)), Mệnh đề 05.20 ((a) "Kì vọng.", (b) "Phương sai.", (c) "Mô-men bậc hai."), Nhận xét 05.17 (**Giả thiết.**/**Bảo đảm.**), bổ đề đóng băng ở Phụ lục B: đạt. Lệch duy nhất là danh sách 500–504 (bảng mục 3).
- **§7a Ví dụ 05.6 Bước 3–4 (570–578):** đạt. Mỗi lựa chọn $i_3$ là một dòng với cùng khuôn ($g_3$; điểm trước chiếu; chuẩn; chiếu hay không; $L_S$), dòng $i_3=3$ nói rõ không chiếu. Bước 4 có điểm $(0{,}8330;-0{,}7670)$, chuẩn $1{,}1324$, điểm chiếu $(0{,}7356;-0{,}6774)$. Đã tính lại cả ba $g_3$, ba điểm trước chiếu, ba chuẩn và bước GD: khớp.
- **§7a Ví dụ 05.7 (683–696):** đạt. Bước 1 (khoảng cách), Bước 2 (hai vế trong `aligned`, có $2\eta=1$ và $\tfrac\eta2\lVert g\rVert^2=1$), Kết luận. Chỉ còn chữ "chặt ngặt".
- **§9a và câu dài:** xem bảng. Không có câu thuật lại quan niệm sai, câu hỏi tu từ hay câu chuyển ý rỗng trong phần đã sửa.
- **Thuật ngữ:** "độ chênh tối ưu" có định nghĩa ở 83 và dùng nhất quán (151, 715, 755, 794, 828); "sai số tối ưu thực nghiệm $\operatorname{opt}_S$" luôn đủ tên (993, 1170, 1181, 1184, 1192); "sai số ước lượng" (1181) dẫn Định nghĩa 04.1 và tách khỏi sai số tối ưu thực nghiệm trong cùng câu, đúng QĐ M14.
- **Văn bản làm chủ ngữ:** không còn "§n cho thấy/xét/tìm". Các câu "Bài 04 đo …" (3), "Bài 01 đặt/đòi …" (966, 1019), "Bài 06 so sánh …" (1186) dùng tên bài làm chủ ngữ, có tiền lệ ở Bài 04 ("Bài 05 xét …", dòng 1046); không đánh dấu.
- **Mẫu `no-ai-slop`:** không có từ cấm, câu nhấn mạnh tầm quan trọng, câu kết châm ngôn hay đoạn tóm tắt kết mục. Một chỗ lặp gần kề: 1098 "các cận không đếm thời gian chạy khi tính song song" và 1111 "không phải so sánh thời gian chạy" (cắt K6 dưới đây).

## 6. Ngân sách

Thân bài $11\,988$. Phần thêm đề xuất ở mục 3: khoảng $8+3+7+6+7+4+8=43$ tiếng (bớt 5 ở dòng 680, nên ròng khoảng 38). Đề xuất cắt **khoảng 107 tiếng** (đếm bằng `split()`), toàn là câu lặp ý đã có ở chỗ khác:

| # | dòng | câu cắt | số tiếng | đã có ở |
|---|---|---|---|---|
| K1 | 775 | "Số vòng lặp đủ theo cận tăng như $1/\epsilon^2$ và không phụ thuộc $p$ hay $m$ ngoài qua $R$, $G$." | 20 | 715 ($p$, $m$ chỉ qua $G$, $\lVert w_1-u\rVert$); 794 □ (giảm một nửa cần gấp bốn) |
| K2 | 843 | "Với $F=L_S$, tổng số dưới gradient trên một quan sát phải tính là $mT$." | 14 | 849 □ ("mỗi vòng GD trên $L_S$ tốn gấp $m$ lần"); 84; Ví dụ 05.9 Bước 4 |
| K3 | 870 | "Bảo đảm là cho $L_S$ với hàm lỗi logistic, không cho tỉ lệ lỗi phân lớp." | 16 | 1127 |
| K4 | 179 | "Với $\alpha_t=1/k$, nó chặn giá trị của $F$ tại trung bình các điểm bởi trung bình các giá trị." | 19 | Bước 5 (749–751), 758 |
| K5 | 474 | "; khi đó một bước không nhất thiết làm $F$ giảm (§8)" | 12 | 947 |
| K6 | 1098 | "; các cận không đếm thời gian chạy khi tính song song" | 9 | 1111 |
| K7 | 1111 | câu đầu "Theo cận, kích thước lô đổi số lần cập nhật lấy số quan sát và chỉ giảm phần phương sai." | 17 | 1098 (Kết luận Ví dụ 05.15), 1077 □, 1117 |

Sau thêm và cắt, thân bài khoảng $11\,988+38-107\approx11\,919$ tiếng. Nếu bỏ K7 thì §10 kết bằng câu giới hạn ở 1111, đúng `van-phong.md` §8.
