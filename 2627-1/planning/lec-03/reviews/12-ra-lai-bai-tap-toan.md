# Rà lại toán học: Bài tập Bài 03 sau vòng sửa 1

**Vai trò:** người rà soát toán học (chỉ đọc), tiếp nối báo cáo `lec03-review-9-bai-tap-toan.md`. **Đầu vào:** `2627-1/materials/lec-03/exercises.md` hiện tại (929 dòng), `lec03-ex-round1.diff`, `2627-1/planning/lec-03/reviews/11-quyet-dinh-bai-tap.md`, `git diff` của ghi chú (hai dòng §10). Số dòng dưới đây là số dòng của tệp hiện tại. Đã đọc lại toàn bộ tệp, không chỉ các đoạn đổi. Các con số mới hoặc đã đổi được đối chiếu với `scratchpad/rev9/num.py`; các khẳng định tổ hợp không đổi so với bản đã kiểm vét cạn.

## 1. Trạng thái 12 phát hiện của vòng trước

| # | Phát hiện vòng trước | Trạng thái | Bằng chứng (dòng hiện tại) |
|---|---|---|---|
| 1 | 03.9 Gợi ý 1: "khi và chỉ khi" sai (trung bình) | ✓ | Dòng 675: "Khi $a_l\le0\le b_l$ với mọi $l$, hình chữ nhật chứa $\mathbf e_j$ khi và chỉ khi $b_j\ge1$." Gợi ý 1 mới (dòng 671) chỉ định hướng, đúng. |
| 2 | 03.8: "chặt" hai nghĩa; "một điểm âm" | ✓ | Dòng 589: "đạt dấu bằng"; dòng 649: "là bất đẳng thức nghiêm ngặt khi $C$ có ít nhất hai điểm không âm … ít nhất một điểm âm". |
| 3 | 03.8(c): trích Mệnh đề 03.5 quá rộng | ✓ | Dòng 655: "$h_x(x)=1$ và $h_{x+1}(x)=0$. Theo Bước 2 của chứng minh Mệnh đề 03.5, không tập hai điểm nào bị tách trọn." |
| 4 | 03.6(d) Bước 1: thiếu viện dẫn phép đếm $w$ | ✓ | Dòng 514: "Theo Bước 1 của (c), $w(T_j(Y^*))=w(Y^*)-k$; vì $T_j(Y^*)=Y^*$ nên $k=0$". |
| 5 | 03.4: vai của $\epsilon$ "trong cả bài" | ✓ | Dòng 216: "Trong (a), (b), (e), $\epsilon$ là cận cho rủi ro vượt mức …; trong (c), $\epsilon$ là độ lệch đều". (d), (f) không dùng $\epsilon$. |
| 6 | 03.4(b): "bằng" thay cho "xấp xỉ bằng" | ✓ | Dòng 282: "$m\approx12\,800\big(d\ln(2em/d)+\ln80\big)$, nên tỉ số xấp xỉ bằng tỉ số của hai ngoặc". |
| 7 | 03.4(a): số bị cắt cụt | ✓ | Dòng 264–265: bốn giá trị mười chữ số, khớp tính lại (mục 2). |
| 8 | 03.11: $D$ phụ thuộc $A$, $m$; tính tất định | ✓ | Dòng 773 "phụ thuộc $A$ và $m$"; dòng 825 nhắc lại; dòng 814 "$A(S)$ cố định vì $A$ là một ánh xạ của mẫu (Định nghĩa 01.4)". |
| 9 | 03.11 Gợi ý 1 lộ ý lấy trung bình | ✓ | Dòng 787 chỉ dẫn tới định lý không có bữa trưa miễn phí; ý lấy trung bình chuyển sang Gợi ý 2 (dòng 791). |
| 10 | 03.11(d): trường hợp $d\le1$ | ✓ | Dòng 856: "Khi $d\le1$, vế phải bằng $1$ …"; dòng 858 "Giả sử $d\ge2$". |
| 11 | 03.11: kí hiệu $X$ hai nghĩa | ✓ | Dòng 801 dùng $U$ cho điểm đơn; dòng 820 "$\mid X_1,\ldots,X_m,F\vert_V$". |
| 12 | Tiêu đề 03.4, 03.5 ở §10 ghi chú | ✓ | `git diff` ghi chú: hai dòng 881–882 nay trùng tiêu đề dòng 211 và 362 của tệp bài tập. |

## 2. Kiểm lại các nội dung mới hoặc đã đổi

