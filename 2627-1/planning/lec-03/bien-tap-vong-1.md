# Biên tập vòng 1 — Bài 03 (2026-10-31)

Tệp nội bộ. Người biên tập áp dụng `reviews/0-quyet-dinh.md` lên `materials/lec-03/lecture-note.md` (bản đóng băng `lec03-draft-frozen.md`). Mỗi dòng: mục quyết định — trạng thái — ghi chú.

**Đánh số lại (do M3):** Định nghĩa 03.14 → **Định nghĩa 03.13** (Tính chất hội tụ đều của một lớp); Nhận xét 03.13 → **Nhận xét 03.14** (Điều kiện (M) cho các lớp của bài). Các khối và ví dụ khác giữ số; số bài tập ở §10 giữ nguyên. Mọi chỗ dẫn (Ví dụ 03.6, đoạn sau (M), Ví dụ 03.7, Phụ lục D) đã sửa theo.

**Số tiếng:** thân bài 11 999 (`wc -w`, trước `## Phụ lục`), phụ lục 2 107.

## A. Nghiêm trọng

- **N1** — áp dụng. Bảng §1 bỏ $d$, $\Pi_{\mathcal H}$, "cách gán nhãn", hàng "Chỉ trong chứng minh" và câu báo §4, §6; hàng ngẫu nhiên ghi "véc-tơ giá trị $(h(X_1),\ldots,h(X_m))$ của mỗi $h$". Mục 8 của §1 viết "một đại lượng của lớp (định nghĩa ở §4)". Mẫu bóng và dấu ngẫu nhiên được giới thiệu tại Bước 1–2 của lộ trình Định lý 03.15, kèm câu "chỉ dùng trong chứng minh".
- **N2** — áp dụng. "Chiều" chỉ còn nghĩa số chiều: mục tiêu 1 ("bằng cận dưới và cận trên … chỉ có một trong hai phần"); tiêu đề Nhận xét 03.4 "Cận dưới và cận trên cho chiều VC"; Nhận xét 03.10 ("không cho cận trên, cũng không cho cận dưới"); "điều kiện đủ/điều kiện cần" trước Định lý 03.17; "(a) Điều kiện cần, không dùng (M)"; "Phép kéo theo (4)⇒(6)"; §9; §10 tiêu đề Bài tập 03.2 "… bằng cận dưới và cận trên"; "Quan hệ với UML". Ghi cho bước bài tập: đổi tiêu đề Bài tập 03.2 trong `exercises.md` theo.
- **N3** — áp dụng. Sau Định lý 03.19: "UML §6.4 phát biểu hai cận dưới này với hằng số tuyệt đối; UML §28.2 chứng minh phần (a); UML không chứng minh phần (b)." §12 "Mở rộng" sửa đúng §28.1/§28.2/§28.3. (`outline.md` §7 do điều phối viên sửa.)

## B. Trung bình

