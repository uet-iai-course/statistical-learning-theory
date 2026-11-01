Based on my review of the diff and the current state of the file, here is my report.

## Báo cáo phản biện — `## Bài tập chọn từ UML` trong `2627-1/materials/lec-03/exercises.md`

### Tóm tắt kiểm tra

**Các thay đổi trong diff thuộc phần UML** (Bài 03.7 và 03.11):
1. **Bài 03.7** (dòng 576–580): đánh số lại bước 2→5, 3→6, 4→7 trong phần (b). Đã xác minh: lời giải có chuỗi bước liên tục 1–7 (Bước 1 ở dòng 564, Bước 2–4 ở phần (a), Bước 5–7 ở phần (b)). Đánh số nhất quán, không trùng, không bỏ sót. ✓
2. **Bài 03.11** (dòng 774–856): đổi "khả thực"→"khả diễn", "bất khả tri"→"bất khả diễn". Đã xác minh toàn bộ 7 chỗ đổi đều đúng thuật ngữ, khớp ghi chú (Định nghĩa 01.16, Định lý 03.17, Nhận xét 01.26). ✓

**Các khối đánh số, con số, kết quả, công thức**: giữ nguyên và đúng. Các trích dẫn (Định nghĩa 01.16/01.18/01.20, Nhận xét 01.26/01.30, Định lý 03.17, Mệnh đề 03.9, Bổ đề 03.12, Ví dụ 03.4/03.5/03.6) đều trỏ tới nội dung còn tồn tại trong ghi chú. ✓

**Không thêm khẳng định mới**: các thay đổi chỉ là đổi thuật ngữ và đánh số lại bước, không thêm nội dung. ✓

**KaTeX / tiếng Việt**: không phát hiện lỗi ký tự hay KaTeX hỏng trong các dòng đổi. ✓

**Không sửa ngoài phạm vi**: các thay đổi trong diff nằm đúng trong tệp bài tập. ✓

### Các vấn đề còn sót

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|
| trung bình | Bài 03.11, Gợi ý 2, dòng 789 | "mẫu" dùng để chỉ tập huấn luyện $S$, vi phạm quy tắc thuật ngữ ("mẫu" → "tập huấn luyện" khi chỉ dữ liệu huấn luyện; không thuộc ngoại lệ "cỡ mẫu/lấy mẫu/tên mẫu cụ thể") | "Tại một điểm $c\in C$ không xuất hiện trong **mẫu**, nhãn $f(c)$ độc lập với mọi thứ thuật toán thấy." | Đổi "trong mẫu" → "trong tập huấn luyện" |
| trung bình | Bài 03.11, lời giải Bước 2, dòng 801 | "mẫu" chỉ tập huấn luyện $S$ | "Với **mẫu** có tập đầu vào $V=\{X_1,\ldots,X_m\}$ và mọi hàm $g$," | Đổi "Với mẫu" → "Với tập huấn luyện" |
| trung bình | Bài 03.11, lời giải Bước 4, dòng 812 | "mẫu" chỉ tập huấn luyện $S$ | "…$A(S)$ cố định vì $A$ là một ánh xạ của **mẫu** (Định nghĩa 01.4)." | Đổi "ánh xạ của mẫu" → "ánh xạ của tập huấn luyện" |

### Nhận xét bổ sung

- Các chỗ "mẫu" nêu trên là văn bản có sẵn (không nằm trong diff), nhưng thuộc phần UML đang xét và vi phạm quy tắc thuật ngữ đã áp dụng cho phần còn lại của tệp (ví dụ dòng 231 đã được đổi "Trên mẫu $S$" → "Trên tập huấn luyện $S$"). Vì nhiệm vụ là "sửa bộ bài tập Bài 03 theo cùng quy tắc", các chỗ này nên được sửa cho nhất quán.
- Các chỗ "mẫu" khác trong phần UML (dòng 781 "độ phức tạp mẫu", dòng 852 "độ phức tạp mẫu") là thuật ngữ chuẩn "sample complexity", không cần sửa.
- Các thay đổi trong diff thuộc phần "Bài tập gốc" (dòng 33, 114, 178, 231, 436, 472, 516) nằm ngoài phần đang xét nhưng đều đúng quy tắc (kiểm→kiểm tra, khoảng một điểm→các khoảng một điểm, mẫu→tập huấn luyện, bỏ câu điều hướng, chỉ thị→chỉ báo). Không phát hiện vấn đề ở đó.

**Kết luận**: Các thay đổi trong diff của phần UML đều đúng và nhất quán. Không có lỗi chặn bàn giao hay nghiêm trọng. Còn 3 chỗ dùng "mẫu" thay cho "tập huấn luyện" trong Bài 03.11 (mức trung bình) cần sửa để hoàn tất việc áp dụng quy tắc thuật ngữ.