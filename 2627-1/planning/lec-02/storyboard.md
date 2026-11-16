# Storyboard — Bộ trang chiếu Bài 02: Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-11-15 bởi tác tử lập storyboard. Nguồn nội dung duy nhất: `materials/lec-02/lecture-note.md` (bản hiện hành); bài tập: `materials/lec-02/exercises.md`. Quy định: `CLAUDE.md` § Slide decks (bản 2026-11-15, gồm mục "Các quy định dễ sót" của `common-brief.md`), `../rl-plan/CLAUDE.md` § Deck structure and content, nhật ký yêu cầu 2026-11-13 hàng 1–6, quyết định của điều phối viên cho khuôn chung (2026-11-15). Khuôn bố cục theo storyboard thí điểm `planning/lec-01/storyboard.md`. Mọi mã trang có dạng `L02-k-mm`; trong bảng viết gọn `k-mm`.

Số âm tiết ghi trong tệp này là ước lượng của người lập (đếm theo khoảng trắng, không tính tiêu đề, KaTeX, số trong bảng, nhãn hình, ghi chú); điều phối viên đếm lại trên deck.

UML đã đọc để đối chiếu (không chép câu chữ): Phụ lục B.4, trang PDF 425–426 (bất đẳng thức Hoeffding, bổ đề Hoeffding); §4.2, trang PDF 55–56 (bước tất định trên tập $\epsilon/2$-đại diện, bất đẳng thức hợp trên lớp hữu hạn). Các mục khác chỉ dẫn theo số mục của ghi chú §12 và `sources/uml-sections.md`.

## 1. Tên tệp và tiêu đề

- **Tệp deck:** `2627-1/lecture-02-bat-dang-thuc-tap-trung.html` (slug ASCII từ phần đầu tên bài; phần "và độ phức tạp mẫu của lớp hữu hạn" bỏ khỏi slug cho ngắn).
- **Tiêu đề deck (h1 trang bìa):** "Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn" (đúng tên bài của ghi chú).
- **`<title>`:** "Bài 02: Bất đẳng thức tập trung".
- **Chân trang:** "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài 02".
- **Liên kết viewer:** `material-viewer.html?doc=materials/lec-02/lecture-note.md&deck=lecture-02-bat-dang-thuc-tap-trung.html` và `…exercises.md&deck=…`.
- **Trang cuối deck Bài 01** (7-05 của storyboard Bài 01) nhận liên kết tới tệp này khi deck Bài 02 xong.

## 2. Khung lý thuyết chung

**Vấn đề trung tâm (hộp "Vấn đề trung tâm", một dòng, bằng lời).** "Câu hỏi: trên một lớp giả thuyết hữu hạn, cần bao nhiêu quan sát để rủi ro thực nghiệm nằm gần rủi ro kì vọng, cho giả thuyết chọn trước và cho giả thuyết chọn theo chính tập huấn luyện?" (câu hỏi trung tâm ở đoạn mở đầu của ghi chú; ≈ 37 âm tiết.)

**Luận điểm (trang bìa, một câu, bằng lời).** "Với quan sát độc lập và hàm lỗi bị chặn, rủi ro thực nghiệm của mọi giả thuyết trong một lớp hữu hạn nằm gần rủi ro kì vọng với xác suất cao, và cỡ mẫu đủ chỉ tăng theo lôgarit của số giả thuyết." (Định lý 02.14 và §9 của ghi chú; ≈ 42 âm tiết; không kí hiệu vì trang bìa là trang tổng quan.)

**Đối tượng và kí hiệu chung** (ghi chú §1–§3, `ky-hieu.md`):
- $\mathcal Z=\mathcal X\times\mathcal Y$, phân bố $D$ cố định chưa biết; $S=(Z_1,\ldots,Z_m)\sim D^m$;
- lớp hữu hạn $\mathcal H$, $K=\lvert\mathcal H\rvert$; hàm lỗi $\ell$ trong $[0,1]$ ($\ell_{0\text{-}1}$), hoặc trong $[a,b]$ ($\ell_c\in\{0,1,4\}$);
- $L_D(h)$, $L_S(h)$, nghiệm ERM $\hat h$, phần tử tốt nhất $h_{\mathcal H}\in\arg\min_{h\in\mathcal H}L_D(h)$;
- biến ngẫu nhiên $V$, $V_1,\ldots,V_m$, $\mu_i$, $\bar V_m$, $\bar\mu_m$; độ lệch $\epsilon$, xác suất thất bại $\delta$, tham số mũ $\tau$;
- bán kính tin cậy $r_m=\sqrt{\ln(2K/\delta)/(2m)}$, $r_m^{+}=\sqrt{\ln(K/\delta)/(2m)}$; $\mathcal H_{>\epsilon}$;
- ví dụ xuyên suốt: $D_\eta$, $D_f$, $h_t$, $S_\eta$ (Bài 01).

**Giả thiết** (ghi chú §2): (T1) $Z_1,\ldots,Z_m$ i.i.d. theo $D$ (dạng yếu: mỗi $Z_i\sim D$); (T2) $\ell\ge0$, $\ell(h,\cdot)$ đo được; (T3) $\ell(h,z)\in[0,1]$; (T4) $\mathcal H$ hữu hạn, $K$ phần tử, chọn trước khi lấy mẫu; (O1) $\hat h\in\arg\min_{h\in\mathcal H}L_S(h)$; (O2) $\epsilon_{\mathrm{opt}}$-ERM; khả diễn (Định nghĩa 01.16) ở §8.

**Chuỗi định nghĩa → kết quả → phương pháp.**
1. Xác suất đuôi và cận đuôi (Định nghĩa 02.1); giá trị chính xác khi biết $D_\eta$ (Ví dụ 02.2).
2. Cận dùng mô-men: Markov (Bổ đề 02.2), Chebyshev (Bổ đề 02.3); giảm như $1/m$, cỡ mẫu như $1/\delta$ (Ví dụ 02.3).
3. Hàm sinh mô-men (Định nghĩa 02.4), phương pháp Chernoff (Bổ đề 02.5), bổ đề Hoeffding (Bổ đề 02.6), bất đẳng thức Hoeffding (Định lý 02.7): cận giảm mũ theo $m\epsilon^2$, cỡ mẫu như $\ln(1/\delta)$.
4. Cận tin cậy (Định nghĩa 02.9, Hệ quả 02.10) cho một $h$ cố định; phản ví dụ khi bỏ độc lập (Ví dụ 02.6), bỏ bị chặn (Nhận xét 02.11).
5. Thiên lệch do chọn (Ví dụ 02.7) → bất đẳng thức hợp → hội tụ đều trên lớp hữu hạn (Định nghĩa 02.13, Định lý 02.14), giá $\ln K$.
6. Bước tất định → rủi ro vượt mức của mọi nghiệm ERM (Hệ quả 02.16), cỡ mẫu $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$.
7. Trường hợp khả diễn: biến cố "không quan sát nào sai" (Mệnh đề 02.17), cỡ mẫu $\lceil\ln(K/\delta)/\epsilon\rceil$; hai tốc độ $1/\epsilon$ và $1/\epsilon^2$ (Nhận xét 02.18).

**Giới hạn áp dụng** (ghi chú §5, §9): hàm lỗi phải bị chặn (Nhận xét 02.11); quan sát phải độc lập (Ví dụ 02.6); lớp giả thuyết phải cố định trước khi lấy mẫu dùng để đánh giá (T4), nên lớp phụ thuộc dữ liệu và dùng lại thích nghi nằm ngoài các kết quả; cận theo $\ln K$ không cho thông tin khi lớp vô hạn (cầu nối Bài 03); các cận đúng cho mọi phân bố nên bảo thủ (gấp khoảng $13$ lần giá trị chính xác ở $m=100$). Tính đo được (Phụ lục C) không đưa lên deck.

## 3. Bảng mạch

Bảy mạch theo đúng thứ tự các mục của ghi chú; mỗi mạch ứng với các mục liên tiếp. Mạch 3 và 4 chia §5 tại Định nghĩa 02.9 (trước đó: công cụ; từ đó: áp dụng cho rủi ro thực nghiệm). Bảng đối chiếu trang → khối ghi chú ở mục 12.

| N | Tên mạch | Mục ghi chú | Chức năng | Đầu vào | Đầu ra | `strand-lead` (âm tiết) | Từ khóa | Trang | Phút |
|---|---|---|---|---|---|---|---|---:|---:|
| 1 | Mở đầu | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết | Bìa, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, câu hỏi mở đầu $5\%$ trên $1000$ quan sát | Bài 01: $\mathbb E_SL_S(h)=L_D(h)$ chỉ với $h$ cố định | Hai câu hỏi: một hàm cố định, một hàm chọn trong $1000$ ứng viên | (không có trang tiêu đề mạch) | — | 6 | 8 |
| 2 | Xác suất đuôi và bất đẳng thức Markov, Chebyshev | §1–§4 | Giả thiết, bốn đại lượng cần chặn; ví dụ $D_\eta$; xác suất đuôi chính xác; hai cận dùng mô-men | câu hỏi mở đầu | Cận Chebyshev $25/m$ không phụ thuộc phân bố; cỡ mẫu tăng như $1/\delta$ | "Kì vọng và phương sai chặn được xác suất tỉ lệ lỗi lệch xa rủi ro kì vọng, nhưng cận chỉ giảm tỉ lệ nghịch với cỡ mẫu." | xác suất đuôi · cận đuôi · bất đẳng thức Markov · bất đẳng thức Chebyshev | 7 | 15,5 |
| 3 | Phương pháp Chernoff và bất đẳng thức Hoeffding | §5, từ Định nghĩa 02.4 đến Nhận xét 02.8 | Hàm sinh mô-men; kỹ thuật Chernoff; bổ đề Hoeffding; Định lý 02.7 | cận chỉ giảm như $1/m$ | Cận $2e^{-2m\epsilon^2/(b-a)^2}$ cho biến độc lập, bị chặn | "Với các biến độc lập và bị chặn, xác suất trung bình lệch xa kì vọng giảm theo hàm mũ của cỡ mẫu." | hàm sinh mô-men · phương pháp Chernoff · bổ đề Hoeffding · dây cung | 6 | 19,5 |
| 4 | Cận tin cậy cho một giả thuyết cố định | §5, từ Định nghĩa 02.9 đến hết mục | Cận tin cậy, khoảng tin cậy; Hệ quả 02.10; kỹ thuật đảo cận đuôi; so sánh ba cận; trả lời phần đầu câu hỏi mở đầu; hai phản ví dụ | Định lý 02.7 | Bán kính $\sqrt{\ln(2/\delta)/(2m)}$, cận một phía $8{,}9\%$; cần (T1), (T3), $h$ cố định | "Rủi ro kì vọng của một giả thuyết chọn trước nằm trong một khoảng tính từ tập huấn luyện, với độ tin cậy cho trước." | cận trên tin cậy · khoảng tin cậy · bán kính tin cậy · cỡ mẫu | 7 | 17 |
| 5 | Hội tụ đều và rủi ro vượt mức trên lớp hữu hạn | §6, §7 | Thiên lệch do chọn; tập đại diện; Định lý 02.14; Bài tập 02.4; trả lời phần sau câu hỏi mở đầu; Hệ quả 02.16; kỹ thuật bước tất định | cận cho $h$ cố định không chuyển sang $\hat h$ | Bán kính $r_m$ đồng thời, rủi ro vượt mức $2r_m$, cỡ mẫu $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$ | "Bất đẳng thức hợp đổi cận cho từng giả thuyết thành cận đồng thời cho cả lớp, với giá là lôgarit của số giả thuyết." | thiên lệch do chọn · tập đại diện · hội tụ đều · rủi ro vượt mức | 13 | 29,5 |
| 6 | Lớp hữu hạn trong trường hợp khả diễn | §8, §9 | Giả thuyết nhất quán, giả thuyết xấu; Mệnh đề 02.17; bốn mức cỡ mẫu; bảng cỡ mẫu; hai tốc độ; Bài tập 02.8; giới hạn (T4) | cỡ mẫu bất khả diễn $\propto1/\epsilon^2$ | Cỡ mẫu khả diễn $\lceil\ln(K/\delta)/\epsilon\rceil$; nguồn của hai tốc độ; lớp phụ thuộc dữ liệu | "Khi lớp giả thuyết có một hàm không sai, chỉ cần loại các giả thuyết xấu, nên cỡ mẫu tăng chậm hơn theo độ chính xác." | giả thuyết nhất quán với tập huấn luyện · giả thuyết xấu · hai tốc độ · lớp phụ thuộc dữ liệu | 9 | 19,5 |
| 7 | Tổng kết | §10, §11, §12 | Bảng kết quả, trả lời vấn đề trung tâm, bài tập tổng hợp, tự kiểm tra, bài tập về nhà, tài liệu | mọi kết quả | Cầu nối sang Bài 03 | "Trên lớp hữu hạn, cỡ mẫu đủ tăng theo lôgarit của số giả thuyết và theo một trong hai tốc độ của độ chính xác." | — | 7 | 11 |
| | **Tổng** | | | | | | | **55** | **120** |

Số trang của deck: **55** (trần), sau quyết định của điều phối viên (thêm trang kỹ thuật chia $\delta/K$, `5-05`; câu hỏi dùng nguyên câu chữ Bài tập 02.3(a), trang riêng `5-12`; bỏ trang so ba cận, gộp vào ghi chú diễn giả `3-04`; chi tiết ở mục 15). Dòng dẫn mạch viết lại theo bài học deck 01 (câu trần thuật về nội dung, không mở bằng "Người học …"). Lý do số trang ban đầu (54): bài có sáu kết quả chính, mỗi kết quả có trang "Ý tưởng chứng minh" riêng theo quyết định khuôn chung; ba kỹ thuật dùng lại qua học phần có trang "Kỹ thuật." riêng (phương pháp Chernoff, đảo cận đuôi, bước tất định); Bài tập 02.4 cần hai trang (đề, lời giải) để giữ trần 60 âm tiết; mạch Tổng kết có thêm trang bài tập tổng hợp theo quy định 2026-11-15. Phương án rút còn 51 ở mục 11, điểm 2.

## 4. Bảng kết quả chính

Số hiệu theo ghi chú. Năm kết quả của blueprint (Lemma 2.1, Theorem 2.2, Theorem 2.3, Corollary 2.4, Proposition 2.5) là Bổ đề 02.6, Định lý 02.7, Định lý 02.14, Hệ quả 02.16, Mệnh đề 02.17; Hệ quả 02.10 là bản áp dụng của Định lý 02.7 cho rủi ro thực nghiệm. Markov và Chebyshev là công cụ có chứng minh một dòng, chung một trang ý tưởng chứng minh. Mọi phát biểu rút gọn trên trang dùng "Giả thiết:" và "Bảo đảm:", giữ đủ giả thiết, lượng từ, hằng số và loại bảo đảm của ghi chú.

| Kết quả | Loại bảo đảm | (a) Trực quan | (b) Ý tưởng chứng minh | (c) Kỹ thuật | (d) Ví dụ bổ trợ | Trang |
|---|---|---|---|---|---|---|
| **Bổ đề 02.2, 02.3** (Markov, Chebyshev; chứng minh đầy đủ) | tất định về xác suất; (b) trung bình, giảm như $1/m$ | Phần $\{V\ge\alpha\}$ đóng góp ít nhất $\alpha\Pr(V\ge\alpha)$ vào $\mathbb EV$ (hình F2). Chebyshev là Markov cho bình phương độ lệch. | Markov: $\alpha\mathbb 1[V\ge\alpha]\le V$ từng điểm (dùng $V\ge0$), lấy kì vọng, chia cho $\alpha>0$. Chebyshev: Markov với $(V-\mathbb EV)^2$, $\alpha=\epsilon^2$; (b) $\operatorname{Var}\bar V_m\le\sigma^2/m$ (độc lập chỉ ở đây, đủ là không tương quan từng đôi). Cực biên: Markov xảy ra dấu bằng khi $V\in\{0,\alpha\}$ (Bài tập 02.1(a)). Bỏ độc lập: $Z_2=Z_1$ giữ phương sai $\sigma^2$ (câu ôn nhanh 2). | Bước "áp dụng Markov cho một hàm không âm của $V$" là một phần của kỹ thuật Chernoff (trang 3-01). | Ví dụ 02.3: bảng $m=6,100,200$; cỡ mẫu $500$. | 2-04, 2-05, 2-06 |
| **Bổ đề 02.5** (phương pháp Chernoff; chứng minh đầy đủ) | tất định | Mũ hóa biến $V$ làm giá trị lớn có trọng số mũ; với tổng độc lập, kì vọng của tích tách thành tích. | Hai bước một dòng: Markov cho $e^{\tau V}$; độc lập của $e^{\tau V_i}$. Coi là kỹ thuật, không là kết quả chính: phát biểu và chứng minh nằm chung trang kỹ thuật (mục 11, điểm 3). | **Phương pháp Chernoff** (lần đầu trong học phần, trang riêng 3-01). | Hàm sinh mô-men Bernoulli $1-q+qe^\tau$; đuôi nặng $c/j^3$ (ghi chú diễn giả). | 3-01 |
| **Bổ đề 02.6** (bổ đề Hoeffding; phác thảo) | tất định, mọi $\tau\in\mathbb R$ | Trong các biến trên $[a,b]$ cùng kì vọng, biến hai điểm $a$, $b$ làm vế trái lớn nhất (dây cung); hằng số $\tfrac18=\tfrac12\cdot\tfrac14$ đến từ phương sai Bernoulli $\le\tfrac14$. Hình F3. | Bốn bước: đưa về kì vọng $0$; dây cung (dùng bị chặn); đổi biến thành $e^{\varphi(u)}$; $\varphi(0)=\varphi'(0)=0$, $\varphi''\le\tfrac14$, Taylor. Bỏ bị chặn: hàm sinh mô-men có thể bằng $\infty$ (đuôi nặng). Cực biên: biến hai điểm đạt dấu bằng ở bước dây cung. | Dây cung của hàm lồi rồi Taylor bậc hai tại $0$ (dòng "Kỹ thuật." trên 3-03, chỉ dùng trong chứng minh này). | Mới N1: $V\sim\mathrm{Bernoulli}(0{,}22)$, $\tau=2$: $1{,}549\le1{,}649$. | 3-02, 3-03 |
| **Định lý 02.7** (bất đẳng thức Hoeffding; chứng minh đầy đủ) | xác suất cao; giảm mũ theo $m\epsilon^2/(b-a)^2$; chỉ phụ thuộc phân bố qua $b-a$ | Cận chỉ dùng độ dài miền giá trị; nhân đôi $m$ thì bình phương thừa số mũ ($2e^{-2}\to2e^{-4}$). | Năm bước: Chernoff tại mức $\epsilon$; tách tích (độc lập); bổ đề Hoeffding cho từng thừa số với $\tau/m$ (bị chặn); chọn $\tau=4m\epsilon/(b-a)^2$; đuôi dưới bằng $-V_i$, hai phía bằng hợp rời nhau. Không dùng cùng phân bố. Bỏ độc lập: Ví dụ 02.6. | Nhắc lại kỹ thuật Chernoff; chọn $\tau$ là câu ôn nhanh 3. | $h_3$: $0{,}2707$, $0{,}0366$ (Ví dụ 02.4). | 3-04, 3-05 |
| **Hệ quả 02.10** (cận tin cậy Hoeffding; chứng minh đầy đủ) | xác suất cao theo $S$, mọi $D$; bán kính $\propto1/\sqrt m$ | Bán kính giảm như $1/\sqrt m$: gấp bốn $m$ thì bán kính giảm một nửa; một phía chỉ đổi $\ln(2/\delta)$ thành $\ln(1/\delta)$. | $V_i=\ell(h,Z_i)$ (dùng $h$ không phụ thuộc $S$); (T1) cho độc lập và $\mu_i=L_D(h)$; (T3) cho $[0,1]$; Định lý 02.7; giải "cận $=\delta$". Bỏ "$h$ cố định": $V_i$ phụ thuộc cả $S$, thiên lệch do chọn (Ví dụ 02.7). | **Đảo cận đuôi thành bán kính và cỡ mẫu** (lần đầu, trang riêng 4-04). | Ví dụ 02.4 (bảng ba cận; $185$, $381$ so với $500$, $25\,000$); Ví dụ 02.5 ($0{,}0887$); Ví dụ 02.6, Nhận xét 02.11 (bỏ giả thiết). | 4-02 đến 4-06 |
| **Định lý 02.14** (hội tụ đều trên lớp hữu hạn; chứng minh đầy đủ) | xác suất cao; đồng thời mọi $h$; phụ thuộc $K$ qua $\ln K$; không phụ thuộc $D$ | Giá của tính đồng thời: $\ln(2K/\delta)=\ln K+\ln(2/\delta)$; $K=1$ cho lại Hệ quả 02.10; hình F4 ($r_m^{+}$ theo $K$). | Bốn bước: biến cố hỏng nằm trong $\bigcup_hB_h$; mỗi $h$ cố định theo (T4) nên $\Pr(B_h)\le2e^{-2mr^2}$; bất đẳng thức hợp, $K$ số hạng (T4); giải $2Ke^{-2mr^2}=\delta$. Không cần độc lập giữa các $B_h$. Cực biên: $B_1=\cdots=B_K$ làm hệ số $K$ lỏng nhất. Bỏ hệ số $K$: Bài tập 02.4. Bỏ (T4): §9. | Nhắc lại bất đẳng thức hợp (Bài 01). Dòng "Kỹ thuật.": mỗi giả thuyết nhận xác suất thất bại $\delta/K$ (ghép bất đẳng thức hợp với đảo cận đuôi; không trang riêng, mục 11, điểm 4). | Ví dụ 02.7 (vấn đề); $S_\eta$ (Định nghĩa 02.13); Bài tập 02.4; Ví dụ 02.8 ($0{,}1204$). | 5-01 đến 5-08 |
| **Hệ quả 02.16** (rủi ro vượt mức của ERM; chứng minh đầy đủ) | xác suất cao; đồng thời mọi nghiệm ERM, mọi quy tắc chọn khi bằng nhau; không phụ thuộc $D$ | Hệ số $2$: một lần so sánh $L_D$ với $L_S$ tại $\hat h$, một lần tại $h_{\mathcal H}$. | Chuỗi ba bất đẳng thức trên biến cố $r$-đại diện: đại diện tại $\hat h$, (O1), đại diện tại $h_{\mathcal H}$; Định lý 02.14(a); $2r_m\le\epsilon$. Bỏ (O1): bất đẳng thức giữa hỏng; (O2) thêm $\epsilon_{\mathrm{opt}}$. Cực biên $K=1$: rủi ro vượt mức bằng $0$. | **Bước tất định trên biến cố đại diện** (lần đầu, trang riêng 5-11). | Ví dụ 02.9 ($1097$, $0{,}32$) trên trang kết quả; Ví dụ 02.10 ($1431$) ở ghi chú diễn giả; Bài tập 02.3(a) làm câu hỏi kiểm tra. | 5-09, 5-10, 5-11 |
| **Mệnh đề 02.17** (lớp hữu hạn, khả diễn; chứng minh đầy đủ) | xác suất cao; rủi ro tuyệt đối; biến cố một phía; mọi nghiệm ERM | Một quan sát bị phân lớp sai đủ loại một giả thuyết xấu; xác suất giả thuyết xấu nhất quán với tập huấn luyện giảm như $(1-\epsilon)^m$. | Bốn bước: một giả thuyết xấu (T1); bất đẳng thức hợp trên $\mathcal H_{>\epsilon}$ cố định (T4); khả diễn cho $L_S(\hat h)=0$; giải $Ke^{-\epsilon m}=\delta$. Bỏ khả diễn: (a), (b) còn đúng, $L_S(\hat h)=0$ hỏng. Cực biên: các biến cố lồng nhau trên lớp hàm ngưỡng ($48\to37$). | Nhắc lại chặn xác suất bỏ sót và bất đẳng thức hợp (Bài 01). | Mới N2 ($h_4$ dưới $D_f$, $0{,}8^m$); Ví dụ 02.11 (48, 37, 30, 14); Ví dụ 02.12 (bảng); Bài tập 02.8. | 6-01 đến 6-07 |

**Kết quả phụ và quyết định.**
- Định nghĩa 02.1 (xác suất đuôi), Ví dụ 02.2: một trang chung (2-03), phép tính $m=6$ ở ghi chú diễn giả.
- Nhận xét 02.8 (miền giá trị khác nhau) và đoạn $\ell_c\in[0,4]$: ghi chú diễn giả 3-04; hệ số $(b-a)^2=16$ dùng lại ở bài tập tổng hợp 7-03 (Bài tập 02.11(b)) với dòng "Nhắc lại:".
- Nhận xét 02.11 (hàm lỗi không bị chặn): nửa phải của trang 4-06.
- Nhận xét 02.15 (cận tổng quát hóa cho mọi ERM trên lớp hữu hạn): ghi chú diễn giả 5-08.
- Ví dụ 02.10 (ERM trên $\mathcal M_{\mathcal X}$, $1431$): ghi chú diễn giả 5-09 và cầu nối 7-06. Lý do: giữ trần trang; ví dụ không có trực quan mới ngoài "tăng tuyến tính theo $\lvert\mathcal X\rvert$".
- Nhận xét 02.18 (hai tốc độ): trang trực quan riêng 6-06 (trọng tâm do điều phối viên nêu).
- Phụ lục A (bất đẳng thức $\varphi(u)\le u^2/8$): bước 3–4 của 3-03; Phụ lục B: số liệu cho bảng; Phụ lục C (đo được): không đưa lên deck.
- Câu ôn nhanh 1–3: ghi chú diễn giả 1-02, 2-05, 3-05.

## 5. Ví dụ bổ trợ

Ví dụ xuyên suốt: **sàng lọc với dữ liệu có nhiễu $D_\eta$** (Ví dụ 02.1), giả thuyết cố định $h_3$ với $\ell_{0\text{-}1}(h_3,Z)\sim\mathrm{Bernoulli}(0{,}22)$. Ví dụ thứ hai: **chọn một hàm phân lớp trong $K$ ứng viên trên tập xác thực** (khối ứng dụng §3, câu hỏi mở đầu). Mỗi lần dùng lại trả lời một câu hỏi mới: phân bố của $L_S(h_3)$ dồn về $0{,}22$ (2-03), cận Markov, Chebyshev (2-06), bổ đề Hoeffding trên một biến Bernoulli (3-02), cận Hoeffding (3-04, 3-04 (ghi chú diễn giả)), $L_S(h)$ không là cận trên tin cậy (4-01), bản sao một quan sát (4-06), độ lệch trên $S_\eta$ (5-02), cỡ mẫu bất khả diễn $1097$ (5-09), dữ liệu tất định $D_f$ trong trường hợp khả diễn (6-01, 6-04). Ví dụ ứng viên: câu hỏi (1-06), hàm cố định (4-05), thiên lệch do chọn (5-01), hàm được chọn (5-08), bảng cỡ mẫu (6-05), câu hỏi cuối buổi (7-04). Bài tập trên mặt trang lấy từ `exercises.md` với cùng số liệu và kết quả: Bài tập 02.4 (5-06, 5-07), 02.3(a) làm "Câu hỏi:" (5-11), 02.8(c)(d) (6-07), 02.11(b) (7-03).

Mọi con số dưới đây đã tính lại bằng Python (thư mục nháp `…/scratchpad/lec-02/storyboard/num.py`) và khớp ghi chú.

**V1. Rủi ro kì vọng dưới $D_\eta$** (Ví dụ 02.1, số của Bài 01). $L_{D_\eta}(h_t)=(0{,}52;\ 0{,}32;\ 0{,}22;\ 0{,}32;\ 0{,}28;\ 0{,}48)$, nhỏ nhất $0{,}22$ tại $t=3$. Trên $S_\eta$: $L_{S_\eta}(h_3)=\tfrac13$, lệch $\tfrac13-0{,}22=0{,}1133$.

**V2. Xác suất đuôi chính xác của $L_S(h_3)$** (Ví dụ 02.2, Phụ lục B.1), $\epsilon=0{,}1$, biến cố "$\ge$".
- $m=6$: $\lvert k/6-0{,}22\rvert$ bằng $0{,}22$; $0{,}0533$; $0{,}1133$ tại $k=0,1,2$, nên biến cố đuôi là $k\ne1$. $\Pr(k=1)=6\cdot0{,}22\cdot0{,}78^5=0{,}3811$; đuôi $=1-0{,}3811=0{,}6189$. Tính lại: $0{,}78^5=0{,}28872$; $1{,}32\cdot0{,}28872=0{,}38111$. Đúng.
- $m=100$: $\Pr(k\le12)=0{,}00779$, $\Pr(k\ge32)=0{,}01336$, tổng $0{,}02115\approx0{,}0211$.
- $m=200$: $\Pr(k\le24)=2{,}01\cdot10^{-4}$, $\Pr(k\ge64)=6{,}93\cdot10^{-4}$, tổng $8{,}94\cdot10^{-4}$.
- Hàm xác suất cho hình F1, $m=6$, $k=0,\ldots,6$: $0{,}2252;\ 0{,}3811;\ 0{,}2687;\ 0{,}1011;\ 0{,}0214;\ 0{,}0024;\ 0{,}0001$ (tổng $1{,}0000$). Kiểm tra cho $m=100$, $200$: giá trị lớn nhất tại $k=22$ ($0{,}0959$) và $k=44$ ($0{,}0680$).

**V3. Cận Markov và Chebyshev** (Ví dụ 02.3).
- Markov, đuôi trên, ngưỡng $\alpha=0{,}32$: $0{,}22/0{,}32=0{,}6875$ với mọi $m$. Đuôi trên chính xác: $0{,}3937$; $0{,}0134$; $6{,}9\cdot10^{-4}$ ($m=6$: $1-0{,}78^6-0{,}3811=1-0{,}2252-0{,}3811=0{,}3937$).
- $\operatorname{Var}\ell_{0\text{-}1}(h_3,Z)=0{,}22\cdot0{,}78=0{,}1716$; Chebyshev biết phương sai $0{,}1716/(0{,}01m)=17{,}16/m$: $2{,}86$; $0{,}1716$; $0{,}0858$.
- Không phụ thuộc phân bố: $\operatorname{Var}V\le\mu(1-\mu)\le\tfrac14$, cận $1/(4m\cdot0{,}01)=25/m$: $4{,}17$; $0{,}25$; $0{,}125$.
- Cỡ mẫu: $25/m\le0{,}05\iff m\ge500$.

