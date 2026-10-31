# Rà 2 — Chính xác toán học, Bài 06 (bản đóng băng `lec06-draft-frozen.md`)

Người rà: R2 (chỉ đọc). Script kiểm số: `reviews06/r2/check.py`, `reviews06/r2/svg.py`, `reviews06/r2/appE.py` (chạy bằng `/data/tqlong/lectures/.venv/bin/python`).

**Tổng kết:** 10 phát hiện — `chặn bàn giao`: 1; `nghiêm trọng`: 0; `trung bình`: 2; `nhẹ`: 7.
Mọi con số trong bài (ví dụ, câu ôn nhanh, câu hỏi mở đầu/cuối buổi, Hình 06.1, phụ lục) tính lại đều khớp; quy tắc làm tròn cận trên lên được tôn trọng. Phép đổi hằng số UML Cor. 13.7 (Nhận xét 06.12) đúng.

## 1. Kết quả đã chứng minh lại

| Kết quả | Kết luận | Ghi chú |
|---|---|---|
| Bổ đề 06.1 (a), (b) | ✓ | Khả tích của ba số hạng được kiểm; chỉ dùng chiều "kì vọng của dưới gradient là dưới gradient". Giả thiết $L_D<\infty$ trên cả $\mathbb R^p$ là cần cho (C) của Bài 05 (F hữu hạn trên $\mathbb R^p$). |
| Hệ quả 06.2 (a)–(c) | ✓ | Khớp Hệ quả 05.15(a)–(c) với $F=L_D$; kì vọng theo $Z_1,\ldots,Z_{T-1}$ đúng theo đoạn sau Thuật toán 05.11; (G1) cần $\mathbb E\lVert v\rVert<\infty$, suy từ (G2) bằng Cauchy–Schwarz. |
| Nhận xét 06.3 | ✓ | $T=m+1$, dùng đúng $Z_1..Z_m$; $5/\sqrt{10^6+1}=0{,}0049999975\to0{,}005$ (làm tròn lên). |
| Định nghĩa 06.4 và ba ví dụ sau | ✓ | $A_{\mathrm{gn}}$: $L_S=0$, $L_D=1$ (Mệnh đề 01.15(a)(b)); $\bar Y$: $1{,}25-0{,}75=0{,}5$. |
| Mệnh đề 06.5 (a), (b) | ✓ | Bước 3 dùng $u$ cố định và dạng yếu (T1) đúng chỗ; $\mathbb E\inf_WL_S\le\inf_WL_D$ đúng. |
| Bổ đề 06.7 | ✓ | Đúng với $u$ trên biên, không cần khả vi. |
| Bổ đề 06.8 (a)–(c), Phụ lục A | ✓ (câu cuối Phụ lục A: xem phát hiện #9) | Cận dưới afin, tập mức compact, tính duy nhất qua Bổ đề 06.7. |
| Định nghĩa 06.9, nhận xét sau (dạng $\mathbb E_\xi\lvert\cdot\rvert$ mạnh hơn; $A_{\mathrm{gn}}$ có hệ số 1; ERM $\lambda=0$ đổi tới $1{,}7988$) | ✓ | $1{,}7988=304/169$ là cực đại chính xác, đạt tại $z=(1,-1)$ và $(-1,1)$. |
| **Định lý 06.10** | **✗ (chứng minh)** | Kết luận đúng; Bước 2 chứa một đẳng thức sai (phát hiện #1). Bước 1, 3, 4 đúng. |
| Mệnh đề 06.11 (a), (b), Phụ lục B | ✓ | Lập luận đối xứng cho $2G/(\lambda m)$ đúng và chặt (Ví dụ 06.8 đạt); lập luận một phía cho $4G/(\lambda m)$ trùng UML (13.7)+(13.9) với $\lambda_{\mathrm{UML}}=\lambda/2$. |
| Nhận xét 06.12 | ✓ | UML Cor. 13.7: $\lambda_{\mathrm{UML}}\ge2\beta/m$, $48\beta C/(\lambda_{\mathrm{UML}}m)$ (tr. 178). Với $\lambda_{\mathrm{UML}}=\lambda/2$: $\lambda\ge4\beta/m$, $96\beta C/(\lambda m)$. Bình phương: Hessian $2xx^\top$ nên $\beta=2C_x^2$, $C=C_y^2$: $\lambda\ge8C_x^2/m$, $192C_x^2C_y^2/(\lambda m)$. Cận một phía, theo kì vọng — nêu đúng. |
| Hệ quả 06.13 (a)–(c), Phụ lục C | ✓ | Khả tích: $\mathbb E\lVert\hat w_S\rVert^2\le\lVert u\rVert^2+2L_D(u)/\lambda$ đúng (cần $\ell\ge0$ trên $W$, có trong giả thiết); $\lambda^*=\sqrt{a/b}=2G/(B\sqrt m)$, $2\sqrt{ab}=2GB/\sqrt m$. |
| Nhận xét 06.14 | ✓ phần Markov; ✗ phần "tăng độ tin cậy" thiếu giả thiết (phát hiện #3) | |
| Nhận xét 06.15 | ✓ | $\lVert\tilde w-\hat w_S\rVert\le\sqrt{2\epsilon_{\mathrm{opt}}/\lambda}$ từ Bổ đề 06.8(c). |
| Phụ lục D | ✓ | $c_s=(1-q^{T-s})/T$, $\sum c_s=1-(1-q^T)/(2\eta T)$ kiểm cả đại số lẫn số; giới hạn $1+1/m$ đúng. |
| Phụ lục E (đẳng thức, ổn định đều ⇒ trung bình) | ✓ | |
| Phụ lục E (iii) phản ví dụ chiều ngược | **✗** | Chỉ xét $D$ không nguyên tử, trong khi định nghĩa đòi mọi $D$ (phát hiện #2). |

Các nhận xét có công thức khác: QR1–QR3, Ví dụ 06.1–06.12, §10, câu hỏi cuối buổi — ✓ (bảng số dưới).

## 2. Bảng số đã tính lại

| Vị trí | Giá trị trong ghi chú | Giá trị tính được | Khớp? |
|---|---|---|---|
| Mở đầu / Bài 05: $\operatorname{opt}_S$, sai số ước lượng | 0,0025; 0,9025 | $0{,}05^2=0{,}0025$; $0{,}95^2=0{,}9025$ | ✓ |
| Câu hỏi mở đầu: $RG/\sqrt T$; số vòng | 0,1; ~400 | $4/40=0{,}1$; $1599/4=399{,}75$ | ✓ |
| QR1 | 0,75; 0,75 | 0,75; 0,75 | ✓ |
| QR2 | 1; 0,75; 1,25; chênh 0,5 | liệt kê 16 mẫu: 1; 0,75; 1,25; 0,5 | ✓ |
| QR3 | $\lambda=0{,}2$, min 0,2 | 0,2; 0,2 | ✓ |
| VD 06.1: ba tổng; ERM; $L_S$ | 3,25; 2,5; 3; 0,7692; 0,2692 | 3,25; 2,5; 3; 0,769231; 0,269231 | ✓ |
| VD 06.2: $\eta$; $\sum c_t$; $\sum c_t^2$; tỉ số | 0,00625; 0,95; 0,000578; 173 | 0,00625; 0,9500000001; 0,00057822; 172,94 | ✓ |
| VD 06.3: $\Pr(\bar Y=0)$ | 0,375 | 6/16 (MC 0,376) | ✓ |
| VD 06.3: $\mathbb E\bar w^2$; $\mathbb E[\bar w\bar Y]$ | 0,2261; 0,2375 | 0,226059; 0,237500 (MC 0,2255) | ✓ |
| VD 06.3: $\mathbb EL_S$; $\mathbb E\inf L_S$; $\mathbb E\operatorname{opt}$ | 0,7511; 0,75; 0,0011 | 0,751059; 0,75; 0,001059 | ✓ |
| VD 06.3: khoảng cách; số hạng giữa; cận (b) | 0,4750; −0,2489; 0,4761 | 0,475000; −0,248941; 0,476059 | ✓ |
| §6: nghiệm sau thay; dịch; tỉ lệ đường kính | 0,1538; 0,6154; ~1/3 | 2/13; 8/13; 0,308 | ✓ |
| VD 06.4 $\lambda=0$ | 0,7692; 0,1538; 0,6154; 0,2692 | 10/13; 2/13; 8/13; 0,269231 | ✓ |
| VD 06.4 $\lambda=1$ | 10/21; 2/21; 8/21≈0,3810; 0,3390 | 0,476190; 0,095238; 0,380952; 0,339002 | ✓ |
| VD 06.4 $\lambda=4$ | 2/9; 2/45; 0,1778; 0,5123 | 0,222222; 0,044444; 0,177778; 0,512346 | ✓ |
| Hình 06.1 (đọc SVG) | cực tiểu 0,769/0,154/0,222/0,044; 0,615; 0,178 | điểm đánh dấu 0,7689; 0,1540; 0,2222; 0,0442; tung độ 0,2693; 0,7307; 0,6107; 0,7440 (đúng $F$: 0,2692; 0,7308; 0,6111; 0,7444); sai số đường cong ≤ 0,002 | ✓ |
| §7: thay đổi lớn nhất của hàm lỗi, $\lambda=0$ | 1,7988 | 304/169 = 1,798817 | ✓ |
| VD 06.5 $\mathbb E\lvert L_S-\tfrac12\rvert$ | 0,1230; 0,0398; 0,0126 | 0,123047; 0,039795; 0,012613 ($1/\sqrt{2\pi m}$: 0,1262; 0,0399; 0,0126) | ✓ |
| VD 06.6 cận | 2; 8; 0,5; 2 | $2/\lambda$, $8/\lambda$ | ✓ |
| VD 06.6 Bước 2 | 240/441≈0,5442; 432/441≈0,9796; 0,3810; 0,1451; 0,7619 | 80/147=0,544218; 48/49=0,979592; 0,380952; 0,145125; 0,761905 | ✓ |
| VD 06.6 lỏng | ~5 lần | 5,25 | ✓ |
| VD 06.7 | 1,3333; 0,3333; 0,0392 / 8; 0,8; 0,08; ~2 lần | 1,333333; 0,333333; 0,039216 / 8; 0,8; 0,08; 2,04 | ✓ |
| VD 06.8 | 0,2; 0,1 so với 0,2 | $2/(0{,}1\cdot100)=0{,}2$; $G^2/(\lambda m)=0{,}1$ (MC 0,0998) | ✓ |
| VD 06.9 | 0,6667; 0,6600; 0,3976; 0,0098; 0,0045; 0,2518; 0,8695 | 0,666667; 0,66; 0,397590; 0,009755; 0,004489; 0,251786; 0,869475 | ✓ |
| VD 06.10 | 0,2; 0,2; 6400; 0,1; 1600; 40 000; $10^4$ | như ghi chú | ✓ |
| VD 06.11 | $4\cdot10^{-4}$; 0,01; 0,002; 0,005 | 0,0004; 0,01; 0,002; 0,0049999975 | ✓ |
| VD 06.12 | 0,0083; 0,25; 0,8264 | 0,008264; 0,25; 0,826446 | ✓ |
| Nhận xét 06.14 | 2 560 000; 400 | 2 560 000; 400 | ✓ |
| Nhận xét 06.15 | 0,1265 | 0,126491 (làm tròn lên) | ✓ |
| Câu hỏi cuối buổi | $G=4$; 0,2; 0,4; 0,4; 0,5 | 4; 0,2; 0,4; 0,4; 0,5 | ✓ |
| Phụ lục D, $T=1600$ | $q=0{,}9875$; $q^T$ không đáng kể; 0,95; 0,000578 | 0,9875; $1{,}82\cdot10^{-9}$; 0,95; 0,00057822 | ✓ |
| Phụ lục D, $T=25\,600$ | 0,9875; $3{,}83\cdot10^{-5}$; 1,2438; 1,9752; 0,4938 | 0,9875; $3{,}833\cdot10^{-5}$; 1,243818; 1,975156; 0,49375 | ✓ |
| Phụ lục E, hằng số | $2\rho^2/(\lambda_{\mathrm{UML}}m)=4\rho^2/(\lambda m)$ | đúng (UML Cor. 13.6) | ✓ |
| §13: cỡ mẫu UML | $8\rho^2B^2/\epsilon^2$ | UML Cor. 13.9 (tr. 179) | ✓ |

## 3. Phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| chặn bàn giao | §7, chứng minh Định lý 06.10, Bước 2, câu thứ hai và ba sau công thức (dòng 671) | Áp dụng Bước 1 cho cặp $(S^{(i)},Z')$ trong khi $Z'$ là thành phần thứ $i$ của $S^{(i)}$, không độc lập với mẫu. Kết quả là đẳng thức sai $\mathbb E\,\ell(A(S;\xi),Z_i)=\mathbb EL_D(A(S;\xi))$; cộng với Bước 3 nó cho $\mathbb EL_S=\mathbb EL_D$, tức khoảng cách tổng quát hóa kì vọng bằng $0$ với mọi thuật toán, mâu thuẫn Ví dụ 06.3 ($0{,}4750$) và $A_{\mathrm{gn}}$ ($1$). Câu "Giả thiết khả tích kéo theo $\mathbb EL_S<\infty$ (Bước 2 của chứng minh)" trong khối định lý dựa vào bước sai này. | Nguyên văn: "Cùng phép đổi chỗ cho $\mathbb E\,\ell(A(S;\xi),Z_i)=\mathbb E\,\ell(A(S^{(i)};\xi),Z')$. Vế phải bằng $\mathbb EL_D(A(S^{(i)};\xi))$ theo Bước 1 áp dụng cho $S^{(i)}$, và bằng $\mathbb EL_D(A(S;\xi))<\infty$ …". Bước 1 cần quan sát kiểm tra độc lập với mẫu; $\ell(A(S^{(i)};\xi),Z')$ là hàm lỗi trên một quan sát huấn luyện. Không có tính ổn định, $\mathbb EL_D<\infty$ không kéo theo $\mathbb EL_S<\infty$ (chẳng hạn một thuật toán chỉ sai trên các điểm của mẫu dưới $D$ không nguyên tử). | Thay hai câu đó bằng: "Với $(s,z')$ cố định, Định nghĩa 06.9 với $z=z_i$ cho $\mathbb E_\xi\ell(A(s;\xi),z_i)\le\mathbb E_\xi\ell(A(s^{(i)};\xi),z_i)+\epsilon_{\mathrm{stab}}(m)$. Lấy kì vọng theo $(S,Z')$ (Fubini, hàm không âm) và dùng đẳng thức vừa chứng minh: $\mathbb E\,\ell(A(S;\xi),Z_i)\le\mathbb EL_D(A(S;\xi))+\epsilon_{\mathrm{stab}}(m)<\infty$." Sửa câu trong khối định lý thành "Giả thiết khả tích cùng tính ổn định đều kéo theo $\mathbb EL_S(A(S;\xi))<\infty$ (Bước 2)". Bỏ câu "Cùng phép đổi chỗ cho …" (không cần cho chứng minh). |
| trung bình | Phụ lục E, đoạn "So với ổn định đều", câu 3–5 (dòng 1281) | Phản ví dụ chỉ chứng minh vế trái bằng $0$ dưới $D$ không nguyên tử, trong khi định nghĩa ổn định thay một theo trung bình (đoạn đầu Phụ lục E, cũng như UML Def. 13.3) đòi điều kiện "với mọi phân bố $D$". Dưới $D$ có nguyên tử, vế trái dương, nên lập luận chưa chứng minh "điều ngược lại sai". | Lấy $D$: nguyên tử $a$ với khối lượng $p$, phần còn lại liên tục; $\ell(w_0,z)=\mathbb 1[z=a]$, $\ell(w_1,\cdot)=0$. Tính đúng: vế trái $=(m-1)p^2(1-p)^{m-1}$; $m=2$, $p=\tfrac12$: $0{,}125$ (mô phỏng $0{,}1247$, `r2/appE.py`). Cực đại theo $p$ cỡ $0{,}54/m$, nên tốc độ trung bình là $O(1/m)$, không phải $0$. | Hai cách: (i) đổi phản ví dụ thành thuật toán "đặt hàm lỗi bằng $1$ tại các quan sát của mẫu": với $\ell(h_s,z)=\mathbb 1[z\in s]$, $L_S=1\ge D(\{z_1..z_m\})=L_D$ với mọi $D$, nên điều kiện một phía đúng với $\epsilon(m)=0$ cho mọi $D$, còn hệ số ổn định đều bằng $1$; (ii) giữ ví dụ hiện tại nhưng nói rõ "với một $D$ không nguyên tử cố định" và thêm cận $O(1/m)$ có chứng minh cho mọi $D$. Cách (i) ngắn và đủ chặt. |
| trung bình | §9, Nhận xét 06.14, ý "Tăng độ tin cậy" (dòng 1032); liên quan §2 dòng 122 | Thủ tục chia khối và chọn bằng mẫu xác thực dựa vào Hệ quả 04.17, mà Hệ quả 04.17 giả thiết (T3) (hàm lỗi bị chặn); UML Bài tập 13.1 ý 2 cũng giả sử hàm lỗi bị chặn bởi 1. Ghi chú không nêu giả thiết này, trong khi §2 khẳng định "Không kết quả nào của bài giả sử hàm lỗi bị chặn" và bài nhắm tới hàm lỗi bình phương và logistic. Đây là chuyển một kết quả cho hàm lỗi bị chặn sang khung chung mà không có lập luận (blueprint §E). | Hệ quả 04.17, mục **Hàm lỗi**: "$\ell$ thỏa (T2) và (T3)". UML tr. 181: "assuming that the loss function is bounded by 1". | Thêm vào ý đó: "khi hàm lỗi nhận giá trị trong $[0,1]$ (giả thiết (T3) của Hệ quả 04.17)". Có thể thêm một câu: với hàm lỗi bình phương trên dữ liệu và $W$ bị chặn, hàm lỗi bị chặn bởi $(BC_x+C_y)^2$ nên thủ tục áp dụng được sau khi chia tỉ lệ; với hàm lỗi logistic trên $W=\mathbb R^p$ thì không. |
| nhẹ | §8, Ví dụ 06.9, Kết luận (dòng 872); §13, mục Mở rộng (dòng 1123) | Ví dụ "dữ liệu không bị chặn thì không học được" của UML là Ví dụ 12.9 (và 12.8) trong §12.2.1, không phải §12.2.2 (§12.2.2 chỉ định nghĩa bài toán lồi–Lipschitz/trơn–bị chặn). UML chỉ chứng minh cho thuật toán tất định (chú thích 1, tr. 165). | UML tr. 164: "12.2.1 Learnability of Convex Learning Problems … Example 12.8"; tr. 165–166: Example 12.9; tr. 166: "12.2.2 Convex-Lipschitz/Smooth-Bounded Learning Problems". | Đổi thành "UML §12.2.1 (Ví dụ 12.9)"; ở §13 tách: "§12.2.1 (ví dụ dữ liệu không bị chặn), §12.2.2 (bài toán lồi–Lipschitz–bị chặn)". Có thể thêm "(UML chứng minh cho thuật toán tất định)". |
| nhẹ | §13, "Quan hệ với giáo trình UML", ý "SGD với quan sát mới" (dòng 1130) | Mô tả UML chưa đầy đủ: UML §14.5.1 xét cả hàm lỗi không khả vi bằng đúng lập luận dưới gradient của Bổ đề 06.1. | UML tr. 197: "The same argument holds for nondifferentiable loss functions. We simply let $v_t$ be a subgradient … It follows that $\mathbb E[v_t\mid w^{(t)}]$ is a subgradient of $L_D$". | Viết: "UML §14.5.1 đổi chỗ gradient và kì vọng cho hàm khả vi và dùng bất đẳng thức dưới gradient cho trường hợp còn lại; học phần nêu lập luận thứ hai thành Bổ đề 06.1 với giả thiết khả tích, và đếm $T-1$ quan sát." |
| nhẹ | §8, câu sau giả thiết (L) (dòng 729) | Câu ngầm nói Hệ quả 06.2 cần Lipschitz trên một tập mở chứa $W$. Hệ quả 06.2 chỉ giả thiết $\mathbb E\lVert v(w,Z)\rVert^2\le G^2$ trên $W$; Lipschitz trên tập mở chỉ là một điều kiện đủ. | Hệ quả 06.2, **Cận gradient**: "$\mathbb E_{Z\sim D}\lVert v(w,Z)\rVert^2\le G^2$ với mọi $w\in W$; điều kiện này thỏa khi …". | "Giả thiết (L) chỉ cần trên $W$; khác Hệ quả 06.2, nó là điều kiện trên giá trị hàm lỗi, không trên dưới gradient, nên không cần một tập mở chứa $W$ để suy ra nó." |
| nhẹ | §6, Ví dụ 06.4, Bước 2, câu cuối (dòng 574) | Công thức một chiều $\hat w=\sum x_iy_i/(\sum x_i^2+\lambda m/2)$ là điểm cực tiểu không ràng buộc; nó là nghiệm trên $W$ chỉ khi thuộc $W$ (hoặc $W=\mathbb R$). Các lần dùng sau (Ví dụ 06.7, 06.9) đều thỏa, nhưng câu không nêu điều kiện. | Ví dụ: $\lambda=0$, mẫu $((0{,}5;1))$, $W=[-1,1]$: công thức cho $2\notin W$. | Thêm "khi giá trị này thuộc $W$ (luôn đúng với $W=\mathbb R$)". |
| nhẹ | §7, đoạn "Ngược lại, ERM trên $W$ …" (dòng 630) | "(dò trên lưới)" làm số trông như xấp xỉ; giá trị $1{,}7988$ là cực đại chính xác. | $\max_{z\in[-1,1]^2}\lvert(ax-y)^2-(bx-y)^2\rvert=(a-b)(a+b+2)=\tfrac8{13}\cdot\tfrac{38}{13}=\tfrac{304}{169}$, đạt tại $z=(1,-1)$. | Thay "(dò trên lưới)" bằng "(tại $z=(1,-1)$; giá trị đúng $304/169$)". |
| nhẹ | Phụ lục A, câu cuối sau $\square$ (dòng 1163) | Lớp $h_w(x)=\langle w,x\rangle$ không có hệ số tự do, nên phản ví dụ cần mẫu tách được bởi một siêu phẳng qua gốc. Với mẫu chỉ tách được khi có hệ số tự do, giá trị nhỏ nhất có thể đạt. | $p=1$, mẫu $(x,\tilde y)=(1,+1),(2,-1)$: tách được bằng ngưỡng $1{,}5$ nhưng $L_s(w)=\tfrac12[\ln(1+e^{-w})+\ln(1+e^{2w})]$ đạt cực tiểu hữu hạn. Với điều kiện "có $w$ thỏa $\tilde y_i\langle w,x_i\rangle>0$ mọi $i$": $L_s(tw)\downarrow0$ khi $t\to\infty$ mà $L_s>0$, đúng như ghi chú. | Viết "trên một mẫu có $w$ với $\tilde y_i\langle w,x_i\rangle>0$ cho mọi $i$ (tách được bởi một siêu phẳng qua gốc)". |
| nhẹ | §12, đoạn cầu nối (dòng 1117); Phụ lục E, cuối đoạn "Đẳng thức" (dòng 1279) | (a) "$L_S\approx0$ và khoảng cách tổng quát hóa bằng chính $L_D$": chỉ xấp xỉ. (b) UML không đặt tên định lý là "thuật toán ổn định không quá khớp"; đó là tên mục §13.2, Định lý 13.2 không có tên. | (a) $L_D-L_S=L_D-(\approx0)$. (b) UML tr. 173–174: tiêu đề "13.2 Stable Rules Do Not Overfit", "theorem 13.2" không tên. | (a) "khoảng cách tổng quát hóa xấp xỉ $L_D$". (b) "UML trình bày kết quả này ở mục §13.2 ‘Stable Rules Do Not Overfit’ (Định lý 13.2)". |

## 4. Kiểm chuẩn lý thuyết học thống kê (blueprint §E)

- Loại bảo đảm được nêu đúng ở mọi khối: Hệ quả 06.2 và 06.13 — rủi ro vượt mức kì vọng (tổng thể) so với $u$ cố định hay $\inf$ trên $W$/$W_B$; Mệnh đề 06.5 — tách rủi ro vượt mức kì vọng thành khoảng cách tổng quát hóa kì vọng + sai số tối ưu thực nghiệm kì vọng; Định lý 06.10 — trị tuyệt đối của khoảng cách tổng quát hóa kì vọng, phân biệt rõ với $\mathbb E\lvert\cdot\rvert$ (Ví dụ 06.5); Mệnh đề 06.11 — tất định; Nhận xét 06.12 — một phía, theo kì vọng; Nhận xét 06.14 — xác suất cao qua Markov.
- Phân biệt cấp thuật toán / cấp lớp được giữ (Hệ quả 06.2, Định lý 06.10, Nhận xét 06.14).
- $u$ cố định so với phụ thuộc mẫu: Mệnh đề 06.5 Bước 3 và Hệ quả 06.13 Bước 2 nêu đúng; $\inf$/$\min$ dùng đúng (min chỉ ở chỗ đạt: $W=[-1,1]$, quả cầu compact với $L_D$ liên tục).
- Không chuyển kết quả hàm lỗi bị chặn sang bình phương/log, trừ ý "Tăng độ tin cậy" của Nhận xét 06.14 (phát hiện #3). Hàm lỗi log chỉ được dùng cho mô hình logistic tuyến tính, có câu giới hạn (Ví dụ 06.11).
- Chỉ số $T-1$ quan sát theo Thuật toán 05.11 nhất quán ở Hệ quả 06.2, Nhận xét 06.3, Ví dụ 06.2, 06.10, Phụ lục D.
