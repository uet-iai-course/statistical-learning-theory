# Duyệt deck Bài 06 — Vai 2 `toan-hoc` (độ chính xác toán học, thống nhất với ghi chú)

Bản duyệt: `2627-1/lecture-06-on-dinh-chinh-quy-hoa.html` (55 trang, đóng băng), `img/lec-06/*.svg`. Đối chiếu: `materials/lec-06/lecture-note.md`, `exercises.md`; ghi chú Bài 01 (Ví dụ 01.8), Bài 02 (Bổ đề 02.2), Bài 05 (Định nghĩa 05.6, Định nghĩa 05.10, Hệ quả 05.15) và deck 05 (kỹ thuật "cân hai số hạng"). `deck_lint.py`: 0 phát hiện.

## 1. Tính lại các con số

Mọi số tính bằng Python (`scratchpad/lec-06/rv-toan-hoc/num.py`, `svg.py`); tất cả khớp mặt trang, ghi chú diễn giả, ghi chú bài giảng và `exercises.md`.

| Nội dung | Trang | Giá trị tính lại | Kết quả |
|---|---|---|---|
| Phụ lục D: $\sum_tc_t$, $\sum_tc_t^2$, tỉ số với cận $0{,}1$ | 2-06 | $0{,}95$; $0{,}000578$; $172{,}9$ | khớp ($173$ lần) |
| Chế độ B, $m=4$: $\mathbb E\bar w_T^2$, $\mathbb EL_S$, $\mathbb E\operatorname{opt}_S$, khoảng cách, số hạng giữa | 2-11 | $0{,}2261$; $0{,}7511$; $0{,}0011$; $0{,}4750=\tfrac2m\sum c_t$; $-0{,}2489$ | khớp |
| $\Pr(\bar Y=0)$ | 2-07 (ghi chú diễn giả) | $\binom42/16=0{,}375$ | khớp |
| $T=25\,600$: $\sum c_t$, khoảng cách | 2-11 (ghi chú diễn giả) | $0{,}9875$; $0{,}49375$ | khớp |
| Ridge thay một quan sát, $\lambda=0;1;2;4$ | 3-01, 3-04, 5-05 | $\hat w_S=0{,}7692;0{,}4762;0{,}3448;0{,}2222$; $\hat w_{S^{(4)}}=0{,}1538;0{,}0952;0{,}0690;0{,}0444$; khoảng cách $0{,}6154;0{,}3810;0{,}2759;0{,}1778$; $L_S(\hat w_S)=0{,}2692;0{,}3390;0{,}4156;0{,}5123$ | khớp |
| $304/169$ và cực đại trên $\mathcal Z=[-1,1]^2$ | 4-01 | $(23/13)^2-(15/13)^2=304/169=1{,}7988$; lưới $201\times201$ cho cùng cực đại tại $(1,-1)$ | khớp |
| Ví dụ 06.6, $\lambda=1$: $240/441$, $432/441$, $0{,}3810$, $0{,}1451$, $0{,}7619$; cận $2/\lambda$, $8/\lambda$ | 5-03 | đúng; $0{,}3810=2{,}625\cdot(8/21)^2$ ($L_S$ tự $1{,}625$-lồi mạnh, đúng lời giải thích ở ghi chú diễn giả) | khớp |
| Ví dụ 06.7, $\lambda=0{,}1$: khoảng cách, cận | 5-04 | $1{,}3333;0{,}3333;0{,}0392$; $8;0{,}8;0{,}08$ | khớp |
| Ví dụ 06.8: $2/(\lambda m)$, khoảng cách, cận | 5-03 | $0{,}2$; $0{,}1$; $0{,}2$ | khớp |
| Ví dụ 06.9: $\hat w_{S^{(100)}}$, thay đổi hàm lỗi | 5-04 | $0{,}66;0{,}3976;0{,}0098$; $0{,}0045;0{,}2518;0{,}8695$ | khớp |
| Ví dụ 06.5: $\mathbb E\lvert L_S(h_0)-\tfrac12\rvert$ | 4-06 | $0{,}1230;0{,}0398;0{,}0126$ | khớp |
| Ví dụ 06.12: $(\lambda/(2+\lambda))^2$ | 6-01 | $0{,}0083;0{,}25;0{,}8264$ | khớp |
| Ví dụ 06.10, 06.11 | 6-04 | $\lambda^*=0{,}2$, cận $0{,}2$, $6400$, $1600\to1599$; $40\,000$, $10^4$; $\lambda^*=4\cdot10^{-4}$, $0{,}01=0{,}005+0{,}005$; $5/\sqrt{10^6+1}=0{,}005$ | khớp |
| Nhận xét 06.14: Markov | 6-05 | $64/(0{,}005)^2=2\,560\,000=400\cdot6400$ | khớp |
| Nhận xét 06.15 | 6-05 (ghi chú diễn giả) | $4\sqrt{10^{-3}}=0{,}1265$ | khớp |
| Đường $0{,}02/\lambda+0{,}5\lambda$ | 1-02, 6-04 | cực tiểu $0{,}2$ tại $\lambda=0{,}2$; $Q(0{,}02)=Q(2)=1{,}01$ | khớp |
| Hệ số ổn định $3/4$, $7/16$ (Bài tập 06.2) | 4-07, 4-04, 7-01 | $2/m-1/m^2$: $0{,}75$ ($m=2$), $0{,}4375$ ($m=4$); $0{,}5>7/16$ | khớp |
| Bài tập 06.1(c): độ chệch $-2y/m$ | 2-12 | $\mp0{,}667$ với $y=\pm1$, $m=3$; $8\cdot9=72$ trường hợp | khớp |
| Bài tập 06.2(b1): $0{,}375$, $0{,}125$, $0{,}25$; trung bình thay một $0{,}375-0{,}125$ | 4-07 | đúng; $a+b\in[1/m,2-1/m]$ | khớp |
| Bài tập 06.4(b), (c) | 6-06, 7-04, 7-05 | $1{,}25$; $5{,}05$; $\lambda_0=0{,}2$, $Q(\lambda_0)=0{,}5$, $\lambda^*=0{,}1$, $Q(\lambda^*)=0{,}4$; $\epsilon_{\mathrm{stab}}=0{,}1$; $0{,}2$; số hạng khớp $0{,}2\to0{,}4$ | khớp |
| Bài tập 06.6(a) | 5-05 | $10/29$, $2/29$, $8/29=0{,}2759$, cận $1$ (lỏng $3{,}6$ lần), $L_S=0{,}4156$ | khớp |
| Bài tập 06.10(c) | 3-05 | $2=2$; $-\tfrac12\ge-1$ | khớp |
| Câu tự kiểm tra 3 | 7-06 | $32/160=0{,}2$; $\lambda^*=0{,}4$, cận $0{,}4$ | khớp |

