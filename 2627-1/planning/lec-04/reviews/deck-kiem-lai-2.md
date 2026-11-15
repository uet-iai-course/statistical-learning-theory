# Kiểm lại sau biên tập deck Bài 04 — lượt 2 (chỉ đọc)

Ngày: 2026-11-15. Bản kiểm: `2627-1/lecture-04-phan-tich-sai-so.html` sau lượt sửa 2. Đối chiếu: `reviews/deck-kiem-lai-1.md` (M1–M15), `storyboard.md` mục 17, bảng "Lượt 2", ghi chú `materials/lec-04/lecture-note.md`. Văn bản đã sửa được đọc theo `no-ai-slop` chế độ Detect và mục "The author's voice". Chỉ đọc; không sửa deck, storyboard, ghi chú.

## Kiểm tra máy (đã chạy)

Thư mục nháp: `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-04/recheck2/` (`snapshot.html` là bản đã kiểm, `vs-frozen.diff`, `check/`, `nar-01…03.png`).

- So với trạng thái lượt 1 (dựng lại từ `recheck/slides.diff`): 16 trang đổi: 1-03, 1-06, 2-02, 2-03 (ghi chú diễn giả), 2-05, 2-07, 3-04, 3-05, 3-06, 4-08, 4-10, 4-11, 5-01, 6-01, 7-01, 7-02. Thứ tự 55 trang không đổi; SVG không đổi.
- `deck_lint.py`: 0. `footer_check.py`: 0.
- `deck_check.py --shots`: console 0, pageerrors 0, failed 0, `.katex-error` 0. OVERFLOW ở 6-01, 7-01, 7-02 là `path` của `\sqrt` (báo động giả đã biết; 7-02 nay có căn ở dòng 4). Ở 390 px `docScrollW` = 390. Cờ mới: **LINE20 ở 3-04** (dòng "Kết luận:" 22 âm tiết). Mật độ trang đổi: 1-03 80 (trần 80), 7-02 58, 6-01 59, các trang khác 35–58.
- Ảnh 390×844 (cả `-end`) của 15 trang đổi trên mặt trang: đã xem; không chồng chữ, dấu câu không còn rơi dòng ở 2-02, 2-05.

## 1. M1–M15

| # | Trang | Trạng thái | Bằng chứng |
|---|---|---|---|
| M1 | 2-05 | đã sửa | "Mọi $D$, xác suất $\ge1-\delta$ theo $S\sim D^m$: (a) đúng đồng thời cho mọi quy tắc." Khớp ghi chú dòng 252. |
| M2 | 3-04 | đã sửa (cờ LINE20 mới, N3) | "… nên phân tích này không cho quy tắc chọn bậc từ dữ liệu." Khớp ghi chú dòng 550; hết mâu thuẫn với 6-04, 7-02. |
| M3 | 7-02 | sửa chưa đủ (N1) | Dòng 1 có "sai số ước lượng $\le2r+\operatorname{opt}_S$, xác suất $\ge1-\delta$"; dòng 4 có "giá $2\sqrt{\ln(2K/\delta)/(2m_v)}$, xác suất $\ge1-\delta$". Nhưng "tính được" ở dòng 1 nay gắn vào sai số ước lượng. |
| M4 | 2-03 (ghi chú diễn giả) | đã sửa | Không còn "Đọc hình:"; câu mới về $0{,}04$, $0{,}10$ và lớp mọi hàm (sai số xấp xỉ $0$) đúng ghi chú Ví dụ 04.2; 142 token. |
| M5 | 4-11 | đã sửa | "khi $S$ có ít nhất một nhãn $0$". |
| M6 | 4-08 | đã sửa | "vế phải của (b) cân hai phần". |
| M7 | 5-01 | đã sửa | "nên cần cỡ mẫu theo lớp chứa $h$". |
| M8 | 2-07 | đã sửa | "$a_{10}\le a_2$, cả hai không quan sát được"; "$1\le d\le m$" trở lại. |
| M9 | 6-01, 4-10 | đã sửa | 6-01: câu nối SRM không nhãn, "**Trực quan.**" mở dòng mẫu xác thực; 4-10: "**Ví dụ 04.9 (tiếp).**". |
| M10 | 3-06 | đã sửa | "$\Pr(Y=1\mid X=x)=0{,}9$: thuật toán dao động nhiều hơn có lỗi $0{,}58$, thuật toán hằng $0$ có lỗi $0{,}90$". |
| M11 | 3-05 | đã sửa | "nhãn đã dùng để huấn luyện … lỗi trên nhãn mới". |
| M12 | 1-03 | đã sửa (bù trần làm hỏng mục tiêu 3, N2) | "Tính cận của mẫu xác thực". |
| M13 | 1-06 | đã sửa | "các cận của Bài 02–03"; "cận rủi ro vượt mức (Bài 03)". |
| M14 | 2-05, 2-02 | đã sửa | "$\delta\in(0,1).$", "$\delta=0{,}05,$" trong KaTeX; ảnh 390 px không còn dấu câu đứng riêng. |
| M15 | 7-01 | đã sửa | "Kết quả (xác suất $\ge1-\delta$, mọi $D$; trừ 04.6)"; bảng vừa khung (`footer_check` 0). |