- **M1** — áp dụng. Câu hỏi mở đầu và câu hỏi thực hành: "Bao nhiêu quan sát là đủ …", câu hỏi thực hành ghi $\delta$ (độ tin cậy $0{,}95$). Dòng 13 giữ dạng hỏi–đáp, thay "cách gán nhãn" bằng "tổ hợp nhãn $0$, $1$", thêm chỉ dẫn §5. Đoạn dẫn thêm mệnh đề "Ngoài vài lớp có cấu trúc riêng, như ở Bài tập 01.9 và 02.7, …". Bỏ câu hỏi thứ hai lặp ở câu hỏi mở đầu (R4); câu trước Nhận xét 03.10 dẫn ngược về câu hỏi mở đầu.
- **M2** — áp dụng. Ví dụ 03.1 kết luận: $L_S(h_t)$ nhận nhiều nhất $m+1$ giá trị, "chưa cho phép thay $K$ bằng $m+1$ … §7 giải thích vì sao". Sau Định nghĩa 03.1: "$L_S$ chỉ phụ thuộc $h$ qua $\lvert\mathcal H_C\rvert$ véc-tơ". Đoạn vì sao cần mẫu bóng dẫn ngược về Ví dụ 03.1 và đoạn sau Định nghĩa 03.1.
- **M3** — áp dụng. §7 theo thứ tự: câu mở mới → Định nghĩa 03.13 → Ví dụ 03.6 → đoạn "hai điều cần thêm" → (M), câu "tập $E_m(D,\epsilon)$ đo được với mọi $D$" chuyển xuống sau (M) → Nhận xét 03.14 → đoạn vì sao cần mẫu bóng → (T5) → Định lý 03.15. Đánh số lại như trên.
- **M4** — áp dụng. Câu "các kết luận có thể sai với lớp bệnh lý" thay bằng "các xác suất dưới đây có thể không xác định". "(M) chỉ được dùng cho điều kiện đủ" ở sau Định lý 03.17 và §9. Câu tóm tắt trước Định lý 03.17 và đầu §9 có "dưới (M)".
- **M5** — áp dụng. Bỏ câu "cả chiều VC hữu hạn lẫn (T5) đều cần cho Định lý 03.15" ở cuối §7. Ví dụ 03.6 kết luận chỉ về lớp này ("Với lớp này, hội tụ đều hỏng …").
- **M6** — áp dụng. Cầu nối viết theo đẳng thức sau Định nghĩa 01.24 (hiển thị), đối tượng so sánh ghi rõ; số hạng thứ nhất không tăng, cận cho rủi ro vượt mức so với lớp tăng $0{,}164\to0{,}280$; "Bài 04 đặt tên cho hai số hạng này". Không có tên "sai số xấp xỉ/ước lượng", không SRM.
- **M7** — áp dụng. Tiêu đề Định lý 03.17 "— phác thảo (điều kiện cần: UML §5.1, §6.4)"; thêm **Mẫu.** (T1) vào giả thiết Định lý 03.17 và vào Định lý 03.19; bỏ "định tính"; đoạn các phép kéo theo thành danh sách năm dòng, dòng (4)⇒(6) nhắc Bài tập 03.11; thêm "UML §6.4 phát biểu định lý này". "Quan hệ với UML" thêm ý $\ge1/8$ / $>1/8$. Hệ quả 01.29(b) ở câu sau chứng minh Hệ quả 03.18.
- **M8** — áp dụng. §9: phép đếm cách gán nhãn ở Bước 3 cần hàm lỗi xác định bởi nhãn dự đoán trong $\{0,1\}$; hàm lỗi bình phương, hàm lỗi log còn có thể không bị chặn.
- **M9** — áp dụng. Xóa đoạn cuối §8. §9 viết lại, không chép lại $54\,330$, $3{,}36$, $4{,}5$–$5{,}7$, $0{,}322$; câu "mỗi giả thiết đều được dùng" chỉ còn ở §9 (thân bài). Các cặp câu lặp R4: cuối §4/đầu §5 (bỏ câu thứ hai cuối §4); cuối §5/đầu §6 (cuối §5 viết lại, không lặp); cuối §6 (bỏ câu lặp $\ln\Pi\le d\ln(em/d)$); cuối §7/§9; câu dẫn trước Định lý 03.19 viết lại, câu sau khối không nhắc lại Nhận xét 02.18; câu đo được của thuật toán ERM chỉ còn sau Hệ quả 03.16 (bỏ ở Nhận xét 03.14 và Phụ lục D).
- **M10** — áp dụng. Bước 4 chứng minh Hệ quả 03.16 thay bằng dẫn Định lý 03.15(c) tại $\epsilon/2$ ($16/(\epsilon/2)^2=64/\epsilon^2$, $32/(\epsilon/2)^2=128/\epsilon^2$) rồi Bước 1–2 với $r=\epsilon/2$. Phần (c) thêm "khi có ít nhất một thuật toán ERM như vậy". Ví dụ 03.9 Bước 1 dẫn Hệ quả 03.16(a) với dạng trực tiếp thay cho Bước 4 cũ.
- **M11** — áp dụng. Định nghĩa 03.7: "nửa không gian afin (affine halfspace), còn gọi là lớp hàm phân lớp tuyến tính afin; mỗi $h_{w,b}$ là một hàm phân lớp tuyến tính". "Nửa không gian phẳng" → "nửa mặt phẳng" (Ví dụ 03.3, 03.5, 03.9). Tiếng Anh lần đầu: hàm ngưỡng (threshold), độ phức tạp mẫu (sample complexity), bất đẳng thức hợp (union bound) ở kiến thức tiên quyết, σ-đại số (σ-algebra), định lý cơ bản (fundamental theorem), PAC viết đầy đủ, phân lớp nhị phân (binary classification), khoảng đóng (closed interval), lực lượng (cardinality), định lý hội tụ bị chặn (bounded convergence theorem), đổi chỗ (swapping); "dấu ngẫu nhiên (random signs)" ở lần dùng đầu (Bước 2 lộ trình). Đơn hình định nghĩa tại chỗ dùng (lộ trình Mệnh đề 03.9).
- **M12** — áp dụng. Tách câu dài: đoạn dẫn, mục tiêu 3 (hai câu), kiến thức tiên quyết Bài 02, Ví dụ 03.5 Bước 3–5, Phụ lục C.3. "Bị chặn bởi một đa thức" ở mục tiêu 2 và Bổ đề 03.12; "không vượt quá cỡ $d\ln m$" ở câu $\square$ và kết luận Ví dụ 03.5. Nhận xét 03.4 gọi tên hai lỗi.
- **M13** — áp dụng. Ví dụ 03.4 Bước 4 tách thành Bước 4–5; Ví dụ 03.5 Bước 3 tách thành Bước 3–5; Ví dụ 03.9 Bước 4 tách thành Bước 4–5; Ví dụ 03.10 Bước 3 có câu thiết lập (lớp sáu hàm vừa hữu hạn vừa có $\Pi\le6$) và Bước 4 với $480$, $\ln480\approx6{,}174$, $240$, $\ln240\approx5{,}481$. Ví dụ 03.7 kết luận: "cận trên của độ lệch đều, không phải giá trị của nó".
- **M14** — áp dụng. Phụ lục A: tổng đổi thành $\alpha$. Phụ lục C: biến cố đổi thành $B_\epsilon$; tiếp tuyến dùng $u$, $u_0$ (cả lộ trình Định lý 03.15 Bước 5). $\kappa$ chỉ còn ở Bước C.7 (chứng minh Hệ quả 03.16 không còn dùng $\kappa$).
- **M15** — áp dụng. Khẳng định $P(n,d)$ viết "Nếu … thì …"; Bước 4 Phụ lục B nói rõ giả thiết quy nạp áp dụng cho hai họ véc-tơ nhãn $Y'$, $Y_1$; phác thảo trong thân bài nói giả thiết quy nạp phát biểu cho mọi tập cách gán nhãn của $m-1$ vị trí.

