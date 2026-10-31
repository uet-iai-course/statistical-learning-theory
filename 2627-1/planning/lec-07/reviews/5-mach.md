# Rà soát 5 — Mạch và móc nối, ghi chú Bài 07 (bản đóng băng)

Người rà: vai trò 5 (mạch và móc nối), chỉ đọc. Đối tượng: `scratchpad/lec07-draft-frozen.md` (SHA-256 bắt đầu `90e35e5025ff45db`, đã kiểm khớp; 1 088 dòng; thân bài 11 999 tiếng theo `wc -w` dòng 1–958, phụ lục 1 634). Số dòng dưới đây là số dòng của bản đóng băng. Đề xuất câu chữ đã soát theo `no-ai-slop` chế độ Detect.

## 1. Tổng kết theo mức

| Mức | Số | Nội dung chính |
|---|---|---|
| chặn bàn giao | 0 | — |
| nghiêm trọng | 0 | — |
| trung bình | 3 | danh sách tiên quyết thiếu và thừa số hiệu; cầu nối Bài 08 ngầm hứa bỏ tính lồi; $\rho_j$ ở Nhận xét 07.18 trùng $\rho_m$ và trái với quy ước "viết $G$ thay cho $\rho$" của chính bài |
| nhẹ | 14 | lời hứa Bài 03 dòng 921 (§28.1) và Bài 05 dòng 1100 chỉ giữ ngầm; câu mở §9 không báo ba khối cuối mục; Bổ đề 07.8, Ví dụ 07.11 và Nhận xét 07.18 không có câu dẫn; vài dẫn chiếu chưa đúng chỗ (Nhận xét 02.11, $\rho_m\ge3{,}33$, "$\tfrac14$ (Mệnh đề 07.2)", "$B$ (§8)"); kí hiệu $\lvert E\rvert$, chỉ số $k$, $j$ trùng nghĩa; "lớp" trơn cho lớp nơ-ron; một câu khuyên chung chung; lặp "bằng chứng, không phải chứng minh" |

Mạch tổng thể tốt: mỗi mục §4–§9 mở bằng vấn đề và kết bằng một câu văn xuôi dẫn sang mục sau; câu hỏi mở đầu được trả lời ở §6 (Ví dụ 07.5), §9 (Ví dụ 07.10) và §10 (đoạn đầu); ba ví dụ xuyên suốt được dùng nhất quán; cầu nối sang Bài 08 khớp blueprint 7.6 và không phát biểu kết quả của Bài 08. Mọi 69 lần dẫn số hiệu 01.x–06.x trỏ đúng khối và đúng nội dung (trừ một chỗ ở mục 5, F7). Tham chiếu nội bộ §k, Phụ lục A–D, Ví dụ 07.k, Bài tập 07.k đều đúng chỗ.

## 2. Kết quả `forward_refs.py`

Bản sao: `scratchpad/reviews07/r5/lec-07/lecture-note.md`. Lệnh `python3 /data/tqlong/lectures/tools/courses/statistical-learning-theory/scripts/forward_refs.py <bản sao>` in `0 forward references` (mã thoát 0).

Kiểm tay thêm: không có dẫn chiếu tới khối 07.k nằm sau trong thân bài. Các lần dùng thuật ngữ trước định nghĩa đều kèm con trỏ mục và thuộc phần thiết lập: "hàm lỗi dốc" (dòng 81, định nghĩa dòng 693), "độ phức tạp Rademacher thực nghiệm", "biến Rademacher" (bảng dòng 92–94, định nghĩa §6), "phép nội suy" (dòng 82, định nghĩa dòng 235); "ReLU" dùng ở dòng 9 với công thức $\max\{0,\cdot\}$ tại chỗ, tên đầy đủ tiếng Anh chỉ có ở bảng §2 (dòng 108). Xem F15.

## 3. Bảng lần dùng đầu của kí hiệu mới

