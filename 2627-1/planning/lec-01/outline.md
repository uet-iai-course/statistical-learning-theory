# Dàn ý Bài 01 — Mô hình học: rủi ro, tối thiểu hóa rủi ro thực nghiệm và học PAC

> **Quyết định của điều phối viên (2026-10-30), ưu tiên hơn mọi chỗ khác trong dàn ý:**
> 1. **Đánh số theo phương án A**: một bộ đếm chung tăng theo thứ tự đọc cho định nghĩa, mệnh đề, định lý, bổ đề, hệ quả, nhận xét và thuật toán; ví dụ và bài tập có bộ đếm riêng. Người viết dùng bảng ánh xạ phương án A ở mục 2 và giữ một dòng đối chiếu số của blueprint trong `outline.md` (không đưa vào ghi chú).
> 2. Chấp nhận các kí hiệu mới ở mục 9: $\eta(x)$ (luôn có đối số, khác $\eta_t$ luôn có chỉ số), $h_{\mathrm{Bayes}}$, $L_D^{\mathrm{Bayes}}$, $\mathcal M_{\mathcal X}$, $\epsilon_{\mathrm{opt}}$, $D_{\mathcal X}$, $A(S;\xi)$; đã thêm vào `ky-hieu.md`.
> 3. Tên định lý: "không có bữa trưa miễn phí" (theo `thuat-ngu.md`).
> 4. Dùng "ghi nhớ" (hàm phân lớp ghi nhớ), không dùng "học thuộc"; thẻ Bài 01 trên trang chỉ mục đã sửa theo.
> 5. Chi phí $(c_{FP},c_{FN})=(1,4)$ là ví dụ minh họa do học phần dựng; ghi chú nói rõ điều này.
> 6. $m_{\mathcal H}(\epsilon,\delta)$ định nghĩa theo từng cặp $(\epsilon,\delta)$ là giá trị nhỏ nhất của $m_A$ trên mọi thuật toán; một nhận xét nói rõ khác biệt với định nghĩa học được PAC (một thuật toán dùng cho mọi $\epsilon,\delta$) và với cách nói "hàm nhỏ nhất" của UML.
> 7. Chấp nhận Hệ quả 01.4(b).
> 8–9. Chấp nhận vị trí thuật toán trong §5 và cách chia tài liệu đọc trước/sau buổi học.
> 10. Các thuật ngữ mới ở mục 8 đã được thêm vào `thuat-ngu.md`.
> 11. Điều phối viên đã tính lại mọi con số đánh dấu †: tất cả đúng.
> 12. **Số hiệu cuối cùng trong ghi chú** (sau vòng biên tập, 2026-10-30; các bảng bên dưới còn dùng số cũ, bảng này thay thế): Định nghĩa 01.1 rủi ro kì vọng; Nhận xét 01.2; Định nghĩa 01.3 phân bố có rủi ro hữu hạn; Định nghĩa 01.4 rủi ro thực nghiệm; **Mệnh đề 01.5 = blueprint Prop 1.1**; Nhận xét 01.6; Định nghĩa 01.7 thuật toán học; Nhận xét 01.8; Định nghĩa 01.9 khoảng cách tổng quát hóa; Định nghĩa 01.10 ERM; Nhận xét 01.11; Định nghĩa 01.12 ERM xấp xỉ; Thuật toán 01.13; Định nghĩa 01.14 thuật toán ghi nhớ; **Mệnh đề 01.15 = Prop 1.2**; Định nghĩa 01.16 tính khả thực; Nhận xét 01.17; Định nghĩa 01.18 học PAC khả thực; Nhận xét 01.19; Định nghĩa 01.20 độ phức tạp mẫu; Nhận xét 01.21; Định nghĩa 01.22 rủi ro Bayes; **Mệnh đề 01.23 = Prop 1.3**; Định nghĩa 01.24 rủi ro vượt mức; Định nghĩa 01.25 học PAC bất khả tri; Nhận xét 01.26, 01.27; Định nghĩa 01.28 cận tổng quát hóa cho mọi thuật toán ERM; **Hệ quả 01.29 = Corollary**; Nhận xét 01.30. Ví dụ 01.1–01.10 (01.6 và 01.7 đổi chỗ so với bản nháp); Bài tập 01.1–01.11 không đổi.
> 13. **Sau duyệt thí điểm vòng 1 (2026-10-30):** ghi chú được sắp xếp lại theo quy tắc "định nghĩa trước khi dùng", thêm Định nghĩa 01.5 (Bài toán học thống kê), bỏ $\xi$ (thuật toán tất định $A(S)$). Bảng đổi số hiệu cũ → mới ở `reorder-plan.md` §4 thay thế mục 12 cho các số đã đổi (Prop 1.1 → Mệnh đề 01.7; Prop 1.2 → Mệnh đề 01.15; Prop 1.3 → Mệnh đề 01.23; Corollary → Hệ quả 01.29).

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-10-30 bởi tác tử lập kế hoạch; chờ điều phối viên duyệt. Dàn ý này ràng buộc người viết ghi chú (`materials/lec-01/lecture-note.md`) và người viết bài tập (`materials/lec-01/exercises.md`).

**Căn cứ, theo thứ tự ưu tiên:** `sources/blueprint.md` mục A, E và "Lecture 1"; `planning/course-plan.md` mục 3–5; quyết định 1–11 của điều phối viên trong `planning/lec-01/review-log.md`; `planning/lec-01/source-analysis.md` (mọi con số của ví dụ xuyên suốt lấy từ mục 4 của báo cáo này); `planning/ky-hieu.md`; `planning/thuat-ngu.md` (quyết định của người dùng ở mục 14); `planning/van-phong.md`; mẫu `materials/_templates/lecture-note.md` và `exercises.md`. Tác tử lập kế hoạch đã đọc lại UML tr. PDF 41–44, 46, 49–53 để kiểm tra phát biểu Định nghĩa 3.1, 3.3, 3.4, Nhận xét 3.1, 3.2 và đề các bài tập 2.1, 3.1–3.9; không chép câu chữ.

**Con số mới.** Một số con số trong dàn ý không có trong `source-analysis.md` mà do tác tử lập kế hoạch tính (đánh dấu † ở nơi xuất hiện). Điều phối viên cần tính lại trước khi duyệt; danh sách đầy đủ ở mục 11.

## 1. Câu hỏi trung tâm, luận điểm và mục tiêu học tập

**Câu hỏi trung tâm.** Học nghĩa là gì: khi nào một hàm dự đoán chọn ra từ một mẫu ngẫu nhiên được xem là đã học được, và một bảo đảm học phải được phát biểu chính xác ra sao?

**Luận điểm (một câu).** Học là chọn từ mẫu $S\sim D^m$ một hàm dự đoán có rủi ro kì vọng không vượt quá mức tốt nhất trong một lớp giả thuyết chọn trước cộng $\epsilon$, với xác suất không thấp hơn $1-\delta$ theo mẫu, khi cỡ mẫu vượt một ngưỡng không phụ thuộc phân bố; rủi ro thực nghiệm nhỏ tự nó không bảo đảm điều đó.

**Câu hỏi mở đầu (blueprint 1.1).** Hai hàm phân lớp khớp mọi quan sát huấn luyện. Vì sao có thể chỉ một trong hai dự đoán đúng các quan sát mới?

**Mục tiêu học tập** (đưa vào ghi chú gần nguyên văn, mỗi mục là một năng lực kiểm tra được):

1. Phát biểu đầy đủ một bài toán học ($\mathcal X$, $\mathcal Y$, $D$, $S$, $\mathcal H$, $\ell$, $A$, đối tượng so sánh) và chỉ ra đại lượng nào cố định, đại lượng nào ngẫu nhiên và ngẫu nhiên theo phân bố nào.
2. Tính rủi ro kì vọng, rủi ro thực nghiệm, tập nghiệm ERM, rủi ro Bayes và rủi ro vượt mức trong một bài toán hữu hạn; xác định ngưỡng tối ưu khi hàm lỗi có chi phí bất đối xứng.
3. Chứng minh rủi ro thực nghiệm của một giả thuyết cố định là ước lượng không chệch của rủi ro kì vọng, và chỉ ra bước hỏng khi giả thuyết được chọn theo mẫu.
4. Viết định nghĩa học PAC trong trường hợp khả thực và bất khả tri với đúng thứ tự lượng từ; phân biệt $\epsilon$ với $\delta$ và độ phức tạp mẫu của một thuật toán với độ phức tạp mẫu của một lớp.
5. Dựng phản ví dụ ERM ghi nhớ, chứng minh nó có rủi ro thực nghiệm bằng 0 và rủi ro kì vọng bằng 1, và giải thích vì sao cần thiên kiến quy nạp hoặc kiểm soát thuật toán.

## 2. Quy ước đánh số

**Quyết định của dàn ý (chờ điều phối viên xác nhận, mục 12, điểm mở 1).** `CLAUDE.md` của học phần và `course-plan.md` mục 3 yêu cầu đồng thời (a) một bộ đếm chung cho định nghĩa và kết quả, (b) giữ số của blueprint. Ở Bài 01 hai yêu cầu xung đột: mọi định nghĩa phải đứng trước Mệnh đề 1.1 của blueprint. Dàn ý chọn **phương án B** theo đúng brief: bốn kết quả giữ số blueprint 01.1–01.4; mọi khối khác trong bộ đếm chung (định nghĩa, nhận xét, thuật toán) đánh số tiếp từ 01.5 theo thứ tự xuất hiện. Hệ quả: số trong ghi chú không tăng đơn điệu (Định nghĩa 01.7 đứng trước Mệnh đề 01.1). Cột cuối bảng dưới cho **phương án A** (một bộ đếm đơn điệu theo thứ tự đọc, kết quả mất số blueprint) để điều phối viên đổi được ngay nếu muốn.

Ví dụ có bộ đếm riêng (Ví dụ 01.1–01.10); bài tập có bộ đếm riêng (Bài tập 01.1–01.11). Khối `application` (một khối duy nhất) không đánh số. Blueprint không đánh số hệ quả; dàn ý đặt là Hệ quả 01.4 theo brief.

| Số (phương án B) | Loại khối | Tên (cụm danh từ) | Mục | Độ sâu | Phương án A |
|---|---|---|---|---|---|
| 01.5 | definition | Hàm lỗi và rủi ro kì vọng | §4 | — | 01.1 |
| 01.6 | remark | Tính khả tích khi hàm lỗi không bị chặn | §4 | — | 01.2 |
| 01.7 | definition | Rủi ro thực nghiệm | §4 | — | 01.3 |
| **01.1** | proposition | Tính không chệch của rủi ro thực nghiệm với giả thuyết cố định | §4 | chứng minh đầy đủ | 01.4 |
| 01.8 | remark | Giả thuyết chọn theo mẫu | §4 | — | 01.5 |
| 01.9 | definition | Thuật toán học | §5 | — | 01.6 |
| 01.10 | remark | Nguồn ngẫu nhiên nội tại của thuật toán học | §5 | — | 01.7 |
| 01.11 | definition | Khoảng cách tổng quát hóa | §5 | — | 01.8 |
| 01.12 | definition | Tối thiểu hóa rủi ro thực nghiệm | §5 | — | 01.9 |
| 01.13 | remark | Sự tồn tại nghiệm ERM và quy tắc chọn khi bằng nhau | §5 | — | 01.10 |
| 01.14 | algorithm | ERM cho lớp hàm ngưỡng trên tập đầu vào hữu hạn | §5 | — | 01.11 |
| 01.15 | definition | ERM xấp xỉ | §5 | — | 01.12 |
| **01.2** | proposition | Nghiệm ERM ghi nhớ có rủi ro kì vọng bằng 1 | §5 | chứng minh đầy đủ | 01.13 |
| 01.16 | definition | Giả thiết khả thực | §6 | — | 01.14 |
| 01.17 | remark | Khả thực là tính chất của cặp $(D,\mathcal H)$ | §6 | — | 01.15 |
| 01.18 | definition | Học PAC trong trường hợp khả thực | §6 | — | 01.16 |
| 01.19 | remark | Độ tin cậy lấy theo mẫu, không phải xác suất hậu nghiệm | §6 | — | 01.17 |
| 01.20 | definition | Độ phức tạp mẫu | §6 | — | 01.18 |
| 01.21 | remark | Độ phức tạp mẫu của thuật toán và của lớp | §6 | — | 01.19 |
| **01.3** | proposition | Quy tắc Bayes cho hàm lỗi 0–1 và hàm lỗi có trọng số | §7 | đọc thêm (có chứng minh ngắn) | 01.20 |
| 01.22 | definition | Rủi ro vượt mức | §7 | — | 01.21 |
| 01.23 | definition | Học PAC bất khả tri | §7 | — | 01.22 |
| 01.24 | remark | Cận dưới đúng thay cho giá trị nhỏ nhất | §7 | — | 01.23 |
| 01.25 | remark | Học đúng lớp và học ngoài lớp | §7 | — | 01.24 |
| 01.26 | remark | Tính đo được | §7 | — | 01.25 |
| **01.4** | corollary | Rủi ro thực nghiệm nhỏ không đủ làm bảo đảm học | §8 | chứng minh đầy đủ | 01.26 |
| 01.27 | remark | Phản ví dụ ghi nhớ và định lý không có bữa trưa miễn phí | §8 | — | 01.27 |

Tiêu đề khối theo mẫu: `::: proposition Mệnh đề 01.1 (Tính không chệch của rủi ro thực nghiệm với giả thuyết cố định) — chứng minh đầy đủ`; `::: definition Định nghĩa 01.5 (Hàm lỗi và rủi ro kì vọng)`; `::: remark Nhận xét 01.6 (Tính khả tích khi hàm lỗi không bị chặn)`. Chứng minh: `::: proof Chứng minh Mệnh đề 01.1`.

**Danh sách ví dụ** (bộ đếm riêng):

