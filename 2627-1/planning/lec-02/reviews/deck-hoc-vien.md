# Duyệt deck Bài 02 — vai học viên cao học (`hoc-vien`)

Deck đóng băng: `2627-1/lecture-02-bat-dang-thuc-tap-trung.html` (55 trang). Đọc như người nghe lần đầu, đã đọc trước `materials/lec-02/lecture-note.md`. Đối chiếu `storyboard.md` (mục 11, 15) và cuối `review-log.md`, mục "Bộ trang chiếu".

Cách kiểm:

- `deck_check.py --shots` tại `http://localhost:8766/` (ảnh 1600×900, 390×844 và ảnh `-end` sau khi cuộn tới cuối; xem hết bằng mắt).
- Hai script riêng trong thư mục nháp: đo chỗ nội dung chạm chân trang ở 16:9 (1600×900 và 1280×720); đo khối chữ rộng hơn 390 px ở chế độ đọc màn hẹp.
- Đếm lại mật độ mọi trang, có tính số trong câu (bảng cuối tệp).

Kết quả máy: console 0, page errors 0, failed 0, không `.katex-error`. Cờ OVERFLOW ở 4-02, 4-04, 4-05, 5-03, 5-08 là đuôi SVG của `\sqrt` (báo động giả đã biết). Trang không cuộn ngang ở 390 px (`docScrollW = 390`).

