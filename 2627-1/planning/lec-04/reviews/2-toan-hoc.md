# Bài 04 — Phản biện 2/5: độ chính xác toán học

**Số phát hiện theo mức độ:** chặn bàn giao 0 · nghiêm trọng 0 · trung bình 2 · nhẹ 11.

Đầu vào: `lec04-draft-frozen.md` (số dòng dẫn theo tệp này). Đã đối chiếu với `materials/lec-0{1,2,3}/lecture-note.md`, `materials/lec-02/exercises.md` (Bài tập 02.4, 02.6), `planning/ky-hieu.md`; `source-analysis.md` chỉ đọc sau khi đã có kết luận riêng (dùng để lấy các rủi ro thực nghiệm giả định $k=5,\ldots,9$ của Bài tập 04.4). Mã Python tính lại: `rev04/r2/c1.py`–`c4.py` trong scratchpad.

Phạm vi phản biện này là toán học. Không có phát hiện về câu chữ, nên không dùng chế độ Detect của `no-ai-slop`.

## 1. Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | Ví dụ 04.8, Bước 2 (dòng 566), Kết luận (dòng 577); §9 (dòng 950) | Ghi "xác suất hỏng là $1-(1-2^{-10})^K$". Thật ra đây chỉ là xác suất của biến cố "có $k$ với $L_S(h_k)=0$", tức một cận dưới của xác suất hỏng. Với $m=10$, $L_D(h_k)=\tfrac12$ và bán kính $0{,}4295$, kết luận của Bổ đề 04.9 cũng sai khi $L_S(h_k)=1$ (độ lệch $\tfrac12$). Vậy biến cố hỏng của lớp $k$ là $L_S(h_k)\in\{0,1\}$, có xác suất $2\cdot2^{-10}$. | Các giá trị $L_S\in\{0,0{,}1,\ldots,1\}$ cho độ lệch $>0{,}4295$ khi và chỉ khi $L_S\in\{0,1\}$. Xác suất hỏng chính xác là $1-(1-2^{-9})^K=0{,}8584$ ($K=1000$) và $0{,}99994$ ($K=5000$), so với $0{,}6236$ và $0{,}9924$ in trong ghi chú. Bài tập 02.4(b) chỉ tính $\Pr(\exists k:L_S(h_k)=0)$; `source-analysis.md` §4(c) cũng viết "fails w.p. $>0{,}62$". Phản ví dụ vẫn đúng hướng ($\ge0{,}62\gg0{,}05$), chỉ đẳng thức là sai. | Cách gọn nhất là sửa dòng 566 thành "…nên xác suất hỏng ít nhất là $\Pr(\exists k:L_S(h_k)=0)=1-(1-2^{-10})^K$: $0{,}6236$ khi $K=1000$, $0{,}9924$ khi $K=5000$ (Bài tập 02.4(b))". Dòng 577 sửa thành "sai với xác suất ít nhất $0{,}62$", dòng 950 thành "xác suất hỏng ít nhất $0{,}62$". Nếu muốn giữ số chính xác: "hỏng khi và chỉ khi có $k$ với $L_S(h_k)\in\{0,1\}$; xác suất $1-(1-2^{-9})^K$, bằng $0{,}8584$ và $0{,}99994$". |
| trung bình | Hệ quả 04.15, mục **Thuật toán** (dòng 789); Phụ lục A, Bước 5 (dòng 1041); Định lý 04.16(b) (dòng 863) | Phần chứng minh đầy đủ của Hệ quả 04.15 dùng $\Pr[L_D(A_{\mathrm{SRM}}(S))\le L_D(h)+\epsilon]$, nên cần $A_{\mathrm{SRM}}$ thỏa điều kiện đo được của Định nghĩa 01.4. Phụ lục A chỉ *giả sử* tồn tại một quy tắc chọn đo được, nhưng mục **Giả thiết** của 04.15 không nêu điều này. Định lý 04.16(b) vì thế khẳng định "$\mathcal H$ học được không đều" mà không có điều kiện, trong khi việc tồn tại một thuật toán đo được chưa được chứng minh. | Hệ quả 03.16 ghi rõ trong giả thiết "thỏa điều kiện đo được của Định nghĩa 01.4". Định lý 03.17(b) ghi "có ít nhất một thuật toán ERM trên $\mathcal H$ thỏa Định nghĩa 01.4". Định lý 04.11 (dòng 610) cũng ghi điều kiện này, nhưng 04.15 thì không. | Dòng 789: thêm "…, và thỏa điều kiện đo được của Định nghĩa 01.4 (Phụ lục A, Bước 5)". Dòng 863: "…thì $\mathcal H$ học được không đều khi có một thuật toán $A_{\mathrm{SRM}}$ thỏa Định nghĩa 01.4 (Hệ quả 04.15)", theo đúng mẫu của Định lý 03.17(b). |
| nhẹ | Ví dụ 04.3, Bước 1–2 (dòng 244, 250–251) | Ghi "$\rho_m\le0{,}1644$ theo dạng trực tiếp", trong khi dạng trực tiếp cho $0{,}16443>0{,}1644$, tức cận trên bị làm tròn xuống. Dòng tiếp theo ghi "$2\cdot0{,}1644+0{,}01=0{,}3389$", nhưng phép tính trên số đã in cho $0{,}3388$; số $0{,}3389$ đến từ giá trị chưa làm tròn $0{,}33886$. | Python: dạng trực tiếp $=0{,}164430$ ($d=3$) và $0{,}279919$ ($d=11$). Khẳng định $\rho_m\le0{,}1644$ vẫn đúng, vì $\Pi_{\mathcal H}(2m)\le\sum_{i\le3}\binom{2m}i$ cho $\rho_m\approx0{,}1608$, nhưng lý do được nêu không cho điều đó. | Viết "$\rho_m\le0{,}16443$" (và $\le0{,}27992$), rồi "$2\cdot0{,}16443+0{,}01\approx0{,}3389$". Cách khác là viết "$\le0{,}1645$", "$\le0{,}2800$". |
| nhẹ | Ví dụ 04.9, Bước 2 và Bước 4 (dòng 715, 719); câu hỏi cuối buổi (b) (dòng 989); §9 (dòng 942) | Các cận trên tin cậy bị làm tròn xuống ở chữ số thứ năm: $0{,}3650$ (chính xác $0{,}365044$), $0{,}4349$ ($0{,}434919$), $0{,}3750$ ($0{,}375044$). Hiệu ở Bước 4 ghi $0{,}0057$, nhưng giá trị chính xác là $0{,}005759\approx0{,}0058$ ($0{,}0057$ là hiệu của hai số đã làm tròn). | `c2.py`, `c4.py`. | Thêm một câu sau bảng: "các tổng làm tròn đến bốn chữ số; cận đúng là giá trị chưa làm tròn". Sửa $0{,}0057$ thành "khoảng $0{,}0058$". Cách khác: dùng "$\approx$" ở các chỗ có chữ "$\le$". |
| nhẹ | Ví dụ 04.9, Bước 5 (dòng 721) | Câu "Với $q_k=1/10$ hoặc $q_k=2^{-k}$, SRM vẫn chọn $k=3$, nhưng tổng tại $k=3$ và $k=4$ chỉ cách nhau $0{,}0131$" gắn số $0{,}0131$ với hai trọng số mới. Thật ra $0{,}0131$ là hiệu của hai số đã làm tròn với trọng số gốc (chính xác $0{,}01304$). | Hiệu $k=4$ trừ $k=3$: trọng số gốc $0{,}01304$; $q_k=1/10$: $0{,}01200$; $q_k=2^{-k}$: $0{,}01338$. Lựa chọn $k=3$ với hai trọng số mới đã được kiểm trên cả mười hàng (dùng các giá trị giả định $0{,}166$; $0{,}163$; $0{,}160$; $0{,}158$; $0{,}156$ cho $k=5,\ldots,9$): đúng. | "…SRM vẫn chọn $k=3$; với cả ba cách chọn trọng số, tổng tại $k=4$ chỉ lớn hơn tổng tại $k=3$ từ $0{,}012$ đến $0{,}013$, nên lựa chọn nhạy với các giá trị giả định." |
| nhẹ | Định nghĩa 04.1 (dòng 142) so với Nhận xét 04.7 (dòng 449) | Định nghĩa 04.1 đòi $\ell$ thỏa (T2), (T3), nhưng Nhận xét 04.7 tính "sai số xấp xỉ" cho hàm lỗi bình phương, có giá trị $\{0,4\}$ trên lớp $\{\pm1\}$, nên (T3) không thỏa. Định nghĩa không dùng (T3); nó chỉ cần các rủi ro hữu hạn. | Dòng 443–449. | Ở Định nghĩa 04.1, thay "thỏa (T2), (T3)" bằng "thỏa (T2), với $L_D(h)<\infty$ trên $\mathcal H$". Cách khác: ở dòng 449 thêm "(Định nghĩa 04.1 áp dụng nguyên văn cho hàm lỗi bình phương khi các rủi ro hữu hạn)". |
| nhẹ | Định lý 04.11, mục **Thuật toán** (dòng 610) | Bảo đảm đúng "đồng thời cho mọi nghiệm $\tau$-chính xác" trên biến cố $E$ của Bổ đề 04.9. Chứng minh không dùng thuật toán, cũng không dùng điều kiện đo được của nó; tính đo được của $E$ đến từ Định nghĩa 04.8. Như vậy có một giả thiết được liệt kê mà không được dùng. | Dòng 633–645. | Đổi mục thành "**Dung sai.** $\tau\ge0$" và chuyển ý về thuật toán vào câu đọc lại: "Khi một thuật toán SRM với dung sai $\tau$ thỏa Định nghĩa 01.4, (a) và (b) đúng cho đầu ra của nó." |
| nhẹ | Thuật toán 04.12, **Đầu vào** (dòng 658) và **Chi phí** (dòng 670) | Với danh sách vô hạn và $\mathrm{pen}_k$ bị chặn (ví dụ dạng chiều VC cắt ở $1$, Phụ lục A Bước 4), vòng lặp không dừng, nên thủ tục không là thuật toán. Đầu vào chưa loại trường hợp này. Ngoài ra, khi phép so sánh có sai số $\tau'$, phép thử dừng "$\mathrm{pen}_k\ge v$" cũng là một phép so sánh, nên dòng 682 phải là $v\le\mathrm{pen}_k+\tau'$. Kết luận $\tau=\epsilon_{\mathrm{opt}}+\tau'$ không đổi. | Dòng 664–682. | Thêm vào mục Họ lớp: "danh sách hữu hạn, hoặc $\mathrm{pen}_k\to\infty$". Ở dòng 682, viết "$\le\mathrm{pen}_k+\tau'$", hoặc nói rõ $\tau'$ gồm cả sai số của phép thử dừng. |
| nhẹ | Phụ lục A (dòng 1020, 1025, 1031) | Kí hiệu $V$ được dùng cho giá trị nhỏ nhất của mục tiêu có phạt, trong khi `ky-hieu.md` và §8 dành $V$ cho mẫu xác thực. | `ky-hieu.md`: "$V=(V_1,\ldots,V_{m_v})$ … Bài 04". | Đổi thành $\Phi^\star$ hoặc $v^\star$ (Thuật toán 04.12 đã dùng $v$ cho giá trị tốt nhất hiện có, nên $v^\star$ khớp với nó). |
| nhẹ | Ý chứng minh của Định lý 04.16(a) (dòng 866) | Định lý 03.17(a) phát biểu cho "mọi thuật toán học $A$" theo Định nghĩa 01.4, tức đầu ra thuộc lớp đang xét. Ở đây lớp là $\mathcal H_k$, còn $A$ trả về phần tử của $\mathcal H\supsetneq\mathcal H_k$. Ý chứng minh vẫn đúng, vì lập luận không có bữa trưa miễn phí không dùng $A(S)\in\mathcal H_k$, nhưng ghi chú chưa nói điều này. Các bước còn lại đã được kiểm: $m=k\ge M(\tfrac18,\tfrac18,h)$; $\Pr[L_D(A(S))>\tfrac18]\le\tfrac18<\tfrac17$; do đó $\operatorname{VCdim}(\mathcal H_k)<2k$. | Lec-03, dòng 788–795. | Thêm nửa câu: "(lập luận của Định lý 03.17(a) không dùng điều kiện đầu ra thuộc $\mathcal H_k$, nên áp dụng được cho $A$ với đầu ra trong $\mathcal H$)". |
| nhẹ | Dòng 190 | "$\operatorname{opt}_S(A(S))$ là một biến ngẫu nhiên": với lớp vô hạn, $\inf_{h\in\mathcal H}L_S(h)$ có thể không đo được nếu không có thêm điều kiện, như (M). Phụ lục A(v) của Bài 01 nêu đúng hiện tượng này cho cận trên đúng. | Lec-03, dòng 512. | "…là một hàm chỉ phụ thuộc mẫu, không phụ thuộc $D$ (đo được, chẳng hạn, khi $\mathcal H$ thỏa (M))." |
| nhẹ | Dòng 776 | Câu "Khác biệt duy nhất là $M$ được phụ thuộc giả thuyết so sánh $h$" bỏ qua một khác biệt: đối tượng so sánh là $L_D(h)$, không phải $\inf_{h'}L_D(h')$. Hai cách viết tương đương khi $M$ không phụ thuộc $h$, nhờ tính liên tục từ trên của xác suất áp dụng cho một dãy $h_n$ có $L_D(h_n)\downarrow\inf$, nhưng ghi chú chưa nêu điều đó. | Định nghĩa 01.25 so với Định nghĩa 04.14. | "Khác biệt là $M$ được phụ thuộc $h$, và đối tượng so sánh là $L_D(h)$; khi $M$ không phụ thuộc $h$, yêu cầu 'với mọi $h$' tương đương với yêu cầu so với $\inf_{h}L_D(h)$ (tính liên tục của xác suất)." |
| nhẹ | Hệ quả 04.17, mục **Ứng viên** (dòng 882) và Bước 3 của chứng minh (dòng 909) | Giả thiết ghi "các hàm đo được của $S$", nhưng chứng minh lại viết "Bước này giả sử các ứng viên đo được theo $S$, nên chứng minh là phác thảo". Hai chỗ mâu thuẫn nhau, và điều thật sự cần là $(s,z)\mapsto\ell(g_j(s),z)$ đo được đồng thời, cùng $K(S)$ đo được. | Dòng 882, 909. | Nêu rõ trong giả thiết: "$K(S)$ và $(s,z)\mapsto\ell(g_j(s),z)$ đo được". Ở Bước 3, nói phần nào là phác thảo: phép lấy kì vọng của xác suất có điều kiện (định lý Fubini). |

