# Rà toán bộ bài tập Bài 10 (người rà 2)

Đối tượng: `lec10-ex-frozen.md` (926 dòng; `cmp` trùng `2627-1/materials/lec-10/exercises.md`). Chỉ đọc repo, không commit. Đã tự giải lại mọi bài và mọi ý. Script `reviews10/r2/ex/ex_check.py` tính lại mọi số: phân số chính xác; liệt kê quỹ đạo; hàm `replay` của `exp_lec10_pg_replay.py` nạp trực tiếp, chạy lại 20 hạt giống, cộng phần rủi ro sau nhiệm vụ A dựng lại theo đúng thứ tự rút. Nguồn đã đối chiếu:
- UML tr. PDF 305–306 (Bài tập 21.4, 21.5);
- `MLbookSol.pdf` tr. 52–53 (lời giải 21.4, 21.5), chỉ để kiểm rằng lời giải của ta không chép;
- tham chiếu chéo: lec-05 Định nghĩa 05.2 (đoạn sau: "$0\in\partial F(w)$ khi và chỉ khi … cực tiểu toàn cục"), Mệnh đề 05.3(a), Hệ quả 05.15(b) ($F_R$); lec-01 (T1) dạng yếu (dòng 100); lec-04 (T7); lec-06 Hệ quả 06.2; lec-09 Định nghĩa 09.1 và 09.7.

## Tổng kết theo mức

| Mức | Số |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 1 |
| nhẹ | 3 |

Mọi đáp số đúng; mọi số khớp lần chạy lại. Đề UML trung thành về toán với PDF. Lời giải 10.8, 10.9 không chép bản lời giải: cấu trúc khác, nhiều bước hơn, và chỉ số đoạn đúng hơn (bản lời giải dùng $\sum_{m=1}^{\lceil\log T\rceil}$). Gợi ý đúng hướng. Lỗi trung bình duy nhất là lập luận đo được ở 10.3(a). Người soạn đã tự nêu nghi ngờ đúng chỗ này (`bai-tap-ghi-chu.md` §6.1).

## Bảng từng bài

