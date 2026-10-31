# Ghi chú của người soạn bài tập — Bài 06

Tệp nội bộ, không liên kết từ trang chỉ mục. Người soạn: sub-agent "soạn bài tập" (2026-10-31), ghi `2627-1/materials/lec-06/exercises.md`. Không commit.

Sản phẩm: 11 bài (06.1–06.6 gốc theo blueprint 6.5; 06.7–06.11 chọn từ UML), 44 khối (11 `exercise`, 22 `hint`, 11 `solution`), 1096 dòng, 9972 tiếng (`wc -w`, trần 10 000). Script tính số: scratchpad `ex06/nums.py`, `ex06/two_d.py` (ngoài repo); kiểm trình xem: `ex06/probe.py`.

## 1. Số bài UML đã kiểm trên PDF

Đọc bằng pymupdf, trang PDF trùng số trang in (đầu trang ghi "13.7 Exercises 181").

| Bài tập học phần | Bài UML | Trang PDF | Ghi chú |
|---|---|---|---|
| 06.7 | 13.1 "From Bounded Expected Risk to Agnostic PAC Learning" | 181 | phát biểu đã chỉnh hằng số |
| 06.8 | 13.2 "Learnability without Uniform Convergence" | 181–182 | $d\to p$ |
| 06.9 | 13.3 "Stability and Asymptotic ERM Are Sufficient for Learnability" | 182 | $\min\to\inf$ |
| 06.10 | 14.1 (chứng minh Claim 14.10) | 201 | §14.8 bài 1 |
| 06.11 | 13.4 "Strong Convexity with Respect to General Norms", ý 1–3 | 183 | tùy chọn; bỏ ý 4 |

§13.7 có đúng 4 bài; §14.8 có 4 bài (14.3, 14.4 đã dùng ở Bài 05; 14.2 bỏ theo QĐ 9).

## 2. Tự giải trước, đối chiếu sau

Lời giải của cả năm bài UML (lập luận, hằng số và mọi con số; `nums.py`) được lập xong trước khi mở `sources/uml/MLbookSol.pdf`. Bản lời giải (tr. 34–38) được mở một lần lúc **2026-10-31 17:29** (giờ ghi bằng `date` ngay trước lệnh đọc); văn bản `exercises.md` viết sau đó, không mở lại bản lời giải.

