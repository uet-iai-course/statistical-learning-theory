# Rà soát 5 — Mạch và móc nối, ghi chú Bài 06 (bản đóng băng)

Người rà: tác tử rà mạch và móc nối (chỉ đọc). Đối tượng: `scratchpad/lec06-draft-frozen.md`, SHA-256 bắt đầu `1a2fd0319e4b55ac` (trùng `2627-1/materials/lec-06/lecture-note.md` hiện tại, `diff -q` rỗng). Số dòng dưới đây là số dòng của bản đóng băng.

**Tổng kết:** 0 `chặn bàn giao` · 0 `nghiêm trọng` · 4 `trung bình` · 16 `nhẹ`.

Mạch chính đứng vững: mỗi mục §4–§9 mở bằng vấn đề và kết bằng câu dẫn sang mục sau, đúng các câu mở/câu kết của `outline.md` §3; câu hỏi mở đầu được trả lời ngay (dòng 22–24), bằng số ở Ví dụ 06.2, 06.3 và nhắc lại ở §10; mọi số hiệu 01.x–05.x đều tồn tại và đúng tên; bốn lời hứa (Bài 01 dòng 913, Bài 02 dòng 574, Bài 05 dòng 1100, 1254) được giữ. Bốn phát hiện `trung bình` là: một trích dẫn kết quả hàm lỗi bị chặn (Hệ quả 04.17) cho bối cảnh có thể không bị chặn; câu báo trước Bài 08 thiếu điều kiện lồi, trơn; kí hiệu $B$ đổi nghĩa so với §2 và `ky-hieu.md`; §10 không trả lời thẳng câu hỏi trung tâm. Các đề xuất thêm chữ đều có chỗ cắt bù (cuối báo cáo).

## 1. Kết quả `forward_refs.py`

`forward_refs.py` lấy số bài từ đường dẫn (`lec-NN`), nên chạy trên bản sao tại `scratchpad/reviews06/r5/lec-06/lecture-note.md` (byte-giống bản đóng băng), từ gốc repo:

```
python3 ../tools/courses/statistical-learning-theory/scripts/forward_refs.py <scratchpad>/reviews06/r5/lec-06/lecture-note.md
0 forward references
```

Kiểm tay (đọc toàn văn 1–1285): không câu nào trong thân bài dẫn một khối 06.x đứng sau. Các tham chiếu tới trước còn lại là con trỏ mục ("§4", "§7", "bổ đề dưới đây", "ví dụ ở cuối mục", "nhận xét cuối mục"), hợp lệ theo quyết định (i)–(xi) của dàn ý mục 12. Lần dùng sớm của thuật ngữ trong §1 dòng 108 ("quan sát thay thế và quan sát kiểm tra của §7") có con trỏ mục, chấp nhận được nhưng nội dung lệch định nghĩa (phát hiện N3).

## 2. Lần dùng đầu của kí hiệu mới