## 2. Các chỗ cắt bù

| Trang | Cắt | Đánh giá |
|---|---|---|
| 1-03, mục tiêu 3 | "chọn lớp từ một bảng số" → "chọn lớp từ bảng" | **Mất ý** (N2). Ghi chú, mục tiêu 3: "tính lựa chọn của quy tắc này từ một bảng rủi ro thực nghiệm và số hạng phạt". "từ bảng" không nói bảng gì, đúng lỗi SP4 đã được chấp nhận và sửa ở lượt trước. |
| 1-06, dòng 1 | "$16$ quan sát … khớp đa thức … bằng bình phương tối thiểu" → "$16$ điểm, …; đa thức bậc …, bình phương tối thiểu (least squares)" | Không mất giả thiết: dữ liệu, ba bậc và phương pháp khớp còn đủ. Câu thành chuỗi danh từ, chấp nhận được trên trang ví dụ. |
| 2-05, Trực quan | "Sai số xấp xỉ (lớp) không quan sát được; $2r$ (cỡ mẫu) và $\operatorname{opt}_S(\tilde h)$ (bộ giải) tính được." | Đạt; giữ đủ ba nguồn và tương phản quan sát được / tính được, đọc thẳng hơn bản lượt 1. |
| 3-06, Nhận xét 04.7 | "Độ chệch thuộc thuật toán, sai số xấp xỉ thuộc lớp." | Giữ nghĩa ghi chú ("tính chất của thuật toán / của lớp"). |
| 3-06, Lưu ý | "thuật toán hằng $0$" | Giữ nghĩa ("luôn dự đoán $0$" của ghi chú); hai số $0{,}58$, $0{,}90$ và dẫn Ví dụ 04.6 đủ. Kết luận "phương sai lớn hơn, lỗi nhỏ hơn" đọc được từ hai số; câu đầy đủ ở ghi chú diễn giả. |
| 3-06, bullet 1 | "không có đầu vào" → "không đầu vào" | Không ảnh hưởng. |
| 4-08 | "$\inf_k[\cdot]$ ở vế phải" → "$\inf_k[\cdot]$" | Không mất ý: công thức (b) đứng ngay trên dòng; "không gồm $\tau$" giữ. |
| 7-02, dòng 1 | bỏ "không quan sát được" | Mất tương phản "không quan sát được / tính được" trên trang trả lời (MT2, MT10); thêm lỗi chủ ngữ của "tính được" (N1). Ý này còn trên mặt trang 2-05, 2-07. |
| 7-02, dòng 2 | bỏ "($m=10^4$)" | Chấp nhận: dòng nói về ví dụ ba chỉ số đo đã cố định $m=10^4$ ở 1-06, 2-02, 4-07. |
| 7-02, dòng 3 | "Bậc tốt nhất phụ thuộc $\sigma^2$, $f^*$ chưa biết; …" → "Bậc đa thức: $\sigma^2$, $f^*$ chưa biết; khi …, chọn bằng mẫu xác thực." | Mất quan hệ "bậc tốt nhất phụ thuộc $\sigma^2$, $f^*$" (N4). |

## 3. Toán và mạch truyện

- Toán: 3-05 "$0+\sigma^2/m+\sigma^2=1{,}25$" với $m=4$, $\sigma^2=1$: đúng. 2-07, 4-08, 4-11, 5-01, 7-01, 7-02 không đổi số; các phát biểu sửa khớp ghi chú (dòng 252, 550, 824). Hai số $0{,}04$, $0{,}10$ ở ghi chú diễn giả 2-03 đúng.
- Mạch truyện: 3-04 → 3-05 … 3-07 → 4-00 nay liền (mạch 3 kết bằng việc thiếu quy tắc chọn từ dữ liệu, mạch 4 đưa ra quy tắc). 6-00 → 6-01 → 6-02 đạt. 7-01 → 7-02 → 7-03: 7-02 trả lời hộp 1-05 với quy tắc SRM, loại bảo đảm và giá của mẫu xác thực. 1-05 → 1-06 → 2-00, 2-01 → 2-03, 2-05 → 2-07, 4-07 → 4-12: không đứt.

