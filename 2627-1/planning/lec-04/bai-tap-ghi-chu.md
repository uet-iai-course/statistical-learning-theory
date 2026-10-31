# Ghi chú của người viết bài tập — Bài 04 (2026-10-31)

Tệp nội bộ. Người viết bài tập duy nhất (`no-ai-slop` chế độ Edit, tự kiểm theo `eval.md`). Sản phẩm: `materials/lec-04/exercises.md` (13 bài, 9 999 tiếng theo `wc -w`). Không commit.

## 1. Thứ tự làm việc

1. Đọc `CLAUDE.md` của học phần và workspace, `van-phong.md` (§3a, §7a, §9a, §10–§14), `thuat-ngu.md` §8, `ky-hieu.md` (các dòng Bài 04), toàn bộ ghi chú Bài 04 (kể cả Phụ lục A–E), `outline.md` §1–§2, §4, §12–§13, `review-log.md` mục "Bài tập — bắt đầu", `reviews/0-quyet-dinh.md` §D, `source-analysis.md` §7, mẫu `lec-03/exercises.md`, `lec-03/bai-tap-ghi-chu.md`, `_templates/exercises.md`, bài thực nghiệm 02.5 (mẫu cho 04.6). Đối chiếu các khối được dẫn của Bài 01–03: Ví dụ 01.1, 01.2, 01.5; Định nghĩa 02.13, Hệ quả 02.10, Định lý 02.14, Hệ quả 02.16, Ví dụ 02.8, §6 Bài 02 (độ lệch $0{,}18$ trên $S_\eta$); Định lý 03.15, Hệ quả 03.16, Định lý 03.17, Nhận xét 03.14; Bài tập 02.4, 02.6, 02.11, 03.2, 03.9.
2. Đọc đề UML trên PDF: tr. 66 (§5.5, Bài tập 5.2), tr. 97–98 (§7.8, Bài tập 7.2, 7.3, 7.4, 7.5 gồm năm ý), tr. 154–155 (§11.5, Bài tập 11.1, 11.2). Số bài khớp `source-analysis.md` §7 và `outline.md` §4.
3. Tự giải cả 13 bài; tính lại mọi con số bằng Python trong scratchpad của phiên (`ex04/nums.py`, `n4.py`, `n5.py`, `n6.py`, `n7.py`; ngoài repo), kể cả duyệt vét cạn số khối nhãn $1$ cho hợp $n$ khoảng ($n\le3$) và mô phỏng ước lượng để lại một quan sát cho thuật toán chẵn lẻ.
4. Sau đó mới mở `MLbookSol.pdf` tr. 10–11 (Ch. 5), 20–22 (Ch. 7), 31–32 (Ch. 11) để đối chiếu (mục 3).
5. Viết theo năm giai đoạn (04.1–04.2; 04.3–04.4; 04.5–04.6; 04.7–04.8; 04.9–04.13), tự kiểm `no-ai-slop` sau mỗi giai đoạn, rồi rút gọn từ khoảng $11\,300$ tiếng xuống $9\,999$ (bỏ ý (c) mở rộng của 04.8 và ý (c) của 04.12, gộp câu, rút các dòng mục tiêu) và sửa hiển thị ở 390 px.

## 2. Lời giải và con số then chốt (đã tính lại)