## Bảng phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | L02-3-05, L02-5-04, L02-5-10 | Ở 390 px, chữ của danh sách bước bị cắt ở mép phải và không đọc được. Công thức hiển thị nằm trong `li` làm cả danh sách rộng ra; vùng cuộn ngang tại chỗ chỉ áp dụng cho công thức, không cho chữ. Đây là ba trang "Ý tưởng chứng minh" của Hoeffding, hội tụ đều và rủi ro vượt mức. | Đo ở 390×844: mọi `li` của 3-05 rộng 537 px (mép phải 593 px), của 5-04 rộng 469 px (mép phải 525 px), của 5-10 rộng 589 px (mép phải 645 px). Ảnh `narrow-018-L02-3-05.png`: "Phương pháp Chernoff cho $\bar V_m-\bar\mu$…", "tách tích (giả thiết độ…", "số mũ b…" bị cắt; `narrow-030-L02-5-04.png`: "Hệ quả 02.10…", "(union b…" bị cắt; `narrow-036-L02-5-10.png`: "nó xác định…", "với mọ…", "đại diệ…" bị cắt. | Cho công thức hiển thị trong `li` một vùng cuộn riêng có `max-width:100%` và `overflow-x:auto` (quy tắc trong `lecture-course.css` hoặc bọc `div.formula`), hoặc đưa công thức ra ngoài `ol`, đặt ngay sau bước. Chụp lại ba trang ở 390 px. |
| nghiêm trọng | L02-3-02, L02-5-08 | Ở 16:9, dòng cuối đè lên chân trang. | Đáy dòng cuối ở 876 px và 879 px, chân trang bắt đầu ở 863 px (1600×900); ở 1280×720 là 701 px và 703 px so với 690 px. Ảnh `wide-015-L02-3-02.png`: "$e^{0{,}5}\approx1{,}649$." chồng lên "Lý thuyết học thống kê · …". Ảnh `wide-034-L02-5-08.png`: "$K$ thêm khoảng $0{,}005$." chồng lên chân trang. | 3-02: rút dòng ví dụ thành "**Ví dụ.** $V=\ell_{0\text{-}1}(h_3,Z)$, $\tau=2$: $1{,}549\le e^{0{,}5}\approx1{,}649$", vì phép tính vế trái đã có trong ghi chú diễn giả, hoặc thu hình. 5-08: rút dòng dữ kiện thứ hai (xem phát hiện về 5-08 bên dưới), hoặc đưa vế "gấp năm lần $K$ …" vào ghi chú diễn giả. |
| trung bình | L02-3-03 | Kí hiệu $\varphi$ xuất hiện ở bước 2 dưới dạng "$\le e^{\varphi(u)}$" mà không được định nghĩa trên mặt trang. Bước 3 ("$\varphi(0)=\varphi'(0)=0$; $\varphi''$ là phương sai Bernoulli") và bước 4 vì thế không theo được tại chỗ: người học không biết $\varphi$ là hàm nào. | Mặt trang: "lấy kì vọng: $\mathbb Ee^{\tau W}\le e^{\varphi(u)}$, $u=\tau(b-a)$." Định nghĩa $\varphi(u)=-\theta u+\ln(1-\theta+\theta e^u)$ chỉ có trong ghi chú diễn giả. Ghi chú bài giảng, chứng minh Bổ đề 02.6, nêu $\varphi$ trước khi dùng. | Ở bước 2, gọi tên $\varphi$ bằng lời: "…, với $\varphi(u)$ là lôgarit của vế phải dây cung", hoặc thêm một dòng "Kí hiệu:" với công thức $\varphi(u)=-\theta u+\ln(1-\theta+\theta e^u)$, $\theta=-a'/(b'-a')$. Trang có 47–50 âm tiết, còn chỗ cho khoảng 8 âm tiết. |
| trung bình | L02-5-10 | (O2) và $\epsilon_{\mathrm{opt}}$ dùng trên mặt trang nhưng chưa có ở trang trước nào của deck. Bảng giả thiết 2-01 chỉ có (T1)–(T4) và (O1). | 5-10: "Bỏ (O1): dấu $\le$ thứ hai hỏng; với (O2), cộng thêm $\epsilon_{\mathrm{opt}}$." (O2) chỉ có trong ghi chú diễn giả 2-01 và 5-09. Ghi chú bài giảng §2 liệt kê (O2) cùng các giả thiết khác. | Thêm hàng "(O2) \| $L_S(\hat h)\le\min_{h\in\mathcal H}L_S(h)+\epsilon_{\mathrm{opt}}$" vào bảng 2-01 (ô bảng không tính âm tiết), hoặc viết thẳng ở 5-10: "với nghiệm ERM xấp xỉ, $L_S(\hat h)\le\min_hL_S(h)+\epsilon_{\mathrm{opt}}$, vế phải cộng thêm $\epsilon_{\mathrm{opt}}$". |
| trung bình | L02-6-04 | Ví dụ bốn mức cỡ mẫu đi quá nhanh. Mặt trang cho bốn số 48, 37, 30, 14 nhưng không nói vì sao mỗi bước giảm, nên người học không giải thích được các số $\ln40$ và $\ln20$. Câu "Các ngưỡng xấu nhất quán với tập huấn luyện lồng nhau thành hai chuỗi." không giải nghĩa được tại chỗ: hai chuỗi nào, và vì sao lồng nhau thì số hạng giảm. "Diễn giải:" chỉ nói chung chung. | Lý do "chỉ cần $2e^{-\epsilon m}\le\delta$" (37) và "$\hat t\ge t^\star$, chỉ còn chuỗi bên phải" (30) chỉ có trong ghi chú diễn giả. Ghi chú bài giảng, Ví dụ 02.11, Bước 1–4, viết từng bước. | Thêm một cột "Số số hạng của bất đẳng thức hợp": $6$; $2$ (hai chuỗi, trái và phải $h^\star$); $1$ ($A_{\max}$ chỉ chọn ngưỡng $\ge3$); "tính chính xác". Thay câu "lồng nhau thành hai chuỗi" bằng "Ngưỡng xấu bên trái (phải) $h^\star$ nhất quán thì ngưỡng xấu gần $h^\star$ nhất bên đó cũng nhất quán." Số trong bảng không tính âm tiết, nên trang không vượt trần. |
| trung bình | L02-1-02, L02-7-06 | Vượt trần 60 âm tiết khi tính số trong câu, và `storyboard.md` không ghi ngoại lệ. Mục 15 của storyboard ghi 60 và 57 theo cách đếm của máy, vốn bỏ các token chỉ gồm chữ số. | 1-02: 64 âm tiết (máy 60; thêm "01.7", "01.16", "01.18,", "01.25)."; đếm tay: 11 + 11 + 11 + 19 + 12). 7-06: 61 (máy 57; thêm "(2014),", "B.1–B.4:", "§2.3.1:", "§§4.1–4.2:"…). | 1-02: bỏ số hiệu ở dòng "Nhắc lại:" thứ hai, giữ "(Định nghĩa 01.16)", và viết "học PAC khả diễn, bất khả diễn (Bài 01)", vì cả hai có tên trên mặt trang. 7-06: gộp hai dòng UML §2.3.1 và §§4.1–4.2 thành một dòng. Hoặc ghi ngoại lệ có số âm tiết vào storyboard. |
| trung bình | L02-2-03, L02-3-02, L02-5-08, L02-6-06 | Chữ trong hình (số trên trục, nhãn số liệu) quá nhỏ: khoảng 0,41–0,45 lần cỡ chữ thân trang ở 1600×900, khoảng 10 px ở 390 px. Trên 2-03, nhãn "m = 6", "0,12; 0,22; 0,32" và tên trục "rủi ro thực nghiệm k/m" khó đọc từ xa. Trên 6-06, các nhãn "165 881", "1 659", "761", "77" nhỏ và đè lên đường. | SVG dùng `font-size` 17–19 trong `viewBox` rộng 600, hiển thị rộng 443–523 đơn vị trang khi chữ thân trang là 34. Ảnh `narrow-009-L02-2-03.png`, `narrow-045-L02-6-06.png`, `wide-015-L02-3-02.png` (nhãn "1,549" bị nét đứt của dây cung cắt qua). | Tăng `font-size` trong SVG lên khoảng 26–30, hoặc thu `viewBox`. Bỏ nhãn trùng với chữ trên trang. Dời nhãn "1,549" ra khỏi dây cung. Theo quy định deck, chữ dưới 0,65 em chỉ dùng cho chú thích ngắn đã được người duyệt xác nhận là đọc được; tôi không xác nhận được ở đây. |
| nhẹ | L02-3-04, L02-4-02, L02-5-03 | Dòng "Trực quan." chỉ nhắc lại kết quả hoặc bước chứng minh, không giải thích vì sao kết quả đúng. | 3-04: "Bổ đề Hoeffding chặn từng thừa số của tích Chernoff chỉ qua độ dài $b-a$" là bước 2 của 3-05. 4-02: "Bán kính tin cậy … giảm như $1/\sqrt m$" là phần (b). 5-03: "thay $\ln(2/\delta)$ bằng $\ln K+\ln(2/\delta)$" là phần (a). | 5-03: "Mỗi giả thuyết nhận xác suất thất bại $\delta/K$; cận đuôi giảm theo hàm mũ, nên chỉ phải trả thêm $\ln K$." 4-02: đưa câu "gấp bốn cỡ mẫu thì bán kính giảm một nửa" từ ghi chú diễn giả lên mặt trang. 3-04: "Mỗi quan sát độc lập nhân thêm vào tích Chernoff một thừa số bị chặn theo $b-a$, nên cận giảm theo hàm mũ của $m$." Ý của 4-02 và 5-03 đã có trong ghi chú diễn giả 4-02 và 5-05. |
| nhẹ | L02-2-03 | Ba xác suất và ba cỡ mẫu được ghép theo vị trí, nên khó đọc ngay. | "$V=L_S(h_3)$, $\epsilon=0{,}1$: $0{,}6189$; $0{,}0211$; $8{,}9\cdot10^{-4}$ tại $m=6$; $100$; $200$." Ở 390 px, "$;200$" rơi xuống dòng riêng. | "$\epsilon=0{,}1$: $m=6$: $0{,}6189$; $m=100$: $0{,}0211$; $m=200$: $8{,}9\cdot10^{-4}$." |
| nhẹ | L02-2-01 | Bốn đại lượng cần chặn viết liền trong một dòng, ngăn bằng dấu chấm phẩy, nên khó tách từng đại lượng. Quy tắc giọng tác giả: ba mục song song trở lên viết thành danh sách. | "$\lvert L_S(h)-L_D(h)\rvert$ với $h$ cố định; $\sup_{h\in\mathcal H}\lvert\cdot\rvert$; rủi ro vượt mức (excess risk) …; $L_D(\hat h)$ khi $(D,\mathcal H)$ khả diễn." | Viết thành danh sách bốn dòng. Nếu vượt sáu dòng, đưa bảng giả thiết lên trước hoặc gộp (T2), (T3) như hiện nay. |
| nhẹ | L02-2-02 | $D_\eta$ dùng trong bảng ($L_{D_\eta}(h_t)$) và ở các trang sau nhưng không được gọi tên trên mặt trang. Người học phải tự ghép $\eta$ với $D_\eta$. | Mặt trang: "$\eta(x)=\Pr(Y=1\mid X=x)$ tại …". Tên "$D_\eta$" chỉ có trong ghi chú diễn giả. Phát hiện cùng loại ở deck 01 (L01-2-02) đã được sửa. | "Phân bố có nhiễu $D_\eta$: $\eta(x)=\Pr(Y=1\mid X=x)$ tại …". |
| nhẹ | L02-6-01 | Dòng "Nhắc lại:" đứng sau công thức đã dùng bất đẳng thức được nhắc lại. | Công thức hiển thị "$\ldots<(1-\epsilon)^m\le e^{-\epsilon m}$" đứng trước "**Nhắc lại:** chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ (Bài 01)". | Đưa dòng "Nhắc lại:" lên trên dòng "Trực quan.". |
| nhẹ | L02-5-08 | Câu điều kiện hóa khó hiểu tại chỗ: "dữ liệu huấn luyện các ứng viên" là dữ liệu nào, và vì sao ứng viên thành cố định. | "Khi biết dữ liệu huấn luyện các ứng viên, $K$ ứng viên cố định đối với $S$." Ghi chú diễn giả và Ví dụ 02.8 dùng dữ liệu huấn luyện $T$. | "Khi biết dữ liệu huấn luyện $T$, $K$ ứng viên cố định và $S\sim D^m$." |
| nhẹ | L02-6-07 | Số $2\,362\,000$ xuất hiện trong lời giải mà không có nguồn gốc. | "Bất khả diễn: $\lceil2\ln2\,362\,000/0{,}01\rceil$". | "$\lceil2\ln(2K/\delta)/\epsilon^2\rceil$, $2K/\delta=2\,362\,000$: $\lceil2935{,}004\rceil=2936$". |
| nhẹ | L02-7-04 | Câu hỏi 1 viết tắt đến mức chủ ngữ không rõ: tỉ lệ lỗi 8% là của hàm nào. Tính cả số trong câu, dòng này 24 âm tiết, trên trần 20. | "Chọn trong $200$ ứng viên, tỉ lệ lỗi $8\%$ trên $2000$ quan sát: tính cận trên tin cậy $95\%$; cận đúng cho hàm nào?" | "Hàm chọn trong $200$ ứng viên có tỉ lệ lỗi $8\%$ trên $2000$ quan sát xác thực. Tính cận trên tin cậy $95\%$." Đưa vế "cận đúng cho hàm nào" thành câu hỏi riêng, hoặc bỏ. |
| nhẹ | L02-1-03 | "hệ số số ứng viên" lặp chữ "số" và lệch câu chữ của ghi chú. | Mục tiêu 6: "Dựng phản ví dụ khi bỏ độc lập, bị chặn hoặc hệ số số ứng viên." Ghi chú bài giảng, Mục tiêu 6: "hệ số đếm số ứng viên trong bất đẳng thức hợp". | "… hoặc hệ số đếm số ứng viên." (thêm 1 âm tiết, 80 = trần). |
| nhẹ | L02-5-09, L02-7-03 | 7-03 dẫn "Ví dụ 02.9", nhưng ví dụ tương ứng ở 5-09 không ghi số. Người học không biết $1097$ ở đâu ra. | 5-09: "**Ví dụ.** Sáu hàm ngưỡng, … $M=\lceil1096{,}1\rceil=1097$". 7-03: "so với cỡ mẫu $1097$ của Ví dụ 02.9". | Ở 5-09 ghi "**Ví dụ** (Ví dụ 02.9)", hoặc ở 7-03 viết "cỡ mẫu $1097$ của sáu hàm ngưỡng ở trang Hệ quả 02.16". |
| nhẹ | L02-3-04, L02-4-01, L02-5-01, L02-2-00, L02-6-00, L02-1-05 | Dòng vượt trần mà storyboard không ghi lý do. Dòng nội dung trên 20 âm tiết: 3-04 (21), 4-01 (21; storyboard chỉ liệt kê, không nêu lý do), 5-01 (21 khi tính số). Dòng dẫn mạch trên 25 âm tiết: 2-00 (28), 6-00 (26). Hộp Vấn đề trung tâm 1-05 có 35 âm tiết, trong khi điều phối viên chọn "bản ngắn (≈ 28 âm tiết)" theo khuôn ≤ 30. | Đếm bằng script trong thư mục nháp (bảng dưới). 2-00: "Kì vọng và phương sai chặn được xác suất tỉ lệ lỗi lệch xa rủi ro kì vọng, nhưng cận chỉ giảm tỉ lệ nghịch với cỡ mẫu." (28). | 2-00: "Kì vọng và phương sai chặn được xác suất đuôi, nhưng cận chỉ giảm tỉ lệ nghịch với cỡ mẫu." 6-00: bỏ "theo độ chính xác" hoặc "giả thuyết" thứ hai. 1-05: điều phối viên xác nhận 35 âm tiết hoặc rút "kể cả khi giả thuyết được chọn theo tập huấn luyện" thành "kể cả với giả thuyết chọn theo dữ liệu". 3-04, 4-01: ghi lý do vào storyboard mục 15. |

