# Bảng thuật ngữ Việt–Anh của học phần

Tệp nội bộ, không liên kết từ trang chỉ mục. Mọi ghi chú và bài tập dùng đúng thuật ngữ ở cột "Thuật ngữ được chọn". Kí hiệu nằm ở `ky-hieu.md`, văn phong ở `van-phong.md`. Mỗi bài thêm thuật ngữ mới vào mục tương ứng khi soạn dàn ý; một thuật ngữ đã chọn chỉ được đổi khi đồng thời sửa mọi ghi chú đã dùng nó. Lập ngày 2026-10-30.

## 1. Cách chọn và cách đếm

- **Ưu tiên lựa chọn đa số trong sách** *Học máy thống kê* (`../SML-textbook-main.zip`, viết tắt SML). Khi sách không thống nhất, bảng chọn một cách gọi và ghi cách gọi bị loại ở cột "Ghi chú". Khi sách không có thuật ngữ, cột "Căn cứ" ghi **đề xuất** kèm lý do.
- **Đối chiếu học phần anh em** khi sách im lặng: M4AI là ghi chú của Cơ sở toán học cho AI (`../math-4-AI/2627-1/materials/*/lecture-note.md`, chủ yếu `lec-05c`), DL là ghi chú của Học sâu (`../deep-learning/2627-1/materials/*/lecture-note.md`). Chỗ học phần này cố ý khác được liệt kê ở mục 3.
- **Cách đếm SML:** đếm chuỗi con, không phân biệt hoa thường, sau khi chuẩn hóa Unicode NFC, trên mọi tệp `.tex` của sách trừ `*backup*.tex` và `rm_sec_parametric_models.tex` (bản nháp không được `\input`), sau khi bỏ chú thích LaTeX (từ `%` đến cuối dòng). Tên tệp trong ngoặc là tệp có nhiều lần xuất hiện nhất; số đếm gồm cả cụm dài hơn chứa chuỗi ("hàm lỗi" gồm cả "hàm lỗi entropy chéo").
- **Sửa số liệu ban đầu.** Các số trong ghi chép ban đầu (214/119 cho "phân bố"/"phân phối", 54/8 cho "kì vọng"/"kỳ vọng", 171 cho "hàm lỗi") tính cả dòng chú thích và tệp nháp. Sau khi bỏ chú thích: "phân bố" 184, "phân phối" 70; "kì vọng" 46, "kỳ vọng" 9; "hàm lỗi" 153, "hàm mất mát" 1; "quá khớp" 6, "phù hợp trội" 2; "tổng quát hóa" 15 (11 lần "hóa", 4 lần "hoá"), "khái quát" 2. Đa số không đổi. Cụm "độc lập, phân phối giống nhau (i.i.d.)" chỉ có trong một dòng chú thích (`07_ensemble_learning/sec_bagging_and_rf.tex`, dòng 40), nên sách không có thuật ngữ cho i.i.d. Ước lượng hợp lý cực đại trong sách là "ước lượng hợp lý cực đại" (22 lần), không phải "cực đại độ hợp lý" (1 lần).

## 2. Các quyết định chính

| Khái niệm | Chọn | Loại | Lý do ngắn |
|---|---|---|---|
| loss | hàm lỗi | hàm mất mát, mất mát | SML 153 so với 1 |
| distribution | phân bố | phân phối | SML 184 so với 70 |
| expectation | kì vọng | kỳ vọng | SML 46 so với 9 |
| overfitting | quá khớp | phù hợp trội | SML 6 so với 2 |
| generalization | tổng quát hóa | khái quát hóa, tổng quát hoá | SML 15 so với 2; dấu thanh kiểu mới |
| ERM | tối thiểu hóa rủi ro thực nghiệm | cực tiểu hóa rủi ro thực nghiệm | SML 4 so với 2 trong cùng tệp; khớp `CLAUDE.md` |
| hypothesis, hypothesis class | giả thuyết, lớp giả thuyết | hàm phân lớp, lớp hàm phân lớp (cho $h$, $\mathcal H$ tổng quát) | đề xuất: $\mathcal H$ còn chứa hàm hồi quy và mật độ; "hàm phân lớp" giữ cho bài toán phân lớp |
| population risk | rủi ro kì vọng | rủi ro tổng thể | theo SML; người dùng chốt 2026-10-30. Ở Bài 06, 08 viết $\mathbb E_S[L_D(A(S))]$ là "kì vọng theo mẫu của rủi ro kì vọng", luôn ghi chỉ số $\mathbb E_S$ |
| gradient | gradient | đạo hàm (cho $\nabla F$) | theo học phần anh em; người dùng chốt 2026-10-30 |
| step size, learning rate $\eta_t$ | độ dài bước | tốc độ học, bước học, bước nhảy | theo học phần anh em, cùng họ gradient; người dùng chốt 2026-10-30 |

## 3. Khác biệt có chủ ý với học phần anh em

| Khái niệm | Học phần này | M4AI | DL | Lý do |
|---|---|---|---|---|
| distribution | phân bố | phân phối (235 lần) | phân phối (20), phân bố (3) | theo SML |
| expectation | kì vọng | kỳ vọng (471) | kỳ vọng (8) | theo SML |
| loss | hàm lỗi | hàm mất mát (26), mất mát | hàm mất mát (36) | theo SML |
| classification | phân lớp | phân loại (135) | phân loại (35) | SML "phân lớp" 210, "phân loại" 56 |
| gradient, GD, subgradient | gradient, hạ gradient, dưới gradient | gradient, hạ gradient, dưới gradient | gradient | giống học phần anh em; người dùng chốt 2026-10-30 |
| regularization | chính quy hóa | chính quy hóa (209) | điều chuẩn (12) | khớp M4AI và `ky-hieu.md`; SML dùng "hàm điều chỉnh" |
| validation set | tập xác thực | tập xác thực (90) | tập xác thực (7), tập kiểm định (4) | khớp đa số anh em; SML gọi là "tập kiểm thử" |

