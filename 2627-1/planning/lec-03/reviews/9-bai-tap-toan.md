# Rà soát toán học: Bài tập Bài 03 (bản đóng băng `lec03-ex-frozen.md`)

**Vai trò:** người rà soát toán học độc lập (chỉ đọc). **Đầu vào:** `lec03-ex-frozen.md` (868 dòng), ghi chú `2627-1/materials/lec-03/lecture-note.md`, ghi chú Bài 01–02 cho các số hiệu được dẫn, UML trang PDF 78–80 (§6.8) và 128–129 (§9.6). Sách lời giải `MLbookSol.pdf` chỉ được mở sau khi đã có kết luận riêng, để kiểm tra việc chép.

**Cách làm:** tự giải từng bài; kiểm từng bước lời giải và từng trích dẫn số hiệu; tính lại mọi con số bằng Python (`scratchpad/rev9/num.py`); kiểm vét cạn các khẳng định tổ hợp trên trường hợp nhỏ (`scratchpad/rev9/comb.py`, 42 phép kiểm, tất cả đạt). Đề xuất câu chữ tiếng Việt được tự kiểm theo `no-ai-slop` chế độ Detect.

## 1. Kết luận theo bài

| Bài | Kết luận | Ghi chú ngắn |
|---|---|---|
| 03.1 | Đúng | Mọi giá trị hàm tăng trưởng, bảng so sánh và điều kiện dấu bằng khớp kiểm vét cạn. |
| 03.2 | Đúng | Cận dưới, cận trên của (a), (b) đầy đủ; (c) đúng theo Nhận xét 03.4. |
| 03.3 | Đúng | Hai hệ tuyến tính giải đúng; (c) đúng cả hai chiều. |
| 03.4 | Đúng, có 3 điểm nhẹ | Mọi con số khớp đến chữ số đã ghi; ba chỗ diễn đạt cần sửa (kí hiệu $\epsilon$ ở (c), "bằng" thay cho "xấp xỉ bằng", số thập phân bị cắt). |
| 03.5 | Đúng | Phép dựng $\theta$ đúng với mọi cách gán nhãn, kiểm chính xác bằng số hữu tỉ đến $k=14$; (d) đúng, chỉ đúng giả thiết bị vi phạm. |
| 03.6 | Đúng, có 1 điểm nhẹ | Chứng minh phép dồn đúng; một bước nhỏ ở (d) Bước 1 cần viện dẫn phép đếm của (c). |
| 03.7 | Đúng | Khớp UML 6.2; đáp số $\min\{2k+1,n\}$ đúng (sách lời giải UML ghi $k$, sai với lớp "hoặc"). |
| 03.8 | Đúng, có 2 điểm nhẹ | Quy nạp của (a) đầy đủ, có trường hợp gốc $n=0$; bảng (b) đúng; từ "chặt" mơ hồ; một trích dẫn ở (c) hơi rộng. |
| 03.9 | Lời giải đúng; Gợi ý 1 sai | Gợi ý 1 khẳng định một điều kiện "khi và chỉ khi" sai (phản ví dụ ở bảng phát hiện). |
| 03.10 | Đúng | $\lvert\mathcal H\rvert$, chiều VC với $p=1,\ldots,4$, phần đơn điệu đều khớp vét cạn; lập luận mod $8$ đúng. |
| 03.11 | Đúng, có 3 điểm nhẹ | Chứng minh đầy đủ, hằng số $\tfrac14$, $\tfrac18$, $\tfrac17$ đúng, thứ tự lượng từ đúng ("với mọi $A$, tồn tại $D$"); vài chỗ nên nói rõ. |
| 03.12 | Đúng | Đẳng thức nâng chiều, các bình phương khoảng cách, bán kính và cách gán nhãn toàn $0$ đều đúng. |

Không có phát hiện mức `chặn bàn giao` hay `nghiêm trọng`.

