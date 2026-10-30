# Ghi chú của người viết bài tập — Bài 03 (2026-10-31)

Tệp nội bộ. Người viết bài tập duy nhất (`no-ai-slop` chế độ Edit, tự kiểm theo `eval.md`). Sản phẩm: `materials/lec-03/exercises.md` (12 bài, 9 873 tiếng theo `wc -w`). Không commit.

## 1. Thứ tự làm việc

1. Đọc `CLAUDE.md` của học phần và workspace, `course-plan.md` §4, toàn bộ ghi chú Bài 03, `outline.md` §4 cùng đoạn "Trạng thái cuối của ghi chú", `reviews/0-quyet-dinh.md` mục D, `reviews/5-mach.md` (mục nhẹ cuối về mục tiêu 3–5), `source-analysis.md` §7, mẫu `lec-02/exercises.md`, `_templates/exercises.md`, ba báo cáo rà bài tập Bài 02 (9, 10, 11), `van-phong.md` (§3a, §7a, §9a, §14), `thuat-ngu.md` §6–7, `ky-hieu.md`, blueprint "Lecture 3".
2. Đọc đề UML trên PDF: tr. 78–80 (§6.8, Bài tập 6.2, 6.4, 6.5, 6.6, 6.10), tr. 66 (Bài tập 5.3, được 6.10 dẫn), tr. 128–129 (§9.6, Bài tập 9.6). Số bài khớp `source-analysis.md` §7.
3. Tự giải cả 12 bài; tính lại mọi con số và duyệt vét cạn các khẳng định tổ hợp bằng Python trong scratchpad (`ex03_nums.py`, `ex03_nums2.py`, `ex03_brute.py`, `ex03_brute2.py`).
4. Sau đó mới mở `MLbookSol.pdf` tr. 11–17 (Ch. 6) và tr. 28 (Bài tập 9.6) để đối chiếu (mục 3).

## 2. Lời giải và con số then chốt (đã tính lại)

