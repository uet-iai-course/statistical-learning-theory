# Duyệt deck Bài 01 — Vai 5: mạch truyện và liên kết (2026-11-15)

- **Vai:** `mach-truyen` (mạch truyện, liên kết, thống nhất thứ tự với ghi chú), chỉ đọc.
- **Bản duyệt:** `2627-1/lecture-01-mo-hinh-hoc.html` (bản đóng băng, 55 trang, `L01-k-mm`).
- **Đối chiếu:** `materials/lec-01/lecture-note.md`, `materials/lec-01/exercises.md`, `planning/lec-01/storyboard.md` (mục 3, 7, 12, 14), `review-log.md` mục "Bộ trang chiếu (2026-11-15)".
- **Kiểm máy (Playwright, 1600×900, thư mục nháp `rv-mach-truyen/`):** sáu liên kết `#/2`…`#/7` của trang 1-04 mở đúng 2-00…7-00 (cả khi gõ hash và khi bấm); hai liên kết viewer của 7-05 mở đúng ghi chú và tệp bài tập Bài 01, viewer hiện liên kết "Bộ trang chiếu" về `lecture-01-mo-hinh-hoc.html`; 0 pageerror, 0 request lỗi, 0 `.katex-error`.
- **Bảng kiểm liên tục:** dùng phần Outline / Threads / Concept của `quill/references/workflows.md` làm khung (không tạo `quill.json`): thứ tự tiên quyết, các câu hỏi mở và nơi đóng, khái niệm xuất hiện trước khi dùng. Không có deck bài trước (Bài 01 là deck đầu).