| Kí hiệu | Dùng đầu (dòng) | Định nghĩa hay đặt tên (dòng) | Nhận xét |
|---|---|---|---|
| $\varsigma$ | 141 | 141, 144 (Định nghĩa 07.1) | lý do bỏ $\sigma$ ở dòng 159 |
| $J$, $N_j$, $N$ | 143 ($N=2000$ đã dùng ở dòng 9 theo nghĩa số nơ-ron ẩn) | 143 | nhất quán: với $J=2$, độ rộng là số nơ-ron ẩn |
| $\Theta_j$, $b_j$, $\theta$, $f_\theta$, $h_\theta$ | 145–154 | 145–154 | đạt |
| $P$ | 233 | 233 (Định nghĩa 07.4) | đạt |
| $\mathcal H_{J,N}$, $\mathcal F_{J,N}$ | 248 | 248 (Định nghĩa 07.5) | đạt |
| $\mathcal H_{J,N}(B)$, $B$ | 249 | 246, 249 | bảng §2 ghi $B$ "(§8)" — F11 |
| $\hat\theta$, $A$, $\xi$ | 246–250 | 246, 250; $\xi$ theo Định nghĩa 05.18 | Định nghĩa 05.18 không có trong danh sách tiên quyết — F1 |
| $\lVert\cdot\rVert_F$, $\lVert\cdot\rVert_{\mathrm{op}}$ | 272, 282 | 272, 282 | đạt |
| $\chi$, $v_j$, $b_{1j}$, $\hat w$ | 295–301 | 295–301 (Ví dụ 07.3) | đạt |
| $\lvert E\rvert$ | 313 | không định nghĩa (kí hiệu cạnh của UML) | F12 |
| $\sigma_i$ (biến Rademacher) | 320 (tên "dấu ngẫu nhiên" của Bài 03) | 325 (Định nghĩa 07.7) | ở câu ôn nhanh 1 (dòng 50) $\sigma_i$ được mô tả tại chỗ |
| $\Omega$, $\omega_{1:m}$, $\mathcal F\circ\omega_{1:m}$ | 323, 333 | 323, 333 | đạt |
| $\widehat{\mathfrak R}(A)$ | 329 | 329 | đạt |
| $\widehat{\mathfrak R}_{\omega_{1:m}}$, $\widehat{\mathfrak R}_S$ | 336, 341 | 336, 341 | đạt |
| $\mathfrak R_m$ | 342 | 342 | đạt |
| $\bar a$ | 358 | 358 (Bổ đề 07.8) | đạt |
| $\tau_i$ | 419 | 419 (Mệnh đề 07.9) | đạt; $\kappa$ ở Phụ lục A tránh trùng |
| $\mathcal G$ | 431 | 431 (Mệnh đề 07.9(b)), dùng lại tổng quát ở 511 | đạt; khớp `ky-hieu.md` |
| $Q$, $c_i$ | 490–491 | 490–491 | đạt |
| $L_D(g)$, $L_S(g)$ | 505 | 505 | đạt |
| $\Psi$, $S'$, $s^{(i)}$ | 535, 539, 561 | 535, 539; $s^{(i)}$ "như Bài 06" | Định nghĩa 06.9 không có trong danh sách tiên quyết — F1 |
| $\mathcal F_B$ | 610 | 610 (Mệnh đề 07.13) | đạt; khớp `ky-hieu.md` |
| $v_\sigma$ | 626 | 626 | đạt |
| $\phi_i$, $\phi$, $G$ | 675–676 | 675–676 | đạt |
| $\phi_\gamma$, $\ell_\gamma$, $L^\gamma_D$, $L^\gamma_S$, $L^{<\gamma}_S$ | 692–694 | 692–694 (Định nghĩa 07.15) | đạt |
| $\gamma$ | 85 (chữ "lề $\gamma$"), 131 | 691–692 | dùng trước bằng chữ, có con trỏ §8 |
| $\mathcal G_\gamma$ | 735 | 735 | đạt |
| $\gamma_k$, $q_k$, $B_k$ | 810, 817 | 810, 817 | đạt |
| $F_\Theta$, $\varsigma_j$, $\rho_j$, $k$, $M_j$, $R_\Theta$ | 867–871 | 867–875 | $\rho_j$ trùng $\rho_m$; $k$, $j$ trùng nghĩa — F3, F13 |
| $r_j$ | 872 | 875 (mệnh đề "với $r_j=\ldots$" ngay sau công thức) | chấp nhận được |
| $\bar N$, $\lVert X\rVert_2$, $\tilde O$ | 879 | 883 (ngay sau công thức) | chấp nhận được |
| $\kappa$ | 963 | 963 (Phụ lục A) | đạt |

## 4. Mạch từng mục

