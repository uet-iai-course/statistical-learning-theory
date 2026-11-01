# Nhật ký rà soát — Bài 02: Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn

Tệp nội bộ. Ghi tác tử, quyết định của điều phối viên, phát hiện rà soát và nguồn đã tham khảo.

Căn cứ bắt đầu (2026-10-30): người dùng giao soạn ghi chú Bài 02 theo blueprint sau ba vòng duyệt thí điểm Bài 01. Các yêu cầu rút ra từ thí điểm áp dụng ngay từ bản thảo: định nghĩa trước khi dùng (`forward_refs.py` báo 0), khối nhiều thành phần viết thành danh sách có nhãn song song (`van-phong.md` §3a), câu thẳng (§9a), "với xác suất ít nhất", thuật toán tất định $A(S)$.

**Người dùng (2026-10-30):** "ghi thêm nguyên tắc viết ví dụ: ví dụ không được quá nhanh, phải diễn giải từng bước, sử dụng xuống dòng để trình bày rõ ràng hơn, không viết díu vào nhau trong 1 đoạn văn quá nhiều ý." **Quyết định:** thêm `van-phong.md` §7a (một bước một ý; xuống dòng, nhãn bước in đậm hoặc danh sách đánh số; công thức hiển thị và `aligned` cho phép tính nhiều bước; không bỏ bước trung gian; câu diễn giải sau con số), mở rộng mục 8 của danh sách kiểm tra §14, thêm một dòng vào `CLAUDE.md` của học phần (áp dụng cả cho lời giải bài tập). Áp dụng cho mọi ví dụ của Bài 02 từ dàn ý và bản thảo; người rà học thuật–sư phạm kiểm tra theo §7a.

## Tác tử