Các thuật ngữ trùng với anh em: quá khớp, tổng quát hóa, rủi ro thực nghiệm, bất đẳng thức tập trung, bất đẳng thức hợp, lô nhỏ, không chệch, biến cố, cỡ mẫu, quan sát, lồi mạnh, tự hồi quy, học theo đáp án.

## 4. Xác suất và thiết lập chung

| English | Thuật ngữ được chọn | Căn cứ | Ghi chú |
|---|---|---|---|
| probability space | không gian xác suất | đề xuất; M4AI 19 | nêu trước mọi cận |
| distribution | phân bố | SML 184 (`11_generative_models/sec_em.tex` 34); "phân phối" 70 | loại "phân phối"; sách lẫn hai từ trong cùng `sec_em.tex` |
| data-generating distribution | phân bố dữ liệu | SML 4; in nghiêng trong định nghĩa của `sec_statistical_learning.tex` | $D$; lần đầu có thể giải thích "phân bố sinh ra các quan sát" |
| random variable | biến ngẫu nhiên | SML 21 | chữ hoa: $Z$, $X$, $Y$ |
| event | biến cố | SML 1 (`chapter_appendix.tex`); M4AI 163 | loại "sự kiện" (SML 4, `sec_statistical_learning.tex`), từ thông thường |
| indicator function | hàm chỉ thị | SML 2 | $\mathbb 1[\cdot]$ (sách viết $\mathbb I$) |
| expectation | kì vọng | SML 46 (`sec_em.tex` 12); "kỳ vọng" 9 | $\mathbb E$, ghi chỉ số khi có nhiều nguồn ngẫu nhiên |
| conditional expectation | kì vọng có điều kiện | đề xuất; M4AI "kỳ vọng có điều kiện" 39 | chỉ đổi chính tả |
| conditional probability | xác suất có điều kiện | SML 6 | |
| density, marginal density | mật độ, mật độ biên | SML 36; "mật độ biên" 1 (`sec_minimize_risk_classifier.tex`) | |
| prior, posterior | tiên nghiệm, phân bố hậu nghiệm | SML 11; 9 | |
| variance | phương sai | SML 72 | |
| unbiased | không chệch | SML 3; M4AI 85 | |
| independent and identically distributed (i.i.d.) | độc lập cùng phân bố (independent and identically distributed, i.i.d.) | đề xuất; M4AI "độc lập cùng phân phối (…, i.i.d.)" | cùng cấu trúc với M4AI, đổi "phân phối" thành "phân bố"; loại "độc lập, phân phối giống nhau" (chỉ có trong dòng chú thích của SML) |
| sample | mẫu, mẫu huấn luyện | `ky-hieu.md` | chỉ cả dãy $S=(Z_1,\ldots,Z_m)$; loại "mẫu dữ liệu", "mẫu huấn luyện" theo nghĩa một điểm (SML 101, 11) |
| example, observation | quan sát | `ky-hieu.md`; SML 30; M4AI 430 | $z_i$, $Z_i$ |
| sample size | cỡ mẫu | đề xuất; M4AI 23 | $m$; SML viết "số mẫu dữ liệu $n$" |
| sampling with replacement | lấy mẫu có hoàn lại | SML 9 (`sec_bagging_and_rf.tex` 7) | |
| input, input space | đầu vào, tập đầu vào | SML 193; "tập đầu vào" 14 | $\mathcal X$ |
| label, label set | nhãn, tập nhãn | SML 153 | $\mathcal Y$ |
| feature, feature dimension | đặc trưng, số chiều đặc trưng | SML 269; "số chiều" 15 | $p$; không dùng $d$ |
| parameter, weight, hyperparameter | tham số, trọng số, siêu tham số | SML 239; 172; 9 | |
| vector, inner product, norm | véc-tơ, tích vô hướng, chuẩn | SML 97; 9; nhiều | loại "vector", "vectơ" |
| measurable | đo được | đề xuất; M4AI 36 | |
| infimum, supremum | cận dưới đúng, cận trên đúng | đề xuất; `ky-hieu.md`; M4AI 89 | SML có "cận dưới đúng" 1 lần nhưng theo nghĩa "cận dưới đúng với mọi phân bố", không làm căn cứ |
| minimum | giá trị nhỏ nhất | SML 2 ("nhỏ nhất" 16) | chỉ dùng khi đạt được |
| minimize, maximize | tối thiểu hóa, cực đại hóa | SML "tối thiểu hóa/hoá" 11, "cực tiểu hóa/hoá" 10; "cực đại hóa/hoá" 26, "tối đa hóa" 2 | động từ "tối thiểu hóa" khớp tên ERM; "cực đại hóa" khớp "hợp lý cực đại"; "cực tiểu" chỉ dùng cho điểm cực tiểu |
| upper bound, lower bound | cận trên, cận dưới | SML 14; 11 | động từ "chặn": "chặn $X$ bởi …"; loại danh từ "chặn trên" (SML 1) |
| with probability at least $1-\delta$ | với xác suất ít nhất $1-\delta$ | người dùng chốt 2026-10-30 | ghi rõ xác suất theo $S\sim D^m$; loại "không thấp hơn" (SML 4) |
| with high probability / in expectation | với xác suất cao / theo kì vọng | SML 5 / đề xuất | hai loại bảo đảm phải tách rõ |
| objective function | hàm mục tiêu | SML 52 (`06_reinforcement_learning/sec_deep_rl.tex` 15) | chỉ cho hàm cần tối ưu; sách còn dùng cho hàm gán nhãn $f$ (`sec_classification_definition.tex`) |
| labeling function | hàm gán nhãn | đề xuất | thay nghĩa thứ hai của "hàm mục tiêu" trong sách |
| counterexample | phản ví dụ | đề xuất; `course-plan.md` | |

