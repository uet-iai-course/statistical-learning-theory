# Bài 05 — Rà lại toán học sau biên tập vòng 1

**Số phát hiện theo mức độ:** chặn bàn giao 0 · nghiêm trọng 0 · trung bình 1 · nhẹ 6.

Đầu vào: `2627-1/materials/lec-05/lecture-note.md` hiện tại (1342 dòng; số dòng dẫn theo tệp này), `lec05-round1.diff`, `planning/lec-05/reviews/0-quyet-dinh.md`, `planning/lec-05/bien-tap-vong-1.md`; đối chiếu Định nghĩa 03.7, 04.1, Nhận xét 01.21 ở các ghi chú trước. Mã tính lại: `py/r05_m3.py` (số mới), `py/r05_tex.py` (cân bằng `$`, ngoặc, `aligned`), `py/r05_render.py` (dựng trang trong Chromium qua HTTP cổng 8797: 1578 phần tử `.katex`, 0 `.katex-error`, 0 lỗi trang). Phạm vi là toán học; không dùng `no-ai-slop`.

## 1. Trạng thái 11 phát hiện của vòng trước

| # | Phát hiện cũ | Trạng thái | Bằng chứng (dòng hiện tại) |
|---|---|---|---|
| 1 | Ví dụ 05.13 "với mọi $T$"; thiếu $W$, $w_1$ | ✓ | 951: $W=[-1,1]$, $w_1=0$, $\lvert\varphi\rvert\le4$, $G=4$; 957: $\mathbb E(\bar w_T-0{,}1)^2\to0$ nên $\mathbb E(\bar w_T-0{,}5)^2\to0{,}16$; 1123: "tiến tới $0{,}16$ khi $T$ tăng, không về $0$". Mô phỏng 300 lần chạy: $0{,}204$ ($T=10$), $0{,}177$ ($T=100$), $0{,}162$ ($T=10^4$). |
| 2 | Bước GD ở Ví dụ 05.6 không nói có chiếu | ✓ | 578: điểm $(0{,}8330;-0{,}7670)$, chuẩn $1{,}1324$, chiếu thành $(0{,}7356;-0{,}6774)$. |
| 3 | Cận trên làm tròn xuống ($4{,}0006$; $0{,}228$; $4-0{,}06112$) | ✓ (một chỗ còn sót, xem bảng §2) | 825, 828: $4{,}000625$ chính xác, "không quá $4<4{,}000625$"; 880, 1117: $0{,}2281$; Phụ lục C (1314) giữ "$\approx0{,}2280$", nhất quán vì có "$\approx$". |
| 4 | Mệnh đề 05.5 đòi tập mở cho cả (a) | ✓ | 310: "$U\subset\mathbb R^p$; ở phần (b), $U$ mở"; 304 áp dụng (a) cho quả cầu đóng. |
| 5 | Tiêu đề Bổ đề 05.12 "rời rạc" | ✓ | 587: "chứng minh cho $\Xi$ hữu hạn". |
| 6 | Ví dụ 05.2 khẳng định đẳng thức dưới vi phân | ✓ | 267: "chứa đoạn … và không chứa $(-1{,}2;-2{,}4)$; Bài tập 05.1 chứng minh nó đúng bằng đoạn này". |
| 7 | Ví dụ 05.11 cận vô ích với $\eta=0{,}15$ | ✓ | 933: "Cận có ích khi $\eta=R/(G\sqrt T)$ … cận là $12{,}81/\sqrt T$"; 935 rút gọn. |
| 8 | "cần" thay cho "đủ" | ✓ | 17, 775, 1032, 1034, 1115, 1117. Dòng 849 "GD và SGD cần cùng số vòng lặp" có "Theo các cận này" đứng trước: chấp nhận. |
| 9 | Giả thiết Mệnh đề 05.20 thiếu khung | ✓ | 1046: "như Định nghĩa 05.10, thỏa (G1); (G2) thay bằng hai cận dưới đây". |
| 10 | "tập mở chứa $W$" sau Định nghĩa 05.1 | ✓ | 173: câu đã bỏ; lý do giữ $F$ hữu hạn trên $\mathbb R^p$ nằm ở 341. |
| 11 | Tính liên tục của $F$; (G1) buộc $F$ lồi trên $W$ | ✓ | 1274: "$F$ lồi và hữu hạn trên $\mathbb R^p$ nên liên tục, do đó $F(w_t)$ đo được"; 739: câu về (G1) (xem thêm hàng cuối bảng §2). |