| Bài | Ý chính | Con số, phép kiểm |
|---|---|---|
| 03.1 | $\mathcal H_6$: $\Pi(m)=\min\{m+1,6\}$ (bộ có điểm lặp); hàm ngưỡng hai phía $\Pi(m)=2m$, $d=2$ | duyệt vét cạn $\mathcal H_6$ với $m\le7$; hai phía với $m\le7$ (bộ có lặp với $m\le5$): $2,4,6,8,\ldots$; tổng Sauer $d=2$: $2,4,7,11,16$; $m=10$: $20$, $56$, $1024$ |
| 03.2 | khoảng mở $d=2$; hợp hai khoảng $d=4$; hai lời giải thiếu một phần | duyệt lưới bước $\tfrac12$: $\{1,2,3,4\}$ đủ $16$; $\{1,\ldots,5\}$ có $31$, chỉ thiếu $(1,0,1,0,1)$; $31=\sum_{j\le4}\binom5j$ |
| 03.3 | ma trận hàng $(x_i^\top,1)$ khả nghịch; $\mathcal H^p_{\mathrm{hom}}$ không tách trọn tập chứa gốc | $p=3$, $y=(0,1,0,1)$: $b=-1$, $w=(2,0,2)$; $p=2$, điểm $(1,1),(2,1),(1,3)$, $y=(1,0,1)$: $w=(-2,0)$, $b=3$, giá trị $1,-1,1$ |
| 03.4 | cỡ mẫu $\epsilon=0{,}05$; hằng số $16=4\cdot4$; lập luận bỏ mẫu bóng; rời rạc hóa $q=3$ | trực tiếp: $589\,118$, $1\,999\,657$ (vế trái $0{,}0024999964$ / $0{,}0025000003$ tại $m$, $m-1$ với $d=3$); dạng đóng $944\,960{,}28\to944\,961$, $3\,165\,708{,}02\to3\,165\,709$; tỉ số $3{,}394$ (dạng đóng $3{,}350$); $4{,}43$, $4{,}47$; ngoặc $46{,}025$, $156{,}223$; $m/d$: $196\,373$, $181\,787$; $2\ln4=2{,}773$, $8\ln4=11{,}09$; ngây thơ $\sqrt{(693{,}147+3{,}689)/2000}=0{,}5903$; $193\ln2+\ln20=136{,}773$, $27\,354{,}6\to27\,355$; $132\,992/27\,355=4{,}862=16\cdot41{,}560/136{,}773$; $32\cdot41{,}560/0{,}01=132\,991{,}2$ |
| 03.5 | $\theta=\pi(1+\sum_j(1-y_j)2^j)$; $\mathcal H_\Sigma$ có ba hàm; lớp một hàm chọn sau khi xem mẫu ($d=0$) | dựng $\sin$ kiểm bằng số hữu tỉ chính xác cho mọi cách gán nhãn, $k\le10$; $y=(1,0,1)\Rightarrow\theta=5\pi$; $y=(0,1,1)\Rightarrow3\pi$; $\sin(5\pi/8)=0{,}9239$; $\rho_{1000}=\sqrt{8\ln80/1000}=0{,}1872$; Hoeffding một hàm $\sqrt{\ln40/2000}=0{,}0429$ |
| 03.6 | phép dồn: đơn ánh, không thêm tập bị tách trọn, dừng ở họ đóng khi giảm | kiểm ngẫu nhiên 2000 họ $Y\subseteq\{0,1\}^n$, $n\le5$: $\lvert T_i(Y)\rvert=\lvert Y\rvert$, $\operatorname{sh}(T_iY)\subseteq\operatorname{sh}(Y)$, điểm dừng đóng khi giảm; $(e/2)^{10}=21{,}51<32$ |
| 03.7 | $\min\{k,n-k\}$; $\min\{2k+1,n\}$ | duyệt vét cạn mọi $n\le7$, mọi $k$ |
| 03.8 | bất đẳng thức "số cách gán nhãn $\le$ số tập con bị tách trọn" bằng quy nạp; một lớp hai hàm cho cả bốn tổ hợp | $\mathcal G=\{0,\mathbb 1[x\ge0]\}$: $\{1\}$: $2,2,2$; $\{1,2\}$: $2,3,3$; $\{-1,1\}$: $2,2,3$; $\{-1,1,2\}$: $2,3,4$; $\{-2,-1,1,2\}$: $2,3,5$; hàm ngưỡng $n+1$ ba lần; kiểm ngẫu nhiên 3000 họ |
| 03.9 | $\pm\mathbf e_j$ với $a_j\in\{-1,-\tfrac12\}$, $b_j\in\{\tfrac12,1\}$; chọn điểm cực trị mỗi tọa độ | duyệt mọi cách gán nhãn, $p\le4$ |
| 03.10 | $d\le p\log_23$ cần $p\ge2$ (số dư mod $8$); $\{\mathbf e_j\}$ với $L=\{\bar x_j: j\notin J\}$; thử thách $d\le p$ cần điểm thứ ba; đơn điệu $2^p+1$ hàm | duyệt vét cạn $p\le4$: $\lvert\mathcal H^p_{\mathrm{conj}}\rvert=4,10,28,82$; $d=2,2,3,4$; $\mathcal H^p_{\mathrm{mon}}$: $3,5,9,17$ hàm, $d=1,2,3,4$; $3^p\bmod8=3,1,3,1,\ldots$ |
| 03.11 | trung bình theo nhãn ngẫu nhiên: $\mathbb E L\ge(k-m)/(2k)$; $\Pr(\theta>a)\ge(\mu-a)/(1-a)$; $\epsilon=\delta=\tfrac18$; $m_{\mathcal H}\ge\lfloor d/2\rfloor+1$ | $k=2m$: $\mu=\tfrac14$, $(\tfrac14-\tfrac18)/(\tfrac78)=\tfrac17$; $d=11$: $6$ |
| 03.12 | $w=(2v,-1)$, $b=r^2-\lVert v\rVert^2$; tâm $v=\sum_{A}\mathbf e_i$, bình phương khoảng cách $a-1,a,a+1$; $r^2=a\pm\tfrac12$ | kiểm đồng nhất thức nâng chiều trên 10 000 bộ nguyên ngẫu nhiên; công thức bán kính đúng với mọi cách gán nhãn, $p\le5$ |

## 3. Đối chiếu với bản lời giải UML (sau khi tự giải)

