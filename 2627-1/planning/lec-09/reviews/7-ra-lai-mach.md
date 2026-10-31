# Rà lại mạch, móc nối và văn phong sau biên tập vòng 1 — Bài 09

Người rà 5, chỉ đọc repo. Đối tượng là bản `lec09-r1-frozen.md` (1 019 dòng; số dòng dưới đây theo bản này). Đối chiếu: `lec09-r1.udiff`, `reviews/0-quyet-dinh.md`, `bien-tap-vong-1.md`, `reviews/4-hoc-thuat-van-phong.md`, `reviews/5-mach.md` và `van-phong.md`. Văn phong của các đoạn mới được soát theo `no-ai-slop` Detect.

## Tổng kết theo mức

- **Chặn bàn giao:** 0. **Nghiêm trọng:** 0.
- **Trung bình:** 1 phát hiện mới, M1: "bằng chứng" được dùng theo hai nghĩa.
- **Nhẹ:** 9 phát hiện mới (M2–M10).
- Phát hiện cũ của người rà 5: 16 ✓, 1 một phần (R10), 2 ✗ (R11, R17). Hai mục ✗ là phần tùy chọn mà biên tập viên đã ghi lý do ngân sách; lý do này chấp nhận được.
- Phát hiện trung bình của người rà 4: T2–T6 ✓; T1 và T7 một phần.

## Kiểm tra chạy

- Bản sao nằm ở `reviews09/r5b/lec-09/lecture-note.md`. `forward_refs.py` cho **0 forward references**.
- Đọc tay các thuật ngữ và kí hiệu đã đổi:
  - "giá" được định nghĩa kèm (support) ở 346, trước lần dùng đầu trong thân bài (381). Không còn nghĩa "cái giá"; 32 và 150 chỉ là chữ "đánh giá".
  - "chuỗi" chỉ còn nghĩa sequence: 353 và 392 viết "tổng", 1007 viết "dãy bất đẳng thức".
  - "dừng" chỉ còn trong "điểm dừng" (632, 898).
  - "người học" chỉ ở 36.
  - KL được mở ở 5 và ở nhãn 349.
  - $x^{(i)}$ dùng nhất quán ở 156–158, 558, 587, 589, 642–644, 694–701 và 1005–1016; thân bài không còn $x_i$ nào mang nghĩa quan sát.
  - $\mathrm{Ber}(\theta)$ định nghĩa ở 164, trước lần dùng ở 355.
  - $U_0$ ở 743 và 824. $\theta^\star$ chỉ còn vai tham số thật; Ví dụ 09.6 viết $\theta=\tfrac16$.
  - Không còn "phân bố xấp xỉ", "mẫu sinh" hay "Không-ví dụ".
- Chuyển chứng minh sang Phụ lục D: tiêu đề hai khối ghi "chứng minh đầy đủ (Phụ lục D)"; câu ở 203 và 649 nói chứng minh dùng gì. Hai chứng minh trong Phụ lục D đều có Lộ trình, các bước, $\square$ và một câu ý nghĩa. Không có tham chiếu tới trước.
- Cầu nối (851) có câu "Câu hỏi cho Bài 10 là: …", tách thành hai câu hỏi, khớp blueprint 9.6 và 10.1 và không phát biểu kết quả của Bài 10. Câu đầu đã đúng sự kiện: "trong mục tiêu huấn luyện, phân bố lấy kì vọng duy nhất phụ thuộc tham số đang tối ưu là $q_\phi$". Câu này đúng với cả EM, vì $q_i$ cố định trong bước M.
- Câu hỏi mở đầu được trả lời ở 30–32 và ở §10 (784).

## Kiểm từng phát hiện cũ

