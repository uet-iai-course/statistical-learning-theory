# Ghi chú của người soạn bài tập Bài 10

Tệp nội bộ, không liên kết từ trang chỉ mục. Người soạn: tác tử soạn bài tập (2026-11-01). Sản phẩm: `2627-1/materials/lec-10/exercises.md` (7 bài gốc, 2 bài UML; 36 khối: 9 `exercise`, 18 `hint`, 9 `solution`; 9 788 tiếng theo `wc -w`; 926 dòng).
Sau vòng sửa §8: 9 961 tiếng, 36 khối, ý mới 10.1(f).

## 1. Bài UML: số bài, thời điểm tự giải, bản lời giải

- **Số bài đã kiểm trên PDF.** `understanding-machine-learning-theory-algorithms.pdf` tr. 305–306, §21.7 có đúng năm bài: 21.1 (Consistent mắc $|\mathcal H|-1$ lỗi), 21.2 (cận của Halving chặt), 21.3 (Halving trên lớp chỉ số), 21.4 (mẹo nhân đôi; đề nằm ở tr. 305–306), 21.5 (chuyển từ học trực tuyến sang học theo lô, gợi ý dẫn Định lý 14.8 của UML; tr. 306). Bài tập 10.8 = 21.5, 10.9 = 21.4 (tùy chọn), khớp dàn ý.
- **Tự giải.** Lập luận của 21.4 và 21.5 (kể cả việc 21.4 cần $\lfloor\log_2T\rfloor$ và điểm so sánh $u$ cố định chung cho mọi đoạn) được lập lúc 01:27 (+07), 2026-11-01; lời giải viết vào `exercises.md` xong lúc 01:37:28.
- **Mở bản lời giải.** `MLbookSol.pdf` tr. 51–53 (chương 21 bắt đầu ở cuối tr. 51; bài 21.4–21.5 ở tr. 52–53), mở lúc 01:37:45 (+07) ngày 2026-11-01, sau khi tự giải. Không chép, không diễn đạt sát; lời giải trong `exercises.md` theo lập luận riêng đã viết trước.
- **Chỗ bản lời giải sai hoặc thiếu.**
  1. 21.4: tổng chạy từ $m=1$ (bỏ đoạn $m=0$) đến $\lceil\log T\rceil$; với trần, bước "$\le\alpha\frac{1-\sqrt{2T}}{1-\sqrt2}$" đi sai chiều khi $T$ không là lũy thừa của $2$, vì $\sqrt2^{\lceil\log T\rceil+1}\ge\sqrt{2T}$. Cần $M=\lfloor\log_2T\rfloor$ và chỉ số từ $0$ (lời giải của học phần). Bản lời giải cũng không nói hối tiếc tách được thành tổng theo đoạn chỉ khi $u$ cố định chung.
  2. 21.5: dòng đầu viết "$L_D(h_r)=\frac1T\sum_tL_D(h_t)$" như một đẳng thức của biến ngẫu nhiên; đúng phải là kì vọng theo $r$. Không nói thuật toán tất định, và dùng cận số lỗi mà không nêu rằng nó đúng trên mọi dãy khả thực (nên đúng sau khi lấy kì vọng).

## 2. Sai khác với `outline.md` §4 (kèm lý do)

Lý do chung: quyết định bài tập Bài 07–09 cấm chép lại chứng minh hoặc phép tính đã có trong ghi chú; ghi chú Bài 10 sau hai vòng biên tập đã làm sẵn một số ý của dàn ý (Hệ quả 10.8 và Phụ lục B; Nhận xét 10.9(i) với $\ln2$; Ví dụ 10.13 Bước 5 về hai quy ước độ quên; Ví dụ 10.14 với năm $\lambda$). Các ý đó được thay bằng biến thể cùng mục tiêu.

