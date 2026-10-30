# Dàn ý Bài 03 — Chiều VC và hàm phân lớp tuyến tính

Tệp nội bộ, không liên kết từ trang chỉ mục. Lập ngày 2026-10-31 bởi tác tử lập kế hoạch; chờ điều phối viên duyệt. Dàn ý ràng buộc người viết ghi chú (`materials/lec-03/lecture-note.md`) và sau đó người viết bài tập (`materials/lec-03/exercises.md`).

**Căn cứ, theo thứ tự ưu tiên:** quyết định 1–14 của điều phối viên trong `planning/lec-03/review-log.md` (dẫn là "QĐ n"); `sources/blueprint.md` mục A, C, D, E, "Lecture 3" và §4.1–4.2 của "Lecture 4"; `CLAUDE.md` của học phần và `../CLAUDE.md`; `planning/lec-03/source-analysis.md` (viết tắt PTN; mọi con số ở đó đã được điều phối viên tính lại); `planning/course-plan.md` §3–5; `planning/van-phong.md` (§2, §3a, §7a, §8, §9a, §11); `planning/thuat-ngu.md` (§7); `planning/ky-hieu.md`; mẫu `materials/_templates/lecture-note.md`; dàn ý, nhật ký và `reviews/0-quyet-dinh.md` của Bài 02; ghi chú Bài 01, Bài 02 (mọi số hiệu dẫn dưới đây đã đối chiếu bằng `grep` trên hai tệp ghi chú). Tác tử lập kế hoạch không đọc lại PDF; số bài tập UML lấy từ PTN §7.

**Trạng thái cuối của ghi chú (2026-10-31, sau hai vòng biên tập; ưu tiên hơn các bảng bên dưới):** 19 khối, Ví dụ 03.1–03.10, §10 liệt kê Bài tập 03.1–03.12 (bỏ 03.13). Khác dàn ý: Định nghĩa 03.13 (tính chất hội tụ đều) đứng trước Nhận xét 03.14 (điều kiện (M)) theo thứ tự mới của §7; tên lớp $\mathcal H_{\mathrm{thr}}$, $\mathcal H_{\mathrm{int}}$, $\mathcal H^p_{\mathrm{aff}}$, $\mathcal H^p_{\mathrm{hom}}$; Nhận xét 03.4 "Cận dưới và cận trên cho chiều VC"; Định lý 03.17 "Định lý cơ bản của học PAC cho phân lớp nhị phân — phác thảo (điều kiện cần: UML §5.1, §6.4)", có (T1); Định lý 03.19 có (T1), dẫn UML §6.4, §28.2; cả bảy mục của thứ tự cắt đã áp dụng (không còn $27\,355$, $12\,401$, cột $m=8,10$); Hệ quả 03.16(c) suy từ Định lý 03.15(c) tại $\epsilon/2$. Cho bước bài tập: tiêu đề Bài tập 03.2 "… bằng cận dưới và cận trên"; Bài tập 03.8 thêm ý (a) "số cách gán nhãn không quá số tập con bị tách trọn"; Bài tập 03.11 phải chứng minh đầy đủ phép kéo theo (4)⇒(6); đo phần còn thiếu của mục tiêu 4, 5. Danh sách đầy đủ: `bien-tap-vong-1.md`, `reviews/0-quyet-dinh.md`.

**Con số mới** được đánh dấu † và đã tính lại bằng Python trong scratchpad của phiên (`lec03_outline_check.py`, ngoài repo); phép tính rút gọn ở mục 12.

**Bài học từ rà soát Bài 02, xử lý ngay trong thiết kế:** (i) không liệt kê sớm: mỗi đối tượng của ví dụ xuất hiện ở chỗ khái niệm của nó được định nghĩa (sáu hàm ngưỡng ngay sau Định nghĩa 03.1, ở Ví dụ 03.2; nửa không gian phẳng ở §5; $\mathcal M_{[0,1]}$ ngay sau Định nghĩa 03.14, ở Ví dụ 03.6); §3 chỉ có lớp hàm ngưỡng trên $\mathbb R$ và khối ứng dụng; (ii) mỗi vai của $\epsilon$ ghi trong bảng §2 và nhắc lại tại Hệ quả 03.16; (iii) mọi mục §4–§8 kết bằng một câu văn xuôi (ghi sẵn ở mục 3); (iv) phạm vi của mỗi cỡ mẫu (mọi thuật toán ERM, mọi phân bố; trực tiếp hay dạng đóng; độ lệch đều hay rủi ro vượt mức) ghi ngay cạnh con số; (v) chỉ so sánh các cỡ mẫu cùng loại bảo đảm (QĐ 8); (vi) không có câu "Bài này…" làm chủ ngữ.

## 1. Câu hỏi trung tâm, luận điểm, câu hỏi mở đầu, mục tiêu

**Câu hỏi trung tâm** (blueprint mục B). Một lớp giả thuyết có vô số phần tử có thể học được không, và đại lượng nào của lớp thay cho $\ln\lvert\mathcal H\rvert$ trong cận cỡ mẫu?

**Luận điểm (một câu).** Trên $m$ điểm, một lớp có chiều VC $d$ hữu hạn chỉ tạo ra nhiều nhất $\sum_{j\le d}\binom mj\le(em/d)^d$ cách gán nhãn, và nhờ một mẫu bóng, số đếm này tại $2m$ điểm thay cho $\lvert\mathcal H\rvert$ trong bất đẳng thức hợp; kết quả là, khi $1\le d\le m$, với xác suất ít nhất $1-\delta$, $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\le4\sqrt{(d\ln(em/d)+\ln(2/\delta))/m}$, nên mọi nghiệm ERM trên lớp hàm phân lớp tuyến tính afin trong $\mathbb R^p$ ($d=p+1$) có rủi ro vượt mức nhỏ khi $m$ lớn so với $d$.

**Câu hỏi mở đầu** (blueprint 3.1; văn phong §9a; viết đúng như sau, có thể sửa chữ nhỏ):

> Lớp hàm ngưỡng $h_t(x)=\mathbb 1[x\ge t]$, $t\in\mathbb R$, có vô số phần tử, nên cận cỡ mẫu theo $\ln\lvert\mathcal H\rvert$ của Bài 02 không cho kết quả. Tuy vậy, mỗi hàm ngưỡng được xác định bởi một số thực, và trên năm mức đo của ví dụ sàng lọc, cả lớp chỉ cho sáu hàm khác nhau.
>
> **Câu hỏi.** Cần bao nhiêu quan sát để, với xác suất ít nhất $0{,}95$ và với mọi phân bố, mọi nghiệm ERM trên lớp hàm ngưỡng có rủi ro vượt mức không quá $0{,}1$? Đại lượng nào của một lớp vô hạn thay cho $\ln\lvert\mathcal H\rvert$?

Câu trả lời hấp dẫn nhưng sai, viết thành câu hỏi thẳng rồi trả lời ngay: "Có thể đếm số tham số thay cho $\ln\lvert\mathcal H\rvert$ không? Không. Lớp các hàm $x\mapsto\mathbb 1[\sin(\theta x)>0]$, $\theta\in\mathbb R$, cũng chỉ có một tham số, nhưng trên những tập điểm lớn tùy ý nó thực hiện được mọi cách gán nhãn." Thêm hai câu: đại lượng cần tìm đếm số cách gán nhãn mà lớp tạo ra trên các tập điểm hữu hạn (§4, §6); câu trả lời bằng số cho lớp hàm ngưỡng nằm ở §8 ($54\,330$ quan sát theo dạng trực tiếp). Không dẫn số khối (quy tắc định nghĩa trước khi dùng); không viết "một câu trả lời … cho rằng …". Câu hỏi thứ nhất được trả lời ở Ví dụ 03.9, câu thứ hai ở Định nghĩa 03.3, 03.11 và Định lý 03.15.

**Mục tiêu học tập** (chỉ chữ, không kí hiệu, không số khối):

1. Tính chiều VC của lớp hàm ngưỡng, lớp khoảng và lớp nửa không gian bằng hai chiều lập luận: một tập bị tách trọn cho cận dưới, mọi tập lớn hơn một đơn vị không bị tách trọn cho cận trên; nhận ra một lập luận chỉ có một chiều.
2. Tính hàm tăng trưởng của các lớp đơn giản, so sánh với cận Sauer–Shelah và với số mọi cách gán nhãn, và giải thích vì sao số cách gán nhãn tăng theo đa thức của số điểm khi chiều VC hữu hạn.
3. Trình bày lộ trình chứng minh cận hội tụ đều theo chiều VC (mẫu bóng, đổi chỗ với dấu ngẫu nhiên, đếm cách gán nhãn trên mẫu gộp, bất đẳng thức Hoeffding và bất đẳng thức hợp, bổ đề Sauer–Shelah), chỉ ra chỗ dùng từng giả thiết, và giải thích vì sao không lấy hợp trên các cách gán nhãn của chính mẫu huấn luyện.
4. Tính cận độ lệch đều và cỡ mẫu đủ cho ERM từ chiều VC, và so sánh trung thực với cận của lớp hữu hạn sau khi rời rạc hóa tham số.
5. Phát biểu định lý cơ bản cho phân lớp nhị phân, và dựng phản ví dụ khi bỏ chiều VC hữu hạn, khi lớp được chọn sau khi xem mẫu, hoặc khi thay chiều VC bằng số tham số.

## 2. Đánh số

Một bộ đếm chung theo thứ tự đọc cho định nghĩa, bổ đề, mệnh đề, định lý, hệ quả, nhận xét (Bài 03 không có thuật toán); ví dụ và bài tập có bộ đếm riêng. Khối `application` không đánh số. Hai giả thiết mới (M), (T5) viết thành gạch đầu dòng như (T4) của Bài 02, không đánh số. Cột "Blueprint" chỉ dùng nội bộ, không đưa vào ghi chú.

| Số | Loại | Tên (cụm danh từ) | Mục | Độ sâu | Blueprint / QĐ |
|---|---|---|---|---|---|
| Định nghĩa 03.1 | definition | Thu hẹp của một lớp lên một bộ điểm | §4 | — | §3.2 restriction |
| Định nghĩa 03.2 | definition | Tập bị tách trọn | §4 | — | §3.2 shattering |
| Định nghĩa 03.3 | definition | Chiều VC | §4 | — | §3.2 VC dimension |
| Nhận xét 03.4 | remark | Hai chiều của phép tính chiều VC | §4 | — | §3.4; QĐ 9(c) |
| Mệnh đề 03.5 | proposition | Chiều VC của lớp hàm ngưỡng | §4 | chứng minh đầy đủ | **Prop 3.1** |
| Mệnh đề 03.6 | proposition | Chiều VC của lớp khoảng đóng | §4 | chứng minh đầy đủ | **Prop 3.2** |
| Định nghĩa 03.7 | definition | Nửa không gian afin và nửa không gian thuần nhất | §5 | — | §3.3 |
| Bổ đề 03.8 | lemma | Phân hoạch Radon | §5 | chứng minh đầy đủ ở Phụ lục A | §3.3 "Radon"; QĐ 5 |
| Mệnh đề 03.9 | proposition | Chiều VC của lớp nửa không gian | §5 | chứng minh đầy đủ (cận trên của phần (b) ở Phụ lục A) | **Prop 3.3**; QĐ 5 |
| Nhận xét 03.10 | remark | Số tham số và chiều VC | §5 | — | §3.5 bài 5; QĐ 10 |
| Định nghĩa 03.11 | definition | Hàm tăng trưởng | §6 | — | §3.2 growth function; QĐ 2 |
| Bổ đề 03.12 | lemma | Bổ đề Sauer–Shelah | §6 | phác thảo (chứng minh đầy đủ ở Phụ lục B) | **Lemma 3.4**; QĐ 4 |
| Nhận xét 03.13 | remark | Điều kiện (M) cho các lớp của bài | §7 | — | §A "measurability"; QĐ 6 |
| Định nghĩa 03.14 | definition | Tính chất hội tụ đều của một lớp | §7 | — | QĐ 3 |
| Định lý 03.15 | theorem | Hội tụ đều trên lớp có chiều VC hữu hạn | §7 | phác thảo (chứng minh đầy đủ ở Phụ lục C) | **Theorem 3.5**; QĐ 1 |
| Hệ quả 03.16 | corollary | Rủi ro vượt mức của ERM trên lớp có chiều VC hữu hạn | §8 | chứng minh đầy đủ | **Corollary 3.6**; QĐ 7 |
| Định lý 03.17 | theorem | Định lý cơ bản cho phân lớp nhị phân | §8 | đọc thêm (một số chiều suy ra từ 03.15, 03.16) | **Fundamental theorem**; QĐ 6 |
| Hệ quả 03.18 | corollary | Lớp mọi hàm phân lớp đo được trên $[0,1]$ không học được PAC | §8 | chứng minh đầy đủ từ Định lý 03.17(a) | QĐ 6 (lời hứa Hệ quả 01.29, Nhận xét 01.21) |
| Định lý 03.19 | theorem | Cận dưới cho độ phức tạp mẫu | §8 | đọc thêm (chỉ phát biểu) | §3.3 "defer sharp-rate"; QĐ 6 (lời hứa Nhận xét 02.18) |

Tiêu đề khối theo mẫu: `::: theorem Định lý 03.15 (Hội tụ đều trên lớp có chiều VC hữu hạn) — phác thảo`; `::: lemma Bổ đề 03.8 (Phân hoạch Radon) — chứng minh đầy đủ ở Phụ lục A`; `::: theorem Định lý 03.17 (Định lý cơ bản cho phân lớp nhị phân) — đọc thêm`. Chứng minh: `::: proof Chứng minh Định lý 03.15 (lộ trình)`.

**Lý do chọn vai.** Radon và Sauer–Shelah là công cụ cho kết quả khác nên là Bổ đề. Ba lớp cụ thể là sự kiện tập trung nên là Mệnh đề. Định lý 03.15 là kết quả chính của bài (bản đồ học phần). Hệ quả 03.16 suy trực tiếp từ 03.15 bằng ba bất đẳng thức. Định lý cơ bản và cận dưới là kết quả chính của lý thuyết nhưng chỉ phát biểu, nên giữ nhãn Định lý với độ sâu *đọc thêm*. Hệ quả 03.18 suy trong hai dòng từ Định lý 03.17(a) và một phép tính chiều VC; chứng minh của nó đầy đủ *khi đã nhận* 03.17(a), và tiêu đề nói rõ điều đó. Tách trọn của tập con, $d\le\log_2\lvert\mathcal H\rvert$ và các tính chất của $\Pi_{\mathcal H}$ chỉ là đoạn đọc sau định nghĩa, không thành khối riêng.

**Ví dụ** (bộ đếm riêng):

| Số | Tên | Mục | Vai trò |
|---|---|---|---|
| Ví dụ 03.1 | Lớp hàm ngưỡng trên đường thẳng thực | §3 | ví dụ tính tay xuyên suốt; vì sao Định lý 02.14 không cho gì |
| Ví dụ 03.2 | Sáu hàm ngưỡng của ví dụ sàng lọc là một thu hẹp | §4 | thu hẹp; QĐ 11 |
| Ví dụ 03.3 | Nửa không gian trong mặt phẳng trên ba và bốn điểm | §5 | tách trọn ba điểm; ba điểm thẳng hàng; hình vuông (XOR); điểm trong tam giác; QĐ 9(c) |
| Ví dụ 03.4 | Hàm tăng trưởng của lớp hàm ngưỡng và lớp khoảng | §6 | $\Pi(m)=m+1$; $\binom{m+1}2+1$; blueprint bài 1 làm mẫu |
| Ví dụ 03.5 | Ba cách đếm cách gán nhãn | §6 | bảng tăng trưởng, Sauer, $2^m$, $(em/3)^3$ |
| Ví dụ 03.6 | Lớp mọi hàm phân lớp đo được trên $[0,1]$ | §7 | phản ví dụ (a) của QĐ 9: chiều VC vô hạn, hội tụ đều hỏng |
| Ví dụ 03.7 | Cận độ lệch đều cho $d=3$ và $d=11$ | §7 | cận số; ứng dụng $p=10$ |
| Ví dụ 03.8 | Hai hàm chọn sau khi xem mẫu | §7 | phản ví dụ (b) của QĐ 9: bỏ (T5) |
| Ví dụ 03.9 | Cỡ mẫu cho rủi ro vượt mức $0{,}1$ | §8 | trả lời câu hỏi mở đầu; $54\,330$, $132\,992$, $447\,194$ |
| Ví dụ 03.10 | So sánh với lớp hữu hạn sau khi rời rạc hóa | §8 | QĐ 8; nhận xét trung thực |

**Không dùng lại $D_\eta$** (QĐ 11): Ví dụ 03.2 chỉ dùng lớp sáu hàm ngưỡng trên $\{1,\ldots,5\}$ (không cần phân bố); phản ví dụ chép mẫu chỉ là một câu dẫn Ví dụ 02.6, không có số dưới $D_\eta$. Vì vậy không cần sửa dòng $D_\eta$ của `ky-hieu.md`. Kí hiệu $h_t$ được mở rộng sang $t\in\mathbb R$ với cùng công thức $\mathbb 1[x\ge t]$ (Ví dụ 01.1 dùng $t\in\{1,\ldots,6\}$); ghi một câu ở Ví dụ 03.1.

## 3. Bản đồ các mục và phát biểu hình thức

