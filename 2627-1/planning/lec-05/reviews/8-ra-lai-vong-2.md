# Bài 05 — Rà lại kết hợp sau biên tập vòng 2

Số phát hiện: chặn bàn giao 0 · nghiêm trọng 0 · trung bình 0 · nhẹ 6.

Đầu vào: `2627-1/materials/lec-05/lecture-note.md` (1341 dòng; số dòng dưới đây là của tệp hiện tại); `scratchpad/lec05-round2.diff` (31 chỗ sửa); mục "Vòng 2" trong `planning/lec-05/bien-tap-vong-1.md`; `reviews/6-ra-lai-toan.md`, `reviews/7-ra-lai-mach.md`; `van-phong.md` §3a, §7a, §9a, §12; ghi chú Bài 01–04 (grep cách in số). Văn bản rà theo `no-ai-slop` chế độ Detect.

**Kiểm tra đã chạy.**
- `forward_refs.py 2627-1/materials/lec-05/lecture-note.md`: **0 forward references**.
- `wc -w`: thân bài (trước `## Phụ lục`) **11 973** ≤ 12 000; phụ lục **1 182** ≤ 3 000.
- Câu mới dài hơn 40 tiếng (script `scratchpad/py/r05_mach_long2.py`, so với `lec05-round1.md`): dòng 739 (49 tiếng) và 974 (42 tiếng). Ba câu dài vòng trước (17, 304, 962) đã được tách.

## 1. Trạng thái phát hiện của 6-ra-lai-toan và 7-ra-lai-mach

| Nguồn | Phát hiện | Trạng thái | Dòng hiện tại |
|---|---|---|---|
| R6 tb, R7 tb | Câu cuối §6 khẳng định không điều kiện | ✓ (cách viết, xem bảng 3) | 642 |
| R6 nhẹ | §9 câu đầu: $\operatorname{opt}_S$ là độ chênh, không phải $F(\bar w_T)$ | ✓ (cụm "khi $R$ phủ $W$", xem bảng 3) | 966 |
| R6 nhẹ | Định nghĩa 05.18: "$s$ cố định" mâu thuẫn tính đo được | ✓ | 969 |
| R6 nhẹ | $P_\xi^{\otimes(T-1)}$, $P_\xi$ hai nghĩa | ✓ | 974 |
| R6 nhẹ | "Mức sàn sai số" cho hai đại lượng | ✓ một phần (tên còn gần nhau, xem bảng 3) | 755, 947, 962 |
| R6 nhẹ | $0{,}1406$ làm tròn xuống | ✓ | 896, 908, 1121: $0{,}140625$ |
| R6 nhẹ | (G1) buộc $F$ lồi không có lý do | ✓ | 739 |
| R7 tb | Câu cuối §4 lệch QĐ M8 | ✓ | 362 |
| R7 nhẹ | □ Mệnh đề 05.13 "bậc hai theo độ dài bước" | ✓ | 680 |
| R7 nhẹ | (C) "đi vào một bước" | ✓ | 883 |
| R7 nhẹ | §9 không kết bằng văn xuôi | ✓ | 1037 (đoạn "Mức (O2) …" sau Ví dụ 05.14) |
| R7 nhẹ | §3 dùng "hàm lồi" trước §4 | ✓ (văn phong, xem bảng 3) | 154 |
| R7 nhẹ | Lý do $\lambda$ trùng kí hiệu | ✓ | 360 |
| R7 nhẹ | Định nghĩa 04.1 vào tiên quyết | ✓ | 40 |
| R7 nhẹ | Nhãn danh sách sau Định nghĩa 05.10 | ✓ | 502 "Phân bố rút không đều"; 504 thêm hệ quả |
| R7 nhẹ | Câu dài 17, 304, 962 | ✓ | 17, 304, 962 |
| R7 nhẹ | "Chặt ngặt" | ✓ | 695 |
| R7 nhẹ | Lớp hàm điểm số nhận giá trị trong $\mathbb R$ | ✓ | 974 |
| R7 nhẹ | Số lớn ở bảng Ví dụ 05.15 và §11 | đã sửa, nhưng tạo lệch mới | 1093, 1117 (mục 4) |
| R7 §6 | Cắt K1–K7 | ✓ cả bảy, đã đối chiếu từng chỗ trong diff | 775, 843, 870, 179, 474, 1098, 1111 |

## 2. Toán học của các câu đã sửa

