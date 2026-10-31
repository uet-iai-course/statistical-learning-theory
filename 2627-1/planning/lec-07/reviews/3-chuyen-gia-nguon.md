# Rà 3 — Chuyên gia lý thuyết học và trung thành nguồn — Bài 07 (bản đóng băng `lec07-draft-frozen.md`)

Người rà 3, chỉ đọc. Số dòng theo bản đóng băng.

## Tổng kết theo mức

| Mức | Số | Mã |
|---|---|---|
| chặn bàn giao | 0 | — |
| nghiêm trọng | 0 | — |
| trung bình | 1 | F1 |
| nhẹ | 8 | F2–F9 |

Đánh giá chung: chuẩn lý thuyết học đạt. Mọi phát biểu hình thức nêu cơ chế lấy mẫu, miền giá trị hàm lỗi, lớp cố định trước mẫu, loại bảo đảm (tất định / kì vọng / xác suất cao, cấp lớp). Ghi chú phân biệt rõ ba đối tượng của Định nghĩa 07.5 và phân biệt lớp điểm số với lớp hàm lỗi (Ví dụ 07.11), không chuyển cận tuyến tính sang mạng sâu (Nhận xét 07.18, §10), và trình bày thí nghiệm là bằng chứng. Phát biểu BFT ở Nhận xét 07.18 đúng từng thành phần so với BFT (1.1)–(1.2) và Định lý 1.1. Dẫn UML theo mục đều đúng, không dùng số định lý UML, khác biệt hằng số ở §13 viết trung tính và đúng. Mọi số của thí nghiệm tôi đã chạy lại bằng `exp_lec07_random_labels.py` (10 hạt giống) và đều khớp, chỉ lệch một chỗ làm tròn (F3). Không có khẳng định hay con số nào thiếu cơ sở.

## Bảng kiểm blueprint §E: 12/12 (mục 2 và 12 đạt, kèm lưu ý F1)

| # | Mục §E | Kết quả | Bằng chứng |
|---|---|---|---|
| 1 | Một bảng kí hiệu; không dùng $d$ cho hai nghĩa | đạt | $d$ = chiều VC, $p$ = số chiều đặc trưng; $C_x$, $J$, $\Theta_j$, $\varsigma$, $\sigma_i$ theo QĐ 3 (dòng 159, 957); lưu ý nhỏ về chữ $c$ ở F9 |
| 2 | Mỗi định lý nêu cơ chế lấy mẫu, hàm lỗi, đối tượng so sánh, nguồn ngẫu nhiên, loại bảo đảm | đạt (lưu ý F1) | Định lý 07.11 (dòng 508–531), Hệ quả 07.16 (708–726), Bổ đề 07.10, Mệnh đề 07.9/07.13 "tất định, kì vọng chỉ theo $\sigma$"; §1 mục 7 nêu đối tượng so sánh. Thí nghiệm nhãn hoán vị không thỏa (T1) đúng nghĩa, ghi chú chưa nói |
| 3 | Chú thích giả thiết trong chứng minh; ít nhất một ví dụ hỏng | đạt | các bước của 07.11 gắn (T1), $[0,1]$, (M); phản ví dụ: Ví dụ 07.6 (lớp kiến trúc), 07.11 (lớp điểm số thay lớp hàm lỗi), Nhận xét 07.17 (chọn $B$, $\gamma$ theo mẫu) |
| 4 | Kết quả là phát biểu của học phần; dẫn UML theo mục đã kiểm; không số định lý chưa kiểm | đạt | chỉ dẫn §20.3, §20.4, §20.5, §26.1–26.3, §15.2.3; số bài tập 20.1, 20.3, 20.4, 20.5 đã kiểm ở tr. 282 |
| 5 | Phân biệt bảo đảm cấp lớp và cấp thuật toán | đạt | Định nghĩa 07.5 và dòng 253, 531, 726, 888, 945 |
| 6 | Nói rõ đại lượng được chặn (rủi ro, rủi ro vượt mức, khoảng cách…) | đạt | 07.11: khoảng cách tổng quát hóa; 07.16: rủi ro 0–1; Ví dụ 07.9 Bước 5: rủi ro vượt mức của ERM |
| 7 | Không chuyển kết quả hàm lỗi bị chặn sang hàm lỗi bình phương/log khi chưa kiểm | đạt | Ví dụ 07.9 chuẩn hóa $\ell/4$ trên miền bị chặn; Ví dụ 07.11 Bước 4 cho hàm lỗi logistic |
| 8 | Không chuyển cận tối ưu lồi sang mạng nơ-ron | đạt | dòng 110, 894: "không dùng tính lồi"; §10 "Thuật toán", "Mạng sâu" |
| 9 | Một ví dụ số và một câu hỏi cuối buổi | đạt | Ví dụ 07.6, 07.8, 07.9; §12 (a)–(c) có lời giải |
| 10 | Tách bài gốc và bài UML; không bịa số bài UML | đạt | §11: 07.1–07.6 gốc, 07.7–07.9 = UML 20.3, 20.4, 20.1 (đã kiểm tr. 282) |
| 11 | Chứng minh dài để ở phụ lục | đạt | McDiarmid (A), bổ đề co (B), chi tiết 07.11 (C) |
| 12 | Minh họa thực nghiệm có mẫu kiểm tra độc lập, nhiều lần chạy, không coi là chứng minh | đạt (lưu ý F1, F2) | 5000 điểm kiểm tra, 10 hạt giống, độ lệch chuẩn, dòng 27, 847, 1088 |

