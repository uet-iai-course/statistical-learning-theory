# Rà 3 — Chuyên gia lý thuyết học và trung thành nguồn — Bài 09 (bản đóng băng `lec09-draft-frozen.md`)

Người rà: tác tử rà 3 (chỉ đọc repo, không commit). Số dòng theo bản đóng băng.

## Tổng kết theo mức

- **chặn bàn giao:** 0
- **nghiêm trọng:** 1 — câu về GAN và mô hình khuếch tán (dòng 806) thêm khẳng định không có cơ sở và không đúng với mô hình khuếch tán; trái QĐ dàn ý (5).
- **trung bình:** 5 — §10 khẳng định gradient tái tham số hóa không chệch mà bỏ điều kiện (dòng 793); thiếu sai khác về dấu của log độ hợp lý trong UML (dòng 870); ý của Ví dụ 09.7 Bước 3 lấy từ UML §24.1.3 mà không dẫn; §10 gộp bảo đảm cho một mô hình cố định với bảo đảm cho một thuật toán (dòng 795); "dưới các điều kiện trên" cho gradient ngẫu nhiên của $-\mathrm{ELBO}$ (dòng 718) chưa nói điều kiện áp lên hàm nào.
- **nhẹ:** 9 (dẫn sai mục Kingma–Welling hai chỗ; câu "xác suất theo mẫu chỉ ở §6"; điều kiện bị chặn với mật độ; "khác" ở học theo đáp án; câu cầu nối "phân bố duy nhất phụ thuộc tham số"; ghi rõ giả thiết khả vi hầu khắp nơi của KW; dẫn UML ở đoạn EM; Kết luận (iii) Ví dụ 09.8).

Nhìn chung, phần lõi lý thuyết đúng và đủ độ sâu: năm kết quả blueprint có mặt với đúng mức chứng minh; đồng nhất thức và kết quả tổng thể được tách khỏi bảo đảm mẫu hữu hạn; không cận nào cho hàm lỗi bị chặn được chuyển sang hàm lỗi log mà thiếu $c>0$; không có số định lý UML nào bị trình bày như của học phần; không thấy đoạn chép hay dịch sát UML hoặc KW.

## Danh sách kiểm §E

| # | Mục §E | Kết quả | Ghi chú |
|---|---|---|---|
| 1 | Một bảng kí hiệu | đạt | theo `ky-hieu.md`; $v$, $\zeta$, $\operatorname{ELBO}$, $\mathrm H$, $\mathrm h$ có giải thích. Lưu ý nhỏ: Ví dụ 09.13 dùng $p$ cho số chiều cạnh $p_{\theta_i}$ cho mật độ (phân biệt được nhờ chỉ số) |
| 2 | Mỗi kết quả nêu cơ chế lấy mẫu, hàm lỗi, đối tượng so sánh, nguồn ngẫu nhiên, loại bảo đảm | đạt | 09.3, 09.8, 09.9, 09.12, 09.13, 09.15 đều có "Giả thiết."/"Bảo đảm." với "đồng nhất thức", "tổng thể", "tất định trên mẫu cố định", "theo kì vọng theo nhiễu phụ" |
| 3 | Chú thích giả thiết trong chứng minh; ví dụ thất bại | đạt | Ví dụ 09.5, 09.7, 09.12, 09.13; mỗi bước chứng minh ghi giả thiết dùng |
| 4 | Kết quả là công thức của học phần; dẫn UML theo mục đã kiểm | đạt một phần | không có số định lý UML; nhưng Ví dụ 09.7 Bước 3 (UML §24.1.3) và đoạn EM (UML §24.4.1) không dẫn trong thân; hai chỗ dẫn sai mục KW |
| 5 | Phân biệt bảo đảm cho lớp mô hình và cho một thuật toán | đạt một phần | dòng 795 gộp Ví dụ 09.4 (mô hình cố định, mẫu kiểm tra) với Bài tập 09.9 (thuật toán làm trơn) |
| 6 | Nói rõ đại lượng được kiểm soát | đạt | rủi ro = entropy + KL, rủi ro vượt mức khi lớp chứa $p_D$ (dòng 420), rủi ro thực nghiệm không tăng (EM), sai lệch $L_S-L_D$ (Ví dụ 09.4), khoảng cách tổng quát hóa (dòng 442) |
| 7 | Không chuyển kết quả hàm lỗi bị chặn sang hàm lỗi log | đạt | dòng 122, Ví dụ 09.4 cần $c>0$, Ví dụ 09.7, §10 |
| 8 | Không chuyển cận lồi sang mạng nơ-ron | đạt | dòng 718, §10 gạch cuối |
| 9 | Một ví dụ số và một câu hỏi cuối buổi | đạt | Ví dụ 09.4 (cận số), §12 |
| 10 | Tách bài gốc và bài UML; không bịa số UML | đạt | §11: 09.1–09.7 gốc, 09.8–09.10 = UML 24.1–24.3 (đã kiểm tr. 356) |
| 11 | Chứng minh dài ở phụ lục | đạt | Phụ lục B cho Mệnh đề 09.15 |
| 12 | Thí nghiệm có mẫu kiểm tra độc lập và nhiều lần chạy; không là chứng minh | đạt | Ví dụ 09.8: 200 chuỗi kiểm tra độc lập, 10 lần chạy, "không phải chứng minh"; Ví dụ 09.5: 10 chuỗi; Phụ lục C cho hạt giống và giao thức |