| Kí hiệu | Dùng lần đầu | Định nghĩa / giới thiệu | Nhận xét |
|---|---|---|---|
| $\bar Y$ | 62 (ôn nhanh 2) | 62 | đúng `ky-hieu.md` |
| $v(w,z)$ | 119 (bảng §2) | 119 | |
| $\psi(w)$ | 197 | 197 (Bổ đề 06.1) | kí hiệu Bài 05, đặt lại |
| $c_t$ | 280–282 | 282 (công thức ở Phụ lục D) | Phụ lục D đổi thành $c_s$ (N12) |
| $\operatorname{opt}_S$ | 44 (tiên quyết), 176 | Định nghĩa 04.2; viết lại 345 | |
| $\tilde w$ | 341 | 341 (Mệnh đề 06.5) | khác $\tilde w_T$ Bài 05, đúng QĐ |
| khoảng cách tổng quát hóa kì vọng | 5 (đoạn dẫn, có tiếng Anh) | 313 (Định nghĩa 06.4) | |
| $F_{s,\lambda}$ | 455 | 455 (Định nghĩa 06.6) | |
| $F_{S,\lambda}$ | 461 | 461 (câu đặt tên) | công thức đầu tiên 560 |
| $\hat w_s$, $\hat w_{s,\lambda}$, $\hat w_S$ | 456 | 456 | tồn tại nhờ Bổ đề 06.8 (con trỏ "bổ đề dưới đây", 461) |
| $S^{(4)}$, $z'$ | 555 | 555 (tại chỗ, Ví dụ 06.4) | trước tên chung ở Định nghĩa 06.9, đúng dàn ý |
| $s^{(i)}$ | 605 | 605 (Định nghĩa 06.9) | |
| $S^{(i)}$, $Z'$ | 624 | 624, 632 | |
| $\epsilon_{\mathrm{stab}}(m)$ | 611 | 611 | |
| (L) | 725 | 727 | |
| $\beta$, $C$ (Nhận xét 06.12) | 881 | 881 (tại chỗ) | |
| $\lambda^*$, $W_B$ | 920 | 920 (Hệ quả 06.13(c)) | $W_B$ chưa có trong `ky-hieu.md` (N16) |
| $\epsilon_{\mathrm{opt}}$ | 1038 | Định nghĩa 01.12 | |
| $\bar z$, $M$ | 848, 858 | tại chỗ | |
| $\lambda_{\mathrm{UML}}$, $\rho$ | 884, 1128 | tại chỗ | |
| $q$ | 1242 | 1242 (Phụ lục D) | |
| $\bar w_T$ | 20 | không đặt tên trong bài (Bài 05) | N4 |
| $g_t$ | 311 | không đặt tên trước 399 (Bài 05) | N4 |
| $B$ | 96, 103 | 118 (bảng §2), nghĩa khác chỗ dùng ở §9 | T3 |
| $R$ | 18 | không có trong bảng §2 (Bài 05) | gộp vào T3 |

## 3. Nhận xét mạch theo từng mục

- **Đoạn dẫn và câu hỏi mở đầu (1–24).** Nối đúng câu hỏi cuối buổi và cầu nối Bài 05 (dòng 1210–1254 của Bài 05: $0{,}0025$, $0{,}9025$, hai câu hỏi). Câu trả lời thẳng ngay sau câu hỏi, dẫn §4, §5, §6–§9. Ổn.
- **Tiên quyết, §1, §2.** Đủ các số hiệu dùng về sau. §1 dùng $B$ trước khi §2 đặt nghĩa, và nghĩa ở §2 ("bán kính của $W$") không khớp cách dùng ở §1 dòng 96 và §9 (T3). Dòng 124 "(C), (G1), (G2) của Bài 05 (§4)" mơ hồ (N5).
- **§3.** Ví dụ 06.1 và khối ứng dụng đặt đúng chỗ. Câu kết 181 "Mỗi ví dụ có hai cách dùng dữ liệu … Cách thứ nhất được xét ở §4" không khớp nội dung: §4 không dùng Ví dụ 06.1 mà dùng phân bố của câu hỏi mở đầu; Ví dụ 06.1 chỉ trở lại ở §6 (N1).
- **§4.** Mở bằng vấn đề (oracle cho $L_D$), Bổ đề 06.1 → Hệ quả 06.2 → Ví dụ 06.2 (nửa đầu câu hỏi mở đầu) → Nhận xét 06.3 (trả lời ý (i) của ứng dụng) → câu kết 307 dẫn sang §5. Ổn.
- **§5.** Mở bằng Hệ quả 05.19 và khoảng trống $L_D$; Định nghĩa 06.4, Mệnh đề 06.5, Ví dụ 06.3 (nửa sau câu hỏi mở đầu); câu kết 445 nêu đúng hai bước tiếp theo (§6 thuật toán, §7 công cụ). Ví dụ 06.3 dùng một mẫu bốn quan sát khác hẳn mẫu bốn quan sát của Ví dụ 06.1 (N2).
- **§6.** Mở bằng Ví dụ 06.1 (nghiệm dịch $0{,}6154$), định nghĩa, hai bổ đề, Ví dụ 06.4, Hình 06.1. Hình 06.1 không được dẫn trong văn bản (N11). Câu 467 nói quá ("mọi lập luận còn lại", N7). Câu kết 593 gọi đại lượng của §7 là "độ nhạy của nghiệm", trong khi §7 đo thay đổi của hàm lỗi (N8).
- **§7.** Mở bằng nhu cầu của Mệnh đề 06.5, Định nghĩa 06.9, Định lý 06.10, đẳng thức (701) được dùng lại ở Nhận xét 06.12 và Phụ lục E đúng như hứa; giữ lời hứa Bài 01 dòng 913 ở dòng 703. Thuật toán hằng xuất hiện hai lần (628 và Ví dụ 06.5) (N15). Câu kết 721 dẫn sang §8. Ổn.
- **§8.** Mở bằng số của Ví dụ 06.4, (L) đặt ngay trước Mệnh đề 06.11; các phản ví dụ 06.7, 06.9 bỏ đúng giả thiết, Ví dụ 06.9 → Bài tập 06.5 → Nhận xét 06.12 nối liền mạch; câu kết 889 dẫn sang §9. Ổn.
- **§9.** Đặt thuật ngữ "đánh đổi khớp–ổn định"; Hệ quả 06.13, Ví dụ 06.10–06.12, hai nhận xét. Ví dụ 06.11 trả lời ý (ii) của ứng dụng; Bước 3 tính hệ số ổn định tại một $\lambda=10^{-3}$ không nối với bước nào (N10). Nhận xét 06.14 dẫn Hệ quả 04.17 cho hàm lỗi có thể không bị chặn (T1). Câu kết 1043 dẫn sang Bài 08.
- **§10.** Trả lời câu hỏi mở đầu bằng số, nhưng không có câu trả lời thẳng cho câu hỏi trung tâm (dòng 5) và câu hỏi thứ hai của cầu nối Bài 05 ("khi nào tối thiểu hóa trên $S$ kiểm soát được $L_D$") (T4). Giới hạn "SGD nhiều vòng" lặp lại câu kết §9 và cầu nối §12. Câu 1051 dẫn Hệ quả 04.17 (T1).
- **§11–§13.** Danh sách bài tập khớp kế hoạch dàn ý mục 4 (tên, mục tiêu). Câu hỏi cuối buổi chỉ dùng khái niệm đã có. Cầu nối Bài 07 khớp blueprint 6.6 và 7.1, không phát biểu kết quả Bài 07; hai câu đầu lặp gần nguyên văn dòng 1060 (N13). Câu báo trước Bài 08 thiếu điều kiện của blueprint 8.1 (T2). Tài liệu đọc khớp dàn ý mục 7.

