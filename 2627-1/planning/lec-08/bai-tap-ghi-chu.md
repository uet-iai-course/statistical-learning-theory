# Ghi chú của người soạn bài tập Bài 08

Tệp nội bộ, không liên kết từ trang chỉ mục. Người soạn: tác tử soạn bài tập (2026-10-31). Sản phẩm: `2627-1/materials/lec-08/exercises.md` (8 bài gốc, 32 khối: 8 `exercise`, 16 `hint`, 8 `solution`; 9 265 tiếng theo `wc -w` ở bản đóng băng, 9 283 sau vòng sửa §8).

## 1. Sai khác với `outline.md` §4 (kèm lý do)

Lý do chung: quyết định bài tập Bài 06–07 (`lec-06/reviews/11-quyet-dinh-bai-tap.md`, `lec-07/reviews/11-quyet-dinh-bai-tap.md`) cấm chép lại chứng minh hoặc phép tính đã có trong ghi chú. Nhiều ý của dàn ý §4 đã được ghi chú làm sẵn sau khi biên tập (Ví dụ 08.4, đoạn sau Định nghĩa 08.3, Phụ lục A Bước 2, đoạn sau Mệnh đề 08.10, đoạn sau Hệ quả 08.7, Ví dụ 08.7 Bước 3), nên được thay bằng biến thể mới cùng mục tiêu.