| Bài | Ý chính | Con số |
|---|---|---|
| 04.1 | $\operatorname{opt}_S(A(S))\le\epsilon_{\mathrm{opt}}$ rồi Mệnh đề 04.3(a); $L^*=\min/\inf_{\mathcal H}L_D$ cho Hệ quả 02.16(b), 03.16(b); hiệu theo rủi ro kì vọng phụ thuộc nghiệm ERM làm mốc, có thể âm, cần $D$ | $\operatorname{opt}_{S_\eta}(h_t)=\tfrac16,0,0,\tfrac16,0,\tfrac16$; cận $0{,}04+0{,}36+\tfrac16\approx0{,}5667$ so với $0{,}14$; $h_4$ so với $h_2,h_3,h_5$: $0$; $0{,}10$; $0{,}04$; $h_3$ so với $h_2$: $-0{,}10$ |
| 04.2 | dạng lấy trung bình theo $X$; số hạng chéo $(\bar f-f^*)(f^*-Y)$ không cần độc lập, $(\hat f-\bar f)(\bar f-f^*)$ cần $X\perp S$, $(\hat f-\bar f)(f^*-Y)$ cần $(X,Y)\perp S$; rủi ro Bayes $\mathbb E\sigma^2(X)$ (ghi chú dẫn bài này sau Mệnh đề 04.6) | $\gamma=1;0{,}8;0{,}5;0$: $1{,}25$; $1{,}20$; $1{,}3125$; $2{,}00$; $\gamma^*=0{,}8$; nhãn trong mẫu: trừ $2\gamma\sigma^2/m$: $0{,}75$; $0{,}80$; $1{,}0625$; $2{,}00$, nhỏ nhất tại $\gamma=1$ (đạo hàm $-2(1-\gamma)(\mu^2+\sigma^2/m)\le0$) |
| 04.3 | $\ln(1/q_k)=2\ln k+0{,}4977$; $g(k)=k\ln2-2\ln k-\ln(\pi^2/6)$ tăng trên $[3,\infty)$, $g(6)>0$; $q_{k_0}=0$: $\delta'=0$ ngoài miền bán kính, mọi số hạng phạt đúng với xác suất $1$ cho mọi $D$ phải $\ge1$ | bảng $k\le10$ (đã in); $2^{-k}$ nặng hơn tại $k=1$ và $k\ge6$; $\mathrm{pen}_k$, $m=1000$: $2^{-k}$: $0{,}0504$; $0{,}0568$; $0{,}0729$; $0{,}0937$; $0{,}1253$ — $6/(\pi^2k^2)$: $0{,}0494$; $0{,}0590$; $0{,}0737$; $0{,}0887$; $0{,}1096$ |
| 04.4 | bảng $k=5..9$ ($a_k$, $b_k$, $\mathrm{pen}_k$); Thuật toán 04.12 duyệt cả mười lớp ($\mathrm{pen}_{10}=0{,}2871<v=0{,}3650$) | tổng $0{,}3901$…$0{,}4321$; $q=1/10$: $0{,}3799$, $0{,}3642$, $0{,}3762$; $2^{-k}$: $0{,}3778$, $0{,}3637$, $0{,}3771$; $m=10^5$: $\mathrm{pen}$ $0{,}0489$…$0{,}1013$, tổng nhỏ nhất $0{,}2409$ ($k=3$), $0{,}2425$ ($k=4$), hiệu $0{,}0015$; $L_S(\hat h_4)=0{,}166$: $0{,}2385\to\hat k=4$; (d) $0{,}04681$, ngưỡng $0{,}05319$ (≥54 nhãn $0$; xác suất ngược lại $1{,}1\cdot10^{-40}$), vế phải $0{,}2936$, rủi ro $0{,}8$; mọi bán kính hợp lệ của $\mathcal H_2$ $\ge0{,}8$ |
| 04.5 | (a) $g_{11}=\mathbb 1_{F_+(V)}$: $L_V=0$, $L_D=0{,}8$, vượt mức $\ge0{,}6$; (b) danh sách $\mathcal G(S)$ có $\le K^J$ phần tử, cần phép giữ nguyên để $L_V(g^{(j)})$ không tăng và để mô hình trung gian thuộc $\mathcal G(S)$; quy trình tham lam không phải ERM trên $\mathcal G(S)$ nên cận so với mô hình trên đường đi | $K=11$: $0{,}1103$; $\ln(4\cdot10^6)=15{,}2018$, $2r=0{,}1744$; mẫu mới $m'_v=1000$: $\sqrt{\ln20/2000}=0{,}0387$ |
| 04.6 | chỉ giao thức và danh sách kiểm; không có số | — |
| 04.7 | $\mathcal R_2\subseteq\mathcal R_5$ cần miền đặc trưng bị chặn ($\mathcal X=I_1\times\cdots\times I_5$); $d=4$ (phép chiếu, Phụ lục C), $d=10$ | $\rho$: $0{,}5157/0{,}7341$; $0{,}1843/0{,}2689$; $0{,}0643/0{,}0953$; ngưỡng $2\Delta\rho$: $0{,}4369$; $0{,}1693$; $0{,}0619$; SRM $q=\tfrac12$: $0{,}1858$, $0{,}2699$, ngưỡng $L_S$ $0{,}0841$ |
| 04.8 | dương và không giảm ⇒ tổng vô hạn; dãy toàn $0$ thỏa đề UML nhưng không thỏa (T6) | — |
| 04.9 | $q(h)=q_{n(h)}/\lvert\mathcal H_{n(h)}\rvert$, tổng $\le\sum q_n$ (không phải $=$); số hạng phạt từng giả thuyết bằng $\mathrm{rad}_{\mathcal H_n}(m,\delta q_n)$; (c) $q(h)=q_{n(h)}2^{-j(h)}$ | ví dụ lồng nhau: $\sum2^{-n}/n=\ln2\approx0{,}693$; $n=3$: $7\ln2+\ln20=7{,}848$, $0{,}0626$ |
| 04.10 | Kraft ⇒ $\lvert\mathcal H_B\rvert\le2^B$, tồn tại $h^*_B$ và $h_S$ (rút về $\mathcal H_L$ hữu hạn); bán kính Hoeffding tại $\delta2^{-\lvert h\rvert}$ cho $\lvert h\rvert\ln2$, không vượt $\lvert h\rvert$; cận đúng đồng thời cho mọi $B$ | $B=100$, $m=10^4$: $0{,}1440$; ERM trên $\mathcal H_B$ với $B$ cố định: $0{,}1208$ |
| 04.11 | số khối nhãn $1$ $\le n$ ⇔ thực hiện được; $d(\mathcal H_n)=2n$; (M) bằng đầu mút hữu tỉ $u_k\uparrow u$, $v_k\downarrow v$; Hệ quả 04.15 với $q_n=6/(\pi^2n^2)$; thử thách: Định lý 04.16(a) + các tập rời nhau $C_k$, $\lvert C_k\rvert=d_k+1$, ghép $f_k$ | duyệt vét cạn: $n=1,2,3$ tách trọn $2n$ điểm, không tách trọn $2n+1$ |
| 04.12 | $A(S^{-i})=P(S)\oplus Y_i$, sai khi và chỉ khi $P(S)=1$; $L_{\mathrm{loo}}=P(S)$; không chệch, phương sai $\tfrac14$ thay cho $\tfrac1{4m}$ | mô phỏng $m=5,6,20$, 2000 lần: sai số luôn $\tfrac12$ |
| 04.13 | cách 1: $\lvert\bigcup\mathcal H_i\rvert<2^{k+1}$; cách 2 với $j$ cố định trước mẫu: phần huấn luyện chỉ cần $\delta/2$ trên riêng $\mathcal H_j$; bước chọn $\delta/2$ với $K=k$ | cách 1: $0{,}0476$; $0{,}1214$; $0{,}3735$; cách 2, $j=1$: $0{,}1174$; $0{,}1304$; $0{,}1419$ (thành phần $0{,}0356$ và $0{,}0818$; $0{,}0948$; $0{,}1063$); $j=k$: $0{,}1349$; $0{,}2305$; $0{,}5238$; điểm đổi chiều $k=119$; bản đồng thời mọi $j$ ($\ln(2^{j+2}k/\delta)$): $0{,}1247$; $0{,}1440$; $0{,}1610$; $k=1$: $0{,}1018$ so với $0{,}0318$ |

