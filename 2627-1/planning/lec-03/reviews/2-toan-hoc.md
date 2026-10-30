# Rà soát 2/5: độ chính xác toán học, Bài 03 (bản nháp đóng băng)

**Tệp được rà soát:** `lec03-draft-frozen.md` (1123 dòng), trong scratchpad của phiên.
**Vai trò:** người rà soát độc lập về độ chính xác toán học, chỉ đọc. Không sửa tệp nào trong repo, không commit.
**Đối chiếu:** ghi chú Bài 01 và Bài 02 (`2627-1/materials/lec-0{1,2}/lecture-note.md`), Bài tập 02.7 (`lec-02/exercises.md`), PDF UML (trang 61–62, 72–73, 78–82, 121, 392, 395–396, 400–401). Mọi phép tính số chạy bằng Python trong `scratchpad/lec03calc/calc.py` và `calc2.py`, không chạy trong repo.

## Kết luận chung

**Đạt về toán học, kèm các sửa nhỏ.** Không có phát hiện ở mức `chặn bàn giao` hay `nghiêm trọng`. Tôi tự chứng minh lại mọi định nghĩa, mệnh đề, bổ đề, định lý và hệ quả, kể cả bốn phụ lục, và mọi bước đều đúng: lượng từ, trường hợp biên, bất đẳng thức chặt và không chặt, các hằng số $4$, $8$, $16/32$, $64/128$, $1/8$, $1/7$. Mọi con số trong mười ví dụ, hai bảng, các tỉ số, câu hỏi ôn nhanh và câu hỏi cuối buổi đều khớp với phép tính lại (khoảng 126 giá trị, liệt kê ở Phụ lục). Mọi khối của Bài 01 và Bài 02 được dẫn đều tồn tại và nói đúng điều ghi chú gán cho chúng.

Có một lỗi trích dẫn ở mức `trung bình`: UML §28.3 bị gọi là cận dưới. Mười hai phát hiện `nhẹ` liên quan đến cách phát biểu: điều kiện ngầm (tính đo được của từng hàm phân lớp, sự tồn tại một thuật toán ERM đo được, (M) trong các câu tóm tắt), một lời giải còn thiếu nhãn cho các điểm còn lại, và vài câu chỉ đúng trong một trường hợp.