1. **08.1.** Dàn ý (a) "viết đầy đủ chứng minh Mệnh đề 08.5(a)" và (b) "chứng minh $\mathbb E\sum\eta_t\mathbb 1[i_t=i]=\frac1m\sum\eta_t$" là chép lại chứng minh. Thay bằng (a) SGD theo lô nhỏ kích thước $b$ (bước vừa chung vừa khác biệt; tách $f_t$ lồi, $\beta$-trơn, Bổ đề 08.4(b); cận $\frac{2G}m\sum\eta_t$ không phụ thuộc $b$; $1/m=\mathbb En_t/b$). Dàn ý (c) xáo trộn lại đã có ở Phụ lục B(i); thay bằng (b) rút không đều theo $\rho$ cố định ($\epsilon_{\mathrm{stab}}=2G^2\max_j\rho_j\sum\eta_t$; số $0{,}3$ so với $0{,}2$; vì sao $\rho$ phải chọn trước mẫu). Dàn ý (d) ($\tfrac{29}{64}$, đã ở Ví dụ 08.4) thay bằng (c) cùng ví dụ Huber với $\eta=1$: $\mathbb E\Delta_2=\tfrac12$ (đạt cận), $\mathbb E\Delta_3=\tfrac{13}{16}<1$, phần hụt $\tfrac3{16}$ từ hai dãy $(4,1)$, $(4,2)$; $\tfrac{29}{64}$ chỉ dùng ở "Kiểm tra lại".
2. **08.2.** Theo dàn ý. Thêm cận theo (a) (không cần máy) bên cạnh giá trị tính bằng máy; thêm $T=10^5$ cho cận ổn định. Số khớp dàn ý (`c3_more.txt`): $0{,}1000$; $0{,}0098$; $0{,}1986$ và $0{,}0500$; $0{,}6756$; $0{,}1359$; $0{,}0275$; $0{,}5470$; $0{,}0519$.
3. **08.3.** Ví dụ phản chứng $-\tfrac12w^2$ và $\Delta_3/\Delta_2=1{,}1$, $275{,}6$ đã có trong ghi chú. Thay: (a) với $f=1+\cos w$ (hàm lỗi của Ví dụ 08.8 tại $z=0$): đồng bức sai tại $u=0$, $v=\tfrac12$; $q_0=f$, $\nabla q_0(0)=0$ nhưng $q_0(0)=2$ là cực đại; bất đẳng thức then chốt sai tại $v=\pi/2$ ($-1<\tfrac12$). (b) bảng vai trò giả thiết của từng bước Mệnh đề 08.5 và Định lý 08.6, nhất quán với ghi chú sau biên tập N1: tính lồi của hàm lỗi chỉ ở bước chung qua Bổ đề 08.4(a); bước khác biệt dùng phép chiếu không giãn, (G), bất đẳng thức tam giác; Lipschitz từ (G) và $W$ lồi. (c) chứng minh cận dưới $1{,}0878$ cho tỉ số một bước khi $\Delta_t\le\tfrac12$, suy ra chỉ số đầu tiên vượt $\tfrac12$ nằm trong $[68,76]$ (giá trị thật $68$). (d) Mệnh đề 08.10 với $\eta_t=0{,}1/t$: $\le0{,}0149$ (tích phân), $0{,}0136$ (tổng bằng máy), so với cận lồi $0{,}0104$; lịch hằng $275{,}6$ (dẫn ghi chú) so với $0{,}2$.
4. **08.4.** (a) dàn ý (đã có trong ghi chú) mở rộng: kiểm giả thiết Mệnh đề 08.12 cho mẫu Ví dụ 08.8, $\sigma^2=0$, vế phải $40/T$, vế trái $0$, $\operatorname{opt}_s(0)=2$. (b) thêm phản ví dụ không lồi với $W=[-4,4]$. (c) dùng $L_S=0{,}134$ (ghi chú), không phải $0{,}135$ của dàn ý (ghi chú §13.1 đã sửa). (d) thêm $\eta$ tốt nhất $\approx0{,}02355$ và giá trị $\le0{,}0118$.
5. **08.5.** Theo dàn ý. Thêm bảng giả thiết 7 dòng; cách sửa (i) cho cận $0{,}4G^2$ (ví dụ $G=1{,}5$ cho $0{,}9$); cách sửa (ii) cho thừa số $1{,}1^{10^5}>10^{4139}$.
6. **08.6.** Dàn ý dẫn "Phụ lục D" (giao thức) theo chữ cũ; ghi chú hiện là Phụ lục F. Phần bắt buộc dùng số đã chạy (mục 2 dưới đây): bốn bảng 3 cột (bảng 5 cột tràn ở 390 px), bảng hiệu ghép cặp theo hạt giống ở bốn ngân sách bằng nhau ($\eta t=50;500;1000;5000$), sai số chuẩn ghép cặp (theo quyết định Bài 07: hai cấu hình dùng chung hạt giống), so với sai số chuẩn coi độc lập ($0{,}0263$ so với $0{,}0021$ ở $\eta t=5000$), số mũ $0{,}49$ (khoảng cách) và $0{,}57$ ($\Delta$) từ 10 đến 100 vòng. Thêm lỗi phân lớp kiểm tra; phát hiện mới: ở ngân sách $50$ và $500$, $\eta=0{,}25$ cho lỗi phân lớp thấp hơn ($6{,}5$ và $4{,}0$ sai số chuẩn), trong khi hiệu khoảng cách đều dưới $2$ sai số chuẩn. Phần tùy chọn yêu cầu viết chương trình theo Phụ lục F; không nêu đường dẫn script (script nằm trong `tools/`, ngoài repo công khai).
7. **08.7.** Phép tính $39{,}975$, $80$ và so với $0{,}4750$ đã có trong ghi chú (đoạn sau Hệ quả 08.7). Thay (b)–(c) bằng: cận và giá trị đúng $\psi(T)=\frac2m\big(1-\frac{1-q^T}{2\eta T}\big)$ (Ví dụ 06.3 Bước 5, Phụ lục D Bài 06) tại $T=11;161;1600$; ngưỡng $T\le161$ (Hệ quả 08.7) và $T\le80$ (Định lý 08.6) để cận không vượt độ rộng $4$; $\psi(T)<2/m$. Kí hiệu cục bộ $\psi(T)$ (tránh $\gamma$: lề Bài 07).
8. **08.8.** $T^*\approx7071$, $0{,}0958$ đã có ở Ví dụ 08.7; (b) đổi sang $\eta=0{,}1$ ($T^*\approx3535{,}5$, $\le0{,}1208$) và $\eta=0{,}02$ ($T^*\approx17\,677{,}7$, $\le0{,}0808$), giới hạn $\eta\to0$ là $0{,}0708$; $0{,}0958$ chỉ ở "Kiểm tra lại". (d) thêm: Hệ quả 08.8 không áp dụng cho thí nghiệm mở đầu ($W=\mathbb R^p$, đầu ra $w_{T+1}$); chọn số bước bằng mẫu xác thực.
9. **Đoạn mở** nêu "chương 12–14" theo §11 của ghi chú (dàn ý §4 viết "13–14").

