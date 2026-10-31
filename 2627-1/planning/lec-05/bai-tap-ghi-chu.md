# Ghi chú của người viết bài tập — Bài 05 (2026-10-31)

Tệp nội bộ. Người viết bài tập duy nhất (`no-ai-slop` chế độ Edit, tự kiểm theo `eval.md`). Sản phẩm: `materials/lec-05/exercises.md` (12 bài; bản đầu 8 311 tiếng, 44 khối; sau vòng sửa ở mục 8: 9 267 tiếng, 45 khối gồm 12 `exercise`, 21 `hint`, 12 `solution`). Không commit.

## 1. Thứ tự làm việc

1. Đọc `CLAUDE.md` của học phần và workspace; `van-phong.md` (§3a, §7a, §9a, §12 với quy tắc tách nhóm số nguyên từ năm chữ số bằng `\,`, §13–§14); các dòng Bài 05 của `ky-hieu.md`; toàn bộ ghi chú Bài 05 (kể cả Phụ lục A–D); `outline.md` §4, §12 (danh sách số) và §13 (ghi chú cho người viết bài tập); `source-analysis.md` §5, §7; `review-log.md` (QĐ 1–13, mục "Bài tập — bắt đầu"); mẫu `lec-04/exercises.md` và `lec-04/bai-tap-ghi-chu.md`.
2. Đọc đề UML trên PDF (mục 2).
3. Tự giải cả 12 bài; tính lại mọi con số bằng Python trong scratchpad của phiên (mục 5).
4. Sau đó mới mở `MLbookSol.pdf` tr. 26, 33–34, 38–39 để đối chiếu (mục 3).
5. Viết theo sáu giai đoạn (05.1–05.2; 05.3–05.4; 05.5–05.6; 05.7–05.9; 05.10–05.11; 05.12), mỗi giai đoạn khoảng 150–200 dòng, tự kiểm `no-ai-slop` sau mỗi giai đoạn; rồi sửa hiển thị ở 390 px và một vòng đọc lại.

## 2. Số bài UML đã kiểm trên PDF

| Bài học phần | UML | Trang PDF | Nội dung đã đọc |
|---|---|---|---|
| 05.7 | Bài tập 12.1 | 169 (§12.6) | cực tiểu địa phương của hàm lỗi 0–1, nhãn $\pm1$, $\mathcal X=\mathbb R^2$ |
| 05.8 | Bài tập 12.2 | 169 | hồi quy logistic, $\mathcal H=\mathcal X$ là quả cầu bán kính $B$; lồi–Lipschitz–bị chặn và lồi–trơn–bị chặn |
| 05.9 | Bài tập 12.3 | 169 | hàm lỗi bản lề, $\lVert x\rVert\le R$, chứng minh $R$-Lipschitz |
| 05.10 | Bài tập 14.3 (ba ý) | 201 (§14.8) | Perceptron như hạ dưới gradient trên $\max_i(1-y_i\langle w,x_i\rangle)$; ý 3 có phần so với Batch Perceptron §9.1.2 (bỏ) |
| 05.11 | Bài tập 14.4 | 201 | độ dài bước $\eta_t=B/(\rho\sqrt t)$, "analog of Theorem 14.8" (không chiếu) |
| 05.12 | Bài tập 9.2 | 128 (§9.6); phương trình (9.6) ở tr. 124 | $A=\sum_ix_ix_i^\top$ khả nghịch khi và chỉ khi các $x_i$ sinh $\mathbb R^d$ |

Các số khớp `outline.md` §4 và §12 của ghi chú. Đề viết lại bằng lời của học phần; không dịch đoạn nào của UML.

## 3. Đối chiếu với bản lời giải UML (sau khi tự giải)

