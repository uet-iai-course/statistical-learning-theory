Số phát hiện: chặn bàn giao 0 · nghiêm trọng 0 · trung bình 4 · nhẹ 13.

# Rà soát toán học — Bài tập Bài 04 (bản đóng băng `lec04-ex-frozen.md`)

Người rà soát: vai trò độc lập về độ chính xác toán học, chỉ đọc. Đầu vào: `lec04-ex-frozen.md` (dẫn theo số dòng), ghi chú Bài 04 và các ghi chú, bài tập Bài 01–03 được dẫn, `ky-hieu.md`, UML tr. 66, 97–98, 154–155, `MLbookSol.pdf` tr. 10, 20–22, 31–32 (mở sau khi đã kiểm lời giải của từng bài). Mọi con số tính lại bằng Python trong `rev04/m9/num*.py` (scratchpad). Phần văn phong dùng `no-ai-slop` chế độ Detect.

Kết luận chung: mọi lời giải đúng về toán ở mức chặn bàn giao và nghiêm trọng; mọi khối được dẫn (Định nghĩa 01.12, Ví dụ 01.2/01.5/01.10, §6 Bài 02, Định lý 02.14, Hệ quả 02.10/02.16, Bài tập 02.6/02.11, Bài tập 03.2(b)/03.9, Định lý 03.15/03.17, Hệ quả 03.16, Nhận xét 03.14, Ví dụ 03.6, và các khối 04.1–04.18, Phụ lục A, C, D của Bài 04) tồn tại và nói đúng điều bài tập dùng. Không có kết quả cho hàm lỗi bị chặn bị chuyển sang hàm lỗi bình phương mà thiếu giả thiết cắt (04.2 là đẳng thức kì vọng, 04.6 dẫn đúng Nhận xét 04.18). Bài tập 04.11(d) nói rõ được dùng Định lý 04.16(a). Không thấy lời giải chép hay diễn lại sát bản lời giải UML; chỗ gần nhất là lựa chọn $\lvert\mathcal H_i\rvert=2^i$ ở 04.13 (dòng 13 của bảng).

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 04.3(d), Lời giải Bước 2, dòng 341 | Khẳng định "mọi số hạng phạt đúng với xác suất $1$ cho mọi $D$ không nhỏ hơn $1$" chỉ đúng với hàm lỗi 0–1 (hoặc hàm lỗi nhận cả hai giá trị $0$ và $1$). Bài đặt hàm lỗi tổng quát thỏa (T2), (T3) ở (c); với một hàm lỗi hằng $\tfrac12$ chẳng hạn, độ lệch luôn bằng $0$ và số hạng phạt $0$ hợp lệ với xác suất $1$. Phép dựng "một phân bố dưới đó $h$ sai với xác suất $p$" cũng cần nhãn nhị phân. | Dòng 253 ("hàm lỗi thỏa (T2), (T3)"); dòng 341 ("$h$ sai với xác suất $p\in(0,1)$", "$L_S(h)=1$"). | Thêm "Với hàm lỗi 0–1" ở đầu Bước 2 (hoặc ở đề (d)); ghi: với hàm lỗi tổng quát, $\mathrm{pen}_{k_0}=1$ luôn hợp lệ theo (T3), và không có cận dưới chung. Bài tập 04.8(b) dùng kết quả này trong phân lớp nhị phân, nên vẫn đúng. |
| trung bình | 04.11, tiêu đề dòng 856, đề dòng 860–870 | UML Bài tập 7.5 có năm ý; bài bỏ ý 1–2 (chứng minh điều kiện cần, tức Định lý 04.16(a)) và gộp ý 3 với ý 5, thu hẹp ý 3 từ "lớp tách trọn một tập vô hạn" về lớp $\mathcal M_{\mathcal X}$ các hàm đo được, mà không nói ra. Dàn ý ghi tiêu đề "UML Bài tập 7.5, ý 4; ý 3 là thử thách"; bản phát hành chỉ ghi "UML Bài tập 7.5". | UML tr. 98, ý 1–5; `outline.md` dòng 240; đề 04.11(d) dòng 869. | Đổi tiêu đề thành "…; UML Bài tập 7.5, ý 3–5" và thêm một câu trong dòng **Mục tiêu.** hoặc đầu đề: "Ý 1–2 của UML là Định lý 04.16(a), phác thảo ở Phụ lục D của ghi chú; (d) gộp ý 3 và ý 5 cho lớp các hàm đo được." |
| trung bình | 04.6, Lời giải "Bậc được chọn", dòng 586 | "quy tắc 1 đạt rủi ro thực nghiệm nhỏ nhất tại bậc $15$ trên mọi mẫu …; một kết quả khác là lỗi lập trình hoặc lỗi số" quá mạnh. Lồng nhau chỉ cho $L_S(\hat f^{(15)})\le L_S(\hat f^{(j)})$; khi có bằng nhau, bậc được chọn phụ thuộc quy tắc chọn. Bằng nhau xảy ra chắc chắn khi $m\le16$ (mọi bậc $\ge m-1$ nội suy, $L_S=0$) và có thể xảy ra với nhiễu rời rạc. Học viên tự chọn $m$ và phân bố nhiễu (dòng 552), nên một bảng có bậc nhỏ hơn $15$ không nhất thiết là lỗi. | Ví dụ 04.1 Bước 2 chỉ chứng minh "không tăng"; Bước 3 cho thấy nội suy khi số điểm bằng số hệ số. | Viết: "Các lớp lồng nhau, nên bậc $15$ luôn đạt rủi ro thực nghiệm nhỏ nhất (Ví dụ 04.1); khi $m>16$, các đầu vào đôi một khác nhau và nhiễu có mật độ, nó là nghiệm duy nhất hầu chắc chắn, nên quy tắc 1 chọn bậc $15$; với $m\le16$ cần ghi quy tắc chọn khi bằng nhau." |
| trung bình | 04.6, Lời giải "Kết luận", dòng 589 | Lý do "số hạng phạt của quy tắc 2 không phải một bán kính hội tụ đều (Bài tập 04.4(d))" không được chứng minh và dẫn sai chỗ. Bài tập 04.4(d) xét một số hạng phạt tùy ý trên một lớp cụ thể với hàm lỗi 0–1; nó không nói gì về số hạng phạt mà học viên chọn cho hồi quy đa thức. Lý do đúng là Định nghĩa 04.8 và Định lý 04.11 cần (T3), mà hàm lỗi bình phương không thỏa. | Định nghĩa 04.8 dòng 518 của ghi chú ("hàm lỗi $\ell$ thỏa (T2), (T3)"); Định lý 04.11 giả thiết **Hàm lỗi.** | Thay bằng: "còn quy tắc 2 chỉ có bảo đảm của Định lý 04.11 khi hàm lỗi đã cắt nằm trong một đoạn bị chặn và số hạng phạt là bán kính hội tụ đều của lớp đã cắt (Định nghĩa 04.8); một số hạng phạt chọn tùy ý không có bảo đảm này (so với Bài tập 04.4(d))." |
| nhẹ | 04.4(d), Lời giải Bước 1–2, dòng 434–443; Gợi ý 2 dòng 369 | Nghiệm ERM trên $\mathcal H_2$ không duy nhất: mọi $\mathbb 1_F$ với $F$ hữu hạn, $F\cap\{X_1,\ldots,X_m\}=F_+$ (thêm điểm ngoài mẫu) đều có $L_S=0$. Đề hỏi "hàm nào"; lời giải chỉ nêu $\mathbb 1_{F_+}$. Kết luận về rủi ro không đổi vì mọi tập hữu hạn có xác suất $0$. | Định nghĩa của $\mathcal H_2$ dòng 361. | Thêm: "SRM chọn một $\mathbb 1_F$ với $F$ chứa đúng các đầu vào nhãn $1$ của mẫu, chẳng hạn $\mathbb 1_{F_+}$; mọi hàm như vậy có $L_D=0{,}8$." |
| nhẹ | 04.3(d), Lời giải Bước 2, dòng 341 | "Để giữ biến cố của bổ đề, cần $\Pr(B_{k_0})=0$" chỉ đúng khi giữ nguyên Bước 2 ($\Pr(B_k)\le\delta q_k$); nếu các trọng số khác có tổng nhỏ hơn hẳn $1$, phần dư cho phép $\Pr(B_{k_0})>0$. | Bước 2–3 của chứng minh Bổ đề 04.9. | "Để Bước 2 vẫn đúng tại $k_0$, tức $\Pr(B_{k_0})\le\delta q_{k_0}=0$, cần …". |
| nhẹ | 04.13, đề dòng 973 | Đề UML 11.2 không cho $\lvert\mathcal H_i\rvert=2^i$; đây là giả thiết thêm để tính số (dàn ý ghi "phần định lượng do học phần đặt"), trùng lựa chọn của bản lời giải UML (tr. 31). Đề không nói đây là phần thêm. | UML tr. 154–155; MLbookSol tr. 31; `outline.md` dòng 242. | Thêm một mệnh đề trong đề: "Để so sánh bằng số, học phần thêm giả thiết $\lvert\mathcal H_i\rvert=2^i$; đề UML chỉ yêu cầu mô tả các trường hợp." |
| nhẹ | 04.7(c) dòng 658, Kiểm tra lại dòng 663; 04.13 Kiểm tra lại dòng 1050 | Làm tròn xuống ở số dùng làm cận trên: $2\cdot0{,}269940=0{,}53988$ in $0{,}5398$ (nên là $0{,}5399$); hiệu tương ứng $0{,}16831$ in $0{,}1682$ (nên $0{,}1683$); cách 1 với $k=1$: $0{,}031860$ in $0{,}0318$ (nên $0{,}0319$). | Danh sách số dưới đây. | Sửa ba số. |
| nhẹ | 04.7(b), dòng 633–647 | Tại $m=10^3$, $2\rho^{(4)}\approx1{,}031$ và $2\rho^{(10)}\approx1{,}468$, nên cả hai cận rủi ro vượt mức lớn hơn $1$ và không cho thông tin; ngưỡng $0{,}4369$ so hai cận vô nghĩa. Lời giải không ghi điều này. | Ví dụ 03.7 của Bài 03 ghi rõ ô lớn hơn $1$ "không cho thông tin". | Thêm ở Bước 3: "Với $10^3$ quan sát, cả hai cận lớn hơn $1$; phép so chỉ có nghĩa từ khoảng $m=10^4$." |
| nhẹ | 04.10(a) Bước 2 dòng 819; (b) Bước 1 dòng 823 | Kí hiệu $L=2m\Phi(h_0)^2-\ln(2/\delta)$ trùng chữ với rủi ro $L_S$, $L_D$ trong cùng câu. Bước 1 của (b) áp dụng Bổ đề 04.9 mà không nói danh sách $\{h\}$, $h\in\mathcal H$, đếm được (cần cho (T6)); điều này có vì $\mathrm d$ đơn ánh vào tập đếm được $\{0,1\}^*$. | (T6) dòng 551 của ghi chú: "hữu hạn hoặc đếm được". | Đổi $L$ thành $B_0$; thêm "Vì $\mathrm d$ đơn ánh vào $\{0,1\}^*$, $\mathcal H$ đếm được, nên các lớp $\{h\}$ lập thành một danh sách đếm được cố định trước mẫu." |
| nhẹ | 04.9, đề dòng 706 và toàn bài | Bài dùng $n(h)$, $q_n$ của UML; ghi chú (Hệ quả 04.15) và `ky-hieu.md` dùng $k(h)$ cho cùng khái niệm, và `outline.md` dòng 410 ghi không dùng $n(h)$. Hai kí hiệu cho một nghĩa. | `ky-hieu.md` dòng "$\hat h_k$, $(\hat k,\hat h)$, $k(h)$". | Đổi chỉ số lớp thành $k$, $k(h)=\min\{k:h\in\mathcal H_k\}$, $q_k$; hoặc giữ $n(h)$ và thêm vào đoạn đầu tệp (dòng 7) rằng 04.9 giữ $n(h)$ của UML và $n(h)$ là $k(h)$ của Hệ quả 04.15. |
| nhẹ | 04.13, đề dòng 973 | $k$ là số lớp; `ky-hieu.md` dành $k$ cho chỉ số lớp và $k_{\max}$ cho số lớp. Bài dùng $i$, $j$ làm chỉ số. | `ky-hieu.md` dòng "$k_{\max}$, $\mathrm{pr}_k$". | Viết $k_{\max}$ hoặc thêm một câu: "ở bài này, theo đề UML, $k$ là số lớp". |
| nhẹ | 04.2(a), Lời giải Bước 1 dòng 142 | "mọi tích của ba số hạng khả tích" cần $\mathbb E\bar f(X)^2<\infty$ và $\mathbb Ef^*(X)^2<\infty$, không có sẵn trong Bước 2 của Mệnh đề 04.6 (bản tại một điểm). | Bất đẳng thức Jensen: $\bar f(x)^2\le\mathbb E_S\hat f_S(x)^2$, $f^*(x)^2\le\mathbb E[Y^2\mid X=x]$. | Thêm: "Theo bất đẳng thức Jensen, $\mathbb E\bar f(X)^2\le\mathbb E\hat f_S(X)^2<\infty$ và $\mathbb Ef^*(X)^2\le\mathbb EY^2<\infty$." |
| nhẹ | 04.4, Kiểm tra lại dòng 458 | Dòng chỉ tính lại một ô đã có ở bảng Bước 3, không kiểm tra điều gì mới. | So với dòng 403. | Thay bằng một kiểm tra độc lập, ví dụ: "$\mathrm{pen}_k$ tăng theo $k$ ở cả ba bảng, nên điều kiện đầu vào của Thuật toán 04.12 thỏa", hoặc "tổng tại $k=3$ ở (b) và (c) đều nhỏ hơn tổng tại $k=3$ ở (a), vì $b_3$ hoặc $m$ thay đổi theo chiều làm giảm số hạng phạt". |
| nhẹ | 04.7, đề dòng 601; Lời giải dòng 625 | Chiều VC $4$ và $10$ cần mỗi $I_j$ (ít nhất $I_1$, $I_2$ cho $\mathcal R_2$) có nhiều hơn một điểm; lời giải đặt điều kiện này, đề thì không. | Dòng 625 "khi mỗi $I_j$ có nhiều hơn một điểm". | Thêm vào đề: "mỗi $I_j$ có độ dài dương". |
| nhẹ | 04.12, Gợi ý 2 dòng 939 | Gợi ý thứ hai gần như là lời giải đầy đủ của (a) (chỉ còn bước đếm). Thứ tự tăng dần vẫn đúng. | So với Lời giải Bước 2–3. | Có thể chấp nhận; nếu muốn để lại việc cho học viên, rút thành "So sánh $P(S)\oplus Y_i$ với $Y_i$ trong hai trường hợp $Y_i=0$, $Y_i=1$." |
| nhẹ (văn phong, Detect) | 04.2(c), Kết luận dòng 237 | Chủ ngữ trừu tượng làm việc của người: "Lỗi trên nhãn đã dùng để huấn luyện chọn $\gamma=1$ và báo $0{,}75$" (mẫu "inanimate things doing human verbs"; `van-phong.md` §9a). | Trích nguyên câu. | "Chọn $\gamma$ theo lỗi trên nhãn đã dùng để huấn luyện cho $\gamma=1$, với lỗi báo cáo $0{,}75$; trên nhãn mới, …" |

