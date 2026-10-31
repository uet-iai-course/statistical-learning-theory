# Rà lại mạch, móc nối và văn phong sau biên tập vòng 1 — Bài 08

Người rà 5 (chỉ đọc repo, không commit). Đối tượng: `lec08-r1-frozen.md` (1 111 dòng; trùng byte với `2627-1/materials/lec-08/lecture-note.md`). Số dòng dưới đây theo bản này. Căn cứ: `reviews/0-quyet-dinh.md`, `bien-tap-vong-1.md`, `reviews/4-hoc-thuat-van-phong.md`, `reviews/5-mach.md`, `lec08-r1.udiff`. `no-ai-slop` dùng ở chế độ Detect.

## Tổng kết theo mức

| Mức | Số | Tóm tắt |
|---|---|---|
| chặn bàn giao | 0 | |
| nghiêm trọng | 0 | |
| trung bình | 2 | M1: câu mới ở dòng 193 nói khoảng cách giữa hai lần chạy với dãy chỉ số độc lập "không đo độ nhạy theo một quan sát của mẫu", nhưng hai lần chạy này chạy trên hai mẫu khác nhau; M2: "Thừa số này" ở dòng 746 mất chỗ dựa sau khi chứng minh chuyển sang Phụ lục F |
| nhẹ | 10 | câu mở §6 mất vế "bước chung"; dòng 218 sai ngữ pháp; cầu nối mất "Câu hỏi cho Bài 09"; câu mở §9 và câu chuyển dòng 796 không khớp ba điều kiện của mạng ReLU; còn hai phép đối ở dòng 445; câu thừa ở dòng 682; $g'$ hai nghĩa; "khoảng cách" hai nghĩa ở dòng 1050; Phụ lục F dùng $\Gamma$ chưa gọi tên; dòng 187 lặp "cho" |

`forward_refs.py` (bản sao `reviews08/r5b/lec-08/lecture-note.md`): **0 forward references** (exit 0). Kiểm tay các dẫn chiếu mới "Phụ lục E", "Phụ lục F" (dòng 599, 630, 715, 744), "Mệnh đề 01.7" (483), "Ví dụ 06.3, Bước 5" (593), "(§7)" ở dòng 109: đều đúng chỗ.

Thân bài 11 982/12 000. Các đề xuất dưới đây thêm khoảng 20 chữ và cắt khoảng 21 chữ, thân bài còn khoảng 11 981 (chi tiết ở §6).

## 1. Phát hiện cũ của người rà 5 (`5-mach.md`)

| Mã | Kết quả | Ghi chú |
|---|---|---|
| TB P1 "tính đồng bức" trước định nghĩa | ✓ | Dòng 109: "chứng minh ở Phụ lục A" |
| TB P2 Phụ lục D Bài 07 | ✓ | Dòng 682: "một lập luận … với độ dài bước đủ nhỏ … khi nghiệm nội suy tồn tại" |
| TB P3 bố cục §9 | ✓ | Thứ tự: Ví dụ 08.8 → Mệnh đề 08.10 → Nhận xét 08.11 → Mệnh đề 08.12 → câu chuyển 796 → Ví dụ 08.9 → Ví dụ 08.10 → câu kết 834. Số vẫn tăng. Có hai điểm chữ nhẹ (N4 dưới đây) |
| P4 tiên quyết | ✓ | Đã bỏ Ví dụ 06.9; thêm trung bình cộng–trung bình nhân và (C) |
| P5 $\beta$, $G$ ở bảng §1 | ✓ | Dòng 82, 86 |
| P6 $c$, $s$ | ✓ | $\kappa$ cho hệ số giãn, $k$ cho chỉ số cộng |
| P7 (T2) | ✓ | Dòng 103 |
| P8 nguồn số ở §10 | ✓ | Dòng 838 |
| P9 cầu nối | một phần | "điểm $z$" và "(likelihood)" đã sửa; nhưng câu dẫn "Câu hỏi cho Bài 09 là" bị bỏ (N3) |
| P10 tiền kích hoạt | ✓ | Dòng 827 |
| P11 Bài tập 07.5(c) | ✓ | Dòng 828 |
| P12 nguồn số $0{,}603$ | ✓ | Dòng 684 |
| P13 §10 kết bằng văn xuôi | ✓ | Dòng 856 |
| P14 lặp (a)–(d) | ✓ | (b) để lại một câu mở §6 thiếu vế (N1) |
| P15 "qua số bước và độ dài bước" | ✓ | Dòng 3 |
| P16 "sai số tối ưu" | ✓ | Dòng 632, 774 |
| $\Delta$ có chỉ số ở Ví dụ 08.6 | ✓ | Dòng 528, 530 |
| Dòng 691 (vai trò của $1/\lambda$) | ✓ | Dòng 682: "chỉ là một gợi ý về dạng công thức" |