Không có phát hiện nào ở mức chặn bàn giao.

Các điểm đã kiểm, không có phát hiện:

- Hành trình khái niệm của Markov và Chebyshev (2-02 → 2-06) và của cận tin cậy (4-01 → 4-05) đủ chậm để theo.
- Câu nối mặt trang 2-06 → mạch 3 và 4-05 → mạch 5 có.
- Các "Diễn giải:" chỉ dùng số có trên trang. Riêng $0{,}005$ ở 5-08 là số của ghi chú, đã ghi ở `review-log.md`.
- Số trang 55 bằng trần, lý do ở storyboard mục 15.
- Phím điều hướng không thuộc phạm vi kiểm của vai này.

## Mật độ (mọi trang)

"máy": số của `deck_check.py` (token có chữ cái, bỏ tiêu đề, KaTeX, hình, ô bảng toàn số, ghi chú diễn giả). "+số chữ": cộng thêm token chỉ gồm chữ số trong câu (số hiệu kết quả, năm, mục UML). "+số KaTeX": cộng thêm mỗi công thức KaTeX trong câu chỉ là một số (ví dụ $1000$, $0{,}05$, $95\%$). "dòng dài nhất" theo cột cuối. Trần: 60 cho trang nội dung; 80 cho Mục tiêu, Nội dung, bảng tổng kết (1-03, 1-04, 7-01); 20 âm tiết mỗi dòng; 25 cho dòng dẫn mạch.

