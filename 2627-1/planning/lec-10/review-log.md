# Nhật ký rà soát — Bài 10: Gradient chính sách và học liên tục

Tệp nội bộ. Ghi tác tử, quyết định của điều phối viên, phát hiện rà soát và nguồn đã tham khảo.

Căn cứ bắt đầu (2026-10-31): người dùng giao lần lượt soạn ghi chú và bài tập Bài 07–10 theo blueprint, commit và push sau mỗi bài (xem `../lec-07/review-log.md`). Các yêu cầu rút ra từ Bài 01–09 áp dụng ngay từ bản thảo.

**Nguồn bổ sung.** Theo blueprint §F (cùng lý do như Bài 07): Sutton, Barto (2018), Chương 13 (đọc bắt buộc, chọn lọc), bản nháp do tác giả cung cấp, tải qua HTTP vì HTTPS của trang dùng chứng chỉ tự ký; Kirkpatrick và cộng sự (2017) (tùy chọn, EWC), bản arXiv:1612.00796v2. Cả hai ở `sources/supp/` (gitignore), ghi ở `sources/README.md`. UML §21.1–21.3 (thuật ngữ học trực tuyến, regret). Bước phân tích nguồn chạy song song với bước biên tập Bài 08: tác tử chỉ đọc repo, báo cáo ghi scratchpad, điều phối viên chép vào `source-analysis.md`.

Lời hứa cần giữ: `thuat-ngu.md` dòng "stability–plasticity trade-off" ("đánh đổi bền vững–mềm dẻo", không dùng "ổn định" ở đây); cầu nối cuối Bài 09 (khi viết xong; blueprint 9.6: người học điều khiển cách thu dữ liệu, hoặc phân bố thay đổi khi học); Bài tập 10.3 của blueprint nối Định lý 05.14.

## Tác tử

