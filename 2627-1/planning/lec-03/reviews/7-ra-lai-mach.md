# Rà lại sau biên tập vòng 1 — mạch lập luận, liên kết và văn phong, Bài 03

**Phạm vi.** Tôi kiểm các phần biên tập viên đã đổi, mỗi phần kèm hai đoạn trước và sau, và mọi ranh giới mục. Bài làm chỉ đọc; không sửa tệp nào của repo và không commit.

**Đầu vào:**

- tệp hiện tại `2627-1/materials/lec-03/lecture-note.md`, 1138 dòng; số dòng trong báo cáo theo tệp này;
- `lec03-round1.diff`;
- `reviews/0-quyet-dinh.md`;
- `bien-tap-vong-1.md`;
- `reviews/4-hoc-thuat-van-phong.md`: từ vòng này tôi kiểm thay cho người rà văn phong;
- báo cáo rà mạch của tôi ở vòng trước (`lec03-review-5-mach.md`).

Các câu sửa đề xuất viết theo `no-ai-slop`, chế độ Detect.

**Kiểm tra máy đã chạy:**

- `forward_refs.py` trên bản chép `scratchpad/fr2/lec-03/lecture-note.md`: **0 tham chiếu tới trước**.
- Số từ thân bài (`awk`, trước `## Phụ lục`): **11 999**.
- Grep `chiều`: ngoài "chiều VC", "số chiều", "nâng chiều" và tên "chiều Vapnik–Chervonenkis", không còn chỗ nào.
- Grep "nửa không gian phẳng", "tăng theo đa thức", "bệnh lý": 0 kết quả.

## Kết luận

Bản biên tập áp dụng đúng gần hết các quyết định.

- §7 theo thứ tự mới đọc liền mạch: mục tiêu → phản ví dụ → hai nhu cầu → (M) → mẫu bóng → (T5) → định lý.
- Cầu nối ghi rõ đối tượng so sánh và không lấn sang nội dung SRM.
- §8 kết bằng một giới hạn cụ thể.
- §9 không còn chép lại các con số.

Còn một lỗi **nghiêm trọng** do chính bước biên tập tạo ra: dòng 574 và 576 trùng nhau từng chữ. Còn một lỗi **trung bình**: câu ở §9 (dòng 874) khẳng định "Mỗi giả thiết của Định lý 03.15 đều được dùng" và đưa Ví dụ 03.6 làm bằng chứng. Nhưng chiều VC hữu hạn không phải giả thiết của Định lý 03.15(a). Hơn nữa đoạn đó đưa bằng chứng về tính cần của giả thiết, trong khi câu mở nói về chỗ dùng chúng.

Cả hai sửa đều cục bộ và làm thân bài ngắn đi. Xóa đoạn trùng giải phóng khoảng 45 từ, đủ bù mọi đề xuất dưới đây.

**Thống kê phát hiện mới:** chặn bàn giao 0; nghiêm trọng 1; trung bình 1; nhẹ 8.

**Kết luận bàn giao: chưa giao được.** Giao được sau khi sửa phát hiện nghiêm trọng S1 và trung bình S2. Hai sửa này chỉ cần kiểm lại dòng sửa, không cần một vòng rà đầy đủ.

## 1. Trạng thái các quyết định và phát hiện