## 4. Móc nối với Bài 01–05 (đã `grep`)

Ba mươi số hiệu dẫn đều tồn tại với đúng tên khối: Định nghĩa 01.4, 01.8, 01.10, 01.12, 01.14, 01.24; Mệnh đề 01.7, 01.15(b); Ví dụ 01.8; Hệ quả 01.29; Bổ đề 02.2; Nhận xét 02.11; Định nghĩa 02.13; Định nghĩa 04.1, 04.2; Mệnh đề 04.3; Hệ quả 04.17; Định nghĩa 05.1, 05.2, 05.4, 05.6, 05.10, 05.18; Mệnh đề 05.3, 05.5(a), 05.5(b); Thuật toán 05.11; Định lý 05.14; Hệ quả 05.15(a)–(c), 05.19; Ví dụ 05.9. Nội dung khớp: (T1)/(T2) ở Bài 01 dòng 82–83; (O1)/(O2) đoạn sau Định nghĩa 01.12; (C) đoạn trước Định lý 05.14; cận $2(BC_x+C_y)C_x$ đoạn sau Định nghĩa 05.4; "$\bar w_T$ dùng $T-1$ lần rút" đoạn sau Thuật toán 05.11; Bước 1 của Mệnh đề 04.3 là thêm bớt; $G=1$ và gradient logistic ở Ví dụ 05.9; $10^4$ bước cho $0{,}05$ ở Ví dụ 05.9; mẫu bóng $S'$ ở Bài 03. Ngoại lệ duy nhất về điều kiện áp dụng: Hệ quả 04.17 cần (T3) (hàm lỗi trong $[0,1]$, Bài 02 dòng 413), xem T1.

Lời hứa: Bài 01 dòng 913 ("tính chất của một thuật toán cụ thể (Bài 06, 08)") → dòng 703. Bài 02 dòng 574 → Nhận xét 06.12 (hàm lỗi bình phương, dữ liệu bị chặn) và Ví dụ 06.11 (hàm lỗi log của mô hình logistic tuyến tính); tình huống "nhãn hiếm có giá trị rất lớn" bị loại bởi $\lvert y\rvert\le C_y$ chứ không được xử lý, chưa nói ra (N14). Bài 05 dòng 377 ($\tfrac\lambda2\lVert w\rVert^2$ là $\lambda$-lồi mạnh) → Bổ đề 06.8(a). Bài 05 dòng 1100 → §8–§9. Bài 05 dòng 1254 → câu hỏi mở đầu, §4–§5, §7–§9.