## 2. Bảng phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | Đoạn nối sau Bổ đề 05.12 (dòng 642) | Câu mới "Gradient ngẫu nhiên không chệch khi biết lịch sử, nên bình phương khoảng cách tới một điểm $u\in W$ giảm theo trung bình, trừ một số hạng tỉ lệ với $\eta^2\lVert g_t\rVert^2$" sai với $u$ bất kì. Từ Mệnh đề 05.13 và Bổ đề 05.12: $\mathbb E[\Delta_{t+1}\mid\mathcal F_{t-1}]\le\Delta_t-2\eta\langle\psi(w_t),w_t-u\rangle+\eta^2\mathbb E[\lVert g_t\rVert^2\mid\mathcal F_{t-1}]$. Số hạng giữa chỉ không dương khi $F(u)\le F(w_t)$, nhờ bất đẳng thức dưới gradient. Với $u=w_t$ thì $\Delta_t=0$, nên khoảng cách không thể giảm. Câu cũng đứng trước chỗ dùng (G1) và tính lồi. | Bản đóng băng (dòng 609) chỉ nói "§7 tìm một đại lượng mà mỗi bước làm giảm theo trung bình", không khẳng định gì cho mọi $u$. | "…nên bình phương khoảng cách tới một điểm $u\in W$ có $F(u)\le F(w_t)$, chẳng hạn một nghiệm tối ưu, không tăng theo trung bình quá một số hạng tỉ lệ với $\eta^2\lVert g_t\rVert^2$." Thêm khoảng 10 tiếng. Cách khác là trở lại câu của bản đóng băng (ngắn hơn). |
| nhẹ | §9, câu đầu (dòng 966) | "Hệ quả 05.15 chặn $F(\bar w_T)$ theo kì vọng; với $F=L_S$, đại lượng đó là $\operatorname{opt}_S$". Đại lượng được chặn là độ chênh $F(\bar w_T)-F_R$, không phải $F(\bar w_T)$; $\operatorname{opt}_S$ là $L_S(\bar w_T)-\inf_WL_S$. | Hệ quả 05.15(b) (dòng 772); §1 mục 7 (dòng 83). | "Hệ quả 05.15 chặn độ chênh tối ưu $F(\bar w_T)-\inf_WF$ theo kì vọng (khi $R$ phủ $W$); với $F=L_S$, đó là $\operatorname{opt}_S(\bar w_T)$ của Định nghĩa 04.2…". Không đổi số chữ đáng kể. |
| nhẹ | Định nghĩa 05.18 (dòng 969) | Câu thêm "trong đó $s\in\mathcal Z^m$ là một mẫu cố định" (R4 #18) mâu thuẫn với điều kiện đo được của ánh xạ $(s,\xi,z)\mapsto\ell(A_m(s;\xi),z)$: ở đây $s$ là một biến của ánh xạ, và tính đo được là theo cả bộ ba. | Định nghĩa 01.4 cũng đòi đo được theo mẫu. | "…đo được theo bộ ba $(s,\xi,z)$, với $s$ chạy trên $\mathcal Z^m$." |
| nhẹ | Đoạn sau Định nghĩa 05.18 (dòng 974) | "$\xi=(\xi_1,\ldots,\xi_{T-1})$ có phân bố $P_\xi^{\otimes(T-1)}$": trong Định nghĩa 05.18, $P_\xi$ là phân bố của *toàn bộ* $\xi$ (có thể là một dãy), còn ở đây $P_\xi$ là phân bố của một lần rút (Định nghĩa 05.10). Cùng một kí hiệu mang hai nghĩa, và câu tự mâu thuẫn nếu đọc theo Định nghĩa 05.18. | Dòng 969 và 479. | "…và $\xi=(\xi_1,\ldots,\xi_{T-1})$ có phân bố tích của $T-1$ lần rút theo phân bố của Định nghĩa 05.10, không phụ thuộc $S$." Hoặc ở Định nghĩa 05.18 đổi phân bố của $\xi$ thành $Q$. |
| nhẹ | Chứng minh Định lý 05.14, câu sau $\square$ (dòng 755) so với dòng 962 và Ví dụ 05.12 (dòng 947) | "Mức sàn sai số (error floor)" được đặt tên cho số hạng $\eta G^2/2$ *của cận* (dòng 755, 947), rồi lại dùng ở dòng 962 cho mức dao động *thực* của điểm lặp cuối khi $F=\tfrac a2w^2$ (mức của Bài tập 05.6, khoảng $\eta\sigma^2/(2(2-\eta a))$). Hai đại lượng khác nhau nhưng cùng một tên, trái quy tắc "một thuật ngữ, một nghĩa". | M3 của quyết định: "mức sàn $\eta G^2/2$ đặt tên một lần". | Dòng 755: "…về mức sàn $\eta G^2/2$ của cận". Dòng 962 giữ "mức sàn sai số (error floor)" cho mức dao động, và đặt thuật ngữ tiếng Anh ở đó. Hoặc ngược lại, miễn mỗi tên chỉ một đại lượng. |
| nhẹ | Ví dụ 05.10, Bước 2 (dòng 896); §11 (dòng 1121) | $RG/\sqrt T=0{,}140625$ (chính xác) in thành $0{,}1406$, tức cận bị làm tròn xuống. Dòng 896 có "$\approx$", nhưng dòng 1121 viết "cận $0{,}1406$". Kết luận không đổi (cận bị vi phạm), chỉ trái quy tắc làm tròn đã quyết định. | $2{,}5\cdot2{,}25/40=0{,}140625$. | In số chính xác $0{,}140625$ ở cả hai chỗ, hoặc "$0{,}1407$". |
| nhẹ | Chứng minh Định lý 05.14, Bước 3 (dòng 739) | "(G1) tại mọi điểm của $W$ buộc $F$ lồi trên $W$" đúng, nhưng được khẳng định mà không có lý do, trong một chứng minh đầy đủ. | Với $w,w'\in W$, $\alpha\in[0,1]$, $\pi=\alpha w+(1-\alpha)w'\in W$: cộng $\alpha$ lần và $1-\alpha$ lần hai bất đẳng thức dưới gradient của $\psi(\pi)$ tại $w$, $w'$ cho $\alpha F(w)+(1-\alpha)F(w')\ge F(\pi)$. | Thêm nửa câu: "(cộng hai bất đẳng thức dưới gradient tại $\alpha w+(1-\alpha)w'\in W$, với trọng số $\alpha$ và $1-\alpha$)". Khoảng 12 tiếng; có thể bù bằng cách bỏ "tại mọi $w$" ở cùng câu. |

