I have read all the required documents. Now I'll produce the plan as requested by the coordinator. The task is to create a plan (not to edit the file), organized by section with specific changes.

# Kế hoạch sửa ghi chú Bài 03 theo văn phong tác giả

## ### mo-dau (Câu hỏi mở đầu đến hết §3)

1. **Dòng 5** — "Ba công cụ là chiều Vapnik–Chervonenkis (VC dimension), gọi tắt là chiều VC, hàm tăng trưởng (growth function) và mẫu bóng (ghost sample)." → Chuyển ba đối tượng song song thành danh sách gạch đầu dòng (quy tắc "ba ý song song trở lên thành danh sách"). Giữ nguyên tên tiếng Anh và số liệu.

2. **Dòng 13** — "Câu trả lời bằng số cho lớp hàm ngưỡng nằm ở §8: theo cận của bài, $54\,330$ quan sát là đủ." → Cắt chỉ dẫn điều hướng "nằm ở §8"; giữ nguyên con số $54\,330$ (bài tập trích dẫn). Viết lại: "Theo cận của bài, $54\,330$ quan sát là đủ cho lớp hàm ngưỡng."

3. **Dòng 21 (Mục tiêu học tập)** — "…trên các cách gán nhãn của chính mẫu huấn luyện." → Đổi thuật ngữ "mẫu huấn luyện" → "tập huấn luyện" (§5 van-phong-tac-gia).

4. **Dòng 29 (Kiến thức tiên quyết)** — "tính khả thực, hai định nghĩa học PAC" → "tính khả diễn" (§5).

5. **Dòng 43 (Lời giải câu hỏi ôn nhanh)** — "nên hàm chỉ thị cho $0$, $1$, $1$." → "hàm chỉ thị" → "hàm chỉ báo" (§5).

6. **Dòng 59 (§1, mục 2)** — "**Mẫu.** $S=(Z_1,\ldots,Z_m)\sim D^m$, với $Z_i=(X_i,Y_i)$, theo (T1)." → Đổi nhãn "**Mẫu.**" → "**Tập huấn luyện.**" (§5; "mẫu" chỉ dữ liệu huấn luyện).

7. **Dòng 60 (§1, mục 3)** — "…điều kiện đo được của lớp nêu ở §7." → Cắt chỉ dẫn điều hướng "nêu ở §7".

8. **Dòng 62 (§1, mục 5)** — "…hoặc một $\epsilon_{\mathrm{opt}}$-ERM (§8)." → Cắt chỉ dẫn điều hướng "(§8)".

9. **Dòng 63 (§1, mục 6, Mục tiêu)** — "**Mục tiêu.** Hai đại lượng cần chặn: *độ lệch đều* (uniform deviation) $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$ giữa rủi ro thực nghiệm (empirical risk) và rủi ro kì vọng (population risk), và rủi ro vượt mức $L_D(\hat h)-\inf_{h\in\mathcal H}L_D(h)$ của nghiệm ERM $\hat h$." → Chuyển thành danh sách, mỗi đại lượng một công thức (§6b): hai gạch đầu dòng "Độ lệch đều (uniform deviation): $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$" và "Rủi ro vượt mức (excess risk): $L_D(\hat h)-\inf_{h\in\mathcal H}L_D(h)$". Giữ nguyên công thức.

10. **Dòng 64 (§1, mục 7, Đối tượng so sánh)** — "**Đối tượng so sánh.** $\inf_{h\in\mathcal H}L_D(h)$; với lớp vô hạn, cận dưới đúng này có thể không đạt (Nhận xét 01.17)." → Giữ nhãn "**Đối tượng so sánh.**" và công thức ngay sau tên (§6b). Cân nhắc cắt "(Nhận xét 01.17)" nếu không cần thiết cho mạch chính (nhận xét bên lề).

11. **Dòng 65 (§1, mục 8, Tài nguyên)** — "…viết theo một đại lượng của lớp (định nghĩa ở §4), $\epsilon$ và $\delta$…" → Cắt chỉ dẫn điều hướng "(định nghĩa ở §4)".