**Tổng: 10/12 đạt đầy đủ, 2/12 đạt một phần (mục 4, 5).**

## Đối chiếu blueprint

- Prop 9.1 → Mệnh đề 09.3 [F] (độ dài cố định; (c) chiều ngược; câu "giới hạn ngữ cảnh hay kiến trúc là giả thiết thêm" khớp blueprint). Đạt.
- Prop 9.2 → Mệnh đề 09.8 [F] (giá, $\mathrm H(p_D)<\infty$, bản mật độ với hai điều kiện khả tích, entropy vi phân âm và không là giới hạn của entropy rời rạc). Đạt.
- Corollary → Hệ quả 09.9 [F]; dòng 442 nói rõ không phải bảo đảm mẫu hữu hạn và không về chất lượng mẫu. Đạt.
- Thm 9.3 → Định lý 09.12 [F], chứng minh khai triển Bayes và KL đúng như blueprint, dấu bằng hầu khắp nơi. Đạt.
- Prop 9.4 → Mệnh đề 09.15 [S] + Phụ lục B; dạng Gauss $\mu_\phi(x)+\sigma_\phi(x)\odot\zeta$ có ở Định nghĩa 09.14; không khẳng định không chệch khi thiếu điều kiện, trừ §10 (phát hiện T1).
- §9.2: Thiết lập A, B (Định nghĩa 09.1), phân tích tự hồi quy, độ hợp lý có điều kiện, hàm lỗi log, học theo đáp án (Định nghĩa 09.4), mô hình biến ẩn, phân bố biến phân, KL, ELBO, tổng so với chuẩn hóa theo độ dài (Định nghĩa 09.6). Đủ.
- §9.4: bảng ba kí tự (Ví dụ 09.1, 09.3), Bernoulli (Ví dụ 09.2), Gauss một chiều với tái tạo và KL (Ví dụ 09.9–09.10). Đủ. Giới hạn: hàm lỗi log không bị chặn, kí tự không độc lập, độ hợp lý khác chất lượng mẫu (§10). Đủ. GAN/khuếch tán: xem N1.
- §9.6 cầu nối: dòng 860 khớp cả hai nhánh của blueprint (người học điều khiển cách thu dữ liệu; phân bố đổi trong lúc học), và khớp hai ví dụ mở đầu blueprint 10.1.
- Sai khác so với blueprint đều nằm trong danh sách đã chấp nhận (QĐ 1–8 phân tích nguồn, QĐ dàn ý 1–6, `outline.md` §13.2): Hệ quả 09.13 (EM) là khối thêm đã duyệt; Bài tập 09.7 gốc thêm đã duyệt; kí hiệu $v$, $\zeta$, $n$, $j$ thay $z$, $\varepsilon$, $T$, $t$ đã duyệt. Riêng câu "các kết quả của bài không áp dụng cho chúng" (dòng 806) vượt QĐ dàn ý (5).

## Lời hứa

- **Bài 02 dòng 574** ("hàm lỗi log khi hàm dự đoán gán xác suất rất nhỏ cho nhãn đúng, tạo ra đúng tình huống này"): giữ. Dòng 122 nêu hàm lỗi log không thỏa (T3); Ví dụ 09.4 cần $c>0$ và Kết luận nhắc Nhận xét 02.11; Ví dụ 09.7 Bước 1 (xác suất nhỏ trên giá cho $L_D$ lớn) và Kết luận dẫn Nhận xét 02.11; §10 gạch đầu.
- **Cầu nối cuối Bài 08** (lec-08 dòng 906: quan sát là chuỗi, hàm lỗi là $-\ln$ độ hợp lý của cả chuỗi, viết lại rủi ro kì vọng, rủi ro thực nghiệm, giả thiết độc lập): dòng 3 nhắc lại gần nguyên văn, dòng 32 trả lời, §1 mục 2 và §6 trả lời phần giả thiết độc lập. Giữ.