## 3. Các khẳng định và chứng minh đã đổi, dựng lại: không có lỗi

- **N1 (hàm điểm số).** Dòng 102–104: $h_w(x)=\langle w,x\rangle$ là hàm điểm số; $h_{w,0}=\mathbb 1[h_w\ge0]$ khớp Định nghĩa 03.7 (lec-03 dòng 243, quy ước $\ge0$); dòng 39 cũng khớp. Hàm lỗi bản lề (245) và logistic (143–147) viết theo $h_w$. Định nghĩa 05.18 (969), dòng 974 và Hệ quả 05.19 (985): $\operatorname{opt}_s(w)=L_s(w)-\inf_{w'\in W}L_s(w')$ đúng là Định nghĩa 04.2 áp dụng cho lớp $\{h_w:w\in W\}$ với $\ell\ge0$; khác biệt của 05.19 không cần chỉnh lại. Nhận xét 01.21 (dòng 1016) tồn tại và đúng chủ đề.
- **M7 (Bổ đề 05.12, trường hợp $\Xi$ hữu hạn).** Đoạn nối (613): mỗi biến cố $\{(\xi_1,\ldots,\xi_{t-1})=k_{1:t-1}\}$ có xác suất $\prod P_\xi(k_s)>0$, và trên đó $\mathbb E[\cdot\mid\mathcal F_{t-1}]$ bằng kì vọng có điều kiện theo biến cố: đúng, vì $\mathcal F_{t-1}$ được sinh bởi phân hoạch hữu hạn này. Bước 2–3 (617–637) với kí hiệu $k_{1:t-1}$ đúng; tổng chạy trên $\Xi^{t-1}$.
- **M8 (Định lý 05.14, Bước 3, và đoạn sau chứng minh).** Bước 3 (735–739) chỉ dùng (G1) và định nghĩa dưới gradient: đúng. "Với $F$ lồi, $\partial F(w)\ne\varnothing$": đúng. "(G1) trên $W$ buộc $F$ lồi trên $W$": đúng (lý do ở bảng §2). Đoạn sau chứng minh (758): với chỉ số chọn đều, độc lập với các lần rút, $\mathbb EF(w_\tau)=\frac1T\sum_t\mathbb EF(w_t)$ nên Bước 5 không cần bất đẳng thức lồi: đúng. Dòng 1127 ("Tính lồi là điều kiện của (G1) và của Bước 5") khớp.
- **M10 (Ví dụ 05.13).** $\lvert\varphi(w,i)\rvert=2\lvert w-y_i\rvert\le4$ trên $[-1,1]$; $L_S=(w-0{,}5)^2+0{,}25$; $\tilde F=(w-0{,}1)^2+0{,}09$; cực tiểu $0{,}1\in W$; Hệ quả 05.15 với $R=1$, $G=4$ cho $\mathbb E\tilde F(\bar w_T)-\min\tilde F\le4/\sqrt T\to0$; hội tụ $L^2$ kéo theo $\mathbb E(\bar w_T-0{,}5)^2\to0{,}16$.
- **Mệnh đề 05.5.** (a) trên $U$ bất kì; (b) cần $U$ mở; lý do ở dòng 341 chấp nhận được.
- **Ví dụ 05.10, Bước 5 và Kết luận (910–919).** $f+f'(1-w)=-s^2+4s+0{,}5>0$ khi và chỉ khi $s>2-\sqrt{4{,}5}$, tức $w>-1{,}1213$ trên nhánh trái; từ $t=26$ điểm lặp nằm trong khoảng này (kiểm lại ở vòng trước: ngưỡng dưới gradient đầy đủ $-1{,}125$, cùng vòng $26$). Kết luận "(G1) hỏng, do $f$ không lồi" đúng: với $w_t\in(-1{,}125;-0{,}125)$, $f$ khả vi tại $w_t$, nên $\partial f(w_t)\subset\{f'(w_t)\}$, vì vậy $\partial f(w_t)=\varnothing$ và không oracle nào thỏa (G1).
- **Ví dụ 05.11, Bước 5 (933).** $W=[-1,1]$, $w_1=1$, $u=0$: $\lVert w_1-u\rVert=1=R$, $RG/\sqrt T=12{,}806/\sqrt T$; in $12{,}81$ là làm tròn lên, đúng chiều.
- **§11 và câu hỏi cuối buổi.** 1115–1127 khớp các ví dụ. Dòng 1170: "Cận chặn sai số tối ưu thực nghiệm $\operatorname{opt}_S$": đúng. Dòng 1181: $L_D(\bar w_{1600})-\min_WL_D\approx0{,}9025$ đúng là sai số ước lượng theo Định nghĩa 04.1 (lec-04 dòng 154: $L_D(h)-\inf_{h'\in\mathcal H}L_D(h')$, cần (T2) và $L_D<\infty$, thỏa với hàm lỗi bình phương ở đây); $\operatorname{opt}_S\approx0{,}0025$. Dòng 1184 đúng.
- **Các thay đổi nhỏ khác.** §1 mục 7 (83): định nghĩa độ chênh tối ưu đúng. Dòng 179: trường hợp $\alpha_t=1/k$. Dòng 360: mô tả trơn/lồi mạnh. Dòng 397: "góc vuông hoặc góc tù". Dòng 420: không giãn kéo theo liên tục. Dòng 489: Cauchy–Schwarz cho $\mathbb E\lVert\varphi\rVert<\infty$. Dòng 646, 680: số hạng $\eta^2\lVert g\rVert^2$ có cả khi $g$ là gradient đúng. Dòng 715, 721, 775, 1016, 1019, 1098, 1111. Phụ lục B với $\Phi$, $\bar\Phi$ (1254–1265): đúng; $\Phi=\lVert\varphi\rVert^2\ge0$ trước, rồi $\Phi=\varphi$ khả tích. Dòng 1319: "thừa số cỡ $\ln T$" đúng theo bậc (tỉ số tiệm cận $(1+H_T)/4$; bằng $2{,}28$ tại $T=1600$).

