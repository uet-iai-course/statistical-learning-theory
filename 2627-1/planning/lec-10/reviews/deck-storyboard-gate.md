# Duyệt cổng storyboard — bộ trang chiếu Bài 10

Người duyệt cổng (chỉ đọc), 2026-11-16. Đối tượng: `planning/lec-10/storyboard.md` (toàn bộ, mục 1–15). Đối chiếu:

- nguồn: `materials/lec-10/lecture-note.md` (đọc toàn bộ, kể cả Phụ lục A–D), `materials/lec-10/exercises.md` (đề và lời giải Bài tập 10.1, 10.2, 10.4, 10.5, 10.7);
- quy định: `CLAUDE.md` § Slide decks, `deck-build/common-brief.md` (gồm "Các quy định dễ sót" và bài học deck 01–08), `deck-build/brief-gate.md`, `deck-build/deck_lint.py` (LEAD25, nhãn, cụm cấm), nhật ký yêu cầu 2026-11-13 hàng 1–5 (hàng 4: dòng dẫn chỉ dùng khái niệm đã có, kể cả tên mạch);
- khuôn và tiền lệ: mục "Bộ trang chiếu" của `lec-06/…/lec-09/review-log.md` (đặc biệt Bài 09, T4: hệ quả trực tiếp giữ dòng "Chứng minh." trên trang phát biểu, không trang ý tưởng chứng minh riêng; bảng tổng kết tách hai trang ở Bài 06, 07, 08), `lec-09/reviews/deck-storyboard-gate.md`, mục 14 của `lec-09/storyboard.md`;
- ghi chú Bài 05 (Định nghĩa 05.10) và Bài 08 (Mệnh đề 08.12) cho các dòng "Nhắc lại:".

`no-ai-slop` chế độ Detect đã nạp (`SKILL.md`, `eval.md`). Script tính lại độc lập: `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-10/gate/chk.py` (phân số chính xác; sai phân hữu hạn; hạ gradient trực tuyến) và `…/lec-10/gate/sim.py` (chạy lại cả hai phần của Phụ lục C theo đúng giao thức). `count.py` của người lập chạy lại, kết quả trùng mục 15.

## 1. Kết luận

**Đạt khi sửa.** 0 chặn bàn giao, 1 nghiêm trọng, 11 trung bình, 18 nhẹ.

Mọi con số V1–V24, hình F1, F2 và các số mô phỏng của Phụ lục C tính lại độc lập khớp storyboard, ghi chú và tệp bài tập (mục 2). Phát biểu Bổ đề 10.3, Định lý 10.4, Mệnh đề 10.7, Hệ quả 10.8, Mệnh đề 10.13 trên mặt trang giữ đủ giả thiết của ghi chú (mục 3). Storyboard không chuyển kết quả lồi hay i.i.d. sang học tăng cường trên các trang nội dung: 3-09 nêu thiếu (C), 3-10 nêu $-J$ không lồi, 4-07 giới hạn cận Hoeffding cho chính sách cố định.

Lỗi tập trung ở các dòng rút gọn của mạch Tổng kết và ở vài trang bỏ một điều kiện:

- **N1 (nghiêm trọng, 7-02 dòng 2):** "giá trị nền chỉ đổi phương sai" bỏ điều kiện "là hàm của lịch sử" của Hệ quả 10.8, trong khi Ví dụ 10.9 (4-04) và Bài tập 10.2(b) (4-08) của chính deck là phản ví dụ.
- Các trung bình đáng chú ý: 7-02 dòng 1 gán sai nguyên nhân cho (C); 7-00 dòng dẫn bỏ điều kiện luật chuyển; 3-05 dạng tổng quát của kỹ thuật thiếu điều kiện tập giá trị và "phần thưởng bị chặn"; 2-03 (PT) thiếu hai vế; 3-10 "Nhắc lại:" Mệnh đề 08.12 thiếu loại bảo đảm; "Trực quan." của Định lý 10.4 là bước 3 của chứng minh; Hệ quả 10.8 không có "Trực quan."; 4-06 không liệt kê dữ kiện; 3-07 "Diễn giải:" dùng số không có trên trang; 5-02 ghi chú diễn giả có câu nguồn gốc; 7-01 bảng năm hàng một trang trái tiền lệ.

## 2. Tính lại con số

