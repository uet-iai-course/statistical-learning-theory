# Rà lại sau biên tập vòng 2 — Bài 04 (toán học, mạch, văn phong)

Phát hiện mới: chặn bàn giao 0 · nghiêm trọng 0 · trung bình 0 · nhẹ 6.

**Đầu vào.**
- Diff `scratchpad/lec04-round2.diff` (191 dòng).
- Bản đóng băng `scratchpad/lec04-round2-frozen.md` (1232 dòng), trùng từng byte với `2627-1/materials/lec-04/lecture-note.md` (đã kiểm bằng `cmp`). Số dòng dưới đây theo bản này.
- Báo cáo `reviews/6-ra-lai-toan.md` (R6), báo cáo `reviews/7-ra-lai-mach.md` (R7), mục "Vòng 2" của `bien-tap-vong-1.md`.

Tôi đọc mọi đoạn đã sửa cùng hai đoạn trước và sau mỗi đoạn. Phát hiện về câu chữ viết theo chế độ Detect của `no-ai-slop`.

**Kiểm tra máy.**
- `forward_refs.py` chạy trên bản sao `scratchpad/rev04/fr3/lec-04/lecture-note.md`: **`0 forward references`**.
- `wc -w`: thân bài **11 978** tiếng (không quá 12 000), phụ lục 1 862 tiếng (không quá 3 000).
- Bảng kí hiệu ở §2 (dòng 92–100) giờ là **một bảng Markdown duy nhất**: chín dòng liền nhau, gồm dòng tiêu đề, dòng phân cách và bảy hàng, không có dòng trống chen giữa.
- Không còn câu nào trên 40 tiếng trong thân bài sau phần mục tiêu học tập.
- Grep: không còn "0,0468", "Hiệu tổng thể" hay "dòng cuối".

## 1. Trạng thái các phát hiện của R6 và R7

| Phát hiện | Trạng thái | Dòng | Ghi chú |
|---|---|---|---|
| R6 trung bình: Phụ lục E, Bước 3 | ✓ | 1229 | Đẳng thức giờ gắn vào vế phải của bất đẳng thức thứ nhất, $L_S(\hat h_k)+\mathrm{pen}_k+\tau'$. Số hạng thay cho $\tau$ được nêu rõ. Không còn cách đếm "dòng". Kiểm lại ở mục 2. |
| R6 nhẹ / R7 T1: bảng §2 bị cắt | ✓ | 92–100 | Hàng $\ln$ bị xóa có chủ ý; chấp nhận được. |
| R6 nhẹ: làm tròn $0{,}0468$, $0{,}16443$ | ✓ | 255, 791, 795, 799, 989 | Phép tính in $\approx0{,}04681$; cận được làm tròn lên, in $0{,}0469$ ở ba chỗ. |
| R6 nhẹ: Phụ lục D, câu sau $\square$, thêm (M) | ✓ | 1201 | |
| R6 nhẹ / R7 T3: Ví dụ 04.6, hai nghĩa | ✓ | 463, 471, 481–485 | Đúng chỉ thị của điều phối viên. Bước 2 dùng "độ chệch bình phương" $0{,}25$ và "phương sai" $0{,}24$ của Mệnh đề 04.6. Bước 3–4 và Kết luận chỉ dùng "*… theo nghĩa phân lớp*". Câu dẫn 463 và Bước 4 trích cùng một câu. Còn một chỗ ở §9, xem mới-5. |
| R7 T2: câu nhử dòng 203, hai tên của một hiệu | ✓ | 202 | |
| R7 T4: Ví dụ 04.8, phép tính trong Kết luận | ✓ | 641 | |
| R7 T5: bốn câu dài | ✓ | 481, 771, 897/902, 944 | |
| R7 T6: chủ ngữ của "cố định trước mẫu" | ✓ | 771 | |
| R7 T7: thứ tự câu lý do ở Nhận xét 04.4 | ✓ | 299 | Câu lý do lặp lại lời của gạch đầu dòng 289, xem mới-4. |
| R7 T8: đoạn kết §7 chỉ tóm tắt | ✓ | 907 | Câu còn lại đứng trơ trọi, xem mới-1. |
| R7 T9: "thiết kế ngẫu nhiên" | ✓ | 385 | |
| R7 T10: đếm "dòng" ở Phụ lục E | ✓ | 1229 | |
| R7 T11: câu kết §6 | ✓ | 806 | Chủ ngữ "cận đó" chưa rõ, xem mới-3. |

## 2. Kiểm lại các đoạn đã sửa