| Bài UML | Bản lời giải | Khác biệt và cách xử lý |
|---|---|---|
| 6.2 | (a) đúng $\min\{k,\lvert\mathcal X\rvert-k\}$. (b) trả lời $k$, bỏ qua vế "hoặc nhiều nhất $k$ nhãn $0$" | Đáp số đúng $\min\{2k+1,n\}$ (khớp PTN §7, duyệt vét cạn $n\le7$). Lời giải của học phần rút cả hai phần về điều kiện theo số nhãn $1$ $s$ của cách gán nhãn. |
| 6.4 | Không chứng minh bất đẳng thức thứ nhất (nằm trong sách §6.5.1). Ví dụ: hình cầu đồng tâm $(<,=)$, hình chữ nhật trên ba điểm thẳng hàng $(=,<)$, nửa không gian thuần nhất trong $\mathbb R^d$, $d\ge3$, với $\mathbf e_1,\mathbf e_2,\mathbf e_1+\mathbf e_2$ $(<,<)$, hàm ngưỡng $(=,=)$ | Ý (a) của học phần chứng minh bất đẳng thức thứ nhất bằng quy nạp theo $\lvert C\rvert$ (quyết định ở `0-quyet-dinh.md` mục D), viết bằng lập luận riêng. Ý (b) dùng một lớp hai hàm $\{0,\mathbb 1[x\ge0]\}$ cho cả bốn tổ hợp, khác hẳn các ví dụ của bản lời giải. Lưu ý: PTN §7 ghi "$6<7<8$" cho nửa không gian thuần nhất; trong $\mathbb R^2$ ($d=2$) tổng nhị thức là $7$, nên ví dụ đó chỉ là $(<,<)$ khi $d\ge3$ (bản lời giải đúng ở điểm này). |
| 6.5 | Câu chuồng bồ câu "có $x$ sao cho với mọi $j$ tồn tại $x'$ với $x'_j\le x_j$…" rỗng nghĩa vì cho phép $x'=x$ | Lời giải của học phần chọn một điểm có tọa độ nhỏ nhất và một điểm có tọa độ lớn nhất cho mỗi $j$ (nhiều nhất $2p$ điểm), gán nhãn $0$ cho điểm còn lại; xử lý thêm $h_\varnothing$. Cận dưới dùng $a_j\in\{-1,-\tfrac12\}$, $b_j\in\{\tfrac12,1\}$ thay vì $\{-2,0\}$, $\{0,2\}$ của bản lời giải. |
| 6.6 | (b) viết "$\le3\log d$" (sai; đúng là $p\log_23$) và không lý giải bước $\lfloor\log_2(3^p+1)\rfloor\le p\log_23$. (c) dùng hội $\bigwedge_{j\in J}x_j$: **sai** khi $\lvert J\rvert\ge2$, vì $\mathbf e_i$ chỉ có một tọa độ $1$ nên hội đó bằng $0$ tại mọi $\mathbf e_i$. (d) đúng, cần $d+1\ge3$ điểm nhưng không nói rõ. (e) đúng | (b): học phần chứng minh $3^p+1$ không là lũy thừa của $2$ khi $p\ge2$ (mod $8$) và chỉ ra $p=1$ cho $d=2>\log_23$. (c): dùng $L=\{\bar x_j: j\notin J\}$. (d): nói rõ chỗ dùng $p\ge2$ (điểm thứ ba). Lỗi ở (c) không có trong PTN §7; đề nghị bổ sung. |
| 6.10 | (a) dùng Bài tập 5.3 với $k=d/m$, ngầm giả sử $d/m$ nguyên $\ge2$; (b) $\epsilon=\tfrac1{16}$, $\delta=\tfrac1{14}$, viết "$L_D\ge1/8>\epsilon$" | Học phần chứng minh trực tiếp bằng trung bình theo nhãn ngẫu nhiên trên tập bị tách trọn: $\mathbb E L\ge(k-m)/(2k)$ với mọi $k>m$, không cần chia hết. Thứ tự lượng từ trong đề UML ("tồn tại $D$, với mọi $m$") được đọc là "với mọi $m$, tồn tại $D$" (phân bố trong chứng minh phụ thuộc $A$ và $m$). Hằng số tự dẫn: $\Pr[L>\tfrac18]\ge\tfrac17$ khớp Định lý 03.17(a), rồi $\epsilon=\delta=\tfrac18$. Thêm ý (d): $m_{\mathcal H}(\epsilon,\delta)\ge\lfloor d/2\rfloor+1$ khi $\epsilon\le\tfrac18$, $\delta<\tfrac17$. |
| 9.6 | (a) viết $b=\lVert\mu\rVert^2-r^2$ trong khi công thức (4) của chính bản lời giải cho $r^2-\lVert\mu\rVert^2$; viết $y\in\{-1,1\}^d$ thay cho $\{-1,1\}^m$. (b) hai bán kính đổi chỗ: khi gốc thuộc tập dương lấy $r=\sqrt{\lvert A\rvert-1}$ (loại gốc), khi không thuộc lấy $\sqrt{\lvert A\rvert}$ (chứa gốc); không xử lý cách gán nhãn toàn $0$ hoặc chỉ gốc | Học phần: $b=r^2-\lVert v\rVert^2$; $r^2=a+\tfrac12$ khi gốc nhận nhãn $1$, $r^2=a-\tfrac12$ khi gốc nhận nhãn $0$ và $a\ge1$, hình cầu xa $v=-3\mathbf e_1$, $r=1$ cho toàn $0$; $a=0$ với gốc dương nằm sẵn trong công thức thứ nhất ($r^2=\tfrac12$). |