| Mục | Trạng thái | Bằng chứng (dòng trong tệp hiện tại) |
|---|---|---|
| N1 bảng §1 | ✓ | 65: "viết theo một đại lượng của lớp (định nghĩa ở §4)". 72: "véc-tơ giá trị $(h(X_1),\ldots,h(X_m))$ của mỗi $h$". Hàng "Chỉ trong chứng minh" đã bỏ. 590: "nó chỉ dùng trong chứng minh". 596: "chúng cũng chỉ dùng trong chứng minh". |
| N2 chữ "chiều" | ✓ | 19 "bằng cận dưới và cận trên"; 180 tiêu đề Nhận xét 03.4; 782 "điều kiện đủ … điều kiện cần"; 794 "Điều kiện cần, không dùng (M)"; 821 "(4)⇒(6)"; 883 tiêu đề Bài tập 03.2; 934. Grep không còn nghĩa "hướng". |
| N3 nguồn cận dưới | ✓ | 862: "UML §6.4 phát biểu …; UML §28.2 chứng minh phần (a); UML không chứng minh phần (b)." 925: §28.1, §28.2, §28.3 đúng nội dung. |
| M1 câu hỏi mở đầu | ✓ | 11, 114: "Bao nhiêu quan sát là đủ"; 114 ghi "xác suất ít nhất $0{,}95$". 13: "tổ hợp nhãn $0$, $1$ … (§5)". 5: "Ngoài vài lớp có cấu trúc riêng, như ở Bài tập 01.9 và 02.7". 327 dẫn ngược về câu hỏi mở đầu. Dạng hỏi–đáp ở dòng 13 giữ theo quyết định (bác bỏ). |
| M2 "hành xử như lớp hữu hạn" | ✓ | 106: "nhận nhiều nhất $m+1$ giá trị … chưa cho phép thay $K$ bằng $m+1$ … §7 giải thích vì sao". 134: "$L_S$ chỉ phụ thuộc $h$ qua $\lvert\mathcal H_C\rvert$ véc-tơ". 526: "như Ví dụ 03.1 và đoạn sau Định nghĩa 03.1 đã chỉ ra". |
| M3 thứ tự §7 | ✓ (xem S1, nhẹ 1) | 476 câu mở → 478 Định nghĩa 03.13 → 500 Ví dụ 03.6 → 512 hai nhu cầu → 516 (M) → 518 "tập $E_m(D,\epsilon)$ … đo được" → 520 Nhận xét 03.14 → 526 vì sao cần mẫu bóng → 533 (T5) → 537 Định lý 03.15. |
| M4 phát biểu về (M) | ✓ | 518: "các xác suất dưới đây có thể không xác định". 823: "(M) chỉ được dùng cho điều kiện đủ". 782, 866: "dưới (M)". |
| M5 phạm vi khi $d=\infty$ | một phần | 509 ("Với lớp này, …") và 665 (bỏ câu "cần cho Định lý 03.15") đúng. Dòng 874 đưa lại Ví dụ 03.6 dưới câu "Mỗi giả thiết của Định lý 03.15 đều được dùng" (S2). |
| M6 cầu nối | ✓ (nhẹ 8) | 911–919: đẳng thức hiển thị với $L_D^{\mathrm{Bayes}}$ và $\inf_{\mathcal H}L_D$; "Bài 04 đặt tên cho hai số hạng này"; không có tên sai số và không có SRM. |
| M7 Định lý 03.17 | ✓ | 784 nhãn "phác thảo (điều kiện cần: UML §5.1, §6.4)"; 788 và 846 có (T1); 792 bỏ "định tính"; 815–821 thành danh sách; 821 nhắc Bài tập 03.11; 935 ghi $\ge1/8$ và $>1/8$, suy luận đúng ($\Pr(L>1/8)\ge(1/4-1/8)/(7/8)=1/7$); 840 "Hệ quả 01.29(b)". |
| M8 hàm lỗi khác 0–1 | ✓ | 872. |
| M9 cắt lặp §8–§9 | một phần | Đoạn tóm tắt cuối §8 đã xóa; §8 kết ở 862. §9 không còn $54\,330$, $3{,}36$, $4{,}5$–$5{,}7$, $0{,}322$. Lặp mới hoặc còn lại: 823↔874 (câu về (M)), 476↔498, 257↔272, 327/332/336 (nhẹ 1, 5, 6; S2). |
| M10 Hệ quả 03.16 Bước 4 | ✓ | 722; 698 "khi có ít nhất một thuật toán ERM như vậy"; 730 dẫn Hệ quả 03.16(a) với dạng trực tiếp. Đạo hàm ở 734 đúng: $\big(d-d\ln\tfrac{2em}d-c\big)/m^2$. |
| M11 tên lớp và thuật ngữ | ✓ | 249; 314 "nửa mặt phẳng"; tiếng Anh ở lần đầu tại 3, 5, 29, 31, 58, 208, 233, 518, 592, 596; 284 định nghĩa đơn hình. |
| M12 câu dài, "đa thức" | ✓ | 5, 21, 31 đã tách; 20, 385, 395 viết "bị chặn bởi"; 183 gọi tên hai lỗi. |
| M13 ví dụ dồn bước | ✓ | 373–375; 440–444; 747–749; 763–777; 635. |
| M14 kí hiệu | ✓ | Phụ lục A dùng $\alpha$; Phụ lục C dùng $B_\epsilon$; tiếp tuyến dùng $u$, $u_0$ (602, C.7). $\kappa$ chỉ còn ở C.7. |
| M15 Phụ lục B | ✓ | "Khẳng định $P(n,d)$. Nếu … thì …"; 406 nói rõ giả thiết quy nạp. |
| R5 D1 (nghiêm trọng) | ✓ | như N1. |
| R5 T1 | ✓ | như M1. |
| R5 T2 | ✓ | như M3. |
| R5 T3 | ✓ | như M2. |
| R5 T4 | ✓ | như M10. |
| R5 T5 | ✓ | §8 kết ở 862. |
| R5 T6 | một phần | xem S2. |
| R5 T7 | ✓ | như M6. |
| R5 T8 | ✓ | 925. |
| R5, các điểm nhẹ | ✓ | Phác thảo Sauer–Shelah rút gọn (401–406). Câu "ba điểm thẳng hàng ở §5" bỏ (183). Lặp đoạn dẫn và dòng 9 bỏ. Hình vuông lên trước Bổ đề 03.8 (257). 327 dẫn ngược. Câu ôn nhanh được dẫn lại (316, 380). 751 trả lời câu hỏi thực hành. 669 câu mở §8. 821 Bài tập 03.11. 906 $h_\varnothing$. 876 trường hợp khả thực. 284 đơn hình. Điểm mục tiêu 4–5 chưa có bài đo: chuyển sang bước bài tập theo quyết định. |
| R4 nghiêm trọng ("chiều") | ✓ | như N2. |
| R4 trung bình, dòng 13 | ✓ phần dùng trước định nghĩa | Dạng hỏi–đáp giữ theo M1 (bác bỏ có lý do). |
| R4 câu hỏi trung tâm lặp | ✓ | 5 giữ; 11 chỉ còn một câu hỏi; 327 dẫn ngược. |
| R4 PAC đầy đủ | ✓ | 5. |
| R4 tiếng Anh lần đầu | ✓ | như M11. |
| R4 ba tên cho một lớp | ✓ | 249; 868 "nửa không gian afin". "Hàm phân lớp tuyến tính" ở tiêu đề, §5 và 919 khớp định nghĩa ở 249. |
| R4 câu quá 40 tiếng | ✓ | 5, 21, 31, 442, Phụ lục C.3. |
| R4 dòng 639 cũ | ✓ | 635: "cận trên của độ lệch đều, không phải giá trị của nó". |
| R4 đoạn cuối §8 | ✓ | đã xóa. |
| R4 câu chuyển ý lặp ở ranh giới | ✓ (nhẹ 2) | 236↔240 hết lặp, nhưng §4 giờ kết bằng một câu tóm tắt trơ (nhẹ 2). 339↔343, 423/472, 665↔874, 843↔862 hết lặp. |
| R4 đoạn 816 cũ thành danh sách | ✓ | 815–821. |
| R4 ví dụ dồn bước | ✓ | như M13. |
| R4 kí hiệu $A$ | ✓ | như M14. |
| R4 khẳng định quy nạp | ✓ | như M15. |
| R4 "tăng theo đa thức" | ✓ | như M12. |
| R4 Nhận xét 03.4 | ✓ | 183. |

