# Rà soát 3 — Chuyên gia lý thuyết học và trung thành nguồn, Bài 10 (bản đóng băng `lec10-draft-frozen.md`)

Người rà chỉ đọc repo, không commit. Số dòng theo bản đóng băng. Văn phong và `no-ai-slop` thuộc người rà 4; các câu đề xuất dưới đây viết theo `van-phong.md`.

## Tổng kết theo mức

- **Chặn bàn giao:** 0.
- **Nghiêm trọng:** 0.
- **Trung bình:** 3 (F1: Mệnh đề 08.12 được áp dụng ngay sau câu nói khác Định nghĩa 05.10; F2: diễn giải hối tiếc dưới tuyến tính là "tiến tới", trái với hối tiếc âm của chính Ví dụ 10.17; F3: §13 không nói REINFORCE của Sutton–Barto dùng $G_t$, khác Thuật toán 10.6).
- **Nhẹ:** 10 (F4–F13).

Đánh giá chung: thiết lập MDP (tầm nhìn $H$ cố định, không chiết khấu, $\mu_0$, $P$ không phụ thuộc $\theta$, chính sách ngẫu nhiên khả vi) đúng blueprint 10.2. Bổ đề 10.3, Định lý 10.4, Mệnh đề 10.7, Hệ quả 10.8 và Mệnh đề 10.13 đủ và đúng độ sâu. REINFORCE được nói là ước lượng không chệch có điều kiện, không có khẳng định hội tụ (dòng 268, 413, 808, 906). (T1) bị vi phạm được nói đúng cho cả hai phần (dòng 79, 595). Giao thức học liên tục có đủ nhiệm vụ, bộ nhớ, truy cập dữ liệu cũ, định danh nhiệm vụ và mẫu kiểm tra độc lập. Các độ đo được ghi là quy ước của học phần (dòng 607, 908), và bài không có định lý học liên tục tổng quát. Học trực tuyến, học liên tục và dịch chuyển phân bố được tách riêng (Nhận xét 10.17). Ví dụ 10.17 phân biệt hối tiếc với độ quên. Thí nghiệm được ghi là kết quả thí nghiệm, có nhiều lần chạy và mẫu kiểm tra riêng (Phụ lục C). Không chép hay dịch sát nguồn nào. Không có số định lý của nguồn được trình bày như kết quả của học phần. Các khác biệt với Sutton–Barto và Kirkpatrick được nói trung tính và đúng, trừ F3 và F9.

Đã tự kiểm: hối tiếc Ví dụ 10.17 ($-116{,}967$, $w_{T+1}\approx1$; $\eta_t=1/t$: $0{,}188$, $w_{T+1}=\tfrac12$); cận $BG\sqrt T$ của Nhận xét 10.16 khớp UML Định lý 21.15 với $w_1=0$; bất đẳng thức hàm trội Gauss ở Phụ lục A Bước 6 ($(a-\mu)^2\ge a^2/2-\mu^2$ cho thừa số $e^{K^2/(2\omega^2)}e^{-a^2/(4\omega^2)}$) đúng; mọi số hiệu Bài 01–09 được dẫn (27 khối) tồn tại và đúng tên.

## Bảng §E (danh sách kiểm bắt buộc): 10/12 đạt, 2 đạt một phần

