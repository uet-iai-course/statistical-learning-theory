# Dàn ý Bài 02 — Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-10-30 bởi tác tử lập kế hoạch; chờ điều phối viên duyệt. Dàn ý ràng buộc người viết ghi chú (`materials/lec-02/lecture-note.md`) và sau đó người viết bài tập (`materials/lec-02/exercises.md`).

**Căn cứ, theo thứ tự ưu tiên:** quyết định 1–10 của điều phối viên trong `planning/lec-02/review-log.md` (dẫn là "QĐ n"); `sources/blueprint.md` mục A, C, D, E và "Lecture 2"; `planning/course-plan.md` mục 3–5; `planning/lec-02/source-analysis.md` (viết tắt PTN; mọi con số ở đó đã được điều phối viên tính lại); `planning/van-phong.md` (đặc biệt §3a, §7, §7a, §9a, §11); `planning/thuat-ngu.md`; `planning/ky-hieu.md`; ghi chú Bài 01 (`materials/lec-01/lecture-note.md`) và dàn ý Bài 01. Tác tử lập kế hoạch đã đọc lại UML tr. PDF 41–42 (Bài tập 2.3), 51–52 (Bài tập 3.4, 3.5), 58–59 (Bài tập 4.1, 4.2) để kiểm tra đề; không chép câu chữ.

**Con số mới.** Con số không có trong PTN được đánh dấu † và đã được tính lại bằng Python trong phiên lập kế hoạch (tệp tạm, không thuộc repo); phép tính rút gọn ở mục 12. Riêng ba giá trị xác suất đuôi chính xác ở $m=100,200$ **khác PTN** vì QĐ 2 chốt biến cố "$\ge\epsilon$" (xem mục 12, điểm 1).

**Trạng thái cuối của ghi chú (2026-10-30, sau ba vòng biên tập; ưu tiên hơn các bảng bên dưới):** số khối 02.1–02.18, Ví dụ 02.1–02.12 và Bài tập 02.1–02.11 không đổi. Khác dàn ý: sáu mục tiêu học tập (mục tiêu 4 tách thành 4 "tính cỡ mẫu đủ" và 5 "giải thích hai tốc độ"; mục tiêu cũ 5 thành 6); Ví dụ 02.1 chỉ nhắc bản $D_\eta$ ($D_f$ ở Ví dụ 02.11, $\mathcal M_{\mathcal X}$ ở Ví dụ 02.10, $\ell_c$ sau (T3)); độ lệch viết $\epsilon$ từ Định nghĩa 02.1, $\alpha$ chỉ là ngưỡng Markov và mức Chernoff; Ví dụ 02.4 bỏ cột $m=6$, Bước 4 dùng $\epsilon=0{,}1$ ($500$/$185$, $25\,000$/$381$); Ví dụ 02.8 dùng cận một phía và lập luận lấy điều kiện theo $T$; Ví dụ 02.11 đổi tên "Bốn mức cỡ mẫu…" ($48$/$37$/$30$/$14$); Ví dụ 02.12 hàng $K=1$ ghi "—" ở hai cột; $h_{\mathcal H}$ cho phần tử tốt nhất trong lớp ở §7; Phụ lục C (tính đo được) mới; Bài tập 02.4 đổi tên "… bỏ hệ số $K$" (mục tiêu 6); Bài tập 02.8 đo mục tiêu 4, 5 (người viết bài tập thêm phần so sánh cỡ mẫu khả thực và bất khả tri). Danh sách đầy đủ: `bien-tap-vong-1.md`.

**Sửa của điều phối viên (2026-10-30), ưu tiên hơn chỗ khác trong dàn ý:** xem mục "Dàn ý — quyết định của điều phối viên" trong `review-log.md` (giá trị $0{,}0211$ đã thay trong tệp; Ví dụ 02.9 bước (5) đổi theo quyết định 3; thân bài ≤ 12 000 tiếng).

## 1. Câu hỏi trung tâm, luận điểm, câu hỏi mở đầu, mục tiêu

**Câu hỏi trung tâm.** Khi chỉ có hữu hạn ứng viên, cần bao nhiêu quan sát để rủi ro thực nghiệm phản ánh đúng rủi ro kì vọng, cho một giả thuyết chọn trước và cho giả thuyết được chọn theo chính mẫu đó?

**Luận điểm (một câu).** Với mẫu độc lập cùng phân bố và hàm lỗi trong $[0,1]$, bất đẳng thức Hoeffding chặn độ lệch $\lvert L_S(h)-L_D(h)\rvert$ của một giả thuyết cố định bởi $\sqrt{\ln(2/\delta)/(2m)}$ với xác suất ít nhất $1-\delta$; bất đẳng thức hợp làm cận này đúng đồng thời cho $K$ giả thuyết với giá chỉ là thay $\ln(2/\delta)$ bằng $\ln(2K/\delta)$, và từ đó mọi nghiệm ERM trên lớp hữu hạn có rủi ro vượt mức không quá $2\sqrt{\ln(2K/\delta)/(2m)}$.

**Câu hỏi mở đầu** (blueprint 2.1; văn phong §9a; viết đúng như sau, có thể sửa chữ nhỏ):

> Một hàm phân lớp sai $5\%$ trên một mẫu xác thực (validation sample) gồm $1000$ quan sát, độc lập với dữ liệu đã dùng để huấn luyện nó.
>
> **Câu hỏi.** Với độ tin cậy $95\%$, rủi ro kì vọng của hàm này có thể lớn đến đâu? Câu trả lời thay đổi thế nào nếu hàm này được chọn trong $1000$ ứng viên vì có tỉ lệ lỗi thấp nhất trên chính mẫu xác thực đó?

Câu trả lời hấp dẫn nhưng sai, viết thành câu hỏi thẳng rồi trả lời ngay: "Có dùng được cùng một cận tin cậy cho hàm được chọn như cho một hàm cố định trước khi xem mẫu không? Không: hàm được chọn vì tỉ lệ lỗi của nó thấp, nên tỉ lệ lỗi đó nghiêng về phía thấp hơn rủi ro kì vọng." Thêm một câu: hai câu trả lời bằng số nằm ở §5 (một hàm cố định) và §6 (một hàm chọn trong $1000$ ứng viên). Không dẫn số khối nào ở đây (quy tắc định nghĩa trước khi dùng). Không viết "Một câu trả lời hấp dẫn nhưng sai cho rằng …".

**Mục tiêu học tập** (chỉ chữ, không kí hiệu, không số khối):

1. Phát biểu và chứng minh các bất đẳng thức Markov, Chebyshev và Hoeffding, và chỉ ra bước nào của mỗi chứng minh dùng tính độc lập, bước nào dùng tính bị chặn.
2. Tính và so sánh xác suất đuôi chính xác, cận Chebyshev và cận Hoeffding cho rủi ro thực nghiệm của một giả thuyết cố định; dựng cận tin cậy một phía và khoảng tin cậy hai phía cho rủi ro kì vọng.
3. Chứng minh cận hội tụ đều trên lớp hữu hạn bằng bất đẳng thức hợp, suy ra bảo đảm cho mọi nghiệm ERM, và giải thích vì sao cận cho từng giả thuyết cố định không áp dụng được cho giả thuyết chọn theo mẫu.
4. Tính cỡ mẫu đủ để ước lượng rủi ro, để đạt rủi ro vượt mức nhỏ trong trường hợp bất khả tri và để học trong trường hợp khả thực; giải thích vì sao cỡ mẫu bất khả tri tăng theo bình phương nghịch đảo của độ chính xác còn cỡ mẫu khả thực tăng theo nghịch đảo, và vì sao chỉ so sánh được các cỡ mẫu cùng loại bảo đảm.
5. Dựng phản ví dụ cho thấy kết luận sai khi bỏ tính độc lập của các quan sát, tính bị chặn của hàm lỗi, hoặc số ứng viên trong bất đẳng thức hợp.

## 2. Đánh số

Một bộ đếm chung theo thứ tự đọc cho định nghĩa, bổ đề, mệnh đề, định lý, hệ quả, nhận xét (Bài 02 không có thuật toán); ví dụ và bài tập có bộ đếm riêng. Khối `application` không đánh số. Cột "Blueprint" chỉ dùng nội bộ, không đưa vào ghi chú.

| Số | Loại | Tên (cụm danh từ) | Mục | Độ sâu | Blueprint |
|---|---|---|---|---|---|
| Định nghĩa 02.1 | definition | Xác suất đuôi và cận đuôi | §4 | — | §2.2 |
| Bổ đề 02.2 | lemma | Bất đẳng thức Markov | §4 | chứng minh đầy đủ | §2.2 (không số) |
| Bổ đề 02.3 | lemma | Bất đẳng thức Chebyshev | §4 | chứng minh đầy đủ | §2.2 (không số) |
| Định nghĩa 02.4 | definition | Hàm sinh mô-men | §5 | — | §2.2 |
| Bổ đề 02.5 | lemma | Phương pháp Chernoff | §5 | chứng minh đầy đủ | §2.2 (không số) |
| Bổ đề 02.6 | lemma | Bổ đề Hoeffding | §5 | phác thảo (phần vô hướng ở Phụ lục A) | **Lemma 2.1** |
| Định lý 02.7 | theorem | Bất đẳng thức Hoeffding | §5 | chứng minh đầy đủ | **Theorem 2.2** |
| Nhận xét 02.8 | remark | Các biến có miền giá trị khác nhau | §5 | — | — (QĐ 2) |
| Định nghĩa 02.9 | definition | Cận tin cậy và khoảng tin cậy | §5 | — | §2.2 |
| Hệ quả 02.10 | corollary | Cận tin cậy Hoeffding cho một giả thuyết cố định | §5 | chứng minh đầy đủ | §2.2 (không số) |
| Nhận xét 02.11 | remark | Hàm lỗi không bị chặn | §5 | — | §2.4 Limit (QĐ 7b) |
| Bổ đề 02.12 | lemma | Bất đẳng thức hợp | §6 | chứng minh đầy đủ | (không số) |
| Định nghĩa 02.13 | definition | Mẫu $\epsilon$-đại diện | §6 | — | §2.2 "uniform-convergence event" |
| Định lý 02.14 | theorem | Hội tụ đều trên lớp hữu hạn | §6 | chứng minh đầy đủ | **Theorem 2.3** |
| Nhận xét 02.15 | remark | Cận tổng quát hóa cho mọi thuật toán ERM trên lớp hữu hạn | §6 | — | — (QĐ 5 ii) |
| Hệ quả 02.16 | corollary | Rủi ro vượt mức của ERM trên lớp hữu hạn | §7 | chứng minh đầy đủ | **Corollary 2.4** |
| Mệnh đề 02.17 | proposition | Cỡ mẫu cho lớp hữu hạn trong trường hợp khả thực | §8 | chứng minh đầy đủ | **Proposition 2.5** |
| Nhận xét 02.18 | remark | Hai tốc độ theo độ chính xác | §8 | — | §2.4 / PTN §2.8 |

Tiêu đề khối theo mẫu: `::: theorem Định lý 02.7 (Bất đẳng thức Hoeffding) — chứng minh đầy đủ`; `::: lemma Bổ đề 02.6 (Bổ đề Hoeffding) — phác thảo`; chứng minh: `::: proof Chứng minh Định lý 02.7`.

**Ví dụ** (bộ đếm riêng):

| Số | Tên | Mục | Bản của ví dụ sàng lọc / ứng dụng |
|---|---|---|---|
| Ví dụ 02.1 | Các đại lượng của ví dụ sàng lọc dùng lại trong bài | §3 | cả hai bản, $\mathcal M_{\mathcal X}$, $\ell_c$ |
| Ví dụ 02.2 | Xác suất đuôi chính xác của rủi ro thực nghiệm của $h_3$ | §4 | $D_\eta$ |
| Ví dụ 02.3 | Cận Markov và cận Chebyshev cho rủi ro thực nghiệm của $h_3$ | §4 | $D_\eta$ |
| Ví dụ 02.4 | Ba cách chặn cùng một xác suất đuôi | §5 | $D_\eta$ |
| Ví dụ 02.5 | Khoảng tin cậy cho một hàm phân lớp cố định có tỉ lệ lỗi 5% | §5 | ứng dụng (câu hỏi mở đầu, phần 1) |
| Ví dụ 02.6 | Một hồ sơ chép lại $m$ lần | §5 | $D_\eta$, bỏ độc lập (QĐ 7a) |
| Ví dụ 02.7 | Thiên lệch do chọn trong 1000 ứng viên | §6 | ứng dụng; **cắt đầu tiên nếu quá độ dài** (QĐ 7) |
| Ví dụ 02.8 | Bán kính tin cậy sau khi chọn trong $K$ ứng viên | §6 | ứng dụng (câu hỏi mở đầu, phần 2) |
| Ví dụ 02.9 | ERM trên lớp hàm ngưỡng dưới $D_\eta$ | §7 | $D_\eta$, $K=6$ |
| Ví dụ 02.10 | ERM trên mọi hàm phân lớp của một tập đầu vào hữu hạn | §7 | $D_\eta$, $\mathcal M_{\mathcal X}$ (QĐ 5 i) |
| Ví dụ 02.11 | Ba mức cỡ mẫu cho bản nhãn tất định | §8 | $D_f$ (QĐ 5 iii) |
| Ví dụ 02.12 | Bảng cỡ mẫu cho $K$ ứng viên | §8 | ứng dụng (blueprint 2.4) |

## 3. Bản đồ các mục và phát biểu hình thức

