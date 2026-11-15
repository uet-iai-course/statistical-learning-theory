# Kiểm lại deck Bài 10 sau lượt biên tập (toán học và mạch truyện)

Vai: kiểm lại sau biên tập, chỉ đọc (general-purpose, Opus 5.5, effort high theo lệnh gọi). Ngày 2026-11-16.

Đầu vào: bản đóng băng `scratchpad/lec-10/master/frozen/lecture-10-gradient-chinh-sach-hoc-lien-tuc.html`; bản sau `2627-1/lecture-10-gradient-chinh-sach-hoc-lien-tuc.html` (55 trang); `facediff2.txt` của điều phối viên; diff ghi chú diễn giả tự lập (44 trang có ghi chú đổi); ghi chú Bài 10, `exercises.md`, ghi chú Bài 05 (G1), (G2), ghi chú Bài 08 Mệnh đề 08.12; năm báo cáo `reviews/deck-*.md`; `review-log.md` mục "Bộ trang chiếu"; `storyboard.md` §12, §17.

## Kiểm máy (bản sau)

- `deck_lint.py`: 0 phát hiện trên 55 trang. Đếm lại theo luật của lint: nhiều trang ở sát trần (60: 2-03, 3-03, 3-05, 4-01, 4-08, 5-01, 5-02, 5-04, 7-03; 59: 1-06, 3-02, 3-08, 3-10, 4-02, 4-05, 4-07, 6-06, 6-07, 7-07). Mọi đề xuất sửa dưới đây đã tính âm tiết.
- `footer_check.py`: 0 trang chạm chân trang.
- `deck_check.py --shots`: slides=55, console 0, pageerrors 0, failed 0, `.katex-error` 0. OVERFLOW ở 1-02, 4-07, 6-02, 6-03, 6-07, 6-08, 7-01, 7-02: mọi phần tử tràn là `path` SVG của `\sqrt` (báo động giả đã biết).
- Liên kết `#/2`…`#/7` mở đúng L10-2-00…L10-7-00. Phím ↓ đi hết mạch 6 (6-06 có một fragment, rồi 6-07, 6-08), → sang 7-00, Space tiến, Esc mở tổng quan.
- Đã xem ảnh 1600×900 của cả 55 trang và ảnh 390×844 (kể cả `-end`) của các mạch 1, 2, 4, 6, 7. Không chồng lấn, không tràn ngang trang; bảng 2-05, 4-05, 5-03, 5-04, 6-04, 6-08, 7-01 cuộn ngang tại chỗ, có nhãn "↔ cuộn ngang".

## 1. Trạng thái các quyết định của điều phối viên

