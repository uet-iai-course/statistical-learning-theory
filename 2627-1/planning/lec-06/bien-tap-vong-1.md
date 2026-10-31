# Biên tập vòng 1 — Bài 06

Tệp nội bộ. Biên tập viên: tác tử viết ghi chú (general-purpose, opus, high), giao qua `SendMessage` của phiên điều phối, 2026-10-31. Căn cứ: `reviews/0-quyet-dinh.md` (ưu tiên cao nhất) và năm báo cáo `reviews/1-hoc-vien.md` (R1), `2-toan-hoc.md` (R2), `3-chuyen-gia-nguon.md` (R3), `4-hoc-thuat-van-phong.md` (R4), `5-mach.md` (R5). Số dòng theo bản đóng băng (SHA-256 `1a2fd0319e4b55ac`). Bản trước biên tập: scratchpad `writer06/note_v0_frozen.md`; các script sửa: `writer06/ed1.py`–`ed10.py`. `no-ai-slop` chế độ Edit.

## Số tiếng (`wc -w`)

| | Trước | Sau | Trần |
|---|---|---|---|
| Thân bài (đến trước `## Phụ lục`) | 11 979 | 11 974 | 12 000 |
| Phụ lục | 1 447 | 1 513 | 3 000 |
| Số dòng | 1 285 | 1 301 | |

Sau các sửa theo quyết định (trước khi cắt bù), thân bài lên 12 353 tiếng; các chỗ cắt ở mục cuối đưa về 11 974.

## Quyết định gộp

