# Rà lại 5 — Mạch, móc nối và văn phong sau biên tập vòng 1, Bài 07

Người rà: vai trò 5, chỉ đọc. Đối tượng: `scratchpad/lec07-r1-frozen.md` (1 103 dòng; trùng byte với `2627-1/materials/lec-07/lecture-note.md`). Thân bài đếm lại: 11 954 tiếng (`wc -w` dòng 1 đến trước `## Phụ lục`). Số dòng dưới đây theo `lec07-r1-frozen.md`. Đề xuất câu chữ soát theo `no-ai-slop` chế độ Detect và `van-phong.md` §7a, §8, §9, §9a, §12.

## 1. Tổng kết

| Mức | Số | Nội dung |
|---|---|---|
| chặn bàn giao | 0 | — |
| nghiêm trọng | 0 | — |
| trung bình | 0 | — |
| nhẹ | 9 | §6 kết bằng khối ví dụ, §7 mở bằng công cụ; "bán kính đại diện" chưa định nghĩa; Định nghĩa 01.14 và Bổ đề 03.12 còn trong danh sách tiên quyết nhưng không còn được dùng; câu dẫn trước Nhận xét 07.18 nói sai phạm vi; sáu câu mới dài hơn 40 tiếng; ba chủ thể trừu tượng làm việc của người (§9a); một câu mở đoạn rỗng ở §10; "viết $G$ thay cho $\rho$" ở §13 thiếu đối tượng; Bước 4 của Ví dụ 07.11 là một kết quả dương nằm trong phản ví dụ mà Kết luận không nhắc |

Mọi phát hiện cũ của tôi (F1–F17) và bảy phát hiện trung bình của người rà 4 đều đã được xử lý (bảng ở mục 2). `forward_refs.py` cho 0. Cầu nối sang Bài 08 nay khớp blueprint 8.1–8.2. Lời hứa Bài 03 dòng 921 và Bài 05 dòng 1100 được giữ tường minh.

## 2. Phát hiện cũ: ✓ / ✗ / một phần

**Của tôi (`reviews/5-mach.md`).**

| Mã | Nội dung | Kết quả | Bằng chứng (dòng mới) |
|---|---|---|---|
| F1 | Danh sách tiên quyết thiếu và thừa | ✓ (có phát hiện mới N3) | 41–45: có tên khối, thêm Ví dụ 03.1, Định nghĩa 04.1, 05.18, 06.9, "Bước 1–4"; bỏ Ví dụ 05.10 |
| F2 | Cầu nối ngầm hứa Bài 08 bỏ tính lồi | ✓ | 960: "với hàm lỗi lồi, trơn và Lipschitz"; nối Phụ lục D; "tính chất của thuật toán chứ không của lớp" |
| F3 | $\rho_j$ trùng $\rho_m$ | ✓ | 880, 884: $G_j$; `ky-hieu.md` dòng 85 ghi lý do |
| F4 | Lời hứa Bài 03 dòng 921 (§28.1) | ✓ | 966 |
| F5 | Lời hứa Bài 05 dòng 1100 | ✓ | 806 (bán kính $r$ của Mệnh đề 04.3), 864–870 (cận cho hàm lỗi logistic) |
| F6 | $\rho_m\ge3{,}33$ cần $d\ge2m$ | ✓ | 778 |
| F7 | Nhận xét 02.11 gán cho hàm lỗi bản lề | ✓ | 864: không còn dẫn |
| F8 | Không có câu dẫn trước Bổ đề 07.8 | ✓ | 342 |
| F9 | Câu mở §9; câu dẫn Ví dụ 07.11, Nhận xét 07.18 | ✓ (câu 875 có vấn đề mới N4) | 765, 853, 875 |
| F10 | "$\tfrac14$ (Mệnh đề 07.2)" | ✓ | 907: bỏ dẫn |
| F11 | Bảng §2 "$B$ (§8)" | ✓ | 108: "(§5, §8)" |
| F12 | $\lvert E\rvert$ | ✓ | 302: $P$ |
| F13 | $j$, $k$ trùng nghĩa trong Nhận xét 07.18 | ✓ | 880: $y'$; $k$ giữ cho số nhãn (khối khác Nhận xét 07.17), chấp nhận |
| F14 | "lớp" trơn ở tiêu đề Ví dụ 07.2 | ✓ | 239 |
| F15 | Tiếng Anh cho ReLU, lớp hàm lỗi | ✓ | 9, 81, 111 |
| F16 | Câu "cần dùng thận trọng" | ✓ | 237 |
| F17 | Lặp "bằng chứng…" và "không nói thuật toán…" | ✓ | còn 27 và 905; 533 rút; 850, 901 viết lại |

