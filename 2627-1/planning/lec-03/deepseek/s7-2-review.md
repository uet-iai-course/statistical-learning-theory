# Báo cáo phản biện — §7 "Hội tụ đều trên lớp có chiều VC hữu hạn"

## Kết quả kiểm tra tổng quát

Tôi đã đối chiếu diff với nội dung hiện tại của §7 (dòng 472–663) và các tài liệu chuẩn. Các mục kiểm tra chính đều **đạt**:

- **Khối đánh số, con số, kết quả, công thức:** Định nghĩa 03.13, Ví dụ 03.6/03.7/03.8, Nhận xét 03.14, Định lý 03.15 (a)(b)(c), chứng minh 5 bước — tất cả còn nguyên số hiệu và nội dung. Các con số trong §7 (0{,}762, 0{,}280, 1{,}33–1{,}37, 8{,}601, 4{,}382, 0{,}322, 18\,122, 29{,}415, 0{,}027037, 0{,}1644, 11{,}09, 3{,}33…) đều khớp và không đổi. Các nhãn mà `exercises.md` trích dẫn (Định lý 03.15, Ví dụ 03.6/03.7/03.8, Nhận xét 03.14, Định nghĩa 03.13, (T5), (M)) đều còn nguyên.
- **Không thêm khẳng định mới:** Mọi thay đổi trong diff chỉ cắt câu điều hướng ("ở Phụ lục A(v) của Bài 01", "(Phụ lục D)", "(chứng minh đầy đủ ở Phụ lục C)", "ở Bước 2 của chứng minh Định lý 02.14", "như Ví dụ 03.1 và đoạn sau Định nghĩa 03.1 đã chỉ ra") và đổi nhãn "**Kết luận.**" → "Tóm lại,". "**Câu hỏi.**" mới thêm chỉ diễn đạt lại nội dung vốn có ("không lấy bất đẳng thức hợp … vì hai lý do"), không thêm ý.
- **Quy tắc văn phong:** "trước mẫu" → "trước khi lấy mẫu" (dòng 496, 533, 660); "hàm chỉ thị" → "hàm chỉ báo" (dòng 643); bỏ nhãn "**Kết luận.**" (dòng 507, 633, 660); giữ "**Lộ trình.**" và dòng **Giả thiết.**/**Bảo đảm.** của Định lý 03.15; "**Câu hỏi.**" đặt đúng chỗ hiểu lầm và trả lời ngay, đúng một câu cho §7.
- **Tiếng Việt chuẩn, KaTeX hợp lệ:** không lỗi ký tự, không dấu cách trước "?", các công thức hiển thị và `aligned` hợp lệ.
- **Phạm vi:** các thay đổi trong §7 đều nằm trong §7.

## Bảng phát hiện

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|
| trung bình | dòng 540 (khối Giả thiết của Định lý 03.15) | Nhãn "**Mẫu.**" chỉ dữ liệu huấn luyện chưa đổi thành "**Tập huấn luyện.**" theo quy ước tác giả (đã đổi ở §1 mục 2) và quy tắc thuật ngữ "mẫu" → "tập huấn luyện" khi chỉ dữ liệu huấn luyện. | `- **Mẫu.** $S\sim D^m$ theo (T1), $m\ge1$.` | Đổi thành `- **Tập huấn luyện.** $S\sim D^m$ theo (T1), $m\ge1$.` (cùng cấu trúc với §1 mục 2). Lưu ý: cùng nhãn "**Mẫu.**" còn ở §8 (dòng 672, 786) — ngoài phạm vi §7, cần sửa đồng bộ khi xử lý §8. |
| nhẹ | dòng 503 (Ví dụ 03.6, Bước 2) | "Với mỗi mẫu" chỉ dữ liệu huấn luyện, chưa đổi thành "tập huấn luyện" theo quy tắc thuật ngữ (không thuộc nhóm được giữ "cỡ mẫu"/"lấy mẫu"/tên mẫu cụ thể). | `**Bước 2: độ lệch đều.** Với mỗi mẫu, đặt $F=\{X_1,\ldots,X_m\}$.` | Đổi thành `Với mỗi tập huấn luyện, đặt $F=\{X_1,\ldots,X_m\}$.` |

## Ghi chú biên

- Các chỗ "mẫu $S$" (dòng 524, 639) và "mẫu bóng"/"mẫu gộp" (dòng 588, 596, 602, 658) được giữ là hợp lệ: $S$ là tên mẫu cụ thể, còn "mẫu bóng"/"mẫu gộp" là thuật ngữ riêng.
- "**Câu hỏi.**" ở dòng 526 là câu hỏi gợi hướng ("Tại sao không…") nhưng được trả lời ngay trong câu sau, đúng tinh thần quy tắc §7 mục 6 và giọng tác giả; không phải mẫu tự hỏi tự đáp cần cắt.
- Không có mức "chặn bàn giao" hay "nghiêm trọng" nào trong §7.