| Bài UML | Bản lời giải | Chỗ hổng hoặc khác biệt; cách xử lý |
|---|---|---|
| 9.2 (tr. 26) | Qua hạng và SVD (Lemma C.4) | Đúng. Học phần dùng $v^\top Av=\sum_i\langle v,x_i\rangle^2$ (ngắn hơn), thêm hằng số lồi mạnh, trơn và trường hợp không sinh. |
| 12.1 (tr. 33) | $S=\{(e_1,1)\}$, $w=-e_1$ | Đúng; một lỗi dấu vô hại: viết $\langle w',x\rangle=\langle w,x\rangle-\langle w'-w,x\rangle$ (phải là $+$), kết luận vẫn đúng nhờ Cauchy–Schwarz. Học phần đổi sang nhãn $\{0,1\}$, thêm (b) hàm lồi không có cực tiểu địa phương không toàn cục, (c) gradient bằng $0$ hầu khắp nơi. |
| 12.2 (tr. 33) | $g(a)=\log(1+e^a)$, $g''\ge0$; $1$-Lipschitz, $\tfrac14$-trơn qua các Claim của UML | Đúng; câu cuối viết "linear regression" thay cho hồi quy logistic (lỗi đánh máy). Học phần tự chứng minh bước "đạo hàm tăng ⇒ lồi" (giá trị trung bình) và dùng Mệnh đề 05.5(a) thay cho Claim của UML; thêm khoảng giá trị trên $W$. |
| 12.3 (tr. 34) | Xét trường hợp, giả sử thứ tự không mất tổng quát | Đúng; lỗi đánh máy $\lVert x'\rVert$. Học phần cho hai cách (Mệnh đề 05.5(a) với dưới vi phân của Bài tập 05.1; trực tiếp), thêm tính chặt của hằng số và tính không trơn. |
| 14.3 (tr. 39) | Ý 1: "nếu bất đẳng thức ngặt thì giảm được chuẩn của $w^\star$"; ý 3: "thuật toán phải có $f(w^{(t)})<0$ sau $\lVert w^\star\rVert^2R^2$ vòng" | **Hai chỗ hổng.** (1) Chỉ suy ra $f(w^\star)=0$; không chứng minh $f\ge0$ trên quả cầu $\lVert w\rVert\le\lVert w^\star\rVert$, cần cho $\min=0$ (học phần: nếu $f(w)<0$ thì $w/\min_i\tilde y_i\langle w,x_i\rangle\in K$ có chuẩn nhỏ hơn). (2) Khẳng định về $f(w^{(t)})<0$ sai: bảo đảm của hạ dưới gradient là cho điểm lặp trung bình, với $f(\bar w_T)<1$ (không phải $<0$), và cần $T>\lVert w^\star\rVert^2R^2$ ngặt. Nhận xét "không đổi khi đặt $\eta=1$" đúng khi không chiếu; học phần chứng minh bằng quy nạp (05.10(d) Bước 5). Thêm (a): $w^\circ=\operatorname{proj}_K(0)$ tồn tại và duy nhất (Phụ lục A). |
| 14.4 (tr. 39) | Không có lời giải, chỉ dẫn tài liệu | Học phần tự chứng minh với phép chiếu lên quả cầu bán kính $B$: tổng Abel, $\Delta_t\le4B^2$, $\sum t^{-1/2}\le2\sqrt T-1$, cận $3BG/\sqrt T$. Đề UML không có phép chiếu; lập luận này cần $W$ bị chặn (05.11(b)). |

Không chép hay diễn lại sát câu chữ của sách hay bản lời giải.

## 4. Sai khác so với `outline.md` §4

