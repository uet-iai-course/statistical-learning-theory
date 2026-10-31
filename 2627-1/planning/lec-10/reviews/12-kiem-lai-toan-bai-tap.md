# Kiểm lại toán bản sửa bài tập Bài 10 (người rà 2)

Đầu vào: `reviews10/ex-diff.txt` (53 khối đổi), tệp hiện tại `2627-1/materials/lec-10/exercises.md` (9 961 tiếng), `reviews/11-quyet-dinh-bai-tap.md`. Chỉ đọc, không commit. Đã tính lại bằng Python (tích phân số, kiểm hàm trội trên lưới).

## 1. Bốn mục toán của `9-bai-tap-toan.md`

| Mục | Trạng thái | Kiểm |
|---|---|---|
| 10.3(a), tính đo được (trung bình) | đóng đúng | Dòng 354: $\{g=\tau'\}$ là giao hữu hạn các tập $\{U_t<\pi_\theta(1\mid s_t)\}$ hay phần bù, cùng các điều kiện chỉ theo $U_{\mathrm{init}}$, $V_t$. $\varphi=\sum_{\tau'}\mathbb 1[g=\tau']\,(-\hat g_\theta(\tau'))$. Lập luận chặt. |
| 10.4(c), điều kiện hóa | đóng đúng (nhẹ, xem dưới) | Dòng 541: điều kiện hóa theo dữ liệu huấn luyện và nguồn ngẫu nhiên; giá trị tổng thể là số cố định có điều kiện, ngẫu nhiên theo dữ liệu huấn luyện. Dòng 557: $\Delta_{\mathrm b}\in[-0{,}19-0{,}0752;\,-0{,}19+0{,}0752]=[-0{,}2652;\,-0{,}1148]$, đúng. |
| 10.9(b), miền của $u$ | đóng đúng | Dòng 874: giả thiết $W$ bị chặn, $R\ge\sup_{u\in W}\lVert w_1-u\rVert$; dòng 911: "với mọi $u\in W$, vốn có $\lVert w_1-u\rVert\le R$". |
| 10.9(a) Bước 4 | đóng đúng | Dòng 907: bỏ câu "Thứ tự này cần thiết"; nêu $\sup_u\sum_m\le\sum_m\sup_u$. |

## 2. Ý mới 10.1(f)

| Kiểm | Kết quả |
|---|---|
| Khớp Nhận xét 10.5 | Ghi chú: phần thưởng bị chặn; mật độ theo độ đo nền không phụ thuộc $\theta$; $\theta\mapsto p_\theta(\tau)$ khả vi liên tục với mọi $\tau$; hàm trội $\lvert R\rvert\lVert\nabla p_\theta\rVert\le\Lambda$ trên một lân cận $U$. Lời giải kiểm đúng bốn mục này. Ở đây $H=1$, không có trạng thái, quỹ đạo là $A$; $\Theta=(0,\infty)$ mở. |
| Đạo hàm | $\partial_\theta(\theta e^{-\theta a})=e^{-\theta a}(1-\theta a)$, liên tục theo $\theta$: đúng. |
| Hàm trội | Với $\theta\in(\theta_0/2,2\theta_0)$ và $a>0$: $\lvert1-\theta a\rvert\le1+\theta a\le1+2\theta_0a$ và $e^{-\theta a}\le e^{-\theta_0a/2}$. $\int_0^\infty\Lambda=\tfrac2{\theta_0}+2\theta_0\cdot\tfrac4{\theta_0^2}=\tfrac{10}{\theta_0}$: đúng (tích phân số tại $\theta_0=1$ cho $10{,}000$; kiểm bất đẳng thức trên lưới $300\times3000$: đúng mọi điểm). Gợi ý 2 nêu đúng hàm này. |
| $J'(1)=e^{-1}$ | $J=1-e^{-\theta}$; $\partial_\theta\ln p_\theta=\tfrac1\theta-a$; $\int_0^1ae^{-a}=1-2e^{-1}$; $\int_0^1(1-a)e^{-a}=e^{-1}=0{,}367879$ (số: $0{,}367879$). Đúng cả hai cách. |
| Bước 4 so với Ví dụ 10.3 | Đúng như ghi chú: giá $[0,\theta]$ di chuyển, $\theta\mapsto p_\theta(a)$ nhảy tại $\theta=a$, nên điều kiện khả vi không thỏa (khớp Nhận xét 10.5 và Phụ lục A, Bước 1). Ở đây giá $(0,\infty)$ cố định. Gợi ý 1 ("giá không phụ thuộc $\theta$") đúng hướng. |