| Mã | Trạng thái | Bằng chứng ở bản mới |
|---|---|---|
| R5-R1 KL | ✓ | 5: "(Kullback–Leibler divergence, KL)"; 349 |
| R5-R2 cầu nối | ✓ | 851 |
| R5-R3 $x_i$ | ✓ | $x^{(i)}$ ở mọi chỗ (xem trên) |
| R5-R4 mẫu kiểm tra | ✓ | 77: "chỉ dùng ở §6 và trong thí nghiệm" |
| R5-R5 phân bố dừng | ✓ | 458 suy luận qua entropy từng hàng, không cần phân bố dừng (đúng); 961 "mọi kí tự có phân bố đều" |
| R5-R6 $\theta^*$/$\theta^\star$ | ✓ | 321, 330, 334 |
| R5-R7 Ber | ✓ | 164 |
| R5-R8 thuật ngữ/tiếng Anh | ✓ | 145, 120, 346, 284, 291, 87, 681, 416, 676 |
| R5-R9 $4^{200}-1$ | ✓ | 217 |
| R5-R10 câu kết §6, §9 | một phần | §9 (780) ✓. §6 (337) mất ý chính của mục: trong Thiết lập A, cận dùng số chuỗi $m$ (M3) |
| R5-R11 mắt xích Bài 06 | ✗ (chấp nhận) | ngân sách; tùy chọn |
| R5-R12 $\phi$, $u$ | ✓ | 502; $U_0$ |
| R5-R13 câu Định nghĩa 01.1 | ✓ | 118 |
| R5-R14 dẫn bước chứng minh | ✓ | 585 |
| R5-R15 "giá không chứa" | ✓ | 383, 431 |
| R5-R16 "Không-ví dụ" | ✓ | 93 "phản ví dụ" |
| R5-R17 bán kính với 200 chuỗi | ✗ (chấp nhận) | ngân sách; tùy chọn |
| R5-R18 câu hỏi lặp | ✓ | đã cắt (30) |
| R4-T1 câu kết mục | một phần | §3 kết bằng khối ứng dụng, có tiền lệ ở Bài 06 và Bài 08. §4 (183) và §9 (780) đạt. §7 (486) vẫn gần như lặp Kết luận của Ví dụ 09.7 ở 452 (M4). §1 nay kết bằng bảng (M2) |
| R4-T2 một chữ một nghĩa | ✓ | "chuỗi", "giá", "người học", "dừng" đã sửa; có lỗi mới cùng loại (M1) |
| R4-T3 "giá" | ✓ | 346, 383, 431 |
| R4-T4 thiết lập đổi giữa chừng | ✓ | 432, 743, 759 ghi rõ phạm vi bước; 432 nói $S$, $\hat\theta$ ngẫu nhiên |
| R4-T5 ví dụ từng bước | ✓ | 174, 229, 271, 429, 434, 438–450, 458–463, 725–733, 775 |
| R4-T6 dòng 3, dòng 860 | ✓ | 3 bỏ "Bài 08 kết thúc bằng câu hỏi"; 851 mỗi câu dưới 40 tiếng |
| R4-T7 bảng Ví dụ 09.10 | một phần (chấp nhận) | Tiêu đề cột giữ "KL"/"Khe" vì giới hạn 271 px, nghĩa được nói ở câu dẫn 605; Bước 3 ghi "cột khe của bảng thứ hai" |

## Mạch sau các chỗ cắt

- **§1.** Câu tóm tắt 105 cũ đã bị cắt, nên mục nay kết bằng bảng (97–101). Các mục 1 của Bài 06–08 đều kết bằng văn xuôi (M2).
- **§3.** Kết bằng khối ứng dụng, có tiền lệ ở Bài 06 và Bài 08. Câu mở §4 (150) nêu đúng nhu cầu, nên chuyển ý vẫn liền.
- **§5.** Câu 203 thay cho chứng minh và giữ ý "không phải giả thiết mô hình". Con số $4^{200}-1$ được trả lời ở 217. Mạch liền.
- **§6.** Thứ tự là Ví dụ 09.4 (A), 284 → Ví dụ 09.5 (B), 300 → Định nghĩa 09.6 → Ví dụ 09.6, rồi câu kết 337. Câu kết nói B và độ dài nhưng bỏ A (M3).
- **§7.** Hệ quả 09.9 dẫn sang ví dụ số (429), rồi Ví dụ 09.7 và 09.8; câu kết 486 lặp (M4).
- **§8.** Câu 649 thay cho chứng minh EM; câu 652 dẫn sang §9 (Kingma–Welling, SGD). Việc cắt câu "Câu ôn nhanh 3 là …" làm câu ôn nhanh 3 không còn chỗ nối trong thân bài (M8, tùy chọn).
- **§9.** Câu mở 656 nêu đúng vấn đề và hai cách giải. Bỏ câu Bernoulli sau Định nghĩa 09.14 không làm hụt gì, vì Ví dụ 09.12 tự đủ với Thiết lập ghi hai phần. Câu kết 780 đủ hai ý.
- **§10, §12, §13.** Khớp nội dung mới: (d) có tái tham số hóa $U_0$; §13 có $L(S;\theta)=-m\,L_S$.
- **Phụ lục.** D đứng sau C, nên thứ tự phụ lục không theo thứ tự đọc (§5, §8 ở D; §9 ở B). Không cần sửa, vì đổi tên sẽ kéo theo nhiều tham chiếu (ghi chú, không tính là phát hiện).

