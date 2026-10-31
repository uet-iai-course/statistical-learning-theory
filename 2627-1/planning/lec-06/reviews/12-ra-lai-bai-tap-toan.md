# Rà lại toán bộ bài tập Bài 06 sau khi sửa (R2)

Đối tượng: `lec06-ex-r1-frozen.md` (trùng byte với `exercises.md`), diff `lec06-ex-r1.udiff`. Script: `reviews06/r2/ex/ex.py` (số cũ), `reviews06/r2/ex/ex_r1.py` (số mới).

**Tổng kết:** cả hai phát hiện cũ đã sửa đúng. Phát hiện mới: `chặn bàn giao` 0; `nghiêm trọng` 0; `trung bình` 0; `nhẹ` 1. Mọi phần toán đã đổi dựng lại đều đúng; số mới tính lại đều khớp.

## 1. Phát hiện cũ

| Phát hiện cũ | Kết luận | Ghi chú |
|---|---|---|
| Nhẹ 1: 06.5(c)/(d) làm tròn xuống $0{,}0466$; $2{,}3955$ | ✓ | Dòng 295–296 ghi "$\le0{,}0467$", "$\le2{,}3956$" (giá trị đúng $0{,}046627$; $2{,}395542$); dòng 305 dùng cùng số. |
| Nhẹ 2: 06.2(c) dùng tên Định nghĩa 06.4 cho mẫu không i.i.d. | ✓ | Đề (dòng 126) nay ghi $\mathbb E[L_D(A(S))-L_S(A(S))]$. |

## 2. Các phần đổi, dựng lại

| Phần | Kết luận | Ghi chú |
|---|---|---|
| 06.3 sau khi bỏ ý cũ (a) | ✓ | (a) đối xứng, (b) một phía, (c) bằng số; mọi dẫn chiếu nội bộ đã đổi tên đúng ("Bước 2 của (a)", "Bước 3 trong (a)", "Bước 1–3 của (b)", "Bước 4 của (c)"). "Tính lồi của $W$ được dùng ở Bước 1 của chứng minh Bổ đề 06.7" đúng. 06.11 Bước 4 dẫn "Bài tập 06.3(b)" cho lập luận một phía, đúng. Không còn dẫn "06.3(c)/(d)" ở bài tập hay ghi chú. Bước 3 mới ($F_{s,1}$ có cực tiểu tại $\hat w$, nên hiệu $=1{,}3125\cdot64/441=4/21$) đúng. |
| 06.4(c) hệ số ổn định logistic | ✓ | $G=4$, $m=1600$: $\epsilon_{\mathrm{stab}}=32/(0{,}2\cdot1600)=0{,}1$ tại $\lambda_0$ và $32/(0{,}1\cdot1600)=0{,}2$ tại $\lambda^*$. Số hạng khớp $\lambda B^2/2$ với $B=2$ bằng $0{,}4$ và $0{,}2$; tổng $0{,}5$ và $0{,}4$, khớp Bước 3–4. |
| Gợi ý mới 06.4 | ✓ | Gợi ý 1 cho (d) ("tính tối ưu của mỗi nghiệm cho mục tiêu của chính nó, so với nghiệm kia") dẫn đúng tới phép cộng ở Gợi ý 2. |
| Gợi ý mới 06.5 | ✓ | "So giá trị nhỏ nhất với giá trị tại một điểm cụ thể; chặn $F(\hat w_s)$ từ dưới", rồi Gợi ý 2 nêu điểm $0$ và $\ell\ge0$. Đúng hướng. |
| Gợi ý mới 06.7 | ✓ | Chia đôi $\epsilon$ và $\delta$ giữa khối tốt nhất và bước chọn trên $V$, khớp lời giải ($\epsilon/2+\epsilon/2$, $\delta/2+\delta/2$). "Xét dấu … rồi dùng một bất đẳng thức chỉ cần kì vọng" dẫn tới Markov. |
| Gợi ý mới 06.8 | ✓ | "Tìm một điểm của $W$ có $L_S=0$ khi một tọa độ bị tắt" dẫn tới $\mathbf e_j$; Gợi ý 2 xác nhận. |
| Gợi ý mới 06.9 | ✓ | Thêm bớt $L_S(A(S))$ và $\inf_{\mathcal H}L_S$ như Mệnh đề 06.5, mỗi định nghĩa chặn một số hạng; Gợi ý 2 nhắc kiểm khả tích trước khi trừ. Đúng. |
| Kí hiệu $\bar m$ (06.7) | ✓ | Đổi nhất quán ở đề, gợi ý và lời giải; không còn $m_{\mathcal H}(\epsilon)$ một tham số; câu phân biệt với $m_{\mathcal H}(\epsilon,\delta)$ đúng. Công thức và số không đổi ($160\,000$; $43\,340$; $78\,954$). |
| Kí hiệu $W_{r_\lambda}$ (06.5) | ✓ | Với $W=\mathbb R^p$, $W_{r_\lambda}=\{w:\lVert w\rVert\le r_\lambda\}$ khớp định nghĩa $W_B$ với $B=r_\lambda$; các Bước 3–5 không đổi nội dung. |
| Kí hiệu $\Omega$ (06.11) | ✓ | Thay $R$ ở mọi chỗ (đề, gợi ý, lời giải, kiểm tra); tránh trùng với $R$ của SGD. |
| Kí hiệu $h_0$ (06.9) | ✓ | Thay $h'$ ở đề, gợi ý và Bước 1, 3; công thức đúng. |
| 06.2(b1) Bước 3 viết lại | ✓ | $\operatorname{Var}\tfrac{Z'+Z_2}2+\operatorname{Var}Z_1=\tfrac18+\tfrac14$ (đúng vì cùng kì vọng nên số hạng chéo bằng $0$); hiệu $0{,}25$. |
| 06.5(d) Bước 3 viết lại | ✓ | "Nhỏ hơn khi $\lambda\le0{,}1$": hai cận bằng nhau khi $8(\sqrt{2/\lambda}+1)^2=192$, tức $\lambda\approx0{,}1316$, nên khẳng định đúng với mọi $\lambda\le0{,}1$, không chỉ hai giá trị được tính. |
| 06.4(c), 06.7(c) chia bước; 06.6 sửa chính tả; 06.10 Bước 1 và 06.9 Bước 5 rút gọn; 06.8 bỏ câu UML | ✓ | Không đổi toán. |

## 3. Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | Bài tập 06.4, lời giải (c), Bước 5, câu sau công thức (dòng 437) | "Ổn định gấp đôi" mơ hồ về toán: hệ số ổn định là cận trên của độ nhạy, nên điều đúng là hệ số giảm một nửa, không phải một đại lượng "ổn định" tăng gấp đôi. | $\epsilon_{\mathrm{stab}}$: $0{,}2$ tại $\lambda^*=0{,}1$, còn $0{,}1$ tại $\lambda_0=0{,}2$. | Viết "Hệ số lớn hơn làm hệ số ổn định giảm một nửa, nhưng số hạng khớp …" (số tiếng gần như không đổi). |