**V4. Hàm sinh mô-men** (sau Định nghĩa 02.4). $V\sim\mathrm{Bernoulli}(q)$: $\mathbb Ee^{\tau V}=1-q+qe^\tau$. Đuôi nặng: $\Pr(V=j)=c/j^3$, $\mathbb EV=c\sum_jj^{-2}<\infty$, $\mathbb Ee^{\tau V}=\infty$ với mọi $\tau>0$.

**V5 (mới, N1). Bổ đề Hoeffding trên $V=\ell_{0\text{-}1}(h_3,Z)$** (trang 3-02, hình F3). Cách dựng: lấy biến của ví dụ xuyên suốt, $V\sim\mathrm{Bernoulli}(0{,}22)$, $[a,b]=[0,1]$, chọn $\tau=2$; tính hai vế của Bổ đề 02.6 bằng công thức hàm sinh mô-men Bernoulli của ghi chú. Đây là biến hai điểm tại hai đầu mút, nên vế phải của bước dây cung (Bước 2 của chứng minh) bằng đúng vế trái.
- $W=V-0{,}22\in\{-0{,}22;\ 0{,}78\}$; $a'=-0{,}22$, $b'=0{,}78$, $b'-a'=1$.
- Vế trái, lần 1: $\mathbb Ee^{2W}=0{,}78\,e^{-0{,}44}+0{,}22\,e^{1{,}56}=0{,}78\cdot0{,}64404+0{,}22\cdot4{,}75882=0{,}50235+1{,}04694=1{,}5493$.
- Vế trái, lần 2: $e^{-0{,}44}\big(1-0{,}22+0{,}22e^2\big)=0{,}64404\cdot(0{,}78+1{,}62562)=0{,}64404\cdot2{,}40562=1{,}5493$. Khớp.
- Dây cung tại $w=0$: $\big(b'e^{\tau a'}-a'e^{\tau b'}\big)/(b'-a')=0{,}78\cdot0{,}64404+0{,}22\cdot4{,}75882=1{,}5493$, trùng vế trái.
- Vế phải: $\exp(\tau^2(b-a)^2/8)=e^{4/8}=e^{0{,}5}=1{,}6487$. Vậy $1{,}549\le1{,}649$.
- Không mâu thuẫn ghi chú: chỉ dùng Bổ đề 02.6 và công thức $1-q+qe^\tau$ của ghi chú.

**V6. Cận Hoeffding và ba cận** (Ví dụ 02.4). $2e^{-0{,}02m}$: $m=100$: $2e^{-2}=0{,}2707$; $m=200$: $2e^{-4}=0{,}0366$ ($=2\cdot(e^{-2})^2=2\cdot0{,}135335^2=0{,}036631$). Giao điểm với $25/m$: $m=107$: $0{,}2336<0{,}2353$; $m=108$: $0{,}2315>0{,}2307$. Tỉ số ở $m=100$: $0{,}1716/0{,}0211=8{,}1$; $0{,}25/0{,}0211=11{,}8$; $0{,}2707/0{,}0211=12{,}8$; ghi chú làm tròn $8$, $12$, $13$.

**V7. Cỡ mẫu theo $\delta$** (Ví dụ 02.4 Bước 4), $\epsilon=0{,}1$. Chebyshev: $1/(4\delta\epsilon^2)$: $500$ ($\delta=0{,}05$), $25\,000$ ($\delta=0{,}001$). Hoeffding: $\ln(2/\delta)/0{,}02$: $\ln40=3{,}6889\to184{,}4\to185$; $\ln2000=7{,}6009\to380{,}05\to381$. Tỉ số: $25\,000/500=50$; $381/185=2{,}06$.

**V8. $L_S(h)$ không là cận trên tin cậy** (sau Định nghĩa 02.9). $\Pr(L_S(h_3)\ge0{,}22)=\Pr(\mathrm{Bin}(100;0{,}22)\ge22)=0{,}5391<0{,}95$.

**V9. Khoảng tin cậy cho hàm cố định** (Ví dụ 02.5). $\sqrt{3{,}6889/2000}=\sqrt{0{,}0018444}=0{,}04295$; khoảng $[0{,}0071;\ 0{,}0929]\approx[0{,}007;\ 0{,}093]$. Một phía: $\sqrt{2{,}9957/2000}=\sqrt{0{,}0014979}=0{,}03870$; $0{,}05+0{,}0387=0{,}0887$.

**V10. Hai phản ví dụ** (Ví dụ 02.6, Nhận xét 02.11).
- Bản sao: $\epsilon=0{,}2$, $m=100$: $2e^{-2\cdot100\cdot0{,}04}=2e^{-8}=6{,}71\cdot10^{-4}$; xác suất thật $1$ vì $\lvert L_S(h_3)-0{,}22\rvert\ge0{,}22$.
- Không bị chặn, $M=m^2$, $m=100$: $(1-10^{-4})^{100}=0{,}99005\ge1-\tfrac1{100}=0{,}99$; cận Hoeffding trên $[0,M]$, $\epsilon=1$: $2e^{-2m/M^2}=2e^{-2/m^3}=2e^{-2\cdot10^{-6}}=1{,}999996$.

**V11. Thiên lệch do chọn** (Ví dụ 02.7, Phụ lục B.2). $\Pr(\mathrm{Bin}(1000;0{,}07)\le50)=0{,}005930$; $(1-0{,}00593)^{1000}=e^{-5{,}947}=0{,}0026$; xác suất ứng viên tốt nhất có tỉ lệ lỗi $\le5\%$: $0{,}9974$.

**V12. Tập huấn luyện $S_\eta$ và tính đại diện** (sau Định nghĩa 02.13). Hiệu $L_{S_\eta}(h_t)-L_{D_\eta}(h_t)$: $\tfrac12-0{,}52=-0{,}02$; $\tfrac13-0{,}32=0{,}0133$; $\tfrac13-0{,}22=0{,}1133$; $\tfrac12-0{,}32=0{,}18$; $\tfrac13-0{,}28=0{,}0533$; $\tfrac12-0{,}48=0{,}02$. Lớn nhất theo trị tuyệt đối $0{,}18$ ($t=4$).

**V13. Bán kính theo $K$** (Ví dụ 02.8; hình F4, các điểm $K=10$, $100$ là số mới tính từ công thức của Định lý 02.14), $m=1000$, $\delta=0{,}05$.

| $K$ | $1$ | $10$ | $100$ | $1000$ | $5000$ |
|---|---|---|---|---|---|
| $\ln(K/\delta)$ | $2{,}9957$ | $5{,}2983$ | $7{,}6009$ | $9{,}9035$ | $11{,}5129$ |
| $r_m^{+}=\sqrt{\ln(K/\delta)/2000}$ | $0{,}0387$ | $0{,}0515$ | $0{,}0616$ | $0{,}0704$ | $0{,}0759$ |
| $r_m=\sqrt{\ln(2K/\delta)/2000}$ | $0{,}0429$ | $0{,}0547$ | $0{,}0644$ | $0{,}0728$ | $0{,}0781$ |

Kiểm tra $K=1000$: $\sqrt{9{,}9035/2000}=\sqrt{0{,}0049518}=0{,}07037$; cận $0{,}05+0{,}0704=0{,}1204$. $K=5000$: $\sqrt{0{,}0057565}=0{,}07587$; cận $0{,}1259$. Hiệu $0{,}0759-0{,}0704=0{,}0055$, ghi chú viết "khoảng $0{,}005$".

**V14. Bài tập 02.4** (5-06, 5-07; số và kết quả của `exercises.md`). $L_D(h_k)=\tfrac12$; $2m\epsilon^2=3{,}2$, $2e^{-3{,}2}=0{,}0815$; một $k$: $j\sim\mathrm{Bin}(10;\tfrac12)$, $j\in\{0,1,9,10\}$, $22/1024=0{,}0215$; $\Pr(\exists k:\ L_S(h_k)=0)=1-(1-2^{-10})^{1000}=1-e^{-0{,}9770}=0{,}6236$ ($K=5000$: $0{,}9924$); cận Định lý 02.14: $2Ke^{-3{,}2}=81{,}5$. Tính lại: $1000\ln(1-1/1024)=-0{,}97704$; $e^{-0{,}97704}=0{,}37642$. Đúng.

**V15. Cỡ mẫu bất khả diễn trên lớp hàm ngưỡng** (Ví dụ 02.9). $2K/\delta=240$, $\ln240=5{,}4806$, $2\cdot5{,}4806/0{,}01=1096{,}13\to1097$; bảo đảm $L_{D_\eta}(\hat h)\le0{,}22+0{,}1=0{,}32$. $m=6$: $r_6=\sqrt{5{,}4806/12}=0{,}676$, $2r_6=1{,}35>1$. Ví dụ 02.10: $5\ln2+\ln40=3{,}4657+3{,}6889=7{,}1546$, $1430{,}9\to1431$, cận $0{,}18+0{,}1=0{,}28$.

**V16 (từ ghi chú, N2). Giả thuyết xấu $h_4$ dưới $D_f$** (trang 6-01). Cách dựng: dùng $D_f$ của Ví dụ 02.11 ($f=h_3$, $D_{\mathcal X}$ đều) và $h_4$, sai đúng tại $x=3$, nên $L_{D_f}(h_4)=0{,}2$. $L_S(h_4)=0$ khi và chỉ khi $S$ không có quan sát nào tại $x=3$, xác suất $0{,}8^m$; đây cũng là biến cố thất bại của $A_{\max}$ ở Ví dụ 02.11 Bước 4. $0{,}8^{14}=0{,}04398\approx0{,}044$. Với $\epsilon=0{,}1$: $0{,}8^m<0{,}9^m\le e^{-0{,}1m}$ (dòng tổng quát $(1-L_D(h))^m<(1-\epsilon)^m\le e^{-\epsilon m}$). Không có con số mới ngoài cách đọc $0{,}8^m$ cho $h_4$.

**V17. Bốn mức cỡ mẫu** (Ví dụ 02.11). $\ln120=4{,}7875\to47{,}87\to48$; $\ln40/0{,}1=36{,}89\to37$; $\ln20/0{,}1=29{,}96\to30$; $0{,}8^{13}=0{,}0550>0{,}05$, $0{,}8^{14}=0{,}0440\le0{,}05\to14$.

**V18. Bảng cỡ mẫu cho $K$ ứng viên** (Ví dụ 02.12, Phụ lục B.3), $\delta=0{,}05$. Giá trị trước khi làm tròn, $\epsilon=0{,}05$ / $0{,}1$: $K=1$: $737{,}8$ / $184{,}4$; $K=100$: $1658{,}8$ / $414{,}7$; $6635{,}2$ / $1658{,}8$; $152{,}02$ / $76{,}01$; $K=1000$: $2119{,}3$ / $529{,}8$; $8477{,}3$ / $2119{,}3$; $198{,}1$ / $99{,}03$. Làm tròn lên: $738$/$185$; $1659$/$415$, $6636$/$1659$, $153$/$77$; $2120$/$530$, $8478$/$2120$, $199$/$100$. Nhân $K$ lên $10$: $\ln10=2{,}3026$; $115{,}1$, $460{,}5$, $23{,}0$.

**V19 (mới, N3). Hai tốc độ theo $\epsilon$** (hình F5, trang 6-06). Cách dựng: hai công thức của Ví dụ 02.12 (Hệ quả 02.16(c), Mệnh đề 02.17(c)) với $K=100$, $\delta=0{,}05$, tại năm mức $\epsilon$; hai cột $\epsilon=0{,}1$ và $0{,}05$ trùng bảng của ghi chú.

| $\epsilon$ | $0{,}2$ | $0{,}1$ | $0{,}05$ | $0{,}02$ | $0{,}01$ |
|---|---|---|---|---|---|
| khả diễn $\lceil\ln(2000)/\epsilon\rceil$ | $39$ | $77$ | $153$ | $381$ | $761$ |
| bất khả diễn $\lceil2\ln(4000)/\epsilon^2\rceil$ | $415$ | $1659$ | $6636$ | $41\,471$ | $165\,881$ |

Tính lại: $7{,}6009/0{,}2=38{,}0\to39$; $7{,}6009/0{,}02=380{,}05\to381$; $7{,}6009/0{,}01=760{,}09\to761$; $16{,}588/0{,}04=414{,}7\to415$; $16{,}588/0{,}0004=41\,470{,}2\to41\,471$; $16{,}588/0{,}0001=165\,880{,}99\to165\,881$. Trên trục log–log, đường khả diễn dốc $-1$, đường bất khả diễn dốc $-2$.

**V20. Bài tập 02.8(c)(d)** (6-07; số và kết quả của `exercises.md`). $p=10$, $K=3^{10}+1=59\,050$. Khả diễn: $\ln59\,050+\ln20=10{,}9861+2{,}9957=13{,}9819$, $/0{,}1=139{,}8\to140$; $/0{,}05=279{,}6\to280$. Bất khả diễn: $2K/\delta=2\,362\,000$, $\ln=14{,}6750$, $2\cdot14{,}6750/0{,}01=2935{,}004\to2936$; $/0{,}0025$: $11\,740{,}02\to11\,741$. Tỉ số: $280/140=2$; $11\,741/2936=4{,}0$.

**V21. Giá của số ứng viên với Chebyshev** (§9). $K/(4\delta\epsilon^2)=1000/(4\cdot0{,}05\cdot0{,}0025)=1000/0{,}0005=2\,000\,000$; so với $2120$ (Ví dụ 02.12, $K=1000$, $\epsilon=0{,}05$, cột ước lượng).

**V22. Bài tập 02.11(b)** (7-03; số và kết quả của `exercises.md`). $(b-a)^2=16$; $\ln240=5{,}4806$; $2\cdot16\cdot5{,}4806/0{,}01=17\,538{,}04\to17\,539$; $17\,538{,}04=16\cdot1096{,}13$. Kiểm tra của lời giải: $m=17\,539$ cho $2\cdot4\sqrt{\ln240/35\,078}=0{,}099997\le0{,}1$.

**V23. Câu hỏi cuối buổi** (§11; trang 7-04). $K=200$, $m=2000$, $\delta=0{,}05$: $\ln4000=8{,}2940$; $r_m^{+}=\sqrt{8{,}2940/4000}=\sqrt{0{,}0020735}=0{,}04554$; cận $0{,}08+0{,}0455=0{,}1255\approx0{,}126$.

## 6. Danh sách trang

**Ghi chú của người viết deck (2026-11-15):** mã trang trong tệp này đã đổi theo deck cuối (bảng đổi mã ở mục 15). Mặt trang trong mục này là bản dự kiến; mặt trang chốt là deck `lecture-02-bat-dang-thuc-tap-trung.html`, và mọi chỗ lệch có lý do ở mục 15.

Mỗi mục: ID, tiêu đề, loại, thời lượng; **Mặt trang** (các dòng dự kiến, theo thứ tự; `[f]` là fragment); **Ghi chú diễn giả** (ý chính, 40–150 âm tiết, đến ~250 cho trang ý tưởng chứng minh; viết cho giảng viên và người học, không mã trang, mã ví dụ của storyboard, câu quy trình hay nguồn gốc; luôn kết thúc bằng dòng `note-source`); **Lý do / nối**; **Mục tiêu / nguồn**. Câu trên mặt trang là bản dự kiến đã tự kiểm theo `no-ai-slop` (chế độ Edit) và `eval.md`; người viết deck có thể rút gọn, không thêm khẳng định.

Quy ước chung cho người viết deck:
- Trang kết quả: "Giả thiết:" và "Bảo đảm:" (nhãn của ghi chú), trích số khối của ghi chú một lần.
- Trang tổng quan (bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm") viết bằng lời, không kí hiệu, không tiếng Anh. Lần đầu một thuật ngữ trên trang nội dung có tiếng Anh trong ngoặc (bảng mục 10).
- Mọi kí hiệu trên mặt trang đã có ở trang trước hoặc có dòng "Nhắc lại:" (bảng đối chiếu mục 12 ghi chỗ đưa vào).
- Số thập phân dùng dấu phẩy KaTeX `0{,}2`; dãy số ngăn bằng `;\ `; số từ năm chữ số tách nhóm bằng `\,`.
- Mỗi trang ví dụ mở bằng dữ kiện dạng danh sách, không câu dẫn. "Diễn giải:" chỉ dùng số có trên chính trang đó.
- Không `\text{}` chứa tiếng Việt trong KaTeX.

### Mạch 1. Mở đầu (6 trang, 8 phút)

#### `1-01` Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn — bìa, điểm vào mạch 1 · 1 phút
- **Mặt trang:** h1 tên bài; h3 "Bài 02"; luận điểm (mục 2, bằng lời); "Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1"; "Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN".
- **Ghi chú diễn giả:** Luận điểm có ba phần: độc lập và bị chặn là hai giả thiết của mọi cận trong bài; "với xác suất cao" là bảo đảm theo tập huấn luyện, như trong định nghĩa học PAC của Bài 01; "lôgarit của số giả thuyết" là giá của việc chọn giả thuyết theo chính tập huấn luyện. Bài 01 cho đẳng thức $\mathbb E_S[L_S(h)]=L_D(h)$ với $h$ cố định; bài này chặn độ lệch trên một tập huấn luyện cụ thể. Nguồn: ghi chú Bài 02, đoạn mở đầu; Định lý 02.14; §9.
- **Lý do / nối:** luận điểm cả bài → tiên quyết.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu, Định lý 02.14, §9.

#### `1-02` Tiên quyết và quy ước — mở đầu · 1,5 phút
- **Mặt trang:**
  - **Nhắc lại:** $\mathbb E_S[L_S(h)]=L_D(h)$ khi $h$ chọn trước khi lấy mẫu (Mệnh đề 01.7); học PAC khả diễn và bất khả diễn (Định nghĩa 01.18, 01.25).
  - **Nhắc lại:** bất đẳng thức hợp (union bound) $\Pr\big(\bigcup_kB_k\big)\le\sum_k\Pr(B_k)$; chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$.
  - **Nhắc lại:** $\operatorname{Var}V=\mathbb EV^2-(\mathbb EV)^2$; phân bố Bernoulli (Bernoulli distribution) $\mathrm{Bernoulli}(q)$; tổng $m$ biến độc lập có phân bố nhị thức (binomial distribution) $\mathrm{Bin}(m;q)$.
  - **Ký hiệu:** $K=\lvert\mathcal H\rvert$; $\ln$ là lôgarit tự nhiên; ERM: tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization); PAC: học xấp xỉ với xác suất cao (probably approximately correct).
  - ≈ 58 âm tiết.
- **Ghi chú diễn giả:** Ba câu ôn nhanh của ghi chú được dùng lại: phương sai Bernoulli $q(1-q)\le\tfrac14$ (cận Chebyshev không phụ thuộc phân bố và bổ đề Hoeffding); phương sai của trung bình hai bản sao giữ nguyên $\sigma^2$, của hai biến độc lập là $\sigma^2/2$ (vai trò của tính độc lập); cực tiểu của $-\tau\epsilon+\tau^2/(8m)$ tại $\tau=4m\epsilon$ (chọn tham số trong bất đẳng thức Hoeffding). Từ giải tích: đồ thị hàm lồi nằm dưới dây cung (chord) và khai triển Taylor với phần dư Lagrange. Nguồn: ghi chú Bài 02, Kiến thức tiên quyết, Câu hỏi ôn nhanh.
- **Lý do / nối:** mọi kết quả Bài 01 dùng trên mặt trang được nhắc lại ở đây; giải nghĩa hai chữ viết tắt trước khi "Mục tiêu" dùng → mục tiêu.
- **Mục tiêu / nguồn:** tất cả; Kiến thức tiên quyết.

#### `1-03` Mục tiêu — mở đầu · 1 phút
- **Mặt trang** (danh sách đánh số, bằng lời, không kí hiệu, ≈ 78 âm tiết, trần 80):
  1. Chứng minh các bất đẳng thức Markov, Chebyshev và Hoeffding.
  2. So sánh xác suất đuôi chính xác với cận Chebyshev và cận Hoeffding; dựng cận tin cậy cho rủi ro kì vọng.
  3. Chứng minh cận hội tụ đều trên lớp hữu hạn và suy ra bảo đảm cho mọi nghiệm ERM.
  4. Tính cỡ mẫu đủ trong trường hợp bất khả diễn và khả diễn; giải thích vì sao hai cỡ mẫu tăng theo hai tốc độ khác nhau khi độ chính xác tăng.
  5. Dựng phản ví dụ khi bỏ tính độc lập, tính bị chặn hoặc số ứng viên trong bất đẳng thức hợp.
- **Ghi chú diễn giả:** Năm mục tiêu rút gọn từ sáu mục tiêu của ghi chú; mục tiêu 4 và 5 của ghi chú gộp thành mục tiêu 4. Cỡ mẫu bất khả diễn tăng theo bình phương nghịch đảo của độ chính xác, cỡ mẫu khả diễn theo nghịch đảo. Bài tập 02.1–02.11 ghi mục tiêu tương ứng trong tệp bài tập. Nguồn: ghi chú Bài 02, Mục tiêu học tập, §10.
- **Lý do / nối:** tiêu chí kiểm tra → nội dung.
- **Mục tiêu / nguồn:** tất cả; Mục tiêu học tập.

#### `1-04` Nội dung — mở đầu · 0,5 phút
- **Mặt trang:** `ol start="2"` với liên kết `#/2`…`#/7`: 2. Xác suất đuôi và bất đẳng thức Markov, Chebyshev; 3. Phương pháp Chernoff và bất đẳng thức Hoeffding; 4. Cận tin cậy cho một giả thuyết cố định; 5. Hội tụ đều và rủi ro vượt mức trên lớp hữu hạn; 6. Lớp hữu hạn trong trường hợp khả diễn; 7. Tổng kết. Dòng đọc trước: "Đọc trước: UML Phụ lục B.1–B.2; §2.3.1."
- **Ghi chú diễn giả:** Mạch 2 và 3 dựng các cận đuôi cho trung bình của các biến độc lập; mạch 4 áp dụng chúng cho một giả thuyết chọn trước; mạch 5 chuyển sang giả thuyết chọn theo tập huấn luyện bằng bất đẳng thức hợp; mạch 6 xét trường hợp lớp giả thuyết có một hàm không lỗi. Nguồn: ghi chú Bài 02; §12.
- **Lý do / nối:** bản đồ mạch → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §12.

#### `1-05` Vấn đề trung tâm — mở đầu · 1 phút
- **Mặt trang:** một hộp `div.box`: "Câu hỏi: trên một lớp giả thuyết hữu hạn, cần bao nhiêu quan sát để rủi ro thực nghiệm nằm gần rủi ro kì vọng, cho giả thuyết chọn trước và cho giả thuyết chọn theo chính tập huấn luyện?" (≈ 37 âm tiết).
- **Ghi chú diễn giả** (câu trả lời theo mạch, không trên mặt trang): (2) cận Chebyshev không phụ thuộc phân bố cần cỡ mẫu tăng như $1/\delta$; (3) với biến độc lập trong $[a,b]$, xác suất lệch ít nhất $\epsilon$ không quá $2e^{-2m\epsilon^2/(b-a)^2}$; (4) với $h$ cố định, $m\ge\ln(2/\delta)/(2\epsilon^2)$ đủ; (5) với giả thuyết chọn trong $K$ ứng viên, thay $\ln(2/\delta)$ bằng $\ln(2K/\delta)$, và mọi nghiệm ERM có rủi ro vượt mức không quá $\epsilon$ khi $m\ge2\ln(2K/\delta)/\epsilon^2$; (6) khi lớp giả thuyết khả diễn, $m\ge\ln(K/\delta)/\epsilon$ đủ. Nguồn: ghi chú Bài 02, đoạn mở đầu, §4–§8.
- **Lý do / nối:** một vấn đề cốt lõi → câu hỏi mở đầu làm cụ thể vấn đề.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu.

#### `1-06` Ví dụ: tỉ lệ lỗi 5% trên tập xác thực — ví dụ dẫn nhập · 3 phút
- **Mặt trang:**
  - Một hàm phân lớp (classifier) $h$, huấn luyện trên một tập dữ liệu khác.
  - Tập xác thực (validation set) $S$: $m=1000$ quan sát, độc lập với tập huấn luyện.
  - Tỉ lệ lỗi trên $S$: $L_S(h)=0{,}05$; độ tin cậy (confidence) $95\%$.
  - **Câu hỏi:** rủi ro kì vọng $L_D(h)$ có thể lớn đến đâu?
  - **Câu hỏi:** câu trả lời thay đổi thế nào nếu $h$ được chọn trong $1000$ ứng viên (candidate) vì có tỉ lệ lỗi nhỏ nhất trên chính $S$?
  - ≈ 58 âm tiết.
- **Ghi chú diễn giả:** Đây là câu hỏi mở đầu của ghi chú. Khi lấy điều kiện theo tập huấn luyện, $K$ ứng viên là một lớp giả thuyết hữu hạn cố định đối với tập xác thực, và chọn ứng viên có tỉ lệ lỗi nhỏ nhất là ERM trên lớp đó. Mệnh đề 01.7 chỉ nói kì vọng của $L_S(h)$ bằng $L_D(h)$; một tỉ lệ lỗi $5\%$ cụ thể có thể lệch khỏi $L_D(h)$. Câu hỏi thứ hai khó hơn: hàm được chọn vì tỉ lệ lỗi của nó thấp, nên tỉ lệ lỗi đó nghiêng về phía thấp. Mạch 4 trả lời câu thứ nhất, mạch 5 câu thứ hai. Nguồn: ghi chú Bài 02, Câu hỏi mở đầu; §3 (khối ứng dụng).
- **Lý do / nối:** ví dụ dẫn nhập trước mọi định nghĩa → tiêu đề mạch 2.
- **Mục tiêu / nguồn:** 2, 3; Câu hỏi mở đầu, §3.

### Mạch 2. Xác suất đuôi và bất đẳng thức Markov, Chebyshev (7 trang, 15,5 phút)

#### `2-00` 2. Xác suất đuôi và bất đẳng thức Markov, Chebyshev — tiêu đề mạch, điểm vào mạch 2 · 0,5 phút
- **Mặt trang:** "2."; h2 tên mạch; `p.strand-lead` (bảng mạch); `p.strand-keys` "xác suất đuôi · cận đuôi · bất đẳng thức Markov · bất đẳng thức Chebyshev".
- **Ghi chú diễn giả:** Kế thừa: câu hỏi về một tỉ lệ lỗi $5\%$ và đẳng thức kì vọng của Bài 01. Nhiệm vụ: nêu các giả thiết của bài, tính xác suất đuôi khi biết phân bố, rồi chặn nó khi không biết phân bố bằng kì vọng và phương sai. Trao cho mạch 3: cận Chebyshev không phụ thuộc phân bố đúng nhưng chỉ giảm như $1/m$. Nguồn: ghi chú Bài 02, §1–§4.
- **Lý do / nối:** câu hỏi mở đầu → giả thiết.
- **Mục tiêu / nguồn:** 1, 2; §1–§4.

#### `2-01` Giả thiết và bốn đại lượng cần chặn — định nghĩa (khung) · 2 phút
- **Mặt trang:**
  - Bốn đại lượng cần chặn: $\lvert L_S(h)-L_D(h)\rvert$ với $h$ cố định; $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$;
  - rủi ro vượt mức (excess risk) $L_D(\hat h)-\min_{h\in\mathcal H}L_D(h)$; $L_D(\hat h)$ khi lớp giả thuyết khả diễn.
  - Bảng hai cột (Giả thiết | Nội dung):
    - (T1) | $Z_1,\ldots,Z_m$ độc lập cùng phân bố (i.i.d.) theo $D$
    - (T2), (T3) | $\ell(h,\cdot)$ đo được, $\ell(h,z)\in[0,1]$
    - (T4) | $\mathcal H$ hữu hạn, $K$ phần tử, chọn trước khi lấy mẫu
    - (O1) | $\hat h\in\arg\min_{h\in\mathcal H}L_S(h)$, mọi quy tắc chọn khi bằng nhau
  - ≈ 48 âm tiết.
- **Ghi chú diễn giả:** Bốn đại lượng theo thứ tự của bài: độ lệch của một giả thuyết cố định, độ lệch đồng thời trên cả lớp, rủi ro vượt mức của nghiệm ERM và rủi ro của nó khi lớp khả diễn. Giá trị nhỏ nhất $\min_{h}L_D(h)$ tồn tại vì lớp hữu hạn. Cố định: $D$, $\mathcal H$, $\ell$, mỗi $h$, $L_D(h)$; ngẫu nhiên theo $S$: $L_S(h)$, độ lệch đồng thời, $\hat h$, $L_D(\hat h)$. Dạng yếu của (T1) chỉ đòi mỗi $Z_i$ có phân bố $D$; Mệnh đề 01.7 chỉ cần dạng yếu. Giả thiết (O2) cho phép nghiệm ERM xấp xỉ sai $\epsilon_{\mathrm{opt}}$. Nguồn: ghi chú Bài 02, §1, §2.
- **Lý do / nối:** nhãn (T1)–(T4), (O1) dùng trên mọi trang kết quả → ví dụ xuyên suốt.
- **Mục tiêu / nguồn:** 1–4; §1, §2.

