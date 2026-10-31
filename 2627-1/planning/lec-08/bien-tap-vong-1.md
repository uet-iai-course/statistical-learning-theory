# Biên tập vòng 1 — Bài 08

Biên tập viên: người viết ghi chú (general-purpose, opus, high; giao qua `SendMessage` của phiên điều phối). Ngày 2026-10-31. Căn cứ: `reviews/0-quyet-dinh.md` (ưu tiên cao nhất) và năm báo cáo `reviews/1-…5-…`. Số dòng ở cột "Dòng" theo bản đóng băng `lec08-draft-frozen.md`. Không commit.

**Số tiếng (`wc -w`).** Trước: thân bài 11 946, phụ lục 1 488, 1 084 dòng. Sau: thân bài 11 982, phụ lục 2 106, 1 111 dòng. Trần: 12 000 / 3 000.

**Kiểm tra sau sửa.** `forward_refs.py` 0; `sync-local-materials.py` rồi `--check` OK; `git diff --check` sạch trên `lec-08/` và `material-local-data.js` (tệp `lec-01/lecture-note.md` có thay đổi chưa commit của người khác, có khoảng trắng cuối dòng; không phải tệp của tôi, nhưng lệnh sync đã gói nó vào `material-local-data.js`); 33 khối mở, 33 khối đóng; viewer qua HTTP (cổng 8783, đã tắt) và `file://` ở 1600×900 và 390×844, mọi `details` mở: 1 434 công thức, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức hay bảng tràn; quét thêm: không dòng công thức nào cắt giữa $\lVert\cdot\rVert$, $\lvert\cdot\rvert$, $\langle\cdot\rangle$ hay mở bằng "$\cdot$". Ảnh chụp ở scratchpad `writer08/shots2/`, `writer08/s2_*.png`.

## 1. Quyết định gộp (bắt buộc)

