# Ghi chú của người viết bài tập — Bài 02 (2026-10-30)

Tệp nội bộ. Người viết bài tập duy nhất (`no-ai-slop` chế độ Edit). Sản phẩm: `materials/lec-02/exercises.md`. Không commit.

## 1. Thứ tự làm việc

1. Đọc toàn bộ ghi chú, `outline.md` §4 và ghi chú "Trạng thái cuối", `bien-tap-vong-1.md`, QĐ 8–9 trong `review-log.md`, mẫu `_templates/exercises.md`, `lec-01/exercises.md`, `van-phong.md` (§3a, §7, §7a, §9a, §12, §14), `thuat-ngu.md` §6, `ky-hieu.md`.
2. Đọc đề UML trên PDF: tr. 41–42 (Bài tập 2.3), 51–52 (3.4, 3.5), 58–59 (4.1, 4.2). Số bài khớp outline.
3. Tự giải cả 11 bài, tính lại mọi con số bằng Python trong scratchpad (`nums.py`, `sim.py`), viết lời giải.
4. Sau đó mới mở bản lời giải `MLbookSol.pdf` tr. 1–6, 9–10 để đối chiếu (mục 3 dưới).

## 2. Lời giải và con số then chốt (đã tính lại)

| Bài | Ý chính | Con số |
|---|---|---|
| 02.1 | (a) dấu bằng Markov khi và chỉ khi $V\in\{0,\alpha\}$; (b) không tương quan từng đôi đủ cho Chebyshev; (c) $V_3=V_1\oplus V_2$ độc lập từng đôi, $\operatorname{Var}=1/12$; (d) hàm sinh mô-men không tách; (e) cỡ mẫu | $(1+3e^2)/4=5{,}7918$, $((1+e)/2)^3=6{,}4259$; $2000$ và $737{,}78\to738$ |
| 02.2 | Chernoff với $C=\sum(b_i-a_i)^2$, $\tau=4m^2\epsilon/C$; $C\le m(b-a)^2$ | $C=2500$, $e^{-8}=3{,}35\cdot10^{-4}$; đoạn chung $e^{-1{,}25}=0{,}2865$ |
| 02.3 | $K$ biến cố đuôi dưới cho $L_S$ + $1$ biến cố đuôi trên tại $h_{\mathcal H}$ | $\ln2020=7{,}6109$, $1522{,}17\to1523$ so với $1658{,}81\to1659$; tiết kiệm $<2\ln2/\epsilon^2=138{,}6$ |
| 02.4 | $Y=0$, $h_k(x)=x_k$, $m=10$, $\epsilon=0{,}4$ | $2e^{-3{,}2}=0{,}0815$; đuôi một giả thuyết $22/1024=0{,}0215$; $1-(1-2^{-10})^K=0{,}6236$ ($K=1000$), $0{,}9924$ ($5000$); vượt $0{,}0815$ từ $K=88$ ($K=87$: $0{,}08149$) |
| 02.5 | Giao thức, so số nguyên tại biên | $p=0{,}02115$ và $8{,}94\cdot10^{-4}$; SE ($R=10^4$) $0{,}00144$, $2{,}99\cdot10^{-4}$; $R\ge1{,}117\cdot10^5$ cho SE $\le10\%$; mở rộng $0{,}00593$, $0{,}9974$. Mô phỏng thử ($R=10^4$): $0{,}0199$ và $0{,}0004$ (4 lần thất bại), khớp sai số chuẩn |
| 02.6 | $r_{m,k}=\sqrt{\ln(2/(w_k\delta))/(2m)}$, bất đẳng thức hợp đếm được | $w_k=2^{-k}$, $m=1000$: $0{,}0468$; $0{,}0729$; $0{,}1106$; $K=1000$ đều: $0{,}0728$. Dùng sai trọng số sau mẫu ($m=10$): bán kính $0{,}4295<\tfrac12$, thất bại với xác suất $\ge0{,}6236$ |
| 02.7 | Dải đóng $T_i$ khối lượng $\ge\epsilon/4$, dải mở $U_i\le\epsilon/4$ | $40\ln80=175{,}28\to176$; $4e^{-4{,}4}=0{,}0491$, $4e^{-4{,}375}=0{,}0504$ |
| 02.8 | $3^p+1$ hàm; thuật toán loại tục biến | $p=10$: $(\ln59\,050+\ln20)/0{,}1=139{,}82\to140$; bất khả tri $2\ln2\,362\,000/0{,}01=2935{,}004\to2936$; $\epsilon=0{,}05$: $279{,}6\to280$ và $11\,740{,}02\to11\,741$ |
| 02.9 | Tích $\prod(1-\rho_i)$ + bất đẳng thức trung bình cộng–trung bình nhân; so với Hoeffding $e^{-2m\epsilon^2}$ | — |
| 02.10 | Markov với $\mathbb EV_m\le\epsilon\delta/2$; $\mathbb EV\le\epsilon+\Pr(V>\epsilon)$; phản ví dụ khi không bị chặn ($V_m=m$ với xác suất $1/m$) | Với $\mathbb EV_m\le1/\sqrt m$, $\epsilon=0{,}1$: $m>1/(\epsilon\delta)^2$, $40\,001$ và $10^8+1$ |
| 02.11 | Hoeffding trên $[a,b]$, bán kính $(b-a)r_m$ | $32\ln240/0{,}01=17\,538{,}04\to17\,539$ ($=16\cdot1096{,}13$; $16\cdot1097=17\,552$) |