| Phát hiện (quyết định) | Trạng thái | Bằng chứng trên bản sau |
|---|---|---|
| 6-05 dòng mô phỏng (nghiêm trọng) | đã sửa, sinh lỗi mới | "Mô phỏng hồi quy $y=wx$ (Phụ lục C), $L_A=\tfrac12(w^2+0{,}25)$: … về $0{,}25$, không về $\min=0{,}125$"; "rủi ro cũ kì vọng giảm về $L_A(\tfrac12)=\tfrac58$". Khớp ghi chú Ví dụ 10.16 Bước 3–4, Phụ lục C. Lỗi mới: xem phát hiện R1. |
| 7-02 dòng 1 và ghi chú diễn giả 1-05 (nghiêm trọng) | đã sửa | "(T1) sai: $\theta_j$ phụ thuộc $\tau_1,\ldots,\tau_{j-1}$." / "(C) sai: $-J$ không lồi (Ví dụ 10.7)." / "$\theta$ cố định: (T1) đúng; …". Ghi chú 1-05: "Mục tiêu nói chung không lõm (Ví dụ 10.7)". Khớp ghi chú dòng 78, 112, 1068. |
| 7-02 (trung bình): Mệnh đề 10.13, ma trận đánh giá, đại lượng được chặn | sửa một phần, đã chấp nhận | Cận đủ: $\lvert\frac1m\sum_jR(\tau_j)-J(\theta)\rvert\le H(r_{\max}-r_{\min})\sqrt{\ln(2/\delta)/(2m)}$ "với xác suất ít nhất $1-\delta$" (khớp lời giải Bài tập 10.7(i)); "giao thức, ma trận đánh giá; xung đột buộc đánh đổi". |
| 1-02, 3-09: (G1), (G2); "điều kiện không chệch của Bài 05" | đã sửa | 1-02: "(G1) $\mathbb E_\xi\varphi(w,\xi)\in\partial F(w)$, (G2) $\mathbb E_\xi\lVert\varphi(w,\xi)\rVert^2\le G^2$" (khớp ghi chú Bài 05 dòng 131–132); Hệ quả 02.10(b) thêm (T2), $\delta\in(0,1)$. 3-09: "(C) và (G1) của Định lý 05.14 cần $-J$ lồi"; không còn "điều kiện không chệch của Bài 05". |
| 3-10: Mệnh đề 08.12 đủ đại lượng, điểm lặp | đã sửa | Bảo đảm khớp Mệnh đề 08.12 với $F=-J$: $F(w_1)-F_*=\sup J-J(\theta_1)$, vế phải $\frac{2(\sup J-J(\theta_1))}{\eta T}+\beta\eta\sigma^2$, "$\theta_\tau$, $\tau$ rút đều"; ghi chú diễn giả nói rõ đọc thêm ở Bài 08, không tại $\theta_{T+1}$. |
| 4-01 "chỉ thêm nhiễu" | đã sửa | "chúng thêm vào số hạng thứ $t$ một đại lượng có kì vọng $0$"; ghi chú diễn giả: phương sai tăng hoặc giảm. |
| 4-05: điều kiện, nghĩa giá trị nền, kết luận | đã sửa | "chọn ở $s_0$ không phụ thuộc $\theta$"; "(ii) trừ phần thưởng kì vọng còn lại: $1{,}75;\ 2;\ \tfrac12$"; "(ii) tăng phương sai". Khớp Ví dụ 10.10 Bước 3. Xem R8 (tên thuật ngữ). |
| 3-03, 2-05, 4-07 câu nối | đã sửa | 3-03 "Trực quan." mới; 2-05 "Tác tử biết $\pi_\theta$, không biết $\mu_0$, $P$, $r$: không tính được $J$, $\nabla J$ bằng công thức."; 4-07 "$\theta$ cố định: các lượt thỏa (T1), có cận với xác suất cao." |
| 2-03, 2-04: $\mu_0$, $H$, chính sách tất định, Mệnh đề 09.3 | đã sửa | 2-03 đủ tên tiếng Anh; chính sách tất định ở ghi chú diễn giả kèm "tại $\theta_s=0$"; 2-04 có "Tối ưu chính sách (policy optimization)"; không còn Mệnh đề 09.3. |
| 2-05, 3-07 ví dụ đi nhanh | đã sửa | 2-05 gọi tên $1{,}7$, $1{,}8$; 3-07 nêu bốn quỹ đạo qua $s_1$, thừa số $a_1-\tfrac12$, $\tfrac d{d\theta}\pi_\theta(1\mid s_0)=\tfrac14$. |
| 6-04 bền vững, mềm dẻo, "dọc đường biên" | đã sửa | Định nghĩa khớp ghi chú dòng 721; "$\lambda$ tăng, $L_A$ giảm, $L_B$ tăng" (Mệnh đề 10.13(c)). |
| 5-02 "trên tập kiểm tra"; 2-01/5-01 Phần B | đã sửa | 5-02 có "trên tập kiểm tra của nhiệm vụ $i$"; 5-01 dòng cố định/ngẫu nhiên/so sánh, "tập kiểm tra độc lập" (khớp bảng §1). Xem R4 về 2-01. |
| Trang bài tập: câu chữ `exercises.md`; khuôn ghi chú diễn giả | đã sửa, còn một biến thể | 3-11 (b), 4-08 (c), 5-04 (a), 6-06 (c), 7-03 (i) khớp câu chữ cho phần được giữ (ghép phần dẫn của đề vào câu đầu). Không còn "Câu chữ đầy đủ của đề"; còn một câu cùng nghĩa với "… là bài về nhà" ở ghi chú 7-03 (R3). |
| 7-05 (nay 7-06), 1-01 ghi chú diễn giả | đã sửa | Câu quy trình và câu nguồn gốc đã bỏ; "Bài tập 10.9 tùy chọn." là câu thay thế do người duyệt sư phạm đề xuất (khớp `exercises.md` dòng 10). |
| 1-03 mục tiêu 1, 3, 5 | đã sửa | Đủ bổ ngữ; 80 âm tiết (trần 80). |
| 7-06 (nay 7-07) dòng khép học phần | sửa một phần, đã chấp nhận | "Bốn bài toán của học phần: …, ước lượng mật độ (Bài 09), …". Vẫn là danh sách treo không vị ngữ (R11). |
| 7-01 "$\mathcal T$ hữu hạn" | đã sửa | "$\mathcal T$ hữu hạn (hoặc Nhận xét 10.5); (MDP); (Π)"; (MDP) định nghĩa trên mặt 2-03. |
| Sáu điểm sửa nhỏ của điều phối viên | (1)–(4) đã sửa; (5), (6) không sửa, đã chấp nhận | 7-02 cận đủ; 2-01 dòng "Ngẫu nhiên: lượt, tham số, ước lượng gradient."; 5-01 "độc lập"; 7-07 tên sách và tên bài báo. 7-07 mất tên đầy đủ của UML (R2). |
| Phát hiện nhẹ đã chấp nhận | đã sửa hoặc không sửa có lý do | Khớp storyboard §17. |

