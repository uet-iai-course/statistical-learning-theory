# Bài tập Bài 09 — rà lại toán sau khi sửa (người rà 2)

**Đối tượng.** Bản `lec09-ex-r1-frozen.md`: 1027 dòng, 9 985 tiếng theo `wc -w`, trùng byte với `2627-1/materials/lec-09/exercises.md` (kiểm bằng `cmp`).

**Đã đọc.** Diff `lec09-ex-r1.udiff`; `11-quyet-dinh-bai-tap.md`; dòng §11 của ghi chú, nay ghi "Bài tập 09.4 … mục tiêu 4, 5" và "Bài tập 09.10 (Tùy chọn: …)".

Chỉ đọc repo, không commit.

## Tổng kết

| Mức | Số phát hiện mới |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 0 |
| nhẹ | 0 |

Cả bốn phát hiện cũ đều đã sửa. Mọi phần toán thay đổi đúng, mọi số mới tính lại khớp, và không còn sót kí hiệu cũ ($\varphi_0$, $S^2$, $N$). Các chỗ cắt câu lặp không làm mất bước nào của lời giải.

## Phát hiện cũ

| Phát hiện | Dòng mới | Đánh giá |
|---|---|---|
| F1: 09.6, tỉ số và phép chia ví dụ | 607–611 | ✓ $6{,}0$; $5{,}7$; "$0{,}00071/0{,}000125\approx5{,}7$" (tính lại được $5{,}68$). Câu "chín lần" đã cắt. |
| F2: 09.6, "của dòng $m=50$" | 573 | ✓ |
| F3: 09.6(a)(iii), mô hình học được | 650 | ✓ $0{,}0392-0{,}00071=0{,}03849\approx0{,}0385$. Độ lệch chuẩn $0{,}0013$ khớp số tôi tính trực tiếp ($0{,}00135$). |
| F4: 09.8, phần do học phần thêm | 782 | ✓ "Ý (a), (c) và số ở (b) do học phần thêm". |

## Phần toán đã đổi

| Vị trí | Đánh giá | Kiểm |
|---|---|---|
| 09.4(b), Bước 5 (tái tạo và KL) | ✓ | Tái tạo: $0{,}1\ln\rho_0(1{,}5)+0{,}9\ln\rho_0(0{,}5)=-0{,}204394-0{,}939545=-1{,}143939$. KL tới tiên nghiệm: $0{,}1\ln0{,}2+0{,}9\ln1{,}8=-0{,}160944+0{,}529008=0{,}368064$. Hiệu bằng $-1{,}512003$, đúng ELBO tính trực tiếp. Giả thiết thêm của Định lý 09.12(c) thỏa vì $\mathcal V$ hữu hạn. Bước 6 cũ (khe = KL) vẫn dẫn đúng "khe của Bước 4". |
| 09.4(d) (biến ẩn rời rạc) | ✓ | Đạo hàm của $\operatorname{ELBO}(\phi)=(1-\phi)\ln\frac{p_1}{1-\phi}+\phi\ln\frac{p_2}{\phi}$ là $\ln\frac{p_2}{\phi}-\ln\frac{p_1}{1-\phi}$ (hai số hạng $\pm1$ triệt tiêu). Tại $\phi=\tfrac12$, giá trị là $\ln(\rho_0(0{,}5)/\rho_0(1{,}5))=1$; sai phân số học cho $1{,}0000$. Với $U_0\ne\phi$ (xác suất $1$), $v$ không đổi khi $\phi$ thay đổi ít, nên $\partial_\phi\kappa=-\partial_\phi\ln q_\phi(v)$, bằng $-2$ hoặc $+2$, mỗi giá trị với xác suất $\tfrac12$; kì vọng bằng $0\ne1$. Thật ra kì vọng này bằng $-\sum_v\partial_\phi q_\phi(v)=0$ với mọi $\phi$; bài không cần nói điều này. $\mathbb E_{U_0}\kappa=\operatorname{ELBO}(\phi)$ vì $v\sim q_\phi$. Điều kiện (i) không thỏa vì $\phi\mapsto v$ nhảy tại $U_0\in\Phi=(0,1)$. Mục tiêu "4 và 5" và dòng §11 của ghi chú khớp nhau. |
| 09.5(a), Bước 2–3 | ✓ | Tính lồi của $-a\ln\theta-b\ln(1-\theta)$ cho điểm cực tiểu. $7(1-\theta)=5\theta\Rightarrow\theta=\tfrac7{12}$. |
| 09.7, Gợi ý 1–2 và (c) Bước 3 | ✓ | $(2\mu-2)^2+(2-\mu)^2=5\mu^2-12\mu+8$; $\sigma^2+5\sigma^2+(\sigma^2-2+1/\sigma^2)-2=7\sigma^2+1/\sigma^2-4$. Gợi ý 1 không còn lộ lời giải; Gợi ý 2 giữ cách thác triển bằng tiếp tuyến. |
| 09.7(e) | ✓ | "(G2) không thỏa trên $[0,2]\times(0,1]$": đúng tập. |
| 09.7(b), đề | ✓ | Câu "chọn lân cận cho mọi điểm" đã bỏ khỏi đề; Gợi ý 2 và lời giải vẫn cho lân cận $U$ tại mọi điểm. |
| 09.8: $V_s$ thay $S^2$; Bước 2 khai triển | ✓ | Khai triển dùng $\sum_i(x^{(i)}-\bar x)=0$. Bước 1 của (b) dẫn đúng "(a), Bước 2". |
| 09.10: $\nu_+$ thay $N$ | ✓ | Đổi nhất quán ở (b) Bước 2, (c) Bước 1–3. Giá trị lớn nhất vẫn là $-6\ln2$. |
| 09.4(b): $\rho_0$ thay $\varphi_0$ | ✓ | Đổi nhất quán ở gợi ý và lời giải. |
| 09.1(c) Bước 2; 09.1(d) "tổng của cấp số nhân", "xác suất kết thúc" | ✓ | Nội dung toán không đổi. |
| Các chỗ cắt (09.2 Bước 5 và (d); 09.3 (b), (c), (d); 09.4 (a) Bước 3 và (c) Bước 1; 09.6 (a) Bước 4 và (b), (c); 09.8 (b), (c); 09.9 Kiểm tra lại; 09.10 (a)) | ✓ | Chỉ bỏ các câu bình luận lặp. Các bước chứng minh và tính còn nguyên. Ở 09.6(a)(iii), câu trả lời vẫn so $18$ với phân bố mô phỏng qua $-1{,}7$ độ lệch chuẩn ($5{,}9\%$ vẫn có trong đề). |

## Phát hiện mới

Không có.
