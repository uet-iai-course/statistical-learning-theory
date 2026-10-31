# Rà lại 5 (kết hợp toán, mạch, văn phong) sau biên tập vòng 2, Bài 06

Người rà: tác tử rà mạch và móc nối, chỉ đọc. Đối tượng: `scratchpad/lec06-r2-frozen.md`, trùng `2627-1/materials/lec-06/lecture-note.md` (`diff -q` rỗng), thân bài 11 989 tiếng (`wc -w`). Căn cứ: `lec06-r2.udiff`, `reviews06/6-ra-lai-toan.md` (R2'), `reviews06/7-ra-lai-mach.md` (R5'), mục "Vòng 2" của `bien-tap-vong-1.md`, `outline.md` §13.2. Văn phong kiểm theo `no-ai-slop` chế độ Detect và `van-phong.md` §7a, §9, §9a. Số dòng là số dòng của `lec06-r2-frozen.md`.

**Tổng kết:** 19/19 phát hiện của hai báo cáo rà lại đã xử lý: R2' 3/3 ✓, R5' 16/16 ✓. Phát hiện mới: 0 `chặn bàn giao` · 0 `nghiêm trọng` · 1 `trung bình` · 3 `nhẹ`.

`forward_refs.py` (chạy từ gốc repo trên bản sao `scratchpad/reviews06/r5c/lec-06/lecture-note.md`): **0 forward references**. Đọc tay các câu đã đổi: không có kí hiệu hay số hiệu mới nào dùng trước định nghĩa. Câu 547 dẫn "cuối Phụ lục A" (dòng 1180 có câu về tính đo được); dẫn phụ lục từ thân bài được phép.

## 1. Phát hiện của hai báo cáo rà lại

| Nguồn | Phát hiện | Trạng thái | Bằng chứng (dòng mới) |
|---|---|---|---|
| R2' trung bình | Câu chọn bằng hàm lỗi 0–1 cho hồi quy logistic sai | ✓ | 1051: câu bị bỏ, thay bằng câu nói phạm vi: hàm lỗi không bị chặn cần một cận trên các ứng viên, ngoài phạm vi bài. Câu thay đúng về toán. Không thêm cận $\ln2+\sqrt{2\ln2/\lambda}$; lý do (ngoài phạm vi theo QĐ) hợp lệ |
| R2' nhẹ | 547 thiếu tính đo được | ✓ | 547 "(tính đo được giả sử như cuối Phụ lục A)"; 1180 có câu tương ứng |
| R2' nhẹ | Phụ lục E "hàm giảm" | ✓ | 1285 "hàm không tăng" |
| R5' M1 | Hai nghĩa của "số hạng khớp/ổn định"; câu kết Ví dụ 06.12 sai | ✓ | 901 bỏ tên; 937 giữ tên cho các số hạng của cận; 1036 "khoảng cách tổng quát hóa bằng $0$". Câu nguyên nhân mới đúng nhưng lặp vòng (N1) |
| R5' M2 | §10 "chủ yếu"; thiếu $0{,}0011$ | ✓ | 1062 |
| R5' M3 | Câu mở §7 | ✓ | 591 |
| R5' M4 | Câu đứng riêng cuối §9 | ✓ | đã cắt; §9 kết bằng Nhận xét 06.15, §10 mở bằng câu trả lời câu hỏi trung tâm, mạch liền |
| R5' M5 | Kết §3, §6, §8 | ✓ | `outline.md` §13.2 mục 5 |
| R5' M6 | $\hat w$, $\hat w'$ ở Ví dụ 06.7 | ✓ | 845 |
| R5' M7 | "Bước 1–3 là các đẳng thức" | ✓ | 713, 1293; về toán, xem N3 |
| R5' M8 | "nói chung không lồi" | ✓ | 1075 |
| R5' M9 | Câu "bất đẳng thức oracle" | ✓ | 937 |
| R5' M10 | Tiêu đề Bài tập 06.7, 06.9 | ✓ | 1087, 1089; `outline.md` 343, 345 đồng bộ. Riêng `outline.md` dòng 381 còn ghi "UML §13.2 (thuật toán ổn định …)", khác ghi chú 1137 "quy tắc ổn định …"; tệp planning, nhẹ, không tính |
| R5' M11 | "Bước 4 cần …" | ✓ | 413 |
| R5' M12 | Câu dài ở Nhận xét 06.14 | ✓ | 1051 tách ba câu, chủ ngữ "ta"; nội dung còn thiếu kết luận (T1 dưới) |
| R5' M13 | Câu dài 117 | ✓ | 117 |
| R5' M14 | Câu hai nghĩa 882 | ✓ | 882 |
| R5' M15 | "(Bài 07)" | ✓ | 854 "(chứng minh ở Bài 07)" |
| R5' M16 | 896, 1140 | ✓ | 896, 1138 |

