# Rà soát 1 — học viên cao học (Bài 02, bản đóng băng 2026-10-30)

Người rà độc lập, chỉ đọc (general-purpose, opus, high). Đã đọc hết ghi chú theo thứ tự và tra lại các khối Bài 01 được dẫn. Không có phát hiện chặn bàn giao.

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | Ví dụ 02.12, bảng (dòng 935) và Bước 5 (dòng 941) | Hàng $K=1$ ở cột "rủi ro vượt mức" và "khả thực" gây hiểu sai: với một ứng viên, ERM trả về chính nó, rủi ro vượt mức bằng 0; lớp một phần tử khả thực thì rủi ro bằng 0; bảng ghi 2952/738 và 60/30; Bước 5 nói "gấp khoảng 4 lần cột ước lượng cùng hàng" kể cả hàng $K=1$ | "\| $1$ \| $738$ / $185$ \| $2952$ / $738$ \| $60$ / $30$ \|" | Ghi "—" (bảo đảm tầm thường) ở hai ô $K=1$, kèm một câu; hoặc thay bằng $K=10$ |
| trung bình | §1 mục 8, bảng §1 | $\epsilon$ dùng trước khi nói nghĩa; ba vai chỉ được nói ở Ví dụ 02.12 | "tập $\{h\in\mathcal H:L_D(h)>\epsilon\}$" | Dòng trong bảng kí hiệu §2 nêu ba vai của $\epsilon$, hoặc bỏ $\epsilon$ khỏi §1 |
| trung bình | Định nghĩa 02.1, Bổ đề 02.2, 02.5(a), Ví dụ 02.3 so với 02.4 | $\alpha$ đổi vai (độ lệch / ngưỡng / số thực); cùng "độ lệch 0,1" lúc là $\alpha$ lúc là $\epsilon$ | "$m\ge1/(4\delta\alpha^2)$" và "$m\ge1/(4\delta\epsilon^2)$" | Một kí hiệu cho ngưỡng trong Markov/Chernoff, $\epsilon$ cho độ lệch; hoặc một câu nói rõ |
| trung bình | Ví dụ 02.11 Bước 2 | Không nhắc công thức $\lceil\ln(1/\delta)/\epsilon\rceil$; không nói rõ lớp hàm ngưỡng với $A_{\max}$ | "$m\ge\lceil10\ln20\rceil$ … đủ cho mọi phân bố khả thực" | Viết công thức, thay số; so với 48 chỉ khác hạng $\ln K/\epsilon$ |
| trung bình | Mệnh đề 02.17(c) | Loại bảo đảm không rõ (từng thuật toán hay đồng thời mọi nghiệm ERM); $\hat h$ chưa định nghĩa trong khối | "với mọi thuật toán ERM, $\Pr(L_D(\hat h)\le\epsilon)\ge1-Ke^{-\epsilon m}$" | Viết song song Hệ quả 02.16(a): "với xác suất ít nhất …, mọi nghiệm ERM $\hat h$ trên $S$ có …" |
| trung bình | Chứng minh Hệ quả 02.16 Bước 1; Ví dụ 02.1; chứng minh Mệnh đề 02.17 Bước 3 | $h^\star$ đổi nghĩa (rủi ro 0 ở Định nghĩa 01.16; phần tử tốt nhất trong lớp ở §7) | "tồn tại $h^\star\in\arg\min$" và "khả thực với $h^\star=h_3$" | Kí hiệu khác ở §7 (vd. $h_{\mathcal H}$) hoặc một câu nói rõ |
| trung bình | Nhận xét 02.11 đoạn 2 | Lượng từ kết luận không rõ; dễ hiểu thành "trung bình không hội tụ" | "không cận nào chỉ phụ thuộc $m$ và $\epsilon$ tiến về $0$" | "…đúng cho mọi phân bố không âm có kì vọng 1…; với từng phân bố cố định luật số lớn vẫn đúng" |
| trung bình | Chứng minh Định lý 02.7 Bước 1 | Dòng đầu gộp Chernoff (a), (b) và đổi tham số $\tau/m$ | "$\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\le e^{-\tau\epsilon}\prod_i\mathbb Ee^{(\tau/m)(V_i-\mu_i)}$" | Thêm dòng $\le e^{-\tau\epsilon}\mathbb Ee^{\tau(\bar V_m-\bar\mu_m)}$; nói rõ áp dụng 02.5(b) cho $(V_i-\mu_i)/m$ |
| trung bình | Ví dụ 02.8 Bước 1 | Lập luận lấy điều kiện rồi lấy kì vọng bị nén; không nói vì sao $S$ vẫn có phân bố $D^m$ | "đúng với mọi giá trị của dữ liệu huấn luyện, nên lấy kì vọng …" | Tách 2–3 câu: $T$ dữ liệu huấn luyện, $E$ biến cố tốt, $\Pr(E)=\mathbb E[\Pr(E\mid T)]\ge1-\delta$; $S$ độc lập với $T$ |
| trung bình | Ví dụ 02.12 Bước 5; mục tiêu 4 | Ba nghĩa của $\epsilon$ được nói sau bảng | Thiết lập rồi Bước 5 | Đưa câu "chỉ so được trong cùng một cột" lên trước bảng |
| nhẹ | Hệ quả 02.10; Định lý 02.14 | $r$ ba vai; "bán kính" dùng trước khi đặt tên "bán kính tin cậy" | "Bán kính của khoảng tin cậy giảm như $1/\sqrt m$" | Đặt tên ở Hệ quả 02.10; nói $r_m$, $r_m^{+}$ trở về $r$, $r^{+}$ khi $K=1$ |
| nhẹ | Ví dụ 02.7; chứng minh Bổ đề 02.12 | $h_k$ đụng $h_t$ và $k\sim\mathrm{Bin}$; biến cố $A$ đụng thuật toán $A$ | "$h_k(x)=x_k$"; "hai biến cố $A$, $B$" | $g_k$; $E$, $F$ |
| nhẹ | Ví dụ 02.6 Bước 3–4 | Độ lệch đổi từ 0,1 sang 0,2 không lý do | "tại $0{,}2$" | Giữ 0,1 hoặc giải thích |
| nhẹ | Nhận xét 02.11 | Bất đẳng thức Bernoulli không có trong tiên quyết; "bằng 0,9900" mơ hồ | "Theo bất đẳng thức Bernoulli…" | Thêm vào tiên quyết; phân biệt cận dưới 0,99 và giá trị 0,9900 |
| nhẹ | §5 sau (T3) | "mọi cỡ mẫu dưới đây nhân thêm $(b-a)^2$" nói quá (khả thực chỉ 0–1; bán kính nhân $b-a$) | — | "cỡ mẫu §5–§7 nhân $(b-a)^2$, bán kính nhân $(b-a)$" |
| nhẹ | §9 đoạn 2 | $K/(4\delta\epsilon^2)$ không kèm bước suy ra | — | "mỗi giả thuyết cần xác suất thất bại $\delta/K$…" |
| nhẹ | §10, Bài tập 02.6, 02.9 | 02.6 cần bất đẳng thức hợp đếm được; 02.9 cần AM–GM, không có trong tiên quyết | — | Một câu sau Bổ đề 02.12 về họ đếm được; AM–GM vào gợi ý |
| nhẹ | Nhận xét 02.15 đoạn 2 | Đoạn đo được nặng, không đánh dấu đọc thêm | — | Chuyển xuống Phụ lục hoặc đánh dấu |
| nhẹ | Ví dụ 02.8 Bước 2–3, 5 | $r_m$ hai phía tính nhưng không dùng; ý 5,93 > 1 làm phân tán | — | Rút gọn |
| nhẹ | §9 đoạn 3–4 | Lặp kết luận của Ví dụ 02.4, 02.11, Nhận xét 02.11 | — | Rút còn một câu chỉ dẫn hoặc thêm ý mới |
| nhẹ | §1 mục 7, mục 4 | $\mathcal M_{\mathcal X}$, $\ell_c$ trước bảng kí hiệu | — | "(lớp mọi hàm phân lớp đo được, Ví dụ 01.8)" |

**Tóm lại (người rà):** dễ đọc khá tốt; phần khó nhất là Bước 1 chứng minh Định lý 02.7 và lập luận lấy điều kiện ở Ví dụ 02.8; câu hỏi mở đầu giải được sau khi đọc (8,9% và khoảng 12%, đúng chỗ hứa); câu hỏi cuối buổi ra 0,126; bài tập làm được trừ 02.6 và 02.9.