**Phụ lục E, Bước 3 (dòng 1229).** Đúng.
- Bước 1 cho $L_S(\hat h_{\hat k})+\mathrm{pen}_{\hat k}\le L_S(\hat h_k)+\mathrm{pen}_k+\tau'$.
- Theo Định nghĩa 04.2, $L_S(\hat h_k)=\inf_{\mathcal H_k}L_S+\operatorname{opt}_S(\hat h_k)$. Đẳng thức được viết là chính xác.
- Trên biến cố $E$, chuỗi bất đẳng thức là $L_D(\hat h_{\hat k})\le L_S(\hat h_{\hat k})+\mathrm{pen}_{\hat k}\le\inf_{\mathcal H_k}L_S+\operatorname{opt}_S(\hat h_k)+\mathrm{pen}_k+\tau'\le L_D(h)+2\,\mathrm{pen}_k+\operatorname{opt}_S(\hat h_k)+\tau'$, với mọi $h\in\mathcal H_k$.
- Lấy cận dưới đúng theo $h$ rồi theo $k$, ta được đúng cận ở dòng 742–747.
- Điều kiện "khi mọi lớp được duyệt" là cần, vì $\hat h_k$ chỉ được định nghĩa cho lớp đã duyệt.

**Phụ lục D, câu sau $\square$ (dòng 1201).** Đúng.
- Phần (a) chỉ cho các lớp có chiều VC hữu hạn.
- Định lý 03.17(b) cho "chiều VC hữu hạn ⇔ học được PAC" dưới (M). Các lớp $\{h:M(\tfrac18,\tfrac18,h)\le k\}$ không nhất thiết thỏa (M), nên vế "khi thêm (M)" là cần.

**Làm tròn $0{,}0469$.** $\sqrt{\ln80/2000}=0{,}0468083$. Phép tính in $\approx0{,}04681$ (đúng); cận làm tròn lên in $0{,}0469$ (đúng quy tắc D). Cùng con số ở dòng 795, 799 và 989.

**Ví dụ 04.3, Bước 1 (dòng 255).** Câu "$\rho_m$ không vượt dạng trực tiếp, $\approx0{,}16443$ …" đúng (dạng trực tiếp $=0{,}1644303$). Bước 2 (dòng 261, 264) vẫn viết "$\le a_2+2\cdot0{,}16443+0{,}01$" với số đã làm tròn xuống. Độ lệch là $6\cdot10^{-7}$; xem mới-6, không bắt buộc sửa.

**Định lý 04.16, giả thiết đo được đã chuyển chỗ (dòng 897, 902).** Nội dung toán học không đổi: (b) vẫn suy từ Hệ quả 04.15. Nhãn **Thuật toán.** nhắc tới "$A_{\mathrm{SRM}}$ của Hệ quả 04.15" trước khi (b) cho họ lớp, và không nói trọng số. Phần (b) cũng mất lời dẫn tới Hệ quả 04.15. Xem mới-2.

**Ví dụ 04.6 (dòng 463–485).** Các con số giữ nguyên và đúng: $0{,}58$; $0{,}90$; $0{,}25$; $0{,}24$; $0{,}81$; $0{,}4$/$0$. Mỗi tên giờ chỉ một nghĩa trong ví dụ. Kết luận đúng ở cả hai nghĩa, vì $A$ có phương sai lớn hơn theo cả hai nghĩa ($0{,}24>0$ và $0{,}4>0$).

**Ví dụ 04.8 (dòng 636–645).** Bước 4: $\sqrt{\ln40\,000/20}=0{,}72790>\tfrac12$, nên độ lệch, vốn không quá $\tfrac12$, luôn nằm trong bán kính. Kết luận không còn chứa phép tính.

**Các ranh giới mục.**
- §6 → §7 (806–810): câu kết thêm việc cận phụ thuộc $\delta$. Câu 834 ("Số hạng phạt của SRM ở §6, nên cả quy tắc, phụ thuộc $\delta$") dùng lại ý này. Câu mở §7 dùng nhu cầu cỡ mẫu. Mạch liền; chỉ có chủ ngữ chưa rõ (mới-3).
- §7 → §8 (904–911): xem mới-1.
- Các đoạn đã sửa khác (202, 299, 385, 771, 944) không phá mạch của hai đoạn trước và sau.

