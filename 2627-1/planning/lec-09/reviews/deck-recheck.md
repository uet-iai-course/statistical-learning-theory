# Kiểm lại sau biên tập — deck Bài 09 (toán học và mạch truyện)

Vai: kiểm lại, chỉ đọc (`general-purpose`, `opus`, effort `high` theo lệnh gọi của điều phối viên). Ngày: 2026-11-16.

Bản trước: bản đóng băng trong thư mục nháp của điều phối viên (`master/frozen/`). Bản sau: `2627-1/lecture-09-hoc-chuoi-mo-hinh-sinh.html` (55 trang). Diff tự lập theo từng trang, cả mặt trang và ghi chú diễn giả, có ánh xạ 7-04→7-05, 7-05→7-06, 7-06→7-07 và 7-03→7-03 + 7-04 (mới); 2-06 bị bỏ. Đối chiếu: `materials/lec-09/lecture-note.md`, `exercises.md`, năm báo cáo `reviews/deck-*.md`, `review-log.md` § Bộ trang chiếu, `storyboard.md` §17. `no-ai-slop` chế độ Detect cho văn bản mới hoặc đã sửa.

## 1. Kiểm bằng máy và trình duyệt

| Kiểm | Kết quả |
|---|---|
| `deck_lint.py` | 0 phát hiện, 55 trang |
| `footer_check.py` (1600×900) | 0 trang chạm chân trang |
| `deck_check.py --shots` | console 0, pageerrors 0, failed 0, `.katex-error` 0 |
| OVERFLOW (1-02, 3-06, 3-07, 6-08, 7-02, 7-04) | đo lại từng phần tử: chỉ có `.katex-mathml` ẩn và đuôi SVG của `\sqrt` (báo động giả đã biết) |
| Liên kết "Nội dung" (1-04) | `#/2`…`#/7` mở đúng 2-00…7-00 (mạch 2 ở `h=1`, …, mạch 7 ở `h=6`) |
| Bàn phím | ↓, →, Space đi đúng thứ tự 1-01→1-02→1-03→2-00→2-01→2-02; Esc mở chế độ tổng quan |
| Ảnh | đã xem 1600×900 và 390×844 (kể cả `-end`) của 38 trang đã đổi: 1-02, 1-03, 1-06, 2-01…2-05, 3-01, 3-03, 3-04, 3-06…3-09, 4-02, 4-05, 4-07, 4-08, 5-01, 5-02, 5-04…5-06, 6-00…6-05, 6-07, 6-08, 7-00…7-05 |

Mật độ (đếm của `deck_check.py`): không trang nội dung nào vượt 60; 7-01 là 72/80 (bảng tổng kết); 7-02 là 60.

## 2. Phát hiện nghiêm trọng và trung bình của năm báo cáo

