# Nhật ký rà soát — Bài 03: Chiều VC và hàm phân lớp tuyến tính

Tệp nội bộ. Ghi tác tử, quyết định của điều phối viên, phát hiện rà soát và nguồn đã tham khảo.

Căn cứ bắt đầu (2026-10-31): người dùng giao soạn ghi chú Bài 03 theo blueprint ("xây dựng lecture note 03 của Lý thuyết học thống kê, tuân thủ các nguyên tắc trong CLAUDE.md và nguyên tắc riêng của môn học, theo blue-print đã thiết kế"). Các yêu cầu rút ra từ Bài 01–02 áp dụng ngay từ bản thảo: định nghĩa trước khi dùng (`forward_refs.py` báo 0), khối nhiều thành phần viết thành danh sách có nhãn song song (`van-phong.md` §3a), câu thẳng (§9a), ví dụ từng bước (§7a), thuật toán tất định $A(S)$, công thức không chứa chữ tiếng Việt có dấu trong `\text{}`.

## Tác tử

| Bước | Vai trò | Loại | Mô hình | Mức | Bằng chứng |
|---|---|---|---|---|---|
| 2026-10-31 · 1 | Phân tích nguồn UML (chỉ ghi `source-analysis.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 2 | Lập dàn ý (ghi `outline.md`, chỉ planning) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 3 | Soạn ghi chú (ghi `lecture-note.md`, `img/lec-03/` nếu cần) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 4 | Năm lượt rà độc lập (học viên; chính xác toán học; chuyên gia và trung thành nguồn; học thuật–sư phạm và `no-ai-slop` Detect; mạch và móc nối), chỉ đọc repo, báo cáo ghi vào scratchpad | general-purpose ×5 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 5 | Biên tập vòng 1 (cùng người viết; ghi `lecture-note.md`, `bien-tap-vong-1.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 6 | Rà lại: toán học trên phần đã sửa (người rà 2); mạch, móc nối và văn phong trên phần đã sửa ±2 đoạn và ranh giới mục (người rà 5), chỉ đọc | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 7 | Biên tập vòng 2 (cùng biên tập viên) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 8 | Rà lại kết hợp vòng 2: toán, mạch, văn phong trên diff vòng 2 (người rà 5, chỉ đọc) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 9 | Soạn bài tập (ghi `exercises.md`, `bai-tap-ghi-chu.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 10 | Rà bài tập: toán học; sư phạm và `no-ai-slop` Detect (chỉ đọc, báo cáo ghi vào scratchpad) | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 11 | Sửa bài tập theo hai lượt rà (cùng người soạn; ghi `exercises.md`, hai dòng §10 của ghi chú) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 12 | Rà lại bài tập: toán; sư phạm (cùng hai người rà, chỉ đọc) | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 13 | Sửa mười điểm nhẹ cuối của bài tập (cùng người soạn) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |

## Phân tích nguồn — quyết định của điều phối viên: **chấp nhận** (2026-10-31)

Báo cáo `source-analysis.md` (150 dòng). Điều phối viên tự kiểm lại chuỗi hằng số của định lý hội tụ đều VC: bổ đề mẫu bóng cần $m\epsilon^2\ge2$ (Chebyshev, $\operatorname{Var}\le\tfrac14$: $\tfrac1{m\epsilon^2}\le\tfrac12$); bước đổi chỗ với dấu ngẫu nhiên có số hạng trong $[-1,1]$, Hoeffding cho $2e^{-mt^2/2}$, tại $t=\epsilon/2$ là $2e^{-m\epsilon^2/8}$; tổng $4\Pi_{\mathcal H}(2m)e^{-m\epsilon^2/8}$, nên bán kính $\sqrt{8\ln(4\Pi_{\mathcal H}(2m)/\delta)/m}$ và $m\epsilon^2=8\ln(4\Pi/\delta)\ge8\ln4$ tự thỏa điều kiện; Sauer tại $2m$ và $d\ln(2em/d)\le(1+\ln2)d\ln(em/d)$, $\ln(4/\delta)\le2\ln(2/\delta)$ cho $C=4$. Tính lại bằng Python (scratchpad `m_check03.py`): bán kính trực tiếp / dạng $C=4$ với $\delta=0{,}05$: $d=1$: $0{,}3223/0{,}4308$, $0{,}1106/0{,}1491$; $d=3$: $0{,}4638/0{,}6212$, $0{,}1644/0{,}2228$, $0{,}0571/0{,}0779$; $d=11$: $0{,}7622/1{,}0143$, $0{,}2799/0{,}3787$, $0{,}0993/0{,}1356$ ($m=10^3,10^4,10^5$); cỡ mẫu cho rủi ro vượt mức $0{,}1$: $54\,330$, $132\,992$, $447\,194$ (trực tiếp), $103\,939$, $261\,198$, $889\,572$ ($C=4$); sáu hàm ngưỡng: $0{,}2222$ so với $r_m=0{,}0523$; $\Pi=16=\binom62+1$ cho khoảng đóng trên 5 điểm; $\lceil2\ln(2^{65}/0{,}05)/0{,}01\rceil=9611$; cách dựng $\sin$ với $x_i=2^{-i}$ đúng cho mọi $2^6$ cách gán nhãn. Tất cả khớp.

Quyết định cho dàn ý và bản thảo:

1. **Định lý hội tụ đều VC** (Theorem 3.5) phát biểu với hằng số tường minh: bán kính $\sqrt{8\ln(4\Pi_{\mathcal H}(2m)/\delta)/m}$ với mọi $m\ge1$; khi $1\le d\le m$, $\le\sqrt{8(d\ln(2em/d)+\ln(4/\delta))/m}\le4\sqrt{(d\ln(em/d)+\ln(2/\delta))/m}$; cắt ở $1$ được. Độ sâu [S]: lộ trình năm bước trong thân bài (mẫu bóng; đổi chỗ với dấu ngẫu nhiên; thu về cách gán nhãn trên mẫu gộp $2m$ điểm; Hoeffding và bất đẳng thức hợp; Sauer–Shelah), chi tiết đầy đủ ở Phụ lục. Nói rõ vì sao không lấy hợp trên các cách gán nhãn của $S$ (§2 bước 3 của báo cáo). Không dùng dạng $1/\delta$ của UML Định lý 6.11; không nói UML sai trong ghi chú, chỉ ghi ở "Quan hệ với giáo trình UML" rằng học phần dùng cận xác suất cao qua đối xứng hóa.
2. **Hàm tăng trưởng** lấy cực đại trên bộ $m$ điểm (cho phép lặp), như blueprint; $\Pi_{\mathcal H}(m)=2^m$ khi $m\le d$.
3. **Tính chất hội tụ đều của lớp** ($m^{UC}_{\mathcal H}$) định nghĩa ở Bài 03 từ Định nghĩa 02.13 (lời hứa của Bài 02).
4. **Sauer–Shelah** [S]: quy nạp kép theo $(m,d)$ tách theo điểm cuối (gợi ý của blueprint) trong thân bài ở mức lộ trình; chứng minh đầy đủ ở Phụ lục. Dạng đóng $(em/d)^d$ với $1\le d\le m$ chứng minh đầy đủ (hai dòng); nêu phản ví dụ $m=1$, $d=3$ cho thấy điều kiện $d\le m$ cần.
5. **Nửa không gian**: cận dưới $p+1$ đầy đủ (đỉnh đơn hình, điểm độc lập afin); cận trên qua định lý Radon [S] trong thân bài, Phụ lục chứng minh Radon đầy đủ; xử lý quy ước $\mathbb 1[\langle w,x\rangle+b\ge0]$ đúng (phía nghiêm ngặt trên tập khác rỗng). Nửa không gian thuần nhất: $p$.
6. **Định lý cơ bản** (fundamental theorem): chỉ phát biểu, kèm điều kiện đo được (M) (lớp con đếm được xấp xỉ theo từng điểm), kiểm (M) cho hàm ngưỡng ($t_k\uparrow t$), khoảng, nửa không gian. Hệ quả của nó đóng lời hứa Bài 01: $\mathcal M_{[0,1]}$ không học được PAC với mọi thuật toán (UML Hệ quả 6.4, §5.1). Cận dưới định lượng (lời hứa Nhận xét 02.18) phát biểu không chứng minh, hằng số $c$, $\epsilon_0$, $\delta_0$ để dạng kí hiệu, đúng lượng từ (mọi thuật toán; tồn tại phân bố); phần khả thực với $d\ge2$.
7. **Hệ quả ERM** (Corollary 3.6) với $\inf_{h\in\mathcal H}L_D(h)$ (không giả sử đạt), nêu ERM tồn tại với hàm lỗi 0–1 vì $L_S$ chỉ nhận hữu hạn giá trị.
8. **Trung thực về con số:** cận VC với hằng số này lớn hơn cận lớp hữu hạn sau khi rời rạc hóa ($132\,992$ so với $9611$ cho một ngưỡng 64 bit; $0{,}222$ so với $0{,}052$ cho sáu hàm ngưỡng). Ghi chú nói giá trị của cận VC là áp dụng cho chính lớp vô hạn và đi kèm điều kiện cần (định lý cơ bản), không nói cận VC chặt hơn.
9. **Phản ví dụ bỏ giả thiết** trong ghi chú: (a) $\mathcal M_{[0,1]}$, chiều VC vô hạn, hội tụ đều hỏng với mọi $m$ (nối Mệnh đề 01.15); (b) lớp chọn sau khi xem mẫu, hai hàm, chiều VC $1$, độ lệch $1$ chắc chắn, trong khi cận hứa $\le0{,}322$ ($m=1000$); (c) nhân chứng và chứng minh (một tập bị tách trọn chỉ cho $d\ge k$; một tập không bị tách trọn không chứng minh gì: ba điểm thẳng hàng). Phản ví dụ chép mẫu (bỏ độc lập) chỉ nhắc một câu hoặc để bài tập.
10. **Số tham số và chiều VC:** một tham số, chiều VC vô hạn ($\mathbb 1[\sin(\theta x)>0]$, cách dựng $x_i=2^{-i}$) và nhiều tham số, chiều VC $1$; ghi chú có thể chỉ phát biểu và để chứng minh cho bài tập gốc 5.
11. **Ví dụ xuyên suốt:** hàm ngưỡng trên $\mathbb R$ (sáu hàm ngưỡng của ví dụ sàng lọc là thu hẹp lên $\{1,\dots,5\}$, $\Pi=6$); ứng dụng: hàm phân lớp tuyến tính afin trên $p=10$ đặc trưng ($d=11$). Nếu dùng lại $D_\eta$, điều phối viên sửa dòng tương ứng của `ky-hieu.md`.
12. **Để Bài 04:** không phân tích sai số xấp xỉ/ước lượng, không SRM; chỉ câu cầu nối. Rademacher để Bài 07. Hàm lỗi khác 0–1 và bài toán nhiều lớp nằm ngoài định lý (giới hạn).
13. **Bài tập UML đề xuất** (cho bước bài tập, sau ghi chú): 6.2, 6.4, 6.5, 6.6 (ý 1–3, 5; ý 4 thử thách), 6.10, 9.6; 6.8 tùy chọn; ghi các chỗ hổng của bản lời giải (6.2(b), 6.5, 6.6(b), 6.8, 6.11, 9.6(b)).
14. **Độ dài:** thân bài ≤ 12 000 tiếng (`wc -w`), phụ lục ≤ 3 000 (Radon, Sauer đầy đủ, chứng minh đầy đủ định lý VC, tính đo được).

## Dàn ý — quyết định của điều phối viên: **chấp nhận có sửa** (2026-10-31)

`outline.md` 466 dòng: 19 khối đánh số (03.1–03.19; Mệnh đề 03.5, 03.6, 03.9 = Prop 3.1–3.3; Bổ đề 03.12 = Lemma 3.4; Định lý 03.15 = Theorem 3.5; Hệ quả 03.16 = Corollary 3.6; Định lý 03.17 = định lý cơ bản; Định lý 03.19 = cận dưới), Ví dụ 03.1–03.10, Bài tập 03.1–03.13. Điều phối viên đọc mục 1–3, 4, 6–7 và lướt 8–12; tự kiểm: dạng đóng $m^{UC}_{\mathcal H}\le(16/\epsilon^2)(d\ln(32/\epsilon^2)+\ln(4/\delta))$ (bất đẳng thức tiếp tuyến tại $a=2em/d$, $a_0=4e\kappa$, $\kappa=8/\epsilon^2$: $\kappa d\ln(2em/d)\le m/2+\kappa d\ln(4\kappa)$) và $M(\epsilon,\delta)$ với $\kappa=32/\epsilon^2$ ($6400(\ln12\,800+\ln80)\approx88\,570$ ở $d=1$); $27\,355=\lceil200(193\ln2+\ln20)\rceil$; $\Pi(m)=2m$ của hàm ngưỡng hai phía; bốn khoảng của Mệnh đề 03.6; lời giải câu hỏi cuối buổi (hình chữ nhật, năm điểm). Đúng. Các số hiệu Bài 01–02 dẫn trong dàn ý (Nhận xét 01.17, 01.26, 01.30, …) có trong ghi chú.

Quyết định về các điểm mở của dàn ý (mục 12):

1. **Ghép cặp ở Ví dụ 03.10:** chấp nhận ghép theo cùng lớp ($54\,330$/$9611$, $132\,992$/$27\,355$, $447\,194$/$98\,333$); QĐ 8 ghép nhầm hai lớp khác nhau.
2. **Bán kính VC** viết $\rho_m$ (đã thêm vào `ky-hieu.md`).
3. **Định nghĩa 03.14** không giới hạn ở lớp thỏa (M): yêu cầu "biến cố $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\le\epsilon$ đo được và có xác suất ít nhất $1-\delta$". Khi đó Ví dụ 03.6 nằm trong định nghĩa: dưới $D$ đã chọn, biến cố là tập rỗng (đo được, xác suất $0$), nên lớp không có tính chất hội tụ đều. Một câu: (M) bảo đảm biến cố đo được với mọi $D$.
4. **Véc-tơ đơn vị** $\mathbf e_i$: chấp nhận.
5. **Chỉ số tên lớp:** dùng chữ viết tắt tiếng Anh như Bài 01–02 ($\mathcal H_{\mathrm{poly}}$, $\mathcal H_{\mathrm{rec}}$, $\mathcal H_{\mathrm{conj}}$): $\mathcal H_{\mathrm{thr}}$ (hàm ngưỡng), $\mathcal H_{\mathrm{int}}$ (khoảng), $\mathcal H^p_{\mathrm{aff}}$ (nửa không gian afin), $\mathcal H^p_{\mathrm{hom}}$ (nửa không gian thuần nhất). Thay ở mọi chỗ của dàn ý khi viết.
6. **Bài tập 03.13** (UML 6.8): bỏ, vì Bài tập 03.5(a) đã dựng lớp $\sin$.
7. **Câu hỏi cuối buổi trùng Bài tập 03.9 ở $p=2$:** chấp nhận; người viết bài tập nói rõ câu hỏi cuối buổi là trường hợp $p=2$.
8. **"Tách trọn", "mẫu bóng"** chốt; đã thêm 20 thuật ngữ của dàn ý mục 9 vào `thuat-ngu.md` §7.
9. **Tên Định lý 03.17:** "Định lý cơ bản của học PAC cho phân lớp nhị phân".
10. **Nhãn độ sâu Hệ quả 03.18:** "chứng minh đầy đủ (dựa trên Định lý 03.17(a))"; câu đầu của chứng minh nói rõ Định lý 03.17(a) được thừa nhận.
11. **`ky-hieu.md`:** đã thêm $\mathcal H_C$, $\operatorname{VCdim}$, $m^{UC}_{\mathcal H}$, $\rho_m$, $S'$, $\sigma_i$, $\mathbf e_i$, (T5), (M); ghi chú cho $\Pi_{\mathcal H}$ (bộ điểm).
12. **(T5)** là nhãn mới; chấp nhận.

Thêm cho người viết: Định lý 03.17(a) dẫn Nhận xét 01.30 (định lý không có bữa trưa miễn phí, Bài 01); Nhận xét 03.4 chỉ dẫn "§5" cho ba điểm thẳng hàng (dẫn mục, không dẫn khối có số, `forward_refs.py` phải báo 0); bảng của Ví dụ 03.5 phải đọc được ở 390 px (tách thành hai bảng hoặc bỏ cột theo thứ tự cắt (1)). Ngân sách: thân bài ≤ 12 000 tiếng, phụ lục ≤ 3 000.

## Bản thảo ghi chú — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-31)

Bản thảo 1123 dòng; thân bài 11 996 tiếng (`wc -w`, trần 12 000), phụ lục 2085 (trần 3 000). 19 khối 03.1–03.19, Ví dụ 03.1–03.10, một khối ứng dụng, §10 liệt kê Bài tập 03.1–03.12. Kiểm tra do điều phối viên chạy: `forward_refs.py` 0; `sync --check` OK; cấu trúc khối đúng dàn ý. Điều phối viên đọc phần mở đầu đến §4 và toàn bộ §7 đến hết lộ trình chứng minh Định lý 03.15: khớp dàn ý và các quyết định; chuỗi hằng số (Chebyshev $1/(m\epsilon^2)\le\tfrac12$; Hoeffding miền dài $2$; $m\rho_m^2\ge8\ln4$) đúng. Người viết báo kiểm tra Playwright: 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng ở 1600 và 390 px, không công thức tràn sau khi ngắt dòng.

Chấp nhận các sai khác người viết báo: áp dụng cả bảy mục của thứ tự cắt (thân bài đã lên 12 262 tiếng; mất Bước 5 của Ví dụ 03.9, bước $q=3$ của Ví dụ 03.10, câu $d\ge2$ của Định lý 03.19, cột $m=8,10$); bảng Ví dụ 03.5 chuyển vị thành hai bảng bốn cột; câu tỉ số $1{,}55$–$1{,}63$ đặt ở Ví dụ 03.9 (tránh dẫn tới trước); Phụ lục B quy nạp trên họ $Y\subseteq\{0,1\}^n$; Định lý 03.17(b) thêm giả thiết có ít nhất một thuật toán ERM đo được; (M) chỉ khẳng định cho nửa không gian afin. Kí hiệu $E_m(D,\epsilon)$ cục bộ trong Định nghĩa 03.14 và Ví dụ 03.6: chấp nhận. Bản đóng băng cho rà soát: scratchpad `lec03-draft-frozen.md`.

## Năm lượt rà — quyết định của điều phối viên: **yêu cầu sửa** (2026-10-31)

Báo cáo trong `reviews/1-hoc-vien.md` (0/0/8/21), `2-toan-hoc.md` (0/0/1/12; tự chứng minh lại mọi kết quả, 126 con số đúng), `3-chuyen-gia-nguon.md` (0/1/5/9), `4-hoc-thuat-van-phong.md` (0/1/15/18), `5-mach.md` (0/1/8/14). Không có lỗi chặn bàn giao, không có lỗi toán. Ba phát hiện nghiêm trọng sau khi gộp: bảng §1 dùng kí hiệu trước định nghĩa (R5); chữ "chiều" hai nghĩa (R4); nguồn của cận dưới, UML §28.3 là cận trên khả thực (R3, R2, R5). Điều phối viên đối chiếu từng mục nghiêm trọng và trung bình với bản đóng băng và kiểm $M(\epsilon,\delta)$ của Hệ quả 03.16(c) bằng dạng đóng của Định lý 03.15(c) tại $\epsilon/2$. **Quyết định:** `reviews/0-quyet-dinh.md` (N1–N3, M1–M15, cắt, nhẹ; bác bỏ đề xuất bỏ dạng câu hỏi thẳng ở câu hỏi mở đầu vì `CLAUDE.md` của học phần yêu cầu dạng đó; hoãn hình SVG; ba điểm chuyển sang bước bài tập). Điều phối viên đã sửa `outline.md` §7 (§28.2/§28.3), thêm "bán kính VC" vào `thuat-ngu.md` §7. Hai bài gốc đổi biến thể so với blueprint (Bài tập 03.3: ghi chú đã làm đỉnh đơn hình nên bài hỏi điểm độc lập afin bất kì; Bài tập 03.6: Phụ lục A, B đã có cả hai chứng minh mà blueprint cho chọn, nên bài hỏi chứng minh khác của Sauer–Shelah) có lý do ở `outline.md` §4: chấp nhận. Giao người viết làm biên tập viên (tiếp tục bằng `SendMessage`).

## Biên tập vòng 1 — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-31)

Biên tập viên áp dụng đủ N1–N3, M1–M15 (danh sách ở `bien-tap-vong-1.md`). Thân bài 11 999 tiếng, phụ lục 2107. Đánh số đổi do thứ tự mới của §7 (M3): Định nghĩa 03.14 cũ → 03.13, Nhận xét 03.13 cũ → 03.14; các số khác và số bài tập giữ nguyên. Cắt thêm (không bỏ toán): danh sách mười bốn cách gán nhãn ở Ví dụ 03.3, phép đếm ở Nhận xét 03.10(iii) (dẫn Mệnh đề 03.9(b)), Bước 5 của Ví dụ 03.10 gộp vào kết luận, gạch "Tính đo được" trong danh sách quan hệ với UML, câu đo được của ERM lặp. Chấp nhận ba điểm áp dụng một phần (dòng $\epsilon$ ở bảng §2 viết "các phát biểu khả thực ở §8" để tránh dẫn tới trước; câu trước Bổ đề 03.8 không dẫn Ví dụ 03.3; bỏ "ba điểm thẳng hàng ở §5" khỏi Nhận xét 03.4) và việc giữ nhãn độ sâu Hệ quả 03.18 theo quyết định dàn ý 10. Điều phối viên chạy lại: `forward_refs.py` 0; `sync --check` OK; `wc -w` 11 999; đọc bảng §1, câu mở §7, câu nguồn sau Định lý 03.19, §9, cầu nối §11: đúng quyết định. Hai con số mới $\ln480\approx6{,}174$, $\ln240\approx5{,}481$ đúng. Diff vòng 1: scratchpad `lec03-round1.diff`. Người viết báo Playwright: 0 `.katex-error`, 0 lỗi, không tràn ở 1600 và 390 px. Chuyển hai lượt rà lại.

## Rà lại sau vòng 1 — quyết định của điều phối viên: **yêu cầu sửa nhỏ** (2026-10-31)

Rà lại toán (`reviews/6-ra-lai-toan.md`): 13/13 phát hiện của rà soát 2 đã xử lý; không lỗi toán mới; 16 con số mới hoặc dời chỗ đúng; một trung bình (đoạn "Khi $d=\infty$ … Khi $d=0$ …" chép đôi ở dòng 574/576, do biên tập), ba nhẹ (cầu nối gán $0{,}164\to0{,}280$ cho rủi ro vượt mức trong khi cận là $2\rho_m$: $0{,}329\to0{,}560$; lý do dấu đạo hàm ở Ví dụ 03.9; Định lý 03.19(b) cỡ $(d+\ln(1/\delta))/\epsilon$). Rà lại mạch và văn phong (`reviews/7-ra-lai-mach.md`): N1–N3, M1–M4, M6–M8, M10–M15 đủ; M5, M9 một phần; một nghiêm trọng (cùng đoạn chép đôi), một trung bình (§9 "Mỗi giả thiết của Định lý 03.15 đều được dùng" sai: $d<\infty$ không là giả thiết của 03.15(a); câu về (M) lặp dòng 823), tám nhẹ. Điều phối viên xác nhận dòng 574 và 576 trùng nhau và tính lại $2\cdot0{,}1644=0{,}329$, $2\cdot0{,}2799=0{,}560$. **Quyết định:** chấp nhận mọi phát hiện của hai báo cáo; giao biên tập viên vòng 2; sau đó một lượt rà lại kết hợp trên diff vòng 2.

## Biên tập vòng 2 và rà lại kết hợp — quyết định của điều phối viên: **chấp nhận** (2026-10-31)

Biên tập vòng 2 áp dụng đủ 14 phát hiện của `reviews/6-ra-lai-toan.md` và `7-ra-lai-mach.md` (danh sách ở mục "Vòng 2" của `bien-tap-vong-1.md`); xóa đoạn chép đôi; thân bài 11 981 tiếng, phụ lục 2104; không đổi số hiệu. Điều phối viên đọc toàn bộ diff vòng 2 (`lec03-round2.diff`, 109 dòng): đúng từng đề xuất; kiểm đạo hàm ở Ví dụ 03.9, $\big(d-d\ln\tfrac{2em}d-c\big)/m^2<0$ vì $\ln(2e)>1$. Rà lại kết hợp (`reviews/8-ra-lai-vong-2.md`): mọi phát hiện của rà soát 6, 7 ✓; 0/0/0/1; **giao được**; con số cầu nối $0{,}164430$, $0{,}279919$, gấp đôi $0{,}3289$, $0{,}5598$. **Bác bỏ** điểm nhẹ đổi $0{,}329$ thành "khoảng $0{,}33$": $0{,}329=2\cdot0{,}16443$ đúng khi làm tròn từ giá trị chưa làm tròn. Ghi nhận: mục "Con số mới" của biên tập viên ghi $0{,}27986$, giá trị đúng $0{,}279919$ (số in trong ghi chú đúng).

## Kiểm định cuối và công bố ghi chú — Bài 03 (2026-10-31)

Kiểm định do điều phối viên chạy (Playwright, Chromium, scratchpad `final03.py`): qua HTTP (máy chủ xem trước của repo, cổng 8766) và `file://`, ở 1600×900 và 390×844, mở hết 13 khối thu gọn: 1574 công thức, 0 `.katex-error`, 0 cảnh báo KaTeX, 0 công thức hay bảng tràn khung, 0 lỗi trang, 0 yêu cầu hỏng, không khối `:::` hay `$$` chưa hiển thị, trang rộng 375 px ở 390 px (không cuộn ngang). In PDF A4: 46 trang. Điều phối viên xem ảnh chụp phần đầu ở 390 px và 1600 px, hai đoạn của §6–§7 ở 390 px, trang 21 của bản in: hiển thị đúng. Quan sát ngoài phạm vi: trình xem cho phép ngắt dòng giữa công thức nội dòng và dấu chấm ngay sau nó (một dấu chấm đứng riêng một dòng ở vài chỗ); đây là hành vi chung của trình xem, không do ghi chú; báo người dùng. `sync --check` OK; `forward_refs.py` 0; `git diff --check` sạch. Thẻ Bài 03 của `2627-1/index.html`: tên và mô tả theo thuật ngữ đã chốt ("hàm phân lớp tuyến tính", "tách trọn", "afin"), liên kết ghi chú; "Bài tập" vẫn "Chưa có" (soạn sau khi ghi chú qua rà soát). Bấm từ trang chỉ mục mở đúng ghi chú qua HTTP và `file://`, 0 lỗi.

**Trạng thái:** ghi chú Bài 03 hoàn tất; commit và push. Việc tiếp theo: bài tập (`exercises.md`) theo `outline.md` §4 và ghi chú trạng thái cuối.

## Nguồn đã tham khảo

UML (trang PDF): 61–64 (§5.1), 67–82 (§6.1–6.8 và bài tập), 118–122 (§9.1), 128–129 (§9.6), 378, 380 (chỉ để đọc §28.1), 392–401 (§28.1–28.3), 419–421 (Phụ lục A, bổ đề A.1–A.6). Bản lời giải: tr. 11–20, 28, chỉ để đánh giá độ khó và chỗ hổng của bài tập đề xuất.

## Bài tập — bắt đầu (2026-10-31)

Định nghĩa "Done means" của `CLAUDE.md` học phần đòi cả bài tập đã qua rà soát; tiếp tục bước 7–8 của `course-plan.md` §5 sau khi ghi chú được công bố. Giao một người viết soạn `exercises.md` theo `outline.md` §4 (đã sửa theo quyết định dàn ý 5–7: bỏ 03.13, tên lớp tiếng Anh, câu hỏi cuối buổi là trường hợp $p=2$ của 03.9) và ghi chú trạng thái cuối trong `outline.md`; lời giải theo §7a; bài UML tự giải trước rồi mới đối chiếu bản lời giải (chỗ hổng đã biết ở `source-analysis.md` §7). Sau đó hai lượt rà độc lập (toán; sư phạm–văn phong).

## Bài tập — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-31)

`exercises.md`: 12 bài (03.1–03.6 gốc; 03.7–03.12 là UML 6.2, 6.4, 6.5, 6.6, 6.10, 9.6, số bài đã đối chiếu PDF), 9873 tiếng (đích ≤ 10 000), 48 khối gợi ý/lời giải. Người viết tự giải trước rồi mới đối chiếu bản lời giải; ghi trong `bai-tap-ghi-chu.md` các chỗ hổng ở 6.2(b), 6.4, 6.5, 6.6(b)(c)(d), 6.10, 9.6(a)(b) — trong đó 6.6(c) (cách dựng của bản lời giải cho giá trị $0$ tại mọi $\mathbf e_i$ khi $\lvert J\rvert\ge2$) chưa có trong `source-analysis.md` §7. Điều phối viên tính lại: dạng đóng $M$ tại $\epsilon=0{,}05$, $d=3$: $25\,600(3\ln51\,200+\ln80)\approx944\,960$; $\theta=5\pi$ cho $(1,0,1)$ trên $(\tfrac12,\tfrac14,\tfrac18)$: $\sin(5\pi/2)>0$, $\sin(5\pi/4)<0$, $\sin(5\pi/8)>0$: đúng. **Quyết định:** chấp nhận Bài tập 03.6 chứng minh bằng phép dồn (tránh trùng 03.8(a)); 03.4(a) dùng $\epsilon=0{,}05$; đọc lượng từ ở 03.11 "với mọi $m$ tồn tại $D$" đúng; thêm "phép dồn", "nguyên lý chuồng bồ câu" vào `thuat-ngu.md` §7. Hai dòng §10 của ghi chú (03.4, 03.5) đổi tên theo bài tập: thực hiện ở vòng sửa bài tập. Bản đóng băng: scratchpad `lec03-ex-frozen.md`. Chuyển hai lượt rà.

## Rà bài tập — quyết định của điều phối viên: **yêu cầu sửa** (2026-10-31)

Rà toán (`reviews/9-bai-tap-toan.md`): không lỗi chặn bàn giao hay nghiêm trọng; cả 12 lời giải đúng; khoảng 130 con số và khẳng định, 42 phép kiểm vét cạn; không chép bản lời giải; một trung bình (Gợi ý 1 của 03.9 "khi và chỉ khi" sai), mười một nhẹ. Rà sư phạm (`reviews/10-bai-tap-su-pham.md`): hai nghiêm trọng ("chặt" hai nghĩa ở 03.8; "theo cả hai chiều" ở 03.5(c)), sáu trung bình (tiêu đề §10; mục tiêu 3 một phần; vai của $\epsilon$ ở 03.4; 03.4(a) cần máy tính; trùng Nhận xét 03.10(iii); §7a ở 17 chỗ), mười bốn nhẹ. Điều phối viên kiểm phản ví dụ của 03.9. **Quyết định:** `reviews/11-quyet-dinh-bai-tap.md` (B1–B2, T1–T7, mọi điểm nhẹ; đích ≤ 10 000 tiếng). Giao người soạn sửa, gồm hai dòng §10 của ghi chú (03.4, 03.5).

## Sửa bài tập — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-31)

Người soạn áp dụng B1–B2, T1–T7 và mọi điểm nhẹ (`bai-tap-ghi-chu.md` §7); `exercises.md` 9997 tiếng, 12 bài, 35 gợi ý; cắt đủ sáu chỗ của quyết định và khoảng mười câu; 03.5 còn ba ý ((a) lớp $\sin$, (b) số tham số dẫn Nhận xét 03.10(iii), (c) lớp chọn sau khi xem mẫu); 03.4(f) mới đo mục tiêu 3; 03.11(c) yêu cầu phát biểu Định lý 03.17(b). Ghi chú: chỉ hai dòng §10 (03.4, 03.5) đổi, thân bài 11 990 tiếng, `forward_refs.py` 0. Điều phối viên kiểm: ánh xạ giả thiết của 03.4(f) khớp dòng kết Phụ lục C của ghi chú ("(M) ở C.1 và C.7": phần (c) cần biến cố của Định nghĩa 03.13 đo được); con số mới $36{,}912511=3\cdot10{,}843495+4{,}382027$. Diff: scratchpad `lec03-ex-round1.diff`. Gửi lại hai người rà.

## Rà lại bài tập — quyết định của điều phối viên: **chấp nhận, sửa nhẹ** (2026-10-31)

Rà lại toán (`reviews/12-ra-lai-bai-tap-toan.md`): 12/12 phát hiện trước ✓; mọi nội dung mới đúng (giá trị biên tại $m$, $m-1$; $36{,}912511$, $123{,}660470$; $944\,961$, $3\,165\,709$; ánh xạ giả thiết của 03.4(f); 03.11(c)); ba nhẹ (03.4(f) dẫn "Phần (d)" thay vì Bài tập 03.5(c); 03.11(c) Bước 4 gộp hai phép kéo theo; 03.2(a) chưa nêu khác biệt ở cận dưới với khoảng mở). Rà lại sư phạm (`reviews/13-ra-lai-bai-tap-su-pham.md`): B1–B2, T1–T7 ✓; 21/22 phát hiện trước ✓; đủ năm mục tiêu; tiêu đề khớp §10; bảy nhẹ (N1–N7). Cả hai: giao được. **Quyết định:** chấp nhận mười điểm nhẹ, giao người soạn sửa, giữ ≤ 10 000 tiếng; không rà lại thêm (sửa câu chữ và dẫn chiếu, không đổi toán), điều phối viên đọc diff.

## Kiểm định cuối và công bố bài tập — Bài 03 (2026-10-31)

Người soạn sửa mười điểm nhẹ cuối (03.4(f) dẫn Bài tập 03.5(c); 03.11(c) Bước 4 tách hai phép kéo theo; 03.2(a) nêu hai khác biệt với Mệnh đề 03.6; N1–N7); điều phối viên đọc diff (`lec03-ex-round2.diff`, 116 dòng): đúng từng điểm, không đổi con số. `exercises.md` 9993 tiếng (đích ≤ 10 000). Kiểm định do điều phối viên chạy (Playwright, Chromium, `final03.py`), qua HTTP và `file://`, 1600×900 và 390×844, mở hết 47 khối gợi ý/lời giải: 1481 công thức, 0 `.katex-error`, 0 cảnh báo KaTeX, 0 công thức hay bảng tràn, 0 lỗi trang, 0 yêu cầu hỏng, trang rộng 375 px ở 390 px; in PDF A4 37 trang; điều phối viên xem ảnh chụp phần đầu ở 1600 px và lời giải 03.4 ở 390 px. Ghi chú sau khi đổi hai dòng §10: 1575 công thức, 0 lỗi, không tràn ở cả hai cỡ, HTTP và `file://`; thân bài 11 990 tiếng; `forward_refs.py` 0. `sync --check` OK; `git diff --check` sạch. Thẻ Bài 03 của `2627-1/index.html` liên kết bài tập.

**Trạng thái:** Bài 03 (ghi chú và bài tập) hoàn tất; commit và push. Điều kiện "Done means" của học phần thỏa: mọi phát hiện chặn bàn giao và nghiêm trọng đã xử lý và ghi lại; `outline.md` và nhật ký khớp ghi chú; trình xem hiển thị ghi chú và bài tập qua HTTP và `file://` ở hai cỡ và bản in; `material-local-data.js` đồng bộ; thẻ chỉ mục liên kết cả hai sau khi qua rà soát.

## Sửa ghi chú theo văn phong tác giả (sau bản sửa tay Bài 01, Bài 02) — Bài 03 (2026-11-01)

**Ngoại lệ quy trình do người dùng quyết định (2026-11-01):** người dùng yêu cầu dùng công cụ OpenRouter MCP với DeepSeek Flash làm điều phối viên và worker, thay cho tác tử con Claude Opus (ghi đè quy định "OpenRouter không thay tác tử con Claude" của `../CLAUDE.md`), như ở Bài 02. Phiên Claude (Opus 5.5) chỉ khởi chạy các lượt gọi, chuyển kết quả giữa các vai và kiểm cuối.

| Vai | Công cụ | Model (theo metadata cầu nối) |
|---|---|---|
| Điều phối viên DeepSeek: kế hoạch, duyệt từng phần, duyệt cuối | `openrouter-mcp-reviewer` (hồ sơ `plan`, `review`) | `deepseek/deepseek-v4-flash-0731` |
| Người biên tập (no-ai-slop Edit) | `openrouter-mcp-writer` (hồ sơ `patch`) | `deepseek/deepseek-v4-flash-0731` |
| Phản biện độc lập (no-ai-slop Detect) | `openrouter-mcp-reviewer` (hồ sơ `review`) | `deepseek/deepseek-v4-flash-0731` |

Đầu vào chuẩn: mục "The author's voice" của `../CLAUDE.md`, `planning/lec-01/van-phong-tac-gia.md` (§5, §6a, §6b, §7), quy tắc từ bản sửa tay Bài 02 (giả thiết tập trung ở §2 dạng danh sách có công thức, (T3) là hàm lỗi trong $[0,1]$, mục tiêu thành danh sách công thức, công thức hiển thị ngay sau tên, $\sup$ thay $\max$, "tăng nghiêm ngặt"), bản Bài 01, Bài 02 đã sửa. Kế hoạch, báo cáo, phán quyết, metadata: `planning/lec-03/deepseek/` (`master-plan.md`, `<phần>-<vòng>-{writer,review,verdict}.md`, `fix{1,2}-writer.md`, `final-{review,verdict}.md`, `calls.jsonl`). Tám phần (mở đầu–§3, §4, §5, §6, §7, §8, §9–§12, Phụ lục).

Nội dung đã sửa: "khả thực/bất khả tri" → "khả diễn/bất khả diễn"; "mẫu" → "tập huấn luyện" khi chỉ dữ liệu huấn luyện (kể cả nhãn "**Mẫu.**" ở §1 và khối Giả thiết của Định lý 03.15, Hệ quả 03.16, Định lý 03.17); "hàm chỉ thị" → "hàm chỉ báo"; "trước mẫu" → "trước khi lấy mẫu"; nhãn "**Kết luận.**" → "Tóm lại,"; bỏ chỉ dẫn điều hướng ("(§5)", "ở §8", "(Bài tập 03.x)", "(Phụ lục D)", "Bài 04 …", "chuẩn bị Bài 07"); §1 mục 6 thành danh sách công thức, mục 7 công thức hiển thị; §2 nêu tập trung (T1), (T2), (T3), (T5), (M), (O1), (O2) và giả thiết khả diễn, §7 chỉ tham chiếu (T5), (M); câu mở đầu thành câu khẳng định; một "**Câu hỏi.**" ở §7.

Kiểm của phiên Claude (điều phối cuối) và các lượt sửa:

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa | quyết định |
|---|---|---|---|---|---|
| nghiêm trọng | §2, §7 | quy tắc Bài 02 "giả thiết tập trung ở §2" chưa được áp dụng: (T5), (M) vẫn định nghĩa ở §7; §2 chỉ còn câu "… được dùng" | diff sau tám phần | danh sách giả thiết ở §2, §7 chỉ tham chiếu | đã sửa (DeepSeek writer, `fix1-writer.md`) |
| trung bình | Mệnh đề 03.9 Bước 4; Bổ đề 03.12 | mất dẫn chiếu tới Phụ lục A/B, nơi duy nhất có chứng minh đầy đủ; "được bỏ qua trong phác thảo này" sai vì Phụ lục B xử lí | diff | khôi phục "được chứng minh ở Phụ lục A", "được xử lí ở Phụ lục B" | đã sửa (`fix1`; trùng yêu cầu của điều phối viên DeepSeek `s5-2-verdict.md`) |
| trung bình | §8, trước Định lý 03.19 | "Trả lời câu hỏi tốc độ … có cần thiết không cần một cận dưới" mơ hồ ngữ pháp | diff | "Để biết tốc độ … có cần thiết hay không, ta cần …" | đã sửa (`fix1`) |
| trung bình | §1 mục 6 | danh sách con ở cột 0 làm vỡ danh sách đánh số | `s6-2-verdict.md` | thụt lề | đã sửa (`fix1`) |
| nhẹ | §6 | "Trên mọi bộ điểm, …; số bên trái là ngẫu nhiên" mâu thuẫn | `s6-2-verdict.md` | "Trên mọi tập huấn luyện" | đã sửa (`fix1`) |
| nhẹ | Phụ lục C, Bước C.1 | dẫn "đoạn sau (M) ở §7" không còn đúng sau khi (M) lên §2; "cặp tập huấn luyện" sai vì $S'$ là mẫu bóng | diff | "Theo đoạn "Dưới (M), …" ở §7, với mọi cặp mẫu $(S,S')$" | đã sửa (`fix1` + thay thế cơ học của phiên Claude) |
| nhẹ | §2, giả thiết khả diễn | chú thích phạm vi "(dùng ở các phát biểu khả diễn)"; chưa nối với Định nghĩa 01.16 | `final-verdict.md` | bỏ chú thích; "Phân bố $D$ khả diễn đối với $\mathcal H$ (Định nghĩa 01.16): …" | đã sửa (`fix2-writer.md`) |
| nhẹ | Phụ lục C | "tự thỏa" → "được thỏa" làm mất nghĩa | `final-review.md` | khôi phục | đã sửa (`fix2`) |
| — | `s6-2-review`, `s8-1-review`, `s9-12-2-writer` | ba lượt gọi lỗi phía nhà cung cấp (rc 1) | `calls.jsonl` | phản biện toàn bài sau sửa (`final-review.md`) phủ §8 | đã làm; phán quyết cuối chỉ còn hai điểm nhẹ ở trên |

Phán quyết điều phối viên DeepSeek: các phần mở đầu, §4, §8, §9–§12, Phụ lục chấp nhận; §5, §6, §7 yêu cầu sửa ở vòng 2, gom vào `fix1`; duyệt cuối yêu cầu sửa một điểm nhẹ, gom vào `fix2`. Phiên Claude đọc toàn bộ word diff: mọi khối đánh số (86 dòng `:::` như HEAD), con số, công thức còn nguyên; không thêm khẳng định mới; nhãn "**Lộ trình.**" giữ nguyên. Kiểm định: `forward_refs.py` 0; `sync-local-materials.py --check` OK; `git diff --check` sạch; 0 ký tự thay thế/Cyrillic/CJK. Playwright (Chromium), HTTP và `file://`, 1600×900 và 390×844: 1590 công thức, 0 `.katex-error`, 0 công thức tràn, 0 lỗi console/trang, 0 yêu cầu hỏng, rộng 375 px ở 390 px; in PDF chạy được; ảnh chụp §2 ở 390 px đã xem.

**Quyết định:** chấp nhận ghi chú Bài 03 sau sửa; commit và push. Bài tập sửa ở lượt sau.

## Sửa bài tập theo văn phong tác giả, khớp ghi chú đã sửa — Bài 03 (2026-11-02)

Cùng ngoại lệ quy trình như mục trên (người dùng yêu cầu DeepSeek Flash qua OpenRouter MCP làm điều phối viên và worker). Mọi lượt gọi thành công: `deepseek/deepseek-v4-flash-0731` (metadata cầu nối, `planning/lec-03/deepseek-bai-tap/calls.jsonl`); điều phối viên DeepSeek lập kế hoạch (`master-plan.md`), writer (`openrouter-mcp-writer`, hồ sơ `patch`), phản biện và phán quyết (`openrouter-mcp-reviewer`). Bảy phần: 03.1, 03.2–03.3, 03.4, 03.5–03.6, 03.7–03.8, 03.9–03.10, 03.11–03.12.

**Lượt 1 (lưu ở `deepseek-bai-tap/lan-1/`), bị loại một phần:** lượt lập kế hoạch và nhiều lượt phản biện vượt giới hạn tool-call (20/10 vòng), nên writer làm không có kế hoạch riêng; writer phần 03.1 (vòng 2) sửa cả `lecture-note.md` đã duyệt (đổi "thu hẹp" → "hạn chế", "tách trọn" → "tách trọn vẹn", "mẫu bóng" → "mẫu ảo", viết lại câu hỏi mở đầu, bỏ số $54\,330$). Phiên Claude hoàn tác toàn bộ thay đổi ở ghi chú (`git checkout`); giữ các thay đổi ở bài tập (đã đọc diff: chỉ thuật ngữ và chính tả).

**Lượt 2:** giới hạn 40 vòng cho kế hoạch, 30 vòng cho phản biện; COMMON ghi rõ ghi chú chỉ đọc và bài tập theo thuật ngữ của ghi chú; sau mỗi lượt writer, kịch bản tự hoàn tác mọi thay đổi ngoài `exercises.md` (không lần nào phải hoàn tác). Kế hoạch của điều phối viên: chỉ một dẫn chiếu sai (Gợi ý 2 của 03.4 "đứng trước (T5) ở §7", nay (T5) ở §2) và các câu điều hướng. Phần 03.5–03.6 chấp nhận; 03.7–03.8 yêu cầu sửa ba chỗ "mẫu" → "tập huấn luyện" ở 03.11; các phần còn lại writer không đổi gì thêm (đã sửa ở lượt 1). Hai yêu cầu còn mở được gom vào `fixex1-writer.md`.

Nội dung đã sửa: "khả thực/bất khả tri" → "khả diễn/bất khả diễn"; "véc-tơ chỉ thị" → "véc-tơ chỉ báo"; "mẫu" → "tập huấn luyện" khi chỉ dữ liệu huấn luyện (03.4(d), 03.11); bỏ "đứng trước (T5)" ở Gợi ý 2 của 03.4, "đoạn sau Định lý 03.15" ở 03.5, câu "Bài tập 03.8(a) chứng minh …" ở 03.6; "kiểm" → "kiểm tra"; đánh số liên tục Bước 5–7 ở 03.7(b). Giữ hai dẫn chiếu "câu hỏi cuối buổi" (đầu tệp và 03.9): lời giải câu hỏi đó nằm ở ghi chú, Bước 6 của 03.9 dùng nó.

Phán quyết cuối của điều phối viên DeepSeek (`final-verdict.md`, sau `final-review.md` toàn tệp): **chấp nhận**, không phát hiện cần sửa.

Kiểm của phiên Claude: đọc toàn bộ word diff; mọi con số, công thức, khối và dẫn chiếu tới ghi chú còn đúng; 118 dòng `:::` như HEAD; không còn thuật ngữ cũ; 0 ký tự thay thế/Cyrillic/CJK; `lecture-note.md` không đổi so với `7b1bc10`. `sync-local-materials.py --check` OK; `git diff --check` sạch. Playwright (Chromium), HTTP và `file://`, 1600×900 và 390×844: 1481 công thức, 0 `.katex-error`, 0 công thức tràn, 0 lỗi console/trang, 0 yêu cầu hỏng, rộng 375 px ở 390 px; in PDF chạy được; ảnh chụp 390 px đã xem.

**Quyết định:** chấp nhận bài tập Bài 03 sau sửa; commit và push.

## Kiểm tuân thủ nguyên tắc ghi chú mới — quyết định của điều phối viên: **chưa tuân thủ đầy đủ** (2026-11-13)

Yêu cầu của người dùng (2026-11-13): kiểm ghi chú Bài 01–10 theo các nguyên tắc ghi chú hiện hành và ghi bảng phát hiện đầy đủ vào nhật ký từng bài. Chỉ kiểm, chưa sửa ghi chú.

**Tác tử:** người kiểm tuân thủ (chỉ đọc, ghi một tệp báo cáo), `general-purpose`, mô hình `opus` (Claude Opus 5.5), effort `high` (theo lệnh gọi Agent); mười tác tử độc lập, mỗi tác tử một bài, chạy song song. Báo cáo gốc: `planning/lec-03/reviews/kiem-nguyen-tac-2026-11-13.md`.

**Bản được kiểm:** `materials/lec-03/lecture-note.md`, HEAD `25dd982`; tệp **có thay đổi chưa commit** (37 dòng: "tách trọn" → "tách trọn vẹn" ở 34 chỗ, bỏ "Khẳng định tất định." và hai vế "chỉ dùng trong chứng minh"), không có trong nhật ký; bản được kiểm là tệp trên đĩa.

Căn cứ: `../CLAUDE.md` mục "Writing course content" và "The author's voice" (gồm quy tắc 2026-11-04 về trạng thái văn bản và 2026-11-09 về từ giảm nhẹ, giải thích đi thẳng vào ý); `CLAUDE.md` của học phần mục "Lecture notes"; `planning/lec-01/van-phong-tac-gia.md` (§1–§7, bảng thuật ngữ §5, §6b: giả thiết gom ở §2, mục tiêu §1 thành danh sách công thức, $\sup$ cho độ lệch đồng thời); `planning/van-phong.md`, `thuat-ngu.md`, `ky-hieu.md`, `materials/_templates/lecture-note.md`; `no-ai-slop` chế độ Detect. Ngoài phạm vi: dẫn lại toán học, tệp bài tập.

**Kiểm của điều phối viên:** `forward_refs.py` báo 0 trước khi giao việc; script đối chiếu xác nhận mọi trích dẫn ở cột `bằng chứng` là chuỗi con nguyên văn của ghi chú, tại hoặc sát dòng được ghi; đếm mức độ khớp với báo cáo. Điều phối viên kiểm lại #1: `thuat-ngu.md` 2 dòng, `exercises.md` Bài 03 50 dòng, ghi chú Bài 04 và Bài 07 vẫn dùng "tách trọn": đúng. Dòng 538 dẫn (T4) trong khi giả thiết của bài là (T5) (dòng 93): đúng.

**Kết luận:** 88 phát hiện (chặn bàn giao 0, nghiêm trọng 1, trung bình 32, nhẹ 55, sau điều chỉnh của điều phối viên). Mọi phát hiện được chấp nhận làm đầu vào cho lượt sửa; chưa phát hiện nào được sửa. Hàng có ghi "văn bản tác giả" hoặc "VBTG" chỉ để báo, không sửa câu chữ của tác giả.

**Câu hỏi mở cho tác giả và chuyển tiếp:**

- #1: chốt "tách trọn" hay "tách trọn vẹn" cho cả học phần (ghi chú, bài tập, dàn ý, `thuat-ngu.md`, Bài 04, Bài 07); quyết định cả việc giữ hay bỏ thay đổi chưa commit.
- #83: khối "Quan hệ với giáo trình UML" (chung cho mọi bài).
- Chuyển người kiểm độ chính xác: dòng 861 đặt chaining ở UML §28.1, dòng 924 mô tả §28.1 là cận Rademacher.

### Bảng phát hiện

| # | mức độ | vị trí | quy tắc | vấn đề | bằng chứng | đề xuất sửa | quyết định |
|---|---|---|---|---|---|---|---|
| 1 | nghiêm trọng | Toàn bài, dòng 132–1019 (34 chỗ); đối chiếu `exercises.md` Bài 03, `thuat-ngu.md` dòng 206 và 520, `outline.md` Bài 03, ghi chú và bài tập Bài 04, Bài 07 | thuật ngữ (nhất quán) | Thay đổi chưa commit đổi "tách trọn" thành "tách trọn vẹn" chỉ trong ghi chú Bài 03. Bảng thuật ngữ vẫn chốt "tách trọn" (điều phối viên, 2026-10-31); bài tập Bài 03 dùng "tách trọn" 64 lần (cả câu mở đầu định nghĩa lại thuật ngữ), dàn ý 41 lần, ghi chú Bài 04 6 lần và bài tập Bài 04 4 lần, ghi chú Bài 07 11 lần và bài tập Bài 07 4 lần. Học viên gặp hai tên cho cùng một khái niệm *shatter*, trái quy tắc "một nghĩa một thuật ngữ". | `## 4. Thu hẹp, tách trọn vẹn và chiều VC` | Điều phối viên hoặc tác giả chốt một thuật ngữ và ghi vào `review-log.md`. Nếu giữ "tách trọn vẹn": sửa `thuat-ngu.md` dòng 206 và 520, `exercises.md` Bài 03 (64 chỗ), ghi chú và bài tập Bài 04, Bài 07, `outline.md` Bài 03 trong cùng một lượt. Nếu không: hoàn tác 34 chỗ trong ghi chú. | chấp nhận; chờ tác giả chốt thuật ngữ |
| 2 | nhẹ | Đoạn dẫn, dòng 5 | từ giảm nhẹ | "vài lớp" là từ giảm nhẹ không có nội dung định lượng; hai lớp được dẫn đích danh ngay sau. | `Ngoài vài lớp có cấu trúc riêng, như ở Bài tập 01.9 và 02.7,` | "Ngoài các lớp của Bài tập 01.9 và 02.7, chúng ta chưa có cận cỡ mẫu cho lớp vô hạn." | chấp nhận; chưa sửa |
| 3 | nhẹ | Đoạn dẫn, dòng 5 | danh sách song song | Ba công cụ song song viết liền trong một câu; quy tắc tác giả: từ ba mục song song trở lên thành danh sách. | `Ba công cụ là chiều Vapnik–Chervonenkis (VC dimension), gọi tắt là chiều VC, hàm tăng trưởng (growth function) và mẫu bóng (ghost sample).` | "Ba công cụ của bài bao gồm:" rồi ba gạch đầu dòng: chiều Vapnik–Chervonenkis (VC dimension), gọi tắt là chiều VC; hàm tăng trưởng (growth function); mẫu bóng (ghost sample). | chấp nhận; chưa sửa |
| 4 | nhẹ | Câu hỏi mở đầu, dòng 9 | công thức thay lời | "năm mức đo" mô tả bằng lời một tập cụ thể. | `trên năm mức đo của ví dụ sàng lọc, cả lớp chỉ cho sáu hàm khác nhau` | "trên năm mức đo $\{1,\ldots,5\}$ của ví dụ sàng lọc (Ví dụ 01.1), cả lớp chỉ cho sáu hàm khác nhau" | chấp nhận; chưa sửa |
| 5 | trung bình | Câu hỏi mở đầu, dòng 13 | câu hỏi mở đầu; dẫn trước | Câu hỏi mở đầu được trả lời ngay trong mục mở đầu bằng một con số của một cận chưa phát biểu; quy tắc tác giả: câu hỏi mở đầu là câu hỏi mở, không gợi đáp án. Dạng "…: …" là kiểu câu "colon reveal"; "cận của bài" không gọi tên kết quả. | `Câu trả lời bằng số cho lớp hàm ngưỡng: theo cận của bài, $54\,330$ quan sát là đủ.` | Bỏ câu. Con số đã có ở câu "Tóm lại" của Ví dụ 03.9 (dòng 754), nơi câu hỏi được trả lời. | chấp nhận; chưa sửa |
| 6 | nhẹ | Mục tiêu học tập 1, dòng 19 | mục tiêu gọn | Vế phụ chú thích cách đánh giá, cùng loại với "với đúng thứ tự lượng từ" mà tác giả đã cắt ở Bài 01. | `và nhận ra một lập luận chỉ có một trong hai phần` | Bỏ vế này. | chấp nhận; chưa sửa |
| 7 | nhẹ | Mục tiêu học tập 2, dòng 20 | mục tiêu gọn | Mục tiêu kèm một vế giải thích dài. | `và giải thích vì sao số cách gán nhãn bị chặn bởi một đa thức của số điểm khi chiều VC hữu hạn` | Bỏ vế, hoặc rút thành "và chặn hàm tăng trưởng bằng một đa thức của số điểm". | chấp nhận; chưa sửa |
| 8 | trung bình | Mục tiêu học tập 3, dòng 21 | mục tiêu gọn | Mục tiêu có hai câu và hai vế phụ ("chỉ ra chỗ dùng từng giả thiết", "giải thích vì sao không lấy bất đẳng thức hợp…"), cùng loại với "chỉ ra bước hỏng khi giả thuyết được chọn theo mẫu" mà tác giả đã cắt ở Bài 01. | `Giải thích vì sao không lấy bất đẳng thức hợp trên các cách gán nhãn của chính tập huấn luyện.` | "Trình bày năm bước chứng minh cận hội tụ đều theo chiều VC." | chấp nhận; chưa sửa |
| 9 | nhẹ | Mục tiêu học tập 4, dòng 22 | mục tiêu gọn | Vế phụ chú thích. | `chỉ ra nguồn chênh lệch` | Bỏ vế ", chỉ ra nguồn chênh lệch". | chấp nhận; chưa sửa |
| 10 | nhẹ | Kiến thức tiên quyết, dòng 30 | tiếng Anh lần đầu | Lần đầu thuật ngữ xuất hiện trong ghi chú nhưng chưa kèm tên tiếng Anh (cũng chưa có ở dòng 785, 824, 923). | `Nhận xét 01.30 (định lý không có bữa trưa miễn phí)` | "Nhận xét 01.30 (định lý không có bữa trưa miễn phí, no-free-lunch theorem)". | chấp nhận; chưa sửa |
| 11 | trung bình | §2, dòng 99 | trạng thái văn bản | Câu nói điều bài không làm. | `Không kết quả nào dùng giả thiết lồi, trơn hay Lipschitz.` | Bỏ câu. | chấp nhận; chưa sửa |
| 12 | trung bình | §3, Ví dụ 03.1, dòng 111 | trạng thái văn bản; văn bản làm chủ ngữ | "Ví dụ chỉ xét…" lấy văn bản làm chủ ngữ và nói điều ví dụ không cần. | `Ví dụ chỉ xét lớp và các bộ điểm, không cần phân bố.` | Bỏ câu. | chấp nhận; chưa sửa |
| 13 | nhẹ | §3, Ví dụ 03.1, dòng 115 | nhãn bước | Bước 2 là một nhận xét một câu, không phải phép tính riêng; quy tắc tác giả gộp bước hiển nhiên vào mạch văn. | `**Bước 2: Định lý 02.14 không áp dụng.**` | Gộp vào Bước 1: "… có vô số phần tử, nên bán kính $r_m=\sqrt{\ln(2K/\delta)/(2m)}$ của Định lý 02.14 không xác định."; đánh lại số bước. | chấp nhận; chưa sửa |
| 14 | nhẹ | §3, Ví dụ 03.1, dòng 117 | công thức thay lời | Số điểm bên trái $t$ mô tả bằng lời. | `chỉ phụ thuộc số điểm $x_i$ nằm bên trái $t$` | "chỉ phụ thuộc $\lvert\{i:x_i<t\}\rvert$" | chấp nhận; chưa sửa |
| 15 | trung bình | §3, Ví dụ 03.1, dòng 119 | trạng thái văn bản; đại từ không rõ | "Điều này chưa cho phép…" nói điều lập luận chưa làm được, với "Điều này" không có tiền ngữ rõ; lý do (tập véc-tơ phụ thuộc mẫu) chỉ có ở dòng 538. | `Điều này chưa cho phép thay $K$ bằng $m+1$ trong Định lý 02.14.` | "Tuy nhiên, tập $m+1$ véc-tơ này phụ thuộc mẫu, nên không thể thay $K$ bằng $m+1$ trong Định lý 02.14." Hoặc bỏ câu. | chấp nhận; chưa sửa |
| 16 | nhẹ | §3, ứng dụng, dòng 125 | công thức thay lời | Điều kiện dương tính nói bằng lời ngay sau công thức của nó. | `kết quả dương tính khi một tổ hợp tuyến tính của các chỉ số đo vượt ngưỡng $-b$` | "kết quả dương tính khi $\langle w,x\rangle\ge-b$" | chấp nhận; chưa sửa |
| 17 | nhẹ | §4, Định nghĩa 03.1, dòng 137 | giải thích vòng vo | Vế "tức …" nhắc lại $y\in\{0,1\}^k$ bằng lời. | `tức một tổ hợp nhãn $0$, $1$ trên các điểm của $C$` | Bỏ vế. | chấp nhận; chưa sửa |
| 18 | nhẹ | §4, dòng 147 | nhắc lại | Vế cuối nhắc lại câu thứ hai của §4 (dòng 134). | `nên trên tập huấn luyện đó $L_S$ chỉ phụ thuộc $h$ qua $\lvert\mathcal H_C\rvert$ véc-tơ` | Giữ công thức $L_S(h)=\frac1m\sum_i\mathbb 1[h(X_i)\ne Y_i]$ và bỏ vế "nên trên tập huấn luyện đó …", hoặc bỏ câu tương ứng ở dòng 134. | chấp nhận; chưa sửa |
| 19 | trung bình | §4, Ví dụ 03.2, dòng 152 | trạng thái văn bản; văn bản làm chủ ngữ | Như dòng 12 của bảng. | `Ví dụ không cần phân bố.` | Bỏ câu. | chấp nhận; chưa sửa |
| 20 | nhẹ | §4, Ví dụ 03.2, dòng 160 và 170 | nhãn bước | Nhãn gọi tên thao tác ("liệt kê", "đếm"), không gọi tên kết quả; Bước 3 là một dòng. | `**Bước 3: đếm.**` | Đổi "Bước 2: liệt kê" thành "**Sáu véc-tơ.**"; bỏ nhãn Bước 3 và nối "Do đó $\lvert\mathcal H_C\rvert=6$, trong khi $C$ có $2^5=32$ cách gán nhãn." vào bước trước. | chấp nhận; chưa sửa |
| 21 | nhẹ | §4, dòng 175 | cấu trúc khó theo | Mệnh đề chen giữa "thì" và chủ ngữ của vế chính. | `thì, dù các nhãn quan sát trên tập đó là gì, lớp vẫn có` | "Nếu lớp thực hiện được mọi cách gán nhãn của một tập điểm thì với mọi nhãn quan sát trên tập đó, lớp có một giả thuyết với rủi ro thực nghiệm bằng $0$." | chấp nhận; chưa sửa |
| 22 | nhẹ | §4, dòng 181 | chủ thể trừu tượng | "Định nghĩa dùng tập" lấy định nghĩa làm chủ ngữ (`van-phong.md` §9a). | `Định nghĩa dùng tập, nên một bộ có điểm lặp không được xét` | "Hai điểm trùng nhau luôn nhận cùng nhãn, nên ta chỉ xét tập, không xét bộ có điểm lặp." | chấp nhận; chưa sửa |
| 23 | nhẹ | §4, Nhận xét 03.4, dòng 196 | danh sách song song | Chuỗi "Lỗi thứ nhất … Lỗi thứ hai …"; tác giả đã tách hai loại lỗi FN/FP ở Bài 01 thành hai gạch đầu dòng. | `Có hai lỗi đối xứng. Lỗi thứ nhất là kết luận $d=k$ từ một tập $k$ phần tử bị tách trọn vẹn` | "Có hai lỗi đối xứng:" rồi hai gạch đầu dòng "**Ở cận dưới.** …", "**Ở cận trên.** …". | chấp nhận; chưa sửa |
| 24 | nhẹ | §4, Mệnh đề 03.5, dòng 205 | công thức thay lời | **Bảo đảm.** nói bằng lời giá trị chiều VC. | `Chiều VC của cả hai lớp bằng $1$;` | "$\operatorname{VCdim}(\mathcal H_{\mathrm{thr}})=\operatorname{VCdim}(\{h_t:t=1,\ldots,6\})=1$;" | chấp nhận; chưa sửa |
| 25 | nhẹ | §4, chứng minh Mệnh đề 03.5, dòng 215 | cặp đối lập | Câu ý nghĩa dựng theo khuôn "đo X, không đo Y"; quy tắc tác giả ưu tiên dạng khẳng định. | `chiều VC đo khả năng gán nhãn tự do của lớp, không đo số phần tử.` | "chiều VC là số điểm lớn nhất mà lớp gán nhãn tùy ý được, dù lớp có vô số phần tử." | chấp nhận; chưa sửa |
| 26 | nhẹ | Câu sau $\square$: dòng 244, 607, 962, 1021, 1117 | chứng minh (câu ý nghĩa) | Các câu sau $\square$ nói về lớp, về hằng số hay về các trường hợp đã xử lý, không nói kết quả có nghĩa gì cho việc học (`CLAUDE.md` học phần, mục Proofs). Dòng 1117 chỉ liệt kê chỗ dùng giả thiết; dòng 1021 bàn trường hợp điểm lặp. | `Hai lớp $\mathcal H_{\mathrm{thr}}$ và $\mathcal H_{\mathrm{int}}$ có cùng lực lượng (cardinality) với $\mathbb R$ nhưng chiều VC khác nhau.` | Thêm hoặc thay bằng một câu về ý nghĩa cho việc học, chỉ dùng điều đã có trong bài; ví dụ dòng 1117: "Cận không phụ thuộc $D$, nên cỡ mẫu đủ chỉ phụ thuộc lớp qua $\Pi_{\mathcal H}(2m)$." | chấp nhận; chưa sửa |
| 27 | nhẹ | §5, Định nghĩa 03.7, dòng 261 | thuật ngữ (tiếng Anh) | Tên tiếng Anh số nhiều, trong khi dòng 260 dùng số ít. | `(homogeneous halfspaces)` | "(homogeneous halfspace)" | chấp nhận; chưa sửa |
| 28 | nhẹ | §5, dòng 268 | câu "dưới đây" | Kiểu "bổ đề dưới đây khẳng định…", cùng loại với "bất đẳng thức dưới đây … Bất đẳng thức đó là" mà tác giả đã sửa. | `Bổ đề dưới đây khẳng định điều này cho mọi $p+2$ điểm của $\mathbb R^p$.` | "Mọi $p+2$ điểm của $\mathbb R^p$ đều chia được như vậy." | chấp nhận; chưa sửa |
| 29 | trung bình | §5, Bổ đề 03.8, dòng 270 và 283 | nhãn kết quả (độ sâu chứng minh) | Tiêu đề khối thiếu độ sâu chứng minh; phần "Ý chứng minh:" nằm ngoài khối `proof`, chứng minh đầy đủ ở Phụ lục A. | `::: lemma Bổ đề 03.8 (Phân hoạch Radon)` | "::: lemma Bổ đề 03.8 (Phân hoạch Radon) — phác thảo"; đưa đoạn dòng 283 vào khối `::: proof Chứng minh Bổ đề 03.8 (phác thảo)`. | chấp nhận; chưa sửa |
| 30 | trung bình | §5, Mệnh đề 03.9, dòng 285 | nhãn kết quả (độ sâu chứng minh) | Tiêu đề khối thiếu độ sâu chứng minh, dù mệnh đề có chứng minh (một phần ở Phụ lục A). | `::: proposition Mệnh đề 03.9 (Chiều VC của lớp nửa không gian)` | Thêm "— chứng minh đầy đủ". | chấp nhận; chưa sửa |
| 31 | nhẹ | §5, chứng minh Mệnh đề 03.9, dòng 319 | câu điều hướng | Câu bị động dẫn sang Phụ lục A; chứng minh ở Phụ lục A chỉ có bốn bước ngắn (dòng 965–980). | `Cận trên $d\le p$ được chứng minh ở Phụ lục A bằng phụ thuộc tuyến tính` | Đưa chứng minh dòng 965–980 vào Bước 4; hoặc viết chủ động: "Cận trên $d\le p$ dùng phụ thuộc tuyến tính của $p+1$ véc-tơ trong $\mathbb R^p$ (chứng minh: Phụ lục A)." | chấp nhận; chưa sửa |
| 32 | nhẹ | §5 dòng 321; §7, Ví dụ 03.7 dòng 611 | câu điều hướng | "của ứng dụng ở §3" dẫn mục thay cho gọi tên lớp. | `Lớp của ứng dụng ở §3 là` | Dòng 321: "Lớp hàm phân lớp tuyến tính trên mười chỉ số đo là"; dòng 611: "lớp $\mathcal H^{10}_{\mathrm{aff}}$ (mười chỉ số đo)". | chấp nhận; chưa sửa |
| 33 | trung bình | §5, Ví dụ 03.3, dòng 331 | danh sách song song | Bốn nhóm cách gán nhãn song song dồn trong một câu sau dấu hai chấm. | `Mười bốn cách còn lại thực hiện được: hai hàm hằng, bốn cách tách riêng một đỉnh,` | "Mười bốn cách còn lại thực hiện được, bao gồm:" rồi bốn gạch đầu dòng (hai hàm hằng; bốn cách tách riêng một đỉnh; bốn cách tách hai đỉnh kề nhau bằng một đường song song với một cạnh; bốn phần bù của cách tách một đỉnh). | chấp nhận; chưa sửa |
| 34 | trung bình | §5, dòng 338 | đại từ không rõ; văn bản làm chủ ngữ | "hai số" không có tiền ngữ rõ (câu trước nói số tham số và $\ln\lvert\mathcal H\rvert$, còn ý là số tham số và chiều VC); "điều đó" mơ hồ; "Câu hỏi mở đầu khẳng định" lấy văn bản làm chủ ngữ. | `Với nửa không gian afin, hai số trùng nhau; điều đó không đúng nói chung.` | "Số tham số không thay được $\ln\lvert\mathcal H\rvert$. Với nửa không gian afin, số tham số và chiều VC cùng bằng $p+1$; với các lớp khác, hai số này có thể khác nhau." | chấp nhận; chưa sửa |
| 35 | nhẹ | §5, Nhận xét 03.10, dòng 347 | phủ định; ý nghĩa tích cực | Kết luận viết bằng hai phủ định. | `Số tham số không cho cận trên, cũng không cho cận dưới, của chiều VC.` | "Theo (ii), chiều VC có thể lớn hơn số tham số; theo (iii), nó có thể nhỏ hơn." | chấp nhận; chưa sửa |
| 36 | trung bình | Cuối §5, dòng 350 | trạng thái văn bản | "chưa cho biết" nói điều khái niệm chưa làm được (cùng loại "Ví dụ 09.1 chưa cho biết …" trong quy tắc 2026-11-04). | `nó chưa cho biết lớp tạo ra bao nhiêu cách gán nhãn trên $m>d$ điểm.` | "Chiều VC là số điểm lớn nhất của một tập bị lớp tách trọn vẹn. Với $m>d$ điểm, ta cần đếm số cách gán nhãn mà lớp tạo ra." | chấp nhận; chưa sửa |
| 37 | trung bình | §6, dòng 364 | dẫn trước | "hai mẫu gộp lại" nói trước mẫu bóng và mẫu gộp, chỉ được đưa vào ở dòng 540 và 601. | `và $2m$ khi áp dụng cho hai mẫu gộp lại.` | Bỏ cả câu dòng 364 (dòng 366 đã nêu $\lvert\mathcal H_{(X_1,\ldots,X_m)}\rvert\le\Pi_{\mathcal H}(m)$). | chấp nhận; chưa sửa |
| 38 | trung bình | §6, dòng 368 | lời bình kĩ thuật | Vế "Nhờ vậy … xác định cả khi $\mathcal X$ có ít hơn $m$ điểm" là lời bình về điều kiện kĩ thuật, không dùng lại. | `Nhờ vậy $\Pi_{\mathcal H}(m)$ xác định cả khi $\mathcal X$ có ít hơn $m$ điểm, và` | "Bộ điểm được phép có điểm lặp, nên $\Pi_{\mathcal H}(m)$ không giảm theo $m$: thêm vào bộ một điểm lặp không làm giảm số cách gán nhãn." | chấp nhận; chưa sửa |
| 39 | nhẹ | §6, Ví dụ 03.4, dòng 379 và 391 | nhãn bước | Nhãn "kết luận" (tác giả đã bỏ nhãn "**Kết luận.**" ở Ví dụ 01.3) và nhãn thao tác "số cụ thể". | `**Bước 3: kết luận cho hàm ngưỡng.**` | Bỏ nhãn Bước 3, nối "Do đó $\Pi_{\mathcal H_{\mathrm{thr}}}(m)=m+1$." vào Bước 2; đổi "Bước 6: số cụ thể" thành "**Giá trị tại $m=5$.**". | chấp nhận; chưa sửa |
| 40 | nhẹ | §6, chứng minh Bổ đề 03.12, dòng 408 | kiểu chữ | "xử lí" trái `van-phong.md` §12 ("xử lý"). | `các trường hợp gốc và điểm lặp được xử lí ở Phụ lục B.` | "xử lý". Dẫn chiếu Phụ lục B giữ được vì đây là chứng minh phác thảo hoàn thiện ở Phụ lục. | chấp nhận; chưa sửa |
| 41 | nhẹ | §6, chứng minh Bổ đề 03.12, dòng 415 | cấu trúc khó theo | Chủ ngữ "Giả thiết quy nạp" xa động từ "cho" bởi một mệnh đề chen. | `Giả thiết quy nạp, phát biểu cho mọi tập cách gán nhãn của $m-1$ vị trí, cho` | "Áp dụng giả thiết quy nạp cho mọi tập cách gán nhãn của $m-1$ vị trí, ta được $\lvert\mathcal H_{C'}\rvert\le\ldots$ và $\lvert Y_1\rvert\le\ldots$." | chấp nhận; chưa sửa |
| 42 | nhẹ | §6, dòng 432 và 478 | công thức thay lời | "không vượt quá cỡ $d\ln m$" là cách nói phỏng chừng trong khi công thức chính xác đã có. | `không vượt quá cỡ $d\ln m$` | Dòng 432: bỏ vế (đã có $\ln\Pi_{\mathcal H}(m)\le d\ln(em/d)$); dòng 478: "đủ để thấy $\ln\Pi_{\mathcal H}(m)\le d\ln(em/d)$". | chấp nhận; chưa sửa |
| 43 | trung bình | §6, Ví dụ 03.5, dòng 455 | trạng thái văn bản | Vế nói điều ví dụ không tính. | `với nửa mặt phẳng, các giá trị với $m\ge5$ không được tính ở đây.` | "Bảng thứ nhất ghi hàm tăng trưởng; cột $\mathcal H^2_{\mathrm{aff}}$ ghi $m\le4$." | chấp nhận; chưa sửa |
| 44 | nhẹ | §6, Ví dụ 03.5 dòng 455, 476; §7, Ví dụ 03.7 dòng 627 | nhãn bước | Nhãn gọi tên thao tác ("hai bảng", "đọc bảng", "bảng"). | `**Bước 7: đọc bảng.**` | Gọi tên kết quả, ví dụ "**Giá trị tại $m=20$.**" (dòng 476), "**Hai cận trên ba cỡ mẫu.**" (dòng 627), hoặc bỏ nhãn. | chấp nhận; chưa sửa |
| 45 | nhẹ | Cuối §6, dòng 481 | trực giác | Đoạn ước lượng trực giác chưa mở bằng dấu hiệu trực giác của tác giả. | `Nếu $d\ln(em/d)$ thay được cho $\ln K$ trong Định lý 02.14,` | "Một cách trực quan, nếu $d\ln(em/d)$ thay được cho $\ln K$ …". | chấp nhận; chưa sửa |
| 46 | nhẹ | §7, dòng 485 | câu điều hướng | "cuối §6" dẫn mục thay cho nêu đại lượng. | `Để biến ước lượng cuối §6 thành một bảo đảm` | "Để biến ước lượng $\sqrt{d\ln m/m}$ thành một bảo đảm" | chấp nhận; chưa sửa |
| 47 | trung bình | §7, dòng 485 | văn bản làm chủ ngữ | "Định nghĩa sau gọi…" lấy văn bản làm chủ ngữ và báo trước khối đứng ngay sau. | `Định nghĩa sau gọi đó là một tính chất của lớp.` | Bỏ câu. | chấp nhận; chưa sửa |
| 48 | nhẹ | §7, Ví dụ 03.6, dòng 510 | công thức thay lời; `\mid` | "$Y=1$ chắc chắn" nói bằng lời một xác suất có điều kiện (tác giả viết $D(Y=f(x)\mid X=x)=1$ ở Bài 01). | `$Y=1$ chắc chắn` | "$D(Y=1\mid X=x)=1$ với mọi $x$" | chấp nhận; chưa sửa |
| 49 | trung bình | §7, Ví dụ 03.6, dòng 518 | câu chẻ; nhắc lại | Cấu trúc "Điều … là …" (`van-phong.md` §9a); câu nhắc lại câu đầu đoạn ("hội tụ đều hỏng với mọi cỡ mẫu"). | `Điều không còn đúng là bảo đảm đồng thời cho mọi giả thuyết của lớp.` | Bỏ câu. | chấp nhận; chưa sửa |
| 50 | trung bình | §7, dòng 523 | câu điều hướng; siêu văn bản | "ở §2" dẫn mục; "đủ cho mọi lớp của bài" là một khẳng định về văn bản, được kiểm ở Nhận xét 03.14 sau đó. | `Điều kiện (M) ở §2 đủ cho mọi lớp của bài.` | "Điều kiện (M) bảo đảm độ lệch đều đo được." | chấp nhận; chưa sửa |
| 51 | trung bình | §7, dòng 525 | lời bình kĩ thuật; câu "dưới đây" | Câu bình về hậu quả kĩ thuật khi thiếu điều kiện, nhắc lại "có thể không đo được" ở dòng 523, kèm "dưới đây". | `Không có một điều kiện như vậy, các xác suất dưới đây có thể không xác định.` | Bỏ câu. | chấp nhận; chưa sửa |
| 52 | trung bình | §7, dòng 535 | tự hỏi tự đáp | Câu hỏi được trả lời ngay bằng "Không, …", đúng khuôn "…không? Không: …" mà tác giả đã cắt ở Bài 01. | `Không, vì hai lý do.` | Giữ "**Câu hỏi.** … không?"; thay "Không, vì hai lý do." bằng câu dẫn "Bất đẳng thức hợp trên các cách gán nhãn của tập huấn luyện gặp hai trở ngại." | chấp nhận; chưa sửa |
| 53 | trung bình | §7, dòng 538 | giả thiết (nhãn) | Dẫn sai giả thiết: bài thay (T4) bằng (T5) (dòng 88, 93); điều cấm "lớp chọn theo mẫu" là (T5), và dòng 540 cũng dùng (T5). Kèm cấu trúc "đúng điều mà". | `Tập các cách gán nhãn phụ thuộc $S$, nên đó là một lớp chọn theo mẫu, đúng điều mà (T4) cấm.` | "Tập các cách gán nhãn phụ thuộc $S$, nên đó là một lớp chọn theo mẫu, trái với (T5)." | chấp nhận; chưa sửa |
| 54 | nhẹ | §7, Định lý 03.15, dòng 550 | tiếng Anh lần đầu | Thuật ngữ mới in nghiêng chưa kèm tiếng Anh (`thuat-ngu.md` dòng 217: VC radius). | `Đặt *bán kính VC*` | "Đặt *bán kính VC* (VC radius)" | chấp nhận; chưa sửa |
| 55 | nhẹ | §7, Định lý 03.15, dòng 554 | phụ thuộc tường minh | Sự phụ thuộc nói bằng lời "ngầm"; quy tắc tác giả: ghi phụ thuộc tường minh như $\hat t=\hat t(S)$. | `phụ thuộc ngầm vào $\mathcal H$ và $\delta$.` | "và $\rho_m=\rho_m(\mathcal H,\delta)$." | chấp nhận; chưa sửa |
| 56 | nhẹ | §7, Định lý 03.15(b), dòng 563 | công thức một dòng | $\rho_m$ đứng riêng một dòng (khuôn `&X\\ &\le…` mà tác giả đã gộp ở Bài 01). Đo ở 390 px: "$\rho_m\le\sqrt{\tfrac8m(\ldots)}$" rộng 225 px, vừa khung danh sách 230 px. | `&\rho_m\\` | `\rho_m&\le\sqrt{\tfrac8m(d\ln\tfrac{2em}d+\ln\tfrac4\delta)}\\ &\le4\sqrt{\tfrac1m(d\ln\tfrac{em}d+\ln\tfrac2\delta)}.` (hai dòng) | chấp nhận; chưa sửa |
| 57 | nhẹ | §7, Định lý 03.15, dòng 576 | dồn ý | Ba tính chất độc lập của cận dồn sau dấu chấm phẩy. | `nó không phụ thuộc $D$, khi $d\ge1$ giảm theo $m$ như $\sqrt{\ln m/m}$, và phụ thuộc $\delta$ qua $\ln(1/\delta)$.` | Tách thành câu riêng: "Cận không phụ thuộc $D$. Khi $d\ge1$, cận giảm theo $m$ như $\sqrt{\ln m/m}$ và phụ thuộc $\delta$ qua $\ln(1/\delta)$." | chấp nhận; chưa sửa |
| 58 | trung bình | §7, chứng minh Định lý 03.15, Bước 1, dòng 593 | công thức thay lời | Bất đẳng thức then chốt của bước nói bằng lời. | `Do đó biến cố có mẫu bóng có xác suất ít nhất một nửa xác suất biến cố ban đầu; đây là hệ số $2$.` | "Do đó $\Pr\big[\sup_h\lvert L_{S'}(h)-L_S(h)\rvert>\epsilon/2\big]\ge\tfrac12\Pr\big[\sup_h\lvert L_S(h)-L_D(h)\rvert>\epsilon\big]$; đây là hệ số $2$." | chấp nhận; chưa sửa |
| 59 | trung bình | §7, chứng minh Định lý 03.15, Bước 2, dòng 595 | thuật ngữ | "phân bố đồng thời" đã được tác giả đổi thành "phân bố liên hợp" (`thuat-ngu.md` dòng 5 và 126; `van-phong-tac-gia.md` §5). | `có cùng phân bố đồng thời với họ` | "có cùng phân bố liên hợp với họ" | chấp nhận; chưa sửa |
| 60 | nhẹ | §7, chứng minh Định lý 03.15, Bước 4, dòng 603 | công thức thay lời | Cận Hoeffding nói bằng lời. | `cho xác suất lệch ít nhất $\epsilon/2$ không quá $2e^{-m\epsilon^2/8}$` | "cho $\Pr_\sigma\big(\lvert\tfrac1m\sum_i\sigma_i(\cdot)\rvert\ge\epsilon/2\big)\le2e^{-m\epsilon^2/8}$" | chấp nhận; chưa sửa |
| 61 | nhẹ | §7, Ví dụ 03.7, dòng 621–622 | công thức một dòng | Một quan hệ ngắn bị ngắt hai dòng. Đo ở 390 px: dạng gộp rộng 267 px, vừa khung khối 271 px. | `&\frac{8(29{,}415+4{,}382)}{10^4}\\` | `&\frac{8(29{,}415+4{,}382)}{10^4}\approx0{,}027037,` trên một dòng. | chấp nhận; chưa sửa |
| 62 | trung bình | §7, Ví dụ 03.7, dòng 638 | ý nghĩa tích cực | Câu nói con số "không phải" là gì; quy tắc tác giả: nêu nghĩa tích cực, có thể vận hành của bảo đảm. | `đây là cận trên của độ lệch đều, không phải giá trị của nó.` | "nghĩa là với xác suất ít nhất $0{,}95$, độ lệch đều không vượt quá $0{,}280$ khi $m=10^4$." | chấp nhận; chưa sửa |
| 63 | nhẹ | Cuối §7, dòng 668 | cấu trúc khó theo | Chủ ngữ là một cụm động từ dài có mệnh đề chen, động từ chính ở xa. | `Bỏ tính độc lập của các quan sát, như khi chép lại một quan sát ở Ví dụ 02.6, làm hỏng Bước 1` | "Khi các quan sát không độc lập, chẳng hạn một quan sát chép lại $m$ lần như ở Ví dụ 02.6, Bước 1 và Bước 2 của chứng minh không còn đúng: …" | chấp nhận; chưa sửa |
| 64 | trung bình | §8, sau Hệ quả 03.16, dòng 706 | giải thích mơ hồ | "bản mở rộng sang trường hợp bất khả diễn" không nói rõ đại lượng nào. | `Độ phức tạp mẫu $m_{\mathcal H}$ ở đây là bản mở rộng sang trường hợp bất khả diễn.` | "Ở đây $m_{\mathcal H}$ là độ phức tạp mẫu của học PAC bất khả diễn (Định nghĩa 01.25)." | chấp nhận; chưa sửa |
| 65 | nhẹ | §8, chứng minh Hệ quả 03.16, Bước 2, dòng 721 | nhận xét bên lề; nhắc lại | Câu so sánh với Bài 02 nhắc lại dòng 672. | `Bước này không cần một phần tử tốt nhất $h_{\mathcal H}$ tồn tại, khác với Bước 1 của chứng minh Hệ quả 02.16.` | Bỏ câu. | chấp nhận; chưa sửa |
| 66 | nhẹ | §8, Ví dụ 03.9, dòng 731 | danh sách song song | Ba lớp song song viết liền. | `Ba lớp: $d=1$ (lớp hàm ngưỡng của câu hỏi mở đầu),` | "Ba lớp, bao gồm:" rồi ba gạch đầu dòng $d=1$, $d=3$, $d=11$. | chấp nhận; chưa sửa |
| 67 | nhẹ | §8, Ví dụ 03.9, dòng 748 | lời bình kĩ thuật | Vế bình luận về số chữ số hiển thị. | `cần bảy chữ số vì hai giá trị rất gần $0{,}01$.` | Bỏ vế; giữ hai giá trị. | chấp nhận; chưa sửa |
| 68 | trung bình | §8, Ví dụ 03.9, dòng 754 | ý nghĩa tích cực; cặp đối lập | Câu cuối nói con số "không phải" là gì. | `Mọi con số là cỡ mẫu đủ, không phải cỡ mẫu cần.` | "Mỗi con số là một cận trên của độ phức tạp mẫu $m_{\mathcal H}(0{,}1;0{,}05)$ của lớp tương ứng." | chấp nhận; chưa sửa |
| 69 | nhẹ | Dòng 13, 754, 782, 869 | siêu văn bản ("của bài") | "cận của bài", "hằng số của bài", "Các cận của bài" chỉ văn bản thay cho gọi tên kết quả; câu dòng 869 là lời đánh giá chung, câu sau đã cho con số. | `theo cận của bài` | Dòng 13 và 754: "theo Hệ quả 03.16(a)"; dòng 782: "với các hằng số của Định lý 03.15 và Định lý 02.14"; dòng 869: bỏ câu "Các cận của bài là bảo thủ." | chấp nhận; chưa sửa |
| 70 | nhẹ | §8, Ví dụ 03.10, dòng 782 | từ giảm nhẹ | "chủ yếu" thay cho con số tính được từ Bước 4: $\rho_m^2/r_m^2=16\ln480/\ln240$. | `chủ yếu do hằng số $8$ của mẫu bóng` | "trong đó thừa số $\sqrt{16}=4$ đến từ hằng số $8$ trong $\rho_m$ và mẫu số $2m$ trong $r_m$" | chấp nhận; chưa sửa |
| 71 | trung bình | §8, dòng 785 | văn bản làm chủ ngữ | "Định lý sau phát biểu…, và gom…" lấy văn bản làm chủ ngữ và báo trước. | `Định lý sau phát biểu điều kiện cần, và gom các khái niệm học của Bài 01–03 vào một danh sách tương đương.` | "Chiều VC hữu hạn cũng là điều kiện cần, và dưới (M) nó tương đương với các khái niệm học của Bài 01–03." | chấp nhận; chưa sửa |
| 72 | nhẹ | §8, dòng 816 | giải thích vòng vo | Câu dẫn "cho kết luận như sau" trước một lập luận nhắc lại kết luận đã có ở dòng 804. | `Khi $d=\infty$, phần (a) cho kết luận như sau:` | "Với $d=\infty$, lấy $\epsilon<1/8$ và $\delta<1/7$: …" | chấp nhận; chưa sửa |
| 73 | nhẹ | §8, dòng 818 | câu điều hướng (nguồn) | Câu nhắc nguồn đã ghi trong tiêu đề Định lý 03.17. | `UML §6.4 phát biểu định lý này.` | Bỏ câu. | chấp nhận; chưa sửa |
| 74 | nhẹ | §8, chứng minh Hệ quả 03.18, dòng 839 | diễn đạt thiếu chính xác | "hàm hằng $1$ vẫn học được": một hàm không học; ý là thuật toán trả về hàm này có rủi ro $0$. | `hàm hằng $1$ vẫn học được` | "thuật toán trả về hàm hằng $1$ có rủi ro $0$" | chấp nhận; chưa sửa |
| 75 | trung bình | Cuối §8, dòng 861 | trạng thái văn bản; dồn ý | Câu nói điều nguồn không làm ("UML không chứng minh phần (b)"), dồn ba nguồn sau dấu chấm phẩy. | `UML §28.2 chứng minh phần (a); UML không chứng minh phần (b).` | "UML §6.4 phát biểu hai cận dưới này với hằng số tuyệt đối. Chứng minh nằm ngoài phạm vi học phần (phần (a): UML §28.2)." | chấp nhận; chưa sửa |
| 76 | nhẹ | §9, dòng 867 | từ giảm nhẹ; cặp đối lập | "gần tuyến tính" trong khi Ví dụ 03.9 cho con số; "Chiều VC, không phải số tham số" dựng theo khuôn đối lập. | `nên cỡ mẫu đủ tăng gần tuyến tính theo số đặc trưng (Ví dụ 03.9)` | "nên khi chuyển từ $p=2$ lên $p=10$, cỡ mẫu đủ tăng $3{,}36$ lần, gần tỉ số $11/3\approx3{,}67$ của hai chiều VC (Ví dụ 03.9)" | chấp nhận; chưa sửa |
| 77 | trung bình | §9, dòng 869 | từ giảm nhẹ | "vài lần" trong khi Ví dụ 03.10 cho số chính xác (quy tắc 2026-11-09). | `lớn hơn cỡ mẫu của lớp đã rời rạc hóa vài lần (Ví dụ 03.10)` | "lớn hơn cỡ mẫu của lớp đã rời rạc hóa từ $4{,}5$ đến $5{,}7$ lần (Ví dụ 03.10)" | chấp nhận; chưa sửa |
| 78 | trung bình | §9, dòng 871 | trạng thái văn bản | Câu liệt kê điều nằm ngoài bài. | `chi phí tính toán của ERM và độ phức tạp Rademacher nằm ngoài bài.` | Bỏ câu "Phân lớp nhiều lớp (multiclass classification), … nằm ngoài bài."; độ phức tạp Rademacher đã có ở mục "Mở rộng" của §12. | chấp nhận; chưa sửa |
| 79 | trung bình | §9, dòng 873 | danh sách song song; số lượng | Câu dẫn nói "Hai ví dụ" nhưng đoạn nêu ba trường hợp (Ví dụ 03.8, Ví dụ 02.6, Ví dụ 03.6), viết liền; "Hai ví dụ cho thấy" lấy ví dụ làm chủ ngữ. | `Hai ví dụ cho thấy giả thiết nào không bỏ được.` | "Các giả thiết sau không bỏ được:" rồi ba gạch đầu dòng "**Bỏ (T5).** …", "**Bỏ (T1).** …", "**Bỏ chiều VC hữu hạn.** …", giữ nguyên số hiệu ví dụ. | chấp nhận; chưa sửa |
| 80 | trung bình | §9, dòng 875 | câu treo | Đoạn một câu đứng riêng, không nối với câu nào; "chỉ" là từ giảm nhẹ. Ý thuộc câu về Định lý 03.19 ở dòng 869. | `Trong trường hợp khả diễn, Định lý 03.19(b) chỉ cho cận dưới cỡ $(d+\ln(1/\delta))/\epsilon$.` | Bỏ đoạn và gộp vào dòng 869: "Định lý 03.19 khẳng định cỡ mẫu ít nhất cỡ $(d+\ln(1/\delta))/\epsilon^2$ trong trường hợp bất khả diễn và cỡ $(d+\ln(1/\delta))/\epsilon$ trong trường hợp khả diễn là cần trong trường hợp xấu nhất." | chấp nhận; chưa sửa |
| 81 | nhẹ | §11, dòng 896 | cấu trúc khó theo | Chủ ngữ dài có mệnh đề chen trước vị ngữ "có chứng minh được … không". | `cùng mười sáu hình chữ nhật, mỗi hình thực hiện một cách gán nhãn, có chứng minh được` | "Cho bốn điểm $(1,0)$, $(0,1)$, $(-1,0)$, $(0,-1)$ và mười sáu hình chữ nhật, mỗi hình thực hiện một cách gán nhãn của bốn điểm. Hai dữ kiện này có chứng minh được … không?" | chấp nhận; chưa sửa |
| 82 | nhẹ | §12, dòng 923 | thuật ngữ (tên riêng) | "bổ đề Sauer" trong khi toàn bài và `thuat-ngu.md` dòng 208 dùng "bổ đề Sauer–Shelah". | `gồm bổ đề Sauer và hội tụ đều` | "gồm bổ đề Sauer–Shelah và hội tụ đều" | chấp nhận; chưa sửa |
| 83 | nhẹ | §12, dòng 926 | nguồn gốc (chờ tác giả) | Câu nói về nguồn gốc định nghĩa và số hiệu; quy tắc workspace đưa thông tin nguồn gốc vào `review-log.md`. Cùng khối có ở Bài 01 (dòng 1204, bản tác giả duyệt) và Bài 02, nên cần tác giả quyết cho cả học phần. | `Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục.` | Hỏi tác giả: giữ khối "Quan hệ với giáo trình UML" như Bài 01, hoặc bỏ câu nguồn gốc ở mọi bài và chuyển danh sách khác biệt vào `review-log.md`. | chấp nhận; chưa sửa |
| 84 | trung bình | Phụ lục C, Bước C.1, dòng 1031 | câu điều hướng (đoạn không đánh số) | Dẫn tới một đoạn không đánh số bằng chữ đầu đoạn; người đọc phải tìm đoạn đó để lấy khẳng định dùng trong chứng minh. | `Theo đoạn "Dưới (M), …" ở §7,` | Đánh số đoạn dòng 525 thành một khối (ví dụ một nhận xét có số) và dẫn số đó; hoặc nêu lại khẳng định tại chỗ: "Theo (M), $L_S(g_k)=L_S(h)$ khi $k$ đủ lớn và $L_D(g_k)\to L_D(h)$ theo định lý hội tụ bị chặn, nên với mọi cặp mẫu $(S,S')$, …". | chấp nhận; chưa sửa |
| 85 | nhẹ | Phụ lục C, Bước C.7, dòng 1112 | `aligned`, một quan hệ một dòng | Hai quan hệ trên một dòng ("…$+\kappa\ln(4/\delta)\le m$"). | `&\qquad+\kappa\ln(4/\delta)\le m,` | Tách "\le m," thành dòng riêng `&\le m,`. | chấp nhận; chưa sửa |
| 86 | nhẹ | Phụ lục D, dòng 1122 | câu điều hướng | Câu báo trước, tiêu đề in đậm ngay sau đã đủ. | `Hai lớp còn lại được kiểm dưới đây.` | Bỏ câu. | chấp nhận; chưa sửa |
| 87 | nhẹ | Phụ lục D, dòng 1137 | từ giảm nhẹ | "một chút" thay cho khoảng đã nêu ở dòng 1126. | `được chọn lớn hơn $b$ một chút` | "được chọn trong $[b+1/k,b+2/k]$" | chấp nhận; chưa sửa |
| 88 | nhẹ | Phụ lục D, dòng 1137 | nhận xét bên lề | Câu cuối phụ lục là nhận xét không dùng lại. | `Với lớp vô hạn, (M) chỉ bảo đảm độ lệch đều đo được.` | Bỏ câu. | chấp nhận; chưa sửa |

### Thống kê theo quy tắc (theo báo cáo)

| Nhóm quy tắc | Nhãn trong bảng | Số lần |
|---|---|---|
| Trạng thái văn bản (2026-11-04) | trạng thái văn bản | 8 |
| Câu điều hướng, dẫn trước | câu điều hướng (kể cả nguồn, đoạn không đánh số), dẫn trước, câu "dưới đây" | 11 |
| Văn bản hoặc chủ thể trừu tượng làm chủ ngữ | văn bản làm chủ ngữ, chủ thể trừu tượng, siêu văn bản | 8 |
| Công thức thay lời và trình bày công thức | công thức thay lời, công thức một dòng, `aligned` một quan hệ một dòng, phụ thuộc tường minh, `\mid` | 13 |
| Từ giảm nhẹ (2026-11-09) | từ giảm nhẹ | 5 |
| Giải thích đi thẳng (2026-11-09) | giải thích vòng vo, giải thích mơ hồ, cấu trúc khó theo, đại từ không rõ, dồn ý, nhắc lại, câu chẻ, câu treo, diễn đạt thiếu chính xác | 17 |
| Nghĩa tích cực thay cho phủ định | ý nghĩa tích cực, cặp đối lập, phủ định | 7 |
| Lời bình kĩ thuật, nhận xét bên lề | lời bình kĩ thuật, nhận xét bên lề | 5 |
| Danh sách song song | danh sách song song, số lượng | 6 |
| Nhãn bước | nhãn bước | 4 |
| Mục tiêu học tập gọn | mục tiêu gọn | 4 |
| Thuật ngữ và tiếng Anh lần đầu | thuật ngữ (nhất quán), thuật ngữ, thuật ngữ (tên riêng), thuật ngữ (tiếng Anh), tiếng Anh lần đầu | 6 |
| Khối kết quả và chứng minh | nhãn kết quả (độ sâu chứng minh), chứng minh (câu ý nghĩa), giả thiết (nhãn) | 4 |
| Câu hỏi | câu hỏi mở đầu, tự hỏi tự đáp | 2 |
| Khác | trực giác, kiểu chữ, nguồn gốc (chờ tác giả) | 3 |

## Giữ thay đổi chưa commit của ghi chú — quyết định của người dùng (2026-11-13)

Người dùng quyết định giữ nguyên và commit các thay đổi chưa commit của `materials/lec-03/lecture-note.md` (xem mục "Kiểm tuân thủ nguyên tắc ghi chú mới" ở trên). Điều phối viên không sửa nội dung. Kiểm định: `forward_refs.py` 0; `sync-local-materials.py --check` OK; Playwright (Chromium), HTTP và `file://`, 1600×900 và 390×844: 0 `.katex-error`, 0 công thức tràn, 0 lỗi console/trang, 0 yêu cầu hỏng, trang rộng 375 px ở 390 px; ảnh chụp đã xem. Các phát hiện của mục kiểm tuân thủ vẫn mở.

## Thuật ngữ "tách trọn vẹn", "tập kiểm tra" — quyết định của tác giả (2026-11-13)

Tác giả chốt "tách trọn vẹn" (shatter) thay cho "tách trọn" và "tập kiểm tra" (test set, test sample) thay cho "mẫu kiểm tra"; bảng kí hiệu vẫn ở §2, mô tả vừa đủ để danh sách giả thiết ở §2 đọc được (ghi ở `CLAUDE.md` học phần và `lec-01/van-phong-tac-gia.md` §6c). Biên tập viên (`general-purpose`, `opus`, effort `high`, theo lệnh gọi Agent) chỉ thay thuật ngữ, không đổi câu chữ khác: bài tập 73 "tách trọn vẹn"; dàn ý 45. `thuat-ngu.md` cập nhật hai hàng và thêm dòng quyết định. Điều phối viên đọc word diff: chỉ có cặp thay thế mẫu → tập, trọn → trọn vẹn; không còn thuật ngữ cũ trong `materials/` và dàn ý; số dòng `:::` như HEAD. Kiểm định: `forward_refs.py` 0; `sync-local-materials.py --check` OK; `git diff --check` sạch; Playwright (Chromium), HTTP và `file://`, 1600×900 và 390×844, mọi tệp đã đổi: 0 `.katex-error`, 0 công thức tràn, 0 lỗi console/trang, 0 yêu cầu hỏng, trang rộng 375 px ở 390 px; ảnh chụp đã xem. **Quyết định: chấp nhận.**

## Sửa ghi chú theo bảng kiểm tuân thủ — quyết định của điều phối viên: **chấp nhận** (2026-11-13)

Yêu cầu của người dùng (2026-11-13): sửa ghi chú Bài 01–10 theo các nguyên tắc ghi chú hiện hành và theo bảng phát hiện trong `reviews/kiem-nguyen-tac-2026-11-13.md`.

**Tác tử** (theo lệnh gọi Agent): người sửa `general-purpose`, mô hình `opus` (Claude Opus 5.5), effort `high`, `no-ai-slop` chế độ Edit; người kiểm lại độc lập, chỉ đọc, `general-purpose`, `opus`, effort `high`, `no-ai-slop` chế độ Detect. Mười người sửa chạy song song, mỗi người một bài, không chung tệp. Brief chung: không đánh số lại khối, không đổi con số, không sửa bốn điểm toán học trong `planning/diem-toan-can-doc-2026-11-13.md`, quyết định tác giả về §2 áp dụng.

**Kết quả của người sửa:** 86/88 hàng đã sửa; #1 đã có từ trước (dc582df); #83 chờ tác giả (khối "Quan hệ với giáo trình UML", câu hỏi chung). Không đổi số khối; thêm khối `proof` (phác thảo) cho Bổ đề 03.8 (#29). Đổi nội dung toán học ở #58, #60 (lời → công thức) và #84 (lập luận (M) ở C.1 bằng dãy $h_j\in\mathcal H_0$). Đánh lại số bước Ví dụ 03.1, 03.2, 03.4 (không chỗ nào dẫn số bước bị đổi). "mẫu" → "tập huấn luyện" ở tám chỗ chỉ $S$. `exercises.md` không đổi.

**Kiểm của điều phối viên (lượt 1):** `forward_refs.py` 0; tiêu đề khối đánh số giống HEAD; đo 390 px bằng Playwright: hai công thức tràn (Định lý 03.15(b) sau khi gộp dòng; công thức mới của #58) → yêu cầu sửa.

**Kiểm lại độc lập:** kết luận `cần sửa`; dẫn lại #58, #60, #84: đúng; xác nhận 32 hàng nghiêm trọng/trung bình đã sửa đúng, hơn 50 hàng nhẹ kiểm mẫu.

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa | quyết định |
|---|---|---|---|---|---|
| trung bình | §9 | Gán cả tỉ số cỡ mẫu $4{,}5$–$5{,}7$ lần cho hằng số 8; Ví dụ 03.10 chỉ gán thừa số $4$ trong tỉ số bán kính $4{,}25$ | `Hằng số $8$ của mẫu bóng làm cỡ mẫu theo cận VC lớn hơn … từ $4{,}5$ đến $5{,}7$ lần` | Tách hai tỉ số, gán thừa số 4 cho hằng số 8 | chấp nhận; đã sửa (điều phối viên kiểm với Ví dụ 03.10) |
| nhẹ | §7 | "cố định đối với tập huấn luyện" làm hẹp ý (đoạn sau cần cả $(S,S')$) | `cố định đối với tập huấn luyện.` | Trả lại "mẫu" | chấp nhận; đã sửa |
| nhẹ | Định lý 03.15 | "nên" sau định nghĩa | `nên $\rho_m=\rho_m(\mathcal H,\delta)$.` | "và" | chấp nhận; đã sửa |
| nhẹ | Ví dụ 03.7 | Câu "Nghĩa là" lặp số $0{,}280$ | `Nghĩa là, với xác suất ít nhất $0{,}95$ …` | Gộp thành một câu tóm lại | chấp nhận; đã sửa |
| nhẹ | §9 | "trường hợp" ba lần trong một câu | `trong trường hợp bất khả diễn và … trong trường hợp khả diễn …` | Viết lại | chấp nhận; đã sửa |
| nhẹ | `exercises.md` (Bài tập 03.1, 03.4, dòng 276) | Mô tả mục tiêu của bài tập dài hơn mục tiêu học tập đã rút gọn; "cận của bài" | `mục tiêu học tập 3, 4; cỡ mẫu đủ …` | Rút gọn | bác bỏ: mô tả trọng tâm riêng của bài tập, không phải dẫn chiếu hỏng; ngoài phạm vi lượt sửa ghi chú |
| nhẹ | Mệnh đề 03.9 | Nhãn "chứng minh đầy đủ" trong khi cận trên của (b) ở Phụ lục A | `— chứng minh đầy đủ` | Ghi độ sâu theo phần | bác bỏ: chứng minh đầy đủ có trong ghi chú (Phụ lục A); giữ như HEAD |

**Lượt sửa 2 (cùng người sửa):** bảy mục trên cùng hai công thức tràn; dòng thứ hai của công thức #58 cũng ngắt. Điều phối viên đọc lại từng chỗ trên tệp: đúng; `measure` 390 px: 0 công thức tràn; `forward_refs.py` 0; `git diff --check` sạch.

**Còn mở cho tác giả:** #83; điểm toán học 1 (UML §28.1) không đụng.

## Bộ trang chiếu (2026-11-15)

Quy định: `CLAUDE.md` § Slide decks. Khuôn bố cục: storyboard Bài 01, 02 và quyết định trong `lec-01/review-log.md` § Bộ trang chiếu.

### Tác tử (ghi từ lời gọi công cụ)

| Vai | Loại | Mô hình | Effort | Đầu ra |
|---|---|---|---|---|
| Lập storyboard | general-purpose | opus (Opus 5.5) | high | `storyboard.md` |
| Duyệt cổng storyboard | general-purpose | opus (Opus 5.5) | high | `reviews/deck-storyboard-gate.md` |
| Viết deck | general-purpose | opus (Opus 5.5) | high | `lecture-03-chieu-vc.html`, `img/lec-03/`, cập nhật `storyboard.md` |
| Duyệt: học viên | general-purpose | opus (Opus 5.5) | high | `reviews/deck-hoc-vien.md` |
| Duyệt: toán học | general-purpose | opus (Opus 5.5) | high | `reviews/deck-toan-hoc.md` |
| Duyệt: chuyên gia | general-purpose | opus (Opus 5.5) | high | `reviews/deck-chuyen-gia.md` |
| Duyệt: sư phạm, no-ai-slop Detect | general-purpose | opus (Opus 5.5) | high | `reviews/deck-su-pham.md` |
| Duyệt: mạch truyện | general-purpose | opus (Opus 5.5) | high | `reviews/deck-mach-truyen.md` |
| Sửa deck (cùng tác tử viết deck, tiếp tục bằng SendMessage) | general-purpose | opus (Opus 5.5) | high | deck, `img/lec-03/`, `storyboard.md` |
| Kiểm lại lượt 1 | general-purpose | opus (Opus 5.5) | high | `reviews/deck-kiem-lai-1.md` |
| Sửa lượt 2 (cùng tác tử viết deck) | general-purpose | opus (Opus 5.5) | high | deck, `storyboard.md` |
| Kiểm lại lượt 2 (cùng tác tử kiểm lại) | general-purpose | opus (Opus 5.5) | high | `reviews/deck-kiem-lai-2.md` |

### Quyết định của điều phối viên về storyboard và cổng duyệt

Cổng duyệt tính lại V1–V16, N1–N3 bằng Python: khớp, trừ F5 ($d=11$, $m=2\cdot10^4$: $0{,}20549\to0{,}205$) và alt F4 ($3\le m\le9$). Cổng duyệt: **đạt khi sửa** (0 chặn, 2 nghiêm trọng, 16 trung bình, 16 nhẹ). **Storyboard: chấp nhận khi sửa**; người viết deck áp dụng trực tiếp và cập nhật storyboard.

| Điểm | Quyết định | Lý do |
|---|---|---|
| Cổng, nghiêm trọng 1: 6-06 thiếu giả thiết "có ít nhất một thuật toán ERM thỏa Định nghĩa 01.4" ở Định lý 03.17(b) | yêu cầu sửa | ghi chú dòng 818; thiếu thì (2)⇒(3), (5)⇒(4) sai |
| Cổng, nghiêm trọng 2: 7-01 hàng Mệnh đề 03.9 "quy ước ≥0" | yêu cầu sửa: "hệ số tự do $b$ (bỏ: $d=p$)" | không có cơ sở trong ghi chú |
| Cổng: mật độ (6-06, 7-01 vượt trần; trang 7–8 dòng) | yêu cầu sửa: đếm bằng `deck_check.py` (số trong câu có tính; công thức hiển thị tính một dòng), tách hoặc chuyển sang ghi chú diễn giả | trần mật độ |
| Cổng: mọi phát hiện trung bình và nhẹ còn lại (lời giải 7-03 đủ hai chiều, "Nhắc lại:" cho tổ hợp lồi/conv, học PAC, khả diễn; dòng "Nhắc lại:" 02.14/02.16 đủ (T1), miền $[0,1]$, loại bảo đảm, đo được; mục 14 cập nhật theo deck 01–02 thực tế; dòng dẫn mạch 5 "trên lớp có chiều VC hữu hạn"; 2-04 không dẫn kết quả chưa phát biểu; 6-05 cơ chế định lý không có bữa trưa miễn phí theo ghi chú; 2-06 khớp số bước; bỏ câu quy trình trong ghi chú diễn giả; giảm chép ghi chú ở 2-03, 4-01, 5-01, 6-02; F5 và alt F4) | chấp nhận tất cả | — |
| Mục 11.1 thuật ngữ "tách trọn vẹn", "mẫu bóng" | chấp nhận; bản giao việc đã sửa | `thuat-ngu.md` |
| Mục 11.2 cắt còn 52 | không cắt | cổng duyệt: 4-04, 6-04 có vai trò riêng |
| Mục 11.3 ba kết quả không có trang ý tưởng chứng minh | chấp nhận: Bổ đề 03.8 công cụ chứng minh một dòng; Định lý 03.19 đọc thêm; Hệ quả 03.18 hệ quả trực tiếp | — |
| Mục 11.4 bài tập tổng hợp | Bài tập 03.1(a) trên mặt trang, lời giải đủ hai chiều; (b) ở ghi chú diễn giả | — |
| Mục 11.6 trang bài tập giữa cụm | yêu cầu sửa: thêm Bài tập 03.2(c) sau 2-06 (55 trang, trần) | quy định mỗi cụm lớn có một bài tập có lời giải trên mặt trang |
| Mục 11.10 mục tiêu | giữ ý "cận độ lệch đều" (mục tiêu 4) và "chặn bằng đa thức" (mục tiêu 2) | — |
| Mục 11.6 cũ: đổi thứ tự 3-02 (Ví dụ 03.3 Bước 1–2 trước Mệnh đề 03.9) | chấp nhận | trong cùng §5, theo hành trình ví dụ trước phát biểu, mặt trang không dùng Mệnh đề 03.9 |

**Đề xuất sửa ghi chú cho tác giả (chưa sửa):** Ví dụ 03.5 Bước 7: "$3\le m\le5$" có thể viết "$3\le m\le9$" (dạng đóng nằm trên $2^m$ với $3\le m\le9$).

### Bản nháp deck và kiểm của điều phối viên trước khi duyệt

Người viết: 55 trang (54 + trang Bài tập 03.2(c)), bảy SVG, chế độ đọc màn hẹp; áp dụng hai phát hiện nghiêm trọng của cổng duyệt và mọi phát hiện được chấp nhận; lệch storyboard ghi ở `storyboard.md` mục 16. Điều phối viên chạy `deck_check.py`: console 0, pageerrors 0, failed 0, không `.katex-error`; `footer_check.py` 0 trang; xem bảng ảnh 1600×900. **Bản nháp: chấp nhận để duyệt**; bản đóng băng trong thư mục nháp của phiên.

### Năm báo cáo duyệt và quyết định của điều phối viên

| Báo cáo | Kết luận | Chặn | Nghiêm trọng | Trung bình | Nhẹ |
|---|---|---:|---:|---:|---:|
| `reviews/deck-hoc-vien.md` | đạt khi sửa | 0 | 0 | 10 | 13 |
| `reviews/deck-toan-hoc.md` | đạt khi sửa | 0 | 0 | 3 | 8 |
| `reviews/deck-chuyen-gia.md` | đạt khi sửa | 0 | 1 | 7 | 8 |
| `reviews/deck-su-pham.md` | đạt khi sửa | 0 | 1 | 16 | 21 |
| `reviews/deck-mach-truyen.md` | đạt khi sửa | 0 | 0 | 5 | 13 |

Điều phối viên đối chiếu hai phát hiện nghiêm trọng: (1) 3-04 "Trực quan. $p+1$ hệ số $(w,b)$ đặt được dấu tùy ý tại $p+1$ đỉnh" đặt cạnh $d=11$ gợi "chiều VC = số tham số", trái Nhận xét 03.10 và mục tiêu 5: **chấp nhận**, nêu cơ chế (ma trận các hàng $(x_i^\top,1)$ khả nghịch tại các đỉnh của đơn hình); (2) ghi chú diễn giả 4-02 "Từ $m>d$, phần lớn các cách gán nhãn bị thiếu" sai ($d=3$, $m=4$: 14/16 thực hiện được): **chấp nhận**, xóa câu (toán học và sư phạm cùng thấy).

**Quyết định chung: chấp nhận mọi phát hiện**, với các điểm sau:

| Phát hiện | Quyết định | Lý do |
|---|---|---|
| 5-07 $\delta/\Pi_{\mathcal H}(2m)$ (toán học, chuyên gia) | yêu cầu sửa: $\delta/(2\Pi_{\mathcal H}(2m))$, thừa số 2 do mẫu bóng | Phụ lục C.4–C.5 |
| (M) "không bỏ được" ở 5-00, 7-01; "các lớp của bài đều thỏa (M)" ở 2-01, 5-03 | yêu cầu sửa: bỏ; theo §9 của ghi chú ((T1), (T5), chiều VC hữu hạn) và Nhận xét 03.14 (bốn lớp cụ thể) | không có cơ sở trong ghi chú |
| 6-08: cận dưới khả diễn $1/\epsilon$ đặt cạnh cận trên $1/\epsilon^2$ (chuyên gia) | yêu cầu sửa: mặt trang không ngụ ý cận trên khả diễn chặt ở $1/\epsilon^2$; ghi chú diễn giả có thể nêu cận $(d\ln(1/\epsilon)+\ln(1/\delta))/\epsilon$ với nguồn UML Định lý 6.8; đề xuất thêm câu vào ghi chú cho tác giả | cơ sở UML; ghi chú chưa có |
| 5-03, 7-04: "mẫu bóng sửa cả hai trở ngại" (chuyên gia) | yêu cầu sửa: trở ngại (ii) sửa nhờ đổi chỗ với dấu ngẫu nhiên khi biết $(S,S')$ | ghi chú §7 |
| 5-05/5-06: $\sigma_i$ và bước $\lvert L_S-L_D\rvert>\epsilon$, $\lvert L_{S'}-L_D\rvert\le\epsilon/2\Rightarrow\lvert L_{S'}-L_S\rvert>\epsilon/2$ trên mặt trang (học viên) | yêu cầu sửa | bước then chốt của ý tưởng chứng minh |
| Mật độ > 60 khi tính số trong câu (1-02, 2-03, 5-05, 5-07, 6-05, 6-06, 7-06); dòng dẫn mạch > 25 âm tiết | yêu cầu sửa: đếm bằng script, không ước lượng | quy ước đếm đã chốt |
| Lỗi đã sửa ở deck 02 quay lại (1-02 "ERM:", "PAC:"; câu quy trình ở ghi chú diễn giả 1-03, 7-00, 7-05; "Nhắc lại:" cho học PAC, khả diễn, Định nghĩa 01.4, (O1)/(O2), đảo cận đuôi) | yêu cầu sửa | bài học trong `common-brief.md` |
| Đề xuất sửa ghi chú | ghi cho tác giả: (1) tên "đối xứng hóa (symmetrization)" trong chứng minh Định lý 03.15; (2) câu về khoảng cách cận trên/cận dưới khả diễn (UML §6.4, §28.3); (3) §7 nói rõ trở ngại (ii) sửa ở Bước 3; (4) §9 dòng 890 thêm $1\le d\le m$; (5) Ví dụ 03.5 Bước 7 "$3\le m\le9$"; (6) "dạng đóng" dùng cho hai đối tượng khác nhau | chưa sửa |

### Sửa sau năm báo cáo

Người sửa: mọi phát hiện nghiêm trọng và trung bình đã sửa; vài phát hiện nhẹ sửa một phần hoặc không sửa có lý do (`storyboard.md` mục 17). `deck_lint.py` 23 → 0; `footer_check.py` 0; `deck_check.py` sạch. Nhắc lại Hệ quả 02.16 chuyển từ 1-02 sang 6-02. Chuyển sang kiểm lại độc lập.

### Kiểm lại lượt 1 và quyết định

`reviews/deck-kiem-lai-1.md`: **đạt khi sửa**; hai phát hiện nghiêm trọng và các quyết định riêng đã sửa đúng; Hệ quả 02.16 không bị dùng trước 6-02; toán đúng trên trang đổi; `deck_lint.py` 0, `footer_check.py` 0. Các mục "không sửa" chấp nhận. Còn mở 2 trung bình (N1 5-03 dùng "mẫu bóng" trước 5-05; N13 7-02 dòng Định lý 03.15 thiếu (M), hàm lỗi 0–1) và 15 nhẹ. **Quyết định: yêu cầu sửa tất cả** (lượt sửa 2). Chữ trong hình ở 390 px: giới hạn chung, giảm nhẹ bằng việc cho phép phóng to (commit 068d9cc); không thêm CSS.

### Kiểm lại lượt 2 và quyết định

`reviews/deck-kiem-lai-2.md`: **đạt**; N1–N17 sửa đúng; `deck_lint.py` 0, `footer_check.py` 0, `deck_check.py` sạch. Còn 3 nhẹ: M1 2-01 "(countable subclass)" gắn sai chỗ; M2 5-06 "Kỹ thuật." mất "$S'\sim D^m$ độc lập"; M3 7-02 mất "bảo đảm cho lớp". **Quyết định:** sửa cả ba (lượt sửa 3, vài dòng; điều phối viên đọc diff).

### Sửa lượt 3 và kiểm cuối của điều phối viên — chấp nhận (2026-11-16)

Lượt 3: M1 2-01 khôi phục "lớp con đếm được (countable subclass) $\mathcal H_0$"; M2 5-06 giữ "$S'\sim D^m$ độc lập"; M3 7-02 "Bảo đảm cho lớp, mọi $h$ cùng lúc". Điều phối viên đọc diff ba trang: đúng yêu cầu, không đổi nội dung toán.

**Kiểm cuối (điều phối viên tự chạy):** `deck_check.py --shots` 55 trang: console 0, pageerrors 0, failed 0, `.katex-error` 0; OVERFLOW chỉ ở đuôi `\sqrt`; ở 390 px `docScrollW` tối đa 390. `footer_check.py` 0; `deck_lint.py` 0. Ảnh 1600×900 và 390×844 đã xem (bảng ảnh). Bàn phím →, ↓, Space, Esc đúng; sáu liên kết `#/2`…`#/7` tới `L03-2-00`…`L03-7-00`. Trang chỉ mục: thẻ Bài 03 liên kết deck; ghi chú và bài tập mở kèm `&deck=`, 0 `.katex-error`, 0 lỗi tải. Deck Bài 02 trang 7-06: "Bài 03" thành liên kết (cơ học, đã kiểm).

**Kết luận của điều phối viên: chấp nhận deck Bài 03.** Giới hạn còn lại: chữ trong F4, F7 ≈ 11 px ở 390 px (cho phép phóng to). Đề xuất sửa ghi chú cho tác giả: các mục ở bảng quyết định (đối xứng hóa, khoảng cách cận khả diễn, trở ngại (ii), $1\le d\le m$, Ví dụ 03.5 Bước 7, "dạng đóng" hai nghĩa).

## Sửa ghi chú theo đề xuất (2026-11-16)

Yêu cầu của tác giả (2026-11-16): "carry out proposed changes to the notes" — thực hiện các đề xuất sửa ghi chú/bài tập ghi ở mục "Bộ trang chiếu". Điều phối viên kiểm lại từng đề xuất trước khi giao; đề xuất "tùy tác giả" chỉ làm khi sửa một điểm sai hoặc lệch; deck nào dẫn chỗ đã đổi thì sửa theo để giữ thống nhất.

**Tác tử (theo lệnh gọi Agent):** biên tập viên Bài 03–04 và người kiểm lại Bài 03–04, cả hai `general-purpose`, `opus`, effort `high`; brief ở scratchpad phiên (`notefix/brief-editor.md`, `brief-recheck.md`). Biên tập viên dùng `no-ai-slop` Edit, người kiểm lại dùng Detect.

| Đề xuất | Quyết định | Lý do |
|---|---|---|
| (1) tên "đối xứng hóa" | chấp nhận: "Bước 1 và Bước 2 tạo thành phép *đối xứng hóa* (symmetrization)." | |
| (2) khoảng cách cận trên/dưới khả diễn | chấp nhận: đoạn mới sau Định lý 03.19, dẫn UML §6.4 (Định lý 6.8, tr. 72–73) và §28.3 (Định lý 28.4, tr. 398–401), "dưới (M)" | đã đối chiếu PDF; deck 6-08 đã có ý này |
| (3) §7 trở ngại (ii) | chấp nhận: "Cách sửa trở ngại (i) …", câu sửa trở ngại (ii) bằng đổi chỗ (swapping); "lý do (i), (ii)" → "trở ngại (i), (ii)" ở ghi chú, `exercises.md`, ghi chú diễn giả 7-04 | không viết "ở Bước 3" (điều hướng tới sau) |
| (4) §9 điều kiện của $d\ln(2em/d)$ | chấp nhận, sửa thành $1\le d\le2m$ (đề xuất gốc $1\le d\le m$) | đúng điều kiện Bổ đề 03.12(b) tại $2m$ điểm; khớp deck 7-02 |
| (5) Ví dụ 03.5 Bước 7 | chấp nhận: $3\le m\le9$, kèm $542{,}31>512$, $743{,}91<1024$ | điều phối viên tính lại; đổi tên bước: bác |
| (6) "dạng đóng" hai nghĩa | chấp nhận: "dạng đóng" chỉ $(em/d)^d$; bước tính $M(\epsilon,\delta)$ gọi "cỡ mẫu $M(\epsilon,\delta)$" ở ghi chú, `exercises.md`, deck 6-03, `outline.md`, `storyboard.md` | |

**Kiểm lại:** lượt 1 "đạt khi sửa" (câu UML thiếu (M), văn bản làm chủ ngữ, "(swapping)" ở lần dùng thứ hai, "lý do"/"trở ngại"), lượt 2 **đạt**. `forward_refs.py` 0; `deck_lint.py` 0.

**Kiểm cuối (điều phối viên tự chạy, 2026-11-16):** `forward_refs.py` 0; `deck_lint.py` không phát hiện mới (chỉ ngoại lệ đã ghi); `deck_check.py --shots` trên các trang deck đã đổi: console 0, pageerrors 0, failed 0, không `.katex-error`; `footer_check.py` 0; ảnh 1600×900 và 390×844 (cuộn tới cuối) của mọi trang đổi đã xem; trình xem ghi chú và bài tập qua HTTP (1600×900, 390×844), `file://` (390×844) và in: 0 `.katex-error`, 0 lỗi console, 0 yêu cầu lỗi, 0 công thức tràn, trang không cuộn ngang; `material-local-data.js` đồng bộ. **Kết luận: chấp nhận; commit và push.**
