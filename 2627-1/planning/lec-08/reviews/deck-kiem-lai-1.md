# Kiểm lại sau biên tập, lượt 1 — deck Bài 08

Vai: kiểm lại (chỉ đọc). Ngày 2026-11-16. Đầu vào: `2627-1/lecture-08-on-dinh-sgd-hoc-sau.html` (sau sửa), bản đóng băng của điều phối viên (thư mục nháp `lec-08/master/frozen/`), năm báo cáo `reviews/deck-*.md`, `review-log.md` mục "Năm báo cáo duyệt và quyết định của điều phối viên", `storyboard.md` mục 17, ghi chú Bài 08 và `exercises.md`. `no-ai-slop` chế độ Detect cho văn bản mới hoặc đã sửa.

## 1. Kiểm máy (chạy trong lượt này)

| Kiểm | Kết quả |
|---|---|
| `deck_lint.py` | 0 phát hiện, 55 trang |
| `footer_check.py` (1600×900) | 0 trang chạm chân trang |
| `deck_check.py --shots` | 55 trang; console 0, pageerrors 0, failed 0, `katexErr` 0 ở mọi trang. OVERFLOW 1–3 px ở 2-03, 5-01, 5-02, 5-05, 7-07: cả năm trang có `\sqrt` (báo động giả đã biết) |
| SVG `img/lec-08/` | bốn tệp trùng byte với bản đóng băng (`cmp`), không đổi |
| Ảnh | đã xem ảnh 390×844 (kể cả `-end`) của mọi trang (55 trang, 82 ảnh, gồm mọi trang đổi và 7-00 với dòng dẫn mới) và ảnh 1600×900 của 1-02, 2-01, 2-03, 2-05, 4-07, 5-01, 5-04, 6-03, 6-06, 7-01, 7-03, 7-06. Ảnh trong thư mục nháp `lec-08/recheck/` |

Phím điều hướng không kiểm lại trong lượt này (không có trang hay liên kết `#/N` nào đổi).

Diff so với bản đóng băng: 48/55 trang đổi (mặt trang hoặc ghi chú diễn giả); không trang nào thêm hay bớt; ID giữ nguyên.

## 2. Phát hiện được chấp nhận → trạng thái

| Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|
| Nghiêm trọng (CG1): 7-03, 6-06 mạng ReLU không thỏa (S′) | đã sửa | 7-03: "Mạng ReLU huấn luyện mọi lớp không thỏa (S), (S′), (G): Định lý 08.6, Mệnh đề 08.10, Nhận xét 08.11 không áp dụng." Khớp ghi chú dòng 888. 6-00 dòng dẫn "(S), (S′)"; 6-06 "không $\beta$-trơn" |
| Nghiêm trọng (HV1): 2-05 hai kì vọng | đã sửa | "$\mathbb E_\xi w_2-\mathbb E_\xi w'_2=\tfrac38-\tfrac18=\tfrac14$"; "hai dãy chỉ số độc lập: $\mathbb E\lvert w_2-w'_2\rvert=\tfrac38>\tfrac14$". Tính lại: $\mathbb E_\xi w_2=(0+\tfrac12\cdot3)/4=\tfrac38$, $\mathbb E_\xi w'_2=(0+\tfrac12+\tfrac12-\tfrac12)/4=\tfrac18$; ghép cặp chỉ khác khi $i_1=4$, $\lvert w_2-w'_2\rvert=1$ → $\tfrac14$ |
| 6-06 câu của người duyệt toán học; (G) "trên toàn không gian tham số" | đã sửa | "không khả vi tại một số tham số có tiền kích hoạt (pre-activation) bằng $0$: không $\beta$-trơn; không lồi"; "không có $G$ đều trên toàn không gian tham số" (đúng đề xuất `deck-toan-hoc.md` phát hiện 1, 2) |
| Điều kiện ở dòng dẫn: 4-00, 5-00, 7-00 | đã sửa | 4-00 "(T1), (T2), (S), (G), $\eta_t\le2/\beta$ … không vượt $2G^2/m$ nhân ngân sách"; 5-00 "Với độ dài bước cố định"; 7-00 dòng dẫn mới (mục 3) |
| 5-01 "nếu $\eta^*\le2/\beta$" | đã sửa, có lỗi mới | điều kiện đúng; cách viết "vế phải tại $\eta^*$ $\le RG\sqrt{3/m}$" hiển thị thành "tại $\eta^*\le RG\sqrt{3/m}$" (phát hiện T1) |
| 5-04 định nghĩa chính quy hóa ngầm đủ điều kiện; "phỏng đoán" | sửa chưa đủ | câu mới khó tách chủ ngữ và bỏ "số bước, cách rút chỉ số" (phát hiện T2); "phỏng đoán thực nghiệm" ở 7-03 và ghi chú diễn giả 5-04: đạt |
| 7-03 "khi độ dài bước hằng" | đã sửa (chuyển) | dòng "Không lồi: cận tăng theo hàm mũ …" bỏ khỏi 7-03; khẳng định có điều kiện ở 6-03 (công thức bước hằng, $\eta_t=c/t$ đa thức) và ghi chú diễn giả 7-03, 1-05 |
| 7-01 hàng Định lý 08.6 "$\xi$ độc lập với $S$" | đã sửa | ô giả thiết viết đủ, không còn "như trên" |
| 4-01/7-03 ba ý (một thuật toán, kì vọng, không phụ thuộc $p$); 2-01 lý do cần ổn định | đã sửa | 7-01 dòng dưới bảng; 7-03 "không qua số tham số"; 2-03 "Nhiều vòng: … Hệ quả 06.2 không áp dụng" (phát hiện nhẹ N3 về câu chữ) |
| Nhận xét 08.11 trên 6-03 | đã sửa | một dòng: "(T3), $\eta_t\le c/t$ không tăng, $W=\mathbb R^p$; $\beta=10$, $c=G=1$, $m=10^4$, $T=10^6$: $\epsilon_{\mathrm{stab}}\le33{,}37>1$". Tính lại: $10^{6\cdot10/11}\approx284\,800$; $2^{1/11}\approx1{,}0650$; $1{,}1/9999$ → $33{,}37$ |
| Kí hiệu: 1-02 $W$, $\operatorname{proj}_W$, (T1), (T2); $\operatorname{opt}_S$; $L_s$; $g_t$, $F$ ở 6-04; 6-06 dữ liệu và "Nhắc lại:" $\Theta_1$, $\Theta_2$ | đã sửa | 1-02 không còn $W$, $\operatorname{proj}_W$, (T1)/(T2) đứng trước Định lý 06.10; (S) có công thức ở 2-02; 5-01 "$\operatorname{opt}_S(w)=L_S(w)-\inf_WL_S$"; 5-02 "tập huấn luyện cố định $s$"; 6-04 "hàm mục tiêu $F$", "gradient ngẫu nhiên $g_t$"; 6-06 "$\pm0{,}01\mapsto\mp0{,}49$", "$0{,}99\mapsto1{,}49$, $1{,}01\mapsto1{,}01$", "Nhắc lại:" mạng ReLU |
| Tên tiếng Anh | đã sửa | neighboring samples, uniform stability (1-02); logistic regression, stochastic gradient descent, epoch, random seed (1-06); averaged iterate, expected generalization gap (2-01); logistic loss (2-02); descent lemma (2-09, đúng ghi chú dòng 980); hinge loss, rectified linear unit (6-06); conjecture (7-03) |
| Đề bài theo `exercises.md`: 4-07, 7-06 | đã sửa | 4-07 "Tìm $T$ lớn nhất để cận của Hệ quả 08.7 không vượt độ rộng miền giá trị của hàm lỗi trên $W$; làm tương tự với Định lý 08.6 cho $w_{T+1}$" (khớp 08.7(b)); 7-06 khớp 08.5(d)(i). Riêng 7-04 bị rút thêm (phát hiện N6) |
| 7-08 câu quy trình; 4-05 lộ đáp số | đã sửa | hai câu bỏ khỏi ghi chú 7-08; ghi chú 4-05 chỉ còn "bài tập sau tính cận cho chương trình này" |
| HV2–HV18, TH1–TH18, CG2–CG15, SP1–SP30, MT M1–M7, N1–N11 còn lại | đã sửa | đối chiếu từng dòng `storyboard.md` mục 17 với diff mặt trang và ghi chú diễn giả: khớp |
| Không sửa có lý do: HV19 (2-06, 2-07), HV21, HV22, SP28, MT M3 (Câu hỏi 2-07), MT N5 (một phần) | chấp nhận lý do | HV21, HV22 đúng quy định màn hẹp; SP28 theo quyết định giữ (T3); M3 và N5 báo cáo ghi "có thể"/nhẹ |

