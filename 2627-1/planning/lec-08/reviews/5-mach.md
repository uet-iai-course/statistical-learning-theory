# Rà soát 5 — Mạch và móc nối, Bài 08 (bản đóng băng `lec08-draft-frozen.md`)

Người rà: tác tử rà 5 (chỉ đọc repo). Bản sao: `reviews08/r5/lec-08/lecture-note.md`. Số dòng dưới đây là số dòng của bản đóng băng (1 084 dòng). `no-ai-slop` dùng ở chế độ Detect cho mọi đề xuất câu chữ. Không dùng `quill` (không cần; không tạo `quill.json`).

## Tổng kết theo mức

| Mức | Số | Tóm tắt |
|---|---|---|
| chặn bàn giao | 0 | |
| nghiêm trọng | 0 | |
| trung bình | 3 | "tính đồng bức" dùng trước Định nghĩa 08.3 (dòng 111); Phụ lục D của Bài 07 bị gọi là "chứng minh" và mất điều kiện độ dài bước (dòng 691); thứ tự §9: Mệnh đề 08.12 bị tách khỏi nhóm không lồi, không có câu chuyển trước Ví dụ 08.9, câu mở §9 không khớp Bước 3 của Ví dụ 08.10 |
| nhẹ | 15 | tiên quyết thừa Ví dụ 06.9, thiếu bất đẳng thức trung bình cộng–trung bình nhân; $\beta$, $G$ ở bảng §1 trước §2; $c$ và $s$ hai nghĩa; (T2) phát biểu lại khác Bài 01/06; dẫn sai nguồn số ở §10; cầu nối nói "mỗi quan sát là một cặp $(x,y)$", thiếu tiếng Anh cho "độ hợp lý"; "tiền kích hoạt" chưa có tiếng Anh; Bài tập 07.5(c) là hàm mục tiêu bình phương; "sai số tối ưu" rút gọn; §10 kết bằng danh sách; ba chỗ lặp |

Mạch tổng thể tốt: câu hỏi mở đầu được trả lời ngay (dòng 23) và khép ở §10 (dòng 870); khối ứng dụng được trả lời ở Ví dụ 08.7; ví dụ Huber, hồi quy logistic và thí nghiệm nhất quán về số và kí hiệu; mọi số hiệu 01.x–07.x đúng tên khối; bốn lời hứa của Bài 06 và câu hỏi cuối Bài 07 được giữ; cầu nối sang Bài 09 khớp blueprint 8.6 và không phát biểu kết quả của Bài 09.

## 1. Kết quả `forward_refs.py`

```
$ python3 /data/tqlong/lectures/tools/courses/statistical-learning-theory/scripts/forward_refs.py reviews08/r5/lec-08/lecture-note.md
0 forward references            (exit 0)
```

Kiểm tay toàn bộ tham chiếu nội bộ (grep mọi "§k", "Phụ lục X", "Ví dụ 08.k", "Bài tập 08.k", khối 08.k): không câu thân bài nào dẫn một khối có số đứng sau. "§k" và "Phụ lục X" đều trỏ đúng chỗ: §2 (dòng 74), §9 (74, 113, 303), §4 (75, 115, 144), §7–§8 (75, 105, 173), §8 (76, 77, 150), §3 (94, 659), Phụ lục A (111, 242, 266), §7 (11, 193), §4–§7 (23, 90), Phụ lục B (368 → B(i), 484 → B(ii)), Phụ lục C (847), Phụ lục D (25, 513), §10 (693). Ví dụ 08.3 Bước 2 → Ví dụ 08.1; Ví dụ 08.9 kết luận → Ví dụ 08.3 ($\lvert1-\eta\beta\rvert=2$ khớp bảng); câu hỏi cuối buổi (d) → Ví dụ 08.10 Bước 2, 3 (đúng). "Bài tập 08.7" (dòng 578) và "Bài tập 08.3" (Phụ lục A, Bước 2) trỏ sang tệp bài tập, tên khớp danh sách §11 (cùng cách Bài 06–07).

## 2. Bảng lần dùng đầu (thuật ngữ, kí hiệu mới)