- **03.4(a), dòng 218–276.** Điều kiện viết lại dạng $\frac{32}m(d\ln\frac{2em}d+\ln\frac4\delta)\le\epsilon^2$: tương đương $2\rho_m\le\epsilon$ theo dạng trực tiếp, đúng. Tính lại: $d=3$: $0{,}0024999964$ tại $589\,118$, $0{,}0025000003$ tại $589\,117$; $d=11$: $0{,}0024999991$ tại $1\,999\,657$, $0{,}0025000002$ tại $1\,999\,656$; đều khớp. Hai ngoặc: chính xác $36{,}912511$ và $123{,}660470$; tệp ghi $36{,}9125$, $123{,}6605$ (khớp sau làm tròn; $3\cdot10{,}8435+4{,}3820=36{,}9125$ và $11\cdot10{,}8435+4{,}3820=123{,}6605$ cũng đúng với các thừa số đã làm tròn). Tích $944\,960{,}28$, $3\,165\,708{,}02$; làm tròn lên $944\,961$, $3\,165\,709$: đúng.
- **03.4(b), dòng 280–285.** $3{,}3943$ so với tỉ số ngoặc $3{,}3943$: "xấp xỉ bằng" đúng; $12\,800=32/\epsilon^2$ với $\epsilon=0{,}05$: đúng. Bước 3: $4{,}43$, $4{,}47$, $\ln4{,}43=1{,}488$: đúng; câu "phần dôi ra đến từ $\ln(2em/d)$" đúng (ngoặc tăng $10{,}7\%$ và $11{,}8\%$).
- **03.4(c), dòng 229, 287–310.** Câu cuối của chứng minh lộ trình (ghi chú, "Hằng số $8$ trong $\rho_m$ đến từ hai nguồn") tồn tại đúng như đề dẫn. Tách thành Bước 1–3: số mũ $-2mr^2$; thừa số $4$ do $\epsilon/2$; thừa số $4$ do miền dài $2$; $-m\epsilon^2/8$; tỉ số $16$: đúng. Bước 4–5 không đổi, đúng ($2\ln4=2{,}77$; $8\ln4=11{,}09$).
- **03.4(d), dòng 312–327.** Tách Bước 3 (chỗ sai) và Bước 4 (cách sửa): nội dung giữ nguyên, đúng ($0{,}3484$, $0{,}590$).
- **03.4(e), dòng 240.** Thêm "Như Ví dụ 03.10 với $q=3$": khớp $K\le2^{64q}$ của Ví dụ 03.10. Các số $27\,355$, $4{,}86$, $16\cdot0{,}3039$ không đổi, đúng.
- **03.4(f) mới, dòng 242, 352–357.** Đối chiếu với các dòng "Chỗ dùng" của chứng minh lộ trình và câu cuối Phụ lục C ("(T1) ở C.2 và C.3, tính bị chặn của hàm lỗi ở C.2 và C.4, (T5) ở C.4, (M) ở C.1 và C.7"):
  - (T1) → Bước 1 (C.2), Bước 2 (C.3): đúng (lộ trình Bước 1 và Bước 2 đều ghi (T1)).
  - Tính bị chặn → Bước 1 (C.2) phương sai $\le\tfrac14$, Bước 4 (C.4) số hạng trong $[-1,1]$: đúng.
  - (T5) → Bước 3 (C.4): đúng (lộ trình Bước 3 ghi (T5); C.4 gộp bước lấy điều kiện và Hoeffding).
  - (M) → Bước 1 (C.1) và C.7: đúng (lộ trình Bước 1 ghi "(M) để chọn $h$ đo được theo $S$").
  - Một câu dẫn ví dụ chưa chuẩn (phát hiện N1).
- **03.5 tái cấu trúc, dòng 366–456.** (b) mới dùng lớp của Nhận xét 03.10(iii) đã được ghi chú khẳng định (ba hàm, $d=1$); lập luận "không là cận trên" (Bước 1) và "không là cận dưới với $p\ge2$" (Bước 2) đúng. (c) (trước là (d)) không đổi về toán; $\rho_{1000}=0{,}187$, $0{,}043$, "gấp hơn mười lần" ($0{,}5/0{,}04295=11{,}6$) đúng. Gợi ý được gán lại đúng phần.
- **03.6, dòng 470–528.** Bỏ phần (e) cũ; câu "Bài tập 03.8(a) chứng minh bất đẳng thức của (d) bằng quy nạp" đúng. (c) tách hai bước, đúng.
- **03.7, dòng 538–584.** Đổi tên $\mathcal H^{0/1}_{\le k}$ nhất quán ở đề và lời giải (dòng 542, 550, 576, 582). Câu bỏ đi không làm hở lập luận.
- **03.8, dòng 589–659.** "Đạt dấu bằng"/"nghiêm ngặt" đúng nghĩa. Quy nạp (a) tách thành Bước 4–7, lớp con đổi tên $\mathcal H'$ (dòng 610, 628, 630): đúng. Kiểm tra lại mới với $C=\{1,2,3\}$: bốn cách $000,001,011,111$; tập bị tách trọn $\varnothing$ và ba tập một điểm; $1+3=4$: đúng.
- **03.9, dòng 670–695.** Gợi ý sắp lại theo mức tăng dần, đúng. Lời giải tách Bước 4–5, đúng. Kiểm tra lại $p=1$ bỏ câu giải thích về $h_\varnothing$ nhưng vẫn đúng: $\mathcal H_{\mathrm{int}}\subseteq\mathcal H^1_{\mathrm{rec}}$ cho $d\ge2$, Bước 3–5 với $p=1$ cho $d\le2$.
- **03.10, dòng 705–763.** (a) chỉ dẫn Bài tập 02.8(a) (đẳng thức, mạnh hơn yêu cầu $\le$): chấp nhận được. Gợi ý (b) tách hai mức, đúng. $h_{\equiv0}$ được định nghĩa ở dòng 5.
- **03.11, dòng 773–862.** (c) Bước 4: danh sách sáu khẳng định khớp đúng thứ tự (1)–(6) của Định lý 03.17(b) trong ghi chú; "không dùng (M)" đúng. Một câu gán phép kéo theo chưa chính xác (phát hiện N2). (d) Bước 1–3 đúng; $\lfloor11/2\rfloor+1=6$.
- **03.12, dòng 870–928.** Đổi tên $\mathcal H^p_{\mathrm{ball}}$ nhất quán. (b) Bước 1 nay định nghĩa $A$, $a$, $v$ trong lời giải (trước chỉ có trong gợi ý): đúng; ba bình phương khoảng cách và các bán kính không đổi, đúng.
- **Đổi tên khác.** $\mathcal H^{(6)}_{\mathrm{thr}}$ ở 03.1 (dòng 16–64) nhất quán; viết gọn $\Pi$ ở dòng 45 rõ phạm vi. Kiểm tra lại mới của 03.1 (dòng 90): thêm hai hàm hằng vào $\mathcal H^\pm_{\mathrm{thr}}$ được $\mathcal H^1_{\mathrm{aff}}$ (đoạn sau Định nghĩa 03.7), $d=2$ theo Mệnh đề 03.9(a): đúng và nhất quán với Bước 4.
- **03.2, 03.3.** 03.2(a) thêm yêu cầu "chỉ ra chỗ khác với chứng minh Mệnh đề 03.6" (phát hiện N3). 03.3 bỏ ý $p=3$ cũ; không còn tham chiếu treo nào tới "03.3(b)" ở tệp bài tập hay ghi chú (đã grep). Hệ $p=2$ đánh số (1)–(3), khử đúng: $w_1=-2$, $w_2=0$, $b=3$.