## 2. Phát hiện trung bình của người rà 4

| Mã | Kết quả | Ghi chú |
|---|---|---|
| T1 chỗ dùng tính lồi | ✓ | Dòng 351, 455, 497, 690, 744, 1106, 1110 thống nhất: tính lồi của hàm lỗi chỉ qua Bổ đề 08.4(a) ở bước chung; tính lồi của $W$ cho tính không giãn của phép chiếu và tính Lipschitz |
| T2 ví dụ từng bước | ✓ | Ví dụ 08.2 Bước 1 liệt kê đạo hàm; Ví dụ 08.4 có lý do cho nhóm $i_1\ne4$ và bảng cho nhóm $i_1=4$ (đã tính lại bốn dòng và quỹ đạo $(2,3,1,4,4,4)$: khớp) |
| T3 dòng 578 | ✓ | Dòng 586–593 |
| T4 câu kết mục | ✓ | 218 → giới hạn (sai ngữ pháp, N2); 305, 407, 593, 834 là văn xuôi nêu giới hạn. §3 nay kết bằng khối ứng dụng, như §3 của Bài 06; chấp nhận được |
| T5 lặp | ✓ | "11–109 lần" chỉ ở dòng 542; "$0{,}309$; …" chỉ ở dòng 684 (Phụ lục D nêu khoảng); "đo tính ngẫu nhiên" chỉ ở dòng 193; $\sqrt3$, $\sqrt2$ ở dòng 627 và 920 |
| T6 phép đối | một phần | Dòng 445 còn hai vế "chứ không" liền nhau (N5); dòng 193 còn một phép đối và nội dung sai (M1) |
| T7 công thức ở 390 px | không kiểm lại | Ngoài phạm vi lượt này; biên tập viên báo đo 0 tràn và 0 dòng cắt giữa chuẩn |

## 3. Mạch sau các chỗ cắt và chuyển

- **Câu ôn nhanh 2 (phép chiếu) bị cắt.** Không còn chỗ nào nhắc "câu ôn nhanh 3". Lời giải đánh số 1–2 khớp đề. Tính không giãn của phép chiếu vẫn có trong danh sách tiên quyết (dòng 41) và được dẫn ở Bổ đề 08.4 Bước 3. Không đứt mạch.
- **Lần chạy không ghép cặp bị chuyển khỏi Ví dụ 08.6.** Thân bài chỉ còn phép tính một bước ở §4 (dòng 191–193). Ví dụ 08.6 không còn nhắc lần chạy thứ ba. Phụ lục D giữ lần chạy thứ ba (1042) và bảy giá trị (1050). Mạch liền, nhưng câu kết luận mới ở dòng 193 sai nội dung (M1).
- **Chứng minh Hệ quả 08.8 chuyển sang Phụ lục E.** Tiêu đề khối ghi "(ở Phụ lục E)". Đoạn lộ trình ở dòng 630 đủ cho người đọc, và câu ở dòng 632 nối tiếp đúng. Đạt.
- **Chứng minh Mệnh đề 08.10 chuyển sang Phụ lục F.** Đoạn lộ trình ở dòng 744 đạt. Dòng 746 mở bằng "Thừa số này", nhưng đoạn ngay trước không còn nhắc thừa số nào. Trước đây, câu $\square$ của chứng minh nói về $\prod_s(1+\beta\eta_s)$ (M2).
- **Thứ tự phụ lục.** Thân bài đọc theo thứ tự E (Hệ quả 08.8), F (Mệnh đề 08.10), C (Mệnh đề 08.12), và giao thức D nằm giữa các chứng minh. Đánh lại chữ (C ↔ Mệnh đề 08.12, E, F, giao thức cuối) sẽ phải sửa mọi chỗ dẫn "Phụ lục D". Tùy chọn, không bắt buộc.
- **Lời hứa.** Bài 06 dòng 620 và 1295 → Định lý 08.6(a) và dòng 187. Bài 06 dòng 1071 → dòng 586–593. Bài 06 dòng 1130 → Hệ quả 08.7. Bài 07 dòng 960 → dòng 3 (đã thêm "qua số bước và độ dài bước") và dòng 838. Tất cả vẫn giữ. Cầu nối sang Bài 09 khớp blueprint 8.6 và không phát biểu kết quả của Bài 09, nhưng không còn gọi tên Bài 09 (N3).