| Số | Tên | Mục | Ví dụ xuyên suốt dùng |
|---|---|---|---|
| Ví dụ 01.1 | Sàng lọc theo ngưỡng trên năm mức đo | §3 | thiết lập cả hai bản |
| Ví dụ 01.2 | Phân bố đều trên $[0,1]$ với nhãn hằng | §3 | thiết lập phản ví dụ ghi nhớ |
| (application, không số) | Sàng lọc y tế với chi phí bất đối xứng | §3 | ứng dụng thực tế |
| Ví dụ 01.3 | Rủi ro kì vọng của các hàm ngưỡng dưới hai hàm lỗi | §4 | bản bất khả tri |
| Ví dụ 01.4 | Hồi quy tuyến tính với hàm lỗi bình phương | §4 | — |
| Ví dụ 01.5 | Rủi ro thực nghiệm trên một mẫu cỡ 6 | §4 | bản bất khả tri, mẫu $S_\eta$ |
| Ví dụ 01.6 | Các nghiệm ERM trên mẫu sàng lọc | §5 | bản bất khả tri, mẫu $S_\eta$ |
| Ví dụ 01.7 | Cận dưới đúng không đạt được của rủi ro thực nghiệm | §5 | — |
| Ví dụ 01.8 | Xác suất thất bại và cỡ mẫu cho một phân bố khả thực | §6 | bản khả thực |
| Ví dụ 01.9 | Quy tắc Bayes trong ví dụ sàng lọc | §7 | bản bất khả tri, hai hàm lỗi |
| Ví dụ 01.10 | Hàm phân lớp ghi nhớ khi phân bố có nguyên tử | §8 | bản khả thực |

## 3. Ví dụ xuyên suốt và vị trí các con số

### 3.1 Sàng lọc theo ngưỡng (ví dụ tính tay)

Thiết lập chung (Ví dụ 01.1, §3 của ghi chú): $\mathcal X=\{1,2,3,4,5\}$ là năm mức của một chỉ số đo; $\mathcal Y=\{0,1\}$, $Y=1$ là có bệnh; phân bố biên $D_{\mathcal X}$ đều, mỗi mức $0{,}2$; $\mathcal H=\{h_t:t\in\{1,\ldots,6\}\}$ với $h_t(x)=\mathbb 1[x\ge t]$ ($h_1\equiv1$, $h_6\equiv0$; mọi ngưỡng thực khác cho một trong sáu hàm này trên $\mathcal X$). Hàm lỗi: $\ell_{0\text{-}1}$, và ở các chỗ đánh dấu, hàm lỗi có trọng số $\ell_c$ với $(c_{FP},c_{FN})=(1,4)$†. Ghi chú nói rõ đây là phân bố giả định để minh họa, không phải số liệu lâm sàng.

**Bản bất khả tri** (phân bố $D_\eta$): $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$ tại $x=1,\ldots,5$. Mẫu cụ thể $S_\eta=((1,0),(2,0),(2,1),(3,1),(4,0),(5,1))$, $m=6$.

**Bản khả thực** (phân bố $D_f$): $Y=f(X)$ với $f=h_3=\mathbb 1[x\ge3]$. Mẫu cụ thể dùng ở câu hỏi mở đầu: $S_f=((1,0),(2,0),(4,1),(5,1))$, $m=4$†. Hai thuật toán ERM: $A_{\max}$ chọn $\hat t$ là quan sát dương nhỏ nhất (6 nếu không có), $L_{D_f}=0{,}2(\hat t-3)$; $A_{\min}$ chọn $\hat t$ là quan sát âm lớn nhất cộng 1 (1 nếu không có), $L_{D_f}=0{,}2(3-\hat t)$.

| Con số | Giá trị | Xuất hiện ở |
|---|---|---|
| Hai giả thuyết khớp $S_f$: $h_3$, $h_4$; $L_{D_f}(h_3)=0$, $L_{D_f}(h_4)=0{,}2$† | — | Câu hỏi mở đầu; trả lời ở §5 (Ví dụ 01.6 nhắc lại) và §11 |
| Rủi ro có trọng số của $h_4$ dưới $D_f$: $4\cdot0{,}2=0{,}8$† | cùng hàm dự đoán, hàm lỗi khác | Câu hỏi mở đầu (một câu), Ví dụ 01.3 |
| $L_{D_\eta}(h_t)$, $t=1..6$ | $0{,}52;\ 0{,}32;\ \mathbf{0{,}22};\ 0{,}32;\ 0{,}28;\ 0{,}48$ | Ví dụ 01.3 (bảng), Phụ lục C (cách tính) |
| $L^{c}_{D_\eta}(h_t)$, $t=1..6$, $(c_{FP},c_{FN})=(1,4)$† | $0{,}52;\ \mathbf{0{,}32};\ 0{,}37;\ 0{,}92;\ 1{,}12;\ 1{,}92$ | Ví dụ 01.3 (cột thứ hai), Ví dụ 01.9 |
| $L_{S_\eta}(h_t)$, $t=1..6$ | $\tfrac12;\ \tfrac13;\ \tfrac13;\ \tfrac12;\ \tfrac13;\ \tfrac12$ | Ví dụ 01.5 |
| $L_{S_\eta}(h_3)=\tfrac13\ne0{,}22=L_{D_\eta}(h_3)=\mathbb E_S L_S(h_3)$ | — | Ví dụ 01.5, ngay sau Mệnh đề 01.1 |
| Tập nghiệm ERM trên $S_\eta$: $\{h_2,h_3,h_5\}$; $L_{D_\eta}$ = 0,32; 0,22; 0,28; rủi ro vượt mức so với $\mathcal H$: 0,10; 0; 0,06 | — | Ví dụ 01.6 |
| Chọn ngẫu nhiên đều trong $\{h_2,h_3,h_5\}$: $\mathbb E_\xi L_{D_\eta}=0{,}82/3\approx0{,}273$; $\Pr_\xi[\text{rủi ro vượt mức}\le0{,}05]=1/3$† | — | Nhận xét 01.10 |
| Trên cả 32 hàm $\mathcal X\to\{0,1\}$, $\min L_{S_\eta}=1/6$ (tại $x=2$ có cả hai nhãn) | — | Nhận xét 01.13 (tập nghiệm ERM không rỗng nhưng $\min$ có thể dương) |
| Hàm Bayes (0–1): $\mathbb 1[x\in\{3,5\}]$, $L^{\mathrm{Bayes}}_{D_\eta}=0{,}18$; $\inf_{\mathcal H}L_{D_\eta}-L^{\mathrm{Bayes}}_{D_\eta}=0{,}04$ | — | Ví dụ 01.9; nhắc lại ở Định nghĩa 01.22 và §8 (thiên kiến quy nạp có giá) |
| Hàm Bayes có trọng số: ngưỡng $c_{FP}/(c_{FP}+c_{FN})=1/5$, dự đoán 1 trên $\{2,3,4,5\}$, tức $h_2$; rủi ro Bayes có trọng số $0{,}32$; $h_3$ có rủi ro vượt mức có trọng số $0{,}05$† | — | Ví dụ 01.9 |
| Rủi ro vượt mức của $h_2$ (0–1): $0{,}10$ so với $\mathcal H$, $0{,}14$ so với rủi ro Bayes | — | Định nghĩa 01.22 (ví dụ) |
| $D_\eta$ không khả thực với mọi $\mathcal H$: tại $x=2$ mọi $h$ sai với xác suất ít nhất $0{,}2\cdot\tfrac14=0{,}05$† | — | Nhận xét 01.17 |
| $\Pr[L_{D_f}(A_{\max}(S))>0]=0{,}8^m$; $0{,}8^{13}=0{,}0550$, $0{,}8^{14}=0{,}0440$; cùng giá trị cho $A_{\min}$ (biến cố $2\notin S$) | ngưỡng $m\ge14$ cho $\epsilon=0{,}1$, $\delta=0{,}05$ | Ví dụ 01.8 |
| $\Pr[L_{D_f}(A_{\max}(S))>0{,}25]=0{,}6^m$; $0{,}6^5=0{,}0778$, $0{,}6^6=0{,}0467$ | ngưỡng $m\ge6$ cho $\epsilon=0{,}25$, $\delta=0{,}05$ | Ví dụ 01.8 |
| $\mathbb E_S L_{D_f}(A_{\max}(S))=0{,}2(0{,}8^m+0{,}6^m+0{,}4^m)\approx0{,}0227$ tại $m=10$; $\mathbb E_S L_S(A_{\max}(S))=0$ | — | Ví dụ 01.8; Nhận xét 01.8 (dẫn tới); Phụ lục C |
| Hàm ghi nhớ trên $\mathcal X=\{1..5\}$ dưới $D_f$: $\mathbb E_S L_{D_f}=0{,}6\cdot0{,}8^m\approx0{,}0644$ tại $m=10$† | so với $0{,}0227$ của $A_{\max}$ | Ví dụ 01.10 |

**Bắt buộc nói rõ ở Ví dụ 01.8 và ở §9:** các cỡ mẫu 14 và 6 là cỡ mẫu đủ cho **riêng thuật toán $A_{\max}$ và riêng phân bố $D_f$**. Chúng không phải độ phức tạp mẫu theo Định nghĩa 01.20, vì định nghĩa đòi một ngưỡng đúng cho mọi phân bố khả thực. Chuyển khối lượng của điểm $x=3$ sang giá trị khác làm thay đổi các con số này; cận đúng cho mọi phân bố là việc của Bài 02 (và Bài tập 01.9 cho một lớp cùng cấu trúc).

### 3.2 Phản ví dụ ghi nhớ một chiều

Ví dụ 01.2 (§3): $\mathcal X=[0,1]$ với σ-đại số Borel, $\mathcal Y=\{0,1\}$, $X\sim U[0,1]$, $Y=1$ chắc chắn; $\mathcal H=\mathcal M_{\mathcal X}$ là mọi hàm phân lớp đo được $[0,1]\to\{0,1\}$; hàm lỗi 0–1. Dùng ở Mệnh đề 01.2 (§5), Hệ quả 01.4 (§8), Nhận xét 01.8 (nhắc $\mathbb E_SL_S=0$, $\mathbb E_SL_D=1$), Nhận xét 01.27. Ví dụ 01.10 (§8) là phép thử bỏ giả thiết "phân bố không có nguyên tử" trên chính bản khả thực của ví dụ sàng lọc.

### 3.3 Ứng dụng thực tế: sàng lọc y tế với chi phí bất đối xứng

Khối `::: application Sàng lọc y tế với chi phí bất đối xứng` ở §3: $\mathcal X\subseteq\mathbb R^p$ là véc-tơ chỉ số đo của một người, $Y\in\{0,1\}$ là tình trạng bệnh, nhãn có nhiễu (cùng chỉ số có thể ứng với cả hai tình trạng), nên không giả sử khả thực. Âm tính giả (false negative) và dương tính giả (false positive) có chi phí $c_{FN}$, $c_{FP}$ khác nhau; hàm lỗi
$$
\ell_c(h,(x,y))=c_{FN}\,\mathbb 1[y=1,\ h(x)=0]+c_{FP}\,\mathbb 1[y=0,\ h(x)=1],
$$
nhận giá trị trong $\{0,c_{FP},c_{FN}\}$. Khối này nêu điểm chính của blueprint: hàm dự đoán $h$ và hàm lỗi dùng để đánh giá nó là hai lựa chọn tách rời. Không đưa số chi phí thực tế (không có nguồn); chỉ dùng $(1,4)$ trong ví dụ tính tay và gọi đó là giá trị minh họa. Ngưỡng tối ưu $c_{FP}/(c_{FP}+c_{FN})$ được chứng minh ở Mệnh đề 01.3(b); với $c_{FP}=c_{FN}$ ngưỡng là $1/2$, với $(1,4)$ là $1/5$.

## 4. Bản đồ các mục của ghi chú

Tiêu đề theo mẫu. Thành phần 7–11 của blueprint mục A nằm xen trong các mục nội dung §4–§8. Mỗi mục ghi: mục đích; đầu vào; đầu ra; nội dung; ví dụ xuyên suốt; nguồn UML.

### `# Bài 01 — Mô hình học: rủi ro, tối thiểu hóa rủi ro thực nghiệm và học PAC` và đoạn dẫn

Một đoạn 3–4 câu: câu hỏi trung tâm; bài không kế thừa kết quả nào; bài đặt khung ($L_D$, $L_S$, ERM, PAC) mà Bài 02–10 dùng. Không viết "Bài này…" làm chủ ngữ theo kiểu dẫn đường; mở bằng bài toán.

### Thành phần 1 — `## Câu hỏi mở đầu`

- **Mục đích:** đặt hiện tượng cần giải thích; tách hàm dự đoán khỏi hàm lỗi.
- **Nội dung:** bối cảnh sàng lọc; mẫu $S_f$; hai hàm $h_3$, $h_4$ cùng có rủi ro thực nghiệm 0 nhưng rủi ro kì vọng 0 và 0,2 dưới $D_f$; $h_4$ bỏ sót mức $x=3$ (âm tính giả), và nếu âm tính giả đắt gấp bốn thì cùng $h_4$ có rủi ro 0,8. **Câu trả lời hấp dẫn nhưng sai:** "hai hàm cùng khớp mọi quan sát huấn luyện nên tốt như nhau; rủi ro thực nghiệm bằng 0 nghĩa là dự đoán đúng trên quan sát mới". Lý do sai: $S_f$ không chứa $x=3$, nơi hai hàm khác nhau; mẫu không phân biệt được chúng. Một câu nhắc trường hợp cực đoan (hàm ghi nhớ, §5).
- **Đầu ra:** câu hỏi được trả lời ở §5 (quy tắc chọn khi bằng nhau, thiên kiến quy nạp), §6 (xác suất mẫu bỏ sót $x=3$ là $0{,}8^m$) và §11.
- **UML:** không có tương ứng (ví dụ của học phần); UML §2.1 dùng ví dụ đu đủ, không dùng.

### Thành phần 2 — `## Mục tiêu học tập`

Năm mục ở mục 1 của dàn ý.

### Thành phần 3 — `## Kiến thức tiên quyết`

- Kì vọng và tính tuyến tính của kì vọng (không cần độc lập); xác suất có điều kiện; kì vọng có điều kiện và tính chất tháp (chỉ cho Mệnh đề 01.3, đọc thêm); hàm, tập hợp, hàm chỉ thị; phân bố đều trên $[0,1]$; bất đẳng thức $1-x\le e^{-x}$ (chỉ dùng trong bài tập). Không cần bất đẳng thức tập trung.
- **Câu hỏi ôn nhanh** (đáp số trong một khối `hint`): (1) $X\sim U[0,1]$: tính $\Pr(X\in\{0{,}1;\,0{,}5;\,0{,}9\})$ (đáp số 0). (2) $Z_1=Z_2$ có cùng phân bố với $\mathbb E Z_1=\mu$: tính $\mathbb E[(Z_1+Z_2)/2]$ (đáp số $\mu$, không cần độc lập). (3) Rút $m$ lần độc lập, đều trên $\{1,\ldots,5\}$: xác suất không lần nào ra 3 (đáp số $0{,}8^m$). Ba câu này chuẩn bị đúng ba bước then chốt của Mệnh đề 01.2, Mệnh đề 01.1 và Ví dụ 01.8.