## 3. Đối chiếu với bản lời giải UML (sau khi tự giải)

| Bài UML | Bản lời giải | Khác biệt và cách xử lý |
|---|---|---|
| 2.3 | Chọn bốn dải có khối lượng đúng $\epsilon/4$; viết xác suất "đúng bằng" $(1-\epsilon/4)^m$; nói $R(S)\subseteq R^\star$ "với mọi $S$"; không xét mẫu không có điểm dương | Khi $D_{\mathcal X}$ có nguyên tử (hoặc $P(R^\star)<\epsilon$) dải khối lượng đúng $\epsilon/4$ có thể không tồn tại. Lời giải của học phần dùng dải đóng $T_i$ (khối lượng $\ge\epsilon/4$, nhờ tính liên tục phải) và dải mở $U_i$ ($\le\epsilon/4$), tách trường hợp $P(R^\star)\le\epsilon$, viết "$\le$". $R(S)\subseteq R^\star$ chỉ hầu chắc chắn. Thêm $h_\varnothing$ vào lớp để thuật toán có đầu ra khi không có điểm dương (QĐ 9). |
| 3.4 | Đếm đúng $3^d+1$, nhưng cận cỡ mẫu viết $\lceil(d\log3+\log(1/\delta))/\epsilon\rceil$, bỏ "$+1$" | Mệnh đề 02.17(c) cho $\ln(3^p+1)$; lời giải của học phần giữ $\ln(3^p+1)$ và chỉ dùng $p\ln3+\ln2$ làm cận trên để nói tăng tuyến tính. Với $p=10$ cả hai đều cho $140$. Ý so sánh với cỡ mẫu bất khả tri (mục tiêu 5) không có trong UML; thêm theo `bien-tap-vong-1.md`. |
| 3.5 | Cùng cách: tích theo tính độc lập, bất đẳng thức trung bình cộng–trung bình nhân, bất đẳng thức hợp | Không khác biệt. Lời giải của học phần dùng phân bố đồng thời $D_i$ trên $\mathcal X\times\mathcal Y$ thay cho $L_{(D,f)}$, thêm (a) $L_{\bar D_m}=\mathbb EL_S$ và (d) so với Định lý 02.7. |
| 4.1 | Chiều "kì vọng $\Rightarrow$ xác suất" chọn $\mathbb E\le\epsilon\delta$ và kết luận "$\le\delta$", trong khi đề cần "$<\delta$"; chiều ngược lại viết $m_{\mathcal H}(\epsilon,\epsilon)$ thay cho $m(\epsilon,\epsilon)$ và lượng hóa "với mọi $D$" | Lời giải của học phần chọn $\mathbb EV_m\le\epsilon\delta/2$ để có dấu chặt; cố định $D$ suốt bài và nói rõ ở (d) đây là khẳng định theo từng phân bố, không phải PAC. |
| 4.2 | Bất đẳng thức Hoeffding tại độ lệch $\epsilon/2$ ghi số mũ $-2m\epsilon^2/(b-a)^2$; đúng phải là $-2m(\epsilon/2)^2/(b-a)^2=-m\epsilon^2/(2(b-a)^2)$ | Công thức cuối của đề UML đúng. Lời giải của học phần suy trực tiếp: bán kính $(b-a)r_m$, điều kiện $2(b-a)r_m\le\epsilon$; không dùng $m^{\mathrm{UC}}_{\mathcal H}$ (QĐ 3). |

