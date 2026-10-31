# Rà soát 5 — Mạch và móc nối, Bài 10 (bản đóng băng `lec10-draft-frozen.md`)

Người rà: tác tử general-purpose (Opus 5.5, effort high), chỉ đọc repo. Bản sao kiểm: `reviews10/r5/lec-10/lecture-note.md` (1 017 dòng; thân 11 982 tiếng theo `wc -w` trên dòng 1–909, phụ lục 1 652). Đề xuất câu chữ viết theo `no-ai-slop` Detect.

## Tổng kết theo mức

- **Chặn bàn giao:** 0.
- **Nghiêm trọng:** 0.
- **Trung bình:** 5. Có hai kí hiệu trùng hoặc lệch so với Bài 05: $M$ mang hai nghĩa trong cùng bài, và $B$ ở Nhận xét 10.16 khác $R$ của Hệ quả 05.15. $\mathcal F_t$ lệch kiểu và lệch chỉ số so với Định nghĩa 05.10. Kết luận của Ví dụ 10.16 dẫn số của một mô hình khác. Câu (f) tổng kết học phần bỏ sót Bài 05, 06, 08 và Thiết lập B của Bài 09.
- **Nhẹ:** 11.
- Mọi số hiệu 01.x–09.x đúng tên khối (30/30, đã grep). Các tham chiếu nội bộ (§k, Phụ lục A–C, "ví dụ dưới đây", "ví dụ thứ ba sau …") đều trỏ đúng chỗ. Cầu nối cuối Bài 09 (dòng 849) được nhắc lại ở dòng 3 và được trả lời ở câu hỏi mở đầu, §10 và §12. Câu (f) khớp "Closing exercise" của blueprint §10.7: bốn bài toán, năm mục, "Bài 01–08".

## Kết quả `forward_refs.py`

```
$ python3 …/forward_refs.py …/reviews10/r5/lec-10/lecture-note.md
0 forward references
```

(Lần chạy đầu bằng đường dẫn tương đối báo lỗi vì script lấy số bài từ `lec-NN` trong đường dẫn. Kết quả trên là lần chạy với đường dẫn tuyệt đối.)

Kiểm tay thêm ba chỗ trỏ tới khối phía sau mà không ghi số (script không bắt được). Cả ba trỏ đúng, nên không ghi thành phát hiện:

- dòng 249 "nêu ngay sau định lý dưới đây" → Nhận xét 10.5;
- dòng 429 "ví dụ thứ ba sau hệ quả dưới đây, Bước 2" → Ví dụ 10.10, Bước 2;
- dòng 645 "ví dụ thứ ba sau mệnh đề dưới đây" → Ví dụ 10.16.

## Bảng lần dùng đầu của kí hiệu mới

