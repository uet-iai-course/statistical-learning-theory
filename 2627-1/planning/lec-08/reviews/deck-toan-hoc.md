# Duyệt bộ trang chiếu Bài 08 — Vai 2 `toan-hoc` (độ chính xác toán học, thống nhất với ghi chú)

Bản duyệt: `2627-1/lecture-08-on-dinh-sgd-hoc-sau.html` (đóng băng, 55 trang), `img/lec-08/*.svg` (4 hình). Đối chiếu: `materials/lec-08/lecture-note.md`, `exercises.md`, Bài 06 (Định nghĩa 06.9, Định lý 06.10, Mệnh đề 06.5, Nhận xét 06.3), Bài 05 (Bài tập 05.8). Đã đọc toàn bộ mặt trang, ghi chú diễn giả và mã SVG. `deck_lint.py`: 0 phát hiện.

## 1. Tính lại độc lập

Kịch bản: `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-08/rv-toan-hoc/check.py`, `svg.py` (số hữu tỉ chính xác bằng `fractions`, liệt kê đủ $4^T$ dãy).

| Đại lượng (trang) | Tính lại | Kết quả |
|---|---|---|
| Ví dụ 08.1, $w_2,\ldots,w_7$ (2-03 ghi chú) | $0;\tfrac12;\tfrac34;\tfrac54;\tfrac74;\tfrac54$ | khớp |
| Ví dụ 08.2, $w'_t$, đạo hàm, $\Delta$ (2-06, F1) | $w'$: $0;0;-\tfrac12;0;\tfrac12;0;0$; đạo hàm $0;1;-1;-1;1;0$; $\Delta_2..\Delta_7=0;1;\tfrac34;\tfrac34;\tfrac74;\tfrac54$ | khớp |
| Một bước, hai kì vọng, ghép cặp, độc lập (2-05) | $\tfrac38-\tfrac18=\tfrac14$; ghép cặp $\tfrac14$; độc lập $7/6/3$ cặp, $\tfrac38$ | khớp |
| Ví dụ 08.3, bảng hệ số giãn (2-10) | $\lvert1-\eta\rvert$, $\max\{\lvert1-\eta\rvert,1\}$, $1+\eta$ tại $\tfrac12,2,3$ | khớp |
| Bài tập 08.3(a), $\eta=3$, $u=\pm0{,}2$ (2-11) | $\Gamma(w)=-2w$, hiệu $0{,}8=2\cdot0{,}4$ | khớp |
| Ví dụ 08.4 (3-03) | $\mathbb E\Delta_2=\tfrac14$, $\mathbb E\Delta_3=\tfrac{29}{64}$, $\mathbb E\Delta_7=\tfrac{228203}{262144}\approx0{,}87053$; dãy $(2,3,1,4,4,4)$: $w_7=2$, $w'_7=-1$ | khớp |
| Bài tập 08.1(c), $\eta=1$ (3-04) | $\mathbb E\Delta_2=\tfrac12$, $\mathbb E\Delta_3=\tfrac{13}{16}$; hụt $(4,1)$: 2, $(4,2)$: 1 | khớp |
| Hằng số $2G$ không giảm được (3-01 ghi chú) | $1\pm\tfrac12$, cách nhau $1=2G\eta$ | khớp |
| Ví dụ 08.5 (4-03) | $0{,}001$; $t/200$ | khớp |
| Đoạn sau Hệ quả 08.7 (4-05 ghi chú) | $16\cdot0{,}00625\cdot1599/4=39{,}975$ | khớp |
| Bài tập 08.7 (4-07) | cận $0{,}25;4;39{,}975$; $q^T=0{,}87078;0{,}13197;1{,}82\cdot10^{-9}$; $\psi=0{,}03011;0{,}28434;0{,}47500$; ngưỡng $T\le161$, $T\le80$ | khớp |
| Ví dụ 08.7 (5-03, F4) | $5/\sqrt{10001}=0{,}049998$; $\eta^*=0{,}028868$; cận $0{,}086600;0{,}079055;0{,}072457$; giới hạn $0{,}070711$; $T^*=7071{,}07$, $B(T^*)=0{,}095706$; $B(5000)=B(10^4)=0{,}099995$, $B(2\cdot10^4)=0{,}137495$, $B(5\cdot10^4)=0{,}279995$ | khớp |
| Bài tập 08.8 (5-05) | $T^*=3535{,}53$, $B=0{,}120701$; $T^*=17677{,}67$, $B=0{,}080709$ | khớp |
| Ví dụ 08.8 (6-01, F3) | $\Delta_2=0{,}00099998$, $\Delta_3/\Delta_2=1{,}1000$, $\Delta_{21}=0{,}0061$, $\Delta_{41}=0{,}0411$, $\Delta_{57}=0{,}1886$, $\Delta_{58}=0{,}20732$, $\Delta_{61}=0{,}2753$, $\Delta_{81}=1{,}529$, $\Delta_{101}=2{,}879$; chỉ số đầu vượt $0{,}2$ là $58$ | khớp |
| Bài tập 08.3(d) (6-07) | $\ln(0{,}5/\Delta_2)=6{,}21462$, $/\ln1{,}1=65{,}20$ nên $\tau\ge68$; $1{,}0877583^{74}\Delta_2=0{,}5051$ nên $\tau\le76$; mô phỏng $\tau=68$ | khớp |
| Đoạn sau Mệnh đề 08.10 (6-03) | $1{,}1^{100}=13780{,}6$; $\tfrac2{100}(1{,}1^{100}-1)=275{,}59$ | khớp |
| Nhận xét 08.11 (6-03 ghi chú) | $33{,}369\le33{,}37$ | khớp |
| Mệnh đề 08.12, hồi quy logistic (6-04 ghi chú) | $2\ln2/500+0{,}0125=0{,}015273\le0{,}0153$ | khớp |
| Ví dụ 08.9 (6-05) | $\eta=1$: $0{,}02\to0$; $\eta=2$: $0{,}04$ không đổi; $\eta=3$: $0{,}06\cdot2^k$ đến $3{,}84$ tại $\Delta_8$, $\lvert w_7\rvert=0{,}96\le1$ | khớp |
| Ví dụ 08.10 (6-06) | $\lvert w\rvert$: $0{,}02\to0{,}98$; bản lề: $0{,}99\mapsto1{,}49$, $1{,}01$ giữ nguyên, $0{,}48$ | khớp |
| Bài tập 08.5 (7-04 đến 7-06) | $0{,}4$; $0{,}4G^2$, $G=1{,}5$: $0{,}9$; $10/(1+e)=2{,}689$; $\log_{10}1{,}1^{10^5}=4139{,}3$ | khớp |
| Câu hỏi tự kiểm tra 3 (7-07) | $0{,}8$; ngân sách $28{,}184\le28{,}19$; cận $0{,}011274\le0{,}0113$ | khớp |
| Câu ôn nhanh (1-02 ghi chú) | $1-(3/4)^6=3367/4096=0{,}82202$ | khớp |

