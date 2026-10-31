# Nhật ký rà soát — Bài 09: Học chuỗi và mô hình sinh

Tệp nội bộ. Ghi tác tử, quyết định của điều phối viên, phát hiện rà soát và nguồn đã tham khảo.

Căn cứ bắt đầu (2026-10-31): người dùng giao lần lượt soạn ghi chú và bài tập Bài 07–10 theo blueprint, commit và push sau mỗi bài (xem `../lec-07/review-log.md`). Các yêu cầu rút ra từ Bài 01–08 áp dụng ngay từ bản thảo.

**Nguồn bổ sung.** Theo blueprint §F (cùng lý do như Bài 07): Kingma, Welling (2014), *Auto-Encoding Variational Bayes*, cho mục tiêu biến phân và tham số hóa lại. Bản arXiv:1312.6114v11 tải về `sources/supp/` (gitignore), ghi ở `sources/README.md`. Bước phân tích nguồn chạy song song với bước soạn ghi chú Bài 08: tác tử phân tích nguồn chỉ đọc repo, báo cáo ghi vào scratchpad, điều phối viên chép vào `source-analysis.md`.

Lời hứa cần giữ: Bài 02 dòng 574 (hàm lỗi log không bị chặn); cầu nối cuối Bài 08 (khi viết xong; blueprint 8.6: cùng ngôn ngữ rủi ro cho mô hình xác suất, quan sát là một chuỗi, hàm lỗi là log-likelihood).

## Tác tử

