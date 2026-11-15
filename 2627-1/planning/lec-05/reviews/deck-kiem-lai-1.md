# Kiểm lại sau biên tập — deck Bài 05, lượt 1 (2026-11-15)

Vai: kiểm lại sau biên tập (chỉ đọc). Đầu vào: deck sau sửa `2627-1/lecture-05-ha-gradient-ngau-nhien.html` và `img/lec-05/`; bản đóng băng trong thư mục nháp của điều phối viên (`…/lec-05/master/frozen/`); năm báo cáo `reviews/deck-*.md`; `review-log.md` mục "Năm báo cáo duyệt và quyết định của điều phối viên"; `storyboard.md` mục 17; `materials/lec-05/lecture-note.md`, `exercises.md`. `no-ai-slop` chế độ Detect trên văn bản mới hoặc đã sửa.

**Kết luận: đạt.** 0 chặn bàn giao, 0 nghiêm trọng, 0 trung bình, 12 nhẹ (đề xuất sửa, không chặn bàn giao).

## 1. Cách kiểm

- So từng trang theo `data-slide-id` (script trong thư mục nháp `…/lec-05/recheck/`): 55 trang, cùng ID và thứ tự; 43 trang đổi (mặt trang hoặc ghi chú diễn giả); 4 SVG đổi (`ba-buoc-sgd`, `do-dai-buoc`, `khong-loi`, `phep-chieu`).
- Tính lại mọi con số trên nội dung đã đổi (mục 3).
- `deck_lint.py`: 1 phát hiện, `L05-7-04 | SYLL60 | 68 > 60` (ngoại lệ 11.9 đã chấp nhận).
- `footer_check.py`: 0 trang chạm chân trang hoặc đáy khung.
- `deck_check.py --shots` (26 trang đã đổi; báo cáo cho cả 55 trang): console 0, pageerrors 0, failed 0, `.katex-error` 0; OVERFLOW chỉ trên `path` SVG (đuôi `\sqrt`, báo động giả đã biết) ở 4-06, 4-07, 4-08, 4-09, 4-10, 5-02, 6-02, 6-03, 7-02, 7-03; không trang nào có `docScrollW > 390`. Mật độ: 7-02 75 âm tiết (trần 80 cho bảng tổng kết), 1-03 80 (trần mục tiêu), 1-01 77 (bìa), 1-04 7 dòng (trang Nội dung, không đổi), 7-04 66 (ngoại lệ).
- Đã xem ảnh 1600×900 của 26 trang đổi và ảnh 390×844 `-end` của 18 trang đổi có cuộn (tờ ghép trong `…/lec-05/recheck/sheets/`). Không tràn ngang trang; công thức dài và bảng (4-03, 3-05, 3-08, 6-05, 7-02) cuộn ngang tại chỗ như chế độ đọc màn hẹp quy định.

## 2. Phát hiện được chấp nhận → trạng thái