| Trang | máy | +số chữ | +số KaTeX | dòng dài nhất | Trang | máy | +số chữ | +số KaTeX | dòng dài nhất |
|---|---|---|---|---|---|---|---|---|---|
| 1-01 | 60 | 63 | 63 | 39 | 1-02 | 60 | 64 | 64 | 19 |
| 1-03 | 79 | 79 | 79 | 16 | 1-04 | 48 | 48 | 48 | 12 |
| 1-05 | 35 | 35 | 35 | 35 | 1-06 | 51 | 51 | 53 | 19 |
| 2-00 | 41 | 41 | 41 | 28 | 2-01 | 48 | 48 | 48 | 12 |
| 2-02 | 23 | 25 | 25 | 18 | 2-03 | 30 | 30 | 35 | 18 |
| 2-04 | 44 | 46 | 46 | 18 | 2-05 | 47 | 48 | 48 | 17 |
| 2-06 | 37 | 37 | 39 | 15 | 3-00 | 34 | 34 | 34 | 23 |
| 3-01 | 43 | 44 | 44 | 17 | 3-02 | 40 | 41 | 41 | 18 |
| 3-03 | 47 | 47 | 50 | 15 | 3-04 | 50 | 51 | 51 | 21 |
| 3-05 | 51 | 51 | 51 | 14 | 4-00 | 38 | 38 | 38 | 25 |
| 4-01 | 53 | 53 | 54 | 21 | 4-02 | 45 | 46 | 46 | 13 |
| 4-03 | 41 | 43 | 43 | 12 | 4-04 | 39 | 39 | 42 | 15 |
| 4-05 | 36 | 36 | 39 | 18 | 4-06 | 45 | 45 | 47 | 20 |
| 5-00 | 39 | 39 | 39 | 25 | 5-01 | 52 | 53 | 56 | 21 |
| 5-02 | 41 | 42 | 43 | 15 | 5-03 | 50 | 51 | 51 | 11 |
| 5-04 | 47 | 48 | 48 | 17 | 5-05 | 40 | 41 | 41 | 20 |
| 5-06 | 52 | 52 | 52 | 17 | 5-07 | 52 | 53 | 55 | 16 |
| 5-08 | 37 | 38 | 43 | 15 | 5-09 | 56 | 57 | 58 | 19 |
| 5-10 | 46 | 46 | 46 | 12 | 5-11 | 42 | 43 | 43 | 20 |
| 5-12 | 59 | 59 | 59 | 59 | 6-00 | 45 | 45 | 45 | 26 |
| 6-01 | 59 | 60 | 60 | 19 | 6-02 | 45 | 47 | 47 | 19 |
| 6-03 | 48 | 49 | 49 | 16 | 6-04 | 55 | 55 | 55 | 16 |
| 6-05 | 41 | 41 | 42 | 15 | 6-06 | 37 | 37 | 39 | 20 |
| 6-07 | 47 | 47 | 51 | 20 | 6-08 | 54 | 54 | 56 | 16 |
| 7-00 | 25 | 25 | 25 | 25 | 7-01 | 68 | 75 | 75 | 0 |
| 7-02 | 58 | 58 | 58 | 20 | 7-03 | 56 | 58 | 60 | 17 |
| 7-04 | 54 | 55 | 59 | 24 | 7-05 | 45 | 45 | 45 | 6 |
| 7-06 | 57 | 61 | 61 | 15 | | | | | |