- **Đoạn dẫn và câu hỏi mở đầu (dòng 3–27).** Dòng 3 nhắc đúng cầu nối cuối Bài 06 (Bài 06 dòng 1130: mạng lớn khớp nhãn ngẫu nhiên, đại lượng nào còn cho thông tin). Câu hỏi thẳng ở dòng 25 đúng `van-phong.md` §9a. Đoạn trả lời trỏ §6, §8, §9 và Phụ lục D, không dẫn số khối. Đạt.
- **Mục tiêu, tiên quyết, ôn nhanh.** Mục tiêu chỉ có chữ. Ba câu ôn nhanh được dùng lại đúng chỗ (câu 1 ở dòng 684, câu 2 ở dòng 305, câu 3 ở dòng 580). Danh sách tiên quyết thiếu và thừa (F1).
- **§1–§3.** §1 mở bằng câu khác biệt so với Bài 05–06; bảng nguồn ngẫu nhiên khớp. §3 đặt ví dụ phép hoặc loại trừ và ứng dụng văn bản; câu kết dòng 134 dẫn sang §4. Đạt.
- **§4.** Mở bằng vấn đề (dòng 138), kết bằng ba câu hỏi ứng với ba số hạng của Mệnh đề 04.3 (dòng 224). Đạt.
- **§5.** Mở bằng vấn đề (dòng 228), kết dòng 316 dẫn sang §6. Dòng 255 kết thúc bằng một câu khuyên chung chung trước Ví dụ 07.2 (F16).
- **§6.** Mở bằng Bước 2–3 của chứng minh Định lý 03.15 (giữ lời hứa Bài 03 dòng 868), kết dòng 480. Bổ đề 07.8 xuất hiện sau đoạn về nhãn thật mà không có câu dẫn; lần dùng đầu của nó ở §7 (Nhận xét 07.12) (F8).
- **§7.** Mở bằng Bước 1 và Bước 4 của chứng minh Định lý 03.15, nêu lý do cần bất đẳng thức McDiarmid; kết dòng 601. Đạt.
- **§8.** Mở bằng Ví dụ 07.6; các câu nối dòng 669, 686 dẫn lần lượt tới bổ đề co và hàm lỗi dốc; dòng 703 dùng lại ví dụ phép hoặc loại trừ; kết dòng 757. Đạt.
- **§9.** Câu mở (dòng 761) báo ba việc (so với cận VC, hàm lỗi bình phương, thí nghiệm) nhưng mục có thêm Nhận xét 07.17, Ví dụ 07.11 và Nhận xét 07.18. Nhận xét 07.17 có câu dẫn (dòng 807); Ví dụ 07.11 và Nhận xét 07.18 thì không (F9). Câu kết dòng 888 đạt.
- **§10.** Trả lời câu hỏi mở đầu ở đoạn đầu; năm giới hạn mỗi ý trỏ một khối; câu thực hành cuối đạt. Chỗ "$\tfrac14$ (Mệnh đề 07.2)" xem F10.
- **§12 và cầu nối.** Câu hỏi cuối buổi dùng Hệ quả 07.16, Nhận xét 07.17, Ví dụ 07.11. Cầu nối khớp blueprint ("A class-based measure does not fully describe which predictor training selects. Can the trajectory of SGD help?"), nhưng câu về Bài 06 ngầm hứa Bài 08 bỏ tính lồi (F2).
- **Ví dụ xuyên suốt.** Phép hoặc loại trừ: Ví dụ 07.1 → Mệnh đề 07.2 → Ví dụ 07.2 → lề ở dòng 703 → §10; thí nghiệm: mở đầu → Ví dụ 07.3, 07.5, 07.6, 07.10 → §10 → cầu nối; ứng dụng văn bản: §3 → Ví dụ 07.5 (kết luận) → Ví dụ 07.8 → Ví dụ 07.11 ($m=10^4$, $\lVert x\rVert\le1$). Số liệu khớp nhau giữa các lần nhắc ($916$, $10\,853$, gần $12$ lần, $1{,}2881$, $0{,}2407$, $0{,}2576$, $0{,}0192$, $75$).
- **Lặp.** "Bằng chứng, không phải chứng minh" ở dòng 27, 847, 1088; ý "cận cấp lớp không nói thuật toán chọn hàm nào" ở dòng 253, 531, 726, 888, 900, 945. Lần đầu là luận điểm của bài; các lần sau có thể cắt để lấy chỗ cho các đề xuất thêm chữ (F17).

