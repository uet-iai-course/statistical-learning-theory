# Duyệt deck Bài 04 — Vai 2 `toan-hoc` (độ chính xác toán học, thống nhất với ghi chú)

Bản duyệt: `2627-1/lecture-04-phan-tich-sai-so.html` (55 trang, đóng băng), `img/lec-04/{phan-tich-sai-so,srm-danh-doi,can-xac-thuc}.svg`. Đối chiếu: `materials/lec-04/lecture-note.md`, `exercises.md`, ghi chú Bài 01 (Ví dụ 01.1, 01.2, 01.5, 01.6), Bài 02 (Định lý 02.14), Bài 03 (Định lý 03.15); quyết định cuối `review-log.md` mục "Bộ trang chiếu". Chỉ đọc; không sửa deck, SVG, ghi chú.

## 1. Tính lại các con số

Tính bằng Python (`/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-04/rv-toan-hoc/check.py`, `svgcheck.py`). Mọi con số trên mặt trang, trong ghi chú diễn giả và trong SVG đều khớp ghi chú và `exercises.md`, trừ hai chỗ làm tròn xuống trong một cận trên (phát hiện 6).

| Trang | Đại lượng | Giá trị tính lại | Deck |
|---|---|---|---|
| 1-02 | $r_m=\sqrt{\ln400/2000}$ | 0,054733 | 0,0547 |
| 1-06, 2-07 | $\rho$ dạng chiều VC, $d=3$; $d=11$ ($m=10^4$, $\delta=0{,}05$) | 0,1644303; 0,2799193 | 0,16443; 0,27992 |
| 1-06 | $2\rho$ | 0,32886; 0,55984 | 0,329; 0,560 |
| 2-07 | $2\rho+0{,}01$; ngưỡng $2(\rho_{11}-\rho_3)$ | 0,338861; 0,569839; 0,230978 | 0,3389; 0,5698; 0,2310 |
| 2-08 | $\operatorname{opt}_{S_\eta}(h_t)$; độ lệch lớn nhất; vế phải; giá trị thật | $\tfrac16,0,0,\tfrac16,0,\tfrac16$; 0,18 (tại $h_4$); 0,56667; 0,14 | khớp |
| 2-04 | $S=((1,0),(2,1))$: nghiệm ERM duy nhất $h_2$; $\operatorname{opt}_S(h_3)$; hiệu | $h_2$; $\tfrac12$; $-0{,}10$ | khớp |
| 3-04 | trọng số; $\bar f(x_0)$; $(5/12)^2$; $\sum w_i^2$ | $(\tfrac1{12},\tfrac13,\tfrac7{12})$, $(-\tfrac18,\tfrac34,\tfrac38)$; $\tfrac23,\tfrac23,\tfrac14$; 0,17361; 0,3333, 0,45833, 0,71875 | khớp; tổng 0,5069 / 0,6319 / 0,7188 và 0,2069 / 0,2194 / 0,0719 đúng |
| 3-05 | $(3/4)^2+3/16$; $1+0{,}25$; hiệu | 0,75; 1,25; $0{,}5=2\sigma^2/m$ | khớp |
| 3-06 (ghi chú) | Ví dụ 04.6: $0{,}04+0{,}54$; $0{,}25+0{,}24+0{,}09$; $0{,}81+0{,}09$ | 0,58; 0,58; 0,90 | khớp |
| 3-07 | lỗi tại $\gamma=1;0{,}8;0{,}5;0$; $\gamma^*$; độ chệch | 1,25; 1,20; 1,3125; 2,00; 0,8; $-0{,}2$ | khớp |
| 4-02 | $0{,}05\cdot2^{-k}$ | 0,025; 0,0125; …; tổng 0,05 | khớp |
| 4-04 | $\ln(\pi^2/6)$; $\ln(1/q_3)$; $4\ln13\,591$; $\ln(4/(0{,}05q_3))$; $8(\cdot)/10^4$; $\mathrm{pen}_3$; không chia | 0,49770; 2,69492; 38,0688; 7,07695; 0,0361166; 0,19004; 0,18428 | khớp |
| 4-04 | tỉ số $\mathrm{pen}_k$/không chia, $k=1..10$ | nhỏ nhất 1,0101 ($k=1$), lớn nhất 1,0317 ($k=4$) | 1 %, 3,2 % |
| 4-05 | $\sqrt{\ln40/20}$; $2^{-9}$; $1-(1-2^{-9})^{1000}$; $(\cdot)^{5000}$; $1-(1-2^{-10})^{1000}$; $\sqrt{\ln40\,000/20}$ | 0,42947; 0,001953; 0,85844; 0,999943; 0,62358; 0,72790 | khớp |
| 4-07 | mười $\mathrm{pen}_k$ và tổng | tổng nhỏ nhất **0,365044 tại $k=3$**; các ô khác khớp bảng Phụ lục C đến bốn chữ số | khớp |
| 4-10 | cận $\hat h_3$; ERM trên $\mathcal H_{10}$; biết trước $k=3$; hiệu; tổng $k=4$ trừ $k=3$; $2\mathrm{pen}_2$, $2\mathrm{pen}_{10}$ | 0,365044; 0,434919; 0,359284; 0,005759; 0,013038; 0,33790, 0,57424 | 0,3651; 0,4350; 0,3593; 0,0058; 0,0130; 0,338, 0,574 |
| 4-11 | $\sqrt{\ln80/2000}$ | 0,046808 | 0,04681; 0,0469 |
| 4-12 | $q_k=1/10$: $\ln800$, tổng $k=1..10$; $q_k=2^{-k}$: $b_3$, tổng | 6,6846; 0,4473, 0,3799, **0,3642**, 0,3762, 0,3875, … tăng; 6,4615; 0,4428, 0,3778, **0,3637**, 0,3771, 0,3896, … tăng | khớp |
| 4-12 (ghi chú) | Bài tập 04.4(a): lớp dừng, $\mathrm{pen}_{19}$, số lần gọi | 19; 0,36761; 18 | khớp |
| 5-03 | cỡ mẫu đủ (chia đôi khoảng); tỉ lệ tăng; $1/m$ | 172 279; 181 575; 213 317; 5,40 %; 17,48 %; $4{,}69\cdot10^{-6}$ | khớp |
| 6-03 | cận (a) tại $m_v=200,500,1000,2000,5000$; $2\ln400/\epsilon^2$; $K=10^6$ | 0,24477; 0,15481; 0,10947; 0,07740; 0,04895; **1198,29; 4793,17** (→ 1199; 4794); 0,18711 | khớp |
| 6-04 | $8\sqrt{\ln600/2000}$ | 0,45244 | 0,4524 |
| 6-05 | $2\sqrt{\ln440/2000}$; $2\sqrt{\ln(4\cdot10^6)/2000}$ | 0,11033; 0,17437 | 0,1103; 0,1744 |
| 7-04 | $\ln160$; $8(38{,}069+5{,}075)/10^4$; $\mathrm{pen}_1$, $\mathrm{pen}_2$; hiệu; $2\mathrm{pen}$; hiệu; ngưỡng (b) | 5,07517; 0,034515; 0,18578, 0,26994; 0,08416; 0,37157, 0,53988; 0,16831; 0,16925 | khớp |
| 7-05 (ghi chú) | $0{,}185+0{,}1900$; $\tau$; cận tin cậy | 0,3750; 0,010; 0,37504 | khớp |