Mục tiêu được đo: 1 (08.1); 2 (08.3); 3 (08.1, 08.2, 08.7); 4 (08.2, 08.8); 5 (08.3, 08.4, 08.5, 08.6). Năm loại bài: chứng minh, tính toán, khái niệm, kiểm tra giả thiết, thực nghiệm tùy chọn.

## 2. Thí nghiệm (Bài tập 08.6)

Script của ghi chú (không sửa): `../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec08_coupled_sgd.py`, chạy `--eta 0.5` (mặc định) và `--eta 0.25`; đầu ra scratchpad `ex08/exp_eta05.txt`, `ex08/exp_eta025.txt`. Số từng hạt giống lấy bằng scratchpad `ex08/run_seeds.py` (nạp hàm `run` của script, ghi `seeds_eta0.5.json`, `seeds_eta0.25.json`); tổng hợp bằng `ex08/nums3.py`, `ex08/nums4.py`. Cột $\eta=0{,}5$ khớp từng số của ghi chú (câu hỏi mở đầu, Ví dụ 08.6, Phụ lục F).

Trung bình 20 hạt giống (bốn chữ số; bài tập ghi ba chữ số, làm tròn gần nhất):

| Vòng | KC 0,25 | KC 0,5 | $\Delta$ 0,25 | $\Delta$ 0,5 | Đổi nhãn 0,25 | Đổi nhãn 0,5 | 0–1 0,25 | 0–1 0,5 |
|---|---|---|---|---|---|---|---|---|
| 0,5 | 0,0246 | 0,0445 | 0,0727 | 0,1417 | 0,0151 | 0,0152 | 0,3839 | 0,3827 |
| 1 | 0,0464 | 0,0792 | 0,1244 | 0,2332 | 0,0156 | 0,0160 | 0,3609 | 0,3562 |
| 5 | 0,1470 | 0,2131 | 0,5229 | 0,8732 | 0,0205 | 0,0218 | 0,3138 | 0,3089 |
| 10 | 0,2121 | 0,2977 | 0,9306 | 1,4719 | 0,0233 | 0,0257 | 0,3029 | 0,3011 |
| 20 | 0,2991 | 0,4192 | 1,4469 | 2,2185 | 0,0242 | 0,0262 | 0,2996 | 0,3009 |
| 50 | 0,4613 | 0,6503 | 2,5308 | 3,7320 | 0,0283 | 0,0310 | 0,2999 | 0,3043 |
| 100 | 0,6511 | 0,9188 | 3,7448 | 5,4583 | 0,0311 | 0,0339 | 0,3054 | 0,3118 |

(Đổi nhãn 0,25 ở 5 vòng: 0,02052 → 0,021.)

Hiệu ghép cặp ($\eta=0{,}25$ trừ $\eta=0{,}5$, cùng hạt giống, cùng ngân sách): trung bình (độ lệch chuẩn của 20 hiệu); SE $=$ độ lệch chuẩn $/\sqrt{20}$.

| $\eta t$ | KC | SE | 0–1 | SE |
|---|---|---|---|---|
| 50 | 0,0019 (0,0048) | 0,0011 | −0,0218 (0,0151) | 0,0034 |
| 500 | −0,0010 (0,0074) | 0,0017 | −0,0061 (0,0068) | 0,0015 |
| 1000 | 0,0013 (0,0059) | 0,0013 | −0,0015 (0,0064) | 0,0014 |
| 5000 | 0,0008 (0,0096) | 0,0021 | 0,0012 (0,0040) | 0,0009 |

Ở $\eta t=5000$: độ lệch chuẩn khoảng cách $0{,}0847$ ($\eta=0{,}25$), $0{,}0817$ ($\eta=0{,}5$); SE coi độc lập $0{,}0263$; tương quan theo hạt giống $0{,}994$. Số mũ (từ bảng ba chữ số, $\eta=0{,}5$, 10→100 vòng): khoảng cách $\ln(0{,}919/0{,}298)/\ln10\approx0{,}49$; $\Delta$ $\ln(5{,}458/1{,}472)/\ln10\approx0{,}57$. Tỉ số cận/khoảng cách với $\eta=0{,}25$: $0{,}25/0{,}025=10$; $50/0{,}651\approx76{,}8$.