12. **Dòng 76 (§2)** — "Bảng dưới gồm các kí hiệu dùng ngay từ §3; chiều VC, hàm tăng trưởng và mỗi kí hiệu khác được đặt tên tại định nghĩa của nó." → Cắt chỉ dẫn điều hướng "dùng ngay từ §3" và "đặt tên tại định nghĩa của nó".

13. **Dòng 86 (§2)** — Đoạn "Các giả thiết (T1), (T2), (T3) của Bài 01–02 được dùng lại. Giả thiết (T4) đòi lớp hữu hạn, nên được thay bằng (T5) ở §7; điều kiện đo được (M) cũng nêu ở §7. Hai mức (O1), (O2) của giả thiết tối ưu dùng ở §8; giả thiết khả thực chỉ dùng trong phần cuối của §8. Không kết quả nào dùng giả thiết lồi, trơn hay Lipschitz." → **Tái cấu trúc theo §6b**: thay bằng danh sách gạch đầu dòng có nhãn đậm, mỗi mục một công thức, nêu tập trung mọi giả thiết dùng trong bài: (T1), (T2), (T3) (từ Bài 01–02), (T5) "Lớp cố định trước khi lấy mẫu", (M) "điều kiện đo được (lớp con đếm được xấp xỉ theo từng điểm)", (O1), (O2). Bỏ các câu kiểu "(T5) … được nêu ở §7", "giả thiết … chỉ dùng ở §8", "được nêu ở chỗ dùng lần đầu". Bỏ câu "Không kết quả nào dùng giả thiết lồi, trơn hay Lipschitz" (nhận xét bên lề). Đổi "khả thực" → "khả diễn". Các chỗ sau (§7, §8) chỉ tham chiếu nhãn, không định nghĩa lại.

14. **Dòng 98 (§3, Ví dụ 03.1)** — "Ví dụ chỉ xét lớp và các bộ điểm, không cần phân bố." → Cắt nhận xét bên lề.

15. **Dòng 106 (§3, Ví dụ 03.1)** — "**Kết luận.** Rủi ro thực nghiệm $L_S(h_t)$ chỉ phụ thuộc véc-tơ trên, nên trên mỗi mẫu nó nhận nhiều nhất $m+1$ giá trị khác nhau khi $t$ chạy trên $\mathbb R$. Điều này chưa cho phép thay $K$ bằng $m+1$ trong Định lý 02.14; §7 giải thích vì sao." → Bỏ nhãn "**Kết luận.**" (gộp vào mạch văn hoặc "Tóm lại,"); cắt chỉ dẫn điều hướng "§7 giải thích vì sao".

16. **Dòng 139 (§3, Ví dụ 03.2)** — "Ví dụ không cần phân bố." → Cắt nhận xét bên lề.

17. **Dòng 159 (§3, Ví dụ 03.2)** — "**Kết luận.** Lớp sáu hàm ngưỡng mà Bài 02 dùng với $K=6$ chính là thu hẹp của một lớp vô hạn lên năm điểm." → Bỏ nhãn "**Kết luận.**".

## ### s4 (Thu hẹp, tách trọn và chiều VC)

1. **Dòng 357 (§6, nhưng nằm trong §4 về tính chất tập con)** — "theo tính chất tập con sau Định nghĩa 03.2" → Cắt chỉ dẫn điều hướng.

2. **Dòng 196 (Chứng minh Mệnh đề 03.5)** — Giữ nhãn "**Lộ trình.**" và câu lộ trình (quy tắc khóa học).

3. **Dòng 202** — "$\square$ Lớp $\mathcal H_{\mathrm{thr}}$ vô hạn nhưng có chiều VC bằng $1$; chiều VC đo khả năng gán nhãn tự do của lớp, không đo số phần tử." → Giữ nguyên (kết quả, không cắt).

4. **Dòng 234** — "Cả hai chứng minh cận trên dùng thứ tự của các điểm trên đường thẳng." → Giữ nguyên (mạch chính).

## ### s5 (Nửa không gian và hàm phân lớp tuyến tính)