**Đã kiểm, không có lỗi** (mỗi mục là một chứng minh tự làm lại):

- **Mệnh đề 04.3.** Chuỗi bốn bất đẳng thức đúng. Việc lấy $\inf$ không cần giá trị nhỏ nhất đạt được. Phần (b) chỉ dùng biến cố đại diện, không phụ thuộc quy tắc chọn. Các giả thiết (T1)+(T4), hoặc (T1)+0–1+(T5)+(M), đều đủ và đều được dùng. Phần (b) trở về đúng Hệ quả 02.16(b) và 03.16(b).
- **Mệnh đề 04.6.** Mọi số hạng đều khả tích nhờ Cauchy–Schwarz. Chỉ số hạng chéo $(\hat f-\bar f)(f^*-Y)$ cần độc lập, và thật ra chỉ cần không tương quan. Đẳng thức lấy trung bình theo $X$ cần $(X,Y)$ độc lập với $S$, và ghi chú đã nêu.
- **Bổ đề 04.9.** Ta có $\Pr(B_k)=1-\Pr[\sup\le\mathrm{rad}]\le\delta q_k$; $\delta q_k\in(0,1)$; bất đẳng thức hợp đếm được cho tổng không quá $\delta$; tính đo được đến từ Định nghĩa 04.8.
- **Định nghĩa 04.8.** Dạng chiều VC (trực tiếp khi $m\ge d$, bằng $1$ khi $m<d$) là một bán kính hợp lệ. Mọi bán kính của $\mathcal M_{[0,1]}$ đều $\ge1$.
- **Định lý 04.11.** Chuỗi ba bất đẳng thức đúng. $\tau$ xuất hiện với hệ số $1$, nằm ngoài $\inf$. Cận đúng đồng thời cho mọi nghiệm $\tau$-chính xác, kể cả khi $\tau$ được đọc từ mẫu (như trong câu hỏi cuối buổi), vì $E$ không phụ thuộc $\tau$.
- **Thuật toán 04.12 và $\tau=\epsilon_{\mathrm{opt}}+\tau'$.** Lớp đã duyệt và lớp chưa duyệt (nhờ $\mathrm{pen}$ không giảm và $L_S\ge0$) đều được kiểm. Cận tinh hơn $\inf_k[\inf L_D+2\mathrm{pen}_k+\operatorname{opt}_S(\hat h_k)]+\tau'$ đúng trên cùng biến cố khi mọi lớp được duyệt.
- **Hệ quả 04.15.** $\delta=1/m\in(0,1)$ khi $m\ge2$. $\mathrm{pen}_k(m)\to0$ trong cả ba trường hợp: hữu hạn, $1\le d_k\le m$, và $d_k=0$. $M_k(\epsilon)$ hữu hạn. $m\ge\max\{\lceil1/\delta\rceil,M_k\}$ kéo theo $m\ge2$, $1/m\le\delta$ và $2\mathrm{pen}_k\le\epsilon$. $M$ chỉ phụ thuộc $h$ qua $k(h)$. Phần (b): lấy $\inf$ trên $E_m$ cho đúng biến cố của Định nghĩa 01.25. Chỉ còn thiếu giả thiết đo được (đã ghi ở bảng trên).
- **Phụ lục B.** $g(m)=\tfrac{32}m(4\ln\tfrac{em}2+c)$ tương đương với $2\mathrm{pen}\le0{,}1$ (vì $8/0{,}0025=32/0{,}01$). Đạo hàm $(4-4\ln\tfrac{em}2-c)/m^2<0$ khi $m\ge4$. Trường hợp thứ ba có tử số $5\ln m+c_0$ với $c_0=5{,}3086>0$, và $5\ln3=5{,}49>5$. Vì $\rho_m\le$ dạng chiều VC, cỡ mẫu tìm được là một cận trên của $M_3(0{,}1)$.
- **Định lý 04.16(a).** Ý chứng minh đúng, kèm nhận xét ở bảng trên.
- **Hệ quả 04.17.** Phép lấy điều kiện theo $S$ (dùng (T7)) đúng. Hệ quả 02.16(a) đúng cho mọi nghiệm ERM trên $V$, và $\hat g$ là một nghiệm như vậy. Trùng lặp ứng viên chỉ làm $K'\le K$, mà cận đơn điệu theo $K$. Phần (b) là Định lý 02.14(b).
- **Nhận xét 04.7.** ERM là dấu đa số, mỗi dấu với xác suất $\tfrac12$. $\bar f=0=f^*$, phương sai $1$, $\mathbb E(c-Y)^2=2$, $L^*=1$, sai số xấp xỉ $1$.
- **Phụ lục A.** Bước 1 (với $\tau>0$) cần ít nhất một lớp khác rỗng. Bước 3: tập $J$ hữu hạn, và $V$ là giá trị nhỏ nhất trên $J$. Bước 4: cả hai bán kính $\to\infty$ vì $q_k\to0$; dạng cắt ở $1$ thì không.
- **Phản ví dụ.** Ví dụ 04.5 chỉ bỏ tính độc lập. Ví dụ 04.8 chỉ bỏ $\sum q_k\le1$. Ví dụ 04.10 chỉ bỏ (T6), qua lớp $\mathcal G_S$ phụ thuộc $S$. Ví dụ 04.6 có giả thiết đúng và cách đọc đúng.
- **Ứng dụng §3.** $d_k=k+1$, cả cận dưới lẫn cận trên qua phép chiếu, và (M).
- **Ví dụ 04.11.** Lớp đếm được, có chiều VC vô hạn trên các số hữu tỉ, áp dụng được Định lý 03.17(a) và Hệ quả 04.15(a).
- **Trích dẫn.** Mọi trích dẫn đều khớp với nguồn: Định lý 02.14(a)(b), Hệ quả 02.10(b), Hệ quả 02.16(a)(b), Định nghĩa 02.13, dạng đếm được sau Bổ đề 02.12, Định lý 03.15(a)(b) (điều kiện $1\le d\le m$), Hệ quả 03.16, Định lý 03.17(a), Ví dụ 03.6/03.7/03.8/03.9, Định nghĩa 01.4/01.12/01.24/01.25, Nhận xét 01.9/01.11/01.26, Ví dụ 01.2/01.6/01.7/01.10, đẳng thức sau Định nghĩa 01.24, §9 và §11 của Bài 02–03, cùng các số $0{,}18$; $0{,}22$; $0{,}32$; $0{,}28$; $0{,}329$; $0{,}560$.

