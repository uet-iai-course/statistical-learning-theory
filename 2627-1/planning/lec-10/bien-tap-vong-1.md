# Biên tập vòng 1 — Bài 10 (2026-11-01)

Biên tập viên: người viết ghi chú (general-purpose, Opus 5.5, high), người duy nhất ghi repo ở bước này. Căn cứ: `reviews/0-quyet-dinh.md` (ưu tiên cao nhất), năm báo cáo `reviews/1-hoc-vien.md` (R1), `2-toan-hoc.md` (R2), `3-chuyen-gia-nguon.md` (R3), `4-hoc-thuat-van-phong.md` (R4), `5-mach.md` (R5); `thuat-ngu.md` (dòng "điểm so sánh", "độ chính xác phân lớp"), `ky-hieu.md` (dòng $\mathcal F_t$). Số dòng theo bản đóng băng (1017 dòng). Không commit.

**Số tiếng (`wc -w`).** Thân bài: 11 982 → 11 976. Phụ lục: 1 652 → 2 219. Tệp: 1017 → 1040 dòng.

## Nghiêm trọng

| Mã | Dòng | Cách sửa |
|---|---|---|
| N1 (R1, R2 S1, R4 T4, R5 T4) | 749 | Chọn phương án giữ thí nghiệm, không chạy lại script. Kết luận của Ví dụ 10.16 chỉ dùng số của mô hình trong ví dụ: rủi ro cũ kì vọng $\tfrac58+\tfrac1{8M}$ giảm về $\tfrac58$ (điểm thỏa hiệp), không về $\min L_A=\tfrac12$; thiết lập ghi thêm "nhỏ nhất bằng $\tfrac12$", Bước 1 ghi $L_A(\tfrac12)=\tfrac58$. Câu thí nghiệm nêu rõ "một mô hình hồi quy khác, có rủi ro tổng thể trên A là $\tfrac12(w^2+0{,}25)$" và viết "giảm từ $0{,}624$ … về $0{,}25$" (không nói $0{,}331$ "gần" $0{,}25$). Phụ lục C mở phần phát lại bằng "Mô hình ở đây khác mô hình của Ví dụ 10.16". |
| N2 (R1, R3 F2, R4 T8) | 768 | "vượt hàm lỗi trung bình của điểm cố định tốt nhất không quá một lượng tiến về $0$, và có thể thấp hơn". |

## Trung bình (quyết định gộp)