- **Cuối §6 (642).** Theo Mệnh đề 05.13, $\Delta_{t+1}\le\Delta_t-2\eta\langle g_t,w_t-u\rangle+\eta^2\lVert g_t\rVert^2$. Lấy $\mathbb E[\cdot\mid\mathcal F_{t-1}]$ rồi dùng Bổ đề 05.12(b) và bất đẳng thức dưới gradient của $\psi(w_t)$:
  $$\mathbb E[\Delta_{t+1}\mid\mathcal F_{t-1}]\le\Delta_t-2\eta\,(F(w_t)-F(u))+\eta^2G^2 .$$
  Vậy lượng giảm theo kì vọng có điều kiện ít nhất là $2\eta(F(w_t)-F(u))-\eta^2G^2$, như câu phát biểu. Câu đúng cả khi $F(u)>F(w_t)$, vì khi đó "lượng giảm" âm. Con trỏ "(§7)" đúng chỗ chứng minh. Cách viết "giảm ít nhất …, trừ số hạng …" có thể đọc thành hai phép trừ nối nhau: xem bảng 3.
- **Lý do (G1) buộc $F$ lồi trên $W$ (739).** Đặt $\pi=\alpha w+(1-\alpha)w'\in W$ (vì $W$ lồi). (G1) cho $\psi(\pi)\in\partial F(\pi)$. Viết bất đẳng thức dưới gradient tại $\pi$ cho $u=w$ và $u=w'$, nhân với $\alpha$ và $1-\alpha$ rồi cộng: số hạng tích vô hướng triệt tiêu vì $\alpha(w-\pi)+(1-\alpha)(w'-\pi)=0$, nên $\alpha F(w)+(1-\alpha)F(w')\ge F(\pi)$. Nửa câu trong ngoặc khớp với lập luận này. $w'$ là kí hiệu cục bộ, không xung đột.
- **Cuối §4 (362).** "Mỗi dưới gradient, theo định nghĩa, cho một cận dưới toàn cục": đúng (Định nghĩa 05.2). "Với $F$ lồi, dưới gradient tồn tại tại mọi điểm": đúng, dẫn ở 193. "Gradient là một dưới gradient (Mệnh đề 05.3(a))": đúng tại điểm khả vi. Câu khớp với 739, 758, 1127 và QĐ M8.
- **Kết luận Ví dụ 05.7 (695).** Không chiếu: $0{,}5053-0{,}1764+1=1{,}3289$, bằng vế trái, nên có dấu bằng như Mệnh đề 05.13 khi $W=\mathbb R^p$. Có chiếu: $0{,}5053-0{,}0034+1=1{,}5019>1{,}3289$, nên bất đẳng thức ngặt. Đúng.
- **Ví dụ 05.12 (947).** $\eta G^2/2=0{,}2\cdot1/2=0{,}1=f(w_t)$; vế phải $0{,}025/T+0{,}1$ không nhỏ hơn $f(\bar w_T)=0$ hay $f(w_{T+1})=0{,}1$. "Số hạng $\eta G^2/2=0{,}1$ của cận" đúng.
- **Đầu §9 (966).** Theo Hệ quả 05.15(b), khi $\lVert w_1-u\rVert\le R$ với mọi $u\in W$ thì $F_R=\inf_WF$, nên $\mathbb EF(\bar w_T)-\inf_WF\le RG/\sqrt T$. Với $F=L_S$ và lớp $\{h_w:w\in W\}$, đại lượng này là $\mathbb E\operatorname{opt}_S(\bar w_T)$ (Hệ quả 05.19(a)). Đúng, trừ cụm không chính xác "khi $R$ phủ $W$".
- **Định nghĩa 05.18 và đoạn sau (969–974).**
  - Tính đo được "theo bộ ba, với $s$ chạy trên $\mathcal Z^m$" khớp Định nghĩa 01.4 (đo được trên $\mathcal Z^m\times\mathcal Z$).
  - $P_\xi$ là phân bố của toàn bộ $\xi$ ở 969 và 972 ($D^m\otimes P_\xi$). Dòng 974 không còn viết $P_\xi^{\otimes(T-1)}$, nên trong phạm vi §9 kí hiệu chỉ có một nghĩa. Định nghĩa 05.10 vẫn dùng $P_\xi$ cho phân bố của *một* lần rút. Cả hai cách dùng đều là "phân bố của $\xi$", với $\xi$ là đại lượng đang xét, nên không mâu thuẫn trong từng câu. Chấp nhận; nên ghi một dòng vào `ky-hieu.md`.
  - "Nhận giá trị trong $\mathbb R$ thay cho $\mathcal Y$": khớp bảng §2 (102–103) và Định nghĩa 03.7.
- **Các sửa còn lại.** Đã đọc trong ngữ cảnh ±2 đoạn, không có lỗi toán:
  - 17, 304, 962: câu được tách, nội dung không đổi.
  - 40: Định nghĩa 04.1 đúng nội dung được dùng ở 1181.
  - 360: $\tfrac\lambda2\lVert w\rVert^2$ đúng là $\lambda$-lồi mạnh.
  - 504: một oracle phụ thuộc $t$ hay các điểm lặp trước không có dạng $\varphi(w_t,\xi_t)$.
  - 680: số hạng $\tfrac\eta2\lVert g\rVert^2$.
  - 883: "những bước đã ghi".
  - 896, 908, 1121: $2{,}5\cdot2{,}25/40=0{,}140625$, in chính xác.