## 2. Thứ tự mới của §7

| Ranh giới hoặc khối | Đánh giá |
|---|---|
| Cuối §6 (472) → câu mở §7 (476) | ~ yếu (nhẹ 1). Câu 476 có nêu nhu cầu ("chúng ta cần tính chất này dưới dạng một định nghĩa") nhưng không nói vì sao: Định lý 03.15(c) và Định lý 03.17 dùng định nghĩa này. Câu đầu của 476 và câu đầu của 498 nói cùng một ý cách nhau 22 dòng. |
| Định nghĩa 03.13 → 496–498 → Ví dụ 03.6 | ✓ Ví dụ 03.6 đứng trước định lý, đúng thứ tự "ví dụ cụ thể trước phát biểu tổng quát"; kết luận ở 509 chỉ nói về lớp này. |
| Ví dụ 03.6 → đoạn hai nhu cầu (512) | ✓ Câu "Với lớp có $d$ hữu hạn, Bổ đề 03.12 chặn …" nối lại §6. |
| (M) → 518 → Nhận xét 03.14 | ✓ Câu "$E_m(D,\epsilon)$ đo được" đã chuyển xuống sau (M); không còn tham chiếu tới trước. |
| Nhận xét 03.14 → 526 (vì sao cần mẫu bóng) → (T5) → định lý | ✓ Có dẫn ngược về Ví dụ 03.1 và đoạn sau Định nghĩa 03.1; câu 531 dẫn tới (T5). |
| Sau Định lý 03.15: 574 và 576 | ✗ Trùng nhau từng chữ (S1). |
| Cuối §7 (665) | ✓ Văn xuôi, nêu giới hạn khi bỏ (T1). |
| Cuối §7 → câu mở §8 (669) | ✓ "Định lý 03.15 chặn độ lệch đều …; thuật toán ERM cần một cận cho rủi ro vượt mức của nghiệm $\hat h$." |