- **05.1.** Ý (b) chứng minh dưới vi phân tại điểm gãy cho $x\ne0$, $\tilde y$ và điểm gãy bất kì, rồi suy ra kết luận của Ví dụ 05.2 (Bước 5), theo ghi chú §13 của dàn ý. Thêm (a) chứng minh tính lồi trực tiếp. Số của (c), (d) đúng dàn ý: $(2,1)$; $0$; $\{\alpha(2,1)\}$; $(0{,}5;-0{,}5)$.
- **05.2.** Gộp (a), (b) của dàn ý; thêm trường hợp điểm so sánh ngoài $W$ ($W=[-1,1]$, $w=1$, $g=-1$, $u=3$: $2>0{,}5$) bên cạnh tập không lồi ($-0{,}2>-1{,}48$). Số (c) khớp: $1{,}6$; $1{,}7799$; thêm vế phải khi bỏ chiếu $1{,}6$ (dấu bằng).
- **05.3.** Ý (a) viết cho $t=2$ dưới dạng tổng kép (trường hợp $t$ bất kì nêu một câu), thay cho chép lại chứng minh Bổ đề 05.12 đã có trong ghi chú. Chín cặp viết thành khối `aligned` ba dòng thay cho bảng bốn cột (tràn ở 390 px). Thêm vào (c) phép so định lượng: vế trái $0$ so với $\mathbb EL_S(w_2)-L_S(u)\approx0{,}4944$. Không nêu lỗ hổng UML tr. 193 (QĐ 1).
- **05.4.** Ý (c) của dàn ý (thừa số $(c+1/c)/2$) trùng Ví dụ 05.8, Bước 4, nên thay bằng hai ý mới cho mục tiêu 3: (b) $\eta$ cố định ($2\epsilon/G^2=0{,}0125$; $\eta=0{,}01$ cần $T=2500$; $\eta=0{,}0125$ không đủ với $T$ nào; tốt nhất $\eta=0{,}00625$, $T=1600$); (c) ước lượng sai $G$ ($\hat G=8$: $T=6400$, $Q=0{,}0625$; $\hat G=2$: $T=400$, $Q=0{,}25>0{,}1$). Thừa số $1{,}25$ chỉ còn trong "Kiểm tra lại". Diễn giải của ý (d) dàn ý nằm trong (b), (c). Hàm vế phải đặt tên $Q(\eta,T)$ (cục bộ; $B$ đã là bán kính).
- **05.5.** Đúng dàn ý. (c) thêm hiệp phương sai $-\sigma^2/3$ và kết luận Mệnh đề 05.20(b) vẫn đúng khi tương quan âm; (d) thêm ngưỡng $m<121\,600$ để so $32\,000+5m$ với $640\,000$.
- **05.6.** Theo ghi chú §13 của dàn ý, thêm ý (e): nhiễu nguyên đối xứng $\Pr(\nu=\pm k)=c/k^3$, $c=1/(2\zeta(3))$; (G1) đúng ($\mathbb E\lvert\nu\rvert=\zeta(2)/\zeta(3)\approx1{,}3684$), $\mathbb Eg^2=\infty$ tại mọi $w$, kể cả trên $W=[-1,1]$; không chiếu thì $\mathbb EF(\bar w_T)=\infty$ với mọi $T\ge2$; có chiếu thì Định lý 05.14 không cho cận nào. (d) thêm $G=\sqrt2$, $\eta G^2/2=0{,}1$ trên $[-1,1]$. Ý (f) là giao thức (không có số, không có notebook), với $N\ge100$ lần chạy (viết $N$, không viết $R$ vì $R$ là cận khoảng cách khởi tạo); với nhiễu của (e), báo cáo thêm trung vị và phân vị. "Mức sàn sai số" chỉ dùng cho mức dao động thật của điểm lặp cuối; ở 05.4 và 05.6(d) viết "số hạng $\eta G^2/2$ của cận".
- **05.7.** Thêm (b) (hàm lồi: cực tiểu địa phương là toàn cục; vi phạm trực tiếp với $\alpha=\tfrac34$: $1>0{,}75$) và (c) (gradient $0$ hầu khắp nơi, điểm dừng). Viết $\langle w,\mathbf e_1\rangle$ thay cho tọa độ $w_1$ (trùng điểm khởi tạo).
- **05.8.** Thêm (d): khoảng giá trị trên $W$: $[0{,}0067;5{,}0067]$ khi $B=5$, $C_x=1$; nối $G=1$ của Ví dụ 05.9.
- **05.9.** Thêm (b) tính chặt của hằng số (số của Ví dụ 05.2: tỉ số $0{,}5/0{,}2236=\sqrt5$) và (c) không $\beta$-trơn.
- **05.10.** $w^\star$ của UML viết $w^\circ$ (vì $w^*$ là nghiệm tối ưu trên $W$ trong `ky-hieu.md`). Dàn ý gợi ý $W$ là quả cầu bán kính $\lVert w^\star\rVert$; bài dùng $W=\mathbb R^p$ (Hệ quả 05.16 cho phép, vì dưới gradient bị chặn bởi $C_x$ trên toàn không gian), để phép cập nhật không cần biết $\lVert w^\circ\rVert$ và để chứng minh tính bất biến theo $\eta$. Thêm (a) sự tồn tại, duy nhất của $w^\circ$, và một phép kiểm tra nhỏ ($m=1$, $T=2$: $0{,}6464\le0{,}7071$).
- **05.11.** Đúng dàn ý; so với $0{,}1$ và "khoảng $0{,}228$" (Nhận xét 05.17 ghi "không quá $0{,}2281$", Phụ lục C ghi $0{,}2280$; giá trị máy $0{,}22801$).
- **05.12.** Thêm tính trơn $\beta=2\lambda_{\max}(A)/m$ (ghi chú dẫn "$\tfrac43$-trơn (Bài tập 05.12)" sau Định nghĩa 05.6) và trường hợp không sinh (không lồi mạnh).

