# Rà soát 5 — Mạch và móc nối, Bài 09 (bản đóng băng `lec09-draft-frozen.md`)

Người rà: tác tử rà mạch và móc nối, chỉ đọc repo. Đối chiếu: `CLAUDE.md` học phần (Define before use, Structure), `planning/lec-09/outline.md`, `review-log.md`, `sources/blueprint.md` (8.6, Lecture 9, 10.1–10.3), ghi chú Bài 01–08, `ky-hieu.md`, `thuat-ngu.md` §11, `van-phong.md` §9a. Số dòng dưới đây là số dòng của bản đóng băng. Đề xuất câu chữ đã soát theo `no-ai-slop` (Detect).

## Tổng kết theo mức

- **Chặn bàn giao:** 0.
- **Nghiêm trọng:** 0.
- **Trung bình:** 5 (R1 viết tắt KL chưa mở; R2 câu đầu cầu nối Bài 10 sai sự kiện và lệch mẫu "Câu hỏi cho Bài N là"; R3 $x_i$ hai nghĩa; R4 §1 nói mẫu kiểm tra chỉ dùng trong thí nghiệm; R5 "phân bố dừng" chưa định nghĩa).
- **Nhẹ:** 13 (R6–R18).

Mạch tổng thể tốt. Câu hỏi mở đầu được trả lời ngay (dòng 30–32) và lại ở §10. Bốn ví dụ xuyên suốt (Ví dụ 09.1, khối DNA, Bernoulli, Gauss) được dùng nhất quán tới câu hỏi cuối buổi. Mọi số hiệu 01.x–08.x đúng tên và nội dung. Lời hứa Bài 02 dòng 574 và cầu nối cuối Bài 08 được giữ.

## Kết quả `forward_refs.py`

Bản sao: `reviews09/r5/lec-09/lecture-note.md`. Kết quả: **0 forward references**. Đọc tay: không câu thân bài nào dẫn khối có số đứng sau. Các chỗ trỏ tới sau đều là "§k", "Phụ lục X", "định lý dưới đây", "ví dụ thứ hai sau mệnh đề dưới đây" hoặc Bài tập 09.k (tệp riêng). Có năm thuật ngữ dùng trước định nghĩa hoặc thiếu tiếng Anh (R8).

## Bảng lần dùng đầu (thân bài; bỏ qua tiêu đề, mục tiêu, cầu nối, tài liệu đọc)

