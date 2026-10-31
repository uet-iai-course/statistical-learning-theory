Số phát hiện mới: chặn bàn giao 0 · nghiêm trọng 0 · trung bình 1 · nhẹ 3.

# Rà lại toán học — Bài tập Bài 04 sau vòng sửa 1

Người rà: cùng vai trò độc lập về toán như `9-bai-tap-toan.md`, chỉ đọc. Đầu vào: `lec04-ex-round1-frozen.md` (dẫn theo số dòng của bản này), `lec04-ex-round1.diff`, `lec04-note-exround.diff`, `reviews/11-quyet-dinh-bai-tap.md`, `bai-tap-ghi-chu.md` §7. Số tính lại trong `rev04/m9/num5.py`.

## 1. Trạng thái các phát hiện cũ

### 17 phát hiện của `9-bai-tap-toan.md`

| # | Phát hiện | Trạng thái | Dòng |
|---|---|---|---|
| 1 | 04.3(d) chỉ đúng với hàm lỗi 0–1 | ✓ | 282 (đề), 356–358 (phạm vi với hàm lỗi tổng quát) |
| 2 | 04.11 bỏ ý 1–2 của UML 7.5 mà không nói | ✓ | 892 (tiêu đề "ý 3–5"), 897; §10 của ghi chú sửa cùng (diff ghi chú) |
| 3 | 04.6 quy tắc 1 "một kết quả khác là lỗi" | ✓ | 620 |
| 4 | 04.6 dẫn sai Bài tập 04.4(d) cho quy tắc 2 | ✓ | 623 (lý do là (T3) của Định nghĩa 04.8, Định lý 04.11, Hệ quả 04.17) |
| 5 | 04.4(d) nghiệm ERM trên $\mathcal H_2$ không duy nhất | ✓ | 459, 461, 470 |
| 6 | 04.3(d) điều kiện $\Pr(B_{k_0})\le\delta q_{k_0}$ | ✓ | 354 |
| 7 | 04.13 giả thiết $\lvert\mathcal H_k\rvert=2^k$ là phần thêm | ✓ | 1009 |
| 8 | Làm tròn xuống ở cận trên ($0{,}5399$; $0{,}1683$; $0{,}0319$) | ✓ | 690, 694, 1088 |
| 9 | 04.7(b) cả hai cận tại $m=10^3$ lớn hơn $1$ | ✓ | 679 |
| 10 | 04.10 chữ $L$ trùng kí hiệu; danh sách đếm được | ✓ | 855 ($B_0$), 859 |
| 11 | 04.9 dùng $n(h)$ thay cho $k(h)$ | ✓ | 743–810 (đổi sạch, xem mục 4) |
| 12 | 04.13 $k$ là số lớp | ✓ | 1009–1088 ($k_{\max}$) |
| 13 | 04.2(a) thiếu Jensen cho tính khả tích | ✓ | 145 |
| 14 | 04.4 "Kiểm tra lại" chỉ tính lại một ô | ✓ | 485 (kiểm điều kiện dừng không bỏ sót) |
| 15 | 04.2(c) chủ ngữ trừu tượng (văn phong) | ✓ | 249 |
| 16 | 04.7 $I_j$ có độ dài dương | ✓ | 635 |
| 17 | 04.12 gợi ý 2 gần là lời giải | ✓ | 975 |

### T1–T9 của `11-quyet-dinh-bai-tap.md`