| # | Mục §E | Kết quả | Ghi chú |
|---|---|---|---|
| 1 | Một bảng kí hiệu, không dùng lại chữ | một phần | $K$ (số nhiệm vụ, §2) dùng lại làm hằng số chặn ở Phụ lục A Bước 6; $M$ (ngân sách bộ nhớ) dùng lại cho hàm trội ở Nhận xét 10.5 và Phụ lục A; $h$ là số gia ở Phụ lục A Bước 1 (F7) |
| 2 | Mỗi kết quả nêu cơ chế lấy mẫu, hàm lỗi, đối tượng so sánh, nguồn ngẫu nhiên, loại bảo đảm | đạt | Mỗi khối có "Giả thiết."/"Bảo đảm."; Định lý 10.4 ghi "Đồng nhất thức … không có mẫu"; Mệnh đề 10.13 "Tất định" |
| 3 | Chú thích chỗ dùng giả thiết; ít nhất một ví dụ hỏng | đạt | Ví dụ 10.3 (giá phụ thuộc $\theta$), 10.6 (luật chuyển phụ thuộc $\theta$, ngược dấu), 10.7, 10.9, 10.10 Bước 2, 10.15 |
| 4 | Kết quả là phát biểu của học phần; UML theo mục | đạt | UML §21.3, Chương 21, Bài tập 21.4, 21.5 (đã kiểm ở source-analysis); không dùng "Định lý 21.15" |
| 5 | Phân biệt bảo đảm cho lớp mô hình và cho một thuật toán | đạt | Nhận xét 10.16 là bảo đảm cho thuật toán; Định lý 10.4 là đồng nhất thức về mục tiêu; dòng 413 |
| 6 | Nêu bảo đảm kiểm soát đại lượng nào | đạt | Dòng 808 liệt kê loại bảo đảm; dòng 768 tách hối tiếc, rủi ro vượt mức, độ quên (nhưng xem F2) |
| 7 | Không chuyển kết quả hàm lỗi bị chặn sang hàm lỗi bình phương hay log | đạt | Ví dụ 10.12 dùng $R\in[0,4]$; Ví dụ 10.16 không dùng cận cho hàm lỗi bị chặn |
| 8 | Không chuyển cận lồi sang RL nếu không có lập luận mới | một phần | Dòng 397 và Ví dụ 10.7 loại Định lý 05.14 đúng, nhưng Mệnh đề 08.12 được áp dụng (dòng 410) ngay sau câu "Khác Định nghĩa 05.10" (dòng 397), không có câu nối (F1) |
| 9 | Một ví dụ số và một câu hỏi cuối buổi | đạt | Ví dụ 10.4, 10.8, 10.12, 10.14; §12 (a)–(f) |
| 10 | Tách bài gốc và bài UML | đạt | §11: bảy bài gốc, hai bài UML có số hiệu |
| 11 | Chứng minh dài ở phụ lục | đạt | Phụ lục A, B |
| 12 | Thí nghiệm có mẫu kiểm tra và nhiều lần chạy; đường cong không phải chứng minh | đạt | Phụ lục C: 100 và 20 hạt giống, 10 000 quan sát kiểm tra; giải thích vì sao phần REINFORCE không cần mẫu kiểm tra; dòng 991 |

## Trang nguồn đã đọc

- **Sutton–Barto** (`sources/supp/sutton-barto-2018-draft.pdf`, trang PDF): 57–59 (§2.8), 343–353 (§13.1–13.5: tr. 346 trạng thái đầu $s_0$ không ngẫu nhiên, $\gamma=1$ trong văn bản; tr. 348 (13.5) với $\propto$, hằng số tỉ lệ là độ dài lượt trung bình, phân bố theo chính sách $\mu$; tr. 350 khung REINFORCE cập nhật trong vòng lặp theo bước, dùng $G$; tr. 351 "baseline can be any function, even a random variable, as long as it does not vary with $a$", khẳng định hội tụ; tr. 353 "local minimum"), 357–360 (§13.7, Bài tập 13.5, §13.8).
- **UML** (trang PDF): 287–289 (§21.1, tr. 288 không giả thiết thống kê, đối thủ), 294–295 (§21.2, hối tiếc), 300–302 (§21.3, OGD có chiếu, $w^{(1)}=0$, Định lý 21.15), 305–306 (§21.7).
- **Kirkpatrick và cộng sự** (`sources/supp/kirkpatrick-2017.pdf`): tr. 1–8 (tr. 1 phát lại bằng bộ nhớ theo lượt tỉ lệ số nhiệm vụ; tr. 3 xấp xỉ Laplace theo MacKay, hậu nghiệm Gauss, độ chính xác là đường chéo ma trận Fisher, (3), tổng hai phạt bậc hai; tr. 4 so với L2; tr. 5 tính Fisher ở mỗi lần đổi nhiệm vụ, phát lại kinh nghiệm của DQN; tr. 6–7 điểm yếu của ước lượng điểm).
- **Repo:** `sources/blueprint.md` §A, cuối Bài 9, Bài 10, §C–§F; `CLAUDE.md` học phần; `lec-10/source-analysis.md`, `outline.md` §13.3, `review-log.md`; `thuat-ngu.md` §12; `ky-hieu.md`; ghi chú Bài 01 (T1, T2), 05 (Định nghĩa 05.10, Mệnh đề 05.13), 08 (Mệnh đề 08.12), 09 (§12, dòng 849).