| Kí hiệu / thuật ngữ | Lần dùng đầu | Được giới thiệu ở | Nhận xét |
|---|---|---|---|
| $\mathcal A$, $x_{1:n}$, $x_j$, $x_{<j}$, $n$, $j$ | 76 (§1 mục 1) | tại chỗ | đạt |
| $n_i$ | 77 | tại chỗ ("độ dài $n_i$"), chính thức ở Định nghĩa 09.1 (89) | đạt |
| $p_\theta$, $\Theta$, $\theta$ | 78 | tại chỗ ("lớp … hàm xác suất"), bảng §2 (116) | đạt |
| $\hat\theta$ | 101 (bảng §1) | tại chỗ | đạt |
| $k$ | 87 (Định nghĩa 09.1) | tại chỗ | tiếng Anh "context length" đặt ở dòng 90, không ở 87 (R8) |
| $u_j$ | 90 | tại chỗ | trùng chữ với $u$ đều trên $[0,1]$ ở 684, 760 (R12) |
| $p_D$ | 117 (bảng §2) | tại chỗ; nhắc lại 167 | đạt |
| $\zeta$ | 51 (tiên quyết, $N(0,1)$) | tại chỗ; vai nhiễu phụ ở Định nghĩa 09.14 (678) | đạt |
| $m_1$ | 170 (Ví dụ 09.2) | tại chỗ; dùng lại 453 | đạt |
| $\mathtt E$ | 266 | tại chỗ | đạt |
| $\ell_{\mathrm{len}}$ | 327 | tại chỗ | đạt |
| $\theta^*$ / $\theta^\star$ | 342 / 429 | tại chỗ | hai dấu sao gần giống nhau cho hai vai khác nhau (R6) |
| $\mathrm H$, $\mathrm h$, $\mathrm{KL}$ | 360, 363, 362 | Định nghĩa 09.7 | đạt về kí hiệu; chữ "KL" dùng từ 103, chưa mở (R1) |
| $\mathrm{Ber}(\cdot)$ | 368 | không định nghĩa | R7 |
| $\mathcal V$, $r$, $v$ | 495, 497 | Định nghĩa 09.10 | đạt ($v$ có ở câu ôn nhanh 3, dòng 57) |
| $q_\phi$, $\phi$, $\Phi$ | 501 | Định nghĩa 09.10 | đạt; phần phân biệt với Bài 07 thiếu $\phi$ trần (R12) |
| $\operatorname{ELBO}$ | 536 | Định nghĩa 09.11 | đạt (viết tắt mở ở dòng 5) |
| $\theta_t$, $q_i$, $\operatorname{ELBO}(\theta,q;x)$ | 638–644 | tại chỗ | đạt |
| $F$, $g_\phi$, $\mu_\phi$, $\sigma_\phi$, $\odot$ | 676–679 | Định nghĩa 09.14 | đạt |
| $\kappa$, $N_0$, $U$, $M$ | 691–693 | Mệnh đề 09.15 | đạt; $C$ ở 698 không ghi "một hằng số" (nhẹ, gộp vào R8) |
| $\xi=(i,\zeta)$ | 711 | tại chỗ | khớp $\xi$ của Bài 05 |
| $c$, $b$ | 276, 278 | tại chỗ | đạt |
| $x_i$ (quan sát thứ $i$) | 162 | không nói; trùng $x_j$ (kí tự) | R3 |
| MLE, ELBO, ERM, SGD, EM, GAN | 5, 5, 79, 79, 79, 806 | đều có tên đầy đủ và tiếng Anh | đạt |
| KL | 103 | không mở | R1 |
| MSE | 312 | "(MSE)", thiếu tên tiếng Anh đầy đủ | R8 |
| hàm lỗi log trung bình theo kí tự | 149 (§3) | Định nghĩa 09.4 (234) | dùng trước định nghĩa (R8) |
| entropy, phân kì KL | 103 (bảng §1, có "của §7") | Định nghĩa 09.7 | chấp nhận được vì có con trỏ |
| hàm trội | 124 (§2) | Mệnh đề 09.15(ii) (693), không có tiếng Anh | R8 |
| giá | 394 (chứng minh 09.8) | tại chỗ bằng tập, không có tiếng Anh | R8 |
| rò rỉ thông tin | 307 (tiêu đề Ví dụ 09.5) | không có tiếng Anh | R8 |
| phân bố dừng | 461 | không định nghĩa, không có tiếng Anh | R5 |
| quá khớp, đặc tả sai, làm trơn cộng một, nat | 483, 439, 453, 290 | tại chỗ, có tiếng Anh hoặc giải nghĩa | đạt; "đặc tả đúng" ở 429 chưa có tiếng Anh (nhẹ) |
| tiên nghiệm, hậu nghiệm, bằng chứng, tái tạo, khe | 498–500, 558, 590 | tại chỗ | đạt |

## Mạch từng mục