## 2. Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 03.9, Gợi ý 1, dòng 637 | Điều kiện "khi và chỉ khi" sai: điều kiện nêu ra là đủ nhưng không cần. Hình chữ nhật $[\tfrac12,1]\times[-1,1]$ chứa $\mathbf e_1=(1,0)$ dù $a_1=\tfrac12>0$. Điều kiện đúng là $a_j\le1\le b_j$ và $a_l\le0\le b_l$ với mọi $l\ne j$. | "Hình chữ nhật chứa $\mathbf e_j$ khi và chỉ khi $b_j\ge1$ và $a_l\le0\le b_l$ với mọi $l$." | "Khi $a_l\le0\le b_l$ với mọi $l$, hình chữ nhật chứa $\mathbf e_j$ khi và chỉ khi $b_j\ge1$." (Lời giải Bước 1, dòng 651, đã dùng đúng dạng có điều kiện này.) |
| nhẹ | 03.8(b), Bước 3, dòng 621; Mục tiêu, dòng 565 | "Chặt" dễ bị đọc là "đạt dấu bằng" (cận chặt), trong khi ở đây nghĩa là dấu $<$. Ghi chú dùng "nghiêm ngặt" cho nghĩa này (ghi chú, Bước 2 chứng minh Mệnh đề 03.9), và Bài tập 03.1 dùng "đạt dấu bằng". "Có một điểm âm" nên là "có ít nhất một điểm âm". | "Bất đẳng thức thứ nhất chặt khi $C$ có ít nhất hai điểm không âm … Bất đẳng thức thứ hai chặt khi $C$ có một điểm âm" | Dòng 621: "Bất đẳng thức thứ nhất là nghiêm ngặt khi $C$ có ít nhất hai điểm không âm … Bất đẳng thức thứ hai là nghiêm ngặt khi $C$ có ít nhất một điểm âm". Dòng 565: "nhận ra khi nào mỗi bất đẳng thức của bổ đề Sauer–Shelah đạt dấu bằng và khi nào là nghiêm ngặt". |
| nhẹ | 03.8(c), dòng 623 | Mệnh đề 03.5 chỉ phát biểu $d=1$; chứng minh của nó chỉ chỉ ra $\{0\}$ bị tách trọn, không phải mọi tập một điểm. | "Theo Mệnh đề 03.5, mọi tập một điểm bị tách trọn" | "Mọi tập một điểm $\{x\}$ bị tách trọn, vì $h_x(x)=1$ và $h_{x+1}(x)=0$; theo Bước 2 của chứng minh Mệnh đề 03.5, không tập hai điểm nào bị tách trọn". |
| nhẹ | 03.6(d), Bước 1, dòng 488 | Từ $T_j(Y^*)=Y^*$ (đẳng thức tập hợp) chưa trực tiếp suy ra $T_j(y)=y$ với từng $y$. Cần phép đếm $w(T_j(Y))=w(Y)-k$ của (c): nếu có véc-tơ bị đổi thì $w$ giảm, nên hai tập khác nhau. | "Nếu $y\in Y^*$ và $y_j=1$ thì $T_j(y)=y$, tức $y^{(j)}\in Y^*$." | Thêm trước câu này: "Theo (c), $w(T_j(Y^*))=w(Y^*)-k$ với $k$ là số véc-tơ bị đổi; vì $T_j(Y^*)=Y^*$ nên $k=0$, tức $T_j$ không đổi véc-tơ nào của $Y^*$." |
| nhẹ | 03.4, đề, dòng 209 so với (c), dòng 215 và lời giải dòng 285–303 | Đề viết "Trong cả bài … $\epsilon$ là cận cho rủi ro vượt mức", nhưng ở (c) $\epsilon$ là độ lệch đều trong chứng minh Định lý 03.15 (theo §2 của ghi chú: $\epsilon$ là độ lệch đều ở §7). | "Trong cả bài, hàm lỗi là hàm lỗi 0–1, $\delta=0{,}05$, và $\epsilon$ là cận cho rủi ro vượt mức của mọi nghiệm ERM" | "Trong các phần (a), (b), (e), $\epsilon$ là cận cho rủi ro vượt mức …; trong (c), $\epsilon$ là độ lệch đều như trong chứng minh Định lý 03.15." |
| nhẹ | 03.4(b), Bước 2, dòng 270 | Tỉ số hai cỡ mẫu nhỏ nhất chỉ xấp xỉ tỉ số hai ngoặc (mỗi cỡ mẫu xấp xỉ $12\,800$ lần ngoặc, sai khác do làm tròn). Tính lại: $3{,}394323$ so với $3{,}394327$. | "Tỉ số bằng tỉ số của hai ngoặc $d\ln(2em/d)+\ln80$ tại hai nghiệm" | "Tỉ số xấp xỉ bằng tỉ số của hai ngoặc …, vì tại cỡ mẫu nhỏ nhất $m\approx12\,800\,(d\ln(2em/d)+\ln80)$." |
| nhẹ | 03.4(a), Bước 2, dòng 253 | Giá trị $0{,}0024999964$ bị cắt thành $0{,}00249999$; làm tròn tới tám chữ số thập phân lại cho $0{,}00250000$, nên con số ghi không cho thấy vế trái nhỏ hơn $0{,}0025$. | "vế trái bằng khoảng $0{,}00249999$ tại $m=589\,118$ và $0{,}00250000032$ tại $m=589\,117$" | "vế trái bằng khoảng $0{,}0024999964$ tại $m=589\,118$ và $0{,}0025000003$ tại $m=589\,117$". |
| nhẹ | 03.11(a), đề dòng 731 và lời giải dòng 770, 778 | UML 6.10(a) viết "for some D, for every sample size m", tức $D$ đứng trước $m$. Ở đây $D$ được chọn sau $A$ và $m$; đây là dạng mà chứng minh cho được, nhưng lời giải không nói rõ. Bước 3 cũng dùng việc $A(S)$ xác định bởi $S$ (thuật toán tất định theo Định nghĩa 01.4) mà không nêu. | "Chứng minh với mọi thuật toán học $A$, có một phân bố $D$ …"; "khi đó $S$ và $A(S)$ cố định." | Thêm cuối Bước 4: "Phân bố $D=D_f$ phụ thuộc $A$ và $m$. Bước 3 dùng việc $A(S)$ là hàm của $S$, như Định nghĩa 01.4 đòi." |
| nhẹ | 03.11, Gợi ý 1, dòng 745 | Gợi ý đầu tiên đã nêu ý chính của chứng minh (lấy trung bình theo nhãn ngẫu nhiên rồi chọn một $f$), nên phần (a) gần như chỉ còn tính toán. | "Chọn nhãn $f$ trên $C$ ngẫu nhiên, đều trên $\{0,1\}^C$, và chứng minh trung bình theo $f$ … ; khi đó có một $f$ đạt ít nhất trung bình." | Gợi ý 1: "Phần (a). Dùng lập luận của định lý không có bữa trưa miễn phí (Nhận xét 01.30; UML §5.1) trên tập $C$, với các phân bố đều trên $C$ và nhãn cho bởi các hàm thuộc lớp." Chuyển câu về trung bình theo $f$ sang đầu Gợi ý 2. |
| nhẹ | 03.11(d), dòng 799 | Khi $d\le1$ không có $m$ nào với $1\le m\le\lfloor d/2\rfloor$; kết luận vẫn đúng (vế phải bằng $1$, mà $m_{\mathcal H}\ge1$ theo định nghĩa) nhưng lời giải không nói. | "Lấy $m$ với $1\le m\le\lfloor d/2\rfloor$." | Thêm đầu đoạn: "Khi $d\le1$, vế phải bằng $1$ và bất đẳng thức đúng vì $m_{\mathcal H}(\epsilon,\delta)\in\mathbb N\cup\{\infty\}$. Giả sử $d\ge2$ và lấy $m$ với …" |
| nhẹ | 03.11(a), Bước 1 dòng 759 và Bước 3 dòng 773 | Chữ $X$ vừa chỉ một điểm ngẫu nhiên ("$(X,f(X))$") vừa chỉ cả bộ $(X_1,\ldots,X_m)$ trong kì vọng có điều kiện. | "$\mathbb E\big[L_{D_F}(A(S))\mid X,F\vert_V\big]$" | Viết "$\mathbb E\big[L_{D_F}(A(S))\mid X_1,\ldots,X_m,F\vert_V\big]$". |
| nhẹ | Ghi chú §10, mục 4–5, so với tiêu đề Bài tập 03.4, 03.5 (dòng 204, 346) | Tiêu đề trong danh sách của ghi chú khác tiêu đề trong tệp bài tập. | Ghi chú: "So sánh cỡ mẫu cho hai chiều VC", "Số tham số không xác định chiều VC"; tệp bài tập: "So sánh cỡ mẫu theo chiều VC và nguồn gốc hằng số $8$", "Số tham số, lớp chọn sau khi xem mẫu và chiều VC". | Thống nhất một bộ tiêu đề; nếu giữ tiêu đề của tệp bài tập thì sửa hai dòng tương ứng ở §10 của ghi chú (việc này thuộc phạm vi ghi chú, chủ trì quyết định). |