**Trung bình của người rà 4 (`reviews/4-hoc-thuat-van-phong.md`).**

| Phát hiện | Kết quả | Bằng chứng |
|---|---|---|
| Danh sách tiên quyết chỉ có số hiệu | ✓ | 41–45 có tên khối (xem N3) |
| Định nghĩa 07.1 cắt giữa ngoặc ở 390 px | ✓ | 147–153: đệ quy $a_0=x$, $a_j=\varsigma(\Theta_ja_{j-1}+b_j)$, $f_\theta=\Theta_Ja_{J-1}+b_J$; trường hợp $J=1$ đúng ($f_\theta=\Theta_1x+b_1$) |
| Ví dụ 07.7 hai thiết lập | ✓ | 660: một thiết lập nêu cả hai bộ điểm; $x_1=x_2=1$; $\mathbf e_i$ có tên. Số kiểm lại: $B/2$, $B/\sqrt2\approx0{,}7071B$, $B/2=B/\sqrt4$ |
| Ví dụ 07.4 dồn ba dãy tám số | ✓ | 394–410: bảng ba cột và câu mẫu cho dòng đầu. Tôi tính lại cả 16 ô và hai tổng ($6$, $8$): khớp |
| "Phần phạt" hai nghĩa | ✓ | không còn "phần phạt" trong tệp; "số hạng phạt" là tổng (84, 730, 780), "số hạng Rademacher" là $2BC_x/(\gamma\sqrt m)$ (770, 843, 917, 946, 1101) |
| "Cận không cho thông tin" đặt tên muộn, ẩn dụ "chứng nhận rỗng" | ✓ | 588 in nghiêng có tiếng Anh; các lần trước (3, 130, 296) chỉ là vị ngữ "không cho thông tin"; ẩn dụ đã bỏ (847) |
| "Bằng chứng, không phải chứng minh" lặp ba lần | ✓ | còn 27 và 905, đúng quyết định TB9 |

## 3. Định nghĩa trước khi dùng

Bản sao: `scratchpad/reviews07/r5b/lec-07/lecture-note.md`. `forward_refs.py` in `0 forward references`.

| Kí hiệu hay thuật ngữ mới/đổi | Dùng đầu | Đặt tên | Nhận xét |
|---|---|---|---|
| $a_j$ | 147 | 147 (tại chỗ) | Trùng chữ với $a\in A$, $a_i$ (tọa độ) ở §6, khác mục; biên tập viên đã ghi ở `outline.md` §13. Chấp nhận |
| $G_j$ | 880 | 880 | đạt |
| $y'$ | 880 | 880 | đạt |
| $K$ | 864 | 864 ($K=\ln(1+e^{BC_x})$) | cục bộ trong Ví dụ 07.11; `ky-hieu.md` dòng 85 ghi; khác $k$ (số nhãn, 880) và $K=\lvert\mathcal H\rvert$ của Bài 02, nhưng khác khối và có định nghĩa tại chỗ. Chấp nhận |
| $\operatorname{err}_\tau$ | 424 | 424 (Giả thiết của Mệnh đề 07.9) | đạt |
| cận không cho thông tin | 588 (thuật ngữ) | 588 | xem bảng mục 2 |
| số hạng phạt; số hạng Rademacher | 84; 770 | 84 (nghĩa: phần cộng thêm vào đại lượng thực nghiệm); 770 (công thức ở nhãn bước) | nhất quán |
| điều kiện định tâm | 688 | 688 | đạt |
| bán kính đại diện | 206 | không có | N2 |
| danh sách tiên quyết có tên | 41–45 | — | tên khớp tiêu đề khối, trừ "hàm tăng trưởng (…, Bổ đề 03.12)" (Bổ đề 03.12 là bổ đề Sauer–Shelah). Xem N3 |