| Mục | Trạng thái | Dòng | Ghi chú |
|---|---|---|---|
| T1 04.4(a) | ✓ | 383, 407–423, 485 | Họ $25$ lớp, dừng ở lớp $19$, $18$ lần gọi bộ giải; ô mới $\mathrm{pen}_{19}$ không có trong ghi chú. |
| T2 04.1(c) | ✓ | 35, 79–90 | Sáu hiệu mới, không lặp Nhận xét 04.4. |
| T3 04.2(d) | ✓ | 124, 251–259 | Xem phát hiện mới N3 (giá trị $-0{,}2$ cần $\mu=1$). |
| T4 04.3(e) | ✓ | 284, 360–371 | Đúng; mục tiêu "3, 5" ở dòng 264 khớp §10 mới. |
| T5 kí hiệu | ✓ | 743–810, 855, 1009–1088 | |
| T6 các bước | ✓ | 425–447 (04.4(b)), 497–502 (04.5(b)) | |
| T7 04.3(d) | ✓ | 282, 350–358 | |
| T8 04.11 | ✓ | 892, 897 | Tiêu đề khớp dòng §10 của ghi chú. |
| T9 04.6 | ✓ | 620, 623 | |

## 2. Các phần mới hoặc viết lại

Tôi tự giải trước khi đọc lời giải.

- **04.1(a), ý xác suất (dòng 31, 64).** Đúng: trên $E_1\cap E_2$, Mệnh đề 04.3(a) với $\operatorname{opt}_S(A(S))\le\epsilon_{\mathrm{opt}}$ cho cận, và $\Pr((E_1\cap E_2)^c)\le\delta+\delta_2$. Xem N4 (cách diễn đạt của đề).
- **04.1(c) (dòng 35, 79–90).** Sáu hiệu $0;0{,}10;0{,}04$ và $-0{,}04;0{,}06;0$ đúng (từ $0{,}32;0{,}22;0{,}32;0{,}28$ của Ví dụ 01.5). Kết luận về dấu và sự phụ thuộc vào mốc đúng.
- **04.2(d) (dòng 124, 251–259).** Sai số xấp xỉ $0$ đúng: $\mathbb E(c-Y)^2=(c-\mu)^2+\sigma^2$, nhỏ nhất bằng $\sigma^2=L^*$ tại $c=\mu$ thuộc lớp; $L^*=\sigma^2\le\inf$ thỏa Định nghĩa 04.1. Độ chệch $(\gamma-1)\mu$. Xem N3.
- **04.3(d) (dòng 350–358).** Đúng, đã nêu phạm vi.
- **04.3(e) (dòng 284, 360–371).** Đúng. Bước hỏng là bất đẳng thức thứ hai ở Bước 3 của Bổ đề 04.9 ($\sum_k\delta q_k\approx0{,}3743>\delta$); Bước 2 vẫn đúng vì $\delta/k\in(0,1)$. Với $k\ge4$, bán kính $\ge0{,}5037>\tfrac12\ge$ độ lệch, nên $B_k=\varnothing$ (biến cố hỏng dùng dấu $>$). Với $k\le3$, bán kính nằm trong $(0{,}4,\,0{,}5)$, nên $B_k=\{L_S(h_k)\in\{0,1\}\}$, xác suất $2^{-9}$, và các tọa độ độc lập. Bước 4 nói đúng điều cần nói: một phân bố có xác suất thất bại nhỏ không cho cận đều theo $D$. Lời giải không khẳng định có một phân bố làm kết luận sai với $q_k=1/k$, và đúng là không cần.
- **04.4(a) (dòng 383, 407–423, 485).** Tính lại $\mathrm{pen}_k$ với $k=11..25$: dãy tăng, $\mathrm{pen}_{18}=0{,}3599<v=0{,}36504\le\mathrm{pen}_{19}=0{,}3676$. Với $11\le k\le18$, tổng nhỏ nhất là $0{,}4526$, không thay $v$. Thuật toán dừng ở bước 2 của lớp $19$, trước khi gọi bộ giải, nên bộ giải được gọi $18$ lần. Danh sách $25$ lớp hữu hạn và $\sum_{k\le25}q_k<1$, nên đầu vào của Thuật toán 04.12 thỏa. Đúng.
- **04.4(b) (dòng 425–447).** Các ô $k=3$ và các tổng tính lại đúng (danh sách số).
- **04.5(b) (dòng 497–511, 540–578).** Đúng. Danh sách $\mathcal G(S)$ có không quá $K_0^J$ phần tử; mọi $g^{(j)}$ thuộc danh sách nhờ phép giữ nguyên.
- **04.6 (dòng 586–625).** Đúng.
- **04.9 (dòng 738–811).** Phép đổi $n\to k$ sạch (diff từng dòng, mục 4); lời giải không đổi về toán.
- **04.10 (dòng 855, 859).** Đúng. $B_0\ge\lvert h_0\rvert\ge0$, vì số hạng căn của $h_0$ không vượt $\Phi(h_0)$.
- **04.11, tiêu đề và câu mở đầu (dòng 892, 897).** Mô tả đúng việc dùng UML 7.5. Ý (c) Bước 2 thêm một câu mới (dòng 935); xem N1.
- **04.13 (dòng 1009–1088).** Đúng. Điểm đổi chiều: tại $k_{\max}=118$, $0{,}131281<0{,}131290$; tại $119$, $0{,}131808>0{,}131334$; cách 2 tốt hơn với mọi $k_{\max}\ge119$ (đã kiểm đến $1500$).

