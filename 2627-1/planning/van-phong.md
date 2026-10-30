# Văn phong ghi chú bài giảng

Tệp nội bộ cho người viết và người rà soát ghi chú, bài tập của học phần Lý thuyết học thống kê. Không liên kết từ trang chỉ mục. Lập ngày 2026-10-30 theo yêu cầu của người dùng: văn phong theo giáo trình *Học máy thống kê* của tác giả (`../SML-textbook-main.zip`). Thuật ngữ nằm ở `thuat-ngu.md`, kí hiệu ở `ky-hieu.md`.

## 1. Phạm vi và thứ tự ưu tiên

Sách là mẫu về cách viết và cách gọi tên, không phải nguồn nội dung. Không lấy định lý, ví dụ, số liệu hay kí hiệu của sách vào ghi chú; nội dung lấy từ UML và `sources/blueprint.md`. Các tệp đã đọc để rút ra hướng dẫn này: chương mở đầu (`00_intro/sec_types_of_ML`), chương 1 (`chapters/01_classification/`: `sec_intro`, `sec_classification_definition`, `sec_statistical_learning`, `sec_erm_framework`, `sec_minimize_risk_classifier`, `sec_nearest_neighbor`, `sec_conclusion`), chương 2 (`sec_optimizer`, `sec_convergence_analysis`, `sec_training_mlp`), chương mô hình sinh (`sec_em`), chương học tăng cường (`sec_policy_gradient`, `sec_deep_rl`), chương hồi quy (`sec_regression_introduction`) và `chapter_appendix.tex`.

Khi thói quen của sách khác quy tắc viết, quy tắc thắng theo thứ tự: chỉ thị của người dùng, `../CLAUDE.md` mục "Writing course content" và `CLAUDE.md` của học phần (mục "Voice", "Statistical learning theory standards"), rồi đến văn phong của sách. Kỹ năng `no-ai-slop` bắt buộc cho mọi văn bản; khi lời khuyên về giọng văn của nó va chạm với văn phong học thuật hoặc độ chính xác toán học, văn phong học thuật thắng. Mục 13 liệt kê các thói quen của sách bị loại vì lý do này.

Các trích đoạn dưới đây là nguyên văn, chỉ bỏ lệnh LaTeX (`\emph`, `\index`, `\ref`) và viết lại macro riêng của sách bằng lệnh chuẩn; `[…]` đánh dấu chỗ lược.

## 2. Mở một mục: nhu cầu trước công cụ

Sách mở mục bằng điều mà kết quả trước chưa làm được, rồi mới đưa công cụ mới. Câu đầu nhắc lại đối tượng đã có bằng tên riêng của nó, câu sau nói cái còn thiếu.

> Định nghĩa […] đã cho thấy nhiệm vụ cần phải giải quyết của bài toán phân lớp nhưng chưa làm rõ làm thế nào để đánh giá độ "tốt" của mô hình phân lớp $h$ một cách định lượng. […] Để giải quyết vấn đề này, chúng ta có thể tiếp cận bài toán phân lớp qua lăng kính của ngành xác suất thống kê. (`sec_statistical_learning.tex`)

Một dạng khác là đi từ đại lượng lý tưởng sang đại lượng tính được, với "Do đó" nối hai câu:

> Trên thực tế, nói chung ta không biết chính xác phân bố $\mathcal{P}$ của dữ liệu mà chỉ biết tập dữ liệu $D$ được giả sử lấy mẫu từ phân bố này. Do đó, đại lượng $\mathrm{err}_{\mathcal P}(h)$ không thể tính được mà phải ước lượng thông qua tập dữ liệu $D$. (`sec_statistical_learning.tex`)

Trong `sec_em.tex`, ví dụ hai đồng xu kết thúc bằng chính cái khó cần giải quyết, và mục con kế tiếp (cận dưới bằng chứng) trả lời cái khó đó:

> Cực đại hoá đại lượng trên không hề dễ dàng mà thường chúng ta phải sử dụng một đại lượng thay thế (cận dưới) dễ tính hơn để cực đại hoá. (`sec_em.tex`)

Quy định cho học phần:

- Câu đầu của mỗi mục nêu bài toán hoặc giới hạn của kết quả trước bằng đối tượng toán học cụ thể. Ví dụ cách viết: "Định lý 02.2 chặn $\lvert L_S(h)-L_D(h)\rvert$ cho một giả thuyết $h$ được chọn trước khi lấy mẫu. Thuật toán ERM chọn $\hat h$ sau khi thấy $S$, nên chúng ta cần một cận đúng đồng thời cho mọi $h\in\mathcal H$."
- Không mở mục bằng câu hỏi tu từ, bằng "Mục này…", "Trong phần này…" hay bằng lời giới thiệu tầm quan trọng của chủ đề.

## 3. Định nghĩa: khung trước, đọc từng phần sau

Sách đặt định nghĩa trong khung có tên là một cụm danh từ (`frameddefn[Bài toán phân lớp thống kê]`), mở bằng "Cho …" để liệt kê đối tượng. Ngay sau khung, sách đọc lại từng thành phần: câu "Trong đó …" giải thích biến cố hay đại lượng vừa dùng, rồi một đoạn so sánh với định nghĩa trước.

> Điểm khác của Định nghĩa […] so với Định nghĩa […] là các mẫu dữ liệu $(x, y)$ được lấy mẫu theo một phân bố xác suất $\mathcal P$ nhất định. Định nghĩa […] cho phép mô tả sự không chắc chắn của nhãn $y$ trong bài toán phân lớp, khác với Định nghĩa […] nhãn $y$ được xác định hoàn toàn bởi hàm mục tiêu $f(x)$. (`sec_statistical_learning.tex`)

Tên gọi mới được đưa vào bằng "Ta gọi … là …" hoặc "… được gọi là …", thuật ngữ in nghiêng, tiếng Anh trong ngoặc.

Quy định cho học phần:

- Dùng khối `::: definition Định nghĩa NN.k (Tên)`; tên là cụm danh từ. Thân định nghĩa mở bằng "Cho …", phát biểu bằng "Ta nói … nếu …" hoặc "… được gọi là …". Không dùng "hãy" trong định nghĩa (sách có, xem mục 13).
- Thuật ngữ đang được định nghĩa in nghiêng một lần, kèm tiếng Anh trong ngoặc ở lần đầu trong ghi chú.
- Đoạn ngay sau khối định nghĩa đọc lại từng phần: đại lượng nào cố định, đại lượng nào ngẫu nhiên và ngẫu nhiên theo phân bố nào, thứ tự lượng từ, định nghĩa này khác định nghĩa trước ở điểm nào. Sau đó là ví dụ và phản ví dụ (thành phần 7 của blueprint mục A).

### 3a. Định nghĩa và phát biểu có nhiều thành phần (yêu cầu của người dùng, 2026-10-30)

Khi một định nghĩa, mệnh đề hay định lý có từ ba thành phần hoặc giả thiết trở lên, viết một câu dẫn ngắn rồi liệt kê từng thành phần bằng gạch đầu dòng, mỗi dòng mở bằng một nhãn in đậm ngắn ("**Tập quan sát:**", "**Chọn trước:**", "**Chưa biết:**", "**Dữ liệu:**", "**Mục tiêu:**"…). Không dồn các giả thiết vào một đoạn văn dài. Đoạn đọc sau định nghĩa không nhắc lại những gì danh sách đã nêu. Mẫu: Định nghĩa 01.5 (Bài toán học thống kê) của Bài 01. Các dòng phải **song song** (góp ý của người dùng): mọi nhãn là tên của một thành phần (danh từ, không dùng cụm động từ hay cụm chỉ thời điểm như "Chọn trước khi lấy mẫu"), và mọi dòng có cùng khuôn nội dung, chẳng hạn kí hiệu, mô tả, rồi vai trò (cố định, chọn trước, chưa biết, quan sát được, cần đạt). Không mở một dòng bằng động từ ("Cần chọn …") khi các dòng khác mở bằng kí hiệu.

## 4. Công thức nằm trong câu văn

Sách dẫn vào công thức bằng một câu nói rõ sắp viết gì ("Xác suất này được định nghĩa theo công thức sau:", "như sau:"), và sau công thức gọi tên kí hiệu mới bằng "trong đó" hoặc "với". Trong sách, "như sau:" xuất hiện 104 lần, "trong đó" 143 lần.

> Ta gọi xác suất của sự kiện phân lớp sai là xác suất lỗi, tỉ lệ lỗi hay rủi ro kì vọng của mô hình phân lớp $h$. Xác suất này được định nghĩa theo công thức sau: (`sec_statistical_learning.tex`)