**SVG.** F1 `hai-lan-chay-huber.svg`: thang $106{,}67$ px/đơn vị, mọi điểm của hai quỹ đạo đúng vị trí, hai dải bước khác biệt từ $t=2$ đến $3$ và $5$ đến $6$, ba mũi tên $1$, $\tfrac74$, $\tfrac54$ đúng điểm đầu cuối. F2 `thi-nghiem-ghep-cap.svg`: trục lôgarit hai chiều ($217{,}3$ px/thập phân ngang, $79{,}07$ dọc), 15 điểm của ba đường (cận, $\Delta$ ghép cặp, khoảng cách) đúng đến $0{,}1$ px. F3 `ham-loi-cosin.svg`: $100$ điểm đúng quỹ đạo mô phỏng; đường $0{,}2$ và $\pi$ đúng; điểm đánh dấu $\Delta_{58}$ tại $(405{,}5;116{,}8)$ đúng. F4 `danh-doi-so-buoc.svg`: ba đường $201$ điểm, sai số lớn nhất $1{,}3\cdot10^{-4}$ (làm tròn tọa độ); đáy tại $T^*=7071$, $0{,}0957$; hai đầu mút $0{,}28$. Văn bản `desc` và `alt` của bốn hình khớp dữ liệu. Không công thức nào vẽ vào SVG.

## 2. Đánh giá điều kiện "trọng số ra tương ứng khác 0" bỏ khỏi trang 6-06

