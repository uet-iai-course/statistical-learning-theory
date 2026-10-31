# Rà soát 1 — Học viên cao học, Bài 10 (bản đóng băng `lec10-draft-frozen.md`)

Vai trò: học viên đã học Bài 01–09, chưa học học tăng cường hay học liên tục. Chỉ đọc; không sửa tệp nào trong repo. Vị trí theo số dòng của bản đóng băng. Đề xuất câu chữ theo `no-ai-slop` Detect.

## Đã kiểm lại (không có lỗi)

- Câu ôn nhanh 1–2 (bán kính $0{,}060736\le0{,}0608$; ba đạo hàm sigmoid).
- Câu hỏi mở đầu ($0{,}2+0{,}6q$; $0{,}5$ và $0{,}74$).
- Ví dụ 10.1, 10.4, 10.8 (bốn phương sai $\tfrac{27}{64},\tfrac3{16},0,\tfrac{147}{64}$; $b^*=\tfrac32$), 10.9, 10.11 ($0{,}1225$; $27{,}6225$; $0{,}06$; tỉ số $225{,}5$), 10.12 ($0{,}17179$; $11\,804{,}4$), 10.13 (cả năm bước), 10.14, 10.15, 10.16 ($1/(8M)=\alpha^2/(2M)$ với $\alpha=\tfrac12$).
- Ví dụ 10.2 và 10.5: tám xác suất, $J(0)=1{,}75$; gradient $(-0{,}025;\,0{,}25;\,-0{,}125)$ trùng sai phân hữu hạn bằng Python.
- Ví dụ 10.6: $0{,}125$ và $-0{,}25$. Ví dụ 10.7: $q=0{,}375$, $\theta=\ln0{,}6$, $J=0{,}375$, đạo hàm bậc hai $0{,}1758$.
- Ví dụ 10.10: ba vết $1{,}94625$; $1{,}62125$; $0{,}324375$ (tỉ số đúng $6$), cùng bước 2.
- Ví dụ 10.17: hối tiếc $-116{,}967$ và $0{,}1876$; $w_{T+1}\approx1$ và $\tfrac12$.
- Nhận xét 10.9(i): $\ln2$. Mệnh đề 10.13 và §12(a)–(e): đều đúng. §12(f) làm được từ bảng §1 và §7–§9.
- Mọi số hiệu dẫn về Bài 01–09 đều tồn tại và khớp nội dung: 01.1, 01.5, 01.6, 01.9, 01.22, 01.24, 02.7, 02.8, 02.10, 02.14, 03.15, 04.11, 04.17, 05.10–05.15, 05.18, 06.2, 07.11, 08.12, 09.1, 09.2, 09.4, 09.8, 09.12 (Bước 4), 09.14, 09.15.
- Thí nghiệm: chạy lại `exp_lec10_pg_replay.py --part all` (1,7 giây). Mọi số của Ví dụ 10.11, Ví dụ 10.16 và Phụ lục C khớp từng chữ số.
- Tái lập độc lập từ lời của Phụ lục C (`reviews10/r1/repro.py`):
  - Phần phát lại: trùng từng chữ số.
  - Phần REINFORCE: chỉ khớp về định tính, chẳng hạn $c=10$, không giá trị nền cho trung bình $0{,}553$ và $45/100$ lần chạy dưới $0{,}5$ (bản ghi chú: $0{,}509$ và $49$). Xem mục T7.
- `forward_refs.py` không chạy được trên đường dẫn scratchpad vì cần chuỗi `lec-NN` trong tên tệp. Người rà soát chính cần chạy nó trên tệp trong repo.

## Tổng kết theo mức

- **Chặn bàn giao: 0.**
- **Nghiêm trọng: 2.**
  - N1: số thí nghiệm ở kết luận Ví dụ 10.16 thuộc một mô hình khác ví dụ, nên mâu thuẫn với các số của chính ví dụ.
  - N2: câu về hối tiếc tĩnh ở dòng 768 sai về toán, và Ví dụ 10.17 là phản ví dụ.
