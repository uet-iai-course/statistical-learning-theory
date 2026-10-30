# Rà lại Bài 03 sau biên tập vòng 2

## Vòng 3 (rà lại kết hợp sau biên tập vòng 2)

**Phạm vi.** Rà lại kết hợp toán, mạch lập luận và văn phong; chỉ đọc. Không sửa tệp nào của repo và không commit. Số dòng theo tệp hiện tại `2627-1/materials/lec-03/lecture-note.md`.

**Đầu vào:**

- `lec03-round2.diff` (109 dòng, 12 khối đổi);
- mục "Vòng 2" trong `bien-tap-vong-1.md`;
- `reviews/6-ra-lai-toan.md`;
- báo cáo rà mạch vòng trước `lec03-review-7-ra-lai-mach.md`.

Các câu sửa được đánh giá theo `no-ai-slop` chế độ Detect và `van-phong.md` §9a.

**Kiểm tra máy đã chạy:**

- `forward_refs.py` trên bản chép `scratchpad/fr3/lec-03/lecture-note.md`: **0 tham chiếu tới trước**.
- Số từ thân bài: **11 981**.
- Quét các dòng dài hơn 60 ký tự xuất hiện hai lần trở lên: không còn dòng nào.
- Tính lại bằng Python dạng trực tiếp của Định lý 03.15(b) tại $m=10^4$, $\delta=0{,}05$:

| $d$ | Cận độ lệch đều | Gấp đôi (cận rủi ro vượt mức) |
|---|---|---|
| $3$ | $0{,}164430$ | $0{,}328861$ |
| $11$ | $0{,}279919$ | $0{,}559839$ |

### Kết luận

**Giao được.** Biên tập viên áp dụng đủ mọi phát hiện của báo cáo 6 và báo cáo 7, và không có câu sửa nào sinh lỗi mới về toán hay mạch lập luận. Còn một điểm nhẹ tùy chọn về làm tròn ở cầu nối, cùng một ghi chú nội bộ về con số trong tệp kế hoạch; ghi chú này không ảnh hưởng nội dung học viên đọc.

**Thống kê:** chặn bàn giao 0; nghiêm trọng 0; trung bình 0; nhẹ 1.

### Trạng thái các phát hiện của báo cáo 6 và báo cáo 7

| Phát hiện | Trạng thái | Bằng chứng (tệp hiện tại) |
|---|---|---|
| R7 S1 (nghiêm trọng) và R6 trung bình: đoạn lặp sau Định lý 03.15 | ✓ | Chỉ còn một đoạn "Khi $d=\infty$ … Khi $d=0$ …" (dòng 572); quét toàn tệp không thấy dòng dài nào lặp. |
| R7 S2 (trung bình): §9 "Mỗi giả thiết … đều được dùng" | ✓ | Dòng 870: "Hai ví dụ cho thấy giả thiết nào không bỏ được. Bỏ (T5), … (Ví dụ 03.8). Bỏ (T1), … (Ví dụ 02.6). Khi $d=\infty$, phần (a) vẫn đúng nhưng không cho thông tin, và lớp ở Ví dụ 03.6 không có tính chất hội tụ đều." Nội dung đúng: chiều VC hữu hạn không còn bị gọi là giả thiết của Định lý 03.15. "Phần (a)" chỉ về Định lý 03.15 ở câu ngay trước. Câu về (M) đã bỏ và không còn lặp dòng 819. |
| R7 nhẹ 1: câu mở §7 | ✓ | Dòng 474: "Để biến ước lượng cuối §6 thành một bảo đảm, chúng ta cần biến cố "$S$ là $\epsilon$-đại diện" (Định nghĩa 02.13) có xác suất ít nhất $1-\delta$ với mọi phân bố khi $m$ đủ lớn." "Ước lượng cuối §6" có thật: dòng 469, "độ lệch đều sẽ có cỡ $\sqrt{d\ln m/m}$". Câu dẫn ngược, không dẫn khối đứng sau. Dòng 496 ("Một lớp hữu hạn … theo Định lý 02.14(c)") không còn lặp câu mở. |
| R7 nhẹ 2: cuối §4 và đầu §5 | ✓ | Dòng 234: "Cả hai chứng minh cận trên dùng thứ tự của các điểm trên đường thẳng." Đúng: Bước 2 của hai chứng minh lấy $x_1<x_2$ và $x_1<x_2<x_3$. Dòng 238: "Trong $\mathbb R^p$ không có thứ tự như vậy, …". Ranh giới nối liền, không lặp. |
| R7 nhẹ 3: dòng 162 | ✓ | "Nếu lớp thực hiện được mọi cách gán nhãn của một tập điểm thì, dù các nhãn quan sát trên tập đó là gì, lớp vẫn có một giả thuyết với rủi ro thực nghiệm bằng $0$." Câu thẳng, đúng §9a. |
| R7 nhẹ 4: câu "Lớp tiếp theo có hai đầu mút" | ✓ | Đã xóa. Khối chứng minh Mệnh đề 03.5 nay đứng ngay trước Mệnh đề 03.6. Mệnh đề 03.6 tự giới thiệu $u\le v$, nên không mất liên kết. |
| R7 nhẹ 5: hình vuông nói lại | ✓ | Dòng 270 bắt đầu bằng "Ý chứng minh: …"; ví dụ hình vuông chỉ còn ở dòng 255. |
| R7 nhẹ 6: "hai số trùng nhau" ba lần | ✓ | Câu cuối Nhận xét 03.10 chỉ còn "Số tham số không cho cận trên, cũng không cho cận dưới, của chiều VC." |
| R7 nhẹ 7: "tổ hợp nhãn" và "cách gán nhãn" | ✓ | Dòng 124: "…, tức một tổ hợp nhãn $0$, $1$ trên các điểm của $C$." |
| R7 nhẹ 8 và R6 nhẹ: số ở cầu nối | ✓ (xem nhẹ V3-1) | Dòng 915: "bằng hai lần cận độ lệch đều (Hệ quả 03.16(a)). Ở $m=10^4$, cận độ lệch đều tăng từ $0{,}164$ lên $0{,}280$ (Ví dụ 03.7), nên cận cho rủi ro vượt mức tăng từ $0{,}329$ lên $0{,}560$." Đúng: $2\cdot0{,}164430=0{,}3289$ và $2\cdot0{,}279919=0{,}5598$. Dẫn Hệ quả 03.16(a) đúng: $L_D(\hat h)-\inf L_D\le2\rho_m$. Đối tượng so sánh vẫn ghi rõ; không có nội dung SRM. |
| R6 nhẹ: Ví dụ 03.9, dấu của đạo hàm | ✓ | Dòng 730: "…$<0$, vì $\ln\tfrac{2em}d\ge\ln(2e)>1$ khi $m\ge d$ và $c>0$." Lập luận đúng: $m\ge d$ cho $2em/d\ge2e$, nên $d-d\ln\tfrac{2em}d<0$; trừ thêm $c>0$ thì tử số vẫn âm. |
| R6 nhẹ: §9, cận dưới khả thực | ✓ | Dòng 872: "Định lý 03.19(b) chỉ cho cận dưới cỡ $(d+\ln(1/\delta))/\epsilon$". Khớp phát biểu ở dòng 853. |