**Số phát hiện:** chặn bàn giao 0, nghiêm trọng 0, trung bình 1, nhẹ 12.

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | §12 Tài liệu đọc, mục "Mở rộng", dòng 910 | UML §28.3 là cận trên cho trường hợp khả thực, không phải cận dưới. UML chỉ chứng minh cận dưới bất khả tri (§28.2); cận dưới khả thực, tức Định lý 03.19(b), là một bài tập của chương. | Dòng 910: "§28.2–28.3: cận dưới". UML tr. 392: "We shall prove the upper bound for both the realizable and agnostic cases and shall prove the lower bound for the agnostic case. The lower bound for the realizable case is left as an exercise." Tiêu đề UML tr. 401: "28.3 The Upper Bound for the Realizable Case". | Thay bằng: "§28.2: cận dưới cho trường hợp bất khả tri; cận dưới cho trường hợp khả thực là bài tập của chương; §28.3: cận trên cho trường hợp khả thực". |
| nhẹ | §11, Lời giải câu hỏi chính, dòng 897 | Một cách gán nhãn phải cho nhãn ở cả năm điểm. Khi một điểm vừa có hoành độ nhỏ nhất vừa có tung độ nhỏ nhất, số điểm được chọn ít hơn bốn và có thể còn lại hai điểm, nhưng lời giải chỉ gán nhãn cho $x$. Lập luận vẫn đúng khi gán $0$ cho mọi điểm không được chọn. | "Gán nhãn $1$ cho các điểm được chọn và $0$ cho $x$." | "Gán nhãn $1$ cho các điểm được chọn và nhãn $0$ cho mọi điểm còn lại, trong đó có $x$." |
| nhẹ | §1 mục 3–4, dòng 60–61 | (T2) đòi $\ell(h,\cdot)$ đo được với mọi $h$, tức mỗi $h$ phải đo được, nhưng mục 3 chỉ nói "các hàm phân lớp". Bài 01 (Định nghĩa 01.1, (T2)) đòi điều này. Đoạn sau (M) (dòng 490) cũng dùng tính đo được của $h_k$ khi viết $L_D(h_k)$. | Dòng 60: "$\mathcal H$ gồm các hàm phân lớp (classifier) $\mathcal X\to\{0,1\}$"; dòng 61: "nó thỏa (T2) và (T3)". | Dòng 60: "$\mathcal H$ gồm các hàm phân lớp (classifier) đo được $\mathcal X\to\{0,1\}$". |
| nhẹ | §7, đoạn sau (M), dòng 490 | Khẳng định không có cơ sở trong các nguồn được giao. Khẳng định này đúng (có phản ví dụ, chẳng hạn của Blumer và cộng sự 1989, dưới giả thuyết continuum), nhưng ghi chú không dẫn nguồn. | "Không có một điều kiện như vậy, các kết luận dưới đây có thể sai với những lớp bệnh lý." | Thay bằng: "Bài không xét các lớp không thỏa một điều kiện như vậy." Hoặc giữ câu cũ và dẫn một nguồn mà tác giả duyệt. |
| nhẹ | §9, đoạn cuối, dòng 869 | Bài chỉ dùng (M) như một điều kiện đủ (Bước C.1), không chứng minh (M) là cần. Chữ "cần" dễ đọc thành tính cần. | "Điều kiện (M) cần cho chiều đủ của Định lý 03.17." | "Điều kiện (M) được dùng cho chiều đủ của Định lý 03.17, tại Bước C.1." |
| nhẹ | Dòng 784 (trước Định lý 03.17) và dòng 861 (§9) | Câu tóm tắt bỏ (M) và giả thiết có một thuật toán ERM đo được, trong khi Định lý 03.15, Hệ quả 03.16 và Định lý 03.17(b) đều cần hai điều này. | Dòng 784: "chiều VC hữu hạn kéo theo học được"; dòng 861: "Một lớp vô hạn học được khi chiều VC của nó hữu hạn". | Dòng 784: "dưới (M), chiều VC hữu hạn kéo theo học được." Dòng 861: "Dưới (M), một lớp vô hạn học được khi chiều VC của nó hữu hạn". |
| nhẹ | Hệ quả 03.16(c), dòng 702 | Câu "do đó $\mathcal H$ học được PAC bất khả tri" cần ít nhất một thuật toán ERM thỏa Định nghĩa 01.4. Dòng 707 nói đây là giả thiết. Định lý 03.17 ghi rõ giả thiết này (dòng 791), còn Hệ quả 03.16 chỉ ngầm hiểu. | "do đó $\mathcal H$ học được PAC bất khả tri và $m_{\mathcal H}(\epsilon,\delta)\le M(\epsilon,\delta)$." | "khi có ít nhất một thuật toán ERM như vậy, $\mathcal H$ học được PAC bất khả tri và $m_{\mathcal H}(\epsilon,\delta)\le M(\epsilon,\delta)$." |
| nhẹ | Định lý 03.17(a), dòng 798–800; dòng 816 | UML Định lý 5.1 phát biểu $L_D(A(S))\ge1/8$ với xác suất ít nhất $1/7$. Bản nháp viết $>1/8$, một dạng mạnh hơn. Dạng này đúng: từ $\mathbb E[L_D(A(S))]\ge1/4$ (UML (5.2)) và $L_D\in[0,1]$, ta có $\tfrac14\le\tfrac18+\tfrac78\Pr(L_D>\tfrac18)$, nên $\Pr(L_D>\tfrac18)\ge\tfrac17$. Bài dẫn UML và không tự chứng minh, nên người đọc đối chiếu sẽ thấy khác. | "$\Pr_{S\sim D^m}\big[L_D(A(S))>1/8\big]\ge1/7$"; UML tr. 61: "With probability of at least 1/7 … $L_D(A(S))\ge1/8$". | Thêm vào dòng 816, sau "(Nhận xét 01.30; UML §5.1)": "UML phát biểu với $L_D(A(S))\ge1/8$; dạng $>1/8$ suy ra từ cùng cận $\mathbb E[L_D(A(S))]\ge1/4$ của chứng minh đó." Cũng có thể đổi thành $\ge1/8$ ở dòng 798 và 823; lập luận ở dòng 814 vẫn đúng vì $\epsilon<1/8$. |
| nhẹ | Ví dụ 03.4, Bước 1, dòng 368 | Hai cách gán nhãn toàn $1$ và toàn $0$ cần ngưỡng $t\le x_1$ và $t>x_m$, không nằm giữa hai điểm liên tiếp. | "mỗi số đó thực hiện được bằng một ngưỡng đặt giữa hai điểm liên tiếp" | "mỗi số đó thực hiện được bằng một ngưỡng $t\le x_1$, $t>x_m$ hoặc $t\in(x_{i-1},x_i]$" |
| nhẹ | Định lý 03.15, đoạn cuối khối, dòng 577 | Tốc độ $\sqrt{\ln m/m}$ chỉ đúng khi $d\ge1$. Khi $d=0$, dòng 580 cho tốc độ $\sqrt{1/m}$. | "giảm theo $m$ như $\sqrt{\ln m/m}$" | "khi $d\ge1$, giảm theo $m$ như $\sqrt{\ln m/m}$" |
| nhẹ | Nhận xét 03.13, dòng 493 | Khi $t$ hữu tỉ, một dãy không tăng ngặt có thể dừng tại $t$ và vẫn hội tụ đúng. Câu phủ định chỉ đúng với dãy $t_k>t$. | "Dãy giảm $t_k\downarrow t$ không dùng được, vì nó hội tụ về $\mathbb 1[x>t]$" | "Dãy $t_k\downarrow t$ với $t_k>t$ không dùng được, vì nó hội tụ về $\mathbb 1[x>t]$" |
| nhẹ | Phụ lục C, Bước C.1 và C.3, dòng 1017–1026 và 1055 | C.3 và C.4 dùng xác suất của $\{\sup_h\lvert\frac1m\sum_i\sigma_ia_i(h)\rvert>\epsilon/2\}$ và định lý Fubini theo $(S,S',\sigma)$, nhưng C.1 chỉ quy về $\mathcal H_0$ hai cận trên đúng không có dấu. Cùng lý do (hữu hạn điểm) áp dụng được ngay. | C.1 chỉ liệt kê "$\sup_{h}\lvert L_S(h)-L_D(h)\rvert$" và "$\sup_{h}\lvert L_{S'}(h)-L_S(h)\rvert$". | Thêm vào cuối câu "đẳng thức thứ hai đúng vì …" ở C.1: "; cùng lý do cho $\sup_h\lvert\frac1m\sum_i\sigma_ia_i(h)\rvert=\sup_k\lvert\frac1m\sum_i\sigma_ia_i(g_k)\rvert$ với mọi $\sigma\in\{-1,1\}^m$." |
| nhẹ | Kiến thức tiên quyết, dòng 31 | Nhận xét 02.8 được liệt kê nhưng không dùng ở đâu. Câu ôn nhanh 3, Bước 4 và Bước C.4 đều dùng Định lý 02.7(c) với đoạn chung $[-1,1]$, nên áp dụng trực tiếp được. | "bất đẳng thức Hoeffding (Định lý 02.7) với miền giá trị khác nhau (Nhận xét 02.8)" | "bất đẳng thức Hoeffding (Định lý 02.7) với miền giá trị $[a,b]$ tổng quát" |

