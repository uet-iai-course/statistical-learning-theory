# Rà soát Bài 08: góc nhìn học viên cao học (người rà 1)

Đối tượng: bản đóng băng `lec08-draft-frozen.md` (1084 dòng). Vai: học viên đã học Bài 01–07, chưa biết lập luận ghép cặp. Chỉ đọc; không sửa tệp nào trong repo.

## Tổng kết

| Mức | Số phát hiện |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 1 |
| trung bình | 9 |
| nhẹ | 17 |

Những gì đã làm lại:

- **Câu ôn nhanh 1–3.** Làm được và khớp lời giải ($g''\le\tfrac14$; $1{,}5\le3{,}5$; $3367/4096\approx0{,}8220$).
- **Ví dụ 08.1, 08.2.** Tính tay từng bước; mọi $w_{t+1}$, $w'_{t+1}$, $\Delta_{t+1}$ khớp.
- **Ví dụ 08.4.** Liệt kê chính xác bằng phân số (`reviews08/r1/check.py`): $\mathbb E\Delta_2=1/4$, $\mathbb E\Delta_3=29/64$, $\mathbb E\Delta_7=228203/262144\approx0{,}8705$. Quỹ đạo $(2,3,1,4,4,4)$ cho $\Delta_7=3$.
- **Ví dụ 08.3, 08.5, 08.7, 08.8, 08.9.** Mọi số khớp, gồm:
  - $\Delta_3/\Delta_2\approx1{,}1$, $\Delta_{21},\ldots,\Delta_{101}$ và $\Delta_{58}\approx0{,}207$;
  - $275{,}6$; $33{,}37$; $0{,}0866$; $0{,}0791$; $0{,}0725$; $T^*\approx7071$ với giá trị $0{,}0957$;
  - $39{,}975$; $0{,}0153$.
- **Hệ quả 08.7, 08.8.** Đổi thứ tự tổng, $\eta^*$, $2\sqrt{ab}$ và giới hạn khi $T\to\infty$ đều đúng.
- **Câu hỏi cuối buổi.** Làm được: (a) $0{,}8$; (b) $\le0{,}0113$ (tổng $\le28{,}19$); (c), (d) trả lời được từ Ví dụ 08.6 và 08.10.
- **Thí nghiệm.** Chạy lại `exp_lec08_coupled_sgd.py` (23 giây; mặc định và `--eta 0.25`); kết quả lưu ở `reviews08/r1/exp_out.txt`.
  - Mọi số ở bảng mở đầu, ở Ví dụ 08.6 và ở Phụ lục D trùng với đầu ra: khoảng của các hạt giống, tỉ lệ đổi nhãn, $0{,}603$, $0{,}827$, $0{,}651$, các tỉ số $11{,}24$ và $108{,}84$.
  - Thứ tự rút và các thời điểm đo trong script khớp Phụ lục D, nên tái lập được.
  - Mô tả mô hình khớp script: $\lVert x\rVert\le1$, SGD không chiếu, rút có hoàn lại, $\eta=0{,}5\le8$. Giả thiết (S), (G), (T1), (T2) thỏa như Ví dụ 08.6 nêu.