Quy tắc định nghĩa trước khi dùng (người dùng, 2026-10-30) thắng thứ tự thành phần của blueprint: các thành phần 7–11 nằm xen trong §4–§8; mỗi giả thiết được nêu ở chỗ dùng lần đầu; không câu nào trong thân bài dẫn một khối có số đứng sau. Mỗi khối kết quả có dòng **Giả thiết.** và **Bảo đảm.**; khi có từ ba thành phần trở lên thì viết danh sách có nhãn in đậm song song (§3a; mẫu: Mệnh đề 01.7). Xác suất cao viết "với xác suất ít nhất $1-\delta$ theo $S\sim D^m$".

**Kí hiệu cục bộ chốt cho bài** (lý do ở mục 10): biến ngẫu nhiên tổng quát $V$, $V_1,\ldots,V_m$ (không dùng $X$, vì $X$ là đầu vào); trung bình $\bar V_m=\frac1m\sum_iV_i$, $\mu_i=\mathbb EV_i$, $\bar\mu_m=\frac1m\sum_i\mu_i$; mức $\alpha>0$ trong Markov và Chernoff; tham số mũ $\tau$ (không dùng $t$, vì $h_t$; không dùng $\lambda$, vì `ky-hieu.md` dành $\lambda$ cho hệ số chính quy hóa); miền $[a,b]$; $K=\lvert\mathcal H\rvert$; tham số Bernoulli $q$.

### `# Bài 02 — Bất đẳng thức tập trung và độ phức tạp mẫu của lớp hữu hạn` và đoạn dẫn

Ba đến bốn câu: Bài 01 cho đẳng thức $\mathbb E_S[L_S(h)]=L_D(h)$ với $h$ cố định (Mệnh đề 01.7) và đòi một bảo đảm xác suất cao cho $L_D(A(S))$ (Định nghĩa 01.25); câu hỏi trung tâm; hai công cụ (bất đẳng thức tập trung (concentration inequality), bất đẳng thức hợp) và hai kết quả cuối (ERM bất khả tri, khả thực). Không viết "Bài này …" làm chủ ngữ.

### `## Câu hỏi mở đầu`, `## Mục tiêu học tập`

Như mục 1.

### `## Kiến thức tiên quyết`

- **Từ Bài 01:** Định nghĩa 01.1, 01.6 ($L_D$, $L_S$); Mệnh đề 01.7 (không chệch, không cần độc lập); Định nghĩa 01.8 và 01.12 (ERM, $\epsilon_{\mathrm{opt}}$-ERM; giả thiết tối ưu (O1), (O2)); Nhận xét 01.9 (giả thuyết chọn theo mẫu; đánh giá trên mẫu độc lập khi lấy điều kiện); Định nghĩa 01.16, 01.18, 01.25 (khả thực, học PAC hai dạng); Định nghĩa 01.28 và Hệ quả 01.29; Định nghĩa 01.22, Mệnh đề 01.23 (rủi ro Bayes, $h_{\mathrm{Bayes}}\in\mathcal M_{\mathcal X}$); Ví dụ 01.1, 01.2, 01.9, 01.10; giả thiết (T1), (T2).
- **Xác suất:** phương sai; phương sai của tổng các biến độc lập bằng tổng các phương sai; kì vọng của tích các biến độc lập (không âm hoặc khả tích) bằng tích các kì vọng; phân bố Bernoulli và phân bố nhị thức; hai biến cố rời nhau có xác suất của hợp bằng tổng.
- **Giải tích:** hàm lồi nằm dưới dây cung; khai triển Taylor với phần dư Lagrange (chỉ Phụ lục A); $1-x\le e^{-x}$ với mọi $x$ (đã có ở Bài 01); $\ln$ là lôgarit tự nhiên.

**Câu hỏi ôn nhanh** (lời giải ngắn trong một khối `solution`, như Bài 01):

1. Cho $V\sim\mathrm{Bernoulli}(q)$. Tính $\operatorname{Var}V$ và giá trị lớn nhất của nó theo $q\in[0,1]$. *Lời giải:* $q(1-q)$, lớn nhất bằng $\tfrac14$ tại $q=\tfrac12$.
2. Cho $Z_1$ với $\operatorname{Var}Z_1=\sigma^2$ và $Z_2=Z_1$ (tiếp câu ôn nhanh 2 của Bài 01). Tính $\operatorname{Var}\big((Z_1+Z_2)/2\big)$, rồi tính lại khi $Z_1,Z_2$ độc lập cùng phân bố. *Lời giải:* $\sigma^2$ và $\sigma^2/2$; kì vọng như nhau, độ phân tán khác nhau.
3. Với $m\ge1$ và $\epsilon>0$ cho trước, tìm $\tau>0$ làm nhỏ nhất $-\tau\epsilon+\tau^2/(8m)$. *Lời giải:* $\tau=4m\epsilon$, giá trị nhỏ nhất $-2m\epsilon^2$.

Ba câu chuẩn bị đúng Ví dụ 02.3, Ví dụ 02.6 và bước tối ưu của chứng minh Định lý 02.7 (không ghi các số khối này trong ghi chú).

### `## 1. Thiết lập bài toán`

Danh sách tám thành phần như §1 của Bài 01 (nhãn in đậm song song), chỉ ghi điểm mới:

1. **Tập quan sát và phân bố dữ liệu.** $\mathcal Z$, $D$ cố định, chưa biết.
2. **Mẫu.** $S=(Z_1,\ldots,Z_m)\sim D^m$ theo (T1); trong ứng dụng, $S$ là mẫu xác thực, độc lập với dữ liệu đã huấn luyện các ứng viên.
3. **Lớp giả thuyết.** $\mathcal H$ hữu hạn, $K=\lvert\mathcal H\rvert$, chọn trước khi lấy mẫu.
4. **Hàm lỗi.** Nhận giá trị trong một khoảng bị chặn, chủ yếu $[0,1]$ (hàm lỗi 0–1); $\ell_c$ của Bài 01 nhận giá trị trong $[0,4]$.
5. **Quy tắc dùng mẫu.** Đánh giá một $h$ cố định; hoặc chọn $\hat h$ bằng một thuật toán ERM bất kì (mọi quy tắc chọn khi bằng nhau); hoặc một $\epsilon_{\mathrm{opt}}$-ERM.
6. **Mục tiêu.** Bốn đại lượng cần chặn: $\lvert L_S(h)-L_D(h)\rvert$ với $h$ cố định; cùng đại lượng đồng thời cho mọi $h\in\mathcal H$; $L_D(\hat h)-\min_{h\in\mathcal H}L_D(h)$; $L_D(\hat h)$ khi khả thực.
7. **Đối tượng so sánh.** $\min_{h\in\mathcal H}L_D(h)$; giá trị nhỏ nhất tồn tại vì $\mathcal H$ hữu hạn. Rủi ro Bayes khi $\mathcal H=\mathcal M_{\mathcal X}$ với $\mathcal X$ hữu hạn.
8. **Tài nguyên.** Cỡ mẫu $m$; câu trả lời là một cỡ mẫu đủ theo $K$, $\epsilon$, $\delta$ và độ dài miền giá trị của hàm lỗi.

Bảng cố định / ngẫu nhiên (bắt buộc): cố định: $D$, $\mathcal H$, $\ell$, mỗi $h\in\mathcal H$, $L_D(h)$, $\min_{\mathcal H}L_D$, tập $\{h:L_D(h)>\epsilon\}$; ngẫu nhiên theo $S\sim D^m$: $S$, $L_S(h)$, $\max_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$, $\hat h$, $L_D(\hat h)$.

### `## 2. Kí hiệu và giả thiết`

- Bảng nhỏ, chỉ kí hiệu dùng từ §3: $K=\lvert\mathcal H\rvert$; $\ln$; các kí hiệu dùng lại của ví dụ sàng lọc ($D_\eta$, $D_f$, $h_t$, $\ell_c$, $\mathcal M_{\mathcal X}$, $L^{\mathrm{Bayes}}_D$). Các kí hiệu khác được đặt tên tại định nghĩa của chúng (như Bài 01).
- Một đoạn: bài dùng lại (T1), (T2) của Bài 01 và thêm hai giả thiết thống kê, nêu ở chỗ dùng lần đầu: **(T3) hàm lỗi bị chặn** ở §5 (trước Hệ quả 02.10), **(T4) lớp hữu hạn chọn trước mẫu** ở §6 (trước Định lý 02.14). Giả thiết khả thực (Định nghĩa 01.16) chỉ dùng ở §8. Giả thiết tối ưu (O1), (O2) chỉ dùng ở §7. Không dùng lồi, trơn, Lipschitz. Trong ghi chú chỉ ghi "§5", "§6", không ghi số khối.

### `## 3. Ví dụ xuyên suốt`

- **Ví dụ 02.1** (QĐ 1): nhắc lại, không tính mới. $\mathcal X=\{1,\ldots,5\}$, $D_{\mathcal X}$ đều; $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$ dưới $D_\eta$; $f=h_3$ dưới $D_f$; lớp sáu hàm ngưỡng ($K=6$); bảng $L_{D_\eta}(h_t)=(0{,}52;0{,}32;0{,}22;0{,}32;0{,}28;0{,}48)$, mức tốt nhất $0{,}22$ tại $h_3$ (Ví dụ 01.2); rủi ro Bayes $0{,}18$ (Ví dụ 01.10); $\mathcal M_{\mathcal X}$ gồm $2^5=32$ hàm; $(D_f,\mathcal H)$ khả thực với $h^\star=h_3$; $\ell_c$ với $(c_{FP},c_{FN})=(1,4)$ nhận giá trị trong $\{0,1,4\}\subset[0,4]$. Câu cuối: dưới $D_\eta$ và hàm lỗi 0–1, $\ell_{0\text{-}1}(h_3,Z)\sim\mathrm{Bernoulli}(0{,}22)$, nên $mL_S(h_3)$ có phân bố nhị thức $\mathrm{Bin}(m;0{,}22)$ khi $S\sim D_\eta^m$ theo (T1).
- **Khối `application` (Chọn một hàm phân lớp trong $K$ ứng viên trên một mẫu xác thực)** (QĐ 1, blueprint 2.4): $K$ hàm phân lớp đã huấn luyện trên dữ liệu khác (khác ngưỡng, khác siêu tham số); một mẫu xác thực $S$ cỡ $m$, độc lập với dữ liệu huấn luyện; chọn hàm có tỉ lệ lỗi nhỏ nhất trên $S$. Khi lấy điều kiện theo dữ liệu huấn luyện, $K$ ứng viên là một lớp hữu hạn cố định đối với $S$ (Nhận xét 01.9), và phép chọn là ERM trên lớp đó. Hai câu hỏi thực hành: báo cáo rủi ro của hàm được chọn thế nào; $m$ phải tăng thế nào khi $K$ tăng. Không đưa số liệu thực tế nào.

### `## 4. Xác suất đuôi, bất đẳng thức Markov và Chebyshev` (blueprint: Markov/Chebyshev 20 phút)

**Câu mở (nhu cầu, §2 văn phong):** Mệnh đề 01.7 cho $\mathbb E_S[L_S(h)]=L_D(h)$, nhưng Ví dụ 01.5 có $L_{S_\eta}(h_3)=\tfrac13\ne0{,}22$; chúng ta cần chặn xác suất để $L_S(h)$ lệch khỏi $L_D(h)$ ít nhất một lượng cho trước.