Câu dẫn thứ hai là mẫu cần theo; câu thứ nhất gộp ba tên cho một đại lượng, điều học phần tránh (mục 13).

> trong đó, tổng trên $Z$ được tính theo mọi khả năng có thể có của biến ẩn $Z$ (do ta không biết $Z$). (`sec_em.tex`)

Trong chứng minh, sách ghi lý do của từng bước, hoặc trong câu sau công thức, hoặc ngay trên dòng biến đổi (`\textrm{[do ERM]}` trong `sec_erm_framework.tex`):

> Trong đó, bất đẳng thức cuối cùng do $\eta \leq \frac{1}{L}$, nên $1 - \frac{L \eta}{2} \geq \frac{1}{2}$. (`sec_optimizer.tex`)

Quy định cho học phần:

- Mỗi công thức hiển thị có một câu dẫn; công thức là một phần của câu, không đứng trơ trọi giữa hai đoạn.
- Ngay sau công thức, "trong đó" gọi tên mọi kí hiệu xuất hiện lần đầu, kèm miền giá trị (ví dụ "$\ell$ nhận giá trị trong $[0,1]$"). Kí hiệu theo `ky-hieu.md`, không theo sách.
- Chuỗi biến đổi viết trong `aligned`, mỗi dòng một quan hệ. Lý do của từng bước đặt ở câu sau ("Bất đẳng thức thứ nhất do …, bất đẳng thức thứ hai do …") hoặc trên dòng bằng `\text{(do ERM)}`, `\text{(bất đẳng thức Hoeffding)}`.
- "Ta có" chỉ đứng sau lý do: "Theo bất đẳng thức hợp, ta có …", không viết chuỗi "Ta có: … Ta có: …".

## 5. "Chúng ta" và "ta"

Sách dùng "chúng ta" (334 lần) khi nói về hướng đi, nhu cầu và giới hạn của trình bày, và "ta" đứng riêng (565 lần, không tính "chúng ta"; riêng "ta có" 314 lần) bên trong tính toán và khi đặt tên.

> Chúng ta không đi sâu vào vấn đề hội tụ của thuật toán tối ưu xuống đồi bằng đạo hàm với trường hợp mạng nơ-ron có cấu trúc phức tạp hơn. (`sec_optimizer.tex`)

Quy định cho học phần, giống quy định trong `CLAUDE.md`: "chúng ta" cho kế hoạch, nhu cầu, giới hạn ("chúng ta cần một cận đúng đồng thời cho mọi $h$"); "ta" trong phép tính và khi đặt tên ("Thay $h=\hat h$, ta được …", "Ta gọi $L_S(h)$ là …"). Không dùng "chúng tôi", "bạn đọc", "người đọc", "chúng ta hãy".

## 6. Nối đoạn và từ nối

Đoạn mới trong sách thường mở bằng tên của đối tượng vừa xây dựng: "Định lý […] cho thấy …", "Đại lượng $\widehat{\mathrm{err}}_{D}(h)$ ở công thức […] được gọi là …". Cách nối này giữ mạch bằng nội dung, không cần "Tiếp theo" hay "Bây giờ".

Từ nối thường gặp trong sách (số lần, đã bỏ chú thích): "trong đó" 143, "cụ thể" 75, "xét" 73, "giả sử" 65, "như vậy" 60, "tuy nhiên" 59, "tức là" 59, "do đó" 43, "khi đó" 40, "nghĩa là" 31, "từ đó" 23, "suy ra" 12, "bên cạnh đó" 10. Cách dùng trong học phần:

| Từ nối | Dùng khi | Không dùng khi |
|---|---|---|
| Xét, Giả sử | mở một trường hợp, cố định giả thiết | giả thiết đã nêu ở hộp "Giả thiết." |
| Khi đó | rút ra điều đúng dưới giả thiết vừa đặt | nối hai ý không phụ thuộc nhau |
| Do đó, Suy ra | hệ quả logic có lý do ngay trước | lý do nằm xa hoặc chưa nêu |
| Như vậy | khép một chuỗi biến đổi bằng điều vừa chứng minh | mở đoạn tóm tắt lặp lại cả mục |
| Tuy nhiên | nêu giới hạn hay chỗ kết quả không áp dụng | làm từ đệm giữa hai câu cùng chiều |
| Tức là, Nghĩa là | đọc công thức bằng lời, thêm thông tin | nhắc lại đúng câu trước |
| Hay nói cách khác | đưa ra dạng tương đương khác hẳn, ví dụ từ dạng $\epsilon$ sang dạng cỡ mẫu (sách dùng đúng như vậy trong `sec_erm_framework.tex`) | diễn đạt lại ý đã rõ |
| Bên cạnh đó | thêm một điều kiện hay sự kiện độc lập | chất nhiều câu không liên quan |