## 3. Các con số khác và script (scratchpad `ex08/`)

| Bài | Con số | Script |
|---|---|---|
| 08.1(c) | $\mathbb E\Delta_2=\tfrac12$, $\mathbb E\Delta_3=\tfrac{13}{16}$ ($\eta=1$); $\tfrac{29}{64}$ ($\eta=\tfrac12$) | `nums.py` (liệt kê phân số đúng) |
| 08.1(b) | $0{,}3$ và $0{,}2$ | tay |
| 08.2 | $H_{10^4}\approx9{,}787606$, $H_{10^5}\approx12{,}090146$, $\sum t^{-1/2}\approx198{,}544645$; $630{,}996759$; $\sum t^{-2}\approx1{,}644834$; $1{,}644924$; bảng cận ở mục 1.2; cận theo (a) $51{,}06$, $995$, $62{,}57$, $3157{,}28$, $0{,}0103$, $0{,}199$, $0{,}0126$, $0{,}6315$ | `nums2.py` |
| 08.3(a) | $-0{,}2397<0{,}2298$; $-1<\tfrac12$ | `nums2.py` |
| 08.3(c) | $\Delta_2\approx0{,}00099998$; $\ln(0{,}5/\Delta_2)\approx6{,}2146$; $\ln1{,}1\approx0{,}0953$, $\ln1{,}087758\approx0{,}08412$; $1{,}087758^{74}\Delta_2\approx0{,}5051$; $\tau=68$ | `nums4.py` |
| 08.3(d) | $\sum_{t\le100}t^{-1{,}1}\approx4{,}2780$, tích phân $4{,}6904$; cận $0{,}014868\to0{,}0149$, $0{,}013560\to0{,}0136$; tích đúng $0{,}013337$; cận lồi $0{,}010375$; $e^{0{,}5187}\approx1{,}680$; $e^{10}\approx22\,026$ | `nums2.py`, `nums4.py` |
| 08.4(d) | $1{,}0000347\to1{,}0001$; $\eta\approx0{,}023548$; $0{,}011774\to0{,}0118$ | `nums2.py` |
| 08.5 | $\ell(1)\approx0{,}31326$; trung bình $0{,}50320$; $0{,}4$ | `nums2.py` |
| 08.7 | $\psi(11)\approx0{,}030107$, $\psi(161)\approx0{,}284340$, $\psi(1600)=0{,}4750$; $q^{11}\approx0{,}87078$, $q^{161}\approx0{,}13197$; tỉ số $8{,}30$; $14{,}07$; $84{,}16$ | `nums2.py`, `nums4.py` |
| 08.8 | $T^*$: $3535{,}53$; $7071{,}07$; $17\,677{,}67$; $B(T^*)$: $0{,}1207007\to0{,}1208$; $0{,}0957057\to0{,}0958$; $0{,}0807087\to0{,}0808$; giới hạn $0{,}0707107\to0{,}0708$ | `nums2.py` |

Quy tắc làm tròn: cận trên làm tròn lên, số đo làm tròn gần nhất.

## 4. Kiểm tra đã chạy

`sync-local-materials.py` và `--check` (OK); không có khoảng trắng cuối dòng trong `exercises.md` (tệp chưa theo dõi nên `git diff --check` không áp dụng; kiểm bằng `grep`); 32 khối mở, 32 khối đóng, không lồng; `wc -w` 9 265; không có "Đáp án", "hãy" (ngoài đề), "rõ ràng", "dễ thấy", không có chữ có dấu trong `\text{}`. Viewer qua HTTP (`reloadserver` cổng 8791, đã tắt), mọi `details` mở, ở 390×844 và 1600×900: 1 271 công thức KaTeX, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức hay bảng tràn (13 công thức tràn ở lần đo đầu đã tách bằng `aligned`), độ rộng trang 375 px ở 390. Console có một cảnh báo CSP do `reloadserver` chèn script nội tuyến (như Bài 07). Ảnh chụp ở scratchpad `ex08/`.

