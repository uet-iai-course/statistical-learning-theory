# Rà lại mạch, móc nối và văn phong sau biên tập vòng 1 — Bài 10

Người rà: người rà 5 (general-purpose, Opus 5.5, high), chỉ đọc repo, không commit.

- **Đối tượng.** Bản sửa cố định `lec10-r1-frozen.md` (1 040 dòng; thân 11 976 tiếng theo `wc -w` trước "## Phụ lục"). Bản sao kiểm ở `reviews10/r5b/lec-10/lecture-note.md`. Số dòng bên dưới theo bản này.
- **Căn cứ.** `reviews/0-quyet-dinh.md`, `bien-tap-vong-1.md`, `reviews/4-hoc-thuat-van-phong.md`, `reviews/5-mach.md`, `ky-hieu.md`, `thuat-ngu.md`.
- **Văn phong.** Kiểm theo `no-ai-slop` Detect và `van-phong.md`.

## Tổng kết theo mức

- **Chặn bàn giao:** 0. **Nghiêm trọng:** 0. **Trung bình:** 0.
- **Nhẹ:** 12 phát hiện mới (bảng cuối). Tất cả sửa được trong ngân sách: tổng chữ thêm khoảng +33, ba chỗ cắt bù −41.
- **Phát hiện cũ của người rà 5:**
  - 5/5 mục trung bình ✓;
  - 10/11 mục nhẹ ✓, 1 mục một phần (N9: câu dẫn có nhưng chưa trọn nghĩa).
- **Mục trung bình của người rà 4:**
  - 8/9 ✓;
  - T1 một phần: §6 và §8 kết bằng khối ví dụ hoặc một câu lặp; xem mục 1 và 12 ở bảng cuối;
  - T6 ✓, nhưng chữ "khác dấu" chưa chính xác (mục 7).
- **`forward_refs.py`:** `0 forward references` (đường dẫn tuyệt đối tới bản sao).
- **Tổng kết học phần:** nhìn lại đủ Bài 01–09. Phụ lục D xếp Bài 01–08 vào dòng học có giám sát, Bài 09 vào dòng ước lượng mật độ, và có Thiết lập B. Mạch §12 → lời giải (f) → Phụ lục D ổn: lời giải tóm một câu rồi dẫn Phụ lục D, Phụ lục D có câu dẫn. Còn hai chỗ lệch nhỏ (mục 8, 9).

## Đối chiếu phát hiện cũ

### Người rà 5

| Mã | Kết quả | Bằng chứng (dòng mới) |
|---|---|---|
| T1 $M$ hai nghĩa | ✓ | Hàm trội là $\Lambda$ ở 309, 900–935; $M$ chỉ còn nghĩa ngân sách bộ nhớ (608 trở đi). `ky-hieu.md` chưa có dòng $\Lambda$ (mục 11) |
| T2 $B$ → $R$ | ✓ | 791–795 ("như Hệ quả 05.15"), 812 |
| T3 $\mathcal F_t$ | ✓ | 428 nêu "bộ biến quan sát được trước $A_t$", σ-đại số, $\mathcal F_{t-1}$, Bổ đề 05.12. `ky-hieu.md` dòng 111 đã sửa |
| T4 Ví dụ 10.16 | ✓ | 753–769: $L_A(\tfrac12)=\tfrac58$, $\tfrac58+\tfrac1{8M}$; câu thí nghiệm nêu mô hình khác; Phụ lục C dòng 988 |
| T5 §12(f) | ✓ | Phụ lục D có Bài 01–08 (1010–1016) và Thiết lập B (1024); lời giải (f) dòng 879 dẫn Phụ lục D |
| N1 $K$ | ✓ | 60 (giới thiệu trước bảng 74); Phụ lục A dùng $C_\mu$ (935) |
| N2 $R$ trần | ✓ | 167, 555–569, 583. $R\equiv1$ (926) và $\lvert R\rvert\le C_R$ (935) là hàm, chấp nhận |
| N3 tên trạng thái | ✓ | 172 (câu phân biệt), 384 ($\ln P(S_1\mid s_0,A_0)$) |
| N4 $\tau$ của 08.12 | ✓ | 169 |
| N5 tiên quyết | ✓ | 30–33: thêm (T3), 05.2, 05.7, 05.15, 09.7, 09.10; bỏ 05.11, 09.14 |
| N6 "người học" | ✓ | Chỉ còn ở 19 ("Sau bài này, người học có thể") |
| N7 "môi trường" = nhiệm vụ | ✓ | 601 |
| N8 mục tiêu 5 | ✓ | 25 |
| N9 câu dẫn Ví dụ 10.12 | một phần | 576 có câu dẫn, nhưng chủ ngữ "các lượt … cho một cận" sai: cận đến từ bất đẳng thức Hoeffding (mục 6) |
| N10 §10 đoạn 2 | ✓ | 827 |
| N11 tự hỏi tự đáp | ✓ | 15 |