Trang vượt trần 60 khi tính số: 1-02 (64), 7-06 (61). Bìa 1-01 có 63, trong đó có dòng tên học phần và năm học bắt buộc. Theo cách đếm của máy, mọi trang ≤ 60, trừ 7-01 (68 máy, 75 khi tính số; trần 80). Các trang sát trần khi tính số: 6-01 (60), 7-03 (60), 7-04 (59), 5-12 (59, ngoại lệ đã ghi). Mọi trang ≤ 6 dòng nội dung, ≤ 1 công thức hiển thị (máy), ≤ 1 hộp chữ.

## Kết luận

**đạt khi sửa.** Hai phát hiện nghiêm trọng (chữ bị cắt ở 390 px trên ba trang ý tưởng chứng minh; dòng cuối đè chân trang ở 3-02, 5-08) và sáu phát hiện trung bình cần sửa trước khi bàn giao. Sau khi sửa, cần chụp lại 3-02, 3-03, 3-05, 5-04, 5-08, 5-10, 6-04 ở 1600×900 và 390×844.

## Đề xuất sửa ghi chú

Không có. Các chỗ người học vấp đều nằm ở mặt trang deck. Ghi chú bài giảng có đủ định nghĩa $\varphi$, (O2) và các bước của Ví dụ 02.11.
