# Quyết định gộp hai lượt rà bài tập — Bài 06 (điều phối viên, 2026-10-31)

Căn cứ: `9-bai-tap-toan.md` (0/0/0/2), `10-bai-tap-su-pham.md` (0/0/6/16). Số dòng theo bản đóng băng `lec06-ex-frozen.md` (SHA-256 `cff790a9b0ad5954`). Người soạn áp dụng mọi mục dưới đây và các điểm nhẹ còn lại theo đề xuất, ghi mục không áp dụng kèm lý do vào `bai-tap-ghi-chu.md` §8. Độ dài ≤ 10 000 tiếng.

## Toán (nhẹ, áp dụng)

1. 06.5(c)/(d) (dòng 528, 529, 540): cận trên làm tròn lên: $0{,}0467$ (từ $0{,}046627$), $2{,}3956$ (từ $2{,}395542$); điều phối viên kiểm: $G_\lambda=2(\sqrt{2/\lambda}+1)$, $2G_\lambda^2/(\lambda m)$ với $m=1000$.
2. 06.2(c) (dòng 126): mẫu gồm các bản sao không có phân bố $D^m$; ở lần dùng đầu viết $\mathbb E[L_D(A(S))-L_S(A(S))]$ thay cho tên "khoảng cách tổng quát hóa kì vọng" (Định nghĩa 06.4 đòi $S\sim D^m$).

## Sư phạm (trung bình, áp dụng)

3. 06.3(a) chép lại chứng minh Bổ đề 06.7: cắt (bù chữ cho các mục khác); giữ (b)–(d) đúng bài gốc 3 của blueprint ("Derive the solution-distance bound").
4. Gợi ý 1 của 06.5, 06.7 (và mức nhẹ hơn 06.4, 06.8, 06.9) lộ lời giải: viết lại thành hướng tiếp cận; bước then chốt chuyển sang gợi ý 2.
5. $m_{\mathcal H}(\epsilon)$ ở 06.7 đổi thành $\bar m(\epsilon)$ (cỡ mẫu cho mức kì vọng), tránh lẫn với độ phức tạp mẫu $m_{\mathcal H}(\epsilon,\delta)$.
6. $K$ ở 06.5 đổi: quả cầu viết $W_{r_\lambda}$ ($K$ giữ nghĩa số ứng viên).
7. $R$ (hàm chính quy hóa) ở 06.11 đổi thành $\Omega$ (khớp Bài 04 dòng 997; $R$ là cận khoảng cách khởi tạo, Bài 05).
8. Phủ mục tiêu 4 ("hệ số ổn định cho hồi quy logistic"): thêm một câu và một kết quả số vào 06.4(c) ($\epsilon_{\mathrm{stab}}=2G^2/(\lambda m)$ với hồi quy logistic của ý đó; người rà đề xuất $0{,}1$ — người soạn tính lại và ghi số). Mục tiêu 2 được đo ở 06.9 và một phần ở 06.1(b): chấp nhận, không thêm bài.

## Nhẹ (áp dụng)

$10.000$ trong công thức viết $10\,000$; "ellip" → "elip"; "ma trận đạo hàm bậc hai" thêm "(Hessian matrix)" ở lần đầu; bỏ "hiển nhiên"; $\lambda_1,\lambda_2$ hai nghĩa ở 06.4(d) đổi một cặp; tách các đoạn dồn phép tính theo §7a; sửa câu dòng 9 về phạm vi kí hiệu chỉ dùng trong bài tập.
