# Storyboard — Bộ trang chiếu Bài 06: Học bằng hạ gradient ngẫu nhiên, chính quy hóa và tính ổn định

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-11-15 bởi tác tử lập storyboard. Nguồn nội dung duy nhất: `materials/lec-06/lecture-note.md` (bản hiện hành, commit faeeba9); bài tập: `materials/lec-06/exercises.md`. Quy định: `CLAUDE.md` § Slide decks, `common-brief.md` (gồm "Các quy định dễ sót" và "Bài học từ năm báo cáo duyệt deck 01"), `brief-storyboard.md`, `../rl-plan/CLAUDE.md` § Deck structure and content, nhật ký yêu cầu 2026-11-13 hàng 1–5, quyết định của điều phối viên trong `lec-0{1,2,3,4,5}/review-log.md` § Bộ trang chiếu, ba báo cáo `lec-0{3,4,5}/reviews/deck-storyboard-gate.md`. Khuôn bố cục theo storyboard Bài 05. Mọi mã trang có dạng `L06-k-mm`; trong bảng viết gọn `k-mm`.

Số âm tiết trong tệp này đếm bằng script (mục 15) theo cách của `deck_lint.py`: token cách nhau bởi khoảng trắng có chữ cái hoặc chữ số, số viết trong câu có tính, KaTeX và số trong bảng không tính, mỗi công thức hiển thị tính một dòng. Điều phối viên đếm lại trên deck.

UML đã đọc để đối chiếu (không chép câu chữ): §13.2 trang PDF 173–174 (Định lý 13.2 của UML: đẳng thức giữa khoảng cách tổng quát hóa kì vọng và trung bình thay một; định nghĩa ổn định thay một theo trung bình); §13.3 trang PDF 175–176 (Bổ đề 13.5: lồi mạnh và tăng trưởng bậc hai qua đạo hàm theo hướng; phép tính (13.7)–(13.10) với hai tập huấn luyện lân cận, lập luận một phía cho hằng số $2\rho/(\lambda m)$ với số hạng $\lambda\lVert w\rVert^2$); §14.5 trang PDF 197 (quan sát mới cho gradient ngẫu nhiên không chệch của $L_D$, kể cả hàm lỗi không khả vi). Các mục khác chỉ dẫn theo §13 của ghi chú và `sources/uml-sections.md` (§13.1 trang 171, §13.4 trang 179, §13.7 trang 181, §12.2 trang 163).

## 1. Tên tệp và tiêu đề

- **Tệp deck:** `2627-1/lecture-06-on-dinh-chinh-quy-hoa.html` (slug ASCII từ tên bài: "tính ổn định", "chính quy hóa"; tên ngắn theo mẫu `lecture-05-ha-gradient-ngau-nhien.html`).
- **Tiêu đề deck (h1 trang bìa):** "Học bằng hạ gradient ngẫu nhiên, chính quy hóa và tính ổn định" (đúng tên bài của ghi chú).
- **`<title>`:** "Bài 06: Chính quy hóa và tính ổn định".
- **Chân trang:** "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài 06".
- **Liên kết viewer:** `material-viewer.html?doc=materials/lec-06/lecture-note.md&deck=lecture-06-on-dinh-chinh-quy-hoa.html` và `…exercises.md&deck=…`.
- **Màn hẹp:** chế độ đọc của `lecture-course.css` (`.slides` bọc trong `div.lecture-viewport`, script màn hẹp của `lecture-template.html`); bảng 2-11, 3-04, 5-04, 7-01, 7-07 đặt trong `.table-scroll`.
- **Trang cuối deck Bài 05** (7-07 của storyboard Bài 05) nhận liên kết tới tệp này khi deck Bài 06 xong.

## 2. Khung lý thuyết chung

**Vấn đề trung tâm (hộp "Vấn đề trung tâm", bằng lời, ≤ 30 âm tiết).** "**Câu hỏi:** khi nào tối ưu trở thành học?" (câu hỏi trung tâm của blueprint, `outline.md` §1; đoạn mở đầu của ghi chú nói rõ: "khi nào một thuật toán tối ưu cũng là một thuật toán học, tức có bảo đảm cho rủi ro kì vọng $L_D$ của đầu ra"; câu này đi vào ghi chú diễn giả 1-05. 9 âm tiết kể cả nhãn.)

**Luận điểm (trang bìa, hai câu, bằng lời).** "Khi mỗi bước dùng một quan sát mới, cận của hạ gradient ngẫu nhiên chặn thẳng rủi ro vượt mức kì vọng. Khi dùng lại tập huấn luyện, cần thêm một cận cho khoảng cách tổng quát hóa kì vọng; với hàm lỗi lồi và Lipschitz, chính quy hóa cho cận đó qua tính ổn định đều." (Hệ quả 06.2, Mệnh đề 06.5, Định lý 06.10, Mệnh đề 06.11; §10 đoạn 1. Câu có điều kiện ở cả hai vế: "khi mỗi bước dùng một quan sát mới", "với hàm lỗi lồi và Lipschitz"; tránh lỗi luận điểm khẳng định không điều kiện của cổng Bài 05. 57 âm tiết theo script; bìa không tính trần.)

**Trọng tâm trực quan của deck.** Bốn chỗ, theo yêu cầu của điều phối viên:
1. **Vì sao một lượt SGD trên quan sát mới cho bảo đảm trực tiếp cho $L_D$** (2-03, 2-06, 2-07, 1-06): điểm lặp $w_t$ chưa thấy $Z_t$, nên với $w_t$ đã biết, gradient trên $Z_t$ là gradient trên một quan sát rút từ $D$ và có trung bình là dưới gradient của $L_D$; khi chỉ số rút từ tập huấn luyện đã lưu, trung bình là dưới gradient của $L_S$ ($2(w_t-\bar Y)$ so với $2w_t$). Số: $0{,}000578$ so với cận $0{,}1$; $0{,}2261$ khi dùng lại bốn quan sát.
2. **Vì sao ổn định thay một điểm kéo theo khoảng cách tổng quát hóa kì vọng nhỏ** (4-02, hình F3, 4-04, trang kỹ thuật 4-05): $L_D(A(S;\xi))$ là hàm lỗi trên một quan sát mới $Z'$; đổi vai $Z'$ với $Z_i$ biến nó thành hàm lỗi của $A(S^{(i)};\xi)$ trên $Z_i$, một quan sát mà thuật toán đó không thấy; mỗi số hạng của khoảng cách là "hàm lỗi tại $Z_i$ khi bỏ $Z_i$ khỏi tập huấn luyện trừ hàm lỗi tại $Z_i$ khi giữ nó".
3. **Chính quy hóa lồi mạnh cho ổn định cỡ $1/(\lambda m)$** (3-03, 3-04 với Hình 06.1, 5-01, 5-02): hai mục tiêu có chính quy hóa chỉ khác một hàm lỗi với trọng số $1/m$, hiệu của chúng $(2G/m)$-Lipschitz trên $W$, còn số hạng $\tfrac\lambda2\lVert w\rVert^2$ cho độ cong ít nhất $\lambda$; điểm cực tiểu dịch không quá $(2G/m)/\lambda$.
4. **Ví dụ ridge thay một quan sát** (3-01, 3-04, 4-01, 5-03, 5-05): tập huấn luyện bốn quan sát của Ví dụ 06.1, thay $z_4=(-1,-1)$ bằng $z'=(1,-1)$; khoảng cách giữa hai nghiệm $0{,}6154$; $0{,}3810$; $0{,}2759$; $0{,}1778$ với $\lambda=0;1;2;4$; Hình 06.1 của ghi chú dùng lại trên 3-04.

**Đối tượng và kí hiệu chung** (ghi chú §1–§2, `outline.md` §10):
- quan sát $z=(x,y)\in\mathcal Z\subset\mathbb R^p\times\mathcal Y$, phân bố $D$; dòng quan sát mới $Z_1,Z_2,\ldots$ (chế độ A); tập huấn luyện $S=(Z_1,\ldots,Z_m)\sim D^m$ lưu lại (chế độ B); $C_x$, $C_y$;
- tham số $w\in W\subset\mathbb R^p$ ($W$ khác rỗng, đóng, lồi), $h_w(x)=\langle w,x\rangle$, $\ell(w,z)\ge0$ lồi theo $w$; $L_S$, $L_D$; quy tắc dưới gradient đo được $v(w,z)$; $G$, $R$, $B$, $W_B$;
- SGD có chiếu (Thuật toán 05.11): $w_1$, $\eta$, $T$, $g_t$, $\bar w_T$, $i_t$, $\mathcal F_{t-1}$; $\psi(w)=\mathbb E_{Z\sim D}v(w,Z)$;
- thuật toán có nguồn ngẫu nhiên riêng $A(S;\xi)$, $\xi\sim P_\xi$; đầu ra $\tilde w$; $\operatorname{opt}_S$; điểm so sánh $u\in W$ cố định;
- ERM có chính quy hóa: $\lambda>0$, $F_{s,\lambda}=L_s+\tfrac\lambda2\lVert\cdot\rVert^2$, $\hat w_s$, $\hat w_S$; $\lambda^*=2G/(B\sqrt m)$;
- ổn định: $s^{(i)}$, $S^{(i)}$, quan sát thay thế $z'$, $Z'$, quan sát kiểm tra $z$, $\epsilon_{\mathrm{stab}}(m)$; trong chứng minh Mệnh đề 06.11: $\hat w$, $\hat w'$;
- cục bộ của ví dụ: $\bar Y$, $c_t$, $q$ (Ví dụ 06.2, 06.3); $S^{(4)}$ (Ví dụ 06.4); $h_0$ (Ví dụ 06.5); $\bar z$, $M$ (Ví dụ 06.8, 06.9); $Q(\lambda)$, $B_0$, $\lambda_0$ (Bài tập 06.4).

**Giả thiết** (ghi chú §2): (T1) lấy mẫu, dạng đầy đủ và dạng yếu; (T2) hàm lỗi; dữ liệu bị chặn ($\lVert x\rVert\le C_x$, $\lvert y\rvert\le C_y$, cho hàm lỗi bình phương); (C), (G1), (G2) của Bài 05; hàm lỗi lồi; (L) Lipschitz trên $W$ với hằng số $G$; (O1) nghiệm đúng, (O2) nghiệm gần đúng; đo được. Các kết quả chính không giả sử hàm lỗi bị chặn.

**Chuỗi định nghĩa → kết quả → phương pháp.**
1. Hai chương trình SGD cùng hằng số, cùng cận $0{,}1$; chỉ khác nguồn nhãn (Câu hỏi mở đầu) → cần biết hàm mà oracle không chệch.
2. Hai chế độ lấy mẫu (§1), kí hiệu, giả thiết (§2); Ví dụ 06.1 và ứng dụng một triệu hồ sơ (§3).
3. Bổ đề 06.1 (kì vọng của dưới gradient) → Hệ quả 06.2 (SGD với quan sát mới, rủi ro vượt mức kì vọng $RG/\sqrt T$) → Ví dụ 06.2 ($0{,}000578$) → Nhận xét 06.3 (một vòng qua tập huấn luyện).
4. Oracle trên tập huấn luyện lưu lại không chệch cho $L_S$ (§5) → Định nghĩa 06.4 (khoảng cách tổng quát hóa kì vọng) → Mệnh đề 06.5 (rủi ro = khoảng cách + sai số tối ưu, theo kì vọng) → Ví dụ 06.3 ($0{,}4750$ so với $0{,}0011$).
5. Một quan sát dịch nghiệm ERM $0{,}6154$ → Định nghĩa 06.6 (ERM có chính quy hóa) → Bổ đề 06.7, 06.8 (tăng trưởng bậc hai, nghiệm duy nhất) → Ví dụ 06.4, Hình 06.1.
6. Định nghĩa 06.9 (tập huấn luyện lân cận, ổn định đều) → lập luận đổi vai → Định lý 06.10 → Ví dụ 06.5 (thuật toán hằng).
7. Mệnh đề 06.11 ($2G/(\lambda m)$, $2G^2/(\lambda m)$) → Ví dụ 06.6, 06.8 (cận và độ chặt) → Ví dụ 06.7, 06.9 (bỏ $\lambda>0$, bỏ dữ liệu bị chặn) → Nhận xét 06.12 (đọc thêm).
8. Đánh đổi khớp–ổn định (§9, Ví dụ 06.12) → Hệ quả 06.13 (bất đẳng thức oracle, $\lambda^*$, $2GB/\sqrt m$) → Ví dụ 06.10, 06.11 (cỡ mẫu; một triệu hồ sơ) → Nhận xét 06.14 (kì vọng so với xác suất cao), Nhận xét 06.15 (đọc thêm).

**Giới hạn áp dụng** (ghi chú §10): mọi bảo đảm của bài là theo kì vọng và cấp thuật toán; bất đẳng thức Markov tốn thừa số $1/\delta^2=400$ về cỡ mẫu; Định lý 06.10 chặn $\lvert\mathbb E[L_D-L_S]\rvert$, không chặn $\mathbb E\lvert L_D-L_S\rvert$ (Ví dụ 06.5); nghiệm gần đúng thêm $G\sqrt{2\epsilon_{\mathrm{opt}}/\lambda}$ (Nhận xét 06.15, đọc thêm); với hàm lỗi bình phương, cận ổn định cần dữ liệu bị chặn (Ví dụ 06.9); SGD nhiều vòng có khoảng cách tổng quát hóa kì vọng $0{,}4750$ ($0{,}4938$ khi $T=25\,600$, Phụ lục D) và cần một hệ số ổn định riêng; hàm lỗi phải lồi theo tham số, nên các cận không chuyển sang mạng nơ-ron. Nhận xét 06.12 và 06.15 (đọc thêm) nói rõ mức đọc thêm ở ghi chú diễn giả. Phụ lục A, B, C, E chỉ vào ghi chú diễn giả; Phụ lục D cho $c_t$, $\sum_tc_t$, $\sum_tc_t^2$.

## 3. Bảng mạch

Bảy mạch theo đúng thứ tự các mục của ghi chú; mỗi mạch ứng với các mục liên tiếp. Mạch 2 gộp §1–§5 (hai cách lấy mẫu là một cụm: §4 cho chế độ A, §5 cho chế độ B, cùng hai chương trình của câu hỏi mở đầu); tách thành hai mạch thì deck có tám mạch. Bảng đối chiếu trang → khối ghi chú ở mục 12.

| N | Tên mạch | Mục ghi chú | Chức năng | Đầu vào | Đầu ra | `strand-lead` (âm tiết) | Từ khóa | Trang | Phút |
|---|---|---|---|---|---|---:|---|---:|---:|
| 1 | Mở đầu | đoạn mở, Câu hỏi mở đầu, Mục tiêu, Tiên quyết | Bìa, tiên quyết, mục tiêu, nội dung, vấn đề trung tâm, ví dụ hai chương trình | Bài 05: cận $RG/\sqrt T$ cho hàm mà oracle không chệch | Câu hỏi: hai chương trình cùng cận $0{,}1$ khác nhau ở $\mathbb EL_D(\bar w_T)$ thế nào | (không có trang tiêu đề mạch) | — | 6 | 9 |
| 2 | Quan sát mới và tập huấn luyện lưu lại | §1–§5 | Thiết lập hai chế độ; Ví dụ 06.1, ứng dụng; Bổ đề 06.1; Hệ quả 06.2 và ý tưởng chứng minh; Ví dụ 06.2; Nhận xét 06.3; oracle trên $S$; Định nghĩa 06.4; Mệnh đề 06.5 và ý tưởng chứng minh; Ví dụ 06.3; Bài tập 06.1(c), (d) | cận kì vọng của Bài 05 | Rủi ro vượt mức kì vọng $\le RG/\sqrt T$ với quan sát mới; với tập huấn luyện dùng lại, rủi ro vượt mức kì vọng $\le$ khoảng cách tổng quát hóa kì vọng $+\ \mathbb E\operatorname{opt}_S$ | "Gradient trên quan sát mới không chệch cho rủi ro kì vọng, trên tập huấn luyện dùng lại thì cho rủi ro thực nghiệm." (24) | quan sát mới · rủi ro vượt mức kì vọng · khoảng cách tổng quát hóa kì vọng · bảo đảm cấp thuật toán | 13 | 32 |
| 3 | ERM có chính quy hóa | §6 | Ví dụ thay một quan sát; Định nghĩa 06.6; Bổ đề 06.7, 06.8; Ví dụ 06.4 và Hình 06.1; Bài tập 06.10(a), (c) | cần một thuật toán có khoảng cách tổng quát hóa kì vọng nhỏ | Nghiệm có chính quy hóa duy nhất, tăng trưởng bậc hai quanh nghiệm; khoảng cách giữa hai nghiệm giảm khi $\lambda$ tăng | "Số hạng phạt chuẩn làm nghiệm duy nhất và ít nhạy hơn khi thay một quan sát." (17) | mục tiêu có chính quy hóa · lồi mạnh · tăng trưởng bậc hai · hồi quy ridge | 6 | 14 |
| 4 | Tính ổn định và khoảng cách tổng quát hóa kì vọng | §7 | Định nghĩa 06.9 (mở bằng ví dụ $1{,}7988$); trực quan đổi vai (hình F3); Định lý 06.10 và ý tưởng chứng minh; **trang "Kỹ thuật." mới: lập luận đổi vai**; Ví dụ 06.5; Bài tập 06.2(b) | khoảng cách tổng quát hóa kì vọng của Mệnh đề 06.5 | $\lvert\mathbb E[L_D-L_S]\rvert\le\epsilon_{\mathrm{stab}}(m)$ với mọi thuật toán ổn định đều, không cần hàm lỗi bị chặn | "Thay một quan sát chỉ làm hàm lỗi đổi ít thì khoảng cách tổng quát hóa kì vọng nhỏ." (19) | tập huấn luyện lân cận · ổn định đều · hệ số ổn định · lập luận đổi vai | 8 | 22 |
| 5 | Tính ổn định của ERM có chính quy hóa | §8 | Mệnh đề 06.11 và ý tưởng chứng minh; Ví dụ 06.6, 06.8; Ví dụ 06.7, 06.9 (hai thẻ); Nhận xét 06.12 (đọc thêm, ghi chú diễn giả); Bài tập 06.6(a) | Định lý 06.10 cần một hệ số ổn định cụ thể | $\epsilon_{\mathrm{stab}}(m)=2G^2/(\lambda m)$; cận khoảng cách đạt được; bỏ $\lambda>0$ hay bỏ dữ liệu bị chặn thì hệ số không giảm theo $m$ | "Với hàm lỗi lồi, Lipschitz, chính quy hóa cho hệ số ổn định giảm theo hệ số chính quy hóa và cỡ mẫu." (23) | ổn định đều · hai tập huấn luyện lân cận · tính Lipschitz · dữ liệu bị chặn | 6 | 16 |
| 6 | Đánh đổi khớp–ổn định | §9 | Trực quan và Ví dụ 06.12; Hệ quả 06.13 và ý tưởng chứng minh; Ví dụ 06.10, 06.11 (hình F2); Nhận xét 06.14; Nhận xét 06.15 (đọc thêm, ghi chú diễn giả); Bài tập 06.4(b) | hệ số ổn định của mạch 5, phân tích rủi ro của mạch 2 | $\mathbb E_SL_D(\hat w_S)-\inf_{W_B}L_D\le2GB/\sqrt m$ với $\lambda^*$; cỡ mẫu $4G^2B^2/\epsilon^2$; xác suất cao tốn thừa số $1/\delta^2$ | "Hệ số chính quy hóa chọn trước cân độ khớp với tính ổn định và cho cỡ mẫu đủ cho một mức rủi ro." (24) | số hạng ổn định · số hạng khớp · bất đẳng thức oracle · cỡ mẫu | 7 | 18 |
| 7 | Tổng kết | §10–§13 | Bảng kết quả, trả lời vấn đề trung tâm, bài tập tổng hợp (Bài tập 06.4(c)), tự kiểm tra, bài tập về nhà, tài liệu | mọi kết quả | Cầu nối sang Bài 07 | "Quan sát mới, phân tích rủi ro và tính ổn định cho mọi bảo đảm của bài." (17) | — | 9 | 9 |
| | **Tổng** | | | | | | | **55** | **120** |

Số trang (54) vượt mục tiêu 45–52 hai trang, dưới trần 55. Lý do: năm kết quả chính có trang phát biểu và trang "Ý tưởng chứng minh" riêng (Hệ quả 06.2, Mệnh đề 06.5, Định lý 06.10, Mệnh đề 06.11, Hệ quả 06.13: 10 trang); một kỹ thuật mới dùng lại ở Bài 08 có trang "Kỹ thuật." riêng (4-05); năm trang bài tập giữa cụm (mạch 2–6) và một bài tập tổng hợp hai trang; ba phản ví dụ bỏ giả thiết mà §10 liệt kê (dùng lại tập huấn luyện, bỏ chính quy hóa, bỏ dữ liệu bị chặn) cộng phản ví dụ chính quy hóa quá mạnh (mục tiêu 5). Đã gộp để giữ 54: Nhận xét 06.3 và đoạn mở §5 chung trang 2-07; Ví dụ 06.1 và khối ứng dụng §3 chung trang 2-02 (hai thẻ); Bổ đề 06.7 và 06.8 chung trang 3-03; bảng của Ví dụ 06.4 và Hình 06.1 chung trang 3-04; ví dụ mở đầu §7 ($304/169$) và đoạn thuật toán ghi nhớ vào trang định nghĩa 4-01; Ví dụ 06.6 và 06.8 chung trang 5-03; Ví dụ 06.7 và 06.9 chung trang 5-04 (hai thẻ); Ví dụ 06.10 và 06.11 chung trang 6-04; Ví dụ 06.12 vào trang trực quan 6-01; Nhận xét 06.12, 06.15 (đọc thêm), Phụ lục A–E ở ghi chú diễn giả. Phương án rút còn 52 ở mục 11, điểm 2.

## 4. Bảng kết quả chính

Số hiệu theo ghi chú. Ánh xạ blueprint → ghi chú (theo `outline.md` §2): Corollary 6.1 → Hệ quả 06.2; Proposition 6.2 → Mệnh đề 06.5; Theorem 6.3 → Định lý 06.10; Proposition 6.4 [S] → Mệnh đề 06.11; Corollary 6.5 [S] → Hệ quả 06.13. Bổ đề 06.1, 06.7, 06.8 là công cụ của học phần. Mọi phát biểu rút gọn trên trang dùng "Giả thiết:" và "Bảo đảm:", giữ đủ giả thiết, lượng từ, hằng số và loại bảo đảm của ghi chú.

| Kết quả | Loại bảo đảm | (a) Trực quan | (b) Ý tưởng chứng minh | (c) Kỹ thuật | (d) Ví dụ bổ trợ | Trang |
|---|---|---|---|---|---|---|
| **Hệ quả 06.2** (SGD với quan sát mới; chứng minh đầy đủ) | kì vọng theo $Z_1,\ldots,Z_{T-1}$; (a) mọi $u\in W$ với $\lVert w_1-u\rVert\le R$; (b) rủi ro vượt mức kì vọng so với $\inf_WL_D$ khi $\lVert w_1-u\rVert\le R$ với mọi $u\in W$; (c) $T\ge R^2G^2/\epsilon^2$; cấp thuật toán; phụ thuộc $p$ chỉ qua $G$, $R$; $T-1$ quan sát | Điểm lặp $w_t$ chưa thấy $Z_t$: với $w_t$ đã biết, gradient trên $Z_t$ là gradient trên một quan sát rút từ $D$, nên trung bình là dưới gradient của $L_D$ (Bổ đề 06.1). Cực biên: nếu $Z_t$ là một quan sát đã dùng thì $w_t$ phụ thuộc nó (2-07, Bài tập 06.1(c)). | Ba bước: oracle của Định nghĩa 05.10 với $\xi_t=Z_t$ ((T1) dạng đầy đủ: tính độc lập dùng ở đây) và Bổ đề 06.1(b) cho (G1), cận gradient cho (G2); Bổ đề 06.1(a) và $W$ đóng, lồi cho (C); Hệ quả 05.15 với $F=L_D$. Bỏ tính độc lập (từ vòng thứ hai trên tập huấn luyện): Bước 1 hỏng, Ví dụ 06.3 và Bài tập 06.1(c). | **Nhắc lại** kì vọng có điều kiện theo lịch sử, tổng triệt tiêu và trung bình các điểm lặp (Bài 05, trang riêng 3-07, 4-05 của deck Bài 05): kì vọng có điều kiện theo lịch sử một dòng "Nhắc lại:" trên 2-03; tổng triệt tiêu ở ghi chú diễn giả 2-05. Bổ đề 06.1: lấy kì vọng của bất đẳng thức dưới gradient (ghi chú diễn giả 2-03). | Ví dụ 06.2 ($G=4$, $R=1$, $\eta=0{,}00625$, cận $0{,}1$, giá trị đúng $0{,}000578$); Nhận xét 06.3 ($5/\sqrt{10^6+1}\approx0{,}005$); Bài tập 06.1(d). | 2-03, 2-04, 2-05, 2-06, 2-07 |
| **Mệnh đề 06.5** (phân tích rủi ro trên tập huấn luyện lưu lại; chứng minh đầy đủ) | (a) đẳng thức trên từng $(S,\xi)$; (b) kì vọng theo $(S,\xi)$; mỗi $Z_i\sim D$ (dạng yếu của (T1) đủ); $u\in W$ cố định, không phụ thuộc $S$, $\xi$ | Rủi ro vượt mức của đầu ra gồm phần đầu ra được tính từ chính $S$ (khoảng cách tổng quát hóa) và phần bộ giải chưa tối ưu ($\operatorname{opt}_S$); Hệ quả 05.19 chỉ chặn phần sau. Cực biên: $A$ trả về $h$ cố định có phần thứ nhất bằng $0$. | Bốn bước: thêm bớt $L_S(\tilde w)$, $L_S(u)$ (như Mệnh đề 04.3); $u\in W$ cho số hạng giữa $\le\operatorname{opt}_S$; $u$ cố định và mỗi $Z_i\sim D$ cho $\mathbb E_SL_S(u)=L_D(u)$ (Mệnh đề 01.7); lấy kì vọng, rồi cận dưới đúng theo $u$. Chọn $u=\tilde w$ (phụ thuộc $S$): Bước 3 hỏng. | Nhắc lại Mệnh đề 01.7, Mệnh đề 04.3 (1-02, ghi chú diễn giả 2-10). | Ví dụ 06.3 ($1{,}2261$; $0{,}7511$; $0{,}75$; khoảng cách $0{,}4750$; $\mathbb E\operatorname{opt}_S\approx0{,}0011$; cận $0{,}4761\ge0{,}2261$). | 2-09, 2-10, 2-11 |
| **Định lý 06.10** (tính ổn định chặn khoảng cách tổng quát hóa kì vọng; chứng minh đầy đủ) | kì vọng theo $(S,\xi)$; chặn trị tuyệt đối của khoảng cách tổng quát hóa kì vọng; (T1) dạng đầy đủ; hàm lỗi không cần bị chặn; cấp thuật toán, phụ thuộc $m$ chỉ qua $\epsilon_{\mathrm{stab}}(m)$ | $L_D$ là hàm lỗi trên quan sát mới $Z'$; đổi vai $Z'$ với $Z_i$: mỗi số hạng của khoảng cách là hàm lỗi tại $Z_i$ khi bỏ $Z_i$ khỏi tập huấn luyện trừ hàm lỗi tại $Z_i$ khi giữ nó (hình F3). Cực biên: thuật toán ghi nhớ, hai vế bằng $1$; thuật toán trả về $h$ cố định, hai vế bằng $0$. | Bốn bước: Fubini và tính độc lập của $Z'$ cho $\mathbb E\,\ell(A(S;\xi),Z')=\mathbb EL_D$; (T1) dạng đầy đủ cho phép đổi chỗ $Z_i$, $Z'$; $\mathbb EL_S$ là trung bình theo $i$ (hữu hạn nhờ tính ổn định); lấy kì vọng theo $\xi$ trước, dùng tính ổn định đều cho từng hiệu. Bỏ dạng đầy đủ của (T1) (các $Z_i$ bằng nhau): Bước 2 hỏng, Bài tập 06.2(c) ($0{,}5>7/16$ khi $m=4$). | **Lập luận đổi vai (thay một điểm)**: lần đầu trong học phần, **trang "Kỹ thuật." riêng 4-05**; dùng lại ở Bài 08 (ghi chú Bài 08 dẫn Định lý 06.10 chín lần, Định nghĩa 06.9 mười một lần). Nhắc lại đối xứng hóa và tập mẫu ảo (Bài 03) để so sánh. | Ví dụ 06.5 (thuật toán hằng: hệ số $0$, khoảng cách $0$, $\mathbb E\lvert L_S-\tfrac12\rvert=0{,}1230$; $0{,}0398$; $0{,}0126$); Bài tập 06.2(b) ($0{,}25=0{,}25$; hệ số $0{,}75$). | 4-02, 4-03, 4-04, 4-05, 4-06, 4-07 |
| **Mệnh đề 06.11** (tính ổn định của ERM có chính quy hóa; phác thảo, chi tiết ở Phụ lục B) | tất định, mọi tập huấn luyện, mọi $i$, $z'$, không cần $D$; (a) $\lVert\hat w_s-\hat w_{s^{(i)}}\rVert\le2G/(\lambda m)$; (b) $\epsilon_{\mathrm{stab}}(m)=2G^2/(\lambda m)$ | Hai mục tiêu chỉ khác một hàm lỗi với trọng số $1/m$; hiệu của chúng $(2G/m)$-Lipschitz trên $W$, còn số hạng chính quy hóa giữ độ cong $\lambda$; điểm cực tiểu dịch cỡ $(2G/m)/\lambda$. Đơn vị: gấp đôi $\lambda$ hoặc $m$ thì cận giảm một nửa. | Bốn bước: Bổ đề 06.8(c) cho hai bất đẳng thức tăng trưởng bậc hai (tính lồi của $\ell$, của $W$, $\lambda>0$); cộng, các số hạng chung và số hạng chính quy hóa triệt tiêu; (L) với $z_i$, $z'$; (L) với $z$. Bỏ $\lambda>0$: Ví dụ 06.7; bỏ dữ liệu bị chặn (hàm lỗi bình phương): Ví dụ 06.9. | Dòng "Kỹ thuật." trên 5-02: cộng hai bất đẳng thức tăng trưởng bậc hai đối xứng; một phía cho $4G/(\lambda m)$ (Phụ lục B). Chỉ dùng ở đây. | Ví dụ 06.6 ($0{,}1451\le0{,}3810\le0{,}7619$; cận $2$, $0{,}5$; lỏng khoảng $5$ lần); Ví dụ 06.8 (cận đạt được, $0{,}2$; khoảng cách tổng quát hóa $0{,}1$ so với $0{,}2$); Bài tập 06.6(a). | 5-01, 5-02, 5-03, 5-04, 5-05 |
| **Hệ quả 06.13** (bất đẳng thức oracle cho ERM có chính quy hóa; phác thảo, chi tiết ở Phụ lục C) | kì vọng theo $S\sim D^m$; (a) $u\in W$ cố định; (b) dạng cận dưới đúng; (c) $\lambda^*=2G/(B\sqrt m)$, $2GB/\sqrt m$, $m\ge4G^2B^2/\epsilon^2$; $\lambda$ chọn trước khi thấy tập huấn luyện | Khi $\lambda$ tăng, số hạng ổn định $2G^2/(\lambda m)$ giảm, số hạng khớp tăng; cực biên $\lambda=0$ (Ví dụ 06.7) và $\lambda$ lớn (Ví dụ 06.12). Hình F2: tổng nhỏ nhất tại $\lambda^*$. | Bốn bước: tính tối ưu của $\hat w_S$ với $u\in W$; Mệnh đề 06.5(a) với $u$ cố định; Định lý 06.10 và Mệnh đề 06.11 ((T1) dạng đầy đủ dùng ở đây; chỉ một phía); cân hai số hạng. Khả tích: Phụ lục C (ghi chú diễn giả). | Nhắc lại "cân hai số hạng" (Bài 05, một dòng) trên 6-03; bất đẳng thức Markov (Bài 02) trên 6-05. | Ví dụ 06.10 ($\lambda^*=0{,}2$, $0{,}2$; $6400$ so với $1599$; $40\,000$ so với $10^4$); Ví dụ 06.11 ($0{,}005+0{,}005=0{,}01$ so với $0{,}005$); Ví dụ 06.12 ($0{,}0083$; $0{,}25$; $0{,}8264$); Bài tập 06.4(b), (c). | 6-01, 6-02, 6-03, 6-04, 6-06, 7-04, 7-05 |