## 3. Phát hiện mới

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | 03.4(f), dòng 356 | Phần (d) bàn về việc bỏ mẫu bóng (hợp trên các cách gán nhãn của chính $S$), không phải một lớp vi phạm (T5) với chứng minh giữ nguyên. Ví dụ cho thấy Bước 3 hỏng khi bỏ (T5) là Bài tập 03.5(c) và Ví dụ 03.8. | "Phần (d) và Ví dụ 03.8 cho thấy bước này hỏng khi bỏ (T5)." | "Bài tập 03.5(c) và Ví dụ 03.8 cho thấy bước này hỏng khi bỏ (T5)." |
| nhẹ | 03.11(c), Bước 4, dòng 852 | Bước 2 là phản đảo của (4)⇒(6). Bước 3 cho phản đảo của (3)⇒(6), qua (3)⇒(4) của Nhận xét 01.26. Gộp cả hai thành "phản đảo của (4)⇒(6)" chưa chính xác. | "Bước 2–3 là phản đảo của phép kéo theo (4)⇒(6), "học được PAC kéo theo $d<\infty$", và không dùng (M)." | "Bước 2 là phản đảo của phép kéo theo (4)⇒(6), "học được PAC kéo theo $d<\infty$"; Bước 3 thêm (3)⇒(6) qua (3)⇒(4). Cả hai bước không dùng (M)." |
| nhẹ | 03.2(a), dòng 114 | Đề (dòng 98) hỏi chỗ khác với Mệnh đề 03.6. Lời giải nói chỉ các bất đẳng thức đổi thành nghiêm ngặt, nhưng cận dưới cũng đổi: Mệnh đề 03.6 dùng khoảng một điểm $[0,0]$, $[1,1]$, mà lớp khoảng mở không có (vì $u<v$ và khoảng mở chứa nhiều điểm), nên phải dùng $(-1,\tfrac12)$, $(\tfrac12,2)$. | "Chứng minh đi theo Mệnh đề 03.6; chỉ các bất đẳng thức đổi thành nghiêm ngặt." | "Chứng minh đi theo Mệnh đề 03.6, với hai chỗ khác: ở cận trên, các bất đẳng thức đổi thành nghiêm ngặt; ở cận dưới, khoảng một điểm $[0,0]$, $[1,1]$ không thuộc lớp, nên được thay bằng $(-1,\tfrac12)$, $(\tfrac12,2)$." |

**Thống kê:** `chặn bàn giao` 0, `nghiêm trọng` 0, `trung bình` 0, `nhẹ` 3.

## 4. Kết luận

Cả 12 phát hiện vòng trước đã được sửa đúng. Mọi phát biểu, gợi ý, bước lời giải và con số mới hoặc đã đổi đều đúng; 03.4(f) gán đúng từng giả thiết vào bước của chứng minh lộ trình và Phụ lục C. Ba phát hiện mới đều nhẹ, thuộc diễn đạt hoặc dẫn chiếu, không ảnh hưởng tính đúng của lời giải.

**Kết luận: giao được** (nên sửa ba điểm nhẹ nếu còn vòng chỉnh sửa; không bắt buộc trước khi giao).