## 4. Bảng phát hiện mới (dòng theo `lec08-r1-frozen.md`)

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | §4, dòng 193 (M1) | Hai lần chạy trong ý này chạy trên $s$ và $s^{(4)}$ với hai dãy chỉ số độc lập. Khoảng cách $\tfrac38$ gồm cả hiệu $\tfrac14$ do thay quan sát, nên câu "không đo độ nhạy" sai. Câu cũ đúng vì khi đó hai lần chạy dùng cùng một mẫu. | "Liệt kê $16$ cặp chỉ số cho $\mathbb E\lvert w_2-w'_2\rvert=\tfrac38$, lớn hơn hiệu. Khoảng cách này đo tính ngẫu nhiên của thuật toán, không đo độ nhạy theo một quan sát của mẫu." (đã tính lại: $6/16=\tfrac38$) | "Khoảng cách này còn chứa tính ngẫu nhiên của thuật toán, nên lớn hơn hiệu cần chặn." (−3 chữ; bỏ luôn phép đối) |
| trung bình | §9, dòng 746 (M2) | "Thừa số này" không còn từ để chỉ: đoạn 744 là lộ trình chứng minh. Mạch đứt sau khi chuyển chứng minh sang Phụ lục F. | "Thừa số này tăng theo hàm mũ khi độ dài bước hằng." | "Thừa số $\prod_k(1+\beta\eta_k)$ trong (c) tăng theo hàm mũ khi độ dài bước hằng." (+3) |
| nhẹ | §6, dòng 309 (N1) | Sau khi bỏ câu về bước chung, "hai trường hợp" không còn vế thứ nhất trong mục. | "Cận gradient (G) giới hạn phần tăng của khoảng cách ở bước khác biệt. Ghép hai trường hợp, ta được…" | "Ghép trường hợp này với bước chung (Bổ đề 08.4), ta được…" (+6) |
| nhẹ | §4, dòng 218 (N2) | Vế sau thiếu động từ ("cần … tức cả hai sự kiện … cho mọi dãy"). | Nguyên câu dòng 218. | "Ví dụ 08.2 chỉ xét một dãy chỉ số; Định nghĩa 06.9 cần kì vọng theo $\xi$, nên hai sự kiện ở Bước 3 phải được chứng minh cho mọi dãy." (+2) |
| nhẹ | §12, dòng 906 (N3) | Cầu nối không còn gọi tên Bài 09. Bài 06 (dòng 1130) và Bài 07 (dòng 960) đều viết "Câu hỏi cho Bài 0x là: …". | "Khi mỗi quan sát là một chuỗi … được viết lại như thế nào?" | "Câu hỏi cho Bài 09 là: khi mỗi quan sát là một chuỗi … được viết lại như thế nào?" (+6) |
| nhẹ | §9, dòng 690 và 796 (N4) | "Cả ba điều kiện" ở dòng 690 là tính lồi, điều kiện độ dài bước và tính trơn, nhưng Ví dụ 08.10 Bước 3 kiểm tính trơn, tính lồi và (G). Dòng 796 nói "hai ví dụ cuối giữ tính lồi", trong khi Bước 3 của ví dụ cuối là mạng ReLU, không lồi. | 690: "ví dụ cuối cũng xét mạng ReLU, nơi cả ba điều kiện đều không thỏa"; 796: "Hai ví dụ cuối giữ tính lồi và bỏ điều kiện độ dài bước hoặc tính trơn." | 690: "…nơi tính lồi, tính trơn và (G) đều không thỏa" (+1). 796: "Hai ví dụ cuối trở lại hàm lỗi lồi và bỏ điều kiện độ dài bước hoặc tính trơn." (+1) |
| nhẹ | Định lý 08.6, dòng 445 (N5) | Còn hai phép đối "chứ không" trong hai câu liền nhau (`no-ai-slop`: binary contrast; R4 T6). Câu thứ hai chỉ cần nói phạm vi áp dụng. | "…chứ không chặn $\mathbb E\lvert L_D-L_S\rvert$ hay $L_D$. Bảo đảm chỉ thuộc về thuật toán với quy tắc rút chỉ số đã nêu, chứ không thuộc về mọi thuật toán tối ưu." | Giữ câu đầu (đối lập thật, blueprint §E). Câu sau: "Bảo đảm chỉ áp dụng cho Thuật toán 08.1 với quy tắc rút chỉ số đã nêu." (−7) |
| nhẹ | §8, dòng 682 (N6) | Câu đầu nhắc lại Định nghĩa 08.9 ngay trên (`no-ai-slop`: recap). | "Chính quy hóa ngầm là một hành vi của thuật toán." | Cắt; đoạn mở bằng "Học phần có một lập luận cho một trường hợp: …" (−11) |
| nhẹ | Mệnh đề 08.5, Bước 2, dòng 342–347 (N7) | $g'$ ở đây là gradient tại $w'_t$ với $z'$, còn ở dòng 52 và 56 $g'$ là đạo hàm của $g$. | "Đặt $g=\nabla\ell(w_t,z_i)$ và $g'=\nabla\ell(w'_t,z')$." | Đặt $g_t=\nabla\ell(w_t,z_i)$ và $g'_t=\nabla\ell(w'_t,z')$, hợp với quy ước $w'_t$ và với $g_t$ ở Bước 4 Định lý 08.6 (vì $i_t=i$ ở bước khác biệt). (0) |
| nhẹ | Phụ lục D, dòng 1050 (N8) | "khoảng cách" mang hai nghĩa trong cùng một đoạn: khoảng cách tổng quát hóa ($0{,}298$, $0{,}650$, $0{,}651$) và khoảng cách giữa hai lần chạy. | "khoảng cách là $0{,}298$ và $0{,}650$ … Khoảng cách giữa lần chạy thứ nhất và lần chạy thứ ba (không ghép cặp) là $2{,}99$; …" | "$\Delta$ giữa lần chạy thứ nhất và lần chạy thứ ba (không ghép cặp) là …" (phụ lục, −1) |
| nhẹ | Phụ lục F, Bước 1, dòng 1095–1104 (N9) | $\Gamma$ dùng mà chưa gọi tên trong phụ lục; câu "phép chiếu không giãn." đứng sau công thức, không có chủ ý rõ. | "Theo bất đẳng thức tam giác và tính $\beta$-trơn, … ; phép chiếu không giãn." | "Với $\Gamma=\Gamma_{\eta,z}$, theo bất đẳng thức tam giác và tính $\beta$-trơn, … Phép chiếu không giãn, nên $\operatorname{proj}_W\circ\Gamma$ có cùng hệ số giãn." (phụ lục, +10) |
| nhẹ | §4, dòng 187 (N10) | Hai chữ "cho" liền nhau; bất đẳng thức Jensen không có trong mục Giải tích của tiên quyết. | "bất đẳng thức Jensen cho hàm trị tuyệt đối cho $\lvert\mathbb E_\xi a-\mathbb E_\xi b\rvert\le\mathbb E_\xi\lvert a-b\rvert$" | "theo bất đẳng thức Jensen với hàm trị tuyệt đối, $\lvert\mathbb E_\xi a-\mathbb E_\xi b\rvert\le\mathbb E_\xi\lvert a-b\rvert$" (0); thêm "Jensen" vào dòng 44 (+1), hoặc gọi là "bất đẳng thức tam giác cho kì vọng" |