### Đánh giá các mục "không sửa/chuyển" của mục 17

- **6-06 bỏ dòng "Kết luận:"**: đạt. Điều kiện áp dụng đầy đủ nằm trên mặt 7-06 ("cố định lớp ẩn trước khi thấy mẫu, chỉ huấn luyện lớp ra như mạng của Ví dụ 07.3"; "(S) với $\beta=G^2/4$, (G) với $G=\sup_x\lVert\chi(x)\rVert$") và ở ghi chú diễn giả 6-06. Mặt 6-06 không còn câu nào nói quá ghi chú.
- **"hàm mũ khi bước hằng" chuyển sang 6-03**: đạt. Mặt 6-03 có vế phải $\frac{2G}{m\beta}((1+\beta\eta)^T-1)$ khi bước hằng và cận đa thức khi $\eta_t=c/t$; hàng Mệnh đề 08.10 ở 7-02 giữ (S′), (G), (I). Không còn khẳng định "tăng theo hàm mũ" thiếu điều kiện trên mặt trang nào.
- **"$10^4$ hồ sơ"**: đạt. Dòng bỏ khỏi 7-03; 5-03 có "$m=10^4$ hồ sơ" và "theo cận ghép, nhiều vòng không tốt hơn một vòng: $0{,}0708>0{,}0500$"; ghi chú diễn giả 7-03 giữ câu.
- **5-04**: so sánh "ngân sách ở vị trí của $1/\lambda$" chuyển vào ghi chú diễn giả theo đúng câu ghi chú (dòng 719): đạt. Định nghĩa chính quy hóa ngầm: sửa chưa đủ (T2).
- **2-03**: CG4 đạt; lý do $T/m$ và điểm lặp phụ thuộc quan sát sắp dùng ở ghi chú diễn giả, khớp ghi chú dòng 198. Câu chữ: N3.
- **7-00 dòng dẫn sửa sau lần chụp cuối**: đã chụp lại trong lượt này (ảnh `narrow-045-L08-7-00`), hiển thị đủ, 24 âm tiết, khớp `storyboard.md` §3. Nội dung đúng ghi chú (dòng 888, §10) và khác ý dòng dẫn 4-00 (MT M4 đạt).

## 3. Toán trên nội dung đã đổi (tính lại)

