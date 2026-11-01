# Kế hoạch sửa ghi chú Bài 02 theo văn phong tác giả

Đã đọc: `van-phong-tac-gia.md` (đầy đủ), `lecture-note.md` Bài 02 (đầy đủ, 1151 dòng), `lecture-note.md` Bài 01 (mẫu, dòng 1–400), `thuat-ngu.md` (dòng 1–400), `exercises.md` Bài 02 (dòng 1–400 + truy vấn nhãn). Chưa đọc `ky-hieu.md` (không cần cho kế hoạch này). Không commit, không viết lại văn bản — chỉ lập kế hoạch.

---

### mo-dau (Câu hỏi mở đầu đến hết §3)

1. **Dòng 5** — "trong trường hợp bất khả tri (agnostic) và trường hợp khả thực (realizable)" → đổi thành "bất khả diễn (agnostic)" và "khả diễn (realizable)". *Quy tắc: §5 thuật ngữ đổi.*
2. **Dòng 13** — "Có dùng được cùng một câu trả lời cho hàm được chọn như cho một hàm cố định trước khi xem mẫu không? Không: …" + "Câu trả lời bằng số cho một hàm cố định nằm ở §5, cho một hàm chọn trong 1000 ứng viên nằm ở §6." → cắt cả đoạn. *Quy tắc: §2.7 đoạn tự hỏi tự đáp; §2.2 chỉ dẫn điều hướng "nằm ở §5/§6".*
3. **Dòng 22, 23** — "trong trường hợp bất khả tri" (2 chỗ) → "bất khả diễn"; "trường hợp khả thực" → "trường hợp khả diễn". *§5.*
4. **Dòng 31** — "Tính khả thực, hai định nghĩa học PAC…" → "Tính khả diễn". *§5.*
5. **Dòng 35** — "khai triển Taylor với phần dư Lagrange (Taylor expansion with Lagrange remainder, **chỉ dùng ở Phụ lục A**)" → bỏ cụm "chỉ dùng ở Phụ lục A". *§2.5 chú thích phạm vi dùng của tiên quyết.*
6. **Dòng 54** — "**Mẫu.** $S=(Z_1,\ldots,Z_m)\sim D^m$…" → đổi nhãn thành "**Tập huấn luyện.**" (khớp Bài 01 §1 mục 3). *§5: "mẫu huấn luyện, mẫu" → "tập huấn luyện" khi chỉ dữ liệu huấn luyện.*
7. **Dòng 58** — "rủi ro $L_D(\hat h)$ khi lớp khả thực" → "khi lớp khả diễn". *§5.*
8. **Dòng 59** — nhãn "**Đối tượng so sánh.**" → **báo tác giả**, không tự đổi: §5 ghi nhãn này đã bỏ ở Bài 01 §1 mục 7 nhưng khái niệm vẫn dùng ở §7 (Hệ quả 02.16). Đề xuất đổi nhãn theo mẫu Bài 01 hoặc giữ nguyên; chờ quyết định.
9. **Dòng 86** — "Hai giả thiết mới được nêu ở chỗ dùng lần đầu: (T3) hàm lỗi bị chặn **ở §5** và (T4) lớp hữu hạn chọn trước mẫu **ở §6**. Giả thiết tối ưu (O1)… **được dùng từ §6**; (O2) **chỉ dùng ở §7**. Giả thiết khả thực **chỉ dùng ở §8**." → bỏ các cụm "ở §5/§6/§7/§8" (chỉ dẫn điều hướng), giữ nội dung rằng (T3), (T4), (O1), (O2) được nêu ở chỗ dùng lần đầu; đổi "khả thực" → "khả diễn". *§2.2, §2.5, §5.*
10. **Dòng 90, 95** — "nhắc lại **bản có nhiễu**", "**Bản có nhiễu $D_\eta$.**" → "dữ liệu có nhiễu". *§5.*
11. **Dòng 115** — "…nên phép chọn là ERM trên lớp này; **lập luận chi tiết ở §6.**" → bỏ cụm "lập luận chi tiết ở §6". *§2.2 chỉ dẫn điều hướng.*

---

### s4 (§4 Xác suất đuôi, Markov, Chebyshev)