## 3. Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 04.11(c) Bước 2, dòng 935 | Suy luận sai chiều: "Cỡ mẫu $M(\epsilon,\delta,h)$ tăng theo $k(h)$ và không bị chặn trên $\mathcal H$, nên không có cỡ mẫu chung như Định nghĩa 01.25 đòi." $M$ ở đây là cỡ mẫu đủ do Hệ quả 04.15 cho; việc nó không bị chặn không chứng minh rằng không có cỡ mẫu chung. Kết luận đúng, nhưng lý do là (b) (chiều VC vô hạn, Định lý 03.17(a)). Câu này chạm đúng mục tiêu học tập 4, nên cách suy luận cần đúng. | So với (b), dòng 929. Phần "không bị chặn" thì đúng: với $m$ cố định và $n\ge m$, $\Pi_{\mathcal H_n}(2m)=2^{2m}$, nên $\rho_m\ge\sqrt{16\ln2}>1$ và $M_n(\epsilon)>m$. | "Cỡ mẫu $M(\epsilon,\delta,h)$ tăng theo $k(h)$ và không bị chặn trên $\mathcal H$. Theo (b), không có cỡ mẫu chung nào, nên sự phụ thuộc vào $h$ là cần." |
| nhẹ | 04.11(c) Bước 1, dòng 933 | Chỉ số của dãy hữu tỉ viết $u_i$, $v_i$, trùng kí hiệu đầu mút $[u_i,v_i]$ của khoảng thứ $i$ trong đề (dòng 897). Bản trước viết $u_k$; vòng sửa đổi thành $i$. | Dòng 897: "$I_i$ là một khoảng đóng $[u_i,v_i]$". | Dùng chỉ số khác, ví dụ $u^{(t)}\uparrow u$, $v^{(t)}\downarrow v$, "khi $t$ đủ lớn". |
| nhẹ | 04.2(d) Lời giải Bước 2–3, dòng 255, 257 | "$(0{,}8-1)\mu=-0{,}2$" chỉ đúng khi $\mu=1$; đề (d) dẫn "thiết lập của (b)", nơi $\mu$ là tổng quát và chỉ phần số dùng $\mu=1$. "$0{,}8\mu\ne\mu$" cần $\mu\ne0$. | Dòng 113 ($\mu$, $\sigma^2$ tổng quát; số với $\mu=1$). | "$(0{,}8-1)\mu=-0{,}2\mu$, bằng $-0{,}2$ khi $\mu=1$"; "khác $\mu$ khi $\mu\ne0$". |
| nhẹ | 04.1(a) đề, dòng 31 | Đề vừa cho "một $\epsilon_{\mathrm{opt}}$-ERM $A$" (đúng trên mọi mẫu, dòng 21) vừa viết "giả sử bộ giải chỉ thỏa … trên một biến cố"; người đọc có thể hiểu là cùng $A$. Cũng nên nói biến cố đó đo được. | Dòng 21 và 31. | "Nếu thay giả thiết $\epsilon_{\mathrm{opt}}$-ERM bằng: $\operatorname{opt}_S(A(S))\le\epsilon_{\mathrm{opt}}$ trên một biến cố đo được có xác suất ít nhất $1-\delta_2$, chứng minh …". |