- **Trung bình: 9.** Gồm: câu hỏi mở đầu chưa được trả lời đủ cho tình huống 2; Mệnh đề 08.12 được áp dụng không kèm lập luận; Ví dụ 10.10 Bước 1 đi quá nhanh; $L_{\mathcal B}$ trùng $L_B$; "độ chính xác" chưa nối với hàm lỗi; Nhận xét 10.9(i) quá dày; thiếu liên hệ Fisher–Hesse; Phụ lục C chưa đủ để tái lập đúng từng số; Ví dụ 10.6 Bước 2 nhảy bước.
- **Nhẹ: 16.**

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | 749 (kết luận Ví dụ 10.16) | Thí nghiệm dùng hồi quy $y=wx$ với nhiễu phương sai $0{,}25$, nên $L_A=\tfrac12(w^2+0{,}25)$. Ví dụ dùng $L_A=\tfrac12(w^2+1)$, với $L_A(\tfrac12)=\tfrac58=0{,}625$ và $\min L_A=0{,}5$. Đọc nối tiếp, học viên thấy "$0{,}624$ khi tinh chỉnh" trùng rủi ro *thỏa hiệp* của ví dụ, còn "$0{,}25$ của điểm thỏa hiệp" và "$0{,}125$ của riêng nhiệm vụ A" không xuất hiện trong ví dụ. Câu thành mâu thuẫn. | "rủi ro kiểm tra trên A sau nhiệm vụ B là $0{,}624$ khi tinh chỉnh và $0{,}331$; $0{,}256$; $0{,}252$ với $M=5$, $50$, $1000$: gần $0{,}25$ của điểm thỏa hiệp, không gần $0{,}125$ của riêng nhiệm vụ A." | Nêu mô hình của thí nghiệm ngay trong câu: "Thí nghiệm của học phần (Phụ lục C) dùng hồi quy $y=wx$, với $L_A(w)=\tfrac12(w^2+0{,}25)$, $\min L_A=0{,}125$ và điểm thỏa hiệp $w=\tfrac12$ cho $0{,}25$. Rủi ro kiểm tra trên A sau nhiệm vụ B là …" (khoảng +20 chữ). |
| nghiêm trọng | 768 | Khi hối tiếc tĩnh là $o(T)$, ta chỉ có $\frac1T\sum\ell(w_t,z_t)\le\min_u\frac1T\sum\ell(u,z_t)+o(1)$, không có "tiến tới". Ví dụ 10.17 Bước 3 là phản ví dụ: hối tiếc $-116{,}97$, nên hàm lỗi trung bình thấp hơn của điểm cố định tốt nhất $0{,}117$ và không tiến tới nó. | "khi nó tăng chậm hơn $T$, hàm lỗi trung bình theo thời gian tiến tới hàm lỗi trung bình của điểm cố định tốt nhất." | "khi nó tăng chậm hơn $T$, hàm lỗi trung bình theo thời gian vượt hàm lỗi trung bình của điểm cố định tốt nhất không quá một lượng tiến về $0$." (+6 chữ) |
| trung bình | 13, 15 | Câu hỏi mở đầu hỏi "Có thể gộp mọi quan sát … không?". Lời đáp cho tình huống 2 chỉ nói về điểm thỏa hiệp, không trả lời việc gộp. Học viên chỉ gặp câu trả lời ở dòng 595 (gộp = học có giám sát với hỗn hợp; ở đây $M=0$ nên không gộp được). | "Ở tình huống thứ hai, mỗi môi trường có phân bố riêng, và không $w$ nào cho cả hai rủi ro bằng $0$, nên cần một điểm thỏa hiệp (§8)." | "Ở tình huống thứ hai, dữ liệu của A không còn khi học B nên không gộp được; nếu giữ được, mẫu gộp có phân bố hỗn hợp của hai môi trường (§7). Không $w$ nào cho cả hai rủi ro bằng $0$, nên cần một điểm thỏa hiệp (§8)." (khoảng +25 chữ) |
| trung bình | 397 và 410 | Dòng 397 nói nguồn ngẫu nhiên của REINFORCE khác Định nghĩa 05.10. Dòng 410 lại nói Mệnh đề 08.12 "áp dụng" mà không nói vì sao. Giả thiết của 08.12 dẫn tới lịch sử "như Định nghĩa 05.10" và cần $\eta$ hằng với $\eta\le1/\beta$, trong khi Thuật toán 10.6 cho $\eta_j$ thay đổi. Học viên thấy hai câu mâu thuẫn. Quy tắc của học phần cũng cấm chuyển kết quả sang học tăng cường mà không có lập luận mới. | "Mệnh đề 08.12 áp dụng cho $F=-J$ khi $J$ trơn và ước lượng có phương sai bị chặn" | "Chứng minh của Mệnh đề 08.12 chỉ dùng kì vọng và phương sai có điều kiện theo lịch sử; với lịch sử là các lượt trước, $\eta_j=\eta\le1/\beta$, $J$ là $\beta$-trơn và phương sai có điều kiện bị chặn, cận của nó áp dụng cho $F=-J$, nhưng chỉ bảo đảm …" Nếu chưa kiểm chứng minh ở Phụ lục E của Bài 08 thì viết "cần kiểm lại chứng minh … (Bài tập 10.3)". (khoảng +20 chữ) |
| trung bình | 523 (Ví dụ 10.10, Bước 1) | Ví dụ đi quá nhanh: ba con số tổng không có bước trung gian, nên không kiểm được bằng tay. Phải viết chương trình mới thấy (iii) giảm chủ yếu ở tọa độ $\theta_{s_0}$. | "Tính trên tám quỹ đạo, tổng phương sai của ba tọa độ, tức vết của ma trận hiệp phương sai, là $1{,}94625$ cho (i), $1{,}62125$ cho (ii) và $0{,}324375$ cho (iii)." | Thêm một dòng phương sai theo tọa độ: (i) $(1{,}011875;\,0{,}6875;\,0{,}246875)$; (ii) $(1{,}011875;\,0{,}5625;\,0{,}046875)$; (iii) $(0{,}24625;\,0{,}0625;\,0{,}015625)$. Thêm một câu: "(ii) không đổi tọa độ $\theta_{s_0}$ vì $R_{\ge0}=R(\tau)$." (khoảng +30 chữ) |
| trung bình | 640, 645, 736 | $L_{\mathcal B}$ (rủi ro trên bộ đệm) và $L_B$ (rủi ro nhiệm vụ B) chỉ khác nét chữ. Ở Ví dụ 10.16 cả hai đứng cạnh nhau. Dòng 645 chỉ phân biệt $\mathcal B$ với bán kính $B$ của Bài 05. | "đạo hàm của $\tfrac12L_B+\tfrac12L_{\mathcal B}$ là $\tfrac12(w-1)+\tfrac12(w-\bar Z_M)$" | Ở dòng 645 thêm: "$L_{\mathcal B}$ khác rủi ro $L_B$ của nhiệm vụ B ở §8." (+10 chữ). Cách khác là đổi tên bộ đệm. |
| trung bình | 585–600, 607 | Định nghĩa 10.10 nói về hàm lỗi $\ell$ và rủi ro $L_k$, còn Định nghĩa 10.11 dùng "độ chính xác" mà không nối với $\ell$. Học viên không biết "độ chính xác" của Ví dụ 10.16 (hồi quy) là gì. Dòng 607 áp dụng Hệ quả 02.10 cũng ngầm cần giá trị trong $[0,1]$. | "$\mathrm{acc}_{k,i}$ là độ chính xác của $w^{(k)}$ trên mẫu kiểm tra của nhiệm vụ $i$" | "… độ chính xác, tức $1$ trừ rủi ro thực nghiệm với hàm lỗi 0–1, của $w^{(k)}$ trên mẫu kiểm tra …; với hàm lỗi khác, dùng rủi ro kiểm tra và đổi chiều các bất đẳng thức." (+20 chữ) |
| trung bình | 531 (Nhận xét 10.9(i)) | Câu dài khoảng 70 chữ, gói bốn ý. Học viên chưa biết vì sao lại "lấy gradient theo $\theta$ của cả tích $(R_{\ge t}-b_\theta)\ln\pi_\theta$"; việc lấy đạo hàm tự động của một hàm thay thế chưa được giới thiệu. Chữ $\vartheta$ dễ đọc nhầm thành $\theta$. | "Nếu giá trị nền dùng chung tham số với chính sách và ta lấy gradient theo $\theta$ của cả tích $\big(R_{\ge t}-b_\theta(S_t)\big)\ln\pi_\theta(A_t\mid S_t)$, kết quả có thêm số hạng …, tức $\ln2\approx0{,}6931$ với bài toán bandit hai hành động, $b_\theta=\theta$, $\theta=0$." | Tách thành ba câu. (1) Động cơ: "Khi cài đặt, ước lượng thường được tính bằng đạo hàm của $(R_{\ge t}-b)\ln\pi_\theta(A_t\mid S_t)$." (2) Số hạng thừa và kì vọng của nó. (3) Ví dụ bằng số. Có thể bỏ ví dụ $\ln2$ để giữ số chữ. |
| trung bình | 705–714, 722 | Nhận xét 10.14 định nghĩa EWC bằng ma trận Fisher, nhưng Ví dụ 10.15 dùng ma trận Hesse và hàm lỗi bình phương. Không câu nào nối hai ma trận, nên học viên không biết vì sao ví dụ dùng Hesse. | "Ma trận Hesse của $L_A$ là $\begin{pmatrix}1&1\\1&1\end{pmatrix}$" | Ở (ii): "Phạt bậc hai là khai triển Taylor bậc hai của rủi ro cũ quanh $w^{(1)}$, với $\Omega$ là ma trận Hesse; với hàm lỗi log và mô hình chứa phân bố thật, ma trận Fisher bằng ma trận Hesse này tại $w^{(1)}$." (khoảng +35 chữ; cần người rà toán xác nhận điều kiện.) |
| trung bình | 991, 998, 1005 (Phụ lục C) | Phụ lục nói "đủ để tái lập", nhưng không nêu cách rút hành động và nhấp. Script so một số đều với $\pi$, còn `rng.binomial` cho chuỗi khác. Bản tái lập độc lập cho $0{,}553$ và $45$ lần chạy thay vì $0{,}509$ và $49$. Phụ lục cũng không nói độ lệch chuẩn dùng $m-1$, và không nói "rút đều từ bộ đệm" là có hoàn lại. | "mỗi hạt giống khởi tạo bộ sinh `numpy.random.default_rng`, và mỗi bước rút hành động rồi rút nhấp." | "… mỗi bước rút một số đều $U$ và chọn hành động $1$ khi $U<\pi_{\theta_j}(1)$, rồi rút một số đều khác cho nhấp. Độ lệch chuẩn chia cho số lần chạy trừ $1$." Ở phần phát lại: "rút đều có hoàn lại từ bộ đệm". Nếu không muốn thêm thì viết "tái lập về định tính". (Phụ lục; nằm ngoài thân bài nếu số chữ chỉ tính thân bài.) |
| trung bình | 373 (Ví dụ 10.6, Bước 2) | Nhảy bước: không nói vì sao số hạng $r_1(A_0-\tfrac12)$ có kì vọng $0$. | "Ở đây $A_0$ không ảnh hưởng tới $S_1$, nên chỉ phần thưởng ở bước đầu đóng góp vào tọa độ $\theta_{s_0}$" | "…; vì $r_1$ độc lập với $A_0$, $\mathbb E[r_1(A_0-\tfrac12)]=\mathbb Er_1\cdot\mathbb E(A_0-\tfrac12)=0$, nên chỉ …" (+15 chữ) |
| nhẹ | 545 (Ví dụ 10.11, Bước 4) | Thuật toán 10.6 không có giá trị nền, nhưng bảng chạy "có giá trị nền" mà không ghi công thức cập nhật. | "Thuật toán 10.6 với $\theta_1=0$, … giá trị nền là trung bình phần thưởng của các lượt trước." | "Thuật toán 10.6, với $R(\tau_j)$ thay bằng $R(\tau_j)-b_j$ khi có giá trị nền $b_j$ là trung bình …" (+10 chữ) |
| nhẹ | 554 | Thiếu ý nghĩa: không giải thích vì sao $c=10$ làm gần nửa số lần chạy hỏng. | "gần một nửa số lần chạy không có giá trị nền kết thúc ở nội dung kém hơn." | Một câu cơ chế: "với $c=10$, mỗi cập nhật đẩy chính sách về phía hành động vừa chọn với cỡ khoảng $c\,\eta$, lớn hơn nhiều so với tín hiệu $0{,}05$." Chỉ thêm nếu còn chỗ. |
| nhẹ | 5 | "chiết khấu" được dùng nhưng không định nghĩa, cũng không có thuật ngữ tiếng Anh. Học viên chưa học học tăng cường. | "số bước cố định và không chiết khấu phần thưởng" | "… và cộng phần thưởng các bước không nhân hệ số giảm dần (chiết khấu, discount)". Hoặc bỏ cụm này ở dòng 5 và giữ dòng 146. |
| nhẹ | 3 và 5 | Hai câu liền nhau cùng dạng "điều gì thay đổi khi…", nên lặp ý. | "Câu hỏi cuối Bài 09 là điều gì thay đổi khi hành động của người học quyết định quan sát tiếp theo, và khi phân bố của dữ liệu thay đổi trong lúc học." | **Cắt** câu này (−34 chữ); dòng 5 đã nêu câu hỏi trung tâm. |
| nhẹ | 97, 102 | "bài toán bandit" có trong tiêu đề khối, nhưng chỉ được định nghĩa ở câu áp chót của phần Thiết lập. | "Bài toán chọn một trong hữu hạn hành động có phần thưởng chưa biết được gọi là *bài toán bandit*" | Đưa câu định nghĩa lên đầu phần Thiết lập (0 chữ). |
| nhẹ | 88 | "như Bài 05, chỉ số $j$" gợi ý rằng Bài 05 dùng $j$, trong khi Bài 05 dùng $t$ (dòng 768 cũng nói vậy). | "độ dài bước tại cập nhật $j$, số cập nhật (như Bài 05, chỉ số $j$)" | "(như $\eta_t$ của Bài 05; chỉ số $j$ vì $t$ là bước trong lượt)" (+6 chữ) |
| nhẹ | 429, 645 | Các câu trỏ vòng ("ví dụ thứ ba sau hệ quả dưới đây") khó theo, và là tham chiếu tới trước dù không ghi số. | "ví dụ thứ ba sau hệ quả dưới đây, Bước 2, cho một trường hợp phương sai tăng."; "ví dụ thứ ba sau mệnh đề dưới đây đo sai lệch này." | **Cắt** cả hai mệnh đề trỏ (−18 và −13 chữ); Ví dụ 10.10 và 10.16 đã tự nói điều đó. |
| nhẹ | 635, 682 | "xung đột" là thuật ngữ trong tiêu đề §8 và Mệnh đề 10.13 nhưng không có định nghĩa. Ví dụ 10.15 chỉ gợi nghĩa. | "Theo (a), khi hai nhiệm vụ xung đột, cải thiện một bên buộc bên kia xấu đi" | Ở dòng 635: "Hai nhiệm vụ *xung đột* khi không tham số nào cực tiểu hóa đồng thời hai rủi ro." (+14 chữ) |
| nhẹ | 33, 531, 771 | Danh sách tiên quyết thiếu entropy $\mathrm H$ (Định nghĩa 09.7, dùng ở dòng 531) và dưới gradient $\partial\ell$ (Định nghĩa 05.2, dùng ở dòng 771). §12(f) dùng (T3) mà danh sách không nêu. | "Giả sử $\ell(\cdot,z)$ lồi với mọi $z$, …, $w_{t+1}=\operatorname{proj}_W(w_t-\eta v_t)$ với $v_t\in\partial\ell(w_t,z_t)$" | Thêm "dưới gradient (Định nghĩa 05.2)", "entropy (Định nghĩa 09.7)" và "(T3) (đoạn sau Nhận xét 02.8)" (+10 chữ). Có thể bỏ Định nghĩa 09.14, vì thân bài không dẫn nó. |
| nhẹ | 949 (Phụ lục A, Bước 6) | $K$ trùng với số nhiệm vụ $K$ trong bảng kí hiệu §2. | "bị chặn bởi một hằng số $K$ với mọi $s$" | Đổi thành $C_\mu$. |
| nhẹ | 795, 797 (Ví dụ 10.17) | Bước 3 không nói rằng hối tiếc tĩnh bằng hối tiếc so với $u=\tfrac12$ (vì $u=\tfrac12$ cực tiểu hóa tổng ở Bước 1). Bước 4 không giải thích vì sao $w_{t+1}$ là trung bình. Các số $-116{,}97$ và $0{,}19$ không tính tay được mà không ghi là tính bằng máy. | "Hối tiếc so với $u=\tfrac12$ bằng $-116{,}97$, âm vì thuật toán theo kịp từng nửa dãy." | "Theo Bước 1, hối tiếc tĩnh bằng hối tiếc so với $u=\tfrac12$; tính trực tiếp trên $1000$ vòng, nó bằng $-116{,}97$ …". Ở Bước 4: "$w_{t+1}=(1-\tfrac1t)w_t+\tfrac1tz_t$, nên theo quy nạp …" (+20 chữ) |
| nhẹ | 744, 816 | $\alpha^2/(2M)$ được viết cho $\alpha$ tổng quát, nhưng chỉ được suy ra với $\alpha=\tfrac12$. §10 nêu nó như một giới hạn chung. | "$=\tfrac12\cdot\tfrac14\cdot\tfrac1M=\frac{\alpha^2}{2M}$"; "Bộ đệm $M$ quan sát thêm $\alpha^2/(2M)$ vào rủi ro cũ theo kì vọng" | Trong ví dụ viết $=\tfrac1{8M}$; ở §10 viết "thêm $1/(8M)$ … trong Ví dụ 10.16". |
| nhẹ | 363 | Kết luận không nối $-0{,}1$ với đạo hàm $-0{,}025$. | "nó mất $1$ ở bước đầu và chỉ được thêm $(0{,}8-0{,}2)(2-\tfrac12)=0{,}9$ ở bước sau." | Thêm: "nên $\partial J/\partial\theta_{s_0}=\tfrac14(1{,}7-1{,}8)$." (+6 chữ) |
| nhẹ | 223 | Câu lắt léo: "điểm trong $\theta$ của $\Theta$" đọc như "θ trong Θ". | "đạt giá trị nhỏ nhất tại điểm trong $\theta$ của $\Theta$" | "đạt giá trị nhỏ nhất tại $\theta$, một điểm trong của $\Theta$" |
| nhẹ | 146 | Câu dài khoảng 60 chữ. "không ảnh hưởng tới các bước sau" mơ hồ (nhiễu của phần thưởng hay phần thưởng?). Khẳng định "vẫn đúng" không kèm lí do. | "Phần thưởng ngẫu nhiên, như ở khối ứng dụng của §3, được phép nếu khi biết trạng thái và hành động của bước đó, nó có phân bố không phụ thuộc $\theta$ và không ảnh hưởng tới các bước sau; …" | Tách hai câu; thêm "(thay $r_t$ bằng kì vọng có điều kiện của nó theo tính chất tháp)". |
| nhẹ | 15 | Phần thưởng của robot chưa được cho, nên "trung bình các phần thưởng … đạo hàm theo $q$ bằng $0$" khó hiểu ngay ở câu mở đầu. | "Trung bình các phần thưởng đã nhận không chứa $q$, nên đạo hàm của nó theo $q$ bằng $0$" | "Khi dữ liệu đã thu, trung bình các phần thưởng là một số cố định, không chứa $q$; nó không cho biết phần thưởng kì vọng đổi thế nào khi $q$ đổi." |

