# Kiểm lại sau biên tập deck Bài 02, lượt 1 (chỉ đọc)

Vai: kiểm lại sau biên tập. Deck: `2627-1/lecture-02-bat-dang-thuc-tap-trung.html` (55 trang), hình `2627-1/img/lec-02/`. So với bản đóng băng trong thư mục nháp `…/scratchpad/lec-02/master/frozen/`. Đầu vào: năm báo cáo `reviews/deck-*.md`, quyết định của điều phối viên (`review-log.md`, mục "Năm báo cáo duyệt và quyết định của điều phối viên"), bảng sửa `storyboard.md` mục 16, `materials/lec-02/lecture-note.md`, `exercises.md`. `no-ai-slop` chế độ Detect trên mọi câu mới hoặc đã sửa.

## Cách kiểm

- Diff theo trang (script `slides.py` trong thư mục nháp `…/scratchpad/lec-02/recheck/`): 49/55 trang đổi (mặt trang hoặc ghi chú diễn giả); ba SVG đổi (`day-cung.svg`, `hai-toc-do.svg`, `tap-trung.svg`).
- `deck_check.py --shots` (thư mục nháp `recheck/dc/`): slides=55, console 0, pageerrors 0, failed 0, không `.katex-error`. OVERFLOW chỉ ở 4-02, 4-04, 4-05, 5-03, 5-08, 6-06, đều là `path` SVG của `\sqrt` (báo động giả đã biết). SYLL ở 7-01 (63) là cờ sai do so khóa "Tổng kết" (trần 80).
- `footer_check.py`: 0 trang ở 1600×900 và 0 trang ở 1280×720.
- 390×844: `docScrollW = 390` ở mọi trang. Script `narrow_clip.py` tìm phần tử vượt mép phải mà không nằm trong vùng cuộn: không có. Các cờ NARROW-H của `deck_check` là công thức/bảng cuộn tại chỗ. Đã xem ảnh 390 px và ảnh `-end` của 3-05, 5-04, 5-10, 2-01, 2-03, 3-01, 3-03, 3-04, 4-01, 5-06, 5-08, 5-09, 5-12, 6-04, 7-01, 7-03; ảnh 1600×900 của 37 trang đổi mặt.
- Tính lại bằng Python mọi số trên nội dung đổi (mục "Toán").

## 1. Phát hiện được chấp nhận → trạng thái

### Phát hiện nghiêm trọng và các mục điều phối viên nêu riêng

| Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|
| Học viên, nghiêm trọng: chữ bị cắt ở 390 px (3-05, 5-04, 5-10) | đã sửa | Sửa CSS 9c34228; ảnh `narrow-018/030/036`: chữ xuống dòng, công thức cuộn tại chỗ; `narrow_clip.py` không thấy phần tử ngoài vùng cuộn |
| Học viên, nghiêm trọng: 3-02, 5-08 đè chân trang | đã sửa | `footer_check.py` 0 trang ở 1600×900 và 1280×720; 3-02 dòng ví dụ "$1{,}549\le e^{0{,}5}\approx1{,}649$", phép tính ở ghi chú diễn giả |
| Bảng so ba cận ở 3-04 (chuyên gia 1, mạch truyện 4) | đã sửa | Bảng chính xác / Chebyshev $25/m$ / Hoeffding $2e^{-0{,}02m}$ tại $m=100,200$: $0{,}0211$, $0{,}25$, $0{,}2707$; $8{,}9\cdot10^{-4}$, $0{,}125$, $0{,}0366$ (đều đúng). "Diễn giải: ở $m=100$, cận Hoeffding lớn hơn cận Chebyshev; ở $m=200$, nhỏ hơn." chỉ dùng số trên trang; không thêm trang |
| 5-08 "Diễn giải:" trả lời câu hỏi thứ hai của 1-06 bằng $0{,}1204$ | đã sửa (một điểm nhẹ ở bảng 4) | "với độ tin cậy $95\%$, hàm chọn trong $1000$ ứng viên có rủi ro kì vọng không quá $0{,}1204$"; "khoảng $0{,}005$" đã bỏ khỏi mặt trang; trang có thêm dữ kiện $L_S(\hat h)=0{,}05$ |
| 6-05 "Lưu ý" | đã sửa | "cột ước lượng dùng $\epsilon$ là độ lệch; khi $D$ khả diễn, hai cột sau so được." khớp lời giải Bài tập 02.8(d); ghi chú diễn giả nêu lý do (rủi ro vượt mức bằng rủi ro) |
| 7-01 ô Markov–Chebyshev | đã sửa | "$V\ge0$; không tương quan từng đôi", khớp 2-05; Mệnh đề 02.17 thêm "hàm lỗi 0–1" (xem phát hiện mới về cột "Kết quả") |
| 5-06 nhãn "Học viên:" | đã sửa | Hộp mở bằng "**Câu hỏi:** một học viên lập luận: "…"", câu trích đúng nguyên văn `exercises.md` Bài tập 02.4, có "Hệ quả 02.10(a)" |
| 1-02 (64), 7-06 (61) | đã sửa | Máy 55 và 49; cộng số trong câu ≈ 56 và ≈ 53 |
| Hộp Vấn đề trung tâm ≤ 30 âm tiết | sửa chưa đủ | Đếm tay phần sau nhãn: 31 âm tiết (bảng 4) |