## 5. Móc nối với Bài 01–06

**Số hiệu.** Đã grep 69 lần dẫn của 37 số hiệu 01.x–06.x với tiêu đề khối trong `materials/lec-0x/lecture-note.md`. Tất cả trỏ đúng loại khối, đúng số. Nội dung đã đối chiếu: Định lý 03.15 (bán kính VC $\rho_m=\sqrt{8\ln(4\Pi(2m)/\delta)/m}$; Bước 1 Chebyshev và mẫu bóng, Bước 2 dấu ngẫu nhiên, Bước 3 đếm trên mẫu gộp, Bước 4 Hoeffding); Ví dụ 03.3 Bước 3 (cách gán nhãn chéo và cách gán nhãn bù, tức phép hoặc loại trừ, không thực hiện được); Nhận xét 03.10 (ii) $\mathcal H_{\sin}$, (iii) ba hàm, khớp các nhãn $(0,1)$, $(1,0)$, $(1,1)$; Mệnh đề 03.9(b) chiều VC bằng $p$; Ví dụ 03.1 $\mathbb 1[x\ge t]$ cho bốn véc-tơ ở Ví dụ 07.4; (M) ở đoạn trước Nhận xét 03.14, (T5) ở đoạn trước Định lý 03.15, (T3) ở đoạn sau Nhận xét 02.8; Định nghĩa 04.1 có $L^*$; Mệnh đề 04.3 có số hạng $2r$; Định nghĩa 05.18 có $\xi$; Định nghĩa 05.4 dùng $G$; Hệ quả 02.10(b) bán kính $\sqrt{\ln(2/\delta)/(2m)}$; Định nghĩa 06.9 cho $s^{(i)}$, $z'$; Ví dụ 06.7 có $W=[-1,1]$ và hàm lỗi bình phương. Chỗ lệch nội dung duy nhất: Nhận xét 02.11 nói về hàm lỗi bình phương và hàm lỗi log, không nhắc hàm lỗi bản lề (F7).

**Lời hứa.**

| Lời hứa | Nội dung | Chỗ giữ trong Bài 07 | Đánh giá |
|---|---|---|---|
| Bài 03 dòng 868 | "độ phức tạp Rademacher (Bài 07)"; phép đếm ở Bước 3 cần nhãn $\{0,1\}$ | §6 câu mở (dòng 320); dòng 484 | giữ |
| Bài 03 dòng 921 | UML §28.1 "cận hội tụ đều qua độ phức tạp Rademacher, chuẩn bị Bài 07" | dàn ý §12 hẹn giữ ở §6 và §13; §13 không nhắc §28.1 | giữ một nửa — F4 |
| Bài 05 dòng 1100 | cận thống kê cho hàm lỗi lồi và Lipschitz (ghép với Mệnh đề 04.3 cho hàm lỗi logistic hay bình phương) thuộc Bài 06–07 | Ví dụ 07.9 (kết luận dòng 804), Ví dụ 07.11 Bước 4, §10 đoạn 2 | giữ ở dạng tổng quát; chưa nối tường minh với Mệnh đề 04.3 và hàm lỗi logistic — F5 |
| Bài 06 dòng 854 | lớp của Ví dụ 06.7 hội tụ đều, "chứng minh ở Bài 07" | Ví dụ 07.9 | giữ đủ |
| Cầu nối cuối Bài 06 (dòng 1130) | mạng lớn khớp nhãn ngẫu nhiên; đại lượng nào còn cho thông tin | dòng 3, câu hỏi mở đầu, Ví dụ 07.5, 07.10, §10 | giữ đủ; câu cuối dòng 1130 hẹn Bài 08 xét SGD nhiều vòng với hàm lỗi lồi, trơn — liên quan F2 |

**Danh sách tiên quyết (dòng 41–46).** Thiếu: Định nghĩa 04.1 (dòng 213), Định nghĩa 05.18 (dòng 246), Ví dụ 03.1 (dòng 405), Định nghĩa 06.9 (mẫu lân cận $s^{(i)}$, dòng 561 "như Bài 06"); Định lý 03.15 ghi "Bước 1–2" nhưng thân bài dùng Bước 1, 2, 3, 4 (dòng 320, 484). Thừa: Ví dụ 05.10 không được dẫn trong thân bài. Các số hiệu còn lại đều được dùng.