## 2. Toán: tính lại trên các trang đã đổi

Tất cả khớp ghi chú và `exercises.md`:

- 2-05: $0+0{,}8\cdot2+0{,}2\cdot\tfrac12=1{,}7$; $1+0{,}2\cdot2+0{,}8\cdot\tfrac12=1{,}8$; $J(0)=1{,}75$.
- 3-07: $\theta_{s_1}$: $0{,}2\cdot3\cdot\tfrac12-0{,}2\cdot1\cdot\tfrac12+0{,}05\cdot4\cdot\tfrac12-0{,}05\cdot2\cdot\tfrac12=0{,}25$; $\theta_{s_2}$: $0-0{,}025+0{,}1-0{,}2=-0{,}125$; $\tfrac14(1{,}7-1{,}8)=-0{,}025$.
- 3-10: $dJ/dq=3{,}2q-1{,}2=0$ tại $q=0{,}375$; bảo đảm Mệnh đề 08.12 với $F=-J$ đúng hằng số.
- 3-11: $\pi_\theta(1)=\tfrac14$, $J'=4\cdot\tfrac14\cdot\tfrac34=\tfrac34$, $\operatorname{Var}\hat g=\tfrac94-\tfrac9{16}=\tfrac{27}{16}$.
- 4-04: $b=J(\ln3)=\tfrac52$.
- 4-05: vết $1{,}94625$; $1{,}62125$; $0{,}324375$ (tỉ số $6$); ví dụ đổi: (i) $\tfrac12$ hằng, (ii) $\tfrac32$ hoặc $-\tfrac12$, phương sai $1$.
- 4-06: $0{,}1225$; $27{,}6225$; $0{,}06$ (dùng $(A-\tfrac12)^2=\tfrac14$, $\mathbb E(c+X)^2=c^2+c+\tfrac12$).
- 4-07: $4\sqrt{\ln40/2000}=0{,}17179\le0{,}1718$; $16\ln40/(2\cdot0{,}05^2)=11\,804{,}4$, nên $11\,805$.
- 4-08: tọa độ $\theta_{s_1}$ nhận $1{,}5;-0{,}5;1;0$ với xác suất $0{,}2;0{,}2;0{,}05;0{,}05$: kì vọng $0{,}25$, mô-men bậc hai $0{,}55$, phương sai $0{,}4875$.
- 5-03: $0{,}81$; $-0{,}11$; $0{,}025$; độ quên $0{,}10$, $0{,}17$; ma trận đổi: $\mathrm{acc}_{2,2}-0{,}95=-0{,}03$; ghi chú diễn giả $0{,}005$, $0{,}07$, $0$.
- 5-04: $2{,}26/3=0{,}7533$; $-0{,}19$; $0{,}15$, $0{,}28$, $0{,}215$; $0{,}015$; ghi chú diễn giả $0{,}86-0{,}60=0{,}26$.
- 6-04: năm hàng, cột $L_A+L_B$: $\tfrac12$; $\tfrac{10}{32}=\tfrac5{16}$; $\tfrac14$; $\tfrac5{16}$; $\tfrac{82}{200}=\tfrac{41}{100}$; cột $\alpha=\lambda/(1+\lambda)$.
- 6-05: $\tfrac1{8M}$; $0{,}125$; $0{,}0125$; $0{,}00125$; mô phỏng khớp Phụ lục C (bảng dòng 36–37).
- 6-06: $\frac{1-\alpha}{1+3\alpha}=\tfrac15$; $\tfrac1{1+\lambda\Omega}=\tfrac12$, $\tfrac15$; $\lambda\Omega=\frac{4\alpha}{1-\alpha}$.
- 7-02, 7-04: miền $[Hr_{\min},Hr_{\max}]$ cho bán kính nhân $H(r_{\max}-r_{\min})$ (lời giải Bài tập 10.7(i)).

