# Rà lại mạch, móc nối và văn phong sau biên tập vòng 1 — Bài 04

Phát hiện mới: chặn bàn giao 0 · nghiêm trọng 0 · trung bình 1 · nhẹ 10.

Đầu vào: `scratchpad/lec04-round1-frozen.md`, 1229 dòng, trùng từng byte với `2627-1/materials/lec-04/lecture-note.md` (đã kiểm bằng `cmp`). Số dòng dưới đây theo bản này. Tôi đã đọc toàn bộ bản đóng băng, cả năm phụ lục. Phát hiện về câu chữ viết theo chế độ Detect của `no-ai-slop`: trích câu, đề xuất sửa, không viết lại.

**Kiểm tra máy.**
- `forward_refs.py` chạy trên bản sao `scratchpad/rev04/fr2/lec-04/lecture-note.md`: **`0 forward references`**.
- `wc -w`: thân bài (trước `## Phụ lục`) có **11 997** tiếng, không quá 12 000; phụ lục có 1 853 tiếng, không quá 3 000.
- Số tiếng theo mục, so với dàn ý: §4 1662 (dự kiến 1650), §5 1861 (1700), §6 2971 (2700), §7 1204 (1150), §8 865 (1050), §9 378 (450).

## 1. Trạng thái các quyết định

| Mục | Trạng thái | Bằng chứng (dòng) |
|---|---|---|
| N1 | ✓ | 636–640: biến cố hỏng của một lớp là $L_S\in\{0,1\}$, xác suất $2^{-9}$; xác suất thất bại $0{,}858$ và $0{,}99994$; câu $0{,}6236$ được giữ cho riêng $L_S=0$. 987: $0{,}86$. |
| N2 | ✓ | Không còn "độ tin cậy" theo nghĩa $\delta$ (grep 0). "Cận trên tin cậy" và "mức $95\%$" vẫn đúng nghĩa. Tiêu đề §6, Ví dụ 04.7, 04.8, Hệ quả 04.15 đã sửa. |
| N3 | ✓ | Câu dẫn 462 viết thẳng cách đọc sẽ bị bác. 480: cách đọc cho hàm phân lớp. 482: bác cách đọc ($0{,}58$/$0{,}90$; $0{,}25$/$0{,}81$). Còn vấn đề thuật ngữ, xem T3. |
| N4 | ✓ | 285–299: tiêu đề mới; câu dẫn khớp ba nhãn danh từ; bốn bước ngắn. Thứ tự câu lý do còn lệch, xem T7. |
| N5 | ✓ | Có $k_{\max}$ (96, 512, 625, 853, 1110). $K$ chỉ còn cho danh sách giả thuyết hay ứng viên. Dòng 532 dùng $\lvert\mathcal H\rvert$. Dòng 625 ghi "với $K=k_{\max}$ của bài tập đó". |
| M1 | ✓ | 691: vế phải là giá trị một người biết $D$ dùng để so các lớp; không còn "SRM đạt mức đó". |
| M3 | ✓ | 144, 282, 301: "cận … tăng theo lớp"; sai số xấp xỉ "không tăng". |
| M4 | ✓ | Chỉ còn một lần, ở câu mở §7 (807), đúng phạm vi (bán kính của Định lý 02.14(a), 03.15(a); $\mathrm{pen}_k\to\infty$, Phụ lục A; "cận không cho cỡ mẫu chung"). Dòng 650 cũ đã bỏ. |
| M6 | ✓ | 1050 ($\min_{\mathcal H}L_D$, rủi ro tuyệt đối), 1053 (ví dụ đa thức của UML §11.2; $\lvert Y\rvert\le B$). |
| M7 | ✓ | 146: tiêu đề "… sai số tối ưu thực nghiệm". 1040: "độ chênh tối ưu (suboptimality)" và câu hỏi thẳng "Câu hỏi cho Bài 05 là: …". |
| M16 | ✓ | 25, đúng câu chữ của quyết định. |
| M17 | ✓ | "Lỗi kiểm tra kì vọng" (334, 373, 426); "nhãn kiểm tra" (311, 332, 435); "rủi ro kì vọng" (796, 986); "tối thiểu hóa" (643, 768); "Phép kéo theo ngược lại" (883); $\mathrm{pr}_k$ chỉ ở Phụ lục C; $v^\star$, $\varphi$ ở Phụ lục A, B. Grep không còn tên cũ. |
| M18 | ✓ | Không còn con trỏ bằng lời tới một khối phía sau. "Quy tắc sau", "Định lý sau", "Ví dụ sau" trỏ khối liền kề, như Bài 03. |
| M21 | một phần | Các câu cũ đã tách (480 thay 435 cũ; 800; 950 thành danh sách 984–989; 342). Biên tập lại sinh bốn câu trên 40 tiếng: 480 (43), 768 (45), 899 (48), 941 (42). Câu 941 do gộp hai câu cũ. Xem T5. |
| M22 | ✓ | 282/301 không còn trùng ý; câu "không phải cận với xác suất cao" chỉ ở 342; câu cuối §7 cũ đã bỏ; cuối §8 (974) còn một câu chung; so sánh SRM với xác thực chỉ ở §9 (980). |
| M23 | ✓ | 978: câu hỏi cầu nối của Bài 03 ($0{,}3651$ so với $0{,}4350$) và câu hỏi mở đầu (không có cận đều cho đa thức với hàm lỗi bình phương; Ví dụ 04.4; khi $\lvert Y\rvert\le B$ và cắt dự đoán thì dùng Nhận xét 04.18). Đúng phạm vi đã chứng minh. |
| C | ✓ | Đã áp dụng các chỗ cắt; thân bài 11 997 tiếng. Việc chuyển chứng minh sang phụ lục được kiểm ở mục 3. |