Không chép hay diễn lại sát câu chữ của sách hay bản lời giải.

## 4. Thuật ngữ và kí hiệu

- **Thuật ngữ mới** (tiếng Anh ở lần đầu trong tệp; chưa có trong `thuat-ngu.md`): phép dồn (shifting) — Bài tập 03.6; nguyên lý chuồng bồ câu (pigeonhole principle) — 03.2, dùng lại ở 03.10; hàm ngưỡng hai phía, lớp hợp hai khoảng, lớp hội đơn điệu, lớp hình cầu đóng (mô tả, không đặt từ mới). Đề nghị điều phối viên thêm "phép dồn" và "nguyên lý chuồng bồ câu" vào `thuat-ngu.md` §7.
- Đoạn mở đầu nhắc "cách gán nhãn (labeling)", "tách trọn (shatters)", "hàm tăng trưởng (growth function)", "chiều Vapnik–Chervonenkis (VC dimension)" vì tệp bài tập là một tài liệu riêng.
- **Kí hiệu cục bộ:** $\mathcal H_6$, $\mathcal H^{\pm}_{\mathrm{thr}}$ (03.1); $\mathcal H^{\circ}_{\mathrm{int}}$, $\mathcal H_{2\mathrm{int}}$ (03.2); $M$, $N$, $(w;b)$ (03.3); $\mathcal H_{\sin}$, $\mathcal H_\Sigma$, $F_1$, $\mathcal G_S$ (03.5; $\mathcal G_S$ theo `ky-hieu.md` cho lớp chọn theo mẫu); $T_i$, $y^{(i)}$, $\operatorname{sh}(Y)$, $w(Y)$, $Y^*$ (03.6); $\mathcal H_{=k}$, $\mathcal H^{\pm}_{\le k}$, $\lvert h\rvert$ (03.7); $\operatorname{sh}_{\mathcal H}(C)$, $\mathcal G$, $Y_1$, $\mathcal H_1$, $C_1,\ldots,C_4$ (03.8); $\mathcal H^p_{\mathrm{rec}}$ (03.9); $\mathcal H^p_{\mathrm{conj}}$, $\mathcal H^p_{\mathrm{mon}}$, $h_-$, $\mathbf 1$, $\mathbf 1_L$ (03.10); $D_f$, $h_f$, $F$, $V$, $\theta$, $\mu$, $a$ (03.11); $B_{v,r}$, $\mathcal B^p$, $\varphi$ (03.12). Không có chữ tiếng Việt trong `\text{}` (không dùng `\text{}`).
- Chữ $w$ dùng cho véc-tơ trọng số và, trong 03.6, cho hàm trọng $w(Y)$; hai bài tách biệt.

## 5. Sai khác so với `outline.md` §4 và đề nghị sửa §10 của ghi chú

- **03.1** giữ biến thể của dàn ý; thêm so sánh tại $m=1,2,3,10$.
- **03.2** đúng dàn ý; ý (c) thêm lời giải thứ hai (một tập năm điểm không bị tách trọn) để đo cả hai lỗi đối xứng của Nhận xét 03.4.
- **03.3** thêm ví dụ $p=2$ không phải đỉnh đơn hình; (c) thêm "tập chứa gốc không bị $\mathcal H^p_{\mathrm{hom}}$ tách trọn".
- **03.4** đổi số: Ví dụ 03.9 của ghi chú đã có mọi con số ở $\epsilon=0{,}1$ ($132\,992$, $447\,194$, $209\,624$, $693\,832$, $261\,198$, $889\,572$), nên ý (a) tính ở $\epsilon=0{,}05$. Thêm (d) lập luận bỏ mẫu bóng áp cho $\mathcal M_{[0,1]}$ ($0{,}590$ so với độ lệch $1$) để đo vế "vì sao không lấy hợp trên các cách gán nhãn của chính mẫu" của mục tiêu 3; thêm (e) rời rạc hóa với $q=3$ ($27\,355$, tỉ số $4{,}86=16\cdot0{,}304$) để đo vế "so với lớp hữu hạn sau khi rời rạc hóa, chỉ ra nguồn chênh lệch" của mục tiêu 4 (rà soát 5, mục nhẹ cuối). Số $27\,355$ đã bị cắt khỏi ghi chú, nên không trùng.
- **03.5** gộp hai ý (c), (d) của dàn ý thành (c); thêm (d) lớp một hàm chọn sau khi xem mẫu ($d=0$, độ lệch $\tfrac12$, $\rho_{1000}=0{,}187$) để đo vế "khi lớp được chọn sau khi xem mẫu" của mục tiêu 5; khác Ví dụ 03.8 (hai hàm, $d=1$, nhãn tất định).
- **03.6** dàn ý giao chứng minh "số cách gán nhãn $\le$ số tập con bị tách trọn" bằng quy nạp, nhưng "Trạng thái cuối" giao chính bất đẳng thức đó cho 03.8(a). Để không trùng, 03.6 chứng minh nó bằng phép dồn (một cách chứng minh khác thứ ba, sau Phụ lục B và 03.8(a)); ý về dạng đóng khi $m<d$ giữ ($21{,}51<32$).
- **03.8** viết theo tập hữu hạn (như UML), thêm ý (a) theo quyết định; các ví dụ ở (b) khác dàn ý (một lớp hai hàm).
- **03.9** một ý; nói rõ câu hỏi cuối buổi là trường hợp $p=2$.
- **03.10** thêm phần chứng minh $p\ge2$ là cần (ở (b) và (d)).
- **03.11** thêm ý (d) cận dưới $\lfloor d/2\rfloor+1$.
- **03.13** bỏ theo "Trạng thái cuối".