| Mã | Đối tượng | Kết quả tính lại | Khớp |
|---|---|---|---|
| V1 | câu hỏi mở đầu (1-06) | $0{,}2+0{,}6q$: $0{,}5$; $0{,}74$; $L_A(1)=\tfrac12$ | có |
| V2 | Ví dụ 10.1 | $\pi=\tfrac34$, $J=\tfrac52$, $J'=\tfrac38$ | có |
| V3 | Ví dụ 10.2 | tám xác suất $\tfrac15,\tfrac15,\tfrac1{20},\tfrac1{20},\tfrac1{20},\tfrac1{20},\tfrac15,\tfrac15$ (tổng $1$), $R=3,1,0,1,4,2,1,2$; $Q(1)=1{,}7$, $Q(0)=1{,}8$; $J(0)=\tfrac74$ | có |
| V4 | Ví dụ 10.3 | $J'=\tfrac12$; $\mathbb E\partial_\theta\ln p_\theta=-1/\theta$; $\mathbb E[A(-1/\theta)]=-\tfrac12$ | có |
| V5 | Ví dụ 10.4 | $\pm0{,}75$; $\mathbb E\hat g=\tfrac38$; kì vọng gradient log $0$ | có |
| V6 | Ví dụ 10.5 | $(-\tfrac1{40};\,\tfrac14;\,-\tfrac18)$ bằng tổng; sai phân hữu hạn $(-0{,}025000;\,0{,}250000;\,-0{,}125000)$ | có |
| V7 | Ví dụ 10.6 | đạo hàm đúng $0{,}125$ (sai phân hữu hạn), $J=1{,}75$; $\mathbb E[r_0(A_0-\tfrac12)]=-\tfrac14$ | có |
| V8 | Ví dụ 10.7 | $\theta=\ln0{,}6=-0{,}51083$; $J=0{,}375$; $J''_\theta=0{,}17578$; đi lên từ $-1$: $J\to0{,}59995$; từ $-0{,}4$: $J\to0{,}99995$ | có |
| V9 | Bài tập 10.1(a), (b) | $\tfrac14$; $1$; $\tfrac34$; giá trị $3$, $0$; $\operatorname{Var}=\tfrac{27}{16}$ ($3$ lần $J'^2$) | có |
| V10, F1 | Ví dụ 10.8 | bốn hàng của bảng; $\operatorname{Var}(\hat g_b)=(12b^2-36b+27)/64=\tfrac3{16}(b-\tfrac32)^2$; $147/27=5{,}44$; trục dọc $[0;\,2{,}6]$ chứa giá trị $2{,}567$ tại $b=5{,}2$ | có |
| V11 | Ví dụ 10.9 | $\tfrac3{16}$; $\kappa=1$: $\tfrac3{16}$; $\kappa=2$: $0$ | có |
| V12 | Ví dụ 10.10 | kì vọng của cả ba $(-\tfrac1{40};\tfrac14;-\tfrac18)$; phương sai (i) $\tfrac{1619}{1600},\tfrac{11}{16},\tfrac{79}{320}$; (ii) $\tfrac{1619}{1600},\tfrac9{16},\tfrac3{64}$; (iii) $\tfrac{197}{800},\tfrac1{16},\tfrac1{64}$; vết $1{,}94625$; $1{,}62125$; $0{,}324375$; tỉ số $6{,}000$ và $4{,}998$; Bước 3: $0$ và $1$ | có |
| V13 | Ví dụ 10.11 | liệt kê đủ bốn tổ hợp $(A,X)$: $J'(0)=0{,}05$; $0{,}1225$; $27{,}6225$; $0{,}06$ (cả hai $c$); tỉ số $225{,}49$ | có |
| V13s | Phụ lục C, REINFORCE | chạy lại 100 hạt giống: $c=0$ không/có: $0{,}969/0{,}011$, $0{,}970/0{,}009$; $c=10$ không: $0{,}509$, $0{,}498$, $0{,}001$–$1{,}000$, **49** lần dưới $0{,}5$; có: $0{,}969$, $0$ lần | có (trùng từng chữ số của bảng) |
| V14 | Ví dụ 10.12 | $0{,}171788\le0{,}1718$; $11\,804{,}41\Rightarrow11\,805$; câu ôn nhanh 1: $0{,}060736\le0{,}0608$ | có |
| V15 | Bài tập 10.2(b), (c) | $\tfrac9{40}=0{,}225$; kì vọng $\tfrac14$, mô-men $\tfrac{11}{20}$, phương sai $\tfrac{39}{80}=0{,}4875$ | có |
| V16 | Ví dụ 10.13 | $0{,}81$; $-0{,}11$; $0{,}10$, $0{,}17$, $0{,}135$; $0{,}025$; ma trận thứ hai: $0{,}005$; $0{,}07$, $0$; tới hàng $K-1$: $-0{,}03$ | có |
| V17 | Bài tập 10.4(a), (d) | $0{,}75333$; $-0{,}19$; $0{,}15$, $0{,}28$, $0{,}215$; $0{,}015$; $\min=0{,}60$, cách $0{,}86$ là $0{,}26$ | có |
| V18, F2 | Mệnh đề 10.13, Ví dụ 10.14 | năm hàng $w_\lambda$, $L_A$, $L_B$, tổng, $\alpha$; $\sqrt{2L_A}+\sqrt{2L_B}=1$ tại cả năm điểm; $\min_{[0,1]}(L_A+L_B)=0{,}25$ tại $w=\tfrac12$; trục $[0;\,0{,}55]$ chứa mọi điểm | có |
| V19 | Ví dụ 10.15 | $v=\tfrac23$, $L_B=\tfrac29$; $v=\tfrac13$, $L_B=\tfrac89$ | có |
| V20 | Ví dụ 10.16 | $L_A(\tfrac12)=\tfrac58$; $\tfrac1{8M}$: $0{,}125$; $0{,}0125$; $0{,}00125$ | có |
| V20s | Phụ lục C, phát lại | chạy lại 20 hạt giống theo thứ tự rút đã ghi: rủi ro A $0{,}624$; $0{,}331$; $0{,}256$; $0{,}252$; $w$ cuối $0{,}998$ ($0{,}049$), $0{,}614$ ($0{,}198$), $0{,}509$ ($0{,}073$), $0{,}498$ ($0{,}087$); rủi ro B $0{,}126$; $0{,}218$; $0{,}248$; $0{,}255$ | có (trùng mọi số của bảng) |
| V21 | Ví dụ 10.17 | so sánh tốt nhất $125$; cận $\sqrt{1000}=31{,}6228\le31{,}63$; $\eta=1/\sqrt T$: hối tiếc $-116{,}967$, $w_{T+1}=1-1{,}05\cdot10^{-7}$, $L_A=0{,}4999999$; $\eta_t=1/t$: $0{,}18765$, $w=\tfrac12$, $L_A=\tfrac18$ | có |
| V22 | Bài tập 10.5(c) | $\tfrac15$; $\tfrac12$; $\tfrac15$; $\lambda\Omega=4$ khi $\alpha=\tfrac12$ | có |
| V23 | Bài tập 10.7(i) | miền $[0,6]$ cho Ví dụ 10.2, bán kính $1{,}5$ lần | có |
| V24 | §12 (a), (b), (d), (e) | $J'(0)=\tfrac12$, giá trị $1$, $0$; $\lambda=\tfrac14$: $\tfrac45$, $\tfrac8{25}$, $\tfrac1{50}$, $\tfrac15$, tổng $\tfrac{17}{50}\ge\tfrac14$ | có |

Hình: F1 là đồ thị đúng công thức Ví dụ 10.8 Bước 1, mọi nhãn có trong bảng 4-04; F2 là đồ thị tham số đúng của Mệnh đề 10.13(c), đường nét đứt tiếp xúc đúng tại $(\tfrac18;\tfrac18)$. Không có ví dụ mới mang số mới trên mặt trang.

## 3. Phát biểu kết quả trên mặt trang so với ghi chú

| Khối | Trang | Giả thiết | Bảo đảm | Nhận xét |
|---|---|---|---|---|
| Bổ đề 10.3 | 3-01 | đủ ba thành phần ($\mathcal T$ hữu hạn không phụ thuộc $\theta$; $p_\theta$ hàm xác suất, $\Theta$ mở; khả vi) | đồng nhất thức, (a), (b) đúng | dòng "Chứng minh." đúng đẳng thức của ghi chú |
| Định lý 10.4 | 3-03 | (MDP), (Π), $\tau\sim p_\theta$ | đồng nhất thức; $J$ khả vi; không chệch; trung bình $m$ lượt | "m lượt độc lập: hiệp phương sai chia cho $m$" thiếu chữ "trung bình" (L5); "Trực quan." là bước chứng minh (T6) |
| Nhận xét 10.5 | 3-05 | thiếu "phần thưởng bị chặn" | — | xem T3 |
| Mệnh đề 10.7 | 4-01 | như Định lý 10.4 | (a), (b) đúng | — |
| Hệ quả 10.8 | 4-02 | như Định lý 10.4; $b_t(\mathcal F_t)$ không phụ thuộc $A_t$ hay biến sau | đồng nhất thức | thiếu "Trực quan." (T7) |
| Nhận xét 10.9 | ghi chú diễn giả 4-04, 4-05 | — | — | đúng (i) entropy $\ln2$, (ii) ba trường hợp |
| Mệnh đề 10.13 | 6-02 | $W=\mathbb R$, $L_A$, $L_B$, $w^{(1)}=0$, $\lambda\ge0$, $\Omega=1$ | tất định; (a)–(d) đúng, "dấu bằng chỉ tại $w=\tfrac12$" đặt đúng ở bất đẳng thức thứ hai | — |
| Nhận xét 10.14 (đọc thêm) | ghi chú diễn giả 6-04 | — | — | ghi "Phần đọc thêm", đúng quy định [O] |
| Nhận xét 10.16 | 6-06 | thiếu "$w_1\in W$ tất định" | tất định, mọi dãy; $RG\sqrt T$ | L1 |
| Mệnh đề 08.12 (nhắc lại) | 3-10 | ba điều kiện của ghi chú (bỏ "hằng") | thiếu "theo kì vọng" | T5 |

Phân bố quỹ đạo do chính sách sinh (2-04), dữ liệu phụ thuộc tham số (2-01, 2-05), không chệch có điều kiện theo các lượt trước (3-09), giá trị nền là hàm của lịch sử (4-02, 4-03), quên và hối tiếc (5-02, 6-06, 6-07) đều đúng ghi chú. Chỗ lệch nằm ở các dòng rút gọn (7-00, 7-02) và ở (PT) (2-03).

## 4. Ý kiến về các điểm của mục 11 (điều phối viên quyết định)

1. **54 trang.** Đồng ý giữ 54 (dưới trần 55, có lý do; Bài 08, 09 đã chấp nhận 54–55). Hai phương án về 52 đều làm mất một bước bắt buộc. Nếu chấp nhận ý kiến ở điểm 2 và gộp hàng ở 7-01 (T11), bảng tổng kết vẫn một trang, nên không cần trang 55.
2. **Bổ đề 10.3 không có trang ý tưởng chứng minh riêng.** Đồng ý, theo tiền lệ T4 của Bài 09 (Hệ quả 09.13 giữ dòng "Chứng minh." trên trang phát biểu). Bổ đề là công cụ; chứng minh hai dòng; Ví dụ 10.3 ngay sau làm bước "bỏ giả thiết". Cùng tiền lệ đó gộp hàng của kết quả phụ vào hàng kết quả chính ở 7-01: nên gộp hàng Bổ đề 10.3 vào hàng Định lý 10.4 (T11).
3. **Mạch 2 không có trang bài tập.** Đồng ý. Bài tập 10.1(a) chỉ là đạo hàm của Ví dụ 10.1 với số khác; tách thành trang riêng thêm một trang mà không thêm ý.
4. **Trang kỹ thuật 3-05.** Đồng ý đặt ở Bài 10 (storyboard Bài 09, mục 11 điểm 3 đã được chấp nhận trong `lec-09/review-log.md`) và tiêu đề "Đạo hàm của kì vọng qua gradient log". **Không dùng** phương án "Gradient log của một kì vọng": cụm này đọc thành $\nabla\ln\mathbb E f$, sai nghĩa. Dạng tổng quát trên trang cần điều kiện (T3).
5. **Trang ý tưởng chứng minh chung 4-03.** Đồng ý: Phụ lục B Bước 4 chứng minh cả hai bằng một bước; trên từng kết quả thứ tự vẫn là phát biểu → ý tưởng chứng minh. Bước 3 của 4-03 nêu rõ bước nào cho kết quả nào.
6. **Ví dụ 10.10 một trang.** Đồng ý.
7. **Câu chữ bài tập rút gọn.** Đồng ý (tiền lệ Bài 08–09), với điều kiện câu đầy đủ ở ghi chú diễn giả như đã ghi; 5-04 không chép "(giá trị giả định)" là bắt buộc.
8. **Nhận xét 10.14 và Ví dụ 10.15 chỉ ở ghi chú diễn giả.** Đồng ý: khối đọc thêm; giữ 6-05 vì giới hạn "phát lại hữu hạn" của §10 cần trên mặt trang.
9. **Bài tập tổng hợp 10.7(i).** Đồng ý: lời giải chỉ cần Định nghĩa 10.2, Ví dụ 10.12, (T1), (T3), (C), đều đã trên mặt trang. 10.3(d) cần (G1) và Hệ quả 05.15 chưa có trên mặt trang. Bài chỉ chạm Phần A; Phần B đã có câu hỏi tự kiểm tra 3–4.
10. **F2 và Bài tập 10.5(b).** Ý kiến: **không lộ lời giải.** Đề 10.5(b) đã nêu sẵn hai tập ($[0,1]$ và $(0,1]$) và chỉ yêu cầu chứng minh; F2 không chứa lập luận nào (ba trường hợp $w<0$, $[0,1]$, $w>1$). Giữ đường cong. Không ghi nhãn "tối ưu Pareto" và không ghi nhãn đầu mút $w=0$, như storyboard đã định.
11. **Nhận xét 10.16 không có dòng chứng minh.** Đồng ý (phác thảo; trang đã 54). Cần thêm "$w_1\in W$ tất định" và tách nghĩa của $R$ (L1, L2); nếu thêm dòng chứng minh thì phải cắt "Câu hỏi:" như storyboard đề xuất.
12. **$R$ hai nghĩa.** Deck theo ghi chú. Đề nghị thêm ba âm tiết "($R$: bán kính)" ở 6-06 và viết "$\lVert w_1-u\rVert\le R$" trong ô giả thiết của hàng Nhận xét 10.16 ở 7-01, vì hàng đó đứng cạnh $R_{\ge t}$ (L2). Đề xuất sửa ghi chú ở mục 13 của storyboard hợp lý.
13. **Các dòng "Nhắc lại:".** Đồng ý, trừ 3-10 (thiếu loại bảo đảm, T5) và thứ tự dòng ở 3-05 (L8).
14. **Mật độ.** Trung vị $50$ trên 42 trang nội dung, vượt mục tiêu $40$ nhưng thấp hơn trung vị lúc chấp nhận của Bài 06–09 (55; 55; 50–51; 53). Sáu trang ở $57$–$60$ có biên $0$–$3$; các sửa của báo cáo này thêm chữ ở 2-03, 3-05, 3-10, 4-02, 4-06, 7-02, nên mục 6 nêu cắt bù cụ thể. Bảy dòng vượt 20 âm tiết chưa được ghi ngoại lệ (L13).
15–17. Đồng ý.
18. **Dòng khép học phần (7-06).** Có cơ sở: §12 (f) và Phụ lục D liệt kê đúng bốn bài toán. Viết "phân lớp có giám sát" như ghi chú (L15). Không có liên kết bài sau là đúng (bài cuối).

## 5. Bảng phát hiện

| Mã | Mức độ | Trang chiếu | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|---|
| N1 | nghiêm trọng | 7-02 dòng 2 | Dòng trả lời vấn đề trung tâm bỏ giả thiết của Hệ quả 10.8; đọc thành mọi giá trị nền chỉ đổi phương sai. Cùng dòng viết "Gradient vẫn không chệch": tính không chệch là của ước lượng | storyboard: "Gradient vẫn không chệch khi luật chuyển không phụ thuộc $\theta$; giá trị nền chỉ đổi phương sai." Ghi chú Hệ quả 10.8: "một hàm $b_t(\mathcal F_t)$ của lịch sử … không phụ thuộc $A_t$"; Ví dụ 10.9: "Giá trị nền $\kappa A$ … ước lượng bị chệch" | Tách hai dòng: "Ước lượng một lượt không chệch khi $P$ không phụ thuộc $\theta$." / "Giá trị nền là hàm của lịch sử chỉ đổi phương sai." (xem mục 6 cho cả trang) |
| T1 | trung bình | 7-02 dòng 1, dòng 4 | (a) Dòng 1 gán việc (C) không đúng cho tính phụ thuộc của dữ liệu; ghi chú nêu hai nguyên nhân riêng. (b) Dòng 4 "xung đột buộc $L_A+L_B\ge\tfrac14$" bỏ "trong ví dụ bậc hai". (c) Bốn dòng cùng khuôn "X: Y" (no-ai-slop: robotic symmetry, colon reveal) | "Dữ liệu phụ thuộc tham số: (T1) và (C) không còn đúng."; Phụ lục D: "(T1), trừ khi đánh giá một chính sách cố định (Ví dụ 10.12), và (C) vì $-J$ không lồi (Ví dụ 10.7)"; §10: "hai nhiệm vụ xung đột buộc $L_A+L_B\ge\tfrac14$ trong ví dụ bậc hai" | "(T1) không đúng vì dữ liệu phụ thuộc tham số; (C) không đúng vì $-J$ không lồi."; dòng 4: "Nhiệm vụ thay đổi: cần giao thức nêu trước; hối tiếc tĩnh không chặn độ quên." và chuyển $L_A+L_B\ge\tfrac14$ (đã có ở 7-01) vào ghi chú diễn giả |
| T2 | trung bình | 7-00 `strand-lead` | Dòng dẫn bỏ điều kiện luật chuyển; "gradient không chệch" thay cho ước lượng. Ví dụ 10.6 của deck là phản ví dụ | "Dữ liệu do chính sách sinh ra vẫn cho gradient không chệch, còn nhiệm vụ thay đổi đòi một giao thức nêu trước." Bài học deck 01: "Phát biểu rút gọn giữ đủ giả thiết" | "Khi môi trường không phụ thuộc tham số, gradient ước lượng được không chệch; nhiệm vụ thay đổi cần một giao thức nêu trước." (≈ 22 âm tiết, dưới LEAD25) |
| T3 | trung bình | 3-05 dòng 1, 3 | Dạng tổng quát của kỹ thuật chỉ nêu "$f$ không phụ thuộc $\theta$", thiếu điều kiện tập giá trị hữu hạn, cố định (chính chỗ Ví dụ 10.3 hỏng); dòng Nhận xét 10.5 thiếu "phần thưởng bị chặn" | "$\nabla_\theta\mathbb E_{\tau\sim p_\theta}f(\tau)=\mathbb E[\ldots]$ khi $f$ không phụ thuộc $\theta$"; Bổ đề 10.3: "$\mathcal T$ hữu hạn, không phụ thuộc $\theta$"; Nhận xét 10.5: "**Giả thiết.** Phần thưởng bị chặn và ba điều kiện sau" | Dòng 1: "… khi $\mathcal T$ hữu hạn, cố định và $f$ không phụ thuộc $\theta$."; dòng 3 thêm "$R$ bị chặn"; cắt bù ở mục 6 |
| T4 | trung bình | 2-03 dòng 4 | (PT) bỏ hai vế của giả thiết: phân bố của $r_t$ không phụ thuộc $\theta$ và $r_t$ không ảnh hưởng tới bước sau; đây là điều làm Hệ quả 10.8 "dưới (PT)" ở 4-06 đúng | "(PT): $\mathbb E[r_t\mid S_t=s,A_t=a]=r(s,a)$."; ghi chú §2 (PT) có đủ ba vế | Chuyển (PT) sang 4-06, nơi duy nhất mặt trang dùng nó, với đủ ba vế (thứ tự khái niệm vẫn đúng: định nghĩa ngay trước khi dùng); 2-03 giảm 1 dòng |
| T5 | trung bình | 3-10 dòng 5 | "Nhắc lại:" Mệnh đề 08.12 không nêu loại bảo đảm (theo kì vọng, cho trung bình $\lVert\nabla F(w_t)\rVert^2$) và bỏ "hằng"; ghi chú diễn giả không nói mệnh đề là *đọc thêm* ở Bài 08 | storyboard: "Mệnh đề 08.12 cho $F=-J$ điểm dừng xấp xỉ khi …, $\eta\le1/\beta$"; ghi chú Bài 08: "— đọc thêm"; "**Bảo đảm.** Theo kì vọng …"; ghi chú Bài 10: "độ dài bước hằng $\eta\le1/\beta$". Bài 09 N2 cùng loại | Hai dòng: "**Nhắc lại:** Mệnh đề 08.12 cho $F=-J$: $J$ $\beta$-trơn, bị chặn trên; phương sai có điều kiện bị chặn; $\eta$ hằng, $\eta\le1/\beta$." / "Bảo đảm: điểm dừng xấp xỉ, theo kì vọng." Ghi chú diễn giả thêm "(đọc thêm ở Bài 08)" |
| T6 | trung bình | 3-03 dòng 1 | "Trực quan." chép bước 3 của chứng minh (thừa số chính sách, lôgarit của tích), trùng 3-04 bước 3; trái bài học deck 02 | "**Trực quan.** Trong $p_\theta(\tau)$ chỉ các thừa số $\pi_\theta(a_t\mid s_t)$ chứa $\theta$; lôgarit biến tích thành tổng." vs 3-04 bước 3 | Dùng câu cơ chế của ghi chú (cuối chứng minh Định lý 10.4): "**Trực quan.** Thừa số gradient log mang ảnh hưởng của $\theta$ lên phân bố dữ liệu; trung bình phần thưởng đã thu thiếu thừa số này." Bỏ dòng cuối 3-04 trùng ý (−14 âm tiết ở 3-04) |
| T7 | trung bình | 4-02 | Hệ quả 10.8 là kết quả chính (bảng mục 4) mà không có "Trực quan."; mục 7 ghi "4-02 dòng cuối (chọn $b_t$ để giảm phương sai)", là hệ quả chứ không là trực quan | storyboard mục 7, hàng Hệ quả 10.8; quy định "Concept journey … intuition ('Trực quan.')" | Thêm: "**Trực quan.** Gradient log có trung bình $0$ khi biết lịch sử (Bổ đề 10.3(b)); trừ một số đã biết trước hành động không dời trung bình." (cơ sở: dòng $\square$ của chứng minh Bổ đề 10.3); cắt bù dòng "Giá trị nền (baseline): …" thành "Giá trị nền (baseline): không phụ thuộc hành động đang xét." |
| T8 | trung bình | 4-06 | Trang mở ví dụ không liệt kê dữ kiện (hai nội dung, xác suất nhấp $0{,}6$; $0{,}4$; $\theta=0$); storyboard mục 4 ghi "dữ liệu ở dòng (PT) của 2-03" nhưng mặt trang 2-03 không có dữ kiện đó, chỉ ghi chú diễn giả | quy định "An example's first slide lists its data at once"; mặt trang 4-06: "$R(\tau)=c+X$, nhấp $X\in\{0,1\}$" | Dòng đầu: "**Ví dụ 10.11.** Hiển thị nội dung $A\in\{0,1\}$, $\theta=0$; nhấp $X=1$ với xác suất $0{,}6$ ($A=1$), $0{,}4$ ($A=0$); $R(\tau)=c+X$." Kèm (PT) theo T4; gộp dòng $J$ với "chính sách tốt nhất" (L6) |
| T9 | trung bình | 3-07 dòng 6 | "Diễn giải:" dùng $1{,}7$; $1{,}8$; $2$; $\tfrac12$, không có trên trang 3-07 | "**Diễn giải:** hành động $1$ mất $1$ …$(0{,}8-0{,}2)(2-\tfrac12)=0{,}9$ …: $\tfrac14(1{,}7-1{,}8)=-0{,}025$"; quy định: "A 'Diễn giải:' uses only numbers shown on the same slide" | "**Nhắc lại:** chọn $1$ hay $0$ ở $s_0$ cho $1{,}7$ hay $1{,}8$ (Ví dụ 10.2)." rồi câu thường: "Do đó $\partial J/\partial\theta_{s_0}=\tfrac14(1{,}7-1{,}8)=-0{,}025$." Phân tích $0{,}9$ chuyển vào ghi chú diễn giả |
| T10 | trung bình | 5-02 ghi chú diễn giả | Câu nguồn gốc trong ghi chú diễn giả | "Ma trận và các độ đo là quy ước của học phần; không nguồn nào của học phần định nghĩa chúng."; quy định speaker notes: no provenance sentences; bộ nhớ tác giả "No provenance sentences" | Xóa câu |
| T11 | trung bình | 7-01 | Bảng năm hàng $77/80$ trên một trang, trong khi Bài 06, 07, 08 đều phải tách bảng tổng kết thành hai trang vì cao quá khung; mục 16 không ghi 7-01 là trang rủi ro. Hàng Nhận xét 10.16 không nêu $\lVert w_1-u\rVert\le R$ nên $R$ đứng cạnh $R_{\ge t}$ mà không được đặt nghĩa | `lec-06/review-log.md` dòng 353 ("bảng năm hàng cao 1022 px"); `lec-07`, `lec-08` cùng tách | Gộp hàng Bổ đề 10.3 vào hàng Định lý 10.4 (tiền lệ T4 Bài 09): "Định lý 10.4 (cùng Bổ đề 10.3) … \| $\mathcal T$ hữu hạn, cố định; (MDP); (Π) \| đạo hàm $\sum p_\theta=1$; bỏ $\ln\mu_0$, $\ln P$"; thêm $\lVert w_1-u\rVert\le R$ vào ô hàng cuối; ghi 7-01 vào mục 16 để kiểm `footer_check.py` |
| L1 | nhẹ | 6-06 dòng 4 | Giả thiết Nhận xét 10.16 thiếu "$w_1\in W$ tất định" (chỉ ở ghi chú diễn giả) | ghi chú: "(C) với $F=\ell(\cdot,z)$ cho mọi $z$; $w_1\in W$ tất định; …" | Thêm "$w_1\in W$ tất định" |
| L2 | nhẹ | 6-06, 7-01 | $R$ hai nghĩa (mục 11, điểm 12) | 6-06 "$\lVert w_1-u\rVert\le R$"; 7-01 hàng 3 $R_{\ge t}$, hàng 5 $RG\sqrt T$ | 6-06: "$\lVert w_1-u\rVert\le R$ ($R$: bán kính)"; 7-01 theo T11 |
| L3 | nhẹ | 2-00, 4-00 `strand-lead` | Dòng dẫn dùng khái niệm chưa có và không nằm trong tên mạch: "tác tử" (2-00, đặt ở 2-01), "theo lịch sử" (4-00, đặt ở 4-01). 5-00 dùng "ma trận đánh giá" có trong tên mạch, đạt | nhật ký hàng 4: "chỉ dùng từ thông thường và khái niệm đã có trước mạch (mạch trước, bài trước, tên mạch)" | 2-00: "Robot chọn hành động theo xác suất đang học, nên phân bố của dữ liệu đổi khi xác suất đó đổi." 4-00: "Trừ một giá trị nền biết trước hành động không đổi kì vọng của ước lượng nhưng đổi phương sai." |
| L4 | nhẹ | 3-04 dòng 4; tiêu đề 3-08 | "Bỏ (MDP)" rộng hơn điều bị bỏ: Ví dụ 10.6 chỉ bỏ "$P$ không phụ thuộc $\theta$", vẫn giữ tập hữu hạn | "Bỏ (MDP): bước 3 còn số hạng $\nabla\ln P$."; ghi chú: "Ví dụ dưới đây bỏ giả thiết luật chuyển không phụ thuộc $\theta$" | "Khi $P$ phụ thuộc $\theta$: bước 3 còn số hạng $\nabla\ln P$."; dòng mô tả 3-08 sửa tương tự |
| L5 | nhẹ | 3-03 dòng 5 | Mất chữ "trung bình" | "$m$ lượt độc lập: hiệp phương sai chia cho $m$"; ghi chú: "trung bình trên $m$ lượt độc lập cũng không chệch, với ma trận hiệp phương sai chia cho $m$" | "Trung bình $m$ lượt độc lập: không chệch, hiệp phương sai chia cho $m$." |
| L6 | nhẹ | 4-06 dòng 3 | "chính sách tốt nhất không đổi": trong họ sigmoid cận trên đúng không đạt, nên không có chính sách tốt nhất trong họ; ghi chú nói "Cộng $c$ chỉ dịch $J$" | ghi chú Ví dụ 10.11 Bước 1 | "… $J'(0)=0{,}05$ với mọi $c$: cộng $c$ chỉ dịch $J$." |
| L7 | nhẹ | 6-02 dòng 1 | "Trực quan." chép bước 1 của 6-03 (bất đẳng thức tam giác) | "mỗi $w$ cách hai tâm tổng cộng ít nhất $1$" vs 6-03 bước 1 | "**Trực quan.** $L_A$, $L_B$ có tâm $0$ và $1$: kéo $w$ về một tâm đẩy nó xa tâm kia." |
| L8 | nhẹ | 3-05 | Dòng "Nhắc lại:" (dòng 4) đứng sau dòng 3 dùng nó (hàm trội của Bài 09) | bài học: "'Nhắc lại:' đứng trước công thức dùng nó" | Đổi thứ tự dòng 3 và 4 |
| L9 | nhẹ | 6-03 bước 1–4 | Ngoặc đầu mục ghi phần của kết quả ("((a))", "((b), (c))"), không ghi giả thiết dùng ở bước, khác quy ước `<ol>` của deck Bài 06 | storyboard mục 6, quy ước chung: "giả thiết dùng ở bước ghi trong ngoặc đầu mục" | Bước 3: "($w^{(1)}=0$, $\Omega=1$) …"; bước 1–2: "($L_A$, $L_B$ bậc hai, tâm $0$, $1$) …"; phần kết quả viết cuối mục: "… : (a)" |
| L10 | nhẹ | 1-03 mục 3 | Mục tiêu bỏ điều kiện "không phụ thuộc hành động" | "Chứng minh giá trị nền giữ kì vọng …"; ghi chú mục tiêu 3: "giá trị nền không phụ thuộc hành động giữ kì vọng" | "Chứng minh giá trị nền không phụ thuộc hành động giữ kì vọng; tính phương sai, chỉ ra trường hợp chệch." (+4 âm tiết; trang đang 80/80, nên cắt bù 4 âm tiết ở một mục khác, người viết chọn) |
| L11 | nhẹ | 5-03 dòng 4 | "$0{,}135\ne0{,}11$": $0{,}11$ không có tên trên trang (là đối của chuyển đổi ngược $-0{,}11$) | storyboard 5-03 | "trung bình $0{,}135$, lớn hơn $0{,}11$ = đối của chuyển đổi ngược: nhiệm vụ 1 đạt đỉnh ở hàng 2." |
| L12 | nhẹ | 7-03 dòng 4 | "(T3): miền $[Hr_{\min},Hr_{\max}]$" mơ hồ | lời giải 10.7(i): "(T3) thay bằng miền $[Hr_{\min},Hr_{\max}]$ … bán kính … nhân với $H(r_{\max}-r_{\min})$" | "(T3) thay bằng miền $[Hr_{\min},Hr_{\max}]$" |
| L13 | nhẹ | 2-03, 3-10, 3-11, 4-02, 5-04, 6-07, 6-08 | Dòng vượt 20 âm tiết (21; 22; 23; 21; 27; 22; 29 theo `count.py`) không được ghi ngoại lệ ở mục 14–15 | `count.py` chạy lại | Tách dòng 5-04 (a)/(d) và 6-08 (c) thành hai dòng (các trang còn ≤ 6 dòng); các dòng 21–23 ghi lý do hoặc cắt |
| L14 | nhẹ | 4-03 ghi chú diễn giả | "Nhắc lại: kì vọng có điều kiện theo lịch sử (Bài 05)": ở Bài 05, $\mathcal F_t$ là σ-đại số của $\xi_1,\ldots,\xi_t$; ở đây là bộ $(S_0,\ldots,S_t)$ | Định nghĩa 05.10; ghi chú §6 "kì vọng có điều kiện theo $\mathcal F_t$ là theo bộ này" | Ghi chú diễn giả thêm một câu: "Ở đây $\mathcal F_t$ là bộ biến quan sát được trước $A_t$; kì vọng có điều kiện theo bộ này dùng như Bổ đề 05.12." |
| L15 | nhẹ | 7-06 dòng 4 | Tên bài toán khác ghi chú | "phân lớp, ước lượng mật độ, …"; §12 (f): "phân lớp có giám sát" | "Bốn bài toán: phân lớp có giám sát, ước lượng mật độ, tối ưu chính sách, học liên tục." (bỏ "của học phần", số âm tiết không đổi) |
| L16 | nhẹ | 6-05 ghi chú diễn giả | Câu nói về trạng thái của số liệu (hedge) | "Các số mô phỏng là kết quả thí nghiệm cho một thiết lập: $20$ hạt giống, một vòng SGD trên mỗi nhiệm vụ." | "Mô phỏng dùng $20$ hạt giống, một vòng qua dữ liệu của SGD trên mỗi nhiệm vụ." ("vòng qua dữ liệu" theo `thuat-ngu.md` dòng 319) |
| L17 | nhẹ | storyboard mục 1 | Danh sách `.table-scroll` gồm 2-01, 3-07, 6-08, 7-02 (không có bảng ở mục 6) | mục 1 vs mục 6 | Sửa danh sách: 2-05, 4-04, 4-05, 5-03, 5-04, 6-04, 6-07, 7-01, 7-05 |
| L18 | nhẹ | storyboard mục 4 vs mục 6, 14 | Mục 4 (Mệnh đề 10.7, cột (c)) ghi "một dòng 'Kỹ thuật.' trên 4-03", mặt trang 4-03 không có dòng đó, mục 14 ghi "một bước của ý tưởng chứng minh" | mục 4, hàng Mệnh đề 10.7 | Chốt một cách; khuyến nghị theo mục 14 (đồng nhất thức đã là bước 1) và sửa mục 4 |

Không phát hiện: cụm cấm của `deck_lint.py` (đã quét mục 6), "Nhu cầu:", "Muốn …, phải …", "Đáp án", tiêu đề "Kỹ thuật: …", nhãn ngoài danh sách, công thức vẽ vào SVG, "minh họa"/"giá trị giả định" trên mặt trang hay chú thích.

## 6. Cắt cụ thể để giữ trần sau khi sửa

Người viết deck đếm lại trên HTML; số dưới đây ước bằng `count.py`.

- **7-02 (59 → ≈ 59), năm dòng:** (1) "(T1) không đúng vì dữ liệu phụ thuộc tham số; (C) không đúng vì $-J$ không lồi." (≈ 16) (2) "Ước lượng một lượt không chệch khi $P$ không phụ thuộc $\theta$." (≈ 10) (3) "Giá trị nền là hàm của lịch sử chỉ đổi phương sai." (≈ 11) (4) "Cận với xác suất ít nhất $1-\delta$ chỉ cho chính sách cố định." (≈ 11) (5) "Nhiệm vụ thay đổi: cần giao thức nêu trước; hối tiếc tĩnh không chặn độ quên." (≈ 15). Nếu vượt 60, dòng 1 viết "(T1) sai vì …; (C) sai vì …".
- **3-05 (60):** dòng 2 "Dùng khi phân bố phụ thuộc tham số, hàm thì không (Định lý 10.4)." → "Dùng khi lấy mẫu theo $p_\theta$ (Định lý 10.4, Mệnh đề 10.7)." (−4); bù T3 (+5, +3); dòng 5 "Hỏng khi giá di chuyển theo $\theta$ (Ví dụ 10.3)." → "Giá di chuyển theo $\theta$: hỏng (Ví dụ 10.3)." (−1). Nếu còn vượt, bỏ "(Định lý 10.4, Mệnh đề 10.7)" vì ghi chú diễn giả đã nêu.
- **3-03 (50) và 3-04 (47):** T6 đổi "Trực quan." (+≈ 8 ở 3-03) và bỏ dòng cuối 3-04 (−14).
- **3-10 (49):** T5 (+≈ 5).
- **4-02 (53):** T7 (+≈ 18) bù bằng: rút dòng 1 (−3), dòng cuối "Chọn $b_t$ để giảm phương sai; một $b_t$ tùy ý có thể tăng phương sai." chuyển vào ghi chú diễn giả (−13; ý này có ở 4-04 bằng số $\tfrac{147}{64}$).
- **4-06 (48):** T4 + T8 (+≈ 22) bù bằng: bỏ "Câu hỏi:" (−12; câu hỏi (ii) của khối ứng dụng vào ghi chú diễn giả), L6 (−2), rút dòng "Thuật toán 10.6, $c=10$, không giá trị nền: …" thành "Mô phỏng (Phụ lục C), $c=10$, $b=0$: $49/100$ lần chạy kết thúc với $\pi_\theta(1)<0{,}5$." (−3).
- **2-03 (47):** T4 (−1 dòng, −1).
- **7-01 (77/80):** T11 gộp hàng (−≈ 12), thêm $\lVert w_1-u\rVert\le R$ (0, KaTeX).

## 7. Đề xuất sửa ghi chú (bổ sung mục 13 của storyboard)

Không thấy lỗi toán học mới. Các đề xuất của mục 13 storyboard hợp lý. Phụ lục C tái lập được từng chữ số bằng giao thức đã ghi (REINFORCE và phát lại), nên không cần ghi thêm chi tiết cách rút. Một đề xuất nhẹ: §6 đặt $\mathcal F_t$ là một bộ biến, còn Bài 05 dùng cùng kí hiệu cho σ-đại số; một câu "khác σ-đại số $\mathcal F_t$ của Định nghĩa 05.10, nhưng kì vọng có điều kiện dùng như Bổ đề 05.12" sẽ chặn nhầm lẫn khi ghi chú dẫn Bổ đề 05.12 ngay sau.

## 8. Kiểm liên tục (bảng kiểm Outline/Threads/Concept của quill)

- **Thứ tự khái niệm:** mỗi mạch ứng với các mục liên tiếp (§1–§4, §5, §6, §7, §8–§9, §10–§13); trong mạch, thứ tự khối trùng ghi chú (đã đối chiếu từng khối mục 12). Định nghĩa trước khi dùng: đạt, trừ "tác tử", "lịch sử" ở dòng dẫn (L3) và dữ kiện bài toán đề xuất (T8).
- **Mạch truyện:** câu nối trên mặt trang có ở 2-05 → 3-00, 3-11 → 4-01 dòng 1, 5-01 dòng 1, 6-01 dòng 1, 6-06 "Câu hỏi:" → 6-07 "Kết luận:". Ba ví dụ xuyên suốt (bandit, MDP hai bước, hai nhiệm vụ bậc hai) mỗi lần dùng lại trả lời một câu hỏi mới; không ví dụ nào lặp số mà không thêm ý.
- **Thuật ngữ:** "giá trị nền", "gradient log", "lượt", "tổng phần thưởng", "tổng phần thưởng từ bước $t$", "tầm nhìn hữu hạn", "dưới vi phân", "tinh chỉnh", "độ quên" đúng `thuat-ngu.md`; lệch duy nhất "phân lớp" (L15). "Vòng qua dữ liệu" cho epoch (L16).
- **Kí hiệu:** $R$ hai nghĩa (L2); $\mathcal F_t$ khác nghĩa với Bài 05 (L14, mục 7); $\eta_j$/$\eta$, $T$ (số cập nhật/số vòng), $m$ (cỡ mẫu/số lượt) dùng như ghi chú, không xung đột trên cùng trang.
- **Kỹ thuật:** danh sách mục 14 đầy đủ đến Bài 10; trang riêng duy nhất 3-05 đúng chỗ (Bài 09 đã nhường); "Nhắc lại:" một dòng cho "Đổi chỗ đạo hàm và kì vọng" (3-05), "Đảo cận đuôi" (4-07), "Kì vọng có điều kiện theo lịch sử" (4-03) đúng chính sách.