## 7. Ví dụ

Khối ví dụ của sách có tên là cụm danh từ (`expl[Hai đồng xu]`, `expl[Phân loại thư rác theo tiêu đề]`). Câu đầu cố định thiết lập rồi mới tính: ví dụ thư rác mở bằng "Khi $\mathcal{X}$ là tập các tiêu đề thư điện tử, $\mathcal{Y}=\{\ldots\}$" (`00_intro/sec_types_of_ML.tex`), ví dụ hai đồng xu mở bằng xác suất ra mặt ngửa của từng đồng xu và cách chọn đồng xu (`sec_em.tex`). Ví dụ cụ thể đứng trước định nghĩa tổng quát mà nó dẫn tới: hai đồng xu đứng trước cận dưới bằng chứng.

Sau một định lý, sách đọc kết quả bằng số:

> Ví dụ, nếu $\epsilon = 1\%, n = 100000$, tỉ lệ lỗi trung bình trên 100.000 mẫu dữ liệu là $10\%$ thì tỉ lệ lỗi thực tế nằm trong khoảng $[10\%\pm 1\%]$ với xác suất không thấp hơn $1 - 2e^{-20}\approx 1 - 4.10^{-9}$, tức là gần bằng 1. (`sec_erm_framework.tex`)

Quy định cho học phần:

- Dùng `::: example Ví dụ NN.k (Tên danh từ)`. Câu đầu nêu $\mathcal X$, $\mathcal Y$, phân bố $D$ (hoặc giả thiết về nó), lớp $\mathcal H$, hàm lỗi $\ell$ và cỡ mẫu $m$, và nói đại lượng nào ngẫu nhiên.
- Ví dụ có số cụ thể, tính đến cùng. Câu cuối nói ví dụ chứng tỏ điều gì về kết quả (ví dụ, với $\lvert\mathcal H\rvert=100$, $\delta=0{,}05$, $\epsilon=0{,}1$: "cận bất khả tri đòi hỏi $m\ge 1659$, còn cận khả thực chỉ cần $m\ge 77$"), không viết "ví dụ trên cho thấy tầm quan trọng của …".
- Ví dụ không chứa "hãy"; viết "Cần ước lượng …" hoặc "Bài toán là ước lượng …".
- Sau mỗi định lý chính có một cách đọc bằng số như trích đoạn trên, với giá trị $\epsilon$, $\delta$, $m$ cụ thể.

## 8. Kết thúc một mục

Mục trong sách thường kết thúc bằng ý nghĩa hoặc cái giá của kết quả cuối cùng:

> Với $k > 1$ càng lớn thì $\mathrm{err}_{\mathcal P}(h_{\mathrm{KNN}})$ càng tiến đến sát $R^\star$. Đây là một kết quả thú vị nhưng nó đòi hỏi số mẫu huấn luyện $n$ rất lớn so với $k$. (`sec_nearest_neighbor.tex`)

Học phần giữ cách kết thúc này và bỏ lời đánh giá ("thú vị"): câu cuối nêu giới hạn bằng đại lượng cụ thể. Một giới hạn cũng có thể viết thành phép bỏ giả thiết, như `sec_optimizer.tex` làm sau định lý hội tụ: khi mạng có từ hai lớp nơ-ron trở lên, hàm lỗi không còn lồi, nên cận hội tụ vừa chứng minh không còn áp dụng.

Quy định cho học phần:

- Mục kết thúc bằng văn xuôi: một hệ quả cho việc học, hoặc một giới hạn (giả thiết nào không còn, đại lượng nào cận không kiểm soát). Không có nhãn "Kết mục", "Chuỗi suy luận", không có đoạn tóm tắt lặp lại mục.
- Cầu nối sang bài sau chỉ nằm ở thành phần "Câu hỏi cuối buổi và cầu nối", và nêu câu hỏi chưa giải quyết bằng đối tượng cụ thể (ví dụ: lớp nửa không gian vô hạn, cận của Định lý 02.3 phụ thuộc $\log\lvert\mathcal H\rvert$).