## 1. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L01-2-05 → L01-3-01 | Giới hạn tạo ra mạch 3 ("$L_D$ không tính được vì $D$ chưa biết, cần đại lượng tính được từ $S$") chỉ nằm trong ghi chú diễn giả; trên mặt trang, 2-05 kết bằng ba câu hỏi hướng về mạch 5, rồi 3-01 mở thẳng ví dụ $L_{S_\eta}$. Người xem không thấy vì sao chuyển sang rủi ro thực nghiệm. | 2-05 mặt trang: "**Câu hỏi:** hiệu trên nhỏ đến đâu, với xác suất nào theo $S$, và trên họ phân bố $D$ nào?"; ghi chú diễn giả 2-05: "Hiệu không tính được vì $L_D(h)$ là kì vọng theo $D$ chưa biết … cần một đại lượng tính được từ $S$ thay cho $L_D(h)$." Ghi chú §4 (Ví dụ 01.4) và đầu §5 nêu giới hạn này trong thân bài. | Thêm một dòng ngắn ở 3-01 trước ví dụ (hoặc cuối 2-05): "$L_D(h)$ không tính được vì $D$ chưa biết; $L_S(h)$ tính được từ $S$." Giữ trần 6 dòng bằng cách chuyển dòng "Diễn giải" của 3-01 xuống dưới hình nếu cần. |
| trung bình | L01-5-07 | Trang mở phần rủi ro Bayes không nêu giới hạn của định nghĩa khả diễn sinh ra nhu cầu đối tượng so sánh mới: ghi chú §7 viết "nên yêu cầu $L_D(A(S))\le\epsilon$ không đạt được khi $\epsilon<0{,}05$". Mặt trang chỉ có nửa đầu (mọi hàm sai ít nhất $0{,}05$), nên liên kết 5-06 → 5-07 không nói giả thiết nào đổi. | 5-07: "Dưới $D_\eta$, tại $x=2$ mọi hàm phân lớp sai với xác suất ít nhất $0{,}2\cdot\min\{\tfrac14,\tfrac34\}=0{,}05$." Ghi chú dòng 877: "… nên yêu cầu $L_D(A(S))\le\epsilon$ không đạt được khi $\epsilon<0{,}05$. Mức rủi ro dùng để so với $L_D(A(S))$ được gọi là *đối tượng so sánh*". Câu nối chỉ có trong ghi chú diễn giả 5-06 và 5-07. | Nối dòng đầu 5-07: "…ít nhất $0{,}05$, nên $L_D(A(S))\le\epsilon$ không đạt khi $\epsilon<0{,}05$." |
| trung bình | L01-5-11, L01-5-12 | Câu hỏi then chốt của nửa sau mạch 5 trong ghi chú ("**Câu hỏi.** Nên so $L_D(A(S))$ với $\inf_{h\in\mathcal H}L_D(h)$ hay với rủi ro Bayes?") không lên mặt trang; ghi chú diễn giả 5-11 dẫn nó bằng cụm điều hướng "Câu hỏi của ghi chú:". Vì vậy dòng "Lưu ý: đối tượng so sánh … là $\inf_hL_D(h)$" ở 5-12 trả lời một câu hỏi người xem chưa thấy, và đối tượng so sánh xuất hiện lần đầu trên mặt trang ở dòng cuối của mạch. | Ghi chú dòng 981 (câu hỏi), dòng 983–986 (hai lý do); 5-11 ghi chú diễn giả: "Câu hỏi của ghi chú: nên so …?"; 5-12 mặt trang: "**Lưu ý:** đối tượng so sánh (comparator) là $\inf_hL_D(h)$, vì $A(S)\in\mathcal H$ không xuống dưới mức này." | Đưa "**Câu hỏi:** nên so $L_D(A(S))$ với $\inf_{h\in\mathcal H}L_D(h)$ hay với $L_D^{\mathrm{Bayes}}$?" lên cuối 5-11 (thay dòng "Diễn giải" hoặc gộp vào nó: "$0{,}04$ chỉ phụ thuộc lớp, không giảm khi $m$ tăng"); trong ghi chú diễn giả 5-11 bỏ cụm "Câu hỏi của ghi chú:". 5-12 giữ dòng "Lưu ý:" làm câu trả lời. |
| trung bình | L01-6-04 → L01-6-05 | Bước chuyển từ phản ví dụ sang bảo đảm dương (nửa sau mạch 6) không có trên mặt trang. Câu nối "một bảo đảm học phải dùng cấu trúc của lớp giả thuyết hoặc tính chất của một thuật toán cụ thể" chỉ ở ghi chú diễn giả 6-02; 6-05 mở bằng "Trực quan." về $A_{\max}$, nên câu hỏi của nửa sau mạch ("có bảo đảm học nào cho một lớp có cấu trúc?") không được nêu. | Ghi chú diễn giả 6-02: "Một bảo đảm học phải dùng cấu trúc của lớp giả thuyết hoặc tính chất của một thuật toán cụ thể."; ghi chú §9 dòng 1153: "Trên lớp hàm ngưỡng, thuật toán $A_{\max}$ có một cỡ mẫu đủ chung cho mọi phân bố khả diễn."; 6-05 dòng đầu: "**Trực quan.** $A_{\max}$ chỉ sai ở các mức …". | Thêm ở đầu 6-05 một câu khẳng định theo ghi chú §9: "Trên lớp hàm ngưỡng, $A_{\max}$ có một cỡ mẫu đủ chung cho mọi phân bố khả diễn." (có thể thay dòng "Ý nghĩa:" của 6-02 bằng "$L_S$ nhỏ chưa đủ; bảo đảm học cần cấu trúc của lớp hoặc của thuật toán.") |
| trung bình | L01-7-05 | Bảng `Mục \| Bài tập` xếp một số bài vào mạch đứng trước kiến thức bài cần. Bài tập 01.8(b) đòi $m_{\mathcal H_{\mathrm{sg}}}(\epsilon,\delta)\le\lceil\ln(1/\delta)/\epsilon\rceil$, tức kỹ thuật chặn xác suất bỏ sót của mạch 6, nhưng được xếp ở "Học PAC"; chính ghi chú diễn giả 7-05 viết "Bài tập 01.8 và 01.9 dùng cùng kỹ thuật chặn xác suất bỏ sót". Tương tự: 01.1(d) cần Mệnh đề 01.23(b) (mạch 5) nhưng xếp ở mạch 2; 01.2(b)(c) cần quy tắc Bayes, rủi ro vượt mức (mạch 5) nhưng xếp ở mạch 3; 01.4(c) so với Ví dụ 01.11 (mạch 6) nhưng xếp ở mạch 4. | `exercises.md` dòng 546 (01.8(b)), 555–557 (Gợi ý 2: "Dùng $1-x\le e^{-x}$"); dòng 24 (01.1(d)), 35–37 (Gợi ý 3: "Dùng Mệnh đề 01.23(b)"); dòng 90, 92 (01.2(b)(c)); dòng 304 (01.4(c) "So sánh với Ví dụ 01.11"); 7-05 bảng: "Học PAC \| 01.5, 01.7, 01.8, 01.10, 01.11", "Rủi ro thực nghiệm nhỏ và bảo đảm học \| 01.9". | Chuyển 01.8 sang dòng mạch 6 ("01.8, 01.9"). Với các bài nhiều phần, ghi phần theo mạch: mạch 2 "01.1(a)–(c)", mạch 3 "01.2(a), 01.3", mạch 4 "01.4(a)(b), 01.6", mạch 5 "01.1(d), 01.2(b)(c), 01.5, 01.7, 01.10, 01.11", mạch 6 "01.4(c), 01.8, 01.9"; hoặc giữ bài nguyên khối ở mạch muộn nhất mà bài cần. |
| trung bình | L01-4-00, L01-4-02 | "Quá khớp" là từ khóa của trang tiêu đề mạch 4 và là ý chính được ghi chú in đậm, nhưng không xuất hiện trên mặt trang nội dung nào (chỉ ở ghi chú diễn giả 4-02 và dòng UML ở 7-06). Trang tiêu đề mạch hứa một khái niệm mà mạch không đưa ra. | 4-00 `strand-keys`: "thuật toán ghi nhớ · nguyên tử · bất đẳng thức hợp · quá khớp · thiên kiến quy nạp"; ghi chú dòng 694: "Hàm phân lớp ghi nhớ là trường hợp cực đoan của **quá khớp** (overfitting)."; quét mặt trang: "quá khớp" chỉ có ở 4-00 và 7-06. | Thêm "**Ý nghĩa:** hàm phân lớp ghi nhớ là trường hợp cực đoan của quá khớp (overfitting)." vào 4-02 (sau (c)); hoặc bỏ "quá khớp" khỏi `strand-keys` của 4-00. |
| nhẹ | L01-4-06 → L01-5-00 | Kết luận mạch 4 trong ghi chú ("một bảo đảm học phải phát biểu trực tiếp cho $L_D(A(S))$ và phải cho phép thất bại trên những tập huấn luyện như $S_f$") là đầu vào của mạch 5 nhưng chỉ có ở ghi chú diễn giả 4-06 và 5-00. 5-01 bù một phần (xác suất bỏ sót $0{,}8^m>0$), phần "phát biểu trực tiếp cho $L_D(A(S))$" không lên mặt trang. | Ghi chú dòng 706; ghi chú diễn giả 4-06 (câu cuối), 5-00 ("Kế thừa: …"). | Nếu còn chỗ, thêm dòng cuối 4-06: "Bảo đảm học phải nói về $L_D(A(S))$ và cho phép thất bại trên những tập như $S_f$." (4-06 đã sáu dòng; có thể gộp hai dòng định nghĩa thiên kiến quy nạp thành một.) |
| nhẹ | L01-7-04 | Câu hỏi 4 dẫn "Ví dụ 01.9" trên mặt trang, nhưng số hiệu này chưa xuất hiện trên mặt trang nào trước đó (5-05 có tiêu đề "Ví dụ: xác suất thất bại của $A_{\max}$ dưới $D_f$", không ghi số). Người chỉ xem deck không biết "Ví dụ 01.9" là trang nào. | Quét mặt trang: "Ví dụ 01.9" chỉ ở 7-04; 5-05 không có số hiệu. | Viết "Cỡ $14$ dưới $D_f$ và cỡ $30$ của Mệnh đề 01.31 …", hoặc thêm "(Ví dụ 01.9)" vào một dòng của 5-05. |
| nhẹ | L01-3-03 | Ghi chú diễn giả dùng $A_{\max}$ và $\hat t$ dưới $D_f$ ("Kỹ thuật này còn cho kì vọng rủi ro của $A_{\max}$ dưới $D_f$: với $N=\hat t-3$ …") trước khi 3-04 định nghĩa $A_{\max}$; đây là câu dẫn về phía sau. | Ghi chú diễn giả 3-03, câu thứ bảy; $A_{\max}$ định nghĩa ở 3-04. | Chuyển câu này sang ghi chú diễn giả 3-05, ngay sau công thức $0{,}2(0{,}8^m+0{,}6^m+0{,}4^m)$ mà nó giải thích. |
| nhẹ | L01-4-03, L01-4-04 | Trang ý tưởng chứng minh 4-03 gọi tên "bất đẳng thức hợp" ở bước 3 trước trang "Kỹ thuật." 4-04 nêu phát biểu chung. Công thức trường hợp riêng có ngay trên 4-03 nên trang vẫn đọc được; thứ tự "kỹ thuật sau chứng minh" lặp lại ở 6-06/6-07. | 4-03 bước 3: "bất đẳng thức hợp và giả thiết không có nguyên tử cho $\Pr(X\in F)\le\sum\Pr(X=x_i)=0$"; 4-04 tiêu đề "Bất đẳng thức hợp". | Chấp nhận được nếu giữ nhất quán cả hai cặp; nếu đổi, đặt 4-04 trước 4-03 (kỹ thuật được dùng ngay ở bước 3). |
| nhẹ | L01-6-06, L01-6-07 | Trùng lặp: công thức hiển thị $\big(1-D_{\mathcal X}(C)\big)^m\le(1-\epsilon)^m\le e^{-\epsilon m}$ xuất hiện nguyên dạng trên cả 6-06 và 6-07. | 6-06 dòng cuối (math-large); 6-07 dòng "Kỹ thuật." (display). | Ở 6-06 thay bằng một dòng "Theo (T1) và kỹ thuật chặn xác suất bỏ sót, $\Pr_S[L_D(h_{\hat t})>\epsilon]\le e^{-\epsilon m}$."; giữ dạng đầy đủ ở 6-07. Hoặc giữ ở 6-06 và để 6-07 chỉ nêu dạng chung, "Dùng khi …" và con số $m=30$. |
| nhẹ | L01-2-02 | Hàm gán nhãn $f$ và $D_f$ dùng trên mặt trang (hàng "$f(x)$" của bảng, dòng "$f=h_3$") mà thuật ngữ "hàm gán nhãn (labeling function, target function)" chỉ nêu trong ghi chú diễn giả 2-01. | 2-02 bảng và dòng cuối; ghi chú diễn giả 2-01: "hàm gán nhãn (labeling function, target function) $f$". Ghi chú §1 mục 2 nêu thuật ngữ trong thân bài. | Ở 2-02 viết "Dữ liệu tất định từ $D_f$ với hàm gán nhãn (labeling function, target function) $f=h_3$: …". |
| nhẹ | L01-7-02 | Ghi chú diễn giả viết "Các câu trả lời theo thứ tự lập luận của bài", nhưng danh sách đặt hai dòng học PAC (mạch 5) trước dòng không chệch (mạch 3) và dòng phản ví dụ (mạch 4, 6). Thứ tự hiện tại hợp lý (câu trả lời trước, căn cứ sau), chỉ câu mô tả là sai. | 7-02 năm dòng; ghi chú diễn giả câu đầu. | Sửa câu đầu ghi chú diễn giả: "Hai dòng đầu trả lời trực tiếp câu hỏi; ba dòng sau là các kết quả đỡ cho câu trả lời." |