| Mã | Dòng (đóng băng) | Đã sửa thế nào |
|---|---|---|
| C1 | 650, 671 | Bỏ câu "Cùng phép đổi chỗ … Vế phải bằng $\mathbb EL_D(A(S^{(i)};\xi))$ theo Bước 1". Bước 2 nay: vế phải của đẳng thức đổi vai bằng $\mathbb EL_D(A(S;\xi))$ theo Bước 1; tính hữu hạn của $\mathbb E\,\ell(A(S;\xi),Z_i)$ chứng minh bằng Định nghĩa 06.9 với quan sát kiểm tra $z_i$, lấy kì vọng theo $(S,Z')$ bằng Fubini cho hàm không âm: $\le\mathbb EL_D(A(S;\xi))+\epsilon_{\mathrm{stab}}(m)<\infty$; ghi "tính ổn định đều được dùng ở đây". Câu cuối khối định lý: "Giả thiết khả tích và tính ổn định đều kéo theo $\mathbb EL_S(A(S;\xi))<\infty$ (Bước 2 của chứng minh)." |
| N1 | 108 | Câu mới: chứng minh ở §7 thêm một quan sát $Z'\sim D$ độc lập với mẫu và nguồn ngẫu nhiên; quan sát kiểm tra là một điểm bất kì của $\mathcal Z$, không ngẫu nhiên. |
| N2 | 1130 | Mục §13 đổi thành "Số quan sát của SGD": UML §14.5.1 đếm $T$ quan sát, học phần đếm $T-1$. |
| TB1 | 1032, 1051 | Nhận xét 06.14, ý "Chia khối và xác thực": nêu điều kiện hàm lỗi trong $[0,1]$ ((T3) của Hệ quả 04.17), $k=\lceil\log_2(2/\delta)\rceil$ khối, mỗi khối đủ cho mức kì vọng $\epsilon/4$, mẫu xác thực cỡ $8\ln(4k/\delta)/\epsilon^2$ (Bài tập 06.7); với hồi quy logistic, chọn bằng hàm lỗi bị chặn (0–1). §10: "Khi $B$ chưa biết và hàm lỗi bị chặn". |
| TB2 | 626, 1043, 1117, 1283 | 626: "Bài 08 dùng dạng này cho SGD với hàm lỗi lồi, trơn và Lipschitz"; 1043: câu về SGD nhiều vòng bỏ (trùng §10); 1117: "Với hàm lỗi lồi, trơn và Lipschitz, …"; 1283: thêm cùng điều kiện; "bằng chính $L_D$" thành "xấp xỉ $L_D$". |
| TB3 | 96, 103, 118 | Bảng §2: dòng $B$ ("bán kính quả cầu tâm $0$: của $W$ khi $W$ là quả cầu, hoặc của tập điểm so sánh $W_B$ (§9)"), dòng $R$; $C_x$, $C_y$. §1 mục 6 không còn dùng $B$ ("các điểm của $W$ có chuẩn không quá một số cho trước (§9)"); bảng §1 ghi "(§2)" sau các hằng số. |
| TB4 | lần dùng đầu | Định nghĩa tại chỗ sau Hệ quả 06.2: "rủi ro vượt mức kì vọng: kì vọng theo mọi nguồn ngẫu nhiên của rủi ro vượt mức (Định nghĩa 01.24) so với $W$, tức của sai số ước lượng (Định nghĩa 04.1)". "Rủi ro thực nghiệm kì vọng" (ôn nhanh 2) và "sai số tối ưu thực nghiệm kì vọng" (Mệnh đề 06.5) đổi thành "kì vọng của …". |
| TB5 | 1047 | §10 mở bằng câu trả lời: tối ưu là học khi oracle không chệch cho $L_D$ (quan sát mới, Hệ quả 06.2), hoặc khi thuật toán trên mẫu cố định có khoảng cách tổng quát hóa kì vọng nhỏ, như ERM có chính quy hóa nhờ ổn định đều (Định lý 06.10, Mệnh đề 06.11). |
| TB6 | 758–787, 830, Phụ lục B | $u$, $v$ đổi thành $\hat w$, $\hat w'$ trong chứng minh Mệnh đề 06.11, Ví dụ 06.6 Bước 2, Ví dụ 06.7 Bước 3, Phụ lục B. Bổ đề 06.7 giữ $u$ (điểm cực tiểu tổng quát). |
| TB7 | 467, 628, 632, 895, 249, 650, 122 | Tiếng Anh: quadratic growth, constant algorithm, exchange argument (đặt tên ở câu dẫn và lộ trình Định lý 06.10), oracle inequality (kèm câu giải thích mốc $\inf_u[L_D(u)+\tfrac\lambda2\lVert u\rVert^2]$, chỉ tính được khi biết $D$). "Cấp thuật toán"/"cấp lớp" giải thích một lần sau Hệ quả 06.2. Dòng 122: "hàm lỗi logistic của mô hình tuyến tính (hàm lỗi log của Nhận xét 02.11)". |
| TB8 | 410–418, 706–716, 628, 703 | Ví dụ 06.3 Bước 3: thêm dòng $\sum_tc_t^2+\tfrac1m\sum_{t\ne s}c_tc_s$ và đẳng thức $\sum_{t\ne s}c_tc_s=(\sum c)^2-\sum c^2$; câu "Bước 4 cần thêm mô-men chéo". Ví dụ 06.5: một thiết lập ($X\sim U[0,1]$, $Y=\mathbb 1[X>\tfrac12]$, $h_0\equiv0$), công thức $2^{-m}\sum_k\binom mk\lvert k/m-\tfrac12\rvert$, lý do $1/\sqrt{2\pi m}$. Dòng 628 tách ba câu. Dòng 703 viết thẳng. |
| TB9 | Phụ lục E | Phản ví dụ mới: lớp hàm chỉ thị $h_C$ của tập hữu hạn, $\ell(h,z)=h(z)$, $A(s)=h_{\{z_1,\ldots,z_m\}}$; vế trái điều kiện thay một theo trung bình $\le0$ dưới mọi $D$ (điều kiện một phía đúng với $\epsilon=0$), hệ số ổn định đều nhỏ nhất bằng $1$. Tên mục UML §13.2 ghi đúng ("Stable Rules Do Not Overfit"); thêm "hàm giảm $\epsilon(m)$". |
| TB10 | 872, 1123, 1075 | UML §12.2.1 (Ví dụ 12.9) cho dữ liệu không bị chặn; §12.2.2 cho bài toán lồi–Lipschitz–bị chặn. "UML Bài tập 14.8.1" thành "UML Bài tập 14.1"; `outline.md` đổi theo (cả 14.8.2 thành 14.2). |
| TB11 | 996–1003 | Ví dụ 06.11 Bước 3 dùng $\lambda^*$: $\epsilon_{\mathrm{stab}}=0{,}005$, số hạng khớp $0{,}005$, tổng $0{,}01$; kết luận mở bằng hai câu trả lời của câu hỏi thực hành ($0{,}005$ và $0{,}01$). |
| TB12 | Hình 06.1 | Script sửa: nhãn "0,615" sát trên mũi tên, dưới đường cong; nhãn "0,178" bên phải mũi tên (khoảng cách hẹp), không chạm đường gióng, điểm hay trục; chú giải "mẫu S⁽⁴⁾"; chú thích thêm "hai khung dùng thang tung khác nhau"; Ví dụ 06.4 Bước 4 dẫn "(Hình 06.1)". SVG sinh lại, đã xem ở 564 px và 317 px. |
| TB13 | 630 | "tại quan sát kiểm tra $z=(1,-1)$ đổi $304/169\approx1{,}7988$, giá trị lớn nhất trên $\mathcal Z$"; bỏ "dò trên lưới". |

## Phát hiện nhẹ của năm báo cáo

| Người rà | Dòng | Xử lý |
|---|---|---|
| R1 | 3 | "độ chênh tối ưu (suboptimality) của một hàm $F$ khi oracle gradient ngẫu nhiên (stochastic gradient oracle) không chệch cho $F$". |
| R1, R5 N5 | 124 | "(C), (G1), (G2) của Bài 05, dùng ở §4"; "mức (O1) của Bài 01 cho mục tiêu có chính quy hóa"; câu chủ động "Ta giả sử …" (R4). |
| R1, R4 | 122 | Sửa như TB7; thêm "hay tính trơn (§8)"; "Các kết quả chính của bài không giả sử hàm lỗi bị chặn" (vì ý chia khối của Nhận xét 06.14 cần hàm lỗi bị chặn). |
| R1 | 374 | Lý do hữu hạn: "$\ell$ nhận giá trị thực và $L_D<\infty$ trên $W$". |
| R1, R2 | 574 | Thêm "khi giá trị này thuộc $W$ (luôn đúng với $W=\mathbb R$)". |
| R1, R4 | 626 | Viết lại câu "Nếu thay hiệu hai kì vọng bằng …". |
| R1 | 628, 630 | "hệ số ổn định nhỏ nhất bằng $1$". **Không áp dụng** câu định nghĩa thêm "số nhỏ nhất … được gọi là hệ số ổn định của $A$": thêm vào Định nghĩa 06.9 sẽ đổi nghĩa của $\epsilon_{\mathrm{stab}}(m)$ dùng trong Mệnh đề 06.11 (một cận, không phải giá trị nhỏ nhất); viết "nhỏ nhất" tại chỗ là đủ. |
| R1, R3 | 836–842 | Ví dụ 06.7 Bước 3 viết rõ $\tfrac2m\lvert\hat w-\hat w'\rvert^2\le\tfrac{2G}m\lvert\hat w-\hat w'\rvert$; kết luận thêm "(Bài 07)" cho hội tụ đều. |
| R1, R4 | 846–852 | Ví dụ 06.8: hàm lỗi $10-zw$, $G=1$; lý do $\mathbb E\bar z^2=1/m$; thêm $L_D-L_S=\bar z^2/\lambda$; tiêu đề mới (R4). |
| R1 | 870 | Thêm câu cho $m$ bất kì: $\hat w_S=2/3$, chọn $M=m$ làm nghiệm trên mẫu lân cận dần về $0$. Câu tách đôi (R4). |
| R1 | 881 | $C$ đổi thành $C_0$. |
| R1, R4 | 445, 597 | Thống nhất "Bài 02–04"; câu thứ hai mở §7 bỏ. |
| R1, R2, R3, R5 | 1117 | "xấp xỉ $L_D$". |
| R1 | Hình | Xem TB12. Không dùng chung thang tung: thang $\lambda=4$ cần tới $2{,}5$, thang chung làm khung trái mất chi tiết; ghi trong chú thích như quyết định cho phép. |
| R1, R4 | 304 | "Hai chế độ của §1 khác nhau ở việc dùng lại quan sát; lưu mẫu mà dùng mỗi quan sát một lần vẫn cho cận của Hệ quả 06.2"; ngoặc "(… bán kính $5$ giả định, $w_1=0$, nên $R=5$)". |
| R1, R4 | 551 | Câu "hệ quả, không phải giả thiết" và câu đo được bỏ; câu ý nghĩa mới sau $\square$; câu đo được giữ ở Phụ lục A. |
| R2 | 729 | Câu sau (L) viết lại: điều kiện trên giá trị hàm lỗi tại các điểm của $W$, không cần tập mở. |
| R2 | Phụ lục A | "tách được bởi một siêu phẳng qua gốc" (có $w$ với $\tilde y_i\langle w,x_i\rangle>0$ mọi $i$). |
| R2, R3 | 1279 | Xem TB9. |
| R3 | 1128 | Thêm "khác biệt này đến từ lập luận đối xứng, không từ chuẩn hóa". |
| R3 | 754 | "không phụ thuộc trực tiếp vào $p$, $D$ hay bán kính của $W$; với hàm lỗi bình phương, $G$ phụ thuộc bán kính". |
| R3 | 1049 | "cận của ERM có chính quy hóa không phụ thuộc số chiều $p$, còn cỡ mẫu cho hội tụ đều tăng theo $p$". |
| R3 | 1281 | Trùng $w_1$: không còn, vì phản ví dụ đã thay. |
| R4 | 467 | "Các lập luận về ERM có chính quy hóa ở §8–§9" (cũng R5 N7). |
| R4 | 461, 505 | Câu sau Định nghĩa 06.6 viết "Khi $\ell(\cdot,z)$ lồi …, như chứng minh dưới đây" (không còn "bổ đề dưới đây" không số); thêm câu dẫn trước Bổ đề 06.8. |
| R4 | 530 | Ngoặc "(câu ôn nhanh 1 …)" bỏ. |
| R4 | 79 | Xem TB4. |
| R4 | 698, 220 | Câu ý nghĩa sau $\square$ của Định lý 06.10 và Bổ đề 06.1 viết lại theo đề xuất. |
| R4 | 701 | Bỏ in đậm. |
| R4 | 779 | "vế trái của (a) bằng $0$" thay "hiển nhiên". |
| R4 | 372, 393 | "thay vì dùng", "chỉ chặn". |
| R4 | 452–456 | Nhãn "Quy tắc" đổi thành "Đầu ra". |
| R4 | 1023–1032 | Nhãn song song ("Loại cận", "Bất đẳng thức Markov", "Chia khối và xác thực"); câu viết lại (TB1). |
| R4 | 725–727 | (L) viết thành câu, không danh sách một dòng. |
| R4 | §9 | "số hạng ổn định", "số hạng khớp" dùng thống nhất; tiêu đề "Đánh đổi khớp–ổn định". |
| R4 | 30, 34 | Mục tiêu 1 rút gọn; mục tiêu 5 tách bằng dấu chấm phẩy. **Không** tách thành mục tiêu 6: sẽ phải đánh số lại ánh xạ mục tiêu–bài tập ở §11 và dàn ý. |
| R4 | 834, 977 | Ví dụ 06.7 Bước 2 thêm $\sum x_iy_i=\pm1$, $\sum x_i^2=1$; Ví dụ 06.10 Bước 3 tách hai phép tính thành hai công thức. |
| R4 | 1123 | Định dạng tiếng Anh ở §13. |
| R4 | 1072 | Tiêu đề Bài tập 06.7 theo quyết định: "Cận với xác suất cao và tăng độ tin cậy cho ERM có chính quy hóa". |
| R4 | 650, 1034 | Câu "Không bước nào … $\mathbb E\lvert L_D-L_S\rvert$" bỏ; giữ ở Định lý 06.10, Ví dụ 06.5, §10 (theo quyết định). |
| R5 N1 | 181 | Câu kết §3 bỏ. |
| R5 N2 | 397 | "khác mẫu cố định của Ví dụ 06.1". |
| R5 N4 | 20, 311 | "Với $\bar w_T$ là điểm lặp trung bình"; "gradient ngẫu nhiên $g_t$". |
| R5 N5 | Phụ lục A, 1141 | **Không áp dụng** đổi "(§4 của Bài 05)" thành "(Mệnh đề 05.3(a))": Mệnh đề 05.3(a) chỉ cho trường hợp khả vi; tính khác rỗng của dưới vi phân hàm lồi hữu hạn được nêu ở §4 Bài 05 (dẫn UML §14.2). |
| R5 N9 | 947, 994 | Ghi $\mathbb E_S$ trong chứng minh Hệ quả 06.13 và Ví dụ 06.11. |
| R5 N12 | Phụ lục D | $c_t$, $y_t$, chỉ số $k$ cho điểm lặp. |
| R5 N13 | 1117 | Hai câu đầu cầu nối thay bằng một câu dẫn §10. |
| R5 N14 | 886 | **Không áp dụng** (đề xuất tùy chọn; hết ngân sách chữ). |
| R5 N15 | 628 | Câu "Thuật toán hằng … $=0$" sau Định nghĩa 06.9 bỏ. |
| R5 N16 | `ky-hieu.md` | Điều phối viên đã thêm $W_B$. |
| R5 cắt 3 | §10 | **Không áp dụng** bỏ mục giới hạn "SGD nhiều vòng": sau khi câu cuối §9 bị cắt, mục này là chỗ duy nhất trong §10 nêu giới hạn đó; rút còn một câu. |

## Các chỗ cắt để bù chữ (thân bài)

1. Câu kết §3 (R4 181), câu kết §6 (R4 593), câu kết §8 (R4 889), câu thứ hai của đoạn mở §7 (R4 597), câu thứ hai cuối §9 (R4 1043).
2. Sau Định nghĩa 06.4: câu về chữ "kì vọng" trong tên.
3. Lời giải ôn nhanh 1: câu "Hai số bằng nhau, …".
4. Mệnh đề 06.5: câu cuối sau $\square$ ($\mathbb E\inf_WL_S\le\inf_WL_D$, R1) và câu "Cận chỉ theo kì vọng …".
5. Đoạn sau Định nghĩa 06.6: câu kí hiệu $F_{S,\lambda}$ (đưa vào dòng **Đầu ra**, R5 cắt 4), câu "Hồi quy ridge một chiều là ví dụ …".
6. Bổ đề 06.7: câu "Mọi cận khoảng cách … đi qua bất đẳng thức này".
7. Kiến thức tiên quyết: Bài 01 và Bài 05 chỉ còn số hiệu (bỏ tên khái niệm lặp lại).
8. Nhận xét 06.12 rút gọn (bảo đảm viết ở dạng đã thay $C_0$; ý áp dụng cho hàm lỗi bình phương giữ).
9. Ví dụ 06.6 Bước 3 gộp vào kết luận; Ví dụ 06.7 Bước 1 rút gọn; Ví dụ 06.11 Bước 4 rút gọn, câu "Định lý 06.10 chỉ cần tính khả tích" bỏ.
10. Câu thừa trong thiết lập Ví dụ 06.9, 06.10, 06.11 và Bước 1 Ví dụ 06.5 ("hoặc trực tiếp theo Mệnh đề 01.7").
11. §10: các số lặp của Ví dụ 06.3, câu "Định lý 06.10 và Mệnh đề 06.11 không dùng chiều VC" (R5 cắt 5), câu về mẫu kiểm tra độc lập (R4), rút các mục giới hạn.
12. §13: mục "Tập tham số" của "Quan hệ với UML".
13. Câu "Quan sát này không phải mẫu bóng $S'$ …" rút còn một mệnh đề.

## Kiểm tra (từ gốc repo, sau biên tập)

`forward_refs.py`: 0. `sync-local-materials.py` và `--check`: OK. `git diff --check`: sạch. Khối `:::` cân bằng, không lồng. Viewer (cổng 8771) qua HTTP và `file://`, 1600×900 và 390×844, mọi `details` mở: 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức/bảng tràn (ba công thức mới của C1 và Mệnh đề 06.11 Bước 4 tràn ở lần chạy đầu, đã tách dòng); Hình 06.1 tải được (naturalWidth 564, rộng 317 px ở 390). Bản in 50 trang.

## Vòng 2 (2026-10-31)

Căn cứ: `reviews/6-ra-lai-toan.md` (R2'), `reviews/7-ra-lai-mach.md` (R5'), mục "Rà lại sau vòng 1 — quyết định" của `review-log.md`. Script: scratchpad `writer06/ed11.py`. Số tiếng: thân bài 11 974 → 11 989; phụ lục 1 513 → 1 515.

| Mã | Dòng (bản vòng 1) | Đã sửa thế nào |
|---|---|---|
| R2' trung bình; QĐ 1 | 1051 | Bỏ câu chọn bằng hàm lỗi 0–1; thay bằng: với hàm lỗi không bị chặn như logistic, cách chia khối cần thêm một cận cho hàm lỗi trên các ứng viên, ngoài phạm vi bài. Câu tách đôi, có chủ ngữ "ta" (R5' M12). §10 (1068) đã ghi "Khi $B$ chưa biết và hàm lỗi bị chặn", không có cùng lỗi, giữ. **Không áp dụng** phương án R2' thêm cận $\ln2+\sqrt{2\ln2/\lambda}$: chi tiết ngoài phạm vi theo QĐ 1. |
| R5' M1; QĐ 2 | 901, 937, 1036 | 901: bỏ "số hạng khớp", giữ $\mathbb E[L_S(\hat w_S)-L_S(u)]$. 937 giữ hai tên cho các số hạng của cận. 1036: "trong khi khoảng cách tổng quát hóa bằng $0$. Nguyên nhân là phần $L_S(\hat w_S)-L_S(u)$ với $u=1$, bằng $L_D(\hat w_S)$ và tăng theo $\lambda$." |
| R5' M2; QĐ 3 | 1064 | "dù kì vọng của sai số tối ưu thực nghiệm chỉ là $0{,}0011$; khoảng cách tổng quát hóa kì vọng ở đó là $0{,}4750$". |
| R2' nhẹ | 547 | Thêm "(tính đo được giả sử như cuối Phụ lục A)". |
| R2' nhẹ | 1287 | "một hàm không tăng $\epsilon(m)$". |
| R5' M3 | 591 | "Cận dưới đây không dùng cấu trúc của lớp, chỉ dùng một tính chất của chính thuật toán". |
| R5' M4 | 1060 | Câu cắt. |
| R5' M5 | kết §3, §6, §8 | Không sửa ghi chú; ghi vào `outline.md` §13.2. |
| R5' M6 | 845 | "Với $\hat w$, $\hat w'$ là hai nghiệm ERM, …". |
| R5' M7 | 713, 1295 | "Các đẳng thức ở Bước 1–3 cho thấy …". |
| R5' M8 | 1077 | "nói chung không lồi". |
| R5' M9 | 937 | "Theo cách gọi của Bài 04, phần (b) là một *bất đẳng thức oracle* …: nó so đầu ra với mốc …, và mốc này chỉ tính được khi biết $D$." |
| R5' M10 | 1089, 1091 | Tiêu đề Bài tập 06.7 "Cận với xác suất cao và tăng độ tin cậy từ một cận kì vọng"; Bài tập 06.9 "Ổn định thay một theo trung bình …"; `outline.md` đồng bộ. |
| R5' M11 | 413 | "Ở Bước 4, ta cần thêm mô-men chéo." |
| R5' M12 | 1051 | Tách câu (xem dòng đầu). |
| R5' M13 | 117 | Dấu chấm phẩy thành dấu chấm. |
| R5' M14 | 882 | "còn với $M=m$, nghiệm trên mẫu lân cận dần về $0$ khi $m$ tăng". |
| R5' M15 | 854 | "(chứng minh ở Bài 07)". |
| R5' M16 | 896, 1140 | 896: "… Dữ liệu bị chặn và tính trơn là giả thiết khác mà Nhận xét 02.11 hứa …"; 1140: định dạng ngoặc như các mục khác. |
| Bù chữ | 582; Ví dụ 06.11, 06.12 | Câu cuối Kết luận Ví dụ 06.4 cắt (theo QĐ); "Tổng hai số hạng" thành "Tổng"; bỏ vế "ví dụ không cần $G$ hữu hạn" ở Ví dụ 06.12 (vế này không còn cần sau khi câu không nói tới số hạng ổn định). |