| Báo cáo | Trang | Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|---|---|
| chuyên gia (nghiêm trọng) | 2-03 | cận cho hàm lỗi bị chặn áp dụng quá rộng | đã sửa | "Với độ dài $n$ cố định, mọi xác suất có điều kiện $\ge c>0$ ($c$ chung cho lớp): $\ell\le n\ln(1/c)$. Khi đó cận Bài 02, 04, 07 …"; Bài 03 bỏ; ghi chú diễn giả nêu Định lý 03.15 chỉ cho hàm lỗi 0–1 |
| chuyên gia (nghiêm trọng) | 6-08 | tiêu đề, $\theta$ cố định, độ chênh tối ưu, $-\operatorname{ELBO}$ không lồi | đã sửa | tiêu đề "Bài tập: SGD cho một mục tiêu lồi"; "$\theta$ cố định, một quan sát $x=2$"; "độ chênh tối ưu, không phải $L_D$"; "Theo $(\theta,\phi)$, $-\operatorname{ELBO}$ nói chung không lồi" |
| toán học (nghiêm trọng) | 4-03 ghi chú | "chỗ duy nhất … $\infty-\infty$" | đã sửa | Bước 2 dùng $\mathrm H<\infty$ để cộng theo số hạng; vế sau của (b) suy từ (a); bỏ giả thiết thì $L_D=+\infty=\mathrm H(p_D)$ — khớp chứng minh Mệnh đề 09.8 |
| học viên | 3-08 | rò rỉ không đọc được tại chỗ | đã sửa | "Hàm dự đoán ghi nhớ tra $u_{j+1}$: đích $x_j$ ở cuối ngữ cảnh"; "$\approx0{,}8\cdot0+0{,}2\cdot1<\operatorname{Var}(x_j)=1$" |
| học viên | 3-09 | hai điểm cực tiểu không có lý do | đã sửa | hai rủi ro, hai cực tiểu, trọng số $\tfrac14$, $\tfrac1{20}$ trên mặt trang; khớp Ví dụ 09.6, Bước 1–3 |
| học viên | 4-07 | $\ln4$, $1{,}0889$ không giải thích | đã sửa, sinh lỗi mới | công thức chuyển xuống ghi chú diễn giả, nhưng dữ liệu xích Markov rơi khỏi mặt trang (R2) |
| học viên | 6-08 | (C), (G1) chỉ có tên | đã sửa | "Nhắc lại: … (C) $F$ lồi, $W$ đóng, lồi; (G1) $\mathbb E\varphi\in\partial F$; (G2) …" |
| học viên | toàn deck | mật độ | sửa một phần, điều phối viên chấp nhận | mọi trang ≤ 60 |
| toán học | 7-05 (cũ 7-04) câu 4 | thiếu Bước 3 | đã sửa | ghi chú diễn giả: "và vế sau của (b) ở Bước 3" |
| toán học | 6-04 | điều kiện như thể đủ | đã sửa | "Với $\zeta$ có phân bố không phụ thuộc $\phi$: … khi: (i) … (ii) … (iii)" |
| toán học | 6-04 ghi chú | khái quát về hàm nhảy | đã sửa | chỉ nói về hàm chỉ báo và biến Bernoulli của Ví dụ 09.12 ($0{,}3521$ và $1$) |
| toán học | 6-03 ghi chú | thiếu điều kiện cho mỗi $\kappa_i$ | đã sửa | "nếu mỗi $\kappa_i$ thỏa (i)–(iii) theo $(\theta,\phi)$" |
| chuyên gia | 7-02 | dòng Hoeffding | đã sửa | "$\lvert L_V(\theta)-L_D(\theta)\rvert\le n\ln(1/c)\sqrt{\ln(2/\delta)/(2m_v)}$, $\theta$ cố định, $n$ cố định, mọi xác suất $\ge c>0$" |
| chuyên gia | 6-08 | (C) cho thác triển | đã sửa | "(C) cho thác triển lồi của $F$"; ghi chú nêu $\tilde F$ trên $\mathbb R\times[\tfrac14,\infty)$ — khớp Bài tập 09.7(a) |
| chuyên gia | 2-01 | cố định và ngẫu nhiên | đã sửa (ghi chú diễn giả) | ba nhóm theo bảng §1 của ghi chú |
| chuyên gia | 3-01, 3-03 | đồng nhất thức và giả thiết mô hình | đã sửa | 3-03 "Ngữ cảnh bậc $k$ (giả thiết mô hình)"; ghi chú 3-01 |
| chuyên gia | 3-08 | chia theo thời gian | đã sửa | "Chia theo thời gian: $0{,}994$; cửa sổ kiểm tra vẫn phụ thuộc nhau" |
| chuyên gia | 3-09 | cực tiểu của $\ell_{\mathrm{len}}$ | đã sửa (ghi chú diễn giả; điều phối viên chấp nhận) | khớp ghi chú dòng 340 |
| chuyên gia | 4-07 | $1{,}088<1{,}0904$ | đã sửa | "$m=500$: mô hình thật cũng $1{,}088$: dao động của tập kiểm tra" — khớp Ví dụ 09.8, Bước 4 |
| chuyên gia | 6-00 | dòng dẫn "khả vi, khả tích" | đã sửa | "khả vi liên tục trên từng đường nhiễu, có hàm trội và khả tích" (xem N5) |
| chuyên gia | 5-03 ghi chú | khối lượng điểm | đã sửa | "Khi mô hình liên hợp không có mật độ …" |
| sư phạm | 4-08, 7-03 | đề rút thành mảnh câu | đã sửa | 4-08 trùng câu chữ (c) của `exercises.md`; 7-03 có (i), (ii) dạng câu đủ (xem R1) |
| sư phạm | 7-05 ghi chú (cũ 7-04/7-05) | câu quy trình, nguồn gốc | đã sửa | ghi chú 7-06 không còn "Mỗi bài xếp vào mạch …", "Bảy bài đầu là bài gốc …" |
| sư phạm | 1-02, 2-01, 2-04, 4-05, 6-08, 7-03 | tên tiếng Anh, tên đầy đủ | đã sửa | ERM (1-02), log loss (2-01), generalization gap (4-05), SGD (6-01), random seed (7-03) |
| sư phạm | 3-08 | "Tra" không chủ thể | đã sửa | — |
| sư phạm | 6-01 | hai dấu hai chấm | đã sửa | hai dòng tách |
| sư phạm | 6-08 | (C), (G1) | đã sửa | — |
| mạch truyện M1 | 5-01 | câu nối 4→5 | đã sửa | "Độ hợp lý của mô hình có biến không quan sát được là một tích phân, nói chung không tính được." |
| mạch truyện M2 | 6-01 | câu nối 5→6 | đã sửa | "Cực đại hóa ELBO bằng hạ gradient ngẫu nhiên (…, SGD) cần $\nabla F$" — khớp ghi chú dòng 695–699 |
| mạch truyện M3 | 6-07 | câu nối, $50$ chuỗi | đã sửa | "Tiêu chí thứ hai: …"; "trên $50$ chuỗi của Ví dụ 09.8" |
| mạch truyện M4 | 4-07 | câu hỏi thực hành | sửa một phần, điều phối viên chấp nhận | (i) trên mặt trang; (iii) ở ghi chú diễn giả |
| mạch truyện M5 | 7-02 | cách học mô hình biến ẩn | đã sửa | "Biến ẩn: cực đại hóa ELBO, khe $=\mathrm{KL}$ tới hậu nghiệm" |