Quy tắc định nghĩa trước khi dùng thắng thứ tự thành phần của blueprint: thành phần 7–11 nằm xen trong §4–§8; mỗi giả thiết được nêu ngay trước khối dùng nó lần đầu; không câu nào trong thân bài dẫn một khối có số đứng sau (được viết "mệnh đề dưới đây", "§7"). Mỗi khối kết quả có **Giả thiết.** và **Bảo đảm.**; từ ba thành phần trở lên thì viết danh sách có nhãn in đậm song song (§3a; mẫu: Định lý 02.14). Xác suất cao viết "với xác suất ít nhất $1-\delta$ theo $S\sim D^m$". Các kết quả tổ hợp (03.5, 03.6, 03.8, 03.9, 03.12) ghi trong **Bảo đảm.** rằng khẳng định là tất định: không có phân bố, không có mẫu ngẫu nhiên.

**Kí hiệu cục bộ chốt cho bài** (lý do ở mục 10): lớp hàm ngưỡng $\mathcal H_{\mathrm{ng}}$, lớp khoảng $\mathcal H_{\mathrm{kh}}$ với $h_{u,v}=\mathbb 1[u\le x\le v]$ (không dùng $[a,b]$ vì $b$ là hệ số tự do của nửa không gian), nửa không gian $\mathcal H^p_{\mathrm{af}}$, $\mathcal H^p_{\mathrm{tn}}$ với $h_{w,b}$; bộ điểm $C=(x_1,\ldots,x_k)$, cỡ $k$; chỉ số tổng Sauer $j$; bán kính VC $\rho_m$; mẫu bóng $S'$; dấu ngẫu nhiên $\sigma_i$; véc-tơ đơn vị $\mathbf e_i$ (in đứng, để khác số $e$); hằng số của Định lý 03.15 viết thẳng là $4$, không đặt $C$.

### `# Bài 03 — Chiều VC và hàm phân lớp tuyến tính` và đoạn dẫn

Ba câu: Định lý 02.14 và Hệ quả 02.16 cho cỡ mẫu theo $\ln K$, $K=\lvert\mathcal H\rvert$; lớp hàm ngưỡng và lớp hàm phân lớp tuyến tính (linear classifier) có vô số phần tử; câu hỏi trung tâm và ba công cụ (chiều VC (Vapnik–Chervonenkis dimension), hàm tăng trưởng (growth function), mẫu bóng (ghost sample)) cùng kết quả cuối (cận hội tụ đều, bảo đảm cho ERM, định lý cơ bản). Không viết "Bài này …".

### `## Câu hỏi mở đầu`, `## Mục tiêu học tập`

Như mục 1.

### `## Kiến thức tiên quyết`

- **Từ Bài 01.** Thuật toán học và điều kiện đo được (Định nghĩa 01.4); ERM, $\epsilon_{\mathrm{opt}}$-ERM, (O1), (O2) (Định nghĩa 01.8, 01.12); lớp $\mathcal M_{\mathcal X}$ (Ví dụ 01.8) và Mệnh đề 01.15; tính khả thực, học PAC hai dạng, độ phức tạp mẫu (Định nghĩa 01.16, 01.18, 01.20, 01.25; Nhận xét 01.21, 01.26); cận tổng quát hóa cho mọi thuật toán ERM và Hệ quả 01.29; ví dụ sàng lọc (Ví dụ 01.1); Phụ lục A(v) (tính đo được với lớp vô hạn).
- **Từ Bài 02.** Bất đẳng thức Chebyshev (Bổ đề 02.3), Hoeffding (Định lý 02.7) với miền khác nhau (Nhận xét 02.8), bất đẳng thức hợp (Bổ đề 02.12), mẫu $\epsilon$-đại diện (Định nghĩa 02.13), Định lý 02.14, Hệ quả 02.16, Ví dụ 02.6, Nhận xét 02.18; giả thiết (T1)–(T4).
- **Đại số tuyến tính và hình học.** $p+1$ véc-tơ trong $\mathbb R^p$ phụ thuộc tuyến tính; hệ thuần nhất có nhiều ẩn hơn phương trình có nghiệm khác $0$; ma trận vuông khả nghịch; *tổ hợp lồi* (convex combination) và *bao lồi* (convex hull) $\operatorname{conv}$ của một tập hữu hạn; *độc lập afin* (affinely independent): $x_0,\ldots,x_k$ độc lập afin khi $x_1-x_0,\ldots,x_k-x_0$ độc lập tuyến tính.
- **Tổ hợp và giải tích.** Hệ số nhị thức, công thức Pascal $\binom mj=\binom{m-1}j+\binom{m-1}{j-1}$, khai triển nhị thức; $1+x\le e^x$ (đã có dạng $1-x\le e^{-x}$ ở Bài 02).

**Câu hỏi ôn nhanh** (lời giải ngắn trong một khối `solution`, như Bài 02):

1. Tính $\sum_{j=0}^{2}\binom5j$ và so sánh với $2^5$. *Lời giải:* $1+5+10=16$, bằng nửa của $32$. (Chuẩn bị Ví dụ 03.4 và Bổ đề 03.12.)
2. Cho ba điểm $(0,0)$, $(1,0)$, $(0,1)$ của $\mathbb R^2$. Tìm $w\in\mathbb R^2$, $b\in\mathbb R$ sao cho $\mathbb 1[\langle w,x\rangle+b\ge0]$ bằng $0$ tại $(0,0)$ và bằng $1$ tại hai điểm còn lại. *Lời giải:* chẳng hạn $b=-1$, $w=(2,2)$: giá trị $-1$, $1$, $1$. (Chuẩn bị Mệnh đề 03.9.)
3. Cho $V_1,\ldots,V_m$ độc lập, $\mathbb EV_i=0$, $-1\le V_i\le1$, và $\epsilon>0$. Dùng Định lý 02.7 để chặn $\Pr(\lvert\bar V_m\rvert\ge\epsilon)$. *Lời giải:* miền dài $2$, nên $2\exp(-2m\epsilon^2/4)=2e^{-m\epsilon^2/2}$. (Chuẩn bị Bước 4 của Định lý 03.15.)

Không ghi số khối của bài trong câu hỏi hay lời giải ôn nhanh (định nghĩa trước khi dùng); các chú thích trong ngoặc ở trên chỉ dành cho người viết.

### `## 1. Thiết lập bài toán`

Câu mở: "Bài toán giữ tám thành phần của §1 Bài 02, với các lựa chọn sau." Danh sách nhãn in đậm song song:

1. **Tập quan sát và phân bố dữ liệu.** $\mathcal Z=\mathcal X\times\{0,1\}$, $D$ cố định, chưa biết; $\mathcal X$ có σ-đại số ($\mathbb R^p$ với σ-đại số Borel trong các ví dụ).
2. **Mẫu.** $S=(Z_1,\ldots,Z_m)\sim D^m$ theo (T1).
3. **Lớp giả thuyết.** $\mathcal H$ gồm các hàm $\mathcal X\to\{0,1\}$, có thể vô hạn, chọn trước khi lấy mẫu; điều kiện đo được nêu ở §7.
4. **Hàm lỗi.** Hàm lỗi 0–1; nó thỏa (T2), (T3).
5. **Quy tắc dùng mẫu.** Một thuật toán ERM bất kì trên $\mathcal H$, hoặc một $\epsilon_{\mathrm{opt}}$-ERM (§8).
6. **Mục tiêu.** Hai đại lượng cần chặn: độ lệch đều $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$ và rủi ro vượt mức $L_D(\hat h)-\inf_{h\in\mathcal H}L_D(h)$.
7. **Đối tượng so sánh.** $\inf_{h\in\mathcal H}L_D(h)$; với lớp vô hạn, cận dưới đúng có thể không đạt (Nhận xét 01.17 có một lớp ngưỡng vô hạn như vậy).
8. **Tài nguyên.** Cỡ mẫu $m$; câu trả lời viết theo chiều VC $d$, $\epsilon$, $\delta$, không theo $\lvert\mathcal H\rvert$.

Bảng cố định / ngẫu nhiên (bắt buộc): cố định: $D$, $\mathcal H$, $d$, $\Pi_{\mathcal H}$, mỗi $h$, $L_D(h)$, $\inf_{\mathcal H}L_D$; ngẫu nhiên theo $S\sim D^m$: $S$, $L_S(h)$, tập các cách gán nhãn của $\mathcal H$ trên $(X_1,\ldots,X_m)$, độ lệch đều, $\hat h$, $L_D(\hat h)$; chỉ trong chứng minh: $S'$ và $\sigma_1,\ldots,\sigma_m$. Trong §1 chỉ nêu tên "chiều VC", "hàm tăng trưởng" bằng chữ, kí hiệu được định nghĩa ở §4, §6 (bảng có thể ghi "xem §4, §6").

### `## 2. Kí hiệu và giả thiết`

- Bảng nhỏ, chỉ kí hiệu dùng từ §3: $h_t$ với $t\in\mathbb R$; $p$ (số chiều đặc trưng); $\langle w,x\rangle$; $\ln$; các vai của $\epsilon$ ("độ lệch đều ở §7; mức rủi ro vượt mức ở §8; mức rủi ro trong phần khả thực của §8"). Chiều VC $d$ và $\Pi_{\mathcal H}$ đặt tên tại định nghĩa (§4, §6), như Bài 02.
- Một đoạn: dùng lại (T1), (T2), (T3) của Bài 01–02 (hàm lỗi 0–1 thỏa (T2), (T3)); (T4) đòi lớp hữu hạn nên được thay bằng **(T5)** (lớp cố định trước mẫu, có thể vô hạn) ở §7; điều kiện đo được **(M)** ở §7; (O1), (O2) ở §8; tính khả thực chỉ ở §8. Không dùng lồi, trơn, Lipschitz.

### `## 3. Ví dụ xuyên suốt`

- **Ví dụ 03.1 (Lớp hàm ngưỡng trên đường thẳng thực).** **Thiết lập.** $\mathcal X=\mathbb R$, $\mathcal H_{\mathrm{ng}}=\{h_t:t\in\mathbb R\}$, $h_t(x)=\mathbb 1[x\ge t]$, cùng công thức với Ví dụ 01.1 nhưng $t$ chạy trên $\mathbb R$. **Bước 1.** Hai ngưỡng $t<t'$ khác nhau đúng trên $[t,t')$, nên $\mathcal H_{\mathrm{ng}}$ vô hạn. **Bước 2.** Định lý 02.14 cần $K=\lvert\mathcal H\rvert$ hữu hạn; ở đây không có $K$, nên định lý không áp dụng. **Bước 3.** Trên một mẫu với các đầu vào $x_1<\cdots<x_m$, rủi ro thực nghiệm của $h_t$ chỉ phụ thuộc vị trí của $t$ so với các $x_i$, nên chỉ có $m+1$ giá trị của véc-tơ $(h_t(x_1),\ldots,h_t(x_m))$ (đếm cẩn thận ở §6). Câu cuối: một lớp vô hạn có thể chỉ tạo ra ít cách gán nhãn trên mẫu; §4 gọi tên số đếm này.
- **Khối `application` (Hàm phân lớp tuyến tính trên mười chỉ số đo)** (QĐ 11). **Đặc trưng.** Mỗi người được mô tả bởi $p=10$ chỉ số đo, $x\in\mathbb R^{10}$. **Lớp.** $h_{w,b}(x)=\mathbb 1[\langle w,x\rangle+b\ge0]$ với $w\in\mathbb R^{10}$, $b\in\mathbb R$; dương tính khi tổ hợp tuyến tính vượt ngưỡng. **Câu hỏi thực hành.** Cần bao nhiêu quan sát để rủi ro vượt mức của nghiệm ERM không quá $0{,}1$ với mọi phân bố; con số thay đổi thế nào nếu thay mười chỉ số bằng hai. Không đưa số liệu thực tế; không nói ERM trên lớp này tính được hiệu quả (tối ưu nằm ngoài bài).

Câu nối sang §4: cả hai lớp vô hạn, nên chúng ta cần một đại lượng đo lớp trên các tập điểm hữu hạn.

### `## 4. Thu hẹp, tách trọn và chiều VC` (blueprint: động cơ/định nghĩa 20 phút, một phần ví dụ 35 phút)

**Câu mở (nhu cầu, văn phong §2):** "Định lý 02.14 đếm $K=\lvert\mathcal H\rvert$ giả thuyết. Trên một mẫu cố định, $L_S(h)$ chỉ phụ thuộc các giá trị của $h$ tại $m$ đầu vào, nên điều cần đếm là số véc-tơ giá trị khác nhau mà lớp tạo ra trên các đầu vào đó."

1. **Định nghĩa 03.1 (Thu hẹp của một lớp lên một bộ điểm).** Cho lớp $\mathcal H$ các hàm $\mathcal X\to\{0,1\}$, $k\ge1$ và bộ điểm $C=(x_1,\ldots,x_k)\in\mathcal X^k$, các điểm có thể trùng nhau. Mỗi $y\in\{0,1\}^k$ được gọi là một *cách gán nhãn* (labeling) của $C$. *Thu hẹp* (restriction) của $\mathcal H$ lên $C$ là tập
   $\mathcal H_C=\{(h(x_1),\ldots,h(x_k)):h\in\mathcal H\}\subseteq\{0,1\}^k$; cách gán nhãn thuộc $\mathcal H_C$ được gọi là *thực hiện được* bởi $\mathcal H$. Với tập hữu hạn $C\subseteq\mathcal X$, ta liệt kê các phần tử theo một thứ tự cố định. Đọc lại: $\lvert\mathcal H_C\rvert\le\min\{\lvert\mathcal H\rvert,2^k\}$; $\mathcal H_C$ chỉ phụ thuộc $\mathcal H$ và $C$; với $C=(X_1,\ldots,X_m)$ lấy từ mẫu, $L_S(h)$ là hàm của $(h(X_1),\ldots,h(X_m))$, nên trên mẫu đó lớp hành xử như $\lvert\mathcal H_C\rvert$ hàm. Phản ví dụ: với $\mathcal H_{\mathrm{ng}}$ và $C=(1,2)$, cách gán nhãn $(1,0)$ không thực hiện được.
2. **Ví dụ 03.2 (Sáu hàm ngưỡng của ví dụ sàng lọc là một thu hẹp)** (QĐ 11). **Thiết lập.** $\mathcal H_{\mathrm{ng}}$ của Ví dụ 03.1, $C=(1,2,3,4,5)$, năm mức đo của Ví dụ 01.1; không cần phân bố. **Bước 1.** Với $t\le1$: $(1,1,1,1,1)$; với $t\in(k-1,k]$, $k=2,\ldots,5$: $k-1$ số $0$ rồi các số $1$; với $t>5$: $(0,0,0,0,0)$. **Bước 2.** Liệt kê sáu véc-tơ; chúng trùng với sáu hàm $h_1,\ldots,h_6$ của Ví dụ 01.1. **Bước 3.** $\lvert\mathcal H_C\rvert=6$, so với $2^5=32$ cách gán nhãn của $C$. **Kết luận.** Lớp sáu hàm ngưỡng mà Bài 02 dùng với $K=6$ chính là thu hẹp của một lớp vô hạn lên năm điểm.
3. **Định nghĩa 03.2 (Tập bị tách trọn).** Cho $\mathcal H$ và tập hữu hạn $C\subseteq\mathcal X$ có $k$ phần tử. Ta nói $\mathcal H$ *tách trọn* (shatters) $C$ nếu $\lvert\mathcal H_C\rvert=2^k$, tức mọi cách gán nhãn của $C$ đều thực hiện được. Quy ước: tập rỗng bị tách trọn bởi mọi lớp khác rỗng. Đọc lại: tính chất của $\mathcal H$ và $C$, không có $D$ hay $S$; mọi tập con của một tập bị tách trọn cũng bị tách trọn (mở rộng một cách gán nhãn của tập con một cách tùy ý rồi lấy giả thuyết thực hiện nó). Ví dụ: $\mathcal H_{\mathrm{ng}}$ tách trọn $\{0\}$. Phản ví dụ: $\mathcal H_{\mathrm{ng}}$ không tách trọn $\{1,2\}$ (Định nghĩa 03.1); một bộ có điểm lặp không được xét vì định nghĩa dùng tập.
4. **Định nghĩa 03.3 (Chiều VC).** Cho lớp $\mathcal H$ khác rỗng. *Chiều Vapnik–Chervonenkis* (VC dimension), viết $d$ hoặc $\operatorname{VCdim}(\mathcal H)$ khi có nhiều lớp, là số phần tử lớn nhất của một tập hữu hạn bị $\mathcal H$ tách trọn; nếu với mọi $k$ có một tập $k$ phần tử bị tách trọn thì $d=\infty$. Đọc lại: $d\ge0$ vì tập rỗng bị tách trọn; $d=0$ khi mọi hàm của lớp trùng nhau; $d$ không phụ thuộc $D$, $m$, cách tham số hóa; lớp hữu hạn có $2^d\le\lvert\mathcal H\rvert$, tức $d\le\log_2\lvert\mathcal H\rvert$ (lớp sáu hàm ngưỡng: $d\le\log_26\approx2{,}585$, nên $d\le2$). Ví dụ và phản ví dụ: hai mệnh đề dưới đây.
5. **Nhận xét 03.4 (Hai chiều của phép tính chiều VC)** (QĐ 9(c); blueprint 3.4). Để chứng minh $d=k$ cần hai phần: **cận dưới**, một tập $k$ phần tử bị tách trọn, cho $d\ge k$; **cận trên**, mọi tập $k+1$ phần tử không bị tách trọn, cho $d\le k$, vì một tập lớn hơn bị tách trọn sẽ chứa một tập con $k+1$ phần tử bị tách trọn. Hai lỗi đối xứng: chỉ vẽ một tập bị tách trọn mới chứng minh $d\ge k$; chỉ ra một tập $k+1$ phần tử không bị tách trọn không chứng minh gì (ba điểm thẳng hàng ở §5). Không viết dạng danh sách lập luận; hai câu cho hai phần, một câu cho hai lỗi.
6. **Mệnh đề 03.5 (Chiều VC của lớp hàm ngưỡng) — chứng minh đầy đủ** (blueprint Prop 3.1). **Giả thiết.** $\mathcal X=\mathbb R$, lớp $\mathcal H_{\mathrm{ng}}$; hoặc $\mathcal X=\{1,\ldots,5\}$ với lớp sáu hàm ngưỡng. **Bảo đảm.** Chiều VC của cả hai lớp bằng $1$; khẳng định tất định về lớp. **Chứng minh.** Lộ trình: cận dưới bằng một điểm, cận trên bằng một cách gán nhãn không thực hiện được trên mọi cặp điểm. Cận dưới: $h_0(0)=1$, $h_1(0)=0$, nên $\{0\}$ bị tách trọn (lớp sáu hàm: $h_1(1)=1$, $h_2(1)=0$). Cận trên: với $x_1<x_2$, cách gán nhãn $(1,0)$ cần $x_1\ge t>x_2$, vô lý; tính chất then chốt là $h_t$ không giảm theo $x$. Câu sau $\square$: lớp vô hạn nhưng chiều VC bằng $1$; con số đo khả năng gán nhãn tự do, không đo số phần tử.
7. **Mệnh đề 03.6 (Chiều VC của lớp khoảng đóng) — chứng minh đầy đủ** (blueprint Prop 3.2; PTN §1: khoảng đóng). **Giả thiết.** $\mathcal X=\mathbb R$, $\mathcal H_{\mathrm{kh}}=\{h_{u,v}:u\le v\}$, $h_{u,v}(x)=\mathbb 1[u\le x\le v]$. **Bảo đảm.** $d=2$; tất định. **Chứng minh.** Cận dưới: $C=\{0,1\}$; bốn cách gán nhãn $(1,1)$, $(1,0)$, $(0,1)$, $(0,0)$ thực hiện bởi $[0,1]$, $[0,0]$, $[1,1]$, $[2,2]$. Cận trên: $x_1<x_2<x_3$, cách gán nhãn $(1,0,1)$ cần $u\le x_1<x_2<x_3\le v$, nên $h_{u,v}(x_2)=1$; tính chất then chốt là tập $\{h=1\}$ là một khoảng. Ghi: hàm hằng $0$ không thuộc lớp, nhưng mọi cách gán nhãn toàn $0$ trên tập hữu hạn đều thực hiện được bằng một khoảng suy biến nằm ngoài tập. Câu sau $\square$: hai lớp có số phần tử như nhau (lực lượng của $\mathbb R$) nhưng chiều VC khác nhau.