**Kết quả phụ và quyết định.**
- Bổ đề 06.1 (công cụ; chứng minh đầy đủ): phát biểu trên 2-03 cùng dòng "Trực quan."; lộ trình (lấy kì vọng của bất đẳng thức lồi và của bất đẳng thức dưới gradient, Cauchy–Schwarz cho tính khả tích) ở ghi chú diễn giả 2-03. Không có trang ý tưởng chứng minh riêng (mục 11, điểm 3).
- Nhận xét 06.3: trang 2-07, cùng đoạn mở §5.
- Định nghĩa 06.4: trang 2-08 với ba ví dụ của ghi chú.
- Định nghĩa 06.6: trang 3-02, cùng ví dụ nghiệm không duy nhất khi $\lambda=0$.
- Bổ đề 06.7 (công cụ; chứng minh đầy đủ) và Bổ đề 06.8 (công cụ; phác thảo, sự tồn tại ở Phụ lục A): phát biểu chung trang 3-03; lộ trình chứng minh Bổ đề 06.7 (điểm trên đoạn thẳng, chia cho $\alpha$, cho $\alpha\to0^+$) ở ghi chú diễn giả 3-03 và trên mặt trang bài tập 3-05 (Bài tập 06.10 dùng đúng kỹ thuật này ở dạng có dưới gradient). Phụ lục A ở ghi chú diễn giả 3-03.
- Định nghĩa 06.9: trang 4-01; câu "với mọi chạy trên mọi tập huấn luyện, kể cả tập có xác suất $0$" trên mặt trang.
- Đoạn sau Định lý 06.10 (đẳng thức thay một; thuật toán ghi nhớ): trang trực quan 4-02 (đặt trước phát biểu vì số liệu không cần định lý; tiền lệ T5 của cổng Bài 04).
- Nhận xét 06.12 (đọc thêm): ghi chú diễn giả 5-04 (cận $192C_x^2C_y^2/(\lambda m)$ khi $\lambda\ge8C_x^2/m$).
- Nhận xét 06.14: trang 6-05.
- Nhận xét 06.15 (đọc thêm): ghi chú diễn giả 6-05 ($4\sqrt{10^{-3}}\approx0{,}1265$).
- Câu ôn nhanh 1–3: ghi chú diễn giả 1-02.
- §10 (ý nghĩa, giới hạn): cột "Giả thiết không được bỏ" của 7-01, trang 7-03, ghi chú diễn giả 7-03.
- §12 (câu hỏi cuối buổi): câu hỏi tự kiểm tra 3 và 4 ở 7-06 (phần (a) và (c)); lời giải ở ghi chú diễn giả.
- Phụ lục D: số $\sum_tc_t\approx0{,}95$, $\sum_tc_t^2\approx0{,}000578$ dùng ở 2-06, 2-11; công thức $c_t$ ở ghi chú diễn giả 2-06; $T=25\,600$ ở ghi chú diễn giả 2-11.
- Phụ lục E (hai quy ước ổn định, Định nghĩa 06.16): ghi chú diễn giả 4-05 và 7-08.

## 5. Ví dụ bổ trợ

Ví dụ xuyên suốt: **hai chương trình SGD trên phân bố $X=1$, $Y=\pm1$** (câu hỏi mở đầu, Ví dụ 06.2, 06.3, Bài tập 06.1) và **tập huấn luyện bốn quan sát** (Ví dụ 06.1, 06.4, 06.6; Bài tập 06.6(a)); thêm ứng dụng **hồi quy logistic trên một triệu hồ sơ** (§3, Nhận xét 06.3, Ví dụ 06.11). Mỗi lần dùng lại trả lời một câu hỏi mới. Hai chương trình: câu hỏi (1-06); oracle không chệch cho $L_D$ hay $L_S$ (2-03, 2-07); giá trị đúng của rủi ro vượt mức kì vọng (2-06, 2-11); độ chệch ở bước thứ hai (2-12). Bốn quan sát: ERM và $G=4$ (2-02); một quan sát dịch nghiệm (3-01); ba giá trị $\lambda$ và Hình 06.1 (3-04); hệ số ổn định của ERM không chính quy hóa (4-01); kiểm chứng minh Mệnh đề 06.11 bằng số (5-03); $\lambda=2$ (5-05); xu hướng của $L_S(\hat w_S)$ cho đánh đổi (6-01). Một triệu hồ sơ: dữ liệu và kết quả của Bài 05 (2-02); một vòng SGD (2-07); ERM có chính quy hóa với $\lambda^*$ (6-04). Bài tập trên mặt trang lấy từ `exercises.md` với cùng số liệu, câu chữ và kết quả: Bài tập 06.1(c), (d) (2-12), 06.10(a), (c) (3-05), 06.2(b) (4-07), 06.6(a) (5-05), 06.4(b) (6-06), 06.4(c) (7-04, 7-05, tổng hợp).