### Các phát hiện còn lại

Đối chiếu từng hàng của `storyboard.md` mục 16 với diff: học viên 3–18, toán học P1–P14, chuyên gia 2–13, sư phạm 1–38, mạch truyện 1–14, 16, 17 đều có thay đổi tương ứng trên deck và đúng nội dung đã ghi. Các điểm cần ghi rõ:

| Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|
| Học viên 3 / chuyên gia 10: $\varphi$, $\mathbb EW=0$ ở 3-03 | đã sửa | "lấy kì vọng, dùng $\mathbb EW=0$ … $\varphi(u)=-\theta u+\ln(1-\theta+\theta e^u)$, $\theta=-a'/(b-a)$"; bước 1 có $b'-a'=b-a$, nên khớp $\theta=-a'/(b'-a')$ của ghi chú diễn giả |
| Học viên 4: (O2) ở 5-10 | đã sửa | "với nghiệm ERM xấp xỉ (O2), $L_S(\hat h)\le\min_hL_S(h)+\epsilon_{\mathrm{opt}}$" |
| Học viên 5: 6-04 | đã sửa | Cột "Số hạng" $6;2;1;$—; "Diễn giải:" nêu hai chuỗi lồng nhau (xem phát hiện mới về $t^\star$) |
| Học viên 18 / mạch truyện: dòng dẫn 6-00 | sửa chưa đủ | Bảng sửa ghi 22 âm tiết; đếm tay 27 (máy 26) > 25 (bảng 4) |
| Toán P1 / chuyên gia 7: 5-09 loại bảo đảm | đã sửa | "với xác suất $\ge0{,}95$, $L_{D_\eta}(\hat h)\le0{,}32$" (xem phát hiện mới về dòng (c) và lớp của ví dụ) |
| Toán P2 / chuyên gia 5: 7-02 | đã sửa | Câu dẫn "Với xác suất ít nhất $1-\delta$ theo $S$:"; dòng khả diễn "$L_D(\hat h)\le\epsilon$" |
| Toán P3: 7-03 giả thiết phần (a) | sửa chưa đủ | Thêm "(T1), (T4), $0\le a\le\ell\le b$" nhưng đồng thời bỏ "học PAC bất khả diễn với" (bảng 4) |
| Toán P5 / chuyên gia 9: 3-01 | đã sửa | "(a) $V$ bất kì …; (b) … $V_i$ độc lập", $\overset{(a)}{\le}$, $\overset{(b)}{=}$ |
| Toán P7: 4-06 | đã sửa | "cận sai" / "cận không cho thông tin"; "Lưu ý:" có "$\epsilon\in(0,1]$", "$m\to\infty$", khớp Nhận xét 02.11 |
| Toán P8: 4-01 | đã sửa | "$\Pr[\underline L_\delta(S)\le L_D(h)\le\overline L_\delta(S)]\ge1-\delta$, mọi $D$", khớp Định nghĩa 02.9 |
| Chuyên gia 4: 6-06 | đã sửa | "cỡ mẫu đủ tỉ lệ với $1/\epsilon^2$"; câu hỏi 7-04 và ghi chú diễn giả dùng "cỡ mẫu đủ" |
| Mạch truyện 1, 2: câu nối 5-01→5-02, 5-08→5-09 | đã sửa | Dòng đầu 5-02; dòng cuối 5-08 (xem gợi ý nhẹ ở bảng 4) |
| Mạch truyện 12: Bài tập 02.6 | đã sửa | 7-05 hàng mạch 5: "02.3, 02.4, 02.5, 02.6, 02.11" |
| Sư phạm 10 / 5-06 câu chữ bài tập | sửa chưa đủ | Ý (b), (c) rút gọn so với `exercises.md` (bảng 4) |