## Lời hứa

- **Cầu nối cuối Bài 09** (lec-09 dòng 849): hai câu hỏi, hành động rời rạc quyết định quan sát và phân bố thay đổi trong lúc học. Dòng 3–5 của Bài 10 nhắc lại và trả lời đúng hai câu này, với hành động hữu hạn. **Giữ.**
- **`thuat-ngu.md` "đánh đổi bền vững–mềm dẻo"**: dòng 682 định nghĩa "tính bền vững", "tính mềm dẻo" và đánh đổi, kèm câu phân biệt với tính ổn định của Bài 06, 08. **Giữ.**
- **Bài tập 10.3 của blueprint (Định lý 05.14)**: dòng 397, Ví dụ 10.7 Kết luận, §11 mục 3, §12(f). **Giữ**, nhưng xem F1 về sự nhất quán với hướng giải đã chốt ((G1) giữ được khi viết lượt dưới dạng $\tau=g(\theta,U)$).

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | dòng 397; Ví dụ 10.7 Kết luận (dòng 410) | F1. Dòng 397 nói nguồn ngẫu nhiên "khác Định nghĩa 05.10" vì phân bố phụ thuộc $\theta_j$. Ví dụ 10.7 lại áp dụng Mệnh đề 08.12, mà giả thiết của nó dùng "lịch sử $\mathcal F_{t-1}$ như Định nghĩa 05.10". Người đọc thấy hai câu mâu thuẫn. Hướng giải Bài tập 10.3 đã chốt (review-log, QĐ 6) lại nói (G1) giữ được khi viết $\tau=g(\theta,U)$ | lec-08 dòng 780: "Với lịch sử $\mathcal F_{t-1}$ như Định nghĩa 05.10, $\mathbb E[g_t\mid\mathcal F_{t-1}]=\nabla F(w_t)$…"; draft dòng 397: "Khác Định nghĩa 05.10, phân bố của nguồn ngẫu nhiên ở cập nhật $j$ phụ thuộc $\theta_j$ (Bài tập 10.3)" | Dòng 397, thay câu thứ hai bằng: "Nếu coi quỹ đạo là nguồn ngẫu nhiên thì phân bố của nó phụ thuộc $\theta_j$, khác Định nghĩa 05.10; Bài tập 10.3 viết lại mỗi lượt thành hàm của $\theta_j$ và một biến độc lập với các lượt trước." Dòng 410: "Mệnh đề 08.12 chỉ dùng kì vọng có điều kiện theo lịch sử $\tau_1,\ldots,\tau_{j-1}$, nên áp dụng cho $F=-J$ …" (khoảng +22 tiếng) |
| trung bình | dòng 768 | F2. "khi nó tăng chậm hơn $T$, hàm lỗi trung bình theo thời gian tiến tới hàm lỗi trung bình của điểm cố định tốt nhất". Hối tiếc dưới tuyến tính chỉ cho cận trên: hàm lỗi trung bình không vượt quá hàm lỗi trung bình tốt nhất cộng một lượng tiến về $0$. Ví dụ 10.17 Bước 3 có hối tiếc $-116{,}97$, tức hàm lỗi trung bình nhỏ hơn hẳn và không "tiến tới" | UML tr. 294 (21.2): "grows sublinearly", định nghĩa bằng cận trên; draft dòng 795 | "… khi nó tăng chậm hơn $T$, hàm lỗi trung bình theo thời gian không vượt quá hàm lỗi trung bình của điểm cố định tốt nhất cộng một lượng tiến về $0$." (+5 tiếng) |
| trung bình | §13 "Quan hệ với nguồn", bullet "Thuật toán và giá trị nền" (dòng 906) | F3. §13.3 của Sutton–Barto là bài đọc trước buổi học. Ở đó REINFORCE (13.6) và khung tr. 350 dùng $G_t$, tức tổng phần thưởng từ bước $t$, không dùng tổng cả lượt $R(\tau)$ như Thuật toán 10.6. §13 chỉ nêu khác biệt về thời điểm cập nhật và về tên kí hiệu. Người học đọc nguồn sẽ thấy hai thuật toán cùng tên nhưng khác ước lượng | SB tr. 349–350: "$G\leftarrow\sum_{k=t+1}^TR_k$ ($G_t$); $\theta\leftarrow\theta+\alpha\gamma^tG\nabla\ln\pi$"; draft dòng 391 dùng $R(\tau_j)$ | Thêm vào bullet: "…cập nhật tham số ở từng bước trong lượt và dùng $G_t$, tức ước lượng của Mệnh đề 10.7(b); Thuật toán 10.6 dùng $R(\tau)$ và cập nhật sau mỗi lượt." (+15 tiếng) |
| nhẹ | Nhận xét 10.14(i)–(ii), Ví dụ 10.15 Bước 2–3 | F4. Nhận xét 10.14 định nghĩa $\Omega$ của EWC bằng đường chéo ma trận Fisher. Ví dụ 10.15 dùng đường chéo ma trận Hesse mà không có câu nối. Câu về "Hesse khi mô hình đúng" đã bị cắt theo quyết định (outline §13.3 mục 3), nên người đọc không biết vì sao dùng Hesse thay cho Fisher | source-analysis dòng 17 (tính chất (a) của Fisher chỉ đúng khi mô hình đúng); draft dòng 724 | Ở Ví dụ 10.15 Bước 3, sau "Đường chéo của ma trận Hesse", thêm "(vai trò của $\Omega$ trong Định nghĩa 10.12; với hàm lỗi bình phương ở đây không có ma trận Fisher)" — hoặc chấp nhận vì Định nghĩa 10.12 cho phép mọi $\Omega$ đường chéo (+16 tiếng) |
| nhẹ | Nhận xét 10.14(i), dòng 712 | F5. "EWC … là chính quy hóa tham số với $\Omega$ là đường chéo của ma trận Fisher". Điều này đúng cho hai nhiệm vụ. Với nhiều nhiệm vụ, bài báo cộng các phạt bậc hai neo ở điểm tối ưu của từng nhiệm vụ cũ, nên tâm không nhất thiết là $w^{(k-1)}$ như Định nghĩa 10.12 | KPK tr. 3: "…the sum of two quadratic penalties is itself a quadratic penalty"; draft dòng 641 | Thêm "với hai nhiệm vụ" sau "chính quy hóa tham số" (+4 tiếng) |
| nhẹ | Nhận xét 10.14 tiêu đề | F6. Blueprint 10.5 giới thiệu EWC như phần tùy chọn ("optional"). Khối này không đánh dấu tùy chọn, dù §13 xếp Kirkpatrick vào mục "Mở rộng" | blueprint dòng 722 | Tiêu đề: "Nhận xét 10.14 (Phạt bậc hai có trọng số theo tầm quan trọng; đọc thêm)" (+2 tiếng) |
| nhẹ | Nhận xét 10.5, Phụ lục A dòng 914–949; §2 | F7. Chữ dùng trùng trong cùng một bài: $M$ vừa là ngân sách bộ nhớ (Định nghĩa 10.10, `ky-hieu.md` dòng 115) vừa là hàm trội; $K$ vừa là số nhiệm vụ (§2) vừa là hằng số chặn ở Phụ lục A Bước 6; $h$ là số gia ở Phụ lục A Bước 1, trong khi $h$ là giả thuyết và Phụ lục B phải dùng chữ đậm để tránh trùng | §E mục 1 | Hàm trội: $\bar M$ (hoặc $\Lambda$); hằng số Bước 6: $C_\mu$; số gia: $\Delta$. Đổi chữ, không thêm tiếng |
| nhẹ | Ví dụ 10.9 | F8. $\gamma$ là kí hiệu chiết khấu trong Sutton–Barto (khung tr. 350, bài đọc bắt buộc), mà bài vừa nói không chiết khấu. Việc chọn $\gamma$ đã được chấp nhận (outline §13.3 mục 11), nên chỉ ghi để điều phối viên cân nhắc | SB tr. 350 "$\alpha\gamma^tG$" | Tùy chọn: đổi thành $\kappa$ |
| nhẹ | §13 bullet "Thuật toán và giá trị nền" | F9. "Sutton và Barto cho phép giá trị nền là biến ngẫu nhiên không thay đổi theo hành động; học phần nêu điều kiện … kèm phản ví dụ" có thể bị đọc như điều kiện của nguồn chưa đủ. Thực ra nguồn phát biểu cho dạng tổng trên mọi hành động (13.8), trong đó điều kiện ấy là đủ | SB tr. 351 (13.8)–(13.9) | "…không thay đổi theo hành động, trong dạng tổng trên mọi hành động (13.8); với ước lượng lấy mẫu, học phần nêu điều kiện…" (+9 tiếng) |
| nhẹ | dòng 595 | F10. "Huấn luyện một lần trên mọi dữ liệu … với các mẫu cùng cỡ, là học có giám sát với phân bố $\frac1K\sum_kD_k$". Mẫu gộp là mẫu phân tầng, với đúng $m$ quan sát từ mỗi $D_k$, nên không phải mẫu i.i.d. theo hỗn hợp. Chỉ rủi ro mục tiêu là rủi ro của hỗn hợp | Định nghĩa 10.10 dòng 588 | "…là học có giám sát với rủi ro mục tiêu $\frac1K\sum_kL_k$, không phải học liên tục." (0 tiếng) |
| nhẹ | Ví dụ 10.16 Kết luận (dòng 749) | F11. "$0{,}331$; $0{,}256$; $0{,}252$ với $M=5$, $50$, $1000$: gần $0{,}25$". Giá trị $0{,}331$ ($M=5$, khoảng $0{,}158$–$0{,}721$) không gần $0{,}25$. Kết luận đúng hơn là rủi ro giảm về $0{,}25$ khi $M$ tăng | Phụ lục C bảng dòng 1015 | "…: giảm về $0{,}25$ của điểm thỏa hiệp khi $M$ tăng, không về $0{,}125$ của riêng nhiệm vụ A." (0 tiếng) |
| nhẹ | dòng 3, 5, 141, 146, 298, 806 so với dòng 19 | F12. "Người học" mang hai nghĩa: tác tử hay thuật toán (dòng 3, 5, 141, 146, 298, 806) và sinh viên (dòng 19, "Sau bài này, người học có thể"). Phần A còn dùng "tác tử" cho cùng đối tượng. Điều phối viên đã giao điểm này cho người rà | `CLAUDE.md` workspace: "one meaning per term"; review-log dòng 42 | Trong Phần A, thay "người học" bằng "tác tử" (dòng 141, 146, 298); dòng 3, 5, 806 dùng "thuật toán học" hoặc "tác tử". Mục tiêu học tập giữ như Bài 09 (0 tiếng) |
| nhẹ | §12(f) dòng 877 | F13. (T3) xuất hiện lần đầu ở lời giải tổng kết mà không được nhắc lại nghĩa. Kiến thức tiên quyết chỉ có (T1), (T2) | lec-04 dòng 74: (T3) là hàm lỗi trong $[0,1]$ | "(T3) (hàm lỗi trong $[0,1]$, Bài 04)" (+6 tiếng) |