Khớp: 2-05 ($\tfrac38$, $\tfrac18$, $\tfrac14$, $\tfrac38$); 6-06 ($0{,}01-\tfrac12=-0{,}49$; bản lề $0{,}99+\tfrac12=1{,}49$, $1{,}01$ đạo hàm $0$); 6-03 ($0{,}02\cdot(1{,}1^{100}-1)\approx275{,}6$; Nhận xét 08.11 $33{,}37$); 4-07 ($0{,}025(T-1)$: $0{,}25$; $4$; $39{,}975$; $\psi(11)\approx0{,}0301$, $\psi(161)\approx0{,}2843$, $\psi(1600)=0{,}4750$; $T\le161$, $T\le80$); 4-02, 4-06 ($L_D(w_{T+1})\le L_D(w_1)+G^2\sum_t\eta_t$ từ $\lVert w_{T+1}-w_1\rVert\le G\sum_t\eta_t$ và (L)); 4-03 (cận $>1$ từ vòng thứ hai, khoảng cách đo được lớn nhất $0{,}919$); 5-03 ($\eta^*=5/\sqrt{29998}\approx0{,}0289$, $0{,}0866$, $T^*=\sqrt{5\cdot10^7}\approx7071$, $0{,}0958$); 7-06 ($0{,}4G^2$; $G=1{,}5$: $0{,}9$; $0{,}1\le8/2{,}25$); 7-07 ($0{,}1(2\sqrt{20000}-1)\approx28{,}18$, cận $\approx0{,}0113$); 2-07 ("khi $u\ne v$"); 2-02 (T3) lượng từ. Không có sai số học.

Phát biểu: các phát biểu rút gọn trên trang đã đổi giữ giả thiết và loại bảo đảm, trừ T1 (đọc nhầm được) và N4 (7-01).

## 4. Mạch truyện (trang đổi ±2, ranh giới mạch)

- 1-06 → 2-00 → 2-01: câu hỏi mở đầu, dòng dẫn mạch 2, thiết lập: liền.
- 2-03 → 2-04: câu "Nhiều vòng: … Hệ quả 06.2 không áp dụng" cho lý do cần công cụ mới trước Định nghĩa 08.2: tốt hơn bản đóng băng.
- 2-06 → 2-07: câu nối một dãy → mọi dãy nay trên mặt 2-06 (MT M3); câu chữ: N1.
- 2-10/2-11 → 3-00 → 3-01: "Bổ đề 08.4 không chặn $\Delta_{t+1}$" → dòng dẫn "$1/m$" → "Trực quan." của 3-01: liền.
- 3-04 → 4-00 → 4-01: dòng dẫn mạch 4 nêu kết quả đủ điều kiện, 4-01 mở bằng nối Mệnh đề 08.5 → (L): liền.
- 4-07 → 5-00 → 5-01: lý do cần số hạng tối ưu ở ghi chú diễn giả 5-00, 5-01; mặt 5-01 có "Nhắc lại:" Mệnh đề 06.5(b) và "Trực quan." $1/T$ đối $T/m$: chấp nhận (MT N5 nhẹ).
- 5-05 → 6-00 → 6-01: liền. 6-02 → 6-03 → 6-04: dòng Nhận xét 08.11 ở cuối 6-03, rồi 6-04 "tính dừng yếu hơn sai số tối ưu": liền.
- 6-07 → 7-00 → 7-01, 7-02 → 7-03: dòng dẫn 7-00 nêu phạm vi (phản ví dụ, mạng ReLU); 7-03 trả lời câu hỏi trung tâm ba ý (cận theo ngân sách với đủ giả thiết, mạng ReLU, phỏng đoán). Câu hỏi 1-05 được 7-03 trả lời.
- 7-03 → 7-04 → 7-06: đề Bài tập 08.5 và lời giải: liền.