### Các mục "không sửa"

| Mục | Đánh giá |
|---|---|
| Chữ trong hình ≈ 10 px ở 390 px | hợp lý: điều phối viên đã chấp nhận như giới hạn của Bài 01; nhãn "1,549" đã ra khỏi dây cung, cột $k=2$ của `tap-trung.svg` nằm trọn bên phải vạch $0{,}32$ (ảnh 2-03) |
| 7-03 giữ $17\,538{,}04$ theo `exercises.md` | hợp lý: $16\cdot1096{,}128=17\,538{,}04$ đúng; sai lệch $\ln240\approx5{,}4806$ đã vào đề xuất cho tác giả |
| Deck 01 "$>\epsilon$" (mạch truyện 15) | hợp lý: ngoài phạm vi deck 02, theo quyết định |
| Không thêm hàng (O2) vào bảng 2-01 | hợp lý: 5-10 viết thẳng (O2) tại chỗ dùng |
| Không thêm câu khép mạch 4 ở 4-06 | hợp lý: 4-06 đã sáu dòng; 5-00 và 5-01 nối sang mạch 5 |
| 5-01 không thêm câu so $0{,}00593$ với $0{,}9974$ | hợp lý: hai số ở hai dòng ngay trên, trang 55–57 âm tiết |
| 5-09 giữ "Trực quan." | hợp lý: câu nêu hai phép so tạo hệ số $2$ (cơ chế) |

## 2. Toán trên nội dung đã đổi

Tính lại bằng Python, đều khớp:

- 2-03: $\Pr(\lvert L_S(h_3)-0{,}22\rvert\ge0{,}1)$ dưới $D_\eta$: $0{,}61889$ ($m=6$), $0{,}02115$ ($m=100$), $8{,}94\cdot10^{-4}$ ($m=200$).
- 3-04: $2e^{-2}=0{,}2707$, $2e^{-4}=0{,}0366$; $25/m=0{,}25$; $0{,}125$; $25/m<2e^{-0{,}02m}$ đúng đến $m=107$ (ghi chú diễn giả).
- 4-06: $2e^{-8}=6{,}71\cdot10^{-4}$; $2e^{-2/m^3}\approx2$; $(1-10^{-4})^{100}=0{,}9900$.
- 5-01: $1-(1-0{,}00593)^{1000}=0{,}9974$.
- 5-08: $\sqrt{\ln20\,000/2000}=0{,}07037$, cận $0{,}1204$; $K=5000$: $0{,}0759$, $0{,}1259$; $K=1$: $0{,}0387$.
- 5-09: $200\ln240=1096{,}13$, $M=1097$.
- 6-04: $\ln120/0{,}1=47{,}87\to48$; $\ln40/0{,}1=36{,}89\to37$; $\ln20/0{,}1=29{,}96\to30$; $0{,}8^{14}=0{,}0440$, $0{,}8^{13}=0{,}0550$.
- 6-06: $\ln2000/\epsilon$: $76{,}01\to77$, $760{,}09\to761$; $2\ln4000/\epsilon^2$: $1658{,}81\to1659$, $165\,880{,}99\to165\,881$.
- 6-07: $2\cdot59\,050/0{,}05=2\,362\,000$; $(\ln59\,050+\ln20)/0{,}1=139{,}82\to140$; $200\ln2\,362\,000=2935{,}004\to2936$.
- 6-08: $1000/(4\cdot0{,}05\cdot0{,}05^2)=2\,000\,000$; $\ln40\,000/0{,}005=2119{,}3\to2120$.
- 7-03: $32\cdot5{,}4806/0{,}01=17\,537{,}92$ (số của tệp bài tập $17\,538{,}04$ ứng với $\ln240$ đầy đủ; đã ở đề xuất cho tác giả).
- 7-04 (ghi chú diễn giả): $\sqrt{\ln4000/4000}=0{,}0455$, cận $0{,}1255\approx0{,}126$.

Phát biểu: 3-01 (a)/(b), 3-03 ($\theta$), 4-01 (Định nghĩa 02.9), 4-06 (Nhận xét 02.11), 5-04 ($\{S$ không là $r$-đại diện$\}\subseteq\bigcup_hB_h$), 5-12 (biến cố $\sup_h\lvert L_S-L_D\rvert\le r$, đúng Định nghĩa 02.13 với "$\le$"), 7-01, 7-02 khớp ghi chú. Hai chỗ bỏ loại bảo đảm mới phát sinh ở 5-09 dòng (c) và 7-03 (bảng 4).