Kiểm tra: sync và `--check` OK; `forward_refs.py` 0; `git diff --check` sạch; 41 khối `:::` cân bằng; viewer qua HTTP ở 390×844, mở mọi `details`: 0 `.katex-error`, 0 công thức hay bảng tràn, 0 lỗi trang, 0 yêu cầu hỏng, Hình 06.1 tải được (naturalWidth 564). Máy chủ đã tắt.

## Vòng 3 (2026-10-31)

Căn cứ: `reviews/8-ra-lai-vong-2.md` và quyết định của điều phối viên (bốn điểm). Thân bài 11 989 → 11 996 tiếng; phụ lục 1 515 → 1 518.

| Mục | Dòng (bản vòng 2) | Đã sửa thế nào |
|---|---|---|
| QĐ 1 (trung bình) | 1051 | Thêm câu bảo đảm: "Khi đó, với xác suất ít nhất $1-\delta$ theo mẫu, đầu ra được chọn có rủi ro vượt mức không quá $\epsilon$; số khối tăng theo $\log_2(2/\delta)$, thay cho thừa số $1/\delta^2$ của bất đẳng thức Markov." Không thêm hằng số ngoài kế hoạch Bài tập 06.7. "((T3) …)" thành ", tức (T3) của Hệ quả 04.17,". |
| QĐ 2 | 1036 | Kết luận Ví dụ 06.12 viết thẳng: "Số hạng phạt kéo $\hat w_S=1/(1+\lambda/2)$ ra xa điểm tốt nhất $1$, nên $L_D(\hat w_S)$ tăng theo $\lambda$ dù khoảng cách tổng quát hóa bằng $0$." Câu đầu cũ ("Rủi ro tăng theo $\lambda$ trong khi …") bỏ vì trùng ý, để vừa trần chữ. |
| QĐ 3 | Phụ lục E, 1293 | "Khi $\mathbb EL_D(A(S))<\infty$, các đẳng thức ở Bước 1–3 …". |
| QĐ 4 | 117, 1040 | Cắt "Tính bị chặn của dữ liệu chỉ cần cho …" và "Ba điểm phân biệt hai loại bảo đảm." |

Sau bốn mục, thân bài lên 12 012 tiếng; hai chỗ rút gọn trong chính các câu vừa sửa (bỏ câu đầu trùng ý ở kết luận Ví dụ 06.12, "cách dùng bất đẳng thức Markov" thành "bất đẳng thức Markov") đưa về 11 996.

Kiểm tra: sync và `--check` OK; `forward_refs.py` 0; `git diff --check` sạch; 41 khối `:::` cân bằng; viewer qua HTTP (cổng 8773) ở 390×844, mở mọi `details`: 0 `.katex-error`, 0 công thức hay bảng tràn, 0 lỗi trang, 0 yêu cầu hỏng, Hình 06.1 tải được. Máy chủ đã tắt.
