# Rà soát 3 — chuyên gia lý thuyết học và trung thành nguồn (Bài 02, bản đóng băng 2026-10-30)

Người rà độc lập, chỉ đọc (general-purpose, opus, high). UML đã đọc (trang PDF): 37–42, 50–52, 54–59, 422–428; không mở bản lời giải. Đã đọc blueprint §A, Bài 2–3, §D, §E; `review-log.md`, `source-analysis.md`, `ky-hieu.md`; các khối tương ứng của Bài 01.

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | Ví dụ 02.11 Bước 2, 4, 5, Kết luận; §9 đoạn 3 | Lẫn bảo đảm cho mọi thuật toán ERM ($48$) với bảo đảm riêng cho $A_{\max}$ ($30$, Bài 01 §9 nói rõ "với $A_{\max}$"); "khoảng cách đến từ bất đẳng thức hợp" chỉ đúng một phần. Với mọi quy tắc chọn trên lớp hàm ngưỡng, hai chuỗi biến cố lồng nhau cho $\lceil\ln(2/\delta)/\epsilon\rceil=37$ | "Cỡ $30$ … vẫn đúng cho mọi phân bố khả thực"; "Khoảng cách này đến từ bất đẳng thức hợp" | Nói rõ phạm vi của $48$, $30$, $14$; tách hai nguồn của khoảng cách; có thể thêm $37$ cho mọi nghiệm ERM; sửa §9 |
| trung bình | sau (T3) (dòng 410) | Hệ số $(b-a)^2$ chỉ cho cỡ mẫu dựng từ Hoeffding | "mọi cỡ mẫu dưới đây nhân thêm $(b-a)^2$" | Giới hạn ở §5–§7; Mệnh đề 02.17 chỉ 0–1 |
| trung bình | §9 đoạn 2; Ví dụ 02.12 Kết luận | "Chi phí $\ln K$" nêu không kèm điều kiện; đây là cỡ mẫu đủ trong một cận trên | "Chi phí thống kê … là $\ln K$" | "Theo các cận của bài, với lớp cố định trước mẫu và hàm lỗi bị chặn, cỡ mẫu đủ chỉ tăng …" |
| trung bình | "Quan hệ với giáo trình UML" | Mô tả sai nguồn: UML cũng phát biểu cho mọi nghiệm ERM (Hệ quả 2.3, tr. 41; Bổ đề 4.2, tr. 54) | "Các bảo đảm cho ERM đúng với mọi quy tắc chọn khi bằng nhau …" | Chỉ giữ ERM xấp xỉ; thêm khác biệt thật (Chernoff tổng quát; chứng minh $\varphi\le u^2/8$; Chebyshev không cùng phân bố) |
| trung bình | Định nghĩa 02.9; Ví dụ 02.8; câu hỏi cuối buổi | Định nghĩa chỉ cho $h$ cố định, câu hỏi cuối buổi hỏi cận tin cậy cho $L_D(\hat h)$ | "Tính một cận trên tin cậy $95\%$ cho rủi ro kì vọng của nó" | Một câu sau Định lý 02.14: $L_S(\hat h)+r_m^{+}$ thỏa $\Pr_S[L_D(\hat h)\le\cdot]\ge1-\delta$ với mọi $D$ |
| nhẹ | cuối §4 (dòng 266) | "cần dùng mọi mô-men" là điều kiện cần quá mức | — | "Phương pháp Chernoff đạt được điều đó bằng hàm sinh mô-men" |
| nhẹ | Bổ đề 02.6 Bước 3; Phụ lục A | Phép đổi biến trùng kí hiệu với UML B.7 (chứng minh kinh điển, không phải dịch; ghi chú tự chứng minh $\varphi''\le\tfrac14$) | — | Chấp nhận được; có thể ghi $\rho(1-\rho)$ là phương sai Bernoulli |
| nhẹ | Phụ lục B của ghi chú | Trùng tên "UML Phụ lục B.1" ở §12 | — | Đổi tên hoặc ghi "của bài này" |
| nhẹ | Mệnh đề 02.17 Giả thiết | Thiếu thành phần "Thuật toán" | — | "**Thuật toán.** (O1), mọi quy tắc chọn; chỉ phần (c) dùng" |
| nhẹ | §2 (dòng 78) | "(O1), (O2) chỉ dùng ở §7" sai | — | "(O1) dùng ở §6–§8; (O2) chỉ ở §7" |
| nhẹ | Ví dụ 02.12 hàng $K=1$ cột khả thực | Với $K=1$ khả thực thì mọi cỡ mẫu đủ | — | Một câu hoặc "—" |
| nhẹ | Nhận xét 02.11 | Lượng từ chưa rõ | — | "không có hàm $g(m,\epsilon)\to0$ chặn … đồng thời cho mọi phân bố không âm có kì vọng 1 ($\epsilon\le1$)" |
| nhẹ | chứng minh Định lý 02.14 câu kết; §9 đoạn 1 | "mọi quy tắc dựa trên $L_S$" hẹp hơn thực tế | — | "mọi giả thuyết trong $\mathcal H$ chọn theo $S$ bằng bất kì quy tắc nào" |
| nhẹ | §9 đoạn 5 | "Có hai cách sửa" nghe như đủ; họ đếm được phải chứa mọi ứng viên có thể lập | — | "Hai cách sửa đơn giản"; thêm điều kiện |
| nhẹ | Nhận xét 02.18; §9 cuối | Hứa cận dưới ở Bài 03; blueprint chỉ phát biểu | blueprint dòng 236–237 | "Bài 03 phát biểu (không chứng minh)" |
| nhẹ | Mục tiêu 4 | Dễ đọc như điều kiện cần | — | "cỡ mẫu đủ" |

**§E:** ✓ trừ một mục ✗ (bảo đảm cho lớp/thuật toán ở Ví dụ 02.11 và §9). Số bài UML đối chiếu PDF: 2.3 (tr. 41–42), 3.4 (51), 3.5 (51–52), 4.1 (58–59), 4.2 (59).

**Kết luận của người rà:** Định lý 02.7, 02.14, Hệ quả 02.16, Mệnh đề 02.17 đúng, lượng từ chính xác; lập luận lấy điều kiện ở Ví dụ 02.8 đúng; không có đoạn dịch hay diễn ý sát UML; mục UML dẫn đúng. Chưa đạt bàn giao do một phát hiện nghiêm trọng.
