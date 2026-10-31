# Bài 05 — Rà lại bài tập: toán học

**Số phát hiện theo mức độ:** chặn bàn giao 0 · nghiêm trọng 0 · trung bình 0 · nhẹ 1.

Đầu vào: `2627-1/materials/lec-05/exercises.md` hiện tại (1106 dòng; số dòng dẫn theo tệp này), `lec05-ex-r1.diff`, `planning/lec-05/reviews/11-quyet-dinh-bai-tap.md`. Mã: `py/r05_ex_2.py` tính lại mọi số mới; `py/r05_tex.py` kiểm cú pháp (108 dấu `$$`, 1425 đoạn công thức cân bằng ngoặc và `aligned`); `py/r05_ex_render.py` dựng trang trong Chromium qua HTTP (1425 phần tử `.katex`, 0 `.katex-error`, 0 lỗi trang).

## 1. Sáu phát hiện của lượt trước

| # | Phát hiện | Trạng thái | Bằng chứng (dòng hiện tại) |
|---|---|---|---|
| 1 | 05.10: $0{,}9950$ là cận làm tròn xuống | ✓ | 924: $0{,}9951$ (giá trị $0{,}99504$). Thêm 930: $1/\sqrt2\approx0{,}7072$, làm tròn lên. |
| 2 | 05.10(d): "không cần biết $\lVert w^\circ\rVert$" | ✓ | Đề (d) đổi thành "giải thích vì sao có thể chạy thuật toán mà không biết $\lVert w^\circ\rVert$". Bước 6 (928) nói đúng: độ dài bước không cần $\lVert w^\circ\rVert$ (nhờ tính bất biến theo tỉ lệ ở Bước 5), số vòng lặp đủ theo cận thì cần, và có thể dừng ở $T$ đầu tiên mà $\bar w_T$ phân lớp đúng $S$, muộn nhất ở $\lfloor\lVert w^\circ\rVert^2C_x^2\rfloor+1$. **Ghi chú cho điều phối viên:** quyết định 11 viết "$\eta$ không cần $\lVert w^\circ\rVert$ là sai — cần $\lVert w^\circ\rVert$ cho cả $\eta$ và $T$ theo cận". Người viết giữ "độ dài bước không cần $\lVert w^\circ\rVert$", và điều đó **đúng**: Bước 5 chứng minh mọi $\eta>0$ cho cùng dấu của $\tilde y_i\langle\bar w_T,x_i\rangle$. Chỉ công thức $\eta=R/(G\sqrt T)$ của cận mới chứa $\lVert w^\circ\rVert$. Không cần sửa thêm. |
| 3 | 05.2(b): cả hai bất đẳng thức của Bổ đề 05.8(b) hỏng | ✓ | Bước 2 và Bước 4 của (b): $4>0{,}8$, $4>1{,}44$; $4>0$, $4>1$; có câu "Mệnh đề 05.13 chỉ dùng bất đẳng thức thứ hai". |
| 4 | 05.8(b): dẫn Mệnh đề 05.5(b) | ✓ | 784: $U=\mathbb R^p$ mở; $w=-t\tilde yx$ cho $s_w=-t\lVert x\rVert^2\to-\infty$, nên $L\ge\lVert x\rVert$. |
| 5 | 05.5(c): dấu bằng lấy từ chứng minh Mệnh đề 05.20 | ✓ | 495: "số hạng chéo ở Bước 2 của chứng minh Mệnh đề 05.20 bằng $0$, và đẳng thức ở bước đó cho…". |
| 6 | 05.7: cấu trúc trùng bản lời giải UML | ✓ | 680–731: mẫu $((1,0),1)$, $((1,1),0)$ và $w=(-1,-1)$, khác bản lời giải $(e_1,-e_1)$. |