| Kí hiệu | Lần dùng đầu | Định nghĩa / giới thiệu | Nhận xét |
|---|---|---|---|
| $q$ | 9 (câu hỏi mở đầu) | 9 | Chữ cục bộ; có nghĩa khác ở Ví dụ 10.6 (xác suất chuyển) và Ví dụ 10.7 ($\pi_\theta(1)$), mỗi lần đều định nghĩa lại. Được |
| $L_A$, $L_B$ | 11 | 11 | Bị dùng lại cho các hàm khác ở Ví dụ 10.15, 10.16, 10.17 và Phụ lục C, mỗi lần có Thiết lập riêng; xem T4 |
| $D_k$, $k$ | 64 | 64 | Được |
| $K$ | **75** (bảng §1) | **90** (bảng §2) | Dùng trước khi giới thiệu 15 dòng; trùng với hằng số $K$ ở Phụ lục A Bước 6 (N1) |
| $\theta$, $\Theta$ | 87, 100 | 87; Ví dụ 10.1 | Được |
| $\pi_\theta$ | 100 (Ví dụ 10.1, dạng $\pi_\theta(1)$) | 100; tổng quát 141 | Được |
| $J(\theta)$ | 104 | 104 (bandit); 156 (tổng quát) | Được; định nghĩa của Ví dụ 10.1 là trường hợp riêng của dòng 156 |
| $H$ | 136 | 136 | Dòng 148 phân biệt với $\mathrm H$, $\mathcal H$. Khớp `ky-hieu.md` |
| $\mu_0$, $P(\cdot\mid s,a)$, $r$ | 138–140 | 138–140 | Được |
| $\tau$, $\mathcal T$, $S_t$, $A_t$ | 153 | 153 | Dòng 168 phân biệt với $\tau$ (Bài 04) và $\tau_i$ (Bài 07), nhưng chưa nhắc $w_\tau$ của Mệnh đề 08.12, khối được dẫn ở Ví dụ 10.7 (N4) |
| $p_\theta(\tau)$ | 154 | 158–165 | Được |
| $R(\tau)$, $r_t$ | 155 | 155 | Có chỗ dùng $R$ không đối số (N2) |
| $\hat g(\tau)$ | 264 | 264 | Dòng 271 phân biệt với $\hat g$ của Bài 02 và 04 |
| $\omega$ | 308 | 308 | Được |
| $M(\tau)$ (hàm trội) | **306** | 306 | Trùng với $M$, ngân sách bộ nhớ (589) (T1) |
| $\hat g_j$, $\tau_j$, $\theta_j$, $\eta_j$, $T$ | 88, 390–392 | 88, 390–392 | Được |
| $R_{\ge t}$ | 419 | 419 | Được |
| $\mathcal F_t$ | 419 | 419 | Khác kiểu và lệch chỉ số so với Định nghĩa 05.10 (T3) |
| $b_t(\mathcal F_t)$ | 454 | 454 | Ví dụ 10.8 và 10.11 dùng hằng số $b$ không đối số (N2) |
| $\vartheta$ | 531 | 531 | Được |
| $\mathcal Z$, $W$, $\ell$ | 585 | 585 ($W$: 65, 89) | Được |
| $M$ (ngân sách bộ nhớ) | 589 | 589 | T1 |
| $w^{(0)}$, $w^{(k)}$ | 590 | 590 | Được |
| $\mathrm{acc}_{k,i}$, $\mathrm{acc}^\circ_i$ | 600 | 600 | Khớp `ky-hieu.md` |
| $\mathcal B$, $\alpha$, $\lambda$, $\Omega$ | 640–641 | 640–641 | Được |
| $\mathcal I_A$ | 708 | 708 | Được |
| $\mathrm{Regret}_T(u)$, $u$, $z_t$ | 763 | 763 | Được |
| $G$, $B$, $v_t$ | 771 | 771 | $B$ lệch so với Bài 05 (T2) |
| $\nu$, $C_R$, $D_eJ$, $\mathcal N_\omega$, $\rho_\tau$ | Phụ lục A | tại chỗ | Được; $h$, $h_0$ (số gia) trùng chữ giả thuyết $h$, chấp nhận được vì cục bộ |
| $\mathbf h$, $\mathbf h^+$, $\Pr_\theta$ | Phụ lục B | 956 | Có ghi rõ khác $h$. Được |

Các thuật ngữ mới đều có tiếng Anh ở lần đầu và khớp `thuat-ngu.md` §12: tác tử, lượt, trạng thái, phần thưởng, chính sách, nhiệm vụ, bài toán bandit, MDP, gradient log, giá, quỹ đạo, tổng phần thưởng, tối ưu chính sách, giá trị nền, tổng phần thưởng từ bước $t$, ngân sách bộ nhớ, định danh nhiệm vụ, ma trận đánh giá, các độ đo, quên thảm họa, phát lại, bộ đệm phát lại, chính quy hóa tham số, trọng số tầm quan trọng, tinh chỉnh, bền vững/mềm dẻo, ma trận Fisher, EWC, xấp xỉ Laplace, hối tiếc, học trực tuyến, dịch chuyển phân bố. Có hai ngoại lệ nhẹ:

- "học trực tuyến" và "hối tiếc" được dùng ở dòng 756, còn tiếng Anh chỉ có ở dòng 763–765 (cách nhau bảy dòng, cùng mục, nên chấp nhận được);
- "ma trận Hesse" (Ví dụ 10.15) không có trong `thuat-ngu.md`, dù Bài 09 Phụ lục đã dùng.

## Nhận xét mạch từng mục

- **Đoạn dẫn (1–5).** Nhắc đúng cầu nối Bài 09 và nêu câu hỏi trung tâm cùng phạm vi. Câu "Phần B không có định lý tổng quát." lặp lại dòng 808, nên có thể cắt (C2).
- **Câu hỏi mở đầu (7–15).** Hai tình huống đúng blueprint 10.1. Câu trả lời ngay sau nêu (T1) và chỉ tới §5, §8. Câu hỏi được trả lời ba lần nhất quán (15, 79, §12(f)). Kịch bản robot không nói phần thưởng ở đâu, dù dòng 9 nhắc "các phần thưởng nó nhận"; phần thưởng chỉ xuất hiện ở Ví dụ 10.2. Lỗi nhỏ, không ghi phát hiện. Cặp tự hỏi tự đáp "…không? Không:" (dòng 15) là mẫu "rhetorical setup" theo `no-ai-slop`, nhưng `van-phong.md` §9a và dàn ý chủ ý dùng nó (N11, tùy chọn).
- **Mục tiêu và tiên quyết.** Mục tiêu 5 đã mất vế "dựa trên ví dụ hai nhiệm vụ bậc hai" của dàn ý, nên §8 và Bài tập 10.5 không còn khớp rõ với mục tiêu nào (N8). Danh sách tiên quyết vừa thừa vừa thiếu (N5).
- **§1–§2.** §1 mở bằng bảy thành phần và kết bằng văn xuôi (dòng 79). $K$ được dùng trước §2 (N1). Quan hệ giữa "người học" và "tác tử" không được nêu (N6).
- **§3.** Ví dụ 10.1 cùng khối ứng dụng. Câu kết (129) nối sang §4. Câu hỏi của khối ứng dụng được trả lời đúng hẹn ở Ví dụ 10.11 (§6).
- **§4.** Mở bằng robot, kết bằng câu nối sang §5 (201). Ví dụ 10.2 nối lại câu hỏi mở đầu đúng như dàn ý. Tên trạng thái $s_1, s_2$ trùng với kí hiệu chung $s_t$ (N3).
- **§5.** Mở bằng vấn đề (205) và nối câu hỏi mở đầu ở 205 và 298. Thứ tự là Bổ đề → phản ví dụ → Định lý → Nhận xét 10.5 → hai ví dụ kiểm → phản ví dụ → Thuật toán → Ví dụ 10.7. Nhận xét 10.5 chen giữa định lý và ví dụ kiểm của nó, nhưng vì Ví dụ 10.3 đã hẹn nó "ngay sau định lý" nên vẫn được. Câu kết (413) lặp ý của dòng 298 và 806 (C3).
- **§6.** Mở bằng vấn đề (417) và kết bằng văn xuôi (578). Ví dụ 10.12 (cận Hoeffding cho chính sách cố định) đến ngay sau Ví dụ 10.11, không có câu dẫn, và lệch khỏi tên mục (N9).
- **§7.** Mở bằng tình huống 2 (582); "môi trường" ở đây mang nghĩa nhiệm vụ (N7). Câu đầu dòng 595 lặp bảng §1 và dòng 79 (C1). Câu kết (631) nối sang §8. Tốt.
- **§8.** Mở bằng câu hỏi mở đầu (635) và kết bằng văn xuôi (752). Ví dụ 10.16 kết luận bằng số của một mô hình khác (T4).
- **§9.** Mở bằng vấn đề (756) và kết bằng văn xuôi (802). Ví dụ 10.17 khớp "Important conclusion" của blueprint 10.5. $B$ cần đổi thành $R$ (T2).
- **§10.** Tóm đúng hai phần. Đoạn 2 chỉ nói tới lượt của Phần A (N10). Các giới hạn dẫn đúng ví dụ (đã kiểm từng dòng: 10.8, 10.11, 10.7, 10.6, 10.13, 10.16, 10.17).
- **§11.** Số và tên Bài tập 10.1–10.9 khớp dàn ý §4 và §13.3 mục 16. Phần ánh xạ mục tiêu khớp dàn ý.
- **§12.** Các câu (a)–(e) dùng lại ví dụ xuyên suốt và dẫn đúng khối. Câu (f) khớp blueprint §10.7, nhưng phần nhìn lại Bài 01–09 chưa đủ (T5). Theo dàn ý, §12 không có đoạn tóm tắt văn xuôi; quyết định này phù hợp với `no-ai-slop`.
- **Ví dụ xuyên suốt.** Mạch bandit đi qua 10.1 → 10.4 → 10.8 → 10.9 → §12(a). Robot/MDP đi qua mở đầu → 10.2 → 10.5 → 10.6 → 10.10 → 10.12 → §12(c). Khối ứng dụng §3 được giải ở 10.11. Hai nhiệm vụ đi qua mở đầu → Mệnh đề 10.13 → 10.14 → §12(d). Các số nhất quán giữa các chỗ ($\tfrac38$, $\pm0{,}75$, $1{,}75$, $(-0{,}025;0{,}25;-0{,}125)$, $\tfrac12$, $0{,}125$/$-0{,}25$).

