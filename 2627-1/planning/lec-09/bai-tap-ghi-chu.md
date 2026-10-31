# Ghi chú của người soạn bài tập Bài 09

Tệp nội bộ, không liên kết từ trang chỉ mục. Người soạn: tác tử soạn bài tập (2026-10-31 → 2026-11-01). Sản phẩm: `2627-1/materials/lec-09/exercises.md` (7 bài gốc, 3 bài UML; 40 khối: 10 `exercise`, 20 `hint`, 10 `solution`; 9 927 tiếng theo `wc -w` ở bản đóng băng, 9 985 sau vòng sửa §8).

## 1. Bài UML: số bài, thời điểm tự giải, bản lời giải

- **Số bài đã kiểm trên PDF.** `understanding-machine-learning-theory-algorithms.pdf` tr. 356, §24.8 có đúng ba bài: 24.1 (MLE của phương sai Gauss bị chệch), 24.2 (MLE có chính quy hóa cho Bernoulli, ba ý), 24.3 (bước M của "soft k-means", bốn ý). "Soft k-means" là tên UML đặt cho EM của hỗn hợp Gauss, §24.4.2 (tr. 352, đã kiểm).
- **Tự giải.** Lời giải 24.1–24.3 lập xong (kể cả cách chia hai trường hợp cho 24.2(c) và trường hợp $\nu_y=0$ của 24.3), số của 24.2 tính bằng `ex99.py`, trước khi mở bản lời giải: 2026-10-31, khoảng 23:47 (+07).
- **Mở bản lời giải.** `MLbookSol.pdf` tr. 61–64 (chương 24 kéo sang tr. 64, không chỉ 61–63 như dàn ý), mở lúc 23:47:58 ngày 2026-10-31, sau khi tự giải. Không chép, không diễn đạt sát; lời giải trong `exercises.md` theo lập luận riêng đã lập trước.
- **Chỗ bản lời giải sai hoặc thiếu.**
  1. 24.1: viết "$(\mathbb E[\hat\sigma])^2=\frac{M-1}M\sigma^2$" (kí hiệu sai: phải là $\mathbb E[\hat\sigma^2]$; $M$ lẫn với $m$); lập luận còn lại đúng và đúng cho mọi phân bố có phương sai hữu hạn.
  2. 24.2(b): viết $\theta$ thay cho $\hat\theta$; $\lvert\mathbb E\hat\theta-\theta^\star\rvert=(1-2\theta^\star)/(m+2)$ thiếu dấu trị tuyệt đối (chỉ đúng khi $\theta^\star\le\tfrac12$).
  3. 24.2(c): chỉ đạt $\tilde O(m^{-1/4})$ (ngưỡng $\sqrt\epsilon$); dùng "$\log$ là 4-Lipschitz trên $[0{,}25;1]$" mà không kiểm $1-\hat\theta\ge0{,}25$. Lời giải của học phần đạt $O(\ln m/\sqrt m)$ đều theo $\theta^\star$ (ngưỡng $2\epsilon_m$, cận $\chi^2$ cho trường hợp lớn).
  4. 24.3: đổi ràng buộc $c_y>0$ của đề thành $c_y\ge0$ mà không nói; không xét $\nu_y=0$ (khi đó bài toán với $c_y>0$ không có nghiệm) hay $\sum\nu_y=0$; viết "$\min_c\sum_{y}D_{RE}(c^\star\Vert c)$" (thừa $\sum_y$); ý cuối chỉ viết "một sự kiện đã biết", không chứng minh.

## 2. Sai khác với `outline.md` §4 (kèm lý do)

Lý do chung: quyết định bài tập Bài 07–08 cấm chép lại chứng minh hoặc phép tính đã có trong ghi chú; ghi chú Bài 09 sau hai vòng biên tập đã làm sẵn nhiều ý của dàn ý (Ví dụ 09.3 Bước 5, Ví dụ 09.5 Bước 2–4 và Kết luận, Ví dụ 09.7 Bước 2, chứng minh Mệnh đề 09.8 và Định lý 09.12, Phụ lục A(iii)). Các ý đó được thay bằng biến thể cùng mục tiêu.

