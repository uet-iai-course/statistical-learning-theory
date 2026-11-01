# Báo cáo phản biện — §5 "Nửa không gian và hàm phân lớp tuyến tính" (Bài 03)

Tôi đã đối chiếu §5 (dòng 238–339) với diff, tệp chuẩn văn phong, và `exercises.md`. Kết quả tổng thể: bản sửa trung thành — không khối đánh số nào bị xóa/đổi số, không con số nào đổi, không khẳng định mới, KaTeX hợp lệ, tiếng Việt chuẩn. Các cắt giảm trong §5 đều là câu điều hướng/dẫn chiếu (đúng quy tắc), không cắt kết quả. Các khối §5 được bài tập trích dẫn (Mệnh đề 03.9(a)/(b), Nhận xét 03.10(ii)/(iii), Ví dụ 03.3, Bổ đề 03.8, Định nghĩa 03.7) đều còn nguyên.

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|
| trung bình | dòng 308, Bước 4 ((b), cận trên) | Sau khi bỏ "được chứng minh ở Phụ lục A", bước chứng minh cận trên $d\le p$ chỉ còn là một câu nêu phương pháp ("dùng phụ thuộc tuyến tính của $p+1$ véc-tơ trong $\mathbb R^p$") mà không trình bày lập luận, đồng thời mất dẫn chiếu tới nơi có chứng minh đầy đủ. Người đọc muốn lấy khẳng định $d\le p$ phải mở Phụ lục A — đúng trường hợp quy tắc 3 cho phép *giữ* dẫn chiếu ("Chỉ giữ một dẫn chiếu khi người đọc thật sự cần mở nơi được dẫn"). | "**Bước 4 ((b), cận trên).** Cận trên $d\le p$ dùng phụ thuộc tuyến tính của $p+1$ véc-tơ trong $\mathbb R^p$." | Cân nhắc giữ lại dẫn chiếu tới Phụ lục A cho riêng bước này (khác với hai tiêu đề Bổ đề 03.8/Mệnh đề 03.9, nơi "Ý chứng minh"/chứng minh đầy đủ đã có trong ghi chú). Đây là quyết định biên; nếu giữ nguyên, nên xác nhận với tác giả. |
| nhẹ | dòng 314, Ví dụ 03.3, "Thiết lập." | Câu "Ví dụ chỉ xét lớp, không cần phân bố hay mẫu." là câu nói hiển nhiên về tính ngẫu nhiên — đúng loại quy tắc 6 (§2 van-phong) yêu cầu cắt ("Không có mẫu, nên mọi đại lượng đều cố định"). Còn sót trong phần này, không nằm trong diff. | "Ví dụ chỉ xét lớp, không cần phân bố hay mẫu." | Cắt câu này; "Thiết lập." chỉ cần "$p=2$ và lớp $\mathcal H^2_{\mathrm{aff}}$ của các nửa mặt phẳng, có $d=3$ theo Mệnh đề 03.9(a)." |
| nhẹ | dòng 327 | Sau khi bỏ "nhận xét sau cho thấy", câu "điều đó không đúng nói chung" thành khẳng định trần. Tuy nhiên Nhận xét 03.10 ngay sau đó minh họa ngay, nên mạch văn vẫn đứng — chỉ ghi nhận, không bắt buộc sửa. | "Với nửa không gian afin, hai số trùng nhau; điều đó không đúng nói chung." | Không cần sửa; nếu muốn chặt hơn có thể nối: "…; điều đó không đúng nói chung, như Nhận xét 03.10 cho thấy." |

**Các kiểm khác — đạt:**
- (1) Khối đánh số, con số, kết quả, công thức: nguyên vẹn. Các cắt trong §5 (dòng 253, 259, 274, 293, 316, 324, 327, 333) đều là điều hướng/dẫn chiếu, không cắt kết quả.
- (2) Không thêm khẳng định, số liệu, nguồn mới.
- (3) Văn phong: đã áp dụng đúng — in nghiêng thuật ngữ mới (*nửa không gian*, *siêu phẳng*, *đơn hình*, *phân hoạch Radon*), bỏ nhãn "**Kết luận.**" → "Tóm lại," (dòng 324), bỏ dẫn chiếu Phụ lục A và bài tập, giữ "**Lộ trình.**" (dòng 284), giữ "**Giả thiết.**/**Bảo đảm.**" cho Bổ đề 03.8 và Mệnh đề 03.9.
- (4) Tiếng Việt chuẩn, không lỗi ký tự; các khối `$$...$$` (dòng 262–268, 287–292, 298–303) hợp lệ KaTeX.
- (5) Không sửa ngoài phạm vi §5.

Không có mức **chặn bàn giao** hay **nghiêm trọng**.