## C. Cắt

- Áp dụng: đoạn cuối §8; phần lặp ở §9; Bước 4 chứng minh Hệ quả 03.16; phác thảo Sauer–Shelah rút còn hai bước (đẳng thức đếm hiển thị, bước quy nạp và Pascal); mệnh đề về chữ $b$ (dòng 206); câu $\mathbb 1[0\le x\le2]$ (dòng 256); câu cuối dòng 363; lặp giữa đoạn dẫn và câu hỏi mở đầu.
- Cắt thêm để giữ $\le12\,000$ (không mất nội dung toán): danh sách mười bốn cách gán nhãn ở Ví dụ 03.3 Bước 3 viết thành một câu; Nhận xét 03.10(iii) dẫn Mệnh đề 03.9(b) thay cho phép đếm; câu "ba điểm thẳng hàng cho thấy …" ở kết luận Ví dụ 03.3 (Bước 2 đã nói); gộp Bước 5 và kết luận Ví dụ 03.10; ý "Tính đo được" ở "Quan hệ với UML" (R5); rút gọn đoạn giả thiết §2, mục tiêu 1, đoạn giới hạn §9.

## D. Nhẹ

- Áp dụng mọi điểm nhẹ của năm báo cáo, trừ các mục dưới đây.
- **Không áp dụng (bác bỏ theo M1):** bỏ dạng hỏi–đáp ở câu hỏi mở đầu (R1, R3, R4, R5).
- **Hoãn:** hình SVG cho Ví dụ 03.3 (R4).
- **Chuyển sang bước bài tập:** bất đẳng thức "số cách gán nhãn không quá số tập con bị tách trọn" (R3, Bài tập 03.8); các ý của mục tiêu 4, 5 chưa có bài đo và tên Bài tập 03.4 (R5); trùng câu hỏi cuối buổi với Bài tập 03.9.
- **Không áp dụng:** đổi nhãn độ sâu Hệ quả 03.18 thành "chứng minh từ Định lý 03.17(a), được thừa nhận" (R1) — giữ nhãn "chứng minh đầy đủ (dựa trên Định lý 03.17(a))" theo quyết định 10 của điều phối viên ở mục dàn ý (`review-log.md`).
- **Áp dụng một phần:** R1 đề nghị liệt kê Định lý 03.17(a), Hệ quả 03.18, Định lý 03.19(b) trong dòng $\epsilon$ của bảng §2 — viết "các phát biểu khả thực ở §8" vì bảng §2 không được dẫn khối có số đứng sau (quy tắc định nghĩa trước khi dùng). R5 đề nghị thêm câu "ba điểm không thẳng hàng bị tách trọn, bốn điểm thì không (Ví dụ 03.3)" trước Bổ đề 03.8 — không thêm vì dẫn khối đứng sau; chỉ chuyển ví dụ hình vuông lên trước bổ đề. R1 đề nghị giữ nguyên câu "ba điểm thẳng hàng ở §5" trong Nhận xét 03.4 — bỏ theo R5 (dẫn tới mục sau; Ví dụ 03.3 Bước 2 đã dẫn ngược).
- Lời giải câu hỏi cuối buổi: gán nhãn $0$ cho mọi điểm còn lại; câu cuối viết theo tọa độ $a_1,a_2,b_1,b_2$; nói rõ vì sao $h_\varnothing$ bị loại; câu hỏi viết thành câu hỏi thẳng (R4). Áp dụng.
- Kiến thức tiên quyết: bỏ Nhận xét 02.8; §1 ghi "hàm phân lớp đo được". Áp dụng.