**Ngoài phạm vi toán học, ghi để master biết.** Dòng 873 dẫn tới `materials/lec-03/exercises.md`, và các chứng minh dẫn Bài tập 03.3 (dòng 292) và 03.5 (dòng 337), nhưng `2627-1/materials/lec-03/` hiện chỉ có `lecture-note.md`. Các ánh xạ sang bài tập UML ở §10 (6.2, 6.4, 6.5, 6.6, 6.10, 9.6) khớp với UML tr. 78–82 và 129.

## Kiểm chứng theo khối

Phần này ghi những gì tôi tự chứng minh lại. "Đúng" nghĩa là tôi tự dựng lại lập luận và không thấy lỗi.

**Định nghĩa.**
- **03.1.** $k\ge1$, cho phép điểm lặp. $\lvert\mathcal H_C\rvert\le\min\{\lvert\mathcal H\rvert,2^k\}$ đúng.
- **03.2.** Cần quy ước tập rỗng vì Định nghĩa 03.1 đòi $k\ge1$, và quy ước được nêu. Tính chất tập con (dòng 171) đúng.
- **03.3.** Có trường hợp $d=\infty$. Hai khẳng định "$d=0$ khi và chỉ khi mọi hàm trùng nhau" và "$d\le\log_2\lvert\mathcal H\rvert$" đúng.
- **03.7.** Quy ước $\ge0$; với $w=0$ được hàm hằng. Mô tả trường hợp $p=1$ (dòng 256) đúng.
- **03.11.** Giá trị lớn nhất tồn tại vì tập giá trị hữu hạn. Các tính chất đúng: không giảm, $\le\min\{2^m,\lvert\mathcal H\rvert\}$, $\Pi(m)=2^m\iff m\le d$ (dòng 363, cả hai chiều).
- **03.14.** Lượng từ $\exists M\,\forall\epsilon,\delta\,\forall D\,\forall m\ge M$. Định nghĩa đòi tính đo được của $E_m(D,\epsilon)$, và tập này dùng "$\le\epsilon$", khớp Định nghĩa 02.13. Với lớp hữu hạn, $m^{UC}\le\lceil\ln(2K/\delta)/(2\epsilon^2)\rceil$, khớp Định lý 02.14(c).

