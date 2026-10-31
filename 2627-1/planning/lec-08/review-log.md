# Nhật ký rà soát — Bài 08: Tính ổn định của SGD và tổng quát hóa trong học sâu

Tệp nội bộ. Ghi tác tử, quyết định của điều phối viên, phát hiện rà soát và nguồn đã tham khảo.

Căn cứ bắt đầu (2026-10-31): người dùng giao lần lượt soạn ghi chú và bài tập Bài 07–10 theo blueprint, commit và push sau mỗi bài (xem `../lec-07/review-log.md`). Các yêu cầu rút ra từ Bài 01–07 áp dụng ngay từ bản thảo (định nghĩa trước khi dùng, danh sách song song, câu thẳng, ví dụ từng bước, công thức vừa 390 px, cận trên làm tròn lên và khoảng quan sát làm tròn gần nhất, danh sách tiên quyết có tên khối, thí nghiệm có giao thức tái lập, mẫu kiểm tra độc lập, nhiều lần chạy).

**Nguồn bổ sung.** Theo blueprint §F (cùng lý do như Bài 07): Hardt, Recht, Singer (2016), lập luận trơn–lồi và phần thảo luận chọn lọc (bắt buộc); phân tích không lồi (đọc thêm). Bản arXiv:1509.01240v2 tải về `sources/supp/` (gitignore), ghi ở `sources/README.md`. Bước phân tích nguồn chạy song song với bước soạn bài tập Bài 07: tác tử phân tích nguồn chỉ đọc repo, ghi báo cáo vào scratchpad, điều phối viên chép vào `source-analysis.md` (một người ghi repo tại một thời điểm).

Lời hứa cần giữ: Bài 06 dòng 620 (dạng $\mathbb E_\xi\lvert\cdot\rvert$ với hai lần chạy dùng chung $\xi$, Bài 08 dùng cho SGD), dòng 1071 (khoảng cách tổng quát hóa kì vọng của SGD nhiều vòng, với hàm lỗi lồi, trơn, Lipschitz), dòng 1130 và 1295; cầu nối cuối Bài 07 (dòng ~960: quỹ đạo tối ưu quyết định nghiệm; câu hỏi cho Bài 08).

## Tác tử