| Bước | Vai trò | Loại | Mô hình | Mức | Bằng chứng |
|---|---|---|---|---|---|
| 2026-10-31 · 1 | Phân tích nguồn UML và Kingma–Welling (chỉ đọc repo; báo cáo ghi scratchpad, điều phối viên chép vào `source-analysis.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 2 | Lập dàn ý (chỉ đọc repo; ghi dàn ý vào scratchpad, điều phối viên chép vào `outline.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 3 | Soạn ghi chú (ghi `lecture-note.md`, script thí nghiệm ngoài repo, `outline.md` §13) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 4 | Năm lượt rà độc lập (học viên; chính xác toán học; chuyên gia và trung thành nguồn; học thuật–sư phạm và `no-ai-slop` Detect; mạch và móc nối), chỉ đọc repo, báo cáo ghi vào scratchpad | general-purpose ×5 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 5 | Biên tập vòng 1 (cùng người viết; ghi `lecture-note.md`, script thí nghiệm, `bien-tap-vong-1.md`, `outline.md` §13) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 6 | Rà lại: toán học trên phần đã sửa (người rà 2); mạch, móc nối và văn phong trên phần đã sửa ±2 đoạn và ranh giới mục (người rà 5), chỉ đọc | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-31 · 7 | Biên tập vòng 2: 1 điểm trung bình và 13 điểm nhẹ của hai lượt rà lại (cùng biên tập viên) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |

## Phân tích nguồn — quyết định của điều phối viên: **chấp nhận** (2026-10-31)

Báo cáo (90 dòng, 7 mục; script ở scratchpad `src09/`), điều phối viên chép vào `source-analysis.md`. Điều phối viên tự kiểm ví dụ Gauss tuyến tính ($a=s=1$, $x=2$): $p(x)=N(0,2)$, $\ln p(2)=-\tfrac12\ln(4\pi)-1\approx-2{,}2655$; hậu nghiệm $N(1,\tfrac12)$; $\mathrm{KL}(N(0,1)\Vert N(1,\tfrac12))=\ln\sqrt{0{,}5}+\tfrac{1+1}{2\cdot0{,}5}-\tfrac12\approx1{,}1534$; $-\mathrm{ELBO}$ theo $(\mu,\sigma)$ bằng $\tfrac{\mu^2+\sigma^2}2+\tfrac{(x-a\mu)^2+a^2\sigma^2}{2s^2}-\ln\sigma+\text{hằng}$, lồi trên $\sigma>0$. Kiểm trên PDF: §24.4 bắt đầu tr. 348; điều phối viên đã sửa `sources/uml-sections.md`.

Quyết định cho dàn ý và bản thảo:

1. **Hàm lỗi log** nhận giá trị trong $[0,\infty]$ với mô hình rời rạc và có thể âm với mật độ: nêu tại chỗ dùng đầu rằng nó nằm ngoài (T2)/(T3) của các bài trước; các kết quả của Bài 09 là đồng nhất thức và bất đẳng thức tổng thể, nêu điều kiện khả tích và điều kiện giá tại chỗ (Mệnh đề 9.2: $\mathrm H(p_D)<\infty$; giá không chứa thì hai vế bằng $+\infty$). Giữ lời hứa Bài 02 dòng 574.
2. **Kí hiệu:** $\ln$; quan sát $x$ (chuỗi $x_{1:n}$, độ dài $n$, chỉ số vị trí $j$; $t$, $T$ để cho SGD); phân bố thật $D$ với hàm xác suất/mật độ $p_D$; mô hình $p_\theta$; phân bố biến phân $q_\phi$ ($\phi$ ở đây là tham số biến phân, ghi rõ khác $\phi_i$ của Bài 07); biến ẩn **$v$** (không dùng $z$ vì $z$ là quan sát của học phần; nói một câu: Kingma–Welling viết $z$); nhiễu **$\zeta$** (không dùng $\varepsilon$); $\mathrm{KL}(\cdot\Vert\cdot)$; $\mathrm H$ chữ đứng; $\operatorname{ELBO}(\theta,\phi;x)$; mô hình trong Mệnh đề 9.2 viết $p_\theta$ hoặc $p_M$, không dùng $q$ (tránh mâu thuẫn của blueprint).
3. **Thuật ngữ:** "tái tham số hóa" (theo `thuat-ngu.md`); "cận dưới bằng chứng (evidence lower bound, ELBO)".
4. **Mệnh đề 9.4** [S] với điều kiện đủ cụ thể (khả vi liên tục trên một tập mở với tập không không phụ thuộc $\phi$, cộng hàm trội khả tích); phản ví dụ $\mathbb 1[v>0]$ và Bernoulli cho thấy "khả vi hầu khắp nơi" chưa đủ.
5. **Quy tắc chuỗi với độ dài thay đổi** cần kí hiệu kết thúc; mất mát tổng và mất mát chuẩn hóa theo độ dài có cực tiểu tổng thể khác nhau (ví dụ $\theta^*=\tfrac16$ so với $\tfrac12$).
6. **Ví dụ:** bảng ba kí hiệu ($p(ABB)=21/125$); ML Bernoulli; Gauss một chiều cho ELBO (tái tạo và KL); ứng dụng bigram trên chuỗi DNA tổng hợp với tốc độ entropy biết trước; phản ví dụ: giá không chứa (UML §24.1.3 có ví dụ Bernoulli), cửa sổ chồng lấn chia ngẫu nhiên rò rỉ (MSE $0{,}20$ so với $0{,}99$), tái tham số hóa thất bại; ví dụ độ hợp lý và chất lượng mẫu (trộn $1\%$) chỉ dùng nếu nêu là bất đẳng thức sơ cấp của học phần. Ví dụ nối SGD (QĐ (c)): một nhận xét ngắn hoặc bài tập, với $W$ giới hạn $\sigma\ge\sigma_0$ để gradient bị chặn.
7. **Bài tập:** sáu bài gốc blueprint 9.5 và UML 24.2, 24.1; 24.3 tùy chọn. Thí nghiệm bigram nhỏ (blueprint 9.5.6) dùng script ở `../tools/courses/statistical-learning-theory/2627-1/scripts/`.
8. **Phạm vi:** Transformer, GAN, khuếch tán chỉ nhắc ngắn như mục tiêu/mô hình khác (blueprint 9.4). Thân ≤ 12 000, phụ lục ≤ 3 000. Tiêu đề "Bài 09 — Học chuỗi và mô hình sinh" (khớp thẻ chỉ mục).

## Dàn ý — quyết định của điều phối viên: **chấp nhận** (2026-10-31)

Dàn ý (606 dòng) do tác tử lập dàn ý ghi vào scratchpad `outline09/outline.md` khi bước soạn ghi chú Bài 08 đang ghi repo; điều phối viên chép vào `outline.md`. 15 khối 09.1–09.15 (**Mệnh đề 09.3 = Prop 9.1** [F]; **Mệnh đề 09.8 = Prop 9.2** [F]; **Hệ quả 09.9 = Corollary**; **Định lý 09.12 = Thm 9.3** [F]; Hệ quả 09.13 EM; **Mệnh đề 09.15 = Prop 9.4** [S]), Ví dụ 09.1–09.13, Bài tập 09.1–09.10 (06 gốc; 09.7 gốc thêm: SGD trên $-\mathrm{ELBO}$ lồi; 09.8–09.10 = UML 24.1, 24.2, 24.3 tùy chọn), phụ lục A–C, thí nghiệm `exp_lec09_bigram.py` (bigram trên chuỗi DNA tổng hợp và cửa sổ chồng lấn; 10 lần chạy, 200 chuỗi kiểm tra độc lập). Điều phối viên đọc mục 1–2, 9–10, 12 và tự kiểm cận số bắt buộc của Ví dụ 09.4: hàm lỗi theo kí tự trong $[0,\ln20]$, $m=50$ chuỗi, $\ln20\sqrt{\ln40/100}\approx0{,}5754$; nếu coi $10^4$ kí tự là độc lập thì $0{,}0407$, con số Định lý 02.7 không chứng minh. Khớp.

Quyết định về các điểm mở (mục 12.2): (1) **"kí tự" (token)** cho phần tử của bảng chữ, ghi tiếng Anh ở lần đầu; "kí tự kết thúc" (thay "kí hiệu kết thúc" của QĐ 5); (2) kí hiệu $p_1$, $p_2$, $\Theta$, $r$, $\kappa$ chấp nhận; (3) Hệ quả 09.13 (EM) giữ là khối đánh số (nội dung UML §24.4); (4) Định nghĩa 09.1 ở §1 chấp nhận; (5) GAN và mô hình khuếch tán: hai câu chỉ nêu đó là mục tiêu/mô hình khác ngoài phạm vi (blueprint 9.4), không thêm khẳng định nào khác; (6) một script chung cho hai phần thí nghiệm. "Phân kì KL" chốt. Điều phối viên đã thêm 25 dòng thuật ngữ vào `thuat-ngu.md` §11 và 14 dòng kí hiệu vào `ky-hieu.md`. Người viết ghi chú bắt đầu sau khi bước biên tập Bài 08 (đang ghi repo) xong.

## Bản thảo ghi chú — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-31)

Bản thảo 987 dòng; thân bài 11 984 tiếng, phụ lục 1 580. 15 khối 09.1–09.15, Ví dụ 09.1–09.13, §11 liệt kê Bài tập 09.1–09.10; 38 khối mở và đóng. Kiểm tra do điều phối viên chạy: `forward_refs.py` 0; không có "Mục này", "rõ ràng", "dễ thấy", "Đáp án", "hãy", "vô nghĩa"; điều phối viên chạy lại `exp_lec09_bigram.py` (1,1 giây): cửa sổ chồng lấn MSE $0{,}1995$ (chia ngẫu nhiên) so với $0{,}9944$ (theo thời gian), khớp ghi chú; câu hỏi mở đầu: $-\ln0{,}6-\ln0{,}7-\ln0{,}4\approx0{,}511+0{,}357+0{,}916$. Chấp nhận các sai khác người viết báo (`outline.md` §13.2, 14 mục): $m_1$ thay $k$; các mục cắt theo thứ tự cắt; bảng hẹp cho 390 px; $\ell\le\ln52\approx3{,}95$ làm tròn lên. Điểm giao người rà toán: Ví dụ 09.6 dùng mô hình kí tự độc lập với độ dài cho trước, không có kí tự kết thúc như Định nghĩa 09.6. Bản đóng băng: scratchpad `lec09-draft-frozen.md` (SHA-256 bắt đầu `b9c3833a317e1e63`).

## Năm lượt rà — quyết định của điều phối viên: **yêu cầu sửa** (2026-10-31)

Báo cáo trong `reviews/1-hoc-vien.md` (0/2/8/18), `2-toan-hoc.md` (0/0/2/10; mọi kết quả chứng minh lại đúng; thí nghiệm khớp), `3-chuyen-gia-nguon.md` (0/1/6/9; §E 10/12; không chép nguồn; lời hứa Bài 02 dòng 574 và cầu nối Bài 08 được giữ), `4-hoc-thuat-van-phong.md` (0/0/7/25), `5-mach.md` (0/0/5/13; `forward_refs.py` 0). Không có lỗi chặn bàn giao. Ba phát hiện nghiêm trọng: câu về GAN và mô hình khuếch tán (sai một phần, không có cơ sở); câu cầu nối "chỉ $q_\phi$ phụ thuộc tham số"; bảng ở §1 dùng thuật ngữ trước định nghĩa. Điều phối viên tự kiểm phản ví dụ của người rà toán cho Hệ quả 09.9 ($\Theta=(0,1)\setminus\{0{,}6\}$, $D=\mathrm{Ber}(0{,}6)$: $\inf\mathrm{KL}=0$ không đạt). Quyết định gộp: `reviews/0-quyet-dinh.md` (N1–N3, 9 mục trung bình, điểm nhẹ). Vòng biên tập giao khi người soạn bài tập Bài 08 (đang ghi repo) xong.

## Biên tập vòng 1 — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-31)

Biên tập viên áp dụng N1–N3, 9 mục trung bình và các điểm nhẹ (`bien-tap-vong-1.md`; năm mục không áp dụng có lý do — độ rộng bảng ở 390 px, hết chữ, mục đã bị loại bỏ — chấp nhận). Để giữ trần: chứng minh Mệnh đề 09.3 và Hệ quả 09.13 chuyển sang Phụ lục D mới (vẫn đầy đủ). Thân bài 11 997 tiếng, phụ lục 2 036. `forward_refs.py` 0. Điều phối viên thêm năm thuật ngữ vào `thuat-ngu.md` §11. Diff `lec09-r1.udiff` giao rà lại: toán (người rà 2, gồm câu mới sau $\square$ của Hệ quả 09.13 ở Phụ lục D: bước M chỉ cần làm tăng tổng), mạch và văn phong (người rà 5).

## Rà lại sau vòng 1 — quyết định của điều phối viên: **chấp nhận, sửa nhẹ** (2026-10-31)

Rà lại toán (`reviews/6-ra-lai-toan.md`): 13/13 phát hiện cũ ✓; mọi phần toán đã đổi đúng (N1–N3, Hệ quả 09.9, Định nghĩa 09.6, Ví dụ 09.6, tái tham số hóa với $\kappa_i$ kiểm Monte Carlo $2{,}3052$ so với $2{,}3055$, Phụ lục B, D); số mới khớp. Mới 0/0/0/4 (dòng 851 với EM phân bố lấy kì vọng $q_i=p_{\theta_t}(\cdot\mid x)$ cũng phụ thuộc tham số — viết "phân bố biến phân ($q_\phi$ hoặc $q_i$)"; Định nghĩa 09.6 thêm $n(x)\ge1$; dòng 1018 "không làm giảm" và tính hữu hạn ở Bước 1; dòng 458 kì vọng có điều kiện theo $x_{j-1}$). Rà lại mạch (`reviews/7-ra-lai-mach.md`): 16 ✓, 1 một phần, 2 tùy chọn bỏ có lý do; T2–T6 ✓, T1, T7 một phần; `forward_refs.py` 0; cầu nối có "Câu hỏi cho Bài 10 là". Mới 0/0/1/9: M1 "bằng chứng thí nghiệm" trùng thuật ngữ "bằng chứng" $=\ln p_\theta(x)$ — đổi "kết quả thí nghiệm"; các điểm nhẹ (§1 kết bằng bảng; câu kết §7, §9; dòng 452 nói quá ý Nhận xét 02.11; câu ôn nhanh 3). Gửi biên tập viên sửa khi người soạn bài tập Bài 08 (đang ghi repo) xong; điều phối viên đọc diff, không rà lại thêm.

## Kiểm định cuối và công bố ghi chú — Bài 09 (2026-10-31)

Vòng 2 (`bien-tap-vong-1.md` mục "Vòng 2"): 4 điểm nhẹ của rà lại toán, M1–M10 của rà lại mạch; bảng nguồn ngẫu nhiên chuyển lên trước Định nghĩa 09.1, bỏ $k$. Điều phối viên đọc toàn bộ diff: đúng các quyết định. Thân bài 12 000 tiếng (đúng trần), phụ lục 2 061.

Kiểm định do điều phối viên chạy (`final06/final05.py`, `idx9.py`; cổng 8772), qua HTTP và `file://`, ở 1600×900 và 390×844: 1 466 công thức, 9 khối thu gọn, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 tràn, độ rộng 375 px ở 390; bản in A4 44 trang. Điều phối viên xem ảnh cuộn ở 390 (Ví dụ 09.10): không tràn. `forward_refs.py` 0; không khoảng trắng cuối dòng. Thẻ Bài 09 liên kết ghi chú; mở từ chỉ mục qua HTTP và `file://` đúng tiêu đề. Gói `material-local-data.js` khi commit dựng bằng `bundle_head.py`.

**Trạng thái:** ghi chú Bài 09 hoàn tất; commit và push. Việc tiếp theo: bài tập Bài 09 (sau khi ghi chú Bài 10 được giao người viết, mỗi lúc một người ghi repo).