## 4. Mạch sau các chỗ cắt và ở cầu nối

- **§3 → §4 (135, 139).** Câu mở cũ của §4 đã bị cắt; vấn đề nay nằm ở câu kết §3 (135), và §4 mở bằng câu mô tả công cụ (139). Mạch vẫn liền. Câu 135 có chủ thể trừu tượng (N6).
- **§4 → §5 (206, 210).** Đạt. Câu 206 dùng "bán kính đại diện" chưa định nghĩa (N2).
- **§5 → §6 (305, 309).** Câu đầu của đoạn kết §5 đã bị cắt. Lý do (số tham số và chiều VC không phân biệt hai loại nhãn) nay chỉ còn ở Kết luận Ví dụ 07.3 (298) và câu cuối Nhận xét 07.6 (302, khối đọc thêm). Câu 305 vẫn đọc được sau 298–302. Đạt.
- **§6 → §7 (481, 484–486).** Câu kết §6 đã bị cắt (theo R4 #32), nên §6 kết bằng Kết luận Ví dụ 07.5, và Kết luận này trỏ sang §8, không sang §7. §7 mở bằng các bước chứng minh của Định lý 03.15 (công cụ) mà không nêu điều cần chứng minh. Trái `van-phong.md` §2 (nhu cầu trước công cụ) và §8 (mục kết bằng văn xuôi). Xem N1.
- **§7 → §8 (605, 609); §8 → §9 (761, 765); §9 → §10 (901, 905).** Đạt. Câu mở §9 báo đủ các khối của mục.
- **Trong §9.** Các câu dẫn 811, 853, 875 nối được các khối; câu 875 nói sai phạm vi (N4). Bước 4 của Ví dụ 07.11 (864–870) là cận dương cho hàm lỗi logistic, đặt trong một phản ví dụ. Kết luận (872) không nhắc đến nó (N9).
- **§10.** Đoạn 1 trả lời câu hỏi mở đầu. Đoạn 2 mở bằng một câu rỗng (N7). Năm giới hạn và câu thực hành đạt.
- **Cầu nối (960).** Khớp blueprint 7.6 ("Can the trajectory of SGD help?") và blueprint 8.2 (hàm lỗi lồi, trơn, Lipschitz); không phát biểu kết quả của Bài 08; khớp câu cuối Bài 06 (dòng 1130). Câu nối qua Phụ lục D cho phép câu hỏi chuyển từ bình phương tối thiểu sang SGD. Đạt.
- **Ví dụ xuyên suốt.** Số trong thí nghiệm nhất quán giữa 9, 27, 281, 838–843, 905, 960, 1101: chuẩn $\lVert w\rVert$ trên đặc trưng chia $\sqrt N$ ($916$, $10\,853$) và $\lVert\Theta_2\rVert$ ($20{,}5$, $242{,}7$). Các con số $0{,}2408$, $0{,}2577$, $0{,}0408$, $0{,}0193$ dùng nhất quán giữa Ví dụ 07.6, 07.8, 07.9, 07.10, §10 và §13.

## 5. Lời hứa

| Lời hứa | Cách giữ hiện nay | Đánh giá |
|---|---|---|
| Bài 03 dòng 868 (độ phức tạp Rademacher ở Bài 07; phép đếm ở Bước 3 cần nhãn $\{0,1\}$) | 309 | giữ |
| Bài 03 dòng 921 (UML §28.1 "chuẩn bị Bài 07") | 966: "§28.1 (cận trên cho học bất khả tri với chiều VC hữu hạn, qua cận Rademacher)" | giữ |
| Bài 05 dòng 1100 (cận thống kê cho hàm lỗi lồi và Lipschitz; Mệnh đề 04.3 cần hàm lỗi trong $[0,1]$ và một bán kính) | 806: với $\ell/4\in[0,1]$, vế phải chia $4$ là bán kính $r$ của Mệnh đề 04.3 (hàm lỗi bình phương); 864–870: cận cho hàm lỗi logistic sau khi chia cho $K$ (tôi tính lại: Lipschitz $1/K$ theo điểm số, rồi nhân $K$, cho đúng $2BC_x/\sqrt m+3K\sqrt{\ln(2/\delta)/(2m)}$) | giữ. Cận logistic là một phía, nên muốn có bán kính $r$ cho Mệnh đề 04.3 phải dùng thêm Nhận xét 07.12. Không bắt buộc sửa |
| Bài 06 dòng 854 | Ví dụ 07.9 | giữ |
| Cầu nối cuối Bài 06 | 3, câu hỏi mở đầu, Ví dụ 07.5, 07.10, §10 | giữ |

## 6. Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | N1 · 481–486 (ranh giới §6–§7) | §6 kết bằng khối ví dụ, Kết luận của khối trỏ sang §8. §7 mở bằng công cụ, chưa nêu điều cần chứng minh (`van-phong.md` §2, §8) | 481 "…; ở §8, một lớp với $10^5$ tham số nhưng chuẩn bị chặn có độ phức tạp nhỏ."; 486 "Bước 1 của chứng minh Định lý 03.15 dùng bất đẳng thức Chebyshev…" | Thêm câu đầu cho §7 (nêu vấn đề, không báo trước): "Muốn dùng độ phức tạp Rademacher, chúng ta cần chứng minh rằng nó chặn khoảng cách tổng quát hóa của mọi hàm trong một lớp hàm lỗi chọn trước mẫu." (+27 tiếng) |
| nhẹ | N2 · 206 | "bán kính đại diện của mẫu" là cụm mới, không có trong Bài 02–04. Mệnh đề 04.3 viết "$S$ là $r$-đại diện" | "năng lực thống kê ứng với số hạng $2r$, với $r$ là bán kính đại diện của mẫu" | "…ứng với số hạng $2r$ khi $S$ là $r$-đại diện (Định nghĩa 02.13)" (+1 tiếng) |
| nhẹ | N3 · 41, 43 | Thay hàm ghi nhớ bằng $\mathbb 1[x\in\mathbb Q]$ (161) khiến Định nghĩa 01.14 không còn được dùng. Bổ đề 03.12 cũng không còn được dẫn trong thân bài (Nhận xét 07.6 bỏ "cùng Bổ đề 03.12"), và tên đi kèm sai: Bổ đề 03.12 là bổ đề Sauer–Shelah, không phải "hàm tăng trưởng" | 41 "…, thuật toán ghi nhớ (Định nghĩa 01.1, 01.6, 01.10, 01.14)"; 43 "hàm tăng trưởng (Định nghĩa 03.11, Bổ đề 03.12)" | 41: "rủi ro, khoảng cách tổng quát hóa (Định nghĩa 01.1, 01.6, 01.10)" (−4). 43: "hàm tăng trưởng (Định nghĩa 03.11)" (−2). Nếu muốn giữ 03.12 cho Bài tập 07.7–07.8 thì viết "bổ đề Sauer–Shelah (Bổ đề 03.12)" |
| nhẹ | N4 · 875 | Câu dẫn nói các cận trên "chỉ dùng cho lớp ra tuyến tính với lớp ẩn cố định", nhưng Hệ quả 07.16, Ví dụ 07.8, 07.9, 07.11 dùng cho mọi lớp tuyến tính bị chặn (văn bản, hồi quy) | "Các cận trên chỉ dùng cho lớp ra tuyến tính với lớp ẩn cố định; khi mọi lớp nơ-ron đều được huấn luyện, cần một đại lượng khác." | "Các cận trên dùng cho lớp tuyến tính; với mạng, đó là lớp ra khi lớp ẩn cố định. Khi mọi lớp nơ-ron đều được huấn luyện, cần một đại lượng khác." (+5) |
| nhẹ | N5 · 25, 195, 235, 609, 808, 905 | Sáu câu mới hoặc vừa viết lại dài hơn 40 tiếng (`van-phong.md` §9: tách câu trên khoảng 40 tiếng). Câu 808 còn có dấu hai chấm "tiết lộ" (no-ai-slop: colon reveal) | 25 (55 tiếng): "Năng lực của cả lớp hàm … như nhau trong hai trường hợp."; 235 (57): "Bảo đảm cấp lớp (Bài 02–03, §7) … như ở Bài 06."; 905 (51); 195 (45); 609 (48); 808 (45): "…, nhưng lớp vẫn hội tụ đều: bổ đề co cho…" | Tách, không đổi số tiếng. 25: chấm sau "cũng không giải thích được"; "Lớp này thực hiện được mọi cách gán nhãn của $200$ điểm huấn luyện. Do đó độ phức tạp Rademacher của nó (§6), đo mức khớp nhãn ngẫu nhiên trên các điểm đó, như nhau trong hai trường hợp." 235: chấm trước "nó không nói": "… bất kể thuật toán. Bảo đảm này không nói thuật toán chọn hàm nào; đó là việc của bảo đảm cấp thuật toán, như ở Bài 06." 905: chấm trước "hai trường hợp khác nhau". 808: "…, nhưng lớp vẫn hội tụ đều. Bổ đề co cho một cận cấp lớp ở chỗ…" |
| nhẹ | N6 · 111, 135, 206 | Chủ thể trừu tượng làm việc của người (`van-phong.md` §9a: "định nghĩa đòi hỏi", "ví dụ đọc") | 111 "Bài 02–03 phát biểu chúng cho lớp giả thuyết, nên định lý viết lại."; 135 "Ví dụ 07.1 đòi một lớp lớn hơn lớp nửa không gian afin"; 206 "Một lớp mạng đặt ra ba câu hỏi" | 111: "…, nên ta viết lại chúng trong giả thiết của định lý." (+5). 135: "Để phân lớp đúng Ví dụ 07.1, chúng ta cần một lớp lớn hơn lớp nửa không gian afin; …" (+5). 206: "Về một lớp mạng, chúng ta có ba câu hỏi, ứng với…" (+2) |
| nhẹ | N7 · 907 | Câu mở đoạn không mang thông tin (no-ai-slop: portability test). Các câu sau đã nêu ba câu trả lời | "Ba câu hỏi về một lớp mạng có ba câu trả lời riêng." | Cắt câu này; mở đoạn bằng "Về biểu diễn, trên Ví dụ 07.1 …" (−11) |
| nhẹ | N8 · 971 | Sau khi rút gọn, "viết $G$ thay cho $\rho$" không nói $G$ là gì; trong bài, $\rho_m$ là bán kính VC | "Học phần giữ $B$, $\gamma$ riêng, dùng độ phức tạp thực nghiệm, và viết $G$ thay cho $\rho$." | "…, và viết hằng số Lipschitz của bổ đề co là $G$ thay cho $\rho$." (+6) |
| nhẹ | N9 · 864–872 | Bước 4 của Ví dụ 07.11 nay chứa cận dương cho hàm lỗi logistic (giữ lời hứa Bài 05), nhưng khối là phản ví dụ, nhãn bước chỉ nói "hàm lỗi không bị chặn", và Kết luận không nhắc đến cận này. Người học dễ bỏ qua | 864 "**Bước 4: hàm lỗi không bị chặn.**"; 872 "**Kết luận.** Định lý 07.11 áp dụng cho lớp hàm lỗi bị chặn, không tự động cho điểm số của mạng." | Nhãn: "**Bước 4: hàm lỗi không bị chặn, chia lại cho bị chặn.**" (+4). Kết luận: "… không tự động cho điểm số của mạng; hàm lỗi logistic dùng được sau khi chia cho $K$." (+9) |

**Ngân sách.** Nếu nhận hết: thêm khoảng +27 (N1) +1 (N2) +5 (N4) +12 (N6) +6 (N8) +13 (N9) = +64; cắt −6 (N3) −11 (N7) = −17. Tăng ròng khoảng +47, thân bài khoảng 12 001. Muốn dưới trần, rút câu N1 còn "Chúng ta cần chứng minh rằng độ phức tạp Rademacher chặn khoảng cách tổng quát hóa của mọi hàm trong một lớp hàm lỗi chọn trước mẫu." (+22 thay vì +27), và bỏ phần thêm cho nhãn bước ở N9 (−4). Khi đó thân bài khoảng 11 992. Ưu tiên N1, N2, N3, N4; N6 và N8 có thể bỏ nếu thiếu chỗ. Biên tập viên chốt bằng `wc -w`.