#### `2-02` Ví dụ: sàng lọc với dữ liệu có nhiễu — ví dụ (ví dụ xuyên suốt) · 2,5 phút
- **Mặt trang:**
  - $\mathcal X=\{1,\ldots,5\}$, $D_{\mathcal X}(x)=\tfrac15$; hàm ngưỡng $h_t(x)=\mathbb 1[x\ge t]$, $t=1,\ldots,6$, nên $K=6$.
  - $\eta(x)=\Pr(Y=1\mid X=x)$: $0;\ \tfrac14;\ \tfrac34;\ \tfrac25;\ 1$ tại $x=1,\ldots,5$.
  - Bảng: $t$ | $1$ … $6$; $L_{D_\eta}(h_t)$ | $0{,}52$ | $0{,}32$ | $\mathbf{0{,}22}$ | $0{,}32$ | $0{,}28$ | $0{,}48$.
  - Hàm lỗi 0–1 (0–1 loss): $\ell_{0\text{-}1}(h_3,Z)\sim\mathrm{Bernoulli}(0{,}22)$, nên $mL_S(h_3)\sim\mathrm{Bin}(m;0{,}22)$.
  - **Nhắc lại:** $S_\eta=((1,0),(2,0),(2,1),(3,1),(4,0),(5,1))$ (Bài 01) cho $L_{S_\eta}(h_3)=\tfrac13$, lệch $0{,}1133$ khỏi $0{,}22$.
  - ≈ 42 âm tiết.
- **Ghi chú diễn giả:** Đây là ví dụ sàng lọc của Bài 01 với phân bố có nhiễu $D_\eta$. Hàm $h_3$ cố định, không phụ thuộc tập huấn luyện, nên $\ell_{0\text{-}1}(h_3,Z_i)$ là các lần thử Bernoulli độc lập với xác suất sai $0{,}22$ và rủi ro thực nghiệm là tỉ lệ thành công trong $m$ lần thử. Tập huấn luyện $S_\eta=((1,0),(2,0),(2,1),(3,1),(4,0),(5,1))$ cho tỉ lệ lỗi $\tfrac13$: kì vọng đúng bằng $0{,}22$ nhưng một tập cụ thể lệch $0{,}1133$. Nguồn: ghi chú Bài 02, §3, Ví dụ 02.1; §4 (đoạn đầu).
- **Lý do / nối:** dữ kiện xuyên suốt, nêu ngay dạng danh sách → xác suất lệch.
- **Mục tiêu / nguồn:** 2; Ví dụ 02.1.

#### `2-03` Xác suất đuôi của rủi ro thực nghiệm — trực quan, định nghĩa, ví dụ · 3 phút
- **Mặt trang:**
  - **Trực quan.** Khi $m$ tăng, phân bố của $L_S(h_3)$ dồn vào khoảng $(0{,}12;\ 0{,}32)$ quanh $0{,}22$ (hình F1).
  - Xác suất đuôi (tail probability) hai phía của $V$ tại $\epsilon$: $\Pr(\lvert V-\mathbb EV\rvert\ge\epsilon)$; cận đuôi (tail bound) là một cận trên của nó.
  - Với $V=L_S(h_3)$, $\epsilon=0{,}1$: $0{,}6189$; $0{,}0211$; $8{,}9\cdot10^{-4}$ tại $m=6$; $100$; $200$.
  - **Diễn giải:** ở $m=6$, tỉ lệ các tập huấn luyện có tỉ lệ lỗi lệch khỏi $0{,}22$ ít nhất $0{,}1$ là $0{,}6189$; ở $m=200$ chỉ còn $8{,}9\cdot10^{-4}$.
  - Hình F1 (`img/lec-02/tap-trung.svg`), cột phải `grid2` hoặc dưới.
  - ≈ 58 âm tiết.
- **Ghi chú diễn giả:** Có ba dạng xác suất đuôi: trên $\Pr(V-\mathbb EV\ge\epsilon)$, dưới $\Pr(V-\mathbb EV\le-\epsilon)$ và hai phía. Ở $m=6$, $L_S(h_3)=k/6$, và chỉ $k=1$ cho độ lệch dưới $0{,}1$ ($\lvert\tfrac16-0{,}22\rvert=0{,}0533$), nên xác suất đuôi là $1-6\cdot0{,}22\cdot0{,}78^5\approx0{,}6189$. Ở $m=100$ và $200$, biến cố đuôi gồm $k\le0{,}12m$ hoặc $k\ge0{,}32m$, và ta cộng các xác suất nhị thức. Các số này tính được vì đã biết $D_\eta$. Một cận đuôi có ích khi nó nhỏ hơn $1$ và tính được mà không cần biết phân bố. Đọc hình: ba biểu đồ cột của hàm xác suất của $L_S(h_3)$, cột trong khoảng $(0{,}12;\ 0{,}32)$ tô đặc, cột ngoài khoảng gạch chéo. Nguồn: ghi chú Bài 02, §4, Định nghĩa 02.1, Ví dụ 02.2; Phụ lục B.1.
- **Lý do / nối:** trực quan của tập trung độ đo trước mọi cận → cận chỉ dùng kì vọng.
- **Mục tiêu / nguồn:** 2; Định nghĩa 02.1, Ví dụ 02.2.

#### `2-04` Bất đẳng thức Markov và Chebyshev — trực quan, kết quả · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Phần $\{V\ge\alpha\}$ đóng góp ít nhất $\alpha\Pr(V\ge\alpha)$ vào $\mathbb EV$, nên $V$ không âm có kì vọng nhỏ thì $\Pr(V\ge\alpha)$ nhỏ.
  - **Bổ đề 02.2** (Markov). **Giả thiết:** $V\ge0$ hầu chắc chắn (almost surely), $\mathbb EV<\infty$, $\alpha>0$. **Bảo đảm:** display $\Pr(V\ge\alpha)\le\mathbb EV/\alpha$.
  - **Bổ đề 02.3** (Chebyshev). **Giả thiết:** $V_1,\ldots,V_m$ độc lập, $\operatorname{Var}V_i\le\sigma^2$, $\bar V_m=\frac1m\sum_iV_i$, $\bar\mu_m=\mathbb E\bar V_m$, $\epsilon>0$. **Bảo đảm:** display $\Pr(\lvert\bar V_m-\bar\mu_m\rvert\ge\epsilon)\le\sigma^2/(m\epsilon^2)$; với $m=1$: $\operatorname{Var}V/\epsilon^2$.
  - ≈ 58 âm tiết; hai công thức hiển thị.
- **Ghi chú diễn giả:** Ngưỡng $\alpha$ là ngưỡng cho chính $V$, khác với độ lệch $\epsilon$ khỏi kì vọng. Cận Markov chỉ dùng kì vọng của một biến không âm và giảm như $1/\alpha$. Chebyshev dùng thêm phương sai; phần (a) của ghi chú là trường hợp một biến, phần (b) là trung bình của $m$ biến độc lập, không cần cùng phân bố, với $\mu_i=\mathbb EV_i$ và $\bar\mu_m=\frac1m\sum_i\mu_i$. Với $V=L_S(h)$, cận Chebyshev giảm như $1/m$ vì phương sai của trung bình giảm như $1/m$. Nguồn: ghi chú Bài 02, §4, Bổ đề 02.2, 02.3.
- **Lý do / nối:** hai cận dùng mô-men, phát biểu gọn → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 1; Bổ đề 02.2, 02.3.

#### `2-05` Ý tưởng chứng minh: Markov và Chebyshev — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** (danh sách đánh số)
  - 1. Từng điểm: $\alpha\,\mathbb 1[V\ge\alpha]\le V$ (hình F2); lấy kì vọng rồi chia cho $\alpha$.
  - 2. Chebyshev: $\{\lvert V-\mathbb EV\rvert\ge\epsilon\}=\{(V-\mathbb EV)^2\ge\epsilon^2\}$; áp dụng Markov cho $(V-\mathbb EV)^2$.
  - 3. Trung bình: $\operatorname{Var}\bar V_m=\frac1{m^2}\sum_i\operatorname{Var}V_i\le\sigma^2/m$.
  - Giả thiết vào: $V\ge0$ ở bước 1; độc lập chỉ ở bước 3, và chỉ cần không tương quan từng đôi (pairwise uncorrelated).
  - Cực biên: Markov xảy ra dấu bằng khi $V\in\{0,\alpha\}$ hầu chắc chắn.
  - Hình F2 (`img/lec-02/markov.svg`), cột phải `grid2`.
  - ≈ 52 âm tiết.
- **Ghi chú diễn giả** (~190 âm tiết): Lộ trình: so sánh hai biến ngẫu nhiên tại từng điểm, rồi lấy kì vọng. Trên $\{V\ge\alpha\}$ vế trái bằng $\alpha\le V$; trên $\{V<\alpha\}$ vế trái bằng $0\le V$, chỗ dùng $V\ge0$. Kì vọng bảo toàn thứ tự và $\mathbb E\,\mathbb 1[V\ge\alpha]=\Pr(V\ge\alpha)$. Chebyshev là Markov áp dụng cho biến không âm $(V-\mathbb EV)^2$ với ngưỡng $\epsilon^2$; cùng mẹo áp dụng Markov cho một hàm không âm của $V$ sẽ cho phương pháp Chernoff với hàm mũ. Bỏ tính độc lập ở bước 3: với hai bản sao $Z_2=Z_1$, phương sai của trung bình vẫn là $\sigma^2$, nên cận không giảm theo $m$. Biến $V$ nhận hai giá trị $0$ và $\alpha$ làm bất đẳng thức từng điểm thành đẳng thức, nên cận Markov không cải thiện được khi chỉ biết kì vọng; Bài tập 02.1(a) chứng minh dấu bằng xảy ra khi và chỉ khi $V\in\{0,\alpha\}$ hầu chắc chắn. Nguồn: ghi chú Bài 02, chứng minh Bổ đề 02.2, 02.3; Câu hỏi ôn nhanh 2; tệp bài tập, Bài tập 02.1(a).
- **Lý do / nối:** lộ trình, chỗ dùng giả thiết, cực biên → ví dụ bằng số.
- **Mục tiêu / nguồn:** 1, 5; chứng minh Bổ đề 02.2, 02.3.

#### `2-06` Ví dụ: cận Markov và Chebyshev cho rủi ro thực nghiệm của $h_3$ — ví dụ, cận bằng số · 2,5 phút
- **Mặt trang:**
  - Dữ kiện: $D_\eta$, $h_3$ cố định, $\epsilon=0{,}1$; $\operatorname{Var}L_S(h_3)=0{,}1716/m$.
  - Bảng (cột $m=6$ | $100$ | $200$):
    - Chính xác, hai phía | $0{,}6189$ | $0{,}0211$ | $8{,}9\cdot10^{-4}$
    - Chính xác, đuôi trên | $0{,}3937$ | $0{,}0134$ | $6{,}9\cdot10^{-4}$
    - Markov, đuôi trên | $0{,}6875$ | $0{,}6875$ | $0{,}6875$
    - Chebyshev, biết phương sai | $2{,}86$ | $0{,}1716$ | $0{,}0858$
    - Chebyshev, không phụ thuộc phân bố | $4{,}17$ | $0{,}25$ | $0{,}125$
  - Không phụ thuộc phân bố: $V\in[0,1]$ cho $\operatorname{Var}V\le\mu(1-\mu)\le\tfrac14$, cận $25/m$.
  - Cỡ mẫu: $25/m\le0{,}05$ khi $m\ge500$; cỡ mẫu Chebyshev tăng như $1/\delta$.
  - **Diễn giải:** cận Markov $0{,}6875$ không đổi theo $m$; ở $m=6$ hai cận Chebyshev $2{,}86$ và $4{,}17$ lớn hơn $1$.
  - ≈ 55 âm tiết.
- **Ghi chú diễn giả:** Markov dùng ngưỡng $\alpha=0{,}22+0{,}1=0{,}32$ cho đuôi trên, nên chỉ so được với hàng đuôi trên chính xác. Phương sai $0{,}22\cdot0{,}78=0{,}1716$ là phương sai Bernoulli của câu ôn nhanh 1. Ở $m=6$ cả hai cận Chebyshev lớn hơn $1$, nên không cho thông tin. Cận $25/m$ đúng cho mọi hàm lỗi nhận giá trị trong $[0,1]$ mà không cần biết $D$; điều kiện "$\le\delta$" cho $m\ge1/(4\delta\epsilon^2)$, tức cỡ mẫu tăng như $1/\delta$. Để cỡ mẫu tăng như $\ln(1/\delta)$, cần dùng thêm tính bị chặn. Nguồn: ghi chú Bài 02, Ví dụ 02.3; Phụ lục B.1.
- **Lý do / nối:** kiểm tra bằng số cho cụm Markov–Chebyshev; giới hạn $1/\delta$ → tiêu đề mạch 3.
- **Mục tiêu / nguồn:** 2; Ví dụ 02.3.

### Mạch 3. Phương pháp Chernoff và bất đẳng thức Hoeffding (6 trang, 19,5 phút)

#### `3-00` 3. Phương pháp Chernoff và bất đẳng thức Hoeffding — tiêu đề mạch, điểm vào mạch 3 · 0,5 phút
- **Mặt trang:** "3."; h2 tên mạch; `p.strand-lead`; `p.strand-keys` "hàm sinh mô-men · phương pháp Chernoff · bổ đề Hoeffding · dây cung".
- **Ghi chú diễn giả:** Kế thừa: cận Chebyshev không phụ thuộc phân bố, đúng nhưng chỉ giảm như $1/m$ và cần cỡ mẫu tăng như $1/\delta$. Nhiệm vụ: dùng thêm tính bị chặn $a\le V\le b$ qua hàm mũ $e^{\tau V}$, chứa mọi mô-men của $V$. Trao cho mạch 4: bất đẳng thức Hoeffding cho trung bình các biến độc lập, bị chặn. Nguồn: ghi chú Bài 02, §5.
- **Lý do / nối:** ví dụ Chebyshev → hàm sinh mô-men.
- **Mục tiêu / nguồn:** 1; §5.

#### `3-01` Hàm sinh mô-men và phương pháp Chernoff — định nghĩa, kỹ thuật (lần đầu trong học phần) · 3,5 phút
- **Mặt trang:**
  - Hàm sinh mô-men (moment generating function) của $V$: $\tau\mapsto\mathbb Ee^{\tau V}$; hữu hạn với mọi $\tau$ khi $a\le V\le b$. Ví dụ: $1-q+qe^{\tau}$ với $V\sim\mathrm{Bernoulli}(q)$.
  - **Kỹ thuật.** Phương pháp Chernoff (Chernoff method), Bổ đề 02.5: với mọi $\tau>0$ và tổng độc lập $V=\sum_{i=1}^mV_i$,
  - display $\Pr(V\ge\alpha)\le e^{-\tau\alpha}\,\mathbb Ee^{\tau V}=e^{-\tau\alpha}\prod_{i=1}^m\mathbb Ee^{\tau V_i}$.
  - Dùng khi: cần cận đuôi của một tổng các biến độc lập; chặn từng thừa số, rồi chọn $\tau$ làm nhỏ nhất vế phải.
  - Dùng ở: bước đầu là Markov cho hàm tăng $x\mapsto e^{\tau x}$; Chebyshev dùng cùng bước với $x\mapsto x^2$.
  - ≈ 60 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Bổ đề 02.5 có hai phần tất định. (a): với $\tau>0$, $\{V\ge\alpha\}=\{e^{\tau V}\ge e^{\tau\alpha}\}$, và Markov cho biến không âm $e^{\tau V}$ cho cận; nếu $\mathbb Ee^{\tau V}=\infty$ cận đúng tầm thường. (b): các $e^{\tau V_i}$ độc lập, không âm, nên kì vọng của tích bằng tích các kì vọng; tính độc lập chỉ dùng ở đây. Khi bỏ tính bị chặn, hàm sinh mô-men có thể bằng $\infty$: với $\Pr(V=j)=c/j^3$, $j=1,2,\ldots$, kì vọng hữu hạn nhưng $\mathbb Ee^{\tau V}=\infty$ với mọi $\tau>0$. Phương pháp này còn dùng ở các bài sau của học phần. Nguồn: ghi chú Bài 02, §5, Định nghĩa 02.4, Bổ đề 02.5 và chứng minh; UML Phụ lục B.3, B.4.
- **Lý do / nối:** kỹ thuật dùng lại qua học phần, đặt ở nơi dùng lần đầu; Bổ đề 02.5 là công cụ, phát biểu và chứng minh hai dòng nằm chung trang kỹ thuật (mục 11, điểm 3) → còn thiếu cận cho từng thừa số.
- **Mục tiêu / nguồn:** 1; Định nghĩa 02.4, Bổ đề 02.5.

#### `3-02` Bổ đề Hoeffding — trực quan, kết quả, ví dụ · 3,5 phút
- **Mặt trang:**
  - **Trực quan.** Trong các biến trên $[a,b]$ có cùng kì vọng, biến chỉ nhận hai giá trị $a$, $b$ làm $\mathbb Ee^{\tau(V-\mathbb EV)}$ lớn nhất (hình F3).
  - **Bổ đề 02.6** (bổ đề Hoeffding, Hoeffding's lemma). **Giả thiết:** $a\le V\le b$ hầu chắc chắn, $a<b$. **Bảo đảm:** với mọi $\tau\in\mathbb R$, display $\mathbb Ee^{\tau(V-\mathbb EV)}\le\exp\big(\tau^2(b-a)^2/8\big)$.
  - **Ví dụ.** $V=\ell_{0\text{-}1}(h_3,Z)\sim\mathrm{Bernoulli}(0{,}22)$, $\tau=2$: vế trái $0{,}78e^{-0{,}44}+0{,}22e^{1{,}56}\approx1{,}549$, vế phải $e^{0{,}5}\approx1{,}649$.
  - Hình F3 (`img/lec-02/day-cung.svg`), cột phải `grid2`.
  - ≈ 45 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Vế trái là một kì vọng, nên bảo đảm là tất định; vế phải chỉ phụ thuộc độ dài $b-a$. Đọc hình: đường cong $e^{2w}$ trên đoạn $[-0{,}22;\ 0{,}78]$, ứng với $W=V-0{,}22$, và dây cung nối hai đầu mút; tại $w=0$ dây cung có độ cao $1{,}549$, bằng vế trái của ví dụ, vì biến Bernoulli chỉ nhận hai giá trị tại hai đầu mút; vạch ngang tại $1{,}649$ là vế phải. Một biến bất kì trên $[0,1]$ với kì vọng $0{,}22$ có $\mathbb Ee^{2W}$ không quá độ cao dây cung tại $w=0$. Nguồn: ghi chú Bài 02, §5, Bổ đề 02.6; ví dụ sàng lọc (Ví dụ 02.1); UML Phụ lục B.4.
- **Lý do / nối:** thừa số còn thiếu của phương pháp Chernoff; trực quan bằng hình và một biến của ví dụ xuyên suốt → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 1; Bổ đề 02.6.

#### `3-03` Ý tưởng chứng minh: bổ đề Hoeffding — ý tưởng chứng minh · 4 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** (danh sách đánh số)
  - 1. Đưa về kì vọng $0$: $W=V-\mathbb EV\in[a',b']$, $a'\le0\le b'$, $b'-a'=b-a$.
  - 2. Dây cung (chord): $e^{\tau w}$ lồi trên $[a',b']$; lấy kì vọng với $\mathbb EW=0$ được $\mathbb Ee^{\tau W}\le e^{\varphi(u)}$, với $u=\tau(b-a)$, $\theta=-a'/(b-a)$, $\varphi(u)=-\theta u+\ln(1-\theta+\theta e^u)$.
  - 3. $\varphi(0)=\varphi'(0)=0$; $\varphi''(u)$ là phương sai của một biến Bernoulli, nên $\varphi''\le\tfrac14$.
  - 4. Taylor tại $0$ với phần dư Lagrange: $\varphi(u)\le u^2/8$.
  - **Kỹ thuật.** Chặn hàm lồi bằng dây cung, rồi chặn một hàm một biến bằng Taylor bậc hai tại $0$.
  - Giả thiết vào: tính bị chặn ở bước 2; bỏ nó thì hàm sinh mô-men có thể bằng $\infty$.
  - ≈ 58 âm tiết; không công thức hiển thị.
- **Ghi chú diễn giả** (~210 âm tiết): Lộ trình: đưa về biến có kì vọng $0$, chặn hàm mũ bằng dây cung, rồi chặn một hàm của một biến thực. Ở bước 2, vế phải sau khi lấy kì vọng là $\big(b'e^{\tau a'}-a'e^{\tau b'}\big)/(b'-a')$; đặt $\theta=-a'/(b'-a')\in[0,1]$, nó bằng $e^{\varphi(u)}$ với $\varphi(u)=-\theta u+\ln(1-\theta+\theta e^u)$. Ở bước 3, $\rho(u)=\theta e^u/(1-\theta+\theta e^u)\in[0,1]$ và $\varphi'=-\theta+\rho$, nên $\varphi''=\rho(1-\rho)$ là phương sai của một biến Bernoulli tham số $\rho(u)$, không quá $\tfrac14$ theo câu ôn nhanh 1. Hằng số $\tfrac18=\tfrac12\cdot\tfrac14$: hệ số Taylor nhân cận phương sai. Trường hợp cực biên là biến hai điểm tại $a$, $b$: bước 2 thành đẳng thức. Mẹo dây cung và Taylor chỉ dùng trong chứng minh này. Chi tiết của bước 3–4 ở Phụ lục A của ghi chú. Nguồn: ghi chú Bài 02, chứng minh Bổ đề 02.6 (phác thảo); Phụ lục A.
- **Lý do / nối:** lộ trình bốn bước, giả thiết vào ở bước 2 → ghép với phương pháp Chernoff.
- **Mục tiêu / nguồn:** 1, 5; chứng minh Bổ đề 02.6, Phụ lục A.

