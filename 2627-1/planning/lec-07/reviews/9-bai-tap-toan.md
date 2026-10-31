# Rà toán bộ bài tập Bài 07 (người rà 2)

Đối tượng: `lec07-ex-frozen.md` (868 dòng). Căn cứ: ghi chú Bài 07 đã duyệt; Bài 02–05 (Định lý 02.14, Bổ đề 03.12, Định nghĩa 04.2, ứng dụng Bài 05); dàn ý §4; `bai-tap-ghi-chu.md`; UML tr. 275, 282–283; bản lời giải tr. 50–51.
Tính toán: `reviews07/r2/ex/ex_nums.py`. Thí nghiệm chạy lại với $m=100,200,400,800$: `reviews07/r2/ex/exp_m{100,200,400,800}.txt`, cùng phần in giá trị chính xác của chuẩn.

## Tổng kết theo mức

| Mức | Số phát hiện |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 0 |
| nhẹ | 4 |

Đã tự giải lại cả 9 bài và mọi ý; tất cả đúng. Lượng từ, giả thiết và chiều bất đẳng thức đều đúng. Mọi số khớp lần chạy lại, trừ hai số làm tròn sai một đơn vị ở chữ số cuối (07.6). Đề UML trung thành với PDF và số bài đúng. Lời giải không chép bản lời giải: 20.3 và 20.4 dùng cùng ý tự nhiên (sắp lại tọa độ, hợp theo $h_1$), nhưng viết và lập luận khác, kết luận "$\le$" kèm lý do, và nêu chỗ cần điểm lặp. Gợi ý đúng hướng.

## Từng bài