**Mệnh đề 03.5 và 03.6.** Cận dưới và cận trên đều đúng, kể cả trường hợp (b) trên $\{1,\ldots,5\}$. Khoảng $[2,2]$ cho cách gán nhãn $(0,0)$. Khẳng định "hàm hằng $0\notin\mathcal H_{\mathrm{int}}$" đúng vì $u\le v$ luôn cho một khoảng khác rỗng.

**Bổ đề 03.8 (Phụ lục A).** Hệ có $p+1$ phương trình và $p+2$ ẩn. Với $I=\{a_i>0\}$ và $J=\{a_j\le0\}$, cả hai tập khác rỗng vì $a\ne0$ và $\sum a_i=0$. Các hệ số $a_i/A$ và $-a_j/A$ không âm và có tổng $1$. Lập luận đúng cả khi có điểm trùng nhau.

**Mệnh đề 03.9.**
- **(a), cận dưới.** Với $b=2y_0-1$ và $w_i=2y_i-1-b$, ta có $\langle w,\mathbf e_i\rangle+b=2y_i-1$.
- **(a), cận trên.** $g$ là hàm afin nên $g(\sum\lambda_ix_i)=\sum\lambda_ig(x_i)$ khi $\sum\lambda_i=1$. Phía chặt nằm trên $J\ne\varnothing$. Một số $\mu_j$ có thể bằng $0$, nhưng $\sum\mu_j=1$ nên $\sum\mu_jg(x_j)<0$.
- **(b), cận dưới.** $w=\sum(2y_i-1)\mathbf e_i$.
- **(b), cận trên (Phụ lục A).** Hai trường hợp đúng. Khi $J\ne\varnothing$, vế trái $\ge0$ và vế phải $<0$. Khi $J=\varnothing$, $\sum_Ia_i\langle w,x_i\rangle<0$ nhưng bằng $\langle w,\sum_ia_ix_i\rangle=0$. Lập luận vẫn đúng khi có $x_i=0$.

**Nhận xét 03.10.** (ii): tập $\{2^{-1},\ldots,2^{-k}\}$ bị tách trọn. Tôi kiểm bằng $\theta=\pi\big(1+\sum_j(1-y_j)2^j\big)$. Khi đó $\theta x_i\equiv(1-y_i)\pi+r_i\pmod{2\pi}$ với $r_i=\pi\big(2^{-i}+\sum_{j<i}(1-y_j)2^{j-i}\big)\in(0,\pi)$, vì các số hạng $j>i$ là bội của $2\pi$. (iii): có ba hàm, $d=1$. Cả hai đều đúng.