| Bước | Vai trò | Loại | Mô hình | Mức | Bằng chứng |
|---|---|---|---|---|---|
| 2026-10-31 · 1 | Phân tích nguồn Sutton–Barto Ch. 13, UML §21, Kirkpatrick và cộng sự (chỉ đọc repo; báo cáo ghi scratchpad) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-31 · 2 | Lập dàn ý (chỉ đọc repo; ghi dàn ý vào scratchpad, điều phối viên chép vào `outline.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-11-01 · 3 | Soạn ghi chú (ghi `lecture-note.md`, script thí nghiệm ngoài repo, `outline.md` §13) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-11-01 · 4 | Năm lượt rà độc lập (học viên; chính xác toán học; chuyên gia và trung thành nguồn; học thuật–sư phạm và `no-ai-slop` Detect; mạch và móc nối), chỉ đọc repo, báo cáo ghi vào scratchpad | general-purpose ×5 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-11-01 · 5 | Biên tập vòng 1 (cùng người viết; ghi `lecture-note.md`, script thí nghiệm, `bien-tap-vong-1.md`, `outline.md` §13) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-11-01 · 6 | Rà lại: toán học trên phần đã sửa (người rà 2); mạch, móc nối và văn phong trên phần đã sửa ±2 đoạn và ranh giới mục (người rà 5), chỉ đọc | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-11-01 · 7 | Biên tập vòng 2: 15 điểm nhẹ của hai lượt rà lại (cùng biên tập viên) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-11-01 · 8 | Soạn bài tập (ghi `exercises.md`, `bai-tap-ghi-chu.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-11-01 · 9 | Rà bài tập: toán học (người rà 2); sư phạm và `no-ai-slop` Detect (người rà 4); chỉ đọc, báo cáo ghi vào scratchpad | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-11-01 · 10 | Sửa bài tập theo hai lượt rà, và hai dòng §11 của ghi chú (cùng người soạn bài tập) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-11-01 · 10 | Rà lại toán bản sửa bài tập (cùng người rà toán) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-11-01 · 10 | Rà lại sư phạm bản sửa bài tập (cùng người rà sư phạm) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-11-01 · 10 | Sửa nhẹ cuối bài tập M1–M6 (cùng người soạn bài tập) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |

## Phân tích nguồn — quyết định của điều phối viên: **chấp nhận** (2026-10-31)

Báo cáo (85 dòng, 7 mục; script ở scratchpad `src10/`), điều phối viên chép vào `source-analysis.md`. Điều phối viên tự kiểm bandit hai hành động ($\theta=\ln3$, phần thưởng $3$ và $1$): $\pi_\theta(a_1)=\tfrac34$, $J'(\theta)=2\cdot\tfrac34\cdot\tfrac14=\tfrac38$; ước lượng REINFORCE nhận $0{,}75$ hoặc $-0{,}75$, kì vọng $\tfrac38$, phương sai $\tfrac{27}{64}$; với giá trị nền $b=J=2{,}5$, phương sai $\tfrac3{16}$. Khớp. Kiểm trên PDF: UML §21.1 bắt đầu tr. 288, §21.2 tr. 294; điều phối viên đã sửa `sources/uml-sections.md`.

Quyết định cho dàn ý và bản thảo:

1. **Kí hiệu:** lợi nhuận $R(\tau)$ luôn kèm đối số (khác $R$ của Bài 05); tổng phần thưởng từ bước $t$ viết **$R_{\ge t}=\sum_{t'=t}^{H-1}r_{t'}$** (không dùng $G_t$; không dùng $u$ cho chỉ số vì $u$ là đối tượng so sánh của regret); ma trận đánh giá **$\mathrm{acc}_{k,i}$** (không dùng $a_{t,i}$); tham số sau nhiệm vụ $k$: $w^{(k)}$; ma trận Fisher $\mathcal I_A$; độ lệch chuẩn của chính sách Gauss $\omega$; $J(\theta)$, $b_t(\cdot)$, $P(s'\mid s,a)$ luôn kèm đối số; phân bố trạng thái đầu $\mu_0$; lịch sử $\mathcal F_t$ (như Bài 05); tầm nhìn $H$ (chữ nghiêng, khác $\mathrm H$ entropy của Bài 09). Thuật ngữ theo `thuat-ngu.md` §12: "giá trị nền" (baseline; điều phối viên chốt), "tổng phần thưởng từ bước $t$", "chuyển đổi xuôi/ngược", "độ chính xác trung bình cuối cùng", "đánh đổi bền vững–mềm dẻo". Điều phối viên đã sửa ba dòng §12 và đóng câu hỏi mở về "giá trị nền".
2. **Thiết lập:** MDP tầm nhìn hữu hạn không chiết khấu, trạng thái và hành động hữu hạn (đổi chỗ đạo hàm–kì vọng là đạo hàm tổng hữu hạn; nêu điều kiện cho trường hợp tổng quát và nối Bài 09); quỹ đạo dạng đẳng thức (không có $\propto$, không cần phân bố đi theo chính sách); một câu so với Sutton–Barto (lượt kết thúc ngẫu nhiên, định lý với $\propto$), trung tính.
3. **Ví dụ và phản ví dụ** (số đã kiểm ở báo cáo): bandit (phương sai $\tfrac{27}{64}$, $\tfrac3{16}$, $0$ với $b^*=\tfrac32$, $\tfrac{147}{64}$ với $b=5$ — giá trị nền không luôn giảm phương sai); MDP $H=2$ (gradient khớp liệt kê và sai phân hữu hạn); bỏ giả thiết: luật chuyển phụ thuộc $\theta$ (sai dấu), giá phụ thuộc $\theta$, giới hạn chính sách tất định, điểm dừng là cực tiểu khi tham số dùng chung; tổng phần thưởng từ bước $t$ có thể tăng phương sai; ứng dụng đề xuất nội dung (dịch phần thưởng $c=10$); Mệnh đề 10.5 với năm giá trị $\lambda$; hai ma trận đánh giá (quy ước làm đổi dấu); regret thấp nhưng quên (OGD); phát lại hữu hạn $\alpha^2/(2M)$; cận Hoeffding cho đánh giá một chính sách cố định ($0{,}0859$). Sutton–Barto §2.8 có giá trị nền lệch thật (trung bình chạy gồm phần thưởng hiện tại): dùng làm ví dụ nếu vừa chữ, dẫn theo mục.
4. **Kirkpatrick:** EWC chỉ ở mức động cơ và phương pháp (phạt bậc hai có trọng số); không gán cho bài báo công thức Fisher mà bài báo không viết; "replay" trong thí nghiệm Atari của bài báo là phát lại kinh nghiệm của DQN, không phải phát lại nhiệm vụ cũ (một câu nếu dẫn).
5. **Độ đo học liên tục:** không nguồn nào định nghĩa; giữ cách nói của blueprint ("các bài báo dùng quy ước khác nhau"), nêu quy ước của học phần.
6. **Bài tập:** sáu bài gốc blueprint 10.6 (bài 10.3: điều kiện (C) hỏng; (G1) giữ được hình thức với $\tau=g(\theta,U)$; (G2) khi phần thưởng và gradient log bị chặn); UML 21.5 (online-to-batch), 21.4 tùy chọn; bài tổng kết của blueprint 10.7 đặt trong §12 (câu hỏi cuối buổi) hoặc bài tập.
7. **Tổng kết học phần** (blueprint 10.7) ở §12; không phát biểu định lý học liên tục phổ quát. Thân ≤ 12 000, phụ lục ≤ 3 000. Tiêu đề "Bài 10 — Gradient chính sách và học liên tục" (khớp thẻ chỉ mục).

## Dàn ý — quyết định của điều phối viên: **chấp nhận** (2026-10-31)

Dàn ý (590 dòng) do tác tử lập dàn ý ghi vào scratchpad `outline10/outline.md` khi bước soạn ghi chú Bài 09 đang ghi repo; điều phối viên chép vào `outline.md`. 17 khối 10.1–10.17 (**Bổ đề 10.3 = Lemma 10.1** [F]; **Định lý 10.4 = Thm 10.2** [F]; **Mệnh đề 10.7 = Prop 10.3** [S], chi tiết Phụ lục B; **Hệ quả 10.8 = Cor 10.4** [F]; **Mệnh đề 10.13 = Prop 10.5** [F]; Thuật toán 10.6 REINFORCE; Định nghĩa 10.1, 10.2, 10.10, 10.11, 10.12, 10.15; Nhận xét 10.5, 10.9, 10.14, 10.16, 10.17), Ví dụ 10.1–10.17, Bài tập 10.1–10.9 (06 gốc; 10.7 gốc thêm; 10.8 = UML 21.5; 10.9 = UML 21.4 tùy chọn), phụ lục A–C, thí nghiệm `exp_lec10_pg_replay.py` (REINFORCE 100 hạt giống; phát lại 20 hạt giống). Điều phối viên đọc mục 1–2, 9–10, 12 và kiểm: bandit $\tfrac38$ (đã kiểm ở bước nguồn); cận Hoeffding của Ví dụ 10.12 với lợi nhuận trong $[0,4]$: $4\sqrt{\ln40/2000}\approx0{,}1718$ (bản phân tích nguồn dùng miền $[0,2]$ cho $0{,}0859$; dàn ý đúng với MDP của Ví dụ 10.2). Khớp.

Quyết định về các điểm mở (mục 12.2): (1) tiêu đề §12 "Câu hỏi cuối buổi và tổng kết học phần" (bài cuối, không có bài sau); (2) cho phép phần thưởng ngẫu nhiên bằng một câu sau Định nghĩa 10.1; (3) không đặt tên $V$, $Q$; (4) chuyển đổi xuôi với mốc $\mathrm{acc}^\circ$ nêu rõ là quy ước của học phần; (5) người viết tránh chữ trùng ($\hat g_j$, $h_t$, $u$, kí hiệu nhiễu) và ghi §13; (6) Nhận xét 10.16 giữ thành khối, ngắn, dẫn UML §21.3 theo mục; (7) Bài tập 10.7 và thuật ngữ "tối ưu Pareto" chấp nhận (tiếng Anh ở lần đầu); (8) không đưa ví dụ chính sách Gauss vào ghi chú. Bài tập 10.3 cần một mở rộng lồi vì (C) của Định lý 05.14 đòi $F$ lồi trên $\mathbb R^p$ — người soạn bài tập xử lý. Điều phối viên đã thêm 26 dòng thuật ngữ vào `thuat-ngu.md` §12 và 18 dòng kí hiệu vào `ky-hieu.md`. Người viết ghi chú bắt đầu sau khi Bài 09 và vòng sửa 2 của Bài 08 xong (mỗi lúc một người ghi repo).

## Bản thảo ghi chú — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-11-01)

Bản thảo 1 017 dòng; thân bài 11 982 tiếng, phụ lục 1 652. 17 khối 10.1–10.17, Ví dụ 10.1–10.17, §11 liệt kê Bài tập 10.1–10.9, §12 "Câu hỏi cuối buổi và tổng kết học phần", Phụ lục A–C; 44 khối mở và đóng. Kiểm tra do điều phối viên chạy: `forward_refs.py` 0; không có "Mục này", "rõ ràng", "dễ thấy", "Đáp án", "hãy", "vô nghĩa", "bằng chứng thí nghiệm"; điều phối viên chạy lại `exp_lec10_pg_replay.py --part all` (1,5 giây): REINFORCE $c=10$ không giá trị nền $0{,}509\pm0{,}498$, $49\%$ dưới $0{,}5$; có giá trị nền $0{,}969$; phát lại $L_A$ $0{,}624$, $0{,}331$, $0{,}256$, $0{,}252$; khớp ghi chú. Chấp nhận các sai khác người viết báo (`outline.md` §13.3): các mục cắt (1), (2), (4)–(7); Nhận xét 10.5 thêm khả vi liên tục và phần thưởng bị chặn; đổi chữ tránh trùng; $b_t(\mathcal F_t)$; Nhận xét 10.16 với $w_1$ tổng quát; tiêu đề Bài tập 10.2, 10.3, 10.5, 10.7 chỉnh theo quy tắc. Điểm giao người rà: Phụ lục A Bước 6 (hàm trội cho chính sách Gauss) mới là phác thảo; "người học" ở đoạn dẫn (một chữ một nghĩa, như Bài 09). Bản đóng băng: scratchpad `lec10-draft-frozen.md` (SHA-256 bắt đầu `74d96d8878c447a0`).

## Năm lượt rà — quyết định của điều phối viên: **yêu cầu sửa** (2026-11-01)

Báo cáo trong `reviews/1-hoc-vien.md` (0/2/9/16), `2-toan-hoc.md` (0/1/2/7; mọi kết quả chứng minh lại đúng, mọi số khớp), `3-chuyen-gia-nguon.md` (0/0/3/10; §E 10/12; không chép nguồn; ba lời hứa được giữ), `4-hoc-thuat-van-phong.md` (0/0/9/20), `5-mach.md` (0/0/5/11; `forward_refs.py` 0; 30 số hiệu đúng). Không có lỗi chặn bàn giao. Hai phát hiện nghiêm trọng: số thí nghiệm ở Ví dụ 10.16 thuộc mô hình khác với mô hình của ví dụ; câu "tiến tới" về hối tiếc sai (Ví dụ 10.17 có hối tiếc âm). Quyết định gộp: `reviews/0-quyet-dinh.md` (N1, N2, 13 mục trung bình, điểm nhẹ). Điều phối viên sửa hai dòng `thuat-ngu.md` (điểm so sánh; "độ chính xác phân lớp") để hết mâu thuẫn người rà 4 chỉ ra.

## Biên tập vòng 1 — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-11-01)

Biên tập viên áp dụng N1, N2, 13 mục trung bình và các điểm nhẹ (`bien-tap-vong-1.md`; bốn mục không áp dụng có lý do, chấp nhận). N1: giữ thí nghiệm; Kết luận Ví dụ 10.16 chỉ dùng số của chính ví dụ ($\tfrac58+\tfrac1{8M}$ giảm về $\tfrac58$, không về $\min L_A=\tfrac12$), số thí nghiệm trong một câu riêng nêu rõ mô hình $\tfrac12(w^2+0{,}25)$; điều phối viên kiểm: $L_A(\tfrac12)=\tfrac12(\tfrac14+1)=\tfrac58$, phần thêm $\alpha^2/(2M)=\tfrac1{8M}$ với $\alpha=\tfrac12$. Sai khác cấu trúc (chấp nhận): lời giải câu (f) của câu hỏi cuối buổi (tổng kết học phần) chuyển sang Phụ lục D mới để giữ trần chữ; câu (f) vẫn ở §12. Thân bài 11 976 tiếng, phụ lục 2 219. `forward_refs.py` 0. Điều phối viên đã sửa dòng $\mathcal F_t$ của `ky-hieu.md`. Diff `lec10-r1.udiff` giao rà lại: toán (người rà 2), mạch và văn phong (người rà 5).

## Rà lại sau vòng 1 — quyết định của điều phối viên: **chấp nhận, sửa nhẹ** (2026-11-01)

Rà lại toán (`reviews/6-ra-lai-toan.md`): 10/10 phát hiện cũ ✓ (kể cả N1); mọi phần toán đã đổi đúng, số mới khớp, Phụ lục C khớp script. Mới 0/0/0/3 (dòng 406 hai câu tự mâu thuẫn — nói rõ các $\xi_j$ độc lập cùng phân bố, trở ngại là (C); dòng 735 Taylor–Hesse khớp khi $\lambda\Omega$ là ma trận Hesse; dòng 626, 834 "khác dấu/đổi dấu" sai vì hai giá trị độ quên là $0$ và $-0{,}03$). Rà lại mạch (`reviews/7-ra-lai-mach.md`): 5/5 trung bình và 10/11 nhẹ của người rà 5 ✓; 8/9 trung bình của người rà 4 ✓; `forward_refs.py` 0; mạch §12 → Phụ lục D ổn, tổng kết đủ Bài 01–09. Mới 0/0/0/12 (dòng 206, 299; 406; 9; 862; 879; 845 tiêu đề Bài tập 10.4; 769; câu kết §8; câu dẫn Ví dụ 10.12; câu (f) so với tiêu đề Phụ lục D). Điều phối viên thêm dòng $\Lambda$, $L_{\mathrm{buf}}$ vào `ky-hieu.md`. Gửi biên tập viên sửa 15 điểm nhẹ trong trần chữ; điều phối viên đọc diff, không rà lại thêm.

## Kiểm định cuối và công bố ghi chú — Bài 10 (2026-11-01)

Vòng 2 (`bien-tap-vong-1.md` mục "Vòng 2"): 15 điểm nhẹ của hai lượt rà lại, bù chữ bằng ba chỗ cắt người rà 5 đề xuất. Điều phối viên đọc toàn bộ diff: đúng các quyết định. Thân bài 11 969 tiếng, phụ lục 2 223.

Kiểm định do điều phối viên chạy (`final06/final05.py`, `idx10.py`; cổng 8772), qua HTTP và `file://`, ở 1600×900 và 390×844: 1 494 công thức, 9 khối thu gọn, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng, 0 tràn, độ rộng 375 px ở 390; bản in A4 46 trang; cảnh báo CSP duy nhất (chỉ HTTP) do `reloadserver`. `forward_refs.py` 0. Thẻ Bài 10 liên kết ghi chú; mở từ chỉ mục qua HTTP và `file://` đúng tiêu đề. Gói `material-local-data.js` khi commit dựng bằng `bundle_head.py`.

**Trạng thái:** ghi chú Bài 10 hoàn tất; commit và push. Việc tiếp theo: bài tập Bài 10 (dùng tiêu đề mới của Bài tập 10.4 và hướng giải Bài tập 10.3 qua các $\xi_j$ độc lập cùng phân bố).

Commit `4864efe`.

## Bài tập — bắt đầu (2026-11-01)

Giao một người viết soạn `exercises.md` theo `outline.md` §4 và §11 của ghi chú (9 bài: 10.1–10.6 gốc theo blueprint 10.6; 10.7 gốc thêm, áp mẫu tổng kết cho hai thiết lập khác; 10.8 = UML 21.5; 10.9 = UML 21.4 tùy chọn). Bài UML tự giải trước rồi mới đối chiếu bản lời giải (chương 21). ≤ 10 000 tiếng.

## Bài tập — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-11-01)

`exercises.md`: 9 bài (10.1–10.7 gốc; 10.8 = UML 21.5, 10.9 = UML 21.4 tùy chọn; số bài đối chiếu PDF tr. 305–306), 9 788 tiếng, 36 khối. Người soạn tự giải hai bài UML trước khi mở bản lời giải (01:37:28 so với 01:37:45); ghi chỗ hổng của bản lời giải ở `bai-tap-ghi-chu.md`. Sai khác với dàn ý §4 (chấp nhận để rà): các ý trùng ghi chú thay bằng biến thể (10.2(a) độ chệch của giá trị nền phụ thuộc hành động; 10.2(d) chứng minh công thức entropy, $0{,}5623$ tại $\theta=\ln3$; 10.4(b), (c) bỏ ý "khác dấu" sai của dàn ý, thay bằng bất đẳng thức giữa độ quên trung bình và chuyển đổi ngược, khoảng tin cậy đồng thời; 10.5(d) giá trị nhỏ nhất $\tfrac25$; 10.6 phần tính trên số đã chạy với sai số chuẩn theo hiệu; 10.3 theo §13.6: trở ngại là (C), (G2) với $G=H^2C_rC_\pi$, hai phản ví dụ cho dạng $\psi\in\partial F$ của (G1)). Kiểm tra do điều phối viên chạy: không có tệp lạ ở gốc repo; `sync --check` OK; 72 dòng `:::`. Bản đóng băng: scratchpad `lec10-ex-frozen.md` (SHA-256 bắt đầu `eebf555da282ea49`).

## Rà bài tập — quyết định của điều phối viên: **yêu cầu sửa** (2026-11-01)

Rà toán (`reviews/9-bai-tap-toan.md`): 0/0/1/3; tự giải lại chín bài, mọi đáp số đúng; script tái lập; đề UML trung thành; lời giải không chép bản lời giải. Rà sư phạm (`reviews/10-bai-tap-su-pham.md`): 0/0/3/19. Quyết định gộp: `reviews/11-quyet-dinh-bai-tap.md` (7 mục, điểm nhẹ; cho phép sửa hai dòng §11 của ghi chú).

## Sửa bài tập theo quyết định — điều phối viên đọc diff: **chấp nhận để rà lại** (2026-11-01)

Người soạn áp dụng 7 mục và N1–N19 (N12 một phần, lý do ở `bai-tap-ghi-chu.md` §8); tệp 9 961 tiếng; §11 của ghi chú đổi đúng hai dòng (10.3: mục tiêu 1, 5; 10.9: "Tùy chọn: …"). Điều phối viên kiểm lại 10.1(f): $\int_0^\infty\Lambda=10/\theta_0$, $\int_0^1(1-a)e^{-a}da=e^{-1}$; 10.4(c) khoảng $[-0{,}2652;-0{,}1148]$; 10.7 tỉ lệ bán kính $6/4$. Giao rà lại toán và sư phạm trên diff.

## Rà lại bài tập — quyết định: **chấp nhận, kèm sửa nhẹ cuối** (2026-11-01)

Rà lại toán (`reviews/12-kiem-lai-toan-bai-tap.md`): đạt; bốn mục toán đóng; 10.1(f), Kiểm tra lại của 10.7, khoảng 10.4(c) đúng; một điểm nhẹ (dòng 561). Rà lại sư phạm (`reviews/13-kiem-lai-su-pham-bai-tap.md`): đạt; 21/22 phát hiện cũ đóng, N12 áp dụng một phần với lý do chấp nhận; sáu điểm nhẹ mới M1–M6 (M2 trùng điểm của rà toán). Quyết định: người soạn áp dụng M1–M6 theo câu sửa đề xuất, giữ ≤ 10 000 tiếng (cắt bù nếu cần); không cần rà lại thêm, điều phối viên đọc diff.

## Sửa nhẹ cuối và kiểm tra cuối bài tập — quyết định: **chấp nhận** (2026-11-01)

Người soạn áp dụng M1–M6 (M2 theo câu của rà toán; M5 định nghĩa $\hat g_\theta(\tau')$ tại chỗ); tệp 9 989 tiếng ≤ 10 000; điều phối viên đọc diff: không mất bước, viện dẫn mới "Định nghĩa 10.10" đúng (mục Đánh giá nêu mẫu kiểm tra độc lập với dữ liệu huấn luyện). Kiểm tra cuối của điều phối viên (Playwright, cổng 8772 và `file://`, 1600×900 và 390×844, in): 1 248 công thức, 0 `.katex-error`, 0 tràn, 0 lỗi trang, 0 yêu cầu hỏng; ảnh đã xem. `index.html`: thẻ Bài 10 mở bài tập, kiểm bằng cả hai cách mở. §11 ghi chú Bài 10 đổi đúng hai dòng (10.3, 10.9). Bàn giao.
