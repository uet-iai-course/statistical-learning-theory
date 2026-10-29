# Rà lại sau tái cấu trúc — toán học (2026-10-30)

Không có lỗi chặn bàn giao, nghiêm trọng hay trung bình. Mọi định nghĩa và phát biểu đúng với thuật toán tất định (thứ tự lượng từ $\exists A\,\exists M\,\forall\epsilon,\delta\,\forall D\,\forall m\ge M$, $\Pr_{S\sim D^m}$; "mọi thuật toán ERM" lượng từ trên quy tắc chọn tất định, đo được; Hệ quả 01.29 đúng). 209 dẫn chiếu tới khối đánh số (157 ghi chú, 51 bài tập, 1 dạng "và 01.25") đều đúng loại và đúng nội dung; tập dẫn chiếu trong bài tập khớp bản cũ qua bảng ánh xạ; 0 sai. Mọi con số trong đoạn chuyển chỗ và đoạn mới đúng (liệt kê $m\le4$ cho Ví dụ 01.9, C.2, Nhận xét 01.21). Không còn `\xi`, "0,273", "chọn đều", "nguồn ngẫu nhiên nội tại".

| mức độ | vị trí | vấn đề | đề xuất sửa |
|---|---|---|---|
| nhẹ | Ví dụ 01.4 đoạn 2 (dòng 233) | Chuyển sang $S_f$ (cỡ 4) mà không nói cỡ mẫu. | "(cỡ $m=4$)". |
| nhẹ | Sau Định nghĩa 01.4 (dòng 216) | Điều kiện đo được còn làm $L_S(A(S))$ đo được (Nhận xét 01.9, Định nghĩa 01.10, 01.28 dùng). | "…để $L_D(A(S))$ và $L_S(A(S))$ là biến ngẫu nhiên…". |
| nhẹ | Định nghĩa 01.5 (dòng 220–228) | Điều kiện rủi ro hữu hạn khi $\ell$ không bị chặn nằm ở đoạn đọc, không trong định nghĩa ($\infty-\infty$). | Đưa vào định nghĩa: "…$D$ (có rủi ro hữu hạn trên $\mathcal H$, Định nghĩa 01.3, khi $\ell$ không bị chặn)…". |
| nhẹ | Dòng 476 | Câu thuật toán ngẫu nhiên nói về loại Định nghĩa 01.4 không bao gồm. | "Khi Bài 05 mở rộng Định nghĩa 01.4 cho thuật toán dùng nguồn ngẫu nhiên riêng, như SGD, xác suất được lấy theo cả mẫu và nguồn đó." |
| nhẹ | `reorder-plan.md` §2 dòng §8 | Kế hoạch ghi bỏ (O1)/(T3)/(T4) ở Hệ quả 01.29; ghi chú vẫn giữ (T1), (O1) kèm lời (đúng). | Sửa câu trong kế hoạch. |
| nhẹ (có từ trước) | exercises.md dòng 49 (01.1(a), dòng $A$) | "ERM dưới $\ell_c$ trên $\mathcal H$" mới là quy tắc. | "với một quy tắc chọn khi bằng nhau cố định". |
| nhẹ (có từ trước) | Phụ lục A mở đầu (dòng 725) | "theo thứ tự chúng xuất hiện trong bài" không đúng (A(iv) dẫn trước A(iii)). | Bỏ cụm hoặc đổi chỗ (iii), (iv). |