**Kiểm tra ngẫu nhiên các mục nghiêm trọng và trung bình ngoài danh sách.**
- R1: M5 ✓ (766, 1028; Nhận xét 01.19), M9 ✓ (151, 168), M10 ✓ (376–392), M11 ✓ (Phụ lục D Bước 2), M12 ✓ (bảng mười hàng 753–764; $0{,}0058$; $0{,}0130$), M13 ✓ (831), M14 ✓ (872), M15 ✓ (1037).
- R4 #3–#23: ✓. Riêng #18 là một phần, xem M21.
- R3 M2: ✓ (250).

**18 phát hiện của tôi ở vòng trước** (`5-mach.md`).

| # | Trạng thái | Ghi chú |
|---|---|---|
| trung bình (§9 khép câu hỏi mở đầu) | ✓ | 978 |
| 2 (650/752/756) | ✓ | chỉ còn 807 |
| 3 (868/872) | ✓ | câu cuối §7 cũ đã bỏ; xem T8 về câu tóm tắt còn lại |
| 4 (938/948) | ✓ | 974, 980 |
| 5 (con trỏ 192, 602, 778) | ✓ | |
| 6 ($0{,}3379$) | ✓ | 774: $0{,}338$, $0{,}574$ |
| 7 ($0{,}0131$) | ✓ | 772: $0{,}0130$; câu về hai bộ trọng số đã bỏ |
| 8 (mục tiêu 5) | ✓ | 25 |
| 9 (tiêu đề Nhận xét 04.4) | ✓ | 285 |
| 10 (thuật ngữ) | ✓ | 146, 1040; công thức "dạng chiều VC" ở 536–542 |
| 11 ($K$ hai nghĩa) | ✓ | N5 |
| 12 (phản ví dụ $0{,}25$) | ✓ | 190, sau Ví dụ 04.2 |
| 13 (mở §5) | ✓ | 305 |
| 14 (Bài tập 02.11) | ✓ | 32 |
| 15 ($\mathcal G_S$) | ✓ | 780 |
| 16 (độ dài) | một phần | §7 về đúng ngân sách (1204); §6 vẫn +10%, §8 −18%. Không bắt buộc sửa. |
| 17 ("được phụ thuộc", "hẳn") | ✓ | 827, 883 |
| 18 (cầu nối lồi / 0–1) | ✓ | 1040 |