Không có phát hiện mới về văn phong.

## 4. Quét hư hại do thay thế tự động

- **Lệnh LaTeX.** Liệt kê mọi lệnh `\[a-zA-Z]+` trong tệp: 64 tên, tất cả hợp lệ (`\aligned` không còn; không có `\ik`, `\lk`, `\mik`, `\ikfty`, `\operatork…`, `\begik`, `\tfrack`, `pek`). `\begin{aligned}` và `\end{aligned}` cùng 43 lần.
- **04.9 ($n\to k$).** Diff từng dòng với bản đóng băng trước: mọi thay đổi chỉ là $n(h)\to k(h)$, $\mathcal H_n\to\mathcal H_k$, $q_n\to q_k$, $N_n\to N_k$, $g_n\to g_k$, $h_{n,j}\to h_{k,j}$; hai câu bị bỏ ("Mỗi $h$ được tính đúng một lần…", "Trọng số dùng vị trí…"), không ảnh hưởng toán. Không còn $n$ thừa trong 04.9. Chữ tiếng Việt không bị đổi.
- **Ngoài 04.9.** 04.8 và 04.11 vẫn dùng $n$ cho chỉ số giả thuyết hoặc số khoảng, đúng nghĩa. $k_{\max}$ chỉ xuất hiện ở dòng 7 (bảng kí hiệu), 04.3(e) và 04.13; $K_0$ chỉ ở 04.5(b); $B_0$ chỉ ở 04.10. Hư hại duy nhất còn lại liên quan là chỉ số $u_i$, $v_i$ ở 04.11(c) (N2), do đổi tay chứ không do thay thế chữ.

## 5. Danh sách số mới hoặc đổi