## 5. Điểm không chắc

1. **08.1(a)** là kết quả mới (không có trong ghi chú); người rà toán nên kiểm Bước 2 (tính $\beta$-trơn của $f_t$ với hệ số $\tfrac{b-n_t}b\le1$) và việc dùng Bổ đề 08.4(b) với cùng $\eta_t\le2/\beta$.
2. **08.1(b) Bước 4** (vì sao $\rho$ phải chọn trước mẫu) lập luận bằng lời qua Định nghĩa 05.18 và ghép cặp.
3. **08.5(d)(ii)** khẳng định gradient Lipschitz trên $W$ bị chặn khi hàm kích hoạt có đạo hàm bậc hai bị chặn, và lập luận của Mệnh đề 08.10 chỉ cần tính trơn trên $W$ (Phụ lục D, Bước 1 dùng hai điểm lặp trong $W$); ghi chú phát biểu Mệnh đề 08.10 với tính trơn trên $\mathbb R^p$.
4. **08.6**: kết luận "ở ngân sách nhỏ, lỗi phân lớp phụ thuộc cả $\eta$" dựa trên hai ngân sách ($6{,}5$ và $4{,}0$ sai số chuẩn ghép cặp), một thiết lập, 20 hạt giống. Bảng hiệu ghép cặp cần dữ liệu từng hạt giống, nên được cho sẵn trong đề.
5. **Độ dài**: 9 265 tiếng, sát trần 10 000; nếu người rà yêu cầu thêm nội dung, cần cắt ở chỗ khác (ứng viên: 08.2 Bước 5, 08.6(c)).

## 8. Vòng sửa theo `reviews/11-quyet-dinh-bai-tap.md` (2026-10-31)

Căn cứ: `reviews/9-bai-tap-toan.md` (0/0/0/3), `reviews/10-bai-tap-su-pham.md` (0/0/4/20), quyết định của điều phối viên (7 mục và các điểm nhẹ). Bản trước khi sửa: scratchpad `ex08/exercises_before_fix.md`.

**Đã áp dụng.**