- **Đoạn dẫn (3–5).** Gần như chép đúng câu hỏi cuối Bài 08 (dòng 906): chuỗi có phần tử phụ thuộc nhau, $-\ln$ độ hợp lý của cả chuỗi, ba đại lượng viết lại. "Nhận xét 01.2" đúng: khối này đặt tên "hàm lỗi log (log loss)" là $-\ln$ xác suất gán cho nhãn đúng. Bài 06 và Bài 08 dẫn Nhận xét 02.11 cho cùng khái niệm; hai cách dẫn đều đúng, không mâu thuẫn.
- **Câu hỏi mở đầu (9–32).** Câu hỏi là câu hỏi thật và được trả lời ngay: quan sát độc lập là cả chuỗi; rủi ro cần làm nhỏ là kì vọng của $-\ln$ xác suất gán cho cả chuỗi (§7). Câu hỏi ở dòng 30 được phép theo `van-phong.md` §9a, nhưng nhắc lại ý của câu hỏi ngay trên đó (có thể cắt, xem phần cắt).
- **Tiên quyết (46–70).** Đúng và đủ. Riêng xích Markov và phân bố dừng được dùng ở Ví dụ 09.8 mà không có trong danh sách (R5).
- **§1.** Mở bằng bảy thành phần, kết bằng câu văn xuôi (105). Dòng 77 nói mẫu kiểm tra chỉ dùng trong thí nghiệm, trái với Ví dụ 09.4 (R4).
- **§2.** Phân biệt $\Theta$/$\Theta_j$ và nói hàm lỗi log nằm ngoài khung cũ; câu nói điều này hơi nhập nhằng (R13). Kết bằng văn xuôi.
- **§3.** Ví dụ 09.1 và khối DNA, rồi câu nối sang §4 (152). Khối ứng dụng dùng "hàm lỗi log trung bình theo kí tự" trước định nghĩa (R8).
- **§4.** Mở bằng vấn đề (cần hàm lỗi chấm một phân bố), kết ở 189. Đạt.
- **§5.** Mở bằng con số $4^{200}-1$ tham số, nhưng mục không quay lại con số đó: Mệnh đề 09.3 không giảm số tham số, còn ngữ cảnh bậc $1$ với $15$ tham số chỉ có ở §3 (R9). Kết ở 269. Đạt.
- **§6.** Mở bằng vấn đề (các số hạng phụ thuộc nhau). Câu kết (351) bỏ bài học của Thiết lập B, Ví dụ 09.5 (R10).
- **§7.** Mở bằng vấn đề, kết ở 488. Ví dụ 09.8 trả lời ba câu hỏi thực hành của §3. Đạt.
- **§8.** Mở bằng vấn đề (tích phân không tính được). Câu kết 669 dẫn sang §9 đúng chỗ.
- **§9.** Mở bằng vấn đề (gradient khi kì vọng lấy theo $q_\phi$). Câu kết 789 chỉ nhắc lại Ví dụ 09.13 và bỏ điều kiện của tái tham số hóa (R10).
- **§10.** Trả lời câu hỏi trung tâm và nhắc lại các con số chính, không có số mới. Các giới hạn khớp blueprint 9.4.
- **§12 và cầu nối.** Câu hỏi (a)–(d) chỉ nhìn lại; con số trùng Ví dụ 09.3, 09.10, 09.12. Cầu nối khớp blueprint 9.6 và 10.1 (tác tử chọn dữ liệu, phân bố thay đổi) và không phát biểu kết quả của Bài 10. Có hai lỗi (R2).

## Móc nối với Bài 01–08 (đã grep)

Mọi số hiệu đều đúng tên và nội dung:

- Định nghĩa 01.1 (Hàm lỗi và rủi ro kì vọng; $\ell\in[0,\infty)$).
- Nhận xét 01.2 (Tính khả tích khi hàm lỗi không bị chặn; định nghĩa hàm lỗi log).
- Định nghĩa 01.6, Mệnh đề 01.7 (dạng yếu của (T1), cần $L_D<\infty$), Định nghĩa 01.8, 01.10 (khoảng cách tổng quát hóa của thuật toán, $0{,}0847$ đúng), 01.14, 01.24 (so với lớp).
- Định lý 02.7, Ví dụ 02.6, Hệ quả 02.10(b) (bán kính hai phía), Nhận xét 02.8 → (T3) ở dòng 413, đoạn sau (T3) nhân bán kính với $b-a$ (dòng 415), Nhận xét 02.11.
- (T7) ở dòng 916, trước Hệ quả 04.17.
- Định nghĩa 05.10 ((G1), (G2)); (C) ở đoạn trước Định lý 05.14.
- Ví dụ 07.11, Bước 4 (hàm lỗi logistic trong $[0,K]$).