## 3. "Kiểm tra lại" mới của 10.7 (dòng 776)

Ví dụ 10.2: $r(s_0,\cdot)\in\{0,1\}$, $r(s_1,\cdot)\in\{3,1\}$, $r(s_2,\cdot)\in\{0,1\}$. Do đó $r_{\min}=0$, $r_{\max}=3$, $H=2$, miền $[0,6]$. Ví dụ 10.12 dùng $[0,4]$ vì bước đầu luôn ở $s_0$ (phần thưởng thuộc $\{0,1\}$), nên $\max R=1+3=4$. Tỉ số bán kính $6/4=1{,}5$. Đúng. Đề đã bỏ câu "nêu thêm một thay đổi … (T1)", khớp với việc bỏ hai đoạn tương ứng trong lời giải; không còn câu hỏi nào bị bỏ lửng.

## 4. Các dòng đổi khác

Đã kiểm từng khối trong diff; không có sai toán và không mất bước:
- 10.1: (c) Bước 4 chỉ còn đường qua đẳng thức đã chứng minh, đủ. (d) Bước 2 có đủ hai giá trị. (e) Bước 1 tự chứa đạo hàm $(1-2\pi)\pi(1-\pi)$.
- 10.2(a) Bước 3 tự chứa đạo hàm theo $\theta_s$.
- 10.3: (b) Bước 4 có nghiệm $\frac{34\pm\sqrt{292}}{48}=0{,}3523;\ 1{,}0643$. (d) Bước 2 dẫn đoạn sau Định nghĩa 05.2, đúng chỗ.
- 10.5: Gợi ý 2(c) cho đạo hàm $(1-\alpha)(w-1)+4\alpha w$, đúng.
- 10.6: Bước 3 tự chứa $L_A+L_B$. "Kiểm tra lại": $\sqrt{0{,}051^2+0{,}132^2}/4{,}472=0{,}0316>0{,}0275$, đúng.
- 10.8: Gợi ý (b) không lộ lời giải.
- 10.9(c): $1000-512+1=489$ vòng; "làm tròn lên" $107{,}97$.

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | dòng 561 (10.4(c), câu cuối) | "Khẳng định đúng với xác suất ít nhất $0{,}95$ có điều kiện, nên cũng đúng khi lấy kì vọng theo dữ liệu huấn luyện" mơ hồ. Điều đúng là xác suất không điều kiện (theo cả dữ liệu huấn luyện và mẫu kiểm tra) cũng ít nhất $0{,}95$, vì nó là kì vọng của xác suất có điều kiện. | Tính chất tháp: $\Pr(E)=\mathbb E[\Pr(E\mid\text{huấn luyện})]\ge0{,}95$ | "Xác suất có điều kiện ít nhất $0{,}95$ với mọi dữ liệu huấn luyện, nên xác suất không điều kiện, lấy theo cả dữ liệu huấn luyện và mẫu kiểm tra, cũng ít nhất $0{,}95$." |

## Kết luận

**Đạt.** Bốn mục toán đã đóng đúng. Ý 10.1(f) đúng: ba điều kiện khớp Nhận xét 10.5, hàm trội và $J'(1)=e^{-1}$ đúng, Bước 4 mô tả đúng Ví dụ 10.3. "Kiểm tra lại" của 10.7 đúng. Không dòng sửa nào sai toán. Còn một điểm nhẹ về câu chữ, không chặn.