## 2. Bảng phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | 05.2(c), Bước 3 (dòng 218) | "Theo Ví dụ 05.7, $\lVert w-u\rVert^2\approx0{,}00344$", nhưng Ví dụ 05.7 của ghi chú in $0{,}0034$ (dòng 686 của ghi chú). Số $0{,}00344$ đúng ($0{,}003437$), chỉ không phải số được dẫn. | `r05_ex_2.py`. | "$\lVert w-u\rVert^2\approx0{,}00344$ (Ví dụ 05.7 in $0{,}0034$)", hoặc tính trực tiếp từ $w-u\approx(-0{,}0402;-0{,}0427)$ ở Bước 1: $0{,}00162+0{,}00182\approx0{,}00344$. |

## 3. Các phát biểu và lời giải đã đổi, dựng lại: không có lỗi

- **05.1(b), Bước 2.** $\langle cx+r,r\rangle=c\langle x,r\rangle+\lVert r\rVert^2=\lVert r\rVert^2$ vì $r\perp x$ và $\ell(w_0)=0$.
- **05.2(a), dạng mới.** Từ giả thiết $\lVert w^+-u\rVert\le\lVert w-\eta g-u\rVert$, bình phương, khai triển và chuyển vế cho bất đẳng thức. Bước 4 dẫn Bổ đề 05.8(b) để kiểm giả thiết cho $w^+=\operatorname{proj}_W(w-\eta g)$: đúng, và đúng là chỗ duy nhất dùng phép chiếu, tính lồi của $W$, $u\in W$. Dấu bằng khi $W=\mathbb R^p$: đúng.
- **05.2(c), bước thứ ba với $i_3=1$.** $w-u=(-0{,}04022;-0{,}04265)$; vế trái $0{,}023562$. $w-\eta g=(1;-0{,}7071)$, chuẩn $1{,}2247$, $w^+=(0{,}8165;-0{,}5774)$. $w^+-u=(0{,}06917;0{,}08710)$, bình phương chuẩn $0{,}012371$. $(w-\eta g)-u=(0{,}25267;-0{,}04265)$, bình phương chuẩn $0{,}065662$. $\lVert g\rVert^2=0{,}343146$, $\tfrac\eta2\lVert g\rVert^2=0{,}085786$. Vế phải $0{,}076853\approx0{,}0769>0{,}0236$. Không chiếu: $0{,}023562$, bằng vế trái. Hiệu $0{,}053291\approx0{,}0533$. "Ra xa $w^*$" ($0{,}01237>0{,}00344$) đúng, và câu "bất đẳng thức vẫn đúng nhờ số hạng $\tfrac\eta2\lVert g\rVert^2$" đúng.
- **05.3(b).** $\psi=\tfrac23\sum_ir_ix_i$: $\tfrac23(0{,}36;1{,}48)$, $\tfrac23(-1{,}48;-0{,}64)$, $\tfrac23(-1,1)$. Ô $(1,2)$: $g_2=(0,2)$, $w_2-u=(0{,}2527;0{,}6645)$, tích $1{,}3289$. Đường chéo bằng $0$, và lý do đúng: phép chiếu không tác động ở bước một. Tổng chín ô $7{,}6139$, chia $9$ được $0{,}8460$. Tổng hàng $2{,}5379$, chia $3$ được $0{,}8460$. $1{,}6667/3=0{,}5556$.
- **05.5(a)–(b) với $\sigma^2=3$.** $T(b)=\lceil100(1+3/b)\rceil$: $400$, $200$, $119$, $105$; số quan sát $400$, $600$, $1904$, $6720$; GD $100$ bước, $10^6$ quan sát (tính bằng phân số). Đọc bảng: điểm gãy $b=\sigma^2/G_F^2=3$, với $T(3)=2\cdot100$; $bT(b)\approx100(b+3)$; so sánh với $b\approx15$ của Ví dụ 05.15 đúng. (b): vì số bước của GD là $100$, một số nguyên, $\lceil x\rceil\le110\iff x\le110$, nên điều kiện là $b\ge10\sigma^2/G_F^2$ (đúng trong thiết lập $R=1$, $\epsilon=0{,}1$, $G_F^2=1$ của bài). $b=30$: $T=110$, $3300$. $b=150$: $T=110$, $16\,500$. Kiểm tra lại đúng.
- **05.5(c), (d).** Bước 4–5 tách thành danh sách, nội dung không đổi và vẫn đúng.
- **05.6, đổi kí hiệu $\rho\to r$, $v_t\to q_t$.** Mọi công thức của (a)–(e) và dòng **Kiểm tra lại** đã đổi nhất quán. Không còn $\rho$ trong tệp ngoài dòng 12 (hằng số Lipschitz của UML, đúng ngữ cảnh), và không còn $v_t$. $r$ của 05.6 và phần dư $r_i$ của 05.3, $q_t$ của 05.6 và $q$ của 05.8, 05.12 đều là kí hiệu cục bộ của từng bài, không lẫn nhau.
- **05.7, cấu trúc mới.** $L_S(w)=\tfrac12\mathbb 1[\langle w,(1,0)\rangle<0]+\tfrac12\mathbb 1[\langle w,(1,1)\rangle\ge0]$ khớp quy ước $\mathbb 1[\cdot\ge0]$. $L_S(-1,-1)=\tfrac12$. Lân cận bán kính $\tfrac12$: $\le-\tfrac12$ và $\le-2+\tfrac{\sqrt2}2=-1{,}293$; kiểm thêm trên $2\cdot10^5$ điểm ngẫu nhiên trong lân cận, chỉ có giá trị $\tfrac12$. $w^*=(1,-2)$ cho $0$. (b): $u=(1,3)$ cho $L_S=\tfrac12$; điểm $0{,}6w+0{,}4u=(-0{,}2;0{,}6)$ cho $L_S=1>0{,}5$. (c): hai đường thẳng, điểm dừng. Kiểm tra lại với hàm lỗi bản lề: $2$, $(-1,0)$, $0$, gradient $(-0{,}5;0)$.
- **05.8.** $p\to q$ đã đổi; Bước 3 của (a) viết hai bất đẳng thức tường minh, đúng. $5{,}0068$ là đầu trên của khoảng giá trị ($5{,}006715$), làm tròn lên; đầu dưới $0{,}0067$ ($0{,}006715$) làm tròn xuống, đúng chiều cho một cận dưới.
- **05.10.** Đề (b), (c) viết lại, nội dung toán không đổi. Câu mới ở Bước 1 ("với $\eta=1$, đây là phép cập nhật của Perceptron, áp dụng cho quan sát có $\tilde y_j\langle w_t,x_j\rangle$ nhỏ nhất") đúng. Bước 5–6 đúng như §1.
- **05.11(d) mới.** $3BG/\sqrt T\le0{,}1\iff\sqrt T\ge120\iff T\ge14\,400=9\cdot1600$. Nhận xét về việc phải biết $T$ trước với độ dài bước hằng, và không cần với $\eta_t$ giảm dần, đúng. $477{,}11$ là $477{,}1043$ làm tròn lên; $0{,}2982$ đúng.
- **05.12.** Đề (a) viết lại; lời giải không đổi và vẫn đúng.
- **Quét lỗi biên tập.** Không có LaTeX hỏng, khối `aligned` thiếu cặp hay `$` lẻ. Không còn kí hiệu cũ ($\mathbf e_1$ ở 05.7, $\rho$ và $v_t$ ở 05.6, $p$ ở 05.8). Số hiệu bước trong các lời giải đã đánh lại liên tục: 05.2(a) Bước 1–5, 05.2(b) Bước 1–4, 05.2(c) Bước 1–5, 05.3(b) Bước 1–7, 05.5(c) Bước 1–5, 05.7(a) Bước 1–4, 05.10(d) Bước 1–6.

## 4. Kiểm tra số

Đã tính lại 52 số mới hoặc đã đổi: 05.2(c) (14), 05.3(b) (12), 05.5(a)–(b) (16), 05.7 (5), 05.8 (1), 05.10 (2), 05.11 (2). Tất cả khớp. Mọi cận trên đều làm tròn lên ($0{,}9951$; $0{,}7072$; $5{,}0068$; $477{,}11$; $0{,}2982$).