Không chấp nhận bỏ. Với điều kiện đó, câu của ghi chú là một khẳng định đúng tại từng điểm. Bỏ điều kiện, câu trên trang ("không trơn tại tiền kích hoạt bằng $0$") khẳng định không khả vi tại mọi tham số có một tiền kích hoạt bằng $0$, và khẳng định này sai: nếu nơ-ron $j$ có tiền kích hoạt $a_j=0$ và trọng số ra $v_j=0$, số hạng $v_j\operatorname{ReLU}(a_j)$ thỏa $\lvert v\operatorname{ReLU}(a)\rvert\le\lvert v\rvert\lvert a\rvert=o(\lVert(a,v)\rVert)$, nên khả vi tại đó với đạo hàm $0$, và hàm lỗi khả vi theo các tọa độ này. Kết luận "không $\beta$-trơn" vẫn đúng, nhưng phát biểu trên trang mất một điều kiện. Xem phát hiện 1 (có hai cách sửa, cách thứ hai ngắn hơn và không vượt trần mật độ).

## 3. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L08-6-06 | 1. Bỏ điều kiện "trọng số ra tương ứng khác 0": khẳng định không khả vi tại mọi tham số có tiền kích hoạt bằng 0 là sai (mục 2). "Không trơn tại một điểm" còn trộn tính chất toàn cục (β-trơn) với tính chất tại điểm. | Trang: "không trơn tại tiền kích hoạt (pre-activation) bằng $0$; không lồi". Ghi chú Ví dụ 08.10, Bước 3: "không khả vi theo $\theta$ tại các tham số có một tiền kích hoạt … bằng $0$ và trọng số ra tương ứng khác $0$; do đó nó không $\beta$-trơn". | "không khả vi tại tham số có tiền kích hoạt (pre-activation) bằng $0$, trọng số ra khác $0$, nên không $\beta$-trơn; không lồi", hoặc ngắn hơn: "không khả vi tại một số tham số có tiền kích hoạt (pre-activation) bằng $0$, nên không $\beta$-trơn; không lồi". |
| trung bình | L08-6-06 | 2. Bỏ điều kiện "khi trọng số không bị chặn" của cận gradient. Trên một $W$ lồi, bị chặn có (G) với một $G$ hữu hạn (Bài tập 08.5(d)(ii), Bước 2), nên câu trên trang nói quá ghi chú. | Trang: "không có $G$ đều: gradient theo $\Theta_1$ (lớp ẩn) tỉ lệ với $\Theta_2$ (lớp ra)". Ghi chú: "nên không có $G$ đều trên toàn không gian tham số khi trọng số không bị chặn". | "không có $G$ đều trên toàn không gian tham số: gradient theo $\Theta_1$ (lớp ẩn) tỉ lệ với $\Theta_2$ (lớp ra)". |
| trung bình | L08-5-00 (dòng dẫn), L08-1-05 (ghi chú diễn giả) | 3. "Tổng hai cận nhỏ nhất ở một số bước hữu hạn" chỉ đúng khi độ dài bước cố định. Với $\eta=\eta^*(T)$ của Hệ quả 08.8(b), cận giảm theo $T$ khi $m>2$ và tiến về $RG\sqrt{2/m}$ khi $T\to\infty$, như chính trang 5-01 ghi; hai câu mâu thuẫn nhau nếu đọc không có điều kiện. | 5-00: "Chạy thêm bước làm cận tối ưu giảm và cận ổn định tăng, nên tổng hai cận nhỏ nhất ở một số bước hữu hạn." Ghi chú Hệ quả 08.8(b): "giảm theo $T$ khi $m>2$"; Ví dụ 08.7 Bước 3 chỉ có $T^*$ với $\eta=0{,}05$ cố định. | 5-00: "Với độ dài bước cố định, chạy thêm bước làm cận tối ưu giảm và cận ổn định tăng, nên tổng hai cận nhỏ nhất ở một số bước hữu hạn." 1-05 ghi chú: thêm "với độ dài bước cố định". |
| trung bình | L08-5-04 | 4. Định nghĩa 08.9, thành phần chính quy hóa ngầm, mất điều kiện "nhiều điểm của $W$ có rủi ro thực nghiệm nhỏ như nhau" và "không qua một số hạng phạt". Không có hai điều kiện này, dòng thứ ba không phân biệt được với hai dòng trên (dừng sớm và chính quy hóa tường minh cũng là quá trình huấn luyện chọn nghiệm). Điều kiện chỉ có ở ghi chú diễn giả. | Trang: "chính quy hóa ngầm (implicit regularization): quá trình huấn luyện tự chọn nghiệm." Ghi chú: "xảy ra khi nhiều điểm của $W$ có rủi ro thực nghiệm nhỏ như nhau và các lựa chọn của quá trình huấn luyện … quyết định điểm được trả về, không qua một số hạng phạt". | "chính quy hóa ngầm (implicit regularization): nhiều điểm có $L_s$ nhỏ như nhau, khởi tạo, độ dài bước, số bước chọn điểm trả về, không có số hạng phạt." |
| nhẹ | L08-1-05 (ghi chú diễn giả) | 5. "Với điểm lặp trung bình, hệ số nhỏ hơn một nửa" thiếu "khi độ dài bước hằng". Với độ dài bước thay đổi, câu này sai: $\eta_1=1$, các $\eta_t=\varepsilon$ còn lại cho tỉ số hai hệ số $\to(T-1)/T$. | Ghi chú Hệ quả 08.7 và §10: "$G^2\eta(T-1)/m$, nhỏ hơn nửa hệ số $2G^2\eta T/m$" (bước hằng). Trang 4-05, 7-02 đều ghi "bước hằng". | "Với điểm lặp trung bình và độ dài bước hằng, hệ số nhỏ hơn một nửa." |
| nhẹ | L08-5-01 | 6. Điều kiện $\eta^*\le2/\beta$ viết như một khẳng định ("$\eta^*=\ldots\le2/\beta$: vế phải …"), không như giả thiết "Nếu" của ghi chú; vế phải tại $\eta^*$ cũng không nói rõ là tại $\eta=\eta^*$. | Trang: "(b) $\eta^*=R/\big(G\sqrt{T+2T(T-1)/m}\big)\le2/\beta$: vế phải $\le RG\sqrt{3/m}$ khi $T=m$ …". Ghi chú: "Nếu $\eta^*\le2/\beta$, vế phải của (a) tại $\eta=\eta^*$ bằng …". | "(b) nếu $\eta^*=R/\big(G\sqrt{T+2T(T-1)/m}\big)\le2/\beta$ thì vế phải tại $\eta^*$ $\le RG\sqrt{3/m}$ khi $T=m$, $\to RG\sqrt{2/m}$ khi $T\to\infty$." |
| nhẹ | L08-4-00 (dòng dẫn) | 7. Thiếu (G) và điều kiện độ dài bước; "tăng không nhanh hơn" là phát biểu về tốc độ, còn định lý cho một cận trên trị tuyệt đối với hằng số $2G^2$. Dòng dẫn 7-00 có "có gradient bị chặn". | Trang: "Với hàm lỗi lồi, trơn, khoảng cách tổng quát hóa kì vọng tăng không nhanh hơn ngân sách độ dài bước chia cho cỡ mẫu." Định lý 08.6(c). | "Với hàm lỗi lồi, trơn, có gradient bị chặn và bước đủ ngắn, khoảng cách tổng quát hóa kì vọng không vượt một hằng số nhân ngân sách độ dài bước chia cho cỡ mẫu." |
| nhẹ | L08-4-03 (ghi chú diễn giả) | 8. "Đạo hàm theo điểm số nằm trong $(-1,0)$" sai khi $\tilde y=-1$: đạo hàm theo điểm số $\langle w,x\rangle$ là $\tilde y f'(\tilde y\langle w,x\rangle)\in(-1,1)$; khoảng $(-1,0)$ là của $f'(s)$ với $s=\tilde y\langle w,x\rangle$. | Bài tập 05.8, Lời giải Bước 1: "$f'(s)=-1/(1+e^s)\in(-1,0)$", $\ell(w)=f(\tilde y\langle w,x\rangle)$. Trang 7-05 ghi chú viết đúng "$x$ nhân một số trong $(-1,1)$". | "đạo hàm theo lề $\tilde y\langle w,x\rangle$ nằm trong $(-1,0)$". |
| nhẹ | L08-4-04 (ghi chú diễn giả) | 9. "Với dãy chỉ số độc lập, khoảng cách giữa hai lần chạy là $2{,}99$": theo Phụ lục F, đây là lần chạy thứ ba trên cùng $S$ với dãy chỉ số độc lập, không phải lần chạy trên mẫu lân cận; câu dễ đọc thành $\Delta$ không ghép cặp giữa $s$ và $s^{(i)}$. | Ghi chú Phụ lục F: "Lần thứ ba trên $S$ với một dãy chỉ số độc lập (không ghép cặp)"; "$\Delta$ giữa lần chạy thứ nhất và lần chạy thứ ba … là $2{,}99$ … ở $0{,}5$ … vòng". | "Hai lần chạy trên cùng $S$ với hai dãy chỉ số độc lập cách nhau $2{,}99$ ở nửa vòng: …". |
| nhẹ | L08-6-06 | 10. "Kết luận:" bỏ hai điều kiện của ghi chú: hàm lỗi logistic huấn luyện bằng SGD, và $G=\sup_x\lVert\chi(x)\rVert$ hữu hạn (cần cho (G)). | Trang: "Định lý 08.6 áp dụng khi lớp ẩn cố định, chỉ lớp ra được huấn luyện." Ghi chú Ví dụ 08.10: "… trên hàm lỗi logistic, như mạng của Ví dụ 07.3 … $G=\sup_x\lVert\chi(x)\rVert$ (hữu hạn với …)". | "… khi lớp ẩn cố định như Ví dụ 07.3, chỉ lớp ra được huấn luyện; $G=\sup_x\lVert\chi(x)\rVert$." |
| nhẹ | L08-6-04 | 11. Kí hiệu $g_t$ đổi nghĩa (gradient ngẫu nhiên không chệch của $F$) so với 3-02 ($g_t=\nabla\ell(w_t,z_i)$); trang không gọi tên $g_t$, chỉ ghi chú diễn giả nói. Ghi chú bài giảng có cùng vấn đề (đã ghi trong `review-log.md`). | Trang 3-02: "$g_t=\nabla\ell(w_t,z_i)$"; 6-04: "$\mathbb E[g_t\mid\mathcal F_{t-1}]=\nabla F(w_t)$". | Thêm "gradient ngẫu nhiên $g_t$:" trước điều kiện không chệch. |
| nhẹ | L08-4-07 | 12. Dữ liệu Bài tập 08.7 thiếu $w_1=0$; $\psi(T)$ và cận đều dựa trên khởi tạo này. | `exercises.md`, Bài tập 08.7: "$W=[-1,1]$, $w_1=0$, $m=4$". | Thêm "$w_1=0$". |
| nhẹ | L08-7-03 | 13. Dòng "Không lồi: cận tăng theo hàm mũ của ngân sách độ dài bước" không nói cận của đại lượng nào và dưới giả thiết nào. | Ghi chú §10: "Mệnh đề 08.10 (tăng theo hàm mũ với độ dài bước hằng)"; Mệnh đề 08.10(c) chặn $\mathbb E\Delta_{T+1}$ dưới (S′), (G). | "Bỏ tính lồi ((S′), (G)): cận của $\mathbb E\Delta_{T+1}$ tăng theo hàm mũ của ngân sách độ dài bước." |
| nhẹ | L08-2-02 | 14. (T3) thiếu lượng từ theo $w$; ghi chú đòi $[0,1]$ với mọi $w\in\mathbb R^p$, không chỉ $w\in W$ (dòng đầu chỉ có "Với mọi $z\in\mathcal Z$"). Ghi chú diễn giả có lượng từ. | Ghi chú §2: "(T3) … $\ell(w,z)\in[0,1]$ với mọi $w\in\mathbb R^p$ và mọi $z\in\mathcal Z$." | "(T3) $\ell(w,z)\in[0,1]$ với mọi $w\in\mathbb R^p$". |
| nhẹ | L08-2-07 | 15. "vế trái $-(u-v)^2<0$" thiếu "khi $u\ne v$". | Ghi chú §5: "vế trái bằng $-(u-v)^2<0$ khi $u\ne v$". | Thêm "khi $u\ne v$". |
| nhẹ | L08-1-02 | 16. Nhắc lại Định nghĩa 06.9 bỏ điều kiện "các kì vọng sau hữu hạn". | Bài 06, Định nghĩa 06.9: "Với mọi $s$, $i$, $z'$ và $z$, các kì vọng sau hữu hạn và …". | "$A$ ổn định đều: với mọi $s,i,z'$, mọi quan sát kiểm tra $z$, hai kì vọng hữu hạn và". |
| nhẹ | L08-2-09 (ghi chú diễn giả) | 17. "Phần (a) chứng minh ở Phụ lục A theo bốn dòng": Phụ lục A có bốn bước. | Ghi chú Phụ lục A, Bước 1–4. | "theo bốn bước". |
| nhẹ | L08-2-09 | 18. Tên tiếng Anh của cận trên bậc hai thiếu "descent lemma" và tên "bổ đề hạ" của ghi chú. | Ghi chú Phụ lục A: "*cận trên bậc hai* (còn gọi là bổ đề hạ; quadratic upper bound, descent lemma)". | "cận trên bậc hai (còn gọi là bổ đề hạ; quadratic upper bound, descent lemma)" hoặc đưa vào ghi chú diễn giả nếu vượt trần. |