| Bài | Chỗ bản lời giải sai hoặc thiếu | Cách viết của học phần khác ở đâu |
|---|---|---|
| 13.1 | Bản lời giải tự sửa hai lỗi của đề ($k=\lceil\log_2(2/\delta)\rceil$, khối $m_{\mathcal H}(\epsilon/4)$) và dùng mẫu xác thực $8\ln(4k/\delta)/\epsilon^2$, khớp hằng số đã chỉnh. Thiếu: không nói giả thiết hàm lỗi trong $[0,1]$ ở bước xác thực; Markov viết với ngưỡng $\mathbb E\theta/\delta$, không xác định khi $\mathbb E\theta=0$; dùng "$>$" ở khối nhưng "$\le$" ở kết luận mà không nói. | Markov dùng ngưỡng $\epsilon$ trực tiếp; bước xác thực dẫn Hệ quả 04.17(a) và (T3), (T7); thêm (c) bằng số (hồi quy ridge chia 4, $G=1$) và (d) chỉ ra hằng số gốc của UML chỉ cho $(1+\sqrt2)\epsilon$ với xác suất thất bại $3\delta/2$. |
| 13.2 | Dùng tính trơn (cần kết quả §13.3.2) thay cho Lipschitz; bất đẳng thức $(1-2^{-m})^d\ge\exp(-2^{1-m}d)$ ngược chiều với điều cần chứng minh (cần cận trên của xác suất "không có $j$"); không cho cận dưới tường minh cho cỡ mẫu hội tụ đều; chú thích nói gợi ý "$\alpha_j=1$" của đề là sai, nhưng gợi ý đó cũng dùng được ($L_S(\mathbf e_j)=1$, $L_D(\mathbf e_j)=\tfrac12$). | Dùng (L) với $G=4$ và Hệ quả 06.13(c) ($8/\sqrt m$); dùng $(1-2^{-m})^p\le e^{-p2^{-m}}$; cận dưới tường minh $m\ge\log_2\big(p/\ln(1/(1-\delta))\big)$, bằng số $17{,}57$ với $p=10^4$, $\delta=0{,}05$; so với Định lý 03.17 (phân lớp nhị phân) thay cho "định lý cơ bản". |
| 13.3 | Giả sử có $h^\star$ đạt $\min L_D$; dùng đẳng thức "ổn định thay một theo trung bình = khoảng cách tổng quát hóa kì vọng" mà không nêu điều kiện khả tích. | Dùng $\inf$ và lấy cận dưới đúng theo $h$ (như Bước 3 của Mệnh đề 06.5); kiểm $\mathbb EL_S(A(S))<\infty$ từ giả thiết gần đúng ERM; nêu chỗ dùng dạng đầy đủ và dạng yếu của (T1); thêm (b): áp dụng cho ERM có chính quy hóa với $\mathcal H=W_B$ để suy lại Hệ quả 06.13(c) (thuật toán học ngoài lớp vẫn được). |
| 14.1 | Dòng cuối viết giới hạn của vế phải là $f(w)-f(u)-\tfrac\lambda2\lVert w-u\rVert^2$ (đổi chỗ $f(w)$, $f(u)$; đúng là $f(u)-f(w)-\ldots$). | Viết đủ bốn bước (chặn trên, chặn dưới, chia, giới hạn) theo cấu trúc Bổ đề 06.7; thêm hệ quả tăng trưởng bậc hai và tính đơn điệu mạnh; kiểm bằng số cả trường hợp không khả vi ($\lvert w\rvert+w^2$). |
| 13.4 | Ý 1 và ý 3 chỉ nói "giống trường hợp $\ell_2$", không viết chứng minh; ý 2 dùng $\tfrac12\lVert w\rVert_1^2$ với $\mathbf e_1$, $\mathbf e_2$. | Viết đủ ý 1 (hai khẳng định) và ý 3 (bốn bước, so hằng số với UML: đối xứng cho $G^2/(\lambda_{\mathrm{UML}}m)$, một phía cho đúng $2\rho^2/(\lambda_{\mathrm{UML}}m)$); ý 2 dùng ví dụ riêng với chuẩn $\ell_\infty$ trên $\mathbb R^2$, đoạn nối $(1,1)$ và $(1,-1)$, chỉ nhắc $\ell_1$ một câu. Chỉ ra bước của §6 cần chuẩn Euclid (đẳng thức ở Kiến thức tiên quyết). |

Không câu nào của `exercises.md` dịch đề hay lời giải UML; đề viết bằng kí hiệu học phần ($p$, $G$, $\tfrac\lambda2\lVert w\rVert^2$, $\inf$).

## 3. Sai khác so với `outline.md` §4 và lý do

