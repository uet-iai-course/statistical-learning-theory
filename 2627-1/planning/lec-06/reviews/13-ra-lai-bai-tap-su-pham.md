# Rà lại sư phạm và văn phong bộ bài tập Bài 06 (sau sửa)

Đối tượng: `lec06-ex-r1-frozen.md` (1119 dòng, 9 938 tiếng), đọc qua diff `lec06-ex-r1.udiff`. Căn cứ: `reviews/11-quyet-dinh-bai-tap.md`, `bai-tap-ghi-chu.md` §8, báo cáo cũ `10-bai-tap-su-pham.md`. Chế độ `no-ai-slop`: Detect. Vị trí ghi theo số dòng của `lec06-ex-r1-frozen.md`.

**Tổng kết:**
- Phát hiện cũ: 22. Đã sửa đạt 21 (✓). Sửa một phần 1: phát hiện về phủ mục tiêu 4 ở 06.4(c). Không sửa 0.
- Phát hiện mới: 5, gồm 0 chặn bàn giao, 0 nghiêm trọng, 0 trung bình, 5 nhẹ.

## 1. Kiểm phát hiện cũ

| Phát hiện cũ (mức) | Kết quả | Lý do |
|---|---|---|
| 06.3(a) chép lại chứng minh Bổ đề 06.7 (trung bình) | ✓ | Đã cắt (a). Các ý (b)–(d) đổi thành (a)–(c). Lời giải dẫn "Bổ đề 06.7" và "Bước 1 của chứng minh Bổ đề 06.7". Ở 06.11 đã bỏ "(hay (a) của Bài tập 06.3)" và đổi tham chiếu thành 06.3(b) (dòng 1116). |
| Gợi ý 1 của 06.5, 06.7 lộ lời giải (trung bình) | ✓ | Gợi ý 1 mới chỉ cho hướng tiếp cận: 06.5 "So giá trị nhỏ nhất … tại một điểm cụ thể…; sau đó chặn … từ dưới"; 06.7 "Xét dấu …, rồi dùng một bất đẳng thức chỉ cần kì vọng" và "Chia sai số … làm hai nửa". Điểm $0$, $\ell\ge0$ và Bổ đề 02.2 đã chuyển xuống Gợi ý 2, nên các gợi ý tăng dần đúng yêu cầu. |
| Gợi ý 1 của 06.8, 06.4, 06.9 (trung bình) | ✓ | 06.8: "tìm một điểm của $W$ có $L_S=0$ …", còn $\mathbf e_j$ nằm ở Gợi ý 2. 06.4(d): "Dùng tính tối ưu của mỗi nghiệm …". 06.9: "Thêm bớt … như trong chứng minh Mệnh đề 06.5; mỗi định nghĩa chặn một số hạng." Gợi ý 1 mới của 06.3 cũng không lộ lời giải, vì đề (a) đã nói rõ phương pháp. |
| $m_{\mathcal H}(\epsilon)$ ở 06.7 (trung bình) | ✓ | Đã đổi thành $\bar m(\epsilon)$ ở mọi chỗ, có thêm vế "khác độ phức tạp mẫu $m_{\mathcal H}(\epsilon,\delta)$". |
| $K$ ở 06.5 trùng số ứng viên (trung bình) | ✓ | Quả cầu viết $W_{r_\lambda}$, khớp kí hiệu $W_B$ của §9. Gợi ý 2 viết "một tập con". $K$ nay chỉ còn nghĩa số ứng viên. |
| $R$ ở 06.11 (trung bình) | ✓ | Đã đổi thành $\Omega$ trong đề, Gợi ý 2, lời giải và mục Kiểm tra lại. |
| Câu dòng 9 về phạm vi kí hiệu (nhẹ) | ✓ | |
| Mục tiêu 4: hệ số ổn định cho hồi quy logistic (nhẹ) | một phần | Đề 06.4(c) và Bước 5 (dòng 427–437) đã thêm; số $0{,}1$ và $0{,}2$ đúng, đồng thời là hai số hạng ổn định của $Q(\lambda_0)$ và $Q(\lambda^*)$. Còn hai chỗ: câu kết Bước 5 mơ hồ, và §11 của ghi chú vẫn ghi 06.4 đo mục tiêu 5 (phát hiện mới 1, 2). |
| $10.000$ (nhẹ) | ✓ | |
| "ellip" (nhẹ) | ✓ | Không còn chỗ nào viết "ellip". |
| "(Hessian matrix)" (nhẹ) | ✓ | |
| "(random seed)", nhãn "Kết quả mong đợi và phạm vi." (nhẹ) | ✓ | |
| "hiển nhiên" (nhẹ) | ✓ | |
| $\lambda_1,\lambda_2$ hai nghĩa ở 06.4(d) (nhẹ) | ✓ | Lưới nay viết $\Lambda$ gồm $K$ giá trị. |
| "Chọn sai $\lambda$ hai lần" (nhẹ) | ✓ | |
| 06.2(b1) Bước 3 dồn phép tính (nhẹ) | ✓ | Viết thành `aligned`, có bước phương sai. |
| Đoạn dồn ở 06.3, 06.4(c), 06.7(c) (nhẹ) | ✓ | 06.3(c) tách thành Bước 3 và Bước 4. 06.4(c) tách thành Bước 3, 4, 5. 06.7(c) Bước 4 là `aligned` ba dòng, câu kết luận thành đoạn riêng. |
| Câu "liệt kê bằng máy" ở 06.2 (nhẹ) | ✓ | |
| Câu đề 06.2(d) (nhẹ) | ✓ | |
| Lượng từ ở 06.5(a) (nhẹ) | ✓ | |
| $h'$ ở 06.9 (nhẹ) | ✓ | Đổi thành $h_0$. Chữ này trùng với hàm phân lớp hằng $h_0$ của Ví dụ 06.5 (`bai-tap-ghi-chu.md` §8); hai đối tượng đều là giả thuyết cố định và nằm ở hai tệp khác nhau, nên chấp nhận được. |
| "bổ đề đóng băng" ở 06.1 (nhẹ) | ✓ | |

