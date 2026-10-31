# Ghi chú của người soạn bài tập — Bài 07

Tệp nội bộ, không liên kết từ trang chỉ mục. Người soạn: sub-agent "soạn bài tập" (2026-10-31), ghi `2627-1/materials/lec-07/exercises.md`. Không commit.

Sản phẩm: 9 bài (07.1–07.6 gốc theo blueprint 7.5; 07.7–07.9 chọn từ UML), 36 khối (9 `exercise`, 18 `hint`, 9 `solution`), 868 dòng, 9771 tiếng (`wc -w`, trần 10 000). SHA-256 lúc bàn giao bắt đầu `25540909ffa6bbc8`. Script tính số và kết quả: scratchpad `ex07/nums.py`, `ex07/nums.txt`; thí nghiệm: `ex07/exp_m{100,200,400,800}.txt`; kiểm trình xem: `ex07/probe.py` (scratchpad của phiên, ngoài repo).

## 1. Số bài UML đã kiểm trên PDF

Đọc `sources/uml/understanding-machine-learning-theory-algorithms.pdf` bằng pymupdf, tr. 282–283 (trang PDF trùng số trang in; §20.9 bắt đầu tr. 282, có đúng 6 bài).

| Bài tập học phần | Bài UML | Trang PDF | Ghi chú |
|---|---|---|---|
| 07.7 | 20.3 "Growth function of product" | 282 | thêm (b) bất đẳng thức thực sự, (c) một lớp nơ-ron ngưỡng |
| 07.8 | 20.4 "Growth function of composition" | 282 | thêm (b) vai trò của điểm lặp, (c) chiều VC của mạng ngưỡng $P=100$ |
| 07.9 | 20.1 "Neural Networks are universal approximators" | 282 | tùy chọn; phát biểu đã sửa: ReLU, một biến (QĐ dàn ý 11) |

## 2. Tự giải trước, đối chiếu sau

Lời giải của cả ba bài UML (lập luận và mọi con số, `nums.py`) được lập xong trước khi mở `sources/uml/MLbookSol.pdf`. Bản lời giải (tr. 50–51, chương 20) được mở một lần lúc **2026-10-31 20:41** (giờ ghi bằng `date` ngay trước lệnh đọc); văn bản `exercises.md` viết sau đó, không mở lại bản lời giải.

| Bài | Chỗ bản lời giải sai hoặc thiếu | Cách viết của học phần khác ở đâu |
|---|---|---|
| 20.3 | Đẳng thức $\lvert\mathcal H_C\rvert=\lvert\mathcal F_{1C}\rvert\cdot\lvert\mathcal F_{2C}\rvert$ cho một $C$ cố định đúng, nhưng kết luận viết $\tau_{\mathcal H}(m)=\tau_{\mathcal F_2}(m)\tau_{\mathcal F_1}(m)$ — sai, chỉ có "$\le$" (hai lớp có thể đạt giá trị lớn nhất tại hai bộ khác nhau). | Kết luận "$\le$" với lý do; (b) dựng phản ví dụ hai lớp hai hàm trên $\{1,2\}$, $m=1$: $\Pi=2<4$; (c) quy nạp cho lớp $N_1$ nơ-ron ngưỡng, $\Pi\le(em)^{N_1(p+1)}$, xử lý cả $m<p+1$. Dùng $\Pi$ với bộ điểm cho phép lặp. |
| 20.4 | Lại kết luận "$=$" (sai, chỉ "$\le$"). Bước "$\le\lvert\mathcal F_{1C}\rvert\cdot\tau_{\mathcal F_2}(m)$" bỏ qua việc bộ $(f_1(c_1),\ldots,f_1(c_m))$ có thể có phần tử lặp: với định nghĩa theo tập của UML, cần tính không giảm của $\tau$ và cần $\lvert\mathcal Z\rvert\ge m$; khi $\mathcal Z$ hữu hạn nhỏ (như $\{0,1\}^{N_1}$ trong mạng) $\tau_{\mathcal F_2}(m)$ không xác định. Dòng đầu thiếu dấu ngoặc tập hợp. | Bước 2 của lời giải nêu rõ chỗ dùng định nghĩa cho phép lặp; (b) dựng tình huống $\mathcal X'=\{0,1\}$, $m=3$; (c) ghép với 07.7(c) và bổ đề Sauer–Shelah cho $\Pi\le(em)^P$ của mạng ngưỡng một lớp ẩn, $P=100$ cho chiều VC $\le1162$. |
| 20.1 | Quy về "$f$ xác định trên tập rời rạc các tâm hộp" rồi nói sigmoid "xấp xỉ được hàm chỉ thị trên miền hữu hạn": miền là liên tục; mạng sigmoid có đầu ra liên tục, không xấp xỉ đều hàm chỉ thị của hộp gần biên (sai số ít nhất $\tfrac12$), nên lời giải không kiểm soát sai số tại điểm gần biên hộp. Ngoài ra $d$ dùng thay $n$, "$\beta\in[0,2]$" không ràng buộc gì. | Phát biểu đã sửa (ReLU, một biến): nội suy tuyến tính từng khúc là mạng $k$ nơ-ron, sai số $\le G/k$ (chứng minh qua tổ hợp lồi, chỉ ra cận đạt được); (c) đếm số hình lập phương $k^p$ của cách chia theo gợi ý UML ($2^{50}$ khi $p=10$) và nói rõ đó không phải cận dưới; (d) chứng minh hàm liên tục không xấp xỉ đều hàm chỉ thị với sai số $<\tfrac12$, chính là chỗ hổng của bản lời giải. |