**Cận mẫu xác thực.** $2\sqrt{\ln(2K/\delta)/(2m_v)}\le\epsilon\iff m_v\ge2\ln(2K/\delta)/\epsilon^2$: đúng (6-03).

**SVG.** `srm-danh-doi.svg`: trục $y=360-640v$; ba đường (30 điểm) lệch công thức tối đa 0,05 px; nhãn 0,4423, 0,300, 0,1423, 0,4421, 0,2871, 0,155, "k = 3: 0,3650" đúng; ô vuông đặc lớn hơn tại $k=3$ (tín hiệu không chỉ bằng màu). `can-xac-thuc.svg`: trục $x=80+250(\log_{10}m_v-2)$, $y=360-1066{,}7v$; đường cong (150 điểm, $m_v$ từ 150 đến 8002) lệch tối đa 0,1 px; năm chấm và hai giao điểm (x = 349,6 ứng với $m_v\approx1198$; 500,2 ứng với $m_v\approx4795$) đúng; "độ tin cậy 95%" đúng nghĩa $1-\delta$ theo `thuat-ngu.md`. `phan-tich-sai-so.svg`: tỉ lệ 4000 px/đơn vị nhất quán cho 0,18; 0,22; 0,32. Không công thức nào vẽ vào SVG.

## 2. Đối chiếu phát biểu với ghi chú