### Thành phần 4 — `## 1. Thiết lập bài toán`

- **Mục đích:** liệt kê các thành phần của một bài toán học trước mọi định nghĩa.
- **Nội dung (văn xuôi và một bảng):** tập đầu vào $\mathcal X$, tập nhãn $\mathcal Y$, $\mathcal Z=\mathcal X\times\mathcal Y$; phân bố dữ liệu $D$ trên $\mathcal Z$ (mô hình phân bố đồng thời ngay từ đầu, quyết định 1; trường hợp nhãn tất định $Y=f(X)$ là trường hợp riêng, $f$ là hàm gán nhãn); mẫu huấn luyện $S=(Z_1,\ldots,Z_m)\sim D^m$ (là một dãy, có thể lặp); lớp giả thuyết $\mathcal H$ cố định trước khi lấy mẫu; hàm lỗi $\ell$; thuật toán học $A$ và hàm dự đoán học được $A(S)$; mục tiêu (rủi ro kì vọng nhỏ); đối tượng so sánh ($\inf_{\mathcal H}L_D$; rủi ro Bayes là mốc tham chiếu khác); tài nguyên (cỡ mẫu $m$; thời gian tính chưa xét). **Điều thuật toán học không thấy:** $D$, $\eta$, $f$, $L_D$.
- **Bảng cố định và ngẫu nhiên** (bắt buộc): cố định: $D$, $\mathcal H$, $\ell$, $A$ (như một quy tắc), mỗi $h\in\mathcal H$, $L_D(h)$ với $h$ cố định, $\inf_{\mathcal H}L_D$; ngẫu nhiên theo $D^m$: $S$, $L_S(h)$; ngẫu nhiên theo $S$ và $\xi$: $A(S;\xi)$, $L_D(A(S;\xi))$, $L_S(A(S;\xi))$. Bảng này là đáp án của câu hỏi cuối buổi.
- **Đầu ra:** các đối tượng mà §2 đặt kí hiệu và §4 định nghĩa.
- **UML:** §2.1 (danh sách thành phần, điều người học không thấy), §3.2.1 (phân bố đồng thời).

### Thành phần 5 — `## 2. Kí hiệu và giả thiết`

- **Bảng kí hiệu** chỉ gồm kí hiệu dùng trong bài (mục 10 của dàn ý), kí hiệu chung theo `ky-hieu.md`.
- **Giả thiết thống kê:** (T1) $S\sim D^m$, độc lập cùng phân bố (independent and identically distributed, i.i.d.); Mệnh đề 01.1 chỉ cần cùng phân bố biên. (T2) $\ell\ge0$, $\ell(h,\cdot)$ đo được; với hàm lỗi không bị chặn cần $L_D(h)<\infty$ (Nhận xét 01.6). (T3) Giả thiết khả thực khi được nêu (Định nghĩa 01.16). (T4) Tính đo được của $(S,\xi)\mapsto L_D(A(S;\xi))$ (Nhận xét 01.26, Phụ lục A).
- **Giả thiết tối ưu:** (O1) thuật toán tính được một nghiệm ERM chính xác, hoặc (O2) chỉ tính được ERM xấp xỉ với dung sai $\epsilon_{\mathrm{opt}}$ (Định nghĩa 01.15). Bài này không dùng giả thiết lồi, trơn hay Lipschitz. Nguồn ngẫu nhiên nội tại $\xi$ độc lập với $S$.
- **UML:** §2.3.1 (i.i.d.), Nhận xét 3.1 (đo được).

### Thành phần 6 — `## 3. Ví dụ xuyên suốt`

Ví dụ 01.1, Ví dụ 01.2, khối application (mục 3 của dàn ý). Chỉ thiết lập, chưa tính; các phép tính nằm ở §4–§8. Bảng phân bố của Ví dụ 01.1 có các cột $x$, $D_{\mathcal X}(x)$, $\eta(x)$ của $D_\eta$, $f(x)$ của $D_f$.

### Thành phần 7–9 và 11 — `## 4. Rủi ro kì vọng và rủi ro thực nghiệm`

- **Mục đích:** định nghĩa đại lượng cần nhỏ ($L_D$) và đại lượng tính được ($L_S$); chứng minh quan hệ duy nhất đúng không điều kiện giữa chúng.
- **Đầu vào:** thiết lập §1, ví dụ §3. **Đầu ra:** $L_S(h)$ không chệch cho $h$ cố định, nhưng $h$ do thuật toán chọn thì không (dẫn sang §5).
- **Trình tự:**
  1. Đoạn nhu cầu: $D$ chưa biết nên $L_D(h)$ không tính được; chỉ có $S$.
  2. **Định nghĩa 01.5 (Hàm lỗi và rủi ro kì vọng).** Cho $\mathcal Z$ có σ-đại số, $D$ trên $\mathcal Z$, lớp $\mathcal H$. Hàm lỗi $\ell:\mathcal H\times\mathcal Z\to[0,\infty)$ với $\ell(h,\cdot)$ đo được cho mọi $h$. Rủi ro kì vọng $L_D(h)=\mathbb E_{Z\sim D}\,\ell(h,Z)\in[0,\infty]$. Ba hàm lỗi: $\ell_{0\text{-}1}(h,(x,y))=\mathbb 1[h(x)\ne y]$ (khi đó $L_D(h)=\Pr(h(X)\ne Y)$, "xác suất lỗi"), $\ell_c$ (§3.3), hàm lỗi bình phương $(h(x)-y)^2$. Đoạn đọc lại: với $h$ cố định, $L_D(h)$ là một số, không ngẫu nhiên, chưa biết. **Phản ví dụ:** giá trị dự đoán dương (precision) $\Pr(Y=1\mid h(X)=1)$ là tỉ số của hai kì vọng, không có dạng $\mathbb E\,\ell(h,Z)$ với một $\ell$ cố định, nên không là rủi ro theo định nghĩa này.
  3. **Ví dụ 01.3** bảng $L_{D_\eta}(h_t)$ dưới $\ell_{0\text{-}1}$ và $\ell_c$; nhận xét bằng số: hàm tốt nhất trong $\mathcal H$ là $h_3$ dưới 0–1 nhưng $h_2$ dưới $\ell_c$. Câu cuối: cùng tập hàm dự đoán, hàm lỗi khác cho hàm tốt nhất khác.
  4. **Ví dụ 01.4 (Hồi quy tuyến tính).** $\mathcal X=\mathbb R^p$, $\mathcal Y=\mathbb R$, $\mathcal H=\{x\mapsto\langle w,x\rangle:w\in\mathbb R^p\}$, hàm lỗi bình phương. Khung rủi ro giữ nguyên; chỉ đổi $\mathcal Y$ và $\ell$. Điều kiện $\mathbb E\lVert X\rVert^2<\infty$, $\mathbb EY^2<\infty$ cho $L_D(h_w)<\infty$ với mọi $w$, vì $(\langle w,X\rangle-Y)^2\le2\lVert w\rVert^2\lVert X\rVert^2+2Y^2$ (Cauchy–Schwarz). UML §3.2.1 nhắc dự báo nhiệt độ; Eq. (3.2) dùng hàm lỗi bình phương.
  5. **Nhận xét 01.6 (Tính khả tích khi hàm lỗi không bị chặn).** Nếu $\mathbb EY^2=\infty$ thì $L_D(h)=\infty$ với $h\equiv0$. Hàm lỗi bình phương không bị chặn; các kết quả của Bài 02 cho hàm lỗi trong $[0,1]$ không tự chuyển sang hàm lỗi bình phương hay hàm lỗi log (blueprint mục E).
  6. **Định nghĩa 01.7 (Rủi ro thực nghiệm).** $L_S(h)=\frac1m\sum_{i=1}^m\ell(h,Z_i)$; là rủi ro dưới phân bố thực nghiệm (phân bố đều trên các phần tử của $S$, tính cả lặp); với hàm lỗi 0–1 là tỉ lệ lỗi. Đọc lại: với $h$ cố định, $L_S(h)$ là biến ngẫu nhiên theo $S$. **Phản ví dụ:** khi $h$ chọn theo chính $S$, $L_S(h)$ vẫn tính được nhưng không còn tính chất của Mệnh đề 01.1 (dẫn Nhận xét 01.8).
  7. **Ví dụ 01.5** bảng $L_{S_\eta}(h_t)$; đặt cạnh $L_{D_\eta}(h_t)$.
  8. **Mệnh đề 01.1** và chứng minh (mục 5 của dàn ý). Ngay sau: $L_{S_\eta}(h_3)=1/3$ trên một mẫu, trong khi $\mathbb E_SL_S(h_3)=0{,}22$; mệnh đề nói về trung bình theo mẫu, không về một mẫu.
  9. **Nhận xét 01.8 (Giả thuyết chọn theo mẫu).** $\ell(A(S),Z_i)$ phụ thuộc toàn bộ $S$ nên không có phân bố của $\ell(h,Z)$ với $h$ cố định; nói chung $\mathbb E_SL_S(A(S))\ne\mathbb E_SL_D(A(S))$. Hai ví dụ dẫn trước (chứng minh ở §5, §6): hàm ghi nhớ cho $0$ và $1$; $A_{\max}$ dưới $D_f$ cho $0$ và $0{,}2(0{,}8^m+0{,}6^m+0{,}4^m)$. Cách sửa: đánh giá $A(S)$ trên một mẫu mới độc lập với $S$; khi đó, có điều kiện theo $S$, Mệnh đề 01.1 áp dụng với $h=A(S)$ cố định. Không phát triển thêm về tập kiểm tra (Bài 04).
- **Đoạn kết (văn xuôi, không có nhãn trong ghi chú):** rủi ro thực nghiệm chỉ đáng tin cho giả thuyết chọn trước; thuật toán học chọn sau khi thấy $S$.
- **UML:** §2.1 Eq. (2.1), §2.2 Eq. (2.2), §3.2.1 Eq. (3.1), §3.2.2 Eq. (3.3)–(3.4); UML Bài tập 2.2 là trường hợp riêng của Mệnh đề 01.1.

### Thành phần 7–11 — `## 5. Tối thiểu hóa rủi ro thực nghiệm`

- **Mục đích:** định nghĩa thuật toán học và ERM; cho thấy quy tắc ERM có thể chọn hàm tệ nhất có thể; đưa khái niệm thiên kiến quy nạp.
- **Đầu vào:** $L_S$, Nhận xét 01.8. **Đầu ra:** cần một yêu cầu đúng cho $L_D(A(S))$, không cho $L_S$; dẫn sang định nghĩa PAC ở §6.
- **Trình tự:**
  1. **Định nghĩa 01.9 (Thuật toán học).** Cho $\mathcal H$ và một không gian xác suất $\Xi$ của nguồn ngẫu nhiên nội tại. Thuật toán học là một họ ánh xạ $A_m:\mathcal Z^m\times\Xi\to\mathcal H$, $m\ge1$, sao cho $(s,\xi,z)\mapsto\ell(A_m(s;\xi),z)$ đo được; $\xi$ độc lập với $S$. Viết $A(S;\xi)$, hoặc $A(S)$ khi $A$ tất định ($\Xi$ một điểm). Mặc định học đúng lớp, $A(S;\xi)\in\mathcal H$ (quyết định 3). $A$ không nhận $D$, $\epsilon$, $\delta$ làm đầu vào. **Ví dụ:** $A_{\max}$, $A_{\min}$. **Phản ví dụ:** "chọn hàm Bayes $\mathbb 1[\eta(x)\ge1/2]$" cần $\eta$, tức cần $D$, nên không là thuật toán học.
  2. **Nhận xét 01.10 (Nguồn ngẫu nhiên nội tại).** Xác suất trong mọi bảo đảm lấy theo cả $S$ và $\xi$; UML không đưa $\xi$ vào định nghĩa (bổ sung của học phần, quyết định 4). Số liệu: với $S_\eta$ cố định, chọn đều trong $\{h_2,h_3,h_5\}$ cho $\mathbb E_\xi L_{D_\eta}\approx0{,}273$ và chỉ với xác suất $1/3$ theo $\xi$ thì rủi ro vượt mức không quá $0{,}05$†. Nhắc: SGD ở Bài 05 có chỉ số ngẫu nhiên, cũng là $\xi$.
  3. **Định nghĩa 01.11 (Khoảng cách tổng quát hóa).** $L_D(A(S;\xi))-L_S(A(S;\xi))$, có dấu, ngẫu nhiên. Với $h$ cố định, kì vọng của $L_D(h)-L_S(h)$ bằng 0 (Mệnh đề 01.1). Không gọi là "sai số tổng quát hóa" (`thuat-ngu.md`).
  4. **Định nghĩa 01.12 (Tối thiểu hóa rủi ro thực nghiệm).** Tập nghiệm ERM $\arg\min_{h\in\mathcal H}L_S(h)=\{h\in\mathcal H:L_S(h)=\inf_{h'\in\mathcal H}L_S(h')\}$; nghiệm ERM $\hat h$ là một phần tử. Thuật toán ERM là thuật toán học có $A(S;\xi)\in\arg\min_{\mathcal H}L_S$ với mọi $S$, $\xi$ (khi tập này khác rỗng); tức là quy tắc ERM cộng một quy tắc chọn khi bằng nhau. Lần đầu: "tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM)". **Phản ví dụ:** $h_4$ có $L_{S_\eta}(h_4)=1/2>1/3$ nên không là nghiệm ERM trên $S_\eta$.
  5. **Nhận xét 01.13 (Sự tồn tại nghiệm ERM và quy tắc chọn khi bằng nhau).** Với hàm lỗi 0–1, $L_S(h)\in\{0,\tfrac1m,\ldots,1\}$, một tập hữu hạn, nên $\arg\min$ khác rỗng với **mọi** $\mathcal H$ khác rỗng, kể cả lớp vô hạn. Giá trị nhỏ nhất có thể dương: trên cả 32 hàm $\mathcal X\to\{0,1\}$, $\min L_{S_\eta}=1/6$. Với hàm lỗi khác tập nghiệm có thể rỗng (Ví dụ 01.7). Khi có nhiều nghiệm, bảo đảm "cho mọi nghiệm ERM" mạnh hơn "cho một nghiệm ERM"; UML Hệ quả 2.3 dùng dạng thứ nhất.
  6. **Ví dụ 01.6 (Các nghiệm ERM trên mẫu sàng lọc).** Tập nghiệm $\{h_2,h_3,h_5\}$; ba quy tắc chọn (ngưỡng nhỏ nhất, lớn nhất, ngẫu nhiên) cho rủi ro kì vọng 0,32; 0,28; trung bình 0,273; chỉ $h_3$ đạt $\inf_{\mathcal H}L_{D_\eta}=0{,}22$. Nhắc lại $S_f$: nghiệm ERM là $h_3$ và $h_4$, $A_{\min}$ chọn $h_3$, $A_{\max}$ chọn $h_4$; đây là phần đầu câu trả lời cho câu hỏi mở đầu.
  7. **Thuật toán 01.14 (ERM cho lớp hàm ngưỡng trên tập đầu vào hữu hạn).** Đầu vào: $S$, $\mathcal X=\{1,\ldots,K\}$. Tính số đếm $n_y(x)=\#\{i:x_i=x,y_i=y\}$. Khởi tạo $E(1)=\sum_x n_0(x)$ (số lỗi của $h_1$); cập nhật $E(t+1)=E(t)-n_0(t)+n_1(t)$ cho $t=1,\ldots,K$; $L_S(h_t)=E(t)/m$. Đầu ra: ngưỡng nhỏ nhất (hoặc lớn nhất) đạt $\min_tE(t)$. Chi phí $O(m+K)$. Dừng sau $K$ bước. Trong trường hợp khả thực, ngưỡng nhỏ nhất trùng $A_{\min}$, lớn nhất trùng $A_{\max}$. Kiểm tra trên $S_\eta$: $E=(3,2,2,3,2,3)$. (Thành phần 10 đặt ở đây, không có mục "Thuật toán" riêng; điểm mở 8.)
  8. **Định nghĩa 01.15 (ERM xấp xỉ).** Cho $\epsilon_{\mathrm{opt}}\ge0$. Thuật toán học là $\epsilon_{\mathrm{opt}}$-ERM nếu $L_S(A(S;\xi))\le\inf_{h\in\mathcal H}L_S(h)+\epsilon_{\mathrm{opt}}$ với mọi $S$, $\xi$. Luôn tồn tại khi $\epsilon_{\mathrm{opt}}>0$ (cận dưới đúng hữu hạn vì $\ell\ge0$). Là giả thiết tối ưu, không phải giả thiết thống kê. Định nghĩa của học phần, không có trong UML Ch. 2–3 (quyết định 5); Bài 04 đặt tên $\operatorname{opt}_S$.
  9. **Ví dụ 01.7 (Cận dưới đúng không đạt được của rủi ro thực nghiệm).** $\mathcal H_+=\{x\mapsto wx:w>0\}$ trên $\mathbb R$, hàm lỗi bình phương, mẫu một quan sát $S=((1,0))$: $L_S(w)=w^2$, $\inf=0$ không đạt; mọi $w\le\sqrt{\epsilon_{\mathrm{opt}}}$ là $\epsilon_{\mathrm{opt}}$-ERM†.
  10. **Mệnh đề 01.2** và chứng minh (mục 5 của dàn ý).
  11. **Đoạn thiên kiến quy nạp** (không đánh số): lần đầu "thiên kiến quy nạp (inductive bias)". Chọn $\mathcal H$ là lớp hàm ngưỡng trước khi thấy dữ liệu loại hàm ghi nhớ khỏi các ứng viên; trên $S_f$ chỉ còn hai nghiệm ERM. Cái giá: lớp có thể không chứa hàm Bayes (dẫn tới con số 0,04 ở §7). Quy tắc chọn khi bằng nhau là một dạng thiên kiến khác, ở mức thuật toán.