1. **Dòng 136** — "Mọi biến cố đuôi trong bài dùng dấu '$\ge$'. Đoạn cầu nối cuối Bài 01 viết biến cố lệch với dấu '$>$'; biến cố đó nằm trong biến cố '$\ge$', nên mọi cận dưới đây cũng chặn nó." → **ứng viên cắt** (bình luận kĩ thuật về quy ước dấu). Nếu giữ, rút gọn còn một câu nêu quy ước "$\ge$". *§2.3 bình luận kĩ thuật.*
2. **Dòng 138** — "Xác suất $\Pr(V\ge\mathbb EV)$ **không phải một xác suất đuôi**, vì nó không có độ lệch $\epsilon>0$." → diễn đạt tích cực: "Xác suất $\Pr(V\ge\mathbb EV)$ không có độ lệch $\epsilon>0$, nên không thuộc ba dạng ở Định nghĩa 02.1." Giữ nguyên con số $0{,}539$. *§6a ý nghĩa tích cực thay cho "không phải".*
3. **Dòng 175** — "**Kết luận.** Ta tính được các xác suất này vì đã biết $D_\eta$. Khi $D$ chưa biết, chúng ta cần một cận đuôi không dùng $D$." → gộp nhãn "Kết luận" vào mạch văn (bước chuyển, không phải phép tính độc lập). *§1 nhãn bước thừa.*
4. **Dòng 178** — "Trong bổ đề dưới, $\alpha$ là một ngưỡng cho chính $V$, **không phải độ lệch khỏi kì vọng**." → diễn đạt tích cực: "…$\alpha$ là một ngưỡng cho chính $V$, tức một mức mà $V$ được so với nó." *§6a.*
5. **Dòng 181** — "**Không cần tính độc lập hay tính bị chặn.**" → **ứng viên cắt** (liệt kê phủ định). Nếu giữ, đổi thành câu khẳng định: "Bổ đề chỉ dùng kì vọng, không dùng tính độc lập hay tính bị chặn." *no-ai-slop: negative listing.*
6. **Dòng 187** — "Đây là một cận trên của $\Pr(V\ge\alpha)$ chỉ dùng kì vọng, đúng cho mọi biến ngẫu nhiên không âm khả tích." → cắt (nhắc lại kết quả vừa chứng minh). *§2.6 câu nhắc lại kết quả.*
7. **Dòng 227** — "Tính độc lập chỉ được dùng ở đẳng thức đầu; **Bài tập 02.1 cho thấy** chỉ cần các $V_i$ không tương quan từng đôi (pairwise uncorrelated)." → bỏ cụm "Bài tập 02.1 cho thấy" (chỉ dẫn điều hướng), giữ thuật ngữ "không tương quan từng đôi (pairwise uncorrelated)". *§2.2.*
8. **Dòng 267** — "**Kết luận.** Cận Chebyshev đúng mà không cần biết $D$, nhưng nó chỉ giảm như $1/m$, và cỡ mẫu cần tăng như $1/\delta$." → gộp nhãn "Kết luận" vào mạch văn. *§1.*

---

### s5 (§5 Phương pháp Chernoff và Hoeffding)

1. **Dòng 306** — "$\square$ **Phương pháp Chernoff có ba bước: bất đẳng thức Markov cho hàm mũ, tách theo tính độc lập, chọn $\tau$ tốt nhất.** Để áp dụng nó cho rủi ro thực nghiệm, chúng ta còn cần chặn $\mathbb Ee^{\tau V_i}$ cho một biến bị chặn." → cắt câu tóm tắt ba bước (recap), giữ câu chuyển tiếp về việc cần chặn $\mathbb Ee^{\tau V_i}$. *no-ai-slop: summary-recap ending.*
2. **Dòng 348** — "$\square$ Sau khi trừ kì vọng, hàm sinh mô-men của một biến bị chặn không vượt quá $e^{\tau^2(b-a)^2/8}$, bất kể phân bố của biến đó." → cắt (nhắc lại Bổ đề 02.6 vừa chứng minh). *§2.6.*

---

### s6 (§6 Bất đẳng thức hợp và hội tụ đều)