| Kết quả | Hằng số, dạng | Lượng từ, loại bảo đảm | Giả thiết | Kết luận |
|---|---|---|---|---|
| Mệnh đề 04.3 (2-05, 2-06) | $2r+\operatorname{opt}_S(\tilde h)$, đúng | (a) tất định trên biến cố $r$-đại diện; (b) xác suất $\ge1-\delta$, đồng thời mọi quy tắc | (T2), (T3), $L^*$, quy tắc đo được, $r>0$; (b): (T1),(T4),$r_m$ hoặc 0–1,(T1),(T5),(M),$\rho_m$ — đủ; thiếu "$\delta\in(0,1)$" (phát hiện 10) | khớp |
| Mệnh đề 04.6 (3-02, 3-03) | đẳng thức ba số hạng, đúng | kì vọng theo $(S,Y)$, một điểm, một thuật toán | $S$ bất kì; $\mathbb EY=f^*(x)$, $\operatorname{Var}Y<\infty$, $Y$ độc lập $S$; mô-men bậc hai | khớp; số hạng chéo thiếu độc lập bằng $-2\operatorname{Cov}(\hat f,Y)$ đúng |
| Bổ đề 04.9 (4-02, 4-03) | $\mathrm{pen}_k=\mathrm{rad}_k(m,\delta q_k)$ | xác suất $\ge1-\delta$, đồng thời mọi $k$, mọi $h\in\mathcal H_k$ | (T1), $m\ge1$; (T2),(T3); (T6) với $\mathrm{rad}_k$, $q_k>0$ **chọn trước**, $\sum_kq_k\le1$; $\delta\in(0,1)$ | khớp; bước 2 dùng "chọn trước", bước 3 dùng $\sum q_k\le1$: đúng chỗ |
| Định lý 04.11 (4-08, 4-09) | $2\,\mathrm{pen}_k$, $+\tau$, đúng | xác suất $\ge1-\delta$, đồng thời mọi nghiệm $\tau$-chính xác; (a) và (b) | (T1),(T2),(T3),(T6), SRM dung sai $\tau$ đo được, $\delta\in(0,1)$ | khớp; định nghĩa "mốc có phạt" lệch (phát hiện 3) |
| Hệ quả 04.15 (5-02, 5-03) | $\mathrm{pen}_k(m)=\mathrm{rad}_k(m,q_k/m)$; $M=\max\{\lceil1/\delta\rceil,M_{k(h)}(\epsilon)\}$ | học không đều; (b) ở bước 4 của 5-03 | 0–1, (T1); họ đếm được, $q_k>0$, $\sum q_k\le1$ chọn trước; $\mathcal H_k$ hữu hạn hoặc (M), $d_k<\infty$; **bán kính của Định lý 02.14(a)/03.15(a)**; $A_{\mathrm{SRM}}$ chính xác, đo được; "Kí hiệu:" $M_k$, $k(h)$ | khớp (N1 của cổng duyệt đã áp dụng); bước 4 thiếu tên loại bảo đảm (phát hiện 11) |
| Định lý 04.16(a) (5-04) | — | định tính về lớp; đọc thêm nêu ở ghi chú diễn giả | 0–1, (T1) | khớp |
| Hệ quả 04.17 (6-01, 6-02) | $2\sqrt{\ln(2K/\delta)/(2m_v)}$; $\sqrt{\ln(K/\delta)/(2m_v)}$ | theo $(S,V)$, **mỗi phần** xác suất $\ge1-\delta$ | $S$ bất kì; ứng viên hàm đo được của $S$; (T7); (T2),(T3) | khớp |

**(T6), (T7)** trên 4-02 và 6-01 đúng câu chữ ghi chú §2. **Điểm toán #47:** mặt trang không có khẳng định chung "qua $\ln(1/\delta)+\ln(1/q_k)$". Ghi chú diễn giả 4-02 giới hạn đúng ("Với hai bán kính của Bài 02–03, …"; đúng vì $\ln(2\lvert\mathcal H\rvert/(\delta q_k))$ và $\ln(4\Pi(2m)/(\delta q_k))$ tách được); 4-04 và 4-12 chỉ nói cho dạng chiều VC; 5-03 "giá: $\ln m$ thay $\ln(1/\delta)$" nằm trong Hệ quả 04.15, nơi bán kính đã cố định là của Định lý 02.14(a)/03.15(a). Tuân thủ quyết định 11.6.