Không giả thiết nào bị rơi trên các trang được chỉ định (3-09, 7-01, 7-02, 6-05, 4-05, 2-01, 5-01), trừ các điểm ghi ở R1, R4, R6.

## 3. Mạch truyện

- Thứ tự mạch 6 sau khi chuyển: 6-05 (Ví dụ 10.16) → 6-06 (Bài tập 10.5(c), §8) → 6-07 (Định nghĩa 10.15, mở bằng "Câu hỏi: hối tiếc nhỏ có kéo theo độ quên nhỏ không?") → 6-08 (Ví dụ 10.17) → 7-00. Theo đúng §8 → §9. Ghi chú diễn giả 6-03 dẫn "Bài tập 10.5(c)", số hiệu có trên mặt 6-06.
- Mạch 7: 7-01 → 7-02 → 7-03 (đề, dẫn "Ví dụ 10.12", có trên mặt 4-07) → 7-04 (lời giải năm mục, đánh số theo thứ tự năm câu hỏi) → 7-05 → 7-06 → 7-07.
- Mọi số hiệu dẫn trên mặt trang của các trang đã đổi có trang nguồn đứng trước: Định lý 05.14, (G1) (1-02); Ví dụ 10.7 (3-10); Nhận xét 10.5 (3-05); Hệ quả 10.8 (4-02); Ví dụ 10.10 (4-05); Mệnh đề 10.13 (6-02); Ví dụ 10.12 (4-07).
- Câu nối mặt trang: 2-05 → mạch 3 và 4-07 (cận với xác suất cao) có. Dòng dẫn 2-00, 4-00, 7-00 mới là câu trần thuật về nội dung.