## 2. Toán của các câu đã đổi

- **Ví dụ 06.12, câu kết (1036).** Với $D$ suy biến tại $(1,1)$, $L_S=L_D=(w-1)^2$ trên mọi mẫu, nên khoảng cách tổng quát hóa bằng $0$ (đúng). Với $u=1$, $L_S(u)=0$, nên $L_S(\hat w_S)-L_S(u)=L_D(\hat w_S)=(\lambda/(2+\lambda))^2$, tăng theo $\lambda$ (đúng). Câu "nguyên nhân là phần $L_S(\hat w_S)-L_S(u)$ … bằng $L_D(\hat w_S)$" đúng nhưng lặp vòng: nó giải thích rủi ro tăng bằng một đại lượng bằng chính rủi ro. Nguyên nhân thật là số hạng phạt kéo $\hat w_S=1/(1+\lambda/2)$ về $0$, và phần này bị chặn bởi số hạng khớp $\tfrac\lambda2\lVert u\rVert^2=\tfrac\lambda2$ (Bước 1 của chứng minh Hệ quả 06.13, đúng cả khi $G=\infty$). Xem N1.
- **Nhận xét 06.14, chia khối (1051).** Các số khớp với kiểm tra của R2': $k=\lceil\log_2(2/\delta)\rceil$; mỗi khối đạt mức kì vọng $\epsilon/4$; Markov cho xác suất vượt $\epsilon/2$ không quá $\tfrac12$; cả $k$ khối hỏng với xác suất $\le\delta/2$; mẫu xác thực $8\ln(4k/\delta)/\epsilon^2$ cho bán kính $\epsilon/4$ trên $k$ ứng viên. Câu về hàm lỗi không bị chặn đúng. Thiếu sót: ý này không còn nói thủ tục đạt được gì, tức rủi ro vượt mức không quá $\epsilon$ với xác suất ít nhất $1-\delta$, với số khối tăng theo $\log(1/\delta)$ thay vì thừa số $1/\delta^2$ của ý Markov ngay trên. Người đọc thấy một thủ tục mà không thấy kết luận phân biệt nó với ý Markov. Thiếu sót này có từ vòng 1 (dòng 1051 bản r1); tôi đã không nêu ở lần rà trước. Xem T1.
- **"Các đẳng thức ở Bước 1–3 cho thấy …" (713).** Đúng: sau Định lý 06.10, mọi kì vọng đã hữu hạn (Bước 2).
- **Câu tương ứng ở Phụ lục E (1293).** Thuật toán ở Phụ lục E không được giả sử ổn định đều, nên phần chứng minh tính hữu hạn ở Bước 2 (dùng ổn định đều) không áp dụng. Đẳng thức vẫn đúng (theo nghĩa số thực mở rộng) khi $\mathbb EL_D(A(S))<\infty$, nhưng giả thiết này chưa được nêu ở Phụ lục E. Xem N3.
- **Các câu khác.** 1062 ($0{,}2261$, $0{,}0011$, $0{,}4750$ khớp Ví dụ 06.3); 1018 "Tổng là $0{,}01$"; 845 (Ví dụ 06.7, $\lambda=0$, hai nghiệm $\pm1$); 882 ($M=m$); 1285 (hàm không tăng, khớp phản ví dụ $\epsilon\equiv0$): đúng.

## 3. Mạch quanh chỗ đổi và hai chỗ cắt

- **Kết luận Ví dụ 06.4 (582) chỉ còn một câu.** Câu bị cắt dẫn sang §8 và §9; câu mở §8 (740) và §9 (901) nêu lại đúng hai ý đó bằng số của Ví dụ 06.4, nên mạch không mất. §6 kết bằng chú thích Hình 06.1, §7 mở bằng nhu cầu của Mệnh đề 06.5 (591). Liền.
- **Câu trước §10 bị cắt.** §9 kết bằng Nhận xét 06.15; §10 mở bằng câu trả lời câu hỏi trung tâm, và mục giới hạn "Nghiệm chính xác" (1071) giữ ý của câu bị cắt. Liền.
- **Nhận xét 06.14 → §10.** §10 mục "Theo kì vọng" (1070) nêu thừa số $400$ của Markov nhưng không nhắc rằng chia khối giảm được thừa số này. Kết hợp với T1, mạch "giá của Markov → cách giảm giá" bị đứt ở cả hai chỗ.
- **§2 (117) và §7 mở đầu (591):** không ảnh hưởng mạch.