## 3. Đối chiếu với bản lời giải UML (sau khi tự giải)

| Bài UML | Bản lời giải | Khác biệt và cách xử lý |
|---|---|---|
| 5.2 | Chỉ định tính: lớp 5 chiều chứa lớp 2 chiều, sai số xấp xỉ nhỏ hơn, sai số ước lượng lớn hơn | Bao hàm $\mathcal H_2\subseteq\mathcal H_5$ không đúng nguyên văn với hình chữ nhật có cạnh bị chặn trên $\mathbb R^5$; học phần đặt $\mathcal X=I_1\times\cdots\times I_5$ bị chặn. Thêm phần định lượng (bán kính, ngưỡng $a_2-a_5$, SRM) theo dàn ý. |
| 7.2 | Đúng cho trọng số dương; không xét trường hợp mọi trọng số bằng $0$ (dãy toàn $0$ thỏa đúng nguyên văn hai điều kiện của đề UML) | Ý (b) xử lý trường hợp toàn $0$ qua điều kiện $q_k>0$ của (T6) và Bài tập 04.3(d). |
| 7.3 | Viết $\sum_{h\in\mathcal H}w(h)=\sum_n\sum_{h\in\mathcal H_n}w(h)=1$: đếm lặp khi các lớp chồng nhau, và dấu $=$ sai | Học phần nhóm theo $n(h)$, được $\le$, kèm ví dụ tổng $\ln2<1$. Ý (*) của bản lời giải dùng $2^{-n}2^{-k}$ cho $h_{n,k}$, cũng không dùng $n(h)$ (đếm lặp); học phần dùng $q_{n(h)}2^{-j(h)}$. |
| 7.4 | Dòng đầu viết $\sup_h\lvert L_D(h)-L_S(h)\rvert\le\sqrt{(\lvert h\rvert+\ln(2/\delta))/(2m)}$, với $\lvert h\rvert$ nằm trong cận của $\sup$; không nêu sự tồn tại của $h_S$, $h^*_B$; không nói rõ cần ngôn ngữ không tiền tố | Học phần viết cận cho từng $h$, nêu chỗ dùng bất đẳng thức Kraft, chứng minh $\lvert\mathcal H_B\rvert\le2^B$ và sự tồn tại; chỉ ra $\lvert h\rvert\ln2\le\lvert h\rvert$. Đáp số $2\sqrt{(B+\ln(2/\delta))/(2m)}$ khớp. |
| 7.5 | (a)(b) chỉ dẫn "xem Định lý 7.2, 7.3"; (c) đúng; (d) dùng $\mathcal X=\mathbb R$ thay cho $[0,1]$, chiều VC $2n$ nêu vắn tắt, "không học được PAC nhưng học được không đều" không lý giải; (e) "lớp mọi hàm $[0,1]\to\{0,1\}$" không xét tính đo được | Học phần làm trên $[0,1]$, chứng minh $d=2n$ cả hai chiều, kiểm (M) và giả thiết của Hệ quả 04.15. Ý thử thách dùng lớp $\mathcal M_{\mathcal X}$ các hàm đo được (σ-đại số chứa mọi tập một điểm), để hàm ghép $f$ thuộc lớp; phát biểu độc lập, dùng Định lý 04.16(a) làm công cụ (QĐ dàn ý 10). |
| 11.1 | Đúng; không giải thích vì sao kiểm tra chéo hỏng | Thêm ý (b): mỗi số hạng không chệch, nhưng các số hạng bằng nhau nên phương sai $\tfrac14$, không tập trung. |
| 11.2 | Giả sử lớp lồng nhau, $\lvert\mathcal H_k\rvert=2^k$; trộn $\log_2$ và $\ln$ ("$k+1+\log(1/\delta)$", "$j+\log(4/\delta)$"); dòng Hoeffding cho từng $r$ ghi $\log(4/\delta)$ nhưng cần $\log(4k/\delta)$ (mất $k$); phần huấn luyện dùng $\mathcal H_j$ cố định, không chia cho $k$; không bàn chiều ngược lại | Học phần không giả sử lồng nhau ($\lvert\bigcup\rvert<2^{k+1}$), dùng $\ln$ thống nhất, giữ $\ln(4k/\delta)$ ở bước chọn; phần huấn luyện cho $j$ cố định trước mẫu như bản lời giải (đúng, vì $j$ là đại lượng tất định); thêm chiều ngược lại ($j=k$) và bản đồng thời mọi $j$. |