## Trang nguồn đã đọc

- UML (PDF): tr. 343, 344, 345, 346, 347 (§24.1–§24.1.3, đầu §24.2); 348 (§24.3, đầu §24.4); 349, 350, 351, 352 (§24.4, §24.4.1, Bổ đề 24.2, Định lý 24.3, đầu §24.4.2); 356 (§24.8, Bài tập 24.1–24.3).
- Kingma–Welling (`sources/supp/kingma-welling-2014.pdf`): tr. 2 (§2.1), 3 (§2.1 cuối, §2.2, §2.3), 4 (Thuật toán 1, (7)–(8), §2.4), 5 (§2.4 cuối, §3), 10–11 (Phụ lục B).
- Repo: `sources/blueprint.md` (§A, cuối Lecture 8, Lecture 9, đầu Lecture 10, §C–§F), `CLAUDE.md` học phần, `2627-1/planning/lec-09/source-analysis.md`, `review-log.md`; `lec-01` Định nghĩa 01.1, (T2), Nhận xét 01.2; `lec-02` dòng 84, 413, 560–577; `lec-08` dòng 906.

## Phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | dòng 806 (§10, câu cuối) — N1 | Câu thêm hai khẳng định không có cơ sở trong nguồn được giao: mô hình khuếch tán có "mục tiêu huấn luyện khác … ELBO", và "các kết quả của bài không áp dụng cho chúng". Khẳng định thứ hai sai: Mệnh đề 09.3, 09.8 đúng cho mọi phân bố, Định lý 09.12 đúng cho mọi mô hình biến ẩn, kể cả mô hình khuếch tán (vốn được huấn luyện bằng một cận biến phân có trọng số). Câu cũng vượt QĐ dàn ý (5): "chỉ nêu đó là mục tiêu/mô hình khác ngoài phạm vi, không thêm khẳng định nào khác" | blueprint 9.4: "Mention GANs and diffusion only as alternative objectives/models in a brief optional comparison"; `review-log.md` QĐ dàn ý (5) | Thay bằng: "Mạng đối kháng sinh (generative adversarial network, GAN) và mô hình khuếch tán (diffusion model) là các mô hình sinh khác; mục tiêu huấn luyện và cách đánh giá chúng nằm ngoài phạm vi bài." (ngắn hơn bản cũ khoảng 6 tiếng) |
| trung bình | dòng 793 (§10, đoạn 1) — T1 | "gradient tái tham số hóa là một gradient ngẫu nhiên không chệch như ở Bài 05 (Mệnh đề 09.15)" bỏ điều kiện; Ví dụ 09.12 chính là trường hợp nó chệch | blueprint 9.3 Prop 9.4: "Do not claim unbiasedness without those conditions" | Viết: "… gradient tái tham số hóa là một gradient ngẫu nhiên không chệch khi các điều kiện của Mệnh đề 09.15 thỏa." Bù chữ: cắt mệnh đề "Với mô hình biến ẩn, $v$ đóng vai một mã của quan sát, và Kingma và Welling (§2.2) gọi $q_\phi$ là *bộ mã hóa xác suất* (probabilistic encoder);" (khoảng 25 tiếng; đồng thời bỏ chỗ dẫn sai mục, xem dòng dưới) |
| trung bình | dòng 870 (§13, "Quan hệ với nguồn", gạch "Kí hiệu") | Thiếu sai khác quan trọng nhất khi học viên đọc UML §24.1: UML kí hiệu $L(S;\theta)$ là **log độ hợp lý** và cực đại nó, ngược dấu với $L_S(\theta)$ của học phần (cực tiểu); UML §24.4 dùng $L(\theta)$ cùng nghĩa. Người đọc dễ nhầm hai chữ $L$ | UML tr. 343 ("log likelihood of S … $L(S;\theta)$", (24.3) argmax), tr. 344, tr. 349; source-analysis dòng 3, 66 | Thêm vào gạch "Kí hiệu": "UML viết $L(S;\theta)$ cho log độ hợp lý và cực đại nó, tức $L(S;\theta)=-m\,L_S(\theta)$." (khoảng 20 tiếng; bù bằng chỗ cắt ở dòng 793 hoặc dòng 152) |
| trung bình | dòng 451 (Ví dụ 09.7, Bước 3) | Ý của bước này (Bernoulli với $\theta^\star$ nhỏ, mẫu toàn $0$ với xác suất $(1-\theta^\star)^m$, $\hat\theta=0$, rủi ro $+\infty$) là phản ví dụ của UML §24.1.3 nhưng không được dẫn; các số $0{,}01$, $m\le68$ là của học phần (UML dùng cận lỏng $m\le\ln2/(2\theta^\star)$). CLAUDE.md: dẫn UML theo mục | UML tr. 346 đoạn "In some situations, the maximum likelihood estimator clearly overfits …" | Thêm "(theo ý của UML §24.1.3)" sau "Lấy $D=\mathrm{Ber}(\theta^\star)$ với $\theta^\star=0{,}01$" (5 tiếng) |
| trung bình | dòng 795 (§10, đoạn 2) | "Bảo đảm cho mẫu hữu hạn chỉ có ở Ví dụ 09.4, với $c>0$, và Bài tập 09.9" gộp hai loại bảo đảm khác nhau: Ví dụ 09.4 là khoảng tin cậy cho **một mô hình cố định** trên mẫu kiểm tra; Bài tập 09.9 là cận rủi ro cho **một thuật toán** (ước lượng làm trơn). §E: "Distinguish a model-class guarantee from a guarantee for one training algorithm" | dòng 276 ("cố định, không phụ thuộc mẫu kiểm tra"); UML tr. 356 Bài tập 2 | Viết: "Bảo đảm cho mẫu hữu hạn chỉ có ở Ví dụ 09.4, cho một mô hình cố định có $c>0$ trên mẫu kiểm tra, và Bài tập 09.9, cho ước lượng có hai quan sát giả; …" (+8 tiếng) |
| trung bình | dòng 711–718 | "là một gradient ngẫu nhiên không chệch … dưới các điều kiện trên": Mệnh đề 09.15 đặt điều kiện cho $\kappa(\phi,\zeta)$ theo $\phi$; ở đây hàm lấy gradient phụ thuộc $(\theta,\phi)$ cả trực tiếp (qua $\ln q_\phi$, $p_\theta$) lẫn qua $g_\phi(\zeta)$, nên cần nói (i)–(iii) áp cho hàm nào và theo biến nào | Định nghĩa 09.14 ($f$ không phụ thuộc $\phi$); Mệnh đề 09.15 (i)–(iii) | Thay "dưới các điều kiện trên" bằng "khi hàm trong ngoặc, xem như $\kappa$ theo tham số $(\theta,\phi)$, thỏa (i)–(iii) của Mệnh đề 09.15" (+12 tiếng). Có thể ghi thêm: Thuật toán 1 của KW dùng tổng nhân $N/M$, khác trung bình của học phần một hằng số |
| nhẹ | dòng 793 | Kingma–Welling gọi $q_\phi$ là "probabilistic encoder" ở §2.1 (cuối mục, tr. 3), không ở §2.2 | KW tr. 3, đoạn trước tiêu đề "2.2 The variational bound" | Nếu giữ câu: đổi "§2.2" thành "§2.1"; đề xuất cắt (xem T1) |
| nhẹ | dòng 669 | "Kingma và Welling (§2.1–§2.2) … cực đại ELBO theo $(\theta,\phi)$ bằng SGD": SGD và Thuật toán 1 ở §2.3 | KW tr. 3–4 | Đổi thành "(§2.1–§2.3)" |
| nhẹ | dòng 105 | "xác suất theo mẫu chỉ xuất hiện ở §6 và trong thí nghiệm" sai: Ví dụ 09.7 Bước 3 (§7) tính $0{,}99^m$ và $\mathbb E_SL_D(\hat\theta)$ | dòng 451 | Đổi thành "chỉ xuất hiện ở §6, Ví dụ 09.7 và trong thí nghiệm" (+2 tiếng) |
| nhẹ | dòng 122 | "Các cận của Bài 02–04 và Bài 07 chỉ áp dụng khi xác suất của mô hình bị chặn dưới": đủ cho hàm xác suất; với mật độ còn cần mật độ bị chặn trên (hàm lỗi có thể âm không bị chặn) | dòng 122 câu trước (mật độ $N(0;0{,}01)$ cho $\ell<0$) | "… chỉ áp dụng khi hàm lỗi bị chặn, chẳng hạn khi xác suất của mô hình rời rạc bị chặn dưới, như …" (+6 tiếng); hoặc chỉ thêm "(với hàm xác suất)" |
| nhẹ | dòng 238 | "phân bố của tiền tố lúc sinh khác lúc huấn luyện" là khẳng định vô điều kiện; nếu $p_\theta=p_D$ hai phân bố trùng | Mệnh đề 09.3(a) | "… có thể khác lúc huấn luyện khi $p_\theta\ne p_D$" (+5 tiếng) |
| nhẹ | dòng 860 | "phân bố duy nhất phụ thuộc tham số là $q_\phi$" không chính xác: $p_\theta$ cũng phụ thuộc tham số; ý đúng là phân bố **lấy kì vọng/rút mẫu** | dòng 377–386, §8 | "phân bố rút mẫu duy nhất phụ thuộc tham số là $q_\phi$" (+1 tiếng) |
| nhẹ | dòng 873 | Câu "một ví dụ cho thấy khả vi hầu khắp nơi tại từng tham số chưa đủ" chưa nói KW giả sử gì; KW §2.1 giả sử các mật độ khả vi hầu khắp nơi theo $\theta$ và $z$, và §2.3 nói "certain mild conditions outlined in section 2.4". Nêu ra để so sánh trung tính, không đánh giá | KW tr. 2 ("PDFs are differentiable almost everywhere w.r.t. both θ and z"), tr. 3 | "… nhắc tới 'một số điều kiện nhẹ' cho tái tham số hóa và giả sử các mật độ khả vi hầu khắp nơi (§2.1)." (+8 tiếng; có thể bù bằng cắt "hay điều kiện khả tích" nếu cần) |
| nhẹ | dòng 638 | Đoạn "cực đại ELBO luân phiên … là thuật toán EM" và Hệ quả 09.13 là nội dung UML §24.4.1 (Bổ đề 24.2, Định lý 24.3) nhưng thân bài không dẫn mục; chỉ §13 nhắc | UML tr. 350–352 | Thêm "(UML §24.4.1)" sau "là thuật toán EM" (3 tiếng) |
| nhẹ | dòng 485 (Ví dụ 09.8, Kết luận (iii)) | "khoảng tin cậy dùng số chuỗi kiểm tra làm cỡ mẫu (Ví dụ 09.4)": Ví dụ 09.4 cần $c>0$; đúng cho mô hình làm trơn, không cho MLE có xác suất $0$ | dòng 276, 302 | Thêm "với mô hình làm trơn" (4 tiếng) hoặc "khi xác suất bị chặn dưới" |
| nhẹ | dòng 492 | "Khi mô hình quan sát là một mạng nơ-ron, tích phân này nói chung không tính được (Kingma và Welling, §2.1)" mạnh hơn nguồn một chút: KW nói các trường hợp này "khá phổ biến", ví dụ "mạng nơ-ron có một lớp ẩn phi tuyến" | KW tr. 2, mục "Intractability" | Có thể giữ; nếu sửa: "chẳng hạn khi mô hình quan sát là một mạng nơ-ron có lớp ẩn phi tuyến" |
| nhẹ (đã giao rà toán) | Ví dụ 09.6 (dòng 333) so với Định nghĩa 09.6 | Định nghĩa 09.6 đặt trên mô hình có kí tự kết thúc; Ví dụ 09.6 coi độ dài cho trước, nên "rủi ro kì vọng" ở đây là hàm lỗi log có điều kiện theo độ dài, không phải $L_D$ của một hàm xác suất trên $\mathcal X$ (Mệnh đề 09.8 không áp trực tiếp). Ví dụ không dùng Mệnh đề 09.8 nên kết luận vẫn đúng | dòng 324, 333 | Thêm "(hàm lỗi log có điều kiện theo độ dài)" vào Thiết lập, hoặc để người rà toán quyết |

## Cân đối số chữ (thân 11 984/12 000)

Tổng phần thêm đề xuất ≈ +70 tiếng (N1 −6, T1 +8, UML dấu +20, §24.1.3 +5, dòng 795 +8, dòng 718 +12, các mục nhẹ ≈ +25). Chỗ cắt đề xuất, đủ bù:

1. Dòng 793: cắt mệnh đề về "mã của quan sát" và "bộ mã hóa xác suất" (≈ −25; đồng thời sửa dẫn sai §2.2).
2. Dòng 152: cắt câu chuyển "Với ví dụ thứ hai, chúng ta cần biết mô hình được chọn theo tiêu chí nào và giá trị tốt nhất của tiêu chí đó." (≈ −25; đầu §4 đã nêu vấn đề).
3. Dòng 504: cắt "Câu ôn nhanh 3 là một mô hình biến ẩn với $\mathcal V=\{1,2\}$." (≈ −12).
4. Dòng 873: cắt "hay điều kiện khả tích" nếu thêm câu về khả vi hầu khắp nơi (≈ −5).
5. Nếu còn thiếu: dòng 801 bỏ "nat" và "mỗi tọa độ" lặp lại Ví dụ 09.13 (≈ −4).