Mọi con số dưới đây đã tính lại bằng Python (thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-06/storyboard/num.py`, `ex.py`) và khớp ghi chú, tệp bài tập. **Không có ví dụ mới mang số mới trên mặt trang.** Hình F2 vẽ đường cong từ công thức của Hệ quả 06.13(a) với số của Ví dụ 06.10 (cũng là hàm của câu ôn nhanh 3); chỉ điểm $\lambda^*=0{,}2$, giá trị $0{,}2$ có nhãn số. Hình F3 là sơ đồ, không có số.

**V1. Câu hỏi mở đầu** (1-06). $L_D(w)=\tfrac12(w-1)^2+\tfrac12(w+1)^2=w^2+1$; $G=4$, $R=1$, $T=1600$: $RG/\sqrt T=4/40=0{,}1$; khoảng $1600/4=400$ vòng.

**V2. Ví dụ 06.1** (2-02). $\sum_ix_i^2=3{,}25$; $\sum_ix_iy_i=2{,}5$; $\sum_iy_i^2=3$; $L_S(w)=\tfrac14(3{,}25w^2-5w+3)$; nghiệm ERM $2{,}5/3{,}25=0{,}769231$; $L_S(0{,}7692)=0{,}269231$; $G=2(BC_x+C_y)C_x=2\cdot2\cdot1=4$. Ứng dụng: $10^4$ bước SGD cho $\mathbb E_\xi\operatorname{opt}_S\le0{,}05$ (Bài 05).

**V3. Ví dụ 06.2** (2-06). $\eta=1/(4\cdot40)=0{,}00625$; $q=1-2\eta=0{,}9875$; $c_t=(1-q^{T-t})/T$; $\sum_tc_t=1-(1-q^T)/(2\eta T)=0{,}9500000$; $\sum_tc_t^2=0{,}000578223$; $\mathbb EL_D(\bar w_T)-1=\sum_tc_t^2\approx0{,}000578$; $0{,}1/0{,}000578=172{,}94\approx173$ lần.

**V4. Nhận xét 06.3** (2-07). $R=5$, $G=1$, $T=m+1=10^6+1$: $5/\sqrt{10^6+1}=0{,}0049999975\approx0{,}005$.

**V5. Ví dụ 06.3** (2-07 Bước 1; 2-11). $\Pr(\bar Y=0)=\binom42/16=0{,}375$. $\mathbb E\bar w_T^2=\tfrac14\cdot0{,}95^2+0{,}75\cdot0{,}000578=0{,}225625+0{,}000434=0{,}226059\approx0{,}2261$; $\mathbb E[\bar w_T\bar Y]=\tfrac14\cdot0{,}95=0{,}2375$; $\mathbb EL_D(\bar w_T)=1{,}226059$; $\mathbb EL_S(\bar w_T)=0{,}226059-0{,}4750+1=0{,}751059$; $\mathbb E\inf_WL_S=1-\tfrac14=0{,}75$; $\mathbb E\operatorname{opt}_S=0{,}001059\approx0{,}0011$; khoảng cách $1{,}226059-0{,}751059=0{,}4750=\tfrac2m\sum_tc_t$; số hạng giữa $-0{,}248941\approx-0{,}2489$; $0{,}4750-0{,}2489=0{,}2261$; cận (b) $0{,}4750+0{,}0011=0{,}4761$. Phụ lục D: $T=25\,600$: $\sum_tc_t=0{,}9875$, $\sum_tc_t^2=3{,}833\cdot10^{-5}$, $\mathbb EL_D=1{,}243818\approx1{,}2438$, khoảng cách $0{,}49375\approx0{,}4938$.

**V6. Định nghĩa 06.4, ba ví dụ** (2-08). $h$ cố định: $0$; $A_{\mathrm{gn}}$: $1$; $\bar Y$ với $m=4$: $\mathbb EL_D(\bar Y)=\mathbb E\bar Y^2+1=1{,}25$, $\mathbb EL_S(\bar Y)=1-\mathbb E\bar Y^2=0{,}75$, hiệu $0{,}5$.

**V7. Đoạn mở §6** (3-01). Thay $z_4$: $\sum_ix_iy_i=1+0+0{,}5-1=0{,}5$; nghiệm $0{,}5/3{,}25=0{,}153846$; dịch $0{,}615385$; $0{,}6154/2=0{,}3077\approx0{,}31$.

**V8. Ví dụ 06.4** (3-04; hình 06.1). $\hat w_S=2{,}5/(3{,}25+2\lambda)$, $\hat w_{S^{(4)}}=0{,}5/(3{,}25+2\lambda)$. $\lambda=0$: $10/13=0{,}7692$, $2/13=0{,}1538$, $0{,}6154$, $L_S=0{,}2692$. $\lambda=1$: $10/21=0{,}4762$, $2/21=0{,}0952$, $8/21=0{,}3810$, $L_S=0{,}339002\approx0{,}3390$. $\lambda=4$: $2/9=0{,}2222$, $2/45=0{,}0444$, $0{,}1778$, $L_S=0{,}512346\approx0{,}5123$. Hình 06.1: khung phải ($\lambda=4$) có trục tung đến $2{,}5$; đường đứt $F_{S^{(4)},4}(w)=2{,}8125w^2-0{,}25w+0{,}75$ vượt $2{,}5$ khi $w>0{,}8345$ và bị cắt ở mép khung (mục 11, điểm 9).

**V9. Hệ số ổn định của ERM khi $\lambda=0$** (4-01). $\hat w=10/13$, $\hat w'=2/13$; tại $z=(1,-1)$: $(23/13)^2-(15/13)^2=(529-225)/169=304/169=1{,}798817\approx1{,}7988$; lưới $201\times201$ trên $\mathcal Z=[-1,1]^2$ cho cực đại $1{,}798817$ tại $(1,-1)$ (khớp: $\lvert\hat w-\hat w'\rvert\,\lvert(\hat w+\hat w')x-2y\rvert\le\tfrac8{13}\cdot\tfrac{38}{13}$).

**V10. Ví dụ 06.5** (4-06). $2^{-m}\sum_k\binom mk\lvert k/m-\tfrac12\rvert$: $m=10$: $0{,}123047\approx0{,}1230$; $m=100$: $0{,}039795\approx0{,}0398$; $m=1000$: $0{,}012613\approx0{,}0126$.

**V11. Ví dụ 06.6** (5-03). $2G/(\lambda m)=2/\lambda$: $2$; $0{,}5$. $2G^2/(\lambda m)=8/\lambda$: $8$; $2$. $\lambda=1$: $\ell(\hat w',z_4)-\ell(\hat w,z_4)=(19/21)^2-(11/21)^2=240/441=0{,}544218$; $\ell(\hat w,z')-\ell(\hat w',z')=(31/21)^2-(23/21)^2=432/441=0{,}979592$; vế phải Bước 2 $=\tfrac14\cdot672/441=8/21=0{,}380952$; vế trái $64/441=0{,}145125$; $2G\lVert\hat w-\hat w'\rVert/m=2\cdot0{,}380952=0{,}761905$; $2/0{,}3810=5{,}25$.

**V12. Ví dụ 06.7** (5-04). $\lambda=0$: nghiệm $\pm1$, cách $2$, hàm lỗi tại $(1,1)$: $0$ và $(-1-1)^2=4$. $\lambda=0{,}1$: khoảng cách $4/(2+0{,}1m)$: $m=10$: $1{,}333333$; $100$: $0{,}333333$; $1000$: $0{,}039216\approx0{,}0392$; cận $8/(0{,}1m)$: $8$; $0{,}8$; $0{,}08$. Bước 3: $\tfrac2m d^2\le\tfrac{2G}md$ cho $d\le G=4$.

**V13. Ví dụ 06.8** (5-03). $\hat w_S=\bar z/\lambda$, $\lvert\bar z\rvert\le1$ nên $\lvert\hat w_S\rvert\le10$; thay $z_i=1$ bằng $-1$: $\bar z$ giảm $2/m$, hai nghiệm cách $2/(\lambda m)=2/10=0{,}2$; khoảng cách tổng quát hóa kì vọng $\mathbb E\bar z^2/\lambda=1/(\lambda m)=0{,}1$; cận $2G^2/(\lambda m)=0{,}2$.

**V14. Ví dụ 06.9** (5-04). $\hat w_S=100/150=0{,}666667$; $\hat w_{S^{(100)}}=99/(149+M^2)$: $M=1$: $0{,}660000$; $M=10$: $0{,}397590\approx0{,}3976$; $M=100$: $0{,}009755\approx0{,}0098$; thay đổi hàm lỗi tại $(1,1)$: $0{,}004489\approx0{,}0045$; $0{,}251786\approx0{,}2518$; $0{,}869475\approx0{,}8695$.

**V15. Ví dụ 06.12** (6-01). $\hat w_S=1/(1+\lambda/2)$; $L_D(\hat w_S)=(\lambda/(2+\lambda))^2$: $\lambda=0{,}2$: $0{,}008264\approx0{,}0083$; $\lambda=2$: $0{,}25$; $\lambda=20$: $0{,}826446\approx0{,}8264$.

**V16. Ví dụ 06.10** (6-04; hình F2). $G=4$, $B=1$, $m=1600$: $\lambda^*=8/40=0{,}2$, $2GB/\sqrt m=8/40=0{,}2$; $\epsilon=0{,}1$: $m\ge4\cdot16/0{,}01=6400$, $\lambda^*=8/80=0{,}1$; SGD: $T\ge16/0{,}01=1600$, $1599$ quan sát. Logistic: $G=1$, $B=5$, $\epsilon=0{,}05$: $m\ge100/0{,}0025=40\,000$; $T\ge25/0{,}0025=10^4$. Hình F2: $Q(\lambda)=2G^2/(\lambda m)+\lambda B^2/2=0{,}02/\lambda+0{,}5\lambda$; $Q(0{,}02)=1{,}01$; $Q(0{,}05)=0{,}425$; $Q(0{,}1)=0{,}25$; $Q(0{,}2)=0{,}2$; $Q(0{,}4)=0{,}25$; $Q(1)=0{,}52$; $Q(2)=1{,}01$ (chỉ $Q(0{,}2)$ có nhãn).

**V17. Ví dụ 06.11** (6-04). $\lambda^*=2/(5\cdot1000)=4\cdot10^{-4}$; $2GB/\sqrt m=10/1000=0{,}01$; $\epsilon_{\mathrm{stab}}=2/(4\cdot10^{-4}\cdot10^6)=0{,}005$; $\tfrac{\lambda^*}2B^2=2\cdot10^{-4}\cdot25=0{,}005$; một vòng SGD $0{,}005$ (V4).

**V18. Nhận xét 06.14** (6-05). $4G^2B^2/(\epsilon\delta)^2=64/(0{,}005)^2=2\,560\,000$; $2\,560\,000/6400=400=1/\delta^2$; $k=\lceil\log_2(2/0{,}05)\rceil=\lceil5{,}32\rceil=6$ (chỉ ở ghi chú diễn giả). Nhận xét 06.15: $G\sqrt{2\epsilon_{\mathrm{opt}}/\lambda}=4\sqrt{10^{-3}}=0{,}126491\approx0{,}1265$.

**V19. Câu hỏi cuối buổi §12** (7-06). $\epsilon_{\mathrm{stab}}(400)=32/(0{,}4\cdot400)=0{,}2$; $\lambda^*=8/20=0{,}4$; $2GB/\sqrt m=0{,}4=0{,}2+0{,}2$; Markov: $0{,}4/0{,}8=0{,}5$.

**V20. Câu ôn nhanh** (ghi chú diễn giả 1-02). (1) $1-0{,}25=0{,}75$ và $\tfrac14\cdot\tfrac34\cdot4=0{,}75$. (2) $1$; $0{,}75$; $1{,}25$. (3) $\lambda=0{,}2$, giá trị $0{,}2$.

**V21. Bài tập 06.1(c), (d)** (2-12; số của `exercises.md`). $w_2=2\eta Y_{i_1}$; $\mathbb E[g_2\mid S,i_1]=2(w_2-\bar Y)$; $\mathbb E[Y_{i_2}\mid w_2]=y/m$; độ chệch $-2y/m$: $m=3$: $\mp0{,}667$; liệt kê $36$ trường hợp có $Y_{i_1}=1$ (trong $72$) với $\eta=0{,}1$: trung bình $g_2-2w_2$ bằng $-2/3$. (d): $\mathbb E[g_2\mid w_2]=2w_2$.

**V22. Bài tập 06.10(c)** (3-05; số của `exercises.md`). $f(w)=w^2$, $w=1$, $u=0$, $v=2$: $2\ge1-0+1=2$. $f(w)=\lvert w\rvert+w^2$, $w=0$, $v=\tfrac12$, $u=1$: $-\tfrac12\ge0-2+1=-1$.

**V23. Bài tập 06.2(b)** (4-07; số của `exercises.md`). Liệt kê bằng phân số: $\mathbb EL_D=3/8=0{,}375$, $\mathbb EL_S=1/8=0{,}125$, khoảng cách $1/4$; trung bình thay một (liệt kê $2^2\cdot2\cdot2$ trường hợp) $1/4$; hệ số ổn định đều nhỏ nhất (liệt kê): $m=2$: $3/4$; $m=4$: $7/16$; khớp $2/m-1/m^2$; cận Lipschitz $2/m=1$ khi $m=2$.

**V24. Bài tập 06.6(a)** (5-05; số của `exercises.md`). $\lambda=2$: $10/29=0{,}344828$; $2/29=0{,}068966$; $8/29=0{,}275862$; $L_S(10/29)=0{,}415577\approx0{,}4156$; cận $2\cdot4/(2\cdot4)=1$; $1/0{,}2759=3{,}62\approx3{,}6$.

**V25. Bài tập 06.4(b), (c)** (6-06, 7-04, 7-05; số của `exercises.md`). $\tfrac12(c+1/c)$: $c=2$: $1{,}25$; $c=\tfrac12$: $1{,}25$; $c=10$: $5{,}05$. (c): $\lambda_0=8/40=0{,}2$; $Q(\lambda_0)=0{,}1\cdot(1+4)=0{,}5$; $B=2$: $\lambda^*=8/80=0{,}1$, $Q(\lambda^*)=16/40=0{,}4$; tỉ số $1{,}25$; $\epsilon_{\mathrm{stab}}$: $32/(0{,}2\cdot1600)=0{,}1$; $32/(0{,}1\cdot1600)=0{,}2$; số hạng khớp $\lambda B^2/2$: $0{,}4$ tại $\lambda_0$, $0{,}2$ tại $\lambda^*$.

## 6. Danh sách trang

Mỗi mục: ID, tiêu đề, loại, thời lượng; **Mặt trang** (các dòng dự kiến, theo thứ tự; `[f]` là fragment; `$$…$$` là công thức hiển thị, tính một dòng; `{{…}}` là chỉ dẫn bố cục, không lên mặt trang); **Ghi chú diễn giả** (ý chính, 40–150 âm tiết, đến ~250 cho trang ý tưởng chứng minh và trang bài tập; viết cho giảng viên và người học; không mã trang, mã ví dụ của storyboard, câu quy trình hay nguồn gốc; luôn kết thúc bằng dòng `note-source`); **Lý do / nối**; **Mục tiêu / nguồn**. Câu trên mặt trang là bản dự kiến đã tự kiểm theo `no-ai-slop` (chế độ Edit) và `eval.md`; người viết deck có thể rút gọn, không thêm khẳng định.

Quy ước chung cho người viết deck:
- Trang kết quả: "Giả thiết:" và "Bảo đảm:" (nhãn của ghi chú), trích số khối của ghi chú một lần.
- Trang tổng quan (bìa, "Mục tiêu", "Nội dung", "Vấn đề trung tâm") viết bằng lời, không kí hiệu, không tiếng Anh. Lần đầu một thuật ngữ trên trang nội dung có tiếng Anh trong ngoặc (bảng mục 10).
- Mọi kí hiệu trên mặt trang đã có ở trang trước hoặc có dòng "Nhắc lại:"/"Kí hiệu:" (bảng đối chiếu mục 12 ghi chỗ đưa vào).
- "Chế độ A", "Chế độ B", "Bước 1 …", "(a)", "(c)" viết thường hoặc in đậm như tên bước, không thành nhãn mới có dấu chấm hay hai chấm trong `<strong>`; chỉ dùng nhãn của danh sách hợp lệ.
- Số thập phân dùng dấu phẩy KaTeX `0{,}2`; dãy số ngăn bằng `;\ `; số từ năm chữ số tách nhóm bằng `\,`; toạ độ có số thập phân viết `(0{,}5;1)` như ghi chú.
- Mỗi trang ví dụ mở bằng dữ kiện dạng danh sách, không câu dẫn. "Diễn giải:" chỉ dùng số có trên chính trang đó.
- Trang ý tưởng chứng minh: lộ trình 3–5 bước, bất đẳng thức hoặc mẹo then chốt, chỗ giả thiết vào, bỏ giả thiết thì hỏng ở đâu; không chép chứng minh đầy đủ của ghi chú.
- Không `\text{}` chứa tiếng Việt trong KaTeX. Trong ghi chú diễn giả, không ghi câu nguồn gốc ("ví dụ mới", "dựng"), mã "V7", "mục 5" (thuật ngữ "quan sát mới" thì giữ), không mở bằng "Trang này", "Mạch này", "Bài này".
- Công thức một dòng khi vừa khung; chỉ ngắt bằng `aligned` khi tràn ở 390 px (đo trong trình duyệt). Ở chế độ đọc hẹp, công thức rộng cuộn ngang tại chỗ.
- Thuật ngữ "tập huấn luyện" theo ghi chú (bản hiện hành), không "mẫu", kể cả trên trang bài tập (mục 11, điểm 6). "Tập huấn luyện lân cận" giữ nguyên (thuật ngữ của Định nghĩa 06.9).

### Mạch 1. Mở đầu (6 trang, 9 phút)

#### `1-01` Học bằng hạ gradient ngẫu nhiên, chính quy hóa và tính ổn định — bìa, điểm vào mạch 1 · 1 phút
- **Mặt trang:** h1 tên bài; h3 "Bài 06"; luận điểm (mục 2, hai câu, bằng lời); "Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1"; "Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN".
- **Ghi chú diễn giả:** Bài 05 chặn độ chênh tối ưu của hàm mà oracle gradient ngẫu nhiên không chệch. Bài 06 hỏi hàm đó là gì trong hai cách dùng dữ liệu. Câu thứ nhất của luận điểm là Hệ quả 06.2: khi mỗi bước dùng một quan sát mới, hàm đó là rủi ro kì vọng, nên cận của Bài 05 chặn thẳng rủi ro vượt mức kì vọng. Câu thứ hai gồm ba kết quả: phân tích rủi ro trên một tập huấn luyện cố định, tính ổn định đều chặn khoảng cách tổng quát hóa kì vọng, và hệ số ổn định $2G^2/(\lambda m)$ của tối thiểu hóa rủi ro thực nghiệm có chính quy hóa. Mọi bảo đảm của bài là theo kì vọng và cho một thuật toán cụ thể. Nguồn: ghi chú Bài 06, đoạn mở đầu, §10.
- **Lý do / nối:** luận điểm cả bài → tiên quyết.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu, §10.

#### `1-02` Tiên quyết và quy ước — mở đầu · 1,5 phút
- **Mặt trang:**
  - **Nhắc lại:** Hệ quả 05.15: với (C), (G1), (G2) cho $F$, $\eta=R/(G\sqrt T)$, $u\in W$, $\lVert w_1-u\rVert\le R$: $\mathbb EF(\bar w_T)-F(u)\le RG/\sqrt T$.
  - $\operatorname{opt}_S(w)=L_S(w)-\inf_{w'\in W}L_S(w')$ (Định nghĩa 04.2); Hệ quả 05.19 chặn $\mathbb E_\xi\operatorname{opt}_S(\bar w_T)$.
  - $h$ cố định: $\mathbb E_SL_S(h)=L_D(h)$ (Mệnh đề 01.7); $A(S;\xi)$, $\xi$ độc lập với $S$ (Định nghĩa 05.18).
  - $\lambda$-lồi mạnh (Định nghĩa 05.6): $f(\alpha w+(1-\alpha)u)\le\alpha f(w)+(1-\alpha)f(u)-\tfrac\lambda2\alpha(1-\alpha)\lVert w-u\rVert^2$, $\alpha\in[0,1]$.
  - Hàm lỗi bình phương trên quả cầu bán kính $B$, $\lVert x\rVert\le C_x$, $\lvert y\rvert\le C_y$: $G$-Lipschitz với $G=2(BC_x+C_y)C_x$ (Định nghĩa 05.4).
- **Ghi chú diễn giả:** Hệ quả 05.15 cần một oracle không chệch cho chính hàm $F$; mạch 2 hỏi $F$ là $L_D$ hay $L_S$. Sai số tối ưu thực nghiệm đo bộ giải trên tập huấn luyện. Mệnh đề 01.7 chỉ đúng khi $h$ không phụ thuộc tập huấn luyện; câu ôn nhanh 2 cho thấy với $\bar Y$ tính từ tập huấn luyện, $\mathbb EL_S(\bar Y)=0{,}75$ còn $\mathbb EL_D(\bar Y)=1{,}25$. Định nghĩa lồi mạnh với $f=\tfrac\lambda2\lVert\cdot\rVert^2$ đúng với dấu bằng (câu ôn nhanh 1: hai vế bằng $0{,}75$). Câu ôn nhanh 3: $0{,}02/\lambda+0{,}5\lambda$ nhỏ nhất bằng $0{,}2$ tại $\lambda=0{,}2$, đúng hàm xuất hiện lại ở mạch 6. Nguồn: ghi chú Bài 06, Kiến thức tiên quyết, Câu hỏi ôn nhanh.
- **Lý do / nối:** các kết quả của Bài 01–05 dùng trên mặt trang được nhắc lại ở đây → mục tiêu.
- **Mục tiêu / nguồn:** 1–5; Kiến thức tiên quyết.

#### `1-03` Mục tiêu — mở đầu · 1 phút
- **Mặt trang (danh sách đánh số, bằng lời, không kí hiệu; trần 80):**
  1. Xác định hàm mà gradient ngẫu nhiên không chệch; cận với quan sát mới.
  2. Tách rủi ro vượt mức kì vọng: khoảng cách tổng quát hóa kì vọng, sai số tối ưu thực nghiệm.
  3. Chứng minh ổn định đều chặn khoảng cách tổng quát hóa kì vọng.
  4. Chặn khoảng cách hai nghiệm có chính quy hóa; hệ số ổn định của hồi quy ridge, logistic.
  5. Chọn hệ số chính quy hóa, cỡ mẫu; phản ví dụ bỏ giả thiết.
- **Ghi chú diễn giả:** Mục tiêu 1 so hai cách: mỗi bước một quan sát mới, và rút đều từ một tập huấn luyện đã lưu; cận là cận rủi ro vượt mức kì vọng. Mục tiêu 2 áp dụng cho đầu ra của một bộ giải bất kì. Ở mục tiêu 3, đại lượng được chặn là trị tuyệt đối của khoảng cách tổng quát hóa kì vọng. Mục tiêu 4 là cho tối thiểu hóa rủi ro thực nghiệm có chính quy hóa, với hồi quy ridge và hồi quy logistic. Ở mục tiêu 5, hệ số chọn từ cận đánh đổi khớp–ổn định, và ba giả thiết bị bỏ là dùng quan sát mới, có chính quy hóa và dữ liệu bị chặn. Nguồn: ghi chú Bài 06, Mục tiêu học tập.
- **Lý do / nối:** tiêu chí kiểm tra → nội dung.
- **Mục tiêu / nguồn:** tất cả; Mục tiêu học tập.

#### `1-04` Nội dung — mở đầu · 0,5 phút
- **Mặt trang:** `ol start="2"` với liên kết `#/2`…`#/7`: 2. Quan sát mới và tập huấn luyện lưu lại; 3. ERM có chính quy hóa; 4. Tính ổn định và khoảng cách tổng quát hóa kì vọng; 5. Tính ổn định của ERM có chính quy hóa; 6. Đánh đổi khớp–ổn định; 7. Tổng kết. Dòng đọc trước: "Đọc trước: UML §14.5, §13.1."
- **Ghi chú diễn giả:** Mạch 2 so hai cách lấy mẫu cho cùng phép cập nhật và tách rủi ro của đầu ra thành hai phần. Mạch 3 thêm một số hạng phạt chuẩn vào rủi ro thực nghiệm. Mạch 4 chặn phần khoảng cách tổng quát hóa bằng tính ổn định của thuật toán. Mạch 5 tính hệ số ổn định của quy tắc có chính quy hóa. Mạch 6 chọn hệ số chính quy hóa và cỡ mẫu. Nguồn: ghi chú Bài 06; §13.
- **Lý do / nối:** bản đồ mạch → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §13.

#### `1-05` Vấn đề trung tâm — mở đầu · 1 phút
- **Mặt trang:** một hộp `div.box`: "**Câu hỏi:** khi nào tối ưu trở thành học?" (9 âm tiết kể cả nhãn).
- **Ghi chú diễn giả** (câu trả lời theo mạch, không trên mặt trang): Cụ thể: khi nào một thuật toán tối ưu cũng là một thuật toán học, tức có bảo đảm cho rủi ro kì vọng của đầu ra? (2) khi mỗi bước dùng một quan sát mới, oracle không chệch cho $L_D$ và cận của Bài 05 chặn rủi ro vượt mức kì vọng; khi dùng lại tập huấn luyện, rủi ro vượt mức kì vọng không quá khoảng cách tổng quát hóa kì vọng cộng sai số tối ưu thực nghiệm; (3) chính quy hóa cho nghiệm duy nhất, ít nhạy khi thay một quan sát; (4) thuật toán ổn định đều có khoảng cách tổng quát hóa kì vọng không quá hệ số ổn định; (5) với hàm lỗi lồi, Lipschitz, hệ số đó là $2G^2/(\lambda m)$; (6) với $\lambda^*$, rủi ro vượt mức kì vọng không quá $2GB/\sqrt m$. Nguồn: ghi chú Bài 06, đoạn mở đầu, §10.
- **Lý do / nối:** một vấn đề cốt lõi → câu hỏi cụ thể.
- **Mục tiêu / nguồn:** tất cả; đoạn mở đầu.

#### `1-06` Ví dụ: hai chương trình hạ gradient ngẫu nhiên — ví dụ dẫn nhập · 4 phút
- **Mặt trang:**
  - $X=1$, $Y=\pm1$ với xác suất $\tfrac12$; $\ell(w,(x,y))=(wx-y)^2$, $W=[-1,1]$; $L_D(w)=w^2+1$, $\min_WL_D=1$.
  - Hạ gradient ngẫu nhiên (SGD) có chiếu, $w_1=0$, $T=1600$, $\eta=0{,}00625$: $w_{t+1}=\operatorname{proj}_W\big(w_t-2\eta(w_t-y_t)\big)$.
  - Chương trình thứ nhất: $y_t$ là nhãn của một quan sát mới (fresh observation) rút từ $D$.
  - Chương trình thứ hai: $y_t$ rút đều có hoàn lại từ $m=4$ quan sát đã lưu.
  - Hệ quả 05.15 cho cả hai cận $RG/\sqrt T=0{,}1$ với $G=4$, $R=1$.
  - **Câu hỏi:** $\mathbb EL_D(\bar w_T)-1$ của hai chương trình khác nhau thế nào?
- **Ghi chú diễn giả:** Hai chương trình có cùng phép cập nhật và cùng các hằng số của Hệ quả 05.15, chỉ khác nguồn của nhãn. Cận $0{,}1$ chỉ đúng cho chương trình thứ nhất. Ở đó nhãn mới độc lập với điểm lặp hiện tại, nên gradient ngẫu nhiên không chệch cho $L_D$, và theo kì vọng $L_D(\bar w_T)$ vượt $1$ khoảng $0{,}0006$. Ở chương trình thứ hai, khi biết bốn quan sát, gradient ngẫu nhiên không chệch cho $L_S$; theo kì vọng, độ chênh tối ưu của $L_S$ khoảng $0{,}001$, còn $L_D(\bar w_T)$ vượt $1$ khoảng $0{,}226$. Phần chênh nằm ở khoảng cách giữa $L_D$ và $L_S$ tại một điểm tính từ chính bốn quan sát đó. Nguồn: ghi chú Bài 06, Câu hỏi mở đầu và hai đoạn sau.
- **Lý do / nối:** ví dụ dẫn nhập trước mọi định nghĩa; ví dụ xuyên suốt của mạch 2 → tiêu đề mạch 2.
- **Mục tiêu / nguồn:** 1, 2; Câu hỏi mở đầu.

### Mạch 2. Quan sát mới và tập huấn luyện lưu lại (13 trang, 32 phút)

#### `2-00` 2. Quan sát mới và tập huấn luyện lưu lại — tiêu đề mạch, điểm vào mạch 2 · 0,5 phút
- **Mặt trang:** "2."; h2 "Quan sát mới và tập huấn luyện lưu lại"; `p.strand-lead` (bảng mạch, 24 âm tiết); `p.strand-keys`: "quan sát mới · rủi ro vượt mức kì vọng · khoảng cách tổng quát hóa kì vọng · bảo đảm cấp thuật toán".
- **Ghi chú diễn giả:** Hai chương trình của câu hỏi mở đầu là hai cách lấy mẫu. Với quan sát mới, bộ giải của Bài 05 trở thành một thuật toán học, và cỡ mẫu của nó bằng số bước trừ một. Với tập huấn luyện dùng lại, cận của Bài 05 chỉ chặn sai số tối ưu thực nghiệm; rủi ro kì vọng của đầu ra còn cần một cận cho khoảng cách tổng quát hóa kì vọng. Mạch kết thúc bằng phép tính chính xác cho cả hai chương trình. Nguồn: ghi chú Bài 06, §1–§5.
- **Lý do / nối:** mạch 1 → thiết lập.
- **Mục tiêu / nguồn:** 1, 2; §1–§5.

#### `2-01` Hai chế độ lấy mẫu — thiết lập · 2,5 phút
- **Mặt trang:**
  - $z=(x,y)\sim D$ chưa biết; $\ell(w,z)\ge0$ lồi theo $w\in W$; $W\subset\mathbb R^p$ khác rỗng, đóng, lồi.
  - Chế độ A, quan sát mới: $Z_1,Z_2,\ldots\sim D$ độc lập, mỗi quan sát dùng một lần.
  - Chế độ B, tập huấn luyện lưu lại: $S\sim D^m$ theo (T1), dùng nhiều lần.
  - Mục tiêu: $\mathbb EL_D$ của đầu ra, theo mọi nguồn ngẫu nhiên.
  - Điểm so sánh: $u\in W$ không phụ thuộc tập huấn luyện, hoặc $\inf_{w\in W}L_D(w)$.
- **Ghi chú diễn giả:** Các đại lượng chia theo nguồn ngẫu nhiên. Cố định: $D$, $W$, $\ell$, $\eta$, $T$, $w_1$, $u$, các hằng số. Ngẫu nhiên theo dữ liệu: dòng quan sát ở chế độ A, tập huấn luyện và $L_S$ ở chế độ B. Ở chế độ B, chỉ số rút từ $S$ là nguồn ngẫu nhiên riêng $\xi$ của thuật toán, và điểm lặp ngẫu nhiên theo cả hai. Ở chế độ A, các lần rút chính là các quan sát. Giả thiết (T2): $\ell(w,\cdot)$ đo được và $L_D(w)<\infty$ trên $W$. Với hàm lỗi bình phương, thêm dữ liệu bị chặn: $\lVert x\rVert\le C_x$, $\lvert y\rvert\le C_y$. Các kết quả chính của bài không giả sử hàm lỗi bị chặn. Nguồn: ghi chú Bài 06, §1, §2.
- **Lý do / nối:** khung chung trước mọi kết quả → ví dụ xuyên suốt.
- **Mục tiêu / nguồn:** 1, 2; §1, §2.

#### `2-02` Ví dụ: bốn quan sát và một triệu hồ sơ — ví dụ xuyên suốt (Ví dụ 06.1, khối ứng dụng §3), danh sách một cột (deck) · 2,5 phút
- **Mặt trang** {{hai thẻ `grid2`}}:
  - {{thẻ trái}} **Ví dụ 06.1.** $z_1=(1,1)$, $z_2=(1,0)$, $z_3=(0{,}5;1)$, $z_4=(-1,-1)$; hàm lỗi bình phương, $W=[-1,1]$, $B=C_x=C_y=1$.
  - $L_S(w)=\tfrac14(3{,}25w^2-5w+3)$; nghiệm tối thiểu hóa rủi ro thực nghiệm (ERM) $2{,}5/3{,}25\approx0{,}7692$; $G=4$.
  - {{thẻ phải, tiêu đề thẻ h3 "Một triệu hồ sơ"}} $m=10^6$, $\lVert x\rVert\le1$, hàm lỗi logistic, $G=1$; quả cầu $\lVert w\rVert\le5$.
  - Bài 05: $10^4$ bước SGD cho $\mathbb E_\xi\operatorname{opt}_S\le0{,}05$; cận cho $L_S$, không cho $L_D$.
  - **Câu hỏi:** bảo đảm nào cho $L_D$ khi SGD đi đúng một vòng qua $10^6$ hồ sơ?
- **Ghi chú diễn giả:** Tập huấn luyện bốn quan sát là cố định và trở lại ở mạch 3 và mạch 5, khi thay quan sát thứ tư. Rủi ro thực nghiệm là đa thức bậc hai có hệ số dẫn dương, nên điểm có đạo hàm $0$ là nghiệm ERM trên $W$, với $L_S\approx0{,}2692$. Hằng số $G=4$ đến từ đạo hàm $2(wx-y)x$ trên $W$ và Mệnh đề 05.5(a). Ứng dụng tiếp hồi quy logistic của Bài 05, với nhãn $\tilde y=2y-1$ và $G=1$ theo Ví dụ 05.9. Câu hỏi thực hành của ghi chú có thêm vế thứ hai, cho tối thiểu hóa rủi ro thực nghiệm có chính quy hóa; vế này được trả lời ở mạch 6. Nguồn: ghi chú Bài 06, §3, Ví dụ 06.1 và khối ứng dụng.
- **Lý do / nối:** đối tượng xuyên suốt đặt ở mục của ghi chú (§3) → gradient trên quan sát mới.
- **Mục tiêu / nguồn:** 1, 4; §3.

#### `2-03` Gradient trên một quan sát mới — trực quan, kết quả (Bổ đề 06.1) · 3 phút
- **Mặt trang:**
  - **Nhắc lại:** kì vọng có điều kiện theo lịch sử $\mathcal F_{t-1}=\sigma(Z_1,\ldots,Z_{t-1})$ (Bài 05).
  - **Trực quan.** $w_t$ chỉ phụ thuộc $\mathcal F_{t-1}$, chưa thấy $Z_t$; khi biết $\mathcal F_{t-1}$, $Z_t$ vẫn có phân bố $D$.
  - Nên $v(w_t,Z_t)$ có trung bình là một dưới gradient của $L_D$ tại $w_t$.
  - **Bổ đề 06.1.** **Giả thiết:** $\ell(\cdot,z)$ lồi với mọi $z$, $L_D<\infty$ trên $\mathbb R^p$; $v(w,z)\in\partial\ell(\cdot,z)(w)$ đo được, $\mathbb E\lVert v(w,Z)\rVert<\infty$.
  - **Bảo đảm:** tất định: $L_D$ lồi, hữu hạn, và $\psi(w)=\mathbb E_{Z\sim D}v(w,Z)\in\partial L_D(w)$.
- **Ghi chú diễn giả:** Lộ trình chứng minh: với từng $z$, bất đẳng thức lồi và bất đẳng thức dưới gradient $\ell(u,z)\ge\ell(w,z)+\langle v(w,z),u-w\rangle$ đúng; lấy kì vọng theo $Z$ hai vế. Số hạng tích vô hướng khả tích nhờ bất đẳng thức Cauchy–Schwarz và $\mathbb E\lVert v(w,Z)\rVert<\infty$. Bổ đề không đổi chỗ đạo hàm và kì vọng, nên không cần $\ell$ khả vi. Câu trực quan dùng tính độc lập của $Z_t$ với các quan sát trước; khi quan sát được rút lại từ một tập huấn luyện đã lưu, điểm lặp đã phụ thuộc quan sát đó. Nguồn: ghi chú Bài 06, §4, Bổ đề 06.1 và chứng minh; UML §14.5.
- **Lý do / nối:** trọng tâm trực quan 1 của deck; công cụ cho (G1) → hệ quả chính của §4.
- **Mục tiêu / nguồn:** 1; §4, Bổ đề 06.1.

#### `2-04` Hạ gradient ngẫu nhiên với quan sát mới — kết quả (Hệ quả 06.2) · 2,5 phút
- **Mặt trang:**
  - **Hệ quả 06.2.** **Giả thiết:** $Z_1,Z_2,\ldots$ độc lập cùng phân bố $D$; hàm lỗi, $v$ như Bổ đề 06.1; $G>0$, $\mathbb E_{Z\sim D}\lVert v(w,Z)\rVert^2\le G^2$ trên $W$.
  - $W$ khác rỗng, đóng, lồi; $w_1\in W$ tất định, $R>0$; Thuật toán 05.11 với $\xi_t=Z_t$, $\varphi=v$, $\eta=R/(G\sqrt T)$.
  - **Bảo đảm:** theo kì vọng theo $Z_1,\ldots,Z_{T-1}$, với mọi $u\in W$ thỏa $\lVert w_1-u\rVert\le R$:
  - $$\mathbb EL_D(\bar w_T)-L_D(u)\le\frac{RG}{\sqrt T}.$$
  - Nếu $\lVert w_1-u\rVert\le R$ với mọi $u\in W$: cận cho rủi ro vượt mức kì vọng (expected excess risk) $\mathbb EL_D(\bar w_T)-\inf_WL_D$; $T\ge R^2G^2/\epsilon^2$ cho mức $\epsilon$.
- **Ghi chú diễn giả:** Rủi ro vượt mức kì vọng là kì vọng theo mọi nguồn ngẫu nhiên của rủi ro vượt mức so với $W$, tức của sai số ước lượng của Bài 04. Đầu ra $\bar w_T$ dùng đúng $T-1$ quan sát, mỗi quan sát một lần, nên cỡ mẫu bằng số bước trừ một. Đây là bảo đảm cấp thuật toán (algorithm-level): cho đầu ra của một thuật toán cụ thể, khác bảo đảm cấp lớp (class-level) của Bài 02–04 đúng đồng thời cho mọi giả thuyết của lớp. Cận phụ thuộc số chiều $p$ chỉ qua $G$ và $R$. Nguồn: ghi chú Bài 06, §4, Hệ quả 06.2 và hai đoạn sau.
- **Lý do / nối:** phát biểu sau trực quan; trang ý tưởng chứng minh riêng ở sau.
- **Mục tiêu / nguồn:** 1; Hệ quả 06.2.

#### `2-05` Ý tưởng chứng minh: hạ gradient ngẫu nhiên với quan sát mới — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - **Bước 1 ((T1) dạng đầy đủ).** $Z_t$ độc lập: $(v,D)$ là oracle với $\xi_t=Z_t$; Bổ đề 06.1(b) cho (G1), $F=L_D$.
  - **Bước 2.** (G2) là cận gradient; Bổ đề 06.1(a) và $W$ khác rỗng, đóng, lồi cho (C).
  - **Bước 3.** Hệ quả 05.15 với $F=L_D$; kì vọng theo $\xi_1,\ldots,\xi_{T-1}=Z_1,\ldots,Z_{T-1}$.
  - Vòng thứ hai trên tập huấn luyện: $Z_t$ đã dùng, Bước 1 hỏng.
- **Ghi chú diễn giả** (~150 âm tiết): Toàn bộ nội dung xác suất mới nằm ở Bước 1: tính độc lập của các quan sát là điều kiện để dãy lần rút có cấu trúc của Định nghĩa 05.10. Theo bất đẳng thức Cauchy–Schwarz và cận gradient, $\mathbb E\lVert v(w,Z)\rVert\le G<\infty$ trên $W$, nên Bổ đề 06.1(b) áp dụng được. Bước 2 không cần xác suất: tính lồi của $L_D$ thừa hưởng từ tính lồi của từng $\ell(\cdot,z)$. Bước 3 chỉ là thay $F=L_D$. Kỹ thuật kì vọng có điều kiện theo lịch sử, cùng tổng triệt tiêu và trung bình các điểm lặp, dùng bên trong Hệ quả 05.15: biết lịch sử thì $w_t$ cố định, còn quan sát mới có trung bình là dưới gradient. Khi SGD đi vòng thứ hai qua cùng tập huấn luyện, điểm lặp đã phụ thuộc quan sát sắp dùng, nên Bước 1 không còn đúng; ví dụ chương trình thứ hai tính hậu quả bằng số. Nguồn: ghi chú Bài 06, chứng minh Hệ quả 06.2; Nhận xét 06.3.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; chỗ dùng tính độc lập → ví dụ bằng số.
- **Mục tiêu / nguồn:** 1; chứng minh Hệ quả 06.2.

#### `2-06` Ví dụ: chương trình dùng quan sát mới — ví dụ (Ví dụ 06.2) · 2 phút
- **Mặt trang:**
  - Chương trình thứ nhất; $v(w,(1,y))=2(w-y)$, $\lvert v\rvert\le4$ trên $W$: $G=4$; $R=1$; $\eta=R/(G\sqrt T)=1/(4\cdot40)=0{,}00625$.
  - Hệ quả 06.2(b): $\mathbb EL_D(\bar w_{1600})-1\le0{,}1$, với $1599$ quan sát mới.
  - $2\eta<1$: $w_{t+1}=(1-2\eta)w_t+2\eta y_t$ là tổ hợp lồi, phép chiếu không tác động; $\bar w_T=\sum_tc_ty_t$, $c_t$ tất định.
  - $L_D(\bar w_T)-1=\bar w_T^2$; các $y_t$ độc lập, kì vọng $0$: $\mathbb E\bar w_T^2=\sum_tc_t^2\approx0{,}000578$.
  - **Diễn giải:** giá trị đúng $0{,}000578$ nhỏ hơn cận $0{,}1$ khoảng $173$ lần.
- **Ghi chú diễn giả:** Với $q=1-2\eta=0{,}9875$, quy nạp cho $c_t=(1-q^{T-t})/T$ (Phụ lục D), với $\sum_tc_t\approx0{,}95$ và $\sum_tc_t^2\approx0{,}000578$. Vì $y_t^2=1$ và các tích chéo $y_ty_s$ với $t\ne s$ có kì vọng $0$, kì vọng của $\bar w_T^2$ chỉ còn tổng các $c_t^2$. Cận của Hệ quả 06.2 đúng với mọi phân bố thỏa giả thiết, nên trên một phân bố cụ thể nó có thể lỏng nhiều. Nguồn: ghi chú Bài 06, Ví dụ 06.2; Phụ lục D.
- **Lý do / nối:** kiểm hệ quả bằng số, trả lời nửa đầu của câu hỏi mở đầu → một vòng và nhiều vòng.
- **Mục tiêu / nguồn:** 1; Ví dụ 06.2.

#### `2-07` Một vòng và nhiều vòng qua tập huấn luyện — kết quả (Nhận xét 06.3), vấn đề (đoạn mở §5, Ví dụ 06.3 Bước 1) · 3 phút
- **Mặt trang:**
  - **Nhận xét 06.3.** $S\sim D^m$ theo (T1), $T=m+1$, mỗi $Z_i$ dùng một lần theo thứ tự: Hệ quả 06.2 cho $\mathbb E_SL_D(\bar w_{m+1})-\inf_WL_D\le RG/\sqrt{m+1}$.
  - Một triệu hồ sơ, $w_1=0$, $R=5$: một vòng cho cận $5/\sqrt{10^6+1}\approx0{,}005$.
  - Từ vòng thứ hai, $w_t$ phụ thuộc quan sát sắp dùng; chỉ số rút đều, có hoàn lại từ $S$: $\mathbb E[g_t\mid S,\mathcal F_{t-1}]\in\partial L_S(w_t)$.
  - **Ví dụ.** Chương trình thứ hai, $\bar Y=\tfrac14\sum_iY_i$: $\mathbb E[g_t\mid S,\mathcal F_{t-1}]=2(w_t-\bar Y)=L_S'(w_t)$, còn $L_D'(w_t)=2w_t$.
  - Hiệu $-2\bar Y$ bằng $0$ khi và chỉ khi $\bar Y=0$, với xác suất $0{,}375$.
- **Ghi chú diễn giả:** Với $m$ quan sát, chỉ chạy được $m+1$ bước dùng quan sát mới. Cận $0{,}005$ trả lời vế thứ nhất của câu hỏi thực hành. Ở chế độ B, khi biết $S$, Hệ quả 05.19 chặn $\mathbb E_\xi\operatorname{opt}_S(\bar w_T)$ với mọi tập huấn luyện, nhưng đại lượng cần chặn là $L_D(\bar w_T)$, và đầu ra phụ thuộc chính $S$. Trong chương trình thứ hai, $\bar Y=0$ khi đúng hai trong bốn nhãn bằng $1$, xác suất $6/16$. Nguồn: ghi chú Bài 06, Nhận xét 06.3, đoạn sau; §5, đoạn mở và Câu hỏi; Ví dụ 06.3, Bước 1.
- **Lý do / nối:** câu nối trên mặt trang từ cụm quan sát mới sang cụm tập huấn luyện lưu lại (bài học deck 01) → cần một đại lượng đo phần chênh.
- **Mục tiêu / nguồn:** 1; Nhận xét 06.3, §5.

#### `2-08` Khoảng cách tổng quát hóa kì vọng — định nghĩa (Định nghĩa 06.4), ví dụ · 2 phút
- **Mặt trang:**
  - Mệnh đề 01.7: $\mathbb E_SL_S(h)=L_D(h)$ khi $h$ cố định; $A(S;\xi)$ được tính từ chính $S$.
  - **Định nghĩa 06.4.** $A$ có nguồn ngẫu nhiên riêng, $S\sim D^m$, $\xi$ độc lập với $S$, $\ell$ thỏa (T2), hai kì vọng hữu hạn.
  - Khoảng cách tổng quát hóa kì vọng (expected generalization gap) với cỡ mẫu $m$:
  - $$\mathbb E_{S,\xi}\big[L_D(A(S;\xi))-L_S(A(S;\xi))\big].$$
  - Một số có dấu, phụ thuộc $D$, $m$, $A$.
  - **Ví dụ.** $h$ cố định: $0$; thuật toán ghi nhớ $A_{\mathrm{gn}}$ (Ví dụ 01.8): $1$; $A(S)=\bar Y$, $Y_i=\pm1$, $m=4$, $\ell=(w-y)^2$: $1{,}25-0{,}75=0{,}5$.
- **Ghi chú diễn giả:** Khi $A$ tất định, khoảng cách tổng quát hóa kì vọng là kì vọng theo $S$ của khoảng cách tổng quát hóa ở Định nghĩa 01.10. Ví dụ thứ ba là câu ôn nhanh 2: với điểm cố định $0$, $\mathbb EL_S(0)=L_D(0)=1$; với $\bar Y$ tính từ tập huấn luyện, $\mathbb EL_S(\bar Y)=0{,}75$ còn $\mathbb EL_D(\bar Y)=1{,}25$. Đại lượng $\mathbb E\lvert L_D-L_S\rvert$ lớn hơn hoặc bằng trị tuyệt đối của khoảng cách tổng quát hóa kì vọng, và có thể dương khi khoảng cách này bằng $0$; mạch 4 trở lại điểm này. Nguồn: ghi chú Bài 06, §5, Định nghĩa 06.4 và ba đoạn sau.
- **Lý do / nối:** câu mở khẳng định trước định nghĩa (không mở khái niệm bằng định nghĩa); ba ví dụ của ghi chú → phân tích rủi ro.
- **Mục tiêu / nguồn:** 2; Định nghĩa 06.4.

#### `2-09` Phân tích rủi ro trên một tập huấn luyện lưu lại — trực quan, kết quả (Mệnh đề 06.5) · 2,5 phút
- **Mặt trang:**
  - **Trực quan.** Rủi ro vượt mức gồm phần do đầu ra phụ thuộc $S$ và phần $\operatorname{opt}_S$ của bộ giải.
  - **Mệnh đề 06.5.** **Giả thiết:** mỗi $Z_i\sim D$ (dạng yếu của (T1)); $\tilde w=A(S;\xi)\in W$, $\xi$ độc lập với $S$, $\mathbb EL_D(\tilde w),\mathbb EL_S(\tilde w)<\infty$;
  - $\ell\ge0$ đo được, $L_D<\infty$ trên $W$; $u\in W$ cố định.
  - **Bảo đảm:** (a) với mọi $(S,\xi)$: $$L_D(\tilde w)-L_D(u)=[L_D(\tilde w)-L_S(\tilde w)]+[L_S(\tilde w)-L_S(u)]+[L_S(u)-L_D(u)],$$
  - số hạng giữa $\le\operatorname{opt}_S(\tilde w)$, số hạng cuối có kì vọng $0$; (b) theo kì vọng: $\mathbb EL_D(\tilde w)-\inf_WL_D\le\mathbb E[L_D(\tilde w)-L_S(\tilde w)]+\mathbb E\operatorname{opt}_S(\tilde w)$.
- **Ghi chú diễn giả:** Vế trái của (b) là rủi ro vượt mức kì vọng so với $W$; vế phải là khoảng cách tổng quát hóa kì vọng của chính thuật toán cộng kì vọng của sai số tối ưu thực nghiệm. Mệnh đề là bản kì vọng của Mệnh đề 04.3 cho một thuật toán: số hạng $2r$ của lớp (khi tập huấn luyện là $r$-đại diện) được thay bằng khoảng cách tổng quát hóa kì vọng của thuật toán, và không có sai số xấp xỉ vì đối tượng so sánh nằm trong $W$. Khi $A$ trả về một $h$ cố định, phần thứ nhất bằng $0$. Nguồn: ghi chú Bài 06, §5, Mệnh đề 06.5 và đoạn sau.
- **Lý do / nối:** trực quan trước phát biểu; ví dụ của Định nghĩa 06.4 ở trang trước → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 2; Mệnh đề 06.5.

#### `2-10` Ý tưởng chứng minh: phân tích rủi ro — ý tưởng chứng minh · 2,5 phút
- **Mặt trang:**
  - **Bước 1.** Cộng và trừ $L_S(\tilde w)$ và $L_S(u)$, như Mệnh đề 04.3: được đẳng thức (a).
  - **Bước 2 ($u\in W$).** $L_S(u)\ge\inf_{w'\in W}L_S(w')$, nên $L_S(\tilde w)-L_S(u)\le\operatorname{opt}_S(\tilde w)$.
  - **Bước 3 ($u$ không phụ thuộc $S$).** Mệnh đề 01.7: $\mathbb E_SL_S(u)=L_D(u)$; chỉ cần mỗi $Z_i$ có phân bố $D$.
  - **Bước 4.** Lấy kì vọng, rồi cận dưới đúng theo $u\in W$.
  - Nếu $u$ được chọn theo $S$, chẳng hạn $u=\tilde w$: Bước 3 không còn đúng.
- **Ghi chú diễn giả** (~110 âm tiết): Bất đẳng thức duy nhất là Bước 2; còn lại là đẳng thức và tính tuyến tính của kì vọng. Bước 1 hữu hạn trên từng tập huấn luyện vì $\ell$ nhận giá trị thực và $L_D<\infty$ trên $W$; Bước 4 dùng các kì vọng hữu hạn của giả thiết. Bước 3 là chỗ duy nhất cần điểm so sánh không phụ thuộc tập huấn luyện; với $u=\tilde w$, số hạng cuối chính là âm khoảng cách tổng quát hóa của đầu ra, và không có lý do để nó có kì vọng $0$. Mệnh đề chỉ cần dạng yếu của (T1); để đánh giá $L_D(\tilde w)$, cần một cận cho khoảng cách tổng quát hóa kì vọng, hoặc một tập kiểm tra độc lập với $S$. Nguồn: ghi chú Bài 06, chứng minh Mệnh đề 06.5.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; chỗ giả thiết vào → kiểm bằng chương trình thứ hai.
- **Mục tiêu / nguồn:** 2; chứng minh Mệnh đề 06.5.

#### `2-11` Ví dụ: chương trình chạy nhiều vòng — ví dụ (Ví dụ 06.3) · 3 phút
- **Mặt trang:**
  - $S=((1,Y_1),\ldots,(1,Y_4))\sim D^4$; $i_t$ đều, có hoàn lại, độc lập với $S$; $T$, $\eta$ như chương trình thứ nhất.
  - $\bar w_T=\sum_tc_tY_{i_t}$; $\mathbb E[Y_{i_t}Y_{i_s}]=\tfrac1m$ khi $t\ne s$: $\mathbb E\bar w_T^2=\tfrac1m(\sum_tc_t)^2+(1-\tfrac1m)\sum_tc_t^2\approx0{,}2261$.
  - Bảng một hàng: $\mathbb EL_D(\bar w_T)\approx1{,}2261$ | $\mathbb EL_S(\bar w_T)\approx0{,}7511$ | $\mathbb E\inf_WL_S=0{,}75$ | $\mathbb E\operatorname{opt}_S\approx0{,}0011$ | khoảng cách tổng quát hóa kì vọng $0{,}4750$
  - Mệnh đề 06.5(b), $u=0$: $0{,}4750+0{,}0011=0{,}4761\ge0{,}2261$.
  - **Diễn giải:** $\mathbb E\operatorname{opt}_S$ nhỏ, nhưng rủi ro vượt mức kì vọng $0{,}2261$ vượt cận $RG/\sqrt T=0{,}1$; phần chênh nằm ở khoảng cách $0{,}4750$.
  - Cần chặn khoảng cách tổng quát hóa kì vọng bằng tính chất của thuật toán.
- **Ghi chú diễn giả:** Tập huấn luyện ở đây là ngẫu nhiên, khác tập huấn luyện bốn quan sát đã cho. Vì $y^2=1$, $L_S(0)=L_D(0)=1$ trên mọi tập huấn luyện, nên số hạng cuối của Mệnh đề 06.5 bằng $0$; số hạng giữa có kì vọng $-0{,}2489$, và $0{,}4750-0{,}2489=0{,}2261$. Khoảng cách tổng quát hóa kì vọng bằng $\tfrac2m\sum_tc_t$. Chạy thêm vòng lặp không làm nó giảm: với $T=25\,600$, nó tăng lên $0{,}4938$ (Phụ lục D). Hội tụ đều là cách của Bài 02–04 qua tập đại diện cho cả lớp. Nguồn: ghi chú Bài 06, Ví dụ 06.3, đoạn sau; Phụ lục D.
- **Lý do / nối:** trả lời nửa sau câu hỏi mở đầu; câu nối trên mặt trang sang cách chặn bằng tính chất của thuật toán → bài tập của mạch.
- **Mục tiêu / nguồn:** 1, 2; Ví dụ 06.3, đoạn cuối §5.

#### `2-12` Bài tập: độ chệch của gradient ở bước thứ hai — bài tập (Bài tập 06.1(c), (d)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - Phân bố của câu hỏi mở đầu, hàm lỗi bình phương, $W=[-1,1]$, $w_1=0$, $\eta\in(0,\tfrac12)$; $Y_j$: nhãn của $Z_j$, $\bar Y=\tfrac1m\sum_jY_j$.
  - (c) Chế độ B với $m\ge2$: tính $w_2$, $\mathbb E[g_2\mid S,i_1]$ và $\mathbb E[g_2\mid w_2]$, rồi so với $L_D'(w_2)$. Tính độ chệch $\mathbb E[g_2\mid w_2]-L_D'(w_2)$ với $m=3$.
  - (d) Một vòng theo thứ tự, $g_t=2(w_t-Y_t)$: tính $\mathbb E[g_2\mid w_2]$ và chỉ ra giả thiết làm độ chệch bằng $0$.
  - **Lời giải:** (c) $w_2=2\eta Y_{i_1}$; $\mathbb E[g_2\mid S,i_1]=2(w_2-\bar Y)=L_S'(w_2)$; $\mathbb E[g_2\mid w_2]=2w_2-2y/m$, $y=Y_{i_1}$.
  - Độ chệch $-2y/m$: $\mp0{,}667$ khi $m=3$, $y=\pm1$.
  - (d) $Y_2$ độc lập với $w_2$, nên $\mathbb E[g_2\mid w_2]=2w_2=L_D'(w_2)$: cần tính độc lập đó.
- **Ghi chú diễn giả** (~150 âm tiết): Dòng dữ kiện gom thiết lập chung của phần (c) và (d). Ở (c), biết $w_2$ tương đương biết $y=Y_{i_1}$ vì $\eta>0$. Với xác suất $\tfrac1m$, chỉ số $i_2$ trùng $i_1$ và $Y_{i_2}=y$; với xác suất $1-\tfrac1m$, $Y_{i_2}$ độc lập với $Y_{i_1}$ và có kì vọng $0$; do đó $\mathbb E[Y_{i_2}\mid w_2]=y/m$. Khi $y=1$, bước tiếp theo bị kéo về phía nhãn đã dùng ở bước một. Độ chệch giảm theo $m$ nhưng khác $0$ với mọi $m$. Ở (d), giả thiết được dùng là Bước 1 của chứng minh Hệ quả 06.2; ở (c), giả thiết này hỏng vì $i_2$ có thể trùng $i_1$. Kiểm tra: với $m=3$, liệt kê $72$ trường hợp đồng khả năng cho $\mathbb E[g_2-2w_2\mid Y_{i_1}=1]=-\tfrac23$. Phần (a), (b) chứng minh hai khẳng định tổng quát của mạch. Nguồn: tệp bài tập, Bài tập 06.1 và lời giải.
- **Lý do / nối:** bài tập của cụm hai cách lấy mẫu, ghép chế độ A và chế độ B trên cùng phân bố → tiêu đề mạch 3.
- **Mục tiêu / nguồn:** 1; Bài tập 06.1(c), (d).

### Mạch 3. ERM có chính quy hóa (6 trang, 14 phút)

#### `3-00` 3. ERM có chính quy hóa — tiêu đề mạch, điểm vào mạch 3 · 0,5 phút
- **Mặt trang:** "3."; h2 "ERM có chính quy hóa"; `p.strand-lead` (bảng mạch, 17 âm tiết); `p.strand-keys`: "mục tiêu có chính quy hóa · lồi mạnh · tăng trưởng bậc hai · hồi quy ridge".
- **Ghi chú diễn giả:** Mạch 2 cần một thuật toán mà khoảng cách tổng quát hóa kì vọng nhỏ. Trên tập huấn luyện bốn quan sát, thay một quan sát làm nghiệm của tối thiểu hóa rủi ro thực nghiệm dịch gần một phần ba đường kính của tập tham số. Thêm một số hạng phạt chuẩn làm hàm mục tiêu lồi mạnh; khi đó nghiệm tồn tại, duy nhất, và hàm mục tiêu tăng ít nhất bậc hai quanh nghiệm. Ví dụ hồi quy ridge cho thấy khoảng cách giữa hai nghiệm giảm khi hệ số chính quy hóa tăng. Nguồn: ghi chú Bài 06, §6.
- **Lý do / nối:** mạch 2 → ví dụ mở đầu §6.
- **Mục tiêu / nguồn:** 4; §6.

#### `3-01` Ví dụ: một quan sát dịch nghiệm ERM — ví dụ, vấn đề (đoạn mở §6) · 2 phút
- **Mặt trang:**
  - Tập huấn luyện bốn quan sát, $W=[-1,1]$: nghiệm ERM $2{,}5/3{,}25\approx0{,}7692$.
  - Thay $z_4=(-1,-1)$ bằng $z'=(1,-1)$: $\sum_ix_iy_i$ giảm từ $2{,}5$ xuống $0{,}5$, $\sum_ix_i^2=3{,}25$ giữ nguyên.
  - Nghiệm ERM mới $0{,}5/3{,}25\approx0{,}1538$: dịch $0{,}6154$, khoảng $0{,}31$ lần đường kính $2$ của $W$.
  - Thêm vào $L_S$ một số hạng phạt chuẩn của $w$ làm nghiệm ít nhạy hơn.
- **Ghi chú diễn giả:** Trong một chiều, khi nghiệm nằm trong $W$, nghiệm ERM với hàm lỗi bình phương là $\sum_ix_iy_i/\sum_ix_i^2$. Thay quan sát thứ tư đổi tử số một lượng $2$ trong khi mẫu số giữ nguyên, vì $1^2=(-1)^2$. Với bốn quan sát, mỗi quan sát chiếm một phần tư rủi ro thực nghiệm, nên một quan sát đủ làm nghiệm dịch xa. Câu cuối dẫn sang định nghĩa: số hạng phạt chuẩn không phụ thuộc dữ liệu, nên không đổi khi thay một quan sát. Nguồn: ghi chú Bài 06, §6, đoạn mở; Ví dụ 06.1, Bước 4.
- **Lý do / nối:** khái niệm mở bằng ví dụ cụ thể, không mở bằng định nghĩa → định nghĩa.
- **Mục tiêu / nguồn:** 4; §6 đoạn mở.

#### `3-02` ERM có chính quy hóa — định nghĩa (Định nghĩa 06.6) · 2 phút
- **Mặt trang:**
  - **Định nghĩa 06.6.** $W$ khác rỗng, đóng, lồi; $s\in\mathcal Z^m$; hệ số chính quy hóa (regularization parameter) $\lambda>0$ chọn trước, không phụ thuộc $s$.
  - Mục tiêu có chính quy hóa (regularized objective); $\hat w_s\in W$ làm nhỏ nhất nó trên $W$:
  - $$F_{s,\lambda}(w)=L_s(w)+\tfrac\lambda2\lVert w\rVert^2.$$
  - ERM có chính quy hóa (regularized ERM): quy tắc $s\mapsto\hat w_s$; hàm lỗi bình phương: hồi quy ridge (ridge regression).
  - $\lambda=0$: nghiệm có thể không duy nhất; $x=(1,0)$, $y=1$, $W=\mathbb R^2$: mọi $w=(1,t)$ có $L_S(w)=0$.
- **Ghi chú diễn giả:** ERM có chính quy hóa còn gọi là chính quy hóa Tikhonov (Tikhonov regularization). Hệ số $\lambda$ cố định, còn $\hat w_S$ ngẫu nhiên theo tập huấn luyện. Khi cần ghi $\lambda$, viết $\hat w_{s,\lambda}$. Với $\lambda=0$, quy tắc là tối thiểu hóa rủi ro thực nghiệm trên $W$ của Bài 01. Ví dụ ở dòng cuối có $p=2$ và một quan sát: mọi điểm trên đường thẳng $w_1=1$ đều khớp hoàn toàn. Hai tính chất của $F_{s,\lambda}$ được dùng về sau: nó lồi mạnh, và nó tăng ít nhất bậc hai quanh điểm cực tiểu. Nguồn: ghi chú Bài 06, §6, Định nghĩa 06.6 và ba đoạn sau.
- **Lý do / nối:** câu cuối của 3-01 dẫn vào định nghĩa → hai tính chất của mục tiêu.
- **Mục tiêu / nguồn:** 4; Định nghĩa 06.6.

#### `3-03` Tăng trưởng bậc hai và nghiệm duy nhất — trực quan, kết quả (Bổ đề 06.7, 06.8) · 3 phút
- **Mặt trang:**
  - **Trực quan.** Tại cực tiểu, $f$ không giảm bậc nhất theo hướng vào $W$; độ cong thêm $\tfrac\lambda2\lVert w-u\rVert^2$.
  - **Bổ đề 06.7.** **Giả thiết:** $f$ $\lambda$-lồi mạnh, $\lambda>0$; $W$ lồi, khác rỗng; $f(u)=\min_Wf$, $u\in W$.
  - **Bảo đảm:** tất định, với mọi $w\in W$: $$f(w)-f(u)\ge\tfrac\lambda2\lVert w-u\rVert^2.$$
  - **Bổ đề 06.8.** **Giả thiết:** như Định nghĩa 06.6, $\ell(\cdot,z)$ lồi.
  - **Bảo đảm:** tất định: $F_{s,\lambda}$ $\lambda$-lồi mạnh, cực tiểu duy nhất $\hat w_s$ trên $W$, tăng trưởng bậc hai (quadratic growth) quanh $\hat w_s$.
- **Ghi chú diễn giả:** Lộ trình Bổ đề 06.7: so $f(u)$ với $f$ tại $u+\alpha(w-u)$, thuộc $W$ vì $W$ lồi; dùng định nghĩa lồi mạnh, chuyển vế, chia cho $\alpha$ rồi cho $\alpha\to0^+$. Bổ đề 06.8 (phác thảo): phần (a) cộng bất đẳng thức lồi của $L_s$ với đẳng thức của $\tfrac\lambda2\lVert\cdot\rVert^2$; phần (b) dùng $F_{s,\lambda}\to\infty$ khi $\lVert w\rVert\to\infty$ và tính compact (Phụ lục A); phần (c) là Bổ đề 06.7, cho cả tính duy nhất. Với $\lambda=0$, giá trị nhỏ nhất có thể không đạt, chẳng hạn hàm lỗi logistic trên một tập huấn luyện tách được bởi một siêu phẳng qua gốc. Nguồn: ghi chú Bài 06, §6, Bổ đề 06.7, 06.8 và chứng minh; Phụ lục A; UML §13.3.
- **Lý do / nối:** hai công cụ cho Mệnh đề 06.11, chung một trang; tính duy nhất làm $\hat w_S$ là đầu ra xác định của một thuật toán → ví dụ ridge.
- **Mục tiêu / nguồn:** 4; Bổ đề 06.7, 06.8.

#### `3-04` Ví dụ: hồi quy ridge khi thay một quan sát — ví dụ (Ví dụ 06.4), Hình 06.1 · 3,5 phút
- **Mặt trang** {{`grid2`: trái chữ và bảng, phải Hình 06.1}}:
  - $F_{S,\lambda}(w)=\tfrac\lambda2w^2+\tfrac14(3{,}25w^2-5w+3)$; $S^{(4)}$ thay $z_4=(-1,-1)$ bằng $z'=(1,-1)$: số hạng $-5w$ thành $-w$.
  - $\hat w_S=2{,}5/(3{,}25+2\lambda)$, $\hat w_{S^{(4)}}=0{,}5/(3{,}25+2\lambda)$.
  - | $\lambda$ | $\hat w_S$ | $\hat w_{S^{(4)}}$ | $\lvert\hat w_S-\hat w_{S^{(4)}}\rvert$ | $L_S(\hat w_S)$ |
    |---|---|---|---|---|
    | $0$ | $0{,}7692$ | $0{,}1538$ | $0{,}6154$ | $0{,}2692$ |
    | $1$ | $0{,}4762$ | $0{,}0952$ | $0{,}3810$ | $0{,}3390$ |
    | $4$ | $0{,}2222$ | $0{,}0444$ | $0{,}1778$ | $0{,}5123$ |
  - {{Hình 06.1: `img/lec-06/ridge-thay-mot-quan-sat.svg`, `figcaption` theo chú thích của ghi chú}}
  - **Diễn giải:** $\lambda$ từ $0$ lên $4$: khoảng cách giảm từ $0{,}6154$ xuống $0{,}1778$, $L_S(\hat w_S)$ tăng từ $0{,}2692$ lên $0{,}5123$.
- **Ghi chú diễn giả:** Mỗi mục tiêu là đa thức bậc hai có hệ số dẫn dương, và cả hai điểm thuộc $W$, nên chúng là các nghiệm trên $W$, duy nhất khi $\lambda>0$. Công thức chung trong một chiều là $\hat w=\sum_ix_iy_i/(\sum_ix_i^2+\lambda m/2)$ khi giá trị này thuộc $W$. Trên hình, số hạng $\tfrac\lambda2w^2$ làm hai đường cong cong hơn, còn hiệu của chúng vẫn là cùng một hàm bậc nhất $F_{S,\lambda}(w)-F_{S^{(4)},\lambda}(w)=-w$, không phụ thuộc $\lambda$; hai điểm cực tiểu vì vậy gần nhau hơn. Cột cuối cho thấy cái giá: nghiệm khớp tập huấn luyện kém hơn. Hai khung của hình dùng thang tung khác nhau. Nguồn: ghi chú Bài 06, Ví dụ 06.4, Hình 06.1.
- **Lý do / nối:** trọng tâm trực quan 4 (ví dụ ridge thay một quan sát, dùng lại SVG của ghi chú); bảng và hình chung trang → bài tập về tính lồi mạnh.
- **Mục tiêu / nguồn:** 4, 5; Ví dụ 06.4, Hình 06.1.

#### `3-05` Bài tập: dạng bậc nhất của tính lồi mạnh — bài tập (Bài tập 06.10(a), (c)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - $f:\mathbb R^p\to\mathbb R$ là $\lambda$-lồi mạnh, $w\in\mathbb R^p$, $v\in\partial f(w)$. (a) Chứng minh rằng với mọi $u\in\mathbb R^p$:
  - $$\langle w-u,v\rangle\ge f(w)-f(u)+\tfrac\lambda2\lVert w-u\rVert^2.$$
  - (c) Kiểm tra (a) với $f(w)=w^2$ ($\lambda=2$) tại $w=1$, $u=0$; và với $f(w)=\lvert w\rvert+w^2$ ($\lambda=2$) tại $w=0$, $v=\tfrac12$, $u=1$.
  - **Lời giải:** (a) $w_\alpha=w+\alpha(u-w)$, $\alpha\in(0,1]$: lồi mạnh chặn $f(w_\alpha)$ từ trên, bất đẳng thức dưới gradient tại $w$ từ dưới.
  - Trừ $f(w)$, chia cho $\alpha$, cho $\alpha\to0^+$, đổi dấu.
  - (c) $f(w)=w^2$: vế trái $2$, vế phải $1-0+1=2$, dấu bằng. $f(w)=\lvert w\rvert+w^2$: $-\tfrac12\ge0-2+1=-1$.
- **Ghi chú diễn giả** (~130 âm tiết): Bài tập chọn từ UML (Bài tập 14.1) và dùng đúng kỹ thuật của chứng minh Bổ đề 06.7: một điểm trên đoạn thẳng, rồi cho điểm đó dần về đầu mút. Ở (a), Bước 1 là định nghĩa lồi mạnh với cặp $(u,w)$ và trọng số $\alpha$; Bước 2 là $f(w_\alpha)\ge f(w)+\alpha\langle v,u-w\rangle$. Ghép hai bước cho $\langle v,u-w\rangle\le f(u)-f(w)-\tfrac\lambda2(1-\alpha)\lVert u-w\rVert^2$; cho $\alpha\to0^+$ rồi đổi dấu. Ở (c), hàm thứ hai là tổng của hàm lồi $\lvert w\rvert$ và hàm $2$-lồi mạnh $w^2$, nên $2$-lồi mạnh; $\partial f(0)=[-1,1]$ chứa $\tfrac12$. Phần (b) suy ra Bổ đề 06.7 khi $W=\mathbb R^p$. Nguồn: tệp bài tập, Bài tập 06.10 và lời giải; UML §14.8.
- **Lý do / nối:** bài tập của cụm chính quy hóa, cùng kỹ thuật với Bổ đề 06.7 (mục 11, điểm 4) → tiêu đề mạch 4.
- **Mục tiêu / nguồn:** 4; Bài tập 06.10.

### Mạch 4. Tính ổn định và khoảng cách tổng quát hóa kì vọng (8 trang, 22 phút)

#### `4-00` 4. Tính ổn định và khoảng cách tổng quát hóa kì vọng — tiêu đề mạch, điểm vào mạch 4 · 0,5 phút
- **Mặt trang:** "4."; h2 "Tính ổn định và khoảng cách tổng quát hóa kì vọng"; `p.strand-lead` (bảng mạch, 19 âm tiết); `p.strand-keys`: "tập huấn luyện lân cận · ổn định đều · hệ số ổn định · lập luận đổi vai".
- **Ghi chú diễn giả:** Mệnh đề 06.5 cần một cận cho khoảng cách tổng quát hóa kì vọng của một thuật toán. Mạch này cho cận đó từ một tính chất của chính thuật toán: khi thay một quan sát của tập huấn luyện, hàm lỗi của đầu ra tại mọi điểm thay đổi ít. Cận không dùng cấu trúc của lớp giả thuyết và không cần hàm lỗi bị chặn. Công cụ là lập luận đổi vai giữa một quan sát huấn luyện và một quan sát mới. Nguồn: ghi chú Bài 06, §7, đoạn mở.
- **Lý do / nối:** mạch 3 → định nghĩa ổn định.
- **Mục tiêu / nguồn:** 3; §7.

#### `4-01` Tập huấn luyện lân cận và tính ổn định đều — ví dụ, định nghĩa (Định nghĩa 06.9) · 3 phút
- **Mặt trang:**
  - Bốn quan sát, $\lambda=0$: thay $z_4$ bằng $z'=(1,-1)$, hàm lỗi tại $z=(1,-1)$ đổi $304/169\approx1{,}7988$.
  - **Định nghĩa 06.9.** Tập huấn luyện lân cận (neighboring samples) $s$, $s^{(i)}$: thay $z_i$ bằng quan sát thay thế (replacement observation) $z'$.
  - $A$ ổn định đều (uniformly stable), hệ số ổn định (stability coefficient) $\epsilon_{\mathrm{stab}}(m)$, nếu với mọi $s$, $i$, $z'$, quan sát kiểm tra (test observation) $z$:
  - $$\big\lvert\mathbb E_\xi\ell(A(s;\xi),z)-\mathbb E_\xi\ell(A(s^{(i)};\xi),z)\big\rvert\le\epsilon_{\mathrm{stab}}(m).$$
  - Mọi $s\in\mathcal Z^m$, kể cả tập có xác suất $0$ dưới $D$.
- **Ghi chú diễn giả:** Hai kì vọng hữu hạn và lấy theo cùng $P_\xi$, cho hai lần chạy riêng; với thuật toán tất định, bỏ $\mathbb E_\xi$. Với tập huấn luyện ngẫu nhiên, ta viết $S^{(i)}$ và $Z'$. Ở dòng đầu, hai nghiệm là $10/13$ và $2/13$, và hàm lỗi tại $(1,-1)$ đổi từ $(15/13)^2$ lên $(23/13)^2$; trên $\mathcal Z=[-1,1]^2$, đây là thay đổi lớn nhất. Với $\lambda=0$, hệ số này không giảm theo $m$. Thuật toán ghi nhớ: lấy một tập huấn luyện có $z_i=(x_i,1)$ với $x_i$ xuất hiện đúng một lần, rồi thay $z_i$ bằng một quan sát tại điểm khác; dự đoán tại $x_i$ đổi từ $1$ sang $0$, nên hàm lỗi tại $(x_i,1)$ đổi từ $0$ sang $1$. Nguồn: ghi chú Bài 06, §7, Định nghĩa 06.9 và ba đoạn sau.
- **Lý do / nối:** khái niệm mở bằng ví dụ bằng số của mạch 3; câu "với mọi" trên mặt trang vì lượng từ là điểm dễ nhầm → trực quan đổi vai.
- **Mục tiêu / nguồn:** 3; Định nghĩa 06.9.

#### `4-02` Đổi vai quan sát huấn luyện và quan sát mới — trực quan, ví dụ, hình F3 · 3 phút
- **Mặt trang** {{`grid2`: trái chữ, phải hình F3}}:
  - **Trực quan.** $L_D(A(S;\xi))$: hàm lỗi trên một quan sát mới $Z'$; $L_S(A(S;\xi))$: trung bình hàm lỗi trên các $Z_i$ đã thấy.
  - Đổi vai $Z_i$ với $Z'$: với $A(S^{(i)};\xi)$, $Z_i$ là quan sát chưa thấy. Do đó
  - $$\mathbb E[L_D(A(S;\xi))-L_S(A(S;\xi))]=\frac1m\sum_{i=1}^m\mathbb E\big[\ell(A(S^{(i)};\xi),Z_i)-\ell(A(S;\xi),Z_i)\big].$$
  - Mỗi số hạng: hàm lỗi tại $Z_i$ khi bỏ $Z_i$ trừ khi giữ $Z_i$; không quá $\epsilon_{\mathrm{stab}}(m)$.
  - **Ví dụ.** Thuật toán ghi nhớ, hàm lỗi 0–1 (Ví dụ 01.8): $\mathbb E[L_D-L_S]=\epsilon_{\mathrm{stab}}=1$; $h$ cố định: cả hai bằng $0$.
- **Ghi chú diễn giả:** Đẳng thức suy ra từ Bước 1–3 của chứng minh Định lý 06.10. Vế phải không còn rủi ro kì vọng nào: chỉ có hàm lỗi trên các quan sát và một quan sát thay thế. Thuật toán ghi nhớ đạt đúng hệ số của nó: hàm lỗi tại $Z_i$ là $0$ khi giữ $Z_i$ và là $1$ khi thay $Z_i$ bằng một điểm khác. Ở đó cận đạt được nhưng không cho thông tin, vì khoảng cách bằng $1$. Hình: hai hàng, tập huấn luyện $S$ với quan sát kiểm tra $Z'$, và $S^{(i)}$ với quan sát kiểm tra $Z_i$. Nguồn: ghi chú Bài 06, §7, đoạn trước Định lý 06.10, đoạn sau chứng minh; UML §13.2.
- **Lý do / nối:** trọng tâm trực quan 2 của deck, trước phát biểu; ví dụ thuật toán ghi nhớ không cần định lý (tiền lệ T5 cổng Bài 04) → phát biểu.
- **Mục tiêu / nguồn:** 3; §7.

#### `4-03` Tính ổn định chặn khoảng cách tổng quát hóa kì vọng — kết quả (Định lý 06.10) · 3 phút
- **Mặt trang:**
  - **Định lý 06.10.** **Giả thiết:** $S\sim D^m$ theo (T1) dạng đầy đủ; $\xi$ độc lập với $S$;
  - $A$ có nguồn ngẫu nhiên riêng, ổn định đều với hệ số $\epsilon_{\mathrm{stab}}(m)$; $\ell$ thỏa (T2), không cần bị chặn; $\mathbb E_{S,\xi}L_D(A(S;\xi))<\infty$.
  - **Bảo đảm:** theo kì vọng theo $(S,\xi)$:
  - $$\big\lvert\mathbb E_{S,\xi}[L_D(A(S;\xi))-L_S(A(S;\xi))]\big\rvert\le\epsilon_{\mathrm{stab}}(m).$$
  - Cấp thuật toán (algorithm-level): phụ thuộc $m$ chỉ qua $\epsilon_{\mathrm{stab}}(m)$, bất kể kích thước của lớp giả thuyết.
- **Ghi chú diễn giả:** Bảo đảm chặn trị tuyệt đối của kì vọng, không chặn kì vọng của trị tuyệt đối; ví dụ thuật toán hằng của mạch này tách hai đại lượng. Giả thiết khả tích và tính ổn định đều kéo theo $\mathbb EL_S(A(S;\xi))<\infty$. Để chặn $L_D$ của đầu ra, cần cộng thêm sai số tối ưu thực nghiệm như Mệnh đề 06.5. Hai giả thiết dễ bỏ sót là dạng đầy đủ của (T1) và tính độc lập của $\xi$ với $S$. Nguồn: ghi chú Bài 06, §7, Định lý 06.10 và đoạn sau, câu sau $\square$.
- **Lý do / nối:** kết quả chính của mạch; trang ý tưởng chứng minh riêng ở sau.
- **Mục tiêu / nguồn:** 3; Định lý 06.10.

#### `4-04` Ý tưởng chứng minh: Định lý 06.10 — ý tưởng chứng minh · 4 phút
- **Mặt trang:**
  - Thêm $Z'\sim D$ độc lập với $(S,\xi)$; $S^{(i)}$: thay $Z_i$ bằng $Z'$.
  - **Bước 1 ($Z'$ độc lập; Fubini).** $\mathbb E\,\ell(A(S;\xi),Z')=\mathbb EL_D(A(S;\xi))$.
  - **Bước 2 ((T1) dạng đầy đủ).** Đổi chỗ $Z_i$, $Z'$ giữ phân bố liên hợp: $\mathbb E\,\ell(A(S;\xi),Z')=\mathbb E\,\ell(A(S^{(i)};\xi),Z_i)$.
  - **Bước 3.** $\mathbb EL_S(A(S;\xi))=\frac1m\sum_i\mathbb E\,\ell(A(S;\xi),Z_i)$, hữu hạn nhờ ổn định đều.
  - **Bước 4 (ổn định đều).** Cố định $(S,Z')$, lấy kì vọng theo $\xi$: mỗi hiệu $\le\epsilon_{\mathrm{stab}}(m)$; trung bình theo $i$.
  - Các $Z_i$ là bản sao của nhau: Bước 2 hỏng.
- **Ghi chú diễn giả** (~200 âm tiết): Lộ trình: thêm một quan sát mới, đổi vai nó với $Z_i$, so hai đầu ra trên hai tập huấn luyện lân cận, rồi lấy trung bình theo $i$. Bước 1 đổi rủi ro kì vọng thành hàm lỗi trên một quan sát; định lý Fubini cho hàm không âm cho phép lấy kì vọng theo $Z'$ trước vì $Z'$ độc lập với $(S,\xi)$. Bước 2 là chỗ duy nhất dùng dạng đầy đủ của (T1): phép đổi chỗ biến cặp $(S,Z')$ thành $(S^{(i)},Z_i)$ và giữ phân bố. Tính hữu hạn của $\mathbb E\,\ell(A(S;\xi),Z_i)$ cũng cần tính ổn định đều: nó không quá $\mathbb EL_D(A(S;\xi))+\epsilon_{\mathrm{stab}}(m)$. Ở Bước 4, $\xi$ độc lập với $(S,Z')$ nên định lý Fubini cho phép cố định $S=s$, $Z'=z'$ rồi áp dụng Định nghĩa 06.9 với quan sát kiểm tra $z=z_i$. Khi các quan sát là bản sao của nhau, mỗi $Z_i$ vẫn có phân bố $D$ nhưng phép đổi chỗ đổi phân bố: Bài tập 06.2(c) với thuật toán trung bình cho khoảng cách $0{,}5$, lớn hơn hệ số ổn định $7/16$ khi $m=4$. Nguồn: ghi chú Bài 06, chứng minh Định lý 06.10; tệp bài tập, Bài tập 06.2(c); UML §13.2.
- **Lý do / nối:** trang ý tưởng chứng minh riêng, chỗ dùng từng giả thiết → kỹ thuật.
- **Mục tiêu / nguồn:** 3; chứng minh Định lý 06.10.

#### `4-05` Lập luận đổi vai — kỹ thuật (lần đầu trong học phần) · 3 phút
- **Mặt trang:**
  - **Kỹ thuật.** Lập luận đổi vai (exchange argument): $Z_1,\ldots,Z_m,Z'$ độc lập cùng phân bố, $\phi\ge0$ đo được và mọi $i$:
  - $$\mathbb E\,\phi(S,Z')=\mathbb E\,\phi(S^{(i)},Z_i).$$
  - Dùng khi so hàm lỗi trên điểm chưa thấy với trên điểm đã dùng.
  - Cần (T1) dạng đầy đủ. Dùng ở Định lý 06.10, Bài tập 06.2, 06.9.
  - **Nhắc lại:** tập mẫu ảo (Bài 03) thêm $m$ quan sát; ở đây chỉ thêm $Z'$.
- **Ghi chú diễn giả:** Với $\phi(s,z)=\ell(A(s;\xi),z)$ lấy kì vọng theo $\xi$ trước, kỹ thuật cho Bước 2 của chứng minh định lý. Trung bình theo $i$ rồi trừ rủi ro thực nghiệm cho đẳng thức thay một: khoảng cách tổng quát hóa kì vọng bằng đúng trung bình của các hiệu hàm lỗi trên hai tập huấn luyện lân cận. UML trình bày đẳng thức này cho thuật toán tất định và dùng một dạng ổn định yếu hơn, ổn định thay một theo trung bình (on-average-replace-one stability, Phụ lục E). Kỹ thuật dùng ở Bài tập 06.2 và 06.9, và trở lại khi chặn khoảng cách tổng quát hóa kì vọng của hạ gradient ngẫu nhiên nhiều vòng bằng tính ổn định của hai lần chạy ghép cặp. Nguồn: ghi chú Bài 06, §7, đoạn trước Định lý 06.10, Bước 2 của chứng minh; Phụ lục E; §12, đoạn cuối.
- **Lý do / nối:** kỹ thuật dùng lại qua học phần, trang riêng ở nơi dùng lần đầu (yêu cầu của điều phối viên) → ví dụ thuật toán hằng.
- **Mục tiêu / nguồn:** 3; §7.

#### `4-06` Ví dụ: thuật toán hằng — ví dụ (Ví dụ 06.5) · 2,5 phút
- **Mặt trang:**
  - Thuật toán hằng (constant algorithm) trả về $h_0\equiv0$ với mọi tập huấn luyện; $X\sim U[0,1]$, $Y=\mathbb 1[X>\tfrac12]$, hàm lỗi 0–1.
  - Đầu ra không phụ thuộc tập huấn luyện: $\epsilon_{\mathrm{stab}}=0$, nên khoảng cách tổng quát hóa kì vọng bằng $0$ (Định lý 06.10).
  - $L_D(h_0)=\tfrac12$, còn hàm phân lớp $\mathbb 1[x>\tfrac12]$ có rủi ro $0$.
  - $\mathbb E\lvert L_S(h_0)-\tfrac12\rvert=2^{-m}\sum_k\binom mk\lvert\tfrac km-\tfrac12\rvert$: $0{,}1230$; $0{,}0398$; $0{,}0126$ với $m=10$; $100$; $1000$.
  - **Kết luận:** tính ổn định không kéo theo rủi ro thấp; $\lvert\mathbb E[L_D-L_S]\rvert=0$, còn $\mathbb E\lvert L_D-L_S\rvert>0$ với mọi $m$.
- **Ghi chú diễn giả:** Hàm lỗi $\ell(h_0,Z)=Y$ có phân bố Bernoulli với tham số $\tfrac12$, nên $mL_S(h_0)$ có phân bố nhị thức với tham số $(m,\tfrac12)$. Ví dụ tách hai điều: ổn định chỉ chặn phần khoảng cách, còn rủi ro thực nghiệm của đầu ra có thể lớn; và Định lý 06.10 chỉ chặn trị tuyệt đối của kì vọng. Mạch 6 cân hai phần này bằng hệ số chính quy hóa. Nguồn: ghi chú Bài 06, Ví dụ 06.5.
- **Lý do / nối:** kiểm sau phát biểu; giới hạn "theo kì vọng" của §10 → bài tập.
- **Mục tiêu / nguồn:** 3; Ví dụ 06.5.

#### `4-07` Bài tập: thuật toán trung bình trên hai điểm — bài tập (Bài tập 06.2(b)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - $\mathcal Z=\{0,1\}$, $D(0)=D(1)=\tfrac12$, $\ell(w,z)=(w-z)^2$ với $w\in[0,1]$, $A(s)=\bar z=\tfrac1m\sum_iz_i$.
  - (b1) $m=2$: liệt kê bốn tập huấn luyện, tính $\mathbb EL_D(A(S))$, $\mathbb EL_S(A(S))$, khoảng cách tổng quát hóa kì vọng và trung bình thay một $\tfrac1m\sum_i\mathbb E[\ell(A(S^{(i)}),Z_i)-\ell(A(S),Z_i)]$.
  - (b2) Chứng minh hệ số ổn định đều nhỏ nhất là $2/m-1/m^2$; so với cận $2/m$ từ tính $2$-Lipschitz của $\ell(\cdot,z)$ trên $[0,1]$.
  - **Lời giải:** (b1) $\bar z=0;\tfrac12;\tfrac12;1$: $L_D=\tfrac12;\tfrac14;\tfrac14;\tfrac12$, $L_S=0;\tfrac14;\tfrac14;0$; $0{,}375-0{,}125=0{,}25$; trung bình thay một $0{,}375-0{,}125=0{,}25$.
  - (b2) $\lvert a-b\rvert\le\tfrac1m$, $a+b\in[\tfrac1m,2-\tfrac1m]$: hiệu $\le\tfrac1m(2-\tfrac1m)$, đạt tại $s=(0,\ldots,0)$, $z'=z=1$; $m=2$: $0{,}75<1$, và $0{,}25\le0{,}75$.
- **Ghi chú diễn giả** (~150 âm tiết): Ở (b1), rủi ro kì vọng là $L_D(w)=\tfrac12w^2+\tfrac12(1-w)^2$; bốn tập huấn luyện có cùng xác suất $\tfrac14$. Khoảng cách $0{,}25$ bằng $2\sigma^2/m$ với $\sigma^2=\tfrac14$. Trung bình thay một: với $i=1$, ba biến $Z'$, $Z_2$, $Z_1$ độc lập, nên $\mathbb E[(\tfrac{Z'+Z_2}2-Z_1)^2]=\tfrac18+\tfrac14=0{,}375$ và $\mathbb E\,\ell(A(S),Z_1)=\tfrac14\mathbb E(Z_2-Z_1)^2=0{,}125$. Hai số bằng nhau đúng như đẳng thức thay một. Ở (b2), $a$, $b$ là trung bình trên $s$ và $s^{(i)}$, và $(a-z)^2-(b-z)^2=(a-b)(a+b-2z)$. Định lý 06.10 cho $0{,}25\le0{,}75$; cận Lipschitz $2/m$ bằng $1$. Phần (c) bỏ dạng đầy đủ của (T1) và cho thấy kết luận của định lý sai khi $m\ge4$. Nguồn: tệp bài tập, Bài tập 06.2 và lời giải.
- **Lý do / nối:** bài tập của cụm ổn định, kiểm cả đẳng thức thay một và định lý trên một thuật toán liệt kê được → tiêu đề mạch 5.
- **Mục tiêu / nguồn:** 3; Bài tập 06.2(b).