Hai giả thiết điều phối viên yêu cầu khôi phục: 7-01 "$\mathcal X$ đếm được; $p_\theta$ tổng $1$; $\mathrm H(p_D)<\infty$" và 1-02 "(T2) $\ell\ge0$, đo được" — có. Ô Định lý 09.12 "$p_\theta(x,v)>0$ trên giá $q$" tương đương "$q$-hầu hết $v$" của ghi chú (dòng 594).

## 3. Toán trên các trang đã đổi (tính lại)

Khớp ghi chú và `exercises.md`: 3-08 ($5000-10=4990$, $20\%$ là $998$); 3-09 ($-\ln\theta-5\ln(1-\theta)$ cực tiểu $\tfrac16$; $-\tfrac12\ln\theta-\tfrac12\ln(1-\theta)$ cực tiểu $\tfrac12$; trọng số $\tfrac12\cdot\tfrac12$, $\tfrac12\cdot\tfrac1{10}$); 4-05 ($0{,}6956-0{,}6109=0{,}0847$); 4-08 ($\mathrm{KL}(p_\theta\Vert p_D)=\tfrac12\ln2\approx0{,}3466$, chiều thuận $+\infty$); 5-04 (KL tới tiên nghiệm $0$; $0{,}5$; $0{,}4166$; $0{,}5966$); 6-05 (một lần rút $(1{,}5;0{,}75)$, $(3;-3)$; $\operatorname{Var}(2\zeta-\zeta^2)=4+2-0=6$ vì $\operatorname{Cov}(\zeta,\zeta^2)=\mathbb E\zeta^3=0$); 6-08 ($\max_W\mathbb E\lVert\varphi\rVert^2=8+4=12$, $G=2\sqrt3$, $R=\sqrt{4{,}25}\approx2{,}0616$, $\eta=R/(100G)\approx0{,}005951$, $RG/100=\sqrt{51}/100\approx0{,}07141\le0{,}0715$); 7-04 ($\ln(1/0{,}087)\approx2{,}4418$, $\sqrt{\ln40/400}\approx0{,}09603$, tích $0{,}23449\le0{,}2345$; $0{,}2345/0{,}0041\approx57$); 7-02 (bán kính theo chuỗi $n\ln(1/c)\sqrt{\cdot}$ = cách của Ví dụ 09.4). Phát biểu 4-02(c), 6-02, 6-04, 7-01 khớp Mệnh đề 09.8, 09.15, Định lý 09.12 (cắt mật độ không làm rơi điều kiện; 6-04 (ii) bỏ "trên lân cận $U$", nhưng hàm trội toàn cục là điều kiện mạnh hơn nên phát biểu vẫn đúng).