**Đề nghị sửa đúng hai dòng ở §10 của ghi chú** (người viết không sửa ghi chú):

```
4. **Bài tập 03.4** (So sánh cỡ mẫu theo chiều VC và nguồn gốc hằng số $8$): mục tiêu 3, 4.
5. **Bài tập 03.5** (Số tham số, lớp chọn sau khi xem mẫu và chiều VC): mục tiêu 5.
```

Các dòng còn lại của §10 khớp tên và mục tiêu trong `exercises.md`.

**Bản đồ mục tiêu:** 1 — 03.2, 03.3, 03.7, 03.9, 03.10, 03.12; 2 — 03.1, 03.6, 03.8; 3 — 03.4(c), (d); 4 — 03.4(a), (b), (e); 5 — 03.5 (cả ba loại phản ví dụ: (a)–(c) số tham số, (d) lớp chọn sau khi xem mẫu) và 03.11 (bỏ chiều VC hữu hạn).

## 6. Kiểm tra đã chạy

- `sync-local-materials.py` rồi `--check`: OK (6 tệp).
- `git diff --check`: sạch; tệp mới chưa theo dõi kiểm thêm bằng `git diff --no-index --check`: sạch, không khoảng trắng cuối dòng.
- `grep -c 'Đáp án'`: 0; `\text{}` có dấu tiếng Việt: 0 (tệp không dùng `\text{}`); "hãy": 0.
- Playwright, máy chủ của repo trên cổng 8766 (đã kiểm `ss -ltnp` và cwd của tiến trình): 1600×900 và 390×844, mở cả 48 khối `details`: 0 `.katex-error`, 1506 công thức, 0 lỗi console, 0 yêu cầu hỏng; 0 công thức hiển thị tràn khung ở 390 px (15 công thức đã ngắt dòng sau lần đo đầu), 0 bảng tràn, `scrollWidth` 375 ≤ 390. Đã xem ảnh chụp đầu trang và ba vùng lời giải ở 390 px.

## 7. Vòng sửa (2026-10-31, theo `reviews/11-quyet-dinh-bai-tap.md`)

Căn cứ: quyết định 11 (B1–B2, T1–T7, mọi điểm nhẹ), báo cáo 9 (toán) và 10 (sư phạm), dòng theo bản đóng băng `lec03-ex-frozen.md`. Người viết duy nhất, `no-ai-slop` chế độ Edit. Không commit. Bản trước vòng sửa lưu ở scratchpad (`lec03-ex-before-rev.md`).

### 7.1. Trạng thái từng mục

