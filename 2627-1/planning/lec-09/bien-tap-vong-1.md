# Biên tập vòng 1 — Bài 09 (2026-10-31)

Biên tập viên: người viết ghi chú (general-purpose, opus, high; giao bằng `SendMessage`). Căn cứ: `reviews/0-quyet-dinh.md` (ưu tiên), năm báo cáo `reviews/1-…5-*.md`. Số dòng trong bảng là số dòng của bản đóng băng `lec09-draft-frozen.md`.

**Số tiếng (`wc -w`).** Trước: thân 11 984, phụ lục 1 580, 987 dòng. Sau: thân 11 997, phụ lục 2 036, 1 019 dòng.

**Kiểm tra sau sửa.** `forward_refs.py` 0; khối `:::` 38/38; sync `--check` OK; `git diff --check -- 2627-1/materials/lec-09` sạch, không có khoảng trắng cuối dòng (grep); viewer qua HTTP (cổng 8779, đã tắt) và `file://` ở 1600×900 và 390×844, 9 `details` mở: 1462 công thức, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức hay bảng tràn, chiều rộng tài liệu 375 px ở 390.

## Chỗ cắt và chuyển để bù chữ

- **Chuyển sang phụ lục.** Chứng minh Mệnh đề 09.3 và chứng minh Hệ quả 09.13 chuyển sang Phụ lục D mới ("Chứng minh Mệnh đề 09.3 và Hệ quả 09.13"). Tiêu đề hai khối ghi "chứng minh đầy đủ (Phụ lục D)". Thân bài giữ câu ý nghĩa của từng chứng minh, và câu cho biết chứng minh dùng gì. Mỗi chứng minh trong phụ lục kết bằng $\square$ và một câu ý nghĩa. Tiết kiệm khoảng 430 tiếng thân bài.
- **Cắt trong thân bài.** Câu kết §3 (−24); câu tóm tắt dòng 105 (−27); mục "Quan sát độc lập" của Định nghĩa 09.1, gộp vào đoạn sau định nghĩa; các ô §7–§9 của bảng §1; câu hỏi lặp dòng 30 (−11); vế "Tên gọi đến từ định lý dưới đây" (−8); câu "Ngược lại, $v=\mathbb 1[u<\phi]$ …" sau Định nghĩa 09.14 (−35); câu "bộ mã hóa xác suất" ở §10 (−25); Kết luận Ví dụ 09.3 rút gọn (−25); câu thứ hai Kết luận Ví dụ 09.7 (−25); giới hạn đầu ở §10 rút gọn; câu "Câu ôn nhanh 3 là …" ở §8; "(đơn vị của logarit tự nhiên)".

## Bảng phát hiện