## 5. Bài 01: rủi ro, ERM và PAC

| English | Thuật ngữ được chọn | Căn cứ | Ghi chú |
|---|---|---|---|
| classification, binary classification | phân lớp, phân lớp nhị phân | SML 210 ("phân loại" 56); 6 | M4AI, DL dùng "phân loại" |
| regression | hồi quy | SML 186 | |
| predictor | hàm dự đoán | SML 3 (`05_regression/sec_regression_introduction.tex`, `sec_knn_regression.tex`) | `ky-hieu.md` ghi "bộ dự đoán"; câu hỏi mở 3 |
| classifier | hàm phân lớp | SML 43 (`sec_erm_framework.tex` 14) | loại "mô hình phân lớp" (SML 14), "bộ phân lớp" (1) trong phát biểu hình thức |
| hypothesis | giả thuyết | đề xuất | SML dùng "giả thuyết" 9 lần theo nghĩa kiểm định thống kê hoặc giả định chung, không dùng cho $h$ (sách gọi $h$ là "hàm phân lớp"); $h$ là một hàm dự đoán $\mathcal X\to\mathcal Y$ |
| hypothesis class | lớp giả thuyết | đề xuất; `ky-hieu.md`; SML "lớp hàm phân lớp" 4 (`sec_erm_framework.tex`) | $\mathcal H$; "lớp hàm phân lớp" chỉ đúng khi $\mathcal H$ gồm hàm phân lớp |
| assumption | giả thiết | SML 8 | không viết "giả thuyết" cho giả định (SML có viết "giả thuyết độc lập xác suất", `sec_naive_bayes.tex`); nhãn "**Giả thiết.**" trong khối kết quả |
| learner, learning algorithm | thuật toán học | SML 34 (`00_intro/sec_types_of_ML.tex` 7); "thuật toán huấn luyện" 43 | $A$, $A(S)$; loại "bộ học"; "thuật toán huấn luyện" không dùng trong phát biểu hình thức |
| loss function | hàm lỗi | SML 153 (`02_multilayer_perceptron/sec_optimizer.tex` 20); "hàm mất mát" 1 | $\ell(h,z)$; giá trị gọi là "lỗi của $h$ trên quan sát $z$"; ghi miền giá trị |
| 0–1 loss | hàm lỗi 0–1 | đề xuất từ "hàm lỗi" | $\ell_{0\text{-}1}$; SML mô tả bằng hàm chỉ thị của biến cố phân lớp sai |
| squared loss, log loss | hàm lỗi bình phương, hàm lỗi log | đề xuất | kết quả cho hàm lỗi bị chặn không tự chuyển sang hai hàm lỗi này |
| cross-entropy loss, hinge loss | hàm lỗi entropy chéo, hàm lỗi bản lề | SML 8; 2 (`08_SVM/sec_soft_margin.tex`) | |
| risk | rủi ro | SML 12 (`sec_erm_framework.tex` 10) | |
| population risk (true risk) | rủi ro kì vọng | SML "rủi ro kì vọng" 3 (`sec_erm_framework.tex`); người dùng chốt 2026-10-30 | $L_D(h)$; với hàm lỗi 0–1 là "xác suất lỗi" (SML 15). Không dùng "rủi ro tổng thể". Khi lấy kì vọng theo mẫu, viết rõ $\mathbb E_S[L_D(A(S))]$ |
| empirical risk | rủi ro thực nghiệm | SML 8 (`sec_erm_framework.tex` 7); M4AI 45 | $L_S(h)$; loại "lỗi thực nghiệm", "lỗi huấn luyện" (SML 4, 3) trong phát biểu hình thức |
| error rate | tỉ lệ lỗi | SML 20 | chỉ cho tỉ lệ lỗi đếm trên một mẫu (rủi ro thực nghiệm với hàm lỗi 0–1); sách dùng cho cả xác suất lỗi |
| empirical risk minimization (ERM) | tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM) | SML 4 (`sec_erm_framework.tex`) | viết thường giữa câu; loại "cực tiểu hóa rủi ro thực nghiệm" (SML 2, cùng tệp) |
| an ERM, ERM rule | nghiệm ERM, quy tắc ERM | đề xuất | $\hat h\in\arg\min_{h\in\mathcal H}L_S(h)$; nêu quy tắc chọn khi có nhiều nghiệm |
| tie-breaking | quy tắc chọn khi bằng nhau | đề xuất | |
| approximate ERM | ERM xấp xỉ | đề xuất | $L_S(\tilde h)\le\inf_{h\in\mathcal H}L_S(h)+\epsilon_{\mathrm{opt}}$; đại lượng $\operatorname{opt}_S$ ở Bài 04 |
| realizable, realizability assumption | khả thực, giả thiết khả thực | đề xuất | có $h^\star\in\mathcal H$ với $L_D(h^\star)=0$; tương đối với cả $D$ và $\mathcal H$ |
| agnostic PAC learning | học PAC bất khả tri | đề xuất | so với $\inf_{h\in\mathcal H}L_D(h)$ |
| probably approximately correct (PAC) | học xấp xỉ với xác suất cao (probably approximately correct, PAC) | SML: tên định lý "Học xấp xỉ với xác suất cao (PAC Learning)" (`sec_erm_framework.tex`) | sau lần đầu: "học PAC" |
| PAC learnable | học được PAC | đề xuất | "lớp $\mathcal H$ học được PAC" |
| distribution-free | không phụ thuộc phân bố | đề xuất | |
| sample complexity | độ phức tạp mẫu | đề xuất; `ky-hieu.md` | $m_{\mathcal H}(\epsilon,\delta)$ |
| accuracy parameter | tham số độ chính xác | `ky-hieu.md` | $\epsilon$ |
| confidence, failure probability | độ tin cậy, xác suất thất bại | `ky-hieu.md` | độ tin cậy là $1-\delta$, xác suất thất bại là $\delta$; không gọi $\delta$ là "độ tin cậy" |
| inductive bias | thiên kiến quy nạp | đề xuất | không dùng "độ lệch quy nạp": "độ lệch" dành cho bias thống kê (Bài 04) |
| overfitting | quá khớp | SML 6 (`03_cnn/sec_training_strategy.tex` 2); M4AI 15, DL 9 | loại "phù hợp trội" (SML 2, `10_ML_in_production/sec_data_preparation.tex`) |
| underfitting | chưa khớp | đề xuất | SML "không phù hợp (underfitting)" 1, quá chung |
| generalization | tổng quát hóa | SML 15; M4AI 18, DL 2 | loại "khái quát hóa" (SML 2) và dạng "hoá" |
| generalization gap | khoảng cách tổng quát hóa | đề xuất | $L_D(A(S))-L_S(A(S))$, có dấu; không gọi là "sai số tổng quát hóa" vì dễ hiểu thành $L_D$ |
| memorization | ghi nhớ | đề xuất | "hàm phân lớp ghi nhớ" cho phản ví dụ 1.2 của blueprint |
| Bayes optimal classifier | hàm phân lớp tối ưu Bayes | SML 7 (`sec_minimize_risk_classifier.tex` 4) | |
| Bayes risk | rủi ro Bayes | đề xuất | SML gọi $R^\star$ là "xác suất lỗi tối ưu"; với lỗi 0–1 hai tên trùng nghĩa |
| regression function $\eta(x)$ | xác suất có điều kiện $\eta(x)=\Pr(Y=1\mid X=x)$ | đề xuất | |
| excess risk | rủi ro vượt mức | đề xuất | luôn ghi so với gì: $\inf_{h\in\mathcal H}L_D(h)$ hay rủi ro Bayes |
| comparator | đối tượng so sánh | `course-plan.md` | |
| no-free-lunch theorem | định lý không có bữa trưa miễn phí | SML 2 (`sec_erm_framework.tex`) | loại "bữa ăn" (`01_classification/sec_conclusion.tex`) |
| marginal distribution | phân bố biên | đề xuất (Bài 01) | $D_{\mathcal X}$ |
| empirical distribution | phân bố thực nghiệm | đề xuất (Bài 01) | phân bố đều trên các quan sát của $S$ |
| almost surely | hầu chắc chắn | đề xuất (Bài 01) | viết tắt "h.c.c." chỉ sau lần đầu |
| atom (of a distribution) | nguyên tử | đề xuất (Bài 01) | điểm có xác suất dương |
| internal randomness | nguồn ngẫu nhiên nội tại | đề xuất (Bài 01) | $\xi$ |
| cost-sensitive (weighted) loss | hàm lỗi có trọng số | đề xuất (Bài 01) | $\ell_c$ với $(c_{FP},c_{FN})$ |
| false positive, false negative | dương tính giả, âm tính giả | đề xuất (Bài 01) | |
| screening | sàng lọc | đề xuất (Bài 01) | |
| conditional risk | rủi ro có điều kiện | đề xuất (Bài 01) | rủi ro tại một $x$ cố định |
| proper learning, improper learning | học đúng lớp, học ngoài lớp | đề xuất (Bài 01) | $A(S)\in\mathcal H$ hay không |
| statistical learning problem (UML: learning setting) | bài toán học thống kê | người dùng yêu cầu định nghĩa hình thức, 2026-10-30 (Bài 01, Định nghĩa 01.5) | tên rút gọn "bài toán học"; một tên tiếng Anh trong ngoặc |
| spam filtering | lọc thư rác | đề xuất (Bài tập 01.1) | |
| least squares | bình phương tối thiểu | đề xuất (Bài tập 01.1) | |
| point mass | khối lượng điểm | đề xuất (Bài tập 01.4) | không dùng $\delta_0$ (trùng $\delta$) |
| thresholded polynomials | lớp đa thức có ngưỡng | đề xuất (Bài tập 01.6) | $\mathcal H_{\mathrm{poly}}$ |
| class of singletons | lớp hàm chỉ thị của một điểm | đề xuất (Bài tập 01.8) | $\mathcal H_{\mathrm{sg}}$ |
| annulus, closed annulus | vành, vành đóng | đề xuất (Bài tập 01.9) | |
| right-continuous | liên tục phải | đề xuất (Bài tập 01.9) | |
| probabilistic label predictor | hàm dự đoán xác suất | đề xuất (Bài tập 01.11) | |
| inclusion–exclusion | bao hàm–loại trừ | đề xuất (Bài tập 01.8) | |
| concentric disks (UML Ex. 3.3), $h_r=\mathbb 1[\lVert x\rVert\le r]$ | lớp hình tròn đồng tâm | điều phối viên chốt 2026-10-30 | "đường tròn" chỉ dùng cho đường biên $\lVert x\rVert=r$ |
| finite-risk distribution | phân bố có rủi ro hữu hạn | đề xuất (Bài 01, thay "chấp nhận được") | $L_D(h)<\infty$ với mọi $h\in\mathcal H$; UML lấy mọi $D$ |
| probability mass | khối lượng xác suất | đề xuất (Bài 01) | lần đầu kèm tiếng Anh, sau đó "khối lượng" |
| population quantity | đại lượng tổng thể | đề xuất (Bài 01) | đại lượng theo $D$; khác tên "rủi ro tổng thể" đã loại |
| precision | giá trị dự đoán dương | đề xuất (Bài 01) | tránh "độ chính xác" (dành cho $\epsilon$) |
| generalization bound valid for every ERM algorithm | cận tổng quát hóa cho mọi thuật toán ERM | đề xuất (Bài 01) | $\beta(m,\delta)$; không dùng "lựa chọn ERM" |
| memorizing algorithm, memorizing classifier | thuật toán ghi nhớ, hàm phân lớp ghi nhớ | đề xuất (Bài 01) | $A_{\mathrm{gn}}$, $A_{\mathrm{gn}}(S)$; hai tên cố định |
| unbiased estimator | ước lượng không chệch | đề xuất (Bài 01) | |
| tower property | tính chất tháp | đề xuất (Bài 01) | |
| posterior probability | xác suất hậu nghiệm | đề xuất (Bài 01) | |
| realizability (property) | tính khả thực | đề xuất (Bài 01) | tiêu đề định nghĩa; "giả thiết khả thực" là giả thiết rằng cặp khả thực |

