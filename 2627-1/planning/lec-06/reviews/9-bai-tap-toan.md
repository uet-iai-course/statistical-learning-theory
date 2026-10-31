# Rà toán bộ bài tập Bài 06 (R2)

Đối tượng: `lec06-ex-frozen.md` (trùng byte với `2627-1/materials/lec-06/exercises.md`, đã kiểm bằng `diff -q`). Script: `reviews06/r2/ex/ex.py` (liệt kê chính xác bằng `Fraction` cho 06.1(c) và 06.2; số thực cho phần còn lại).

**Tổng kết:** `chặn bàn giao` 0; `nghiêm trọng` 0; `trung bình` 0; `nhẹ` 2. Tôi tự giải lại 11 bài và mọi ý: các lời giải đúng, lượng từ, giả thiết và chiều bất đẳng thức đều đúng chỗ. Mọi con số khớp, trừ hai cận ở 06.5(c) bị làm tròn xuống. Đề UML trung thành với PDF, số bài đúng. Lời giải không chép bản lời giải UML. Gợi ý đúng và không dẫn sai hướng.

## 1. Từng bài

| Bài | Kết luận | Ghi chú |
|---|---|---|
| 06.1 (a)–(d) | ✓ | (a): $w_t$ đo được theo $\mathcal F_{t-1}$, $Z_t$ độc lập với $\mathcal F_{t-1}$, lấy kì vọng khi cố định $w_t$, rồi Bổ đề 06.1(b) (cần $\mathbb E\lVert v\rVert\le G$, đã nêu). (b): Mệnh đề 05.3(b). (c): $w_2=2\eta Y_{i_1}\in W$ vì $2\eta<1$. Điều kiện theo $w_2$ tương đương điều kiện theo $Y_{i_1}$ vì $\eta>0$. $\mathbb E[Y_{i_2}\mid Y_{i_1}=y]=y/m$, nên độ chệch là $-2y/m$, bằng $\mp\tfrac23$ khi $m=3$. Liệt kê 72 trường hợp cho đúng $-\tfrac23$. (d): độ chệch $0$ nhờ tính độc lập. |
| 06.2 (a)–(d) | ✓ (một ghi chú nhẹ ở (c)) | (a): phép đổi chỗ $\tau_i$ là song ánh giữ trọng số tích; không cần khả tích vì mọi tổng hữu hạn. (b1): $3/8$, $1/8$, khoảng cách $1/4=2\sigma^2/m$, trung bình thay một $1/4$, tất cả chính xác. (b2): cận $\lvert a-b\rvert\,\lvert a+b-2z\rvert\le\tfrac1m(2-\tfrac1m)$ đúng; đạt tại $s=0$, $z'=z=1$. Liệt kê $m=2..5$ cho $3/4,5/9,7/16,9/25$. (c): khoảng cách $1/2$, trung bình thay một $1/8$. Phản ví dụ trọng số $((0,0),1)\mapsto((1,0),0)$ đúng. Với $m\ge4$, $0{,}5>2/m-1/m^2$; với $m=3$ thì $5/9>0{,}5$. (d): $1/4$. |
| 06.3 (a)–(d) | ✓ | Phần (a)–(c) dựng lại khớp. Phần (d): $F_{s,1}=1{,}3125w^2-1{,}25w+0{,}75$, hai hiệu $\pm4/21$, chuỗi $0{,}0726\le0{,}1905\le0{,}7619$ và $0{,}1451\le0{,}3810\le0{,}7619$. Cận lỏng $5{,}25$ và $10{,}5$ lần. Độ cong $1{,}625$ của $L_s$ đúng. |
| 06.4 (a)–(d) | ✓ | (b): thừa số $\tfrac12(c+1/c)$ cho $1{,}25$ và $5{,}05$. (c): $\lambda_0=0{,}2$, $Q=0{,}5$; $\lambda^*=0{,}1$, $Q=0{,}4$; tỉ số $1{,}25$ đúng với $c=2$. Kiểm với $B_0=4$ (tức $c=\tfrac12$) cho $0{,}5$. (d): cộng hai bất đẳng thức tối ưu cho $\tfrac{\lambda_2-\lambda_1}2(\lVert\hat w_1\rVert^2-\lVert\hat w_2\rVert^2)\ge0$; Bước 2 suy ra đúng. Chia hàm lỗi cho $4$ để có (T3) là đúng (ứng viên nằm trong $W$). |
| 06.5 (a)–(d) | ✓ (số: phát hiện 1) | (b): $F(\hat w)\le F(0)\le C_y^2$ và $\ell\ge0$ cho $r_\lambda$. Bước thu về quả cầu (nghiệm trên $\mathbb R^p$ nằm trong $K$ nên cũng là nghiệm trên $K$, duy nhất theo Bổ đề 06.8) đúng và áp dụng cho cả $s^{(i)}$. Bậc $\lambda^{-2}$ với hằng $16C_x^4C_y^2/m$ đúng; tỉ số $76{,}6$ cho "khoảng 77 lần". (d): $192/(\lambda m)$ đúng, và hai khác biệt nêu đúng. |
| 06.6 (a)–(c) | ✓ | (a): $10/29$, $2/29$, $8/29$, $L_S=0{,}41558$, cận $1$ lỏng $3{,}625$ lần. (b): giao thức hợp lệ (tập kiểm tra độc lập, nhiều lần lặp, sai số chuẩn, không chọn $\lambda$ trên tập báo cáo); cận $2G_\lambda/(\lambda m)$ chặn được cả khoảng cách lẫn thay đổi dự đoán vì $\lVert x\rVert\le1$. (c): $H_1$ có các phần tử $1{,}925$; $0{,}965$; $2{,}065$ và vế phải $(0{,}4;0{,}3)$ đúng; trị riêng, tỉ số trục, nghiệm và khoảng cách khớp (bảng số). |
| 06.7 (a)–(d) | ✓ | (a): Markov, cần $\Gamma_S\ge0$. (b): khối cỡ $m_{\mathcal H}(\epsilon/4)$, Markov với $(\epsilon/2,\tfrac12)$, $2^{-k}\le\delta/2$; Hệ quả 04.17(a) với $K=k$, $\delta/2$ cho bán kính $\le\epsilon/2$ khi $m_v\ge8\ln(4k/\delta)/\epsilon^2$; (T7) đúng. (c): $\ell\in[0,1]$, $G=1$, $m_{\mathcal H}=\lceil4/\epsilon^2\rceil$ (Hệ quả 06.13(c) với $G=B=1$), học đúng lớp. (d): với hằng số UML được $(1+\sqrt2)\epsilon$ với xác suất $1-3\delta/2$, đúng. |
| 06.8 (a)–(c) | ✓ | (a): chuẩn gradient $\le2\lVert w-x\rVert\le4$; Hệ quả 06.13 áp dụng được ($\ell$ lồi trên $\mathbb R^p$, không âm, (L) trên $W$); cận $8/\sqrt m$. (b): $L_D=\tfrac12\lVert w\rVert^2$; $\mathbf e_j$ cho $\lvert L_S-L_D\rvert=\tfrac12$; xác suất $1-(1-2^{-m})^p$ và cận dưới dùng $1-t\le e^{-t}$ đúng chiều. (c): biến đổi điều kiện tương đương đúng; ngưỡng $17{,}57$; kiểm $m=17$: $0{,}9265<0{,}95$. So với Định lý 03.17 đúng. |
| 06.9 (a)–(b) | ✓ | (a): $\mathbb E\inf L_S\le\inf L_D$ (dạng yếu); tính khả tích của $\mathbb EL_S$ trước khi trừ; đẳng thức đổi vai (dạng đầy đủ). Không cần giả thuyết đạt $\inf$ và không cần $A(S)\in\mathcal H$. (b): $\epsilon_1=2G^2/(\lambda m)$ từ ổn định đều; $\epsilon_2=\lambda B^2/2$ từ Bước 1 của Hệ quả 06.13; tính đo được của $\inf_{W_B}L_S$ qua tập đếm được trù mật (vì $L_S$ lồi hữu hạn nên liên tục) đúng. |
| 06.10 (a)–(c) | ✓ | Định nghĩa 05.6 với cặp $(u,w)$; bất đẳng thức dưới gradient tại $w$; chia cho $\alpha$ rồi cho $\alpha\to0^+$. (b) cộng hai bất đẳng thức. (c): $2\ge2$, $-\tfrac12\ge-1$. |
| 06.11 (a)–(c) | ✓ | (b) với $\ell_\infty$: $w=(1,1)$, $u=(1,-1)$, $f\equiv\tfrac12$ trên đoạn, $\lVert w-u\rVert_\infty=2$, nên điều kiện thành $\tfrac12\le\tfrac12-\tfrac\mu2$, sai; ghi chú về $\ell_1$ đúng. (c): $2G^2/(\lambda m)$; với $\lambda=2\lambda_{\mathrm{UML}}$ được $G^2/(\lambda_{\mathrm{UML}}m)$, bằng một nửa tốc độ của UML; lập luận một phía khớp tốc độ UML. |