**Ghi chú cho điều phối viên (không phải phát hiện về deck):** `review-log.md`, mục "Bộ trang chiếu", dòng "Mục 11.5" ghi trang kỹ thuật chặn xác suất bỏ sót là "6-06"; ở deck cuối trang này là 6-07 (6-06 là ý tưởng chứng minh). Storyboard mục 14 đã ghi ánh xạ mã 6-06 → 6-07; nên sửa con số trong `review-log.md` khi ghi quyết định.

**Số phát hiện:** 0 chặn bàn giao, 0 nghiêm trọng, 6 trung bình, 7 nhẹ.

## 2. Kiểm từng mạch

| Mạch | Câu hỏi trung tâm của mạch | Xuất hiện trên mặt trang (trước nửa sau?) | Đầu vào → đầu ra trên mặt trang | Nhận xét |
|---|---|---|---|---|
| 1. Mở đầu (1-01…1-06) | Học có nghĩa là gì? | 1-05, hộp "Câu hỏi:" duy nhất | luận điểm → câu hỏi → ví dụ $h_3$, $h_4$ cùng khớp $S_f$ | Đạt: một hộp, câu trả lời theo phần ở ghi chú diễn giả (quyết định 2026-11-14). |
| 2. Bài toán học thống kê (2-00…2-05) | Đo chất lượng hàm dự đoán bằng gì, mục tiêu là gì? | Lời dẫn 2-00; 2-01 (thành phần), 2-03 (rủi ro kì vọng) — có | ví dụ mở đầu → $L_D$, $\ell_c$, mục tiêu $L_D(A(S))-\inf_hL_D(h)$ | Đầu ra "không tính được $L_D$" chỉ ở ghi chú diễn giả (phát hiện trung bình 2-05). |
| 3. Rủi ro thực nghiệm và ERM (3-00…3-07) | Khi nào trung bình của $L_S$ bằng $L_D$? | 3-02 (trang thứ ba) — có | $L_S$ → Mệnh đề 01.7 → ERM, quy tắc chọn → chỗ hỏng với $A(S)$ → tập độc lập | Đạt; câu hỏi 2-03 được đóng ở 3-06 (mặt trang) và ghi chú diễn giả 3-06 nói rõ. |
| 4. Thuật toán ghi nhớ và thiên kiến quy nạp (4-00…4-06) | Vì sao khớp mọi quan sát vẫn sai với xác suất 1? | Lời dẫn 4-00; 4-01, 4-02 — có | quy tắc chọn quyết định rủi ro → $L_S=0$, $L_D=1$ → thiên kiến quy nạp | Đầu ra sang mạch 5 chỉ ở ghi chú diễn giả (nhẹ); "quá khớp" không lên mặt trang (trung bình). |
| 5. Học PAC (5-00…5-12) | Thế nào là học được (độ chính xác, xác suất, họ phân bố, đối tượng so sánh)? | Ba câu hỏi ở 2-05; 5-01, 5-03 — có cho nửa đầu. Nửa sau (5-07…5-12) do câu hỏi đối tượng so sánh dẫn, câu hỏi này không lên mặt trang | bảo đảm phải cho phép thất bại → $\epsilon$, $\delta$ → định nghĩa khả diễn → $m_A$, $m_{\mathcal H}$ → rủi ro Bayes → rủi ro vượt mức → học PAC bất khả diễn | Mạch dài 13 trang đã được chấp nhận (quyết định 11.6). Hai chỗ nối thiếu: 5-07 và 5-11/5-12 (trung bình). |
| 6. Rủi ro thực nghiệm nhỏ và bảo đảm học (6-00…6-07) | $L_S$ nhỏ có đủ không; có cỡ mẫu chung cho mọi phân bố không? | 6-01 "Câu hỏi:" (nửa đầu) — có; câu hỏi của nửa sau không nêu | định nghĩa học PAC, phản ví dụ → Hệ quả 01.29 → Ví dụ 01.11 → Mệnh đề 01.31 → kỹ thuật | Chỗ nối 6-04 → 6-05 thiếu (trung bình). |
| 7. Tổng kết (7-00…7-06) | Trả lời "học có nghĩa là gì" | 7-02 | mọi kết quả → bảng, trả lời, bài tập tổng hợp, tự kiểm tra, bài tập về nhà, tài liệu | Không có khái niệm mới (lọc thư rác là bối cảnh của Bài tập 01.1, không phải khái niệm). Thứ tự trang đúng quy định. Trang "Vấn đề trung tâm" cuối trả lời cho cả bài, không theo từng mạch. |