## 9. Độ dài câu và đoạn

Đo trên bảy tệp (`sec_statistical_learning`, `sec_erm_framework`, `sec_minimize_risk_classifier`, `sec_optimizer`, `sec_em`, `sec_regression_introduction`, `sec_policy_gradient`), sau khi thay công thức bằng một từ: 259 câu, trung vị 23 tiếng, trung bình 24 tiếng, 90% số câu không quá 39 tiếng; 106 đoạn, trung vị 2 câu, 90% số đoạn không quá 4 câu. Đoạn trong sách ngắn vì công thức hiển thị thường cắt đoạn.

Quy định cho học phần: câu khoảng 15–35 tiếng; tách câu dài hơn khoảng 40 tiếng hoặc có hơn hai mệnh đề phụ. Đoạn 2–4 câu, mỗi đoạn một khẳng định. Không cố làm mọi câu dài bằng nhau; câu ngắn dùng để chốt một kết luận.

### 9a. Câu thẳng, không lắt léo (yêu cầu của người dùng, 2026-10-30)

Mỗi câu nói thẳng điều cần nói, theo thứ tự chủ thể – hành động – đối tượng. Người dùng nêu ví dụ cần sửa: "Một câu trả lời hấp dẫn nhưng sai cho rằng hai hàm tốt như nhau, vì cả hai đều không sai trên mẫu" → "Hai hàm có tốt như nhau vì đều phân lớp hoàn hảo trên mẫu huấn luyện không?". Các dạng lắt léo cần sửa:

- **Bọc ý trong lời thuật lại**: "một câu trả lời … cho rằng …", "có ý kiến cho rằng …", "điều này cho thấy rằng …", "người ta có thể nghĩ rằng …". Viết thẳng mệnh đề, hoặc hỏi thẳng.
- **Phủ định kép hoặc phủ định vòng**: "không sai trên mẫu" (→ "phân lớp đúng mọi quan sát của mẫu"), "không phải là không …", "không thể không …", "chưa hẳn không …".
- **Danh từ hóa thay cho động từ**: "việc thực hiện tính toán", "sự phụ thuộc của … vào …" khi viết được "tính", "… phụ thuộc vào …".
- **Chủ thể trừu tượng làm việc của người hoặc của toán tử**: "định nghĩa đòi hỏi", "ví dụ đọc", "bất đẳng thức nói rằng" khi viết được thẳng điều đúng.
- **Cấu trúc đảo, rào đón, vòng vo**: "Điều mà … là …", "Chính … mới là …", "không phải … mà là …" khi không có đối lập thật; nhiều mệnh đề phụ lồng nhau trước động từ chính.
- **Câu chuyển ý mơ hồ**: một câu chỉ để báo rằng sắp có ý khác. Nói luôn ý đó.

Câu hỏi được phép khi nó là câu hỏi thật và được trả lời ngay trong bài (câu hỏi mở đầu, câu hỏi cuối buổi, câu hỏi dẫn vào một mục mà mục đó trả lời). Câu hỏi thẳng tốt hơn lời thuật lại một quan niệm sai. Câu hỏi tu từ (không cần trả lời, hoặc không được trả lời) vẫn bị cấm.

## 10. Thuật ngữ tiếng Anh và chữ viết tắt

Sách in nghiêng thuật ngữ tiếng Việt và đặt tiếng Anh viết thường trong ngoặc: "*tỉ lệ lỗi* (error rate)", "*rủi ro thực nghiệm* (empirical risk)". Học phần giữ cách này. Với chữ viết tắt, sách không thống nhất: "(Empirical Risk Minimization - ERM)", "(evidence lower bound - ELBO)", "SGD (Stochastic Gradient Descent)", "MLE (Maximum Likelihood Estimation)".

Định dạng của học phần:

- Lần đầu trong mỗi ghi chú: tên tiếng Việt đầy đủ, rồi trong ngoặc tên tiếng Anh viết thường, dấu phẩy, chữ viết tắt: "tối thiểu hóa rủi ro thực nghiệm (empirical risk minimization, ERM)". Những lần sau dùng chữ viết tắt hoặc tên tiếng Việt, không nhắc lại tiếng Anh.
- Tên riêng giữ nguyên và viết hoa: Hoeffding, Markov, Chebyshev, Chernoff, Rademacher, Bayes, Kullback–Leibler, Vapnik–Chervonenkis (VC), Sauer–Shelah, REINFORCE. Tên ghép hai người và cặp đối lập dùng gạch nối ngắn (–): "bổ đề Sauer–Shelah", "đánh đổi độ lệch–phương sai".
- Tên lĩnh vực và tên phương pháp viết thường giữa câu: "học máy", "tối thiểu hóa rủi ro thực nghiệm", "hạ gradient" (sách viết hoa "Học máy", "nguyên tắc Tối thiểu hóa rủi ro thực nghiệm").
- Khi có hai tên cho một khái niệm: `X (còn gọi là Y)` ở lần đầu, chỉ `X` về sau. Danh sách tên chọn và tên loại ở `thuat-ngu.md`.

## 11. Phát biểu kết quả và chứng minh

Sách đặt tên định lý bằng cụm danh từ ("Xấp xỉ rủi ro kì vọng bằng rủi ro thực nghiệm"), mở thân định lý bằng "Xét … cố định, nếu … thì với mọi …", và đưa thêm dạng tương đương bằng "Hay nói cách khác, với mọi giá trị $\epsilon, \delta>0$, với xác suất không thấp hơn $1-\delta$ …". Chứng minh mở bằng công cụ ("Áp dụng định lý Hoeffding với $X_i = \mathbb I[h(x_i) \neq y_i]$ …"), và sau định lý là một câu "Định lý […] cho thấy …" kèm ví dụ số.

Học phần giữ các thói quen đó và thêm các yêu cầu của `CLAUDE.md`:

- Tên khối mang số, tên và độ sâu chứng minh: `::: theorem Định lý 02.3 (Hội tụ đều cho lớp hữu hạn) — chứng minh đầy đủ`. Vai trò đúng nhãn: Bổ đề là công cụ, Mệnh đề là sự kiện tập trung, Định lý là kết quả chính, Hệ quả là suy ra trực tiếp.
- Hai dòng in đậm "**Giả thiết.**" (không gian xác suất, cơ chế lấy mẫu, hàm lỗi và miền giá trị, lớp giả thuyết, cái gì cố định, cái gì ngẫu nhiên) và "**Bảo đảm.**" (theo kì vọng hay với xác suất cao; đại lượng thực nghiệm hay tổng thể; phụ thuộc vào $m$, số chiều, số vòng lặp, $\delta$, chuẩn). Điều kiện về cỡ mẫu đứng trong "Bảo đảm.", tách khỏi giả thiết về phân bố.
- Cụm "với xác suất ít nhất $1-\delta$" là cách nói chuẩn của học phần cho cận xác suất cao (người dùng chốt 2026-10-30; sách viết "không thấp hơn" 4 lần, không dùng); ghi rõ xác suất lấy theo $S\sim D^m$.
- Chứng minh mở bằng một câu lộ trình, gọi tên bất đẳng thức then chốt, đánh dấu chỗ dùng từng giả thiết, kết thúc bằng $\square$ và một câu nói kết quả có nghĩa gì cho việc học. Học phần không dùng "ta có điều phải chứng minh" làm câu cuối.

## 12. Chính tả và trình bày số

- Theo đa số trong sách: "kì vọng" (46 lần, "kỳ vọng" 9), "bất kì" (24, "bất kỳ" 5), "tỉ lệ" (36, "tỷ lệ" 3). Các từ sách viết với "y" giữ nguyên: "lý thuyết", "định lý", "hợp lý", "xử lý", "kỹ thuật".
- "Kí hiệu" viết theo sách ("kí hiệu" 12 lần, "ký hiệu" 2), người dùng chốt 2026-10-30; tên tệp `ky-hieu.md` giữ nguyên.
- Dấu thanh theo kiểu mới: "hóa", "thỏa", "hòa" (sách lẫn lộn: "hoá" 206, "hóa" 139; tệp của học phần và workspace đều dùng "hóa").
- Từ mượn có gạch nối như sách: "véc-tơ" (97 lần), "nơ-ron" (200), "mô-men".
- Số thập phân dùng dấu phẩy, trong KaTeX viết `0{,}05`; số lớn tách nhóm bằng dấu chấm trong văn bản ("100.000") hoặc viết lũy thừa trong công thức ($10^{5}$). Không viết "4.10^{-9}" như sách; viết $4\cdot10^{-9}$.

