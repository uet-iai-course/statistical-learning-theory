# Rà soát 4 — học thuật–sư phạm và `no-ai-slop` Detect (Bài 02, bản đóng băng 2026-10-30)

Người rà độc lập, chỉ đọc (general-purpose, opus, high), đã nạp `no-ai-slop` chế độ Detect. `forward_refs.py` 0; grep không thấy "hãy", "chúng tôi", "Mục này", "phân phối", "kỳ", "hàm mất mát", "không thấp hơn", "rõ ràng", "dễ thấy", "hoá", nhãn nội bộ. Không có lỗi chặn bàn giao. Số dòng theo tệp ghi chú.

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | Ví dụ 02.1 (95–99); bảng §2 (69–71) | Danh mục sớm các đối tượng của ví dụ xuyên suốt ($D_f$, $\mathcal M_{\mathcal X}$, $\ell_c$), trái quy tắc "not in an early catalogue" | "**Bản nhãn tất định $D_f$.**", "**Lớp mọi hàm phân lớp.**", "**Hàm lỗi có trọng số.**" | Ví dụ 02.1 chỉ giữ $D_\eta$, bảng rủi ro, phân bố nhị thức; chuyển $D_f$ vào Ví dụ 02.11, $\mathcal M_{\mathcal X}$ vào Ví dụ 02.10, $\ell_c$ vào đoạn sau (T3) |
| nghiêm trọng | Ví dụ 02.4 Bước 4 (496–501) | Bỏ bước trung gian ($\ln40$, $\ln2000$ không ghi), dồn hai phép tính mỗi dòng, $\epsilon$ đổi $0{,}1\to0{,}05$ không báo (§7a) | "$\lceil\ln40/0{,}005\rceil=\lceil737{,}8\rceil=738$" | Báo $\epsilon=0{,}05$; ghi $\ln40\approx3{,}6889$, chia, làm tròn; tách dòng |
| trung bình | toàn bài | Thiếu tiếng Anh ở lần đầu cho thuật ngữ mang từ Bài 01 | lớp giả thuyết, giả thuyết, hàm lỗi, độc lập cùng phân bố, rủi ro Bayes, quy tắc chọn khi bằng nhau, phân bố biên, hầu chắc chắn, cận dưới đúng, xác suất hậu nghiệm, hàm lỗi bình phương, hàm lỗi log, nửa không gian | Thêm tiếng Anh ở lần đầu |
| trung bình | dòng 25; 949, 968 | PAC, UML không có dạng đầy đủ | "học PAC"; "UML Phụ lục B.5" | Viết đầy đủ lần đầu như Bài 01 |
| trung bình | tiêu đề; Hệ quả 02.16(c), Mệnh đề 02.17(c) | "độ phức tạp mẫu" chỉ ở tiêu đề; không nối $M$ với $m_{\mathcal H}$ | — | Một câu: $m_{\mathcal H}(\epsilon,\delta)\le M(\epsilon,\delta)$ |
| trung bình | Mục tiêu 4 | Câu 72 tiếng gộp hai mục tiêu | — | Tách thành hai mục tiêu |
| trung bình | §1 (43–52) | Câu mở là lời dẫn về danh sách, tự mâu thuẫn ("chỉ ghi điểm mới" nhưng đủ tám mục); mục 4–6 mở bằng động từ (§3a) | — | "Bài toán giữ tám thành phần của §1 Bài 01, với các lựa chọn sau."; mở các mục song song |
| trung bình | Ví dụ 02.3 | "$m=6,100,200$" nhập nhằng với dấu phẩy thập phân | — | "$m=6$, $100$ và $200$" |
| trung bình | Ví dụ 02.12 Bước 4 | Ba phép tính dồn một câu (§7a) | — | Ba gạch đầu dòng |
| trung bình | Ví dụ 02.12 Bước 5 | Đoạn 5 câu dày; câu 3 mơ hồ; "giá" ngược nghĩa | "số nhỏ hơn của nó là giá của một bảo đảm khác" | Tách đoạn; viết lại |
| trung bình | Ví dụ 02.11 Bước 2 | Không nói $10\ln20$ đến từ đâu | — | "$\ln(1/\delta)/\epsilon=\ln20/0{,}1$, $\ln20\approx2{,}9957$" |
| trung bình | §8 câu mở | Câu không chủ ngữ, "loại" mơ hồ (§9a) | "chỉ cần loại các giả thuyết …" | Viết lại thành chặn xác suất một giả thuyết xấu khớp mẫu |
| trung bình | Nhận xét 02.11 | Câu then chốt hai cách đọc; đoạn 5 câu | "không cận nào … tiến về $0$" | "…mà tiến về $0$…"; tách đoạn |
| trung bình | §9 đoạn 5 | Định dạng thuật ngữ sai; câu 56 tiếng; "điểm" lệch "tỉ lệ lỗi" | "(dùng lại thích nghi, adaptive reuse)" | "*dùng lại thích nghi* (adaptive reuse)"; "tỉ lệ lỗi"; tách câu |
| trung bình | Ví dụ 02.8 Bước 3 | Bỏ bước $\ln200\,000$; bán kính hai phía là phần đệm | — | Bỏ bán kính hai phía hoặc ghi đủ |
| nhẹ | Mở bài | Đoạn 5 câu, câu dài, "phản ánh đúng" mơ hồ | — | Tách câu hỏi trung tâm |
| nhẹ | 3, 75, 270, 640 | Chủ thể trừu tượng (§9a) | "Định nghĩa 01.25 lại đòi …" | Viết lại |
| nhẹ | 340, 534 | Văn bản làm chủ ngữ | "Phụ lục A chứng minh …"; "Ví dụ sau bỏ …" | Viết lại |
| nhẹ | 681, 720, 877, 1003 | Hai chữ "cho" trong một câu | "Bổ đề 02.12 cho $K$ biến cố $B_h$ cho" | "Áp dụng Bổ đề 02.12 …, ta được" |
| nhẹ | Nhận xét 02.8 | Câu lồng mệnh đề (§9a) | — | Viết lại |
| nhẹ | Ví dụ 02.6 | Câu chốt kiểu cách ngôn, từ nhấn "thật sự" | "Tính không chệch còn, tính tập trung mất." | Câu thường |
| nhẹ | Ví dụ 02.6 tiêu đề | "hồ sơ" không có trong thuật ngữ; nên dùng "quan sát" | — | "(Một quan sát chép lại $m$ lần)" |
| nhẹ | 569, 573 | Chuyển tiếp lặp cuối §5 và đầu §6 | — | Giữ một lần |
| nhẹ | sau Định nghĩa 02.4 | Đoạn 5 câu; "Phản ví dụ" không nói phản điều gì | — | Tách đoạn; nói rõ |
| nhẹ | 345 | Câu thiếu động từ chính | "Kiểm tra bằng số …: …" | Viết lại |
| nhẹ | Nhận xét 02.18; §9 | Giới hạn nói hai lần; "nối hai chế độ" mơ hồ | — | Giữ một nơi |
| nhẹ | §9 đoạn 3–4 | Lặp số đã có | — | Rút gọn |
| nhẹ | Hệ quả 02.10; Bổ đề 02.2 | Câu sai ngữ pháp; "mọi phân bố không âm" | "Các bảo đảm là với xác suất cao…" | Sửa câu; "mọi biến ngẫu nhiên không âm" |
| nhẹ | Ví dụ 02.4 | $\alpha$ và $\epsilon$ cho cùng mức lệch trong một bảng | — | Ghi một lần |
| nhẹ | Ví dụ 02.9 Bước 2 | Công thức hiển thị không câu dẫn | — | Thêm câu dẫn |
| nhẹ | 803, 812, 898, 879 | $A_{\min}$, $A_{\max}$, $h^\star$ không nhắc lại | — | Nhắc trong ngoặc |
| nhẹ | dòng 26; Định nghĩa 02.13 | $\Pr(k)$, $L_s$ chưa gọi tên | — | Gọi tên |
| nhẹ | 632 | "Biến cố cần chặn" không chính xác | — | "Biến cố cần có xác suất cao" |
| nhẹ | Mục tiêu 5; §10 Bài tập 02.4 | "bỏ số ứng viên" mơ hồ | — | "hệ số $K$" |
| nhẹ | Khối ứng dụng | Nhãn không song song | "**Phép chọn là ERM.**" | "**Phép chọn.**" |
| nhẹ | Nhận xét 02.15 | Đoạn 5 câu; "phía đối lập" mơ hồ; §6 kết bằng chi tiết đo được | — | "Trái với Hệ quả 01.29 …"; đổi thứ tự |
| nhẹ | Ví dụ 02.10 Kết luận | Lặp câu dẫn | — | Kết bằng con số hoặc bỏ |
| nhẹ | dòng 25; 1011 | Câu 111 tiếng; đoạn 7 câu là liệt kê | — | Chuyển thành danh sách |
| nhẹ | 27, 68 | $\ln$ định nghĩa hai lần | — | Giữ ở bảng §2 |

**Danh sách §14 (người rà):** 1 ✗ (§1 mở bằng lời dẫn); 2 ✓; 3 ✗ (câu dẫn Ví dụ 02.9, kí hiệu chưa gọi tên); 4 ✓; 5 ✓; 6 ✗ (thiếu tiếng Anh, PAC/UML, định dạng); 7 ✓; 8 ✗ (§7a ở Ví dụ 02.4 B4, 02.12 B4–B5, 02.11 B2, 02.8 B3); 9 ✓; 10 ✗ (chuyển §5→§6 lặp, §6 kết bằng chi tiết đo được, §9 lặp); 11 ✗ (6–8 câu > 40 tiếng, 8 đoạn > 4 câu); 12 ✓ (trừ "$m=6,100,200$").

**Kết luận của người rà:** giọng văn khớp Bài 01; hai lỗi nghiêm trọng (danh mục sớm ở Ví dụ 02.1; §7a ở Ví dụ 02.4 Bước 4); yêu cầu sửa.