**Thống kê:** `chặn bàn giao` 0, `nghiêm trọng` 0, `trung bình` 1, `nhẹ` 11.

## 3. Các điểm được yêu cầu chú ý đặc biệt

- **03.4.** Cỡ mẫu tại $\epsilon=0{,}05$ đúng ($589\,118$; $1\,999\,657$; $944\,961$; $3\,165\,709$). Hằng số $8$: số mũ $-2m(\epsilon/2)^2/2^2=-m\epsilon^2/8$, hai thừa số $4$ đến từ chia đôi độ lệch (Bước 1) và miền dài $2$ (Bước 4), tỉ số $2:\tfrac18=16$ đúng. Dùng Hoeffding ở Bước 1 cần $m\epsilon^2\ge2\ln4\approx2{,}77$ (chặt hơn $m\epsilon^2\ge2$ của Chebyshev) và vẫn thỏa tại $\epsilon=\rho_m$ vì $m\rho_m^2>8\ln4$; $\rho_m$ không đổi: đúng. Lập luận bỏ mẫu bóng cho $0{,}590$ trong khi độ lệch thật bằng $1$ trên mọi mẫu: đúng, và chỗ sai được quy đúng về lý do (i), (ii). So sánh với rời rạc hóa: $27\,355$, tỉ số $4{,}86=16\cdot0{,}3039$: đúng.
- **03.5(d).** Lớp một hàm chọn sau khi xem mẫu: $d=0$, $L_S=0$ và $L_D=\tfrac12$ hầu chắc chắn (cần các $X_i$ đôi một khác nhau, đã nêu), $\rho_{1000}\approx0{,}187<\tfrac12$, cận Hoeffding cho hàm cố định $\approx0{,}043$. Giả thiết bị vi phạm là (T5), khớp chỗ dùng (T5) ở Bước 3 của chứng minh Định lý 03.15 và Ví dụ 03.8.
- **03.6.** Đơn ánh, $\operatorname{sh}$ không tăng (hai trường hợp $i\notin B$, $i\in B$), hàm thế $w$ giảm, tính đóng khi giảm và phép đếm đều đúng; kiểm ngẫu nhiên $3000$ tập $Y$ với $n\le5$ cho thấy mọi khẳng định (a)–(d) đúng. Điểm nhẹ duy nhất ở bảng trên.
- **03.8(a).** Quy nạp theo $n$ đồng thời cho mọi lớp khác rỗng, có trường hợp gốc $n=0$ (khớp quy ước $\{0,1\}^0$ của Phụ lục B), lớp con $\mathcal H_1$ khác rỗng với $(\mathcal H_1)_{C'}=Y_1$, ánh xạ $B\mapsto B\cup\{x\}$ là đơn ánh vào họ tách trọn chứa $x$, hai họ rời nhau: đầy đủ. Kiểm ngẫu nhiên $2000$ lớp trên $n\le5$ điểm cho chuỗi $\lvert\mathcal H_C\rvert\le\lvert\operatorname{sh}\rvert\le\sum_{j\le d}\binom nj$ luôn đúng.
- **03.11.** Họ $D_f$ khả thực; cận $\mathbb E[L_{D_F}(A(S))\mid\cdot]\ge(k-\lvert V\rvert)/(2k)\ge(k-m)/(2k)$ đúng; phương pháp xác suất cho một $f$; bất đẳng thức kiểu Markov ngược với $\mu=\tfrac14$, $a=\tfrac18$ cho $\tfrac17$; với PAC dùng $\epsilon=\delta=\tfrac18$ và $m=M(\tfrac18,\tfrac18)\ge1$, nên $k=2m\ge2>m$; $\Pr[L\le\tfrac18]\le\tfrac67<\tfrac78$: mâu thuẫn đúng. (d) đúng theo Định nghĩa 01.20 (chỉ cần $m=\lfloor d/2\rfloor$ thất bại). Lớp PAC bất khả tri được loại qua Nhận xét 01.26 (kiểm nội dung: học PAC bất khả tri kéo theo học PAC khả thực, cùng $M$). Kiểm số: với $(k,m)\in\{(2,1),(3,1),(4,2),(4,3),(5,2)\}$, trung bình theo $f$ của rủi ro kì vọng của các thuật toán tất định ngẫu nhiên và của thuật toán ghi nhớ luôn $\ge(k-m)/(2k)$.
- **03.12.** $w=(2v,-1)$, $b=r^2-\lVert v\rVert^2$ cho đúng tương đương (kiểm $1000$ điểm ngẫu nhiên); bình phương khoảng cách $a$, $a-1$, $a+1$; $r^2=a\pm\tfrac12>0$ trong hai trường hợp; toàn $0$ dùng $v=-3\mathbf e_1$, $r=1$ với khoảng cách $3$, $4$, $\sqrt{10}$; vét cạn với $p\le4$ cho mọi $2^{p+1}$ cách gán nhãn đúng.

## 4. Đối chiếu với UML và sách lời giải

- **Số hiệu và nội dung:** 03.7 = UML 6.2, 03.8 = 6.4, 03.9 = 6.5, 03.10 = 6.6, 03.11 = 6.10, 03.12 = 9.6: đúng số và đúng nội dung. Các phần thêm (03.8(a), (c); 03.10(b) phần $p=1$; 03.11(b), (d)) không mâu thuẫn với bản gốc. Quy ước $\operatorname{sign}(0)=1$ của UML 9.6 khớp quy ước $\ge0$. Lớp $\mathcal H^p_{\mathrm{rec}}$ có thêm $h_\varnothing$, theo Bài tập 02.7; không ảnh hưởng chiều VC. Số chiều đặc trưng viết $p$ ở cả 03.9, 03.10, 03.12.
- **Không chép sách lời giải.** Lời giải của chúng ta khác sách ở các điểm chính: 03.7(b) đáp số đúng $\min\{2k+1,n\}$ (sách ghi $k$); 03.8 dùng một lớp hai hàm cho cả bốn tổ hợp (sách dùng bốn lớp khác nhau); 03.10(c) dùng phủ định của biến (cách của sách với $\bigwedge_{j\in J}x_j$ không thực hiện đúng cách gán nhãn khi $\lvert J\rvert\ge2$); 03.11 dùng $\epsilon=\delta=\tfrac18$ và cận $>\tfrac18$ (sách dùng $\tfrac1{16}$, $\tfrac1{14}$). Ở 03.12(b), tâm $\sum_{\mathbf e_i\in A}\mathbf e_i$ và độ lệch $\pm\tfrac12$ trùng ý với sách (đây là phép dựng chuẩn), nhưng chúng ta đặt $r^2$, còn sách đặt $r$ (sai), và câu chữ khác hẳn. Không phát hiện đoạn diễn đạt lại sát sách.

## 5. Phụ lục: các số và khẳng định đã kiểm

Mọi phép tính chạy bằng `/data/tqlong/lectures/.venv/bin/python -I` trong `scratchpad/rev9/`. "Đạt" nghĩa là khớp con số hoặc khẳng định ghi trong tệp đóng băng.

**03.1.** $\Pi_{\mathcal H_6}(m)$, $m=1..8$: $2,3,4,5,6,6,6,6$ (vét cạn trên bộ có lặp) đạt; $\Pi(3)=4$, $\Pi(8)=6$ đạt; dấu bằng Sauer đúng tại $m=1..5$ đạt. $\Pi_{\mathcal H^\pm_{\mathrm{thr}}}(m)=2m$, $m=1..7$ (vét cạn, có lặp) đạt; chiều VC $=2$ đạt; bảng $(2,2,2)$, $(4,4,4)$, $(6,7,8)$, $(20,56,1024)$ đạt; dấu bằng Sauer chỉ tại $m=1,2$ (giải $m^2-3m+2=0$) đạt; trên $(1,2,3)$ thiếu đúng $010$, $101$ đạt.

**03.2.** Bốn khoảng mở cho $(1,1)$, $(1,0)$, $(0,1)$, $(0,0)$ đạt; chiều VC khoảng mở $=2$ đạt; lưới bước $\tfrac12$ trên $[0,6]$: $\{1,..,4\}$ có $16$, $\{1,..,5\}$ có $31$ và thiếu đúng $(1,0,1,0,1)$ đạt; $31=\sum_{j\le4}\binom5j$ đạt; $200$ tập năm điểm ngẫu nhiên, $(1,0,1,0,1)$ không thực hiện được đạt.

**03.3.** Công thức $b=2y_0-1$, $w_i=2y_i-1-b$ đúng với mọi cách gán nhãn, $p=1..4$ đạt; $w=(2,0,2)$, giá trị $-1,1,-1,1$ đạt; hệ $p=2$ cho $(w_1,w_2,b)=(-2,0,3)$, giá trị $1,-1,1$ đạt; kiểm $p=1$: $b=1$, $w=-2$ đạt.

**03.4.** $\ln80=4{,}38203$ đạt. Cỡ mẫu trực tiếp $\epsilon=0{,}05$: $589\,118$ ($d=3$), $1\,999\,657$ ($d=11$) đạt; vế trái tại $589\,118$ và $589\,117$: $0{,}0024999964$ và $0{,}0025000003$ (xem phát hiện nhẹ). Kiểm thêm $\epsilon=0{,}1$: $54\,330$, $132\,992$, $447\,194$ khớp Ví dụ 03.9. Dạng đóng: $64/\epsilon^2=25\,600$, $128/\epsilon^2=51\,200$, $\ln51\,200=10{,}8435$, ngoặc $36{,}9125$ và $123{,}6605$, tích $944\,960{,}28$ và $3\,165\,708{,}02$, làm tròn lên $944\,961$, $3\,165\,709$ đạt. Tỉ số theo $d$: $3{,}3943<3{,}6667$ đạt; ngoặc $46{,}025$ và $156{,}223$, $\ln(2em/d)=13{,}881$ và $13{,}804$, $m/d=196\,372{,}7$ và $181\,787$ đạt. Tỉ số theo $\epsilon$: $4{,}430$ và $4{,}472$, $\ln4{,}43=1{,}488$ đạt; ngoặc tăng $10{,}7\%$ ($d=3$) và $11{,}8\%$ ($d=11$), "khoảng $10\%$" chấp nhận được. (c): $2\ln4=2{,}773$, $8\ln4=11{,}090$, số mũ $-m\epsilon^2/8$, tỉ số $16$ đạt. (d): $1000\ln2=693{,}147$, $\ln40=3{,}689$, $0{,}34842$, căn $0{,}5903$, $\sqrt{16\ln2}=3{,}330$ đạt. (e): $193\ln2=133{,}777$, $\ln20=2{,}996$, tổng $136{,}773$, $200\cdot136{,}773=27\,354{,}63$, làm tròn lên $27\,355$, tỉ số $4{,}862$ đạt; ngoặc tại $132\,992$: $37{,}178+4{,}382=41{,}560$, $32\cdot41{,}560/(2\cdot136{,}773)=4{,}862=16\cdot0{,}3039$ đạt; $32\cdot41{,}560/0{,}01=132\,991{,}2$ đạt.

**03.5.** Phép dựng $\theta$: với mọi $k\le14$ và mọi $y\in\{0,1\}^k$, tính chính xác $\theta x_i/\pi$ bằng phân số, phần lẻ thuộc $(0,1)$ và tính chẵn lẻ của phần nguyên cho đúng $y_i$ (tổng $2^{15}-2$ cách gán nhãn) đạt; $\sum_{j=1}^{i-1}2^{j-i}=1-2^{1-i}$ nên $f_i\le1-2^{-i}$ đạt; $y=(1,0,1)\Rightarrow\theta=5\pi$, sin $1$, $-0{,}707$, $0{,}924$ đạt; $y=(0,1,1)\Rightarrow\theta=3\pi$ đạt. (b): đúng ba hàm theo dấu của $s$ đạt. (d): $8\ln80/1000=0{,}035056$, $\rho=0{,}1872$ đạt; $\sqrt{\ln40/2000}=0{,}0429$ đạt.

**03.6.** $3000$ tập $Y$ ngẫu nhiên, $n\le5$: $T_i$ đơn ánh, $\operatorname{sh}(T_i(Y))\subseteq\operatorname{sh}(Y)$, điểm dừng đóng khi giảm, $\lvert Y\rvert\le\lvert\operatorname{sh}(Y)\rvert$ đạt; ví dụ $Y=\{00,10,11\}$: $T_1(Y)=\{00,10,01\}$, cố định với $T_2$, $\lvert\operatorname{sh}(Y)\rvert=3$ đạt; $(e/2)^{10}=21{,}510<32$ đạt.

**03.7.** Vét cạn mọi $n\le7$, mọi $0\le k\le n$: $\operatorname{VCdim}(\mathcal H_{=k})=\min\{k,n-k\}$ và $\operatorname{VCdim}(\mathcal H^\pm_{\le k})=\min\{2k+1,n\}$ đạt; ví dụ $n=5$, $k=1$: $1$ và $3$ đạt.

**03.8.** $\operatorname{VCdim}(\mathcal G)=1$ đạt; bảng $(\lvert\mathcal G_C\rvert,\lvert\operatorname{sh}\rvert,1+n)$: $(2,2,2)$, $(2,3,3)$, $(2,2,3)$, $(2,3,4)$ đạt; $\{-2,-1,1,2\}$: $(2,3,5)$ đạt; $2000$ lớp ngẫu nhiên thỏa (a) đạt; hàm ngưỡng, $n\le6$: $n+1=n+1=n+1$ đạt.

**03.9.** Cận dưới với $a_j\in\{-1,-\tfrac12\}$, $b_j\in\{1,\tfrac12\}$, mọi cách gán nhãn, $p=1,2,3$ đạt; tập $2p+1$ điểm ngẫu nhiên ($p=1,2$) không bị tách trọn đạt; phản ví dụ cho Gợi ý 1: $[\tfrac12,1]\times[-1,1]\ni\mathbf e_1$ xác nhận.

**03.10.** $\lvert\mathcal H^p_{\mathrm{conj}}\rvert=4,10,28,82=3^p+1$; chiều VC $2,2,3,4$ với $p=1..4$ đạt; tách trọn $\{\mathbf e_j\}$ đạt; $\lvert\mathcal H^p_{\mathrm{mon}}\rvert=2^p+1$, chiều VC $p$, tách trọn $\{\mathbf 1-\mathbf e_j\}$ đạt; $3^p+1\bmod8\in\{2,4\}$ ($p\le99$) và $3^p+1$ không là lũy thừa của $2$ với $2\le p\le200$ đạt.

**03.11.** $(\tfrac14-\tfrac18)/(1-\tfrac18)=\tfrac17$ đạt; $(2m-m)/(4m)=\tfrac14$ đạt; cận trung bình $(k-m)/(2k)$ trên năm cặp $(k,m)$ đạt; $\lfloor11/2\rfloor+1=6$ đạt; kiểm tra $k=2$, $m=1$: $\tfrac14$ đạt.

**03.12.** Đẳng thức nâng chiều ($1000$ điểm ngẫu nhiên, $p\le4$) đạt; tách trọn $\{0,\mathbf e_1,\ldots,\mathbf e_p\}$ với tâm và bán kính đã cho, $p\le4$ đạt; khoảng cách $3$, $4$, $\sqrt{10}$ đạt.

**Tổng:** khoảng $130$ con số và khẳng định được tính lại hoặc kiểm vét cạn (42 phép kiểm tổ hợp tự động, cộng các phép tính số ở `num.py`); không phát hiện sai số nào trong các con số của tệp.