## 13. Khác biệt cần tránh

Các thói quen sau có trong sách nhưng bị quy tắc của học phần loại. Người viết không bắt chước chúng dù sách là mẫu văn phong.

| Thói quen trong sách | Ví dụ (tệp) | Quy tắc loại | Cách viết trong học phần |
|---|---|---|---|
| "Hãy" trong định nghĩa và ví dụ | "hãy tìm một mô hình phân lớp $h$ …" trong khung định nghĩa (`sec_statistical_learning.tex`, `sec_classification_definition.tex`); "Hãy ước lượng bộ tham số …" trong ví dụ (`sec_em.tex`) | `CLAUDE.md` học phần: không "hãy" ngoài đề bài tập | "Bài toán phân lớp thống kê là tìm $h$ sao cho …"; "Cần ước lượng …" |
| Câu hỏi tu từ | "Giả thiết này có thật sự không thực tế?", mở mục bằng "Xấp xỉ … bằng … tốt đến mức nào?" (`sec_erm_framework.tex`); "Câu hỏi đầu tiên đặt ra … là ``Hàm phân lớp $h^\star(x)$ nào là hàm phân lớp tối ưu?''" (`sec_minimize_risk_classifier.tex`) | `../CLAUDE.md`: cấm câu hỏi tu từ | Phát biểu bài toán hoặc khẳng định. Ngoại lệ: "Câu hỏi mở đầu", "Câu hỏi ôn nhanh", "Câu hỏi cuối buổi" là câu hỏi thật mà học viên phải trả lời |
| Văn bản làm chủ ngữ, câu dẫn đường | "Trong mục này, chúng ta sẽ tìm hiểu về …" (`sec_minimize_risk_classifier.tex`); "Chương … tập trung vào …" (`sec_intro.tex`); "Trong phần này, chúng tôi sẽ đề cập đến …" (`sec_policy_gradient.tex`) | `CLAUDE.md` học phần: văn bản không làm chủ ngữ; `no-ai-slop`: lời dẫn đường | Mở bằng bài toán (mục 2) |
| "Chúng tôi" | `sec_policy_gradient.tex`, `preface.tex` | Mục "Voice" | "chúng ta" cho kế hoạch, hoặc câu không chủ ngữ người |
| Khen, phóng đại | "một trong những kết quả quan trọng nhất trong Học máy" (`sec_erm_framework.tex`); "một thuật toán nổi tiếng" (`sec_training_mlp.tex`); "một kết quả thú vị" (`sec_nearest_neighbor.tex`) | `../CLAUDE.md`: cấm lời khen, ngôn ngữ quảng bá | Nói kết quả bảo đảm gì và không bảo đảm gì |
| Nhiều tên cho một khái niệm | "xác suất lỗi, tỉ lệ lỗi hay rủi ro kì vọng" trong một câu (`sec_statistical_learning.tex`); "phân bố" và "phân phối" trong cùng mục (`sec_em.tex`); "cực tiểu hóa" và "tối thiểu hóa" trong cùng đoạn (`sec_erm_framework.tex`) | Mỗi thuật ngữ một nghĩa; `X (còn gọi là Y)` một lần | Một tên theo `thuat-ngu.md` |
| Từ chêm thay cho lý do | "Dễ thấy, do …" (`sec_minimize_risk_classifier.tex`); "Tất nhiên, còn có …" (`sec_training_mlp.tex`); "rõ ràng" (7 lần trong sách) | Mọi bước phải có lý do; `no-ai-slop`: lời bình chen ngang | Bỏ từ chêm, giữ lý do: "Do …, nên …" |
| Khẳng định không nguồn | "Trong thực hành, người ta thường sử dụng …" (`sec_optimizer.tex`); "Đây cũng là một trong các lý do tại sao Học máy lại cần nhiều dữ liệu …" (`sec_erm_framework.tex`) | `../CLAUDE.md`: không thêm điều không có căn cứ; `no-ai-slop`: quy cho "người ta" | Dẫn nguồn trong UML hoặc nguồn bổ sung đã duyệt, hoặc bỏ |
| Đoạn tổng kết lặp lại chương | "Tổng kết chương" (`01_classification/sec_conclusion.tex`) kể lại các khái niệm đã trình bày | `no-ai-slop`: kết bằng tóm tắt; `CLAUDE.md`: kết mục bằng văn xuôi | Kết bằng hệ quả hoặc giới hạn (mục 8) |
| Gạch đầu dòng cho lập luận | Danh sách hướng nghiên cứu và lưu ý (`sec_convergence_analysis.tex`); hai vấn đề của GD (`sec_optimizer.tex`) | `no-ai-slop`: gạch đầu dòng thay cho văn xuôi | Lập luận viết thành đoạn; danh sách chỉ cho giả thiết, bước thuật toán, liệt kê thật sự |
| Định lý đặt trong khung định nghĩa, "Chứng minh:" là chữ thường | "Định lý đạo hàm chính sách" trong `frameddefn`, tiếp theo "Chứng minh:" (`sec_policy_gradient.tex`) | Cấu trúc khối của học phần | `::: theorem` và `::: proof` |
| Viết tắt trước, tiếng Anh viết hoa, gạch ngang trong ngoặc | "SGD (Stochastic Gradient Descent)", "(Empirical Risk Minimization - ERM)" | `../CLAUDE.md`: tiếng Việt đầy đủ trước | Định dạng ở mục 10 |
| Kí hiệu của sách | $\mathcal P$ cho phân bố, $D$ cho tập dữ liệu, $n$ cho cỡ mẫu, $\mathrm{err}_{\mathcal P}$, $h_D$ | `ky-hieu.md` | $D$, $S$, $m$, $L_D$, $L_S$, $A(S)$, $\hat h$ |
| "Mẫu dữ liệu", "mẫu huấn luyện" cho một điểm dữ liệu | "mỗi giá trị $(x_i, y_i)$ được gọi là mẫu huấn luyện" (`sec_classification_definition.tex`) | Học phần dùng "mẫu" cho cả $S$ | "quan sát $z_i$"; "mẫu huấn luyện $S$" |