## 4. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L10-6-05 (R1) | Một kí hiệu hai nghĩa trên cùng trang, do biên tập sinh ra: dòng 1 đặt $L_A(w)=\tfrac12(w^2+1)$, dòng 6 đặt $L_A=\tfrac12(w^2+0{,}25)$. Cùng lúc dòng 6 bỏ tên đại lượng đo: bốn số $0{,}624$; $0{,}331$; … không còn ghi là rủi ro kiểm tra trên A. | Mặt trang: "Ví dụ 10.16. Nhiệm vụ A: …, $L_A(w)=\tfrac12(w^2+1)$" và "Mô phỏng hồi quy $y=wx$ (Phụ lục C), $L_A=\tfrac12(w^2+0{,}25)$: $0{,}624$ khi tinh chỉnh; …". Ghi chú Ví dụ 10.16 Bước 4: "Mô hình hồi quy của Phụ lục C có rủi ro tổng thể trên A là $\tfrac12(w^2+0{,}25)$. Sau nhiệm vụ B, rủi ro kiểm tra trên A là $0{,}624$ …" (không đặt tên $L_A$). Bản đóng băng: "rủi ro kiểm tra trên A $0{,}624$ khi tinh chỉnh". | "Mô phỏng hồi quy $y=wx$ (Phụ lục C), rủi ro trên A $\tfrac12(w^2+0{,}25)$; rủi ro kiểm tra trên A $0{,}624$ khi tinh chỉnh; $0{,}331$; $0{,}256$; $0{,}252$ với $M=5;\,50;\,1000$, về $0{,}25$, không về $0{,}125$." (52 → khoảng 58 âm tiết). |
| trung bình | L10-7-07 (R2) | "UML" xuất hiện lần đầu (và duy nhất) trên mặt trang mà không có tên sách, tác giả. Decks 06–09 đều viết đủ "Shalev-Shwartz và Ben-David (2014), *Understanding Machine Learning: From Theory to Algorithms* (UML)" ở trang tài liệu. Lỗi sinh ra từ điểm sửa nhỏ (4) chuyển tác giả UML xuống ghi chú diễn giả. | Mặt trang: "UML §21.1–21.3 sau buổi học."; bản đóng băng: "UML (Shalev-Shwartz, Ben-David, 2014), §21.1–21.3". Deck 09, L09-7-07: "Shalev-Shwartz và Ben-David (2014), Understanding Machine Learning: From Theory to Algorithms (UML)." | Viết "Shalev-Shwartz, Ben-David (2014), *Understanding Machine Learning: From Theory to Algorithms* (UML): §21.1–21.3 sau buổi học." Trang đang 59 âm tiết: đổi dòng cuối thành "Học phần xét bốn bài toán: …" (bớt 1 âm tiết, xem R11) và ghi ngoại lệ trần cho trang tài liệu (tên sách, tên bài báo) trong storyboard, như tiền lệ ngoại lệ bài tập tổng hợp. |
| trung bình | L10-7-03, ghi chú diễn giả (R3) | Biến thể của khuôn "… là bài về nhà" mà quyết định đã yêu cầu bỏ (lần thứ ba); câu chỉ là con trỏ điều hướng. | "Thiết lập (ii) của bài, chuỗi thời gian với cửa sổ chồng lấn, thuộc bảng bài tập về nhà." Quyết định: "bỏ khuôn 'Câu chữ đầy đủ của đề' và 'là bài về nhà'"; `deck-su-pham.md`: "thay khuôn … bằng một câu nội dung hoặc bỏ". | Bỏ câu, hoặc thay bằng nội dung của lời giải 10.7(ii): "Với chuỗi thời gian có cửa sổ chồng lấn, (T1) ở dạng đầy đủ không thỏa và (T3) không thỏa với hàm lỗi log." |
| nhẹ | L10-2-01 (R4) | Kí hiệu $\theta$ và chỉ số $j$ dùng trước khi định nghĩa ($\theta$ được giới thiệu ở 2-02, 2-03). Bản đóng băng viết bằng chữ ("Tham số ở cập nhật $j$ …"). | "$\theta$ cố định: lượt độc lập cùng phân bố; $\theta$ ở cập nhật $j$ phụ thuộc lượt trước: (T1) không đúng." | "Tham số cố định: lượt độc lập cùng phân bố; tham số ở cập nhật $j$ phụ thuộc lượt trước: (T1) không đúng." (58 → 60). |
| nhẹ | L10-3-09 (R5) | Dòng 4 mở bằng cụm danh từ không chủ ngữ; "không chệch có điều kiện" dễ đọc thành "không chệch khi có điều kiện". | "Gradient ngẫu nhiên không chệch có điều kiện; (C) và (G1) của Định lý 05.14 cần $-J$ lồi." | "$\hat g_j$ là gradient ngẫu nhiên không chệch có điều kiện; (C) và (G1) của Định lý 05.14 cần $-J$ lồi." (49 → 51). |
| nhẹ | L10-7-02 (R6) | Dòng 3 rút "là hàm của lịch sử" thành "theo lịch sử" (điều kiện của Hệ quả 10.8, phát hiện N1 ở cổng duyệt) và bỏ "một lượt". | "(MDP), (Π): ước lượng không chệch; giá trị nền theo lịch sử chỉ đổi phương sai." Bản đóng băng: "Dưới (MDP), (Π): ước lượng một lượt không chệch." Ghi chú §10: "ước lượng được không chệch từ một lượt". | "(MDP), (Π): ước lượng một lượt không chệch; giá trị nền là hàm của lịch sử chỉ đổi phương sai." (58 → 60; nếu vượt, bỏ "một lượt"). |
| nhẹ | L10-6-08 (R7) | Kết luận mất quan hệ nhân quả và "tại thời điểm của": hai mệnh đề đặt cạnh nhau bằng dấu chấm phẩy. | "hối tiếc cộng hàm lỗi tại từng vòng; cận hối tiếc tĩnh không chặn độ quên." Ghi chú Ví dụ 10.17: "Hối tiếc cộng hàm lỗi tại thời điểm của từng vòng, nên cận hối tiếc tĩnh không phải cận cho độ quên." | "hối tiếc cộng hàm lỗi tại thời điểm của từng vòng, nên cận hối tiếc tĩnh không chặn độ quên." (45 → 49). |
| nhẹ | L10-4-05 (R8) | Thuật ngữ rút gọn: "phần thưởng kì vọng còn lại" thay cho "tổng phần thưởng kì vọng còn lại từ trạng thái hiện tại". | Mặt trang: "(iii) (ii) trừ phần thưởng kì vọng còn lại: $1{,}75;\ 2;\ \tfrac12$". Ghi chú Ví dụ 10.10: "bằng tổng phần thưởng kì vọng còn lại từ trạng thái hiện tại". | "(iii) (ii) trừ tổng phần thưởng kì vọng còn lại: …" (59 → 60). |
| nhẹ | L10-5-03 (R9) | Đuôi câu "phụ thuộc quy ước" treo sau dấu hai chấm thứ hai, không chủ ngữ; "độ quên âm" của bản đóng băng thành "độ quên $-0{,}03$". | "cực đại chỉ tới hàng $K-1$: độ quên $-0{,}03$ ở nhiệm vụ 2: phụ thuộc quy ước." | "cực đại chỉ tới hàng $K-1$: độ quên $-0{,}03$ ở nhiệm vụ 2; độ đo phụ thuộc quy ước." (58 → 59). |
| nhẹ | L10-7-03 (R10) | Đề không có động từ nhiệm vụ: câu chữ `exercises.md` "Trả lời năm câu hỏi cho hai thiết lập sau" thành cụm danh từ. | "Bài tập 10.7. Năm câu hỏi cho thiết lập (i): quá trình sinh dữ liệu; …; các giả thiết của Bài 01–08 cần thay đổi." | "Trả lời năm câu hỏi cho thiết lập (i): …". Trang đang 60: nếu vượt trần, ghi ngoại lệ bài tập tổng hợp như Bài 01, 05. |
| nhẹ | L10-7-07 (R11) | Dòng khép học phần vẫn là danh sách treo, không vị ngữ (quyết định ban đầu: "câu đủ"). | "Bốn bài toán của học phần: phân lớp có giám sát, ước lượng mật độ (Bài 09), tối ưu chính sách, học liên tục." | "Học phần xét bốn bài toán: phân lớp có giám sát, ước lượng mật độ (Bài 09), tối ưu chính sách, học liên tục." (bớt 1 âm tiết). |
| nhẹ | L10-4-07 (R12) | Mặt trang không còn tên công cụ (Hệ quả 02.10(b) cho $R/4$, nhân bán kính với $4$); thừa số $4$ trong công thức không có lời giải thích trên mặt trang, chỉ có ở ghi chú diễn giả và tiêu đề "cận Hoeffding". | "$\Big\lvert\tfrac1m\sum_jR(\tau_j)-J(\theta)\Big\rvert\le4\sqrt{\ln40/2000}\le0{,}1718$." Bản đóng băng: "Hệ quả 02.10(b) cho $R/4$, nhân bán kính với $4$". | Tùy chọn: thêm "(Hệ quả 02.10(b) cho $R/4$)" sau "$0{,}95$" nếu trang còn biên (59 hiện tại); nếu không, giữ như đã chấp nhận. |
| nhẹ | L10-4-08 (R13) | Câu so sánh bỏ chữ "phương sai" của đề. | "Tính kì vọng và phương sai của tọa độ $\theta_{s_1}$, so với $\tfrac9{16}$ (ước lượng (ii), Ví dụ 10.10)." `exercises.md`: "rồi so với phương sai $\tfrac9{16}$ của ước lượng (ii) trong Ví dụ 10.10." | Trang ở trần 60: chấp nhận, hoặc đổi "(ước lượng (ii), Ví dụ 10.10)" thành "(phương sai của (ii), Ví dụ 10.10)". |
| nhẹ | L10-6-05, ghi chú diễn giả (R14) | "SGD" không có tên đầy đủ trong ghi chú diễn giả (có từ bản đóng băng). | "một vòng qua dữ liệu của SGD trên mỗi nhiệm vụ". | "… của hạ gradient ngẫu nhiên (SGD) …". |
| nhẹ | `storyboard.md` §12 dòng kiểm, §17 (R15) | Tài liệu kế hoạch chưa theo vị trí mới: "(C) ở 1-02 trước 3-09, 6-06, …" (nay (C) dùng ở 6-07); §17 ghi "Bỏ … câu nguồn gốc ('Bài tập 10.9 tùy chọn.')" trong khi câu này là câu thay thế được giữ. | `storyboard.md` §12 dòng cuối; §17 hàng "7-05 (nay 7-06)". | Sửa "6-06" thành "6-07"; viết lại hàng §17: "bỏ câu quy trình và câu nguồn gốc, thay bằng 'Bài tập 10.9 tùy chọn.'". |