**SVG.**

- **F2 (`danh-doi-khop-on-dinh.svg`).** Trục: $x=80+640\log_{100}(\lambda/0{,}02)$, $y=370-340v/1{,}2$; vạch $0{,}05$; $0{,}1$; $0{,}5$; $1$ đúng vị trí. Ba đường $0{,}02/\lambda$ (nét đứt), $0{,}5\lambda$ (nét chấm), tổng (nét liền đậm), mỗi đường 301 điểm, lệch tối đa $0{,}10$ px so với công thức. Chấm $(0{,}2;0{,}2)$ tại $(400;313{,}3)$ đúng. Nhãn "số hạng khớp" (trái) và "số hạng ổn định" (phải) nằm cạnh đúng đường.
- **F3 (`doi-vai.svg`).** Hàng trên $S$ có $Z_i$ ở vị trí $i$ và ô kiểm tra $Z'$; hàng dưới $S^{(i)}$ có $Z'$ ở vị trí $i$ và ô kiểm tra $Z_i$. Mũi tên từ $Z_i$ (trên, vị trí $i$) tới ô kiểm tra $Z_i$ (dưới), và từ $Z'$ (trên, ô kiểm tra) tới vị trí $i$ (dưới): đúng phép đổi chỗ $(S,Z')\mapsto(S^{(i)},Z_i)$ của Bước 2 chứng minh Định lý 06.10. Chú thích "cùng phân bố khi $Z_1,\ldots,Z_m,Z'$ độc lập cùng phân bố $D$" đúng.
- **Hình 06.1 (tệp của ghi chú).** Kiểm tọa độ: điểm cực tiểu $0{,}7692$; $0{,}1538$ ($\lambda=0$) và $0{,}2222$; $0{,}0444$ ($\lambda=4$) cùng giá trị mục tiêu $0{,}2692$; $0{,}7308$; $0{,}6111$; $0{,}7445$ khớp vị trí điểm vẽ.

