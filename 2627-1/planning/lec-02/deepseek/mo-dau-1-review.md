Tôi đã hoàn tất việc xem xét phần `## Câu hỏi mở đầu` (dòng 7–11) trong `2627-1/materials/lec-02/lecture-note.md` và đối chiếu với diff, chuẩn văn phong tác giả, và `exercises.md`.

## Kết quả kiểm

**(1) Khối đánh số, con số, kết quả, công thức:** Phần này không có khối đánh số. Các con số `$5\%$`, `$1000$`, `$95\%$`, `$1000$` ở dòng 9 và 11 đều được giữ nguyên và đúng. `exercises.md` không trích dẫn nhãn/con số nào từ phần này. ✓

**(2) Không thêm khẳng định mới:** Bản sửa chỉ cắt một đoạn, không thêm gì. ✓

**(3) Quy tắc văn phong:** Đoạn bị xóa là đoạn tự hỏi tự đáp ("Có dùng được cùng một câu trả lời… Không: …") kèm câu điều hướng ("nằm ở §5", "nằm ở §6") — đúng hai loại tác giả yêu cầu bỏ (§2.7 và §2.2 của `van-phong-tac-gia.md`). Câu hỏi mở đầu còn lại là câu hỏi mở, không gợi sẵn đáp án. ✓

**(4) Tiếng Việt chuẩn, KaTeX hợp lệ:** Không có dấu cách trước "?", `$5\%$`, `$1000$`, `$95\%$` đều hợp lệ. ✓

**(5) Không sửa ngoài phạm vi:** Các thay đổi khác trong diff (khả thực→khả diễn, bất khả tri→bất khả diễn, bản có nhiễu→dữ liệu có nhiễu, Mẫu→Tập huấn luyện, bỏ câu điều hướng) đều khớp bảng thuật ngữ §5 và quy tắc §2.2 của chuẩn — nằm trong phạm vi nhiệm vụ sửa toàn bài. ✓

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | dòng 9 | Thuật ngữ mới "mẫu xác thực (validation sample)" ở lần dùng đầu không in nghiêng, trong khi chuẩn §1/§7.7 yêu cầu "in nghiêng thuật ngữ mới". | "Một hàm phân lớp (classifier) sai $5\%$ trên một mẫu xác thực (validation sample)…" | Có thể in nghiêng *mẫu xác thực* ở lần dùng đầu. Lưu ý: đây là quy ước có sẵn của toàn tệp (12 chỗ dùng, không chỗ nào in nghiêng, kể cả chỗ định nghĩa chính thức ở §3), không phải do bản sửa này gây ra; nếu giữ nhất quán với tệp thì không cần sửa. |

## Kết luận

Không có vấn đề **chặn bàn giao**, **nghiêm trọng** hay **trung bình** trong phần `## Câu hỏi mở đầu`. Bản sửa cắt đúng đoạn tự hỏi tự đáp và câu điều hướng theo đúng văn phong tác giả, giữ nguyên mọi con số, không thêm khẳng định, tiếng Việt và KaTeX chuẩn. Chỉ có một quan sát mức **nhẹ** (in nghiêng thuật ngữ mới) mang tính tùy chọn và nhất quán với quy ước sẵn có của tệp.