### Mạch 5. Tính ổn định của ERM có chính quy hóa (6 trang, 16 phút)

#### `5-00` 5. Tính ổn định của ERM có chính quy hóa — tiêu đề mạch, điểm vào mạch 5 · 0,5 phút
- **Mặt trang:** "5."; h2 "Tính ổn định của ERM có chính quy hóa"; `p.strand-lead` (bảng mạch, 23 âm tiết); `p.strand-keys`: "ổn định đều · hai tập huấn luyện lân cận · tính Lipschitz · dữ liệu bị chặn".
- **Ghi chú diễn giả:** Định lý 06.10 cần một thuật toán có hệ số ổn định nhỏ. Trong ví dụ ridge, khoảng cách giữa hai nghiệm giảm từ $0{,}6154$ xuống $0{,}1778$ khi $\lambda$ tăng từ $0$ lên $4$. Mạch này chặn khoảng cách đó cho mọi tập huấn luyện, mọi cách thay một quan sát và mọi hàm lỗi lồi, Lipschitz trên tập tham số, rồi dựng hai phản ví dụ khi bỏ chính quy hóa hoặc bỏ tính bị chặn của dữ liệu. Nguồn: ghi chú Bài 06, §8, đoạn mở.
- **Lý do / nối:** mạch 4 → mệnh đề chính của §8.
- **Mục tiêu / nguồn:** 4, 5; §8.

