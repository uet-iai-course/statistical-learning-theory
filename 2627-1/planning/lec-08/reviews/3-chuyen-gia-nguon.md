# Rà 3 — Chuyên gia lý thuyết học và trung thành nguồn — Bài 08 (bản đóng băng `lec08-draft-frozen.md`)

Người rà 3, chỉ đọc repo. Số dòng theo bản đóng băng. Script kiểm số: scratchpad `rv3_08/chk.py`.

## Tổng kết theo mức

| Mức | Số | Mã |
|---|---|---|
| chặn bàn giao | 0 | — |
| nghiêm trọng | 0 | — |
| trung bình | 6 | F1–F6 |
| nhẹ | 12 | F7–F18 |

Đánh giá chung: chuẩn lý thuyết học đạt. Mọi phát biểu hình thức nêu cơ chế lấy mẫu (chỉ số đều có hoàn lại, $\xi$ độc lập với $S$), giả thiết (S), (G), $\eta_t\le2/\beta$, tập $W$ và phép chiếu, đầu ra ($w_{T+1}$ ở Định lý 08.6, $\bar w_T$ ở Hệ quả 08.7–08.8), cái gì cố định và ngẫu nhiên (bảng §1, dòng 82–90). Ghi chú phân biệt khoảng cách tổng quát hóa kì vọng (08.6, 08.7), rủi ro vượt mức kì vọng (08.8) và tính dừng (08.12); phân biệt cấp lớp với cấp thuật toán (dòng 872); không chuyển sang ReLU, hàm lỗi bản lề, mạng sâu (Ví dụ 08.10, §10); dừng sớm không được nói là luôn tốt (dòng 678, 695, 874); chính quy hóa ngầm là hành vi chọn lựa (dòng 688–693, có một lưu ý ở F3); thí nghiệm có mẫu kiểm tra $5000$ điểm, $20$ hạt giống, khoảng nhỏ nhất – lớn nhất, giả thiết thỏa được nêu (Ví dụ 08.6 Bước 1). Nhận xét 08.11 phát biểu đúng Định lý 3.12 của HRS (hàm lỗi trong $[0,1]$, $L$-Lipschitz, $\beta$-trơn, $\alpha_t\le c/t$ không tăng; công thức khớp từng thừa số) và ghi "đọc thêm". Không thấy đoạn nào dịch sát HRS hay UML; chứng minh tính không giãn và tính đồng bức là dạng chuẩn, cách trình bày của học phần (hàm phụ $q_u$, chú thích chỗ dùng giả thiết) khác Phụ lục A của HRS.

Mọi hằng số tôi tính lại đều khớp: $\mathbb E\Delta_2=\tfrac14$, $\mathbb E\Delta_3=\tfrac{29}{64}$, $\mathbb E\Delta_7=\tfrac{228203}{262144}$ (liệt kê đủ $4^6$ dãy, phân số chính xác); Ví dụ 08.8: $\Delta_3/\Delta_2=1{,}1000$, $\Delta_{21},\Delta_{41},\Delta_{61},\Delta_{81},\Delta_{101}=0{,}0061;0{,}0411;0{,}2753;1{,}529;2{,}879$, lần đầu vượt $0{,}2$ tại $\Delta_{58}\approx0{,}207$, giới hạn $\pi$; $(1{,}1)^{100}\approx13\,780{,}6$ và $275{,}59$; Nhận xét 08.11: $33{,}369\le33{,}37$; Ví dụ 08.7: $0{,}08660$, $0{,}07906$, $0{,}07246$, $0{,}07071$, $T^*=7071{,}07$, $0{,}09571$, $0{,}099995$, $0{,}137495$, $0{,}279995$, $\eta^*\approx0{,}0289$; $39{,}975$; câu hỏi cuối buổi $28{,}184\le28{,}19$, $0{,}011276\le0{,}0113$. Các bảng Huber (Ví dụ 08.1, 08.2), Ví dụ 08.9, 08.10 tính tay: khớp.

## Bảng kiểm blueprint §E: 12/12 (mục 1, 3, 12 đạt kèm lưu ý)