## 4. Văn phong các câu mới

Không có mẫu no-ai-slop nào trong các câu mới, trừ câu lặp vòng ở 1036 (N1). Các câu 591, 937, 896, 1051, 1062 thẳng, có chủ ngữ, đúng §9a. Lỗi trình bày nhỏ: 1051 "((T3) của Hệ quả 04.17)" có hai dấu ngoặc mở liền nhau (N2).

## 5. Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | Nhận xét 06.14, ý "Chia khối và xác thực", 1051 | Ý này mô tả thủ tục mà không nói thủ tục bảo đảm gì, nên không phân biệt được với ý Markov ngay trên (thừa số $1/\delta^2$). Đây là lý do ý này nằm trong nhận xét về bảo đảm với xác suất cao. | "… ta chia mẫu thành $k=\lceil\log_2(2/\delta)\rceil$ khối độc lập, mỗi khối đủ cho mức kì vọng $\epsilon/4$. Ta chọn đầu ra bằng một mẫu xác thực cỡ $8\ln(4k/\delta)/\epsilon^2$ (Bài tập 06.7)." Không có câu kết luận. | Thêm sau câu thứ hai: "Khi đó, với xác suất ít nhất $1-\delta$, đầu ra có rủi ro vượt mức không quá $\epsilon$, và cỡ mẫu tăng theo $\ln(1/\delta)$ thay vì $1/\delta^2$." (+27 tiếng). Cắt bù: 117, câu "Tính bị chặn của dữ liệu chỉ cần cho một hằng số $G$ hữu hạn của hàm lỗi bình phương." (−17), vì §1 mục 1 (85) đã nêu điều kiện này cho hàm lỗi bình phương; 1040, câu dẫn "Ba điểm phân biệt hai loại bảo đảm." (−6), vì ba nhãn in đậm đã đủ rõ. Cùng N1, thân bài khoảng 11 996. |
| nhẹ | Ví dụ 06.12 Kết luận, 1036 câu thứ hai | Câu nguyên nhân lặp vòng: rủi ro tăng "vì" một đại lượng bằng chính rủi ro. Ví dụ không còn nối với số hạng khớp của Hệ quả 06.13, vốn là lý do ví dụ đứng ở §9. | "Nguyên nhân là phần $L_S(\hat w_S)-L_S(u)$ với $u=1$, bằng $L_D(\hat w_S)$ và tăng theo $\lambda$." | "Số hạng phạt kéo $\hat w_S$ về $0$, xa điểm tốt nhất $u=1$; Bước 1 của chứng minh Hệ quả 06.13 chặn phần tăng này bởi số hạng khớp $\tfrac\lambda2\lVert u\rVert^2=\tfrac\lambda2$." (khoảng +6 tiếng; đúng cả khi $G=\infty$, vì Bước 1 không dùng (L)). |
| nhẹ | Nhận xét 06.14, 1051 | Hai dấu ngoặc mở liền nhau. | "trong $[0,1]$ ((T3) của Hệ quả 04.17)" | "trong $[0,1]$, tức (T3) của Hệ quả 04.17," (±0). |
| nhẹ | Phụ lục E, 1293 (ngoài trần thân bài) | Đẳng thức "khoảng cách tổng quát hóa kì vọng bằng đúng vế trái" cần $\mathbb EL_D(A(S))<\infty$. Ở §7, tính hữu hạn của các số hạng còn lại đến từ ổn định đều; thuật toán ở Phụ lục E không có giả thiết này, và giả thiết khả tích chưa được nêu. | "Các đẳng thức ở Bước 1–3 của chứng minh Định lý 06.10 cho thấy khoảng cách tổng quát hóa kì vọng bằng đúng vế trái trên." | Thêm vào câu định nghĩa (1285): "… và $\mathbb EL_D(A(S))<\infty$"; hoặc ở 1293: "Khi $\mathbb EL_D(A(S))<\infty$, các đẳng thức ở Bước 1 và Bước 2 (phần đổi vai) cho thấy …" (phụ lục, ngoài trần). Đề nghị người rà toán xác nhận. |
