# Duyệt cổng storyboard — bộ trang chiếu Bài 07

Người duyệt cổng (chỉ đọc), 2026-11-15. Đối tượng: `planning/lec-07/storyboard.md` (toàn bộ, mục 1–15). Đối chiếu: `materials/lec-07/lecture-note.md`, `materials/lec-07/exercises.md`, `CLAUDE.md` § Slide decks, `deck-build/common-brief.md` (gồm "Các quy định dễ sót" và các bài học deck 01–05), `deck-build/brief-gate.md`, `deck-build/deck_lint.py` (bản 2026-11-16: chữ trong ô bảng có tính, số trong bảng và KaTeX không tính), mục "Bộ trang chiếu" của `lec-05/review-log.md`, `lec-06/review-log.md`, mục 14 của `lec-06/storyboard.md`, deck đã xuất bản `lecture-0{1..6}-*.html` (ID `L01-4-04`, `L03-5-06`, `L04-4-04` có thật; khuôn trang ý tưởng chứng minh `L06-4-04`), ghi chú Bài 02 (Hệ quả 02.10, Định lý 02.14), Bài 03 (Định lý 03.15, Nhận xét 03.10, Ví dụ 03.3, 03.8), Bài 04 (Mệnh đề 04.3, Bổ đề 04.9), Bài 05 (Ví dụ 05.10), Bài 06 (Ví dụ 06.7), Bài 08–10 (dùng lại kết quả Bài 07). `no-ai-slop` chế độ Detect đã nạp.