**§12 của ghi chú:** tên và mục tiêu của 12 bài khớp nguyên văn (kiểm bằng script). Các chỗ ghi chú dẫn bài tập (§3 → 05.8; §4 → 05.7, 05.8, 05.9, 05.12; Ví dụ 05.2 → 05.1; câu sau Hệ quả 05.15 → 05.4; Ví dụ 05.14 → 05.5(d); cuối §8 → 05.6; Nhận xét 05.17 → 05.11) đều được bài tương ứng đáp ứng. Không cần sửa ghi chú.

**Bản đồ mục tiêu:** 1 — 05.1, 05.2, 05.8, 05.9, 05.10, 05.11; 2 — 05.3; 3 — 05.4, 05.5, 05.10, 05.11; 4 — 05.5; 5 — 05.3(c), 05.6 (gồm (e) cho (G2)), 05.7.

## 5. Con số và script

Script trong scratchpad của phiên, thư mục `/tmp/claude-1000/-data-tqlong-lectures/4b001abf-4561-4493-868c-a2610e5c7ac9/scratchpad/py/` (ngoài repo).

| Bài | Con số | Script |
|---|---|---|
| 05.1 | $\ell=1$; $0$; $0$ tại ba điểm; $(0{,}5;-0{,}5)$; $\ell(w_0+x)=5<6$; $L_S(1,-1)=2$ | `l05_ex_1to3.py` (kiểm thêm bằng 20 000 điểm ngẫu nhiên: $\alpha\in\{0;0{,}5;1\}$ là dưới gradient, $\alpha\in\{1{,}1;-0{,}1\}$ không) |
| 05.2 | $-0{,}2$; $-1{,}5$; $0{,}02$; $-1{,}48$; $2$; $0{,}5$; $1{,}6$; $0{,}8$; $0{,}0201$; $1{,}7799$; $0{,}2$; $1{,}6$; $0{,}1799$ | `l05_ex_1to3.py` |
| 05.3 | $w^*=(0{,}74733;-0{,}66445)$, $L_S=0{,}061117$; $\psi$: $(0{,}24;0{,}9867)$, $(-0{,}9867;-0{,}4267)$, $(-\tfrac23,\tfrac23)$; chín ô $0$; $1{,}3289$; $0{,}8198$; $1{,}4947$; $0$; $1{,}1469$; $1{,}4947$; $1{,}3289$; $0$; hàng $0{,}7162$; $0{,}8805$; $0{,}9412$; $0{,}8460$; $0{,}4533$; $0{,}5467$; $0{,}6667$; $0{,}5556$; $0$; $0{,}4944$ | `l05_ex_1to3.py` |
| 05.4 | $\eta^*=0{,}00625$; $0{,}08$, $T=2500$; $0{,}1$; $T=1600$; $6400$, $0{,}0015625$, $0{,}0625$; $400$, $0{,}025$, $0{,}25$; $1{,}25$ | `l05_ex_4to6.py` |
| 05.5 | $6400/6400$; $1900/7600$; $775/12\,400$; $494/31\,616$ ($493{,}75$); $424/108\,544$; $400/4\cdot10^6$; $b=150$, $T=440$, $66\,000$; $9{,}5$; $4{,}75$; sáu trung bình; $19/6=3{,}1667$; $-3{,}1667$; $\log_220=4{,}32$; $0{,}03125$; $0{,}0625$; $6400$; $32\,000$; $121\,600$ | `l05_ex_4to6.py` |
| 05.6 | $0{,}02632$; $0{,}01282$; $0{,}002513$ (so $0{,}025$; $0{,}0125$; $0{,}0025$); $\sum_{k<2000}(1-0{,}9^k)^2=1985{,}26$; $\mathbb E\bar w^2=0{,}000496$; $\mathbb EF(\bar w)=0{,}000248$; $v_\infty=0{,}0526$, tỉ số $106$; $G=\sqrt2$, $0{,}1$; $\zeta(3)=1{,}2021$; $c=0{,}41595$; $\zeta(2)/\zeta(3)=1{,}3684$; $v_2=0{,}01$. Mô phỏng 20 000 lần chạy: $\mathbb Ew_{2000}^2\approx0{,}0522$, $\mathbb E\bar w^2\approx0{,}000495$ (chỉ để kiểm, không in) | `l05_ex_4to6.py` |
| 05.7 | $L_S(-\tfrac12,0)=1>0{,}75$ | `l05_ex_7to12.py` |
| 05.8 | $\max f''=0{,}25$; $\ln(1+e^{-5})=0{,}0067$; $\ln(1+e^5)=5{,}0067$; $\ln2=0{,}6931$ | `l05_ex_7to12.py` |
| 05.9 | $\sqrt5=2{,}236$; $\lVert u-w_0\rVert=0{,}2236$; tỉ số $\sqrt5$ | `l05_ex_7to12.py` |
| 05.10 | $10/\sqrt{101}=0{,}9950$; $T=100$ cho $1$; $m=1$: $\eta=70{,}71$, $\bar w_2=(3{,}5355;0)$, $f=0{,}6464\le0{,}7071$; bất biến theo $\eta$ kiểm trên một mẫu 30 điểm | `l05_ex_7to12.py`, `l05_ex_10check.py` |
| 05.11 | $0{,}3$; $\sum_{t\le1600}t^{-1/2}=78{,}552\le79$; $477{,}10/1600=0{,}2982$ | `l05_ex_7to12.py`, `l05_ex_10check.py` |
| 05.12 | $A=\begin{pmatrix}1{,}36&0{,}48\\0{,}48&1{,}64\end{pmatrix}$; $\det=2$; trị riêng $1$, $2$; $\tfrac23$; $\tfrac43$; đẳng thức dây cung kiểm bằng số | `l05_ex_7to12.py` |