| Bước | Vai trò | Loại | Mô hình | Mức | Bằng chứng |
|---|---|---|---|---|---|
| 2026-10-30 · 1 | Phân tích nguồn UML (chỉ ghi `source-analysis.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 2 | Lập dàn ý (ghi `outline.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 3 | Soạn ghi chú (ghi `lecture-note.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 4 | Năm lượt rà độc lập (học viên; chính xác toán học; chuyên gia và trung thành nguồn; học thuật–sư phạm và `no-ai-slop` Detect; mạch và móc nối), chỉ đọc | general-purpose ×5 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 5 | Biên tập vòng 1 (cùng người viết, ghi `lecture-note.md`, `bien-tap-vong-1.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-30 · 6 | Rà lại: toán học trên phần đã sửa; mạch, văn phong trên phần đã sửa và ranh giới mục (chỉ đọc) | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 7 | Biên tập vòng 2 (cùng biên tập viên) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-30 · 8 | Rà lại vòng 2: toán, mạch, văn phong trên phần đã sửa (chỉ đọc) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 9 | Biên tập vòng 3 và sửa công thức có chữ tiếng Việt (cùng biên tập viên) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-30 · 10 | Rà lại vòng 3 (cùng người rà lại vòng 2, chỉ đọc) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-30 · 11 | Soạn bài tập (ghi `exercises.md`, `bai-tap-ghi-chu.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 12 | Rà bài tập: toán học; sư phạm và `no-ai-slop` Detect (chỉ đọc) | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 13 | Sửa bài tập theo hai lượt rà (cùng người soạn; ghi `exercises.md`, hai dòng §10 của ghi chú) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-30 · 14 | Rà lại bài tập: toán; sư phạm (cùng hai người rà, chỉ đọc) | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |

## Phân tích nguồn — quyết định của điều phối viên: **chấp nhận** (2026-10-30)

Báo cáo `source-analysis.md` (142 dòng). Điều phối viên tính lại độc lập: bảng thực đơn hữu hạn với $\delta=0{,}05$ ($K=1$: 738/185, 2952/738, 60/30; $K=100$: 1659/415, 6636/1659, 153/77; $K=1000$: 2120/530, 8478/2120, 199/100); bán kính câu hỏi mở đầu ở $m=1000$ ($0{,}0429$; $0{,}0728$ với $K=1000$; $0{,}0781$ với $K=5000$); $\Pr[\mathrm{Bin}(1000;0{,}07)\le50]=0{,}00593$ và $1-(1-0{,}00593)^{1000}=0{,}9974$; xác suất đuôi chính xác của $L_S(h_3)$ dưới $D_\eta$ ($0{,}6189$; $0{,}0109$; $4{,}9\cdot10^{-4}$ ở $m=6,100,200$) cùng cận Hoeffding và Chebyshev; ERM trên $\mathcal M_{\mathcal X}$: $1431$; lớp hàm ngưỡng bất khả tri $1097$, khả thực $48$; phản ví dụ (a) $2e^{-8}=6{,}7\cdot10^{-4}$, (b) $0{,}9900$, (c) $0{,}6236$, $0{,}9924$, $2e^{-3{,}2}=0{,}0815$; UML 3.4 với $p=10$: $140$; UML 2.3: $176$. Tất cả đúng. Hằng số của blueprint đúng; ghi chú viết $\ln$.

Quyết định cho dàn ý và bản thảo:

1. Dùng lại ví dụ sàng lọc của Bài 01 ($\mathcal X=\{1,\dots,5\}$, lớp sáu hàm ngưỡng, $D_\eta$, $D_f$, $\mathcal M_{\mathcal X}$); đã sửa dòng tương ứng trong `ky-hieu.md` (Bài 01–02). Ứng dụng thực tế: thực đơn hữu hạn $K$ bộ phân lớp đánh giá trên một mẫu kiểm định (câu hỏi mở đầu, blueprint §2.4).
2. Bất đẳng thức Hoeffding giữ vai trò **Định lý** (công cụ chính của bài theo bản đồ học phần), phát biểu một phía và hai phía, sự kiện "$\ge\epsilon$"; miền $[a_i,b_i]$ khác nhau ở một nhận xét. Markov, Chebyshev, phương pháp Chernoff, bất đẳng thức hợp là **Bổ đề** có số (được dẫn về sau). Bổ đề Hoeffding [S]: bước lồi trong thân bài, bất đẳng thức vô hướng $L(u)\le u^2/8$ chứng minh ở Phụ lục.
3. Thứ tự theo quy tắc định nghĩa trước khi dùng: cận tin cậy sau Hoeffding; sự kiện hội tụ đều (mẫu $\epsilon$-đại diện) sau bất đẳng thức hợp. Tính chất hội tụ đều của lớp ($m^{UC}$) để Bài 03.
4. Hệ quả ERM phát biểu cho **mọi** nghiệm ERM (mọi quy tắc chọn khi bằng nhau), kèm ERM xấp xỉ ($2r_m+\epsilon_{\mathrm{opt}}$), viết lại bằng ngôn ngữ Định nghĩa 01.25 với $M(\epsilon,\delta)=\lceil2\ln(2\lvert\mathcal H\rvert/\delta)/\epsilon^2\rceil$.
5. Thực hiện ba lời hứa của Bài 01 mà blueprint không ghi: (i) ERM trên $\mathcal M_{\mathcal X}$ với $\mathcal X$ hữu hạn đạt rủi ro Bayes cộng $\epsilon$ (ví dụ số $1431$); (ii) một câu: với lớp hữu hạn, $\beta(m,\delta)=r_m$ là cận của Định nghĩa 01.28, đối lập với Hệ quả 01.29; (iii) so sánh ba mức trong trường hợp khả thực: cận lớp hữu hạn $48$, cận riêng lớp hàm ngưỡng $30$, giá trị riêng $A_{\max}$ và $D_f$ là $14$.
6. Mệnh đề khả thực: nói rõ cận cho từng giả thuyết không dùng tính khả thực; tính khả thực chỉ bảo đảm $L_S(\hat h)=0$ cho mọi nghiệm ERM.
7. Phản ví dụ bỏ giả thiết trong ghi chú: (a) bỏ độc lập (một hồ sơ chép $m$ lần, nối với câu hỏi ôn nhanh 2 của Bài 01) và (b) bỏ tính bị chặn (một nhận xét ngắn có số, thực hiện lời hứa về hàm lỗi bình phương và hàm lỗi log). Phản ví dụ (c) (bất đẳng thức hợp bỏ $\lvert\mathcal H\rvert$) dành cho bài tập gốc 4; ghi chú có thể dùng ví dụ thiên lệch do chọn (1000 ứng viên rủi ro $7\%$) ở phần câu hỏi mở đầu hoặc sau Định lý hội tụ đều, nếu độ dài cho phép.
8. Nhận xét tinh chỉnh $\ln((\lvert\mathcal H\rvert+1)/\delta)$: không đưa vào ghi chú; để làm ý thử thách của bài tập gốc 3.
9. Bài tập UML chọn: 4.1, 4.2 (phát biểu với hàm lỗi có trọng số $\ell_c\in[0,4]$), 2.3 ý 1–2, 3.4, 3.5. Bài gốc 2 (Hoeffding một phía) đổi thành Hoeffding với miền $[a_i,b_i]$ khác nhau hoặc cận tin cậy một phía, vì ghi chú đã chứng minh đầy đủ bản một phía. Bài gốc 5 (mô phỏng) chỉ mô tả giao thức. Ghi các chỗ hổng của bản lời giải (2.3 khi $D$ có nguyên tử và mẫu không có điểm dương; 3.4 bỏ "+1"; 4.1 "$\le\delta$"; 4.2 sai số mũ).
10. Không nói $1/\epsilon^2$ là cần thiết (cận dưới để sau); Bernstein [O] chỉ trỏ tới UML B.5. Mục tiêu độ dài thân bài ≤ 11 000 tiếng, phụ lục ≤ 1 500.

## Dàn ý — quyết định của điều phối viên: **chấp nhận có sửa** (2026-10-30)

`outline.md` 391 dòng: 18 khối đánh số (02.1–02.18; Bổ đề 02.6 = Lemma 2.1, Định lý 02.7 = Theorem 2.2, Định lý 02.14 = Theorem 2.3, Hệ quả 02.16 = Corollary 2.4, Mệnh đề 02.17 = Proposition 2.5), Ví dụ 02.1–02.12, Bài tập 02.1–02.11. Điều phối viên đọc toàn bộ và tính lại mọi con số †: $0{,}5391$; $0{,}6189$; $0{,}3937$, $0{,}0134$, $6{,}9\cdot10^{-4}$; $8{,}94\cdot10^{-4}$; $1{,}1059\le1{,}1331$; $0{,}0887$, $0{,}1204$, $0{,}1259$; $(1+3e^{2})/4$ (cấu trúc XOR); $1523$; $334$. Đúng, trừ một chỗ.

Quyết định:

1. **Sửa số:** xác suất đuôi hai phía chính xác ở $m=100$ là $0{,}02115$, viết $0{,}0211$ (dàn ý ghi $0{,}0212$) ở mọi nơi (Ví dụ 02.2, 02.4, §9, Phụ lục B.1, Bài tập 02.5).
2. **Chấp nhận năm sai khác:** biến cố "$\ge$" với giá trị chính xác mới; Định lý 02.7(c) dùng tính rời nhau, không dùng bất đẳng thức hợp; Ví dụ 02.7 so xác suất chính xác, không dùng khoảng chuẩn; Định lý 02.7 trên $[a,b]$ và Định lý 02.14(b) một phía; Bài tập 02.1 kiểm tra giả thiết yếu hơn.
3. **Ví dụ 02.9 bước (5):** bỏ câu "đúng ở biên" (ở $m=6$ không có bảo đảm nào). Thay bằng: ở $m=6$, $r_6=\sqrt{\ln240/12}\approx0{,}676$, nên $2r_6>1$ và cận vô nghĩa; điều đó giải thích vì sao Ví dụ 01.6 có thể trả về $h_2$.
4. **Điểm mở:** (1) tham số mũ $\tau$; (2) chốt "mẫu xác thực" (đã ghi `thuat-ngu.md`); (3) dùng kí hiệu $r_m^{+}$; (4) "literal" quyết định ở bước bài tập; (5) giữ Ví dụ 02.7 trong thân bài, là phần cắt đầu tiên nếu vượt độ dài.
5. **Độ dài:** thân bài ≤ 12 000 tiếng (`wc -w`), phụ lục ≤ 1 500 — nới từ 11 000 vì văn phong từng bước của §7a (Bài 01 tăng khoảng 6% khi áp dụng); thứ tự cắt theo dàn ý §11.2.
6. Đã thêm 18 thuật ngữ vào `thuat-ngu.md` §6 và chốt "mẫu xác thực".

## Bản thảo ghi chú — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-30)

Bản thảo 1081 dòng; thân bài 11 220 tiếng (`wc -w`, trần 12 000), phụ lục 444. 18 khối đánh số 02.1–02.18, Ví dụ 02.1–02.12, một khối ứng dụng, §10 liệt kê Bài tập 02.1–02.11. Điều phối viên đọc phần mở đầu đến §4 và toàn bộ Định lý 02.7, Nhận xét 02.8, Định nghĩa 02.9, Hệ quả 02.10 cùng chứng minh: khớp dàn ý và quyết định. Kiểm tra do điều phối viên chạy: Playwright 390 px (trang 375 px, `scrollX` 0) và 1600 px: 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng; `sync --check` OK. Chấp nhận bảy sai khác người viết báo (câu hỏi mở đầu là đoạn văn; $r$, $r^{+}$ cục bộ trong Hệ quả 02.10; $a<b$ trong Bổ đề 02.6; ngắt công thức cho 390 px; câu chính xác hơn ở Nhận xét 02.11; lý do khoảng cách 48/30 ở Ví dụ 02.11).

**Công cụ:** `forward_refs.py` chỉ dò mẫu `01.x`. Điều phối viên sửa để lấy số bài từ đường dẫn (`lec-NN`); thử chèn một tham chiếu tới trước vào bản sao thì công cụ báo 1; Bài 01 và Bài 02 báo 0. Bản đóng băng cho rà soát: scratchpad `lec02-draft-frozen.md`.

## Năm lượt rà — quyết định của điều phối viên: **yêu cầu sửa** (2026-10-30)

Báo cáo trong `reviews/1-hoc-vien.md`, `2-toan-hoc.md`, `3-chuyen-gia-nguon.md`, `4-hoc-thuat-van-phong.md`, `5-mach.md`. Không có lỗi chặn bàn giao. Rà soát toán học xác nhận mọi phát biểu, chứng minh và khoảng 120 con số. Năm phát hiện nghiêm trọng sau khi gộp trùng: phạm vi của các cỡ mẫu khả thực $48/30/14$ (thêm $37$ cho mọi nghiệm ERM trên lớp hàm ngưỡng; rà soát 2, 3); hàng $K=1$ của Ví dụ 02.12 (1, 2, 3); §6–§8 kết bằng khối (5); liệt kê sớm $D_f$, $\mathcal M_{\mathcal X}$, $\ell_c$ ở Ví dụ 02.1 (4, 5); Ví dụ 02.4 Bước 4 trái §7a (4, 5). Điều phối viên tính lại $37$, $185$, $381$, $500$, $25\,000$ và điểm cắt $m\le107$ (cả hai cận còn trên khoảng $0{,}23$). **Quyết định:** `reviews/0-quyet-dinh.md` (N1–N5, M1–M16; chấp nhận các điểm nhẹ trừ ba ngoại lệ có lý do). Giao người viết làm biên tập viên (tiếp tục bằng `SendMessage`).

## Biên tập vòng 1 — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-30)

Biên tập viên áp dụng N1–N5, M1–M16 và các điểm nhẹ (danh sách ở `bien-tap-vong-1.md`); chưa áp dụng gợi ý AM–GM (để bước bài tập). Thân bài 11 997 tiếng, phụ lục 580; cắt thêm cột $m=6$ của Ví dụ 02.4 (thứ tự cắt 4 của dàn ý), phép kiểm số của Bổ đề 02.6, rút Nhận xét 02.8. Không đổi số khối, ví dụ, bài tập; mục tiêu 4 tách hai nên mục tiêu cũ 5 thành 6; Ví dụ 02.11 đổi tên "Bốn mức cỡ mẫu…"; thêm Phụ lục C (tính đo được). Điều phối viên đọc Ví dụ 02.11, ba câu kết §6–§8, hàng $K=1$: đúng quyết định. **Phát hiện của điều phối viên:** câu kết luận Ví dụ 02.11 "Bốn cỡ … trả lời cùng một câu hỏi" trái với Bước 5 — sửa ở vòng sau. Diff vòng 1 ở scratchpad `lec02-round1.diff`. Chuyển hai lượt rà lại.

## Rà lại sau vòng 1 — quyết định của điều phối viên: **yêu cầu sửa nhỏ** (2026-10-30)

Rà lại toán (`reviews/6-ra-lai-toan.md`): không lỗi chặn bàn giao hay nghiêm trọng; 10/10 phát hiện của rà soát 2 đã xử lý; mọi con số mới đúng ($37$ với cận chính xác $2\cdot0{,}9^{37}-0{,}8^{37}=0{,}0403$; $185$, $381$, $500$, $25\,000$; giao nhau Chebyshev–Hoeffding đúng khi $18\le m\le107$); một trung bình (câu kết §5 về Nhận xét 02.11), sáu nhẹ. Rà lại mạch (`reviews/7-ra-lai-mach.md`): N1–N5, M1–M16 đã áp dụng, N4 và M14 một phần; ba trung bình (câu kết §8 quá rộng; $\mathcal M_{\mathcal X}$ chưa gọi tên ở Nhận xét 02.15; cách dẫn Định nghĩa 02.9 cho $\hat h$), các điểm nhẹ. Điều phối viên đối chiếu từng mục trung bình với văn bản: đúng. Phát hiện của điều phối viên về câu kết Ví dụ 02.11 trùng một điểm nhẹ của rà soát 7 (rà soát 6 cho câu đó đúng; điều phối viên giữ yêu cầu sửa vì câu mâu thuẫn Bước 5). **Quyết định:** chấp nhận cả bốn trung bình và mọi điểm nhẹ; giao biên tập viên vòng 2.

## Biên tập vòng 2 — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-30)

Biên tập viên áp dụng năm mục trung bình và mọi điểm nhẹ (`bien-tap-vong-1.md`, mục "Vòng 2"); thân bài 11 994 tiếng, phụ lục 603; không đổi số hiệu; Bài tập 02.8 đo mục tiêu 4, 5 (người viết bài tập phải thêm phần so sánh cỡ mẫu khả thực và bất khả tri). Con số mới duy nhất: phép kiểm tại $m=107$, $108$. Cắt lặp: đoạn cuối §9 về lớp vô hạn (đã có ở §11), câu §9 về hàm lỗi bình phương và log (đã có ở Nhận xét 02.11), câu thứ hai sau $\square$ của Bổ đề 02.2, dòng "Kí hiệu" của danh sách UML, ví dụ $h_5$/$h_4$ ở Ví dụ 02.11 Bước 6. Điều phối viên đọc toàn bộ diff vòng 2 (`lec02-round2.diff`): đúng các quyết định. Chuyển một lượt rà lại kết hợp.

## Rà lại vòng 2, biên tập vòng 3 — quyết định của điều phối viên: **chấp nhận** (2026-10-30)

Rà lại vòng 2 (`reviews/8-ra-lai-vong-2.md`): mọi phát hiện của rà soát 6, 7 đã xử lý; giao được; một trung bình (câu kết §5: thiếu "tiến về $0$") và mười hai nhẹ. Điều phối viên chấp nhận tất cả (riêng ghi chú về Bài tập 02.8 chuyển cho bước bài tập). Biên tập vòng 3 áp dụng đủ; điều phối viên đọc diff (`lec02-round3.diff`): đúng từng đề xuất. Người rà lại vòng 2 xác nhận diff vòng 3: giao được. Thân bài 11 999 tiếng, phụ lục 622.

## Kiểm định cuối và công bố ghi chú — Bài 02 (2026-10-30)

Kiểm định do điều phối viên chạy (Playwright, Chromium): qua HTTP và `file://`, ở 1600×900 và 390×844: 1395 công thức, 0 `.katex-error`, 0 công thức hiển thị tràn khung, 0 lỗi trang, 0 yêu cầu hỏng, không khối `:::` hay `$$` chưa hiển thị, trang rộng 375 px ở 390 px (không cuộn ngang). Cảnh báo KaTeX "Unrecognized Unicode character ạ/ệ" (do `\text{… đại diện}` trong chứng minh Định lý 02.14) đã sửa bằng biến cố viết thuần kí hiệu, giờ 0 cảnh báo. Thông báo CSP chỉ có qua HTTP, do đoạn script tải lại tự động mà máy chủ xem trước chèn vào, không có qua `file://`. In PDF A4: 44 trang. Điều phối viên xem ảnh chụp phần đầu ở 390 px và 1600 px, Ví dụ 02.12 ở 390 px: hiển thị đúng. `sync --check` OK; `forward_refs.py` 0; `git diff --check` sạch. `outline.md` có ghi chú trạng thái cuối. Thẻ Bài 02 của `2627-1/index.html` liên kết ghi chú; "Bài tập" vẫn "Chưa có" (soạn sau khi ghi chú qua rà soát, theo quy trình).

**Trạng thái:** ghi chú Bài 02 hoàn tất, commit và push. Việc tiếp theo: bài tập (`exercises.md`), theo `outline.md` mục 4 và các ghi chú trong `bien-tap-vong-1.md`.

## Nguồn đã tham khảo

UML (trang PDF): 37–42 (§2.3, §2.3.1, Bài tập 2.1–2.3), 50–52 (§3.5, Bài tập 3.1–3.9), 54–59 (§4.1–4.5, Bài tập 4.1–4.2), 422–428 (Phụ lục B.1–B.7). Bản lời giải: tr. 1–6, 9–10, chỉ để kiểm tra độ khó và chỗ thiếu của bài tập đề xuất.

## Bài tập — bắt đầu (2026-10-30)

**Người dùng:** "Làm bài tập đi". Giao một người viết soạn `exercises.md` theo `outline.md` mục 4, ghi chú trạng thái cuối, `bien-tap-vong-1.md` (Bài tập 02.8 đo thêm mục tiêu 5; 02.4 mục tiêu 6; AM–GM vào gợi ý 02.9) và QĐ 8–9; lời giải theo §7a; bài UML tự giải trước rồi mới đối chiếu bản lời giải. Sau đó hai lượt rà độc lập (toán; sư phạm–văn phong).

## Bài tập — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-30)

`exercises.md`: 11 bài (02.1–02.6 gốc; 02.7–02.11 là UML 2.3 ý 1–2, 3.4, 3.5, 4.1, 4.2, số bài đã đối chiếu PDF), 10 044 từ (`wc -w`), vượt mục tiêu 8 000–9 000 (người viết: do lời giải từng bước và công thức tách dòng cho 390 px; người rà sư phạm đề xuất chỗ cắt). Người viết tự giải trước rồi mới đối chiếu bản lời giải; xử lý chỗ hổng ở 2.3, 3.4, 4.1, 4.2 (ghi trong `bai-tap-ghi-chu.md`). Điều phối viên tính lại: $2\ln(2\cdot59050/0{,}05)/0{,}01\to2936$; $\epsilon=0{,}05$: $11\,741$ và $280$; bán kính $0{,}0468$, $0{,}0729$, $0{,}1106$ (trọng số $2^{-k}$, $k=1,10,30$); $22/1024$; sai số chuẩn tương đối $33\%$ ở $R=10^4$, $m=200$ và $R\ge1{,}12\cdot10^5$ cho $10\%$: đúng. **Thuật ngữ:** không dùng "tục biến" (không có nguồn); literal viết "biến hoặc phủ định của biến (literal)"; thêm "sai số chuẩn", "hạt giống ngẫu nhiên" vào `thuat-ngu.md` §6. Bản đóng băng: scratchpad `lec02-ex-frozen.md`. Chuyển hai lượt rà.

## Rà bài tập — quyết định của điều phối viên: **yêu cầu sửa** (2026-10-30)

Rà toán (`reviews/9-bai-tap-toan.md`): không lỗi chặn bàn giao; 10/11 bài đúng mọi con số; một nghiêm trọng (02.1(d)–(e): ở $\tau=1$ hàm sinh mô-men của tổng nhỏ hơn tích, đúng chiều chứng minh đuôi trên cần; chỉ đuôi dưới hỏng), một trung bình (02.10(c) hai cách hiểu), mười nhẹ. Rà sư phạm (`reviews/10-bai-tap-su-pham.md`): một chặn bàn giao ("tục biến" 14 lần), một nghiêm trọng (vế cận và khoảng tin cậy của mục tiêu 2 không có bài đo), bốn trung bình, các nhẹ và chỗ cắt khoảng 600–700 tiếng. Điều phối viên tính lại $(x-1)^3/8$, giá trị tại $\tau=\pm1$ và $\tfrac14>e^{-1{,}5}$: đúng. **Quyết định:** `reviews/11-quyet-dinh-bai-tap.md` (B1–B3, T1–T5, mọi điểm nhẹ; đích ≤ 9 500 tiếng). Điều phối viên sửa `outline.md` §4 (02.4 → mục tiêu 6). Giao người soạn sửa, gồm hai dòng §10 của ghi chú (02.2 mục tiêu 1, 2; 02.10 mục tiêu 1, 6).

## Sửa bài tập — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-30)

Người soạn áp dụng B1–B3, T1–T4 và các điểm nhẹ; T5 xóa hẳn phần mở rộng $\mathbb R^p$ (không thêm "Câu hỏi:") để giữ độ dài — chấp nhận; bỏ ví dụ $R=2\cdot10^5$ ở 02.5(b) — chấp nhận; 02.1 thêm ý (e) mới nên ý cũ (e) thành (f). `exercises.md` 9 498 tiếng; 0 lần "tục biến". Ghi chú: chỉ §10 đổi (02.2 "mục tiêu 1, 2"; 02.10 "mục tiêu 1, 6"; bỏ "học tập" ở câu dẫn để thân bài giữ 11 999). Điều phối viên tính lại 02.2(d): $r^{+}=0{,}0612$, $r=0{,}0679$ ($C=2500$), $0{,}1548$, $0{,}1718$ ($C=16\,000$); và kiểm bằng numpy float32: phép thử $\lvert k/m-0{,}22\rvert\ge0{,}1$ sai tại $k=32$ ($m=100$) và $k=64$ ($m=200$), đúng tại $12$, $24$ — khớp câu của người soạn (khác ghi nhận của rà soát 9, vì kết quả phụ thuộc cách tính). Diff ở scratchpad `lec02-ex-round1.diff`. Gửi lại hai người rà.

## Rà lại bài tập — quyết định của điều phối viên: **chấp nhận, sửa nhẹ** (2026-10-30)

Rà lại toán: không lỗi chặn bàn giao hay nghiêm trọng; mọi con số mới đúng ($(x-1)^3/8$; $\tau=\pm1$; $\tfrac14>e^{-1{,}5}$; $0{,}0612$, $0{,}0679$, $0{,}1548$, $0{,}1718$; $2r'(1523)=0{,}099973$; $40\,001$, $10^8+1$, $160\,000$; $0{,}0999973$ / $0{,}10000013$); người rà tự đính chính giá trị biên float32 ($k=32$, $64$, khớp kiểm tra của điều phối viên); mọi phát hiện trước ✓; một điểm nhẹ (02.2(b) câu so sánh số mũ đọc ngược). Rà lại sư phạm: B1, B2, B3, T2–T5 ✓; đủ 6/6 mục tiêu (2: 02.2(d) bắt buộc, 02.1(f), 02.4(a), 02.5); 9 498 tiếng; ba điểm nhẹ (§9a ở 02.1(f), 02.8(d); chọn $R$ cụ thể ở 02.5(b); thuật ngữ "độ chính xác đơn"). Cả hai: giao được. **Quyết định:** chấp nhận bốn điểm nhẹ, giao người soạn sửa; không cần rà lại thêm (sửa câu chữ, không đổi toán), điều phối viên đọc diff.

## Kiểm định cuối và công bố bài tập — Bài 02 (2026-10-30)

Người soạn sửa bốn điểm nhẹ cuối (02.2(b) so sánh số mũ viết tường minh; §9a ở 02.1(f), 02.8(d); "Chọn chẳng hạn $R=1{,}2\cdot10^5$" ở 02.5(b); "số dấu phẩy động độ chính xác đơn (single precision)"); điều phối viên kiểm từng chỗ trên văn bản. `exercises.md` 9 489 tiếng (đích ≤ 9 500); 0 "tục biến". Kiểm định do điều phối viên chạy (Playwright, Chromium), qua HTTP và `file://`, 1600×900 và 390×844: 43 khối gợi ý/lời giải thu gọn mặc định; mở hết: 1242 công thức, 0 `.katex-error`, 0 cảnh báo KaTeX, 0 công thức tràn, 0 lỗi trang, 0 yêu cầu hỏng, trang rộng 375 px ở 390 px; in PDF A4 39 trang; ảnh chụp 390 px đã xem. Ghi chú sau khi sửa §10: 0 `.katex-error`, không cuộn ngang. `sync --check` OK; `forward_refs.py` 0; `git diff --check` sạch. Thẻ Bài 02 của `2627-1/index.html` liên kết bài tập; bấm từ trang chỉ mục mở đúng tệp qua HTTP và `file://`.

**Trạng thái:** Bài 02 (ghi chú và bài tập) hoàn tất; commit và push.

## Sửa ghi chú theo văn phong tác giả (sau bản sửa tay Bài 01) — Bài 02 (2026-11-01)

**Ngoại lệ quy trình do người dùng quyết định (2026-11-01):** vì hạn mức Claude gần hết, người dùng yêu cầu dùng OpenRouter với DeepSeek làm điều phối viên và worker, thay cho tác tử con Claude Opus (ghi đè quy định "OpenRouter không thay tác tử con Claude" của `../CLAUDE.md`). Phiên Claude (Opus 5.5) chỉ khởi chạy các lượt gọi, chuyển kết quả giữa các vai và kiểm cuối.

| Vai | Công cụ | Model (theo metadata cầu nối) |
|---|---|---|
| Điều phối viên DeepSeek: kế hoạch, duyệt từng phần | `openrouter-mcp-reviewer` (hồ sơ `plan`, `review`) | `deepseek/deepseek-v4-flash-0731` |
| Người biên tập (no-ai-slop Edit) | `openrouter-mcp-writer` (hồ sơ `patch`) | `deepseek/deepseek-v4-flash-0731` |
| Phản biện độc lập (no-ai-slop Detect) | `openrouter-mcp-reviewer` (hồ sơ `review`) | `deepseek/deepseek-v4-flash-0731` |

Đầu vào chuẩn: `planning/lec-01/van-phong-tac-gia.md`, mục "The author's voice" của `../CLAUDE.md`, `thuat-ngu.md`, bản Bài 01 đã sửa. Kế hoạch, báo cáo phản biện, phán quyết và metadata từng lượt gọi: `planning/lec-02/deepseek/` (`master-plan.md`, `<phần>-<vòng>-{writer,review,verdict}.md`, `calls.jsonl`). Tám phần (mở đầu–§3, §4, §5, §6, §7, §8, §9–§12, Phụ lục), mỗi phần: biên tập → phản biện → phán quyết → tối đa một vòng sửa.

Nội dung đã sửa: "khả thực/bất khả tri" → "khả diễn/bất khả diễn"; "mẫu" → "tập huấn luyện" khi chỉ dữ liệu huấn luyện; "trước mẫu" → "trước khi lấy mẫu"; "bản có nhiễu/bản nhãn tất định" → "dữ liệu có nhiễu/dữ liệu tất định"; "phân bố đồng thời" → "phân bố liên hợp"; bỏ chỉ dẫn điều hướng ("ở §6", "(Phụ lục C)", "Bài tập 02.x cho thấy", "Bài 06 …"), câu rào đón, câu nhắc lại kết quả vừa chứng minh, nhãn "**Kết luận.**" (gộp vào mạch văn hoặc "Tóm lại,"); diễn đạt tích cực thay cho "không phải …"; ý nghĩa vận hành của độ tin cậy $1-\delta$; danh sách bốn cỡ mẫu ở §9.

Kiểm của phiên Claude (điều phối cuối):

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa | quyết định |
|---|---|---|---|---|---|
| nghiêm trọng | chứng minh Hệ quả 02.16; Phụ lục A | writer xóa câu lộ trình, trái quy tắc khóa học "chứng minh mở đầu bằng lộ trình"; Bài 01 của tác giả giữ 4 nhãn "Lộ trình." | `git diff`: dòng "**Lộ trình.** Một bước tất định …", "**Lộ trình.** Tính $\varphi(0)$ …" bị xóa | khôi phục nguyên văn | đã sửa (DeepSeek writer, `fix1-writer.json`); 11 nhãn như HEAD |
| trung bình | §8, yêu cầu của điều phối viên DeepSeek | đề nghị bỏ nhãn "Lộ trình." ở Mệnh đề 02.17 | `s8-2-verdict.md` | — | bác bỏ (cùng lí do trên) |
| trung bình | §2, dòng 84 | một cụm "được nêu ở chỗ dùng lần đầu" lặp ba lần | sau vòng sửa mở đầu | gộp thành một câu | đã sửa |
| nhẹ | (T4), §9, §10 | còn "trước mẫu", "khả thực" | `grep` | đổi theo thuật ngữ | đã sửa; `grep` còn 0 |
| nhẹ | §4, Bổ đề Markov | "tức một mức mà $V$ được so với nó" tối nghĩa | diff | "khác với độ lệch $\epsilon$ khỏi kì vọng trong Định nghĩa 02.1" | đã sửa (`fix2-writer.json`) |
| nhẹ | §5, sau Định nghĩa 02.9 | cách hiểu "95 lần trong 100" thiếu điều kiện $\delta=0{,}05$ | diff | thêm "khi $\delta=0{,}05$" | đã sửa |
| nhẹ | Ví dụ 02.7, 02.10, 02.12 | "Ứng dụng:" mất tên ứng dụng sau khi bỏ "ở §3" | diff | "Ứng dụng chọn hàm phân lớp trên mẫu xác thực" | đã sửa |
| — | §6 | lượt writer đầu lỗi JSON phía nhà cung cấp, không đổi gì | `calls.jsonl` (`s6-1-writer`, rc 1) | chạy lại §6 | chạy lại; phán quyết chấp nhận |

Phiên Claude đọc toàn bộ diff (word diff): mọi khối đánh số, con số và công thức còn nguyên; không thêm khẳng định mới; 88 dòng `:::` như HEAD. Kiểm định do phiên Claude chạy: `sync-local-materials.py --check` OK; `forward_refs.py` 0; `git diff --check` sạch; không có ký tự thay thế, Cyrillic hay CJK. Playwright (Chromium), HTTP: 1600×900 và 390×844, 1381 công thức, 0 `.katex-error`, 0 công thức tràn, 0 lỗi console/trang, 0 yêu cầu hỏng, trang rộng 375 px ở 390 px; in PDF chạy được; ảnh chụp 390 px đã xem.

**Còn mở:** nhãn "**Đối tượng so sánh.**" (§1, mục 7) giữ nguyên, chờ tác giả quyết (Bài 01 đã bỏ nhãn này, Bài 02 còn dùng khái niệm ở Hệ quả 02.16). `exercises.md` Bài 02 còn 17 dòng dùng thuật ngữ cũ (khả thực, bất khả tri, …); chưa sửa trong lượt này.

**Quyết định:** chấp nhận ghi chú Bài 02 sau sửa; commit và push.

## Sửa bài tập theo văn phong tác giả, khớp ghi chú đã sửa — Bài 02 (2026-11-01)

Cùng ngoại lệ quy trình như mục trên (người dùng yêu cầu DeepSeek qua OpenRouter làm điều phối viên và worker). Mọi lượt gọi: `deepseek/deepseek-v4-flash-0731` (metadata cầu nối, `planning/lec-02/deepseek-bai-tap/calls.jsonl`); điều phối viên DeepSeek lập kế hoạch (`master-plan.md`), writer (`openrouter-mcp-writer`, hồ sơ `patch`), phản biện và phán quyết (`openrouter-mcp-reviewer`). Bảy phần: 02.1, 02.2–02.3, 02.4–02.5, 02.6, 02.7–02.8, 02.9–02.10, 02.11.

Nội dung đã sửa: "bất khả tri" → "bất khả diễn", "khả thực" → "khả diễn", "trước mẫu" → "trước khi lấy mẫu", "hàm chỉ thị" → "hàm chỉ báo" (toàn tệp, 25 chỗ); bỏ bốn chỉ dẫn "(Phụ lục B.1)", "Phụ lục B.2" ở Bài tập 02.5 (con số đã nêu tại chỗ); $\ell_c$ ở Bài tập 02.11(b) viết thành công thức $4\cdot\mathbb 1[h(x)=0,\,y=1]+\mathbb 1[h(x)=1,\,y=0]$. Phán quyết DeepSeek: 02.4–02.5 và 02.11 chấp nhận; năm phần còn lại "không thay đổi" vì writer của phần 02.1 đã đổi thuật ngữ toàn tệp (vượt phạm vi phần, nội dung đúng).

Kiểm của phiên Claude:

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa | quyết định |
|---|---|---|---|---|---|
| nhẹ | Bài tập 02.5(d) | còn "ghi hai chỉ thị" sau khi đổi "hàm chỉ thị" → "hàm chỉ báo" | `grep "chỉ thị"` | "ghi hai giá trị của hàm chỉ báo" | đã sửa (thay thế cơ học do phiên Claude làm) |
| nhẹ | phạm vi | writer phần 02.1 sửa thuật ngữ ngoài phần được giao | `bt01-1-writer.md` | — | chấp nhận nội dung (chỉ thay thuật ngữ, đã kiểm từng chỗ trong word diff) |

Phiên Claude đọc toàn bộ word diff: thay thế thuật ngữ đúng, công thức $\ell_c$ khớp ba trường hợp cũ, mọi con số, khối và trích dẫn tới ghi chú còn nguyên; 108 dòng `:::` như HEAD; không còn thuật ngữ cũ; 0 ký tự thay thế/Cyrillic/CJK. `sync-local-materials.py --check` OK; `git diff --check` sạch. Playwright (Chromium), HTTP, 1600×900 và 390×844: 1234 công thức, 0 `.katex-error`, 0 công thức tràn, 0 lỗi console/trang, 0 yêu cầu hỏng, trang rộng 375 px ở 390 px; in PDF chạy được.

**Quyết định:** chấp nhận bài tập Bài 02 sau sửa.

## Bản sửa tay của tác giả, §1–§2 và Bổ đề 02.5 — Bài 02 (2026-11-01)

Tác giả sửa §1 mục 6 (bốn mục tiêu thành danh sách, $\sup$), mục 7 (công thức hiển thị, giữ nhãn "Đối tượng so sánh"), bảng nguồn ngẫu nhiên ($\max\to\sup$), §2 (nêu (T3), (T4), (O1), (O2) tập trung thành danh sách; bỏ câu "được nêu ở chỗ dùng lần đầu") và Bổ đề 02.5 ("tăng ngặt" → "tăng nghiêm ngặt"). Phân tích đưa vào `planning/lec-01/van-phong-tac-gia.md` §6b. Không đổi câu chữ của tác giả; chỉ xóa một dấu cách cuối dòng 56 để `git diff --check` sạch. Theo yêu cầu của tác giả: commit và push.

Kiểm định do phiên Claude chạy: `forward_refs.py` 0; `sync-local-materials.py --check` OK; `git diff --check` sạch; Playwright 1600×900 và 390×844: 1392 công thức, 0 `.katex-error`, 0 công thức tràn, 0 lỗi, 0 yêu cầu hỏng, rộng 375 px ở 390 px; in PDF chạy được.

**Chỗ khác bị ảnh hưởng (chưa sửa, chờ tác giả):**

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | §2 dòng 87 và §5 dòng 416–418 | (T3) được định nghĩa hai lần với nội dung khác nhau: §2 "$\ell(h,z)\in[a,b]$", §5 "$0\le\ell(h,z)\le1$"; §5 kết luận "$\ell_c$ … $[0,4]$ nên không thỏa (T3)", sai theo bản §2; dòng 445 dùng "$L_D(h)\le1$ theo (T3)" | `grep -n "(T3)"` | thống nhất một định nghĩa: hoặc (T3) là $[0,1]$ ở §2 (đổi "ví dụ $[0,1]$"), hoặc giữ $[a,b]$ và sửa §5 (dòng 416–418, 445) cùng các hằng số dùng $b-a=1$ |
| trung bình | §6 dòng 651 | (T4) được định nghĩa lần thứ hai ("$K\ge1$, được chọn trước và không phụ thuộc $S$") | `grep -n "(T4)"` | bỏ gạch đầu dòng ở §6, giữ câu dẫn tham chiếu (T4) của §2; chuyển "$K\ge1$, không phụ thuộc $S$" lên §2 nếu tác giả đồng ý |
| nhẹ | §7 dòng 745 | câu "Bước này dùng giả thiết tối ưu: (O1) …, hoặc (O2) …" nhắc lại định nghĩa vừa đưa lên §2 | dòng 745 | rút còn tham chiếu "(O1) hoặc (O2)" |

**Giải quyết (2026-11-01, quyết định của tác giả):** (T3) là hàm lỗi trong $[0,1]$; (T4), (O1), (O2) chỉ định nghĩa ở §2, các chỗ sau chỉ tham chiếu. DeepSeek writer (`deepseek/deepseek-v4-flash-0731`, `planning/lec-02/deepseek/fix3-writer.json`) thay bốn đoạn: (T3) ở §2 thành "$\ell(h,z)\in[0,1]$" (theo quyết định của tác giả); bỏ định nghĩa lại (T3) ở §5 và (T4) ở §6, thay bằng câu tham chiếu §2; câu (O1)/(O2) ở §7 rút thành tham chiếu. Ba phát hiện ở bảng trên: đã sửa. Bài tập dùng (T3) theo nghĩa $[0,1]$; Bài tập 02.11 tự nêu giả thiết $[a,b]$, không mâu thuẫn. Phiên Claude kiểm diff; `forward_refs.py` 0; sync OK; `git diff --check` sạch; Playwright 1600×900 và 390×844: 1385 công thức, 0 `.katex-error`, 0 tràn, 0 lỗi, 0 yêu cầu hỏng; in PDF chạy được. **Quyết định:** chấp nhận; commit và push.