**Các mạch câu hỏi (threads) mở và nơi đóng**

| Câu hỏi hoặc chuỗi | Mở | Đóng | Trạng thái |
|---|---|---|---|
| "Học có nghĩa là gì?" | 1-05 | 7-02 | đóng trên mặt trang |
| $h_3$, $h_4$ cùng khớp $S_f$ | 1-06 | 2-05 ($0$ và $0{,}2$), 3-04 ($A_{\min}$, $A_{\max}$), 4-06, 5-06, ghi chú diễn giả 7-02 | đóng |
| "Tại sao không nên đo trên tập huấn luyện?" | 2-03 | 3-06 (dòng "Do đó …", ghi chú diễn giả nói rõ) | đóng |
| Câu hỏi thực hành: ngưỡng khi hai loại lỗi có chi phí khác nhau | 2-03 (ghi chú diễn giả), 2-04 (bảng $L^c$) | 5-10 (mặt trang), 7-03 (chi phí đảo) | đóng |
| Ba câu hỏi chính (nhỏ đến đâu, xác suất nào, họ phân bố nào) | 2-05 | 5-01 ($\epsilon$, $\delta$), 5-03 ($\forall D$), 5-12 (họ phân bố có rủi ro hữu hạn) | đóng; liên kết ngược chỉ ở ghi chú diễn giả 5-01 |
| $\mathbb E_SL_S(A(S))=\mathbb E_SL_D(A(S))$? | 3-05 | 3-05 (fragment) | đóng |
| Bỏ "không có nguyên tử" thì sao? | 4-03 (dòng cuối) | 6-04 | đóng |
| "Cỡ mẫu đủ có được phụ thuộc $D$?" | 5-03 | 5-03 (dòng 1), 5-05 ("chỉ đủ cho riêng $D_f$"), 6-05 ($30$), 7-04 câu 4 | đóng |
| Đối tượng so sánh: $\inf_hL_D(h)$ hay $L_D^{\mathrm{Bayes}}$? | ghi chú §7 (không có trên mặt trang) | 5-12 "Lưu ý:" | mở thiếu trên mặt trang (phát hiện trung bình) |
| "Có cận nào nhỏ hơn $\beta\equiv1$?" | 6-01 | 6-01 (fragment), 6-02 | đóng |
| Kỹ thuật: tính tuyến tính → bất đẳng thức hợp → chặn xác suất bỏ sót | 3-03, 4-04, 6-07 | 7-01 (cột ý tưởng), 7-05 (ghi chú diễn giả) | đóng; tên kỹ thuật thống nhất ở 4-03, 4-04, 4-05, 6-07, 7-01 |
| "Quá khớp" | 4-00 (từ khóa) | không có trên mặt trang | thiếu (phát hiện trung bình) |