Không câu nào của `exercises.md` dịch đề hay lời giải UML; đề viết bằng kí hiệu học phần ($\Pi_{\mathcal H}$, $\mathcal H_1$, $\mathcal H_2$, $\mathcal X'$, $\varsigma$, $G$, $p$).

## 3. Sai khác so với `outline.md` §4 và lý do

1. **07.1(a).** Dàn ý: "kiểm bốn giá trị của Mệnh đề 07.2" — đó là chứng minh đầy đủ đã có trong ghi chú (bài học từ rà soát bài tập Bài 06: không chép lại chứng minh có sẵn). Thay bằng mạng thứ hai cùng kiến trúc $f_{\theta_{\mathrm{abs}}}=\lvert x_1-x_2\rvert-\tfrac12$; (c) so hai miền (dải $\tfrac12\le x_1+x_2\le\tfrac32$ và hợp hai nửa mặt phẳng) và nhãn khác nhau tại $(\tfrac12,\tfrac12)$: phân lớp đúng mẫu không xác định hàm ngoài mẫu. (b), (d) như dàn ý; (d) thêm số tham số $16$.
2. **07.2.** (a) thêm bảng tám bộ dấu và giải thích; (b) thêm so sánh Định lý 07.11 với Hệ quả 02.10(c) cho lớp một phần tử ($0{,}2881$ so với $0{,}0866$) và chỉ bước làm cận yếu đi (hai lần McDiarmid) — nối với mục tiêu 3; (c) thêm liệt kê $\tau$ để kiểm Mệnh đề 07.9(a) ($\mathbb E\min\operatorname{err}_\tau=\tfrac14$) — đo phần "nối với lỗi khớp nhãn ngẫu nhiên" của mục tiêu 2; (d) thêm lập luận Bổ đề 07.8 hỏng với quy ước có trị tuyệt đối. Dòng "Mục tiêu" ghi mục tiêu 2 (khớp §11 ghi chú).
3. **07.3.** Dàn ý (a) "viết đầy đủ chứng minh Mệnh đề 07.13" là chép lại chứng minh đầy đủ của ghi chú. Thay bằng chứng minh mở rộng cho lớp afin $\mathcal F_{B,B_0}$ (có hệ số tự do), cận $(BC_x+B_0)/\sqrt m$, với nhãn giả thiết tại từng bước (vẫn đo đúng ý blueprint "Prove the linear norm bound"); (b) mới: so với cách thêm tọa độ hằng ($0{,}06$ so với $0{,}0633$); (c) thay "dấu bằng khi trực chuẩn" (đã có ở Ví dụ 07.7) bằng điều kiện cần và đủ: đẳng thức khi và chỉ khi các $x_i$ đôi một vuông góc, kiểm với $(1,0),(1,1)$ ($0{,}8090B<0{,}8660B$); (d) như dàn ý; (e) thêm cận theo lề ($0{,}0141$) và cận logistic ($0{,}0304$) để đo phần "tính bằng số cận theo lề" của mục tiêu 4.
4. **07.4.** (b) bán kính làm tròn lên $0{,}1095$ (dàn ý ghi $0{,}1094$, làm tròn gần nhất); (c) bỏ việc lặp lại Ví dụ 07.5 đơn thuần, thay bằng $\mathbb E_\tau\min\operatorname{err}_\tau=0$ và vế phải $1{,}2881$ với $P/m=0{,}005$; (d) mới: ba giả thiết của Định lý 07.11, bước dùng và tình huống vi phạm trong bài (đo mục tiêu 3, mục "kiểm tra giả thiết").
5. **07.5.** (b) chứng minh bằng quy nạp với mọi quy ước $\operatorname{ReLU}'(0)$, mọi $\eta$; thêm $b_2$ giữ $0$ vì $\sum\tilde y_i=0$, và SGD (chỉ $b_2$ đổi, lỗi vẫn $\tfrac12$). Kiểm bằng số (1000 bước, $\eta=0{,}1$, ba quy ước; SGD 1000 bước): $\theta$ giữ $0$, lỗi $\tfrac12$. (c) điểm mở 10 của dàn ý: tính lại $F(\theta_{\mathrm{mid}})=27/16=1{,}6875$ — khớp; hàm mục tiêu là trung bình bình phương với đích $\tilde y/2$. (d) dùng Mệnh đề 04.3 với $D$ đều trên bốn quan sát: toàn bộ rủi ro vượt mức $\tfrac12$ là $\operatorname{opt}_S$.
6. **07.6.** Theo lời giao: giao thức có mẫu kiểm tra độc lập, nhiều hạt giống; phần tính bắt buộc dùng số đã chạy (bốn cỡ mẫu). Thêm (b) về sai số chuẩn: từ $m=400$ đến $800$, hiệu $0{,}0013$ nhỏ hơn sai số chuẩn của hiệu ($\approx0{,}002$), nên không kết luận được lỗi kiểm tra giảm. Cận dưới của số hạng Rademacher dùng $C_x\ge1{,}5$ và làm tròn **xuống** (cận dưới). Bảng chia ba bảng ba cột để vừa 390 px.
7. **07.7, 07.8.** Như dàn ý; (c) của 07.8 dùng kiến trúc $p=9$, $N_1=9$ để có $P=100$ (dàn ý ghi $\lvert E\rvert=100$ theo đồ thị UML); thêm lập luận $m\le144$ không thỏa để chắc $1163$ là giá trị nhỏ nhất. "Hàm kích hoạt ngưỡng" $\varsigma(t)=\mathbb 1[t\ge0]$ là thuật ngữ mới (bản $\{0,1\}$ của "hàm kích hoạt dấu" ở Nhận xét 07.6).
8. **07.9.** Bỏ ý tùy chọn "thay ReLU bằng sigmoid" của dàn ý (dài, ngoài ngân sách); thay bằng (d) ngắn chứng minh vì sao hàm liên tục không xấp xỉ đều hàm chỉ thị — đúng chỗ hổng của bản lời giải. Thêm ví dụ đạt cận $f(x)=\lvert x-0{,}1\rvert-0{,}5$. $n$ của UML viết $p$, $\rho$ viết $G$.
9. **Không có trong dàn ý:** chuẩn bị "Kiểm tra lại" cho mọi bài; không dùng kết quả "liệt kê bằng máy" làm lý do (chỉ dùng số đo ở 07.6, 07.9, ghi là số đo).

## 4. Kí hiệu cục bộ mới (đề xuất cho `ky-hieu.md`, người soạn không sửa tệp đó)

$\theta_{\mathrm{II}}$, $\theta_{\mathrm{par}}$ (07.1); $\theta_{\mathrm{swap}}$, $\theta_{\mathrm{mid}}$ (07.5); $\mathcal F_{B,B_0}$, $B_0$, $v_\sigma$ (07.3, $v_\sigma$ như chứng minh Mệnh đề 07.13); $h_a$, $h_{a'}$, $u$, $v$ (07.2, cục bộ trong lời giải); $\bar B$ (07.6, chuẩn trung bình); $\mathcal H_1$, $\mathcal H_2$, $\mathcal Y_1$, $\mathcal Y_2$, $\mathcal X'$ (07.7–07.8; ở 07.8(c) dùng lại $\mathcal H_1$, $\mathcal H_2$ của (a); $\mathcal H_k$ theo nghĩa "lớp thứ $k$" của Bài 04); $t_i$, $\mu_i$, $\Delta\mu_i$, $\alpha$, $\tilde f$ (07.9). Tránh có chủ ý: $\mathcal F_1,\mathcal F_2$ (trùng $\mathcal F_B$ với $B=2$ ở câu hỏi cuối buổi), $Q$, $c_{ij}$ (trùng hàm và hằng số McDiarmid), $\beta_i$ ($\beta$ là hằng số trơn), $r$ cho đạo hàm ReLU (trùng bán kính $r$ của Mệnh đề 04.3), $\mathcal Z$ cho tập trung gian (trùng tập quan sát).

## 5. Bảng con số và nguồn

Mọi số tính bằng `/data/tqlong/lectures/.venv/bin/python` (`ex07/nums.py` → `nums.txt`); cận trên làm tròn lên, khoảng quan sát làm tròn gần nhất, cận dưới làm tròn xuống.

| Bài | Con số | Giá trị chính xác hoặc nguồn |
|---|---|---|
| 07.1 | $f_\theta$, $f_{\theta_{\mathrm{abs}}}$ tại 4 điểm; $f_{\theta_{\mathrm{par}}}$ tại 8 điểm; số tham số $9$, $16$ | liệt kê trong `nums.py` |
| 07.2 | $\max\tfrac13\sum\sigma_ia_i=0{,}4$; trung bình $0$; $7/30\approx0{,}2333$ | liệt kê 8 bộ dấu |
| 07.2 | $3\sqrt{\ln40/400}\le0{,}2881$ (0,288097); $\sqrt{\ln20/400}\le0{,}0866$ (0,086541); tỉ số $3{,}33$ | khớp Ví dụ 07.6 |
| 07.2 | $\widehat{\mathfrak R}(\{a,a'\})=\tfrac14$; $\mathbb E\min\operatorname{err}_\tau=6/24$ | liệt kê, khớp Ví dụ 07.4 |
| 07.3 | $0{,}06$; $\sqrt{10}/50\le0{,}0633$ (0,063246); $0{,}8090B$, $0{,}8660B$; $0{,}005$; $0{,}004074$; $0{,}0141$ (0,014074); $K\approx5{,}0067$; $0{,}0304$ (0,030399) | `nums.py`; liệt kê dấu cho $(1,0),(1,1)$ |
| 07.4 | $r_m\le0{,}1095$ (0,109402); $r_m^+\le0{,}1012$ (0,101172); $1{,}2881$; $\ln120\approx4{,}7875$ | `nums.py` |
| 07.5 | $F(\theta)=F(\theta_{\mathrm{swap}})=0$; $F(\theta_{\mathrm{mid}})=1{,}6875$; GD và SGD từ $0$: lỗi $\tfrac12$ | `nums.py` (GD 1000 bước, ba quy ước ReLU′(0); SGD 1000 bước) |
| 07.6 | bảng lỗi kiểm tra, chuẩn, khoảng, độ lệch chuẩn; tỉ số $8{,}45$; $11{,}85$; $12{,}05$; $21{,}84$; cận dưới $134{,}0$; $194{,}2$; $345{,}1$; $609{,}3$; $\alpha\approx1{,}23$; tỉ số tăng $4{,}55$; trung bình số hạng Rademacher $136{,}5$; $197{,}9$; $352{,}1$; $620{,}1$ | `exp_m*.txt` từ `../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec07_random_labels.py m` |
| 07.7 | $\Pi=2<4$; $16$; $(2e)^4\approx874$ | tay |
| 07.8 | $P=100$; $m=1163$ nhỏ nhất ($805{,}88<806{,}13$; tại $1162$: $805{,}79>805{,}44$); tỉ số $1{,}42$, $0{,}78$; $d\le1162$ | `nums.py` |
| 07.9 | $k=10$, $31$ tham số; sai số đo $0{,}0149$ (0,014851, lưới 200 001 điểm) cho $\sin(3x)/3$; $k=15$, $225$; $k=32$, $2^{50}\approx1{,}13\cdot10^{15}$ | `nums.py` |

**Thí nghiệm (mười hạt giống 0–9, $N=2000$, 5000 điểm kiểm tra).** Chạy từ gốc repo: `../.venv/bin/python ../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec07_random_labels.py m`.

| $m$ | Lỗi KT thật (độ lệch chuẩn) | Lỗi KT hoán vị | $\lVert\hat w\rVert$ thật: trung bình (nhỏ nhất–lớn nhất) | $\lVert\hat w\rVert$ hoán vị | $C_x$ | Hạng |
|---|---|---|---|---|---|---|
| 100 | 0,03404 (0,00988) | 0,49902 | 446,721 (252,571–871,462) | 3774,25 (2731,42–8750,29; trình bày $3774{,}2$) | 1,5173–1,5439 | 100; 200 |
| 200 | 0,02298 (0,00736) | 0,50108 | 915,67 (351,478–1720,82) | 10 852,6 (6791,53–14 051,9) | 1,5176–1,5440 | 200; 400 |
| 400 | 0,01466 (0,00401) | 0,4994 | 2301,33 (1111–3316,58) | 27 739,3 (18 311,7–46 585,5) | 1,5224–1,5383 | 400; 800 |
| 800 | 0,01336 (0,00499) | 0,49902 | 5744,7 (3532,13–9249,8) | 125 453 (76 307,1–316 483) | 1,5173–1,5364 | 800; 1600 |

Lỗi huấn luyện $0$ và lề nhỏ nhất $1$ trong mọi lần chạy. Số của $m=200$ trùng ghi chú (câu hỏi mở đầu, Ví dụ 07.10).

## 6. Kiểm tra đã chạy

- `sync-local-materials.py` và `--check`: OK. `git diff --check`: sạch. Khối `:::` cân bằng, không lồng (36 mở, 36 đóng). `wc -w`: 9771.
- Trình xem qua HTTP (reloadserver cổng 8781, đã tắt), mọi `details` mở: 390×844 và 1600×900 — 0 `.katex-error` (1241 công thức), 0 công thức/bảng tràn, không tràn ngang trang, 0 yêu cầu lỗi. Một lỗi console CSP "inline script" do reloadserver chèn script; cùng lỗi xuất hiện trên trang bài tập Bài 06, không do tệp này. Ảnh chụp đã xem: đầu trang 1600, các bảng của 07.6 ở 390 và 1600, 07.5 và 07.7 ở 390.
- Không có "Đáp án", "hãy", "rõ ràng", "dễ thấy", "hiển nhiên", "chính là"; tiêu đề không có "Từ … đến …" hay câu hỏi; không chữ có dấu trong `\text{}`.

## 7. Điểm cần người rà soát kiểm

1. 07.3(c): điều kiện cần và đủ cho đẳng thức (Jensen chặt + mô-men bậc hai của tổng chéo).
2. 07.5(b): công thức gradient theo từng khối và quy nạp; $\nabla_{\Theta_1}f_\theta=\nabla_{b_1}f_\theta\,x^\top$.
3. 07.6(b) Bước 3: dùng sai số chuẩn $\mathrm{sd}/\sqrt{10}$ coi mười lần chạy độc lập (mỗi $m$ dùng cùng hạt giống 0–9, nên hai cỡ mẫu không độc lập hoàn toàn; kết luận "không phân biệt được" vẫn đứng).
4. 07.8(b): cách nói về định nghĩa theo tập của UML khi họ rỗng.
5. 07.9(c): "cận dưới theo hàm mũ của $p$ là kết quả của UML §20.3 (Nhận xét 07.3)" — Nhận xét 07.3 nêu cho mạng sigmoid; người rà kiểm cách diễn đạt.
6. 07.1 dùng tên tham số $\theta_{\mathrm{abs}}$, $\theta_{\mathrm{par}}$ (chỉ số Latin, không dấu).

## 8. Sửa theo hai lượt rà (2026-10-31)

Căn cứ: `reviews/11-quyet-dinh-bai-tap.md` (bắt buộc), `reviews/9-bai-tap-toan.md`, `reviews/10-bai-tap-su-pham.md`. Đã áp dụng:

- **Toán 1–4.** $3774{,}2$ (bảng và tỉ số; tỉ số vẫn $8{,}45$), $46\,585$; 07.6(b) Bước 3 nêu hai nhóm dùng chung hạt giống và sai số chuẩn ghép cặp $0{,}0019$ (theo người rà 2; kết luận không đổi); 07.7, 07.8 ghi "(a) là UML …; (b), (c) do học phần thêm"; 07.9 dùng $k=\max\{1,\lceil G/\epsilon\rceil\}$.
- **Sư phạm 5–8.** "lớp hàm hợp" ở tiêu đề, đề, gợi ý, lời giải 07.8 và đúng một dòng §11 của ghi chú (ngoại lệ phạm vi); "lực lượng của hợp các tập $(\mathcal H_2)_u$"; 07.8(b) bỏ $\tau_{\mathcal H_2}$, tách ba bước; Gợi ý 1 của 07.4(d), 07.7(b) viết lại thành hướng tiếp cận, câu cũ chuyển xuống Gợi ý 2; 07.6(b) Bước 1 thành câu dẫn và ba gạch đầu dòng.
- **Kí hiệu.** $\vartheta_i\to\Delta\mu_i$ (viết ngay ở Bước 1), $\mathcal H_{(1)},\mathcal H_{(2)}\to\mathcal H_1,\mathcal H_2$, $\bar n\to\bar B$, $\theta_{\mathrm{abs}}\to\theta_{\mathrm{II}}$.
- **Điểm nhẹ của rà sư phạm.** Tiếng Anh ở lần đầu (ReLU, score function, architecture class, margin violation rate, minimum-norm interpolant, random seed, permuted labels); 07.4(b) thêm (T1) vào đề và Bước 1; 07.4(a) viết lại; 07.6(b) đề nêu tiêu chí (hiệu so với sai số chuẩn), Gợi ý 2 chỉ còn cách tính sai số chuẩn; 07.6 và 07.9 "Kiểm tra lại" bỏ số đo bằng máy; 07.1 "Kiểm tra lại" bỏ câu nhắc lại; 07.3(e) Bước 3 hiển thị phép tính trung gian; 07.5(b) thêm động từ "Chạy", bước cơ sở quy nạp đặt trước; 07.7(c) tách câu định nghĩa hàm kích hoạt ngưỡng; 07.9(d) phát biểu cho mọi hàm liên tục, Bước 2 viết thẳng; "Vẫn vậy" → "Dù vậy"; bỏ in nghiêng "tốt nhất".

Không áp dụng hoặc áp dụng khác đề xuất, có lý do:

1. **07.9(d) dùng $\tilde f$ thay cho $g$** do người rà đề xuất: trong tệp, $g$ đã là một hàm lỗi $\mathcal Z\to[0,1]$ (07.2(b), lớp $\mathcal G$).
2. **Tiêu đề 07.5** giữ nguyên: đề xuất "Xấp xỉ phổ quát và hạ gradient khởi tạo tại gốc" để điều phối viên quyết, và phải đổi §11 của ghi chú, ngoài ngoại lệ phạm vi được giao (chỉ dòng 07.8).
3. **07.1 đổi tên** theo quyết định điều phối viên ($\theta_{\mathrm{II}}$), không dùng $\theta'$ như người rà nghiêng về.

Sau khi sửa: số tiếng và kết quả kiểm tra ghi ở báo cáo bàn giao; bảng số ở §5 cập nhật $3774{,}2$ và $46\,585$.

### 8.1. Sửa theo rà lại sư phạm (`reviews/13-ra-lai-bai-tap-su-pham.md`)

1. 07.8(b): dòng 764 tách câu tại dấu hai chấm, viết "bất đẳng thức ở Bước 2 của (a)"; dòng 766 viết "Bước 2 của (a)".
2. 07.6(b) Bước 3: ba phép tính sai số chuẩn đặt trong `aligned`; đoạn ghép cặp riêng, nêu độ lệch chuẩn của mười hiệu ghép cặp $0{,}0061$ (tính từ `ex07/exp_m400.txt`, `exp_m800.txt`: 0,006091; sai số chuẩn 0,001926) và ghi rõ số này cần dữ liệu từng lần chạy; kết luận thành đoạn riêng. Cụm "Coi hai nhóm như độc lập" giữ ở câu dẫn của khối tính, không cắt, để phân biệt hai cách tính.
3. 07.6(b) Bước 1: dòng "Số hạng Rademacher" thêm chủ ngữ.