| # | Mục §E | Kết quả | Bằng chứng |
|---|---|---|---|
| 1 | Một bảng kí hiệu; không dùng $d$ hai nghĩa | đạt (lưu ý F16) | $\Delta_t$ phân biệt với Bài 05 (dòng 115); $G$ thay $L$, $m$ thay $n$ (dòng 948). Kí hiệu cục bộ $d$ (dòng 268) và $c$ hai nghĩa (dòng 225, 796) |
| 2 | Mỗi định lý nêu cơ chế lấy mẫu, hàm lỗi, đối tượng so sánh, nguồn ngẫu nhiên, loại bảo đảm | đạt | 08.5 (dòng 313–335), 08.6 (408–439), 08.7, 08.8 (587–617, đối tượng so sánh $\inf_WL_D$), 08.10, 08.11, 08.12 (861: tính dừng) |
| 3 | Chú thích giả thiết trong chứng minh; ít nhất một ví dụ hỏng | đạt (lưu ý F1) | mọi bước gắn (S), (G), $\eta_t\le2/\beta$, (T1), (T2); phản ví dụ: Ví dụ 08.3, 08.8, 08.9, 08.10, ghép cặp sai (dòng 193) |
| 4 | Kết quả là phát biểu của học phần; dẫn UML theo mục; không số định lý chưa kiểm | đạt | chỉ UML §13.1–13.2, §20.6, §20.9, §31.1; số định lý HRS (3.8, 3.12) đã kiểm tr. 9, 12; khai báo ở dòng 946 |
| 5 | Phân biệt bảo đảm cấp lớp và cấp thuật toán | đạt | dòng 3, 70, 439, 872 |
| 6 | Nói rõ đại lượng được chặn | đạt | dòng 439 (không phải $\mathbb E\lvert L_D-L_S\rvert$, không phải $L_D$), 617, 861, 884–888 |
| 7 | Không chuyển kết quả hàm lỗi bị chặn sang bình phương/log | đạt | kết quả chính không cần hàm lỗi bị chặn (dòng 105); bình phương cần $W$ bị chặn (113, 887); Nhận xét 08.11 nêu $[0,1]$ |
| 8 | Không chuyển cận lồi sang mạng nơ-ron | đạt | Ví dụ 08.10 Bước 3, dòng 866, 878–880, câu hỏi cuối buổi (d) |
| 9 | Một ví dụ số và một câu hỏi cuối buổi | đạt | Ví dụ 08.4, 08.5, 08.7; §12 (a)–(d) có lời giải |
| 10 | Tách bài gốc và bài UML; không bịa số bài UML | đạt | §11: tám bài gốc; lý do không có bài UML đúng (UML tr. 282–283: §20.9 không có bài về SGD hay ổn định) |
| 11 | Chứng minh dài để ở phụ lục | đạt | tính đồng bức (A), xáo trộn lại và đo được (B), điểm dừng (C) |
| 12 | Thí nghiệm có mẫu kiểm tra độc lập, nhiều lần chạy, không coi là chứng minh | đạt (lưu ý F13) | dòng 11, 25, 534–540, Phụ lục D |

## Đối chiếu blueprint (Lecture 8, đầu Lecture 9, §C, §D)

- **8.1:** đủ. Thí nghiệm mở đầu đổi "cùng kiến trúc" thành hồi quy logistic (QĐ 7, đã chấp nhận); có câu trả lời sai hấp dẫn (dòng 23) và năm mục tiêu.
- **8.2:** đủ. Chỉ số đều có hoàn lại (Thuật toán 08.1), ghép cặp cùng khởi tạo và dãy chỉ số (Định nghĩa 08.2), $\Delta_t$, $\beta$, $G$, ngân sách độ dài bước. Bản có chiếu thay bản không chiếu (QĐ 2), gồm $W=\mathbb R^p$; (S) đặt trên toàn $\mathbb R^p$ đúng với yêu cầu "miền mà tính chất ánh xạ gradient đúng".
- **8.3:** đủ, đúng độ sâu.
  - Lemma 8.1 [S] = Bổ đề 08.4 [S], tính đồng bức ở Phụ lục A (đúng §D: "smooth-gradient co-coercivity" ở phụ lục).
  - Prop 8.2 [F] = Mệnh đề 08.5 [F]: điểm trung gian đúng như blueprint; viết trên từng quỹ đạo trước (QĐ phân tích nguồn §2.2).
  - Thm 8.3 [F] = Định lý 08.6 [F]: tổng $\sum_{t=1}^T$ do đánh số từ $w_1$ (QĐ 1); có câu "không cho mọi thuật toán tối ưu" (dòng 439).
  - Corollary [F]: bước hằng $2G^2\eta T/m$ (dòng 439), Hệ quả 08.7, 08.8 [F]; "không chứng minh dừng sớm" (dòng 678).
  - Nonconvex extension [S]: Ví dụ 08.8, Mệnh đề 08.10 [S] (thừa số $1+\beta\eta_t$, tích), Nhận xét 08.11 [O]; không dùng lại công thức lồi (dòng 788).
  - Optional appendix [O]: Mệnh đề 08.12 [O], Phụ lục C, đúng hằng số blueprint (chỉ số dịch $0\to1$); "không chặn rủi ro vượt mức hay khoảng cách tổng quát hóa" (dòng 861).