## 3. Mạch truyện trên trang đổi ±2 và ranh giới mạch

- 1-05 → 1-06 → 2-00: câu hỏi thứ hai của 1-06 nay là câu đủ ("…, câu trả lời thay đổi thế nào?"); 4-05 trả lời câu thứ nhất, 5-08 trả lời câu thứ hai.
- 2-06 → 3-00 … 3-04 → 3-05 → 4-00: bảng 3-04 nối thẳng bảng Chebyshev của 2-06 và dẫn tới 4-04 (cỡ mẫu theo $\delta$); dòng dẫn mạch 3 "cận giảm theo hàm mũ" không còn trông trái với số ở $m=100$, vì "Diễn giải:" nói rõ đổi chiều ở $m=200$.
- 4-05 → 4-06 → 5-00 → 5-01 → 5-02: bỏ dòng cuối 4-05 không làm mất điều kiện ($h$ cố định ở dòng dữ kiện đầu); câu nối mới ở đầu 5-02 đúng chỗ.
- 5-06 … 5-08 → 5-09 → 5-10: dòng cuối 5-08 dẫn sang rủi ro vượt mức; 5-10 nay tự đủ về (O2).
- 6-00 → 6-01 → 6-02; 6-04 → 6-05 → 6-06 → 6-07: "Lưu ý" mới của 6-05 hết mâu thuẫn với so sánh ở 6-06, 6-07.
- 7-00 → 7-01 → 7-02 → 7-03: ghi chú diễn giả 7-00 nay nêu nội dung (ba giả thiết, $\ln K$, hai tốc độ).
- Ranh giới mạch và liên kết `#/2`…`#/7` không đổi; từ khóa mạch 2 có "giả thiết (T1)–(T4)".