1. **Dòng 408** — "Khi mọi $b_i-a_i$ bằng $b-a$, cận trở về Định lý 02.7(a) **(Bài tập 02.2)**." → bỏ "(Bài tập 02.2)". Giữ nguyên khối Nhận xét 02.8 (bài tập 02.2(a) trích dẫn nó). *§2.2; ràng buộc giữ khối bài tập trích dẫn.*
2. **Dòng 415** — "…các cỡ mẫu dựng từ Định lý 02.7 **ở §5–§7** nhân thêm $(b-a)^2$, bằng $16$ với $\ell_c$, và các bán kính nhân thêm $b-a$ **(Bài tập 02.11)**. **§8 chỉ xét hàm lỗi 0–1.**" → bỏ các cụm "ở §5–§7", "(Bài tập 02.11)", "§8 chỉ xét hàm lỗi 0–1". Giữ nội dung về $(b-a)^2$ và ví dụ $\ell_c$. *§2.2.*
3. **Dòng 440** — "Xác suất $1-\delta$ lấy theo các lần lấy mẫu lặp lại, **không phải xác suất hậu nghiệm** (posterior probability; Nhận xét 01.19)." → diễn đạt tích cực theo §6a: "Xác suất $1-\delta$ lấy theo các lần lấy mẫu lặp lại (Nhận xét 01.19)." *§6a.*
4. **Dòng 509** — "**Kết luận.** Cỡ mẫu đủ theo Hoeffding tăng như $\ln(1/\delta)$, theo Chebyshev như $1/\delta$; **ở §6, $\delta$ được chia cho số ứng viên.**" → bỏ cụm "ở §6, $\delta$ được chia cho số ứng viên" (chỉ dẫn điều hướng); gộp nhãn "Kết luận". *§2.2, §1.*
5. **Dòng 537** — "**Kết luận.** Cận một phía $8{,}9\%$ chặt hơn đầu mút $9{,}3\%$ của khoảng hai phía. **Phần thứ hai của câu hỏi mở đầu cần một cận cho hàm được chọn theo $S$.**" → bỏ câu thứ hai (chỉ dẫn điều hướng); gộp nhãn "Kết luận". *§2.2, §1.*
6. **Dòng 574** — "…tạo ra đúng tình huống này; **Bài 06 xét chúng với giả thiết khác.**" → bỏ cụm "Bài 06 xét chúng với giả thiết khác". *§2.2; §2.4 nhận xét bên lề.*
7. **Dòng 577** — "Bỏ tính độc lập (Ví dụ 02.6), cận của Định lý 02.7 sai. Bỏ tính bị chặn (Nhận xét 02.11), không còn cận đuôi nào… **Phần còn lại của bài giữ cả hai giả thiết.**" → bỏ câu cuối "Phần còn lại của bài giữ cả hai giả thiết" (chỉ dẫn điều hướng). *§2.2.*
8. **Dòng 586** — "**Cấu trúc độc lập này chỉ dựng ra để tính chính xác, không mô tả các mô hình thực.**" → cắt (câu rào đón). *§2.1.*
9. **Dòng 640** — "…tính liên tục của xác suất cho $\Pr(\bigcup_kB_k)\le\sum_k\Pr(B_k)$. **Bài tập 02.6 dùng dạng này.**" → bỏ câu "Bài tập 02.6 dùng dạng này". *§2.2.*
10. **Dòng 648** — "**Tính đại diện phụ thuộc $D$ chưa biết, nên không kiểm tra được từ $s$.** Với $\mathcal H$ hữu hạn, **biến cố hội tụ đều là giao của $K$ biến cố đo được, nên đo được.** Trên mẫu $S_\eta$…" → cắt câu thứ nhất (câu nói hiển nhiên) và câu thứ hai (bình luận đo được). Giữ nguyên phần tính toán các hiệu $-0{,}02$; $0{,}0133$; …; $0{,}02$ và kết luận $\epsilon\ge0{,}18$. *§2.6, §2.3.*
11. **Dòng 711** — "…chọn theo $S$ bằng một quy tắc đo được **(Phụ lục C)** và mọi $D$…" → bỏ "(Phụ lục C)". *§2.2.*
12. **Dòng 739** — "Các đại lượng dùng ở đây đo được với lớp hữu hạn **(Phụ lục C)**." → bỏ "(Phụ lục C)". *§2.2.*

---

### s7 (§7 ERM trên lớp hữu hạn trong trường hợp bất khả tri)