- **Đoạn kết (văn xuôi, không có nhãn trong ghi chú):** rủi ro thực nghiệm bằng 0 không nói gì về rủi ro kì vọng khi lớp quá giàu; cần phát biểu yêu cầu trực tiếp cho $L_D(A(S))$.
- **UML:** §2.2, §2.2.1 (quá khớp, hàm ghi nhớ hai chiều với $L_D=1/2$; ghi chú dùng bản một chiều của blueprint, quyết định 7), §2.3 (thiên kiến quy nạp).

### Nghỉ giữa giờ (chỉ trong lịch dạy, không trong ghi chú)

### Thành phần 7–9 — `## 6. Học PAC trong trường hợp khả thực`

- **Mục đích:** phát biểu yêu cầu "xấp xỉ đúng với xác suất cao" với đúng thứ tự lượng từ khi có $h^\star\in\mathcal H$ không lỗi.
- **Đầu vào:** thuật toán học, ERM, nhu cầu từ §5. **Đầu ra:** định nghĩa và một phép tính cho một phân bố; nhu cầu bỏ giả thiết khả thực vì nhãn có nhiễu (dẫn sang §7).
- **Trình tự:**
  1. Đoạn nhu cầu: mẫu có thể không đại diện (ví dụ: không chứa $x=3$, xác suất $0{,}8^m$), nên mọi bảo đảm phải cho phép một xác suất thất bại $\delta$; mẫu hữu hạn không thấy hết chi tiết của $D$, nên cho phép sai số $\epsilon$ (cấu trúc theo UML §3.1, viết lại).
  2. **Định nghĩa 01.16 (Giả thiết khả thực).** Với hàm lỗi 0–1: cặp $(D,\mathcal H)$ khả thực nếu tồn tại $h^\star\in\mathcal H$ với $L_D(h^\star)=0$ (giá trị nhỏ nhất bằng 0 **đạt được**, quyết định 2). Hệ quả đọc lại: $Y=h^\star(X)$ hầu chắc chắn; $L_S(h^\star)=0$ với xác suất 1; nghiệm ERM có $L_S=0$. **Ví dụ:** $(D_f,\mathcal H)$ với $h^\star=h_3$. **Phản ví dụ:** $D_\eta$.
  3. **Nhận xét 01.17 (Khả thực là tính chất của cặp $(D,\mathcal H)$).** Cùng $D_f$: khả thực với lớp hàm ngưỡng, không khả thực với lớp hai hàm hằng $\{h_1,h_6\}$. Cùng lớp hàm ngưỡng: khả thực với $D_f$, không với $D_\eta$. $D_\eta$ không khả thực với bất kì lớp nào, vì tại $x=2$ mọi hàm phân lớp sai với xác suất ít nhất $0{,}2\cdot\tfrac14=0{,}05$† (lập luận trực tiếp, không cần Mệnh đề 01.3). **$\inf=0$ khác $\min=0$:** $X\sim U[0,1]$, $f=\mathbb 1[x>1/2]$, $\mathcal H=\{\mathbb 1[x\ge1/2+1/n]:n\ge1\}$ có $L_D=1/n$, cận dưới đúng 0 không đạt; cặp này không khả thực theo Định nghĩa 01.16. Nhận xét rằng bản lời giải UML Bài tập 3.6 ngầm dùng dạng $\inf$ thuộc `review-log.md`, không đưa vào ghi chú.
  4. **Định nghĩa 01.18 (Học PAC trong trường hợp khả thực).** Cho $\mathcal X$, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1, $\mathcal H$. Thuật toán $A$ cùng hàm $m_A:(0,1)^2\to\mathbb N$ là thuật toán học PAC cho $\mathcal H$ nếu với mọi $\epsilon,\delta\in(0,1)$, mọi $D$ sao cho $(D,\mathcal H)$ khả thực, mọi $m\ge m_A(\epsilon,\delta)$:
     $$\Pr_{S\sim D^m,\ \xi}\big[L_D(A(S;\xi))\le\epsilon\big]\ge1-\delta.$$
     Lớp $\mathcal H$ học được PAC nếu tồn tại $A$ và $m_A$ như vậy. Hiển thị thứ tự lượng từ thành một dòng riêng: $\exists A\ \exists m_A\ \forall\epsilon,\delta\in(0,1)\ \forall D\text{ khả thực}\ \forall m\ge m_A(\epsilon,\delta)$. Đọc lại: $m_A$ không phụ thuộc $D$ (không phụ thuộc phân bố); xác suất theo $S$ và $\xi$; $\epsilon$ là tham số độ chính xác về rủi ro kì vọng; $\delta$ là xác suất thất bại, $1-\delta$ là độ tin cậy. Lần đầu: "học xấp xỉ với xác suất cao (probably approximately correct, PAC)". **Phản ví dụ:** đổi chỗ thành $\forall D\ \exists m$ cho một khái niệm yếu hơn; phép tính ở Ví dụ 01.8 chỉ là một khẳng định dạng này cho một $D$.
  5. **Nhận xét 01.19 (Độ tin cậy lấy theo mẫu, không phải xác suất hậu nghiệm).** Xác suất tính trước khi lấy mẫu, theo các lần lấy mẫu (và $\xi$) giả định lặp lại; sau khi thấy $S$, $L_D(A(S))$ là một số, hoặc $\le\epsilon$ hoặc không. Câu "với xác suất 0,95" không phải xác suất hậu nghiệm của biến cố đó khi biết $S$, cũng không phải xác suất chẩn đoán đúng cho một người cụ thể (đại lượng đó liên quan đến $\eta(x)$). Bổ sung của học phần; UML chỉ nói "over the choice of the examples".
  6. **Định nghĩa 01.20 (Độ phức tạp mẫu).** Với thuật toán $A$ (trong một thiết lập: khả thực hoặc bất khả tri), $m_A(\epsilon,\delta)=\min\{m_0\in\mathbb N:\ \forall D\text{ chấp nhận được},\ \forall m\ge m_0,\ \text{bảo đảm đúng}\}$, bằng $\infty$ nếu không có $m_0$. Độ phức tạp mẫu của lớp: $m_{\mathcal H}(\epsilon,\delta)=\min_A m_A(\epsilon,\delta)$. $\mathcal H$ học được PAC khi và chỉ khi có $A$ với $m_A$ hữu hạn khắp nơi. Thuật toán đạt giá trị nhỏ nhất có thể khác nhau theo $(\epsilon,\delta)$ (điểm mở 6).
  7. **Nhận xét 01.21 (Độ phức tạp mẫu của thuật toán và của lớp).** $m_{\mathcal H}\le m_A$ với mọi $A$; cận trên cho $m_{\mathcal H}$ chỉ cần một thuật toán, cận dưới phải lập luận cho mọi thuật toán (Bài 03, UML §5.1). Vì sao viết "mọi $m\ge$": một thuật toán chạy ERM khi $m$ chẵn và trả $h_6$ khi $m$ lẻ thất bại dưới $D_f$ với mọi $m$ lẻ khi $\epsilon<0{,}6$ ($L_{D_f}(h_6)=0{,}6$)†, dù thành công ở các $m$ chẵn đủ lớn; với thuật toán bất kì, thành công ở cỡ $m$ không kéo theo thành công ở $m+1$ (quyết định 6).
  8. **Ví dụ 01.8 (Xác suất thất bại và cỡ mẫu cho một phân bố khả thực).** Dưới $D_f$: $L_{D_f}(A_{\max}(S))\in\{0;0{,}2;0{,}4;0{,}6\}$; $\Pr[L>0]=\Pr[3\notin S]=0{,}8^m$; với $\epsilon=0{,}1$, $\delta=0{,}05$, biến cố thành công là $L=0$, cần $0{,}8^m\le0{,}05$, tức $m\ge14$ ($0{,}8^{13}=0{,}0550$, $0{,}8^{14}=0{,}0440$). Với $\epsilon=0{,}25$: $\Pr[L>0{,}25]=0{,}6^m$, cần $m\ge6$. $A_{\min}$ cho cùng $0{,}8^m$ (biến cố $2\notin S$). $\mathbb E_SL_{D_f}(A_{\max}(S))=0{,}2(0{,}8^m+0{,}6^m+0{,}4^m)\approx0{,}0227$ tại $m=10$, trong khi $\mathbb E_SL_S(A_{\max}(S))=0$ (số liệu cho Nhận xét 01.8). Đoạn đọc: ở $m=14$, khoảng 4,4% các mẫu huấn luyện cho hàm có rủi ro ít nhất 0,2. **Câu bắt buộc:** đây là cỡ mẫu cho riêng $A_{\max}$ và riêng $D_f$, không phải $m_{A_{\max}}(\epsilon,\delta)$ theo Định nghĩa 01.20.
- **Đoạn kết (văn xuôi, không có nhãn trong ghi chú):** giả thiết khả thực đòi nhãn tất định, không đúng với sàng lọc thực tế; §7 bỏ nó.
- **UML:** §2.3.1 (cấu trúc lập luận $\delta$, $\epsilon$; không lấy phép chứng minh bất đẳng thức hợp), §3.1 Định nghĩa 3.1, mục "Sample Complexity".

### Thành phần 7–9 — `## 7. Học PAC bất khả tri và quy tắc Bayes`

