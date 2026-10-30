# Rà lại toán học sau biên tập vòng 1, Bài 03

**Tệp được rà:** `2627-1/materials/lec-03/lecture-note.md`, bản hiện tại, 1138 dòng; số dòng dưới đây theo tệp này.
**Đối chiếu:** `lec03-round1.diff`, `planning/lec-03/reviews/0-quyet-dinh.md`, `planning/lec-03/bien-tap-vong-1.md`.
**Vai trò:** người rà soát toán học, chỉ đọc. Không sửa tệp nào trong repo, không commit.

## Kết luận

**Giao được sau khi xóa đoạn lặp ở dòng 576.** Cả 13 phát hiện của tôi ở lượt rà 2 đã được giải quyết.

Mọi phát biểu, bước chứng minh và con số mới hoặc đã đổi đều đúng. Đã kiểm:
- Hệ quả 03.16, Bước 4 mới.
- Giả thiết và danh sách phép kéo theo của Định lý 03.17.
- Định lý 03.19, có thêm (T1).
- Thứ tự mới của §7.
- Các bước mới của Ví dụ 03.3, 03.4, 03.5, 03.9 và 03.10.
- Đẳng thức cầu nối và lời giải câu hỏi cuối buổi.
- Các kí hiệu đổi tên ở Phụ lục A và C.

Lượt biên tập sinh ra một lỗi mới: dòng 576 lặp nguyên văn dòng 574 (kiểm bằng md5). Tôi xếp lỗi này ở mức `trung bình` vì học viên sẽ thấy nó. Ngoài ra có ba điểm `nhẹ` về cách diễn đạt.

`forward_refs.py` báo 0. Không còn chỗ nào dẫn số hiệu cũ "Định nghĩa 03.14" hay "Nhận xét 03.13".

**Số phát hiện mới:** chặn bàn giao 0, nghiêm trọng 0, trung bình 1, nhẹ 3.

## Trạng thái 13 phát hiện của lượt rà 2

| # | Phát hiện cũ (dòng trong bản đóng băng) | Trạng thái | Bằng chứng trong bản hiện tại |
|---|---|---|---|
| 1 | UML §28.3 bị gọi là cận dưới (910) | ✓ đã giải quyết | Dòng 925: "§28.2: cận dưới cho trường hợp bất khả tri; §28.3: cận trên cho trường hợp khả thực". Dòng 862: "UML §28.2 chứng minh phần (a); UML không chứng minh phần (b)". Cả hai khớp UML tr. 392 và 401. |
| 2 | Lời giải câu hỏi cuối buổi thiếu nhãn cho các điểm còn lại (897) | ✓ | Dòng 904: "nhãn $0$ cho mọi điểm còn lại, trong đó có $x$". |
| 3 | Chưa nói từng $h$ đo được (60) | ✓ | Dòng 60: "các hàm phân lớp (classifier) đo được". |
| 4 | Khẳng định "lớp bệnh lý" không có nguồn (490) | ✓ | Dòng 518: "các xác suất dưới đây có thể không xác định". Câu này đúng và không cần nguồn ngoài. |
| 5 | Viết "(M) cần" (869) | ✓ | Dòng 823 và 874: "(M) chỉ được dùng cho điều kiện đủ". |
| 6 | Câu tóm tắt bỏ (M) (784, 861) | ✓ | Dòng 782: "dưới (M), chiều VC hữu hạn kéo theo học được". Dòng 866: "Dưới (M), một lớp vô hạn học được …". |
| 7 | Hệ quả 03.16(c) chưa ghi điều kiện có một thuật toán ERM đo được (702) | ✓ | Dòng 698: "khi có ít nhất một thuật toán ERM như vậy". |
| 8 | Định lý 03.17(a): $>1/8$ khác $\ge1/8$ của UML | ✓ | Dòng 935 ghi rõ khác biệt và cách suy ra. |
| 9 | Ngưỡng "giữa hai điểm liên tiếp" bỏ sót hai trường hợp đầu mút (368) | ✓ | Dòng 364: "$t\le x_1$, $t>x_m$ hoặc $t\in(x_{i-1},x_i]$". Tôi kiểm lại: khoảng $(x_{i-1},x_i]$ với $i=2,\ldots,m$ cho từ $1$ đến $m-1$ nhãn $1$. |
| 10 | Tốc độ $\sqrt{\ln m/m}$ chỉ đúng khi $d\ge1$ (577) | ✓ | Dòng 571: "khi $d\ge1$ giảm theo $m$ như …". |
| 11 | Dãy $t_k\downarrow t$ chưa nói $t_k>t$ (493) | ✓ | Dòng 521: "Dãy $t_k\downarrow t$ với $t_k>t$". |
| 12 | Tính đo được của cận trên đúng có dấu ngẫu nhiên $\sigma$ (C.1) | ✓ | Dòng 1041: "Cùng lý do cho $\sup_h\lvert\frac1m\sum_i\sigma_ia_i(h)\rvert=\sup_k\ldots$ với mọi $\sigma$". |
| 13 | Nhận xét 02.8 được liệt kê nhưng không dùng (31) | ✓ | Dòng 31 không còn Nhận xét 02.8. |