| Bài | Kết luận | Ghi chú kiểm |
|---|---|---|
| 07.1 | ✓ | (a) $\operatorname{ReLU}(t)+\operatorname{ReLU}(-t)=\lvert t\rvert$, nên $f_{\theta_{\mathrm{abs}}}=\lvert x_1-x_2\rvert-\tfrac12$. (b) Bốn bất đẳng thức đúng chiều (quy ước $\ge0$ cho nhãn $1$); mâu thuẫn chặt. (c) Trên $s\le0$ cả hai ReLU bằng $0$; miền là dải $\tfrac12\le s\le\tfrac32$; miền thứ hai là hợp hai nửa mặt phẳng; nhãn tại $(\tfrac12,\tfrac12)$ là $1$ và $0$. (d) Tham số đúng, $16$ tham số; đã liệt kê đủ tám điểm. |
| 07.2 | ✓ | (a) Bảng tám bộ dấu đúng; giá trị lớn nhất $0{,}4$. (b) $\{g\}$ thỏa (T5), (M) với $\mathcal G_0=\{g\}$; $0{,}2881$ so với $0{,}0866$ (Hệ quả 02.10(c) dạng một phía), tỉ số $3{,}33$; một lần McDiarmid với $c_i=1/m$ và $\mathbb E\Psi=0$ cho đúng Hệ quả 02.10(c). (c) $\max\{u,v\}=\tfrac{u+v}2+\tfrac{\lvert u-v\rvert}2$; bảng số điểm sai đúng từng ô, tổng $6$; Mệnh đề 07.9(a) khớp. (d) $7/30$; phản ví dụ cho tính bất biến khi dịch đúng. |
| 07.3 | ✓ | (a) Cận trên đúng tách được vì tập tham số là tích; $\mathbb E\lvert\sum\sigma_i\rvert\le\sqrt m$; cận $(BC_x+B_0)/\sqrt m$. (b) Bao hàm qua $\tilde x_i=(x_i,1)$ và tính đơn điệu của $\widehat{\mathfrak R}$ theo tập; so sánh bằng Cauchy–Schwarz trong $\mathbb R^2$. (c) Chỉ Jensen là bất đẳng thức thực sự; $\sqrt{\cdot}$ lõm chặt và mỗi bộ dấu có xác suất dương, nên đẳng thức khi và chỉ khi $Y$ hằng, tức tổng chéo có kì vọng $0$ và mô-men bậc hai $\sum_{i<j}\langle x_i,x_j\rangle^2=0$. Ví dụ $(1,0),(1,1)$: $v_\sigma\in\{\pm(2,1),\pm(0,1)\}$, $0{,}8090B<0{,}8660B$. (d) Hai tập véc-tơ giá trị trùng nhau. (e) Khớp ứng dụng Bài 05 ($m=10^6$, $\lVert x\rVert\le1$, $B=5$); hằng số đúng. "Kiểm tra lại" với $m=1$ đúng. |
| 07.4 | ✓ | (a) Tỉ số lỗi $0{,}501/0{,}023\approx21{,}8$. (b) Định lý 02.14 đúng dạng: $r_m=\sqrt{\ln(2K/\delta)/(2m)}$, $r_m^+=\sqrt{\ln(K/\delta)/(2m)}$; $K=3$; (T4) thỏa. (c) Tách trọn, nên $\mathbb E\min\operatorname{err}_\tau=0$; vế phải $1{,}2881$; $P/m=0{,}005$. Bài chỉ tính vế phải, không khẳng định định lý áp dụng (lớp $\mathcal H_{\sin}$ với "$>0$" không hiển nhiên thỏa (M) qua $\theta$ hữu tỉ, nhưng không cần ở đây). (d) Bước dùng từng giả thiết khớp tiêu đề các bước của chứng minh trong ghi chú; ba tình huống vi phạm đúng. |
| 07.5 | ✓ | (a) Đúng. (b) $\partial F=\tfrac12\sum(f-\tilde y/2)\partial f$. Tại $\Theta_1=b_1=\Theta_2=0$: $a_1=0$, nên đạo hàm theo $\Theta_2$ bằng $0$; đạo hàm theo $b_1$ và $\Theta_1$ chứa $\Theta_2=0$, với mọi quy ước $\operatorname{ReLU}'(0)$ và mọi $\eta$. $\partial F/\partial b_2=2b_2$; $f\equiv0$ cho $h\equiv1$, lỗi $\tfrac12$, $F=\tfrac14$. SGD: chỉ $b_2$ đổi, hàm phân lớp hằng, lỗi $\tfrac12$. (c) $\theta_{\mathrm{swap}}$, $\theta_{\mathrm{mid}}$ đúng; $f_{\mathrm{mid}}=-\operatorname{ReLU}(s-\tfrac12)-\tfrac12$; $F=27/16=1{,}6875$; lỗi 0–1 của trung điểm bằng $\tfrac12$. (d) $\operatorname{opt}_S$ đúng Định nghĩa 04.2; mẫu là $r$-đại diện với mọi $r$. |
| 07.6 | ✓ (số: xem N1) | Lỗi kiểm tra, độ lệch chuẩn, chuẩn trung bình và khoảng, $C_x$ ($1{,}5173$–$1{,}5440$ qua mọi $m$), các tỉ số, cận dưới (làm tròn xuống, đúng cả khi dùng trung bình chính xác), $\alpha=1{,}228$, tỉ số tăng khi $m$ gấp đôi, $4{,}55$, trung bình số hạng Rademacher: đều khớp. (b) Kết luận đúng. Từ $m=100$ đến $400$, hiệu $0{,}0194$ so với sai số chuẩn $0{,}0034$: giảm thật. Từ $400$ đến $800$, hiệu $0{,}0013$ nhỏ hơn sai số chuẩn: không kết luận được (xem N2 về giả thiết độc lập giữa hai nhóm). |
| 07.7 | ✓ | (a) Song ánh với từng $C$, rồi "$\le$" cho hàm tăng trưởng. (b) Phản ví dụ $\Pi=2<4$, đúng từng ô. (c) Trường hợp $m<p+1$: $2^m<e^m\le e^{p+1}\le(em)^{p+1}$. Trường hợp $m\ge p+1$: Bổ đề 03.12(b) với $1\le d\le m$. Quy nạp qua lớp tích với $\mathcal Y=\{0,1\}^{k-1}$ hữu hạn. "Kiểm tra lại": $16$ và $(2e)^4=873{,}6$. Đề (a) trung thành với UML 20.3; (b), (c) do học phần thêm (N3). |
| 07.8 | ✓ | (a) Hợp theo $u\in(\mathcal H_1)_C$, rồi $\lvert(\mathcal H_2)_u\rvert\le\Pi_{\mathcal H_2}(m)$ nhờ định nghĩa cho phép lặp. (b) Đúng: UML lấy max trên họ rỗng khi $\lvert\mathcal X'\rvert<m$. (c) $\Pi_{\mathcal H_{(2)}}\le(em)^{N_1+1}$ vì thu hẹp miền không tăng số cách gán nhãn; $P=100$. Nhỏ nhất $m=1163$: hàm $m\ln2-100(1+\ln m)$ tăng khi $m>144{,}27$, và $e^{100}=2^{144{,}27}>2^{144}$; nên $d\le1162$. Tỉ số $1{,}42$; $0{,}78$. |
| 07.9 | ✓ | (a) Tham số và $3k+1$ tham số đúng; quy nạp trên đoạn đúng; mạng trùng hàm nội suy (kiểm số: sai khác $7\cdot10^{-16}$). (b) $4\alpha(1-\alpha)G/k\le G/k$; $f_\theta\in[-1,1]$. Ví dụ $\lvert x-0{,}1\rvert-0{,}5$: miền giá trị $[-0{,}5;0{,}6]$, sai số $0{,}1$ (đo được $0{,}1$). (c) Khoảng cách tới tâm $\le\sqrt p/k$; $k=10,15,32$; $2^{50}=1{,}126\cdot10^{15}$. (d) Lập luận giới hạn trái đúng; sai số đều ít nhất $\tfrac12$. "Kiểm tra lại": $k=1$, $f=1-\lvert x\rvert$ cho sai số $1$; $\sin(3x)/3$ cho $0{,}014851$. Đề đã ghi rõ phần sửa so với UML 20.1 (sigmoid, $n$ chiều). Ngoài lề: nếu $G=0$ thì $\lceil G/\epsilon\rceil=0<1$ (N4). |