Kết mục bằng văn xuôi: hai lớp trên đường thẳng có chiều VC $1$ và $2$; lớp của khối ứng dụng sống trong $\mathbb R^{10}$, nơi không còn thứ tự để lập luận như trên.

### `## 5. Nửa không gian và hàm phân lớp tuyến tính` (phần còn lại của 35 phút ví dụ)

**Câu mở:** "Trong $\mathbb R^p$ không có thứ tự, nên cận trên cho lớp nửa không gian cần một công cụ hình học: định lý Radon."

1. **Định nghĩa 03.7 (Nửa không gian afin và nửa không gian thuần nhất).** Cho $p\ge1$. Với $w\in\mathbb R^p$, $b\in\mathbb R$, đặt $h_{w,b}(x)=\mathbb 1[\langle w,x\rangle+b\ge0]$. Lớp *nửa không gian afin* (affine halfspaces), còn gọi là lớp hàm phân lớp tuyến tính afin, là $\mathcal H^p_{\mathrm{af}}=\{h_{w,b}:w\in\mathbb R^p,b\in\mathbb R\}$; lớp *nửa không gian thuần nhất* (homogeneous halfspaces) là $\mathcal H^p_{\mathrm{tn}}=\{h_{w,0}:w\in\mathbb R^p\}$. Đọc lại: nhãn $\{0,1\}$, không phải $\pm1$ như UML §9.1; điểm trên siêu phẳng nhận nhãn $1$, và quy ước này được dùng trong chứng minh cận trên; $w=0$ cho hàm hằng ($b\ge0$: hằng $1$; $b<0$: hằng $0$). Ví dụ: $p=1$, lớp afin gồm $\mathbb 1[x\ge t]$, $\mathbb 1[x\le t]$ và hai hàm hằng. Phản ví dụ: hàm $\mathbb 1[0\le x\le2]$ không thuộc $\mathcal H^1_{\mathrm{af}}$, vì trên $(-1,1,3)$ nó cho $(0,1,0)$, cách gán nhãn mà không nửa đường thẳng nào thực hiện được.
2. **Bổ đề 03.8 (Phân hoạch Radon) — chứng minh đầy đủ ở Phụ lục A** (QĐ 5). **Giả thiết.** $p\ge1$; $x_1,\ldots,x_{p+2}\in\mathbb R^p$. **Bảo đảm.** Có hai tập chỉ số khác rỗng, rời nhau $I\cup J=\{1,\ldots,p+2\}$ và một điểm $z\in\operatorname{conv}\{x_i:i\in I\}\cap\operatorname{conv}\{x_j:j\in J\}$; tất định. Trong thân bài: phát biểu, một hình chữ nhật/hình vuông minh họa bằng lời ($p=2$: bốn đỉnh hình vuông, $I$ là một đường chéo, $J$ đường chéo kia, $z$ là tâm), và một câu nói ý chứng minh (hệ $\sum_ia_ix_i=0$, $\sum_ia_i=0$ có $p+1$ phương trình, $p+2$ ẩn). Tên tiếng Anh "định lý Radon (Radon's theorem)" ở lần đầu.
3. **Mệnh đề 03.9 (Chiều VC của lớp nửa không gian) — chứng minh đầy đủ (cận trên của phần (b) ở Phụ lục A)** (blueprint Prop 3.3; QĐ 5). **Giả thiết.** $p\ge1$; hai lớp của Định nghĩa 03.7. **Bảo đảm.** **(a)** $\operatorname{VCdim}(\mathcal H^p_{\mathrm{af}})=p+1$; **(b)** $\operatorname{VCdim}(\mathcal H^p_{\mathrm{tn}})=p$; tất định; phụ thuộc số chiều đặc trưng $p$, không phụ thuộc $m$. **Chứng minh.** Lộ trình: cận dưới bằng nghiệm tường minh trên các đỉnh của một đơn hình (simplex), cận trên bằng Bổ đề 03.8. (a) cận dưới: $C=\{0,\mathbf e_1,\ldots,\mathbf e_p\}$, cách gán nhãn $(y_0,y_1,\ldots,y_p)$; đặt $b=2y_0-1$, $w_i=2y_i-1-b$; khi đó $\langle w,0\rangle+b=2y_0-1$ và $\langle w,\mathbf e_i\rangle+b=2y_i-1$, không âm khi và chỉ khi nhãn là $1$. Một câu: cùng lập luận đúng cho mọi $p+1$ điểm độc lập afin, vì ma trận với các hàng $(x_i^\top,1)$ khả nghịch (Bài tập 03.3). (a) cận trên: cho $p+2$ điểm phân biệt, lấy $I$, $J$, $z$ của Bổ đề 03.8; gán nhãn $1$ trên $I$, $0$ trên $J$. Nếu $h_{w,b}$ thực hiện cách gán nhãn này thì $g(x)=\langle w,x\rangle+b$ là hàm afin, nên $g(z)$ là tổ hợp lồi của các $g(x_i)\ge0$, $i\in I$, và cũng là tổ hợp lồi của các $g(x_j)<0$, $j\in J$; do đó $g(z)\ge0$ và $g(z)<0$, vô lý. **Chỗ dùng quy ước $\ge0$:** phía nghiêm ngặt $<0$ nằm trên $J\ne\varnothing$, nên tổ hợp lồi của các số âm là số âm. (b) cận dưới: $\{\mathbf e_1,\ldots,\mathbf e_p\}$ với $w=\sum_i(2y_i-1)\mathbf e_i$. (b) cận trên: Phụ lục A (phụ thuộc tuyến tính của $p+1$ véc-tơ, hai trường hợp theo dấu các hệ số; PTN §1, dòng Prop 3.3 (ii)). Câu sau $\square$: lớp của khối ứng dụng có $d=11$.
4. **Ví dụ 03.3 (Nửa không gian trong mặt phẳng trên ba và bốn điểm)** (QĐ 9(c); blueprint 3.4 "planar affine separators"). **Thiết lập.** $p=2$, $\mathcal H^2_{\mathrm{af}}$, $d=3$ theo Mệnh đề 03.9. **Bước 1 (ba điểm không thẳng hàng).** $(0,0)$, $(1,0)$, $(0,1)$; tám cách gán nhãn, công thức $b=2y_0-1$, $w_i=2y_i-1-b$; viết một trường hợp, như câu ôn nhanh 2. **Bước 2 (ba điểm thẳng hàng).** $(0,0)$, $(1,0)$, $(2,0)$: cách gán nhãn $(1,0,1)$ không thực hiện được, vì trên đường thẳng chứa ba điểm, $h_{w,b}$ là một nửa đường thẳng; tập này không bị tách trọn dù $d=3$ (Nhận xét 03.4). **Bước 3 (bốn đỉnh hình vuông).** $(0,0)$, $(1,0)$, $(1,1)$, $(0,1)$: cách gán nhãn "XOR" ($1$ tại $(0,0)$ và $(1,1)$, $0$ tại hai đỉnh kia) không thực hiện được; tâm $(\tfrac12,\tfrac12)$ là điểm Radon của hai đường chéo. Cách gán nhãn bù cũng không thực hiện được; mười bốn cách còn lại thực hiện được (liệt kê theo số nhãn $1$: $0$, $1$, $2$ kề nhau, $3$, $4$). **Bước 4 (một điểm trong tam giác).** $(0,0)$, $(3,0)$, $(0,3)$, $(1,1)$: nhãn $1$ ở ba đỉnh, $0$ ở điểm trong không thực hiện được, vì $(1,1)$ là tổ hợp lồi của ba đỉnh. **Kết luận.** Mọi cấu hình bốn điểm đều thiếu ít nhất một cách gán nhãn, khớp $d=3$; lý do chung là Bổ đề 03.8. Ghi chú cho người viết: một hình SVG nhỏ (bốn điểm hình vuông, hai đường chéo) là tùy chọn, có `role="img"` và alt cụ thể; không dùng màu làm tín hiệu duy nhất.
5. **Nhận xét 03.10 (Số tham số và chiều VC)** (QĐ 10; trả lời câu trả lời sai của câu hỏi mở đầu). Ba lớp: **(i)** $\mathcal H^p_{\mathrm{af}}$ có $p+1$ tham số và $d=p+1$; **(ii)** $\mathcal H_{\sin}=\{x\mapsto\mathbb 1[\sin(\theta x)>0]:\theta\in\mathbb R\}$ có một tham số và $d=\infty$: với mọi $k$, tập $\{2^{-1},\ldots,2^{-k}\}$ bị tách trọn (chứng minh là Bài tập 03.5; cách dựng $\theta=\pi(1+\sum_j(1-y_j)2^j)$ chỉ ghi ở bài tập); **(iii)** trên $\mathbb R$, $\{x\mapsto\mathbb 1[(w_1+\cdots+w_p)x\ge0]:w\in\mathbb R^p\}$ có $p$ tham số nhưng chỉ ba hàm $\mathbb 1[x\ge0]$, $\mathbb 1[x\le0]$, hằng $1$, nên $d=1$. Kết luận một câu: số tham số không xác định chiều VC theo chiều nào; với nửa không gian, hai số trùng nhau do cấu trúc tuyến tính. Ở dạng song song ba nhãn in đậm (i)–(iii).

Kết mục bằng văn xuôi: chiều VC cho biết đến cỡ nào lớp tạo ra mọi cách gán nhãn; với $m>d$, Định lý 02.14 cần biết lớp tạo ra bao nhiêu cách gán nhãn trên $m$ điểm, và §6 đếm số này.

### `## 6. Hàm tăng trưởng và bổ đề Sauer–Shelah` (hàm tăng trưởng 15 phút; nghỉ 10 phút; Sauer–Shelah 20 phút)

**Câu mở:** "Định lý 02.14 cộng $K$ biến cố hỏng. Với lớp vô hạn, đại lượng thay cho $K$ là số cách gán nhãn mà lớp tạo ra trên các điểm, lấy trong trường hợp xấu nhất."

1. **Định nghĩa 03.11 (Hàm tăng trưởng)** (QĐ 2). Cho lớp $\mathcal H$ và số nguyên $m\ge1$. *Hàm tăng trưởng* (growth function) của $\mathcal H$ là
   $\Pi_{\mathcal H}(m)=\max_{(x_1,\ldots,x_m)\in\mathcal X^m}\lvert\mathcal H_{(x_1,\ldots,x_m)}\rvert$. Đọc lại (một ý một câu): ở đây $m$ là số điểm, trùng với cỡ mẫu khi áp dụng cho $(X_1,\ldots,X_m)$ và bằng $2m$ ở §7; giá trị lớn nhất lấy trên mọi bộ điểm, không phải trên mẫu quan sát được, nên $\Pi_{\mathcal H}(m)$ tất định và $\lvert\mathcal H_{(X_1,\ldots,X_m)}\rvert\le\Pi_{\mathcal H}(m)$ trên mọi mẫu; bộ cho phép điểm lặp, nên $\Pi_{\mathcal H}$ xác định cả khi $\mathcal X$ có ít hơn $m$ điểm và không giảm theo $m$ (thêm một điểm lặp); $\Pi_{\mathcal H}(m)\le\min\{2^m,\lvert\mathcal H\rvert\}$; $\Pi_{\mathcal H}(m)=2^m$ khi và chỉ khi $m\le d$ (chiều thuận: lấy $m$ điểm của một tập bị tách trọn có $d$ phần tử, dùng tính chất tập con của Định nghĩa 03.2; chiều nghịch: bộ có điểm lặp cho ít hơn $2^m$, bộ không lặp có $m>d$ điểm không bị tách trọn). Ví dụ: Ví dụ 03.2 cho $\Pi_{\mathcal H_{\mathrm{ng}}}(5)\ge6$. Phản ví dụ: số cách gán nhãn trên mẫu cụ thể $\lvert\mathcal H_{(X_1,\ldots,X_m)}\rvert$ là ngẫu nhiên, không phải $\Pi_{\mathcal H}(m)$.
2. **Ví dụ 03.4 (Hàm tăng trưởng của lớp hàm ngưỡng và lớp khoảng)** (blueprint 3.4, bài gốc 1 làm mẫu cho lớp hàm ngưỡng; bài tập chỉ hỏi biến thể trên tập hữu hạn). **Thiết lập.** $\mathcal H_{\mathrm{ng}}$, $\mathcal H_{\mathrm{kh}}$; $m\ge1$ điểm. **Bước 1.** Điểm phân biệt $x_1<\cdots<x_m$: cách gán nhãn của $h_t$ là một dãy $0$ rồi một dãy $1$, xác định bởi số nhãn $1$ từ $0$ đến $m$: $m+1$ cách. **Bước 2.** Bộ có điểm lặp: các điểm trùng nhau nhận cùng nhãn, nên số cách không lớn hơn số cách trên các điểm phân biệt của bộ. **Bước 3.** $\Pi_{\mathcal H_{\mathrm{ng}}}(m)=m+1$. **Bước 4.** Lớp khoảng: cách gán nhãn là một khối liền các nhãn $1$ hoặc toàn $0$; chọn chỉ số đầu $i\le$ chỉ số cuối $i'$: $\binom m2+m=\binom{m+1}2$ cách, thêm cách toàn $0$: $\Pi_{\mathcal H_{\mathrm{kh}}}(m)=\binom{m+1}2+1$. **Bước 5.** Tại $m=5$: $6$ và $16$, so với $32$; tại $m=10$: $11$ và $56$, so với $1024$†. **Kết luận.** Hai hàm tăng trưởng là đa thức bậc $1$ và $2$ theo $m$, đúng bằng chiều VC.
3. **Bổ đề 03.12 (Bổ đề Sauer–Shelah) — phác thảo (chứng minh đầy đủ ở Phụ lục B)** (blueprint Lemma 3.4; QĐ 4). **Giả thiết.** $\mathcal H$ khác rỗng, gồm các hàm $\mathcal X\to\{0,1\}$, chiều VC $d<\infty$; $m\ge1$. **Bảo đảm.** **(a)** $\Pi_{\mathcal H}(m)\le\sum_{j=0}^{d}\binom mj$, với quy ước $\binom mj=0$ khi $j>m$; **(b)** nếu $1\le d\le m$ thì $\sum_{j=0}^{d}\binom mj\le(em/d)^d$. Tất định, tổ hợp; số cách gán nhãn tăng theo đa thức bậc $d$ của $m$. **Chứng minh (thân bài).** Lộ trình của (a): quy nạp kép theo $(m,d)$, tách các cách gán nhãn theo điểm cuối. Cố định bộ $C=(x_1,\ldots,x_m)$, đặt $C'=(x_1,\ldots,x_{m-1})$. Mỗi cách gán nhãn của $\mathcal H_{C'}$ mở rộng được thành một hoặc hai cách gán nhãn của $\mathcal H_C$; gọi $Y_1$ là tập các cách gán nhãn của $C'$ mở rộng được theo cả hai nhãn của $x_m$. Đẳng thức đếm then chốt: $\lvert\mathcal H_C\rvert=\lvert\mathcal H_{C'}\rvert+\lvert Y_1\rvert$. Nếu $Y_1$ tách trọn một tập $B$ các điểm của $C'$ thì $\mathcal H$ tách trọn $B\cup\{x_m\}$, nên "chiều VC" của $Y_1$ không quá $d-1$; giả thiết quy nạp và công thức Pascal cho $\sum_{j\le d}\binom{m-1}j+\sum_{j\le d-1}\binom{m-1}j=\sum_{j\le d}\binom mj$. Trường hợp gốc ($d=0$; $m=1$) và cách coi $Y_1$ là một lớp hàm trên các vị trí của $C'$ (gồm trường hợp $x_m$ trùng một điểm trước, khi $Y_1=\varnothing$) để ở Phụ lục B. (b) chứng minh đầy đủ trong thân bài, trong `aligned`, một quan hệ một dòng:
   $\sum_{j\le d}\binom mj\le\sum_{j\le d}\binom mj(m/d)^{d-j}\le(m/d)^d\sum_{j=0}^m\binom mj(d/m)^j=(m/d)^d(1+d/m)^m\le(m/d)^de^d$; lý do từng dòng: $m/d\ge1$ (dùng $d\le m$); thêm số hạng không âm; khai triển nhị thức; $1+x\le e^x$. Một câu: khi $m<d$, tổng bằng $2^m$ và dạng đóng có thể sai, chẳng hạn $m=1$, $d=3$: $(e/3)^3\approx0{,}744<2$ (QĐ 4). Câu sau $\square$: sau khi qua chiều VC, $\ln\Pi_{\mathcal H}(m)\le d\ln(em/d)$ tăng như $d\ln m$, so với $m\ln2$ của $2^m$. Người viết không chép cách chứng minh "khẳng định mạnh hơn" của UML; nó là Bài tập 03.6.