Không có số nào chưa kiểm được.

## 6. Thuật ngữ và kí hiệu

- **Tiếng Anh ở lần đầu trong tệp:** hàm điểm số, dưới vi phân, phép chiếu Euclid, điểm lặp trung bình, độ chênh tối ưu, GD, SGD (đoạn mở đầu); hàm lỗi bản lề (05.1); hàm lỗi logistic (05.8).
- **Kí hiệu cục bộ:** $a(w)$ (05.1); $w(k_1)$ (05.3, như $w(k_{1:t-1})$ của ghi chú); $Q(\eta,T)$, $T_\eta$, $\hat G$ (05.4); $X_j$, $e_1,e_2$ (05.5); $\rho$, $v_t$, $v_\infty$, $\zeta$, $c$, $X$, $N$ (05.6); $\mathbf e_1$, $z_\alpha$ (05.7); $f$, $s_w$, $p$ (05.8); $d$ (05.9, hướng); $K$, $w^\circ$, $f$, $w'_t$ (05.10); $q$, $M$, $c$, $\mu$ (05.12; $\mu$ cho trị riêng trong phương trình đặc trưng, $\lambda_{\min}$, $\lambda_{\max}$ theo cách viết chuẩn). Mỗi kí hiệu chỉ sống trong bài của nó.
- Không có "hãy", "Đáp án", "rõ ràng", "dễ thấy", "Mục này", `\text{}`; một dấu gạch dài (trong tiêu đề).

## 7. Kiểm tra đã chạy