1. **Dòng 251** — "…quy ước này được dùng trong chứng minh cận trên dưới đây." → Cắt chỉ dẫn điều hướng "được dùng trong chứng minh cận trên dưới đây".

2. **Dòng 291** — "…vì ma trận có các hàng $(x_i^\top,1)$ khả nghịch (Bài tập 03.3)." → Cân nhắc cắt "(Bài tập 03.3)" (chỉ dẫn điều hướng; chỉ giữ khi người đọc phải mở để lấy số/kết quả).

3. **Dòng 306** — "**Bước 4 ((b), cận trên).** Cận trên $d\le p$ được chứng minh ở Phụ lục A bằng phụ thuộc tuyến tính của $p+1$ véc-tơ trong $\mathbb R^p$." → Cắt chỉ dẫn điều hướng "được chứng minh ở Phụ lục A".

4. **Dòng 308** — "$\square$ Lớp của ứng dụng ở §3 là $\mathcal H^{10}_{\mathrm{aff}}$, nên có chiều VC $d=11$; nếu chỉ dùng hai chỉ số đo, lớp $\mathcal H^2_{\mathrm{aff}}$ có $d=3$." → Cắt chỉ dẫn điều hướng "ở §3"; giữ nguyên các số $11$, $3$ (bài tập trích dẫn).

5. **Dòng 312 (Ví dụ 03.3)** — "Ví dụ chỉ xét lớp, không cần phân bố hay mẫu." → Cắt nhận xét bên lề.

6. **Dòng 325** — "…nhận xét sau cho thấy điều đó không đúng nói chung." → Cắt chỉ dẫn điều hướng "nhận xét sau cho thấy".

7. **Dòng 334** — "Số tham số không cho cận trên, cũng không cho cận dưới, của chiều VC." → Giữ nguyên (kết luận then chốt).

## ### s6 (Hàm tăng trưởng và bổ đề Sauer–Shelah)

1. **Dòng 351** — "…và $2m$ trong chứng minh ở §7." → Cắt chỉ dẫn điều hướng "trong chứng minh ở §7".

2. **Dòng 357** — "theo tính chất tập con sau Định nghĩa 03.2" → Cắt chỉ dẫn điều hướng.

3. **Dòng 380 (Ví dụ 03.4)** — "**Kết luận.** Hai hàm tăng trưởng là đa thức bậc $1$ và bậc $2$ của $m$; bậc trùng với chiều VC." → Bỏ nhãn "**Kết luận.**".

4. **Dòng 397 (Chứng minh Bổ đề 03.12)** — "…các trường hợp gốc và điểm lặp ở Phụ lục B." → Cắt chỉ dẫn điều hướng "ở Phụ lục B". Giữ nhãn "**Lộ trình của (a).**".

5. **Dòng 467 (Ví dụ 03.5)** — "**Kết luận.** Dạng đóng lỏng hơn tổng nhị thức khi $m$ nhỏ, nhưng đủ để thấy lôgarit của số cách gán nhãn không vượt quá cỡ $d\ln m$." → Bỏ nhãn "**Kết luận.**".

## ### s7 (Hội tụ đều trên lớp có chiều VC hữu hạn)

1. **Dòng 474** — "Để biến ước lượng cuối §6 thành một bảo đảm… Định nghĩa sau gọi đó là một tính chất của lớp." → Cắt chỉ dẫn điều hướng "cuối §6" và "Định nghĩa sau gọi đó là một tính chất của lớp".

2. **Dòng 496** — "Một lớp hữu hạn chọn trước mẫu có tính chất hội tụ đều, với $m^{UC}_{\mathcal H}(\epsilon,\delta)\le\lceil\ln(2K/\delta)/(2\epsilon^2)\rceil$ theo Định lý 02.14(c). Ví dụ sau là một lớp không có tính chất này." → Cắt chỉ dẫn điều hướng "Ví dụ sau là một lớp không có tính chất này"; đổi "chọn trước mẫu" → "chọn trước khi lấy mẫu".