## Con số mới

- Ví dụ 03.10 Bước 4: $\ln480\approx6{,}174$, $\ln240\approx5{,}481$ (Python: $6{,}17379$, $5{,}48064$); $\sqrt{8\cdot6{,}174/1000}\approx0{,}2222$, $\sqrt{5{,}481/2000}\approx0{,}0523$ (khớp giá trị cũ).
- Hệ quả 03.16 Bước 4: dạng đóng của Định lý 03.15(c) tại $\epsilon/2$ trùng $M(\epsilon,\delta)$; kiểm số tại $\epsilon=0{,}1$, $\delta=0{,}05$: $88\,572$, $209\,624$, $693\,832$ cho cả hai cách viết.

## Kiểm tra đã chạy

`forward_refs.py`: 0. `sync-local-materials.py --check`: OK. Grep `\text{}` có dấu: 0. `git diff --check`: sạch. Playwright (máy chủ cổng 8766 của repo) ở 1600×900 và 390×844, mở hết 13 khối thu gọn: 0 `.katex-error`, 0 lỗi console, 0 yêu cầu hỏng, không công thức hay bảng nào tràn.

## Vòng 2 (2026-10-31)

Căn cứ: `reviews/6-ra-lai-toan.md` (1 trung bình, 3 nhẹ) và `reviews/7-ra-lai-mach.md` (1 nghiêm trọng, 1 trung bình, 8 nhẹ); điều phối viên chấp nhận tất cả. Không đánh số lại khối nào. Thân bài 11 981 tiếng, phụ lục 2 107.