Không chép hay diễn lại sát câu chữ của sách hay bản lời giải; bối cảnh UML 5.2 viết lại (biến cố tim mạch, năm chỉ số).

## 4. Thuật ngữ và kí hiệu

- **Tiếng Anh ở lần đầu trong tệp:** rủi ro tham chiếu, sai số tối ưu thực nghiệm, số hạng phạt, mẫu xác thực, sai số xấp xỉ, sai số ước lượng, độ chệch, phương sai, bất đẳng thức oracle, học không đều, ERM, SRM, PAC, chiều VC (đoạn mở đầu); ước lượng co (shrinkage estimator), tập kiểm tra (test set), ngôn ngữ mô tả (description language), độ dài mô tả tối thiểu (minimum description length, MDL), tính chẵn lẻ (parity), để lại một quan sát (leave-one-out) tại bài dùng.
- **Đề nghị thêm vào `thuat-ngu.md` §8:** "ngôn ngữ mô tả" (description language); "độ dài mô tả tối thiểu (minimum description length, MDL)" (ghi chú §12 đã dùng cụm này, bảng chưa có); "tính chẵn lẻ" (parity). Các thuật ngữ khác đã có trong bảng.
- **Thuật ngữ chốt đã theo:** "độ chệch"; $\delta$ là "xác suất thất bại"; "chia xác suất thất bại"; "sai số tối ưu thực nghiệm"; "học không đều"; "bất đẳng thức oracle"; "lỗi kiểm tra kì vọng"; "nhãn kiểm tra"; "Lời giải"; không có "hãy" ngoài đề, không có "Đáp án", không có `\text{}`.
- **Kí hiệu cục bộ:** $\gamma$ (04.2); $a_k$, $b_k$ (04.4, như Phụ lục C); $g_{11}$, $F_+(V)$, $g^{(j)}$, $J$, $\mathcal G(S)$, $V'$, $m'_v$ (04.5; $\mathcal G(S)$ theo nghĩa "lớp phụ thuộc mẫu" của `ky-hieu.md`); $\mathcal R_2$, $\mathcal R_5$, $I_j$, $\rho^{(d)}$, $a_2$, $a_5$ (04.7); $q(h)$, $n(h)$, $N_n$, $j(h)$ (04.8–04.9; trọng số trên giả thuyết viết $q(h)$, không viết $w$, theo `ky-hieu.md`); $\mathrm d$ (ngôn ngữ mô tả, in đứng để khác chiều VC $d$), $\Phi$, $P(h)$, $\mathcal H_B$, $h_S$, $h^*_B$ (04.10); $C_k$, $f_k$ (04.11); $P(S)$, $\oplus$, $S^{-i}$, $L_{\mathrm{loo}}$ (04.12); $\alpha$ (04.13). $P(h)$ ở 04.10 và $P(S)$ ở 04.12 nằm ở hai bài riêng.

## 5. Sai khác so với `outline.md` §4 và §10 của ghi chú