### Người rà 4, các mục trung bình

| Mã | Kết quả | Bằng chứng |
|---|---|---|
| T1 câu kết mục | một phần | §5: 422 là một câu giới hạn cụ thể ✓. §7: 652 ✓. §9: 821 ✓. §6 kết bằng Kết luận của Ví dụ 10.12 (596), không có câu văn xuôi ngoài khối; biên tập viên chủ ý, chấp nhận được. §8: 772 lặp ý của 700 và 735 (mục 12) |
| T2 ý "chỉ giữ kì vọng" | ✓ | Còn ở 269, 438, 545 (dạng mới "giảm hoặc tăng tùy bài toán"), 490 (một vế) |
| T3 "người học" | ✓ | như N6 ở trên |
| T4 ví dụ đổi thiết lập | ✓ | 529 ("Bước 3 dùng một biến thể"), 631 ("Bước 5 dùng ma trận thứ hai"), 753–769 |
| T5 ví dụ từng bước | ✓ | 376–382, 531–541, 559–567, 592, 745, 767, 814–816 |
| T6 quy ước độ đo | ✓, có lưu ý | 626 bỏ "các bài báo", khớp 894. Chữ "khác dấu" chưa đúng (mục 7) |
| T7 đoạn mở | ✓ | 3, 5. Câu cuối dòng 5 vẫn lặp 827 (chỗ cắt C1) |
| T8 dòng 768 cũ | ✓ | 786 |
| T9 câu dài | ✓ | 143, 549, 703, 733, 827 đã tách. Có một câu dài mới ở 769 (khoảng 55 tiếng, mục 10) |

## Kí hiệu và thuật ngữ đã đổi (đọc tay)

- **$\Lambda$.** Dùng thống nhất ở Nhận xét 10.5 và Phụ lục A, không còn $M(\tau)$. Phụ lục A dòng 903 nối với "điều kiện (i) của Mệnh đề 09.15" nhưng không nhắc rằng Bài 09 gọi hàm trội là $M$. Không cần sửa.
- **$R$.** Ở Phần B, $R$ trần là cận $\lVert w_1-u\rVert$ như Bài 05; Phần A luôn viết $R(\tau)$ hoặc $R_{\ge t}$. Nhất quán.
- **$\mathcal F_t$.** Dòng 428 khớp `ky-hieu.md` dòng 111. Các chỗ dùng (442–452, 463, 529, 551, Phụ lục B dòng 942) đều là "bộ biến trước $A_t$".
- **$L_{\mathrm{buf}}$.** Dùng ở 661, 666, 757; không còn trùng $L_B$. Chưa có trong `ky-hieu.md` (mục 11).
- **$\mathbf o$, $\mathbf o^+$, $\Delta$, $\Delta_0$, $C_\mu$, $\kappa$.** Mỗi chữ một nghĩa trong bài: $\kappa$ ở Ví dụ 10.9 khác $\kappa$ của Mệnh đề 09.15, nhưng ở hai bài khác nhau.
- **"tác tử" / "thuật toán học".** "Thuật toán học" chỉ ở đoạn mở (3, 5); "tác tử" từ §1 trở đi.
- **"độ chính xác phân lớp".** Được định nghĩa ở 619. Mục tiêu 4 (24), 620, 628, 639, 652 dùng thống nhất. Tiêu đề Bài tập 10.4 (845) còn tên cũ (mục 5).
- **"chính xác" (trạng từ) và "nghiệm".** Còn "nghiệm" ở §12(d), dòng 862 (mục 4). Dòng 9 có "chính xác suất $q$": chữ "chính" (nhấn mạnh) đứng trước "xác suất" làm câu đọc thành "chính xác" (mục 3).

