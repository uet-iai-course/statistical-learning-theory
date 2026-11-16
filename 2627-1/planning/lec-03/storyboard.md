# Storyboard — Bộ trang chiếu Bài 03: Chiều VC và hàm phân lớp tuyến tính

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-11-15 bởi tác tử lập storyboard. Nguồn nội dung duy nhất: `materials/lec-03/lecture-note.md` (bản hiện hành); bài tập: `materials/lec-03/exercises.md`. Quy định: `CLAUDE.md` § Slide decks (bản 2026-11-15, gồm mục "Các quy định dễ sót" của `common-brief.md`), `../rl-plan/CLAUDE.md` § Deck structure and content, nhật ký yêu cầu 2026-11-13 hàng 1–8, quyết định của điều phối viên cho khuôn chung (2026-11-15) và `lec-01/review-log.md` § Bộ trang chiếu. Khuôn bố cục theo storyboard Bài 01 và Bài 02. Mọi mã trang có dạng `L03-k-mm`; trong bảng viết gọn `k-mm`.

Số âm tiết ghi trong tệp này là ước lượng của người lập (đếm theo khoảng trắng, không tính tiêu đề, KaTeX, số trong bảng, nhãn hình, ghi chú); điều phối viên đếm lại trên deck.

UML đã đọc để đối chiếu (không chép câu chữ): §6.4–6.5, trang PDF 73–74 (thứ tự các phép kéo theo của định lý cơ bản; bổ đề Sauer–Shelah và phép quy nạp tách theo một điểm), trang PDF 76 (chứng minh hội tụ đều của UML qua kì vọng và tập mẫu ảo, để ghi khác biệt với ghi chú ở ghi chú diễn giả 7-06). Các mục khác chỉ dẫn theo §12 của ghi chú và `sources/uml-sections.md` (§6.1–6.3 trang 67–71, §9.1 trang 119, §5.1 trang 61, Chương 28 trang 392).

**Thuật ngữ.** Bản giao việc viết "phá vỡ tập điểm" và "mẫu ma"; deck dùng thuật ngữ của ghi chú: "tách trọn vẹn" (shatter; tác giả chốt 2026-11-13, `thuat-ngu.md` dòng 206 loại "phá vỡ") và "mẫu bóng" (nay "tập mẫu ảo", 2026-11-16) (ghost sample; `thuat-ngu.md` dòng 214).

## 1. Tên tệp và tiêu đề

- **Tệp deck:** `2627-1/lecture-03-chieu-vc.html` (slug ASCII từ phần đầu tên bài; phần "và hàm phân lớp tuyến tính" bỏ khỏi slug cho ngắn).
- **Tiêu đề deck (h1 trang bìa):** "Chiều VC và hàm phân lớp tuyến tính" (đúng tên bài của ghi chú).
- **`<title>`:** "Bài 03: Chiều VC".
- **Chân trang:** "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài 03".
- **Liên kết viewer:** `material-viewer.html?doc=materials/lec-03/lecture-note.md&deck=lecture-03-chieu-vc.html` và `…exercises.md&deck=…`.
- **Trang cuối deck Bài 02** (7-06 của storyboard Bài 02) nhận liên kết tới tệp này khi deck Bài 03 xong.

## 2. Khung lý thuyết chung

**Vấn đề trung tâm (hộp "Vấn đề trung tâm", bằng lời, ≤ 30 âm tiết).** "Câu hỏi: với một lớp giả thuyết vô hạn, đại lượng nào thay cho lôgarit của số giả thuyết trong cận cỡ mẫu?" (câu hỏi trung tâm ở đoạn mở đầu của ghi chú, viết bằng lời; 22 âm tiết sau nhãn.)

**Luận điểm (trang bìa, một câu, bằng lời).** "Trên mỗi tập điểm, một lớp có chiều VC hữu hạn chỉ tạo ra một số cách gán nhãn tăng theo đa thức của số điểm, nên dưới một điều kiện đo được lớp đó học được, với cỡ mẫu đủ tăng theo chiều VC thay cho lôgarit của số giả thuyết." (Bổ đề 03.12, Định lý 03.15, 03.17 và §9 của ghi chú; ≈ 48 âm tiết; không kí hiệu.)

**Trọng tâm trực quan của deck.** Rủi ro thực nghiệm $L_S(h)$ chỉ phụ thuộc cách gán nhãn của $h$ trên các đầu vào của tập huấn luyện, nên số "hành vi" của lớp trên $m$ điểm, không phải số phần tử của lớp, quyết định số biến cố hỏng phải cộng. Ý này xuất hiện ở bốn chỗ: 2-02 (lớp hàm ngưỡng vô hạn chỉ cho $m+1$ véc-tơ), 4-02 (hình F4: đa thức bậc $d$ so với $2^m$), 5-03 (vì sao không cộng ngay trên các cách gán nhãn của $S$), 5-07 (kỹ thuật hàm tăng trưởng thay cho số giả thuyết).

**Đối tượng và kí hiệu chung** (ghi chú §1–§3, `ky-hieu.md`):
- $\mathcal Z=\mathcal X\times\{0,1\}$, phân bố $D$ cố định chưa biết; $S=(Z_1,\ldots,Z_m)\sim D^m$, $Z_i=(X_i,Y_i)$; hàm lỗi 0–1 $\ell_{0\text{-}1}$;
- lớp $\mathcal H$ có thể vô hạn; $d=\operatorname{VCdim}(\mathcal H)$; $p$ số chiều đặc trưng, $\mathcal X=\mathbb R^p$;
- thu hẹp $\mathcal H_C$, cách gán nhãn, tách trọn vẹn; hàm tăng trưởng $\Pi_{\mathcal H}(m)$;
- các lớp $\mathcal H_{\mathrm{thr}}$, $\mathcal H_{\mathrm{int}}$, $\mathcal H^p_{\mathrm{aff}}$, $\mathcal H^p_{\mathrm{hom}}$, $\mathcal H_{\sin}$, $\mathcal M_{[0,1]}$, $\mathcal G_S$; $h_t$, $h_{u,v}$, $h_{w,b}$;
- độ lệch đều $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$; bán kính VC $\rho_m=\rho_m(\mathcal H,\delta)$; $m^{UC}_{\mathcal H}(\epsilon,\delta)$; $M(\epsilon,\delta)$;
- trong chứng minh: tập mẫu ảo $S'=(Z'_1,\ldots,Z'_m)$, dấu ngẫu nhiên $\sigma_i$, tập gộp $2m$ điểm;
- ví dụ xuyên suốt: lớp hàm ngưỡng (Ví dụ 03.1, năm mức đo của ví dụ sàng lọc) và hàm phân lớp tuyến tính trên hai hoặc mười chỉ số đo (khối ứng dụng §3).

**Giả thiết** (ghi chú §2): (T1) $Z_1,\ldots,Z_m$ độc lập cùng phân bố theo $D$; (T2) $\ell\ge0$, $\ell(h,\cdot)$ đo được; (T3) $\ell\in[0,1]$; (T5) $\mathcal H$ hữu hạn hoặc vô hạn, chọn trước, không phụ thuộc $S$; (M) có lớp con đếm được $\mathcal H_0$ sao cho mỗi $h$ là giới hạn theo từng điểm của một dãy trong $\mathcal H_0$; (O1) nghiệm ERM chính xác; (O2) nghiệm $\epsilon_{\mathrm{opt}}$-ERM; khả diễn (Định nghĩa 01.16) ở Định lý 03.17, 03.19.

**Chuỗi định nghĩa → kết quả → phương pháp.**
1. Lớp vô hạn làm $\ln\lvert\mathcal H\rvert$ không xác định; $L_S(h)$ chỉ phụ thuộc véc-tơ giá trị trên tập huấn luyện (Ví dụ 03.1) → thu hẹp, cách gán nhãn (Định nghĩa 03.1, Ví dụ 03.2).
2. Tách trọn vẹn, chiều VC (Định nghĩa 03.2, 03.3); cận dưới và cận trên (Nhận xét 03.4); $d=1$ cho hàm ngưỡng, $d=2$ cho khoảng (Mệnh đề 03.5, 03.6).
3. Nửa không gian (Định nghĩa 03.7); phân hoạch Radon (Bổ đề 03.8); $d=p+1$ và $d=p$ (Mệnh đề 03.9); bốn điểm trong mặt phẳng (Ví dụ 03.3); số tham số khác chiều VC (Nhận xét 03.10).
4. Hàm tăng trưởng (Định nghĩa 03.11, Ví dụ 03.4); bổ đề Sauer–Shelah (Bổ đề 03.12): đa thức bậc $d$; so sánh ba cách đếm (Ví dụ 03.5).
5. Tính chất hội tụ đều (Định nghĩa 03.13), lớp không có tính chất này (Ví dụ 03.6); vì sao không cộng trên các cách gán nhãn của $S$; tập mẫu ảo → Định lý 03.15 với $\rho_m$; số liệu (Ví dụ 03.7); bỏ (T5) (Ví dụ 03.8).
6. Bước tất định → rủi ro vượt mức của mọi nghiệm ERM (Hệ quả 03.16); cỡ mẫu $54\,330$, $132\,992$, $447\,194$ (Ví dụ 03.9); so với rời rạc hóa (Ví dụ 03.10); định lý cơ bản (Định lý 03.17), Hệ quả 03.18; cận dưới (Định lý 03.19, đọc thêm).

**Giới hạn áp dụng** (ghi chú §9): chỉ phân lớp nhị phân với hàm lỗi 0–1 (phép đếm cách gán nhãn ở Bước 3 cần nhãn dự đoán trong $\{0,1\}$); bỏ (T5): cận sai dù $d=1$ (Ví dụ 03.8); bỏ (T1): rủi ro thực nghiệm có thể không tập trung (Ví dụ 02.6); $d=\infty$: Định lý 03.15(a) đúng nhưng không cho thông tin ($\rho_m\ge3{,}33$), Ví dụ 03.6 không có hội tụ đều; phân tích VC kiểm soát cả lớp và mọi phân bố nên có thể lỏng cho một thuật toán hay một phân bố cụ thể; cận trên lớn hơn cận dưới một thừa số cỡ $\ln(1/\epsilon)$. Tính đo được (M) chỉ nêu ở giả thiết và ghi chú diễn giả; Phụ lục C.1, D không đưa lên deck.

## 3. Bảng mạch

Bảy mạch theo đúng thứ tự các mục của ghi chú; mỗi mạch ứng với các mục liên tiếp. Bảng đối chiếu trang → khối ghi chú ở mục 12.

| N | Tên mạch | Mục ghi chú | Chức năng | Đầu vào | Đầu ra | `strand-lead` (âm tiết) | Từ khóa | Trang | Phút |
|---|---|---|---|---|---|---|---|---:|---:|
| 1 | Mở đầu | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết, §3 (khối ứng dụng) | Bìa, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, hai câu hỏi cỡ mẫu | Bài 02: cỡ mẫu theo $\ln K$ cho lớp hữu hạn | Hai câu hỏi: lớp hàm ngưỡng và mười chỉ số đo, rủi ro vượt mức $0{,}1$ | (không có trang tiêu đề mạch) | — | 6 | 8 |
| 2 | Tách trọn vẹn và chiều VC | §1–§4 | Thiết lập; số véc-tơ của lớp hàm ngưỡng; thu hẹp; tách trọn vẹn; chiều VC; kỹ thuật cận dưới và cận trên; $d=1$, $d=2$ | lớp vô hạn, $\ln\lvert\mathcal H\rvert$ không xác định | Chiều VC tính bằng hai chiều lập luận; lớp vô hạn có chiều VC hữu hạn | "Một lớp vô hạn được đo bằng số điểm lớn nhất mà lớp gán nhãn tùy ý được; với lớp hàm ngưỡng, số đó bằng một." (deck) | thu hẹp · cách gán nhãn · tách trọn vẹn · chiều VC · cận dưới và cận trên | 8 | 18 |
| 3 | Nửa không gian và hàm phân lớp tuyến tính | §5 | Định nghĩa 03.7; ba điểm trong mặt phẳng; phân hoạch Radon; Mệnh đề 03.9; bốn điểm; số tham số | thứ tự trên đường thẳng không có trong $\mathbb R^p$ | $d=p+1$ (afin), $d=p$ (thuần nhất); $d=3$, $d=11$ cho ứng dụng; số tham số không thay được chiều VC | "Hàm phân lớp tuyến tính trên mười chỉ số đo gán nhãn tùy ý được một tập mười một điểm, và không gán nhãn tùy ý được tập mười hai điểm nào." (deck) | nửa không gian · đơn hình · phân hoạch Radon · số tham số | 8 | 19 |
| 4 | Hàm tăng trưởng và bổ đề Sauer–Shelah | §6 | Định nghĩa 03.11; Ví dụ 03.4; Bổ đề 03.12; hai trang ý tưởng chứng minh; ví dụ tách theo điểm cuối; Ví dụ 03.5 | chiều VC chỉ nói về $m\le d$ | $\Pi_{\mathcal H}(m)\le\sum_{j\le d}\binom mj\le(em/d)^d$; $\ln\Pi_{\mathcal H}(m)\le d\ln(em/d)$ | "Trên nhiều điểm hơn chiều VC, số cách gán nhãn của lớp tăng như một đa thức của số điểm, thay cho hàm mũ." (deck) | hàm tăng trưởng · tổng nhị thức · quy nạp kép · công thức Pascal | 7 | 18,5 |
| 5 | Hội tụ đều trên lớp có chiều VC hữu hạn | §7 | Định nghĩa 03.13; Ví dụ 03.6; câu hỏi về bất đẳng thức hợp trên các cách gán nhãn của $S$; Định lý 03.15; hai trang kỹ thuật; Ví dụ 03.7; Ví dụ 03.8 | số cách gán nhãn đa thức trên $m$ điểm | $\rho_m$, cận $\sqrt{d\ln m/m}$; cần (T1), (T5), (M) | "Trên lớp có chiều VC hữu hạn, rủi ro thực nghiệm của mọi hàm gần rủi ro kì vọng với xác suất cao, nhờ một tập thứ hai chỉ dùng trong chứng minh." (deck) | hội tụ đều · tập mẫu ảo · đổi chỗ · tập gộp · bán kính VC | 10 | 27 |
| 6 | Rủi ro vượt mức của ERM và định lý cơ bản | §8, §9 | Hệ quả 03.16; Ví dụ 03.9 trả lời câu hỏi mở đầu; Ví dụ 03.10; Định lý 03.17 (hai trang phát biểu) và ý tưởng chứng minh; Định lý 03.19 (đọc thêm) | cận độ lệch đều $\rho_m$ | Cỡ mẫu $54\,330$, $447\,194$; học được khi và chỉ khi $d<\infty$ (dưới (M)); tốc độ $1/\epsilon^2$ cần thiết | "Mọi nghiệm ERM có rủi ro vượt mức nhỏ khi cỡ mẫu tăng theo chiều VC; dưới điều kiện đo được, lớp học được khi và chỉ khi chiều VC hữu hạn." (deck) | bước tất định · rời rạc hóa · định lý cơ bản · cận dưới | 9 | 20 |
| 7 | Tổng kết | §9–§12 | Bảng kết quả, trả lời vấn đề trung tâm, bài tập tổng hợp, tự kiểm tra, bài tập về nhà, tài liệu | mọi kết quả | Cầu nối sang Bài 04 | "Với lớp vô hạn, chiều VC thay cho lôgarit của số giả thuyết trong cỡ mẫu, khi quan sát độc lập và lớp được chọn trước khi lấy mẫu." (deck) | — | 7 | 9,5 |
| | **Tổng** | | | | | | | **55** | **120** |

Số trang **55** (bản deck, 2026-11-15): 54 trang của storyboard đã duyệt cộng trang `2-07` (Bài tập 03.2(c)) theo quyết định của điều phối viên; đúng trần 55. Lý do của 54 trang ban đầu: bài có bảy kết quả chính (Mệnh đề 03.5–03.6 chung một trang ý tưởng chứng minh, Mệnh đề 03.9, Bổ đề 03.12 với hai phần có hai trang ý tưởng chứng minh, Định lý 03.15, Hệ quả 03.16, Định lý 03.17), mỗi kết quả có trang "Ý tưởng chứng minh" riêng; ba kỹ thuật dùng lại qua học phần có trang "Kỹ thuật." riêng (cận dưới và cận trên cho chiều VC, đối xứng hóa và tập mẫu ảo, hàm tăng trưởng thay cho số giả thuyết); trần mật độ đếm bằng script (≤ 60 âm tiết, ≤ 20 âm tiết mỗi dòng, ≤ 6 dòng) buộc tách hai cặp trang: câu hỏi mở đầu được trả lời ở 6-03, tách khỏi so sánh với rời rạc hóa (6-04), và định lý cơ bản có hai trang phát biểu (6-05 điều kiện cần, 6-06 sáu khẳng định tương đương). Phương án rút còn 52 ở mục 11, điểm 2.

## 4. Bảng kết quả chính

Số hiệu theo ghi chú. Ánh xạ blueprint → ghi chú (theo `outline.md` §2): Propositions 3.1–3.3 → Mệnh đề 03.5, 03.6, 03.9; Lemma 3.4 → Bổ đề 03.12; Theorem 3.5 → Định lý 03.15; Corollary 3.6 → Hệ quả 03.16; Fundamental theorem → Định lý 03.17. Mọi phát biểu rút gọn trên trang dùng "Giả thiết:" và "Bảo đảm:", giữ đủ giả thiết, lượng từ, hằng số và loại bảo đảm của ghi chú.

| Kết quả | Loại bảo đảm | (a) Trực quan | (b) Ý tưởng chứng minh | (c) Kỹ thuật | (d) Ví dụ bổ trợ | Trang |
|---|---|---|---|---|---|---|
| **Mệnh đề 03.5, 03.6** (hàm ngưỡng $d=1$, khoảng đóng $d=2$; chứng minh đầy đủ) | tất định, về lớp | $h_t$ không giảm theo $x$; tập $\{h=1\}$ của $h_{u,v}$ là một khoảng. Cùng lực lượng với $\mathbb R$, khác chiều VC. Hình F1. | Cận dưới: $\{0\}$, $\{1\}$; $\{0,1\}$ với bốn khoảng $[0,1]$, $[0,0]$, $[1,1]$, $[2,2]$ (hàm hằng $0$ không thuộc lớp). Cận trên: $(1,0)$ đòi $x_2<t\le x_1$; $(1,0,1)$ đòi $u\le x_2\le v$. Bỏ "mọi tập" ở cận trên: lỗi của Nhận xét 03.4. | **Cận dưới và cận trên cho chiều VC** (lần đầu trong học phần, trang riêng 2-04; dùng lại ở Mệnh đề 03.9, Bài 04). Dòng "Kỹ thuật." trên 2-06: thứ tự trên đường thẳng cho cận trên. | Ví dụ 03.2 (sáu véc-tơ trên năm mức đo); $d\le\log_26\approx2{,}585$. | 2-03 đến 2-06 |
| **Mệnh đề 03.9** (nửa không gian; chứng minh đầy đủ, (b) cận trên ở Phụ lục A) | tất định, theo $p$ | $p+1$ đỉnh đơn hình gán nhãn tùy ý được; mọi $p+2$ điểm có phân hoạch Radon. Hình F2, F3. | Bốn bước: nghiệm tường minh $b=2y_0-1$, $w_i=2y_i-1-b$; Radon $(I,J)$, gán $1$ trên $I$, $0$ trên $J$; $g$ afin nên $g(z)\ge0$ và $g(z)<0$; dấu $<0$ cần $J\ne\varnothing$ và quy ước $\ge0$. (b): $w=\sum_i(2y_i-1)\mathbf e_i$; phụ thuộc tuyến tính. Bỏ hệ số tự do: gốc luôn nhãn $1$, mất một điểm. | Dòng "Kỹ thuật." trên 3-05: hàm afin giữ tổ hợp lồi. Nhắc lại kỹ thuật cận dưới và cận trên. | Ví dụ 03.3 (ba điểm, thẳng hàng, hình vuông $14$ trên $16$, điểm trong tam giác); ứng dụng $d=11$, $d=3$. | 3-01 đến 3-06 |
| **Bổ đề 03.8** (phân hoạch Radon; phác thảo) | tất định | Hai đường chéo hình vuông cắt nhau tại $(\tfrac12,\tfrac12)$. | Hệ $p+1$ phương trình, $p+2$ ẩn có nghiệm $a\ne0$; tách theo dấu. Công cụ, không là kết quả chính: phát biểu và chứng minh một dòng chung trang 3-03 (mục 11, điểm 3). | — | Hình vuông, tam giác với $(1,1)$ (hình F3). | 3-03 |
| **Bổ đề 03.12** (Sauer–Shelah; (a) phác thảo, (b) chứng minh đầy đủ) | tất định, tổ hợp | Trên $m>d$ điểm, số cách gán nhãn tăng như đa thức bậc $d$ thay cho $2^m$ (hình F4). | (a) Năm bước: cố định $C$, $C'$; $\lvert\mathcal H_C\rvert=\lvert\mathcal H_{C'}\rvert+\lvert Y_1\rvert$; $Y_1$ có chiều VC $\le d-1$; quy nạp kép; công thức Pascal. (b) $(m/d)^{d-j}\ge1$, thêm số hạng ($d\le m$), khai triển nhị thức, $1+x\le e^x$. Bỏ $d\le m$: $m=1$, $d=3$ cho $(e/3)^3\approx0{,}744<2$. | Dòng "Kỹ thuật." trên 4-03: tách theo nhãn của điểm cuối rồi cộng bằng công thức Pascal (chỉ dùng ở đây). | Mới N1: lớp khoảng trên $(1,2,3)$: $7=4+3$ (4-04); Ví dụ 03.4, 03.5 (bảng, $14<15$, $1351$ so với $1\,048\,576$). | 4-01 đến 4-06 |
| **Định lý 03.15** (hội tụ đều trên lớp có chiều VC hữu hạn; phác thảo, đầy đủ ở Phụ lục C) | xác suất cao theo $S$; đồng thời mọi $h$; không phụ thuộc $D$; $\sqrt{\ln m/m}$, $\ln(1/\delta)$ | Thay $\ln K$ bằng $\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$, độ lệch cỡ $\sqrt{d\ln m/m}$. | Năm bước: tập mẫu ảo (Chebyshev, hệ số $2$; (T1), bị chặn, (M)); đổi chỗ với dấu ngẫu nhiên ((T1)); $\Pi_{\mathcal H}(2m)$ cách gán nhãn trên tập gộp ((T5)); Hoeffding miền dài $2$ và bất đẳng thức hợp; giải theo $\delta$, Sauer–Shelah tại $2m$. Bỏ (T5): Ví dụ 03.8. Bỏ tập mẫu ảo: Bài tập 03.4(d) ($0{,}590$ so với $1$). Cực biên $d=\infty$: $\rho_m\ge3{,}33$. | **Đối xứng hóa và tập mẫu ảo** (lần đầu, trang riêng 5-06; dùng lại ở Bài 07). **Hàm tăng trưởng thay cho số giả thuyết** (lần đầu, trang riêng 5-07; dùng lại ở Bài 04, 07). Nhắc lại Chebyshev, Hoeffding, bất đẳng thức hợp, đảo cận đuôi. Dòng "Kỹ thuật." trên 5-05 (ghi chú diễn giả): bất đẳng thức tiếp tuyến $\ln u\le u/u_0+\ln u_0-1$ cho phần (c). | Ví dụ 03.7 (bảng, hình F5); Ví dụ 03.8 ($0{,}322$ so với $1$). | 5-03 đến 5-09 |
| **Hệ quả 03.16** (rủi ro vượt mức của ERM; chứng minh đầy đủ) | xác suất cao; đồng thời mọi nghiệm ERM, mọi quy tắc chọn khi bằng nhau; không phụ thuộc $D$ | Hệ số $2$ từ hai phép so sánh; $\inf$ thay cho $\min$ vì lớp vô hạn có thể không đạt giá trị nhỏ nhất. | Nhắc lại bước tất định; lấy $\inf_h$ ở vế phải; $r=\rho_m$; (c) Định lý 03.15(c) với $\epsilon/2$ cho $64/\epsilon^2$, $128/\epsilon^2$. Bỏ (O1): bất đẳng thức giữa hỏng; (O2) thêm $\epsilon_{\mathrm{opt}}$. | Nhắc lại bước tất định trên biến cố đại diện (Bài 02). | Ví dụ 03.9 ($54\,330$; $132\,992$; $447\,194$; dạng đóng; dạng hằng số $4$); Ví dụ 03.10 (rời rạc hóa $9611$, $98\,333$; $0{,}2222$ so với $0{,}0523$). | 6-01 đến 6-04 |
| **Định lý 03.17** (định lý cơ bản; phác thảo, điều kiện cần theo UML §5.1, §6.4) | (a) "với mọi thuật toán, tồn tại phân bố", không dùng (M); (b) sáu khẳng định tương đương dưới (M) | Khi $d=\infty$, với mọi $m$ có $2m$ điểm bị tách trọn vẹn; tập huấn luyện thấy nhiều nhất một nửa, nhãn nửa kia tùy ý. | Chuỗi kéo theo (hình F7): (6)⇒(1) Định lý 03.15; (1)⇒(2) bước tất định; (2)⇒(3), (5)⇒(4) định nghĩa; (2)⇒(5), (3)⇒(4) Nhận xét 01.26; (4)⇒(6) phần (a), định lý không có bữa trưa miễn phí (thừa nhận). | Nhắc lại bước tất định. | Hệ quả 03.18 ($\mathcal M_{[0,1]}$); Ví dụ 03.6. | 6-05 đến 6-07 |

**Kết quả phụ và quyết định.**
- Định nghĩa 03.1, Ví dụ 03.1, 03.2: một trang chung (2-02), cùng lập luận "véc-tơ giá trị" của Ví dụ 03.1 Bước 2.
- Nhận xét 03.4: trang kỹ thuật 2-04 (cận dưới và cận trên dùng lại ở Bài 04 khi tính chiều VC của $\mathcal H_k$, ghi chú Bài 04 dòng 1196, và ở mọi bài tập tính chiều VC).
- Nhận xét 03.10: trang riêng 3-07 (mục tiêu 5; ý "số tham số không thay được" là một phần của trọng tâm trực quan).
- Nhận xét 03.14 (điều kiện (M) cho các lớp của bài) và đoạn về tính đo được ở §7: ghi chú diễn giả 5-03 và 5-04; (M) có trên mặt trang ở 2-01 và trong "Giả thiết:" của 5-04, 6-01.
- Định nghĩa 03.13: trang riêng 5-01; Ví dụ 03.6: trang riêng 5-02 (cũng là phản ví dụ cho $d=\infty$).
- Hệ quả 03.18: dòng "Kết luận:" cuối 6-07 (hai bước, kiểm giả thiết của Định lý 03.17(a)).
- Định lý 03.19 (đọc thêm [O]): phát biểu rút gọn trên 6-08; ghi chú diễn giả nói kết quả ở mức đọc thêm và chứng minh nằm ngoài phạm vi học phần (UML §28.2); không có trang ý tưởng chứng minh (mục 11, điểm 4).
- Phụ lục A (Radon, cận trên (b)): một dòng ở 3-05; Phụ lục B (Sauer–Shelah đầy đủ): bước 1–5 của 4-03; Phụ lục C (Định lý 03.15 đầy đủ): số liệu hằng số ở 5-05, 5-06; Phụ lục C.1, D (đo được): không đưa lên deck.
- Câu ôn nhanh 1–3: ghi chú diễn giả 1-02 (câu 1: $16=\tfrac12\cdot32$), 3-02 (câu 2: $b=-1$, $w=(2,2)$), 5-05 (câu 3: $2e^{-m\epsilon^2/2}$, miền dài $2$).
- §9 (ý nghĩa, giới hạn): ghi chú diễn giả 6-08 và cột "Giả thiết không được bỏ" của bảng 7-01; không có trang giới hạn riêng (gộp để giữ 54 trang).

## 5. Ví dụ bổ trợ

Ví dụ xuyên suốt: **lớp hàm ngưỡng** $h_t(x)=\mathbb 1[x\ge t]$ (Ví dụ 03.1, năm mức đo của ví dụ sàng lọc Bài 01) và **hàm phân lớp tuyến tính trên hai hoặc mười chỉ số đo** (khối ứng dụng §3). Mỗi lần dùng lại trả lời một câu hỏi mới: lớp hàm ngưỡng: câu hỏi cỡ mẫu (1-06), $m+1$ véc-tơ và sáu véc-tơ trên năm mức đo (2-02), tách trọn vẹn một điểm (2-03), $d=1$ (2-05), $\Pi=m+1$ (4-01), dấu bằng của Bổ đề 03.12 (4-06), $54\,330$ quan sát (6-03), so với $9611$ của lớp rời rạc hóa (6-04). Hàm phân lớp tuyến tính: câu hỏi (1-06), lớp $\mathcal H^{10}_{\mathrm{aff}}$ (3-01), $d=11$, $d=3$ (3-04), $\Pi(4)=14$ (4-06), độ lệch đều $0{,}762$, $0{,}280$ (5-08), $447\,194$ quan sát và tỉ số $3{,}36$ (6-03), so với lớp rời rạc hóa (6-04), cầu nối Bài 04 (7-06). Bài tập trên mặt trang lấy từ `exercises.md` với cùng số liệu, câu chữ và kết quả: Bài tập 03.1(a) (7-03, bài tập tổng hợp). Các bài tập khác chỉ được dẫn trong ghi chú diễn giả (03.2(c) ở 2-04, 03.3 ở 3-05, 03.4(c)(d)(e) ở 5-03, 5-06, 6-04, 03.5 ở 3-07, 5-09, 03.11 ở 6-07).

Mọi con số dưới đây đã tính lại bằng Python (thư mục nháp `…/scratchpad/lec-03/storyboard/num.py`) và khớp ghi chú.

**V1. Lớp hàm ngưỡng trên năm mức đo** (Ví dụ 03.1, 03.2). Trên $x_1<\cdots<x_m$ có $m+1$ véc-tơ. $C=(1,2,3,4,5)$: $\mathcal H_C=\{11111,\ 01111,\ 00111,\ 00011,\ 00001,\ 00000\}$, $\lvert\mathcal H_C\rvert=6$, so với $2^5=32$. Lớp sáu hàm: $\log_26=2{,}585$, nên $d\le2$; Mệnh đề 03.5(b) cho $d=1$.