- **04.1** đúng dàn ý; (c) thêm phép so $h_3$ với $h_2$ trên chính $S_\eta$ ($-0{,}10$) để thấy dấu âm mà không cần mẫu của Nhận xét 04.4.
- **04.2** thêm vào (a) phần rủi ro Bayes $\mathbb E\sigma^2(X)$ và điều kiện dấu bằng, vì đoạn sau Mệnh đề 04.6 của ghi chú dẫn "(Bài tập 04.2)" cho khẳng định này. (c) thêm giá trị $\gamma$ làm lỗi trên nhãn trong mẫu nhỏ nhất ($\gamma=1$).
- **04.3(b)** dàn ý ghi "$k=6$"; bảng cho thấy $2^{-k}$ cũng nặng hơn tại $k=1$ ($0{,}6931>0{,}4977$). Lời giải nêu cả $k=1$ và mọi $k\ge6$. (c) thêm năm giá trị cho $6/(\pi^2k^2)$ (dàn ý không ghi số).
- **04.4(c)** đổi giá trị giả định: dàn ý dùng $L_S(\hat h_4)=0{,}165$, nhỏ hơn $L_S(\hat h_5)=0{,}166$, trái với tính không tăng của các lớp lồng nhau. Bài dùng $0{,}166$; tổng $0{,}2385$ (thay cho $0{,}2375$), vẫn chọn $\hat k=4$. Hiệu tại $m=10^5$ in $0{,}0015$ (giá trị chưa làm tròn $0{,}00152$). (a) thêm câu hỏi về các lớp được Thuật toán 04.12 duyệt.
- **04.5(b)** thêm hai giả thiết cần cho lập luận: có phép giữ nguyên trong mỗi vòng, và cận so với các mô hình trên đường đi (quy trình tham lam không phải ERM trên danh sách $K^J$ mô hình). Con số $0{,}1744$ khớp dàn ý. (a) thêm $g_1\equiv1$ để có $\min_jL_D(g_j)\le0{,}2$; cận $K=11$ là $0{,}1103$.
- **04.7** thêm giả thiết miền đặc trưng bị chặn để có $\mathcal R_2\subseteq\mathcal R_5$.
- **04.8** thêm ý (b) (trường hợp toàn $0$) theo dàn ý; không có ý thêm.
- **04.11** ý thử thách dùng lớp mọi hàm phân lớp *đo được* trên miền vô hạn có σ-đại số chứa mọi tập một điểm. **Đề nghị sửa một câu ở cuối §7 của ghi chú** (người viết không sửa): "Lớp mọi hàm trên một miền vô hạn được xét ở ý thử thách của Bài tập 04.11." → "Lớp mọi hàm phân lớp đo được trên một miền vô hạn được xét ở ý thử thách của Bài tập 04.11."
- **04.12** đúng dàn ý (không có ý so với mẫu xác thực mới, bỏ khi rút gọn).
- **04.13** (điểm mở 7 của dàn ý, người viết tính lại) **số khác dàn ý:** với lớp so sánh $\mathcal H_j$ cố định trước mẫu, phần huấn luyện không cần chia $\delta/2$ cho $k$ lớp, nên cận của cách 2 là $0{,}1174$; $0{,}1304$; $0{,}1419$ (trùng số của `source-analysis.md` §7 và cách làm của bản lời giải), không phải $0{,}1247$; $0{,}1440$; $0{,}1610$. Số của dàn ý được giữ ở Bước 5 như bản đúng đồng thời cho mọi $j$. Số của cách 1 khớp dàn ý ($0{,}0476$; $0{,}1214$; $0{,}3735$). Kết luận định tính không đổi: cách 1 tốt hơn khi $k$ nhỏ (đến $k=118$ với $j=1$) hoặc khi lớp tốt nhất là lớp lớn nhất; cách 2 tốt hơn khi $k$ lớn và lớp tốt nhất nhỏ.

**§10 của ghi chú:** tên và mục tiêu của 13 bài trong `exercises.md` khớp nguyên văn với §10; không cần sửa.

**Bản đồ mục tiêu:** 1 — 04.1, 04.7; 2 — 04.2, 04.6; 3 — 04.3, 04.4, 04.7, 04.8, 04.9, 04.10, 04.13; 4 — 04.11; 5 — 04.5, 04.6, 04.12, 04.13.

## 6. Kiểm tra đã chạy

- `wc -w materials/lec-04/exercises.md`: 9 999.
- `sync-local-materials.py` rồi `--check`: OK (8 tệp).
- `git diff --check`: sạch; tệp mới không có khoảng trắng cuối dòng hay tab. `grep`: 0 "hãy", 0 "Đáp án", 0 `\text`, 1 dấu gạch dài (trong tiêu đề, như Bài 03).
- Playwright (Chromium, `../.venv/bin/python`), máy chủ của repo trên cổng 8766 (cwd của tiến trình đã kiểm: thư mục gốc học phần), `material-viewer.html?doc=materials/lec-04/exercises.md`, 1600×900 và 390×844, mở cả 41 khối `details`: 0 `.katex-error`, 1308 công thức, 0 lỗi trang hay console, 0 yêu cầu hỏng, 0 phần tử vượt khung `.markdown-body` hay có `scrollWidth>clientWidth` (bỏ qua `svg` của dấu căn KaTeX); chiều rộng tài liệu 375 ≤ 390; 0 dòng `innerText` bắt đầu bằng `|`, `:::` hoặc chứa `$$`. Lần đo đầu ở 390 px có 21 công thức/bảng tràn; đã ngắt dòng, bỏ cột (bảng 04.4(a), 04.7(b), 04.13), chuyển hai phép tính sang văn xuôi. Đã xem ảnh chụp đầu trang (1600) và các vùng lời giải 04.4, 04.7 (390).

## 7. Vòng sửa