## 4. Phát hiện còn mở

| # | mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|---|
| N1 | nhẹ | L04-7-02 | Dòng 1: "tính được" đứng sau "xác suất $\ge1-\delta$" nên đọc như sai số ước lượng tính được; cái tính được là cận. Tương phản "không quan sát được" của sai số xấp xỉ bị cắt. | "Lớp lồng nhau, cùng $L^*$: sai số xấp xỉ không tăng; sai số ước lượng $\le2r+\operatorname{opt}_S$, xác suất $\ge1-\delta$, tính được." Ghi chú cuối §4: "sai số xấp xỉ … không quan sát được, còn số hạng $2r$ … tính được". | Tối thiểu: "… xác suất $\ge1-\delta$; cận tính được." (+1 âm tiết, trang 59). Nếu muốn giữ cả tương phản: "sai số xấp xỉ không tăng, không quan sát được" (+4) và bù bằng cách bỏ "Lớp lồng nhau," ở đầu dòng (đã có ở bìa, 1-06, 4-08). Người sửa đếm lại. |
| N2 | nhẹ | L04-1-03 | Mục tiêu 3 "chọn lớp từ bảng" không nói bảng gì; hồi lại lỗi SP4 đã sửa. | Ghi chú, mục tiêu 3: "từ một bảng rủi ro thực nghiệm và số hạng phạt". | "chọn lớp từ bảng rủi ro thực nghiệm và số hạng phạt"; bù trần 80 trên cùng trang, ví dụ mục tiêu 2 "tách độ chệch khỏi sai số xấp xỉ" → "phân biệt độ chệch, sai số xấp xỉ", mục tiêu 4 bỏ "qua một phản ví dụ" nếu cần. Người sửa đếm lại. |
| N3 | nhẹ | L04-3-04 | Dòng "Kết luận:" 22 âm tiết, vượt 20 âm tiết/dòng (`deck_check` LINE20; trang 35 âm tiết nên còn chỗ). | Kết luận: "bậc tốt nhất là $0$ … hoặc $2$ …; $\sigma^2$, $f^*$ chưa biết nên phân tích này không cho quy tắc chọn bậc từ dữ liệu." | Tách hai dòng: "**Kết luận:** bậc tốt nhất là $0$ ($\sigma^2=1$) hoặc $2$ ($\sigma^2=0{,}1$)." / "$\sigma^2$, $f^*$ chưa biết, nên phân tích này không cho quy tắc chọn bậc từ dữ liệu." |
| N4 | nhẹ | L04-7-02 | Dòng 3 mất quan hệ "bậc tốt nhất phụ thuộc $\sigma^2$, $f^*$": "$\sigma^2$, $f^*$ chưa biết" đứng một mình. | "Bậc đa thức: $\sigma^2$, $f^*$ chưa biết; khi $\lvert Y\rvert\le B$, dự đoán cắt, chọn bằng mẫu xác thực." | "Bậc tốt nhất phụ thuộc $\sigma^2$, $f^*$ chưa biết; khi $\lvert Y\rvert\le B$, dự đoán cắt, chọn bằng mẫu xác thực." (+3 âm tiết; gộp với N1 khi đếm lại trần 60). |

**Văn phong (Detect).** Văn bản sửa không có rào đón, câu về trạng thái văn bản, câu chỉ đường hay chuỗi dấu hai chấm mới; nhãn đúng danh sách. Các mẫu còn lại là chuỗi danh từ (1-06 dòng 1, chấp nhận) và chủ ngữ lệch (N1).

## Kết luận

M1–M15: 14 đã sửa, M3 sửa chưa đủ (N1). Cắt bù: mục tiêu 3 (1-03) và dòng 1, 3 của 7-02 làm mất ý; 3-06, 4-08, 1-06, 2-05 giữ đủ giả thiết và ý. Máy: `deck_lint.py` 0, `footer_check.py` 0, `deck_check.py` sạch trừ LINE20 mới ở 3-04. Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 0 trung bình, **4 nhẹ** (N1–N4).

**Kết luận: đạt.** N1–N4 là sửa câu chữ trên ba trang (1-03, 3-04, 7-02), nên làm trước khi xuất bản; sau khi sửa chỉ cần `deck_lint.py`, `footer_check.py` và ảnh 390 px `-end` của ba trang đó.

## Đề xuất sửa ghi chú

Không có.