## Mạch sau các chỗ cắt và chỗ đổi

- **Đoạn mở → câu hỏi mở đầu → §5.**
  - Câu hỏi mở đầu (15) không còn nói "đạo hàm theo $q$ bằng $0$", mà dòng 206 ("Ở câu hỏi mở đầu, đạo hàm … bằng $0$") và 299 vẫn nhắc lại ý đó như đã nêu (mục 1).
  - Câu trả lời cho tình huống 2 (15) dẫn đúng §7 (614) và §8.
- **§3 → §4.** Câu cuối §3 đã cắt. §4 mở bằng robot (130), nên ranh giới vẫn rõ.
- **§5.**
  - Câu trỏ vòng ở 249 cũ đã bỏ; Ví dụ 10.3 kết thúc ở 250 và Nhận xét 10.5 (311) nhắc lại Ví dụ 10.3, nên không mất móc nối.
  - Đoạn 406 có cụm "các biến đều" đọc được thành "mọi biến" (mục 2), và cụm "Trở ngại thật là" (mục 2).
- **§6.**
  - 576 có câu dẫn mới (mục 6).
  - Mục kết ở Ví dụ 10.12 (596), không có câu kết văn xuôi; chấp nhận được.
- **§6 → §7 → §8.**
  - 601 nối tình huống 2 đúng.
  - Đoạn 626–628 tách thành hai đoạn; "ví dụ dưới đây" vẫn trỏ đúng Ví dụ 10.13.
  - 656 định nghĩa "xung đột" trước Mệnh đề 10.13.
  - 703 dùng đúng (a) và (c).
- **§8 → §9.** 772 lặp 700 và 735 (mục 12). 776 mở §9 với thuật ngữ in nghiêng và có tiếng Anh ✓.
- **§10.** Câu "Đổi quy ước đo làm độ quên đổi dấu" (834) không khớp kết luận của Ví dụ 10.13 (649: "$0$ hay $-0{,}03$") (mục 7).
- **§12 → Phụ lục D.**
  - Câu (f) hỏi "phân lớp có giám sát", nhưng tiêu đề Phụ lục D là "Phân lớp và hồi quy có giám sát" (mục 8).
  - Câu tóm tắt ở 879 bỏ thay đổi (T3), (T2) của ước lượng mật độ, cột chính của dòng Bài 09 (mục 9).
  - Phụ lục D đứng sau Phụ lục C, có câu dẫn (1008). `forward_refs.py` chỉ quét phần trước "## Phụ lục", nên Phụ lục D, vốn nhìn lại các khối trước, không gây lỗi.

