# Rà lại 4b — Sư phạm và văn phong của bộ bài tập Bài 10 sau vòng sửa 1

Đối tượng: `2627-1/materials/lec-10/exercises.md` (9 961 tiếng) và diff `reviews10/ex-diff.txt` so với `lec10-ex-frozen.md` (242 dòng diff, đã đọc toàn bộ). Đầu vào: `planning/lec-10/reviews/11-quyet-dinh-bai-tap.md`, `planning/lec-10/bai-tap-ghi-chu.md` §8, `git diff` của `materials/lec-10/lecture-note.md`. Chế độ `no-ai-slop`: Detect. Phạm vi: các đoạn đã đổi, cộng một đoạn trước và một đoạn sau mỗi đoạn. Vị trí ghi theo số dòng của tệp hiện tại. Người rà chỉ đọc, không sửa, không commit.

**Tổng kết:** 22/22 phát hiện cũ đã xử lý: 21 ✓, 1 một phần (N12, lý do chấp nhận được). Phát hiện mới: 6, đều nhẹ. Chặn bàn giao: 0. Nghiêm trọng: 0. Trung bình: 0.

**Kiểm tra đã chạy.** Ở 390×844 (Playwright, `scratchpad/rv4site10/`, mở mọi `details`): 0 lỗi trang, 0 `.katex-error`, 47/47 công thức hiển thị vừa khung (có một công thức mới ở 10.1(f)), sáu bảng vừa 271 px, `scrollWidth` 375. `git diff` của `lecture-note.md` chỉ đổi đúng hai dòng §11 (dòng 844: 10.3 "mục tiêu 1, 5"; dòng 850: 10.9 "(Tùy chọn: mẹo nhân đôi; UML Bài tập 21.4)"), khớp tên trong tệp bài tập (dòng 861) và dòng mục tiêu của 10.3 (317). Cây làm việc còn diff của `lec-01/lecture-note.md`, `review-log.md` và `material-local-data.js`, ngoài phạm vi bài tập Bài 10; khi commit, không đưa `lec-01` vào nếu đó không phải việc của vòng này.

## Kiểm từng phát hiện cũ

| Phát hiện | Kết quả | Ghi chú |
|---|---|---|
| T1 (mục tiêu 2, điều kiện đổi chỗ) | ✓ | 10.1(f) đo đúng vế này: đề yêu cầu kiểm ba điều kiện của Nhận xét 10.5, tính $J'(1)$ theo hai cách, và đối chiếu với Ví dụ 10.3. Lời giải kiểm cả giả thiết phần thưởng bị chặn, đưa hàm trội cụ thể với $\int\Lambda=\tfrac{10}{\theta_0}$ (đã tính lại: $\tfrac2{\theta_0}+2\theta_0\cdot\tfrac4{\theta_0^2}$), và tính $e^{-1}$ bằng tích phân từng phần. Dòng "Mức độ/Mục tiêu" đã cập nhật. Gợi ý 1 nêu giá cố định, gợi ý 2 nêu hàm trội: hai gợi ý tăng dần; gợi ý 2 làm sẵn phần khó nhất của điều kiện hàm trội, mức chấp nhận được với một gợi ý 2. Tên bài 10.1 vẫn nói "bài toán bandit", còn (f) dùng hành động liên tục; câu mở của (f) ("Thay bài toán bandit bằng …") đủ để người học không nhầm. |
| T2 (lời giải dựa vào gợi ý) | ✓ | 10.1(e) Bước 1, 10.2(a) Bước 3, 10.3(b) Bước 4 (nghiệm $\frac{34\pm\sqrt{292}}{48}$, đã kiểm), 10.3(d) Bước 2, 10.6(b) Bước 3. 10.4(c) Bước 2 cũng thôi dẫn gợi ý. |
| T3 (Kiểm tra lại 10.7) | ✓ | Phép kiểm miền $[0,6]$ so với $[0,4]$ đúng và kiểm một điều mới; lý do "phần thưởng ở bước đầu chỉ thuộc $\{0,1\}$" đúng ($1+3=4$). |
| N1 (Mức độ/Mục tiêu) | ✓ | 10.1, 10.3, 10.7, 10.8; §11 của ghi chú khớp. |
| N2 (gợi ý lộ lời giải) | ✓ | 10.8(b): tên bất đẳng thức Markov chuyển sang Gợi ý 2. 10.5(c): Gợi ý 2 chỉ cho đạo hàm. |
| N3 (tiếng Anh lần đầu) | ✓ | |
| N4, N5, N6, N7, N8, N9, N10, N11 | ✓ | N6: khoảng $[-0{,}2652;\,-0{,}1148]$. Về câu mới ở 10.4(c), xem M1, M2. |
| N12 (10.6(a)) | một phần | "Ước lượng thấp hơn giá trị tổng thể" ✓. Vế "cùng số cấu hình" bị bỏ để giữ trần chữ; "cùng quy tắc" vẫn giữ yêu cầu đối xử như nhau, nên chấp nhận. Câu Hậu quả mới của "Ngân sách bộ nhớ" có lỗi câu chữ (M3). |
| N13–N19 | ✓ | |