3. **Dòng 512** — "…nên có thể không đo được (Phụ lục A(v) của Bài 01)." → Cân nhắc cắt "(Phụ lục A(v) của Bài 01)" (chỉ dẫn điều hướng; chỉ giữ khi người đọc phải mở để lấy số/kết quả).

4. **Dòng 514 (định nghĩa (M))** — Sau khi chuyển (M) lên §2 theo §6b, dòng này chỉ tham chiếu nhãn "(M)", không định nghĩa lại. Giữ công thức đầy đủ ở §2.

5. **Dòng 516** — "…và tập $E_m(D,\epsilon)$ của Định nghĩa 03.13 đo được với mọi $D$. Không có một điều kiện như vậy, các xác suất dưới đây có thể không xác định." → Cắt chỉ dẫn điều hướng "các xác suất dưới đây" và câu liệt kê phủ định "Không có một điều kiện như vậy…" (quy tắc cắt liệt kê phủ định).

6. **Dòng 519** — "…với lớp con gồm các tham số hữu tỉ (Phụ lục D)." → Cắt chỉ dẫn điều hướng "(Phụ lục D)".

7. **Dòng 524** — "Trên một mẫu $S$, như Ví dụ 03.1 và đoạn sau Định nghĩa 03.1 đã chỉ ra, lớp chỉ tạo ra…" → Cắt chỉ dẫn điều hướng "như Ví dụ 03.1 và đoạn sau Định nghĩa 03.1 đã chỉ ra".

8. **Dòng 527** — "…đúng điều mà (T4) cấm ở Bước 2 của chứng minh Định lý 02.14." → Cắt chỉ dẫn điều hướng "ở Bước 2 của chứng minh Định lý 02.14".

9. **Dòng 531 (định nghĩa (T5))** — "**(T5) Lớp cố định trước mẫu.** $\mathcal H$, hữu hạn hoặc vô hạn, được chọn trước và không phụ thuộc $S$." → Chuyển định nghĩa (T5) lên §2 theo §6b; ở đây chỉ tham chiếu nhãn "(T5)". Đổi "trước mẫu" → "trước khi lấy mẫu".

10. **Dòng 631 (Ví dụ 03.7)** — "**Kết luận.** Với mười chỉ số đo, cận độ lệch đều là $0{,}762$ ở $10^3$ quan sát và $0{,}280$ ở $10^4$ quan sát; đây là cận trên của độ lệch đều, không phải giá trị của nó. Dạng hằng số $4$ lớn hơn dạng trực tiếp từ $1{,}33$ đến $1{,}37$ lần." → Bỏ nhãn "**Kết luận.**"; giữ nguyên mọi con số.

11. **Dòng 634** — "Định lý 03.15 dùng (T5) ở Bước 3. Trong ví dụ sau, ta bỏ (T5) và giữ chiều VC nhỏ." → Cắt chỉ dẫn điều hướng "Trong ví dụ sau".

12. **Dòng 641 (Ví dụ 03.8)** — "gồm hàm hằng $0$ và hàm chỉ thị của $F$" → "hàm chỉ thị" → "hàm chỉ báo" (§5).

13. **Dòng 658 (Ví dụ 03.8)** — "**Kết luận.** Chiều VC nhỏ không đủ; lớp phải cố định trước mẫu." → Bỏ nhãn "**Kết luận.**"; đổi "trước mẫu" → "trước khi lấy mẫu".

## ### s8 (ERM, định lý cơ bản và cận dưới)

1. **Dòng 687, 694, 800, 802, 806, 858, 930** — "bất khả tri" → "bất khả diễn" (§5).

2. **Dòng 699** — "Độ phức tạp mẫu $m_{\mathcal H}$ ở đây là bản mở rộng sang trường hợp bất khả tri, như sau Hệ quả 02.16." → Cắt chỉ dẫn điều hướng "như sau Hệ quả 02.16"; đổi "bất khả tri" → "bất khả diễn".

3. **Dòng 720** — "$\square$ Hệ số $2$ đến từ hai phép so sánh, tại $\hat h$ và tại $h$, như ở Bài 02; cận dưới đúng thay cho giá trị nhỏ nhất mà không làm thay đổi hằng số." → Cắt chỉ dẫn điều hướng "như ở Bài 02".