- **8.4:** đủ. Dừng sớm, độ dài bước, độ nhạy dự đoán (tỉ lệ đổi nhãn), chính quy hóa ngầm (Định nghĩa 08.9), ba mức khẳng định (dòng 876–880), ReLU không trơn, không có $G$ đều (Ví dụ 08.10).
- **8.5:** sáu bài gốc + hai bài gốc thêm (QĐ 9).
- **8.6:** tài liệu đọc đủ ba mức (lưu ý F5, F7, F8); cầu nối Bài 09 (dòng 938) đúng câu hỏi blueprint (rủi ro cho mô hình xác suất, quan sát là chuỗi, hàm lỗi log).
- **§C (Recitation 4, Exam 4):** ghép cặp SGD, kiểm tra giả thiết mạng nơ-ron, phân biệt định lý và thí nghiệm: có.
- **Sai khác** đều nằm trong QĐ 1–10 của `review-log.md` và `outline.md` §13.2 (16 mục), trừ F6 (QĐ 1 chưa thực hiện đủ) và F7 (dàn ý dòng 378 yêu cầu một câu về quan sát mới).

## Lời hứa

| Lời hứa | Giữ ở | Kết quả |
|---|---|---|
| Bài 06 dòng 620 (dạng $\mathbb E_\xi\lvert\cdot\rvert$, chung $\xi$, SGD lồi, trơn, Lipschitz) | Định lý 08.6(a), dòng 191 | giữ |
| Bài 06 dòng 1071 (khoảng cách tổng quát hóa kì vọng của SGD dùng lại mẫu) | Định lý 08.6(c), Hệ quả 08.7 | giữ |
| Bài 06 dòng 1130 (SGD nhiều vòng của §5, có chiếu, $\bar w_T$) | Hệ quả 08.7 áp cho Ví dụ 06.3 (dòng 578; đã kiểm Ví dụ 06.3: rút có hoàn lại, $W=[-1,1]$, đầu ra $\bar w_T$; $G=4$, $\beta=2$ đúng), Hệ quả 08.8 | giữ, nói thẳng cận $39{,}975$ không cho thông tin |
| Bài 06 dòng 1295 (dạng mà Bài 08 chặn) | Định lý 08.6(a) | giữ |
| Bài 07 dòng 960 (quỹ đạo, số bước, độ dài bước cho bảo đảm của hàm SGD trả về) | dòng 3 nhắc lại; trả lời ở Định lý 08.6 và dòng 870; Phụ lục D Bài 07 dẫn ở dòng 691 | giữ |

## Trang nguồn đã đọc

