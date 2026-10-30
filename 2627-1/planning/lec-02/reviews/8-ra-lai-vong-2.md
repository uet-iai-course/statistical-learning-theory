# Rà lại 8 — toán, mạch, văn phong trên phần sửa vòng 2 (Bài 02, 2026-10-30)

Người rà độc lập, chỉ đọc (general-purpose, opus, high), `no-ai-slop` Detect. `forward_refs.py` 0; thân bài 11 994, phụ lục 603. Mọi phát hiện của rà soát 6 và 7 đã xử lý (✓). Số tính lại đúng ($m=107$: $0{,}23364<0{,}23531$; $m=108$: $0{,}23148>0{,}23065$; $37$, $30$, $48$, $14$; $0{,}0704$; $1097$; $1431$). Các phần bị cắt không làm mất nội dung còn cần. Kết luận: **giao được**; nên sửa một dòng trung bình.

| mức độ | vị trí | vấn đề | đề xuất sửa |
|---|---|---|---|
| trung bình | câu kết §5 | Nghĩa đen sai: cận hằng $1$ chỉ phụ thuộc $m$, $\epsilon$ và đúng cho mọi phân bố; Nhận xét 02.11 chỉ chứng minh không có cận tiến về $0$ | "…không còn cận đuôi nào chỉ phụ thuộc $m$, $\epsilon$, tiến về $0$ khi $m\to\infty$ và đúng cho mọi phân bố" |
| nhẹ | Ví dụ 02.11 Bước 2 | "khi và chỉ khi" nhưng nguồn dẫn chỉ cho một chiều | "chỉ khi" |
| nhẹ | Ví dụ 02.10 Kết luận | "so với … so với"; hiệu hai cận đủ viết như nhu cầu thật | "cỡ mẫu đủ … là $1431$, hơn $1097$ … là $334$" |
| nhẹ | Ví dụ 02.9 Kết luận | "đúng" → "đủ" | |
| nhẹ | Ví dụ 02.4 Kết luận | Danh từ hóa, lặp "lợi thế"; mất so sánh với Chebyshev | "Cỡ mẫu đủ theo Hoeffding tăng như $\ln(1/\delta)$, theo Chebyshev như $1/\delta$; ở §6 …" |
| nhẹ | Ví dụ 02.12 Bước 5 | "hàng … là một giả thuyết" | "ứng với một giả thuyết cố định (Hệ quả 02.10(d))" |
| nhẹ | câu mở §6 | "thấp hơn hẳn" mơ hồ | "thấp hơn rủi ro kì vọng một khoảng cho trước" |
| nhẹ | Nhận xét 02.15 | Thiếu "gồm" | "lớp $\mathcal M_{\mathcal X}$ gồm mọi …" |
| nhẹ | bảng §2 dòng $\epsilon$ | "chỗ … chỗ" | "ở các mục khác, nghĩa được nêu khi dùng" |
| nhẹ | sau $\square$ Bổ đề 02.2 | Mất câu nối với việc học | "…; với $V=L_S(h)$, cận không giảm khi $m$ tăng." |
| nhẹ | câu sau Định lý 02.14; Phụ lục C | Phụ lục C chỉ xét thứ tự ưu tiên | Thêm vào Phụ lục C câu cho quy tắc tổng quát với $\{s:\hat h(s)=h\}$ đo được |
| nhẹ | §10 Bài tập 02.8 | "mục tiêu 4, 5" phụ thuộc tệp bài tập | Ghi vào brief người viết bài tập |
| nhẹ | sau Mệnh đề 02.17 | "Ở đây" mơ hồ | "Trong Mệnh đề 02.17, …" |