1. **06.1(c):** độ chệch $\mp\tfrac23$ kiểm bằng liệt kê chính xác 72 trường hợp thay cho mô phỏng; thêm $\mathbb E[g_2\mid S,i_1]=L_S'(w_2)$ để đặt cạnh $\mathbb E[g_2\mid w_2]$.
2. **06.2(b):** thêm ý (b2) chứng minh hệ số ổn định đều nhỏ nhất của thuật toán trung bình là $2/m-1/m^2$ (giá trị $0{,}75$ của dàn ý là trường hợp $m=2$). **06.2(c):** thêm khẳng định với $m\ge4$ bản sao, khoảng cách tổng quát hóa kì vọng $0{,}5$ vượt $\epsilon_{\mathrm{stab}}(m)=2/m-1/m^2$ (ví dụ $0{,}4375$ khi $m=4$): bỏ dạng đầy đủ của (T1) thì kết luận của Định lý 06.10 sai, không chỉ đẳng thức của chứng minh. Số $0{,}5$ và $0{,}125$ của dàn ý đã tính lại (khớp; điểm mở 10). **06.2(d):** thêm $\mathbb E\lvert L_D-L_S\rvert=0{,}25$ cho thuật toán ở (b1).
3. **06.3(d):** thêm chuỗi của lập luận một phía ($0{,}0726\le0{,}1905\le0{,}7619$) cạnh chuỗi đối xứng của dàn ý.
4. **06.4(c):** dàn ý cho $G=4$, $m=1600$ trừu tượng; đề đặt vào hồi quy logistic với $\lVert x\rVert\le4$, $W=\mathbb R^p$ để có $G=4$ và cho phép điểm so sánh chuẩn $2$. **06.4(d):** thay "giải thích" bằng chứng minh $L_S(\hat w_{S,\lambda})$ không giảm và $\lVert\hat w_{S,\lambda}\rVert$ không tăng theo $\lambda$; mẫu xác thực chỉ nêu dạng cận của Hệ quả 04.17(a) và điều kiện (T3).
5. **06.5(d):** thêm giá trị $19{,}2$ với $\lambda=0{,}01$ để so cả ba $\lambda$.
6. **06.6:** thêm một mẫu hai chiều cụ thể cho ý đường mức (ý (c)), kèm trị riêng và nghiệm đã tính, để kết quả kiểm được; giao thức (b) so độ nhạy với $2G_\lambda/(\lambda m)$ của Bài tập 06.5(b) (vì $W=\mathbb R^p$), không với $2G/(\lambda m)$.
7. **06.7:** thêm (c) bằng số và (d) hằng số gốc của UML (nêu ở dàn ý như ghi chú, nay thành một ý của bài).
8. **06.8:** điều kiện "cỡ mẫu hội tụ đều tăng theo $\log p$" được làm tường minh ở (c). Ý xác suất cao qua Bài tập 06.7(a) đã viết rồi bỏ khi cắt chữ cho trần 10 000.
9. **06.9:** thêm ý (b) suy lại Hệ quả 06.13(c).
10. **06.10:** thêm tính đơn điệu mạnh ở (b) và một kiểm tra không khả vi ở (c).
11. **06.11 ý 2:** dàn ý ghi "$1\le1-\lambda$" cho $\lVert w\rVert_1^2$ với $\mathbf e_1$, $\mathbf e_2$, $\alpha=\tfrac12$; theo Định nghĩa 05.6, vế phải là $1-\tfrac\lambda2$ (sai số nhỏ của dàn ý, không ảnh hưởng kết luận). Bài viết dùng $\tfrac12\lVert w\rVert_\infty^2$ và cho $\tfrac12\le\tfrac12-\tfrac\mu2$.

## 4. Đề xuất cho `thuat-ngu.md` và `ky-hieu.md` (không sửa)

