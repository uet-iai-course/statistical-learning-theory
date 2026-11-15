# Kiểm lại sau biên tập, lượt 2 — deck Bài 08

Vai: kiểm lại (chỉ đọc). Ngày 2026-11-16. Đầu vào: deck sau lượt sửa 2, `reviews/deck-kiem-lai-1.md`, `storyboard.md` mục 17 bảng "Lượt 2", ghi chú Bài 08, `exercises.md`. Cách so: diff mặt trang và ghi chú diễn giả với bản đóng băng, rồi so diff đó với diff đã kiểm ở lượt 1 để tách phần đổi mới. `no-ai-slop` chế độ Detect cho câu mới.

## 1. Kiểm máy (chạy trong lượt này)

- `deck_lint.py`: 0 phát hiện, 55 trang. `footer_check.py`: 0 trang.
- `deck_check.py --shots`: console 0, pageerrors 0, failed 0, `katexErr` 0 ở mọi trang. OVERFLOW chỉ ở 2-03, 5-01, 5-02, 5-05, 7-07 (có `\sqrt`, báo động giả đã biết).
- Ảnh 390×844 (kể cả `-end`) đã xem: 1-06, 2-03, 2-06, 3-01, 4-01, 5-01, 5-02, 5-03, 5-04, 6-06, 7-01, 7-04. Thư mục nháp `lec-08/recheck2/`.

Phần đổi trong lượt 2: mặt trang 1-06, 2-03, 2-06, 3-01, 4-01, 5-01, 5-02, 5-03, 5-04, 6-06, 7-01, 7-04; ghi chú diễn giả 1-02, 4-07, 7-03. Không trang nào khác đổi.

## 2. Phát hiện lượt 1 → trạng thái

| Phát hiện | Trạng thái | Bằng chứng |
|---|---|---|
| T1 (5-01) | đã sửa | "nếu $\eta^*\le2/\beta$, vế phải (a) tại $\eta=\eta^*$ không vượt $RG\sqrt{3/m}$ khi $T=m$, $\to RG\sqrt{2/m}$ khi $T\to\infty$"; ảnh 390 px không còn đọc nhầm |
| T2 (5-04) | đã sửa | "khi nhiều điểm có $L_s$ nhỏ như nhau, khởi tạo, độ dài bước, số bước và cách rút chỉ số quyết định điểm trả về, không qua số hạng phạt" (đủ bốn lựa chọn của ghi chú dòng 716; "khi" mở mệnh đề nên chủ ngữ của "quyết định" rõ). Cắt bù làm mất một điều kiện (T3 mới) |
| N1 (2-06) | đã sửa | "$\Delta_7=\tfrac54\le2\cdot2G\eta=2$ trên một dãy chỉ số; Định nghĩa 06.9 lấy kì vọng theo $\xi$, nên cần hai sự kiện trên với mọi dãy." |
| N2 (4-01) | đã sửa | "hiệu hàm lỗi tại mọi $z$ không quá $G\Delta_{T+1}$" |
| N3 (2-03) | đã sửa | "hồ sơ được dùng lại" |
| N4 (7-01) | đã sửa | "Các cận ổn định theo kì vọng, …" |
| N6 (7-04) | đã sửa | "(c) Lập bảng giả thiết của Định lý 08.6: thỏa, không thỏa, không xác định; …" |
| N7 (6-06) | đã sửa | "$0{,}99\mapsto1{,}49$; $1{,}01\mapsto1{,}01$" |
| N8 (5-02, 1-06, 3-01, 5-03) | đã sửa | ảnh 390 px: không còn dấu câu mồ côi ở bốn trang. 5-03 có lỗi hiển thị nhỏ mới (N12) |
| N9, N10, N11 (ghi chú 1-02, 4-07, 7-03) | đã sửa | câu điều hướng và câu lặp đề đã cắt; 7-03 thêm "Định lý 08.6 đúng theo kì vọng, cho một thuật toán" |

## 3. Cắt bù tự quyết của người sửa