## 3. Bảng chức năng từng trang

Ký hiệu: "MT" = mặt trang, "GCDG" = ghi chú diễn giả. Cột cuối đánh dấu liên kết chỉ có ở GCDG khi điều đó đáng lưu ý.

| Trang | Vai trò trong mạch | Kết nối vào | Kết nối ra |
|---|---|---|---|
| 1-01 | Bìa, luận điểm một câu | — | luận điểm được trả lời ở 7-02 (dòng 1–2) |
| 1-02 | Tiên quyết, (T1), (T2), ERM, PAC | — | (T1) dùng ở 3-02, 5-05, 6-02, 6-05; $1-x\le e^{-x}$ ở 6-06/6-07; $\mathbb E[\mathbb E[U\mid X]]$ ở 5-09 |
| 1-03 | Mục tiêu (bằng lời) | — | năm mục tiêu ứng với mạch 2–6 |
| 1-04 | Nội dung, liên kết `#/2`…`#/7` | — | khớp sáu trang tiêu đề mạch (đã kiểm trình duyệt) |
| 1-05 | Vấn đề trung tâm, một hộp | luận điểm 1-01 | 7-02 |
| 1-06 | Ví dụ dẫn nhập $h_3$, $h_4$, $S_f$ | câu hỏi 1-05 | 2-00 (GCDG "Kế thừa"), 2-02 ($S_f$), 2-05 |
| 2-00 | Tiêu đề mạch 2 | 1-06 | 2-01 |
| 2-01 | Tám thành phần; cái cố định, cái ngẫu nhiên | 1-06 | 2-02 (ví dụ cụ thể của các thành phần) |
| 2-02 | Ví dụ xuyên suốt $D_\eta$, $D_f$, $S_\eta$, $S_f$ | 2-01, 1-06 ($S_f$) | 2-04, 3-01, 3-04 |
| 2-03 | Rủi ro kì vọng, $\ell_c$; câu hỏi về tập huấn luyện | 2-02 | 2-04 (tính); câu hỏi đóng ở 3-06; $\ell_c$ dùng lại 5-10, 7-03 |
| 2-04 | Ví dụ tính $L_{D_\eta}$, $L^c_{D_\eta}$ | 2-03 | 2-05 ($0{,}22$), 3-01 (đường $L_D$ trên hình), 5-10 ($0{,}32$), 5-11 |
| 2-05 | Mục tiêu của bài toán học; ba câu hỏi chính | 2-04, 1-06 | 5-01/5-03/5-12 (ba câu hỏi); sang 3-01 chỉ qua GCDG (trung bình) |
| 3-00 | Tiêu đề mạch 3 | 2-05 (GCDG) | 3-01 |
| 3-01 | Ví dụ mở $L_S$ trên $S_\eta$; ba ngưỡng cùng $\tfrac13$ | 2-02, 2-04 | 3-02 (lệch trên một tập), 3-04 (tập nghiệm $\{h_2,h_3,h_5\}$) |
| 3-02 | Trực quan, ví dụ, phát biểu Mệnh đề 01.7 | 3-01 | 3-03 |
| 3-03 | Ý tưởng chứng minh, cực biên, bỏ giả thiết, kỹ thuật tuyến tính | 3-02 | 3-05 ("Bước 1 … hỏng"), 4-04 (chứng minh bất đẳng thức hợp dùng lại), 6-04 |
| 3-04 | ERM, quy tắc chọn khi bằng nhau, $A_{\min}$, $A_{\max}$ | 3-01, 1-06 ($S_f$) | 3-05 ($A_{\max}$), 4-00 (GCDG "Kế thừa"), 5-05 |
| 3-05 | Phản ví dụ $m=1$: chỗ hỏng khi $h=A(S)$ | 3-03 (bước 1), 3-04 | 3-06 |
| 3-06 | Khoảng cách tổng quát hóa; đóng câu hỏi 2-03; tập độc lập | 3-05, 2-03 | 3-07; 6-01 (khoảng cách tổng quát hóa dùng lại) |
| 3-07 | Bài tập 01.2(a): Thuật toán 01.13 | 3-04 | 4-00 |
| 4-00 | Tiêu đề mạch 4 | 3-04 (GCDG) | 4-01 |
| 4-01 | Ví dụ dẫn nhập: $[0,1]$, $\mathcal M_{\mathcal X}$, $A_{\mathrm{gn}}$ | 4-00 | 4-02 |
| 4-02 | Trực quan, phát biểu Mệnh đề 01.15 | 4-01 | 4-03; 6-01, 6-02 dẫn lại |
| 4-03 | Ý tưởng chứng minh; bỏ "không có nguyên tử" | 4-02 | 4-04 (kỹ thuật), 6-04 (phản ví dụ khi bỏ giả thiết) |
| 4-04 | Kỹ thuật: bất đẳng thức hợp | 4-03 bước 3 | 4-05, 7-01 |
| 4-05 | Bài tập 01.4(a) | 4-02, 4-04 | 4-06 |
| 4-06 | Thiên kiến quy nạp; $\tilde S_f$ so với $S_f$ | 4-01, 2-02 ($D_f$) | 5-00 (GCDG); 5-11 (giá của thiên kiến, GCDG) |
| 5-00 | Tiêu đề mạch 5 | 4-06 (GCDG) | 5-01 |
| 5-01 | Vai trò $\delta$, $\epsilon$ | 2-05 (câu hỏi), 1-06 ($S_f$ bỏ sót mức 3) | 5-02 |
| 5-02 | Khả diễn, định nghĩa học PAC khả diễn, lớp học được PAC | 5-01 | 5-03 |
| 5-03 | Thứ tự lượng từ; "cỡ mẫu có phụ thuộc $D$?" | 5-02 | 5-04, 5-05 ("chỉ đủ cho $D_f$"), 5-12 ("cùng thứ tự lượng từ"), 7-04 câu 4 |
| 5-04 | $m_A$, $m_{\mathcal H}$ | 5-02, 5-03 | 5-05, 6-05 ($m_{A_{\max}}$) |
| 5-05 | Ví dụ 01.9: $14$ và $6$ dưới $D_f$ | 3-04/3-05 ($A_{\max}$), 5-04 | 5-06, 6-05 (Ý nghĩa), 6-07 (hình) |
| 5-06 | Bài tập 01.5(d): đọc bảo đảm PAC | 5-05 | 5-07 (qua GCDG: câu không đúng dưới $D_\eta$) |
| 5-07 | Rủi ro Bayes; trực quan; Ví dụ 01.10 ($0{,}18$) | 2-02 ($\eta$), 5-02 (khả diễn) — giới hạn không nêu trên MT (trung bình) | 5-08 |
| 5-08 | Phát biểu Mệnh đề 01.23 | 5-07 | 5-09; "Ý nghĩa" → 5-11 |
| 5-09 | Ý tưởng chứng minh; kỹ thuật tối thiểu hóa từng điểm | 5-08 | 5-10 |
| 5-10 | Ví dụ $\ell_c$: ngưỡng $\tfrac15$, $h_2$; đóng câu hỏi thực hành | 5-08(b), 2-04 | 5-11, 7-03 |
| 5-11 | Rủi ro vượt mức, phân tách $0{,}10+0{,}04$ | 5-07, 5-08, 2-04 | 5-12 (câu hỏi đối tượng so sánh chỉ ở GCDG, trung bình) |
| 5-12 | Học PAC bất khả diễn; đối tượng so sánh | 5-03 (thứ tự lượng từ), 5-11 | 6-00 |
| 6-00 | Tiêu đề mạch 6 | 5-12, 4-02 (GCDG) | 6-01 |
| 6-01 | Định nghĩa 01.28; câu hỏi $\beta<1$? | 3-06 (khoảng cách tổng quát hóa), 4-02 | 6-02 |
| 6-02 | Phát biểu Hệ quả 01.29 | 6-01, 4-02 | 6-03 |
| 6-03 | Ý tưởng chứng minh Hệ quả 01.29 | 6-02, 5-04 ($m_A=\infty$) | 6-04 |
| 6-04 | Ví dụ 01.11: bỏ "không có nguyên tử" | 4-03 (dòng bỏ giả thiết), 3-03 (tuyến tính) | 6-05 chỉ qua GCDG 6-02 (trung bình) |
| 6-05 | Phát biểu Mệnh đề 01.31; $30$ so với $14$ | 5-04, 5-05 | 6-06 |
| 6-06 | Ý tưởng chứng minh Mệnh đề 01.31 | 6-05 | 6-07 |
| 6-07 | Kỹ thuật: chặn xác suất bỏ sót | 6-06, 1-02 ($1-x\le e^{-x}$), 5-05 (hình) | 7-01 |
| 7-00 | Tiêu đề mạch 7 | toàn bài | 7-01 |
| 7-01 | Bảng tổng kết năm kết quả | 3-02, 4-02, 5-08, 6-02, 6-05 | 7-02 |
| 7-02 | Vấn đề trung tâm, trả lời cho cả bài | 1-05, 5-12, 3-02, 4-02, 6-05 | 7-03 |
| 7-03 | Bài tập tổng hợp 01.1(d) | 5-08, 5-10, 5-02 | 7-04 |
| 7-04 | Câu hỏi tự kiểm tra | 2-01, 3-04, 5-06, 5-05/6-05 | 7-05 |
| 7-05 | Bài tập về nhà, liên kết viewer | mọi mạch | 7-06 |
| 7-06 | Tài liệu tham khảo; một dòng Bài 02 | §12 ghi chú | Bài 02 (chữ, chưa liên kết; quyết định 11.13) |

