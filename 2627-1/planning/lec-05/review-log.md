# Nhật ký rà soát — Bài 05: Hạ gradient, hạ gradient ngẫu nhiên và cận tối ưu

Tệp nội bộ. Ghi tác tử, quyết định của điều phối viên, phát hiện rà soát và nguồn đã tham khảo.

Căn cứ bắt đầu (2026-10-31): người dùng giao soạn ghi chú và bài tập Bài 05 theo blueprint ("xây dựng lecture note, bài tập 05 của Lý thuyết học thống kê, tuân thủ các nguyên tắc trong CLAUDE.md và nguyên tắc riêng của môn học, theo blue-print đã thiết kế"). Các yêu cầu rút ra từ Bài 01–04 áp dụng ngay từ bản thảo: định nghĩa trước khi dùng (`forward_refs.py` báo 0), khối nhiều thành phần viết thành danh sách có nhãn song song (`van-phong.md` §3a), câu thẳng (§9a), ví dụ từng bước (§7a), công thức không chứa chữ tiếng Việt có dấu trong `\text{}`. Từ bài này thuật toán có nguồn ngẫu nhiên riêng $\xi$ (`ky-hieu.md`; lời hứa ở Bài 01 dòng 629).

## Tác tử

| Bước | Vai trò | Loại | Mô hình | Mức | Bằng chứng |
|---|---|---|---|---|---|
| 2026-10-31 · 1 | Phân tích nguồn UML (chỉ ghi `source-analysis.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 2 | Lập dàn ý (ghi `outline.md`, chỉ planning) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 3 | Soạn ghi chú (ghi `lecture-note.md`, đồng bộ `outline.md` theo quyết định dàn ý) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 4 | Năm lượt rà độc lập (học viên; chính xác toán học; chuyên gia và trung thành nguồn; học thuật–sư phạm và `no-ai-slop` Detect; mạch và móc nối), chỉ đọc repo, báo cáo ghi vào scratchpad | general-purpose ×5 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 5 | Biên tập vòng 1 (cùng người viết; ghi `lecture-note.md`, `bien-tap-vong-1.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 6 | Rà lại: toán học trên phần đã sửa (người rà 2); mạch, móc nối và văn phong trên phần đã sửa ±2 đoạn và ranh giới mục (người rà 5), chỉ đọc | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 7 | Biên tập vòng 2 (cùng biên tập viên) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 8 | Rà lại kết hợp vòng 2: toán, mạch, văn phong, thống nhất cách viết số trên diff vòng 2 (người rà 5, chỉ đọc) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 9 | Sửa sáu điểm nhẹ cuối, cách viết số và 43 công thức tràn ở 390 px (cùng biên tập viên) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 10 | Soạn bài tập (ghi `exercises.md`, `bai-tap-ghi-chu.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 11 | Rà bài tập: toán học (người rà 2); sư phạm và `no-ai-slop` Detect (người rà 4); chỉ đọc, báo cáo ghi vào scratchpad | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 12 | Sửa bài tập theo hai lượt rà (cùng người soạn; ghi `exercises.md`, `bai-tap-ghi-chu.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 13 | Rà lại bài tập: toán; sư phạm (cùng hai người rà, chỉ đọc) | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 14 | Sửa các điểm cuối của bài tập (cùng người soạn) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |

## Phân tích nguồn — quyết định của điều phối viên: **chấp nhận** (2026-10-31)

Báo cáo `source-analysis.md` (96 dòng, 7 mục). Điều phối viên tự tính lại bằng Python (scratchpad `m/m_check05.py`): Ví dụ hồi quy (a) $L_S(w_1)=0{,}6667$, bước 1 $w_2=(1,0)$, $L_S=0{,}4533$, bước 2 $v=(1,-1)$ chiếu thành $(0{,}7071,-0{,}7071)$, $L_S=0{,}0639$; cực tiểu trên quả cầu $0{,}06112$ tại $(0{,}7473,-0{,}6645)$, nghiệm bình phương tối thiểu không ràng buộc $(1{,}06,-0{,}92)$, chuẩn $1{,}404$, $L_S=0{,}00667$; bảng lô nhỏ ($G^2=1+15/b$, $\epsilon=0{,}1$): $T=1600,475,194,124,106$, số quan sát $1600,1900,3104,7936,27136$, GD $100$ bước, $10^6$; mức sàn $\eta\sigma^2/(2(2-\eta a))$: $0{,}02632$, $0{,}01282$, $0{,}002513$; $\mathbb E\bar w_T^2=0{,}000496$; SGD trên $5w^2$ với $\eta=0{,}15$: $\mathbb E\ln\lvert\cdot\rvert=0{,}087$, $\mathbb E[\cdot^2]=1{,}69$; Markov $T=640\,000$; bước thay đổi $0{,}2964$ (đều), $0{,}228$ (có trọng số); lấy không hoàn lại $9{,}5$, $4{,}75$, $3{,}1667$; oracle chệch $0{,}16$. Mọi số khớp.

Quyết định cho dàn ý và bản thảo:

1. **Oracle cụ thể.** $g_t=\varphi(w_t,\xi_t)$ với $\xi_1,\xi_2,\ldots$ độc lập cùng phân bố, độc lập với $w_1$ (và với $S$); lịch sử $\mathcal F_{t-1}=\sigma(\xi_1,\ldots,\xi_{t-1})$. Hai giả thiết tất định trên $W$: (O1) $\mathbb E_\xi\varphi(w,\xi)\in\partial F(w)$, (O2) $\mathbb E_\xi\lVert\varphi(w,\xi)\rVert^2\le G^2$ với mọi $w\in W$; dạng có điều kiện của blueprint suy ra từ đó (một bổ đề "đóng băng" phát biểu không chứng minh, hoặc lập luận trực tiếp cho $\xi$ rời rạc). Thuật toán là $A(S;\xi)$ (lời hứa Bài 01 dòng 629). Không nêu lỗ hổng của UML tr. 193 trong ghi chú (chỉ ghi ở đây).
2. **Giả thiết của $F$.** $F$ lồi, hữu hạn trên $\mathbb R^p$ (hoặc trên một tập mở chứa $W$); $W\subset\mathbb R^p$ khác rỗng, đóng, lồi; $w_1\in W$. Định lý chính so với **mọi** $u\in W$: $\mathbb E F(\bar w_T)-F(u)\le\lVert w_1-u\rVert^2/(2\eta T)+\eta G^2/2$. Hệ quả: $R$ chặn $\lVert w_1-w^*\rVert$ với $w^*$ là một nghiệm tối ưu khi tồn tại, hoặc lấy cận dưới đúng trên $\{u\in W:\lVert u-w_1\rVert\le R\}$; không cần giả sử tồn tại nghiệm tối ưu cho định lý. Sai khác này ghi trong `outline.md`.
3. **Độ dài bước hằng $\eta$** trong định lý chính; $\eta$ phụ thuộc $T$ nên $T$ cố định trước. Bước thay đổi $\eta_t$: một nhận xét [O] (dạng trung bình có trọng số, có thừa số $\ln T$) và một bài tập (UML 14.8.4 thêm phép chiếu lên quả cầu, cận $3BG/\sqrt T$ theo kí hiệu học phần). Sửa `ky-hieu.md`: $\eta$ không chỉ số là độ dài bước hằng; $\eta(x)$ luôn có đối số.
4. **Kí hiệu phép chiếu: $\operatorname{proj}_W$**, không dùng $\Pi_W$ của blueprint (trùng hàm tăng trưởng $\Pi_{\mathcal H}(m)$ của Bài 03; một kí hiệu một nghĩa). Ghi sai khác trong `outline.md`. Không giãn của phép chiếu: một câu hoặc nhận xét, không cần cho định lý.
5. **Tham số hóa.** $w\in W\subset\mathbb R^p$; viết $\ell(w,z)$ cho $\ell(h_w,z)$, $L_S(w)$, $L_D(w)$ (như UML Ch. 12); hàm phân lớp tuyến tính thuần nhất $h_w$ (không hệ số chặn $b$, vì $b$ là kích thước lô theo `thuat-ngu.md`). Hàm lỗi bản lề với $\tilde y=2y-1$ (nhãn $\{0,1\}$ của học phần).
6. **Kí hiệu khác.** $B$ bán kính của $W$; $C_x$, $C_y$ cận của $\lVert x\rVert$, $\lvert y\rvert$; $\nu_t$ nhiễu gradient trong phản ví dụ; $\psi(w)=\mathbb E_\xi\varphi(w,\xi)$; $\sigma^2$ phương sai của gradient ngẫu nhiên chỉ trong mục lô nhỏ (nói rõ khác $\sigma_i$ Bài 03, $\sigma^2(x)$ Bài 04), hoặc chọn kí hiệu khác nếu người lập dàn ý thấy lẫn; $\lambda$ hệ số lồi mạnh (khớp với chính quy hóa $\frac\lambda2\lVert w\rVert^2$ của Bài 06); $\beta$ hằng số trơn (khác $\beta(m,\delta)$ Bài 01, nói một câu). $g_t$ là gradient ngẫu nhiên (khác ứng viên $g_j$ — không dùng ứng viên trong bài này).
7. **Phạm vi Bài 05.** Bảo đảm là bảo đảm tối ưu cho mục tiêu mà oracle không chệch. Lấy chỉ số đều từ $S$ có hoàn lại: Định lý áp dụng cho $F=L_S$ khi $S$ cố định, cho $\mathbb E_\xi\operatorname{opt}_S(\bar w_T)$ (nối Bài 04). Rủi ro tổng thể với mẫu mới mỗi bước, và mọi phát biểu về $L_D$ khi dùng lại $S$, để Bài 06 (cầu nối). Hàm lỗi bản lề không cho phát biểu 0–1 trong bài này.
8. **Chuyển kì vọng sang xác suất cao** bằng bất đẳng thức Markov theo $\xi$: một hệ quả hoặc nhận xét có số ($640\,000$ so với $1600$). Tăng độ tin cậy bằng nhiều lần chạy: chỉ ở bài tập nếu dùng.
9. **Lô nhỏ (Mệnh đề [O] của blueprint).** Cùng kì vọng có điều kiện, độc lập có điều kiện; phương sai chia $b$; nối với định lý: $G_b^2=G_F^2+\sigma^2/b$, chỉ phần phương sai giảm. Phản ví dụ tương quan (lặp lại cùng quan sát). Xáo trộn theo vòng (epoch) nằm ngoài định lý: một câu. Bảng so sánh số bước và số quan sát đã xử lý (ví dụ số).
10. **GD** là trường hợp riêng tất định (Thuật toán và một hệ quả), chi phí $m$ gradient mỗi bước khi $F=L_S$. Không dẫn tốc độ nhanh hơn của GD dưới giả thiết trơn (không có trong nguồn được giao). Trơn và lồi mạnh: định nghĩa là phần mở rộng, không phải giả thiết của định lý chính.
11. **Phản ví dụ bỏ giả thiết trong ghi chú:** (i) không lồi ($(w^2-1)^2$ hoặc hàm min hai parabol); (ii) gradient không bị chặn / bước quá lớn, SGD trên $5w^2$; (iii) điểm lặp cuối và điểm lặp trung bình với $\lvert w\rvert$ (diễn đạt trung thực theo §3(iii) của báo cáo); (iv) oracle chệch. (v) mức sàn sai số để bài tập (blueprint bài 6), ghi chú có thể nêu một câu.
12. **Bài tập.** Sáu bài gốc blueprint 5.5 và UML 12.6.1, 12.6.2, 12.6.3, 14.8.3 (ý 1–3), 14.8.4 (thêm phép chiếu); 9.6.2 tùy chọn. Tổng không quá 13. Đổi tên $R=\max\lVert x_i\rVert$ của UML. Tránh trùng bài gốc 1 với 12.6.3.
13. **Độ dài:** thân bài ≤ 12 000 tiếng (`wc -w`), phụ lục ≤ 3 000.

## Dàn ý — quyết định của điều phối viên: **chấp nhận có sửa** (2026-10-31)

`outline.md` 493 dòng: 20 khối đánh số (05.1–05.20; Bổ đề 05.8 = Lemma 5.1; Mệnh đề 05.13 = Prop 5.2; Định lý 05.14 = Theorem 5.3; Hệ quả 05.15 = Corollary 5.4; Mệnh đề 05.20 = Prop 5.5; GD: Thuật toán 05.9, Hệ quả 05.16; Markov: Hệ quả 05.19(b); bước thay đổi: Nhận xét 05.17; $A(S;\xi)$: Định nghĩa 05.18), Ví dụ 05.1–05.16, một khối ứng dụng, Bài tập 05.1–05.12 (05.1–05.6 gốc; 05.7–05.12 là UML 12.1, 12.2, 12.3, 14.3 ý 1–3, 14.4 thêm phép chiếu, 9.2 tùy chọn). Điều phối viên đọc mục 1–3 đầy đủ, mục 4–12; tự tính lại bằng Python (scratchpad `m/m_check05b.py`, `m_check05c.py`): bước thứ ba của Ví dụ 05.6 ($0{,}0710$; $0{,}1021$; $0{,}0694$; trung bình $0{,}0808$; GD $0{,}0614$), $\bar w_3=(0{,}5690;-0{,}2357)$, $L_S(\bar w_3)=0{,}2644$; Ví dụ 05.7 ($1{,}3289$; $0{,}5053$; $1{,}5019$; $0{,}4200$; $0{,}1730$); Ví dụ 05.4 ($0{,}7654$; $-0{,}1213$); trị riêng $\tfrac23$, $\tfrac43$; Ví dụ 05.10 ($\eta=0{,}02778$, $\bar w=-1{,}0056$, $f=0{,}5000>0{,}1406$; $G=2{,}25$); Ví dụ 05.11 ($164w^2$); Bài tập 05.2 ($-0{,}2$, $-1{,}48$; $1{,}6$, $1{,}7799$), 05.3 ($0{,}8460$; $0{,}5556$; $0$), 05.5(b) ($150$, $440$), 05.11 ($0{,}2982$); Phụ lục D ($M$, $c$, $\kappa=0{,}1350$); câu hỏi cuối buổi ($0{,}05$; $0{,}95$; $0{,}0025$; $1{,}9025$). Sai một chỗ làm tròn: $\lVert w_3-w^*\rVert=0{,}058614$ phải in $0{,}0586$, không phải $0{,}0587$.

Quyết định về các điểm mở (mục 12 của dàn ý):

1. **Nhãn giả thiết:** (C), (G1), (G2) — chấp nhận; QĐ 1 viết (O1), (O2) là nhầm, vì (O1), (O2) là hai mức tối ưu của Bài 01.
2. **$\varphi$:** giữ cho ánh xạ oracle; đã sửa dòng `ky-hieu.md` ($\varphi$ ở Bài 02, 04 là hàm phụ cục bộ).
3. **$B$:** giữ bán kính của $W$; đã ghi chú ở `ky-hieu.md`.
4. **Chỗ dùng tính lồi:** xác nhận cách đánh dấu của dàn ý: tính lồi của $F$ đi vào Bước 3 (bất đẳng thức dưới gradient) và Bước 5 (bất đẳng thức lồi hữu hạn); tính lồi của $W$ đi vào phép chiếu và $\bar w_T\in W$. Mục tiêu học tập 1 giữ nguyên chữ "bước nào dùng tính lồi".
5. **UML §14.4.1** vào phần đọc sau buổi: chấp nhận.
6. **"Tổng triệt tiêu"** (telescoping sum): chấp nhận; đã thêm vào `thuat-ngu.md` §9.
7. **$7{,}85$ và $1{,}81$** (tính trên lưới, không chứng minh): **bỏ** khỏi thân bài và phụ lục.
8. **Câu hỏi cuối buổi với $m=1$:** chấp nhận; bỏ dòng tùy chọn $0{,}3162$/$1{,}4675$.
9–15. Chấp nhận như dàn ý.
16. Điều phối viên đã sửa ba dòng `thuat-ngu.md` §9 (gradient ngẫu nhiên, phép chiếu, độ chênh tối ưu) và thêm 18 dòng thuật ngữ mới.
17. **Khoảng cách trong chứng minh:** dùng $\Delta_t=\lVert w_t-u\rVert^2$ (bình phương), không dùng $d_t$ (trùng chiều VC) hay $r_t$ (trùng bán kính $r_m$ của Bài 02).

Điều phối viên đã sửa `ky-hieu.md`: dòng $\eta(x)$ ($\eta$ không đối số là độ dài bước hằng), dòng $R$, dòng $v^\star$/$\varphi$; thêm 16 dòng của Bài 05 ($w$, $W$, $\ell(w,z)$, $h_w$, $\tilde y$, $B$, $C_x$, $C_y$, $F$, $\partial F$, $w^*$, $u$, $\operatorname{proj}_W$, $\Xi$, $P_\xi$, $\xi_t$, $i_t$, $\varphi$, $\psi$, $\mathcal F_t$, $g_t$, $v(w)$, $v_t$, $w_t$, $\bar w_T$, $\tilde w_T$, $w_{T+1}$, (C), (G1), (G2), $\Delta_t$, $b$, $\varphi_b$, $G_F$, $\sigma^2$, $G_b$, $\nu_t$, $\delta'$, $\operatorname{diam}(W)$).

Sai khác với blueprint (chấp nhận): đối tượng so sánh là mọi $u\in W$ (QĐ 2); giả thiết có điều kiện suy ra từ oracle $\varphi(w,\xi)$ (Bổ đề 05.12); $\operatorname{proj}_W$ thay $\Pi_W$; thêm Mệnh đề 05.3, 05.5, Bổ đề 05.12, Hệ quả 05.16, 05.19, Nhận xét 05.17, Định nghĩa 05.18; ví dụ hồi quy ba bước; §14.4.1 thành bài đọc sau buổi.

Thêm cho người viết: thân bài ≤ 12 000 tiếng (`wc -w`), phụ lục ≤ 3 000; `forward_refs.py` phải báo 0; sửa `outline.md` cho khớp các quyết định 7, 8, 17 và số $0{,}0586$; ghi sai khác khi viết vào §13 của `outline.md`.

## Bản thảo ghi chú — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-31)

Bản thảo 1278 dòng; thân bài 11 979 tiếng (`wc -w`, trần 12 000), phụ lục 1159 (trần 3 000). 20 khối 05.1–05.20, Ví dụ 05.1–05.16, một khối ứng dụng, §12 liệt kê Bài tập 05.1–05.12; 52 khối mở và đóng, không lồng. Kiểm tra do điều phối viên chạy: `forward_refs.py` 0; `sync --check` OK; mục lục đúng dàn ý. Điều phối viên đọc phần mở đầu đến hết §3: khớp dàn ý và các quyết định (nhãn (C), (G1), (G2); không có $7{,}85$, $1{,}81$).

Chấp nhận các sai khác người viết báo (`outline.md` §13): Ví dụ 05.10 Bước 5 sửa đúng (đạo hàm của nhánh trái là dưới gradient ở các bước đầu, hỏng từ $t=26$, ngưỡng $-1{,}1213$; người rà toán kiểm lại); áp dụng các mục (1), (2), (5), (6), (7), (9) của thứ tự cắt và bỏ điểm thử $\alpha=-0{,}1$ ở Ví dụ 05.2; Mệnh đề 05.3 chỉ đòi tính lồi cho (a); Mệnh đề 05.5 chỉ cần $A$ mở; Bổ đề 05.12(c) thêm $\mathbb E\lvert F(w_t)\rvert<\infty$ (Phụ lục B); kí hiệu cục bộ $F_R$ ở Hệ quả 05.15(b); bảng $w_4$ và $\nabla L_S(w_3)$ ở Ví dụ 05.6; Phụ lục D kiểm $w^*$ bằng điều kiện bậc nhất. Bản đóng băng cho rà soát: scratchpad `lec05-draft-frozen.md` (SHA-256 bắt đầu `ef6289d5c94e93f2`).

## Năm lượt rà — quyết định của điều phối viên: **yêu cầu sửa** (2026-10-31)

Báo cáo trong `reviews/1-hoc-vien.md` (0/1/5/22), `2-toan-hoc.md` (0/0/1/10; tự chứng minh lại mọi kết quả, 206 con số, sai chỉ ba cận trên làm tròn xuống), `3-chuyen-gia-nguon.md` (0/0/6/10; §E 10/12), `4-hoc-thuat-van-phong.md` (0/0/14/21), `5-mach.md` (0/0/5/12; `forward_refs.py` 0 trên bản sao, các lời hứa của Bài 01 và Bài 04 được giữ, lời hứa Bài 01 dòng 846 giữ một phần). Không có lỗi chặn bàn giao, không có lỗi trong chứng minh. Một phát hiện nghiêm trọng (N1: $\ell(h_{w,0},z)$ không xác định với hàm lỗi bản lề, logistic; dùng hàm điểm số $h_w(x)=\langle w,x\rangle$). Quyết định gộp: `reviews/0-quyet-dinh.md` (N1, M1–M15, cắt, nhẹ). Sửa quyết định 4 của dàn ý: Bước 3 của Định lý 05.14 dùng (G1); tính lồi dùng ở Bước 5 và là điều kiện để (G1) thỏa được (M8, theo R1).

Điều phối viên đã kiểm lại trên PDF và tự sửa ngoài bản thảo: `sources/uml-sections.md` (§12.1 tr. 156, §14.2 tr. 188; R3 đúng); UML §14.4.1 tr. 193 viết phép chiếu bằng $\arg\min$ (R3 đúng, M11); `thuat-ngu.md` dòng "internal randomness" thống nhất "nguồn ngẫu nhiên riêng"; `ky-hieu.md` dòng $h_w$ (N1) và kí hiệu cục bộ $U$, $k_{1:t-1}$, $\Phi$, $\bar\Phi$.

## Biên tập vòng 1 — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-31)

Biên tập viên áp dụng N1, M1–M15, mười hai chỗ cắt của mục C và mọi điểm nhẹ của mục D (danh sách ở `bien-tap-vong-1.md`). Không áp dụng (chấp nhận lý do): tách Mục tiêu 1 (M8 giữ nguyên); thuật ngữ "cắt gradient" bỏ hẳn thay vì định nghĩa; bất đẳng thức lồi hữu hạn giữ dạng văn xuôi, không thêm khối (giữ số hiệu); bổ đề đóng băng ghi "phát biểu không chứng minh", không thêm nguồn. Số hiệu khối và ví dụ không đổi; §8 đổi tên "Vai trò của từng giả thiết". Thân bài 11 988 tiếng, phụ lục 1182. Kiểm tra do điều phối viên chạy: `forward_refs.py` 0; `sync --check` OK; diff so với bản đóng băng `lec05-round1.diff` (466 dòng đổi). Điều phối viên đọc Bước 3–5 và đoạn sau chứng minh Định lý 05.14: đúng M8; khẳng định thêm "(G1) tại mọi điểm của $W$ buộc $F$ lồi trên $W$" tự kiểm lại đúng (cộng hai bất đẳng thức dưới gradient tại điểm tổ hợp lồi). Điều phối viên thêm vào `ky-hieu.md` các kí hiệu cục bộ $\theta$, $\gamma$, $q_i$, $a'$.

## Rà lại sau vòng 1 — quyết định của điều phối viên: **yêu cầu sửa nhỏ** (2026-10-31)

Rà lại toán (`reviews/6-ra-lai-toan.md`): 0/0/1/6; 11/11 phát hiện cũ ✓; các phát biểu mới (N1, M7, M8 gồm khẳng định "(G1) trên $W$ buộc $F$ lồi trên $W$", M10, Mệnh đề 05.5, Ví dụ 05.10, 05.11) dựng lại đúng; mọi số mới đúng. Trung bình: câu cuối §6 (dòng 642) nói bình phương khoảng cách tới mọi $u\in W$ giảm theo trung bình, không điều kiện — sai. Rà lại mạch (`reviews/7-ra-lai-mach.md`): 0/0/2/11; 14/17 phát hiện cũ ✓, T3 một phần, N11–N12 giữ theo quyết định; 12/12 chỗ cắt; `forward_refs.py` 0. Trung bình: dòng 642 (như trên); dòng 362 còn câu "tính lồi biến dưới gradient thành cận dưới toàn cục", trái M8.

Quyết định gửi biên tập vòng 2: sửa mọi phát hiện của hai báo cáo; dòng 642 viết đúng lượng giảm $2\eta(F(w_t)-F(u))$ trừ $\eta^2G^2$; dòng 362 theo M8; số hạng $\tfrac\eta2\lVert g\rVert^2$ một tên duy nhất (không "bậc hai theo độ dài bước", tỉ lệ bậc nhất với $\eta$); "mức sàn sai số" chỉ một nghĩa; cận in sau so sánh làm tròn lên ($0{,}1407$ hoặc in đủ $0{,}140625$).

## Biên tập vòng 2 — quyết định của điều phối viên: **chấp nhận, chuyển rà lại kết hợp** (2026-10-31)

Biên tập viên áp dụng mọi phát hiện của `reviews/6-ra-lai-toan.md` và `7-ra-lai-mach.md` (mục "Vòng 2" của `bien-tap-vong-1.md`); bảy chỗ cắt K1–K7. Thân bài 11 973 tiếng, phụ lục 1182; `forward_refs.py` 0 (một tham chiếu mới tới Ví dụ 05.3 ở cuối §3 đã được gỡ); `sync --check` OK. Điều phối viên đọc toàn bộ diff vòng 2 (`lec05-round2.diff`, 130 dòng): câu cuối §6 đúng lượng giảm $2\eta(F(w_t)-F(u))$ trừ $\eta^2G^2$; câu cuối §4 đúng M8; "mức sàn sai số" chỉ còn nghĩa mức dao động của điểm lặp cuối, $\eta G^2/2$ gọi là "số hạng/mức sàn của cận"; $0{,}140625$ in đủ. Còn lại: cách viết số lớn chưa thống nhất ($2{,}7136\cdot10^4$ trong bảng lô nhỏ; $640\,000$ và $6{,}4\cdot10^5$) — giao rà lại kết hợp kiểm toàn bài.

## Rà lại kết hợp vòng 2 — quyết định của điều phối viên: **chấp nhận, sửa nhẹ** (2026-10-31)

`reviews/8-ra-lai-vong-2.md`: 0/0/0/6; mọi phát hiện của `6-ra-lai-toan.md`, `7-ra-lai-mach.md` đã xử lý; các câu đổi ở vòng 2 dựng lại đúng; `forward_refs.py` 0; thân bài 11 973. Sáu điểm nhẹ gửi biên tập viên. Cách viết số: điều phối viên chốt quy tắc mới trong `van-phong.md` §12 (số nguyên từ năm chữ số trong công thức tách nhóm bằng `\,`, như Bài 02–03). $P_\xi$ hai cách dùng (một lần rút; cả dãy): ghi rõ ở `ky-hieu.md`.

Kiểm định sơ bộ của điều phối viên (Playwright, cổng 8766 phục vụ gốc học phần, scratchpad `final05/final05.py`, `probe.py`): 1584 công thức, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng ở cả HTTP và `file://`; nhưng ở 390×844 có 43 công thức hiển thị rộng hơn khung (cuộn ngang bên trong công thức; Bài 04: 0). Giao biên tập viên tách dòng theo cách của Bài 04, đo lại đến khi bằng 0.

## Kiểm định cuối và công bố ghi chú — Bài 05 (2026-10-31)

Vòng sửa cuối (sáu điểm nhẹ của `reviews/8-ra-lai-vong-2.md`, cách viết số theo `van-phong.md` §12, tách dòng 43 công thức tràn ở 390 px; mục "Vòng 3" của `bien-tap-vong-1.md`). Điều phối viên đọc diff phần chữ (cắt: đoạn (O1)/(O2) cuối §2, nửa lộ trình Mệnh đề 05.5, mệnh đề phụ về $\mathcal F_t$, câu dẫn Bước 3 Ví dụ 05.6, câu cuối Ví dụ 05.12; đúng quyết định) và so nội dung công thức hiển thị trước và sau khi tách dòng (scratchpad `m/mathcmp.py`): chỉ khác ở các sửa có chủ ý ($\cdot$, $0{,}140625$, $640\,000$). Thân bài 11 984 tiếng, phụ lục 1189.

Kiểm định do điều phối viên chạy (Playwright, Chromium, scratchpad `final05/final05.py`, `probe.py`, `idx_note.py`; máy chủ cổng 8766 phục vụ gốc học phần), qua HTTP và `file://`, ở 1600×900 và 390×844, mở hết khối thu gọn: 1579 công thức, 15 khối thu gọn, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 thông báo lỗi console, 0 công thức hay bảng tràn (Bài 04 cũng 0), độ rộng tài liệu 375 px ở 390; bản in A4 54 trang. Điều phối viên xem ảnh đầu trang 1600, ba ảnh cuộn ở 390, hai trang PDF: không chồng lấn, không tràn. `forward_refs.py` 0; `sync --check` OK; `git diff --check` sạch; không có chữ có dấu trong `\text{}`. Thẻ Bài 05 ở `2627-1/index.html` liên kết ghi chú; mở từ chỉ mục qua HTTP và `file://` đúng tiêu đề.

**Trạng thái:** ghi chú Bài 05 hoàn tất; commit và push. Việc tiếp theo: bài tập (`exercises.md`) theo `outline.md` §4 (và ghi chú cho người viết bài tập ở cuối `outline.md`).

## Bài tập — bắt đầu (2026-10-31)

Giao một người viết soạn `exercises.md` theo `outline.md` §4 và §12 của ghi chú (12 bài: 05.1–05.6 gốc theo blueprint 5.5; 05.7–05.12 là UML 12.1, 12.2, 12.3, 14.3 ý 1–3, 14.4 thêm phép chiếu, 9.2 tùy chọn) và ghi chú của biên tập viên ở cuối `outline.md` §13: thêm một ý dựng oracle có $\mathbb E\lVert g\rVert^2$ không bị chặn trên $W$ (mục tiêu 5, giả thiết (G2)); Bài tập 05.1 chứng minh đủ dưới vi phân của hàm lỗi bản lề tại điểm gãy (Ví dụ 05.2 hứa). Công thức hiển thị viết nhiều dòng để vừa 390 px; độ dài ≤ 10 000 tiếng.

## Bài tập — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-31)

`exercises.md`: 12 bài (05.1–05.6 gốc; 05.7–05.12 là UML 12.1, 12.2, 12.3, 14.3 ý 1–3, 14.4 thêm phép chiếu, 9.2; số bài đã đối chiếu PDF tr. 128, 169, 201), 8311 tiếng (đích ≤ 10 000), 44 khối (12 đề, 20 gợi ý, 12 lời giải). Người viết tự giải trước rồi mới đối chiếu bản lời giải; ghi chỗ hổng ở 14.3 (ý 1, ý 3), 14.4 (không có lời giải), lỗi nhỏ ở 12.1–12.3 trong `bai-tap-ghi-chu.md`. Sai khác với dàn ý §4 (chấp nhận để rà): 05.4 thay ý thừa số $(c+1/c)/2$ (trùng Ví dụ 05.8) bằng ý $\eta$ cố định và ý ước lượng sai $G$; 05.6(e) oracle đuôi nặng, (G1) đúng, $\mathbb Eg^2=\infty$ (ghi chú của biên tập viên); 05.1(b) chứng minh đủ dưới vi phân tại điểm gãy; 05.10 viết $w^\circ$ cho $w^\star$ của UML và chạy với $W=\mathbb R^p$; thêm ý ở 05.2, 05.7, 05.9, 05.12 ($\beta=\tfrac43$). Kiểm tra do điều phối viên chạy: `sync --check` OK; 88 dòng `:::` (44 khối); `probe.py` ở 390×844 với mọi khối mở: 0 công thức tràn. Điều phối viên đọc phần mở đầu và Bài tập 05.1: đúng mẫu Bài 04, lời giải từng bước. Bản đóng băng: scratchpad `lec05-ex-frozen.md`.

## Rà bài tập — quyết định của điều phối viên: **yêu cầu sửa** (2026-10-31)

Rà toán (`reviews/9-bai-tap-toan.md`): 0/0/0/6; tự giải mọi bài, mọi số đúng trừ $0{,}9950$ (phải $0{,}9951$); 05.1(b), 05.3, 05.6(e) (với $W=\mathbb R$, $\mathbb EF(\bar w_T)=\infty$ với mọi $T\ge2$), 05.10 ($W=\mathbb R^p$ thỏa Hệ quả 05.16) đúng; đề và số bài UML trung thành; không chép bản lời giải. Rà sư phạm (`reviews/10-bai-tap-su-pham.md`): 0/0/4/13; phủ năm mục tiêu; $w^\circ$ chấp nhận được. Quyết định gộp: `reviews/11-quyet-dinh-bai-tap.md` (T1–T4 và các điểm nhẹ; 05.7 dùng cấu trúc riêng thay vì cấu trúc trùng bản lời giải UML; 05.5(a) thay bằng biến thể không phải nhân hằng số).

## Sửa bài tập — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-31)

Người soạn áp dụng T1–T4 và mọi điểm nhẹ (`bai-tap-ghi-chu.md` §8; hai ngoại lệ một phần có lý do: 05.1(c) giữ làm bài gốc 1 của blueprint với số liệu khác Ví dụ 05.2; 05.2(c) đổi sang bước thứ ba với $i_3=1$, $u=w^*$). 05.7 cấu trúc riêng ($((1,0),1)$, $((1,1),0)$; cực tiểu địa phương $(-1,-1)$, $L_S=\tfrac12$; điểm $(1,-2)$ có $L_S=0$), hai gợi ý; 05.5(a) với $\sigma^2=3$ ($T=400,200,119,105$; GD $100$), (b) $b\ge10\sigma^2$ ($3300$; $16\,500$); 05.11(d) $T\ge14\,400$ (giữ mục tiêu 3; ghi chú không cần sửa); cận làm tròn lên ($0{,}9951$; $0{,}7072$; $5{,}0068$; $477{,}11$). $9267$ tiếng, 45 khối. Điều phối viên tự kiểm: cực tiểu địa phương của 05.7 (trong quả cầu bán kính $\tfrac12$ hai dấu không đổi), bảng 05.5(a), $3300$, $16\,500$, $10/\sqrt{101}=0{,}99504$, $14\,400$; `sync --check` OK. Diff `lec05-ex-r1.diff` (579 dòng) giao rà lại.

## Rà lại bài tập — quyết định của điều phối viên: **chấp nhận, sửa nhỏ** (2026-10-31)

Rà lại toán (`reviews/12-ra-lai-bai-tap-toan.md`): 0/0/0/1; 6/6 phát hiện cũ ✓; mọi phần sửa dựng lại đúng; 52 số mới đúng, mọi cận làm tròn lên; nhẹ: 05.2(c) in $0{,}00344$ "theo Ví dụ 05.7" trong khi ghi chú in $0{,}0034$. Người rà chỉ ra **quyết định của điều phối viên ở `11-quyet-dinh-bai-tap.md` (05.10(d)) nhầm**: Bước 5 của lời giải chứng minh mọi $\eta>0$ cho cùng phân lớp, nên chỉ số vòng lặp $T$ cần $\lVert w^\circ\rVert$; lời giải hiện tại (Bước 6) đúng. Điều phối viên kiểm lại và chấp nhận; không sửa thêm. Rà lại sư phạm (`reviews/13-ra-lai-bai-tap-su-pham.md`): 0/0/0/5; 15/17 ✓, 2 một phần có lý do (chấp nhận); năm điểm nhẹ ("gần như đứng yên" ở 05.5(a); chữ $L$ cho hằng số Lipschitz ở 05.8(b); $0{,}00344$; định dạng tiếng Anh ở 05.11 gợi ý 1 và 05.8(c); dòng mục tiêu 05.10 dài 41 tiếng). Gửi người soạn sửa sáu điểm nhẹ; không cần rà lại.

## Kiểm định cuối và công bố bài tập — Bài 05 (2026-10-31)

Người soạn sửa sáu điểm nhẹ của `reviews/12-ra-lai-bai-tap-toan.md` và `13-ra-lai-bai-tap-su-pham.md` (`bai-tap-ghi-chu.md` §8): 05.2(c) tính $0{,}00344$ từ Bước 1 và ghi rằng Ví dụ 05.7 in $0{,}0034$; 05.5(a) phần vượt $T(b)-100\approx300/b$ ($19$ ở $b=16$, $5$ ở $b=64$; điều phối viên kiểm lại); 05.8 dùng $G'$ thay $L$, tách Bước 3; định dạng tiếng Anh ở 05.8(c), 05.11 gợi ý 1; tách dòng mục tiêu 05.10. Điều phối viên đọc toàn bộ diff (đúng sáu điểm, không đổi gì khác). $9283$ tiếng, 45 khối.

Kiểm định do điều phối viên chạy (Playwright, Chromium, `final05/final05.py`, `probe.py`, `idx.py`), qua HTTP (cổng 8766) và `file://`, ở 1600×900 và 390×844, mở hết khối thu gọn: 1432 công thức, 33 khối thu gọn, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 thông báo lỗi console, 0 công thức hay bảng tràn, độ rộng tài liệu 375 px ở 390; bản in A4 39 trang. Điều phối viên xem ảnh đầu trang 1600 và ảnh cuộn 390: không chồng lấn, không tràn. `sync --check` OK; `git diff --check` sạch; không có "Đáp án", "rõ ràng", "dễ thấy", "Mục này". Thẻ Bài 05 ở `2627-1/index.html` liên kết bài tập; mở từ chỉ mục qua HTTP và `file://` đúng tiêu đề.

**Trạng thái:** Bài 05 (ghi chú và bài tập) hoàn tất; commit và push. Điều kiện "Done means" của học phần thỏa: mọi phát hiện chặn bàn giao và nghiêm trọng đã xử lý và ghi lại (N1 của ghi chú; không có lỗi nghiêm trọng ở bài tập); `outline.md` (§13 sai khác khi viết và ghi chú biên tập) và nhật ký khớp ghi chú; trình xem hiển thị ghi chú và bài tập qua HTTP và `file://` ở hai cỡ và bản in; `material-local-data.js` đồng bộ; thẻ chỉ mục liên kết ghi chú và bài tập sau khi qua rà soát.