## Kiểm chứng các phần đã đổi

**Hệ quả 03.16, Bước 4 (dòng 722).** Dạng đóng của Định lý 03.15(c) tại $\epsilon/2$ là $\lceil\frac{16}{(\epsilon/2)^2}(d\ln\frac{32}{(\epsilon/2)^2}+\ln\frac4\delta)\rceil=\lceil\frac{64}{\epsilon^2}(d\ln\frac{128}{\epsilon^2}+\ln\frac4\delta)\rceil=M(\epsilon,\delta)$. Tôi kiểm thêm bằng số tại $\epsilon\in\{0{,}1;0{,}3;0{,}9\}$ và $d\in\{1,3,11\}$.

Với $\epsilon\in(0,1)$ thì $\epsilon/2\in(0,1/2)$, nằm trong miền của Định nghĩa 03.13. Với $m\ge M\ge m^{UC}(\epsilon/2,\delta)$, biến cố "$S$ là $\epsilon/2$-đại diện" đo được và có xác suất ít nhất $1-\delta$. Bước 1–2 với $r=\epsilon/2$ cho $L_D(\hat h)\le\inf L_D+\epsilon$. Định lý 03.15(c) cần $1\le d<\infty$, và Hệ quả 03.16 đã giả sử điều này. Lập luận đúng.

Câu mở đầu "$2\rho_m\le\epsilon$ khi và chỉ khi $\rho_m\le\epsilon/2$" không còn được dùng trong lập luận, nhưng vẫn đúng.

**Định lý 03.17 (dòng 784–823).**
- Giả thiết có thêm **Mẫu** theo (T1). Phần (a) không dùng (M): $D$ có giá hữu hạn, nên $L_D(A(S))$ đo được với mọi thuật toán.
- Danh sách phép kéo theo: $6\Rightarrow1$ dùng 03.15(c) khi $d\ge1$ và 03.15(a) khi $d=0$; $1\Rightarrow2$ dùng biến cố đo được theo Định nghĩa 03.13; $2\Rightarrow3$, $5\Rightarrow4$, $2\Rightarrow5$, $3\Rightarrow4$, $4\Rightarrow6$ như trước. Chuỗi vẫn khép kín.
- Câu "(M) chỉ được dùng … ở phép kéo theo (6)⇒(1)" đúng, vì $1\Rightarrow2$ dùng tính đo được có sẵn trong định nghĩa.
- Dòng 821 dẫn Bài tập 03.11 (UML 6.10). Bài tập này phải thật sự chứng minh $d=\infty\Rightarrow$ không học được PAC; UML 6.10 làm được điều đó qua cận kì vọng. Người viết bài tập cần lưu ý.

**Định lý 03.19 (dòng 845–862).** Thêm (T1) là đúng. Phần ghi nguồn khớp UML: §6.4, Định lý 6.8 phát biểu cả hai cận dưới với hằng số tuyệt đối; §28.2 chứng minh phần bất khả tri; phần khả thực là bài tập (tr. 392). Câu ở dòng 870, "cỡ mẫu ít nhất cỡ $(d+\ln(1/\delta))/\epsilon^2$ là cần trong trường hợp xấu nhất", đúng với phần (a).

**Thứ tự §7 (dòng 474–537).** Định nghĩa 03.13 nêu tính đo được của $E_m$ như một yêu cầu, không như một khẳng định. Câu khẳng định "$E_m(D,\epsilon)$ đo được với mọi $D$" giờ nằm ở dòng 518, sau (M). Khẳng định về lớp hữu hạn ở dòng 498 không cần (M): biến cố là giao của hữu hạn biến cố đo được. Ví dụ 03.6 chỉ dùng tập rỗng. Các chỗ dùng Nhận xét 03.14 (Ví dụ 03.7, dòng 608; Phụ lục D) đều đứng sau nó. Không còn chỗ dùng tính đo được trước khi nó được nêu.

**Ví dụ 03.3, Bước 1 (dòng 316).** Cách gán nhãn $(0,1,1)$ cho $b=-1$ và $w_i=2-1+1=2$, tức $w=(2,2)$, khớp câu ôn nhanh 2. Mười bốn cách ở Bước 3 gồm $2+4+4+4$, đúng.