## 4. Mạch truyện sau khi bỏ 2-06 và tách 7-03/7-04

- 2-05 → 3-00: mạch 2 kết ở Ví dụ 09.2 với $m_1=0$, $\ell(\hat\theta,1)=+\infty$; dòng dẫn 3-00 nối được. Nội dung 2-06 ở ghi chú diễn giả 2-05 (khớp Bài tập 09.8(c)). Không trang nào trên mặt trang còn dẫn tới 2-06; 09.8 vẫn ở hàng mạch 2 của 7-06.
- 7-02 → 7-03 → 7-04 → 7-05: đề và lời giải tách đúng; tiêu đề 7-04 thêm ", lời giải" như tiền lệ 3-05.
- 1-02 bỏ dòng Nhận xét 02.11 khỏi mặt trang: Định lý 02.7 xuất hiện lần đầu trên mặt trang ở 3-06 kèm nội dung ("cần số hạng độc lập, bị chặn"), nên vẫn hiểu được tại chỗ.
- Số hiệu dẫn trên mặt trang (Ví dụ 09.4 ở 3-07, Ví dụ 09.8 ở 6-07, Mệnh đề 09.8(c), Hệ quả 05.15, Định lý 09.12(a), (c)) đều có trang chứa số hiệu ấy đứng trước.
- 7-06 (`Mục | Bài tập`) khớp `exercises.md` (09.1–09.10, mỗi bài một lần).

