# Rà soát 2 — Chính xác toán học, Bài 08 (bản đóng băng `lec08-draft-frozen.md`)

Người rà: người rà 2 (chính xác toán học), chỉ đọc. Phép tính lại: `reviews08/r2/check.py` (đầu ra `check_out.txt`); thí nghiệm chạy lại: `reviews08/r2/exp_eta05.txt`, `reviews08/r2/exp_eta025.txt`. Đối chiếu: ghi chú Bài 01, 05, 06, 07; `ky-hieu.md`; `sources/blueprint.md` (§E, Lecture 8); Hardt–Recht–Singer 2016 (tr. 5, 8–9, 12–13, 18–19, 31).

Không tải `no-ai-slop`: bản rà này chỉ xét toán học và con số; một ghi chú văn phong nằm ở cuối, dành cho người rà 4.

## 1. Tổng kết theo mức

| Mức | Số phát hiện |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 1 |
| nhẹ | 10 |

Mọi kết quả chứng minh lại được, với giả thiết như phát biểu. Mọi con số (ví dụ tay, cận, thí nghiệm) khớp với phép tính lại và với lần chạy lại script; cận trên làm tròn lên, số đo làm tròn gần nhất. Lỗi duy nhất có thực chất là một câu tổng kết ở §9 (và hai câu dẫn ở §5–§6) mâu thuẫn với chứng minh của Mệnh đề 08.5. Chứng minh vẫn đúng.

## 2. Danh sách kết quả