## 3. Phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | Cuối §6, dòng 642 | Lượng giảm đúng là hiệu $2\eta(F(w_t)-F(u))-\eta^2G^2$ (mục 2). Cách viết "giảm ít nhất A, trừ số hạng B" để người đọc tự ghép, và "trừ" dễ hiểu thành "ngoại trừ". | "…giảm ít nhất $2\eta(F(w_t)-F(u))$, trừ số hạng $\eta^2G^2$ (§7)." | "…giảm ít nhất $2\eta(F(w_t)-F(u))-\eta^2G^2$ (§7)." (bớt 2 tiếng) |
| nhẹ | Dòng 755 so với 947, 962 | Quy ước của biên tập viên giữ "mức sàn sai số (error floor)" cho mức dao động của điểm lặp cuối (962, khớp tên Bài tập 05.6), nhưng số hạng $\eta G^2/2$ của cận vẫn có hai tên: "mức sàn $\eta G^2/2$ của cận" (755) và "số hạng $\eta G^2/2$ … của cận" (947). "Mức sàn" ở 755 và "mức sàn sai số" ở 962 gần như trùng tên mà chỉ hai đại lượng khác nhau, nên mục đích của quy ước một tên một nghĩa chưa đạt. | 755: "giảm như $1/T$ về mức sàn $\eta G^2/2$ của cận"; 947: "bằng số hạng $\eta G^2/2=0{,}1$ của cận"; 962: "Mức dao động là một *mức sàn sai số* (error floor)". | Dòng 755: "…giảm như $1/T$ về số hạng $\eta G^2/2$ của cận…". Từ đó "mức sàn" chỉ xuất hiện ở 962 và §12 (Bài tập 05.6). Số tiếng không đổi. |
| nhẹ | Đầu §9, dòng 966 | "Khi $R$ phủ $W$" là cách nói không định nghĩa; điều kiện thật là ở Hệ quả 05.15(b) (772). | "Hệ quả 05.15 chặn độ chênh tối ưu $F(\bar w_T)-\inf_WF$ theo kì vọng (khi $R$ phủ $W$)" | "(khi $\lVert w_1-u\rVert\le R$ với mọi $u\in W$)" (thêm khoảng 5 tiếng; bù bằng dòng 642 và 154). |
| nhẹ | Cuối §3, dòng 154 | "§4" lặp hai lần trong một câu ngắn. | "…là một hàm lồi của $w$ theo nghĩa của §4 (kiểm ở §4 và Bài tập 05.8)." | "…là một hàm lồi của $w$ (định nghĩa và kiểm tra ở §4 và Bài tập 05.8)." (bớt 2 tiếng) |
| nhẹ | Câu dài mới (`van-phong.md` §9a): 739 (49 tiếng), 974 (42 tiếng) | Phần thêm của vòng 2 làm hai câu vượt 40 tiếng. | 739: "Tính lồi của $F$ là điều kiện để (G1) thỏa được: … ; ngược lại, (G1) tại mọi điểm của $W$ buộc $F$ lồi trên $W$ (cộng hai …)." | 739: tách trước "ngược lại" thành câu mới: "Ngược lại, (G1) tại mọi điểm của $W$ buộc $F$ lồi trên $W$: cộng …". 974: tách tại dấu chấm phẩy: "…thay cho $\mathcal Y$. Đầu ra là $A(S;\xi)=\bar w_T$, và $\xi=\ldots$" |
| nhẹ | Cách in số lớn: dòng 1093, 1027, 1117 (xem mục 4) | Ô "$2{,}7136\cdot10^4$" lệch với các ô khác của cùng cột ($1600$, $1900$, $3104$, $7936$). $640\,000$ in dạng $6{,}4\cdot10^5$, khác Bài 02–03, nơi số nguyên lớn trong công thức được tách nhóm bằng `\,`. | Bài 02 dòng 504, 721, 729 ($25\,000$, $20\,000$, $100\,000$); Bài 03 dòng 13, 611 ($54\,330$, $18\,122$). | Theo quy ước đề xuất ở mục 4. |

## 4. Cách in số lớn trên toàn ghi chú

**Hiện trạng** (grep toàn tệp: số nguyên từ 4 chữ số, `\,`, dấu chấm nhóm, `\cdot10^k`):