Theo `reviews/11-quyet-dinh-bai-tap.md` (căn cứ `9-bai-tap-toan.md`, `10-bai-tap-su-pham.md`; dòng dẫn theo `lec04-ex-frozen.md`). Diff: `scratchpad/lec04-ex-round1.diff` (bài tập), `scratchpad/lec04-note-exround.diff` (ghi chú, so với `HEAD`). Không commit.

**Trạng thái từng mục.**

| Mục | Trạng thái | Nội dung |
|---|---|---|
| T1 | đã sửa | 04.4(a) mới: họ kéo dài $25$ lớp ($15$ đặc trưng dựng sẵn, $d_k=k+1$, $L_S(\hat h_k)=0{,}155$ khi $k\ge10$); Thuật toán 04.12 duyệt lớp $1$–$18$, dừng ở lớp $19$, gọi bộ giải $18$ lần; một ô mới $\mathrm{pen}_{19}$; "Kiểm tra lại" kiểm điều kiện dừng không bỏ sót. Bảng $k=5..9$ lặp Ví dụ 04.9 đã bỏ. |
| T2 | đã sửa | 04.1(c): sáu hiệu $L_{D_\eta}(\tilde h)-L_{D_\eta}(\hat h)$ cho $\tilde h=h_4,h_5$ và ba mốc $h_2,h_3,h_5$; bỏ yêu cầu "ba lý do". |
| T3 | đã sửa | 04.2(d): lớp hàm hằng, $L^*=\sigma^2$, sai số xấp xỉ $0$, độ chệch $-0{,}2$ tại $\gamma=0{,}8$. |
| T4 | đã sửa | 04.3(e): $q_k=1/k$; bước hỏng là Bước 3 (tổng $7{,}4855$, cận $0{,}3743$); trong Ví dụ 04.8 chỉ $k\le3$ có bán kính dưới $\tfrac12$; xác suất thất bại $0{,}0058$; vì sao không đủ. Mục tiêu của 04.3 thành "3, 5" (đã sửa §10). |
| T5 | đã sửa | 04.13: $k_{\max}$ cho số lớp, chỉ số $k$; 04.9: $k(h)$, $q_k$, $\mathcal H_k$ thay $n(h)$, $q_n$, $\mathcal H_n$; 04.10: $B_0$, $\mathcal H_{B_0}$ thay $L$, $\mathcal H_L$. |
| T6 | đã sửa | 04.4(b) bốn bước (mỗi trọng số một ô đầy đủ $k=3$ và một khối `aligned`, các lớp còn lại, kết luận); đề 04.5(b) thành câu dẫn và danh sách nhãn song song; số phép sửa mỗi vòng đổi thành $K_0$, danh sách $K=K_0^J$. |
| T7 | đã sửa | 04.3(d): giả thiết hàm lỗi 0–1 trong đề; lời giải tách bốn bước (bước hỏng, điều kiện, phân bố, kết luận) và nêu phạm vi với hàm lỗi tổng quát. |
| T8 | đã sửa | Tiêu đề 04.11 "Hợp nhiều khoảng: học được không đều, không học được PAC; UML Bài tập 7.5, ý 3–5"; câu đầu của đề nói ý 1–2 không lấy (Định lý 04.16(a)), (a)–(c) là ý 4, (d) gộp ý 3 và 5 cho lớp hàm đo được. |
| T9 | đã sửa | 04.6: quy tắc 1 đạt rủi ro thực nghiệm nhỏ nhất tại bậc $15$, khi bằng nhau ghi quy tắc chọn; lý do đúng là (T3) của Định nghĩa 04.8, Định lý 04.11, Hệ quả 04.17; bỏ dẫn Bài tập 04.4(d). |
| B làm tròn | đã sửa | $0{,}5399$, $0{,}1683$ (04.7), $0{,}0319$ (04.13). |
| B đổi tên | đã sửa | 04.3 "… số hạng phạt của từng lớp"; 04.8 "Trọng số không giảm có tổng hữu hạn bằng $0$"; 04.12 "Thất bại của kiểm tra chéo để lại một quan sát" (§10 sửa cùng). |
| B 04.7, 04.13 | đã sửa | 04.7(b): tại $m=10^3$ cả hai cận lớn hơn $1$ ($2\rho=1{,}03$; $1{,}47$); 04.13: đề nói $\lvert\mathcal H_k\rvert=2^k$ là giả thiết học phần thêm. |
| B 04.8 gợi ý | đã sửa | Hai gợi ý tăng dần; (b) tách ba bước. |
| B nhẹ khác (B1) | đã sửa | 04.4(d) nghiệm ERM không duy nhất; 04.3(d) điều kiện $\Pr(B_{k_0})\le\delta q_{k_0}$; 04.2(a) Jensen cho khả tích; 04.4 "Kiểm tra lại" mới; 04.7 $I_j$ độ dài dương; 04.10 danh sách đếm được; 04.12 gợi ý 2 rút gọn; 04.2(c) kết luận không lấy chủ ngữ trừu tượng. |
| B nhẹ khác (B2) | đã sửa | 04.1(a) thêm biến thể bộ giải đúng với xác suất $1-\delta_2$ (cận $1-\delta-\delta_2$); đoạn mở đầu rút gọn thành câu dẫn và danh sách; câu dài ở 04.5(c), 04.6 tách; 04.6 hai mức nhiễu, danh sách song song, "số liệu báo cáo", Kiểm tra lại viết lại; 04.4(d) đề thành danh sách năm ý, nêu giá trị nhị thức chính xác, "cận trên tin cậy của Định lý 04.11(a)"; 04.3(b)(c) "số hạng $\ln(1/q_k)$", "họ đếm được các lớp hữu hạn", "theo đúng chiều của bảng"; 04.2(b) đề tách; 04.2(c) Bước 3 dạng `aligned`; 04.7 thống nhất "dạng chiều VC", định nghĩa $\hat h_{(2)}$, $\hat h_{(5)}$, $\hat h$, một ô đầy đủ cho $\mathrm{pen}_1$; 04.9(b) dẫn đúng công thức 04.3(c); 04.12 "(a) Độ lệch"; 04.13 Bước 1 thành danh sách, phương trình điểm đổi chiều ($k_{\max}=118$: $0{,}13128<0{,}13129$; $119$: $0{,}13181>0{,}13133$); 04.5(c) $V'$ cỡ $m'_v$ nêu trước khi dùng; 04.5(a) dẫn Ví dụ 04.10 cho hai rủi ro; 04.11(a) "Đảo lại", lý do khoảng không chứa điểm nhãn $0$; 04.11(c) thêm câu: $M(\epsilon,\delta,h)$ không bị chặn trên $\mathcal H$ (mục tiêu 4). |
| D | đã sửa | Ghi chú: câu cuối §7 (dòng 910) và bốn dòng §10 (04.3, 04.8, 04.11, 04.12). |