4. **Ví dụ 03.5 (Ba cách đếm cách gán nhãn).** **Thiết lập.** Các lớp $\mathcal H_{\mathrm{ng}}$ ($d=1$), $\mathcal H_{\mathrm{kh}}$ ($d=2$), $\mathcal H^2_{\mathrm{af}}$ ($d=3$). **Bước 1.** Với $d=1$, tổng Sauer là $1+m$, bằng $\Pi_{\mathcal H_{\mathrm{ng}}}(m)$. **Bước 2.** Với $d=2$, $1+m+\binom m2=\binom{m+1}2+1=\Pi_{\mathcal H_{\mathrm{kh}}}(m)$; cận đạt dấu bằng. **Bước 3.** Nửa không gian phẳng: $\Pi(m)=2^m$ khi $m\le3$; $\Pi(4)\le14$ vì Bổ đề 03.8 cho bốn điểm bất kì hai cách gán nhãn bù nhau không thực hiện được (lập luận của Mệnh đề 03.9 áp dụng cho cả $I\mapsto1$ lẫn $J\mapsto1$), và hình vuông của Ví dụ 03.3 đạt $14$; tổng Sauer cho phép $15$, nên ở đây cận không đạt. **Bước 4.** Bảng (PTN §4; cột $m=10$, $20$ là †):

   | $m$ | 1 | 2 | 3 | 4 | 5 | 8 | 10 | 20 |
   |---|---|---|---|---|---|---|---|---|
   | $\mathcal H_{\mathrm{ng}}$: $m+1$ | 2 | 3 | 4 | 5 | 6 | 9 | 11 | 21 |
   | $\mathcal H_{\mathrm{kh}}$: $\binom{m+1}2+1$ | 2 | 4 | 7 | 11 | 16 | 37 | 56 | 211 |
   | $\mathcal H^2_{\mathrm{af}}$ | 2 | 4 | 8 | 14 | — | — | — | — |
   | Sauer $d=3$ | 2 | 4 | 8 | 15 | 26 | 93 | 176 | 1351 |
   | $2^m$ | 2 | 4 | 8 | 16 | 32 | 256 | 1024 | 1 048 576 |
   | $(em/3)^3$ | — | — | 20,09 | 47,61 | 92,99 | 380,88 | 743,91 | 5951,27 |

   Dòng nửa không gian phẳng chỉ ghi các giá trị chứng minh được trong bài ($m\le4$); công thức cho $m\ge5$ (định lý Cover) nằm ngoài UML nên không đưa vào. Cột $(em/3)^3$ để trống khi $m<3$ (Bổ đề 03.12(b) cần $d\le m$). **Bước 5.** Tại $m=20$: $1351$ so với khoảng một triệu. **Kết luận.** Dạng đóng $(em/d)^d$ lỏng hơn tổng Sauer khi $m$ nhỏ, nhưng đủ để thấy logarit của số cách gán nhãn tăng như $d\ln m$.

Kết mục bằng văn xuôi: với $d$ hữu hạn, $\ln\Pi_{\mathcal H}(m)\le d\ln(em/d)$; nếu số này thay được cho $\ln K$ trong Định lý 02.14, độ lệch đều sẽ có cỡ $\sqrt{d\ln m/m}$.

**Nghỉ giữa giờ 10 phút** (chỉ trong lịch dạy).

### `## 7. Hội tụ đều trên lớp có chiều VC hữu hạn` (30 phút)

**Câu mở:** "Bổ đề 03.12 chặn số cách gán nhãn trên $m$ điểm. Để dùng nó thay cho $K$ trong chứng minh Định lý 02.14, chúng ta cần thêm hai điều: các đại lượng $\sup_{h\in\mathcal H}$ phải đo được, và mỗi biến cố hỏng phải ứng với một giả thuyết cố định đối với mẫu."

1. **Đoạn giả thiết (M)** (QĐ 6; thực hiện Phụ lục A(v) của Bài 01). Một câu nhu cầu: với lớp vô hạn, $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$ là cận trên đúng của vô hạn biến ngẫu nhiên và có thể không đo được. Rồi gạch đầu dòng: **(M) Lớp xấp xỉ được bởi một lớp con đếm được.** Có một lớp con đếm được $\mathcal H_0\subseteq\mathcal H$ sao cho mỗi $h\in\mathcal H$ là giới hạn theo từng điểm của một dãy $h_k\in\mathcal H_0$, tức $h_k(x)\to h(x)$ với mọi $x\in\mathcal X$. Hai câu hệ quả: dưới (M), $\sup_{\mathcal H}\lvert L_S-L_D\rvert=\sup_{\mathcal H_0}\lvert L_S-L_D\rvert$ trên mọi mẫu, vì $L_S(h_k)=L_S(h)$ khi $k$ đủ lớn (chỉ hữu hạn điểm) và $L_D(h_k)\to L_D(h)$ (hội tụ bị chặn); do đó độ lệch đều là cận trên đúng của một họ đếm được, nên đo được. Ghi: không có (M), kết luận có thể sai với lớp bệnh lý (chỉ nói, không dựng ví dụ; PTN §3).
2. **Nhận xét 03.13 (Điều kiện (M) cho các lớp của bài)**. Ba nhãn song song: **Hàm ngưỡng.** $\mathcal H_0$ gồm $h_t$ với $t$ hữu tỉ; với $t$ bất kì lấy dãy hữu tỉ $t_k\uparrow t$ (dãy giảm dần về $t$ hội tụ về $\mathbb 1[x>t]$, sai tại $x=t$). **Khoảng.** $u_k\uparrow u$, $v_k\downarrow v$ hữu tỉ. **Nửa không gian.** $w_k$ hữu tỉ gần $w$ và $b_k$ hữu tỉ hơi lớn hơn $b$ (chi tiết ở Phụ lục D). Thêm một câu: lớp hữu hạn thỏa (M) với $\mathcal H_0=\mathcal H$; điều kiện đo được đồng thời của thuật toán (Định nghĩa 01.4) vẫn là giả thiết riêng cho thuật toán ERM.
3. **Định nghĩa 03.14 (Tính chất hội tụ đều của một lớp)** (QĐ 3; thực hiện lời hứa trong "Quan hệ với giáo trình UML" của Bài 02). Cho $\mathcal X$, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 và lớp $\mathcal H$ thỏa (M). Lớp $\mathcal H$ có *tính chất hội tụ đều* (uniform convergence property) nếu tồn tại hàm $M:(0,1)^2\to\mathbb N$ sao cho với mọi $\epsilon,\delta\in(0,1)$, mọi phân bố $D$ trên $\mathcal X\times\mathcal Y$ và mọi $m\ge M(\epsilon,\delta)$:
   $\Pr_{S\sim D^m}[S\text{ là }\epsilon\text{-đại diện đối với }(\mathcal H,\ell_{0\text{-}1},D)]\ge1-\delta$ (viết biến cố bằng kí hiệu: $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\le\epsilon$, không dùng chữ có dấu trong `\text{}`). Số $m_0\in\mathbb N$ nhỏ nhất để bất đẳng thức đúng với mọi $D$ và mọi $m\ge m_0$ (bằng $\infty$ nếu không có) được kí hiệu $m^{UC}_{\mathcal H}(\epsilon,\delta)$. Danh sách nhãn song song nếu dài (§3a). Đọc lại: thứ tự lượng từ như Định nghĩa 01.18 ($\exists M$ trước $\forall D$); đây là tính chất của lớp, không nhắc tới thuật toán; khác Định nghĩa 02.13 ở chỗ đòi biến cố có xác suất cao với mọi $D$ và mọi $m$ đủ lớn. Ví dụ: lớp hữu hạn chọn trước mẫu có tính chất hội tụ đều, $m^{UC}_{\mathcal H}(\epsilon,\delta)\le\lceil\ln(2K/\delta)/(2\epsilon^2)\rceil$ theo Định lý 02.14(c). Phản ví dụ: ví dụ dưới đây.