- **Kiểm tra tham chiếu trước.** `forward_refs.py` chạy trên một bản sao báo 0. Mọi khối tiên quyết được dẫn đều tồn tại ở Bài 01–07.

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | 491, 699, 778 (đối chiếu 445, 352) | Bài khẳng định tính lồi chỉ đi vào qua Bổ đề 08.4(a) và chỉ ở bước chung, nhưng hai chứng minh dùng nó ở chỗ khác. Bước 1 của Định lý 08.6 dùng tính lồi qua Mệnh đề 05.5(a); Mệnh đề 05.5 có giả thiết "$F$ lồi". Bước 2 của Mệnh đề 08.5 dùng Bổ đề 08.4(b) ở bước khác biệt. Mục tiêu 2 và Bài tập 08.3 yêu cầu chỉ ra bước dùng tính lồi, nên học viên nhận hai câu trả lời mâu thuẫn. | 491: "tính lồi chỉ qua Bổ đề 08.4(a)". 699: "chỉ đi vào chứng minh qua Bổ đề 08.4, tức qua các bước chung". 445: "hàm $\ell(\cdot,z)$ lồi theo (S) … Theo Mệnh đề 05.5(a)". 352: "Số hạng thứ nhất không quá $\Delta_t$ theo Bổ đề 08.4(b) … (S) được dùng ở đây". | (1) Ở Bước 1 của Định lý 08.6, thay Mệnh đề 05.5(a) bằng định lý giá trị trung bình trên đoạn $[u,v]\subset W$ ($W$ lồi, $\ell(\cdot,z)$ khả vi, $\lVert\nabla\ell\rVert\le G$ trên $W$). Khi đó tính lồi của hàm lỗi thật sự chỉ vào qua Bổ đề 08.4(a), và giữ được câu ở dòng 491, 778. Nếu giữ Mệnh đề 05.5(a) thì sửa 491 và 778 cho khớp. (2) Dòng 699: thay "tức qua các bước chung" bằng "ở các bước chung và ở số hạng thứ nhất của bước khác biệt (Mệnh đề 08.5, Bước 2)". |
| trung bình | 84–88 | §1 dùng $\beta$, $G$, $w_1$, $\eta_t$, $\xi$, $\bar w_T$, $w'_t$ trong bảng phân loại trước khi chúng được đặt tên. $\beta$ và $G$ chỉ được định nghĩa ở §2 (dòng 102, 107–108). Quy tắc "định nghĩa trước khi dùng" của học phần bị vi phạm; `forward_refs.py` không bắt được vì chỉ kiểm tra số hiệu khối. | 84: "Cố định \| $D$, $W$, $\ell$, $\beta$, $G$, $m$, $T$, $\eta_1,\ldots,\eta_T$, $w_1$". | Chuyển bảng phân loại xuống cuối §2, sau (S) và (G). Nếu giữ ở §1, ghi tên tại chỗ: "hằng số trơn $\beta$ và cận gradient $G$ (§2)". |
| trung bình | 191–193 | Ý chính của bài (vì sao được dùng chung $\xi$) gói trong một đoạn ba mệnh đề. Bất đẳng thức $\lvert\mathbb Ea-\mathbb Eb\rvert\le\mathbb E\lvert a-b\rvert$ không có tên công cụ. Người chưa biết ghép cặp thiếu một phép tính nhỏ cho thấy ghép cặp cho cận chặt hơn không ghép cặp. | 191: "Ghép cặp đặt hai lần chạy trên cùng không gian xác suất của $\xi$; mỗi lần chạy riêng vẫn có đúng phân bố của Thuật toán 08.1, nên hai kì vọng trong Định nghĩa 06.9 không đổi." | Thêm khoảng 45 tiếng sau dòng 193, với số của Ví dụ 08.1 (một bước, $s^{(4)}=(0,1,2,-3)$) đã kiểm bằng tay: "Sau một bước, $\mathbb E_\xi w_2=\tfrac38$ trên $s$ và $\mathbb E_\xi w'_2=\tfrac18$ trên $s^{(4)}$, hiệu $\tfrac14$. Ghép cặp cho $\mathbb E\lvert w_2-w'_2\rvert=\tfrac14$, đúng bằng hiệu. Hai dãy chỉ số độc lập cho $\tfrac38$." Gọi tên bất đẳng thức: "(bất đẳng thức tam giác cho kì vọng)". |
| trung bình | 180 | Câu ngầm nói Hệ quả 06.2 áp dụng được khi $T\le m$. Thuật toán 08.1 rút có hoàn lại, nên quan sát bị dùng lại ngay trong vòng đầu với xác suất dương. Nhận xét 06.3 nói về một vòng theo thứ tự, một thuật toán khác. | 180: "Khi $T>m$, mỗi quan sát được dùng trung bình $T/m$ lần, nên điểm lặp phụ thuộc vào quan sát sắp được dùng, và Hệ quả 06.2 không áp dụng (Nhận xét 06.3)." | "Khi rút có hoàn lại, một quan sát có thể được dùng lại ngay trong vòng đầu; khi $T>m$, mỗi quan sát được dùng trung bình $T/m$ lần. Điểm lặp vì thế phụ thuộc vào quan sát sắp được dùng, và Hệ quả 06.2 không áp dụng." |
| trung bình | 578 | Số $0{,}4750$ được dẫn tới Bài tập 08.7, khối chưa có và nằm sau ghi chú; học viên không kiểm được. Số này đã được tính ở Ví dụ 06.3, Bước 5 (Bài 06, dòng 430). | 578: "khoảng cách tổng quát hóa kì vọng thật khoảng $0{,}4750$ (Bài tập 08.7)". | "… thật là $0{,}4750$ (Ví dụ 06.3, Bước 5)". Bài tập 08.7 có thể được nhắc ở §11. |
| trung bình | 524–538 | Ở $100$ vòng, $\Delta$ ghép cặp ($5{,}458$) lớn hơn $\Delta$ không ghép cặp ($4{,}00$), ngược với cách đọc bảng mà Bước 4 gợi ý. Bước 4 không giải thích; học viên sẽ hỏi. Đầu ra script cho thấy $\Delta$ không ghép cặp giảm từ $4{,}93$ (10 vòng) xuống $4{,}00$. | 538: "$\Delta$ không ghép cặp đã cỡ $3$ đến $5$ từ nửa vòng đầu; nó đo tính ngẫu nhiên của thuật toán, không đo độ nhạy theo mẫu." | Thêm khoảng 35 tiếng: "Hai lần chạy không ghép cặp tối ưu cùng một hàm $L_S$, nên khoảng cách giữa chúng giảm dần sau $10$ vòng. Hai lần chạy ghép cặp tối ưu hai hàm $L_S$ và $L_{S^{(i)}}$ khác nhau, nên khoảng cách tiếp tục tăng." Nếu chưa chắc về cơ chế, chỉ nêu số và ghi rằng định lý không nói gì về $\Delta$ không ghép cặp. |
| trung bình | 659–678 (đối chiếu 150) | Hai điểm dễ gây hiểu lầm trong Ví dụ 08.7. (1) Bước 1 và Bước 2 đều ghi "một vòng" nhưng cho hai cận khác nhau ($0{,}0500$ và $0{,}0866$); ví dụ không nói đây là hai thuật toán khác nhau (theo thứ tự, mỗi quan sát một lần; và rút có hoàn lại). (2) Với $\eta=0{,}05$, số bước tốt nhất $T^*\approx7071$ nhỏ hơn $m=10^4$, tức chưa hết một vòng; ví dụ không ghi điều này, dù câu hỏi ứng dụng là "chạy nhiều vòng". | 666: "với $T=10^4$ (một vòng), $\eta^*\approx0{,}029\le8$". 676: "Hàm nhỏ nhất gần $T^*=\frac{R\sqrt{m/2}}{\eta G}\approx7071$". | (1) Bước 2: "với $T=10^4$ bước rút có hoàn lại (số bước bằng một vòng, nhưng không phải thuật toán của Nhận xét 06.3)". (2) Kết luận: "$T^*\approx7071<m$: với độ dài bước này, cận tốt nhất đạt trước khi hết một vòng." Khoảng 40 tiếng. |
| trung bình | 691 (đối chiếu 491) | Dòng 691 nói học phần chứng minh hai trường hợp của chính quy hóa ngầm. Trường hợp thứ hai là phép so sánh mà dòng 491 tự gọi là "không phải một định lý". | 691: "Học phần có chứng minh cho hai trường hợp. … Trong Định lý 08.6, ngân sách độ dài bước giới hạn hệ số ổn định như $1/\lambda$ trong Mệnh đề 06.11." | "Học phần có một chứng minh: hạ gradient … (Phụ lục D của Bài 07). Định lý 08.6 cho một kết quả gần với nó: ngân sách độ dài bước giới hạn hệ số ổn định, như $1/\lambda$ trong Mệnh đề 06.11." |
| trung bình | 198 | Ví dụ bỏ qua bốn bước tính của lần chạy trên $s^{(4)}$, trái quy tắc "ví dụ đi từng bước" của học phần. Học viên phải tự tính $w'_4,\ldots,w'_7$ để kiểm bảng. | 198: "Các bước khác tính như Ví dụ 08.1." | Thêm cột "Đạo hàm tại $w'_t$" vào bảng ở dòng 202 ($0$; $1$; $-1$; $-1$; $1$; $0$), như bảng của Ví dụ 08.1. Chi phí khoảng 8 tiếng. |
| trung bình | 213 | Ngân sách $3$ được tính rồi không dùng: dòng so sánh $\Delta_7$ với $2$, không với $3$. Học viên không thấy liên hệ giữa ngân sách và cận. | 213: "Ngân sách độ dài bước là $\sum_{t=1}^6\eta_t=6\cdot\tfrac12=3$. Dãy có hai bước khác biệt, nên tổng các phần tăng ở Bước 3 là $2\cdot2G\eta=2$, và $\Delta_7=\tfrac54\le2$." | Thêm một câu: "Mỗi bước là bước khác biệt với xác suất $\tfrac14$, nên số bước khác biệt kì vọng là $\tfrac64$ và phần tăng kì vọng không quá $2G\cdot\tfrac14\cdot3=1{,}5$." |
| nhẹ | 3 | Động từ "cho" bị đọc thành hai nghĩa: "dành cho ERM" hay "đem lại một hệ số". | "Mệnh đề 06.11 cho tối thiểu hóa rủi ro thực nghiệm … có chính quy hóa một hệ số ổn định $2G^2/(\lambda m)$." | "Mệnh đề 06.11 chứng minh rằng ERM có chính quy hóa ổn định đều với hệ số $2G^2/(\lambda m)$." |
| nhẹ | 43 | Trong bài này, "thí nghiệm mở đầu" là thí nghiệm hồi quy logistic; ở dòng 43 nó lại chỉ thí nghiệm của Bài 07. | "lớp kiến trúc của thí nghiệm mở đầu, với đặc trưng ngẫu nhiên (Ví dụ 07.3)". | "lớp kiến trúc với đặc trưng ngẫu nhiên trong thí nghiệm của Bài 07 (Ví dụ 07.3)". |
| nhẹ | 39–44 | Danh sách tiên quyết vừa có mục không dùng, vừa thiếu mục được dùng. Ví dụ 06.9 chỉ xuất hiện trong danh sách. Thiếu (C) của Bài 05 (dòng 632), Bước 1 Phụ lục B của Bài 05 (dòng 1019) và bất đẳng thức trung bình cộng–trung bình nhân (dòng 651). | 42: "dữ liệu không bị chặn (Ví dụ 06.9)". | Bỏ Ví dụ 06.9 (bớt khoảng 6 tiếng). Thêm "(C) (§7 của Bài 05)" vào dòng Bài 05 và "bất đẳng thức trung bình cộng–trung bình nhân" vào dòng Giải tích. |
| nhẹ | 111, 632 | (G2), (G1), (C) được dùng mà không có một cụm giải nghĩa. | 111: "(G) cũng kéo theo (G2) cho oracle rút đều một quan sát". | "(G2) (cận mô-men bậc hai của oracle, Định nghĩa 05.10)". |
| nhẹ | 77 | Câu cụt; "cận dưới đúng" dễ đọc thành "cận dưới đúng đắn". | "Không cần cho cận khoảng cách tổng quát hóa; cận dưới đúng $\inf_WL_D$ ở §8." | "Cận khoảng cách tổng quát hóa không cần đối tượng so sánh; §8 so với $\inf_WL_D$." |
| nhẹ | 90 | Bảng phân loại nhắc "lần chạy thứ hai" trước khi §4 giới thiệu nó; câu có dạng tương phản "không phải". | "Lần chạy thứ hai là công cụ chứng minh, không phải một lần huấn luyện thật." | Chuyển câu sang sau Định nghĩa 08.2: "Lần chạy thứ hai chỉ dùng trong chứng minh." |
| nhẹ | 11–19 | Bảng mở đầu không có cột cận, trong khi script in sẵn cột "Cận (§7)". Học viên phải tự nhân trong đầu. | 11: "Cận mà §7 chứng minh … bằng đúng số vòng ở cột đầu." | Thêm cột "Cận" ($0{,}5$; $1$; $5$; $20$; $100$) và bỏ câu ở dòng 11. Tổng số chữ giảm. |
| nhẹ | 242 | Tiêu đề ghi "phác thảo", nhưng (b), (c) chứng minh đủ và (a) chứng minh đủ ở Phụ lục A. Học viên không biết phần nào còn thiếu. | "Bổ đề 08.4 (Bước gradient không giãn) — phác thảo (tính đồng bức chứng minh ở Phụ lục A)". | "— chứng minh đầy đủ (phần (a) ở Phụ lục A)". |
| nhẹ | 287 | Bài dùng "hệ số giãn nhỏ nhất", nhưng Định nghĩa 08.3 chỉ định nghĩa "có hệ số giãn $c$". Bảng ở dòng 297 ghi "hệ số giãn" mà thực chất là hằng số nhỏ nhất. | "Hệ số giãn nhỏ nhất của một ánh xạ tuyến tính từng khúc và liên tục là trị tuyệt đối lớn nhất của hệ số góc." | Thêm vào Định nghĩa 08.3: "số $c$ nhỏ nhất như vậy gọi là hệ số giãn nhỏ nhất". Đổi tiêu đề bảng thành "Hệ số giãn nhỏ nhất". |
| nhẹ | 377 | Bỏ qua một bước kiểm: vì sao $\Delta_3=1$ với cả $w_2=0$ lẫn $w_2=\tfrac12$. | "Bước thứ hai cho $\Delta_3=1$ khi $i_2=4$ và $\Delta_3=0$ khi không". | Thêm: "với $w_2\in\{0,\tfrac12\}$, $w_2-3<-1$ và $w_2+3>1$, nên hai đạo hàm là $-1$ và $1$, cách nhau $2G\eta=1$". |
| nhẹ | 252–261 | Công thức (b) bị ngắt thành năm dòng, có một dòng bắt đầu bằng "$\cdot$"; khó đọc trên màn hình rộng. | "&\quad-\eta\big(\tfrac2\beta-\eta\big)\\ &\qquad\cdot\lVert\nabla f(u)-\nabla f(v)\rVert^2" | Gộp thành ba dòng: $\le\lVert u-v\rVert^2-\eta(\tfrac2\beta-\eta)\lVert d\rVert^2$, với $d$ đặt trước như ở chứng minh. |
| nhẹ | 584 | Câu nói về các đại lượng, nhưng Định lý 05.14 và Hệ quả 08.7 chỉ cho cận của chúng. | "số hạng thứ hai giảm khi $T$ tăng (Định lý 05.14), còn số hạng thứ nhất tăng (Hệ quả 08.7)." | "cận của số hạng thứ hai giảm khi $T$ tăng (Định lý 05.14), còn cận của số hạng thứ nhất tăng (Hệ quả 08.7)." |
| nhẹ | 686 | Câu định nghĩa dài; cụm "trước khi chạy hoặc bằng một mẫu xác thực" khó biết bổ nghĩa cho từ nào. | "là chọn số bước $T$ nhỏ hơn số bước cần để đưa sai số tối ưu thực nghiệm về gần $0$, trước khi chạy hoặc bằng một mẫu xác thực độc lập với $s$; đầu ra là điểm lặp tại bước dừng." | Tách thành hai câu: "… về gần $0$. Số bước được chọn trước khi chạy, hoặc chọn bằng một mẫu xác thực độc lập với $s$; đầu ra là …". |
| nhẹ | 693 | Giá trị $0{,}603$ ở $10$ vòng không có trong bảng mở đầu; "khoảng 5 đến 10 vòng" là nội suy giữa các thời điểm đo. | "hàm lỗi logistic trên mẫu kiểm tra nhỏ nhất ở khoảng $5$ đến $10$ vòng ($0{,}589$ và $0{,}603$)." | "Trong các thời điểm đo, … nhỏ nhất ở $5$ vòng ($0{,}589$); ở $10$ vòng là $0{,}603$ (Phụ lục D)." |
| nhẹ | 781 | Đoạn so cận của $\mathbb E\Delta$ (một khoảng cách tham số) với miền giá trị của hàm lỗi mà không nhân $G$. | "vế phải của (c) là … $\approx275{,}6$, trong khi hàm lỗi cosin chỉ nhận giá trị trong $[0,2]$." | "… $\approx275{,}6$; nhân với $G=1$, cận cho hiệu hàm lỗi vượt xa độ rộng $2$ của miền giá trị." |
| nhẹ | 840 | $\Theta_1$, $\Theta_2$ chưa được gọi tên trong bài này. | "Gradient theo $\Theta_1$ tỉ lệ với độ lớn của $\Theta_2$". | "Gradient theo ma trận trọng số lớp ẩn $\Theta_1$ tỉ lệ với độ lớn của ma trận lớp ra $\Theta_2$ (Định nghĩa 07.1)". |
| nhẹ | 517, 1073 | Mỗi hạt giống rút một $w^\star$ riêng, nên phân bố $D$ đổi theo hạt giống; bảng lấy trung bình trên $20$ phân bố. Kết luận vẫn đúng vì cận đúng cho từng $D$, nhưng bài chưa nói. | 1073: "Véc-tơ $w^\star$ … rút một lần cho mỗi hạt giống." | Thêm vào Ví dụ 08.6, Bước 1: "Với mỗi hạt giống, $w^\star$ cố định xác định $D$; cận đúng cho từng $D$, nên đúng cho trung bình." |
| nhẹ | 25, 90, 491, 540, 866, 872, 401 | `no-ai-slop` Detect. (1) Câu chốt kiểu châm ngôn ở 540 và 872. (2) Đoạn tóm tắt lặp lại điều vừa nói ở 401 và 866. (3) Tương phản nhị phân ở 25, 90, 491 và 540. Các tương phản cần cho độ chính xác (439, 861) giữ nguyên. | 540: "đường cong của thí nghiệm không phải là cận, và cận không dự đoán được hình dạng của chúng". 872: "Bảo đảm cấp lớp và bảo đảm cấp thuật toán không thay được nhau." 401: "Cận của Mệnh đề 08.5 tăng tuyến tính … $0{,}8705$ so với $1{,}5$ sau sáu bước." | 540: cắt mệnh đề sau dấu chấm phẩy. 872: bỏ câu, vì hai câu trước đã đủ. 401 và 866: cắt cả đoạn (xem bảng cắt). 25: "Bảng là bằng chứng thí nghiệm; giao thức ở Phụ lục D." |
| nhẹ | 1080 | Thời gian chạy đo được khác số ghi trong bài. | "Khoảng $15$ giây trên một máy nhiều nhân." | "Khoảng $15$–$25$ giây trên một máy nhiều nhân." |