## 6. Bài 02: bất đẳng thức tập trung và lớp hữu hạn

| English | Thuật ngữ được chọn | Căn cứ | Ghi chú |
|---|---|---|---|
| tail probability | xác suất đuôi | đề xuất; M4AI `lec-05c` | $\Pr(X\ge t)$ |
| tail bound | cận đuôi | đề xuất | cận trên của xác suất đuôi |
| concentration inequality | bất đẳng thức tập trung | đề xuất; M4AI 9 | |
| Markov's inequality, Chebyshev's inequality | bất đẳng thức Markov, bất đẳng thức Chebyshev | SML 1 (`chapter_appendix.tex`); M4AI | |
| Chernoff method, Chernoff bound | phương pháp Chernoff, cận Chernoff | đề xuất; M4AI | |
| moment generating function | hàm sinh mô-men | đề xuất | gạch nối như "mô-men" trong SML (3, `sec_optimizer.tex`); M4AI viết "hàm sinh mômen" (15) |
| Hoeffding's lemma | bổ đề Hoeffding | SML 2 (`chapter_appendix.tex`) | |
| Hoeffding's inequality | bất đẳng thức Hoeffding | đề xuất; M4AI | SML gọi "định lý Hoeffding" (1, `sec_erm_framework.tex`); tên theo đối tượng, khớp blueprint |
| union bound | bất đẳng thức hợp | đề xuất; M4AI 8 | SML mô tả "cận trên của biến cố hợp" (1, `chapter_appendix.tex`) |
| uniform convergence | hội tụ đều | đề xuất | "tính chất hội tụ đều" của lớp; "biến cố hội tụ đều" |
| $\epsilon$-representative sample | mẫu $\epsilon$-đại diện | đề xuất | SML nói "mức độ đại diện của dữ liệu" (`01_classification/sec_intro.tex`) |
| confidence interval | khoảng tin cậy | đề xuất; M4AI 14 | |
| law of large numbers | luật số lớn | đề xuất; M4AI 4 | |
| finite class | lớp hữu hạn | SML "lớp hàm phân lớp $\mathcal H$ hữu hạn" (`sec_erm_framework.tex`) | |
| consistent hypothesis | giả thuyết nhất quán với mẫu | đề xuất | $L_S(h)=0$ |

