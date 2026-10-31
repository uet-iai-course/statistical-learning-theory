# Rà lại toán học sau biên tập vòng 1 — Bài 08 (người rà 2)

Bản kiểm: `lec08-r1-frozen.md`; số dòng ở bảng phát hiện mới theo bản này. Tôi đọc toàn bộ bản sửa, đối chiếu với `0-quyet-dinh.md` (N1 và các mục nhẹ). Phép tính lại nằm ở `reviews08/r2/recheck.py` (đầu ra `recheck_out.txt`); các số không đổi đã kiểm ở `reviews08/r2/check.py`. Phạm vi chỉ gồm toán học, nên không dùng `no-ai-slop`. Tôi chỉ đọc, không sửa repo và không commit.

## 1. Tổng kết theo mức

| Mức | Phát hiện mới |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 0 |
| nhẹ | 2 |

Cả 11 phát hiện cũ đã được xử lý đúng. Mọi phần toán thay đổi đều dựng lại được và mọi số mới đều khớp. Bản sửa không đưa thêm lỗi toán học nào.

## 2. Phát hiện cũ (`2-toan-hoc.md`)

| Phát hiện cũ | Kết quả | Vị trí trong bản r1 |
|---|---|---|
| trung bình: chỗ dùng tính lồi mâu thuẫn với chứng minh (§9, §5, §6) | ✓ | Bước 2 của 08.5 (dòng 342–351) không còn điểm trung gian, chỉ dùng phép chiếu không giãn, bất đẳng thức tam giác và (G). Các câu ở dòng 305, 309, 411, 497, 690, 744 và Phụ lục F (dòng 1106, 1110) nay nhất quán: tính lồi **của hàm lỗi** chỉ đi vào qua Bổ đề 08.4(a) ở bước chung, còn tính lồi **của $W$** cho phép chiếu và tính Lipschitz |
| nhẹ: giả thiết khả tích của Mệnh đề 08.12 | ✓ | dòng 782, 1022 |
| nhẹ: "giảm về" chỉ đúng khi $m>2$ | ✓ | dòng 625 |
| nhẹ: ví dụ đạt hằng số ở 08.10(a) vi phạm (G) | ✓ | dòng 723 dùng hàm cosin |
| nhẹ: so cận khoảng cách tham số với miền giá trị hàm lỗi | ✓ | dòng 746 |
| nhẹ: "nhỏ nhất ở 5–10 vòng" | ✓ | dòng 684 |
| nhẹ: HRS §7 | ✓ | dòng 912 |
| nhẹ: ReLU cần trọng số ra khác 0 | ✓ | dòng 827 |
| nhẹ: Bài 07 chỉ có lập luận, không có chứng minh | ✓ | dòng 682 |
| nhẹ: Ví dụ 05.12 không trơn | ✓ | dòng 632 |
| nhẹ: phạm vi xáo trộn lại của 08.5 | ✓ | dòng 317, 367, 983 |
| ngoài phạm vi: câu hỏi tu từ ở dòng 23 | ✓ | dòng 23 |

## 3. Phần toán đã đổi