## 2. Đối chiếu các phát biểu với ghi chú

| Kết quả | Trang | Điểm kiểm | Kết quả |
|---|---|---|---|
| Hai chế độ lấy mẫu (§1) | 2-01, 2-07, 2-11 | A: $Z_1,Z_2,\ldots$ độc lập cùng phân bố $D$, dùng một lần; B: $S\sim D^m$ theo (T1), chỉ số đều có hoàn lại, độc lập với $S$, $\xi_t=i_t$ | khớp |
| Bổ đề 06.1 | 2-03 | $\ell(\cdot,z)\ge0$ lồi; $\ell(w,\cdot)$ đo được; $L_D<\infty$ trên $\mathbb R^p$; $v$ đo được; $\mathbb E\lVert v(w,Z)\rVert<\infty$ tại $w$; bảo đảm tất định (a), (b) | khớp |
| Hệ quả 06.2 | 2-04, 2-05, 2-06 | năm giả thiết đủ; kì vọng theo $Z_1,\ldots,Z_{T-1}$; $T-1$ quan sát, mỗi quan sát một lần ($1599$); (a), (b), (c); cấp thuật toán; Bổ đề 06.1(b) vào ở bước 1 nhờ $\mathbb E\lVert v\rVert\le G$ (ghi chú diễn giả) | khớp |
| Nhận xét 06.3 | 2-07 | $T=m+1$, cận $RG/\sqrt{m+1}$, $0{,}005$; vòng thứ hai làm hỏng bước 1 | khớp |
| Định nghĩa 06.4 | 2-08 | $\xi$ độc lập với $S$, (T2), hai kì vọng hữu hạn; ba ví dụ $0$; $1$; $0{,}5$ | khớp |
| Mệnh đề 06.5 | 2-09, 2-10 | dạng yếu của (T1); $\xi$ độc lập; hai kì vọng hữu hạn; $u\in W$ cố định; (a) với mọi $(S,\xi)$, (b) theo kì vọng; bước 3 hỏng khi $u$ chọn theo $S$ | khớp |
| Định nghĩa 06.6, Bổ đề 06.7, 06.8 | 3-02, 3-03 | $\lambda>0$ chọn trước; $\hat w_s\in W$; $W$ lồi (06.7), đóng, lồi (06.8); tất định | khớp |
| Định nghĩa 06.9 | 4-01 | với mọi $s$, $i$, $z'$, $z$; kì vọng hữu hạn; $\mathbb E_\xi$ bên trong trị tuyệt đối; mọi $s\in\mathcal Z^m$ kể cả tập có xác suất $0$ | khớp |
| Định lý 06.10 | 4-02 – 4-05 | (T1) dạng đầy đủ; $\xi$ độc lập với $S$; ổn định đều; (T2), không cần bị chặn; $\mathbb E_{S,\xi}L_D<\infty$; trị tuyệt đối của kì vọng; Fubini bước 1, đổi vai bước 2, hữu hạn nhờ ổn định, $\xi$ trước ở bước 4; phản ví dụ bản sao | khớp |
| Kỹ thuật đổi vai | 4-05 | $\mathbb E\Phi(S,Z')=\mathbb E\Phi(S^{(i)},Z_i)$ với $\Phi\ge0$ đo được, $Z_1,\ldots,Z_m,Z'$ độc lập cùng phân bố; đẳng thức trung bình thay một khớp đẳng thức sau chứng minh | khớp |
| Mệnh đề 06.11 | 5-01, 5-02 | $W$ đóng, lồi; $\ell(\cdot,z)$ lồi, không âm trên $W$; (L) với $G$; $\lambda>0$; tất định, không cần $D$; $2G/(\lambda m)$, $2G^2/(\lambda m)$; hai tăng trưởng bậc hai; lập luận một phía cho $4G/(\lambda m)$ | khớp |
| Hệ quả 06.13 | 6-01 – 6-03 | (T1); như Mệnh đề 06.11, $\ell(w,\cdot)$ đo được, $L_D(w_0)<\infty$; $\lambda$ chọn trước; $u$ cố định; kì vọng theo $S$; (a), (b), (c) với $W_B\ne\varnothing$, $\lambda^*=2G/(B\sqrt m)$, $2GB/\sqrt m$, $m\ge4G^2B^2/\epsilon^2$; (T1) dạng đầy đủ vào ở bước 3 | khớp |
| Nhận xét 06.14, 06.15 | 6-05 | Markov với $L_D(\hat w_S)-\inf_WL_D\ge0$, $W$ quả cầu bán kính $B$; chia khối cần hàm lỗi trong $[0,1]$; 06.15 ghi "đọc thêm" | khớp |

## 3. Bảng thống nhất trang → khối ghi chú

| Trang | Khối ghi chú | Kí hiệu, nhãn, số hiệu, số liệu |
|---|---|---|
| 1-01 | đoạn mở, §10 | khớp |
| 1-02 | Kiến thức tiên quyết; Hệ quả 05.15, Định nghĩa 05.6, Mệnh đề 01.7, Định nghĩa 05.18, Định nghĩa 04.2 | khớp |
| 1-03 | Mục tiêu học tập | khớp |
| 1-04 | §4–§10 (năm mạch) | khớp |
| 1-05 | đoạn mở (câu hỏi trung tâm) | khớp |
| 1-06 | Câu hỏi mở đầu | khớp |
| 2-00 | §1–§5 | khớp |
| 2-01 | §1 (mục 1–5), §2 ((T1), (T2)) | khớp |
| 2-02 | Ví dụ 06.1; ứng dụng §3 | khớp |
| 2-03 | §4, Bổ đề 06.1 | khớp |
| 2-04 | Hệ quả 06.2 | khớp |
| 2-05 | Chứng minh Hệ quả 06.2 | khớp |
| 2-06 | Ví dụ 06.2; Phụ lục D | khớp |
| 2-07 | Nhận xét 06.3; §5 đoạn mở; Ví dụ 06.3 Bước 1 | khớp |
| 2-08 | Định nghĩa 06.4 và ba đoạn sau | khớp |
| 2-09 | Mệnh đề 06.5 | khớp; phát hiện N3 |
| 2-10 | Chứng minh Mệnh đề 06.5 | khớp |
| 2-11 | Ví dụ 06.3; Phụ lục D | khớp; phát hiện N2 |
| 2-12 | Bài tập 06.1(c), (d) | khớp |
| 3-00 | §6 | khớp |
| 3-01 | §6 đoạn mở; đoạn sau Định nghĩa 06.6 | khớp; phát hiện N5 |
| 3-02 | Định nghĩa 06.6 | khớp |
| 3-03 | Bổ đề 06.7, 06.8; Phụ lục A | khớp; phát hiện N6 |
| 3-04 | Ví dụ 06.4; Hình 06.1 | khớp |
| 3-05 | Bài tập 06.10(a), (c) | khớp |
| 4-00 | §7 đoạn mở | khớp |
| 4-01 | Định nghĩa 06.9 và ba đoạn sau | khớp; phát hiện N1 |
| 4-02 | đoạn trước Định lý 06.10; câu sau đẳng thức sau chứng minh | khớp |
| 4-03 | Định lý 06.10 | khớp |
| 4-04 | Chứng minh Định lý 06.10; Bài tập 06.2(c) | khớp |
| 4-05 | đoạn trước Định lý 06.10; đẳng thức sau chứng minh; Phụ lục E | khớp |
| 4-06 | Ví dụ 06.5 | khớp |
| 4-07 | Bài tập 06.2(b) | khớp |
| 5-00 | §8 đoạn mở | khớp |
| 5-01 | (L); Mệnh đề 06.11; Nhận xét 06.12 | khớp; phát hiện N9 |
| 5-02 | Chứng minh Mệnh đề 06.11; Phụ lục B | khớp; phát hiện T1 |
| 5-03 | Ví dụ 06.6, 06.8 | khớp |
| 5-04 | Ví dụ 06.7, 06.9 | khớp |
| 5-05 | Bài tập 06.6(a) | khớp |
| 6-00 | §9 | khớp |
| 6-01 | §9 đoạn mở; Ví dụ 06.12 | khớp; phát hiện N8 |
| 6-02 | Hệ quả 06.13 | khớp |
| 6-03 | Chứng minh Hệ quả 06.13; Phụ lục C | khớp |
| 6-04 | Ví dụ 06.10, 06.11 | khớp; phát hiện N10 (hình F2) |
| 6-05 | Nhận xét 06.14, 06.15 | khớp; phát hiện N4 |
| 6-06 | Bài tập 06.4(b) | khớp |
| 7-00 | §10–§13 | khớp |
| 7-01 | Hệ quả 06.2, Mệnh đề 06.5, Định lý 06.10 | khớp; phát hiện N7 |
| 7-02 | Mệnh đề 06.11, Hệ quả 06.13 | khớp |
| 7-03 | §10 | phát hiện T2 |
| 7-04, 7-05 | Bài tập 06.4(c) | khớp |
| 7-06 | Câu hỏi mở đầu; Định lý 06.10; §12 | khớp |
| 7-07 | §11; `exercises.md` | khớp (mỗi bài ở mạch cung cấp kiến thức cuối cùng nó cần) |
| 7-08 | §13; Quan hệ với UML | khớp |

## 4. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L06-5-02 (ghi chú diễn giả) | Cơ chế khi bỏ $\lambda>0$ bị nói ngược: câu gán "không giảm theo $m$" cho độ cong của $L_S$, trong khi độ cong đó giảm như $2/m$ và chính điều này làm cận không giảm. | Deck: "Bỏ $\lambda&gt;0$: bước 1 chỉ còn độ cong của chính $L_S$, có thể không giảm theo $m$." Ghi chú, Ví dụ 06.7 Bước 3: "$L_S(w)=\tfrac1m(w-1)^2$ … là $(2/m)$-lồi mạnh … $\lvert\hat w-\hat w'\rvert\le G=4$, … không giảm theo $m$." | "Bỏ $\lambda&gt;0$: bước 1 chỉ còn độ cong của chính $L_S$, có thể nhỏ cỡ $2/m$ (Ví dụ 06.7), nên cận không giảm theo $m$." |
| trung bình | L06-7-03 | Hai dòng rút gọn bỏ giả thiết. Dòng quan sát mới bỏ cận mô-men $\mathbb E\lVert v\rVert^2\le G^2$, điều kiện $\lVert w_1-u\rVert\le R$ với mọi $u\in W$ và độ dài bước, trong khi $G$, $R$ có mặt trong cận. Dòng Mệnh đề 06.11 bỏ "không âm trên $W$" và gắn "$\lambda&gt;0$ chọn trước" vào hệ số ổn định, vốn tất định. | Deck: "quan sát mới, $\ell$ lồi: $\mathbb EL_D(\bar w_T)-\inf_WL_D\le RG/\sqrt T$"; "$\ell$ lồi, (L), $\lambda&gt;0$ chọn trước: $\epsilon_{\mathrm{stab}}=2G^2/(\lambda m)$". Ghi chú, Hệ quả 06.2 (b) và giả thiết "Cận gradient", "Thuật toán … $\eta=R/(G\sqrt T)$"; Mệnh đề 06.11 "lồi và không âm trên $W$", "tất định". Quy định "Consistency with the note": phát biểu rút gọn không bỏ điều kiện. | "quan sát mới, $\ell$ lồi, $\mathbb E\lVert v\rVert^2\le G^2$, $\lVert w_1-u\rVert\le R$ trên $W$, $\eta=R/(G\sqrt T)$: …"; "$\ell$ lồi, không âm, (L), $\lambda&gt;0$: $\epsilon_{\mathrm{stab}}=2G^2/(\lambda m)$; với $\lambda^*$ chọn trước: …". |
| nhẹ | L06-4-01 (ghi chú diễn giả) | Chiều thay đổi bị đảo: khi thay $z_4$ bằng $z'$ (đi từ $S$ sang $S^{(4)}$), hàm lỗi tại $(1,-1)$ giảm từ $(23/13)^2$ xuống $(15/13)^2$. | Deck: "hàm lỗi tại $(1,-1)$ đổi từ $(15/13)^2$ lên $(23/13)^2$". Tính: $\hat w_S=10/13$ cho $(23/13)^2$, $\hat w_{S^{(4)}}=2/13$ cho $(15/13)^2$. | "hàm lỗi tại $(1,-1)$ đổi từ $(23/13)^2$ xuống $(15/13)^2$". |
| nhẹ | L06-2-11 | Phần (b) của Mệnh đề 06.5 không có điểm so sánh $u$; ghi "(b) với $u=0$" lẫn hai phần. | Deck: "Mệnh đề 06.5(b) với $u=0$: $0{,}4750+0{,}0011=0{,}4761\ge0{,}2261$." Ghi chú, Ví dụ 06.3 Bước 5: "phân tích theo Mệnh đề 06.5 với $u=0$ … Cận (b) của Mệnh đề 06.5 cho $0{,}4750+0{,}0011=0{,}4761\ge0{,}2261$." | "Mệnh đề 06.5(b), $\inf_WL_D=L_D(0)=1$: $0{,}4750+0{,}0011=0{,}4761\ge0{,}2261$." |
| nhẹ | L06-2-09 | "Trực quan." viết như một đẳng thức hai phần; ghi chú có ba số hạng ở (a) và một bất đẳng thức theo kì vọng ở (b). | Deck: "Rủi ro vượt mức gồm phần do đầu ra phụ thuộc $S$ và phần $\operatorname{opt}_S$." Ghi chú, Mệnh đề 06.5(a), (b). | "Theo kì vọng, rủi ro vượt mức không quá phần do đầu ra phụ thuộc $S$ cộng phần $\operatorname{opt}_S$; phần thứ nhất bằng $0$ khi đầu ra cố định." |
| nhẹ | L06-6-05 | Nhắc lại bất đẳng thức Markov dùng chữ $t$, đã là chỉ số vòng lặp trong cùng deck; Bổ đề 02.2 dùng $\alpha$. | Deck: "$V\ge0$, $t&gt;0$ thì $\Pr(V\ge t)\le\mathbb EV/t$." Ghi chú Bài 02, Bổ đề 02.2: "$V\ge0$ hầu chắc chắn, $\mathbb EV&lt;\infty$ và $\alpha&gt;0$ … $\Pr(V\ge\alpha)\le\mathbb EV/\alpha$." | Viết "$V\ge0$, $\alpha&gt;0$: $\Pr(V\ge\alpha)\le\mathbb EV/\alpha$." |
| nhẹ | L06-3-01 (ghi chú diễn giả) | "$w_1$" ở đây là tọa độ, trùng kí hiệu điểm khởi tạo SGD. | Deck: "mọi điểm trên đường thẳng $w_1=1$". Ghi chú §2 và Hệ quả 06.2: $w_1\in W$ là điểm khởi tạo. | "mọi điểm $(1,t)$, tức tọa độ thứ nhất bằng $1$, đều khớp …". |
| nhẹ | L06-3-03 (ghi chú diễn giả) | Phản ví dụ hàm lỗi logistic cần $W=\mathbb R^p$; với $W$ đóng, bị chặn, giá trị nhỏ nhất luôn đạt. | Deck: "Với $\lambda=0$, giá trị nhỏ nhất có thể không đạt, chẳng hạn hàm lỗi logistic trên một tập huấn luyện tách được …". Ghi chú, Phụ lục A, câu sau $\square$: "như hàm lỗi logistic với $W=\mathbb R^p$ …". | Thêm "với $W=\mathbb R^p$". |
| nhẹ | L06-7-01 | Hàng Hệ quả 06.2 không ghi độ dài bước, trong khi cận $RG/\sqrt T$ cần $\eta=R/(G\sqrt T)$; thiếu $u\in W$. | Deck, cột giả thiết: "quan sát mới độc lập; $\ell(\cdot,z)$ lồi; $\mathbb E\lVert v\rVert^2\le G^2$; $W$ đóng, lồi; $\lVert w_1-u\rVert\le R$". Ghi chú, Hệ quả 06.2, giả thiết "Thuật toán". | Thêm "$\eta=R/(G\sqrt T)$" (và "$u\in W$"). |
| nhẹ | L06-6-01 | "Trực quan." nêu chung "$\lambda=0$: hệ số ổn định không giảm theo $m$", trong khi ghi chú chỉ ra điều đó trên ví dụ cụ thể (§7 với thiết lập Ví dụ 06.4, Ví dụ 06.7). | Deck: "$\lambda=0$: hệ số ổn định không giảm theo $m$". Ghi chú §7: "với $\lambda=0$, hệ số không giảm theo $m$" (cho ERM trên $W$ của Ví dụ 06.4); Ví dụ 06.7 "Tóm lại, … ERM ở đây không ổn định đều …". | "$\lambda=0$: hệ số ổn định có thể không giảm theo $m$ (Ví dụ 06.7)". |
| nhẹ | L06-5-01 (ghi chú diễn giả) | Câu về Nhận xét 06.12 không nói cận chặn đại lượng nào và bỏ $W=\mathbb R^p$, (T1). | Deck: "Nhận xét 06.12 (đọc thêm) cho một cận một phía cho hàm lỗi trơn và không âm, không cần (L): $192C_x^2C_y^2/(\lambda m)$ …". Ghi chú, Nhận xét 06.12: "$S\sim D^m$ theo (T1); $W=\mathbb R^p$ … khoảng cách tổng quát hóa kì vọng … không quá $96\beta C_0/(\lambda m)$". | "… cho khoảng cách tổng quát hóa kì vọng một cận một phía khi $W=\mathbb R^p$ và hàm lỗi trơn, không âm, không cần (L): …". |
| nhẹ | L06-6-04 (hình F2) | Nhãn "tổng" đặt ở đoạn $\lambda\approx0{,}02$–$0{,}05$, nơi đường tổng và đường số hạng ổn định cách nhau dưới $0{,}03$ (khoảng $8$ px); chỉ kiểu nét phân biệt được hai đường tại nhãn. | `danh-doi-khop-on-dinh.svg`: nhãn "tổng" tại $(136;143)$; tại $x=136$, tổng $y\approx175$, số hạng ổn định $y\approx180$. | Đặt nhãn "tổng" gần $\lambda\in[0{,}3;0{,}5]$, nơi hai đường cách nhau rõ (tại $\lambda=0{,}2$: $0{,}2$ so với $0{,}1$). |

Không có phát hiện chặn bàn giao hoặc nghiêm trọng. Mọi ý tưởng chứng minh (2-05, 2-10, 4-04, 5-02, 6-03) có các bước đúng, đúng tên bất đẳng thức then chốt (Fubini, đổi vai, tăng trưởng bậc hai, Cauchy–Schwarz, trung bình cộng–trung bình nhân) và giả thiết vào đúng bước như ghi chú; ba phản ví dụ (bước 1 hỏng khi dùng lại quan sát, $u$ chọn theo $S$, các $Z_i$ là bản sao) đúng.

## 5. Đề xuất sửa ghi chú

- **Hệ quả 06.13, giả thiết "Đo được" (nhẹ).** §2 liệt kê giả thiết "Đo được: ánh xạ $s\mapsto\hat w_s$ đo được", và Định lý 06.10 cần $A$ là thuật toán học theo Định nghĩa 05.18 (đo được). Khối Hệ quả 06.13 chỉ ghi "$\ell(w,\cdot)$ đo được", không dẫn giả thiết "Đo được" của §2. Đề xuất thêm nhãn này vào gạch đầu dòng "Hàm lỗi và tập tham số" của Hệ quả 06.13 (deck 6-02 khi đó thêm theo). Deck hiện theo đúng ghi chú.

Ngoài điểm trên, không thấy lỗi hay khoảng trống toán học trong các khối ghi chú mà deck dùng.

## Kết luận

**đạt khi sửa** — 0 chặn bàn giao, 0 nghiêm trọng, 2 trung bình (5-02 ghi chú diễn giả; 7-03), 10 nhẹ.