## 3. Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | cuối §7, dòng 907 | Sau lượt cắt (theo đề xuất T8 của tôi), câu kết §7 đứng trơ trọi. Nó nối tiếp câu "Phần (a) được phác thảo ở Phụ lục D." mà không cho biết vì sao lớp này đáng xét. Ngữ cảnh "lớp có chiều VC vô hạn vẫn học được không đều" đã mất. | "Lớp mọi hàm trên một miền vô hạn được xét ở ý thử thách của Bài tập 04.11." | Một câu khoảng 25 tiếng, không thêm khẳng định mới (QĐ dàn ý 10): "Ví dụ 04.11 cho một lớp có chiều VC vô hạn vẫn học được không đều; ý thử thách của Bài tập 04.11 xét lớp mọi hàm trên một miền vô hạn." |
| nhẹ | Định lý 04.16, dòng 897 và 902 | Nhãn **Thuật toán.** dùng "$A_{\mathrm{SRM}}$ của Hệ quả 04.15", nhưng họ lớp chỉ được cho ở (b) phía dưới và trọng số $q_k$ không được nêu. Phần (b) cũng mất lời dẫn tới Hệ quả 04.15, kết quả chứng minh nó. | 897: "ở phần (b), có một cách chọn nghiệm SRM chính xác làm $A_{\mathrm{SRM}}$ của Hệ quả 04.15 thỏa Định nghĩa 01.4". 902: "… mỗi lớp thỏa (M), thì $\mathcal H$ học được không đều." | 897: "ở phần (b), với họ lớp của (b) và một bộ trọng số $q_k>0$, $\sum_kq_k\le1$, có một cách chọn …". 902: thêm "(Hệ quả 04.15)" ở cuối. Thêm khoảng 15 tiếng. |
| nhẹ | câu kết §6, dòng 806 | "Cận đó" có thể chỉ "mốc có phạt" hoặc bất đẳng thức của Định lý 04.11. Thật ra cả số hạng phạt lẫn quy tắc đều phụ thuộc $\delta$, như dòng 834 nói. | "…, và Định lý 04.11 so đầu ra của nó với mốc có phạt; cận đó còn phụ thuộc $\delta$, một đầu vào của quy tắc." | "…; cả số hạng phạt lẫn quy tắc đều phụ thuộc $\delta$, một đầu vào." |
| nhẹ | Nhận xét 04.4, dòng 289 và 299 | Câu lý do mới lặp lại gần nguyên lời gạch đầu dòng ngay trên (lặp trong cùng một khối). | 289: "… phụ thuộc nghiệm ERM được chọn (…) và có thể âm, như phép tính dưới đây." 299: "Vì hiệu này phụ thuộc nghiệm ERM được chọn và có thể âm, học phần dùng …" | 299: "Vì vậy học phần dùng đại lượng thực nghiệm, không âm, $\operatorname{opt}_S$." (bớt 9 tiếng) |
| nhẹ | §9, dòng 985 | Ví dụ 04.6 giờ phân biệt "phương sai" của Mệnh đề 04.6 với "phương sai theo nghĩa phân lớp", nhưng §9 dẫn ví dụ này bằng chữ "phương sai" trơn. Câu vẫn đúng, vì phương sai của $A$ lớn hơn theo cả hai nghĩa, nhưng không khớp tên gọi mà điều phối viên đã chốt. | "với hàm phân lớp, khi dự đoán đa số sai, phương sai lớn hơn có thể cho lỗi nhỏ hơn (Ví dụ 04.6)" | "… phương sai theo nghĩa phân lớp lớn hơn có thể cho lỗi nhỏ hơn …" (thêm 4 tiếng) |
| nhẹ | Ví dụ 04.3, Bước 2, dòng 261 và 264 | Bước 1 giờ viết "$\approx0{,}16443$", nhưng Bước 2 vẫn viết "$\le\ldots2\cdot0{,}16443$" với số đã làm tròn xuống ($0{,}1644303$). Độ lệch $6\cdot10^{-7}$ không đổi kết quả $\approx0{,}3389$ hay $\approx0{,}5698$. | 261: "$\le a_2+2\cdot0{,}16443+0{,}01$" | Không bắt buộc. Có thể viết "$\le a_2+2\rho_m+0{,}01\approx a_2+2\cdot0{,}16443+0{,}01\approx a_2+0{,}3389$". |

Các sửa đề xuất cộng lại chỉ thay đổi khoảng 35 tiếng, nên thân bài vẫn dưới 12 000.

## Kết luận

**Giao được.** Mọi phát hiện của R6 và R7 đã được sửa. Phép tính ở Phụ lục E, câu cuối Phụ lục D, cận $0{,}0469$ và giả thiết đo được của Định lý 04.16 đều đúng. Bảng ở §2 là một bảng duy nhất, `forward_refs.py` báo 0, và thân bài có 11 978 tiếng. Sáu phát hiện nhẹ không chặn bàn giao; nên sửa mới-1 và mới-2 khi còn sửa ghi chú, không cần thêm một vòng rà.
