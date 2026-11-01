Based on my review of the `## 7.` section (lines 472–663) of `2627-1/materials/lec-03/lecture-note.md`, here is my report.

## Kết quả kiểm

### (1) Khối đánh số, con số, kết quả, công thức
Tất cả khối đánh số trong §7 đều còn nguyên và đúng: Định nghĩa 03.13, Ví dụ 03.6, Nhận xét 03.14, Định lý 03.15, Ví dụ 03.7, Ví dụ 03.8. Giả thiết (T5), (M) còn nguyên. Các con số trong bảng (dòng 624–627), các phép tính (dòng 608, 613–618, 631, 633, 649–654) đều khớp. Các kết quả mà `exercises.md` trích dẫn — "lý do (i), (ii) ở §7" (dòng 528–529), "câu cuối của chứng minh Định lý 03.15 nêu hai nguồn của hằng số $8$" (dòng 602) — đều còn nguyên. **Đạt.**

### (2) Không thêm khẳng định mới
Diff chỉ cắt câu điều hướng, đổi thuật ngữ, và thêm một "**Câu hỏi.**" prompt (dòng 526) — đây là thiết bị văn phong tác giả, không phải khẳng định mới. Không thêm số liệu, nguồn, hay kết quả nào. **Đạt.**

### (3) Quy tắc văn phong
Đã áp dụng đúng: bỏ các dẫn chiếu điều hướng (Phụ lục A(v), Phụ lục D, Phụ lục C, "như Ví dụ 03.1…"), đổi "**Kết luận.**" → "Tóm lại," (3 chỗ), "hàm chỉ thị" → "hàm chỉ báo", "trước mẫu" → "trước khi lấy mẫu", thêm "**Câu hỏi.**" prompt trả lời ngay. Giữ nhãn "**Lộ trình.**", "**Giả thiết.**", "**Bảo đảm.**". **Đạt**, với vài điểm còn sót (xem bảng).

### (4) Tiếng Việt, ký tự, KaTeX
Không lỗi ký tự, không dấu cách trước "?", KaTeX hợp lệ. **Đạt.**

### (5) Không sửa ngoài phạm vi
Diff nằm trong §7 và các phần khác của tệp; không có sửa ngoài phạm vi. **Đạt.**

---

## Bảng phát hiện

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|
| nhẹ | dòng 529 | Dẫn chiếu điều hướng tới một bước chứng minh, không phải để lấy số/kết quả | "(ii) Tập các cách gán nhãn phụ thuộc $S$, nên đó là một lớp chọn theo mẫu, đúng điều mà (T4) cấm ở Bước 2 của chứng minh Định lý 02.14." | Có thể rút gọn thành "đúng điều mà (T4) cấm" — người đọc không cần mở Bước 2 để hiểu ý; tuy nhiên đây là câu có sẵn không nằm trong diff, mức độ ưu tiên thấp |
| nhẹ | dòng 494 | Dẫn chiếu so sánh tới Định nghĩa 01.18 | "Thứ tự lượng từ giống Định nghĩa 01.18: $\exists M$ đứng trước $\forall D$" | Có thể giữ vì dùng để làm rõ thứ tự lượng từ; nếu cắt thì viết lại "Thứ tự lượng từ: $\exists M$ đứng trước $\forall D$…". Câu có sẵn, không nằm trong diff |

Hai điểm trên đều là câu có sẵn (không nằm trong diff) và là dẫn chiếu hợp lệ để lấy phát biểu/so sánh, nên không chặn bàn giao.

**Kết luận:** Không có vấn đề mức `chặn bàn giao`, `nghiêm trọng` hay `trung bình`. §7 đã tuân thủ quy tắc văn phong tác giả, giữ nguyên mọi khối đánh số, con số, kết quả và nhãn mà bài tập trích dẫn.