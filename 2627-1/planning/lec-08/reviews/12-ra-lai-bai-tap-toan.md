# Rà lại toán bộ bài tập Bài 08 sau khi sửa (người rà 2)

**Đối tượng.** Bản `lec08-ex-r1-frozen.md`; số dòng ở bảng phát hiện theo bản này.

**Căn cứ.**
- Diff `lec08-ex-r1.udiff`.
- Quyết định gộp hai lượt rà: `11-quyet-dinh-bai-tap.md`.
- Ghi chép của người soạn: `bai-tap-ghi-chu.md` §8.

**Phép tính lại.** Script `reviews08/r2/ex/r1_check.py`, đầu ra `r1_check_out.txt`. Những số không đổi đã kiểm ở `9-bai-tap-toan.md`.

Tôi chỉ đọc repo và không commit. Phạm vi là toán học, nên không dùng `no-ai-slop`.

## 1. Tổng kết

| Mức | Phát hiện mới |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 0 |
| nhẹ | 0 |

Cả ba phát hiện cũ đã được sửa đúng. Mọi phần toán thay đổi đều dựng lại được và mọi số mới đều khớp. Bản sửa không đưa thêm lỗi nào.

## 2. Phát hiện cũ

| Phát hiện cũ | Kết quả | Vị trí trong bản r1 |
|---|---|---|
| Tỉ số $1{,}8$ phải là $1{,}7$ | ✓ | dòng 682: "$0{,}0011$; $1{,}7$". Tính lại: $0{,}0019/0{,}0011=1{,}73$; với số chưa làm tròn là $1{,}74$ |
| Ô "08.5, Bước 1" thiếu "$W$ lồi" | ✓ | dòng 346 |
| Dẫn Nhận xét 08.11 ra ngoài phát biểu của nó | ✓ | dòng 574 nêu đúng phạm vi: SGD không chiếu, hàm lỗi trong $[0,1]$; cần chia hàm lỗi cho cận trên và kiểm lại lập luận khi có phép chiếu |

## 3. Phần toán đã đổi

| Phần | Kết quả | Kiểm tra |
|---|---|---|
| 08.3(a) mới: tính không giãn của bước gradient Huber | ✓ | Với $u>v$ và $\delta=d(u)-d(v)$, tính không giảm cho $\delta\ge0$, tính $1$-Lipschitz cho $\delta\le u-v$. Từ đó $(1-\eta)(u-v)\le\Gamma(u)-\Gamma(v)\le u-v$, và $\lvert1-\eta\rvert\le1$ khi $0\le\eta\le2$. Tính lồi (tức $d$ không giảm) cho cận trên; điều kiện $\eta\le2/\beta$ cho cận dưới. Lập luận dùng đúng hai tính chất mà đề cho và không dùng Bổ đề 08.4. Phản ví dụ $\eta=3$, $z=0$, $u=0{,}2$, $v=-0{,}2$: ảnh là $-0{,}4$ và $0{,}4$, hiệu $0{,}8=2\lvert u-v\rvert$, khớp cột Huber của Ví dụ 08.3. Mô phỏng $2\cdot10^6$ bộ $(u,v,z)$ ngẫu nhiên cho tỉ số lớn nhất $1{,}0000$ với $\eta\in\{0;0{,}5;1;1{,}5;2\}$, $1{,}5$ với $\eta=2{,}5$, $2$ với $\eta=3$ |
| 08.3(b)–(e) đánh lại nhãn | ✓ | Nội dung toán giữ nguyên (đã kiểm ở `9-bai-tap-toan.md`). Gợi ý ghi Phần (b), (d), (e) đúng chỗ; "Kiểm tra lại" ghi Ở (a), Ở (d) đúng. Không còn dẫn chiếu theo nhãn cũ, trong bộ bài tập cũng như trong ghi chú |
| 08.3(c), câu tổng kết | ✓ | Câu "tính lồi của hàm lỗi chỉ đi vào qua Bổ đề 08.4(a), ở Bước 1 của Mệnh đề 08.5" khớp ghi chú |
| 08.5(d)(ii): giả thiết đạo hàm cấp một và cấp hai bị chặn nay nằm trong đề | ✓ | $W$ bị chặn và gradient liên tục cho $G$ hữu hạn; đạo hàm cấp hai bị chặn cho $\beta_W$ trên $W$. Bước 1 của Phụ lục D chỉ dùng hai điểm lặp thuộc $W$, nên thừa số $(1+\beta_W\eta)^T$ hợp lệ. $1{,}1^{10^5}=10^{4139{,}27}$. Câu dẫn Nhận xét 08.11 nêu đúng phạm vi. Bảng 08.5(c): "$W$ là toàn bộ không gian tham số" đúng. "Kiểm tra lại": $10/(1+e)=2{,}689$ |
| 08.6: "sai số chuẩn của hiệu theo hạt giống" | ✓ | Chỉ đổi thuật ngữ; số giữ nguyên và khớp lần chạy lại: độ lệch chuẩn của hiệu chia $\sqrt{20}$. Tỉ số với sai số chuẩn khi coi hai nhóm độc lập: $0{,}026313/0{,}002147=12{,}3$, đúng "khoảng $12$ lần" |
| 08.8 sau khi cắt (c) | ✓ | Ý (d) cũ thành (c); gợi ý và lời giải đánh lại đúng. Ý (b) bỏ câu "$10^{-8}$" nhưng các giá trị $B(T^*)$ là cận làm tròn lên, vẫn đúng. Câu dẫn Hệ quả 08.8(b) ở Bước 4 đúng |
| 08.2(c) Bước 4: tự chứng minh $\sum1/t^2\le2$ | ✓ | $\sum_{t\ge2}1/t^2\le\int_1^\infty x^{-2}dx=1$, như (a) |
| 08.1(c): "nhỏ hơn ngặt cận của Mệnh đề 08.5(a) trên dãy đó"; phần hụt $\tfrac3{16}$ | ✓ | Đúng hai dãy $(4,1)$ và $(4,2)$; $\tfrac3{16}=1-\tfrac{13}{16}$ |
| 08.4(a) gợi ý; 08.4(c) Bước 1 ($L_D(w_1)=\ln2$, nói rõ là theo ước lượng) | ✓ | |

## 4. Phát hiện mới

Không có.