1. **Định nghĩa 02.1 (Xác suất đuôi và cận đuôi).** Cho biến ngẫu nhiên $V$ khả tích và $\alpha>0$. *Xác suất đuôi trên* (tail probability) tại $\alpha$ là $\Pr(V-\mathbb EV\ge\alpha)$, *đuôi dưới* là $\Pr(V-\mathbb EV\le-\alpha)$, *đuôi hai phía* là $\Pr(\lvert V-\mathbb EV\rvert\ge\alpha)$. Một *cận đuôi* (tail bound) là một cận trên của một trong ba xác suất này. Đọc lại: biến cố dùng "$\ge$" (QĐ 2); cận đuôi có ích khi nhỏ hơn $1$ và không cần biết phân bố của $V$. Ví dụ: Ví dụ 02.2. Phản ví dụ: $\Pr(V\ge\mathbb EV)$ không phải đuôi theo nghĩa này (không có độ lệch $\alpha>0$); với $V=L_S(h_3)$, $m=100$, xác suất này bằng $0{,}539$† nên không nhỏ khi $m$ tăng.
2. **Ví dụ 02.2 (Xác suất đuôi chính xác của rủi ro thực nghiệm của $h_3$).** Thiết lập: $D_\eta$, hàm lỗi 0–1, $h_3$ cố định, $S\sim D_\eta^m$, $\alpha=0{,}1$. Bước: (1) $L_S(h_3)=k/m$ với $k\sim\mathrm{Bin}(m;0{,}22)$ (Ví dụ 02.1, (T1)); (2) ở $m=6$, $\lvert k/6-0{,}22\rvert\ge0{,}1$ đúng với mọi $k\ne1$ (viết ra: $k=0$ cho độ lệch $0{,}22$; $k=1$ cho $0{,}0533$; $k=2$ cho $0{,}1133$); (3) do đó xác suất bằng $1-6\cdot0{,}22\cdot0{,}78^5=0{,}6189$; (4) ở $m=100$ và $m=200$, cùng cách đếm cho $0{,}0211$† và $8{,}9\cdot10^{-4}$† (cộng xác suất nhị thức trên các $k$ thỏa điều kiện, Phụ lục B.1); (5) câu nghĩa: với $m=100$, khoảng $2\%$ các mẫu cho tỉ lệ lỗi lệch khỏi $0{,}22$ ít nhất $0{,}1$. Câu cuối: tính được vì biết $D_\eta$; khi $D$ chưa biết, cần cận không dùng $D$.
3. **Bổ đề 02.2 (Bất đẳng thức Markov) — chứng minh đầy đủ.** **Giả thiết.** $V\ge0$ hầu chắc chắn, khả tích; $\alpha>0$; không cần độc lập, không cần bị chặn. **Bảo đảm.** $\Pr(V\ge\alpha)\le\mathbb EV/\alpha$; cận đuôi trên từ kì vọng; không phụ thuộc $m$. **Chứng minh.** Lộ trình: so sánh từng điểm rồi lấy kì vọng. Bất đẳng thức then chốt $\alpha\,\mathbb 1[V\ge\alpha]\le V$ (dùng $V\ge0$ trên biến cố $V<\alpha$); lấy kì vọng; chia cho $\alpha$ (dùng $\alpha>0$; UML viết $a\ge0$, ghi chú sửa thành $\alpha>0$, không bình luận về UML trong thân bài). Câu sau $\square$: chỉ biết kì vọng thì cận chỉ giảm như $1/\alpha$.
4. **Bổ đề 02.3 (Bất đẳng thức Chebyshev) — chứng minh đầy đủ.** **Giả thiết.** (a) $V$ có $\mathbb EV^2<\infty$; (b) $V_1,\ldots,V_m$ độc lập, mỗi $V_i$ có $\operatorname{Var}V_i\le\sigma^2$. **Bảo đảm.** (a) $\Pr(\lvert V-\mathbb EV\rvert\ge\alpha)\le\operatorname{Var}V/\alpha^2$; (b) $\Pr(\lvert\bar V_m-\bar\mu_m\rvert\ge\alpha)\le\sigma^2/(m\alpha^2)$; cận hai phía, giảm như $1/m$. **Chứng minh.** (a) Markov cho $(V-\mathbb EV)^2\ge0$ tại mức $\alpha^2$, vì $\{\lvert V-\mathbb EV\rvert\ge\alpha\}=\{(V-\mathbb EV)^2\ge\alpha^2\}$. (b) $\operatorname{Var}\bar V_m=m^{-2}\sum_i\operatorname{Var}V_i\le\sigma^2/m$; **chỗ dùng độc lập**: phương sai của tổng (kiến thức tiên quyết); Bài tập 02.1 cho thấy chỉ cần không tương quan từng đôi. Câu sau $\square$: tính độc lập làm phương sai của trung bình giảm theo $1/m$.
5. **Ví dụ 02.3 (Cận Markov và cận Chebyshev cho rủi ro thực nghiệm của $h_3$).** Thiết lập như Ví dụ 02.2. Bước: (1) Markov cho đuôi trên: $\Pr(L_S(h_3)\ge0{,}32)\le0{,}22/0{,}32=0{,}6875$† với mọi $m$, trong khi giá trị chính xác là $0{,}3937$†, $0{,}0134$†, $6{,}9\cdot10^{-4}$† ở $m=6,100,200$; câu nghĩa: cận Markov không giảm khi $m$ tăng. (2) Phương sai: $\operatorname{Var}\ell_{0\text{-}1}(h_3,Z)=0{,}22\cdot0{,}78=0{,}1716$ (câu ôn nhanh 1), nên $\operatorname{Var}L_S(h_3)=0{,}1716/m$ theo (T1). (3) Chebyshev (a): $0{,}1716/(0{,}01m)=17{,}16/m$, bằng $2{,}86$; $0{,}1716$; $0{,}0858$ ở $m=6,100,200$. (4) Khi không biết $q$: mọi biến trong $[0,1]$ có $\operatorname{Var}\le\mu(1-\mu)\le\tfrac14$ (một dòng: $\mathbb EV^2\le\mathbb EV$), nên cận không phụ thuộc phân bố là $1/(4m\alpha^2)=25/m$: $4{,}17$†; $0{,}25$†; $0{,}125$†. (5) Cỡ mẫu để cận Chebyshev không phụ thuộc phân bố $\le\delta$: $m\ge1/(4\delta\alpha^2)$; với $\alpha=0{,}1$, $\delta=0{,}05$: $1/(4\cdot0{,}05\cdot0{,}01)=500$†. Câu cuối: cận đúng nhưng giảm như $1/m$ và cỡ mẫu tăng như $1/\delta$.

Kết mục bằng văn xuôi: muốn cỡ mẫu tăng như $\ln(1/\delta)$ thay vì $1/\delta$, cần dùng mọi mô-men của $V$, không chỉ phương sai.

### `## 5. Phương pháp Chernoff và bất đẳng thức Hoeffding` (40 phút)

1. **Định nghĩa 02.4 (Hàm sinh mô-men).** Cho biến ngẫu nhiên $V$. *Hàm sinh mô-men* (moment generating function) của $V$ là $\tau\mapsto\mathbb Ee^{\tau V}\in(0,\infty]$, $\tau\in\mathbb R$. **Không đặt kí hiệu riêng** (mục 10). Đọc lại: hữu hạn với mọi $\tau$ khi $V$ bị chặn. Ví dụ: $V\sim\mathrm{Bernoulli}(q)$ cho $1-q+qe^{\tau}$. Phản ví dụ (đuôi nặng): $\Pr(V=k)$ tỉ lệ với $1/k^3$, $k\ge1$: $\mathbb EV<\infty$ nhưng $\mathbb Ee^{\tau V}=\infty$ với mọi $\tau>0$ (số hạng $e^{\tau k}/k^3\to\infty$); không cần nêu hằng số chuẩn hóa.
2. **Bổ đề 02.5 (Phương pháp Chernoff) — chứng minh đầy đủ.** **Giả thiết.** (a) $V$ bất kì, $\alpha\in\mathbb R$; (b) $V=\sum_{i=1}^mV_i$ với $V_1,\ldots,V_m$ độc lập. **Bảo đảm.** (a) $\Pr(V\ge\alpha)\le e^{-\tau\alpha}\,\mathbb Ee^{\tau V}$ với mọi $\tau>0$, nên $\le\inf_{\tau>0}e^{-\tau\alpha}\mathbb Ee^{\tau V}$; (b) $\mathbb Ee^{\tau V}=\prod_i\mathbb Ee^{\tau V_i}$. **Chứng minh.** (a) $x\mapsto e^{\tau x}$ tăng nên $\{V\ge\alpha\}=\{e^{\tau V}\ge e^{\tau\alpha}\}$; Markov (Bổ đề 02.2) cho $e^{\tau V}\ge0$ tại mức $e^{\tau\alpha}>0$; nếu $\mathbb Ee^{\tau V}=\infty$ thì cận tầm thường. (b) **chỗ dùng độc lập**: $e^{\tau V_i}$ là các biến không âm độc lập, kì vọng của tích bằng tích kì vọng. Câu sau $\square$: ba bước của phương pháp là Markov trên hàm mũ, tách theo độc lập, tối ưu theo $\tau$.
3. **Bổ đề 02.6 (Bổ đề Hoeffding) — phác thảo.** **Giả thiết.** $a\le V\le b$ hầu chắc chắn; không cần $\mathbb EV=0$. **Bảo đảm.** $\mathbb Ee^{\tau(V-\mathbb EV)}\le\exp\big(\tau^2(b-a)^2/8\big)$ với mọi $\tau\in\mathbb R$; một bất đẳng thức tất định về một kì vọng, chỉ phụ thuộc độ dài $b-a$. **Chứng minh (thân bài).** Lộ trình: đưa về biến có kì vọng $0$, chặn hàm mũ bằng dây cung, rồi chặn một hàm vô hướng. Bước 1: $W=V-\mathbb EV\in[a',b']$ với $a'=a-\mathbb EV\le0\le b'=b-\mathbb EV$, $b'-a'=b-a$ (**chỗ dùng tính bị chặn**); trường hợp $a'=b'$ tầm thường. Bước 2 (lồi): với $w\in[a',b']$, $e^{\tau w}\le\frac{b'-w}{b'-a'}e^{\tau a'}+\frac{w-a'}{b'-a'}e^{\tau b'}$; lấy kì vọng, dùng $\mathbb EW=0$. Bước 3: đặt $\theta=-a'/(b'-a')\in[0,1]$, $u=\tau(b-a)$; vế phải bằng $e^{\varphi(u)}$ với $\varphi(u)=-\theta u+\ln(1-\theta+\theta e^u)$ (viết ra phép kiểm: $e^{-\theta u}=e^{\tau a'}$, $1-\theta=b'/(b'-a')$). Bước 4: $\varphi(u)\le u^2/8$ với mọi $u\in\mathbb R$, chứng minh ở **Phụ lục A**. Một câu kiểm bằng số (tùy chọn): với $V\sim\mathrm{Bernoulli}(0{,}22)$, $\tau=1$: $\mathbb Ee^{V-0{,}22}=0{,}78e^{-0{,}22}+0{,}22e^{0{,}78}\approx1{,}1059\le e^{1/8}\approx1{,}1331$†. Câu sau $\square$: hàm sinh mô-men của một biến bị chặn đã trừ kì vọng không lớn hơn của một biến chuẩn có phương sai $(b-a)^2/4$; không cần viết câu so sánh với phân bố chuẩn nếu thiếu chỗ.
4. **Định lý 02.7 (Bất đẳng thức Hoeffding) — chứng minh đầy đủ** (QĐ 2; blueprint Theorem 2.2, mở rộng từ $[0,1]$ sang $[a,b]$). **Giả thiết** (danh sách có nhãn): **Biến ngẫu nhiên.** $V_1,\ldots,V_m$ độc lập, không cần cùng phân bố; **Miền giá trị.** $a\le V_i\le b$ hầu chắc chắn với mọi $i$, $a<b$; **Độ lệch.** $\epsilon>0$. **Bảo đảm** (danh sách song song): **(a) Đuôi trên.** $\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\le\exp\!\big(-2m\epsilon^2/(b-a)^2\big)$; **(b) Đuôi dưới.** $\Pr(\bar V_m-\bar\mu_m\le-\epsilon)\le$ cùng cận; **(c) Hai phía.** $\Pr(\lvert\bar V_m-\bar\mu_m\rvert\ge\epsilon)\le2\exp\!\big(-2m\epsilon^2/(b-a)^2\big)$. Cận xác suất cao cho một trung bình thực nghiệm quanh trung bình tổng thể; giảm theo hàm mũ của $m\epsilon^2$; phụ thuộc phân bố chỉ qua $b-a$. **Chứng minh.** Lộ trình: Chernoff cho $\bar V_m-\bar\mu_m$, tách bằng độc lập, Bổ đề 02.6 cho từng thừa số, tối ưu $\tau$. Bất đẳng thức then chốt (trong `aligned`, một quan hệ một dòng):
   $\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\le e^{-\tau\epsilon}\prod_i\mathbb Ee^{(\tau/m)(V_i-\mu_i)}\le e^{-\tau\epsilon}\prod_ie^{\tau^2(b-a)^2/(8m^2)}=\exp\!\big(-\tau\epsilon+\tau^2(b-a)^2/(8m)\big)$.
   Ghi chỗ dùng: dòng 1 Bổ đề 02.5(a) với $V=\sum_i(V_i-\mu_i)/m$ và 02.5(b) (**độc lập**); dòng 2 Bổ đề 02.6 với $\tau/m$ (**bị chặn**). Chọn $\tau=4m\epsilon/(b-a)^2$ (câu ôn nhanh 3 với $(b-a)^2$): số mũ $-4m\epsilon^2/(b-a)^2+2m\epsilon^2/(b-a)^2=-2m\epsilon^2/(b-a)^2$. (b): áp dụng (a) cho $-V_i\in[-b,-a]$. (c): hai biến cố của (a) và (b) **rời nhau** vì $\epsilon>0$, nên xác suất của hợp bằng tổng; **không cần bất đẳng thức hợp** (quyết định của dàn ý, để bất đẳng thức hợp chỉ xuất hiện ở §6 mà không có tham chiếu tới trước). Không dùng tính cùng phân bố ở bước nào. Câu sau $\square$: cỡ mẫu để xác suất hai phía $\le\delta$ tăng như $\ln(2/\delta)$, không như $1/\delta$.