- **Bốn chữ số, không tách nhóm, trong công thức:** $1600$ (804, 806, 810, 821, 824, 830, 880, 894, 902, 906, 1022, 1089, 1117, 1148, 1154, 1168, 1175–1176, 1181, 1310); $6400$ (804); $1900$, $3104$, $7936$ (1090–1092).
- **Năm chữ số:** chỉ có $2{,}7136\cdot10^4$ (1093), in dạng lũy thừa.
- **Sáu chữ số trở lên:** $6{,}4\cdot10^5$ (1027, 1117); $4\cdot10^6$ (1032, hai lần); $10^4$, $10^6$, $10^{10}$, $10^4\cdot10^6$ (9, 11, 17, 141, 853, 865, 868, 1081, 1085, 1094, 1115).
- **Không còn** `640\,000`, `27\,136`, "640.000" hay "27.136" ở đâu trong tệp. Không có số lớn nào nằm ngoài công thức.

Lệch duy nhất trong Bài 05 là ô bảng ở 1093. Lệch với các bài đã xuất bản là $6{,}4\cdot10^5$ (1027, 1117) và $2{,}7136\cdot10^4$ (1093), vì Bài 02–03 viết $25\,000$, $100\,000$, $54\,330$, $18\,122$ (Bài 03 dòng 465 còn có $1\,048$, bốn chữ số có tách nhóm).

**Quy ước đề xuất (một quy ước cho cả học phần), ghi vào `van-phong.md` §12:**

1. Số nguyên đếm được (số bước, số quan sát, cỡ mẫu) luôn viết trong công thức. Từ năm chữ số trở lên thì tách nhóm ba chữ số bằng `\,`: $27\,136$, $640\,000$. Bốn chữ số không tách nhóm: $1600$, $7936$. Cách này khớp Bài 02–03; riêng $1\,048$ ở Bài 03 là ngoại lệ, sửa khi chạm lại Bài 03.
2. Lũy thừa của 10 chỉ dùng khi số là một lũy thừa đúng hay một bội đơn giản của lũy thừa, xuất hiện tự nhiên trong phép tính ($10^4$, $10^6$, $10^{10}$, $4\cdot10^6$ so với $10^6$ một bước GD). Không đổi một kết quả tính được sang dạng phần thập phân nhân lũy thừa.
3. Số thập phân dùng `{,}` như hiện nay. Dấu chấm nhóm ("100.000") chỉ dùng khi một số lớn buộc phải đứng ngoài công thức; Bài 05 không còn trường hợp nào.

**Thay đổi trong Bài 05 theo quy ước này:**

| Dòng | Hiện tại | Sửa thành |
|---|---|---|
| 1093 | $2{,}7136\cdot10^4$ | $27\,136$ |
| 1027 | $6{,}4\cdot10^{5}$ | $640\,000$ |
| 1117 | $6{,}4\cdot10^5$ | $640\,000$ |

Số tiếng không đổi.

## 5. Văn phong của phần đã sửa (`no-ai-slop`, Detect)

- **§3a:** đạt. Nhãn ở 502–504 nay đều là cụm danh từ ("Phân bố rút không đều", "Xáo trộn lại …", "Oracle phụ thuộc thời điểm"), và mỗi dòng nêu cả mô tả lẫn hệ quả.
- **§7a:** Ví dụ 05.7 Kết luận (695) có bất đẳng thức bằng số. Ví dụ 05.10 Bước 2 và 4 in số chính xác.
- **§9a:** hai câu dài (bảng 3). Không có câu thuật lại, câu hỏi tu từ hay câu chuyển ý rỗng.
- **Thuật ngữ:**
  - "Độ chênh tối ưu" dùng ở 966 khớp định nghĩa ở 83.
  - "Sai số tối ưu thực nghiệm $\operatorname{opt}_S$" luôn đủ tên.
  - "Mức sàn sai số" nay chỉ ở 962 (một nghĩa), trừ chữ "mức sàn" còn lại ở 755 (bảng 3).
- **Mạch:**
  - §9 nay kết bằng văn xuôi (1037), là một giới hạn: (O2) chỉ đạt với xác suất cao; Mệnh đề 04.3 không ghép trực tiếp được.
  - §10 kết bằng câu giới hạn duy nhất (1111).
  - Bỏ con trỏ "(§8)" ở 474 không làm mất liên kết: Ví dụ 05.12 (947) vẫn nói một bước theo dưới gradient không nhất thiết làm $f$ giảm.
- **Mẫu `no-ai-slop`:** không có từ cấm, câu nhấn mạnh, câu kết châm ngôn hay đoạn tóm tắt cuối mục trong phần đã sửa.

## 6. Ngân sách

Thân bài $11\,973$. Các đề xuất ở bảng 3 và mục 4 cộng lại khoảng $+5-2-2-1=0$ tiếng. Không cần cắt thêm.