## 2. Trung thành với UML, không chép bản lời giải

| Bài | Đề so với UML (tr. 181–183, 201) | Lời giải so với `MLbookSol.pdf` tr. 34–38 |
|---|---|---|
| 06.7 = UML 13.1 | Đúng. (d) nêu hằng số gốc của UML ($m_{\mathcal H}(\epsilon/2)$, $\lceil\log_2(1/\delta)\rceil$, $\ln(4k/\delta)/\epsilon^2$), khớp tr. 181; phần chỉnh hằng số được ghi rõ. | Hằng số đã chỉnh trùng chú thích sửa lỗi 11–12 của bản lời giải, nhưng đó là cách sửa duy nhất tự nhiên. Lập luận viết theo Hệ quả 04.17 với hai biến cố $E_1$, $E_2$; câu chữ khác hẳn. Không chép. |
| 06.8 = UML 13.2 | Đúng ($\mathcal Z=B\times\{0,1\}^d$, phân bố $x$ cố định, $\alpha$ đều). Dùng đúng $\alpha_j=0$; gợi ý của UML in nhầm $\alpha_j=1$. | Bản lời giải dùng tính trơn và cận $\ge\exp(-2^{-m+1}d)$; ta dùng (L) với $G=4$, cận $1-e^{-t}$ và ngưỡng định lượng ở (c). Khác. |
| 06.9 = UML 13.3 | Đúng; dùng $\inf$ thay $\min$ (mạnh hơn). | Bản lời giải giả sử $h^\star$ tồn tại; ta không giả sử. Khác. |
| 06.10 = UML 14.1 | Đúng (Claim 14.10). | Cùng lập luận chuẩn (chia cho $\alpha$, giới hạn), mà UML tự gợi ý ("extend Lemma 13.5"); trình bày theo bốn bước riêng, câu chữ khác. Chấp nhận được. |
| 06.11 = UML 13.4 ý 1–3 | Đúng; ý 2 dùng $\ell_\infty$ (một ví dụ hợp lệ cho "một chuẩn làm mục 1 của Bổ đề 13.5 sai"). | Bản lời giải dùng $\ell_1$; ta dùng $\ell_\infty$ và chỉ nhắc $\ell_1$ một câu. Khác. |