**Ý tưởng chứng minh.** Sáu trang (2-09, 3-02, 4-02, 4-06, 5-02, 6-03) kiểm từng bước: bất đẳng thức then chốt gọi đúng tên (tính đồng bức; Mệnh đề 08.5(a) trên từng quỹ đạo; Mệnh đề 08.5(b); Mệnh đề 06.5(b); hệ số giãn $1+\beta\eta$), giả thiết vào đúng bước như ghi chú ((S) và $\eta_t\le2/\beta$ chỉ ở bước chung; (G) ở bước khác biệt và ở tính Lipschitz; (I) chỉ ở bước lấy kì vọng; (R) ở cận tối ưu), "không cần $i_t$ độc lập với $\Delta_t$" đúng. Các phản ví dụ (hàm lõm, cosin, $\eta=3$, $\lvert w\rvert$, bản lề, ReLU) đúng và đúng giả thiết bị bỏ.

## 4. Bảng thống nhất trang → khối ghi chú

| Trang | Khối ghi chú | Kí hiệu, nhãn, số hiệu, dữ liệu | Ghi chú |
|---|---|---|---|
| 1-01 | Đoạn mở đầu, §10 | khớp | — |
| 1-02 | Tiên quyết; Định nghĩa 06.9, Định lý 06.10; (T1), (T2) | khớp | phát hiện 16 |
| 1-03 | Mục tiêu học tập | khớp (giữ điều kiện "hai lần nghịch đảo hằng số trơn") | — |
| 1-04 | §4–§12 | khớp | — |
| 1-05 | §10, câu hỏi trung tâm | khớp | phát hiện 3, 5 (ghi chú diễn giả) |
| 1-06 | Câu hỏi mở đầu, Phụ lục F | bảng khớp từng số | — |
| 2-01 | §1, Thuật toán 08.1 | khớp | — |
| 2-02 | §2: (S), (S′), (G), (L), (I), (T3), (R), (X); hằng số logistic, bình phương | khớp | phát hiện 14 |
| 2-03 | Ví dụ 08.1; khối ứng dụng §3 | khớp | — |
| 2-04 | Định nghĩa 08.2 | khớp | — |
| 2-05 | §4, hai đoạn sau Định nghĩa 08.2 | khớp ($\tfrac14$, $\tfrac38$) | — |
| 2-06 | Ví dụ 08.2 | khớp; F1 khớp | — |
| 2-07 | Định nghĩa 08.3, ba đoạn sau | khớp | phát hiện 15 |
| 2-08 | Bổ đề 08.4 | giả thiết $0\le\eta\le2/\beta$, $W$ đóng lồi, (a)–(c) khớp | — |
| 2-09 | Chứng minh Bổ đề 08.4; Phụ lục A | khớp | phát hiện 17, 18 |
| 2-10 | Ví dụ 08.3, đoạn cuối §5 | khớp | — |
| 2-11 | Bài tập 08.3(a) | khớp | — |
| 3-01 | Mệnh đề 08.5, hai đoạn sau; Phụ lục B(i) | giả thiết (S), (G), (I), $0<\eta_t\le2/\beta$; (a) tất định, (b) kì vọng theo $\xi$ khớp | — |
| 3-02 | Chứng minh Mệnh đề 08.5 | khớp | — |
| 3-03 | Ví dụ 08.4 | khớp | — |
| 3-04 | Bài tập 08.1(c) | khớp | — |
| 4-01 | Định lý 08.6 | (T1), (T2), (S), (G), $\eta_t\le2/\beta$, $\xi$ độc lập; (a)–(c), kì vọng theo $(S,\xi)$, trị tuyệt đối khớp | — |
| 4-02 | Chứng minh Định lý 08.6; danh sách giả thiết | khớp; lập luận đổi vai khớp Bài 06 | — |
| 4-03 | Ví dụ 08.5 | khớp | phát hiện 8 (ghi chú diễn giả) |
| 4-04 | Ví dụ 08.6; Phụ lục F | khớp; F2 khớp | phát hiện 9 (ghi chú diễn giả) |
| 4-05 | Hệ quả 08.7, đoạn sau | khớp | — |
| 4-06 | Chứng minh Hệ quả 08.7 | khớp | — |
| 4-07 | Bài tập 08.7 | khớp | phát hiện 12 |
| 5-01 | §8 đoạn mở, Hệ quả 08.8; Mệnh đề 06.5(b) | (T1), (T2), (S), (G), (R), $\eta$ hằng, $\bar w_T$ khớp | phát hiện 6 |
| 5-02 | Phụ lục C; đoạn sau Hệ quả 08.8 | khớp | — |
| 5-03 | Ví dụ 08.7 | khớp; F4 khớp | — |
| 5-04 | Định nghĩa 08.9, hai đoạn sau | dừng sớm, chính quy hóa tường minh khớp | phát hiện 4 |
| 5-05 | Bài tập 08.8 | khớp | — |
| 5-00 | §8 | — | phát hiện 3 |
| 6-01 | Ví dụ 08.8 | khớp; F3 khớp | — |
| 6-02 | Mệnh đề 08.10, đoạn sau | (S′), (G), $\eta_t>0$ bất kì; (a)–(c) khớp | — |
| 6-03 | Phụ lục D; đoạn sau Mệnh đề 08.10; Nhận xét 08.11 | khớp; Nhận xét 08.11 ở ghi chú diễn giả theo quyết định cổng duyệt | — |
| 6-04 | Mệnh đề 08.12 (đọc thêm), đoạn sau | khớp | phát hiện 11 |
| 6-05 | Ví dụ 08.9 | khớp | — |
| 6-06 | Ví dụ 08.10, đoạn sau | Bước 1, 2 khớp | phát hiện 1, 2, 10 |
| 6-07 | Bài tập 08.3(d) | khớp | — |
| 7-01, 7-02 | §5–§10 | sáu dòng kết quả khớp phát biểu, loại bảo đảm, giả thiết | — |
| 7-03 | §10 | khớp | phát hiện 13 |
| 7-04 đến 7-06 | Bài tập 08.5 | đề, bảng (c), (d)(i) khớp | — |
| 7-07 | §12 câu hỏi cuối buổi, §4, §7 | khớp | — |
| 7-08 | §11; `exercises.md` | tám bài, số hiệu khớp | — |
| 7-09 | §12 đoạn cuối, §13 | khớp | — |
| 2-00, 3-00, 4-00, 6-00, 7-00 | đoạn mở các mục | khớp | phát hiện 7 (4-00) |