Các ranh giới khác:

- §3 → §4 (117/121) ✓.
- §4 → §5 (236/240) ~ (nhẹ 2).
- §5 → §6 (339/343) ✓.
- §8 → §9 (862/866) ✓.
- §9 → §10 ✓.
- §11 cầu nối ✓ (nhẹ 8).

## 3. §9, cầu nối và cuối §8

- **§9.** Các đoạn 866–872 tổng hợp đúng vai trò: điều kiện học được, vai trò của chiều VC so với số tham số, tính bảo thủ, phạm vi hàm lỗi. Không còn chép lại con số. Hai từ "cần" và "đủ" dùng đúng ở 868 ("cỡ mẫu đủ") và 870 ("là cần trong trường hợp xấu nhất"). Đoạn 874 sai như nêu ở S2. Câu "(M) chỉ được dùng cho điều kiện đủ" lặp dòng 823. Dòng 876 khép mắt xích khả thực từ Bài 02.
- **Cầu nối (911–919).** Đối tượng so sánh ghi rõ: $L_D^{\mathrm{Bayes}}$ và $\inf_{h\in\mathcal H}L_D(h)$. Lý do số hạng thứ nhất không tăng đúng. Không có tên "sai số xấp xỉ/ước lượng" và không có SRM; chỉ có "Bài 04 đặt tên cho hai số hạng này". Một chỗ thiếu chính xác: cận cho rủi ro vượt mức là $2\rho_m$, nhưng câu gán thẳng $0{,}164\to0{,}280$ cho nó (nhẹ 8).
- **Cuối §8 (862).** Kết bằng giới hạn cụ thể (thừa số $\ln(1/\epsilon)$, kỹ thuật xích); không còn đoạn tóm tắt.

