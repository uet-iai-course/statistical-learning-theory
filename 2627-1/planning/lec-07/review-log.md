# Nhật ký rà soát — Bài 07: Mạng nơ-ron, năng lực mô hình và tham số hóa thừa

Tệp nội bộ. Ghi tác tử, quyết định của điều phối viên, phát hiện rà soát và nguồn đã tham khảo.

Căn cứ bắt đầu (2026-10-31): người dùng giao lần lượt soạn ghi chú và bài tập Bài 07–10 theo blueprint, commit và push sau mỗi bài ("lần lượt xây dựng lecture note, bài tập 7, 8, 9, 10 của Lý thuyết học thống kê, tuân thủ các nguyên tắc trong CLAUDE.md và nguyên tắc riêng của môn học, theo blue-print đã thiết kế, commit & push sau khi hoàn thành mỗi bài"). Các yêu cầu rút ra từ Bài 01–06 áp dụng ngay từ bản thảo: định nghĩa trước khi dùng (`forward_refs.py` báo 0), khối nhiều thành phần viết thành danh sách có nhãn song song (`van-phong.md` §3a), câu thẳng (§9a), ví dụ từng bước (§7a), không chữ có dấu trong `\text{}`, công thức hiển thị tách dòng để vừa 390 px, cận trên làm tròn lên, số bài tập UML theo quy ước "chương.số" (như Bài 05–06).

**Nguồn bổ sung.** `CLAUDE.md` của học phần ghi nguồn bổ sung cho Bài 07–10 được chốt với người dùng khi bắt đầu bài. Người dùng giao làm liên tục bốn bài theo blueprint; blueprint §F (thứ tự ưu tiên cao hơn `CLAUDE.md`) đã liệt kê đúng nguồn bổ sung từng bài. Điều phối viên lấy danh mục §F làm quyết định và báo người dùng: Bài 07 dùng Bartlett, Foster, Telgarsky (2017) ở mức phát biểu định lý và thảo luận (tùy chọn); bản arXiv:1706.08498v2 tải về `sources/supp/` (gitignore), ghi ở `sources/README.md`.

Lời hứa cần giữ: Bài 03 dòng 868 và 921 (độ phức tạp Rademacher, UML §28.1); Bài 05 dòng 1100 (cận thống kê cho hàm lỗi lồi và Lipschitz, Bài 06–07); Bài 06 dòng 854 (lớp hồi quy bình phương với dữ liệu và $W=[-1,1]$ bị chặn có hội tụ đều, "chứng minh ở Bài 07"); cầu nối cuối Bài 06 (dòng 1130: mạng lớn khớp nhãn ngẫu nhiên; đại lượng đo độ phức tạp nào còn cho thông tin).

## Tác tử