**Nhận xét 03.10(iii) (dòng 334).** $\mathcal H^1_{\mathrm{hom}}=\{\mathbb 1[wx\ge0]\}$ gồm đúng ba hàm $\mathbb 1[x\ge0]$, $\mathbb 1[x\le0]$ và hằng $1$. Mệnh đề 03.9(b) với $p=1$ cho $d=1$. Đúng.

**Ví dụ 03.4, Bước 4–6 và Ví dụ 03.5, Bước 3–7.** Các bước tách ra không đổi nội dung toán. Hai bảng không đổi. $\binom62+1=16=\sum_{j\le2}\binom5j$, đúng.

**Ví dụ 03.9, Bước 1 (dòng 730–734).**
- Việc dẫn Hệ quả 03.16(a) với dạng trực tiếp là đúng.
- Đạo hàm của $(d\ln\frac{2em}d+c)/m$ bằng $(d-d\ln\frac{2em}d-c)/m^2$, đúng. Dấu $<0$ đúng vì $\ln(2em/d)\ge\ln(2e)>1$ khi $m\ge d$, nhưng câu này bị bỏ trong bản mới (phát hiện nhẹ 2).
- Các số $54\,330$, $132\,992$, $447\,194$, $88\,572$, $209\,624$, $693\,832$, $103\,939$, $261\,198$, $889\,572$, $1{,}55$–$1{,}63$ và $3{,}36$ không đổi so với lần kiểm trước.

**Ví dụ 03.10, Bước 3–4 (dòng 763–779).**
- Lớp sáu hàm hữu hạn và có $\Pi\le6$, nên cả hai bán kính áp dụng; Định lý 03.15 cần (M), và lớp hữu hạn thỏa (M).
- $4\cdot6/0{,}05=480$; $\ln480=6{,}17379\approx6{,}174$; $\sqrt{8\cdot6{,}174/1000}=0{,}22224\approx0{,}2222$.
- $2K/\delta=240$; $\ln240=5{,}48064\approx5{,}481$; $\sqrt{5{,}481/2000}=0{,}05235\approx0{,}0523$.
- Tỉ số $4{,}25$; $4{,}5$–$5{,}7$; $9611$; $98\,333$. Tất cả đúng.

**Đẳng thức cầu nối (dòng 911–919).** $L_D(\hat h)-L^{\mathrm{Bayes}}_D=[\inf_{\mathcal H}L_D-L^{\mathrm{Bayes}}_D]+[L_D(\hat h)-\inf_{\mathcal H}L_D]$ là đẳng thức sau Định nghĩa 01.24 với hai số hạng đổi chỗ. Đúng. Khẳng định "số hạng thứ nhất không tăng khi lớp lớn hơn" đúng, vì cận dưới đúng lấy trên một tập lớn hơn. Xem phát hiện nhẹ 1 về các con số.

**Lời giải câu hỏi cuối buổi (dòng 902–908).** Các điểm được chọn đạt $a_1,a_2,b_1,b_2$, nên mọi hình chữ nhật chứa chúng thỏa $u_1\le a_1$, $a_2\le v_1$, $u_2\le b_1$, $b_2\le v_2$, và do đó chứa $x$. $h_\varnothing$ bị loại vì các điểm được chọn có nhãn $1$. Câu hỏi phụ đúng. Các chữ $a_i$, $b_i$, $u_i$, $v_i$ chỉ dùng trong lời giải này, nên không trùng nghĩa trong cùng một lập luận.

**Đổi tên kí hiệu.**
- Phụ lục A: $\alpha$ thay cho $A$ (dòng 957–959). Không trùng với chữ nào khác trong bài.
- Phụ lục C: $B_\epsilon$ thay cho biến cố $A$ (dòng 1041–1090). Chữ $B$ (tập vị trí) ở Phụ lục B và ở phác thảo Sauer–Shelah thuộc chứng minh khác, nên không trùng trong cùng một lập luận.
- Tiếp tuyến dùng $u$, $u_0$ (dòng 602, 1100), không còn trùng với $a_i(h)$. $\kappa$ chỉ còn ở C.7.
- Không còn chỗ nào dẫn số hiệu hay kí hiệu đã bỏ.