## Bảng phát hiện mới (dòng theo `lec09-r1-frozen.md`)

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 959 (Phụ lục C) | M1. "Bằng chứng" là thuật ngữ của bài, $\ln p_\theta(x)$ (Định nghĩa 09.10, 497), nhưng ở đây mang nghĩa "evidence" thông thường. Đây là lỗi cùng loại với R4-T2. | 959: "Các số của Ví dụ 09.5 và 09.8 là bằng chứng thí nghiệm cho một thiết lập, không phải chứng minh." | "Các số của Ví dụ 09.5 và 09.8 là kết quả thí nghiệm cho một thiết lập, không phải chứng minh." (phụ lục, 0 tiếng thân bài) |
| nhẹ | 95–101 | M2. §1 kết bằng bảng sau khi câu 105 cũ bị cắt. Quy tắc học phần yêu cầu kết mục bằng văn xuôi, và Bài 06–08 đều theo quy tắc này. | 101: "\| Tất định \| $L_D(\theta)$ với mỗi $\theta$ \|", rồi "## 2." | Chuyển câu 95 và bảng lên trước 84 ("Dữ liệu chuỗi có hai cách lấy mẫu."), bỏ $k$ ở hàng đầu vì $k$ chưa được định nghĩa ở đó và đã có trong bảng §2. §1 khi đó kết bằng đoạn 93. (−1 tiếng) |
| nhẹ | 337 | M3. Câu kết §6 bỏ ý chính của mục: trong Thiết lập A, cỡ mẫu trong cận là số chuỗi. Câu về Thiết lập B lại đứng ngay sau Ví dụ 09.6 (độ dài chuỗi), cách Ví dụ 09.5 hai khối. | 337: "Trong Thiết lập B, chia ngẫu nhiên các cửa sổ làm mẫu kiểm tra phụ thuộc hàm đã học. Khi độ dài …" | "Trong Thiết lập A, các cận dùng số chuỗi $m$; trong Thiết lập B, chia ngẫu nhiên các cửa sổ làm mẫu kiểm tra phụ thuộc hàm đã học. Khi độ dài …" (+9) |
| nhẹ | 486 | M4. Câu kết §7 nhắc lại Kết luận của Ví dụ 09.7 (452) và Mệnh đề 09.8(a). Đây là dạng summary-recap (R4-T1). | 452: "Trên mẫu hữu hạn, ước lượng hợp lý cực đại có thể có rủi ro kì vọng vô hạn"; 486: "Trên mẫu hữu hạn, một mô hình gán xác suất $0$ cho một giá trị có thể xảy ra có rủi ro vô hạn." | Viết thành câu nêu điều §8 cần: "Với mô hình biến ẩn, $p_\theta(x)$ là một tổng hay tích phân theo biến ẩn, nên chính $L_s(\theta)$ có thể không tính được." Cách khác là rút 486 còn "Mô hình gán xác suất $0$ trên giá của $p_D$ có rủi ro $+\infty$." (−8). Câu thứ nhất không thêm chữ, nhưng điều phối viên cần xem nó có trùng câu mở §8 (490) không. |
| nhẹ | 452 | M5. Nhận xét 02.11 nói về cận đuôi cho hàm lỗi không bị chặn, không nói về rủi ro kì vọng vô hạn của một ước lượng. Thêm nữa, khối văn bản làm chủ ngữ của "báo trước" (`van-phong.md`). | 452: "như Nhận xét 02.11 đã báo trước." | "…có thể có rủi ro kì vọng vô hạn; hàm lỗi log là một hàm lỗi không bị chặn như ở Nhận xét 02.11." (+5) |
| nhẹ | 780 | M6. "Điều không xảy ra với biến ẩn rời rạc" có chủ ngữ mơ hồ và nói rộng hơn điều đã chỉ ra. Ví dụ 09.12 chỉ cho thấy (i) không thỏa với tái tham số hóa bằng hàm bậc thang. | 780: "…thỏa (i)–(iii) của Mệnh đề 09.15, điều không xảy ra với biến ẩn rời rạc." | "…thỏa (i)–(iii) của Mệnh đề 09.15; với biến ẩn rời rạc, (i) không thỏa (Ví dụ 09.12)." (+3) |
| nhẹ | 775 | M7. Hai vế "nên" nối tiếp trong một câu dài 78 tiếng. | "…$\approx8{,}9\cdot10^{-44}$, nên hàm lỗi log kiểm tra gần như chắc chắn bằng $+\infty$." | Tách câu: "…$\approx8{,}9\cdot10^{-44}$. Do đó hàm lỗi log kiểm tra gần như chắc chắn bằng $+\infty$." (0) |
| nhẹ | 502 | M8. Sau khi cắt câu "Câu ôn nhanh 3 là …", câu ôn nhanh 3 (chuẩn bị §8) không còn chỗ nối nào trong thân bài. | 57 (đề); thân bài không dẫn | Tùy chọn, cuối 502: "Câu ôn nhanh 3 là một mô hình biến ẩn với $\mathcal V=\{1,2\}$." (+14) |
| nhẹ | 145 | M9. Cụm "trên chuỗi mới" bị kẹp giữa hai dấu phẩy, câu khó đọc. | "(i) Với $m=50$, hàm lỗi log chia cho độ dài chuỗi, trên chuỗi mới, cách giá trị tốt nhất bao xa?" | "(i) Với $m=50$, trên chuỗi mới, hàm lỗi log chia cho độ dài chuỗi cách giá trị tốt nhất bao xa?" (0) |
| nhẹ | 1018 (Phụ lục D) | M10. Dòng thứ hai của dãy bất đẳng thức chỉ cần "không giảm"; "làm tăng" nói mạnh hơn mức cần. | "Bước M chỉ cần làm tăng, không cần cực đại hóa, tổng …" | "Bước M chỉ cần không làm giảm tổng $\sum_i\mathbb E_{q_i}\ln p_\theta(x^{(i)},v)$, không cần cực đại hóa nó, để dòng thứ hai … vẫn đúng." (phụ lục) |