## 2. Phát hiện mới do lượt biên tập

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | §2, dòng 99–101 | **Bảng kí hiệu bị cắt đôi.** Dòng trống 100 nằm giữa hai hàng, nên Markdown kết thúc bảng sau hàng $p$. Hàng $\epsilon$ còn lại không có dòng tiêu đề và dòng phân cách, nên hiển thị thành một đoạn văn có các dấu `|`. Lỗi này không sinh `.katex-error` hay yêu cầu hỏng, nên kiểm Playwright của biên tập viên không bắt được. Hàng $\ln$ cũng bị xóa; việc này chấp nhận được, vì $\ln$ là kí hiệu chuẩn. | 99: `\| $p$ \| số chiều đặc trưng, …\|`; 100: dòng trống; 101: `\| $\epsilon$ \| tham số độ chính xác: …\|` (diff: dòng trống đi kèm thay đổi ở hàng $\epsilon$). | Xóa dòng trống 100. Sau khi sửa, kiểm lại §2 bằng mắt ở 1600 px và 390 px. |
| nhẹ | dòng 203 so với 290 | Câu ở 203 giờ là một câu nhử: nói hiệu này "là một đại lượng khác" nhưng không nói khác thế nào, và con trỏ đã bị bỏ theo M18. Cùng một hiệu còn có hai tên: "hiệu tổng thể" (203) và "hiệu theo rủi ro kì vọng" (290). | 203: "Hiệu tổng thể $L_D(\tilde h)-L_D(\hat h)$, với $\hat h$ là một nghiệm ERM, là một đại lượng khác." 290: "**Hiệu theo rủi ro kì vọng.** Hiệu $L_D(\tilde h)-L_D(\hat h)$…" | Xóa câu 203 (bớt 17 tiếng); Nhận xét 04.4 đã giới thiệu hiệu này với tên duy nhất. |
| nhẹ | Ví dụ 04.6, dòng 462, 469–484 | Hai thuật ngữ mang hai nghĩa trong năm dòng. "Phương sai" của $A$ là $0{,}24$ ở Bước 2 (Định nghĩa 04.5) nhưng $0{,}4$ ở Bước 3 (nghĩa phân lớp). "Độ chệch" của hai thuật toán "như nhau" ở Bước 3 nhưng "$0{,}25$ so với $0{,}81$" ở Bước 4. Câu dẫn và Bước 4 còn diễn đạt cách đọc bị bác bằng hai câu khác nhau. | 478–480: "phương sai là xác suất dự đoán khác dự đoán đa số … phương sai là $0{,}4$ với $A$". 469: "phương sai $0{,}4\cdot0{,}6=0{,}24$". 462: "khi độ chệch như nhau, phương sai lớn hơn cho lỗi lớn hơn"; 482: "cùng độ chệch thì phương sai nhỏ hơn tốt hơn". | Ở Bước 3–4 viết "độ chệch theo nghĩa phân lớp" và "phương sai theo nghĩa phân lớp" (hoặc đặt tên khác, chẳng hạn "tần suất lệch khỏi dự đoán đa số"). Ở Bước 4, trích lại đúng câu đã dùng ở 462. |
| nhẹ | Ví dụ 04.8, Kết luận, dòng 640 | Kết luận chứa một phép tính mới (chia đều, $\ln40\,000$, $0{,}7279$). Trước đây phép tính này là Bước 3; nay bị dồn vào Kết luận, trái `van-phong.md` §7a. | 640: "Với $q_k=1/k_{\max}$, $k_{\max}=1000$, bán kính thành $\sqrt{\ln40\,000/20}\approx0{,}7279>\tfrac12$ và bổ đề đúng trên mọi mẫu." | Tách thành "**Bước 4: khi chia đều.**" ngay trước Kết luận (thêm khoảng 4 tiếng). |
| nhẹ | dòng 480, 768, 899, 941 | Bốn câu trên 40 tiếng do lượt biên tập sinh ra (43, 45, 48, 42 tiếng). Câu 941 gộp hai câu vốn đã tách ở bản trước. Câu 899 nhồi ba điều kiện vào một mệnh đề "Nếu". | 941: "Khi biết $S$, $K$ ứng viên là một lớp hữu hạn cố định, và theo (T7) mẫu $V$ vẫn có phân bố $D^{m_v}$ (Nhận xét 01.9), nên (T1) và (T4) thỏa …". 899: "Nếu $\mathcal H$ là hợp đếm được …, mỗi lớp thỏa (M), và có một cách chọn nghiệm SRM chính xác làm $A_{\mathrm{SRM}}$ … thỏa Định nghĩa 01.4, thì …". | 941: tách lại sau "cố định". 899: chuyển điều kiện đo được thành một nhãn trong **Giả thiết.** ("**Thuật toán, cho phần (b).** …"), như Mệnh đề 04.3. 480 và 768: tách sau dấu phẩy thứ nhất. Số tiếng không đổi. |
| nhẹ | Ví dụ 04.9 Bước 3, dòng 768 | "Cố định trước mẫu" có thể gắn sai chủ ngữ: câu đọc được như thể hàm được chọn là cố định trước mẫu. | "luôn chọn một hàm của lớp lớn nhất $\mathcal H_{10}$, cố định trước mẫu, nên Định lý 03.15 cho riêng $\mathcal H_{10}$ áp dụng" | "… luôn chọn một hàm của lớp lớn nhất $\mathcal H_{10}$. Lớp này cố định trước mẫu, nên Định lý 03.15 áp dụng cho riêng $\mathcal H_{10}$ với $\delta$ không chia: …" |
| nhẹ | Nhận xét 04.4, dòng 290–298 | Câu lý do đứng trước phép tính chứng minh nó, và nhận xét kết thúc ở con số $-0{,}10$, không có câu nối lại với lý do. | 290: "… và có thể âm, như phép tính dưới đây. Vì vậy học phần dùng đại lượng thực nghiệm, không âm, $\operatorname{opt}_S$." 298: "**Hiệu.** … $=-0{,}10$." | Chuyển câu "Vì vậy học phần dùng … $\operatorname{opt}_S$." xuống sau bước **Hiệu.** |
| nhẹ | cuối §7, dòng 904 (`no-ai-slop` Detect: kết bằng tóm tắt) | Hai câu đầu của đoạn kết nhắc lại Hệ quả 04.15(a)(b) và kết luận của Ví dụ 04.11. | "Với một danh sách hữu hạn lớp, $A_{\mathrm{SRM}}$ là thuật toán học PAC bất khả tri cho hợp các lớp; với một danh sách đếm được, nó là thuật toán học không đều (Hệ quả 04.15). Theo Ví dụ 04.11, một lớp có chiều VC vô hạn vẫn có thể học được không đều; …" | Chỉ giữ vế "lớp mọi hàm trên một miền vô hạn được xét ở ý thử thách của Bài tập 04.11", viết thành một câu (bớt khoảng 35 tiếng). Câu mở §8 (908) đủ để chuyển mục. |
| nhẹ | dòng 384 | "Thiết kế ngẫu nhiên" xuất hiện lần đầu không có tiếng Anh và không có câu giải thích, trong khi "thiết kế cố định (fixed design)" đã được định nghĩa ở 108. | "Với thiết kế ngẫu nhiên, khi $X\sim D_{\mathcal X}$ và $(X,Y)$ độc lập với $S$, …" | "Với *thiết kế ngẫu nhiên* (random design), tức đầu vào $X\sim D_{\mathcal X}$ độc lập với $S$, …" |
| nhẹ | Phụ lục E, Bước 3, dòng 1226 | Đếm "dòng" trong một chuỗi bất đẳng thức; R1-4 đã bỏ cách đếm này ở thân bài. | "dòng cuối của Bước 1 bằng …" | "vế phải cuối cùng của chuỗi ở Bước 1 bằng …" |
| nhẹ | ranh giới §6/§7, dòng 803 | Câu kết §6 giờ chỉ tóm tắt, không còn dẫn sang nhu cầu của §7; nhu cầu đó chỉ còn ở câu mở 807. Mạch vẫn liền, vì 807 mở bằng Định lý 04.11. | 803: "SRM thay câu hỏi chọn lớp bằng một bài toán tối ưu có phạt, và Định lý 04.11 so đầu ra của nó với mốc có phạt." | Không bắt buộc. Có thể thêm "; cận đó còn phụ thuộc $\delta$, một đầu vào của quy tắc", vì 831 dùng lại ý này mà không lặp M4. |