**Ý tưởng chứng minh.** 2-06, 3-03, 4-03, 4-09, 5-03, 6-02: các bước đúng, bất đẳng thức then chốt đúng tên (tính đại diện dùng hai lần; Cauchy–Schwarz và độc lập; bất đẳng thức hợp dạng đếm được; cận đồng thời; $\delta=1/m$; lấy điều kiện và Fubini). Giả thiết vào đúng bước. Phản ví dụ 3-05, 4-05, 4-11, 6-05 đúng.

## 3. Bảng thống nhất trang → khối ghi chú

| Trang | Khối ghi chú | Lệch |
|---|---|---|
| 1-01 | đoạn mở đầu, §4, §6, §8 | — |
| 1-02 | Tiên quyết; §2 (T1)–(T5), (M); Định lý 02.14(a), 03.15(a) | thiếu (T2) khi nhắc Định lý 02.14(a) (phát hiện 10) |
| 1-03 | Mục tiêu học tập | mục tiêu 4 thiếu "bất khả diễn" (phát hiện 5) |
| 1-04 | §12 | — |
| 1-05 | câu hỏi trung tâm | — |
| 1-06 | Câu hỏi mở đầu và đoạn sau | ghi chú diễn giả "là $2\rho_m$" (phát hiện 8) |
| 2-00 | §1–§4 | — |
| 2-01 | §1 (thành phần 2, 3, 5; bảng nguồn ngẫu nhiên) | — |
| 2-02 | Ví dụ 04.1; khối ứng dụng; Phụ lục C | "(Bài 03) $d_k=k+1$" (phát hiện 9) |
| 2-03 | Định nghĩa 04.1, đoạn sau; Ví dụ 04.2 | "$D_\eta$ (Ví dụ 01.2)" (phát hiện 9) |
| 2-04 | Định nghĩa 04.2, đoạn sau; Nhận xét 04.4 | — |
| 2-05 | Mệnh đề 04.3 | thiếu $\delta\in(0,1)$ (phát hiện 10) |
| 2-06 | Chứng minh Mệnh đề 04.3 | — |
| 2-07 | Ví dụ 04.3 | làm tròn xuống trong cận trên (phát hiện 6) |
| 2-08 | Bài tập 04.1(b), (c) | — |
| 3-00 | §5 | — |
| 3-01 | Định nghĩa 04.5, hai đoạn sau | — |
| 3-02 | Mệnh đề 04.6, đoạn sau | — |
| 3-03 | Chứng minh Mệnh đề 04.6 | ghi chú diễn giả khái quát hóa (phát hiện 4) |
| 3-04 | Ví dụ 04.4; Phụ lục C | — |
| 3-05 | Ví dụ 04.5 | — |
| 3-06 | Nhận xét 04.7; Ví dụ 04.6 (ghi chú diễn giả) | — |
| 3-07 | Bài tập 04.2(d) (và (b), (c) ở ghi chú diễn giả) | — |
| 4-00 | §6 | — |
| 4-01 | Định nghĩa 04.8 và ba đoạn sau | — |
| 4-02 | (T6); Bổ đề 04.9 | — |
| 4-03 | Chứng minh Bổ đề 04.9 | — |
| 4-04 | Bổ đề 04.9; Ví dụ 04.7; Phụ lục C | — |
| 4-05 | Ví dụ 04.8 | "Bổ đề 04.9 sai" (phát hiện 12) |
| 4-06 | Định nghĩa 04.10 và hai đoạn sau | — |
| 4-07 | Ví dụ 04.9 Bước 1; Thuật toán 04.12 | — (đặt trước Định lý 04.11 theo quyết định T5) |
| 4-08 | Định lý 04.11, đoạn "oracle" | "Mốc có phạt: vế phải của (b)" (phát hiện 3) |
| 4-09 | Chứng minh Định lý 04.11 | — |
| 4-10 | Ví dụ 04.9 Bước 2–5 | cách nói cận trên tin cậy (phát hiện 1) |
| 4-11 | Ví dụ 04.10; Nhận xét 04.13 (ghi chú diễn giả) | — |
| 4-12 | Bài tập 04.4(b) (và (a), (c) ở ghi chú diễn giả) | — |
| 5-00 | §7 | — |
| 5-01 | đoạn mở §7; Định nghĩa 04.14 và hai đoạn sau | bỏ điều kiện bán kính khi nói $\mathrm{pen}_k\to\infty$ (phát hiện 2) |
| 5-02 | Hệ quả 04.15 | — |
| 5-03 | Phụ lục B; đoạn số sau Hệ quả 04.15 | bước 4 thiếu "học PAC bất khả diễn" (phát hiện 11) |
| 5-04 | Ví dụ 04.11; Định lý 04.16 | bỏ cách chọn đo được (phát hiện 13) |
| 6-00 | §8 đoạn mở | "tăng theo lôgarit" (phát hiện 14) |
| 6-01 | (T7); định nghĩa $L_V$; Hệ quả 04.17 | thiếu $\delta\in(0,1)$ (phát hiện 10) |
| 6-02 | Chứng minh Hệ quả 04.17; Hệ quả 02.16(a), Định lý 02.14(b) | nhắc lại 02.14(b) thiếu "đồng thời" (phát hiện 15) |
| 6-03 | Ví dụ 04.12 | — |
| 6-04 | Nhận xét 04.18, đoạn sau | — |
| 6-05 | Bài tập 04.5(a) (và (b), (c) ở ghi chú diễn giả) | — |
| 7-00 | §9 | — |
| 7-01 | §4–§9 | hàng Hệ quả 04.17 không có cận (phát hiện 16) |
| 7-02 | §9 | cận tin cậy (phát hiện 1); dòng 1 thiếu điều kiện (phát hiện 17) |
| 7-03 | Bài tập 04.7(a), (c) | — |
| 7-04 | Bài tập 04.7(c) | — |
| 7-05 | §11 và lời giải; Nhận xét 04.7; Bổ đề 04.9; Ví dụ 04.8 | — |
| 7-06 | §10 | bảng `Mục | Bài tập` đủ 13 bài, mỗi bài ở mạch kiến thức cuối cùng nó cần: khớp |
| 7-07 | §11, §12 | — |