**V2. Bốn khoảng trên hai điểm và cách gán nhãn bị chặn** (chứng minh Mệnh đề 03.5, 03.6; hình F1). $\{0,1\}$: $(1,1)$ bởi $[0,1]$, $(1,0)$ bởi $[0,0]$, $(0,1)$ bởi $[1,1]$, $(0,0)$ bởi $[2,2]$. Hàm ngưỡng trên $\{1,2\}$: thực hiện được $00$, $01$, $11$; thiếu $10$ (đòi $2<t\le1$). Khoảng trên ba điểm: thiếu $101$.

**V3. Nửa mặt phẳng trên ba điểm** (Ví dụ 03.3 Bước 1–2; hình F2). Điểm $(0,0)$, $(1,0)$, $(0,1)$, $b=2y_0-1$, $w=(2y_1-1-b,\ 2y_2-1-b)$. Tám cách gán nhãn, tính lại và kiểm dấu từng điểm:

| $(y_0,y_1,y_2)$ | $b$ | $w$ | giá trị tại ba điểm | đường $\langle w,x\rangle+b=0$ |
|---|---|---|---|---|
| $000$ | $-1$ | $(0,0)$ | $-1;\ -1;\ -1$ | không có (hằng $0$) |
| $001$ | $-1$ | $(0,2)$ | $-1;\ -1;\ 1$ | $x_2=\tfrac12$ |
| $010$ | $-1$ | $(2,0)$ | $-1;\ 1;\ -1$ | $x_1=\tfrac12$ |
| $011$ | $-1$ | $(2,2)$ | $-1;\ 1;\ 1$ | $x_1+x_2=\tfrac12$ |
| $100$ | $1$ | $(-2,-2)$ | $1;\ -1;\ -1$ | $x_1+x_2=\tfrac12$ |
| $101$ | $1$ | $(-2,0)$ | $1;\ -1;\ 1$ | $x_1=\tfrac12$ |
| $110$ | $1$ | $(0,-2)$ | $1;\ 1;\ -1$ | $x_2=\tfrac12$ |
| $111$ | $1$ | $(0,0)$ | $1;\ 1;\ 1$ | không có (hằng $1$) |

Hai dòng $101$ và $011$ trùng ghi chú (Ví dụ 03.3 Bước 1; câu ôn nhanh 2). Ba điểm thẳng hàng $(0,0)$, $(1,0)$, $(2,0)$: $101$ không thực hiện được.

**V4. Bốn điểm** (Ví dụ 03.3 Bước 3–4; hình F3). Kiểm bằng lưới $(w_1,w_2,b)\in\{-4;-3{,}9;\ldots;4\}^3$: hình vuông $(0,0)$, $(1,0)$, $(1,1)$, $(0,1)$ nhận đúng $14$ cách, thiếu $1010$ và $0101$ (thứ tự đỉnh như trên). $14=2+4+4+4$. Điểm trong tam giác: $(1,1)=\tfrac13(0,0)+\tfrac13(3,0)+\tfrac13(0,3)$.

**V5. Hàm tăng trưởng** (Ví dụ 03.4, 03.5). $\Pi_{\mathcal H_{\mathrm{thr}}}(m)=m+1$; $\Pi_{\mathcal H_{\mathrm{int}}}(m)=\binom{m+1}2+1$: $m=1,\ldots,5,20$: $(2,2)$, $(3,4)$, $(4,7)$, $(5,11)$, $(6,16)$, $(21,211)$. $\sum_{j\le2}\binom5j=16$. Với $d=3$:

| $m$ | $\sum_{j\le3}\binom mj$ | $(em/3)^3$ | $2^m$ |
|---|---|---|---|
| $3$ | $8$ | $20{,}09$ | $8$ |
| $4$ | $15$ | $47{,}61$ | $16$ |
| $5$ | $26$ | $92{,}99$ | $32$ |
| $20$ | $1351$ | $5951{,}27$ | $1\,048\,576$ |

$\Pi_{\mathcal H^2_{\mathrm{aff}}}(m)=2,4,8,14$ tại $m=1,\ldots,4$. $(e/3)^3=0{,}7439<2$.