| Mã | Dòng | Cách sửa |
|---|---|---|
| N1 (i) | 445–449 | Bước 1 Định lý 08.6: định lý giá trị trung bình dọc đoạn thẳng trong $W$ (tính lồi của $W$) và (G); câu "Bước này không dùng tính lồi của hàm lỗi". Bỏ Mệnh đề 05.5(a) ở đây |
| N1 (ii) | 343–352, 306, 699, 774, 778 | Bước khác biệt (Mệnh đề 08.5, Bước 2) viết lại: $\Delta_{t+1}\le\lVert(w_t-w'_t)-\eta_t(g-g')\rVert\le\Delta_t+\eta_t\lVert g\rVert+\eta_t\lVert g'\rVert\le\Delta_t+2G\eta_t$, chỉ dùng (G) tại $w_t,w'_t\in W$, tam giác và phép chiếu không giãn; nhãn bước "(G) và tính không giãn của phép chiếu". Câu kết §5 (306): "hai lần chạy áp dụng hai ánh xạ khác nhau … nên Bổ đề 08.4 không chặn được $\Delta_{t+1}$". Câu mở §9 (699): "Trong chứng minh Định lý 08.6, tính lồi của hàm lỗi, tính trơn và $\eta_t\le2/\beta$ chỉ đi vào qua Bổ đề 08.4, tức qua các bước chung". Mệnh đề 08.10 Bước 2: bước khác biệt dùng lại Bước 2 của 08.5. $\square$ của 08.10: "ở các bước chung, chỗ duy nhất mà tính lồi của hàm lỗi từng được dùng" |
| N1 (iii) | 405, 111, 491 | §7 mở: "Theo (G) và tính lồi của $W$ …". §2: "(G) kéo theo (L) … theo định lý giá trị trung bình dọc đoạn thẳng trong $W$ (§7), không cần tính lồi của hàm lỗi". Đoạn sau định lý: tính lồi của hàm lỗi chỉ qua Bổ đề 08.4(a) ở bước chung; tính lồi của $W$ cho tính không giãn của phép chiếu và tính Lipschitz |
| N1 (iv) | 33, 896, Phụ lục A Bước 2 | Mục tiêu 2 giữ nguyên (nay có một đáp án: Bổ đề 08.4(a), Phụ lục A Bước 2). Tiêu đề Bài tập 08.3: "Bước chứng minh không còn đúng khi bỏ tính lồi" (§11 và `outline.md` mục 4). Phụ lục A: "dòng duy nhất của chứng minh dùng tính lồi của $f$" |
| TB1 | 84, 88, 90, 111 | Bảng §1: "hằng số trơn $\beta$ và cận gradient $G$ (§2)"; "điểm lặp của lần chạy thứ hai (§4)" (bỏ $w'_t$). Câu 90 bỏ; "Lần chạy thứ hai chỉ dùng trong chứng minh" chuyển sau Định nghĩa 08.2. Dòng 111: "chứng minh ở Phụ lục A" thay "chứng minh tính đồng bức" |
| TB2 | 180 | "Chỉ số được rút có hoàn lại, nên một quan sát có thể được dùng lại ngay từ bước thứ hai …; Hệ quả 06.2 không áp dụng khi $T\ge2$; hệ quả này áp dụng cho một vòng theo thứ tự (Nhận xét 06.3)" |
| TB3 | 691 | "Chính quy hóa ngầm là một hành vi của thuật toán. Học phần có một lập luận cho một trường hợp: … với độ dài bước đủ nhỏ … khi nghiệm nội suy tồn tại (Phụ lục D của Bài 07)." Phép so sánh $1/\lambda$ chuyển về đây, nói là gợi ý về dạng công thức; bỏ khỏi dòng 491 |
| TB4 | 198, 213, 377–378, 396, 191 | Ví dụ 08.2: liệt kê đạo hàm tại $w'_t$ ($0;1;-1;-1;1;0$), bỏ câu "tính như Ví dụ 08.1"; bỏ câu ngân sách $3$ (bước đổi tên "tổng các phần tăng"; chọn "bỏ" vì ngân sách đã dùng ở Ví dụ 08.4 qua cận $T/4$). Ví dụ 08.4: nhóm $i_1\ne4$ có lý do ($w_2-3<-1$, $w_2+3>1$); nhóm $i_1=4$ có bảng $i_2$/$w_3$/$w'_3$/$\Delta_3$ (đã tính lại, tổng $\tfrac{17}4$); Bước 4 thêm $w_7=2$, $w'_7=-1$. §4: thêm phép tính một bước ($\tfrac38$, $\tfrac18$, hiệu $\tfrac14$; ghép cặp $\tfrac14$; độc lập $\tfrac38$ — kiểm bằng liệt kê 4 và 16 trường hợp), thay không-ví dụ cũ; tên công cụ "bất đẳng thức Jensen cho hàm trị tuyệt đối" |
| TB5 | 659–678 | Bước 2 Ví dụ 08.7: "$T=10^4$ bước rút có hoàn lại; số bước bằng một vòng, nhưng thuật toán khác thuật toán theo thứ tự của Bước 1"; tính $1+2\cdot9999/10^4=2{,}9998$, $\eta^*\approx0{,}0289$. Bước 3: đạo hàm theo $T$ cho $T^2=5\cdot10^7$; bảng hai cột $T$/Cận. Kết luận: "$7071<m$ bước, tức trước khi hết một vòng" |
| TB6 | 524–538, 1073 | Lần chạy không ghép cặp ra khỏi thân bài; bảy giá trị ở Phụ lục D kèm "các định lý của bài không nói gì về đại lượng này" (không đưa cơ chế chưa kiểm). Phụ lục D: mỗi hạt giống một $D$ qua $w^\star$; cận đúng với mọi $D$ nên đúng cho trung bình |
| TB7 | 578 | Cận viết thành công thức; lý do không cho thông tin: hàm lỗi trên $W$ trong $[0,4]$, cận $39{,}975>4$; số $0{,}4750$ dẫn "Ví dụ 06.3, Bước 5" |
| TB8 | 699–866 | §9 sắp lại: Ví dụ 08.8 → Mệnh đề 08.10 → Nhận xét 08.11 → câu dẫn và Mệnh đề 08.12 với đoạn sau → câu chuyển "Hai ví dụ cuối giữ tính lồi …" → Ví dụ 08.9 → Ví dụ 08.10 → câu kết. Thứ tự số vẫn tăng, không đánh số lại; `forward_refs.py` 0. Câu mở nêu ba ví dụ bỏ ba điều kiện, ví dụ cuối xét mạng ReLU nơi cả ba không thỏa |
| TB9 | 942–952 | HRS: "nêu kết quả cho cả rút đều lẫn hoán vị ngẫu nhiên" (bỏ khẳng định khác biệt); §6 thí nghiệm, §7 câu hỏi mở; "Bài báo bắt đầu từ $w_0$ …"; $\sqrt3$, $\sqrt2$: "Hai cách cho cùng hai thừa số …; bài báo đọc chúng như mức chênh tối đa" (đã đối chiếu HRS tr. 19). UML §20.6 thêm "mỗi bước dùng một quan sát mới từ $D$"; Phụ lục A của HRS: "chứng minh Bổ đề 3.7 từ tính đồng bức" |
| TB10 | 153, 218, 306, 401, 580, 866; lặp | 153 cắt; 218 → giới hạn (một dãy so với kì vọng theo $\xi$); 306 xem N1; 401 → giới hạn (cận bỏ qua việc bước chung kéo lại gần); 580 cắt (§7 kết bằng giới hạn $39{,}975>4$); 866 → giới hạn (mạng ReLU không có cận ổn định trong học phần). Lặp: "cận bằng số vòng" chỉ ở dòng 11; "11–109 lần" chỉ ở Ví dụ 08.6; "$0{,}309$; …" chỉ ở §8; "đo tính ngẫu nhiên …" chỉ ở §4; "(G) dùng hai lần" chỉ ở đoạn sau định lý; chính quy hóa ngầm là giả thuyết chỉ ở §10; $\sqrt3$/$\sqrt2$ ở khối Hệ quả 08.8 và một lần ở §13. Phép đối: 25, 90, 439, 491, 540, 691, 880 viết lại hoặc cắt. §10 kết bằng đoạn văn xuôi |
| TB11 | 253–261, 345–351, 418–437, 605–610, 718–724, 749–756 | Bổ đề 08.4(b) với $g_{uv}$, không dòng mở bằng "$\cdot$". Bảo đảm của Định lý 08.6, Hệ quả 08.8, Mệnh đề 08.10 viết thành đoạn có nhãn in đậm (271 px thay 230 px); $\eta^*=R/(G\sqrt{T+2T(T-1)/m})$. Danh sách $\Delta$ cosin viết trong câu. Đo lại: 0 tràn |

## 2. Điểm nhẹ của quyết định gộp

| Điểm | Cách sửa |
|---|---|
| Khả tích Mệnh đề 08.12 | Thêm giả thiết **Khả tích**; Phụ lục C Bước 4 dẫn nó |
| "giảm về" 08.8(b) | "tiến về $RG\sqrt{2/m}$ khi $T\to\infty$, và giảm theo $T$ khi $m>2$" |
| Ví dụ đạt hằng số 08.10(a) | Dùng hàm cosin (thỏa (G)): đạo hàm ánh xạ bước $1+\eta\cos(w-z)$, bằng $1+\eta$ tại $w=z$; bỏ $-\tfrac\beta2\lVert w\rVert^2$ |
| Dòng 781 | "Nhân với $G=1$, cận cho hiệu hàm lỗi tại một quan sát kiểm tra cũng là khoảng $275{,}6$" |
| "5–10 vòng" | "Trong các thời điểm đo …, nhỏ nhất ở $5$ vòng ($0{,}589$; ở $10$ vòng là $0{,}603$, Phụ lục D)" |
| ReLU không khả vi | "tiền kích hoạt (pre-activation), tức một tọa độ của $\Theta_1x+b_1$, bằng $0$ và trọng số ra tương ứng khác $0$" |
| Ví dụ 05.12 | "Với hàm không trơn của Ví dụ 05.12, …"; "độ chênh tối ưu của $\bar w_T$" |
| Phạm vi xáo trộn lại | Mệnh đề 08.5: "theo phép cập nhật của Thuật toán 08.1"; "một quy tắc rút chỉ số với $\Pr(i_t=i)=1/m$ cho mọi $t$, chẳng hạn rút đều có hoàn lại" |
| $c$, $s$, $d$ | Hệ số giãn $\kappa$; chỉ số cộng $k$; $g_{uv}$ thay $d$ |
| (T2) | "(T2) ($\ell\ge0$, đo được) cùng điều kiện $L_D(w_1)<\infty$" |
| Tiên quyết | Bỏ Ví dụ 06.9; thêm trung bình cộng–trung bình nhân, (C), Mệnh đề 01.7 (nay được dẫn ở Bước 4 Định lý 08.6) |
| Tiếng Anh | ổn định đều (dòng 3), step size (còn gọi là tốc độ học), ReLU (rectified linear unit), pre-activation, burn-in (đã có), likelihood |
| Từ thân mật | "hỏng", "tính tay", "thua", "tệ hơn", "tách nhau" đã thay; grep 0 |
| "chỉ số bước", "dừng" | "chỉ có số bước thay đổi"; "hội tụ tới hai điểm" |
| Dòng 3 | Không mở bằng "Bài 07 kết thúc bằng câu hỏi"; câu đầu tách đôi; thêm "qua số bước và độ dài bước" (R5 P15) |
| Câu hỏi tu từ dòng 23 | Thành câu khẳng định |

## 3. Phát hiện nhẹ theo người rà

| Người rà, mã/dòng | Kết quả |
|---|---|
| R1 · 3, 43, 39–44, 111, 77, 90 | Áp dụng (xem trên); 111: "(G2), cận mô-men bậc hai của oracle (Định nghĩa 05.10)"; 77: "**Đối tượng so sánh.** $\inf_WL_D$, chỉ dùng ở §8; …" |
| R1 · 11–19 (thêm cột "Cận") | **Không áp dụng.** Bảng năm cột tràn ở 390 px (đã đo ở bản nháp); giữ câu "bằng đúng số vòng ở cột đầu" |
| R1 · 242 (tiêu đề "phác thảo") | **Không áp dụng.** Quy ước của Bài 07 (Bổ đề 07.10): "phác thảo (… chứng minh ở Phụ lục A)" nghĩa là thân bài phác thảo, phụ lục đầy đủ; blueprint ghi Lemma 8.1 [S] |
| R1 · 287, 377, 252–261, 584, 686, 693, 781, 840, 517/1073, 1080 | Áp dụng (hệ số giãn nhỏ nhất được gọi tên trong Ví dụ 08.3; "cận của số hạng"; định nghĩa dừng sớm tách hai câu; $\Theta_1$, $\Theta_2$ có tên; "15–25 giây") |
| R1 · 540, 872 (no-ai-slop) | 540 viết lại kết luận; 872 bỏ câu châm ngôn, đoạn chuyển xuống cuối §10 |
| R1 · ngân sách $3$ (213) | Chọn phương án bỏ (TB4) |
| R1 · cơ chế $\Delta$ ghép cặp > không ghép cặp | **Không áp dụng câu giải thích cơ chế**: chưa có căn cứ kiểm được; theo TB6, chuyển số ra Phụ lục D |
| R2 · 1–10 | Phát hiện trung bình theo N1; nhẹ: khả tích 08.12, "giảm về", ví dụ đạt hằng số, 781, 693, HRS §7, ReLU trọng số ra, Phụ lục D Bài 07 là lập luận, Ví dụ 05.12, phạm vi xáo trộn lại: áp dụng hết. Phương án HRS cho bước khác biệt: được dùng (N1) |
| R3 · F1–F16, F18 | Áp dụng. F11: Bước 4 Định lý 08.6 thêm cận $\mathbb EL_S(w_{T+1})$. F16: $\kappa$, $g_{uv}$. F18: "hữu hạn với véc-tơ đặc trưng ngẫu nhiên $\chi(x)$ của Ví dụ 07.3" |
| R3 · F17 (thừa số $1+(1-\tfrac1m)\beta\eta_t$) | **Không áp dụng** (tùy chọn, thiếu chữ); Bước 2 ở Phụ lục F nói bước khác biệt cho $\Delta_t+2G\eta_t$, không quá vế phải |
| R4 · T1–T7 | Theo N1 và TB4, TB7, TB10, TB11 |
| R4 · N1–N26 | Áp dụng, trừ: N12 (xem R1 213, cùng kết quả); N23 thay bằng câu trung tính có nguồn (HRS tr. 19 có $\sqrt3$, $\sqrt2$). N2: "ổn định đều (uniform stability)" ở dòng 3, bỏ ở dòng 5. N9 nhãn "Ánh xạ không giãn.". N16 dạng "Bước k của chứng minh Định lý 08.6". N17: dòng 959 "Chứng minh phần (a) … dựa trên *cận trên bậc hai* (còn gọi là bổ đề hạ; quadratic upper bound, descent lemma)" |
| R5 · P1–P16 | Áp dụng. P4: bỏ Ví dụ 06.9 (không dẫn lại ở §10). P13: đoạn cấp lớp/cấp thuật toán chuyển xuống cuối §10. P14(d): kết luận Ví dụ 08.6 viết lại. Δ có chỉ số ở Ví dụ 08.6 |

## 4. Chỗ cắt bù chữ

| Chỗ cắt | Tiếng (ước) |
|---|---|
| Chứng minh Hệ quả 08.8 chuyển sang Phụ lục E (thân bài giữ một câu lộ trình) | −330 |
| Phác thảo chứng minh Mệnh đề 08.10 chuyển sang Phụ lục F (giữ một câu) | −200 |
| Câu ôn nhanh 2 (phép chiếu) và lời giải (thứ tự cắt 6 của dàn ý) | −70 |
| Lần chạy không ghép cặp khỏi Ví dụ 08.6 | −60 |
| Câu kết §3, §7; câu lỗi phân lớp ở câu hỏi mở đầu; "cận bằng số vòng" lặp; câu "(G) dùng lần thứ hai" | −120 |
| Câu "Công thức … không được dùng lại" (§9); gạch đầu dòng "Bài tập" ở §13 | −25 |
| Rút gọn: đoạn §2 về (L), gạch đầu dòng "Giả thuyết thực nghiệm" ở §10, đoạn chính quy hóa ngầm | −60 |

Phần thêm (khoảng +900): phép tính ghép cặp một bước, các bước của Ví dụ 08.2, 08.4, 08.7, định lý giá trị trung bình ở Bước 1, cận $\mathbb EL_S$, giả thiết khả tích, ví dụ cosin đạt hằng số, câu chuyển và câu kết §9, sửa §13.

## Vòng 2 (2026-10-31)

Căn cứ: `reviews/6-ra-lai-toan.md` (2 nhẹ), `reviews/7-ra-lai-mach.md` (M1, M2, 10 nhẹ, P9 một phần), quyết định "Rà lại sau vòng 1" trong `review-log.md`. Số dòng theo bản trước vòng 2 (`lec08-r1-frozen.md`, trùng tệp lúc đó).

| Mã | Dòng | Cách sửa |
|---|---|---|
| R6 · nhẹ 1 | 497 | "Giả thiết (G) được dùng ở bước khác biệt, cho tính Lipschitz tại mọi quan sát kiểm tra, và cho tính khả tích ở Bước 4." |
| R6 · nhẹ 2 | 1110 (□ Phụ lục F cũ) | "Thừa số $1+\beta\eta_k$ xuất hiện vì các bước chung, chỗ duy nhất mà tính lồi của hàm lỗi từng được dùng; để lấy kì vọng mà không cần tính độc lập, (b) nhân thừa số này ở mọi bước." |
| M1 | 193 | "Khoảng cách này gồm cả hiệu $\tfrac14$ do thay quan sát và phần do tính ngẫu nhiên của thuật toán." (bỏ phép đối) |
| M2 | 746 | "Thừa số $\prod_k(1+\beta\eta_k)$ trong (c) tăng theo hàm mũ …" |
| N1 | 309 | "Ghép trường hợp này với bước chung (Bổ đề 08.4), ta được …" |
| N2 | 218 | "…; Định nghĩa 06.9 cần kì vọng theo $\xi$, nên hai sự kiện ở Bước 3 phải được chứng minh cho mọi dãy." |
| N3 / P9 | 906 | Thêm "Câu hỏi cho Bài 09 là: …" như Bài 06–07; không phát biểu kết quả Bài 09 |
| N4 | 690, 796 | "nơi tính lồi, tính trơn và (G) đều không thỏa"; "Hai ví dụ cuối trở lại hàm lỗi lồi …" |
| N5 | 445 | Câu sau: "Bảo đảm chỉ áp dụng cho Thuật toán 08.1 với quy tắc rút chỉ số đã nêu." |
| N6 | 682 | Cắt câu nhắc lại định nghĩa |
| N7 | 342–347 | $g_t=\nabla\ell(w_t,z_i)$, $g'_t=\nabla\ell(w'_t,z')$ |
| N8 | 1050 | "$\Delta$ giữa lần chạy thứ nhất và lần chạy thứ ba …" |
| N9 | Phụ lục F cũ, Bước 1 | "Với $\Gamma=\Gamma_{\eta,z}$, …"; "Phép chiếu không giãn, nên $\operatorname{proj}_W\circ\Gamma$ có cùng hệ số giãn." |
| N10 | 187, 44 | "theo bất đẳng thức Jensen với hàm trị tuyệt đối, …"; thêm "Jensen" vào mục Giải tích |
| Ghi chú nhỏ | 198 | Bỏ chữ trong công thức: "$w'_{t+1}$ bằng $w'_t$ trừ nửa đạo hàm" |
| Thứ tự phụ lục | Phụ lục | Đánh lại chữ theo thứ tự đọc (0 tiếng): A tính đồng bức, B chi tiết truy hồi, C chứng minh Hệ quả 08.8 (cũ E), D phác thảo Mệnh đề 08.10 (cũ F), E điểm dừng xấp xỉ (cũ C), F giao thức thí nghiệm (cũ D). Mọi dẫn chiếu trong thân bài, tiêu đề khối và phụ lục đã đổi; "Phụ lục D của Bài 07", "Phụ lục B trong Bài 05" giữ nguyên; docstring script đổi thành "Phụ lục F" |

Cắt bù chữ: N6 (−11), M1 bỏ vế "nên lớn hơn hiệu cần chặn" (−6), N5 (−7), câu ghi chú dòng 198 rút gọn. Số tiếng: thân bài 11 995 (trước vòng 2: 11 982), phụ lục 2 131 (trước 2 106). Kiểm tra: `forward_refs.py` 0; sync và `--check` OK; `git diff --check -- 2627-1/materials/lec-08` sạch; 33/33 khối; viewer HTTP (cổng 8783, đã tắt) 390×844 và 1600×900: 1 439 công thức, 0 `.katex-error`, 0 tràn, 0 lỗi trang, 0 yêu cầu hỏng. Không động vào `lec-01`.