## Bảng phát hiện mới (dòng theo `lec10-r1-frozen.md`)

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | 1. 15; 206; 299 | Hai chỗ dẫn ngược nhắc một khẳng định mà câu hỏi mở đầu không còn nói | 15 "trung bình các phần thưởng là một số cố định, không chứa $q$; nó không cho biết …"; 206 "Ở câu hỏi mở đầu, đạo hàm theo $q$ của trung bình các phần thưởng đã nhận bằng $0$." | Dòng 15: "…là một số cố định, không chứa $q$, nên đạo hàm của nó theo $q$ bằng $0$, dù phần thưởng kì vọng đổi khi $q$ đổi; đạo hàm của phần thưởng kì vọng vẫn ước lượng được từ dữ liệu (§5)." (khoảng +4) |
| nhẹ | 2. 406 | "các biến đều" đọc được thành "mọi biến"; "Trở ngại thật là" là kiểu câu "cái thật sự là X" (`no-ai-slop`) | "Viết mỗi lượt như một hàm của $\theta_j$ và các biến đều độc lập với các lượt trước, … Trở ngại thật là (C)" | "…như một hàm của $\theta_j$ và các biến có phân bố đều, độc lập với các lượt trước, … Trở ngại là (C), …" (+2) |
| nhẹ | 3. 9 | "chính xác suất $q$": người đọc ngắt thành "chính xác / suất", trái quyết định 6 về chữ "chính xác" | "phụ thuộc chính xác suất $q$ mà robot đang học" | "phụ thuộc xác suất $q$ mà robot đang học" (−1) |
| nhẹ | 4. 862 | Còn "nghiệm", trái quyết định 6 ("nghiệm" → "điểm cực tiểu") | "(d) … tỉ lệ phát lại $\alpha$ cho cùng nghiệm." | "…cho cùng điểm cực tiểu." (+2) |
| nhẹ | 5. 845 | Tiêu đề Bài tập 10.4 chưa theo thuật ngữ mới; tệp bài tập phải dùng cùng tiêu đề | "(Độ chính xác trung bình cuối cùng, chuyển đổi và độ quên …)" | "(Độ chính xác phân lớp trung bình cuối cùng, chuyển đổi và độ quên …)" (+2); báo người viết bài tập |
| nhẹ | 6. 576 | Câu dẫn gán việc "cho một cận" cho các lượt, trong khi cận đến từ bất đẳng thức Hoeffding | "khi chính sách cố định, các lượt thỏa (T1) và cho một cận với xác suất cao." | "Các kết quả trên là đồng nhất thức. Khi chính sách cố định, các lượt thỏa (T1), và bất đẳng thức Hoeffding cho một cận với xác suất cao." (+4) |
| nhẹ | 7. 626; 834 | "khác dấu" và "đổi dấu" không khớp Ví dụ 10.13: với quy ước của học phần, độ quên ở nhiệm vụ 2 bằng $0$, không dương | 626 "hai quy ước gần nhau cho độ quên khác dấu"; 834 "Đổi quy ước đo làm độ quên đổi dấu"; 649 "bằng $0$ hay $-0{,}03$" | 626: "…ví dụ dưới đây cho thấy một quy ước gần với quy ước này cho độ quên âm." 834: "Đổi quy ước đo có thể cho độ quên âm (Ví dụ 10.13)." (+2) |
| nhẹ | 8. 866 và Phụ lục D dòng 1010, 1013 | Câu hỏi (f) và lời giải nói "phân lớp có giám sát", tiêu đề Phụ lục D nói "phân lớp và hồi quy". Bài 08 có phần không lồi (Mệnh đề 08.12), không chỉ "hàm lỗi lồi" | 866 "(phân lớp có giám sát, …)"; 1010 "*Phân lớp và hồi quy có giám sát (Bài 01–08).*"; 1013 "hay hàm lỗi lồi (Bài 05–06, 08)" | Giữ chữ của blueprint ở 866. Phụ lục D: "*Phân lớp có giám sát (Bài 01–08).*" và "…hay hàm lỗi lồi hoặc trơn thay cho hàm lỗi 0–1 (Bài 05–06, 08)." (phụ lục, không tính vào thân) |
| nhẹ | 9. 879 | Câu tóm tắt chỉ nêu (T1) cho ước lượng mật độ. Thay đổi chính của Bài 09 là (T3), (T2) (hàm lỗi log không bị chặn), mà ở §12 chỉ thấy được qua Phụ lục D | "Phân lớp có giám sát và ước lượng mật độ dùng (T1) với một $D$ cố định, trừ chuỗi thời gian của Bài 09; …" | "Phân lớp có giám sát dùng (T1) với một $D$ cố định; ước lượng mật độ bỏ (T3) vì hàm lỗi log không bị chặn, và bỏ (T1) với chuỗi thời gian; …" (+8) |
| nhẹ | 10. 769 | Câu thí nghiệm dài khoảng 55 tiếng, gộp mô hình, bốn số và hai mốc (`van-phong.md` §9) | "Thí nghiệm của học phần (Phụ lục C) dùng một mô hình hồi quy khác, có rủi ro tổng thể trên A là …; rủi ro kiểm tra trên A sau nhiệm vụ B giảm từ $0{,}624$ … không về $0{,}125$." | Tách sau "$\tfrac12(w^2+0{,}25)$": "…là $\tfrac12(w^2+0{,}25)$. Sau nhiệm vụ B, rủi ro kiểm tra trên A giảm từ …" (0) |
| nhẹ | 11. `ky-hieu.md` (điều phối viên) | Hai kí hiệu mới của bản sửa chưa có trong bảng kí hiệu | $\Lambda$ (309, Phụ lục A); $L_{\mathrm{buf}}$ (661) | Thêm "$\Lambda$: hàm trội (Bài 10; Bài 09 viết $M$)" và "$L_{\mathrm{buf}}$: rủi ro thực nghiệm trên bộ đệm (Bài 10; khác $L_B$)" |
| nhẹ | 12. 772 (so với 700, 735) | Câu kết §8 lặp lần thứ ba ý "phạt bậc hai đúng khi rủi ro cũ là hàm bậc hai, chỉ xấp xỉ khi khác" (`no-ai-slop`: lặp; người rà 4 T1) | 700 "Phạt $\frac\lambda2w^2$ đúng bằng $\lambda L_A(w)$ …"; 735 "nó bằng đúng phần tăng của rủi ro cũ khi rủi ro cũ là hàm bậc hai (Mệnh đề 10.13)"; 772 "Mọi rủi ro cũ trong §8 là hàm bậc hai; …" | Giữ 772 làm câu kết mục. Cắt ở 735 vế "; nó bằng đúng phần tăng của rủi ro cũ khi rủi ro cũ là hàm bậc hai (Mệnh đề 10.13)", để câu còn "Phạt bậc hai là khai triển Taylor bậc hai của rủi ro cũ quanh điểm cực tiểu $w^{(1)}$, với $\Omega$ là ma trận Hesse." (−17; chỗ cắt C2) |

## Ngân sách chữ (thân 11 976/12 000)

- **Chữ thêm.** Mục 1 (+4), 2 (+2), 3 (−1), 4 (+2), 5 (+2), 6 (+4), 7 (+2), 9 (+8): khoảng +23. Nếu viết dài hơn ở mục 1 và 9, tối đa khoảng +33.
- **Chỗ cắt.**
  - **C1 (−8).** Dòng 5: bỏ "Phần B không có định lý tổng quát.", vì 827 đã nói "chưa có định lý học liên tục tổng quát".
  - **C2 (−17).** Dòng 735: bỏ vế lặp như mục 12.
  - **C3 (−16).** Dòng 614: bỏ vế "; mỗi mẫu thỏa (T1) với phân bố của nó, nhưng không có một $D$ chung", lặp gần nguyên văn dòng 78. Câu còn: "Các mẫu, bộ nhớ, nguồn ngẫu nhiên của thuật toán và các mẫu kiểm tra là ngẫu nhiên."
- **Kết quả.** C1 + C2 + C3 = −41. Thân bài sau sửa khoảng 11 958–11 968 tiếng, dưới trần.