4. **Dòng 747 (Ví dụ 03.9)** — "**Kết luận.** Theo cận của bài, $54\,330$ quan sát là đủ cho câu hỏi mở đầu, và $447\,194$ quan sát là đủ cho câu hỏi thực hành ở §3 với mười chỉ số đo. …" → Bỏ nhãn "**Kết luận.**"; cắt chỉ dẫn điều hướng "ở §3"; giữ nguyên mọi con số ($54\,330$, $447\,194$, $3{,}36$, $11/3\approx3{,}67$).

5. **Dòng 775 (Ví dụ 03.10)** — "**Kết luận.** Với các hằng số của bài, cỡ mẫu theo cận VC lớn hơn cỡ mẫu của lớp đã rời rạc hóa từ $4{,}5$ đến $5{,}7$ lần (Bước 1–2), và bán kính VC lớn hơn $r_m$ khoảng $4{,}25$ lần (Bước 4), chủ yếu do hằng số $8$ của mẫu bóng. …" → Bỏ nhãn "**Kết luận.**"; cắt chỉ dẫn điều hướng "(Bước 1–2)", "(Bước 4)"; giữ nguyên mọi con số.

6. **Dòng 778** — "Định lý sau phát biểu điều kiện cần, và gom các khái niệm học của Bài 01–03 vào một danh sách tương đương." → Cắt chỉ dẫn điều hướng "Định lý sau phát biểu điều kiện cần". Giữ nguyên dẫn nguồn UML (nguồn có tên, không phải chỉ dẫn điều hướng nội bộ).

7. **Dòng 811** — "UML §6.4 phát biểu định lý này. Các phép kéo theo của (b) đến từ các kết quả sau." → Cắt chỉ dẫn điều hướng "Các phép kéo theo của (b) đến từ các kết quả sau".

8. **Dòng 819** — "Điều kiện (M) chỉ được dùng cho điều kiện đủ, ở phép kéo theo (6)⇒(1)." → Cân nhắc cắt (bình luận về chỗ dùng của tiên quyết, quy tắc cắt "chỉ dùng ở §8" kiểu câu).

9. **Dòng 858** — "…bỏ thừa số này cần kỹ thuật xích (chaining), ngoài phạm vi của học phần (UML §28.1)." → Cân nhắc cắt "ngoài phạm vi của học phần" (nhận xét bên lề); giữ dẫn nguồn UML.

## ### s9-12 (Ý nghĩa, Bài tập, Câu hỏi cuối buổi, Tài liệu đọc)

1. **Dòng 868 (§9)** — "Phân lớp nhiều lớp (multiclass classification), chi phí tính toán của ERM và độ phức tạp Rademacher (Bài 07) nằm ngoài bài." → Cắt chỉ dẫn điều hướng "(Bài 07)". Giữ nội dung giới hạn (đây là §9 "giới hạn").

2. **Dòng 872 (§9)** — "Trong trường hợp khả thực, Định lý 03.19(b) chỉ cho cận dưới cỡ $(d+\ln(1/\delta))/\epsilon$; cận trên tương ứng ở UML §28.3." → "khả thực" → "khả diễn" (§5). Giữ dẫn nguồn UML.

3. **Dòng 907 (§11)** — "Theo đẳng thức sau Định nghĩa 01.24, với nghiệm ERM $\hat h$," → Cắt chỉ dẫn điều hướng "sau Định nghĩa 01.24".

4. **Dòng 915 (§11)** — "Câu hỏi cho Bài 04 là: với một cỡ mẫu cho trước, nên chọn lớp nào giữa các lớp lồng nhau như vậy? Bài 04 đặt tên cho hai số hạng này." → Cắt chỉ dẫn điều hướng "Câu hỏi cho Bài 04" và "Bài 04 đặt tên cho hai số hạng này" (chỉ dẫn điều hướng sang bài sau).

