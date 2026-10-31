# Rà lại toán bộ bài tập Bài 07 sau khi sửa (người rà 2)

Đối tượng: `lec07-ex-r1-frozen.md` (889 dòng; trùng `materials/lec-07/exercises.md`). Đầu vào: `lec07-ex-r1.udiff`, `reviews/11-quyet-dinh-bai-tap.md`. Số tham chiếu: `reviews07/r2/ex/ex_nums.py` và các tệp `exp_m*.txt` của lượt rà trước.

## Tổng kết

Không có phát hiện mới ở mức nào. Bốn phát hiện cũ đã sửa ✓. Mọi phần toán đã đổi đều dựng lại được và đúng; mọi số mới khớp; các phép đổi kí hiệu không làm sai công thức nào.

## Phát hiện cũ

| Phát hiện (9-bai-tap-toan.md) | Trạng thái | Bằng chứng (dòng `lec07-ex-r1-frozen.md`) |
|---|---|---|
| Hai số làm tròn ($3774{,}3$; $46\,586$) | ✓ | 567 ($3774{,}2$), 598 ($3774{,}2/446{,}7\approx8{,}45$; giá trị đúng $8{,}4488$), 569 ($46\,585$) |
| Sai số chuẩn khi hai nhóm dùng chung hạt giống | ✓ | 634: "Coi hai nhóm như độc lập … $\approx0{,}002$ … ghép cặp theo hạt giống (từ các lần chạy riêng lẻ) … $0{,}0019$. Cả hai lớn hơn hiệu $0{,}0013$". Tính lại: $0{,}002026$ và $0{,}001926$; hiệu $0{,}0013$ |
| 07.7, 07.8: ghi rằng (b), (c) do học phần thêm | ✓ | 660, 724 |
| 07.9: $k\ge1$ khi $G=0$ | ✓ | 812, 864: $k=\max\{1,\lceil G/\epsilon\rceil\}$. Khi $G=0$ thì $G/k=0\le\epsilon$ |

## Dựng lại các phần đã đổi