## 4. Phát hiện còn mở (lỗi mới hoặc sửa chưa đủ)

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L02-7-03 | Phát biểu phần (a) mất loại bảo đảm: "mọi thuật toán ERM có $M(\epsilon,\delta)=…$" không nói $M$ là cỡ mẫu của học PAC bất khả diễn. Bản đóng băng có "mọi thuật toán ERM học PAC bất khả diễn với …". Thiếu thêm (T2) và $a<b$. | Mặt trang: "Theo phần (a), với (T1), (T4), $0\le a\le\ell\le b$, mọi thuật toán ERM có $M(\epsilon,\delta)=\lceil…\rceil$." `exercises.md` Bài tập 02.11: "(T2) với $a\le\ell(h,z)\le b$ … $0\le a<b$ … mọi thuật toán ERM trên $\mathcal H$ là thuật toán học PAC bất khả diễn (Định nghĩa 01.25) với $M(\epsilon,\delta)$". | "Theo phần (a), với (T1), (T2), (T4), $0\le a\le\ell\le b$, $a<b$: mọi thuật toán ERM học PAC bất khả diễn với $M(\epsilon,\delta)=\lceil…\rceil$." Trang 52 âm tiết, còn chỗ. |
| trung bình | L02-7-01 | Cột "Kết quả" chỉ còn số hiệu; tên kết quả (Markov, Chebyshev, Hoeffding, cận tin cậy, hội tụ đều, rủi ro vượt mức, khả diễn) bị bỏ, không có phát hiện nào yêu cầu. Bảng tổng kết mất các từ khóa của bài; cột "Ý tưởng chứng minh" vẫn dùng tên "Markov", nên hàng đầu đọc như vòng tròn. | Bản đóng băng: "Markov, Chebyshev (Bổ đề 02.2, 02.3)", "Hoeffding (…)", "Hệ quả 02.10 (cận tin cậy)", "Định lý 02.14 (hội tụ đều)", "Hệ quả 02.16 (rủi ro vượt mức)", "Mệnh đề 02.17 (khả diễn)". Hiện tại: "Bổ đề 02.2, 02.3", "Hệ quả 02.10", …; máy đếm 63, trần 80. | Trả lại tên ngắn trong ô "Kết quả" như bản đóng băng; ước tính ≈ 78 âm tiết, dưới trần 80. |
| nhẹ | L02-1-05 | Hộp Vấn đề trung tâm còn 31 âm tiết, trên mức ≤ 30 điều phối viên yêu cầu; bảng sửa ghi 28. | Đếm tay sau nhãn: "cần bao nhiêu quan sát … kể cả với giả thuyết chọn theo tập huấn luyện?" = 31. | "…trên lớp giả thuyết hữu hạn, kể cả khi chọn giả thuyết theo dữ liệu?" (29). |
| nhẹ | L02-6-00 | Dòng dẫn mạch 27 âm tiết (máy 26, cộng "$0$"), trên trần 25; bảng sửa ghi 22. "tăng chậm hơn" thiếu đối tượng so sánh (bản cũ: "theo độ chính xác"). | "Khi lớp giả thuyết chứa một hàm có rủi ro $0$, chỉ cần loại các giả thuyết có rủi ro lớn, nên cỡ mẫu tăng chậm hơn." | "Khi lớp chứa một hàm có rủi ro $0$, chỉ cần loại giả thuyết có rủi ro lớn, nên cỡ mẫu tăng chậm hơn theo $1/\epsilon$." hoặc rút khác ≤ 25 mà giữ "lớp giả thuyết". |
| nhẹ | L02-5-09 | Dòng "(c) học PAC bất khả diễn với …" thiếu chủ ngữ, và nhãn "(c)" đứng một mình (không có (a), (b) trên trang); ghi chú diễn giả phải giải thích "Dòng (c) nói mọi thuật toán ERM là …". Dòng ví dụ bỏ lớp (sáu hàm ngưỡng, $K=6$) và điều kiện $m\ge1097$. | Mặt trang: "(c) học PAC bất khả diễn với $M(\epsilon,\delta)=…$"; "**Ví dụ.** (Ví dụ 02.9) $\epsilon=0{,}1$, $\delta=0{,}05$: $M=1097$; với xác suất $\ge0{,}95$, $L_{D_\eta}(\hat h)\le0{,}32$." Ghi chú Ví dụ 02.9: "với ít nhất $1097$ quan sát, mọi nghiệm ERM có …". | "Do đó mọi thuật toán ERM học PAC bất khả diễn với $M(\epsilon,\delta)=…$." Ví dụ: "(Ví dụ 02.9) Sáu hàm ngưỡng, $\epsilon=0{,}1$, $\delta=0{,}05$: $M=1097$; khi $m\ge1097$, với xác suất $\ge0{,}95$, $L_{D_\eta}(\hat h)\le0{,}32$." Bỏ câu giải thích (c) ở ghi chú diễn giả. Trang 56, cần rút chỗ khác nếu vượt 60. |
| nhẹ | L02-6-04 | "Diễn giải:" dùng $t^\star$ chưa có trên mặt trang (dòng dữ kiện viết $h^\star=h_3$). | "biến cố "ngưỡng xấu $t$ nhất quán" lồng nhau ở mỗi bên $t^\star$" | "… ở mỗi bên ngưỡng $3$ …" hoặc ghi "$h^\star=h_3$ ($t^\star=3$)" ở dòng dữ kiện. |
| nhẹ | L02-5-08 | "Diễn giải:" dùng "$95\%$", trên trang chỉ có $\delta=0{,}05$ (quy định: chỉ số có trên trang). Câu hỏi 1-06 hỏi "câu trả lời thay đổi thế nào", mặt trang chưa đặt $0{,}1204$ cạnh cận của hàm cố định. Dòng cuối là định nghĩa nhắc lại hơn là câu nối ("Rủi ro vượt mức so …, không với $L_S(\hat h)$"). | Mặt trang 5-08; $0{,}0387$ ($K=1$) có trên hình. | "**Diễn giải:** với xác suất ít nhất $0{,}95$, hàm chọn trong $1000$ ứng viên có rủi ro kì vọng không quá $0{,}1204$, so với $0{,}05+0{,}0387=0{,}0887$ khi $K=1$." Dòng cuối: "Bước tiếp theo so $L_D(\hat h)$ với $\min_{h\in\mathcal H}L_D(h)$ (rủi ro vượt mức)." |
| nhẹ | L02-5-06 | Ý (b), (c) rút gọn câu chữ của `exercises.md`; "kết luận" đứng một mình không nói kết luận về gì. | Deck: "…; kết luận."; "chỉ ra bước bị bỏ qua." `exercises.md` 02.4: "Kết luận về khẳng định của học viên."; "chỉ ra bước của chứng minh Định lý 02.14 mà học viên đã bỏ qua." | "…; kết luận về lập luận trên." và "chỉ ra bước của chứng minh mà học viên bỏ qua." |
| nhẹ | L02-7-03 | Câu nối số cuối đặt cụm đồng vị sai chỗ: đọc như $17\,538{,}04$ là giá trị của Ví dụ 02.9. | "$17\,538{,}04=16\cdot1096{,}13$, giá trị của Ví dụ 02.9 trước khi làm tròn." | "$17\,538{,}04=16\cdot1096{,}13$, với $1096{,}13$ là giá trị của Ví dụ 02.9 trước khi làm tròn." |
| nhẹ | L02-1-01 | Luận điểm thành dãy cụm danh từ trước dấu hai chấm (khuôn "colon reveal"); "mọi rủi ro thực nghiệm" không nói của giả thuyết nào. | "Quan sát độc lập, hàm lỗi bị chặn, lớp hữu hạn chọn trước: mọi rủi ro thực nghiệm gần rủi ro kì vọng với xác suất cao; …" | "Với quan sát độc lập, hàm lỗi bị chặn và lớp hữu hạn chọn trước, rủi ro thực nghiệm của mọi giả thuyết gần rủi ro kì vọng với xác suất cao; cỡ mẫu tăng theo lôgarit số giả thuyết." |
| nhẹ | L02-4-06 | "Hoeffding áp dụng sai cho …" đọc như "áp dụng cho số $2e^{-8}$". | "Hoeffding áp dụng sai cho $2e^{-8}\approx6{,}7\cdot10^{-4}$ ở $m=100$: cận sai." | "Áp dụng sai Hoeffding được $2e^{-8}\approx6{,}7\cdot10^{-4}$ ở $m=100$: cận sai." |
| nhẹ | L02-5-12 | Chữ hoa sau "Câu hỏi:", khác mọi trang còn lại. | "**Câu hỏi:** Với bất đẳng thức thứ nhất …" | "**Câu hỏi:** với …" |
| nhẹ | L02-2-01 | Ở 1600×900, cột phải của danh sách bốn đại lượng bắt đầu ngang dòng "Cần chặn …", cao hơn cột trái một dòng. | Ảnh `wide-007-L02-2-01.png`. | Đặt "Cần chặn ($\hat h$: nghiệm ERM):" ra ngoài `grid2`, hai cột chỉ chứa hai danh sách. |
| nhẹ | L02-4-06, L02-5-06 | Dòng trên 20 âm tiết không có trong danh sách lý do của mục 16. | `deck_check`: 4-06 maxLine 21; 5-06 maxLine 24 (hộp trích nguyên văn bài tập). | Ghi lý do vào `storyboard.md` mục 16 (5-06: câu chữ bài tập). |
| nhẹ | ghi chú diễn giả 4-01, 7-04 | Lỗi gõ. | 4-01: "chứa $L_D(h)$.Hàm hằng" (thiếu dấu cách); 7-04: "$\tfrac12$ ;" (dấu cách trước dấu chấm phẩy). | Sửa dấu cách. |

