Phát hiện mới: chặn bàn giao 0 · nghiêm trọng 0 · trung bình 2 · nhẹ 8. Trạng thái 38 mục cũ: ✓ 36, một phần 2, ✗ 0. T1–T9: ✓ 9.

# Rà lại sư phạm và văn phong — Bài tập Bài 04 sau vòng sửa

Vai trò: người rà soát sư phạm–văn phong độc lập, chỉ đọc, `no-ai-slop` chế độ Detect. Dòng dẫn theo `lec04-ex-round1-frozen.md`. Đã đọc toàn bộ tệp đóng băng, `lec04-ex-round1.diff`, `lec04-note-exround.diff`, `reviews/11-quyet-dinh-bai-tap.md`, `bai-tap-ghi-chu.md` §7 và báo cáo trước của tôi (`10-bai-tap-su-pham.md`).

Kiểm tra máy đã chạy:
- Tệp đóng băng trùng từng byte với `2627-1/materials/lec-04/exercises.md`.
- 13 tên bài và 13 dòng mục tiêu khớp đúng §10 của ghi chú hiện tại (diff rỗng cả hai; 04.3 là "mục tiêu 3, 5" ở cả hai nơi).
- 0 "hãy", 0 "Đáp án", 0 "độ tin cậy", 0 `\text`. Tệp có 9 981 tiếng (`wc -w`, ngân sách 10 000).
- Còn ba câu trên 40 tiếng: dòng 10 (44, danh sách chữ viết tắt, chấp nhận), dòng 381 (43, danh sách thiết lập, chấp nhận) và dòng 623 (43, xem mục 11).

## 1. Trạng thái các mục cũ

### 1a. Mục của điều phối viên (T1–T9)

| Mục | Trạng thái | Căn cứ |
|---|---|---|
| T1 — 04.4(a) | ✓ | Dòng 383: họ 25 lớp mới, ghi rõ là giả định ("Giả sử họ được kéo dài", "rủi ro thực nghiệm giả định"). Dòng 407–423: duyệt lớp 1–18, dừng ở lớp 19, gọi bộ giải 18 lần, ô mới $\mathrm{pen}_{19}$. "Kiểm tra lại" (dòng 485) kiểm điều kiện dừng. Bảng lặp Ví dụ 04.9 đã bỏ. Còn một điểm nhẹ (N3). |
| T2 — 04.1(c) | ✓ | Dòng 35, 79–90: sáu hiệu mới, cặp $h_5$/$h_2$ cho $-0{,}04$; bỏ "ba lý do". |
| T3 — mục tiêu 2 | ✓ | Dòng 124, 251–257: 04.2(d), sai số xấp xỉ $0$, độ chệch $-0{,}2$, lý do "tính chất của lớp" và "tính chất của thuật toán". |
| T4 — mục tiêu 5 | ✓ theo quyết định | Dòng 284, 360–371: bước hỏng (Bước 3 của bổ đề), $0{,}0058$, vì sao không đủ. Phủ mục tiêu vẫn chỉ một phần (N2). |
| T5 — kí hiệu | ✓ | 04.13 dùng $k_{\max}$ (dòng 1009–1086); 04.9 dùng $k(h)$, $q_k$, $\mathcal H_k$ (dòng 743–810); 04.10 dùng $B_0$ (dòng 855); phần dẫn (dòng 7) nêu $k_{\max}$. |
| T6 — bước, danh sách | ✓ | 04.4(b) có bốn bước và hai khối `aligned` (dòng 425–447); đề 04.5(b) là danh sách bốn nhãn song song (dòng 497–502). |
| T7 — 04.3(d) | ✓ | Đề nêu hàm lỗi 0–1 (dòng 282); lời giải có Bước 1–4 và nêu phạm vi (dòng 358). |
| T8 — 04.11 | ✓ | Tên bài ghi "ý 3–5"; câu đầu của đề nêu cách lấy các ý (dòng 897); §10 của ghi chú sửa cùng. Còn hai điểm nhẹ (N5, N6). |
| T9 — 04.6 | ✓ | Dòng 620: bỏ "lỗi lập trình", có quy tắc chọn khi bằng nhau. Dòng 623: lý do là (T3), bỏ dẫn 04.4(d). |

