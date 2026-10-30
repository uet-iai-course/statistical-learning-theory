# Rà lại 6 — toán học trên phần đã sửa (Bài 02, sau biên tập vòng 1, 2026-10-30)

Người rà độc lập, chỉ đọc (general-purpose, opus, high). Diff `lec02-round1.diff` khớp bản hiện tại; mọi con số mới tính lại (tổng nhị thức bằng phân số chính xác). `forward_refs.py`: 0. Không có lỗi chặn bàn giao hay nghiêm trọng; cả 10 phát hiện của `2-toan-hoc.md` đã xử lý.

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | câu kết §5 | "Bỏ … tính bị chặn (Nhận xét 02.11), cận của Định lý 02.7 không còn đúng" sai: với miền $[0,M]$ cận Hoeffding vẫn đúng; điều mất là cận chỉ phụ thuộc $m$, $\epsilon$ | Nhận xét 02.11: "không có mâu thuẫn" | "Bỏ tính độc lập, cận của Định lý 02.7 sai. Bỏ tính bị chặn, không còn cận đuôi nào chỉ phụ thuộc $m$ và $\epsilon$ đúng cho mọi phân bố." |
| nhẹ | Ví dụ 02.11 Bước 2 | Thiếu: vì sao "ngưỡng xấu khớp mẫu" là biến cố thất bại của mọi nghiệm ERM ($L_S=0$ hầu chắc chắn); $t_L$ có thể không tồn tại | cận chính xác $2\cdot0{,}9^{37}-0{,}8^{37}=0{,}0403$ | Dẫn Bước 3 chứng minh Mệnh đề 02.17; "(nếu có ngưỡng xấu bên trái)" |
| nhẹ | chứng minh Mệnh đề 02.17 Bước 3 | Viết cho một $\hat h$, chưa khớp (c) dạng đồng thời | — | "biến cố 'có một nghiệm ERM $\hat h$ với $L_D(\hat h)>\epsilon$' nằm trong …" |
| nhẹ | đoạn sau Định lý 02.14 | Dẫn Định nghĩa 02.9 như áp dụng thẳng; cần quy tắc chọn đo được | — | "theo nghĩa mở rộng của Định nghĩa 02.9 cho giả thuyết chọn theo mẫu; quy tắc đo được" |
| nhẹ | Phụ lục C | Thiếu bước nối tới điều kiện đo được đồng thời của Định nghĩa 01.4 | Bài 01 Phụ lục A(iv) | $\ell(A_m(s),z)=\sum_h\mathbb 1[A_m(s)=h]\ell(h,z)$ |
| nhẹ | câu sau Nhận xét 02.18 | "Mọi cỡ mẫu của §6–§8 tăng theo $\ln K$" quá rộng ($37$, $30$, $14$) | — | "Các cỡ mẫu tổng quát (Định lý 02.14, Hệ quả 02.16, Mệnh đề 02.17) …" |
| nhẹ | Nhận xét 02.18 (Bernstein) | "gần $1/\epsilon$ khi phương sai nhỏ" mơ hồ | dạng Bernstein $(2\sigma^2/\epsilon^2+2(b-a)/(3\epsilon))\ln(\cdot)$ | "khi phương sai cỡ $\epsilon$ hoặc nhỏ hơn" |

**Đã kiểm đúng:** Ví dụ 02.11 ($48$, $37$, $30$, $14$, phạm vi); Mệnh đề 02.17(c) đồng thời và dòng Thuật toán; $m_{\mathcal H}\le M$ khớp Định nghĩa 01.20; $h_{\mathcal H}$; Nhận xét 02.11 ($\epsilon\in(0,1]$, $0{,}990049$); dòng trung gian Định lý 02.7; lấy điều kiện theo $T$; Ví dụ 02.8 Bước 5; Ví dụ 02.4 (giao nhau đúng khi $18\le m\le107$; $185$, $381$, $500$, $25\,000$); câu $(b-a)^2$; họ đếm được (liên tục từ dưới); hàng $K=1$; §9; các phần bị cắt không làm mất nội dung toán.