Ghi chú hình thức, không tính là phát hiện: có hai dòng trống liền nhau ở 204–205 và 650–651. Markdown hiển thị như một dòng trống, nhưng nên xóa một dòng cho sạch diff.

**Văn phong các đoạn mới.** Các đoạn 3, 30, 93, 118, 183, 203, 215, 217, 284, 337, 429, 649, 656, 667, 756, 780, 797, 851 và 959 không có câu hỏi tu từ, chủ ngữ là văn bản, dấu hai chấm tiết lộ, "không phải … mà là …" giả hay câu kết kiểu châm ngôn. Riêng 452 có chủ ngữ là văn bản (M5). Cặp "…, không phải chứng minh" ở 959 là đối lập thật nên giữ được.

## Ngân sách (thân 11 997/12 000)

- **Thêm nếu nhận:** M3 +9, M5 +5, M6 +3 (M8 +14 tùy chọn). Cộng khoảng +17, hoặc +31 nếu nhận M8.
- **Cắt bù (không mất nội dung):**
  1. 649: bỏ "tại $\theta_{t+1}$ và tại $\theta_t$, nơi $q_i$ là hậu nghiệm" (≈ −12). Chi tiết này đã có ở Phụ lục D, Bước 2.
  2. M2: bỏ $k$ khỏi bảng §1 (−1).
  3. M4: rút 486 (≈ −8).
  4. 795 (giới hạn "Tối ưu không lồi"): rút còn "**Tối ưu không lồi.** $-\operatorname{ELBO}$ nói chung không thỏa (C) (§9)." (≈ −4). Câu 701 đã nói đủ.
  5. 183: "Hàm lỗi log của mô hình ở Bước 4 bằng $+\infty$ trên quan sát $1$." (≈ −10).

  Cộng khoảng −35, đủ bù cả khi nhận M8.