## 3. Bảng số

| Vị trí | Trong bài tập | Tính lại | Khớp? |
|---|---|---|---|
| 06.1(c), kiểm tra | 72 trường hợp; $-\tfrac23$ | 72; $-2/3$ (chính xác) | ✓ |
| 06.2(b1) | 0,375; 0,125; 0,25; 0,25 | 3/8; 1/8; 1/4; 1/4 | ✓ |
| 06.2(b2), kiểm tra | 0,75; 3/4, 5/9, 7/16, 9/25 | như vậy (liệt kê) | ✓ |
| 06.2(c) | 0,5; 0,125; 0,4375 | 1/2; 1/8; 7/16 | ✓ |
| 06.2(d) | 0,25 | 1/4 | ✓ |
| 06.3(d) | 0,1451; 0,3810; 0,7619; 0,0726; ±0,1905; 5 và 10 lần | 0,145125; 0,380952; 0,761905; 0,072562; ±4/21; 5,25; 10,5 | ✓ |
| 06.4(b) | 1,25; 5,05 | 1,25; 5,05 | ✓ |
| 06.4(c) | 0,2; 0,5; 0,1; 0,4; 1,25 | 0,2; 0,5; 0,1; 0,4; 1,25 | ✓ |
| 06.5(a) | 133,3; 13 333; 0,3976; 0,2518 | 133,33; 13 333,3; 0,397590; 0,251786 | ✓ |
| 06.5(c) $\lambda=1$ | 1,4142; 4,8284; 23,314; **0,0466** | 1,414214; 4,828427; 23,3137; **0,046627** | làm tròn xuống (phát hiện 1) |
| 06.5(c) $\lambda=0{,}1$ | 4,4721; 10,944; 119,78; **2,3955** | 4,472136; 10,944272; 119,7771; **2,395542** | làm tròn xuống (phát hiện 1) |
| 06.5(c) $\lambda=0{,}01$ | 14,142; 30,284; 917,14; 183,43; ~77 lần | 14,142136; 30,284271; 917,1371; 183,4274; 76,57 | ✓ |
| 06.5(d) | 0,008; 0,192; 1,92; 19,2 | như vậy | ✓ |
| 06.6(a) | 0,3448; 0,0690; 0,2759; 3,6 lần; 0,4156 | 0,344828; 0,068966; 0,275862; 3,625; 0,415577 | ✓ |
| 06.6(c) trị riêng | 0,0375; 1,9725; 1,0275; 2,9625 | 0,037464; 1,972536; 1,027464; 2,962536 | ✓ |
| 06.6(c) tỉ số trục | 7,3; 1,7 | 7,256; 1,698 | ✓ |
| 06.6(c) nghiệm $\lambda=0{,}01$ | (1,9012; −1,4276); (3,7145; −3,6198); 2,8449 | (1,901218; −1,427605); (3,714479; −3,619756); 2,844898 | ✓ |
| 06.6(c) nghiệm $\lambda=1$ | (0,1763; 0,0629); (0,2528; −0,0228); 0,1149; ~25 lần | (0,176254; 0,062913); (0,252801; −0,022833); 0,114942; 24,75 | ✓ |
| 06.7(c) $\delta=0{,}05$ | 160 000; $k=6$ (5,32); 6400; 4939,03 → 4940; 43 340; 3,7 lần | 160 000; 6 (5,3219); 6400; 4939,029 → 4940; 43 340; 3,69 | ✓ |
| 06.7(c) $\delta=0{,}001$ | $4\cdot10^8$; $k=11$; 8553,56 → 8554; 78 954 | $4\cdot10^8$; 11 (10,966); 8553,556 → 8554; 78 954 | ✓ |
| 06.7(d), kiểm tra | $\sqrt2\epsilon$; 2,414; 0,03125; 0,0156 | 1,41421; 2,41421; 0,03125; 0,015625 | ✓ |
| 06.8(a) | $8/\sqrt m$; 6400 | 8; 64/0,01 = 6400 | ✓ |
| 06.8(b) | 0,6236; 0,6234; 0,9999 | 0,623576; 0,623397; 0,999943 | ✓ |
| 06.8(c) | 0,05129; 194 957; 17,57; 0,927 | 0,051293; 194 957,3; 17,5728; 0,926544 | ✓ |
| 06.9, kiểm tra | 0,4750; 0,0011; 0,4761; 0,2261 | khớp Ví dụ 06.3 | ✓ |
| 06.10(c) | 2 = 2; −½ ≥ −1 | đúng | ✓ |

