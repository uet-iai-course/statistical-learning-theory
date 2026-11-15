# Duyệt cổng storyboard — bộ trang chiếu Bài 09

Người duyệt cổng (chỉ đọc), 2026-11-16. Đối tượng: `planning/lec-09/storyboard.md` (toàn bộ, mục 1–15). Đối chiếu:

- nguồn: `materials/lec-09/lecture-note.md` (đọc toàn bộ, kể cả Phụ lục A–D), `materials/lec-09/exercises.md` (đề và lời giải của Bài tập 09.1, 09.3, 09.4, 09.6, 09.7, 09.8 dùng trên mặt trang);
- quy định: `CLAUDE.md` § Slide decks, `deck-build/common-brief.md` (gồm "Các quy định dễ sót" và bài học deck 01–07), `deck-build/brief-gate.md`, `deck-build/deck_lint.py` (chữ trong ô bảng có tính, số trong bảng và KaTeX không tính; trần 80 chỉ khi tiêu đề chứa "Mục tiêu", "Nội dung" hoặc "tổng kết"), nhật ký yêu cầu 2026-11-13 hàng 1–5;
- khuôn: mục "Bộ trang chiếu" của `lec-05/…/lec-08/review-log.md`, `lec-08/reviews/deck-storyboard-gate.md`, mục 14 của `lec-08/storyboard.md`, slide `L02-4-04` của deck Bài 02 (đã kiểm bằng `grep`), `deck_lint.py` chạy trên deck 01–08;
- ghi chú Bài 10 (dòng 33, Nhận xét 10.5, Phụ lục A) và ghi chú Bài 02, Bài 05 (Hệ quả 02.10, Nhận xét 02.11, Hệ quả 05.15).