## 7. Bài 03: chiều VC

| English | Thuật ngữ được chọn | Căn cứ | Ghi chú |
|---|---|---|---|
| VC dimension | chiều VC (Vapnik–Chervonenkis dimension) | đề xuất; SML không có | $d$; không dùng $d$ cho số chiều đặc trưng |
| restriction of $\mathcal H$ to $C$ | thu hẹp của $\mathcal H$ lên $C$ | đề xuất | $\mathcal H_C$ |
| labeling | cách gán nhãn | đề xuất | một phần tử của $\{0,1\}^C$ |
| shatter, shattering | tách trọn | đề xuất | "$\mathcal H$ tách trọn $C$" khi $\mathcal H_C$ chứa mọi cách gán nhãn của $C$; loại "phá vỡ" (dịch từng chữ, không nói lên tính chất); câu hỏi mở 6 |
| growth function | hàm tăng trưởng | `ky-hieu.md` | $\Pi_{\mathcal H}(m)$ |
| Sauer–Shelah lemma | bổ đề Sauer–Shelah | tên riêng | |
| threshold, interval | hàm ngưỡng, khoảng | SML "ngưỡng" 13 (`sec_decision_tree.tex`) | |
| linear classifier, affine halfspace | hàm phân lớp tuyến tính, nửa không gian afin | đề xuất | trong $\mathbb R^p$ |
| affinely independent | độc lập afin | đề xuất | |
| Radon's theorem | định lý Radon | tên riêng | |
| symmetrization | đối xứng hóa | đề xuất | |
| ghost sample | mẫu bóng | đề xuất | mẫu $S'\sim D^m$ độc lập với $S$, chỉ dùng trong chứng minh; câu hỏi mở 6 |

## 8. Bài 04: phân tích sai số, SRM và chọn mô hình

