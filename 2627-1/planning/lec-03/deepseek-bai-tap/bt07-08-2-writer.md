Tôi đã xác minh xong. Đây là báo cáo phản biện của tôi.

---

## Báo cáo phản biện — `2627-1/materials/lec-03/exercises.md`

**PHÁN QUYẾT: yêu cầu sửa** (3 chỗ, đều ở Bài 03.11)

### Xác minh các phát hiện của báo cáo phản biện

Cả 3 phát hiện đều **đúng** — tôi đã đọc trực tiếp các dòng tương ứng trên tệp hiện tại:

1. **Dòng 789** (Gợi ý 2, Bài 03.11): "Tại một điểm $c\in C$ không xuất hiện trong **mẫu**, nhãn $f(c)$ độc lập với mọi thứ thuật toán thấy." — "mẫu" chỉ tập huấn luyện $S$. **Vi phạm** quy tắc thuật ngữ ("mẫu" → "tập huấn luyện" khi chỉ dữ liệu huấn luyện).

2. **Dòng 801** (Bước 2, Bài 03.11): "Với **mẫu** có tập đầu vào $V=\{X_1,\ldots,X_m\}$ và mọi hàm $g$," — "mẫu" chỉ tập huấn luyện $S$. **Vi phạm**.

3. **Dòng 812** (Bước 4, Bài 03.11): "…$A(S)$ cố định vì $A$ là một **ánh xạ của mẫu** (Định nghĩa 01.4)." — "mẫu" chỉ tập huấn luyện $S$. **Vi phạm**.

### Xác minh các thay đổi trong diff

- **Bài 03.7 đánh số lại bước** (dòng 576–580): Bước 1 (dòng 564), Bước 2–4 (phần a, dòng 568–572), Bước 5–7 (phần b, dòng 576–580). Chuỗi liên tục 1–7, không trùng, không bỏ sót. ✓
- **"khả thực"→"khả diễn", "bất khả tri"→"bất khả diễn"** (Bài 03.11): cả 7 chỗ đổi đều đúng thuật ngữ, khớp ghi chú. ✓
- **Các thay đổi ở "Bài tập gốc"** (dòng 33, 114, 178, 231, 436, 472, 516): "kiểm tra", "các khoảng một điểm", "tập huấn luyện $S$", bỏ "đoạn sau Định lý 03.15,", bỏ câu điều hướng, "véc-tơ chỉ báo" — tất cả đều đúng quy tắc. ✓
- **Không thêm khẳng định, số liệu, nguồn mới**; các trích dẫn (Định nghĩa 01.16/01.18/01.20, Nhận xét 01.26/01.30, Định lý 03.17, Mệnh đề 03.9, Bổ đề 03.12, Ví dụ 03.4/03.5/03.6) đều trỏ tới nội dung còn tồn tại trong ghi chú. ✓

### Danh sách sửa cụ thể cho writer

| Vị trí | Văn bản hiện có | Văn bản đích |
|---|---|---|
| Dòng 789, Gợi ý 2, Bài 03.11 | "không xuất hiện trong **mẫu**" | "không xuất hiện trong **tập huấn luyện**" |
| Dòng 801, Bước 2, Bài 03.11 | "Với **mẫu** có tập đầu vào" | "Với **tập huấn luyện** có tập đầu vào" |
| Dòng 812, Bước 4, Bài 03.11 | "ánh xạ của **mẫu**" | "ánh xạ của **tập huấn luyện**" |

### Nhận xét bổ sung

- Các chỗ "cỡ mẫu", "mẫu bóng", "lấy mẫu", "trước khi lấy mẫu", "sau khi xem mẫu", "độ phức tạp mẫu" (dòng 5, 211–339, 362–454, 781, 852) đều là thuật ngữ chuẩn hoặc ngoại lệ hợp lệ, không cần sửa. ✓
- **Dòng 323** (Bài 03.4, "Bài tập gốc"): "độ lệch đều bằng $1$ trên mọi **mẫu**" — cũng dùng "mẫu" chỉ tập huấn luyện, là vi phạm tương tự. Nằm ngoài phạm vi UML mà báo cáo phản biện xét, nhưng nếu nhiệm vụ là sửa toàn bộ tệp theo quy tắc thì nên sửa luôn: "trên mọi **tập huấn luyện**".

---

**Tóm tắt:** Báo cáo phản biện chính xác. Diff đã đúng quy tắc; còn 3 chỗ dùng "mẫu" thay cho "tập huấn luyện" trong Bài 03.11 cần sửa để hoàn tất việc áp dụng quy tắc thuật ngữ. Không có lỗi chặn bàn giao hay nghiêm trọng.