Tôi đã đọc toàn bộ phần `## Phụ lục` (dòng 931–1132) và đối chiếu với diff, `exercises.md`, cùng các quy tắc văn phong. Dưới đây là báo cáo phản biện.

## Tóm tắt kiểm tra

- **(1) Khối đánh số, con số, kết quả, công thức:** ĐẠT. Mọi số (p+2, p+1, 2m, mε²≥2, ε/2, 1/4, 1/mε²≤1/2, 2e^(−mε²/8), 4Π(2m)e^(−mε²/8), 8ln4≈11,09, (2em/d)^d, 1+ln2, 16(dln(em/d)+ln(2/δ))/m, κ=8/ε², u₀=4eκ, 16/ε²(dln(32/ε²)+ln(4/δ)), …) đều nguyên vẹn. Các nhãn `exercises.md` trích dẫn — "câu cuối của Phụ lục C" (dòng 1112), "Bước 6 của Phụ lục B" (dòng 1014), "Phụ lục A" — đều còn nguyên.
- **(2) Không thêm khẳng định mới:** ĐẠT. Thay đổi duy nhất trong phần này là dòng 1086 "tự thỏa" → "được thỏa", chỉ đổi từ ngữ, không thêm nội dung.
- **(3) Quy tắc văn phong:** ĐẠT phần lớn; còn 2 điểm nhẹ (xem bảng).
- **(4) Tiếng Việt chuẩn, KaTeX hợp lệ:** ĐẠT. Không lỗi ký tự; mọi khối `$$...$$`/`aligned` hợp lệ.
- **(5) Không sửa ngoài phạm vi:** ĐẠT. Thay đổi duy nhất trong Phụ lục là dòng 1086, đúng phạm vi.

## Bảng phát hiện

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|
| nhẹ | dòng 1026 | "mẫu" dùng chung chung để chỉ cặp tập huấn luyện (S,S′), chưa theo quy tắc "mẫu" → "tập huấn luyện" khi chỉ dữ liệu huấn luyện (giữ "cỡ mẫu", "lấy mẫu", tên mẫu cụ thể như "mẫu bóng"). | "Theo đoạn sau (M) ở §7, với mọi **cặp mẫu**," | Đổi thành "với mọi cặp tập huấn luyện" (hoặc "với mọi cặp (S,S′)"). |
| nhẹ | dòng 1026 | Con trỏ tới trước "Theo đoạn sau (M) ở §7" — quy tắc cắt con trỏ điều hướng trừ khi người đọc phải mở ra để lấy số/khẳng định. Đây là trường hợp biên: trong phụ lục chứng minh, tham chiếu tới khẳng định đo được ở §7 là cần thiết để theo dõi, nên có thể chấp nhận. | "**Theo đoạn sau (M) ở §7**, với mọi cặp mẫu," | Có thể giữ (cần thiết cho chứng minh); nếu muốn gọn, thay bằng "Theo khẳng định đo được sau (M) ở §7" hoặc nêu lại ngắn gọn khẳng định đó. |

## Ghi chú

- Thay đổi dòng 1086 ("tự thỏa" → "được thỏa") đúng quy tắc cắt lời bình "điều kiện tự thỏa" (commentary on technicalities) và không làm đổi nghĩa; câu tiếp theo vẫn giải thích vì sao điều kiện được thỏa.
- Dòng 1112 ("Mọi giả thiết đều được dùng: (T1) ở C.2…") là "câu cuối của Phụ lục C" mà `exercises.md` dòng 250 trích dẫn, nên **phải giữ nguyên** — không coi là lời bình cần cắt.
- Không có mức `chặn bàn giao`, `nghiêm trọng` hay `trung bình` nào trong phần Phụ lục.