Script độc lập trong thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-07/gate/`: `num.py` (tính lại V1–V23, liệt kê bộ dấu và nhãn, kiểm F1 trên lưới, vét cạn lớp afin), `exp.py` (chạy lại thí nghiệm Phụ lục D, mười hạt giống), `mycount.py` (âm tiết mặt trang theo quy ước 2026-11-16). Không dùng script của người lập storyboard để tính; chỉ chạy `num.py` của họ để đối chiếu.

## Kết luận

**Đạt khi sửa.** 0 chặn bàn giao, 2 nghiêm trọng, 10 trung bình, 18 nhẹ.

Mọi con số V1–V23 tính lại độc lập khớp storyboard, ghi chú và tệp bài tập; chạy lại Phụ lục D cho đúng mọi số đo của thí nghiệm. Phát biểu của Mệnh đề 07.2, 07.9, 07.13, Định lý 07.11, Hệ quả 07.16, Bổ đề 07.10, 07.14 trên mặt trang khớp ghi chú (giả thiết, loại bảo đảm, hằng số $2$, $3$, $2BC_x/(\gamma\sqrt m)$, thực nghiệm so với kì vọng). Không trang nào chuyển kết quả lồi sang mạng nơ-ron. Hai phát hiện nghiêm trọng: (N1) theo quy ước đếm mới, ba trang bảng vượt trần ngay trên storyboard (1-06 ≈ 82, 2-06 ≈ 68, 7-01 ≈ 82/80); (N2) trang Nhận xét 07.18 (6-06) bỏ điều kiện quan sát độc lập cùng phân bố, giấu thừa số $\ln\bar N$ mà ghi chú viết ra, nói "cận không chứa số tham số" mạnh hơn ghi chú ("ngoài thừa số logarit") và dùng $r_j$ chưa định nghĩa trên mặt trang.

## 1. Tính lại số

| Mục | Kết quả tính lại | Khớp |
|---|---|---|
| V2 câu ôn | $\mathbb E\lvert\sigma_1+\sigma_2+\sigma_3\rvert=3/2$; $\sqrt3=1{,}73205$; $t=\sqrt{\ln40/400}=0{,}096032$ | có |
| V3, V4, F1 | lớp afin: vét cạn lưới $61^3$ cho ít nhất $1$ lỗi; $w=(1,1)$, $b=-\tfrac12$: $-\tfrac12;\tfrac12;\tfrac12;\tfrac32$; Mệnh đề 07.2: $-\tfrac12;\tfrac12;\tfrac12;-\tfrac12$, $f_\theta(\tfrac12,\tfrac12)=\tfrac12$; miền $f_\theta\ge0$ trùng dải $\tfrac12\le s\le\tfrac32$ trên lưới $351^2$ của $[-0{,}25;1{,}5]^2$; $9$ tham số | có |
| V5 (Bài tập 07.5(c)) | $F(\theta)=F(\theta_{\mathrm{swap}})=0$; $f_{\theta_{\mathrm{mid}}}=-\tfrac12;-1;-1;-2$; $F(\theta_{\mathrm{mid}})=27/16$; trung điểm sai $2/4$ | có |
| V6 | tổng bình phương $10{,}25$; $500{,}30$ ($c=10$, $0{,}1$); căn $3{,}2016$; $22{,}3674$; tích chuẩn phổ $4{,}47214$ với mọi $c$; hàm điểm số không đổi | có |
| V7, V16 | $\sqrt{8\ln2}=2{,}3548$; $\sqrt{16\ln2}=3{,}3302$; $6000$ | có |
| V8, V9 | Ví dụ 07.4: giá trị lớn nhất $-1,0,0,2,1,1,1,2$ (tổng $6$), $0,1,0,2,0,1,1,3$ ($8$), $\{0,1\}^3$ tổng $12$; $0,\tfrac14,\tfrac13,\tfrac12$; kiểm Mệnh đề 07.9(a) cho ba lớp $0$–$1$: $\tfrac12-\mathbb E_\tau\min\operatorname{err}_\tau$ trùng; bảng Bài tập 07.2(c) $1,2,2,3,0,1,1,2$ / $2,1,1,0,3,2,2,1$; công thức hai véc-tơ cho $1{,}5/6=\tfrac14$ | có |
| V11, V12 | $0{,}288097$; $0{,}081486$; $0{,}040743$; $1{,}288097$; $\sqrt{\ln20/400}=0{,}086541$; tỉ số $3{,}329$ | có |
| V13, V14 | $\mathbb E\lvert\sigma_1+\sigma_2\rvert=1$; $0{,}70711$; $\lVert v_\sigma\rVert=2$ với mọi $\sigma\in\{\pm1\}^4$; bản trị tuyệt đối $\tfrac12$ | có |
| V16 | $0{,}2$; $0{,}2408$; $4{,}074305$; $57\,957{,}21\to57\,958$; $231\,828{,}86\to231\,829$; $3689{,}72\to3690$ (kiểm lại: số hạng phạt tại các cỡ mẫu này $\le\epsilon$) | có |
| V17, V21 | $q_1=\tfrac12$; $3\sqrt{\ln80/5000}=0{,}088812$; $0{,}16$; $0{,}2815$; $0{,}2889$; $\sum q_k\to1$ | có |
| V18 + Phụ lục D | chạy lại `exp.py` theo đúng thứ tự rút: lỗi kiểm tra $0{,}02298$ (sd $0{,}0074$, $0{,}014$–$0{,}0364$) và $0{,}5011$ ($0{,}480$–$0{,}512$); lỗi huấn luyện $0$; hạng $200$; lề nhỏ nhất $1$; $C_x$ $1{,}518$–$1{,}544$; $\lVert\hat w\rVert$ $915{,}7$ ($351{,}5$–$1721$) và $10\,850$ ($6792$–$14\,052$); lề chuẩn hóa $3{,}80\cdot10^{-4}$–$1{,}875\cdot10^{-3}$ và $4{,}64\cdot10^{-5}$–$9{,}64\cdot10^{-5}$; số hạng Rademacher $75{,}4$–$371{,}7$ và $1467$–$3047$; chuẩn $\Theta_2$ $20{,}47$, $242{,}67$; bán kính kiểm tra $0{,}019206$ | có |
| V19, V20 | $10^{-8}$; $\ln80=4{,}38203$; $0{,}8147$; $0{,}2576$; $0{,}0815$; $25{,}7625$; $66\,371$; $2\cdot0{,}25762=0{,}5152$ | có |
| V22 | $r_m=\sqrt{\ln120/400}=0{,}109402$; một phía $0{,}101172$; $P/m=5000$, $0{,}005$ | có |
| Ghi chú diễn giả 7-07 | $4\sqrt{2\ln80/10^4}=0{,}11842\to0{,}1185$ | có |
| F2, F3 | điểm đặc/rỗng của $\mathbb 1[t\le0]$ tại $0$ và $\mathbb 1[t<\gamma]$ tại $\gamma$ đúng; trục lôgarit $100$–$20\,000$ chứa $351$–$14\,052$ | có |

## 2. Phát biểu đối chiếu ghi chú

| Khối | Trang | Kết quả |
|---|---|---|
| Mệnh đề 07.2 | 2-04 | khớp (kiến trúc, tham số, "tất định, chỉ về bốn điểm") |
| Bổ đề 07.8 | 3-02 | khớp đẳng thức; thiếu "$A$ khác rỗng, bị chặn" và hai nhãn Giả thiết/Bảo đảm (L6) |
| Mệnh đề 07.9 | 3-03 | khớp (a)–(c), tất định, kì vọng theo $\tau$ hay $\sigma$; "cho phép lặp" ở ghi chú diễn giả |
| Bổ đề 07.10 | 4-01 | khớp ($V_i$ độc lập, không cần cùng phân bố; $Q$ đo được; mọi $t>0$; cả hai đuôi) |
| Định lý 07.11 | 4-02, 4-03, 7-01 | khớp: (a) theo kì vọng với $\mathfrak R_m$, (b) với xác suất ít nhất $1-\delta$, $\widehat{\mathfrak R}_S$, hằng số $2$ và $3$, đồng thời cho mọi $g$; lộ trình đúng thứ tự giả thiết vào bước |
| Mệnh đề 07.13 | 5-01, 5-02 | khớp; 7-01 và 5-06 viết $\widehat{\mathfrak R}(\mathcal F_B)$ thay cho $\widehat{\mathfrak R}_{x_{1:m}}(\mathcal F_B)$ (L7); "bất đẳng thức duy nhất" ở Bước 2 không đúng cho cận thứ hai (L8) |
| Bổ đề 07.14 | 5-03 | khớp ($G$-Lipschitz trên tập chứa $\{a_i\}$, tất định, không cần định tâm) |
| Hệ quả 07.16 | 5-05, 5-06 | khớp (chuỗi hai bất đẳng thức, $B$, $\gamma$ chọn trước, cấp lớp) |
| Nhận xét 07.6 | ghi chú diễn giả 2-11 | khớp, có "đọc thêm" |
| Nhận xét 07.17 | 6-02 | khớp |
| Nhận xét 07.18 | 6-06 | **không khớp** (N2) |

## 3. Bảng phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | 1-06, 2-06, 7-01 (và 6-03 sát trần) | N1. Theo quy ước đếm 2026-11-16, ba trang bảng vượt trần ngay trong storyboard; mục 11 điểm 13 đề nghị đếm theo cách bỏ bảng, nay không còn áp dụng | `deck_lint.py` dòng 1–4: "words in tables count"; storyboard mục 15: 1-06 $59+34$, 2-06 $38+35$, 7-01 $6+81$/80; đếm độc lập: 1-06 ≈ 82, 2-06 ≈ 68, 7-01 ≈ 82; 6-03 ≈ 38 + chú thích hình 18 = 56 | cắt cụ thể ở mục 5 (1-06 còn ≈ 58, 2-06 ≈ 58, 7-01 ≈ 70, 6-03 ≈ 45); người viết deck chạy `deck_lint.py` sau mỗi đợt |
| nghiêm trọng | 6-06 | N2. Phát biểu Nhận xét 07.18 khác ghi chú: bỏ "với quan sát độc lập cùng phân bố"; đổi $\lVert X\rVert_2R_\Theta\ln\bar N/(\gamma m)$ thành $C_xR_\Theta/(\gamma\sqrt m)$ và giấu $\ln\bar N$ vào $\tilde O$ (ghi chú diễn giả: "$\tilde O$ ẩn thêm thừa số $\ln\bar N$"); "cận không chứa số tham số" trong khi ghi chú viết "Ngoài thừa số logarit, cận không phụ thuộc số tham số"; $r_j$, $M_j$ trong $R_\Theta$ và $\mu_\Theta$, $\hat y_\Theta$ chỉ được nêu tên | ghi chú §9, Nhận xét 07.18, gạch "Cận" ("Với quan sát độc lập cùng phân bố …") và đoạn "Khi $\lVert x_i\rVert\le C_x$ … có dạng $C_xR_\Theta\ln\bar N/(\gamma\sqrt m)$"; storyboard 6-06 dòng 3–5; mục 11 điểm 20 | Mặt trang: "Với quan sát độc lập cùng phân bố, với xác suất ít nhất $1-\delta$, …"; công thức giữ $\ln\bar N$: $\tilde O\big(C_xR_\Theta\ln\bar N/(\gamma\sqrt m)+\sqrt{\ln(1/\delta)/m}\big)$, với "$\bar N$: số lớn nhất trong $p$, số nhãn và các độ rộng"; dòng cuối "ngoài thừa số lôgarit, cận không phụ thuộc số tham số"; $R_\Theta$ viết bằng lời ("tích các chuẩn phổ nhân một thừa số theo chuẩn nhóm của $\Theta_j-M_j$, $M_j$ cố định trước"), công thức đầy đủ vào ghi chú diễn giả; bù chữ bằng chuyển "Chứng minh nằm ngoài phạm vi học phần" vào ghi chú diễn giả (mục 11 điểm 20 đã cho phép) |
| trung bình | toàn deck | T1. Trung vị $55$, 15 trang ≥ $57$ (1-02, 1-06, 2-06, 2-08, 2-09, 3-01, 3-03, 4-02, 4-05, 5-07, 6-02, 6-06, 7-01, 7-02, 7-04): không còn biên cho người sửa sau năm báo cáo duyệt (quyết định Bài 06: "cắt trước … còn biên sửa") | storyboard mục 15; `lec-06/review-log.md` § Bộ trang chiếu, dòng "Mật độ: 15 trang 57–59" | áp dụng các cắt ở mục 5 trước khi viết deck; mục tiêu mọi trang nội dung ≤ 55, trung vị ≈ 50 |
| trung bình | 2-01, 2-03, 3-03, 5-04, 6-05 | T2. Chép ghi chú: 2-01 chép thiết lập tám thành phần §1; 2-03 chép đủ Định nghĩa 07.1 cùng ba ví dụ; 3-03 chép đủ sáu dòng Mệnh đề 07.9; 5-04 chép bốn thành phần của Định nghĩa 07.15 cùng ba tính chất và lề chuẩn hóa; 6-05 chép Bước 1–4 của Ví dụ 07.11 thành năm dòng | storyboard 2-01, 2-03, 3-03, 5-04, 6-05 so với ghi chú §1, Định nghĩa 07.1, Mệnh đề 07.9, Định nghĩa 07.15 với (i)–(iii), Ví dụ 07.11 | 2-03: bỏ ví dụ $\mathbb 1[x\in\mathbb Q]$ khỏi mặt trang (ghi chú diễn giả). 5-04: dòng lề chuẩn hóa chuyển sang 6-03, nơi nó được dùng. 6-05: giữ Bước 2–3 (lớp phân lớp không nhỏ đi; chỗ lập luận hỏng) và một dòng hàm lỗi logistic; Bước 1 gộp vào dòng dữ kiện. Các cắt cụ thể ở mục 5 |
| trung bình | 4-01 | T3. "Trực quan." nhắc lại giả thiết sai phân bị chặn và trường hợp riêng, không nêu cơ chế (bài học deck 02). Đây cũng là chỗ duy nhất có thể đưa ý tưởng chứng minh của bất đẳng thức McDiarmid lên mặt trang mà không thêm trang | storyboard 4-01: "**Trực quan.** Không biến nào đổi $Q$ quá $c_i$; trung bình trong $[a,b]$ có $c_i=(b-a)/m$"; common-brief: "Trực quan." nêu cơ chế, không nhắc lại phát biểu | "**Trực quan.** Khi lần lượt biết $V_1,V_2,\ldots$, mỗi bước làm kì vọng có điều kiện của $Q$ dịch đi trong một đoạn dài không quá $c_i$; bổ đề Hoeffding chặn từng bước như một biến bị chặn." Trường hợp riêng Định lý 02.7 giữ một vế ngắn hoặc vào ghi chú diễn giả |
| trung bình | 2-05, F1, 7-06 | T4. Trang ý tưởng chứng minh và hình F1 cho sẵn lời giải nửa đầu Bài tập 07.1(c) (miền dải $\tfrac12\le x_1+x_2\le\tfrac32$), trong khi 7-06 giao Bài tập 07.1 về nhà | `exercises.md`, Lời giải 07.1(c), Bước 2: "$f_\theta(x)\ge0$ khi và chỉ khi $\tfrac12\le x_1+x_2\le\tfrac32$"; storyboard 2-05 dòng 4, mục 8 F1, mục 11 điểm 8 | Chọn một: (a) giữ F1 và ghi ở 7-06 rằng 07.1(c) phần $\theta$ đã chữa trên lớp, phần $\theta_{\mathrm{II}}$ làm ở nhà; (b) bỏ dòng miền và hình, giữ điểm $(\tfrac12,\tfrac12)$ theo đoạn sau Mệnh đề 07.2 (trang còn ≈ 27 âm tiết, có biên). Ý kiến: (a), vì F1 là trực quan duy nhất cho "hai biên tuyến tính" |
| trung bình | 7-01 | T5. Cột "Giả thiết không được bỏ" của Mệnh đề 07.2 ghi "hai nơ-ron ẩn, ReLU": ghi chú không chứng minh một nơ-ron ẩn là không đủ; đối chiếu có cơ sở chỉ là lớp afin ($J=1$) | ghi chú, Mệnh đề 07.2 và câu "Với $J=1$, $h_\theta=h_{w,b}$"; Ví dụ 07.1, Bước 1; storyboard mục 4 hàng Mệnh đề 07.2: "Bỏ hàm kích hoạt phi tuyến: không có trong ghi chú" | "$J=2$, ReLU; chỉ bốn điểm của $\{0,1\}^2$ (với $J=1$: lớp afin sai một quan sát)" |
| trung bình | 2-11 → 3-01 | T6. Câu nối mạch 2 → 3 thiếu "cái còn thiếu" trên mặt trang: đại lượng cho lớp hàm giá trị thực (lớp hàm điểm số, lớp hàm lỗi) và nhỏ đi khi bị chặn theo chuẩn chỉ nằm ở ghi chú diễn giả 3-00 (bài học deck 01) | ghi chú, câu cuối §5 "Chúng ta cần một đại lượng xác định cho cả lớp hàm giá trị thực …"; storyboard 2-11 Diễn giải, 3-00, 3-01 dòng 1; mục 11 điểm 14 | Thay dòng "Nhắc lại:" của 3-01 bằng: "Chiều VC đếm cách gán nhãn; lớp hàm điểm số và lớp hàm lỗi cần đại lượng cho hàm giá trị thực." (≈ 18, cắt bù ở mục 5) |
| trung bình | 7-02 | T7. Trang "Vấn đề trung tâm" không có dòng trả lời thẳng câu hỏi "đại lượng nào …"; câu trả lời chỉ ở ghi chú diễn giả | storyboard 7-02, ghi chú diễn giả: "Đại lượng đo được năng lực thống kê … là độ phức tạp Rademacher của một lớp chứa hàm do huấn luyện chọn"; CLAUDE.md: hộp mở đầu "answered by the closing Vấn đề trung tâm slide" | Dòng đầu mặt trang: "Độ phức tạp Rademacher của lớp chứa mô hình do huấn luyện chọn; với lớp tuyến tính, tỉ số $BC_x/\gamma$." Gộp dòng 1 và 3 hiện có để giữ ≤ 4 dòng, ≤ 55 âm tiết |
| trung bình | 2-05, 3-04, 4-03, 5-02, 5-06 | T8. Quy ước "**Bước 1 …**" in đậm có dấu chấm sẽ bị `deck_lint.py` báo LABEL (chỉ miễn "Định nghĩa/…/Bài tập + số"); deck 06 dùng `ol` với giả thiết trong ngoặc đầu mục | `deck_lint.py`, vòng `for lab in re.findall(r'<strong>([^<]{1,40}?[.:])</strong>'…`; `lecture-06-on-dinh-chinh-quy-hoa.html`, `L06-4-04`: `<ol><li>($Z'$ độc lập; định lý Fubini) …`; storyboard mục 6, quy ước chung gạch 4 | Dùng `ol` như `L06-4-04`: "<li>((T1), (T5)) Mẫu bóng …</li>"; "(a)", "(b)" in đậm không dấu chấm giữ được |
| trung bình | 1-01 | T9. Luận điểm bìa 65 âm tiết, một câu hai vế nối bằng dấu chấm phẩy; vế giữa ("bằng một nửa cho lớp kiến trúc …") là một số liệu, không phải luận điểm. Bản 44 âm tiết (mục 11 điểm 10) đúng và có điều kiện, nhưng không trả lời "đại lượng nào" của câu hỏi trung tâm | storyboard mục 2; mục 11 điểm 10; bài học deck 05: "Luận điểm bìa đúng một câu, có điều kiện" | Ý kiến ở mục 4, điểm 10 (đề xuất bản 47 âm tiết, không dấu chấm phẩy) |
| trung bình | 2-09 | T10. Trang mở bằng "**Định nghĩa 07.5.**" (bảng kiểm cổng, mục 3: không mở khái niệm bằng định nghĩa); câu vấn đề của ghi chú nằm ở ghi chú diễn giả | ghi chú §5: "Một bảo đảm học có thể nói về một lớp hay về riêng hàm mà phép huấn luyện chọn."; storyboard mục 11 điểm 12 | Thêm dòng mở "Một bảo đảm nói về một lớp hoặc về riêng hàm do huấn luyện chọn." (13); bù bằng bỏ "(lỗi của Ví dụ 03.8)" (ghi chú diễn giả) và gộp dòng 4–5: "Bảo đảm cấp lớp (class-level) đúng cho $h_{\hat\theta}$ khi $\lVert\hat\theta\rVert\le B$; $B=\lVert\hat\theta\rVert$ phụ thuộc $S$." |
| nhẹ | 2-06 | L1. Nhận xét 07.3 bỏ miền giá trị: ghi chú "mọi hàm Lipschitz từ $[-1,1]^p$ vào $[-1,1]$" | ghi chú Nhận xét 07.3; storyboard 2-06 dòng 1–2 | viết $[-1,1]^p\to[-1,1]$ trong KaTeX (0 âm tiết) |
| nhẹ | 2-10 | L2. Ghi chú diễn giả "Ba chuẩn $\sqrt{10{,}25}\approx3{,}20$ và $\sqrt{500{,}30}\approx22{,}37$" liệt kê hai chuẩn | storyboard 2-10, ghi chú diễn giả câu 4 | "Hai chuẩn …" |
| nhẹ | 4-03 ghi chú diễn giả, 7-01 ghi chú diễn giả | L3. "Bỏ (T3): lớp điểm số không bị chặn trong $[0,1]$" không nói bước nào hỏng; Bài tập 07.4(d) nêu Bước 3 ($c_i=1/m$) | `exercises.md`, Lời giải 07.4(d), gạch "Giá trị trong $[0,1]$" | "Bỏ (T3): Bước 3 hỏng vì sai phân không còn ≤ $1/m$; ví dụ hàm lỗi logistic trên $\mathbb R^p$" |
| nhẹ | 4-03 | L4. Bước 3 dùng mẫu thay một điểm $s^{(i)}$ "như Bài 06"; storyboard Bài 06 mục 14 ghi "Deck Bài 07 trở đi nhắc lại 'lập luận đổi vai' bằng tên"; storyboard Bài 07 mục 14 ghi "không dùng" | ghi chú, chứng minh Định lý 07.11, Bước 3: "(như Bài 06)"; `lec-06/storyboard.md` mục 14, câu cuối | ghi chú diễn giả 4-03 một câu: "Mẫu $s^{(i)}$ là mẫu lân cận của Bài 06 (Định nghĩa 06.9); ở đây chỉ cần thay một điểm, không cần đổi vai." Sửa dòng mục 14 cho khớp |
| nhẹ | 5-02, mục 4 | L5. "bất đẳng thức duy nhất" ở Bước 2: Bước 4 ($\lVert x_i\rVert\le C_x$) cũng là bất đẳng thức | ghi chú, chứng minh Mệnh đề 07.13, Bước 4 | "bất đẳng thức duy nhất của cận thứ nhất", hoặc bỏ cụm |
| nhẹ | 3-02 | L6. Bổ đề 07.8 không có "Giả thiết:"/"Bảo đảm:" và bỏ "$A$ khác rỗng, bị chặn"; trên trang, bổ đề đứng sau ví dụ, ngược thứ tự ghi chú | ghi chú, Bổ đề 07.8 đứng trước Ví dụ 07.4; common-brief "Phát biểu kết quả trên trang dùng hai nhãn" | "**Bổ đề 07.8.** **Giả thiết:** $A$ như trên, $c\in\mathbb R$, $\bar a\in\mathbb R^m$. **Bảo đảm:** tất định, …"; đặt bổ đề ở dòng 1 hoặc giữ cuối và ghi lý do |
| nhẹ | 5-06, 7-01 | L7. $\widehat{\mathfrak R}(\mathcal F_B)$ là kí hiệu của tập véc-tơ, không của lớp hàm | Định nghĩa 07.7; Hệ quả 07.16, chứng minh Bước 2: $\widehat{\mathfrak R}_{x_{1:m}}(\mathcal F_B)$ | viết $\widehat{\mathfrak R}_S(\mathcal F_B)$ (quy ước của ghi chú cho lớp điểm số) |
| nhẹ | 6-05, 7-04 | L8. $K$ hai nghĩa trên mặt trang ($\ln(1+e^{BC_x})$ và số hàm $3$) | storyboard mục 11 điểm 21 | 7-04 không đặt tên: "(T4) với ba hàm, $r_m=\sqrt{\ln(2\cdot3/\delta)/(2m)}=\sqrt{\ln120/400}\le0{,}1095$"; ghi chú diễn giả 7-04 dẫn $K=3$ của Định lý 02.14. Đề xuất cho tác giả ở mục 13 giữ |
| nhẹ | 6-02 | L9. Từ khóa mạch "lưới lề" không có trên mặt trang nào ("lưới" chỉ xuất hiện ở 6-04 cho $B_k$) | storyboard 6-00 `strand-keys`; 6-02 mặt trang | 6-02: "lưới $\gamma_k=2^{-k}$, trọng số $q_k=\ldots$" |
| nhẹ | 6-02 | L10. "vi phạm Hệ quả 07.16" — vi phạm giả thiết, không vi phạm kết quả | ghi chú Nhận xét 07.17: "vi phạm giả thiết bán kính và lề chọn trước khi lấy mẫu" | "trái giả thiết chọn trước của Hệ quả 07.16" |
| nhẹ | 6-05 | L11. "Hàm lỗi logistic, $\lVert w\rVert\le B$: trong $[0,K]$" thiếu $\lVert x\rVert\le C_x$ | ghi chú Ví dụ 07.11, Bước 4 | "$\lVert w\rVert\le B$, $\lVert x\rVert\le C_x$" (KaTeX) |
| nhẹ | 1-06 | L12. $f$ trong "$f(x_i)=2y_i-1$" chưa có trên mặt trang | storyboard 1-06 dòng 3; $f$ chỉ ở ghi chú diễn giả | "hàm điểm số $f$ của mạng" hoặc dạng gộp ở mục 5 |
| nhẹ | 2-01 | L13. (M) chỉ là nhãn trên mặt trang (1-02 và 2-01), chưa có nghĩa | storyboard 1-02, 2-01 dòng 5 | "(M) lớp con đếm được" |
| nhẹ | 3-06 | L14. "Hai hàm sai trung bình $\tfrac14$" dễ hiểu thành mỗi hàm sai $\tfrac14$ | `exercises.md` Lời giải 07.2(c), Bước 3: "Hai hàm khớp nhãn ngẫu nhiên với lỗi trung bình $\tfrac14$" | "Lớp hai hàm có lỗi nhỏ nhất trung bình $\tfrac14$; một hàm cố định sai $\tfrac12$" |
| nhẹ | 3-00, 4-00 | L15. Câu dẫn mạch 3 và 4 cùng khuôn "Mức … khớp … đo/chặn …" (bài học deck 01: không lặp một khuôn); mạch 4 bỏ "lớp chọn trước" | storyboard mục 3, cột `strand-lead` | mạch 4: "Với lớp hàm lỗi chọn trước, độ phức tạp Rademacher thực nghiệm chặn khoảng cách tổng quát hóa của mọi hàm trong lớp, với xác suất cao." (≈ 24) |
| nhẹ | 2-00 | L16. "bốn điểm" ở câu dẫn mạch chưa có nghĩa trước 2-02 | storyboard mục 3, mạch 2 | "Mạng nhỏ biểu diễn được hàm mà hàm afin sai, nhưng số tham số không phân biệt nhãn thật với nhãn hoán vị." (22) |
| nhẹ | ghi chú diễn giả 1-06, 2-02, 2-04, 3-00, 4-02, 5-01, 6-00 | L17. `no-ai-slop` Detect: (a) đối lập nhị phân và câu về tình trạng văn bản: "Bảng là kết quả của một thí nghiệm, không phải một định lý." (1-06); (b) lời bình về chính trang: "Câu trực quan đọc hai cực biên" (4-02), "Câu trực quan đọc cơ chế" (5-01); (c) dẫn đường: "câu trả lời nằm ở mạch 6" (2-02), "trang sau vẽ miền đó" (2-04), "Hai trang cuối nêu hai giới hạn" (6-00); (d) khuôn nhãn bị cấm dạng câu: "Kết quả trao cho mạch sau: …" (3-00, bài học "không nhãn Kết quả trao đi:"); (e) nhịp lặp: ghi chú 3-00, 4-00, 5-00, 7-00 đều mở bằng "Mạch …" | CLAUDE.md workspace, "No hedging about the text's own status", "Navigation and forward pointers"; common-brief, bài học deck 01 | (a) cắt câu; (b) mở thẳng bằng nội dung ("Hai cực biên: …"); (c) cắt hoặc nói thẳng nội dung; (d) "Với lớp kiến trúc của thí nghiệm, độ phức tạp bằng một nửa với cả hai loại nhãn."; (e) mở bằng chủ thể toán học ("Độ phức tạp Rademacher …") |
| nhẹ | 2-07 ghi chú diễn giả, 3-04, 5-06 | L18. "Phần (b) của bài tập cho thêm một hiện tượng:" (lời dẫn); "Ý nghĩa cho học:" lặp ở hai ghi chú như một nhãn ngoài danh sách | storyboard 2-07, 3-04, 5-06 | "Ở phần (b), hạ gradient khởi tạo tại $0$ …"; bỏ "Ý nghĩa cho học:", giữ câu |

## 4. Ý kiến về mục 11 (không phán quyết thay điều phối viên)

1. **Mạch 2 gộp §1–§5.** Đồng ý giữ. Phương án tách §1–§4 | §5–§6 chỉ dời trang dài nhất sang mạch 3 (≈ 12 trang) và cắt đôi một lập luận của ghi chú: câu cuối §5 nối thẳng sang §6. Điều kiện: câu nối hai nửa của mạch phải lên mặt trang (T10 cho 2-09; dòng đầu 2-08 có thể dùng câu mở §5 "lớp khớp mọi cách gán nhãn thì lỗi huấn luyện $0$ không phân biệt nhãn mang thông tin" nếu cắt bù dòng "Nhắc lại:" như mục 5).
2. **54 trang.** Chấp nhận được (dưới trần, có lý do). Nếu cần biên, phương án (a) gộp 6-03/6-04 tốt hơn (b): 6-06 là trang duy nhất nói về mạng sâu và là chỗ phân biệt kết quả đọc thêm.
3. **Trang ý tưởng chứng minh cho McDiarmid.** Không cần trang riêng: Bổ đề 07.10 là công cụ phác thảo; đưa cơ chế (martingale Doob, bổ đề Hoeffding cho từng bước tăng) vào "Trực quan." của 4-01 (T3).
4. **Ví dụ 07.9 ở ghi chú diễn giả.** Đồng ý.
5. **Trang "Kỹ thuật." riêng.** Đồng ý không có. Kiểm lại bằng `grep`: ghi chú Bài 08–10 không dùng McDiarmid, độ phức tạp Rademacher, bổ đề co hay đối xứng hóa (Bài 08 dẫn Hệ quả 07.16, Ví dụ 07.1, 07.3; Bài 09 dẫn Ví dụ 07.11, Bước 4; Bài 10 dẫn Định lý 07.11 như thiết lập). Đối xứng hóa và mẫu bóng đã có trang `L03-5-06`; nhắc lại một dòng ở 4-03 là đúng quy định. Bổ đề co dùng ba lần trong cùng bài, không qua bài khác: một dòng "Kỹ thuật." ở 5-06 là đủ.
6. **Bài tập tổng hợp 07.4(b), (c).** Đồng ý; hai rút gọn câu chữ giữ nghĩa. Thêm L8.
7. **Bảng `Mục | Bài tập` ba hàng.** Đồng ý giữ quy tắc cả bài vào một mạch (đã kiểm từng bài: 07.2(b) cần mạch 4; 07.3(e), 07.4(a)(d), 07.6 cần mạch 6; 07.7, 07.8 gần Nhận xét 07.6 ở mạch 2).
8. **Bài tập giữa cụm.** Đồng ý; xem T4 về 07.1(c).
9. **Tiếng Anh ở 2-03, 4-01.** Thêm cả hai; 4-01 bù bằng T3 (câu trực quan mới không dài hơn) và mục 5.
10. **Luận điểm bìa.** Không chọn bản 65. Bản 44 đúng, nhưng hai vế cho hai bảo đảm và không trả lời câu hỏi trung tâm. Đề xuất (47 âm tiết, một câu, có điều kiện): "Với quan sát độc lập, hàm lỗi bị chặn và lớp chọn trước khi lấy mẫu, độ phức tạp Rademacher của lớp chứa mô hình do huấn luyện chọn chặn khoảng cách tổng quát hóa với xác suất cao, kể cả khi số tham số vượt cỡ mẫu." Nếu muốn giữ ý lớp tuyến tính, dùng bản 44.
11. **Mục tiêu 79/80.** Đồng ý.
12. **2-09.** Xem T10.
13. **Đếm bảng.** Không còn lựa chọn sau quy ước 2026-11-16; xem N1, mục 5.
14. **Câu nối giữa mạch.** 3→4, 4→5, 5→6 đạt; 2→3 thiếu (T6); 6→7: "dòng cuối 6-06" là câu "Chứng minh nằm ngoài phạm vi", không phải câu nối — sau N2, dòng cuối 6-06 nên là "ngoài thừa số lôgarit, cận không phụ thuộc số tham số", đủ làm câu nối sang Tổng kết.
15. **Công thức đo ở 390 px.** Đồng ý danh sách; thêm 6-02 (đã có), 7-04 ($r_m$).
16. **Trang sát trần.** Xem T1, mục 5.
17–19. Đồng ý.
20. **Nhận xét 07.18.** Không đồng ý dạng hiện tại; xem N2.
21. **$K$ hai nghĩa.** Deck tránh được trên mặt trang (L8); đề xuất cho tác giả giữ ở mức nhẹ.

## 5. Cắt cụ thể (ước lượng theo quy ước 2026-11-16; người viết deck đo lại bằng `deck_lint.py`)

| Trang | Hiện | Đề xuất | Sau |
|---|---:|---|---:|
| 1-06 | ≈ 82 | Bỏ `caption` bảng, đưa "mười hạt giống, $5000$ điểm kiểm tra" vào ghi chú diễn giả (−7); tiêu đề cột "Lỗi kiểm tra" và "Khoảng" (−5); gộp dòng 2–3: "Lớp nơ-ron ẩn (hidden layer) $N=2000$ ReLU cố định; lớp nơ-ron ra (output layer): $w$ chuẩn nhỏ nhất, $f(x_i)=2y_i-1$" (−8; "(rectified linear unit)" chuyển sang dòng hàm kích hoạt của 2-03); "**Câu hỏi:** vì sao lỗi kiểm tra khác nhau?" (−5) | ≈ 57 |
| 2-06 | ≈ 68 | Bỏ cột "Ví dụ 07.1" (số $0$ và $\tfrac14$ vào ghi chú diễn giả, đã có) (−3); tiêu đề cột "Số hạng (Mệnh đề 04.3)" (−1); Nhận xét 07.3 bỏ "mọi", viết miền bằng KaTeX (−4) | ≈ 60; thêm bỏ "(UML §20.3)" nếu có trên mặt trang |
| 7-01 | ≈ 82/80 | Bỏ "(đầy đủ)/(phác thảo)" khỏi cột cuối, độ sâu chứng minh vào ghi chú diễn giả (−10); hàng 07.2 theo T5 | ≈ 72 |
| 6-03 | ≈ 56 | `figcaption` chỉ "$m=200$, mười lần chạy" (số đã có trong bảng) (−14); nhận dòng lề chuẩn hóa từ 5-04 nếu áp dụng T2 (+10) | ≈ 52 |
| 1-02 | 59 | "Bất đẳng thức hợp, Hoeffding (Định lý 02.7), Hệ quả 02.10." (−5); "(M) lớp con đếm được" (+4, L13) | ≈ 58; nếu cần thêm, chuyển "$G$-Lipschitz (Định nghĩa 05.4)" thành "Nhắc lại:" trên 5-03 |
| 2-08 | 60 | "**Nhắc lại:** $\mathcal H_{\sin}$: một tham số, $d=\infty$; lớp (iii) của Nhận xét 03.10: $p$ tham số, ba hàm." (−6) | ≈ 54 |
| 2-09 | 57 | xem T10 (+13 −5 −4, còn ≈ 61); thêm: gộp dòng lớp con vào dòng cấp lớp ("Bảo đảm cấp lớp (class-level) cho lớp con bị chặn theo chuẩn (norm-bounded class), $B$ chọn trước, đúng cho $h_{\hat\theta}$ khi $\lVert\hat\theta\rVert\le B$") (−4) | ≈ 57 |
| 3-01 | 58 | thay "Nhắc lại:" (17) bằng câu nối T6 (≈ 18); "**Trực quan.** Với mỗi bộ dấu, chọn hàm tương quan nhiều nhất, rồi lấy trung bình." (−3); bỏ "Thực nghiệm (empirical)/tổng thể (population)" thành tên đủ "độ phức tạp thực nghiệm (empirical)…" giữ nguyên | ≈ 56 |
| 3-03 | 60 | (b): "lớp hàm lỗi (loss class) 0–1 có cùng giá trị với mọi nhãn cố định" giữ; (c): "$\le\tfrac12$, dấu bằng khi và chỉ khi lớp tách trọn vẹn bộ điểm" (−2); bỏ "tất định;" ở (a), giữ một lần ở dòng **Bảo đảm:** (−1); dòng giả thiết "$\mathcal H\ne\varnothing$, $h:\mathcal X\to\{0,1\}$" toàn KaTeX (−1) | ≈ 56 |
| 4-02 | 58 | "Cận phụ thuộc dữ liệu (data-dependent bound), cấp lớp, không chứa $p$" giữ; "**Trực quan.** $\widehat{\mathfrak R}_S=\tfrac12$: riêng $2\widehat{\mathfrak R}_S$ đã bằng rủi ro 0–1 lớn nhất; lớp một phần tử chỉ còn số hạng tin cậy." (−2) | ≈ 56 |
| 6-02 | 60 | bỏ dòng cuối "Thêm $\ln(k(k+1))$ …" (đọc được từ công thức; vào ghi chú diễn giả) (−9); thêm "lưới" (+1, L9) | ≈ 52 |
| 6-06 | 59 | theo N2: chuyển "Chứng minh nằm ngoài phạm vi học phần" vào ghi chú diễn giả (−7); $R_\Theta$ bằng lời (+8); thêm điều kiện độc lập (+6); $\bar N$ (+9); bỏ dòng định nghĩa $\hat y_\Theta$, $\mu_\Theta$ thành một cụm "lề nhiều lớp (multiclass margin) $\mu_\Theta$" (−5) | ≈ 60; nếu vượt, chuyển dòng "Không hệ số tự do; $\varsigma_j$ …" vào ghi chú diễn giả |
| 7-02 | 60 | theo T7: dòng đầu là câu trả lời; gộp "$P$, chiều VC và độ phức tạp của lớp kiến trúc như nhau …" với dòng thí nghiệm | ≈ 55 |
| 6-05 | 51 | theo T2: bỏ Bước 1 riêng | ≈ 42 |

Với các cắt trên, trung vị ≈ 52 và chỉ còn 1-06, 2-06, 2-09, 6-06 ở 57–60.

## 6. Kiểm tra khác (đạt)

- Quyết định tác giả 2026-11-14 (nhật ký dòng 1–5): không "Nhu cầu:", không "Muốn …, phải …", mạch cuối "Tổng kết", "Vấn đề trung tâm" một hộp "Câu hỏi:", trang cuối "Tài liệu tham khảo".
- Mạch: 7 mạch, theo thứ tự mục ghi chú, mục liên tiếp; câu dẫn mạch ≤ 25 âm tiết, trần thuật.
- Thời lượng 120 phút, 54 trang ≤ 55 có lý do.
- Kỹ thuật: tên và trang lần đầu khớp các deck đã xuất bản; không xem trước kết quả bài sau trên mặt trang (Bài 08 chỉ ở dòng tên của 7-07).
- Không chuyển kết quả lồi sang mạng: 2-01 ("không cần tính lồi"), 2-07 (hàm mục tiêu không lồi, $27/16$), ghi chú diễn giả 5-05, 7-01, 7-02; Hệ quả 07.16 chỉ phát biểu cho lớp tuyến tính, mạng chỉ qua lớp ẩn cố định.
- Bài tập trên mặt trang (2-07, 3-06, 4-05, 5-07, 7-03, 7-04) khớp đề, số và lời giải của `exercises.md`; nhãn "Lời giải:".
- Thứ tự khái niệm, thuật ngữ, kí hiệu (bảng kiểm Outline/Threads/Concept của `quill`): $\Psi$ đặt sớm ở 4-01 (mục 11 điểm 19) khớp kí hiệu ghi chú; "lớp nơ-ron"/"lớp" tách đúng `thuat-ngu.md`; "cận không cho thông tin", "lôgarit", "Kí hiệu:" đúng.
- Đề xuất sửa ghi chú (mục 13): ba mục đều có cơ sở; giữ ở mức nhẹ.