## Bảng số

| Vị trí | Bài viết | Tính được | Khớp? |
|---|---|---|---|
| 104 | $16$ tham số | $3\cdot4+4$ | ✓ |
| 171, 233 | $0{,}4$; $7/30\approx0{,}2333$ | $0{,}4$; $0{,}23333$ | ✓ |
| 187–191 | $\le0{,}2881$; $\le0{,}0866$; $\ln20\approx2{,}9957$; $3{,}33$ | $0{,}288097$; $0{,}086541$; $2{,}995732$; $3{,}329$ | ✓ |
| 207, 225 | $\tfrac14$; tổng $6$ | $0{,}25$; $6$ | ✓ |
| 239 | $\sqrt3/6\approx0{,}2887$ | $0{,}288675$ | ✓ |
| 323–325 | $0{,}06$; $\le0{,}0633$ | $0{,}06$; $0{,}063246$ | ✓ |
| 345–347 | $0{,}8090B$; $0{,}8660B$ | $0{,}809017B$; $0{,}866025B$ | ✓ |
| 357–368 | $0{,}005$; $0{,}01$; $0{,}004074$; $0{,}0141$; $K\approx5{,}0067$; $0{,}001358$; $0{,}0304$ | $0{,}005$; $0{,}01$; $0{,}0040743$; $0{,}0140743$; $5{,}006715$; $0{,}0013581$; $0{,}0303989$ | ✓ (cận làm tròn lên) |
| 411–415, 440 | $\le0{,}1095$; $\ln120\approx4{,}7875$; $\le0{,}1012$ | $0{,}109402$; $4{,}787492$; $0{,}101172$ | ✓ |
| 426 | $1{,}2881$ | $1{,}288097$ | ✓ |
| 511 | $27/16=1{,}6875$ | $1{,}6875$ | ✓ |
| 539–542 | lỗi KT thật $0{,}0340$; $0{,}0230$; $0{,}0147$; $0{,}0134$; hoán vị $0{,}499$; $0{,}501$; $0{,}499$; $0{,}499$ | $0{,}03404$; $0{,}02298$; $0{,}01466$; $0{,}01336$; $0{,}49902$; $0{,}50108$; $0{,}4994$; $0{,}49902$ | ✓ |
| 544 | độ lệch chuẩn $0{,}0099$; $0{,}0074$; $0{,}0040$; $0{,}0050$ | $0{,}009877$; $0{,}007357$; $0{,}004012$; $0{,}004993$ | ✓ |
| 550–553 | thật: $446{,}7$ ($253$–$871$); $915{,}7$ ($351$–$1721$); $2301{,}3$ ($1111$–$3317$); $5744{,}7$ ($3532$–$9250$) | $446{,}7213$ ($252{,}571$–$871{,}462$); $915{,}67$ ($351{,}478$–$1720{,}82$); $2301{,}326$ ($1110{,}995$–$3316{,}578$); $5744{,}704$ ($3532{,}131$–$9249{,}801$) | ✓ |
| 559 | hoán vị $m=100$: $3774{,}3$ ($2731$–$8750$) | $3774{,}2496$ ($2731{,}416$–$8750{,}290$) | ✗ gần nhất là $3774{,}2$ (N1) |
| 560 | $10\,852{,}6$ ($6792$–$14\,052$) | $10\,852{,}6$ ($6791{,}53$–$14\,051{,}9$) | ✓ |
| 561 | $27\,739{,}3$ ($18\,312$–$46\,586$) | $27\,739{,}288$ ($18\,311{,}749$–$46\,585{,}475$) | ✗ đầu trên gần nhất là $46\,585$ (N1) |
| 562 | $125\,453$ ($76\,307$–$316\,483$) | $125\,452{,}66$ ($76\,307{,}07$–$316\,482{,}65$) | ✓ |
| 590–593 | $8{,}45$; $11{,}85$; $12{,}05$; $21{,}84$ | $8{,}4488$; $11{,}8521$; $12{,}0536$; $21{,}8380$ | ✓ |
| 601–604 | $134{,}0$; $194{,}2$; $345{,}1$; $609{,}3$ (làm tròn xuống) | $134{,}016$; $194{,}243$; $345{,}199$; $609{,}310$ | ✓ |
| 608–614 | $12{,}86$; $2{,}554$; $2{,}079$; $\alpha\approx1{,}23$; $2{,}05$; $2{,}51$; $2{,}50$; $m^{0{,}73}$; $4{,}55$ | $12{,}8603$; $2{,}5541$; $2{,}0794$; $1{,}2283$; $2{,}0499$; $2{,}5132$; $2{,}4963$; $0{,}7283$; $4{,}5465$ | ✓ |
| 622 | $0{,}0013$; $0{,}0016$; $\approx0{,}002$; hiệu $0{,}0013$ | $0{,}001269$; $0{,}001579$; $0{,}002026$; $0{,}0013$; ghép cặp theo hạt giống: sai số chuẩn $0{,}00193$, tương quan $0{,}10$ | ✓ |
| 636 | $136{,}5$; $197{,}9$; $352{,}1$; $620{,}1$ | $136{,}549$; $197{,}933$; $352{,}057$; $620{,}07$ | ✓ |
| 533 | $C_x$ $1{,}517$–$1{,}544$ (mọi $m$) | $1{,}5173$–$1{,}5440$ | ✓ |
| 704 | $16$; $(2e)^4\approx874$ | $16$; $873{,}57$ | ✓ |
| 769–780 | $P=100$; $805{,}79>805{,}44$; $805{,}88<806{,}13$; $144{,}3$; $1162$; $11{,}6P$; $1{,}42$; $0{,}78$ | $805{,}790$/$805{,}437$; $805{,}876$/$806{,}130$; $144{,}27$; $1{,}423$; $0{,}775$ | ✓ |
| 843, 845 | $31$ tham số; sai số $0{,}1$ | $3\cdot10+1$; $0{,}1$ | ✓ |
| 855–857 | $10$; $15$ ($14{,}14$); $32$ ($31{,}62$); $2^{50}\approx1{,}13\cdot10^{15}$ | $10$; $15$; $32$; $1{,}1259\cdot10^{15}$ | ✓ |
| 867 | $0{,}0149$ | $0{,}014851$ | ✓ |

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | 559, 590; 561 | Hai số quan sát làm tròn sai một đơn vị ở chữ số cuối, trái quy ước "khoảng quan sát làm tròn gần nhất". | Trung bình chuẩn hoán vị $m=100$ là $3774{,}2496$, nên ra $3774{,}2$ chứ không phải $3774{,}3$. Đầu trên khoảng hoán vị $m=400$ là $46\,585{,}47$, nên ra $46\,585$ chứ không phải $46\,586$. Script in $3774{,}25$ và $46\,585{,}5$ (6 chữ số có nghĩa) nên dễ làm tròn hai lần. | Sửa thành $3774{,}2$ (dòng 559 và 590; tỉ số vẫn $8{,}45$) và $46\,585$ (dòng 561). |
| nhẹ | 622 (Bước 3 của (b)), 580 (Gợi ý 2) | Sai số chuẩn của hiệu coi hai nhóm $m=400$ và $m=800$ độc lập, nhưng hai nhóm dùng chung mười hạt giống $0,\ldots,9$. Hai nhóm không độc lập theo thiết kế (cùng dòng số ngẫu nhiên ở đầu). Kết luận không đổi: ghép cặp theo hạt giống cho sai số chuẩn $0{,}0019$, vẫn lớn hơn hiệu $0{,}0013$; tương quan đo được $0{,}10$. | Thứ tự rút trong script: điểm huấn luyện rồi điểm kiểm tra, cùng `default_rng(seed)` cho mọi $m$. | Thêm nửa câu: "coi hai nhóm như độc lập; ghép cặp theo hạt giống cho sai số chuẩn khoảng $0{,}0019$, cùng kết luận". Hoặc ghi rằng sai số chuẩn chỉ là ước lượng thô. |
| nhẹ | 641–655, 707–718 (tiêu đề 07.7, 07.8) và dòng 11 | Dòng 11 chỉ nói Bài tập 07.9 có phát biểu đã sửa. Trong 07.7 và 07.8, phần (a) trung thành với UML 20.3, 20.4 (với $\Pi$ cho phép lặp, đã nêu ở dòng 11), nhưng các ý (b), (c) do học phần thêm mà đề không ghi. | UML tr. 282: Bài tập 3 và 4 chỉ có bất đẳng thức hàm tăng trưởng. `bai-tap-ghi-chu.md` dòng 13–14 ghi "thêm (b), (c)". | Thêm vào đề mỗi bài một câu: "Phần (a) là UML Bài tập 20.3 (20.4); (b), (c) do học phần thêm." |
| nhẹ | 794, 843 | Câu "$k=\lceil G/\epsilon\rceil$ nơ-ron là đủ" cho $k=0$ khi $G=0$ (hàm hằng), trái giả thiết $k\ge1$ ở dòng 790. | Dòng 790: "số nguyên $k\ge1$". | Viết $k=\max\{1,\lceil G/\epsilon\rceil\}$, hoặc thêm "với $G>0$". |