## Đối chiếu blueprint (7.1–7.6, phần bổ sung)

- **7.1:** đủ. Bảng thay cho đường cong huấn luyện (QĐ phân tích nguồn 5). Có câu trả lời sai hấp dẫn (dòng 25) và đủ năm mục tiêu.
- **7.2:** đủ mọi định nghĩa: mạng lan truyền tới, độ sâu, độ rộng, hàm kích hoạt, hàm điểm số (Định nghĩa 07.1), lề (07.15), tham số hóa thừa so với mẫu (07.4), ba đối tượng (07.5), $\widehat{\mathfrak R}_S$ và $\mathfrak R_m$ (07.7). Câu "định lý áp dụng cho lớp hàm lỗi, không cho điểm số" có ở Ví dụ 07.11 và câu kết.
- **7.3:** đủ.
  - Mệnh đề 07.2 [F]: dùng $b_2=-\tfrac12$ và ngưỡng $0$, tương đương ngưỡng $\tfrac12$ của blueprint.
  - Định lý 07.11 [S]: dùng $\ln(2/\delta)$, đúng hằng số blueprint; bổ đề sai phân bị chặn ở phụ lục.
  - Mệnh đề 07.13 [F]: đủ hai bất đẳng thức.
  - Hệ quả 07.16 [S]: bổ đề co và quy ước định tâm phát biểu trước khi dùng (dòng 684).
  - Phần bổ sung: Nhận xét 07.18 [O].
- **7.4:** đủ ba ý.
  - Xấp xỉ phổ quát chỉ nói về sự tồn tại: Nhận xét 07.3.
  - Cận không cho thông tin không phải bằng chứng mô hình kém: Ví dụ 07.10(ii).
  - Đổi tỉ lệ hai lớp kề nhau: Ví dụ 07.2.
- **7.5–7.6:** §11 liệt kê đủ sáu bài gốc. Phần đọc bắt buộc (§20.1–20.5, §26.1–26.2) được chia hai mốc trước và sau buổi học; §26.3 và BFT ở phần mở rộng. Cầu nối (dòng 945) khớp với đầu Bài 08 (số bước, quỹ đạo SGD). Các sai khác đều nằm trong danh sách đã chấp nhận (`outline.md` §13.2, review-log).