| Bước | Vai trò | Loại | Mô hình | Mức | Bằng chứng |
|---|---|---|---|---|---|
| 2026-10-31 · 1 | Phân tích nguồn UML và Hardt–Recht–Singer (chỉ đọc repo; báo cáo ghi scratchpad, điều phối viên chép vào `source-analysis.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 2 | Lập dàn ý (chỉ đọc repo; ghi dàn ý vào scratchpad, điều phối viên chép vào `outline.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 3 | Soạn ghi chú (ghi `lecture-note.md`, script thí nghiệm ngoài repo, `outline.md` §13) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 4 | Năm lượt rà độc lập (học viên; chính xác toán học; chuyên gia và trung thành nguồn; học thuật–sư phạm và `no-ai-slop` Detect; mạch và móc nối), chỉ đọc repo, báo cáo ghi vào scratchpad | general-purpose ×5 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 5 | Biên tập vòng 1 (cùng người viết; ghi `lecture-note.md`, script thí nghiệm, `bien-tap-vong-1.md`, `outline.md` §13) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 6 | Rà lại: toán học trên phần đã sửa (người rà 2); mạch, móc nối và văn phong trên phần đã sửa ±2 đoạn và ranh giới mục (người rà 5), chỉ đọc | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 7 | Biên tập vòng 2: 2 điểm trung bình và 12 điểm nhẹ của hai lượt rà lại (cùng biên tập viên) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |

## Phân tích nguồn — quyết định của điều phối viên: **chấp nhận** (2026-10-31)

Báo cáo (95 dòng, 7 mục; script ở scratchpad `src08/`), điều phối viên chép vào `source-analysis.md`. Điều phối viên tự kiểm: cận ghép cho hồi quy logistic $R^2/(2\eta T)+\eta G^2/2+\eta G^2(T-1)/m$ với $R=5$, $G=1$, $\eta=0{,}05$, $m=10^4$ đạt cực tiểu tại $T^*=R\sqrt{m/2}/\eta\approx7071$, giá trị $2\sqrt{(R^2/2\eta)(\eta/m)}+\eta/2\approx0{,}0957$; ổn định của điểm lặp trung bình $\tfrac1T\sum_t2G\eta(t-1)/m\cdot G=G^2\eta(T-1)/m$. Khớp.

Quyết định cho dàn ý và bản thảo (§6.4 của báo cáo):

1. **(a) Chỉ số** từ $t=1$ như Thuật toán 05.11; điểm lặp cuối $w_{T+1}$; tổng $\sum_{t=1}^T\eta_t$ (ghi khác biệt chỉ số với HRS ở §13 của ghi chú, trung tính).
2. **(b) Định lý cho SGD có chiếu** lên $W$ đóng, lồi (gồm $W=\mathbb R^p$), thêm một dòng nhờ phép chiếu không giãn; giả thiết hàm lỗi lồi, $\beta$-trơn trên $\mathbb R^p$ (cho tính đồng bức), gradient bị chặn bởi $G$ trên $W$.
3. **(c), (d)** Định lý cho $w_{T+1}$ (blueprint); hệ quả cho $\bar w_T$ ($G^2\eta(T-1)/m$ với bước hằng); hệ quả ghép [F] cho rủi ro vượt mức kì vọng qua Mệnh đề 06.5, Định lý 06.10 và Hệ quả 05.19, nêu rõ cận này không tốt hơn cận một vòng (Hệ quả 06.2) và chỉ cho thấy đánh đổi giữa hai cận trên, không chứng minh dừng sớm luôn tốt hơn.
4. **(e) Bổ đề 8.1** [S] theo blueprint; tính đồng bức chứng minh ở phụ lục.
5. **(f) Không lồi** [S]: hồi quy với thừa số $1+\beta\eta_t$ và tích; HRS Thm 3.12 chỉ phát biểu [O] với đủ giả thiết (hàm lỗi bị chặn, $\eta_t\le c/t$).
6. **Phụ lục tối ưu [O]** (điểm dừng) theo blueprint, chứng minh tự dẫn.
7. **(g) Thí nghiệm** hồi quy logistic $p=100$, $m=200$, 20 hạt giống, mẫu kiểm tra độc lập (dạng của báo cáo §3(e)); script ở `../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec08_coupled_sgd.py`; nói rõ là bằng chứng.
8. **(h) Ví dụ tính tay** dùng hàm lỗi Huber (định nghĩa tại chỗ), $m=4$, $\eta=\tfrac12$.
9. **(i) Bài tập:** sáu bài gốc blueprint 8.5; không có bài UML phù hợp (ghi lý do ở §11 và §13 của ghi chú: chương 13–14 đã dùng ở Bài 05–06, §20.6 không có bài tập về ổn định); có thể thêm tối đa hai bài gốc gắn với khối của ghi chú (ví dụ ổn định của điểm lặp trung bình; hằng số của hàm lỗi logistic).
10. **Kí hiệu:** $\Delta_t=\lVert w_t-w'_t\rVert$ (nói một câu: khác $\Delta_t$ cục bộ trong chứng minh Bài 05); $w'_t$; $\xi=(i_1,\ldots,i_T)$ dùng chung; $G$ (không $L$ của HRS); không đặt tên hàm phụ là $\varphi$. Thân bài ≤ 12 000 tiếng, phụ lục ≤ 3 000. Tiêu đề: "Bài 08 — Tính ổn định của SGD và tổng quát hóa trong học sâu" (khớp thẻ chỉ mục).

## Dàn ý — quyết định của điều phối viên: **chấp nhận có sửa** (2026-10-31)

Dàn ý (535 dòng) do tác tử lập dàn ý ghi vào scratchpad `outline08/outline.md` khi bước soạn bài tập Bài 07 đang ghi repo; điều phối viên chép vào `outline.md`. 12 khối: Thuật toán 08.1 (SGD có chiếu, bước thay đổi, đầu ra $w_{T+1}$); Định nghĩa 08.2, 08.3; **Bổ đề 08.4 = Lemma 8.1** [S] (có thêm phần có chiếu); **Mệnh đề 08.5 = Prop 8.2** [F] ((a) trên từng quỹ đạo, (b) chỉ dùng $\Pr(i_t=i)=1/m$); **Định lý 08.6 = Thm 8.3** [F] (gồm dạng ghép cặp $\mathbb E_\xi\lvert\cdot\rvert$); Hệ quả 08.7 (điểm lặp trung bình) [F]; **Hệ quả 08.8 = Corollary** [F] (cận ghép); Định nghĩa 08.9; **Mệnh đề 08.10 = Nonconvex extension** [S]; Nhận xét 08.11 [O] (HRS Thm 3.12); **Mệnh đề 08.12 = Optional appendix** [O]. Ví dụ 08.1–08.10, Bài tập 08.1–08.8 (sáu bài gốc, 08.7 giữ lời hứa Bài 06 với hồi quy bình phương có chiếu, 08.8 chọn $T^*$), phụ lục A–D. Điều phối viên đọc mục 1–2, 9–10, 12 và kết quả script (`outline08/c1_numbers.txt`, `exp_p100_eta05.txt`) và tự kiểm: ví dụ Huber ($\mathbb E\Delta_2=\tfrac14$ đạt cận; $\mathbb E\Delta_7=228\,203/262\,144\approx0{,}8705\le1{,}5$); cận logistic $2G^2\eta t/m=0{,}005t$ với $G=1$, $\eta=0{,}5$, $m=200$, $\eta\le2/\beta=8$; thí nghiệm có nhiễu nhãn độc lập nên (T1) thỏa; khoảng cách tổng quát hóa $0{,}0445$ → $0{,}9188$ so với cận $0{,}5$ → $100$; cận ghép tại $T^*\approx7071$ là $0{,}0958$ (làm tròn lên).

Quyết định về các điểm mở (mục 12.2): (1) "bất đẳng thức truy hồi"; (2) nhãn **(S)** (lồi và $\beta$-trơn trên $\mathbb R^p$) và **(G)** (cận tất định cho gradient trên $W$, nói một câu: mạnh hơn (G2) của Bài 05); (3) viết thẳng vế phải, không đặt $\epsilon_T$; (4) "cận trên bậc hai (còn gọi là bổ đề hạ)"; (5) Phụ lục B là chi tiết bất đẳng thức truy hồi: đúng; (6) Ví dụ 08.4 với $T=6$; (7) Ví dụ 08.9 dùng hàm Huber; (8) biến thể mạng đặc trưng ngẫu nhiên chỉ bằng lời. Điều phối viên đã thêm 11 dòng thuật ngữ vào `thuat-ngu.md` §10 và 3 dòng kí hiệu vào `ky-hieu.md`. Thêm cho người viết: script thí nghiệm `../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec08_coupled_sgd.py`; mọi số từ lần chạy cuối; thân ≤ 12 000, phụ lục ≤ 3 000; `forward_refs.py` 0; ghi sai khác vào §13.

## Bản thảo ghi chú — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-31)

Bản thảo 1 084 dòng; thân bài 11 946 tiếng, phụ lục 1 488. 12 khối 08.1–08.12, Ví dụ 08.1–08.10, một khối ứng dụng, §11 liệt kê Bài tập 08.1–08.8 (kèm câu vì sao không có bài UML); 33 khối mở và đóng. Kiểm tra do điều phối viên chạy: `forward_refs.py` 0; `sync --check` OK; không có "Mục này", "rõ ràng", "dễ thấy", "Đáp án", "hãy", "vô nghĩa". Điều phối viên chạy lại `exp_lec08_coupled_sgd.py`: ở 100 vòng lỗi logistic huấn luyện $0{,}1345$, kiểm tra $1{,}0533$, khoảng cách $0{,}9188$, $\Delta$ ghép cặp $5{,}4583$, tỉ số cận/khoảng cách $108{,}84$; khớp ghi chú. Điều phối viên đọc phần mở đầu đến tiên quyết: khớp dàn ý. Chấp nhận các sai khác người viết báo (`outline.md` §13.2, 16 mục): bỏ cột "Cận" khỏi bảng (bằng số vòng; tràn ở 390 px), hàm Huber viết thành danh sách, cắt theo thứ tự cắt, Phụ lục B còn (i)–(ii). Bản đóng băng: scratchpad `lec08-draft-frozen.md` (SHA-256 bắt đầu `161fab6ba2139bb4`).

## Năm lượt rà — quyết định của điều phối viên: **yêu cầu sửa** (2026-10-31)

Báo cáo trong `reviews/1-hoc-vien.md` (0/1/9/17), `2-toan-hoc.md` (0/0/1/10; mọi kết quả chứng minh lại đúng, mọi số khớp, thí nghiệm tái lập với $\eta=0{,}5$ và $0{,}25$), `3-chuyen-gia-nguon.md` (0/0/6/12; §E 12/12; Nhận xét 08.11 khớp HRS Thm 3.12; năm lời hứa được giữ), `4-hoc-thuat-van-phong.md` (0/0/7/26), `5-mach.md` (0/0/3/15; `forward_refs.py` 0; mọi số hiệu 01.x–07.x đúng). Nghiêm trọng N1 (bốn người rà cùng nêu): câu chữ về chỗ dùng tính lồi mâu thuẫn với chứng minh; chứng minh vẫn đúng. Điều phối viên quyết cách sửa: Lipschitz trên $W$ lấy từ (G) và tính lồi của $W$ (định lý giá trị trung bình), tính lồi của hàm lỗi chỉ ở bước chung. Quyết định gộp: `reviews/0-quyet-dinh.md` (N1, 11 mục trung bình, các điểm nhẹ). Điều phối viên thêm hai thuật ngữ vào `thuat-ngu.md`.

## Biên tập vòng 1 — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-31)

Biên tập viên áp dụng N1 (bước khác biệt của Mệnh đề 08.5 viết lại: $\Delta_{t+1}\le\lVert(w_t-w'_t)-\eta_t(g-g')\rVert\le\Delta_t+2G\eta_t$, chỉ dùng (G) và phép chiếu không giãn; Lipschitz trên $W$ ở Định lý 08.6 Bước 1 bằng định lý giá trị trung bình; mọi câu về chỗ dùng tính lồi sửa cho khớp; Mệnh đề 08.5 phát biểu cho mọi quy tắc rút có $\Pr(i_t=i)=1/m$), 11 mục trung bình và các điểm nhẹ (`bien-tap-vong-1.md`; bốn mục không áp dụng có lý do, chấp nhận). Để giữ trần chữ: chứng minh Hệ quả 08.8 chuyển sang Phụ lục E, phác thảo Mệnh đề 08.10 sang Phụ lục F (thân bài giữ lộ trình), bỏ câu ôn nhanh 2, lần chạy không ghép cặp chuyển sang Phụ lục D. Thân bài 11 982 tiếng, phụ lục 2 106. `forward_refs.py` 0.

**Thay đổi ngoài phiên.** Biên tập viên báo `2627-1/materials/lec-01/lecture-note.md` có thay đổi chưa commit (sửa lúc 22:14, không do tác tử nào của phiên này), và lệnh sync đã gói thay đổi đó vào `material-local-data.js`. Quyết định của điều phối viên: không stage, không sửa tệp Bài 01; khi commit, `material-local-data.js` được dựng với Bài 01 lấy theo `HEAD` (script scratchpad `bundle_head.py`), rồi đồng bộ lại bản đầy đủ cho cây làm việc sau commit; báo người dùng.

Diff `lec08-r1.udiff` giao rà lại: toán (người rà 2), mạch và văn phong (người rà 5).

## Rà lại sau vòng 1 — quyết định của điều phối viên: **chấp nhận, sửa nhẹ** (2026-10-31)

Rà lại toán (`reviews/6-ra-lai-toan.md`): 11/11 phát hiện cũ ✓ (kể cả N1); mọi phần toán đã đổi dựng lại đúng (Mệnh đề 08.5 cho mọi quy tắc rút có $\Pr(i_t=i)=1/m$, kể cả xáo trộn lại; Định lý 08.6 Bước 1, 4; Phụ lục E, F; Mệnh đề 08.10(a); Mệnh đề 08.12); số mới khớp. Mới 0/0/0/2 (dòng 497 "(G) dùng hai lần" bỏ sót Bước 4; dòng 1110 câu kết Phụ lục F). Rà lại mạch (`reviews/7-ra-lai-mach.md`): 16 ✓, 1 một phần (cầu nối thiếu câu "Câu hỏi cho Bài 09 là"); T1–T5 của người rà 4 ✓, T6 một phần; `forward_refs.py` 0. Mới 0/0/2/10: M1 dòng 193 (khoảng cách $\tfrac38$ của hai dãy chỉ số độc lập còn chứa hiệu $\tfrac14$ do thay quan sát — sửa theo đề xuất); M2 dòng 746 ("Thừa số này" mất chỗ dựa); các điểm nhẹ (câu mở §6, dòng 218, 690, 796 mô tả ví dụ ReLU, 445, 682, $g'$ hai nghĩa, "khoảng cách" hai nghĩa ở dòng 1050, $\Gamma$ ở Phụ lục F, dòng 187). Thứ tự chữ phụ lục: đánh lại theo thứ tự đọc nếu không tốn chữ. Gửi biên tập viên sửa sau khi người viết Bài 09 (đang ghi repo) xong; điều phối viên đọc diff, không rà lại thêm.

## Kiểm định cuối và công bố ghi chú — Bài 08 (2026-10-31)

Vòng 2 (`bien-tap-vong-1.md` mục "Vòng 2"): hai điểm nhẹ của rà lại toán; M1, M2 và các điểm nhẹ của rà lại mạch; cầu nối có câu "Câu hỏi cho Bài 09 là …"; phụ lục đánh lại chữ theo thứ tự đọc (A đồng bức, B truy hồi, C Hệ quả 08.8, D Mệnh đề 08.10, E điểm dừng, F giao thức), mọi dẫn chiếu đổi theo. Điều phối viên đọc diff (180 dòng đổi, phần lớn là chữ phụ lục). Thân bài 11 995 tiếng, phụ lục 2 131.

Kiểm định do điều phối viên chạy (`final06/final05.py`, `idx8.py`; cổng 8772), qua HTTP và `file://`, ở 1600×900 và 390×844: 1 439 công thức, 10 khối thu gọn, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 tràn, độ rộng 375 px ở 390; bản in A4 47 trang; cảnh báo CSP duy nhất (chỉ HTTP) do `reloadserver`. `forward_refs.py` 0; `git diff --check` sạch trên tệp của bài. Thẻ Bài 08 liên kết ghi chú; mở từ chỉ mục qua HTTP và `file://` đúng tiêu đề.

**Gói `material-local-data.js` khi commit:** dựng bằng scratchpad `bundle_head.py` — ghi chú Bài 08 lấy từ cây làm việc, mọi tệp khác lấy theo `HEAD` (Bài 01 không gồm thay đổi chưa commit của người dùng; bản thảo Bài 09 chưa duyệt không có trong gói). Sau commit, chạy lại lệnh sync để cây làm việc có gói đầy đủ.

**Trạng thái:** ghi chú Bài 08 hoàn tất; commit và push. Việc tiếp theo: bài tập Bài 08.