## 4. Số mới hoặc đã đổi, tính lại

Mọi số khớp (`r05_m3.py`).

| Vị trí | Số in | Giá trị tính lại |
|---|---|---|
| Ví dụ 05.4 (444) | $(-0{,}2929;-0{,}7071)$; $\sqrt{0{,}0858+0{,}5}\approx0{,}7654$; $0{,}0858-0{,}2071=-0{,}1213$ | khớp |
| Ví dụ 05.6, Bước 3 (572–574) | $g_3$: $(-0{,}5858;0)$, $(0;0{,}5858)$, $(-0{,}1697;-0{,}2263)$; điểm $(1;-0{,}7071)$, $(0{,}7071;-1)$, $(0{,}7920;-0{,}5940)$; chuẩn $1{,}2247$, $1{,}2247$, $0{,}9899$; $w_4$ và $L_S$ như cũ | $(-0{,}585786;0)$, $(0;0{,}585786)$, $(-0{,}169706;-0{,}226274)$; chuẩn $1{,}224745$ (hai lần), $0{,}989949$ (không chiếu, đúng); $0{,}071030$; $0{,}102142$; $0{,}069380$ |
| Ví dụ 05.6, Bước 4 (578) | $(0{,}8330;-0{,}7670)$, chuẩn $1{,}1324$, chiếu $(0{,}7356;-0{,}6774)$, $0{,}0614$ | $(0{,}833022;-0{,}767025)$; $1{,}132367$; $(0{,}735647;-0{,}677365)$; $0{,}061359$ |
| Ví dụ 05.7 (686–695) | $0{,}0034$; $0{,}1764$; $0{,}5053-0{,}0034+1\approx1{,}5019$; vế phải không chiếu $1{,}3289$ | $0{,}003437$; $0{,}176434$; $1{,}5019$; $0{,}5053-0{,}1764+1=1{,}3289$ |
| Ví dụ 05.8 (812–828) | hai số hạng với $\gamma$; $4{,}000625$ | đại số đúng; chính xác |
| Ví dụ 05.9 (865) | $\eta=5/\sqrt{10^4}=0{,}05$ | khớp |
| Nhận xét 05.17, §11 | $0{,}2281$ | $0{,}2280087\le0{,}2281$, làm tròn lên |
| Ví dụ 05.10, Bước 3 (902–906) | $\bar w_{1600}+1\approx-0{,}0056$ | $-0{,}005625$ (công thức trung bình cấp số nhân đúng, $1-q=2\eta$) |
| Ví dụ 05.11 (927, 929, 933) | $0{,}7$; $-1{,}7$; $1{,}69$; $12{,}81$ | khớp; $\sqrt{164}=12{,}806$ |
| Ví dụ 05.13 (951, 957) | $G=4$; $0{,}09$; $0{,}16$ | khớp |
| Ví dụ 05.14 (1029, 1034) | $6{,}4\cdot10^5$; $4\cdot10^6$ | khớp |
| Ví dụ 05.15 (1083, 1093) | $T(4)=\lceil475\rceil=475$; $27.136$ | khớp |
| Câu hỏi cuối buổi (1175–1181) | tổng cấp số nhân; $0{,}9875^{1600}\approx1{,}8\cdot10^{-9}$; $0{,}9025$; $0{,}0025$ | $1{,}817\cdot10^{-9}$; khớp |