## Đối chiếu móc nối

- **Số hiệu.** Đã grep đủ 30 số hiệu được dẫn trên `materials/lec-0x/lecture-note.md`, và mọi tên trong ngoặc khớp tên khối: 01.1, 01.5, 01.6, 01.9, 01.22, 01.24, 02.7, 02.8, 02.10, 02.14, 03.15, 04.11, 04.17, 05.10, 05.11, 05.12, 05.13, 05.14, 05.15, 05.18, 06.2, 07.11, 08.12, 09.1, 09.2, 09.4, 09.8, 09.12 (Bước 4: $v/\phi$, đúng), 09.14, 09.15 (Phụ lục B của Bài 09 là "Đổi chỗ đạo hàm và kì vọng", đúng).
- **Nội dung dẫn.** Các chỗ dẫn đều đúng nội dung:
  - Hệ quả 02.10(b), bán kính $\sqrt{\ln(2/\delta)/(2m)}$;
  - đoạn sau Nhận xét 02.8: bán kính nhân $b-a$;
  - Định nghĩa 05.4: $G$-Lipschitz (§13 dòng 905);
  - Mệnh đề 05.13: tất định, không dùng tính lồi (Nhận xét 10.16);
  - Mệnh đề 08.12: $F$ trơn, không cần lồi, phương sai có điều kiện bị chặn, $W=\mathbb R^p$ (Ví dụ 10.7);
  - Mệnh đề 09.8: entropy khi lớp chứa phân bố thật;
  - Ví dụ 09.4: cần cận dưới cho xác suất;
  - "(T3), và (T2) khi có mật độ": khớp Bài 09 dòng 118.
