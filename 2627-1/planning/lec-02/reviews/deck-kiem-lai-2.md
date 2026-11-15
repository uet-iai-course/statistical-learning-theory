# Kiểm lại sau biên tập deck Bài 02, lượt 2 (chỉ đọc)

Vai: kiểm lại sau biên tập, lượt 2. Đầu vào: `reviews/deck-kiem-lai-1.md`, bảng "Lượt 2" cuối mục 16 của `storyboard.md`, deck hiện tại, bản đóng băng và diff theo trang của lượt 1 (thư mục nháp `…/scratchpad/lec-02/recheck/`). `no-ai-slop` chế độ Detect trên câu mới.

## Cách kiểm

- So diff theo trang (bản đóng băng → hiện tại) với diff của lượt 1. Có 14 trang đổi ở lượt 2: 1-02, 1-05, 2-01, 4-01, 4-06, 5-06, 5-08, 5-09, 5-12, 6-00, 6-04, 7-01, 7-03, 7-04 (4-01, 1-02, 7-04 chỉ đổi ghi chú diễn giả). SVG và CSS không đổi sau lượt 1.
- `deck_lint.py`: 0 phát hiện trên 55 trang. `footer_check.py`: 0 trang ở 1600×900 và 0 trang ở 1280×720.
- `deck_check.py --shots` (`recheck/dc2/`): slides=55, console 0, pageerrors 0, failed 0, không `.katex-error`. OVERFLOW chỉ ở 4-02, 4-04, 4-05, 5-03, 5-08, 6-06 (`path` của `\sqrt`, báo động giả). SYLL ở 7-01 (76) là cờ sai do tiêu đề (trần 80 của bảng tổng kết).
- 390×844: `narrow_clip.py` không thấy phần tử nào vượt mép phải ngoài vùng cuộn. Đã xem ảnh 1600×900 và 390×844 (cả `-end`) của 1-05, 2-01, 4-06, 5-06, 5-08, 5-09, 6-00, 6-04, 7-01, 7-03.
- Số âm tiết đếm bằng script: tách token theo khoảng trắng, bỏ nhãn "Câu hỏi:" và KaTeX, giữ token có chữ cái.
  - 1-05: 30 (đạt ≤ 30).
  - 6-00: 23; cộng "$0$" thành 24 (đạt ≤ 25). `deck_check` đếm 32 cho 1-05 vì tính cả nhãn.

## 1. Các điểm của lượt 1