Không chép hay diễn lại sát câu chữ của sách hay bản lời giải. Ví dụ kiểm tra của Bài tập 02.8 dùng một mẫu tự dựng, không dùng mẫu minh họa trong đề UML.

## 4. Quyết định thuật ngữ và kí hiệu

- **literal → "tục biến" (literal).** Người viết chọn từ này theo trí nhớ về cách dùng trong tài liệu toán rời rạc tiếng Việt, chưa kiểm tra được nguồn trong workspace (SML không có thuật ngữ này). Giới thiệu lần đầu ở Bài tập 02.8 kèm "(literal)". Đề nghị điều phối viên xác nhận, hoặc đổi sang cách gọi mô tả "biến hoặc phủ định của biến", rồi ghi vào `thuat-ngu.md` §6 (người viết không sửa tệp đó).
- Thuật ngữ mới khác, có tiếng Anh ở lần đầu: hiệp phương sai, không tương quan từng đôi, độc lập từng đôi, hình chữ nhật song song với trục, nguyên tử (atom), hội Boole, hội (conjunction), tần suất thất bại, sai số chuẩn (standard error), bất đẳng thức hợp có trọng số, bất đẳng thức trung bình cộng–trung bình nhân. "Sai số chuẩn", "nguyên tử", "hạt giống (seed)" chưa có trong `thuat-ngu.md`.
- Kí hiệu cục bộ: $r_{m,k}$ (02.6), $T_i$, $U_i$, $c_i$, $P=D_{\mathcal X}$ (02.7), $M_{\mathrm{kt}}$ (02.8), $\rho_i$ (02.9), $V_m$ (02.10), $r'$, $M'$ (02.3). $p$ thay $d$ của UML. Không có chữ tiếng Việt trong công thức.

## 5. Sai khác so với `outline.md` §4

- **02.1** thêm ý (a) dấu bằng Markov; cỡ mẫu ở ý (e) giữ $\epsilon=\delta=0{,}05$ ($2000$/$738$) như outline, khác $\epsilon=0{,}1$ của Ví dụ 02.4.
- **02.2** thêm ý so sánh với đoạn chung ($C\le m(b-a)^2$).
- **02.4** thêm xác suất đuôi chính xác của một giả thuyết ($22/1024$) để thấy cận Hoeffding cho từng giả thuyết vẫn đúng; giá trị $K=88$ chỉ ghi ở "Kiểm tra lại".
- **02.5** outline ghi $R=10\,000$; lời giải chỉ ra ở $m=200$ sai số chuẩn bằng $33\%$ giá trị cần ước lượng và đề nghị $R\ge1{,}12\cdot10^5$.
- **02.6** thêm ý (c): chọn trọng số sau khi xem mẫu (dùng cấu trúc của 02.4), nối mục tiêu 3 với §9 của ghi chú.
- **02.7** ý 3–4 của UML chỉ còn một câu mở rộng trong lời giải (c).
- **02.10** thêm ý (c) cỡ mẫu theo đường Markov ($1/\delta^2$ so với $\ln(1/\delta)$) và ý (d) theo từng phân bố.
- Độ dài: $\approx10\,000$ tiếng theo `wc -w` (khoảng $9\,200$ khi bỏ công thức), vượt mục tiêu $8\,000$–$9\,000$; Bài 01 là $9\,224$ ($8\,509$ khi bỏ công thức). Phần dôi chủ yếu do lời giải từng bước (§7a) và công thức ngắt dòng cho màn hình 390 px.