## Phần cắt chữ

- 10.7: bỏ yêu cầu phụ "một thay đổi làm (T1) đúng hay hỏng" cùng hai đoạn trả lời. Yêu cầu này không có trong dàn ý (`outline.md` §4, mục 7). Năm câu hỏi, trong đó có "giả thiết cần thay đổi", vẫn đo mục tiêu 1 và 5. Ý "$\theta$ chọn từ chính các lượt làm hỏng (T1)" vẫn có ở Ví dụ 10.12, Bước 4 của ghi chú và ở 10.3. Không mất ý cần cho mục tiêu.
- 10.2(a) Bước 2, 10.4 "Kiểm tra lại", 10.8(c) Bước 3, 10.9(a) Bước 4, 10.3 Gợi ý 1 (c)(i), 10.6(c) gộp thành đoạn: không mất bước tính hay lập luận. Gợi ý 2 của 10.3 vẫn có phần (c)(i).
- 10.1(c) Bước 5: mất vế kết luận (M4).
- 10.3(a) Bước 2: bỏ vế định nghĩa $\hat g_\theta$ nhưng kí hiệu vẫn được dùng (M5).

## Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | M1. 10.4(c) Bước 1, dòng 541 | Câu đầu không có chủ ngữ, đọc như một nhãn. Vế "độc lập với các mẫu kiểm tra" không rõ gắn với đối tượng nào. Câu thứ hai ghép "một số cố định" với "ngẫu nhiên theo dữ liệu huấn luyện" mà không nói theo nghĩa nào, nên đọc như mâu thuẫn. | "Điều kiện hóa theo mọi dữ liệu huấn luyện và nguồn ngẫu nhiên của các thuật toán, độc lập với các mẫu kiểm tra. Khi đó … cố định; giá trị tổng thể của mỗi ô là một số cố định, nhưng ngẫu nhiên theo dữ liệu huấn luyện." | "Ta điều kiện hóa theo mọi dữ liệu huấn luyện và nguồn ngẫu nhiên của các thuật toán; các đại lượng này độc lập với các mẫu kiểm tra (Định nghĩa 10.10). Khi đó $w^{(k)}$ và các mô hình của $\mathrm{acc}^\circ_i$ cố định, nên giá trị tổng thể của mỗi ô là một số; số này vẫn phụ thuộc dữ liệu huấn luyện." (±0) |
| nhẹ | M2. 10.4(c) Bước 3, câu cuối (dòng 561) | "Khẳng định đúng với xác suất … có điều kiện" là cụm lủng củng. "đúng khi lấy kì vọng theo dữ liệu huấn luyện" không nói đại lượng nào được lấy kì vọng; ý đúng là xác suất không điều kiện cũng ít nhất $0{,}95$. | "Khẳng định đúng với xác suất ít nhất $0{,}95$ có điều kiện, nên cũng đúng khi lấy kì vọng theo dữ liệu huấn luyện." | "Xác suất có điều kiện của khẳng định này ít nhất $0{,}95$ với mọi giá trị của dữ liệu huấn luyện; lấy kì vọng theo dữ liệu đó, xác suất không điều kiện cũng ít nhất $0{,}95$." (+8) |
| nhẹ | M3. 10.6(a) "Ngân sách bộ nhớ" (dòng 689) | Lặp "so sánh … so sánh" trong một câu ngắn; câu không nói vì sao kết quả sai lệch. | "Hậu quả: so sánh gần với so sánh với huấn luyện chung." | "Hậu quả: phát lại gần như thành huấn luyện chung, nên không còn đo tác dụng của một bộ nhớ hạn chế." (+8) |
| nhẹ | M4. 10.1(c) Bước 5 (dòng 114) | Sau khi rút gọn, vế cuối "hành động hiếm hơn có gradient log lớn hơn" đứng lơ lửng; lời giải không còn nói điều đó dẫn tới gì, trong khi đề hỏi "vì sao $b^*\ne J$". | "…, tức xác suất của hành động nhân bình phương gradient log; hành động hiếm hơn có gradient log lớn hơn." | "…; hành động hiếm hơn có gradient log lớn hơn, nên phần thưởng của nó nặng hơn trong $b^*$." (+8) |
| nhẹ | M5. 10.3(a) Bước 2 (dòng 354) | Kí hiệu $\hat g_\theta(\tau')$ xuất hiện không có định nghĩa: vế giải thích đã bị cắt, nơi khác chỉ có $\hat g(\tau)$. | "$\varphi(\theta,\xi)=\sum_{\tau'}\mathbb 1[g(\theta,\xi)=\tau']\big(-\hat g_\theta(\tau')\big)$" | Thêm sau công thức: "với $\hat g_\theta(\tau')$ là ước lượng của Định lý 10.4 tính tại tham số $\theta$" (+12), hoặc viết $\hat g(\tau')$ và nói "tính tại $\theta$" ở câu sau. |
| nhẹ | M6. 10.6(a) "Chọn siêu tham số" (dòng 692); 10.9(b) Bước 1 (dòng 911); 10.6(c) (dòng 734) | 692: sau khi cắt, "cùng quy tắc cho hai phương pháp" đứng sau dấu phẩy mà không có giới từ. 911: "vốn có" là khẩu ngữ. 734: một câu khoảng 55 tiếng nối năm vế bằng dấu chấm phẩy (van-phong §9). | 692: "theo (T7), cùng quy tắc cho hai phương pháp."; 911: "với mọi $u\in W$, vốn có $\lVert w_1-u\rVert\le R$"; 734: "Chỉ có thứ tự A rồi B; mỗi bước phát lại …; …; bảng chỉ ghi …" | 692: "theo (T7), với cùng quy tắc cho hai phương pháp." 911: "với mọi $u\in W$ (theo giả thiết, $\lVert w_1-u\rVert\le R$)". 734: tách sau "tinh chỉnh tính một." thành hai câu. (+3) |

**Ngân sách:** M1 ±0, M2 +8, M3 +8, M4 +8, M5 +12, M6 +3; tổng khoảng +39, tệp lên khoảng 10 000 tiếng. Nếu cần giữ dưới trần: ở M5 dùng cách thứ hai (+5); ở M3 viết "Hậu quả: phát lại gần như thành huấn luyện chung." (+3). Khi đó tổng khoảng +27, tệp khoảng 9 988.

**Kết luận: đạt.** Ba mục trung bình và các điểm nhẹ của vòng trước đã đóng; phần áp dụng một phần N12 có lý do chấp nhận được. 10.1(f) đo đúng vế "điều kiện đổi chỗ đạo hàm và kì vọng" của mục tiêu 2, và gợi ý 1 không lộ lời giải. Phần cắt chữ không làm mất bước hay ý cần cho mục tiêu, trừ vế kết luận ở M4. Hai dòng §11 của ghi chú đúng. Sáu mục nhẹ mới (M1–M6) nên sửa trong cùng vòng chỉnh câu chữ; chúng không chặn bàn giao.