## 5. Phát hiện mới

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 7-03 (R1) | Đề bài tập tổng hợp mất dữ liệu cần để giải khi cắt: mặt trang không còn "$200$ chuỗi kiểm tra", độ dài $n=200$ hay "thí nghiệm của Ví dụ 09.8"; câu (i) hỏi "Cỡ mẫu trong cận là bao nhiêu?" và lời giải 7-04 dùng "$m_v=200$ chuỗi, không phải $40\,000$ kí tự". Bản đóng băng có "$200$ chuỗi kiểm tra". Câu (i) cũng bỏ "dùng cách của Ví dụ 09.4" của đề. | 7-03: "Bài tập 09.6. Làm trơn, $m=50$: mọi xác suất $\ge0{,}087$; độ lệch chuẩn qua hạt giống ngẫu nhiên (random seed) $0{,}0041$."; `exercises.md` dòng 562: "Thí nghiệm của Ví dụ 09.8 (… $n=200$, $200$ chuỗi kiểm tra độc lập, mười hạt giống …)", (b)(i) "dùng cách của Ví dụ 09.4" | Mở dòng đầu bằng "Thí nghiệm của Ví dụ 09.8 ($n=200$, $200$ chuỗi kiểm tra), làm trơn, $m=50$: …" và giữ "dùng cách của Ví dụ 09.4" trong (i); trang đang ở $59$ âm tiết, nên điều phối viên quyết cách cắt bù (ví dụ chuyển "So bán kính với độ lệch chuẩn." thành vế ngắn, hoặc chấp nhận vượt nhẹ có ghi lý do ở storyboard) |
| trung bình | 4-07 (R2) | Dữ liệu của Ví dụ 09.8 không đủ trên mặt trang: "giữ nguyên kí tự với xác suất $0{,}6$" không xác định ba xác suất còn lại ($0{,}2$; $0{,}1$; $0{,}1$), mà giá trị tốt nhất $1{,}0904$ phụ thuộc chúng; "$10$ lần chạy" (bảng là trung bình) cũng chỉ còn ở ghi chú diễn giả. Hai người duyệt (học viên, sư phạm) đề xuất giữ dãy này trên mặt trang. | 4-07: "Xích Markov (Markov chain), kí tự đầu đều, giữ nguyên kí tự với xác suất $0{,}6$; $n=200$; $200$ chuỗi kiểm tra."; ghi chú dòng 500: entropy hàng $-(0{,}6\ln0{,}6+0{,}2\ln0{,}2+2\cdot0{,}1\ln0{,}1)$ | "…, mỗi hàng: giữ nguyên $0{,}6$, ba kí tự kia $0{,}2$; $0{,}1$; $0{,}1$; …" (sư phạm đề xuất); cắt bù trong cột phải (ví dụ "dao động của tập kiểm tra" → "dao động kiểm tra") hoặc điều phối viên quyết |
| trung bình | 2-02 ghi chú diễn giả (R3) | Câu chuyển từ mặt trang xuống ghi chú bị đặt sai chỗ và nói ngược ghi chú: "Khi đó (T1) không áp dụng" đứng ngay sau câu về Thiết lập A, nên đọc thành (T1) không áp dụng cho $m$ chuỗi độc lập. | "… Như vậy $m$ chuỗi là $m$ quan sát độc lập, không phải $3m$. Khi đó (T1) không áp dụng. Phản ví dụ là các cửa sổ chồng lấn …" | Bỏ câu đó; viết câu cuối "… hai cửa sổ liền nhau chung $k-1$ giá trị, nên (T1) không áp dụng cho các cửa sổ." |
| nhẹ | 6-01 | Định nghĩa 09.14 rút còn "phân bố cố định", bỏ "không phụ thuộc $\phi$" — đúng ý then chốt mà 6-04 và ghi chú nêu. | 6-01: "Nhiễu phụ (auxiliary noise) $\zeta$: phân bố cố định"; ghi chú dòng 704: "có phân bố cố định, không phụ thuộc $\phi$" | "phân bố không phụ thuộc $\phi$" |
| nhẹ | 6-01 | "Trực quan." mơ hồ sau khi cắt: "hàm" không rõ là hàm nào (Detect: cấu trúc khó theo). | "$\phi$ chỉ nằm trong hàm." (bản trước: "chỉ còn trong hàm dưới kì vọng") | "$\phi$ chỉ nằm trong $f(g_\phi(\zeta))$." |
| nhẹ | 6-08 | Lời giải trên mặt trang không nêu kết quả của câu (c) được hỏi ($\max_W\mathbb E\lVert\varphi\rVert^2=12$), chỉ có $G=2\sqrt3$. | "(c) Tính $\max_W\mathbb E\lVert\varphi(w,\zeta)\rVert^2$, $G$." / "Lời giải: $G=2\sqrt3$, …" | "Lời giải: $\max_W=12$ tại $(0,1)$, $G=2\sqrt3$, …" nếu còn chỗ |
| nhẹ | 6-00 | Dòng dẫn mạch dùng "đường nhiễu", "hàm trội" trước khi mạch định nghĩa (quy định: dòng dẫn dùng khái niệm đã có). Đổi lấy độ đúng theo phát hiện của chuyên gia; ghi để điều phối viên cân nhắc. | "Tái tham số hóa cho gradient không chệch khi hàm khả vi liên tục trên từng đường nhiễu, có hàm trội và khả tích." | giữ, hoặc "… khi đạo hàm được đưa vào trong kì vọng một cách hợp lệ" và để (i)–(iii) cho 6-02 |
| nhẹ | 1-02, 6-08 (390 px) | Mảnh mồ côi: dấu "." đứng một dòng sau công thức $L_S$ (1-02) và sau $RG/\sqrt T$ (6-08); dòng mở bằng "," trước $\varphi$ (6-08). | ảnh `narrow-001-L09-1-02`, `narrow-046-L09-6-08` | bọc công thức cuối câu cùng dấu chấm trong `white-space:nowrap` |
| nhẹ | 4-05 ghi chú diễn giả | Detect: "nó" không rõ tiền ngữ, "thắng … mà thua" là lời nói. | "nên nó thắng phân bố thật trên chính tập huấn luyện mà thua trên phân bố thật" | "nên ước lượng này có rủi ro thực nghiệm nhỏ hơn của phân bố thật nhưng rủi ro kì vọng lớn hơn" |
| nhẹ | storyboard §3 | Bảng mạch chưa theo deck sau sửa: hàng mạch 2 còn "Bài tập 09.8(c)" ở cột chức năng; cột `strand-lead` của mạch 6 và 7 còn câu cũ ("Viết lần rút thành hàm …", "Học một phân bố là …"). | `storyboard.md` dòng 64, 68, 69; deck 6-00, 7-00 | cập nhật ba ô |