| Mã / người rà | Dòng (bản đóng băng) | Cách sửa hoặc không áp dụng + lý do |
|---|---|---|
| N1 / R3 | 806 | Thay bằng: "GAN và mô hình khuếch tán là các mô hình sinh khác; mục tiêu huấn luyện và cách đánh giá chúng nằm ngoài phạm vi bài." |
| N2 / R1, R5 R2, R4 T6 | 860 | Viết lại: dữ liệu từ $D$ cố định, không phụ thuộc tham số; trong mục tiêu huấn luyện, phân bố lấy kì vọng duy nhất phụ thuộc tham số đang tối ưu là $q_\phi$, và thuật toán học chọn nó. Thêm "Câu hỏi cho Bài 10 là:", tách thành hai câu hỏi, không phát biểu kết quả Bài 10. |
| N3 / R1, R4 N3 | 100–103 | Bảng chỉ còn đối tượng của §1: "Cố định, chọn trước", "Ngẫu nhiên theo dữ liệu", "Tất định" ($L_D(\theta)$). Bỏ cụm "phân bố xấp xỉ" ở mọi chỗ, dòng 527 thành "phân bố biến phân". |
| TB1 / R2 | 439 | Câu sau $\square$ của Hệ quả 09.9: "khi lớp không chứa $p_D$, mô hình bị đặc tả sai; nếu thêm $\inf_\Theta\mathrm{KL}>0$, phần chênh này còn lại …". |
| TB2 / R2, R3 | 324–333 | Định nghĩa 09.6: $n(x)$ là số kí tự trước $\mathtt E$, đặt $x_{n(x)+1}=\mathtt E$, tổng chạy đến $n(x)+1$ và gồm số hạng của $\mathtt E$. Ví dụ 09.6: xác suất của $\mathtt E$ có tham số riêng, không phụ thuộc $\theta$, nên số hạng của nó là hằng trong cả hai mục tiêu. |
| TB3 / R3, R2 | 673, 711–718, 726, 793 | §9 mở: gradient nói chung khác $\mathbb E_{q_\phi}\nabla_\phi f$ (bằng $0$), nên có hai cách (gradient log, tái tham số hóa). Định nghĩa $\kappa_i(\theta,\phi,\zeta)=\ln\big(q_\phi/p_\theta\big)$; tính không chệch nói rõ "nếu $\kappa_i$ thỏa (i)–(iii) với $(\theta,\phi)$ ở chỗ của $\phi$". Mục "Hàm" của Mệnh đề 09.15: "$\phi$ gồm mọi tham số cần lấy gradient". Câu sau $\square$ và §10 kèm điều kiện. |
| TB4 / R3 | 870, 451, 793, 669, 795 | §13 thêm $L(S;\theta)=-m\,L_S(\theta)$; Ví dụ 09.7 dẫn "theo ý của UML §24.1.3"; câu bộ mã hóa §2.2 cắt; SGD dẫn §2.1–§2.3; §10 tách bảo đảm cho mô hình cố định (Ví dụ 09.4) với bảo đảm cho ước lượng (Bài tập 09.9). Thêm "(UML §24.4.1)" ở đoạn EM; §13 thêm "giả sử các mật độ khả vi hầu khắp nơi (§2.1)". |
| TB5 / R1, R4, R5 | 77, 366, 405, 394, 396, 444, 461, 860, 162, 342, 368 | Bỏ "Thiết lập A" ở dòng 77; "chuỗi" (series) thành "tổng"; "chuỗi bất đẳng thức" thành "dãy bất đẳng thức"; Định nghĩa 09.7 thêm mục "**Giá.** *Giá* (support)"; Bước 1 Mệnh đề 09.8 và tên Ví dụ 09.7 thành "… bằng $0$ … trên giá của $p_D$"; "giá" (cái giá) ở Ví dụ 09.8 bỏ; "dừng" chỉ còn nghĩa điểm dừng ("chuỗi kết thúc"; bỏ "phân bố dừng"); "người học" chỉ ở mục tiêu học tập; KL mở thành "(Kullback–Leibler divergence, KL)" và nhãn "Phân kì Kullback–Leibler (KL)"; quan sát của mẫu viết $x^{(i)}$ (Định nghĩa 09.2, Định lý 09.12(d), Hệ quả 09.13, đoạn gradient ngẫu nhiên); bỏ $\theta^*$ ở Ví dụ 09.6; $\mathrm{Ber}(\theta)$ định nghĩa ở Ví dụ 09.2; mẫu kiểm tra "chỉ dùng ở §6 và trong thí nghiệm". |
| TB6 / R1, R4 T4–T5 | 180, 253, 292, 442, 447, 451, 453, 464, 742, 784, 310–316, 459–461, 485 | Thêm phép thay số: $L_s(0{,}7)$; ba số hạng của $\ell$ ở Ví dụ 09.3; bán kính $0{,}0407$; khoảng cách $0{,}6956-0{,}6109$; $L_D(0{,}1)$; $L_D(\hat\theta)=0{,}0192+0{,}0395$; $\mathrm H(p_D)\approx218{,}08$; $\operatorname{Var}(2\zeta-\zeta^2)$ trong `aligned`; xác suất lớn nhất $\tfrac14\cdot0{,}6^{199}$. Ví dụ 09.7 Bước 3–4 tách bốn và ba đoạn. Ví dụ 09.7, 09.12, 09.13: Thiết lập nêu rõ thiết lập của từng nhóm bước, thêm "$S$ và $\hat\theta$ là ngẫu nhiên". Ví dụ 09.5 Bước 4 thêm "hàm dự đoán của Bước 1 chỉ khai thác rò rỉ qua $u_{j+1}$". Ví dụ 09.8: thiết lập ghi $0{,}6$, $0{,}2$, $0{,}1$, $0{,}1$; Bước 1 dùng "entropy của hàng ứng với $x_{j-1}$", không dùng phân bố dừng; (i) trả lời khoảng cách tới giá trị tốt nhất ($0{,}0009$) và tới mô hình thật ($0{,}0007$), trung bình 10 lần chạy. |
| TB7 / R4 T1, R5 R10 | 152, 189, 351, 488, 789 | §3: cắt. §4: câu về hàm lỗi $+\infty$. §6: hai câu về Thiết lập B và mục tiêu theo độ dài. §7: bỏ vế lặp. §9: điều kiện (i)–(iii) và hai tiêu chí báo cáo riêng. |
| TB8 / R4 T7 | 606–631 | Giữ hai bảng; câu dẫn nói cột KL là KL tới tiên nghiệm và ELBO bằng tái tạo trừ KL; Bước 3 "trùng cột khe của bảng thứ hai". **Không áp dụng nguyên văn** tiêu đề "KL tới tiên nghiệm" và "khe $=\ln p-\mathrm{ELBO}$" trong ô tiêu đề: đã đo, bảng rộng 273 px với chỗ 271 px ở 390 px. Nghĩa của cột được nói trong câu dẫn. |
| TB9 / R2 | 312, 483, 278, 453 | $0{,}245$ (ghi $0{,}200$ và $0{,}994$ ba chữ số theo Phụ lục C); "khoảng $0{,}032$"; $[0,\ln20]$ với $\ln20\approx2{,}9957$; $\ell\le\ln52<3{,}952$. |
| Nhẹ / R4 T6 | 3 | Đoạn mở không còn "Bài 08 kết thúc bằng câu hỏi"; độ hợp lý định nghĩa riêng một câu; dẫn "(câu hỏi cuối Bài 08)". |
| Nhẹ / R4 N18 | 590, 633, 638, 669, 673 | "cực đại hóa", "tối thiểu hóa" cho động từ. |
| Nhẹ / R4 N5 | 32, 81, 82, 193, 238, 273, 442, 928 | Bỏ chủ ngữ là văn bản hay kết quả ("ở §7, ta tách", "tính ở §7", "theo §6", "Theo Mệnh đề 09.3, …", "Hệ quả 09.9 chỉ áp dụng …"; câu "Phụ lục này chứng minh" cắt). |
| Nhẹ / R4 N7 | 5, 147, 233, 235, 302, 312, 439, 544 | "mạng nơ-ron hồi tiếp (recurrent neural network)"; "(bigram model, còn gọi là mô hình Markov bậc một)"; *học theo đáp án* (teacher forcing) định nghĩa đúng dạng; "cỡ mẫu trong cận"; "(mean squared error, MSE)"; *đặc tả sai* đưa ra ngoài ngoặc; "còn gọi là cận dưới biến phân" vào Định nghĩa 09.11; "khe (gap)". |
| Nhẹ / R4 N9, N10 | 348, 483, 485, 758; 32, 156, 226, 481, 633, 635 | Bỏ dấu hai chấm tiết lộ; câu "kết quả thí nghiệm, không phải chứng minh" chỉ còn một lần (Phụ lục C); "chấm" thành "đánh giá"; "tự động chuẩn hóa" thành "là hàm xác suất, không cần chuẩn hóa thêm"; "Điểm dừng trùng với hậu nghiệm"; "trả một KL" viết lại. |
| Nhẹ / R4 N12 | 534–540, 712–717 | Định nghĩa 09.11 và gradient ngẫu nhiên viết dạng $\ln\frac{\cdot}{\cdot}$, không gãy giữa ngoặc vuông. |
| Nhẹ / R4 N24 | 765, 782, 786, 801 | "mẫu sinh" thành "điểm/chuỗi/dữ liệu sinh ra"; tên Ví dụ 09.13 thành "Độ hợp lý và chất lượng dữ liệu sinh ra theo hai chiều". |
| Nhẹ / R4 N2, N4, N8, N11, N14–N17, N19–N23, N25 | nhiều dòng | Áp dụng như đề xuất. Riêng N17 (câu $\square$ của Hệ quả 09.13) thì chứng minh đã chuyển về Phụ lục D, câu kết mới nói bước M chỉ cần làm tăng tổng. |
| Nhẹ / R4 N13 | 11, 32, 94, 238, 481, 793, 872 | Đã tách các câu 94, 238, 481, 793, 872. **Không áp dụng** ở dòng 11: câu dưới 45 tiếng, tách sẽ tốn chữ. |
| Nhẹ / R4 N6 | 156, 355, 530, 673 | "chúng ta" cho nhu cầu và kế hoạch. |
| Nhẹ / R2 | 950, 940 | Phụ lục B: liên tục tại $\phi_0$, rồi trên $\Phi$ vì $\phi_0$ tùy ý; hợp các tập ngoại lệ là khoảng đối. |
| Nhẹ / R2, R3 | 122 | Điều kiện đủ: hàm lỗi bị chặn, chẳng hạn mô hình rời rạc bị chặn dưới bởi $c>0$; với mật độ cần chặn cả trên lẫn dưới. Câu về Định nghĩa 01.1, (T2), (T3) viết lại theo R5 R13. |
| Nhẹ / R3 | 238, 485, 873 | "có thể khác … khi $p_\theta\ne p_D$"; (iii) thêm "với mô hình làm trơn, có xác suất bị chặn dưới"; khác biệt khả vi hầu khắp nơi ghi trung tính. |
| Nhẹ / R3 | 492 | **Không áp dụng** (tùy chọn): câu hiện tại dẫn đúng §2.1, và sửa sẽ tốn chữ. |
| Nhẹ / R5 R5 | 461, 970 | **Không áp dụng** thêm "phân bố dừng" vào tiên quyết. Bước 1 Ví dụ 09.8 không còn dùng thuật ngữ này, theo cách sửa của R1; Phụ lục C viết "mọi kí tự có phân bố đều". |
| Nhẹ / R5 R11 | 122 | **Không áp dụng** (tùy chọn, +25 tiếng), vì ngân sách thân bài đã hết. |
| Nhẹ / R5 R17 | 485 | **Không áp dụng** (tùy chọn, +15 tiếng), cùng lý do ngân sách. |
| Nhẹ / R5 R9 | 193, 238 | Thêm: với ngữ cảnh bậc $1$, mô hình trên chuỗi DNA có $15$ tham số tự do thay cho $4^{200}-1$. |
| Nhẹ / R5 R12 | 504, 684, 760 | $\phi$ khác các ánh xạ $\phi$, $\phi_i$, $\phi_\gamma$ của bổ đề co; biến đều đổi thành $U_0$ (Ví dụ 09.12, câu hỏi cuối buổi (d)). |
| Nhẹ / R5 R14 | 586 | Bước 4 Định lý 09.12 dẫn Mệnh đề 09.8(c) (Bước 3–4). |
| Nhẹ / R1 | 833, 744, 504, 139, 985 | Câu (d) nêu tái tham số hóa $v=\mathbb 1[U_0<\phi]$; Ví dụ 09.11 kiểm (iii); khối lượng điểm (point mass); $1-0{,}58=0{,}42$; "cả mười hạt giống, hai phần". |