1. **09.1.** (a), (b), (d) theo dàn ý (số khớp: $0{,}02$; $3{,}9120$; $0{,}9780$; $2{,}6591$; $0{,}128$; $2{,}0557$; $0{,}5139$; $1{,}6719$; $\tfrac{27}{12\,800}$; kì vọng $4$). (c) "kiểm tổng $81$ chuỗi bằng $1$ theo Mệnh đề 09.3(c)" lặp lập luận của Ví dụ 09.3 Bước 5; thay bằng $\Pr(x_3=\mathtt C\mid x_1)$: $0{,}40$ và $0{,}69$, cho thấy ngữ cảnh bậc $1$ không làm $x_1$, $x_3$ độc lập. Tổng bằng $1$ vẫn dùng ở (d) Bước 2. Thêm kí hiệu cục bộ $\pi_0$, $\pi$, $Q_n$.
2. **09.2.** (a) theo dàn ý, thêm điều kiện hai cửa sổ rời nhau ($i'-i\ge k+1$). (b) dàn ý ($1-f^k$, MSE $\approx f$) đã có ở Ví dụ 09.5 Bước 2, 4; thay bằng hàm dự đoán dùng $k-1$ cửa sổ, MSE $\approx f^{k-1}$ ($5{,}1\cdot10^{-7}$ với $k=10$, $f=0{,}2$; $0{,}25$ với $k=3$, $f=0{,}5$). (c) dàn ý ($0{,}2$ không ước lượng rủi ro; (T7)) đã có ở Ví dụ 09.5 Bước 4; thay bằng đếm khoảng đệm: bỏ $k$ cửa sổ mỗi phía, còn $3972$ cửa sổ huấn luyện. (d) thêm (T3) không thỏa (lỗi bình phương với đích Gauss không bị chặn) bên cạnh sự phụ thuộc.
3. **09.3.** (a) dàn ý "chứng minh Mệnh đề 09.8(a)–(b) cho $\mathcal X$ hữu hạn" là chép chứng minh của ghi chú; thay bằng chứng minh (b) qua bất đẳng thức Jensen (ghi chú dùng $\ln t\le t-1$). (b), (d) theo dàn ý. (c) chiều ngược của dàn ý ($p_D=(\tfrac12,\tfrac12,0)$, $p_\theta$ đều, $\ln1{,}5$) gần Ví dụ 09.7 Bước 2; thay bằng $\mathrm{KL}(p_\theta\Vert p_D)=\tfrac12\ln2$ cho cùng cặp với chiều thuận $+\infty$.
4. **09.4.** (a) dàn ý "chứng minh Định lý 09.12(a)–(b) cho $\mathcal V$ hữu hạn" là chép; bỏ. Ý (b) của dàn ý (chứng minh trực tiếp bằng $\ln t\le t-1$, không qua đồng nhất thức) thành (a). (c), (d) của dàn ý gộp: (b) số, (c) hai trường hợp về giá. Thêm $q(2)=1$: ELBO $-1{,}7371$, khe $0{,}3133=-\ln\Pr(v=2\mid x)$.
5. **09.5.** Theo dàn ý ($\tfrac38$, $\tfrac7{12}$, $\tilde p=(\tfrac34,\tfrac14)$). (b) nêu rõ giả thiết để điểm cực tiểu ở trong; (c) nêu giả thiết $\mathrm H(\tilde p)<\infty$; (d) chứng minh hai chiều.
6. **09.6.** Phần bắt buộc dùng số đã chạy (mục 3). Theo quyết định Bài 07–08: hai mô hình đánh giá trên cùng mẫu kiểm tra, nên sai số chuẩn tính theo hiệu theo hạt giống ($0{,}00013$ ở $m=50$, so với $0{,}0018$ nếu coi độc lập). Thêm mô hình so sánh $p_{\mathrm{alt}}$ (đường chéo $0{,}46$): phần vượt lý thuyết $\tfrac{199}{200}\cdot0{,}03938\approx0{,}0392$ khớp hiệu đo được $0{,}0392$; chuỗi $40$ kí tự ($18$ cặp giữ nguyên) gần kì vọng dưới $p_{\mathrm{alt}}$ ($17{,}9$) hơn dưới mô hình học được ($23{,}3$). Thêm bán kính Hoeffding theo cách của Ví dụ 09.4 với $c=0{,}087$ (xác suất nhỏ nhất của mười mô hình làm trơn với $m=50$; hợp lệ vì mô hình được học trước khi rút mẫu kiểm tra) và $200$ chuỗi: $\le0{,}2345$, so với độ lệch chuẩn $0{,}0041$. Phần tùy chọn: $200$ chuỗi sinh ra mỗi hạt giống, tỉ lệ giữ nguyên $0{,}597$ ($0{,}586$–$0{,}621$). Không nêu đường dẫn script (ngoài repo).
7. **09.7.** (a) dàn ý (ma trận Hesse) đã có ở Phụ lục A(iii); thay bằng thác triển lồi $\tilde F$ lên $\mathbb R^2$ (Định nghĩa 05.10 và (C) cần hàm xác định trên toàn $\mathbb R^p$; $F$ chỉ xác định khi $\sigma>0$): thay $g(\sigma)=\sigma^2-\ln\sigma$ trên $(-\infty,\tfrac14)$ bằng tiếp tuyến tại $\tfrac14$ ($g'(\tfrac14)=-3{,}5$). (b) (G1) qua Mệnh đề 09.15 với lân cận cho mọi điểm của $\Phi$ (lân cận của Ví dụ 09.11 Bước 4 không chứa $(2,\tfrac12)\in W$), rồi Mệnh đề 05.3(a); đặt $\varphi=0$ khi $\sigma\le0$ cho đủ Định nghĩa 05.10. (c) (G2) theo dàn ý: $\mathbb E\lVert\varphi\rVert^2=(5\mu^2-12\mu+8)+(7\sigma^2+1/\sigma^2-4)$, lớn nhất $12$ tại $(0,1)$, $G=2\sqrt3$. (d) $R=\sqrt{4{,}25}$ đúng định nghĩa Bài 05 (điểm xa nhất $(2,\tfrac12)$); điểm cực tiểu $(1,1/\sqrt2)\in W$; cận $\sqrt{51}/100\le0{,}0715$; đọc thành kì vọng của $\mathrm{KL}(q_{\bar w_T}\Vert p_\theta(\cdot\mid2))$; mô phỏng $0{,}00014$ (dàn ý ghi $0{,}0001$). (e) thêm $\sigma_0=0{,}1$: $G\approx10{,}20$.
8. **09.8.** Thêm (a) dẫn ra MLE như ERM với hàm lỗi log cho mật độ, và (c) $m=1$: $\inf L_s=-\infty$, nối §2 của ghi chú (ý (c) ghi "do học phần thêm"). Không dùng Monte Carlo trong lời giải.
9. **09.9.** $m_1$ thay $k$ (theo ghi chú, `outline.md` §13.2 mục 1). Trường hợp $\theta^\star>2\epsilon_m$: cận $3\epsilon_m$ (dàn ý ghi $4\epsilon_m$), và chứng minh $3\epsilon_m\le B_m$ vì $2\epsilon_m(m+2)\ge2$. Ý (d) của dàn ý (cận đều $\chi^2\approx1{,}9$) chuyển vào "Kiểm tra lại". $\epsilon_{100}=0{,}145614$ (dàn ý ghi $0{,}14559$, có lẽ đã nhân $\tfrac m{m+2}$); $B_m$ khớp dàn ý.
10. **09.10.** Theo điểm mở 7 của dàn ý: thay "bước M của soft k-means" bằng phần trọng số của bước M trong Hệ quả 09.13 (nêu UML §24.4.2 trong dòng mục tiêu). Thêm trường hợp có $\nu_y=0$.
11. **Tên bài** khớp §11 của ghi chú. **Mục tiêu được đo:** 1 (09.1); 2 (09.3, 09.8, 09.9, 09.10); 3 (09.2, 09.5, 09.6); 4 (09.4, 09.10); 5 (09.7). Năm loại bài: chứng minh, tính toán, khái niệm, kiểm tra giả thiết, thực nghiệm tùy chọn.

## 3. Thí nghiệm (Bài tập 09.6)

Script của ghi chú (không sửa): `../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec09_bigram.py`, chạy lúc 2026-10-31 23:45 (1,1 giây); đầu ra scratchpad `ex09/exp_all.txt`, khớp `outline.md` §13.1 đến bốn chữ số. Số theo hạt giống lấy bằng `ex09/bigram_seeds.py`, `ex09/ex96b.py` (nạp hàm `gen`, `fit`, `nll_tok` của script); phần tùy chọn bằng `ex09/optional96.py` (bộ sinh `default_rng(1000+seed)` cho bước sinh chuỗi).

| $m$ | Làm trơn (độ lệch chuẩn) | Thật (độ lệch chuẩn) | Hiệu trung bình | Độ lệch chuẩn hiệu | SE hiệu | SE coi độc lập | Tương quan |
|---|---|---|---|---|---|---|---|
| 1 | 1,1223 (0,0113) | 1,0907 (0,0038) | 0,03157 | 0,01295 | 0,00410 | 0,00376 | −0,31 |
| 5 | 1,0971 (0,0055) | 1,0904 (0,0035) | 0,00671 | 0,00354 | 0,00112 | 0,00207 | 0,78 |
| 50 | 1,0913 (0,0041) | 1,0906 (0,0040) | 0,00071 | 0,00040 | 0,00013 | 0,00182 | 0,995 |
| 500 | 1,0882 (0,0028) | 1,0882 (0,0028) | 0,00008 | 0,00005 | 0,00002 | 0,00127 | 1,000 |

Ở $m=1$, tương quan âm nên sai số chuẩn của hiệu lớn hơn sai số chuẩn coi độc lập; bài tập chỉ so hai cách ở $m=50$. Tỉ số (từ số làm tròn trong đề): $7{,}7$; $6{,}1$; $5{,}6$; $5{,}1$.

- Mô hình học được (hạt giống 0, $m=50$): đường chéo $0{,}5945$; $0{,}6047$; $0{,}5918$; $0{,}5998$; phân bố dừng gần đều, tỉ lệ giữ nguyên dừng $0{,}5977$. Mô phỏng $200\,000$ chuỗi $40$ kí tự (`default_rng(12345)`): số cặp giữ nguyên trung bình $23{,}30$, độ lệch chuẩn $3{,}057$, $\Pr(\le18)=0{,}0594$; dưới xích thật $23{,}40$, $3{,}059$, $0{,}0558$.
- $p_{\mathrm{alt}}$ (đường chéo $0{,}46$; hàng $\mathtt A$ $(0{,}46;\,0{,}27;\,0{,}135;\,0{,}135)$, các cột có tổng $1$): $\mathrm{KL}$ hàng $0{,}039380$; phần vượt $0{,}039183$; trên mười mẫu kiểm tra: lỗi kiểm tra $1{,}1297$ (độ lệch chuẩn $0{,}0028$), hiệu với mô hình thật $0{,}03918$ (độ lệch chuẩn $0{,}00125$).
- Xác suất nhỏ nhất của mười mô hình làm trơn với $m=50$: $0{,}08717$; $\ln(1/0{,}087)=2{,}441847$; $\sqrt{\ln40/400}=0{,}0960323$; bán kính $0{,}234496\to0{,}2345$ (làm tròn lên). Với cận thô $c=1/9954$ (mọi hàng có tối đa $50\cdot199$ chuyển), bán kính là $0{,}884$; bài tập dùng $c=0{,}087$.
- Phần tùy chọn: tỉ lệ giữ nguyên trên $200$ chuỗi sinh ra mỗi hạt giống: $0{,}5992$; $0{,}5979$; $0{,}5963$; $0{,}5863$; $0{,}5913$; $0{,}5915$; $0{,}5967$; $0{,}5965$; $0{,}6213$; $0{,}5958$; trung bình $0{,}5973$.

## 4. Các con số khác và script (scratchpad `ex09/`)

| Bài | Con số | Script |
|---|---|---|
| 09.1 | $0{,}02=\tfrac1{50}$; $\ln50=3{,}91202$; $0{,}97801$; $2{,}65915$; $\tfrac{16}{125}$; $2{,}05573$; $0{,}51393$; $1{,}67185$; $\Pr(x_3=\mathtt C\mid x_1)=\tfrac25,\tfrac9{25},\tfrac{69}{100}$; tổng $81$ chuỗi $=1$; $\tfrac{27}{12\,800}=0{,}0021094$ | `nums.py` (phân số đúng) |
| 09.2 | $0{,}2^9=5{,}12\cdot10^{-7}$; $0{,}5^2$; $1-0{,}2^{10}$; $4990-998-20=3972$ | `nums.py` |
| 09.3 | $\mathrm H=1{,}039721$; $\ln3=1{,}098612$; $\mathrm{KL}=0{,}058892$; ngược $0{,}056633$; $\tfrac12\ln2=0{,}346574$; $3\ln2=2{,}079442$; $7\ln2=4{,}852030$ | `nums.py` |
| 09.4 | $p(x)=0{,}240791$; $\ln=-1{,}423824$; hậu nghiệm $0{,}731059$; ELBO $-1{,}543939$ (khe $0{,}120115$), $-1{,}512003$ (khe $0{,}088179$ $=\mathrm{KL}$), $q(2)=1$: $-1{,}737086$ (khe $0{,}313262$) | `nums.py` |
| 09.5 | $\tfrac38$; $\tfrac7{12}$; $c=\tfrac13$; $\tilde p=(\tfrac34,\tfrac14)$ | `nums.py` |
| 09.7 | $F^*=2{,}265512$; $\max\mathbb E\lVert\varphi\rVert^2=12$ (lưới và Monte Carlo $2\cdot10^6$ mẫu tại ba điểm); $R=2{,}061553$; $\eta=0{,}0059512$; cận $0{,}0714143\to0{,}0715$; mô phỏng $20$ hạt giống ($T=10^4$, chiếu lên $W$, $\bar w_T=\frac1T\sum_{t\le T}w_t$): trung bình $0{,}000135$, độ lệch chuẩn $0{,}000102$, lớn nhất $0{,}000354$; $\sigma_0=0{,}25$: $G=4{,}5208$; $\sigma_0=0{,}1$: $G^2=104{,}07$, $G=10{,}2015$ | `sgd_elbo.py` |
| 09.8 | $3{,}2$ | `nums.py` |
| 09.9 | $\epsilon_m$: $0{,}145614\to0{,}1457$; $0{,}0439447\to0{,}04395$; $0{,}0136810\to0{,}01369$; $B_m$: $1{,}278877\to1{,}279$; $0{,}481468\to0{,}4815$; $0{,}180916\to0{,}1810$; phân vị $95\%$ lớn nhất của KL thật (nhị thức chính xác, lưới $0{,}001$): $0{,}02098$; $0{,}002007$; $0{,}000196$; cận đều $\chi^2$: $2{,}18$; $1{,}94$; $1{,}87$; kiểm ngẫu nhiên $2\cdot10^5$ bộ $(m,\theta^\star,\hat\theta)$: $\mathrm{KL}/\text{cận}\le0{,}29$ | `ex99.py` |
| 09.10 | $-6\ln2=-4{,}158883$; $4\ln\tfrac13=-4{,}394449$; hiệu $0{,}235566=4\cdot0{,}058892$ | `nums.py` |

Quy tắc làm tròn: cận trên làm tròn lên, số đo làm tròn gần nhất.

## 5. Kiểm tra đã chạy

`sync-local-materials.py` và `--check` (OK, 18 tệp); không có khoảng trắng cuối dòng; 40 khối mở, 40 khối đóng, không lồng; `wc -w` 9 927; không có "Đáp án", "hãy", "rõ ràng", "dễ thấy", "hiển nhiên", không có `\text{}`; tệp kết thúc bằng đúng một ký tự xuống dòng. Viewer qua HTTP (`reloadserver` cổng 8793, đã tắt), mọi `details` mở (30), ở 390×844 và 1600×900: 1 287 công thức KaTeX, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức hay bảng tràn (28 công thức tràn ở lần đo đầu đã tách bằng `aligned`), độ rộng trang 375 px ở 390. Console chỉ có cảnh báo CSP do `reloadserver` chèn script nội tuyến (như Bài 07–08). Ảnh `ex09/ex09_390.png`, `ex09/shot0.png`, `ex09/shot2.png`.

## 6. Điểm không chắc

1. **09.2(b)** dùng xấp xỉ gán độc lập với xác suất $f$ cho hoán vị ngẫu nhiên (đề nói rõ) và bỏ qua cửa sổ gần cuối chuỗi; "với xác suất $1$" dựa trên tính liên tục của $N(0,1)$. Chưa chạy thí nghiệm cho hàm dự đoán dùng $k-1$ cửa sổ.
2. **09.7(a)** thác triển tiếp tuyến: người rà toán nên kiểm $\tilde F$ khả vi trên $\mathbb R^2$ và việc Định lý 05.14 chỉ dùng $\tilde F$ trên $W$; câu "đặt $\varphi=0$ khi $\sigma\le0$" là một chi tiết kĩ thuật để khớp Định nghĩa 05.10.
3. **09.6(b)(i)** dùng $c=0{,}087$ lấy từ các mô hình đã học (phụ thuộc mẫu huấn luyện, không phụ thuộc mẫu kiểm tra); người rà nên xác nhận cách đọc này khớp Ví dụ 09.4 ("mô hình cố định, không phụ thuộc mẫu kiểm tra").
4. **09.9(c)** là lời giải của học phần, khác bản lời giải UML; hằng số $3\epsilon_m$ và $2\epsilon_m$ ở hai trường hợp cần người rà toán kiểm lại.
5. **Độ dài**: 9 927 tiếng, sát trần 10 000; nếu người rà yêu cầu thêm nội dung, cần cắt ở chỗ khác (ứng viên: 09.6(c), 09.2(d) Bước 1, 09.8(c)).

## 8. Vòng sửa theo `reviews/11-quyet-dinh-bai-tap.md` (2026-11-01)

Căn cứ: `reviews/9-bai-tap-toan.md` (0/0/0/4), `reviews/10-bai-tap-su-pham.md` (0/0/3/21), quyết định của điều phối viên (7 mục và các điểm nhẹ). Bản trước khi sửa: scratchpad `ex09/exercises_before_fix.md`. Số mới tính bằng `ex09/t1t2.py`.

**Đã áp dụng.**

1. Toán 1: 09.6 bảng tỉ số $6{,}1\to6{,}0$, $5{,}6\to5{,}7$; câu ví dụ "$0{,}00040/3{,}162\approx0{,}000125$ và $0{,}00071/0{,}000125\approx5{,}7$"; cắt câu "giảm khoảng chín lần" (giá trị đúng $8{,}75$).
2. Toán 2: "Trên mười mẫu kiểm tra của dòng $m=50$".
3. Toán 3 (gộp N7): 09.6(a) Bước 5 viết lại; thêm so sánh với mô hình học được: hiệu trung bình $0{,}0392-0{,}00071\approx0{,}0385$ (tính lại theo hạt giống: $0{,}038469$, độ lệch chuẩn $0{,}001350$, nhỏ nhất $0{,}0364$).
4. Toán 4: 09.8 dòng mục tiêu "Ý (a), (c) và số ở (b) do học phần thêm".
5. T1: 09.4(b) đề thêm yêu cầu tách cận; lời giải thêm **Bước 5: tái tạo và KL** (Bước 5 cũ thành Bước 6): tái tạo $0{,}1\ln\rho_0(1{,}5)+0{,}9\ln\rho_0(0{,}5)=-0{,}204394-0{,}939545=-1{,}143939$; KL tới tiên nghiệm $0{,}1\ln0{,}2+0{,}9\ln1{,}8=-0{,}160944+0{,}529008=0{,}368064$; hiệu $-1{,}512003$ trùng ELBO.
6. T2: thêm 09.4(d) (đề, mỗi gợi ý một câu, lời giải ba bước): $\operatorname{ELBO}(\phi)=(1-\phi)\ln\frac{p_\theta(x,1)}{1-\phi}+\phi\ln\frac{p_\theta(x,2)}{\phi}$; đạo hàm $\ln\frac{p_\theta(x,2)}\phi-\ln\frac{p_\theta(x,1)}{1-\phi}$ bằng $1$ tại $\phi=\tfrac12$ (sai phân số: $0{,}9999999998$); ước lượng theo đường đi bằng $-2$ hoặc $2$, kì vọng $0$ (Monte Carlo $10^6$ mẫu: $-0{,}0008$; ước lượng gradient log cho $0{,}9988$, không đưa vào bài); (i) của Mệnh đề 09.15 không thỏa. Dòng mức độ thêm "kiểm tra giả thiết", mục tiêu "4 và 5". Ngoại lệ phạm vi: ghi chú §11 sửa đúng hai dòng (09.4 "mục tiêu 4, 5"; 09.10 "Tùy chọn: bước M cho trọng số hỗn hợp; UML Bài tập 24.3"); `forward_refs.py` 0.
7. T3: "kết quả thí nghiệm" thay "bằng chứng thí nghiệm" (dòng mục tiêu 09.6 và (b) Bước 4; câu ở (b) Bước 2 bị cắt khi rút gọn); "Tổng của cấp số nhân"; "xác suất kết thúc"; "Điểm dừng" ở 09.5 thay bằng phép tính đạo hàm (N10).
8. Nhẹ: N1 (KL, ELBO vào danh sách viết tắt; "kí tự (token)", "mô hình bigram (bigram model)", "độ bối rối (perplexity)", "phân bố hình học (geometric distribution)", "hỗn hợp (mixture)", "hạt giống ngẫu nhiên (random seed)", "làm trơn cộng một (add-one smoothing)", "*khe* (gap) $\ln p_\theta(x)-\operatorname{ELBO}$" ở đề 09.4(b)); N2 $S^2\to V_s$; N3 $N\to\nu_+$, $\varphi_0\to\rho_0$; N4 (09.8(a) Bước 2 tự khai triển; (b) Bước 1 dẫn (a), Bước 2); N5 câu đầu "Tính bằng máy …", cắt câu thứ hai; N6, N8, N13, N14, N17 cắt; N9 (09.7(c) Bước 3 thêm hai phép cộng); N10 (09.5(a) Bước 2 lí do cực tiểu, Bước 3 đạo hàm); N11, N12 (gợi ý tăng dần ở 09.7(a), 09.6(b)(i)); N15; N16 (dấu hai chấm ở 09.1, 09.4, 09.6; "$x_1$ ảnh hưởng tới $x_3$ qua phân bố của $x_2$"; "dùng nhiều cửa sổ hơn hàm của Ví dụ 09.5"); N18 (câu $p_{\mathrm{alt}}$ tách đôi; cột "Hiệu" rút thành "(làm trơn trừ thật, cùng hạt giống)" và tách câu ngoặc); N19; N20; N21 (ghi chú §11).

**Không áp dụng (lý do).**

- Toán 4, phần tùy chọn "Ý (c) cụ thể hóa yêu cầu của UML" ở 09.9: hết chữ (người rà ghi "nếu còn chỗ").
- N5, phép kiểm tay thay câu thứ hai: hết chữ; "Kiểm tra lại" của 09.9 giữ câu tính bằng máy.
- N18, câu đầu của đề 09.6 (giao thức trong ngoặc): giữ nguyên, khoảng 35 tiếng.

**Cắt thêm để giữ trần 10 000** (sau T1, T2 tệp lên 10 223 tiếng): 09.1(b) Bước 1 câu cuối; 09.2(d) Bước 1 rút, Bước 4 gộp; 09.3(b) Bước 4 câu cuối, (c) Bước 3 bỏ vế "dù …"; 09.4(c) Bước 1 câu cuối rút; 09.5(a) Bước 4 câu đầu; 09.6 đề câu mô phỏng rút, (a) Bước 4 bỏ vế "$5{,}9\%$" và "có đường chéo khoảng $0{,}6$", (b) Bước 1–2 rút, (c) Bước 1, 3 rút; 09.7 đề (b) rút, (a) Bước 3, (e) Bước 1–2 rút; 09.8(b) Bước 3, (c) rút; 09.9(a) bỏ "so với $0{,}7$"; 09.10(a) bỏ diễn giải $\nu_v$; đoạn mở bỏ "tức đối của log độ hợp lý". Không cắt bước tính, số liệu hay lập luận.

**Kiểm tra sau sửa.** `sync` và `--check` OK (19 tệp); 0 khoảng trắng cuối dòng (bài tập và ghi chú); 40 khối mở, 40 khối đóng, không lồng; 9 985 tiếng; `forward_refs.py` ghi chú Bài 09: 0; tệp kết thúc bằng một ký tự xuống dòng. Viewer qua HTTP (cổng 8794, đã tắt), mọi `details` mở, ở 390×844 và 1600×900: 1 316 công thức, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức hay bảng tràn; chỉ cảnh báo CSP của `reloadserver`. Ảnh ở scratchpad `ex09/`, không ở gốc repo.

### 8.1. Sửa theo `reviews/13-ra-lai-bai-tap-su-pham.md` (2026-11-01)

Áp dụng M1–M8, không sửa gì khác. Bản trước khi sửa: scratchpad `ex09/exercises_before_fix2.md`.

1. M1 (dạng rút gọn): 09.4(d) Bước 1 "Đạo hàm của $-(1-\phi)\ln(1-\phi)-\phi\ln\phi$ là $\ln\frac{1-\phi}\phi$, nên" (kiểm: $\ln(1-\phi)+1-\ln\phi-1$).
2. M2: 09.6(a) Bước 5 bỏ độ lệch chuẩn $0{,}0013$ (không có trong đề); thay bằng cận theo bất đẳng thức tam giác cho độ lệch chuẩn: hiệu ($p_{\mathrm{alt}}$ trừ làm trơn) bằng ($p_{\mathrm{alt}}$ trừ thật) trừ (làm trơn trừ thật), nên độ lệch chuẩn không quá $0{,}0012+0{,}00040=0{,}0016$ (giá trị thật $0{,}00135$); $0{,}0385/0{,}0016\approx24$.
3. M3: cắt vế "$5{,}9\%$" khỏi đề 09.6.
4. M4: 09.1(b) Bước 1 thêm "Hai độ bối rối ở (a), $2{,}6591$ và $1{,}6719$, đều nhỏ hơn $3$."
5. M5: 09.6(c) Bước 1 "nên dự đoán tỉ lệ giữ nguyên gần $0{,}6$"; Bước 3 thêm "khớp dự đoán".
6. M6: "nên nó lỏng với xích Markov này".
7. M7: dòng mục tiêu 09.4 "tách cận thành số hạng tái tạo và KL"; đề (b) "rồi tính số hạng tái tạo, $\mathrm{KL}$ tới tiên nghiệm, và kiểm …".
8. M8: 09.1(c) Bước 2 "Kí tự $x_1$ …". Phần 09.7(b) của M8 không áp dụng (hết chữ, theo chỉ thị của điều phối viên).
9. Cắt "(xấp xỉ của một hoán vị ngẫu nhiên khi số cửa sổ lớn)" ở đề 09.2(b) (điều phối viên cho phép) để giữ trần; đề nay giả sử gán độc lập, và $f^{k-1}$ đúng chính xác dưới giả sử này.

**Kiểm tra sau sửa.** `sync` và `--check` OK (19 tệp); 0 khoảng trắng cuối dòng; 40/40 khối; 9 998 tiếng; tệp kết thúc bằng một ký tự xuống dòng. Viewer qua HTTP (cổng 8795, đã tắt), mọi `details` mở, 390×844 và 1600×900: 1 318 công thức, 0 `.katex-error`, 0 lỗi trang, 0 tràn.