5. **Nhận xét 02.8 (Các biến có miền giá trị khác nhau)** (QĐ 2). Nếu $a_i\le V_i\le b_i$, cùng chứng minh cho $\Pr(\bar V_m-\bar\mu_m\ge\epsilon)\le\exp\!\big(-2m^2\epsilon^2/\sum_i(b_i-a_i)^2\big)$; với $b_i-a_i=b-a$ trở về Định lý 02.7. Chứng minh là Bài tập 02.2. Hai đến ba câu, không có ví dụ số trong ghi chú.
6. **Đoạn nối + giả thiết (T3).** Áp dụng cho hàm lỗi cần (T3): **(T3) Hàm lỗi bị chặn.** $0\le\ell(h,z)\le1$ với mọi $h\in\mathcal H$, $z\in\mathcal Z$; khi miền là $[a,b]$, các cận dưới đây nhân thêm $(b-a)^2$ vào cỡ mẫu (dẫn Định lý 02.7; Bài tập 02.11 với $\ell_c$).
7. **Định nghĩa 02.9 (Cận tin cậy và khoảng tin cậy).** Cho hàm lỗi thỏa (T3), $h$ cố định, $m\ge1$, $\delta\in(0,1)$. Một hàm đo được $\overline L_\delta:\mathcal Z^m\to\mathbb R$ là *cận trên tin cậy* (upper confidence bound) mức $1-\delta$ cho $L_D(h)$ nếu với **mọi** phân bố $D$ trên $\mathcal Z$, $\Pr_{S\sim D^m}[L_D(h)\le\overline L_\delta(S)]\ge1-\delta$. Một cặp $(\underline L_\delta,\overline L_\delta)$ là *khoảng tin cậy* (confidence interval) mức $1-\delta$ nếu $\Pr_S[\underline L_\delta(S)\le L_D(h)\le\overline L_\delta(S)]\ge1-\delta$ với mọi $D$. Đọc lại: hai đầu mút ngẫu nhiên, $L_D(h)$ cố định; "mọi $D$" đứng sau hàm (lượng từ như Định nghĩa 01.18); xác suất lấy theo các lần lấy mẫu lặp lại (Nhận xét 01.19). Ví dụ: $\overline L_\delta\equiv1$ là cận trên tin cậy ở mọi mức nhưng vô dụng. Phản ví dụ: $\overline L(S)=L_S(h)$ không phải cận trên tin cậy mức $0{,}95$: dưới $D_\eta$, $m=100$, $\Pr(L_S(h_3)\ge0{,}22)=0{,}539$†.
8. **Hệ quả 02.10 (Cận tin cậy Hoeffding cho một giả thuyết cố định) — chứng minh đầy đủ.** **Giả thiết.** **Mẫu.** (T1); **Hàm lỗi.** (T2), (T3); **Giả thuyết.** $h\in\mathcal H$ cố định, không phụ thuộc $S$; **Tham số.** $\delta\in(0,1)$, $m\ge1$. **Bảo đảm.** **(a)** $\Pr_S(\lvert L_S(h)-L_D(h)\rvert\ge\epsilon)\le2e^{-2m\epsilon^2}$ với mọi $\epsilon>0$; **(b)** $L_S(h)\pm\sqrt{\ln(2/\delta)/(2m)}$ là khoảng tin cậy mức $1-\delta$; **(c)** $L_S(h)+\sqrt{\ln(1/\delta)/(2m)}$ là cận trên tin cậy mức $1-\delta$; **(d)** nếu $m\ge\ln(2/\delta)/(2\epsilon^2)$ thì $\lvert L_S(h)-L_D(h)\rvert\le\epsilon$ với xác suất ít nhất $1-\delta$. Xác suất cao; so đại lượng thực nghiệm với tổng thể; không phụ thuộc $D$. **Chứng minh.** $V_i=\ell(h,Z_i)\in[0,1]$, độc lập vì $h$ cố định và các $Z_i$ độc lập (**chỗ dùng $h$ cố định**, như Bước 1 của Mệnh đề 01.7), $\mu_i=L_D(h)$; Định lý 02.7 với $a=0,b=1$ cho (a). (b), (c): giải $2e^{-2mr^2}=\delta$ và $e^{-2mr^2}=\delta$; lấy phần bù; biến cố "$<r$" nằm trong "$\le r$". (d): $\epsilon\ge\sqrt{\ln(2/\delta)/(2m)}$. Câu sau $\square$: bán kính giảm như $1/\sqrt m$; đổi sang một phía chỉ đổi $\ln(2/\delta)$ thành $\ln(1/\delta)$.
9. **Ví dụ 02.4 (Ba cách chặn cùng một xác suất đuôi).** Thiết lập như Ví dụ 02.2, $\epsilon=0{,}1$. Bước: (1) Hoeffding hai phía $2e^{-2m\cdot0{,}01}$: $1{,}774$ (vô dụng), $2e^{-2}=0{,}2707$, $2e^{-4}=0{,}0366$ ở $m=6,100,200$; (2) bảng ba dòng × bốn cột: chính xác $0{,}6189$ / $0{,}0211$† / $8{,}9\cdot10^{-4}$†; Chebyshev biết phương sai $2{,}86$ / $0{,}1716$ / $0{,}0858$; Chebyshev không phụ thuộc phân bố $4{,}17$† / $0{,}25$† / $0{,}125$†; Hoeffding $1{,}774$ / $0{,}2707$ / $0{,}0366$; (3) câu nghĩa, **nói đúng sự thật**: ở $m=100$ cả hai cận Chebyshev nhỏ hơn cận Hoeffding; ở $m=200$ Hoeffding nhỏ hơn; mọi cận đều lớn hơn giá trị chính xác nhiều lần; (4) cỡ mẫu theo $\delta$ với $\epsilon=0{,}05$: $\delta=0{,}05$: Chebyshev không phụ thuộc phân bố $2000$, Hoeffding $\lceil\ln40/0{,}005\rceil=\lceil737{,}8\rceil=738$; $\delta=0{,}001$: $100\,000$ so với $\lceil\ln2000/0{,}005\rceil=\lceil1520{,}2\rceil=1521$. Câu cuối: lợi thế của Hoeffding nằm ở sự phụ thuộc $\ln(1/\delta)$; ở §6 lợi thế này quyết định khi $\delta$ được chia cho $K$.
10. **Ví dụ 02.5 (Khoảng tin cậy cho một hàm phân lớp cố định có tỉ lệ lỗi 5%).** Thiết lập: ứng dụng ở §3, một hàm $h$ cố định trước khi xem $S$, hàm lỗi 0–1, $m=1000$, $L_S(h)=0{,}05$, $\delta=0{,}05$. Bước: (1) $\ln(2/0{,}05)=\ln40\approx3{,}6889$; (2) bán kính hai phía $\sqrt{3{,}6889/2000}\approx0{,}0429$; (3) khoảng $[0{,}007;\ 0{,}093]$; (4) một phía: $\sqrt{\ln20/2000}=\sqrt{2{,}9957/2000}\approx0{,}0387$, cận trên $0{,}0887$†; (5) câu nghĩa: với hàm cố định, rủi ro kì vọng không quá khoảng $8{,}9\%$, theo nghĩa của Nhận xét 01.19. Câu cuối: đây là phần thứ nhất của câu trả lời cho câu hỏi mở đầu; phần thứ hai cần hàm được chọn theo $S$.
11. **Ví dụ 02.6 (Một hồ sơ chép lại $m$ lần)** (QĐ 7a; bỏ giả thiết độc lập). Thiết lập: $Z\sim D_\eta$, $Z_1=\cdots=Z_m=Z$ (mỗi $Z_i$ vẫn có phân bố $D_\eta$), $h_3$, hàm lỗi 0–1. Bước: (1) $L_S(h_3)=\ell(h_3,Z)\in\{0,1\}$; (2) $\mathbb EL_S(h_3)=0{,}22$ theo Mệnh đề 01.7 dạng yếu (nối câu ôn nhanh 2 của Bài 01 và câu ôn nhanh 2 của bài này); (3) $\lvert L_S(h_3)-0{,}22\rvert\ge0{,}22\ge0{,}2$ chắc chắn, với mọi $m$; (4) nếu áp dụng sai Định lý 02.7 với $\epsilon=0{,}2$, $m=100$: $2e^{-2\cdot100\cdot0{,}04}=2e^{-8}\approx6{,}7\cdot10^{-4}$; (5) chỗ hỏng: Bổ đề 02.5(b), vì $\mathbb Ee^{\tau\sum_i\ell(h_3,Z_i)}=\mathbb Ee^{\tau m\ell(h_3,Z)}$ không bằng tích. Câu cuối: tính không chệch còn, tính tập trung mất; tính độc lập là giả thiết của Định lý 02.7, không phải chi tiết kỹ thuật.
12. **Nhận xét 02.11 (Hàm lỗi không bị chặn)** (QĐ 7b; thực hiện lời hứa ở Nhận xét 01.2). Các biến $V_i$ độc lập cùng phân bố, $V_i\in\{0,M\}$, $\Pr(V_i=M)=1/M$, nên $\mathbb EV_i=1$; lấy $M=m^2$. Khi đó $\Pr(\bar V_m=0)=(1-1/m^2)^m\ge1-1/m$ (bất đẳng thức Bernoulli), tại $m=100$ bằng $0{,}9900$; trên biến cố này $\lvert\bar V_m-1\rvert=1$. Định lý 02.7 với $[0,M]$ cho $2e^{-2m/M^2}\approx2$, không mâu thuẫn; nhưng không cận nào chỉ phụ thuộc $m$ và $\epsilon$ đúng cho mọi hàm lỗi không âm có kì vọng $1$. Một câu: hàm lỗi bình phương với một nhãn hiếm có giá trị rất lớn cho tình huống này; hàm lỗi log tương tự. Không chứng minh thêm (Bài 05–06 dùng giả thiết khác).

Kết mục: Hệ quả 02.10 chỉ đúng cho $h$ chọn trước khi xem $S$; thuật toán ERM và phép chọn trong $K$ ứng viên chọn sau.

**Nghỉ giữa giờ 10 phút** (chỉ trong lịch dạy).

### `## 6. Bất đẳng thức hợp và hội tụ đều trên lớp hữu hạn` (một phần của 35 phút)

Câu mở theo mẫu §2 văn phong: "Hệ quả 02.10 chặn $\lvert L_S(h)-L_D(h)\rvert$ cho một $h$ chọn trước khi lấy mẫu. Thuật toán ERM chọn $\hat h$ sau khi thấy $S$, nên chúng ta cần một cận đúng đồng thời cho mọi $h\in\mathcal H$."