## 4. Phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | Bài tập 06.5, lời giải (c), dòng 528–529; (d) Bước 3, dòng 540 | Hai giá trị của cận trên (hệ số ổn định $2G_\lambda^2/(\lambda m)$) bị làm tròn xuống, trái quy tắc "cận trên làm tròn lên". | $2\cdot23{,}3137/1000=0{,}046627$ được ghi $0{,}0466$; $2\cdot119{,}7771/100=2{,}395542$ được ghi $2{,}3955$. | Sửa $0{,}0466\to0{,}0467$ và $2{,}3955\to2{,}3956$ ở dòng 528, 529 và 540 (số tiếng không đổi). Kết luận so sánh ở (d) giữ nguyên. |
| nhẹ | Bài tập 06.2(c), đề dòng 126 và lời giải Bước 1, 4 (dòng 228, 234) | "Khoảng cách tổng quát hóa kì vọng" được Định nghĩa 06.4 định nghĩa với $S\sim D^m$. Ở (c) mẫu gồm các bản sao, không có phân bố $D^m$, nên tên gọi nằm ngoài định nghĩa. Đại lượng được tính, $\mathbb E[L_D(A(S))-L_S(A(S))]$, vẫn đúng. | Định nghĩa 06.4, mục **Mẫu và nguồn ngẫu nhiên**: "$S\sim D^m$". | Ở lần dùng đầu trong (c) (dòng 126), thay "tính khoảng cách tổng quát hóa kì vọng" bằng "tính $\mathbb E[L_D(A(S))-L_S(A(S))]$" (thêm khoảng 0 tiếng). Ở dòng 228 và 234 giữ tên, vì đề đã nêu đại lượng. Nếu muốn giữ nguyên câu chữ, có thể bỏ qua. |