1. **10.1.** (a), (b) theo dàn ý ($\tfrac14$; $1$; $\tfrac34$; giá trị $3$ và $0$; phương sai $\tfrac{27}{16}$). (c) thêm đẳng thức $\operatorname{Var}(\hat g_b)=\operatorname{Var}(\hat g_{b^*})+\pi(1-\pi)(b-b^*)^2$ (ghi chú chỉ có $b^*$ ở Ví dụ 10.8); $b=J=1$: $\tfrac94$, $\tfrac14$, phương sai $\tfrac34$; $b^*=3$, phương sai $0$. Thêm (d): xác suất bước ngược dấu với $b\in\{0,1,5\}$ là $0$, $0$, $\tfrac14$; $b=1$ và $b=5$ có cùng phương sai $\tfrac34$. (e) theo dàn ý ($J''=\tfrac38$, lõm khi $\theta\ge0$).
2. **10.2.** (a) dàn ý "chứng minh Hệ quả 10.8 cho $b_t$ là hàm của lịch sử" chép lại Hệ quả 10.8 và Phụ lục B; thay bằng công thức độ chệch của giá trị nền phụ thuộc hành động $\tilde b(S_t,A_t)$ (tọa độ $\theta_s$: $\Pr(S_t=s)\pi(1-\pi)(\tilde b(s,1)-\tilde b(s,0))$), khái quát Ví dụ 10.9. (b) theo dàn ý ($0{,}225$, ngược dấu $-0{,}025$), thêm cách tính bằng (a). (c) theo dàn ý, thêm phương sai tọa độ $\theta_{s_1}$: $0{,}4875$ so với $\tfrac9{16}$. (d) dàn ý ($\ln2$ tại $\theta=0$) đã có ở Nhận xét 10.9(i); thay bằng chứng minh công thức entropy (ghi chú chỉ phát biểu) và tính tại $\theta=\ln3$: $\mathrm H(\tfrac34)\approx0{,}5623$, kì vọng $0{,}9373$.
3. **10.3.** Theo §13.6 của dàn ý: (a) viết lượt thành $g(\theta,\xi)$ với $\xi$ gồm $2H$ biến đều độc lập, các $\xi_j$ độc lập cùng phân bố; $\psi=\nabla F$ trên cả không gian. (b) thêm cận chung $G=H^2C_rC_\pi$ khi phần thưởng và gradient log bị chặn ($C_\pi=1$ cho chính sách bảng); giá trị đúng $\pi(1-\pi)(9-8\pi)$, lớn nhất $1{,}25$ trên $[0,2]$ (chứng minh bằng nghiệm của $f'$). (c)(i) thêm phản ví dụ cho dạng $\psi\in\partial F$ của (G1) tại $\theta=-2$ (tiếp tuyến tại $u=0$: $-1{,}6584>F(0)=-2$). (c)(ii) mở rộng lồi tiếp tuyến tại $0$ như ghi chú của dàn ý; đã kiểm: $\tilde F$ khả vi, $\tilde F'$ không giảm, (G1) qua Mệnh đề 05.3(a) trên $W$. (c)(iii) $\eta\approx0{,}01789$, cận $\le0{,}0224$, $\mathbb EJ(\bar\theta_T)\ge2{,}7392$. (d) thêm: tại điểm dừng của Ví dụ 10.7, $\psi=0\notin\partial F$. Kết luận: (G1) dạng không chệch và (G2) giữ được; giả thiết hỏng là (C).
4. **10.4.** Tiêu đề mới theo §13.6. (a) theo dàn ý. (c) dàn ý (ma trận $2\times2$ cho hai quy ước độ quên "khác dấu") vừa trùng Ví dụ 10.13 Bước 5 vừa sai như phát hiện của người rà ghi chú (hai giá trị là $0$ và một số âm, không khác dấu); thay (b) bằng chứng minh "độ quên trung bình $\ge$ đối của chuyển đổi ngược, dấu bằng khi đỉnh ở hàng $i$", và (c) bằng khoảng tin cậy đồng thời cho chuyển đổi ngược và xuôi (Hệ quả 02.10, cận hợp trên bảy ô, $n=2000$, $\delta=0{,}05$). (d) theo dàn ý.
5. **10.5.** (a) dàn ý (ba giá trị $\lambda$) giữ, vì tên bài ở §11 là "ba hệ số"; thêm câu hỏi ngược: $\lambda$ nhỏ nhất để $L_A\le0{,}02$ là $4$. (b) theo dàn ý (tối ưu Pareto; thêm chiều "$w\notin[0,1]$ không tối ưu"). (c) theo dàn ý, thêm điều kiện tổng quát $\lambda\Omega=4\alpha/(1-\alpha)$. (d) dàn ý ("có $\lambda$ nào làm $L_A+L_B<\tfrac14$") chỉ nhắc lại Mệnh đề 10.13(a); thay bằng giá trị nhỏ nhất $\tfrac25$ của $L_A+L_B$ với độ cong $4$, so với $\tfrac58$ của phép phạt $\Omega=1$.
6. **10.6.** (a) theo danh sách của dàn ý, mỗi mục thêm một cách làm sai và hậu quả. Thêm (b) phần tính trên số đã chạy (mục 3) theo quyết định Bài 07–09 (sai số chuẩn theo hiệu khi chung hạt giống), và (c) thiếu sót của Phụ lục C (một thứ tự; phát lại tính hai gradient mỗi bước; siêu tham số cố định; không có hàng sau nhiệm vụ A trong bảng; không có hiệu theo hạt giống). Đề không nêu đường dẫn script (ngoài repo).
7. **10.7.** Tiêu đề theo §11 ("Năm câu hỏi tổng kết cho hai thiết lập khác"). Theo dàn ý; (ii) viết cho "giá trị kế tiếp" (Thiết lập B cho phép giá trị thực), thêm dạng yếu của (T1) khi chuỗi dừng; thêm câu hỏi "thay đổi làm (T1) đúng hay hỏng". Định nghĩa 09.1 đã kiểm (Hai thiết lập lấy mẫu cho dữ liệu chuỗi).
8. **10.8.** Theo dàn ý. Thêm (b) bất đẳng thức Markov: $\Pr(L_D(h_r)\ge0{,}05)\le0{,}05$ khi $T\ge4000$ với $M_A=10$; (c) hai phân bố $D_1$, $D_2$: cận chỉ chặn trung bình rủi ro theo phân bố của từng vòng, như hối tiếc ở Ví dụ 10.17, không chặn độ quên. Dòng mục tiêu ghi "(b), (c) do học phần thêm". Câu "lập luận dùng đúng giả thiết mà học liên tục bỏ" thành (c).
9. **10.9.** Theo dàn ý; thêm (b) kiểm giả thiết của (a) cho hạ gradient trực tuyến của Nhận xét 10.16 khởi động lại mỗi đoạn, kể cả đoạn bị cắt ($\alpha=RG$). Câu về điểm so sánh cố định chung (ghi chú của dàn ý) nằm ở (a) Bước 4.
10. **Mục tiêu được đo:** 1 (10.7); 2 (10.1); 3 (10.1, 10.2); 4 (10.4, 10.6); 5 (10.3, 10.5, 10.7, 10.8, 10.9). Loại bài: chứng minh, tính toán, khái niệm, kiểm tra giả thiết, thực nghiệm (thiết kế và tính trên số đã chạy).
11. **Thuật ngữ mới trong bài tập** (đã có trong `thuat-ngu.md` §12 với ghi chú "chỉ bài tập"): cận số lỗi (mistake bound), chuyển từ học trực tuyến sang học theo lô (online-to-batch conversion), mẹo nhân đôi (doubling trick), tối ưu Pareto (Pareto optimal). Kí hiệu cục bộ: $\tilde b$ (10.2), $\Delta r$, $d$ (10.1), $C_r$, $C_\pi$, $g(\theta,\xi)$, $U_{\mathrm{init}}$, $U_t$, $V_t$, $\tilde F$ (10.3), $\Delta_{\mathrm b}$, $\Delta_{\mathrm f}$ (10.4), $I_m$ (10.9).

## 3. Thí nghiệm (Bài tập 10.6)

Script của ghi chú (không sửa): `../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec10_pg_replay.py --part replay`. Số theo hạt giống lấy bằng scratchpad `ex10/replay_seeds.py`: hàm `replay2` chép giao thức của script (cùng thứ tự rút) và thêm rủi ro kiểm tra sau nhiệm vụ A; script kiểm `np.allclose` với `replay` của script cho mọi $M$ (khớp). Chạy lúc 2026-11-01 01:34.

| $M$ | Rủi ro A sau A (độ lệch chuẩn) | Rủi ro B sau A | Rủi ro A sau B (độ lệch chuẩn) | Rủi ro B sau B (độ lệch chuẩn) | Tổng sau B |
|---|---|---|---|---|---|
| 0 | 0,12507 (0,00175) | 0,61407 | 0,62352 (0,05061) | 0,12626 (0,00347) | 0,74978 |
| 5 | như trên | như trên | 0,33130 (0,13235) | 0,21835 (0,07607) | 0,54965 |
| 50 | như trên | như trên | 0,25646 (0,03626) | 0,24786 (0,03776) | 0,50433 |
| 1000 | như trên | như trên | 0,25163 (0,04193) | 0,25461 (0,04491) | 0,50624 |

Hiệu rủi ro A sau B theo hạt giống (trung bình; độ lệch chuẩn; sai số chuẩn; tỉ số; sai số chuẩn coi độc lập): $0-5$: $0{,}29222$; $0{,}12348$; $0{,}02761$; $10{,}58$; $0{,}03168$. $5-50$: $0{,}07484$; $0{,}11652$; $0{,}02606$; $2{,}87$; $0{,}03069$. $50-1000$: $0{,}00484$; $0{,}04272$; $0{,}00955$; $0{,}51$; $0{,}01239$. Với số đã làm tròn trong đề: sai số chuẩn $0{,}0275$; $0{,}0262$; $0{,}0096$; tỉ số $10{,}6$; $2{,}9$; $0{,}5$; coi độc lập ở cặp cuối $0{,}0124$. Rủi ro B sau B (không dùng trong bài): hiệu $0-5$: $-0{,}092$ (sai số chuẩn $0{,}017$). Độ quên theo thang rủi ro (theo hạt giống): $0{,}4985$; $0{,}2062$; $0{,}1314$; $0{,}1266$. Số trung bình khớp Phụ lục C ($0{,}624$; $0{,}331$; $0{,}256$; $0{,}252$ và $0{,}126$; $0{,}218$; $0{,}248$; $0{,}255$).

## 4. Các con số khác và script (scratchpad `ex10/`)

| Bài | Con số | Script |
|---|---|---|
| 10.1 | $\pi=\tfrac14$, $J=1$, $J'=\tfrac34$, $J''=\tfrac38$; $b=0$: $3,0$, $\tfrac{27}{16}$; $b=1$: $\tfrac94,\tfrac14$, $\tfrac34$; $b=3$: $\tfrac34,\tfrac34$, $0$; $b=5$: $-\tfrac34,\tfrac54$, $\tfrac34$ | `nums.py` (phân số đúng) |
| 10.2 | $\partial J/\partial\theta_{s_0}=-0{,}025$; $\mathbb E r_0(a_0-\tfrac12)=-0{,}25$; số hạng $t=0$ có giá trị nền $r_0$: $0{,}225$; tọa độ $\theta_{s_1}$: kì vọng $0{,}25$, phương sai $0{,}5625\to0{,}4875$; $\theta_{s_2}$: $-0{,}125$, phương sai $0{,}046875$ không đổi; $\mathrm H(\tfrac34)=0{,}562335$; $0{,}375+0{,}562335=0{,}937335$ | `nums.py` |
| 10.3 | $\max_{[0,2]}\mathbb E\varphi^2=1{,}25$ tại $\theta=0$ (lưới $20\,001$ điểm); $\sup_{\mathbb R}=1{,}41055$ tại $\theta\approx-0{,}609$; nghiệm $f'$: $0{,}352333$, $1{,}064333$; $\pi_2(1)=0{,}880797$; $G=1{,}118034$; $J''(-2)=0{,}159925$; $F(-2)=-1{,}238406$, $F'(-2)=-0{,}209987$, tiếp tuyến tại $0$: $-1{,}658380$; $\eta=0{,}0178885$; cận $0{,}0223607\to0{,}0224$; $J(2)=2{,}761594$; $2{,}761594-0{,}0224=2{,}739194\to2{,}7392$ | `nums.py`, `ex103.py` |
| 10.4 | $0{,}753333$; $-0{,}19$; độ quên $0{,}15$, $0{,}28$, trung bình $0{,}215$; xuôi $0{,}015$; bảy ô: $\ln280=5{,}634790$, $\epsilon=0{,}0375326\to0{,}0376$, $2\epsilon\le0{,}0752$; ngược $\le-0{,}1148$; xuôi $[-0{,}0602;\,0{,}0902]$ (bốn ô cho riêng chuyển đổi ngược: $\epsilon=0{,}0356$) | `nums.py` và lệnh một dòng |
| 10.5 | $\lambda=\tfrac12,2,4$: $w=\tfrac23,\tfrac13,\tfrac15$; $L_A=\tfrac29,\tfrac1{18},\tfrac1{50}$; $L_B=\tfrac1{18},\tfrac29,\tfrac8{25}$; $\alpha=\tfrac13,\tfrac23,\tfrac45$; tổng $\tfrac5{18},\tfrac5{18},\tfrac{17}{50}$; độ cong $4$: tổng nhỏ nhất $\tfrac25$ tại $\tfrac15$, tại $\tfrac12$: $\tfrac58$ | `nums.py` |
| 10.8 | $10/1000=0{,}01$; $10/(0{,}05\cdot0{,}05)=4000$ | tay |
| 10.9 | $M=9$; $\sum_{m=0}^92^{m/2}=74{,}8406$; $\frac{\sqrt2}{\sqrt2-1}=3{,}414214$; cận $107{,}9669\to107{,}97$; $\sqrt{1000}=31{,}6228$ | `nums.py` |

Quy tắc làm tròn: cận trên làm tròn lên, số đo làm tròn gần nhất.

## 5. Kiểm tra đã chạy

`sync-local-materials.py` và `--check` (OK, 20 tệp); 0 khoảng trắng cuối dòng; 36 khối mở, 36 khối đóng, không lồng (kiểm bằng script; một khối đóng thiếu ở 10.4 được phát hiện và thêm); `wc -w` 9 788; không có "Đáp án", "hãy", "rõ ràng", "dễ thấy", "hiển nhiên", "người học", không có `\text{}`; tệp kết thúc bằng đúng một ký tự xuống dòng. Viewer qua HTTP (`reloadserver` cổng 8786, đã tắt), mọi `details` mở (27), ở 390×844 và 1600×900: 1 180 công thức KaTeX, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức hay bảng tràn (lần đo đầu có 18 công thức và 2 bảng tràn ở 390, đã tách bằng `aligned` và rút cột), độ rộng trang 375 px ở 390. Console chỉ có cảnh báo CSP do `reloadserver` chèn script nội tuyến (như Bài 07–09). Ảnh `ex10/shot_390.png`, `ex10/shot_390_103.png`, `ex10/shot_390_end.png`, `ex10/shot_1600.png`. Bản trước khi tách công thức: `ex10/ex_before_wrap.md`.

## 6. Điểm không chắc

1. **10.3(a)** Tính đo được của $\varphi$ theo cặp $(\theta,\xi)$ chỉ lập luận một câu (hằng trên từng hộp khi $\theta$ cố định, liên tục theo $\theta$ trên mỗi hộp); các hộp phụ thuộc $\theta$ qua ngưỡng $\pi_\theta(1\mid s)$. Người rà toán nên kiểm câu này (một cách viết chặt: $\varphi$ là tổng hữu hạn của tích các hàm chỉ thị $\mathbb 1[U_t<\pi_\theta(1\mid s)]$, đo được theo cặp vì $\{(\theta,u):u<\pi_\theta(1\mid s)\}$ mở, với các hàm liên tục của $\theta$).
2. **10.3(c)(i)** câu "$F$ không lồi trên mọi khoảng chứa một điểm âm" dùng $F''<0$ trên $(-\infty,0)$; khoảng suy biến bị bỏ qua.
3. **10.4(c)** "giá trị tổng thể" của chuyển đổi xuôi dùng $\mathrm{acc}^\circ_i$ của một mô hình huấn luyện riêng, cũng đánh giá trên mẫu kiểm tra của nhiệm vụ $i$; cận hợp không cần độc lập giữa các ô. Mô hình được cố định khi điều kiện hóa theo dữ liệu huấn luyện.
4. **10.6(a)** mục "Chọn siêu tham số" nêu hai cách (theo thời điểm, hoặc một lần cho cả dãy và ghi rõ); học phần không có nguồn về thực hành của cộng đồng, nên không khẳng định cách nào phổ biến.
5. **Độ dài**: 9 788 tiếng, dưới trần 10 000 khoảng 200 tiếng; nếu người rà yêu cầu thêm nội dung, ứng viên cắt: 10.1(d) Bước 4, 10.6(c), 10.7 "Kiểm tra lại".

## 8. Vòng sửa theo `reviews/11-quyet-dinh-bai-tap.md` (2026-11-01)

Căn cứ: `reviews/9-bai-tap-toan.md` (0/0/1/3), `reviews/10-bai-tap-su-pham.md` (0/0/3/19), quyết định của điều phối viên (7 mục và các điểm nhẹ). Bản trước khi sửa: scratchpad `ex10/ex_before_fix.md`; sau khi sửa, trước khi cắt chữ: `ex10/ex_after_fix_before_cut.md`. Script sửa: `ex10/fix1.py`, `ex10/cut1.py`.

**Đã áp dụng.**

1. Toán 1: 10.3(a) Bước 2 viết lại theo đề xuất của người rà 2. Mỗi tập $\{g(\theta,\xi)=\tau'\}$ là giao hữu hạn của các tập $\{U_t<\pi_\theta(1\mid s_t)\}$ hay phần bù của chúng; do đó $\varphi$ là tổng hữu hạn của các tích (chỉ thị đo được theo cặp) × (hàm liên tục theo $\theta$).
2. Toán 2: 10.4(c) Bước 1 điều kiện hóa theo dữ liệu huấn luyện và nguồn ngẫu nhiên; giá trị tổng thể là một số cố định khi điều kiện hóa, nhưng ngẫu nhiên theo dữ liệu huấn luyện. Bước 3 cho khoảng $\Delta_{\mathrm b}\in[-0{,}2652;\,-0{,}1148]$ (N6) và câu "đúng có điều kiện, nên đúng khi lấy kì vọng".
3. Toán 3: 10.9(b) đề thêm "$W$ bị chặn và $R\ge\sup_{u\in W}\lVert w_1-u\rVert$"; lời giải "với mọi $u\in W$, vốn có $\lVert w_1-u\rVert\le R$".
4. Toán 4: 10.9(a) Bước 4 bỏ "Thứ tự này cần thiết"; viết "vì $\sup_u\sum_m\le\sum_m\sup_u$, lấy cận trên đúng theo từng đoạn trước cũng cho cùng cận". Vai trò của $u$ chung đã nằm ở Bước 2.
5. T1: thêm 10.1(f) (đề, một câu ở mỗi gợi ý, lời giải bốn bước). Mật độ $p_\theta(a)=\theta e^{-\theta a}$, $r(a)=\mathbb 1[a\le1]$. Ba điều kiện của Nhận xét 10.5 với hàm trội $\Lambda(a)=(1+2\theta_0a)e^{-\theta_0a/2}$ trên $U=(\theta_0/2,2\theta_0)$, $\int\Lambda=10/\theta_0$. $J(\theta)=1-e^{-\theta}$, $J'(1)=e^{-1}\approx0{,}3679$. Theo gradient log: $\int_0^1(1-a)e^{-a}da=(1-e^{-1})-(1-2e^{-1})=e^{-1}$. Đối lập với Ví dụ 10.3 (giá di chuyển). Kiểm bằng `ex10/f101.py`:
   - sai phân hữu hạn $0{,}3678794412$;
   - `scipy.integrate.quad` cho $0{,}3678794412$;
   - $\max_{\theta\in[1/2,2],\,a\in(0,60]}\lvert\partial_\theta p_\theta(a)\rvert/\Lambda(a)=0{,}9999975\le1$;
   - $\int\Lambda=10{,}0$;
   - Monte Carlo $10^6$ mẫu: $0{,}36835$ (sai số chuẩn $0{,}00036$).

   Dòng "Mức độ/Mục tiêu" của 10.1 thêm "chứng minh, kiểm tra giả thiết" và "kiểm điều kiện đổi chỗ đạo hàm và kì vọng". §11 của ghi chú đã ghi 10.1 đo mục tiêu 2, 3, nên không sửa.
6. T2: năm lời giải không còn dựa vào gợi ý.
   - 10.1(e) Bước 1 tự nêu đạo hàm của $\pi(1-\pi)$.
   - 10.2(a) Bước 3 tự nêu đạo hàm của chính sách bảng.
   - 10.3(b) Bước 4 tính nghiệm $\frac{34\pm\sqrt{292}}{48}$.
   - 10.3(d) Bước 2 dẫn "đoạn sau Định nghĩa 05.2".
   - 10.6(b) Bước 3 dẫn Phụ lục C và viết công thức của $L_A+L_B$.

   Thêm một chỗ: 10.4(c) Bước 2 trước đó dẫn "(Gợi ý 2)"; nay liệt kê bảy ô.
7. T3: "Kiểm tra lại" của 10.7 thay bằng phép kiểm miền $[0,6]$ so với $[0,4]$ của Ví dụ 10.12 (tỉ số bán kính $1{,}5$).
8. Nhẹ:
   - N1: dòng "Mức độ" của 10.1, 10.7, 10.8. 10.3 đo "mục tiêu học tập 1 và 5".
   - N2: Gợi ý 1 của 10.8(b) không nêu tên bất đẳng thức Markov; tên đó chuyển sang Gợi ý 2. Gợi ý 2 của 10.5(c) chỉ cho đạo hàm của hàm mục tiêu phát lại.
   - N3: tiếng Anh ở đoạn mở: agent, episode, score function, evaluation matrix, backward/forward transfer, forgetting measure.
   - N4: dòng mục tiêu 10.2.
   - N5: "Suy ra rằng".
   - N7: Ví dụ 10.4, Bước 1.
   - N8: "điểm so sánh" ở 10.3(c)(iii); "điểm cực tiểu của $J$".
   - N9: cắt câu "Trực tiếp: …" ở 10.1(c) Bước 4; 10.1(d) Bước 2 ghi hai phép tính.
   - N10, N11: cắt các câu chốt.
   - N12: 10.6(a) "ước lượng thấp hơn giá trị tổng thể". Vế "cùng số cấu hình" bỏ; mục chỉ giữ "cùng quy tắc", và Hậu quả nêu lợi thế của phương pháp có nhiều siêu tham số.
   - N13: "Kiểm tra lại" của 10.6 so sai số chuẩn coi độc lập ở cặp $0$–$5$: $\sqrt{0{,}051^2+0{,}132^2}/4{,}472\approx0{,}0316$.
   - N14: "Ý (a) là một phép …".
   - N15: đoạn cuối $489$ vòng; "không quá $107{,}97$ (làm tròn lên)".
   - N16: tên 10.9 "(Tùy chọn: mẹo nhân đôi; UML Bài tập 21.4)".
   - N17: ", tức cận".
   - N18, N19: dòng mục tiêu 10.5, 10.9.
9. Ngoại lệ phạm vi: §11 của `lecture-note.md` sửa đúng hai dòng (10.3 "mục tiêu 1, 5"; 10.9 "(Tùy chọn: mẹo nhân đôi; UML Bài tập 21.4)"). `git diff` của ghi chú chỉ có hai dòng này; `forward_refs.py` 0.

**Không áp dụng hoặc áp dụng một phần (lý do).**

- N12, vế "chuyển ý cùng số cấu hình vào Hậu quả": để giữ trần chữ, Hậu quả chỉ nêu lợi thế của phương pháp có nhiều siêu tham số hơn.

**Cắt thêm để giữ trần 10 000** (sau các mục trên, tệp lên 10 258 tiếng):
- 10.1(c) Bước 5 rút gọn.
- 10.2(a) Bước 2 bỏ câu nối Hệ quả 10.8.
- 10.3: bỏ gợi ý (c)(i) nhắc Bài tập 10.1(e); bỏ vế "$\hat g_\theta$ là ước lượng tính tại $\theta$".
- 10.4: bỏ câu kiểm Ví dụ 10.13 trong "Kiểm tra lại"; Bước 1 rút gọn.
- 10.6: Gợi ý 2 (b)(i) không cho sẵn công thức; (c) viết thành một đoạn; "Ngân sách bộ nhớ" rút Hậu quả.
- 10.7: bỏ yêu cầu phụ "một thay đổi làm (T1) đúng hay hỏng" (không có trong dàn ý) và hai đoạn trả lời.
- 10.8(c) Bước 3 bỏ câu đầu.
- 10.9(a) Bước 4 bỏ câu thứ ba.

Không cắt bước tính, số liệu hay lập luận được người rà yêu cầu.

**Kiểm tra sau sửa.**
- `sync` và `--check` OK (20 tệp).
- 0 khoảng trắng cuối dòng (bài tập và ghi chú).
- 36 khối mở, 36 khối đóng.
- 9 961 tiếng.
- Tệp kết thúc bằng một ký tự xuống dòng.
- `forward_refs.py` ghi chú Bài 10: 0.
- Viewer qua HTTP (cổng 8786, đã tắt), 27 `details` mở, ở 390×844 và 1600×900: 1 245 công thức, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 tràn. Lần đo đầu có một công thức mới của 10.1(f) tràn; đã tách.
- Ảnh `ex10/shot_390_103.png` (ý (f)), `ex10/shot_390.png`, `ex10/shot_1600.png`.

### 8.1. Sửa theo `reviews/13-kiem-lai-su-pham-bai-tap.md` và `reviews/12-kiem-lai-toan-bai-tap.md` (2026-11-01)

Bản trước khi sửa: scratchpad `ex10/ex_before_fix2.md`; script `ex10/fix2.py`, `ex10/cut2.py`. Áp dụng M1–M6 theo câu đề xuất, không sửa gì khác:
- **M1:** 10.4(c) Bước 1 viết lại; nêu rõ các đại lượng được điều kiện hóa độc lập với mẫu kiểm tra (Định nghĩa 10.10).
- **M2:** câu cuối 10.4(c) Bước 3 theo người rà toán: xác suất có điều kiện ít nhất $0{,}95$ với mọi dữ liệu huấn luyện, nên xác suất không điều kiện, theo cả dữ liệu huấn luyện và mẫu kiểm tra, cũng ít nhất $0{,}95$.
- **M3:** Hậu quả ở "Ngân sách bộ nhớ".
- **M4:** vế kết luận của 10.1(c) Bước 5.
- **M5:** $\hat g_\theta(\tau')$ định nghĩa ngay tại chỗ dùng ("ước lượng của Định lý 10.4 tại $\theta$"). Câu tách đôi để tránh hai chữ "là" liền nhau.
- **M6:** "với cùng quy tắc"; "(theo giả thiết, $\lVert w_1-u\rVert\le R$)"; 10.6(c) tách thành hai câu.

Sau sửa, tệp lên 10 030 tiếng. Tôi cắt năm câu và vế thừa, không cắt bước nào:
- 10.1(b) Bước 3: vế "như Định lý 10.4 bảo đảm";
- 10.3(b) Bước 4: vế "nhỏ hơn cận chung $3$";
- 10.5(a) Bước 2: câu "Bảng ghi cả ba hệ số";
- 10.6(b) Bước 5: câu "Ở cả hai cách, tỉ số dưới $1$";
- đoạn mở: câu "Kí hiệu chỉ dùng trong một bài được đặt tên tại chỗ".

Kiểm tra:
- **Tệp:** 9 989 tiếng; `sync` và `--check` OK; 0 khoảng trắng cuối dòng; 36/36 khối; tệp kết thúc bằng một ký tự xuống dòng.
- **Ghi chú Bài 10:** không sửa thêm; `git diff` vẫn chỉ có hai dòng §11.
- **Viewer** (cổng 8786, đã tắt), 390×844 và 1600×900: 1 248 công thức, 0 `.katex-error`, 0 lỗi trang, 0 tràn.