| Phát hiện | Trang | Trạng thái | Bằng chứng |
|---|---|---|---|
| $\partial F=\{\nabla F\}$ bỏ giả thiết lồi (CG1, SP1, TH1) | 2-03 | đã sửa | "Với $F$ lồi, hữu hạn trên $\mathbb R^p$: $\partial F(w)\ne\varnothing$, và $\partial F(w)=\{\nabla F(w)\}$ khi $F$ khả vi tại $w$." khớp ghi chú dòng 224; không còn mâu thuẫn với hình $(w^2-1)^2$ |
| Luận điểm bìa một câu, có điều kiện | 1-01 | đã sửa | một câu: hàm mục tiêu lồi, oracle không chệch, mô-men bậc hai bị chặn, độ dài bước theo số vòng lặp, điểm lặp trung bình; xem nhẹ #1 về cấu trúc câu |
| Ghi chú 4-01 dùng bước ba $i_3=1$ (TH2) | 4-01 | đã sửa | $\langle g_3,w_3-w^*\rangle\approx0{,}0236<\tfrac\eta2\lVert g_3\rVert^2\approx0{,}0858$; khoảng cách $0{,}0586\to0{,}1112$; bước hai "lại gần" ($1{,}3289>1$). Tính lại: $g_3=(-0{,}5858;0)$, $w_3-w^*=(-0{,}0402;-0{,}0426)$, $w_4=\operatorname{proj}(1;-0{,}7071)=(0{,}8165;-0{,}5774)$ — khớp |
| 7-03 phạm vi $1/\delta'^2$ (TH3) | 7-03 | đã sửa | "cho $\operatorname{opt}_S$ ($W$ bị chặn) với xác suất $\ge1-\delta'$ theo $\xi$: thêm thừa số $1/\delta'^2$" |
| 4-05 $c_t\ge F(w_t)-F(u)$ (CG2, HV8) | 4-05 | đã sửa | "(với SGD: theo kì vọng)"; ghi chú diễn giả nói rõ; xem nhẹ #5 |
| 6-02 bảo đảm cho thuật toán, không chặn $L_D$ (CG4) | 6-02 | đã sửa | "Trực quan. Với $F=L_s$, Hệ quả 05.15 chặn $\operatorname{opt}_s$ của SGD trên $s$ cố định, không chặn $L_D$"; ghi chú diễn giả có "không phải cho lớp (Nhận xét 01.21)" |
| 6-03 "rút có hoàn lại" gán cho (G1) (CG3) | 6-03 | đã sửa | bước 1: "(rút đều) … (G1); … (G2); rút có hoàn lại: các $\xi_t$ độc lập" |
| 5-01 giới hạn mạng nơ-ron (CG5) | 5-01 | đã sửa | "Kết luận: tính lồi cần cho (G1) và bước 5; các cận không chuyển sang mạng nơ-ron khi chưa có lập luận mới." khớp ghi chú dòng 1206 |
| 4-09, 7-03 "theo cận" (CG6) | 4-09, 7-03 | đã sửa | "theo các cận, …"; "theo cận, $10^4$ bước SGD đủ …" |
| Số hiệu ở trang nguồn (MT P2) | 3-05, 3-08, 6-03, 6-05 | đã sửa | "Ví dụ 05.6.", "(Bài tập 05.3(b))", "Ví dụ 05.14.", "Ví dụ 05.15."; kiểm bằng script: mọi "Ví dụ/Bài tập 05.k" trên mặt trang (05.1, 05.3, 05.5, 05.6, 05.9, 05.12–05.15, Bài tập 05.3(b)) đều có trang nguồn mang số |
| Câu nối mạch 3→4 (MT P3, SP11) | 4-00 | đã sửa | dòng dẫn "Phép chiếu, kì vọng theo lịch sử và tính lồi ghép lại cho cận kì vọng tại điểm lặp trung bình." |
| Câu nối vào mạch 6 và liên hệ (O2) (MT P4, SP11) | 6-00, 6-01, 6-03 | đã sửa | 6-00 "Với hàm lỗi lồi và đủ số bước, …"; 6-01 dòng mở; 6-03 "Ý nghĩa: SGD đạt (O2) …"; xem nhẹ #7, #9 |
| Câu nối vào mạch 5 (SP11) | 5-00, 5-01 | sửa một phần, chấp nhận | dòng dẫn 5-00 có sẵn nêu bỏ giả thiết → kết luận sai; câu "bỏ đúng một giả thiết" ở ghi chú diễn giả 5-01; mặt trang 5-01 đủ ý qua dòng "Kết luận:" |
| Tiêu đề trang kỹ thuật (MT P6) | 3-07, 4-05 | đã sửa | "Kì vọng có điều kiện theo lịch sử"; "Tổng triệt tiêu và trung bình các điểm lặp"; 3-06 đổi thành "Tính không chệch có điều kiện" nên không trùng tiêu đề |
| 6-04 "Nhắc lại:" kỹ thuật Bài 04 (HV13, CG13, MT P7) | 6-04 | đã sửa | "Nhắc lại: thêm bớt kì vọng rồi bình phương (Bài 04)"; tên khớp trang "Kỹ thuật." của deck 04 (`lecture-04-*.html` dòng 281); 3-07 nhắc "lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện (Bài 04)", khớp deck 04 dòng 650; xem nhẹ #10 |
| 3-04 nhãn ngoài danh sách (SP9) | 3-04 | đã sửa | một câu "Cả hai dùng …, trả về điểm lặp trung bình …" |
| 3-06 bảy dòng (HV14), 7-02 81 âm tiết | 3-06, 7-02 | đã sửa | 3-06: 6 dòng; 7-02: 75 âm tiết (deck_check), dưới trần 80 |
| F4 trục, F2 nhãn (TH11, TH12) | `do-dai-buoc.svg`, `phep-chieu.svg` | đã sửa | trục dọc tới $1$ (vạch $0{,}2$…$1$), chứa $0{,}8031$; nhãn "π" |