Không có phát hiện khác về văn phong trong phạm vi rà soát toán.

## Đối chiếu với đề UML

| Bài | Đề UML | Đánh giá |
|---|---|---|
| 04.7 | 5.2 (tr. 66): ưu, nhược; ảnh hưởng của cỡ mẫu | Đủ hai ý; thêm miền bị chặn để có bao hàm, thêm phần định lượng và (c). Đúng. |
| 04.8 | 7.2 (tr. 97) | Đủ; thêm (b) xử lý dãy toàn $0$. Đúng. |
| 04.9 | 7.3 (tr. 97): hai ý, ý (*) cho lớp đếm được | Đủ; thêm ví dụ tổng nhỏ hơn hẳn $1$ và (b). Kí hiệu $n(h)$ giữ của UML (xem bảng). |
| 04.10 | 7.4 (tr. 97–98) | Đủ; cụ thể hóa cận, thêm (a), (c). UML §7.3 đòi ngôn ngữ không tiền tố, nên giả thiết này đúng với nguồn. |
| 04.11 | 7.5 (tr. 98), năm ý | Ý 4 → (a)–(c); ý 3 + ý 5 → (d) (thu hẹp); ý 1–2 bỏ, không nói (phát hiện trung bình). |
| 04.12 | 11.1 (tr. 154) | Đủ; thêm (b). |
| 04.13 | 11.2 (tr. 154–155) | Đủ ý "mô tả các trường hợp"; thêm $\lvert\mathcal H_i\rvert=2^i$ không nói ra (phát hiện nhẹ). |

