# Kiểm lại sau biên tập — deck Bài 03, lượt 2 (2026-11-15)

Vai: kiểm lại (chỉ đọc). Đầu vào: deck sau sửa lượt 2 `2627-1/lecture-03-chieu-vc.html`, bảng "Lượt 2" cuối mục 17 `storyboard.md`, báo cáo lượt 1 `reviews/deck-kiem-lai-1.md` (N1–N17). Đối chiếu bằng diff mặt trang và ghi chú diễn giả với bản trích lượt 1 (`scratchpad/lec-03/recheck/faces.txt` → `recheck/r2/faces.txt`). `no-ai-slop` chế độ Detect trên câu mới.

Diff: 15 trang đổi (mặt trang 1-02, 2-01, 2-07, 3-04, 4-02, 5-03, 5-04, 5-05, 5-06, 6-03, 6-08, 7-02; chỉ ghi chú diễn giả 3-06, 6-00, 7-04), `so-cach-gan-nhan.svg` (nhãn), và thẻ `meta viewport` nay là `width=device-width,initial-scale=1`, khớp `lecture-template.html` và deck 01, 02, 04, 05.

## 1. Kiểm tra máy (đã chạy)

| Kiểm tra | Kết quả |
|---|---|
| `deck_lint.py` | 0 phát hiện / 55 trang |
| `footer_check.py` | 0 trang |
| `deck_check.py --shots` | console 0, page errors 0, failed 0, `.katex-error` 0; OVERFLOW chỉ ở 1-02, 5-01, 5-04, 5-09, 6-04, 7-02 (đuôi `\sqrt`, báo động giả); SYLL chỉ 1-01 (bìa) và 7-01 (68 ≤ 80); hết LINE20 ở 6-08 (maxLine 15). Mật độ trang đổi: 2-01 58, 2-07 59, 3-04 58, 5-03 60, 5-05 57, 5-06 49, 6-03 34, 6-08 54, 7-02 55 |
| Ảnh | 1600×900 và 390×844 (cả `-end`) của mọi trang đổi, đã xem (`recheck/r2/w-wide-01.png`, `n-narrow-01.png`): không chồng lấn, không tràn; nhãn mới của hình 4-02 đọc được ở 1600×900 |

## 2. N1–N17 → trạng thái

| Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|
| N1 (trung bình) 5-03 thuật ngữ trước định nghĩa | đã sửa | 5-03: "Mẫu bóng (ghost sample) $S'\sim D^m$ độc lập thay $L_D(h)$ bằng $L_{S'}(h)$: sửa (i)." / "Đổi chỗ ngẫu nhiên (swapping) $Z_i\leftrightarrow Z'_i$ khi biết $(S,S')$: sửa (ii)." 5-05 bỏ hai tên tiếng Anh này, giữ "dấu ngẫu nhiên (random signs)" và $\Pr(\sigma_i=\pm1)=\tfrac12$. Thứ tự giới thiệu: mẫu bóng, đổi chỗ (5-03) → dấu ngẫu nhiên (5-05) → đối xứng hóa (5-06); mỗi thuật ngữ có tên tiếng Anh đúng một lần ở lần dùng đầu trên mặt trang nội dung. Khớp ghi chú §7 (Bước 1 sửa (i); Bước 3: khi biết $(S,S')$, nguồn ngẫu nhiên còn lại là $\sigma$) |
| N2 1-02/5-03 "(union bound)" | đã sửa | 1-02 "bất đẳng thức hợp (union bound)"; 5-03 không còn |
| N3 2-01 "(countable subclass)" | đã sửa, cách viết còn lệch | xem M1 |
| N4 1-02 thiếu "đo được" | đã sửa | "hàm lỗi đo được, trong $[0,1]$"; ghi chú diễn giả bỏ câu trùng |
| N5 4-02 "Trực quan." | đã sửa | "Thêm một điểm, các cách gán nhãn được nhân đôi tạo thành một tập có chiều VC $\le d-1$."; ghi chú diễn giả: "khi và chỉ khi nó thuộc tập $Y_1$, và $Y_1$, coi như một lớp, có chiều VC không quá $d-1$" (đúng Bước 1–3 Phụ lục B) |
| N6 3-04 "đơn hình chứa gốc" | đã sửa | "tập đỉnh có gốc, như $\{0,\mathbf e_1,\ldots,\mathbf e_p\}$, không còn bị tách trọn vẹn" (đúng: lớp thuần nhất gán nhãn $1$ cho gốc) |
| N7 5-04 $\rho_m$ trước định nghĩa | đã sửa | "$d=\infty$: cận $\ge3{,}33$" |
| N8 5-05 ngoặc chồng | đã sửa | "; dùng (T1), (M).", "; dùng (T1).", "; dùng (T5)."; bước 3 "$\le\Pi_{\mathcal H}(2m)$ cách" giữ nghĩa "nhiều nhất" |
| N9 5-06 dòng gói hai ý | đã sửa | dòng riêng "Chia đôi độ lệch và miền dài $2$ cho hằng số $8$ trong $\rho_m$." Dòng "Kỹ thuật." rút gọn: xem M2 |
| N10 2-07 mảnh câu | đã sửa | "Thứ nhất:", "Thứ hai:"; "Thứ hai xét một tập năm điểm nên không cho cận trên, và thiếu cận dưới." (khớp lời giải 03.2(c)) |
| N11 6-00, 7-02 "$1/\epsilon^2$" | đã sửa | cả hai câu có "trong trường hợp bất khả diễn" |
| N12 6-08 "Ý nghĩa:" | đã sửa | "khi bất khả diễn, độ phức tạp mẫu (sample complexity) cần tốc độ $1/\epsilon^2$." / "$M(\epsilon,\delta)$ của Hệ quả 03.16(c) dư một thừa số cỡ $\ln(1/\epsilon)$." |
| N13 (trung bình) 7-02 thiếu (M), hàm lỗi 0–1 | đã sửa | "(T1), (T5), (M), hàm lỗi 0–1, mọi $D$, xác suất ít nhất $1-\delta$: độ lệch đều $\le\rho_m$ …" (đủ giả thiết Định lý 03.15). Cụm "bảo đảm cho lớp" bị bỏ: xem M3 |
| N14 7-04 ghi chú câu 1 | đã sửa | "$0$ cho các điểm còn lại, trong đó có ít nhất một điểm $x$" |
| N15 6-03 "mọi ERM" | đã sửa | "mọi nghiệm ERM"; bỏ "cho rủi ro vượt mức" ở dòng đầu: nghĩa của $\epsilon$ vẫn rõ từ tiêu đề "Ví dụ: cỡ mẫu cho rủi ro vượt mức $0{,}1$" và dòng Hệ quả 03.16(a) ngay dưới |
| N16 3-06 ghi chú | đã sửa | "Hai cấu hình là hai bộ bốn điểm cụ thể;" |
| N17 SVG 4-02 | đã sửa | nhãn "dạng đóng" / "d = 3: 5951", cùng kiểu "tổng nhị thức" / "d = 3: 1351"; `desc` và `alt` không đổi, vẫn khớp |

## 3. Toán trên nội dung đổi

Không con số nào đổi. Các phát biểu đổi đều kiểm lại: 1-02 giả thiết Định lý 02.14 nay đủ (T1)–(T4) bằng lời; 3-04 khẳng định về tập đỉnh có gốc đúng; 4-02 phát biểu về $Y_1$ đúng (Phụ lục B); 5-03 phân công (i)/(ii) đúng ghi chú §7; 5-05 bước 1–5 không đổi nội dung; 5-06 bất đẳng thức tam giác và nguồn hằng số $8$ ($2m(\epsilon/2)^2/2^2=m\epsilon^2/8$) đúng; 6-08 khớp đoạn sau Định lý 03.19; 7-02 giả thiết khớp Định lý 03.15.

## 4. Mạch truyện (trang đổi ±2)

- 5-01 → 5-07: câu hỏi và hai trở ngại (5-03) → định lý (5-04) → lộ trình dùng lại "mẫu bóng", "đổi chỗ" đã giới thiệu và giới thiệu "dấu ngẫu nhiên" (5-05) → kỹ thuật đối xứng hóa gọi tên bước 1–2 (5-06) → hàm tăng trưởng thay $K$ (5-07). Không thuật ngữ nào dùng trước khi giới thiệu.
- 1-01 → 1-04, 1-06 → 2-03, 2-05 → 3-01, 3-02 → 3-06, 4-00 → 4-04, 6-01 → 6-05, 6-06 → 7-00, 7-00 → 7-04: liền; không còn dẫn kết quả trang sau. Hệ quả 02.16 vẫn chỉ xuất hiện trên mặt trang từ 6-02.

## 5. Phát hiện còn mở (văn phong câu mới, `no-ai-slop` Detect)

| # | mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|---|
| M1 | nhẹ | L03-2-01 | Tên tiếng Anh "countable subclass" gắn với tính từ "đếm được"; thuật ngữ tiếng Việt "lớp con đếm được" không còn trên mặt trang lẫn ghi chú diễn giả. | "(M), điều kiện đo được: $\mathcal H_0\subseteq\mathcal H$ đếm được (countable subclass), mỗi $h\in\mathcal H$ …" | Ghi chú diễn giả: thêm lại "$\mathcal H_0$ là một lớp con đếm được (countable subclass)." (không đổi mật độ mặt trang), hoặc mặt trang "lớp con $\mathcal H_0\subseteq\mathcal H$ đếm được (countable subclass)" nếu bớt được một âm tiết ở dòng khác. |
| M2 | nhẹ | L03-5-06 | Dạng chung một dòng của kỹ thuật đối xứng hóa (dùng lại ở các bài sau) bỏ tính độc lập của mẫu bóng, điều kiện then chốt của Bước 1; điều kiện chỉ còn ở 5-03, 5-05. | "**Kỹ thuật.** Đối xứng hóa (symmetrization): thay $L_D(h)$ bằng $L_{S'}(h)$ của mẫu bóng $S'$." | "… của mẫu bóng $S'\sim D^m$ độc lập." nếu `footer_check.py` vẫn 0 (mặt trang 49 âm tiết); nếu chạm chân trang, giữ nguyên. |
| M3 | nhẹ | L03-7-02 | Khi sửa N13, cụm "bảo đảm cho lớp" (sửa CG3 của lượt duyệt) bị thay bằng "đúng cho mọi $h$ cùng lúc". Nghĩa theo lớp vẫn đọc được qua "mọi $h$", nhưng chữ phân biệt lớp / thuật toán mà CG3 yêu cầu trên mặt trang không còn; ghi chú diễn giả vẫn có. | "…, cỡ $\sqrt{d\ln m/m}$, đúng cho mọi $h$ cùng lúc." | "…, cỡ $\sqrt{d\ln m/m}$; bảo đảm cho lớp, mọi $h$ cùng lúc." (+2 âm tiết, 55 → 57). |

Ngoài ba mục trên, câu mới không có mẫu `no-ai-slop` (không rào đón, không câu khẩu hiệu, không chuỗi dấu hai chấm nén, không chủ ngữ là văn bản).

## 6. Kết luận

N1–N17 đã sửa đúng (N3 đạt yêu cầu tên tiếng Anh nhưng cách gắn còn lệch, M1). Toán không đổi và đúng; mạch 5-03 → 5-05 giới thiệu "mẫu bóng", "đổi chỗ", "dấu ngẫu nhiên" đúng thứ tự. `deck_lint.py` 0, `footer_check.py` 0, `deck_check.py` sạch.

Còn mở: chặn bàn giao 0, nghiêm trọng 0, trung bình 0, nhẹ 3 (M1–M3, mỗi mục một dòng, không cần lượt kiểm lại riêng ngoài `deck_lint.py`/`footer_check.py`).

**Kết luận: đạt.**

Tệp nháp: `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-03/recheck/r2/` (`faces.txt`, `facediff.txt`, `deck_check.txt`, `check/`, `w-wide-01.png`, `n-narrow-01.png`).