| Vị trí | Số in | Tính lại | |
|---|---|---|---|
| 04.1(c) dòng 84–85 | $0;\,0{,}10;\,0{,}04$ / $-0{,}04;\,0{,}06;\,0$ | giống hệt | ✓ |
| 04.2(d) dòng 253–255 | $0$; $-0{,}2$ | $0$; $-0{,}2\mu$ ($=-0{,}2$ khi $\mu=1$) | ✓ (N3) |
| 04.3(e) dòng 362 | $7{,}4855$; $0{,}3743$ | $7{,}485471$; $0{,}374274$ | ✓ |
| 04.3(e) dòng 364 | $e^5/40\approx3{,}71$; $0{,}4295;0{,}4681;0{,}4893;0{,}5037$ | $3{,}710329$; $0{,}429469;0{,}468083;0{,}489259;0{,}503745$ | ✓ |
| 04.3(e) dòng 368 | $0{,}0058$ | $0{,}005848$ | ✓ |
| 04.4(a) dòng 409 | $4{,}880$ | $4{,}879727$ | ✓ |
| 04.4(a) dòng 411 | $0{,}4423;0{,}3790;0{,}3650$ | giống hệt ($v=0{,}365044$) | ✓ |
| 04.4(a) dòng 413 | $\mathrm{pen}_{18}\approx0{,}3599$; $\ge0{,}4421$ | $0{,}359875$; nhỏ nhất $0{,}4526$ ($k=11$) | ✓ |
| 04.4(a) dòng 415–419 | $7{,}9078$; $158{,}16$; $5{,}889$; $10{,}769$; $168{,}92$; $0{,}13514$; $0{,}3676$ | $7{,}907755$; $158{,}155$; $5{,}888878$; $10{,}7686$; $168{,}924$; $0{,}135139$; $0{,}367608$ | ✓ |
| 04.4(a) dòng 423 | $18$ lần gọi | lớp $1$–$18$ có $\mathrm{pen}_k<v$ | ✓ |
| 04.4 Kiểm tra lại dòng 485 | $0{,}5226$ | $0{,}155+0{,}367608=0{,}522608$ | ✓ |
| 04.4(b) dòng 427 | $6{,}685$; $38{,}069$; $44{,}753$; $0{,}1892$ | $6{,}684612$; $38{,}068773$; $44{,}753385$; $0{,}189217$ | ✓ |
| 04.4(b) dòng 430–432 | $0{,}1699$; $0{,}2062$; tổng $0{,}3799;0{,}3642;0{,}3762$ | $0{,}169904$; $0{,}206167$; giống hệt | ✓ |
| 04.4(b) dòng 436 | $6{,}461$; $44{,}530$; $0{,}1887$ | $6{,}461468$; $44{,}530241$; $0{,}188743$ | ✓ |
| 04.4(b) dòng 439–441 | $0{,}1678$; $0{,}2071$; tổng $0{,}3778;0{,}3637;0{,}3771$ | $0{,}167838$; $0{,}207137$; giống hệt | ✓ |
| 04.4(b) dòng 445 | $0{,}4473$; $0{,}4428$; $\ge0{,}3875$; $\ge0{,}3896$ | $0{,}447336$; $0{,}442806$; tổng nhỏ nhất với $k\ge5$ là $0{,}387512$ và $0{,}389642$ | ✓ |
| 04.4(c) dòng 451 | $[0{,}2466;\,0{,}3489]$ | các tổng khác: $0{,}3489$ ($k=1$), $0{,}2466$–$0{,}2563$ ($k=6..10$) | ✓ |
| 04.4(d) dòng 468 | $1{,}1\cdot10^{-40}$ | $1{,}12\cdot10^{-40}$ | ✓ |
| 04.5(b) dòng 563–567 | $15{,}2018$; $0{,}0872$; $0{,}1744$ | $15{,}201805$; $0{,}087183$; $0{,}174366$ | ✓ |
| 04.7 dòng 679 | $1{,}03$; $1{,}47$ | $1{,}031356$; $1{,}468226$ | ✓ |
| 04.7 dòng 683 | $38{,}069$; $5{,}075$; $0{,}03452$; $0{,}1858$; $0{,}2699$ | $38{,}068773$; $5{,}075174$; $0{,}034515$; $0{,}185783$; $0{,}269940$ | ✓ |
| 04.7 dòng 690, 694 | $0{,}5399$; $0{,}1683$ | $0{,}539879$; $0{,}168314$ | ✓ |
| 04.13 dòng 1084 | $0{,}13128/0{,}13129$; $0{,}13181/0{,}13133$; $119$ | $0{,}131281/0{,}131290$; $0{,}131808/0{,}131334$; $119$ | ✓ |
| 04.13 dòng 1088 | $0{,}1018$; $0{,}0319$ | $0{,}101817$; $0{,}031860$ | ✓ |

Các số không đổi (04.1(b), 04.2(b)(c), 04.3(a)–(c), 04.4(c)(d), 04.5(a)(c), 04.7(b), 04.9, 04.10, 04.13 bảng) khớp danh sách của `9-bai-tap-toan.md`; đã đối chiếu lại các dòng tương ứng.

## 6. Kết luận

**Giao được.** Cả 17 phát hiện cũ và T1–T9 đều đã sửa. Không có phát hiện mới mức chặn bàn giao hay nghiêm trọng. Đề nghị sửa N1 (một câu ở dòng 935) trước khi phát hành; N2–N4 là sửa một dòng.