**Kí hiệu và thuật ngữ.** Khớp `ky-hieu.md` (Bài 07: $J$, $N_j$, $N$, $\Theta_j$, $b_j$, $\theta$, $P$, $\varsigma$, $\mathcal H_{J,N}$, $\mathcal F_B$, $\mathcal G$, $\sigma_i$, $\tau_i$, $\phi_\gamma$, $L^{<\gamma}_S$, $\chi$) và `thuat-ngu.md` §10, trừ: $\rho_j$ (F3); "lớp" trơn cho lớp nơ-ron ở tiêu đề Ví dụ 07.2 (F14); "lớp hàm lỗi" (thuật ngữ mới của Bài 07 trong `thuat-ngu.md`) chưa có tiếng Anh ở lần dùng đầu (dòng 110) (F15). Nhãn $\tilde y=2y-1$, $h_w$, $h_{w,0}$, $C_x$, $G$, $B$ dùng đúng nghĩa của Bài 05–06.

**Cầu nối sang Bài 08 (dòng 945).** Khớp blueprint 7.6 và mở đầu blueprint 8.1 (số bước huấn luyện); không phát biểu kết quả của Bài 08. Vấn đề ở F2.

## 6. Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | F1 · dòng 41–45 (Kiến thức tiên quyết) | Danh sách tiên quyết thiếu bốn số hiệu được dùng, ghi sai phạm vi các bước của Định lý 03.15 và có một số hiệu không dùng | Dòng 213 "sai số xấp xỉ (Định nghĩa 04.1)"; dòng 246 "(Định nghĩa 05.18)"; dòng 405 "lớp hàm ngưỡng của Ví dụ 03.1"; dòng 561 "$s^{(i)}$ … (như Bài 06)"; dòng 43 "Định lý 03.15 với Bước 1–2 của chứng minh" nhưng dòng 320 dùng Bước 3 và dòng 484 dùng Bước 4; dòng 45 "Ví dụ 05.10" không xuất hiện trong thân bài | Sửa dòng 43: "Ví dụ 03.1, 03.3, 03.8; …; Định lý 03.15 với Bước 1–4 của chứng minh". Dòng 44: "**Từ Bài 04.** Định nghĩa 04.1, Mệnh đề 04.3, Bổ đề 04.9, Ví dụ 04.10." Dòng 45: "… Định nghĩa 05.4, 05.18, Mệnh đề 05.5; Định nghĩa 06.9; Ví dụ 05.10, 06.7." Giữ Ví dụ 05.10 nếu nhận F10 (dẫn ở §10), nếu không thì bỏ. Tăng khoảng 8 tiếng |
| trung bình | F2 · dòng 945 (cầu nối) | Câu về Bài 06 đặt "nhưng với hàm lỗi lồi" ngay trước câu hỏi cho Bài 08, nên đọc như Bài 08 bỏ được tính lồi. Theo blueprint 8.1–8.2 và cầu nối cuối Bài 06 (dòng 1130), Bài 08 vẫn giả thiết hàm lỗi lồi, trơn, Lipschitz. Câu hỏi nhảy sang SGD, trong khi thí nghiệm dùng bình phương tối thiểu; mối nối (nghiệm nội suy chuẩn nhỏ nhất là giới hạn của hạ gradient khởi tạo tại $0$) chỉ nằm ở Phụ lục D | Dòng 945: "Bài 06 chặn khoảng cách tổng quát hóa qua tính ổn định của một thuật toán, nhưng với hàm lỗi lồi." | Thay hai câu cuối: "Trong thí nghiệm, nghiệm nội suy chuẩn nhỏ nhất cũng là giới hạn của hạ gradient khởi tạo tại $0$ (Phụ lục D), nên chuẩn của nghiệm do quỹ đạo tối ưu quyết định. Bài 06 chặn khoảng cách tổng quát hóa qua tính ổn định đều, một tính chất của thuật toán chứ không của lớp. Câu hỏi cho Bài 08 là: quỹ đạo của SGD, qua số bước và độ dài bước, có cho một bảo đảm cho chính hàm mà SGD trả về không?" Tăng khoảng 25 tiếng; bù bằng F17 |
| trung bình | F3 · Nhận xét 07.18, dòng 867, 871 | $\rho_j$ là hằng số Lipschitz của hàm kích hoạt, trong khi $\rho_m$ là bán kính VC (`ky-hieu.md`; dùng ở dòng 307, 774) và §13 của chính bài ghi "hằng số Lipschitz của bổ đề co viết $G$ thay cho $\rho$" | Dòng 867 "mỗi $\varsigma_j$ là $\rho_j$-Lipschitz … (ReLU: $\rho_j=1$)"; dòng 871 "$\prod_j\rho_j\lVert\Theta_j\rVert_{\mathrm{op}}$"; dòng 956 "viết $G$ thay cho $\rho$" | Đổi $\rho_j$ thành $G_j$ ở dòng 867 và 871 ("mỗi $\varsigma_j$ là $G_j$-Lipschitz … (ReLU: $G_j=1$)"; "$\prod_jG_j\lVert\Theta_j\rVert_{\mathrm{op}}$"). Không đổi số tiếng |
| nhẹ | F4 · §13, dòng 951 | Lời hứa Bài 03 dòng 921 (UML §28.1 "chuẩn bị Bài 07") không được nhắc lại; dàn ý §12 hẹn giữ ở §13 | Bài 03 dòng 921: "§28.1: cận hội tụ đều qua độ phức tạp Rademacher, chuẩn bị Bài 07"; §13 chỉ dẫn §26.1–26.3, §15.2.3, §20 | Thêm vào ý "Mở rộng": "UML §28.1 (cận VC suy từ độ phức tạp Rademacher và hàm tăng trưởng)". Tăng khoảng 12 tiếng; nội dung §28.1 cần người rà chuyên gia kiểm trên PDF |
| nhẹ | F5 · Ví dụ 07.9 Bước 5 (dòng 802) hoặc Ví dụ 07.11 Bước 4 (dòng 859) | Lời hứa Bài 05 dòng 1100 nhắc Mệnh đề 04.3 và hàm lỗi logistic, bình phương; Bài 07 chỉ giữ ở dạng tổng quát ("hàm lỗi Lipschitz theo điểm số và bị chặn"), không nối lại với Mệnh đề 04.3 | Bài 05 dòng 1100: "Mệnh đề 04.3 cần hàm lỗi trong $[0,1]$ và một bán kính hội tụ đều … cận thống kê cho hàm lỗi lồi và Lipschitz thuộc Bài 06–07"; dòng 804 Bài 07 không nhắc Mệnh đề 04.3 | Cuối Bước 5 (dòng 802) thêm: "Đây là bán kính hội tụ đều mà Mệnh đề 04.3(a) cần cho hàm lỗi $\ell/4$." Tăng khoảng 14 tiếng |
| nhẹ | F6 · dòng 774 | Đoạn sau Định lý 03.15 nói $\rho_m\ge3{,}33$ khi $d=\infty$; ở đây $d=p$ hữu hạn, cần thêm bước $d\ge2m\Rightarrow\Pi(2m)=2^{2m}$ | Bài 03 dòng 572: "Khi $d=\infty$, $\Pi_{\mathcal H}(2m)=2^{2m}$, nên $\rho_m\ge\sqrt{16\ln2}\approx3{,}33$"; Bài 07 dòng 774: "Với $d=p>2m$, Định lý 03.15 chỉ cho $\rho_m\ge3{,}33$ (đoạn sau Định lý 03.15)" | "Với $d=p>2m$, một bộ $2m$ điểm bị tách trọn, nên $\Pi(2m)=2^{2m}$ và $\rho_m\ge3{,}33$ như đoạn sau Định lý 03.15." Tăng khoảng 10 tiếng |
| nhẹ | F7 · dòng 859 | Nhận xét 02.11 không nói hàm lỗi bản lề và logistic không bị chặn; nó nói hàm lỗi bình phương và hàm lỗi log, và hệ quả của việc không bị chặn | Bài 02 dòng 578: "Hàm lỗi bình phương … hay hàm lỗi log …"; Bài 07 dòng 859: "Hàm lỗi bản lề và logistic không bị chặn trên $\mathbb R^p$ (Nhận xét 02.11)" | "Hàm lỗi bản lề và logistic không bị chặn khi $w$ chạy trên $\mathbb R^p$, nên không thỏa giả thiết giá trị trong $[0,1]$; …" và bỏ dẫn Nhận xét 02.11 ở đây (hoặc dẫn "như hàm lỗi log ở Nhận xét 02.11"). Không đổi số tiếng |
| nhẹ | F8 · trước Bổ đề 07.8 (dòng 351–353) | Bổ đề 07.8 đứng sau đoạn về nhãn thật mà không có câu dẫn; lần dùng đầu ở Nhận xét 07.12 (§7), rồi Ví dụ 07.11 và Phụ lục B | Dòng 351 kết bằng "nên đo riêng khả năng khớp của lớp"; dòng 353 mở khối bổ đề | Thêm một câu trước khối: "Ở §7–§8, ta cộng hằng số vào hàm lỗi, đổi dấu và nhân nó với một số; bổ đề sau cho biết độ phức tạp đổi thế nào." Tăng khoảng 25 tiếng |
| nhẹ | F9 · §9, dòng 761, trước dòng 850 và 864 | Câu mở §9 chỉ báo ba việc; Nhận xét 07.17, Ví dụ 07.11 (phản ví dụ bỏ giả thiết) và Nhận xét 07.18 không được báo; Ví dụ 07.11 và Nhận xét 07.18 không có câu dẫn | Dòng 761: "Ta so nó với cận VC khi $p\gg m$, dùng cùng công cụ cho hàm lỗi bình phương của Bài 06, rồi đọc lại thí nghiệm mở đầu." Dòng 848 đóng Ví dụ 07.10, dòng 850 mở Ví dụ 07.11 ngay | Dòng 761 thêm: "…, đọc lại thí nghiệm mở đầu, rồi xét giả thiết hàm lỗi bị chặn và cận cho mạng sâu." Trước dòng 850: "Ví dụ sau thay lớp hàm lỗi bằng lớp điểm số." Tăng khoảng 22 tiếng |
| nhẹ | F10 · dòng 892 | Số $\tfrac14$ của lớp afin đến từ Ví dụ 07.1, không từ Mệnh đề 07.2; câu "khả năng tối ưu cần lập luận riêng, vì Bài 05 dùng tính lồi" có thể dẫn Ví dụ 05.10 (đang thừa trong danh sách tiên quyết) | Dòng 892: "mạng hai nơ-ron ẩn có sai số xấp xỉ $0$ trên Ví dụ 07.1, lớp afin có $\tfrac14$ (Mệnh đề 07.2)" | "… lớp afin có $\tfrac14$ (Ví dụ 07.1, Mệnh đề 07.2); … khả năng tối ưu cần lập luận riêng, vì Bài 05 dùng tính lồi (Ví dụ 05.10)." Tăng khoảng 4 tiếng |
| nhẹ | F11 · bảng §2, dòng 107 | $B$ ghi "(§8)" nhưng được dùng từ Định nghĩa 07.5 (§5) và Ví dụ 07.3 | Dòng 107 "cận chuẩn của véc-tơ trọng số (§8)"; dòng 249 "$\lVert\theta\rVert\le B$" | "(§5, §8)". Tăng 1 tiếng |
| nhẹ | F12 · Nhận xét 07.6, dòng 313 | $\lvert E\rvert$ là kí hiệu tập cạnh của UML, chưa định nghĩa trong bài; khi mọi trọng số được huấn luyện, đó là $P$ của Định nghĩa 07.4 | Dòng 313 "Với hàm kích hoạt dấu và $\lvert E\rvert$ trọng số (kể cả hệ số tự do) … $(em)^{\lvert E\rvert}$ … $O(\lvert E\rvert\ln\lvert E\rvert)$" | Viết $P$ thay cho $\lvert E\rvert$: "Với hàm kích hoạt dấu và $P$ trọng số được huấn luyện (kể cả hệ số tự do), …" Không đổi số tiếng |
| nhẹ | F13 · Nhận xét 07.18, dòng 867 | Trong cùng khối, $j$ vừa là chỉ số lớp nơ-ron ($\Theta_j$) vừa là chỉ số nhãn ($\arg\max_jF_\Theta(x)_j$, $\max_{j\ne y}$); $k$ là số nhãn, trong khi Nhận xét 07.17 ngay trước dùng $k$ làm chỉ số lưới | Dòng 867 "nhãn dự đoán là $\arg\max_jF_\Theta(x)_j$ … $\max_{j\ne y}F_\Theta(x)_j$"; dòng 810 "$\gamma_k=2^{-k}$" | Dùng $c$ cho chỉ số nhãn: "$\arg\max_cF_\Theta(x)_c$", "$F_\Theta(x)_y-\max_{c\ne y}F_\Theta(x)_c$"; giữ $k$ cho số nhãn hoặc đổi thành $K$ (cả ở dòng 883). Không đổi số tiếng |
| nhẹ | F14 · tiêu đề Ví dụ 07.2, dòng 257 | "lớp" trơn cho lớp nơ-ron, trái `thuat-ngu.md` §10 ("không dùng 'lớp' trơn cho lớp nơ-ron"); "mạng hoặc loại trừ" là cụm khó đọc | "Ví dụ 07.2 (Đổi tỉ lệ hai lớp kề nhau của mạng hoặc loại trừ)" | "Ví dụ 07.2 (Đổi tỉ lệ hai lớp nơ-ron kề nhau của mạng biểu diễn phép hoặc loại trừ)". Tăng 3 tiếng |
| nhẹ | F15 · dòng 9, 110 | Tên đầy đủ của ReLU chỉ có ở bảng §2, sau lần dùng đầu; "lớp hàm lỗi" (thuật ngữ mới, `thuat-ngu.md` §10 "loss class") chưa có tiếng Anh ở lần dùng đầu | Dòng 9 "nơ-ron ReLU, mỗi nơ-ron tính $\max\{0,\langle v,x\rangle+c\}$"; dòng 108 "hàm ReLU (rectified linear unit)"; dòng 110 "ba điều cho lớp hàm lỗi" | Dòng 9: "nơ-ron ReLU (rectified linear unit)"; dòng 110: "lớp hàm lỗi (loss class)"; bảng §2 giữ "hàm ReLU". Tăng khoảng 5 tiếng |
| nhẹ | F16 · dòng 255 | Câu khuyên chung chung, không nói cần thận trọng vì sao (no-ai-slop: metadiscourse); lý do nằm ở Ví dụ 07.2 ngay sau | "Chuẩn của toàn bộ véc-tơ tham số cũng cần dùng thận trọng." | "Chuẩn của toàn bộ véc-tơ tham số còn đổi khi đổi tỉ lệ hai lớp nơ-ron mà hàm không đổi, như ví dụ sau." Tăng khoảng 10 tiếng |
| nhẹ | F17 · dòng 847, 888 (chỗ cắt để bù chữ) | Lặp: "bằng chứng, không phải chứng minh" đã ở dòng 27 và Phụ lục D dòng 1088; mệnh đề "không nói thuật toán nào chọn được hàm có chuẩn nhỏ" ở dòng 888 lặp lại ở §10 (dòng 900) và cầu nối (dòng 945) | Dòng 847 "Thí nghiệm là bằng chứng, không phải chứng minh: chuẩn và lề …"; dòng 888 "…, và không nói thuật toán nào chọn được hàm có chuẩn nhỏ." | Dòng 847: "**Kết luận.** Chuẩn và lề phân biệt hai trường hợp mà số tham số không phân biệt." (−8 tiếng). Dòng 888 bỏ vế cuối (−11 tiếng). Dòng 531 bỏ câu "Cận đúng đồng thời cho mọi $g$, …: đây là bảo đảm cấp lớp." vì dòng 253 đã nói (−35 tiếng, sửa câu cuối khối thành "Bảo đảm là cấp lớp; cận phụ thuộc $\delta$ qua $\ln(2/\delta)$, không phụ thuộc trực tiếp vào $p$."). Tổng cắt khoảng 54 tiếng |

**Cân đối ngân sách.** Nếu nhận mọi đề xuất thêm chữ (F1 ~8, F2 ~25, F4 ~12, F5 ~14, F6 ~10, F8 ~25, F9 ~22, F10 ~4, F11 1, F14 3, F15 ~5, F16 ~10; tổng khoảng 139 tiếng), các chỗ cắt ở F17 (~54) chưa đủ. Ưu tiên giữ F1, F2, F4, F5; nếu cần thêm chỗ, cắt Ví dụ 07.6 Bước 1 phần "$0{,}0815$; $0{,}0407$; $0{,}0041$ khi $m=2500$; $10^4$; $10^6$" chỉ giữ $m=2500$ và $10^4$ (−4), bỏ đoạn "Tham số hóa thừa không kéo theo nội suy, và nội suy không cần tham số hóa thừa." ở dòng 241 vì câu trước đã chỉ ra cả hai chiều (−15). Biên tập viên chốt bằng `wc -w` dòng 1 đến trước `## Phụ lục`.