| English | Thuật ngữ được chọn | Căn cứ | Ghi chú |
|---|---|---|---|
| error decomposition | phân tích sai số | đề xuất | "sai số" cho các thành phần của phân tích, "lỗi" cho giá trị hàm lỗi |
| approximation error | sai số xấp xỉ | đề xuất | so với rủi ro tham chiếu $L^*$, ghi rõ $L^*$ là gì; SML "lỗi xấp xỉ" 1 (`sec_xgb_applications.tex`) theo nghĩa khác |
| estimation error | sai số ước lượng | đề xuất | |
| optimization error | sai số tối ưu hóa | đề xuất | $\operatorname{opt}_S(\tilde h)=L_S(\tilde h)-\inf_{h\in\mathcal H}L_S(h)$ |
| bias, variance | độ lệch, phương sai | SML 18; 72; M4AI 94 | tham số bias $b$ của mạng nơ-ron gọi là "hệ số tự do" (SML 6), không gọi là "độ lệch"; DL viết "độ chệch" |
| bias–variance decomposition, trade-off | phân tích độ lệch–phương sai, đánh đổi độ lệch–phương sai | đề xuất; M4AI "đánh đổi" | loại "sự tráo đổi giữa độ lệch và phương sai" (SML 1, `05_regression/sec_regression_introduction.tex`): "tráo đổi" nghĩa là đổi chỗ |
| nonuniform learnability | học được không đều | đề xuất | |
| structural risk minimization (SRM) | tối thiểu hóa rủi ro cấu trúc (structural risk minimization, SRM) | đề xuất theo mẫu tên ERM | |
| penalty | số hạng phạt | đề xuất; SML "số hạng" 8 | $p_k$ trong blueprint; cẩn thận: $p$ là số chiều đặc trưng |
| oracle inequality | bất đẳng thức oracle | đề xuất | giữ "oracle" vì chưa có tên tiếng Việt ổn định; câu hỏi mở 6 |
| model selection | chọn mô hình | SML 2; M4AI | |
| training set, validation set, test set | tập huấn luyện, tập xác thực, tập kiểm tra | SML 39; đề xuất (M4AI 90); SML 25 | SML gọi tập dùng để chọn siêu tham số là "tập kiểm thử" (18, `10_ML_in_production/sec_data_preparation.tex`) và tập đánh giá cuối là "tập kiểm tra"; học phần loại "tập kiểm thử" vì dễ hiểu thành tập kiểm tra cuối; câu hỏi mở 4 |
| held-out sample | mẫu xác thực | đề xuất | độc lập với dữ liệu huấn luyện các ứng viên |
| cross-validation | kiểm tra chéo | SML 2 | |
| regularization, regularizer | chính quy hóa, hàm chính quy hóa | đề xuất; `ky-hieu.md` ("hệ số chính quy hóa" $\lambda$); M4AI 209 | SML gọi số hạng $\Omega$ là "hàm điều chỉnh" (12, `05_regression/sec_bias_variance_analysis.tex` 7); loại vì "điều chỉnh" là từ chung (36 lần trong SML); DL "điều chuẩn"; câu hỏi mở 7 |

## 9. Bài 05–06: tối ưu ngẫu nhiên, chính quy hóa và ổn định

| English | Thuật ngữ được chọn | Căn cứ | Ghi chú |
|---|---|---|---|
| convex function, convex set | hàm lồi, tập lồi | SML "hàm lồi" 9, "lồi" 15 (`sec_optimizer.tex` 7) | |
| strongly convex | lồi mạnh | đề xuất; M4AI 198 | |
| gradient | gradient | M4AI, DL; người dùng chốt 2026-10-30 | $\nabla F(w)$; "đạo hàm" chỉ dùng cho đạo hàm theo nghĩa giải tích (đạo hàm riêng, đạo hàm hàm hợp) |
| subgradient, subdifferential | dưới gradient, dưới vi phân | M4AI "dưới gradient" (58); người dùng chốt 2026-10-30 | $g\in\partial f(w)$ |
| Lipschitz, $G$-Lipschitz | liên tục Lipschitz, $G$-Lipschitz | SML 1; M4AI 110 | $G$ cũng là cận của chuẩn gradient ngẫu nhiên |
| smooth, $\beta$-smooth | trơn, $\beta$-trơn | SML "tính trơn" 4, "hàm trơn" 3 (`sec_optimizer.tex`) | gradient $\beta$-Lipschitz; sách viết "trơn theo $L$" |
| gradient descent (GD) | hạ gradient (gradient descent, GD) | M4AI; người dùng chốt 2026-10-30 | loại "xuống đồi bằng đạo hàm" (SML); viết thường giữa câu |
| stochastic gradient descent (SGD) | hạ gradient ngẫu nhiên (stochastic gradient descent, SGD) | M4AI; người dùng chốt 2026-10-30 | sau lần đầu viết SGD; loại "xuống đồi bằng đạo hàm ngẫu nhiên" (SML) |
| projected SGD | SGD có chiếu | `course-plan.md` | |
| stochastic gradient | gradient ngẫu nhiên | người dùng chốt 2026-10-30 | $g_t$, ước lượng không chệch của $\nabla F(w_t)$ khi biết lịch sử |
| projection | phép chiếu | SML "chiếu" 5 (`09_features/sec_pca.tex`) | $\Pi_W$, chiếu Euclid lên tập lồi đóng $W$ |
| step size, learning rate | độ dài bước | M4AI; người dùng chốt 2026-10-30 | $\eta_t$; lần đầu "độ dài bước (step size, còn gọi là tốc độ học)"; loại "bước nhảy" |
| iterate, averaged iterate | điểm lặp, điểm lặp trung bình | đề xuất | $w_t$, $\bar w_T$ |
| iteration | vòng lặp | SML 22 | số vòng lặp $T$ |
| initialization | khởi tạo | SML 51 | |
| mini-batch, batch size | lô nhỏ, kích thước lô | SML "lô" 7 ("lô dữ liệu (batch)", `sec_optimizer.tex`); M4AI 24; DL 3 | $b$ |
| convergence, convergence rate | hội tụ, tốc độ hội tụ | SML 72; 4 | |
| suboptimality | độ chênh tối ưu | đề xuất | $F(\bar w_T)-F(w^\star)$; SML mô tả "độ chênh lệch … so với cực tiểu toàn cục" (`sec_convergence_analysis.tex`) |
| local minimum, global minimum | cực tiểu địa phương, cực tiểu toàn cục | SML 1; 1 (`sec_convergence_analysis.tex`) | |
| stationary point | điểm dừng | đề xuất | $\nabla F(w)=0$; khác "phân bố dừng" của Bài 10 |
| filtration, history | lịch sử | đề xuất; M4AI `lec-05b` | $\mathcal F_t$; kì vọng có điều kiện theo lịch sử |
| regularized ERM | ERM có chính quy hóa | đề xuất | |
| neighboring samples | hai mẫu lân cận | đề xuất | khác nhau đúng một quan sát; không dùng "láng giềng" (SML 15, nghĩa KNN) |
| algorithmic stability, uniform stability | tính ổn định của thuật toán, ổn định đều | đề xuất | SML dùng "ổn định" 35 lần theo nghĩa thông thường; $\beta_m$ |
| expected generalization gap | khoảng cách tổng quát hóa kì vọng | đề xuất | $\mathbb E_S[L_D(A(S))-L_S(A(S))]$ |
| fresh sample | quan sát mới | đề xuất | mỗi bước SGD dùng một quan sát chưa dùng, rút từ $D$ |

