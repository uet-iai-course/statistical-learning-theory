VERDICT: yêu cầu sửa

Tôi đã tự kiểm lại các phát hiện trên tệp thực tế. Có một phát hiện đúng (nghiêm trọng) và một phát hiện cần bỏ (nhẹ, ngoài phạm vi).

## Phát hiện đúng (giữ lại)

**nghiêm trọng | Nhận xét 02.18 (dòng 988) | Cắt mất nội dung "tính cần thiết" mà exercises.md dòng 744 trích dẫn | exercises.md dòng 744: "Đây là tốc độ của các cận đủ; Nhận xét 02.18 bàn tính cần thiết của tốc độ này." Câu bị cắt trong lecture-note: "Chúng ta chưa chứng minh tốc độ $1/\epsilon^2$ là cần thiết; một cận dưới phải lập luận cho mọi thuật toán, và Bài 03 phát biểu (không chứng minh) một cận dưới như vậy." | Khôi phục phần nội dung về tính cần thiết, nhưng bỏ phần chỉ dẫn điều hướng "Bài 03 phát biểu (không chứng minh) một cận dưới như vậy" (chỉ giữ ý "chưa chứng minh tốc độ $1/\epsilon^2$ là cần thiết; một cận dưới phải lập luận cho mọi thuật toán")**

Lí do giữ: quy tắc văn phong nêu rõ "A change the author makes can break other passages: a removed claim that §9 or §11 still cites… Find those passages and fix them." exercises.md dòng 744 trích dẫn Nhận xét 02.18 *chính xác* cho nội dung "tính cần thiết của tốc độ". Sau khi cắt, Nhận xét 02.18 chỉ còn bàn hai tốc độ của Bernstein, không còn bàn tính cần thiết — dẫn chiếu của bài tập bị hỏng. Đây là vi phạm ràng buộc cứng "giữ mọi … kết quả và nhãn mà exercises.md trích dẫn".

## Phát hiện bỏ (không đúng / ngoài phạm vi)

**Phát hiện nhẹ về "khả thực" ở §9 (dòng 995) — BỎ.** Đây nằm ngoài phạm vi `## 8.` đang xét. Theo `thuat-ngu.md` ("Bài 02–10 còn dùng thuật ngữ cũ; đổi khi sửa từng bài"), việc §9 chưa đổi là hành vi dự kiến, sẽ được xử lý khi sửa §9. Không phải khuyết tật của bản sửa §8.

## Các kiểm tra đã qua (không có phát hiện)

- **Thuật ngữ §5 trong §8:** mọi "khả thực" → "khả diễn", "bất khả tri" → "bất khả diễn", "bản nhãn tất định" → "dữ liệu tất định", "mẫu" → "tập huấn luyện" đều đúng và đầy đủ trong §8. ✓
- **Cắt chỉ dẫn điều hướng (§2.2):** dòng 936 bỏ "cỡ mẫu ở §9 của Bài 01 (lập luận của Bài tập 01.9)", dòng 952 bỏ "Ba cỡ mẫu của §6–§8 trả lời…", dòng 1004 bỏ câu cuối — đúng. ✓
- **Giữ mọi khối đánh số và con số:** Mệnh đề 02.17, Ví dụ 02.11 (48/37/30/14), Ví dụ 02.12 (bảng, 1659), Nhận xét 02.18 — tất cả nhãn và số đều giữ nguyên. ✓
- **Markdown:** chỉ dùng `$...$`/`$$...$$`, không đổi kí hiệu toán, không dấu cách trước "?", dùng `\mid`/`\Pr`. ✓
- **Không thêm khẳng định/số liệu/nguồn mới** trong §8. ✓
- **"Lộ trình."** trong chứng minh Mệnh đề 02.17 được tác giả giữ (trong khi bỏ ở Hệ quả 02.16) — là lựa chọn của tác giả, không phải khuyết tật. ✓

## Danh sách sửa cụ thể cho writer

**Vị trí:** Nhận xét 02.18, dòng 988 (cuối remark).

**Văn bản hiện có:**
> … và $1/\epsilon^2$ khi phương sai cỡ hằng số (đọc thêm, Phụ lục B.5 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* của Shalev-Shwartz và Ben-David (2014), viết tắt UML).

**Văn bản đích (khôi phục nội dung cần thiết, bỏ chỉ dẫn điều hướng Bài 03):**
> … và $1/\epsilon^2$ khi phương sai cỡ hằng số (đọc thêm, Phụ lục B.5 của giáo trình *Understanding Machine Learning: From Theory to Algorithms* của Shalev-Shwartz và Ben-David (2014), viết tắt UML). Chúng ta chưa chứng minh tốc độ $1/\epsilon^2$ là cần thiết; một cận dưới phải lập luận cho mọi thuật toán.

(Lưu ý: bỏ cụm "và Bài 03 phát biểu (không chứng minh) một cận dưới như vậy" — đây là chỉ dẫn điều hướng Bài 03, đúng quy tắc §2.2; nhưng giữ nguyên phần "Chúng ta chưa chứng minh tốc độ $1/\epsilon^2$ là cần thiết; một cận dưới phải lập luận cho mọi thuật toán" vì exercises.md dòng 744 trích dẫn Nhận xét 02.18 cho nội dung này.)