Không có phát hiện chặn bàn giao hay nghiêm trọng. Không có đề xuất sửa ghi chú mới ngoài các đề xuất đã ghi ở `review-log.md`.

## 5. Văn phong (no-ai-slop, chế độ Detect) trên văn bản mới

Văn bản mới trên mặt trang (dòng dẫn 2-00, 4-00, 7-00; 3-03 "Trực quan."; 2-05, 4-07 câu nối; 6-04 định nghĩa; 7-02) viết câu toán học ngắn, không rào đón, không khẩu hiệu, không câu tự hỏi tự đáp. Các điểm còn lại là câu thiếu chủ ngữ hoặc vị ngữ do cắt mật độ (R5, R9, R10, R11) và một quan hệ nhân quả bị bỏ (R7). Ghi chú diễn giả mới không mở bằng "Trang này", không ID trang, không câu quy trình; "chưa phải (G1)" ở 3-09 là phủ định toán học, được phép.

## Kết luận

**Đạt khi sửa.** 0 chặn bàn giao, 0 nghiêm trọng, 3 trung bình (R1–R3), 12 nhẹ (R4–R15). Mọi phát hiện nghiêm trọng và trung bình của năm báo cáo đã sửa đúng hoặc có lý do không sửa được chấp nhận; R1 và R2 là lỗi mới do biên tập sinh ra, R3 là phần còn sót của một quyết định. Sửa R1–R3 xong thì kiểm lại 6-05, 7-03, 7-07 (±2) và chạy lại `deck_lint.py`, `footer_check.py`.