**Lời hứa Bài 02 dòng 574** ("Bài 06 xét chúng với giả thiết khác"): Bài 06 (dòng 1022) đã xử lý hàm lỗi logistic bằng tính Lipschitz và ghi rằng kết luận không chuyển sang hàm lỗi log của một mô hình bất kì. Bài 09 khép lại ý này ở §2 (122), Ví dụ 09.4 (cần $c>0$), Ví dụ 09.7 (Nhận xét 02.11) và §10. Lời hứa được giữ; có thể thêm mắt xích Bài 06 (R11).

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | dòng 5; 103 | R1. Viết tắt "KL" dùng từ 103 nhưng không được mở. Quy tắc viết tắt của workspace và `thuat-ngu.md` §11 đều yêu cầu dạng "(Kullback–Leibler divergence, KL)". | 5: "phân kì Kullback–Leibler (Kullback–Leibler divergence)"; 103: "phân kì KL của §7" | Dòng 5: "phân kì Kullback–Leibler (Kullback–Leibler divergence, KL)". |
| trung bình | dòng 860 (cầu nối) | R2. (a) "Phân bố duy nhất phụ thuộc tham số là $q_\phi$" sai: $p_\theta$ phụ thuộc $\theta$ và được rút để sinh chuỗi (238, Ví dụ 09.13), còn bước E lấy kì vọng theo $q_i=p_{\theta_t}(\cdot\mid x_i)$ (644). (b) Thiếu mẫu "Câu hỏi cho Bài N là:" của Bài 01–08, và vế "và khi phân bố…" bị tỉnh lược. | 860: "phân bố duy nhất phụ thuộc tham số là $q_\phi$ … Câu hỏi cho Bài 10: … ; và khi phân bố dữ liệu thay đổi trong lúc học?"; lec-05..08: "Câu hỏi cho Bài 0x là: …" | "Trong cả bài, dữ liệu đến từ một phân bố $D$ cố định, không phụ thuộc tham số; trong mục tiêu huấn luyện, phân bố lấy kì vọng duy nhất phụ thuộc tham số đang tối ưu là $q_\phi$, do người học chọn. Câu hỏi cho Bài 10 là: điều gì thay đổi khi người học điều khiển cách thu dữ liệu, chẳng hạn khi các hành động rời rạc của một tác tử quyết định quan sát tiếp theo, nên phân bố của dữ liệu phụ thuộc chính tham số đang học, và điều gì thay đổi khi phân bố dữ liệu thay đổi trong lúc học?" (+≈10 tiếng) |
| trung bình | 162; 559; 643 | R3. $x_i$ là quan sát thứ $i$ của mẫu (Định nghĩa 09.2, Định lý 09.12(d), Hệ quả 09.13), trong khi §1 vừa đặt $x_j$ là kí tự thứ $j$ của một chuỗi. Không câu nào nói hai cách đọc. | 76: "$x_{1:n}=(x_1,\ldots,x_n)$"; 162: "tại mẫu $s=(x_1,\ldots,x_m)$" | Thêm một dòng vào bảng §2: "$s=(x_1,\ldots,x_m)$ \| mẫu cố định ở §4 và §8, $x_i$ là quan sát thứ $i$; trong một chuỗi, $x_j$ là kí tự thứ $j$". (+≈20 tiếng) |
| trung bình | 77 | R4. §1 nói mẫu kiểm tra độc lập chỉ dùng trong thí nghiệm, nhưng Ví dụ 09.4 dùng mẫu kiểm tra $m=50$ chuỗi cho một cận, và Ví dụ 09.8 (iii) dựa vào cận đó. | 77: "Mẫu kiểm tra độc lập chỉ dùng trong thí nghiệm."; 276: "Mẫu kiểm tra $S$ gồm $m=50$ chuỗi" | "Mẫu kiểm tra độc lập chỉ dùng ở §6 và trong thí nghiệm." (+2) |
| trung bình | 461; 970 (Phụ lục C) | R5. "Phân bố dừng" chưa được định nghĩa, không có tiếng Anh và không có trong tiên quyết, nhưng là một bước suy luận của Ví dụ 09.8, Bước 1. | 461: "Mỗi kí tự sau cũng có phân bố đều (phân bố dừng)" | Thêm vào mục "Xác suất và giải tích" của tiên quyết: "xích Markov hữu hạn trạng thái và phân bố dừng (stationary distribution)". (+≈10) |
| nhẹ | 342, 344; 429, 451 | R6. $\theta^*$ (điểm cực tiểu, Ví dụ 09.6) và $\theta^\star$ (tham số thật, Hệ quả 09.9, Ví dụ 09.7) là hai vai khác nhau nhưng gần như cùng một chữ. `ky-hieu.md` dùng $w^*$ cho nghiệm tối ưu. | 342: "tại $\theta^*=\tfrac16$"; 429: "$p_D=p_{\theta^\star}$" | Ví dụ 09.6: bỏ kí hiệu và viết "nhỏ nhất tại $\theta=\tfrac16$" / "tại $\theta=\tfrac12$"; giữ $\theta^\star$ cho tham số thật. |
| nhẹ | 368 | R7. $\mathrm{Ber}(\cdot)$ dùng mà không định nghĩa. | 368: "$\mathrm{KL}(\mathrm{Ber}(0{,}6)\Vert\mathrm{Ber}(0{,}7))$" | Ví dụ 09.2, Thiết lập: "Phân bố Bernoulli $\mathrm{Ber}(\theta)$: $\mathcal X=\{0,1\}$, …". (+2) |
| nhẹ | 149; 124; 394; 307; 312; 87; 698; 429 | R8. Thuật ngữ dùng trước định nghĩa hoặc thiếu tiếng Anh ở lần đầu: "hàm lỗi log trung bình theo kí tự" (149, định nghĩa ở 234); "hàm trội" (124, không có tiếng Anh ở bất kì đâu); "giá" (support); "rò rỉ thông tin" (leakage); "MSE"; "độ dài ngữ cảnh" (tiếng Anh ở 90, không ở 87); $C$ chưa gọi là hằng số; "đặc tả đúng" (well-specified). | các dòng đã nêu | 149: "hàm lỗi log chia cho độ dài chuỗi"; 124: "(tính khả vi, một cận khả tích cho gradient)" và 693: "**(ii) Hàm trội** (dominating function)."; 394: "trên giá (support) $\{x:p_D(x)>0\}$"; 305: "… ngay ở bước đánh giá, qua rò rỉ thông tin (leakage) từ mẫu huấn luyện sang mẫu kiểm tra."; 312: "Lỗi bình phương trung bình (mean squared error, MSE)"; chuyển "(context length)" lên 87; 698: "với một hằng số $C$"; 429: "(well-specified)". (+≈25) |
| nhẹ | 193; 238 | R9. §5 mở bằng $4^{200}-1$ tham số nhưng không trả lời con số này. Mệnh đề 09.3 không giảm số tham số; việc giảm đến từ giả thiết ngữ cảnh bậc $k$. | 193: "cần $\lvert\mathcal A\rvert^n-1$ tham số, tức $4^{200}-1$"; 226: "giới hạn độ dài ngữ cảnh … là giả thiết thêm vào" | Cuối đoạn 238: "Với ngữ cảnh bậc $1$, mô hình trên chuỗi DNA của §3 có $15$ tham số tự do thay cho $4^{200}-1$." (+≈20) |
| nhẹ | 351; 789 | R10. Câu kết của §6 bỏ bài học của Thiết lập B; câu kết của §9 chỉ nhắc lại Ví dụ 09.13 mà bỏ điều kiện của tái tham số hóa. `outline.md` mục 3 có sẵn cả hai ý. | 351; 789: "Trong Ví dụ 09.13, hỗn hợp tốt theo hàm lỗi log nhưng kém theo mẫu sinh, còn mô hình ghi nhớ thì ngược lại; vì vậy hai tiêu chí được báo cáo riêng." | 351: "Các cận cho quan sát độc lập cùng phân bố dùng số chuỗi $m$, dù mỗi chuỗi dài bao nhiêu; trong Thiết lập B, chia ngẫu nhiên các cửa sổ làm mẫu kiểm tra phụ thuộc hàm đã học; khi độ dài các chuỗi khác nhau, chuẩn hóa theo độ dài thay đổi cả mục tiêu tổng thể." 789: "Gradient theo đường đi của ELBO không chệch khi hàm dưới kì vọng khả vi liên tục theo $\phi$ trên mọi đường nhiễu và bị trội bởi một hàm khả tích; điều kiện này không thỏa với biến ẩn rời rạc. Hàm lỗi log và chất lượng mẫu sinh là hai tiêu chí khác nhau, nên được báo cáo riêng." (+≈30) |
| nhẹ | 122 | R11. Chuỗi lời hứa Bài 02 → Bài 06 → Bài 09 thiếu mắt xích Bài 06. Bài 06 (dòng 1022) ghi rằng kết luận cho hàm lỗi logistic "không chuyển sang hàm lỗi log của một mô hình bất kì". | 122: "Các cận của Bài 02–04 và Bài 07 chỉ áp dụng khi …" | Tùy chọn, thêm sau câu đó: "Cận của Bài 06 dùng tính lồi và Lipschitz của hàm lỗi logistic theo tham số, nên cũng không chuyển sang một mô hình xác suất tùy ý." (+≈25) |
| nhẹ | 504; 684, 760 | R12. Phần phân biệt kí hiệu thiếu ánh xạ $\phi$ trần của bổ đề co ở Bài 07 (lec-07 dòng 680). Chữ $u$ (biến đều) trùng $u_j$ (cửa sổ). | 504: "$\phi$ khác $\phi_i$, $\phi_\gamma$ của Bài 07"; 684: "$u$ đều trên $[0,1]$" | 504: "$\phi$ khác các ánh xạ $\phi$, $\phi_i$, $\phi_\gamma$ của bổ đề co ở Bài 07"; ở 684 và 760 đổi $u$ thành $U_0$ hoặc ghi "(khác cửa sổ $u_j$)". |
| nhẹ | 122 | R13. Câu nhập nhằng: theo cách đọc "khi có mật độ" gắn với cả Định nghĩa 01.1, câu sẽ sai, vì với hàm xác suất $\ell$ cũng nhận $+\infty\notin[0,\infty)$. | 122: "hàm lỗi log không thỏa Định nghĩa 01.1, (T2) khi có mật độ, và (T3)" | "Vì vậy hàm lỗi log nằm ngoài Định nghĩa 01.1 (giá trị trong $[0,\infty)$), trái (T2) khi có mật độ, và không thỏa (T3)". |
| nhẹ | 586 | R14. Định lý 09.12 áp dụng cho mật độ trên $\mathcal V$, nhưng dòng 586 dẫn Bước 3 (bản rời rạc) của chứng minh Mệnh đề 09.8. Bản mật độ là phần (c) và Bước 4. | 586: "Bước 3 của chứng minh Mệnh đề 09.8, áp dụng cho hai mật độ" | "Mệnh đề 09.8(c) (Bước 3–4 của chứng minh), áp dụng cho hai mật độ …". |
| nhẹ | 396; 444 | R15. Cụm "giá không chứa" thiếu tân ngữ; người đọc không biết giá nào không chứa giá nào. | 444: "Ví dụ 09.7 (Giá không chứa và mẫu toàn số $0$)"; 396: "Bước 1 (giá không chứa)" | 444: "Ví dụ 09.7 (Mô hình bằng $0$ trên giá của $p_D$ và mẫu toàn số $0$)"; 396: "Bước 1 (mô hình bằng $0$ trên giá của $p_D$)". |
| nhẹ | 94 | R16. "Không-ví dụ" là từ ghép mới, không có trong Bài 01–08. | 94: "Không-ví dụ: các cửa sổ chồng lấn …" | "Phản ví dụ: các cửa sổ chồng lấn …". |
| nhẹ | 485 | R17. Câu trả lời (iii) chỉ trỏ tới Ví dụ 09.4 (50 chuỗi), trong khi Ví dụ 09.8 dùng 200 chuỗi kiểm tra. Người đọc không thấy cận ứng với 200 chuỗi lớn hơn rất nhiều so với chênh lệch $0{,}001$ đo được. | 485: "(iii) khoảng tin cậy dùng số chuỗi kiểm tra làm cỡ mẫu (Ví dụ 09.4)" | Tùy chọn: "… (Ví dụ 09.4): với $200$ chuỗi và $c=0{,}05$, bán kính theo kí tự là $\ln20\sqrt{\ln40/400}\le0{,}2877$." ($=0{,}28769$, đã tính lại.) (+≈15) |
| nhẹ | 30 | R18. Câu hỏi đầu dòng 30 nhắc lại ý của câu hỏi ngay trên đó. Câu được `van-phong.md` §9a cho phép, nhưng thừa. | 28 và 30 | Cắt "Có phải ba số hạng là ba quan sát độc lập không?" (xem phần cắt). |