| Bài | Đánh giá | Ghi chú |
|---|---|---|
| 10.1 | ✓ | $\pi=\tfrac14$, $J=1$, $J'=\tfrac34$; phương sai $\tfrac{27}{16}$; đồng nhất thức (c) với hệ số $\mathbb E[(A-\pi)^2]=\pi(1-\pi)$; $b^*=3$, phương sai $0$; $b=1$: $\tfrac34$; $b^*-J=(1-2\pi)(r(1)-r(0))$, nên "trùng khi và chỉ khi $\pi=\tfrac12$ hoặc $r(1)=r(0)$" đúng; (d) $\Pr=0,0,\tfrac14$; $\operatorname{Var}\hat g_5=\tfrac34$; (e) $J''=4\pi(1-\pi)(1-2\pi)=\tfrac38$, lõm trên $[0,\infty)$. |
| 10.2 | ✓ | (a) đúng, kể cả chỗ $\pi=0$ (Bổ đề 10.3(a)). (b) $-\tfrac14$ và $0{,}225$, kiểm bảng: $0{,}425-0{,}2$. (c) $r_0$ là hàm của $\mathcal F_1$; kì vọng $0{,}25$, phương sai $0{,}4875<0{,}5625$. (d) quy tắc nhân, $\mathbb E[\ln\pi\mid\mathcal F_t]=-\mathrm H$; $\mathrm H(\tfrac34)=0{,}21576+0{,}34657=0{,}56234$; $\tfrac38+0{,}5623=0{,}9373$, gấp $2{,}4996$ lần. "Kiểm tra lại" khớp Ví dụ 10.9 và Nhận xét 10.9(i). |
| 10.3 | ✓ (một lỗi trung bình ở (a)) | (a) Biểu diễn bằng hàm phân phối ngược đúng ($2H$ biến đều); $\psi=\nabla F$ đúng theo Định lý 10.4. Câu về tính đo được sai lập luận (phát hiện 1). (b) $G=H^2C_rC_\pi$, $C_\pi=1$; $\mathbb E\varphi^2=\pi(1-\pi)(9-8\pi)$; $f'=24\pi^2-34\pi+9$, nghiệm $0{,}35233$ và $1{,}06433$; giá trị lớn nhất trên $[0,2]$ là $1{,}25$ tại $\theta=0$. (c)(i) $\pi_{-2}=0{,}11920$, $F(-2)=-1{,}23841$, $\psi(-2)=-0{,}20999$, đường thẳng tại $0$ cho $-1{,}65838>-2$: bất đẳng thức dưới gradient sai, đúng chiều. (ii) $\tilde F$ lồi, khả vi, (C), (G1) qua Mệnh đề 05.3(a), (G2) chỉ cần trên $W$ (Định nghĩa 05.10). (iii) $\eta=0{,}017889$; $RG/\sqrt T=0{,}022361\le0{,}0224$; $J(2)=2{,}761594$; cận dưới $2{,}739233\ge2{,}7392$, hợp lệ cả khi làm tròn. (d) Miền lồi đổi theo dấu của $r(1)-r(0)$. Ví dụ 10.7: $F=-0{,}375$ tại điểm dừng, $\inf F=-1$, nên $0\notin\partial F$. |
| 10.4 | ✓ (nhẹ, phát hiện 2) | (a) $0{,}7533$; $-0{,}19$; $0{,}15$, $0{,}28$, trung bình $0{,}215$; $0{,}015$. (b) đúng, dấu bằng đúng điều kiện. (c) bảy ô đúng; $\epsilon=\sqrt{\ln280/4000}=0{,}037533\le0{,}0376$; $2\epsilon=0{,}075065\le0{,}0752$; $\Delta_{\mathrm b}\le-0{,}1148$, $\Delta_{\mathrm f}\in[-0{,}0602;0{,}0902]$. Cận hợp không cần độc lập giữa các ô: đúng. (d) đúng. |
| 10.5 | ✓ | (a) bảng ba hệ số đúng; $\lambda\ge4\iff(1+\lambda)^2\ge25$; tỉ số $\tfrac{100}9\approx11{,}1$ và $5{,}76$ ("gần sáu lần"). (b) tập Pareto $[0,1]$, ảnh $(0,1]$ đúng. (c) $w=\frac{1-\alpha}{1+3\alpha}$, $\tfrac15$; $\tfrac12$; $\tfrac15$; $\lambda\Omega=\frac{4\alpha}{1-\alpha}$. (d) cực tiểu $\tfrac25$ tại $\tfrac15$; tại $\tfrac12$: $\tfrac58$, chênh $\tfrac9{40}$. |
| 10.6 | ✓ | Mọi số của đề khớp lần chạy lại (bảng số). (b)(i) độ quên theo thang rủi ro $0{,}499$, $0{,}131$; tổng $0{,}750$, $0{,}504$; $\min(L_A+L_B)=\tfrac14+0{,}25=0{,}5$. (ii) sai số chuẩn tính từ độ lệch chuẩn đã làm tròn trong đề ($0{,}0275$; $0{,}0262$; $0{,}0096$; tỉ số $10{,}6$; $2{,}9$; $0{,}5$), nhất quán với dữ liệu đề cho. Từ số chưa làm tròn: $0{,}02761$; $0{,}02606$; $0{,}00955$; tỉ số $10{,}58$; $2{,}87$; $0{,}51$, cùng kết luận. Hai nhóm độc lập: $0{,}0124$. (iii), (c): kết luận đúng phạm vi. |
| 10.7 | ✓ | (i) (T1) đầy đủ với quan sát là lượt; bán kính nhân $H(r_{\max}-r_{\min})$. (ii) (T1) dạng yếu khi chuỗi dừng, khớp lec-01 dòng 100; (T3) thay bằng $[0,\ln(1/c)]$ theo Ví dụ 09.4. |
| 10.8 | ✓ | (a) đúng: điều kiện hóa, tháp, cận số lỗi đúng trên mọi dãy, chỉ số đều. (b) Markov; $0{,}01$; $T\ge4000$. (c) đúng; $2M_A/T$ cho nửa đầu đúng. "Kiểm tra lại" với $M_A=0$ đúng (đối thủ chọn được mọi $x$). Đề trung thành UML 21.5; thêm "tất định" và (b), (c), đã ghi là của học phần. |
| 10.9 | ✓ (nhẹ, phát hiện 3, 4) | (a) $M=\lfloor\log_2T\rfloor$; tổng cấp số nhân, $<\sqrt2\,2^{M/2}/(\sqrt2-1)\le\frac{\sqrt2}{\sqrt2-1}\sqrt T$. (b) vế phải tăng theo $L$; $\eta=R/(G\sqrt{2^m})$ cho $RG\sqrt{2^m}$. (c) $10$ đoạn; $74{,}8406$; $107{,}9669\le107{,}97$; tỉ số $2{,}37$. Đề trung thành UML 21.4; giả thiết "kể cả đoạn bị cắt" do học phần thêm và được (b) kiểm. |