Kí hiệu ($L^*$, $\operatorname{opt}_S$, $\mathrm{rad}_k$, $\mathrm{pen}_k$, $q_k$, $\hat h_k$, $(\hat k,\hat h)$, $k(h)$, $M_k(\epsilon)$, $A_{\mathrm{SRM}}$, $V$, $m_v$, $L_V$, $g_j$, $\hat g$, $\mathcal R_2$, $\mathcal R_5$), số hiệu khối và nhãn giả thiết thống nhất với ghi chú; bốn trang bài tập khớp `exercises.md` về dữ liệu, câu hỏi và kết quả.

## 4. Phát hiện

| # | mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|---|
| 1 | trung bình | 4-10, 7-02 | Cận trên tin cậy viết như một xác suất về con số đã quan sát. Ghi chú nói rõ đây là thủ tục đúng với xác suất $0{,}95$ theo $S$ (Nhận xét 01.19); mặt trang đặt "xác suất $\ge0{,}95$" trước $L_D(\hat h_3)\le0{,}3651$, nơi cả $\hat h_3$ và $0{,}3651$ đã phụ thuộc $S$. | 4-10: "Định lý 04.11(a), xác suất $\ge0{,}95$: $L_D(\hat h_3)\le0{,}3651$."; 7-02: "SRM chọn ba, $L_D\le0{,}3651$, xác suất $\ge0{,}95$". Ghi chú Ví dụ 04.9 Bước 2: "$0{,}3651$ là một cận trên tin cậy ở mức $95\%$ cho $L_D(\hat h_3)$ …: thủ tục tính cận này đúng với xác suất ít nhất $0{,}95$ theo $S$". | 4-10: "Định lý 04.11(a): $0{,}3651$ là cận trên tin cậy mức $95\%$ cho $L_D(\hat h_3)$." 7-02: "SRM chọn ba, cận trên tin cậy mức $95\%$: $0{,}3651$ (mười: $0{,}4350$)." |
| 2 | trung bình | 5-01 | Bỏ điều kiện của khẳng định $\mathrm{pen}_k\to\infty$. Với bán kính tổng quát điều này sai: $\mathrm{rad}\equiv1$ luôn là bán kính, và dạng chiều VC cắt ở $1$ không tiến ra vô cùng (Phụ lục A Bước 4). Cũng không có "cỡ mẫu trong Định lý 04.11(b)". | 5-01: "Danh sách vô hạn: $\mathrm{pen}_k\to\infty$, nên cỡ mẫu trong Định lý 04.11(b) phụ thuộc lớp chứa $h$." Ghi chú §7: "Với bán kính của Định lý 02.14(a) hoặc 03.15(a) và một danh sách vô hạn, $\mathrm{pen}_k\to\infty$, nên cỡ mẫu để cận của hiệu này nhỏ hơn $\epsilon$ phụ thuộc lớp chứa $h$". | "Bán kính của Định lý 02.14(a), 03.15(a), danh sách vô hạn: $\mathrm{pen}_k\to\infty$, nên cỡ mẫu để $2\,\mathrm{pen}_k\le\epsilon$ phụ thuộc lớp chứa $h$." |
| 3 | trung bình | 4-08 | "Mốc có phạt" định nghĩa lệch ghi chú: ghi chú gọi cận dưới đúng $\inf_k[\cdot]$ là mốc, không gồm $+\tau$. 7-01 lại viết đúng "$\le$ mốc có phạt $+\tau$", nên deck tự mâu thuẫn. | 4-08: "Mốc có phạt (penalized benchmark): vế phải của (b)." Ghi chú sau Định lý 04.11: "Phần (b) chặn rủi ro so với một *mốc có phạt* (penalized benchmark), tức cận dưới đúng ở vế phải". 7-01: "$L_D(\hat h)\le$ mốc có phạt $+\tau$". | "Mốc có phạt (penalized benchmark): $\inf_k\big[\inf_{h\in\mathcal H_k}L_D(h)+2\,\mathrm{pen}_k\big]$." |
| 4 | trung bình | 3-03 (ghi chú diễn giả) | Khái quát hóa không có cơ sở: tương quan dương giữa $\hat f$ và một nhãn huấn luyện chỉ đúng cho ví dụ $\hat f=\bar Y$. Một thuật toán bất kì có thể cho hiệp phương sai âm. | "Khi nhãn kiểm tra nằm trong tập huấn luyện, $\hat f$ và $Y$ tương quan dương, số hạng chéo âm, và lỗi đo được nhỏ hơn lỗi trên nhãn mới." Ghi chú Ví dụ 04.5 chỉ tính cho $\hat f=\bar Y$: "$-2\operatorname{Cov}(\bar Y,Y_1)=-2\sigma^2/m$". | "Khi nhãn kiểm tra nằm trong tập huấn luyện, số hạng chéo bằng $-2\operatorname{Cov}(\hat f,Y)$; với $\hat f=\bar Y$, nó bằng $-2\sigma^2/m<0$, nên lỗi đo được nhỏ hơn lỗi trên nhãn mới." |
| 5 | trung bình | 1-03 | Mục tiêu 4 thiếu "bất khả diễn", trái mục tiêu 4 của ghi chú và quyết định 11.5 của điều phối viên ("giữ vế 'so với học PAC bất khả diễn'"). Ghi chú diễn giả có, mặt trang không. | 1-03: "Định nghĩa học không đều, so với học PAC; nêu lớp học được không đều, không học được PAC." Ghi chú: "so sánh với học PAC bất khả diễn (agnostic PAC learning)". | "Định nghĩa học không đều, so với học PAC bất khả diễn; nêu lớp học được không đều, không học được PAC." |
| 6 | nhẹ | 2-07 | Hai số làm tròn xuống trong một cận trên: $\rho_m\le0{,}1644303$ viết "$\le0{,}16443$"; $a_{10}+0{,}569839$ viết "$\le a_{10}+0{,}5698$". Ghi chú dùng "$\approx$". | 2-07: "$\rho_m\le0{,}16443$ ($d=3$)"; "$L_D(\tilde h_{10})-L_D^{\mathrm{Bayes}}\le a_{10}+0{,}5698$". Ghi chú Ví dụ 04.3: "$\approx a_{10}+0{,}5698$". | Dùng "$\approx$" như ghi chú, hoặc làm tròn lên: $0{,}16444$, $a_{10}+0{,}5699$. |
| 7 | nhẹ | 4-10 (ghi chú diễn giả) | $0{,}43492$ viết "$\approx0{,}4350$". Ghi chú nói "làm tròn lên". | "$0{,}155+0{,}27992\approx0{,}4350$". Ghi chú Bước 3: "$=0{,}43492$, làm tròn lên $0{,}4350$". | "$0{,}155+0{,}27992=0{,}43492$, làm tròn lên $0{,}4350$". |
| 8 | nhẹ | 1-06 (ghi chú diễn giả) | $0{,}329$, $0{,}560$ là hai lần vế phải của Định lý 03.15(b), một cận trên của $\rho_m$, không phải $2\rho_m$. | "$0{,}329$ và $0{,}560$ là $2\rho_m$ với chiều VC $3$ và $11$". | "… là hai lần vế phải của Định lý 03.15(b) với chiều VC $3$ và $11$, …". |
| 9 | nhẹ | 2-02, 2-03 | Hai chỗ dẫn lệch nguồn. $d_k=k+1$ được chứng minh ở Bài 04 (khối ứng dụng, Phụ lục C) từ Mệnh đề 03.9. $D_\eta$ được định nghĩa ở Ví dụ 01.1; Ví dụ 01.2 cho các rủi ro. | 2-02: "chiều VC (Bài 03) $d_k=k+1$"; 2-03: "$D_\eta$ (Ví dụ 01.2)". Ghi chú Ví dụ 04.2: "Phân bố $D_\eta$ của Ví dụ 01.1"; khối ứng dụng: "theo Mệnh đề 03.9 qua phép chiếu". | 2-02: "chiều VC $d_k=k+1$ (Mệnh đề 03.9, phép chiếu)"; 2-03: "$D_\eta$ (Ví dụ 01.1, 01.2)". |
| 10 | nhẹ | 1-02, 2-05, 6-01, 6-02 | Thiếu một điều kiện nhỏ khi nhắc lại hoặc phát biểu rút gọn: (T2) cho Định lý 02.14 (1-02, 6-02 viết "(T1), (T3), (T4)"); $\delta\in(0,1)$ cho Mệnh đề 04.3(b) và Hệ quả 04.17. | Định lý 02.14 (Bài 02): "Hàm lỗi. $\ell$ thỏa (T2) và (T3)"; Hệ quả 04.17: "Tham số. $\delta\in(0,1)$". | 1-02, 6-02: "(T1)–(T4)"; 2-05 (b), 6-01: thêm "$\delta\in(0,1)$". |
| 11 | nhẹ | 5-03 | Bước 4 (phần (b) của Hệ quả 04.15) nêu hàm cỡ mẫu nhưng không nêu loại bảo đảm. | "Phần (b), $k_{\max}$ lớp: $M(\epsilon,\delta)=\max\{\ldots\}$, lấy $\inf_h$." Ghi chú: "$A_{\mathrm{SRM}}$ là thuật toán học PAC bất khả diễn cho $\mathcal H$ với …". | "Phần (b), $k_{\max}$ lớp: lấy $\inf_h$, $A_{\mathrm{SRM}}$ học PAC bất khả diễn với $M(\epsilon,\delta)=\ldots$". |
| 12 | nhẹ | 4-05 | Bổ đề không "sai": kết luận của nó sai khi bỏ một giả thiết. | "Bổ đề 04.9 sai với xác suất …". Ghi chú Ví dụ 04.8 Bước 3: "kết luận của Bổ đề 04.9 sai với xác suất". | "kết luận của Bổ đề 04.9 sai với xác suất …". |
| 13 | nhẹ | 5-04 | Hệ quả 04.15 đòi $A_{\mathrm{SRM}}$ đo được; ghi chú chọn chỉ số nhỏ nhất để có điều này. Deck bỏ ở cả mặt trang và ghi chú diễn giả. | Ghi chú Ví dụ 04.11 Bước 3: "chọn chỉ số $j$ nhỏ nhất trong các nghiệm cho một $A_{\mathrm{SRM}}$ đo được". | Thêm vào ghi chú diễn giả: "Chọn chỉ số $j$ nhỏ nhất trong các nghiệm cho một $A_{\mathrm{SRM}}$ đo được." |
| 14 | nhẹ | 6-00 (dòng dẫn), 1-01 (ghi chú diễn giả) | Cận tăng theo $\sqrt{\ln K}$, không theo $\ln K$. | 6-00: "cho cận tăng theo lôgarit của số ứng viên"; 1-01: "với giá theo lôgarit của số ứng viên". Ghi chú: "tốn một lượng tỉ lệ với $\sqrt{\ln K/m_v}$". | "cho cận tăng theo căn bậc hai của lôgarit số ứng viên" (hoặc "… $K$ chỉ vào qua $\ln K$"). |
| 15 | nhẹ | 6-02 | Nhắc lại Định lý 02.14(b) thiếu "đồng thời cho mọi $h\in\mathcal H$", điều mà bước 2 cần vì $\hat g$ chọn theo $V$. | "$L_D(h)\le L_S(h)+\sqrt{\ln(K/\delta)/(2m)}$ (Định lý 02.14(b))". Bài 02: "đồng thời cho mọi $h\in\mathcal H$". | "… $\le L_S(h)+\sqrt{\ln(K/\delta)/(2m)}$ mọi $h$ đồng thời (Định lý 02.14(b))". |
| 16 | nhẹ | 7-01 | Hàng Hệ quả 04.17 nêu đại lượng mà không nêu cận; các hàng khác có cận. | "Hệ quả 04.17: $L_D(\hat g)-\min_jL_D(g_j)$". | "Hệ quả 04.17: $L_D(\hat g)-\min_jL_D(g_j)\le2\sqrt{\ln(2K/\delta)/(2m_v)}$". |
| 17 | nhẹ | 7-02 | Dòng 1 bỏ "với cùng $L^*$" và "lớp lồng nhau". | "Sai số xấp xỉ không tăng theo lớp". Ghi chú §4: "Với cùng $L^*$, sai số xấp xỉ giảm hoặc giữ nguyên khi lớp lớn hơn". | "Cùng $L^*$, lớp lồng nhau: sai số xấp xỉ không tăng; …". |
| 18 | nhẹ | 4-08 (ghi chú diễn giả) | "vẫn đạt mốc này" có thể đọc là bằng mốc. Định lý cho $L_D(\hat h)\le$ mốc $+\tau$. | "… và trên biến cố có xác suất ít nhất $1-\delta$ vẫn đạt mốc này." | "… có rủi ro kì vọng không quá mốc này cộng $\tau$." |