- **Thuật ngữ mới trong bài tập:** "đường mức" (level curve), Bài tập 06.6; "ma trận đạo hàm bậc hai" cho Hessian (tránh tên riêng), Bài tập 06.6; "tính đơn điệu mạnh" không dùng tên, chỉ viết bất đẳng thức (06.10).
- **Kí hiệu cục bộ:** $H_\lambda$ (06.6); $P(s,z')$, $\tau_i$, $a$, $b$ (06.2); $Q(\lambda)$, $B_0$, $\lambda_0$, $\hat w_1$, $\hat w_2$ (06.4); $K=\{w:\lVert w\rVert\le r_\lambda\}$ (06.5); $\Gamma_S$, $E_1$, $E_2$, $m_{\mathcal H}(\epsilon)$ một đối số (cỡ mẫu cho mức kì vọng, khác $m_{\mathcal H}(\epsilon,\delta)$ của bảng chung) (06.7); $h'$, $\epsilon_1(m)$, $\epsilon_2(m)$ (06.9); $w_\alpha$, $w^*$ (06.10, $w^*$ đúng nghĩa trong bảng chung); $\lVert\cdot\rVert_\infty$, $\lambda_{\mathrm{UML}}$, $R$ là hàm chính quy hóa (06.11; $R$ trùng chữ với cận khoảng cách khởi tạo của Bài 05, nhưng đó là kí hiệu của UML trong đề gốc và chỉ dùng trong bài tùy chọn — điều phối viên có thể đổi thành $\Omega$).
- $K$ ở 06.5 trùng chữ với số ứng viên $K$ của Hệ quả 04.17 (dùng ở 06.4(d), 06.7); hai bài khác nhau, nhưng điều phối viên có thể đổi thành một chữ khác.

## 5. Bảng con số và script

| Bài | Con số | Nguồn |
|---|---|---|
| 06.1(c) | độ chệch $-2y/m$; $m=3$: $\mp0{,}667$ (liệt kê đúng, cả $m=2,4,10$) | `nums.py` |
| 06.2(b) | $\mathbb EL_D=0{,}375$, $\mathbb EL_S=0{,}125$, khoảng cách $0{,}25$, trung bình thay một $0{,}25$; $\epsilon_{\mathrm{stab}}(m)=3/4,5/9,7/16,9/25$ ($m=2..5$) | `nums.py` (phân số đúng) |
| 06.2(c) | khoảng cách $0{,}5$, trung bình thay một $0{,}125$ | `nums.py` |
| 06.3(d) | $0{,}1451$; $0{,}3810$; $0{,}7619$; $0{,}0726$; $0{,}1905$; cận $2$, $4$ | `nums.py` |
| 06.4 | thừa số $1{,}25$; $5{,}05$; $Q(\lambda_0)=0{,}5$, $Q(\lambda^*)=0{,}4$ | `nums.py` |
| 06.5 | $99/249\approx0{,}3976$; $0{,}2518$; $r_\lambda$, $G_\lambda$; hệ số $0{,}0466$; $2{,}3955$; $183{,}43$; $192/(\lambda m)$: $0{,}192$; $1{,}92$; $19{,}2$ | `nums.py` |
| 06.6(a) | $10/29\approx0{,}3448$; $2/29\approx0{,}0690$; $8/29\approx0{,}2759$; $L_S=0{,}4156$ | `nums.py` |
| 06.6(c) | trị riêng $0{,}0375$, $1{,}9725$ ($\lambda=0{,}01$), $1{,}0275$, $2{,}9625$ ($\lambda=1$); tỉ số trục $7{,}3$; $1{,}7$; nghiệm $(1{,}9012;-1{,}4276)$, $(3{,}7145;-3{,}6198)$, khoảng cách $2{,}8449$; $(0{,}1763;0{,}0629)$, $(0{,}2528;-0{,}0228)$, khoảng cách $0{,}1149$; cận $2{,}41$, $1514$ | `two_d.py` |
| 06.7 | $k=6$; $800\ln480\approx4939{,}03\to4940$; $160\,000$ so với $43\,340$; $\delta=0{,}001$: $k=11$, $8553{,}56\to8554$, $4\cdot10^8$ so với $78\,954$; $1+\sqrt2\approx2{,}414$ | `nums.py` |
| 06.8 | $0{,}6236$ (cận dưới $0{,}6234$), $0{,}99994$; $\ln(1/0{,}95)\approx0{,}05129$, $\log_2194\,957\approx17{,}57$; $m=17$: $0{,}927$ | `nums.py`, `two_d.py` |
| 06.10 | $2\ge2$; $-\tfrac12\ge-1$ | tính tay |

Mọi số dẫn lại từ ghi chú (Ví dụ 06.3, 06.4, 06.5, 06.6, 06.9) khớp ghi chú.

## 6. Kiểm tra đã chạy (từ gốc repo, 2026-10-31)

- `sync-local-materials.py` và `--check`: OK; `git diff --check`: sạch.
- Khối `:::` cân bằng, không lồng: 11 `exercise`, 22 `hint`, 11 `solution`; không "hãy", "Đáp án", "rõ ràng", "dễ thấy"; không `\text{}` nào.
- Trình xem qua HTTP (cổng 8783, `reloadserver`), mọi `details` mở, 1600×900 và 390×844: 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức hay bảng tràn (độ rộng tài liệu 375 px ở 390); 33 khối thu gọn. Console chỉ có cảnh báo CSP của script nội tuyến do `reloadserver` chèn (như ở ghi chú). Lần kiểm đầu có 23 công thức tràn ở 390 px; đã tách dòng `aligned`. Ảnh chụp ở scratchpad `ex06/`.
- Chưa kiểm `file://` và bản in (ngoài phạm vi được giao).

## 7. Ghi chú số dòng

Các mục 1–6 mô tả bản đóng băng `lec06-ex-frozen.md` (1096 dòng, 9972 tiếng). Bản sau sửa: 1119 dòng, 9938 tiếng.

## 8. Sửa sau rà soát (theo `reviews/11-quyet-dinh-bai-tap.md`, 2026-10-31)

Áp dụng đủ 8 mục:

1. 06.5(c), (d): cận trên làm tròn lên, $0{,}0467$ và $2{,}3956$ (viết "$\le$" ở (c)).
2. 06.2(c): đề viết $\mathbb E[L_D(A(S))-L_S(A(S))]$ thay cho tên "khoảng cách tổng quát hóa kì vọng" (mẫu bản sao không có phân bố $D^m$). Lời giải Bước 1, 4 giữ tên như người rà đề xuất.
3. 06.3: bỏ ý (a) (chép chứng minh Bổ đề 06.7). (b)–(d) thành (a)–(c), lời giải dẫn "Bổ đề 06.7" và "Bước 1 của chứng minh Bổ đề 06.7". Bước 3 của (c) cũ tách thành Bước 3 (hai hiệu mục tiêu) và Bước 4 (chuỗi). 06.11 bỏ "(hay (a) của Bài tập 06.3)" và đổi "06.3(c)" thành "06.3(b)".
4. Gợi ý 1 của 06.4, 06.5, 06.7, 06.8, 06.9 viết lại thành hướng tiếp cận; bước then chốt ($F_{s,\lambda}(0)$ và $\ell\ge0$; Bổ đề 02.2; $\mathbf e_j$; hai bất đẳng thức tối ưu; phép tách ba số hạng) chuyển sang Gợi ý 2. 06.3 cũng tách theo cách này.
5. 06.7: $m_{\mathcal H}(\epsilon)$ thành $\bar m(\epsilon)$, thêm "(cỡ mẫu cho mức kì vọng, khác độ phức tạp mẫu $m_{\mathcal H}(\epsilon,\delta)$)".
6. 06.5: quả cầu viết $W_{r_\lambda}$; Gợi ý 2 nói "một tập con" thay cho $K$.
7. 06.11: $R$ thành $\Omega$ trong đề, gợi ý và lời giải.
8. 06.4(c): thêm yêu cầu tính hệ số ổn định và Bước 5 của lời giải: $\epsilon_{\mathrm{stab}}=2\cdot16/(0{,}2\cdot1600)=0{,}1$ tại $\lambda_0=0{,}2$ và $0{,}2$ tại $\lambda^*=0{,}1$ (tính bằng Python, khớp đề xuất $0{,}1$ của người rà); dòng Mục tiêu của 06.4 thêm mục tiêu 4.

Điểm nhẹ đã áp dụng: $10\,000$; "elip"; "(Hessian matrix)"; bỏ "hiển nhiên"; lưới $\Lambda$ ở 06.4(d); câu "Lệch $\lambda^*$ một thừa số …" ở 06.4(b); 06.2(b1) Bước 3 thành `aligned` có bước phương sai; tách 06.4(c) Bước 3–4 và 06.7(c) Bước 4 (`aligned` ba dòng, kết luận đoạn riêng); bỏ câu "liệt kê bằng máy" ở 06.2; câu đề 06.2(d); lượng từ ở 06.5(a); "(random seed)" và nhãn "Kết quả mong đợi và phạm vi." ở 06.6(b); câu kí hiệu ở đoạn mở; bỏ "bổ đề đóng băng" ở 06.1, chỉ giữ "như Bổ đề 05.12(b)"; $h'$ thành $h_0$ ở 06.9.

Không áp dụng: không có mục nào bị bỏ. Ghi chú riêng: $h_0$ ở 06.9 trùng chữ với hàm phân lớp hằng $h_0$ của Ví dụ 06.5. Cả hai đều là một giả thuyết cố định và nằm ở hai tệp khác nhau, nên đề xuất của người rà vẫn được giữ.

Cắt để bù chữ: câu UML về không gian vô hạn chiều ở 06.8(c) Bước 4; câu về $W$ lồi bất kì ở 06.10(b) Bước 1; câu về $\delta$ sau tổng cỡ mẫu ở 06.7(b); 06.5(d) Bước 3, 06.9 Bước 5, 06.11 Bước 4 rút gọn.

Bảng số bổ sung (mục 5): 06.4(c) $\epsilon_{\mathrm{stab}}=0{,}1$ ($\lambda_0=0{,}2$) và $0{,}2$ ($\lambda^*=0{,}1$), số hạng khớp $0{,}4$ và $0{,}2$; 06.5 $0{,}046627\to0{,}0467$, $2{,}395542\to2{,}3956$.

Kiểm tra sau sửa (từ gốc repo): sync và `--check` OK; `git diff --check` sạch; khối `:::` gồm 11/22/11, cân bằng, không lồng; 9938 tiếng; trình xem qua HTTP (cổng 8784, đã tắt) ở 390×844 và 1600×900 với mọi `details` mở: 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 công thức tràn (một công thức tràn ở 06.7(c) Bước 4 đã tách dòng).

### 8.1 Sửa lần cuối (theo `reviews/12-ra-lai-bai-tap-toan.md`, `reviews/13-ra-lai-bai-tap-su-pham.md`, 2026-10-31)

1. 06.4(c) Bước 5: câu sau công thức viết lại thành "Tại $\lambda_0=2\lambda^*$, hệ số ổn định giảm một nửa, từ $0{,}2$ xuống $0{,}1$, còn số hạng khớp … tăng từ $0{,}2$ lên $0{,}4$; hai tổng là $0{,}4$ và $0{,}5$, như Bước 4". Câu này không còn dùng "hệ số" cho cả $\lambda$ lẫn hệ số ổn định.
2. 06.9 Bước 5: nhãn đổi thành "hai giả thiết không cần".
3. 06.3(c) Bước 3: thêm bước $F_{s,\lambda}(w)-F_{s,\lambda}(\hat w)=1{,}3125(w-\hat w)^2$ và $(\hat w'-\hat w)^2=\tfrac{64}{441}$. Python kiểm: hai vế cùng bằng $0{,}190476$; đỉnh của parabol $1{,}25/2{,}625=10/21=\hat w$.
4. 06.8(c) Bước 4: thêm câu giải thích tên bài. Bù chữ: bỏ ý (d) trong Gợi ý 2 của 06.7 (câu đó lộ đáp số) và câu "Tổng cỡ mẫu là …" ở 06.7(b).
5. Ngoại lệ phạm vi do điều phối viên giao: `lecture-note.md` dòng 1082 (§11, Bài tập 06.4) đổi "mục tiêu 5" thành "mục tiêu 4, 5". Không sửa gì khác trong ghi chú; `git diff --stat` cho đúng 1 dòng.
6. Đề xuất thêm "hệ số ổn định của hồi quy logistic" vào dòng Mục tiêu của 06.4: không áp dụng. Dòng này đã ghi mục tiêu 4, và giữ số tiếng dưới trần.

Kiểm tra: sync và `--check` OK; `git diff --check` sạch; khối 11/22/11; 9969 tiếng, 1119 dòng; `forward_refs.py` cho ghi chú: 0. Trình xem qua HTTP (cổng 8785, đã tắt) ở 390×844 và 1600×900: 0 `.katex-error`, 0 lỗi trang, 0 công thức tràn.