## Ghi chú

- Phụ lục C thêm câu "Các số của Ví dụ 09.5 và 09.8 là bằng chứng thí nghiệm cho một thiết lập, không phải chứng minh", vì ở thân bài câu này đã bị cắt.
- Không đổi số liệu thí nghiệm hay script. Số mới tính lại trong scratchpad `writer09/`: $L_D(\hat\theta)=0{,}019224+0{,}039512$; $\mathrm H(p_D)=218{,}085$; chênh lệch $0{,}00091$ và $0{,}00073$ (theo `2-toan-hoc.md`).
- Đề nghị điều phối viên thêm vào `thuat-ngu.md` §11: "mạng nơ-ron hồi tiếp (recurrent neural network)", "khe (gap)", "khối lượng điểm (point mass)", "dữ liệu sinh ra (generated samples)", "hàm trội (dominating function)".

## Vòng 2 (2026-10-31)

Căn cứ: `reviews/6-ra-lai-toan.md` (4 điểm nhẹ), `reviews/7-ra-lai-mach.md` (M1–M10), mục "Rà lại sau vòng 1" của `review-log.md`. Số dòng trong bảng theo bản sau vòng 1. Thân bài từ 11 997 lên 12 000 tiếng (vừa đúng trần), phụ lục từ 2 036 lên 2 061, tệp 1 017 dòng.