| Mục | Trạng thái | Chỗ sửa |
|---|---|---|
| B1 "chặt" | xong | 03.8 Mục tiêu: "đạt dấu bằng"; (b) Bước 3: "bất đẳng thức nghiêm ngặt", "ít nhất một điểm âm". `grep chặt`: 0 |
| B2 "theo cả hai chiều" | xong | 03.5(b) (trước là (c)): "không là cận trên … và cũng không là cận dưới"; tiêu đề lời giải "Số tham số và chiều VC". Quét "chiều": chỉ còn chiều VC, số chiều, chiều đặc trưng, "nâng chiều" (03.12, nghĩa số chiều) |
| T1 Gợi ý 03.9 | xong | Gợi ý 2: "Khi $a_l\le0\le b_l$ với mọi $l$, hình chữ nhật chứa $\mathbf e_j$ khi và chỉ khi $b_j\ge1$." Gợi ý 1 chỉ còn hướng (hai điểm mỗi trục, đối xứng; điểm cực trị mỗi tọa độ) |
| T2 §10 ghi chú | xong | Hai dòng 03.4, 03.5 thay đúng văn bản; ghi chú: 14 097 tiếng cả tệp, 11 990 tiếng thân bài (trước "## Phụ lục"); `forward_refs.py`: 0 |
| T3 mục tiêu 3 | xong | 03.4(f) mới: (T1) ở Bước 1 (C.2) và Bước 2 (C.3); tính bị chặn ở Bước 1 (C.2) và Bước 4 (C.4); (T5) ở Bước 3 (C.4), dẫn (d) và Ví dụ 03.8; (M) ở C.1 và C.7. Gợi ý 2 chỉ tới các dòng "Chỗ dùng" và câu cuối Phụ lục C |
| T4 vai của $\epsilon$ | xong | Đề 03.4: (a), (b), (e) là rủi ro vượt mức, (c) là độ lệch đều; (b) Bước 2 "xấp xỉ bằng … vì tại cỡ mẫu nhỏ nhất $m\approx12\,800(\cdot)$"; (a) ghi đủ $0{,}0024999964$ |
| T5 máy tính | xong | Đề (a) viết điều kiện $\frac{32}m(d\ln\frac{2em}d+\ln\frac4\delta)\le\epsilon^2$ và "dùng máy tính (chia đôi khoảng)"; lời giải kiểm $m$, $m-1$ cho cả $d=3$ và $d=11$; ghi $3\cdot10{,}8435+4{,}3820=36{,}9125$, $11\cdot10{,}8435+4{,}3820=123{,}6605$ |
| T6 trùng Nhận xét 03.10(iii) | xong (cắt) | Bỏ 03.5(b) cũ và gợi ý của nó; ý (b) mới dẫn thẳng Nhận xét 03.10(iii). 03.5 còn (a) $\sin$, (b) số tham số, (c) lớp chọn sau khi xem mẫu |
| T7 §7a | xong | 58 (03.1(b) Bước 1–2); 127 (03.2(b) Bước 1–2); 135 (03.2(c) rút gọn, ba câu); 191 (03.3(b) Bước 1–3, phép khử trong `aligned`, đánh số (1)–(3)); 281 (rút còn hai câu); 318 (03.4(d) Bước 3–4); 408 (bỏ cùng 03.5(b) cũ); 410 (03.5(b) Bước 1–3); 474 (03.6(a) ba trường hợp gạch đầu dòng); 484 (03.6(c) Bước 1–2); 602 (03.8(a) Bước 4–7); 623 (03.8(c) Bước 1–3); 693 (03.10(a) còn một câu); 703 (03.10(c) Bước 1–2); 717 (03.10(e) Bước 1–3); 797 (03.11(c) Bước 1–4); 799 (03.11(d) Bước 1–3) |

**Điểm nhẹ (R9).** 03.8(c) Bước 2: "$\{x\}$ bị tách trọn vì $h_x(x)=1$, $h_{x+1}(x)=0$; theo Bước 2 của chứng minh Mệnh đề 03.5 …". 03.6(d) Bước 1 dẫn phép đếm $w$ của (c) để có $k=0$. 03.11: đề (a) ghi "$D$ phụ thuộc $A$ và $m$"; Bước 4 dùng tính tất định (Định nghĩa 01.4); Gợi ý 1 chỉ dẫn lập luận không có bữa trưa miễn phí (Nhận xét 01.30), ý lấy trung bình chuyển sang Gợi ý 2; (d) Bước 1 trường hợp $d\le1$; điểm ngẫu nhiên của $D_f$ đổi thành $U$, kì vọng có điều kiện viết $X_1,\ldots,X_m$.

