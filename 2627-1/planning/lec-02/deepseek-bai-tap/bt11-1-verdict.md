VERDICT: chấp nhận

Tôi đã kiểm tra lại toàn bộ phần Bài tập 02.11 (dòng 907–hết tệp) trong `2627-1/materials/lec-02/exercises.md` theo diff đã cho và các quy tắc văn phong.

## Kết quả kiểm tra

**1. Thuật ngữ (bắt buộc, 25 chỗ toàn tệp)**
- "bất khả tri" → "bất khả diễn": dòng 909 (Mức độ), 914 (đề a), 726, 740, 902, 272, 666 — đã đổi đúng.
- "khả thực" → "khả diễn": dòng 584, 586, 589, 657, 666, 669, 675, 677, 689, 705, 730, 740, 902 — đã đổi đúng.
- "hàm chỉ thị" → "hàm chỉ báo": dòng 784 — đã đổi đúng.
- "trước mẫu" → "trước khi lấy mẫu": dòng 495, 545, 577, 707 — đã đổi đúng.
- Các thuật ngữ khác ("tập huấn luyện", "phân bố", "dữ liệu có nhiễu", "Lời giải") đã đúng, không cần đổi. ✓

**2. Cấu trúc khối và số khối**
- Bài 02.11 giữ đúng 1 `::: exercise`, 3 `::: hint`, 1 `::: solution`. Không thêm/bớt khối. ✓
- Nhãn "::: solution Lời giải Bài tập 02.11" đúng (không phải "Đáp án"). ✓

**3. Lời giải từng bước**
- Giữ nguyên các bước "**Bước 1/2/3/4**" và `aligned` cho tính toán nhiều bước (Bước 4(a), Bước 3(b), (c)). Không gộp bước tính toán thật sự. ✓
- Nhãn bước đặt theo kết quả ("**Cỡ mẫu với miền $[a,b]$.**", "**Bước tất định.**", "**Đổi thang đo.**") — đúng văn phong tác giả. ✓

**4. "Lộ trình."**
- Bài tập không có nhãn này; diff không xóa nhãn nào. Quy tắc là "không xóa", không bắt buộc thêm. Không vi phạm. ✓

**5. Con số, kết quả, dẫn chiếu**
- Cỡ mẫu $17\,539$, $17\,538{,}04=16\cdot1096{,}13$, $1097$ của Ví dụ 02.9, $M(0{,}1;0{,}05)=17\,539$ — đã kiểm số học, đúng. ✓
- "Kiểm tra lại" (dòng 989): $8\sqrt{\ln240/35078}\approx0{,}099997\le0{,}1$; với $m=17538$ giá trị $\approx0{,}1000001>0{,}1$. Đúng. ✓
- Dẫn chiếu Định nghĩa 01.25, Hệ quả 02.16(c), Định lý 02.7(c), Ví dụ 02.9, Bước 2 chứng minh Hệ quả 02.16 — đều trỏ tới nội dung còn tồn tại trong ghi chú đã sửa. ✓
- Công thức (a) $\lceil2(b-a)^2\ln(2K/\delta)/\epsilon^2\rceil$ khớp ghi chú dòng 415 ("các cỡ mẫu dựng từ Định lý 02.7 nhân thêm $(b-a)^2$"). ✓

**6. Công thức $\ell_c$ (dòng 922, tùy chọn)**
- $\ell_c(h,(x,y))=4\cdot\mathbb 1[h(x)=0,\,y=1]+\mathbb 1[h(x)=1,\,y=0]$ — đúng với $(c_{FP},c_{FN})=(1,4)$: FN=4, FP=1, đúng khi $h(x)=y$ là 0. Không đổi giá trị (1, 4, 0). Đây là "viết công thức thay mô tả bằng lời" hợp lệ theo văn phong tác giả, không thêm khẳng định/số liệu mới. ✓

**7. no-ai-slop**
- Không có câu mở đầu rào đón, kết thúc tổng kết thừa, in đậm trang trí thừa. "**Kiểm tra lại.**" là bước kiểm số thực chất. ✓
- KaTeX hợp lệ (các khối `aligned`, `\mathbb 1`, `\,`, `\Big\lceil`). ✓
- Tiếng Việt chuẩn, không có khoảng trắng trước "?", không dùng em-dash. ✓

## Phát hiện nhẹ (không bắt buộc sửa)

1. **Dòng 922 — hai dấu hai chấm trong một câu.** "Xét ví dụ sàng lọc: … với $(c_{FP},c_{FN})=(1,4)$: $\ell_c(...)=...$." Dấu hai chấm thứ hai giới thiệu công thức (đối tượng cụ thể), hợp lệ theo văn phong tác giả, không phải "colon reveal" kiểu faux-insight. Có thể để nguyên; nếu muốn gọn có thể viết "… với $(c_{FP},c_{FN})=(1,4)$, tức $\ell_c(...)=...$." — nhưng không bắt buộc.

2. **Lời giải 02.11 dài nhưng không có nhãn "**Lộ trình.**".** Quy tắc chỉ cấm *xóa* nhãn, không bắt buộc *thêm*; bản gốc cũng không có, diff không đụng tới lời giải. Không vi phạm, không cần sửa.

## Kết luận

Không có lỗi chặn, lỗi nghiêm trọng hay lỗi trung bình. Toàn bộ thay đổi bắt buộc (25 chỗ thuật ngữ) và tùy chọn (cắt 4 cụm Phụ lục B.1/B.2, viết công thức $\ell_c$) đã được áp dụng đúng, giữ nguyên mọi con số, kết quả, cấu trúc khối và kí hiệu toán. Phần Bài tập 02.11 đạt yêu cầu.