| Kết quả | Đánh giá | Ghi chú |
|---|---|---|
| Định nghĩa 08.3, đoạn sau (đồng bức ⇒ $\beta$-Lipschitz; $\tfrac\beta2\lVert w\rVert^2$ dấu bằng; $-\tfrac12w^2$ không đồng bức) | ✓ | |
| Bổ đề 08.4(a), Phụ lục A (cận trên bậc hai, hàm phụ $q_u$, đổi vai) | ✓ | Tính lồi chỉ ở Bước 2; $v^+$ có thể ra ngoài $W$ nên (S) cần trên $\mathbb R^p$: đúng |
| Bổ đề 08.4(b) (khai triển, hệ số $\eta(2/\beta-\eta)\ge0$ khi $0\le\eta\le2/\beta$) | ✓ | Khớp HRS Lemma 3.7.2 / (A.1) |
| Bổ đề 08.4(c) (hợp với phép chiếu không giãn) | ✓ | Bài 05, đoạn sau Bổ đề 05.8 |
| Mệnh đề 08.5(a) trên từng quỹ đạo; bước khác biệt qua điểm trung gian $\Gamma(w'_t)$; (G) dùng hai lần tại $w'_t\in W$ | ✓ | Xem phát hiện 1 về câu tổng kết ở §9 |
| Mệnh đề 08.5(b) chỉ dùng $\Pr(i_t=i)=1/m$ và tính tuyến tính | ✓ | Không cần độc lập giữa $i_t$ và $\Delta_t$: đúng |
| Định lý 08.6(a) dạng ghép cặp $\mathbb E_\xi\lvert\cdot\rvert$ | ✓ | Lipschitz của hàm lỗi kiểm tra trên $W$ (Mệnh đề 05.5(a), $U=W$), hai điểm $w_{T+1},w'_{T+1}\in W$: đủ |
| Định lý 08.6(b) hiệu hai kì vọng, Định nghĩa 06.9 | ✓ | Ghép cặp giữ phân bố biên; kì vọng hữu hạn vì $\xi$ hữu hạn giá trị |
| Định lý 08.6(c) qua Định lý 06.10; khả tích (Bước 4); chỉ số $\sum_{t=1}^T$ | ✓ | Giả thiết của 06.10 đủ: (T1) đầy đủ, $\xi\perp S$, (T2), $\mathbb EL_D<\infty$. Khớp HRS Thm 3.8 (đổi $\alpha_t\to\eta_t$, $n\to m$, $L\to G$) |
| Hệ quả 08.7 ($\sum_{s=1}^{T-1}(T-s)\eta_s$; bước hằng $G^2\eta(T-1)/m$; khả tích) | ✓ | Đã kiểm hoán đổi tổng bằng số |
| Hệ quả 08.8(a) ghép Mệnh đề 06.5(b) + Hệ quả 08.7 + Định lý 05.14 (oracle như Hệ quả 05.19 Bước 1) | ✓ | Cùng đầu ra $\bar w_T=\frac1T\sum_{t=1}^Tw_t$ (Thuật toán 05.11), cùng $W$, (C) đúng, $L_D<\infty$ trên $W$ (giả thiết của 06.5) được kiểm; điều kiện $\eta\le2/\beta$ chỉ cho số hạng ổn định |
| Hệ quả 08.8(b) ($\eta^*$, giá trị $RG\sqrt{(1+2(T-1)/m)/T}$, $\le RG\sqrt{3/m}$ khi $T=m$, giới hạn $RG\sqrt{2/m}$; luôn lớn hơn $RG/\sqrt{m+1}$) | ✓ | "giảm về" chỉ đúng khi $m>2$ (phát hiện 3). Khớp HRS Prop 5.4 và đoạn $\sqrt3$, $\sqrt2$ (tr. 19) |
| Mệnh đề 08.10 (thừa số $1+\beta\eta_t$; khai triển; tổng hình học $((1+\beta\eta)^T-1)/\beta$; $1+x\le e^x$; $(T/t)^{\beta c}$) | ✓ | Khớp HRS Lemma 3.7.1 |
| Nhận xét 08.11 | ✓ | Đúng giả thiết HRS Thm 3.12: $f\in[0,1]$, $L$-Lipschitz, $\beta$-trơn với mọi $z$, $\alpha_t$ không tăng, $\alpha_t\le c/t$, SGM không chiếu; hằng số $\frac{1+1/(\beta c)}{n-1}(2cL^2)^{1/(\beta c+1)}T^{\beta c/(\beta c+1)}$; lập luận giai đoạn đầu $t_0/n$ (Lemma 3.11) |
| Mệnh đề 08.12, Phụ lục C ($\eta\le1/\beta\Rightarrow1-\beta\eta/2\ge\tfrac12$; hằng số $2(F(w_1)-F_*)/(\eta T)+\beta\eta\sigma^2$) | ✓ | Khớp blueprint 8.3 [O]; giả thiết khả tích nằm trong chứng minh, không trong phát biểu (phát hiện 2) |
| Phụ lục B(i) xáo trộn lại; B(ii) đo được | ✓ | |
| Câu ôn nhanh 1–3; câu hỏi cuối buổi (a)–(d) | ✓ | |
| Ví dụ 08.1–08.10, khối ứng dụng, đoạn Bài 06 (Ví dụ 06.3) | ✓ | Mọi số khớp (bảng §3) |

**Lượng từ, biến lấy kì vọng, (T1), tính đo được.** Mệnh đề 08.5 và Định lý 08.6(a)(b) ghi "với mọi $s,i,z',z$", kì vọng theo $\xi$; (c), Hệ quả 08.7, 08.8 ghi kì vọng theo $(S,\xi)$; (T1) dạng đầy đủ chỉ dùng qua Định lý 06.10; (G) "với mọi $z\in\mathcal Z$" chạy trên mọi quan sát có thể. Tính đo được theo bộ ba ở Phụ lục B(ii) đúng (hàm Carathéodory). Không thấy chỗ nào áp định lý trơn–lồi cho ReLU hay hàm lỗi bản lề; dừng sớm luôn được nói là cực tiểu một cận trên, không phải kết quả đã chứng minh về lỗi kiểm tra (dòng 678, 695, 874). Loại bảo đảm (khoảng cách tổng quát hóa kì vọng, cấp thuật toán; rủi ro vượt mức kì vọng so với $W$; tính dừng) được nêu ở mỗi kết quả, như blueprint §E đòi.

## 3. Bảng số

| Vị trí | Giá trị trong bản nháp | Tính lại | Khớp |
|---|---|---|---|
| Ôn nhanh 1 | $\max g''=\tfrac14$ | $0{,}25$ | ✓ |
| Ôn nhanh 2 | $1{,}5\le3{,}5$ | $1{,}5$; $3{,}5$ | ✓ |
| Ôn nhanh 3 | $1{,}5$; $3367/4096\approx0{,}8220$ | $3/2$; $3367/4096=0{,}82202$ | ✓ |
| Ví dụ 08.1 | $w_1..w_7=0,0,\tfrac12,\tfrac34,\tfrac54,\tfrac74,\tfrac54$; đạo hàm $0,-1,-\tfrac12,-1,-1,1$ | như vậy | ✓ |
| Dòng 193 (không ghép cặp) | $w_2=0$, $w'_2=\tfrac12$ | như vậy | ✓ |
| Ví dụ 08.2 | $w'$: $0,-\tfrac12,0,\tfrac12,0,0$; $\Delta$: $0,1,\tfrac34,\tfrac34,\tfrac74,\tfrac54$ | như vậy | ✓ |
| Dòng 368 ($2G$ chặt) | $\tfrac32$, $\tfrac12$, hiệu $1$ | như vậy | ✓ |
| Ví dụ 08.4 | $\mathbb E\Delta_2=\tfrac14$; nhóm $i_1=4$: $\tfrac12,\tfrac34,1,2$; $\mathbb E\Delta_3=\tfrac{29}{64}\approx0{,}4531$; $\mathbb E\Delta_7=\tfrac{228203}{262144}\approx0{,}8705$ | liệt kê đủ $4^T$ dãy, phân số đúng | ✓ |
| Ví dụ 08.4 Bước 4 | dãy $(2,3,1,4,4,4)$: $w_4=w'_4=\tfrac12$, $\Delta_7=3$ | như vậy | ✓ |
| Ví dụ 08.3 | bảng hệ số giãn $\{\tfrac12,1,\tfrac32\},\{1,1,3\},\{2,2,4\}$ | như vậy | ✓ |
| Ví dụ 08.5 | $0{,}001$; $t/200$; $1$; $100$ | như vậy | ✓ |
| Ví dụ 08.6 Bước 3 | $0{,}5/0{,}0445\approx11{,}2$; $100/0{,}9188\approx108{,}8$ | $11{,}24$; $108{,}84$ | ✓ |
| Dòng 578 (Ví dụ 06.3) | $\beta=2$, $G=4$, cận $39{,}975$; thật $0{,}4750$ | $39{,}975$; Bài 06 ghi $0{,}4750$ | ✓ |
| Ví dụ 08.7 Bước 1 | $5/\sqrt{10001}\le0{,}0500$ | $0{,}049998$ | ✓ |
| Ví dụ 08.7 Bước 2 | $\eta^*\approx0{,}029$; $0{,}0866$; $0{,}0791$; $0{,}0725$; $0{,}0708$ | $0{,}02887$; $0{,}086600$; $0{,}079055$; $0{,}072457$; $0{,}070711$ | ✓ (làm tròn lên) |
| Ví dụ 08.7 Bước 3 | $T^*\approx7071$; $\le0{,}0958$; $0{,}1000$; $0{,}1000$; $0{,}1375$; $0{,}2800$ | $7071{,}07$ (nguyên tốt nhất $7071$); $0{,}095706$; $0{,}099995$; $0{,}099995$; $0{,}137495$; $0{,}279995$ | ✓ |
| Ví dụ 08.8 (cosin) | $w'_2\approx-0{,}0010$; $\Delta_3/\Delta_2\approx1{,}1000$; $\Delta_{21},\Delta_{41},\Delta_{61},\Delta_{81},\Delta_{101}\approx0{,}0061;0{,}0411;0{,}2753;1{,}529;2{,}879$; đầu tiên vượt $0{,}2$: $\Delta_{58}\approx0{,}207$; $\Delta_t\to\pi$ | $-0{,}00099998$; $1{,}10000$; $0{,}006116;0{,}041139;0{,}275281;1{,}52903;2{,}87931$; $\Delta_{58}=0{,}20732$ ($\Delta_{57}=0{,}1886$); $\Delta_{399}=3{,}14159$ | ✓ |
| Dòng 781 | $(1{,}1)^{100}\approx1{,}378\cdot10^4$; $275{,}6$ | $13780{,}6$; $275{,}59$ | ✓ |
| Nhận xét 08.11 | $\le33{,}37$ | $33{,}369$ | ✓ |
| Ví dụ 08.9 | $\eta=1$: $0{,}02$ rồi $0$; $\eta=2$: $0{,}04$ không đổi, $w=\pm\tfrac1{50}$; $\eta=3$: $0{,}06\ldots3{,}84$ | như vậy; $\lvert w_8\rvert=1{,}92>1$ | ✓ |
| Ví dụ 08.10 | $\pm0{,}49$, $0{,}98$; $1{,}49$, $1{,}01$, $0{,}48$ | như vậy | ✓ |
| Dòng 864 (Mệnh đề 08.12) | $\le0{,}0153$ | $0{,}015273$ | ✓ |
| Câu hỏi cuối buổi | $0{,}8$; $\le28{,}19$; $\le0{,}0113$ | $0{,}8$; $28{,}1843$ (tổng thật $28{,}1386$); $0{,}011274$ | ✓ |
| Câu hỏi mở đầu (bảng) | $0{,}618/0{,}662/0{,}045$; $0{,}561/0{,}640/0{,}079$; $0{,}376/0{,}589/0{,}213$; $0{,}243/0{,}662/0{,}419$; $0{,}134/1{,}053/0{,}919$ | script in đúng các số này | ✓ |
| Câu hỏi mở đầu, dòng 25, 693 | lỗi phân lớp $0{,}309;0{,}301;0{,}312$; tỉ số $11$–$109$ | $0{,}3089;0{,}3009;0{,}3118$; $11{,}24$–$108{,}84$ | ✓ |
| Ví dụ 08.6 bảng | $\Delta$ ghép cặp $0{,}142;0{,}233;0{,}873;2{,}219;5{,}458$; không ghép cặp $2{,}99;3{,}83;4{,}90;4{,}82;4{,}00$ | như vậy | ✓ |
| Ví dụ 08.6 | khoảng $1{,}31$–$15{,}08$; đổi nhãn $0{,}015;0{,}016;0{,}022;0{,}026;0{,}034$; khoảng cách $0{,}693$–$1{,}149$ | $1{,}3096$–$15{,}0812$; $0{,}0152;0{,}0159;0{,}0218;0{,}0262;0{,}0339$; $0{,}6930$–$1{,}1494$ | ✓ |
| Phụ lục D | $0{,}603$, $0{,}827$; $0{,}298$, $0{,}650$; $0{,}383$; $0{,}301$–$0{,}312$; $\lVert\nabla L_S\rVert$ $0{,}039\to0{,}004$; $\eta=0{,}25$: $0{,}651$; $0{,}0445\to0{,}045$ | $0{,}6027$, $0{,}8269$; $0{,}2977$, $0{,}6503$; $0{,}3827$; $0{,}3009$–$0{,}3118$; $0{,}0387\to0{,}0042$; $0{,}6511$; $0{,}0445$ (script in $0{,}045$) | ✓ |
| Phụ lục D, chi phí | khoảng $15$ giây | $24{,}5$ giây thời gian thực, chạy song song với lần $\eta=0{,}25$; không đủ để bác bỏ | — |

## 4. Phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | §9 dòng 699; §5 dòng 306; §6 dòng 310 | Câu tổng kết mâu thuẫn với chứng minh. Dòng 699 nói tính lồi, tính trơn và $\eta_t\le2/\beta$ "chỉ đi vào chứng minh qua Bổ đề 08.4, tức qua các bước chung". Dòng 306 nói bổ đề "không nói gì về bước khác biệt", và dòng 310 nói (G) giới hạn phần tăng ở bước khác biệt. Thực ra chứng minh Mệnh đề 08.5 dùng Bổ đề 08.4(b) ở cả bước khác biệt. | Dòng 343–352: "Số hạng thứ nhất không quá $\Delta_t$ theo Bổ đề 08.4(b) với $f=\ell(\cdot,z_i)$; (S) được dùng ở đây"; tiêu đề Bước 2 "(bước khác biệt; (S) và (G))". Mệnh đề 08.10 Bước 2 (dòng 774): "(a) thay cho Bổ đề 08.4 ở cả bước chung và bước khác biệt". | Giữ chứng minh, vì blueprint 8.3 yêu cầu dùng điểm trung gian. Sửa dòng 699 thành: "… chỉ đi vào chứng minh qua Bổ đề 08.4: phần (c) ở bước chung, phần (b) cho điểm trung gian ở bước khác biệt." Sửa dòng 306 thành: "Bổ đề không tự chặn bước khác biệt, vì ở đó hai lần chạy áp dụng hai ánh xạ khác nhau; §6 dùng nó cho một điểm trung gian." Dòng 310: "(G) giới hạn phần chênh do hai quan sát khác nhau." Phương án khác: dùng lập luận "bị chặn" của HRS (Lemma 3.3, 2.5), $\Delta_{t+1}\le\Delta_t+\eta_t\lVert\nabla\ell(w_t,z_i)\rVert+\eta_t\lVert\nabla\ell(w'_t,z')\rVert$, chỉ cần (G); khi đó câu ở §9 đúng nguyên văn. |
| nhẹ | Mệnh đề 08.12 (dòng 848–853); Phụ lục C Bước 4 (dòng 1056) | Giả thiết khả tích $\mathbb E\lvert F(w_t)\rvert<\infty$ chỉ xuất hiện trong chứng minh ("Giả sử …"), không có trong phát biểu. Tính đo được của $g_t$ cũng không được nêu. | Phát biểu chỉ có ba giả thiết; Bước 4 thêm "Giả sử $\mathbb E\lvert F(w_t)\rvert<\infty$". | Thêm vào phần Giả thiết: "$\mathbb E\lvert F(w_t)\rvert<\infty$ với mọi $t$ (đúng khi nguồn ngẫu nhiên hữu hạn giá trị)". Cách khác: suy ra nó từ tính trơn, vì $F_*\le F(w)\le F(w_1)+\langle\nabla F(w_1),w-w_1\rangle+\tfrac\beta2\lVert w-w_1\rVert^2$, cộng quy nạp cho $\mathbb E\lVert w_t-w_1\rVert^2<\infty$ nhờ cận phương sai. |
| nhẹ | Hệ quả 08.8(b), dòng 615 | Câu "giảm về $RG\sqrt{2/m}$ khi $T\to\infty$" không có điều kiện, nhưng hàm chỉ giảm khi $m>2$: hằng khi $m=2$, tăng khi $m=1$. | Dòng 651 ghi "giảm theo $T$ khi $m>2$". Tính lại $(1+2(T-1)/m)/T$ với $m=1$: $1;1{,}5;1{,}67;\ldots$ | "tiến về $RG\sqrt{2/m}$ khi $T\to\infty$ (và giảm theo $T$ khi $m>2$)". |
| nhẹ | Mệnh đề 08.10(a), dòng 740; Bước 1 dòng 772 | Ví dụ đạt hằng số, $\ell=-\tfrac\beta2\lVert w\rVert^2$, vi phạm (G) và $\ell\ge0$, hai giả thiết của chính mệnh đề. | Giả thiết của mệnh đề có "(G) với hằng số $G$"; §1 mục 3 có $\ell\ge0$. | Thêm: "trong lớp thỏa (G), hàm lỗi cosin của Ví dụ 08.8 cho cùng hằng số, vì $\sup_w\lvert1+\eta\cos(w-z)\rvert=1+\eta$ đạt tại $w=z$." |
| nhẹ | Dòng 781 | So vế phải của (c), là cận cho $\mathbb E\Delta$ (khoảng cách tham số), với miền giá trị $[0,2]$ của hàm lỗi. Hai đại lượng khác loại. | Mệnh đề 08.10(c) chặn $\mathbb E\Delta_{T+1}$; cận cho hiệu hàm lỗi là $G$ nhân vế phải. | "…nên cận cho hiệu hàm lỗi, $G$ nhân vế phải của (c), là khoảng $275{,}6$, trong khi hàm lỗi cosin chỉ nhận giá trị trong $[0,2]$." |
| nhẹ | Dòng 693 | Câu "nhỏ nhất ở khoảng $5$ đến $10$ vòng" suy từ bảy thời điểm đo. Cực tiểu thật có thể nằm bất cứ đâu trong khoảng $(1,10)$ vòng. | Script chỉ đo ở $0{,}5;1;5;10;20;50;100$ vòng: $0{,}640$ ở $1$ vòng, $0{,}589$ ở $5$ vòng, $0{,}603$ ở $10$ vòng. | "trong các thời điểm đo, hàm lỗi logistic trên mẫu kiểm tra nhỏ nhất ở $5$ vòng ($0{,}589$; $10$ vòng: $0{,}603$)". |
| nhẹ | §13 dòng 944 | §7 của HRS là "Future Work and Open Problems", không phải thí nghiệm. | HRS tr. 25: mục "7 Future Work and Open Problems"; thí nghiệm ở §6.1–6.4. | "§6 (thí nghiệm trên mạng sâu, là quan sát thực nghiệm), §7 (vấn đề mở)". |
| nhẹ | Ví dụ 08.10 Bước 3, dòng 838 | Hàm lỗi chỉ không khả vi tại tiền kích hoạt bằng $0$ khi trọng số ra tương ứng khác $0$. | Nếu trọng số ra của nơ-ron đó bằng $0$, gấp khúc không ảnh hưởng tới đầu ra. | "tại các tham số có một tiền kích hoạt bằng $0$ và trọng số ra tương ứng khác $0$". |
| nhẹ | Dòng 691 | Câu "Học phần có chứng minh" cho kết quả hạ gradient hội tụ tới nghiệm nội suy chuẩn nhỏ nhất nói quá. Phụ lục D của Bài 07 chỉ có lập luận không gian hàng; tính hội tụ với bước đủ nhỏ được thừa nhận. | Bài 07 dòng 1099: "Đây cũng là giới hạn của hạ gradient … mọi điểm lặp nằm trong không gian hàng … chỉ có một nghiệm nội suy." | "Học phần có lập luận cho hai trường hợp" hoặc "(lập luận ngắn ở Phụ lục D của Bài 07)". |
| nhẹ | Dòng 656 | Ví dụ 05.12 dùng $\lvert w\rvert$, không trơn, nên nằm ngoài (S). Lý do chính đã đủ mà không cần ví dụ: Định lý 05.14 không nói về $w_{T+1}$. | Ví dụ 05.12: $f(w)=\lvert w\rvert$. | Thêm "(ví dụ không trơn)" hoặc chỉ giữ lý do chính. |
| nhẹ | Mệnh đề 08.5, giả thiết "Thuật toán", "Chỉ số"; dòng 368 | Phần Thuật toán buộc rút có hoàn lại (Thuật toán 08.1), nên khẳng định "giữ nguyên khi xáo trộn lại" nằm ngoài phát biểu. Phụ lục B(i) chứng minh đúng, nhưng phát biểu không phủ trường hợp đó. | Dòng 317: "Hai lần chạy ghép cặp của Thuật toán 08.1"; Thuật toán 08.1 bước 1 rút có hoàn lại, độc lập. | "Hai lần chạy ghép cặp theo phép cập nhật của Thuật toán 08.1, với một quy tắc rút chỉ số thỏa $\Pr(i_t=i)=1/m$ với mọi $t$ (chẳng hạn rút đều có hoàn lại)". |

## 5. Ngoài phạm vi (chuyển người rà 4)

- Dòng 23: "Có phải khoảng cách tăng vì mô hình có 100 tham số … không?" là câu hỏi tu từ, thuộc giọng văn bị cấm ở CLAUDE.md. Đề xuất: "Số tham số ($100$) so với cỡ mẫu ($200$) không giải thích sự thay đổi theo số bước, vì …".