Thứ tự khái niệm theo thứ tự mục của ghi chú (§1–§2 → §3 → §4 → §5 → §6 → §7 → §8 → §9 → §10–§13); mỗi mạch ứng với các mục liên tiếp. Nhãn (X), (S′), (I), (R), (S), (G), (L), (T1)–(T3) dùng đúng như §2. Số hiệu kết quả, ví dụ, bài tập trên mặt trang trùng khối ghi chú cùng số.

## 5. Đề xuất sửa ghi chú

- Ví dụ 08.8, bảng Bước 4: các giá trị lấy độ chính xác khác nhau ($0{,}0061$; $0{,}0411$; $0{,}207$; $0{,}2753$; $1{,}529$; $2{,}879$). Đề xuất thống nhất bốn chữ số có nghĩa hoặc bốn chữ số thập phân, chẳng hạn $\Delta_{58}\approx0{,}2073$ (giá trị tính lại $0{,}20732$). Không ảnh hưởng đến deck.
- Không thấy lỗi toán học mới trong ghi chú. Các điểm đã ghi ở `review-log.md` ($g_t$ ba nghĩa; "gần 0" trong Định nghĩa 08.9) vẫn còn.

## 6. Kết luận

Mọi con số trên mặt trang, trong ghi chú diễn giả và trong bốn SVG đã tính lại và khớp ghi chú, `exercises.md`. Không có phát hiện chặn bàn giao hoặc nghiêm trọng. Bốn phát hiện trung bình đều là điều kiện bị bỏ trong phát biểu rút gọn: hai ở 6-06, một ở dòng dẫn 5-00, một ở 5-04. Mười bốn phát hiện nhẹ.

**Kết luận: đạt khi sửa** (0 chặn bàn giao, 0 nghiêm trọng, 4 trung bình, 14 nhẹ).