- **Kí hiệu.** $H$ và $\mathrm H$, cũng như $\tau$ và $\hat g$, được phân biệt đúng `ky-hieu.md`. $G$ dùng đúng nghĩa Bài 05. $\mathcal F_t$ sai lệch: xem T3. $B$ và $R$: xem T2. $R$ và $b$ không đối số: xem N2.

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình (T1) | Nhận xét 10.5 dòng 306, 308; Phụ lục A dòng 914–949; so với Định nghĩa 10.10 dòng 589 và §8–§10, Phụ lục C | $M$ mang hai nghĩa trong cùng bài: hàm trội và ngân sách bộ nhớ. `ky-hieu.md` dòng 115 giữ $M$ cho ngân sách bộ nhớ ("khác … hàm trội (Bài 09)") | 306 "một hàm khả tích $M\ge0$ với $\lvert R(\tau)\rvert\,\lVert\nabla_\theta p_\theta(\tau)\rVert\le M(\tau)$"; 589 "**Ngân sách bộ nhớ** … Số $M\ge0$" | Đổi hàm trội thành $\Lambda$ ở Nhận xét 10.5 và Phụ lục A (Bước 1–6, câu ⊡). Thêm ở 306 "(như hàm $M$ của Mệnh đề 09.15)" nếu muốn giữ mối nối với Bài 09 (+6 tiếng, tùy chọn). Không đổi số chữ nếu bỏ phần ngoặc |
| trung bình (T2) | Nhận xét 10.16 dòng 771–775; Ví dụ 10.17 Bước 2 dòng 793 | $B$ dùng cho cận $\lVert w_1-u\rVert$, còn Bài 05 dùng $R$ cho đại lượng này (Định lý 05.14, Hệ quả 05.15: $\eta=R/(G\sqrt T)$, cận $RG/\sqrt T$) và $B$ cho bán kính của $W$. Chính dòng 645 viết "bán kính $B$ của Bài 05". `ky-hieu.md` dòng 108: "$R$ trần là cận khoảng cách Bài 05" | 771 "với mọi $u\in W$ có $\lVert w_1-u\rVert\le B$"; Bài 05 dòng 815 "$\lVert w_1-u\rVert\le R$" | Thay $B$ bằng $R$ ở 771–775 và 793 ("$\lVert w_1-u\rVert\le1=R$"). Sửa 775 thành "và vế phải bằng $RG\sqrt T$ khi $\eta=R/(G\sqrt T)$, như Hệ quả 05.15" (+2 tiếng). Phần B không dùng $R(\tau)$, nên $R$ trần ở đây không trùng |
| trung bình (T3) | §6 dòng 419; Phụ lục B dòng 956 | $\mathcal F_t$ là một bộ biến ngẫu nhiên chứa $S_t$ và đứng trước hành động $A_t$. Định nghĩa 05.10 lại đặt $\mathcal F_t=\sigma(\xi_1,\ldots,\xi_t)$, là σ-đại số, và điều kiện hóa trước lần rút thứ $t$ theo $\mathcal F_{t-1}$ (Bổ đề 05.12, Mệnh đề 08.12). Câu "cùng vai lịch sử của Định nghĩa 05.10" che cả khác biệt về kiểu lẫn độ lệch chỉ số. `ky-hieu.md` dòng 111 ghi "cùng nghĩa với Bài 05" | 419 "*Lịch sử* đến bước $t$ là bộ $\mathcal F_t=(S_0,A_0,\ldots,A_{t-1},S_t)$, cùng vai lịch sử của Định nghĩa 05.10"; Bài 05 "$\mathcal F_t=\sigma(\xi_1,\ldots,\xi_t)$"; Bổ đề 05.12 "$\mathbb E[g_t\mid\mathcal F_{t-1}]$" | Viết 419 thành: "…là bộ $\mathcal F_t=(S_0,A_0,\ldots,A_{t-1},S_t)$, gồm mọi biến được rút trước $A_t$. Bộ này đóng vai $\mathcal F_{t-1}$ của Bổ đề 05.12; kì vọng có điều kiện theo $\mathcal F_t$ hiểu là theo bộ này." (+20 tiếng). Đề nghị điều phối viên sửa `ky-hieu.md` dòng 111 thành "bộ biến trước $A_t$; vai như $\mathcal F_{t-1}$ của Bài 05" |
| trung bình (T4) | Ví dụ 10.16, Kết luận, dòng 749 | Hai mốc $0{,}25$ ("điểm thỏa hiệp") và $0{,}125$ ("riêng nhiệm vụ A") thuộc mô hình hồi quy của Phụ lục C, $L_A(w)=\tfrac12(w^2+0{,}25)$. Ví dụ lại đặt $L_A(w)=\tfrac12(w^2+1)$, với giá trị nhỏ nhất $0{,}5$ và giá trị tại $w=\tfrac12$ là $0{,}625$. Người đọc sẽ so $0{,}252$ với hàm của chính ví dụ và thấy mâu thuẫn | 732 "$L_A(w)=\tfrac12(w^2+1)$"; 749 "gần $0{,}25$ của điểm thỏa hiệp, không gần $0{,}125$ của riêng nhiệm vụ A"; 1004 "$L_A(w)=\tfrac12(w^2+0{,}25)$, nhỏ nhất bằng $0{,}125$" | "Trong thí nghiệm của học phần (Phụ lục C), một bài toán hồi quy với $L_A(w)=\tfrac12(w^2+0{,}25)$, rủi ro kiểm tra trên A sau nhiệm vụ B là …" (+8 tiếng) |
| trung bình (T5) | §12(f) và lời giải, dòng 848, 863–877 | Phần tổng kết học phần không nhắc Bài 05, 06, 08: dòng "Phân lớp có giám sát (Bài 01–04, 07)" chỉ xét hàm lỗi 0–1. Bài 09 được tóm bằng Thiết lập A, bỏ Thiết lập B (một chuỗi thời gian, các cửa sổ chồng lấn), nơi (T1) và (T7) không thỏa. Thiết lập B có ở Định nghĩa 09.1, §6 và câu (b) cuối Bài 09. Blueprint §10.7 chỉ yêu cầu bốn bài toán, nhưng tiêu đề §12 hứa "tổng kết học phần" | 863 "*Phân lớp có giám sát (Bài 01–04, 07).*"; 866 "với hàm lỗi 0–1"; 869 "các cận như Định lý 02.14, 03.15, 04.11, 07.11"; 877 "(T3), và (T2) khi có mật độ" | (i) Đổi 863 thành "*Phân lớp có giám sát (Bài 01–08).*". (ii) Đổi 866 thành "$L_D(h)$ nhỏ, với hàm lỗi 0–1, hoặc hàm lỗi lồi thay thế ở Bài 05–06, 08." (iii) Đổi 869 thành "… 04.11, 07.11, và của Bài 05–06, 08 khi thêm (C), (G1), (G2)." (iv) Thêm vào 877 "; (T1) ở Thiết lập B, vì các cửa sổ chồng lấn phụ thuộc nhau (Định nghĩa 09.1)". Tổng cộng khoảng +34 tiếng |
| nhẹ (N1) | §1 dòng 61, 75; Phụ lục A dòng 949 | $K$ xuất hiện ở bảng dòng 75 trước khi được giới thiệu ở §2 dòng 90. Phụ lục A dùng $K$ làm hằng số chặn, trùng với số nhiệm vụ | 75 "$D_1,\ldots,D_K$"; 949 "bị chặn bởi một hằng số $K$" | Dòng 61: "Một mô hình nhận lần lượt dữ liệu của $K$ nhiệm vụ (task)…" (+1). Dòng 949: đổi $K$ thành $C_\mu$ (ba chỗ) |
| nhẹ (N2) | 168; Ví dụ 10.11 dòng 537–543; Ví dụ 10.12 dòng 562; Ví dụ 10.8 dòng 486–507 | Có $R$ và $b$ không đối số, trái quyết định kí hiệu 1 (`review-log.md`) và `ky-hieu.md` dòng 108, 112. Ở Ví dụ 10.11, $R$ là phần thưởng một bước có khoản $c$, không phải $R(\tau)$ tổng quát | 168 "còn $R$ thì không"; 537 "phần thưởng $R=c+X$"; 562 "$R/4\in[0,1]$" | 168: "$R(\tau)$". Ví dụ 10.11: vì $H=1$, viết "$R(\tau)=c+X$" (hoặc $r_0$) ở 537 và các dòng 541–543. 562: "$R(\tau_j)/4$". Hằng số $b$ ở Ví dụ 10.8 và 10.11 là cục bộ nên có thể giữ; nếu giữ, thêm "(hằng số, khác $b_t(\cdot)$)" ở 486 (+4, tùy chọn) |
| nhẹ (N3) | Ví dụ 10.2 dòng 171; Ví dụ 10.5 dòng 351; Ví dụ 10.6 dòng 375 | Tên trạng thái $s_0,s_1,s_2$ trùng với kí hiệu chung $\tau=(s_0,a_0,s_1,a_1)$ của Định nghĩa 10.2, trong đó chỉ số là bước. Ví dụ, ở 351 "$s_1$" là tên trạng thái nhưng "$a_1$" là hành động ở bước 1; ở 375, "$\ln P(s_1\mid s_0,a_0)$" đọc được theo cả hai nghĩa | 351 "chỉ khác $0$ trên bốn quỹ đạo qua $s_1$, với thừa số $a_1-\tfrac12$" | Thêm vào cuối Thiết lập của Ví dụ 10.2: "Trong các ví dụ dựa trên ví dụ này, $s_1$, $s_2$ là tên trạng thái, còn trạng thái ở bước $1$ là $S_1\in\{s_1,s_2\}$." (+20). Ở 375, viết "$\ln P(S_1\mid s_0,A_0)$" |
| nhẹ (N4) | dòng 168 | Câu phân biệt các nghĩa của $\tau$ bỏ sót chỉ số ngẫu nhiên $w_\tau$ của Mệnh đề 08.12, khối được dẫn ở Ví dụ 10.7 | Bài 08: "$\mathbb E\lVert\nabla F(w_\tau)\rVert^2$ với $\tau$ rút đều trên $\{1,\ldots,T\}$" | "…khác dung sai $\tau$ của Bài 04, nhãn $\tau_i$ của Bài 07 và chỉ số ngẫu nhiên $\tau$ của Mệnh đề 08.12" (+7) |
| nhẹ (N5) | Kiến thức tiên quyết, dòng 30–33 | Thuật toán 05.11 có trong danh sách nhưng không được dẫn trong thân bài. Ngược lại, thân bài dùng mà danh sách không nêu: dưới gradient (Định nghĩa 05.2) và phép chiếu (Định nghĩa 05.7) ở Nhận xét 10.16; entropy (Định nghĩa 09.7) ở Nhận xét 10.9; phân bố hậu nghiệm (Định nghĩa 09.10) ở Nhận xét 10.14; (T3) ở §12(f). Bài 07 và 09 đều viết "(T3) (đoạn sau Nhận xét 02.8)" | 31 "hạ gradient ngẫu nhiên có chiếu (Thuật toán 05.11)"; 531 "entropy $\mathrm H$"; 712 "phân bố hậu nghiệm"; 771 "$v_t\in\partial\ell(w_t,z_t)$" | Bài 02: "…và (T3) cùng đoạn sau Nhận xét 02.8 về miền $[a,b]$". Bài 05: thay "hạ gradient ngẫu nhiên có chiếu (Thuật toán 05.11)" bằng "dưới gradient (Định nghĩa 05.2); phép chiếu (Định nghĩa 05.7)". Bài 09: thêm "entropy (Định nghĩa 09.7); phân bố hậu nghiệm (Định nghĩa 09.10)". Khoảng +10 tiếng |
| nhẹ (N6) | §1 dòng 51–55; các dòng 141, 146, 201, 298 | Phần A dùng cả "tác tử" (51, 98, 198, 400) lẫn "người học" (141, 146, 201, 298, 806) nhưng không nói hai vai này liên quan thế nào | 51 "Một *tác tử* (agent) tương tác với môi trường"; 806 "Khi người học tương tác với môi trường" | Dòng 55: "**Lớp mô hình.** Một họ *chính sách* (policy) có tham số do người học chọn; …" (+4). Dòng 806: "Khi tác tử tương tác với môi trường" (0) |
| nhẹ (N7) | §7 dòng 582 | "môi trường" mang hai nghĩa: môi trường MDP ở Phần A, và nhiệm vụ ở tình huống 2 của câu hỏi mở đầu. Chỗ chuyển sang chữ "nhiệm vụ" không được nói ra. Ngoài ra "thuật toán được giữ gì" thiếu chữ | 582 "mỗi môi trường có phân bố riêng … thuật toán được giữ gì" | "Ở tình huống thứ hai của câu hỏi mở đầu, mỗi môi trường là một nhiệm vụ với phân bố riêng, và dữ liệu đến lần lượt. … thuật toán được phép giữ gì …" (+4) |
| nhẹ (N8) | Mục tiêu 5, dòng 25 | Bản rút gọn đã bỏ vế của dàn ý "dựa trên ví dụ hai nhiệm vụ bậc hai và các phản ví dụ của bài". Vì vậy §8 (Định nghĩa 10.12, Mệnh đề 10.13) và Bài tập 10.5 (§11 dòng 828, "mục tiêu 5") không khớp rõ với mục tiêu nào | outline dòng 41 | "5. Giải thích, dựa trên ví dụ hai nhiệm vụ bậc hai và các phản ví dụ của bài, vì sao …" (+11) |
| nhẹ (N9) | §6, giữa Ví dụ 10.11 và 10.12 (dòng 555–557) | Ví dụ 10.12 (cận với xác suất cao cho chính sách cố định) đến không có câu dẫn, trong một mục có tên về giá trị nền | 556–557 | Thêm trước khối: "Các kết quả ở trên là đồng nhất thức; khi chính sách cố định, các lượt thỏa (T1) và cho một cận với xác suất cao." (+20) |
| nhẹ (N10) | §10 dòng 808 | "mẫu cố định trở thành các lượt sinh bởi chính sách hiện tại" chỉ đúng cho Phần A | 808 | "…trở thành các lượt sinh bởi chính sách hiện tại (Phần A) hay một dãy mẫu từ $D_1,\ldots,D_K$ (Phần B)." (+10) |
| nhẹ (N11, tùy chọn) | dòng 15 | Cặp tự hỏi tự đáp ("rhetorical setup" theo `no-ai-slop` Detect). Đây là lựa chọn có chủ ý của dàn ý và `van-phong.md` §9a, nên chỉ báo, không bắt buộc | "Các quan sát của robot có tạo thành một mẫu $S\sim D^m$ như (T1) không? Không:" | Nếu bỏ: "Các quan sát của robot không tạo thành một mẫu $S\sim D^m$ như (T1): …" (−1) |