- **Mục đích:** xác định mức tốt nhất có thể (rủi ro Bayes) và lý do đối tượng so sánh là $\inf_{\mathcal H}L_D$; định nghĩa học PAC bất khả tri cho hàm lỗi tổng quát.
- **Đầu vào:** Định nghĩa 01.18, ví dụ có nhiễu $D_\eta$. **Đầu ra:** định nghĩa đầy đủ của bài; §8 dùng nó để đọc phản ví dụ ghi nhớ.
- **Trình tự:**
  1. Đoạn nhu cầu: dưới $D_\eta$, không hàm nào có rủi ro 0 (Nhận xét 01.17); cần một đối tượng so sánh khác 0.
  2. **Mệnh đề 01.3** và chứng minh ngắn (mục 5 của dàn ý; quyết định 8).
  3. **Ví dụ 01.9 (Quy tắc Bayes trong ví dụ sàng lọc).** Hàm lỗi 0–1: $h_{\mathrm{Bayes}}=\mathbb 1[x\in\{3,5\}]$, không phải hàm ngưỡng; $L^{\mathrm{Bayes}}_{D_\eta}=0{,}2(0+\tfrac14+\tfrac14+\tfrac25+0)=0{,}18$; $\inf_{\mathcal H}L_{D_\eta}=0{,}22$, chênh 0,04. Hàm lỗi $\ell_c$ với $(1,4)$: ngưỡng $1/5$, hàm Bayes là $h_2\in\mathcal H$, rủi ro Bayes có trọng số $0{,}32$ bằng $\min_tL^c_{D_\eta}(h_t)$†. Câu cuối: lớp hàm ngưỡng chứa hàm Bayes dưới hàm lỗi này nhưng không chứa dưới hàm lỗi 0–1.
  4. **Định nghĩa 01.22 (Rủi ro vượt mức).** Của $h$ so với $\mathcal H$: $L_D(h)-\inf_{h'\in\mathcal H}L_D(h')$; so với rủi ro Bayes: $L_D(h)-L^{\mathrm{Bayes}}_D$, với $L^{\mathrm{Bayes}}_D=\inf_{g\in\mathcal M_{\mathcal X}}L_D(g)$. Luôn ghi so với gì. Có thể hiển thị tổng $L_D(h)-L^{\mathrm{Bayes}}_D=[L_D(h)-\inf_{\mathcal H}L_D]+[\inf_{\mathcal H}L_D-L^{\mathrm{Bayes}}_D]$ và nói Bài 04 đặt tên hai số hạng; không dùng "sai số ước lượng", "sai số xấp xỉ" ở bài này (quyết định 5). **Ví dụ:** $h_2$ dưới $D_\eta$: 0,10 so với $\mathcal H$, 0,14 so với Bayes.
  5. **Định nghĩa 01.23 (Học PAC bất khả tri).** Cho $\mathcal Z$, $\mathcal H$, $\ell:\mathcal H\times\mathcal Z\to[0,\infty)$. Phân bố chấp nhận được: mọi $D$ trên $\mathcal Z$ với $L_D(h)<\infty$ cho mọi $h\in\mathcal H$ (mọi $D$ khi $\ell$ bị chặn). $A$ cùng $m_A$ là thuật toán học PAC bất khả tri nếu với mọi $\epsilon,\delta\in(0,1)$, mọi $D$ chấp nhận được, mọi $m\ge m_A(\epsilon,\delta)$:
     $$\Pr_{S\sim D^m,\ \xi}\Big[L_D(A(S;\xi))\le\inf_{h\in\mathcal H}L_D(h)+\epsilon\Big]\ge1-\delta,$$
     tức rủi ro vượt mức so với $\mathcal H$ không quá $\epsilon$. Công thức hiển thị đúng như blueprint 1.2, thêm $\xi$. Cùng dòng lượng từ như Định nghĩa 01.18, thay "khả thực" bằng "chấp nhận được". Lần đầu: "học PAC bất khả tri (agnostic PAC learning)". **Phản ví dụ:** yêu cầu $L_D(A(S))\le L^{\mathrm{Bayes}}_D+\epsilon$ cho mọi $D$ không phải định nghĩa này; UML §3.2.1 nêu rằng không thuật toán nào bảo đảm được điều đó khi không có giả định về $D$, chứng minh ở UML §5.1 (chỉ dẫn, không chứng minh).
  6. **Nhận xét 01.24 (Cận dưới đúng thay cho giá trị nhỏ nhất).** UML Định nghĩa 3.3, 3.4 viết $\min$; ghi chú viết $\inf$ vì $\min$ có thể không tồn tại (ví dụ ở Nhận xét 01.17), còn $\inf$ luôn tồn tại trong $[0,\infty)$; hai cách viết trùng khi cận dưới đúng đạt được, như $\min_tL_{D_\eta}(h_t)=0{,}22$. Với hàm lỗi 0–1 và $D$ khả thực, Định nghĩa 01.23 trở thành Định nghĩa 01.18 (Bài tập 01.10).
  7. **Nhận xét 01.25 (Học đúng lớp và học ngoài lớp).** Mặc định $A(S;\xi)\in\mathcal H$ (như UML Định nghĩa 3.4). Học ngoài lớp (improper, UML gọi là representation-independent learning): đầu ra trong một lớp lớn hơn, đối tượng so sánh vẫn là $\inf_{\mathcal H}L_D$. Một thuật toán ngoài lớp có thể có rủi ro nhỏ hơn đối tượng so sánh: $\mathbb 1[x\in\{3,5\}]$ có rủi ro $0{,}18<0{,}22$.
  8. **Nhận xét 01.26 (Tính đo được).** Ngắn, 3–4 câu: biến cố trong định nghĩa PAC cần $(S,\xi)\mapsto L_D(A(S;\xi))$ đo được; Định nghĩa 01.9 đã gộp điều kiện này; với $\mathcal X$ hữu hạn mọi hàm đều đo được; UML không xét điểm này (chỉ đòi $\ell(h,\cdot)$ đo được, Nhận xét 3.1). Chi tiết ở Phụ lục A.
- **Đoạn kết (văn xuôi, không có nhãn trong ghi chú):** định nghĩa đã đủ; câu hỏi còn lại là thuật toán nào đạt được nó và với cỡ mẫu bao nhiêu.
- **UML:** §3.2.1 (Bayes Optimal Predictor, Định nghĩa 3.3), §3.2.2 (Định nghĩa 3.4, Nhận xét 3.1, 3.2); UML Bài tập 3.7 là chứng minh Mệnh đề 01.3(a).

### Thành phần 11 — `## 8. Giới hạn của rủi ro thực nghiệm`

- **Mục đích:** rút hệ quả chính xác từ phản ví dụ ghi nhớ dưới ngôn ngữ PAC; thử bỏ giả thiết; tách khỏi định lý không có bữa trưa miễn phí.
- **Đầu vào:** Mệnh đề 01.2, Định nghĩa 01.18, 01.23. **Đầu ra:** nhu cầu kiểm soát lớp hoặc thuật toán, dẫn sang §9 và Bài 02.
- **Trình tự:**
  1. **Hệ quả 01.4** và chứng minh (mục 5 của dàn ý; quyết định 9).
  2. **Ví dụ 01.10 (Hàm phân lớp ghi nhớ khi phân bố có nguyên tử).** Bỏ giả thiết "$D_{\mathcal X}$ không có nguyên tử": trên $\mathcal X=\{1,\ldots,5\}$ dưới $D_f$, hàm ghi nhớ (nhãn quan sát được tại điểm đã thấy, 0 ở điểm chưa thấy) là ERM trên lớp mọi hàm $\mathcal X\to\{0,1\}$; nó sai đúng tại các điểm dương $\{3,4,5\}$ chưa xuất hiện, nên $\mathbb E_SL_{D_f}=0{,}6\cdot0{,}8^m$†, bằng $0{,}0644$ tại $m=10$, so với $0{,}0227$ của $A_{\max}$ trên lớp hàm ngưỡng. Câu cuối: khi mọi điểm có khối lượng dương, ghi nhớ vẫn tổng quát hóa, chậm hơn ERM trên lớp nhỏ; Mệnh đề 01.2 dùng thật sự tính không có nguyên tử.
  3. **Nhận xét 01.27 (Phản ví dụ ghi nhớ và định lý không có bữa trưa miễn phí).** Mệnh đề 01.2 nói về **một** lựa chọn ERM, **một** phân bố, trong một lớp rất giàu; hàm hằng 1 cũng là nghiệm ERM và có rủi ro 0. Định lý không có bữa trưa miễn phí (UML §5.1) nói về **mọi** thuật toán: với mỗi thuật toán có một phân bố làm nó thất bại khi cỡ mẫu nhỏ so với $\lvert\mathcal X\rvert$. Chỉ dẫn mục, không nêu hằng số, không chứng minh (quyết định 7).
- **UML:** §2.2.1, §2.3 (đoạn ý nghĩa); §5.1 (chỉ trỏ).

### Thành phần 12 — `## 9. Ý nghĩa, tác động và giới hạn`

Văn xuôi, 4–6 đoạn, không gạch đầu dòng cho lập luận.

- **Định nghĩa PAC bảo đảm gì:** rủi ro vượt mức so với $\mathcal H$ (đại lượng tổng thể) không quá $\epsilon$, với xác suất không thấp hơn $1-\delta$ theo $S$ và $\xi$, cho mọi phân bố chấp nhận được, khi $m\ge m_A(\epsilon,\delta)$. Phân biệt bảo đảm cho lớp ("tồn tại thuật toán") với bảo đảm cho một thuật toán cụ thể (blueprint mục E).
- **Không bảo đảm gì:** không nói về một dự đoán riêng lẻ (Nhận xét 01.19); không so với rủi ro Bayes; không nói về thời gian tính (UML §3.4 nhắc yêu cầu đa thức của Valiant; tùy chọn một câu); không áp dụng khi mẫu không độc lập cùng phân bố.
- **Quyết định thực hành nó định hướng:** chọn hàm lỗi theo chi phí (ngưỡng $c_{FP}/(c_{FP}+c_{FN})$); cố định $\mathcal H$ trước khi xem dữ liệu; không đọc $L_S(\hat h)$ như rủi ro; đánh giá trên mẫu độc lập (Nhận xét 01.8); ghi rõ quy tắc chọn khi bằng nhau.
- **Một phân bố so với mọi phân bố:** cỡ mẫu 14 của Ví dụ 01.8 chỉ cho $D_f$. Một câu dẫn Bài tập 01.9: với lớp có cùng cấu trúc (đường tròn đồng tâm, và theo cùng lập luận là hàm ngưỡng), $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$ đủ cho mọi phân bố khả thực, tức 30 khi $\epsilon=0{,}1$, $\delta=0{,}05$†. Tùy chọn; nếu giữ, ghi là kết quả của bài tập.
- **Hàm lỗi không bị chặn:** Nhận xét 01.6 nhắc lại một câu.

### Thành phần 13 — `## 10. Bài tập`

Danh sách ngắn 11 bài, mỗi bài một dòng: số, tên, mục tiêu đo; trỏ sang `exercises.md`. Tách bài gốc (01.1–01.5) và bài chọn từ UML (01.6–01.11). Chi tiết ở mục 7 của dàn ý.

### Thành phần 14 — `## 11. Câu hỏi cuối buổi và cầu nối`

- **Câu hỏi:** "Trong $L_D(A(S))$ phân bố $D$ cố định. Đại lượng nào ngẫu nhiên, và ngẫu nhiên theo phân bố nào?" (blueprint). Hai câu phụ: (2) "Trên mẫu $S_\eta$, nghiệm ERM có rủi ro kì vọng bằng bao nhiêu?" (phụ thuộc quy tắc chọn: 0,32; 0,22 hoặc 0,28). (3) "Với $\delta=0{,}05$, có thể nói hàm phân lớp vừa học đúng với xác suất 95% không?" (không; Nhận xét 01.19). Đáp án trong khối `hint`.
- **Trả lời câu hỏi mở đầu** bằng một đoạn: $h_3$ và $h_4$ chỉ khác nhau tại $x=3$; mẫu bỏ sót $x=3$ với xác suất $0{,}8^m$; khi đó quy tắc chọn quyết định ($A_{\min}$ hay $A_{\max}$); lớp hàm ngưỡng giới hạn ứng viên còn hai, lớp mọi hàm thì không giới hạn.
- **Cầu nối (blueprint):** Ví dụ 01.8 tính được $\Pr[L_{D_f}(A_{\max}(S))>0]$ chính xác vì biết $D_f$. Với $D$ chưa biết, cần chặn $\Pr\big(\lvert L_S(h)-L_D(h)\rvert>\epsilon\big)$ cho $h$ cố định (Mệnh đề 01.1 cho kì vọng; cần thêm độc lập và hàm lỗi bị chặn), rồi đồng thời cho mọi $h\in\mathcal H$ vì $\hat h$ chọn theo $S$. Bài 02 làm việc đó cho lớp hữu hạn bằng bất đẳng thức Hoeffding và bất đẳng thức hợp.

### Thành phần 15 — `## 12. Tài liệu đọc`

- **Trước buổi học:** UML §§2.1–2.2.
- **Sau buổi học:** UML §2.3 (§2.3.1 là phần mở đầu của Bài 02), §§3.1–3.2; các bài tập UML §2.4, §3.5 đã chọn.
- **Mở rộng:** UML §5.1 (định lý không có bữa trưa miễn phí); không đồng nhất phản ví dụ ghi nhớ với định lý này.

Blueprint chỉ chia "bắt buộc" và "tùy chọn"; cách chia trước/sau buổi là đề xuất (điểm mở 9).

### `## Phụ lục`

- **A. Tính đo được.** (i) $\ell(h,\cdot)$ đo được; (ii) điều kiện $(s,\xi,z)\mapsto\ell(A_m(s;\xi),z)$ đo được kéo theo $L_D(A(S;\xi))=\int\ell(A(S;\xi),z)\,dD(z)$ là biến ngẫu nhiên (định lý Tonelli); (iii) hàm ghi nhớ: tập $\{(s,x):\exists i,\ x=x_i\}$ là hợp hữu hạn của các tập đóng nên Borel, do đó $(s,x)\mapsto\mathbb 1[x\in\{x_1,\ldots,x_m\}]$ đo được; (iv) với lớp vô hạn tổng quát, cận trên đúng theo $\mathcal H$ có thể không đo được; học phần dùng điều kiện đo được chuẩn khi cần (Bài 02–03).
- **B. Quy tắc Bayes tổng quát.** Sự tồn tại của $\eta$ đo được với $\eta(X)=\Pr(Y=1\mid X)$ hầu chắc chắn (định lý Doob–Dynkin); tính không duy nhất (tập $\{\eta=\text{ngưỡng}\}$ và tập có xác suất 0); công thức rủi ro Bayes cho $\ell_{0\text{-}1}$ và $\ell_c$; trường hợp $\mathcal X$ rời rạc, nơi $\eta(x)=\Pr(Y=1,X=x)/\Pr(X=x)$ khi $\Pr(X=x)>0$.
- **C. Tính toán chi tiết cho ví dụ xuyên suốt.** Công thức $L_{D_\eta}(h_t)=0{,}2\big[\sum_{x<t}\eta(x)+\sum_{x\ge t}(1-\eta(x))\big]$ và bản có trọng số; công thức tổng đuôi $\mathbb E[\hat t-3]=\sum_{k=1}^{3}\Pr(\hat t-3\ge k)$ cho $\mathbb E L_{D_f}(A_{\max}(S))$; $\mathbb E L_{D_f}$ của hàm ghi nhớ trên $\{1,\ldots,5\}$; trung bình theo quy tắc chọn ngẫu nhiên.

Mọi chứng minh [F] ở lại thân bài vì đều ngắn; Phụ lục không chứa chứng minh bắt buộc.

## 5. Phát biểu hình thức: giả thiết, bảo đảm và lộ trình chứng minh

Mỗi khối kết quả có hai dòng in đậm "**Giả thiết.**" và "**Bảo đảm.**". Nội dung dưới đây là nội dung bắt buộc; người viết diễn đạt lại bằng văn xuôi học thuật.

### Mệnh đề 01.1 (Tính không chệch của rủi ro thực nghiệm với giả thuyết cố định) — chứng minh đầy đủ

**Giả thiết.** $Z_1,\ldots,Z_m$ là biến ngẫu nhiên trên cùng một không gian xác suất, mỗi $Z_i$ có phân bố $D$ trên $\mathcal Z$; không cần độc lập. $h\in\mathcal H$ cố định, không phụ thuộc $S$. $\ell(h,\cdot)$ đo được, nhận giá trị trong $[0,\infty)$, và $L_D(h)<\infty$.