## 5. Phát hiện còn mở

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 5-01 (T1) | Hai kí hiệu $\eta^*$ và $\le$ đứng sát nhau, nên dòng (b) đọc thành một cận cho $\eta^*$, không phải cho vế phải. Lỗi sinh khi sửa HV5/TH6. | Mặt trang: "nếu $\eta^*\le2/\beta$, vế phải tại $\eta^*$ $\le RG\sqrt{3/m}$ khi $T=m$, $\to RG\sqrt{2/m}$ khi $T\to\infty$." Ảnh 1600×900 và 390×844: "vế phải tại $\eta^*\le RG\sqrt{3/m}$". | "nếu $\eta^*\le2/\beta$, vế phải của (a) tại $\eta=\eta^*$ không vượt $RG\sqrt{3/m}$ khi $T=m$ và tiến về $RG\sqrt{2/m}$ khi $T\to\infty$." (5-01 đang 48 âm tiết, còn chỗ) |
| trung bình | 5-04 (T2) | Câu định nghĩa chính quy hóa ngầm liệt kê ba cụm bằng dấu phẩy nên đọc như ba chủ ngữ của "quyết định"; bỏ "số bước, cách rút chỉ số" của ghi chú. | Mặt trang: "chính quy hóa ngầm (implicit regularization): nhiều điểm có $L_s$ nhỏ như nhau, khởi tạo, độ dài bước quyết định điểm trả về, không qua số hạng phạt." Ghi chú dòng 716: "xảy ra khi nhiều điểm của $W$ có rủi ro thực nghiệm nhỏ như nhau và các lựa chọn của quá trình huấn luyện (khởi tạo, độ dài bước, số bước, cách rút chỉ số) quyết định điểm được trả về, không qua một số hạng phạt." | "chính quy hóa ngầm (implicit regularization): khi nhiều điểm có $L_s$ nhỏ như nhau, khởi tạo, độ dài bước, số bước và cách rút chỉ số quyết định điểm trả về, không qua số hạng phạt." Trang đang 58/60: cắt bù, ví dụ "$T$ chọn trước hoặc bằng mẫu xác thực độc lập" thành "$T$ chọn trước hoặc bằng mẫu xác thực" (giữ "độc lập" ở ghi chú diễn giả, đã có). Điều phối viên đếm lại |
| nhẹ | 4-01 (N2) | Cùng lỗi đặt kí hiệu như T1: "tại mọi $z$ $\le G\Delta_{T+1}$" hiển thị "mọi $z\le G\Delta_{T+1}$". Bản đóng băng viết "không quá". | Ảnh 390×844 `narrow-024-L08-4-01`. | Trả lại "hiệu hàm lỗi tại mọi $z$ không quá $G\Delta_{T+1}$". |
| nhẹ | 2-06 (N1) | Câu nối gán cho định nghĩa điều mà chứng minh cần: Định nghĩa 06.9 lấy kì vọng theo $\xi$; chính vì thế hai sự kiện phải đúng với mọi dãy. | "Đây là một dãy chỉ số; Định nghĩa 06.9 cần hai sự kiện trên với mọi dãy." Ghi chú diễn giả bản đóng băng: "Định nghĩa 06.9 cần kì vọng theo $\xi$, nên hai sự kiện … phải được chứng minh cho mọi dãy." | "Đây là một dãy chỉ số; Định nghĩa 06.9 lấy kì vọng theo $\xi$, nên cần hai sự kiện trên với mọi dãy." (47 → khoảng 52 âm tiết) |
| nhẹ | 2-03 (N3) | "mỗi hồ sơ dùng lại" mạnh hơn ghi chú: rút có hoàn lại, một hồ sơ *có thể* được dùng lại, trung bình $T/m$ lần. | Ghi chú dòng 198: "một quan sát có thể được dùng lại ngay từ bước thứ hai". | "Nhiều vòng: hồ sơ được dùng lại, nên Hệ quả 06.2 không áp dụng." (cùng số âm tiết) |
| nhẹ | 7-01 (N4) | "Mọi bảo đảm theo kì vọng" mâu thuẫn hàng Bổ đề 08.4 "tất định" của chính bảng (và Mệnh đề 08.5(a) tất định). | "Mọi bảo đảm theo kì vọng, cho một thuật toán, không phụ thuộc $p$; không có cận với xác suất cao." | "Các cận ổn định theo kì vọng, cho một thuật toán, không phụ thuộc $p$; không có cận với xác suất cao." |
| nhẹ | 7-04 (N6) | Mục (c) bị rút thêm so với bản đóng băng, mất "của Định lý 08.6" của đề. | "(c) Lập bảng giả thiết: thỏa, không thỏa, không xác định; $0{,}4$ có căn cứ không?" `exercises.md` 08.5(c): "Lập bảng các giả thiết của Định lý 08.6 cho thiết lập của báo cáo: thỏa, không thỏa, hay không xác định." | "(c) Lập bảng giả thiết của Định lý 08.6: thỏa, không thỏa, không xác định; $0{,}4$ có căn cứ không?" Cắt bù nếu vượt 60 (ví dụ bỏ "được" trong "mọi trọng số được huấn luyện"). |
| nhẹ | 6-06 (N7) | Dấu phẩy thập phân đứng cạnh dấu phẩy phân cách: "$1{,}49$, $1{,}01$" đọc thành "1,49, 1,01". | Ảnh `narrow-043-L08-6-06`. | Dùng dấu chấm phẩy: "$0{,}99\mapsto1{,}49$; $1{,}01\mapsto1{,}01$". |
| nhẹ | 5-02, 1-06, 3-01, 5-03 (N8) | Dấu câu mồ côi đầu dòng ở 390 px trên trang đã đổi: 5-02 ", không của $w_{T+1}$" (dòng mới), 1-06 ", $\lVert x\rVert\le1$", 3-01 ", $t$:", 5-03 ": $\le0{,}0708$". | Ảnh `narrow-033`, `narrow-005`, `narrow-019`, `narrow-034`. | Đưa dấu câu vào trong KaTeX như đã làm ở 2-02 (ví dụ "$\bar w_T,$"), hoặc đổi thứ tự cho 5-02: "Định lý 05.14 không chặn sai số tối ưu của $w_{T+1}$, chỉ của $\bar w_T$." |
| nhẹ | ghi chú diễn giả 1-02 (N9) | Câu điều hướng, và chỉ sai chỗ: tính không giãn của phép chiếu được nhắc ở Bổ đề 08.4(c) (2-08), không ở Định nghĩa 08.3. | "Tính trơn và phép chiếu được nhắc lại ở chỗ dùng (giả thiết (S), Định nghĩa 08.3)." | Cắt câu. |
| nhẹ | ghi chú diễn giả 4-07 (N10) | Câu nay lặp nguyên đề trên mặt trang. | "Câu hỏi đầy đủ của phần (b): tìm $T$ lớn nhất …" | Cắt câu. |
| nhẹ | ghi chú diễn giả 7-03 (N11) | Câu cuối mất vế so sánh khi sửa, nên Hệ quả 07.16 đứng một mình không có đối chiếu. | "Hệ quả 07.16 đúng với xác suất ít nhất $1-\delta$ cho mọi hàm của một lớp chọn trước." | Thêm "; Định lý 08.6 đúng theo kì vọng, cho một thuật toán." |