## Ngân sách chữ (thân 11 982/12 000)

Phần thêm cho các mục trung bình (T2 +2, T3 +20, T4 +8, T5 +34) khoảng +64 tiếng. Cần các chỗ cắt sau:

- **C1 (−33).** Dòng 595: bỏ cả câu đầu "Các mẫu, bộ nhớ, nguồn ngẫu nhiên của thuật toán và các mẫu kiểm tra là ngẫu nhiên; mỗi mẫu thỏa (T1) với phân bố của nó, nhưng không có một $D$ chung." Câu này lặp bảng §1 (dòng 76) và gần như nguyên văn dòng 79. Đoạn bắt đầu luôn bằng "Hai giao thức chỉ khác $M$ …".
- **C2 (−8).** Dòng 5: bỏ "Phần B không có định lý tổng quát." vì dòng 808 đã nói "không có định lý học liên tục tổng quát".
- **C3 (−18).** Dòng 413: bỏ câu đầu, vì dòng 298 (câu ⊡) và 806 đã nói cùng ý. Đoạn còn lại: "Định lý 10.4 không bảo đảm Thuật toán 10.6 tới cực đại của $J$, và theo Ví dụ 10.4, mỗi ước lượng có thể ngược dấu với gradient."
- **C4 (−11, nếu cần).** §13, dòng 907: bỏ "định nghĩa ma trận Fisher ở Nhận xét 10.14 là định nghĩa chuẩn". Người rà chuyên gia nên xác nhận trước.

C1 + C2 + C3 = −59 tiếng. Sau khi thêm các mục trung bình, thân bài vào khoảng 11 987, vẫn dưới trần. Các mục nhẹ có thêm chữ (N1, N3, N4–N10, khoảng +87) chỉ nên làm khi có thêm chỗ cắt. Các mục không đổi số chữ (T1, N1 phần Phụ lục, N2, N6 dòng 806) làm được ngay.