## 10. Bài 07–08: mạng nơ-ron, Rademacher và ổn định của SGD

| English | Thuật ngữ được chọn | Căn cứ | Ghi chú |
|---|---|---|---|
| feedforward network | mạng lan truyền tới | SML 16 (`sec_optimizer.tex` 4) | |
| depth, width | độ sâu, độ rộng | SML 5; đề xuất | |
| layer, neuron, activation function | lớp nơ-ron, nơ-ron, hàm kích hoạt | SML 28; 200; 33 | viết "lớp nơ-ron", không viết "lớp" trơn, để khỏi lẫn với "lớp giả thuyết" |
| score function (network output) | hàm điểm số | đề xuất; DL "điểm số" (`lec-02`) | $f(x)$; khác "gradient log" của Bài 10 |
| margin | lề, lề phân lớp | SML "lề" 70 (`08_SVM/sec_soft_margin.tex` 35) | $y f(x)$; tham số $\gamma$ |
| ramp loss | hàm lỗi dốc | đề xuất | bị chặn, $1/\gamma$-Lipschitz |
| contraction lemma | bổ đề co | đề xuất | nêu quy ước định tâm trước khi dùng |
| Rademacher variables | biến Rademacher | tên riêng | nhận $\pm1$ với xác suất bằng nhau |
| Rademacher complexity (empirical, population) | độ phức tạp Rademacher (thực nghiệm, tổng thể) | `ky-hieu.md` | $\widehat{\mathfrak R}_S(\mathcal F)$ |
| loss class | lớp hàm lỗi | đề xuất | $\mathcal G$; cận áp dụng cho lớp hàm lỗi, không tự động cho điểm số mạng |
| norm-bounded class | lớp bị chặn theo chuẩn | đề xuất | |
| overparameterization | quá tham số hóa | đề xuất; M4AI "quá tham số" 1 | luôn nói so với cỡ mẫu và bài toán cụ thể |
| coupled runs | hai lần chạy ghép cặp | đề xuất | cùng khởi tạo, cùng dãy chỉ số |
| nonexpansive | không giãn | đề xuất | |
| co-coercivity | tính đồng bức | đề xuất | |
| early stopping | dừng sớm | SML 1 (`03_cnn/sec_training_strategy.tex`) | |

## 11. Bài 09: mô hình chuỗi và mô hình sinh

| English | Thuật ngữ được chọn | Căn cứ | Ghi chú |
|---|---|---|---|
| sequence | chuỗi | SML 111 | |
| autoregressive factorization | phân tích tự hồi quy | đề xuất; DL "tự hồi quy" 4 | |
| chain rule (of probability) | quy tắc nhân xác suất | đề xuất | không viết "quy tắc chuỗi", dễ lẫn với đạo hàm hàm hợp (SML) |
| likelihood | độ hợp lý | SML 17 (`sec_logistic_regression.tex` 11) | loại "hàm hợp lý" (SML 8, `sec_em.tex`, `sec_parametric_models.tex`) |
| log-likelihood | log độ hợp lý | đề xuất | SML giữ tiếng Anh "log-likelihood" (4) |
| negative log-likelihood | hàm lỗi log (đối của log độ hợp lý) | đề xuất | $-\log q(x)$; phân biệt tổng trên chuỗi với trung bình theo độ dài |
| conditional likelihood | độ hợp lý có điều kiện | đề xuất | |
| maximum likelihood estimation (MLE) | ước lượng hợp lý cực đại (maximum likelihood estimation, MLE) | SML 22 (`11_generative_models/sec_parametric_models.tex` 7) | loại "cực đại độ hợp lý" (SML 1) |
| teacher forcing | học theo đáp án | DL `lec-08`, `lec-11` | thống nhất với DL; "đáp án" ở đây là chuỗi đích, không phải nhãn "Lời giải" của bài tập |
| density estimation | ước lượng mật độ | đề xuất | $Z=X$ |
| generative model | mô hình sinh | SML 26 | |
| latent variable, latent-variable model | biến ẩn, mô hình biến ẩn | SML 15 (`sec_em.tex` 8) | $p_\theta(x,z)$ |
| variational distribution | phân bố biến phân | đề xuất; SML "biến phân" 10 (VAE) | $q_\phi(z\mid x)$ |
| Kullback–Leibler divergence | phân kì Kullback–Leibler (Kullback–Leibler divergence, KL) | đề xuất | SML viết "khoảng cách Kullback–Leibler", "khoảng cách KL" (14, `sec_generator.tex`, `sec_parametric_models.tex`); loại vì KL không đối xứng và không thỏa bất đẳng thức tam giác; câu hỏi mở 5 |
| forward KL | phân kì KL thuận | đề xuất | $\mathrm{KL}(p\,\Vert\,q)$ với $p$ là phân bố thật |
| evidence | bằng chứng | SML (`sec_em.tex`) | $\log p_\theta(x)$ |
| evidence lower bound (ELBO) | cận dưới bằng chứng (evidence lower bound, ELBO) | SML 4 (`sec_em.tex`) | |
| reparameterization | tái tham số hóa | đề xuất | $z=\mu_\phi(x)+\sigma_\phi(x)\odot\varepsilon$ |
| pathwise gradient estimator | ước lượng gradient theo đường đi | đề xuất | nêu điều kiện cho phép đổi đạo hàm và kì vọng |