## Lượt 2 (2026-11-16)

Phạm vi: các trang người sửa đổi theo R1–R15 (2-01, 3-09, 4-05, 5-03, 6-05, 6-08, 7-02, 7-03 cả đề và ghi chú diễn giả, 7-07) ±2 trang. Đã đối chiếu bản sau với bản kiểm ở lượt 1 bằng diff văn bản mặt trang và ghi chú diễn giả. Ngoài các trang này, chỉ có ghi chú diễn giả của 6-05 ("hạ gradient ngẫu nhiên (SGD)") và của 7-07 đổi.

**Kiểm máy.**

- `deck_lint.py`: 1 phát hiện, `L10-7-07 | SYLL60 | 70 > 60`. Đây là ngoại lệ đã được điều phối viên chấp nhận (văn bản thư mục).
- `footer_check.py`: 0 trang chạm chân trang.
- `deck_check.py --shots --ids` trên chín trang: console 0, pageerrors 0, failed 0, `.katex-error` 0. OVERFLOW ở 6-08 và 7-02 chỉ là đuôi `\sqrt`.
- Đã xem ảnh 1600×900 và 390×844 (kể cả `-end`) của chín trang: không tràn, không chồng lấn, bảng cuộn ngang có nhãn.

**Trạng thái R1–R15.**