## 2. Danh sách số đã kiểm (khoảng 130 số)

✓ nghĩa là số in trùng với giá trị tính lại sau khi làm tròn. ~ nghĩa là đúng sau khi làm tròn nhưng có lệch nhỏ (xem bảng phát hiện). ✗ nghĩa là sai.

| vị trí | số in | tính lại | |
|---|---|---|---|
| Câu ôn 1 | $\ln400\approx5{,}9915$; $r_m\approx0{,}0547$ | $5{,}99146$; $0{,}054733$ | ✓ |
| Câu ôn 2 | $0{,}05$ | $0{,}05$ | ✓ |
| Dòng 13 | $0{,}164\to0{,}280$ | $0{,}16443$; $0{,}27992$ | ✓ |
| Dòng 159 | $-0{,}03$ | $0{,}22-0{,}25$ | ✓ |
| Ví dụ 04.2 | $0{,}04$; $0{,}10$; $0{,}14$; $0{,}32-0{,}18$ | như in | ✓ |
| Ví dụ 04.3 | $\rho\le0{,}1644$; $0{,}2799$ | $0{,}164430$; $0{,}279919$ (giá trị thật của $\rho_m$ theo tổng Sauer: $0{,}1608$; $0{,}2769$) | ~ |
| Ví dụ 04.3 | $2\cdot0{,}1644+0{,}01=0{,}3389$ | $0{,}33886$ (trên số đã in: $0{,}3388$) | ~ |
| Ví dụ 04.3 | $0{,}5698$; "khoảng $0{,}231$" | $0{,}56984$; $0{,}23098$ | ✓ |
| Nhận xét 04.4 | $L_S(h_2)=0$ (nghiệm ERM duy nhất); $\operatorname{opt}(h_3)=\tfrac12$; $0{,}32$; $0{,}22$; $-0{,}10$ | như in ($L_S(h_t)=\tfrac12$ với mọi $t\ne2$) | ✓ |
| Dòng 289 | $\bar f=\tfrac23$; $f^*=\tfrac14$; độ chệch $\tfrac5{12}$ | như in | ✓ |
| Ví dụ 04.4 B1 | $\hat b=(Y_3-Y_1)/2$; trọng số $(\tfrac1{12},\tfrac13,\tfrac7{12})$; $(-\tfrac18,\tfrac34,\tfrac38)$ | như in | ✓ |
| Ví dụ 04.4 B2 | $\tfrac23$; $\tfrac23$; $\tfrac14$ | như in | ✓ |
| Ví dụ 04.4 B3 | $\tfrac{25}{144}\approx0{,}1736$ | $0{,}173611$ | ✓ |
| Ví dụ 04.4 B4 | $0{,}3333$; $\tfrac{66}{144}\approx0{,}4583$; $\tfrac{46}{64}=0{,}71875$ | $\tfrac13$; $\tfrac{11}{24}$; $\tfrac{23}{32}$ | ✓ |
| Ví dụ 04.4 B5 | $0{,}5069$; $0{,}6319$; $0{,}7188$ | $0{,}506944$; $0{,}631944$; $0{,}71875$ | ✓ |
| Ví dụ 04.4 B6 | $0{,}2069$; $0{,}2194$; $0{,}0719$ | $0{,}206944$; $0{,}219444$; $0{,}071875$ | ✓ |
| Ví dụ 04.5 | $0{,}25$; $1{,}25$; $0{,}75$; $0{,}5=2\sigma^2/m$ | như in | ✓ |
| Ví dụ 04.6 | $0{,}58$; $0{,}9$; $0{,}24$; $0{,}09$; $0{,}81$ | như in | ✓ |
| Nhận xét 04.7 | độ chệch $0$; phương sai $1$; $\mathbb E(c-Y)^2=2$; sai số xấp xỉ $1$ | như in | ✓ |
| Ví dụ 04.7 B2 | $\ln(\pi^2/6)\approx0{,}4977$; $2{,}695$; $5{,}103$ | $0{,}497700$; $2{,}694925$; $5{,}102870$ | ✓ |
| Ví dụ 04.7 B3 | $\ln80\approx4{,}382$; $13\,591$; $38{,}069$; $7{,}077$; $0{,}036117$; $0{,}1900$; $0{,}1843$ | $4{,}382027$; $13\,591{,}4$; $38{,}06877$; $7{,}07695$; $0{,}0361166$; $0{,}190044$; $0{,}184284$ | ✓ |
| Ví dụ 04.7 B4 | $0{,}1644\to0{,}1690$; $0{,}2799\to0{,}2871$ | $0{,}16443\to0{,}16895$; $0{,}27992\to0{,}28712$ | ✓ |
| Ví dụ 04.7 KL | $1\%$ ($k=1$) đến $3{,}2\%$ ($k=4$) | $0{,}998\%$; $3{,}165\%$ (cực đại trên $k=1..10$ tại $k=4$) | ✓ |
| Ví dụ 04.8 B1 | $0{,}4295$ | $0{,}429469$ | ✓ |
| Ví dụ 04.8 B2 | xác suất hỏng $0{,}6236$; $0{,}9924$ | $\Pr(\exists k:L_S=0)=0{,}623576$; $0{,}992442$; xác suất hỏng chính xác $0{,}858440$; $0{,}999943$ | ✗ (chỉ là cận dưới) |
| Ví dụ 04.8 B3 | $0{,}7279$ | $0{,}727895$ | ✓ |
| Ví dụ 04.9 bảng | tổng $0{,}4423$; $0{,}3790$; $0{,}3650$; $0{,}3781$; $0{,}4421$ | $0{,}442269$; $0{,}378951$; $0{,}365044$; $0{,}378082$; $0{,}442119$ | ✓ |
| Ví dụ 04.9 bảng | $\mathrm{pen}$ $0{,}1423$; $0{,}1690$; $0{,}1900$; $0{,}2081$; $0{,}2871$ | $0{,}142269$; $0{,}168951$; $0{,}190044$; $0{,}208082$; $0{,}287119$ | ✓ |
| Dòng 713 | hàng $k=5..9$: $0{,}3901$ đến $0{,}4321$ | $0{,}3901$; $0{,}4016$; $0{,}4120$; $0{,}4224$; $0{,}4321$ (rủi ro thực nghiệm giả định $0{,}166$…$0{,}156$ lấy từ PTN §3(a)) | ✓ |
| Ví dụ 04.9 B3 | $0{,}4349$ | $0{,}434919$ | ✓ |
| Ví dụ 04.9 B4 | $0{,}3593$; hiệu $0{,}0057$ | $0{,}359284$; $0{,}005759$ | ~ |
| Ví dụ 04.9 B5 | chọn $k=3$ với $1/10$ và $2^{-k}$; cách nhau $0{,}0131$ | chọn $k=3$ trên cả mười hàng; hiệu $0{,}01304$ / $0{,}01200$ / $0{,}01338$ | ~ |
| Ví dụ 04.9 KL, §9 | $2\mathrm{pen}$: $0{,}3379$; $0{,}5742$; so với $0{,}329$; $0{,}560$ | $0{,}337902$; $0{,}574237$; $0{,}328861$; $0{,}559839$ | ✓ |
| Ví dụ 04.10 | $0{,}2$; $0{,}8$; $0{,}0468$; $1-0{,}8^{1000}$ | như in; $0{,}046808$ | ✓ |
| Dòng 841 | $172\,279$; $181\,575$; $213\,317$; $\lceil1/\delta\rceil=20$ | $172\,279$; $181\,575$; $213\,317$ (chia đôi khoảng, đã kiểm thêm $2\cdot10^5$ giá trị phía trên); $20$ | ✓ |
| Dòng 841, §9 | $5{,}4\%$; $17{,}5\%$ | $5{,}396\%$; $17{,}48\%$ | ✓ |
| Phụ lục B | $c=4{,}382$; $7{,}077$; $c(213\,317)\approx16{,}35$ | $4{,}38203$; $7{,}07695$; $16{,}3518$ | ✓ |
| Phụ lục B | $g\approx0{,}0099999$; $g(m-1)>0{,}01$ | $0{,}00999995$; $0{,}00999998$; $0{,}00999996$ / $0{,}010000004$; $0{,}010000029$; $0{,}010000005$ | ✓ |
| Phụ lục B | $c_0>0$; ngưỡng $m\ge3$ | $c_0=5{,}3086$; $5\ln3=5{,}493>5$ | ✓ |
| Ví dụ 04.11 | $\ln(1/q_j)=2\ln j+\ln(\pi^2/6)$ | như in | ✓ |
| Ví dụ 04.12 | $5{,}9915$; $0{,}0547$; $0{,}1095$ | $5{,}99146$; $0{,}054733$; $0{,}109467$ | ✓ |
| Ví dụ 04.12 B3 | $0{,}2448$; $0{,}1548$; $0{,}0774$; $0{,}0490$ | $0{,}244775$; $0{,}154809$; $0{,}077405$; $0{,}048955$ | ✓ |
| Ví dụ 04.12 B4 | $1198{,}3\to1199$; $4794$ | $1198{,}29$; $4793{,}17\to4794$ | ✓ |
| Ví dụ 04.12 KL | $K=10^6$: $0{,}1871$ | $0{,}187106$ | ✓ |
| Nhận xét 04.18 | $4\cdot2\sqrt{\ln600/2000}\approx0{,}4524$ | $0{,}452440$ | ✓ |
| §9 | $0{,}3650$; $0{,}4349$; $3{,}2\%$; $0{,}58/0{,}90$; $0{,}1095$; $0{,}0468/0{,}8$; $0{,}75/1{,}25$ | như trên | ✓ |
| §9 | "xác suất hỏng $0{,}62$" | cận dưới $0{,}6236$; chính xác $0{,}8584$ | ✗ |
| Câu hỏi cuối buổi | $\operatorname{opt}=0{,}010$; $0{,}3750$; $\tau=0{,}010$ | $0{,}010$; $0{,}375044$; $0{,}010000$ | ✓ |
| Phụ lục C | cột $a$: $20{,}42$; $29{,}41$; $38{,}07$; $46{,}47$; $93{,}56$ | $20{,}4207$; $29{,}4146$; $38{,}0688$; $46{,}4702$; $93{,}5615$ | ✓ |
| Phụ lục C | cột $b$: $4{,}880$; $6{,}266$; $7{,}077$; $7{,}652$; $9{,}485$ | $4{,}8797$; $6{,}2660$; $7{,}0770$; $7{,}6523$; $9{,}4849$ | ✓ |
| Phụ lục C | không chia: $0{,}1409$; $0{,}1644$; $0{,}1843$; $0{,}2017$; $0{,}2799$ | $0{,}140861$; $0{,}164430$; $0{,}184284$; $0{,}201699$; $0{,}279919$ | ✓ |
| Phụ lục C | tỉ số $1{,}010$; $1{,}027$; $1{,}031$; $1{,}032$; $1{,}026$ | $1{,}00998$; $1{,}02749$; $1{,}03125$; $1{,}03165$; $1{,}02572$ | ✓ |
| Phụ lục C | $u_i(\tfrac12)$: $-\tfrac18$; $\tfrac34$; $\tfrac38$; tổng $1$ | như in | ✓ |
| §3 | $d_k=k+1$; $\mathcal H_{10}=\mathcal H^{10}_{\mathrm{aff}}$ | Mệnh đề 03.9 với phép chiếu | ✓ |

Làm tròn: trong toàn ghi chú, các số được làm tròn bốn chữ số một cách nhất quán. Ngoại lệ là các cận trên bị làm tròn xuống ở chữ số thứ năm và hai hiệu tính trên số đã làm tròn ($0{,}0057$; $0{,}0131$), đã ghi ở bảng phát hiện.

## 3. Kết luận

**Giao được**, sau khi sửa hai phát hiện mức trung bình. Hai chỗ cần sửa là xác suất hỏng của Ví dụ 04.8 (và câu tương ứng ở §9), và giả thiết đo được trong Hệ quả 04.15 cùng Định lý 04.16(b). Mỗi chỗ chỉ cần sửa một hoặc hai câu, không phải viết lại chứng minh. Không có lỗi chặn bàn giao hay nghiêm trọng: mọi chứng minh đầy đủ (04.3, 04.6, 04.9, 04.11, 04.15) đều được dựng lại và đều đúng, mọi trích dẫn từ Bài 01–03 đều nói đúng điều ghi chú dùng, kể cả hằng số và giả thiết. Các phát hiện nhẹ có thể giao cho người biên tập xử lý trong cùng lượt.