(Phụ lục A Bước 6, điểm điều phối viên giao: đã kiểm, hàm trội đúng và khả tích, không có phát hiện.)

## Ngân sách chữ (thân bài 11 982 / 12 000)

Các sửa có thêm chữ: F1 (+22), F2 (+5), F3 (+15), F4 (+16, tùy chọn), F5 (+4), F6 (+2), F9 (+9), F13 (+6). Tổng khoảng +79 nếu sửa tất cả; khoảng +42 nếu chỉ sửa F1–F3. Có thể cắt các câu sau, tổng khoảng −85 tiếng, không mất nội dung:

1. Dòng 129: "Hai ví dụ trên chỉ có một bước, nên không có trạng thái nào nối các bước với nhau." (−18). Câu mở §4, dòng 133, đã nêu ý này.
2. Dòng 802: bỏ vế "chọn đại lượng nào là một phần của việc đặc tả bài toán, như chọn hàm lỗi ở Bài 01" (−22). Ý chính đã có ở dòng 768 và §10.
3. Dòng 607: "Độ chính xác $\mathrm{acc}_{K,K}$ trên nhiệm vụ cuối không cho biết gì về quên." (−13). Định nghĩa độ quên chỉ lấy $i<K$ nên ý này đã có sẵn.
4. Dòng 752: rút còn "Khi hai nhiệm vụ xung đột, chính quy hóa tham số và phát lại chỉ chọn một điểm trên đánh đổi bền vững–mềm dẻo." (−14). Bỏ vế sau vì lặp Mệnh đề 10.13(a) và dòng 682.
5. Dòng 413: bỏ "và theo Ví dụ 10.4, mỗi ước lượng có thể ngược dấu với gradient" (−15). Kết luận Ví dụ 10.4 đã nói ý này.