## 5. Đề xuất sửa ghi chú

Deck vẫn theo ghi chú. Các điểm sau để điều phối viên ghi cho tác giả:

1. **Điểm toán #47 (đang chờ tác giả).** Không đổi; deck tuân thủ (mục 2).
2. **Ví dụ 04.5, câu "Tóm lại".** "lỗi trên một nhãn đã dùng để huấn luyện thấp hơn lỗi trên một nhãn mới" đọc như một khẳng định chung, nhưng ví dụ chỉ tính cho $\hat f=\bar Y$. Đề xuất: "Tóm lại, với $\hat f=\bar Y$, lỗi trên một nhãn đã dùng để huấn luyện thấp hơn lỗi trên một nhãn mới $2\sigma^2/m$." (Nguồn của phát hiện 4.) Mức nhẹ.
3. **Đoạn sau Định lý 04.11.** Định nghĩa "mốc có phạt … tức cận dưới đúng ở vế phải", nhưng câu "oracle" ngay sau viết "vế phải của (b) là giá trị mà một người biết $D$ … có thể dùng", tức gồm cả $+\tau$. Đề xuất: "cận dưới đúng ở vế phải của (b) là giá trị …". (Nguồn của phát hiện 3.) Mức nhẹ.

## 6. Kết luận

0 chặn bàn giao, 0 nghiêm trọng, 5 trung bình (1–5), 13 nhẹ (6–18). Mọi con số, ba SVG và mọi chứng minh trên deck đều đúng; sáu kết quả chính giữ đủ hằng số, lượng từ, loại bảo đảm và giả thiết của ghi chú, kể cả $q_k$ chọn trước, $\sum q_k\le1$, bán kính của Định lý 02.14(a)/03.15(a) trong Hệ quả 04.15, (T6), (T7). Các lỗi còn lại là cách nói cận trên tin cậy, một điều kiện bị bỏ khi nói $\mathrm{pen}_k\to\infty$, định nghĩa "mốc có phạt" và một khái quát hóa trong ghi chú diễn giả.

**Kết luận: đạt khi sửa.**