**Bảo đảm.** $\mathbb E_S[L_S(h)]=L_D(h)$ với mọi $m\ge1$. Bảo đảm theo kì vọng, so một đại lượng thực nghiệm với một đại lượng tổng thể; không phụ thuộc $m$; không nói gì về độ lệch $\lvert L_S(h)-L_D(h)\rvert$ trên một mẫu cụ thể.

**Lộ trình.** Viết $L_S(h)$ là trung bình $m$ biến ngẫu nhiên; công cụ then chốt là tính tuyến tính của kì vọng (không có bất đẳng thức).

1. $\ell(h,Z_i)$ là biến ngẫu nhiên không âm và khả tích. *Dùng:* $h$ cố định nên $\ell(h,Z_i)$ chỉ phụ thuộc $Z_i$; $\ell(h,\cdot)$ đo được; $L_D(h)<\infty$.
2. $\mathbb E\,\ell(h,Z_i)=\int\ell(h,z)\,dD(z)=L_D(h)$ với mỗi $i$. *Dùng:* $Z_i$ có phân bố $D$.
3. Tính tuyến tính cho $\mathbb E_S L_S(h)=\frac1m\sum_i\mathbb E\,\ell(h,Z_i)=L_D(h)$. *Ghi rõ:* bước này không dùng độc lập; độc lập cần cho Bài 02 (tập trung).

Câu ý nghĩa sau $\square$: rủi ro thực nghiệm của một giả thuyết chọn trước khi thấy mẫu là ước lượng không chệch của rủi ro kì vọng; đó là cơ sở của việc đánh giá trên mẫu độc lập.

### Mệnh đề 01.2 (Nghiệm ERM ghi nhớ có rủi ro kì vọng bằng 1) — chứng minh đầy đủ

**Giả thiết.** $\mathcal X=[0,1]$ với σ-đại số Borel, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1. $D$: $X\sim U[0,1]$, $Y=1$ chắc chắn (Ví dụ 01.2). $\mathcal H=\mathcal M_{\mathcal X}$, mọi hàm phân lớp Borel $[0,1]\to\{0,1\}$. $m\ge1$ tùy ý, $S=((X_1,1),\ldots,(X_m,1))\sim D^m$. Thuật toán ghi nhớ $A_{\mathrm{gn}}$: $A_{\mathrm{gn}}(S)(x)=y_i$ nếu $x=x_i$ (chỉ số $i$ nhỏ nhất), $0$ nếu $x\notin\{x_1,\ldots,x_m\}$.

**Bảo đảm.** Với **mọi** giá trị của $S$: (i) $A_{\mathrm{gn}}(S)\in\mathcal H$ và $L_S(A_{\mathrm{gn}}(S))=0=\min_{\mathcal H}L_S$, nên $A_{\mathrm{gn}}$ là một thuật toán ERM; (ii) $L_D(A_{\mathrm{gn}}(S))=1$; (iii) hàm hằng $h_{\equiv1}$ cũng là nghiệm ERM và $L_D(h_{\equiv1})=0$, nên $(D,\mathcal H)$ khả thực và $\inf_{\mathcal H}L_D=0$. Khẳng định tất định, đúng với mọi mẫu, không phải với xác suất cao; khoảng cách tổng quát hóa bằng 1 với mọi $m$.

**Lộ trình.** Kiểm tra $A_{\mathrm{gn}}(S)$ thuộc lớp, tính $L_S$, tính $L_D$; sự kiện then chốt là tập hữu hạn có xác suất 0 dưới phân bố đều.

1. Tập $\{x_1,\ldots,x_m\}$ hữu hạn nên đóng, do đó Borel; hàm chỉ thị của nó đo được, nên $A_{\mathrm{gn}}(S)\in\mathcal H$. *Dùng:* $\mathcal H$ gồm **mọi** hàm phân lớp đo được (lớp giàu).
2. $A_{\mathrm{gn}}(S)(x_i)=1=y_i$ với mọi $i$, nên $L_S=0$; vì $\ell\ge0$, đây là giá trị nhỏ nhất. *Dùng:* hàm lỗi 0–1 không âm.
3. Vì $Y=1$, lỗi xảy ra khi và chỉ khi $A_{\mathrm{gn}}(S)(X)=0$, tức $X\notin\{x_1,\ldots,x_m\}$; $\Pr(X\in\{x_1,\ldots,x_m\})\le\sum_i\Pr(X=x_i)=0$, nên $L_D=1$. *Dùng:* $D_{\mathcal X}$ không có nguyên tử. Đây là chỗ Ví dụ 01.10 bỏ giả thiết.
4. $h_{\equiv1}$: $L_S=0$, $L_D=0$.

Câu ý nghĩa: trên lớp quá giàu, quy tắc ERM không xác định một hàm dự đoán; quy tắc chọn khi bằng nhau quyết định toàn bộ rủi ro kì vọng. Kết luận nói về một lựa chọn ERM, không phải mọi lựa chọn ERM, và không phải định lý không có bữa trưa miễn phí.

### Mệnh đề 01.3 (Quy tắc Bayes cho hàm lỗi 0–1 và hàm lỗi có trọng số) — đọc thêm

**Giả thiết.** $\mathcal Y=\{0,1\}$; $D$ trên $\mathcal X\times\{0,1\}$ với biên $D_{\mathcal X}$; $\eta:\mathcal X\to[0,1]$ đo được và $\eta(X)=\Pr(Y=1\mid X)$ hầu chắc chắn. Đối tượng so sánh: $\mathcal M_{\mathcal X}$, mọi hàm phân lớp đo được (không giới hạn trong $\mathcal H$). (a) Hàm lỗi 0–1. (b) Hàm lỗi $\ell_c$ với $c_{FP},c_{FN}>0$.

**Bảo đảm.** (a) $h_{\mathrm{Bayes}}(x)=\mathbb 1[\eta(x)\ge1/2]$ thuộc $\mathcal M_{\mathcal X}$ và $L_D(h_{\mathrm{Bayes}})\le L_D(g)$ với mọi $g\in\mathcal M_{\mathcal X}$; $L^{\mathrm{Bayes}}_D=L_D(h_{\mathrm{Bayes}})=\mathbb E\min\{\eta(X),1-\eta(X)\}$. (b) Với $\ell_c$, hàm $\mathbb 1[\eta(x)\ge c_{FP}/(c_{FP}+c_{FN})]$ tối ưu trong $\mathcal M_{\mathcal X}$, với rủi ro $\mathbb E\min\{c_{FN}\eta(X),\,c_{FP}(1-\eta(X))\}$. Bảo đảm về đại lượng tổng thể, không liên quan đến mẫu; hàm tối ưu không duy nhất.

**Lộ trình.** Rủi ro có điều kiện tại $X=x$, tối thiểu hóa từng điểm, lấy kì vọng theo $D_{\mathcal X}$.

1. Với $g$ đo được, $\Pr(g(X)\ne Y\mid X)=\eta(X)\mathbb 1[g(X)=0]+(1-\eta(X))\mathbb 1[g(X)=1]$ hầu chắc chắn. *Dùng:* định nghĩa $\eta$; $g(X)$ là hàm của $X$; hàm lỗi 0–1.
2. Biểu thức đó không nhỏ hơn $\min\{\eta(X),1-\eta(X)\}$, dấu bằng khi $g=h_{\mathrm{Bayes}}$ (khi $\eta=1/2$ hai lựa chọn bằng nhau). $h_{\mathrm{Bayes}}$ đo được vì $\eta$ đo được.
3. Tính chất tháp: $L_D(g)=\mathbb E[\Pr(g(X)\ne Y\mid X)]\ge\mathbb E\min\{\eta,1-\eta\}=L_D(h_{\mathrm{Bayes}})$.
4. (b) Cùng lộ trình: dự đoán 1 tốn $c_{FP}(1-\eta)$, dự đoán 0 tốn $c_{FN}\eta$; chọn 1 khi $c_{FP}(1-\eta)\le c_{FN}\eta$, tương đương $\eta\ge c_{FP}/(c_{FP}+c_{FN})$. Ghi rõ: ngưỡng $1/2$ chỉ đúng khi $c_{FP}=c_{FN}$.

Câu ý nghĩa: rủi ro Bayes là mức thấp nhất mọi hàm dự đoán đạt được; $\mathcal H$ có thể không chứa $h_{\mathrm{Bayes}}$ và thuật toán không biết $\eta$, nên đối tượng so sánh của học PAC bất khả tri là $\inf_{\mathcal H}L_D$. Nhãn đọc thêm: không kiểm tra trên lớp trừ khi giao bài; chứng minh vẫn viết đủ trong thân bài (quyết định 8).

### Hệ quả 01.4 (Rủi ro thực nghiệm nhỏ không đủ làm bảo đảm học) — chứng minh đầy đủ

**Giả thiết.** Thiết lập của Mệnh đề 01.2: $\mathcal X=[0,1]$, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1, $\mathcal H=\mathcal M_{\mathcal X}$, $S\sim D^m$ độc lập cùng phân bố. Một hàm $\varepsilon:\mathbb N\times(0,1)\to[0,\infty)$ được gọi là cận tổng quát hóa cho mọi lựa chọn ERM nếu với mọi thuật toán ERM $\hat A$ trên $\mathcal H$ (mọi quy tắc chọn), mọi $D$ trên $\mathcal X\times\mathcal Y$, mọi $m\ge1$ và mọi $\delta\in(0,1)$: $\Pr_S\big[L_D(\hat A(S))\le L_S(\hat A(S))+\varepsilon(m,\delta)\big]\ge1-\delta$.

**Bảo đảm.** (a) Mọi cận như vậy thỏa $\varepsilon(m,\delta)\ge1$ với mọi $m$, $\delta$; do đó không có cận nào với $\varepsilon(m,\delta)\to0$ khi $m\to\infty$, dù chỉ với một $\delta$. (b) $A_{\mathrm{gn}}$ không là thuật toán học PAC cho $\mathcal H$ trong trường hợp khả thực (do đó cũng không trong trường hợp bất khả tri): với mọi $\epsilon\in(0,1)$, mọi $m$, $\Pr_S[L_D(A_{\mathrm{gn}}(S))\le\epsilon]=0$ dưới phân bố khả thực $D$ của Ví dụ 01.2. Kết luận nói về các lựa chọn ERM trên một lớp; không khẳng định $\mathcal M_{\mathcal X}$ không học được PAC (Bài 03; UML §5.1).

**Lộ trình.** Áp dụng Mệnh đề 01.2 cho một phân bố và đọc biến cố.

1. Theo Mệnh đề 01.2, $L_D(A_{\mathrm{gn}}(S))-L_S(A_{\mathrm{gn}}(S))=1$ với mọi $S$.
2. Biến cố trong (a) có xác suất $\mathbb 1[\varepsilon(m,\delta)\ge1]$; yêu cầu xác suất này $\ge1-\delta>0$ buộc $\varepsilon(m,\delta)\ge1$. *Dùng:* $\delta<1$; định nghĩa "cho mọi lựa chọn ERM" cho phép chọn $\hat A=A_{\mathrm{gn}}$.
3. (b): $L_D(A_{\mathrm{gn}}(S))=1>\epsilon$ với mọi $S$, trong khi $(D,\mathcal H)$ khả thực theo Mệnh đề 01.2(iii).

*Chỗ dùng giả thiết của Mệnh đề 01.2:* lớp chứa hàm ghi nhớ; $D_{\mathcal X}$ không có nguyên tử. Câu ý nghĩa: một bảo đảm phải dùng cấu trúc của lớp (Bài 02–03) hoặc tính chất của thuật toán cụ thể (Bài 06, 08), không thể chỉ dựa vào $L_S$ nhỏ.

### Danh sách kiểm tra theo blueprint mục E cho người viết

Mỗi phát biểu trên nêu: cơ chế lấy mẫu; hàm lỗi và miền giá trị; đối tượng so sánh; nguồn ngẫu nhiên; loại bảo đảm (kì vọng, xác suất cao hay tất định); bảo đảm cho lớp hay cho thuật toán; đại lượng được kiểm soát (rủi ro, rủi ro vượt mức hay khoảng cách tổng quát hóa). Bài có một cận số (Ví dụ 01.8), một phép bỏ giả thiết (Ví dụ 01.10, và Mệnh đề 01.2 như phép bỏ giả thiết "lớp chọn trước, đủ nhỏ"), một câu hỏi cuối buổi.

## 6. Các nhận xét bắt buộc (đối chiếu brief)

| Yêu cầu | Khối | Nội dung chính |
|---|---|---|
| $\inf$ và $\min$, ví dụ không đạt | Nhận xét 01.17, 01.24 | $\mathcal H=\{\mathbb 1[x\ge1/2+1/n]\}$, $L_D=1/n$ |
| Học đúng lớp và học ngoài lớp | Nhận xét 01.25 | $\mathbb 1[x\in\{3,5\}]$ có rủi ro $0{,}18<0{,}22$ |
| Nguồn ngẫu nhiên $\xi$ | Định nghĩa 01.9, Nhận xét 01.10 | $\Pr_{S,\xi}$; chọn ngẫu nhiên trong tập nghiệm ERM |
| Tính đo được (ngắn) | Nhận xét 01.26, Phụ lục A | đo được của $(S,\xi)\mapsto L_D(A(S;\xi))$ |
| Khả thực tương đối với $(D,\mathcal H)$ | Nhận xét 01.17 | hai chiều thay đổi; $D_\eta$ không khả thực với lớp nào |
| Độ tin cậy theo mẫu, không phải hậu nghiệm | Nhận xét 01.19 | sau khi thấy $S$, $L_D(A(S))$ là một số |
| $m_A$ và $m_{\mathcal H}$ | Định nghĩa 01.20, Nhận xét 01.21 | "mọi $m\ge$"; thuật toán chẵn–lẻ |
| Quy tắc chọn khi bằng nhau; $\arg\min$ khác rỗng với lỗi 0–1 | Nhận xét 01.13, Ví dụ 01.6 | $L_S$ nhận hữu hạn giá trị |
| Khả tích với hàm lỗi không bị chặn | Nhận xét 01.6, Ví dụ 01.4 | $\mathbb EY^2=\infty$; cận Bài 02 không chuyển sang |
| Không phải định lý không có bữa trưa miễn phí | Nhận xét 01.27 | một lựa chọn ERM so với mọi thuật toán; trỏ UML §5.1 |

## 7. Kế hoạch bài tập (`exercises.md`)