| Mục | Lần dùng đầu (dòng) | Định nghĩa / giới thiệu nghĩa (dòng) | Kết luận |
|---|---|---|---|
| $w'_t$ | 88 (bảng §1: "điểm lặp $w'_t$ của lần chạy thứ hai") | 185 (Định nghĩa 08.2) | đạt; nghĩa có ở bảng, câu dòng 90 nói lần chạy thứ hai là công cụ chứng minh |
| $\Delta_t$ | 115 (nêu nghĩa, trỏ §4, phân biệt với Bài 05) | 187 | đạt |
| (S), (G), điều kiện độ dài bước | 107–109 | 107–109 | đạt |
| $\beta$, $G$ | 84 (bảng §1, chưa nêu nghĩa) | 102, 107–108 | nhẹ (P5) |
| $\xi$, $i_t$ | 86 | 86, 100 | đạt |
| bước chung, bước khác biệt, ngân sách độ dài bước | 186, 188 | 186, 188 | đạt ("tổng các độ dài bước" ở dòng 23 bằng lời) |
| hệ số giãn, ánh xạ không giãn | 5 (tên, tiếng Anh), 227–228 | 227–228 | đạt |
| tính đồng bức | 5 (tên), **111 (dùng trong lập luận)** | 229 | **trung bình (P1)** |
| $\Gamma_{\eta,z}$, ánh xạ bước gradient | 238 | 238 | đạt |
| $\ell_{\mathrm H}$, hàm lỗi Huber | 120–123 | 120–123 | đạt |
| xáo trộn lại sau mỗi vòng | 368 | 368 (in nghiêng, tiếng Anh; thuật ngữ Bài 05) | đạt |
| tỉ lệ đổi nhãn dự đoán | 534 | 534 | đạt |
| $\eta^*$ | 607 | 607 | đạt |
| $T^*$ | 676 (công thức) | 676, tên bằng lời 678 | đạt |
| dừng sớm, chính quy hóa tường minh, chính quy hóa ngầm | 686–688 | 686–688 | đạt; không dùng trước (grep) |
| điểm dừng | 706 | 706 (tiếng Anh) | đạt |
| giai đoạn đầu (burn-in) | 806 | 806 | đạt |
| tiền kích hoạt | 838 | không có tiếng Anh, không có ở `thuat-ngu.md` và Bài 07 | nhẹ (P10) |
| lớp ẩn, lớp ra; $\theta$, $\Theta_1$, $\Theta_2$; $\chi(x)$ | 836–842 | Bài 07 (Định nghĩa 07.1, Ví dụ 07.3); $\chi$ tại chỗ | đạt |
| $F_*$, $\sigma^2$, $\tau$, $\mathcal F_{t-1}$ | 850–861 | tại chỗ; $\mathcal F_{t-1}$ của Định nghĩa 05.10 | đạt |
| điểm dừng xấp xỉ, tính dừng | 861 | 861 | đạt |
| cận trên bậc hai (còn gọi là bổ đề hạ) | 959 | 959 | đạt (dạng "X, còn gọi là Y") |
| $c$ | 225 (hệ số giãn) | 781 lại là hằng số của $\eta_t=c/t$ | nhẹ (P6) |
| $d$, $a$, $b$, $g_t$, $q_u$, $v^+$ | trong chứng minh | tại chỗ | đạt (cục bộ) |
| độ hợp lý | 938 (cầu nối, được miễn định nghĩa) | không có tiếng Anh | nhẹ (P9) |

## 3. Mạch từng mục