**Điểm nhẹ (R10).**
- Kí hiệu: $\mathcal H_6\to\mathcal H^{(6)}_{\mathrm{thr}}$; $\mathcal H_1\to\mathcal H'$; $\mathcal H^{\pm}_{\le k}\to\mathcal H^{0/1}_{\le k}$; $h_-\to h_{\equiv0}$ (khai báo ở đoạn mở đầu; $h_\varnothing$ giữ ở 03.9); $\mathcal B^p\to\mathcal H^p_{\mathrm{ball}}$.
- Thuật ngữ tiếng Anh: đoạn mở đầu thêm mẫu bóng, rủi ro vượt mức, độc lập afin, đơn hình; tại chỗ: nguyên tử (atom) ở 03.5, *hội đơn điệu* (monotone conjunction) ở 03.10, phân bố biên (marginal distribution) ở 03.11.
- 03.2(a) nói chỗ khác Mệnh đề 03.6 (bất đẳng thức nghiêm ngặt) và rút ngắn.
- 03.6: bỏ (e); câu đề "Suy ra khi áp dụng lặp lại …"; thêm "Bài tập 03.8(a) chứng minh bất đẳng thức của (d) bằng quy nạp".
- Kiểm tra lại: 03.8 kiểm (a) với $\mathcal H_{\mathrm{thr}}$, $C=\{1,2,3\}$ ($4=4=4$); 03.5 bỏ Bước 4 cũ, giữ một trường hợp số ($y=(1,0,1)$); 03.1 thêm $\mathcal H^{\pm}_{\mathrm{thr}}\cup\{0,1\}=\mathcal H^1_{\mathrm{aff}}$, $d=2=p+1$.
- 03.4(c): đề dẫn câu cuối của chứng minh Định lý 03.15; nhãn "Bước 1 của chứng minh (mẫu bóng)", "Bước 4 của chứng minh (Hoeffding)". 03.4(e) dẫn Ví dụ 03.10 với $q=3$.
- Mục tiêu 5, vế "phát biểu định lý cơ bản": 03.11(c) yêu cầu phát biểu sáu khẳng định của Định lý 03.17(b) và chỉ ra phép kéo theo được chứng minh; lời giải Bước 4.
- Gợi ý theo độ mạnh: 03.9 (tập cụ thể sang Gợi ý 2), 03.10 ("chia cho $8$" sang Gợi ý 2), 03.11 (như trên).
- Câu dài: đoạn mở đầu tách thành ba đoạn; 03.4 dòng Mục tiêu viết lại; 03.8 Bước 4 cũ tách ba bước; 03.9 Bước 3 cũ tách hai bước.
- §9a: các câu ở dòng 56, 58, 199, 303, 316, 410, 428, 438, 602, 365 viết lại theo đề xuất (303 bị bỏ hẳn vì trùng câu trước).

**Cắt để giữ độ dài** (theo danh sách của quyết định): 03.6(e); 03.5(b) cũ; 03.2(a) thu gọn; 03.5 Bước 4 cũ; 03.4(b) Bước 3; 03.3(b) bỏ trường hợp $p=3$ (vốn chỉ thay số vào công thức của Mệnh đề 03.9). Cắt thêm nhỏ: Gợi ý 1 chung của 03.2 (bài còn hai gợi ý), câu cuối 03.4(d) Bước 4 cũ về $\rho_m\ge3{,}33$, câu cuối 03.4(c) Bước 3 cũ, câu so với Định lý 03.19(b) ở 03.11(d), câu về tổng hữu hạn ở 03.11(a) Bước 6, phần giải thích của 03.10(a), câu lớp gồm mọi hàm ở 03.7(b) Bước 4, câu "liệt kê với $n\le7$" ở Kiểm tra lại 03.7, câu dẫn đỉnh đơn hình ở 03.12(b) Bước 3, câu đối chiếu với Ví dụ 03.8 ở 03.5(c) Bước 5. Mọi mục tiêu vẫn được đo: 1 (03.2, 03.3, 03.7, 03.9, 03.10, 03.12); 2 (03.1, 03.6, 03.8); 3 (03.4(c), (d), (f)); 4 (03.4(a), (b), (e)); 5 (03.5, 03.11 gồm cả phát biểu định lý cơ bản).

Thêm một chỗ tự phát hiện: 03.12(b) dùng $A$, $a$ chỉ định nghĩa trong gợi ý; Bước 1 của lời giải nay định nghĩa chúng.

### 7.2. Con số mới hoặc đổi (tính lại trong scratchpad, `ex03_nums.py`, `ex03_nums2.py`)

- $d=11$, $\epsilon=0{,}05$: vế trái $32(11\ln(2em/11)+\ln80)/m$ bằng $0{,}0024999991$ tại $m=1\,999\,657$ và $0{,}0025000002$ tại $m=1\,999\,656$.
- $d=3$: $0{,}0024999964$ (ghi đủ chữ số) tại $m=589\,118$; $0{,}0025000003$ tại $589\,117$.
- $3\cdot10{,}843495+4{,}382027=36{,}912511$; $11\cdot10{,}843495+4{,}382027=123{,}660470$.
- $12\,800=32/0{,}0025$; tỉ số cỡ mẫu $3{,}394323$ so với tỉ số ngoặc $3{,}394327$.
- Không con số nào khác đổi; các con số bị cắt ($21{,}51$; $w=(2,0,2)$; ngoặc $46{,}02$, $156{,}22$ vẫn giữ trong văn bản) không cần tính lại.