## 5. Quét lỗi do biên tập

- **LaTeX.** 156 dấu `$$` (chẵn); 1578 đoạn công thức đều cân bằng ngoặc nhọn và `\begin{aligned}`/`\end{aligned}`; không còn dòng nào có số `$` lẻ. Trang dựng trong Chromium không có `.katex-error` hay lỗi trang. Khối nhiều dòng mới ở Bổ đề 05.12, Bước 3 (628–636) dùng `\big\langle`/`\big\rangle` tách qua hai dòng của `aligned`; cách này hợp lệ vì `\big` không cần cặp.
- **Đổi kí hiệu.** Không còn sót: không còn `proj_W(v`, `q(\alpha)`, `c_I`, lịch sử $h$, `H(v)` hay tập $A$ của Mệnh đề 05.5. $\theta$ (điểm bị chiếu) dùng nhất quán ở Định nghĩa 05.7, Bổ đề 05.8, Ví dụ 05.4, Mệnh đề 05.13 Bước 1 và Phụ lục A. $\Phi$, $\bar\Phi$ chỉ ở Phụ lục B. $k_{1:t-1}$ nhất quán ở 613–637. $\gamma$ chỉ ở Ví dụ 05.8. $q_i$ chỉ ở câu ôn nhanh 3. $a'$ ở dòng 41, 46–54, 676 nhất quán. $U$ ở Mệnh đề 05.5. $\Pi$ chỉ còn ở dòng 1199, đúng ngữ cảnh.
- **Một chỗ trùng kí hiệu mới:** $P_\xi$ ở dòng 974 (bảng §2).