| Chỗ cắt | Đánh giá |
|---|---|
| 5-01 bỏ chỉ số $S,\xi$ dưới $\mathbb E$ ở (a) | không mất ý: dòng mở "**Bảo đảm:** kì vọng theo $(S,\xi)$" ghi loại kì vọng ngay trước công thức; các trang 7-02 và Hệ quả 08.8 ghi chú dùng cùng nghĩa |
| 5-01 giả thiết "$\eta\in(0,2/\beta]$ hằng" | tương đương "$0<\eta\le2/\beta$ hằng": đạt |
| 5-01 "Nhắc lại:" rút gọn, "$\tilde w=A(S;\xi)$" | đủ ý (định nghĩa $\operatorname{opt}_S$, Mệnh đề 06.5(b), đầu ra là đầu ra của thuật toán, nên kì vọng theo $(S,\xi)$). Kí hiệu gọn "$\mathbb E[L_D-L_S](\tilde w)$" không có trong ghi chú (N13, nhẹ) |
| 5-04 "$\operatorname{opt}_s\approx0$", "phạt $\tfrac\lambda2\lVert w\rVert^2$" | đạt (ghi chú: "về gần $0$"; "thêm một số hạng phạt") |
| 5-04 bỏ "độc lập" sau "mẫu xác thực" | **mất điều kiện** (T3) |
| 7-04 "quan sát theo (T1)" | (T1) là "độc lập cùng phân bố $D$" (1-02): tương đương đề 08.5, đạt |
| 7-04 "mọi trọng số huấn luyện", "Báo cáo viết:" | đạt; "Báo cáo viết:" là câu, không phải nhãn |
| 2-06 chú thích "$w_t$ trên $s$, $w'_t$ trên $s^{(4)}$, $t=1,\ldots,7$; bước khác biệt: $t=2$, $t=5$" | đạt: chú thích vẫn nêu dữ liệu vẽ; giá trị $s$, $z'$ có ở dòng Ví dụ 08.2 và trang 2-03, 2-05 |

## 4. Toán và mạch truyện

- Toán: không có con số mới. Các con số giữ nguyên trên trang đổi (5-01, 5-03, 6-06, 7-04) khớp kết quả đã tính lại ở lượt 1. Phát biểu 5-01 (b) nay đúng nghĩa.
- Mạch truyện: chỉ đổi câu chữ trong trang, không đổi thứ tự hay câu nối giữa các trang. 2-05 → 2-06 → 2-07: câu nối một dãy → mọi dãy rõ hơn. 5-00 → 5-01 → 5-02: liền. 7-03 → 7-04: liền. Ranh giới mạch không bị ảnh hưởng.
- Văn phong (Detect): câu mới không có mẫu cấm. "Định lý 05.14 không chặn sai số tối ưu của $w_{T+1}$, chỉ của $\bar w_T$" là phát biểu toán, không phải câu rào đón.

## 5. Phát hiện còn mở

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 5-04 (T3) | Cắt bù bỏ "độc lập" khỏi định nghĩa dừng sớm. Với mẫu xác thực phụ thuộc tập huấn luyện, cách chọn $T$ không còn hợp lệ, nên đây là điều kiện, không chỉ là câu chữ (quy định: "a compact statement may drop wording, never a condition"). 5-05 ghi chú diễn giả cũng dùng điều kiện này ("bằng mẫu xác thực độc lập"). | Mặt trang: "$T$ chọn trước hoặc bằng mẫu xác thực;". Ghi chú dòng 715: "chọn bằng một mẫu xác thực độc lập với $s$". | Trả lại "bằng mẫu xác thực độc lập"; giữ 60 bằng cách bỏ "số hạng" ở câu chính quy hóa ngầm ("không qua phạt", cùng từ với dòng trên "phạt $\tfrac\lambda2\lVert w\rVert^2$"), hoặc "cách rút chỉ số" → "cách rút". Điều phối viên đếm lại |
| nhẹ | 5-03 (N12) | Dấu hai chấm đưa vào KaTeX bị dàn cách như quan hệ: "$\eta^*\approx0{,}0289 : \le0{,}0866$", "$T\to\infty : \le0{,}0708$". | Ảnh `narrow-…-L08-5-03`: "0,0289 : ≤ 0,0866; T → ∞ : ≤ 0,0708." | Dùng `\colon` hoặc `{:}` trong KaTeX ("$\eta^*\approx0{,}0289{:}\ \le0{,}0866;$"). |
| nhẹ | 5-01 (N13) | Kí hiệu gọn "$\mathbb E[L_D-L_S](\tilde w)$" không có trong ghi chú và `ky-hieu.md`; ở mọi chỗ khác deck viết $\mathbb E[L_D(\tilde w)-L_S(\tilde w)]$. | "Mệnh đề 06.5(b): $\mathbb EL_D(\tilde w)-\inf_WL_D\le\mathbb E[L_D-L_S](\tilde w)+\mathbb E\operatorname{opt}_S(\tilde w)$" | Viết lại $\mathbb E[L_D(\tilde w)-L_S(\tilde w)]$ nếu dưới 60 âm tiết (công thức không tính vào số âm tiết) và không chạm chân trang. Chạy lại `footer_check.py` |

## 6. Kết luận

Các phát hiện của lượt 1 (T1, T2 và mười mục nhẹ) đã sửa đúng. Còn mở: chặn bàn giao 0, nghiêm trọng 0, trung bình 1 (T3: 5-04 mất "độc lập" do cắt bù), nhẹ 2 (N12, N13). Kiểm máy sạch.

**Kết luận: đạt khi sửa.** Sau khi sửa T3 (và N12, N13 nếu làm), chỉ cần kiểm lại 5-01, 5-03, 5-04: chạy `deck_lint.py`, `footer_check.py` và xem ảnh 390×844 của ba trang này.