Không phát hiện mới mức chặn bàn giao hoặc nghiêm trọng.

## 6. Kết luận

**Đạt khi sửa.** Mọi phát hiện nghiêm trọng (3) và trung bình của năm báo cáo đã sửa đúng quyết định hoặc được điều phối viên chấp nhận sửa một phần. Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 3 trung bình (R1 7-03 thiếu dữ liệu đề, R2 4-07 thiếu dữ liệu ví dụ, R3 2-02 ghi chú diễn giả đặt sai câu về (T1)), 7 nhẹ. Sau khi sửa R1–R3: kiểm lại 2-02, 4-07, 7-03 ±2, `footer_check.py` và ảnh 390 px của hai trang mặt.

## Lượt 2 (2026-11-16)

Phạm vi: các trang người sửa đổi sau lượt 1 (`storyboard.md` §17, đoạn "Sửa sau kiểm lại") — 1-02, 2-02 (ghi chú diễn giả), 4-05 (ghi chú diễn giả), 4-07, 6-00, 6-01, 6-08, 7-03 — và các trang ±2, ranh giới mạch 5→6 (5-06, 6-00, 6-01) và 6→7 (6-08, 7-00, 7-01).

**Kiểm máy.** `deck_lint.py`: 1 phát hiện, chỉ 7-03 (`SYLL60`, $74>60$; ngoại lệ bài tập tổng hợp đã được điều phối viên ghi). `footer_check.py`: 0 trang. `deck_check.py --shots` trên 21 trang: console 0, pageerrors 0, failed 0, `.katex-error` 0; OVERFLOW ở 1-02, 6-08, 7-02, 7-04 là MathML ẩn và đuôi `\sqrt` như lượt 1. Đã xem ảnh 1600×900 và 390×844 (kể cả `-end`) của tám trang: không chạm chân trang, không mảnh mồ côi còn lại ở 1-02, 6-01, 6-08.

**Xử lý phát hiện lượt 1.**

| Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|
| R1 7-03 thiếu dữ liệu đề | đã sửa (ngoại lệ mật độ) | "Ví dụ 09.8: $n=200$, $200$ chuỗi kiểm tra. Mô hình làm trơn học với $m=50$: mọi xác suất $\ge0{,}087$; độ lệch chuẩn qua mười hạt giống $0{,}0041$." và (i) "… theo cách của Ví dụ 09.4. Cỡ mẫu trong cận là bao nhiêu? So bán kính với độ lệch chuẩn." Khớp `exercises.md` dòng 562, 575, 586–587 (câu chữ rút gọn, không mất dữ kiện, câu hỏi hay điều kiện nào); lời giải 7-04 không đổi, số đúng |
| R2 4-07 thiếu dữ liệu ví dụ | đã sửa, sinh lỗi mới (R4) | "giữ nguyên kí tự với xác suất $0{,}6$, ba kí tự còn lại $0{,}2$; $0{,}1$; $0{,}1$; … trung bình $10$ lần chạy" — khớp ghi chú dòng 500; entropy hàng $1{,}0889$, $(\ln4+199\cdot1{,}0889)/200\approx1{,}0904$ |
| R3 2-02 ghi chú diễn giả | đã sửa | "… hai cửa sổ liền nhau chung $k-1$ giá trị, nên (T1) không áp dụng cho các cửa sổ." |
| nhẹ 6-01 | đã sửa | "phân bố không phụ thuộc $\phi$"; "$\phi$ chỉ nằm trong $f(g_\phi(\zeta))$" — khớp Định nghĩa 09.14 |
| nhẹ 6-08 | đã sửa | "$\max_W\mathbb E\lVert\varphi\rVert^2=12$, $G=2\sqrt3$, …" ($8+4=12$) |
| nhẹ 6-00 | đã sửa | "… khi hàm khả vi liên tục, khả tích và có gradient bị chặn bởi hàm khả tích." Hàm chỉ báo của Ví dụ 09.12 không khả vi liên tục theo $\mu$, nên câu vẫn loại phản ví dụ; không dùng thuật ngữ chưa định nghĩa |
| nhẹ 1-02, 6-08 (390 px) | đã sửa | ảnh `narrow-001`, `narrow-046` |
| nhẹ 4-05 ghi chú diễn giả | đã sửa | "nên ước lượng này có rủi ro thực nghiệm nhỏ hơn của phân bố thật nhưng rủi ro kì vọng lớn hơn" ($0{,}6109<0{,}6730$, $0{,}6956>0{,}6730$) |
| nhẹ storyboard §3 | đã sửa (theo §17) | — |

**Mạch truyện.** 5-06 → 6-00 → 6-01: dòng dẫn mới nêu điều kiện; 6-01 mở bằng "Cực đại hóa ELBO bằng hạ gradient ngẫu nhiên … cần $\nabla F$", nối từ EM; ghi chú diễn giả 6-00 nêu lý do bước E không tính được. 6-08 → 7-00 → 7-01: không đổi so với lượt 1, nối được. 4-05 → 4-06 → 4-07 → 4-08: dữ liệu 4-07 đủ để 6-07 ("$50$ chuỗi của Ví dụ 09.8") và 7-03 ("Ví dụ 09.8: $n=200$, $200$ chuỗi kiểm tra") dẫn tới.