5. **Dòng 930 (§12)** — "…định lý cơ bản tách riêng điều kiện cần, không dùng (M); cận dưới phát biểu với miền $\epsilon<\epsilon_0$, $\delta<\delta_0$ và $d\ge2$ cho phần khả thực." → "khả thực" → "khả diễn" (§5).

## ### phu-luc (Phụ lục A–D)

1. **Dòng 976 (Phụ lục A)** — "…cùng Bước 3 của chứng minh Mệnh đề 03.9, ta được $\operatorname{VCdim}(\mathcal H^p_{\mathrm{hom}})=p$." → Cắt chỉ dẫn điều hướng "cùng Bước 3 của chứng minh Mệnh đề 03.9".

2. **Dòng 397 (đã nêu ở s6)** — "các trường hợp gốc và điểm lặp ở Phụ lục B" → cắt chỉ dẫn điều hướng.

3. **Dòng 519 (đã nêu ở s7)** — "(Phụ lục D)" → cắt chỉ dẫn điều hướng.

4. **Dòng 306 (đã nêu ở s5)** — "được chứng minh ở Phụ lục A" → cắt chỉ dẫn điều hướng.

5. **Dòng 1114 (Phụ lục C)** — "$\square$ Mọi giả thiết đều được dùng: (T1) ở C.2 và C.3, tính bị chặn của hàm lỗi ở C.2 và C.4, (T5) ở C.4, (M) ở C.1 và C.7, chiều VC hữu hạn ở C.6." → Giữ nguyên (tóm tắt chỗ dùng giả thiết, phù hợp với phụ lục; không phải chỉ dẫn điều hướng thừa).

## ### chung (quy tắc áp dụng cho mọi phần)

1. **Thuật ngữ (§5 van-phong-tac-gia):** đổi toàn bài "khả thực" → "khả diễn", "bất khả tri" → "bất khả diễn", "hàm chỉ thị" → "hàm chỉ báo", "mẫu huấn luyện"/"mẫu" (chỉ dữ liệu huấn luyện) → "tập huấn luyện", "trước mẫu" → "trước khi lấy mẫu". Giữ "cỡ mẫu", "lấy mẫu", "mẫu bóng", "mẫu gộp", "mẫu $S$", "mẫu $s$" (tên mẫu cụ thể).

2. **Giả thiết tập trung ở §2 (§6b):** mọi giả thiết (T1), (T2), (T3), (T5), (M), (O1), (O2) nêu thành danh sách gạch đầu dòng có nhãn đậm, mỗi mục một công thức; bỏ câu kiểu "nêu ở §7", "chỉ dùng ở §8", "được nêu ở chỗ dùng lần đầu". Các chỗ sau chỉ tham chiếu nhãn. (M) cần khái niệm "lớp con đếm được" — nêu bằng lời ngắn/công thức dùng kí hiệu đã có, giữ quy tắc "định nghĩa trước khi dùng".

3. **Mục tiêu §1 thành danh sách (§6b):** mỗi đại lượng một công thức; mô tả bằng lời thay bằng công thức.

4. **Công thức hiển thị ngay sau tên (§6b):** giữ nhãn "**Đối tượng so sánh.**" và công thức $\inf_{h\in\mathcal H}L_D(h)$ ngay sau.

5. **$\sup$ thay cho $\max$** cho độ lệch đồng thời trên lớp giả thuyết (đã dùng $\sup$ đúng chỗ; kiểm tra không còn $\max$ cho độ lệch đồng thời).

6. **Cắt:** câu rào đón, chỉ dẫn điều hướng ("ở §…", "Phụ lục … chứng minh", "Ví dụ sau", "như sau Hệ quả …", "Bài 04 đặt tên"), bình luận kĩ thuật, nhận xét bên lề không dùng lại, câu nói hiển nhiên, đoạn tự hỏi tự đáp, liệt kê phủ định. Chỉ giữ một dẫn chiếu khi người đọc phải mở nơi được dẫn để lấy số/kết quả.

7. **Bỏ nhãn "**Kết luận.**"** ở mọi Ví dụ (03.1, 03.2, 03.3, 03.4, 03.5, 03.6, 03.7, 03.8, 03.9, 03.10): gộp vào mạch văn hoặc "Tóm lại,".