1. Toán 1: 08.6, ô $\eta t=50$, tỉ số $1{,}8\to1{,}7$.
2. Toán 2: bảng 08.3, ô "08.5, Bước 1" thêm "$W$ lồi".
3. Toán 3 (và N18): 08.5(d)(ii) nói rõ Nhận xét 08.11 phát biểu cho SGD không chiếu, hàm lỗi trong $[0,1]$; cần chia hàm lỗi cho cận trên và kiểm lại lập luận khi có phép chiếu. Câu Phụ lục D tách khỏi ngoặc.
4. T1: 08.6 dùng "sai số chuẩn của hiệu theo hạt giống" ở mọi chỗ (đề (a)(ii), lời giải Bước 3, 4, (b) Bước 1, (c)); "ghép cặp" chỉ còn cho hai lần chạy (tiêu đề và bảng $\Delta$).
5. T2: 08.3 thêm ý (a) mới, chứng minh trực tiếp tính không giãn của bước gradient cho hàm lỗi Huber với $0\le\eta\le2$ ($\delta=d(u)-d(v)\in[0,u-v]$, $\Gamma(u)-\Gamma(v)\in[(1-\eta)(u-v),u-v]$), vai trò của tính lồi (cận trên) và của $\eta\le2/\beta$ (cận dưới), phản ví dụ $\eta=3$, $u=0{,}2$, $v=-0{,}2$ cho hệ số $2$ (khớp Ví dụ 08.3). Kiểm bằng scratchpad `ex08/huber_nonexp.py`: tỉ số lớn nhất trên khoảng $4\cdot10^7$ bộ ngẫu nhiên với $\eta\in[0,2]$ là $1{,}0000$; $\eta=2{,}5$ cho $1{,}5$, $\eta=3$ cho $2$. Các ý cũ (a)–(d) thành (b)–(e); gợi ý, lời giải và "Kiểm tra lại" đánh lại theo.
6. T3: cắt 08.8(c) (ghép sai đầu ra; ghi chú đã nêu ở §8) cùng hai câu gợi ý và lời giải; (d) thành (c); mục tiêu bỏ "nhận ra một cách ghép cận sai".
7. T4: 08.5 câu đầu có động từ chính ("Một báo cáo mô tả việc huấn luyện …"); (d)(ii) nêu "đạo hàm cấp một và cấp hai bị chặn" trong đề; bảng bỏ $\mathbb R^P$ ("$W$ là toàn bộ không gian tham số"); lời giải Bước 2 nói đạo hàm cấp hai bị chặn là giả thiết.
8. Nhẹ: tiếng Anh ở lần đầu (gradient step map, stability coefficient, recurrence inequality, expected generalization gap, co-coercivity, "còn gọi là bổ đề hạ", stationarity, stationary point, standard deviation); năm dòng "Mục tiêu" rút ngắn (08.1, 08.2, 08.3, 08.6, 08.8; thêm 08.4, 08.5); 08.1(c) "nhỏ hơn ngặt cận của Mệnh đề 08.5(a)", "Phần hụt là …", câu $\tfrac3{16}$; cắt câu lặp ở "Kiểm tra lại" 08.1; dấu hai chấm ở 08.1(b) Bước 3 và 08.7(a) Bước 1; bảng ngân sách 08.2(b) Bước 2; 08.2(c) "độ chênh tối ưu", "đọc thêm của Bài 05", $R\ge\lVert w_1-u\rVert$, bỏ nhãn "Lưu ý:", lời giải Bước 4 tự chứng minh $\sum1/t^2\le2$; 08.3 thay đoạn tóm tắt (bỏ "hỏng"), "Tính bằng máy", "cận nhân thêm một thừa số hàm mũ"; 08.4(c) Bước 1 viết lại, gợi ý (a) tăng dần, câu đề (c) tách; 08.5 "Kiểm tra lại" mới ($10/(1+e)\approx2{,}69$, kiểm bằng Python); 08.6 câu dẫn bảng, câu giải thích ô lên trước bảng, bỏ câu "Cận cũng chỉ phụ thuộc $\eta t$", bỏ gạch đầu dòng "Phạm vi", "che mất" thay bằng số; 08.7 bỏ câu "Lời hứa của Bài 06 …"; 08.8 bỏ câu "$10^{-8}$", tách câu dài ở Bước 4; tách câu dài ở 08.1(a), 08.3(b) Bước 2, 08.6(b).

**Không áp dụng (lý do).**

- T1, đề xuất thêm thuật ngữ "sai số chuẩn của hiệu theo hạt giống" vào `thuat-ngu.md`: ngoài phạm vi ghi của người soạn; chuyển điều phối viên.
- Đề xuất "Tỉ số $0{,}25/0{,}0246=10{,}2$" (người rà toán, bảng §2): giữ $10$ vì lời giải tính từ số ba chữ số trong bảng của đề ($0{,}25/0{,}025$); người rà không ghi thành phát hiện.

**Kiểm tra sau sửa.** `sync` và `--check` OK; 0 khoảng trắng cuối dòng; 32 khối mở, 32 khối đóng, không lồng; 9 283 tiếng; không có `\text{}`. Viewer qua HTTP (cổng 8791, đã tắt), mọi `details` mở, ở 390×844 và 1600×900: 1 320 công thức, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức hay bảng tràn; chỉ cảnh báo CSP của `reloadserver`. Ảnh `ex08/huber390.png`.

### 8.1. Sửa theo `reviews/13-ra-lai-bai-tap-su-pham.md` (2026-10-31)

Áp dụng M1–M5 theo đề xuất, không sửa gì khác. M1: 08.6 lời giải Bước 3 bỏ câu lặp ("Sai số chuẩn bằng độ lệch chuẩn của các hiệu chia cho $\sqrt{20}$."). M2: 08.6 Bước 4 bỏ lần thứ hai của "khoảng $12$ lần". M3: 08.7(a) Bước 1 bỏ "nên … nên" ("; do đó (S) đúng với $\beta=2$"). M4: 08.5(d) Bước 2 tách thành "Bước 2: hằng số trên $W$" và "Bước 3: cận không lồi"; câu cuối về Nhận xét 08.11 tách đôi. M5: 08.2(b) tách câu 45 tiếng ("Tính trước hết bằng (a), rồi bằng …").