## 4. Bảng đối chiếu trang → mục ghi chú

Đối chiếu độc lập với tiêu đề mục và khối của `lecture-note.md` (grep `^##`, `^:::`). "Thứ tự" = khối trên mặt trang có đứng sau khối của trang trước trong thứ tự đọc của ghi chú không.

| Trang | Mục ghi chú | Khối trên mặt trang | Thứ tự |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §7 đoạn cuối | — | tổng quan |
| 1-02 | Kiến thức tiên quyết; §2 | (T1), (T2) | tổng quan |
| 1-03 | Mục tiêu học tập | — | tổng quan |
| 1-04 | toàn bài | — | tổng quan |
| 1-05 | đoạn mở đầu | — | tổng quan |
| 1-06 | Câu hỏi mở đầu | — | đúng |
| 2-01 | §1 | danh sách tám thành phần, bảng nguồn ngẫu nhiên | đúng |
| 2-02 | §3 | Ví dụ 01.1 | đúng |
| 2-03 | §3 (ứng dụng sàng lọc), §4 | Định nghĩa 01.1; **Câu hỏi.** dòng 208 | đúng |
| 2-04 | §4 | Ví dụ 01.2 | đúng |
| 2-05 | §4 | Định nghĩa 01.5, Ví dụ 01.4 | đúng (Ví dụ 01.3, Định nghĩa 01.3, 01.4 chỉ ở GCDG 2-01, 2-03) |
| 3-01 | §5 | Định nghĩa 01.6, Ví dụ 01.5 | đúng |
| 3-02 | §5 | Mệnh đề 01.7 | đúng |
| 3-03 | §5 | chứng minh Mệnh đề 01.7 | đúng |
| 3-04 | §5 | Định nghĩa 01.8, Ví dụ 01.6 | đúng |
| 3-05 | §5 | Nhận xét 01.9 (**Câu hỏi.** dòng 512); ví dụ $m=1$ dựng mới | đúng |
| 3-06 | §5 | Định nghĩa 01.10 và đoạn sau | đúng |
| 3-07 | §5; tệp bài tập | Thuật toán 01.13; Bài tập 01.2(a) | đúng (Nhận xét 01.11, Ví dụ 01.7, Định nghĩa 01.12 nằm giữa, chỉ ở GCDG 3-04) |
| 4-01 | §5 | Định nghĩa 01.14, Ví dụ 01.8 | đúng |
| 4-02 | §5 | Mệnh đề 01.15 | đúng |
| 4-03 | §5 | chứng minh Mệnh đề 01.15 | đúng |
| 4-04 | §5 | chứng minh Mệnh đề 01.15, Bước 3 | đúng |
| 4-05 | tệp bài tập | Bài tập 01.4(a) | nguồn phụ |
| 4-06 | §5, đoạn sau chứng minh Mệnh đề 01.15 | thiên kiến quy nạp, $\tilde S_f$ | đúng |
| 5-01 | §6 đoạn đầu | $\delta$, $\epsilon$, ví dụ $0{,}999^{500}$ | đúng |
| 5-02 | §6 | Định nghĩa 01.16, 01.18 | đúng (Nhận xét 01.17 ở GCDG) |
| 5-03 | §6 | đoạn thứ tự lượng từ, **Câu hỏi.** dòng 758 | đúng |
| 5-04 | §6 | Định nghĩa 01.20, Nhận xét 01.21 | đúng |
| 5-05 | §6 | Ví dụ 01.9 | đúng |
| 5-06 | tệp bài tập; §6 | Bài tập 01.5(d) câu 4; Nhận xét 01.19 | lệch nhẹ có lý do: Nhận xét 01.19 đứng trước Định nghĩa 01.20 trong ghi chú; bài tập cần con số của Ví dụ 01.9 nên phải đứng sau 5-05 |
| 5-07 | §7 đoạn đầu | Định nghĩa 01.22; Ví dụ 01.10 (phần 0–1) | đúng |
| 5-08 | §7 | Mệnh đề 01.23 | đúng |
| 5-09 | §7; Phụ lục B | đoạn ý tưởng sau Mệnh đề 01.23 | đúng |
| 5-10 | §7 | Ví dụ 01.10 (phần $\ell_c$) | đúng |
| 5-11 | §7 | Định nghĩa 01.24 và ví dụ sau | đúng; **Câu hỏi.** dòng 981 không lên MT |
| 5-12 | §7 | Định nghĩa 01.25 và đoạn sau | đúng (Nhận xét 01.26, 01.27 ở GCDG) |
| 6-01 | §8 | Định nghĩa 01.28, **Câu hỏi.** dòng 1051 | đúng |
| 6-02 | §8 | Hệ quả 01.29 | đúng |
| 6-03 | §8 | chứng minh Hệ quả 01.29 | đúng |
| 6-04 | §8 | Ví dụ 01.11 | đúng (Nhận xét 01.30 ở GCDG 6-02) |
| 6-05 | §9 | Mệnh đề 01.31 | đúng; đoạn mở §9 (hai loại phát biểu học PAC, bốn quyết định thực hành) không lên MT, một phần ở GCDG 7-01 và MT 3-06 ("Lưu ý: … $S'$ độc lập") |
| 6-06 | §9 | chứng minh Mệnh đề 01.31 (phác thảo) | đúng |
| 6-07 | §9; Kiến thức tiên quyết | bước cuối của chứng minh | đúng |
| 7-01 | §5–§9 | năm kết quả | tổng kết |
| 7-02 | §7 đoạn cuối; §11 | — | tổng kết |
| 7-03 | tệp bài tập | Bài tập 01.1(d) | tổng kết |
| 7-04 | §11; §6 | câu hỏi cuối buổi và hai câu hỏi phụ của §11, thêm câu 4 | tổng kết |
| 7-05 | §10; tệp bài tập | Bài tập 01.1–01.11 | tổng kết (xem phát hiện 7-05) |
| 7-06 | §11 đoạn cuối, §12 | UML §§2.1–2.3, §§3.1–3.2, §5.1; tên Bài 02 khớp `materials/lec-02/lecture-note.md` | tổng kết |