4. **Ví dụ 03.6 (Lớp mọi hàm phân lớp đo được trên $[0,1]$)** (QĐ 9(a); nối Mệnh đề 01.15). **Thiết lập.** $\mathcal X=[0,1]$, $\mathcal M_{[0,1]}$ (Ví dụ 01.8), $D$: $X\sim U[0,1]$, $Y=1$. **Bước 1 (chiều VC).** Với tập hữu hạn $C$ và cách gán nhãn bất kì, hàm chỉ thị của tập các điểm nhãn $1$ là hàm Borel, nên thuộc lớp; mọi tập hữu hạn bị tách trọn, $d=\infty$. **Bước 2 (độ lệch).** Với mọi mẫu, $\mathbb 1_F$, $F=\{X_1,\ldots,X_m\}$, có $L_S=0$, $L_D=1$ (Mệnh đề 01.15), nên $\sup_h\lvert L_S(h)-L_D(h)\rvert=1$ chắc chắn. **Bước 3.** Với $\epsilon<1$, biến cố "$S$ là $\epsilon$-đại diện" rỗng với mọi $m$; không có hàm $M$ nào thỏa Định nghĩa 03.14. **Kết luận.** Bỏ chiều VC hữu hạn thì hội tụ đều hỏng với mọi cỡ mẫu. Giữ câu của PTN §5(a): Mệnh đề 01.15(c) vẫn đúng (hàm hằng $1$ là một nghiệm ERM tốt dưới $D$ này); thất bại ở đây là thất bại đều theo phân bố. Về tính đo được: biến cố ở Bước 3 là tập rỗng nên đo được; xem điểm mở 3.
5. **Đoạn vì sao cần mẫu bóng** (bắt buộc, QĐ 1; PTN §2 bước 3; blueprint "Do not simply union bound…"). Hai đến ba câu, văn xuôi: trên mẫu $S$, lớp chỉ có $\lvert\mathcal H_{(X_1,\ldots,X_m)}\rvert\le\Pi_{\mathcal H}(m)$ cách gán nhãn, nhưng không lấy hợp trên các cách gán nhãn này được, vì hai lý do: (i) $L_D(h)$ không xác định bởi cách gán nhãn của $h$ trên $S$ (hai hàm cùng cách gán nhãn trên $S$ có thể có rủi ro kì vọng khác nhau), nên một cách gán nhãn không ứng với một biến cố hỏng duy nhất; (ii) tập các cách gán nhãn phụ thuộc $S$, nên đó là một lớp chọn theo mẫu, đúng chỗ (T4) cấm (Bước 2 của chứng minh Định lý 02.14). Cách sửa: thay $L_D(h)$ bằng rủi ro thực nghiệm trên một mẫu thứ hai độc lập, cỡ $m$; khi đó mọi đại lượng chỉ phụ thuộc $h$ qua cách gán nhãn trên $2m$ điểm.
6. **Đoạn giả thiết (T5).** **(T5) Lớp cố định trước mẫu.** $\mathcal H$, hữu hạn hoặc vô hạn, được chọn trước và không phụ thuộc $S$. Một câu: (T4) là (T5) cộng điều kiện hữu hạn.
7. **Định lý 03.15 (Hội tụ đều trên lớp có chiều VC hữu hạn) — phác thảo (chứng minh đầy đủ ở Phụ lục C)** (blueprint Theorem 3.5; QĐ 1). **Giả thiết** (danh sách): **Mẫu.** $S\sim D^m$ theo (T1), $m\ge1$; **Hàm lỗi.** hàm lỗi 0–1, $\mathcal Y=\{0,1\}$; **Lớp.** $\mathcal H$ thỏa (T5) và (M), chiều VC $d$; **Tham số.** $\delta\in(0,1)$. **Bảo đảm** (danh sách song song, xác suất theo $S\sim D^m$): **(a) Dạng hàm tăng trưởng.** Đặt $\rho_m=\sqrt{8\ln\big(4\Pi_{\mathcal H}(2m)/\delta\big)/m}$, phụ thuộc ngầm vào $\mathcal H$ và $\delta$. Với xác suất ít nhất $1-\delta$, $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert\le\rho_m$; đúng với mọi $m\ge1$ và mọi lớp thỏa (T5), (M). **(b) Dạng chiều VC.** Nếu $1\le d\le m$ thì
   $\rho_m\le\sqrt{8\big(d\ln(2em/d)+\ln(4/\delta)\big)/m}\le4\sqrt{\big(d\ln(em/d)+\ln(2/\delta)\big)/m}$. **(c) Tính chất hội tụ đều.** Nếu $1\le d<\infty$ thì $\mathcal H$ có tính chất hội tụ đều, với $m^{UC}_{\mathcal H}(\epsilon,\delta)\le\big\lceil(16/\epsilon^2)\big(d\ln(32/\epsilon^2)+\ln(4/\delta)\big)\big\rceil$†. Ghi trong **Bảo đảm.**: các vế phải trong (a), (b) được thay bằng $\min\{1,\cdot\}$ vì độ lệch đều không quá $1$; cận xác suất cao cho độ lệch đều giữa đại lượng thực nghiệm và tổng thể; không phụ thuộc $D$; phụ thuộc $m$ qua $\sqrt{\ln m/m}$, phụ thuộc $\delta$ qua $\ln(1/\delta)$. Một câu sau khối: khi $d=\infty$, $\Pi_{\mathcal H}(2m)=2^{2m}$ và $\rho_m\ge\sqrt{16\ln2}\approx3{,}33$†, nên (a) vẫn đúng nhưng không cho gì; khi $d=0$, $\Pi=1$ và (a) cho $\sqrt{8\ln(4/\delta)/m}$.
   **Chứng minh trong thân bài (lộ trình năm bước, không quá khoảng 450 tiếng).** Bất đẳng thức then chốt, viết trong `aligned` cho $\epsilon>0$ với $m\epsilon^2\ge2$:
   $\Pr\big[\sup_h\lvert L_D(h)-L_S(h)\rvert>\epsilon\big]\le2\Pr\big[\sup_h\lvert L_{S'}(h)-L_S(h)\rvert>\epsilon/2\big]\le4\,\Pi_{\mathcal H}(2m)\,e^{-m\epsilon^2/8}$.
   **Bước 1 (mẫu bóng).** $S'=(Z'_1,\ldots,Z'_m)\sim D^m$ độc lập với $S$, chỉ dùng trong chứng minh. Nếu một $h$ lệch hơn $\epsilon$ trên $S$, thì $L_{S'}(h)$ nằm trong $\epsilon/2$ quanh $L_D(h)$ với xác suất điều kiện ít nhất $\tfrac12$ (Bổ đề 02.3 với $\operatorname{Var}\le\tfrac14$, cần $m\epsilon^2\ge2$); do đó hệ số $2$. Chỗ dùng: (T1) (độc lập giữa $S'$ và $S$), hàm lỗi bị chặn (phương sai), (M) (chọn $h$ đo được theo $S$). **Bước 2 (đổi chỗ với dấu ngẫu nhiên).** Đổi $Z_i\leftrightarrow Z'_i$ không đổi phân bố của $(S,S')$, nên $L_{S'}(h)-L_S(h)$ có cùng phân bố, đồng thời theo $h$, với $\frac1m\sum_i\sigma_i\big(\ell(h,Z'_i)-\ell(h,Z_i)\big)$, trong đó $\sigma_i$ độc lập, nhận $\pm1$ với xác suất $\tfrac12$. Chỗ dùng: (T1) (các cặp độc lập cùng phân bố). **Bước 3 (cách gán nhãn trên mẫu gộp).** Khi biết $(S,S')$, đại lượng trên chỉ phụ thuộc $h$ qua cách gán nhãn của $h$ trên bộ $2m$ điểm $(X_1,\ldots,X_m,X'_1,\ldots,X'_m)$, nên có nhiều nhất $\Pi_{\mathcal H}(2m)$ giá trị khác nhau (bộ có thể có điểm lặp; đây là lý do Định nghĩa 03.11 dùng bộ). Chỗ dùng: (T5) (lớp không phụ thuộc mẫu); khác với đoạn "vì sao cần mẫu bóng": nguồn ngẫu nhiên còn lại là $\sigma$, độc lập với các cách gán nhãn. **Bước 4 (Hoeffding và bất đẳng thức hợp).** Với một cách gán nhãn cố định, các số hạng $\sigma_i(\cdot)$ độc lập, kì vọng $0$, nằm trong $[-1,1]$; Định lý 02.7 với Nhận xét 02.8 (miền dài $2$; câu ôn nhanh 3) cho $2e^{-m\epsilon^2/8}$ tại độ lệch $\epsilon/2$; Bổ đề 02.12 trên $\le\Pi_{\mathcal H}(2m)$ cách gán nhãn, rồi lấy kì vọng theo $(S,S')$. **Bước 5 (giải theo $\delta$ và Sauer–Shelah).** Đặt vế phải bằng $\delta$: $\epsilon=\rho_m$; điều kiện $m\rho_m^2=8\ln(4\Pi_{\mathcal H}(2m)/\delta)\ge8\ln4\approx11{,}09>2$ tự thỏa; Bổ đề 03.12(b) tại $2m$ điểm cho (b); hằng số $4$ từ $d\ln(2em/d)\le(1+\ln2)d\ln(em/d)$ và $\ln(4/\delta)\le2\ln(2/\delta)$ (Phụ lục C). (c) từ (b) và bất đẳng thức tiếp tuyến $\ln a\le a/a_0+\ln a_0-1$ (Phụ lục C). Câu sau $\square$: hằng số $8$ đến từ hai nguồn: độ lệch bị chia đôi ở Bước 1 và miền dài $2$ ở Bước 4; đó là giá của mẫu bóng.
8. **Ví dụ 03.7 (Cận độ lệch đều cho $d=3$ và $d=11$)** (cận số bắt buộc; ứng dụng QĐ 11). **Thiết lập.** Lớp $\mathcal H^2_{\mathrm{af}}$ ($d=3$) và lớp của khối ứng dụng $\mathcal H^{10}_{\mathrm{af}}$ ($d=11$, Mệnh đề 03.9); $\delta=0{,}05$; $m=10^3,10^4,10^5$. **Bước 1.** $\ln(4/\delta)=\ln80\approx4{,}3820$. **Bước 2 (một ô đầy đủ).** $d=3$, $m=10^4$: $2em/d=2e\cdot10^4/3\approx18\,122{,}3$; $3\ln18\,122{,}3\approx3\cdot9{,}8049=29{,}415$; $8(29{,}415+4{,}382)/10^4\approx0{,}027037$; căn bậc hai $\approx0{,}1644$. **Bước 3 (bảng).** Dạng trực tiếp / dạng hằng số $4$: $d=3$: $0{,}464/0{,}621$, $0{,}164/0{,}223$, $0{,}0571/0{,}0779$; $d=11$: $0{,}762/1{,}014$ (cắt ở $1$), $0{,}280/0{,}379$, $0{,}0993/0{,}136$. **Bước 4.** Nhân $m$ lên $10$ lần làm cận giảm từ $2{,}7$ đến $2{,}9$ lần†, ít hơn $\sqrt{10}\approx3{,}16$ vì $\ln m$ tăng. **Kết luận.** Với mười chỉ số đo, cận độ lệch đều là $0{,}762$ ở $10^3$ quan sát và $0{,}280$ ở $10^4$ quan sát (cỡ mẫu đủ, không phải cần); dạng hằng số $4$ lớn hơn dạng trực tiếp khoảng $1{,}33$–$1{,}37$ lần (PTN §2).
9. **Ví dụ 03.8 (Hai hàm chọn sau khi xem mẫu)** (QĐ 9(b); bỏ (T5)). **Thiết lập.** $D$ của Ví dụ 03.6; với mẫu $S$, đặt $F=\{X_1,\ldots,X_m\}$ và $\mathcal G_S=\{h_{\equiv0},\mathbb 1_F\}$ (không viết $\mathcal H_S$, dễ đọc thành thu hẹp). **Bước 1.** $\mathcal G_S$ có hai hàm, nên chiều VC không quá $\log_22=1$ (bằng $1$). **Bước 2.** $L_S(\mathbb 1_F)=0$, $L_D(\mathbb 1_F)=1$, nên độ lệch đều bằng $1$ với xác suất $1$. **Bước 3.** Nếu áp dụng sai Định lý 03.15 với $d=1$, $m=1000$, $\delta=0{,}05$: $\rho_m\le0{,}322$ (dạng trực tiếp). **Bước 4 (chỗ hỏng).** Bước 3 của chứng minh: cách gán nhãn của lớp phụ thuộc mẫu. **Kết luận.** Chiều VC nhỏ không đủ; lớp phải cố định trước mẫu. Một câu thêm (QĐ 9): bỏ tính độc lập, như chép lại một quan sát ở Ví dụ 02.6, làm hỏng Bước 1 và Bước 2 của chứng minh; không tính thêm số.

Kết mục bằng văn xuôi: Định lý 03.15 cho độ lệch đều; với ERM, bước còn lại là ba bất đẳng thức như Hệ quả 02.16, nhưng với cận dưới đúng thay cho giá trị nhỏ nhất.

### `## 8. ERM, định lý cơ bản và cận dưới` (ứng dụng và câu hỏi cuối buổi 20 phút)

**Câu mở:** viết theo câu kết của §7, không lặp lại nó; ví dụ: "Với lớp vô hạn, giá trị nhỏ nhất của $L_D$ trên $\mathcal H$ có thể không đạt, nên phép so sánh với phần tử tốt nhất của Hệ quả 02.16 phải viết lại cho mọi $h\in\mathcal H$."

1. **Hệ quả 03.16 (Rủi ro vượt mức của ERM trên lớp có chiều VC hữu hạn) — chứng minh đầy đủ** (blueprint Corollary 3.6; QĐ 7). **Giả thiết** (danh sách): **Mẫu.** (T1), $m\ge1$; **Hàm lỗi.** 0–1; **Lớp.** (T5), (M), chiều VC $d$ với $1\le d<\infty$; **Thuật toán.** theo (O1), một thuật toán ERM bất kì trên $\mathcal H$ thỏa điều kiện đo được của Định nghĩa 01.4, với mọi quy tắc chọn khi bằng nhau; hoặc theo (O2), một $\epsilon_{\mathrm{opt}}$-ERM $A$; **Tham số.** $\delta\in(0,1)$, $\rho_m$ như Định lý 03.15. **Bảo đảm** (song song): **(a) ERM chính xác.** Với xác suất ít nhất $1-\delta$, đồng thời cho mọi nghiệm ERM $\hat h$ trên $S$: $L_D(\hat h)\le\inf_{h\in\mathcal H}L_D(h)+2\rho_m$; khi $d\le m$, có thể thay $\rho_m$ bằng hai vế phải của Định lý 03.15(b). **(b) ERM xấp xỉ.** Trên cùng biến cố, $L_D(A(S))\le\inf_{\mathcal H}L_D+2\rho_m+\epsilon_{\mathrm{opt}}$. **(c) Học PAC bất khả tri.** Mọi thuật toán ERM như trên là thuật toán học PAC bất khả tri (Định nghĩa 01.25) với $M(\epsilon,\delta)=\big\lceil(64/\epsilon^2)\big(d\ln(128/\epsilon^2)+\ln(4/\delta)\big)\big\rceil$†; do đó $\mathcal H$ học được PAC bất khả tri và $m_{\mathcal H}(\epsilon,\delta)\le M(\epsilon,\delta)$ (độ phức tạp mẫu mở rộng sang bất khả tri như sau Hệ quả 02.16). Câu đọc ngay sau khối (M1 của Bài 02): ở (c), $\epsilon$ là mức rủi ro vượt mức, độ lệch đều tương ứng là $\epsilon/2$. Một câu về sự tồn tại: với hàm lỗi 0–1, $L_S$ chỉ nhận các giá trị $0,\frac1m,\ldots,1$, nên giá trị nhỏ nhất trên $\mathcal H$ đạt được và nghiệm ERM tồn tại; điều kiện đo được của thuật toán là giả thiết, không chứng minh. **Chứng minh.** Lộ trình: một bước tất định trên biến cố $r$-đại diện, rồi Định lý 03.15. Bước 1 (tất định, cho mọi $h\in\mathcal H$): nếu $S$ là $r$-đại diện thì $L_D(\hat h)\le L_S(\hat h)+r\le L_S(h)+r\le L_D(h)+2r$; ba chỗ dùng: tính đại diện tại $\hat h$, (O1), tính đại diện tại $h$. Bước 2: vế trái không phụ thuộc $h$, lấy cận dưới đúng theo $h$ được $L_D(\hat h)\le\inf_{\mathcal H}L_D+2r$; **không cần $h_{\mathcal H}$ tồn tại** (khác Bước 1 của chứng minh Hệ quả 02.16). Bước 3: Định lý 03.15(a) với $r=\rho_m$. Bước 4 (phần c): cần $2\rho_m\le\epsilon$; đủ khi $32\big(d\ln(2em/d)+\ln(4/\delta)\big)/m\le\epsilon^2$ và $m\ge d$; với $\kappa=32/\epsilon^2$ và $a_0=4e\kappa$, bất đẳng thức tiếp tuyến $\ln a\le a/a_0+\ln a_0-1$ tại $a=2em/d$ cho $\kappa d\ln(2em/d)\le m/2+\kappa d\ln(4\kappa)$, nên $m\ge2\kappa\big(d\ln(4\kappa)+\ln(4/\delta)\big)$ là đủ (không dùng $A$, trùng thuật toán, hay $c$, trùng hằng số của Định lý 03.19); giá trị này lớn hơn $d$. Câu sau $\square$: hệ số $2$ đến từ hai phép so sánh như ở Bài 02; dạng đóng của $M$ lớn hơn cỡ mẫu nhỏ nhất thỏa điều kiện ẩn từ $1{,}55$ đến $1{,}63$ lần† (Ví dụ 03.9).
2. **Ví dụ 03.9 (Cỡ mẫu cho rủi ro vượt mức $0{,}1$)** (trả lời câu hỏi mở đầu và câu hỏi thực hành của khối ứng dụng). **Thiết lập.** $\epsilon=0{,}1$ (rủi ro vượt mức), $\delta=0{,}05$, mọi thuật toán ERM, mọi phân bố; $d=1$ (lớp hàm ngưỡng), $d=3$ (nửa không gian phẳng, tức hai chỉ số đo), $d=11$ (mười chỉ số đo). **Bước 1 (điều kiện).** $2\rho_m\le0{,}1$ được bảo đảm khi $32(d\ln(2em/d)+4{,}382)/m\le0{,}01$; vế trái giảm theo $m\ge d$, nên cỡ mẫu nhỏ nhất thỏa điều kiện đúng cho mọi $m$ lớn hơn. **Bước 2 (giải số).** Chia đôi khoảng: $54\,330$, $132\,992$, $447\,194$. **Bước 3 (kiểm một ô).** $d=1$: vế trái bằng $0{,}0099999$ tại $m=54\,330$ và $0{,}0100001$ tại $m=54\,329$† (cần bảy chữ số vì vế trái rất gần $0{,}01$). **Bước 4 (dạng đóng của Hệ quả 03.16(c)).** $88\,572$, $209\,624$, $693\,832$†; dạng hằng số $4$ của Định lý 03.15(b) cho $103\,939$, $261\,198$, $889\,572$. **Bước 5 (chỉ ước lượng $\pm0{,}1$, không có hệ số $2$).** Theo Định lý 03.15: $12\,401$†, $29\,646$, $98\,484$. **Kết luận.** Câu trả lời cho câu hỏi mở đầu: theo cận của bài, $54\,330$ quan sát đủ cho lớp hàm ngưỡng, và đủ cho mọi phân bố, mọi thuật toán ERM; chuyển từ hai lên mười chỉ số đo nhân cỡ mẫu khoảng $3{,}36$ lần, gần tỉ số $11/3\approx3{,}67$ của chiều VC (bài gốc 4). Mọi con số là cỡ mẫu đủ, không phải cỡ mẫu cần.
3. **Ví dụ 03.10 (So sánh với lớp hữu hạn sau khi rời rạc hóa)** (QĐ 8; PTN §4). **Thiết lập.** Mỗi tham số thực được lưu bằng $64$ bit, nên lớp đã rời rạc hóa có $K\le2^{64q}$ hàm với $q$ tham số; Hệ quả 02.16(c): $\lceil2\ln(2K/\delta)/\epsilon^2\rceil$, $\epsilon=0{,}1$, $\delta=0{,}05$. **Bước 1.** Một ngưỡng ($q=1$): $\ln(2^{65}/0{,}05)\approx48{,}050$, cỡ mẫu $9611$, so với $54\,330$ ($d=1$). **Bước 2.** Nửa không gian phẳng ($q=3$): $27\,355$†, so với $132\,992$ ($d=3$). **Bước 3.** Mười chỉ số đo ($q=11$): $98\,333$, so với $447\,194$ ($d=11$). **Bước 4.** Sáu hàm ngưỡng, $m=1000$, $\delta=0{,}05$: đường VC cho $\sqrt{8\ln480/1000}\approx0{,}2222$, Định lý 02.14 cho $r_m=\sqrt{\ln240/2000}\approx0{,}0523$. **Bước 5 (nhận xét trung thực, bắt buộc).** Với các hằng số của bài, cỡ mẫu theo đường VC lớn hơn cỡ mẫu của lớp đã rời rạc hóa từ $4{,}5$ đến $5{,}7$ lần†, và bán kính lớn hơn $4{,}25$ lần; hằng số $8$ của mẫu bóng là nguyên nhân chính. Giá trị của cận VC: nó áp dụng cho chính lớp vô hạn, không phụ thuộc cách lưu tham số, không có sai số xấp xỉ do lưới, và đi kèm một điều kiện cần (định lý dưới đây). **Kết luận.** Không viết "cận VC chặt hơn"; viết rằng hai cận trả lời hai câu hỏi khác nhau về cùng một bài toán. Ghi chú cho người viết: QĐ 8 ghép $132\,992$ với $9611$; dàn ý ghép theo cùng số tham số (xem mục 12, điểm mở 1).
4. **Định lý 03.17 (Định lý cơ bản cho phân lớp nhị phân) — đọc thêm** (blueprint "Fundamental theorem [statement only]"; QĐ 6; UML §6.4, §5.1). **Giả thiết** (danh sách): **Bài toán.** $\mathcal X$ có σ-đại số, $\mathcal Y=\{0,1\}$, hàm lỗi 0–1; **Lớp.** $\mathcal H$ khác rỗng, chiều VC $d\in\{0,1,\ldots\}\cup\{\infty\}$; **Thuật toán.** thuật toán học tất định theo Định nghĩa 01.4. **Bảo đảm.** **(a) Điều kiện cần, không cần (M).** Nếu $\mathcal H$ tách trọn một tập có $2m$ phần tử thì với mọi thuật toán $A$ có một phân bố $D$, khả thực đối với $\mathcal H$ và tập trung trên tập đó, sao cho $\Pr_{S\sim D^m}[L_D(A(S))>1/8]\ge1/7$. Do đó nếu $d=\infty$ thì $\mathcal H$ không học được PAC (lấy $\epsilon<1/8$, $\delta<1/7$), nên cũng không học được PAC bất khả tri (Nhận xét 01.26). **(b) Sáu khẳng định tương đương, dưới (M) và với thuật toán ERM đo được.** (1) $\mathcal H$ có tính chất hội tụ đều; (2) mọi thuật toán ERM là thuật toán học PAC bất khả tri; (3) $\mathcal H$ học được PAC bất khả tri; (4) $\mathcal H$ học được PAC; (5) mọi thuật toán ERM là thuật toán học PAC; (6) $d<\infty$. Bảo đảm định tính; khẳng định cho lớp, lượng từ "mọi thuật toán" ở (a), "tồn tại" ở (3), (4). **Đoạn sau khối (không phải chứng minh).** Các chiều đã có trong bài: (6)⇒(1) là Định lý 03.15(c) (với $d=0$: lớp một hàm trên $\mathcal X$, dùng Hệ quả 02.10); (1)⇒(2) là lập luận tất định của Hệ quả 03.16 với $r=\epsilon/2$, $M(\epsilon,\delta)=m^{UC}_{\mathcal H}(\epsilon/2,\delta)$; (2)⇒(3) và (5)⇒(4) theo định nghĩa; (2)⇒(5) và (3)⇒(4) theo Nhận xét 01.26. Chiều (4)⇒(6) là (a), dựa trên định lý không có bữa trưa miễn phí (Nhận xét 01.30; UML §5.1); bài không chứng minh. Hằng số $1/8$, $1/7$ từ PTN §1 (dòng NFL), đã kiểm. Một câu: blueprint nói "dưới điều kiện đo được chuẩn"; ở đây (M) chỉ cần cho chiều đủ.
5. **Hệ quả 03.18 (Lớp mọi hàm phân lớp đo được trên $[0,1]$ không học được PAC) — chứng minh đầy đủ từ Định lý 03.17(a)** (QĐ 6; đóng lời hứa ở Hệ quả 01.29 và Nhận xét 01.21). **Giả thiết.** $\mathcal X=[0,1]$ với σ-đại số Borel, $\mathcal H=\mathcal M_{[0,1]}$, hàm lỗi 0–1. **Bảo đảm.** Không thuật toán học nào (Định nghĩa 01.4) là thuật toán học PAC cho $\mathcal M_{[0,1]}$; cụ thể, với mọi $A$ và mọi $m$ có một phân bố khả thực $D$ với $\Pr[L_D(A(S))>1/8]\ge1/7$. **Chứng minh.** Ví dụ 03.6 Bước 1 cho $d=\infty$, nên lớp tách trọn một tập $2m$ phần tử với mọi $m$; áp dụng Định lý 03.17(a). Câu sau $\square$: Hệ quả 01.29 chỉ bác bỏ một thuật toán ERM dưới một phân bố; ở đây mọi thuật toán đều thất bại dưới một phân bố chọn theo thuật toán; dưới $D$ cố định của Ví dụ 01.8, hàm hằng $1$ vẫn học được (Mệnh đề 01.15(c)).
6. **Định lý 03.19 (Cận dưới cho độ phức tạp mẫu) — đọc thêm** (QĐ 6; PTN §6; UML §6.4 và §28.2 (chỉ phần bất khả tri; UML không chứng minh phần khả thực); đóng lời hứa ở Nhận xét 02.18 và Nhận xét 01.21). **Giả thiết.** Bài toán như Định lý 03.17; lớp $\mathcal H$ có chiều VC $d$. **Bảo đảm.** Có các hằng số phổ quát $c>0$ và $\epsilon_0,\delta_0\in(0,1)$ sao cho với mọi $\epsilon\in(0,\epsilon_0)$, $\delta\in(0,\delta_0)$, mọi thuật toán học $A$ và mọi cỡ mẫu $m$: **(a) Bất khả tri.** Nếu $1\le d<\infty$ và $m<c\,(d+\ln(1/\delta))/\epsilon^2$ thì có một phân bố $D$ trên $\mathcal X\times\{0,1\}$ với $\Pr_{S\sim D^m}[L_D(A(S))>\inf_{\mathcal H}L_D+\epsilon]>\delta$. **(b) Khả thực.** Nếu $2\le d<\infty$ và $m<c\,(d+\ln(1/\delta))/\epsilon$ thì có một phân bố $D$ khả thực đối với $\mathcal H$ với $\Pr[L_D(A(S))>\epsilon]>\delta$. Lượng từ: mọi thuật toán, tồn tại phân bố (Nhận xét 01.21: cận dưới phải lập luận cho mọi thuật toán). Không chứng minh; giữ $c$, $\epsilon_0$, $\delta_0$ dạng kí hiệu; không trích hằng số $512$ của UML. Đoạn sau khối (hai câu): theo (a), tốc độ $1/\epsilon^2$ trong trường hợp bất khả tri là cần thiết, trả lời câu bỏ ngỏ của Nhận xét 02.18; cận trên của bài, $M(\epsilon,\delta)$ ở Hệ quả 03.16(c), lớn hơn cận dưới một thừa số $\ln(1/\epsilon)$, và bỏ thừa số này cần kỹ thuật xích (chaining), ngoài phạm vi (UML §28.1). Điều kiện $d\ge2$ ở (b): khi $\mathcal X$ chỉ có một điểm và $\mathcal H$ gồm hai hàm ($d=1$), một quan sát xác định nhãn, nên số hạng $\ln(1/\delta)/\epsilon$ không đúng (PTN §6; chỉ ghi nếu còn chỗ).

Kết mục bằng văn xuôi: chiều VC hữu hạn vừa đủ vừa cần cho học PAC trong phân lớp nhị phân, và trong trường hợp bất khả tri, cỡ mẫu cần thiết tỉ lệ với $d/\epsilon^2$, sai khác cận trên của bài một thừa số $\ln(1/\epsilon)$; cận chỉ nói về lớp, không về một thuật toán hay một phân bố cụ thể.

### `## 9. Ý nghĩa, tác động và giới hạn` (văn xuôi, 4–5 đoạn ngắn, không nhãn)

Nội dung ở mục 5 của dàn ý.

### `## 10. Bài tập`, `## 11. Câu hỏi cuối buổi và cầu nối`, `## 12. Tài liệu đọc`

Theo mục 4, 6, 7. Câu về Bài 04 chỉ nằm ở §11. §10 mở bằng liên kết `material-viewer.html?doc=materials/lec-03/exercises.md` và một dòng mỗi bài (tên, mục tiêu đo), như Bài 02.

### `## Phụ lục`

Theo mục 8.

## 4. Kế hoạch bài tập (`exercises.md`, viết sau khi ghi chú qua rà soát)

Danh sách ở §10 của ghi chú: một dòng mỗi bài (tên, mục tiêu đo). Đề, gợi ý tăng dần, lời giải đầy đủ theo §7a trong `exercises.md`; bài gốc và bài UML tách riêng (QĐ 13). Mức: KN khái niệm, TT tính toán, CM chứng minh, GT kiểm tra giả thiết, TN thực nghiệm tùy chọn. Bài UML: tự giải trước, rồi mới đối chiếu bản lời giải; các chỗ hổng đã biết ghi trong PTN §7.

**Bài gốc (blueprint 3.5).**

1. **Bài tập 03.1 (Hàm tăng trưởng của lớp hàm ngưỡng trên tập hữu hạn)** — mục tiêu 2; TT+CM; dễ. Blueprint bài 1, đổi biến thể vì ghi chú đã tính $\Pi_{\mathcal H_{\mathrm{ng}}}(m)=m+1$ (Ví dụ 03.4). (a) Lớp sáu hàm ngưỡng trên $\{1,\ldots,5\}$: $\Pi(m)=\min\{m+1,6\}$, vì bộ điểm được phép lặp; $\Pi(3)=4$, $\Pi(8)=6$. (b) So với tổng Sauer $m+1$: bằng nhau khi và chỉ khi $m\le5$. (c) Hàm ngưỡng hai phía $\{\mathbb 1[x\ge t]\}\cup\{\mathbb 1[x\le t]\}$ trên $\mathbb R$: $d=2$ và $\Pi(m)=2m$† ($m\ge1$), nhỏ hơn tổng Sauer $\binom{m+1}2+1$ khi $m\ge3$ ($6<7$ tại $m=3$).
2. **Bài tập 03.2 (Chiều VC của lớp khoảng bằng hai chiều lập luận)** — mục tiêu 1; CM; dễ–vừa. (a) Khoảng mở $(u,v)$, $u<v$: $d=2$ (cách gán nhãn toàn $0$ vẫn thực hiện được trên tập hữu hạn). (b) Hợp của hai khoảng đóng: $d=4$†; bốn điểm bị tách trọn vì mọi cách gán nhãn có nhiều nhất hai khối $1$; năm điểm thiếu $(1,0,1,0,1)$. (c) Chỉ ra phần còn thiếu của một lời giải cho (b) chỉ vẽ bốn điểm.
3. **Bài tập 03.3 (Cận dưới cho nửa không gian afin qua điểm độc lập afin)** — mục tiêu 1; CM+TT; vừa. Ghi chú đã làm đỉnh đơn hình; bài yêu cầu: (a) mọi $p+1$ điểm độc lập afin bị $\mathcal H^p_{\mathrm{af}}$ tách trọn (ma trận các hàng $(x_i^\top,1)$ khả nghịch; giải $\langle w,x_i\rangle+b=2y_i-1$); (b) $p=3$, điểm $0,\mathbf e_1,\mathbf e_2,\mathbf e_3$, cách gán nhãn $(0,1,0,1)$: $b=-1$, $w=(2,0,2)$†; (c) cận dưới $p$ cho nửa không gian thuần nhất. Ghi: Bài tập 03.12 (UML 9.6) dùng lại (a); người viết bài tập nói rõ chỗ trùng.
4. **Bài tập 03.4 (So sánh cỡ mẫu cho hai chiều VC)** — mục tiêu 3, 4; TT+KN; vừa. (a) $d=3$ và $d=11$, $\epsilon=0{,}1$ (rủi ro vượt mức), $\delta=0{,}05$: dạng trực tiếp $132\,992$ và $447\,194$, tỉ số $3{,}36<11/3\approx3{,}67$; dạng hằng số $4$: $261\,198$ và $889\,572$ (tỉ số $3{,}41$); dạng đóng của Hệ quả 03.16(c): $209\,624$ và $693\,832$ (tỉ số $3{,}31$†). (b) Giải thích vì sao tỉ số nhỏ hơn $11/3$: số hạng $\ln(4/\delta)$ không nhân với $d$, và $\ln(2em/d)$ giảm khi $d$ tăng. (c) $\epsilon=0{,}05$: $589\,118$ và $1\,999\,657$; giảm $\epsilon$ một nửa nhân cỡ mẫu khoảng $4{,}4$ lần ($1/\epsilon^2$ cộng logarit). (d) Đo mục tiêu 3: chỉ ra bước nào của chứng minh Định lý 03.15 sinh ra hệ số $8$ trong $\rho_m$, và kiểm rằng dùng Hoeffding thay Chebyshev ở Bước 1 (cần $m\epsilon^2\ge2\ln4\approx2{,}77$) cho cùng bán kính, vì $m\rho_m^2\ge8\ln4\approx11{,}09$ (PTN §2 bước 1).
5. **Bài tập 03.5 (Số tham số không xác định chiều VC)** — mục tiêu 5; CM+KN; vừa–khó. (a) $\mathcal H_{\sin}$ tách trọn $\{2^{-1},\ldots,2^{-k}\}$ với $\theta=\pi\big(1+\sum_{j=1}^k(1-y_j)2^j\big)$ (PTN §4: phần nguyên của $\theta x_i/\pi$ có tính chẵn lẻ $1-y_i$, phần lẻ nằm trong $(0,1)$; đã kiểm bằng số hữu tỉ chính xác với $k\le8$†). (b) Lớp $\mathbb 1[(w_1+\cdots+w_p)x\ge0]$ có $d=1$. (c) Lớp hữu hạn có $d\le\log_2\lvert\mathcal H\rvert$ dù có bao nhiêu tham số. (d) Viết lại câu trả lời sai của câu hỏi mở đầu và bác bỏ nó bằng (a), (b).
6. **Bài tập 03.6 (Tùy chọn: một cách chứng minh khác của bổ đề Sauer–Shelah)** — mục tiêu 2; CM; khó. (a) Chứng minh $\lvert\mathcal H_C\rvert\le\#\{B\subseteq C:\mathcal H\text{ tách trọn }B\}$ cho tập hữu hạn $C$ bằng quy nạp theo $\lvert C\rvert$ (cách của UML §6.5.1, viết bằng lập luận riêng), rồi suy ra Bổ đề 03.12(a). (b) Dạng đóng sai khi $m<d$: $d=3$, $m=1$: $0{,}744<2$; $d=10$, $m=5$: $(e/2)^{10}\approx21{,}5<32$†. Blueprint bài 6 cho phép chọn giữa Sauer và cận trên nửa không gian; Phụ lục A, B của ghi chú đã có cả hai chứng minh, nên bài hỏi một chứng minh khác.

**Bài chọn từ UML** (số bài theo PTN §7; đánh số theo thứ tự UML như Bài 01–02; UML viết $d$ cho số chiều đặc trưng, bài viết $p$).

7. **Bài tập 03.7 (Chiều VC của hai lớp trên tập hữu hạn; UML Bài tập 6.2)** — mục tiêu 1; CM; dễ–vừa. (a) Hàm có đúng $k$ nhãn $1$: $\min\{k,\lvert\mathcal X\rvert-k\}$. (b) Hàm có nhiều nhất $k$ nhãn $1$ hoặc nhiều nhất $k$ nhãn $0$: $\min\{2k+1,\lvert\mathcal X\rvert\}$ (bản lời giải sai ở (b)).
8. **Bài tập 03.8 (Bốn trường hợp dấu bằng của bổ đề Sauer–Shelah; UML Bài tập 6.4)** — mục tiêu 2; KN+CM; vừa. Viết theo hàm tăng trưởng trên bộ điểm; ví dụ của PTN §7 (hàm ngưỡng; hình cầu đồng tâm; hình chữ nhật trên ba điểm thẳng hàng; nửa không gian thuần nhất với $\mathbf e_1,\mathbf e_2,\mathbf e_1+\mathbf e_2$: $6<7<8$).
9. **Bài tập 03.9 (Hình chữ nhật song song với trục trong $\mathbb R^p$; UML Bài tập 6.5)** — mục tiêu 1; CM; vừa. $d=2p$; nối Bài tập 02.7 và câu hỏi cuối buổi (trường hợp $p=2$); sửa câu chuồng bồ câu của bản lời giải như PTN §7.
10. **Bài tập 03.10 (Lớp hội Boole; UML Bài tập 6.6, ý 1–3 và 5; ý 4 là thử thách)** — mục tiêu 1; CM; vừa–khó. $\lvert\mathcal H\rvert\le3^p+1$, $d\le p\log_23$, tách trọn $\mathbf e_1,\ldots,\mathbf e_p$, hội đơn điệu có $d=p$; thử thách $d\le p$. Nối Bài tập 02.8; bản lời giải viết sai $p\log_23$ ở (b).
11. **Bài tập 03.11 (Chiều VC vô hạn kéo theo không học được PAC; UML Bài tập 6.10)** — mục tiêu 5; CM; vừa. Chứng minh chiều cần của Định lý 03.17(a) mà ghi chú chỉ phát biểu; hằng số theo lời giải tự làm (bản lời giải dùng $\epsilon=1/16$, $\delta=1/14$).
12. **Bài tập 03.12 (Hình cầu đóng trong $\mathbb R^p$; UML Bài tập 9.6)** — mục tiêu 1; CM; vừa. Nâng $x\mapsto(x,\lVert x\rVert^2)$ và Mệnh đề 03.9 cho $d\le p+2$; $0,\mathbf e_1,\ldots,\mathbf e_p$ cho $d\ge p+1$ với bán kính chọn đúng (bản lời giải đổi chỗ hai bán kính; PTN §7).
13. **Bài tập 03.13 (Tùy chọn, thử thách: $\lceil\sin(\theta x)\rceil$; UML Bài tập 6.8)** — mục tiêu 5; CM; khó. Chỉ giữ nếu Bài tập 03.5(a) dùng cách dựng khác; nếu trùng, bỏ (điểm mở 6).

Mục tiêu được đo: 1 (03.2, 03.3, 03.7, 03.9, 03.10, 03.12); 2 (03.1, 03.6, 03.8); 3 (03.4(d)); 4 (03.4); 5 (03.5, 03.11, 03.13). Bài thực nghiệm tùy chọn không đặt (blueprint 3.5 không có).

## 5. Ý nghĩa, tác động và giới hạn (§9 của ghi chú)

Thứ tự đoạn, mỗi đoạn kết bằng một đại lượng cụ thể (van-phong §8):

1. **Lớp vô hạn học được.** Trả lời câu hỏi mở đầu: với lớp hàm ngưỡng, $54\,330$ quan sát đủ cho rủi ro vượt mức $0{,}1$ với độ tin cậy $0{,}95$, mọi phân bố, mọi nghiệm ERM; $\ln\lvert\mathcal H\rvert$ được thay bằng $\ln\Pi_{\mathcal H}(2m)\le d\ln(2em/d)$. Định lý 03.15 là bảo đảm cho lớp, Hệ quả 03.16 cho mọi thuật toán ERM.
2. **Chiều VC, không phải số tham số.** Nhận xét 03.10; với hàm phân lớp tuyến tính, $d=p+1$, nên cỡ mẫu đủ tăng gần tuyến tính theo số đặc trưng ($3{,}36$ lần khi từ hai lên mười chỉ số đo).
3. **Tính bảo thủ và so sánh trung thực.** Hằng số $8$ của mẫu bóng; Ví dụ 03.10 (cỡ mẫu của lớp sau khi rời rạc hóa nhỏ hơn $4{,}5$–$5{,}7$ lần); giá trị của cận VC là áp dụng cho chính lớp vô hạn và đi kèm điều kiện cần (Định lý 03.17). Phân tích VC kiểm soát cả lớp và mọi phân bố, nên có thể lỏng cho một thuật toán hay một phân bố cụ thể (blueprint 3.4); Định lý 03.19 chỉ nói tốc độ $d/\epsilon^2$ là cần thiết trong trường hợp xấu nhất.
4. **Phạm vi.** Chỉ phân lớp nhị phân với hàm lỗi 0–1; bài toán nhiều lớp (multiclass) cần các đại lượng khác, hàm lỗi bình phương và hàm lỗi log cần lập luận khác (QĐ 12; Nhận xét 02.11); bài không xét chi phí tính toán của ERM trên nửa không gian. Không dẫn chiều Natarajan hay nguồn ngoài UML.
5. **Các giả thiết.** (T5): lớp chọn sau khi xem mẫu làm hỏng cận dù $d=1$ (Ví dụ 03.8, $1$ so với $0{,}322$); (T1): Ví dụ 02.6; (M): cần cho chiều đủ của Định lý 03.17.
6. **Điều không khẳng định.** Cận không phải tốc độ tốt nhất (thừa số $\ln(1/\epsilon)$ so với Định lý 03.19); không nói ERM tính được hiệu quả; không so sánh với Rademacher (Bài 07).

## 6. Câu hỏi cuối buổi và cầu nối

**Câu hỏi** (blueprint 3.6: "What is missing from a proposed proof that only draws a shattered set?"; viết đúng như sau, có thể sửa chữ nhỏ):

> Một lời giải khẳng định lớp hình chữ nhật song song với trục $\mathcal H_{\mathrm{rec}}$ của Bài tập 02.7 có chiều VC bằng $4$. Lời giải vẽ bốn điểm $(1,0)$, $(0,1)$, $(-1,0)$, $(0,-1)$ và mười sáu hình chữ nhật, mỗi hình thực hiện một cách gán nhãn. Lời giải còn thiếu phần nào? Viết phần thiếu đó.
>
> **Câu hỏi phụ.** Bốn đỉnh của hình vuông đơn vị không bị $\mathcal H_{\mathrm{rec}}$ tách trọn. Điều này có mâu thuẫn với kết luận $d=4$ không?

*Lời giải (khối `solution`).* Hình vẽ chỉ cho $d\ge4$ (cận dưới, Nhận xét 03.4). Phần thiếu là cận trên: mọi tập năm điểm không bị tách trọn. Với năm điểm phân biệt, chọn một điểm có hoành độ nhỏ nhất, một điểm có hoành độ lớn nhất, một điểm có tung độ nhỏ nhất, một điểm có tung độ lớn nhất (nhiều nhất bốn điểm); còn ít nhất một điểm $x$. Gán nhãn $1$ cho các điểm đã chọn, $0$ cho $x$. Mọi hình chữ nhật chứa các điểm đã chọn chứa hình chữ nhật nhỏ nhất bao chúng, và hình này chứa $x$; hàm $h_\varnothing$ gán $0$ cho mọi điểm. Vậy cách gán nhãn này không thực hiện được, và $d=4$. Câu phụ: không mâu thuẫn; một tập bốn điểm không bị tách trọn không chứng minh gì về cận trên (Nhận xét 03.4); với hình vuông, cách gán nhãn $1$ ở hai đỉnh đối diện, $0$ ở hai đỉnh còn lại không thực hiện được. Ghi cho người viết: bài trùng trường hợp $p=2$ của Bài tập 03.9; Bài tập 03.9 nói rõ điều này.

**Cầu nối sang Bài 04** (một đoạn, không có nội dung SRM; blueprint 3.6 và Bài 4 §4.1–4.2): thay hai chỉ số đo bằng mười chỉ số đo làm lớp giàu hơn; rủi ro tốt nhất trong lớp $\inf_{\mathcal H}L_D$ không tăng (mỗi hàm phân lớp tuyến tính trên hai chỉ số cũng là một hàm trên mười chỉ số, với hệ số $0$ cho tám chỉ số còn lại), nhưng cận độ lệch đều ở $m=10^4$ tăng từ $0{,}164$ lên $0{,}280$ (Ví dụ 03.7). Câu hỏi cho Bài 04: với một cỡ mẫu cho trước, chọn lớp nào giữa các lớp lồng nhau như vậy? Không đặt tên "sai số xấp xỉ", "sai số ước lượng", "SRM" ngoài một cụm "Bài 04 tách hai phần này" nếu cần (QĐ 12).

## 7. Tài liệu đọc (theo mục UML)

- **Trước buổi học:** UML §6.1–6.3 (lớp vô hạn có thể học được; chiều VC; các ví dụ).
- **Sau buổi học:** UML §6.4–6.5 (định lý cơ bản; chứng minh, gồm bổ đề Sauer và hội tụ đều), §9.1 (nửa không gian, chiều VC của nửa không gian), §5.1 (phát biểu định lý không có bữa trưa miễn phí); các bài tập UML §6.8, §9.6 đã chọn ở §10.
- **Mở rộng:** UML Chương 28 (§28.1 cận hội tụ đều qua độ phức tạp Rademacher, chuẩn bị Bài 07; §28.2 cận dưới cho trường hợp bất khả tri; §28.3 cận trên cho trường hợp khả thực — sửa của điều phối viên 2026-10-31, `reviews/0-quyet-dinh.md` N3).

**Quan hệ với giáo trình UML** (danh sách, như Bài 02; chỉ khác biệt thật):

- **Quy ước lớp.** Hàm ngưỡng $\mathbb 1[x\ge t]$ (UML dùng $\mathbb 1[x<a]$); khoảng đóng; nửa không gian nhãn $\{0,1\}$ với quy ước $\ge0$, chứng minh cận trên xử lý phía nghiêm ngặt.
- **Hàm tăng trưởng.** Lấy cực đại trên bộ điểm, cho phép lặp, thay cho tập điểm.
- **Bổ đề Sauer–Shelah.** Dạng đóng $(em/d)^d$ với $1\le d\le m$, chứng minh hai dòng; quy nạp kép theo $(m,d)$ thay cho khẳng định mạnh hơn.
- **Hội tụ đều.** Cận xác suất cao qua bổ đề mẫu bóng (Chebyshev) và Hoeffding với miền dài $2$, hằng số tường minh, phụ thuộc $\ln(1/\delta)$; UML §6.5 chặn kì vọng rồi dùng bất đẳng thức Markov, nên phụ thuộc $1/\delta$. Không nói UML sai (QĐ 1).
- **Nửa không gian.** Cận trên qua định lý Radon, chứng minh ở Phụ lục A; UML §9.1 dùng phụ thuộc tuyến tính sau khi nâng chiều.
- **Tính đo được.** Điều kiện (M) nêu rõ và kiểm cho các lớp của bài.
- **ERM, định lý cơ bản, cận dưới.** Bảo đảm cho ERM với cận dưới đúng; định lý cơ bản tách điều kiện cần (không cần (M)); cận dưới phát biểu với miền $\epsilon<\epsilon_0$, $\delta<\delta_0$ và $d\ge2$ cho phần khả thực.

## 8. Phụ lục (≤ 3 000 tiếng; QĐ 14)

- **A. Phân hoạch Radon và cận trên cho nửa không gian thuần nhất** (chứng minh đầy đủ, khoảng 550 tiếng). Radon: hệ $\sum_ia_ix_i=0$, $\sum_ia_i=0$ ($p+1$ phương trình, $p+2$ ẩn) có nghiệm khác $0$; $I=\{i:a_i>0\}$ khác rỗng và $J=\{j:a_j\le0\}$ chứa mọi chỉ số âm nên khác rỗng, vì $\sum_ia_i=0$ và các $a_i$ không đồng thời bằng $0$; $A=\sum_{i\in I}a_i>0$; $z=\sum_{i\in I}(a_i/A)x_i=\sum_{j\in J}(-a_j/A)x_j$, các hệ số không âm và có tổng $1$ (hai tập $I$, $J$ là phân hoạch thật, khác PTN chỗ $J=\{a_j<0\}$). Thuần nhất: $p+1$ véc-tơ phụ thuộc tuyến tính, $\sum_ia_ix_i=0$, đổi dấu để có hệ số dương; $I=\{a_i>0\}$, $J=\{a_i<0\}$; nếu $J\ne\varnothing$, gán $I\mapsto1$, $J\mapsto0$: $0\le\sum_Ia_i\langle w,x_i\rangle=\sum_J\lvert a_j\rvert\langle w,x_j\rangle<0$; nếu $J=\varnothing$, gán $0$ cho $I$: $0>\sum_Ia_i\langle w,x_i\rangle=0$. Câu cuối nối về Mệnh đề 03.9(b).
- **B. Bổ đề Sauer–Shelah, chứng minh đầy đủ** (khoảng 650 tiếng). Khẳng định $P(m)$: với mọi $d\ge0$, mọi lớp có chiều VC $\le d$ và mọi bộ $m$ điểm, $\lvert\mathcal H_C\rvert\le\sum_{j\le d}\binom mj$. Trường hợp $d=0$ với mọi $m$ ($\le1$, vì hai cách gán nhãn khác nhau tại một điểm sẽ tách trọn điểm đó); gốc $m=1$; bước quy nạp với $Y_1$ coi là lớp hàm trên các điểm phân biệt của $C'$; trường hợp $x_m$ trùng một điểm trước ($Y_1=\varnothing$); công thức Pascal; lấy cực đại trên bộ điểm.
- **C. Chứng minh đầy đủ Định lý 03.15** (khoảng 1 300 tiếng; PTN §2, đã được điều phối viên kiểm). C.1 tính đo được qua (M), chọn $h_S$ là phần tử đầu tiên của một liệt kê $\mathcal H_0$ có độ lệch lớn hơn $\epsilon$; C.2 bổ đề mẫu bóng với $m\epsilon^2\ge2$ (Chebyshev có điều kiện, $\operatorname{Var}\le\tfrac14$, xác suất $\ge\tfrac12$; viết $\operatorname{Var}$, không dùng $\sigma^2$); C.3 đổi chỗ và dấu ngẫu nhiên; C.4 lấy điều kiện theo $(S,S')$, nhiều nhất $\Pi_{\mathcal H}(2m)$ véc-tơ $(a_i(h))_i$, Hoeffding với Nhận xét 02.8 ($2e^{-m\epsilon^2/8}$), bất đẳng thức hợp, lấy kì vọng; C.5 ghép, giải theo $\delta$, điều kiện $m\rho_m^2\ge8\ln4$ tự thỏa, cắt ở $1$; C.6 Sauer tại $2m$ (cần $d\le2m$) và hằng số $4$; C.7 phần (c) bằng $\ln a\le a/a_0+\ln a_0-1$ với $\kappa=8/\epsilon^2$, $a_0=4e\kappa$: $m\ge2\kappa(d\ln(4\kappa)+\ln(4/\delta))=(16/\epsilon^2)(d\ln(32/\epsilon^2)+\ln(4/\delta))$.
- **D. Điều kiện (M) cho nửa không gian** (khoảng 350 tiếng). $w_k$ hữu tỉ với $\lVert w_k-w\rVert\le1/k^2$, $b_k$ hữu tỉ trong $[b+1/k,b+2/k]$; điểm trên biên: $\langle w_k,x\rangle+b_k\ge-\lVert x\rVert/k^2+1/k\ge0$ khi $k\ge\lVert x\rVert$; điểm ngoài biên: dấu đúng khi $k$ đủ lớn (PTN §3). Một câu: thuật toán ERM trên lớp vô hạn vẫn cần điều kiện đo được của Định nghĩa 01.4, được giả sử.
- Không đưa vào Phụ lục: chứng minh định lý không có bữa trưa miễn phí, cận dưới, định lý Cover, kỹ thuật xích.

## 9. Thuật ngữ mới (chưa có trong `thuat-ngu.md`; điều phối viên bổ sung §7 trước khi viết)

`thuat-ngu.md` §7 đã có: chiều VC, thu hẹp, cách gán nhãn, tách trọn, hàm tăng trưởng, bổ đề Sauer–Shelah, hàm ngưỡng, khoảng, hàm phân lớp tuyến tính, nửa không gian afin, độc lập afin, định lý Radon, đối xứng hóa, mẫu bóng; §6 đã có hội tụ đều ("tính chất hội tụ đều" của lớp), mẫu $\epsilon$-đại diện. "Tách trọn" và "mẫu bóng" còn ghi "còn mở" ở §14: cần chốt (điểm mở 8). Đề xuất thêm:

| English | Đề xuất | Ghi chú |
|---|---|---|
| realized labeling | cách gán nhãn thực hiện được | Định nghĩa 03.1 |
| uniform deviation | độ lệch đều | $\sup_{h}\lvert L_S(h)-L_D(h)\rvert$ |
| homogeneous halfspace | nửa không gian thuần nhất | Định nghĩa 03.7 |
| hyperplane | siêu phẳng | |
| simplex (vertices of a) | đỉnh của một đơn hình | Mệnh đề 03.9 |
| convex combination; convex hull | tổ hợp lồi; bao lồi | $\operatorname{conv}$ |
| Radon partition | phân hoạch Radon | Bổ đề 03.8; tên định lý giữ "định lý Radon" |
| linear dependence | phụ thuộc tuyến tính | Phụ lục A |
| binomial coefficient; Pascal's rule; double induction | hệ số nhị thức; công thức Pascal; quy nạp kép | Bổ đề 03.12 |
| measurability condition; countable subclass; pointwise limit | điều kiện đo được; lớp con đếm được; giới hạn theo từng điểm | (M) |
| uniform convergence sample size | hàm cỡ mẫu hội tụ đều | $m^{UC}_{\mathcal H}$ |
| combined (double) sample | mẫu gộp | bộ $2m$ điểm trong chứng minh |
| random signs | dấu ngẫu nhiên | $\sigma_i$; tên "biến Rademacher" để Bài 07 |
| swapping (in symmetrization) | đổi chỗ | Bước 2 |
| fundamental theorem (of PAC learning) | định lý cơ bản | Định lý 03.17 |
| discretization | rời rạc hóa | Ví dụ 03.10 |
| chaining | kỹ thuật xích (chaining) | chỉ một lần, sau Định lý 03.19 |
| multiclass classification | phân lớp nhiều lớp | §9 |
| lower bound on sample complexity | cận dưới cho độ phức tạp mẫu | Định lý 03.19 |

## 10. Kí hiệu mới (đối chiếu `ky-hieu.md`)

| Kí hiệu | Nghĩa | Lý do / xung đột tránh |
|---|---|---|
| $C=(x_1,\ldots,x_k)$, $k$ | bộ điểm, số điểm | $C$ chỉ là bộ hay tập điểm; hằng số của Định lý 03.15 viết thẳng $4$ |
| $\mathcal H_C$ | thu hẹp của $\mathcal H$ lên $C$ | thêm vào `ky-hieu.md`; không đặt chỉ số $S$ cho lớp khác (Ví dụ 03.8 dùng $\mathcal G_S$) |
| $\operatorname{VCdim}(\mathcal H)$ | chiều VC khi có nhiều lớp | $d$ vẫn là kí hiệu chính |
| $\mathcal H_{\mathrm{ng}}$, $\mathcal H_{\mathrm{kh}}$, $h_{u,v}$ | lớp hàm ngưỡng, lớp khoảng $\mathbb 1[u\le x\le v]$ | không dùng $[a,b]$ vì $b$ của nửa không gian; điểm mở 5 |
| $\mathcal H^p_{\mathrm{af}}$, $\mathcal H^p_{\mathrm{tn}}$, $h_{w,b}$ | nửa không gian afin, thuần nhất | $p$ là số chiều đặc trưng, không viết $d$ như UML |
| $\mathbf e_i$ | véc-tơ đơn vị thứ $i$ của $\mathbb R^p$ | in đứng để khác $e$ trong $(em/d)^d$; điểm mở 4 |
| $\operatorname{conv}$; $I$, $J$, $z$ | bao lồi; phân hoạch và điểm Radon | $I$, $J$, $z$ chỉ trong Bổ đề 03.8, Mệnh đề 03.9, Phụ lục A |
| $\mathcal H_{\sin}$, $\theta$ | lớp $\mathbb 1[\sin(\theta x)>0]$ | $\theta$ cục bộ (Bài 02 dùng $\theta$ ở Phụ lục A) |
| $\mathcal M_{[0,1]}$ | $\mathcal M_{\mathcal X}$ với $\mathcal X=[0,1]$ | kí hiệu của Bài 01 |
| (M), $\mathcal H_0$ | điều kiện đo được, lớp con đếm được | chỉ số dãy $k$ trong (M) chỉ dùng cục bộ |
| (T5) | lớp cố định trước mẫu, có thể vô hạn | (T4) $=$ (T5) cộng hữu hạn; điểm mở 12 |
| $m^{UC}_{\mathcal H}(\epsilon,\delta)$ | hàm cỡ mẫu hội tụ đều | theo mẫu $m_{\mathcal H}$ của Định nghĩa 01.20 |
| $\rho_m$ | bán kính VC $\sqrt{8\ln(4\Pi_{\mathcal H}(2m)/\delta)/m}$ | khác $r_m$ của Định lý 02.14 (chỉ xuất hiện ở Ví dụ 03.10); điểm mở 2 |
| $S'=(Z'_1,\ldots,Z'_m)$, $X'_i$ | mẫu bóng | chỉ trong chứng minh |
| $\sigma_1,\ldots,\sigma_m$ | dấu ngẫu nhiên | bài không dùng $\sigma^2$ (Bổ đề 02.3 viết $\sigma^2$; ở đây viết $\operatorname{Var}$) |
| $a_i(h)$, $h_S$ | hiệu hàm lỗi trên cặp thứ $i$; giả thuyết lệch được chọn theo $S$ | chỉ ở Phụ lục C |
| $C'$, $Y_1$ | bộ bỏ điểm cuối; các cách gán nhãn mở rộng được hai cách | chỉ ở Bổ đề 03.12 và Phụ lục B |
| $\kappa$, $a_0$ | hằng số trong bất đẳng thức tiếp tuyến | chỉ ở chứng minh Hệ quả 03.16(c) và Phụ lục C.7 |
| $c$, $\epsilon_0$, $\delta_0$ | hằng số phổ quát của cận dưới | chữ thường, khác bộ điểm $C$ |
| $\mathcal G_S$ | lớp hai hàm chọn theo mẫu | Ví dụ 03.8 |
| $\mathcal H_{\mathrm{rec}}$ | lớp hình chữ nhật song song với trục | của Bài tập 02.7, dùng lại ở câu hỏi cuối buổi |
| $t$ | chỉ là ngưỡng của $h_t$ | độ lệch luôn là $\epsilon$ hoặc $\epsilon/2$, không dùng $t$ |

`ky-hieu.md`: điều phối viên thêm $\mathcal H_C$, $\operatorname{VCdim}$, $m^{UC}_{\mathcal H}$, $\rho_m$, $S'$, $\sigma_i$, (M), (T5); dòng $D_\eta$ không đổi (Bài 03 không dùng $D_\eta$).

## 11. Phân bổ thời gian và ngân sách độ dài

### 11.1 Phân bổ thời gian 140 phút (chỉ trong dàn ý)

| Khối blueprint 3.6 | Phút | Mục ghi chú | Nội dung giảng |
|---|---|---|---|
| Động cơ/định nghĩa | 20 | Câu hỏi mở đầu đến §4 mục 5 | câu hỏi mở đầu; ba câu ôn nhanh; Ví dụ 03.1; Định nghĩa 03.1–03.3, Ví dụ 03.2, Nhận xét 03.4 |
| Ví dụ | 35 | §4 mục 6–7, §5 | Mệnh đề 03.5, 03.6 có chứng minh; Định nghĩa 03.7; Bổ đề 03.8 (phát biểu, hình vuông); Mệnh đề 03.9(a) chứng minh; Ví dụ 03.3 trên bảng; Nhận xét 03.10 |
| Hàm tăng trưởng | 15 | §6 mục 1–2 | Định nghĩa 03.11; Ví dụ 03.4 |
| Nghỉ | 10 | — | — |
| Sauer–Shelah | 20 | §6 mục 3–4 | Bổ đề 03.12: quy nạp bằng đẳng thức đếm và công thức Pascal; dạng đóng hai dòng; Ví dụ 03.5 |
| Định lý VC/lộ trình | 30 | §7 | (M) và Nhận xét 03.13 (lướt); Định nghĩa 03.14, Ví dụ 03.6; đoạn vì sao cần mẫu bóng; Định lý 03.15 và lộ trình năm bước; Ví dụ 03.7; Ví dụ 03.8 |
| Ứng dụng/câu hỏi cuối buổi | 20 | §8, §11 | Hệ quả 03.16 (bước tất định); Ví dụ 03.9, 03.10 (đọc bảng, nhận xét trung thực); Định lý 03.17, Hệ quả 03.18, Định lý 03.19 (chỉ phát biểu); câu hỏi cuối buổi |

Nếu 150 phút là thời gian giảng không tính nghỉ: 10 phút dư chữa câu hỏi cuối buổi trọn vẹn hoặc Bài tập 03.2(b). Khối 20 phút cuối dày; khi thiếu giờ, Định lý 03.19 và Ví dụ 03.10 giao đọc.

### 11.2 Ngân sách độ dài

Đếm như Bài 02: `wc -w` trên Markdown, gồm công thức; thân bài từ dòng đầu đến trước `## Phụ lục`. Bài 02 thực tế: thân $11\,999$, phụ lục $622$. Bài 03: **thân ≤ 12 000, phụ lục ≤ 3 000** (QĐ 14).

| Phần | Tiếng | Phần | Tiếng |
|---|---|---|---|
| Tiêu đề, đoạn dẫn | 150 | §5 | 1 550 |
| Câu hỏi mở đầu | 280 | §6 | 1 500 |
| Mục tiêu | 170 | §7 | 2 200 |
| Tiên quyết, ôn nhanh | 450 | §8 | 1 600 |
| §1 | 400 | §9 | 450 |
| §2 | 250 | §10 | 250 |
| §3 | 400 | §11 | 350 |
| §4 | 1 650 | §12 | 300 |

Tổng thân bài khoảng $11\,950$; phụ lục khoảng $2\,850$ (A 550, B 650, C 1 300, D 350). **Thứ tự cắt khi vượt:** (1) Ví dụ 03.5 bỏ cột $m=8$, $10$; (2) Ví dụ 03.9 bỏ Bước 5 (chỉ ước lượng); (3) Định lý 03.19 bỏ câu về điều kiện $d\ge2$; (4) Ví dụ 03.3 rút Bước 4 thành một câu; (5) Nhận xét 03.13 chỉ giữ hàm ngưỡng, phần còn lại trỏ Phụ lục D; (6) Ví dụ 03.4 bỏ giá trị $m=10$; (7) Ví dụ 03.10 bỏ Bước 2. **Không cắt:** chứng minh của 03.5, 03.6, 03.9(a), 03.12(b), 03.16; lộ trình của 03.15 và đoạn vì sao cần mẫu bóng; Ví dụ 03.6 và 03.8 (QĐ 9); Bước 5 của Ví dụ 03.10 (QĐ 8); phần (a) của Định lý 03.17 và Hệ quả 03.18 (QĐ 6).

**Giai đoạn viết** (mỗi giai đoạn khoảng 150 dòng, điều phối viên đọc sau mỗi giai đoạn): (1) tiêu đề đến §3; (2) §4; (3) §5; (4) §6; (5) §7 đến hết Định lý 03.15; (6) phần còn lại của §7 và §8; (7) §9–§12, Phụ lục A–B; (8) Phụ lục C–D.

## 12. Rủi ro, điểm mở và danh sách con số †

**Kiểm tra tham chiếu tới trước (đã chạy trên giấy theo thứ tự mục 3).** Mỗi khối chỉ dùng khối đứng trước, kết quả Bài 01–02 và kiến thức tiên quyết. Chỗ dễ sai đã xử lý: (i) Định nghĩa 03.3 nói "hai mệnh đề dưới đây", không dẫn số; (ii) Nhận xét 03.4 dẫn "§5" cho ba điểm thẳng hàng (dẫn mục, không dẫn khối; người rà mạch có thể đề nghị đổi thành câu không dẫn); (iii) (M) và (T5) nêu ngay trước Định nghĩa 03.14 và Định lý 03.15; (iv) Ví dụ 03.10 nói "định lý dưới đây" cho điều kiện cần; (v) $\mathcal M_{[0,1]}$ chỉ xuất hiện từ Ví dụ 03.6. Dẫn Bài tập 03.3, 03.5 trong thân bài theo cách Bài 02 dẫn Bài tập 02.6.

**Quyết định của điều phối viên được phản ánh:** QĐ 1 (Định lý 03.15, đoạn vì sao cần mẫu bóng, "Quan hệ với UML"); QĐ 2 (Định nghĩa 03.11); QĐ 3 (Định nghĩa 03.14); QĐ 4 (Bổ đề 03.12, phản ví dụ $m=1$, $d=3$); QĐ 5 (Bổ đề 03.8, Mệnh đề 03.9, Phụ lục A); QĐ 6 ((M), Nhận xét 03.13, Định lý 03.17, Hệ quả 03.18, Định lý 03.19); QĐ 7 (Hệ quả 03.16); QĐ 8 (Ví dụ 03.10, với ghép cặp khác, điểm mở 1); QĐ 9 (Ví dụ 03.6, 03.8, Nhận xét 03.4, Ví dụ 03.3 Bước 2, câu về Ví dụ 02.6); QĐ 10 (Nhận xét 03.10, Bài tập 03.5); QĐ 11 (Ví dụ 03.1, 03.2, khối ứng dụng); QĐ 12 (§9, cầu nối); QĐ 13 (mục 4); QĐ 14 (mục 11.2).

**Điểm khác blueprint hoặc QĐ, cần điều phối viên xác nhận:**

1. **Ghép cặp của QĐ 8.** QĐ 8 so $132\,992$ (VC, $d=3$) với $9611$ (một ngưỡng 64 bit). Hai số ứng với hai lớp khác nhau. Dàn ý ghép theo cùng lớp: $54\,330$ với $9611$ ($d=1$, một tham số), $132\,992$ với $27\,355$† ($d=3$, ba tham số), $447\,194$ với $98\,333$ ($d=11$). Thông điệp trung thực không đổi.
2. **Bổ đề 03.8 và Mệnh đề 03.9:** blueprint cho cận trên nửa không gian là [S]; với Radon chứng minh đầy đủ ở Phụ lục A, cận trên của (a) chỉ dài năm dòng nên dàn ý ghi "chứng minh đầy đủ".
3. **Phần (c) mới của Định lý 03.15** ($m^{UC}_{\mathcal H}$ dạng đóng†) và **dạng đóng của $M$ ở Hệ quả 03.16(c)**† (PTN §4 có công thức nhưng QĐ không ghi đã kiểm): cần để đóng QĐ 3 và để viết Định nghĩa 01.25 với một $M$ tường minh. Đã chứng minh trên giấy bằng bất đẳng thức tiếp tuyến và quét số ($d<60$, năm giá trị $\epsilon$, năm giá trị $\delta$: không vi phạm).
4. **Định lý cơ bản** tách (a) điều kiện cần với hằng số $1/8$, $1/7$ (không cần (M)) và (b) sáu khẳng định tương đương; blueprint chỉ nói "statement only". Hệ quả 03.18 là khối riêng để đóng lời hứa của Bài 01.
5. **Bài gốc 1, 3, 6 đổi biến thể** vì ghi chú đã làm bản gốc (Ví dụ 03.4; cận dưới đỉnh đơn hình; Phụ lục A, B); bài gốc 4 thêm ý (d) đo mục tiêu 3.
6. **Câu hỏi cuối buổi** cụ thể hóa bằng lớp hình chữ nhật (trùng trường hợp $p=2$ của UML 6.5).
7. **Hàm tăng trưởng của nửa không gian phẳng** chỉ ghi $m\le4$; công thức $m^2-m+2$ của PTN cần định lý Cover, ngoài UML.
8. **Phân hoạch Radon** dùng $J=\{a_j\le0\}$ để $I\cup J$ là phân hoạch (PTN viết $J=\{a_j<0\}$, bỏ sót các chỉ số có $a_j=0$).

**Điểm mở cho điều phối viên:**

1. Ghép cặp của QĐ 8 (trên).
2. Tên bán kính VC: $\rho_m$ (dàn ý) hay $r^{\mathrm{VC}}_m$?
3. **Tính đo được trong Định nghĩa 03.14.** Định nghĩa đòi (M); $\mathcal M_{[0,1]}$ có lẽ không thỏa (M), nên về hình thức Ví dụ 03.6 nằm ngoài phạm vi định nghĩa. Hai cách: (i) giữ (M) trong định nghĩa và viết ở Ví dụ 03.6 rằng dưới $D$ của Ví dụ 01.8 biến cố là rỗng, nên không hàm $M$ nào thỏa yêu cầu, dù hiểu xác suất theo cách nào; (ii) phát biểu định nghĩa cho lớp bất kì, đòi biến cố "$S$ là $\epsilon$-đại diện" chứa một biến cố đo được có xác suất ít nhất $1-\delta$ (dưới (M), đó chính là biến cố đã cho). Dàn ý đề xuất (i), vì đơn giản cho học viên.
4. $\mathbf e_i$ in đứng hay $e_i$ thường.
5. Tên lớp viết tắt tiếng Việt ($\mathcal H_{\mathrm{ng}}$, $\mathcal H_{\mathrm{kh}}$, $\mathcal H^p_{\mathrm{af}}$, $\mathcal H^p_{\mathrm{tn}}$) trong khi Bài 02 có $\mathcal H_{\mathrm{rec}}$ tiếng Anh.
6. Giữ hay bỏ Bài tập 03.13 (UML 6.8).
7. Câu hỏi cuối buổi trùng một phần Bài tập 03.9.
8. Chốt "tách trọn" và "mẫu bóng" (còn mở ở `thuat-ngu.md` §14).
9. Tên Định lý 03.17: "Định lý cơ bản cho phân lớp nhị phân" hay "Định lý cơ bản của học PAC" (UML §6.4).
10. Độ sâu của Hệ quả 03.18: "chứng minh đầy đủ từ Định lý 03.17(a)" có chấp nhận được không, khi 03.17(a) không chứng minh?
11. Bổ sung `ky-hieu.md` (mục 10).
12. Đặt tên (T5) mới hay viết "(T4) bỏ điều kiện hữu hạn".

**Rủi ro cho bản thảo:**

- **Các vai của $\epsilon$:** độ lệch đều (§7), mức rủi ro vượt mức (Hệ quả 03.16(c), Ví dụ 03.9), mức rủi ro (Định lý 03.19(b)); câu nhắc sau Hệ quả 03.16 là bắt buộc.
- **"Đủ" và "cần":** mọi cỡ mẫu của §7–§8 là cỡ mẫu đủ; chỉ Định lý 03.19 nói về cỡ mẫu cần.
- **Trực tiếp, hằng số $4$, dạng đóng:** ba con số khác nhau cho cùng một câu hỏi ($54\,330$, $103\,939$, $88\,572$ với $d=1$); mỗi con số ghi nguồn công thức.
- **$\inf$ và $\min$:** Hệ quả 03.16 không dùng $h_{\mathcal H}$; người rà toán kiểm Bước 2.
- **$d\le m$ và $d\le2m$:** Định lý 03.15(b) cần $d\le m$; bước Sauer dùng $2m$.
- **Mệnh đề 03.9:** cận trên xét tập $p+2$ điểm phân biệt; chỗ dùng quy ước $\ge0$ phải hiện rõ.
- **Không chép UML:** không dùng $\tau_{\mathcal H}$, $\lceil\sin\rceil$ trong thân bài, hằng số $\frac{4+\sqrt{\cdot}}{\delta\sqrt{2m}}$, $512$, "Fundamental Theorem" dịch từng chữ.
- **Hiển thị 390 px:** bảng Ví dụ 03.5 có chín cột; người viết tách thành hai bảng ($m\le5$; $m=8,10,20$) hoặc chuyển vị. Biến cố trong công thức viết bằng kí hiệu, không có chữ tiếng Việt có dấu trong `\text{}` (bài học Bài 02).
- **Độ dài:** công thức của §7 dày; người viết đếm sau mỗi giai đoạn.

**Danh sách con số † (đã tính lại bằng `lec03_outline_check.py`, `lec03_outline_check2.py` trong scratchpad):**

| Con số | Phép tính rút gọn | Dùng ở |
|---|---|---|
| $16$ | $1+5+10$ | câu ôn nhanh 1 |
| $b=-1$, $w=(2,2)$ | giá trị $-1,1,1$ tại ba điểm | câu ôn nhanh 2 |
| $11$, $56$; $1024$ | $m+1$, $\binom{11}2+1$, $2^{10}$ tại $m=10$ | Ví dụ 03.4, 03.5 |
| $21$, $211$, $176$, $1351$, $1\,048\,576$ | $m+1$, $\binom{21}2+1$, $\sum_{j\le3}\binom{10}j$, $\sum_{j\le3}\binom{20}j$, $2^{20}$ | Ví dụ 03.5 |
| $743{,}91$; $5951{,}27$ | $(10e/3)^3$; $(20e/3)^3$ | Ví dụ 03.5 |
| $3{,}33$ | $\sqrt{16\ln2}=3{,}3302$ (bán kính khi $\Pi(2m)=2^{2m}$) | sau Định lý 03.15 |
| $2{,}7$–$2{,}9$ | $0{,}4638/0{,}1644=2{,}82$; $0{,}1644/0{,}0571=2{,}88$; $0{,}7622/0{,}2799=2{,}72$; $0{,}2799/0{,}0993=2{,}82$ | Ví dụ 03.7 |
| $m^{UC}$ dạng đóng | $(16/\epsilon^2)(d\ln(32/\epsilon^2)+\ln(4/\delta))$: tại $\epsilon=0{,}1$, $\delta=0{,}05$: $19\,925$, $45\,752$, $149\,060$ ($d=1,3,11$); thỏa điều kiện ẩn tại $M,2M,10M,10^3M$; quét không vi phạm | Định lý 03.15(c) |
| $88\,572$; $209\,624$; $693\,832$ | $(64/\epsilon^2)(d\ln(128/\epsilon^2)+\ln80)$ tại $\epsilon=0{,}1$: $88\,571{,}1$; $209\,623{,}2$; $693\,831{,}9$ (trùng PTN; đánh dấu vì QĐ chưa kiểm) | Hệ quả 03.16(c), Ví dụ 03.9, Bài tập 03.4 |
| $1{,}55$–$1{,}63$ | $88\,572/54\,330=1{,}630$; $209\,624/132\,992=1{,}576$; $693\,832/447\,194=1{,}552$ | sau chứng minh Hệ quả 03.16 |
| $0{,}0099999$; $0{,}0100001$ | $32(\ln(2em)+\ln80)/m$ tại $m=54\,330$, $54\,329$ ($d=1$) | Ví dụ 03.9 Bước 3 |
| $12\,401$ | cỡ mẫu nhỏ nhất với $8(\ln(2em)+\ln80)/m\le0{,}01$ ($d=1$) | Ví dụ 03.9 Bước 5 |
| $27\,355$ | $2(193\ln2+\ln20)/0{,}01=27\,354{,}6$ | Ví dụ 03.10 |
| $4{,}5$–$5{,}7$; $4{,}25$ | $54\,330/9611=5{,}65$; $132\,992/27\,355=4{,}86$; $447\,194/98\,333=4{,}55$; $0{,}2222/0{,}0523=4{,}25$ | Ví dụ 03.10, §9 |
| $2m$ | hàm ngưỡng hai phía trên $m$ điểm phân biệt: $(m+1)+(m+1)-2$; liệt kê với $m\le7$ | Bài tập 03.1(c) |
| $d=4$ | hợp hai khoảng: duyệt mọi cách gán nhãn của $4$ và $5$ điểm | Bài tập 03.2(b) |
| $b=-1$, $w=(2,0,2)$ | $b=2y_0-1$, $w_i=2y_i-1-b$ với $y=(0,1,0,1)$ | Bài tập 03.3(b) |
| $3{,}31$ | $693\,832/209\,624$ | Bài tập 03.4(a) |
| $21{,}5$ | $(5e/10)^{10}=21{,}51<32$ | Bài tập 03.6(b) |
| cách dựng $\sin$ | kiểm bằng số hữu tỉ chính xác cho mọi cách gán nhãn, $k\le8$ (PTN kiểm $k\le10$) | Bài tập 03.5(a) |

Các con số còn lại (bảng bán kính $d=1,3,11$; $54\,330$, $132\,992$, $447\,194$; $103\,939$, $261\,198$, $889\,572$; $29\,646$, $98\,484$; $589\,118$, $1\,999\,657$; $9611$, $98\,333$; $0{,}2222$, $0{,}0523$; $0{,}322$; $0{,}744$; $8\ln4\approx11{,}09$; bảng tăng trưởng đến $m=8$; tỉ số $3{,}36$, $3{,}41$) lấy từ PTN và đã được tính lại trong phiên này: khớp.