`no-ai-slop` chế độ Detect đã nạp. Script tính lại độc lập: thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-09/gate/chk.py` (có kiểm Monte Carlo cho phương sai Ví dụ 09.11 và $\mathbb E\lVert\varphi\rVert^2$ của Bài tập 09.7); `num.py` của người lập cũng chạy lại, kết quả trùng.

## 1. Kết luận

**Đạt khi sửa.** 0 chặn bàn giao, 2 nghiêm trọng, 14 trung bình, 15 nhẹ.

Mọi con số V1–V25 và hình F2 tính lại độc lập khớp storyboard, ghi chú và tệp bài tập (mục 2). Phát biểu của Mệnh đề 09.8, Hệ quả 09.9, 09.13, Định lý 09.12, Mệnh đề 09.15 giữ đủ giả thiết chính; Mệnh đề 09.3 thiếu quy ước và một vế của (c) (T1). Storyboard không thêm giả thiết trộn hay cận nào cho chuỗi phụ thuộc, đúng §1, Ví dụ 09.5 và §10 của ghi chú.

Hai phát hiện nghiêm trọng đều là phát biểu rút gọn bỏ điều kiện, đúng loại lỗi mà quy định cấm ("không chuyển kết quả hàm lỗi bị chặn sang hàm lỗi log, kết quả lồi sang trường hợp khác, khi không có lập luận mới"):

- **N1 (7-02, dòng 3):** "Mẫu hữu hạn: cận Hoeffding (xác suất $\ge1-\delta$) cần mọi xác suất $\ge c>0$" bỏ điều kiện "mô hình cố định, trên tập kiểm tra" của Ví dụ 09.4 và §10; đọc được như một bảo đảm cho $\hat\theta$ trên tập huấn luyện.
- **N2 (6-08, dòng "Nhắc lại:"):** Hệ quả 05.15 được nhắc mà không có (C), (G1) (giả thiết "Như Định lý 05.14"); Bài tập 09.7(a), (b) kiểm đúng hai điều kiện này và không có trên mặt trang.

## 2. Tính lại con số

| Mã | Đối tượng | Kết quả tính lại | Khớp |
|---|---|---|---|
| V1 | câu hỏi mở đầu (1-06) | $0{,}22314$; $0{,}168$; $1{,}78379=0{,}51083+0{,}35667+0{,}91629$ | có |
| V2 | Ví dụ 09.1 | $0{,}58$; $0{,}42$ | có |
| V3 | §2, mật độ | $\ln(0{,}1\sqrt{2\pi})=-1{,}38365$ | có |
| V4 | Ví dụ 09.2 | $0{,}69315$; $0{,}63247$; $0{,}61086$; $0{,}63903$ | có |
| V5 | Bài tập 09.8(c) | $L_s=\tfrac12\ln(2\pi\sigma^2)\to-\infty$ | có |
| V6 | Ví dụ 09.3 | $0{,}59460$; $1{,}81230$ | có |
| V7 | Bài tập 09.1(a), (c) | $0{,}02$; $3{,}91202$; $0{,}97801$; $2{,}65915$; $0{,}128$; $2{,}05573$; $0{,}51393$; $1{,}67185$; $0{,}40$; $0{,}69$ | có |
| V8 | Ví dụ 09.4 | $b=599{,}146$; $0{,}192065$; $115{,}0748$; $0{,}575374$; $0{,}040685$; $6621{,}105\Rightarrow6622$ | có |
| V9 | Ví dụ 09.5 | $1-0{,}2^{10}=1-1{,}024\cdot10^{-7}$ | có |
| V10 | Ví dụ 09.6 | cực tiểu số $0{,}166667$; $\tfrac12$; trọng số $\tfrac14$, $\tfrac1{20}$ | có |
| V11 | KL Bernoulli | $0{,}022582$; $0{,}021601$; $\mathrm h=-0{,}693147$ | có |
| V12 | câu hỏi sau Hệ quả 09.9 | $\mathrm H=0{,}673012$; $L_D(0{,}7)=0{,}695594$ (trùng $-0{,}6\ln0{,}7-0{,}4\ln0{,}3$); hiệu $0{,}084730$ | có |
| V13 | Ví dụ 09.7 | $1{,}203973$; $3{,}454378$; $6{,}907756$; $\ln2{,}5$; $\ln1{,}25$; $0{,}904382$; $0{,}605006$; $0{,}366032$; $0{,}99^{68}=0{,}504886$, $0{,}99^{69}=0{,}499837$; $\ln52=3{,}951244$; $0{,}058736$; $0{,}056002$ | có |
| V14 | Ví dụ 09.8 | $1{,}088900$; $218{,}0774$; $1{,}090387$; $e^{\cdot}=2{,}97543$ | có |
| V15 | Bài tập 09.3(b), (c) | $1{,}039721$; $\ln3$; $0{,}058892$; $0{,}056633$; $0{,}346574$ | có |
| V16 | Ví dụ 09.9 | $-2{,}265512$ | có |
| V17 | Ví dụ 09.10 (bốn dòng) | khe $1{,}153426$; $0{,}153426$; $0{,}040000$; $0$, mỗi khe trùng $\mathrm{KL}(q_\phi\Vert N(1,\tfrac12))$ tính trực tiếp | có |
| F2 | hai parabol | tám giá trị $\mu\in\{-0{,}5;\ldots;2{,}5\}$ với $\sigma^2=\tfrac12$ và $1$: sai lệch so với $-2{,}2655-(\mu-1)^2$ và $-2{,}4189-(\mu-1)^2$ bằng $0$ (bốn chữ số); tại hậu nghiệm $(1,\tfrac12)$ ELBO $=-2{,}2655=\ln p_\theta(2)$; giá trị nhỏ nhất trên trục ngang $-4{,}6689$, trong miền trục dọc $[-4{,}8;-2{,}0]$ | có |
| V18 | Bài tập 09.4(b) | $p_\theta(0{,}5)=0{,}240791$; $-1{,}423824$; $0{,}731059$; ELBO $-1{,}543939$, khe $0{,}120115$; ELBO $-1{,}512003$, khe $0{,}088179$ (bằng KL tới hậu nghiệm); tái tạo $-1{,}143939$, KL tiên nghiệm $0{,}368064$ | có |
| V19 | Ví dụ 09.11 | phương sai $1$; $6$ (Monte Carlo $2\cdot10^6$ lần rút: $0{,}9997$; $5{,}9905$); gradient log $29{,}02702$ (Monte Carlo $28{,}99$, kì vọng $1{,}995$) | có |
| V20 | Ví dụ 09.12 | $0{,}352065$; $2{,}3333$ | có |
| V21 | Ví dụ 09.13 | $4{,}605170$; $1{,}418939$; $1{,}424812$; $2{,}548376$; $8{,}892\cdot10^{-44}$; $0{,}005874$ | có |
| V22 | Bài tập 09.7(c), (d) | $12$; $8$; $9{,}75$; $5{,}75$ (Monte Carlo tại $(0,1)$: $11{,}98$); $R=2{,}061553$; $\eta=0{,}005951$; $\sqrt{51}/100=0{,}071414$; $0{,}0714/0{,}00014\approx510$ | có |
| V23 | Bài tập 09.6(b) | $2{,}441847$; $0{,}096032$; $0{,}234496$; $57{,}2$ | có |
| V24 | §12 (a), (c) | $0{,}096$; $2{,}343407$; $0{,}781136$; $2{,}183951$; $0{,}0400$ | có |
| V25 | câu ôn nhanh | $0{,}192065$; $0{,}4$; $0{,}75$ | có |

## 3. Phát biểu kết quả trên mặt trang so với ghi chú

| Kết quả | Trang | Đối chiếu |
|---|---|---|
| Mệnh đề 09.3 | 3-01 | Thiếu quy ước "tích bằng $0$ khi có tiền tố xác suất $0$" ở (a) (không có quy ước, vế phải không xác định), điều kiện "$p_1(x_{<j})>0$" của dòng "Kí hiệu:", và vế sau của (c) ("xác suất có điều kiện của nó bằng $p_\theta(\cdot\mid x_{<j})$ trên mọi tiền tố có xác suất dương") (T1). |
| Mệnh đề 09.8 | 4-02 | Khớp ((a) trong $[0,\infty]$, (b) dấu bằng, (c) hai điều kiện khả tích). Dòng "Trực quan." lặp Bước 2 của chứng minh và đọc sai dấu (T2). |
| Hệ quả 09.9 | 4-04 | Khớp ((a) với $L_D$ hữu hạn; $\inf$; (b) đặc tả đúng). |
| Định lý 09.12 | 5-02 | Khớp bốn giả thiết (thiếu chữ "mật độ trên $\mathcal X\times\mathcal V$", chấp nhận). (d), "mọi số hạng hữu hạn" của (a) và "khi kì vọng xác định" của Định nghĩa 09.11 chỉ ở ghi chú diễn giả (L4). |
| Hệ quả 09.13 | 5-05 | Khớp (tập huấn luyện cố định, bước E, bước M hữu hạn, phạm vi). Không có trang ý tưởng chứng minh dù có hàng riêng ở 7-01 (T4). |
| Mệnh đề 09.15 | 6-02 | Khớp (i)–(iii), loại bảo đảm. (ii) thiếu "$\zeta\notin N_0$" (L12). |
| Hệ quả 05.15 (nhắc lại) | 6-08 | Thiếu (C), (G1) (N2). |
| Hệ quả 02.10(b) (nhắc lại) | 1-02 | Khớp ("hàm lỗi trong $[0,1]$" gộp (T2), (T3)). |

Các điểm được giao kiểm riêng:

- **Hàm lỗi log không bị chặn, điều kiện $c>0$.** Đúng ở 2-03, 3-05, 3-06, 4-06, 7-03. Sai ở 7-02 (N1). Ghi chú diễn giả 1-05 viết "và chỉ khi xác suất của mô hình bị chặn dưới": "khi" thành "chỉ khi" (L1).
- **Quan sát độc lập ở cấp chuỗi so với phụ thuộc trong chuỗi.** Đúng ở 1-06, 2-02, 3-05, 3-06, 7-03; phép đếm $0{,}0407$ được gọi đúng là "không được chứng minh".
- **Chuỗi phụ thuộc yếu.** 2-02, 3-07 (ghi chú diễn giả), 7-02, 7-04 câu 2 chỉ nói "cần thêm giả thiết về sự phụ thuộc", như §1 và Ví dụ 09.5. Không vượt ghi chú.
- **Phân kì KL, ELBO, tái tham số hóa.** Khớp, trừ: 5-03 bước 4 dẫn "Mệnh đề 09.8(b)" cho hai mật độ (ghi chú dùng lập luận Bước 3–4, bản mật độ) (L5); 7-02 dòng 4 và 6-04 dòng 2 đổi điều kiện đủ (i)–(iii) thành điều kiện cần (T3); 6-07 gán cận dưới $1{,}4189$ cho $p_{\theta_3}\ge0{,}01\,p_{\theta_1}$ thay cho Mệnh đề 09.8(c) (T13).
- **Kỹ thuật "Đổi chỗ đạo hàm và kì vọng" dùng lại ở Bài 10.** Đúng là dùng lại, nhưng ở Nhận xét 10.5 và Phụ lục A của ghi chú Bài 10 ("Như chứng minh Mệnh đề 09.15 ở Phụ lục B của Bài 09", dòng 932), không ở chứng minh Định lý 10.4 như storyboard ghi (mục 4, mục 11 điểm 3, mục 14) (T6). Bài 10 còn dẫn Mệnh đề 09.15 trong Kiến thức tiên quyết (dòng 33) và Mục tiêu 2 ("nêu điều kiện đổi chỗ đạo hàm và kì vọng"). Trang riêng 6-04 là đúng quy định. Không deck 01–08 nào đã có kỹ thuật này (`grep` "đổi chỗ đạo hàm" trên deck 01–08: $0$).

## 4. Ý kiến về các điểm của mục 11 (điều phối viên quyết định)

1. **54 trang.** Đồng ý giữ 54, không lấy phương án (a) hay (b). Nếu chấp nhận T4 (thêm trang ý tưởng chứng minh cho Hệ quả 09.13) thì deck có 55 trang, đúng trần; lý do ghi ở `review-log.md`. Cách khác giữ 54: gộp Hệ quả 09.13 vào hàng Định lý 09.12 ở 7-01 (như Mệnh đề 09.8 với Hệ quả 09.9), khi đó Hệ quả 09.13 không là kết quả chính và dòng "Chứng minh." ở 5-05 đủ.
2. **Hệ quả 09.9, 09.13.** Hệ quả 09.9: đồng ý (chung hàng với Mệnh đề 09.8, chứng minh một phép trừ). Hệ quả 09.13: không đồng ý giữ như hiện tại khi nó có hàng riêng ở 7-01; tiền lệ `lec-08/review-log.md` dòng 318 (Hệ quả 08.7: "thêm trang 'Ý tưởng chứng minh' riêng", "khuôn chung"). Xem T4.
3. **Trang kỹ thuật 6-04.** Đồng ý có trang riêng; sửa chỗ dẫn Bài 10 (T6) và chữ "Cần:" (T3).
4. **Nhận xét 09.5 ở 3-08.** Đồng ý; mạch 3 vẫn là §5–§6 liên tiếp, và Định nghĩa 09.6 dẫn chính Nhận xét 09.5.
5. **Ví dụ 09.1 trên trang Định nghĩa 09.1.** Đồng ý.
6. **Câu chữ bài tập rút gọn.** Đồng ý theo tiền lệ Bài 08, trừ 6-08 dòng (d): "cận này là kì vọng của KL nào?" đổi nghĩa câu hỏi (T14).
7. **Bài tập tổng hợp 09.6(b).** Đồng ý; lời giải trên mặt trang cần phần kết luận được phép (T7).
8. **6-08 nhắc lại Bài 05.** Đồng ý giữ Bài tập 09.7(c), (d), với điều kiện dòng "Nhắc lại:" có (C), (G1) (N2). Đồng ý thêm Hệ quả 05.15 vào Kiến thức tiên quyết của ghi chú (đề xuất mục 13, hàng 2).
9. **Mật độ, trung vị 53.** Không đạt mức các bài trước (Bài 08 cổng duyệt yêu cầu $\approx50$–$51$). Đề xuất cắt cụ thể ở mục 6, trung vị ước $\approx50$–$51$. Ngoài ra 7-05 vượt trần $60$ của `deck_lint.py` (T9).
10. **Đảo cận đuôi ở 3-06.** Nên lên mặt trang, đúng quy định "later decks recall it by name with 'Nhắc lại:' in one line": 6622 là phép đảo của Bước 5. Cắt bù: chuyển dòng 4 "Cần $c>0$: …" vào ghi chú diễn giả, vì 2-03 dòng 3, 3-05 dòng 3 và 7-02 đã nêu điều kiện này (T5).
11. **Chuỗi phụ thuộc yếu.** Đồng ý (mục 3).
12.–13. **Đo ở 390 px, trang có hình.** Đồng ý. Ở 5-04, nên đặt dòng định nghĩa khe lên trước bảng (L6).
14. **"Trực quan." của Mệnh đề 09.15 ở 6-01.** Đồng ý.
15.–17. Đồng ý.

## 5. Bảng phát hiện

`mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa`

| Mã | Mức độ | Trang chiếu | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|---|
| N1 | nghiêm trọng | 7-02 dòng 3 | Dòng rút gọn bỏ điều kiện "mô hình cố định, trên tập kiểm tra"; đọc được như cận Hoeffding cho ước lượng học từ tập huấn luyện, tức chuyển kết quả của một giả thuyết cố định sang $\hat\theta$. | Storyboard: "Mẫu hữu hạn: cận Hoeffding (xác suất $\ge1-\delta$) cần mọi xác suất $\ge c>0$." Ghi chú §10: "Ví dụ 09.4: một mô hình cố định có $c>0$, trên tập kiểm tra"; Ví dụ 09.4, Thiết lập: "cố định, không phụ thuộc tập kiểm tra". | "Mẫu hữu hạn: mô hình cố định có mọi xác suất $\ge c>0$, trên $m_v$ chuỗi kiểm tra: cận Hoeffding với xác suất $\ge1-\delta$." Ghi chú diễn giả 7-02 thêm: ước lượng hợp lý cực đại không chính quy hóa có $\mathbb E_SL_D(\hat\theta)=+\infty$ (đã có). |
| N2 | nghiêm trọng | 6-08 dòng 1 | "Nhắc lại:" Hệ quả 05.15 bỏ (C) và (G1); trang dùng một kết quả lồi mà mặt trang không nêu tính lồi, trong khi chính Bài tập 09.7(a), (b) kiểm hai điều kiện này. | Storyboard: "Hệ quả 05.15: $\eta=R/(G\sqrt T)$ cho $\mathbb EF(\bar w_T)-\min_WF\le RG/\sqrt T$ khi mọi $u\in W$ có $\lVert w_1-u\rVert\le R$." Ghi chú Bài 05, Hệ quả 05.15: "Giả thiết. Như Định lý 05.14, thêm hai thành phần"; `lec-05/reviews/deck-storyboard-gate.md` T7 (cùng lỗi ở bảng tổng kết Bài 05). | "**Nhắc lại:** Hệ quả 05.15: dưới (C), (G1), (G2) và $\lVert w_1-u\rVert\le R$ trên $W$, $\eta=R/(G\sqrt T)$ cho $\mathbb EF(\bar w_T)-\min_WF\le RG/\sqrt T$." Thêm một dòng sau đề: "(C), (G1) thỏa theo (a), (b) (về nhà)." Định nghĩa $\bar w_T$ (trung bình các điểm lặp) trong cùng dòng (L15). Cắt bù: bỏ "mô phỏng: $0{,}00014$" khỏi mặt trang (đã ở ghi chú diễn giả). |
| T1 | trung bình | 3-01 | Phát biểu Mệnh đề 09.3 thiếu quy ước của (a), điều kiện xác định xác suất có điều kiện, và vế sau của (c). | Ghi chú: "(a) … với quy ước tích bằng $0$ khi có tiền tố xác suất $0$"; "khi $p_1(x_{<j})>0$"; "(c) … và xác suất có điều kiện của nó bằng $p_\theta(\cdot\mid x_{<j})$ trên mọi tiền tố có xác suất dương". | Dòng "Kí hiệu:" thêm "khi $p_1(x_{<j})>0$"; (a) thêm "(tích $=0$ khi có tiền tố xác suất $0$)"; (c) thêm "có xác suất có điều kiện $p_\theta(\cdot\mid x_{<j})$". Cắt bù: dòng 1 "Bảng cho từng chuỗi: $\lvert\mathcal A\rvert^n-1$ tham số." (bỏ "($4^{200}-1$ với DNA)", DNA chưa có trên mặt trang; đưa vào ghi chú diễn giả); "**Bảo đảm:** tất định, với mọi $x_{1:n}$:" giữ. Người viết đếm lại; nếu vượt $60$, rút "Trực quan." thành "**Trực quan.** Thừa số thứ $j$: phân lớp kí tự $j$." |
| T2 | trung bình | 4-02 dòng 1 | "Trực quan." lặp Bước 2 của chứng minh (bài học deck 02) và gợi ý sai: tại từng $x$, $\ln(p_D/p_\theta)$ có thể âm, chỉ kì vọng không âm. | "**Trực quan.** Ở mỗi $x$, mô hình trả thêm $\ln\frac{p_D(x)}{p_\theta(x)}$; vô hạn khi $p_\theta(x)=0<p_D(x)$." Chứng minh Mệnh đề 09.8, Bước 2; `common-brief.md`: "'Trực quan.' nêu cơ chế hoặc cách đọc kết quả …, không nhắc lại phát biểu hay một bước chứng minh". | "**Trực quan.** Gán xác suất nhỏ cho điểm hay xảy ra thì hàm lỗi lớn; bỏ sót một điểm của giá thì rủi ro $+\infty$." Ghi chú diễn giả: số hạng $\ln(p_D/p_\theta)$ âm ở chỗ mô hình gán nhiều hơn $p_D$, kì vọng theo $D$ của nó là KL, không âm. |
| T3 | trung bình | 7-02 dòng 4; 6-04 dòng 2 | Điều kiện đủ (i)–(iii) viết thành điều kiện cần ("khi" thành "chỉ khi", bài học deck 01); 6-04 bỏ "liên tục" của (i). | 7-02: "gradient theo đường đi cần (i)–(iii)"; 6-04: "Cần: khả vi trên mọi đường ngoài một tập xác suất $0$ chung; hàm trội khả tích." Ghi chú §10: "không chệch khi các điều kiện của Mệnh đề 09.15 thỏa"; (i): "khả vi liên tục". | 7-02: "gradient theo đường đi không chệch khi (i)–(iii) thỏa". 6-04: "Đủ: khả vi liên tục trên mọi đường ngoài một tập xác suất $0$ chung, hàm trội khả tích, $\mathbb E\lvert\kappa\rvert<\infty$." Dòng "Dùng khi" thêm "(Mệnh đề 09.15)". |
| T4 | trung bình | 5-05; 7-01 | Hệ quả 09.13 có hàng riêng trong bảng kết quả chính nhưng không có trang "Ý tưởng chứng minh"; tiền lệ Bài 08 đã yêu cầu thêm trang trong trường hợp này. | 7-01 hàng "Hệ quả 09.13, tất định …"; `common-brief.md`: "Mỗi kết quả chính có trang 'Ý tưởng chứng minh' riêng"; `lec-08/review-log.md` dòng 318. | Hoặc thêm trang của mục 11 điểm 2 (55 trang; dãy ba quan hệ chuyển từ 5-05 sang trang mới, 5-05 còn phát biểu, nên 5-05 xuống $\approx45$), hoặc gộp Hệ quả 09.13 vào hàng Định lý 09.12 ở 7-01. |
| T5 | trung bình | 3-06 | Dùng kỹ thuật "Đảo cận đuôi thành bán kính và cỡ mẫu" (`L02-4-04`) cho $6622$ chuỗi mà không nhắc tên trên mặt trang. | Mục 14 storyboard; `CLAUDE.md` § Slide decks, Techniques: "later decks recall it by name with 'Nhắc lại:' in one line". | Thêm "**Nhắc lại:** đảo cận đuôi (Bài 02): cỡ mẫu cho một bán kính cho trước." ($\approx13$). Chuyển dòng 4 "Cần $c>0$: …" ($13$) vào ghi chú diễn giả (điều kiện đã có ở 2-03, 3-05, 7-02). Ước $\approx52$. |
| T6 | trung bình | mục 4 (hàng Mệnh đề 09.15), mục 11 điểm 3, mục 14 | Dẫn sai chỗ Bài 10 dùng lại kỹ thuật. Danh sách mục 14 là đầu vào của storyboard Bài 10. | Ghi chú Bài 10, dòng 932: Phụ lục A, "Chứng minh khẳng định của Nhận xét 10.5 … Như chứng minh Mệnh đề 09.15 ở Phụ lục B của Bài 09"; Định lý 10.4 (dòng 272–317) chứng minh bằng tổng hữu hạn và Bổ đề 10.3, không đổi chỗ đạo hàm và kì vọng. | Thay "chứng minh Định lý 10.4" bằng "Nhận xét 10.5 (chứng minh ở Phụ lục A của Bài 10)" ở ba chỗ. |
| T7 | trung bình | 7-03 | "Lời giải:" chỉ nêu kết luận không được phép (liệt kê phủ định) và bỏ phần so với độ lệch chuẩn của câu (b)(i); mặt trang bài tập phải giữ kết quả của `exercises.md`, và giọng tác giả đòi nghĩa dương của bảo đảm. | Storyboard: "[f] Chỉ cho thiết lập này; không cho phân bố khác, mạng nơ-ron, Thiết lập B." `exercises.md`, lời giải 09.6(b), Bước 2–4: "lớn hơn khoảng $57$ lần …"; "Kết luận được phép: … hiệu với mô hình thật giảm từ $0{,}0316$ … xuống $0{,}00008$"; danh sách không được phép có "lớp mô hình không chứa phân bố thật". | Fragment cuối: "Bán kính gấp $\approx57$ lần độ lệch chuẩn $0{,}0041$. Được phép: trong thiết lập này, hiệu với mô hình thật giảm khi $m$ tăng; không suy ra cho phân bố, lớp mô hình khác hay Thiết lập B." Cắt bù: bỏ "(Ví dụ 09.8)" ở dòng 1 và "Chỉ cho thiết lập này" ($\approx-7$); người viết đếm lại, trần $60$. |
| T8 | trung bình | nhiều trang (mục 6) | Trung vị $53$ trên $42$ trang nội dung; cổng duyệt Bài 08 yêu cầu $\approx50$–$51$; storyboard ghi "mục tiêu $50$", trong khi `common-brief.md` đặt mục tiêu $\le40$. | Mục 15 storyboard: "median 53.0 <=50 11 51-56 22 57-60 9"; `lec-08/reviews/deck-storyboard-gate.md` mục 6. | Cắt theo mục 6. Sửa câu "trên mục tiêu $50$" thành "mục tiêu $\le40$, trần $60$". |
| T9 | trung bình | 7-05 | $61$ âm tiết vượt trần $60$ của `deck_lint.py`: tiêu đề "Bài tập về nhà" không thuộc nhóm trần $80$. Mục 9, 11 điểm 9 và 15 ghi sai "$61$/80"; `count.py` của người lập cũng báo "$>60$". | `deck_lint.py` dòng 54: `cap = 80 if re.search(r'Mục tiêu|Nội dung|[Tt]ổng kết', title)`; `counts2.txt`: "7-05 | 61 | … | >60 dòng>20". Deck Bài 08 (`L08-7-08`) dùng tên mạch không số, đạt trần $60$. | Hoặc ghi ngoại lệ có lý do (năm hàng, tên mạch dài, tên phải trùng tiêu đề mạch), hoặc gộp hàng mạch 5 (một bài) vào hàng mạch 6 thành "5–6. Biến ẩn, cận dưới bằng chứng và tái tham số hóa" nếu điều phối viên chấp nhận tên gộp. Không rút chữ liên kết "Ghi chú bài giảng · Bài tập" (bắt buộc theo `CLAUDE.md`). Sửa con số "$61$/80" ở mục 9, 11, 15. |
| T10 | trung bình | ghi chú diễn giả 4-00, 3-00 | Mạch làm chủ ngữ (trái quy ước mục 6 của chính storyboard) và câu nói điều một phần chưa cho biết (quy tắc tác giả 2026-11-04). | 4-00: "Mạch 3 cho hàm lỗi của một chuỗi và cỡ mẫu trong cận, nhưng chưa cho biết rủi ro kì vọng nhỏ nhất bằng bao nhiêu"; 3-00: "Mạch trước cho ERM với hàm lỗi log". `CLAUDE.md` gốc: "No hedging about the text's own status … 'Ví dụ 09.1 chưa cho biết …'". | 4-00: "Rủi ro kì vọng phụ thuộc phân bố thật chưa biết. Tách nó thành …" (bỏ câu đầu). 3-00: "ERM với hàm lỗi log coi mỗi chuỗi là một quan sát. …" |
| T11 | trung bình | ghi chú diễn giả 3-01, 3-02, 4-02, 5-02, 5-05, 6-03 | Câu điều hướng chỉ vào dòng của trang (no-ai-slop: interpretive metadiscourse; giọng tác giả: cắt "như dòng thứ hai của bảng"). | "Dòng 'Trực quan.' đọc mệnh đề theo câu hỏi mở đầu" (3-01); "Dòng 'Trực quan.' đọc phần vượt của rủi ro" (4-02); "Dòng 'Trực quan.' đọc (a)" (5-02); "Dòng thứ hai của dãy dùng …" (5-05); "Dòng cuối nêu chỗ hỏng" (6-03); "cho đẳng thức của dòng 'Kỹ thuật.'" (3-02). | Nói thẳng nội dung: "Ba số $0{,}511$, $0{,}357$, $0{,}916$ là ba lần phân lớp …"; "Bất đẳng thức thứ hai dùng …"; "Nếu tập ngoại lệ phụ thuộc $\phi$, …". |
| T12 | trung bình | 7-02 dòng 1 | Dòng tổng kết bỏ điều kiện của Mệnh đề 09.8 (bài học deck 01, 02: dòng rút gọn ở bảng tổng kết giữ điều kiện). | "Học một phân bố: ERM với hàm lỗi log, $L_D=\mathrm H(p_D)+\mathrm{KL}(p_D\Vert p_\theta)$." Mệnh đề 09.8: "$\mathcal X$ đếm được", "$\mathrm H(p_D)<\infty$". | Thêm "khi $\mathrm H(p_D)<\infty$" (KaTeX, $+1$ âm tiết). |
| T13 | trung bình | 6-07 dòng 2 | Cận dưới $1{,}4189$ được gán cho bất đẳng thức hỗn hợp; ghi chú lấy nó từ Mệnh đề 09.8(c). | "Theo $p_{\theta_3}\ge0{,}01\,p_{\theta_1}$: $1{,}4189\le L_D(\theta_3)/p\le1{,}4249$". Ví dụ 09.13, Bước 2: "cũng là cận dưới của Mệnh đề 09.8(c)". | "Mệnh đề 09.8(c) và $p_{\theta_3}\ge0{,}01\,p_{\theta_1}$: $1{,}4189\le\ldots\le1{,}4249$". |
| T14 | trung bình | 6-08 dòng 4 | Câu hỏi (d) rút gọn đổi đối tượng: đề hỏi đại lượng $\mathbb EF(\bar w_T)-\min_\Phi F$ bằng kì vọng của KL nào, mặt trang hỏi "cận này". | Storyboard: "(d) $T=10^4$: tính $R$, độ dài bước, cận; cận này là kì vọng của KL nào?" `exercises.md` 09.7(d): "Đại lượng này bằng kì vọng của phân kì KL nào?" | "(d) $T=10^4$: tính $R$, $\eta$, cận; $\mathbb EF(\bar w_T)-\min F$ là kì vọng của KL nào?" |
| L1 | nhẹ | 2-03 dòng 3; ghi chú diễn giả 1-05 | "cần" thay cho "áp dụng khi", thiếu "mô hình rời rạc" (với mật độ cần chặn cả hai phía); 1-05 "và chỉ khi". | Ghi chú §2: "Các cận … áp dụng khi hàm lỗi bị chặn. Với mô hình rời rạc, điều này đúng khi các xác suất bị chặn dưới bởi $c>0$"; 1-05: "nên các cận dùng số chuỗi, và chỉ khi xác suất của mô hình bị chặn dưới". | 2-03: "Không bị chặn, trái (T3); cận Bài 02–04, 07 áp dụng khi mọi xác suất của mô hình rời rạc $\ge c>0$." 1-05: "… các cận dùng số chuỗi và cần xác suất của mô hình bị chặn dưới". |
| L2 | nhẹ | 2-03; 1-02 | $\hat\theta$ dùng ở (T7) trước khi định nghĩa ở 2-04; (T2), (T3) gọi tên mà chưa nhắc lại trên mặt trang. | 2-03: "$\hat\theta=\hat\theta(S)$ không phụ thuộc $V$"; 1-02 chỉ có "hàm lỗi trong $[0,1]$". | (T7): "mô hình được đánh giá $\hat\theta=\hat\theta(S)$ không phụ thuộc $V$" (như ghi chú). 1-02: "(T1), (T2), (T3): hàm lỗi trong $[0,1]$". |
| L3 | nhẹ | 2-01 | $\mathcal X$ trên mặt trang chưa định nghĩa. | "hàm xác suất (hoặc mật độ) trên $\mathcal X$"; ghi chú §1 mục 1: "Tập quan sát $\mathcal X$ là $\mathcal A^n$ … hoặc tập mọi chuỗi hữu hạn". | Dòng 1: "… $\mathcal X=\mathcal A^n$ hoặc mọi chuỗi hữu hạn". |
| L4 | nhẹ | 5-02 | (d) của Định lý 09.12, cầu nối với rủi ro thực nghiệm, chỉ ở ghi chú diễn giả; "Trực quan." vế sau lặp (b). | "ELBO lớn nhất khi $q$ là hậu nghiệm"; (b) "dấu bằng khi và chỉ khi $q=p_\theta(\cdot\mid x)$". | "**Trực quan.** Bằng chứng không phụ thuộc $q$: tăng ELBO theo $q$ là thu hẹp khoảng cách tới bằng chứng." (d) để ở ghi chú diễn giả là chấp nhận được; 5-05 dùng dạng tổng của (b). |
| L5 | nhẹ | 5-03 bước 4 | Dẫn Mệnh đề 09.8(b) (tập đếm được) cho hai mật độ trên $\mathcal V$. | Chứng minh Định lý 09.12, Bước 4: "Áp dụng lập luận ở Bước 3–4 của chứng minh Mệnh đề 09.8 cho hai mật độ". | "(lập luận của Mệnh đề 09.8(b), (c))". |
| L6 | nhẹ | 5-04 | Cột "Khe" của bảng đứng trước dòng định nghĩa khe. | Dòng 3 (bảng), dòng 4 "Khe (gap) $\ln p_\theta(2)-\operatorname{ELBO}=\ldots$". | Đưa dòng 4 lên ngay sau dòng 2. |
| L7 | nhẹ | 6-00 dòng dẫn | "nhiễu cố định" sai nghĩa: phân bố của nhiễu cố định, lần rút thì ngẫu nhiên. | "Viết lần rút thành hàm của một nhiễu cố định …"; Định nghĩa 09.14: "phân bố cố định, không phụ thuộc $\phi$". | "Viết lần rút thành hàm của một nhiễu có phân bố cố định đưa đạo hàm vào trong kì vọng, khi hàm khả vi và khả tích." |
| L8 | nhẹ | 1-03 mục 2 | Chữ viết tắt tiếng Anh "ERM" trên trang tổng quan (quy ước mục 6: "không tiếng Anh"); trang đã ở trần $80$. | "Viết ước lượng hợp lý cực đại thành ERM". | "Viết ước lượng hợp lý cực đại thành tối thiểu hóa rủi ro thực nghiệm"; cắt bù mục 5: "Dẫn ra gradient theo đường đi; nêu điều kiện không chệch và một trường hợp chệch." |
| L9 | nhẹ | ghi chú diễn giả 7-04 | Câu lạc chỗ và câu nguồn gốc. | "(1) Chuỗi đo hằng ngày; câu hỏi gốc hỏi thêm hàm lỗi log trung bình theo kí tự." | "(1) Theo Mệnh đề 09.3, …" (bỏ câu đầu; nếu muốn, thêm "hàm lỗi log trung bình theo kí tự" vào câu hỏi 1 trên mặt trang). |
| L10 | nhẹ | ghi chú diễn giả 2-00, 6-00, 7-00 | Câu điều hướng lộ trình (giọng tác giả: cắt navigation). | 2-00: "Trước hết cần nói rõ … Sau đó, …"; 6-00: "Cuối mạch, …"; 7-00: "sau đó là câu trả lời …, một bài tập …, câu hỏi tự kiểm tra và bài tập về nhà." | Giữ ý nội dung, bỏ phần liệt kê trình tự trang (7-00: chỉ giữ câu phân loại sáu kết quả). |
| L11 | nhẹ | 3-03; 3-05 | 3-03 mở khái niệm bằng định nghĩa; 3-05 dùng "DNA" mà chưa nêu bảng chữ trên mặt trang. | 3-03 dòng 1 "**Định nghĩa 09.4.** …"; 3-05: "DNA, $n=200$". | 3-03: mở bằng "Theo Mệnh đề 09.3(c), mỗi họ xác suất có điều kiện cho một mô hình." (bù bằng cắt ở mục 6). 3-05: "DNA trên $\{\mathtt A,\mathtt C,\mathtt G,\mathtt T\}$, $n=200$". |
| L12 | nhẹ | 6-02 (ii) | Thiếu "$\zeta\notin N_0$". | Mệnh đề 09.15(ii): "với mọi $\phi\in U$ và $\zeta\notin N_0$". | Thêm "$\zeta\notin N_0$" vào KaTeX (không tăng âm tiết). |
| L13 | nhẹ | dòng `note-source` | Phần lớn dòng nguồn không có mục UML, trong khi khuôn là "Nguồn: ghi chú Bài NN, §k; UML §x.y." | Ví dụ 2-04 "Nguồn: ghi chú Bài 09, §4, …" (UML §24.1, §24.1.2 có ở §13 của ghi chú). | Người viết thêm UML §24.1/§24.1.2 (mạch 2, 4), §24.1.3 (4-06), §24.4, §24.4.1 (mạch 5) ở các trang tương ứng. |
| L14 | nhẹ | 1-01 | Luận điểm $47$ âm tiết gói ba khẳng định độc lập trong một câu (giọng tác giả: padding). | "Với hàm lỗi log, ước lượng hợp lý cực đại là tối thiểu hóa rủi ro thực nghiệm, ở mức tổng thể chọn mô hình …, và khi các chuỗi được rút độc lập, cỡ mẫu là số chuỗi." | Ý kiến: rút còn hai ý, ví dụ "Với hàm lỗi log, ước lượng hợp lý cực đại là tối thiểu hóa rủi ro thực nghiệm, và khi các chuỗi được rút độc lập, cỡ mẫu là số chuỗi."; ý KL vào ghi chú diễn giả. Điều phối viên quyết định. |
| L15 | nhẹ | 6-08 | $\bar w_T$, $T$ dùng trong "Nhắc lại:" mà chưa nêu nghĩa. | "$\mathbb EF(\bar w_T)$". | "$\bar w_T$: trung bình $T$ điểm lặp" (gộp vào dòng N2). |

## 6. Cắt cụ thể để hạ trung vị

Số ước bằng cách đếm của `count.py`; người viết deck đếm lại bằng `deck_lint.py`. Mọi câu cắt chuyển vào ghi chú diễn giả của chính trang đó (ghi chú diễn giả các trang này còn dưới $150$).

| Trang | Hiện | Cắt | Ước sau |
|---|---:|---|---:|
| 3-02 | 54 | bước 4 → "(mỗi hàng tổng $1$) Lấy tổng theo kí tự cuối, quy nạp từ $j=n$: (c)." (dòng "Kỹ thuật." đã có công thức) | 48 |
| 3-03 | 55 | dòng "Học theo đáp án (teacher forcing): …" vào ghi chú diễn giả (thuật ngữ không dùng lại trên mặt trang) | 45 (55 nếu thêm dòng mở L11) |
| 3-04 | 51 | lời giải (c) → "… $=0{,}40\ne0{,}69$: không độc lập." | 45 |
| 3-08 | 52 | dòng cuối → "Điểm cực tiểu: $\tfrac16$ (hàm lỗi tổng), $\tfrac12$ (chuẩn hóa)." | 47 |
| 4-01 | 52 | dòng entropy vi phân bỏ vế "có thể âm: đều trên $[0,\tfrac12]$ cho $-\ln2$" (4-02 ghi chú diễn giả đã nói $\mathrm h$ có thể âm) | 45 |
| 4-07 | 53 | dòng "$m=500$: … dao động của tập kiểm tra" vào ghi chú diễn giả | 38 |
| 5-01 | 54 | dòng hậu nghiệm → "Hậu nghiệm $N(\tfrac x2,\tfrac12)=N(1,\tfrac12)$." (cách đọc vào ghi chú diễn giả, đã có) | 44 |
| 6-01 | 57 | dòng 1 → "$\nabla F$ nói chung khác $\mathbb E_{v\sim q_\phi}\nabla_\phi f(v)=0$: phân bố phụ thuộc $\phi$." ("SGD trên ELBO" đã ở 6-00) | 51 |
| 6-06 | 54 | bỏ dòng "Khả vi tại từng $\mu$ cho hầu hết $\zeta$ chưa đủ." (lặp dòng trên; ghi chú diễn giả đã có) | 45 |
| 5-05 | 60 | nếu theo T4 (trang ý tưởng chứng minh riêng): dãy và dòng "Chứng minh." sang trang mới | ≈45 |

Các thêm bắt buộc: T1 (3-01, $\approx+6$ sau cắt bù), T5 (3-06, $\approx+0$), T7 (7-03, $\approx+0$), N2 (6-08, $\approx+8$, cắt bù "mô phỏng"), N1, T12 (7-02, $\approx+5$). Sau các cắt có khoảng $20$–$21$ trên $42$ trang nội dung $\le50$, nên trung vị $\approx50$–$51$, như mức Bài 06–08.

**Trang chép ghi chú nhiều nhất.** 5-01 (Định nghĩa 09.10 đủ năm thành phần cộng Ví dụ 09.9), 6-01 (Định nghĩa 09.14 đủ bốn thành phần), 4-01 (Định nghĩa 09.7 cộng ba đoạn sau), 2-03 (ba gạch đầu dòng của §2 gần nguyên văn) và 3-08 (ba khối). 5-01 và 4-01 giảm theo bảng trên; 6-01 chấp nhận được vì 6-02, 6-05, 6-06 dùng cả bốn thành phần. Ghi chú diễn giả của 1-06, 2-02, 2-04, 4-04, 4-05 chép nguyên câu của ghi chú (ví dụ 2-02: "Các chuỗi ba kí tự của câu hỏi mở đầu, rút độc lập, thuộc Thiết lập A; phản ví dụ là …", ghi chú dòng 114); không trái quy định, nhưng phần giải thích riêng của deck ở các trang này mỏng. Deck chỉ có hai hình (F1, F2); không đề xuất thêm hình mới ở bước này.

## 7. Đề xuất sửa ghi chú (bổ sung mục 13 của storyboard)

| Mức độ | Vị trí | Vấn đề | Đề xuất |
|---|---|---|---|
| nhẹ | mục 13 storyboard, ba hàng | Đã kiểm: (1) $1{,}122-1{,}091=0{,}031$ từ bảng, $0{,}0316$ là trung bình hiệu theo hạt giống (`exercises.md` 09.6, "Kiểm tra lại"); (2) Bài tập 09.7(d) dùng Hệ quả 05.15 mà Kiến thức tiên quyết chỉ nêu Định lý 05.14; (3) lời giải 09.4(b) dùng $\rho_0$ chỉ đặt tên ở Gợi ý 2 (`exercises.md` dòng 366). | Đồng ý cả ba. |
| nhẹ | ghi chú, Ví dụ 09.13, Bước 2 | Không sai; deck nên giữ đúng nguồn của cận dưới (T13). | — |

## 8. Kiểm liên tục (bảng kiểm Outline/Threads/Concept của quill)

- **Thứ tự khái niệm.** Bảy mạch ứng với §1–§4, §5–§6, §7, §8, §9, §10–§13 liên tiếp. Lệch nhỏ có lý do: Ví dụ 09.1 (§3) lên trang Định nghĩa 09.1 (§1); Nhận xét 09.5 (cuối §5) sang 3-08 (§6); Phụ lục D vào 3-02, 5-05; Phụ lục B vào 6-03.
- **Hành trình khái niệm.** Đủ bước cho Mệnh đề 09.3, 09.8, Định lý 09.12, Mệnh đề 09.15 (ví dụ của 09.15 đứng sau phát biểu, có lý do, theo tiền lệ T5 Bài 04). Hệ quả 09.13 thiếu trang ý tưởng chứng minh (T4). 3-03 mở bằng định nghĩa (L11).
- **Mạch và dòng dẫn.** Năm dòng dẫn là câu trần thuật, $\le25$ âm tiết, không "Nhu cầu:", không "Muốn …", không mở bằng "Người học"; 6-00 sai một chữ (L7). Câu nối giữa các mạch có trên mặt trang: 2→3 (3-01 dòng 1), 3→4 (4-01 dòng 1), 4→5 (5-01 dòng 1), 5→6 (6-01 dòng 1), 6→7 (6-07 "Kết luận:").
- **Thuật ngữ.** Khớp `thuat-ngu.md` và bảng mục 10 ("mô hình ghi nhớ" theo "thuật toán ghi nhớ"; "khe", "nhiễu phụ", "hàm trội", "học theo đáp án"). Ý in đậm của ghi chú "quá khớp" có trên mặt trang 4-07; "rò rỉ thông tin", "cửa sổ chồng lấn", "khối lượng điểm" (chỉ ghi chú diễn giả) đúng tên.
- **Kí hiệu chưa có nghĩa trên mặt trang:** $\mathcal X$ (L3), $\hat\theta$ ở 2-03 (L2), (T2), (T3) (L2), $\bar w_T$ (L15), $\operatorname{ELBO}(\theta,q;x)$ ở 5-05 (chấp nhận: $q_i$ định nghĩa ở dòng bước E cùng trang).
- **Kỹ thuật.** Bốn kỹ thuật mới đúng chỗ dùng đầu tiên; "Đổi chỗ đạo hàm và kì vọng" là kỹ thuật dùng lại duy nhất, có trang riêng; chỗ dẫn Bài 10 cần sửa (T6); "Đảo cận đuôi" của Bài 02 cần dòng "Nhắc lại:" (T5).
- **Quyết định của tác giả 2026-11-14 (hàng 1–5).** Tuân thủ: tiêu đề tiếng Việt tự nhiên với tiền tố chức năng; mạch cuối "Tổng kết"; "Vấn đề trung tâm" mở đầu một hộp, câu trả lời ở ghi chú diễn giả, trang kết luận cùng tên; không "Nhu cầu:"; trang mở ví dụ (1-06, 2-05, 3-07, 4-06) nêu dữ kiện ngay.
- **Không dẫn trang sau hay bài sau trên mặt trang.** Đạt; Bài 10 chỉ ở dòng chữ trang cuối 7-06.