- `wc -w`: $8\,311$ (trần $10\,000$).
- Một tiêu đề `#`; 44 khối mở và 44 khối đóng, không lồng (script); không dòng nào có số dấu `$` lẻ; không khoảng trắng cuối dòng.
- Tên và mục tiêu 12 bài so với §12 của ghi chú: khớp (script).
- `sync-local-materials.py` rồi `--check`: OK (10 tệp).
- Chromium (Python Playwright, `http.server` trên cổng 8791 từ thư mục gốc học phần, đã tắt sau khi chạy), `material-viewer.html?doc=materials/lec-05/exercises.md`, 1600×900 và 390×844, mở cả 32 khối `details`: 0 `.katex-error`, 1 300 công thức, 0 lỗi trang hay console, 0 yêu cầu hỏng; chiều rộng tài liệu 375 ≤ 390. Lần đo đầu ở 390 px có 7 khối tràn (05.2(b), 05.3(a), 05.3(b) hai khối gồm bảng chín cặp, 05.4(c), 05.12(b) hai khối); đã ngắt dòng và đổi bảng thành `aligned`; lần đo cuối 0 khối `.katex-display` hay bảng tràn. Đây là kiểm tra lỗi, không thay cho phép đo chiều rộng của điều phối viên.

## 8. Sửa theo rà soát

Căn cứ: `reviews/11-quyet-dinh-bai-tap.md` (bắt buộc), `reviews/9-bai-tap-toan.md` (R2), `reviews/10-bai-tap-su-pham.md` (R4); dòng cũ theo bản đóng băng, dòng mới theo `exercises.md` sau khi sửa. Bản trước khi sửa: `scratchpad/fix05/before.md`. Con số mới: `py/l05_ex_fix1.py`, `py/l05_ex_fix2.py`. Không commit.

**Quyết định của điều phối viên.**