#### `3-04` Bất đẳng thức Hoeffding — trực quan, kết quả, cận bằng số · 3,5 phút
- **Mặt trang:**
  - **Trực quan.** Mỗi thừa số của tích Chernoff được bổ đề Hoeffding chặn qua $b-a$, nên cận chỉ dùng phân bố qua độ dài miền giá trị.
  - **Định lý 02.7** (bất đẳng thức Hoeffding, Hoeffding's inequality). **Giả thiết:** $V_1,\ldots,V_m$ độc lập, không cần cùng phân bố; $a\le V_i\le b$ hầu chắc chắn; $\epsilon>0$.
  - **Bảo đảm:** mỗi đuôi một phía không quá $\exp\big(-2m\epsilon^2/(b-a)^2\big)$; hai phía: display $\Pr(\lvert\bar V_m-\bar\mu_m\rvert\ge\epsilon)\le2\exp\big(-2m\epsilon^2/(b-a)^2\big)$.
  - **Ví dụ.** $L_S(h_3)$, $[a,b]=[0,1]$, $\epsilon=0{,}1$: $2e^{-2}\approx0{,}2707$ ở $m=100$; $2e^{-4}\approx0{,}0366$ ở $m=200$.
  - **Diễn giải:** nhân đôi $m$ thì thừa số $e^{-2}$ thành $e^{-4}=(e^{-2})^2$.
  - ≈ 55 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Cận giảm theo hàm mũ của $m\epsilon^2$ và không phụ thuộc phân bố của các $V_i$ ngoài miền giá trị, nên dùng được khi $D$ chưa biết. Khi các $V_i$ có miền $[a_i,b_i]$ khác nhau, cùng chứng minh cho số mũ $-2m^2\epsilon^2/\sum_i(b_i-a_i)^2$ (Nhận xét 02.8, Bài tập 02.2). Hàm lỗi có trọng số $\ell_c$ của ứng dụng sàng lọc với $(c_{FP},c_{FN})=(1,4)$ nhận giá trị trong $\{0,1,4\}\subset[0,4]$: định lý vẫn áp dụng, các cỡ mẫu nhân thêm $(b-a)^2=16$ và các bán kính nhân thêm $4$. Cỡ mẫu để cận hai phía không vượt $\delta$ là $(b-a)^2\ln(2/\delta)/(2\epsilon^2)$, tăng như $\ln(2/\delta)$. Nguồn: ghi chú Bài 02, §5, Định lý 02.7, Nhận xét 02.8, đoạn về $\ell_c$; UML Phụ lục B.4.
- **Lý do / nối:** kết quả chính của mạch; số của $h_3$ so được với bảng Chebyshev → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 1, 2; Định lý 02.7.

#### `3-05` Ý tưởng chứng minh: bất đẳng thức Hoeffding — ý tưởng chứng minh · 4,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** (danh sách đánh số)
  - 1. Phương pháp Chernoff cho $\bar V_m-\bar\mu_m=\sum_i(V_i-\mu_i)/m$ tại mức $\epsilon$; tách tích theo tính độc lập.
  - 2. Bổ đề Hoeffding cho từng thừa số với tham số $\tau/m$:
  - display $\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\le\exp\Big(-\tau\epsilon+\dfrac{\tau^2(b-a)^2}{8m}\Big)$.
  - 3. Chọn $\tau=4m\epsilon/(b-a)^2$: số mũ bằng $-2m\epsilon^2/(b-a)^2$.
  - 4. Đuôi dưới: áp dụng cho $-V_i\in[-b,-a]$; hai phía: hợp hai biến cố rời nhau.
  - Giả thiết vào: độc lập ở bước 1, bị chặn ở bước 2; không bước nào dùng tính cùng phân bố.
  - ≈ 55 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả** (~200 âm tiết): Lộ trình: Chernoff, tách tích, chặn từng thừa số, chọn $\tau$. Số mũ ở bước 2 là một hàm bậc hai lồi của $\tau$; câu ôn nhanh 3 cho điểm nhỏ nhất $\tau=4m\epsilon$ khi $b-a=1$, và hệ số $(b-a)^2$ chỉ đổi thang. Thay vào: $-\tau\epsilon=-4m\epsilon^2/(b-a)^2$ và $\tau^2(b-a)^2/(8m)=2m\epsilon^2/(b-a)^2$. Đoạn $[-b,-a]$ có cùng độ dài $b-a$, nên đuôi dưới có cùng cận. Hai biến cố đuôi trên và dưới rời nhau vì $\epsilon>0$, nên cận hai phía là tổng hai cận, có hệ số $2$. Bỏ độc lập: nếu mọi quan sát là bản sao của một quan sát, kì vọng của tích không tách được, và kết luận sai; phần cận tin cậy cho phản ví dụ bằng số. Bỏ bị chặn: bổ đề Hoeffding không áp dụng. Nguồn: ghi chú Bài 02, chứng minh Định lý 02.7; Câu hỏi ôn nhanh 3; UML Phụ lục B.4.
- **Lý do / nối:** lộ trình, chỗ dùng hai giả thiết → tiêu đề mạch 4 áp dụng cho rủi ro thực nghiệm.
- **Mục tiêu / nguồn:** 1, 5; chứng minh Định lý 02.7.

### Mạch 4. Cận tin cậy cho một giả thuyết cố định (8 trang, 19,5 phút)

#### `4-00` 4. Cận tin cậy cho một giả thuyết cố định — tiêu đề mạch, điểm vào mạch 4 · 0,5 phút
- **Mặt trang:** "4."; h2 tên mạch; `p.strand-lead`; `p.strand-keys` "cận trên tin cậy · khoảng tin cậy · bán kính tin cậy · cỡ mẫu".
- **Ghi chú diễn giả:** Kế thừa: bất đẳng thức Hoeffding cho trung bình các biến độc lập, bị chặn. Nhiệm vụ: áp dụng nó cho rủi ro thực nghiệm của một giả thuyết chọn trước, biến cận đuôi thành một khoảng báo cáo được, rồi chỉ ra kết luận sai khi bỏ tính độc lập hoặc tính bị chặn. Trao cho mạch 5: bán kính $\sqrt{\ln(2/\delta)/(2m)}$ chỉ đúng cho $h$ không phụ thuộc $S$. Nguồn: ghi chú Bài 02, §5.
- **Lý do / nối:** mạch 3 → định nghĩa đối tượng cần báo cáo.
- **Mục tiêu / nguồn:** 2; §5.

#### `4-01` Cận tin cậy và khoảng tin cậy — định nghĩa, trực quan, câu hỏi · 3 phút
- **Mặt trang:**
  - Cho $\ell$ thỏa (T3), $h$ cố định, $\delta\in(0,1)$.
  - Cận trên tin cậy (upper confidence bound) mức $1-\delta$: một hàm đo được $\overline L_\delta$ của tập huấn luyện sao cho với mọi $D$, display $\Pr_{S\sim D^m}\big[L_D(h)\le\overline L_\delta(S)\big]\ge1-\delta$.
  - Khoảng tin cậy (confidence interval): $\underline L_\delta(S)\le L_D(h)\le\overline L_\delta(S)$ với xác suất ít nhất $1-\delta$, với mọi $D$.
  - **Ý nghĩa:** đầu mút ngẫu nhiên, $L_D(h)$ cố định; với $\delta=0{,}05$, trong $100$ lần lấy mẫu có khoảng $95$ lần khoảng chứa $L_D(h)$.
  - **Câu hỏi:** hàm $S\mapsto L_S(h)$ có là cận trên tin cậy mức $0{,}95$ không?
  - `[f]` Không: dưới $D_\eta$, $m=100$, biến cố $L_{D_\eta}(h_3)\le L_S(h_3)$ có xác suất $\approx0{,}539$.
  - ≈ 60 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Lượng từ "với mọi $D$" đứng sau hàm: hàm được chọn trước và không biết $D$. Hàm hằng $\overline L_\delta\equiv1$ là cận trên tin cậy ở mọi mức vì $L_D(h)\le1$ theo (T3), nhưng không cho thông tin. Cận trên tin cậy là một cận một phía (one-sided bound), khoảng tin cậy là một cận hai phía (two-sided bound). Xác suất $0{,}539$ là $\Pr(\mathrm{Bin}(100;0{,}22)\ge22)$, nhỏ hơn nhiều so với $0{,}95$; cần cộng thêm một bán kính. Nguồn: ghi chú Bài 02, §5, Định nghĩa 02.9 và hai đoạn sau.
- **Lý do / nối:** câu hỏi mở đầu đòi một cận báo cáo được; câu hỏi trên trang chỉ ra vì sao cần bán kính → Hệ quả 02.10.
- **Mục tiêu / nguồn:** 2; Định nghĩa 02.9.

#### `4-02` Cận tin cậy Hoeffding cho một giả thuyết cố định — trực quan, kết quả · 3 phút
- **Mặt trang:**
  - **Trực quan.** Bán kính tin cậy (confidence radius) giảm như $1/\sqrt m$: gấp bốn cỡ mẫu thì bán kính giảm một nửa.
  - **Hệ quả 02.10.** **Giả thiết:** (T1), (T2), (T3); $h$ cố định, không phụ thuộc $S$; $\delta\in(0,1)$.
  - **Bảo đảm** (xác suất theo $S\sim D^m$, mọi $D$):
    - (a) $\Pr\big(\lvert L_S(h)-L_D(h)\rvert\ge\epsilon\big)\le2e^{-2m\epsilon^2}$ với mọi $\epsilon>0$;
    - (b) khoảng tin cậy $L_S(h)\pm\sqrt{\ln(2/\delta)/(2m)}$; (c) cận trên tin cậy $L_S(h)+\sqrt{\ln(1/\delta)/(2m)}$;
    - (d) nếu $m\ge\ln(2/\delta)/(2\epsilon^2)$, thì $\lvert L_S(h)-L_D(h)\rvert\le\epsilon$ với xác suất ít nhất $1-\delta$.
  - ≈ 50 âm tiết.
- **Ghi chú diễn giả:** Bốn khẳng định chặn độ lệch giữa đại lượng thực nghiệm $L_S(h)$ và đại lượng tổng thể $L_D(h)$ với xác suất cao, không phụ thuộc $D$. Bán kính hai phía là $\sqrt{\ln(2/\delta)/(2m)}$, một phía là $\sqrt{\ln(1/\delta)/(2m)}$: đổi sang cận một phía chỉ đổi $\ln(2/\delta)$ thành $\ln(1/\delta)$, vì chỉ dùng một đuôi. Mạch 5 bỏ điều kiện "$h$ cố định". Nguồn: ghi chú Bài 02, §5, Hệ quả 02.10.
- **Lý do / nối:** kết quả trả lời trực tiếp câu hỏi mở đầu thứ nhất → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 2; Hệ quả 02.10.

#### `4-03` Ý tưởng chứng minh: cận tin cậy Hoeffding — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** (danh sách đánh số)
  - 1. Đặt $V_i=\ell(h,Z_i)$; vì $h$ cố định, $V_i$ chỉ phụ thuộc $Z_i$.
  - 2. (T1): các $V_i$ độc lập, $\mu_i=L_D(h)$; (T3): $V_i\in[0,1]$; do đó $\bar V_m=L_S(h)$, $\bar\mu_m=L_D(h)$.
  - 3. Định lý 02.7 với $[a,b]=[0,1]$ cho (a).
  - 4. Đặt cận bằng $\delta$ và giải theo bán kính; biến cố bù cho (b), (c), (d).
  - Bỏ "$h$ cố định": với $h$ chọn theo $S$, các $\ell(h,Z_i)$ phụ thuộc cả tập huấn luyện, bước 1 hỏng.
  - ≈ 55 âm tiết.
- **Ghi chú diễn giả** (~150 âm tiết): Lộ trình: áp dụng Định lý 02.7 cho giá trị của hàm lỗi trên từng quan sát, rồi giải phương trình "cận bằng $\delta$". Ba giả thiết vào ở bước 1–2: $h$ cố định để $V_i$ là hàm của riêng $Z_i$; (T1) để các $V_i$ độc lập và cùng kì vọng; (T3) để miền giá trị là $[0,1]$. Bán kính hai phía là nghiệm dương của $2e^{-2mr^2}=\delta$; bán kính một phía là nghiệm của $e^{-2mr^2}=\delta$ với đuôi dưới của Định lý 02.7. Phần (d) là điều kiện bán kính không vượt $\epsilon$. Khi $h$ được chọn theo $S$, tỉ lệ lỗi của $h$ nghiêng về phía thấp; mạch 5 đo độ nghiêng đó. Nguồn: ghi chú Bài 02, chứng minh Hệ quả 02.10.
- **Lý do / nối:** lộ trình và chỗ hỏng khi $h$ chọn theo tập huấn luyện → so sánh ba cận trên cùng ví dụ.
- **Mục tiêu / nguồn:** 2, 3; chứng minh Hệ quả 02.10.

#### (bỏ trang) Ví dụ: ba cách chặn cùng một xác suất đuôi — gộp vào ghi chú diễn giả của `3-04`
- **Lý do (người viết deck, 2026-11-15):** trang "Bài tập: hệ số hai trong bảo đảm của ERM" (`5-12`) phải dùng nguyên câu chữ Bài tập 02.3(a) (quyết định của điều phối viên, mục 11.8), câu này một mình đã 58 âm tiết nên cần một trang riêng; để giữ trần 55 trang, bỏ trang dư thừa nhất theo cổng duyệt (mục 3.1 của báo cáo cổng: "4-04 lặp hai hàng Chebyshev và hàng chính xác của 2-06"). Hàng Hoeffding ($0{,}2707$; $0{,}0366$) đã ở mặt trang `3-04`; thứ tự các cận, giao điểm $m\le107$ và tỉ số $8$, $12$, $13$ chuyển vào ghi chú diễn giả của `3-04`; Bước 4 của Ví dụ 02.4 (bảng cỡ mẫu theo $\delta$) vẫn ở trang kỹ thuật `4-04`.

#### `4-04` Đảo cận đuôi thành bán kính và cỡ mẫu — kỹ thuật (lần đầu trong học phần) · 2,5 phút
- **Mặt trang:**
  - **Kỹ thuật.** Đảo cận đuôi: từ một cận $g(m,r)$ của xác suất lệch ít nhất $r$, giải $g(m,r)=\delta$ được bán kính $r$; giải $r\le\epsilon$ được cỡ mẫu.
  - Hoeffding: display $\sqrt{\dfrac{\ln(2/\delta)}{2m}}\le\epsilon\iff m\ge\dfrac{\ln(2/\delta)}{2\epsilon^2}$.
  - Dùng khi: có cận đuôi giảm theo $m$ và $r$, cần báo cáo một bán kính hoặc một cỡ mẫu. Dùng ở: Hệ quả 02.10(b)–(d).
  - Bảng $\epsilon=0{,}1$ (cột $\delta$ | Chebyshev $1/(4\delta\epsilon^2)$ | Hoeffding): $0{,}05$ | $500$ | $185$; $0{,}001$ | $25\,000$ | $381$.
  - **Diễn giải:** giảm $\delta$ $50$ lần: cỡ mẫu Chebyshev gấp $50$, cỡ mẫu Hoeffding gấp khoảng $2$.
  - ≈ 60 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Hai giá trị Hoeffding: $\ln40/0{,}02\approx184{,}4$ làm tròn lên $185$, $\ln2000/0{,}02\approx380{,}05$ làm tròn lên $381$. Cỡ mẫu Chebyshev tăng như $1/\delta$, cỡ mẫu Hoeffding như $\ln(2/\delta)$; đó là lợi ích của tính bị chặn. Cùng kỹ thuật cho bán kính đồng thời của lớp hữu hạn, cỡ mẫu học PAC bất khả diễn và cỡ mẫu khả diễn trong bài này, và dùng lại ở các bài sau. Nguồn: ghi chú Bài 02, chứng minh Hệ quả 02.10 (Bước 3–5); Ví dụ 02.4, Bước 4.
- **Lý do / nối:** kỹ thuật dùng lại qua học phần, đặt ngay sau nơi dùng lần đầu (chứng minh Hệ quả 02.10); số lấy từ Bước 4 của Ví dụ 02.4 theo đúng thứ tự ghi chú → câu hỏi mở đầu thứ nhất.
- **Mục tiêu / nguồn:** 2, 4; Hệ quả 02.10, Ví dụ 02.4.

#### `4-05` Ví dụ: khoảng tin cậy cho hàm phân lớp có tỉ lệ lỗi 5% — ví dụ, trả lời câu hỏi mở đầu · 2 phút
- **Mặt trang:**
  - Dữ kiện: $h$ cố định trước khi xem tập xác thực $S$; $m=1000$; $L_S(h)=0{,}05$; $\delta=0{,}05$.
  - Hai phía: $\sqrt{\ln40/2000}\approx0{,}0429$; khoảng $[0{,}007;\ 0{,}093]$.
  - Một phía: $0{,}05+\sqrt{\ln20/2000}\approx0{,}05+0{,}0387=0{,}0887$.
  - **Diễn giải:** với độ tin cậy $95\%$, rủi ro kì vọng của hàm cố định không quá khoảng $8{,}9\%$, chặt hơn đầu mút $9{,}3\%$ của khoảng hai phía.
  - ≈ 45 âm tiết.
- **Ghi chú diễn giả:** Đây là câu trả lời cho câu hỏi mở đầu thứ nhất. Báo cáo một phía hợp với câu hỏi "rủi ro có thể lớn đến đâu"; khoảng hai phía tốn thêm vì chia $\delta$ cho hai đuôi. Với $\ln40\approx3{,}6889$ và $\ln20\approx2{,}9957$. Bảo đảm chỉ đúng khi $h$ được cố định trước khi xem $S$; câu hỏi thứ hai bỏ đúng điều kiện này. Nguồn: ghi chú Bài 02, Ví dụ 02.5.
- **Lý do / nối:** trả lời nửa đầu câu hỏi mở đầu → chỗ hỏng khi bỏ giả thiết.
- **Mục tiêu / nguồn:** 2; Ví dụ 02.5.

#### `4-06` Ví dụ: bỏ tính độc lập hoặc tính bị chặn — ví dụ (Ví dụ 02.6, Nhận xét 02.11), kiểm tra bỏ giả thiết · 3,5 phút
- **Mặt trang** (`grid2`, hai `card`):
  - Thẻ trái "Bản sao của một quan sát": $Z_1=\cdots=Z_m=Z\sim D_\eta$; $L_S(h_3)\in\{0,1\}$, $\mathbb EL_S(h_3)=0{,}22$; $\Pr\big(\lvert L_S(h_3)-0{,}22\rvert\ge0{,}2\big)=1$ với mọi $m$, trong khi $2e^{-2\cdot100\cdot0{,}04}=2e^{-8}\approx6{,}7\cdot10^{-4}$.
  - Thẻ phải "Hàm lỗi không bị chặn": $V_i$ độc lập, $\Pr(V_i=m^2)=1/m^2$, còn lại $V_i=0$, nên $\mathbb EV_i=1$; $\Pr(\bar V_m=0)\ge1-1/m$; Hoeffding trên $[0,m^2]$ với $\epsilon=1$ cho $2e^{-2/m^3}\approx2$.
  - **Lưu ý:** không có hàm $g(m,\epsilon)\to0$ chặn xác suất đuôi đồng thời cho mọi phân bố không âm có kì vọng $1$.
  - ≈ 60 âm tiết (trần; nếu vượt, tách thành hai trang và bỏ một trang ở mục 11, điểm 2).
- **Ghi chú diễn giả:** Thẻ trái: mỗi $Z_i$ vẫn có phân bố $D_\eta$, nên dạng yếu của (T1) thỏa và kì vọng vẫn là $0{,}22$; nhưng $L_S(h_3)$ không tập trung khi $m$ tăng. Chỗ hỏng là bước tách tích của phương pháp Chernoff: $\mathbb Ee^{\tau m\ell(h_3,Z)}=0{,}78+0{,}22e^{\tau m}$ lớn hơn $(0{,}78+0{,}22e^\tau)^m$ khi $\tau\ne0$, $m\ge2$, theo bất đẳng thức Jensen. Thẻ phải: ở $m=100$, $\Pr(\bar V_m=0)\approx0{,}9900$, và trên biến cố đó $\lvert\bar V_m-1\rvert=1$; cận Hoeffding đúng nhưng không cho thông tin. Với từng phân bố cố định, luật số lớn (law of large numbers) vẫn đúng; điều hỏng là tính đồng đều theo phân bố. Do đó mọi cận của lớp hữu hạn cần cả (T1) lẫn (T3). Nguồn: ghi chú Bài 02, Ví dụ 02.6, Nhận xét 02.11.
- **Lý do / nối:** hai phản ví dụ "bỏ giả thiết" của Định lý 02.7 và Hệ quả 02.10 (mục tiêu 5) → tiêu đề mạch 5.
- **Mục tiêu / nguồn:** 5; Ví dụ 02.6, Nhận xét 02.11.

### Mạch 5. Hội tụ đều và rủi ro vượt mức trên lớp hữu hạn (11 trang, 26,5 phút)

#### `5-00` 5. Hội tụ đều và rủi ro vượt mức trên lớp hữu hạn — tiêu đề mạch, điểm vào mạch 5 · 0,5 phút
- **Mặt trang:** "5."; h2 tên mạch; `p.strand-lead`; `p.strand-keys` "thiên lệch do chọn · tập đại diện · hội tụ đều · rủi ro vượt mức".
- **Ghi chú diễn giả:** Kế thừa: cận tin cậy Hoeffding cho một giả thuyết chọn trước khi lấy mẫu. Nhiệm vụ: chỉ ra cận đó không chuyển sang giả thuyết chọn theo $S$, dựng một cận đúng đồng thời cho cả lớp bằng bất đẳng thức hợp, rồi suy ra rủi ro vượt mức của mọi nghiệm ERM. Trao cho mạch 6: cỡ mẫu bất khả diễn $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$, tăng như $1/\epsilon^2$. Nguồn: ghi chú Bài 02, §6, §7.
- **Lý do / nối:** câu hỏi mở đầu thứ hai → ví dụ thiên lệch do chọn.
- **Mục tiêu / nguồn:** 3, 4; §6, §7.

#### `5-01` Ví dụ: thiên lệch do chọn trong 1000 ứng viên — ví dụ (vấn đề) · 3 phút
- **Mặt trang:**
  - $K=1000$ ứng viên $g_j(x)=x_j$ trên $\mathcal X=\{0,1\}^K$; nhãn $Y=0$ chắc chắn.
  - Các tọa độ của $X$ độc lập, mỗi tọa độ bằng $1$ với xác suất $0{,}07$; nên $L_D(g_j)=0{,}07$ với mọi $j$.
  - Tập xác thực $S\sim D^m$, $m=1000$, hàm lỗi 0–1.
  - Một ứng viên cố định: $\Pr\big(L_S(g_j)\le0{,}05\big)\approx0{,}00593$.
  - Ứng viên tốt nhất trên $S$: display $\Pr\big(\min_jL_S(g_j)\le0{,}05\big)=1-(1-0{,}00593)^{1000}\approx0{,}9974$.
  - **Diễn giải:** tỉ lệ lỗi của ứng viên được chọn lệch xuống dưới rủi ro kì vọng $0{,}07$; đó là thiên lệch do chọn (selection bias).
  - ≈ 60 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Mỗi $1000\,L_S(g_j)$ có phân bố $\mathrm{Bin}(1000;0{,}07)$. Tỉ lệ lỗi của $g_j$ chỉ phụ thuộc tọa độ thứ $j$ của các quan sát, và các tọa độ khác nhau độc lập, nên $K$ tỉ lệ lỗi độc lập và xác suất "có ít nhất một ứng viên đạt $5\%$" bằng một trừ tích. Một biến cố hiếm cho một ứng viên cố định, xác suất khoảng $0{,}6\%$, gần như chắc chắn xảy ra cho ứng viên được chọn. Xác suất của một biến cố tính cho $h$ cố định không chuyển sang $\hat h$. Nguồn: ghi chú Bài 02, §6, Ví dụ 02.7; Phụ lục B.2.
- **Lý do / nối:** vấn đề của Định lý 02.14 bằng con số, trước mọi định nghĩa → biến cố cần có xác suất cao.
- **Mục tiêu / nguồn:** 3; Ví dụ 02.7.

#### `5-02` Tập đại diện và biến cố hội tụ đều — định nghĩa, ví dụ · 1,5 phút
- **Mặt trang:**
  - Tập huấn luyện $s$ là $\epsilon$-đại diện ($\epsilon$-representative) đối với $(\mathcal H,\ell,D)$ nếu $\lvert L_s(h)-L_D(h)\rvert\le\epsilon$ với mọi $h\in\mathcal H$ (Định nghĩa 02.13).
  - Với $S\sim D^m$, biến cố "$S$ là $\epsilon$-đại diện" là biến cố hội tụ đều (uniform convergence event).
  - Bảng: $t$ | $1$ … $6$; $L_{S_\eta}(h_t)-L_{D_\eta}(h_t)$ | $-0{,}02$ | $0{,}0133$ | $0{,}1133$ | $0{,}18$ | $0{,}0533$ | $0{,}02$.
  - **Diễn giải:** $S_\eta$ là $\epsilon$-đại diện khi và chỉ khi $\epsilon\ge0{,}18$; nó không là $0{,}1$-đại diện vì $h_3$, $h_4$ lệch hơn $0{,}1$.
  - ≈ 52 âm tiết.
- **Ghi chú diễn giả:** Biến cố cần có xác suất cao là biến cố mọi giả thuyết trong lớp có rủi ro thực nghiệm gần rủi ro kì vọng; trên biến cố đó, giả thuyết nào được chọn cũng có độ lệch nhỏ. Bảng là hiệu giữa rủi ro thực nghiệm trên $S_\eta$ của Bài 01 và rủi ro kì vọng dưới $D_\eta$. Nguồn: ghi chú Bài 02, §6, Định nghĩa 02.13 và bảng sau.
- **Lý do / nối:** đặt tên biến cố tốt → định lý chặn xác suất của nó.
- **Mục tiêu / nguồn:** 3; Định nghĩa 02.13.

#### `5-03` Hội tụ đều trên lớp hữu hạn — trực quan, kết quả · 3 phút
- **Mặt trang:**
  - **Trực quan.** Cận đồng thời cho $K$ giả thuyết chỉ thay $\ln(2/\delta)$ bằng $\ln(2K/\delta)=\ln K+\ln(2/\delta)$.
  - **Định lý 02.14.** **Giả thiết:** (T1), (T2), (T3), (T4); $\delta\in(0,1)$.
  - **Bảo đảm** (xác suất theo $S\sim D^m$, mọi $D$), với $r_m=\sqrt{\ln(2K/\delta)/(2m)}$, $r_m^{+}=\sqrt{\ln(K/\delta)/(2m)}$:
    - (a) với xác suất ít nhất $1-\delta$, display $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\le r_m$;
    - (b) với xác suất ít nhất $1-\delta$, $L_D(h)\le L_S(h)+r_m^{+}$ đồng thời cho mọi $h\in\mathcal H$;
    - (c) nếu $m\ge\ln(2K/\delta)/(2\epsilon^2)$, thì $S$ là $\epsilon$-đại diện với xác suất ít nhất $1-\delta$.
  - ≈ 55 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Bảo đảm đúng đồng thời cho mọi $h$, phụ thuộc $K$ qua $\ln K$ và không phụ thuộc $D$. Với $K=1$, hai bán kính trở về bán kính hai phía và một phía của cận tin cậy Hoeffding. Vì (b) đúng cho mọi $h\in\mathcal H$ cùng lúc, mọi giả thuyết $\hat h\in\mathcal H$ chọn theo $S$ bằng một quy tắc đo được có $L_D(\hat h)\le L_S(\hat h)+r_m^{+}$ với xác suất ít nhất $1-\delta$: $L_S(\hat h)+r_m^{+}$ là một cận trên tin cậy cho giả thuyết được chọn. Nguồn: ghi chú Bài 02, §6, Định lý 02.14 và đoạn sau; UML §4.2.
- **Lý do / nối:** kết quả chính của mạch; trực quan bằng phân tích lôgarit → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 3; Định lý 02.14.

#### `5-04` Ý tưởng chứng minh: hội tụ đều trên lớp hữu hạn — ý tưởng chứng minh · 3,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** (danh sách đánh số)
  - 1. Biến cố hỏng nằm trong $\bigcup_{h\in\mathcal H}B_h$, với $B_h=\{\lvert L_S(h)-L_D(h)\rvert\ge r\}$.
  - 2. Mỗi $h$ cố định theo (T4), nên Hệ quả 02.10(a) cho $\Pr(B_h)\le2e^{-2mr^2}$.
  - 3. **Nhắc lại:** bất đẳng thức hợp; $K$ số hạng cho display $\Pr\big(\bigcup_hB_h\big)\le2Ke^{-2mr^2}$.
  - 4. Giải $2Ke^{-2mr^2}=\delta$ được $r=r_m$.
  - **Kỹ thuật.** Mỗi giả thuyết nhận xác suất thất bại $\delta/K$; các $B_h$ không cần độc lập.
  - Cực biên: khi $B_1=\cdots=B_K$, vế phải gấp $K$ lần xác suất của hợp.
  - ≈ 55 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả** (~200 âm tiết): Lộ trình: viết biến cố hỏng thành hợp các biến cố hỏng của từng giả thuyết, chặn từng biến cố bằng bất đẳng thức Hoeffding, cộng lại bằng bất đẳng thức hợp. Giả thiết (T4) vào hai lần: ở bước 2, mỗi $h$ cố định đối với $S$ nên cận tin cậy Hoeffding áp dụng được; ở bước 3, tổng có đúng $K$ số hạng. (T1) và (T3) đi vào qua cận tin cậy Hoeffding. Phần (b) thay $B_h$ bằng biến cố một phía và được $Ke^{-2mr^2}$. Bất đẳng thức hợp đúng với mọi cấu trúc phụ thuộc giữa các biến cố, nên không cần các tỉ lệ lỗi độc lập như ở ví dụ $1000$ ứng viên. Nếu cố định trước một họ đếm được với trọng số $w_k$, $\sum_kw_k\le1$, mỗi giả thuyết nhận $w_k\delta$ thay cho $\delta/K$ (Bài tập 02.6). Nguồn: ghi chú Bài 02, chứng minh Định lý 02.14; Bổ đề 02.12; §9; UML §4.2.
- **Lý do / nối:** lộ trình bốn bước, (T4) vào ở hai bước → kiểm tra bỏ hệ số $K$.
- **Mục tiêu / nguồn:** 3, 5; chứng minh Định lý 02.14.

#### `5-05` Chia xác suất thất bại cho từng giả thuyết — kỹ thuật (lần đầu trong học phần) · 1,5 phút
- **Mặt trang** (thêm theo quyết định của điều phối viên, mục 11.4): **Kỹ thuật.** nếu $\Pr(B_h)\le\delta/K$ với mọi $h$, bất đẳng thức hợp cho $\Pr(\bigcup_hB_h)\le\delta$; đảo cận đuôi tại mức $\delta/K$: $2e^{-2mr^2}=\delta/K$ cho $r=r_m$, bán kính tăng theo $\ln K$; dòng "Dùng khi …; dùng ở Định lý 02.14". deck_check: 40 âm tiết.
- **Ghi chú diễn giả:** kỹ thuật ghép bất đẳng thức hợp và đảo cận đuôi; với cận đuôi mũ chia $\delta$ cho $K$ chỉ cộng $\ln K$, với Chebyshev nhân cỡ mẫu với $K$; họ đếm được với trọng số $w_k$ (Bài tập 02.6). Nguồn: chứng minh Định lý 02.14 (Bước 3–4), §9; Bài tập 02.6.
- **Lý do / nối:** kỹ thuật dùng lại ở Bài 03 (hàm tăng trưởng thay $K$), Bài 04 (trọng số $w_k$) → bài tập bỏ hệ số $K$.
- **Mục tiêu / nguồn:** 3, 6; Định lý 02.14, §9.

#### `5-06` Bài tập: phản ví dụ cho bất đẳng thức hợp bỏ hệ số $K$ — bài tập (Bài tập 02.4), đề · 2 phút (1 phút tự làm)
- **Mặt trang:**
  - Lập luận của một học viên: với mỗi $h$ cố định, $\Pr(\lvert L_S(h)-L_D(h)\rvert\ge\epsilon)\le2e^{-2m\epsilon^2}$; vì vậy, với xác suất ít nhất $1-2e^{-2m\epsilon^2}$, mọi $h\in\mathcal H$ có $\lvert L_S(h)-L_D(h)\rvert<\epsilon$.
  - Dữ kiện: $\mathcal X=\{0,1\}^K$; các tọa độ $X_k\sim\mathrm{Bernoulli}(\tfrac12)$ độc lập; $Y=0$; $h_k(x)=x_k$; $m=10$; $\epsilon=0{,}4$.
  - **Câu hỏi:** (a) tính $L_D(h_k)$, cận $2e^{-2m\epsilon^2}$ và xác suất lệch chính xác với $k$ cố định; (b) tính chính xác $\Pr(\exists k:\ L_S(h_k)=0)$ khi $K=1000$ và kết luận về khẳng định của học viên; (c) chỉ ra bước của chứng minh Định lý 02.14 mà học viên bỏ qua.
  - ≈ 60 âm tiết.
- **Ghi chú diễn giả:** Gợi ý: một giả thuyết $h_k$ nhất quán với tập huấn luyện khi cả $10$ quan sát có tọa độ thứ $k$ bằng $0$; biến cố này chỉ phụ thuộc tọa độ thứ $k$. Bài tập nằm trong tệp bài tập cùng gợi ý và lời giải đầy đủ. Nguồn: tệp bài tập, Bài tập 02.4.
- **Lý do / nối:** bài tập có lời giải trên mặt trang cho cụm hội tụ đều, lấy từ `exercises.md` với đúng dữ kiện và câu hỏi; hai trang để giữ trần mật độ → lời giải.
- **Mục tiêu / nguồn:** 5; Bài tập 02.4.

#### `5-07` Bài tập: phản ví dụ cho bất đẳng thức hợp bỏ hệ số $K$, lời giải — bài tập, lời giải trên mặt trang · 2 phút
- **Mặt trang:**
  - **Lời giải:** (a) $h_k$ sai khi và chỉ khi $X_k=1$, nên $L_D(h_k)=\tfrac12$; cận của học viên là $2e^{-3{,}2}\approx0{,}0815$.
  - `[f]` Với $k$ cố định, $10L_S(h_k)\sim\mathrm{Bin}(10;\tfrac12)$, độ lệch $\ge0{,}4$ khi số lỗi thuộc $\{0,1,9,10\}$: $22/1024\approx0{,}0215$.
  - `[f]` (b) $K$ biến cố $\{L_S(h_k)=0\}$ độc lập, mỗi biến cố có xác suất $2^{-10}$: $1-(1-2^{-10})^{1000}\approx0{,}6236>0{,}0815$; khẳng định sai.
  - `[f]` (c) Định lý 02.14 cho $2Ke^{-3{,}2}\approx81{,}5$, không mâu thuẫn; học viên bỏ bước bất đẳng thức hợp.
  - ≈ 58 âm tiết.
- **Ghi chú diễn giả:** Trên biến cố $L_S(h_k)=0$, độ lệch bằng $\tfrac12\ge0{,}4$. Với $K=5000$ xác suất ở (b) là $0{,}9924$. Tổng các xác suất $\Pr(L_S(h_k)=0)$ là $1000/1024\approx0{,}977$, cùng bậc với xác suất $0{,}6236$ của hợp, vì các biến cố độc lập và mỗi biến cố có xác suất nhỏ. Với $K=1$, xác suất ở (b) là $1/1024$, nhỏ hơn $0{,}0815$; nó vượt $0{,}0815$ từ $K=88$. Nguồn: tệp bài tập, lời giải Bài tập 02.4.
- **Lý do / nối:** lời giải mỗi dòng một bước, kết thúc bằng kết luận → trả lời câu hỏi mở đầu thứ hai.
- **Mục tiêu / nguồn:** 5; lời giải Bài tập 02.4.

#### `5-08` Ví dụ: bán kính tin cậy sau khi chọn trong $K$ ứng viên — ví dụ, trả lời câu hỏi mở đầu · 2,5 phút
- **Mặt trang:**
  - Dữ kiện: $m=1000$, $\delta=0{,}05$, hàm lỗi 0–1; hàm được chọn có $L_S(\hat h)=0{,}05$; ứng viên cố định khi biết tập huấn luyện của chúng.
  - $K=1000$: $r_m^{+}=\sqrt{\ln20\,000/2000}\approx0{,}0704$, cận trên $0{,}05+0{,}0704=0{,}1204$.
  - $K=5000$: $r_m^{+}=\sqrt{\ln100\,000/2000}\approx0{,}0759$, cận trên $0{,}1259$; $K=1$: $r_m^{+}\approx0{,}0387$, như hàm cố định.
  - Hình F4 (`img/lec-02/ban-kinh-theo-K.svg`): $r_m^{+}$ theo $K$ ở $m=1000$, $\delta=0{,}05$.
  - **Diễn giải:** chọn trong $1000$ ứng viên làm bán kính tăng từ $0{,}0387$ lên $0{,}0704$; thêm năm lần số ứng viên chỉ thêm khoảng $0{,}005$.
  - ≈ 58 âm tiết.
- **Ghi chú diễn giả:** Đây là câu trả lời cho câu hỏi mở đầu: với độ tin cậy $95\%$, rủi ro kì vọng không quá khoảng $8{,}9\%$ cho một hàm cố định và khoảng $12\%$ cho hàm chọn trong $1000$ ứng viên. Định lý áp dụng được vì khi biết tập huấn luyện $T$ của các ứng viên, $K$ ứng viên cố định và $S$ vẫn có phân bố $D^m$; bảo đảm có điều kiện đúng với mọi $T$, lấy kì vọng theo $T$ được bảo đảm không điều kiện. Ở ví dụ $1000$ ứng viên có rủi ro $0{,}07$, độ lệch $L_D(g_j)-L_S(g_j)\le0{,}07<0{,}0704$ chắc chắn, nên thiên lệch do chọn nằm trong bán kính. Với hàm lỗi 0–1 và lớp hữu hạn, $r_m^{+}$ là một cận tổng quát hóa cho mọi thuật toán ERM, và $r_m^{+}\to0$ khi $m\to\infty$. Đọc hình: trục ngang $K$ theo thang lôgarit từ $1$ đến $10^4$, điểm tại $K=1;\ 10;\ 100;\ 1000;\ 5000$ với $r_m^{+}=0{,}0387;\ 0{,}0515;\ 0{,}0616;\ 0{,}0704;\ 0{,}0759$; mỗi lần nhân $K$ lên $10$, bán kính tăng ít hơn lần trước. Nguồn: ghi chú Bài 02, Ví dụ 02.8, Nhận xét 02.15.
- **Lý do / nối:** áp dụng Định lý 02.14(b), trả lời nửa sau câu hỏi mở đầu → so với mức tốt nhất trong lớp.
- **Mục tiêu / nguồn:** 3, 4; Ví dụ 02.8.

#### `5-09` Rủi ro vượt mức của ERM trên lớp hữu hạn — trực quan, kết quả, cận bằng số · 3 phút
- **Mặt trang:**
  - **Trực quan.** Hệ số $2$: một lần so sánh $L_D$ với $L_S$ tại $\hat h$, một lần tại phần tử tốt nhất $h_{\mathcal H}\in\arg\min_{h\in\mathcal H}L_D(h)$.
  - **Hệ quả 02.16.** **Giả thiết:** (T1), (T2), (T3), (T4); thuật toán ERM bất kì theo (O1), mọi quy tắc chọn khi bằng nhau; $\delta\in(0,1)$.
  - **Bảo đảm:** với xác suất ít nhất $1-\delta$ theo $S$, đồng thời cho mọi nghiệm ERM, display $L_D(\hat h)\le\min_{h\in\mathcal H}L_D(h)+2r_m$;
  - mọi thuật toán ERM là thuật toán học PAC bất khả diễn với $M(\epsilon,\delta)=\lceil2\ln(2K/\delta)/\epsilon^2\rceil$.
  - **Ví dụ.** Sáu hàm ngưỡng, $\epsilon=0{,}1$, $\delta=0{,}05$: $M=\lceil1096{,}1\rceil=1097$; mọi nghiệm ERM có $L_{D_\eta}(\hat h)\le0{,}32$ với xác suất ít nhất $0{,}95$.
  - ≈ 60 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Bảo đảm chặn rủi ro vượt mức so với lớp giả thuyết, không phụ thuộc $D$ và không phụ thuộc quy tắc chọn khi bằng nhau: cỡ mẫu $1097$ đúng cho cả $A_{\min}$ lẫn $A_{\max}$ và cho mọi phân bố trên $\{1,\ldots,5\}\times\{0,1\}$. Trong $M(\epsilon,\delta)$, $\epsilon$ là mức rủi ro vượt mức; độ lệch đồng thời tương ứng là $\epsilon/2$. Với nghiệm ERM xấp xỉ theo (O2), vế phải thêm $\epsilon_{\mathrm{opt}}$. Ở $m=6$, $2r_6\approx1{,}35>1$, nên cận không loại trừ rủi ro vượt mức $0{,}10$ của $A_{\min}$ trên $S_\eta$. Trên lớp mọi hàm phân lớp của năm mức, $K=32$ và cùng công thức cho $1431$ quan sát với đối tượng so sánh là rủi ro Bayes $0{,}18$; cỡ mẫu tăng tuyến tính theo số mức. Nguồn: ghi chú Bài 02, §7, Hệ quả 02.16, Ví dụ 02.9, 02.10; UML §4.2.
- **Lý do / nối:** kết quả chính thứ hai của mạch, con số trên ví dụ xuyên suốt → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 3, 4; Hệ quả 02.16, Ví dụ 02.9.

#### `5-10` Ý tưởng chứng minh: rủi ro vượt mức của ERM — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** (danh sách đánh số)
  - 1. $h_{\mathcal H}$ tồn tại vì $\mathcal H$ hữu hạn; nó xác định bởi $D$, không phụ thuộc $S$.
  - 2. Trên biến cố "$S$ là $r$-đại diện", với mọi nghiệm ERM $\hat h$: display $L_D(\hat h)\le L_S(\hat h)+r\le L_S(h_{\mathcal H})+r\le L_D(h_{\mathcal H})+2r$.
  - 3. Bất đẳng thức thứ nhất: tính đại diện tại $\hat h$; thứ hai: (O1); thứ ba: tính đại diện tại $h_{\mathcal H}$.
  - 4. Định lý 02.14(a) với $r=r_m$; $2r_m\le\epsilon$ cho $M(\epsilon,\delta)$.
  - Bỏ (O1): bất đẳng thức thứ hai hỏng; với (O2) cộng thêm $\epsilon_{\mathrm{opt}}$. Cực biên $K=1$: rủi ro vượt mức bằng $0$.
  - ≈ 55 âm tiết; một công thức hiển thị (đo ở 390 px; ngắt bằng `aligned` chỉ khi tràn).
- **Ghi chú diễn giả** (~170 âm tiết): Lộ trình: một bước tất định trên biến cố $r$-đại diện, rồi Định lý 02.14. Bước 2 không dùng xác suất: trên mọi tập $r$-đại diện, mọi nghiệm ERM thỏa chuỗi bất đẳng thức, nên bảo đảm đúng đồng thời cho mọi nghiệm ERM, với mọi quy tắc chọn khi bằng nhau. Xác suất chỉ vào ở bước 4, qua một biến cố không phụ thuộc thuật toán. Hệ số $2$ đến từ hai phép so sánh, tại $\hat h$ và tại $h_{\mathcal H}$, không đến từ biến cố hai phía. Với $K=1$, ERM trả về ứng viên duy nhất, nên rủi ro vượt mức bằng $0$ với mọi $m$, trong khi công thức vẫn cho cỡ mẫu dương: chứng minh không dùng tính chất riêng của trường hợp này. Nguồn: ghi chú Bài 02, chứng minh Hệ quả 02.16; Ví dụ 02.12, Bước 3; UML §4.2.
- **Lý do / nối:** lộ trình và chỗ dùng (O1) → tách riêng bước tất định thành kỹ thuật.
- **Mục tiêu / nguồn:** 3; chứng minh Hệ quả 02.16.

#### `5-11` Bước tất định trên biến cố đại diện — kỹ thuật (lần đầu trong học phần), câu hỏi · 2,5 phút
- **Mặt trang:**
  - **Kỹ thuật.** Tách chứng minh thành hai phần: một biến cố tốt $E$ không phụ thuộc thuật toán, với $\Pr(E)\ge1-\delta$; và một bước tất định trên $E$: so sánh $L_D$ với $L_S$ tại $\hat h$, dùng tính tối ưu của $\hat h$, so sánh lại tại $h_{\mathcal H}$.
  - Dùng khi: thuật toán chọn giả thuyết theo $S$ và cần một bảo đảm cho mọi nghiệm, mọi quy tắc chọn khi bằng nhau. Dùng ở: Hệ quả 02.16.
  - **Câu hỏi:** trong chuỗi ba bất đẳng thức, bất đẳng thức nào cần một cận đúng đồng thời cho mọi $h\in\mathcal H$, bất đẳng thức nào chỉ cần một cận cho một giả thuyết cố định?
  - `[f]` **Lời giải:** bất đẳng thức thứ nhất, tại $\hat h$ chọn theo $S$, cần cận đồng thời; bất đẳng thức thứ ba, tại $h_{\mathcal H}$ không phụ thuộc $S$, chỉ cần một cận cho một giả thuyết.
  - ≈ 60 âm tiết.
- **Ghi chú diễn giả:** Bất đẳng thức thứ nhất dùng chiều $L_D-L_S\le r$ tại $\hat h$, bất đẳng thức thứ ba dùng chiều $L_S-L_D\le r$ tại $h_{\mathcal H}$; bất đẳng thức thứ hai là (O1), không dùng xác suất. Vì vậy chỉ cần $K$ biến cố đuôi một phía cộng một biến cố đuôi tại $h_{\mathcal H}$, và cỡ mẫu giảm từ $1659$ xuống $1523$ khi $K=100$, $\epsilon=0{,}1$, $\delta=0{,}05$ (Bài tập 02.3). Khi lớp giả thuyết vô hạn, cùng bước tất định vẫn dùng được nếu có một biến cố đại diện với xác suất cao. Nguồn: ghi chú Bài 02, chứng minh Hệ quả 02.16 (Bước 2–3); tệp bài tập, Bài tập 02.3(a), (c); UML §4.2.
- **Lý do / nối:** kỹ thuật dùng lại qua học phần, đặt ngay sau nơi dùng lần đầu; câu hỏi lấy từ Bài tập 02.3(a), cùng kết quả → tiêu đề mạch 6.
- **Mục tiêu / nguồn:** 3; Hệ quả 02.16, Bài tập 02.3(a).

#### `5-12` Bài tập: hệ số hai trong bảo đảm của ERM — bài tập (Bài tập 02.3(a)) · 2 phút
- **Mặt trang** (thêm theo quyết định của điều phối viên, mục 11.8: câu hỏi dùng nguyên câu chữ Bài tập 02.3(a)): chuỗi ba bất đẳng thức (công thức hiển thị); **Câu hỏi:** nguyên văn Bài tập 02.3(a). deck_check: 59 âm tiết (ngoại lệ trên mục tiêu 40, dưới trần 60: câu chữ của bài tập đã 58 âm tiết; dòng duy nhất vượt 20 âm tiết vì là một đoạn đề bài).
- **Ghi chú diễn giả:** lời giải theo tệp bài tập (chiều $L_D-L_S\le r$ tại $\hat h$, cận đồng thời; (O1); chiều $L_S-L_D\le r$ tại $h_{\mathcal H}$ cố định; $K$ biến cố một phía cộng một biến cố; $1659\to1523$ ở phần (c)). Lời giải ở ghi chú diễn giả vì bài chính của cụm là Bài tập 02.4 (`5-06`, `5-07`, lời giải trên mặt trang).
- **Lý do / nối:** kiểm tra bước tất định ngay sau trang kỹ thuật → tiêu đề mạch 6.
- **Mục tiêu / nguồn:** 3; Bài tập 02.3(a).

### Mạch 6. Lớp hữu hạn trong trường hợp khả diễn (9 trang, 19,5 phút)

#### `6-00` 6. Lớp hữu hạn trong trường hợp khả diễn — tiêu đề mạch, điểm vào mạch 6 · 0,5 phút
- **Mặt trang:** "6."; h2 tên mạch; `p.strand-lead`; `p.strand-keys` "giả thuyết nhất quán · giả thuyết xấu · hai tốc độ · lớp phụ thuộc dữ liệu".
- **Ghi chú diễn giả:** Kế thừa: cỡ mẫu bất khả diễn $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$, tăng như $1/\epsilon^2$. Nhiệm vụ: khi lớp giả thuyết chứa một hàm có rủi ro $0$, thay bất đẳng thức Hoeffding bằng biến cố "không quan sát nào bị phân lớp sai", được cỡ mẫu tăng như $1/\epsilon$; giải thích nguồn của hai tốc độ; nêu giới hạn của mọi cận trong bài khi lớp giả thuyết phụ thuộc dữ liệu. Nguồn: ghi chú Bài 02, §8, §9.
- **Lý do / nối:** mạch 5 → giả thuyết nhất quán.
- **Mục tiêu / nguồn:** 4; §8, §9.

#### `6-01` Giả thuyết nhất quán và giả thuyết xấu — trực quan, định nghĩa, ví dụ · 2,5 phút
- **Mặt trang:**
  - Giả thuyết $h$ nhất quán với tập huấn luyện (consistent hypothesis) nếu $L_S(h)=0$; $h$ là giả thuyết xấu nếu $L_D(h)>\epsilon$.
  - **Trực quan.** Một quan sát bị phân lớp sai đủ loại một giả thuyết xấu; theo (T1), display $\Pr\big(L_S(h)=0\big)=\big(1-L_D(h)\big)^m<(1-\epsilon)^m$.
  - **Nhắc lại:** chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$.
  - **Ví dụ.** Dưới $D_f$ ($D_{\mathcal X}$ đều trên năm mức, $Y=h_3(X)$), $h_4$ chỉ sai tại $x=3$, $L_{D_f}(h_4)=0{,}2$; $h_4$ nhất quán với tập huấn luyện khi và chỉ khi $S$ không có quan sát nào tại $x=3$, xác suất $0{,}8^m$, bằng $0{,}044$ ở $m=14$.
  - ≈ 60 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Với hàm lỗi 0–1, $L_S(h)=0$ khi và chỉ khi $h(X_i)=Y_i$ với mọi $i$; mỗi quan sát được $h$ phân lớp đúng với xác suất $1-L_D(h)$, và các quan sát độc lập. Khi lớp giả thuyết chứa một hàm có rủi ro $0$, nghiệm ERM nhất quán với tập huấn luyện hầu chắc chắn, nên chỉ cần chặn xác suất để một giả thuyết xấu nhất quán với tập huấn luyện. $D_f$ là phân bố tất định của Bài 01: $D_{\mathcal X}$ đều trên năm mức và $Y=h_3(X)$. Biến cố "$S$ không có quan sát tại mức $3$" là biến cố bỏ sót của Bài 01. Nguồn: ghi chú Bài 02, §8 (đoạn đầu), chứng minh Mệnh đề 02.17 (Bước 1); Ví dụ 02.11, Bước 4.
- **Lý do / nối:** vấn đề và trực quan trước phát biểu; con số $0{,}8^m$ quen từ Bài 01 → mệnh đề cỡ mẫu.
- **Mục tiêu / nguồn:** 4; §8.

#### `6-02` Cỡ mẫu cho lớp hữu hạn trong trường hợp khả diễn — kết quả · 2,5 phút
- **Mặt trang:**
  - **Mệnh đề 02.17.** **Giả thiết:** $\mathcal Y=\{0,1\}$, hàm lỗi 0–1; (T1), (T4); $(D,\mathcal H)$ khả diễn; thuật toán ERM bất kì theo (O1); $\epsilon,\delta\in(0,1)$.
  - **Bảo đảm** (xác suất theo $S$), với $\mathcal H_{>\epsilon}=\{h\in\mathcal H:L_D(h)>\epsilon\}$ cố định:
    - (a) mỗi $h\in\mathcal H_{>\epsilon}$: $\Pr(L_S(h)=0)<(1-\epsilon)^m\le e^{-\epsilon m}$;
    - (b) $\Pr\big(\exists h\in\mathcal H_{>\epsilon}:\ L_S(h)=0\big)\le Ke^{-\epsilon m}$;
    - (c) với xác suất ít nhất $1-Ke^{-\epsilon m}$, mọi nghiệm ERM có $L_D(\hat h)\le\epsilon$; mọi thuật toán ERM là thuật toán học PAC với display $M(\epsilon,\delta)=\Big\lceil\dfrac{\ln K+\ln(1/\delta)}{\epsilon}\Big\rceil$.
  - **Ý nghĩa:** $K=6$, $\epsilon=0{,}1$, $\delta=0{,}05$: $M=\lceil\ln120/0{,}1\rceil=48$.
  - ≈ 52 âm tiết; một công thức hiển thị.
- **Ghi chú diễn giả:** Tính khả diễn và thuật toán chỉ dùng ở phần (c). Phần (c) chặn rủi ro tuyệt đối $L_D(\hat h)$ với xác suất cao, với đối tượng so sánh $0$ và một biến cố một phía. Tập $\mathcal H_{>\epsilon}$ xác định bởi $D$, không bởi $S$, nên mỗi phần tử của nó là một giả thuyết cố định. Theo định nghĩa độ phức tạp mẫu của Bài 01, $m_{\mathcal H}(\epsilon,\delta)\le\lceil\ln(K/\delta)/\epsilon\rceil$. Số $48$ đúng cho mọi nghiệm ERM, mọi lớp $6$ phần tử và mọi phân bố khả diễn. Nguồn: ghi chú Bài 02, §8, Mệnh đề 02.17 và đoạn sau; Ví dụ 02.11, Bước 1; UML §2.3.1.
- **Lý do / nối:** kết quả chính của mạch → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 4; Mệnh đề 02.17.

#### `6-03` Ý tưởng chứng minh: trường hợp khả diễn — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** (danh sách đánh số)
  - 1. Một giả thuyết xấu cố định: lũy thừa $m$ nhờ (T1), rồi chặn xác suất bỏ sót.
  - 2. **Nhắc lại:** bất đẳng thức hợp trên $\mathcal H_{>\epsilon}$, tối đa $K$ phần tử theo (T4), cho $Ke^{-\epsilon m}$.
  - 3. Khả diễn: có $h^\star\in\mathcal H$ với $L_D(h^\star)=0$, nên $L_S(h^\star)=0$ hầu chắc chắn, nên mọi nghiệm ERM có $L_S(\hat h)=0$; nếu $L_D(\hat h)>\epsilon$ thì $\hat h\in\mathcal H_{>\epsilon}$ nhất quán với tập huấn luyện.
  - 4. $Ke^{-\epsilon m}\le\delta\iff m\ge\ln(K/\delta)/\epsilon$.
  - Bỏ khả diễn: (a), (b) vẫn đúng, nhưng $L_S(\hat h)=0$ không còn bảo đảm; khi đó cần Hệ quả 02.16.
  - Cực biên: trên lớp hàm ngưỡng các biến cố lồng nhau, nên bất đẳng thức hợp lỏng.
  - ≈ 60 âm tiết.
- **Ghi chú diễn giả** (~180 âm tiết): Lộ trình: tính xác suất để một giả thuyết xấu nhất quán với tập huấn luyện, cộng trên các giả thuyết xấu bằng bất đẳng thức hợp, rồi dùng tính khả diễn để nghiệm ERM nhất quán với tập huấn luyện. Chứng minh không dùng bất đẳng thức Hoeffding: biến cố cần chặn là "mọi quan sát đều được phân lớp đúng", có xác suất tính chính xác được. Tính độc lập vào ở bước 1, (T4) ở bước 2, tính khả diễn ở bước 3. Trên lớp hàm ngưỡng, nếu một ngưỡng xấu bên trái nhất quán với tập huấn luyện thì ngưỡng xấu gần $t^\star$ nhất bên trái cũng vậy; các biến cố lồng nhau thành hai chuỗi, và chỉ cần cộng hai số hạng thay cho sáu. Nguồn: ghi chú Bài 02, chứng minh Mệnh đề 02.17; Ví dụ 02.11, Bước 2; UML §2.3.1.
- **Lý do / nối:** lộ trình bốn bước, giả thiết vào ở đâu → bốn mức cỡ mẫu trên cùng ví dụ.
- **Mục tiêu / nguồn:** 4, 5; chứng minh Mệnh đề 02.17.

#### `6-04` Ví dụ: bốn mức cỡ mẫu cho dữ liệu tất định — ví dụ, cận bằng số · 2,5 phút
- **Mặt trang:**
  - Dữ kiện: $D_f$ với $f=h_3$; sáu hàm ngưỡng; $(D_f,\mathcal H)$ khả diễn, $h^\star=h_3$; $\epsilon=0{,}1$, $\delta=0{,}05$.
  - Bảng (Cỡ mẫu | Phạm vi | Cách tính):
    - $48$ | mọi nghiệm ERM, mọi lớp $6$ phần tử, mọi phân bố khả diễn | $\lceil\ln120/0{,}1\rceil$
    - $37$ | mọi nghiệm ERM trên lớp hàm ngưỡng | hai chuỗi lồng nhau, $\lceil\ln40/0{,}1\rceil$
    - $30$ | riêng $A_{\max}$ (chọn ngưỡng lớn nhất khi bằng nhau) trên lớp hàm ngưỡng | một chuỗi, $\lceil\ln20/0{,}1\rceil$
    - $14$ | riêng $A_{\max}$, riêng $D_f$ | $0{,}8^{14}\approx0{,}044\le0{,}05$
  - **Diễn giải:** mỗi bước từ $48$ xuống $14$ dùng thêm cấu trúc của lớp giả thuyết, của thuật toán hoặc của phân bố.
  - ≈ 55 âm tiết (bảng so sánh, trần 80).
- **Ghi chú diễn giả:** Bốn số đều là cỡ mẫu đủ cho cùng $\epsilon$, $\delta$, với phạm vi hẹp dần. Từ $48$ xuống $37$: Mệnh đề 02.17 cộng $6$ số hạng $e^{-\epsilon m}$, trong khi các biến cố "ngưỡng xấu nhất quán với tập huấn luyện" lồng nhau thành hai chuỗi, nên chỉ cần $2e^{-\epsilon m}\le\delta$. Từ $37$ xuống $30$: $A_{\max}$ chọn ngưỡng lớn nhất trong tập nghiệm, nên $\hat t\ge t^\star$ và chỉ còn chuỗi bên phải. Từ $30$ xuống $14$: dưới $D_f$, $A_{\max}$ thất bại khi và chỉ khi tập huấn luyện không có quan sát tại $x=3$; $0{,}8^{13}\approx0{,}0550>0{,}05$. Nguồn: ghi chú Bài 02, Ví dụ 02.11.
- **Lý do / nối:** kiểm tra bằng số; cho thấy bất đẳng thức hợp bảo thủ → bảng cỡ mẫu theo $K$.
- **Mục tiêu / nguồn:** 4; Ví dụ 02.11.

#### `6-05` Ví dụ: bảng cỡ mẫu cho $K$ ứng viên — ví dụ, so sánh · 2,5 phút
- **Mặt trang:**
  - Dữ kiện: $\delta=0{,}05$; mỗi ô ghi cỡ mẫu tại $\epsilon=0{,}05$ / $\epsilon=0{,}1$; ba cột ứng với ba bảo đảm.
  - Bảng ($K$ | ước lượng $\pm\epsilon$, $\lceil\ln(2K/\delta)/(2\epsilon^2)\rceil$ | rủi ro vượt mức $\le\epsilon$, $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$ | khả diễn, $\lceil\ln(K/\delta)/\epsilon\rceil$): $1$ | $738$ / $185$ | — | —; $100$ | $1659$ / $415$ | $6636$ / $1659$ | $153$ / $77$; $1000$ | $2120$ / $530$ | $8478$ / $2120$ | $199$ / $100$.
  - **Diễn giải:** từ $K=100$ lên $K=1000$, ở $\epsilon=0{,}1$: $415\to530$, $1659\to2120$, $77\to100$, mỗi cột cộng một lượng cố định.
  - **Lưu ý:** ba cột dùng $\epsilon$ theo ba nghĩa, nên chỉ so sánh trong cùng một cột.
  - ≈ 50 âm tiết (bảng so sánh, trần 80).
- **Ghi chú diễn giả:** Nhân $K$ lên $10$ lần cộng $\ln10\approx2{,}3026$ vào lôgarit, nên ở $\epsilon=0{,}1$ cỡ mẫu tăng khoảng $115{,}1$, $460{,}5$ và $23{,}0$ ở ba cột. Cột rủi ro vượt mức bằng cột ước lượng tại $\epsilon/2$, vì cần hai độ lệch $\epsilon/2$; ở các hàng $K=100$ và $1000$ nó gấp khoảng $4$ lần cột ước lượng. Cột khả diễn chặn rủi ro tuyệt đối với một biến cố một phía, dưới giả thiết mạnh hơn. Với $K=1$, ERM trả về ứng viên duy nhất, nên hai cột sau ghi "—". Một ô tính đầy đủ: $K=100$, $\epsilon=0{,}1$: $2\cdot8{,}2940/0{,}01=1658{,}8$, làm tròn lên $1659$. Nguồn: ghi chú Bài 02, Ví dụ 02.12; Phụ lục B.3.
- **Lý do / nối:** câu hỏi thực hành "cỡ tập xác thực tăng thế nào khi $K$ tăng" của ví dụ ứng viên; hai cột cuối dẫn tới hai tốc độ → trực quan hai tốc độ.
- **Mục tiêu / nguồn:** 4; Ví dụ 02.12.

#### `6-06` Hai tốc độ theo độ chính xác — trực quan, ví dụ · 2 phút
- **Mặt trang:**
  - **Trực quan.** Khả diễn: một quan sát sai loại một giả thuyết xấu, xác suất để nó nhất quán với tập huấn luyện nhỏ hơn $e^{-\epsilon m}$; số mũ tỉ lệ với $\epsilon$, nên $m\approx\ln(K/\delta)/\epsilon$.
  - Bất khả diễn: $\operatorname{Var}L_S(h)=L_D(h)(1-L_D(h))/m$, bằng $1/(4m)$ khi $L_D(h)=\tfrac12$; độ lệch chuẩn $1/(2\sqrt m)$ chỉ xuống cỡ $\epsilon$ khi $m$ cỡ $1/\epsilon^2$.
  - Hình F5 (`img/lec-02/hai-toc-do.svg`): hai cỡ mẫu theo $\epsilon$, $K=100$, $\delta=0{,}05$, thang log–log.
  - **Diễn giải:** giảm $\epsilon$ từ $0{,}1$ xuống $0{,}01$: cỡ mẫu khả diễn từ $77$ lên $761$, cỡ mẫu bất khả diễn từ $1659$ lên $165\,881$.
  - ≈ 60 âm tiết.
- **Ghi chú diễn giả:** Hai tốc độ đến từ hai biến cố khác nhau. Trong trường hợp khả diễn, cần loại các giả thuyết có rủi ro trên $\epsilon$, và mỗi quan sát có xác suất hơn $\epsilon$ để làm điều đó. Trong trường hợp bất khả diễn, cần ước lượng mọi rủi ro với sai số $\epsilon/2$, và độ lệch chuẩn của một tỉ lệ lỗi gần $\tfrac12$ là $1/(2\sqrt m)$. Đọc hình: trục ngang $\epsilon$ từ $0{,}01$ đến $0{,}2$, trục dọc từ $10$ đến $10^6$, cả hai thang lôgarit; đường khả diễn qua $39;\ 77;\ 153;\ 381;\ 761$ tại $\epsilon=0{,}2;\ 0{,}1;\ 0{,}05;\ 0{,}02;\ 0{,}01$, dốc $-1$; đường bất khả diễn qua $415;\ 1659;\ 6636;\ 41\,471;\ 165\,881$, dốc $-2$. Bất đẳng thức Bernstein, dùng cả phương sai, cho tốc độ gần $1/\epsilon$ khi phương sai cỡ $\epsilon$ (UML Phụ lục B.5, đọc thêm). Nguồn: ghi chú Bài 02, Nhận xét 02.18; Ví dụ 02.12; §12.
- **Lý do / nối:** trọng tâm "vì sao $1/\epsilon$ và $1/\epsilon^2$"; hình mang số liệu của hai công thức → bài tập trên một lớp khác.
- **Mục tiêu / nguồn:** 4; Nhận xét 02.18.

#### `6-07` Bài tập: lớp hội Boole — bài tập (Bài tập 02.8(c)(d)), lời giải trên mặt trang · 2,5 phút (1 phút tự làm)
- **Mặt trang:**
  - Dữ kiện: $\mathcal X=\{0,1\}^p$, $p=10$; lớp hội Boole (Boolean conjunctions) $\mathcal H_{\mathrm{conj}}$ có $\lvert\mathcal H_{\mathrm{conj}}\rvert=3^{p}+1=59\,050$; $(D,\mathcal H_{\mathrm{conj}})$ khả diễn; $\epsilon=0{,}1$, $\delta=0{,}05$.
  - **Câu hỏi:** tính cỡ mẫu đủ theo Mệnh đề 02.17(c) và $M(\epsilon,\delta)$ theo Hệ quả 02.16(c); tính lại cả hai khi $\epsilon=0{,}05$.
  - `[f]` **Lời giải:** khả diễn: $\lceil(\ln59\,050+\ln20)/0{,}1\rceil=\lceil139{,}8\rceil=140$.
  - `[f]` Bất khả diễn: $\lceil2\ln2\,362\,000/0{,}01\rceil=\lceil2935{,}004\rceil=2936$.
  - `[f]` $\epsilon=0{,}05$: $280$ và $11\,741$; cỡ mẫu khả diễn tăng $2$ lần, bất khả diễn tăng khoảng $4$ lần.
  - ≈ 50 âm tiết.
- **Ghi chú diễn giả:** Dưới một phân bố khả diễn, $\min_hL_D(h)=0$, nên bảo đảm của Hệ quả 02.16 trở thành $L_D(\hat h)\le\epsilon$, đúng bảo đảm của Mệnh đề 02.17(c): hai số $140$ và $2936$ bảo đảm cùng một biến cố và so sánh được. Cỡ mẫu khả diễn tăng tuyến tính theo $p$ vì $p\ln3<\ln(3^p+1)\le p\ln3+\ln2$. Phần (a) đếm $3^p+1$ hàm, phần (b) chứng minh thuật toán loại dần là một ERM; hai phần này giao về nhà. Nguồn: tệp bài tập, Bài tập 02.8(c)(d).
- **Lý do / nối:** bài tập có lời giải trên mặt trang cho cụm khả diễn, lấy từ `exercises.md`, cùng số liệu và kết quả; kiểm tra hai tốc độ trên một lớp khác → giới hạn.
- **Mục tiêu / nguồn:** 4, 5; Bài tập 02.8.

#### `6-08` Giá của số ứng viên và lớp phụ thuộc dữ liệu — ý nghĩa, giới hạn · 1,5 phút
- **Mặt trang:**
  - Chebyshev thay Hoeffding: mỗi giả thuyết nhận $\delta/K$, nên $m\ge K/(4\delta\epsilon^2)$; $K=1000$, $\epsilon=\delta=0{,}05$: $2\,000\,000$ quan sát, so với $2120$.
  - **Lưu ý:** lớp phụ thuộc dữ liệu (data-dependent class), lập sau khi xem $S$ hoặc qua dùng lại thích nghi (adaptive reuse), vi phạm (T4).
  - Cách sửa: một tập xác thực mới; hoặc một họ đếm được $h_1,h_2,\ldots$ cố định trước, $h_k$ nhận xác suất thất bại $w_k\delta$, $\sum_kw_k\le1$.
  - ≈ 58 âm tiết.
- **Ghi chú diễn giả:** Cận đuôi mũ làm số ứng viên chỉ đi vào qua $\ln K$; với cận đuôi đa thức như Chebyshev, nó đi vào tuyến tính. Các cận phải đúng cho mọi phân bố, nên bảo thủ; bất đẳng thức hợp bỏ qua quan hệ giữa các biến cố, như các biến cố lồng nhau trên lớp hàm ngưỡng. Họ đếm được ở cách sửa thứ hai phải chứa mọi ứng viên có thể được lập ra sau này. Dùng lại thích nghi nghĩa là thiết kế ứng viên mới theo tỉ lệ lỗi cũ trên cùng $S$. Nguồn: ghi chú Bài 02, §9.
- **Lý do / nối:** §9 của ghi chú: giá của số ứng viên và giới hạn (T4) → tiêu đề mạch Tổng kết.
- **Mục tiêu / nguồn:** 3, 4; §9.

### Mạch 7. Tổng kết (7 trang, 11,5 phút)

#### `7-00` 7. Tổng kết — tiêu đề mạch, điểm vào mạch 7 · 0,5 phút
- **Mặt trang:** "7."; h2 "Tổng kết"; `p.strand-lead` (bảng mạch); không có dòng từ khóa.
- **Ghi chú diễn giả:** Kế thừa: sáu kết quả chính và ba kỹ thuật của bài. Nhiệm vụ: gom giả thiết của từng kết quả, trả lời vấn đề trung tâm, làm một bài tập tổng hợp, tự kiểm tra, giao bài tập. Không có khái niệm mới. Nguồn: ghi chú Bài 02, §9–§12.
- **Lý do / nối:** mạch 6 → bảng tổng kết.
- **Mục tiêu / nguồn:** tất cả; §9–§12.

#### `7-01` Bảng tổng kết — tổng kết · 2,5 phút
- **Mặt trang:** bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh` (≈ 78 âm tiết, trần 80):

| Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh |
|---|---|---|
| Markov, Chebyshev (Bổ đề 02.2, 02.3) | $V\ge0$; độc lập hoặc không tương quan cho trung bình | Markov cho $V$ hoặc $(V-\mathbb EV)^2$ |
| $2e^{-2m\epsilon^2/(b-a)^2}$ (Bổ đề 02.6, Định lý 02.7) | độc lập; $a\le V_i\le b$ | Chernoff, tách tích, dây cung, chọn $\tau$ |
| $L_S(h)\pm\sqrt{\ln(2/\delta)/(2m)}$ (Hệ quả 02.10) | (T1), (T3); $h$ không phụ thuộc $S$ | Định lý 02.7 cho $\ell(h,Z_i)$, đảo cận đuôi |
| $\sup_h\lvert L_S(h)-L_D(h)\rvert\le r_m$ (Định lý 02.14) | thêm (T4) | bất đẳng thức hợp trên $K$ biến cố |
| $L_D(\hat h)\le\min_hL_D(h)+2r_m$ (Hệ quả 02.16) | thêm (O1) | bước tất định, hai phép so sánh |
| $m\ge\ln(K/\delta)/\epsilon$ (Mệnh đề 02.17) | khả diễn; (T1); (T4) | $(1-\epsilon)^m\le e^{-\epsilon m}$, bất đẳng thức hợp |

- **Ghi chú diễn giả:** Cột giữa là giả thiết mà bỏ đi thì kết luận sai, kèm phản ví dụ của bài: bản sao của một quan sát (bỏ độc lập: xác suất lệch bằng $1$ trong khi cận là $6{,}7\cdot10^{-4}$); biến nhận giá trị $m^2$ với xác suất $1/m^2$ (bỏ bị chặn); $1000$ ứng viên với tỉ lệ lỗi độc lập (bỏ hệ số $K$: $0{,}6236$ so với $0{,}0815$); danh sách ứng viên lập sau khi xem $S$ (bỏ (T4)). Các bảo đảm đều với xác suất cao theo $S$, không phụ thuộc $D$; Định lý 02.14 là bảo đảm cho lớp giả thuyết, Hệ quả 02.16 và Mệnh đề 02.17 là bảo đảm cho mọi thuật toán ERM. Nguồn: ghi chú Bài 02, §4–§9.
- **Lý do / nối:** một hàng cho mỗi kết quả chính → trả lời vấn đề trung tâm.
- **Mục tiêu / nguồn:** 1–5; §4–§9.

#### `7-02` Vấn đề trung tâm — tổng kết · 1,5 phút
- **Mặt trang:** danh sách câu trả lời cho cả bài (≈ 70 âm tiết):
  - Với $h$ chọn trước: $m\ge\ln(2/\delta)/(2\epsilon^2)$ quan sát cho $\lvert L_S(h)-L_D(h)\rvert\le\epsilon$ với xác suất ít nhất $1-\delta$.
  - Với $\hat h$ chọn theo $S$ trong $K$ ứng viên: thay $\ln(2/\delta)$ bằng $\ln(2K/\delta)$; giá của phép chọn là $\ln K$.
  - Để mọi nghiệm ERM có rủi ro vượt mức không quá $\epsilon$: $m\ge2\ln(2K/\delta)/\epsilon^2$.
  - Khi lớp giả thuyết khả diễn: $m\ge\ln(K/\delta)/\epsilon$, tăng như $1/\epsilon$ thay cho $1/\epsilon^2$.
  - Các cỡ mẫu cần quan sát độc lập, hàm lỗi bị chặn và lớp giả thuyết cố định trước khi lấy mẫu.
- **Ghi chú diễn giả:** Các câu trả lời theo thứ tự lập luận của bài. Câu hỏi mở đầu được trả lời trọn: với tỉ lệ lỗi $5\%$ trên $1000$ quan sát và độ tin cậy $95\%$, rủi ro kì vọng không quá khoảng $8{,}9\%$ cho một hàm cố định và khoảng $12\%$ cho hàm chọn trong $1000$ ứng viên. So với $K=1$, cỡ mẫu tăng thêm $\ln K/(2\epsilon^2)$, $2\ln K/\epsilon^2$ hoặc $\ln K/\epsilon$ cho ba bảo đảm. Nguồn: ghi chú Bài 02, đoạn mở đầu, Ví dụ 02.8, §9.
- **Lý do / nối:** trả lời vấn đề của trang 1-05 cho cả bài → bài tập tổng hợp.
- **Mục tiêu / nguồn:** tất cả; §9, Ví dụ 02.8.

#### `7-03` Bài tập: hàm lỗi có trọng số trong $[0,4]$ — bài tập tổng hợp (Bài tập 02.11(a)(b)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - **Nhắc lại:** hàm lỗi có trọng số (cost-weighted loss) $\ell_c$ của ví dụ sàng lọc: báo âm tính sai tốn $4$, báo dương tính sai tốn $1$, nên $\ell_c\in\{0,1,4\}\subset[0,4]$.
  - Dữ kiện: sáu hàm ngưỡng trên $\{1,\ldots,5\}$; $\epsilon=0{,}1$ (đơn vị chi phí), $\delta=0{,}05$; (a) cho $M(\epsilon,\delta)=\lceil2(b-a)^2\ln(2K/\delta)/\epsilon^2\rceil$.
  - **Câu hỏi:** tính $M(\epsilon,\delta)$ và so với cỡ mẫu $1097$ của Ví dụ 02.9.
  - `[f]` **Lời giải:** Định lý 02.7 trên $[a,b]$ cho bán kính đồng thời $(b-a)r_m$; bước tất định cho $2(b-a)r_m\le\epsilon$, tức công thức của (a).
  - `[f]` $(b-a)^2=16$, $\ln240\approx5{,}4806$: $2\cdot16\cdot5{,}4806/0{,}01\approx17\,538{,}04$, nên $M=17\,539$.
  - `[f]` $17\,538{,}04=16\cdot1096{,}13$: đúng $16$ lần giá trị của Ví dụ 02.9 trước khi làm tròn.
  - ≈ 60 âm tiết.
- **Ghi chú diễn giả:** Bài tập ghép ba bước của bài: bất đẳng thức Hoeffding với miền giá trị $[a,b]$, bất đẳng thức hợp trên $K=6$ giả thuyết, bước tất định cho nghiệm ERM. Hệ số $16$ là bình phương tỉ số giữa độ dài miền giá trị $4$ và độ dài $1$ của hàm lỗi 0–1. Phần (c) chứng minh cùng kết quả bằng cách đổi thang $\ell'=\ell_c/4$ và độ chính xác $\epsilon/4$. Kiểm tra: ở $m=17\,539$, $2\cdot4\sqrt{\ln240/35\,078}\approx0{,}099997\le0{,}1$. Nguồn: tệp bài tập, Bài tập 02.11; ghi chú Bài 02, §5 (đoạn về $\ell_c$), Hệ quả 02.16.
- **Lý do / nối:** bài tập tổng hợp của mạch Tổng kết, lấy từ `exercises.md` với đúng dữ kiện, câu hỏi và kết quả → tự kiểm tra.
- **Mục tiêu / nguồn:** 4; Bài tập 02.11.

#### `7-04` Câu hỏi tự kiểm tra — tổng kết · 2,5 phút
- **Mặt trang:** "Câu hỏi: trả lời và nêu kết quả đã dùng." rồi bốn câu (≈ 75 âm tiết):
  1. Một hàm phân lớp được chọn trong $200$ ứng viên vì có tỉ lệ lỗi nhỏ nhất, $8\%$, trên tập xác thực $2000$ quan sát. Tính một cận trên tin cậy $95\%$ cho rủi ro kì vọng của nó; cận đúng cho những hàm nào?
  2. Bước nào của chứng minh Định lý 02.14 hỏng nếu danh sách $200$ ứng viên được lập sau khi xem tỉ lệ lỗi trên chính tập xác thực đó?
  3. Bất đẳng thức Hoeffding dùng tính độc lập và tính bị chặn ở bước nào?
  4. Vì sao cỡ mẫu khả diễn tỉ lệ với $1/\epsilon$, còn cỡ mẫu bất khả diễn tỉ lệ với $1/\epsilon^2$?
- **Ghi chú diễn giả** (câu trả lời, mỗi câu trả lời được chỉ bằng ghi chú): (1) Định lý 02.14(b) với $K=200$, $m=2000$, $\delta=0{,}05$: $\ln4000\approx8{,}2940$, $r_m^{+}=\sqrt{8{,}2940/4000}\approx0{,}0455$, cận $0{,}08+0{,}0455\approx0{,}126$; cận đúng đồng thời cho cả $200$ ứng viên, nên đúng cho hàm được chọn (câu hỏi cuối buổi §11). (2) Bước 2: cận tin cậy Hoeffding cần mỗi $h$ cố định đối với $S$; khi danh sách lập sau khi xem $S$, (T4) không còn thỏa. (3) Độc lập ở bước tách kì vọng của tích (phương pháp Chernoff); bị chặn ở bổ đề Hoeffding, bước dây cung; phản ví dụ là bản sao của một quan sát và biến nhận giá trị $m^2$ (Ví dụ 02.6, Nhận xét 02.11). (4) Khả diễn: mỗi giả thuyết xấu nhất quán với tập huấn luyện với xác suất nhỏ hơn $e^{-\epsilon m}$, số mũ tỉ lệ với $\epsilon$; bất khả diễn: độ lệch chuẩn của $L_S(h)$ là $\sqrt{L_D(h)(1-L_D(h))/m}$, bằng $1/(2\sqrt m)$ khi $L_D(h)=\tfrac12$ (Nhận xét 02.18). Nguồn: ghi chú Bài 02, §11, chứng minh Định lý 02.7, 02.14, Nhận xét 02.18.
- **Lý do / nối:** câu hỏi cuối buổi và câu hỏi phụ của ghi chú §11 (1–2), hai câu về giả thiết và tốc độ (3–4) → bài tập về nhà.
- **Mục tiêu / nguồn:** 1, 3, 4, 5; §11.

#### `7-05` Bài tập về nhà — tổng kết · 1 phút
- **Mặt trang:** bảng `Mục | Bài tập`:

| Mục | Bài tập |
|---|---|
| Xác suất đuôi và bất đẳng thức Markov, Chebyshev | 02.1, 02.10 |
| Phương pháp Chernoff và bất đẳng thức Hoeffding | 02.2 |
| Cận tin cậy cho một giả thuyết cố định | 02.5 |
| Hội tụ đều và rủi ro vượt mức trên lớp hữu hạn | 02.3, 02.4, 02.6, 02.11 |
| Lớp hữu hạn trong trường hợp khả diễn | 02.7, 02.8, 02.9 |

  - Dòng liên kết: "Ghi chú bài giảng · Bài tập" (viewer, kèm `&deck=lecture-02-bat-dang-thuc-tap-trung.html`).
- **Ghi chú diễn giả:** Sáu bài đầu là bài gốc, năm bài sau chọn từ UML (§2.4, §3.5, §4.5). Bài tập 02.1 còn so tích hàm sinh mô-men với kì vọng của tổng khi các biến chỉ độc lập từng đôi, và cỡ mẫu Chebyshev $2000$ với cỡ mẫu Hoeffding $738$ tại $\epsilon=\delta=0{,}05$. Bài tập 02.5 là mô phỏng tùy chọn, đọc một cận đuôi như một phát biểu về tần suất trên nhiều lần lấy mẫu. Bài tập 02.6 mở rộng bất đẳng thức hợp sang họ đếm được có trọng số. Bài tập 02.7 cho một lớp vô hạn, hình chữ nhật song song với trục, có cỡ mẫu khả diễn $4\ln(4/\delta)/\epsilon$. Nguồn: ghi chú Bài 02, §10; tệp bài tập Bài 02.
- **Lý do / nối:** ánh xạ bài tập vào mạch, mỗi bài một mạch → tài liệu.
- **Mục tiêu / nguồn:** tất cả; §10, `exercises.md`.

#### `7-06` Tài liệu tham khảo — tổng kết · 0,5 phút
- **Mặt trang:**
  - Shalev-Shwartz và Ben-David (2014), *Understanding Machine Learning: From Theory to Algorithms*: Phụ lục B.1–B.4 (Markov, Chebyshev, Chernoff, Hoeffding); §2.3.1 (lớp hữu hạn trong trường hợp khả diễn); §§4.1–4.2 (hội tụ đều, lớp hữu hạn học được PAC bất khả diễn); đọc thêm Phụ lục B.5 (Bennett, Bernstein).
  - Dòng nối: "Bài 03: Chiều VC và hàm phân lớp tuyến tính." (liên kết thêm khi deck Bài 03 có tên tệp).
- **Ghi chú diễn giả:** Trước buổi học: UML Phụ lục B.1–B.2 và §2.3.1; sau buổi học: Phụ lục B.3–B.4, §§4.1–4.2 và bài tập §2.4, §3.5, §4.5. Khác biệt so với UML: bất đẳng thức Hoeffding không cần tính cùng phân bố; phương pháp Chernoff phát biểu thành một bổ đề; bất đẳng thức $\varphi(u)\le u^2/8$ chứng minh đầy đủ; trường hợp khả diễn viết với phân bố liên hợp; có dạng ERM xấp xỉ. Cầu nối: lớp hàm ngưỡng trên $\mathbb R$ và lớp nửa không gian (halfspace) trong $\mathbb R^p$ là vô hạn, nên cận theo $\ln\lvert\mathcal H\rvert$ không cho thông tin; trên lớp mọi hàm phân lớp của một tập đầu vào hữu hạn, cỡ mẫu tăng tuyến tính theo số phần tử của tập đầu vào. Câu hỏi cho Bài 03: với một lớp vô hạn, đại lượng nào thay cho $\ln\lvert\mathcal H\rvert$? Nguồn: ghi chú Bài 02, §11, §12; Ví dụ 02.10.
- **Lý do / nối:** trang cuối theo quy định → (hết).
- **Mục tiêu / nguồn:** —; §12.

## 7. Hành trình khái niệm

Thứ tự bước theo quy định: vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh (trang riêng) → kỹ thuật hoặc kiểm tra. Các bước có thể chung trang nhưng không đảo thứ tự trên mặt trang; ví dụ đứng sau phát biểu chỉ khi nó là bước kiểm tra (ghi ở cột cuối).

| Kết quả hoặc khái niệm | Vấn đề | Trực quan | Ví dụ | Phát biểu | Ý tưởng chứng minh | Kỹ thuật / kiểm tra | Gộp, `không áp dụng`, lý do |
|---|---|---|---|---|---|---|---|
| Xác suất đuôi (Định nghĩa 02.1) | 1-06, 2-02 ($\tfrac13$ so với $0{,}22$) | 2-03 (hình F1) | 2-03 (ba giá trị chính xác) | 2-03 | `không áp dụng` (định nghĩa) | 2-06 (so với các cận) | Trực quan, định nghĩa, ví dụ chung trang 2-03. |
| Markov, Chebyshev (Bổ đề 02.2, 02.3) | 2-03 (cần cận không dùng $D$) | 2-04 | 2-06 | 2-04 | 2-05 | 2-06 (bảng; cận Markov không giảm; cỡ mẫu $500$) | Ví dụ là bước kiểm tra sau ý tưởng chứng minh, theo thứ tự Ví dụ 02.3 của ghi chú. |
| Phương pháp Chernoff (Bổ đề 02.5) | 2-06 (cỡ mẫu như $1/\delta$) | 3-01 (dòng "Dùng khi") | 3-01 (hàm sinh mô-men Bernoulli) | 3-01 | 3-01 (ghi chú diễn giả, hai dòng) | 3-01 là trang kỹ thuật | Công cụ, không là kết quả chính: phát biểu, chứng minh hai dòng và kỹ thuật chung một trang (mục 11, điểm 3). |
| Bổ đề 02.6 | 3-01 (còn thiếu cận cho từng thừa số) | 3-02 (hình F3) | 3-02 (Bernoulli, $\tau=2$) | 3-02 | 3-03 | 3-03 (dòng "Kỹ thuật."; bỏ bị chặn: đuôi nặng) | Ví dụ sau phát biểu trên 3-02 là bước kiểm tra hai vế. |
| Định lý 02.7 | 2-06, 3-00 | 3-04 | 3-04 ($0{,}2707$, $0{,}0366$) | 3-04 | 3-05 | 3-04 (ghi chú diễn giả) (so ba cận); 4-06 (bỏ độc lập, bỏ bị chặn) | Ví dụ là bước kiểm tra sau phát biểu. |
| Cận tin cậy, Hệ quả 02.10 | 1-06 (câu hỏi thứ nhất), 4-01 (Câu hỏi: $L_S(h)$ không đủ) | 4-02 | 3-04 (ghi chú diễn giả), 4-05 | 4-01, 4-02 | 4-03 | 4-04 (kỹ thuật, bảng theo $\delta$); 4-05 (trả lời câu hỏi mở đầu); 4-06 | 3-04 (ghi chú diễn giả) đứng giữa ý tưởng chứng minh và kỹ thuật vì ghi chú đặt Ví dụ 02.4 Bước 1–3 trước Bước 4. |
| Định lý 02.14 | 1-06 (câu hỏi thứ hai), 5-01 (thiên lệch do chọn) | 5-03 (dòng lôgarit) | 5-01, 5-02 ($S_\eta$) | 5-03 | 5-04 | 5-06, 5-07 (Bài tập 02.4, bỏ hệ số $K$); 5-08 (hình F4, trả lời câu hỏi mở đầu); 6-08 (bỏ (T4)) | Ví dụ 5-01 là ví dụ dẫn nhập cùng vấn đề, trước trực quan. |
| Hệ quả 02.16 | 5-08 (chưa so với $\min_hL_D(h)$) | 5-09 (hệ số $2$) | 5-09 (Ví dụ 02.9, $1097$) | 5-09 | 5-10 | 5-11 (kỹ thuật; Câu hỏi từ Bài tập 02.3(a)); 7-03 | Ví dụ là dòng kiểm tra sau phát biểu. |
| Mệnh đề 02.17 | 6-00, 6-01 (chỉ cần loại giả thuyết xấu) | 6-01 | 6-01 ($h_4$ dưới $D_f$) | 6-02 | 6-03 | 6-04 (bốn mức cỡ mẫu); 6-05; 6-07 (Bài tập 02.8) | Trực quan, định nghĩa và ví dụ chung trang 6-01. |
| Hai tốc độ (Nhận xét 02.18) | 6-05 (hai cột cuối) | 6-06 | 6-06 (hình F5) | 6-06 | `không áp dụng` (nhận xét) | 6-07 ($140\to280$, $2936\to11\,741$); 7-04 câu 4 | — |

Thời lượng theo mạch (deck cuối): 8 + 15,5 + 19,5 + 17 + 29,5 + 19,5 + 11 = 120 phút; 55 trang.

## 8. Hình vẽ

Mọi hình là SVG trong `2627-1/img/lec-02/`, `role="img"`, có `<title>` và alt cụ thể; màu không là tín hiệu duy nhất (dùng hình dạng điểm, kiểu nét, mẫu gạch); chữ trong hình chỉ là nhãn trục, nhãn điểm và số (Unicode), không công thức; công thức và chú thích nằm ở `figcaption` (KaTeX). Chú thích nêu dữ liệu. Trục lôgarit phải chứa hết dữ liệu. Dữ liệu chính xác lấy từ mục 5.

| Mã | Tệp | Trang | Nội dung và dữ liệu | Alt dự kiến |
|---|---|---|---|---|
| F1 | `tap-trung.svg` | 2-03 | Ba biểu đồ cột xếp dọc, cùng trục ngang $[0;\ 1]$ (vạch $0$; $0{,}12$; $0{,}22$; $0{,}32$; $1$), mỗi biểu đồ có trục dọc riêng. Cột tại $k/m$ cao $\binom mk0{,}22^k0{,}78^{m-k}$, $m=6$ (bảy cột: $0{,}2252;\ 0{,}3811;\ 0{,}2687;\ 0{,}1011;\ 0{,}0214;\ 0{,}0024;\ 0{,}0001$), $m=100$ (đỉnh $0{,}0959$ tại $k=22$), $m=200$ (đỉnh $0{,}0680$ tại $k=44$); vẽ các cột có chiều cao lớn hơn $10^{-4}$. Dải $(0{,}12;\ 0{,}32)$ tô nền nhạt; cột trong dải tô đặc, cột ngoài dải gạch chéo. Nhãn mỗi biểu đồ "m = 6", "m = 100", "m = 200". `figcaption`: "Hàm xác suất của $L_S(h_3)$ dưới $D_\eta$; khối lượng ngoài dải: $0{,}6189$; $0{,}0211$; $8{,}9\cdot10^{-4}$." | "Ba biểu đồ cột của phân bố rủi ro thực nghiệm của ngưỡng 3 dưới dữ liệu có nhiễu, với cỡ mẫu 6, 100 và 200. Dải từ 0,12 đến 0,32 quanh 0,22 được tô nền. Ở cỡ mẫu 6, phần lớn xác suất nằm ngoài dải; ở cỡ mẫu 100 và 200, gần như toàn bộ xác suất nằm trong dải." |
| F2 | `markov.svg` | 2-05 | Trục ngang $v\in[0;\ 2\alpha]$ với vạch "0", "α", "2α"; trục dọc $[0;\ 2\alpha]$. Đường liền: $v\mapsto v$. Đường bậc thang nét đứt: $0$ trên $[0,\alpha)$, $\alpha$ trên $[\alpha,2\alpha]$, chấm đặc tại $(\alpha,\alpha)$, chấm rỗng tại $(\alpha,0)$. Vùng giữa hai đường tô gạch. `figcaption`: "Hàm $v\mapsto v$ và hàm $v\mapsto\alpha\,\mathbb 1[v\ge\alpha]$ trên $[0,2\alpha]$; hàm bậc thang không vượt đường chéo khi $v\ge0$." | "Đường chéo v và hàm bậc thang bằng 0 trước α, bằng α từ α trở đi, trên đoạn từ 0 đến 2α. Hàm bậc thang luôn nằm dưới đường chéo, hai đường chạm nhau tại 0 và tại α." |
| F3 | `day-cung.svg` | 3-02 | Trục ngang $w\in[-0{,}3;\ 0{,}9]$ với vạch $-0{,}22$; $0$; $0{,}78$; trục dọc $[0;\ 5]$. Đường cong liền $e^{2w}$; hai đầu mút $(-0{,}22;\ 0{,}644)$ và $(0{,}78;\ 4{,}759)$ đánh dấu vuông; dây cung nét đứt nối hai điểm. Vạch đứng chấm tại $w=0$; điểm tròn rỗng trên đường cong tại $(0;\ 1)$, điểm tròn đặc trên dây cung tại $(0;\ 1{,}549)$; vạch ngang ngắn gạch chấm tại $1{,}649$. Nhãn số "1,549", "1,649". `figcaption`: "$e^{2w}$ trên $[-0{,}22;\ 0{,}78]$ và dây cung; tại $w=0$, dây cung cao $1{,}549=\mathbb Ee^{2W}$ với $W=V-0{,}22$, $V\sim\mathrm{Bernoulli}(0{,}22)$; cận của bổ đề Hoeffding là $e^{0{,}5}\approx1{,}649$." | "Đường cong hàm mũ e mũ 2w trên đoạn từ âm 0,22 đến 0,78, cùng dây cung nối hai đầu mút. Tại w bằng 0, đường cong có độ cao 1, dây cung có độ cao 1,549, và vạch cận của bổ đề Hoeffding ở độ cao 1,649, cao hơn dây cung." |
| F4 | `ban-kinh-theo-K.svg` | 5-08 | Trục ngang $K$ thang lôgarit từ $1$ đến $10^4$ (vạch $1$; $10$; $100$; $1000$; $10^4$); trục dọc tuyến tính $[0{,}03;\ 0{,}08]$. Năm chấm tròn nối nét liền: $(1;\ 0{,}0387)$, $(10;\ 0{,}0515)$, $(100;\ 0{,}0616)$, $(1000;\ 0{,}0704)$, $(5000;\ 0{,}0759)$; nhãn số tại $K=1$, $1000$, $5000$. `figcaption`: "Bán kính một phía $r_m^{+}=\sqrt{\ln(K/\delta)/(2m)}$ theo $K$, với $m=1000$, $\delta=0{,}05$." | "Bán kính tin cậy một phía theo số ứng viên trên thang lôgarit, với cỡ mẫu 1000 và độ tin cậy 95%. Bán kính bằng 0,0387 khi có một ứng viên, 0,0704 khi có 1000 ứng viên và 0,0759 khi có 5000 ứng viên." |
| F5 | `hai-toc-do.svg` | 6-06 | Trục ngang $\epsilon$ thang lôgarit từ $0{,}01$ đến $0{,}2$ (vạch $0{,}01$; $0{,}02$; $0{,}05$; $0{,}1$; $0{,}2$), trục dọc thang lôgarit từ $10$ đến $10^6$ (vạch $10;\ 10^2;\ \ldots;\ 10^6$). Tam giác nối nét đứt (khả diễn): $39;\ 77;\ 153;\ 381;\ 761$; chấm tròn nối nét liền (bất khả diễn): $415;\ 1659;\ 6636;\ 41\,471;\ 165\,881$, tại $\epsilon=0{,}2;\ 0{,}1;\ 0{,}05;\ 0{,}02;\ 0{,}01$. Nhãn trực tiếp cuối mỗi đường: "khả diễn", "bất khả diễn"; nhãn số tại $\epsilon=0{,}1$ và $0{,}01$ trên cả hai đường ($77$, $761$, $1659$, $165\,881$). `figcaption`: "Cỡ mẫu đủ $\lceil\ln(K/\delta)/\epsilon\rceil$ và $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$ với $K=100$, $\delta=0{,}05$." | "Hai cỡ mẫu đủ theo độ chính xác trên thang lôgarit cả hai trục, với 100 ứng viên và độ tin cậy 95%. Khi độ chính xác giảm từ 0,1 xuống 0,01, cỡ mẫu khả diễn tăng từ 77 lên 761, cỡ mẫu bất khả diễn tăng từ 1659 lên 165 881; đường thứ hai dốc gấp đôi đường thứ nhất." |

## 9. Trang tổng kết

Chi tiết từng trang ở mục 6 (7-01 đến 7-06). Tóm tắt:
- **Bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh`:** sáu hàng: Bổ đề 02.2–02.3, Bổ đề 02.6 với Định lý 02.7, Hệ quả 02.10, Định lý 02.14, Hệ quả 02.16, Mệnh đề 02.17 (7-01).
- **Vấn đề trung tâm:** năm câu trả lời cho cả bài (7-02), không theo mạch.
- **Bài tập tổng hợp:** Bài tập 02.11(a)(b), hàm lỗi có trọng số trong $[0,4]$, $M=17\,539=\lceil16\cdot1096{,}13\rceil$, lời giải trên mặt trang (7-03).
- **Câu hỏi tự kiểm tra:** bốn câu; câu 1–2 là câu hỏi cuối buổi và câu hỏi phụ của ghi chú §11 ($0{,}126$; Bước 2, (T4)); câu 3 (chỗ dùng độc lập và bị chặn); câu 4 (hai tốc độ). Câu trả lời ở ghi chú diễn giả, mỗi câu trả lời được chỉ bằng ghi chú (7-04).
- **Bảng `Mục | Bài tập`:** khớp `exercises.md` (02.1–02.11), mỗi bài một mạch (7-05); liên kết "Ghi chú bài giảng · Bài tập".
- **Tài liệu tham khảo:** UML Phụ lục B.1–B.4 (B.5 đọc thêm), §2.3.1, §§4.1–4.2 (7-06).
- **Câu nối sang Bài 03:** "Bài 03: Chiều VC và hàm phân lớp tuyến tính." (7-06); nội dung cầu nối (lớp vô hạn, đại lượng thay cho $\ln\lvert\mathcal H\rvert$) ở ghi chú diễn giả.

## 10. Bảng thuật ngữ Việt–Anh của deck

Thuật ngữ xuất hiện trên mặt trang, theo ghi chú và `thuat-ngu.md`; cột cuối là trang có tiếng Anh trong ngoặc (lần dùng đầu trên trang nội dung). Thuật ngữ đã có trong Bài 01 vẫn kèm tiếng Anh ở lần đầu trong deck này.

| Tiếng Việt | Tiếng Anh | Trang |
|---|---|---|
| bất đẳng thức hợp | union bound | 1-02 |
| phân bố Bernoulli, phân bố nhị thức | Bernoulli distribution, binomial distribution | 1-02 |
| tối thiểu hóa rủi ro thực nghiệm (ERM) | empirical risk minimization | 1-02 |
| học xấp xỉ với xác suất cao (PAC) | probably approximately correct | 1-02 |
| hàm phân lớp | classifier | 1-06 |
| tập xác thực | validation set | 1-06 |
| độ tin cậy | confidence | 1-06 |
| ứng viên | candidate | 1-06 |
| rủi ro vượt mức | excess risk | 2-01 |
| độc lập cùng phân bố | independent and identically distributed, i.i.d. | 2-01 |
| hàm lỗi 0–1 | 0–1 loss | 2-02 |
| xác suất đuôi | tail probability | 2-03 |
| cận đuôi | tail bound | 2-03 |
| hầu chắc chắn | almost surely | 2-04 |
| bất đẳng thức Markov, bất đẳng thức Chebyshev | Markov's inequality, Chebyshev's inequality | 2-04 (ghi chú diễn giả; tên riêng đã có trong thuật ngữ tiếng Việt) |
| không tương quan từng đôi | pairwise uncorrelated | 2-05 |
| hàm sinh mô-men | moment generating function | 3-01 |
| phương pháp Chernoff | Chernoff method | 3-01 |
| đuôi nặng | heavy tail | 3-01 (ghi chú diễn giả) |
| bổ đề Hoeffding | Hoeffding's lemma | 3-02 |
| dây cung | chord | 3-03 (1-02 ghi chú diễn giả) |
| bất đẳng thức Hoeffding | Hoeffding's inequality | 3-04 |
| cận trên tin cậy | upper confidence bound | 4-01 |
| khoảng tin cậy | confidence interval | 4-01 |
| cận một phía, cận hai phía | one-sided bound, two-sided bound | 4-01 (ghi chú diễn giả) |
| bán kính tin cậy | confidence radius | 4-02 |
| luật số lớn | law of large numbers | 4-06 (ghi chú diễn giả) |
| thiên lệch do chọn | selection bias | 5-01 |
| tập $\epsilon$-đại diện | $\epsilon$-representative sample | 5-02 |
| biến cố hội tụ đều | uniform convergence event | 5-02 |
| bất đẳng thức hợp có trọng số | weighted union bound | 5-04 (ghi chú diễn giả) |
| giả thuyết nhất quán với tập huấn luyện | consistent hypothesis | 6-01 |
| lớp hội Boole | Boolean conjunctions | 6-07 |
| lớp phụ thuộc dữ liệu | data-dependent class | 6-08 |
| dùng lại thích nghi | adaptive reuse | 6-08 |
| hàm lỗi có trọng số | cost-weighted loss | 7-03 |
| nửa không gian | halfspace | 7-06 (ghi chú diễn giả) |

## 11. Rủi ro và điểm cần điều phối viên quyết định

1. **Hộp "Vấn đề trung tâm" (1-05)** lấy câu hỏi trung tâm của ghi chú, viết bằng lời, ≈ 37 âm tiết; dài hơn hộp Bài 01. Phương án ngắn hơn (≈ 28 âm tiết): "Câu hỏi: cần bao nhiêu quan sát để rủi ro thực nghiệm gần rủi ro kì vọng trên một lớp giả thuyết hữu hạn, kể cả khi giả thuyết được chọn theo tập huấn luyện?"
2. **Số trang 54, vượt mục tiêu 45–52, dưới trần 55** (lý do ở mục 3). Phương án rút còn 51, không bỏ bước nào của hành trình khái niệm: (a) gộp 5-02 vào 5-01 (Định nghĩa 02.13 thành dòng cuối của 5-01, bảng $S_\eta$ chuyển vào ghi chú diễn giả); (b) gộp 2-01 vào 1-02 (bảng giả thiết thay dòng "Nhắc lại:" thứ ba, phương sai và Bernoulli chuyển vào ghi chú diễn giả); (c) gộp 5-06 và 5-07 thành một trang chỉ với phần (b) của Bài tập 02.4, lời giải ba dòng. Mỗi phương án bớt 1–1,5 phút; thời gian dư chuyển cho mạch 5.
3. **Bổ đề 02.5 nằm trên trang kỹ thuật 3-01**, không có trang phát biểu và trang ý tưởng chứng minh riêng. Lý do: đây là công cụ (blueprint không xếp nó vào kết quả chính), chứng minh hai dòng, và nội dung của nó chính là kỹ thuật. Nếu điều phối viên xếp nó là kết quả chính: thêm một trang "Ý tưởng chứng minh: phương pháp Chernoff" (55 trang) hoặc kết hợp với phương án 2(a).
4. **"Chia xác suất thất bại $\delta/K$ cho từng giả thuyết" chỉ là dòng "Kỹ thuật." trên 5-04**, không trang riêng: nó ghép bất đẳng thức hợp (kỹ thuật của Bài 01, nhắc lại một dòng theo quyết định khuôn chung) với đảo cận đuôi (trang 4-04). Bài 03 (hàm tăng trưởng thay $K$) và Bài 04 (trọng số $w_k$) dùng lại nó; nếu điều phối viên muốn trang riêng, đặt sau 5-04 (55 trang).
5. **Bước "Markov cho một hàm không âm, tăng" không có trang riêng:** dùng lần đầu ở chứng minh Chebyshev (2-05, ghi chú diễn giả), được gọi tên trên trang kỹ thuật Chernoff (3-01, dòng "Dùng ở").
6. **Trang sát trần 60 âm tiết:** 2-03, 3-01, 4-01, 4-04, 4-06, 5-01, 5-06, 5-09, 5-11, 6-01, 6-03, 6-06, 7-03. Riêng 4-06 (hai thẻ) có thể vượt; nếu vượt, tách thành hai trang "Ví dụ: bản sao của một quan sát" và "Ví dụ: hàm lỗi không bị chặn", rồi dùng một phương án ở điểm 2.
7. **Thứ tự trên mặt trang:** ví dụ đứng sau phát biểu ở 3-02, 3-04, 5-09 vì đó là bước kiểm tra bằng số; 3-04 (ghi chú diễn giả) (Ví dụ 02.4 Bước 1–3) đứng giữa ý tưởng chứng minh 4-03 và trang kỹ thuật 4-04 để giữ thứ tự Bước 1–4 của ghi chú.
8. **Trang bài tập:** 5-06/5-07 (Bài tập 02.4, đề rút gọn câu chữ của ba ý, giữ nguyên dữ kiện, câu hỏi và kết quả), 6-07 (Bài tập 02.8(c)(d)), 7-03 (Bài tập 02.11(a)(b), bài tập tổng hợp). Câu hỏi trên 5-11 lấy ý của Bài tập 02.3(a), đặt dạng câu hỏi mở thay cho "Giải thích vì sao …" để không gợi sẵn câu trả lời; kết quả giữ nguyên. Nếu điều phối viên đòi câu chữ của bài tập, dùng nguyên câu (a).
9. **Ví dụ mới (ghi cách dựng vào `review-log.md` khi duyệt):** N1 bổ đề Hoeffding trên $\mathrm{Bernoulli}(0{,}22)$ với $\tau=2$ (3-02, hình F3; mục 5, V5); N2 cách đọc $0{,}8^m$ cho $h_4$ dưới $D_f$ (6-01; V16); N3 năm mức $\epsilon$ của hình F5 (V19; ba mức $0{,}2$, $0{,}02$, $0{,}01$ ngoài bảng của ghi chú); N4 hai điểm $K=10$, $100$ của hình F4 (V13). Mọi số tính từ công thức của ghi chú, không mâu thuẫn số nào của ghi chú.
10. **Trang tổng quan không kí hiệu:** bìa, Mục tiêu, Nội dung, Vấn đề trung tâm viết bằng lời; "ERM" trên trang Mục tiêu là chữ viết tắt đã giải nghĩa ở 1-02.
11. **Nhãn trong SVG:** F2 dùng "α", "2α" làm nhãn vạch trục; F4, F5 dùng số. Không có công thức trong SVG; công thức ở `figcaption`.
12. **Công thức cần đo ở 390 px:** 3-01 (đẳng thức Chernoff có tích), 3-05, 4-01, 4-04, 5-03, 5-10 (chuỗi ba bất đẳng thức), 6-02 ($M(\epsilon,\delta)$). Ngắt bằng `aligned` chỉ khi tràn (quy tắc của tác giả).
13. **Liên kết hai chiều:** trang 7-05 của deck Bài 01 nhận liên kết tới `lecture-02-bat-dang-thuc-tap-trung.html`; trang 7-06 ở đây là dòng chữ không liên kết cho đến khi deck Bài 03 có tên tệp.
14. **`outline.md` Bài 02 còn thuật ngữ cũ** ("bất khả tri", "khả thực" ở tiêu đề mục 3 và mục tiêu 4); deck theo ghi chú ("bất khả diễn", "khả diễn"). Xem mục 13.

## 12. Bảng đối chiếu trang → mục và khối của ghi chú

Cột "Đưa vào" ghi kí hiệu, thuật ngữ hoặc kết quả xuất hiện lần đầu trên mặt trang (định nghĩa hoặc "Nhắc lại:"), để kiểm quy tắc định nghĩa trước khi dùng.

| Trang | Mục ghi chú | Khối (số của ghi chú) | Đưa vào |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §9 | Định lý 02.14 (bằng lời) | — |
| 1-02 | Kiến thức tiên quyết | Mệnh đề 01.7, Định nghĩa 01.18, 01.25 (nhắc lại); Câu hỏi ôn nhanh (ghi chú diễn giả) | $\mathbb E_S$, $L_S$, $L_D$, bất đẳng thức hợp, $(1-\epsilon)^m\le e^{-\epsilon m}$, $\operatorname{Var}$, $\mathrm{Bernoulli}$, $\mathrm{Bin}$, $K$, $\ln$, ERM, PAC |
| 1-03 | Mục tiêu học tập | — | — |
| 1-04 | toàn bài; §12 | — | — |
| 1-05 | đoạn mở đầu | — | — |
| 1-06 | Câu hỏi mở đầu; §3 | khối ứng dụng | tập xác thực, ứng viên, $h$, $S$, $m$ |
| 2-00 | §1–§4 | — | — |
| 2-01 | §1, §2 | bốn đại lượng; (T1)–(T4), (O1); (O2) ở ghi chú diễn giả | $\hat h$, $\sup_h$, rủi ro vượt mức, (T1)–(T4), (O1) |
| 2-02 | §3; §4 (đoạn đầu) | Ví dụ 02.1 | $D_\eta$, $h_t$, $\eta$, $\ell_{0\text{-}1}$, $S_\eta$ (nhắc lại) |
| 2-03 | §4 | Định nghĩa 02.1, Ví dụ 02.2; Phụ lục B.1 | xác suất đuôi, cận đuôi |
| 2-04 | §4 | Bổ đề 02.2, 02.3 | $\bar V_m$, $\bar\mu_m$, $\sigma^2$, hầu chắc chắn |
| 2-05 | §4 | chứng minh Bổ đề 02.2, 02.3; Bài tập 02.1(a) (cực biên) | không tương quan từng đôi |
| 2-06 | §4 | Ví dụ 02.3; Phụ lục B.1 | — |
| 3-00 | §5 | — | — |
| 3-01 | §5 | Định nghĩa 02.4, Bổ đề 02.5 và chứng minh; đoạn đuôi nặng (ghi chú diễn giả) | hàm sinh mô-men, $\tau$, phương pháp Chernoff |
| 3-02 | §5 | Bổ đề 02.6; Ví dụ 02.1 (biến Bernoulli) | bổ đề Hoeffding |
| 3-03 | §5; Phụ lục A | chứng minh Bổ đề 02.6 | $W$, $a'$, $b'$, $\varphi$, $\rho$, $u$, dây cung |
| 3-04 | §5 | Định lý 02.7; Nhận xét 02.8 và đoạn $\ell_c$, Ví dụ 02.4 Bước 1–3 (ghi chú diễn giả) | bất đẳng thức Hoeffding |
| 3-05 | §5 | chứng minh Định lý 02.7 | — |
| 4-00 | §5 | — | — |
| 4-01 | §5 | Định nghĩa 02.9 và hai đoạn sau | cận trên tin cậy, khoảng tin cậy, $\overline L_\delta$, $\underline L_\delta$ |
| 4-02 | §5 | Hệ quả 02.10 | bán kính tin cậy |
| 4-03 | §5 | chứng minh Hệ quả 02.10 | — |
| 4-04 | §5 | chứng minh Hệ quả 02.10 (Bước 3–5); Ví dụ 02.4, Bước 4 | đảo cận đuôi, $g(m,r)$ |
| 4-05 | §5 | Ví dụ 02.5 | — |
| 4-06 | §5 | Ví dụ 02.6, Nhận xét 02.11 | — |
| 5-00 | §6, §7 | — | — |
| 5-01 | §6 | Ví dụ 02.7; Phụ lục B.2 | $g_j$, thiên lệch do chọn |
| 5-02 | §6 | Định nghĩa 02.13 và bảng sau | tập $\epsilon$-đại diện, biến cố hội tụ đều, $L_s$ |
| 5-03 | §6 | Định lý 02.14 và đoạn sau | $r_m$, $r_m^{+}$ |
| 5-04 | §6; §9 | chứng minh Định lý 02.14; Bổ đề 02.12 (nhắc lại) | $B_h$ |
| 5-05 | §6; §9 | chứng minh Định lý 02.14 (Bước 3–4); §9 (ghi chú diễn giả) | chia xác suất thất bại $\delta/K$ |
| 5-06 | tệp bài tập | Bài tập 02.4 (đề) | $h_k$ |
| 5-07 | tệp bài tập | lời giải Bài tập 02.4 | — |
| 5-08 | §6 | Ví dụ 02.8, Nhận xét 02.15 (ghi chú diễn giả) | — |
| 5-09 | §7 | Hệ quả 02.16; Ví dụ 02.9; Ví dụ 02.10 (ghi chú diễn giả) | $h_{\mathcal H}$, $M(\epsilon,\delta)$ |
| 5-10 | §7 | chứng minh Hệ quả 02.16; Ví dụ 02.12, Bước 3 (ghi chú diễn giả) | — |
| 5-11 | §7; tệp bài tập | chứng minh Hệ quả 02.16 (Bước 2–3); Bài tập 02.3(a), (c) | bước tất định, $E$ |
| 5-12 | tệp bài tập | Bài tập 02.3(a) | — |
| 6-00 | §8, §9 | — | — |
| 6-01 | §8 | đoạn đầu §8; chứng minh Mệnh đề 02.17 (Bước 1); Ví dụ 02.11, Bước 4 | giả thuyết nhất quán, giả thuyết xấu, $D_f$ (giải nghĩa tại chỗ) |
| 6-02 | §8 | Mệnh đề 02.17 và đoạn sau; Ví dụ 02.11, Bước 1 | $\mathcal H_{>\epsilon}$ |
| 6-03 | §8 | chứng minh Mệnh đề 02.17; Ví dụ 02.11, Bước 2 | $h^\star$ |
| 6-04 | §8 | Ví dụ 02.11 | $A_{\max}$ (của Bài 01, giải nghĩa trong ô bảng) |
| 6-05 | §8 | Ví dụ 02.12; Phụ lục B.3 | — |
| 6-06 | §8; §12 | Nhận xét 02.18; Ví dụ 02.12 | — |
| 6-07 | tệp bài tập | Bài tập 02.8(c)(d) | lớp hội Boole, $p$, $\mathcal H_{\mathrm{conj}}$ |
| 6-08 | §9 | — | lớp phụ thuộc dữ liệu, dùng lại thích nghi, $w_k$ |
| 7-00 | §9–§12 | — | — |
| 7-01 | §4–§9 | Bổ đề 02.2, 02.3, 02.6, Định lý 02.7, Hệ quả 02.10, Định lý 02.14, Hệ quả 02.16, Mệnh đề 02.17 | — |
| 7-02 | đoạn mở đầu; §9 | Ví dụ 02.8 (ghi chú diễn giả) | — |
| 7-03 | §5 (đoạn $\ell_c$); tệp bài tập | Bài tập 02.11(a)(b) | $\ell_c$ (nhắc lại) |
| 7-04 | §11 | câu hỏi cuối buổi và lời giải; chứng minh Định lý 02.7, 02.14; Nhận xét 02.18 | — |
| 7-05 | §10; tệp bài tập | Bài tập 02.1–02.11 | — |
| 7-06 | §11, §12 | Ví dụ 02.10 (ghi chú diễn giả) | — |

Kiểm tra thứ tự: đọc cột "Mục ghi chú" từ trên xuống, các mục không giảm (Kiến thức tiên quyết và tệp bài tập là nguồn phụ). Trong §5, thứ tự khối là Định nghĩa 02.4, Bổ đề 02.5, 02.6, Định lý 02.7, Nhận xét 02.8, Định nghĩa 02.9, Hệ quả 02.10, Ví dụ 02.4, 02.5, 02.6, Nhận xét 02.11, đúng thứ tự trên deck. Kí hiệu của Bài 01 trên mặt trang ($S_\eta$, $D_f$, $h^\star$, $A_{\max}$, $\ell_c$) đều có dòng "Nhắc lại:" hoặc giải nghĩa ngay tại chỗ.

## 13. Đề xuất sửa ghi chú và tệp bài tập (không sửa; chờ điều phối viên và tác giả)

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất |
|---|---|---|---|---|
| nhẹ | ghi chú Ví dụ 02.8, Bước 4 | Hiệu hai bán kính là $0{,}0759-0{,}0704=0{,}0055$ (giá trị chưa làm tròn $0{,}07587-0{,}07037=0{,}0055$); câu "chỉ thêm khoảng $0{,}005$" làm tròn xuống | "tăng số ứng viên thêm năm lần chỉ thêm khoảng $0{,}005$." | Không bắt buộc: "chỉ thêm khoảng $0{,}0055$". Deck dùng nguyên "khoảng $0{,}005$" (5-08). |
| nhẹ | ghi chú Bổ đề 02.2, 02.3, Định lý 02.7 (tiêu đề khối) | Tên tiếng Anh của ba bất đẳng thức (Markov's inequality, Chebyshev's inequality, Hoeffding's inequality) có trong `thuat-ngu.md` nhưng không xuất hiện trong ghi chú; bổ đề Hoeffding cũng vậy | Tiêu đề "Bổ đề 02.2 (Bất đẳng thức Markov)", "Định lý 02.7 (Bất đẳng thức Hoeffding)"; đoạn mở đầu chỉ có "(concentration inequality)" | Không bắt buộc (tên riêng nằm sẵn trong thuật ngữ tiếng Việt). Deck thêm tiếng Anh cho bổ đề Hoeffding và bất đẳng thức Hoeffding ở 3-02, 3-04. |
| nhẹ | `planning/lec-02/outline.md` §1 (mục tiêu 4), §3 (tiêu đề `## 7`, `## 8`) | Tệp kế hoạch còn "bất khả tri", "khả thực" sau quyết định thuật ngữ 2026-11-01 của tác giả; ghi chú đã dùng "bất khả diễn", "khả diễn" | "`## 7. ERM trên lớp hữu hạn trong trường hợp bất khả tri`", "`## 8. Lớp hữu hạn trong trường hợp khả thực`" | Đồng bộ thuật ngữ trong `outline.md` (không phải tệp cho người học). |

Không thấy lỗi toán học trong các khối deck dùng; mọi con số của ví dụ đã tính lại (mục 5).

## 14. Danh sách kỹ thuật đã giới thiệu đến hết Bài 02

Mã trang Bài 01 theo deck Bài 01 hiện hành (`lecture-01-mo-hinh-hoc.html`).

| Kỹ thuật | Bài, trang (lần đầu) | Dạng | Trong deck Bài 02 |
|---|---|---|---|
| Tính tuyến tính của kì vọng | Bài 01, 3-03 | một dòng "Kỹ thuật." | nhắc qua Mệnh đề 01.7 ở 1-02 |
| Bất đẳng thức hợp | Bài 01, 4-04 | trang riêng | "Nhắc lại:" ở 5-04 (Bổ đề 02.12); dùng ở 5-05, 6-03 |
| Chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ | Bài 01, 6-07 | trang riêng | "Nhắc lại:" ở 6-01; bước 1 của 6-03 |
| Tối thiểu hóa từng điểm rồi lấy kì vọng | Bài 01, 5-09 | một dòng | không dùng |
| Phương pháp Chernoff (Markov cho $e^{\tau V}$, tách tích bằng độc lập, chọn $\tau$) | Bài 02, 3-01 | trang riêng | dùng ở 3-05 |
| Dây cung của hàm lồi và Taylor bậc hai tại $0$ | Bài 02, 3-03 | một dòng (chỉ trong chứng minh bổ đề Hoeffding) | — |
| Đảo cận đuôi thành bán kính và cỡ mẫu | Bài 02, 4-04 | trang riêng | dùng ở 5-04, 5-05, 5-10, 6-03 |
| Chia xác suất thất bại $\delta/K$ (hoặc $w_k\delta$) cho từng giả thuyết | Bài 02, 5-05 | trang riêng (quyết định của điều phối viên, mục 11.4) | ghi chú diễn giả 6-08 (Chebyshev, trọng số) |
| Bước tất định trên biến cố đại diện | Bài 02, 5-11 | trang riêng | kiểm tra ở 5-12; dùng ở 7-03 |

Deck Bài 03 trở đi nhắc lại các kỹ thuật có trang riêng bằng tên, một dòng "Nhắc lại:".

## 15. Đối chiếu storyboard ↔ deck đã viết (người viết deck, 2026-11-15)

Deck: `2627-1/lecture-02-bat-dang-thuc-tap-trung.html`, **55 trang** (bảy mạch, sáu trang tiêu đề mạch). Hình: `img/lec-02/tap-trung.svg` (F1), `markov.svg` (F2), `day-cung.svg` (F3), `ban-kinh-theo-K.svg` (F4), `hai-toc-do.svg` (F5); tọa độ tính bằng script từ các công thức của mục 5 (V2, V5, V13, V19). Người viết deck không đọc thêm trang UML nào ngoài các trang ghi ở đầu tệp.

**Bảng đổi mã trang** (đã áp dụng cho toàn tệp, trừ mã của Bài 01):

| Storyboard đã duyệt | Deck |
|---|---|
| 4-04 (Ví dụ: ba cách chặn) | bỏ trang; nội dung vào ghi chú diễn giả `3-04` |
| 4-05, 4-06, 4-07 | 4-04, 4-05, 4-06 |
| — | 5-05 (kỹ thuật chia $\delta/K$, mới) |
| 5-05, 5-06, 5-07, 5-08, 5-09, 5-10 | 5-06, 5-07, 5-08, 5-09, 5-10, 5-11 |
| câu hỏi trên 5-10 | 5-12 (Bài tập 02.3(a), trang mới) |

**Chỗ lệch và lý do.**

1. **Quyết định của điều phối viên đã áp dụng:** hộp Vấn đề trung tâm bản ngắn (1-05); sáu mục tiêu theo số của ghi chú, bằng lời (1-03, 79 âm tiết, trần 80); tiêu đề "Đảo cận đuôi thành bán kính và cỡ mẫu" (4-04); trang kỹ thuật chia $\delta/K$ riêng sau ý tưởng chứng minh Định lý 02.14 (5-05); câu hỏi dùng nguyên câu chữ Bài tập 02.3(a) (5-12); mọi phát hiện được chấp nhận của cổng duyệt: 6-04 thêm "mọi phân bố khả diễn" (cột "Phân bố khả diễn"); 6-01 mở bằng ví dụ $h_4$ dưới $D_f$; 4-01 mở bằng định nghĩa có danh từ (không "Cho $\ell$ …"); 3-03, 5-10 không chép chứng minh ($\theta$, $\varphi$, $\rho$ ở ghi chú diễn giả; ba dấu $\le$ ghi một dòng); 5-06/5-07 giữ $K=5000$, "không mâu thuẫn với Định lý 02.14(a)" và "trên đó độ lệch $\tfrac12\ge0{,}4$"; 3-01 có nhãn Giả thiết/Bảo đảm, $\alpha\in\mathbb R$, bỏ câu sai về $x\mapsto x^2$ (câu "bước đầu là Markov cho $e^{\tau V}$, như Chebyshev là Markov cho $(V-\mathbb EV)^2$" chuyển vào ghi chú diễn giả để giữ mật độ); 3-02 có $a<b$; 2-03 định nghĩa cả đuôi trên; 1-02 có $\delta$ và "khả diễn"; 4-06 thẻ phải ghi i.i.d.; 6-08 có $w_k\ge0$; 5-09 ghi chú diễn giả nêu phần (b); 7-03 lời giải có bất đẳng thức hợp (ở ghi chú diễn giả, xem điểm 6); các đầu câu "Dùng khi", "Bỏ …", "Dấu bằng …" viết chữ thường, không in đậm; ghi chú diễn giả bỏ mọi câu quy trình, số mạch, câu thiếu vị ngữ mà cổng duyệt nêu; 7-01 ghi đúng ví dụ Bài tập 02.4.
2. **Bỏ trang so ba cận (cũ 4-04), để giữ 55 trang.** Hai quyết định "trang kỹ thuật $\delta/K$ riêng" và "câu hỏi dùng nguyên câu chữ Bài tập 02.3(a)" cộng với trần 60 âm tiết không đặt được trên 54 trang: câu chữ của Bài tập 02.3(a) đã 58 âm tiết (deck_check), nên không ghép được với trang kỹ thuật bước tất định (19 + 19 âm tiết). Trang cũ 4-04 là trang dư thừa nhất theo cổng duyệt (lặp hàng chính xác và hai hàng Chebyshev của 2-06; hàng Hoeffding đã ở 3-04). Nội dung riêng của nó (thứ tự các cận, $m\le107$, tỉ số $8$, $12$, $13$) ở ghi chú diễn giả 3-04; "khoảng 13 lần" còn ở ghi chú diễn giả 7-02. **Điều phối viên cần xác nhận.** Phương án thay thế: gộp chiến lược khác (ví dụ bỏ 6-07) hoặc cho phép 56 trang.
3. **5-12 (Bài tập 02.3(a))**: lời giải nằm ở ghi chú diễn giả, không ở mặt trang, vì mặt trang đã 59 âm tiết; bài chính của cụm là Bài tập 02.4 (5-06, 5-07) với lời giải trên mặt trang (quy tắc của `brief-writer.md`).
4. **Dòng dẫn mạch** viết lại theo bài học deck 01 (câu trần thuật về nội dung, không "Người học …"); ghi chú diễn giả của trang tiêu đề mạch viết câu thường, không nhãn "Kế thừa/Nhiệm vụ", không nói về chính văn bản ("Phần này …").
5. **Câu nối trên mặt trang** (bài học deck 01): 2-06 "Cận Chebyshev chỉ giảm như $1/m$; cần dùng thêm tính bị chặn."; 4-05 "Bảo đảm cần $h$ cố định trước khi xem $S$."; các mạch khác nối bằng dòng dẫn mạch.
6. **Rút mặt trang để giữ mật độ** (văn xuôi chuyển vào ghi chú diễn giả): 2-01 (bốn đại lượng thành một dòng), 2-03 (bỏ "Diễn giải:"), 2-06 (bỏ dòng dữ kiện, ghi vào đầu bảng; bỏ dòng "$V\in[0,1]$ … $500$", số $500$ ở 4-04), 3-02 (ví dụ đặt sau phát biểu, như storyboard), 3-04 (bỏ "Diễn giải:"), 4-01 (ý nghĩa "95 trong 100 lần" vào ghi chú), 4-02 (trực quan "gấp bốn cỡ mẫu" vào ghi chú), 4-06 (hai cột không dùng `card`, để không vượt quy định một hộp), 5-08 (câu điều kiện hóa theo $T$ rút còn một dòng), 5-11 (dòng "Dùng khi" rút gọn), 7-03 (dòng lời giải "Định lý 02.7 trên $[a,b]$ và bất đẳng thức hợp …" vào ghi chú diễn giả; mặt trang giữ dữ kiện, câu hỏi, hai dòng lời giải với $17\,539$ và $16\cdot1096{,}13$), 7-04 (ba câu: bỏ câu "Hoeffding dùng độc lập và bị chặn ở bước nào", vì 3-05 đã trả lời trên mặt trang), 7-01 (cột "Kết quả" ghi tên kết quả, không ghi công thức, để bảng vừa khung; công thức ở 7-02).
7. **Bảng `Mục | Bài tập`** (bài học deck 01: xếp vào mạch cung cấp kiến thức cuối cùng): 02.1 → mạch 3 (phần (e), (f) cần Định lý 02.7); 02.2, 02.10 → mạch 4 (02.2(d) cần Định nghĩa 02.9; 02.10(c) so với cỡ mẫu Hoeffding của Ví dụ 02.4); 02.3, 02.4, 02.5, 02.11 → mạch 5 (02.5(d) cần Ví dụ 02.7); 02.6, 02.7, 02.8, 02.9 → mạch 6 (02.6: họ đếm được có trọng số của §9). Mạch 2 không có dòng.
8. **Hình:** nhãn trong SVG chỉ là chữ và số ("đường chéo", "hàm bậc thang", "hàm mũ", "dây cung", "khả diễn", "bất khả diễn"), không công thức; F1: cột đúng trên vạch $0{,}12$, $0{,}32$ thuộc biến cố đuôi (gạch chéo ở $m=6$, màu khác ở $m=100$, $200$); F3: đường cong vẽ trên $[-0{,}22;\ 0{,}78]$, hai nhãn $1{,}549$ và $1{,}649$ ở hai phía của vạch $w=0$; không dùng `figcaption`, dữ liệu nằm trong alt và ghi chú diễn giả.
9. **Ghi chú diễn giả 1-04** giữ dòng đọc trước (UML Phụ lục B.1–B.2, §2.3.1), không đặt trên mặt trang.

**Mật độ (deck_check, âm tiết mặt trang):** 1-01 60; 1-02 60; 1-03 79; 1-04 48; 1-05 35; 1-06 51; 2-00 41; 2-01 48; 2-02 23; 2-03 30; 2-04 44; 2-05 47; 2-06 37; 3-00 34; 3-01 43; 3-02 40; 3-03 47; 3-04 50; 3-05 51; 4-00 38; 4-01 53; 4-02 45; 4-03 41; 4-04 39; 4-05 36; 4-06 45; 5-00 39; 5-01 52; 5-02 41; 5-03 50; 5-04 47; 5-05 40; 5-06 52; 5-07 52; 5-08 37; 5-09 56; 5-10 46; 5-11 42; 5-12 59; 6-00 45; 6-01 59; 6-02 45; 6-03 48; 6-04 55; 6-05 41; 6-06 37; 6-07 47; 6-08 54; 7-00 25; 7-01 68; 7-02 58; 7-03 56; 7-04 54; 7-05 45; 7-06 57. Không trang nào vượt trần 60, trừ **7-01 "Bảng tổng kết" (68, trần 80 của bảng tổng kết)**; deck_check gắn cờ SYLL ở trang này vì so khóa "Tổng kết" phân biệt chữ hoa, còn tiêu đề là "Bảng tổng kết". Các trang kết quả (3-04, 4-01, 5-03, 5-09, 6-01) ở mức 50–59 vì giữ đủ "Giả thiết:"/"Bảo đảm:" và tên tiếng Anh lần đầu. Dòng trên 20 âm tiết còn ở 1-01 (luận điểm), 1-05 (hộp câu hỏi), 1-06 (câu hỏi thứ hai, 23), 4-01 (định nghĩa, 21), 5-12 (đề bài nguyên văn).

**Kiểm tra máy:** console 0, page errors 0, failed 0, không `.katex-error`. Cờ OVERFLOW còn ở 4-02, 4-04, 4-05, 5-03, 5-08 đều là đuôi SVG của `\sqrt` (đã kiểm phần tử: `path`), báo động giả đã biết. Ở 390 px, trang không cuộn ngang (`docScrollW = 390`); các công thức hiển thị và bảng rộng cuộn ngang tại chỗ.

## 16. Sửa sau năm báo cáo duyệt (người sửa deck, 2026-11-15)

Đầu vào: `reviews/deck-{hoc-vien,toan-hoc,chuyen-gia,su-pham,mach-truyen}.md` và quyết định của điều phối viên trong `review-log.md` (mục "Năm báo cáo duyệt và quyết định của điều phối viên"). Số trang giữ 55, mã trang không đổi. Mục 15 vẫn đúng, trừ các điểm đổi ở bảng dưới; riêng bảng `Mục | Bài tập` (mục 15, điểm 7) nay xếp 02.6 vào mạch 5, và Ví dụ 02.4 Bước 1–3 nay có bảng trên mặt trang 3-04 (mục 12, hàng 3-04).

### Học viên (`deck-hoc-vien.md`)

| # | Phát hiện | Kết quả |
|---|---|---|
| 1 | 3-05, 5-04, 5-10: chữ bị cắt ở 390 px | đã sửa (điều phối viên sửa `lecture-course.css`, commit 9c34228); kiểm lại ảnh 390×844 và `-end` của ba trang: chữ xuống dòng, công thức cuộn tại chỗ |
| 2 | 3-02, 5-08 đè chân trang | đã sửa: 3-02 rút dòng ví dụ thành "$1{,}549\le e^{0{,}5}\approx1{,}649$" (phép tính vế trái vào ghi chú diễn giả); 5-08 đổi bố cục (hình bên trái, rộng 2/5), bỏ dòng $K=5000$ khỏi mặt trang (ở ghi chú diễn giả và trên hình). `footer_check.py` báo 0 trang |
| 3 | 3-03: $\varphi$ chưa định nghĩa | đã sửa: bước 2 ghi $\varphi(u)=-\theta u+\ln(1-\theta+\theta e^u)$, $\theta=-a'/(b-a)$ |
| 4 | 5-10: (O2), $\epsilon_{\mathrm{opt}}$ chưa có trước đó | đã sửa: viết thẳng ở 5-10 "với nghiệm ERM xấp xỉ (O2), $L_S(\hat h)\le\min_hL_S(h)+\epsilon_{\mathrm{opt}}$"; không thêm hàng vào bảng 2-01 vì trang đó chạm chân trang |
| 5 | 6-04 đi quá nhanh | đã sửa: thêm cột "Số hạng" ($6$; $2$; $1$; —) và "Diễn giải:" nêu hai chuỗi lồng nhau ở mỗi bên $t^\star$, $A_{\max}$ chỉ còn bên phải |
| 6 | 1-02 (64), 7-06 (61) khi tính số | đã sửa: 1-02 còn 56, 7-06 còn 53 (đếm cả số trong câu) |
| 7 | Chữ trong hình nhỏ; nhãn "1,549" bị dây cung cắt | nhãn: đã sửa (đặt "1,549" ra ngoài, nối bằng đường dẫn); cỡ chữ: không sửa, điều phối viên chấp nhận như giới hạn đã ghi ở Bài 01 |
| 8 | "Trực quan." 3-04, 4-02, 5-03 lặp kết quả | đã sửa: 3-04 "Cận chỉ dùng độ dài $b-a$, nên đúng cho mọi phân bố trên $[a,b]$"; 4-02 "Cộng vào $L_S(h)$ một bán kính tin cậy; gấp bốn cỡ mẫu thì bán kính giảm một nửa"; 5-03 câu của chuyên gia (mọi $h$ gần thì $\hat h$ cũng gần; giá $\ln K$) |
| 9 | 2-03 ghép số theo vị trí | đã sửa: "$m=6$: $0{,}6189$; $m=100$: $0{,}0211$; $m=200$: $8{,}9\cdot10^{-4}$" |
| 10 | 2-01 bốn đại lượng một dòng | đã sửa: danh sách hai cột |
| 11 | 2-02 chưa gọi tên $D_\eta$ | đã sửa: "Phân bố có nhiễu $D_\eta$: …" |
| 12 | 6-01 "Nhắc lại:" đứng sau công thức | đã sửa: lên đầu trang, gộp với $D_f$ |
| 13 | 5-08 câu điều kiện hóa khó hiểu | đã sửa: "Khi biết tập huấn luyện $T$ (độc lập với $S$), $K$ ứng viên cố định và $S\sim D^m$" |
| 14 | 6-07 số $2\,362\,000$ không nguồn | đã sửa: "Theo Hệ quả 02.16(c), $2K/\delta=2\,362\,000$: …" |
| 15 | 7-04 câu 1 thiếu chủ ngữ, 24 âm tiết | đã sửa: "Hàm chọn trong $200$ ứng viên, tỉ lệ lỗi …: tính cận trên tin cậy $95\%$"; vế "cận đúng cho hàm nào" thành câu riêng (4 câu) |
| 16 | 1-03 "hệ số số ứng viên" | đã sửa: "bỏ tính độc lập, tính bị chặn hoặc hệ số đếm ứng viên" (80 âm tiết, trần) |
| 17 | 5-09/7-03 thiếu số Ví dụ 02.9 | đã sửa: 5-09 ghi "(Ví dụ 02.9)" |
| 18 | Dòng vượt trần không ghi lý do; hộp 1-05 35 âm tiết | đã sửa: hộp 1-05 còn 28 âm tiết theo khuôn (deck_check đếm 33 vì tính nhãn "Câu hỏi:" và các từ trong hộp); dòng dẫn 2-00 rút; 6-00 viết lại (22 âm tiết). Dòng trên 20 âm tiết còn lại có lý do ở cuối mục này |

### Toán học (`deck-toan-hoc.md`)

| # | Phát hiện | Kết quả |
|---|---|---|
| P1 | 5-09 ví dụ thiếu loại bảo đảm | đã sửa: "$M=1097$; với xác suất $\ge0{,}95$, $L_{D_\eta}(\hat h)\le0{,}32$" |
| P2 | 7-02 thiếu "với xác suất ít nhất $1-\delta$" | đã sửa: câu dẫn chung "Với xác suất ít nhất $1-\delta$ theo $S$:" cho cả danh sách; dòng khả diễn nêu $L_D(\hat h)\le\epsilon$ |
| P3 | 7-03 phần (a) bỏ giả thiết; số làm tròn | đã sửa giả thiết: "(T1), (T4), $0\le a\le\ell\le b$"; số giữ theo `exercises.md` (đề xuất sửa tệp bài tập đã ở `review-log.md`) |
| P4 | 7-01 Chebyshev "độc lập" | đã sửa: "không tương quan từng đôi" |
| P5 | 3-01 gộp hai phần Bổ đề 02.5 | đã sửa: Giả thiết "(a) $V$ bất kì …; (b) $V_i$ độc lập", công thức đánh dấu $\overset{(a)}{\le}$, $\overset{(b)}{=}$; "mọi $\tau\in\mathbb R$" của (b) ở ghi chú diễn giả |
| P6 | 5-04 "biến cố hỏng", "vế phải" mơ hồ | đã sửa: "$\{S$ không là $r$-đại diện$\}\subseteq\bigcup_hB_h$"; "$\sum_h\Pr(B_h)$ gấp $K$ lần" |
| P7 | 4-06 không nói áp dụng sai; "Lưu ý" thiếu miền $\epsilon$ | đã sửa |
| P8 | 4-01 khoảng tin cậy "thêm cận dưới" | đã sửa: viết đủ $\Pr[\underline L_\delta(S)\le L_D(h)\le\overline L_\delta(S)]\ge1-\delta$ |
| P9 | 2-03 thiếu đuôi dưới | đã sửa: "đuôi trên, dưới: $\Pr(\pm(V-\mathbb EV)\ge\epsilon)$" |
| P10 | Lượng từ (T2)/(T3), Bổ đề 02.3(b) | đã sửa: "$\forall h\in\mathcal H$", "$\forall h,z$", "$\forall i$" |
| P11 | 1-02 "$\epsilon$ độ chính xác" | đã sửa: bỏ $\epsilon$ khỏi dòng "Kí hiệu:"; ba nghĩa của $\epsilon$ ở ghi chú diễn giả 1-02 và "Lưu ý:" 6-05 |
| P12 | 6-01, 6-06 thiếu "hàm lỗi 0–1" | đã sửa |
| P13 | Ghi chú diễn giả 1-05 thiếu loại bảo đảm | đã sửa |
| P14 | `tap-trung.svg` cột $k=2$ đè vạch $0{,}32$ | đã sửa: cột khung $m=6$ rộng $20$ đơn vị, mỗi cột nằm trọn một phía vạch |

### Chuyên gia (`deck-chuyen-gia.md`)

| # | Phát hiện | Kết quả |
|---|---|---|
| 1 | 3-04 mất so sánh Hoeffding–Chebyshev | đã sửa theo quyết định của điều phối viên: bảng $m=100$, $200$ × chính xác / Chebyshev $25/m$ / Hoeffding và "Diễn giải:" trên 3-04; tỉ số $13$ lần ở ghi chú diễn giả |
| 2 | 3-04 "Trực quan." là bước chứng minh | đã sửa (câu ngắn: "Cận chỉ dùng độ dài $b-a$, nên đúng cho mọi phân bố trên $[a,b]$") |
| 3 | 6-05 cấm so giữa các cột | đã sửa theo quyết định: "cột ước lượng dùng $\epsilon$ là độ lệch; khi $D$ khả diễn, hai cột sau so được"; đề xuất sửa Ví dụ 02.12 do điều phối viên ghi |
| 4 | 6-06 "cần $m$ cỡ $1/\epsilon^2$" | đã sửa: "cỡ mẫu đủ tỉ lệ với $1/\epsilon^2$"; ghi chú diễn giả 7-04 cũng dùng "cỡ mẫu đủ" |
| 5 | 7-02 bỏ loại bảo đảm | đã sửa (như P2) |
| 6 | 5-03 "Trực quan." chỉ nêu giá | đã sửa |
| 7 | 5-09 ví dụ thiếu bảo đảm | đã sửa (như P1) |
| 8 | 7-01 Chebyshev "độc lập"; Mệnh đề 02.17 thiếu hàm lỗi 0–1 | đã sửa; (T2) của Hệ quả 02.10, Định lý 02.14 giữ ở ghi chú diễn giả |
| 9 | 3-01 độc lập gộp cho cả bất đẳng thức | đã sửa (như P5) |
| 10 | 3-03 thiếu $\mathbb EW=0$ | đã sửa |
| 11 | 5-11 thiếu đối chiếu Mệnh đề 01.15 | đã sửa ở ghi chú diễn giả, nguồn §9, Mệnh đề 01.15 |
| 12 | 1-01 luận điểm thiếu "lớp chọn trước" | đã sửa: "lớp hữu hạn chọn trước" |
| 13 | 5-08 thiếu "độc lập với $S$" | đã sửa |

### Sư phạm (`deck-su-pham.md`)

| # | Phát hiện | Kết quả |
|---|---|---|
| 1 | 1-02 chữ viết tắt trước tên tiếng Việt | đã sửa |
| 2 | Ghi chú diễn giả 1-03 câu quy trình | đã sửa (xóa) |
| 3 | 1-03 mục tiêu 6 sai ngữ pháp | đã sửa |
| 4 | 6-00, 1-04 "một hàm không sai" | đã sửa: "chứa một hàm có rủi ro $0$"; 6-00 dùng "giả thuyết có rủi ro lớn" thay "giả thuyết xấu" |
| 5 | Trang đầu ví dụ chưa thành danh sách; 2-01 | đã sửa: 1-06, 2-02, 4-05, 5-01 có danh sách dữ kiện; 2-01 danh sách |
| 6 | 2-03 cấu trúc "lần lượt" | đã sửa |
| 7 | 4-01 dòng không vị ngữ về một/hai phía | đã sửa: "…, cận hai phía (two-sided bound): …; cận trên tin cậy là cận một phía (one-sided bound)"; bỏ câu tương ứng ở ghi chú diễn giả |
| 8 | 4-06 câu dồn, thiếu kết luận | đã sửa: mỗi cột nêu "cận sai" / "cận không cho thông tin"; giữ một đoạn mỗi cột để không vượt sáu dòng |
| 9 | 5-05 "bán kính tăng theo $\ln K$" | đã sửa: "$\ln(2/\delta)$ dưới dấu căn thành $\ln(2/\delta)+\ln K$" |
| 10 | 5-06 nhãn "Học viên:" | đã sửa theo quyết định: hộp mở bằng "Câu hỏi: một học viên lập luận: "…"", câu chữ của bài tập, có "Hệ quả 02.10(a)" |
| 11 | 5-12 công thức thiếu điều kiện | đã sửa: thêm công thức hiển thị điều kiện $\sup_h\lvert L_S-L_D\rvert\le r$, $\hat h\in\arg\min L_S$, $h_{\mathcal H}\in\arg\min L_D$ (viết bằng kí hiệu để giữ trần 60 với câu chữ nguyên văn của bài tập) |
| 12 | "Trực quan." 3-04, 4-02, 5-03, 5-09 | đã sửa 3-04, 4-02, 5-03; 5-09 giữ ("hai phép so", người duyệt nói giữ được) |
| 13 | Lặp câu qua nhiều ghi chú diễn giả | đã sửa: bỏ ở 4-02, 4-05 (điều kiện $h$ cố định), 6-08, 7-02 (bảo thủ), 6-00 (hai biến cố) |
| 14 | Ghi chú diễn giả 7-00 nói về các trang | đã sửa: viết nội dung (ba giả thiết, $\ln K$, hai tốc độ) |
| 15 | 6-01 "Nhắc lại:" sau công thức; tiêu đề rút tên thuật ngữ | đã sửa: "Giả thuyết nhất quán với tập huấn luyện và giả thuyết xấu" |
| 16 | Ghi chú 1-05 câu điều hướng | đã sửa (xóa) |
| 17 | 1-06 mảnh câu "và khi …", thiếu "được" | đã sửa |
| 18 | 1-02 "Nhắc lại:" chỉ tên | đã sửa: nêu định nghĩa khả diễn |
| 19 | 2-01 i.i.d. thiếu tên tiếng Anh | đã sửa |
| 20 | 2-02 tên phân bố treo sau công thức | đã sửa |
| 21 | Ghi chú 2-02 "mẫu" | đã sửa: "tập huấn luyện" |
| 22 | 2-03 "nó" không rõ | đã sửa |
| 23 | Ghi chú 2-00, 3-00 "không phụ thuộc phân bố đúng"; "Câu hỏi … đòi" | đã sửa |
| 24 | 3-01 thiếu "dùng ở" | đã sửa: "dùng ở Định lý 02.7" |
| 25 | Ghi chú 3-02 văn bản làm chủ ngữ | đã sửa |
| 26 | 4-04, 6-07 hai dấu hai chấm | đã sửa |
| 27 | Ghi chú 4-01 "muốn …, cần …" | đã sửa |
| 28 | Ghi chú 4-06 câu chẻ | đã sửa |
| 29 | 5-01 "Diễn giải:" | đã sửa: "ứng viên được chọn có tỉ lệ lỗi lệch xuống so với $0{,}07$, gọi là thiên lệch do chọn"; câu so $0{,}00593$ với $0{,}9974$ không thêm vì trần 60 (hai số đã ở hai dòng ngay trên) |
| 30 | 5-08 câu sai ngữ pháp | đã sửa: vế "gấp năm lần $K$" bỏ khỏi mặt trang theo quyết định về 5-08 |
| 31 | Ghi chú 3-04, 5-08, 5-09 dài | đã sửa: bỏ đoạn $\ell_c$ (3-04), câu cận tổng quát hóa (5-08), lớp $K=32$ và phủ định "không loại trừ" (5-09) |
| 32 | Ghi chú 5-12 "Lời giải." | đã sửa: "Lời giải:" |
| 33 | 6-04 "ngưỡng xấu" lồng nhau, "mỗi bước xuống" | đã sửa: "biến cố "ngưỡng xấu $t$ nhất quán" lồng nhau ở mỗi bên $t^\star$" trong "Diễn giải:"; câu "mỗi hàng dùng thêm cấu trúc …" ở ghi chú diễn giả |
| 34 | 6-08 thiếu "được"; $2120$ không nói cận nào | đã sửa |
| 35 | 7-03 FP, FN; "Phần (a):" | đã sửa: "âm tính giả tốn $4$, dương tính giả tốn $1$" (không dùng chữ viết tắt trên mặt trang); "Theo phần (a), …"; 5-09 có "(Ví dụ 02.9)" |
| 36 | Ghi chú 7-05 câu quy trình | đã sửa (xóa) |
| 37 | "Bảo đảm" không dấu hai chấm (4-02, 5-03, 5-09, 6-02) | đã sửa |
| 38 | `hai-toc-do.svg` "1 659" | đã sửa: "1659" (chỉ tách nhóm từ năm chữ số) |

### Mạch truyện (`deck-mach-truyen.md`)

| # | Phát hiện | Kết quả |
|---|---|---|
| 1 | Câu nối 5-01 → 5-02 | đã sửa: dòng đầu 5-02 "Ứng viên được chọn theo $S$, nên cần một biến cố đúng đồng thời cho mọi $h\in\mathcal H$" |
| 2 | Câu nối 5-08 → 5-09 | đã sửa: dòng cuối 5-08 "Rủi ro vượt mức so $L_D(\hat h)$ với $\min_hL_D(h)$, không với $L_S(\hat h)$" |
| 3 | 5-08 không trả lời câu hỏi thứ hai | đã sửa theo quyết định: "Diễn giải:" "với độ tin cậy $95\%$, hàm chọn trong $1000$ ứng viên có rủi ro kì vọng không quá $0{,}1204$"; bỏ "khoảng $0{,}005$" |
| 4 | Thiếu so sánh Hoeffding–Chebyshev | đã sửa (như chuyên gia 1) |
| 5 | 7-01 ô "độc lập" | đã sửa (như P4) |
| 6 | 4-01 → 4-02 thiếu câu về bán kính | đã sửa ("Trực quan." của 4-02) |
| 7 | 4-05 lặp điều kiện; câu khép mạch 4 | đã sửa: bỏ dòng cuối 4-05 (dòng dữ kiện đầu trang còn điều kiện); không thêm câu khép mạch ở 4-06 vì trang đã sáu dòng, dòng dẫn 5-00 và ví dụ 5-01 nối sang mạch 5 (người duyệt chấp nhận phương án này) |
| 8 | 2-03 lý do chuyển sang cận đuôi | đã sửa: "Cận đuôi (tail bound): một cận trên của xác suất đuôi, tính được khi chưa biết $D$", số chính xác ghi "dưới $D_\eta$" |
| 9 | Mạch 2 chứa khung chung | đã sửa: thêm "giả thiết (T1)–(T4)" vào từ khóa mạch 2 |
| 10 | 6-01 "Nhắc lại:" và $D_f$ | đã sửa |
| 11 | 6-04 hàng $30$ thiếu Mệnh đề 01.31 | đã sửa: "$30$ (Mệnh đề 01.31)" |
| 12 | 7-05 Bài tập 02.6 | đã sửa: chuyển vào hàng mạch 5 |
| 13 | Ghi chú 7-00 nói về các trang | đã sửa (như sư phạm 14) |
| 14 | 1-03 mục tiêu 6 | đã sửa |
| 15 | Deck 01 "$>\epsilon$" | không sửa: ngoài phạm vi deck 02 (quyết định của điều phối viên) |
| 16 | Đuôi nặng lặp ở ghi chú 3-01, 3-03 | đã sửa: giữ ở 3-03 |
| 17 | 7-03 ↔ 5-09 số Ví dụ 02.9 | đã sửa |

### Kiểm tra sau khi sửa

- `deck_check.py --shots` (thư mục nháp `…/scratchpad/lec-02/editor/`): 55 trang, console 0, page errors 0, failed 0, không `.katex-error`. OVERFLOW còn ở 4-02, 4-04, 4-05, 5-03, 5-08, 6-06, đều là đuôi SVG của `\sqrt` (phần tử `path`), báo động giả đã biết. Ở 390 px trang không cuộn ngang; công thức hiển thị và bảng rộng cuộn tại chỗ.
- `footer_check.py`: 0 trang chạm chân trang ở 1600×900.
- Phím: ↓, →, Space, Esc (tổng quan) hoạt động; sáu liên kết `#/2`…`#/7` của "Nội dung" tới đúng `L02-k-00`.
- Mật độ, đếm cả số trong câu (số KaTeX chỉ gồm chữ số, số hiệu kết quả, năm): 1-01 59; 1-02 56; 1-03 80 (trần 80); 1-04 48; 1-05 33; 1-06 59; 2-00 36; 2-01 43; 2-02 31; 2-03 38; 2-04 46; 2-05 37; 2-06 39; 3-00 34; 3-01 50; 3-02 37; 3-03 52; 3-04 60; 3-05 51; 4-00 38; 4-01 56; 4-02 58; 4-03 43; 4-04 47; 4-05 31; 4-06 57; 5-00 39; 5-01 59; 5-02 58; 5-03 57; 5-04 45; 5-05 41; 5-06 55; 5-07 56; 5-08 53; 5-09 59; 5-10 52; 5-11 43; 5-12 59; 6-00 46; 6-01 55; 6-02 47; 6-03 49; 6-04 52; 6-05 44; 6-06 51; 6-07 54; 6-08 59; 7-00 25; 7-01 68 (trần 80 của bảng tổng kết; deck_check gắn cờ SYLL vì so khóa "Tổng kết" phân biệt chữ hoa); 7-02 56; 7-03 57; 7-04 60; 7-05 45; 7-06 53.
- Dòng trên 20 âm tiết còn lại, có lý do: 1-01 (luận điểm, một câu), 1-05 (hộp câu hỏi, một câu), 1-06 (câu hỏi thứ hai theo câu hỏi mở đầu của ghi chú), 4-01, 4-02 (định nghĩa, trực quan một câu), 5-01 ("Diễn giải:"), 5-12 (đề bài nguyên văn), 6-04 ("Diễn giải:"), 7-03 (dòng nhắc lại có tên tiếng Anh).

### Lượt 2 (theo `reviews/deck-kiem-lai-1.md`)

| Phát hiện | Kết quả |
|---|---|
| 7-03 phần (a) mất loại bảo đảm, thiếu (T2), $a<b$ | đã sửa: "Theo phần (a), với (T1), (T2), (T4), $0\le a\le\ell\le b$, $a<b$: mọi thuật toán ERM học PAC bất khả diễn với $M(\epsilon,\delta)=\ldots$"; dòng cuối "…, với $1096{,}13$ là giá trị của Ví dụ 02.9 trước khi làm tròn" |
| 7-01 cột "Kết quả" mất tên | đã sửa: Markov, Chebyshev; Hoeffding; Cận tin cậy; Hội tụ đều; Rủi ro vượt mức; Khả diễn (kèm số hiệu); 76 âm tiết, trần 80 của bảng tổng kết |
| 1-05 hộp 31 âm tiết | đã sửa: "…, kể cả khi chọn giả thuyết theo dữ liệu?" = 30 (đếm bằng script: token cách khoảng trắng sau nhãn, bỏ KaTeX) |
| 6-00 dòng dẫn 27 | đã sửa: "Khi lớp giả thuyết chứa một hàm có rủi ro $0$, chỉ cần loại giả thuyết có rủi ro lớn; cỡ mẫu tăng như $1/\epsilon$." = 23 (cùng script) |
| 5-09 dòng "(c)" thiếu chủ ngữ; ví dụ thiếu lớp và $m\ge1097$ | đã sửa: "Do đó mọi thuật toán ERM học PAC bất khả diễn với …"; "(Ví dụ 02.9) Sáu hàm ngưỡng, …: khi $m\ge1097$, với xác suất $\ge0{,}95$, …"; bỏ câu giải thích (c) ở ghi chú diễn giả. Để giữ trần 60, Giả thiết ghi "thuật toán ERM theo (O1)"; ý "mọi quy tắc chọn khi bằng nhau" nằm ở "đồng thời cho mọi nghiệm ERM" của dòng Bảo đảm |
| 6-04 $t^\star$ chưa có | đã sửa: "$h^\star=h_3$ ($t^\star=3$)" |
| 5-08 "Diễn giải:" dùng $95\%$; chưa so với hàm cố định; dòng cuối | đã sửa: "với xác suất ít nhất $0{,}95$, … không quá $0{,}1204$, so với $0{,}05+0{,}0387=0{,}0887$ khi $K=1$" ($0{,}0387$ có trên hình); dòng cuối "Bước tiếp theo so $L_D(\hat h)$ với $\min_{h\in\mathcal H}L_D(h)$ (rủi ro vượt mức)." |
| 5-06 câu chữ (b), (c) | đã sửa: (b) "…; kết luận về lập luận", (c) "…; chỉ ra bước chứng minh bị bỏ qua". Để không chạm chân trang: bỏ khung `box` của câu trích (giữ nhãn "Câu hỏi:" và câu chữ nguyên văn), dòng dữ kiện bỏ "$\mathcal X=\{0,1\}^K$" (ghi ở ghi chú diễn giả) |
| 5-12 chữ hoa sau "Câu hỏi:" | đã sửa |
| 2-01 cột phải lệch một dòng | đã sửa: "Cần chặn ($\hat h$: nghiệm ERM):" đặt ra ngoài `grid2` |
| Dòng > 20 âm tiết ở 4-06, 5-06 | ghi lý do: 4-06 mỗi cột là một đoạn hai câu ngắn (21); tách thành bốn dòng sẽ vượt sáu dòng nội dung. 5-06 dòng 24 là câu trích nguyên văn lập luận của học viên trong Bài tập 02.4 |
| Lỗi gõ ghi chú diễn giả 4-01, 7-04 | đã sửa |
| (thêm) 1-01 luận điểm dạng cụm danh từ + dấu hai chấm | không sửa: phương án của người kiểm lại cho bìa 63 âm tiết khi tính số (dòng năm học bắt buộc); điều phối viên không đưa vào danh sách lượt 2 |
| (thêm) 4-06 "Hoeffding áp dụng sai cho …" | đã sửa: "Áp dụng sai Hoeffding được $2e^{-8}\approx6{,}7\cdot10^{-4}$ ở $m=100$: cận sai." |

Kiểm tra lượt 2: `deck_check.py` 55 trang, console 0, page errors 0, failed 0, không `.katex-error`; SYLL chỉ ở 7-01 (76, trần 80, cờ sai do tiêu đề "Bảng tổng kết"); OVERFLOW chỉ ở các trang có `\sqrt` (báo động giả). `footer_check.py`: 0 trang. `deck_lint.py`: 0 phát hiện (đã rút ghi chú diễn giả 1-02 dưới 150 âm tiết và 7-03 về 60). Đã xem ảnh 1600×900 và 390×844 (cả `-end`) của 1-05, 2-01, 4-06, 5-06, 5-08, 5-09, 5-12, 6-00, 6-04, 7-01, 7-03.

### Lượt 3 (theo `reviews/deck-kiem-lai-2.md`)

| Phát hiện | Kết quả |
|---|---|
| 5-06 thiếu dữ kiện $\mathcal X=\{0,1\}^K$ | đã sửa: đưa lại vào dòng dữ kiện; để không chạm chân trang, ý (b) viết "$\Pr(\exists k:\ L_S(h_k)=0)$, $K=1000$, $5000$; kết luận về lập luận" (một dòng ở 16:9) |
| 7-03 dòng cuối > 60 âm tiết khi tính số | đã sửa: "$17\,538{,}04=16\cdot1096{,}13$ (Ví dụ 02.9, trước khi làm tròn)" |
| 7-01 | không sửa: quyết định của điều phối viên, số trong ô bảng không tính |

Kiểm tra lượt 3: `deck_lint.py` 0 phát hiện; `footer_check.py` 0 trang; `deck_check.py --ids L02-5-06,L02-7-03 --shots`: console 0, page errors 0, failed 0, không `.katex-error`; đã xem ảnh 1600×900 và 390×844 (cả `-end`) của hai trang.