| Phát hiện lượt 1 | Trạng thái | Bằng chứng |
|---|---|---|
| Trung bình, 7-03: mất loại bảo đảm, thiếu (T2), $a<b$ | đã sửa | "Theo phần (a), với (T1), (T2), (T4), $0\le a\le\ell\le b$, $a<b$: mọi thuật toán ERM học PAC bất khả diễn với $M(\epsilon,\delta)=…$", khớp Bài tập 02.11(a) |
| Trung bình, 7-01: mất tên kết quả | đã sửa | "Markov, Chebyshev (Bổ đề 02.2, 02.3)", "Hoeffding (…)", "Cận tin cậy (Hệ quả 02.10)", "Hội tụ đều (Định lý 02.14)", "Rủi ro vượt mức (Hệ quả 02.16)", "Khả diễn (Mệnh đề 02.17)"; ô ý tưởng của hàng khả diễn đổi thành "$(1-\epsilon)^m\le e^{-\epsilon m}$, bất đẳng thức hợp", đúng chứng minh Mệnh đề 02.17 |
| 1-05 hộp 31 âm tiết | đã sửa | 30 (script); "kể cả khi chọn giả thuyết theo dữ liệu" giữ nghĩa |
| 6-00 dòng dẫn 27 | đã sửa | 23/24; "cỡ mẫu tăng như $1/\epsilon$" nói rõ tốc độ; $\epsilon$ đã có từ mạch 2 |
| 5-09 dòng (c), lớp và $m\ge1097$ | đã sửa | "Do đó mọi thuật toán ERM học PAC bất khả diễn với …"; "(Ví dụ 02.9) Sáu hàm ngưỡng, …: khi $m\ge1097$, với xác suất $\ge0{,}95$, $L_{D_\eta}(\hat h)\le0{,}32$" |
| 6-04 $t^\star$ | đã sửa | "$h^\star=h_3$ ($t^\star=3$)" |
| 5-08 "Diễn giải:" | đã sửa | "với xác suất ít nhất $0{,}95$, … không quá $0{,}1204$, so với $0{,}05+0{,}0387=0{,}0887$ khi $K=1$": $0{,}95=1-\delta$; $0{,}0387$ có trên hình; dòng cuối "Bước tiếp theo so $L_D(\hat h)$ với $\min_{h\in\mathcal H}L_D(h)$ (rủi ro vượt mức)." |
| 5-06 câu chữ (b), (c) | đã sửa, có lỗi mới | "kết luận về lập luận"; "chỉ ra bước chứng minh bị bỏ qua". Lỗi mới: bỏ $\mathcal X=\{0,1\}^K$ (bảng 4) |
| 7-03 cụm đồng vị | đã sửa | "…, với $1096{,}13$ là giá trị của Ví dụ 02.9 trước khi làm tròn" |
| 5-12 chữ hoa | đã sửa | "**Câu hỏi:** với …" |
| 2-01 lệch cột | đã sửa | Dòng "Cần chặn …" ra ngoài `grid2`; ảnh 1600×900: hai danh sách cùng mép trên |
| Dòng > 20 ở 4-06, 5-06 | đã ghi lý do | Lý do ở bảng Lượt 2 của mục 16 hợp lý |
| Lỗi gõ ghi chú 4-01, 7-04 | đã sửa | "$L_D(h)$. Hàm hằng"; "$\tfrac12$;" |
| 1-01 luận điểm | không sửa | Hợp lý: ngoài danh sách lượt 2 của điều phối viên; phương án đề xuất tăng số âm tiết của bìa |
| 4-06 "áp dụng sai Hoeffding" | đã sửa | "Áp dụng sai Hoeffding được $2e^{-8}\approx6{,}7\cdot10^{-4}$ ở $m=100$: cận sai." Câu có vị ngữ rõ |

## 2. Thay đổi do người sửa tự quyết

- **5-09, Giả thiết bỏ "mọi quy tắc chọn khi bằng nhau":** không mất giả thiết.
  - Ghi chú (Hệ quả 02.16, dòng "Thuật toán") nêu cụm này như lượng từ "một thuật toán ERM bất kì …, với mọi quy tắc chọn khi bằng nhau", không phải điều kiện.
  - Trên trang, lượng từ vẫn còn ở hai chỗ: "đồng thời cho mọi nghiệm ERM" (biến cố đúng cho mọi phần tử của $\arg\min L_S$, nên đúng với mọi quy tắc chọn) và "Do đó mọi thuật toán ERM …".
  - Ghi chú diễn giả 5-09 và 7-01 vẫn nêu "không phụ thuộc quy tắc chọn khi bằng nhau".
  - Chấp nhận được. Phần (b) với (O2) chỉ có ở ghi chú diễn giả và ở 5-10, như trước.
- **5-06, bỏ khung của câu trích:** hợp lý. Nhãn "Câu hỏi:" và câu chữ nguyên văn Bài tập 02.4 vẫn còn; không có quy định đòi khung.
- **4-06:** xem bảng 1.
- **Rút ghi chú diễn giả 1-02 và 7-03:**
  - 1-02 bỏ câu mở "Ba câu ôn nhanh …" và rút phần nhắc định nghĩa. Vẫn giữ đủ số hiệu Định nghĩa 01.16, 01.18, 01.25 và ba nghĩa của $\epsilon$.
  - 7-03 không mất nội dung: còn ba bước, hệ số $16$, phần (c), phép kiểm $0{,}099997\le0{,}1$.

## 3. Toán và mạch truyện trên trang đổi ±2