### Mạch lập luận và văn phong ở các chỗ đổi

- **Cuối §4 và đầu §5 (234/238).** Câu cuối §4 nêu giới hạn của phương pháp: hai chứng minh dựa vào thứ tự trên đường thẳng. Câu đầu §5 lấy đúng giới hạn đó làm nhu cầu, đúng `van-phong.md` §2 và §8.
- **Cuối §6 và đầu §7 (469/474).** Ước lượng cuối §6 dẫn sang nhu cầu một tính chất của lớp. Ngay sau đó là Định nghĩa 03.13, rồi dòng 496 cho trường hợp lớp hữu hạn và Ví dụ 03.6 cho phản ví dụ. Thứ tự đã kiểm ở vòng trước được giữ nguyên.
- **§9 (870–872).** Hai đoạn cuối nêu vai trò của giả thiết và mắt xích khả thực. Không còn con số hay câu nào lặp với §8 hoặc dòng 819.
- **Detect.** Các câu đổi không có từ cấm, câu hỏi tu từ, dấu hai chấm kiểu lộ ý, lời đánh giá hay câu kết kiểu châm ngôn. Câu dài nhất là dòng 474, khoảng 35 tiếng, dưới ngưỡng 40.

### Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | V3-1 · dòng 915 (cầu nối) | Người đọc gấp đôi số đã làm tròn $0{,}164$ sẽ được $0{,}328$, lệch với $0{,}329$ in trong câu. $0{,}329$ đúng theo giá trị chưa làm tròn: $0{,}1644$ ở Ví dụ 03.7 Bước 2, gấp đôi là $0{,}3289$. Không sai, chỉ có thể gây thắc mắc. | "cận độ lệch đều tăng từ $0{,}164$ lên $0{,}280$ (Ví dụ 03.7), nên cận cho rủi ro vượt mức tăng từ $0{,}329$ lên $0{,}560$." | Tùy chọn: viết "từ khoảng $0{,}33$ lên khoảng $0{,}56$", hoặc giữ nguyên. Không thay đổi số từ. |

**Ghi chú nội bộ (không phải phát hiện về nội dung học viên đọc).** Mục "Con số mới" của "Vòng 2" ghi $0{,}27986$ và $0{,}55973$ cho $d=11$. Tính lại cho $0{,}279919$ và $0{,}559839$. Hai số làm tròn in trong ghi chú bài giảng ($0{,}280$ và $0{,}560$) vẫn đúng. Nên sửa con số trong `bien-tap-vong-1.md` hoặc `review-log.md` khi ghi nhật ký.