| Mục | Trạng thái | Nội dung, dòng mới |
|---|---|---|
| T1 (05.7 gợi ý; cấu trúc trùng bản lời giải) | đã sửa | Mẫu mới hai quan sát $((1,0),1)$, $((1,1),0)$; cực tiểu địa phương $w=(-1,-1)$, $L_S=\tfrac12$, $\epsilon=\tfrac12$ (cận $-1+\tfrac12$ và $-2+\tfrac{\sqrt2}2$); điểm tốt hơn $(1,-2)$, $L_S=0$ (dòng 690–712). Gợi ý 1 chỉ nói tìm điểm có lân cận phân lớp sai cùng các quan sát; gợi ý 2 cho mẫu và hướng của $w$ (dòng 680–686). (b) Bước 3 dùng $u=(1,3)$, $\alpha=0{,}6$: điểm $(-0{,}2;0{,}6)$ có $L_S=1>0{,}5$. Kiểm tra lại: gradient bản lề $(-0{,}5;0)$. |
| T2 (05.3(b) từng bước) | đã sửa | Ba $\psi(w_2)$ với phép thay số $\tfrac23(0{,}36;1{,}48)$, $\tfrac23(-1{,}48;-0{,}64)$, $\tfrac23(-1,1)$ (dòng 304–308); ô $(1,2)$ tính đủ: $g_2=(0,2)$, $w_2-u\approx(0{,}2527;0{,}6645)$, tích $1{,}3289$ (dòng 310–316); đường chéo giải thích (dòng 318); tổng chín ô $7{,}6139$, $7{,}6139/9\approx0{,}8460$; hàng đầu $(0+1{,}3289+0{,}8198)/3$; tổng ba hàng $2{,}5379$; $1{,}6667/3$. |
| T3 (05.5(a) lặp Ví dụ 05.15) | đã sửa | (a) mới: $\epsilon=0{,}1$, $\sigma^2=3$ (giả định): $T$ và số quan sát $400/400$; $200/600$; $119/1904$; $105/6720$; GD $100/10^6$; điểm đổi chiều $b\approx3$ so với $15$ (dòng 446, 466–481). (b) sửa cho khớp: $T(b)\le1{,}1\,T_{\mathrm{GD}}$ khi và chỉ khi $b\ge10\sigma^2/G_F^2$; $\sigma^2=3$: $b=30$, $T=110$, $3300$; $\sigma^2=15$: $b=150$, $T=110$, $16\,500$ (dòng 448, 483–489). (c), (d) giữ. |
| T4 (kí hiệu trùng) | đã sửa | 05.6: $v_t\to q_t$, $v_\infty\to q_\infty$ ($s$ đã là chỉ số tổng trong (c)), $\rho\to r$ (dòng 533–660). 05.8: $p\to q$ cho $1/(1+e^{-s})$ (dòng 759, 788). |
| 05.10 cận làm tròn (R2) | đã sửa | $0{,}9951$ (dòng 924); kiểm tra lại $1/\sqrt2\approx0{,}7072$ (làm tròn lên, dòng 930). |
| 05.10 $\lVert w^\circ\rVert$ (R2) | đã sửa | Đề (d) hỏi vì sao chạy được mà không biết $\lVert w^\circ\rVert$; Bước 6 mới: độ dài bước không cần $\lVert w^\circ\rVert$; số vòng lặp theo cận vẫn cần, nhưng dừng ở $T$ đầu tiên $\bar w_T$ phân lớp đúng $S$, muộn nhất $\lfloor\lVert w^\circ\rVert^2C_x^2\rfloor+1$ (dòng 928). |
| 05.2(b) (R2) | đã sửa | Cả hai bất đẳng thức của Bổ đề 05.8(b) hỏng: $4>0{,}8$, $4>1{,}44$; $4>0$, $4>1$; Mệnh đề 05.13 chỉ dùng bất đẳng thức thứ hai (dòng 200, 210). |
| 05.8(b) (R2) | đã sửa | Tính không giảm được qua Mệnh đề 05.5(b) với $U=\mathbb R^p$ và $w=-t\tilde yx$ (dòng 784). |
| 05.5(c) (R2) | đã sửa | Dấu bằng từ đẳng thức ở Bước 2 của chứng minh Mệnh đề 05.20 (dòng 495). |
| 05.11 và mục tiêu 3 (R4 #16) | đã sửa, thêm ý | Ý (d) mới: $3BG/\sqrt T\le0{,}1$ cho $T\ge14\,400$, gấp $9$ lần $1600$; độ dài bước hằng cần $T$ trước, $\eta_t$ thì không (dòng 953, 1025–1031). Giữ mục tiêu 3; không cần sửa §12 của ghi chú. |
| Đề bám câu chữ UML (R4 #6) | đã sửa | 05.7(a) (dòng 672), 05.10(b), (c) (dòng 880, 882), 05.12(a) (dòng 1043) viết lại theo khung của học phần. |

**Các điểm nhẹ còn lại của R4.**

| # | Trạng thái | Nội dung, dòng mới |
|---|---|---|
| 5 | đã sửa một phần | 05.2(a) thành biến thể: $w^+\in W$ bất kì với $\lVert w^+-u\rVert\le\lVert w-\eta g-u\rVert$, "không dùng chứng minh trong ghi chú" (dòng 135). 05.2(c) đổi sang bước thứ ba với $i_3=1$, $u=w^*$ (chưa có trong ghi chú): vế trái $0{,}0236$; $\lVert w-u\rVert^2=0{,}00344$, $\lVert w^+-u\rVert^2=0{,}01237$, $\lVert w-\eta g-u\rVert^2=0{,}06566$, $\tfrac\eta2\lVert g\rVert^2=0{,}08579$; vế phải $0{,}0769$; bỏ chiếu $0{,}0236$; bước đưa điểm lặp ra xa $w^*$ (dòng 212–232). 05.3(a) ghi "Không dẫn Bổ đề 05.12" (dòng 246). 05.1(c) giữ: bài 1 của blueprint, dữ liệu khác Ví dụ 05.2 ($y=0$, ba điểm khác). |
| 7 | đã sửa | "kiểm tra giả thiết" thêm vào dòng mức độ của 05.2, 05.3, 05.6, 05.7, 05.11; bỏ "(khó)" ở 05.11. |
| 8 | đã sửa | 05.10 gợi ý 1 chỉ nói $K$ lồi đóng, Định nghĩa 05.7, Phụ lục A, "co $w$ về $K$"; phép chia cụ thể chuyển sang gợi ý 2. |
| 9 | đã sửa | 05.1(b) $\langle cx+r,r\rangle=c\langle x,r\rangle+\lVert r\rVert^2$ (dòng 74); 05.4(b) $0{,}2-0{,}16=0{,}04$ (dòng 405); 05.11(c) $2BG\sqrt T=320$, $BG/2=2$ (dòng 1015); 05.8(a) Bước 3 hai bất đẳng thức trong `aligned` rồi một dòng cộng (dòng 772); 05.5(c) Bước 4 tách ba dòng (dòng 499). |
| 10 | đã sửa | Thiết lập thành danh sách nhãn song song ở 05.2 (dòng 128), 05.3 (dòng 239), 05.6 (dòng 533). |
| 11 | đã sửa | 05.6(f) câu "Báo cáo" tách hai câu (dòng 657); 05.10 Bước 5 tách thành Bước 5 và Bước 6; 05.5(c) chia (c1), (c2) (dòng 452). |
| 12 | đã sửa | Tiếng Anh ở lần đầu: subgradient (dòng 5), batch size, mini-batch (dòng 8), sampling with replacement (05.3), without replacement (05.5(c1)), AM–GM với tên tiếng Việt đầy đủ (dòng 372), error floor (dòng 543), normal distribution (dòng 655), local minimum (dòng 670), stationary point (dòng 729), smooth (dòng 749), Abel summation (dòng 957), normal equations, least squares (dòng 1041), strongly convex (dòng 1045). |
| 13 | đã sửa | Dòng 3 "Định nghĩa, kết quả và ví dụ được dẫn theo …"; 05.7(c) "Hàm lỗi bản lề và hàm lỗi logistic (§3, §4) lồi và có gradient khác $0$ ở đây." (dòng 729); câu về ý 3 của UML chuyển ra dòng "Mục tiêu" của 05.10 (dòng 866). |
| 14 | đã sửa | "phân bố chuẩn (normal distribution)" (dòng 655); kết luận cho (e) và "Đường cong là minh họa, không phải chứng minh, kể cả cho các tham số đã chọn" (dòng 658). |
| 15 | đã sửa | 05.10 Bước 1: với $\eta=1$ là phép cập nhật của Perceptron trên quan sát có lề nhỏ nhất (dòng 914). |
| 16 | đã sửa | Xem 05.11 ở bảng trên. |
| 17 | đã sửa | Không còn $4\cdot10^6$ cho số quan sát (bảng mới dùng $10^6=100\cdot10^4$); $4\cdot10^6=T^2$ ở 05.6(c) giữ theo đề xuất. |

**Thêm khi sửa.** Cận trên làm tròn lên: $\ln(1+e^5)=5{,}006715$ in $5{,}0068$ (đầu trên của khoảng giá trị, dòng 807); $477{,}104$ in $477{,}11$ (05.11(c)). Không bài nào đổi tên; tên và mục tiêu 12 bài vẫn khớp §12 của ghi chú.

**Kiểm tra sau khi sửa.** `wc -w` $9\,267$; một tiêu đề `#`; 45 khối mở, 45 khối đóng, không lồng (thêm gợi ý 2 của 05.7); `probe.py` của điều phối viên in `0` (lần chạy đầu in `1`: dòng $\langle w_2,x_i\rangle-y_i$ của 05.3(c), đã ngắt thêm một dòng); Chromium 1600×900 và 390×844, 33 khối `details` mở: 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, chiều rộng tài liệu 375; một chỗ `\lvertr` do phép thay $\rho\to r$ đã sửa trước khi đo; `sync-local-materials.py` và `--check` OK; `git diff --check` sạch; 0 "hãy", "Đáp án", "rõ ràng", "dễ thấy", "Mục này", `\text{`.

**Vòng sửa cuối (theo `reviews/12-ra-lai-bai-tap-toan.md`, `13-ra-lai-bai-tap-su-pham.md`).** 05.2(c) Bước 3 tính $\lVert w-u\rVert^2\approx0{,}00162+0{,}00182\approx0{,}00344$ từ Bước 1, ghi Ví dụ 05.7 in $0{,}0034$ (dòng 218); 05.5(a) Bước 3: phần vượt $T(b)-100\approx300/b$, còn $19$ ở $b=16$ và $5$ ở $b=64$ (dòng 481); 05.8(b): $L\to G'$, tách thành Bước 3 "hằng số không giảm được" (dòng 786); "(smooth) theo Định nghĩa 05.6" (dòng 749); "tức lấy tổng Abel (Abel summation)" (dòng 959); dòng mục tiêu 05.10 tách câu về nguồn (dòng 868). Bước 6 của 05.10(d) giữ nguyên (điều phối viên xác nhận quyết định 11 về $\eta$ là nhầm). Kiểm tra: `wc -w` $9\,283$; 45/45 khối; `probe.py` in `0`; sync và `--check` OK; `git diff --check` sạch. Không commit.