- Toán, tính lại đều khớp:
  - 5-08: $0{,}05+0{,}0387=0{,}0887$; $0{,}05+0{,}07037=0{,}1204$.
  - 5-09: $200\ln240=1096{,}13\to1097$; $0{,}22+0{,}1=0{,}32$.
  - 7-03: $16\cdot1096{,}128=17\,538{,}04$, $M=17\,539$.
  - 7-01: các giả thiết khớp lượt 1.
  - 6-04: $t^\star=3$ khớp $h^\star=h_3$.
- Mạch truyện:
  - 5-07 → 5-08 → 5-09 → 5-10: dòng cuối 5-08 dẫn thẳng sang tiêu đề "Rủi ro vượt mức của ERM …".
  - 4-05 → 4-06 → 5-00 và 6-00 → 6-01: không đổi ý.
  - 7-00 → 7-01 → 7-02 → 7-03 → 7-04: không đổi ý.
  - 1-04 → 1-05 → 1-06: câu hỏi trung tâm vẫn được 7-02 trả lời.

## 4. Phát hiện còn mở

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | L02-5-06 | Lỗi mới ở lượt 2: trang bài tập bỏ dữ kiện $\mathcal X=\{0,1\}^K$ của `exercises.md`, nên $X_k$ (tọa độ thứ $k$ của $X$) không được giới thiệu trên mặt trang; $h_k(x)=x_k$ cũng cần $x\in\{0,1\}^K$. | Mặt trang: "$X_k\sim\mathrm{Bernoulli}(\tfrac12)$ độc lập, $Y=0$, $h_k(x)=x_k$, …". `exercises.md` 02.4: "Xét $\mathcal X=\{0,1\}^K$ … các tọa độ $X_1,\ldots,X_K$ của $X$ độc lập". Dữ kiện chỉ có ở ghi chú diễn giả. | "$\mathcal X=\{0,1\}^K$, $X_k\sim\mathrm{Bernoulli}(\tfrac12)$ độc lập, …" (thêm một công thức, không thêm âm tiết; trang 58). Nếu đáy trang chạm chân trang, rút "Tính chính xác" ở ý (b) thành "Tính". |
| nhẹ | L02-7-03 | Mật độ vượt trần 60 khi tính số trong câu. | Máy 58; cộng $4$, $1$, $1097$, $1096{,}13$ và hai lần "02.9" thành 64. | Dòng cuối: "$17\,538{,}04=16\cdot1096{,}13$ (Ví dụ 02.9, trước khi làm tròn)." Còn khoảng 58. |
| nhẹ (ghi để điều phối viên quyết) | L02-7-01 | Máy đếm 76; nếu tính cả tám số hiệu kết quả trong ô bảng thì 84 > 80. Quy ước "số trong câu" có áp cho ô bảng hay không chưa rõ. | Tám số hiệu 02.2–02.17 trong cột "Kết quả". | Nếu tính ô bảng: rút "Bổ đề 02.6, Định lý 02.7" thành "Định lý 02.7" và "Bổ đề 02.2, 02.3" thành "Bổ đề 02.2–02.3", hoặc ghi ngoại lệ vào storyboard. |

Mật độ các trang đổi khác (máy + số trong câu): 1-02 56, 4-06 57, 5-06 58, 5-08 58, 5-09 60, 6-04 51, 7-04 60. Tất cả đạt.

Detect `no-ai-slop` trên câu mới (5-08 "Diễn giải:" và dòng cuối, 5-09 "Do đó …", 6-00, 4-06, 7-03, ghi chú diễn giả 1-02, 7-03): không thấy mẫu nào.

## Kết luận

Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 0 trung bình, 3 nhẹ (5-06 thiếu $\mathcal X=\{0,1\}^K$; 7-03 có 64 âm tiết khi tính số; 7-01 tùy quy ước đếm số trong ô bảng). Hai phát hiện trung bình và mọi phát hiện nhẹ của lượt 1 đã sửa đúng, trừ 1-01 (không sửa, hợp lý). `deck_lint` 0, `footer_check` 0, `deck_check` sạch.

**Kết luận: đạt** (ba mục nhẹ nên sửa trước khi chốt; mỗi mục là sửa một dòng).