| Mục | Dòng | Cách sửa |
|---|---|---|
| 1. Nhận xét 10.9(ii) (R2) | 533 | Giá trị nền dùng hành động hay phần thưởng từ bước $t$ trở đi (chẳng hạn $R(\tau)$, $r(A_t)$) không là hàm của $\mathcal F_t$; phần thưởng nhận trước bước $t$ thì hợp lệ, dẫn phần thưởng $-2$ ở Ví dụ 10.10, Bước 3. |
| 2. 05.10 và 08.12 (R1, R3 F1, R2) | 397, 410 | Đoạn sau Thuật toán 10.6: viết mỗi lượt như hàm của $\theta_j$ và các biến đều độc lập với các lượt trước thì được một oracle như Định nghĩa 05.10 (Bài tập 10.3); trở ngại thật là (C). Ví dụ 10.7: câu nối "chứng minh Mệnh đề 08.12 chỉ dùng kì vọng và phương sai có điều kiện theo lịch sử, ở đây là các lượt trước", và đủ giả thiết ($J$ $\beta$-trơn, bị chặn trên, phương sai có điều kiện bị chặn, bước hằng $\eta\le1/\beta$). |
| 3. $\mathcal F_t$ (R5 T3) | 419 | "bộ biến quan sát được trước $A_t$; kì vọng có điều kiện theo $\mathcal F_t$ là theo bộ này. Ở Bài 05, lịch sử là σ-đại số và điều kiện hóa trước lần rút thứ $t$ dùng $\mathcal F_{t-1}$ (Bổ đề 05.12); bộ $\mathcal F_t$ ở đây đóng vai đó." Bỏ "cùng vai". |
| 4. Kí hiệu một nghĩa | nhiều | Hàm trội $M\to\Lambda$ (Nhận xét 10.5, Phụ lục A); hằng số Phụ lục A Bước 6 $K\to C_\mu$; số gia Phụ lục A $h\to\Delta$, $h_0\to\Delta_0$; Nhận xét 10.16, Ví dụ 10.17 dùng $R$ cho $\lVert w_1-u\rVert$ ("như Hệ quả 05.15"); rủi ro trên bộ đệm $L_{\mathcal B}\to L_{\mathrm{buf}}$; Ví dụ 10.2 thêm câu "$s_1$, $s_2$ là tên trạng thái; trạng thái ở bước $1$ là $S_1\in\{s_1,s_2\}$", Ví dụ 10.6 viết $\ln P(S_1\mid s_0,A_0)$; Phụ lục B dùng $\mathbf o$, $\mathbf o^+$ thay chữ đậm $\mathbf h$ (bỏ câu "khác giả thuyết $h$"); $K$ giới thiệu ở câu dẫn Phần B của §1. |
| 5. "Người học" | 3, 5, 141, 146, 201, 298, 806 | Thay bằng "thuật toán học" (đoạn mở) hoặc "tác tử" (Phần A). Chỉ còn ở dòng "Sau bài này, người học có thể". |
| 6. "Độ chính xác" | 600, 607, mục tiêu 4 | "độ chính xác phân lớp" $=1-$ rủi ro thực nghiệm với hàm lỗi 0–1, định nghĩa tại Định nghĩa 10.11; "độ chính xác phân lớp trung bình cuối cùng"; thêm câu "với hàm lỗi khác, ta thay $\mathrm{acc}$ bằng rủi ro kiểm tra và đổi chiều các so sánh". "Chính xác" (trạng từ) → "đúng" (408, 640, 997); "nghiệm" → "điểm cực tiểu" (Mệnh đề 10.13, Ví dụ 10.14–10.16). |
| 7. Quy ước độ đo (R4 T6) | 607 | Bỏ "các bài báo dùng những quy ước khác nhau"; viết "Các công thức ở trên là quy ước của học phần; ví dụ dưới đây cho thấy hai quy ước gần nhau cho độ quên khác dấu." Khớp dòng §13. |
| 8. Sutton–Barto (R3 F3, F9) | 906 | §13: khung REINFORCE của Sutton và Barto dùng $G_t$, tức ước lượng của Mệnh đề 10.7(b), còn Thuật toán 10.6 dùng $R(\tau)$; điều kiện giá trị nền của họ nói cho dạng tổng trên mọi hành động. |
| 9. Câu hỏi mở đầu (R1) | 13, 15 | Trả lời việc gộp ở tình huống 2: dữ liệu của A không còn khi học B nên không gộp được; nếu giữ được, mẫu gộp phục vụ rủi ro trung bình (§7). Bỏ cặp tự hỏi tự đáp (R4 N1). |
| 10. Ví dụ từng bước (R1, R4 T4–T5) | 373, 523, 525, 541, 571, 626, 724, 744, 795–797; 705–724 | Ví dụ 10.6 Bước 2: nêu $r_1$ độc lập với $A_0$ nên $\mathbb E[r_1(A_0-\tfrac12)]=0$, rồi phép tính trên hai giá trị của $A_0$ trong `aligned`. Ví dụ 10.10: Thiết lập báo Bước 3 đổi quá trình; Bước 1 tính một tọa độ; Bước 2 bảng phương sai từng tọa độ (phân số đúng, vừa 390 px); Bước 3 tính đủ phương sai $1$. Ví dụ 10.11 Bước 2 tách hai dòng. Ví dụ 10.12 Bước 3 thêm bất phương trình. Ví dụ 10.13: Thiết lập báo Bước 5 dùng ma trận thứ hai. Ví dụ 10.15 Bước 3: phép thay $w=(v,-v)$. Ví dụ 10.16: dừng ở $\tfrac1{8M}$, nêu dạng tổng quát $w_M=(1-\alpha)+\alpha\bar Z_M$. Ví dụ 10.17: Bước 1 nói hối tiếc tĩnh bằng hối tiếc so với $u=\tfrac12$; Bước 3–4 ghi "tính bằng máy/tính trên 1000 vòng" và quy nạp $w_{t+1}=(1-\tfrac1t)w_t+\tfrac1tz_t$. Nhận xét 10.14(ii): phạt bậc hai là khai triển Taylor bậc hai quanh $w^{(1)}$ với $\Omega$ là ma trận Hesse; với hàm lỗi log và mô hình chứa phân bố thật, tại tham số thật, Fisher bằng Hesse. Định nghĩa 10.12 nới $\Omega$ thành đối xứng nửa xác định dương, thường là đường chéo (R2), nên Ví dụ 10.15 Bước 2 nằm trong định nghĩa. EWC: "với hai nhiệm vụ" (R3 F5). |
| 11. §10 và §12(f) (R2, R5 T5) | 812, 816, 808, 863–877 | "$225$ lần" và "$\tfrac1{8M}$" ghi là của Ví dụ 10.11, 10.16. §10 đoạn 2 nói cả hai phần. Lời giải (f): xét "Phân lớp và hồi quy có giám sát (Bài 01–08)" (hàm lỗi 0–1 hay lồi; Bài 05–06, 08 khi thêm giả thiết tối ưu), Thiết lập B của Bài 09 vi phạm (T1), (T3) có chú thích. Bốn danh sách chuyển sang Phụ lục D (lý do: ngân sách thân bài; xem cuối tệp); §12 giữ một câu tóm tắt và dẫn Phụ lục D. |
| 12. Văn phong (R4 T1, T2, T7, T9) | 413, 578, 631, 752, 802; 465, 507, 527; 3; 146, 531, 682, 712, 808 | Câu kết: §5 giữ một câu giới hạn; §6 bỏ câu kết (mục kết bằng Kết luận Ví dụ 10.12); §7 "Ma trận đánh giá chỉ ghi độ chính xác phân lớp của các tham số mà một thuật toán đi qua; nó không cho biết tham số nào có rủi ro nhỏ trên mọi nhiệm vụ cùng lúc"; §8 "Mọi rủi ro cũ trong §8 là hàm bậc hai; với rủi ro khác, phạt bậc hai chỉ xấp xỉ rủi ro cũ quanh $w^{(1)}$"; §9 "Nhận xét 10.16 chặn hối tiếc tĩnh trên mọi dãy; độ quên thì chưa có cận nào trong bài". Ý "không nói về phương sai" chỉ còn ở Định lý 10.4, Mệnh đề 10.7, Ví dụ 10.8 (bỏ ở Hệ quả 10.8, cuối Ví dụ 10.8, Kết luận Ví dụ 10.10 viết lại). Đoạn mở bỏ câu "Câu hỏi cuối Bài 09 là …", câu hỏi trung tâm ghi "nêu ở cuối Bài 09". Tách câu dài 146, 531, 682 (dùng (a) và (c) đúng chỗ), 712, 808. |
| 13. Phụ lục C (R1) | 991–1005 | Thêm dòng "Cách rút" (số đều $U$, chọn $A_j=1$ khi $U<\pi_{\theta_j}(1)$, rồi số đều $U'$ cho nhấp), công thức cập nhật, độ lệch chuẩn chia $n-1$, phát lại rút có hoàn lại. |

## Điểm nhẹ

| Người rà | Dòng | Cách sửa hoặc lý do không áp dụng |
|---|---|---|
| R1 | 545 | Bước 4 Ví dụ 10.11 nêu $R(\tau_j)-b_j$. |
| R1 | 554 | Không áp dụng: câu cơ chế cho $c=10$ (người rà ghi "chỉ thêm nếu còn chỗ"); thân bài sát trần. |
| R1 | 5 | "chiết khấu" bỏ khỏi đoạn mở; đoạn sau Định nghĩa 10.1 viết "không nhân *hệ số chiết khấu* (discount factor)". |
| R1 | 3, 5 | Áp dụng (mục 12). |
| R1 | 97, 102 | Định nghĩa bài toán bandit đưa lên đầu Thiết lập. |
| R1 | 88 | Bảng §2: "(như $\eta_t$ của Bài 05; chỉ số $j$ vì $t$ là bước trong lượt)". |
| R1, R4 N5 | 249, 429, 645 | Bỏ ba câu trỏ vòng. |
| R1 | 635 | Định nghĩa "xung đột" ở câu mở §8. |
| R1, R5 N5 | 30–33 | Tiên quyết: thêm (T3), Định nghĩa 05.2, 05.7, 09.7, 09.10, Hệ quả 05.15; bỏ Thuật toán 05.11, Định nghĩa 09.14 (không dẫn); bỏ dòng "Chỉ cho bài tập" (Hệ quả 04.17, 06.2 chỉ dùng trong tệp bài tập; bù chữ). |
| R1 | 949 | $K\to C_\mu$. |
| R1 | 795, 797 | Áp dụng (mục 10). |
| R1 | 744, 816 | Áp dụng. |
| R1 | 363 | Thêm "$\partial J/\partial\theta_{s_0}=\tfrac14(1{,}7-1{,}8)$". |
| R1, R4 N15 | 223 | "tại $\theta$, một điểm trong của $\Theta$"; nhãn bước "**Bước 1: phần (a), …**" (Bổ đề 10.3, Mệnh đề 10.13). |
| R1 | 146 | Áp dụng (mục 12), thêm "theo tính chất tháp". |
| R1 | 15 | Áp dụng (mục 9). |
| R1 | 531 (chữ $\vartheta$) | Không đổi chữ: $\psi$ trùng trung bình oracle của Bài 05, các chữ Hy Lạp khác đều đã có nghĩa; $\vartheta$ đứng cạnh $b_\theta$ để đối chiếu. Câu được tách ba ý theo đề xuất. |
| R2 | 397; Ví dụ 10.7; $M$, $K$; $B$; $\Omega$; 595; Ví dụ 10.11 Bước 1 | Áp dụng (mục 2, 4, 10; 595: "tối thiểu hóa rủi ro thực nghiệm cho rủi ro trung bình $\frac1K\sum_kL_k$"; Ví dụ 10.11: "trong họ sigmoid, $J$ … tiến tới cận trên đúng $c+0{,}6$ khi $\pi_\theta(1)\to1$"). |
| R3 F4 | 724 | Áp dụng qua Nhận xét 10.14(ii) (Taylor/Hesse; Fisher = Hesse khi mô hình đúng). |
| R3 F5, F6 | 712 | "Với hai nhiệm vụ"; tiêu đề "— đọc thêm". |
| R3 F7 | | Áp dụng (mục 4). |
| R3 F8 | Ví dụ 10.9 | $\gamma\to\kappa$ ($\gamma$ là hệ số chiết khấu trong Sutton–Barto). |
| R3 F9, F10, F11, F12, F13 | | Áp dụng (mục 8, 11; N1). |
| R4 N1 | 15 | Áp dụng. |
| R4 N2 | 198, 298, 375, 397, 799 | Bỏ dấu hai chấm "tiết lộ"; 198 thay bằng số $0{,}2+0{,}6\,\pi_\theta(1\mid s_0)$. |
| R4 N3 | 991, 682 | Bỏ "không phải chứng minh" ở Phụ lục C; 682: "Mệnh đề 10.13 chỉ xét hai hàm bậc hai; nó không nói gì về phương pháp học liên tục cho mạng nơ-ron." |
| R4 N4 | 15, 120, 298, 447, 808 | Viết lại không lấy mục hay văn bản làm chủ ngữ ("ở §5, ta tính lại …"; "Bước 1–2 được viết … ở Phụ lục B"; "Chưa có cận hội tụ nào …"). 235 ("Ví dụ dưới đây bỏ …") giữ: câu dẫn ngắn, cùng kiểu Bài 09. |
| R4 N6 | | Áp dụng (mục 6); "lần lượt" ở 11, 61, 582 đổi; "hiệu năng" → "rủi ro"/"kết quả"; "quy tắc chọn" bỏ, chính sách giới thiệu ở câu dẫn Phần A. |
| R4 N7 | 600 | Áp dụng (mục 6). |
| R4 N8 | §1, 455, 818 | Nhãn **Thuật toán.** mở bằng danh từ; **Mục tiêu.** "…, cần làm lớn"; **Tài nguyên.** không danh từ hóa; **Khả tích.** "Các tập hữu hạn (mọi kì vọng hữu hạn)"; dòng "Phạm vi của UML Chương 21" bỏ khỏi §10. |
| R4 N9 | 332, 363, 840, 408 | Áp dụng. |
| R4 N10 | 123, 380, 399, 788, 525, 626 | Tiêu đề: "Hệ thống đề xuất với hai nội dung", "Thuật toán 10.6 (REINFORCE với một cập nhật mỗi lượt)", "Ví dụ 10.7 (Điểm dừng cực tiểu của mục tiêu chính sách)", "Ví dụ 10.17 (Hối tiếc tĩnh nhỏ và độ quên lớn)"; nhãn "Bước 3: một trường hợp phương sai tăng", "Bước 5: ma trận thứ hai". |
| R4 N11 | 756, 153, 155 | In nghiêng và tiếng Anh ở lần dùng đầu. |
| R4 N12 | Nhận xét 10.5, 10.16 | Thêm **Giả thiết.**/**Bảo đảm.** |
| R4 N13 | 498 | Tiêu đề cột $A=1$, $A=0$, $\operatorname{Var}\hat g_b$; cột đầu $\tfrac52$ (câu dẫn ghi $b=\tfrac52=J(\ln3)$); đo lại: không tràn. |
| R4 N14 | 205 | "chúng ta cần". |
| R4 N16 | 575, 628 | Áp dụng. |
| R4 N17 | 148, 168 | Tách đoạn kí hiệu trùng. |
| R4 N18 | 369, 718 | Bỏ nhãn ở 369; 718 "(hàm giả định)". |
| R4 N19 | 5 | Bỏ câu về §12. |
| R4 N20 | 523 | "sáu lần so với (i) và khoảng năm lần so với (ii)". |
| R5 N2 | 168, 537, 562; Ví dụ 10.8 | $R(\tau)$, $R(\tau_j)/4$; hằng số $b$ cục bộ ở Ví dụ 10.8, 10.11 giữ (không thêm chú thích, bù chữ). |
| R5 N3, N4, N6, N7, N8, N9, N10, N11 | | Áp dụng. |

## Kiểm sau sửa

- **Số liệu và script.** Không đổi thí nghiệm, nên không chạy lại script. Mọi số mới đã tính lại:
  - $\tfrac58+\tfrac1{8M}$;
  - phương sai theo tọa độ ở Ví dụ 10.10: $\tfrac{1619}{1600}=1{,}011875$, $\tfrac{11}{16}$, $\tfrac{79}{320}$, $\tfrac9{16}$, $\tfrac3{64}$, $\tfrac{197}{800}$, $\tfrac1{16}$, $\tfrac1{64}$, khớp các số người rà 1 đã tính;
  - tỉ số giảm phương sai $1{,}62125/0{,}324375\approx4{,}998$, ghi "khoảng năm lần".
- **Tham chiếu và cấu trúc.** `forward_refs.py` báo 0; khối `:::` 44/44.
- **Định dạng tệp.** Không có khoảng trắng cuối dòng, không có dòng trống kép, tệp kết thúc bằng một ký tự xuống dòng. Sync và `--check` OK.
- **Hiển thị.** Viewer qua HTTP (cổng 8783, đã tắt) và `file://`, ở 1600×900 và 390×844, với 9 `details` mở:
  - 1490 công thức, 0 `.katex-error`;
  - 0 lỗi trang, 0 yêu cầu hỏng;
  - 0 công thức hay bảng tràn; bản in 46 trang.
  - Ảnh chụp ở scratchpad `lec10/shots2/`.

## Chỗ cắt bù chữ và lý do chuyển sang phụ lục

**Chữ thêm.** Các sửa bắt buộc thêm khoảng 760 tiếng vào thân bài.

**Chỗ cắt.**
- Câu thứ ba của đoạn mở; câu về §12.
- Câu cuối §3; câu kết §6.
- Ba câu trỏ vòng.
- Bốn chỗ lặp ý "không nói về phương sai".
- Câu "Cả hai bài toán cần thêm vào Định nghĩa 01.5 …".
- Dòng "Chỉ cho bài tập" ở tiên quyết.
- Câu "Chẳng hạn …" ở cuối Nhận xét 10.17.
- Dòng "Phạm vi của UML" ở §10.
- Bước 4 của Ví dụ 10.11 rút còn một câu; số chi tiết đã có ở Phụ lục C.
- Câu chính sách Gauss ở Nhận xét 10.5 chuyển sang Phụ lục A, Bước 6.
- Rút gọn các câu ở §13.

**Chuyển sang phụ lục.** Bốn danh sách lời giải (f) chuyển sang Phụ lục D (khoảng 450 tiếng). Đây là chỗ chuyển duy nhất có thể làm mà không bỏ nội dung bắt buộc của quyết định gộp.

## Vòng 2 (2026-11-01)

Theo mục "Rà lại sau vòng 1" của `review-log.md`, áp dụng 15 điểm nhẹ của `reviews/6-ra-lai-toan.md` (R6) và `reviews/7-ra-lai-mach.md` (R7). Số dòng là số của bản trước vòng 2.

| Người rà | Dòng | Cách sửa |
|---|---|---|
| R6, R7 mục 2 | 406 | "một biến ngẫu nhiên $\xi_j$, với $\xi_1,\xi_2,\ldots$ độc lập cùng phân bố, ta được nguồn ngẫu nhiên và ánh xạ oracle như Định nghĩa 05.10 (Bài tập 10.3). Điều còn thiếu là (C): …". Bỏ "các biến đều" và "Trở ngại thật là". |
| R6 | 735 | "Khi $\lambda\Omega$ bằng ma trận Hesse của rủi ro cũ tại $w^{(1)}$, phạt bậc hai là phần bậc hai của khai triển Taylor quanh điểm cực tiểu $w^{(1)}$." Bỏ vế "bằng đúng phần tăng …" (cũng là chỗ cắt C2). |
| R6, R7 mục 7 | 626, 834 | "một quy ước gần với quy ước này cho độ quên âm"; §10: "Đổi quy ước đo có thể cho độ quên âm". |
| R7 mục 1 | 15 (khớp 206, 299) | Câu hỏi mở đầu nói rõ đạo hàm của trung bình theo $q$ bằng $0$, dù phần thưởng kì vọng đổi theo $q$. |
| R7 mục 3 | 9 | "phụ thuộc xác suất $q$". |
| R7 mục 4 | 862 | "cho cùng điểm cực tiểu". |
| R7 mục 5 | 845 | Tiêu đề Bài tập 10.4: "Độ chính xác phân lớp trung bình cuối cùng, …". Người viết bài tập cần dùng tiêu đề này. |
| R7 mục 6 | 576 | "Khi chính sách cố định, các lượt thỏa (T1), và bất đẳng thức Hoeffding cho một cận với xác suất cao." |
| R7 mục 8 | 866, Phụ lục D | Câu (f) và Phụ lục D cùng dùng "Phân lớp có giám sát (Bài 01–08)"; mục tiêu ghi "hàm lỗi lồi hoặc trơn thay cho hàm lỗi 0–1 (Bài 05–06, 08)". |
| R7 mục 9 | 879 | Lời giải (f) nêu ước lượng mật độ bỏ (T3) vì hàm lỗi log không bị chặn, và bỏ (T1) với chuỗi thời gian. |
| R7 mục 10 | 769 | Tách câu thí nghiệm sau "$\tfrac12(w^2+0{,}25)$". |
| R7 mục 11 | `ky-hieu.md` | Điều phối viên đã thêm; biên tập viên không sửa. |
| R7 mục 12 | 735, 772 | Giữ câu kết §8 ở 772; cắt vế lặp ở 735 (C2). |

**Chỗ cắt bù chữ** (đề xuất của R7):
- C1: dòng 5, bỏ "Phần B không có định lý tổng quát".
- C2: dòng 735, bỏ vế lặp.
- C3: dòng 614, bỏ vế "mỗi mẫu thỏa (T1) …".

**Số tiếng.** Thân bài 11 976 → 11 969; phụ lục 2 219 → 2 223.

**Kiểm tra.**
- `forward_refs.py` báo 0; khối `:::` 44/44.
- Sync và `--check` OK.
- Không có khoảng trắng cuối dòng, không có dòng trống kép, tệp kết thúc bằng một ký tự xuống dòng.
- Viewer chạy qua HTTP (cổng 8784, đã tắt) và `file://`, ở 1600×900 và 390×844: 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 tràn. Ảnh ở scratchpad `lec10/shots3/`.