So với bản lời giải: 04.8 và 04.10 dùng cùng chuỗi bất đẳng thức chuẩn, nhưng lời văn và các bước (Kraft, $\ln2<1$, sự tồn tại) là của học phần; 04.9 nhóm theo $n(h)$ (bản lời giải đếm lặp); 04.11(a) chứng minh bằng số khối, khác cách ghép cặp điểm của bản lời giải; 04.12 dùng phép cộng modulo $2$, khác cách chia hai trường hợp; 04.13 không giả sử lồng nhau và giữ $\ln(4k/\delta)$. Không có đoạn chép hay diễn lại sát.

## Danh sách số đã tính lại

Ghi theo (vị trí; số in; số tính lại; ✓/✗). Mọi số tính bằng `math` của Python, $\delta=0{,}05$.

| Vị trí | Số in | Tính lại | |
|---|---|---|---|
| 04.1(b) dòng 63 | $\operatorname{opt}_{S_\eta}(h_t)=\tfrac16,0,0,\tfrac16,0,\tfrac16$ | từ $L_{S_\eta}=\tfrac12,\tfrac13,\tfrac13,\tfrac12,\tfrac13,\tfrac12$ (Ví dụ 01.5) | ✓ |
| 04.1(b) dòng 66 | độ lệch lớn nhất $0{,}18$ tại $h_4$ | $\lvert0{,}5-0{,}32\rvert=0{,}18$; các độ lệch khác $0{,}02;0{,}0133;0{,}1133;0{,}0533;0{,}02$ | ✓ |
| 04.1(b) dòng 68 | $0{,}04$; $0{,}36$; $\tfrac16$ | $0{,}22-0{,}18$; $2\cdot0{,}18$; $\tfrac12-\tfrac13$ | ✓ |
| 04.1(b) dòng 70 | $\approx0{,}5667$; $0{,}14$; hiệu $\approx0{,}43$ | $0{,}566667$; $0{,}14$; $0{,}426667$ | ✓ |
| 04.1(c) dòng 77–83 | $0$; $0{,}10$; $0{,}04$; $-0{,}10$ | $0{,}32-0{,}32$; $0{,}32-0{,}22$; $0{,}32-0{,}28$; $0{,}22-0{,}32$ | ✓ |
| 04.1 Kiểm tra lại | $\tfrac13+\tfrac16=\tfrac12$ | đúng | ✓ |
| 04.2(b) dòng 193–198 | $1{,}25$; $1{,}20$; $1{,}3125$; $2{,}00$ | $1{,}25$; $1{,}2$; $1{,}3125$; $2$ | ✓ |
| 04.2(b) dòng 206, 209 | $\gamma^*=0{,}8$; $0{,}09$; $0{,}04$ | $1/1{,}25$; $0{,}25-0{,}16$; $0{,}2^2$ | ✓ |
| 04.2(c) dòng 226 | $0{,}5;0{,}4;0{,}25;0$ và $0{,}75;0{,}80;1{,}0625;2{,}00$ | $\gamma/2$; $0{,}75;0{,}8;1{,}0625;2$ | ✓ |
| 04.2(c) dòng 232 | đạo hàm $-2(1-\gamma)(\mu^2+\sigma^2/m)$ | khai triển lại | ✓ |
| 04.3(a) dòng 281 | $\ln(\pi^2/6)\approx0{,}4977$ | $0{,}497700$ | ✓ |
| 04.3(b) bảng dòng 289–298 | 20 giá trị | $0{,}4977/0{,}6931$; $1{,}8840/1{,}3863$; $2{,}6949/2{,}0794$; $3{,}2703/2{,}7726$; $3{,}7166/3{,}4657$; $4{,}0812/4{,}1589$; $4{,}3895/4{,}8520$; $4{,}6566/5{,}5452$; $4{,}8921/6{,}2383$; $5{,}1029/6{,}9315$ | ✓ |
| 04.3(b) dòng 300 | $2^{-k}$ lớn hơn tại $k=1$, $6..10$ | $g(1)=0{,}195>0$; $g(2..5)<0$; $g(6)=0{,}0777>0$ | ✓ |
| 04.3(b) dòng 302 | $2/\ln2\approx2{,}885$ | $2{,}88539$ | ✓ |
| 04.3(c) bảng dòng 327–331 | $0{,}0504/0{,}0494$; $0{,}0568/0{,}0590$; $0{,}0729/0{,}0737$; $0{,}0937/0{,}0887$; $0{,}1253/0{,}1096$ | $0{,}050374/0{,}049395$; $0{,}056840/0{,}058988$; $0{,}072871/0{,}073726$; $0{,}093680/0{,}088666$; $0{,}125329/0{,}109638$ | ✓ |
| 04.3(c) dòng 323, 333 | $\ln20\approx2{,}9957$; $17{,}552$; $0{,}0937$ | $2{,}995732$; $17{,}5518$; $0{,}093680$ | ✓ |
| 04.3(c) dòng 335 | $\le4\%$ khi $k\le5$; $14\%$ tại $k=20$ | tỉ số lớn nhất $1/0{,}9636=1{,}038$ ($k=2$); $1{,}1431$ | ✓ |
| 04.3 Kiểm tra lại | $5{,}0752$; $4{,}8797$; $0{,}195$ | $5{,}075174$; $4{,}879727$; $0{,}195447$ | ✓ |
| 04.4(a) dòng 383 | $4{,}880$ | $\ln80+\ln(\pi^2/6)=4{,}879727$ | ✓ |
| 04.4(a) dòng 387–391 | $9{,}1117$; $54{,}67$; $3{,}219$; $8{,}099$; $62{,}77$; $0{,}05022$; $0{,}2241$ | $9{,}111728$; $54{,}670$; $2\ln5=3{,}2189$; $8{,}0992$; $62{,}769$; $0{,}050215$; $0{,}224090$ | ✓ |
| 04.4(a) bảng dòng 399–403 | $a_k$, $b_k$, $\mathrm{pen}_k$, $k=5..9$ | $54{,}67/8{,}099/0{,}2241$; $62{,}70/8{,}463/0{,}2386$; $70{,}59/8{,}772/0{,}2520$; $78{,}36/9{,}039/0{,}2644$; $86{,}01/9{,}274/0{,}2761$ | ✓ |
| 04.4(a) dòng 407 | $0{,}3901;0{,}4016;0{,}4120;0{,}4224;0{,}4321$; $0{,}4423;0{,}3790;0{,}3781;0{,}4421$; $0{,}3650$ | giống hệt | ✓ |
| 04.4(a) dòng 409 | $\mathrm{pen}_{10}\approx0{,}2871<0{,}3650$; duyệt cả mười lớp | $0{,}287078$; $\mathrm{pen}_k<v$ ở mọi bước | ✓ |
| 04.4(b) dòng 411 | $\ln800\approx6{,}685$; $0{,}3799;0{,}3642;0{,}3762$; $0{,}3778;0{,}3637;0{,}3771$; $\hat k=3$ | $6{,}684612$; giống hệt; giống hệt; argmin $=3$ ở cả hai dãy (mười tổng) | ✓ |
| 04.4(c) bảng dòng 419–426 | $\mathrm{pen}$: $0{,}0489;0{,}0584;0{,}0659;0{,}0725;0{,}0783;0{,}1013$; tổng $0{,}3489;0{,}2684;0{,}2409;0{,}2425;0{,}2443;0{,}2563$; $k=6..9$: $0{,}2466\to0{,}2533$ | giống hệt; $k=6..9$: $0{,}2466;0{,}2484;0{,}2510;0{,}2533$ | ✓ |
| 04.4(c) dòng 428 | hiệu $0{,}0015$; $0{,}0130$; "giảm khoảng ba lần" | $0{,}001520$; $0{,}013038$; $\mathrm{pen}_3$: tỉ số $2{,}88$ | ✓ |
| 04.4(c) dòng 430 | $0{,}2385<0{,}2409$; $\hat k=4$ | $0{,}238463$; $0{,}240943$ | ✓ |
| 04.4(d) dòng 434–443 | $0{,}04681$; $0{,}05319$; $\ge54$ nhãn $0$; $\Pr(\le53)<10^{-39}$; $0{,}8$ | $0{,}046808$; $0{,}053192$; $\lceil53{,}19\rceil=54$; $1{,}12\cdot10^{-40}$ (scipy) | ✓ |
| 04.4(d) dòng 445 | $0{,}2936$; $1$; $0{,}1$ | $0{,}293617$; $0{,}8+0{,}2$; $0+0{,}1$ | ✓ |
| 04.4(d) dòng 454 | $\ge0{,}8$; $\approx0{,}753$ | $0{,}8$; $0{,}753192$ | ✓ |
| 04.4 Kiểm tra lại | $0{,}07623$; $0{,}2761$ | $0{,}076227$; $0{,}276093$ | ✓ |
| 04.5(a) dòng 493–502 | $L_V(g_{11})=0$; $0{,}8$; $\ge0{,}6$; $0{,}1103$; $0{,}1095$ | đúng; $0{,}110334$; $0{,}109467$ | ✓ |
| 04.5(b) dòng 529–533 | $15{,}2018$; $0{,}0872$; $0{,}1744$ | $15{,}201805$; $0{,}087183$; $0{,}174366$ | ✓ |
| 04.5(c) dòng 542 | $0{,}0387$ | $0{,}038702$ | ✓ |
| 04.5 Kiểm tra lại | $\ln400$; $0{,}1095$ | $J=1$: $\ln(2K/\delta)=\ln400$ | ✓ |
| 04.7(b) bảng dòng 635–637 | $0{,}5157/0{,}7341$; $0{,}1843/0{,}2689$; $0{,}0643/0{,}0953$ | $0{,}515678/0{,}734113$; $0{,}184284/0{,}268910$; $0{,}064288/0{,}095254$ | ✓ |
| 04.7(b) dòng 639 | $86{,}01$; $4{,}382$; $0{,}07231$; $0{,}2689$ | $86{,}009$; $4{,}382027$; $0{,}072313$ | ✓ |
| 04.7(b) dòng 645, 647 | $0{,}4369;0{,}1693;0{,}0619$; $0{,}44$; $0{,}062$ | $0{,}436870;0{,}169253;0{,}061931$ | ✓ |
| 04.7(c) dòng 651 | $\ln160\approx5{,}075$; $0{,}1858$; $0{,}2699$ | $5{,}075174$; $0{,}185783$; $0{,}269940$ | ✓ |
| 04.7(c) dòng 653 | $0{,}0841$ | $0{,}084157$ | ✓ |
| 04.7(c) dòng 657–658 | $0{,}3716$; $0{,}5398$ | $0{,}371565$; $0{,}539879$ (làm tròn xuống ở một cận trên; nên $0{,}5399$) | ✗ (nhẹ) |
| 04.7(c) dòng 661 | $0{,}0015$; $0{,}0010$ | $0{,}001498$; $0{,}001029$ | ✓ |
| 04.7 Kiểm tra lại | $0{,}1682$; $0{,}1693$ | $0{,}168314$ (nên $0{,}1683$); $0{,}169253$ | ✗ (nhẹ) |
| 04.9(a) dòng 741 | $\ln2\approx0{,}693$ | $\sum_n2^{-n}/n=0{,}693147$ | ✓ |
| 04.9(b) dòng 755–760 | $2^{-6}$; $7{,}848$; $0{,}0626$ | $2^{-3}/2^3$; $7{,}847763$; $0{,}062641$ | ✓ |
| 04.10(c) dòng 844–851 | $\ln40\approx3{,}689$; $0{,}0720$; $0{,}1440$; $0{,}1208$; $0{,}023$ | $3{,}688879$; $0{,}072003$; $0{,}144006$; $0{,}120833$; $0{,}023173$ | ✓ |
| 04.11(a), Kiểm tra lại | $2n$; $n=2$: $4$ | lập luận số khối; khớp Bài tập 03.2(b) | ✓ |
| 04.12 | $\tfrac12$; $\tfrac14$; $\tfrac1{4m}$; ví dụ $(1,1,0)$ | đúng; ví dụ: tính chẵn lẻ $1,1,0$, dự đoán đúng cả ba, $L_{\mathrm{loo}}=0$ | ✓ |
| 04.13(c) dòng 1032 | $0{,}0356$; $0{,}0818;0{,}0948;0{,}1063$ | $0{,}035620$; $0{,}081760;0{,}094800;0{,}106254$ | ✓ |
| 04.13(c) bảng dòng 1038–1040 | $0{,}0476/0{,}1174$; $0{,}1214/0{,}1304$; $0{,}3735/0{,}1419$ | $0{,}047568/0{,}117380$; $0{,}121406/0{,}130421$; $0{,}373505/0{,}141874$ | ✓ |
| 04.13(c) dòng 1042 | $697{,}53$; $0{,}3735$ | $697{,}529$; $0{,}373505$ | ✓ |
| 04.13(c) dòng 1044 | điểm đổi chiều $k=119$ | $k=118$: $0{,}131281<0{,}131290$; $k=119$: $0{,}131808>0{,}131334$; đúng với mọi $k\ge119$ đến $1500$; cùng kết quả khi dùng $\lvert\mathcal H\rvert=2^{k+1}-2$ chính xác | ✓ |
| 04.13(c) dòng 1046 | $0{,}1349;0{,}2305;0{,}5238$ | $0{,}134942;0{,}230536;0{,}523843$ | ✓ |
| 04.13(c) dòng 1048 | $0{,}1247;0{,}1440;0{,}1610$ | $0{,}124707;0{,}143994;0{,}160988$ | ✓ |
| 04.13 Kiểm tra lại | $0{,}1018$; $0{,}0318$ | $0{,}101817$; $0{,}031860$ (nên $0{,}0319$) | ✗ (nhẹ) |