**Hai mục "không sửa" (storyboard §17):**
- MT P8 (thứ tự khối 2-04/2-05, 3-03/3-04): chấp nhận. Thứ tự mục của ghi chú giữ đúng; Ví dụ 05.2 trên deck dùng Mệnh đề 05.3(a), (c) nên đứng sau mệnh đề; Thuật toán 05.11 cần Định nghĩa 05.10.
- 3-01 dòng Định nghĩa 05.7 dài 27 âm tiết: chấp nhận như ngoại lệ (tách dòng làm trang chạm chân trang; câu giữ đủ "tồn tại vì $W$ đóng, duy nhất vì $W$ lồi"). Đề nghị điều phối viên ghi ngoại lệ này cạnh ngoại lệ 7-04 trong `review-log.md`.

**Các mục "sửa một phần":**
- HV12 (hai nghĩa của $G$): chấp nhận. 2-06 "Ý nghĩa: $G$ chặn mọi dưới gradient; đó là hằng số $G$ của các cận sau" và 4-09 dòng đầu nối hai nghĩa; xem nhẹ #6.
- CG8 (phụ thuộc $p$, $m$): chấp nhận. 4-07 "Ý nghĩa: cận phụ thuộc chiều $p$, cỡ mẫu $m$ chỉ qua $G$ và $R$"; 4-03 có ý này ở ghi chú diễn giả.
- HV25 (trang 55–60 âm tiết): chấp nhận. Không trang nội dung nào vượt 60 trừ ngoại lệ 7-04.
- SP11 phần mạch 5: xem bảng trên.

Các phát hiện còn lại trong bảng §17 (HV1–HV25, TH1–TH12, CG1–CG15, SP1–SP28 cùng hai mục SP không đánh số, MT P1–P15) đều có trên deck như mô tả; đã đối chiếu từng trang đổi.

## 3. Toán trên nội dung đã đổi

Tính lại, khớp: 1-06 thứ tự $0{,}0710;0{,}1021;0{,}0694$ theo $i_3=1,2,3$; 3-05 $\mathbb EL_S(w_4)=0{,}2425/3\approx0{,}0808$; 2-05 $\ell(u)=0{,}5$, $\langle v,u-w_0\rangle=0{,}12+0{,}48=0{,}6$; 4-02 $\lVert(1,-1)-w^*\rVert^2\approx0{,}1764$, $\lVert w_3-w^*\rVert^2\approx0{,}0034$, $0{,}5053-0{,}1764+1\approx1{,}3289$, $0{,}5053-0{,}0034+1\approx1{,}5019$; 4-04 bước 4 $\sum_t\mathbb E[F(w_t)-F(u)]\le\Delta_1/(2\eta)+\eta TG^2/2$; 4-06 $\eta^*=0{,}00625$, $0{,}1$, $0{,}125$, $0{,}505$; 4-09 $\lVert\nabla_w\ell\rVert=\lVert x\rVert/(1+e^{\tilde y\langle w,x\rangle})\le1$, $T=25/0{,}0025=10^4$, $\eta=5/100=0{,}05$; 5-01 $RG/\sqrt T=2{,}5\cdot2{,}25/40=0{,}140625$, $\eta\approx0{,}02778$, ngưỡng $w>-1{,}1213$ đạt từ $t=26$ ($0{,}5\cdot0{,}9444^{k}<0{,}1213\iff k\ge25$); 5-03 $0{,}01/(0{,}4T)=0{,}025/T$, $\eta G^2/2=0{,}1$, $\tilde F=(w-0{,}1)^2+0{,}09$, $0{,}16$; 6-03 $16/(0{,}0025\cdot0{,}01)=640\,000=400\cdot1600$; ghi chú $10^4/0{,}0025=4\cdot10^6$; 6-05 $T(b)=1600,475,194,124,106$, số quan sát $1600,1900,3104,7936,27\,136$; 6-06 $b=30$, $3300$; $b=150$, $16\,500$; 7-01 $L_D=w^2+1$, $0{,}9875^{t-1}$, $\bar w\approx0{,}95$, $0{,}0025$, $1{,}9025$, $0{,}9025$; 7-05 $6400$, $32\,000$, $(640\,000-32\,000)/5=121\,600$, ghi chú $5\cdot4=20$. Phát biểu Hệ quả 05.19 trên 6-02 khớp ghi chú dòng 1059–1077 (đủ $w_1\in W$, $G>0$, $\varphi(w,i)=v(w,z_i)$, Thuật toán 05.11). Hệ quả 05.16 trên 4-09 đủ $R>0$, $u\in W$.