Detect `no-ai-slop` trên các câu mới khác (3-04 "Trực quan.", 4-02 "Trực quan.", 5-02 câu nối, 5-03 "Trực quan.", 6-01, 6-05 "Lưu ý", 7-02, 7-04, ghi chú diễn giả 7-00, 5-11, 3-02): không thấy mẫu nào (không câu khẩu hiệu, không tương phản nhị phân ngoài phủ định toán học, không lời rào đón, không câu điều hướng).

Mật độ (máy + số trong câu, đếm lại trên trang đổi): mọi trang nội dung ≤ 60 (cao nhất 3-04 ≈ 60, 7-04 ≈ 60, 1-06 ≈ 59, 5-12 59); 1-03 80, 7-01 63 dưới trần 80.

## Kết luận

Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 2 trung bình (7-03 bỏ loại bảo đảm; 7-01 bỏ tên kết quả), 12 nhẹ. Hai phát hiện nghiêm trọng của vai học viên và các mục điều phối viên nêu riêng (3-04, 5-08, 6-05, 7-01 ô Chebyshev, 5-06 nhãn) đã sửa đúng; sáu mục "không sửa" hợp lý. Máy: console 0, page errors 0, failed 0, KaTeX 0, `footer_check` 0 trang, không cuộn ngang ở 390 px.

**Kết luận: đạt khi sửa** (hai mục trung bình; các mục nhẹ do điều phối viên quyết).