8. **Giữ:** mọi khối đánh số (Định nghĩa 03.1–03.13, Mệnh đề 03.5, 03.6, 03.9, Bổ đề 03.8, 03.12, Định lý 03.15, 03.17, 03.19, Hệ quả 03.16, 03.18, Ví dụ 03.1–03.10, Nhận xét 03.4, 03.10, 03.14), mọi con số, mọi kết quả và nhãn mà `exercises.md` trích dẫn (Định nghĩa 03.11, 03.13, Mệnh đề 03.5, 03.6, 03.9, Bổ đề 03.12, Định lý 03.15, 03.17, Hệ quả 03.16, Nhận xét 03.4, 03.10, 03.14, Ví dụ 03.4, 03.6, 03.7, 03.8, 03.9, 03.10, các số $54\,330$, $447\,194$, $132\,992$, $0{,}762$, $0{,}280$, $d=11$, $d=3$, $d=1$, $d=2$, $d=4$, $d=p+1$, $d=p$, $d=2p$, $d=p$, $d\le p\log_23$, $d=p$, $d\le p+2$, $d\ge p+1$, $\Pi_{\mathcal H_{\mathrm{thr}}}(m)=m+1$, $\Pi_{\mathcal H_{\mathrm{int}}}(m)=\binom{m+1}2+1$, $\Pi_{\mathcal H^{2}_{\mathrm{aff}}}(4)\le14$, $\rho_m$, $m^{UC}_{\mathcal H}$, $M(\epsilon,\delta)$, $\lceil\ln(2K/\delta)/(2\epsilon^2)\rceil$, $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$).

9. **Giữ nhãn "**Lộ trình.**"** và câu lộ trình đầu mỗi chứng minh (quy tắc khóa học).

10. **Giữ dòng "Giả thiết.**/**Bảo đảm.**"** của mọi kết quả; định nghĩa trước khi dùng.

11. **Giọng văn:** chủ ngữ là thuật toán/hàm/"ta", động từ trực tiếp; từ nối giải thích ("Nghĩa là", "Do đó", "Tóm lại"); in nghiêng thuật ngữ mới ở lần đầu, in đậm ý then chốt (dùng tiết kiệm); gọi đủ tên thuật ngữ ("lớp giả thuyết", không "lớp").

12. **Tên tiếng Anh thường dùng ở lần đầu:** kiểm tra các thuật ngữ mới của Bài 03 đã kèm tiếng Anh (VC dimension, growth function, ghost sample, labeling, shatters, restriction, uniform deviation, excess risk, Radon partition, simplex, hyperplane, countable subclass, pointwise limit, combined sample, random signs, discretization, chaining, multiclass classification) — giữ nguyên.

13. **Markdown:** chỉ dùng $...$ và $$...$$; không đổi kí hiệu toán; không thêm khẳng định, số liệu, nguồn không có trong bản hiện tại; chỉ cắt câu, không cắt kết quả.

14. **no-ai-slop:** không thêm nhận xét tác giả, không thêm câu kết thúc giả tạo, không thêm lời dẫn dắt; giữ nguyên giọng văn của tác giả ở các câu đã chuẩn.

---

**Ghi chú về các điểm cần phán quyết của điều phối viên/tác giả** (không tự sửa):
- Dòng 64: giữ hay cắt "(Nhận xét 01.17)" về cận dưới đúng không đạt.
- Dòng 512: giữ hay cắt "(Phụ lục A(v) của Bài 01)".
- Dòng 291: giữ hay cắt "(Bài tập 03.3)".
- Dòng 819: giữ hay cắt câu "Điều kiện (M) chỉ được dùng cho điều kiện đủ".
- Dòng 858: giữ hay cắt "ngoài phạm vi của học phần".
- Dòng 56 (§1): câu "Bài toán giữ tám thành phần của §1 Bài 02" — chỉ dẫn điều hướng sang Bài 02; cân nhắc cắt hoặc viết lại gọn.

Không commit; chỉ lập kế hoạch.