Viết sau khi ghi chú qua rà soát. Mỗi bài có: mức độ, mục tiêu, đề đủ dữ kiện, 1–3 khối `hint` tăng dần, một khối `solution` có dòng "**Kiểm tra lại.**". Lời giải bài UML viết bằng lập luận riêng; `MLbookSol.pdf` chỉ để đối chiếu sau khi tự giải. Đề UML viết lại theo kí hiệu học phần (phân bố đồng thời $D$, $\mathbb R^p$ thay cho $\mathbb R^d$, $\inf$ thay cho $\min$), ghi "UML Bài tập X.Y" trong tiêu đề, không dịch nguyên văn.

### Bài tập gốc (blueprint 1.5)

| Số | Tên | Mức độ | Mục tiêu | Dùng kết quả | Ý gợi ý (tăng dần) | Lỗi thường gặp |
|---|---|---|---|---|---|---|
| 01.1 | Thiết lập bài toán học cho lọc thư rác và dự báo nhiệt độ | khái niệm | Phân biệt hàm dự đoán với hàm lỗi; nêu đủ $\mathcal X,\mathcal Y,D,S,\mathcal H,\ell,A$, đối tượng so sánh, đại lượng ngẫu nhiên | §1, Định nghĩa 01.5, Ví dụ 01.4, Nhận xét 01.6, Mệnh đề 01.3(b) | (1) liệt kê tám thành phần của §1; (2) nhiệt độ: $\mathcal Y=\mathbb R$, hàm lỗi bình phương, điều kiện khả tích; (3) thư rác: chi phí của hai loại lỗi khác nhau, ngưỡng $c_{FP}/(c_{FP}+c_{FN})$ | đồng nhất $h$ với $\ell$; cho $\mathcal H$ phụ thuộc $S$; giả sử khả thực cho thư rác |
| 01.2 | Hai nghiệm ERM cho một tập dữ liệu ngưỡng | tính toán | Tập nghiệm ERM và quy tắc chọn khi bằng nhau | Định nghĩa 01.12, Nhận xét 01.13, Thuật toán 01.14 | Dữ liệu đề xuất†: $\mathcal X=\mathbb R$, $h_t=\mathbb 1[x\ge t]$, $S=((0{,}3;0),(1{,}1;1),(1{,}8;0),(2{,}5;1),(3{,}4;1))$; $L_S$ = 2/5, 1/5, 2/5, 1/5, 2/5, 3/5 trên sáu khoảng; tập nghiệm $t\in(0{,}3;1{,}1]\cup(1{,}8;2{,}5]$. Phần tùy chọn: $X\sim U[0,4]$, $\eta=0{,}2$ trên $[0,2)$, $0{,}8$ trên $[2,4]$: $L_D(h_t)=0{,}5-0{,}15t$ ($t\le2$), $0{,}15t-0{,}1$ ($t\ge2$); $t=0{,}7$ cho 0,395, $t=2{,}2$ cho 0,23, $t=2$ đạt 0,2. Gợi ý: (1) $L_S$ hằng trên mỗi khoảng giữa hai quan sát liên tiếp; (2) đếm lỗi khi $t$ vượt qua từng quan sát | coi nghiệm ERM là duy nhất; quy tắc "chọn $t$ nhỏ nhất" không xác định vì $(0{,}3;1{,}1]$ không có phần tử nhỏ nhất |
| 01.3 | Tính không chệch và giả thuyết chọn theo mẫu | chứng minh | Chứng minh Mệnh đề 01.1 khi chỉ có cùng phân bố biên; chỉ ra lỗi khi thay $h=A(S)$ | Mệnh đề 01.1, Nhận xét 01.8, Ví dụ 01.8 | (1) thử $Z_1=\cdots=Z_m$; (2) giả thuyết và mẫu đánh giá phụ thuộc nhau (gợi ý của blueprint); (3) tính $\mathbb E_SL_S(A_{\max}(S))=0$ và $\mathbb E_SL_{D_f}(A_{\max}(S))=0{,}2(0{,}8^m+0{,}6^m+0{,}4^m)$; phần (c): $h$ ngẫu nhiên nhưng độc lập với $S$, lấy điều kiện | áp dụng Mệnh đề 01.1 sau khi "cố định" $S$; nghĩ cần độc lập cho đẳng thức kì vọng |
| 01.4 | Dựng hàm phân lớp ghi nhớ và tính hai rủi ro | chứng minh, tính toán | Dùng chặt chẽ tập có xác suất 0 | Mệnh đề 01.2, Ví dụ 01.10, Phụ lục A | Biến thể đề xuất†: $D_{\mathcal X}$ bất kì không có nguyên tử, $Y=f(X)$; hàm ghi nhớ có $L_D=\Pr(f(X)=1)$. Phần có nguyên tử: $D_{\mathcal X}=\tfrac12\delta_0+\tfrac12U[0,1]$, $Y\equiv1$: $\mathbb E_SL_D=0{,}5+0{,}5\cdot0{,}5^m$. Gợi ý: (1) tính đo được của tập hữu hạn; (2) $\Pr(X\in F)\le\sum_{x\in F}\Pr(X=x)$ | quên kiểm tra hàm ghi nhớ thuộc lớp; dùng "xác suất 0 nên không xảy ra" cho từng mẫu thay cho tập hữu hạn |
| 01.5 | Định nghĩa PAC với đủ lượng từ | khái niệm, kiểm tra giả thiết | Viết hai định nghĩa, phủ định "học được PAC", phân biệt $\epsilon$ và $\delta$ | Định nghĩa 01.18, 01.20, 01.23, Nhận xét 01.19, 01.21 | (1) viết dòng lượng từ rồi phủ định từng lượng từ; (2) so sánh $\forall D\ \exists m$ với $\exists m\ \forall D$ bằng Ví dụ 01.8; (3) diễn giải "$\delta=0{,}05$" bằng các lần lấy mẫu lặp lại | gọi $\delta$ là độ tin cậy; coi $\epsilon$ là xác suất; đặt $\forall D$ trước $\exists m_A$ |

### Bài tập chọn từ UML (số đã kiểm tra trên PDF tr. 41–42, 50–52)

| Số | Bài UML | Mức độ | Mục tiêu | Dùng kết quả | Ý gợi ý (tăng dần) | Lỗi thường gặp, chỗ hổng của bản lời giải |
|---|---|---|---|---|---|---|
| 01.6 | 2.1 | chứng minh | Hàm ghi nhớ là một đa thức có ngưỡng, nên ERM trên lớp đa thức có ngưỡng có thể quá khớp | Mệnh đề 01.2 | (1) cần đa thức không âm đúng tại các điểm dương của mẫu; (2) $p_S(x)=-\prod_{i:y_i=1}\lVert x-x_i\rVert^2$ | trường hợp không có quan sát dương (tích rỗng bằng 1, $p_S\equiv-1$); viết $\mathbb R^p$, không $\mathbb R^d$ |
| 01.7 | 3.1 | chứng minh | $m_{\mathcal H}$ không tăng theo từng tham số | Định nghĩa 01.20 | (1) thuật toán đạt $(\epsilon_1,\delta)$ cũng đạt $(\epsilon_2,\delta)$ khi $\epsilon_1\le\epsilon_2$; (2) chứng minh cho $m_A$ trước, rồi lấy $\min_A$ | dùng $m_{\mathcal H}$ mà không dùng tính nhỏ nhất của nó |
| 01.8 | 3.2 | chứng minh, tính toán | Thiết kế ERM có quy tắc chọn cho lớp singleton; cận $\lceil\ln(1/\delta)/\epsilon\rceil$ | Định nghĩa 01.12, 01.18, Nhận xét 01.13 | (1) nếu thấy quan sát dương $z$ thì trả $h_z$, nếu không trả $h_-$; (2) thất bại chỉ khi $f=h_{z^\star}$ với $D_{\mathcal X}(z^\star)>\epsilon$ và $z^\star$ không xuất hiện; (3) $(1-\epsilon)^m\le e^{-\epsilon m}$ | trường hợp $D_{\mathcal X}(z^\star)\le\epsilon$ (rủi ro tự động $\le\epsilon$); khi không có quan sát dương, mọi $h_z$ với $z$ chưa thấy cũng là nghiệm ERM, nên quy tắc chọn quyết định |
| 01.9 | 3.3 | chứng minh | Lớp đường tròn đồng tâm học được PAC với $\lceil\ln(1/\delta)/\epsilon\rceil$ | Định nghĩa 01.18; cùng cấu trúc với $A_{\max}$ | (1) ERM chọn bán kính nhỏ nhất nhất quán, vùng lỗi là vành $\{\hat r<\lVert x\rVert\le r^\star\}$; (2) đặt $r_\epsilon=\inf\{r:D(r<\lVert X\rVert\le r^\star)\le\epsilon\}$, chứng minh vành **đóng** $\{r_\epsilon\le\lVert X\rVert\le r^\star\}$ có khối lượng $\ge\epsilon$ (liên tục phải); (3) thất bại kéo theo không quan sát nào rơi vào vành đóng đó | bản lời giải chọn bán kính có khối lượng **đúng** $\epsilon$; không tồn tại khi $D$ có nguyên tử. **Kiểm tra lại:** với $\epsilon=0{,}1$, $\delta=0{,}05$ cận cho 30, so với 14 của Ví dụ 01.8 cho riêng $D_f$† |
| 01.10 | 3.6 | chứng minh, kiểm tra giả thiết | Bất khả tri kéo theo khả thực, cùng thuật toán | Định nghĩa 01.16, 01.18, 01.23, Nhận xét 01.24 | (1) với $D$ khả thực, $\inf_{\mathcal H}L_D=0$; (2) phân bố khả thực nằm trong họ chấp nhận được; so sánh $m_A$ hai thiết lập | dùng $\min$ khi chưa biết đạt được; bản lời giải ngầm dùng khả thực dạng $\inf=0$; quên rằng cả hai định nghĩa đều học đúng lớp |
| 01.11 | 3.8 (thử thách) | chứng minh | (1) Bayes tối ưu cả trong lớp hàm dự đoán xác suất với hàm lỗi $\lvert h(x)-y\rvert$; (2) với mỗi $D$ có thuật toán tốt hơn mọi thuật toán khác; (3) với mỗi thuật toán có $D$ và $B$ để $A$ không tốt hơn $B$ | Mệnh đề 01.3 | (1) rủi ro có điều kiện $h(x)(1-\eta(x))+(1-h(x))\eta(x)$ tuyến tính theo $h(x)$, nhỏ nhất tại đầu mút; (2) $A_D$ trả $h_{\mathrm{Bayes}}$ với mọi mẫu, cần (1) khi $B$ trả hàm dự đoán xác suất; (3) chọn một mẫu $S_0$, đặt $D$ là khối lượng điểm tại $(x_0,1-A(S_0)(x_0))$, $B$ trả hàm hằng $1-A(S_0)(x_0)$ | bản lời giải thiếu ở (1) (trường hợp $\eta=1/2$, tính đo được) và (3) (cần khối lượng điểm và đúng cách hiểu "với mọi mẫu $S\in(\mathcal X\times\{0,1\})^m$", kể cả mẫu ngoài giá của $D$); nêu rõ $A$ tất định |

Bài không chọn: 2.2 (trùng bài gốc 01.3 và Mệnh đề 01.1), 3.7 (trùng chứng minh Mệnh đề 01.3), 3.9 (ngoài phạm vi); để sang Bài 02: 2.3, 3.4, 3.5 (quyết định 11).

## 8. Bảng thuật ngữ Việt–Anh của bài

Tập con của `thuat-ngu.md` mục 4–5 được dùng trong ghi chú; tiếng Anh trong ngoặc ở lần đầu, viết thường. Thuật ngữ đánh dấu (mới) chưa có trong `thuat-ngu.md`; điều phối viên bổ sung trước khi người viết bắt đầu.

| Thuật ngữ | English | Ghi chú |
|---|---|---|
| không gian xác suất, biến ngẫu nhiên, biến cố | probability space, random variable, event | |
| phân bố, phân bố dữ liệu, phân bố biên (mới) | distribution, data-generating distribution, marginal distribution | $D$, $D_{\mathcal X}$ |
| phân bố thực nghiệm (mới) | empirical distribution | Định nghĩa 01.7 |
| kì vọng, kì vọng có điều kiện, xác suất có điều kiện | expectation, conditional expectation, conditional probability | |
| hàm chỉ thị | indicator function | $\mathbb 1[\cdot]$ |
| độc lập cùng phân bố | independent and identically distributed, i.i.d. | |
| hầu chắc chắn (mới) | almost surely | |
| nguyên tử, phân bố không có nguyên tử (mới) | atom, atomless distribution | Mệnh đề 01.2, Ví dụ 01.10 |
| mẫu, mẫu huấn luyện, quan sát, cỡ mẫu | sample, training sample, example, sample size | |
| tập đầu vào, tập nhãn | input space, label set | |
| đo được | measurable | |
| cận dưới đúng, giá trị nhỏ nhất | infimum, minimum | |
| không chệch | unbiased | |
| phân lớp nhị phân, hồi quy | binary classification, regression | |
| giả thuyết, lớp giả thuyết | hypothesis, hypothesis class | quyết định của người dùng |
| hàm dự đoán, hàm phân lớp, hàm gán nhãn | predictor, classifier, labeling function | |
| hàm ngưỡng | threshold | |
| giả thiết | assumption | nhãn "**Giả thiết.**" |
| thuật toán học | learning algorithm, learner | |
| nguồn ngẫu nhiên nội tại (mới) | internal randomness | $\xi$ |
| hàm lỗi, hàm lỗi 0–1, hàm lỗi bình phương | loss function, 0–1 loss, squared loss | |
| hàm lỗi có trọng số (mới) | cost-weighted loss | $\ell_c$ |
| dương tính giả, âm tính giả (mới) | false positive, false negative | $c_{FP}$, $c_{FN}$ |
| sàng lọc (mới) | screening | |
| rủi ro, rủi ro kì vọng, rủi ro thực nghiệm, tỉ lệ lỗi | risk, population risk, empirical risk, error rate | "rủi ro kì vọng" theo quyết định của người dùng |
| rủi ro có điều kiện (mới) | conditional risk | Mệnh đề 01.3 |
| tối thiểu hóa rủi ro thực nghiệm | empirical risk minimization, ERM | |
| nghiệm ERM, quy tắc ERM, quy tắc chọn khi bằng nhau | an ERM, ERM rule, tie-breaking | |
| ERM xấp xỉ | approximate ERM | $\epsilon_{\mathrm{opt}}$ |
| khả thực, giả thiết khả thực | realizable, realizability assumption | |
| học xấp xỉ với xác suất cao | probably approximately correct, PAC | sau lần đầu: "học PAC" |
| học được PAC, học PAC bất khả tri | PAC learnable, agnostic PAC learning | |
| không phụ thuộc phân bố | distribution-free | |
| độ phức tạp mẫu | sample complexity | $m_A$, $m_{\mathcal H}$ |
| tham số độ chính xác, độ tin cậy, xác suất thất bại | accuracy parameter, confidence, failure probability | $\epsilon$; $1-\delta$; $\delta$ |
| học đúng lớp, học ngoài lớp (mới) | proper learning, improper (representation-independent) learning | |
| thiên kiến quy nạp | inductive bias | quyết định của người dùng |
| quá khớp, tổng quát hóa, khoảng cách tổng quát hóa | overfitting, generalization, generalization gap | |
| ghi nhớ, hàm phân lớp ghi nhớ | memorization, memorizing classifier | xem điểm mở 4 |
| hàm phân lớp tối ưu Bayes, rủi ro Bayes | Bayes optimal classifier, Bayes risk | |
| rủi ro vượt mức | excess risk | luôn ghi so với gì |
| đối tượng so sánh | comparator | |
| phân bố hậu nghiệm | posterior distribution | Nhận xét 01.19 |
| phản ví dụ | counterexample | |
| định lý không có bữa trưa miễn phí | no-free-lunch theorem | xem điểm mở 3 |