### 1b. 38 mục của báo cáo trước

| # | Mức cũ | Mục | Trạng thái | Căn cứ |
|---|---|---|---|---|
| 1 | trung bình | 04.4(a) lặp Ví dụ 04.9 | ✓ | Như T1 |
| 2 | trung bình | 04.1(c) lặp Nhận xét 04.4 | ✓ | Như T2 |
| 3 | trung bình | 04.4(b) dồn đoạn | ✓ | Như T6. Bước 3–4 còn sơ lược (N4) |
| 4 | trung bình | Mục tiêu 2: độ chệch và sai số xấp xỉ | ✓ | 04.2(d) |
| 5 | trung bình | Mục tiêu 5: không chia xác suất thất bại | một phần | 04.3(e) tính $0{,}0058<\delta$: phân bố này không phải phản ví dụ; học viên không dựng phản ví dụ nào (N2) |
| 6 | trung bình | 04.13 $k$ thay cho $k_{\max}$ | ✓ | Như T5 |
| 7 | trung bình | Đề 04.5(b) | ✓ | Như T6 |
| 8 | nhẹ | 04.1(a) lặp ghi chú | ✓ | Dòng 31, 64: biến thể $1-\delta-\delta_2$ |
| 9 | nhẹ | Phần dẫn dòng 3, 7 dài | ✓ | Dòng 3–12: câu dẫn và danh sách bốn mục |
| 10 | nhẹ | 04.5(c) câu dài | ✓ | Dòng 513, 574 tách câu |
| 11 | nhẹ | 04.6 kết luận dài, lý do sai | một phần | Lý do đã đúng (dòng 623). Câu cuối còn 43 tiếng, nối bằng dấu chấm phẩy: thay "; quy tắc 2" bằng ". Quy tắc 2" |
| 12 | nhẹ | 04.6 hai mức nhiễu | ✓ | Dòng 586 |
| 13 | nhẹ | 04.6 danh sách không song song | ✓ | Dòng 590–592: ba dòng mở bằng "bậc …" |
| 14 | nhẹ | 04.6 "đường cong" | ✓ | Dòng 623: "Số liệu báo cáo" |
| 15 | nhẹ | 04.6 câu "cho thấy" | ✓ | Dòng 625 |
| 16 | nhẹ | 04.4(d) đề dồn ý | ✓ | Dòng 389–395: danh sách năm ý |
| 17 | nhẹ | 04.4(d) đuôi nhị thức; "(a)" mơ hồ | ✓ | Dòng 468, 472 |
| 18 | nhẹ | Tên 04.3 "số hạng tin cậy" | ✓ | Dòng 262 và §10 |
| 19 | nhẹ | 04.3(b)(c) "số hạng tương ứng", "họ lớp hữu hạn" | ✓ | Dòng 271, 273 |
| 20 | nhẹ | 04.3(c) "theo thứ tự ở (b)" | ✓ | Dòng 348: "theo đúng chiều của bảng ở (b)" |
| 21 | nhẹ | 04.3(d) dồn đoạn | ✓ | Dòng 352–358 |
| 22 | nhẹ | 04.8(b) dồn đoạn | ✓ | Dòng 727–733: ba bước |
| 23 | nhẹ | Gợi ý 04.8 | ✓ | Dòng 709–715: hai gợi ý tăng dần |
| 24 | nhẹ | Tên 04.8 phủ định chồng | ✓ | Dòng 697 và §10 |
| 25 | nhẹ | Tên 04.12 dễ đọc sai | ✓ | Dòng 954 và §10: "Thất bại của kiểm tra chéo để lại một quan sát" |
| 26 | nhẹ | Đề 04.2(b) | ✓ | Dòng 113 |
| 27 | nhẹ | 04.2(c) Bước 3 dạng văn xuôi | ✓ | Dòng 229–238: `aligned` |
| 28 | nhẹ | 04.7 hai tên bán kính; $\hat h_{(2)}$ chưa định nghĩa | ✓ | Dòng 639, 641 |
| 29 | nhẹ | 04.7(c) thiếu ô trung gian | ✓ | Dòng 683 |
| 30 | nhẹ | 04.9(b) "hàng $k=3$" | ✓ | Dòng 800 |
| 31 | nhẹ | 04.10 chữ $L$ | ✓ | Dòng 855 |
| 32 | nhẹ | 04.12 "Sai số" | ✓ | Dòng 979: "Độ lệch" |
| 33 | nhẹ | 04.13(c) dồn đoạn; "$k=119$" | ✓ | Dòng 1068–1084: danh sách và điểm đổi chiều $118$/$119$ |
| 34 | nhẹ | 04.5 $K$ đổi nghĩa | ✓ | $K_0$, $K=K_0^J$ (dòng 500, 542) |
| 35 | nhẹ | 04.5(c) $m'_v$ | ✓ | Dòng 576 |
| 36 | nhẹ | Cấu trúc $\mathbb 1_{F_+}$ lặp | ✓ | 04.5(a) dẫn thẳng Ví dụ 04.10 (dòng 527) |
| 37 | nhẹ | 04.11(a) "Ngược lại" | ✓ | Dòng 923 |
| 38 | nhẹ | Mục tiêu 4 mỏng | ✓ | Dòng 935: $M(\epsilon,\delta,h)$ không bị chặn trên $\mathcal H$, không có cỡ mẫu chung |

