# Báo cáo phản biện §8 — `2627-1/materials/lec-02/lecture-note.md`

## Kết quả kiểm

**Đã đạt (không có vấn đề):**
- **(1) Khối đánh số, con số, kết quả, công thức:** Mệnh đề 02.17 (a)(b)(c), Ví dụ 02.11 (48/37/30/14), Ví dụ 02.12 (bảng 738/185, 1659/415, 6636/1659, 153/77, 2120/530, 8478/2120, 199/100), Nhận xét 02.18 — tất cả còn nguyên, đúng số. Các công thức `aligned` hợp lệ KaTeX, dấu phẩy thập phân `{,}` nhất quán.
- **(2) Không thêm khẳng định mới:** các sửa trong §8 chỉ là đổi thuật ngữ, bỏ câu điều hướng, bỏ nhãn "**Kết luận.**".
- **(3) Thuật ngữ:** "khả diễn"/"bất khả diễn"/"tập huấn luyện" được áp dụng đúng toàn §8 (khớp `thuat-ngu.md` §5 và `van-phong-tac-gia.md` §5); không còn "khả thực" trong §8.
- **(4) Tiếng Việt/Ký tự:** không lỗi ký tự, không dấu cách trước "?", `\Pr` dùng đúng.
- **(5) Phạm vi:** mọi sửa nằm trong §8.

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | dòng 877 (chứng minh Mệnh đề 02.17) | Giữ nhãn "**Lộ trình.**" (báo trước các bước chứng minh) trong khi cùng tệp đã bỏ "**Lộ trình.**" khỏi chứng minh Hệ quả 02.16 — không nhất quán khi áp dụng quy tắc cắt "câu điều hướng, báo trước" (`van-phong-tac-gia.md` §2 mục 2) | dòng 877: "**Lộ trình.** Tính xác suất để một giả thuyết xấu khớp mẫu, cộng trên các giả thuyết xấu bằng bất đẳng thức hợp, rồi dùng tính khả diễn để nghiệm ERM khớp mẫu." — đối chiếu diff đã xóa "**Lộ trình.** Một bước tất định trên biến cố $r$-đại diện, rồi Định lý 02.14." | Bỏ dòng "**Lộ trình.**" cho nhất quán với Hệ quả 02.16 (hoặc giữ lại ở cả hai chỗ) |
| nhẹ | dòng 995 (§9, ngoài §8) | "khả thực" còn sót ở §9 trong khi §8 đã đổi sang "khả diễn" — hệ quả của việc đổi thuật ngữ, chưa được sửa | dòng 995: "cho trường hợp khả thực (Mệnh đề 02.17)" | Đổi thành "khả diễn" khi sửa §9 (ngoài phạm vi §8, chỉ báo cho điều phối) |
| nhẹ | dòng 861, 862 (Giả thiết Mệnh đề 02.17) | Ghi chú "chỉ phần (c) dùng thành phần này" lặp hai lần — là ghi chú về nơi dùng giả thiết, thuộc loại "commentary on technicalities" mà văn phong khuyến khích cắt | dòng 861: "Tính khả diễn. $(D,\mathcal H)$ khả diễn (Định nghĩa 01.16); chỉ phần (c) dùng thành phần này."; dòng 862: "…; chỉ phần (c) dùng thành phần này." | Cân nhắc bỏ cụm "chỉ phần (c) dùng thành phần này" ở cả hai dòng (giữ nguyên giả thiết) |

**Ghi chú:** các dẫn chiếu còn lại trong §8 (Định nghĩa 01.16, 01.20, Ví dụ 01.6, 01.9, Mệnh đề 02.17(a), Bước 3 chứng minh) đều là dẫn chiếu hợp lệ — người đọc phải mở để lấy số hoặc phát biểu, nên được giữ đúng quy tắc.