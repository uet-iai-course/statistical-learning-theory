# Duyệt deck Bài 05 — vai học viên cao học (2026-11-15)

Người duyệt: vai 1 `hoc-vien`, chỉ đọc. Bản đóng băng: `2627-1/lecture-05-ha-gradient-ngau-nhien.html` (55 trang). Đối chiếu: `materials/lec-05/lecture-note.md`, `exercises.md`, `planning/lec-05/storyboard.md`, mục "Bộ trang chiếu" của `review-log.md`, deck 01–04.

## Kiểm tra máy đã chạy

- `deck_lint.py`: 1 phát hiện, L05-7-04 68 âm tiết (ngoại lệ 11.9 đã chấp nhận).
- `footer_check.py` (1600×900): 0 trang chạm chân trang.
- `deck_check.py --shots`: console 0, pageerrors 0, failed 0, không `.katex-error`. OVERFLOW ở 4-06, 4-07, 4-08, 4-09, 4-10, 5-02, 6-02, 6-03, 7-02, 7-03: đều là đuôi SVG của `\sqrt` (báo động giả đã biết), không thấy tràn thật trên ảnh. Ở 390 px: `docScrollW = 390` mọi trang; trang không cuộn ngang.
- Đã xem toàn bộ ảnh 1600×900 và 390×844, kể cả ảnh `-end` (tờ ghép trong thư mục nháp `…/lec-05/rv-hoc-vien/sheets/`). Ở 390 px, chữ thân đọc được; bảng và công thức rộng cuộn ngang tại chỗ (3-05, 3-07, 3-08, 4-01, 4-03, 4-04, 4-05, 4-10, 6-04, 6-05); chữ trong hình nhỏ (giới hạn đã biết).

## Đếm mật độ

Cách đếm: token cách nhau bởi khoảng trắng trên mặt trang, bỏ tiêu đề, KaTeX, nhãn hình, ghi chú diễn giả, dòng từ khóa mạch; số trong câu có tính; trong bảng chỉ tính chữ, không tính số. Script riêng trong thư mục nháp, đối chiếu với `deck_check.py` (lệch ≤ 7 do token như "(C)," trong bảng).

| Nhóm | Trang |
|---|---|
| Vượt trần 60 | 7-04: 68 (ngoại lệ đã chấp nhận, câu chữ Bài tập 05.5(d)) |
| Bìa (không áp trần nhưng dài) | 1-01: 101, trong đó luận điểm 77 âm tiết, hai câu |
| Trang trần 80 | 1-03 Mục tiêu: 80 (đúng trần); 7-02 Bảng tổng kết: 81 theo cách đếm của tôi, 74 theo `deck_check` (sát trần); 7-07: 41 |
| Sát trần 60 (55–60) | 2-02: 60; 3-03: 60; 3-06: 59; 4-03: 59; 6-05: 59 (55 + 4 chữ trong bảng); 7-06: 59; 1-06: 58; 2-06: 58; 6-02: 58; 3-04: 56; 6-01: 55; 6-04: 55 |
| 41–54 | 2-01, 2-04, 2-05, 3-01, 3-02, 3-07, 3-08, 4-01, 4-02, 4-04, 4-05, 4-07, 4-08, 4-09, 5-02, 5-04, 6-03, 6-06, 7-03, 7-05, 7-08 |
| ≤ 40 | 1-04, 1-05, 2-03, 2-07, 3-05, 4-06, 4-10, 5-01, 5-03, 7-01 và các trang tiêu đề mạch |
| Quá 6 dòng nội dung | 3-06: 7 dòng (`deck_check` LINES) |
| Dòng > 20 âm tiết (ngoài câu chữ bài tập) | 3-01: 27 (dòng Định nghĩa 05.7); 7-05: 23 (dòng "Kết luận:"); 4-09: 22 (dòng "Kết luận:"); 6-01: 21 |
| Dòng > 20 âm tiết trong câu chữ bài tập | 3-08: 41; 7-04: 36; 5-04: 32; 6-06: 27; 4-10: 25 |

Không trang nội dung nào ngoài 7-04 vượt trần 60; 12 trang ở mức 55–60, xa mục tiêu 40.

## Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L05-1-01 | Luận điểm bìa dài hai câu (77 âm tiết); câu đầu khó đọc khi nghe lần đầu: "tăng không quá một số hạng … có thể âm, cộng một số hạng …". Quy định là luận điểm một câu. | "Sau mỗi bước hạ gradient ngẫu nhiên, bình phương khoảng cách tới một điểm so sánh tăng không quá một số hạng tỉ lệ với độ dài bước, có thể âm, cộng một số hạng tỉ lệ với bình phương độ dài bước. Với độ dài bước chọn theo số vòng lặp, …"; `REPO/CLAUDE.md` § Slide decks: "cover (title, one-sentence thesis, …)". | Giữ một câu: "Với độ dài bước chọn theo số vòng lặp, độ chênh tối ưu kì vọng tại trung bình các điểm lặp của hạ gradient ngẫu nhiên tỉ lệ nghịch với căn bậc hai của số vòng lặp." Bất đẳng thức một bước đã có ở 4-01 và 7-03. |
| trung bình | L05-1-06 | Dòng số liệu ba quan sát không nói các số đến từ đâu và không nêu ý chính; người nghe thấy bốn số mà không biết chúng chứng minh điều gì. Thứ tự $0{,}0694; 0{,}0710; 0{,}1021$ khác thứ tự theo $i_3=1,2,3$ của bảng 3-05 ($0{,}0710; 0{,}1021; 0{,}0694$). | "Ba quan sát, từ $L_S=0{,}0639$: bước SGD cho $0{,}0694$; $0{,}0710$; $0{,}1021$; bước GD cho $0{,}0614$."; ý "cả ba lựa chọn quan sát đều làm $L_S$ tăng" chỉ có trong ghi chú diễn giả; ghi chú bài giảng, Câu hỏi mở đầu: "cả ba lựa chọn quan sát đều làm $L_S$ tăng … Một bước GD với cùng độ dài bước … đưa $L_S$ xuống $0{,}0614$". | "Tập huấn luyện ba quan sát, cùng độ dài bước, từ $L_S=0{,}0639$: mọi bước SGD làm $L_S$ tăng ($0{,}0710$; $0{,}1021$; $0{,}0694$), bước GD làm $L_S$ giảm ($0{,}0614$)." (khoảng +6 âm tiết, trang còn 58 → nên rút chữ ở dòng GD/SGD nếu cần). |
| trung bình | L05-4-02 | Hai số $0{,}1764$ và $0{,}0034$ xuất hiện trong phép tính mà không được gọi tên trên mặt trang; người nghe không biết đó là khoảng cách bình phương tới $w^*$ của điểm chưa chiếu và của $w_3$. | "Không chiếu: vế phải $0{,}5053-0{,}1764+1\approx1{,}3289$; có chiếu: $0{,}5053-0{,}0034+1\approx1{,}5019$." Chỉ ghi chú diễn giả nói "$0{,}1764$ (điểm chưa chiếu $(1,-1)$ …) xuống $0{,}0034$ ($w_3$ …)"; Ví dụ 05.7, Bước 1. | Thêm vào dòng "Ví dụ.": "$\lVert(1,-1)-w^*\rVert^2\approx0{,}1764$, $\lVert w_3-w^*\rVert^2\approx0{,}0034$". |
| trung bình | L05-4-04 | Lộ trình 5 bước không có dòng ghép các bước thành bất đẳng thức tổng trước khi chia cho $T$; bước nhảy từ bước 4 sang bước 5 ("chia cho $T$") khó theo khi nghe lần đầu. | Bước 4: "$\mathbb E\lVert g_t\rVert^2\le G^2$ …"; bước 5: "… (giả thiết (C)); chia cho $T$." Bất đẳng thức $\sum_t\mathbb E[F(w_t)-F(u)]\le\Delta_1/(2\eta)+\eta TG^2/2$ chỉ có trong ghi chú diễn giả; ghi chú bài giảng, chứng minh Định lý 05.14, Bước 4. | Thêm một công thức hiển thị sau bước 4 (trang có 1 công thức, 46 âm tiết): $$\sum_{t=1}^T\mathbb E\big[F(w_t)-F(u)\big]\le\frac{\Delta_1}{2\eta}+\frac{\eta TG^2}{2}.$$ |
| trung bình | L05-4-09 | Gradient của hàm lỗi logistic được dùng để lấy $G=1$, nhưng công thức hàm lỗi logistic chưa xuất hiện trên mặt trang nào của deck; người nghe không kiểm tra được dòng gradient. | "$\lVert\nabla_w\ell\rVert=\lVert x\rVert/(1+e^{\tilde y\langle w,x\rangle})\le1$: $G=1$"; 1-06 và 2-06 chỉ gọi tên "hàm lỗi logistic"; ghi chú bài giảng §3, khối ứng dụng: $\ell(w,(x,y))=\ln\big(1+e^{-\tilde y\langle w,x\rangle}\big)$. | Thêm "$\ell(w,(x,y))=\ln(1+e^{-\tilde y\langle w,x\rangle})$" vào dòng "Ví dụ 05.9." (hoặc vào dòng đầu của 1-06). |
| trung bình | L05-5-01 | Kết luận "(G1) hỏng" được nêu mà không có lý do trên mặt trang; trang chỉ có 20 âm tiết nên còn chỗ. Không nói "bước 3" là của chứng minh nào. | "Từ $t=26$, $f'(w_t)\notin\partial f(w_t)$: (G1) hỏng, bước 3 hỏng."; lý do ($f(1)=0<f(w_t)+f'(w_t)(1-w_t)$ khi $w_t>-1{,}1213$) chỉ trong ghi chú diễn giả; Ví dụ 05.10, Bước 5. 5-02 viết "bước 4 của chứng minh". | "Từ $t=26$: $f(1)=0<f(w_t)+f'(w_t)(1-w_t)$, nên $f'(w_t)\notin\partial f(w_t)$: (G1) hỏng, bước 3 của chứng minh hỏng." |
| nhẹ | L05-4-03 | "Trực quan." không khớp số hạng thứ nhất: số hạng là bình phương khoảng cách chia $2\eta T$, câu nói "khoảng cách ban đầu chia cho tổng độ dài bước". | "Khoảng cách ban đầu chia cho tổng độ dài bước $\eta T$, cộng phần $\eta G^2/2$ mỗi bước góp." so với $\frac{\lVert w_1-u\rVert^2}{2\eta T}$. | "Bình phương khoảng cách ban đầu chia cho $2\eta T$ (tổng độ dài bước), cộng phần $\eta G^2/2$ mỗi bước góp." |
| nhẹ | L05-4-05 | Dòng chuyển sang điểm lặp trung bình viết như thể $c_t\ge F(w_t)-F(u)$ đúng trên từng quỹ đạo; trong Định lý 05.14 điều này chỉ đúng theo kì vọng (ghi chú diễn giả có nói, mặt trang không). | "$F$ lồi và $c_t\ge F(w_t)-F(u)$: chia cho $T$ được $F(\bar w_T)-F(u)\le\frac1T\sum_tc_t$." | Thêm "(trong Định lý 05.14: sau khi lấy kì vọng)" hoặc viết dòng với $\mathbb E$. |
| nhẹ | L05-3-05, L05-3-08 | $w^*$ lần đầu có giá trị trên mặt trang ở câu hỏi 3-08 mà chưa được gọi là nghiệm tối ưu trên $W$; 3-05 chỉ ghi $\min_WL_S\approx0{,}06112$, tên $w^*$ chỉ có trong hình (chữ ≈ 7 px ở 390 px). | 3-05: "$\min_WL_S\approx0{,}06112$"; 3-08: "$u=w^*\approx(0{,}7473;-0{,}6645)$"; Ví dụ 05.6, Bước 5. | 3-05: "$\min_WL_S\approx0{,}06112$, đạt tại $w^*\approx(0{,}7473;-0{,}6645)$". |
| nhẹ | L05-3-05 | "GD: $0{,}0614$" không nói bước GD xuất phát từ $w_3$ với cùng $\eta$; người nghe có thể hiểu là GD từ $w_1$. | "$\mathbb EL_S(w_4)\approx0{,}0808$; GD: $0{,}0614$" | "một bước GD từ $w_3$: $0{,}0614$". |
| nhẹ | L05-3-08 | Cột "hàng" khó hiểu khi đọc tại chỗ; ở 390 px các cột $i_2$ và "hàng" chỉ thấy sau khi cuộn ngang. | Tiêu đề cột `hàng`; ảnh `narrow-022-L05-3-08-end.png`. | Đổi tên cột thành "$\langle\psi(w_2),w_2-u\rangle$" hoặc "trung bình hàng". |
| nhẹ | L05-3-03 | Hằng số $G$ ở 2-06 là hằng số Lipschitz, ở 3-03 là cận mô-men bậc hai; mặt trang không nối hai nghĩa. | 2-06: "$G$ chặn độ dài của mọi dưới gradient trên $U$"; 3-03: "(G2) … $\le G^2$"; ghi chú §2, bảng kí hiệu: "$G$ … hằng số Lipschitz, cận của căn mô-men bậc hai …". | Một dòng "Lưu ý: oracle tất định $\varphi(w,\xi)=v(w)$ thỏa (G2) khi $\lVert v(w)\rVert\le G$, chẳng hạn $F$ là $G$-Lipschitz (Mệnh đề 05.5)". Trang đang 60 âm tiết: bỏ bớt chữ ở dòng mở. |
| nhẹ | L05-6-04, L05-3-07 | Bài 04 đã có trang "Kỹ thuật." cho số hạng chéo ("Thêm bớt kì vọng rồi bình phương; mỗi số hạng chéo …") và cho "Lấy điều kiện theo $S$, rồi bỏ điều kiện"; deck 05 nêu lại thành "Kỹ thuật." mới mà không "Nhắc lại:" tên của Bài 04 trên mặt trang. | 6-04: "**Kỹ thuật.** $e_j=\ldots$ không tương quan: số hạng chéo bằng $0$."; deck 04: "**Kỹ thuật.** Lấy điều kiện theo $S$, rồi bỏ điều kiện." ; `REPO/CLAUDE.md`: "later decks recall it by name with "Nhắc lại:" in one line". | 6-04: "Nhắc lại: thêm bớt kì vọng rồi bình phương (Bài 04); số hạng chéo bằng $0$ vì các $e_j$ không tương quan." 3-07: thêm một dòng "Nhắc lại: lấy điều kiện theo $S$ rồi bỏ điều kiện (Bài 04); ở đây điều kiện là lịch sử." |
| nhẹ | L05-3-06 | 7 dòng nội dung (trần 6), 59 âm tiết. | `deck_check` LINES; năm dòng chữ cộng ba ý (a)–(c). | Chuyển dòng "Để chặn …" vào ghi chú diễn giả, hoặc gộp "Kí hiệu:" với "Trực quan.". |
| nhẹ | L05-6-04 | Ở 390 px công thức hiển thị chứa ba kết luận; định nghĩa $G_b^2$ nằm ngoài khung cho tới khi cuộn ngang. | Ảnh `narrow-043-L05-6-04.png`. | Tách thành `aligned` ba dòng hoặc hai công thức. |
| nhẹ | L05-2-05 | Dòng điểm gãy đọc vấp: "hai nhánh bằng $0$; $0$, $(-1,-2)$ và …". | Bullet thứ hai. | "hai nhánh cùng bằng $0$; các véc-tơ $0$, $(-1,-2)$ và $(-\alpha,-2\alpha)$, $\alpha\in[0,1]$, là dưới gradient." |
| nhẹ | L05-2-01, L05-6-01 | Kí hiệu chưa nêu trên mặt trang: $p$ (chiều của $\mathbb R^p$), $\Xi$ (tập giá trị của $\xi$), $\mathcal Z$, $\mathcal H$ (Bài 01). | 2-01: "$W\subset\mathbb R^p$"; 6-01: "$A_m:\mathcal Z^m\times\Xi\to\mathcal H$". | Thêm $p$ vào dòng "Kí hiệu:" của 1-02; ở 6-01 "$\xi$ nhận giá trị trong $\Xi$" và "Nhắc lại:" $\mathcal Z$, $\mathcal H$ của Định nghĩa 01.4. |
| nhẹ | L05-6-02, L05-1-02, L05-7-01 | Deck chuyển giữa $\operatorname{opt}_S$ và $\operatorname{opt}_s$ không nói $s$ là một giá trị cố định của $S$. | 1-02: "$\operatorname{opt}_S(w)$"; 6-02: "$s=(z_1,\ldots,z_m)$ cố định … $\operatorname{opt}_s$"; 7-01: "$\operatorname{opt}_S$". | 6-02: "$s$: một tập huấn luyện cố định". |
| nhẹ | L05-4-08 | Nội dung cân hai số hạng lặp lại 4-06 ("Tổng nhỏ nhất khi hai số hạng bằng nhau: $\eta^*=R/(G\sqrt T)$"). | 4-06 và dòng "Kỹ thuật." của 4-08. | Giữ ở 4-08 dòng "Kỹ thuật." và bỏ câu tương ứng ở 4-06, hoặc ngược lại. |
| nhẹ | L05-7-02 | Hàng Hệ quả 05.16 thiếu $\eta=R/(G\sqrt T)$, trong khi hàng Hệ quả 05.15 ghi; bảng sát trần 80. | "(C); $\lVert v(w)\rVert\le G$; $\lVert w_1-u\rVert\le R$". | Thêm "$\eta=R/(G\sqrt T)$" hoặc "như Hệ quả 05.15". |
| nhẹ | L05-1-03 | "bản ngẫu nhiên" không phải thuật ngữ của ghi chú. | Mục tiêu 4: "So sánh hạ gradient, bản ngẫu nhiên, lô nhỏ …". | "So sánh GD, SGD và lô nhỏ theo số cập nhật, số quan sát." |
| nhẹ | L05-6-05 | "Diễn giải:" dùng $b=15$ mà không nói vì sao là ngưỡng; lý do ($b=\sigma^2/G_F^2$) chỉ trong ghi chú diễn giả. | "$T(b)$ giảm nhanh đến khoảng $b=15$ …". | "… đến khoảng $b=\sigma^2/G_F^2=15$ …". |
| nhẹ | L05-5-03 | Thẻ Ví dụ 05.12 so với cận mà không nêu điểm so sánh $u=0$. | "Định lý 05.14 chặn $f(\bar w_T)$: $\bar w_T=0$ khi $T$ chẵn, và $0\le0{,}025/T+0{,}1$." | "… với $u=0$: …". |
| nhẹ | L05-3-08 (ghi chú diễn giả) | Câu về câu chữ của tệp bài tập là chuyện biên soạn, không giúp người nghe. | "Câu chữ của bài viết "bằng vế phải của (a)"; phần (a) là đẳng thức …". | Giữ ý toán ("phần (a) là đẳng thức … tức Bổ đề 05.12(c) với $t=2$"), bỏ nửa câu về câu chữ. |
| nhẹ | nhiều trang | 12 trang ở mức 55–60 âm tiết, xa mục tiêu 40 (xem bảng mật độ). Không trang nào vượt trần ngoài 7-04. | Bảng đếm ở trên. | Khi sửa các phát hiện trên, ưu tiên chuyển chữ sang ghi chú diễn giả ở 2-02, 3-03, 3-06, 4-03, 7-06. |

**Tổng:** 0 chặn bàn giao, 0 nghiêm trọng, 6 trung bình, 19 nhẹ.

Điểm tốt khi đọc lần đầu: các trang "Trực quan." ở 3-02, 4-06, 6-02 nêu đúng cơ chế; ví dụ ba bước (3-05) và bảng chín ô (3-08) cho thấy tận mắt vì sao cần kì vọng; mạch 5 đặt mỗi phản ví dụ cạnh đúng bước chứng minh bị hỏng; 7-01 cho thấy bằng số rằng $\operatorname{opt}_S$ nhỏ không kéo theo $L_D$ nhỏ. Số trên hình (4-06, 5-01, 3-05) đều có trong chữ, trừ $(1{,}06;-0{,}92)$ ở 3-05, số không được câu chữ dùng.

## Đề xuất sửa ghi chú

Không có.

## Kết luận

**đạt khi sửa** (sửa sáu phát hiện trung bình; các phát hiện nhẹ tùy điều phối viên).