## 12. Bài 10: gradient chính sách và học liên tục

| English | Thuật ngữ được chọn | Căn cứ | Ghi chú |
|---|---|---|---|
| agent, state, action | tác tử, trạng thái, hành động | SML 45; 222; 124 | |
| policy | chính sách | SML 133 | $\pi_\theta(a\mid s)$ |
| trajectory, episode, horizon | quỹ đạo, lượt, độ dài lượt | SML 12; đề xuất; đề xuất | $\tau$, $H$ |
| reward, return | phần thưởng, tổng phần thưởng | SML 37; 6 | loại "giá trị trả về" (SML 2) |
| reward-to-go | tổng phần thưởng từ bước $t$ | SML "tổng phần thưởng trả về từ bước $t$" (`sec_deep_rl.tex`) | $G_t=\sum_{u=t}^{H-1}r_u$ |
| discount factor | hệ số chiết khấu | SML 4 | |
| policy gradient | gradient chính sách | người dùng chốt 2026-10-30; khớp họ gradient | loại "đạo hàm chính sách" (SML 5) và "tối ưu chính sách (Policy Gradient)" (SML 3) |
| score function $\nabla_\theta\log p_\theta$, score identity | gradient log, đồng nhất thức gradient log | đề xuất | không gọi là "điểm số" (đã dùng ở Bài 07) |
| REINFORCE | thuật toán REINFORCE | tên riêng | loại "thuật toán tối ưu tăng cường" (SML, `sec_policy_gradient.tex`) |
| baseline | giá trị nền | đề xuất | $b_t(S_t)$; "đường cơ sở" chỉ dùng cho phương pháp đối chứng trong thực nghiệm; câu hỏi mở 6 |
| advantage | hàm lợi ích | SML 2 | $A(s,a)=Q(s,a)-V(s)$ |
| on-policy | đi theo chính sách | SML 7 | |
| stationary distribution | phân bố dừng | SML 6 | |
| Monte Carlo | Monte Carlo | tên riêng | SML viết "Monte-Carlo" (5); không gạch nối |
| regret | hối tiếc | đề xuất | phân biệt với rủi ro vượt mức và độ quên |
| continual learning | học liên tục | đề xuất | |
| task | nhiệm vụ | SML 65 (nghĩa chung) | $D_1,\ldots,D_K$ |
| catastrophic forgetting, forgetting measure | quên thảm họa, độ quên | đề xuất | ghi rõ quy ước đo (đỉnh đến cuối) |
| forward transfer, backward transfer | chuyển đổi xuôi, chuyển đổi ngược | theo SML "học chuyển đổi" 13 (`03_cnn/sec_training_strategy.tex` 7) | |
| replay, parameter regularization | phát lại, chính quy hóa tham số | đề xuất | |
| stability–plasticity trade-off | đánh đổi bền vững–mềm dẻo | đề xuất | không dùng "ổn định" ở đây; "ổn định" dành cho tính ổn định của thuật toán (Bài 06, 08) |
| evaluation matrix, final average accuracy | ma trận đánh giá, độ chính xác trung bình cuối cùng | đề xuất | $a_{t,i}$, $K^{-1}\sum_i a_{K,i}$ |
| memory budget, task identity | ngân sách bộ nhớ, định danh nhiệm vụ | đề xuất | |

## 13. Chính tả

Chi tiết ở `van-phong.md` mục 12. Tóm tắt: "kì vọng", "bất kì", "tỉ lệ", "phân kì", "kí hiệu" theo SML; "lý thuyết", "định lý", "hợp lý", "kỹ thuật"; dấu thanh kiểu mới ("hóa", "thỏa"); "véc-tơ", "nơ-ron", "mô-men" có gạch nối.

## 14. Quyết định của người dùng (2026-10-30)

1. **$L_D(h)$** gọi là "rủi ro kì vọng" (theo sách), không dùng "rủi ro tổng thể".
2. **Chính tả** "kí hiệu" (theo sách, đồng bộ với "kì vọng"); tên tệp `ky-hieu.md` giữ nguyên.
3. **Thuật ngữ mới cho Bài 01** được chấp nhận: giả thuyết, lớp giả thuyết, khả thực, bất khả tri, thiên kiến quy nạp, rủi ro vượt mức, khoảng cách tổng quát hóa.
4. **Họ gradient** theo các học phần anh em: gradient, hạ gradient, hạ gradient ngẫu nhiên, dưới gradient, gradient chính sách, độ dài bước.
5. **Hàm dự đoán** (theo sách) cho predictor; điều phối viên đã sửa `ky-hieu.md`.

Còn mở, quyết định khi đến bài tương ứng: "tập xác thực" hay "tập kiểm thử" của sách (Bài 04); "phân kì KL" hay "khoảng cách KL" của sách (Bài 09); "chính quy hóa" hay "hàm điều chỉnh" của sách (Bài 04–06); các từ mới "tách trọn", "mẫu bóng", "bất đẳng thức oracle" (Bài 03–04) và "giá trị nền" (Bài 10).