## 14. Danh sách kiểm tra cho người rà soát

Người rà soát dùng `no-ai-slop` ở chế độ Detect cùng danh sách này; mỗi phát hiện ghi theo mẫu `mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa`.

1. Câu đầu của mỗi mục nêu một bài toán hay giới hạn cụ thể; không có "Mục này …", "Trong phần này …", câu hỏi tu từ.
2. Mỗi định nghĩa nằm trong khối `definition`, không có "hãy"; đoạn ngay sau nêu cái gì cố định, cái gì ngẫu nhiên, thứ tự lượng từ; có ví dụ và phản ví dụ.
3. Mỗi công thức hiển thị có câu dẫn; mọi kí hiệu mới được gọi tên ngay sau công thức, đúng `ky-hieu.md`.
4. Mỗi bước biến đổi có lý do (công cụ hoặc giả thiết); "dễ thấy", "rõ ràng", "tất nhiên" không đứng thay lý do.
5. "Chúng ta" chỉ cho kế hoạch, nhu cầu, giới hạn; "ta" trong tính toán; không có "chúng tôi", "bạn đọc", "hãy" ngoài đề bài tập.
6. Mỗi khái niệm một thuật ngữ, đúng `thuat-ngu.md`; tiếng Anh trong ngoặc ở lần đầu trong ghi chú, đúng định dạng mục 10; "phân bố" không lẫn với "phân phối", "hàm lỗi" không lẫn với "hàm mất mát".
7. Không có lời khen, phóng đại ("quan trọng nhất", "nổi tiếng", "thú vị", "mạnh mẽ") và không có khẳng định kiểu "người ta thường" thiếu nguồn.
8. Ví dụ mở bằng thiết lập ($\mathcal X$, $\mathcal Y$, $D$, $\mathcal H$, $\ell$, $m$), có số cụ thể, câu cuối nói ví dụ chứng tỏ điều gì.
9. Mỗi phát biểu hình thức có "**Giả thiết.**" và "**Bảo đảm.**"; chứng minh mở bằng lộ trình, kết thúc bằng $\square$ và một câu về ý nghĩa cho việc học.
10. Mục kết thúc bằng hệ quả hoặc giới hạn cụ thể; không có đoạn tóm tắt lặp lại, không có nhãn "Kết mục".
11. Câu không quá khoảng 40 tiếng; đoạn 2–4 câu; gạch đầu dòng chỉ cho liệt kê thật sự.
12. Chính tả theo mục 12: "kì vọng", "bất kì", "tỉ lệ", "-hóa", "véc-tơ", số thập phân dấu phẩy.