## Ngân sách: chữ thêm và chỗ cắt (thân 11 984/12 000)

Nếu nhận R1–R10 và R13–R15: thêm khoảng **+120 tiếng**; R11 và R17 tùy chọn (+40). Các chỗ cắt đề xuất (khoảng **−125 tiếng**, không mất nội dung):

1. Dòng 105, cắt cả câu "Các đồng nhất thức của §5, §7 và §8 … trong thí nghiệm." (≈ −29). Bảng ở dòng 98–103 và dòng **Bảo đảm.** của từng khối đã nói điều này.
2. Dòng 30, cắt câu hỏi đầu (≈ −11; R18).
3. Ví dụ 09.3, Kết luận (262): rút còn "Độ hợp lý của chuỗi là tích các độ hợp lý có điều kiện." (≈ −25). Phần sau lặp lại Bước 4.
4. Ví dụ 09.6, Kết luận (348): bỏ vế "chọn mục tiêu là chọn trọng số cho từng kí tự" (≈ −10). Ý này đã có ở 330 và Bước 3.
5. Dòng 789 thay bằng câu kết mới của R10 (đã tính trong phần thêm). Cắt thêm ở 167 "có hàm xác suất (hoặc mật độ) $p_D$," (≈ −8), vì bảng §2 đã định nghĩa $p_D$.
6. Dòng 799 (giới hạn đầu ở §10): rút còn "**Hàm lỗi log không bị chặn.** Cần một cận dưới cho xác suất của mô hình (§2; Ví dụ 09.7)." (≈ −10).
7. Dòng 544: bỏ "Tên gọi đến từ định lý dưới đây;" (≈ −8).
8. Dòng 30–31: "Nhưng kí tự thứ ba được dự đoán từ kí tự thứ hai, mà kí tự thứ hai ngẫu nhiên: theo bảng, …" → "Theo bảng, xác suất rút $\mathtt B$ ở vị trí thứ ba bằng $0{,}7$ sau $\mathtt A$ và $0{,}4$ sau $\mathtt B$, nên ba số hạng không độc lập; …" (≈ −20).

Số tiếng ở trên là ước lượng bằng `wc -w` trên dòng gốc. Người biên tập chạy lại bộ đếm của học phần sau khi sửa.