#### `5-01` Hai nghiệm có chính quy hóa khi thay một quan sát — trực quan, kết quả (Mệnh đề 06.11) · 3 phút
- **Mặt trang:**
  - **Nhắc lại:** (L): $\lvert\ell(w,z)-\ell(w',z)\rvert\le G\lVert w-w'\rVert$ với mọi $w,w'\in W$, $z\in\mathcal Z$.
  - **Trực quan.** $F_{s,\lambda}-F_{s^{(i)},\lambda}=\tfrac1m[\ell(\cdot,z_i)-\ell(\cdot,z')]$ là $(2G/m)$-Lipschitz; độ cong $\lambda$ giữ cực tiểu dịch cỡ $(2G/m)/\lambda$.
  - **Mệnh đề 06.11.** **Giả thiết:** $W$ khác rỗng, đóng, lồi; $\ell(\cdot,z)$ lồi, không âm trên $W$, (L) với $G$; $\lambda>0$; $s$, $i$, $z'$ bất kì.
  - **Bảo đảm:** tất định, không cần $D$: (a) $\lVert\hat w_s-\hat w_{s^{(i)}}\rVert\le\dfrac{2G}{\lambda m}$; (b) với mọi $z$, $\lvert\ell(\hat w_s,z)-\ell(\hat w_{s^{(i)}},z)\rvert\le\dfrac{2G^2}{\lambda m}$.
  - Tức ERM có chính quy hóa ổn định đều với $\epsilon_{\mathrm{stab}}(m)=2G^2/(\lambda m)$.
- **Ghi chú diễn giả:** Mỗi quan sát chỉ chiếm trọng số $1/m$ trong mục tiêu, còn số hạng chính quy hóa giữ độ cong $\lambda$ cố định; vì vậy cận giảm như $1/(\lambda m)$: gấp đôi $\lambda$ hoặc gấp đôi $m$ thì cận giảm một nửa. Hiệu hai mục tiêu không chứa số hạng chính quy hóa và $m-1$ số hạng chung. Với hàm lỗi bình phương, $G=2(BC_x+C_y)C_x$ phụ thuộc bán kính $B$ của $W$; khi $W=\mathbb R^p$ cần thêm một cận cho chuẩn của nghiệm (Bài tập 06.5). Nhận xét 06.12 (đọc thêm) cho một cận một phía cho hàm lỗi trơn và không âm, không cần (L). Nguồn: ghi chú Bài 06, §8, Mệnh đề 06.11 và đoạn sau; câu sau $\square$; Phụ lục B, Bước 3.
- **Lý do / nối:** trọng tâm trực quan 3 của deck, trên cùng trang phát biểu → ý tưởng chứng minh.
- **Mục tiêu / nguồn:** 4; Mệnh đề 06.11.

#### `5-02` Ý tưởng chứng minh: Mệnh đề 06.11 — ý tưởng chứng minh · 3,5 phút
- **Mặt trang:**
  - **Bước 1 (Bổ đề 06.8(c); $\ell$, $W$ lồi, $\lambda>0$).** Với $\hat w=\hat w_s$, $\hat w'=\hat w_{s^{(i)}}$: tăng trưởng bậc hai của $F_{s,\lambda}$ tại $\hat w'$, của $F_{s^{(i)},\lambda}$ tại $\hat w$.
  - **Bước 2.** Cộng lại; số hạng chính quy hóa và $m-1$ số hạng chung triệt tiêu:
  - $$\lambda\lVert\hat w-\hat w'\rVert^2\le\tfrac1m[\ell(\hat w',z_i)-\ell(\hat w,z_i)]+\tfrac1m[\ell(\hat w,z')-\ell(\hat w',z')].$$
  - **Bước 3 ((L) với $z_i$, $z'$).** Vế phải $\le2G\lVert\hat w-\hat w'\rVert/m$: được (a). **Bước 4 ((L) với $z$).** Được (b).
  - **Kỹ thuật.** Cộng hai bất đẳng thức tăng trưởng bậc hai đối xứng; dùng một: $4G/(\lambda m)$.
- **Ghi chú diễn giả** (~200 âm tiết): Bất đẳng thức then chốt là tổng của hai bất đẳng thức tăng trưởng bậc hai, mỗi cái có vế phải $\tfrac\lambda2\lVert\hat w-\hat w'\rVert^2$. Hai mục tiêu chỉ khác nhau ở quan sát thứ $i$: $F_{s,\lambda}-F_{s^{(i)},\lambda}=\tfrac1m[\ell(\cdot,z_i)-\ell(\cdot,z')]$, nên khi cộng, mọi thứ còn lại triệt tiêu. Ở Bước 3, nếu $\hat w\ne\hat w'$ thì chia hai vế cho $\lambda\lVert\hat w-\hat w'\rVert$; nếu bằng nhau thì vế trái của (a) bằng $0$. Lập luận một phía (Phụ lục B) chỉ dùng tăng trưởng bậc hai của $F_{s,\lambda}$ và tính tối ưu $F_{s^{(i)},\lambda}(\hat w')\le F_{s^{(i)},\lambda}(\hat w)$; vế trái chỉ còn $\tfrac\lambda2$ nên hằng số gấp đôi, đúng hằng số của UML. Bỏ $\lambda>0$: Bước 1 chỉ còn độ cong của chính $L_S$, có thể không giảm theo $m$. Bỏ dữ liệu bị chặn với hàm lỗi bình phương: không có $G$ hữu hạn, Bước 3 không dùng được. Ví dụ 06.7 và 06.9 dựng hai trường hợp này. (L) chỉ dùng tại các điểm của $W$, nên khi $W=\mathbb R^p$ cần $\ell(\cdot,z)$ Lipschitz trên cả không gian, như hàm lỗi logistic hay bản lề. Nguồn: ghi chú Bài 06, chứng minh Mệnh đề 06.11; Phụ lục B; UML §13.3.1.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; kỹ thuật một dòng (chỉ dùng trong chứng minh này) → kiểm bằng số.
- **Mục tiêu / nguồn:** 4; chứng minh Mệnh đề 06.11, Phụ lục B.

#### `5-03` Ví dụ: kiểm tra và độ chặt của cận ổn định — ví dụ (Ví dụ 06.6, 06.8), danh sách một cột (deck) · 2,5 phút
- **Mặt trang** {{hai thẻ `grid2`}}:
  - {{thẻ trái}} **Ví dụ 06.6.** Bốn quan sát, $G=4$, $m=4$: $2G/(\lambda m)=2/\lambda$, $2G^2/(\lambda m)=8/\lambda$; $\lambda=1$: $2$, $8$; $\lambda=4$: $0{,}5$, $2$.
  - $\lambda=1$, $\hat w=10/21$, $\hat w'=2/21$: $\lambda\lVert\hat w-\hat w'\rVert^2\approx0{,}1451\le0{,}3810\le2G\lVert\hat w-\hat w'\rVert/m\approx0{,}7619$.
  - Khoảng cách thật $0{,}3810\le2$ và $0{,}1778\le0{,}5$: cận lỏng khoảng $5$ lần khi $\lambda=1$.
  - {{thẻ phải}} **Ví dụ 06.8.** $\ell(w,z)=10-zw$, $z=\pm1$ đều, $W=[-10,10]$, $G=1$, $\lambda=0{,}1$, $m=100$: $\hat w_S=\bar z/\lambda$.
  - Thay một $z_i=1$ bằng $-1$: hai nghiệm cách đúng $2/(\lambda m)=0{,}2$; khoảng cách tổng quát hóa kì vọng $0{,}1$, cận $0{,}2$.
- **Ghi chú diễn giả:** Ở thẻ trái, số giữa $0{,}3810$ là vế phải của Bước 2 trong chứng minh: hai hiệu hàm lỗi $240/441$ và $432/441$ chia cho $m=4$. Bất đẳng thức đầu lỏng vì $L_S$ tự nó đã lồi mạnh, còn chứng minh chỉ dùng độ cong $\lambda$. Ở thẻ phải, hàm lỗi tuyến tính không âm trên $W$ và $1$-Lipschitz; $\bar z=\tfrac1m\sum_iz_i$ giảm $2/m$ khi thay một quan sát, nên cận (a) không cải thiện được. Khoảng cách tổng quát hóa kì vọng bằng $\mathbb E\bar z^2/\lambda=1/(\lambda m)$, bằng nửa cận $2G^2/(\lambda m)$ của Định lý 06.10 với Mệnh đề 06.11. Nguồn: ghi chú Bài 06, Ví dụ 06.6, 06.8.
- **Lý do / nối:** kiểm bằng số và độ chặt của cận, hai ví dụ của ghi chú chung trang → bỏ giả thiết.
- **Mục tiêu / nguồn:** 4; Ví dụ 06.6, 06.8.

#### `5-04` Ví dụ: bỏ chính quy hóa hoặc bỏ dữ liệu bị chặn — ví dụ (Ví dụ 06.7, 06.9), phản ví dụ, hai thẻ · 3,5 phút
- **Mặt trang** {{hai thẻ `grid2`}}:
  - {{thẻ trái}} **Ví dụ 06.7.** $m-1$ bản sao $(0,0)$ và $z_m=(1,1)$; tập huấn luyện lân cận thay $z_m$ bằng $(1,-1)$; $W=[-1,1]$, $G=4$.
  - $\lambda=0$: nghiệm $\pm1$; hàm lỗi tại $(1,1)$ đổi từ $0$ lên $4$, với mọi $m$.
  - Bảng $\lambda=0{,}1$: hàng $m=10;100;1000$; cột khoảng cách $1{,}3333$; $0{,}3333$; $0{,}0392$; cột cận $8/(\lambda m)$: $8$; $0{,}8$; $0{,}08$.
  - {{thẻ phải}} **Ví dụ 06.9.** $W=\mathbb R$, $\lambda=1$, $m=100$; $S$: $100$ bản sao $(1,1)$; $S^{(100)}$: quan sát cuối thay bằng $(M,0)$.
  - $\hat w_S\approx0{,}6667$, $\hat w_{S^{(100)}}=99/(149+M^2)$; hàm lỗi tại $(1,1)$ đổi $0{,}0045$; $0{,}2518$; $0{,}8695$ khi $M=1$; $10$; $100$.
  - Không có $G$ hữu hạn; với $M=m$, thay đổi không giảm theo $m$.
- **Ghi chú diễn giả:** Thẻ trái: các quan sát $(0,0)$ có hàm lỗi $0$, nên $L_S(w)=\tfrac1m(w\mp1)^2$; với $\lambda=0$, hai nghiệm cách nhau bằng đường kính $2$ của $W$. Không có $\lambda$, chứng minh chỉ còn độ cong $2/m$ của chính $L_S$, và cách lập luận cũ chỉ cho khoảng cách không quá $G=4$, lớn hơn đường kính. Với $\lambda=0{,}1$, hai nghiệm là $\pm2/(2+\lambda m)$; khi $m$ lớn, cận chỉ lỏng khoảng hai lần. Thẻ phải: đạo hàm $2(wx-y)x$ không bị chặn quanh $\hat w_S$ khi $x$ không bị chặn; với $M=m$, nghiệm trên tập huấn luyện lân cận dần về $0$ trong khi $\hat w_S=2/3$. Với hàm lỗi bình phương, cận ổn định cần dữ liệu bị chặn; khi $x$ không bị chặn, không thuật toán nào học được bài toán này (UML §12.2.1, Ví dụ 12.9). Nguồn: ghi chú Bài 06, Ví dụ 06.7, 06.9; Nhận xét 06.12 (đọc thêm).
- **Lý do / nối:** hai phản ví dụ bỏ giả thiết mà §10 liệt kê, mỗi phản ví dụ chỉ vào một bước của 5-02 (ghi chú diễn giả) → bài tập.
- **Mục tiêu / nguồn:** 5; Ví dụ 06.7, 06.9.

#### `5-05` Bài tập: hồi quy ridge với hệ số chính quy hóa bằng 2 — bài tập (Bài tập 06.6(a)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - (a) Lập lại Bước 2–3 của Ví dụ 06.4 với $\lambda=2$: tính $\hat w_S$, $\hat w_{S^{(4)}}$, khoảng cách giữa hai nghiệm và $L_S(\hat w_S)$.
  - So khoảng cách với cận $2G/(\lambda m)$ của Mệnh đề 06.11. Xếp bốn giá trị $\lambda\in\{0,1,2,4\}$ theo khoảng cách và theo $L_S(\hat w_S)$.
  - **Lời giải:** $\hat w_S=2{,}5/7{,}25=10/29\approx0{,}3448$, $\hat w_{S^{(4)}}=2/29\approx0{,}0690$; khoảng cách $8/29\approx0{,}2759$.
  - Cận $2\cdot4/(2\cdot4)=1$, lỏng khoảng $3{,}6$ lần; $L_S(\hat w_S)\approx0{,}4156$.
  - $\lambda=0;1;2;4$: khoảng cách $0{,}6154$; $0{,}3810$; $0{,}2759$; $0{,}1778$ giảm; $L_S(\hat w_S)$: $0{,}2692$; $0{,}3390$; $0{,}4156$; $0{,}5123$ tăng.
- **Ghi chú diễn giả:** Bước 2 của Ví dụ 06.4 cho $\hat w_S=2{,}5/(3{,}25+2\lambda)$ và $\hat w_{S^{(4)}}=0{,}5/(3{,}25+2\lambda)$; với $\lambda=2$, mẫu số là $7{,}25$. Rủi ro thực nghiệm tính bằng $L_S(w)=\tfrac14(3{,}25w^2-5w+3)$ tại $w=10/29$. Dòng cuối là hai dãy ngược chiều: chính quy hóa mạnh hơn làm nghiệm ổn định hơn nhưng khớp tập huấn luyện kém hơn. Phần (b), (c) là thực nghiệm tùy chọn: giao thức đo độ nhạy trên dữ liệu tổng hợp và đường mức trong $\mathbb R^2$. Nguồn: tệp bài tập, Bài tập 06.6 và lời giải.
- **Lý do / nối:** bài tập của cụm ổn định của ERM có chính quy hóa, dùng ví dụ xuyên suốt; dòng cuối dẫn sang đánh đổi khớp–ổn định → tiêu đề mạch 6.
- **Mục tiêu / nguồn:** 4, 5; Bài tập 06.6(a).

### Mạch 6. Đánh đổi khớp–ổn định (7 trang, 18 phút)

#### `6-00` 6. Đánh đổi khớp–ổn định — tiêu đề mạch, điểm vào mạch 6 · 0,5 phút
- **Mặt trang:** "6."; h2 "Đánh đổi khớp–ổn định"; `p.strand-lead` (bảng mạch, 24 âm tiết); `p.strand-keys`: "số hạng ổn định · số hạng khớp · bất đẳng thức oracle · cỡ mẫu".
- **Ghi chú diễn giả:** Bài tập vừa làm cho hai dãy ngược chiều: khi hệ số chính quy hóa tăng, khoảng cách giữa hai nghiệm giảm còn rủi ro thực nghiệm của nghiệm tăng. Mạch này đưa hai dãy đó vào một cận cho rủi ro kì vọng, chọn hệ số làm nhỏ nhất cận, suy ra cỡ mẫu đủ, so với hạ gradient ngẫu nhiên dùng quan sát mới, và nêu cái giá khi đổi bảo đảm theo kì vọng thành bảo đảm với xác suất cao. Nguồn: ghi chú Bài 06, §9.
- **Lý do / nối:** mạch 5 → trực quan đánh đổi.
- **Mục tiêu / nguồn:** 5; §9.

#### `6-01` Hai số hạng của rủi ro vượt mức — trực quan, ví dụ (đoạn mở §9, Ví dụ 06.12) · 2,5 phút
- **Mặt trang:**
  - Mệnh đề 06.5(a) lấy kì vọng, $u\in W$ cố định: $$\mathbb E_SL_D(\hat w_S)-L_D(u)=\mathbb E_S[L_D(\hat w_S)-L_S(\hat w_S)]+\mathbb E_S[L_S(\hat w_S)-L_S(u)].$$
  - Khi $\lambda$ tăng, cận $2G^2/(\lambda m)$ của số hạng đầu giảm, số hạng sau có thể tăng: đánh đổi khớp–ổn định (fitting–stability trade-off).
  - **Trực quan.** $\lambda=0$: hệ số ổn định không giảm theo $m$ (Ví dụ 06.7); $\lambda$ lớn: $L_S(\hat w_S)$ tăng (Ví dụ 06.4).
  - **Ví dụ.** $X=Y=1$ chắc chắn, hàm lỗi bình phương, $W=\mathbb R$: $L_S=L_D$, $\hat w_S=1/(1+\lambda/2)$, $L_D(\hat w_S)=(\lambda/(2+\lambda))^2$: $0{,}0083$; $0{,}25$; $0{,}8264$ với $\lambda=0{,}2$; $2$; $20$.
- **Ghi chú diễn giả:** Đẳng thức ở dòng đầu đúng với điểm so sánh cố định, vì số hạng $L_S(u)-L_D(u)$ có kì vọng $0$. Cận của số hạng thứ nhất đến từ Định lý 06.10 với Mệnh đề 06.11. Ví dụ là chính quy hóa quá mạnh: mọi quan sát bằng $(1,1)$, nên khoảng cách tổng quát hóa bằng $0$ trên mọi tập huấn luyện; số hạng phạt kéo $\hat w_S$ ra xa điểm tốt nhất $1$, và $L_D(\hat w_S)$ tăng theo $\lambda$. Hai cực biên cho thấy hệ số phải nằm giữa. Nguồn: ghi chú Bài 06, §9, đoạn mở; Ví dụ 06.12.
- **Lý do / nối:** trực quan và ví dụ phản "càng nhiều chính quy hóa càng tốt" trước phát biểu (số liệu không cần hệ quả) → bất đẳng thức oracle.
- **Mục tiêu / nguồn:** 5; §9 đoạn mở, Ví dụ 06.12.

#### `6-02` Bất đẳng thức oracle cho ERM có chính quy hóa — kết quả (Hệ quả 06.13) · 2,5 phút
- **Mặt trang:**
  - **Hệ quả 06.13.** **Giả thiết:** $S\sim D^m$ theo (T1); hàm lỗi, $W$ như Mệnh đề 06.11, $\ell(w,\cdot)$ đo được, $L_D(w_0)<\infty$ với một $w_0\in W$;
  - $\lambda>0$ chọn trước khi thấy tập huấn luyện; $u\in W$ cố định.
  - **Bảo đảm:** theo kì vọng theo $S$: (a) $\mathbb E_SL_D(\hat w_S)-L_D(u)\le\frac{2G^2}{\lambda m}+\frac\lambda2\lVert u\rVert^2$, số hạng ổn định cộng số hạng khớp;
  - (b) bất đẳng thức oracle (oracle inequality): $\mathbb E_SL_D(\hat w_S)\le\inf_{u\in W}\big[L_D(u)+\tfrac\lambda2\lVert u\rVert^2\big]+\frac{2G^2}{\lambda m}$;
  - (c) $W_B=\{u\in W:\lVert u\rVert\le B\}\ne\varnothing$, $\lambda^*=2G/(B\sqrt m)$: $m\ge4G^2B^2/\epsilon^2$ đủ cho mức $\epsilon$ và
  - $$\mathbb E_SL_D(\hat w_S)-\inf_{u\in W_B}L_D(u)\le\frac{2GB}{\sqrt m}.$$
- **Ghi chú diễn giả:** Đại lượng được chặn là rủi ro vượt mức kì vọng so với một điểm so sánh cố định, hay so với $W_B$. Bảo đảm (c) có thể hiểu theo nghĩa: lấy trung bình trên nhiều tập huấn luyện cỡ $m$, rủi ro kì vọng của $\hat w_S$ vượt $\inf_{W_B}L_D$ không quá $2GB/\sqrt m$. Phần (b) so đầu ra với mốc $\inf_u[L_D(u)+\tfrac\lambda2\lVert u\rVert^2]$, mốc chỉ tính được khi biết $D$; vì vậy gọi là bất đẳng thức oracle như ở Bài 04. Hệ số $\lambda^*$ phụ thuộc $G$, $B$, $m$, được chọn trước khi thấy tập huấn luyện. Kết quả ở mức phác thảo; chi tiết về tính khả tích ở Phụ lục C. Nguồn: ghi chú Bài 06, §9, Hệ quả 06.13 và đoạn sau.
- **Lý do / nối:** phát biểu sau trực quan; trang ý tưởng chứng minh riêng ở sau.
- **Mục tiêu / nguồn:** 5; Hệ quả 06.13.

#### `6-03` Ý tưởng chứng minh: bất đẳng thức oracle — ý tưởng chứng minh · 3 phút
- **Mặt trang:**
  - **Bước 1 ($u\in W$).** $L_S(\hat w_S)\le F_{S,\lambda}(\hat w_S)\le F_{S,\lambda}(u)=L_S(u)+\tfrac\lambda2\lVert u\rVert^2$.
  - **Bước 2 ($u$ cố định).** Mệnh đề 06.5(a) theo kì vọng; Bước 1 chặn số hạng khớp.
  - **Bước 3 ((T1)).** Định lý 06.10, Mệnh đề 06.11 chặn số hạng ổn định bởi $2G^2/(\lambda m)$: (a).
  - **Bước 4.** Cận dưới đúng theo $u$: (b).
  - **Bước 5.** **Nhắc lại:** cân hai số hạng (Bài 05), $a/\lambda+b\lambda\ge2\sqrt{ab}$ với $a=2G^2/m$, $b=B^2/2$: $\lambda^*=\sqrt{a/b}$, cận $2GB/\sqrt m$.
  - $u$ chọn theo $S$: Bước 2 hỏng.
- **Ghi chú diễn giả** (~170 âm tiết): Lộ trình: tính tối ưu của $\hat w_S$, phân tích rủi ro, rồi tính ổn định. Bước 1 dùng $\tfrac\lambda2\lVert\hat w_S\rVert^2\ge0$ và $u\in W$. Ở Bước 3, Định lý 06.10 chặn trị tuyệt đối, nhưng chỉ cần phía trên; (T1) dạng đầy đủ vào ở đây. Phụ lục C kiểm các kì vọng hữu hạn: Bước 1 cho $\mathbb EL_S(\hat w_S)<\infty$; cùng chuỗi bất đẳng thức cho $\mathbb E\lVert\hat w_S\rVert^2\le\lVert u\rVert^2+2L_D(u)/\lambda$; rồi (L) cho $\mathbb EL_D(\hat w_S)<\infty$. Ở Bước 5, với $u\in W_B$, vế phải của (a) không quá $a/\lambda+b\lambda$; tại $\lambda^*$, hai số hạng bằng nhau, mỗi số hạng $GB/\sqrt m$. Câu ôn nhanh 3 là đúng phép tính này với $a=0{,}02$, $b=0{,}5$. Giá trị cân bằng phụ thuộc $\lVert u\rVert$, nên đoán sai $B$ làm cận tăng; bài tập cuối mạch đo mức tăng. Nguồn: ghi chú Bài 06, chứng minh Hệ quả 06.13; Phụ lục C.
- **Lý do / nối:** trang ý tưởng chứng minh riêng; kỹ thuật của Bài 05 nhắc lại bằng tên → ví dụ cỡ mẫu.
- **Mục tiêu / nguồn:** 5; chứng minh Hệ quả 06.13.

#### `6-04` Ví dụ: cỡ mẫu theo cận và một triệu hồ sơ — ví dụ (Ví dụ 06.10, 06.11), hình F2 · 3,5 phút
- **Mặt trang** {{`grid2`: trái chữ, phải hình F2}}:
  - **Ví dụ 06.10.** Hồi quy ridge, $\lVert x\rVert\le1$, $\lvert y\rvert\le1$, $W$ quả cầu đơn vị: $G=4$, $B=1$; $m=1600$: $\lambda^*=0{,}2$, cận $0{,}2$.
  - Mức $\epsilon=0{,}1$: ERM có chính quy hóa cần $m\ge6400$; SGD, quan sát mới: $T\ge1600$, tức $1599$ quan sát.
  - **Ví dụ 06.11.** $m=10^6$ hồ sơ, $B=5$: $\lambda^*=4\cdot10^{-4}$, hai số hạng $0{,}005+0{,}005=0{,}01$; một vòng SGD: $0{,}005$.
  - **Diễn giải:** hai cận cùng bậc $GB/\sqrt m$; ERM có chính quy hóa cần khoảng bốn lần số quan sát.
  - {{Hình F2 bên phải}}
- **Ghi chú diễn giả:** Hình F2 vẽ vế phải của Hệ quả 06.13(a) với $\lVert u\rVert=B=1$, $G=4$, $m=1600$: $0{,}02/\lambda+0{,}5\lambda$, nhỏ nhất $0{,}2$ tại $\lambda=0{,}2$. Với hồi quy logistic, $G=1$, $B=5$, $\epsilon=0{,}05$, tối thiểu hóa rủi ro thực nghiệm có chính quy hóa cần $m\ge40\,000$, còn SGD với quan sát mới cần $T\ge10^4$. Thừa số bốn đến từ hằng số $2$ trong $2GB/\sqrt m$; ngoài ra, quy tắc có chính quy hóa còn cần giải đúng $F_{S,\lambda}$. Với một triệu hồ sơ, câu hỏi thực hành có hai câu trả lời: một vòng SGD bảo đảm mức $0{,}005$, quy tắc có chính quy hóa với $\lambda^*$ bảo đảm mức $0{,}01$. Hàm lỗi logistic của mô hình tuyến tính không bị chặn nhưng lồi và $1$-Lipschitz theo $w$; với mô hình khác, các cận có thể không áp dụng. Nguồn: ghi chú Bài 06, Ví dụ 06.10, 06.11.
- **Lý do / nối:** cận số bắt buộc của bài; trả lời vế thứ hai của câu hỏi thực hành → giới hạn theo kì vọng.
- **Mục tiêu / nguồn:** 5; Ví dụ 06.10, 06.11.

#### `6-05` Bảo đảm theo kì vọng và bảo đảm với xác suất cao — kết quả (Nhận xét 06.14) · 3 phút
- **Mặt trang:**
  - Hệ quả 06.2, 06.13, Định lý 06.10: theo kì vọng, cho một thuật toán.
  - Bài 02–04: xác suất $\ge1-\delta$, đồng thời mọi giả thuyết của lớp.
  - **Nhắc lại:** bất đẳng thức Markov (Bổ đề 02.2): $V\ge0$, $\alpha>0$ thì $\Pr(V\ge\alpha)\le\mathbb EV/\alpha$.
  - $W$ quả cầu bán kính $B$: $\Pr_S[L_D(\hat w_S)-\inf_WL_D\ge\epsilon]\le2GB/(\epsilon\sqrt m)$; $G=4$, $B=1$, $\epsilon=0{,}1$, $\delta=0{,}05$: $m\ge2\,560\,000$, gấp $1/\delta^2=400$ lần $6400$.
  - Chia khối và xác thực (Bài tập 06.7, hàm lỗi trong $[0,1]$): số khối $\lceil\log_2(2/\delta)\rceil$ thay cho thừa số $1/\delta^2$.
- **Ghi chú diễn giả:** Bất đẳng thức Markov áp dụng được vì $\hat w_S\in W$, nên $L_D(\hat w_S)-\inf_WL_D\ge0$. Cách chia khối: chia dữ liệu thành $k=\lceil\log_2(2/\delta)\rceil$ khối huấn luyện, mỗi khối đủ cho mức kì vọng $\epsilon/4$, và một tập xác thực cỡ $8\ln(4k/\delta)/\epsilon^2$; chạy quy tắc trên từng khối rồi chọn ứng viên có rủi ro thực nghiệm nhỏ nhất trên tập xác thực. Với hàm lỗi không bị chặn như hàm lỗi logistic, bước chọn cần thêm một cận cho hàm lỗi trên các ứng viên. Nhận xét 06.15 (đọc thêm): nghiệm gần đúng theo (O2) thêm $G\sqrt{2\epsilon_{\mathrm{opt}}/\lambda}$ vào cận, bằng $0{,}1265$ khi $G=4$, $\lambda=0{,}2$, $\epsilon_{\mathrm{opt}}=10^{-4}$. Nguồn: ghi chú Bài 06, Nhận xét 06.14, 06.15.
- **Lý do / nối:** phân biệt kì vọng và xác suất cao (blueprint §6.2); câu nối về loại bảo đảm trước bài tập → bài tập.
- **Mục tiêu / nguồn:** 5; Nhận xét 06.14.

#### `6-06` Bài tập: hệ số chính quy hóa lệch một thừa số — bài tập (Bài tập 06.4(b)), lời giải trên mặt trang · 3 phút (1 phút tự làm)
- **Mặt trang:**
  - Hệ quả 06.13(a) với $\lVert u\rVert\le B$: $\mathbb E_SL_D(\hat w_S)-L_D(u)\le Q(\lambda)$, $Q(\lambda)=\frac{2G^2}{\lambda m}+\frac{\lambda B^2}2$.
  - (b) Với $\lambda=c\lambda^*$ và $c>0$, chứng minh $Q(c\lambda^*)=Q(\lambda^*)\cdot\tfrac12(c+1/c)$. Tính thừa số $\tfrac12(c+1/c)$ với $c=2$, $c=\tfrac12$ và $c=10$.
  - **Lời giải:** $\frac{2G^2}{c\lambda^*m}=\frac{GB}{c\sqrt m}$ và $\frac{c\lambda^*B^2}2=\frac{cGB}{\sqrt m}$; tổng $\frac{GB}{\sqrt m}(c+\tfrac1c)=Q(\lambda^*)\cdot\tfrac12(c+\tfrac1c)$.
  - $c=2$ và $c=\tfrac12$: $1{,}25$; $c=10$: $5{,}05$. Lệch thừa số $2$: cận tăng $25\%$; lệch thừa số $10$: cận gấp $5{,}05$ lần.
- **Ghi chú diễn giả:** Phần (a) của bài là phép tính ở Bước 5 của chứng minh Hệ quả 06.13: $Q(\lambda^*)=2GB/\sqrt m$. Thừa số $\tfrac12(c+1/c)$ đối xứng giữa $c$ và $1/c$: chọn hệ số lớn gấp đôi hay nhỏ một nửa đều làm cận tăng $25\%$. Cận vẫn đúng với mọi $\lambda>0$; chỉ giá trị của nó tăng. Phần (c) đặt tình huống đoán sai chuẩn của điểm so sánh và là bài tập tổng hợp ở mạch cuối; phần (d) giải thích vì sao không chọn $\lambda$ bằng rủi ro thực nghiệm trên chính tập huấn luyện. Nguồn: tệp bài tập, Bài tập 06.4 và lời giải.
- **Lý do / nối:** bài tập của cụm đánh đổi, ngắn vì mạch Tổng kết dùng tiếp phần (c) → tiêu đề mạch 7.
- **Mục tiêu / nguồn:** 5; Bài tập 06.4(b).

### Mạch 7. Tổng kết (9 trang, 9 phút)

#### `7-00` 7. Tổng kết — tiêu đề mạch, điểm vào mạch 7 · 0,5 phút
- **Mặt trang:** "7."; h2 "Tổng kết"; `p.strand-lead` (bảng mạch, 17 âm tiết); không có dòng từ khóa.
- **Ghi chú diễn giả:** Bài có một bảo đảm trực tiếp cho rủi ro kì vọng khi dùng quan sát mới, một phân tích rủi ro cho đầu ra tính trên tập huấn luyện lưu lại, một định lý ổn định, một hệ số ổn định cho quy tắc có chính quy hóa và một bất đẳng thức oracle ghép các kết quả đó. Kỹ thuật mới dùng lại về sau là lập luận đổi vai. Mạch cuối gom các giả thiết không được bỏ, trả lời vấn đề trung tâm cho cả bài, làm một bài tập ghép hệ số ổn định với cận đánh đổi, rồi tự kiểm tra và giao bài tập. Nguồn: ghi chú Bài 06, §10–§13.
- **Lý do / nối:** mạch 6 → bảng tổng kết.
- **Mục tiêu / nguồn:** tất cả; §10–§13.

#### `7-01` Bảng tổng kết — tổng kết · 1 phút

Deck: bảng tách hai trang (mục 16): `7-01` hai hàng Hệ quả 06.2, Mệnh đề 06.5; `7-02` "Bảng tổng kết (tiếp)" ba hàng Định lý 06.10, Mệnh đề 06.11, Hệ quả 06.13 (sau sửa, mục 17) · 0,5 phút. Bảng năm hàng dưới đây là nội dung gộp của hai trang.
- **Mặt trang (bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh`, trần 80):**
  | Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh |
  |---|---|---|
  | Hệ quả 06.2: $\mathbb EL_D(\bar w_T)-L_D(u)\le RG/\sqrt T$ | quan sát mới độc lập; $\ell(\cdot,z)$ lồi; $\mathbb E\lVert v\rVert^2\le G^2$; $W$ đóng, lồi; $\lVert w_1-u\rVert\le R$ | Bổ đề 06.1; Hệ quả 05.15 |
  | Mệnh đề 06.5: $\mathbb EL_D(\tilde w)-\inf_WL_D\le\mathbb E[L_D(\tilde w)-L_S(\tilde w)]+\mathbb E\operatorname{opt}_S(\tilde w)$ | $Z_i\sim D$; $u$ cố định | thêm bớt $L_S$ |
  | Định lý 06.10: $\lvert\mathbb E[L_D-L_S]\rvert\le\epsilon_{\mathrm{stab}}(m)$ | (T1) dạng đầy đủ; ổn định đều | đổi vai |
  | Mệnh đề 06.11, tất định: $\lVert\hat w_s-\hat w_{s^{(i)}}\rVert\le2G/(\lambda m)$, $\epsilon_{\mathrm{stab}}=2G^2/(\lambda m)$ | $\ell(\cdot,z)$ lồi; (L); $\lambda>0$; $W$ đóng, lồi | hai tăng trưởng bậc hai |
  | Hệ quả 06.13: $\mathbb E_SL_D(\hat w_S)-\inf_{W_B}L_D\le2GB/\sqrt m$ ($\lambda=\lambda^*$) | như trên; (T1); $\lambda$ chọn trước | ba kết quả trên; cân hai số hạng |
- **Ghi chú diễn giả:** Mỗi giả thiết có một phản ví dụ hoặc một bước hỏng trong bài: bỏ quan sát mới, chương trình thứ hai có rủi ro vượt mức kì vọng $0{,}2261$ trong khi cận là $0{,}1$; chọn điểm so sánh theo tập huấn luyện, bước kì vọng bằng $0$ của Mệnh đề 06.5 hỏng; bỏ dạng đầy đủ của (T1), phép đổi chỗ đổi phân bố; bỏ $\lambda>0$, hai nghiệm cách nhau bằng đường kính của tập tham số với mọi $m$; bỏ dữ liệu bị chặn với hàm lỗi bình phương, không có hằng số Lipschitz hữu hạn. Bổ đề 06.1, 06.7, 06.8 là công cụ, không có hàng riêng. Nhận xét 06.12 và 06.15 ở mức đọc thêm. Nguồn: ghi chú Bài 06, §4–§9, §10.
- **Lý do / nối:** một hàng cho mỗi kết quả chính, giữ loại bảo đảm và giả thiết đầy đủ khi đặt cạnh nhau → vấn đề trung tâm.
- **Mục tiêu / nguồn:** tất cả; §4–§9.

#### `7-03` Vấn đề trung tâm — tổng kết · 1,5 phút
- **Mặt trang:**
  - Quan sát mới, hàm lỗi lồi, $\mathbb E\lVert v\rVert^2\le G^2$, $\eta=R/(G\sqrt T)$: $\mathbb EL_D(\bar w_T)-\inf_WL_D\le RG/\sqrt T$ khi $\lVert w_1-u\rVert\le R$ trên $W$.
  - Tập huấn luyện dùng lại: $\mathbb EL_D(\tilde w)-\inf_WL_D\le$ khoảng cách tổng quát hóa kì vọng $+\ \mathbb E\operatorname{opt}_S(\tilde w)$.
  - Ổn định đều, (T1) dạng đầy đủ: $\lvert\mathbb E[L_D-L_S]\rvert\le\epsilon_{\mathrm{stab}}(m)$.
  - Hàm lỗi lồi không âm, (L), $W$ đóng, lồi, $\lambda>0$ chọn trước: $\epsilon_{\mathrm{stab}}=2G^2/(\lambda m)$; với $\lambda^*$: $\mathbb E_SL_D(\hat w_S)-\inf_{W_B}L_D\le2GB/\sqrt m$.
  - Theo kì vọng, cấp thuật toán; với xác suất ít nhất $1-\delta$: thêm thừa số $1/\delta^2$ về cỡ mẫu (Markov).
- **Ghi chú diễn giả:** Trả lời cho câu hỏi "khi nào tối ưu trở thành học": khi gradient ngẫu nhiên không chệch cho rủi ro kì vọng, tức mỗi bước dùng một quan sát mới; hoặc khi bộ giải chạy trên tập huấn luyện lưu lại có khoảng cách tổng quát hóa kì vọng nhỏ. Tối thiểu hóa rủi ro thực nghiệm có chính quy hóa với hàm lỗi lồi, Lipschitz là một thuật toán như vậy nhờ tính ổn định đều. Trong câu hỏi mở đầu, rủi ro vượt mức kì vọng là $0{,}0006$ với quan sát mới và $0{,}2261$ khi dùng lại bốn quan sát. Hạ gradient ngẫu nhiên với quan sát mới dùng $T-1$ quan sát. Các kết quả cần hàm lỗi lồi theo tham số, nên không chuyển sang mạng nơ-ron mà không có lập luận mới. Nguồn: ghi chú Bài 06, §10.
- **Lý do / nối:** trả lời vấn đề trung tâm cho cả bài, giữ loại bảo đảm và điều kiện của từng câu → bài tập tổng hợp.
- **Mục tiêu / nguồn:** tất cả; §10.

#### `7-04` Bài tập: đoán sai chuẩn của điểm so sánh — bài tập tổng hợp (Bài tập 06.4(c)), đề · 1,5 phút
- **Mặt trang:**
  - Bài tập 06.4: $Q(\lambda)=\frac{2G^2}{\lambda m}+\frac{\lambda B^2}2$; (a) chọn $\lambda=2G/(B\sqrt m)$.
  - (c) Hồi quy logistic, $\lVert x\rVert\le4$, $W=\mathbb R^p$: gradient của hàm lỗi có chuẩn không quá $\lVert x\rVert$ (Ví dụ 05.9),
  - nên (L) đúng với $G=4$; $m=1600$; hệ số theo (a) với $B_0=1$, điểm so sánh có chuẩn $B=2$.
  - Viết $Q$ tại hệ số đó theo $G$, $m$, $B_0$, $B$, tính giá trị và so với $Q(\lambda^*)$ với $B=2$.
  - Tính hệ số ổn định (Mệnh đề 06.11) tại hai hệ số.
- **Ghi chú diễn giả:** Bài ghép ba kết quả của bài: hệ số ổn định $2G^2/(\lambda m)$ của Mệnh đề 06.11, cận đánh đổi của Hệ quả 06.13(a), và hệ số $\lambda^*$ của phần (c) của hệ quả. Tình huống thực tế là chuẩn của điểm so sánh tốt nhất chưa biết, nên hệ số được chọn theo một giá trị đoán $B_0$. Gợi ý: hệ số đã chọn là $\lambda_0=2G/(B_0\sqrt m)$; thay vào $Q$ và tách hai số hạng. Nguồn: tệp bài tập, Bài tập 06.4(c) và hai gợi ý.
- **Lý do / nối:** bài tập tổng hợp từ `exercises.md`; đề trên một trang vì câu chữ dài → lời giải.
- **Mục tiêu / nguồn:** 4, 5; Bài tập 06.4(c).

#### `7-05` Lời giải: đoán sai chuẩn của điểm so sánh — bài tập tổng hợp (Bài tập 06.4(c)), lời giải · 2 phút
- **Mặt trang:**
  - **Lời giải:** $\sqrt m=40$, $\lambda_0=2\cdot4/(1\cdot40)=0{,}2$.
  - $Q(\lambda_0)=\frac{GB_0}{\sqrt m}+\frac{GB^2}{B_0\sqrt m}=\frac G{\sqrt m}\big(B_0+\frac{B^2}{B_0}\big)=0{,}1\cdot(1+4)=0{,}5$.
  - $B=2$: $\lambda^*=8/80=0{,}1$, $Q(\lambda^*)=16/40=0{,}4$; $\lambda_0=2\lambda^*$, tỉ số $1{,}25$ như $c=2$ ở phần (b).
  - $\epsilon_{\mathrm{stab}}=2\cdot16/(0{,}2\cdot1600)=0{,}1$ tại $\lambda_0$ và $0{,}2$ tại $\lambda^*$.
  - **Kết luận:** tại $\lambda_0$, số hạng ổn định giảm từ $0{,}2$ xuống $0{,}1$, số hạng khớp tăng từ $0{,}2$ lên $0{,}4$; cận $0{,}5$ vẫn đúng.
- **Ghi chú diễn giả:** Cận $0{,}5$ vẫn đúng vì phần (a) của Hệ quả 06.13 đúng với mọi $\lambda>0$ và mọi $u\in W$; chọn sai $B$ chỉ làm cận lớn hơn mức tốt nhất $0{,}4$. Ở đây hệ số đã chọn gấp đôi hệ số đúng, nên tỉ số $0{,}5/0{,}4$ là thừa số $\tfrac12(c+1/c)$ với $c=2$. Kiểm tra: với $B_0=B$, công thức cho lại $2GB/\sqrt m$; với $B_0=4$, $B=2$, nó cho $0{,}1\cdot(4+1)=0{,}5$, như thừa số với $c=\tfrac12$. Nguồn: tệp bài tập, lời giải Bài tập 06.4(c).
- **Lý do / nối:** lời giải trên mặt trang, mỗi dòng một bước → tự kiểm tra.
- **Mục tiêu / nguồn:** 4, 5; Bài tập 06.4(c).

#### `7-06` Câu hỏi tự kiểm tra — tổng kết · 1 phút
- **Mặt trang:**
  - 1. Vì sao cận $RG/\sqrt T$ chặn $\mathbb EL_D(\bar w_T)$ ở chương trình thứ nhất mà không chặn ở chương trình thứ hai?
  - 2. Bước nào của chứng minh Định lý 06.10 cần dạng đầy đủ của (T1)?
  - 3. Hồi quy ridge, $\lVert x\rVert\le1$, $\lvert y\rvert\le1$, $W$ quả cầu đơn vị, $m=400$, $\lambda=0{,}4$: hệ số ổn định bằng bao nhiêu?
  - 4. Cận ở câu 3 có chặn $\mathbb E_S\lvert L_D(\hat w_S)-L_S(\hat w_S)\rvert$ không?
- **Ghi chú diễn giả** (câu trả lời dự kiến, chỉ dùng ghi chú): (1) Ở chương trình thứ nhất, nhãn mới độc lập với điểm lặp, nên gradient ngẫu nhiên không chệch cho $L_D$; ở chương trình thứ hai, khi biết tập huấn luyện, nó chỉ không chệch cho $L_S$, và cận chặn độ chênh tối ưu của $L_S$. (2) Bước đổi chỗ $Z_i$ và $Z'$: phép đổi chỗ giữ phân bố liên hợp chỉ khi các quan sát độc lập cùng phân bố. (3) $G=4$, $\epsilon_{\mathrm{stab}}(400)=32/160=0{,}2$, nên $\lvert\mathbb E_S[L_D(\hat w_S)-L_S(\hat w_S)]\rvert\le0{,}2$; ở đây $\lambda=0{,}4=\lambda^*$ và cận của Hệ quả 06.13(c) là $0{,}4$. (4) Không: Định lý 06.10 chặn trị tuyệt đối của kì vọng, không chặn kì vọng của trị tuyệt đối (thuật toán hằng). Nguồn: ghi chú Bài 06, Câu hỏi mở đầu, chứng minh Định lý 06.10, Ví dụ 06.5, §12 và lời giải.
- **Lý do / nối:** bốn câu ngắn trả lời được chỉ bằng ghi chú; câu 3, 4 là câu hỏi cuối buổi §12 → bài tập về nhà.
- **Mục tiêu / nguồn:** 1, 3, 4; §4, §7, §12.

#### `7-07` Bài tập về nhà — tổng kết · 0,5 phút
- **Mặt trang:**
  | Mục | Bài tập |
  |---|---|
  | 2. Quan sát mới và tập huấn luyện lưu lại | 06.1 |
  | 3. ERM có chính quy hóa | 06.10 |
  | 4. Tính ổn định và khoảng cách tổng quát hóa kì vọng | 06.2 |
  | 5. Tính ổn định của ERM có chính quy hóa | 06.3, 06.5, 06.11 |
  | 6. Đánh đổi khớp–ổn định | 06.4, 06.6, 06.7, 06.8, 06.9 |
  - Liên kết "Ghi chú bài giảng · Bài tập" (viewer `&deck=`).
- **Ghi chú diễn giả:** Mỗi bài xếp vào mạch cung cấp kiến thức cuối cùng bài đó cần. Bài tập 06.3 cần Mệnh đề 06.11 và số của Ví dụ 06.6; 06.5 cần Ví dụ 06.9 và Nhận xét 06.12; 06.11 tổng quát hóa Bổ đề 06.7 và Mệnh đề 06.11 sang chuẩn bất kì. Bài tập 06.4 cần Hệ quả 06.13 và cách chọn bằng tập xác thực; 06.6 đọc đánh đổi khớp–ổn định trên dữ liệu; 06.7 cần Nhận xét 06.14; 06.8 và 06.9 cần Hệ quả 06.13(c). Sáu bài đầu là bài gốc của học phần, năm bài sau chọn từ UML §13.7, §14.8; phần thực nghiệm của Bài tập 06.6 và Bài tập 06.11 là tùy chọn. Nguồn: ghi chú Bài 06, §11; tệp bài tập.
- **Lý do / nối:** giao bài tập theo mạch → tài liệu.
- **Mục tiêu / nguồn:** tất cả; §11.

#### `7-08` Tài liệu tham khảo — tổng kết · 0,5 phút
- **Mặt trang:**
  - Trước buổi học: UML §14.5, §13.1.
  - Sau buổi học: UML §13.2, §13.3.
  - Mở rộng: UML §13.4, §13.3.2, §12.2.1, §12.2.2.
  - Shalev-Shwartz, S. và Ben-David, S. (2014). *Understanding Machine Learning: From Theory to Algorithms*. Cambridge University Press.
  - Bài 07: Mạng nơ-ron, năng lực mô hình và tham số hóa thừa.
- **Ghi chú diễn giả:** UML §14.5 trình bày học bằng hạ gradient ngẫu nhiên với quan sát mới; §13.1 tối thiểu hóa rủi ro có chính quy hóa và hồi quy ridge; §13.2 quy tắc ổn định không quá khớp; §13.3 chính quy hóa Tikhonov như một cơ chế ổn định; §13.4 đánh đổi khớp–ổn định; §13.3.2 hàm lỗi trơn và không âm; §12.2.2 bài toán lồi–Lipschitz–bị chặn (convex-Lipschitz-bounded problem). Khác biệt chính với UML: UML dùng ổn định thay một theo trung bình, một phía, cho thuật toán tất định; học phần dùng ổn định đều, hai phía, cho thuật toán có nguồn ngẫu nhiên riêng. UML dùng $\lambda\lVert w\rVert^2$ và lập luận một phía, nên cỡ mẫu là $8\rho^2B^2/\epsilon^2$ thay cho $4G^2B^2/\epsilon^2$. Bài 07 hỏi đại lượng đo độ phức tạp nào của lớp mạng nơ-ron còn cho thông tin khi mạng khớp được cả nhãn gán ngẫu nhiên. Nguồn: ghi chú Bài 06, §12 đoạn cuối, §13 và quan hệ với UML.
- **Lý do / nối:** trang cuối; dòng chữ Bài 07 (không liên kết cho đến khi deck Bài 07 có tên tệp).
- **Mục tiêu / nguồn:** —; §13.

## 7. Hành trình khái niệm

Thứ tự bước theo quy định: vấn đề → trực quan → ví dụ → phát biểu → ý tưởng chứng minh (trang riêng) → kỹ thuật hoặc kiểm tra. Các bước có thể chung trang nhưng không đảo thứ tự trên mặt trang. Theo cổng duyệt Bài 04 (T5), ví dụ đặt trước phát biểu khi số liệu của nó không cần chính kết quả đó; ví dụ của ghi chú dùng kết quả để kiểm tra thì đứng sau, ở cột cuối.

| Kết quả hoặc khái niệm | Vấn đề | Trực quan | Ví dụ | Phát biểu | Ý tưởng chứng minh | Kỹ thuật / kiểm tra | Gộp, `không áp dụng`, lý do |
|---|---|---|---|---|---|---|---|
| Bổ đề 06.1 | 1-06 (hai chương trình, cùng cận) | 2-03 ("Trực quan.": $w_t$ chưa thấy $Z_t$) | 1-06 (chương trình thứ nhất, dữ liệu) | 2-03 | `không áp dụng`: công cụ, lộ trình hai dòng ở ghi chú diễn giả 2-03 (mục 11, điểm 3) | 2-06 ($v=2(w-y)$, $G=4$) | Trực quan và phát biểu chung trang. |
| Hệ quả 06.2 | 1-06 | 2-03 | 1-06, 2-02 (ứng dụng) | 2-04 | 2-05 | 2-06 (Ví dụ 06.2: $0{,}000578$ so với $0{,}1$); 2-07 (Nhận xét 06.3, $0{,}005$); 2-12 (Bài tập 06.1(d)) | — |
| Định nghĩa 06.4 | 2-07 (oracle không chệch cho $L_S$) | ghi chú diễn giả 2-08 (số có dấu; $\mathbb E\lvert\cdot\rvert$ khác) | 2-08 (ba ví dụ: $0$; $1$; $0{,}5$) | 2-08 | `không áp dụng` (định nghĩa) | 2-11 ($0{,}4750$) | Dòng mở khẳng định (Mệnh đề 01.7) trước định nghĩa. |
| Mệnh đề 06.5 | 2-07, 2-08 | 2-09 ("Trực quan.": hai phần của rủi ro vượt mức) | 2-08 ($\bar Y$: $1{,}25$ so với $0{,}75$) | 2-09 | 2-10 | 2-11 (Ví dụ 06.3: cận $0{,}4761\ge0{,}2261$); 2-12 (Bài tập 06.1(c)) | — |
| Định nghĩa 06.6, Bổ đề 06.7, 06.8 | 3-01 (một quan sát dịch nghiệm $0{,}6154$) | 3-03 ("Trực quan.": không giảm bậc nhất, độ cong $\lambda$) | 3-02 ($\lambda=0$, nghiệm không duy nhất) | 3-02, 3-03 | `không áp dụng`: công cụ, lộ trình ở ghi chú diễn giả 3-03; kỹ thuật điểm trên đoạn thẳng hiện trên mặt trang bài tập 3-05 | 3-04 (Ví dụ 06.4, Hình 06.1); 3-05 (Bài tập 06.10) | Hai bổ đề chung trang (mục 3). |
| Định nghĩa 06.9 | 3-04 (khoảng cách giữa hai nghiệm) | 4-02 | 4-01 dòng đầu ($304/169$) | 4-01 | `không áp dụng` (định nghĩa) | 4-02 dòng "Ví dụ." (thuật toán ghi nhớ: hệ số $1$) | Ví dụ ở dòng đầu trước định nghĩa vì không cần định nghĩa để tính. |
| Định lý 06.10 | 2-11 (câu nối), 4-00 | 4-02 ("Trực quan.": đổi vai; hình F3) | 4-01 ($1{,}7988$), 4-02 (thuật toán ghi nhớ; $h$ cố định) | 4-03 | 4-04 | 4-05 (trang "Kỹ thuật."); 4-06 (Ví dụ 06.5); 4-07 (Bài tập 06.2(b)) | Đẳng thức sau chứng minh của ghi chú đặt ở 4-02, trước phát biểu, vì đọc được mà không cần định lý (mục 11, điểm 12). |
| Mệnh đề 06.11 | 3-01, 3-04 (khoảng cách giảm khi $\lambda$ tăng), 5-00 | 5-01 ("Trực quan.": hiệu $(2G/m)$-Lipschitz, độ cong $\lambda$); Hình 06.1 ở 3-04 | 3-04 (Ví dụ 06.4) | 5-01 | 5-02 | 5-03 (Ví dụ 06.6, 06.8); 5-04 (Ví dụ 06.7, 06.9: bỏ giả thiết); 5-05 (Bài tập 06.6(a)) | Trực quan và phát biểu chung trang. |
| Hệ quả 06.13 | 5-05 (hai dãy ngược chiều), 6-00 | 6-01 ("Trực quan.": hai cực biên) | 6-01 (Ví dụ 06.12) | 6-02 | 6-03 | 6-04 (Ví dụ 06.10, 06.11, hình F2); 6-05 (Nhận xét 06.14); 6-06 (Bài tập 06.4(b)); 7-04, 7-05 (Bài tập 06.4(c)) | Ví dụ 06.12 đặt trước phát biểu (số liệu không cần hệ quả; mục 11, điểm 12). |

Thời lượng theo mạch: 9 + 32 + 14 + 22 + 16 + 18 + 9 = 120 phút; 55 trang (bản deck, mục 16).

## 8. Hình vẽ

Mọi hình là SVG trong `2627-1/img/lec-06/`, `role="img"`, có `<title>` và alt cụ thể; màu không là tín hiệu duy nhất (kiểu nét và hình dạng điểm khác nhau cho từng dãy); chữ trong hình chỉ là nhãn trục, nhãn điểm, số và nhãn ngắn (Unicode), không công thức; công thức và chú thích nằm ở `figcaption` (KaTeX). Chú thích nêu dữ liệu.

| Mã | Tệp | Trang | Nội dung và dữ liệu | Alt dự kiến |
|---|---|---|---|---|
| Hình 06.1 (có sẵn) | `ridge-thay-mot-quan-sat.svg` (dùng chung với ghi chú, 564×340) | 3-04 | Hai khung, $w\in[-0{,}25;1]$: $\lambda=0$ (trục tung đến $1{,}4$) và $\lambda=4$ (trục tung đến $2{,}5$); nét liền $F_{S,\lambda}$ với điểm cực tiểu tròn đặc, nét đứt $F_{S^{(4)},\lambda}$ với điểm cực tiểu vuông rỗng; nhãn khoảng cách $0{,}615$ và $0{,}178$. `figcaption` theo chú thích Hình 06.1 của ghi chú. Hai điểm cần quyết định (mục 11, điểm 9): chú giải trong SVG ghi "mẫu S", "mẫu S⁽⁴⁾", trong khi ghi chú viết "tập huấn luyện"; ở khung phải, nét đứt vượt $2{,}5$ khi $w>0{,}8345$ và bị cắt ở mép trên. | Alt của ghi chú: "Hai đồ thị của mục tiêu có chính quy hóa theo w trên đoạn từ −0,25 đến 1. Mỗi đồ thị có một đường liền cho tập huấn luyện S và một đường đứt cho tập huấn luyện thay quan sát thứ tư. Với λ = 0, hai điểm cực tiểu là 0,769 và 0,154, cách nhau 0,615. Với λ = 4, hai điểm cực tiểu là 0,222 và 0,044, cách nhau 0,178." |
| F2 | `danh-doi-khop-on-dinh.svg` | 6-04 | Trục ngang $\lambda$ thang lôgarit từ $0{,}02$ đến $2$ (vạch $0{,}02$; $0{,}05$; $0{,}1$; $0{,}2$; $0{,}5$; $1$; $2$); trục dọc tuyến tính $[0;1{,}2]$ (vạch từng $0{,}2$). Ba đường từ vế phải của Hệ quả 06.13(a) với $\lVert u\rVert=B=1$, $G=4$, $m=1600$ (số liệu V16): số hạng ổn định $0{,}02/\lambda$ (nét đứt, giảm từ $1$ xuống $0{,}01$), số hạng khớp $0{,}5\lambda$ (nét chấm, tăng từ $0{,}01$ lên $1$), tổng (nét liền đậm, $1{,}01$ ở hai đầu mút). Một chấm tại $(0{,}2;0{,}2)$ nhãn "λ* = 0,2: 0,2"; nhãn trực tiếp cuối đường: "số hạng ổn định", "số hạng khớp", "tổng". Giá trị lớn nhất $1{,}01<1{,}2$: trục chứa hết dữ liệu. `figcaption`: "Vế phải của Hệ quả 06.13(a) với $\lVert u\rVert=B=1$, $G=4$, $m=1600$: số hạng ổn định $0{,}02/\lambda$, số hạng khớp $0{,}5\lambda$ và tổng; nhỏ nhất $0{,}2$ tại $\lambda^*=0{,}2$." | "Đồ thị theo hệ số chính quy hóa trên trục lôgarit từ 0,02 đến 2. Đường nét đứt giảm, đường nét chấm tăng, và tổng của chúng có dạng chữ U với đáy 0,2 tại hệ số 0,2. Ở hai đầu mút, tổng xấp xỉ 1." |
| F3 | `doi-vai.svg` | 4-02 | Sơ đồ hai hàng, không có số. Hàng trên, nhãn trái "S": năm ô viền liền "Z₁", "…", "Zᵢ", "…", "Zₘ"; cách một khoảng, một ô viền đứt, nền xám nhạt "Z′" với nhãn trên "kiểm tra". Hàng dưới, nhãn trái "S⁽ⁱ⁾": "Z₁", "…", "Z′", "…", "Zₘ" viền liền; ô viền đứt nền xám "Zᵢ", nhãn "kiểm tra". Hai mũi tên chéo nối ô "Zᵢ" hàng trên với ô "Zᵢ" hàng dưới và ô "Z′" hàng trên với ô "Z′" hàng dưới. Viền (liền/đứt) và nền phân biệt quan sát huấn luyện với quan sát kiểm tra, không chỉ bằng màu. `figcaption`: "Đổi vai $Z_i$ và $Z'$: cặp $(S,Z')$ thành $(S^{(i)},Z_i)$; hai cặp cùng phân bố khi $Z_1,\ldots,Z_m,Z'$ độc lập cùng phân bố $D$." | "Sơ đồ hai hàng. Hàng trên là tập huấn luyện gồm Z một đến Z m, cùng quan sát kiểm tra Z phẩy. Hàng dưới là tập huấn luyện trong đó Z i được thay bằng Z phẩy, cùng quan sát kiểm tra Z i. Hai mũi tên chéo cho thấy Z i và Z phẩy đổi vị trí giữa tập huấn luyện và quan sát kiểm tra." |

Cách dựng dữ liệu hình không có số mới trên nhãn: F2 vẽ đường cong từ công thức của Hệ quả 06.13(a) với số của Ví dụ 06.10 (cùng hàm $0{,}02/\lambda+0{,}5\lambda$ của câu ôn nhanh 3), chỉ điểm cực tiểu có nhãn số, là số của ghi chú; F3 là sơ đồ của chứng minh Định lý 06.10, Bước 2. Điều phối viên ghi cách dựng vào `review-log.md`.

## 9. Trang tổng kết

Chi tiết từng trang ở mục 6 (7-01 đến 7-08). Tóm tắt:
- **Bảng `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh` (7-01):** năm hàng: Hệ quả 06.2 (kì vọng), Mệnh đề 06.5 (kì vọng), Định lý 06.10 (kì vọng, trị tuyệt đối), Mệnh đề 06.11 (tất định), Hệ quả 06.13 (kì vọng). Ba bổ đề công cụ và hai nhận xét đọc thêm ở ghi chú diễn giả; phản ví dụ của từng giả thiết ở ghi chú diễn giả.
- **Vấn đề trung tâm (7-03):** năm câu trả lời cho cả bài: quan sát mới cho bảo đảm trực tiếp; tập huấn luyện dùng lại cần khoảng cách tổng quát hóa kì vọng; tính ổn định đều chặn khoảng cách đó; hệ số ổn định và cận $2GB/\sqrt m$ của quy tắc có chính quy hóa; loại bảo đảm (kì vọng, cấp thuật toán, giá $1/\delta^2$ của xác suất cao). Mỗi câu giữ điều kiện của nó.
- **Bài tập tổng hợp (7-04, 7-05):** Bài tập 06.4(c), hai trang (đề; lời giải trên mặt trang). Lý do chọn: ghép Mệnh đề 06.11 (hệ số ổn định tại hai hệ số), Hệ quả 06.13(a) và (c) (cận đánh đổi, $\lambda^*$), và thừa số của Bài tập 06.4(b) ở 6-06; dùng hồi quy logistic, một mô hình khác ví dụ ridge xuyên suốt.
- **Câu hỏi tự kiểm tra (7-06):** bốn câu, câu trả lời dự kiến ở ghi chú diễn giả: (1) oracle không chệch cho $L_D$ hay $L_S$; (2) bước đổi chỗ cần dạng đầy đủ của (T1); (3) $\epsilon_{\mathrm{stab}}(400)=0{,}2$ (câu hỏi cuối buổi (a)); (4) không chặn $\mathbb E\lvert L_D-L_S\rvert$ (câu hỏi cuối buổi (c)).
- **Bài tập về nhà (7-07):** bảng `Mục | Bài tập` ánh xạ mười một bài vào mạch 2–6 theo mạch cung cấp kiến thức cuối cùng; liên kết viewer.
- **Tài liệu tham khảo (7-08):** UML §14.5, §13.1 (trước buổi học); §13.2, §13.3 (sau buổi học); §13.4, §13.3.2, §12.2.1, §12.2.2 (mở rộng); dòng chữ "Bài 07: Mạng nơ-ron, năng lực mô hình và tham số hóa thừa".
- **Câu nối sang bài sau** (ghi chú diễn giả 7-08): Bài 07 hỏi đại lượng độ phức tạp nào của lớp mạng nơ-ron còn cho thông tin khi mạng khớp cả nhãn gán ngẫu nhiên.

## 10. Bảng thuật ngữ Việt–Anh của deck

Theo ghi chú và `thuat-ngu.md`; tiếng Anh trong ngoặc ở lần dùng đầu trên trang nội dung (trang ghi ở cột cuối).

| Tiếng Việt | Tiếng Anh | Lần đầu trên mặt trang |
|---|---|---|
| quan sát mới | fresh observation | 1-06 |
| hạ gradient ngẫu nhiên (SGD) | stochastic gradient descent | 1-06 (chữ viết tắt; tiếng Anh đã có ở Bài 05) |
| tối thiểu hóa rủi ro thực nghiệm (ERM) | empirical risk minimization | 2-02 (chữ viết tắt; tiếng Anh đã có ở Bài 01) |
| rủi ro vượt mức kì vọng | expected excess risk | 2-04 |
| khoảng cách tổng quát hóa kì vọng | expected generalization gap | 2-08 |
| hệ số chính quy hóa | regularization parameter | 3-02 |
| mục tiêu có chính quy hóa | regularized objective | 3-02 |
| ERM có chính quy hóa | regularized ERM | 3-02 |
| hồi quy ridge | ridge regression | 3-02 |
| tăng trưởng bậc hai | quadratic growth | 3-03 |
| tập huấn luyện lân cận | neighboring samples | 4-01 |
| quan sát thay thế | replacement observation | 4-01 |
| ổn định đều | uniformly stable (uniform stability) | 4-01 |
| hệ số ổn định | stability coefficient | 4-01 |
| quan sát kiểm tra | test observation | 4-01 |
| cấp thuật toán | algorithm-level | 4-03 |
| lập luận đổi vai | exchange argument | 4-05 |
| thuật toán hằng | constant algorithm | 4-06 |
| đánh đổi khớp–ổn định | fitting–stability trade-off | 6-01 |
| bất đẳng thức oracle | oracle inequality | 6-02 |

Chỉ ở ghi chú diễn giả (tiếng Anh trong ngoặc ở đó): chính quy hóa Tikhonov (Tikhonov regularization; "ERM có chính quy hóa (còn gọi là chính quy hóa Tikhonov)" ở ghi chú diễn giả 3-02), cấp lớp (class-level), ổn định thay một theo trung bình (on-average-replace-one stability), bài toán lồi–Lipschitz–bị chặn (convex-Lipschitz-bounded problem), nguồn ngẫu nhiên riêng (internal randomness). Đã có ở Bài 01–05, không nhắc tiếng Anh: rủi ro kì vọng, rủi ro thực nghiệm, sai số tối ưu thực nghiệm, dưới gradient, dưới vi phân, lồi mạnh, oracle gradient ngẫu nhiên, điểm lặp trung bình, hàm lỗi logistic, hàm lỗi bản lề, thuật toán ghi nhớ, thuật toán học có nguồn ngẫu nhiên riêng.

Người viết deck thêm "(còn gọi là chính quy hóa Tikhonov)" lên mặt trang 3-02 nếu mật độ cho phép (trang đang ở 58).

## 11. Rủi ro và điểm cần điều phối viên quyết định

1. **Mạch 2 gộp §1–§5** (13 trang, 32 phút). Tách thành "Hạ gradient ngẫu nhiên với quan sát mới" (§1–§4) và "Tối ưu trên một tập huấn luyện cố định" (§5) thì deck có tám mạch, vượt trần bảy. Hai chế độ lấy mẫu là một câu hỏi (hai chương trình của câu hỏi mở đầu); trang 2-07 là câu nối giữa hai nửa. Khuyến nghị giữ.
2. **Số trang 54**, vượt mục tiêu 45–52 hai trang, dưới trần 55 (lý do ở mục 3). Phương án rút còn 52, không bỏ bước nào của hành trình khái niệm: (a) bỏ 6-06 (Bài tập 06.4(b)) và để bài tập tổng hợp 7-04, 7-05 làm bài tập của cụm đánh đổi (bài tổng hợp dùng thừa số $1{,}25$ của phần (b), nên 7-05 thêm một dòng giải thích thừa số); (b) chuyển Nhận xét 06.14 (6-05) vào ghi chú diễn giả 6-04 và dòng cuối của 7-03: mất trang phân biệt kì vọng với xác suất cao (blueprint §6.2). Khuyến nghị giữ 54, hoặc chỉ (a) nếu cần 53.
3. **Kết quả không có trang ý tưởng chứng minh riêng:** Bổ đề 06.1 (công cụ, chứng minh hai bước; lộ trình ở ghi chú diễn giả 2-03); Bổ đề 06.7 (công cụ; lộ trình ở ghi chú diễn giả 3-03, kỹ thuật hiện trên mặt trang bài tập 3-05); Bổ đề 06.8 (công cụ, phác thảo; Phụ lục A ở ghi chú diễn giả); Nhận xét 06.3 (là Hệ quả 06.2 với $T=m+1$); Nhận xét 06.12, 06.15 (đọc thêm); Nhận xét 06.14 (một dòng bất đẳng thức Markov trên mặt trang). Năm kết quả chính có trang riêng: Hệ quả 06.2 (2-05), Mệnh đề 06.5 (2-10), Định lý 06.10 (4-04), Mệnh đề 06.11 (5-02), Hệ quả 06.13 (6-03).
4. **Bài tập của mạch 3: Bài tập 06.10(a), (c)** (UML Bài tập 14.1; cùng kỹ thuật với Bổ đề 06.7). Phương án khác: Bài tập 06.4(d), phần đầu (chứng minh $\lVert\hat w_1\rVert\ge\lVert\hat w_2\rVert$, $L_S(\hat w_1)\le L_S(\hat w_2)$ khi $\lambda_1<\lambda_2$, kiểm bằng Ví dụ 06.4): gần ví dụ xuyên suốt hơn nhưng chỉ dùng hai câu đầu của một phần, và phần (d) còn lại cần Hệ quả 04.17 và số hạng ổn định của mạch 6. Khuyến nghị 06.10.
5. **Bài tập của mạch 2: Bài tập 06.1(c), (d) trên một trang** (59 âm tiết). Dòng dữ kiện gom thiết lập chung; câu (d) rút "SGD đi một vòng qua mẫu theo thứ tự như Nhận xét 06.3, tức $g_t=2(w_t-Y_t)$" thành "Một vòng theo thứ tự, $g_t=2(w_t-Y_t)$" (Nhận xét 06.3 đã ở 2-07). Lời giải (d) viết gọn "cần tính độc lập đó" cho "Giả thiết được dùng là quan sát của bước $t$ độc lập với các quan sát đã dùng". Tương tự, 7-04 mở bằng dòng "Bài tập 06.4: $Q(\lambda)=\ldots$; (a) chọn $\lambda=2G/(B\sqrt m)$" thay cho đề phần (a). Đề nghị chấp nhận.
6. **"Tập huấn luyện" thay "mẫu" trên trang bài tập.** `exercises.md` còn dùng "mẫu" cho tập huấn luyện (Bài tập 06.1(b), (d), 06.2(b1): "liệt kê bốn mẫu"; điểm đang mở cho tác giả trong `lec-06/review-log.md`). Deck theo thuật ngữ của ghi chú bản hiện hành: "bốn tập huấn luyện", "tập huấn luyện lưu lại"; "tập huấn luyện lân cận" giữ nguyên vì là thuật ngữ của Định nghĩa 06.9. Đề nghị chấp nhận; nếu điều phối viên muốn giữ nguyên văn `exercises.md`, ba chỗ ở 2-12 và 4-07 đổi lại.
7. **Câu hỏi thực hành của khối ứng dụng §3** có hai vế. Trang 2-02 chỉ hỏi vế (i) (một vòng SGD), vì vế (ii) dùng "ERM có chính quy hóa" trước Định nghĩa 06.6; vế (ii) nêu ở ghi chú diễn giả 2-02 và được trả lời trên 6-04.
8. **Ví dụ 06.1 trên 2-02** (mạch 2, đúng §3), dùng lại ở mạch 3 và 5. Đặt ở 3-01 thì mạch 3 ứng với §3 và §6, không liên tiếp (lỗi cổng duyệt Bài 05, T13).
9. **Hình 06.1 dùng lại** (tệp chung với ghi chú). Hai điểm: (a) chú giải và `<desc>` trong SVG ghi "mẫu S", "mẫu S⁽⁴⁾", khác "tập huấn luyện" của ghi chú (điểm đang mở cho tác giả); (b) ở khung phải, nét đứt $F_{S^{(4)},4}$ vượt mép trên $2{,}5$ khi $w>0{,}8345$ và bị cắt (bài học "trục hình chứa hết dữ liệu"). Hai điểm cực tiểu và hai nhãn khoảng cách nằm trong khung. Phương án: (i) dùng nguyên tệp, `figcaption` và alt của deck viết "tập huấn luyện", ghi đề xuất sửa SVG cho tác giả (mục 13); (ii) người viết deck làm bản sao riêng `ridge-thay-mot-quan-sat-deck.svg` với chú giải "tập huấn luyện S", "tập huấn luyện S⁽⁴⁾" và trục tung khung phải đến $3{,}5$; bản sao lệch hình của ghi chú. Khuyến nghị (i).
10. **Hình F3 mới** (sơ đồ đổi vai, không có số) trên 4-02. Nếu điều phối viên không duyệt, 4-02 vẫn đứng được bằng chữ và công thức; ghi chú diễn giả tả sơ đồ.
11. **Hình F2 mới** trên 6-04 (đường cong từ công thức của Hệ quả 06.13(a), số của Ví dụ 06.10). Trang có chữ ($51$ âm tiết) và hình: người viết deck kiểm 1600×900 với `footer_check.py`; nếu chạm chân trang, chuyển dòng "Diễn giải:" vào ghi chú diễn giả.
12. **Thứ tự trong §7 và §9:** đẳng thức thay một và đoạn thuật toán ghi nhớ (sau Định lý 06.10 trong ghi chú) đặt ở trang trực quan 4-02, trước phát biểu; Ví dụ 06.12 (sau Hệ quả 06.13 trong ghi chú) đặt ở 6-01, trước phát biểu. Cả hai không cần kết quả để tính (tiền lệ T5 của cổng Bài 04); vẫn trong cùng mục, nên mạch vẫn ứng với các mục liên tiếp. Đề nghị chấp nhận và ghi vào `review-log.md`.
13. **Mục tiêu (1-03)** giữ đủ năm mục tiêu của ghi chú theo thứ tự, rút câu chữ trong trần 80 (đếm $79$): mục tiêu 1 viết "cận với quan sát mới" cho "suy ra cận rủi ro vượt mức kì vọng khi dùng quan sát mới", không nêu "hai cách lấy mẫu"; mục tiêu 3 bỏ "Định nghĩa"; mục tiêu 4 bỏ "chứng minh"; mục tiêu 5 không liệt kê ba giả thiết. Ghi chú diễn giả nêu đủ các ý đã rút. Nếu điều phối viên muốn giữ "Định nghĩa" ở mục tiêu 3, cần rút một chỗ khác (mục tiêu 2 đang $20$ âm tiết, đúng trần dòng).
14. **Luận điểm bìa** $57$ âm tiết (Bài 05: $52$; Bài 01: $63$, ngoại lệ đã ghi). Bản ngắn hơn, $42$ âm tiết, mất tên "khoảng cách tổng quát hóa kì vọng": "Với quan sát mới, hạ gradient ngẫu nhiên có cận trực tiếp cho rủi ro kì vọng. Với tập huấn luyện dùng lại, cần thêm tính ổn định; chính quy hóa cho tính ổn định đó khi hàm lỗi lồi và Lipschitz." Điều phối viên chọn.
15. **Công thức cần đo ở 390 px** (ngắt `aligned` chỉ khi tràn): 1-02 (định nghĩa lồi mạnh), 2-09 (đẳng thức ba ngoặc vuông; gần như chắc chắn cần ngắt), 2-09 dòng (b), 4-01, 4-02 (đẳng thức thay một), 4-03, 5-02 Bước 2, 6-01, 6-02 (b), 7-03; bảng 2-11, 3-04, 5-04, 7-01, 7-07 đặt trong `.table-scroll`.
16. **Trang sát trần** (đếm bằng script, mục 15): 1-03 ($79$/80), 7-01 ($77$/80); 3-03, 2-11, 2-12, 5-02, 7-04 ($59$); 2-07, 2-08, 3-02, 4-02, 4-05, 6-03, 6-05 ($58$); 1-06, 4-04, 4-06 ($57$). Người viết deck không thêm chữ trên các trang này; điều phối viên đếm lại trên deck. Trung vị $54$ trên 42 trang nội dung, 11 trang ≤ 50: không đạt mục tiêu "phần lớn trang 40–50" của bản giao việc. Lý do: các trang kết quả giữ đủ bốn đến năm thành phần giả thiết của ghi chú (Hệ quả 06.2, Mệnh đề 06.5, Định lý 06.10, Mệnh đề 06.11, Hệ quả 06.13), tiếng Anh ở lần dùng đầu (năm thuật ngữ trên 4-01), và số viết trong câu có tính. Biên sửa còn lại $1$–$3$ âm tiết ở 15 trang; khi cổng duyệt yêu cầu thêm chữ, cắt bù trên cùng trang hoặc chuyển dòng "Diễn giải:"/"Ví dụ." vào ghi chú diễn giả.
17. **Ghi chú diễn giả dẫn bài sau** ở 4-05 (kỹ thuật trở lại khi chặn khoảng cách tổng quát hóa của hạ gradient ngẫu nhiên nhiều vòng, không nêu số bài) và 7-08 (Bài 07): chỉ trong ghi chú diễn giả.
18. **"Chế độ A", "Chế độ B"** viết thường trên 2-01, 2-12, không thành nhãn in đậm (không có trong danh sách nhãn hợp lệ).
19. **Kí hiệu $\mathcal F_{t-1}$** được nhắc lại ở 2-03 cho chế độ A ($\sigma(Z_1,\ldots,Z_{t-1})$); ở 2-07 và 2-12 dùng cho chế độ B theo nghĩa lịch sử các lần rút chỉ số, như §5 của ghi chú và Bài tập 06.1(b). Ghi chú diễn giả 2-07 nói rõ.

## 12. Bảng đối chiếu trang → mục và khối của ghi chú

Cột "Đưa vào" ghi kí hiệu, thuật ngữ hoặc kết quả xuất hiện lần đầu trên mặt trang (định nghĩa hoặc "Nhắc lại:"/"Kí hiệu:"), để kiểm quy tắc định nghĩa trước khi dùng.

| Trang | Mục ghi chú | Khối (số của ghi chú) | Đưa vào |
|---|---|---|---|
| 1-01 | đoạn mở đầu; §10 | — (bằng lời) | — |
| 1-02 | Kiến thức tiên quyết; Câu hỏi ôn nhanh | Hệ quả 05.15, 05.19; Định nghĩa 04.2, 05.4, 05.6, 05.18; Mệnh đề 01.7 (nhắc lại) | (C), (G1), (G2), $F$, $\eta$, $R$, $G$, $T$, $u$, $W$, $w_1$, $\bar w_T$, $\operatorname{opt}_S$, $L_S$, $L_D$, $h$, $A(S;\xi)$, $\xi$, $\lambda$-lồi mạnh, $G$-Lipschitz, $B$, $C_x$, $C_y$ |
| 1-03 | Mục tiêu học tập | — | — |
| 1-04 | toàn bài; §13 | — | — |
| 1-05 | đoạn mở đầu | — | — |
| 1-06 | Câu hỏi mở đầu và hai đoạn sau | — | $X$, $Y$, $D$, $\ell$, $\operatorname{proj}_W$, $y_t$, $m$, quan sát mới, SGD |
| 2-00 | §1–§5 | — | — |
| 2-01 | §1, §2 | bảy thành phần; (T1), (T2) | $z=(x,y)$, $\mathcal Z$, $p$, chế độ A, chế độ B, $Z_1,Z_2,\ldots$, $S\sim D^m$, (T1), điểm so sánh |
| 2-02 | §3 | Ví dụ 06.1; khối ứng dụng | $z_1,\ldots,z_4$, ERM, hàm lỗi logistic (Bài 05) |
| 2-03 | §4 | Bổ đề 06.1 | kì vọng có điều kiện theo lịch sử (nhắc lại trên mặt trang), $\mathcal F_{t-1}$, $v(w,z)$, $\psi$, $\partial$ |
| 2-04 | §4 | Hệ quả 06.2 và hai đoạn sau | Thuật toán 05.11 (tên), $\xi_t$, $\varphi$, rủi ro vượt mức kì vọng, $\epsilon$ |
| 2-05 | §4 | chứng minh Hệ quả 06.2 | oracle (Định nghĩa 05.10, ghi chú diễn giả) |
| 2-06 | §4; Phụ lục D | Ví dụ 06.2 | $c_t$ |
| 2-07 | §4, §5 | Nhận xét 06.3; đoạn mở §5; Ví dụ 06.3 Bước 1 | $g_t$, $\bar Y$, $L_S'$, $L_D'$ |
| 2-08 | §5 | Định nghĩa 06.4 và ba đoạn sau | khoảng cách tổng quát hóa kì vọng, $A_{\mathrm{gn}}$ (Ví dụ 01.8) |
| 2-09 | §5 | Mệnh đề 06.5 | $\tilde w$, dạng yếu của (T1) |
| 2-10 | §5 | chứng minh Mệnh đề 06.5 | Mệnh đề 04.3 (tên) |
| 2-11 | §5; Phụ lục D | Ví dụ 06.3; đoạn cuối §5 | $Y_i$, $i_t$ |
| 2-12 | Bài tập 06.1 | Bài tập 06.1(c), (d) | độ chệch |
| 3-00 | §6 | — | — |
| 3-01 | §6 | đoạn mở §6 | $z'$ (dùng trong ví dụ) |
| 3-02 | §6 | Định nghĩa 06.6 và ba đoạn sau | $s$, $\lambda$, $F_{s,\lambda}$, $\hat w_s$, $\hat w_S$, ERM có chính quy hóa, hồi quy ridge |
| 3-03 | §6 | Bổ đề 06.7, 06.8 | $f$, tăng trưởng bậc hai |
| 3-04 | §6 | Ví dụ 06.4, Hình 06.1 | $S^{(4)}$ |
| 3-05 | Bài tập 06.10 | Bài tập 06.10(a), (c) | $w_\alpha$, $\alpha$ |
| 4-00 | §7 | — | — |
| 4-01 | §7 | Định nghĩa 06.9 và ba đoạn sau | $s^{(i)}$, $i$, tập huấn luyện lân cận, quan sát thay thế, quan sát kiểm tra, $\epsilon_{\mathrm{stab}}(m)$, ổn định đều |
| 4-02 | §7 | đoạn trước Định lý 06.10; đẳng thức sau chứng minh; đoạn thuật toán ghi nhớ | $Z'$, $S^{(i)}$ |
| 4-03 | §7 | Định lý 06.10 | dạng đầy đủ của (T1), cấp thuật toán |
| 4-04 | §7 | chứng minh Định lý 06.10 | — |
| 4-05 | §7; Phụ lục E | lập luận đổi vai; đẳng thức sau chứng minh | $\Phi$, đối xứng hóa và tập mẫu ảo (nhắc lại), trung bình thay một |
| 4-06 | §7 | Ví dụ 06.5 | thuật toán hằng, $h_0$ |
| 4-07 | Bài tập 06.2 | Bài tập 06.2(b) | $\bar z$, $a$, $b$ (cục bộ) |
| 5-00 | §8 | — | — |
| 5-01 | §2 (L), §8 | Mệnh đề 06.11 | (L) (nhắc lại) |
| 5-02 | §8; Phụ lục B | chứng minh Mệnh đề 06.11 | $\hat w$, $\hat w'$ |
| 5-03 | §8 | Ví dụ 06.6, 06.8 | $\bar z$ (Ví dụ 06.8) |
| 5-04 | §8 | Ví dụ 06.7, 06.9 | $M$, $S^{(100)}$ |
| 5-05 | Bài tập 06.6 | Bài tập 06.6(a) | — |
| 6-00 | §9 | — | — |
| 6-01 | §9 | đoạn mở §9; Ví dụ 06.12 | đánh đổi khớp–ổn định |
| 6-02 | §9 | Hệ quả 06.13 và đoạn sau | $w_0$, $W_B$, $\lambda^*$, số hạng ổn định, số hạng khớp, bất đẳng thức oracle |
| 6-03 | §9; Phụ lục C | chứng minh Hệ quả 06.13 | cân hai số hạng (nhắc lại), $a$, $b$ |
| 6-04 | §9 | Ví dụ 06.10, 06.11 | — |
| 6-05 | §9 | Nhận xét 06.14; Nhận xét 06.15 (ghi chú diễn giả) | bất đẳng thức Markov (nhắc lại), $\delta$, $V$, $\alpha$ |
| 6-06 | Bài tập 06.4 | Bài tập 06.4(b) | $Q(\lambda)$, $c$ |
| 7-00 | §10–§13 | — | — |
| 7-01 | §4, §5, §10 | Hệ quả 06.2, Mệnh đề 06.5 | — |
| 7-02 | §7–§10 | Định lý 06.10, Mệnh đề 06.11, Hệ quả 06.13 | — |
| 7-03 | §10 | — | — |
| 7-04 | Bài tập 06.4 | Bài tập 06.4(c) (đề) | $B_0$ |
| 7-05 | Bài tập 06.4 | Bài tập 06.4(c) (lời giải) | $\lambda_0$ |
| 7-06 | Câu hỏi mở đầu, §7, §12 | câu hỏi cuối buổi (a), (c) | — |
| 7-07 | §11 | `exercises.md` | — |
| 7-08 | §12, §13 | — | — |

## 13. Đề xuất sửa ghi chú và tệp bài tập (không sửa; chờ điều phối viên và tác giả)

Không thấy lỗi toán học trong các khối deck dùng; mọi con số của ví dụ và bảy bài tập trên mặt trang đã tính lại (mục 5) và khớp ghi chú, tệp bài tập.

| Mức độ | Vị trí | Vấn đề | Bằng chứng | Đề xuất |
|---|---|---|---|---|
| nhẹ | `img/lec-06/ridge-thay-mot-quan-sat.svg`, chú giải và `<desc>` | Chữ "mẫu S", "mẫu S⁽⁴⁾", "mẫu thay quan sát thứ tư", khác "tập huấn luyện" của ghi chú (alt dòng 647, chú thích dòng 649); điểm đã mở cho tác giả trong `lec-06/review-log.md` | SVG dòng 3, 63, 66 | "tập huấn luyện S", "tập huấn luyện S⁽⁴⁾"; `<desc>` theo alt của ghi chú |
| nhẹ | cùng tệp, khung phải ($\lambda=4$) | Trục tung đến $2{,}5$; nét đứt $F_{S^{(4)},4}(w)=2{,}8125w^2-0{,}25w+0{,}75$ vượt $2{,}5$ khi $w>0{,}8345$ (bằng $3{,}3125$ tại $w=1$) và bị cắt ở mép trên | `num.py`; clipPath `clip4` cao $210$ px, $84$ px một đơn vị | Trục tung khung phải đến $3{,}5$, hoặc ghi trong chú thích rằng hai đường bị cắt ở mép trên |
| nhẹ | `exercises.md`, Bài tập 06.1(b), (d), 06.2(b1), (c) | "mẫu" cho tập huấn luyện ("liệt kê bốn mẫu", "SGD đi một vòng qua mẫu"); điểm đã mở cho tác giả | `exercises.md` dòng 31, 35, 123 | "tập huấn luyện"; deck đã viết theo ghi chú (mục 11, điểm 6) |

## 14. Danh sách kỹ thuật đã giới thiệu đến hết Bài 06

| Kỹ thuật | Bài, trang (lần đầu) | Dạng | Trong deck Bài 06 |
|---|---|---|---|
| Tính tuyến tính của kì vọng | Bài 01, `L01-3-03` | một dòng | dùng không nhắc tên (2-06, 2-11) |
| Bất đẳng thức hợp | Bài 01, `L01-4-04` | trang riêng | không dùng |
| Chặn xác suất bỏ sót $(1-\epsilon)^m\le e^{-\epsilon m}$ | Bài 01, `L01-6-07` | trang riêng | không dùng |
| Tối thiểu hóa từng điểm rồi lấy kì vọng | Bài 01 | một dòng | không dùng |
| Phương pháp Chernoff | Bài 02, `L02-3-01` | trang riêng | không dùng (chỉ bất đẳng thức Markov, nhắc lại ở 6-05) |
| Dây cung của hàm lồi và Taylor bậc hai tại $0$ | Bài 02 | một dòng | không dùng |
| Đảo cận đuôi thành bán kính và cỡ mẫu | Bài 02, `L02-4-04` | trang riêng | không dùng (đảo $2GB/\sqrt m\le\epsilon$ thành cỡ mẫu ở 6-02 là phép tính một dòng) |
| Chia xác suất thất bại $\delta/K$ cho từng giả thuyết | Bài 02, `L02-5-05` | trang riêng | không dùng (bước chọn bằng tập xác thực của Nhận xét 06.14 ở ghi chú diễn giả 6-05) |
| Bước tất định trên biến cố đại diện | Bài 02, `L02-5-11` | trang riêng | không dùng |
| Cận dưới và cận trên cho chiều VC | Bài 03, `L03-2-04` | trang riêng | không dùng |
| Thứ tự trên đường thẳng cho cận trên | Bài 03 | một dòng | không dùng |
| Hàm afin giữ tổ hợp lồi (với phân hoạch Radon) | Bài 03 | một dòng | không dùng |
| Tách theo nhãn của điểm cuối rồi quy nạp | Bài 03 | một dòng | không dùng |
| Đối xứng hóa và tập mẫu ảo | Bài 03, `L03-5-06` | trang riêng | nhắc lại một dòng ở 4-05 để so với lập luận đổi vai |
| Hàm tăng trưởng thay cho số giả thuyết | Bài 03, `L03-5-07` | trang riêng | không dùng |
| Bất đẳng thức tiếp tuyến $\ln u\le u/u_0+\ln u_0-1$ để giải cỡ mẫu | Bài 03 | một dòng (ghi chú diễn giả) | không dùng |
| Thêm bớt kì vọng rồi bình phương; mỗi số hạng chéo một lý do | Bài 04, 3-03 | một dòng | gần với khai triển $\mathbb E\bar w_T^2$ ở 2-06, 2-11 (tích chéo có kì vọng $0$ hoặc $\tfrac1m$), không nhắc tên |
| Chia xác suất thất bại theo trọng số | Bài 04, 4-04 | trang riêng | không dùng |
| Chọn $\delta=1/m$ để bỏ $\delta$ khỏi đầu vào | Bài 04, 5-03 | một dòng | không dùng |
| Lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện | Bài 04, 6-02 | một dòng | gần với Bước 4 của 4-04 (cố định $(S,Z')$, lấy kì vọng theo $\xi$ trước, Fubini), không nhắc tên |
| Kì vọng có điều kiện theo lịch sử | Bài 05, 3-07 | trang riêng | **nhắc lại một dòng ở 2-03**; dùng ở 2-07, 2-12 |
| Tổng triệt tiêu và trung bình các điểm lặp | Bài 05, 4-05 | trang riêng | nằm trong Hệ quả 05.15; nêu tên ở ghi chú diễn giả 2-05 |
| Cân hai số hạng, $a/\eta+b\eta\ge2\sqrt{ab}$ | Bài 05, 4-08 | một dòng | **nhắc lại một dòng ở 6-03** (Bước 5, với $\lambda$); dùng ở 6-06, 7-05 |
| Số hạng chéo bằng $0$ cho véc-tơ không tương quan | Bài 05, 6-04 | một dòng | dùng không nhắc tên ở 2-06 ($\mathbb E[y_ty_s]=0$) |
| **Lập luận đổi vai** (thay một điểm; thêm một quan sát mới $Z'$, đổi chỗ với $Z_i$) | **Bài 06, 4-05** | **trang riêng** | dùng ở 4-02, 4-04, 4-07; dùng lại ở Bài 08 (ghi chú Bài 08 dẫn Định lý 06.10, Định nghĩa 06.9) |
| Cộng hai bất đẳng thức tăng trưởng bậc hai đối xứng (một phía cho hằng số gấp đôi) | Bài 06, 5-02 | một dòng | — |
| Điểm trên đoạn thẳng rồi cho dần về đầu mút (chia cho $\alpha$, $\alpha\to0^+$) | Bài 06, ghi chú diễn giả 3-03; mặt trang bài tập 3-05 | một dòng | — |

Deck Bài 07 trở đi nhắc lại "lập luận đổi vai" bằng tên, một dòng "Nhắc lại:".

## 15. Mật độ mặt trang đo bằng script

Bản deck sau khi sửa theo năm báo cáo duyệt (2026-11-16; bảng đếm cũ của bản đóng băng thay bằng bảng này), đếm theo đúng quy ước của `deck_lint.py` đã cập nhật: token có chữ cái hoặc chữ số, KaTeX không tính, số trong câu có tính, chữ trong ô bảng có tính, số trong bảng không tính; ghi chú diễn giả không tính dòng nguồn (script: thư mục nháp `lec-06/writer/counts.py`). Bảng này thay bảng đếm trên văn bản dự kiến của storyboard. `deck_lint.py`: 0 phát hiện trên 55 trang.

| Trang | Mặt trang | Ghi chú diễn giả | Trang | Mặt trang | Ghi chú diễn giả |
|---|---:|---:|---|---:|---:|
| 1-01 | 75 | 135 | 4-03 | 55 | 107 |
| 1-02 | 58 | 113 | 4-04 | 58 | 181 |
| 1-03 | 78 | 123 | 4-05 | 60 | 145 |
| 1-04 | 45 | 97 | 4-06 | 55 | 74 |
| 1-05 | 27 | 115 | 4-07 | 60 | 92 |
| 1-06 | 57 | 126 | 5-00 | 36 | 88 |
| 2-00 | 46 | 95 | 5-01 | 58 | 129 |
| 2-01 | 59 | 109 | 5-02 | 60 | 173 |
| 2-02 | 60 | 143 | 5-03 | 34 | 110 |
| 2-03 | 59 | 108 | 5-04 | 48 | 119 |
| 2-04 | 56 | 104 | 5-05 | 47 | 74 |
| 2-05 | 52 | 151 | 6-00 | 38 | 89 |
| 2-06 | 43 | 57 | 6-01 | 54 | 107 |
| 2-07 | 49 | 92 | 6-02 | 49 | 111 |
| 2-08 | 56 | 105 | 6-03 | 48 | 114 |
| 2-09 | 51 | 136 | 6-04 | 56 | 150 |
| 2-10 | 49 | 122 | 6-05 | 59 | 102 |
| 2-11 | 54 | 103 | 6-06 | 33 | 86 |
| 2-12 | 59 | 115 | 7-00 | 25 | 127 |
| 3-00 | 32 | 97 | 7-01 | 42 | 74 |
| 3-01 | 58 | 112 | 7-02 | 70 | 124 |
| 3-02 | 58 | 88 | 7-03 | 58 | 146 |
| 3-03 | 53 | 146 | 7-04 | 57 | 77 |
| 3-04 | 26 | 113 | 7-05 | 30 | 65 |
| 3-05 | 47 | 95 | 7-06 | 48 | 115 |
| 4-00 | 34 | 89 | 7-07 | 47 | 130 |
| 4-01 | 58 | 120 | 7-08 | 44 | 140 |
| 4-02 | 58 | 146 |  |  |  |

Trần: 60 cho trang nội dung; 80 cho 1-03, 1-04, 7-01, 7-02, 7-07; bìa không tính. Không trang nào vượt trần (`deck_lint.py`: 0). Sau khi sửa theo năm báo cáo duyệt, trung vị trên 42 trang nội dung là $55$–$56$ (bản đóng băng: $49$); 14 trang ≤ 50; các trang 57–60: 1-02, 1-06, 2-01, 2-02, 2-03, 2-12, 3-01, 3-02, 4-01, 4-02, 4-04, 4-05, 4-07, 5-01, 5-02, 6-05, 7-03, 7-04. Lý do tăng: các "Nhắc lại:", câu nối, giả thiết và tiếng Anh mà người duyệt yêu cầu; phần cắt bù đã dồn văn xuôi sang ghi chú diễn giả đến khi mỗi trang ≤ 60. Ghi chú diễn giả: mọi trang ≤ 150; trang ý tưởng chứng minh, bài tập ≤ 250.

## 16. Đối chiếu với bản deck (người viết deck, 2026-11-16)

Tệp: `2627-1/lecture-06-on-dinh-chinh-quy-hoa.html`, 55 trang. Câu chữ trên mặt trang và ghi chú diễn giả của deck là bản chuẩn; văn bản dự kiến ở mục 6 giữ để đối chiếu. Mọi "yêu cầu sửa" và phát hiện nhẹ của cổng duyệt (quyết định của điều phối viên trong `review-log.md`) đã áp dụng như sau.

| Chỗ lệch | Trang | Nội dung trong deck | Lý do |
|---|---|---|---|
| Luận điểm bìa | 1-01 | Một câu, có điều kiện lồi, theo đề xuất N1 ("Với hàm lỗi lồi, cận của hạ gradient ngẫu nhiên trên quan sát mới chặn thẳng rủi ro vượt mức kì vọng; trên tập huấn luyện lưu lại, khi hàm lỗi thêm Lipschitz, …"); "dùng lại" đổi thành "lưu lại" | N1; L6 (một tên cho chế độ B) |
| Hộp vấn đề trung tâm | 1-05 | Câu hỏi đầy đủ của ghi chú (27 âm tiết) | L19 |
| Tiên quyết | 1-02 | Bỏ câu "Hệ quả 05.19 chặn …" (chuyển vào ghi chú diễn giả); "(đoạn sau Định nghĩa 05.4)" cho $G=2(BC_x+C_y)C_x$ | mật độ; đúng chỗ của ghi chú Bài 05 |
| Mục tiêu | 1-03 | Giữ động từ đầu mỗi mục và "trị tuyệt đối"; bỏ "của hồi quy ridge, logistic" và danh sách ba giả thiết (ghi chú diễn giả nêu) | L11, mục 4 điểm 13 của cổng |
| (T2) trên mặt trang | 2-01 | Dòng "$\ell(w,z)$ lồi theo $w$ và thỏa (T2): …"; (T1) giải nghĩa ở ghi chú diễn giả | T5 |
| Ví dụ 06.1 và một triệu hồ sơ | 2-02 | Danh sách một cột thay hai thẻ; tiêu đề rút thành "Ví dụ: bốn quan sát và một triệu hồ sơ"; tiếng Anh đầy đủ "(empirical risk minimization, ERM)"; câu hỏi có đối tượng so sánh | hai thẻ tràn khung 1600×900 ở cỡ chữ KaTeX của theme; L3, L10 |
| Bổ đề 06.1 | 2-03 | Đủ giả thiết ($\ell\ge0$, $\ell(w,\cdot)$ đo được, khả tích tại $w$); "Nhắc lại:" $\mathcal F_{t-1}=\sigma(\xi_1,\ldots,\xi_{t-1})$, chế độ A $\xi_t=Z_t$; "Trực quan." bằng lời, đứng trước bổ đề | T1, L14 |
| Hệ quả 06.2 | 2-04 | Bảo đảm dạng `ol type="a"`, có "cấp thuật toán (algorithm-level)" | T4; giảm chiều cao |
| Bước chứng minh | 2-05, 2-10, 4-04, 5-02, 6-03 | `<ol>`, giả thiết trong ngoặc đầu mục, không nhãn in đậm "Bước k" | T2 |
| Nhận xét 06.3 | 2-07 | Tách hai dòng (vòng thứ hai; rút chỉ số với $\xi_t=i_t$, $g_t=v(w_t,Z_{i_t})$); dòng "Hiệu $-2\bar Y$ … $0{,}375$" chuyển vào ghi chú diễn giả | T12, T11 |
| Định nghĩa 06.4 | 2-08 | "Nhắc lại:" Mệnh đề 01.7; "Một số có dấu …" chuyển vào ghi chú diễn giả | T11 |
| Mệnh đề 06.5 | 2-09 | (T2) thay cho liệt kê lại; đẳng thức (a) ngắt `aligned` hai dòng (tràn ngang ở 1600×900); (b) viết nội dòng | đo trong trình duyệt; mật độ |
| Ví dụ 06.3 | 2-11 | Tiêu đề rút "Ví dụ: chương trình chạy nhiều vòng"; công thức $\mathbb E\bar w_T^2$ đầy đủ chuyển vào ghi chú diễn giả; câu nối "cần một cận theo tính chất của thuật toán" gộp vào "Diễn giải:" | tiêu đề hai dòng và tràn chân trang; câu nối vẫn trên mặt trang |
| Bài tập 06.1 | 2-12 | Nhãn "Bài tập 06.1."; lời giải (c) gộp độ chệch vào một đoạn | chạm chân trang |
| Định nghĩa 06.6 | 3-01, 3-02 | Ví dụ nghiệm không duy nhất khi $\lambda=0$ chuyển sang 3-01; 3-02 có "(regularized ERM; còn gọi là chính quy hóa Tikhonov, Tikhonov regularization)" và $\hat w_s\in\arg\min_{w\in W}F_{s,\lambda}(w)$ | T11, L13 |
| Bổ đề 06.7, 06.8 | 3-03 | "Trực quan." nêu cơ chế (không giảm bậc nhất theo hướng vào $W$, độ cong cộng thêm); Bổ đề 06.8 gộp ba phần | T11 |
| Ví dụ 06.4, Hình 06.1 | 3-04 | Một dòng thiết lập; bảng và "Diễn giải:" cột trái, Hình 06.1 cột phải (tệp của ghi chú, không sửa), chú thích ngắn; cột "khoảng cách" thay tiêu đề công thức | tràn khung; L2 |
| Bài tập 06.10 | 3-05 | Lời giải (a) một đoạn; nguồn UML Bài tập 14.1 chỉ ở dòng nguồn | chạm chân trang; câu nguồn gốc không vào ghi chú diễn giả |
| Định nghĩa 06.9 | 4-01 | Có "các kì vọng hữu hạn" | L5 |
| Trực quan đổi vai | 4-02 | Tiêu đề "Đổi vai quan sát huấn luyện và quan sát mới"; chỉ cơ chế bằng lời, hình F3 và ví dụ thuật toán ghi nhớ; không có đẳng thức thay một, không có "$\le\epsilon_{\mathrm{stab}}$" | N2, L8 |
| Định lý 06.10 | 4-03 | "Cấp thuật toán: phụ thuộc $m$ chỉ qua $\epsilon_{\mathrm{stab}}(m)$" (không tiếng Anh lần hai); "bất kể kích thước của lớp giả thuyết" vào ghi chú diễn giả | T4; mật độ |
| Trang kỹ thuật | 4-05 | Tiêu đề "Lập luận đổi vai"; $\Phi$ thay $\phi$; đẳng thức thay một (trung bình thay một) đặt ở đây, sau chứng minh, kèm điều kiện "$A$ ổn định đều, $\mathbb EL_D<\infty$"; bỏ "Cần (T1) dạng đầy đủ"; "Nhắc lại:" tập mẫu ảo một dòng | N2, T3, L7, T11 |
| Ví dụ 06.5 | 4-06 | Nhãn "Ví dụ 06.5."; bỏ "với mọi tập huấn luyện" ở dòng đầu (dòng hai nói lại) | mật độ |
| Bài tập 06.2(b) | 4-07 | Nhãn "Bài tập 06.2."; $A(s)=\bar z$, trung bình của $s$; lời giải (b2) có $\lvert a-b\rvert\in\{0,1/m\}$ trước khi chặn tích; liệt kê $L_D$, $L_S$ của bốn tập huấn luyện chuyển vào ghi chú diễn giả | L4; chạm chân trang |
| Mệnh đề 06.11 | 5-01 | Như storyboard; Nhận xét 06.12 (đọc thêm) ở ghi chú diễn giả | — |
| Ý tưởng chứng minh Mệnh đề 06.11 | 5-02 | Tiêu đề "Ý tưởng chứng minh: Mệnh đề 06.11"; kí hiệu $\hat w$, $\hat w'$ đặt trong bước 1 | tiêu đề hai dòng đẩy nội dung chạm chân trang |
| Ví dụ 06.6, 06.8 | 5-03 | Danh sách một cột thay hai thẻ; tiêu đề "Ví dụ: kiểm tra và độ chặt của cận ổn định" | hai thẻ tràn khung 135 px |
| Ví dụ 06.7, 06.9 | 5-04 | Danh sách một cột; bảng $\lambda=0{,}1$ viết thành dãy số trong một dòng | hai thẻ và bảng tràn khung |
| Bài tập 06.6(a) | 5-05 | Nhãn "Bài tập 06.6."; "Lập lại Ví dụ 06.4 với $\lambda=2$" (bỏ "Bước 2–3" vì các bước không đánh số trên trang 3-04) | trang nguồn phải ghi số được dẫn |
| Ví dụ 06.12 | 6-01 | Nhãn "Ví dụ 06.12."; tên Ví dụ 06.7, 06.4 ở dòng "Trực quan." chuyển vào ghi chú diễn giả | mật độ |
| Hệ quả 06.13 | 6-02 | $\lambda=\lambda^*$ ở (c); ba phần viết nội dòng với phân số dạng $/$ | L16; tràn khung |
| Ví dụ 06.10, 06.11 | 6-04 | "Diễn giải:" giữ "theo các cận"; "hai cận cùng bậc $GB/\sqrt m$" và $T\ge1600$ vào ghi chú diễn giả; chú thích hình F2 ngắn | T6; chạm chân trang |
| Nhận xét 06.14 | 6-05 | Nhãn "Nhận xét 06.14."; Markov với $t$; "Hệ quả 06.13(c), $W$ quả cầu bán kính $B$"; Bài tập 06.7 vào ghi chú diễn giả | T7, L7, mật độ |
| Bài tập 06.4(b) | 6-06 | Nhãn "Bài tập 06.4." (7-05 dẫn "phần (b)") | trang nguồn ghi số |
| Bảng tổng kết | 7-01, 7-02 | Tách hai trang (3 hàng + 2 hàng), mỗi hàng giữ loại bảo đảm và đại lượng được chặn; thêm "$\xi$ độc lập với $S$" ở Mệnh đề 06.5, Định lý 06.10; "không âm" ở Mệnh đề 06.11 | bảng năm hàng cao 1022 px ở 1600×900 (tràn 140–380 px dù đã rút câu chữ); không bảng nào dưới cỡ chữ tối thiểu nên không thu nhỏ chữ |
| Vấn đề trung tâm | 7-03 | Dòng mở trả lời bằng lời ("Tối ưu là học khi …; theo kì vọng:"); dòng cuối "Các cận cần hàm lỗi lồi theo tham số; mạng nơ-ron cần lập luận mới."; giá $1/\delta^2$ của Markov ở ghi chú diễn giả (đã có trên 6-05) | T8; trần 60 |
| Bài tập tổng hợp | 7-04, 7-05 | Đề gộp hai dòng; "Tính $\epsilon_{\mathrm{stab}}$ …" | trần 60 |
| Tài liệu tham khảo | 7-08 | Sách UML ở đầu danh sách; ghi chú diễn giả theo câu của ghi chú về $8\rho^2$/$4G^2$ (khác biệt do lập luận đối xứng) | L18, T10 |
| Ghi chú diễn giả | mọi trang | Không "Mạch này", "mạch N", "thẻ trái/phải", câu nói về mặt trang | T9, L12 |

**Số trang 55** (trần), một trang hơn storyboard: bảng tổng kết tách hai trang (lý do ở hàng "Bảng tổng kết"). Thời lượng không đổi: 7-01 và 7-02 chia 1,5 phút của bảng cũ.

**Hình.** `img/lec-06/danh-doi-khop-on-dinh.svg` (F2, 760×440) và `img/lec-06/doi-vai.svg` (F3, 600×290) vẽ bằng script `lec-06/writer/figs.py` trong thư mục nháp, theo mục 8: F2 ba đường $0{,}02/\lambda$ (nét đứt), $0{,}5\lambda$ (nét chấm), tổng (nét liền đậm), chấm và nhãn "λ* = 0,2: 0,2"; F3 hai hàng, ô kiểm tra viền đứt nền xám, nhãn "huấn luyện", "kiểm tra", hai mũi tên chéo. Chú thích F3 trong deck: "Hai cặp $(S,Z')$ và $(S^{(i)},Z_i)$ cùng phân bố khi $Z_1,\ldots,Z_m,Z'$ độc lập cùng phân bố $D$." Hình 06.1 dùng nguyên tệp của ghi chú (chú giải "mẫu S" vẫn chờ tác giả, mục 13).

**Kiểm tra máy (2026-11-16).** `deck_check.py`: slides=55, console=0, pageerrors=0, failed=0, không `.katex-error`, không OVERFLOW thật (chỉ đuôi SVG của `\sqrt`); `footer_check.py`: 0 trang; `deck_lint.py` (bản đã cập nhật, chữ trong bảng có tính): 0 phát hiện. Ảnh 1600×900 và 390×844 (kể cả `-end`) đã xem: `scratchpad/lec-06/writer/check5/`, tấm ghép `sheet-*.png`. Ở 390 px, công thức hiển thị và bảng rộng (2-09, 2-11, 3-04, 4-01, 4-03, 4-05, 5-02, 6-01, 7-01, 7-02) cuộn ngang tại chỗ, trang không tràn.

## 17. Sửa sau năm báo cáo duyệt (người sửa, 2026-11-16)

Đầu vào: `reviews/deck-{hoc-vien,toan-hoc,chuyen-gia,su-pham,mach-truyen}.md`; quyết định của điều phối viên (chấp nhận mọi phát hiện; công thức rộng ở 390 px cuộn tại chỗ, không tách `aligned`). Số trang giữ 55. Kiểm máy sau sửa (lượt 1): `deck_lint.py` báo 1 (`L06-2-08 | LINES6 | 7 dòng`; ghi "0" ở bản trước của mục này là sai, đã sửa ở lượt 2); `footer_check.py` 0; `deck_check.py` console 0, pageerrors 0, failed 0, `.katex-error` 0, không OVERFLOW thật; phím →, ↓, Space, Esc (tổng quan) và `#/2`…`#/7` mở đúng 2-00…7-00. Ảnh 1600×900 và 390×844 (cả `-end`) của mọi trang đã xem: thư mục nháp `lec-06/editor/shots/`, tấm ghép `lec-06/editor/sheet-*.png`.

| Báo cáo · phát hiện | Trang | Xử lý |
|---|---|---|
| học viên · trung bình · kí hiệu Bài 05 chưa giải nghĩa ((C), (G1), (G2), $\varphi$, $\bar w_T$, Thuật toán 05.11) | 1-02 | đã sửa: dòng "Nhắc lại:" SGD có chiếu (Thuật toán 05.11), điểm lặp trung bình (averaged iterate), dòng (C)/(G1)/(G2); định nghĩa lồi mạnh chuyển sang "Nhắc lại:" ở 3-03; công thức $G=2(BC_x+C_y)C_x$ chuyển sang 2-02, nơi dùng |
| học viên · trung bình · (T1) không có nội dung trên mặt trang | 2-01 | đã sửa: dòng "(T1) dạng đầy đủ: …; dạng yếu: mỗi $Z_i\sim D$" |
| học viên · trung bình · bước nhảy ở 4-04 | 4-04 | đã sửa: bước 3 có "trừ: khoảng cách bằng $\tfrac1m\sum_i\mathbb E[\ldots]$" |
| học viên · trung bình · $0{,}3810$ hai nghĩa | 5-03 | đã sửa: số giữa viết $\tfrac14(\tfrac{240}{441}+\tfrac{432}{441})$, khoảng cách viết $8/21$; ghi chú diễn giả nói rõ hai số trùng nhau |
| học viên · trung bình · Bổ đề 06.8 không có (a), (b), (c) | 3-03 | đã sửa |
| học viên · trung bình · công thức bị cắt ở 390 px | 2-08, 2-09, 3-03, 3-05, 4-01, 4-03, 4-05, 5-02, 6-01 | không sửa bằng `aligned` (quyết định của điều phối viên: cuộn tại chỗ); 4-03 rút công thức bằng $\tilde w=A(S;\xi)$, 3-03 đưa "$\forall w\in W$" vào cuối công thức |
| học viên · trung bình · mật độ sát trần | toàn deck | sửa một phần: 1-06 bỏ $L_D(w)=w^2+1$ (ghi chú diễn giả, 2-06), 3-03 chuyển "Trực quan." vào ghi chú diễn giả, 6-05 viết lại; các yêu cầu thêm chữ của người duyệt làm trung vị tăng (mục 15) |
| học viên · trung bình · dòng chia khối 6-05 | 6-05 | đã sửa: "Bài tập 06.7 (hàm lỗi trong $[0,1]$): … khối rời nhau, chọn đầu ra tốt nhất trên tập xác thực (validation set)" |
| học viên · nhẹ · "tập huấn luyện cố định" | 2-09 | đã sửa trong ghi chú diễn giả 2-09, 2-02 (một câu phân biệt); tiêu đề giữ theo §5 của ghi chú |
| học viên · nhẹ · "Mệnh đề 06.5(b) với $u=0$" | 2-11 | đã sửa: "$\inf_WL_D=1$" |
| học viên · nhẹ · số không tên ở lời giải (b2) | 4-07 | đã sửa: "hệ số $0{,}75<1$ (cận Lipschitz), khoảng cách $0{,}25\le0{,}75$" |
| học viên · nhẹ · "bản sao" | 4-04 | đã sửa: "$Z_1=\cdots=Z_m$ (mỗi $Z_i\sim D$)" |
| học viên · nhẹ · dòng "Kỹ thuật." 5-02 cụt | 5-02 | đã sửa |
| học viên · nhẹ · 4-01 dòng mở | 4-01 | đã sửa: "ERM, $\lambda=0$, …" |
| học viên · nhẹ · "Nhắc lại:" tập mẫu ảo cuối trang | 4-05 | đã sửa: đứng sau "Dùng khi …", trước công thức trung bình thay một |
| học viên · nhẹ · cấu trúc 7-03 | 7-03 | đã sửa: câu dẫn là đoạn, ba ý là danh sách |
| học viên · nhẹ · luận điểm bìa | 1-01 | đã sửa: "có cận trực tiếp", "khi hàm lỗi còn Lipschitz", nối bằng "còn" |
| học viên · nhẹ · bảng ở 390 px | 2-11, 3-04 | đã sửa: tiêu đề cột "khoảng cách" (2-11); bỏ cột $\hat w_{S^{(4)}}$ ở 3-04 (giá trị vào ghi chú diễn giả; cũng để bảng không đẩy nội dung chạm chân trang) |
| học viên · nhẹ · chữ SVG nhỏ ở 390 px | 3-04, 4-02, 6-04 | không sửa: số trên hình đều có trong chữ hoặc bảng; Hình 06.1 không thuộc phạm vi ghi |
| học viên · nhẹ · dòng > 20 âm tiết | nhiều trang | sửa một phần: 3-02 tách hai dòng; 6-05, 2-11 rút; 4-01, 4-03, 6-02 giữ (tách sẽ vượt trần 60 hoặc quá 6 dòng) |
| toán học · trung bình · cơ chế bỏ $\lambda>0$ | 5-02 (ghi chú diễn giả) | đã sửa: độ cong $2/m$ cùng bậc độ dịch $2G/m$, cận thành $G$ |
| toán học · trung bình · dòng rút gọn 7-03 thiếu giả thiết | 7-03 | đã sửa: bỏ dòng công thức quan sát mới (giả thiết đủ ở ghi chú diễn giả); dòng chính quy hóa ghi "$\ell$ lồi, không âm, (L), $\lambda^*$ chọn trước" |
| toán học · nhẹ · chiều đổi $(23/13)^2\to(15/13)^2$ | 4-01 (ghi chú diễn giả) | đã sửa |
| toán học · nhẹ · 06.5(b) với $u=0$ | 2-11 | đã sửa |
| toán học · nhẹ · "Trực quan." 2-09 | 2-09 | đã sửa (cơ chế: $u$ cố định nên $\mathbb E_SL_S(u)=L_D(u)$, $\tilde w$ thì không) |
| toán học · nhẹ · Markov dùng $t$ | 6-05 | đã sửa: $\alpha$ |
| toán học · nhẹ · "$w_1=1$" | 3-01 (ghi chú diễn giả) | đã sửa: "mọi điểm $(1,t)$" |
| toán học · nhẹ · logistic cần $W=\mathbb R^p$ | 3-03 (ghi chú diễn giả) | đã sửa |
| toán học · nhẹ · hàng Hệ quả 06.2 thiếu $\eta$, $u\in W$ | 7-01 | đã sửa |
| toán học · nhẹ · "$\lambda=0$: … không giảm" | 6-01 | đã sửa: "có thể không giảm theo $m$ (Ví dụ 06.7)" |
| toán học · nhẹ · Nhận xét 06.12 | 5-01 (ghi chú diễn giả) | đã sửa: đại lượng được chặn, $W=\mathbb R^p$, (T1) |
| toán học · nhẹ · nhãn "tổng" F2 | `danh-doi-khop-on-dinh.svg` | đã sửa: nhãn "tổng" ở $\lambda\approx0{,}3$, nhãn đáy "λ* = 0,2, tổng 0,2" đặt trên đường |
| chuyên gia · trung bình · giới hạn lồi gán cho mọi cận | 7-03, 4-03 (ghi chú diễn giả) | đã sửa: 7-03 "SGD nhiều vòng, mạng nơ-ron (không lồi): cần hệ số ổn định riêng"; ghi chú diễn giả 4-03, 7-03: Định lý 06.10 không cần tính lồi |
| chuyên gia · trung bình · cận không dùng kích thước lớp | 4-03 | đã sửa: "Bảo đảm cấp thuật toán: cận không dùng kích thước của lớp giả thuyết, …"; "không phụ thuộc số chiều $p$" ở ghi chú diễn giả 7-03 (mặt trang 7-03 ở trần) |
| chuyên gia · trung bình · "cố định" hai nghĩa | 2-02, 2-09 (ghi chú diễn giả) | đã sửa |
| chuyên gia · trung bình · cơ chế bỏ $\lambda>0$ | 5-02 | đã sửa (như trên) |
| chuyên gia · nhẹ · "cho cả hai cận" | 1-06 | đã sửa: "Cùng $G=4$, $R=1$, $T$, nên cùng số $RG/\sqrt T=0{,}1$ của Hệ quả 05.15" |
| chuyên gia · nhẹ · "Trực quan." 2-09 | 2-09 | đã sửa |
| chuyên gia · nhẹ · 7-03 thiếu $\mathbb E\operatorname{opt}_S$ | 7-03 | đã sửa |
| chuyên gia · nhẹ · 7-03 dòng quan sát mới thiếu điều kiện | 7-03 | đã sửa (dòng bỏ; điều kiện ở ghi chú diễn giả) |
| chuyên gia · nhẹ · 6-01 khẳng định chung | 6-01 | đã sửa |
| chuyên gia · nhẹ · "Không có $G$ hữu hạn" | 5-04 | đã sửa: "quanh hai nghiệm" |
| chuyên gia · nhẹ · câu dẫn UML 12.9 | 5-04 (ghi chú diễn giả) | đã sửa |
| chuyên gia · nhẹ · "như ở Bài 04" | 4-04 (ghi chú diễn giả) | đã sửa: Fubini; tên kỹ thuật Bài 04 giữ ở mặt trang theo mạch truyện M6(b) |
| chuyên gia · nhẹ · dòng dẫn 6-00 | 6-00 | đã sửa: "một mức rủi ro vượt mức kì vọng" (25 âm tiết) |
| sư phạm · trung bình · luận điểm bìa | 1-01 | đã sửa; ghi chú diễn giả "chặn trực tiếp" |
| sư phạm · trung bình · nhãn "Mục tiêu:", "Cấp thuật toán:" | 2-01, 4-03 | đã sửa: "Cần chặn …"; "Bảo đảm cấp thuật toán: …" |
| sư phạm · trung bình · "Trực quan." 2-09 | 2-09 | đã sửa |
| sư phạm · trung bình · "Diễn giải:" 2-11 | 2-11 | đã sửa: hai câu, "rủi ro vượt mức kì vọng $0{,}2261>0{,}1$", "Vế phải của (b) chủ yếu là khoảng cách tổng quát hóa kì vọng $0{,}4750$, …" |
| sư phạm · trung bình · "Trực quan." 4-02 dừng ở hai bước | 4-02 | đã sửa: thêm "$L_S$ lấy hàm lỗi tại $Z_i$ khi giữ $Z_i$; ổn định đều chặn hiệu"; câu đổi vai có chủ ngữ "kì vọng đó" |
| sư phạm · trung bình · 5-02 tiền ngữ mơ hồ | 5-02 (ghi chú diễn giả) | đã sửa |
| sư phạm · trung bình · cấu trúc 7-03 | 7-03 | đã sửa |
| sư phạm · nhẹ · tiếng Anh thiếu | 1-02, 2-02, 2-08, 3-03 | đã sửa: empirical optimization error, averaged iterate (1-02); squared loss, logistic loss (2-02); memorizing algorithm (2-08); strongly convex (3-03, nơi dùng lần đầu) |
| sư phạm · nhẹ · bỏ "kì vọng" khỏi tên đại lượng | 4-04, 1-04 (ghi chú diễn giả) | đã sửa: tiêu đề "Ý tưởng chứng minh: Định lý 06.10" |
| sư phạm · nhẹ · Ví dụ 06.2, 06.3 không số | 2-06, 2-11 | đã sửa |
| sư phạm · nhẹ · Bổ đề 06.8(c) | 3-03 | đã sửa |
| sư phạm · nhẹ · "theo kì vọng theo", "tất định:" | 2-03, 2-04, 3-03, 4-03, 6-02 | đã sửa: "kì vọng lấy theo …", "(tất định)" |
| sư phạm · nhẹ · ba ví dụ thành danh sách | 2-08 | đã sửa (trang 7 dòng, lý do: danh sách ba ví dụ theo quy tắc văn phong tác giả) |
| sư phạm · nhẹ · công thức đứng chỗ được gọi tên | 2-09 | đã sửa: "ngoặc thứ hai …, ngoặc thứ ba …" sau công thức |
| sư phạm · nhẹ · "Diễn giải:" 3-04 không dùng số | 3-04 | đã sửa: "$\lambda=0\to4$: khoảng cách giảm $0{,}6154\to0{,}1778$, …"; ghi chú diễn giả bỏ "cho thấy cái giá:" |
| sư phạm · nhẹ · mảnh câu 4-01 | 4-01 | sửa một phần: "Với mọi $s\in\mathcal Z^m$, kể cả $s$ có xác suất $0$; …" (thêm "Điều kiện đúng" vượt trần 60) |
| sư phạm · nhẹ · "Nhắc lại:" 4-05 lơ lửng | 4-05 | đã sửa: tên đầy đủ "đối xứng hóa và tập mẫu ảo", đặt trước công thức; ý so sánh trong ghi chú diễn giả |
| sư phạm · nhẹ · số không tên 4-07 | 4-07 | đã sửa |
| sư phạm · nhẹ · "chỉ dùng một:" | 5-02 | đã sửa |
| sư phạm · nhẹ · "cần $1599$" | 6-04 | đã sửa: "$1599$ quan sát ($T=1600$)" |
| sư phạm · nhẹ · 6-05 số khối và "xác suất $\ge1-\delta$" | 6-05 | đã sửa: "xác suất ít nhất $1-\delta$"; dòng chia khối viết lại |
| sư phạm · nhẹ · "thêm bớt" | 7-01 | đã sửa: "cộng và trừ $L_S$" |
| sư phạm · nhẹ · dòng dẫn 6-00, 7-00 | 6-00, 7-00 | đã sửa |
| sư phạm · nhẹ · "gradient", "oracle" rút gọn | 2-00, 2-05, 7-03 | đã sửa |
| sư phạm · nhẹ · câu nói về văn bản trong ghi chú diễn giả | 1-01, 1-02, 2-02, 2-03, 7-01, 7-02, 7-07 | đã sửa |
| sư phạm · nhẹ · câu khó đọc | 2-00, 2-03, 2-10 (ghi chú diễn giả) | đã sửa |
| sư phạm · nhẹ · nhãn F2 "λ* = 0,2: 0,2" | `danh-doi-khop-on-dinh.svg` | đã sửa: "λ* = 0,2, tổng 0,2"; alt cập nhật |
| mạch truyện · M1 · câu hỏi §5 trên mặt trang | 2-08 | đã sửa: "**Câu hỏi:** vì sao cận $\operatorname{opt}_S$ của Bài 05 không chặn $\mathbb EL_D(\bar w_T)$ khi rút từ $S$?"; trả lời ở ghi chú diễn giả và định nghĩa ngay sau |
| mạch truyện · M2 · câu nối 2→3 | 3-01 | đã sửa: "Tính chất xét ở đây: nghiệm đổi bao nhiêu khi thay một quan sát." |
| mạch truyện · M3 · câu nối 4→5 | 5-01 | đã sửa: "Định lý 06.10 cần hệ số ổn định nhỏ; Ví dụ 06.4: …"; dòng "Tức …" gộp vào Bảo đảm (b) |
| mạch truyện · M4 · 7-03 lặp bảng, thiếu ví dụ mở đầu và giới hạn SGD nhiều vòng | 7-03 | đã sửa: câu trả lời bằng lời, $0{,}0006$ / $0{,}2261$, giới hạn SGD nhiều vòng và mạng nơ-ron |
| mạch truyện · M5 · điểm lặp trung bình | 1-02 | đã sửa |
| mạch truyện · M6 · nhắc tên kỹ thuật | 2-03, 4-04, 4-05 | đã sửa: "kì vọng có điều kiện theo lịch sử (Bài 05)"; "lấy điều kiện rồi bỏ điều kiện (Bài 04)"; "đối xứng hóa và tập mẫu ảo (Bài 03)" |
| mạch truyện · N1 · Ví dụ 06.2, 06.3 không số | 2-06, 2-11 | đã sửa |
| mạch truyện · N2 · nối câu hỏi cuối buổi Bài 05 | 1-06 | đã sửa: "Như cuối Bài 05: …" |
| mạch truyện · N3 · cận dưới hệ số ERM | 4-01 | đã sửa: "ERM ở dòng đầu: $\epsilon_{\mathrm{stab}}\ge1{,}7988$" |
| mạch truyện · N4 · vế đối chiếu hội tụ đều | 2-11 | đã sửa: "…, không qua hội tụ đều" |
| mạch truyện · N5 · câu nói về văn bản | 2-02, 7-01, 7-02 (ghi chú diễn giả) | đã sửa |
| mạch truyện · N6 · liên kết Bài 06 trong deck 05 | deck 05 | không sửa: ngoài phạm vi ghi (bước xuất bản của điều phối viên) |
| mạch truyện · N7 · §12 storyboard | storyboard §12 | đã sửa: hàng 2-03, 4-05 |

Lệch khác do sửa: 7-01/7-02 đổi phân bố hàng (2 + 3: Định lý 06.10 chuyển sang 7-02) để bảng 7-01 không chạm chân trang sau khi thêm $\eta$, $u\in W$; 3-04 bỏ cột $\hat w_{S^{(4)}}$ (bảng gọn, số ở ghi chú diễn giả và ở lời giải 5-05 cho $\lambda=2$).

### Lượt 2 (theo `reviews/deck-kiem-lai-1.md`, 2026-11-16)

| Phát hiện | Trang | Xử lý |
|---|---|---|
| K1 · dòng chính quy hóa thiếu $W_B$, (T1); "mở đầu:" không nêu đại lượng | 7-03 | đã sửa theo bản viết lại của người kiểm lại: câu dẫn là câu trọn; danh sách "$\mathbb EL_D(\bar w_T)-1$: $0{,}0006$ … $0{,}2261$ …", "ERM có chính quy hóa, $\ell$ lồi, không âm, (L), (T1), $\lambda^*$ chọn trước: $\mathbb E_SL_D(\hat w_S)-\inf_{W_B}L_D\le2GB/\sqrt m$", K6 |
| K2 · $0{,}2261$ đồng nhất với $0{,}4750$ | 7-03 (ghi chú diễn giả) | đã sửa: "$\mathbb E\operatorname{opt}_S\approx0{,}0011$, còn khoảng cách tổng quát hóa kì vọng bằng $0{,}4750$" |
| K3 · "$0{,}6154\approx0{,}31$" | 3-01 | đã sửa: "dịch $0{,}6154$, khoảng $0{,}31$ lần đường kính" |
| K4 · 2-08 bảy dòng | 2-08 | đã sửa: ví dụ $h$ cố định vào ghi chú diễn giả; hai ví dụ một đoạn; 6 dòng |
| K5 · mật độ | nhiều trang | đã sửa theo mục 4: 2-01, 2-02, 2-03, 2-08, 2-12, 4-05, 4-07, 5-02, 6-05, 2-11 (tách "Diễn giải:"), 3-03 (tách Bổ đề 06.8 thành "Giả thiết:"/"Bảo đảm:" và (c) riêng) |
| K6 · "(không lồi)" gắn cả SGD nhiều vòng | 7-03 | đã sửa |
| K7 · điều kiện cận gắn vào "không chệch" | 7-03 (ghi chú diễn giả) | đã sửa |
| K8 · "khoảng cách" hai nghĩa | 2-11 | đã sửa: tiêu đề cột $\mathbb E[L_D-L_S](\bar w_T)$ |
| K9 · "độ dịch $2G/m$" | 5-02 (ghi chú diễn giả) | đã sửa: "hằng số Lipschitz $2G/m$ của hiệu hai mục tiêu" |
| K10 · "chỉ cần tính ổn định đều" | 4-03 (ghi chú diễn giả) | đã sửa |
| K11 · lồi viết sau nhãn (T2) | 2-01 | đã sửa: "hàm lỗi lồi: $\ell(\cdot,z)$ lồi" |
| K12 · dòng dẫn 2-00, 6-00 | 2-00, 6-00 | đã sửa: 2-00 giữ "lưu lại" (25 âm tiết, vế sau tỉnh lược động từ "không chệch"); 6-00 đủ "độ khớp", "tính ổn định" (25) |
| K13 · Bổ đề 06.8 (b), "cực tiểu" | 3-03 | đã sửa: "(b) có điểm cực tiểu trên $W$; (c) điểm cực tiểu $\hat w_s$ duy nhất" |
| K14 · $\epsilon_{\mathrm{stab}}$ thiếu đối số | 4-01 | đã sửa: $\epsilon_{\mathrm{stab}}(4)$ |
| K15 · "Tính chất xét ở đây:" | 3-01 | đã sửa: "Tính chất của thuật toán cần đo là độ dịch của nghiệm khi thay một quan sát." (bù: dòng đầu rút thành "Ví dụ 06.1, $W=[-1,1]$: …") |
| K16 · "hiệu" không tiền ngữ; câu nối Fubini–Bài 04 | 4-02, 4-04 (ghi chú diễn giả) | đã sửa: "chặn hiệu giữa hai giá trị" (bù: "độc lập với $(S,\xi)$" chuyển vào ghi chú diễn giả); ghi chú diễn giả 4-04 nối Fubini với bước lấy điều kiện của Bài 04 |
| Dòng > 20 âm tiết mới sinh | 2-08, 2-11, 3-03, 4-04 | đã tách hoặc rút (2-08 tách định nghĩa và tên đại lượng; 3-03 tách; 4-04 bước 4 viết lại; 2-11 rút còn 22) |
| Dòng > 20 âm tiết còn lại | 1-02 (23), 2-11 (22), 7-03 (23, câu của người kiểm lại), 6-04 (26) | không tách: tách 1-02 vượt trần 60 và chạm chân trang; tách 6-04 chạm chân trang (904 px); 2-11 không còn chỗ dọc |

Kiểm máy lượt 2: `deck_lint.py` 0 (kể cả LINES6); `footer_check.py` 0; `deck_check.py --shots` console 0, pageerrors 0, failed 0, `.katex-error` 0, không OVERFLOW thật. Đã xem ảnh 1600×900 và 390×844 (cả `-end`) của 2-08, 2-11, 3-01, 3-03, 4-04, 7-03 (thư mục nháp `lec-06/editor/r2/`, tấm ghép `lec-06/editor/r2sel2/`). Mật độ sau lượt 2 (đếm theo quy ước `deck_lint.py`): trung vị trên 42 trang nội dung 54–55; 15 trang ≤ 50; không trang nào 60; trang 58–59: 1-02, 2-01, 3-02, 4-01, 5-01 (58), 4-02, 7-03 (59).

### Lượt 3 (theo `reviews/deck-kiem-lai-2.md`, 2026-11-16)

| Phát hiện | Trang | Xử lý |
|---|---|---|
| L2-1 · tiêu đề cột | 2-11 | đã sửa: $\mathbb E[(L_D-L_S)(\bar w_T)]$ |
| L2-2 · "Diễn giải:" mất từ nối | 2-11 | đã sửa: "…, nhưng rủi ro vượt mức kì vọng $0{,}2261>RG/\sqrt T$."; "Vế phải của (b) … cần cận theo tính chất thuật toán, không qua hội tụ đều." Bù chiều cao: bỏ "$=0{,}1$" khỏi mặt trang (giá trị ở 1-06, 2-06; ghi chú diễn giả 2-11 nhắc "$RG/\sqrt T=0{,}1$ như Ví dụ 06.2"), vì bản đủ chữ chạm chân trang (874 px) |
| L2-3 · "ví dụ thứ ba" | 2-08 (ghi chú diễn giả) | đã sửa: "Ví dụ thứ hai là câu ôn nhanh 2." |

Kiểm máy lượt 3: `deck_lint.py` 0; `footer_check.py` 0; `deck_check.py --ids L06-2-08,L06-2-11 --shots` console 0, pageerrors 0, failed 0, không `.katex-error`; ảnh 1600×900 và 390×844 (cả `-end`) đã xem (thư mục nháp `lec-06/editor/r3b/`).