`no-ai-slop` Detect trên văn bản mới hoặc đã sửa: không có mẫu cấm (khẩu hiệu, câu hỏi tu từ, mở bằng "Trang này", câu về trạng thái văn bản, rào đón). Các điểm văn phong còn lại là N1, N9, N10, N11 ở trên. Câu "Định lý 08.6 chặn khoảng cách tổng quát hóa, không chặn rủi ro kì vọng" lặp ở ghi chú diễn giả 5-00 và 5-01 (hai trang liền): chấp nhận, vì 5-00 là trang tiêu đề mạch.

## 6. Kết luận

Hai phát hiện nghiêm trọng đã sửa đúng; mọi quyết định của điều phối viên đã thực hiện, trừ 5-04 sửa chưa đủ. Còn mở: chặn bàn giao 0, nghiêm trọng 0, trung bình 2 (T1 5-01, T2 5-04), nhẹ 10. Kiểm máy sạch (`deck_lint` 0, `footer_check` 0, `deck_check` không lỗi; OVERFLOW chỉ ở `\sqrt`).

**Kết luận: đạt khi sửa.** Sau khi sửa T1, T2 (và các mục nhẹ), cần kiểm lại 4-01, 5-01, 5-04 (±2) và chạy lại `deck_lint.py`, `footer_check.py`, đếm âm tiết 5-04, 7-04.