**V6 (mới, N1). Tách theo điểm cuối cho lớp khoảng trên ba điểm** (trang 4-04). Cách dựng: áp dụng Bước 1–2 của chứng minh Bổ đề 03.12(a) cho $\mathcal H_{\mathrm{int}}$ ($d=2$, Mệnh đề 03.6), $C=(1,2,3)$, $C'=(1,2)$; liệt kê bằng mọi khoảng có đầu mút trên lưới bước $\tfrac12$ trong $[-1;5{,}5]$ (đủ vì mọi khoảng cho cùng cách gán nhãn với một khoảng có đầu mút trên lưới này).
- $\mathcal H_C=\{000,\ 100,\ 010,\ 001,\ 110,\ 011,\ 111\}$: $7$ cách, thiếu $101$; khớp $\Pi_{\mathcal H_{\mathrm{int}}}(3)=\binom42+1=7$.
- $\mathcal H_{C'}=\{00,\ 10,\ 01,\ 11\}$: $4$ cách.
- $Y_1$: $00\to000,001$; $01\to010,011$; $11\to110,111$; $10\to100$ (không có $101$). Vậy $Y_1=\{00,\ 01,\ 11\}$, $\lvert Y_1\rvert=3$; $7=4+3$.
- $Y_1$ tách trọn vẹn $\{1\}$ (giá trị $0,0,1$ ở vị trí $1$) và $\{2\}$, không tách trọn vẹn $\{1,2\}$ (thiếu $10$): chiều VC của $Y_1$ bằng $1=d-1$.
- Cận: $\lvert\mathcal H_{C'}\rvert\le\binom20+\binom21+\binom22=4$, $\lvert Y_1\rvert\le\binom20+\binom21=3$; Pascal: $4+3=7=\binom30+\binom31+\binom32$. Dấu bằng ở cả hai bước.
- Kiểm thêm (ghi chú diễn giả): lớp hàm ngưỡng trên $(1,2,3)$: $\mathcal H_C=\{000,001,011,111\}$, $\mathcal H_{C'}=\{00,01,11\}$, $Y_1=\{00\}$; $4=3+1$.
- Không mâu thuẫn ghi chú: chỉ dùng Mệnh đề 03.6, Ví dụ 03.4 và các bước của chứng minh.

**V7. Hình F4** (mới về số điểm, N2; công thức của Bổ đề 03.12 và Ví dụ 03.5). $d=3$, $m=1,\ldots,20$: tổng nhị thức $2,4,8,15,26,42,64,93,130,176,232,299,378,470,576,697,834,988,1160,1351$; dạng đóng ($m\ge3$) $20{,}1;\ 47{,}6;\ 93{,}0;\ 160{,}7;\ 255{,}2;\ 380{,}9;\ 542{,}3;\ 743{,}9;\ 990{,}1;\ 1285{,}5;\ 1634{,}4;\ 2041{,}3;\ 2510{,}7;\ 3047{,}1;\ 3654{,}8;\ 4338{,}5;\ 5102{,}5;\ 5951{,}3$; $2^m$ đến $1\,048\,576$. Các giá trị tại $m=3,4,5,20$ trùng bảng của ghi chú. Trục dọc lôgarit từ $1$ đến $10^7$ chứa hết dữ liệu (nhỏ nhất $2$, lớn nhất $1\,048\,576$).

**V8. Vì sao không cộng trên các cách gán nhãn của $S$** (Bài tập 03.4(d), ghi chú diễn giả 5-03). $\mathcal M_{[0,1]}$, $\Pi(m)=2^m$, $m=1000$, $\delta=0{,}05$: $\sqrt{(1000\ln2+\ln40)/2000}=\sqrt{0{,}3484}=0{,}590$; độ lệch đều thật bằng $1$.

**V9. Cận độ lệch đều** (Ví dụ 03.7; hình F5). $\ln80=4{,}3820$. Ô $d=3$, $m=10^4$: $2em/3=18\,121{,}9$; $3\ln18\,121{,}9=29{,}4146$; $8(29{,}4146+4{,}3820)/10^4=0{,}027037$; căn $0{,}1644$. Bảng (dạng trực tiếp / dạng hằng số $4$): $d=3$: $0{,}4638/0{,}6212$; $0{,}1644/0{,}2228$; $0{,}0571/0{,}0779$. $d=11$: $0{,}7622/1{,}0143$; $0{,}2799/0{,}3787$; $0{,}0993/0{,}1356$. Tỉ số khi nhân $m$ lên $10$: $2{,}82$, $2{,}88$ ($d=3$); $2{,}72$, $2{,}82$ ($d=11$): từ $2{,}7$ đến $2{,}9$. Tỉ số hai dạng: $1{,}331$ đến $1{,}366$. Điểm thêm cho hình F5 (mới, N3; cùng công thức dạng trực tiếp): $m=2000$: $0{,}3404$ / $0{,}5665$; $5000$: $0{,}2253$ / $0{,}3801$; $20\,000$: $0{,}1198$ / $0{,}2055$; $50\,000$: $0{,}0786$ / $0{,}1360$ ($d=3$ / $d=11$).

**V10. Lớp chọn sau khi xem tập huấn luyện** (Ví dụ 03.8). $\ln(2e\cdot1000)=8{,}6009$; $\sqrt{0{,}008\cdot(8{,}6009+4{,}3820)}=\sqrt{0{,}103863}=0{,}3223$. Cực biên $d=\infty$: $\sqrt{16\ln2}=3{,}330$.

**V11. Cỡ mẫu cho rủi ro vượt mức $0{,}1$** (Ví dụ 03.9), $\delta=0{,}05$. Chia đôi khoảng trên $2\cdot\text{dạng trực tiếp}\le0{,}1$: $54\,330$; $132\,992$; $447\,194$. Dạng đóng $\lceil6400(d\ln12\,800+4{,}382)\rceil$: $88\,572$; $209\,624$; $693\,832$ (tỉ số $1{,}63$; $1{,}58$; $1{,}55$). Dạng hằng số $4$: $103\,939$; $261\,198$; $889\,572$. $447\,194/132\,992=3{,}363$; $11/3=3{,}667$.

**V12. Rời rạc hóa** (Ví dụ 03.10). $q=1$: $65\ln2+\ln20=48{,}0503$, $\lceil9610{,}06\rceil=9611$; $q=11$: $705\ln2+\ln20=491{,}6645$, $98\,333$. Tỉ số $54\,330/9611=5{,}65$; $447\,194/98\,333=4{,}55$. Sáu hàm ngưỡng, $m=1000$: $\rho_m\le\sqrt{8\ln480/1000}=0{,}2222$; $r_m=\sqrt{\ln240/2000}=0{,}0523$; tỉ số $4{,}25$.

**V13. Bài tập 03.4(a)(b)** (ghi chú diễn giả 7-05; số và kết quả của `exercises.md`). $\epsilon=0{,}05$: $589\,118$ ($d=3$), $1\,999\,657$ ($d=11$); cỡ mẫu $M(\epsilon,\delta)$: $944\,961$, $3\,165\,709$. Tỉ số $1\,999\,657/589\,118=3{,}394<3{,}667$; $589\,118/132\,992=4{,}430$; $1\,999\,657/447\,194=4{,}472$. Ngoặc tại cỡ mẫu nhỏ nhất: $46{,}02$, $156{,}22$; $m/d$: $196\,373$, $181\,787$; $\ln4{,}43=1{,}49$.

**V14. Cầu nối Bài 04** (§11; 7-06). $2\cdot0{,}1644=0{,}329$; $2\cdot0{,}2799=0{,}560$ ($m=10^4$).

**V15. Bài tập 03.1(a)(b)** (7-03; số và kết quả của `exercises.md`). Bộ $k$ điểm phân biệt của $\{1,\ldots,5\}$, $k\le\min\{m,5\}$, cho $k+1$ cách (ngưỡng $t=x_i$, $i=1,\ldots,k$, và $t=x_k+1\le6$). $\Pi(m)=\min\{m,5\}+1=\min\{m+1,6\}$: $\Pi(3)=4$, $\Pi(8)=6$. Phần (b): $1+m=\Pi(m)$ khi và chỉ khi $m\le5$; với $m\ge6$, $\Pi(m)=6=\lvert\mathcal H^{(6)}_{\mathrm{thr}}\rvert<2^m$. Kiểm bằng liệt kê: $m=3$, bộ $(1,2,3)$ cho $000,001,011,111$ (4 cách); bộ tám điểm chứa $1,\ldots,5$ cho đúng sáu véc-tơ của sáu hàm.

**V16. Câu hỏi cuối buổi** (§11; ghi chú diễn giả 7-04). Bốn điểm $(\pm1,0)$, $(0,\pm1)$; lời giải của ghi chú (năm điểm, bốn điểm cực trị theo tọa độ). Không có số mới.

## 6. Danh sách trang

Mỗi mục: ID, tiêu đề, loại, thời lượng; **Mặt trang** (các dòng dự kiến, theo thứ tự; `[f]` là fragment); **Ghi chú diễn giả** (ý chính, 40–150 âm tiết, đến ~250 cho trang ý tưởng chứng minh; viết cho giảng viên và người học; không mã trang, mã ví dụ của storyboard, câu quy trình hay nguồn gốc; luôn kết thúc bằng dòng `note-source`); **Lý do / nối**; **Mục tiêu / nguồn**. Câu trên mặt trang là bản dự kiến đã tự kiểm theo `no-ai-slop` (chế độ Edit) và `eval.md`; người viết deck có thể rút gọn, không thêm khẳng định.

Quy ước chung cho người viết deck:
- Trang kết quả: "Giả thiết:" và "Bảo đảm:" (nhãn của ghi chú), trích số khối của ghi chú một lần.
- Trang tổng quan (bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm") viết bằng lời, không kí hiệu, không tiếng Anh. Lần đầu một thuật ngữ trên trang nội dung có tiếng Anh trong ngoặc (bảng mục 10).
- Mọi kí hiệu trên mặt trang đã có ở trang trước hoặc có dòng "Nhắc lại:" (bảng đối chiếu mục 12 ghi chỗ đưa vào).
- Số thập phân dùng dấu phẩy KaTeX `0{,}2`; dãy số ngăn bằng `;\ `; số từ năm chữ số tách nhóm bằng `\,`. Cách gán nhãn viết liền ba chữ số ($101$) chỉ trong bảng và danh sách; trong câu viết $(1,0,1)$ như ghi chú.
- Mỗi trang ví dụ mở bằng dữ kiện dạng danh sách, không câu dẫn, không "Câu hỏi:" trước dữ kiện. "Diễn giải:" chỉ dùng số có trên chính trang đó.
- Trang ý tưởng chứng minh: lộ trình 3–5 bước, bất đẳng thức hoặc mẹo then chốt, chỗ giả thiết vào, bỏ giả thiết thì hỏng ở đâu; không chép chứng minh đầy đủ của ghi chú (chi tiết ở ghi chú diễn giả).
- Không `\text{}` chứa tiếng Việt trong KaTeX. Trong ghi chú diễn giả, không ghi "mới", "dựng", "V6", "mục 5"; nguồn gốc ví dụ mới chỉ ở storyboard và `review-log.md`.

### Mạch 1. Mở đầu (6 trang, 8 phút)

#### `1-01` Chiều VC và hàm phân lớp tuyến tính — bìa, điểm vào mạch 1 · 1 phút
- **Mặt trang:** h1 tên bài; h3 "Bài 03"; luận điểm (mục 2, bằng lời); "Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1"; "Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN".
- **Ghi chú diễn giả:** Bài 02 cho cỡ mẫu đủ theo lôgarit của số giả thuyết, nên không áp dụng được cho lớp hàm ngưỡng trên đường thẳng thực hay lớp hàm phân lớp tuyến tính, hai lớp có vô số phần tử. Luận điểm có ba phần: số cách gán nhãn trên một tập điểm hữu hạn đo độ phong phú của lớp; khi chiều VC hữu hạn, số này tăng theo đa thức; một tập thứ hai, chỉ dùng trong chứng minh, cho phép thay số giả thuyết bằng số cách gán nhãn. Điều kiện đo được là giả thiết (M) của bài. Nguồn: ghi chú Bài 03, đoạn mở đầu; Bổ đề 03.12; Định lý 03.15, 03.17; §9.
- **Lý do / nối:** luận điểm cả bài → tiên quyết.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu, §9.

#### `1-02` Tiên quyết và quy ước — mở đầu · 1,5 phút
- **Mặt trang:**
  - **Nhắc lại:** bất đẳng thức hợp (union bound), Chebyshev (Bổ đề 02.3), Hoeffding (Định lý 02.7).
  - **Ký hiệu:** ERM: tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization).
  - PAC: học xấp xỉ với xác suất cao (probably approximately correct).
  - **Nhắc lại:** lớp hữu hạn $\lvert\mathcal H\rvert=K$ chọn trước: $\sup_h\lvert L_S(h)-L_D(h)\rvert\le r_m=\sqrt{\ln(2K/\delta)/(2m)}$ với xác suất $\ge1-\delta$ (Định lý 02.14).
  - **Nhắc lại:** rủi ro vượt mức (excess risk) của ERM $\le2r_m$.
- **Ghi chú diễn giả:** Bất đẳng thức Hoeffding: với $V_1,\ldots,V_m$ độc lập, $V_i\in[a,b]$, xác suất trung bình lệch kì vọng ít nhất $\epsilon$ không quá $2e^{-2m\epsilon^2/(b-a)^2}$. Cận $2r_m$ cho rủi ro vượt mức là Hệ quả 02.16. Bài dùng lại ba công cụ của Bài 02 và ba kết quả của Bài 01: học PAC khả diễn và bất khả diễn (Định nghĩa 01.18, 01.25), điều kiện đo được của thuật toán (Định nghĩa 01.4), định lý không có bữa trưa miễn phí (Nhận xét 01.30). Ba câu ôn nhanh của ghi chú được dùng lại: $\sum_{j\le2}\binom5j=16$, bằng nửa $2^5=32$ (bổ đề Sauer–Shelah); $w=(2,2)$, $b=-1$ cho cách gán nhãn $(0,1,1)$ của ba điểm (nửa mặt phẳng); với biến trong $[-1,1]$, Định lý 02.7 cho $2e^{-m\epsilon^2/2}$ (miền dài $2$, tập mẫu ảo). Từ đại số tuyến tính: $p+1$ véc-tơ trong $\mathbb R^p$ phụ thuộc tuyến tính; hệ thuần nhất có nhiều ẩn hơn phương trình có nghiệm khác $0$. Nguồn: ghi chú Bài 03, Kiến thức tiên quyết, Câu hỏi ôn nhanh.
- **Lý do / nối:** mọi kết quả Bài 01–02 dùng trên mặt trang được nhắc lại ở đây; giải nghĩa hai chữ viết tắt trước khi "Mục tiêu" dùng → mục tiêu.
- **Mục tiêu / nguồn:** tất cả; Kiến thức tiên quyết.

#### `1-03` Mục tiêu — mở đầu · 1 phút
- **Mặt trang(danh sách đánh số, bằng lời, không kí hiệu; trần 80):**
  1. Tính chiều VC của lớp hàm ngưỡng, khoảng, nửa không gian bằng cận dưới và cận trên.
  2. Tính hàm tăng trưởng; so với cận Sauer–Shelah và số mọi cách gán nhãn.
  3. Trình bày năm bước chứng minh cận hội tụ đều.
  4. Tính cỡ mẫu đủ cho ERM từ chiều VC; so với lớp đã rời rạc hóa.
  5. Phát biểu định lý cơ bản; phản ví dụ: chiều VC vô hạn, lớp chọn theo tập huấn luyện, đếm tham số.
- **Ghi chú diễn giả:** Năm mục tiêu rút gọn câu chữ từ năm mục tiêu của ghi chú, giữ thứ tự. Mục tiêu 2 gồm cả so sánh hàm tăng trưởng với cận Sauer–Shelah và với số mọi cách gán nhãn; mục tiêu 2 của ghi chú nói "khi chiều VC hữu hạn". Mỗi bài tập trong tệp bài tập ghi mục tiêu tương ứng. Nguồn: ghi chú Bài 03, Mục tiêu học tập, §10.
- **Lý do / nối:** tiêu chí kiểm tra → nội dung.
- **Mục tiêu / nguồn:** tất cả; Mục tiêu học tập.

#### `1-04` Nội dung — mở đầu · 0,5 phút
- **Mặt trang:** `ol start="2"` với liên kết `#/2`…`#/7`: 2. Tách trọn vẹn và chiều VC; 3. Nửa không gian và hàm phân lớp tuyến tính; 4. Hàm tăng trưởng và bổ đề Sauer–Shelah; 5. Hội tụ đều trên lớp có chiều VC hữu hạn; 6. Rủi ro vượt mức của ERM và định lý cơ bản; 7. Tổng kết. Dòng đọc trước: "Đọc trước: UML §6.1–6.3."
- **Ghi chú diễn giả:** Mạch 2 và 3 đo một lớp vô hạn bằng số điểm lớn nhất mà lớp gán nhãn tùy ý được; mạch 4 đếm số cách gán nhãn trên nhiều điểm hơn; mạch 5 dùng số đếm đó thay cho số giả thuyết trong bất đẳng thức hợp; mạch 6 suy ra cỡ mẫu cho ERM và nêu điều kiện cần và đủ để học được. Nguồn: ghi chú Bài 03; §12.
- **Lý do / nối:** bản đồ mạch → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §12.

#### `1-05` Vấn đề trung tâm — mở đầu · 1 phút
- **Mặt trang:** một hộp `div.box`: "Câu hỏi: với một lớp giả thuyết vô hạn, đại lượng nào thay cho lôgarit của số giả thuyết trong cận cỡ mẫu?" (22 âm tiết sau nhãn).
- **Ghi chú diễn giả** (câu trả lời theo mạch, không trên mặt trang): (2) chiều VC, số điểm lớn nhất mà lớp gán nhãn tùy ý được, hữu hạn cho lớp hàm ngưỡng ($1$) và lớp khoảng ($2$) dù hai lớp vô hạn; (3) hàm phân lớp tuyến tính afin trên $p$ chỉ số đo có chiều VC $p+1$, và số tham số không thay được chiều VC; (4) trên $m$ điểm, lớp có chiều VC $d$ cho nhiều nhất $(em/d)^d$ cách gán nhãn khi $d\le m$; (5) lôgarit của số cách gán nhãn trên $2m$ điểm thay cho lôgarit của số giả thuyết, nên độ lệch đều có cỡ $\sqrt{d\ln m/m}$; (6) cỡ mẫu đủ cho ERM tăng theo chiều VC, và dưới (M) một lớp học được khi và chỉ khi chiều VC hữu hạn. Nguồn: ghi chú Bài 03, đoạn mở đầu, §4–§9.
- **Lý do / nối:** một vấn đề cốt lõi → hai câu hỏi cụ thể.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu.

#### `1-06` Ví dụ: hai câu hỏi về cỡ mẫu — ví dụ dẫn nhập · 3 phút
- **Mặt trang:**
  - Hàm ngưỡng (threshold) $h_t(x)=\mathbb 1[x\ge t]$, $t\in\mathbb R$: vô số hàm, nhưng chỉ sáu hàm khác nhau trên năm mức đo $\{1,\ldots,5\}$.
  - Hàm phân lớp tuyến tính (linear classifier) trên $p=10$ chỉ số đo: $h_{w,b}(x)=\mathbb 1[\langle w,x\rangle+b\ge0]$, $w\in\mathbb R^{10}$, $b\in\mathbb R$.
  - Với mọi phân bố, mọi nghiệm ERM cần rủi ro vượt mức $\le0{,}1$ với xác suất $\ge0{,}95$.
  - **Câu hỏi:** cần bao nhiêu quan sát cho mỗi lớp, và cho hai chỉ số đo?
- **Ghi chú diễn giả:** Đây là câu hỏi mở đầu và câu hỏi thực hành của ghi chú. Cả hai lớp có vô số phần tử, nên bán kính $r_m$ của Định lý 02.14 không xác định. Đếm số tham số thay cho lôgarit của số giả thuyết không dùng được: lớp các hàm $x\mapsto\mathbb 1[\sin(\theta x)>0]$, $\theta\in\mathbb R$, cũng chỉ có một tham số nhưng nhận được mọi tổ hợp nhãn trên những tập điểm lớn tùy ý. Đại lượng cần tìm đếm số tổ hợp nhãn mà lớp tạo ra trên các tập điểm hữu hạn. Nguồn: ghi chú Bài 03, Câu hỏi mở đầu; §3 (khối ứng dụng).
- **Lý do / nối:** ví dụ dẫn nhập trước mọi định nghĩa; hai ví dụ xuyên suốt của bài → tiêu đề mạch 2.
- **Mục tiêu / nguồn:** 4, 5; Câu hỏi mở đầu, §3.

### Mạch 2. Tách trọn vẹn và chiều VC (8 trang, 18 phút; thêm `2-07`)

#### `2-00` 2. Tách trọn vẹn và chiều VC — tiêu đề mạch, điểm vào mạch 2 · 0,5 phút
- **Mặt trang:** "2."; h2 "Tách trọn vẹn và chiều VC"; `p.strand-lead` (bảng mạch, 20 âm tiết); `p.strand-keys`: "thu hẹp · cách gán nhãn · tách trọn vẹn · chiều VC · cận dưới và cận trên".
- **Ghi chú diễn giả:** Kế thừa: cỡ mẫu theo lôgarit của số giả thuyết, chỉ cho lớp hữu hạn. Nhiệm vụ: thay việc đếm hàm bằng việc đếm các véc-tơ nhãn mà lớp tạo ra trên một tập điểm, rồi định nghĩa chiều VC. Đầu ra: chiều VC của lớp hàm ngưỡng và lớp khoảng, và cách chứng minh một chiều VC bằng hai chiều lập luận. Nguồn: ghi chú Bài 03, §1–§4.
- **Lý do / nối:** mạch 1 → thiết lập.
- **Mục tiêu / nguồn:** 1; §1–§4.

#### `2-01` Thiết lập bài toán — định nghĩa (khung) · 2,5 phút
- **Mặt trang:**
  - Quan sát $Z=(X,Y)\in\mathcal X\times\{0,1\}$, $S\sim D^m$; hàm lỗi 0–1 (0–1 loss); lớp $\mathcal H$ có thể vô hạn.
  - **Giả thiết:** (T1) độc lập cùng phân bố; (T5) $\mathcal H$ chọn trước khi lấy mẫu.
  - **Giả thiết:** (M) mỗi $h\in\mathcal H$ là giới hạn theo từng điểm của một dãy trong lớp con đếm được (countable subclass) $\mathcal H_0$.
  - Cần chặn: độ lệch đều (uniform deviation) $\sup_h\lvert L_S(h)-L_D(h)\rvert$ và rủi ro vượt mức $L_D(\hat h)-\inf_hL_D(h)$.
- **Ghi chú diễn giả:** Bài toán giữ tám thành phần của Bài 02; chỉ giả thiết (T4) đổi thành (T5), vì (T4) là (T5) cộng điều kiện lớp hữu hạn. Đối tượng so sánh là cận dưới đúng $\inf_hL_D(h)$, vì trên lớp vô hạn giá trị nhỏ nhất có thể không đạt (Nhận xét 01.17). Cố định: $D$, $\mathcal H$, mỗi $L_D(h)$. Ngẫu nhiên theo $S$: $L_S(h)$, véc-tơ giá trị $(h(X_1),\ldots,h(X_m))$ của mỗi $h$, độ lệch đều, $\hat h$. Điều kiện (M) bảo đảm độ lệch đều là một biến ngẫu nhiên; các lớp của bài đều thỏa (M) với lớp con có tham số hữu tỉ. Nguồn: ghi chú Bài 03, §1, §2.
- **Lý do / nối:** khung chung trước mọi kết quả; giả thiết (T5), (M) xuất hiện lần đầu → ví dụ lớp hàm ngưỡng.
- **Mục tiêu / nguồn:** 3, 4; §1, §2.

#### `2-02` Ví dụ: lớp hàm ngưỡng trên năm mức đo — ví dụ (ví dụ xuyên suốt), định nghĩa · 3 phút
- **Mặt trang:**
  - $\mathcal H_{\mathrm{thr}}=\{h_t:\ t\in\mathbb R\}$; với $t<t'$, $h_t$ và $h_{t'}$ khác nhau trên $[t,t')$: vô số hàm.
  - Trên $x_1<\cdots<x_m$: véc-tơ $(h_t(x_1),\ldots,h_t(x_m))$ chỉ phụ thuộc $\lvert\{i:x_i<t\}\rvert\in\{0,\ldots,m\}$: có $m+1$ véc-tơ.
  - **Định nghĩa 03.1.** Thu hẹp (restriction) $\mathcal H_C=\{(h(x_1),\ldots,h(x_k)):h\in\mathcal H\}$; mỗi phần tử là một cách gán nhãn (labeling) thực hiện được.
  - $C=(1,2,3,4,5)$: $\mathcal H_C=\{11111,\ 01111,\ 00111,\ 00011,\ 00001,\ 00000\}$, $6$ trong $2^5=32$ cách gán nhãn.
  - **Lưu ý:** $L_S(h)$ chỉ phụ thuộc véc-tơ trên $(X_1,\ldots,X_m)$, nhưng tập véc-tơ này phụ thuộc $S$.
  - {{một công thức hiển thị: định nghĩa thu hẹp}}
- **Ghi chú diễn giả:** Sáu véc-tơ là giá trị của sáu hàm $h_1,\ldots,h_6$ của Ví dụ 01.1 trên năm mức đo: lớp sáu hàm ngưỡng mà Bài 02 dùng với $K=6$ là thu hẹp của một lớp vô hạn lên năm điểm. Thu hẹp chỉ phụ thuộc lớp và bộ điểm, không phụ thuộc phân bố hay tập huấn luyện, và $\lvert\mathcal H_C\rvert\le\min\{\lvert\mathcal H\rvert,2^k\}$. Rủi ro thực nghiệm $L_S(h_t)$ nhận nhiều nhất $m+1$ giá trị khi $t$ chạy trên $\mathbb R$; vì tập $m+1$ véc-tơ đổi theo tập huấn luyện, chưa thể thay $K$ bằng $m+1$ trong Định lý 02.14. Một cách gán nhãn có thể không thực hiện được: với $C=(1,2)$, cách $(1,0)$ đòi $1\ge t$ và $2<t$. Nguồn: ghi chú Bài 03, §3 (Ví dụ 03.1), §4 (Định nghĩa 03.1, Ví dụ 03.2).
- **Lý do / nối:** trọng tâm trực quan lần đầu: số véc-tơ nhãn, không phải số hàm → tách trọn vẹn.
- **Mục tiêu / nguồn:** 1, 2; Ví dụ 03.1, Định nghĩa 03.1, Ví dụ 03.2.

#### `2-03` Tách trọn vẹn và chiều VC — định nghĩa, ví dụ · 2,5 phút
- **Mặt trang:**
  - **Định nghĩa 03.2.** $\mathcal H$ tách trọn vẹn (shatters) tập $C$ có $k$ phần tử nếu $\lvert\mathcal H_C\rvert=2^k$; tập rỗng luôn bị tách trọn vẹn.
  - **Định nghĩa 03.3.** Chiều Vapnik–Chervonenkis (VC dimension) $d=\operatorname{VCdim}(\mathcal H)$: số phần tử lớn nhất của một tập bị tách trọn vẹn.
  - $d=\infty$ nếu không có số lớn nhất như vậy.
  - **Ví dụ.** $\mathcal H_{\mathrm{thr}}$ tách trọn vẹn $\{0\}$ ($h_0(0)=1$, $h_1(0)=0$), không tách trọn vẹn $\{1,2\}$.
  - Lớp hữu hạn: $d\le\log_2\lvert\mathcal H\rvert$; sáu hàm ngưỡng: $d\le\lfloor\log_26\rfloor=2$.
- **Ghi chú diễn giả:** Tách trọn vẹn là tính chất của cặp lớp và tập điểm, không có phân bố hay tập huấn luyện. Hai điểm trùng nhau luôn nhận cùng nhãn, nên chỉ xét tập. Chiều VC không phụ thuộc $D$, $m$ hay cách tham số hóa lớp; $d\ge0$, và $d=0$ khi và chỉ khi mọi hàm của lớp trùng nhau trên $\mathcal X$. Mọi tập con của một tập bị tách trọn vẹn cũng bị tách trọn vẹn: mở rộng một cách gán nhãn của tập con một cách tùy ý rồi lấy giả thuyết thực hiện cách mở rộng. Nguồn: ghi chú Bài 03, §4, Định nghĩa 03.2, 03.3 và các đoạn sau.
- **Lý do / nối:** hai định nghĩa then chốt, ví dụ ngay trên lớp xuyên suốt → cách chứng minh $d=k$.
- **Mục tiêu / nguồn:** 1; Định nghĩa 03.2, 03.3.

#### `2-04` Cận dưới và cận trên cho chiều VC — kỹ thuật (lần đầu trong học phần) · 2,5 phút
- **Mặt trang:**
  - **Kỹ thuật.** Cận dưới $d\ge k$: một tập $k$ phần tử bị tách trọn vẹn.
  - Cận trên $d\le k$: mọi tập $k+1$ phần tử có một cách gán nhãn không thực hiện được.
  - **Lưu ý:** cận trên cần mọi tập $k+1$ phần tử, không chỉ một tập.
  - Dùng khi: tính chiều VC của một lớp cụ thể. Dùng ở: Mệnh đề 03.5, 03.6, 03.9.
- **Ghi chú diễn giả:** Cận trên chỉ cần xét tập $k+1$ phần tử: một tập lớn hơn bị tách trọn vẹn sẽ chứa một tập con $k+1$ phần tử bị tách trọn vẹn, theo tính chất tập con. Hai lỗi đối xứng: một hình vẽ tập bị tách trọn vẹn chỉ là nhân chứng cho cận dưới; một tập không bị tách trọn vẹn không cho cận trên. Một ví dụ của lỗi thứ hai: ba điểm thẳng hàng không bị lớp nửa mặt phẳng tách trọn vẹn, dù lớp này có chiều VC bằng $3$ (Mệnh đề 03.9, Ví dụ 03.3). Bài tập 03.2(c) có hai lời giải chưa đầy đủ, mỗi lời giải mắc một trong hai lỗi. Nguồn: ghi chú Bài 03, Nhận xét 03.4; tệp bài tập, Bài tập 03.2(c).
- **Lý do / nối:** kỹ thuật dùng lại qua học phần, đặt trước nơi dùng lần đầu theo thứ tự của ghi chú → hai mệnh đề trên đường thẳng.
- **Mục tiêu / nguồn:** 1; Nhận xét 03.4.

#### `2-05` Chiều VC của lớp hàm ngưỡng và lớp khoảng — trực quan, kết quả · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** $h_t(x)$ không giảm theo $x$; với lớp khoảng, tập $\{x:h(x)=1\}$ là một khoảng.
  - **Mệnh đề 03.5.** **Giả thiết:** (a) $\mathcal X=\mathbb R$, lớp $\mathcal H_{\mathrm{thr}}$; (b) $\mathcal X=\{1,\ldots,5\}$, lớp $\{h_t:t=1,\ldots,6\}$. **Bảo đảm:** chiều VC của cả hai lớp bằng $1$.
  - **Mệnh đề 03.6.** **Giả thiết:** $\mathcal X=\mathbb R$, lớp khoảng đóng (closed interval) $\mathcal H_{\mathrm{int}}=\{h_{u,v}:u\le v\}$, $h_{u,v}(x)=\mathbb 1[u\le x\le v]$.
  - **Bảo đảm:** $\operatorname{VCdim}(\mathcal H_{\mathrm{int}})=2$. Cả hai mệnh đề là khẳng định tất định về lớp.
  - {{hình F1 bên phải, grid2}}
- **Ghi chú diễn giả:** Hai mệnh đề là khẳng định tất định: không có phân bố hay tập huấn luyện ngẫu nhiên. Lớp hàm ngưỡng có vô số phần tử, nên lôgarit của số giả thuyết không cho cận cỡ mẫu; lớp chỉ gán nhãn tùy ý được các tập một điểm. Đọc hình: hàng trên là hai điểm $0$, $1$ với bốn khoảng $[0,1]$, $[0,0]$, $[1,1]$, $[2,2]$, mỗi khoảng thực hiện một cách gán nhãn; hàng dưới là ba điểm với cách gán nhãn $(1,0,1)$: mọi khoảng chứa điểm đầu và điểm cuối thì chứa điểm giữa. Nguồn: ghi chú Bài 03, §4, Mệnh đề 03.5, 03.6.
- **Lý do / nối:** hai kết quả chính đầu tiên, trực quan trên cùng trang → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 1; Mệnh đề 03.5, 03.6.

#### `2-06` Ý tưởng chứng minh: chiều VC trên đường thẳng — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.**
  1. Cận dưới: $\{0\}$ bị $\mathcal H_{\mathrm{thr}}$ tách trọn vẹn; $\{0,1\}$ bị $\mathcal H_{\mathrm{int}}$ tách trọn vẹn, nhờ $[0,1]$, $[0,0]$, $[1,1]$, $[2,2]$.
  2. Hàm ngưỡng, mọi $x_1<x_2$: cách $(1,0)$ đòi $x_2<t\le x_1$.
  3. Khoảng, mọi $x_1<x_2<x_3$: cách $(1,0,1)$ đòi $u\le x_1$, $x_3\le v$, nên $h_{u,v}(x_2)=1$.
  - **Kỹ thuật.** Cận trên dùng thứ tự của các điểm trên đường thẳng.
  - **Kết luận:** hai lớp cùng lực lượng (cardinality) với $\mathbb R$ nhưng khác chiều VC.
- **Ghi chú diễn giả** (~170 âm tiết): Lộ trình theo kỹ thuật vừa nêu: một tập bị tách trọn vẹn cho cận dưới, một cách gán nhãn không thực hiện được trên mọi tập lớn hơn một điểm cho cận trên. Tính chất then chốt của hàm ngưỡng là tính không giảm: mọi điểm bên phải một điểm nhãn $1$ cũng nhãn $1$. Lập luận ở bước 2 đúng với mọi $t\in\mathbb R$, nên đúng cho cả lớp vô hạn và lớp sáu hàm. Tính chất then chốt của lớp khoảng là tính lồi của tập nhãn $1$. Ở bước 3, bốn khoảng là nghiệm tường minh và chỉ cho cận dưới; cận trên là bước 4, đúng cho mọi bộ ba điểm. Trong $\mathbb R^p$ không có thứ tự như vậy, nên cận trên cho nửa không gian cần một công cụ hình học. Nguồn: ghi chú Bài 03, chứng minh Mệnh đề 03.5, 03.6; đoạn cuối §4.
- **Lý do / nối:** một trang ý tưởng chứng minh cho hai mệnh đề cùng cấu trúc → mạch 3 (không có thứ tự trong $\mathbb R^p$).
- **Mục tiêu / nguồn:** 1; chứng minh Mệnh đề 03.5, 03.6.

#### `2-07` Bài tập: hai lời giải cho lớp hợp hai khoảng — bài tập trên lớp (Bài tập 03.2(c)), lời giải ở fragment · 2 phút (thêm theo quyết định của điều phối viên, 2026-11-15)
- **Mặt trang (deck):** $\mathcal H_{2\mathrm{int}}$: hợp hai khoảng đóng; lời giải thứ nhất ($16$ cách của $\{1,2,3,4\}$, nên $d=4$); lời giải thứ hai ($(1,0,1,0,1)$ của $\{1,\ldots,5\}$ không thực hiện được, nên $d\le4$); **Câu hỏi:** theo Nhận xét 03.4, mỗi lời giải thiếu phần nào? `[f]` **Lời giải:** thứ nhất thiếu cận trên cho mọi tập năm điểm; `[f]` thứ hai: một tập không cho cận trên; thiếu cả cận dưới.
- **Ghi chú diễn giả:** lời giải đầy đủ của (b) (hai khối nhãn $1$; nguyên lý chuồng bồ câu cho mọi bộ năm điểm), nối với ba điểm thẳng hàng của lớp nửa mặt phẳng.
- **Lý do / nối:** cụm chính của mạch 2 có một bài tập với lời giải trên mặt trang (quyết định điều phối viên; cổng duyệt, phát hiện "không có trang Bài tập giữa các cụm") → tiêu đề mạch 3.
- **Mục tiêu / nguồn:** 1; tệp bài tập, Bài tập 03.2(b), (c) và lời giải; Nhận xét 03.4.

### Mạch 3. Nửa không gian và hàm phân lớp tuyến tính (8 trang, 19 phút)

#### `3-00` 3. Nửa không gian và hàm phân lớp tuyến tính — tiêu đề mạch, điểm vào mạch 3 · 0,5 phút
- **Mặt trang:** "3."; h2 "Nửa không gian và hàm phân lớp tuyến tính"; `p.strand-lead` (bảng mạch, 25 âm tiết); `p.strand-keys`: "nửa không gian · đơn hình · phân hoạch Radon · số tham số".
- **Ghi chú diễn giả:** Kế thừa: kỹ thuật cận dưới và cận trên, và hai chứng minh dùng thứ tự trên đường thẳng. Nhiệm vụ: tính chiều VC của lớp hàm phân lớp tuyến tính trong không gian nhiều chiều, nơi không có thứ tự; công cụ thay thế là một kết quả hình học về bao lồi. Đầu ra: chiều VC bằng số chỉ số đo cộng một cho lớp có hệ số tự do, và chiều VC khác số tham số ở các lớp khác. Nguồn: ghi chú Bài 03, §5.
- **Lý do / nối:** mạch 2 → định nghĩa nửa không gian.
- **Mục tiêu / nguồn:** 1, 5; §5.

#### `3-01` Nửa không gian afin và nửa không gian thuần nhất — định nghĩa · 2 phút
- **Mặt trang:**
  - **Định nghĩa 03.7.** Với $w\in\mathbb R^p$, $b\in\mathbb R$: $h_{w,b}(x)=\mathbb 1[\langle w,x\rangle+b\ge0]$.
  - Nửa không gian afin (affine halfspace): $\mathcal H^p_{\mathrm{aff}}=\{h_{w,b}\}$, lớp hàm phân lớp tuyến tính afin.
  - Nửa không gian thuần nhất (homogeneous halfspace): $\mathcal H^p_{\mathrm{hom}}=\{h_{w,0}\}$, không có hệ số tự do.
  - Điểm trên siêu phẳng (hyperplane) $\langle w,x\rangle+b=0$ nhận nhãn $1$; $w=0$ cho hàm hằng.
  - $p=1$: $\mathcal H^1_{\mathrm{aff}}$ gồm $\mathbb 1[x\ge t]$, $\mathbb 1[x\le t]$ và hai hàm hằng.
- **Ghi chú diễn giả:** Với $w=0$, $h_{0,b}$ là hằng $1$ khi $b\ge0$ và hằng $0$ khi $b<0$. Quy ước "$\ge0$" đặt siêu phẳng vào phía nhãn $1$; quy ước này được dùng ở cận trên của chứng minh. Hàm phân lớp tuyến tính trên mười chỉ số đo của câu hỏi thực hành là lớp $\mathcal H^{10}_{\mathrm{aff}}$, trên hai chỉ số đo là $\mathcal H^2_{\mathrm{aff}}$, lớp các nửa mặt phẳng. Trong $\mathbb R^p$ không có thứ tự như trên đường thẳng, nên cận trên cần một công cụ hình học. Nguồn: ghi chú Bài 03, §5, Định nghĩa 03.7 và hai đoạn sau.
- **Lý do / nối:** định nghĩa lớp của ứng dụng → ba điểm trong mặt phẳng.
- **Mục tiêu / nguồn:** 1; Định nghĩa 03.7.

#### `3-02` Ví dụ: nửa mặt phẳng trên ba điểm — ví dụ (Ví dụ 03.3, Bước 1–2) · 3 phút
- **Mặt trang:**
  - Ba điểm $(0,0)$, $(1,0)$, $(0,1)$; cách gán nhãn $(y_0,y_1,y_2)$; lớp $\mathcal H^2_{\mathrm{aff}}$.
  - Đặt $b=2y_0-1$, $w_i=2y_i-1-b$: khi đó $\langle w,x\rangle+b$ bằng $1$ tại điểm nhãn $1$, $-1$ tại điểm nhãn $0$.
  - $(1,0,1)$: $b=1$, $w=(-2,0)$; $(0,1,1)$: $b=-1$, $w=(2,2)$.
  - Cả tám cách gán nhãn thực hiện được: ba điểm bị tách trọn vẹn.
  - Ba điểm thẳng hàng $(0,0)$, $(1,0)$, $(2,0)$: cách $(1,0,1)$ không thực hiện được.
  - {{hình F2 bên phải, grid2}}
- **Ghi chú diễn giả:** Ba điểm là các đỉnh của một đơn hình trong mặt phẳng. Công thức cho $\langle w,0\rangle+b=2y_0-1$ và $\langle w,\mathbf e_i\rangle+b=w_i+b=2y_i-1$; số $2y-1$ bằng $1$ khi $y=1$ và $-1$ khi $y=0$. Cách $(0,1,1)$ là lời giải của câu ôn nhanh 2. Đọc hình: tám ô nhỏ, mỗi ô một cách gán nhãn; điểm nhãn $1$ tô đặc, điểm nhãn $0$ rỗng, đường thẳng là $\langle w,x\rangle+b=0$ theo công thức, phía nhãn $1$ tô nền; hai cách hằng không có đường thẳng. Trên đường thẳng chứa ba điểm thẳng hàng, mỗi $h_{w,b}$ là một nửa đường thẳng hoặc một hàm hằng, nên $(1,0,1)$ không thực hiện được. Tập này không bị tách trọn vẹn, và theo kỹ thuật cận dưới và cận trên, điều đó không cho cận trên. Nguồn: ghi chú Bài 03, Ví dụ 03.3, Bước 1–2; Câu hỏi ôn nhanh 2.
- **Lý do / nối:** ví dụ trước phát biểu: cận dưới tường minh trên ba điểm → công cụ cho cận trên.
- **Mục tiêu / nguồn:** 1; Ví dụ 03.3.

#### `3-03` Phân hoạch Radon — trực quan, bổ đề (công cụ) · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Hai đường chéo hình vuông cắt nhau tại $(\tfrac12,\tfrac12)$: bao lồi (convex hull) của hai cặp đỉnh giao nhau.
  - **Bổ đề 03.8.** **Giả thiết:** $p\ge1$; $p+2$ điểm $x_1,\ldots,x_{p+2}\in\mathbb R^p$.
  - **Bảo đảm:** có $I$, $J$ khác rỗng, rời nhau, $I\cup J=\{1,\ldots,p+2\}$, và display $z\in\operatorname{conv}\{x_i:i\in I\}\cap\operatorname{conv}\{x_j:j\in J\}$.
  - **Chứng minh.** Hệ $\sum_ia_ix_i=0$, $\sum_ia_i=0$ có $p+1$ phương trình, $p+2$ ẩn: có nghiệm $a\ne0$; $I=\{i:a_i>0\}$.
  - {{hình F3 bên phải, grid2; một công thức hiển thị}}
- **Ghi chú diễn giả:** Nhắc lại: một tổ hợp lồi (convex combination) của $x_1,\ldots,x_k$ là $\sum_i\lambda_ix_i$ với $\lambda_i\ge0$, $\sum_i\lambda_i=1$, và bao lồi $\operatorname{conv}$ là tập mọi tổ hợp lồi đó. Cặp $(I,J)$ gọi là một phân hoạch Radon (Radon partition); tên định lý là định lý Radon (Radon's theorem). Trong chứng minh, $J=\{j:a_j\le0\}$; vì $a\ne0$ và tổng các hệ số bằng $0$, nghiệm có cả hệ số dương lẫn hệ số âm, nên hai tập khác rỗng. Chia cho $\alpha=\sum_{i\in I}a_i$ được hai tổ hợp lồi của cùng điểm $z$. Đọc hình: bên trái hình vuông với hai đường chéo và điểm $z=(\tfrac12,\tfrac12)$; bên phải tam giác $(0,0)$, $(3,0)$, $(0,3)$ với điểm $(1,1)$ bên trong, $J=\{(1,1)\}$. Nguồn: ghi chú Bài 03, §5, Bổ đề 03.8 và chứng minh; Phụ lục A.
- **Lý do / nối:** công cụ cho cận trên của mệnh đề sau, phát biểu và chứng minh một dòng chung trang → phát biểu chiều VC của nửa không gian.
- **Mục tiêu / nguồn:** 1; Bổ đề 03.8.

#### `3-04` Chiều VC của lớp nửa không gian — trực quan, kết quả · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** $p+1$ đỉnh của một đơn hình (simplex) gán nhãn tùy ý được; mọi $p+2$ điểm có một phân hoạch Radon.
  - **Mệnh đề 03.9.** **Giả thiết:** $p\ge1$; hai lớp $\mathcal H^p_{\mathrm{aff}}$, $\mathcal H^p_{\mathrm{hom}}$.
  - **Bảo đảm** (tất định, theo $p$): (a) $\operatorname{VCdim}(\mathcal H^p_{\mathrm{aff}})=p+1$; (b) $\operatorname{VCdim}(\mathcal H^p_{\mathrm{hom}})=p$.
  - Mười chỉ số đo: $\mathcal H^{10}_{\mathrm{aff}}$ có $d=11$; hai chỉ số đo: $\mathcal H^2_{\mathrm{aff}}$ có $d=3$.
- **Ghi chú diễn giả:** Một đơn hình là bao lồi của $p+1$ điểm độc lập afin (affinely independent), tức các hiệu $x_1-x_0,\ldots,x_p-x_0$ độc lập tuyến tính; trong mặt phẳng là một tam giác. Hệ số tự do $b$ cho thêm đúng một điểm: lớp thuần nhất luôn gán nhãn $1$ cho gốc tọa độ, nên không tách trọn vẹn tập nào chứa gốc. Hai con số $11$ và $3$ là chiều VC của hai lớp trong câu hỏi thực hành. Nguồn: ghi chú Bài 03, §5, Mệnh đề 03.9 và câu cuối chứng minh; tệp bài tập, Bài tập 03.3(c).
- **Lý do / nối:** kết quả chính của mạch → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 1; Mệnh đề 03.9.

#### `3-05` Ý tưởng chứng minh: chiều VC của nửa không gian — ý tưởng chứng minh · 3,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.**
  1. Cận dưới (a): $\{0,\mathbf e_1,\ldots,\mathbf e_p\}$, với $\mathbf e_i$ là véc-tơ đơn vị; $b=2y_0-1$, $w_i=2y_i-1-b$.
  2. Cận trên (a): lấy $p+2$ điểm, phân hoạch Radon $(I,J)$, gán $1$ trên $I$, $0$ trên $J$; đặt $g(x)=\langle w,x\rangle+b$.
  3. $g$ afin: display $g(z)=\sum_{i\in I}\lambda_ig(x_i)\ge0$ và $g(z)=\sum_{j\in J}\mu_jg(x_j)<0$.
  4. Dấu $<0$ cần $J\ne\varnothing$ và quy ước $\ge0$; (b) dùng phụ thuộc tuyến tính của $p+1$ véc-tơ.
  - **Kỹ thuật.** Hàm afin giữ tổ hợp lồi: $g(\sum_i\lambda_ix_i)=\sum_i\lambda_ig(x_i)$.
  - {{một công thức hiển thị; đo ở 390 px}}
- **Ghi chú diễn giả** (~220 âm tiết): Lộ trình: cận dưới bằng nghiệm tường minh trên các đỉnh của đơn hình, cận trên bằng phân hoạch Radon. Bước 1 là công thức của ví dụ ba điểm, đúng cho mọi $p$; cùng lập luận đúng cho mọi $p+1$ điểm độc lập afin vì ma trận có các hàng $(x_i^\top,1)$ khả nghịch (Bài tập 03.3(a)). Bước 2–3: viết $z=\sum_{i\in I}\lambda_ix_i=\sum_{j\in J}\mu_jx_j$ với hệ số không âm, mỗi họ có tổng $1$; nếu $h_{w,b}$ thực hiện cách gán nhãn thì $g(x_i)\ge0$ trên $I$ và $g(x_j)<0$ trên $J$, nên hai biểu diễn của $g(z)$ cho hai dấu trái nhau. Quy ước $\ge0$ vào ở bước 4: phía nghiêm ngặt $g<0$ nằm trên $J$, và một tổ hợp lồi của các số âm với ít nhất một số hạng là số âm. Phần (b): cận dưới dùng $\mathbf e_1,\ldots,\mathbf e_p$ với $w=\sum_i(2y_i-1)\mathbf e_i$; cận trên dùng một quan hệ phụ thuộc tuyến tính $\sum_ia_ix_i=0$, tách chỉ số theo dấu (Phụ lục A). Kết quả: $d=11$ cho mười chỉ số đo, $d=3$ cho hai chỉ số đo. Nguồn: ghi chú Bài 03, chứng minh Mệnh đề 03.9; Phụ lục A; tệp bài tập, Bài tập 03.3.
- **Lý do / nối:** lộ trình bốn bước, chỗ dùng quy ước $\ge0$ → kiểm tra trên bốn điểm.
- **Mục tiêu / nguồn:** 1; chứng minh Mệnh đề 03.9.

#### `3-06` Ví dụ: bốn điểm trong mặt phẳng — ví dụ (Ví dụ 03.3, Bước 3–4), kiểm tra · 3 phút
- **Mặt trang:**
  - Hình vuông $(0,0)$, $(1,0)$, $(1,1)$, $(0,1)$; lớp $\mathcal H^2_{\mathrm{aff}}$; $16$ cách gán nhãn.
  - Cách "chéo" ($1$ tại $(0,0)$, $(1,1)$) và cách bù không thực hiện được; $z=(\tfrac12,\tfrac12)$.
  - Thực hiện được $14=2+4+4+4$: hằng, tách một đỉnh, tách hai đỉnh kề, bù của tách một đỉnh.
  - Tam giác $(0,0)$, $(3,0)$, $(0,3)$ và $(1,1)=\tfrac13(0,0)+\tfrac13(3,0)+\tfrac13(0,3)$: nhãn $1$ tại ba đỉnh, $0$ tại $(1,1)$ không thực hiện được.
  - **Diễn giải:** mỗi cấu hình bốn điểm thiếu ít nhất một cách gán nhãn, khớp $d=3$.
- **Ghi chú diễn giả:** Với hình vuông, phân hoạch Radon là hai đường chéo; đổi vai $I$ và $J$ cho cách gán nhãn bù. Với tam giác, $J=\{(1,1)\}$ và $I$ là ba đỉnh. Mỗi cấu hình bốn điểm của mặt phẳng thiếu ít nhất một cách gán nhãn; lý do chung là bổ đề Radon. Cách tách hai đỉnh kề dùng một đường song song với một cạnh. Nguồn: ghi chú Bài 03, Ví dụ 03.3, Bước 3–4.
- **Lý do / nối:** kiểm tra cận trên bằng số trên hai cấu hình → số tham số.
- **Mục tiêu / nguồn:** 1; Ví dụ 03.3.

#### `3-07` Số tham số và chiều VC — nhận xét, phản ví dụ · 2 phút
- **Mặt trang:**
  - **Nhận xét 03.10.**
  - (i) $\mathcal H^p_{\mathrm{aff}}$: $p+1$ tham số $(w,b)$ và $d=p+1$.
  - (ii) $\mathcal H_{\sin}=\{x\mapsto\mathbb 1[\sin(\theta x)>0]:\theta\in\mathbb R\}$: một tham số; với mọi $k$, $\{2^{-1},\ldots,2^{-k}\}$ bị tách trọn vẹn, nên $d=\infty$.
  - (iii) Trên $\mathbb R$, $\{x\mapsto\mathbb 1[(w_1+\cdots+w_p)x\ge0]:w\in\mathbb R^p\}$: $p$ tham số, ba hàm, $d=1$.
  - **Kết luận:** chiều VC có thể lớn hơn hoặc nhỏ hơn số tham số.
- **Ghi chú diễn giả:** Ở (iii), ba hàm là $\mathbb 1[x\ge0]$, $\mathbb 1[x\le0]$ và hằng $1$, theo dấu của $w_1+\cdots+w_p$; đây là $\mathcal H^1_{\mathrm{hom}}$ viết với $p$ tham số, nên $d=1$ theo Mệnh đề 03.9(b). Ở (ii), với $x_i=2^{-i}$ và cách gán nhãn $y$, tham số $\theta=\pi\big(1+\sum_{j=1}^k(1-y_j)2^j\big)$ thực hiện $y$ (Bài tập 03.5(a)); chẳng hạn $k=3$, $y=(1,0,1)$ cho $\theta=5\pi$, và $\sin(5\pi/2)=1$, $\sin(5\pi/4)<0$, $\sin(5\pi/8)>0$. Với nửa không gian afin, đẳng thức $d=p+1$ được chứng minh riêng cho lớp đó, không suy ra từ việc đếm tham số. Nguồn: ghi chú Bài 03, Nhận xét 03.10; tệp bài tập, Bài tập 03.5(a), (b).
- **Lý do / nối:** phản ví dụ "thay chiều VC bằng số tham số" (mục tiêu 5), đúng vị trí của ghi chú → tiêu đề mạch 4.
- **Mục tiêu / nguồn:** 5; Nhận xét 03.10.

### Mạch 4. Hàm tăng trưởng và bổ đề Sauer–Shelah (7 trang, 18,5 phút)

#### `4-00` 4. Hàm tăng trưởng và bổ đề Sauer–Shelah — tiêu đề mạch, điểm vào mạch 4 · 0,5 phút
- **Mặt trang:** "4."; h2 "Hàm tăng trưởng và bổ đề Sauer–Shelah"; `p.strand-lead` (bảng mạch, 23 âm tiết); `p.strand-keys`: "hàm tăng trưởng · tổng nhị thức · quy nạp kép · công thức Pascal".
- **Ghi chú diễn giả:** Kế thừa: chiều VC, số điểm lớn nhất mà lớp gán nhãn tùy ý được. Chiều VC chỉ nói rằng trên nhiều điểm hơn có cách gán nhãn bị thiếu; bất đẳng thức hợp cần biết còn lại bao nhiêu cách. Nhiệm vụ: đếm số cách gán nhãn trong trường hợp xấu nhất và chặn nó theo chiều VC. Đầu ra: một đa thức bậc $d$ của số điểm, thay cho $2^m$. Nguồn: ghi chú Bài 03, §6.
- **Lý do / nối:** mạch 3 → định nghĩa hàm tăng trưởng.
- **Mục tiêu / nguồn:** 2; §6.

#### `4-01` Hàm tăng trưởng — định nghĩa, ví dụ · 3 phút
- **Mặt trang:**
  - Định lý 02.14 cộng $K$ biến cố hỏng; với lớp vô hạn, đếm số cách gán nhãn trong trường hợp xấu nhất.
  - **Định nghĩa 03.11.** Hàm tăng trưởng (growth function): display $\Pi_{\mathcal H}(m)=\max_{C\in\mathcal X^m}\lvert\mathcal H_C\rvert$, trên mọi bộ $m$ điểm, cho phép điểm lặp.
  - $\Pi_{\mathcal H}(m)$ tất định; trên mọi tập huấn luyện, $\lvert\mathcal H_{(X_1,\ldots,X_m)}\rvert\le\Pi_{\mathcal H}(m)\le\min\{2^m,\lvert\mathcal H\rvert\}$.
  - $\Pi_{\mathcal H}(m)=2^m$ khi và chỉ khi $m\le d$.
  - **Ví dụ 03.4.** $\Pi_{\mathcal H_{\mathrm{thr}}}(m)=m+1$; $\Pi_{\mathcal H_{\mathrm{int}}}(m)=\binom{m+1}2+1$; tại $m=5$: $6$ và $16$, so với $2^5=32$.
  - {{một công thức hiển thị}}
- **Ghi chú diễn giả:** Số $\lvert\mathcal H_{(X_1,\ldots,X_m)}\rvert$ là ngẫu nhiên; giá trị lớn nhất lấy trên mọi bộ điểm nên $\Pi_{\mathcal H}(m)$ là một số. Vì bộ điểm được phép lặp, $\Pi_{\mathcal H}(m)$ không giảm theo $m$. Đẳng thức $\Pi_{\mathcal H}(m)=2^m$ khi $m\le d$: lấy $m$ điểm của một tập bị tách trọn vẹn; ngược lại, một bộ có điểm lặp cho nhiều nhất $2^{m-1}$ cách, và một bộ $m$ điểm phân biệt có đủ $2^m$ cách là một tập bị tách trọn vẹn. Với hàm ngưỡng trên $x_1<\cdots<x_m$, cách gán nhãn là một dãy $0$ rồi một dãy $1$, xác định bởi số nhãn $1$. Với lớp khoảng, cách gán nhãn là toàn $0$ hoặc một khối liền các nhãn $1$ từ chỉ số $i$ đến $i'\ge i$: $\binom{m+1}2$ khối và cách toàn $0$. Số $16$ bằng $\sum_{j\le2}\binom5j$ của câu ôn nhanh 1. Nguồn: ghi chú Bài 03, §6, Định nghĩa 03.11, Ví dụ 03.4.
- **Lý do / nối:** đại lượng thay cho $K$, giá trị trên hai lớp xuyên suốt → bổ đề Sauer–Shelah.
- **Mục tiêu / nguồn:** 2; Định nghĩa 03.11, Ví dụ 03.4.

#### `4-02` Bổ đề Sauer–Shelah — trực quan, kết quả · 3 phút
- **Mặt trang:**
  - **Trực quan.** Khi $m>d$, số cách gán nhãn tăng như đa thức bậc $d$ của $m$, thay cho $2^m$ (hình, $d=3$).
  - **Bổ đề 03.12.** **Giả thiết:** $\mathcal H$ khác rỗng, chiều VC $d<\infty$; $m\ge1$.
  - **Bảo đảm** (tất định): (a) $\Pi_{\mathcal H}(m)\le\sum_{j=0}^{d}\binom mj$, với $\binom mj=0$ khi $j>m$;
  - (b) nếu $1\le d\le m$ thì $\sum_{j=0}^{d}\binom mj\le(em/d)^d$.
  - Do đó $\ln\Pi_{\mathcal H}(m)\le d\ln(em/d)$, so với $\ln2^m=m\ln2$.
  - {{hình F4 bên phải, grid2}}
- **Ghi chú diễn giả:** Bổ đề là hai bất đẳng thức tổ hợp, tất định. Phần (a) phụ thuộc lớp chỉ qua $d$, không qua số phần tử. Đọc hình: trục ngang $m$ từ $1$ đến $20$, trục dọc thang lôgarit từ $1$ đến $10^7$; ba đường cho $2^m$, tổng nhị thức với $d=3$ và $(em/3)^3$ (từ $m=3$); bốn điểm vuông là hàm tăng trưởng của lớp nửa mặt phẳng tại $m=1,\ldots,4$: $2;\ 4;\ 8;\ 14$. Tại $m=20$, tổng nhị thức bằng $1351$, dạng đóng bằng $5951{,}27$, còn $2^{20}=1\,048\,576$. Đường $2^m$ là đường thẳng trên thang lôgarit, hai đường kia cong xuống. Nguồn: ghi chú Bài 03, §6, Bổ đề 03.12 và câu cuối chứng minh; Ví dụ 03.5.
- **Lý do / nối:** kết quả chính của mạch, trực quan bằng hình → ý tưởng chứng minh phần (a).
- **Mục tiêu / nguồn:** 2; Bổ đề 03.12.

#### `4-03` Ý tưởng chứng minh: bổ đề Sauer–Shelah, phần (a) — ý tưởng chứng minh · 3,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.**
  1. Cố định $C=(x_1,\ldots,x_m)$, $C'=(x_1,\ldots,x_{m-1})$; $Y_1$: các cách gán nhãn của $C'$ mở rộng được theo cả hai nhãn của $x_m$.
  2. Đếm: display $\lvert\mathcal H_C\rvert=\lvert\mathcal H_{C'}\rvert+\lvert Y_1\rvert$.
  3. $Y_1$ tách trọn vẹn $B$ thì $\mathcal H$ tách trọn vẹn $B\cup\{x_m\}$: chiều VC của $Y_1$ không quá $d-1$.
  4. Quy nạp kép (double induction) theo $(m,d)$, rồi công thức Pascal (Pascal's rule) $\binom{m-1}j+\binom{m-1}{j-1}=\binom mj$.
  - **Kỹ thuật.** Tách theo nhãn của điểm cuối rồi quy nạp.
  - {{một công thức hiển thị}}
- **Ghi chú diễn giả** (~200 âm tiết): Lộ trình: quy nạp kép theo số điểm và chiều VC. Mỗi cách gán nhãn của $C'$ mở rộng thành một hoặc hai cách gán nhãn của $C$, và thành hai khi và chỉ khi nó thuộc $Y_1$; đó là đẳng thức đếm ở bước 2. Bước 3 là chỗ chiều VC giảm: nếu $Y_1$ tách trọn vẹn một tập vị trí $B$ của $C'$, mỗi cách gán nhãn của $B$ khớp một phần tử của $Y_1$, và cả hai nhãn của $x_m$ đi kèm được, nên $B\cup\{x_m\}$ bị tách trọn vẹn. Giả thiết quy nạp cho $\lvert\mathcal H_{C'}\rvert\le\sum_{j\le d}\binom{m-1}j$ và $\lvert Y_1\rvert\le\sum_{j\le d-1}\binom{m-1}j$; công thức Pascal cộng hai tổng thành $\sum_{j\le d}\binom mj$, rồi lấy giá trị lớn nhất trên các bộ $C$. Giả thiết quy nạp áp dụng cho mọi tập véc-tơ nhãn trên $m-1$ vị trí, không chỉ cho các thu hẹp của $\mathcal H$; trường hợp gốc $m=0$ hoặc $d=0$ và bộ có điểm lặp nằm ở Phụ lục B. Khi $x_m$ trùng một điểm trước nó, $Y_1=\varnothing$. Bài tập 03.6 cho một cách chứng minh khác bằng phép dồn. Nguồn: ghi chú Bài 03, chứng minh Bổ đề 03.12, Bước 1–2; Phụ lục B; UML §6.5.1.
- **Lý do / nối:** lộ trình bốn bước, chỗ chiều VC giảm → kiểm tra trên lớp khoảng.
- **Mục tiêu / nguồn:** 2; chứng minh Bổ đề 03.12(a), Phụ lục B.

#### `4-04` Ví dụ: tách theo điểm cuối cho lớp khoảng trên ba điểm — ví dụ, kiểm tra · 2,5 phút
- **Mặt trang:**
  - $\mathcal H_{\mathrm{int}}$ ($d=2$), $C=(1,2,3)$, $C'=(1,2)$.
  - $\mathcal H_C=\{000,\ 100,\ 010,\ 001,\ 110,\ 011,\ 111\}$: $7$ cách, thiếu $101$.
  - $\mathcal H_{C'}=\{00,\ 10,\ 01,\ 11\}$; $Y_1=\{00,\ 01,\ 11\}$, vì $10$ chỉ mở rộng thành $100$.
  - $7=4+3$; $Y_1$ thiếu $10$, nên chiều VC của $Y_1$ bằng $1=d-1$.
  - Pascal: $4+3=\big(\binom20+\binom21+\binom22\big)+\big(\binom20+\binom21\big)=\binom30+\binom31+\binom32=7$.
- **Ghi chú diễn giả:** Các phần tử của $Y_1$ là $00$, mở rộng thành $000$ và $001$; $01$, thành $010$ và $011$; $11$, thành $110$ và $111$. Cách $10$ chỉ mở rộng thành $100$, vì $101$ không thực hiện được. $Y_1$ tách trọn vẹn vị trí $1$ (giá trị $0$, $0$, $1$) và vị trí $2$, nhưng không tách trọn vẹn cặp vị trí $\{1,2\}$. Cả hai cận của bước quy nạp đạt dấu bằng, nên bổ đề đạt dấu bằng tại $m=3$, khớp $\Pi_{\mathcal H_{\mathrm{int}}}(3)=7$. Với lớp hàm ngưỡng trên cùng ba điểm: $\mathcal H_C=\{000,001,011,111\}$, $\mathcal H_{C'}=\{00,01,11\}$, $Y_1=\{00\}$, và $4=3+1$, với $Y_1$ có chiều VC $0=d-1$. Nguồn: ghi chú Bài 03, chứng minh Bổ đề 03.12, Bước 1–2; Mệnh đề 03.6; Ví dụ 03.4.
- **Lý do / nối:** kiểm tra từng bước của lộ trình trên số cụ thể → phần (b).
- **Mục tiêu / nguồn:** 2; chứng minh Bổ đề 03.12(a).

#### `4-05` Ý tưởng chứng minh: dạng đóng của bổ đề Sauer–Shelah — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** Với $1\le d\le m$: display $\sum_{j\le d}\binom mj\le\sum_{j\le d}\binom mj(\tfrac md)^{d-j}\le(\tfrac md)^d(1+\tfrac dm)^m\le(\tfrac md)^de^d$.
  1. $(m/d)^{d-j}\ge1$ khi $j\le d$, vì $m/d\ge1$.
  2. Thêm các số hạng $d<j\le m$, rồi khai triển nhị thức; bước này cần $d\le m$.
  3. $1+x\le e^x$ với $x=d/m$, nâng lên lũy thừa $m$.
  - Bỏ $d\le m$: $m=1$, $d=3$ cho $(e/3)^3\approx0{,}744<2=\Pi_{\mathcal H}(1)$.
  - {{một công thức hiển thị; đo ở 390 px, ngắt bằng aligned chỉ khi tràn}}
- **Ghi chú diễn giả** (~130 âm tiết): Lộ trình: nhân mỗi số hạng với một thừa số không nhỏ hơn $1$, thêm số hạng để được một khai triển nhị thức đầy đủ, rồi chặn bằng hàm mũ. Bất đẳng thức thứ hai trên mặt trang gộp hai bước của ghi chú: rút $(m/d)^d$ ra ngoài được $\sum_{j\le d}\binom mj(d/m)^j$, rồi thêm các số hạng không âm với $d<j\le m$ được $(1+d/m)^m$. Khi $m<d$, tổng trong (a) bằng $2^m=\Pi_{\mathcal H}(m)$, và dạng đóng có thể nhỏ hơn: với $m=1$, $d=3$, $(e/3)^3\approx0{,}744<2$. Hệ quả: $\ln\Pi_{\mathcal H}(m)\le d\ln(em/d)$ tăng như $\ln m$, còn $\ln2^m$ tăng tuyến tính. Nguồn: ghi chú Bài 03, chứng minh Bổ đề 03.12, Bước 3 và hai đoạn sau.
- **Lý do / nối:** kết quả thứ hai của bổ đề, chỗ dùng $d\le m$ và phản ví dụ → so sánh ba cách đếm.
- **Mục tiêu / nguồn:** 2; chứng minh Bổ đề 03.12(b).

#### `4-06` Ví dụ: ba cách đếm cách gán nhãn — ví dụ (Ví dụ 03.5), cận bằng số · 3 phút
- **Mặt trang:**
  - Lớp $\mathcal H_{\mathrm{thr}}$ ($d=1$), $\mathcal H_{\mathrm{int}}$ ($d=2$), $\mathcal H^2_{\mathrm{aff}}$ ($d=3$).
  - $d=1$, $d=2$: tổng nhị thức bằng $m+1$ và $\binom{m+1}2+1$; Bổ đề 03.12(a) đạt dấu bằng.
  - $\mathcal H^2_{\mathrm{aff}}$, $m=4$: phân hoạch Radon loại hai cách gán nhãn, $\Pi=14<15$.
  - bảng `m | tổng (d = 3) | (em/3)^3 | 2^m`, các hàng $m=3,4,5,20$: $8;\ 20{,}09;\ 8$ / $15;\ 47{,}61;\ 16$ / $26;\ 92{,}99;\ 32$ / $1351;\ 5951{,}27;\ 1\,048\,576$.
  - **Diễn giải:** ba hàng đầu, dạng đóng còn lớn hơn $2^m$; tại $m=20$, tổng nhị thức nhỏ hơn gần ba bậc.
- **Ghi chú diễn giả:** Bốn điểm có điểm lặp cho nhiều nhất $2^3=8$ cách; bốn điểm phân biệt có một phân hoạch Radon, và cả cách gán nhãn "$1$ trên $I$, $0$ trên $J$" lẫn cách bù đều không thực hiện được, nên $\Pi(4)\le14$, và hình vuông đạt $14$. Tổng nhị thức với $d=3$ cho phép $15$, nên với lớp nửa mặt phẳng bổ đề không đạt dấu bằng. Dạng đóng lỏng hơn tổng nhị thức khi $m$ nhỏ, nhưng cho $\ln\Pi_{\mathcal H}(m)\le d\ln(em/d)$, tăng theo $m$ chậm hơn $m\ln2$. Nguồn: ghi chú Bài 03, Ví dụ 03.5.
- **Lý do / nối:** số liệu cho cả hai phần của bổ đề trên ba lớp xuyên suốt → tiêu đề mạch 5.
- **Mục tiêu / nguồn:** 2; Ví dụ 03.5.

### Mạch 5. Hội tụ đều trên lớp có chiều VC hữu hạn (10 trang, 27 phút)

#### `5-00` 5. Hội tụ đều trên lớp có chiều VC hữu hạn — tiêu đề mạch, điểm vào mạch 5 · 0,5 phút
- **Mặt trang:** "5."; h2 "Hội tụ đều trên lớp có chiều VC hữu hạn"; `p.strand-lead` (bảng mạch, 24 âm tiết); `p.strand-keys`: "hội tụ đều · tập mẫu ảo · đổi chỗ · tập gộp · bán kính VC".
- **Ghi chú diễn giả:** Kế thừa: trên $m$ điểm, lớp có chiều VC $d$ cho nhiều nhất $(em/d)^d$ cách gán nhãn. Nhiệm vụ: dùng số đếm này thay cho số giả thuyết trong chứng minh hội tụ đều của Bài 02. Hai trở ngại phải vượt qua: rủi ro kì vọng không xác định bởi cách gán nhãn trên tập huấn luyện, và tập các cách gán nhãn phụ thuộc tập huấn luyện. Đầu ra: bán kính VC, cận độ lệch đều có cỡ $\sqrt{d\ln m/m}$, và các giả thiết không bỏ được. Nguồn: ghi chú Bài 03, §7.
- **Lý do / nối:** mạch 4 → định nghĩa tính chất hội tụ đều.
- **Mục tiêu / nguồn:** 3, 4; §7.

#### `5-01` Tính chất hội tụ đều của một lớp — định nghĩa · 2,5 phút
- **Mặt trang:**
  - **Nhắc lại:** $S$ là $\epsilon$-đại diện khi $\sup_h\lvert L_S(h)-L_D(h)\rvert\le\epsilon$ (Định nghĩa 02.13).
  - **Định nghĩa 03.13.** $\mathcal H$ có tính chất hội tụ đều (uniform convergence property) nếu có $M:(0,1)^2\to\mathbb N$ sao cho display $\Pr_{S\sim D^m}\big[\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\le\epsilon\big]\ge1-\delta$
  - với mọi $\epsilon,\delta\in(0,1)$, mọi phân bố $D$, mọi $m\ge M(\epsilon,\delta)$; biến cố trong ngoặc đo được.
  - $m^{UC}_{\mathcal H}(\epsilon,\delta)$: $m_0$ nhỏ nhất như vậy, hàm cỡ mẫu hội tụ đều (uniform convergence sample size).
  - Lượng từ: $\exists M$ trước $\forall D$; lớp hữu hạn: $m^{UC}_{\mathcal H}\le\lceil\ln(2K/\delta)/(2\epsilon^2)\rceil$ (Định lý 02.14(c)).
  - {{một công thức hiển thị}}
- **Ghi chú diễn giả:** Thứ tự lượng từ giống định nghĩa học PAC (Định nghĩa 01.18): hàm $M$ được chọn trước khi biết phân bố, nên cỡ mẫu không phụ thuộc $D$. Đây là tính chất của lớp, không có thuật toán nào trong định nghĩa. Chính xác hơn, $m^{UC}_{\mathcal H}(\epsilon,\delta)$ là số $m_0$ nhỏ nhất sao cho điều kiện đúng với mọi $D$ và mọi $m\ge m_0$, và bằng $\infty$ khi không có $m_0$ nào. Một lớp hữu hạn chọn trước khi lấy mẫu có tính chất này theo Định lý 02.14(c). Nguồn: ghi chú Bài 03, §7, Định nghĩa 03.13 và hai đoạn sau.
- **Lý do / nối:** đích của mạch được định nghĩa trước → một lớp không có tính chất này.
- **Mục tiêu / nguồn:** 3, 5; Định nghĩa 03.13.

#### `5-02` Ví dụ: lớp mọi hàm phân lớp đo được trên [0,1] — ví dụ (Ví dụ 03.6), phản ví dụ · 2 phút
- **Mặt trang:**
  - $\mathcal X=[0,1]$; $\mathcal M_{[0,1]}$: mọi hàm phân lớp đo được $[0,1]\to\{0,1\}$ (Ví dụ 01.8).
  - $D$: $X\sim U[0,1]$, $D(Y=1\mid X=x)=1$ với mọi $x$.
  - Chiều VC: với mọi tập hữu hạn $C$ và tập $F_1\subseteq C$ các điểm nhãn $1$, $\mathbb 1_{F_1}$ thực hiện cách gán nhãn; $d=\infty$.
  - Đặt $F=\{X_1,\ldots,X_m\}$: $L_S(\mathbb 1_F)=0$, $L_D(\mathbb 1_F)=1$ (Mệnh đề 01.15); độ lệch đều bằng $1$ trên mọi tập huấn luyện.
  - Với $\epsilon<1$, biến cố $\epsilon$-đại diện có xác suất $0<1-\delta$ với mọi $m$: không có tính chất hội tụ đều.
- **Ghi chú diễn giả:** Hàm $\mathbb 1_{F_1}$ là hàm Borel vì $F_1$ hữu hạn, nên thuộc lớp. Hàm $\mathbb 1_F$ là hàm phân lớp ghi nhớ của Bài 01: nó khớp mọi quan sát của tập huấn luyện, nhưng một quan sát mới rơi vào $F$ với xác suất $0$. Tập các tập đại diện là tập rỗng, đo được, xác suất $0$, nên không hàm $M$ nào thỏa định nghĩa. Lớp vẫn có nghiệm ERM tốt dưới phân bố này: hàm hằng $1$ có rủi ro thực nghiệm và rủi ro kì vọng bằng $0$ (Mệnh đề 01.15(c)); hội tụ đều hỏng vì nó đòi cận cho mọi hàm của lớp cùng lúc. Nguồn: ghi chú Bài 03, Ví dụ 03.6; Ví dụ 01.8, Mệnh đề 01.15.
- **Lý do / nối:** phản ví dụ với chiều VC vô hạn, trước định lý → vì sao không cộng ngay trên các cách gán nhãn.
- **Mục tiêu / nguồn:** 5; Ví dụ 03.6.

#### `5-03` Bất đẳng thức hợp trên các cách gán nhãn của tập huấn luyện — vấn đề, câu hỏi · 3 phút
- **Mặt trang:**
  - Trên $S$, lớp chỉ cho $\lvert\mathcal H_{(X_1,\ldots,X_m)}\rvert\le\Pi_{\mathcal H}(m)$ cách gán nhãn.
  - **Câu hỏi:** có thể lấy bất đẳng thức hợp trên các cách gán nhãn này không?
  - `[f]` (i) $L_D(h)$ không xác định bởi cách gán nhãn của $h$ trên $S$.
  - `[f]` (ii) Tập các cách gán nhãn phụ thuộc $S$: một lớp chọn theo tập huấn luyện, trái (T5).
  - `[f]` Cách sửa: thay $L_D(h)$ bằng $L_{S'}(h)$, với $S'\sim D^m$ độc lập với $S$.
- **Ghi chú diễn giả:** Ở (i), hai hàm có cùng cách gán nhãn trên $S$ có thể có rủi ro kì vọng khác nhau, nên một cách gán nhãn không ứng với một biến cố hỏng duy nhất. Lập luận bỏ qua hai trở ngại cho kết quả sai: với lớp $\mathcal M_{[0,1]}$ và phân bố của ví dụ trước, $\Pi(m)=2^m$, và cận "$\sqrt{\ln(2\Pi(m)/\delta)/(2m)}$" bằng khoảng $0{,}590$ tại $m=1000$, $\delta=0{,}05$, trong khi độ lệch đều bằng $1$ trên mọi tập huấn luyện (Bài tập 03.4(d)). Sau khi thay $L_D(h)$ bằng $L_{S'}(h)$, mọi đại lượng chỉ phụ thuộc $h$ qua cách gán nhãn trên $2m$ điểm; phép thay cần lớp cố định đối với cả hai tập, tức (T5). Độ lệch đều là cận trên đúng của vô hạn biến ngẫu nhiên; dưới (M), nó bằng cận trên đúng trên lớp con đếm được $\mathcal H_0$, nên đo được. Các lớp của bài thỏa (M) với tham số hữu tỉ; với lớp hàm ngưỡng, dãy $t_k\uparrow t$ dùng được, dãy $t_k\downarrow t$ thì không, vì nó hội tụ về $\mathbb 1[x>t]$ (Nhận xét 03.14). Nguồn: ghi chú Bài 03, §7, đoạn trước Định lý 03.15, Nhận xét 03.14; tệp bài tập, Bài tập 03.4(d).
- **Lý do / nối:** trọng tâm trực quan: số cách gán nhãn thay cho $K$ chỉ sau một bước sửa → phát biểu định lý.
- **Mục tiêu / nguồn:** 3; §7 (Câu hỏi và hai trở ngại).

#### `5-04` Hội tụ đều trên lớp có chiều VC hữu hạn — trực quan, kết quả · 3,5 phút
- **Mặt trang:**
  - **Trực quan.** Thay $\ln K$ bằng $\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$: độ lệch đều có cỡ $\sqrt{d\ln m/m}$.
  - **Định lý 03.15.** **Giả thiết:** (T1), $m\ge1$; hàm lỗi 0–1; $\mathcal H$ thỏa (T5), (M), chiều VC $d$; $\delta\in(0,1)$.
  - **Bảo đảm** (xác suất theo $S\sim D^m$, mọi $D$), với bán kính VC (VC radius) display $\rho_m=\sqrt{8\ln(4\Pi_{\mathcal H}(2m)/\delta)/m}$:
  - (a) với xác suất ít nhất $1-\delta$, $\sup_h\lvert L_S(h)-L_D(h)\rvert\le\rho_m$;
  - (b) nếu $1\le d\le m$: display $\rho_m\le\sqrt{\tfrac8m(d\ln\tfrac{2em}d+\ln\tfrac4\delta)}\le4\sqrt{\tfrac1m(d\ln\tfrac{em}d+\ln\tfrac2\delta)}$;
  - (c) nếu $1\le d<\infty$: hội tụ đều, $m^{UC}_{\mathcal H}(\epsilon,\delta)\le\big\lceil\tfrac{16}{\epsilon^2}(d\ln\tfrac{32}{\epsilon^2}+\ln\tfrac4\delta)\big\rceil$.
  - {{hai công thức hiển thị; đo ở 390 px}}
- **Ghi chú diễn giả:** Bảo đảm với xác suất cao cho độ lệch giữa đại lượng thực nghiệm và đại lượng tổng thể, đồng thời cho mọi $h\in\mathcal H$, không phụ thuộc $D$. Khi $d\ge1$, cận giảm theo $m$ như $\sqrt{\ln m/m}$ và phụ thuộc $\delta$ qua $\ln(1/\delta)$. Bán kính $\rho_m=\rho_m(\mathcal H,\delta)$; vì độ lệch đều không vượt quá $1$, các vế phải ở (a), (b) có thể thay bằng $\min\{1,\cdot\}$. Hai trường hợp biên: khi $d=\infty$, $\Pi_{\mathcal H}(2m)=2^{2m}$ nên $\rho_m\ge\sqrt{16\ln2}\approx3{,}33$, và (a) đúng nhưng không cho thông tin; khi $d=0$, mọi hàm của lớp trùng nhau, $\Pi_{\mathcal H}=1$, và (a) cho $\sqrt{8\ln(4/\delta)/m}$. So với Định lý 02.14, $\ln(2K/\delta)/(2m)$ thành $8\ln(4\Pi_{\mathcal H}(2m)/\delta)/m$. Nguồn: ghi chú Bài 03, §6 (câu cuối), §7, Định lý 03.15 và đoạn sau.
- **Lý do / nối:** kết quả chính của bài → lộ trình chứng minh.
- **Mục tiêu / nguồn:** 3, 4; Định lý 03.15.

#### `5-05` Ý tưởng chứng minh: hội tụ đều theo chiều VC — ý tưởng chứng minh · 4,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** Với $m\epsilon^2\ge2$: display $\Pr[\sup_h\lvert L_D-L_S\rvert>\epsilon]\le2\Pr[\sup_h\lvert L_{S'}-L_S\rvert>\tfrac\epsilon2]\le4\Pi_{\mathcal H}(2m)e^{-m\epsilon^2/8}$.
  1. Tập mẫu ảo (ghost sample) $S'\sim D^m$ độc lập; Chebyshev, $\operatorname{Var}\le\tfrac14$: hệ số $2$ [(T1), bị chặn, (M)].
  2. Đổi chỗ (swapping) $Z_i\leftrightarrow Z'_i$, dấu ngẫu nhiên (random signs) $\sigma_i$ [(T1)].
  3. Biết $(S,S')$: nhiều nhất $\Pi_{\mathcal H}(2m)$ cách gán nhãn trên tập gộp (combined sample) [(T5)].
  4. Hoeffding, miền dài $2$: $2e^{-m\epsilon^2/8}$ mỗi cách; bất đẳng thức hợp trên các cách.
  5. Giải theo $\delta$: $\epsilon=\rho_m$; (b) từ Bổ đề 03.12 tại $2m$ điểm.
  - {{một công thức hiển thị, aligned ba dòng nếu tràn ở 390 px}}
- **Ghi chú diễn giả** (~250 âm tiết): Lộ trình: thay rủi ro kì vọng bằng rủi ro trên tập mẫu ảo, đối xứng hóa bằng dấu ngẫu nhiên, đếm cách gán nhãn trên tập gộp, rồi Hoeffding và bất đẳng thức hợp. Bước 1: nếu một $h$ chọn theo $S$ có $\lvert L_S(h)-L_D(h)\rvert>\epsilon$, thì khi biết $S$, bất đẳng thức Chebyshev cho $L_{S'}(h)$ nằm trong khoảng $\epsilon/2$ quanh $L_D(h)$ với xác suất ít nhất $1-1/(m\epsilon^2)\ge\tfrac12$, và khi đó $\lvert L_{S'}(h)-L_S(h)\rvert>\epsilon/2$; đây là hệ số $2$. (M) cho phép chọn $h$ đo được theo $S$. Bước 2: các cặp $(Z_i,Z'_i)$ độc lập cùng phân bố, nên đổi chỗ trong từng cặp không đổi phân bố. Bước 3 là chỗ (T5) vào: lớp không đổi theo $(S,S')$, và nguồn ngẫu nhiên còn lại là $\sigma$, độc lập với các cách gán nhãn, khác với trở ngại (ii). Bước 4: các số hạng $\sigma_i(\cdot)$ độc lập, kì vọng $0$, trong $[-1,1]$, nên Định lý 02.7 cho $2e^{-m\epsilon^2/8}$, như câu ôn nhanh 3 với $\epsilon/2$. Bước 5: điều kiện $m\epsilon^2\ge2$ tự thỏa tại $\epsilon=\rho_m$, vì $m\rho_m^2\ge8\ln4\approx11{,}09$; phần (c) dùng bất đẳng thức tiếp tuyến $\ln u\le u/u_0+\ln u_0-1$. Khi quan sát không độc lập, Bước 1 và Bước 2 hỏng. Nguồn: ghi chú Bài 03, chứng minh Định lý 03.15 (lộ trình) và đoạn sau Ví dụ 03.8; Phụ lục C; UML §6.5.2.
- **Lý do / nối:** lộ trình năm bước, chỗ từng giả thiết vào → tách hai kỹ thuật dùng lại.
- **Mục tiêu / nguồn:** 3; chứng minh Định lý 03.15, Phụ lục C.

#### `5-06` Đối xứng hóa và tập mẫu ảo — kỹ thuật (lần đầu trong học phần) · 3 phút
- **Mặt trang:**
  - **Kỹ thuật.** Thay $L_D(h)$ bằng $L_{S'}(h)$ trên tập mẫu ảo $S'\sim D^m$ độc lập với $S$.
  - Đổi chỗ $Z_i\leftrightarrow Z'_i$ không đổi phân bố của $(S,S')$, nên họ $(L_{S'}(h)-L_S(h))_{h\in\mathcal H}$ có cùng phân bố liên hợp với họ display $\big(\tfrac1m\sum_i\sigma_i(\ell(h,Z'_i)-\ell(h,Z_i))\big)_{h\in\mathcal H}$.
  - Giá: độ lệch chia đôi và miền dài $2$ cho hằng số $8$ trong $\rho_m$.
  - Dùng khi: chặn một cận trên đúng trên lớp vô hạn, nơi $L_D$ chưa biết. Dùng ở: Định lý 03.15.
  - {{hình F6 bên phải, grid2; một công thức hiển thị}}
- **Ghi chú diễn giả:** Tên chung của bước 1–2 là đối xứng hóa (symmetrization). Tập mẫu ảo chỉ dùng trong chứng minh; thuật toán không thấy nó. Đọc hình: hai hàng bốn ô, hàng trên $Z_1,\ldots,Z_4$, hàng dưới $Z'_1,\ldots,Z'_4$; với $\sigma=(+1,-1,+1,-1)$, mũi tên đổi chỗ ở cột $2$ và $4$, và sau khi đổi, hàng trên là $Z_1,Z'_2,Z_3,Z'_4$. Phép đổi này biến mỗi hiệu $\ell(h,Z'_i)-\ell(h,Z_i)$ thành $\sigma_i$ lần hiệu đó, đồng thời cho mọi $h$. Hằng số: số mũ $-2mr^2$ của Định lý 02.14 thành $-2m(\epsilon/2)^2/2^2=-m\epsilon^2/8$; tỉ số $16$ giữa hai hằng số được kiểm ở Bài tập 03.4(c). Nguồn: ghi chú Bài 03, chứng minh Định lý 03.15, Bước 1–2, câu cuối; Phụ lục C.2–C.3; tệp bài tập, Bài tập 03.4(c).
- **Lý do / nối:** kỹ thuật dùng lại qua học phần, trang riêng ngay sau nơi dùng lần đầu → kỹ thuật thứ hai.
- **Mục tiêu / nguồn:** 3; chứng minh Định lý 03.15.

#### `5-07` Hàm tăng trưởng thay cho số giả thuyết — kỹ thuật (lần đầu trong học phần) · 2,5 phút
- **Mặt trang:**
  - **Kỹ thuật.** Khi biết tập gộp, mọi đại lượng chỉ phụ thuộc $h$ qua cách gán nhãn trên $2m$ điểm.
  - Bất đẳng thức hợp lấy trên nhiều nhất $\Pi_{\mathcal H}(2m)$ cách gán nhãn, thay cho $K$: display $\ln(4\Pi_{\mathcal H}(2m)/\delta)\le d\ln(2em/d)+\ln(4/\delta)$ thay cho $\ln(2K/\delta)$.
  - Cần (T5): lớp cố định với cả hai tập.
  - Dùng khi: lớp vô hạn, hàm tăng trưởng đa thức. Dùng ở: Định lý 03.15.
  - {{một công thức hiển thị}}
- **Ghi chú diễn giả:** Khi đó nguồn ngẫu nhiên còn lại là $\sigma$, độc lập với các cách gán nhãn. Kỹ thuật ghép ba công cụ: bất đẳng thức hợp của Bài 01, cận Hoeffding cho một cách gán nhãn cố định, và bổ đề Sauer–Shelah. Nó là trọng tâm trực quan của bài: số "hành vi" của lớp trên các điểm của tập huấn luyện, không phải số phần tử của lớp, quyết định số biến cố hỏng phải cộng. Bất đẳng thức hợp lấy theo điều kiện trên tập gộp, rồi lấy kì vọng theo $(S,S')$; cận đúng với mọi giá trị của tập gộp. Với lớp hữu hạn, cả hai cách đều dùng được, và $\Pi_{\mathcal H}(2m)\le K$. Nguồn: ghi chú Bài 03, chứng minh Định lý 03.15, Bước 3–5; Phụ lục C.4, C.6; §9.
- **Lý do / nối:** kỹ thuật dùng lại qua học phần → số liệu trên hai lớp tuyến tính.
- **Mục tiêu / nguồn:** 3; chứng minh Định lý 03.15.

#### `5-08` Ví dụ: cận độ lệch đều cho d = 3 và d = 11 — ví dụ (Ví dụ 03.7), cận bằng số · 2,5 phút
- **Mặt trang:**
  - $\mathcal H^2_{\mathrm{aff}}$ ($d=3$), $\mathcal H^{10}_{\mathrm{aff}}$ ($d=11$), thỏa (M); $\delta=0{,}05$, $\ln(4/\delta)\approx4{,}382$.
  - Dạng trực tiếp $\sqrt{\tfrac8m(d\ln\tfrac{2em}d+\ln\tfrac4\delta)}$ tại $d=3$, $m=10^4$: $\sqrt{8(3\ln18\,122+4{,}382)/10^4}\approx\sqrt{0{,}02704}\approx0{,}164$.
  - $m=10^3;\ 10^4;\ 10^5$: $0{,}464;\ 0{,}164;\ 0{,}0571$ ($d=3$) và $0{,}762;\ 0{,}280;\ 0{,}0993$ ($d=11$).
  - Nhân $m$ lên $10$ lần: cận giảm ít hơn $\sqrt{10}$ lần, vì $\ln m$ tăng.
  - **Diễn giải:** $d=11$: với xác suất ít nhất $0{,}95$, độ lệch đều $\le0{,}762$ ở $10^3$ quan sát, $\le0{,}280$ ở $10^4$.
  - {{hình F5 bên phải, grid2}}
- **Ghi chú diễn giả:** Cả hai lớp thỏa (M) với tham số hữu tỉ. Dạng hằng số $4$ cho $0{,}621;\ 0{,}223;\ 0{,}0779$ ($d=3$) và $1{,}014;\ 0{,}379;\ 0{,}136$ ($d=11$), lớn hơn dạng trực tiếp từ $1{,}33$ đến $1{,}37$ lần; ô $1{,}014$ lớn hơn $1$, nên sau khi cắt ở $1$ nó không cho thông tin. Nhân $m$ lên $10$ lần làm cận giảm từ $2{,}7$ đến $2{,}9$ lần, so với $\sqrt{10}\approx3{,}16$. Đọc hình: trục ngang $m$ thang lôgarit từ $10^3$ đến $10^5$, trục dọc từ $0$ đến $0{,}8$; hai đường dạng trực tiếp cho $d=3$ (chấm tròn, nét liền) và $d=11$ (tam giác, nét đứt) tại bảy cỡ mẫu. Nguồn: ghi chú Bài 03, Ví dụ 03.7.
- **Lý do / nối:** con số cụ thể cho cận của định lý trên lớp của ứng dụng → bỏ (T5).
- **Mục tiêu / nguồn:** 4; Ví dụ 03.7.

#### `5-09` Ví dụ: hai hàm chọn sau khi xem tập huấn luyện — ví dụ (Ví dụ 03.8), kiểm tra bỏ giả thiết · 3 phút
- **Mặt trang:**
  - $D$: $X\sim U[0,1]$, $D(Y=1\mid X=x)=1$; hàm lỗi 0–1; $F=\{X_1,\ldots,X_m\}$.
  - $\mathcal G_S=\{h_{\equiv0},\mathbb 1_F\}$: hàm hằng $0$ và hàm chỉ báo của $F$, chọn sau khi xem tập huấn luyện.
  - Chiều VC bằng $1$: hai hàm, khác nhau tại $X_1$.
  - $L_S(\mathbb 1_F)=0$, $L_D(\mathbb 1_F)=1$: độ lệch đều bằng $1$ với xác suất $1$.
  - Định lý 03.15(b) áp dụng sai, $d=1$, $m=1000$, $\delta=0{,}05$: $\rho_m\le\sqrt{0{,}008\,(8{,}601+4{,}382)}\approx0{,}322<1$.
  - **Kết luận:** Bước 3 của chứng minh cần lớp cố định; đổi chỗ $Z_i\leftrightarrow Z'_i$ làm đổi cả lớp.
- **Ghi chú diễn giả:** Hai hàm cho nhiều nhất hai cách gán nhãn, nên chiều VC không quá $\log_22=1$; chúng khác nhau tại $X_1$, nên $\{X_1\}$ bị tách trọn vẹn. Số $8{,}601$ là $\ln(2e\cdot1000)$, số $4{,}382$ là $\ln80$. Chiều VC nhỏ không đủ: lớp phải cố định trước khi lấy mẫu. Bài tập 03.5(c) cho một phiên bản với nhãn ngẫu nhiên, lớp một hàm, chiều VC $0$ và độ lệch $\tfrac12$, so với bán kính $0{,}187$. Hai giả thiết khác cũng không bỏ được: khi một quan sát được chép lại $m$ lần như Ví dụ 02.6, Bước 1 và Bước 2 của chứng minh hỏng. Nguồn: ghi chú Bài 03, Ví dụ 03.8 và đoạn sau; tệp bài tập, Bài tập 03.5(c).
- **Lý do / nối:** phản ví dụ bỏ (T5) với số cụ thể → tiêu đề mạch 6.
- **Mục tiêu / nguồn:** 5; Ví dụ 03.8.

### Mạch 6. Rủi ro vượt mức của ERM và định lý cơ bản (9 trang, 20 phút)

#### `6-00` 6. Rủi ro vượt mức của ERM và định lý cơ bản — tiêu đề mạch, điểm vào mạch 6 · 0,5 phút
- **Mặt trang:** "6."; h2 "Rủi ro vượt mức của ERM và định lý cơ bản"; `p.strand-lead` (bảng mạch, 23 âm tiết); `p.strand-keys`: "bước tất định · rời rạc hóa · định lý cơ bản · cận dưới".
- **Ghi chú diễn giả:** Kế thừa: cận độ lệch đều $\rho_m$ trên lớp có chiều VC hữu hạn. Nhiệm vụ: chuyển cận này thành bảo đảm cho mọi nghiệm ERM, tính cỡ mẫu cho hai câu hỏi mở đầu, rồi hỏi chiều VC hữu hạn có cần không. Đầu ra: cỡ mẫu đủ theo chiều VC, định lý cơ bản cho phân lớp nhị phân, và cận dưới cho thấy tốc độ $1/\epsilon^2$ không bỏ được. Nguồn: ghi chú Bài 03, §8, §9.
- **Lý do / nối:** mạch 5 → hệ quả cho ERM.
- **Mục tiêu / nguồn:** 4, 5; §8.

#### `6-01` Rủi ro vượt mức của ERM trên lớp có chiều VC hữu hạn — trực quan, kết quả · 3 phút
- **Mặt trang:**
  - **Trực quan.** Hệ số $2$: so sánh $L_D$ với $L_S$ tại $\hat h$ và tại mỗi $h$.
  - **Hệ quả 03.16.** **Giả thiết:** (T1), hàm lỗi 0–1; $\mathcal H$ thỏa (T5), (M), $1\le d<\infty$; $\delta\in(0,1)$.
  - ERM chính xác (O1), mọi quy tắc chọn khi bằng nhau, hoặc $\epsilon_{\mathrm{opt}}$-ERM $A$ (O2).
  - **Bảo đảm** (mọi $D$): (a) với xác suất $\ge1-\delta$, đồng thời mọi nghiệm ERM: display $L_D(\hat h)\le\inf_{h\in\mathcal H}L_D(h)+2\rho_m$; (b) (O2): thêm $\epsilon_{\mathrm{opt}}$.
  - (c) ERM như trên học PAC bất khả diễn, với display $M(\epsilon,\delta)=\big\lceil\tfrac{64}{\epsilon^2}(d\ln\tfrac{128}{\epsilon^2}+\ln\tfrac4\delta)\big\rceil$.
  - {{hai công thức hiển thị}}
- **Ghi chú diễn giả:** (O1) là nghiệm ERM chính xác, $\hat h\in\arg\min_hL_S(h)$; (O2) là $L_S(A(S))\le\inf_hL_S(h)+\epsilon_{\mathrm{opt}}$. Thuật toán ERM phải thỏa điều kiện đo được của Định nghĩa 01.4; với hàm lỗi 0–1, nghiệm ERM tồn tại trên mọi tập huấn luyện, kể cả với lớp vô hạn (Nhận xét 01.11). Đây là bảo đảm với xác suất cao cho rủi ro vượt mức so với lớp, không phụ thuộc $D$. Khi $d\le m$, có thể thay $\rho_m$ bằng một trong hai vế phải của Định lý 03.15(b). Trong (c), $\epsilon$ là cận cho rủi ro vượt mức; độ lệch đều tương ứng là $\epsilon/2$. Nếu có ít nhất một thuật toán ERM như vậy, $\mathcal H$ học được PAC bất khả diễn và $m_{\mathcal H}(\epsilon,\delta)\le M(\epsilon,\delta)$. Nguồn: ghi chú Bài 03, §8, Hệ quả 03.16 và đoạn sau.
- **Lý do / nối:** kết quả chính cho thuật toán → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 4; Hệ quả 03.16.

#### `6-02` Ý tưởng chứng minh: rủi ro vượt mức của ERM — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  - **Nhắc lại:** bước tất định trên biến cố đại diện (Hệ quả 02.16).
  - **Ý tưởng chứng minh.**
  1. Trên biến cố "$S$ là $r$-đại diện", với mọi $h\in\mathcal H$: display $L_D(\hat h)\le L_S(\hat h)+r\le L_S(h)+r\le L_D(h)+2r$.
  2. Ba bất đẳng thức: đại diện tại $\hat h$; (O1); đại diện tại $h$. Vế trái không phụ thuộc $h$: lấy $\inf_h$.
  3. $r=\rho_m$ theo Định lý 03.15(a); với (O2), bất đẳng thức giữa thêm $\epsilon_{\mathrm{opt}}$.
  4. Phần (c): $2\rho_m\le\epsilon$ khi $\rho_m\le\epsilon/2$; Định lý 03.15(c) với $\epsilon/2$: $16/(\epsilon/2)^2=64/\epsilon^2$, $32/(\epsilon/2)^2=128/\epsilon^2$.
  - {{một công thức hiển thị; đo ở 390 px}}
- **Ghi chú diễn giả** (~150 âm tiết): Lộ trình: một bước tất định trên biến cố $r$-đại diện, rồi Định lý 03.15. Bước 1–2 không dùng xác suất và đúng cho mọi nghiệm ERM cùng lúc, với mọi quy tắc chọn khi bằng nhau; xác suất chỉ vào ở bước 3, qua một biến cố không phụ thuộc thuật toán. So với Hệ quả 02.16, phần tử tốt nhất $h_{\mathcal H}$ có thể không tồn tại trên lớp vô hạn, nên chuỗi được viết cho mọi $h$ rồi lấy cận dưới đúng; hằng số không đổi. Hệ số $2$ đến từ hai phép so sánh, tại $\hat h$ và tại $h$. Với (O2), bất đẳng thức giữa thành $L_S(A(S))\le L_S(h)+\epsilon_{\mathrm{opt}}$, vì $\inf_{h'}L_S(h')\le L_S(h)$. Ở bước 4, bước tất định với $r=\epsilon/2$ cho đúng bất đẳng thức của định nghĩa học PAC bất khả diễn với mọi $D$ và mọi $m\ge M(\epsilon,\delta)$. Nguồn: ghi chú Bài 03, chứng minh Hệ quả 03.16.
- **Lý do / nối:** lộ trình và chỗ dùng (O1), (O2) → số liệu cho hai câu hỏi mở đầu.
- **Mục tiêu / nguồn:** 4; chứng minh Hệ quả 03.16.

#### `6-03` Ví dụ: cỡ mẫu cho rủi ro vượt mức 0,1 — ví dụ (Ví dụ 03.9), trả lời câu hỏi mở đầu · 3 phút
- **Mặt trang:**
  - $\epsilon=0{,}1$ cho rủi ro vượt mức, $\delta=0{,}05$; mọi thuật toán ERM, mọi phân bố.
  - $d=1$: lớp hàm ngưỡng; $d=3$: hai chỉ số đo; $d=11$: mười chỉ số đo.
  - Điều kiện của dạng trực tiếp, $m\ge d$: display $\tfrac{32}m\big(d\ln\tfrac{2em}d+4{,}382\big)\le0{,}01$; vế trái giảm theo $m$, chia đôi khoảng.
  - bảng `d | dạng trực tiếp | cỡ mẫu M(0,1; 0,05)`: $1$ | $54\,330$ | $88\,572$; $3$ | $132\,992$ | $209\,624$; $11$ | $447\,194$ | $693\,832$.
  - **Diễn giải:** $54\,330$ quan sát đủ cho lớp hàm ngưỡng, $447\,194$ cho mười chỉ số đo; tỉ số $447\,194/132\,992\approx3{,}36$, gần $11/3$.
  - {{một công thức hiển thị}}
- **Ghi chú diễn giả:** Điều kiện đến từ Hệ quả 03.16(a) với dạng trực tiếp của Định lý 03.15(b): $2\rho_m\le0{,}1$ tương đương $8(\cdots)/m\le0{,}0025$. Vế trái giảm theo $m\ge d$: đạo hàm của $(d\ln\tfrac{2em}d+c)/m$ bằng $(d-d\ln\tfrac{2em}d-c)/m^2<0$, vì $\ln\tfrac{2em}d\ge\ln(2e)>1$; nên cỡ mẫu nhỏ nhất thỏa điều kiện cũng đủ cho mọi cỡ mẫu lớn hơn. Kiểm một ô: với $d=1$, vế trái bằng khoảng $0{,}0099999$ tại $m=54\,330$ và $0{,}0100001$ tại $m=54\,329$. Dạng đóng lớn hơn từ $1{,}55$ đến $1{,}63$ lần; dạng hằng số $4$ cho $103\,939$, $261\,198$, $889\,572$. Mỗi con số là một cận trên của độ phức tạp mẫu của lớp tương ứng. Chuyển từ hai lên mười chỉ số đo nhân cỡ mẫu khoảng $3{,}36$ lần, gần tỉ số $11/3\approx3{,}67$ của hai chiều VC. Nguồn: ghi chú Bài 03, Ví dụ 03.9; §9.
- **Lý do / nối:** trả lời bằng số hai câu hỏi của trang mở đầu → so với lớp hữu hạn.
- **Mục tiêu / nguồn:** 4; Ví dụ 03.9.

#### `6-04` Ví dụ: so sánh với lớp hữu hạn sau khi rời rạc hóa — ví dụ (Ví dụ 03.10), so sánh · 2,5 phút
- **Mặt trang:**
  - Mỗi tham số thực lưu bằng $64$ bit: $q$ tham số cho lớp hữu hạn $K\le2^{64q}$; rời rạc hóa (discretization).
  - Hệ quả 02.16(c): $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$ với $\epsilon=0{,}1$, $\delta=0{,}05$.
  - $q=1$: $65\ln2+\ln20\approx48{,}05$, cỡ mẫu $9611$, so với $54\,330$ (tỉ số $5{,}65$).
  - $q=11$: $705\ln2+\ln20\approx491{,}66$, cỡ mẫu $98\,333$, so với $447\,194$ (tỉ số $4{,}55$).
  - Sáu hàm ngưỡng, $m=1000$: $\rho_m\le\sqrt{8\ln480/1000}\approx0{,}2222$; $r_m=\sqrt{\ln240/2000}\approx0{,}0523$.
  - **Diễn giải:** cận VC lớn hơn nhưng áp dụng cho chính lớp vô hạn, mọi cách lưu tham số.
- **Ghi chú diễn giả:** Lớp sáu hàm ngưỡng là hữu hạn ($K=6$) và có $\Pi_{\mathcal H}(2m)\le6$, nên cả hai bán kính áp dụng; nó tách riêng ảnh hưởng của hằng số. Bán kính VC lớn hơn $r_m$ khoảng $4{,}25$ lần, trong đó thừa số $\sqrt{16}=4$ đến từ hằng số $8$ của tập mẫu ảo trong $\rho_m$ và mẫu số $2m$ trong $r_m$. Cận VC không có sai số xấp xỉ do lưới. Với hai chỉ số đo, Bài tập 03.4(e) cho cỡ mẫu $27\,355$ của lớp rời rạc hóa ba tham số, và tách tỉ số $4{,}86$ thành thừa số $16$ của hằng số nhân với tỉ số $0{,}30$ của hai số hạng lôgarit. Nguồn: ghi chú Bài 03, Ví dụ 03.10; §9; tệp bài tập, Bài tập 03.4(e).
- **Lý do / nối:** so sánh trung thực với cận của Bài 02 (mục tiêu 4) → chiều VC hữu hạn có cần không.
- **Mục tiêu / nguồn:** 4; Ví dụ 03.10.

#### `6-05` Định lý cơ bản: điều kiện cần — trực quan, kết quả · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Với một tập $2m$ điểm bị tách trọn vẹn, tập huấn luyện thấy nhiều nhất một nửa tập.
  - **Định lý 03.17.** **Giả thiết:** hàm lỗi 0–1, (T1); $\mathcal H$ khác rỗng; $A$ theo Định nghĩa 01.4.
  - **Bảo đảm** (a): nếu $\mathcal H$ tách trọn vẹn một tập $2m$ phần tử,
  - thì với mọi $A$ có $D$ khả diễn, tập trung trên tập đó: display $\Pr_{S\sim D^m}\big[L_D(A(S))>1/8\big]\ge1/7$.
  - **Kết luận:** $d=\infty$ kéo theo không học được PAC.
  - {{một công thức hiển thị}}
- **Ghi chú diễn giả:** Khi $d=\infty$, với mọi $m$ có một tập $2m$ điểm bị tách trọn vẹn, và tập huấn luyện thấy nhiều nhất một nửa tập đó. Phần (a) không dùng (M); chiều VC $d\in\{0,1,2,\ldots\}\cup\{\infty\}$. Với $d=\infty$, lấy $\epsilon<1/8$ và $\delta<1/7$: với mọi $m$, lớp tách trọn vẹn một tập $2m$ phần tử, nên mọi thuật toán thất bại với xác suất ít nhất $1/7>\delta$. Lượng từ của (a) là "với mọi thuật toán, tồn tại phân bố", như một cận dưới cần. Phân bố phụ thuộc thuật toán: trên nửa tập không thấy trong tập huấn luyện, nhãn có thể chọn ngược với dự đoán của thuật toán. Khi đó $\mathcal H$ cũng không học được PAC bất khả diễn, theo Nhận xét 01.26. Ở đây $\mathcal Y=\{0,1\}$ và $\mathcal X$ có một σ-đại số. Định lý được phát biểu ở mức phác thảo; điều kiện cần dựa trên định lý không có bữa trưa miễn phí (UML §5.1, §6.4). Nguồn: ghi chú Bài 03, §8, Định lý 03.17(a) và đoạn sau.
- **Lý do / nối:** chiều VC hữu hạn là điều kiện cần → sáu khẳng định tương đương.
- **Mục tiêu / nguồn:** 5; Định lý 03.17(a).

#### `6-06` Định lý cơ bản: sáu khẳng định tương đương — kết quả · 2 phút
- **Mặt trang:**
  - **Giả thiết:** như phần (a), thêm (M).
  - **Bảo đảm** (b): sáu khẳng định tương đương:
  - (1) $\mathcal H$ có tính chất hội tụ đều; (2) mọi ERM là thuật toán học PAC bất khả diễn;
  - (3) $\mathcal H$ học được PAC bất khả diễn; (4) $\mathcal H$ học được PAC;
  - (5) mọi ERM là thuật toán học PAC; (6) $d<\infty$.
  - Lượng từ: (a) "với mọi thuật toán, tồn tại phân bố"; (3), (4) "tồn tại thuật toán".
- **Ghi chú diễn giả:** Định lý 03.15 và Hệ quả 03.16 cho điều kiện đủ: dưới (M), chiều VC hữu hạn kéo theo học được. Phần (a) cho điều kiện cần, không dùng (M). Phần (b) gộp hai chiều: dưới (M), chiều VC hữu hạn tương đương với cả năm khái niệm học của Bài 01–03, trong trường hợp khả diễn cũng như bất khả diễn, với một thuật toán cũng như với mọi thuật toán ERM. Định lý chỉ cho phân lớp nhị phân với hàm lỗi 0–1. Nguồn: ghi chú Bài 03, §8, Định lý 03.17(b), đoạn trước định lý.
- **Lý do / nối:** phát biểu phần (b) tách khỏi phần (a) để giữ trần mật độ → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 5; Định lý 03.17(b).

#### `6-07` Ý tưởng chứng minh: định lý cơ bản — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  - **Ý tưởng chứng minh.** {{hình F7 bên phải, grid2}}
  - (6)⇒(1): Định lý 03.15(c) khi $d\ge1$; Định lý 03.15(a) với $\Pi_{\mathcal H}=1$ khi $d=0$.
  - (1)⇒(2): bước tất định với $r=\epsilon/2$, $M(\epsilon,\delta)=m^{UC}_{\mathcal H}(\epsilon/2,\delta)$.
  - (2)⇒(3), (5)⇒(4): theo định nghĩa; (2)⇒(5), (3)⇒(4): Nhận xét 01.26.
  - (4)⇒(6): phần (a), từ định lý không có bữa trưa miễn phí (no-free-lunch theorem; Nhận xét 01.30).
  - **Kết luận:** $\mathcal M_{[0,1]}$ tách trọn vẹn mọi tập hữu hạn, nên không học được PAC (Hệ quả 03.18).
- **Ghi chú diễn giả** (~170 âm tiết): Lộ trình: một vòng kéo theo qua sáu khẳng định. Hai phép kéo theo có nội dung là (6)⇒(1), từ Định lý 03.15, và (4)⇒(6), từ phần (a); các phép còn lại đến từ định nghĩa, từ bước tất định hoặc từ Nhận xét 01.26 (học PAC bất khả diễn kéo theo học PAC khi phân bố khả diễn). Phần (a) được thừa nhận: chứng minh dùng định lý không có bữa trưa miễn phí của UML §5.1 trên tập $2m$ điểm bị tách trọn vẹn, với cận $\mathbb E[L_D(A(S))]\ge1/4$, rồi đổi kì vọng thành xác suất; Bài tập 03.11 đi qua các bước đó. Hệ quả 03.18 chỉ kiểm giả thiết của phần (a) cho $\mathcal M_{[0,1]}$. So với Hệ quả 01.29(b), nơi một thuật toán ERM thất bại dưới một phân bố, ở đây mọi thuật toán đều thất bại dưới một phân bố chọn theo thuật toán; dưới phân bố cố định của Ví dụ 01.8, hàm hằng $1$ có rủi ro $0$. Đọc hình: sáu nút đánh số $(1)$ đến $(6)$, mũi tên có nhãn là kết quả dùng. Nguồn: ghi chú Bài 03, §8, danh sách phép kéo theo sau Định lý 03.17; Hệ quả 03.18 và chứng minh; tệp bài tập, Bài tập 03.11.
- **Lý do / nối:** lộ trình kéo theo và phần được thừa nhận → cận dưới.
- **Mục tiêu / nguồn:** 5; §8, Hệ quả 03.18.

#### `6-08` Cận dưới cho độ phức tạp mẫu — kết quả (đọc thêm), giới hạn · 1,5 phút
- **Mặt trang:**
  - **Định lý 03.19** (đọc thêm). **Giả thiết:** hàm lỗi 0–1, (T1); chiều VC $d$.
  - **Bảo đảm:** có hằng số phổ quát $c>0$, $\epsilon_0,\delta_0\in(0,1)$: với mọi $\epsilon<\epsilon_0$, $\delta<\delta_0$, mọi thuật toán $A$, mọi $m$:
  - (a) $1\le d<\infty$, $m<c(d+\ln\tfrac1\delta)/\epsilon^2$: có $D$ với $\Pr\big[L_D(A(S))>\inf_hL_D(h)+\epsilon\big]>\delta$.
  - (b) $2\le d<\infty$, $m<c(d+\ln\tfrac1\delta)/\epsilon$: có $D$ khả diễn với $\Pr\big[L_D(A(S))>\epsilon\big]>\delta$.
  - **Ý nghĩa:** tốc độ $1/\epsilon^2$ khi bất khả diễn là cần thiết; Hệ quả 03.16(c) dư một thừa số cỡ $\ln(1/\epsilon)$.
- **Ghi chú diễn giả:** Kết quả ở mức đọc thêm; chứng minh nằm ngoài phạm vi học phần (phần (a): UML §28.2). UML §6.4 phát biểu hai cận dưới với hằng số tuyệt đối. Bỏ thừa số $\ln(1/\epsilon)$ cần kỹ thuật xích (chaining), ngoài phạm vi học phần (UML §28.1). Giới hạn của các kết quả trong bài: chỉ phân lớp nhị phân với hàm lỗi 0–1, vì phép đếm cách gán nhãn cần nhãn dự đoán trong $\{0,1\}$; hàm lỗi bình phương và hàm lỗi log còn có thể không bị chặn (Nhận xét 02.11). Phân tích VC kiểm soát cả lớp và mọi phân bố, nên có thể lỏng cho một thuật toán hay một phân bố cụ thể. Ba giả thiết không bỏ được: (T5) (Ví dụ 03.8), (T1) (Ví dụ 02.6), chiều VC hữu hạn (Ví dụ 03.6). Nguồn: ghi chú Bài 03, Định lý 03.19 và đoạn sau; §9.
- **Lý do / nối:** cận dưới khớp tốc độ của cận trên; giới hạn của bài ở ghi chú diễn giả → tiêu đề mạch 7.
- **Mục tiêu / nguồn:** 4, 5; Định lý 03.19, §9.

### Mạch 7. Tổng kết (7 trang, 11,5 phút)

#### `7-00` 7. Tổng kết — tiêu đề mạch, điểm vào mạch 7 · 0,5 phút
- **Mặt trang:** "7."; h2 "Tổng kết"; `p.strand-lead` (bảng mạch, 22 âm tiết); không có dòng từ khóa.
- **Ghi chú diễn giả:** Kế thừa: bảy kết quả chính và ba kỹ thuật mới của bài. Nhiệm vụ: gom giả thiết của từng kết quả, trả lời vấn đề trung tâm cho cả bài, làm một bài tập tổng hợp, tự kiểm tra, giao bài tập. Không có khái niệm mới. Nguồn: ghi chú Bài 03, §9–§12.
- **Lý do / nối:** mạch 6 → bảng tổng kết.
- **Mục tiêu / nguồn:** tất cả; §9–§12.

#### `7-01` Bảng tổng kết — tổng kết · 2,5 phút
- **Mặt trangbảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh` (trần 80):**
  | Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh |
  |---|---|---|
  | $d=1$; $d=2$ (Mệnh đề 03.5, 03.6) | — | tách trọn vẹn; thứ tự trên $\mathbb R$ |
  | $d=p+1$ (Mệnh đề 03.9) | quy ước $\ge0$ | đơn hình; phân hoạch Radon |
  | $\Pi_{\mathcal H}(m)\le\sum_{j\le d}\binom mj\le(em/d)^d$ (Bổ đề 03.12) | $d<\infty$; $d\le m$ cho dạng đóng | tách điểm cuối; $1+x\le e^x$ |
  | mọi $D$, xác suất $\ge1-\delta$: $\sup_h\lvert L_S-L_D\rvert\le\rho_m$ (Định lý 03.15) | (T1), (T5), (M), hàm lỗi 0–1 | tập mẫu ảo, đổi chỗ, $\Pi_{\mathcal H}(2m)$ cách |
  | mọi $D$, xác suất $\ge1-\delta$, mọi nghiệm ERM: $L_D(\hat h)\le\inf_hL_D(h)+2\rho_m$ (Hệ quả 03.16) | thêm (O1) hoặc (O2) | bước tất định |
  | học được $\iff d<\infty$ (Định lý 03.17) | (M) cho (b) | Định lý 03.15; không có bữa trưa miễn phí |
- **Ghi chú diễn giả:** Mỗi hàng giữ loại bảo đảm của ghi chú. Hàng thứ nhất không có giả thiết thống kê; cận trên phải xét mọi tập lớn hơn một điểm. Ở các hàng sau: hai mệnh đề và bổ đề là khẳng định tất định; định lý và hệ quả là bảo đảm với xác suất cao theo tập huấn luyện, cho mọi phân bố; định lý cơ bản là một đặc trưng của lớp. Ở hàng thứ hai, bỏ hệ số tự do làm chiều VC giảm còn $p$, và quy ước $\ge0$ đặt phía nghiêm ngặt trên $J$. Ba giả thiết của Định lý 03.15 có phản ví dụ khi bỏ: (T5) ở Ví dụ 03.8 (cận $0{,}322$ so với độ lệch $1$), (T1) ở Ví dụ 02.6, chiều VC hữu hạn ở Ví dụ 03.6. Định lý 03.19 (đọc thêm) không có trong bảng. Nguồn: ghi chú Bài 03, §4–§9.
- **Lý do / nối:** bảng tổng kết theo quy định → trả lời vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §4–§9.

#### `7-02` Vấn đề trung tâm — tổng kết · 1,5 phút
- **Mặt trang:** danh sách câu trả lời cho cả bài:
  - Lôgarit của số cách gán nhãn trên $2m$ điểm, $\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$, thay cho $\ln\lvert\mathcal H\rvert$.
  - $L_S(h)$ chỉ phụ thuộc cách gán nhãn trên tập huấn luyện; tập mẫu ảo đưa $L_D$ về $2m$ điểm.
  - Số tham số không thay được chiều VC: $\mathcal H_{\sin}$ có một tham số, $d=\infty$.
  - Cỡ mẫu cho rủi ro vượt mức $0{,}1$: $54\,330$ ($d=1$), $447\,194$ ($d=11$).
  - Dưới (M), học được khi và chỉ khi $d<\infty$; cần (T1), (T5) và hàm lỗi 0–1.
- **Ghi chú diễn giả:** Các câu trả lời theo thứ tự lập luận của bài. Câu hỏi mở đầu được trả lời trọn: với xác suất ít nhất $0{,}95$ và với mọi phân bố, $54\,330$ quan sát đủ để mọi nghiệm ERM trên lớp hàm ngưỡng có rủi ro vượt mức không quá $0{,}1$; với hàm phân lớp tuyến tính, $132\,992$ quan sát cho hai chỉ số đo và $447\,194$ cho mười chỉ số đo. Mỗi con số là một cận trên của độ phức tạp mẫu; cận dưới của Định lý 03.19 cho thấy tốc độ theo $1/\epsilon^2$ không bỏ được. Nguồn: ghi chú Bài 03, đoạn mở đầu, Ví dụ 03.9, §9.
- **Lý do / nối:** trả lời vấn đề của trang mở đầu cho cả bài → bài tập tổng hợp.
- **Mục tiêu / nguồn:** tất cả; §9, Ví dụ 03.9.

#### `7-03` Bài tập: hàm tăng trưởng của lớp sáu hàm ngưỡng — bài tập tổng hợp (Bài tập 03.1(a)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - $\mathcal H^{(6)}_{\mathrm{thr}}=\{h_t:t=1,\ldots,6\}$, $h_t(x)=\mathbb 1[x\ge t]$, trên $\mathcal X=\{1,\ldots,5\}$; $\Pi_{\mathcal H}(m)$ lấy trên mọi bộ $m$ điểm, kể cả bộ có điểm lặp.
  - **Câu hỏi:** chứng minh $\Pi_{\mathcal H^{(6)}_{\mathrm{thr}}}(m)=\min\{m+1,6\}$ với mọi $m\ge1$. Tính giá trị tại $m=3$ và $m=8$.
  - `[f]` **Lời giải:** $x_1<\cdots<x_m$, $m\le5$: ngưỡng $t=x_i$ cho nhãn $0$ trước $x_i$, $1$ từ $x_i$; $t=x_m+1\le6$ cho toàn $0$; đủ $m+1$ cách.
  - `[f]` Bộ có điểm lặp: $k$ điểm phân biệt cho $k+1$ cách, với $k\le\min\{m,5\}$.
  - `[f]` Do đó $\Pi(m)=\min\{m,5\}+1=\min\{m+1,6\}$; $\Pi(3)=4$, $\Pi(8)=6=\lvert\mathcal H^{(6)}_{\mathrm{thr}}\rvert$.
  - `[f]` **Diễn giải:** từ $m=6$, số cách gán nhãn bằng số hàm, nhỏ hơn $m+1$.
- **Ghi chú diễn giả:** Bài tập ghép ba ý của bài: lớp sáu hàm là thu hẹp của lớp hàm ngưỡng lên năm mức đo và có chiều VC $1$; hàm tăng trưởng lấy trên bộ có điểm lặp; và bổ đề Sauer–Shelah so với cận theo số hàm của Bài 02. Một bộ điểm của $\{1,\ldots,5\}$ có nhiều nhất năm điểm phân biệt, nên một bộ tám điểm chứa đủ năm mức đo cho sáu cách gán nhãn, mỗi hàm một cách. Phần (b) của bài tập: tổng nhị thức $1+m$ của Bổ đề 03.12(a) bằng $\Pi(m)$ khi và chỉ khi $m\le5$; với $m\ge6$, cận $\min\{2^m,\lvert\mathcal H\rvert\}=6$ cho đúng giá trị, vì cận Sauer–Shelah chỉ phụ thuộc $d$, không phụ thuộc số hàm. Nguồn: tệp bài tập, Bài tập 03.1(a), (b); ghi chú Bài 03, Ví dụ 03.2, 03.4, Bổ đề 03.12.
- **Lý do / nối:** bài tập tổng hợp của mạch Tổng kết, lấy từ `exercises.md` với đúng dữ kiện, câu hỏi và kết quả; nối mạch 2, 4 với lớp hữu hạn của Bài 02 → tự kiểm tra.
- **Mục tiêu / nguồn:** 2; Bài tập 03.1(a).

#### `7-04` Câu hỏi tự kiểm tra — tổng kết · 2,5 phút
- **Mặt trang:**
  - **Câu hỏi:** trả lời và nêu kết quả đã dùng.
  1. Lớp hình chữ nhật song song với trục tách trọn vẹn $\{(\pm1,0),(0,\pm1)\}$: đã có $d=4$ chưa?
  2. Vì sao không cộng trên các cách gán nhãn của tập huấn luyện?
  3. Một tham số thực có bảo đảm chiều VC hữu hạn không?
  4. Bỏ (T5) thì bước nào của chứng minh Định lý 03.15 hỏng?
- **Ghi chú diễn giả** (câu trả lời, mỗi câu trả lời được chỉ bằng ghi chú): (1) Chưa: bốn điểm và mười sáu hình chữ nhật chỉ cho cận dưới $d\ge4$ (Nhận xét 03.4); phần thiếu là cận trên. Với năm điểm phân biệt, chọn điểm có hoành độ nhỏ nhất, lớn nhất, tung độ nhỏ nhất, lớn nhất; còn ít nhất một điểm $x$; gán $1$ cho các điểm được chọn, $0$ cho phần còn lại; hình chữ nhật chứa các điểm được chọn thì chứa $x$, và hàm $h_\varnothing\equiv0$ cũng không thực hiện được cách này; vậy $d=4$ (câu hỏi cuối buổi §11). (2) Hai lý do: $L_D(h)$ không xác định bởi cách gán nhãn trên $S$, và tập các cách gán nhãn phụ thuộc $S$, trái (T5); tập mẫu ảo sửa cả hai (§7). (3) Không: $\mathcal H_{\sin}$ có một tham số và $d=\infty$ (Nhận xét 03.10(ii)). (4) Bước 3, đếm cách gán nhãn trên tập gộp: khi lớp phụ thuộc tập huấn luyện, đổi chỗ $Z_i\leftrightarrow Z'_i$ đổi cả lớp; Ví dụ 03.8 cho cận $0{,}322$ trong khi độ lệch bằng $1$. Câu hỏi phụ của §11: bốn đỉnh hình vuông không bị lớp hình chữ nhật tách trọn vẹn, không mâu thuẫn với $d=4$, vì một tập không bị tách trọn vẹn không cho cận trên. Nguồn: ghi chú Bài 03, §11 và lời giải; §7; Nhận xét 03.4, 03.10; Ví dụ 03.8.
- **Lý do / nối:** câu hỏi cuối buổi của ghi chú (1) và ba câu về các điểm dễ nhầm (2–4) → bài tập về nhà.
- **Mục tiêu / nguồn:** 1, 3, 5; §11.

#### `7-05` Bài tập về nhà — tổng kết · 1 phút
- **Mặt trang:** bảng `Mục | Bài tập`:

  | Mục | Bài tập |
  |---|---|
  | Tách trọn vẹn và chiều VC | 03.2, 03.7, 03.9, 03.10 |
  | Nửa không gian và hàm phân lớp tuyến tính | 03.3, 03.12 |
  | Hàm tăng trưởng và bổ đề Sauer–Shelah | 03.1, 03.6, 03.8 |
  | Hội tụ đều trên lớp có chiều VC hữu hạn | 03.5 |
  | Rủi ro vượt mức của ERM và định lý cơ bản | 03.4, 03.11 |

  (Bản deck: 03.5 sang mạch 5 vì 03.5(c) cần Định lý 03.15(a); 03.4 sang mạch 6 vì 03.4(a), (b), (e) cần Hệ quả 03.16(c), Ví dụ 03.9, 03.10. Quy tắc: mạch cung cấp kiến thức cuối cùng bài cần.)

  - Dòng liên kết: "Ghi chú bài giảng · Bài tập" (viewer, kèm `&deck=lecture-03-chieu-vc.html`).
- **Ghi chú diễn giả:** Sáu bài đầu là bài gốc, sáu bài sau chọn từ UML (§6.8, §9.6). Bài tập 03.4 gồm cả cỡ mẫu tại $\epsilon=0{,}05$ ($589\,118$ và $1\,999\,657$), nguồn gốc hằng số $8$, lập luận bỏ tập mẫu ảo và chỗ dùng từng giả thiết. Bài tập 03.5 gồm cả phản ví dụ số tham số và lớp chọn sau khi xem tập huấn luyện. Bài tập 03.6 là tùy chọn: một cách chứng minh khác của bổ đề Sauer–Shelah bằng phép dồn. Bài tập 03.9 với $p=2$ là câu hỏi cuối buổi. Bài tập 03.11 đi qua chứng minh phần điều kiện cần của định lý cơ bản. Nguồn: ghi chú Bài 03, §10; tệp bài tập Bài 03.
- **Lý do / nối:** ánh xạ bài tập vào mạch, mỗi bài một mạch → tài liệu.
- **Mục tiêu / nguồn:** tất cả; §10, `exercises.md`.

#### `7-06` Tài liệu tham khảo — tổng kết · 0,5 phút
- **Mặt trang:**
  - Shalev-Shwartz và Ben-David (2014), *Understanding Machine Learning: From Theory to Algorithms* (UML).
  - UML §6.1–6.5: chiều VC, bổ đề Sauer–Shelah, hội tụ đều, định lý cơ bản.
  - UML §9.1: nửa không gian; §5.1: định lý không có bữa trưa miễn phí.
  - Đọc thêm: UML Chương 28.
  - Bài 04: Phân tích sai số, tối thiểu hóa rủi ro cấu trúc và chọn mô hình. {{chữ, liên kết thêm khi deck Bài 04 có tên tệp}}
- **Ghi chú diễn giả:** Trước buổi học: UML §6.1–6.3; sau buổi học: §6.4–6.5, §9.1.3, §5.1 và các bài tập §6.8, §9.6. Mở rộng: Chương 28 (§28.1 cận hội tụ đều qua độ phức tạp Rademacher, §28.2 cận dưới bất khả diễn, §28.3 cận trên khả diễn). Khác biệt so với UML: hàm tăng trưởng lấy trên bộ điểm có thể lặp; bổ đề Sauer–Shelah bằng quy nạp kép, dạng đóng đúng với mọi $1\le d\le m$; hội tụ đều với xác suất cao qua bất đẳng thức Chebyshev và Hoeffding, phụ thuộc $\ln(1/\delta)$, còn UML §6.5 chặn kì vọng rồi dùng bất đẳng thức Markov nên phụ thuộc $1/\delta$; cận trên cho nửa không gian qua định lý Radon. Cầu nối: thay hai chỉ số đo bằng mười làm lớp lớn hơn; sai số xấp xỉ không tăng, nhưng ở $m=10^4$ cận cho rủi ro vượt mức so với lớp tăng từ $0{,}329$ lên $0{,}560$. Câu hỏi cho Bài 04: với một cỡ mẫu cho trước, nên chọn lớp nào giữa các lớp lồng nhau như vậy? Nguồn: ghi chú Bài 03, §11, §12.
- **Lý do / nối:** trang cuối theo quy định → (hết).
- **Mục tiêu / nguồn:** —; §12.

## 7. Hành trình khái niệm

Thứ tự bước theo quy định: vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh (trang riêng) → kỹ thuật hoặc kiểm tra. Các bước có thể chung trang nhưng không đảo thứ tự trên mặt trang; ví dụ đứng sau phát biểu chỉ khi nó là bước kiểm tra (ghi ở cột cuối).

| Kết quả hoặc khái niệm | Vấn đề | Trực quan | Ví dụ | Phát biểu | Ý tưởng chứng minh | Kỹ thuật / kiểm tra | Gộp, `không áp dụng`, lý do |
|---|---|---|---|---|---|---|---|
| Thu hẹp, tách trọn vẹn, chiều VC (Định nghĩa 03.1–03.3) | 1-06 (vô số hàm, sáu hàm trên năm mức đo) | 2-02 (chỉ $m+1$ véc-tơ) | 2-02 (sáu véc-tơ), 2-03 ($\{0\}$, $\{1,2\}$) | 2-02, 2-03 | `không áp dụng` (định nghĩa) | 2-04 (kỹ thuật cận dưới và cận trên) | Ví dụ và định nghĩa chung trang; ví dụ đứng trước định nghĩa trên 2-02. |
| Mệnh đề 03.5, 03.6 | 2-02, 2-03 ($d\le2$ từ $\log_26$) | 2-05 (không giảm; tập nhãn $1$ là khoảng; hình F1) | 2-03 ($\{0\}$ bị tách trọn vẹn), hình F1 | 2-05 | 2-06 | 2-04 (kỹ thuật, trước theo thứ tự Nhận xét 03.4 → Mệnh đề 03.5 của ghi chú); 2-06 dòng "Kết luận:" | Trang kỹ thuật đứng trước phát biểu vì ghi chú đặt Nhận xét 03.4 trước hai mệnh đề; hai mệnh đề chung một trang phát biểu và một trang ý tưởng chứng minh vì cùng cấu trúc. |
| Mệnh đề 03.9 | 2-06 (không có thứ tự trong $\mathbb R^p$), 3-01 | 3-03, 3-04 (đơn hình, phân hoạch Radon; hình F3) | 3-02 (ba điểm, hình F2; ba điểm thẳng hàng) | 3-04 | 3-05 | 3-06 (bốn điểm: $14$ trên $16$; điểm trong tam giác); 3-07 (số tham số) | Bổ đề 03.8 là công cụ, phát biểu và chứng minh một dòng trên 3-03. |
| Bổ đề 03.12 | 3-06, 4-01 ($\Pi=2^m$ khi $m\le d$; cần biết khi $m>d$) | 4-02 (hình F4) | 4-01 ($m+1$, $\binom{m+1}2+1$) | 4-02 | 4-03 (phần (a)), 4-05 (phần (b)) | 4-04 (tách theo điểm cuối trên lớp khoảng, $7=4+3$); 4-05 (bỏ $d\le m$: $0{,}744<2$); 4-06 (Ví dụ 03.5) | Hai phần có hai trang ý tưởng chứng minh; ví dụ 4-04 là bước kiểm tra giữa hai trang. |
| Tính chất hội tụ đều (Định nghĩa 03.13) | 5-00 | 5-01 (thứ tự lượng từ) | 5-02 (phản ví dụ $\mathcal M_{[0,1]}$) | 5-01 | `không áp dụng` (định nghĩa) | 5-02 | Ví dụ sau định nghĩa là phản ví dụ, theo thứ tự của ghi chú. |
| Định lý 03.15 | 5-02 (độ lệch $1$), 5-03 (hai trở ngại) | 5-04 (dòng "Trực quan.": $\sqrt{d\ln m/m}$) | 5-03 (ghi chú diễn giả: $0{,}590$ so với $1$) | 5-04 | 5-05 | 5-06, 5-07 (hai kỹ thuật); 5-08 (bảng, hình F5); 5-09 (bỏ (T5): $0{,}322$ so với $1$) | Số liệu Ví dụ 03.7 là bước kiểm tra sau phát biểu, theo thứ tự ghi chú. |
| Hệ quả 03.16 | 5-08 (chưa có cận cho ERM), 6-00 | 6-01 (hệ số $2$) | 6-03 (Ví dụ 03.9) | 6-01 | 6-02 | 6-03 (trả lời câu hỏi mở đầu), 6-04 (so với rời rạc hóa), 7-03 | Ví dụ là bước kiểm tra sau phát biểu. |
| Định lý 03.17 | 6-04 (điều kiện đủ đã có; có cần không), 5-02 | 6-05 (dòng "Trực quan.": tập huấn luyện thấy nửa tập $2m$ điểm) | 5-02 (lớp $\mathcal M_{[0,1]}$); 6-07 (Hệ quả 03.18) | 6-05 (phần (a)), 6-06 (phần (b)) | 6-07 (hình F7) | 6-08 (cận dưới, tốc độ $1/\epsilon^2$) | Phát biểu chia hai trang vì trần mật độ; phần (a) được thừa nhận (UML §5.1), trang ý tưởng chứng minh nêu rõ điều đó. |
| Định lý 03.19 (đọc thêm) | 6-07 | `không áp dụng` | `không áp dụng` | 6-08 | `không áp dụng` (chứng minh ngoài phạm vi, UML §28.2) | 6-08 dòng "Ý nghĩa:" | Kết quả mức đọc thêm; một trang. |

Thời lượng theo mạch (bản deck): 8 + 18 + 19 + 18,5 + 27 + 20 + 9,5 = 120 phút; 55 trang.

## 8. Hình vẽ

Mọi hình là SVG trong `2627-1/img/lec-03/`, `role="img"`, có `<title>` và alt cụ thể; màu không là tín hiệu duy nhất (điểm nhãn $1$ tô đặc, nhãn $0$ rỗng; nửa mặt phẳng nhãn $1$ tô gạch; đường khác nhau bằng kiểu nét và hình dạng điểm); chữ trong hình chỉ là nhãn trục, nhãn điểm, số và nhãn ngắn (Unicode), không công thức; công thức và chú thích nằm ở `figcaption` (KaTeX). Chú thích nêu dữ liệu. Trục lôgarit phải chứa hết dữ liệu. Dữ liệu chính xác lấy từ mục 5.

| Mã | Tệp | Trang | Nội dung và dữ liệu | Alt dự kiến |
|---|---|---|---|---|
| F1 | `khoang-hai-diem.svg` | 2-05 | Hai phần. Trên: trục số từ $-0{,}5$ đến $2{,}5$, hai điểm $0$, $1$; bốn hàng, mỗi hàng một khoảng và cách gán nhãn tương ứng: $[0,1]$ (đoạn) → $(1,1)$; $[0,0]$ (chấm tại $0$) → $(1,0)$; $[1,1]$ (chấm tại $1$) → $(0,1)$; $[2,2]$ (chấm tại $2$) → $(0,0)$; điểm nhãn $1$ tô đặc, nhãn $0$ rỗng. Dưới: ba điểm tại $1$, $2$, $3$ với nhãn $1$ (đặc), $0$ (rỗng), $1$ (đặc); một đoạn ngoặc từ $1$ đến $3$ phủ cả điểm $2$, nhãn "phải chứa 2". `figcaption`: "Bốn khoảng thực hiện bốn cách gán nhãn của $\{0,1\}$; trên $1<2<3$, mọi khoảng chứa $1$ và $3$ thì chứa $2$, nên $(1,0,1)$ không thực hiện được." | "Trên trục số, bốn khoảng 0 đến 1, chỉ điểm 0, chỉ điểm 1 và chỉ điểm 2 cho bốn cách gán nhãn của hai điểm 0 và 1. Bên dưới, ba điểm 1, 2, 3 với nhãn 1, 0, 1; khoảng chứa điểm 1 và điểm 3 phủ cả điểm 2." |
| F2 | `nua-mat-phang-ba-diem.svg` | 3-02 | Tám ô ($2$ hàng × $4$ cột), mỗi ô trục $[-0{,}5;1{,}5]^2$, ba điểm $(0,0)$, $(1,0)$, $(0,1)$. Nhãn ô: "000", "001", …, "111" theo thứ tự $(y_0,y_1,y_2)$. Đường thẳng theo bảng V3: $x_2=\tfrac12$ (ô 001, 110), $x_1=\tfrac12$ (010, 101), $x_1+x_2=\tfrac12$ (011, 100); ô 000, 111 không có đường. Phía $\langle w,x\rangle+b\ge0$ tô gạch nhạt (ô 111 tô cả ô, ô 000 không tô). Điểm nhãn $1$ tô đặc, nhãn $0$ rỗng. `figcaption`: "Tám cách gán nhãn của $(0,0)$, $(1,0)$, $(0,1)$ và nửa mặt phẳng $\langle w,x\rangle+b\ge0$ với $b=2y_0-1$, $w_i=2y_i-1-b$." | "Tám ô nhỏ, mỗi ô ba điểm tại gốc, (1,0) và (0,1) với một cách gán nhãn. Trong sáu ô có một đường thẳng tách điểm tô đặc khỏi điểm rỗng: đường dọc x bằng một nửa, đường ngang y bằng một nửa, hoặc đường x cộng y bằng một nửa. Hai ô còn lại là hai hàm hằng." |
| F3 | `radon.svg` | 3-03 | Hai phần. Trái: hình vuông $(0,0)$, $(1,0)$, $(1,1)$, $(0,1)$, hai đường chéo; $(0,0)$, $(1,1)$ tô đặc (tập $I$), $(1,0)$, $(0,1)$ rỗng (tập $J$); dấu chữ thập tại $z=(\tfrac12,\tfrac12)$, nhãn "z". Phải: tam giác $(0,0)$, $(3,0)$, $(0,3)$ tô đặc ($I$), điểm $(1,1)$ rỗng ($J$), nhãn "z = (1, 1)". Trục có vạch $0$; $1$; $3$. `figcaption`: "Hai phân hoạch Radon trong mặt phẳng: hai đường chéo của hình vuông giao nhau tại $(\tfrac12,\tfrac12)$; $(1,1)=\tfrac13(0,0)+\tfrac13(3,0)+\tfrac13(0,3)$ nằm trong tam giác." | "Bên trái, hình vuông đơn vị với hai đường chéo cắt nhau tại tâm; hai đỉnh đối diện tô đặc, hai đỉnh kia rỗng. Bên phải, tam giác với ba đỉnh (0,0), (3,0), (0,3) tô đặc và điểm (1,1) rỗng nằm bên trong." |
| F4 | `so-cach-gan-nhan.svg` | 4-02 | Trục ngang $m$ từ $1$ đến $20$ (vạch $1$; $5$; $10$; $15$; $20$); trục dọc thang lôgarit từ $1$ đến $10^7$ (vạch $1$; $10$; …; $10^7$). Ba đường: $2^m$ (nét liền, chấm tròn), tổng nhị thức $\sum_{j\le3}\binom mj$ (nét đứt, tam giác), $(em/3)^3$ từ $m=3$ (nét chấm, không điểm); dữ liệu V7. Bốn ô vuông đặc: $\Pi_{\mathcal H^2_{\mathrm{aff}}}(m)=2;\ 4;\ 8;\ 14$ tại $m=1,\ldots,4$. Nhãn trực tiếp cuối mỗi đường: "2^m", "tổng nhị thức", "dạng đóng"; nhãn số tại $m=20$: "1 048 576", "1351", "5951". `figcaption`: "Ba cận trên cho số cách gán nhãn của một lớp có $d=3$ trên $m$ điểm: $2^m$, $\sum_{j\le3}\binom mj$ và $(em/3)^3$; ô vuông là $\Pi_{\mathcal H^2_{\mathrm{aff}}}(m)$, $m\le4$." | "Đồ thị thang lôgarit theo số điểm từ 1 đến 20. Đường hai mũ m tăng thẳng đến khoảng một triệu; tổng nhị thức bậc 3 tăng đến 1351; dạng đóng tăng đến khoảng 5951 và nằm trên đường hai mũ m khi m từ 3 đến 9. Bốn ô vuông 2, 4, 8, 14 là hàm tăng trưởng của lớp nửa mặt phẳng." |
| F5 | `ban-kinh-vc.svg` | 5-08 | Trục ngang $m$ thang lôgarit từ $10^3$ đến $10^5$ (vạch $10^3$; $10^4$; $10^5$); trục dọc tuyến tính $[0;\ 0{,}8]$ (vạch $0$; $0{,}2$; $0{,}4$; $0{,}6$; $0{,}8$). Hai đường dạng trực tiếp tại $m=1000;\ 2000;\ 5000;\ 10^4;\ 2\cdot10^4;\ 5\cdot10^4;\ 10^5$: $d=3$ (chấm tròn, nét liền) $0{,}464;\ 0{,}340;\ 0{,}225;\ 0{,}164;\ 0{,}120;\ 0{,}0786;\ 0{,}0571$; $d=11$ (tam giác, nét đứt) $0{,}762;\ 0{,}567;\ 0{,}380;\ 0{,}280;\ 0{,}205;\ 0{,}136;\ 0{,}0993$. Nhãn số tại $10^3$, $10^4$, $10^5$ trên cả hai đường; nhãn trực tiếp "d = 3", "d = 11". `figcaption`: "Vế phải thứ nhất của Định lý 03.15(b) theo $m$, với $\delta=0{,}05$, $d=3$ và $d=11$." | "Hai đường giảm theo cỡ mẫu trên trục lôgarit từ 1000 đến 100 000, với độ tin cậy 95%. Với chiều VC 3, cận giảm từ 0,464 xuống 0,057; với chiều VC 11, từ 0,762 xuống 0,099. Đường chiều VC 11 luôn nằm trên." |
| F6 | `doi-cho.svg` | 5-06 | Hai hàng bốn ô: hàng trên "Z1 Z2 Z3 Z4", hàng dưới "Z'1 Z'2 Z'3 Z'4"; trên mỗi cột ghi dấu "+1", "−1", "+1", "−1"; mũi tên hai chiều nối hai ô ở cột 2 và cột 4; bên phải là kết quả sau đổi chỗ: hàng trên "Z1 Z'2 Z3 Z'4", hàng dưới "Z'1 Z2 Z'3 Z4". Ô đổi chỗ có viền đứt. `figcaption`: "Đổi chỗ $Z_i\leftrightarrow Z'_i$ tại các cột có $\sigma_i=-1$, với $m=4$, $\sigma=(+1,-1,+1,-1)$; phân bố của cặp tập không đổi." | "Hai hàng bốn ô, tập huấn luyện ở trên, tập mẫu ảo ở dưới. Ở cột hai và cột bốn, nơi dấu bằng âm một, hai quan sát đổi chỗ cho nhau; hai cột kia giữ nguyên." |
| F7 | `dinh-ly-co-ban.svg` | 6-07 | Sáu nút hình chữ nhật bo góc: "(1) hội tụ đều", "(2) mọi ERM học PAC bất khả diễn", "(3) học được PAC bất khả diễn", "(4) học được PAC", "(5) mọi ERM học PAC", "(6) chiều VC hữu hạn". Mũi tên có nhãn: (6)→(1) "Định lý 03.15"; (1)→(2) "bước tất định"; (2)→(3) "định nghĩa"; (5)→(4) "định nghĩa"; (2)→(5) "Nhận xét 01.26"; (3)→(4) "Nhận xét 01.26"; (4)→(6) "phần (a)", nét đậm. `figcaption`: "Các phép kéo theo của Định lý 03.17(b), dưới (M); phép kéo theo $(4)\Rightarrow(6)$ dùng phần (a)." | "Sơ đồ sáu khẳng định nối bằng mũi tên thành vòng. Chiều VC hữu hạn kéo theo hội tụ đều, rồi mọi ERM học PAC bất khả diễn, rồi các khẳng định học được; học được PAC kéo theo chiều VC hữu hạn qua phần (a) của định lý." |

## 9. Trang tổng kết

Chi tiết từng trang ở mục 6 (7-01 đến 7-06). Tóm tắt:
- **Bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh`:** sáu hàng: Mệnh đề 03.5–03.6, Mệnh đề 03.9, Bổ đề 03.12, Định lý 03.15, Hệ quả 03.16, Định lý 03.17 (7-01); hai hàng xác suất giữ lượng từ "mọi $D$" và "xác suất $\ge1-\delta$", hàng Hệ quả 03.16 giữ "mọi nghiệm ERM".
- **Vấn đề trung tâm:** năm câu trả lời cho cả bài (7-02), không theo mạch.
- **Bài tập tổng hợp:** Bài tập 03.1(a), hàm tăng trưởng của lớp sáu hàm ngưỡng, $\Pi(m)=\min\{m+1,6\}$, $\Pi(3)=4$, $\Pi(8)=6$; lời giải trên mặt trang; phần (b) ở ghi chú diễn giả (7-03).
- **Câu hỏi tự kiểm tra:** bốn câu; câu 1 là câu hỏi cuối buổi §11 (thiếu cận trên); câu 2 (hai trở ngại, §7); câu 3 ($\mathcal H_{\sin}$); câu 4 (Bước 3, Ví dụ 03.8). Câu trả lời ở ghi chú diễn giả, mỗi câu trả lời được chỉ bằng ghi chú (7-04).
- **Bảng `Mục | Bài tập`:** khớp `exercises.md` (03.1–03.12), mỗi bài một mạch (7-05); liên kết "Ghi chú bài giảng · Bài tập".
- **Tài liệu tham khảo:** UML §6.1–6.5, §9.1, §5.1, Chương 28 (đọc thêm) (7-06).
- **Câu nối sang Bài 04:** "Bài 04: Phân tích sai số, tối thiểu hóa rủi ro cấu trúc và chọn mô hình." (7-06); nội dung cầu nối (lớp lồng nhau, $0{,}329$ lên $0{,}560$) ở ghi chú diễn giả.

## 10. Bảng thuật ngữ Việt–Anh của deck

Thuật ngữ xuất hiện trên mặt trang, theo ghi chú và `thuat-ngu.md`; cột cuối là trang có tiếng Anh trong ngoặc (lần dùng đầu trên trang nội dung). Thuật ngữ đã có trong Bài 01–02 vẫn kèm tiếng Anh ở lần đầu trong deck này.

| Tiếng Việt | Tiếng Anh | Trang |
|---|---|---|
| bất đẳng thức hợp | union bound | 1-02 |
| tối thiểu hóa rủi ro thực nghiệm (ERM) | empirical risk minimization | 1-02 |
| học xấp xỉ với xác suất cao (PAC) | probably approximately correct | 1-02 |
| rủi ro vượt mức | excess risk | 1-02 |
| hàm ngưỡng | threshold | 1-06 |
| hàm phân lớp tuyến tính | linear classifier | 1-06 |
| hàm lỗi 0–1 | 0–1 loss | 2-01 |
| lớp con đếm được | countable subclass | 2-01 |
| độ lệch đều | uniform deviation | 2-01 |
| thu hẹp | restriction | 2-02 |
| cách gán nhãn (thực hiện được) | labeling (realized) | 2-02 |
| tách trọn vẹn | shatter | 2-03 |
| chiều Vapnik–Chervonenkis, chiều VC | VC dimension | 2-03 |
| khoảng đóng | closed interval | 2-05 |
| lực lượng | cardinality | 2-06 |
| nửa không gian afin | affine halfspace | 3-01 |
| nửa không gian thuần nhất | homogeneous halfspace | 3-01 |
| siêu phẳng | hyperplane | 3-01 |
| bao lồi | convex hull | 3-03 |
| tổ hợp lồi | convex combination | 3-03 (ghi chú diễn giả) |
| phân hoạch Radon, định lý Radon | Radon partition, Radon's theorem | 3-03 (ghi chú diễn giả) |
| đơn hình | simplex | 3-04 |
| độc lập afin | affinely independent | 3-04 (ghi chú diễn giả) |
| hàm tăng trưởng | growth function | 4-01 |
| quy nạp kép | double induction | 4-03 |
| công thức Pascal | Pascal's rule | 4-03 |
| tính chất hội tụ đều | uniform convergence property | 5-01 |
| hàm cỡ mẫu hội tụ đều | uniform convergence sample size | 5-01 |
| bán kính VC | VC radius | 5-04 |
| tập mẫu ảo | ghost sample | 5-05 |
| đổi chỗ | swapping | 5-05 |
| dấu ngẫu nhiên | random signs | 5-05 |
| tập gộp | combined sample | 5-05 |
| đối xứng hóa | symmetrization | 5-06 (ghi chú diễn giả) |
| rời rạc hóa | discretization | 6-04 |
| định lý không có bữa trưa miễn phí | no-free-lunch theorem | 6-07 |
| kỹ thuật xích | chaining | 6-08 (ghi chú diễn giả) |

## 11. Rủi ro và điểm cần điều phối viên quyết định

1. **Thuật ngữ của bản giao việc.** Bản giao việc viết "phá vỡ tập điểm" và "mẫu ma"; storyboard dùng "tách trọn vẹn" và "mẫu bóng" (nay "tập mẫu ảo", 2026-11-16) của ghi chú (tác giả chốt 2026-11-13; `thuat-ngu.md` dòng 206, 214). Đề nghị điều phối viên xác nhận và sửa bản giao việc cho các bài sau.
2. **Số trang 54, vượt mục tiêu 45–52, dưới trần 55** (lý do ở mục 3). Phương án rút còn 52, không bỏ bước nào của hành trình khái niệm: (a) chuyển Ví dụ 03.10 (6-04) vào ghi chú diễn giả của 6-03, để so sánh với rời rạc hóa chỉ còn ở ghi chú diễn giả và Bài tập 03.4(e) (mục tiêu 4 khi đó chỉ được kiểm ở bài tập); (b) chuyển ví dụ tách theo điểm cuối (4-04) vào ghi chú diễn giả của 4-03 (mất bước kiểm tra bằng số của phép quy nạp). Không khuyến nghị gộp 6-05 với 6-06: bản gộp vượt trần $60$ âm tiết và $6$ dòng.
3. **Bổ đề 03.8 (Radon) không có trang ý tưởng chứng minh riêng:** phát biểu và chứng minh một dòng chung trang 3-03 vì đây là công cụ (blueprint không xếp vào kết quả chính), chứng minh của ghi chú chỉ có một câu. Nếu điều phối viên xếp nó là kết quả chính: thêm một trang (55).
4. **Định lý 03.19 (đọc thêm [O]) không có trang ý tưởng chứng minh:** chứng minh nằm ngoài phạm vi học phần (UML §28.2); ghi chú diễn giả 6-08 nói rõ mức đọc thêm. Hệ quả 03.18 chỉ là dòng "Kết luận:" trên 6-07 vì chứng minh của nó chỉ kiểm giả thiết của Định lý 03.17(a).
5. **Bài tập tổng hợp (7-03) chọn Bài tập 03.1(a)**, giữ nguyên dữ kiện, câu chữ và kết quả; phần (b) (so với tổng nhị thức và với $\min\{2^m,\lvert\mathcal H\rvert\}$) ở ghi chú diễn giả. Lý do: ghép thu hẹp (mạch 2), hàm tăng trưởng và bổ đề Sauer–Shelah (mạch 4) với lớp hữu hạn của Bài 02, đúng trọng tâm "số hành vi so với số phần tử". Phương án khác: đưa cả (b) lên mặt trang thành hai trang (55 trang); hoặc dùng Bài tập 03.4(b) (tỉ số cỡ mẫu theo $d$ và $\epsilon$), cần hai trang vì đề, giữ nguyên câu chữ, và lời giải cộng lại vượt trần $60$ âm tiết của một trang.
6. **Không có trang "Bài tập:" giữa các cụm**, ngoài bài tập tổng hợp. Lý do: trần 55 trang. Các bài tập liên quan được dẫn trong ghi chú diễn giả (mục 5, đoạn đầu). Nếu điều phối viên muốn mỗi cụm chính có một bài tập trên mặt trang, ứng viên tốt nhất là Bài tập 03.2(c) sau 2-06 (hai lời giải thiếu một chiều lập luận), kèm phương án 2(a) để giữ $\le55$.
7. **Ví dụ mới (ghi cách dựng vào `review-log.md` khi duyệt):** N1 tách theo điểm cuối cho lớp khoảng trên $(1,2,3)$: $7=4+3$, $Y_1=\{00,01,11\}$ (4-04; mục 5, V6); N2 các điểm $m=6,\ldots,19$ của hình F4 (V7); N3 bốn cỡ mẫu thêm của hình F5 (V9). Mọi số tính từ công thức hoặc kết quả của ghi chú; không mâu thuẫn số nào của ghi chú.
8. **(O1), (O2) xuất hiện lần đầu trên mặt trang ở 6-01**, không ở 2-01, để giữ trần mật độ của 2-01; 6-01 gọi tên tại chỗ ("ERM chính xác (O1)", "$\epsilon_{\mathrm{opt}}$-ERM (O2)").
9. **Công thức Hoeffding và công thức Pascal không có trên 1-02** (mật độ); Hoeffding được nhắc tên ở 1-02 và công thức ở ghi chú diễn giả; công thức Pascal được viết tại chỗ ở 4-03, tổ hợp lồi và bao lồi ở 3-03 (bao lồi trên mặt trang, tổ hợp lồi ở ghi chú diễn giả). Định lý 03.17 trên 6-05 không ghi "$\mathcal Y=\{0,1\}$" và σ-đại số trên mặt trang (đã có ở 2-01 và ghi chú diễn giả).
10. **Mục tiêu (1-03)** giữ đủ năm mục tiêu của ghi chú theo đúng thứ tự, rút câu chữ: mục tiêu 2 bỏ cụm "và chặn hàm tăng trưởng bằng một đa thức của số điểm khi chiều VC hữu hạn" (nằm trong "so với cận Sauer–Shelah"); mục tiêu 3 bỏ "theo chiều VC"; mục tiêu 4 bỏ "cận độ lệch đều"; mục tiêu 5 viết ba phản ví dụ dạng liệt kê. Đếm được $77$ âm tiết (trần $80$). Nếu điều phối viên muốn giữ cụm của mục tiêu 2, cần bỏ "bằng cận dưới và cận trên" ở mục tiêu 1.
11. **Cột "Giả thiết không được bỏ" ở hàng Mệnh đề 03.5–03.6 của 7-01 là "—"** (khẳng định tất định, không có giả thiết thống kê); ghi chú diễn giả nói cận trên phải xét mọi tập.
12. **Công thức cần đo ở 390 px:** 3-03 (giao hai bao lồi), 3-05 (hai biểu diễn của $g(z)$), 4-03, 4-05 (chuỗi dạng đóng), 5-01, 5-04 (hai dạng của (b)), 5-05 (bất đẳng thức then chốt), 5-06, 5-07, 6-01 ($M(\epsilon,\delta)$), 6-02 (chuỗi ba bất đẳng thức), 6-03. Ngắt bằng `aligned` chỉ khi tràn (quy tắc của tác giả).
13. **Trang sát trần 60 âm tiết** (đếm bằng script, mục 15): 1-02, 1-06, 2-03, 5-05, 5-07, 6-01, 6-02, 6-05, 6-06, 7-03, 7-04 (từ $58$ đến $60$). Người viết deck không thêm chữ trên các trang này; điều phối viên đếm lại trên deck.
14. **Ghi chú diễn giả dẫn kết quả về phía sau** ở 2-04 (Mệnh đề 03.9, Ví dụ 03.3), 3-04 (Bài tập 03.3(c)), 4-03 (Bài tập 03.6): chỉ trong ghi chú diễn giả, không trên mặt trang.
15. **Liên kết hai chiều:** trang 7-06 của deck Bài 02 nhận liên kết tới `lecture-03-chieu-vc.html`; trang 7-06 ở đây là dòng chữ không liên kết cho đến khi deck Bài 04 có tên tệp.
16. **Hình F7 có chữ tiếng Việt trong nút** (nhãn ngắn, không công thức); cần kiểm độ dài nhãn ở 390 px, có thể rút còn "(1)", …, "(6)" kèm chú thích dưới hình.

## 12. Bảng đối chiếu trang → mục và khối của ghi chú

Cột "Đưa vào" ghi kí hiệu, thuật ngữ hoặc kết quả xuất hiện lần đầu trên mặt trang (định nghĩa hoặc "Nhắc lại:"), để kiểm quy tắc định nghĩa trước khi dùng.

| Trang | Mục ghi chú | Khối (số của ghi chú) | Đưa vào |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §9 | Bổ đề 03.12, Định lý 03.15, 03.17 (bằng lời) | — |
| 1-02 | Kiến thức tiên quyết | Bổ đề 02.3, 02.12, Định lý 02.7, 02.14, Hệ quả 02.16 (nhắc lại); Câu hỏi ôn nhanh (ghi chú diễn giả) | bất đẳng thức hợp, ERM, PAC, $K$, $L_S$, $L_D$, $r_m$, $\delta$, rủi ro vượt mức |
| 1-03 | Mục tiêu học tập | — | — |
| 1-04 | toàn bài; §12 | — | — |
| 1-05 | đoạn mở đầu | — | — |
| 1-06 | Câu hỏi mở đầu; §3 | khối ứng dụng | $h_t$, $\mathbb 1[\cdot]$, $p$, $h_{w,b}$, $\langle w,x\rangle$ |
| 2-00 | §1–§4 | — | — |
| 2-01 | §1, §2 | tám thành phần; (T1), (T5), (M) | $Z$, $\mathcal X$, $S\sim D^m$, $\ell_{0\text{-}1}$, $\mathcal H_0$, (T1), (T5), (M), độ lệch đều, $\hat h$, $\inf_h$ |
| 2-02 | §3, §4 | Ví dụ 03.1, Định nghĩa 03.1, Ví dụ 03.2 | $\mathcal H_{\mathrm{thr}}$, $\mathcal H_C$, thu hẹp, cách gán nhãn |
| 2-03 | §4 | Định nghĩa 03.2, 03.3 và các đoạn sau | tách trọn vẹn, $d$, $\operatorname{VCdim}$ |
| 2-04 | §4 | Nhận xét 03.4 | kỹ thuật cận dưới và cận trên |
| 2-05 | §4 | Mệnh đề 03.5, 03.6 | $h_{u,v}$, $\mathcal H_{\mathrm{int}}$ |
| 2-06 | §4 | chứng minh Mệnh đề 03.5, 03.6 | lực lượng |
| 2-07 | tệp bài tập | Bài tập 03.2(b), (c); Nhận xét 03.4 | $\mathcal H_{2\mathrm{int}}$ |
| 3-00 | §5 | — | — |
| 3-01 | §5 | Định nghĩa 03.7 và hai đoạn sau | $\mathcal H^p_{\mathrm{aff}}$, $\mathcal H^p_{\mathrm{hom}}$, siêu phẳng |
| 3-02 | §5 | Ví dụ 03.3, Bước 1–2; Câu hỏi ôn nhanh 2 | $y_0,y_1,y_2$ |
| 3-03 | §5; Phụ lục A | đoạn trước Bổ đề 03.8; Bổ đề 03.8 và chứng minh | bao lồi, $\operatorname{conv}$, $I$, $J$, $z$, $a_i$ |
| 3-04 | §5 | Mệnh đề 03.9 | đơn hình |
| 3-05 | §5; Phụ lục A | chứng minh Mệnh đề 03.9; chứng minh cận trên (b) | $\mathbf e_i$, $g$, $\lambda_i$, $\mu_j$ |
| 3-06 | §5 | Ví dụ 03.3, Bước 3–4 | — |
| 3-07 | §5 | Nhận xét 03.10; Bài tập 03.5(a) (ghi chú diễn giả) | $\mathcal H_{\sin}$, $\theta$ |
| 4-00 | §6 | — | — |
| 4-01 | §6 | Định nghĩa 03.11 và hai đoạn sau; Ví dụ 03.4 | hàm tăng trưởng, $\Pi_{\mathcal H}$ |
| 4-02 | §6 | Bổ đề 03.12; Ví dụ 03.5 (hình) | $\binom mj$, $e$ |
| 4-03 | §6; Phụ lục B | chứng minh Bổ đề 03.12, Bước 1–2 | $C'$, $Y_1$, $B$, quy nạp kép, công thức Pascal |
| 4-04 | §6 | chứng minh Bổ đề 03.12, Bước 1–2 (áp dụng); Mệnh đề 03.6 | — |
| 4-05 | §6 | chứng minh Bổ đề 03.12, Bước 3 và đoạn sau | — |
| 4-06 | §6 | Ví dụ 03.5 | — |
| 5-00 | §7 | — | — |
| 5-01 | §7 | Định nghĩa 02.13 (nhắc lại); Định nghĩa 03.13 và hai đoạn sau | tập $\epsilon$-đại diện, $M$, $m^{UC}_{\mathcal H}$, $m_0$ |
| 5-02 | §7 | Ví dụ 03.6; Ví dụ 01.8, Mệnh đề 01.15 (nhắc lại) | $\mathcal M_{[0,1]}$, $U[0,1]$, $F_1$, $F$, $\mathbb 1_F$ |
| 5-03 | §7 | đoạn về (M), Nhận xét 03.14 (ghi chú diễn giả); Câu hỏi và hai trở ngại; Bài tập 03.4(d) (ghi chú diễn giả) | $S'$ |
| 5-04 | §6 (câu cuối), §7 | Định lý 03.15 và đoạn sau | bán kính VC, $\rho_m$ |
| 5-05 | §7; Phụ lục C | chứng minh Định lý 03.15 (lộ trình) | tập mẫu ảo, đổi chỗ, dấu ngẫu nhiên $\sigma_i$, tập gộp, $\operatorname{Var}$ |
| 5-06 | §7; Phụ lục C.2–C.3 | chứng minh Định lý 03.15, Bước 1–2 và câu cuối; Bài tập 03.4(c) (ghi chú diễn giả) | đối xứng hóa (ghi chú diễn giả), $\ell(h,Z'_i)$ |
| 5-07 | §7; Phụ lục C.4, C.6 | chứng minh Định lý 03.15, Bước 3–5 | kỹ thuật hàm tăng trưởng thay cho số giả thuyết |
| 5-08 | §7 | Ví dụ 03.7 | — |
| 5-09 | §7 | Ví dụ 03.8 và đoạn sau; Bài tập 03.5(c) (ghi chú diễn giả) | $\mathcal G_S$, $h_{\equiv0}$ |
| 6-00 | §8, §9 | — | — |
| 6-01 | §8 | Hệ quả 03.16 và đoạn sau | (O1), (O2), $\epsilon_{\mathrm{opt}}$, $M(\epsilon,\delta)$ |
| 6-02 | §8 | chứng minh Hệ quả 03.16; Hệ quả 02.16 (nhắc lại) | $r$ |
| 6-03 | §8; §9 | Ví dụ 03.9 | — |
| 6-04 | §8; §9 | Ví dụ 03.10; Bài tập 03.4(e) (ghi chú diễn giả) | $q$, rời rạc hóa |
| 6-05 | §8 | đoạn trước Định lý 03.17; Định lý 03.17(a) và đoạn sau | khả diễn (Định nghĩa 01.16, ghi chú diễn giả) |
| 6-06 | §8 | Định lý 03.17(b) | — |
| 6-07 | §8 | danh sách phép kéo theo; Hệ quả 03.18 và chứng minh; Nhận xét 01.26, 01.30 (nhắc lại); Bài tập 03.11 (ghi chú diễn giả) | định lý không có bữa trưa miễn phí |
| 6-08 | §8, §9 | Định lý 03.19 và đoạn sau; §9 (ghi chú diễn giả) | $c$, $\epsilon_0$, $\delta_0$ |
| 7-00 | §9–§12 | — | — |
| 7-01 | §4–§9 | Mệnh đề 03.5, 03.6, 03.9, Bổ đề 03.12, Định lý 03.15, Hệ quả 03.16, Định lý 03.17 | — |
| 7-02 | đoạn mở đầu; §9 | Ví dụ 03.9 | — |
| 7-03 | tệp bài tập | Bài tập 03.1(a); (b) ở ghi chú diễn giả | $\mathcal H^{(6)}_{\mathrm{thr}}$ |
| 7-04 | §11; §7 | câu hỏi cuối buổi và lời giải; Nhận xét 03.4, 03.10; Ví dụ 03.8 | lớp hình chữ nhật song song với trục (gọi tên tại chỗ) |
| 7-05 | §10; tệp bài tập | Bài tập 03.1–03.12 | — |
| 7-06 | §11, §12 | — | — |

Kiểm tra thứ tự: đọc cột "Mục ghi chú" từ trên xuống, các mục không giảm (Kiến thức tiên quyết, tệp bài tập và các phụ lục là nguồn phụ). Trong §5, thứ tự khối trên deck là Định nghĩa 03.7, Ví dụ 03.3 (Bước 1–2), Bổ đề 03.8, Mệnh đề 03.9, Ví dụ 03.3 (Bước 3–4), Nhận xét 03.10; ghi chú đặt cả Ví dụ 03.3 sau Mệnh đề 03.9. Lệch thứ tự này là cố ý: Bước 1–2 là ví dụ trước phát biểu theo hành trình khái niệm (ví dụ ba điểm chỉ dùng công thức, không dùng mệnh đề); nếu điều phối viên muốn giữ đúng thứ tự khối, chuyển 3-02 sau 3-05 và đổi câu "điều đó không cho cận trên" thành dẫn Mệnh đề 03.9. Kí hiệu của Bài 01–02 trên mặt trang ($\mathcal M_{[0,1]}$, Mệnh đề 01.15, Định nghĩa 02.13, Hệ quả 02.16) đều có dòng "Nhắc lại:" hoặc được dẫn kèm số tại chỗ.

## 13. Đề xuất sửa ghi chú và tệp bài tập (không sửa; chờ điều phối viên và tác giả)

Không thấy lỗi toán học trong các khối deck dùng; mọi con số của ví dụ đã tính lại (mục 5), kể cả các bảng của Ví dụ 03.5, 03.7, 03.9, 03.10 và Bài tập 03.1, 03.4. Không có đề xuất sửa ghi chú. Hai ghi chú cho điều phối viên, không thuộc ghi chú bài giảng:

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất |
|---|---|---|---|---|
| nhẹ | bản giao việc của điều phối viên (lời gọi storyboard Bài 03) | Thuật ngữ "phá vỡ tập điểm", "mẫu ma" khác thuật ngữ tác giả đã chốt | `thuat-ngu.md` dòng 206 ("loại 'phá vỡ'"), dòng 214 ("mẫu bóng" (nay "tập mẫu ảo", 2026-11-16)) | Dùng "tách trọn vẹn", "mẫu bóng" trong các bản giao việc sau. |
| nhẹ (đã sửa trong `common-brief.md`) | `common-brief.md`, mục "Tinh thần của bộ trang chiếu" | Danh sách kỹ thuật viết "đối xứng hóa và mẫu ma" | dòng "kỹ thuật cần nhớ … (cận hợp, Hoeffding, đối xứng hóa và mẫu ma, …)" | Đổi thành "đối xứng hóa và mẫu bóng (nay "tập mẫu ảo", 2026-11-16)". |

## 14. Danh sách kỹ thuật đã giới thiệu đến hết Bài 03

| Kỹ thuật | Bài, trang (lần đầu) | Dạng | Trong deck Bài 03 |
|---|---|---|---|
| Tính tuyến tính của kì vọng | Bài 01, 3-03 | một dòng "Kỹ thuật." | không dùng |
| Bất đẳng thức hợp | Bài 01, 4-04 | trang riêng | "Nhắc lại:" ở 1-02 (kèm tên tiếng Anh); dùng ở 5-03, 5-05, 5-07 |
| Chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ | Bài 01, 6-07 | trang riêng | không dùng |
| Tối thiểu hóa từng điểm rồi lấy kì vọng | Bài 01, 5-09 | một dòng | không dùng |
| Phương pháp Chernoff | Bài 02, 3-01 | trang riêng | qua bất đẳng thức Hoeffding (1-02, 5-05) |
| Dây cung của hàm lồi và Taylor bậc hai tại $0$ | Bài 02, 3-03 | một dòng | — |
| Đảo cận đuôi thành bán kính tin cậy và cỡ mẫu | Bài 02, 4-04 | trang riêng | gọi tên ở bước 5 của 5-05 ("Đảo cận đuôi: …"); dùng ở 6-03 |
| Chia xác suất thất bại $\delta/K$ cho từng giả thuyết | Bài 02, 5-05 | trang riêng | dòng "Nhắc lại:" ở 5-07: $\delta/\Pi_{\mathcal H}(2m)$ cho từng cách gán nhãn |
| Bước tất định trên biến cố đại diện | Bài 02, 5-11 | trang riêng | "Nhắc lại:" ở 6-02; dùng ở 6-07 |
| **Cận dưới và cận trên cho chiều VC** | Bài 03, 2-04 | trang riêng | dùng ở 2-06, 3-05, 3-06; dùng lại ở Bài 04 |
| Thứ tự trên đường thẳng cho cận trên | Bài 03, 2-06 | một dòng | — |
| Hàm afin giữ tổ hợp lồi (với phân hoạch Radon) | Bài 03, 3-05 | một dòng | — |
| Tách theo nhãn của điểm cuối rồi quy nạp | Bài 03, 4-03 | một dòng | 4-04 |
| **Đối xứng hóa và tập mẫu ảo** | Bài 03, 5-06 | trang riêng | dùng lại ở Bài 07 |
| **Hàm tăng trưởng thay cho số giả thuyết** | Bài 03, 5-07 | trang riêng | dùng lại ở Bài 04, 07 |
| Bất đẳng thức tiếp tuyến $\ln u\le u/u_0+\ln u_0-1$ để giải cỡ mẫu | Bài 03, 5-05 (ghi chú diễn giả) | một dòng | — |

Deck Bài 04 trở đi nhắc lại các kỹ thuật có trang riêng bằng tên, một dòng "Nhắc lại:".

## 15. Mật độ mặt trang đo bằng script (ước lượng của người lập; số đo trên deck ở mục 16)

Đếm bằng `…/scratchpad/lec-03/storyboard/count.py` trên văn bản dự kiến của mục 6: token cách nhau bởi khoảng trắng; bỏ tiêu đề, công thức `$…$`, đoạn mã, ghi chú `{{…}}` của người lập, nhãn liệt kê "(a)", "(i)" và token không có chữ cái (số, dấu); nhãn "(T1)", "(M)" và tiếng Anh trong ngoặc được đếm. Mỗi dòng là một gạch đầu dòng hoặc một hàng bảng. Trang tổng quan và trang tiêu đề mạch không đếm (bìa ≈ 48 âm tiết luận điểm; hộp Vấn đề trung tâm 22; câu dẫn mạch 20–25).

| Trang | Tổng | Theo dòng | Trang | Tổng | Theo dòng |
|---|---:|---|---|---:|---|
| 1-02 | 60 | 14, 13, 11, 12, 10 | 5-02 | 56 | 8, 2, 17, 12, 17 |
| 1-03 | 77 | 17, 14, 10, 16, 20 | 5-03 | 54 | 7, 16, 9, 14, 8 |
| 1-06 | 58 | 16, 11, 15, 16 | 5-04 | 45 | 9, 12, 13, 5, 2, 4 |
| 2-01 | 56 | 10, 14, 20, 12 | 5-05 | 59 | 6, 13, 9, 12, 12, 7 |
| 2-02 | 49 | 8, 7, 17, 4, 13 | 5-06 | 58 | 10, 18, 12, 18 |
| 2-03 | 59 | 18, 18, 8, 9, 6 | 5-07 | 57 | 18, 16, 9, 14 |
| 2-04 | 54 | 12, 15, 13, 14 | 5-08 | 31 | 2, 4, 1, 10, 14 |
| 2-05 | 49 | 12, 15, 9, 13 | 5-09 | 51 | 2, 12, 8, 7, 6, 16 |
| 2-06 | 51 | 4, 11, 5, 5, 13, 13 | 6-01 | 59 | 11, 10, 14, 14, 10 |
| 3-01 | 44 | 3, 13, 13, 10, 5 | 6-02 | 59 | 12, 4, 9, 17, 11, 6 |
| 3-02 | 39 | 6, 10, 0, 14, 9 | 6-03 | 55 | 12, 11, 14, 1, 17 |
| 3-03 | 43 | 20, 5, 9, 9 | 6-04 | 55 | 17, 4, 6, 6, 3, 19 |
| 3-04 | 41 | 20, 6, 5, 10 | 6-05 | 59 | 17, 12, 10, 12, 8 |
| 3-05 | 45 | 4, 7, 11, 3, 12, 8 | 6-06 | 59 | 6, 7, 16, 9, 7, 14 |
| 3-06 | 59 | 6, 10, 16, 12, 15 | 6-07 | 52 | 4, 9, 4, 5, 14, 16 |
| 3-07 | 34 | 2, 3, 10, 5, 14 | 6-08 | 49 | 11, 13, 2, 4, 19 |
| 4-01 | 53 | 20, 16, 7, 4, 6 | 7-01 | 80 | 11, 8, 9, 8, 15, 15, 14 |
| 4-02 | 36 | 16, 8, 6, 2, 4 | 7-02 | 56 | 10, 13, 12, 7, 14 |
| 4-03 | 56 | 4, 15, 2, 12, 12, 11 | 7-03 | 58 | 12, 11, 11, 10, 2, 12 |
| 4-04 | 14 | 0, 2, 5, 6, 1 | 7-04 | 60 | 10, 14, 13, 12, 11 |
| 4-05 | 27 | 6, 2, 12, 5, 2 | 7-05 | 57 | 3, 6, 9, 7, 10, 11, 11 |
| 4-06 | 32 | 1, 11, 8, 3, 9 | 7-06 | 56 | 11, 13, 12, 4, 16 |
| 5-01 | 59 | 8, 16, 12, 14, 9 |  |  |  |

Trần: 60 cho trang nội dung, 80 cho 1-03, 7-01, 7-05; mọi dòng ≤ 20; mọi trang ≤ 6 dòng (bảng tính theo hàng, không tính hàng tiêu đề vào giới hạn dòng). Kết quả: không trang nào vượt.

## 16. Đối chiếu storyboard ↔ deck đã viết (người viết deck, 2026-11-15)

Deck: `2627-1/lecture-03-chieu-vc.html`, **55 trang** (bảy mạch, sáu trang tiêu đề mạch). Hình (sinh bằng script từ công thức của ghi chú, mục 5; script và ảnh kiểm trong thư mục nháp `…/scratchpad/lec-03/writer/`): `img/lec-03/khoang-hai-diem.svg` (F1, 2-05), `nua-mat-phang-ba-diem.svg` (F2, 3-02), `radon.svg` (F3, 3-03), `so-cach-gan-nhan.svg` (F4, 4-02), `ban-kinh-vc.svg` (F5, 5-08), `doi-cho.svg` (F6, 5-06), `dinh-ly-co-ban.svg` (F7, 6-07). Người viết deck không đọc thêm trang UML nào ngoài các trang ghi ở đầu tệp.

**Mã trang:** giữ nguyên mọi mã của storyboard; thêm `2-07`.

**Chỗ lệch và lý do.**

1. **Quyết định của điều phối viên đã áp dụng:** 6-06 có giả thiết "một thuật toán ERM trên $\mathcal H$ thỏa Định nghĩa 01.4", dòng "Lượng từ" sang ghi chú diễn giả; 7-01 hàng Mệnh đề 03.9 ghi "hệ số tự do $b$" (ghi chú diễn giả: bỏ $b$ thì $d=p$); thêm `2-07` (Bài tập 03.2(c), lời giải ở fragment); 7-03 lời giải đủ hai chiều (nhiều nhất $k+1$ cách; đủ $k+1$ cách), "Diễn giải:" sang ghi chú diễn giả; mục tiêu 2 giữ "chặn bằng đa thức của số điểm", mục tiêu 4 giữ "cận độ lệch đều".
2. **Phát hiện trung bình và nhẹ của cổng duyệt:** 3-03 có "Nhắc lại:" bao lồi và tổ hợp lồi; 1-02 nhắc Định lý 02.14 với (T1)–(T3), $K$ hàm chọn trước, mọi $D$, xác suất $\ge1-\delta$, và Hệ quả 02.16 "cùng biến cố"; học PAC, học PAC bất khả diễn, khả diễn được dẫn số định nghĩa tại chỗ dùng đầu tiên (6-01: Định nghĩa 01.25; 6-05: Định nghĩa 01.16, 01.18), không có dòng "Nhắc lại:" riêng vì 6-01 và 6-05 đã ở trần 60; 6-01 có "ERM (O1) thỏa Định nghĩa 01.4"; 5-07 có "Nhắc lại:" chia $\delta/K$; 5-05 bước 5 gọi tên "Đảo cận đuôi"; 2-04 không dẫn số mệnh đề phía sau ("Dùng khi tính chiều VC của một lớp cụ thể"); 6-05 ghi chú diễn giả theo cơ chế lấy trung bình trên các cách gán nhãn; 2-06 ghi chú diễn giả khớp ba bước; 2-03 mở bằng câu "Lớp thực hiện được mọi cách gán nhãn của $C$ thì khớp được mọi nhãn trên $C$", tiêu đề "Tập bị tách trọn vẹn và chiều VC", "tập rỗng bị mọi lớp khác rỗng tách trọn vẹn", dòng $d\le\log_2\lvert\mathcal H\rvert$ sang ghi chú diễn giả; 4-01 giữ định nghĩa và Ví dụ 03.4, các nhận xét gộp một dòng; 5-01 mở bằng câu nối "Nếu $d\ln(em/d)$ thay được $\ln K$ …", lượng từ sang ghi chú diễn giả; 6-02 bước 4 chỉ gọi Định lý 03.15(c) với $\epsilon/2$, phép tính $64$, $128$ sang ghi chú diễn giả, bước 3 nêu "không có (O1), (O2) thì nó hỏng"; F5 ghi $0{,}205$; alt F4 "m từ 3 đến 9"; 4-04 "$Y_1$ tách trọn vẹn từng vị trí, thiếu $10$"; 3-06 "Kết luận:" thay "Diễn giải:"; 2-02 tách "cách gán nhãn" và "thực hiện được"; 2-01 "của nghiệm ERM $\hat h$"; 5-07 điều kiện $1\le d\le2m$ (4-02 chỉ còn (a), (b), hệ quả lôgarit ở ghi chú diễn giả kèm $1\le d\le m$); 5-06 "Phép chia đôi độ lệch …"; 1-01 luận điểm viết lại; F1 phần dưới có trục riêng $[0{,}5;3{,}5]$; 7-04 "(Bài tập 02.7)"; ghi chú diễn giả 1-02 "ba định nghĩa và một nhận xét".
3. **Dòng dẫn mạch** viết lại theo bài học deck 01 (câu trần thuật về nội dung, không "Người học …"); mục 3 đã sửa theo deck. Ghi chú diễn giả các trang tiêu đề mạch bỏ nhãn "Kế thừa/Nhiệm vụ/Đầu ra".
4. **Bài học deck 02 (tin nhắn điều phối viên):** trang ví dụ mở bằng danh sách dữ kiện (`ul`): 1-06, 2-02, 3-02, 3-06, 4-04, 4-06, 5-02, 5-08, 5-09, 6-03, 6-04; "Trực quan." viết theo cơ chế hoặc cách đọc kết quả: 2-05 (nhãn phải khớp thứ tự trên đường thẳng), 3-04 ($p+1$ hệ số đặt dấu tại $p+1$ đỉnh; hai bao lồi giao nhau), 4-02 (đọc hình thang lôgarit), 6-01 (hai sai số $\rho_m$ cộng lại), 6-05 (tập huấn luyện thấy nhiều nhất nửa tập); 7-01 và 7-02 giữ "xác suất $\ge1-\delta$" và đại lượng được chặn ở mọi hàng xác suất ("mọi $D$" ở 7-02 và ghi chú diễn giả 7-01).
5. **Câu nối trên mặt trang giữa các mạch:** 3-01 dòng đầu "Trong $\mathbb R^p$ không có thứ tự như trên đường thẳng; cận trên cần một công cụ hình học."; 3-07 dòng cuối "Với $m>d$ điểm, cần đếm số cách gán nhãn mà lớp tạo ra."; 5-01 dòng đầu (ước lượng $\sqrt{d\ln m/m}$, câu cuối §6 của ghi chú, chuyển từ cuối 4-06 sang để 4-06 không chạm chân trang); 5-09 "Kết luận:"; các mạch khác nối bằng dòng dẫn mạch.
6. **Rút mặt trang để giữ mật độ và chân trang** (văn xuôi chuyển vào ghi chú diễn giả): 1-02 (bỏ tên tiếng Anh "excess risk" khỏi 1-06, giữ ở 1-02; "union bound" ở 1-02); 2-02 (dòng "vô số hàm" sang ghi chú diễn giả); 3-01 (dòng "mười chỉ số đo: $\mathcal H^{10}_{\mathrm{aff}}$" sang ghi chú diễn giả, con số $d=11$, $d=3$ ở 3-04); 3-03 ("Trực quan." rút còn một câu, tọa độ $(\tfrac12,\tfrac12)$ ở ghi chú diễn giả và 3-06); 5-03 ((ii) bỏ "một lớp chọn theo mẫu", ở ghi chú diễn giả); 5-04 (hai vế phải của (b) viết nội dòng); 5-08 (ô tính đầy đủ $d=3$, $m=10^4$ sang ghi chú diễn giả); 6-03 (hai dòng dữ kiện gộp một); 7-01 (cột "Kết quả" ghi số khối trước, công thức rút gọn; Bổ đề 03.12 ghi dạng đóng $(em/d)^d$ với giả thiết $1\le d\le m$, phần (a) ở ghi chú diễn giả; giả thiết hàm lỗi 0–1 và "mọi $D$" ở ghi chú diễn giả và 7-02).
7. **Bảng `Mục | Bài tập`** (bài học deck 01): 03.5 sang mạch 5 (03.5(c) cần Định lý 03.15(a)), 03.4 sang mạch 6 (03.4(a), (b), (e) cần Hệ quả 03.16(c), Ví dụ 03.9, 03.10); mục 6 trang 7-05 đã sửa.
8. **Hình:** không dùng `figcaption` (như deck 01–02); dữ liệu nằm trong alt và ghi chú diễn giả. F2, F3, F1, F7, F5 đặt trong `grid2 wide-right` (hình bên trái); F1, F3 dùng lớp `short-l`; F6 đặt trong `grid2` cạnh câu đổi chỗ; F4, F5 tăng cỡ chữ để đọc được ở cột hẹp. F7 dùng nút "(1)" … "(6)" với nhãn ngắn, chỉ ghi nhãn trên hai mũi tên có nội dung ("Định lý 03.15", "phần (a)"), các phép kéo theo khác ghi trên mặt trang.
9. **Ghi chú diễn giả** bỏ mọi câu quy trình và lời bình về chính văn bản mà cổng duyệt nêu (1-01, 1-02, 1-03, 1-05, 1-06, 5-07, 7-00, 7-01, 7-02).

**Mật độ (deck_check, âm tiết mặt trang):** 1-01 60; 1-02 60; 1-03 80; 1-04 45; 1-05 20; 1-06 59; 2-00 41; 2-01 58; 2-02 47; 2-03 60; 2-04 54; 2-05 43; 2-06 49; 2-07 59; 3-00 43; 3-01 49; 3-02 31; 3-03 41; 3-04 55; 3-05 40; 3-06 59; 3-07 49; 4-00 36; 4-01 55; 4-02 26; 4-03 51; 4-04 18; 4-05 22; 4-06 27; 5-00 45; 5-01 56; 5-02 54; 5-03 58; 5-04 44; 5-05 60; 5-06 53; 5-07 59; 5-08 24; 5-09 49; 6-00 44; 6-01 56; 6-02 59; 6-03 45; 6-04 54; 6-05 60; 6-06 55; 6-07 45; 6-08 52; 7-00 29; 7-01 67; 7-02 55; 7-03 48; 7-04 58; 7-05 51; 7-06 56. Không trang nội dung nào vượt 60; mọi trang ≤ 6 dòng, ≤ 3 công thức hiển thị. **7-01 "Bảng tổng kết" 67 âm tiết (trần 80 của bảng tổng kết);** deck_check gắn cờ SYLL vì so khóa "Tổng kết" phân biệt chữ hoa. Dòng trên 20 âm tiết chỉ còn ở 1-01 (luận điểm trên trang bìa, 39).

**Kiểm tra máy:** deck_check: console 0, page errors 0, failed 0, không `.katex-error`; cờ OVERFLOW còn ở 1-02, 5-01, 5-04, 5-09, 6-04, 7-02, đều là đuôi SVG của `\sqrt` (phần tử `path`), báo động giả đã biết. `footer_check.py`: 0 trang. Ở 390 px, trang không cuộn ngang (`docScrollW = 390` ở mọi trang); công thức hiển thị và bảng rộng cuộn ngang tại chỗ.


## 17. Sửa sau năm báo cáo duyệt (người sửa, 2026-11-15)

Đầu vào: `reviews/deck-{hoc-vien,toan-hoc,chuyen-gia,su-pham,mach-truyen}.md`; quyết định của điều phối viên ở cuối `review-log.md` (chấp nhận mọi phát hiện; bảng quyết định thắng báo cáo). Deck vẫn 55 trang, mã trang không đổi; mục này thay các chỗ của mục 6 và 16 mà nó nêu. Kiểm tra sau sửa: `deck_lint.py` 0 phát hiện; `footer_check.py` 0 trang; `deck_check.py --shots`: console 0, page errors 0, failed 0, không `.katex-error`, OVERFLOW chỉ còn đuôi SVG của `\sqrt` ở 1-02, 5-01, 5-04, 5-09, 6-04, 7-02 (báo động giả đã biết), `docScrollW = 390` ở mọi trang; liên kết `#/2`…`#/7` mở đúng 2-00…7-00; →, ↓, Space, Esc hoạt động. Mật độ đếm bằng `deck_lint.py` (số trong câu có tính): mọi trang nội dung ≤ 60, 1-03 79/80, 7-01 dưới 80; dòng dẫn mạch ≤ 25; ghi chú diễn giả ≤ 150 (≤ 250 trang chứng minh, bài tập). Bìa 1-01 (luận điểm một dòng) được miễn.

Kí hiệu vai: HV học viên, TH toán học, CG chuyên gia, SP sư phạm, MT mạch truyện; số là thứ tự hàng trong bảng phát hiện của báo cáo.

| Phát hiện | Trang | Nội dung | Kết quả |
|---|---|---|---|
| HV1 | 1-02, 2-03, 5-05, 5-07, 6-05, 6-06, 7-06 | mật độ > 60 khi tính số | đã sửa (lint 0) |
| HV2 | 2-00, 3-00, 5-00, 6-00, 7-00 | dòng dẫn > 25 | đã sửa (viết lại, ≤ 25) |
| HV3 | 5-05 | $\sigma_i$ chưa định nghĩa | đã sửa: bước 2 "$\Pr(\sigma_i=\pm1)=\tfrac12$, độc lập" |
| HV4 | 5-06 | bước tam giác của tập mẫu ảo | đã sửa: dòng $\lvert L_S-L_D\rvert>\epsilon$, $\lvert L_{S'}-L_D\rvert\le\tfrac\epsilon2\Rightarrow\lvert L_{S'}-L_S\rvert>\tfrac\epsilon2$ |
| HV5 | 6-01 | nhãn (a), (b), (c) | đã sửa |
| HV6 | 4-03 | $B$, chiều VC của $Y_1$ | đã sửa: "tập điểm $B\subseteq C'$"; nghĩa "$Y_1$ tách trọn vẹn $B$" ở ghi chú diễn giả |
| HV7 | 3-05 | bước 4 gộp hai ý | đã sửa: bước 4 (quy ước $\ge0$), bước 5 (phần (b)) |
| HV8 | 5-08 | "dạng trực tiếp" | đã sửa |
| HV9 | 6-07, 7-01 | "(a)" hai nghĩa | đã sửa |
| HV10 | 7-02 | thiếu $1\le d\le2m$; $\ln K$ | đã sửa |
| HV11 | 6-01 | (O1), (O2) chưa nhắc lại | đã sửa: dòng "Nhắc lại:" |
| HV12 | 2-01 | (M) chưa gọi tên | đã sửa: "(M), điều kiện đo được" |
| HV13 | 6-04 | dòng hai bán kính không được đọc | đã sửa: "Cùng lớp sáu hàm ($K=6$, $\Pi\le6$)"; "Diễn giải:" thêm "$\rho_m$ gấp hơn bốn lần $r_m$" |
| HV14 | 6-05 | "kể cả bất khả diễn" | đã sửa |
| HV15 | 4-02 | hình thiếu $d=3$; chữ nhỏ ở 390 px | đã sửa nhãn ("tổng nhị thức / d = 3: 1351", "(em/3)³: 5951"), cỡ chữ tăng; ở 390 px chữ còn nhỏ: không sửa thêm, cần lớp CSS cho hình toàn bề ngang (ngoài phạm vi ghi) |
| HV16 | 6-07 | chữ nút nhỏ ở 390 px | sửa một phần: chữ nút 20 px trong viewBox 620; lý do như HV15 |
| HV17 | 4-01, 6-01 | dòng > 20 | đã sửa |
| HV18 | 1-06, 3-03, 5-01 | dấu chấm đứng đầu dòng | đã sửa (dấu chấm trong KaTeX) |
| HV19 | 1-06 | "chỉ sáu hàm" | đã sửa |
| HV20 | 3-04 | "hai bao lồi" | đã sửa (câu thay theo SP8 và CG1) |
| HV21 | 6-03 | "chia đôi khoảng" | đã sửa: "$m$ nhỏ nhất tìm bằng chia đôi khoảng (bisection)" |
| HV22 | 7-02 | dòng trả lời câu hỏi mở đầu | đã sửa: thêm $132\,992$ ($d=3$); "mọi nghiệm ERM, mọi phân bố" ở ghi chú diễn giả (trần 60) |
| HV23 | 3-05, 6-02, 4-06 | vế quyết định khuất ở 390 px | 3-05 đã sửa (`aligned` hai dòng); 6-02, 4-06 không sửa: cuộn tại chỗ đúng quy định, 6-02 đã sát trần khung 16:9 |
| TH1, CG10 | 5-07 | $\delta/\Pi_{\mathcal H}(2m)$ | đã sửa: $\delta/(2\Pi_{\mathcal H}(2m))$; thừa số $2$ ở ghi chú diễn giả |
| TH2, CG6, SP1 | 4-02 | câu sai "phần lớn bị thiếu" | đã sửa (xóa) |
| TH3, SP14 | 2-01, 5-03 | "các lớp của bài thỏa (M)" | đã sửa: ba lớp cụ thể và lớp hữu hạn (Nhận xét 03.14) |
| TH4 | 1-05, 5-00 | thiếu $d\ge1$ | đã sửa |
| TH5 | 5-04, 7-02 | thiếu $1\le d\le2m$ | đã sửa (5-04: "Trực quan." mới; 7-02 có điều kiện) |
| TH6, CG12 | 6-07 | "(a)" | đã sửa |
| TH7, CG2 | 7-01, 5-00 | (M) "không bỏ được" | đã sửa: 7-01 "(T1), (T5), $d<\infty$"; ghi chú diễn giả theo §9 |
| TH8 | 5-07 | "bất đẳng thức hợp của Bài 01" | đã sửa |
| TH9 | 7-05 | thiếu $d$ cho hai cỡ mẫu | đã sửa |
| TH10 | 5-05, 4-06 | kí hiệu rút gọn | 4-06 đã sửa; 5-05 không sửa: thêm $(h)$ làm bất đẳng thức then chốt vượt bề ngang khung (đề xuất ghi "nếu vừa dòng") |
| TH11 | 2-07 | cách toàn $0$ | đã sửa (ghi chú diễn giả) |
| CG1 | 3-04 | "Trực quan." gợi $d$ = số tham số | đã sửa: ma trận các hàng $(x_i^\top,1)$ khả nghịch; ghi chú diễn giả dẫn Nhận xét 03.10 |
| CG3 | 6-01/7-02 | bảo đảm theo lớp hay theo thuật toán | đã sửa ở 7-02 ("bảo đảm cho lớp, mọi $h$ cùng lúc"; ghi chú diễn giả: Hệ quả 03.16 cho mọi thuật toán ERM) |
| CG4 | 5-03, 7-04 | tập mẫu ảo sửa cả hai | đã sửa: tập mẫu ảo sửa (i), dấu ngẫu nhiên khi biết $(S,S')$ sửa (ii) |
| CG5 | 5-05 | chỗ dùng tính bị chặn | đã sửa (bước 1, bước 4) |
| CG7, SP25 | 5-07 | "hành vi" | đã sửa |
| CG8 | 6-08 | cận khả diễn | đã sửa: "Ý nghĩa:" chỉ nói bất khả diễn; ghi chú diễn giả dẫn UML Định lý 6.8, §28.3 |
| CG9, MT N7 | 5-05, 5-06 | phạm vi "đối xứng hóa"; tiếng Anh | đã sửa |
| CG11 | 6-05 | "kể cả" | đã sửa |
| CG13 | 6-01 | "Trực quan." | đã sửa |
| CG14 | 3-04 | suy luận về gốc tọa độ | đã sửa |
| CG15 | 2-01 | σ-đại số | đã sửa (ghi chú diễn giả) |
| CG16 | 4-02 | "Trực quan." nêu cơ chế | đã sửa; cách đọc hình ở ghi chú diễn giả |
| SP2 | 2-01, 6-01, 6-06, F7 | "lớp giả thuyết", "thuật toán ERM" | đã sửa |
| SP3 | 1-02 | "ERM:", "PAC:"; nhắc lại | đã sửa: tên đầy đủ trước, chữ viết tắt trong ngoặc; giả thiết Định lý 02.14 viết bằng lời; Hệ quả 02.16 chuyển sang "Nhắc lại:" ở 6-02 |
| SP4 | 6-01, 6-05, 6-06 | "Nhắc lại:" học PAC, khả diễn, Định nghĩa 01.4 | đã sửa: học PAC và PAC bất khả diễn ở 1-02; khả diễn tại chỗ ở 6-05 ($L_D(h^\star)=0$); "đo được" trên mặt trang, số Định nghĩa 01.4 ở ghi chú diễn giả (trần 60) |
| SP5 | 1-03 | mục tiêu mảnh câu; câu quy trình | đã sửa; vế "thay chiều VC bằng số tham số" của mục tiêu 5 ở ghi chú diễn giả (trần 80) |
| SP6 | 1-04 | văn bản làm chủ ngữ | đã sửa |
| SP7, MT N13 | 7-00, 7-05 | câu trạng thái, câu quy trình | đã sửa |
| SP8, MT3 | 5-04, 3-04 | "Trực quan." lặp phát biểu | đã sửa (5-04: hai trường hợp biên; 3-04: cơ chế, "Bỏ $b$") |
| SP9 | nhiều trang | câu ghi chú lặp | đã sửa (lint REPEAT 0) |
| SP10 | 5-08 | bảng, "Diễn giải:" vận hành | đã sửa |
| SP11 | 6-01 | nhãn phần | đã sửa |
| SP12 | 6-05 | lượng từ (a); "kể cả" | đã sửa |
| SP13 | 3-06 | "Kết luận:" | đã sửa: cách thiếu do phân hoạch Radon (Bổ đề 03.8); "mọi bộ bốn điểm, $d\le3$" ở ghi chú diễn giả (trần 60) |
| SP15 | 7-01, 5-03, … | ghi chú diễn giả > 150 | đã sửa (lint) |
| SP16 | 4-01, 3-05 | dồn ý bằng dấu chấm phẩy | đã sửa |
| SP17 | 3-03, 5-06, 6-05, 6-08 | thiếu tên tiếng Anh | đã sửa; "fundamental theorem" ở dòng từ khóa 6-00 (lần đầu trên mặt trang) |
| SP18 | 2-05, 3-04, 4-02, 5-04, 6-01, 6-05, 6-06 | "Bảo đảm (…):" | đã sửa |
| SP19 | 6-08 | "(đọc thêm)" trên mặt trang | đã sửa |
| SP20 | 5-03 | "Cách sửa:" | đã sửa |
| SP21 | 2-02 | tiêu đề; "chưa thể" | đã sửa: "Cách gán nhãn và thu hẹp của một lớp"; "không thể" |
| SP22 | 2-04 | "Lưu ý:" lặp | đã sửa |
| SP23 | 4-06 | "Diễn giải:" | đã sửa |
| SP24 | 6-03 | "chia đôi khoảng"; tên lớp | đã sửa; số $447\,194$ của mười chỉ số đo đọc ở bảng |
| SP26 | 4-00 | chủ thể trừu tượng | đã sửa |
| SP27 | 4-05 | câu về ghi chú | đã sửa |
| SP28 | 5-05 | "tự thỏa" | đã sửa |
| SP29 | 3-06 | $z$; "bổ đề Radon" | đã sửa |
| SP30 | 2-07 | mảnh câu | đã sửa: "Thứ hai xét một tập, không cho cận trên; thiếu cận dưới." (câu dài hơn vượt trần 60) |
| SP31 | 3-03 | chứng minh dừng trước $z$ | đã sửa |
| SP32 | 5-09 | "áp dụng sai" | đã sửa |
| SP33 | 3-00 | ẩn dụ | đã sửa |
| SP34 | 1-06 | "cần" | đã sửa |
| SP35 | 1-01 | luận điểm | đã sửa |
| SP36 | 5-06 | "Dùng khi …" | đã sửa: "Dùng khi chặn độ lệch đều trên lớp vô hạn" |
| SP37 | 5-01 | thứ tự tên – kí hiệu | đã sửa |
| SP38 | 6-02 | "nó" | đã sửa |
| MT T1 | 6-05 | câu nối điều kiện đủ → cần | đã sửa: "Trực quan. Chiều đủ: Hệ quả 03.16. Chiều cần: …" |
| MT T2, N5 | 3-02, 2-07 | ba điểm thẳng hàng; báo trước | đã sửa: "Lưu ý:" ở 3-02; bỏ câu báo trước ở 2-07 |
| MT4 | 6-01 | (O1), (O2) | đã sửa (như HV11) |
| MT5 | 6-02 | $h_{\mathcal H}$ trên lớp vô hạn | đã sửa |
| MT N1 | 1-06 | thứ tự mục §3 trước §1 | không sửa deck: Câu hỏi mở đầu của ghi chú đứng trước §1; ngoại lệ ghi ở đây |
| MT N2 | 2-01 | (T4) → (T5) | không sửa mặt trang (trần 60); ở ghi chú diễn giả |
| MT N3 | 2-01 | vai trò của (M) | đã sửa: tên "điều kiện đo được" trên mặt trang, vai trò ở ghi chú diễn giả |
| MT N4 | 4-06 | $\Pi=14$ là ô vuông của hình 4-02 | đã sửa (ghi chú diễn giả) |
| MT N6 | 5-05 | "Nhắc lại:" đảo cận đuôi | đã sửa |
| MT N8, N9 | 5-08, 6-04 | như HV8, HV13 | đã sửa |
| MT N10 | 7-00 | dòng dẫn thiếu điều kiện đo được | đã sửa |
| MT N11 | 7-02 | (T1), (T5) gán cho định lý cơ bản | đã sửa |
| MT N12 | 5-05 | ý lặp ở bước 3 | đã sửa |

**Đề xuất sửa ghi chú (chuyển điều phối viên, không sửa):** như mục cuối `review-log.md`; thêm của HV: "dạng đóng" dùng cho cả $(em/d)^d$ và $M(\epsilon,\delta)$.

**Rà toàn deck theo bài học deck 02** (tin nhắn điều phối viên): không còn chữ viết tắt làm nhãn; không còn câu quy trình trong ghi chú diễn giả (1-03, 1-04, 4-05, 7-00, 7-05 đã sửa); "Nhắc lại:" có ở 1-02 (học PAC, ba bất đẳng thức, Định lý 02.14), 3-03 (bao lồi), 5-05 (đảo cận đuôi), 5-07 (chia $\delta/K$), 6-01 ((O1), (O2)), 6-02 (bước tất định).

### Lượt 2 (theo `reviews/deck-kiem-lai-1.md`, người sửa, 2026-11-15)

| Phát hiện | Trang | Sửa | Trạng thái |
|---|---|---|---|
| N1 | 5-03, 5-05 | 5-03 tách hai mảnh: "Tập mẫu ảo (ghost sample) $S'\sim D^m$ độc lập thay $L_D(h)$ bằng $L_{S'}(h)$: sửa (i)." / "Đổi chỗ ngẫu nhiên (swapping) $Z_i\leftrightarrow Z'_i$ khi biết $(S,S')$: sửa (ii)."; 5-05 bỏ "(ghost sample)", "(swapping)" (tên tiếng Anh ở lần dùng đầu là 5-03), giữ "(random signs)" | đã sửa |
| N2 | 1-02, 5-03 | "(union bound)" trả về 1-02; 5-03 bỏ, Câu hỏi rút "các cách gán nhãn này" thành "các cách này" để giữ trần 60 | đã sửa |
| N3 | 2-01 | "(M), điều kiện đo được: $\mathcal H_0\subseteq\mathcal H$ đếm được (countable subclass), mỗi $h\in\mathcal H$ là giới hạn từng điểm (pointwise limit) của dãy trong $\mathcal H_0$." (dòng 20, mặt trang 60); bỏ câu trùng ở ghi chú diễn giả | đã sửa |
| N4 | 1-02 | "hàm lỗi đo được, trong $[0,1]$"; ghi chú diễn giả bỏ "hàm lỗi còn phải đo được" | đã sửa |
| N5 | 4-02 | mặt trang và ghi chú diễn giả theo đề xuất ($Y_1$, coi như một lớp) | đã sửa |
| N6 | 3-04 | "tập đỉnh có gốc, như $\{0,\mathbf e_1,\ldots,\mathbf e_p\}$, không còn bị tách trọn vẹn" | đã sửa |
| N7 | 5-04 | "$d=\infty$: cận $\ge3{,}33$" | đã sửa |
| N8 | 5-05 | "; dùng (T1), (M).", "; dùng (T1).", "; dùng (T5)."; bước 3 "$\le\Pi_{\mathcal H}(2m)$ cách" để giữ trần 60 | đã sửa |
| N9 | 5-06 | tách dòng "Chia đôi độ lệch và miền dài $2$ cho hằng số $8$ trong $\rho_m$."; dòng "Kỹ thuật." rút thành "… bằng $L_{S'}(h)$ của tập mẫu ảo $S'$." (định nghĩa $S'\sim D^m$ độc lập ở 5-03, 5-05) để không chạm chân trang | đã sửa |
| N10 | 2-07 | "Thứ nhất:", "Thứ hai:" ở hai dòng đề; "Thứ hai xét một tập năm điểm nên không cho cận trên, và thiếu cận dưới." | đã sửa |
| N11 | 6-00, 7-02 (ghi chú) | thêm "trong trường hợp bất khả diễn" | đã sửa |
| N12 | 6-08 | hai câu theo đề xuất; hết LINE20 | đã sửa |
| N13 | 7-02 | dòng 2: "(T1), (T5), (M), hàm lỗi 0–1, mọi $D$, xác suất ít nhất $1-\delta$: độ lệch đều $\le\rho_m$, cỡ $\sqrt{d\ln m/m}$, đúng cho mọi $h$ cùng lúc." (20 âm tiết); dòng cuối "Dưới (M): học được …" | đã sửa |
| N14 | 7-04 (ghi chú) | "$0$ cho các điểm còn lại, trong đó có ít nhất một điểm $x$" | đã sửa |
| N15 | 6-03 | "mọi nghiệm ERM"; bỏ "cho rủi ro vượt mức" (đã ở tiêu đề) để dòng không xuống hàng | đã sửa |
| N16 | 3-06 (ghi chú) | "Hai cấu hình là hai bộ bốn điểm cụ thể;" | đã sửa |
| N17 | `so-cach-gan-nhan.svg` | nhãn "(em/3)³: 5951" thay bằng hai dòng "dạng đóng" / "d = 3: 5951", cùng kiểu nhãn "tổng nhị thức" / "d = 3: 1351" | đã sửa |

Kiểm tra lượt 2: `deck_lint.py` 0; `footer_check.py` 0; `deck_check.py --shots` console 0, page errors 0, failed 0, `.katex-error` 0, chỉ còn OVERFLOW `\sqrt` (báo động giả) và SYLL ở 1-01 (bìa), 7-01 (68 ≤ 80). Ảnh 1600×900 và 390×844 (cả ảnh `-end`) của các trang đổi ±2 đã xem. Meta viewport giữ `width=device-width,initial-scale=1`.

### Lượt 3 (theo `reviews/deck-kiem-lai-2.md`, người sửa, 2026-11-15)

| Phát hiện | Trang | Sửa | Trạng thái |
|---|---|---|---|
| M1 | 2-01 | Khôi phục cụm "lớp con đếm được (countable subclass) $\mathcal H_0$": "(M): mỗi $h\in\mathcal H$ là giới hạn từng điểm (pointwise limit) của dãy trong lớp con đếm được (countable subclass) $\mathcal H_0$." Cắt bù: dòng giả thiết viết "(T1) $Z_1,\ldots,Z_m\sim D$ độc lập; (T5) …; (M) điều kiện đo được." (mặt trang 60, dòng dài nhất 18) | đã sửa |
| M2 | 5-06 | "**Kỹ thuật.** … thay $L_D(h)$ bằng $L_{S'}(h)$, $S'\sim D^m$ độc lập." (dòng xuống hàng; footer vẫn 0, không cần cắt bù) | đã sửa |
| M3 | 7-02 | Dòng 2 kết thúc ở "cỡ $\sqrt{d\ln m/m}$."; dòng 3: "Bảo đảm cho lớp, mọi $h$ cùng lúc, nên trên cùng biến cố, rủi ro vượt mức của mọi nghiệm ERM $\le2\rho_m.$" (dấu chấm trong KaTeX để không mồ côi ở 390 px; mặt trang 60, dòng dài nhất 20) | đã sửa |

Kiểm tra lượt 3: `deck_lint.py` 0; `footer_check.py` 0; `deck_check.py --ids L03-2-01,L03-5-06,L03-7-02 --shots` console 0, page errors 0, failed 0, `.katex-error` 0 (7-02 OVERFLOW là đuôi `\sqrt`, báo động giả). Ảnh 1600×900 và 390×844 (cả `-end`) của ba trang đã xem.