**Phát hiện lượt 2.**

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 4-07 (R4) | Để lấy chỗ cho dữ liệu R2, dòng "$m=500$: mô hình thật cũng $1{,}088$: dao động của tập kiểm tra" đã chuyển xuống ghi chú diễn giả. Phát hiện trung bình (9) của chuyên gia (đã chấp nhận, đã sửa ở lượt 1) mở lại: bảng trên mặt trang có $1{,}088$ ở cả ba cột với $m=500$, cạnh "Tốt nhất … $\approx1{,}0904$", mà không có lời giải thích, nên dễ đọc là trái Mệnh đề 09.8(b). | 4-07 cột phải chỉ còn ba dòng (tốt nhất, $m=1$, $m=50$); ghi chú Ví dụ 09.8, Bước 4: "nhưng mô hình thật trên cùng tập kiểm tra cũng cho $1{,}088$, nên đây là dao động của tập kiểm tra" | Đưa lại một dòng ngắn: "$m=500$: mô hình thật cũng $1{,}088$: dao động kiểm tra." (trang đang $51$ âm tiết theo `deck_check.py`, thêm khoảng $12$); nếu vượt $60$, cắt "trung bình $10$ lần chạy" xuống ghi chú diễn giả hoặc điều phối viên quyết |
| nhẹ | 7-03 | Tên tiếng Anh của "hạt giống" rơi khỏi mặt trang (chỉ còn ở ghi chú diễn giả); 7-03 là trang nội dung đầu tiên dùng thuật ngữ này. Phát hiện tên tiếng Anh của sư phạm (lượt 1 đã sửa) mở lại ở mức nhẹ. | 7-03: "độ lệch chuẩn qua mười hạt giống $0{,}0041$"; ghi chú diễn giả: "Mười hạt giống ngẫu nhiên (random seed) …" | "qua mười hạt giống (random seed)"; trang đã là ngoại lệ mật độ |

**Kết luận lượt 2: đạt khi sửa.** Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 1 trung bình (R4, 4-07), 1 nhẹ (7-03). R1–R3 và sáu phát hiện nhẹ của lượt 1 đã đóng. Sau khi sửa R4: kiểm 4-07 ±2, `footer_check.py`, ảnh 4-07 ở hai cỡ.

## Lượt 3 (2026-11-16)

Phạm vi: 4-05…4-08 và 7-03 (±2: 7-02, 7-04) sau khi người sửa xử lý R4 và phát hiện nhẹ ở 7-03 của lượt 2.

| Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|
| R4 4-07, dòng $m=500$ | đã sửa | "$m=500$: mô hình thật cũng $1{,}088$: dao động của tập kiểm tra." — khớp Ví dụ 09.8, Bước 4. "Tốt nhất: $\mathrm H(p_D)/200\approx1{,}0904$" giữ số; "(Mệnh đề 09.8(b))" chuyển xuống ghi chú diễn giả cùng công thức $(\ln4+199\cdot1{,}0889)/200$. Dữ liệu xích Markov ($0{,}6$; $0{,}2$; $0{,}1$; $0{,}1$; $n=200$; $200$ chuỗi kiểm tra; trung bình $10$ lần chạy) vẫn đủ trên mặt trang |
| nhẹ 7-03, tên tiếng Anh | đã sửa | "độ lệch chuẩn qua mười hạt giống (random seed) $0{,}0041$"; dữ kiện và câu hỏi (i), (ii) không đổi so với lượt 2, khớp `exercises.md` Bài tập 09.6(b) |

Mạch truyện: 4-05 → 4-06 → 4-07 → 4-08 không đổi thứ tự hay câu nối; 4-05, 4-06, 4-08 không đổi trong lượt này. 7-02 → 7-03 → 7-04 nối như lượt 2; lời giải 7-04 dùng đúng $m_v=200$ và $c=0{,}087$ có trên 7-03.

Kiểm máy: `deck_lint.py` 1 phát hiện, chỉ 7-03 ($76>60$, ngoại lệ bài tập tổng hợp đã ghi); `footer_check.py` 0 trang; `deck_check.py --shots`: console 0, pageerrors 0, failed 0, `.katex-error` 0; 4-07 $57$ âm tiết. Ảnh 1600×900 và 390×844 (kể cả `-end`) của 4-07 và 7-03: không chạm chân trang, không mảnh mồ côi, bảng 4-07 cuộn ngang trong khung ở 390 px.

**Kết luận lượt 3: đạt.** Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 0 trung bình, 0 nhẹ.