| Bước | Vai trò | Loại | Mô hình | Mức | Bằng chứng |
|---|---|---|---|---|---|
| 2026-10-31 · 1 | Phân tích nguồn UML và nguồn bổ sung (chỉ ghi `source-analysis.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 2 | Lập dàn ý (ghi `outline.md`, chỉ planning) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 3 | Soạn ghi chú (ghi `lecture-note.md`, script thí nghiệm ngoài repo, đồng bộ `outline.md` theo quyết định dàn ý) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 4 | Năm lượt rà độc lập (học viên; chính xác toán học; chuyên gia và trung thành nguồn; học thuật–sư phạm và `no-ai-slop` Detect; mạch và móc nối), chỉ đọc repo, báo cáo ghi vào scratchpad | general-purpose ×5 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 5 | Biên tập vòng 1 (cùng người viết; ghi `lecture-note.md`, script thí nghiệm, `bien-tap-vong-1.md`, `outline.md` §13) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 6 | Rà lại: toán học trên phần đã sửa (người rà 2); mạch, móc nối và văn phong trên phần đã sửa ±2 đoạn và ranh giới mục (người rà 5), chỉ đọc | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 7 | Biên tập vòng 2: 13 điểm nhẹ của hai lượt rà lại (cùng biên tập viên) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 8 | Soạn bài tập (ghi `exercises.md`, `bai-tap-ghi-chu.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 9 | Rà bài tập: toán học (người rà 2); sư phạm và `no-ai-slop` Detect (người rà 4); chỉ đọc, báo cáo ghi vào scratchpad | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 10 | Sửa bài tập theo hai lượt rà, và một dòng §11 của ghi chú (cùng người soạn bài tập) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 11 | Rà lại bài tập: toán; sư phạm (cùng hai người rà, chỉ đọc) | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 12 | Sửa ba điểm nhẹ cuối của bài tập (cùng người soạn) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |

## Phân tích nguồn — quyết định của điều phối viên: **chấp nhận** (2026-10-31)

Báo cáo `source-analysis.md` (93 dòng, 7 mục; script ở scratchpad `src07/`). Điều phối viên tự dẫn lại: Hệ quả 7.4 cho $2\cdot\tfrac1\gamma\cdot BC_x/\sqrt m=2BC_x/(\gamma\sqrt m)$; lời hứa Bài 06: hàm lỗi $(wx-y)^2\in[0,4]$ chia $4$ thành $1$-Lipschitz theo điểm số $wx\in[-1,1]$, Định lý 7.2 hai phía (mỗi phía $\delta/2$) cho $\sup_w\lvert L_D-L_S\rvert\le8/\sqrt m+12\sqrt{\ln(4/\delta)/(2m)}$, bằng $0{,}2576$ ở $m=10^4$, $\delta=0{,}05$ (điều phối viên tính lại: $0{,}08+12\cdot0{,}01480$); hằng số $3\sqrt{\ln(2/\delta)/(2m)}$ từ hai lần McDiarmid, mỗi lần $\delta/2$ (sai phân $1/m$ cho cả $\Psi$ và $\widehat{\mathfrak R}_S$). Kiểm trên PDF: §26.1 bắt đầu tr. 375 (không phải 377); chương 26 không có bài tập; điều phối viên đã sửa `sources/uml-sections.md`.

Quyết định cho dàn ý và bản thảo:

1. **Định lý 7.2** phát biểu đúng như blueprint ($\ln(2/\delta)$, cho mọi $g\in\mathcal G$ đồng thời, hàm lỗi trong $[0,1]$), chứng minh bằng hai lần McDiarmid; [S] theo blueprint, bất đẳng thức sai phân bị chặn (McDiarmid) phát biểu trong thân bài, chứng minh ở phụ lục (martingale Doob và Bổ đề 02.6 có điều kiện; đoạn chứa bước tăng có độ dài $c_k$). Bản $\ln(1/\delta)$ không đưa vào.
2. **Bổ đề co** [S]: phát biểu dạng không trị tuyệt đối (UML §26.1), chứng minh ở phụ lục. Hằng số Lipschitz của $\phi_i$ viết $G$ (nhất quán học phần: "$G$-Lipschitz"); hàm lỗi dốc là $(1/\gamma)$-Lipschitz.
3. **Kí hiệu:** $C_x$ thay $R_x$ của blueprint ($R$ là cận khoảng cách Bài 05); $B$ cận chuẩn trọng số; $\gamma$ lề; $\sigma_i$ chỉ cho dấu Rademacher; hàm kích hoạt viết tên (ReLU) hoặc $\varsigma$ nếu cần chữ chung; mạng: $J$ số lớp, $\Theta_j$ ma trận trọng số lớp $j$, $N$ độ rộng; lề $\tilde y\,h(x)$; lớp hàm lỗi không dùng $\mathcal G_S$ (Bài 03). Mệnh đề 7.3 [F], Hệ quả 7.4 [S] với hằng số $2BC_x/(\gamma\sqrt m)$, $B$, $\gamma$ cố định trước mẫu.
4. **Thuật ngữ:** "tham số hóa thừa" (khớp tiêu đề thẻ chỉ mục); lề $\tilde y\,h_w(x)$. Điều phối viên đã sửa `thuat-ngu.md`.
5. **Câu mở đầu:** dùng thí nghiệm nhỏ tái lập được của học phần (mạng ReLU một lớp ẩn với đặc trưng ngẫu nhiên hoặc mạng nhỏ, nhãn thật so với nhãn hoán vị, nhiều lần chạy với hạt giống ghi rõ, mẫu kiểm tra độc lập; bảng số, không hình), script đặt ở `../tools/courses/statistical-learning-theory/2627-1/scripts/` và ghi giao thức; nói rõ là minh họa, không phải chứng minh (blueprint §E). Đồng nhất thức nối Rademacher với lỗi khớp nhãn ngẫu nhiên dùng để trả lời câu hỏi mở đầu (người rà toán kiểm hằng số cho hàm giá trị $\pm1$ so với $\{0,1\}$).
6. **Bài tập:** sáu bài gốc blueprint 7.5 và UML 20.3, 20.4; 20.1 tùy chọn giới hạn $n=1$; 20.5 chỉ ở tài liệu đọc thêm; bỏ 20.2, 20.6. Bài luyện Rademacher là bài gốc (chương 26 không có bài tập).
7. **Lời hứa Bài 06 dòng 854** thành một ví dụ có số trong ghi chú; lời hứa Bài 03, 05 giữ ở chỗ phù hợp.
8. **Phát biểu BFT** (bổ sung): một khối nhận xét [O] "phát biểu và thảo luận", ghi đúng các thành phần (chuẩn phổ, chuẩn $(2,1)$, lề, độ sâu, phân lớp nhiều lớp, thừa số $\log$), dẫn nguồn đầy đủ; không thay bằng cận tuyến tính.
9. **Độ dài:** thân bài ≤ 12 000 tiếng, phụ lục ≤ 3 000. Tiêu đề: "Bài 07 — Mạng nơ-ron, năng lực mô hình và tham số hóa thừa" (khớp thẻ chỉ mục, không vi phạm quy tắc tiêu đề).

## Dàn ý — quyết định của điều phối viên: **chấp nhận có sửa** (2026-10-31)

`outline.md` 524 dòng: 18 khối 07.1–07.18 (**Mệnh đề 07.2 = Example/Proposition 7.1**; **Định lý 07.11 = Theorem 7.2**; **Mệnh đề 07.13 = Proposition 7.3**; **Hệ quả 07.16 = Corollary 7.4**; **Nhận xét 07.18 = Supplement**; Bổ đề 07.10 McDiarmid, 07.14 bổ đề co, 07.8 biến đổi afin; Mệnh đề 07.9 nối Rademacher với lỗi khớp nhãn ngẫu nhiên), Ví dụ 07.1–07.11, Bài tập 07.1–07.9 (07.7 = UML 20.3, 07.8 = UML 20.4, 07.9 = UML 20.1 tùy chọn), phụ lục A–D. Điều phối viên đọc mục 1–2, 9–10, 12, kết quả các script của người lập dàn ý (`outline07/c1_numbers.txt`, `exp_m200.txt`), và tự tính lại: Ví dụ 07.9 đủ $0{,}1$ khi $m\ge(25{,}7625/0{,}1)^2\approx66\,371$; thí nghiệm nháp (10 hạt giống): lỗi kiểm tra nhãn thật $0{,}023$ ($0{,}014$–$0{,}036$), nhãn hoán vị $0{,}501$ ($0{,}480$–$0{,}512$), lỗi huấn luyện $0$, $\lVert\hat w\rVert$ trung bình $916$ so với $10\,853$. Kiểm trên PDF: §20.4 bắt đầu tr. 274; điều phối viên đã sửa `sources/uml-sections.md`.

Quyết định về các điểm mở (mục 12 của dàn ý):

1. "Mạng nơ-ron lan truyền tới" theo `thuat-ngu.md`: chấp nhận.
2. **"Xấp xỉ phổ quát"** (universal approximation) là tên chính.
3. Không đặt nhãn mới cho (T3), (T5) của lớp hàm lỗi: chấp nhận.
4. Lớp kiến trúc viết **$\mathcal H_{J,N}$, $\mathcal F_{J,N}$** (không dùng chỉ số "kt").
5. Kí hiệu cục bộ: nhãn ngẫu nhiên viết **$\tau_i$** (không $\beta_i$, vì $\beta$ là hằng số trơn); $Q$, $L^{<\gamma}_S$, $\chi$ chấp nhận.
6. Ví dụ 07.3: viết bản an toàn "chiều VC ít nhất $200=m$, vì nghiệm nội suy tồn tại với mọi cách gán nhãn" và "dạng (b) của Định lý 03.15 không áp dụng vì $d\ge m$"; không dựa vào hạng số học $400$.
7. Không phát biểu hằng số $\sqrt2$ tổng quát (Khintchine): chấp nhận.
8. Chấp nhận.
9. Thí nghiệm với lớp ẩn cố định (đặc trưng ngẫu nhiên): chấp nhận. Việc chuẩn tăng theo $m$ chỉ ở Bài tập 07.6.
10. Bài tập 07.5(c): người soạn bài tập và người rà toán kiểm.
11. Bài tập 07.9 (UML 20.1): **ReLU với $n=1$**, ghi rõ "phát biểu đã sửa so với UML".
12. Đã sửa `uml-sections.md`.
13. Câu "nghiệm nội suy chuẩn nhỏ nhất là giới hạn của hạ gradient khởi tạo tại $0$": giữ một câu kèm lý do (các điểm lặp nằm trong không gian hàng), ở Phụ lục D.
14. Bổ đề Massart: bỏ (ngân sách).
15. Ví dụ 07.6 Bước 2: dùng bản trên mẫu hữu hạn ($\widehat{\mathfrak R}=\tfrac12$ trên $200$ điểm vì lớp khớp mọi cách gán nhãn), không cần điều kiện (M) cho lớp thuần nhất.

Điều phối viên đã sửa `thuat-ngu.md` (17 dòng ở §10) và `ky-hieu.md` (8 dòng của Bài 07). Thêm cho người viết: script thí nghiệm ở `../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec07_random_labels.py` (ngoài repo), số trong ghi chú lấy từ lần chạy của script cuối; thân bài ≤ 12 000 tiếng, phụ lục ≤ 3 000; `forward_refs.py` 0; sửa `outline.md` theo các quyết định 2, 4, 5, 6, 11, 13, 14, 15 và ghi sai khác khi viết vào §13.

## Bản thảo ghi chú — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-31)

Bản thảo 1 088 dòng; thân bài 11 999 tiếng (trần 12 000), phụ lục 1 634. 18 khối 07.1–07.18, Ví dụ 07.1–07.11, một khối ứng dụng, §11 liệt kê Bài tập 07.1–07.9; 40 khối mở và đóng. Kiểm tra do điều phối viên chạy: `forward_refs.py` 0; `sync --check` OK; không có "Mục này", "rõ ràng", "dễ thấy", "Đáp án", "hãy", "vô nghĩa"; không chữ có dấu trong `\text{}`. Điều phối viên chạy lại `exp_lec07_random_labels.py` (3,7 giây): lỗi kiểm tra nhãn hoán vị /bin/bash{,}50108$ (/bin/bash{,}480$–/bin/bash{,}512$), $\lVert\hat w\rVert$ trung bình 0\,852{,}6$, tỉ số 1{,}85$; khớp ghi chú. Điều phối viên đọc phần mở đầu đến hết câu hỏi ôn nhanh: khớp dàn ý; ghi nhận cho người rà: danh sách tiên quyết chỉ ghi số hiệu, không kèm tên (Bài 06 có tên). Chấp nhận các sai khác người viết báo (`outline.md` §13, 17 mục): $\mathcal H_{J,N}(B)$ cho lớp con bị chặn theo chuẩn; kí hiệu cục bộ $\bar a$, $\kappa$, $r_j$, $\bar N$; ứng dụng dùng hàm phân lớp thuần nhất nên $d=p$; Ví dụ 07.3 theo QĐ 6 ($\rho_m\ge\sqrt{8\ln2}$); áp dụng các mục cắt (1)–(6). Bản đóng băng: scratchpad `lec07-draft-frozen.md` (SHA-256 bắt đầu `90e35e5025ff45db`).

## Năm lượt rà — quyết định của điều phối viên: **yêu cầu sửa** (2026-10-31)

Báo cáo trong `reviews/1-hoc-vien.md` (0/1/8/10), `2-toan-hoc.md` (0/0/1/8; mọi kết quả chứng minh lại đúng; Nhận xét 07.18 khớp BFT Theorem 1.1 và (1.2)), `3-chuyen-gia-nguon.md` (0/0/1/8; §E 12/12; không chép nguồn), `4-hoc-thuat-van-phong.md` (0/0/7/28), `5-mach.md` (0/0/3/14; `forward_refs.py` 0 trên bản sao; 69 lần dẫn 37 số hiệu đúng trừ một chỗ gán nội dung cho Nhận xét 02.11). Ba người rà chạy lại thí nghiệm: khớp. Nghiêm trọng N1: chuẩn $916$, $10\,853$ là chuẩn trên đặc trưng chia $\sqrt N$, trong khi mô tả mạng ở câu hỏi mở đầu ngụ ý trọng số trên đặc trưng chưa chia (điều phối viên kiểm: $916/\sqrt{2000}\approx20{,}48$). Trung bình chung của R2, R3: nhãn hoán vị vi phạm (T1) nên các cận chỉ áp cho nhãn thật. Cận trên làm tròn xuống ở bảy chỗ (điều phối viên kiểm $0{,}2+3\sqrt{\ln40/20\,000}=0{,}240738$). Quyết định gộp: `reviews/0-quyet-dinh.md` (N1, 13 mục trung bình, các điểm nhẹ).

## Biên tập vòng 1 — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-31)

Biên tập viên áp dụng N1 (một quy ước: chuẩn của $w$ trên đặc trưng chuẩn hóa $\chi$; Ví dụ 07.3 nêu $\lVert\Theta_2\rVert=\lVert w\rVert/\sqrt N$; Ví dụ 07.10 báo thêm $20{,}5$ và $242{,}7$; script in thêm chuẩn của $\Theta_2$, trung bình $20{,}475$ và $242{,}672$), 13 mục trung bình và các điểm nhẹ (`bien-tap-vong-1.md`; mục không áp dụng có lý do, chấp nhận). Thân bài 11 954 tiếng, phụ lục 1 715. Điều phối viên tự kiểm: cận logistic mới (hàm lỗi trong $[0,K]$, $K=\ln(1+e^{BC_x})$; chia $K$ thành $(1/K)$-Lipschitz theo điểm số; bổ đề co và Mệnh đề 07.13 rồi nhân $K$ cho $L_D\le L_S+2BC_x/\sqrt m+3K\sqrt{\ln(2/\delta)/(2m)}$); không-ví dụ $\mathbb 1[x\in\mathbb Q]$ ($\{f_\theta\ge0\}$ đóng vì $f_\theta$ liên tục). `forward_refs.py` 0; `sync --check` OK. Điều phối viên thêm dòng $a_j$, $G_j$, $\operatorname{err}_\tau$, $K$ vào `ky-hieu.md` và sửa dòng "lớp (con) bị chặn theo chuẩn" của `thuat-ngu.md`. Diff `lec07-r1.udiff` giao rà lại: toán (người rà 2), mạch và văn phong (người rà 5).

## Rà lại sau vòng 1 — quyết định của điều phối viên: **chấp nhận, sửa nhẹ** (2026-10-31)

Rà lại toán (`reviews/6-ra-lai-toan.md`): 8/8 phát hiện cũ ✓; mọi phần toán mới dựng lại đúng (N1, cận logistic, Nhận xét 07.18, không-ví dụ, $\Pi(2m)$, bảng Ví dụ 07.4, câu hỏi cuối buổi (b)); mọi số làm tròn lên khớp; script khớp. Mới 0/0/0/4 (quy ước làm tròn các khoảng quan sát; "tổng các nhãn cố định"; $R_\Theta$ bất biến với mọi hàm kích hoạt, ReLU cần cho $F_\Theta$ không đổi; Ví dụ 07.11 Bước 4: $B$ chọn trước mẫu, $C_x$ so với $\lVert x\rVert\le1$, tên rủi ro logistic). Rà lại mạch (`reviews/7-ra-lai-mach.md`): F1–F17 và 7 mục trung bình của người rà 4 ✓; `forward_refs.py` 0; cầu nối khớp blueprint 8; lời hứa Bài 03 dòng 921, Bài 05 dòng 1100 được giữ. Mới 0/0/0/9 (N1 câu mở §7; N2 "bán kính đại diện" chưa định nghĩa; N3 tiên quyết thừa Định nghĩa 01.14, Bổ đề 03.12 gắn nhầm tên; N4 câu dẫn trước Nhận xét 07.18; N5–N9 văn phong và §13). Gửi biên tập viên sửa 13 điểm nhẹ trong trần chữ; điều phối viên đọc diff, không rà lại thêm.

## Kiểm định cuối và công bố ghi chú — Bài 07 (2026-10-31)

Vòng 2 (`bien-tap-vong-1.md` mục "Vòng 2"): 4 điểm toán và N1–N9 (trừ hai câu N5 có lý do, chấp nhận); quy ước làm tròn khoảng quan sát gần nhất, cận trên của định lý làm tròn lên (Phụ lục D nêu quy ước). Điều phối viên đọc toàn bộ diff: đúng các quyết định. Thân bài 11 994 tiếng, phụ lục 1 743.

Kiểm định do điều phối viên chạy (`final06/final05.py`, `idx7.py`; cổng 8772), qua HTTP và `file://`, ở 1600×900 và 390×844, mở hết khối thu gọn: 1 401 công thức, 10 khối thu gọn, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức hay bảng tràn, độ rộng 375 px ở 390; bản in A4 46 trang; cảnh báo CSP duy nhất (chỉ HTTP) do `reloadserver`. Điều phối viên xem ảnh cuộn ở 390: không chồng lấn, không tràn. `forward_refs.py` 0; `sync --check` OK; `git diff --check` sạch. Thẻ Bài 07 ở `2627-1/index.html` liên kết ghi chú; mở từ chỉ mục qua HTTP và `file://` đúng tiêu đề. Script thí nghiệm `exp_lec07_random_labels.py` ở `../tools/` (ngoài repo, không commit).

**Trạng thái:** ghi chú Bài 07 hoàn tất; commit và push. Việc tiếp theo: bài tập theo `outline.md` §4.

## Bài tập — bắt đầu (2026-10-31)

Giao một người viết soạn `exercises.md` theo `outline.md` §4 và §11 của ghi chú (9 bài: 07.1–07.6 gốc theo blueprint 7.5; 07.7 = UML 20.3, 07.8 = UML 20.4, 07.9 = UML 20.1 tùy chọn, phát biểu đã sửa: ReLU, $n=1$). Bài UML tự giải trước rồi mới đối chiếu bản lời giải (chương 20). Công thức hiển thị vừa 390 px; ≤ 10 000 tiếng.

## Bài tập — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-31)

`exercises.md`: 9 bài (07.1–07.6 gốc; 07.7–07.9 là UML 20.3, 20.4, 20.1 tùy chọn bản sửa), 9 771 tiếng, 36 khối (9 đề, 18 gợi ý, 9 lời giải). Người soạn tự giải ba bài UML trước khi mở bản lời giải (20:41); ghi chỗ hổng của bản lời giải ở `bai-tap-ghi-chu.md` (20.3, 20.4 viết "=" thay "≤"; 20.4 bỏ qua điểm lặp; 20.1 không kiểm soát sai số gần biên). Sai khác với dàn ý §4 (chấp nhận để rà): không chép lại chứng minh của ghi chú (07.1(a) mạng thứ hai; 07.3(a) lớp afin, 07.3(c) điều kiện dấu bằng, 07.3(e)); 07.2, 07.4(d) thêm ý; 07.4(b) làm tròn lên /bin/bash{,}1095$; 07.9 bỏ ý sigmoid. Kiểm tra do điều phối viên chạy: `sync --check` OK; 72 dòng `:::`; không có "Đáp án", "rõ ràng", "dễ thấy", "hãy". Điểm để rà: 07.6(b) sai số chuẩn coi mười lần chạy độc lập; 07.9(c) dẫn Nhận xét 07.3; kí hiệu cục bộ mới ($\theta_{\mathrm{abs}}$, …, $\vartheta_i$, $\bar n$); thuật ngữ mới ("hàm kích hoạt ngưỡng", "lớp tích", "lớp hợp"). Bản đóng băng: scratchpad `lec07-ex-frozen.md` (SHA-256 bắt đầu `25540909ffa6bbc8`).

## Rà bài tập — quyết định của điều phối viên: **yêu cầu sửa** (2026-10-31)

Rà toán (`reviews/9-bai-tap-toan.md`): 0/0/0/4; tự giải lại cả 9 bài, mọi lời giải đúng; thí nghiệm với $m=100$–$800$ khớp trừ hai chữ số cuối; đề UML trung thành, không chép bản lời giải. Rà sư phạm (`reviews/10-bai-tap-su-pham.md`): 0/0/4/21; phủ đủ mục tiêu và loại bài. Quyết định gộp: `reviews/11-quyet-dinh-bai-tap.md` (8 mục, kí hiệu, điểm nhẹ). Điều phối viên thêm ba thuật ngữ vào `thuat-ngu.md`.

## Sửa bài tập — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-31)

Người soạn áp dụng 8 mục, 4 điểm toán và các điểm nhẹ (`bai-tap-ghi-chu.md` §8; ba chỗ làm khác có lý do, chấp nhận: $\tilde f$ ở 07.9(d); giữ tiêu đề 07.5; $\theta_{\mathrm{II}}$). Ghi chú: chỉ dòng Bài tập 07.8 ở §11 ("lớp hàm hợp"). 9 911 tiếng, 36 khối. Diff `lec07-ex-r1.udiff` giao rà lại: toán (người rà 2), sư phạm (người rà 4).

## Rà lại bài tập — quyết định của điều phối viên: **chấp nhận, sửa nhỏ** (2026-10-31)

Rà lại toán (`reviews/12-ra-lai-bai-tap-toan.md`): 4/4 ✓; mọi phần đổi dựng lại đúng; số mới khớp; không phát hiện mới. Rà lại sư phạm (`reviews/13-ra-lai-bai-tap-su-pham.md`): 24/25 ✓, 1 không áp dụng có lý do (tiêu đề 07.5); gợi ý 1 của chín bài không lộ lời giải; mới 0/0/0/3 (07.8(b) "Bước 2 của (a)", câu 55 tiếng; 07.6(b) Bước 3 tách ba phép tính và cho số liệu để tính lại $0{,}0019$; dòng 630 thiếu chủ ngữ). Gửi người soạn sửa ba điểm nhẹ; không rà lại sau khi điều phối viên đọc diff.

## Kiểm định cuối và công bố bài tập — Bài 07 (2026-10-31)

Người soạn sửa ba điểm nhẹ (`bai-tap-ghi-chu.md` §8.1); điều phối viên đọc diff (đúng ba điểm; $0{,}0061/\sqrt{10}\approx0{,}0019$). Bài tập 9 962 tiếng, 36 khối. Kiểm định do điều phối viên chạy (`final06/final05.py`, `idx7e.py`; cổng 8772), qua HTTP và `file://`, ở 1600×900 và 390×844, mở hết khối thu gọn: bài tập 1 242 công thức, 27 khối thu gọn; ghi chú (sau khi đổi một dòng §11) 1 401 công thức; cả hai 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 tràn, độ rộng 375 px ở 390; bản in A4: bài tập 34 trang, ghi chú 46 trang; cảnh báo CSP duy nhất (chỉ HTTP) do `reloadserver`. `forward_refs.py` 0; `sync --check` OK; `git diff --check` sạch. Thẻ Bài 07 ở `2627-1/index.html` liên kết ghi chú và bài tập; mở từ chỉ mục qua HTTP và `file://` đúng tiêu đề.

**Trạng thái:** Bài 07 (ghi chú và bài tập) hoàn tất; commit và push. "Done means" thỏa: không có phát hiện chặn bàn giao; phát hiện nghiêm trọng N1 của ghi chú đã xử lý và ghi lại; `outline.md` §13 và nhật ký khớp sản phẩm; trình xem hiển thị ở hai cỡ, bản in và `file://`; `material-local-data.js` đồng bộ; thẻ chỉ mục liên kết sau khi qua rà soát.