**Kết quả đối chiếu.** Mỗi mạch ứng với các mục liên tiếp: mạch 2 ↔ §1, §3, §4 (§2 ở 1-02); mạch 3 ↔ §5 từ Định nghĩa 01.6 đến Thuật toán 01.13; mạch 4 ↔ §5 từ Định nghĩa 01.14 đến hết mục; mạch 5 ↔ §6, §7; mạch 6 ↔ §8, §9; mạch 7 ↔ §10–§12. Đọc từ trên xuống, khối trên mặt trang theo đúng thứ tự đọc của ghi chú, trừ 5-06 (có lý do). Bảng mục 12 của storyboard khớp deck cuối (55 mã, cùng khối). Tám câu "**Câu hỏi.**" của ghi chú: bảy câu có trên mặt trang (1-06, 2-03, 3-05, 5-03, 6-01, 7-04, câu hỏi thực hành ở 5-10); câu dòng 981 thiếu. Trang tiêu đề mạch: tên mạch khác tiêu đề trang nội dung đầu tiên ở cả sáu mạch; lời dẫn là câu trần thuật nêu điều người học làm được, không "Nhu cầu:", không "Muốn …, phải …"; lời dẫn chỉ dùng từ thông thường. Mặt trang không xem trước bài sau (chỉ 7-06 có một dòng tên Bài 02 theo quy định); "Bài 02" trong GCDG 4-04, 6-07, 7-06 là cầu nối, không trên MT.