## Ngân sách chữ (thân bài 11 982/12 000)

Đề xuất thêm theo thứ tự ưu tiên, tổng khoảng 170 chữ:

| Mục | Số chữ thêm (ước tính) |
|---|---|
| N1 | +20 |
| N2 | +6 |
| Câu hỏi mở đầu | +25 |
| Mệnh đề 08.12 | +20 |
| Ví dụ 10.10 | +30 |
| $L_{\mathcal B}$ | +10 |
| acc | +20 |
| Fisher–Hesse | +35 |
| Ví dụ 10.6 | +15 |

Có thể cắt khoảng 175 chữ mà không mất nội dung:

| Dòng | Câu cắt | Số chữ |
|---|---|---|
| 3 | Câu cuối ("Câu hỏi cuối Bài 09 là …"), lặp dòng 5 | −34 |
| 129 | "Hai ví dụ trên chỉ có một bước, nên không có trạng thái nào nối các bước với nhau.", vì dòng 133 đã dẫn sang | −19 |
| 429 | Mệnh đề trỏ "ví dụ thứ ba …" | −18 |
| 645 | Mệnh đề trỏ "ví dụ thứ ba …" | −13 |
| 413 | Câu đầu, lặp đoạn sau $\square$ ở dòng 298 | −20 |
| 752 | Cả câu tổng kết, lặp dòng 682 và Ví dụ 10.14 | −42 |
| 808 | Câu "Rủi ro kì vọng trở thành … chính sách hiện tại.", vì §12(f) đã làm việc này | khoảng −28 |

Nếu vẫn thiếu chỗ, rút ví dụ bằng số $\ln2$ ở Nhận xét 10.9(i) (khoảng −20 chữ).

## Ghi chú `no-ai-slop` (Detect)

Không có từ bị cấm, câu hỏi tu từ hay lời chỉ dẫn của giảng viên. Ba câu kết hơi mang dạng châm ngôn, có thể giữ vì vẫn mang nội dung:

- Dòng 628: "một con số "độ quên" chỉ có nghĩa khi kèm quy ước tính nó".
- Dòng 802: "chọn đại lượng nào là một phần của việc đặc tả bài toán, như chọn hàm lỗi ở Bài 01".
- Dòng 752: câu tổng kết lặp ý (đã đề xuất cắt ở trên).