## 4. Mạch truyện (trang đổi ±2, ranh giới mạch)

- 1-02 → 1-06: bỏ "sai số ước lượng" khỏi 1-02, nhắc lại ở 7-01 nơi dùng (P11) — đúng quy tắc nhắc lại gần nơi dùng.
- 2-07 → 3-00 → 3-01: dòng dẫn 3-00 nêu phép chiếu và oracle; 3-01 mở bằng lý do cần tập bị chặn. Liền mạch.
- 3-05 → 3-06 → 3-07 → 3-08: tiêu đề mới tách "tính không chệch có điều kiện" (bổ đề) và "kì vọng có điều kiện theo lịch sử" (kỹ thuật); không trùng.
- 3-08 → 4-00 → 4-01: dòng dẫn 4-00 nối ba công cụ của mạch 3 với cận kì vọng.
- 4-09 → 4-10 → 5-00 → 5-01: liền mạch.
- 5-04 → 6-00 → 6-01 → 6-02: liền mạch; câu mở 6-01 và "Trực quan." 6-02 gần trùng ý (nhẹ #7).
- 6-06 → 7-00 → 7-01 → 7-03: 7-01 bỏ "Kết luận:", 7-03 dòng cuối mang số $0{,}0025$, $0{,}9025$ của 7-01; không còn trùng kết luận (P10).

## 5. Phát hiện mới

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | 1-01 | Chủ ngữ dài đẩy xa động từ (author's voice: "a subject pushed far from its verb") | "cận của độ chênh tối ưu kì vọng tại điểm lặp trung bình của hạ gradient ngẫu nhiên có chiếu tỉ lệ nghịch với căn bậc hai của số vòng lặp" | Đưa thuật toán lên làm chủ ngữ: "…, hạ gradient ngẫu nhiên có chiếu có cận của độ chênh tối ưu kì vọng tại điểm lặp trung bình tỉ lệ nghịch với căn bậc hai của số vòng lặp." |
| nhẹ | 1-06 | "mọi bước SGD" đọc theo nghĩa đen là sai: hai bước đầu làm $L_S$ giảm ($\tfrac23\to0{,}4533\to0{,}0639$); ý đúng là ba lựa chọn của bước tiếp theo | "Ba quan sát, từ $L_S=0{,}0639$: mọi bước SGD làm $L_S$ tăng ($0{,}0710$; $0{,}1021$; $0{,}0694$)" | "… cả ba lựa chọn của bước SGD tiếp theo làm $L_S$ tăng (…)" |
| nhẹ | 4-03 | "Trực quan." dùng "tiến về phía $u$" mà không nêu đơn vị; phần tiến thật là $(\lVert w_t-u\rVert^2-\lVert w_{t+1}-u\rVert^2)/(2\eta)$ | "mỗi bước tiến về phía $u$ ít nhất $F(w_t)-F(u)$ và trả thêm $\eta G^2/2$" | Thêm một lần định nghĩa phần tiến, ví dụ "phần tiến $(\Delta_t-\Delta_{t+1})/(2\eta)$, $\Delta_t=\lVert w_t-u\rVert^2$, theo kì vọng ít nhất $F(w_t)-F(u)-\eta G^2/2$"; hoặc giữ chữ và thêm dòng này vào ghi chú diễn giả |
| nhẹ | 4-03 (mặt trang và ghi chú), 4-03/7-00/7-03 ghi chú | Thiếu giới từ "cho" (điều phối viên đã ghi lỗi này của ghi chú cho tác giả; deck không bắt buộc chép lỗi câu chữ) | "với $F$ là hàm mà oracle không chệch:" | "với $F$ là hàm mà oracle không chệch cho" |
| nhẹ | 4-05 | Dòng kết luận viết như bất đẳng thức tất định; với SGD vế trái phải là $\mathbb EF(\bar w_T)-F(u)$ | "$F$ lồi và $c_t\ge F(w_t)-F(u)$ (với SGD: theo kì vọng): chia cho $T$ được $F(\bar w_T)-F(u)\le\frac1T\sum_tc_t$" | "(với SGD: lấy kì vọng hai vế)" hoặc ghi "$\mathbb E$" trong ngoặc ở vế kết luận |
| nhẹ | 4-09 | Trích dẫn đặt sai chỗ: (G2) thành $\lVert v(w)\rVert\le G$ là do oracle tất định; Mệnh đề 05.5 chỉ cho cận đó khi $F$ là $G$-Lipschitz | "(G2) thành $\lVert v(w)\rVert\le G$ (Mệnh đề 05.5)" | "(G2) thành $\lVert v(w)\rVert\le G$, đúng khi $F$ là $G$-Lipschitz (Mệnh đề 05.5)" hoặc bỏ trích dẫn trên mặt trang (ghi chú diễn giả đã nói) |
| nhẹ | 6-01/6-02 | Hai trang liền nhau lặp cùng ý "Với $F=L_S$, Hệ quả 05.15 chặn sai số tối ưu thực nghiệm"; đồng thời 6-01 viết $S$ cố định, 6-02 viết $s$ cố định | 6-01: "Với $F=L_S$, Hệ quả 05.15 chặn sai số tối ưu thực nghiệm; …"; 6-02: "Với $F=L_s$, Hệ quả 05.15 chặn $\operatorname{opt}_s$ của SGD trên $s$ cố định, không chặn $L_D$." | 6-02 "Trực quan." chỉ giữ phần mới (bảo đảm cho một thuật toán, không chặn $L_D$) hoặc cơ chế Markov ngắn; 6-01 dùng "$s$ cố định" như ghi chú |
| nhẹ | 6-02 | "theo $\xi$" gắn sau $\delta'$ thành cụm vô nghĩa ($\delta'$ là một số); bản đóng băng có "(xác suất thất bại theo $\xi$, khác $\delta$ theo $S$)" như ghi chú | "(b) với xác suất cao: $\epsilon_{\mathrm{opt}}&gt;0$, $\delta'\in(0,1)$ theo $\xi$, $T\ge\ldots$" | "$\delta'\in(0,1)$ (xác suất thất bại theo $\xi$)" hoặc bỏ "theo $\xi$" vì $\Pr_\xi$ đã nêu |
| nhẹ | 6-03 | (O2) theo định nghĩa là tất định; "SGD đạt (O2) … với xác suất" tự mâu thuẫn về chữ. Ý nghĩa thao tác bị rút gọn, mất "độc lập trên cùng $s$" và điều xảy ra trong 95 lần (author's voice: nghĩa thao tác dương) | "SGD đạt (O2), $\operatorname{opt}_s\le\epsilon_{\mathrm{opt}}$, với xác suất $\ge1-\delta'$, không tất định; $\delta'=0{,}05$: khoảng 95/100 lần chạy." | "SGD đạt mức của (O2), $\operatorname{opt}_s&lt;\epsilon_{\mathrm{opt}}$, với xác suất $\ge1-\delta'$: với $\delta'=0{,}05$, khoảng 95 trong 100 lần chạy độc lập trên cùng $s$." |
| nhẹ | 6-04 | "Nhắc lại:" đứng sau phát biểu dùng nó (bài học chung: "Nhắc lại:" đứng trước công thức dùng nó) | dòng "Nhắc lại: thêm bớt kì vọng rồi bình phương (Bài 04) …" là dòng cuối, sau "Bảo đảm:" | Chấp nhận được vì kỹ thuật thuộc chứng minh không trình bày trên trang; nếu đủ chỗ, chuyển lên trước "Mệnh đề 05.20." |
| nhẹ | 7-03 | Đối lập nhị phân "X, không phải Y" (no-ai-slop: binary contrast; author's voice: nói dạng dương) | "Đại lượng được chặn là $\operatorname{opt}_S$, không phải sai số ước lượng ($0{,}0025$ so với $0{,}9025$)." | "Cận chặn $\operatorname{opt}_S\approx0{,}0025$; sai số ước lượng vẫn $\approx0{,}9025$." |
| nhẹ | 4-02, 4-09, 7-01 (390 px) | Dấu câu sau công thức inline rơi xuống đầu dòng riêng | ảnh `narrow-025-L05-4-02-end.png` (dấu "." sau $1{,}5019$), `narrow-032-L05-4-09-end.png` ("," trước $\eta=0{,}05$), `narrow-047-L05-7-01-end.png` ("." sau $\min_WL_D=1$) | Đưa dấu câu vào trong biểu thức KaTeX hoặc bỏ dấu chấm cuối dòng liệt kê |

Văn phong (Detect) trên các câu mới khác: không thấy "ta thấy", "rõ ràng", "chúng ta", "minh họa", "giả định", "Đáp án", "Trang này"; nhãn chỉ trong danh sách hợp lệ; không câu rào đón về chính văn bản. Ghi chú diễn giả mới không có ID trang, mã storyboard hay câu quy trình.

## 6. Đề xuất sửa ghi chú

Không có đề xuất mới.
