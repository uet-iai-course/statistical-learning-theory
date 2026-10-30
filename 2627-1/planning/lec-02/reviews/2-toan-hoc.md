# Rà soát 2 — chính xác toán học (Bài 02, bản đóng băng 2026-10-30)

Người rà độc lập, chỉ đọc (general-purpose, opus, high). Tự chứng minh lại mọi phát biểu 02.2–02.18 và Phụ lục A; tính lại khoảng 120 con số bằng Python (tổng nhị thức bằng phân số chính xác). Không có lỗi chặn bàn giao hay nghiêm trọng.

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | Ví dụ 02.11 Bước 4, 5, Kết luận; §9 đoạn 3 | $30$ là cận cho riêng $A_{\max}$, $48$ cho mọi ERM; so sánh như cùng loại; khoảng cách có hai nguồn. Với mọi ERM trên lớp hàm ngưỡng: $\lceil\ln(2/\delta)/\epsilon\rceil=37$; $48\to37$ do bất đẳng thức hợp cộng 6 biến cố lồng nhau thay vì 2; $37\to30$ do $A_{\max}$ chỉ lệch một phía | Bài tập 01.9(c), §9 Bài 01 "áp dụng … với $A_{\max}$" | Ghi rõ phạm vi; tách hai nguồn hoặc so $48$ với $37$; sửa §9 |
| nhẹ | sau (T3) | "mọi cỡ mẫu … nhân $(b-a)^2$" quá rộng | Mệnh đề 02.17 chỉ 0–1 | Chỉ cỡ mẫu dựa trên Hoeffding; bán kính nhân $b-a$ |
| nhẹ | Nhận xét 02.11 | Lập luận chỉ phủ $\epsilon\le1$ | độ lệch trên biến cố bằng 1 | "với mỗi $\epsilon\in(0,1]$" hoặc co giãn; "$\ge0{,}99$" thay "bằng $0{,}9900$" |
| nhẹ | Nhận xét 02.18 câu 1 | "một giả thuyết … khớp mẫu, xác suất $(1-\epsilon)^m$" đọc được như "tồn tại" (cận đúng $K(1-\epsilon)^m$) | Mệnh đề 02.17(a), (b) | "với mỗi giả thuyết cố định …" |
| nhẹ | Nhận xét 02.15 đoạn 2 | "quy tắc chọn cố định" chưa đủ: cần thứ tự ưu tiên cố định trên $\mathcal H$ cho tính đo được | — | "theo một thứ tự ưu tiên cố định trên $\mathcal H$ (như $A_{\min}$, $A_{\max}$)" |
| nhẹ | Ví dụ 02.12 hàng $K=1$ | Với $K=1$ rủi ro vượt mức bằng 0 (và rủi ro 0 khi khả thực) với mọi $m\ge1$ | — | Một câu: chỉ là giá trị công thức |
| nhẹ | Ví dụ 02.4 Bước 4 | "cần $m\ge$" là điều kiện đủ | Hệ quả 02.10(d) dạng "nếu … thì" | "đủ khi $m\ge$" |
| nhẹ | Ví dụ 02.7 Bước 2 | Cần $mK$ tọa độ độc lập đồng thời (T1 và cách dựng) | — | Thêm một mệnh đề |
| nhẹ | Ví dụ 02.8 Bước 5 | "độ lệch $0{,}02$" không chính xác (trung vị của $\min_kL_S$ khoảng $0{,}045$) | $\Pr(\min\le0{,}045)\approx0{,}48$ | Vì $L_S\ge0$, $L_D-L_S\le0{,}07<0{,}0704$ chắc chắn, biến cố của Định lý 02.14(b) xảy ra với xác suất 1 |
| nhẹ | Bổ đề 02.6 Bước 1–2 | Chỗ dùng thiết yếu của tính bị chặn là Bước 2 (dây cung) | — | Đánh dấu ở Bước 2 |

**Đã kiểm đúng:** Markov, Chebyshev, Chernoff (Tonelli), bổ đề Hoeffding và Phụ lục A ($c_u$, $\theta\in\{0,1\}$), Định lý 02.7 (a)(b)(c), Nhận xét 02.8, Hệ quả 02.10, Định lý 02.14, lập luận lấy điều kiện, Nhận xét 02.15 khớp Định nghĩa 01.28, Hệ quả 02.16 khớp Định nghĩa 01.25 ("với mọi $m\ge M$"), Mệnh đề 02.17 khớp Định nghĩa 01.16, 01.18; mọi tham chiếu 01.x. Con số: $0{,}5391$; $0{,}6189$; $0{,}02115$; $8{,}94\cdot10^{-4}$; $0{,}0109$, $4{,}9\cdot10^{-4}$ (biến cố ngặt); Markov và đuôi trên; Chebyshev; $500$; $1{,}1059<1{,}1331$; Hoeffding $1{,}774$, $0{,}2707$, $0{,}0366$; $2000/738$, $100\,000/1521$; Ví dụ 02.5, 02.6, 02.7 ($0{,}005930$, $0{,}9974$, $5{,}93$), 02.8, 02.9 ($r_6=0{,}676$), 02.10, 02.11, cả 18 ô của Ví dụ 02.12 và phép nhân $K$ lên 10; $2\,000\,000$; câu hỏi cuối buổi $0{,}126$. Tất cả khớp.

**Kết luận của người rà:** mọi phát biểu và chứng minh đúng; mọi con số khớp; sửa so sánh 48/30 trước khi bàn giao.