**Con số mới hoặc đổi** (tính lại trong `scratchpad/ex04/r1.py` và các lệnh kèm):

- 04.1(c): $h_5$ so với $h_2,h_3,h_5$: $-0{,}04$; $0{,}06$; $0$.
- 04.2(d): sai số xấp xỉ $0$; độ chệch $-0{,}2$.
- 04.3(e): $\sum_{k\le1000}1/k=7{,}4855$; $\delta\sum q_k=0{,}3743$; $e^5/40=3{,}71$; bán kính $\sqrt{\ln(40k)/20}$ tại $k=1..4$: $0{,}4295$; $0{,}4681$; $0{,}4893$; $0{,}5037$; xác suất thất bại $1-(1-2^{-9})^3=0{,}005848\approx0{,}0058$.
- 04.4(a): $v=0{,}36504$; $\mathrm{pen}_{18}=0{,}3599$ ($a=151{,}22$, $b=10{,}660$); $\mathrm{pen}_{19}=0{,}3676$ ($d=20$, $\ln2718{,}28=7{,}9078$, $a=158{,}16$, $b=10{,}769$, tổng $168{,}92$, $0{,}13514$); $0{,}155+0{,}2871=0{,}4421$; $0{,}155+0{,}3676=0{,}5226$.
- 04.4(b): ô $k=3$: $a_3=38{,}069$; $q=1/10$: $44{,}753$, $\mathrm{pen}_3=0{,}1892$; $q=2^{-k}$: $b_3=6{,}461$, $44{,}530$, $\mathrm{pen}_3=0{,}1887$; tổng $k=1$: $0{,}4473$, $0{,}4428$; $k\ge5$: $\ge0{,}3875$, $\ge0{,}3896$; $\mathrm{pen}_2,\mathrm{pen}_4$: $0{,}1699$, $0{,}2062$ / $0{,}1678$, $0{,}2071$.
- 04.4(d): $\Pr(\mathrm{Bin}(1000;0{,}2)\le53)=1{,}12\cdot10^{-40}$.
- 04.7: $4\ln(2e\cdot10^4/4)=38{,}069$; $+5{,}075$; $\times8\cdot10^{-4}=0{,}03452$; $\mathrm{pen}_1=0{,}1858$; $2\rho$ tại $m=10^3$: $1{,}031$; $1{,}468$; $0{,}5399$; $0{,}1683$.
- 04.13: $0{,}0319$; điểm đổi chiều như bảng trên.

**Kiểm tra đã chạy.**

- `wc -w`: bài tập $9\,981$; thân ghi chú (trước "## Phụ lục") $12\,000$ (trước vòng này $11\,999$; các tên bài dài hơn được bù bằng cách rút tên 04.11 và câu §7, xem diff).
- `forward_refs.py` cho ghi chú: 0. Tên và mục tiêu của 13 bài khớp §10 (kiểm bằng script).
- `sync-local-materials.py` và `--check`: OK (8 tệp). `git diff --check` sạch; tệp bài tập không có khoảng trắng cuối dòng. 0 `\text`, 0 "hãy", 0 "Đáp án".
- Playwright, cổng 8766, 1600×900 và 390×844, mở cả 40 khối `details`: 0 `.katex-error`, 0 lỗi trang hay console, 0 yêu cầu hỏng, 0 phần tử tràn `.markdown-body`, 0 dòng `|`, `:::`, `$$` thô; chiều rộng tài liệu 375 ≤ 390 (lần đo đầu có hai khối `aligned` của 04.4(b) tràn 16 px, đã bỏ nhãn dòng).
- Lỗi phát hiện khi sửa: phép đổi $n\to k$ tự động ở 04.9 làm hỏng `aligned` thành `aligked` một chỗ; đã sửa và kiểm lại bằng `grep`.