## 3. Phần chuyển sang phụ lục và ranh giới mục

**Thân bài vẫn đọc được khi không mở phụ lục.**
- 139: chiều VC $d_k=k+1$ được nêu cùng lý do ngắn (Mệnh đề 03.9 qua phép chiếu). Chứng minh ở Phụ lục C.
- 400: nghiệm bậc $1$ được nêu. Hệ phương trình chuẩn ở Phụ lục C.
- 739–746: phát biểu $\tau=\epsilon_{\mathrm{opt}}+\tau'$ và công thức cận tinh hơn nằm trong thân bài. Chứng minh ở Phụ lục E, có lộ trình.
- 864: lộ trình chứng minh Hệ quả 04.15 nằm trong thân bài. Chứng minh đủ ở Phụ lục B.
- 902: con trỏ tới Phụ lục D.
- Mọi chỗ dẫn "Phụ lục A–E" đều có đích. Phụ lục A Bước 4 thật sự chứng minh $\mathrm{pen}_k\to\infty$, điều mà 807 dẫn.

**Nhãn độ sâu chứng minh trung thực.**
- "Hệ quả 04.15 … — chứng minh đầy đủ ở Phụ lục B": Phụ lục B có đủ bốn bước.
- Định lý 04.16 "— đọc thêm", với Phụ lục D tên "Ý chứng minh": nhất quán.
- Hệ quả 04.17 "— phác thảo": Bước 3 nói rõ phần nào là phác thảo.
- Các khối ghi "chứng minh đầy đủ" khác (Mệnh đề 04.3, 04.6, Bổ đề 04.9, Định lý 04.11) vẫn có chứng minh đủ trong thân bài.