## 6. Kiểm tra đã chạy

`sync-local-materials.py` và `--check`; `git diff --check`; Playwright 1600×900 và 390×844 (mở mọi `details`): 0 `.katex-error`, 1250 công thức, không lỗi trang, không yêu cầu hỏng, không công thức hiển thị nào tràn khung ở 390 px (33 công thức đã được ngắt dòng), `scrollWidth` 375 ≤ 390. Thông báo CSP về script nội tuyến của trình xem có cả ở Bài 01.

## 7. Vòng sửa (2026-10-30)

Căn cứ: `reviews/9-bai-tap-toan.md`, `reviews/10-bai-tap-su-pham.md`, quyết định `reviews/11-quyet-dinh-bai-tap.md`. Mục 4 ở trên (thuật ngữ "tục biến") được thay bằng B1.

- **B1.** Bỏ mọi "tục biến". Đề 02.8 định nghĩa một lần: $x\mapsto x_j$ là một biến, $x\mapsto\bar x_j$ là phủ định của biến đó, gọi chung là *biến hoặc phủ định của biến* (literal), tập $\mathcal U_p$; sau đó viết $u\in\mathcal U_p$, $L\subseteq\mathcal U_p$, "thuật toán loại dần". Hội của tập rỗng ghi bằng chữ để không trùng kí hiệu $h_\varnothing$ của 02.7.
- **B2.** 02.1(d): thêm $x=e^\tau$, hiệu tích trừ kì vọng của tổng bằng $(x-1)^3/8$, so sánh tại $\tau=1$ ($5{,}7918<6{,}4259$) và $\tau=-1$ ($0{,}3515>0{,}3199$). Ý mới (e): Định lý 02.7(a) còn đúng (chỉ cần "$\le$" với $\tau>0$), Định lý 02.7(b) sai: $m=3$, $\epsilon=\tfrac12$, $\Pr(\bar V_3\le0)=\tfrac14>e^{-1{,}5}\approx0{,}2231$. Ý cỡ mẫu cũ thành (f), kết luận $2000$ / $738$ giữ, lý do dẫn tới (e). Gợi ý 3 sửa theo.
- **B3.** 02.2 thêm (d), gợi ý 3 và lời giải bốn bước: $r^{+}=\sqrt{C\ln(1/\delta)/(2m^2)}\approx0{,}0612$, $r=\sqrt{C\ln(2/\delta)/(2m^2)}\approx0{,}0679$ với $C=2500$; đoạn chung ($C=16\,000$): $0{,}1548$ và $0{,}1718$, gấp $\sqrt{6{,}4}\approx2{,}53$ lần. Dòng Mục tiêu 02.2: "mục tiêu học tập 1, 2"; §10 của ghi chú sửa tương ứng.
- **T1.** 02.10(c) ghi rõ cận Markov của Bước 1 với dấu "$<\delta$"; giữ $40\,001$ và $10^8+1$; thêm câu: cách chọn $\epsilon\delta/2$ cho $m\ge4/(\epsilon\delta)^2$, lớn hơn khoảng $4$ lần.
- **T2.** Bỏ câu "Lập luận này bỏ hệ số $K$…" khỏi đề 02.4.
- **T3.** 02.5(c): "với xác suất ít nhất $\tfrac89$, $\hat p$ nằm trong $p\pm3\sqrt{p(1-p)/R}$"; bỏ "phải gần".
- **T4.** 02.8(d) Bước 4: bỏ "phải"; "độ lệch chuẩn chỉ xuống cỡ $\epsilon$ khi $m$ cỡ $1/\epsilon^2$", tốc độ của cận đủ, dẫn Nhận xét 02.18.
- **T5.** Xóa Bước 3 (mở rộng $\mathbb R^p$) của 02.7(c); không thêm "Câu hỏi:" để giữ độ dài.
- **Nhẹ (rà soát 9).** 02.10(d) dẫn Định nghĩa 01.25 cho trường hợp $\inf L_D>0$; 02.10(c) Bước 3 "chỉ so cách phụ thuộc vào $\delta$"; 02.6 ghi $r_{1000}\approx0{,}0728$ và $r_{10}\approx0{,}728$; 02.8(c) thêm $p\ln3<\ln(3^p+1)$; 02.8(a) "đổi vai trò nếu cần"; 02.5(a) ngưỡng nguyên, nói rõ phụ thuộc độ chính xác (kiểm lại: số thực đơn ghi sai tại $k=32$, $m=100$ và $k=64$, $m=200$; số thực kép đúng ở cả bốn biên); 02.4(c) "cùng bậc độ lớn"; 02.2 Gợi ý 2 nêu cả Bổ đề 02.5(b) và 02.6.
- **Nhẹ (rà soát 10).** "Hệ quả." → "Đếm biến cố." (02.3); $s$, $R(s)$ trong 02.7(a), 02.8(b); văn bản làm chủ ngữ ở 02.1(f), 02.5 đề, 02.10(d) viết lại; "*hạt giống ngẫu nhiên* (random seed)"; AM–GM viết đủ tên tiếng Anh và dùng lại trong lời giải 02.9; "Kiểm tra lại" của 02.2, 02.3, 02.10, 02.11 thành phép kiểm số ($C=m$ cho lại Hệ quả 02.10(c); $2r'\approx0{,}09997$ tại $m=1523$; $m=40\,000$ cho đúng $0{,}05$; $0{,}099997$ tại $17\,539$, $0{,}1000001$ tại $17\,538$); dấu câu gợi ý 02.10; 02.10 "mục tiêu học tập 1, 6" (§10 của ghi chú sửa tương ứng).
- **Cắt độ dài.** Đoạn mở bỏ $\mathbb N$; 02.1(b), (c) gộp bước; 02.2(b) một đoạn, (c) Bước 4 gộp; 02.3(a), (b) Bước 2, (c) gộp; 02.4(c) gộp Bước 2–3, bỏ câu ERM 62%; 02.5(d) bỏ câu Định lý 02.14(b); 02.6(a) gộp bước, (b) gộp ý nghĩa; 02.7(a) một đoạn, bỏ câu lỗi thường gặp; 02.8(b) hai đoạn, (d) Bước 2 rút; 02.9(d) hai đoạn; 02.10 gộp bước; 02.11(b) Bước 4 và (c) gộp.
- **Ghi chú.** §10: hai dòng 02.2, 02.10 như trên; thân bài thành $12\,001$ tiếng, nên bỏ "học tập" trong câu dẫn của §10 ("mỗi dòng ghi mục tiêu mà bài kiểm tra"); thân bài $11\,999$.
- **Độ dài bài tập:** $9\,498$ tiếng (`wc -w`). 02.5(b) bỏ ví dụ "$R=2\cdot10^5$" để bù các công thức ngắt dòng cho 390 px.
- **Sau rà lại (bốn điểm nhẹ).** (1) 02.2(b): khôi phục so sánh tường minh $2m^2\epsilon^2/C\ge2m\epsilon^2/(b-a)^2$, "nên cận ở (a) không lớn hơn cận dùng đoạn chung". (2) §9a: đề 02.1(f) "vẫn được Bổ đề 02.3 hoặc Định lý 02.7 bảo đảm"; 02.8(d) Bước 4 "Nhận xét 02.18 bàn tính cần thiết của tốc độ này." (3) 02.5(b) Bước 3: thêm câu "Chọn chẳng hạn $R=1{,}2\cdot10^5$." sau công thức (công thức hiển thị không đổi). (4) 02.5(a): "số dấu phẩy động độ chính xác đơn (single precision)", câu gộp lại để bù độ dài. Độ dài: $9\,489$ tiếng.