| Mục | Trạng thái | Bằng chứng |
|---|---|---|
| R1 6-05 | đã sửa | $L_A$ chỉ còn nghĩa $\tfrac12(w^2+1)$. Mô hình mô phỏng viết "rủi ro trên A $\tfrac12(w^2+0{,}25)$". Bốn số có tên: "rủi ro kiểm tra trên A: $0{,}624$ (tinh chỉnh); $0{,}331$; $0{,}256$; $0{,}252$". Đẳng thức $\mathbb EL_A(w_M)-L_A(\tfrac12)=\tfrac1{8M}$ đúng: $w_M-\tfrac12=\tfrac12\bar Z_M$, $\operatorname{Var}w_M=\tfrac1{4M}$, độ lệch $\tfrac12\operatorname{Var}w_M=\tfrac1{8M}$. Ba giá trị $0{,}125$; $0{,}0125$; $0{,}00125$ khớp Ví dụ 10.16. 60 âm tiết. |
| R2 7-07 | đã sửa | "Shalev-Shwartz và Ben-David (2014), *Understanding Machine Learning: From Theory to Algorithms* (UML): §21.1–21.3 sau buổi học.", khớp decks 06–09. Ngoại lệ 70 âm tiết đã được chấp nhận. |
| R3 7-03, ghi chú diễn giả | đã sửa | Câu "… thuộc bảng bài tập về nhà." đã bỏ. |
| R4 2-01 | đã sửa, sinh lỗi mới | "Tham số cố định: …; tham số ở cập nhật $j$ phụ thuộc lượt trước: (T1) sai." Nhưng dòng Học liên tục bỏ chữ "phân bố" (xem phát hiện L2-1). |
| R5 3-09 | đã sửa | "$\hat g_j$ là gradient ngẫu nhiên không chệch có điều kiện; …". |
| R6 7-02 | đã sửa một phần, đã chấp nhận | "giá trị nền là hàm của lịch sử chỉ đổi phương sai"; cụm "một lượt" nằm ở ghi chú diễn giả. |
| R7 6-08 | đã sửa | "… tại thời điểm của từng vòng, nên cận hối tiếc tĩnh không chặn độ quên." |
| R8 4-05 | đã sửa | "trừ tổng phần thưởng kì vọng còn lại". |
| R9 5-03 | đã sửa | "…; độ đo phụ thuộc quy ước." |
| R10 7-03 | đã sửa | "Trả lời năm câu hỏi cho (i): …". Thiết lập (i) có ngay dòng sau. |
| R11 7-07 | đã sửa | "Học phần xét bốn bài toán: …". |
| R12 4-07, R13 4-08 | không sửa, đã chấp nhận | Theo quyết định của điều phối viên. |
| R14 6-05, ghi chú diễn giả | đã sửa | "hạ gradient ngẫu nhiên (SGD)". |
| R15 storyboard | theo bảng §17 của người sửa | Không kiểm thêm trong lượt này. |

**Toán và dữ kiện.** Không con số nào đổi ngoài 6-05 (đã tính lại ở trên). Các trang 3-09, 4-05, 5-03, 6-08, 7-02 giữ nguyên số liệu đã kiểm ở lượt 1. 7-03 giữ đủ năm câu hỏi và thiết lập (i) theo `exercises.md`; "đại lượng ngẫu nhiên" thay "các đại lượng ngẫu nhiên" không đổi nghĩa.

**Mạch truyện.** Thứ tự trang không đổi. Số hiệu dẫn trên mặt trang vẫn có trang nguồn đứng trước. Câu nối 2-05 và 4-07 không bị chạm tới.

**Phát hiện lượt 2.**

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L10-2-01 (L2-1) | Khi cắt mật độ, chữ "phân bố" trước $D_1,\ldots,D_K$ bị bỏ. Kí hiệu $D_k$ vì vậy xuất hiện trên mặt trang mà không có nghĩa; nó chỉ được định nghĩa ở 5-01 ("phân bố $D_k$ trên $\mathcal Z$"). Đây là vi phạm quy tắc định nghĩa trước khi dùng, và là đúng loại dữ kiện rơi mà lượt này phải kiểm. | Bản sau: "Học liên tục (continual learning): $K$ nhiệm vụ (task), $D_1,\ldots,D_K$, theo thứ tự." Lượt 1: "…, phân bố $D_1,\ldots,D_K$, theo thứ tự." Ghi chú §1, Phần B: "mỗi nhiệm vụ có một phân bố riêng". | Khôi phục "phân bố $D_1,\ldots,D_K$". Trang từ 59 lên 60 âm tiết, vẫn trong trần. |

**Kết luận lượt 2: đạt khi sửa.** 0 chặn bàn giao, 0 nghiêm trọng, 1 trung bình (L2-1, sửa một từ), 0 nhẹ mới. R1–R3 đã đóng. Sau khi sửa L2-1, chạy lại `deck_lint.py` (chỉ còn ngoại lệ 7-07) và `footer_check.py` cho 2-01.