1. **Ví dụ 02.7 (Thiên lệch do chọn trong 1000 ứng viên)** (QĐ 7; khung khác PTN, xem mục 12 điểm 2). Thiết lập dựng sẵn: $K=1000$, $\mathcal X=\{0,1\}^{K}$, các tọa độ của $X$ độc lập, mỗi tọa độ bằng $1$ với xác suất $0{,}07$; $Y=0$; ứng viên $h_k(x)=x_k$; hàm lỗi 0–1; mẫu xác thực $m=1000$. Mọi ứng viên có $L_D(h_k)=0{,}07$. Bước: (1) với một ứng viên cố định, $mL_S(h_k)\sim\mathrm{Bin}(1000;0{,}07)$ và $\Pr(L_S(h_k)\le0{,}05)=\Pr(\mathrm{Bin}\le50)\approx0{,}00593$ (Phụ lục B.2); (2) do các tọa độ độc lập, $K$ tỉ lệ lỗi độc lập, nên $\Pr(\min_kL_S(h_k)\le0{,}05)=1-(1-0{,}00593)^{1000}\approx0{,}9974$; (3) câu nghĩa: một ứng viên cố định trông tốt như $5\%$ với xác suất $0{,}6\%$, còn ứng viên tốt nhất trên mẫu trông như vậy với xác suất $99{,}7\%$, dù rủi ro kì vọng của nó là $7\%$. (4) Câu cuối: tỉ lệ lỗi của ứng viên được chọn lệch xuống; xác suất của một biến cố cho $h$ cố định không chuyển sang $\hat h$. Ghi rõ: tính độc lập giữa các ứng viên là một cấu trúc dựng để tính chính xác, không phải khẳng định về mô hình thực. **Không** dùng bất đẳng thức hợp trong ví dụ này (chưa định nghĩa); phép so với cận đều để ở Ví dụ 02.8. **Không** so với khoảng chuẩn xấp xỉ của PTN (học phần chưa dùng định lý giới hạn trung tâm).
2. **Bổ đề 02.12 (Bất đẳng thức hợp) — chứng minh đầy đủ.** **Giả thiết.** $B_1,\ldots,B_K$ là các biến cố bất kì trên cùng một không gian xác suất; không cần độc lập, không cần rời nhau. **Bảo đảm.** $\Pr(\bigcup_kB_k)\le\sum_k\Pr(B_k)$. **Chứng minh.** Quy nạp theo $K$; bước hai biến cố: $A\cup B=A\cup(B\setminus A)$ rời nhau, $\Pr(B\setminus A)\le\Pr(B)$. Lần đầu trong ghi chú: "bất đẳng thức hợp (union bound)" (Bài 01 đã dùng tên này trong chứng minh Mệnh đề 01.15; vẫn ghi tiếng Anh lần đầu trong Bài 02). Đọc lại: cận chặt khi các biến cố gần rời nhau, lỏng khi chúng chồng lên nhau (các hàm ngưỡng gần nhau sai trên gần cùng các mẫu; số liệu ở §8).
3. **Định nghĩa 02.13 (Mẫu $\epsilon$-đại diện).** Cho $\mathcal H$, $\ell$, $D$, $\epsilon>0$. Một mẫu $s\in\mathcal Z^m$ là *$\epsilon$-đại diện* ($\epsilon$-representative) đối với $(\mathcal H,\ell,D)$ nếu $\lvert L_s(h)-L_D(h)\rvert\le\epsilon$ với mọi $h\in\mathcal H$. Biến cố "$S$ là $\epsilon$-đại diện" được gọi là *biến cố hội tụ đều* (uniform convergence). Đọc lại: phụ thuộc $D$ chưa biết nên không kiểm tra được từ $s$; với $\mathcal H$ hữu hạn, biến cố là giao hữu hạn các biến cố đo được. **Ví dụ / phản ví dụ** (†): dưới $D_\eta$, các hiệu $L_{S_\eta}(h_t)-L_{D_\eta}(h_t)$ là $-0{,}02;\ 0{,}0133;\ 0{,}1133;\ 0{,}18;\ 0{,}0533;\ 0{,}02$ (Ví dụ 01.5 trừ Ví dụ 01.2), nên $S_\eta$ là $\epsilon$-đại diện khi và chỉ khi $\epsilon\ge0{,}18$; nó không là $0{,}1$-đại diện vì $h_3$ và $h_4$. Không định nghĩa tính chất hội tụ đều của lớp và $m^{UC}_{\mathcal H}$ (QĐ 3: Bài 03).
4. **Đoạn giả thiết (T4).** **(T4) Lớp hữu hạn chọn trước mẫu.** $\mathcal H$ hữu hạn, $K=\lvert\mathcal H\rvert\ge1$, được chọn trước và không phụ thuộc $S$.
5. **Định lý 02.14 (Hội tụ đều trên lớp hữu hạn) — chứng minh đầy đủ** (blueprint Theorem 2.3). **Giả thiết.** **Mẫu.** (T1); **Hàm lỗi.** (T2), (T3); **Lớp.** (T4); **Tham số.** $\delta\in(0,1)$, $m\ge1$. **Bảo đảm.** Đặt $r_m=\sqrt{\ln(2K/\delta)/(2m)}$ và $r_m^{+}=\sqrt{\ln(K/\delta)/(2m)}$. **(a) Hai phía.** Với xác suất ít nhất $1-\delta$ theo $S\sim D^m$, $S$ là $r_m$-đại diện, tức $\lvert L_S(h)-L_D(h)\rvert\le r_m$ đồng thời cho mọi $h\in\mathcal H$. **(b) Một phía.** Với xác suất ít nhất $1-\delta$, $L_D(h)\le L_S(h)+r_m^{+}$ đồng thời cho mọi $h\in\mathcal H$. **(c) Dạng cỡ mẫu.** Nếu $m\ge\ln(2K/\delta)/(2\epsilon^2)$ thì $S$ là $\epsilon$-đại diện với xác suất ít nhất $1-\delta$. Xác suất cao; đồng thời cho mọi $h$; phụ thuộc $K$ qua $\ln K$; với $K=1$, (a) và (b) trở về Hệ quả 02.10(b)(c). **Chứng minh.** Lộ trình: biến cố hỏng của từng $h$, cận Hoeffding cho từng biến cố, cộng lại bằng bất đẳng thức hợp. Bước 1: với $r>0$, $B_h=\{\lvert L_S(h)-L_D(h)\rvert\ge r\}$; $\{S\text{ không là }r\text{-đại diện}\}\subseteq\bigcup_hB_h$. Bước 2: $\Pr(B_h)\le2e^{-2mr^2}$ theo Hệ quả 02.10(a) (**(T4) dùng ở đây**: mỗi $h$ cố định đối với $S$; (T1), (T3) qua Hệ quả 02.10). Bước 3: Bổ đề 02.12: $\Pr(\bigcup_hB_h)\le2Ke^{-2mr^2}$ (**(T4) dùng lần nữa**: tổng hữu hạn $K$ số hạng). **Không dùng** độc lập giữa các $B_h$: chúng tính trên cùng một mẫu và phụ thuộc mạnh. Bước 4: $2Ke^{-2mr_m^2}=\delta$; phần bù cho (a). (b): các biến cố một phía $\{L_D(h)-L_S(h)\ge r\}$, Định lý 02.7(b), $Ke^{-2mr^2}=\delta$. (c): $r_m\le\epsilon$. Câu sau $\square$: mọi quy tắc chọn nào dựa trên $L_S$ cũng được hưởng cận này, vì cận đúng cho mọi $h$ cùng lúc.
6. **Ví dụ 02.8 (Bán kính tin cậy sau khi chọn trong $K$ ứng viên)** (câu hỏi mở đầu, phần 2). Thiết lập: ứng dụng ở §3, $m=1000$, $\delta=0{,}05$, hàm được chọn có $L_S(\hat h)=0{,}05$. Bước: (1) **vì sao định lý áp dụng**: lấy điều kiện theo dữ liệu huấn luyện, $K$ ứng viên cố định đối với $S$ và $S$ vẫn có phân bố $D^m$ (Nhận xét 01.9), nên (T1), (T4) thỏa với xác suất điều kiện; xác suất ít nhất $1-\delta$ với mọi dữ liệu huấn luyện thì cũng đúng khi lấy trung bình; (2) $K=1000$: $\ln(2000/0{,}05)=\ln40000\approx10{,}5966$, $r_m=\sqrt{10{,}5966/2000}\approx0{,}0728$; một phía $\ln20000\approx9{,}9035$, $r_m^{+}\approx0{,}0704$, cận trên $0{,}1204$†; (3) $K=5000$: $r_m\approx0{,}0781$, $r_m^{+}\approx0{,}0759$, cận trên $0{,}1259$†; (4) so với hàm cố định ($0{,}0387$, Ví dụ 02.5): chọn trong $1000$ ứng viên làm bán kính một phía tăng từ $0{,}039$ lên $0{,}070$; tăng $K$ thêm năm lần chỉ thêm khoảng $0{,}005$; (5) nối Ví dụ 02.7: độ lệch $0{,}02$ ở đó nhỏ hơn $r_m^{+}=0{,}0704$, nên không mâu thuẫn; bất đẳng thức hợp với $K=1000$ cho $1000\cdot0{,}00593\approx5{,}93>1$, cũng không mâu thuẫn. Câu cuối: câu trả lời cho câu hỏi mở đầu là khoảng $8{,}9\%$ cho hàm cố định và khoảng $12\%$ cho hàm được chọn trong $1000$ ứng viên.
7. **Nhận xét 02.15 (Cận tổng quát hóa cho mọi thuật toán ERM trên lớp hữu hạn)** (QĐ 5 ii). Với hàm lỗi 0–1 và $\mathcal H$ hữu hạn, Định lý 02.14(b) cho thấy $\beta(m,\delta)=r_m^{+}$ (và cả $r_m$) thỏa Định nghĩa 01.28: biến cố của định lý không phụ thuộc quy tắc chọn khi bằng nhau và đúng với mọi $D$. Đối lập với Hệ quả 01.29, nơi $\beta\ge1$ trên $\mathcal M_{[0,1]}$. Tính đo được (thực hiện Phụ lục A(v) của Bài 01 cho lớp hữu hạn): $\max_h\lvert L_S(h)-L_D(h)\rvert$ là giá trị lớn nhất của hữu hạn hàm đo được; một thuật toán ERM với quy tắc chọn cố định nhận hữu hạn giá trị trên các tập đo được (tổ hợp Boole của $\{L_s(h)\le L_s(h')\}$), nên thỏa Định nghĩa 01.4.

### `## 7. ERM trên lớp hữu hạn trong trường hợp bất khả tri` (phần còn lại của 35 phút)

1. **Hệ quả 02.16 (Rủi ro vượt mức của ERM trên lớp hữu hạn) — chứng minh đầy đủ** (blueprint Corollary 2.4; QĐ 4). **Giả thiết.** **Mẫu.** (T1); **Hàm lỗi.** (T2), (T3); **Lớp.** (T4); **Thuật toán.** (O1): $\hat A$ là một thuật toán ERM bất kì trên $\mathcal H$ (mọi quy tắc chọn khi bằng nhau); hoặc (O2): một $\epsilon_{\mathrm{opt}}$-ERM; **Tham số.** $\delta\in(0,1)$. **Bảo đảm.** **(a)** Với xác suất ít nhất $1-\delta$, đồng thời cho mọi nghiệm ERM $\hat h$ trên $S$: $L_D(\hat h)\le\min_{h\in\mathcal H}L_D(h)+2r_m$. **(b)** Dưới (O2): $L_D(A(S))\le\min_{\mathcal H}L_D+2r_m+\epsilon_{\mathrm{opt}}$ trên cùng biến cố. **(c)** Mọi thuật toán ERM trên $\mathcal H$ là thuật toán học PAC bất khả tri (Định nghĩa 01.25) với $M(\epsilon,\delta)=\lceil2\ln(2K/\delta)/\epsilon^2\rceil$; do đó lớp hữu hạn học được PAC bất khả tri. Xác suất cao; rủi ro vượt mức so với lớp; không phụ thuộc $D$. Ghi: $D$ có rủi ro hữu hạn tự động vì (T3). **Chứng minh.** Lộ trình: một bước tất định trên biến cố $r$-đại diện, rồi Định lý 02.14. Bước 1: $h^\star\in\arg\min_{\mathcal H}L_D$ tồn tại vì $\mathcal H$ hữu hạn (**(T4)**) và cố định (không phụ thuộc $S$). Bước 2 (tất định): nếu $S$ là $r$-đại diện thì $L_D(\hat h)\le L_S(\hat h)+r\le L_S(h^\star)+r\le L_D(h^\star)+2r$; bước giữa **dùng (O1)** (với (O2) thêm $\epsilon_{\mathrm{opt}}$); hai bước ngoài dùng tính đại diện tại $\hat h$ và tại $h^\star$. Bước 3: Định lý 02.14(a) với $r=r_m$. Bước 4: $2r_m\le\epsilon\iff m\ge2\ln(2K/\delta)/\epsilon^2$ (tương đương chính xác); lấy trần cho $M$. Câu sau $\square$: hệ số $2$ đến từ hai phép so sánh; ý tinh chỉnh $\ln((K+1)/\delta)$ **không** đưa vào ghi chú (QĐ 8; Bài tập 02.3).
2. **Ví dụ 02.9 (ERM trên lớp hàm ngưỡng dưới $D_\eta$).** $K=6$, $\epsilon=0{,}1$, $\delta=0{,}05$, hàm lỗi 0–1. Bước: (1) $2K/\delta=240$, $\ln240\approx5{,}4806$; (2) $2\cdot5{,}4806/0{,}01\approx1096{,}1$; (3) $\lceil1096{,}1\rceil=1097$; (4) câu nghĩa: với ít nhất $1097$ quan sát, mọi nghiệm ERM có $L_{D_\eta}(\hat h)\le0{,}22+0{,}1=0{,}32$ với xác suất ít nhất $0{,}95$, dù dùng $A_{\min}$ hay $A_{\max}$; (5) so với Ví dụ 01.6: trên $S_\eta$ ($m=6$), $A_{\min}$ trả về $h_2$ với rủi ro vượt mức $0{,}10$, đúng ở biên. Câu cuối: cỡ mẫu không phụ thuộc $\eta$.
3. **Ví dụ 02.10 (ERM trên mọi hàm phân lớp của một tập đầu vào hữu hạn)** (QĐ 5 i; lời hứa ở §7(ii) của Bài 01). Bước: (1) $\mathcal H=\mathcal M_{\mathcal X}$, $K=2^{\lvert\mathcal X\rvert}$; (2) $h_{\mathrm{Bayes}}\in\mathcal M_{\mathcal X}$ (Mệnh đề 01.23(a)) nên $\min_{\mathcal M_{\mathcal X}}L_D=L_D^{\mathrm{Bayes}}$; (3) Hệ quả 02.16(c): $m\ge2(\lvert\mathcal X\rvert\ln2+\ln(2/\delta))/\epsilon^2$ đủ cho $L_D(\hat h)\le L_D^{\mathrm{Bayes}}+\epsilon$, cho mọi $D$; (4) số: $\lvert\mathcal X\rvert=5$: $5\ln2+\ln40\approx3{,}4657+3{,}6889=7{,}1546$, $2\cdot7{,}1546/0{,}01\approx1430{,}9$, $\lceil\cdot\rceil=1431$; dưới $D_\eta$: $L_{D_\eta}(\hat h)\le0{,}18+0{,}1=0{,}28$ với xác suất ít nhất $0{,}95$; (5) so với Ví dụ 02.9: $334$ quan sát thêm để so với rủi ro Bayes thay vì với $0{,}22$; (6) cỡ mẫu tăng tuyến tính theo $\lvert\mathcal X\rvert$, khớp Nhận xét 01.30; khi $\mathcal X$ vô hạn, cận này không cho gì. Câu cuối: với $\mathcal X$ hữu hạn, đối tượng so sánh rủi ro Bayes đạt được bằng ERM với cỡ mẫu không phụ thuộc phân bố.

### `## 8. Lớp hữu hạn trong trường hợp khả thực` (20 phút)

Câu mở: Hệ quả 02.16 cần $m$ tỉ lệ $1/\epsilon^2$; khi lớp chứa một hàm có rủi ro $0$, chỉ cần loại các hàm có rủi ro trên $\epsilon$ mà không sai lần nào trên mẫu.

1. **Mệnh đề 02.17 (Cỡ mẫu cho lớp hữu hạn trong trường hợp khả thực) — chứng minh đầy đủ** (blueprint Proposition 2.5; QĐ 6). **Giả thiết.** **Bài toán.** $\mathcal Y=\{0,1\}$, hàm lỗi 0–1; **Mẫu.** (T1); **Lớp.** (T4); **Khả thực.** $(D,\mathcal H)$ khả thực (Định nghĩa 01.16), chỉ dùng ở (c); **Tham số.** $\epsilon,\delta\in(0,1)$. **Bảo đảm.** Đặt $\mathcal H_{>\epsilon}=\{h\in\mathcal H:L_D(h)>\epsilon\}$, tập cố định (xác định bởi $D$, không bởi $S$). **(a)** Với mỗi $h\in\mathcal H_{>\epsilon}$, $\Pr_S[L_S(h)=0]<(1-\epsilon)^m\le e^{-\epsilon m}$, không cần khả thực. **(b)** $\Pr_S[\exists h\in\mathcal H_{>\epsilon}:L_S(h)=0]\le Ke^{-\epsilon m}$. **(c)** Dưới giả thiết khả thực, với mọi thuật toán ERM, $\Pr_S[L_D(\hat h)\le\epsilon]\ge1-Ke^{-\epsilon m}$; nếu $m\ge\ln(K/\delta)/\epsilon=[\ln K+\ln(1/\delta)]/\epsilon$ thì xác suất này ít nhất $1-\delta$, nên mọi thuật toán ERM là thuật toán học PAC (Định nghĩa 01.18) với $M(\epsilon,\delta)=\lceil\ln(K/\delta)/\epsilon\rceil$. Xác suất cao; rủi ro tuyệt đối, đối tượng so sánh $0$; biến cố một phía. **Chứng minh.** Lộ trình: xác suất một hàm xấu khớp mẫu, bất đẳng thức hợp trên các hàm xấu, khả thực để $\hat h$ khớp mẫu. Bước 1: $L_S(h)=0$ khi và chỉ khi $h(X_i)=Y_i$ với mọi $i$; **(T1)** cho $\Pr=(1-L_D(h))^m$; $L_D(h)>\epsilon$ và $1-x\le e^{-x}$. Bước 2: Bổ đề 02.12 trên $\mathcal H_{>\epsilon}$, $\lvert\mathcal H_{>\epsilon}\rvert\le K$ (**(T4)**). Bước 3: khả thực cho $L_S(h^\star)=0$ hầu chắc chắn, nên mọi nghiệm ERM có $L_S(\hat h)=0$ hầu chắc chắn (sau Định nghĩa 01.16 của Bài 01); do đó $\{L_D(\hat h)>\epsilon\}$ nằm trong biến cố của (b), sai khác một tập xác suất $0$. **Chỗ dùng khả thực chỉ ở Bước 3.** Bước 4: $Ke^{-\epsilon m}\le\delta$. Câu sau $\square$: bỏ khả thực thì (a), (b) vẫn đúng nhưng nghiệm ERM không còn khớp mẫu; khi đó cần Hệ quả 02.16.
2. **Ví dụ 02.11 (Ba mức cỡ mẫu cho bản nhãn tất định)** (QĐ 5 iii). $D_f$, lớp hàm ngưỡng, $\epsilon=0{,}1$, $\delta=0{,}05$. Bước: (1) Mệnh đề 02.17 với $K=6$: $\ln120\approx4{,}7875$, $/0{,}1\approx47{,}87$, $\lceil\cdot\rceil=48$; (2) lập luận riêng cho lớp hàm ngưỡng với $A_{\max}$ (§9 của Bài 01, Bài tập 01.9): $\lceil10\ln20\rceil=\lceil29{,}96\rceil=30$, đúng cho mọi phân bố khả thực; (3) giá trị riêng của $A_{\max}$ dưới $D_f$ (Ví dụ 01.9): $14$ ($0{,}8^{13}\approx0{,}0550$, $0{,}8^{14}\approx0{,}0440$); (4) câu nghĩa cho từng con số: cận cho mọi lớp $K$ phần tử, cận cho riêng lớp hàm ngưỡng, giá trị cho riêng một phân bố; (5) khoảng cách $48$ so với $30$ đến từ bất đẳng thức hợp: các biến cố "hàm ngưỡng xấu khớp mẫu" chồng lên nhau. Câu cuối: $48\ge30\ge14$ là ba mức của cùng một câu hỏi; chỉ hai mức đầu là bảo đảm không phụ thuộc phân bố.
3. **Ví dụ 02.12 (Bảng cỡ mẫu cho $K$ ứng viên)** (blueprint 2.4; QĐ 1). $\delta=0{,}05$; ba công thức: ước lượng đồng thời $\pm\epsilon$ $\lceil\ln(2K/\delta)/(2\epsilon^2)\rceil$ (Định lý 02.14(c); $K=1$ là Hệ quả 02.10(d)); rủi ro vượt mức $\le\epsilon$ $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$ (Hệ quả 02.16); khả thực $\lceil\ln(K/\delta)/\epsilon\rceil$ (Mệnh đề 02.17). Bước: (1) bảng log: $\ln(2K/\delta)=3{,}6889;\ 8{,}2940;\ 10{,}5966$ và $\ln(K/\delta)=2{,}9957;\ 7{,}6009;\ 9{,}9035$ cho $K=1;100;1000$; (2) một ô tính đầy đủ: $K=100$, $\epsilon=0{,}1$ bất khả tri: $2\cdot8{,}2940/0{,}01=1658{,}8\Rightarrow1659$; (3) bảng (cột $\epsilon=0{,}05$ / $0{,}1$):

   | $K$ | ước lượng $\pm\epsilon$ | rủi ro vượt mức $\le\epsilon$ | khả thực |
   |---|---|---|---|
   | 1 | 738 / 185 | 2952 / 738 | 60 / 30 |
   | 100 | 1659 / 415 | 6636 / 1659 | 153 / 77 |
   | 1000 | 2120 / 530 | 8478 / 2120 | 199 / 100 |

   (4) nhân $K$ lên $10$ lần (câu hỏi của blueprint): log tăng $\ln10\approx2{,}3026$, cỡ mẫu tăng thêm $115{,}1$ (ước lượng), $460{,}5$ (bất khả tri), $23{,}0$ (khả thực) ở $\epsilon=0{,}1$, ví dụ $415\to530$, $1659\to2120$, $77\to100$; (5) **nhận xét công bằng** (bắt buộc): chỉ cột ước lượng so sánh trực tiếp được giữa các $K$; cột bất khả tri bằng cột ước lượng tại $\epsilon/2$ (hai độ lệch $\epsilon/2$, nên gấp khoảng $4$ lần cùng hàng); cột khả thực chặn rủi ro tuyệt đối dưới một giả thiết thêm, với biến cố một phía, nên số nhỏ hơn không phải là "cùng bảo đảm với giá rẻ hơn"; (6) giảm $\epsilon$ một nửa nhân cột khả thực khoảng $2$ lần, hai cột kia khoảng $4$ lần. Câu cuối: chi phí thống kê của việc tìm trong $K$ ứng viên tăng theo $\ln K$.
4. **Nhận xét 02.18 (Hai tốc độ theo độ chính xác)** (QĐ 10). Trường hợp khả thực chỉ loại biến cố "một hàm có rủi ro trên $\epsilon$ khớp mẫu", xác suất $(1-\epsilon)^m$, ứng với biến Bernoulli có kì vọng gần $0$ và phương sai nhỏ; trường hợp bất khả tri có rủi ro gần $\tfrac12$, phương sai tới $\tfrac14$ (Ví dụ 02.3), độ lệch cỡ $1/\sqrt m$. Bất đẳng thức Bernstein dùng phương sai để nối hai chế độ (đọc thêm, UML Phụ lục B.5). Ghi rõ: bài **không** chứng minh $1/\epsilon^2$ là cần thiết; cận dưới cần lập luận cho mọi thuật toán (Bài 03).

### `## 9. Ý nghĩa, tác động và giới hạn` (văn xuôi, 4–5 đoạn ngắn, không nhãn)

1. **Bảo đảm cho lớp và cho thuật toán.** Định lý 02.14 là bảo đảm cho lớp, đúng cho mọi quy tắc dựa trên $L_S$; Hệ quả 02.16 và Mệnh đề 02.17 là bảo đảm cho mọi thuật toán ERM (mọi quy tắc chọn khi bằng nhau), khác Bài 01 nơi quy tắc chọn quyết định rủi ro (Mệnh đề 01.15).
2. **Chi phí lôgarit của việc tìm mô hình.** Bảng Ví dụ 02.12; dùng Chebyshev với bất đẳng thức hợp thì cỡ mẫu là $K/(4\delta\epsilon^2)$: với $K=1000$, $\epsilon=\delta=0{,}05$ là $2\,000\,000$, so với $2120$ của Hoeffding; đuôi mũ là lý do chi phí chỉ là $\ln K$.
3. **Tính bảo thủ.** Ví dụ 02.4: $0{,}2707$ so với $0{,}0211$; cận không phụ thuộc phân bố, nên lớn hơn giá trị cho một phân bố cụ thể; bất đẳng thức hợp lỏng khi các giả thuyết giống nhau ($48$ so với $30$).
4. **Không chuyển sang hàm lỗi không bị chặn** (Nhận xét 02.11): hàm lỗi bình phương, hàm lỗi log cần lập luận mới (Bài 05–06 với giả thiết khác).
5. **Lớp phụ thuộc dữ liệu và dùng lại mẫu xác thực** (PTN §2.6–2.7). Lớp phải cố định trước mẫu dùng để đánh giá (T4); lập danh sách ứng viên sau khi xem điểm trên $S$, hoặc dùng lại $S$ để thiết kế ứng viên mới theo điểm cũ (dùng lại thích nghi), làm hỏng Bước 2 của chứng minh Định lý 02.14. Cách sửa: một mẫu mới, hoặc cố định trước một họ đếm được với trọng số và chia $\delta$ (Bài tập 02.6; Bài 04).
6. **Điều không khẳng định.** $1/\epsilon^2$ không được chứng minh là cần thiết; không nói gì về lớp vô hạn; không có cận dưới.

### `## 10. Bài tập`, `## 11. Câu hỏi cuối buổi và cầu nối`, `## 12. Tài liệu đọc`

Theo mục 4, 6, 7 của dàn ý. Câu nói về Bài 03 chỉ nằm ở §11.

### `## Phụ lục`

Theo mục 8 của dàn ý.

## 4. Kế hoạch bài tập (`exercises.md`, viết sau khi ghi chú qua rà soát)

Danh sách ở §10 của ghi chú: một dòng mỗi bài (tên, mục tiêu đo). Đề, gợi ý tăng dần, lời giải đầy đủ trong `exercises.md`; bài gốc và bài UML tách riêng (QĐ 9). Mức: KN khái niệm, TT tính toán, CM chứng minh, GT kiểm tra giả thiết, TN thực nghiệm tùy chọn.

**Bài gốc (blueprint 2.5).**

1. **Bài tập 02.1 (Markov, Chebyshev và các giả thiết yếu hơn)** — mục tiêu 1; CM+TT. (a) Dấu bằng của Markov: $V\in\{0,\alpha\}$. (b) Bổ đề 02.3(b) chỉ cần không tương quan từng đôi (hiệp phương sai bằng $0$). (c) $V_1,V_2$ là hai bit đều độc lập, $V_3=V_1\oplus V_2$: độc lập từng đôi, không độc lập; (b) áp dụng nhưng Bổ đề 02.5(b) hỏng: $\mathbb Ee^{\tau(V_1+V_2+V_3)}=(1+3e^{2\tau})/4$ so với $\big((1+e^\tau)/2\big)^3$, tại $\tau=1$: $5{,}792$ so với $6{,}426$†. (d) Cỡ mẫu Chebyshev không phụ thuộc phân bố $2000$ so với Hoeffding $738$ ($\epsilon=\delta=0{,}05$).
2. **Bài tập 02.2 (Bất đẳng thức Hoeffding với miền giá trị khác nhau)** — mục tiêu 1; CM. Đổi theo QĐ 9 (ghi chú đã chứng minh đầy đủ bản một phía). Chứng minh Nhận xét 02.8. Áp dụng: $m=1000$, $900$ biến trong $[0,1]$ và $100$ biến trong $[0,4]$, $\epsilon=0{,}1$: $\sum(b_i-a_i)^2=2500$, cận một phía $e^{-8}\approx3{,}4\cdot10^{-4}$†; nếu chỉ dùng miền chung $[0,4]$: $e^{-1{,}25}\approx0{,}287$†.
3. **Bài tập 02.3 (Hệ số hai trong bảo đảm của ERM)** — mục tiêu 3; KN+CM. (a) Chỉ ra hai phép so sánh tạo ra $2r_m$. (b, thử thách, QĐ 8) Chỉ cần $K$ biến cố một phía trên và một biến cố một phía dưới tại $h^\star$ cố định: bán kính $\sqrt{\ln((K+1)/\delta)/(2m)}$; $K=100$, $\delta=0{,}05$: $\ln2020\approx7{,}611$ so với $\ln4000\approx8{,}294$; cỡ mẫu $\epsilon=0{,}1$: $1523$† so với $1659$.
4. **Bài tập 02.4 (Phản ví dụ cho bất đẳng thức hợp bỏ số ứng viên)** — mục tiêu 6; GT. Cấu trúc PTN §4(c): $Y=0$, $X$ đều trên $\{0,1\}^K$, $h_k(x)=x_k$, $L_D(h_k)=\tfrac12$, $m=10$, $\epsilon=0{,}4$: $\Pr[\exists k:L_S(h_k)=0]=1-(1-2^{-10})^K=0{,}6236$ ($K=1000$), $0{,}9924$ ($K=5000$), trong khi cận bỏ $K$ là $2e^{-3{,}2}\approx0{,}0815$; có hệ số $K$ thì cận $\ge1$, không mâu thuẫn.
5. **Bài tập 02.5 (So sánh cận giải tích với mô phỏng Bernoulli)** — mục tiêu 2; TN, tùy chọn; chỉ mô tả giao thức (QĐ 9). $q=0{,}22$, $m\in\{100,200\}$, $\epsilon=0{,}1$, $R=10\,000$ lần lặp độc lập; báo cáo tần suất thất bại kèm sai số chuẩn, so với giá trị chính xác ($0{,}0211$; $8{,}9\cdot10^{-4}$) và các cận của Ví dụ 02.4; phần mở rộng: lặp lại cấu trúc của Ví dụ 02.7. Sản phẩm là tần suất trên nhiều lần chạy, không phải một lần chạy (blueprint E). Không đưa mã vào repo.
6. **Bài tập 02.6 (Bất đẳng thức hợp có trọng số trên lớp đếm được)** — mục tiêu 3; CM; chuẩn bị Bài 04. Trọng số $w_k\ge0$, $\sum_kw_k\le1$, chọn trước mẫu: với xác suất ít nhất $1-\delta$, mọi $k$: $\lvert L_S(h_k)-L_D(h_k)\rvert\le\sqrt{\ln(2/(w_k\delta))/(2m)}$. Số: $w_k=2^{-k}$, $k=10$, $m=1000$, $\delta=0{,}05$: $\ln40960\approx10{,}620$, bán kính $\approx0{,}0729$†, gần bán kính $0{,}0728$ của $K=1000$ trọng số đều.

**Bài chọn từ UML (số đã kiểm tra trên PDF; đánh số theo thứ tự UML như Bài 01).**

7. **Bài tập 02.7 (Hình chữ nhật song song với trục trong trường hợp khả thực; UML Bài tập 2.3 ý 1–2)** — mục tiêu 4; CM, khó vừa. Thuật toán chữ nhật nhỏ nhất chứa mọi điểm dương là ERM; $m\ge4\ln(4/\delta)/\epsilon$ đủ; $\epsilon=0{,}1$, $\delta=0{,}05$: $40\ln80\approx175{,}3\Rightarrow176$. Hai chỗ hổng của bản lời giải phải xử lý (QĐ 9): phân bố có nguyên tử (lấy dải đóng nhỏ nhất có khối lượng $\ge\epsilon/4$) và mẫu không có điểm dương (quy ước thêm hàm âm toàn phần). Ý nghĩa: bất đẳng thức hợp trên $4$ biến cố, không trên giả thuyết, cho một lớp vô hạn; cầu nối Bài 03. Ý 3–4 (chiều $p$, thời gian chạy) chỉ là gợi ý mở rộng, dùng $p$ thay $d$ của UML.
8. **Bài tập 02.8 (Lớp hội Boole; UML Bài tập 3.4)** — mục tiêu 4; CM+TT. $\mathcal X=\{0,1\}^p$ (UML viết $d$); $\lvert\mathcal H\rvert=3^p+1$; Mệnh đề 02.17: $p=10$, $\epsilon=0{,}1$, $\delta=0{,}05$: $(\ln59050+\ln20)/0{,}1\approx139{,}8\Rightarrow140$; ERM bằng phép loại literal, $O(mp)$. Ghi chỗ hổng của bản lời giải (bỏ "+1").
9. **Bài tập 02.9 (Quan sát độc lập nhưng không cùng phân bố; UML Bài tập 3.5)** — mục tiêu 1; CM. $\Pr[\exists h:L_{\bar D_m}(h)>\epsilon,\ L_S(h)=0]\le Ke^{-\epsilon m}$ qua bất đẳng thức trung bình cộng–trung bình nhân; nối với Định lý 02.7 (không cần cùng phân bố). Viết lại bằng nhãn $y=f(x)$, không dùng kí hiệu $L_{(D,f)}$ của UML.
10. **Bài tập 02.10 (Kì vọng và xác suất cao; UML Bài tập 4.1)** — mục tiêu 1; CM. Một $D$ cố định, hàm lỗi trong $[0,1]$: tương đương giữa "$\forall\epsilon,\delta\ \exists m(\epsilon,\delta)$: $\Pr[L_D(A(S))>\epsilon]<\delta$ khi $m\ge m(\epsilon,\delta)$" và $\mathbb E_SL_D(A(S))\to0$; hai chiều dùng Markov và $\mathbb E\le\epsilon+\Pr[>\epsilon]$. Ghi: khẳng định theo từng phân bố, không phải PAC; dấu "$<\delta$" cần $\mathbb E\le\epsilon\delta/2$ (chỗ hổng của bản lời giải).
11. **Bài tập 02.11 (Hàm lỗi có trọng số trong $[0,4]$; UML Bài tập 4.2)** — mục tiêu 4; TT+CM. Phát biểu với $\ell_c$, $(c_{FP},c_{FN})=(1,4)$, **không dùng $m^{UC}_{\mathcal H}$** (QĐ 3): mọi thuật toán ERM là thuật toán học PAC bất khả tri với $M=\lceil2(b-a)^2\ln(2K/\delta)/\epsilon^2\rceil$; lớp hàm ngưỡng, $\epsilon=0{,}1$ (đơn vị chi phí), $\delta=0{,}05$: $32\ln240/0{,}01\approx17\,538{,}04\Rightarrow17\,539$, gấp $16$ lần so với $1097$. Ghi sai hằng số của bản lời giải.

## 5. Ý nghĩa, tác động và giới hạn

Nội dung bắt buộc ở §9 của mục 3. Thứ tự đoạn: bảo đảm cho lớp/thuật toán → chi phí $\ln K$ → bảo thủ → hàm lỗi không bị chặn → lớp phụ thuộc dữ liệu → điều không khẳng định. Mỗi đoạn kết bằng một đại lượng cụ thể (van-phong §8).

## 6. Câu hỏi cuối buổi và cầu nối

**Câu hỏi.** Một hàm phân lớp được chọn trong $200$ ứng viên vì có tỉ lệ lỗi nhỏ nhất, $8\%$, trên một mẫu xác thực gồm $2000$ quan sát. Tính một cận trên tin cậy $95\%$ cho rủi ro kì vọng của nó. Cận này đúng cho những hàm nào?

**Câu hỏi phụ.** Bước nào của chứng minh Định lý 02.14 hỏng nếu danh sách $200$ ứng viên được lập sau khi xem tỉ lệ lỗi trên chính mẫu xác thực đó?

*Lời giải (khối `solution`).* $\ln(200/0{,}05)=\ln4000\approx8{,}294$; $r_m^{+}=\sqrt{8{,}294/4000}\approx0{,}0455$†; cận $0{,}08+0{,}0455\approx0{,}126$†, đúng đồng thời cho cả $200$ ứng viên, nên cho hàm được chọn. Câu phụ: Bước 2 (mỗi $h$ cố định đối với $S$); giả thiết (T4) hỏng.

**Cầu nối sang Bài 03** (một đoạn): lớp hàm ngưỡng trên $\mathbb R$ và lớp nửa không gian là vô hạn; cận của Định lý 02.14 phụ thuộc $\ln\lvert\mathcal H\rvert$ nên không cho gì. Tuy vậy lập luận của Bài tập 01.9 cho lớp hình tròn đồng tâm và Bài tập 02.7 cho hình chữ nhật cho cận cỡ mẫu với lớp vô hạn trong trường hợp khả thực. Câu hỏi cho Bài 03: đại lượng nào thay $\ln\lvert\mathcal H\rvert$ cho một lớp vô hạn? Không nêu tên chiều VC ngoài một câu dẫn nếu cần.

## 7. Tài liệu đọc (theo mục UML; đề xuất chia trước/sau)

- **Trước buổi học:** UML Phụ lục B.1–B.2 (Markov, Chebyshev); đọc lại §2.3.1 (lớp hữu hạn khả thực, đã giao sau Bài 01).
- **Sau buổi học:** UML Phụ lục B.3–B.4 (Chernoff, Hoeffding), §§4.1–4.2 (hội tụ đều đủ cho học được; lớp hữu hạn học được PAC bất khả tri); các bài tập UML §2.4, §3.5, §4.5 đã chọn.
- **Mở rộng:** UML Phụ lục B.5 (Bennett, Bernstein; cận dùng phương sai); không cần cho Bài 03.

Đoạn "Quan hệ với giáo trình UML" (như Bài 01, 4–5 câu): Hoeffding không cần cùng phân bố và dùng biến cố "$\ge$"; Markov với $\alpha>0$; hàm sinh mô-men được đặt tên; khả thực viết với $D$ đồng thời thay cho $(D,f)$; bảo đảm cho mọi quy tắc chọn khi bằng nhau và cho ERM xấp xỉ; mẫu $\epsilon$-đại diện chỉ dùng như một biến cố, tính chất hội tụ đều của lớp để Bài 03; viết $\ln$ thay $\log$.

## 8. Phụ lục (≤ 1 500 tiếng)

- **A. Bất đẳng thức vô hướng của bổ đề Hoeffding** (chứng minh đầy đủ, khoảng 450 tiếng). Cho $\theta\in[0,1]$, $\varphi(u)=-\theta u+\ln(1-\theta+\theta e^u)$, $u\in\mathbb R$; đối số của $\ln$ dương. Bước: $\varphi(0)=0$; $\varphi'(u)=-\theta+\rho(u)$ với $\rho(u)=\theta e^u/(1-\theta+\theta e^u)\in[0,1]$, nên $\varphi'(0)=0$; $\varphi''(u)=\rho(u)(1-\rho(u))\le\tfrac14$ (viết đạo hàm của $\rho$: $\rho'=\rho(1-\rho)$); Taylor với phần dư Lagrange: $\varphi(u)=\tfrac12\varphi''(\xi)u^2\le u^2/8$ với $\xi$ giữa $0$ và $u$. Kí hiệu $\xi$ ở đây là điểm trung gian của định lý Taylor; **đổi thành $c_u$ hoặc $\bar u$** để tránh $\xi$ (nguồn ngẫu nhiên nội tại trong `ky-hieu.md`). Câu cuối nối về Bước 4 của Bổ đề 02.6.
- **B. Tính toán chi tiết cho các ví dụ** (khoảng 800 tiếng). B.1 Xác suất đuôi chính xác của $L_S(h_3)$: tập $k$ thỏa $\lvert k/m-0{,}22\rvert\ge0{,}1$ ($m=100$: $k\le12$ hoặc $k\ge32$; $m=200$: $k\le24$ hoặc $k\ge64$), tổng nhị thức, giá trị $0{,}0211$ và $8{,}9\cdot10^{-4}$; ghi rằng biến cố "$>$" cho $0{,}0109$ và $4{,}9\cdot10^{-4}$, vì $k/m$ chạm đúng biên. B.2 Ví dụ 02.7: $\Pr[\mathrm{Bin}(1000;0{,}07)\le50]=0{,}00593$; $(1-0{,}00593)^{1000}=0{,}0026$. B.3 Các log và trần của bảng Ví dụ 02.12 (một dòng mỗi ô).
- Không đưa vào Phụ lục: chứng minh Bernstein, cận dưới, đo được tổng quát.

## 9. Thuật ngữ mới (chưa có trong `thuat-ngu.md`; điều phối viên bổ sung mục 6 trước khi viết)

`thuat-ngu.md` §6 đã có: xác suất đuôi, cận đuôi, bất đẳng thức tập trung, bất đẳng thức Markov/Chebyshev, phương pháp Chernoff, hàm sinh mô-men, bổ đề Hoeffding, bất đẳng thức Hoeffding, bất đẳng thức hợp, hội tụ đều, mẫu $\epsilon$-đại diện, khoảng tin cậy, lớp hữu hạn, giả thuyết nhất quán với mẫu; §8 đã có mẫu xác thực, tập xác thực. Đề xuất thêm:

| English | Đề xuất | Ghi chú |
|---|---|---|
| upper confidence bound, confidence bound | cận trên tin cậy, cận tin cậy | Định nghĩa 02.9 |
| confidence radius | bán kính tin cậy | $r_m$, $r_m^{+}$ |
| one-sided / two-sided bound | cận một phía / cận hai phía | |
| selection bias | thiên lệch do chọn | tránh "độ lệch" (dành cho bias thống kê, Bài 04) và "thiên kiến" (thiên kiến quy nạp) |
| candidate (model) | ứng viên | |
| validation sample | mẫu xác thực | đã có ở §8 (Bài 04); Bài 02 dùng trước, cần chốt sớm |
| heavy tail | đuôi nặng | |
| Bernoulli / binomial distribution | phân bố Bernoulli / phân bố nhị thức | |
| covariance; pairwise uncorrelated; pairwise independent | hiệp phương sai; không tương quan từng đôi; độc lập từng đôi | Bài tập 02.1 |
| chord (of a convex function) | dây cung | Bổ đề 02.6 |
| Taylor expansion with Lagrange remainder | khai triển Taylor với phần dư Lagrange | Phụ lục A |
| adaptive reuse (of a validation sample) | dùng lại thích nghi | §9 |
| data-dependent class | lớp phụ thuộc dữ liệu | §9 |
| weighted union bound | bất đẳng thức hợp có trọng số | Bài tập 02.6 |
| Bernstein's inequality | bất đẳng thức Bernstein | Nhận xét 02.18 |
| AM–GM inequality | bất đẳng thức trung bình cộng–trung bình nhân | Bài tập 02.9 |
| axis-aligned rectangle | hình chữ nhật song song với trục | Bài tập 02.7 |
| Boolean conjunction; literal | hội Boole; literal (giữ tiếng Anh, giải thích "một biến hoặc phủ định của nó") | Bài tập 02.8; điểm mở 4 |
| failure frequency (simulation) | tần suất thất bại | Bài tập 02.5 |

## 10. Kí hiệu mới (đối chiếu `ky-hieu.md`)

| Kí hiệu | Nghĩa | Lý do / xung đột tránh |
|---|---|---|
| $V$, $V_i$, $\bar V_m$, $\mu_i$, $\bar\mu_m$ | biến ngẫu nhiên tổng quát, trung bình mẫu, kì vọng | không dùng $X_i$ (blueprint, UML) vì $X$ là đầu vào; không dùng $U$ vì $U[0,1]$ ở Bài 01 |
| $\alpha$ | mức trong xác suất đuôi, Markov, Chernoff | không dùng $a$ vì $[a,b]$ là miền giá trị; không dùng $\epsilon$ cho mức không phải độ lệch |
| $\tau$ | tham số của hàm mũ (hàm sinh mô-men, Chernoff, Hoeffding) | $t$ trùng chỉ số ngưỡng $h_t$; $\lambda$ đã dành cho hệ số chính quy hóa; điểm mở 1 |
| hàm sinh mô-men: **không đặt kí hiệu**, viết $\mathbb Ee^{\tau V}$ | — | $M_X(t)$ trùng $M(\epsilon,\delta)$ và gần $\mathcal M_{\mathcal X}$; nếu điều phối viên muốn một kí hiệu, đề xuất $\psi_V(\tau)$ |
| $q$ | tham số của phân bố Bernoulli | $p$ là số chiều đặc trưng |
| $K=\lvert\mathcal H\rvert$ | số giả thuyết của lớp hữu hạn | Bài 01 dùng $K$ cục bộ trong Thuật toán 01.13 (số mức); không trùng trong Bài 02 |
| $r_m$, $r_m^{+}$ | bán kính hai phía $\sqrt{\ln(2K/\delta)/(2m)}$, một phía $\sqrt{\ln(K/\delta)/(2m)}$ | phụ thuộc ngầm $K$, $\delta$; ghi rõ ở Định lý 02.14 |
| $\overline L_\delta(S)$, $\underline L_\delta(S)$ | cận trên, cận dưới tin cậy | dạng gạch trên/dưới của $L$ vì chúng chặn rủi ro |
| $\mathcal H_{>\epsilon}$ | $\{h\in\mathcal H:L_D(h)>\epsilon\}$ | thay $\mathcal H_B$ của UML |
| $B_h$, $B_k$ | biến cố hỏng | chỉ trong chứng minh |
| $\varphi$, $\theta$, $u$ | hàm vô hướng và tham số của Phụ lục A | thay $L(u)$ của UML (trùng $L_D$, $L_S$) và $p$ của UML (trùng số chiều) |
| (T3), (T4) | hàm lỗi bị chặn; lớp hữu hạn chọn trước mẫu | tiếp (T1), (T2) của Bài 01 |

## 11. Phân bổ thời gian và ngân sách độ dài

### 11.1 Phân bổ thời gian 140 phút (chỉ trong dàn ý)

| Khối blueprint 2.6 | Phút | Mục ghi chú | Nội dung giảng |
|---|---|---|---|
| Động cơ | 10 | Câu hỏi mở đầu đến §3 | câu hỏi $5\%$, $1000$ ứng viên; ba câu ôn nhanh; nhắc ví dụ sàng lọc |
| Markov/Chebyshev | 20 | §4 | Định nghĩa 02.1, Ví dụ 02.2 ($m=6$ tính tay), Bổ đề 02.2, 02.3 có chứng minh, Ví dụ 02.3 |
| Chernoff/Hoeffding | 40 | §5 | Bổ đề 02.5; Bổ đề 02.6 bước lồi (Phụ lục A tự đọc); Định lý 02.7 chứng minh đầy đủ; Hệ quả 02.10; Ví dụ 02.4, 02.5, 02.6; Nhận xét 02.8, 02.11 nêu lướt |
| Nghỉ | 10 | — | — |
| Hội tụ đều và ERM | 35 | §6–§7 | Ví dụ 02.7 (kết quả, không tính chi tiết); Bổ đề 02.12; Định nghĩa 02.13; Định lý 02.14 chứng minh; Ví dụ 02.8; Hệ quả 02.16 chứng minh; Ví dụ 02.9, 02.10 |
| Khả thực | 20 | §8 | Mệnh đề 02.17 chứng minh; Ví dụ 02.11; Ví dụ 02.12 (bảng, nhận xét công bằng); Nhận xét 02.18 |
| Bài tập và câu hỏi cuối buổi | 15 | §9–§11 | ý nghĩa và giới hạn; chữa nhanh Bài tập 02.3(a) hoặc 02.4; câu hỏi cuối buổi |

Nếu 150 phút là thời gian giảng không tính nghỉ: 10 phút dư chữa trọn Bài tập 02.4.

### 11.2 Ngân sách độ dài

Đếm như Bài 01: `wc -w` trên Markdown, gồm công thức; thân bài là từ dòng đầu đến trước `## Phụ lục`. Bài 01 thực tế: thân $13\,234$, phụ lục $1\,631$ (đếm ngày 2026-10-30), vượt mức; Bài 02 phải giữ **thân ≤ 11 000, phụ lục ≤ 1 500** (QĐ 10).

| Phần | Tiếng | Phần | Tiếng |
|---|---|---|---|
| Tiêu đề, đoạn dẫn | 150 | §5 | 2 400 |
| Câu hỏi mở đầu | 250 | §6 | 1 550 |
| Mục tiêu | 150 | §7 | 1 100 |
| Tiên quyết, ôn nhanh | 350 | §8 | 1 350 |
| §1 | 450 | §9 | 500 |
| §2 | 250 | §10 | 200 |
| §3 | 350 | §11 | 350 |
| §4 | 1 300 | §12 | 150 |

Tổng thân bài khoảng $10\,850$. **Thứ tự cắt khi vượt:** (1) Ví dụ 02.7 rút thành hai câu trong Ví dụ 02.8, số chuyển sang Phụ lục B.2; (2) bỏ bước Markov của Ví dụ 02.3; (3) Nhận xét 02.8 còn một câu; (4) Ví dụ 02.4 bỏ cột $m=6$; (5) Ví dụ 02.12 chỉ giữ cột $\epsilon=0{,}1$. **Không cắt:** chứng minh của 02.7, 02.14, 02.16, 02.17; Ví dụ 02.6 và Nhận xét 02.11 (QĐ 7); con số $1431$ (QĐ 5 i); ba mức $48/30/14$ (QĐ 5 iii); nhận xét công bằng của Ví dụ 02.12.

**Giai đoạn viết** (mỗi giai đoạn khoảng 150 dòng, điều phối viên đọc sau mỗi giai đoạn): (1) tiêu đề đến §3; (2) §4 và §5 đến Định lý 02.7; (3) phần còn lại của §5; (4) §6–§7; (5) §8–§12 và Phụ lục.

## 12. Rủi ro, điểm mở và danh sách con số †

**Kiểm tra tham chiếu tới trước (đã chạy trên giấy theo thứ tự mục 3).** Mỗi khối chỉ dùng khối đứng trước, kết quả Bài 01 và kiến thức tiên quyết. Ba chỗ dễ sai đã xử lý: (i) Định lý 02.7(c) dùng tính rời nhau, không dùng Bổ đề 02.12; (ii) Ví dụ 02.7 không dùng bất đẳng thức hợp; (iii) các giả thiết (T3), (T4) và khả thực được nêu ngay trước khối dùng chúng. Câu hỏi mở đầu và §2 chỉ dẫn số mục, không dẫn số khối.

**Quyết định của điều phối viên được phản ánh:** QĐ 1 (§3, Ví dụ 02.1, ứng dụng); QĐ 2 (Định lý 02.7 hai phần một phía và hai phía, "$\ge$", Nhận xét 02.8; Markov, Chebyshev, Chernoff, bất đẳng thức hợp là Bổ đề có số; Bổ đề 02.6 phác thảo, Phụ lục A); QĐ 3 (Định nghĩa 02.9 sau Định lý 02.7; Định nghĩa 02.13 sau Bổ đề 02.12; không có $m^{UC}$); QĐ 4 (Hệ quả 02.16 (a)–(c)); QĐ 5 (Ví dụ 02.10, Nhận xét 02.15, Ví dụ 02.11); QĐ 6 (Mệnh đề 02.17(a) và Bước 3); QĐ 7 (Ví dụ 02.6, Nhận xét 02.11, Ví dụ 02.7 tùy độ dài; phản ví dụ (c) ở Bài tập 02.4); QĐ 8 (Bài tập 02.3(b)); QĐ 9 (mục 4); QĐ 10 (Nhận xét 02.18, §9, ngân sách).

**Điểm khác blueprint hoặc PTN, cần điều phối viên xác nhận:**

1. **Xác suất đuôi chính xác với "$\ge$".** PTN tính $\Pr(\lvert L_S(h_3)-0{,}22\rvert>0{,}1)$: $0{,}0109$ và $4{,}9\cdot10^{-4}$ ở $m=100,200$. Với biến cố "$\ge$" của QĐ 2, $k/m$ chạm đúng biên ($k=12,32$ ở $m=100$; $k=24,64$ ở $m=200$), nên giá trị là $0{,}0211$† và $8{,}9\cdot10^{-4}$†. Ở $m=6$ hai giá trị trùng nhau ($0{,}6189$). Dàn ý dùng "$\ge$" để khớp Định nghĩa 02.1 và Định lý 02.7.
2. **Ví dụ thiên lệch do chọn** dùng xác suất chính xác ($0{,}6\%$ so với $99{,}7\%$), không dùng khoảng chuẩn xấp xỉ của PTN: khoảng Hoeffding cho hàm cố định $[0{,}007;0{,}093]$ vẫn chứa $0{,}07$, nên ví dụ không thể nói "khoảng cho hàm cố định sai".
3. **Định lý 02.7 với miền $[a,b]$** thay vì $[0,1]$ của blueprint; cần cho $\ell_c$ (Bài tập 02.11) và không làm dài chứng minh.
4. **Định lý 02.14(b) một phía** thêm so với blueprint: dùng cho câu hỏi mở đầu, Nhận xét 02.15 và câu hỏi cuối buổi.
5. **Bài tập 02.1** không yêu cầu chứng minh lại Markov và Chebyshev (ghi chú đã chứng minh đầy đủ), mà kiểm tra giả thiết yếu hơn, đúng mục tiêu của blueprint.

**Điểm mở cho điều phối viên:**

1. Tham số mũ: $\tau$ (dàn ý), $t$ (thông dụng nhưng trùng $h_t$) hay $\lambda$ (UML, nhưng trùng hệ số chính quy hóa của `ky-hieu.md`)?
2. Chốt "mẫu xác thực" (đã có ở `thuat-ngu.md` §8 cho Bài 04, còn ghi "còn mở" ở §14) cho Bài 02.
3. Kí hiệu $r_m^{+}$ cho bán kính một phía, hay viết thẳng biểu thức?
4. "Literal" giữ tiếng Anh trong Bài tập 02.8?
5. Giữ Ví dụ 02.7 trong thân bài (khoảng 250 tiếng) hay đưa thẳng vào Phụ lục B.2?

**Rủi ro cho bản thảo:**

- **Ba nghĩa của $\epsilon$** (độ chính xác ước lượng, rủi ro vượt mức, rủi ro tuyệt đối khi khả thực): mỗi ví dụ ghi rõ đang dùng nghĩa nào; nhận xét công bằng ở Ví dụ 02.12 là bắt buộc.
- **"Với mỗi $h$" và "đồng thời cho mọi $h$"**: Hệ quả 02.10 chỉ là "với mỗi $h$ cố định"; mọi phát biểu cho $\hat h$ dẫn Định lý 02.14.
- **Chebyshev thắng Hoeffding ở $m=100$**: viết đúng như vậy; không viết "Hoeffding luôn tốt hơn".
- **Không chép UML:** không dùng $L_{(D,f)}$, $\mathcal H_B$, "misleading samples", $\delta$ hay $h$ theo nghĩa của UML B.3, nhận xét rời rạc hóa $2^{64d}$ (PTN §3).
- **Lẫn hai bản của ví dụ sàng lọc:** mỗi ví dụ ghi $D_\eta$ hay $D_f$, hàm lỗi 0–1 hay $\ell_c$.
- **Lập luận điều kiện cho mẫu xác thực** (Ví dụ 02.8 bước 1) dễ bị viết tắt; người rà toán kiểm tra.
- **Độ dài:** Bài 01 vượt $2\,200$ tiếng so với mục tiêu; người viết đếm sau mỗi giai đoạn.

**Danh sách con số † (đều đã tính lại; phép tính rút gọn):**

| Con số | Phép tính | Dùng ở |
|---|---|---|
| $0{,}539$ | $\Pr(\mathrm{Bin}(100;0{,}22)\ge22)=0{,}5391$ | Định nghĩa 02.1, 02.9 (phản ví dụ) |
| $0{,}0211$; $8{,}9\cdot10^{-4}$ | $\Pr(\lvert k/m-0{,}22\rvert\ge0{,}1)$, $k\sim\mathrm{Bin}(m;0{,}22)$, $m=100$: $0{,}02115$; $m=200$: $0{,}000894$ | Ví dụ 02.2, 02.4, Phụ lục B.1, Bài tập 02.5 |
| $0{,}6875$; $0{,}3937$; $0{,}0134$; $6{,}9\cdot10^{-4}$ | $0{,}22/0{,}32$; $\Pr(k/m\ge0{,}32)$ ở $m=6,100,200$ | Ví dụ 02.3 |
| $4{,}17$; $0{,}25$; $0{,}125$; $500$ | $25/m$ ở $m=6,100,200$; $1/(4\cdot0{,}05\cdot0{,}01)$ | Ví dụ 02.3, 02.4 |
| $1{,}1059\le1{,}1331$ | $0{,}78e^{-0{,}22}+0{,}22e^{0{,}78}$; $e^{1/8}$ | Bổ đề 02.6 (tùy chọn) |
| $0{,}0887$ | $0{,}05+\sqrt{\ln20/2000}=0{,}05+0{,}0387$ | Ví dụ 02.5 |
| $0{,}1204$; $0{,}1259$ | $0{,}05+0{,}07037$; $0{,}05+\sqrt{\ln10^5/2000}=0{,}05+0{,}07587$ | Ví dụ 02.8 |
| $-0{,}02;\ 0{,}0133;\ 0{,}1133;\ 0{,}18;\ 0{,}0533;\ 0{,}02$ | $L_{S_\eta}(h_t)-L_{D_\eta}(h_t)$ từ Ví dụ 01.5, 01.2 | Định nghĩa 02.13 |
| $0{,}0455$; $0{,}126$ | $\sqrt{\ln4000/4000}=\sqrt{8{,}2940/4000}=0{,}04554$; $0{,}08+0{,}0455$ | câu hỏi cuối buổi |
| $5{,}792$; $6{,}426$ | $(1+3e^2)/4$; $\big((1+e)/2\big)^3$ | Bài tập 02.1 |
| $3{,}4\cdot10^{-4}$; $0{,}287$ | $\exp(-2\cdot10^6\cdot0{,}01/2500)=e^{-8}$; $\exp(-2\cdot10^6\cdot0{,}01/16000)=e^{-1{,}25}$ | Bài tập 02.2 |
| $1523$ | $2\ln(101/0{,}05)/0{,}01=2\cdot7{,}6109/0{,}01=1522{,}2$ | Bài tập 02.3 |
| $0{,}0729$ | $\sqrt{\ln(2\cdot2^{10}/0{,}05)/2000}=\sqrt{10{,}6204/2000}$ | Bài tập 02.6 |
| $334$ | $1431-1097$ | Ví dụ 02.10 |

Các con số còn lại (bảng thực đơn, $1097$, $1431$, $48/30/14$, bán kính câu hỏi mở đầu, $0{,}00593$, $0{,}9974$, $2e^{-8}$, $0{,}9900$, $0{,}6236$, $0{,}9924$, $0{,}0815$, $176$, $140$, $17\,539$, $2\,000\,000$, $1521$) lấy từ PTN và đã được tính lại trong phiên này: khớp.