| Phần | Kết quả | Kiểm tra |
|---|---|---|
| N1, Mệnh đề 08.5 Bước 2 | ✓ | $\Delta_{t+1}\le\lVert(w_t-w'_t)-\eta_t(g-g')\rVert\le\Delta_t+\eta_t\lVert g\rVert+\eta_t\lVert g'\rVert\le\Delta_t+2G\eta_t$. Bước này chỉ cần (G) tại $w_t,w'_t\in W$ và tính không giãn của phép chiếu; không dùng tính lồi của hàm lỗi và không dùng $\eta_t\le2/\beta$. Cách làm này giống HRS Lemma 3.3 và 2.5 |
| Mệnh đề 08.5 với mọi quy tắc có $\Pr(i_t=i)=1/m$ | ✓ | (a) đúng trên từng quỹ đạo với mọi dãy dùng chung; (b) chỉ dùng xác suất biên, không cần độc lập. Xáo trộn lại sau mỗi vòng, và cả một hoán vị rút một lần rồi dùng lại (dòng 983), đều cho $\Pr(i_t=i)=1/m$ do tính đối xứng. Định lý 08.6 vẫn đúng vì $\xi$ độc lập với $S$ và hữu hạn giá trị; Hệ quả 08.8 chỉ phát biểu cho rút có hoàn lại vì Định nghĩa 05.10 đòi các lần rút độc lập: đúng |
| Định lý 08.6 Bước 1 (định lý giá trị trung bình trên $W$) | ✓ | $W$ lồi nên đoạn thẳng nằm trong $W$; $\ell(\cdot,z)$ khả vi trên $\mathbb R^p$ nên định lý giá trị trung bình áp dụng được; (G) dùng tại điểm trung gian thuộc $W$. Không cần tính lồi của $\ell$. Dòng 109 cũng đúng: (G) và $W$ lồi kéo theo (L) |
| Định lý 08.6 Bước 4 | ✓ | $\ell(w_{T+1},z)\le\ell(w_1,z)+G^2\sum_t\eta_t$ với mọi $z$. Lấy $z=Z_j$, lấy trung bình theo $j$ rồi kì vọng, và dùng Mệnh đề 01.7 cho $w_1$ cố định: $\mathbb EL_S(w_{T+1})\le L_D(w_1)+G^2\sum_t\eta_t$. Phụ lục E dùng đúng cận này |
| Phụ lục E (Hệ quả 08.8) | ✓ | Không đổi so với bản đã kiểm, chỉ chuyển chỗ. Bước 1 nay dựa trên Bước 1 mới (định lý giá trị trung bình) để có $L_D\le L_D(w_1)+GR$ trên $W$: hợp lệ. $\eta^*=R/(G\sqrt{T+2T(T-1)/m})$ bằng $\sqrt{a/b}$ |
| Phụ lục F (Mệnh đề 08.10) | ✓ | (a) $(1+\beta\eta)$, với phép chiếu không giãn. (b) Bước chung dùng (a); bước khác biệt dùng Bước 2 của 08.5, cho $\Delta_t+2G\eta_t\le(1+\beta\eta_t)\Delta_t+2G\eta_t$. (c) Kì vọng tuyến tính, không cần độc lập. Tổng hình học bằng $((1+\beta\eta)^T-1)/\beta$ |
| Mệnh đề 08.10(a), hàm cosin | ✓ | Đạo hàm của $w\mapsto w+\eta\sin(w-z)$ là $1+\eta\cos(w-z)\le1+\eta$, dấu bằng tại $w=z$; (G) đúng với $G=1$ và $\ell\in[0,2]$. Kiểm số: cực đại $1{,}37$ khi $\eta=0{,}37$ |
| Mệnh đề 08.12, giả thiết khả tích | ✓ | Có trong phát biểu (dòng 782) và được dùng ở Bước 4 (dòng 1022) |
| Ví dụ 08.2 (đạo hàm tại $w'_t$ là $0;1;-1;-1;1;0$) | ✓ | Tính lại cho đúng dãy này và $w'_{t+1}$ khớp bảng |
| §4 ($\mathbb Ew_2=\tfrac38$, $\mathbb Ew'_2=\tfrac18$; $\tfrac14$ so với $\tfrac38$) | ✓ | Giá trị $w_2$ trên $s$: $0,\tfrac12,\tfrac12,\tfrac12$; trên $s^{(4)}$: $0,\tfrac12,\tfrac12,-\tfrac12$. Hiệu hai kì vọng là $\tfrac14$; kì vọng của trị tuyệt đối là $\tfrac14$ khi ghép cặp và $\tfrac38$ với hai dãy độc lập |
| Ví dụ 08.4 (bảng $w_3,w'_3,\Delta_3$; nhóm $i_1\ne4$; $w_7=2$, $w'_7=-1$) | ✓ | Bảng $(\tfrac14,-\tfrac14,\tfrac12)$, $(\tfrac34,0,\tfrac34)$, $(1,0,1)$, $(1,-1,2)$; với $w_2\in\{0,\tfrac12\}$, $w_2-3<-1$, $w_2+3>1$ và $\Delta_3=1$; dãy $(2,3,1,4,4,4)$ cho $w_7=2$, $w'_7=-1$ |
| Ví dụ 08.7 | ✓ | $\eta^*=0{,}028868\approx0{,}0289$; $250/T^2=5\cdot10^{-6}\Rightarrow T^2=5\cdot10^7$, $T^*=7071$. Bảng (làm tròn lên): $0{,}099995\to0{,}1000$; $0{,}095706\to0{,}0958$; $0{,}099995\to0{,}1000$; $0{,}137495\to0{,}1375$; $0{,}279995\to0{,}2800$. $7071<m$ |
| Ví dụ 08.6 Bước 3 | ✓ | $0{,}5/0{,}045=11{,}11$; $100/0{,}919=108{,}81$ |
| Phụ lục D, các số không ghép cặp | ✓ | $2{,}99;3{,}83;4{,}90;4{,}93;4{,}82;4{,}34;4{,}00$ khớp lần chạy lại (`exp_eta05.txt`); đỉnh ở 10 vòng rồi giảm. "15–25 giây" khớp lần đo $24{,}5$ giây |
| Nhận xét 08.11 (hằng số viết lại) | ✓ | Cùng biểu thức HRS Thm 3.12 |
| §13 (HRS: $w_0$; Thm 3.8 dạng $\frac{2L^2}n\sum_{t=1}^T\alpha_t$; hai cách rút; $\sqrt3$, $\sqrt2$ "at most worse") | ✓ | HRS tr. 8, 9, 19 |

## 4. Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | dòng 497 | Câu "Giả thiết (G) được dùng hai lần" thiếu một lần dùng: Bước 4 (tính khả tích) cũng dùng (G) để có $\lVert g_t\rVert\le G$. Lỗi này đã có từ bản nháp. | Dòng 475: "Bước 4 (tính khả tích; (G) và (T2)). Theo (G), gradient $g_t$ … có chuẩn không quá $G$". | "Giả thiết (G) được dùng ở bước khác biệt, cho tính Lipschitz tại mọi quan sát kiểm tra, và cho tính khả tích ở Bước 4." |
| nhẹ | dòng 1110 | Câu kết Phụ lục F nói thừa số thay cho $1$ "ở các bước chung". Thực ra (b) và (c) nhân $(1+\beta\eta_k)$ ở mọi bước, kể cả bước khác biệt (dòng 1106: "không quá vế phải của (b)"). Cách viết thô này là cần thiết: nó cho phép lấy kì vọng mà không cần $i_t$ độc lập với $\Delta_t$. | Dòng 737: tích $\prod_{k=t+1}^T(1+\beta\eta_k)$ chạy trên mọi $k$. | "Thừa số $1+\beta\eta_k$ xuất hiện vì các bước chung, chỗ duy nhất mà tính lồi của hàm lỗi từng được dùng; để lấy kì vọng không cần tính độc lập, (b) nhân thừa số này ở mọi bước." |