### 7.3. Kiểm tra đã chạy

- `exercises.md`: 9 997 tiếng (`wc -w`), 12 bài, 35 khối `hint`, 12 dòng "Kiểm tra lại".
- `sync-local-materials.py` rồi `--check`: OK (6 tệp). `git diff --check`: sạch; `git diff --no-index --check` cho tệp mới: sạch. `\text{}` có dấu tiếng Việt: 0 (chỉ còn `\text{(1)}`, `\text{(2)}`, `\text{(3)}`); "Đáp án": 0; "chặt": 0.
- `forward_refs.py` trên ghi chú: 0.
- Playwright, máy chủ của repo trên cổng 8766: bài tập ở 1600×900 và 390×844, mở cả 47 khối: 0 `.katex-error` (1484 công thức), 0 lỗi console, 0 yêu cầu hỏng, 0 công thức hay bảng tràn (đã ngắt lại hai công thức sau lần đo đầu), `scrollWidth` 375; ghi chú ở hai cỡ: 0 `.katex-error` (1575 công thức), 0 lỗi, 0 yêu cầu hỏng, 0 tràn. Đã xem ảnh 03.4(f) và 03.3(b) ở 390 px.

## 8. Vòng sửa cuối (2026-10-31, theo `reviews/12-ra-lai-bai-tap-toan.md` và `13-ra-lai-bai-tap-su-pham.md`)

Cả hai báo cáo kết luận "giao được"; áp đủ 10 điểm nhẹ.

- **R12-1.** 03.4(f): "Bài tập 03.5(c) và Ví dụ 03.8 cho thấy bước này hỏng khi bỏ (T5)."
- **R12-2.** 03.11(c) Bước 4: Bước 2 là phản đảo của (4)⇒(6); Bước 3 thêm (3)⇒(6) qua (3)⇒(4); cả hai không dùng (M).
- **R12-3.** 03.2(a): nêu hai chỗ khác Mệnh đề 03.6 (bất đẳng thức nghiêm ngặt ở cận trên; khoảng $(-1,\tfrac12)$, $(\tfrac12,2)$ thay khoảng một điểm ở cận dưới).
- **N1.** 03.4(f): $\sigma_ia_i$ thay bằng $\sigma_i(\ell(h,Z'_i)-\ell(h,Z_i))$.
- **N2.** 03.4(c): nhãn "Bước 2: mẫu bóng (Bước 1 của chứng minh)", "Bước 3: Hoeffding (Bước 4 của chứng minh)".
- **N3.** 03.2(c): "(Ví dụ 03.3, Bước 2: một tập ba điểm không bị tách trọn dù $d=3$)"; bù bằng cách bỏ câu "Với $d=11$, cận này là $6$" ở 03.11(d).
- **N4.** 03.9 Kiểm tra lại: thêm lý do $h_\varnothing$ trùng một khoảng một điểm ngoài tập; bù bằng cách bỏ câu "Cận trên $p+2=3$ không đạt khi $p=1$" và cụm "có độ dài dương" ở 03.12.
- **N5.** 03.10(a): đề đổi thành "Nhắc lại từ Bài tập 02.8(a): …"; lời giải giữ dẫn chiếu.
- **N6.** 03.4(c): tách câu dài tại dấu chấm phẩy (dòng 213 giữ nguyên, là dòng Mục tiêu).
- **N7.** Độ dài: bù thêm bằng ba câu cắt — câu cuối 03.3(c) Bước 3 (đã có ở Bước 2), câu "Cách toàn $0$ vẫn cần một khoảng nằm ngoài $C$" ở 03.2(a) Bước 1 (nay nằm trong câu dẫn của (a)), phần "gấp hơn mười lần …" ở 03.5(c) Bước 5. Kết quả 9 993 tiếng.

Không con số nào đổi. Kiểm tra: sync và `--check` OK; `git diff --check` sạch (tệp mới: `--no-index --check` sạch); `\text{}` có dấu: 0; Playwright cổng 8766, 1600×900 và 390×844, mở 47 khối: 0 `.katex-error` (1481 công thức), 0 lỗi console, 0 yêu cầu hỏng, 0 công thức hay bảng tràn, `scrollWidth` 375.