- **Đoạn dẫn và câu hỏi mở đầu.** Đoạn 1 nhìn lại Định lý 06.10, Mệnh đề 06.11, §10 Bài 06 và câu hỏi cuối Bài 07; đoạn 2 nêu câu hỏi trung tâm. Câu hỏi mở đầu được trả lời ngay ở dòng 23 và khép lại ở §10 (dòng 870). Câu cuối Bài 07 có cụm "qua số bước và độ dài bước"; dòng 3 bỏ cụm này, trong khi chính đại lượng đó là câu trả lời (P15). Dòng 25 lặp số lỗi phân lớp của dòng 693 (P14).
- **§1–§2.** Mở bằng bảy thành phần, kết bằng câu văn xuôi (dòng 90, 115). Bảng §1 dùng $\beta$, $G$ trước khi §2 nêu nghĩa (P5). Dòng 111 dùng "tính đồng bức" trước định nghĩa (P1). Dòng 105 viết lại (T2) với điều kiện $L_D(w_1)<\infty$, khác cách Bài 01 và Bài 06 dùng nhãn (T2) (P7).
- **§3.** Mục mở thẳng bằng khối Ví dụ 08.1, không có câu dẫn (Bài 06–07 cũng vậy; chấp nhận được). Khối ứng dụng đặt câu hỏi, trỏ §8; câu kết dòng 153 nêu vấn đề cho §4. Đạt.
- **§4.** Mở bằng vấn đề (hai kì vọng của Định nghĩa 06.9), kết bằng câu nêu hai sự kiện cần chứng minh (dòng 218), sau đó §5 và §6 lần lượt chứng minh hai sự kiện này. Đạt. Ví dụ 08.2 nhất quán với Ví dụ 08.1 (đã tính lại $w'_t$: $0,-\tfrac12,0,\tfrac12,0,0$).
- **§5.** Mở bằng vấn đề (bước chung), kết dòng 306 chuyển sang bước khác biệt. Đạt.
- **§6.** Câu đầu dòng 310 lặp ý của dòng 218 và dòng 283 (P14); phần còn lại của câu mở đúng vấn đề. Kết dòng 401 bằng một con số. Đạt.
- **§7.** Mở bằng cách ghép (G) với Mệnh đề 08.5, kết dòng 580 chuyển sang sai số tối ưu. Ví dụ 08.6 trả lời thí nghiệm mở đầu. Câu "đo tính ngẫu nhiên của thuật toán, không đo độ nhạy theo mẫu" xuất hiện hai lần (dòng 193 và 538) (P14). Lời hứa Bài 06 (Ví dụ 06.3, $\eta=0{,}00625$, $T=1600$, khoảng cách $0{,}4750$) khớp Bài 06 dòng 389–434.
- **§8.** Mở bằng Mệnh đề 06.5(b), trả lời khối ứng dụng ở Ví dụ 08.7, không dùng "dừng sớm" trước Định nghĩa 08.9. Kết dòng 695 bằng văn xuôi. Dòng 691 mô tả sai mức độ của Phụ lục D Bài 07 (P2). Dòng 693 dẫn giá trị $0{,}603$ ở $10$ vòng, chỉ có ở Phụ lục D (P12).
- **§9.** Câu mở (dòng 699) hứa "mỗi ví dụ dưới đây bỏ một trong ba điều kiện". Thứ tự thực tế: Ví dụ 08.8 (bỏ tính lồi) → Mệnh đề 08.10, Nhận xét 08.11 (không lồi) → Ví dụ 08.9 (bỏ $\eta\le2/\beta$, không có câu chuyển sau Nhận xét 08.11) → Ví dụ 08.10 (bỏ tính trơn; Bước 3 bỏ cả ba) → quay lại không lồi với Mệnh đề 08.12 (dòng 845). Mạch đi vòng (P3). Câu kết dòng 866 tốt.
- **§10.** Dòng 870 trả lời câu hỏi trung tâm; dòng 872 nối với Bài 07 (cấp lớp và cấp thuật toán). Mục kết bằng danh sách năm giới hạn, không có câu văn xuôi (P13). Dòng 870 dẫn "(Ví dụ 08.6)" cho các số $0{,}045$ và $0{,}919$, vốn ở bảng câu hỏi mở đầu (P8).
- **§11–§13.** Danh sách bài tập khớp dàn ý. Câu hỏi cuối buổi dùng Ví dụ 08.5, 08.10 đúng chỗ. Cầu nối khớp blueprint 8.6 ("same risk language … sequence … log-likelihood"), không khẳng định gì về Bài 09; hai chỗ chữ ở P9.

## 4. Móc nối với Bài 01–07 (đã grep)

Mọi số hiệu đúng tên khối và nội dung: Định nghĩa 01.10, 01.24; Nhận xét 02.11 (đoạn sau nhắc hàm lỗi log, Bài 02 dòng 574); Định nghĩa 04.2; §8 Bài 04 (mẫu xác thực); Định nghĩa 05.4 (đoạn sau có $2(BC_x+C_y)C_x$), Mệnh đề 05.5(a) với $U$, Định nghĩa 05.6, 05.7, Bổ đề 05.8 (đoạn sau, dòng 440: không giãn), Ví dụ 05.9 ($m=10^6$, $\eta=0{,}05$, $T=10^4$), Định nghĩa 05.10 (đẳng thức sau nó; rút độc lập), Thuật toán 05.11, Ví dụ 05.12 (điểm lặp cuối dao động), Định lý 05.14 (cận $\lVert w_1-u\rVert^2/(2\eta T)+\eta G^2/2$; (C)), Định nghĩa 05.18 ($\xi$ có thể là dãy; đo được theo bộ ba), Hệ quả 05.19 (Bước 1: (G1), (G2)), Phụ lục B Bài 05 Bước 1 (đo được); Hệ quả 06.2, Nhận xét 06.3 ($RG/\sqrt{m+1}$; từ vòng hai Hệ quả 06.2 hỏng), Ví dụ 06.3, Định nghĩa 06.4, Mệnh đề 06.5(b), Định nghĩa 06.6, 06.9, Định lý 06.10 (bốn giả thiết khớp Bước 5 chứng minh Định lý 08.6), Mệnh đề 06.11 ($2G^2/(\lambda m)$) và (L); Định nghĩa 07.1, Ví dụ 07.3 ($\chi(x)$, lớp ẩn cố định), Hệ quả 07.16 (xác suất $1-\delta$, mọi $w$ trong quả cầu), Bài tập 07.5(c), Phụ lục D Bài 07.

Lời hứa: Bài 06 dòng 620 và 1295 (dạng $\mathbb E_\xi\lvert\cdot\rvert$ với chung $\xi$) → Định lý 08.6(a), đoạn dòng 191; dòng 1071 (SGD nhiều vòng chưa chặn) → Định lý 08.6, Hệ quả 08.7 và đoạn dòng 578; dòng 1130 (SGD nhiều vòng của §5 Bài 06, đầu ra $\bar w_T$) → Hệ quả 08.7. Cầu nối Bài 07 dòng 960 → dòng 3 và §10. Đều được giữ.

Kí hiệu nhất quán với Bài 05–07 và `ky-hieu.md`: $\xi=(i_1,\ldots,i_T)$ theo Định nghĩa 05.18 (Bài 05 viết $\xi_t=i_t$); $w_1$ tất định; $w_{T+1}$, $\bar w_T$ như Bài 05; $\epsilon_{\mathrm{stab}}(m)$, $s^{(i)}$, $z'$ như Bài 06; $G$ có quan hệ với (G2) và (L) được nói rõ ở dòng 111; $\beta$ như Định nghĩa 05.6; $\Delta_t$ có câu phân biệt với Bài 05 (dòng 115); $\varphi$ chỉ dùng cho oracle (dòng 632), đúng QĐ 10.

Danh sách tiên quyết: đủ các khối được dẫn trong thân bài, trừ hai chỗ ở P4.

## 5. Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | §2, dòng 111 (P1) | "Tính đồng bức" được dùng để lập luận trước Định nghĩa 08.3 (dòng 224); dòng 5 chỉ nêu tên. Vi phạm quy tắc định nghĩa trước khi dùng. | "Giả thiết (S) được đặt trên toàn $\mathbb R^p$ vì chứng minh tính đồng bức (Phụ lục A) dùng những điểm có thể nằm ngoài $W$." | "Giả thiết (S) được đặt trên toàn $\mathbb R^p$ vì chứng minh ở Phụ lục A dùng những điểm có thể nằm ngoài $W$." (−3 chữ) |
| trung bình | §8, dòng 691 (P2) | Phụ lục D Bài 07 chỉ có một câu lập luận trong giao thức thí nghiệm, kèm điều kiện "độ dài bước đủ nhỏ"; ghi chú gọi đó là "chứng minh" và bỏ điều kiện. | Ghi chú: "Học phần có chứng minh cho hai trường hợp. Hạ gradient trên hàm lỗi bình phương, khởi tạo tại $0$, hội tụ tới nghiệm nội suy chuẩn nhỏ nhất (Phụ lục D của Bài 07)." Bài 07 dòng 1099: "Đây cũng là giới hạn của hạ gradient … khởi tạo tại $0$ với độ dài bước đủ nhỏ: mọi điểm lặp nằm trong không gian hàng…" | "Học phần có lập luận cho hai trường hợp. Hạ gradient trên hàm lỗi bình phương, khởi tạo tại $0$, với độ dài bước đủ nhỏ, hội tụ tới nghiệm nội suy chuẩn nhỏ nhất (Phụ lục D của Bài 07)." (+5 chữ) |
| trung bình | §9, dòng 699, 807–809, 845 (P3) | Câu mở §9 hứa ba ví dụ, mỗi ví dụ bỏ một điều kiện, nhưng Mệnh đề 08.10, Nhận xét 08.11 chen giữa; sau Nhận xét 08.11, Ví dụ 08.9 bắt đầu không có câu chuyển; dòng 845 lại quay về trường hợp không lồi. Bước 3 Ví dụ 08.10 (ReLU) bỏ cả ba giả thiết, không phải "một". | Thứ tự khối: Ví dụ 08.8 → Mệnh đề 08.10 → Nhận xét 08.11 → Ví dụ 08.9 → Ví dụ 08.10 → dòng 845 "Không có tính lồi, SGD vẫn có một bảo đảm tối ưu…" → Mệnh đề 08.12. | Chuyển dòng 845, khối Mệnh đề 08.12 và đoạn dòng 864 lên ngay sau Nhận xét 08.11 (không đổi số: bộ đếm khối vẫn 08.10, 08.11, 08.12; bộ đếm ví dụ riêng). Trước Ví dụ 08.9 thêm: "Hai ví dụ cuối giữ tính lồi và bỏ điều kiện độ dài bước hoặc tính trơn." (+17). Dòng 699 sửa "Mỗi ví dụ dưới đây bỏ một trong ba điều kiện" thành "Ba ví dụ dưới đây lần lượt bỏ tính lồi, điều kiện độ dài bước và tính trơn" (+2). Câu kết dòng 866 giữ nguyên, vẫn đứng sau Ví dụ 08.10. |
| nhẹ | Tiên quyết, dòng 42, 44 (P4) | Ví dụ 06.9 có trong danh sách nhưng không được dẫn ở thân bài (người viết đã cắt câu dẫn, §13.2 mục 4 của dàn ý). Bất đẳng thức trung bình cộng–trung bình nhân dùng ở chứng minh Hệ quả 08.8 (dòng 651) nhưng không có ở "Giải tích". | grep "Ví dụ 06.9": chỉ dòng 42. Dòng 651: "Theo bất đẳng thức trung bình cộng–trung bình nhân". | Dẫn lại ở §10, giới hạn "Cận gradient đều": "…cần $W$ bị chặn và dữ liệu bị chặn (Ví dụ 06.9)." (+3); thêm "bất đẳng thức trung bình cộng–trung bình nhân" vào mục Giải tích (+5). |
| nhẹ | §1, dòng 84 (P5) | $\beta$, $G$ xuất hiện trong bảng "cố định / ngẫu nhiên" trước khi §2 nêu nghĩa; tương tự $G$, $\lambda$ ở dòng 3. Cả hai đã có nghĩa từ Bài 05–06, nên chỉ là nhẹ. | Dòng 84: "$D$, $W$, $\ell$, $\beta$, $G$, …"; dòng 102 mới nêu nghĩa. | Dòng 84: thay "$\beta$, $G$" bằng "hằng số trơn $\beta$, cận gradient $G$" (+5). Dòng 3 có thể để nguyên (nhìn lại Bài 06). |
| nhẹ | Định nghĩa 08.3 (dòng 225) và §9 (dòng 781, 796) (P6) | $c$ mang hai nghĩa: hệ số giãn và hằng số của lịch $\eta_t=c/t$. $s$ vừa là mẫu vừa là chỉ số cộng ($\sum_{s=1}^{t-1}\eta_s$, dòng 563–571; $\prod_{s=t+1}^T$, dòng 753, 784). | "$\Gamma$ có hệ số giãn $c$"; "Với $\eta_t=c/t$, trong đó $c>0$"; "$\mathbb E\Delta_t\le\frac{2G}m\sum_{s=1}^{t-1}\eta_s$". | Đổi chỉ số cộng $s$ thành $r$ (hoặc $k$) ở Hệ quả 08.7 và Mệnh đề 08.10 (0 chữ). Với $c$: đặt hệ số giãn là $\kappa$ trong Định nghĩa 08.3 (0 chữ), hoặc giữ và chấp nhận. |
| nhẹ | §2, dòng 105 (P7) | Nhãn (T2) bị phát biểu lại thành "$\ell\ge0$ đo được, $L_D(w_1)<\infty$". Bài 01 (dòng 83) đặt điều kiện hữu hạn cho mọi $h$; Bài 06 dùng (T2) cho "$\ell\ge0$ đo được" và tách điều kiện khả tích. | Bài 01 dòng 83: "(T2) Hàm lỗi. $\ell\ge0$ và $\ell(h,\cdot)$ đo được…; khi hàm lỗi không bị chặn, cần thêm $L_D(h)<\infty$." | "…và (T2) ($\ell\ge0$, đo được), cùng điều kiện $L_D(w_1)<\infty$." (+3) |
| nhẹ | §10, dòng 870 (P8) | Số $0{,}045$ và $0{,}919$ là của bảng câu hỏi mở đầu; Ví dụ 08.6 dùng $0{,}0445$ và $0{,}9188$ trong tỉ số. | Dòng 870: "khoảng cách đo được tăng từ $0{,}045$ lên $0{,}919$ (Ví dụ 08.6)". | "(câu hỏi mở đầu)" thay "(Ví dụ 08.6)" (+1). |
| nhẹ | §12, dòng 938 (P9) | (i) "Các kết quả của bài dùng mỗi quan sát là một cặp $(x,y)$" không đúng: các định lý phát biểu cho $z\in\mathcal Z$ bất kì; ví dụ Huber dùng $\mathcal Z=\mathbb R$. (ii) "độ hợp lý" lần đầu trong tài liệu, thiếu tiếng Anh (`thuat-ngu.md` §11: likelihood). | "Các kết quả của bài dùng mỗi quan sát là một cặp $(x,y)$, các quan sát độc lập…"; "$-\ln$ độ hợp lý của cả chuỗi". | "Các kết quả của bài dùng các quan sát độc lập, mỗi quan sát là một điểm $z$ (với hồi quy logistic, một cặp $(x,y)$), và hàm lỗi lồi…"; "$-\ln$ độ hợp lý (likelihood) của cả chuỗi". (+8) |
| nhẹ | Ví dụ 08.10, dòng 838 (P10) | "tiền kích hoạt" là từ mới, không có ở Bài 07 và `thuat-ngu.md`, không có tiếng Anh. | "tại các tham số có một tiền kích hoạt bằng $0$" | "có một tiền kích hoạt (pre-activation), tức một tọa độ của $\Theta_1x+b_1$, bằng $0$" (+7), hoặc chỉ thêm "(pre-activation)" (+1); bổ sung vào `thuat-ngu.md` §10. |
| nhẹ | Ví dụ 08.10, dòng 839 (P11) | Bài tập 07.5(c) chứng minh trung điểm tệ hơn cho hàm mục tiêu bình phương $F(\theta)=\tfrac14\sum(f_\theta(x_i)-\tilde y_i/2)^2$, còn câu đang nói về hàm lỗi logistic. Kết luận vẫn đúng với cùng cặp tham số, nhưng chỗ dẫn cần nói rõ. | Bài tập 07.5: "hàm mục tiêu $F(\theta)=\frac14\sum_{i=1}^4\big(f_\theta(x_i)-\frac{\tilde y_i}2\big)^2$". | "…có thể tệ hơn cả hai (Bài tập 07.5(c), với hàm mục tiêu bình phương)…" (+5) |
| nhẹ | §8, dòng 693 (P12) | Giá trị $0{,}603$ ở $10$ vòng chỉ xuất hiện ở Phụ lục D (dòng 1084); người đọc thân bài không thấy nguồn. | "nhỏ nhất ở khoảng $5$ đến $10$ vòng ($0{,}589$ và $0{,}603$)" | "($0{,}589$ và $0{,}603$; Phụ lục D)" (+2). |
| nhẹ | §10, cuối mục (dòng 882–888) (P13) | Mục kết bằng danh sách, không có câu văn xuôi (Bài 06 §10 kết bằng một câu sau danh sách). | Dòng cuối §10 là gạch đầu dòng "Rủi ro kì vọng." | Chuyển đoạn dòng 872 ("Hệ quả 07.16 đúng với xác suất…không thay được nhau.") xuống cuối §10 (0 chữ). |
| nhẹ | Dòng 25, 310, 538 (P14) | Ba chỗ lặp. (a) Dòng 25 nêu lỗi phân lớp $0{,}309$; $0{,}301$; $0{,}312$, dòng 693 nêu lại để lập luận. (b) Câu đầu §6 lặp dòng 218 và 283. (c) Dòng 538 lặp dòng 193. | (a) dòng 25 và 693; (b) "Theo Bổ đề 08.4, một bước chung không làm tăng khoảng cách giữa hai lần chạy."; (c) "nó đo tính ngẫu nhiên của thuật toán, không đo độ nhạy theo mẫu" và dòng 193 "đo tính ngẫu nhiên của thuật toán, không đo độ nhạy theo một quan sát của mẫu". | Chỗ cắt: (a) bỏ câu lỗi phân lớp ở dòng 25 (−25 chữ), giữ ở dòng 693; (b) bỏ câu đầu dòng 310, câu mở §6 bắt đầu từ "Ở bước khác biệt…" (−16); (c) dòng 538 bỏ vế sau dấu chấm phẩy (−15). Tùy chọn (d): bỏ câu "Các đại lượng đo được nằm dưới cận, đúng như định lý khẳng định." ở dòng 540, đã có ở Bước 4 (−11; `no-ai-slop`: câu tóm lại điều vừa nói). |
| nhẹ | Dòng 3 (P15) | Câu hỏi cuối Bài 07 có "qua số bước và độ dài bước"; dòng 3 bỏ cụm này, trong khi đó là đại lượng bài trả lời. | Bài 07 dòng 960: "quỹ đạo của SGD, qua số bước và độ dài bước, có cho một bảo đảm…" | "…quỹ đạo của SGD, qua số bước và độ dài bước, có cho một bảo đảm cho chính hàm mà SGD trả về không." (+6) |
| nhẹ | Dòng 656, 845 (P16) | "sai số tối ưu" dùng cho hai đại lượng: Định lý 05.14 chặn $F(\bar w_T)-F(u)$ (Bài 05: "độ chênh tối ưu"), còn `thuat-ngu.md` dành "sai số tối ưu thực nghiệm" cho $\operatorname{opt}_S$. | Dòng 656: "Định lý 05.14 chỉ chặn sai số tối ưu của $\bar w_T$". | Dòng 656: "chỉ chặn độ chênh tối ưu của $\bar w_T$" (0); dòng 845: "yếu hơn sai số tối ưu thực nghiệm" (+2). |
| nhẹ | Ví dụ 08.6, dòng 522–538 | "$\Delta$" không có chỉ số trong khi Định nghĩa 08.2 định nghĩa $\Delta_t$. | "Mệnh đề 08.5(b) chặn $\mathbb E_\xi\Delta$" | "$\mathbb E_\xi\Delta_{t+1}$" ở câu dòng 522; trong bảng giữ "$\Delta$" (0). |
| nhẹ | Dòng 691, câu thứ ba | Gọi tính ổn định của Định lý 08.6 là một "trường hợp" của chính quy hóa ngầm hơi xa Định nghĩa 08.9 (chọn giữa các điểm có rủi ro thực nghiệm như nhau). Chuyển cho người rà 3 xác nhận. | "Trong Định lý 08.6, ngân sách độ dài bước giới hạn hệ số ổn định như $1/\lambda$ trong Mệnh đề 06.11." | Giữ, hoặc nói rõ: "Định lý 08.6 cho một cách đọc khác: ngân sách độ dài bước đóng vai $1/\lambda$ của Mệnh đề 06.11." (≈0) |

## 6. Ngân sách chữ (thân bài 11 946 / 12 000)

Thêm: P2 +5, P3 +19, P1 −3, P4 +8, P5 +5, P7 +3, P8 +1, P10 +1, P11 +5, P12 +2, P15 +6, P16 +2 (P9 nằm ở cầu nối, cũng tính vào thân bài: +8). Tổng thêm khoảng +62.

Cắt: P14(a) −25, P14(b) −16, P14(c) −15, P14(d) −11. Tổng cắt −67. Thân bài sau sửa khoảng 11 941 chữ. Nếu không dùng P14(d), bỏ P5 (dòng 3 và 84 đều có nghĩa từ Bài 05–06) và P10 bản dài.