Tổng cộng khoảng $190$ giá trị được tính lại; $3$ giá trị lệch một đơn vị ở chữ số thứ tư do làm tròn xuống, không ảnh hưởng kết luận.

## Kiểm tra các dòng "Kiểm tra lại"

- **Có kiểm tra thật:** 04.1 (định nghĩa của $\operatorname{opt}_S$), 04.2 (trường hợp $\gamma=1$ cho lại Ví dụ 04.5, $\gamma=0$ không dùng mẫu), 04.3 (hiệu giữa hai cột bằng $\ln2-\ln(\pi^2/6)$), 04.5 ($J=1$ cho lại Ví dụ 04.12), 04.6 (lỗi dưới rủi ro Bayes là dấu hiệu rò rỉ), 04.7 (hiệu hai cận gần ngưỡng của (b)), 04.9 (lớp rời nhau cho dấu bằng), 04.10 (bản $\lvert h\rvert\ln2$ cho lại Định lý 04.11), 04.11 ($n=2$ khớp Bài tập 03.2(b)), 04.12 (một mẫu cụ thể), 04.13 ($k=1$).
- **Yếu:** 04.4 (tính lại một ô của bảng; xem phát hiện nhẹ); 04.8 (một nhận xét đối chiếu, chấp nhận được).

## Gợi ý

Mọi gợi ý đúng và dẫn đúng khối. Gợi ý trong mỗi bài tăng dần (gợi ý cho từng phần xen nhau, chấp nhận được). Gợi ý 2 của 04.12 gần như là lời giải của (a) (phát hiện nhẹ). Không gợi ý nào nêu điều sai.

## Kết luận

**Giao được**: không có phát hiện chặn bàn giao hay nghiêm trọng. Đề nghị sửa bốn phát hiện mức trung bình trước khi phát hành (04.3(d) phạm vi hàm lỗi; 04.11 nói rõ các ý UML bị bỏ hoặc gộp; 04.6 hai câu về quy tắc 1 và quy tắc 2). Các phát hiện nhẹ có thể sửa cùng lượt hoặc để lại theo quyết định của điều phối viên.