**Ranh giới mục.** Mỗi mục mở bằng nhu cầu do mục trước để lại: §4 (148), §5 (305), §6 (512), §7 (807), §8 (908). Mỗi mục kết bằng văn xuôi. Chỗ còn có thể cải thiện là 803 và 904 (T8, T11).

**§9 và cầu nối.**
- §9 tổng hợp thay vì nhắc lại. Đoạn 978 trả lời cả hai câu hỏi (cầu nối Bài 03 và câu hỏi mở đầu). Danh sách 984–989 gom bốn giả thiết, mỗi giả thiết có con số. Đoạn 991 về chính quy hóa nêu một điểm khác cụ thể, dựa trên (T6).
- Cầu nối (1040) theo đúng blueprint. Nó dùng "độ chênh tối ưu", câu hỏi viết thẳng, có vế "hàm lỗi lồi theo tham số thay cho hàm lỗi 0–1", và không khẳng định ERM khó tính.

**Số lặp lại giữa các mục.** Đều nhất quán:
- cận $0{,}3651$ (766, 774, 978) và $0{,}4350$ (768, 774, 978);
- $0{,}338$/$0{,}574$ (774), so với $0{,}329$/$0{,}560$ (13, 774);
- $0{,}858$ (638, 640) và $0{,}86$ (987);
- $0{,}0468$ (788, 792, 796, 986);
- $0{,}75$/$1{,}25$ (438, 453, 988);
- $0{,}3750$ và $0{,}3751$ ở lời giải câu hỏi cuối buổi (1024, 1028), dùng đúng quy tắc làm tròn D: số trong bảng làm tròn gần nhất, số đứng sau "$\le$" làm tròn lên.

## Kết luận

**Giao được sau khi sửa T1** (xóa dòng trống 100, kiểm lại §2 bằng mắt). Mọi quyết định N1–N5, M1, M3, M4, M6, M7, M16–M18, M22, M23 và C đã được thực hiện; M21 thực hiện một phần. Mười phát hiện nhẹ có thể sửa cùng lượt đó, không cần một vòng rà nữa. Các sửa đề xuất cộng lại làm thân bài ngắn đi khoảng 50 tiếng.