## Bảng số

| Bài | Số trong tệp | Tính lại | Kết luận |
|---|---|---|---|
| 10.1 | $\tfrac14$, $1$, $\tfrac34$, $\tfrac{27}{16}$, $3$, $0$, $\tfrac34$, $\tfrac94$/$\tfrac14$, $-\tfrac34$/$\tfrac54$, $\tfrac38$ | khớp (phân số) | ✓ |
| 10.2 | $-\tfrac14$; $0{,}225$; $0{,}425-0{,}2$; $0{,}25$; $0{,}55$; $0{,}4875$; $0{,}2158+0{,}3466=0{,}5623$; $0{,}9373$; "khoảng $2{,}5$" | $0{,}225$; $0{,}25$; $0{,}4875$; $0{,}562335$; $0{,}937335$; $2{,}4996$ | ✓ |
| 10.3 | $0{,}3523$; $1{,}0643$; $0{,}8808$; $1{,}25$; $1{,}1180$; $0{,}1192$; $-1{,}2384$; $-0{,}2100$; $-1{,}6584$; $0{,}01789$; $0{,}0224$; $2{,}7616$; $2{,}7392$; $-0{,}375$ | $0{,}352333$; $1{,}064333$; $0{,}880797$; $1{,}25$; $1{,}118034$; $0{,}119203$; $-1{,}238406$; $-0{,}209987$; $-1{,}658380$; $0{,}017889$; $0{,}022361$; $2{,}761594$; $2{,}739233$ | ✓ |
| 10.4 | $0{,}7533$; $-0{,}19$; $0{,}15$; $0{,}28$; $0{,}215$; $0{,}015$; $0{,}0376$; $0{,}0752$; $-0{,}1148$; $[-0{,}0602;0{,}0902]$; $0{,}025$ | $0{,}753333$; $0{,}037533$; $0{,}075065$; $-0{,}114935$; $[-0{,}060065;0{,}090065]$ | ✓ |
| 10.5 | bảng (a); $11$ lần; "gần sáu lần"; $\tfrac25$; $\tfrac58$; $\tfrac9{40}$; $\tfrac5{18}$, $\tfrac{17}{50}$ | khớp; $\tfrac{100}9$; $5{,}76$ | ✓ |
| 10.6 (đề) | sau A: $0{,}125$ ($0{,}002$), $0{,}614$; bảng 4 hàng (trung bình, độ lệch chuẩn); hiệu $0{,}292$ ($0{,}123$), $0{,}075$ ($0{,}117$), $0{,}005$ ($0{,}043$) | $0{,}12507$ ($0{,}00175$), $0{,}61407$; A: $0{,}6235$ ($0{,}0506$), $0{,}3313$ ($0{,}1324$), $0{,}2565$ ($0{,}0363$), $0{,}2516$ ($0{,}0419$); B: $0{,}1263$ ($0{,}0035$), $0{,}2183$ ($0{,}0761$), $0{,}2479$ ($0{,}0378$), $0{,}2546$ ($0{,}0449$); hiệu $0{,}29222$ ($0{,}12348$), $0{,}07484$ ($0{,}11652$), $0{,}00484$ ($0{,}04272$) | ✓ |
| 10.6 (lời giải) | $0{,}499$; $0{,}131$; $0{,}750$; $0{,}504$; $0{,}5$; $0{,}004$; $0{,}0275$/$10{,}6$; $0{,}0262$/$2{,}9$; $0{,}0096$/$0{,}5$; $0{,}0553$; $0{,}0124$ | khớp với đầu vào đã làm tròn (xem bảng từng bài) | ✓ |
| 10.8 | $0{,}01$; $4000$ | khớp | ✓ |
| 10.9 | $M=9$; $10$ đoạn; $74{,}84$; $3{,}4142$; $31{,}623$; $\le107{,}97$; "khoảng $2{,}4$" | $74{,}8406$; $107{,}9669$; $2{,}3667$ | ✓ |

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | dòng 329 (10.3(a), Bước 2) | Lập luận đo được không đứng: "với $\theta$ cố định, $g(\theta,\cdot)$ hằng trên từng hộp … và trên mỗi hộp, $\varphi$ là hàm liên tục của $\theta$". Các hộp phụ thuộc $\theta$ qua ngưỡng $\pi_\theta(1\mid S_t)$ (và qua $S_t$), nên "trên mỗi hộp, liên tục theo $\theta$" không có nghĩa. Ngoài ra, tính đo được theo $\xi$ với từng $\theta$ cộng tính liên tục theo $\theta$ với từng $\xi$ (hàm Carathéodory) mới là điều cần, nhưng $\varphi(\cdot,\xi)$ không liên tục: nó nhảy khi $\pi_\theta(1\mid s)$ đi qua $U_t$. Kết luận vẫn đúng. | Bước 1 dòng 324: $A_t=\mathbb 1[U_t<\pi_\theta(1\mid S_t)]$; `bai-tap-ghi-chu.md` §6.1 | "Với mỗi quỹ đạo $\tau'$, tập $\{(\theta,\xi):g(\theta,\xi)=\tau'\}$ là giao hữu hạn các tập $\{U_t<\pi_\theta(1\mid s_t)\}$ hay phần bù của chúng, cùng các điều kiện chỉ theo $U_{\mathrm{init}}$, $V_t$; mỗi tập đó đo được (thậm chí mở hay đóng tương đối) vì $\theta\mapsto\pi_\theta(1\mid s)$ liên tục. Do đó $\varphi(\theta,\xi)=\sum_{\tau'}\mathbb 1[g(\theta,\xi)=\tau']\cdot\big(-\hat g_\theta(\tau')\big)$ là tổng hữu hạn của tích một hàm chỉ thị đo được theo cặp với một hàm liên tục theo $\theta$, nên đo được theo cặp $(\theta,\xi)$." (Ghi $\hat g_\theta(\tau')$ để nhắc rằng gradient log tính tại $\theta$.) |
| nhẹ | dòng 455, 516 (10.4(c)) | Đề gọi "giá trị tổng thể" $1-L_{D_i}(w^{(k)})$ nhưng không nói đây là đại lượng ngẫu nhiên theo dữ liệu huấn luyện và xác suất lấy theo mẫu kiểm tra. Bước 1 chỉ viết "Khi các tham số đã cố định". | Hệ quả 02.10 cần $h$ không phụ thuộc mẫu; $w^{(k)}$ phụ thuộc mẫu huấn luyện, bộ đệm, nguồn ngẫu nhiên | Thêm vào Bước 1: "Điều kiện hóa theo mọi dữ liệu huấn luyện và nguồn ngẫu nhiên của thuật toán (độc lập với các mẫu kiểm tra); khi đó $w^{(k)}$ và mô hình riêng của $\mathrm{acc}^\circ_i$ cố định. Khẳng định đúng với xác suất $\ge1-\delta$ có điều kiện, nên cũng đúng khi lấy kì vọng theo dữ liệu huấn luyện. Giá trị tổng thể là một số ngẫu nhiên theo dữ liệu huấn luyện, không phải một hằng số của phương pháp." |
| nhẹ | dòng 856, 862, 899 (10.9(a)–(b)) | (a) giả sử cận theo đoạn "với mọi $u\in W$", nhưng (b) chỉ chứng minh cận cho các $u$ có $\lVert w_1-u\rVert\le R$. "Thỏa giả thiết của (a) với $\alpha=RG$" chỉ đúng khi $R\ge\sup_{u\in W}\lVert w_1-u\rVert$. | Nhận xét 10.16, Bảo đảm (chỉ cho $u$ với $\lVert w_1-u\rVert\le R$) | Ở (b): "với $R\ge\sup_{u\in W}\lVert w_1-u\rVert$" (cần $W$ bị chặn), hoặc phát biểu (a) cho một tập điểm so sánh $U\subseteq W$ rồi dùng $U=\{u\in W:\lVert w_1-u\rVert\le R\}$. |
| nhẹ | dòng 895 (10.9(a), Bước 4) | "Thứ tự này cần thiết" không đúng. Lấy cận trên đúng theo từng đoạn trước cũng cho cận đúng, vì $\sup_u\sum_m\le\sum_m\sup_u\le\alpha\sum_m2^{m/2}$; chính nửa sau của câu nói điều đó. | Bất đẳng thức $\sup_u\sum_m f_m(u)\le\sum_m\sup_uf_m(u)$ | "Vế phải không phụ thuộc $u$, nên lấy cận trên đúng theo $u\in W$ ta được cùng cận cho hối tiếc tĩnh; điểm so sánh tốt nhất của từng đoạn có thể khác nhau, nhưng $\sup_u\sum_m\le\sum_m\sup_u$ nên điều này không làm hỏng cận." |