## 2. Phát hiện mới trong các đoạn đã sửa

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | Lời giải 04.4(c) Bước 1, dòng 451 | Lùi so với bản trước. Bảng ba cột ($k$, $\mathrm{pen}_k$, tổng) đã bị đổi thành một câu chứa công thức, tám số và một khoảng, trái §7a (yêu cầu của người dùng: không dồn nhiều phép tính vào một đoạn). | "… từ $0{,}0489$ ($k=1$) đến $0{,}1013$ ($k=10$). Tại $k=2,3,4,5$, $\mathrm{pen}_k$ là $0{,}0584$; …, và các tổng là $0{,}2684$; …; các tổng khác nằm trong $[0{,}2466;\,0{,}3489]$." Diff: các dòng `-| $1$ | $0{,}0489$ | $0{,}3489$ |` … đã bị xóa. | Khôi phục bảng ba cột (các hàng $k=1,\ldots,5$ và $10$, in đậm tổng tại $k=3$), giữ câu "các tổng tại $k=6,\ldots,9$ nằm trong …". Bảng không làm tăng số tiếng đáng kể. |
| trung bình | 04.3(e), dòng 284, 366–371 | Vế "dựng phản ví dụ … khi xác suất thất bại không được chia" của mục tiêu 5 mới đạt một phần. Phân bố của (e) cho $0{,}0058<\delta$, nên kết luận của bổ đề vẫn đúng ở đó. Học viên chỉ đọc lại con số $0{,}858$ của Ví dụ 04.8 mà không tự dựng phản ví dụ. | Bước 4: "$0{,}0058$ là của một phân bố, và chứng minh không còn cho cận $\delta$. Với $q_k=1$, cùng cấu trúc cho $0{,}858$ (Ví dụ 04.8)." | Thêm vào đề (e) một câu, chẳng hạn: "Với $q_k=1$ (không chia), tìm $k_{\max}$ nhỏ nhất để xác suất này vượt $\delta$." Lời giải: $1-(1-2^{-9})^{k_{\max}}>0{,}05$ khi và chỉ khi $k_{\max}>\ln0{,}95/\ln(1-2^{-9})\approx26{,}2$, nên $k_{\max}=27$ (xác suất $\approx0{,}0514$). Số này không có trong ghi chú. Câu này thay câu cuối của Bước 4 và thêm nói rõ "$0{,}0058<\delta$: phân bố này không bác bỏ kết luận". Bù số tiếng bằng cách bỏ "Kiểm tra lại" của 04.3 hoặc rút Bước 2 của (e). |
| nhẹ | 04.4(a), đề dòng 383; lời giải dòng 413 | "Đặc trưng dựng sẵn" không rõ nghĩa. $\mathrm{pen}_{18}\approx0{,}3599$ quyết định lớp 18 còn được duyệt, nhưng không có phép tính; chỉ $\mathrm{pen}_{19}$ có ô đầy đủ. | "(thêm $15$ đặc trưng dựng sẵn)"; "$\mathrm{pen}_{18}\approx0{,}3599<0{,}3650$" | Viết "thêm $15$ chỉ số giả định"; ghi một dòng cho $\mathrm{pen}_{18}$ ($a_{18}\approx151{,}22$, $b_{18}\approx10{,}660$, theo `bai-tap-ghi-chu.md`). |
| nhẹ | Lời giải 04.4(b) Bước 3–4, dòng 445, 447 | Bước 3 nêu hai cận dưới cho $k\ge5$ mà không có lý do. "Chúng" mơ hồ. Bước 4 đưa một lời giải thích ("trọng số chỉ đi vào qua $b_k$") làm lý do của lựa chọn, trong khi lý do là phép so các tổng. | "với $k\ge5$, chúng không nhỏ hơn $0{,}3875$ và $0{,}3896$"; "Cả hai dãy vẫn chọn $\hat k=3$, vì trọng số chỉ đi vào qua $b_k$" | Bước 3: "với $k\ge5$, tổng nhỏ nhất đạt tại $k=5$: $0{,}3875$ ($q_k=1/10$) và $0{,}3896$ ($q_k=2^{-k}$)". Bước 4: "Theo Bước 1–3, tổng nhỏ nhất ở $k=3$ với cả hai dãy. Trọng số chỉ đi vào qua $b_k$, nhỏ so với $a_k$." |
| nhẹ | Đề 04.11, dòng 897 | Câu đầu của đề là ghi chú nguồn của người soạn ("nên không lấy") và đứng trước thiết lập toán học. | "Ý 1–2 của UML Bài tập 7.5 là Định lý 04.16(a) (Phụ lục D của ghi chú) nên không lấy; (a)–(c) là ý 4; (d) gộp ý 3 và ý 5 …" | Đưa câu xuống cuối phần thiết lập và viết trung tính: "Các phần (a)–(c) là ý 4 của UML Bài tập 7.5; (d) gộp ý 3 và 5, phát biểu cho lớp các hàm phân lớp đo được. Ý 1–2 là Định lý 04.16(a), phác thảo ở Phụ lục D của ghi chú." |
| nhẹ | Tên 04.11, dòng 892 và §10 của ghi chú | Dấu phẩy giữa hai vị ngữ đọc như phép liệt kê, không như phép đối. | "Hợp nhiều khoảng: học được không đều, không học được PAC" | "… học được không đều nhưng không học được PAC". Ghi chú thêm một tiếng, nên phải bù một tiếng (thân ghi chú đang đúng $12\,000$), chẳng hạn bằng cách viết lại câu §7 như mục sau. |
| nhẹ | Ghi chú §7, câu cuối (dòng 910 của `lecture-note.md`) | Gán nhầm loại: một lớp hàm "là ý thử thách". | "Lớp mọi hàm phân lớp đo được trên miền vô hạn là ý thử thách của Bài tập 04.11." | Cùng số tiếng: "Ý thử thách của Bài tập 04.11 xét lớp mọi hàm phân lớp đo được trên miền vô hạn." |
| nhẹ | Đề 04.1(c), dòng 35 | Danh từ hóa (§9a). | "Xác định dấu của các hiệu và sự phụ thuộc của chúng vào nghiệm ERM được lấy làm mốc." | "Xác định dấu của các hiệu và cho biết mỗi hiệu đổi thế nào khi đổi nghiệm ERM làm mốc." |
| nhẹ | Lời giải 04.2(d) Bước 2, dòng 255 | Dùng ngầm $\mu=1$. Đề chỉ nói "thiết lập của (b)", và (b) có cả phần tổng quát lẫn phần số. | "độ chệch của $0{,}8\bar Y$ là $(0{,}8-1)\mu=-0{,}2$" | "… là $(0{,}8-1)\mu=-0{,}2$ với $\mu=1$ của (b)"; trong đề (d) ghi "với các số của (b)". |