## 5. Đề xuất sửa ghi chú

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | `exercises.md`, dòng "**Mức độ:** … **Mục tiêu:** …" của mỗi bài; ghi chú §10 | Tệp bài tập và §10 chỉ ánh xạ bài tập sang mục tiêu học tập, không sang mục của ghi chú, nên bảng `Mục \| Bài tập` của deck phải suy ra và dễ xếp bài trước kiến thức nó cần (phát hiện 7-05). | `exercises.md` dòng 9, 70, 186, 295, 356, 449, 498, 539, 599, 671, 710; ghi chú §10 dòng 1211–1221. | Nếu tác giả đồng ý: thêm "**Mục ghi chú:** §k" vào dòng "Mức độ / Mục tiêu" của mỗi bài (với bài nhiều phần, ghi mục theo phần). Không bắt buộc cho deck. |

Không thấy lỗi thứ tự hay khoảng trống mới trong ghi chú; đề xuất về cụm "(giá trị dựng để luyện tập)" ở `exercises.md` dòng 73 đã có trong `review-log.md`.

## 6. Kết luận

**đạt khi sửa** — 0 chặn bàn giao, 0 nghiêm trọng, 6 trung bình (2-05→3-01, 5-07, 5-11/5-12, 6-04→6-05, 7-05, 4-00/4-02), 7 nhẹ. Cấu trúc bảy mạch, trang "Nội dung" và `#/N`, hai trang "Vấn đề trung tâm", mạch "Tổng kết", liên kết viewer và thứ tự khái niệm theo ghi chú đều đạt. Các phát hiện trung bình cùng một dạng: câu nối giữa các mạch hoặc nửa mạch (giới hạn nào tạo bước tiếp) chỉ nằm trong ghi chú diễn giả; mỗi chỗ sửa bằng một dòng trên mặt trang lấy từ câu có sẵn trong ghi chú.