| Phần | Kết luận | Ghi chú |
|---|---|---|
| 07.1, $\theta_{\mathrm{abs}}\to\theta_{\mathrm{II}}$ (22–100) | ✓ | Chỉ đổi tên; tham số, giá trị và miền không đổi. |
| 07.3(e), hiển thị mới cho cận logistic | ✓ | $2BC_x/\sqrt m=0{,}01$; $\sqrt{\ln40/(2\cdot10^6)}=0{,}0013581$; $0{,}01+3\cdot5{,}006715\cdot0{,}0013581=0{,}030399\le0{,}0304$. |
| 07.4(b), thêm "$S\sim D^m$ theo (T1)" | ✓ | Đúng giả thiết của Định lý 02.14. |
| 07.4(d), gợi ý mới | ✓ | Gợi ý 1 ("tìm một đẳng thức hay một cận sẽ sai khi bỏ giả thiết") đúng hướng: Mệnh đề 01.7 và phép đổi chỗ cần (T1); $c_i=1/m$ cần giá trị trong $[0,1]$; $L_D(g)=\mathbb E_{S'}L_{S'}(g)$ cần lớp cố định. Gợi ý 2 chuyển tiêu đề bước và các ví dụ vi phạm sang, đúng. |
| 07.5(b), quy nạp viết lại | ✓ | Bước cơ sở $t=1$ ở đầu, rồi bước quy nạp; lập luận không đổi. |
| 07.6, $\bar n\to\bar B$ | ✓ | Định nghĩa ở 575; bảng cận dưới (607–612) giữ $134{,}0$; $194{,}2$; $345{,}1$; $609{,}3$. |
| 07.6(b) đề mới và Bước 1 dạng danh sách | ✓ | Ba kết luận được phép không đổi nội dung. Đề hỏi so sánh hiệu với sai số chuẩn; độ lệch chuẩn đã cho ở bảng, nên học viên tính được bản coi hai nhóm độc lập. Lời giải ghi rõ bản ghép cặp lấy từ các lần chạy riêng lẻ. |
| 07.6 "Kiểm tra lại" mới | ✓ | $194{,}2\in[75,372]$; tỉ số $11{,}85$. |
| 07.7(b), gợi ý mới | ✓ | Gợi ý 1 "tìm điểm mà tại đó mỗi lớp đạt $\Pi(1)=2$", Gợi ý 2 "hai điểm khác nhau": đúng hướng tới lời giải $\Pi=2<4$. |
| 07.7(c), câu định nghĩa hàm kích hoạt ngưỡng viết lại | ✓ | Nội dung toán không đổi. |
| 07.8, $\mathcal H_{(1)},\mathcal H_{(2)}\to\mathcal H_1,\mathcal H_2$; "lớp hàm hợp" | ✓ | Ở (c), $\mathcal H_1$ (ánh xạ lớp ẩn, $\mathcal X\to\mathcal X'=\{0,1\}^{N_1}$) và $\mathcal H_2$ (thu hẹp của $\mathcal H^{N_1}_{\mathrm{aff}}$ lên $\mathcal X'$) đúng vai của (a). Công thức $\Pi\le\Pi_{\mathcal H_2}\Pi_{\mathcal H_1}\le(em)^{N_1+1}(em)^{N_1(p+1)}=(em)^P$ đúng. Trong 07.7, $\mathcal H_1$, $\mathcal H_2$ là hai lớp của tích, ở khối khác, nên không xung đột. |
| 07.8(b), bỏ $\tau_{\mathcal H}$ | ✓ | Viết "hàm tăng trưởng theo định nghĩa đó", ba bước. (1) $\lvert\mathcal X'\rvert<m$: giá trị lớn nhất lấy trên họ rỗng. (2) $\lvert\mathcal X'\rvert\ge m$: cần tính không giảm theo $m$. (3) $\Pi$ cho phép lặp; xảy ra khi $m>2^{N_1}$. Cả ba đúng. |
| 07.9, $\vartheta_i\to\Delta\mu_i$ (830–846) | ✓ | $\Delta\mu_0=\mu_0$ (vì $\mu_{-1}=0$, theo Gợi ý 2 mà Bước 1 dẫn tới). Bước quy nạp $f(t_{j-1})+\mu_{j-1}(x-t_{j-1})+\Delta\mu_j(x-t_j)=f(t_j)+\mu_j(x-t_j)$ đúng. Khớp Gợi ý 2 (dòng 824). |
| 07.9(d), $\tilde f$ | ✓ | Mệnh đề cho hàm liên tục bất kì rồi suy ra cho mạng có hàm kích hoạt liên tục, đúng. Lập luận giới hạn trái không đổi. |

## Số mới

| Dòng | Bài viết | Tính được | Khớp? |
|---|---|---|---|
| 567, 598 | $3774{,}2$; $8{,}45$ | $3774{,}2496$; $8{,}4488$ | ✓ |
| 569 | $46\,585$ | $46\,585{,}47$ | ✓ |
| 634 | $\approx0{,}002$; $0{,}0019$; hiệu $0{,}0013$ | $0{,}002026$; $0{,}001926$; $0{,}0013$ | ✓ |
| 07.3(e) | $0{,}01+3\cdot5{,}0067\cdot0{,}001358\le0{,}0304$ | $0{,}030399$ | ✓ |
| 07.6 "Kiểm tra lại" | $194{,}2$ trong $75$–$372$; $11{,}85$ | $194{,}243$; $11{,}852$ | ✓ |
| 812, 864 | $k=\max\{1,\lceil G/\epsilon\rceil\}$; $k=10$, $31$ tham số | $3\cdot10+1=31$ | ✓ |

## Phát hiện mới

Không có.
