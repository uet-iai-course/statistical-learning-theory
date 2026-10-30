# Rà bài tập — chính xác toán học (Bài 02, bản đóng băng 2026-10-30)

Người rà độc lập, chỉ đọc (general-purpose, opus, high). Tự giải từng bài trước; tính lại mọi con số; đối chiếu số và nội dung bài UML trên PDF (2.3 tr. 41–42; 3.4, 3.5 tr. 51; 4.1, 4.2 tr. 58–59). Không có lỗi chặn bàn giao.

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | 02.1(d) Bước 3, (e) Bước 3, Gợi ý 3 | So sánh tại $\tau=1$ cho tổng nhỏ hơn tích, đúng chiều chứng minh đuôi trên cần; chỉ đẳng thức của Bổ đề 02.5(b) hỏng, còn "$\le$" đúng khi $\tau>0$. Đuôi dưới ($\tau<0$) mới hỏng | $(1+x)^3/8-(1+3x^2)/4=(x-1)^3/8$; $\tau=-1$: $0{,}3515>0{,}3199$; $m=3$: $\Pr(\bar V_3-\tfrac12\le-\tfrac12)=\tfrac14>e^{-1{,}5}\approx0{,}2231$ | Thêm $\tau=-1$ và dấu của $(x-1)^3$; (e): chứng minh chỉ cần "$\le$", đúng khi $\tau>0$, sai khi $\tau<0$; nêu vi phạm cụ thể của Định lý 02.7(b) |
| trung bình | 02.10(c) đề, Bước 1–2 | "Cách làm của (a)" có hai cách hiểu cho hai đáp số ($40\,001$ / $10^8+1$ theo Markov trực tiếp; $160\,000$ / $4\cdot10^8$ theo $\epsilon\delta/2$) | — | Đề ghi rõ "cận Markov ở Bước 1 của (a), với dấu '$<\delta$'" hoặc nêu cả hai |
| nhẹ | 02.10(d) | Nhận xét "$\inf L_D>0$" thuộc Định nghĩa 01.25, không phải 01.18 | — | Ghi rõ trường hợp bất khả tri |
| nhẹ | 02.10(c) Bước 3 | So với cỡ mẫu Hoeffding của Ví dụ 02.4 (bảo đảm khác) | — | "chỉ so cách phụ thuộc vào $\delta$" |
| nhẹ | 02.6(c) Bước 4 | $r_m$ hai giá trị | — | $r_{10}$ |
| nhẹ | 02.8(c) Bước 1 | "tăng tuyến tính" chỉ có cận trên | — | Thêm $\ln(3^p+1)\ge p\ln3$ |
| nhẹ | 02.8(a) Bước 2 | Bỏ sót $L\subsetneq L'$ | — | "(đổi vai trò nếu cần)" |
| nhẹ | 02.5(a) | So với tích số thực $0{,}12m$; ghi chú dấu phẩy động nói chung | float64 đúng; float32 sai tại $12/100$, $64/200$ | Dùng ngưỡng nguyên; nói rõ phụ thuộc độ chính xác |
| nhẹ | 02.5(c) | "phải gần" quá mạnh | Chebyshev cho $8/9$ | "với xác suất ít nhất $8/9$" |
| nhẹ | 02.4(c) Bước 3 | "không xa" lỏng | $0{,}977$ / $0{,}6236$ | "cùng bậc độ lớn" |
| nhẹ | 02.2 Gợi ý 2 | Số mũ cần cả Bổ đề 02.6 | — | Ghi rõ |
| nhẹ | `outline.md` §4 mục 4 | Ghi 02.4 "mục tiêu 5"; đúng là 6 | — | Sửa dàn ý |

**Từng bài:** 02.1 cần sửa (a–c đúng; $5{,}7918$, $6{,}4259$, $1/12$, $2000$, $738$); 02.2 đúng ($2500$, $3{,}35\cdot10^{-4}$, $0{,}2865$); 02.3 đúng ($1523$, $1659$, hiệu $136$, cận $139$); 02.4 đúng ($0{,}0815$, $22/1024$, $0{,}6236$, $0{,}9924$); 02.5 đúng (sai số chuẩn $0{,}00144$, $2{,}99\cdot10^{-4}$; $R\ge1{,}117\cdot10^5$); 02.6 đúng; 02.7 đúng (nguyên tử, $h_\varnothing$, $176$); 02.8 đúng ($140$, $2936$, $280$, $11\,741$); 02.9 đúng; 02.10 cần sửa; 02.11 đúng ($17\,539$). Mọi dẫn chiếu tới ghi chú đúng; gợi ý tăng dần; "Kiểm tra lại" đúng.