Thuật ngữ, kí hiệu: khớp `ky-hieu.md` dòng 67–74 ($\epsilon_{\mathrm{stab}}$, $S^{(i)}$, $Z'$, $F_{S,\lambda}$, $\hat w_S$, $\lambda^*$, $\tilde w$, (L), $\bar Y$, $c_t$, $q$) và `thuat-ngu.md` §9 dòng 303–341, trừ $B$ (T3), $c_s$ (N12), chỉ số $\mathbb E_S$ (N9), tiếng Anh ở lần đầu (N6).

## 5. Tham chiếu nội bộ

Mọi "§k" trỏ đúng mục và đúng nội dung (dòng 22, 24, 94, 104, 108, 112, 122, 124, 178, 181, 304, 333, 445, 586, 593, 630, 701, 721, 889, 893, 1076, 1117, 1122), trừ dòng 124 "(§4)" mơ hồ (N5). "Phụ lục A–E" trỏ đúng (282, 442, 507, 528, 540, 626, 731, 770, 884, 895, 944, 1127). Ví dụ 06.k, Bài tập 06.k đúng chỗ và đúng nội dung (ví dụ: 824 → Ví dụ 06.4 Bước 3; 834, 860 → công thức một chiều ở 574; 872, 1206 → Bài tập 06.5; 1032 → Bài tập 06.7; 1049 → Bài tập 06.8). "Bước k của chứng minh …" đúng (304, 372, 836, 870, 1216). Phụ lục A dẫn "§4 của Bài 05" cho dưới vi phân khác rỗng: đúng mục, nhưng nên dẫn thẳng Mệnh đề 05.3(a) (N17 gộp vào N5).

## 6. Bảng phát hiện

Mã: T = trung bình, N = nhẹ. Đề xuất câu chữ đã kiểm theo `no-ai-slop` chế độ Detect (không thêm câu bình luận, không câu kết kiểu châm ngôn, giữ câu thẳng).

| Mã | mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|---|
| T1 | trung bình | §9 Nhận xét 06.14, dòng 1032; §10 dòng 1051 | Dẫn Hệ quả 04.17 (cần (T3): hàm lỗi trong $[0,1]$) cho bối cảnh có hàm lỗi không bị chặn (hồi quy logistic trên $W=\mathbb R^p$), trái chuẩn "không chuyển kết quả hàm lỗi bị chặn sang hàm lỗi bình phương, log khi chưa có lập luận mới" và trái câu 122 "Không kết quả nào của bài giả sử hàm lỗi bị chặn". | Bài 04 dòng 920–927: "**Hàm lỗi.** $\ell$ thỏa (T2) và (T3)"; Bài 02 dòng 413: "(T3) … $0\le\ell(h,z)\le1$". Dòng 1051: "Khi $B$ chưa biết, $\lambda$ được chọn bằng mẫu xác thực (Hệ quả 04.17)." | Dòng 1051: "Khi $B$ chưa biết và hàm lỗi bị chặn, $\lambda$ được chọn bằng mẫu xác thực (Hệ quả 04.17, sau khi chia hàm lỗi cho cận của nó)." Dòng 1032: thêm "với hàm lỗi bị chặn, như hồi quy ridge trên quả cầu đơn vị ($\ell\le4$)". Khoảng +20 tiếng, bù ở mục 7. |
| T2 | trung bình | §12 dòng 1117 (câu cuối); cũng 626, 1043, 1283 | Câu báo trước Bài 08 hứa chặn khoảng cách tổng quát hóa kì vọng của "SGD nhiều vòng" không kèm điều kiện; blueprint 8.1–8.2 chỉ làm trong thiết lập lồi, trơn, Lipschitz. Học viên có thể hiểu Bài 08 phủ cả mạng nơ-ron (tên Bài 08 có "deep learning"), mâu thuẫn với câu ngay trước về mạng nơ-ron. | Dòng 1117: "Khoảng cách tổng quát hóa kì vọng của SGD nhiều vòng (§5) được chặn ở Bài 08 bằng tính ổn định của hai lần chạy ghép cặp." Blueprint 8.1: "derive a coupled-run stability estimate in a smooth convex setting"; 8.2: "convex, differentiable, $\beta$-smooth, $G$-Lipschitz per-example losses". | "Với hàm lỗi lồi, trơn và Lipschitz, khoảng cách tổng quát hóa kì vọng của SGD nhiều vòng (§5) được chặn ở Bài 08 bằng tính ổn định của hai lần chạy ghép cặp." (+6 tiếng). Dòng 1043 tương tự: "(Bài 08, cho hàm lỗi lồi và trơn)". |
| T3 | trung bình | §1 dòng 96, 103; §2 dòng 118; §9 Hệ quả 06.13(c) dòng 920; Ví dụ 06.11 | Kí hiệu $B$ được dùng ở §1 trước khi §2 đặt nghĩa, và §2 (cùng `ky-hieu.md` dòng 51) đặt nghĩa "bán kính của $W$ khi $W$ là quả cầu tâm $0$", trong khi §1 dòng 96 và §9 dùng $B$ làm cận chuẩn của điểm so sánh với $W$ bất kì (Ví dụ 06.11: $W=\mathbb R^p$, $B=5$). Một kí hiệu, hai nghĩa. $R$ (dòng 18, 103) không có trong bảng §2. | Dòng 118: "$B$ … bán kính của $W$ khi $W$ là quả cầu tâm $0$"; dòng 920: "Cho $B>0$ với $W_B=\{u\in W:\lVert u\rVert\le B\}$ khác rỗng"; dòng 985–987: $W=\mathbb R^p$, "Với $B=5$". | Sửa dòng bảng §2: "$B$; $R$ \| cận chuẩn của điểm so sánh (bằng bán kính của $W$ khi $W$ là quả cầu tâm $0$); cận $\lVert w_1-u\rVert$ (Bài 05)". Điều phối viên cập nhật `ky-hieu.md` dòng 51 và thêm $W_B$ (N16). Không đổi số tiếng đáng kể. |
| T4 | trung bình | §10 dòng 1047 | §10 không có câu trả lời thẳng cho câu hỏi trung tâm (dòng 5: "khi nào một thuật toán tối ưu cũng là một thuật toán học") và câu hỏi thứ hai của cầu nối Bài 05 ("khi nào tối thiểu hóa trên $S$ cũng kiểm soát được $L_D$"). Câu mở của §10 là câu siêu ngôn ngữ (no-ai-slop: interpretive metadiscourse). | Dòng 1047: "Câu hỏi mở đầu có câu trả lời bằng số." Bài 05 dòng 1254: "khi nào tối thiểu hóa trên $S$ cũng kiểm soát được $L_D$?" | Thay câu đầu dòng 1047 bằng: "Một bộ giải tối ưu là một thuật toán học khi gradient ngẫu nhiên không chệch cho $L_D$, tức mỗi bước dùng một quan sát mới (Hệ quả 06.2), hoặc khi thuật toán ổn định đều, như ERM có chính quy hóa với hàm lỗi lồi, Lipschitz (Định lý 06.10, Mệnh đề 06.11)." (+40 tiếng, bù ở mục 7). |
| N1 | nhẹ | §3 dòng 181 | Câu kết §3 nói "mỗi ví dụ" có hai cách dùng dữ liệu và §4 xét cách thứ nhất, nhưng §4 không dùng Ví dụ 06.1; hai cách dùng dữ liệu thực ra áp dụng cho khối ứng dụng và cho phân bố của câu hỏi mở đầu. | "Mỗi ví dụ có hai cách dùng dữ liệu: dùng mỗi quan sát một lần, hoặc lưu mẫu và dùng lại. Cách thứ nhất được xét ở §4." | "Dữ liệu của ứng dụng và của câu hỏi mở đầu được dùng theo hai cách: mỗi quan sát một lần, hoặc lưu mẫu và dùng lại. Cách thứ nhất được xét ở §4; mẫu của Ví dụ 06.1 trở lại ở §6." (+8 tiếng). |
| N2 | nhẹ | §5 Ví dụ 06.3 dòng 397 | Hai "mẫu bốn quan sát" khác nhau (Ví dụ 06.1: $x$ thay đổi, cố định; Ví dụ 06.3: $X=1$, $Y_i=\pm1$, ngẫu nhiên), trong khi tiêu đề Ví dụ 06.1 và 06.4 dùng chính cụm "mẫu bốn quan sát"; §10 dòng 1047 viết "dùng lại bốn quan sát". Dễ lẫn. | Dòng 397: "Mẫu $S=((1,Y_1),\ldots,(1,Y_4))\sim D^4$ là ngẫu nhiên"; tiêu đề Ví dụ 06.4: "Hồi quy ridge trên mẫu bốn quan sát". | Thêm vào dòng 397: "khác mẫu cố định của Ví dụ 06.1" (+6 tiếng). |
| N3 | nhẹ | §1 dòng 108 | "Quan sát kiểm tra" được mô tả như biến ngẫu nhiên độc lập, nhưng Định nghĩa 06.9 (610) đặt nó là "một điểm $z\in\mathcal Z$ bất kì" (tất định), và chứng minh Định lý 06.10 dùng $Z'$, $Z_i$ chứ không có quan sát kiểm tra ngẫu nhiên riêng. | "Quan sát thay thế và quan sát kiểm tra của §7 độc lập với mọi đại lượng khác." | "Quan sát thay thế $Z'$ của §7 chỉ xuất hiện trong chứng minh và độc lập với mọi đại lượng khác." (bớt 1–2 tiếng). |
| N4 | nhẹ | dòng 20; dòng 311 | $\bar w_T$ (câu hỏi mở đầu) và $g_t$ (câu mở §5) là kí hiệu Bài 05, dùng không gọi tên; $g_t$ chỉ được viết ra ở dòng 399. | Dòng 20: "$\mathbb EL_D(\bar w_T)-\min_WL_D$"; dòng 311: "kì vọng có điều kiện của $g_t$". | Dòng 20: "… chặn $\mathbb EL_D(\bar w_T)-\min_WL_D$, với $\bar w_T$ là điểm lặp trung bình, …" (+6); dòng 311: "của gradient ngẫu nhiên $g_t$" (+3). |
| N5 | nhẹ | §2 dòng 124; Phụ lục A dòng 1141 | "(C), (G1), (G2) của Bài 05 (§4)" không rõ §4 của Bài 05 hay của ghi chú (ý định là §4 của ghi chú). "Mức (O1) của Bài 01" được áp cho $F_{S,\lambda}$ mà không nói (Nhận xét 06.15 có nói "cho $F_{S,\lambda}$"). Phụ lục A dẫn "§4 của Bài 05" thay cho số khối. | Dòng 124: "Giả thiết tối ưu là (C), (G1), (G2) của Bài 05 (§4), …"; "tức mức (O1) của Bài 01"; dòng 1141: "(§4 của Bài 05)". | "(C), (G1), (G2) của Bài 05, dùng ở §4"; "tức mức (O1) của Bài 01 cho $F_{S,\lambda}$"; dòng 1141: "(Mệnh đề 05.3(a))". |
| N6 | nhẹ | dòng 32/122 ("lập luận đổi vai"), 469 ("tăng trưởng bậc hai"), 628/705 ("thuật toán hằng"), 895 ("bất đẳng thức oracle") | Thuật ngữ điều phối viên chốt ở `thuat-ngu.md` §9 (dòng 333–336) và "bất đẳng thức oracle" (dòng 249, "ghi chú giải thích một câu ở lần đầu") xuất hiện không kèm tiếng Anh ở lần đầu trong thân bài. | Tiêu đề Bổ đề 06.7, Hệ quả 06.13; dòng 122 "§7 (lập luận đổi vai)". | Thêm "(quadratic growth)", "(exchange argument)", "(constant algorithm)", "(oracle inequality)" ở lần đầu trong thân bài (+8 tiếng). |
| N7 | nhẹ | §6 dòng 467 | Nói quá: "Mọi lập luận còn lại của bài" dùng tính lồi mạnh, nhưng Định lý 06.10 và §7 không dùng. | "Mọi lập luận còn lại của bài dùng hai tính chất của $F_{s,\lambda}$" | "Các lập luận về ERM có chính quy hóa ở §8–§9 dùng hai tính chất của $F_{s,\lambda}$" (+2). |
| N8 | nhẹ | §6 dòng 593 | Câu kết §6 gọi đại lượng được định nghĩa ở §7 là "độ nhạy của nghiệm"; §7 đo thay đổi của hàm lỗi tại mọi quan sát kiểm tra, §8 mới nối khoảng cách nghiệm với hàm lỗi. | "Đại lượng cần đo là độ nhạy của nghiệm khi thay một quan sát. Định nghĩa của nó và cận cho khoảng cách tổng quát hóa kì vọng nằm ở §7." | "Ở §7, độ nhạy khi thay một quan sát được đo bằng thay đổi của hàm lỗi tại mọi quan sát kiểm tra, và đại lượng này chặn khoảng cách tổng quát hóa kì vọng." (≈ cùng độ dài). |
| N9 | nhẹ | dòng 947, 994 | `thuat-ngu.md` dòng 23: "Ở Bài 06, 08 viết $\mathbb E_S[L_D(A(S))]$ … luôn ghi chỉ số $\mathbb E_S$". Phát biểu Hệ quả 06.13 ghi $\mathbb E_S$, nhưng chứng minh và Ví dụ 06.11 bỏ chỉ số. | Dòng 994: "tức $\mathbb EL_D(\hat w_S)-\min_{\lVert u\rVert\le5}L_D(u)\le0{,}01$". | Ghi $\mathbb E_S$ ở 947, 994 (0 tiếng). |
| N10 | nhẹ | §9 Ví dụ 06.11 Bước 3, dòng 996–999 | Bước 3 tính hệ số ổn định tại $\lambda=10^{-3}$, một giá trị không được dùng ở bước nào khác; mạch của ví dụ (chọn $\lambda^*$, so với SGD) bị đứt. Tính tại $\lambda^*$ cho thấy luôn hai số hạng bằng nhau, nối với Phụ lục C Bước 4. | "**Bước 3: hệ số ổn định với một $\lambda$ khác.** Với $\lambda=10^{-3}$, … $=0{,}002$." | "**Bước 3: hệ số ổn định tại $\lambda^*$.** Mệnh đề 06.11 cho $\epsilon_{\mathrm{stab}}=2/(4\cdot10^{-4}\cdot10^6)=0{,}005$, đúng một nửa cận $0{,}01$." (≈ cùng độ dài; điều phối viên kiểm số: $2/400=0{,}005$). |
| N11 | nhẹ | §6 Ví dụ 06.4 Bước 4, dòng 584 | Hình 06.1 không được dẫn ở đâu trong văn bản; người đọc gặp hình mà không biết nó minh họa bước nào. | Chỉ có chú thích dòng 591 chứa "Hình 06.1". | Cuối dòng 584 thêm "(Hình 06.1)" (+2). |
| N12 | nhẹ | Phụ lục D dòng 1243–1263 | Phụ lục D đổi $c_t$ của thân bài (dòng 282, `ky-hieu.md` dòng 74) thành $c_s$ và dùng $s$ làm chỉ số cộng, trùng $s$ (mẫu tất định) của Định nghĩa 06.6, 06.9. | Dòng 1248: "$\bar w_T=\sum_{s=1}^{T-1}c_sy_s,\qquad c_s=\frac{1-q^{\,T-s}}{T}$". | Giữ $c_t$, $y_t$ như thân bài; dùng $k$ cho chỉ số trung bình: $w_k=2\eta\sum_{t<k}q^{k-1-t}y_t$ (phụ lục, ngoài trần thân bài). |
| N13 | nhẹ | §12 dòng 1117 (hai câu đầu) | Hai câu đầu cầu nối lặp gần nguyên văn dòng 1060 của §10; "Bổ đề 06.7 … không áp dụng" không chính xác (Bổ đề 06.7 nói về một hàm lồi mạnh bất kì; thứ mất đi là Bổ đề 06.8(a)); "khoảng cách tổng quát hóa bằng chính $L_D$" khi $L_S\approx0$ phải là "xấp xỉ". | Dòng 1060: "hàm lỗi của mạng nơ-ron theo trọng số không lồi, nên các cận không chuyển sang mạng nơ-ron"; dòng 1117: "Hàm lỗi của một mạng nơ-ron theo trọng số không lồi, nên Bổ đề 06.7 và Mệnh đề 06.11 không áp dụng. … khoảng cách tổng quát hóa bằng chính $L_D$". | Thay hai câu đầu bằng: "Mệnh đề 06.11 cần hàm lỗi lồi theo tham số, và hàm lỗi của mạng nơ-ron theo trọng số nói chung không lồi (§10)." Đổi "bằng chính $L_D$" thành "xấp xỉ $L_D$". (−13 tiếng). |
| N14 | nhẹ | §8 Ví dụ 06.9 Kết luận dòng 872 hoặc Nhận xét 06.12 dòng 886 | Lời hứa Bài 02 dòng 574 nêu "hàm lỗi bình phương với một nhãn hiếm có giá trị rất lớn"; ghi chú loại tình huống này bằng giả thiết $\lvert y\rvert\le C_y$ mà không nói ra, nên người đọc Bài 02 không thấy lời hứa được xử lý thế nào. | Bài 02 dòng 574; Bài 06 dòng 886: "dữ liệu bị chặn và tính trơn thay cho hàm lỗi bị chặn". | Tùy chọn, thêm vào dòng 886: "Giả thiết $\lvert y\rvert\le C_y$ loại nhãn hiếm có giá trị rất lớn của Nhận xét 02.11." (+15; chỉ làm nếu còn ngân sách, Nhận xét 06.12 là khối đọc thêm). |
| N15 | nhẹ | §7 dòng 628 và Ví dụ 06.5 Bước 1 | Thuật toán hằng được giới thiệu hai lần với cùng kết luận $\epsilon_{\mathrm{stab}}=0$. | Dòng 628: "Hai ví dụ. Thuật toán hằng $A(s)=w_0$ có $\epsilon_{\mathrm{stab}}(m)=0$."; dòng 708: "nên $\epsilon_{\mathrm{stab}}(m)=0$". | Bỏ câu đầu dòng 628 và đổi "Thuật toán ghi nhớ …" thành câu mở đoạn (−9 tiếng). |
| N16 | nhẹ | `ky-hieu.md` (planning, việc của điều phối viên) | $W_B$ (dòng 920) chưa có trong `ky-hieu.md`; dòng 51 của `ky-hieu.md` giữ nghĩa cũ của $B$ (xem T3). | `outline.md` §13 mục 14 đã đề xuất. | Thêm dòng "$W_B$ \| $\{u\in W:\lVert u\rVert\le B\}$ \| Bài 06, cục bộ" và sửa nghĩa $B$. |

## 7. Ngân sách tiếng (thân bài 11 979 / 12 000, đếm `wc -w` dòng 1–1131)

Thêm (ước tính): T4 +40, T1 +20, T2 +6, N1 +8, N2 +6, N4 +9, N6 +8, N7 +2, N11 +2 → khoảng +101.

Cắt đề xuất:

1. N13: hai câu đầu cầu nối §12 thay bằng một câu (−13).
2. N15: câu "Hai ví dụ. Thuật toán hằng …" ở dòng 628 (−9).
3. §10 dòng 1058, mục giới hạn **SGD nhiều vòng** (lặp câu kết §9 dòng 1043 và cầu nối §12): bỏ mục, đổi "Bốn giới hạn còn lại." thành "Ba giới hạn còn lại." (−20).
4. §6 dòng 461, câu "Kí hiệu $F_{S,\lambda}$ dành cho mục tiêu có chính quy hóa; $L_S$ giữ tên rủi ro thực nghiệm." chuyển thành ba tiếng trong Định nghĩa 06.6 dòng 456 ("với mẫu ngẫu nhiên, $F_{S,\lambda}$ và $\hat w_S$") (−12).
5. §10 dòng 1049, câu "Định lý 06.10 và Mệnh đề 06.11 không dùng chiều VC hay hội tụ đều" trùng nhận xét sau Định lý 06.10 (dòng 650); giữ vế về Bài tập 06.8 (−12).
6. Ví dụ 06.9 Kết luận dòng 872, vế "UML §12.2.2 có một ví dụ cho thấy khi $x$ không bị chặn thì không thuật toán nào học được bài toán này" chuyển xuống §13 (mục Mở rộng đã dẫn §12.2.2) (−22 trong thân bài; §13 nằm trong thân bài nhưng đã có cụm "ví dụ dữ liệu không bị chặn", nên không cần thêm).
7. Nếu vẫn thiếu: N1, N2, N6 là các đề xuất có thể bỏ trước (cộng 22).

Tổng cắt 1–6: khoảng −88. Ưu tiên: làm T1–T4 (+66) với cắt 1–4 (−54) và 5 hoặc 6; các đề xuất nhẹ còn lại làm khi còn chỗ.