**Các câu đổi khác, đều đúng.**
- Dòng 5: Bài tập 01.9 (lớp hình tròn đồng tâm) và 02.7 (hình chữ nhật) là hai lớp vô hạn có cận khả thực riêng.
- Dòng 162, 170, 183, 229, 257, 284 (đơn hình là bao lồi của $p+1$ điểm độc lập afin; $0,\mathbf e_1,\ldots,\mathbf e_p$ độc lập afin).
- Dòng 406 (phác thảo Sauer–Shelah, phần điểm lặp chuyển xuống Phụ lục B theo dòng 399).
- Dòng 590, 592, 665, 703, 751, 813, 866, 868, 872.
- Dòng 929 (UML dùng $\mathbb 1[x<a]$ và khoảng mở) và dòng 931 (UML Bổ đề 6.10 cần $m>d+1$ cho dạng đóng).
- Phụ lục B, $P(n,d)$ viết dạng "Nếu … thì …".

## Bảng phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | Sau Định lý 03.15, dòng 574 và 576 | Cùng một đoạn xuất hiện hai lần liên tiếp (md5 trùng nhau), lỗi do lượt biên tập. Nội dung toán đúng, nhưng học viên sẽ thấy đoạn lặp. | Dòng 574 và 576 đều là: "Khi $d=\infty$, $\Pi_{\mathcal H}(2m)=2^{2m}$, nên $\rho_m\ge\sqrt{16\ln2}\approx3{,}33$: phần (a) vẫn đúng nhưng không cho thông tin. Khi $d=0$, …". | Xóa dòng 576 và một dòng trống đi kèm. Chạy lại `sync-local-materials.py`. |
| nhẹ | §11, cầu nối, dòng 919 | Cận cho rủi ro vượt mức so với lớp là $2\rho_m$ (Hệ quả 03.16(a)), không phải $\rho_m$. Câu hiện tại có thể đọc thành "cận cho số hạng thứ hai tăng từ $0{,}164$ lên $0{,}280$", trong khi đó là cận độ lệch đều. Cận cho rủi ro vượt mức tăng từ $0{,}329$ lên $0{,}560$ ($2\cdot0{,}16443$ và $2\cdot0{,}27986$). | "Cận cho số hạng thứ hai, rủi ro vượt mức so với lớp, tăng theo cận độ lệch đều, từ $0{,}164$ lên $0{,}280$ ở $m=10^4$ (Ví dụ 03.7)." | "Cận cho số hạng thứ hai, rủi ro vượt mức so với lớp, bằng hai lần cận độ lệch đều (Hệ quả 03.16(a)). Ở $m=10^4$, cận độ lệch đều tăng từ $0{,}164$ lên $0{,}280$ (Ví dụ 03.7), nên cận cho rủi ro vượt mức tăng từ $0{,}329$ lên $0{,}560$." |
| nhẹ | Ví dụ 03.9, Bước 1, dòng 734 | Dấu $<0$ của đạo hàm không có lý do. Bản cũ có "vì $\ln(2em/d)>1$". | "đạo hàm của … bằng $\big(d-d\ln\tfrac{2em}d-c\big)/m^2<0$." | Thêm vào sau "$<0$": ", vì $\ln\tfrac{2em}d\ge\ln(2e)>1$ khi $m\ge d$ và $c>0$". |
| nhẹ | §9, đoạn cuối, dòng 876 | Định lý 03.19(b) cho cận dưới $c\,(d+\ln(1/\delta))/\epsilon$, không chỉ theo $d/\epsilon$. | "Định lý 03.19(b) chỉ cho cận dưới theo $d/\epsilon$" | "Định lý 03.19(b) chỉ cho cận dưới cỡ $(d+\ln(1/\delta))/\epsilon$" |

**Ngoài phạm vi toán học, ghi để master biết.** `materials/lec-03/exercises.md` vẫn chưa có. Ghi chú hiện dẫn Bài tập 03.3, 03.5 và 03.11; dòng 821 giao cho Bài tập 03.11 phép kéo theo (4)⇒(6), nên người viết bài tập phải chứng minh đầy đủ phép kéo theo này.

## Các con số đã kiểm lại

Tổng cộng 16 giá trị, gồm các giá trị mới và các giá trị bị đổi chỗ:
- $\ln480=6{,}17379$, $\ln240=5{,}48064$, $0{,}22224$, $0{,}05235$, tỉ số $4{,}245$.
- Sự trùng nhau giữa dạng đóng tại $\epsilon/2$ và $M(\epsilon,\delta)$ (9 bộ tham số).
- $w=(2,2)$, $b=-1$ ở Ví dụ 03.3.
- $16=\binom62+1$.
- $2\rho_m$ ở cầu nối: $0{,}329$ và $0{,}560$.

Phép tính chạy bằng Python trong scratchpad. Các con số không đổi đã được kiểm ở lượt rà 2 (126 giá trị) và vẫn đúng.