Các điểm đã kiểm và đạt:
- **Lời giải từng bước.** Các đoạn mới 04.1(a) Bước 5, 04.2(d), 04.3(d)(e), 04.4(a), 04.5(b), 04.8(b), 04.13(c) đều tách bước có nhãn và hiển thị công thức.
- **Gợi ý tăng dần.** 04.3 (Gợi ý 2 cho (e)), 04.4 (gợi ý quy tắc dừng cho (a)), 04.8 và 04.12 đều đi từ hướng đi đến bước then chốt.
- **Danh sách song song.** Đạt ở 04.4(d), 04.5(b), 04.6(a) và 04.13(c) Bước 1.
- **Tên bài.** Tên của 04.3, 04.8, 04.12 là cụm danh từ hay phát biểu kết quả rõ nghĩa, khớp §10.
- **Lớp giả định của 04.4(a).** Được ghi rõ là giả định (hai lần, dòng 383).

## 3. Phủ mục tiêu học tập

| Mục tiêu | Bài tập | Đánh giá |
|---|---|---|
| 1. Phân tích sai số; cận ba thành phần; đẳng thức và cận | 04.1, 04.7 | Đủ; vế "đẳng thức và cận" được kiểm gián tiếp ở 04.1(b) (cận $0{,}5667$ so với giá trị thật $0{,}14$) |
| 2. Phân tích độ chệch–phương sai; nhãn kiểm tra độc lập; độ chệch khác sai số xấp xỉ | 04.2(a)–(d), 04.6 | Đủ cả ba vế; vế thứ ba ở 04.2(d) |
| 3. Chia xác suất thất bại; bất đẳng thức oracle; tính lựa chọn của SRM | 04.3, 04.4, 04.7, 04.8, 04.9, 04.10, 04.13 | Đủ |
| 4. Học không đều; so với học PAC bất khả tri; lớp học được không đều nhưng không học được PAC | 04.11 | Đủ; so sánh cỡ mẫu ở 04.11(c) Bước 2 |
| 5. Cận xác thực; điều kiện độc lập; phản ví dụ khi chọn sau khi xem dữ liệu hoặc khi không chia xác suất thất bại | 04.3(e), 04.5, 04.6, 04.12, 04.13 | Một phần: vế "không chia xác suất thất bại" có bước hỏng và một con số, chưa có phản ví dụ do học viên dựng (mục trung bình thứ hai) |

## 4. Kết luận

**Giao được.** Không có mục chặn bàn giao hay nghiêm trọng, cũ hay mới. Tên và mục tiêu của 13 bài khớp §10. Nên sửa hai mục trung bình trước khi công bố: khôi phục bảng ở 04.4(c) Bước 1, và thêm phép tìm $k_{\max}=27$ vào 04.3(e) để vế cuối của mục tiêu 5 có một phản ví dụ do học viên dựng. Ngân sách tiếng không cho phép thêm mà không bù (9 981/10 000; thân ghi chú 12 000/12 000).