## 8. Vòng sửa cuối

Theo `reviews/12-ra-lai-bai-tap-toan.md` và `reviews/13-ra-lai-bai-tap-su-pham.md` (dòng theo `lec04-ex-round1-frozen.md`). Diff: `scratchpad/lec04-ex-round2.diff`. Không commit.

| Mục | Trạng thái | Nội dung |
|---|---|---|
| N1 (toán, trung bình) | đã sửa | 04.11(c) Bước 2: $M(\epsilon,\delta,h)$ là cỡ mẫu đủ, việc nó không bị chặn chưa loại trừ cỡ mẫu chung; lý do đúng là (b), $\mathcal H$ không học được PAC (Định lý 03.17(a)). |
| N2 | đã sửa | 04.11(c) Bước 1: dãy hữu tỉ viết $u^{(t)}$, $v^{(t)}$. |
| N3 | đã sửa | 04.2(d): "với các số của (b)" trong đề; độ chệch $-0{,}2\mu$, bằng $-0{,}2$ khi $\mu=1$; $0{,}8\mu\ne\mu$ khi $\mu\ne0$. |
| N4 | đã sửa | 04.1(a): "thay giả thiết $\epsilon_{\mathrm{opt}}$-ERM bằng …", biến cố đo được. |
| Sư phạm, trung bình 1 | đã sửa | 04.4(c) Bước 1 khôi phục bảng ba cột ($k=1..5$, $10$; tổng tại $k=3$ in đậm), câu cho $k=6..9$. |
| Sư phạm, trung bình 2 | đã sửa | 04.3(e) thêm ý: với $q_k=1$, $k_{\max}$ nhỏ nhất để xác suất thất bại vượt $\delta$; lời giải Bước 5: $k_{\max}>\ln0{,}95/\ln(1-2^{-9})\approx26{,}24$, $k_{\max}=26$: $0{,}0496$; $27$: $0{,}0514$; đáp số $27$. |
| Sư phạm, nhẹ | đã sửa | 04.4(a) "chỉ số giả định", ô $\mathrm{pen}_{18}$ ($a=151{,}22$, $b=10{,}660$, $161{,}88$); 04.4(b) Bước 3 "tổng nhỏ nhất đạt tại $k=5$", Bước 4 lý do là phép so; đề 04.11 đưa câu về nguồn xuống cuối, viết trung tính; tên 04.11 "… học được không đều nhưng không học được PAC …" (§10 sửa cùng); câu cuối §7 của ghi chú "Ý thử thách của Bài tập 04.11 xét mọi hàm phân lớp đo được trên miền vô hạn." (bù một tiếng); 04.1(c) bỏ danh từ hóa; 04.2(d) $\mu=1$; 04.6 câu 43 tiếng tách hai câu. |

**Con số mới:** $\ln0{,}95/\ln(1-2^{-9})=26{,}2365$; $1-(1-2^{-9})^{26}=0{,}04956$; $1-(1-2^{-9})^{27}=0{,}05142$ (khớp số điều phối viên đã kiểm). Không số nào khác đổi.

**Kiểm tra đã chạy.** `wc -w` bài tập $9\,988$ (bù bằng rút câu ở 04.1, 04.2, 04.5, 04.10, 04.12, 04.13, 04.4(d), 04.11; không bỏ phép toán nào); thân ghi chú $12\,000$; `forward_refs.py` 0; tên và mục tiêu khớp §10. `sync-local-materials.py` và `--check`: OK. `git diff --check` sạch. Quét LaTeX sau các phép thay bằng script: không dòng nào có số dấu `$` lẻ, `\begin{aligned}`/`\end{aligned}` 44/44, 0 `\text{`, 0 `aligked`. Playwright cổng 8766, 1600×900 và 390×844, mở 40 khối `details`: 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 tràn `.markdown-body`, 0 dòng `|`/`:::`/`$$` thô; chiều rộng tài liệu 375 ≤ 390.
- Hồi quy T8 (sau vòng 2): khôi phục ở cuối thiết lập 04.11 câu "Ý 1–2 của UML Bài tập 7.5 là Định lý 04.16(a) nên không dùng; (a)–(c) là ý 4; (d) gộp ý 3 và 5 cho hàm phân lớp đo được."; bù bằng bỏ vế "chỉ $\tfrac16$ tính được từ mẫu" ở 04.1(b) Bước 4; `wc -w` 9 990; sync và `--check` OK.