- **S1 / toán-trung bình (đoạn lặp sau Định lý 03.15)** — áp dụng. Xóa bản thứ hai của đoạn "Khi $d=\infty$ … Khi $d=0$ …" cùng dòng trống đi kèm; lỗi sinh ra khi ghép lại §7 ở vòng 1. Đã quét toàn tệp: không còn dòng dài nào bị lặp.
- **S2 (§9, "Mỗi giả thiết … đều được dùng")** — áp dụng theo câu của người rà: (T5) và (T1) không bỏ được (Ví dụ 03.8, Ví dụ 02.6); khi $d=\infty$ phần (a) vẫn đúng nhưng không cho thông tin, lớp ở Ví dụ 03.6 không có tính chất hội tụ đều. Bỏ câu về (M) (đã có sau Định lý 03.17).
- **Nhẹ 1 (câu mở §7)** — áp dụng, viết lại không dùng dấu hai chấm kiểu "lộ ý": "Để biến ước lượng cuối §6 thành một bảo đảm, chúng ta cần biến cố … Định nghĩa sau gọi đó là một tính chất của lớp." Không nêu Định lý 03.15(c), 03.17 để tránh dẫn khối đứng sau.
- **Nhẹ 2 (cuối §4)** — áp dụng: "Cả hai chứng minh cận trên dùng thứ tự của các điểm trên đường thẳng."; câu mở §5: "Trong $\mathbb R^p$ không có thứ tự như vậy, …".
- **Nhẹ 3 (câu trước Định nghĩa 03.2)** — áp dụng theo câu đề xuất.
- **Nhẹ 4 (câu "Lớp tiếp theo có hai đầu mút")** — áp dụng: xóa.
- **Nhẹ 5 (hình vuông nói lại sau Bổ đề 03.8)** — áp dụng: đoạn sau bổ đề bắt đầu từ "Ý chứng minh".
- **Nhẹ 6 ("hai số trùng nhau" ba lần)** — áp dụng: câu cuối Nhận xét 03.10 chỉ giữ "Số tham số không cho cận trên, cũng không cho cận dưới, của chiều VC."
- **Nhẹ 7 ("tổ hợp nhãn" và "cách gán nhãn")** — áp dụng ở Định nghĩa 03.1: "…, tức một tổ hợp nhãn $0$, $1$ trên các điểm của $C$." Không dẫn khối nào từ phần mở đầu.
- **Nhẹ 8 / toán-nhẹ 1 (cầu nối)** — áp dụng: cận cho rủi ro vượt mức so với lớp bằng hai lần cận độ lệch đều (Hệ quả 03.16(a)); ở $m=10^4$ cận độ lệch đều tăng $0{,}164\to0{,}280$ (Ví dụ 03.7), nên cận cho rủi ro vượt mức tăng $0{,}329\to0{,}560$.
- **Toán-nhẹ 2 (Ví dụ 03.9, dấu đạo hàm)** — áp dụng: ", vì $\ln\tfrac{2em}d\ge\ln(2e)>1$ khi $m\ge d$ và $c>0$".
- **Toán-nhẹ 3 (§9, cận dưới khả thực)** — áp dụng: "Định lý 03.19(b) chỉ cho cận dưới cỡ $(d+\ln(1/\delta))/\epsilon$".

**Con số mới:** $0{,}329=2\cdot0{,}16443$ và $0{,}560=2\cdot0{,}27986$ (hai ô dạng trực tiếp của Ví dụ 03.7 tại $m=10^4$, $d=3$ và $d=11$; Python: $0{,}32886$, $0{,}55973$).

**Kiểm tra đã chạy:** `forward_refs.py`: 0. `sync-local-materials.py --check`: OK. Grep `\text{}` có dấu: 0. `git diff --check`: sạch. Playwright (cổng 8766 của repo) ở 1600×900 và 390×844, mở hết 13 khối thu gọn: 0 `.katex-error`, 0 lỗi console, 0 yêu cầu hỏng, không công thức hay bảng nào tràn.
