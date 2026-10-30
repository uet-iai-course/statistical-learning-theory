# Quyết định của điều phối viên sau hai lượt rà bài tập — Bài 02 (2026-10-30)

Căn cứ: `9-bai-tap-toan.md`, `10-bai-tap-su-pham.md`. Không có lỗi chặn bàn giao về toán; một lỗi chặn bàn giao về thuật ngữ ("tục biến"). Điều phối viên tính lại phát hiện nghiêm trọng của 02.1: $(1+x)^3/8-(1+3x^2)/4=(x-1)^3/8$; tại $\tau=1$: $5{,}7918<6{,}4259$; tại $\tau=-1$: $0{,}3515>0{,}3199$; $m=3$: $\tfrac14>e^{-1{,}5}\approx0{,}2231$ — đúng.

Mọi mục dưới đây **chấp nhận**, trừ khi ghi khác.

## Bắt buộc

- **B1 — Thuật ngữ** (rà soát 10). Bỏ "tục biến". Định nghĩa một lần: với mỗi $j$, $x\mapsto x_j$ là một biến, $x\mapsto\bar x_j$ là phủ định của biến đó; gọi chung $2p$ hàm này là các *biến hoặc phủ định của biến* (literal), tập $\mathcal U_p$; sau đó viết $u\in\mathcal U_p$, "tập $L\subseteq\mathcal U_p$"; tên bước "Thuật toán loại dần".
- **B2 — 02.1(d)–(e)** (rà soát 9). So sánh thêm tại $\tau=-1$, nêu hiệu $(x-1)^3/8$ và dấu của nó; (e): chứng minh Định lý 02.7(a) chỉ cần "$\le$", đúng khi $\tau>0$ ở ví dụ này, sai khi $\tau<0$; nêu vi phạm cụ thể của Định lý 02.7(b) tại $m=3$, $\epsilon=\tfrac12$ ($\tfrac14>e^{-1{,}5}$); sửa Gợi ý 3 theo. Kết luận về cỡ mẫu $738$ giữ.
- **B3 — Mục tiêu 2** (rà soát 10). Thêm 02.2(d): từ (a), dựng cận trên tin cậy một phía và khoảng tin cậy hai phía mức $1-\delta$ cho $\bar\mu_m$ (theo Định nghĩa 02.9, Hệ quả 02.10); tính hai bán kính với dữ liệu của (c) và $\delta=0{,}05$, so với bán kính khi dùng đoạn chung $[0,4]$; có gợi ý và lời giải từng bước. Người viết bài tập sửa đúng dòng này ở §10 của ghi chú: 02.2 "mục tiêu 1, 2".

## Trung bình

- **T1 — 02.10(c)** (9). Đề ghi rõ "dùng cận Markov ở Bước 1 của (a), với dấu '$<\delta$'"; giữ $40\,001$ và $10^8+1$; một câu nói cách $\epsilon\delta/2$ cho hệ số $4$.
- **T2 — 02.4 đề** (10). Xóa câu lộ đáp án của (c).
- **T3 — 02.5(c)** (9, 10). "Với xác suất ít nhất $\tfrac89$, $\hat p$ nằm trong $p\pm3\sqrt{p(1-p)/R}$"; bỏ "phải gần".
- **T4 — 02.8(d) Bước 4** (10). Bỏ "phải"; nói tốc độ của cận đủ; dẫn Nhận xét 02.18.
- **T5 — 02.7(c) Bước 3** (10). Bỏ khẳng định không chứng minh; nếu giữ, chuyển thành một "Câu hỏi:" mở rộng cuối đề, không kèm kết quả.

## Nhẹ

Chấp nhận mọi điểm nhẹ của hai báo cáo, gồm các cắt "nhẹ (độ dài)" của rà soát 10. Ghi thêm: 02.10 "mục tiêu 1, 6" ở dòng Mục tiêu (người viết sửa dòng tương ứng ở §10 của ghi chú). Điều phối viên đã sửa `outline.md` §4 (02.4 → mục tiêu 6).

**Độ dài:** sau khi thêm 02.2(d) và cắt, đích ≤ 9 500 tiếng (`wc -w`).