## Lời hứa

| Lời hứa | Kết quả |
|---|---|
| Bài 03 dòng 868 (độ phức tạp Rademacher, Bài 07) | giữ: §6–§7 |
| Bài 03 dòng 921 (UML §28.1 "chuẩn bị Bài 07") | giữ một phần: dàn ý ghi "giữ ở §13", nhưng §13 không nhắc §28.1 (F8) |
| Bài 05 dòng 1100 (cận thống kê cho hàm lỗi lồi Lipschitz, Bài 06–07) | giữ cho hàm lỗi bình phương (Ví dụ 07.9). Hàm lỗi logistic chỉ được nêu hướng (Ví dụ 07.11 Bước 4), chưa có cận (F7) |
| Bài 06 dòng 854 (hội tụ đều cho Ví dụ 06.7, "chứng minh ở Bài 07") | giữ đúng nguyên văn ($\mathcal Z=[-1,1]^2$, $W=[-1,1]$): Ví dụ 07.9, số tính lại đúng ($0{,}8147$; $0{,}2576$; $0{,}0815$; $66\,371$) |
| Cầu nối cuối Bài 06 (dòng 1130: nhãn ngẫu nhiên, đại lượng còn cho thông tin) | giữ: câu hỏi mở đầu, Ví dụ 07.5, 07.10 |

## Trang nguồn đã đọc

- **UML (trang PDF):**
  - 210: §15.2.3, hàm lỗi dốc.
  - 269–277: §20.1–20.5 và đầu §20.6, gồm Claim 20.1 (tr. 271), Thm 20.2–20.3 (tr. 272), Lemma 20.4 và Thm 20.5 (tr. 273), Thm 20.6 (tr. 274–275), Thm 20.7 (tr. 276).
  - 282: §20.9, Bài tập 20.1–20.5.
  - 375–385: §26.1 với Def 26.1, (26.4)–(26.5), Lemma 26.2, Thm 26.3, Lemma 26.4, Thm 26.5, Lemma 26.6, Lemma 26.9; §26.2 với Lemma 26.10–26.11; §26.3 với Thm 26.12–26.14.
- **BFT (arXiv:1706.08498v2):**
  - tr. 1–3: tóm tắt, §1.1, (1.1)–(1.2), Định lý 1.1.
  - tr. 6–8: Lemma 3.1, Lemma 3.2, Thm 3.3, Dudley, Thm 3.4, §3.4.
- **Bài trước:** Bài 03 dòng 866–869 và 919–922; Bài 05 dòng 1098–1101 và Mệnh đề 05.5; Bài 06 Ví dụ 06.7 (dòng 838–855) và dòng 1130; Bài 02 Nhận xét 02.11.
- **Thí nghiệm:** đã chạy lại `../tools/courses/statistical-learning-theory/2627-1/scripts/exp_lec07_random_labels.py` (không ghi tệp).

## Phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | F1 · Câu hỏi mở đầu (dòng 14), Ví dụ 07.6 Bước 2 (dòng 586), Ví dụ 07.10 Bước 3–4, §10 (dòng 892), Phụ lục D (dòng 1082) | Cơ chế lấy mẫu của trường hợp nhãn hoán vị không thỏa (T1). Hoán vị nhãn cho các cặp $(x_i,y_{\pi(i)})$ có thể hoán đổi nhưng không độc lập: tổng các nhãn cố định, và không có phân bố $D$ nào cho mẫu đó là $D^m$. Ghi chú vẫn tính vế phải của Định lý 07.11 và Hệ quả 07.16 "như nhau cho nhãn thật và nhãn hoán vị" mà không nêu điểm này. Không có kết luận sai, vì vế phải lớn hơn 1, nhưng §E mục 2 đòi nêu rõ cơ chế lấy mẫu. | Định lý 07.11 giả thiết $S\sim D^m$ theo (T1) (dòng 510); Phụ lục D: "Một hoán vị đều của $200$ nhãn huấn luyện" | Thêm vào Phụ lục D, mục "Nhãn hoán vị", một câu (khoảng 45 tiếng, tính vào ngân sách phụ lục 1634/3000, không vào thân bài): "Với nhãn hoán vị, các cặp $(x_i,y_i)$ không độc lập (tổng các nhãn cố định), nên (T1) không đúng; các số của Ví dụ 07.6 và 07.10 cho trường hợp này là giá trị của vế phải, không phải cận đã chứng minh. Nhãn ngẫu nhiên độc lập với $x$, như các $\tau_i$ của Mệnh đề 07.9, thỏa (T1) và cho cùng hiện tượng." |
| nhẹ | F2 · Ví dụ 07.10 Bước 4(iii), dòng 845 | Câu "Hàm đã chọn cố định trước khi rút $5000$ điểm kiểm tra" trái với thứ tự rút ở Phụ lục D (điểm kiểm tra được rút thứ hai, trước lớp ẩn). Điều Hệ quả 02.10(b) cần là tính độc lập, không phải thứ tự thời gian. | Phụ lục D, dòng 1085: "điểm huấn luyện, điểm kiểm tra, lớp ẩn …" | Sửa thành "Hàm đã chọn chỉ phụ thuộc mẫu huấn luyện và lớp ẩn, độc lập với $5000$ điểm kiểm tra, nên …" (+3 tiếng; bù bằng các chỗ cắt ở cuối bảng) |
| nhẹ | F3 · Ví dụ 07.10 Bước 2, dòng 834 | Đầu dưới của khoảng chuẩn ghi "$352$". Script cho $351{,}478$, làm tròn thành $351$. Đầu dưới của một khoảng không nên làm tròn lên. | Lần chạy lại: `chuan_w … min 351.478`; `outline.md` §13.1: "$351{,}48$" | "từ $351$ đến $1721$" (không đổi số tiếng) |
| nhẹ | F4 · Nhận xét 07.18, dòng 885 | Câu "Vì $\lVert X\rVert_2/m\le C_x/\sqrt m$" cần thêm giả thiết $\lVert x_i\rVert\le C_x$. BFT Định lý 1.1 không có giả thiết này: cận phụ thuộc trực tiếp vào $\lVert X\rVert_2$. | BFT tr. 3, Định lý 1.1: "$\lVert X\rVert_2=\sqrt{\sum_i\lVert x_i\rVert_2^2}$", không có giả thiết chặn dữ liệu | "Khi $\lVert x_i\rVert\le C_x$, ta có $\lVert X\rVert_2/m\le C_x/\sqrt m$, nên …" (+3 tiếng) |
| nhẹ | F5 · Nhận xét 07.18, dòng 885 | "Với $M_j=0$, $R_\Theta$ không đổi khi đổi tỉ lệ như Ví dụ 07.2". Mạng của Ví dụ 07.2 có hệ số tự do, còn mạng của BFT thì không, nên $R_\Theta$ không áp dụng trực tiếp cho mạng phép hoặc loại trừ. Phép đổi tỉ lệ $(c\Theta_j,\Theta_{j+1}/c)$ giữ $R_\Theta$ chỉ với hàm kích hoạt thuần nhất dương như ReLU. | BFT (1.1): "$F_A(x):=\sigma_L(A_L\cdots\sigma_1(A_1x))$", không hệ số tự do; Ví dụ 07.2 có $b_1$, $b_2$ | "Với ReLU và $M_j=0$, $R_\Theta$ không đổi khi đổi tỉ lệ hai lớp kề nhau như Bước 2 của Ví dụ 07.2." (+6 tiếng) |
| nhẹ | F6 · Nhận xét 07.3, dòng 219 | Câu xấp xỉ phổ quát không nêu hàm kích hoạt. UML §20.3 và Bài tập 20.1 phát biểu cho sigmoid, còn Bài tập 07.9 đã sửa sang ReLU với $p=1$. Người đọc có thể hiểu UML phát biểu cho mọi hàm kích hoạt. | UML tr. 273 ("In Exercise 1 …"), tr. 282, Bài tập 20.1: "with the sigmoid activation function" | "… bởi một mạng sigmoid nào đó (UML §20.3; Bài tập 07.9 cho ReLU và $p=1$)" (+2 tiếng) |
| nhẹ | F7 · Ví dụ 07.11 Bước 4, dòng 859 (lời hứa Bài 05 dòng 1100) | Hàm lỗi logistic, hàm lỗi lồi Lipschitz mà Bài 05 nhắc, mới được chỉ hướng ("phải được chia cho hằng số này"), chưa có cận. Cận chỉ cần một dòng. | Bài 05 dòng 1100: "cận thống kê cho hàm lỗi lồi và Lipschitz thuộc Bài 06–07"; hàm lỗi logistic là $1$-Lipschitz theo điểm số | Nối vào cuối Bước 4: "; bổ đề co và Mệnh đề 07.13 khi đó cho $L_D\le L_S+2BC_x/\sqrt m+3\ln(1+e^{BC_x})\sqrt{\ln(2/\delta)/(2m)}$." (khoảng +14 tiếng). Tôi đã dẫn lại: chia cho $K=\ln(1+e^{BC_x})$, mỗi $\phi_i$ là $(1/K)$-Lipschitz, $\widehat{\mathfrak R}\le BC_x/(K\sqrt m)$, rồi nhân lại với $K$ |
| nhẹ | F8 · §13 Tài liệu đọc, dòng 951 (lời hứa Bài 03 dòng 921) | Bài 03 giới thiệu UML §28.1 là "chuẩn bị Bài 07", và `outline.md` dòng 493 ghi "giữ ở §6 câu mở và §13". §13 không nhắc §28.1. | `outline.md` dòng 493; bản đóng băng dòng 949–951 | Thêm vào "Mở rộng": "UML §28.1 (cận hội tụ đều cho lớp nhị phân qua độ phức tạp Rademacher)" (+10 tiếng) |
| nhẹ | F9 · Câu hỏi mở đầu, dòng 9 | Hệ số tự do của nơ-ron ẩn viết $c$ ("$\max\{0,\langle v,x\rangle+c\}$"), nhưng từ dòng 295 lại là $b_{1j}$; $c$ còn là hằng số đổi tỉ lệ (Ví dụ 07.2) và hệ số của Bổ đề 07.8 (§E mục 1). | dòng 9, 258, 295, 357 | Viết "$\max\{0,\langle v,x\rangle+b\}$ với $v$, $b$ riêng" (không đổi số tiếng) |

**Ngân sách thân bài (11 999/12 000 tiếng).** Các chỗ thêm trong thân bài là F2 (+3), F4 (+3), F5 (+6), F6 (+2), F7 (+14) và F8 (+10), tổng khoảng 38 tiếng. F1 nằm ở phụ lục; F3 và F9 không đổi số tiếng. Đề xuất cắt khoảng 45 tiếng, toàn câu lặp ý:

1. Dòng 888, câu đầu: "Trong các ví dụ trên, chuẩn và lề cho thông tin mà số tham số không cho." (17 tiếng). §10 nói lại ý này.
2. Dòng 138, câu đầu: "Lớp nửa không gian afin không phân lớp đúng mẫu của Ví dụ 07.1." (14 tiếng). Ý này trùng dòng 134 ngay trước tiêu đề §4.
3. Dòng 652, vế sau dấu chấm phẩy: "; với lớp nửa không gian, chiều VC bằng $p$ hay $p+1$ (Mệnh đề 03.9)" (khoảng 14 tiếng). Dòng 622 và ứng dụng đã nói cận không phụ thuộc $p$.