Ghi chú nhỏ, không xếp mức: dòng 198 viết "$w'_{t+1}=w'_t-\tfrac12\cdot$(đạo hàm)", chữ nằm ngoài công thức sau dấu nhân. Có thể viết "$w'_{t+1}=w'_t-\tfrac12\,\partial_w\ell_{\mathrm H}(w'_t,z_{i_t})$", như dòng 129.

## 5. Văn phong các đoạn mới (Detect)

Các đoạn mới ở dòng 3, 23, 25, 109, 176, 187–193, 305, 351, 407, 455, 497, 593, 630, 682, 690, 744, 774, 796, 834, 846, 856 và 906 không có câu hỏi tu từ, không có câu lấy văn bản làm chủ ngữ, không dùng từ thân mật (đã grep "hỏng", "tính tay", "thua", "tệ hơn": 0), và không có câu kết chỉ báo trước mục sau. Còn lại ba mẫu `no-ai-slop`: phép đối ở dòng 193 và 445 (M1, N5) và câu nhắc lại định nghĩa ở dòng 682 (N6). Thuật ngữ mới hay đổi khớp `thuat-ngu.md`: "tiền kích hoạt (pre-activation)", "giai đoạn đầu (burn-in)", "độ dài bước (step size, còn gọi là tốc độ học)", "độ hợp lý (likelihood)", "độ chênh tối ưu" và "ReLU (rectified linear unit)". Kí hiệu $\kappa$, $k$, $g_{uv}$, $g_r$ là kí hiệu cục bộ và được đặt tên tại chỗ.

## 6. Ngân sách chữ (thân bài)

Thêm: M2 +3, N1 +6, N2 +2, N3 +6, N4 +2, N10 +1, tổng +20. Cắt: M1 −3, N5 −7, N6 −11, tổng −21. Thân bài sau sửa khoảng 11 981/12 000. N8, N9 nằm ở phụ lục (2 106/3 000).