**Bổ đề 03.12.**
- **Phác thảo.** Đẳng thức $\lvert\mathcal H_C\rvert=\lvert\mathcal H_{C'}\rvert+\lvert Y_1\rvert$ đúng, và Pascal được áp dụng cho từng $j\ge1$.
- **Phụ lục B.** Hai trường hợp gốc $n=0$ ($\Phi(0,d)=1$) và $d=0$ đúng. Bước 4 đúng: $Y'$ không tách trọn $d+1$ vị trí, còn $Y_1$ không tách trọn $d$ vị trí. Với quy ước đã nêu, Pascal đúng cả khi $j\ge n$ ($j=n$: $0+1=1$; $j>n$: $0+0=0$). Quy nạp theo $n$ cho mọi $d$ cùng lúc là hợp lệ. Bước 6 đúng: hai vị trí có cùng điểm không thể bị tách trọn. Trường hợp $x_m$ trùng một điểm trước nó cho $Y_1=\varnothing$.
- **(b).** Bốn bước đúng, và giả thiết $d\le m$ được dùng đúng chỗ. Phản ví dụ $m=1$, $d=3$ đúng.

**Điều kiện (M), Nhận xét 03.13, Phụ lục D.**
- **Cận trên đúng trên $\mathcal H$ bằng trên $\mathcal H_0$.** $\mathcal H_0\subseteq\mathcal H$ cho chiều $\ge$. Với chiều $\le$, $h_k$ trùng $h$ trên mọi điểm của mẫu khi $k$ đủ lớn, và $L_D(h_k)\to L_D(h)$ theo định lý hội tụ bị chặn.
- **Hàm ngưỡng.** Dãy $t_k\uparrow t$ cho kết quả đúng.
- **Khoảng.** $u_k\le u\le v\le v_k$, đúng.
- **Nửa không gian.** $g_k\ge g+1/k-\lVert x\rVert/k^2\ge g$ khi $k\ge\lVert x\rVert$, và $g_k\le g+2/k+\lVert x\rVert/k^2\to g$. Các điểm trên siêu phẳng giữ nhãn $1$.

**Định lý 03.15 và Phụ lục C.**
- **C.1.** Trên $A$ có $k$ với $\lvert L_S(g_k)-L_D(g_k)\rvert>\epsilon$, vì cận trên đúng chặt $>\epsilon$ đạt được trên $\mathcal H_0$. Mỗi tập $\{h_S=g_k\}$ đo được. Phép chọn này làm định lý Fubini ở C.2 hợp lệ, vì $h_S$ chỉ nhận đếm được giá trị trên các tập đo được.
- **C.2.** Bổ đề 02.3(b) với $\sigma^2=1/4$ và độ lệch $\epsilon/2$ cho $1/(m\epsilon^2)\le1/2$. Biến cố bù có dạng chặt $<\epsilon/2$, và bất đẳng thức tam giác cho $>\epsilon/2$. Do đó $\Pr(W)\ge\tfrac12\Pr(A)$. Chiều chặt và không chặt nhất quán: $A$ dùng $>\epsilon$, $W$ dùng $>\epsilon/2$, Hoeffding dùng $\ge\epsilon/2\supseteq$.
- **C.3.** Theo (T1), mỗi cặp có phân bố $D\otimes D$, đối xứng. Với $\sigma$ cố định, phép đổi chỗ giữ nguyên phân bố đồng thời của toàn bộ quá trình theo $h$, rồi lấy trung bình theo $\sigma$.
- **C.4.** Véc-tơ $a_i(h)=\mathbb 1[h(x'_i)\ne y'_i]-\mathbb 1[h(x_i)\ne y_i]$ chỉ phụ thuộc cách gán nhãn trên $2m$ điểm, nên có nhiều nhất $\Pi(2m)$ véc-tơ. $\sigma_ia_i\in[-1,1]$ có kì vọng $0$. Định lý 02.7(c) cho $2\exp(-2m(\epsilon/2)^2/4)=2e^{-m\epsilon^2/8}$, và Bổ đề 02.12 lấy hợp trên một tập hữu hạn.
- **C.5.** Với $\epsilon=\rho_m$, vế phải bằng $\delta$. $m\rho_m^2=8\ln(4\Pi/\delta)>8\ln4\approx11{,}09\ge2$.
- **C.6.** $d\le2m$, nên $\Pi(2m)\le(2em/d)^d$. Từ $\ln(em/d)\ge1$ suy ra $d\ln(2em/d)\le(1+\ln2)\,d\ln(em/d)$. Ngoài ra $\ln(4/\delta)\le2\ln(2/\delta)$ và $1+\ln2\approx1{,}693<2$, cho hằng số $4$.
- **C.7.** Với $\kappa=8/\epsilon^2$ và $a_0=4e\kappa$, ta có $a/a_0=m/(2\kappa d)$ và $\ln a_0-1=\ln4\kappa$. $2\kappa=16/\epsilon^2$ và $4\kappa=32/\epsilon^2$. Từ $2\kappa\ln4\kappa>48>1$ suy ra $m\ge d$, nên điều kiện Sauer được thỏa. Tôi kiểm thêm bằng số trên lưới $\epsilon\in\{0{,}9;0{,}5;0{,}1;0{,}01\}$, $d\in\{1,5,100\}$, $\delta\in\{0{,}9;0{,}05;10^{-6}\}$: dạng đóng luôn $\ge d$ và cho $\rho_m\le\epsilon$.
- **Các trường hợp biên.** Khi $d=\infty$, $\rho_m\ge\sqrt{16\ln2}$. Khi $d=0$, $\Pi=1$.

**Hệ quả 03.16.**
- Bước tất định đúng cho mọi nghiệm ERM, kể cả trường hợp (O2). Phép lấy cận dưới đúng theo $h$ không cần $h_{\mathcal H}$.
- Với (c), từ $2\rho_m\le\epsilon$ suy ra $32(\cdot)/m\le\epsilon^2$. $\kappa=32/\epsilon^2$, nên $2\kappa=64/\epsilon^2$ và $4\kappa=128/\epsilon^2$. Giá trị này lớn hơn $d$.

**Định lý 03.17.**
- (a) không cần (M), vì $D$ có giá hữu hạn. Lập luận ở dòng 814 cho $d=\infty$ đúng.
- (b): chuỗi $1\Rightarrow2\Rightarrow3\Rightarrow4\Rightarrow6\Rightarrow1$ và $2\Rightarrow5\Rightarrow4$ khép kín.
- Từng chiều được gán đúng chỗ. (6)⇒(1) dùng 03.15(c) khi $d\ge1$ và 03.15(a) khi $d=0$. (1)⇒(2) dùng $M=m^{UC}(\epsilon/2,\delta)$. (2)⇒(5) và (3)⇒(4) dùng Nhận xét 01.26. (4)⇒(6) không chứng minh và được ghi rõ là không chứng minh.

**Hệ quả 03.18.** Đúng khi thừa nhận Định lý 03.17(a).

**Định lý 03.19.**
- Lượng từ "mọi $A$, tồn tại $D$" đúng thứ tự.
- Cận $\epsilon<\epsilon_0$, $\delta<\delta_0$ khớp UML: §28.2.1 cần $\epsilon^2\le1/2$, $m\le0{,}5\ln(1/(4\delta))/\epsilon^2$; §28.2.2 cho $m(\epsilon,1/8)\ge8d/\epsilon^2$ khi $\epsilon<1/(8\sqrt2)$. Với $\delta<1/8$, tính đơn điệu cho cận theo $d$, và dấu chặt được bù bằng hằng số.
- Phần khả thực cần $d\ge2$ là cẩn thận đúng mức: với lớp chỉ gồm hai hàm hằng trên một điểm, $d=1$ và $m=1$ đã đủ, nên số hạng $\ln(1/\delta)/\epsilon$ không đúng khi $d=1$.

**Ví dụ 03.6 và 03.8.** Độ lệch đều bằng $1$ trên mọi mẫu. Tập rỗng đo được và có xác suất $0$. $\mathcal G_S$ có chiều VC bằng $1$.

**Câu hỏi cuối buổi.** Cận dưới với bốn điểm hình thoi và cận trên với năm điểm đều đúng, trừ phần gán nhãn ghi ở bảng. Câu hỏi phụ đúng. $\mathcal H_{\mathrm{rec}}$ của Bài tập 02.7 chứa $h_\varnothing$, khớp lời giải.

**Không chuyển kết quả cho hàm lỗi bị chặn sang hàm lỗi khác.** Mọi bước đều dùng hàm lỗi 0–1. Dòng 867 loại rõ hàm lỗi bình phương và hàm lỗi log (Nhận xét 02.11). Mỗi bất đẳng thức đều nêu công cụ của nó: Chebyshev, Hoeffding, bất đẳng thức hợp, bất đẳng thức tam giác, Fubini, định lý hội tụ bị chặn, bất đẳng thức tiếp tuyến của hàm lõm, $1+x\le e^x$, Cauchy–Schwarz.

## Phụ lục: các con số đã kiểm

Mọi giá trị dưới đây được tính lại bằng Python (`calc.py`, `calc2.py`). "Đúng" nghĩa là khớp với bản nháp sau khi làm tròn đến số chữ số mà bản nháp ghi.

| # | Vị trí (dòng) | Giá trị trong bản nháp | Tính lại | Kết luận |
|---|---|---|---|---|
| 1–2 | Ôn nhanh 1 (42) | $16$, $2^5=32$ | $1+5+10=16$; $32$ | đúng |
| 3–5 | Ôn nhanh 2 (43) | $w=(2,2)$, $b=-1$; giá trị $-1,1,1$ | $-1$; $2-1=1$; $1$ | đúng |
| 6 | Ôn nhanh 3 (44–50) | $2e^{-m\epsilon^2/2}$ | $2\exp(-2m\epsilon^2/2^2)$ | đúng |
| 7–9 | Ví dụ 03.2 (150–160) | sáu véc-tơ; $6$; $32$ | liệt kê theo $t\le1$, $(k-1,k]$, $t>5$ | đúng |
| 10–11 | dòng 179 | $\log_26\approx2{,}585$; $d\le2$ | $2{,}58496$ | đúng |
| 12–14 | Ví dụ 03.3 Bước 1 (315) | $b=1$, $w=(-2,0)$; giá trị $1,-1,1$ | $w_1=0-1-1=-2$, $w_2=2-1-1=0$ | đúng |
| 15 | Ví dụ 03.3 Bước 3 (321–324) | $2+4+4+4=14$ | $16-2$; $\binom42=4+2$ | đúng |
| 16 | Ví dụ 03.3 Bước 4 (326) | $(1,1)=\frac13\sum$ đỉnh | $(3,3)/3$ | đúng |
| 17–18 | dòng 309 | $d=11$; $d=3$ | $p+1$ | đúng |
| 19–23 | Ví dụ 03.4 (368–382) | $m+1$; $\binom{m+1}2+1$; $6$; $16$; $32$ | đếm khối; $15+1$ | đúng |
| 24–45 | Bảng 1 (458–463), 22 ô số | $2,3,4,5,6,21$; $2,4,7,11,16,211$; $2,4,8,14$ | $m+1$; $\binom{m+1}2+1$; $m^2-m+2$ tại $m\le4$ | đúng |
| 46–58 | Bảng 2 (468–473), 13 ô số | tổng $2,4,8,15,26$; $20{,}09$; $47{,}61$; $92{,}99$; $2^m$ | $20{,}0855$; $47{,}6102$; $92{,}9886$ | đúng |
| 59–61 | dòng 475 | $1351$; $5951{,}27$; $1\,048\,576$ | $1+20+190+1140$; $5951{,}2702$ | đúng |
| 62 | dòng 475 | dạng đóng $>2^m$ khi $3\le m\le5$ | $20>8$, $47{,}6>16$, $93>32$ | đúng |
| 63 | dòng 433 | $(e/3)^3\approx0{,}744$ | $0{,}74391$ | đúng |
| 64–65 | Ví dụ 03.5 Bước 3 (452) | $\Pi(4)\le14$, đạt $14$; tổng $15$ | $1+4+6+4$ | đúng |
| 66 | dòng 580 | $\sqrt{16\ln2}\approx3{,}33$ | $3{,}3302$ | đúng |
| 67 | dòng 606, 1077 | $8\ln4\approx11{,}09$ | $11{,}0904$ | đúng |
| 68–70 | Định lý 03.15(b) (565–566) | hệ số $8$; hằng số $4$; $1+\ln2<2$ | $\sqrt{16}=4$; $1{,}6931$ | đúng |
| 71–72 | Định lý 03.15(c) (572) | $16/\epsilon^2$, $32/\epsilon^2$ | $2\kappa$, $4\kappa$ với $\kappa=8/\epsilon^2$ | đúng |
| 73–74 | Hệ quả 03.16(c) (698) | $64/\epsilon^2$, $128/\epsilon^2$ | $\kappa=32/\epsilon^2$ | đúng |
| 75 | dòng 728, 748 | hệ số $32$ | $4\cdot8$ | đúng |
| 76 | dòng 614 | $\ln80\approx4{,}3820$ | $4{,}38203$ | đúng |
| 77–81 | Ví dụ 03.7 Bước 2 (619–626) | $18\,122$; $9{,}8049$; $29{,}415$; $0{,}027037$; $0{,}1644$ | $18121{,}88$; $9{,}80488$; $29{,}4146$; $0{,}0270373$; $0{,}16443$ | đúng |
| 82–93 | Bảng Ví dụ 03.7 (632–633), 12 ô | $0{,}464/0{,}621$; $0{,}164/0{,}223$; $0{,}0571/0{,}0779$; $0{,}762/1{,}014$; $0{,}280/0{,}379$; $0{,}0993/0{,}136$ | $0{,}4638/0{,}6212$; $0{,}1644/0{,}2228$; $0{,}0571/0{,}0779$; $0{,}7622/1{,}0143$; $0{,}2799/0{,}3787$; $0{,}0993/0{,}1356$ | đúng |
| 94 | dòng 635 | $1{,}014>1$ | $1{,}0143$ | đúng |
| 95–96 | dòng 637 | giảm $2{,}7$–$2{,}9$ lần; $\sqrt{10}\approx3{,}16$ | tỉ số $2{,}678$–$2{,}881$; $3{,}1623$ | đúng |
| 97 | dòng 639 | $1{,}33$–$1{,}37$ lần | $1{,}3308$–$1{,}3657$ | đúng |
| 98–100 | Ví dụ 03.8 (655–659) | $8{,}601$; $4{,}382$; $0{,}322$ | $8{,}60090$; $4{,}38203$; $0{,}32228$ | đúng |
| 101–103 | Ví dụ 03.9 Bước 2 (755–757) | $54\,330$; $132\,992$; $447\,194$ | tìm nhị phân, với $4{,}382$ và với $\ln80$ chính xác cho cùng kết quả | đúng |
| 104–105 | Ví dụ 03.9 Bước 3 (761) | $0{,}0099999$ tại $54\,330$; $0{,}0100001$ tại $54\,329$ | $0{,}00999991$; $0{,}01000009$ | đúng |
| 106 | Ví dụ 03.9 Bước 1 (750) | vế trái giảm khi $m\ge d$ | đạo hàm $<0$ khi $d\ln(2em/d)+c>d$ | đúng |
| 107–109 | Ví dụ 03.9 Bước 4 (763) | $88\,572$; $209\,624$; $693\,832$ | $\lceil88571{,}05\rceil$; $\lceil209623{,}22\rceil$; $\lceil693831{,}88\rceil$ | đúng |
| 110 | dòng 763 | $1{,}55$–$1{,}63$ lần | $1{,}5515$–$1{,}6303$ | đúng |
| 111–113 | dòng 763 | $103\,939$; $261\,198$; $889\,572$ | điều kiện $64(d\ln(em/d)+\ln40)/m\le0{,}01$ | đúng |
| 114–115 | dòng 765, 863 | $3{,}36$; $11/3\approx3{,}67$ | $3{,}3626$; $3{,}6667$ | đúng |
| 116 | Ví dụ 03.10 (771) | $2K/\delta\le2^{64q+1}\cdot20$ | $40\cdot2^{64q}$ | đúng |
| 117–118 | dòng 773 | $48{,}050$; $9611$ | $48{,}0503$; $\lceil9610{,}06\rceil$ | đúng |
| 119–120 | dòng 775 | $491{,}664$; $98\,333$ | $491{,}6645$; $\lceil98332{,}90\rceil$ | đúng |
| 121–122 | dòng 777 | $0{,}2222$; $0{,}0523$ | $0{,}22224$; $0{,}05235$ | đúng |
| 123–124 | dòng 779, 865 | $4{,}5$–$5{,}7$ lần; $4{,}25$ lần | $4{,}548$ và $5{,}653$; $4{,}2454$ | đúng |
| 125 | Định lý 03.17(a) (798–800) | $1/8$, $1/7$ | $(1/4-1/8)/(7/8)=1/7$ | đúng (xem phát hiện về $>$ và $\ge$) |
| 126 | dòng 904 | $0{,}164\to0{,}280$ | ô $d=3$ và $d=11$ tại $m=10^4$ | đúng |

**Tổng số giá trị đã kiểm: 126.** Không giá trị nào sai.