## 4. Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | S1 · 574 và 576 | Một đoạn bị chép đôi, trùng từng chữ, ngay sau Định lý 03.15. Lỗi sinh ra ở bước biên tập; người đọc thấy ngay. | 574 và 576 cùng là: "Khi $d=\infty$, $\Pi_{\mathcal H}(2m)=2^{2m}$, nên $\rho_m\ge\sqrt{16\ln2}\approx3{,}33$: phần (a) vẫn đúng nhưng không cho thông tin. Khi $d=0$, …" | Xóa dòng 576 cùng dòng trống trước nó. Thân bài giảm khoảng 45 từ, đủ bù các đề xuất bên dưới. Kiểm lại diff để chắc không còn khối nào bị chép đôi. |
| trung bình | S2 · 874 (và 823) | (a) Câu mở "Mỗi giả thiết của Định lý 03.15 đều được dùng" nói về chỗ dùng trong chứng minh, nhưng ba câu sau đưa phản ví dụ, tức bằng chứng về tính cần. (b) Chiều VC hữu hạn không phải giả thiết của Định lý 03.15: dòng 542 chỉ ghi "có chiều VC $d$", phần (a) đúng cả khi $d=\infty$ (dòng 574), chỉ (b) và (c) cần $d$ hữu hạn. Vì vậy Ví dụ 03.6 không minh họa việc bỏ một giả thiết của định lý, trái tinh thần M5. (c) Câu cuối nói về (M) cho Định lý 03.17, không phải 03.15, và lặp dòng 823. | 874: "Mỗi giả thiết của Định lý 03.15 đều được dùng. Ví dụ 03.8 cho thấy cận sai khi bỏ (T5), dù $d=1$; Ví dụ 02.6 cho thấy rủi ro thực nghiệm không tập trung khi bỏ (T1); Ví dụ 03.6 cho một lớp có $d=\infty$ không có tính chất hội tụ đều. Điều kiện (M) chỉ được dùng cho điều kiện đủ của Định lý 03.17." | "Hai ví dụ cho thấy giả thiết nào không bỏ được. Bỏ (T5), cận của Định lý 03.15 sai dù $d=1$ (Ví dụ 03.8). Bỏ (T1), rủi ro thực nghiệm có thể không tập trung (Ví dụ 02.6). Khi $d=\infty$, phần (a) vẫn đúng nhưng không cho thông tin, và lớp ở Ví dụ 03.6 không có tính chất hội tụ đều." Bỏ câu về (M), vì dòng 823 đã nói. Số từ gần bằng bản cũ. |
| nhẹ | 1 · 476, 498 | Câu mở §7 không nói vì sao cần một định nghĩa. Câu đầu của 476 lặp câu đầu của 498: lớp hữu hạn có tính chất hội tụ đều theo Định lý 02.14(c). | 476: "Với lớp hữu hạn chọn trước mẫu, biến cố hội tụ đều của Định nghĩa 02.13 có xác suất cao với mọi phân bố khi $m$ đủ lớn. Với lớp vô hạn, chúng ta cần tính chất này dưới dạng một định nghĩa." 498: "Một lớp hữu hạn chọn trước mẫu có tính chất hội tụ đều, với …" | Thay 476 bằng: "Ước lượng cuối §6 cần một đích chính xác: biến cố "$S$ là $\epsilon$-đại diện" (Định nghĩa 02.13) có xác suất ít nhất $1-\delta$ với mọi phân bố khi $m$ đủ lớn. Định nghĩa sau gọi đó là một tính chất của lớp." Giữ 498, vì câu này cho cận tường minh. Số từ không tăng. |
| nhẹ | 2 · 236 (cuối §4) | Sau khi bỏ câu lặp, §4 kết bằng một câu tóm tắt trơ, không nêu hệ quả hay giới hạn (`van-phong.md` §8). | "Hai lớp trên đường thẳng có chiều VC $1$ và $2$." | "Cả hai chứng minh cận trên dùng thứ tự của các điểm trên đường thẳng." Câu mở §5 (240) sửa tương ứng: "Trong $\mathbb R^p$ không có thứ tự như vậy, nên …". Thêm khoảng 5 từ. |
| nhẹ | 3 · 162 | Câu lủng củng (`van-phong.md` §9a): "có" lặp, cụm "các điểm đó" lặp ba lần. | "Khi lớp thực hiện được mọi cách gán nhãn của một tập điểm, với mọi nhãn đặt trên các điểm đó, lớp có một giả thuyết có rủi ro thực nghiệm bằng $0$ trên mẫu gồm các điểm đó." | "Nếu lớp thực hiện được mọi cách gán nhãn của một tập điểm thì, dù các nhãn quan sát trên tập đó là gì, lớp vẫn có một giả thuyết với rủi ro thực nghiệm bằng $0$." Ngắn hơn khoảng 6 từ. |
| nhẹ | 4 · 205 | Câu chuyển ý còn lại sau khi cắt mệnh đề về chữ $b$. Câu không nêu nhu cầu và đứng một mình. | "Lớp tiếp theo có hai đầu mút $u\le v$." | Xóa câu này, vì Mệnh đề 03.6 tự giới thiệu $u\le v$ (−8 từ). Nếu muốn giữ một câu dẫn: "Hàm ngưỡng có một đầu mút; lớp sau có hai." |
| nhẹ | 5 · 257, 272 | Ví dụ hình vuông (đã chuyển lên trước bổ đề) được nói lại ngay sau bổ đề. | 257: "hai đường chéo của hình vuông đơn vị cắt nhau tại tâm $(\tfrac12,\tfrac12)$ …". 272: "Với hình vuông, $I$ và $J$ là hai đường chéo và $z=(\tfrac12,\tfrac12)$." | 272 bỏ câu đầu, bắt đầu từ "Ý chứng minh: …" (−14 từ). |
| nhẹ | 6 · 327, 332, 336 | Ba lần nói "với nửa không gian afin, hai số trùng nhau" trong mười dòng. | 327: "Với nửa không gian afin, hai số trùng nhau"; 332: "(i) … có $p+1$ tham số … và $d=p+1$"; 336: "…; với nửa không gian afin, hai số trùng nhau (Mệnh đề 03.9)." | 336 chỉ giữ "Số tham số không cho cận trên, cũng không cho cận dưới, của chiều VC." (−9 từ). |
| nhẹ | 7 · 13 so với 124 | Phần mở đầu viết "tổ hợp nhãn", Định nghĩa 03.1 gọi cùng khái niệm là "cách gán nhãn"; không có câu nối hai tên. Việc tránh thuật ngữ trước định nghĩa là đúng, nhưng nên khép lại một lần. | 13: "Đại lượng cần tìm đếm số tổ hợp nhãn mà lớp tạo ra …". 124: "Mỗi $y\in\{0,1\}^k$ được gọi là một *cách gán nhãn* (labeling) của $C$." | Ở 124: "… được gọi là một *cách gán nhãn* (labeling) của $C$, tức một tổ hợp nhãn $0$, $1$ trên các điểm của $C$." (+9 từ, bù bằng nhẹ 4 hoặc 6). Có thể bỏ qua nếu không còn ngân sách. |
| nhẹ | 8 · 919 (cầu nối) | Cận cho số hạng thứ hai là $2\rho_m$, nhưng câu có thể đọc như cận cho rủi ro vượt mức tăng từ $0{,}164$ lên $0{,}280$; đó là cận độ lệch đều. | "Cận cho số hạng thứ hai, rủi ro vượt mức so với lớp, tăng theo cận độ lệch đều, từ $0{,}164$ lên $0{,}280$ ở $m=10^4$ (Ví dụ 03.7)." | "Cận cho số hạng thứ hai, rủi ro vượt mức so với lớp, bằng hai lần cận độ lệch đều, và cận độ lệch đều tăng từ $0{,}164$ lên $0{,}280$ ở $m=10^4$ (Ví dụ 03.7)." (+6 từ). |

**Ngân sách từ.** S1 cho −45 từ; nhẹ 3, 4, 5, 6 cho khoảng −37 từ; S2 và nhẹ 1 giữ nguyên số từ; nhẹ 2, 7, 8 cho khoảng +20 từ. Áp dụng tất cả, thân bài còn khoảng 11 935 từ.

**Văn phong các câu đã đổi** (Detect; `van-phong.md` §3a, §7a, §9a):

- Không thấy từ cấm, câu hỏi tu từ mới, lời khen, mẫu "không phải X mà là Y", câu kết kiểu châm ngôn hay đoạn tóm tắt.
- Câu hỏi cuối buổi (897) là câu hỏi thẳng; lời giải trả lời ngay ("Chưa.").
- Danh sách năm phép kéo theo (815–821) và giả thiết Định lý 03.17 (785–790) đúng §3a.
- Các bước tách mới của ví dụ đúng §7a.
- Ngoài dòng 162 (nhẹ 3), không thấy câu lắt léo nào khác.