| Mã | Dòng | Cách sửa |
|---|---|---|
| R6-1 | 851 | "…là phân bố biến phân ($q_\phi$ hoặc $q_i$), và thuật toán học chọn nó." |
| R6-2 | 303 | Định nghĩa 09.6: "$n(x)\ge1$ kí tự trước $\mathtt E$". |
| R6-3, M10 | 1005, 1018 | Bước 1 của Hệ quả 09.13: tính hữu hạn suy từ $\sum_i\mathbb E_{q_i}\ln p_{\theta_{t+1}}\ge\sum_i\mathbb E_{q_i}\ln p_{\theta_t}>-\infty$ và $\mathcal V$ hữu hạn. Câu sau $\square$: bước M chỉ cần "không làm giảm" tổng. |
| R6-4 | 458 | Ví dụ 09.8 Bước 1: kì vọng có điều kiện khi biết $x_{j-1}$; mọi hàng cùng entropy nên kì vọng bằng $1{,}0889$. |
| M1 | 959 | "kết quả thí nghiệm" thay "bằng chứng thí nghiệm". |
| M2 | 84–101 | Câu dẫn và bảng nguồn ngẫu nhiên chuyển lên trước "Dữ liệu chuỗi có hai cách lấy mẫu."; bỏ $k$ khỏi bảng; §1 kết bằng đoạn văn sau Định nghĩa 09.1. |
| M3 | 337 | Câu kết §6 thêm "Trong Thiết lập A, các cận dùng số chuỗi $m$". |
| M4 | 486 | Câu kết §7 rút còn "Mô hình gán xác suất $0$ trên giá của $p_D$ có rủi ro $+\infty$." |
| M5 | 452 | "…; hàm lỗi log là một hàm lỗi không bị chặn như ở Nhận xét 02.11." |
| M6 | 780 | "…; với biến ẩn rời rạc, (i) không thỏa (Ví dụ 09.12)." |
| M7 | 775 | Tách câu ("Do đó …"). |
| M8 | 502 | Thêm "Câu ôn nhanh 3 là một mô hình biến ẩn với $\mathcal V=\{1,2\}$." |
| M9 | 145 | Đảo "trên chuỗi mới" lên trước. |
| Hình thức | 204–205, 650–651 | Xóa dòng trống kép. |

**Cắt bù:** câu ở dòng 649 bỏ "tại $\theta_{t+1}$ và tại $\theta_t$, nơi $q_i$ là hậu nghiệm"; dòng 183 rút gọn; giới hạn "Tối ưu không lồi" rút gọn; câu cuối Bước 3 của Ví dụ 09.12 rút còn "khả vi tại từng $\mu$ hầu chắc chắn chưa đủ"; "chênh lệch này" thành "đây".

**Kiểm tra:** `forward_refs.py` 0; khối `:::` 38/38; sync `--check` OK; `git diff --check` sạch, không có khoảng trắng cuối dòng; viewer qua HTTP (cổng 8779, đã tắt) và `file://` ở 1600×900 và 390×844: 1466 công thức, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 tràn.