1. **Dòng 782** — "…được mở rộng sang trường hợp **bất khả tri**, phần (c) cho…" → "bất khả diễn". *§5.*
2. **Dòng 803** — "$\square$ Hệ số $2$ đến từ hai phép so sánh, tại $\hat h$ và tại $h_{\mathcal H}$ **(Bài tập 02.3)**; bảo đảm không phụ thuộc quy tắc chọn khi bằng nhau." → bỏ "(Bài tập 02.3)". *§2.2.*
3. **Dòng 832** — "**Theo lý do (ii) ở §7 của Bài 01,** khi $\mathcal X$ hữu hạn, ERM trên $\mathcal M_{\mathcal X}$ đạt rủi ro Bayes cộng $\epsilon$ cho mọi $D$." → bỏ cụm "Theo lý do (ii) ở §7 của Bài 01". *§2.2.*
4. **Dòng 858** — "Cỡ mẫu tăng tuyến tính theo $|\mathcal X|$, **phù hợp với Nhận xét 01.30.** Khi $\mathcal X$ vô hạn, cận này không cho gì." → bỏ cụm "phù hợp với Nhận xét 01.30". *§2.2.*

---

### s8 (§8 Lớp hữu hạn trong trường hợp khả thực)

1. **Dòng 865, 869, 875, 901, 905, 984, 996, 1004** — mọi "khả thực" → "khả diễn" (tiêu đề §8, tên Mệnh đề 02.17, nhãn "**Tính khả thực.**", "Bỏ tính khả thực", "cặp $(D_f,\mathcal H)$ khả thực", "khi khả thực", "Cột khả thực… giả thiết khả thực", "Trong trường hợp khả thực"). *§5.*
2. **Dòng 904** — "Ví dụ 02.11 (Bốn mức cỡ mẫu cho **bản nhãn tất định**)" → "dữ liệu tất định". *§5.*
3. **Dòng 936** — "Làm tròn lên được $30$, **cỡ mẫu ở §9 của Bài 01 (lập luận của Bài tập 01.9).**" → bỏ cụm "cỡ mẫu ở §9 của Bài 01 (lập luận của Bài tập 01.9)". *§2.2.*
4. **Dòng 952** — "**Ba cỡ mẫu của §6–§8 trả lời câu hỏi thực hành thứ hai của ứng dụng ở §3.**" → cắt (chỉ dẫn điều hướng). *§2.2.*
5. **Dòng 1004** — "…và $1/\epsilon^2$ khi phương sai cỡ hằng số (đọc thêm, Phụ lục B.5 của giáo trình…). **Chúng ta chưa chứng minh tốc độ $1/\epsilon^2$ là cần thiết; một cận dưới phải lập luận cho mọi thuật toán, và Bài 03 phát biểu (không chứng minh) một cận dưới như vậy.**" → bỏ câu cuối (chỉ dẫn điều hướng Bài 03 + nhận xét bên lề). *§2.2, §2.4.*

---

### s9-12 (§9 Ý nghĩa, §10 Bài tập, §11 Câu hỏi cuối buổi, §12 Tài liệu đọc)

1. **Dòng 1011** — "…cho trường hợp **khả thực** (Mệnh đề 02.17)…" → "khả diễn". *§5.*
2. **Dòng 1015** — "…nhờ các cận đuôi mũ (Hoeffding; $(1-\epsilon)^m$ khi **khả thực**)." → "khả diễn". *§5.*
3. **Dòng 1021** — "…chia $\delta$ theo trọng số **(Bài tập 02.6; Bài 04)**." → bỏ "(Bài tập 02.6; Bài 04)". *§2.2.*
4. **Dòng 1060** — "…trong trường hợp **khả thực**, ta đã có cận cỡ mẫu cho hai lớp vô hạn…" → "khả diễn". Giữ "(Bài tập 01.9)", "(Bài tập 02.7)" (cần để định danh lớp) và câu cầu nối "Câu hỏi cho Bài 03 là…" (đây là mục đích của §11 cầu nối). *§5; §2.2 giữ dẫn chiếu khi cần mở để lấy đối tượng.*
5. **Dòng 1072** — "**Trường hợp khả thực.** Viết với **phân bố đồng thời** $D$ thay cho cặp $(D,f)$ của UML Chương 2." → "khả diễn"; "phân bố liên hợp". *§5.*