## Cân đối số chữ (thân bài đang ở 11 946/12 000)

Tổng phần thêm khoảng 160 tiếng; tổng phần cắt khoảng 170 tiếng, nên số chữ của thân bài không tăng.

**Thêm**

| Vị trí | Nội dung | Ước lượng |
|---|---|---|
| 193 | Ví dụ ghép cặp một bước | +45 tiếng |
| 538 | Giải thích $\Delta$ ghép cặp > không ghép cặp | +35 tiếng |
| 666, 678 | Hai câu cho Ví dụ 08.7 | +40 tiếng |
| 213 | Câu nối ngân sách với kì vọng | +25 tiếng |
| 202 | Cột đạo hàm của lần chạy trên $s^{(4)}$ | +8 tiếng |
| 377 | Câu kiểm $\Delta_3=1$ | +20 tiếng |
| Các dòng khác | Sửa câu | khoảng 0 |

**Cắt**

| Vị trí | Nội dung | Ước lượng |
|---|---|---|
| 25 | Câu thứ hai (lỗi phân lớp; đã có nguyên văn ở dòng 693) | −25 tiếng |
| 401 | Cả đoạn (lặp lại kết luận Ví dụ 08.4) | −30 tiếng |
| 866 | Cả đoạn (tóm tắt §9) | −40 tiếng |
| 885 | Gạch đầu dòng "Cận trên" (lặp lại dòng 25 và Ví dụ 08.6, Bước 3) | −20 tiếng |
| 874 | Vế sau dấu chấm phẩy (lặp lại kết luận Ví dụ 08.7) | −15 tiếng |
| 872 | Câu cuối | −12 tiếng |
| 11 | Câu cuối (thay bằng cột "Cận") | −15 tiếng |
| 42 | Ví dụ 06.9 trong danh sách tiên quyết | −6 tiếng |