## 2. Phủ mục tiêu sau sửa

| Mục tiêu | Bài đo | Kết luận |
|---|---|---|
| 1 | 06.1 | Đạt. |
| 2 | 06.9(a), một phần 06.1(b) | Đạt. Điều phối viên đã chấp nhận không thêm bài. |
| 3 | 06.2, 06.8, 06.9 | Đạt. |
| 4 | 06.3(a)–(c), 06.4(c) Bước 5 (hồi quy logistic), 06.5(b)(c) và 06.6(a) (hồi quy ridge), 06.10, 06.11 | Đạt. Cắt 06.3(a) không làm hở mục tiêu nào, vì Bổ đề 06.7 không phải nội dung của mục tiêu. |
| 5 | 06.4, 06.5(a), 06.6, 06.7, 06.8 | Đạt. |

## 3. Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | 06.4(c) Bước 5, dòng 437 | Câu dùng chữ "hệ số" cho cả $\lambda$ lẫn hệ số ổn định. Cụm "ổn định gấp đôi" không nói đại lượng nào gấp đôi. | "Hệ số lớn hơn làm hồi quy logistic ổn định gấp đôi, nhưng số hạng khớp $\lambda B^2/2$ tăng từ $0{,}2$ lên $0{,}4$." | "Tại $\lambda_0=2\lambda^*$, hệ số ổn định giảm một nửa, từ $0{,}2$ xuống $0{,}1$, còn số hạng khớp $\lambda B^2/2$ tăng từ $0{,}2$ lên $0{,}4$; hai tổng là $0{,}4$ và $0{,}5$, như Bước 4." (+8 tiếng) |
| nhẹ | Ghi chú §11, dòng 1082 của `lecture-note.md` (ngoài tệp bài tập) | Danh sách bài tập trong ghi chú lệch với dòng Mục tiêu của 06.4 (dòng 360), dòng này nay ghi "mục tiêu học tập 4, 5". | "4. **Bài tập 06.4** (…): mục tiêu 5." | Sửa thành "mục tiêu 4, 5." Nên thêm vào phần mô tả ở dòng 360 của bài tập: "…, hệ số ổn định của hồi quy logistic, …" (+6). |
| nhẹ | 06.9 lời giải Bước 5, dòng 937 | Sau khi rút gọn, nhãn bước còn nói "so với Mệnh đề 06.5" nhưng nội dung không còn phép so sánh nào. | "**Bước 5: so với Mệnh đề 06.5.** Bước 1 lấy cận dưới đúng theo mọi $h$, nên không cần $h$ đạt $\inf_{\mathcal H}L_D$ và không cần $A(S)\in\mathcal H$." | Đổi nhãn: "**Bước 5: hai giả thiết không cần.**". Hoặc giữ nhãn cũ và viết "Bước 1 làm như Bước 3 của chứng minh Mệnh đề 06.5 cho mọi $h$, rồi lấy cận dưới đúng, nên …" (+8). |
| nhẹ | 06.3(c) Bước 3, dòng 335–339 | Bước trung gian bị ẩn (§7a): từ "đạt cực tiểu tại $\hat w$" chuyển thẳng sang $1{,}3125\cdot\tfrac{64}{441}$, không nói rằng hiệu bằng hệ số dẫn nhân bình phương khoảng cách. Bản cũ còn có câu về đạo hàm bậc hai, nay đã bị bỏ. | "$F_{s,\lambda}(w)=1{,}3125w^2-1{,}25w+0{,}75$ đạt cực tiểu tại $\hat w$, nên" | "… đạt cực tiểu tại $\hat w$, nên $F_{s,\lambda}(w)-F_{s,\lambda}(\hat w)=1{,}3125(w-\hat w)^2$; với $(\hat w'-\hat w)^2=\tfrac{64}{441}$," (+12) |
| nhẹ | 06.8(c) Bước 4, dòng 847 | Câu về không gian vô hạn chiều đã bị cắt để bù chữ. Lời giải nay chỉ nói cỡ mẫu tăng theo $p$, trong khi tên bài khẳng định "Học được mà không có hội tụ đều". Với mỗi $p$ hữu hạn, hội tụ đều vẫn đúng với cỡ mẫu cỡ $\log p$, nên người học không thấy được tên bài nghĩa là gì. | "…, tăng không giới hạn khi $p\to\infty$, còn cận ở (a) không dùng $p$." | Thêm: "Vì vậy, với cùng một cỡ mẫu, cận ở (a) đúng cho mọi $p$, còn hội tụ đều hỏng khi $p$ đủ lớn; đó là nghĩa của tên bài." (+25). Bù chữ: cắt "Phần (d). Với $m_v=\ln(4k/\delta)/\epsilon^2$, số hạng đó bằng $\sqrt2\,\epsilon$." ở Gợi ý 2 của 06.7, vì câu này là đáp số của (d) (−14), và rút "Tổng cỡ mẫu là $k\,\bar m(\epsilon/4)+m_v$." ở dòng 717, vì câu không được dùng ở bước nào sau (−9). |

Văn phong của các đoạn đã đổi và các đoạn liền kề không có vi phạm mới: không có "hãy", "hiển nhiên", câu hỏi tu từ hay đoạn dồn phép tính. Kí hiệu mới ($\bar m$, $W_{r_\lambda}$, $\Omega$, $h_0$, $\Lambda$) được dùng nhất quán trong toàn tệp. Nếu áp dụng cả năm đề xuất, tổng là khoảng 9 938 + 59 − 23 ≈ 9 974 tiếng, dưới trần 10 000.