---

### phu-luc (Phụ lục)

1. **Dòng 1148** — "Với lớp hữu hạn, điều kiện đo được nêu ở **Phụ lục A(v) của Bài 01** tự thỏa." → **ứng viên giữ** (dẫn chiếu cần để định danh điều kiện đo được); nếu cắt thì chỉ bỏ "của Bài 01" và giữ "Phụ lục A(v)". *§2.2: giữ dẫn chiếu khi người đọc phải mở để lấy phát biểu.*
2. Không có thay đổi khác: Phụ lục A, B, C giữ nguyên số liệu và khối.

---

### chung (quy tắc áp dụng cho mọi phần)

1. **Thuật ngữ theo §5** (đổi toàn bộ bài): "khả thực" → "khả diễn"; "bất khả tri" → "bất khả diễn"; "bản có nhiễu / bản nhãn tất định" → "dữ liệu có nhiễu / dữ liệu tất định"; "phân bố đồng thời" → "phân bố liên hợp"; "mẫu" (chỉ dữ liệu huấn luyện) → "tập huấn luyện" (giữ "cỡ mẫu", "lấy mẫu", "mẫu $S_\eta$", "mẫu xác thực"). Không thấy "hàm chỉ thị" trong bài nên không cần đổi.
2. **Cắt chỉ dẫn điều hướng / báo trước** (§2.2): mọi cụm "ở §…", "Bài tập …", "Bài 0X …", "Phụ lục …" chỉ để báo trước đều bỏ; chỉ giữ dẫn chiếu khi người đọc phải mở để lấy số hoặc phát biểu (Ví dụ 01.x, Định nghĩa 01.x, Mệnh đề 01.x, Nhận xét 01.x, Phụ lục A(v)).
3. **Cắt câu rào đón, nhận xét bên lề, câu nhắc lại kết quả, câu nói hiển nhiên, đoạn tự hỏi tự đáp** (§2.1, §2.4, §2.6, §2.7).
4. **Cắt bình luận kĩ thuật đo được / quy ước dấu** (§2.3) khi không phục vụ mạch chính; giữ định nghĩa và giả thiết.
5. **Giữ mọi khối đánh số và mọi con số** — bài tập trích dẫn: Bổ đề 02.2, 02.3, 02.5, 02.6, 02.12; Định lý 02.7, 02.14; Hệ quả 02.10, 02.16; Mệnh đề 02.17; Định nghĩa 02.9, 02.13; Nhận xét 02.8; Ví dụ 02.3, 02.7, 02.12. Chỉ cắt câu trong mạch văn, không cắt kết quả, không đổi số.
6. **Ý nghĩa tích cực thay cho "không phải"** (§6a): các câu phủ định về bản chất của bảo đảm (dòng 138, 178, 440) diễn đạt lại theo nghĩa vận hành.
7. **Gộp nhãn bước "Kết luận"** (§1) khi chỉ là bước chuyển/recap, không phải phép tính độc lập (dòng 175, 267, 509, 537).
8. **Giọng văn**: chủ ngữ là thuật toán/hàm/"ta", động từ trực tiếp; từ nối giải thích ("Nghĩa là", "Do đó", "Tóm lại"); in nghiêng thuật ngữ mới ở lần đầu, in đậm ý then chốt dùng tiết kiệm. Không thêm khẳng định, số liệu, nguồn mới ngoài bản hiện tại.
9. **Markdown**: chỉ dùng `$...$` và `$$...$$`; không đổi kí hiệu toán; không thêm dấu cách trước "?"; dùng `\mid` và `\Pr` trong xác suất có điều kiện.
10. **Câu hỏi cho người học** (§7.6): bài đã có "**Câu hỏi.**" ở mở đầu (dòng 11) và §11 (dòng 1041), "**Câu hỏi thực hành.**" (dòng 117) — đủ, không thêm mới trừ khi tác giả yêu cầu.

---

**Ghi chú bổ sung cho tác giả (không tự sửa):** nhãn "**Đối tượng so sánh.**" ở §1 mục 7 (dòng 59) — §5 của `van-phong-tac-gia.md` cho biết nhãn này đã bỏ ở Bài 01 nhưng khái niệm vẫn dùng ở §7; cần quyết định đổi nhãn hay giữ.