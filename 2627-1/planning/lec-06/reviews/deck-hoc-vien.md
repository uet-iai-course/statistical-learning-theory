# Duyệt deck Bài 06 — vai `hoc-vien` (học viên cao học)

Bản duyệt: `2627-1/lecture-06-on-dinh-chinh-quy-hoa.html` (bản đóng băng, 55 trang), đọc sau ghi chú `materials/lec-06/lecture-note.md`. Chỉ đọc; không sửa deck, SVG, storyboard, ghi chú.

## Kiểm máy đã chạy (2026-11-15)

- `deck_lint.py`: 0 phát hiện.
- `footer_check.py` (1600×900): 0 trang chạm chân trang hoặc đáy khung.
- `deck_check.py --shots`: console 0, pageerrors 0, failed 0, `.katex-error` 0. Mọi mục OVERFLOW là `path` SVG của `\sqrt` (báo động giả đã biết). Ở 390 px không trang nào cuộn ngang cả trang (`docScrollW = 390` ở mọi trang); các công thức và bảng rộng cuộn ngang tại chỗ.
- Đã xem toàn bộ ảnh 1600×900 và 390×844, kể cả mọi ảnh `-end` (bảng ghép trong thư mục nháp `rv-hoc-vien/sheets/`).

## Đếm mật độ

Cách đếm như `deck_lint.py`: âm tiết là token cách nhau bởi khoảng trắng; không tính tiêu đề, KaTeX, số trong bảng, nhãn hình, dòng từ khóa mạch, ghi chú; số viết trong câu và chữ trong bảng có tính. Trần 60 (80 cho Mục tiêu, Nội dung, bảng tổng kết); mục tiêu 40.

| Trang | Âm tiết | Trang | Âm tiết | Trang | Âm tiết |
|---|---|---|---|---|---|
| 1-02 | 48 | 2-12 | **60** | 4-07 | 57 |
| 1-03 (Mục tiêu) | 78 / 80 | 3-01 | 49 | 5-01 | 56 |
| 1-04 (Nội dung) | 45 | 3-02 | 58 | 5-02 | 54 |
| 1-05 | 27 | 3-03 | **60** | 5-03 | 34 |
| 1-06 | **60** | 3-04 | 34 | 5-04 | 45 |
| 2-01 | 48 | 3-05 | 47 | 5-05 | 47 |
| 2-02 | 59 | 4-01 | 59 | 6-01 | 49 |
| 2-03 | 56 | 4-02 | 59 | 6-02 | 49 |
| 2-04 | 56 | 4-03 | 43 | 6-03 | 48 |
| 2-05 | 49 | 4-04 | 58 | 6-04 | 54 |
| 2-06 | 39 | 4-05 | 58 | 6-05 | **60** |
| 2-07 | 49 | 4-06 | 55 | 6-06 | 33 |
| 2-08 | 57 | | | 7-01 (bảng) | 60 / 80 |
| 2-09 | 49 | | | 7-02 (bảng) | 51 / 80 |
| 2-10 | 49 | | | 7-03 | 57 |
| 2-11 | 46 | | | 7-04 | 57 |
| | | | | 7-05 | 30 |
| | | | | 7-06 | 48 |
| | | | | 7-07 | 47 |
| | | | | 7-08 | 44 |

Bìa 1-01: 73 (trang tổng quan; luận điểm một câu 49 âm tiết). Dòng dẫn mạch: 25, 17, 20, 23, 24, 17 (trần 25). **Không trang nào vượt trần.** Bốn trang chạm đúng 60 (1-06, 2-12, 3-03, 6-05); 19 trang nội dung từ 55 trở lên; trung vị trang nội dung khoảng 49, cao hơn mục tiêu 40.

Dòng trên 20 âm tiết (một `p` hoặc `li`; KaTeX không tính): 1-01 (49, luận điểm), 1-05 (27, hộp câu hỏi), 2-00 (25, dòng dẫn), 2-02 (23), 2-03 (22 Trực quan; 21 Bổ đề), 2-11 (22), 3-02 (21; 28), 4-01 (27), 4-02 (21), 4-03 (24), 5-00 (23, dòng dẫn), 6-00 (24, dòng dẫn), 6-02 (26), 6-04 (24), 6-05 (28), 7-03 (21), 7-04 (24). Đề xuất tách ở phát hiện "các dòng > 20 âm tiết" trong bảng dưới.

## Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L06-1-02, L06-2-04, L06-2-05, L06-1-06 | Kí hiệu của Bài 05 dùng trên mặt trang mà không giải nghĩa: nhãn (C), (G1), (G2); $\varphi$; $\bar w_T$; "Thuật toán 05.11". Người học chỉ đọc deck không biết (G1) là gì khi bước 1 ở 2-05 viết "Bổ đề 06.1(b) cho (G1) với $F=L_D$". | 1-02: "Hệ quả 05.15: với (C), (G1), (G2) cho $F$ … $\mathbb EF(\bar w_T)-F(u)\le RG/\sqrt T$"; 2-04: "Thuật toán 05.11 với $\xi_t=Z_t$, $\varphi=v$"; 2-05 bước 1–2. Ghi chú §2 có danh sách "(C) Tính lồi", "(G1) Tính không chệch. $\mathbb E_\xi\varphi(w,\xi)\in\partial F(w)$", "(G2) Cận mô-men bậc hai"; Câu hỏi mở đầu: "$\bar w_T$ là điểm lặp trung bình (averaged iterate)". | Thêm ở 1-02 một dòng "Nhắc lại:" ngắn: "(C) $F$ lồi, $W$ khác rỗng, đóng, lồi; (G1) $\mathbb E_\xi\varphi(w,\xi)\in\partial F(w)$; (G2) $\mathbb E_\xi\lVert\varphi(w,\xi)\rVert^2\le G^2$; $\bar w_T$: điểm lặp trung bình (averaged iterate) của SGD có chiếu (Thuật toán 05.11)". Để giữ trần 60, chuyển dòng định nghĩa lồi mạnh từ 1-02 sang 3-03 (nơi Bổ đề 06.7 dùng nó lần đầu) dưới dạng "Nhắc lại:". |
| trung bình | L06-2-01 (dùng ở 2-05, 2-09, 4-03, 4-04, 6-03, 7-01, 7-03) | Nhãn (T1) và hai dạng "dạng đầy đủ"/"dạng yếu" không có nội dung trên mặt trang nào; nội dung chỉ ở ghi chú diễn giả 2-01. "Dạng yếu" được giải nghĩa tại chỗ ở 2-09 ("mỗi $Z_i\sim D$"), "dạng đầy đủ" thì không. Đây lại là giả thiết then chốt của Định lý 06.10 (bước 2 ở 4-04, Câu hỏi tự kiểm tra 2). | 2-01: "$S=(Z_1,\ldots,Z_m)\sim D^m$ theo (T1), dùng nhiều lần"; 4-03: "theo (T1) dạng đầy đủ". Ghi chú §2: "(T1) Lấy mẫu. Các quan sát … độc lập cùng phân bố theo $D$. Ở dạng yếu, mỗi $Z_i$ có phân bố $D$, không cần độc lập." | Ở 2-01 thêm một gạch đầu dòng: "(T1): các quan sát độc lập cùng phân bố $D$ (dạng đầy đủ); dạng yếu: mỗi $Z_i\sim D$." Bù mật độ bằng cách rút gạch "Mục tiêu: …" thành "Mục tiêu: $\mathbb EL_D$ của đầu ra so với $\inf_WL_D$". |
| trung bình | L06-4-04 | Bước nhảy trong ý tưởng chứng minh: bước 4 nói "mỗi hiệu có trị tuyệt đối $\le\epsilon_{\mathrm{stab}}(m)$" nhưng hiệu nào thì chưa viết; đẳng thức "khoảng cách = trung bình thay một" chỉ xuất hiện ở 4-05, sau trang chứng minh. Người nghe phải tự ghép bước 1–3 thành hiệu $\ell(A(S^{(i)};\xi),Z_i)-\ell(A(S;\xi),Z_i)$. | 4-04 bước 3: "$\mathbb EL_S(A(S;\xi))=\frac1m\sum_i\mathbb E\,\ell(A(S;\xi),Z_i)$"; bước 4: "Cố định $(S,Z')$, lấy kì vọng theo $\xi$: mỗi hiệu có trị tuyệt đối $\le\epsilon_{\mathrm{stab}}(m)$". 4-05: "khoảng cách tổng quát hóa kì vọng bằng trung bình thay một $\tfrac1m\sum_i\mathbb E[\ell(A(S^{(i)};\xi),Z_i)-\ell(A(S;\xi),Z_i)]$". | Gộp vào cuối bước 3 (bằng chữ, không cần công thức hiển thị mới): "trừ: khoảng cách $=\tfrac1m\sum_i\mathbb E[\ell(A(S^{(i)};\xi),Z_i)-\ell(A(S;\xi),Z_i)]$". Quyết định N2 của cổng duyệt chỉ cấm đặt công thức này trước định lý; trang chứng minh đứng sau định lý nên được phép. |
| trung bình | L06-5-03 | Số $0{,}3810$ xuất hiện hai lần trên cùng trang với hai nghĩa: vế phải bước 2 của chứng minh và khoảng cách thật giữa hai nghiệm. Học viên đọc dòng 2 sẽ hiểu $0{,}3810$ là $\lVert\hat w-\hat w'\rVert$ và không thấy chuỗi bất đẳng thức kiểm cái gì. Hai số trùng nhau thật ($168/441=8/21$). | 5-03: "$\lambda\lVert\hat w-\hat w'\rVert^2\approx0{,}1451\le0{,}3810\le2G\lVert\hat w-\hat w'\rVert/m\approx0{,}7619$" và "Khoảng cách thật $0{,}3810\le2$". Ghi chú diễn giả: "số giữa $0{,}3810$ là vế phải của bước 2 … $240/441$ và $432/441$ chia cho $m=4$". | Ghi tên số giữa trên mặt trang: "… $\le\tfrac14(\tfrac{240}{441}+\tfrac{432}{441})\approx0{,}3810\le$ …", và trong ghi chú diễn giả thêm một câu: vế phải bước 2 ở đây bằng đúng khoảng cách $8/21$. |
| trung bình | L06-3-03, L06-5-02 | 5-02 dẫn "Bổ đề 06.8(c)" nhưng 3-03 phát biểu Bổ đề 06.8 không có nhãn (a), (b), (c); học viên không tìm được phần (c) trên deck. | 3-03: "**Bảo đảm:** tất định: $F_{s,\lambda}$ $\lambda$-lồi mạnh, có điểm cực tiểu duy nhất $\hat w_s$ trên $W$, tăng trưởng bậc hai (quadratic growth) quanh $\hat w_s$." 5-02 bước 1: "(Bổ đề 06.8(c); …)". Ghi chú: "(a) Lồi mạnh. (b) Tồn tại. (c) Duy nhất và tăng trưởng bậc hai." | 3-03: "(a) $F_{s,\lambda}$ $\lambda$-lồi mạnh; (b) có điểm cực tiểu trên $W$; (c) điểm đó duy nhất, kí hiệu $\hat w_s$, và tăng trưởng bậc hai quanh $\hat w_s$." |
| trung bình | L06-2-08, 2-09, 3-03, 3-05, 4-01, 4-03, 4-05, 5-02, 6-01 | Ở 390×844, công thức hiển thị chính của trang tràn khung và bị cắt; phần kết luận ("$\le\epsilon_{\mathrm{stab}}(m)$" của Định lý 06.10, vế phải của bất đẳng thức then chốt ở 5-02, nửa sau đẳng thức phân tích ở 2-09 và 6-01) chỉ thấy khi cuộn ngang. Quy định "The author's voice": tách bằng `aligned` khi công thức tràn hộp ở 390 px. | Ảnh `narrow-028-L06-4-03.png`: "$\lvert\mathbb E_{S,\xi}[L_D(A(S;\xi))-L_S(A(S;$" bị cắt; `narrow-035-L06-5-02.png`: "$\lambda\lVert\hat w-\hat w'\rVert^2\le\frac1m[\ell(\hat w',z_i)-$" bị cắt; `narrow-040-L06-6-01.png`, `narrow-015-L06-2-09.png`, `narrow-026-L06-4-01.png`, `narrow-030-L06-4-05.png`, `narrow-022-L06-3-03.png`. `deck_check`: narrowWide 5–142 phần tử ở các trang này. | 4-03 và 2-08: dùng $\tilde w=A(S;\xi)$ như 2-09 và 7-03 (đặt $\tilde w$ ngay ở 2-08), công thức còn $\lvert\mathbb E[L_D(\tilde w)-L_S(\tilde w)]\rvert\le\epsilon_{\mathrm{stab}}(m)$. 2-09, 6-01: `aligned` một ngoặc vuông mỗi dòng. 4-01, 4-05, 5-02, 3-05: `aligned` tách tại dấu quan hệ hoặc dấu trừ giữa hai số hạng. 3-03: đưa "$\forall w\in W$" ra chữ trước công thức ("với mọi $w\in W$:"). Đo lại ở 390 px trước khi chốt. |
| trung bình | toàn deck (1-06, 2-12, 3-03, 6-05 bằng 60; 2-02, 4-01, 4-02 bằng 59) | Mật độ sát trần một cách hệ thống: 19 trang nội dung từ 55 âm tiết, trung vị khoảng 49 so với mục tiêu 40. Không vượt trần, nhưng người nghe lần đầu đọc không kịp ở các trang 59–60. | Bảng đếm ở trên. | Cắt cụ thể: 1-06 bỏ "$L_D(w)=w^2+1$" khỏi gạch đầu (đưa vào ghi chú diễn giả; trang 2-06 đã dùng lại) và rút gạch SGD thành "SGD có chiếu, $w_1=0$, $T=1600$, $\eta=0{,}00625$"; 2-12 bỏ "và chỉ ra giả thiết làm độ chệch bằng 0" (lời giải (d) đã nói); 3-03 bỏ "Trực quan." sang ghi chú diễn giả hoặc rút còn "Độ cong $\lambda$ cộng thêm $\tfrac\lambda2\lVert w-u\rVert^2$ quanh điểm cực tiểu"; 6-05 xem phát hiện về L06-6-05. |
| trung bình | L06-6-05 | Dòng "Chia khối và xác thực" không hiểu được tại chỗ: chưa nói khối là gì, chạy gì trên khối, chọn ứng viên thế nào; "xác thực" thiếu tên tiếng Anh. Trang đã 60 âm tiết. | "Chia khối và xác thực (hàm lỗi trong $[0,1]$): $\lceil\log_2(2/\delta)\rceil$ khối thay cho thừa số $1/\delta^2$." Ghi chú diễn giả mới có cơ chế (khối huấn luyện, mẫu xác thực cỡ $8\ln(4k/\delta)/\epsilon^2$, chọn ứng viên có rủi ro thực nghiệm nhỏ nhất). | Thay bằng: "Bài tập 06.7: chạy quy tắc trên $\lceil\log_2(2/\delta)\rceil$ khối rời nhau, chọn đầu ra tốt nhất trên một mẫu xác thực (validation sample); hàm lỗi trong $[0,1]$." và rút "Nhận xét 06.14." còn "Hệ quả 06.2, Định lý 06.10, Hệ quả 06.13: kì vọng, một thuật toán; Bài 02–04: xác suất $\ge1-\delta$, cả lớp." để giữ ≤ 60. |
| nhẹ | L06-2-09 (tiêu đề), L06-2-00 (tên mạch) | "Tập huấn luyện cố định" dễ hiểu là tập không ngẫu nhiên, trong khi trang lấy kì vọng theo $S$; 2-01 lại gọi là "tập huấn luyện lưu lại". Ghi chú diễn giả 2-11 phải nói thêm "Tập huấn luyện ở đây là ngẫu nhiên". | Tiêu đề 2-09 "Phân tích rủi ro trên một tập huấn luyện cố định"; 2-01 "Chế độ B, tập huấn luyện lưu lại". Ghi chú §5: "Tối ưu trên một tập huấn luyện cố định". | Deck theo ghi chú nên giữ tên mạch; với tiêu đề 2-09 có thể dùng "Phân tích rủi ro cho đầu ra tính trên tập huấn luyện" (không đổi thuật ngữ). Xem mục Đề xuất sửa ghi chú. |
| nhẹ | L06-2-11 | "Mệnh đề 06.5(b) với $u=0$" lẫn hai phần: (b) không có $u$, nó so với $\inf_WL_D$; ở đây $\inf_WL_D=L_D(0)=1$. | "Mệnh đề 06.5(b) với $u=0$: $0{,}4750+0{,}0011=0{,}4761\ge0{,}2261$." | "Mệnh đề 06.5(b), $\inf_WL_D=L_D(0)=1$: …". |
| nhẹ | L06-4-07 | Lời giải (b2) kết thúc bằng hai so sánh số không ghi đại lượng; học viên phải đoán $0{,}75$ là hệ số ổn định với $m=2$, $1$ là cận Lipschitz, $0{,}25$ là khoảng cách của (b1). | "$m=2$: $0{,}75&lt;1$, $0{,}25\le0{,}75$." | "$m=2$: hệ số $0{,}75$ nhỏ hơn cận Lipschitz $2/m=1$; khoảng cách $0{,}25\le0{,}75$." |
| nhẹ | L06-4-04 | "Các $Z_i$ là bản sao của nhau" chưa nói rõ là cùng một biến ngẫu nhiên; người nghe có thể hiểu "bản sao" là các bản độc lập cùng phân bố, đúng là trường hợp định lý áp dụng. | "Các $Z_i$ là bản sao của nhau: bước 2 hỏng." | "$Z_1=\cdots=Z_m$ (mỗi $Z_i$ vẫn có phân bố $D$): bước 2 hỏng." |
| nhẹ | L06-5-02 | Dòng "Kỹ thuật." nén quá mức: "chỉ dùng một" (một bất đẳng thức tăng trưởng bậc hai) không có chủ ngữ. | "Cộng hai bất đẳng thức tăng trưởng bậc hai đối xứng; chỉ dùng một: hằng số $4G/(\lambda m)$." | "Cộng hai bất đẳng thức tăng trưởng bậc hai đối xứng; dùng một bất đẳng thức thì hằng số là $4G/(\lambda m)$." |
| nhẹ | L06-4-01 | Dòng mở trang không nói hàm lỗi của điểm nào đổi. | "Bốn quan sát, $\lambda=0$, thay $z_4$ bằng $z'=(1,-1)$: hàm lỗi tại $z=(1,-1)$ đổi $304/169\approx1{,}7988$." | "… hàm lỗi của nghiệm ERM tại $z=(1,-1)$ đổi …". |
| nhẹ | L06-4-05 | "Nhắc lại:" về mẫu bóng đứng cuối trang, sau công thức; bài học deck 02 yêu cầu "Nhắc lại:" đứng trước chỗ dùng. | "Nhắc lại: mẫu bóng (Bài 03) thêm $m$ quan sát." là dòng cuối. | Đưa lên ngay sau dòng "Kỹ thuật." hoặc gộp vào "Dùng khi …": "khác mẫu bóng (Bài 03) thêm $m$ quan sát, ở đây chỉ thêm một". |
| nhẹ | L06-7-03 | Gạch đầu dòng thứ nhất là câu dẫn ("…; theo kì vọng:") nhưng đứng ngang hàng với các ý trả lời; gạch thứ tư gộp hai kết quả (Định lý 06.10 và Mệnh đề 06.11 cùng Hệ quả 06.13). | "Tối ưu là học khi … nhỏ; theo kì vọng:" rồi "quan sát mới, …"; gạch 4 dài ba dòng ở 1600 px. | Câu dẫn thành đoạn `p` trước danh sách; tách gạch 4 thành "ổn định đều, (T1) dạng đầy đủ: …" và "$\ell$ lồi, (L), $\lambda&gt;0$ chọn trước: $\epsilon_{\mathrm{stab}}=2G^2/(\lambda m)$; với $\lambda^*$: …". |
| nhẹ | L06-1-01 | Luận điểm bìa một câu 49 âm tiết, khó đọc một lượt; "khi hàm lỗi thêm Lipschitz" là cụm lạ. | Bìa: "… trên tập huấn luyện lưu lại, khi hàm lỗi thêm Lipschitz, chính quy hóa chặn …". | "… khi hàm lỗi còn Lipschitz, …" và bỏ "thẳng" ("chặn rủi ro vượt mức kì vọng"). |
| nhẹ | L06-2-11, L06-3-04 (390 px) | Ở 390 px, bảng cuộn ngang và cột chứa số chính bị khuất: cột "khoảng cách tổng quát hóa kì vọng" ($0{,}4750$) ở 2-11; cột "khoảng cách" và $L_S(\hat w_S)$ ở 3-04. Ô tiêu đề dài ở 2-11 làm hàng tiêu đề cao gấp ba hàng số. Số vẫn có trong "Diễn giải:" (2-11) và trong Bài tập 06.6 (3-04 thì không). | `narrow-017-L06-2-11.png`, `narrow-023-L06-3-04.png`. | 2-11: rút tiêu đề cột thành "khoảng cách" (đã định nghĩa ở 2-08). 3-04: chấp nhận cuộn, hoặc bỏ cột $\hat w_{S^{(4)}}$ (suy từ $\hat w_S/5$; giữ trong ghi chú diễn giả) để bảng vừa 390 px. |
| nhẹ | L06-4-02, L06-3-04, L06-6-04 (390 px) | Chữ trong SVG khoảng 5–7 px ở 390 px ($Z_1$, $Z_i$, $Z'$ trong hình đổi vai; "mẫu S", trục, nhãn số hạng ở hai đồ thị). Số trên hình đều có lại trong chữ hoặc bảng, nên chỉ ảnh hưởng việc đọc hình. | `narrow-027-L06-4-02.png`, `narrow-023-L06-3-04-end.png`, `narrow-043-L06-6-04-end.png`. | Không bắt buộc sửa; nếu chỉnh SVG đổi vai, tăng cỡ chữ nhãn ô. |
| nhẹ | các dòng > 20 âm tiết | Một số dòng dài khó theo, nhất là dòng chứa hai ý. | Danh sách ở mục Đếm mật độ. | 3-02 (28): tách "Quy tắc $s\mapsto\hat w_s$: ERM có chính quy hóa (regularized ERM; còn gọi là chính quy hóa Tikhonov, Tikhonov regularization)." / "Với hàm lỗi bình phương: hồi quy ridge (ridge regression)." 4-01 (27): tách "$A$ ổn định đều … với hệ số ổn định … nếu với mọi $s$, $i$, $z'$ và mọi quan sát kiểm tra (test observation) $z$:" / công thức / "các kì vọng hữu hạn". 6-05 (28): xem phát hiện về 6-05. 6-04 (24): tách Ví dụ 06.10 thành dòng thiết lập và dòng "Mức $0{,}1$: …". 6-02 (26) và 4-03 (24): giả thiết thành danh sách ngắn như 2-04 (hai đoạn). 2-11 (22): "Diễn giải: $\mathbb E\operatorname{opt}_S\approx0{,}0011$ nhưng $0{,}2261&gt;0{,}1$; phần chênh là khoảng cách $0{,}4750$." 2-02, 2-03, 7-04 (22–24): giữ, mỗi dòng một ý. |

Tổng: 0 chặn bàn giao, 0 nghiêm trọng, 8 trung bình, 12 nhẹ.

## Nhận xét chung của người học

- Mạch đọc được: ví dụ hai chương trình ở 1-06 được trả lời số ở 2-06 ($0{,}000578$) và 2-11 ($0{,}2261$), rồi được nhắc lại ở 7-03 (ghi chú diễn giả); ví dụ hồi quy ridge đi qua 3-01, 3-04, 5-03, 5-05, 6-04. Đây là phần giúp hiểu nhất.
- Trực quan có ích: 2-03 (điểm lặp chưa thấy $Z_t$), 4-02 (hình đổi vai và thuật toán ghi nhớ), 5-01 (hiệu hai mục tiêu $(2G/m)$-Lipschitz, độ cong $\lambda$). Trực quan 2-09 ("gồm phần do đầu ra phụ thuộc $S$ và phần $\operatorname{opt}_S$") gần như nhắc lại phát biểu; chấp nhận được.
- Ví dụ đủ chậm, trừ 2-06 (hệ số $c_t$ không có công thức trên mặt trang; ghi chú diễn giả có $c_t=(1-q^{T-t})/T$) và 2-11 (khai triển $\mathbb E\bar w_T^2$ chỉ ở ghi chú diễn giả). Hai chỗ này đã có trong ghi chú bài giảng nên không ghi thành phát hiện.
- Các con số tôi kiểm khi đọc đều khớp: $\eta=1/160$; $8/21$, $64/441$, $168/441$, $16/21$ ở 5-03; $4/(2+\lambda m)$ ở 5-04; $99/(149+M^2)$; $(\lambda/(2+\lambda))^2$; $\lambda^*=0{,}2$, $6400$, $1599$; $m\ge(2GB/(\epsilon\delta))^2=2\,560\,000$; $Q(\lambda_0)=0{,}5$, $Q(\lambda^*)=0{,}4$; Câu hỏi tự kiểm tra 3 cho $0{,}2$.

## Kết luận

**đạt khi sửa** — không có phát hiện chặn hay nghiêm trọng; cần xử lý tám phát hiện trung bình (kí hiệu Bài 05 và (T1) chưa có nội dung trên mặt trang, bước nhảy ở 4-04, số $0{,}3810$ hai nghĩa, nhãn Bổ đề 06.8(c), công thức chính bị cắt ở 390 px, mật độ sát trần, dòng chia khối ở 6-05).

## Đề xuất sửa ghi chú

- §5 "Tối ưu trên một tập huấn luyện cố định" và tên mạch 2 của deck: "cố định" ở đây nghĩa là "lưu lại, dùng nhiều lần", trong khi mọi kết quả của §5 lấy kì vọng theo $S$. Đề xuất tác giả cân nhắc "tập huấn luyện lưu lại" (đã dùng ở §1 và deck 2-01) cho tiêu đề §5. Điểm này nối với mục đang mở cho tác giả trong `review-log.md` ("cố định" hai nghĩa ở Ví dụ 06.3).