## 9. Kí hiệu mới của bài (đối chiếu `ky-hieu.md`)

| Kí hiệu | Ý nghĩa | Đối chiếu `ky-hieu.md` |
|---|---|---|
| $D_{\mathcal X}$ | phân bố biên của $X$ | chưa có; không xung đột |
| $\xi$, $\Xi$ | nguồn ngẫu nhiên nội tại của thuật toán và không gian của nó; $A(S;\xi)$ | chưa có; không xung đột. $A(S)$ giữ nghĩa cũ khi $A$ tất định |
| $\epsilon_{\mathrm{opt}}$ | dung sai của ERM xấp xỉ | `thuat-ngu.md` dòng "approximate ERM" ghi $\epsilon'$ và nói Bài 01 đặt kí hiệu; dàn ý chọn $\epsilon_{\mathrm{opt}}$ để khớp $\operatorname{opt}_S$ của Bài 04 (điểm mở 2) |
| $c_{FP}$, $c_{FN}$, $\ell_c$, $L^{c}_D$ | chi phí dương tính giả, âm tính giả; hàm lỗi có trọng số; rủi ro dưới $\ell_c$ | chưa có. $c$ không dùng cho hằng số phổ quát trong bài này ($C$ của Bài 03 viết hoa) |
| $\eta(x)=\Pr(Y=1\mid X=x)$ | xác suất có điều kiện của nhãn 1 | **trùng chữ** với $\eta_t$ (độ dài bước, Bài 05–08). Đề xuất giữ $\eta(x)$ (UML và tài liệu chuẩn) vì luôn có đối số $x$, còn độ dài bước luôn có chỉ số $t$; thêm dòng vào `ky-hieu.md` (điểm mở 2) |
| $h_{\mathrm{Bayes}}$, $L^{\mathrm{Bayes}}_D$ | hàm phân lớp tối ưu Bayes, rủi ro Bayes | chưa có. UML viết $f_D$, dễ lẫn với hàm gán nhãn $f$; tránh $L^\star$ vì Bài 04 dùng $L^*$ cho rủi ro tham chiếu tổng quát (điểm mở 2) |
| $\mathcal M_{\mathcal X}$ | tập mọi hàm phân lớp đo được $\mathcal X\to\{0,1\}$ | chưa có (điểm mở 2) |
| $h^\star$ | giả thuyết không lỗi trong giả thiết khả thực | `thuat-ngu.md` dùng sẵn |
| $\hat h$, $A_{\max}$, $A_{\min}$, $A_{\mathrm{gn}}$, $\hat t$ | nghiệm ERM; ba thuật toán ERM của các ví dụ | $\hat h$ theo `ky-hieu.md`; còn lại là kí hiệu cục bộ |
| $h_t=\mathbb 1[x\ge t]$, $D_\eta$, $D_f$, $S_\eta$, $S_f$ | hàm ngưỡng; hai phân bố và hai mẫu cụ thể của ví dụ sàng lọc | cục bộ; $S_\eta$, $S_f$ là giá trị cụ thể của $S$ |
| $m_A(\epsilon,\delta)$ | độ phức tạp mẫu của thuật toán $A$ | bổ sung cho dòng $m_{\mathcal H}$ |
| $\ell_{0\text{-}1}$ | hàm lỗi 0–1 | đã có |

Số thập phân trong ghi chú viết dấu phẩy ($0{,}22$ trong KaTeX; "0,22" trong văn bản). Dàn ý này cũng viết như vậy.

## 10. Phân bổ thời gian 140 phút (chỉ dùng nội bộ, không đưa vào ghi chú)

| Khối blueprint | Phút | Mục ghi chú | Nội dung giảng |
|---|---|---|---|
| Động cơ | 15 | Câu hỏi mở đầu, Mục tiêu, Tiên quyết | $S_f$, $h_3$ và $h_4$; chi phí bất đối xứng; ba câu ôn nhanh |
| Thiết lập | 25 | §1–§4 | bảng cố định/ngẫu nhiên; Ví dụ 01.1–01.2; Định nghĩa 01.5, 01.7; Ví dụ 01.3, 01.5; Mệnh đề 01.1 có chứng minh; Nhận xét 01.8. Ví dụ 01.4 và Nhận xét 01.6 chỉ nêu |
| ERM và ví dụ | 30 | §5 | Định nghĩa 01.9, 01.12; Ví dụ 01.6; Nhận xét 01.13; Mệnh đề 01.2 có chứng minh; thiên kiến quy nạp. Thuật toán 01.14, Định nghĩa 01.15, Ví dụ 01.7, Nhận xét 01.10 nói lướt hoặc để tự đọc |
| Nghỉ | 10 | — | — |
| Định nghĩa PAC | 30 | §6–§7 | Định nghĩa 01.16, 01.18, 01.20 với dòng lượng từ; Ví dụ 01.8; Mệnh đề 01.3 chỉ phát biểu kèm Ví dụ 01.9 (chứng minh để tự đọc); Định nghĩa 01.22, 01.23 |
| Phản ví dụ và diễn giải | 25 | §8–§9 | Hệ quả 01.4 có chứng minh; Ví dụ 01.10; Nhận xét 01.17, 01.19, 01.21, 01.27; ý nghĩa và giới hạn |
| Bài tập và câu hỏi cuối buổi | 15 | §10–§11 | chữa nhanh Bài tập 01.2 hoặc 01.5; câu hỏi cuối buổi; cầu nối |

Blueprint mục A: nếu 150 phút là thời gian giảng không tính nghỉ, 10 phút dư dùng để chữa trọn một bài (đề xuất Bài tập 01.4).

## 11. Độ dài mục tiêu và giai đoạn viết

- **Ghi chú:** thân bài khoảng 8.000–10.500 tiếng (đếm `wc -w` trên Markdown, gồm cả công thức), Phụ lục khoảng 1.000–1.800 tiếng; tổng không quá khoảng 12.000, tương đương 650–850 dòng Markdown. Căn cứ: 4 kết quả ngắn có chứng minh [F], 11 định nghĩa có đọc lại và ví dụ, 12 nhận xét, 10 ví dụ có số, cho một buổi 150 phút ở bậc cao học; ghi chú là chương tự đọc được nên dài hơn phần giảng. Bài 01 là bài thí điểm: người dùng sẽ duyệt độ dài, và con số này cần được hiệu chỉnh sau khi duyệt.
- **Bài tập:** khoảng 4.500–6.500 tiếng cho 11 bài có gợi ý và lời giải.
- **Giai đoạn viết** (mỗi giai đoạn khoảng 150 dòng, điều phối viên đọc sau mỗi giai đoạn): (1) tiêu đề đến §3; (2) §4; (3) §5; (4) §6–§7; (5) §8–§12 và Phụ lục.
- **Con số mới cần điều phối viên tính lại** (†): $L_{D_f}(h_4)=0{,}2$ và rủi ro có trọng số 0,8; bảng $L^c_{D_\eta}(h_t)$ = 0,52; 0,32; 0,37; 0,92; 1,12; 1,92 và rủi ro Bayes có trọng số 0,32; trung bình 0,273 và xác suất 1/3 của quy tắc chọn ngẫu nhiên; xác suất lỗi tối thiểu 0,05 tại $x=2$; thuật toán chẵn–lẻ với $L_{D_f}(h_6)=0{,}6$; $\mathbb E L_{D_f}$ của hàm ghi nhớ $=0{,}6\cdot0{,}8^m\approx0{,}0644$ tại $m=10$; $E=(3,2,2,3,2,3)$ của Thuật toán 01.14; Ví dụ 01.7; số liệu đề xuất của Bài tập 01.2 và 01.4; con số 30 $=\lceil\ln20/0{,}1\rceil$.

## 12. Rủi ro và điểm mở cho điều phối viên

**Điểm mở cần quyết định:**

1. **Đánh số.** Phương án B (kết quả giữ 01.1–01.4, các khối khác từ 01.5, không đơn điệu) theo brief, hay phương án A (một bộ đếm đơn điệu theo thứ tự đọc, ghi ánh xạ blueprint → ghi chú trong `review-log.md`)? Tác tử lập kế hoạch nghiêng về A vì học viên đọc "Định nghĩa 01.7" rồi mới đến "Mệnh đề 01.1" sẽ khó tra cứu; quy tắc "giữ số blueprint" của `CLAUDE.md` có vẻ được viết cho các bài mà kết quả đứng trước định nghĩa mới. Cũng cần quyết định nhận xét và thuật toán có vào bộ đếm chung không (mẫu ghi chú đưa vào).
2. **Kí hiệu mới:** $\eta(x)$ trùng chữ với $\eta_t$; $h_{\mathrm{Bayes}}$, $L^{\mathrm{Bayes}}_D$ (thay $f_D$ của UML); $\mathcal M_{\mathcal X}$; $\epsilon_{\mathrm{opt}}$ (thay $\epsilon'$ ghi trong `thuat-ngu.md`); $D_{\mathcal X}$; $A(S;\xi)$. Cần thêm vào `ky-hieu.md` trước khi viết.
3. **Tên định lý NFL:** `thuat-ngu.md` chọn "định lý không có bữa trưa miễn phí", còn quyết định 7 trong `review-log.md` viết "Không có bữa ăn miễn phí". Dàn ý theo `thuat-ngu.md`; cần xác nhận.
4. **"Ghi nhớ" hay "học thuộc":** `thuat-ngu.md` chọn "ghi nhớ" ("hàm phân lớp ghi nhớ"); brief viết "ERM học thuộc"; thẻ Bài 01 trong `2627-1/index.html` viết "hiện tượng học thuộc". Dàn ý dùng "ghi nhớ"; nếu giữ, thẻ chỉ mục cần sửa khi ghi chú được liên kết.
5. **Chi phí minh họa $(c_{FP},c_{FN})=(1,4)$** và mọi con số suy ra từ nó không có trong `source-analysis.md`; cần chấp nhận như ví dụ dựng, ghi rõ trong ghi chú là giá trị minh họa.
6. **Định nghĩa $m_{\mathcal H}=\min_A m_A$ theo từng điểm** (thuật toán đạt giá trị nhỏ nhất có thể đổi theo $(\epsilon,\delta)$), khác cách UML gắn một thuật toán với một hàm "nhỏ nhất". Cách này làm Bài tập 01.7 rõ ràng; cần xác nhận.
7. **Thứ tự:** Mệnh đề 01.2 đặt trong §5 (trước giờ nghỉ, theo thứ tự UML), Hệ quả 01.4 trong §8 (sau định nghĩa PAC, vì phần (b) cần Định nghĩa 01.18). Blueprint đặt "phản ví dụ và diễn giải" sau PAC trong lịch dạy; cách chia này giữ lịch dạy và giữ kết quả đơn điệu 01.1→01.4.
8. **Thành phần 10 (Thuật toán)** đặt thành khối trong §5, không có mục riêng.
9. **Tài liệu đọc:** chia trước/sau buổi là đề xuất; blueprint chỉ có "bắt buộc" và "tùy chọn".
10. **Hệ quả 01.4(b)** bổ sung so với quyết định 9 (hàm ghi nhớ không là thuật toán học PAC dù $D$ khả thực); cần xác nhận.
11. **Thuật ngữ mới** (đánh dấu "mới" ở mục 8): phân bố biên, phân bố thực nghiệm, hầu chắc chắn, nguyên tử, nguồn ngẫu nhiên nội tại, hàm lỗi có trọng số, dương tính giả, âm tính giả, sàng lọc, rủi ro có điều kiện, học đúng lớp, học ngoài lớp. Cần thêm vào `thuat-ngu.md` mục 5.

**Rủi ro cho bản thảo:**

- **Khối PAC 30 phút chật:** ba định nghĩa có lượng từ, một ví dụ số, Mệnh đề 01.3 và hai định nghĩa bất khả tri. Giảm tải bằng cách để chứng minh Mệnh đề 01.3 tự đọc (nhãn đọc thêm).
- **Mật độ nhận xét:** 12 nhận xét có thể làm loãng mạch. Người viết giữ mỗi nhận xét 2–5 câu, có một con số hoặc một ví dụ cụ thể; không viết nhận xét chỉ để nhắc lại định nghĩa.
- **Lẫn hai bản của ví dụ sàng lọc:** mọi ví dụ phải ghi rõ $D_\eta$ hay $D_f$, mẫu $S_\eta$ hay $S_f$, hàm lỗi 0–1 hay $\ell_c$.
- **Đọc sai cỡ mẫu 14:** người đọc có thể hiểu là độ phức tạp mẫu của lớp hàm ngưỡng. Câu bắt buộc ở Ví dụ 01.8 và §9 xử lý điều này.
- **Trượt sang Bài 02:** không chứng minh bất đẳng thức hợp hay Hoeffding; UML §2.3.1 chỉ dùng để dẫn cầu nối.
- **Chép UML:** hàm ghi nhớ của ghi chú là bản một chiều; không dùng ví dụ đu đủ hay hình vuông của UML; định nghĩa PAC viết lại với $\inf$ và $\xi$.
- **Thuật ngữ:** "rủi ro kì vọng" (không "rủi ro tổng thể"), "kí hiệu", "phân bố", "kì vọng", "hàm lỗi", "hàm dự đoán"; "giả thiết" cho giả định và "giả thuyết" cho $h$, hai từ dễ gõ nhầm.