- **HRS** (`sources/supp/hardt-recht-singer-2016.pdf`, trang PDF): 1–9 (tóm tắt, §1, §2 Def 2.1, Thm 2.2, Def 2.3–2.4, Lemma 2.5, §3.1–3.3, Def 3.1–3.6, Lemma 3.3, 3.7, Thm 3.8 và chứng minh), 12–14 (Lemma 3.11, Thm 3.12 và chứng minh), 16–20 (Lemma 4.6, Thm 4.7, §5 Lemma 5.1, Thm 5.2, Cor 5.3, Prop 5.4 và thảo luận $\sqrt3$, $\sqrt2$; §6 giao thức và bốn quan sát), 25–28 (cuối §6, §7 "Future Work and Open Problems"), 31–32 (Phụ lục A).
- **UML** (trang PDF): 277–280 (§20.6), 282–283 (§20.9).
- **Ghi chú học phần:** Bài 06 dòng 302–312, 389–420 (Ví dụ 06.3), 618–642 (Định nghĩa 06.9, Định lý 06.10), 1069–1071, 1128–1131, 1265–1280, 1293–1296; Bài 07 dòng 9, 283, 825, 960, 1092–1099 (Phụ lục D).

## Phát hiện

| Mã | mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|---|
| F1 | trung bình | dòng 111, 445–449 (Định lý 08.6 Bước 1); mâu thuẫn với dòng 491, 699, 778 | Bước 1 lấy tính Lipschitz từ (G) qua Mệnh đề 05.5(a), tức có dùng tính lồi trong (S); nhưng dòng 491 viết "tính lồi chỉ qua Bổ đề 08.4(a)", dòng 699 "chỉ đi vào chứng minh qua Bổ đề 08.4", dòng 778 "chỗ duy nhất mà tính lồi từng được dùng". Chú thích chỗ dùng giả thiết vì vậy không nhất quán, và điều này quan trọng cho §9 | dòng 445: "hàm $\ell(\cdot,z)$ lồi theo (S) … Theo Mệnh đề 05.5(a)"; dòng 111: "Khi (S) đúng, (G) kéo theo (L)". Thực ra hàm khả vi với $\lVert\nabla\ell\rVert\le G$ trên $W$ lồi là $G$-Lipschitz trên $W$ theo định lý giá trị trung bình (đã có trong danh sách tiên quyết, dòng 44), không cần tính lồi | Bước 1: "Với $u,v\in W$, đoạn $[u,v]$ nằm trong $W$ vì $W$ lồi; theo định lý giá trị trung bình và (G), $\lvert\ell(u,z)-\ell(v,z)\rvert\le G\lVert u-v\rVert$." Tiêu đề bước: "(G) và tính lồi của $W$". Dòng 111: "(G) kéo theo (L) của Bài 06 vì $W$ lồi (định lý giá trị trung bình)". Khi đó dòng 491, 699, 778 đúng nguyên văn. Số chữ gần như không đổi |
| F2 | trung bình | dòng 180 | "Khi $T>m$, … Hệ quả 06.2 không áp dụng" gợi ý rằng với $T\le m$ hệ quả áp dụng được. Với chỉ số rút có hoàn lại, một quan sát có thể được dùng lại từ bước thứ hai với xác suất dương, nên Hệ quả 06.2 (cần quan sát mới mỗi bước) không áp dụng với mọi $T\ge2$ | Thuật toán 08.1 bước 1 (rút có hoàn lại); Bài 06 dòng 300: "Hệ quả 06.2 cần một quan sát mới cho mỗi bước"; Nhận xét 06.3 là một vòng theo thứ tự, không hoàn lại | "Chỉ số rút có hoàn lại, nên một quan sát có thể được dùng lại ngay từ bước thứ hai; khi $T>m$, mỗi quan sát được dùng trung bình $T/m$ lần. Điểm lặp vì vậy phụ thuộc vào quan sát được dùng, và Hệ quả 06.2 không áp dụng (Nhận xét 06.3)." (+10 tiếng) |
| F3 | trung bình | dòng 691 | "Học phần có chứng minh cho hai trường hợp" rồi nêu trường hợp thứ hai là "ngân sách độ dài bước giới hạn hệ số ổn định như $1/\lambda$". Đây không phải một trường hợp chính quy hóa ngầm theo Định nghĩa 08.9 (chọn nghiệm trong nhiều nghiệm $L_S$ nhỏ như nhau), và chính dòng 491 gọi phép so sánh này là "về dạng công thức, không phải một định lý". Blueprint 8.4 yêu cầu tách chính quy hóa ngầm khỏi định lý đã chứng minh | dòng 491 và 691; blueprint 8.4 "distinguish it … from a proved theorem" | "Học phần có một trường hợp có chứng minh: với ma trận đặc trưng hạng đủ và độ dài bước đủ nhỏ, hạ gradient trên hàm lỗi bình phương, khởi tạo tại $0$, hội tụ tới nghiệm nội suy chuẩn nhỏ nhất (Phụ lục D của Bài 07). Trong Định lý 08.6, ngân sách độ dài bước đóng vai $1/\lambda$ của Mệnh đề 06.11; đó là so sánh về dạng công thức." Xóa câu cuối dòng 491 (≈30 tiếng) vì đã chuyển về đây |
| F4 | trung bình | dòng 950 (§13, "Lập luận truy hồi") | Gạch đầu dòng nằm trong "các khác biệt chính" và viết "kết quả đúng cả khi xáo trộn lại sau mỗi vòng", gợi ý đó là điểm học phần hơn bài báo. HRS tự nêu kết quả đúng cho cả hai cách rút (rút đều, và một hoán vị ngẫu nhiên lặp lại) | HRS tr. 7: "There are two popular schemes … Our results hold for both variants"; tr. 8: "the proofs are almost identical for both rules"; Lemma 3.11 tr. 12 xét cả hai | "Bài báo chia hai trường hợp theo quan sát được chọn rồi dùng tính tuyến tính của kì vọng, và nêu kết quả đúng cho cả rút đều lẫn một hoán vị ngẫu nhiên lặp lại. Học phần viết bất đẳng thức trên từng quỹ đạo trước (Mệnh đề 08.5(a)), nên chỉ cần $\Pr(i_t=i)=1/m$ (Phụ lục B)." (+12 tiếng). Phụ lục B(i) có thể thêm một mệnh đề phụ: "một hoán vị đều dùng lại ở mọi vòng cũng cho $\Pr(i_t=i)=1/m$" |
| F5 | trung bình | dòng 944 | "§6–§7 (thí nghiệm trên mạng sâu, là quan sát thực nghiệm)": §7 của HRS là "Future Work and Open Problems", không phải thí nghiệm. Dẫn sai mục | HRS tr. 25: tiêu đề "7 Future Work and Open Problems"; tr. 25–28 gồm cận xác suất cao, ổn định của hạ gradient, động lượng, chọn mô hình | "§6 (thí nghiệm trên mạng sâu, là quan sát thực nghiệm), §7 (câu hỏi mở)" (+3 tiếng) |
| F6 | trung bình | dòng 948 (§13, "Kí hiệu và chỉ số") | QĐ 1 yêu cầu ghi khác biệt chỉ số với HRS ở §13, trung tính. Gạch đầu dòng chỉ nêu quy ước của học phần, không nói bài báo đánh số thế nào, nên khác biệt chưa được ghi | HRS tr. 6 (Lemma 2.5: $w_0=w'_0$, $\delta_0=0$), tr. 9 (Thm 3.8: "$w_T$ … outputs", $\sum_{t=1}^T\alpha_t$); `review-log.md` QĐ 1 | Thêm sau câu cuối: "Bài báo bắt đầu từ $w_0$ và gọi điểm lặp sau $T$ bước là $w_T$; cận của Định lý 3.8 và của Định lý 08.6 cùng dạng $\frac{2G^2}m\sum_{t=1}^T\eta_t$." (+22 tiếng) |
| F7 | nhẹ | dòng 942 | Mô tả UML §20.6 chỉ ghi "không có định lý ổn định". Thuật toán ở UML rút quan sát mới từ $D$ ở mỗi bước, có suy giảm trọng số và chọn đầu ra bằng mẫu xác thực, nên khác thiết lập mẫu cố định của bài. Dàn ý dòng 378 yêu cầu một câu về điều này | UML tr. 278 ("sample $(x,y)\sim D$", "$\eta_i(v_i+\lambda w^{(i)})$", "best performing … on a validation set"); `outline.md` dòng 378 | "UML §20.6 (SGD và lan truyền ngược; mỗi bước dùng một quan sát mới từ $D$; không có định lý ổn định)" (+9 tiếng) |
| F8 | nhẹ | dòng 943 | "Phụ lục A (tính đồng bức)": Phụ lục A của HRS phát biểu tính đồng bức (A.1) không chứng minh và dùng nó để chứng minh Bổ đề 3.7; dòng 951 đã nói đúng "bài báo dẫn tài liệu tối ưu" | HRS tr. 8 (dẫn Polyak, Nesterov), tr. 31 (A.1) | "Phụ lục A (chứng minh Bổ đề 3.7 từ tính đồng bức)" (+3 tiếng) |
| F9 | nhẹ | dòng 952 | "Hai cách cho cùng kết luận": HRS đọc các thừa số theo hướng tích cực ("at most worse by a factor of $\sqrt3$", "the classical bound does not apply when $T>n$"), còn ghi chú kết luận "không tốt hơn một vòng". Hai bên cho cùng thừa số, không cùng cách đọc. Hệ quả 08.7 có đối ứng ở HRS Thm 4.7 (hằng số $T$, chứng minh ra $T+1$, giả thiết hàm lỗi trong $[0,1]$) nhưng không được nêu | HRS tr. 16–17, 19 | "Hai cách cho cùng các thừa số: …". Tùy ngân sách chữ: "Hệ quả 08.7 ứng với Định lý 4.7 của bài báo, không cần hàm lỗi bị chặn." |
| F10 | nhẹ | dòng 90 | "Trong Định nghĩa 06.9 và ở §4–§7, mẫu $s$ … là các điểm bất kì, không ngẫu nhiên; chỉ $\xi$ là ngẫu nhiên": Định lý 08.6(c) và Hệ quả 08.7 (ở §7) lấy kì vọng theo $(S,\xi)$ | dòng 430–437, 552 | "… ở §4–§6 và trong các phần (a)–(b) của Định lý 08.6, …" (+5 tiếng) |
| F11 | nhẹ | dòng 630 (Hệ quả 08.8 Bước 1) | "Các kì vọng $\mathbb EL_D(\bar w_T)$ và $\mathbb EL_S(\bar w_T)$ hữu hạn như Bước 4 của Định lý 08.6": Bước 4 chỉ chặn $\mathbb EL_D$. Định nghĩa 06.4 cần cả hai | dòng 477–484; Bài 06 Định nghĩa 06.4 | Ở Định lý 08.6 Bước 4 thêm: "Cùng lập luận với $z=Z_j$ cho $\mathbb E_{S,\xi}L_S(w_{T+1})\le L_D(w_1)+G^2\sum_t\eta_t$." (giao người rà toán xác nhận) |
| F12 | nhẹ | dòng 693 | "nhỏ nhất ở khoảng $5$ đến $10$ vòng": lỗi chỉ đo tại $0{,}5;1;5;10;20;50;100$ vòng; trong các điểm đo, nhỏ nhất ở $5$ vòng; cực tiểu thật có thể nằm giữa $1$ và $10$ vòng | `outline.md` §13.1: $0{,}6404$ (1 vòng), $0{,}5894$ (5), $0{,}6027$ (10) | "Trong các thời điểm đo, hàm lỗi logistic trên mẫu kiểm tra nhỏ nhất ở $5$ vòng ($0{,}589$; ở $10$ vòng là $0{,}603$)." |
| F13 | nhẹ | Phụ lục D dòng 1073, 1078; Ví dụ 08.6 Bước 3 dòng 536 | $w^\star$ rút lại cho mỗi hạt giống, nên mỗi hạt giống là một phân bố $D$ khác. Trung bình $20$ hạt giống là trung bình qua $20$ phân bố, không phải ước lượng $\mathbb E[L_D-L_S]$ cho một $D$. So sánh với cận vẫn đúng vì cận đúng cho mọi $D$ | dòng 1073 "rút một lần cho mỗi hạt giống"; dòng 536 "ước lượng $\mathbb E[L_D-L_S]$" | Phụ lục D (không tính vào thân bài): "Mỗi hạt giống cho một phân bố $D$ riêng qua $w^\star$; cận của Định lý 08.6 đúng với mọi $D$, nên đúng cho trung bình qua các hạt giống." |
| F14 | nhẹ | dòng 781 | $275{,}6$ là cận của $\mathbb E\Delta_{T+1}$ (khoảng cách tham số), đặt cạnh miền giá trị $[0,2]$ của hàm lỗi mà không nói bước nhân $G$ | Mệnh đề 08.10(c) chặn $\mathbb E\Delta$ | "… $\approx275{,}6$; nhân với $G=1$, đó cũng là cận cho hiệu hàm lỗi, trong khi …" (+8 tiếng) |
| F15 | nhẹ | dòng 888 | "số hạng này chỉ có cho điểm lặp trung bình" đọc như khẳng định chung | Định lý 05.14 chỉ cho $\bar w_T$ | "… và trong học phần, số hạng này chỉ có cho điểm lặp trung bình (Định lý 05.14, Hệ quả 08.8)" (+4 tiếng) |
| F16 | nhẹ | dòng 225, 268, 796 | $c$ vừa là hệ số giãn (Định nghĩa 08.3) vừa là hằng số trong $\eta_t\le c/t$ (dòng 781, 796); $d$ là kí hiệu cục bộ trong chứng minh Bổ đề 08.4, trong khi `ky-hieu.md` dành $d$ cho chiều VC (§E mục 1) | dòng 225, 268, 781, 796 | Định nghĩa 08.3 dùng $\kappa$ cho hệ số giãn (kiểm `ky-hieu.md` trước); chứng minh Bổ đề 08.4 dùng $\gamma$ hoặc $g_{uv}$ thay $d$ |
| F17 | nhẹ | Mệnh đề 08.10(b), dòng 741–747, 774 | Ở bước khác biệt, chứng minh dùng hệ số giãn $1+\beta\eta_t$; HRS dùng tính bị chặn của bước ($\Delta_t+2G\eta_t$, không giãn), nên thừa số kì vọng là $1+(1-\tfrac1m)\beta\eta_t$. Bản của ghi chú đúng nhưng yếu hơn; không bắt buộc sửa ở mức [S] | HRS tr. 6 (Lemma 2.5, nhánh thứ hai), tr. 13 | Tùy chọn, một câu sau chứng minh: "Ở bước khác biệt có thể dùng $\Delta_{t+1}\le\Delta_t+2G\eta_t$ (bất đẳng thức tam giác), cho thừa số $1+(1-\tfrac1m)\beta\eta_t$." Bỏ qua nếu thiếu chữ |
| F18 | nhẹ | dòng 842 | $G=\sup_x\lVert\chi(x)\rVert$ cần hữu hạn; điều này đúng cho Ví dụ 07.3 nhưng không được nói | Bài 07 dòng 825 ($\lVert x\rVert\le1$, $\lVert v_j\rVert=1$, $\lvert b_{1j}\rvert\le1$) | "… $G=\sup_x\lVert\chi(x)\rVert$, hữu hạn vì $\lVert x\rVert\le1$ (Bài 07, Ví dụ 07.10) …" (+6 tiếng; Bài 07 dòng 824–825 là Ví dụ 07.10, đã kiểm) |

## Ngân sách chữ (thân bài 11 946 / 12 000)

Các sửa F2–F10, F14, F15 thêm khoảng $80$–$90$ tiếng vào thân bài (F13 ở phụ lục; F1 gần như không đổi; F17, F18 tùy chọn). Đề xuất cắt tương ứng, đều là câu lặp:

1. **Dòng 401** (32 tiếng): "Cận của Mệnh đề 08.5 tăng tuyến tính … sau sáu bước." Lặp kết luận Ví dụ 08.4 (dòng 398) và số ở Bước 3. Cắt cả đoạn.
2. **Dòng 491, câu cuối** (≈30 tiếng): "Hệ số ổn định có cùng dạng … không phải một định lý." Chuyển ý về dòng 691 theo F3.
3. **Dòng 25, câu thứ hai** (25 tiếng): "Lỗi phân lớp trên mẫu kiểm tra gần như không đổi … ở $5$, $20$ và $100$ vòng." Lặp nguyên văn số ở dòng 693.
4. **Dòng 870, câu thứ hai** (22 tiếng): "Trong thí nghiệm mở đầu, cận này là $t/200$, … (Ví dụ 08.6)." Lặp gạch đầu dòng "Cận trên" (dòng 885) và Ví dụ 08.6.

Tổng cắt ≈ $109$ tiếng, đủ cho mọi sửa đề xuất và để dư khoảng $20$ tiếng.
