# Nhật ký rà soát — Bài 01: Mô hình học, rủi ro, ERM và PAC

Tệp nội bộ. Ghi tác tử, quyết định của điều phối viên, phát hiện rà soát và nguồn đã tham khảo.

## Tác tử

| Bước | Vai trò | Loại | Mô hình | Mức | Bằng chứng |
|---|---|---|---|---|---|
| 2026-10-30 · 1 | Phân tích nguồn UML (chỉ đọc) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 1 | Văn phong và thuật ngữ (ghi `van-phong.md`, `thuat-ngu.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 2 | Lập dàn ý (ghi `outline.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 3 | Soạn ghi chú (ghi `lecture-note.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 4 | Năm lượt rà độc lập (học viên; chính xác toán học; chuyên gia và trung thành nguồn; học thuật–sư phạm và `no-ai-slop` Detect; mạch và móc nối), chỉ đọc | general-purpose ×5 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 5 | Biên tập (ghi `lecture-note.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 6 | Rà lại: toán học trên phần đã sửa; mạch toàn bài (chỉ đọc) | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 7 | Vòng sửa cuối (cùng biên tập viên, tiếp tục bằng `SendMessage`) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-30 · 8 | Soạn bài tập (ghi `exercises.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 9 | Rà bài tập: toán học; sư phạm và văn phong (chỉ đọc) | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 10 | Sửa bài tập theo hai lượt rà (cùng người soạn, tiếp tục bằng `SendMessage`) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-30 · 11 | Rà lại toán trên phần bài tập đã đổi (chỉ đọc) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 12 | Sửa ngắn bài tập theo rà lại toán (cùng người soạn) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-30 · 13 | Tái cấu trúc thứ tự (ghi `lecture-note.md`, tham chiếu trong `exercises.md`, `reorder-plan.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 14 | Rà lại sau tái cấu trúc: mạch–thứ tự; toán học (chỉ đọc) | general-purpose ×2 | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 15 | Sửa cuối sau rà lại (cùng biên tập viên tái cấu trúc) | general-purpose | opus (Opus 5.5) | high | lệnh `SendMessage` của phiên điều phối |
| 2026-10-30 · 16 | Dò và sửa câu lắt léo (ghi `lecture-note.md`, `exercises.md`, `cau-lat-leo.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 17 | Rà giữ nguyên nghĩa của 104 câu sửa (chỉ đọc) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 18 | Viết lại Định nghĩa 01.5 dạng danh sách (ghi `lecture-note.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 19 | Rà và sửa mọi khối hình thức theo §3a, §9a (ghi `lecture-note.md`, `ra-khoi-hinh-thuc.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 20 | Rà giữ nghĩa và song song của 12 khối hình thức đã sửa (chỉ đọc) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |

## Phân tích nguồn — quyết định của điều phối viên: **chấp nhận** (2026-10-30)

Điều phối viên đã kiểm tra lại: (1) mọi con số của ví dụ xuyên suốt bằng số học hữu tỉ chính xác ($L_D$ = 0.52, 0.32, 0.22, 0.32, 0.28, 0.48; rủi ro Bayes 0.18; $L_S$ = 1/2, 1/3, 1/3, 1/2, 1/3, 1/2; $0.8^{13}=0.0550$, $0.8^{14}=0.0440$, $0.6^5=0.0778$, $0.6^6=0.0467$; $\mathbb E L_D(A_{\max})\approx0.0227$ tại $m=10$); (2) vị trí Định nghĩa 3.1 (tr. 43), 3.3 (tr. 46), 3.4 (tr. 49) và mục "Bayes Optimal Predictor" (tr. 46) trong PDF; (3) cụm "approximate ERM" chỉ xuất hiện ở tr. 152 (§11.3), nên kết luận "không có trong Ch. 2–3" đúng.

Quyết định cho dàn ý và bản thảo:

1. Dùng mô hình phân bố đồng thời $D$ trên $\mathcal X\times\mathcal Y$ ngay từ đầu; trường hợp khả thực là trường hợp riêng (nhãn tất định và $\exists h^\star\in\mathcal H$ với $L_D(h^\star)=0$). Không lặp lại bước chuyển $L_{(D,f)}\to L_D$ của UML.
2. Đối tượng so sánh viết bằng $\inf_{h\in\mathcal H}L_D(h)$ (blueprint), kèm nhận xét vì sao UML viết $\min$ và ví dụ cận dưới đúng không đạt được. Khả thực định nghĩa bằng giá trị nhỏ nhất bằng 0 **đạt được**, phân biệt với $\inf=0$.
3. Mặc định học đúng lớp ($A(S)\in\mathcal H$) như UML Định nghĩa 3.4; một nhận xét ngắn về học ngoài lớp (UML Remark 3.2).
4. Thêm tính ngẫu nhiên nội tại của thuật toán học vào định nghĩa PAC ($\Pr$ theo $S$ và nguồn ngẫu nhiên $\xi$) — bổ sung của học phần, UML không có.
5. Định nghĩa ERM gần đúng và rủi ro dư so với $\mathcal H$ là định nghĩa của học phần; tách rủi ro dư so với $\mathcal H$ khỏi rủi ro dư so với bộ phân lớp Bayes; chưa dùng tên "sai số ước lượng" (để Bài 04).
6. Phân biệt độ phức tạp mẫu của một thuật toán $m_A$ với của lớp $m_{\mathcal H}$; giữ "với mọi $m\ge m_{\mathcal H}(\epsilon,\delta)$".
7. Phản ví dụ 1.2 dùng phiên bản một chiều của blueprint ($X\sim U[0,1]$, $Y\equiv1$, $L_D=1$); nói rõ đây là một lựa chọn ERM tồi trong lớp rất giàu, không phải mọi ERM, và không phải định lý Không có bữa ăn miễn phí (chỉ trỏ tới UML §5.1).
8. Mệnh đề 1.3 (quy tắc Bayes) có chứng minh ngắn trong ghi chú; nêu rõ ngưỡng $1/2$ chỉ đúng với lỗi 0–1, với hàm lỗi bất đối xứng của ví dụ sàng lọc y tế ngưỡng là $c_{FP}/(c_{FP}+c_{FN})$.
9. Phát biểu chính xác cho Hệ quả: với lớp mọi bộ phân lớp đo được, bộ ERM học thuộc có $L_S=0$, $L_D=1$ với mọi $S$, nên không có cận $L_D(\hat h)\le L_S(\hat h)+\varepsilon(m,\delta)$ với $\varepsilon\to0$ đúng cho mọi lựa chọn ERM.
10. Ví dụ xuyên suốt: quy tắc sàng lọc theo ngưỡng trên $\mathcal X=\{1,\dots,5\}$ (bản bất khả tri với $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$ và bản khả thực với $f=1[x\ge3]$), theo báo cáo mục 4; ví dụ thực tế: sàng lọc y tế với hàm lỗi có trọng số. Nhắc rằng cỡ mẫu tính được là cho một $D$ cụ thể, cầu nối sang Bài 02.
11. Bài tập UML chọn: 2.1, 3.1, 3.2, 3.3, 3.6, 3.8 (thử thách). Bỏ 2.2 (trùng bài gốc 3 và Mệnh đề 1.1), 3.7 (trùng chứng minh Mệnh đề 1.3); để 2.3, 3.4, 3.5 sang Bài 02; bỏ 3.9. Lưu ý chỗ hổng của bản lời giải: 3.3 (chọn bán kính có khối lượng đúng $\epsilon$ hỏng khi $D$ có nguyên tử), 3.8(1) và 3.8(3).

## Văn phong và thuật ngữ — quyết định của điều phối viên: **chấp nhận, còn câu hỏi mở** (2026-10-30)

Đã kiểm tra lại số đếm trên mã nguồn sách (trừ dòng chú thích và tệp nháp): "ước lượng hợp lý cực đại" 22, "quá khớp" 6 so với "phù hợp trội" 2, "tốc độ học" 23, "hàm dự đoán" 3, "kí hiệu" 12 so với "ký hiệu" 2; "i.i.d." không có trong phần sách đang dùng. Đối chiếu ngẫu nhiên các đoạn trích trong `van-phong.md` với mã nguồn sách. Điều phối viên chọn "hàm dự đoán" (theo sách) và đã sửa `ky-hieu.md`; tên "tốc độ học"/"độ dài bước" chốt cùng họ thuật ngữ gradient. Các câu hỏi mở về thuật ngữ được chuyển cho người dùng.

**Quyết định của người dùng (2026-10-30):** $L_D(h)$ gọi là "rủi ro kì vọng" (theo sách); viết "kí hiệu"; chấp nhận giả thuyết, lớp giả thuyết, khả thực, bất khả tri, thiên kiến quy nạp, rủi ro vượt mức, khoảng cách tổng quát hóa; họ gradient theo học phần anh em (gradient, hạ gradient, dưới gradient, độ dài bước). Điều phối viên đã cập nhật `thuat-ngu.md`, `ky-hieu.md`, `van-phong.md`, mẫu ghi chú và trang chỉ mục.

## Dàn ý — quyết định của điều phối viên: **chấp nhận** (2026-10-30)

Đã tính lại mọi con số † của dàn ý (rủi ro có trọng số 0,52/0,32/0,37/0,92/1,12/1,92 và rủi ro Bayes có trọng số 0,32 với $h_2$; chọn ngẫu nhiên 0,82/3 và 1/3; $0{,}6\cdot0{,}8^{10}\approx0{,}0644$; $L_{D_f}(h_6)=0{,}6$; bảng $L_S$ của Bài tập 01.2 và $L_D(h_t)=0{,}5-0{,}15t$, $0{,}15t-0{,}1$; Ví dụ 01.7; $\lceil\ln20/0{,}1\rceil=30$): tất cả đúng. Các quyết định cho 10 điểm mở được ghi ở đầu `outline.md`.

## Bản thảo ghi chú — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-30)

Bản thảo 741 dòng; thân bài khoảng 12 600 từ (vượt mục tiêu 10 500), phụ lục khoảng 950 từ. Hiển thị sạch qua HTTP ở 1600×900 và 390×844 và qua `file://` (0 lỗi KaTeX, 44 khối). Điều phối viên đã tính lại các con số người viết thêm ngoài bảng của dàn ý ($L_{D_f}(h_1)=0{,}4$; $1/3-0{,}22\approx0{,}11$; $n_0=(1,1,0,1,0)$, $n_1=(0,1,1,0,1)$; $a(t)$, $b(t)$ ở Phụ lục C.1; $0{,}8^{10}$, $0{,}6^{10}$, $0{,}4^{10}$; 4,4% tại $m=14$): đúng. Chấp nhận ba sai khác so với dàn ý (hàm ghi nhớ theo nhãn đa số để là ERM trên mọi mẫu; ví dụ inf≠min bắt đầu từ $n\ge2$; $A_{\max}$, $A_{\min}$ gắn với Thuật toán 01.11). Độ dài để người dùng hiệu chỉnh sau thí điểm; người rà mạch đề xuất chỗ rút gọn.

## Biên tập vòng 1 — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-30)

Biên tập viên xử lý đủ 20 quyết định và mọi phát hiện nghiêm trọng, trung bình; danh sách không áp dụng có lý do (bài tập hoãn; giữ đoạn precision rút gọn vì outline cần phản ví dụ; giữ "Mẫu là một dãy" rút gọn; vài câu 41–47 tiếng trong khối định nghĩa). Điều phối viên kiểm lại: thân bài 11 466 tiếng, phụ lục 1 618 (chấp nhận vượt ≈ 470 tiếng vì phần thêm là nội dung bắt buộc; người dùng hiệu chỉnh sau thí điểm); 0 lần xuất hiện các biến thể bị loại; đánh số 01.1–01.30 liên tục; con số mới đúng ($0{,}999^{500}\approx0{,}606$; $0{,}8^{10}=1048576/9765625$; precision hỗn hợp $2/3$; hiệu Bayes của $h_3$ là $1/25$). Đã cập nhật `thuat-ngu.md` (10 thuật ngữ mới), `ky-hieu.md` ($M$, $\beta$, các phân bố và mẫu của ví dụ) và bảng số hiệu cuối cùng trong `outline.md`.

## Rà lại và vòng sửa cuối — quyết định của điều phối viên: **ghi chú đạt, chờ kiểm định cuối** (2026-10-30)

Rà lại toán học (`reviews/6-ra-lai-toan.md`): không còn lỗi nghiêm trọng/trung bình, 20/20 phát hiện của rà soát 2 đã xử lý, mọi con số mới đúng; 7 điểm nhẹ. Rà lại mạch toàn bài (`reviews/7-ra-lai-mach.md`): T1–T9 ✓, không lỗi nghiêm trọng; vài điểm trung bình về văn phong và danh sách cắt ≈ 400 tiếng. Vòng sửa cuối (cùng biên tập viên) áp dụng cả hai báo cáo, trừ hai ngoại lệ của điều phối viên (giữ đoạn giá trị dự đoán dương và Phụ lục C.4 vì outline cần phản ví dụ; câu §9 về Bài tập 01.9 theo cách nói của điều phối viên). Điều phối viên kiểm lại: thân bài 11 120 tiếng, phụ lục 1 617; 30 khối đánh số và 10 ví dụ không đổi; 0 biến thể bị loại; `material-local-data.js` đồng bộ. Hai công thức còn cuộn ngang nhẹ trong khung ở 390 px (3 px, 15 px), không ẩn nội dung: chấp nhận.

Việc cho bước bài tập: Bài tập 01.9 có thêm ý cho lớp hàm ngưỡng với $A_{\max}$ (khớp câu ở §9); một bài đo Mục tiêu 2 (quy tắc Bayes dưới $\ell_{0\text{-}1}$ và $\ell_c$, rủi ro vượt mức); Bài tập 01.3 không hỏi lại điều Mệnh đề 01.5 đã chứng minh.

## Bài tập — quyết định của điều phối viên: **chấp nhận để rà soát** (2026-10-30)

`exercises.md`: 11 bài (01.1–01.5 gốc, 01.6–01.11 là UML 2.1, 3.1, 3.2, 3.3, 3.6, 3.8), 31 gợi ý, 11 lời giải; ≈ 10 700 tiếng (vượt dự kiến 4 500–6 500; để người dùng hiệu chỉnh). Bài 01.2 đo Mục tiêu 2 bằng bảng $\eta$ mới trên $\{1,\dots,6\}$; Bài 01.3 không hỏi lại Mệnh đề 01.5; Bài 01.9 có phần lớp hàm ngưỡng với $A_{\max}$. Người soạn tự giải trước rồi mới đối chiếu bản lời giải: không có con số nào lệch; đã vá các chỗ hổng của bản lời giải (3.1, 3.2, 3.3, 3.8(1), 3.8(3)). Điều phối viên kiểm nhanh $0{,}9^{28}$, $0{,}9^{29}$, $0{,}9^{30}$, $e^{-3}$, $0{,}899^{28}$, $\lceil10\ln20\rceil$: đúng. Thuật ngữ: điều phối viên đổi "lớp đường tròn đồng tâm" thành "lớp hình tròn đồng tâm" trong ghi chú và bài tập (lớp gồm các đĩa), thêm vào `thuat-ngu.md`. Chuyển hai lượt rà: toán học (giải lại từng bài) và sư phạm–văn phong.

## Công bố ghi chú trên trang học kỳ (2026-10-30, theo yêu cầu người dùng)

Thẻ Bài 01 của `2627-1/index.html` liên kết `material-viewer.html?doc=materials/lec-01/lecture-note.md`; "Bài tập" vẫn "Chưa có" cho đến khi bài tập qua rà soát. Đã xóa thẻ giữ chỗ cũ "Bản giữ chỗ" còn sót (trỏ tới tệp đã xóa). Kiểm tra bằng Playwright qua HTTP và `file://` ở 1600×900 và 390×844: 10 thẻ, bấm liên kết mở đúng ghi chú, 0 lỗi, 0 `.katex-error`, không cảnh báo.

## Rà bài tập — quyết định của điều phối viên (2026-10-30)

Rà toán (`reviews/8-bai-tap-toan.md`): không lỗi nghiêm trọng, mọi con số đúng; hai lỗi trung bình (01.2(d) "ngưỡng lớn nhất" không xác định thuật toán trên mọi mẫu; 01.5(d) câu 2 chỉ đúng với $D_f$), điều phối viên đã kiểm lại cả hai. Rà sư phạm (`reviews/9-bai-tap-su-pham.md`): một lỗi nghiêm trọng (độ dài 10 724 tiếng so với kế hoạch 4 500–6 500), mười lỗi trung bình (đề chưa tự đứng, mục tiêu 5 thiếu thiên kiến quy nạp, gợi ý 1 lộ đáp án ở 01.5 và 01.11, kí hiệu trùng, thiếu tiếng Anh, tiêu đề lệch §10…). Điều phối viên đổi "affine" → "afin" trong ghi chú theo `thuat-ngu.md`. **Quyết định:** `reviews/10-quyet-dinh-bai-tap.md` — chấp nhận mọi phát hiện; bỏ hai phần mở rộng ngoài kế hoạch (01.9(d), 01.11(d)); mục tiêu ≈ 8 500 tiếng, người dùng hiệu chỉnh sau thí điểm. Giao lại cho cùng người soạn (tiếp tục bằng `SendMessage`).

## Sửa bài tập — quyết định của điều phối viên: **chấp nhận, chuyển rà lại toán** (2026-10-30)

Người soạn áp dụng mọi phát hiện và quyết định trong `reviews/10-quyet-dinh-bai-tap.md`, trừ chỉ tiêu độ dài: 9 023 tiếng (giảm từ 10 724; phần vượt ≈ 500 do các ý điều phối viên yêu cầu thêm — 01.3(a), 01.5(e), 01.6(c), đề tự đứng). Điều phối viên chấp nhận độ dài này để người dùng hiệu chỉnh sau thí điểm. Đã kiểm con số mới: $M'(0{,}6)=1001$, $M'(0{,}4)=1$; ≤ $k/2$ điểm ở 01.6(c) (nghiệm bội chẵn). §10 của ghi chú không đổi. Đã thêm 9 thuật ngữ mới vào `thuat-ngu.md`. Chuyển một lượt rà lại toán trên phần đã đổi.

## Rà lại toán bài tập (2026-10-30)

Không có lỗi chặn bàn giao hay nghiêm trọng; không con số nào sai (liệt kê đủ cho 01.3 với $m\le4$, 01.10 với $m\le3$). Hai lỗi trung bình của rà soát 8 đã giải quyết. Một lỗi trung bình mới: 01.5(e) thiếu tên thuật toán và điều kiện $m\ge M(0{,}1;0{,}05)$ (với $A_{\max}$ dưới $D_\eta$: $\Pr[L\le0{,}32]=0{,}48$ tại $m=1$). Năm điểm nhẹ (lý do nghiệm bội chẵn ở 01.6(c); "không loại thêm ứng viên"; lý do tồn tại max ở 01.2(d); tính đo được đồng thời ở 01.9(a); cách nói ở 01.5(d)). Không còn tham chiếu treo tới 01.9(d), 01.11(d). **Quyết định:** chấp nhận cả sáu; giao người soạn sửa ngắn (tiếp tục bằng `SendMessage`).

## Kiểm định cuối và công bố — Bài 01 (2026-10-30)

Người soạn sửa đủ sáu điểm của lượt rà lại toán (01.5(e) nêu thuật toán và điều kiện $m\ge M(0{,}1;0{,}05)$; lý do nghiệm bội chẵn và câu về mọi cách gán nhãn ở 01.6(c); lý do tồn tại phần tử lớn nhất ở 01.2(d); tính đo được đồng thời ở 01.9(a); cách nói ở 01.5(d)); không con số nào đổi. Điều phối viên kiểm lại văn bản. Thẻ Bài 01 của `2627-1/index.html` liên kết ghi chú và bài tập. Kiểm định bằng Playwright, bấm từ trang chỉ mục, qua HTTP và `file://`, ở 1600×900 và 390×844: 0 lỗi trang, cảnh báo hay yêu cầu hỏng; 0 `.katex-error`; không cảnh báo của trình đọc; không khối `:::` chưa hiển thị; không cuộn ngang trang; gợi ý và lời giải thu gọn (6 khối ở ghi chú, 42 ở bài tập); in PDF A4 được cả hai tài liệu. `material-local-data.js` đồng bộ. Độ dài: ghi chú thân bài 11 120 tiếng, phụ lục 1 617; bài tập 9 163 tiếng — người dùng hiệu chỉnh sau thí điểm.

**Trạng thái:** Bài 01 (ghi chú và bài tập) hoàn tất, chờ người dùng duyệt thí điểm. Chưa commit.

## Duyệt thí điểm của người dùng — vòng 1 (2026-10-30)

**Người dùng:** "Sắp xếp lại thứ tự, tôi thấy nhiều đoạn hoặc khái niệm được đưa ra trước khi định nghĩa." Điều phối viên kiểm: 19 dòng thân bài dẫn tới khối đánh số đứng sau; nhiều thuật ngữ dùng sớm (khả thực dòng 22, định nghĩa dòng 440; hàm phân lớp ghi nhớ dòng 13 / 396; thuật toán học dòng 3 / 308). Nguyên nhân cấu trúc: §2 (nhãn giả thiết trỏ tới định nghĩa sau) và §3 (ví dụ xuyên suốt đã dùng rủi ro, ERM, $A_{\max}$, hàm ghi nhớ) đứng trước các định nghĩa. **Quyết định:** quy tắc "định nghĩa trước khi dùng" ghi vào `CLAUDE.md` của học phần (ưu tiên hơn thứ tự thành phần của blueprint), kèm công cụ `../tools/courses/statistical-learning-theory/scripts/forward_refs.py`; giao một biên tập viên tái cấu trúc ghi chú (kế hoạch ở `reorder-plan.md`, đánh số lại, cập nhật tham chiếu trong bài tập). Bản trước khi sắp xếp lưu ở scratchpad `reorder/`.

**Người dùng (bổ sung cùng vòng):** "Cần làm rõ định nghĩa learning setting: cực tiểu rủi ro kì vọng khi không biết phân bố D nhưng có một tập quan sát lấy mẫu iid từ D (sau khi định nghĩa các khái niệm này)." **Quyết định:** thêm khối định nghĩa "Bài toán học thống kê" ngay sau khi đã định nghĩa $D$, lớp $\mathcal H$, hàm lỗi, rủi ro kì vọng và mẫu i.i.d.; nêu mục tiêu (tiến tới $\inf_{h\in\mathcal H}L_D(h)$), cái chưa biết ($D$), cái chọn trước ($\mathcal H$, $\ell$), cái ngẫu nhiên ($S$, $A(S)$, $L_D(A(S))$); rủi ro thực nghiệm và ERM đến sau như đại lượng thay thế tính được. Chuyển cho biên tập viên tái cấu trúc (cùng lượt).

**Người dùng (bổ sung cùng vòng):** "Tính ngẫu nhiên của thuật toán không cần đưa ra quá sớm, sẽ làm notation quá phức tạp trong buổi đầu tiên. Có thể viết A(S) thay cho A(S; \xi)." **Quyết định:** thay thế quyết định 4 (nguồn ngẫu nhiên $\xi$ trong định nghĩa PAC). Bài 01 dùng thuật toán tất định $A(S)$; bỏ $\xi$ khỏi định nghĩa, kết quả, ví dụ và bài tập; bỏ nhận xét "Nguồn ngẫu nhiên nội tại", giữ tối đa một câu (sau định nghĩa PAC hoặc ở §12) nói thuật toán ngẫu nhiên (ví dụ SGD, Bài 05) được xử lý bằng cách lấy xác suất theo cả mẫu và nguồn ngẫu nhiên của thuật toán. Chuyển cho biên tập viên tái cấu trúc (cùng lượt). Người dùng cũng yêu cầu: sau khi sửa xong, tạo repo, commit, tạo remote, push và bật GitHub Pages.

## Tái cấu trúc — quyết định của điều phối viên: **chấp nhận, chuyển rà lại** (2026-10-30)

Biên tập viên làm đủ ba yêu cầu của người dùng (định nghĩa trước khi dùng; Định nghĩa 01.5 "Bài toán học thống kê" ở §4 sau rủi ro kì vọng, mẫu và thuật toán học; bỏ $\xi$). Kế hoạch, kết quả rà (44 chỗ dùng trước định nghĩa ở bản cũ, 0 ở bản mới ngoài ngoại lệ cho phép) và bảng đổi số ở `reorder-plan.md`. Bỏ nhận xét nguồn ngẫu nhiên nội tại và dòng chọn ngẫu nhiên 0,273 của Ví dụ 01.6. Điều phối viên kiểm lại: `forward_refs.py` 0; không còn `\xi` trong ghi chú và bài tập; Định nghĩa 01.5 ở dòng 220; thân bài 11 678 tiếng, phụ lục 1 595, bài tập 9 142; `material-local-data.js` đồng bộ; không cuộn ngang trang ở 390 px. Chuyển hai lượt rà lại: mạch–thứ tự và toán học.

## Rà lại sau tái cấu trúc (2026-10-30)

Mạch–thứ tự (`reviews/11-ra-lai-sap-xep-mach.md`): `forward_refs.py` 0; đọc tuần tự không còn chỗ dùng trước định nghĩa; ba yêu cầu của người dùng đạt (định nghĩa bài toán học "đạt phần lớn": thiếu hệ quả "$D$ chưa biết ⇒ $A$ không phụ thuộc $D$ ⇒ đúng với mọi $D$"); 3 trung bình, 10 nhẹ. Toán (`reviews/12-ra-lai-sap-xep-toan.md`): không lỗi nghiêm trọng/trung bình; 209 dẫn chiếu đúng; mọi con số đúng; 7 nhẹ. **Quyết định:** áp dụng tất cả; giao lại cùng biên tập viên (tiếp tục bằng `SendMessage`). Đã thêm "bài toán học thống kê" vào `thuat-ngu.md`.

## Kiểm định sau duyệt thí điểm vòng 1 — **đạt** (2026-10-30)

Biên tập viên áp dụng mọi phát hiện của `reviews/11-…` và `12-…`, không đổi số hiệu (Định nghĩa 01.5 nêu thuật toán chọn trước, không phụ thuộc $D$, nên yêu cầu đúng với mọi $D$; điều kiện rủi ro hữu hạn nằm trong định nghĩa; $\forall D$ của học PAC nối về Định nghĩa 01.5). Điều phối viên kiểm lại: `forward_refs.py` 0; 0 `\xi`; `material-local-data.js` đồng bộ; 390 px không cuộn ngang trang, 0 `.katex-error`, không cảnh báo, cả ghi chú và bài tập; không tệp PDF, `.env`, `._*` trong danh sách commit. Người dùng đã yêu cầu commit, tạo remote, push và bật GitHub Pages.

## Duyệt thí điểm của người dùng — vòng 2 (2026-10-30)

**Người dùng:** "Một câu trả lời hấp dẫn nhưng sai cho rằng hai hàm tốt như nhau, vì cả hai đều không sai trên mẫu — Những câu kiểu thế này quá lắt léo, phải sửa. Ví dụ sửa thành: Hai hàm có tốt như nhau vì đều phân lớp hoàn hảo trên mẫu huấn luyện không? Dò tất cả các câu lắt léo như trên và tìm cách sửa." **Quyết định:** thêm `van-phong.md` §9a "Câu thẳng, không lắt léo" (các dạng cần sửa; câu hỏi thật được trả lời trong bài được phép) và một dòng trong `CLAUDE.md` của học phần; giao một biên tập viên dò toàn bộ ghi chú và bài tập, ghi danh sách vào `cau-lat-leo.md`, rồi sửa.

**Kết quả dò câu lắt léo:** 104 câu được viết lại (90 trong ghi chú, 14 trong bài tập; danh sách đầy đủ ở `cau-lat-leo.md`): chủ thể trừu tượng 51, câu đảo/rào đón/lồng mệnh đề 31, phủ định kép hoặc vòng 15, danh từ hóa 11, chuyển thành câu hỏi thẳng 4, câu chỉ báo chuyển ý 3, lời thuật lại 1 (ví dụ của người dùng, áp dụng nguyên văn ở câu hỏi mở đầu). Ba chỗ sửa trong khối hình thức (Mệnh đề 01.23(b), Hệ quả 01.29(a), giả thiết của 01.23). Điều phối viên kiểm: `forward_refs.py` 0; câu hỏi mở đầu dùng đúng câu của người dùng. Chuyển một lượt rà độc lập về giữ nguyên nghĩa toán của từng câu sửa.

**Người dùng (cùng vòng):** "Với xác suất không thấp hơn — sửa thành — Với xác suất ít nhất." Điều phối viên thay 6 chỗ (4 ghi chú, 2 bài tập) và đổi cách nói chuẩn trong `thuat-ngu.md`, `van-phong.md`.

**Rà giữ nguyên nghĩa (104 câu sửa + 6 câu thay cụm):** không lỗi chặn bàn giao hay nghiêm trọng; mọi câu giữ đúng giả thiết, lượng từ, chiều bất đẳng thức, con số; không có sửa ngoài danh sách. Hai lỗi trung bình (câu duy nhất ở Mệnh đề 01.23(b) mơ hồ; lời giải 01.4(c) "chỉ đúng trên các nguyên tử" sai theo từng điểm) và 9 điểm nhẹ. **Quyết định:** áp dụng cả hai lỗi trung bình và các điểm nhẹ; giao lại cùng biên tập viên câu chữ.

**Vòng chỉnh sau rà nghĩa — đạt (2026-10-30):** biên tập viên áp dụng hai lỗi trung bình và chín điểm nhẹ. Điều phối viên kiểm: `forward_refs.py` 0; câu duy nhất ở Mệnh đề 01.23(b) và lời giải 01.4(c) đã sửa; 0 biến thể bị loại (kể cả "không thấp hơn"); `material-local-data.js` đồng bộ; 390 px không cuộn ngang trang, 0 `.katex-error`, không cảnh báo. Chưa commit; chờ người dùng quyết định push.

## Duyệt thí điểm của người dùng — vòng 3 (2026-10-30)

**Người dùng:** "Viết lại định nghĩa 01.5 sao cho gãy gọn hơn, các giả thiết cần liệt kê (gạch đầu dòng) thay vì viết trong đoạn văn rất khó theo dõi." **Quyết định:** viết lại Định nghĩa 01.5 thành câu dẫn và danh sách thành phần có nhãn in đậm; gọt đoạn đọc sau đó để không nhắc lại danh sách. Ghi quy tắc chung `van-phong.md` §3a và một dòng trong `CLAUDE.md` của học phần. Giao một người viết (một khối).

**Kết quả:** Định nghĩa 01.5 thành câu dẫn và sáu dòng có nhãn in đậm (Tập quan sát, Chọn trước khi lấy mẫu, Phân bố dữ liệu, Dữ liệu, Thuật toán, Mục tiêu), công thức hiệu nằm trong dòng Mục tiêu; đoạn đọc sau định nghĩa rút còn bốn câu, bỏ phần nhắc lại. Nội dung toán, dẫn chiếu và đánh số không đổi. Điều phối viên kiểm: ảnh chụp ở 1600×900 và 390×844 (danh sách hiển thị đúng trong khối); `forward_refs.py` 0; `material-local-data.js` đồng bộ; liên kết "Bỏ qua phần điều hướng" ẩn khi không focus (chỉ hiện khi bấm Tab), chồng lấn trong ảnh chụp là hiện tượng của cách chụp. Chưa commit.

**Người dùng:** "Gạch đầu dòng 'chọn trước khi lấy mẫu' không song song với các gạch đầu dòng khác." **Sửa (điều phối viên, sửa nhỏ do người dùng chỉ định):** nhãn đổi thành tên thành phần — Tập quan sát, Lớp giả thuyết và hàm lỗi, Phân bố dữ liệu, Mẫu huấn luyện, Thuật toán học, Mục tiêu; nội dung mỗi dòng cùng khuôn "kí hiệu, mô tả, vai trò" (bỏ "Cần chọn …"). Kiểm: 6 dòng hiển thị, 0 `.katex-error`, `forward_refs.py` 0. Thêm yêu cầu "song song" vào `van-phong.md` §3a.

**Người dùng:** "Sau khi sửa hãy rà lại các phát biểu định nghĩa, định lý khác." **Quyết định:** giao một biên tập viên rà mọi khối hình thức của Bài 01 (định nghĩa, mệnh đề, hệ quả, thuật toán, nhận xét) theo §3a (danh sách có nhãn, song song) và §9a (câu thẳng), lập bảng ở `rà-khoi-hinh-thuc.md` rồi sửa; sau đó một lượt rà độc lập về giữ nguyên nghĩa.

**Kết quả rà khối hình thức:** 30 khối được rà, 12 khối sửa (01.7, 01.8, 01.12, 01.13, 01.14, 01.15, 01.18, 01.20, 01.23, 01.25, 01.28, 01.29) cùng đoạn ba lý do trước 01.25; 18 khối giữ nguyên (bảng ở `ra-khoi-hinh-thuc.md`). Nhãn thống nhất giữa các khối (Tập đầu vào, Phân bố dữ liệu, Mẫu huấn luyện, Lớp giả thuyết, Hàm lỗi, Thuật toán, Cỡ mẫu, Sai số và xác suất thất bại). Điều phối viên xem ảnh 01.18 và 01.29: hiển thị rõ; thứ tự lượng từ của 01.18 giữ nguyên (∃M, rồi các ∀ giao hoán). `forward_refs.py` 0. Chuyển một lượt rà độc lập về giữ nghĩa và tính song song.

**Rà giữ nghĩa và các vòng sửa tiếp (2026-10-30).** Người rà độc lập (dòng 20) xác nhận 12 khối giữ nghĩa toán, kể cả thứ tự lượng từ ở 01.18, 01.25, 01.28; nêu 2 lỗi trung bình và 9 lỗi nhẹ.

| mức độ | vị trí | vấn đề | quyết định |
|---|---|---|---|
| trung bình | Mệnh đề 01.23, câu sau danh sách | "như dưới $D_\eta$" sai cho (b) với chi phí $(1,3)$: ngưỡng $\tfrac14=\eta(2)$; "ngưỡng" chưa gọi tên | chấp nhận — điều phối viên kiểm lại; sửa vòng 2, tách đoạn vòng 3–5 |
| trung bình | Đoạn trước 01.25 | (iii) là kết luận, không phải lý do | chấp nhận — "hai lý do" + đoạn kết |
| trung bình | Hệ quả 01.29 (vòng 2) | câu phản ví dụ thiếu $A_{\mathrm{gn}}$; $\hat A$ tự do gợi sai phạm vi của (b) | chấp nhận — sửa vòng 3, đưa câu phản ví dụ vào Bước 1 |
| trung bình | §6, nhãn 01.18 | "tham số độ chính xác" dùng trước khi giới thiệu (§6 gọi là "sai số") | chấp nhận — giới thiệu thuật ngữ ở §6 (vòng 3), viết lại câu (vòng 4–5) |
| nhẹ | 01.14, 01.15, 01.18, 01.20, 01.25, 01.28, 01.29, mục tiêu 4 | nhãn, câu dẫn báo số mục, cỡ mẫu theo §11, công thức một dòng, câu "trong đó", "tham số độ tin cậy" | chấp nhận |
| nhẹ | 01.18/01.25 | câu "bất đẳng thức dưới đây … Bất đẳng thức đó là" hơi vòng | bác bỏ — đọc được, thêm nhãn (∗) không cần |
| nhẹ | 01.25, 01.23(a), Phụ lục B | ngắt dòng công thức đọc gượng | bác bỏ — biên tập viên đo: cần ngắt để không cuộn ngang ở 390 px |
| nhẹ | Bước 1 chứng minh 01.29 | "Cặp … là phản ví dụ" nêu trước đích | bác bỏ — câu ngay sau nói rõ |

Biên tập viên (dòng 19, tiếp tục bằng SendMessage) sửa 4 vòng; sửa thêm công thức cuộn ngang ở 01.23(a) (do vòng 1) và ở Phụ lục B (có từ trước). Người rà kết luận sau vòng 4: có thể bàn giao. Điều phối viên đọc diff từng vòng (`round2..5.diff` trong scratchpad), kiểm $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$ không trùng $\tfrac12$, $\tfrac15$; xem ảnh 01.25 ở 390 px và 01.29. Kiểm cuối do điều phối viên chạy: `sync --check` OK, `forward_refs` 0, `git diff --check` sạch; Playwright (biên tập viên): 0 katex-error, 0/41 công thức cuộn ngang ở 390 px. Số từ ghi chú 13 661 → 14 025. Kết luận: **chấp nhận**.

## Nguồn đã tham khảo

UML (trang PDF): 33–53 (§2.1–2.4, §3.1–3.5), 60–64 (Ch. 5 mở đầu, §5.1, đầu §5.2); tìm từ khóa trên tr. 1–130. Bản lời giải: tr. 1–8 (Ch. 2–3), chỉ để kiểm tra độ khó và chỗ thiếu.

## Phát hiện rà soát — vòng 1 (2026-10-30)

Năm báo cáo trong `reviews/1-hoc-vien.md`, `2-toan-hoc.md`, `3-chuyen-gia-nguon.md`, `4-hoc-thuat-van-phong.md`, `5-mach.md`. Không có lỗi chặn bàn giao. Phát hiện nghiêm trọng (sau khi gộp trùng): thiên kiến quy nạp trên ví dụ rời rạc (rà soát 1, 2); $A_{\max}/A_{\min}$ định nghĩa hai lần (1, 2, 4); thiếu điều kiện $\mathcal X$ vô hạn ở câu Bayes $+\epsilon$ (2, 3, 5); câu hỏi trung tâm không được trả lời tường minh (5); lý do chọn $\inf_{\mathcal H}$ rải và một phần sai (5); "chấp nhận được" hai nghĩa (1, 4); định nghĩa độ phức tạp mẫu dẫn trước và $m_A$ hai nghĩa (1); lý thuyết độ đo không có trong tiên quyết (1); độ dài vượt khoảng 20% (1, 5). Mọi con số đều đúng (rà soát 2).

Điều phối viên đã kiểm lại trên văn bản và bằng tính toán: 2/32 hàm khớp $S_f$; câu dòng 523 ("không biết $\eta$"); câu UML tr. 44 về $m_{\mathcal H}$; câu UML tr. 43–44 bị diễn ý; $S=((1,0),(4,1))$ cho $A_{\min}\to h_2$; tính duy nhất của quy tắc Bayes dưới $D_\eta$; kì vọng $0{,}8^m$ và $0{,}6\cdot0{,}8^m$ cùng tốc độ; hai ví dụ thay thế (mẫu $((1,0),(3,1),(5,1))$; phân bố $Y\equiv1$, $0{,}8^{10}\approx0{,}107$).

**Quyết định:** `reviews/0-quyet-dinh.md` (chấp nhận mọi phát hiện nghiêm trọng và trung bình, trừ các mục hoãn sang bước bài tập; 20 quyết định nội dung; mục tiêu thân bài ≤ 11 000 tiếng).

## Trình bày ví dụ từng bước (§7a) — 2026-10-30

**Người dùng:** "ghi thêm nguyên tắc viết ví dụ: ví dụ không được quá nhanh, phải diễn giải từng bước, sử dụng xuống dòng để trình bày rõ ràng hơn, không viết díu vào nhau trong 1 đoạn văn quá nhiều ý", rồi "hãy giao 1 biên tập ra các ví dụ của Bài 01". **Quyết định:** quy tắc ghi ở `van-phong.md` §7a, §14 mục 8 và `CLAUDE.md` của học phần; giao một biên tập viên trình bày lại Ví dụ 01.1–01.11, khối ứng dụng và các phép tính ở §5, §7, §9, §11, Phụ lục C, không đổi con số hay lập luận.

| Bước | Vai trò | Loại | Mô hình | Mức | Bằng chứng |
|---|---|---|---|---|---|
| 2026-10-30 · 21 | Biên tập ví dụ theo §7a (ghi `lecture-note.md`, `vi-du-tung-buoc.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-10-30 · 22 | Rà giữ nghĩa và §7a (chỉ đọc) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |

**Bản sửa:** thân bài 12 435 → 13 234 từ (đếm bằng `wc -w`); `forward_refs.py` 0; `sync --check` OK. Điều phối viên đọc toàn bộ diff: chỉ tách bước, thêm giá trị trung gian suy ra trực tiếp từ ghi chú.

**Rà lại** (`reviews/13-ra-vi-du-tung-buoc.md`): giữ nguyên nghĩa, đạt §7a; một phát hiện trung bình (bác bỏ — Định nghĩa 01.22 có định nghĩa rủi ro Bayes dưới $\ell_c$) và mười điểm nhẹ (chấp nhận chín). Giao lại cùng biên tập viên sau khi tác tử lập dàn ý Bài 02 ghi xong (một người ghi tại một thời điểm).

**Lỗi hiển thị phát hiện kèm:** ở 390 px trang cuộn ngang (ghi chú 477 px, bài tập 405 px, có từ trước lần sửa này; lượt kiểm định trước đã đo sai). Nguyên nhân: bản MathML ẩn của KaTeX (`position: absolute`) trong bảng có khối chứa nằm ngoài khung cuộn của bảng. Điều phối viên thêm `2627-1/material-viewer-course.css` (`.markdown-body table { position: relative; }`), nạp sau `material-viewer.css` trong `material-viewer.html`. Đo lại bằng Playwright: 390 px chiều rộng trang 375, `scrollX` 0 ở cả ghi chú và bài tập; 1600 px không đổi; 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng. Quy tắc chung trong `shared/css/material-viewer.css` có cùng lỗi; chờ người dùng quyết định sửa bản gốc.

**Vòng sửa sau rà lại — chấp nhận (2026-10-30).** Cùng biên tập viên (tiếp tục bằng `SendMessage`) áp dụng chín điểm nhẹ được chấp nhận ở `reviews/13-ra-vi-du-tung-buoc.md` (nhãn song song ở Ví dụ 01.9, 01.10; bỏ nhãn bị lặp; "báo âm tính tại $x=1$"; dẫn Mệnh đề 01.23(b); câu §7 sau Định nghĩa 01.24; gộp đoạn thiên kiến quy nạp; nhãn đầu khối ứng dụng; tách phép tính ở Nhận xét 01.9, 01.21). Điều phối viên kiểm từng chỗ sửa trên văn bản; `sync --check` OK; `forward_refs.py` 0; `git diff --check` sạch; Playwright (điều phối viên chạy) 390 px: trang rộng 375 px, `scrollX` 0, 0 `.katex-error`, 0 lỗi trang, 0 yêu cầu hỏng; 1600 px sạch. Thân bài 13 241 từ (`wc -w`). **Kết luận: chấp nhận, commit và push.**

## Sửa §5–hết theo văn phong của tác giả — 2026-11-01

**Người dùng:** "tôi đã sửa bài 1 đến hết mục 4. Hãy so sánh bản sửa của tôi với bản ở HEAD để phân tích văn phong, cách tôi viết, cách tôi bố cục, cách tôi lựa chọn nội dung (tôi đã bỏ bớt một số đoạn không cần thiết) so với cách AI viết, sau đó chỉnh sửa các mục còn lại của bài 1 theo cách viết của tôi để tôi duyệt". **Quyết định của điều phối viên:** phân tích diff (`git diff HEAD`, phần mở đầu–§4) ghi ở `van-phong-tac-gia.md`; bản sửa tay của tác giả sao lưu ở scratchpad (`lecture-note.user-edit.md`, md5 dòng 1–340 `6ded8c08…`) và không bị động tới; không xóa khối đánh số (bài tập dẫn số); không commit trước khi tác giả duyệt.

| Bước | Vai trò | Loại | Mô hình | Mức | Bằng chứng |
|---|---|---|---|---|---|
| 2026-11-01 · 1 | Biên tập §5–Phụ lục theo `van-phong-tac-gia.md` (ghi `lecture-note.md` từ §5) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-11-01 · 2 | Rà độ chính xác toán học §5–hết (chỉ đọc; `review-math.md` trong scratchpad) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |
| 2026-11-01 · 3 | Rà văn phong tác giả + sư phạm, `no-ai-slop` Detect (chỉ đọc; `review-style.md`) | general-purpose | opus (Opus 5.5) | high | lệnh `Agent` của phiên điều phối |

**Vòng 1 (biên tập viên, dòng 1).** Đổi thuật ngữ (khả diễn, bất khả diễn, tập huấn luyện, hàm chỉ báo, phân bố liên hợp), cắt câu điều hướng/rào đón/hiển nhiên, tách danh sách, thêm công thức, gộp công thức một dòng, thêm bốn "Câu hỏi.". Điều phối viên đọc toàn bộ diff (`round1.diff`): md5 dòng 1–340 không đổi, 41 số hiệu khối không đổi, con số không đổi.

**Phát hiện vòng 1** (`mức độ | vị trí | vấn đề | quyết định`):

| mức độ | vị trí | vấn đề | quyết định |
|---|---|---|---|
| nghiêm trọng | Ví dụ 01.11, Kết luận | "Khi phân bố có nguyên tử, kì vọng của rủi ro tiến về 0" sai tổng quát (phân bố trộn nguyên tử + liên tục cho giới hạn ½; mâu thuẫn Bài tập 01.4(c)) | chấp nhận — điều phối viên kiểm phản ví dụ; giới hạn vào $D_1$ |
| trung bình | mở §7, Mệnh đề 01.23 | "đối tượng so sánh" định nghĩa là "mức rủi ro dương" (sai khi khả diễn); thuật ngữ hai nghĩa | chấp nhận — "mức tham chiếu"; nhãn "Tập hàm được xét" |
| trung bình | sau Định nghĩa 01.10 | "có thể âm" không minh họa; giá trị một mẫu làm bằng chứng cho kì vọng | chấp nhận — $0{,}28-\tfrac13=-\tfrac4{75}$ (điều phối viên tính lại); cận kì vọng $\ge0{,}2\cdot0{,}8^m$ |
| trung bình | sau Định nghĩa 01.25 | thiếu thành phần $\mathcal Z$, $\ell$ tổng quát | chấp nhận |
| trung bình | §6, câu về $\xi$ | gán xác suất cho Định nghĩa 01.18 mà Định nghĩa 01.4 tất định; thiếu $\xi$ độc lập $S$ | chấp nhận |
| trung bình | 4 câu hỏi mới, mở §6, Ví dụ 01.6, Nhận xét 01.9/01.19/01.21, §9, §12 | câu hỏi gợi đáp án; chủ ngữ trừu tượng; liệt kê gượng; chưa nối câu hỏi của tác giả sau Định nghĩa 01.1 | chấp nhận |
| trung bình | §10 tiêu đề bài tập | còn thuật ngữ cũ | hoãn — phải khớp `exercises.md`; tác giả quyết |
| trung bình | Phụ lục C.3, C.4 | không còn được dẫn | hoãn — tác giả quyết xóa |
| nhẹ | ~40 công thức một dòng | cuộn ngang trong khung ở 390 px (trang không tràn) | hoãn — văn phong tác giả (một dòng) mâu thuẫn chuẩn điện thoại; tác giả quyết |

**Vòng 2** (biên tập viên, tiếp tục bằng `SendMessage`): áp dụng mọi mục chấp nhận. Rà lại (cùng hai người rà): toán — 5/5 phát hiện giải quyết, 4 điểm nhẹ mới; văn phong — 17/20 giải quyết, 1 một phần (§9 dẫn Bài tập 01.9: bác bỏ, bài tập ở tệp riêng), 2 hoãn; ba dẫn chiếu Phụ lục thêm lại bị đánh giá trái văn phong tác giả (chấp nhận — gỡ). Vòng 3 sửa các điểm nhẹ.

**Vòng 3** (biên tập viên): bốn điểm nhẹ về toán (Nhận xét 01.19 "không phải là", "cận dưới đúng", phạm vi khẳng định rủi ro $1$ của $A_{\mathrm{gn}}$, câu nhân quả Ví dụ 01.11); gỡ ba dẫn chiếu Phụ lục A(iv), B, C.3 thêm ở vòng 2; bốn điểm nhẹ về văn phong. Điều phối viên kiểm từng chỗ trên văn bản.

**Kiểm cuối (điều phối viên chạy):** md5 dòng 1–340 (phần tác giả) `6ded8c08…` không đổi; `forward_refs.py` 0; `sync-local-materials.py --check` OK; `git diff --check` chỉ báo khoảng trắng cuối dòng ở dòng 3, 5, 109, 126 (phần tác giả, không sửa). Playwright qua `http.server` và `file://`, 1600×900 và 390×844: 0 lỗi console, 0 yêu cầu hỏng, 0 `.katex-error`, trang 375 px không cuộn ngang; 41/82 công thức hiển thị cuộn ngang trong khung ở 390 px (3 trong phần tác giả); bản in 51 trang, 0 `.katex-error`, Phụ lục B hiển thị đủ. Số từ 14 458 → 14 456. **Kết luận: chấp nhận để tác giả duyệt; chưa commit.** Chờ tác giả quyết: ngắt công thức cho 390 px; tiêu đề bài tập §10 và thuật ngữ trong `exercises.md`, `thuat-ngu.md`; xóa Phụ lục C.3, C.4, A(i)/(iv)/(v); các lỗi gõ ở §0–§4 liệt kê trong `van-phong-tac-gia.md` §6.

## Quyết định của tác giả và vòng 4 — 2026-11-01

**Người dùng** (trả lời bốn câu hỏi): ngắt dòng công thức chỉ khi rộng quá khung ở 390 px; đổi thuật ngữ đồng bộ trong `exercises.md`, §10 và `thuat-ngu.md`; xóa Phụ lục C.3, C.4, giữ Phụ lục A; sửa lỗi gõ và kí hiệu ở phần tác giả (§0–§4), không đổi câu chữ. **Điều phối viên:** `thuat-ngu.md` đổi lựa chọn thuật ngữ kèm ghi chú rằng Bài 02–10 còn dùng từ cũ (≈190 chỗ trong 15 tệp) cho đến khi sửa từng bài; giao cùng biên tập viên (dòng 1, tiếp tục bằng `SendMessage`). Bản trước vòng 4: `lecture-note.after-r3.md`, `exercises.before-r4.md` (scratchpad).

**Vòng 4–5** (biên tập viên): (A) phần tác giả chỉ sửa lỗi gõ, kí hiệu, dấu câu theo danh sách đã báo (dấu cách trước "?", khoảng trắng cuối dòng, $D\to S$ cho tập huấn luyện mở đầu, $h_1,h_2\to h_3,h_4$ kèm vế "chỉ số dưới của $h$ là ngưỡng báo dương tính" — **lời mới, chờ tác giả xác nhận**, `\mid`/`\Pr`, `\ell_{0\text{-}1}`, $S\sim D^m$, "phân bố", "Tập huấn luyện.", "(joint distribution)", dấu câu quanh công thức); (B) ngắt `aligned` mọi công thức rộng quá khung ở 390 px, nội dung toán không đổi (người rà toán so bằng script `r4/mathcmp.py`); (C) xóa Phụ lục C.3, C.4; (D) `exercises.md` đổi thuật ngữ, ba tiêu đề đổi, §10 khớp từng chữ, Bài tập 01.1(b) nói rõ dòng $\xi$ của bảng §1 không dùng; (E) `thuat-ngu.md`, `ky-hieu.md` đổi lựa chọn thuật ngữ, ghi chú Bài 02–10 còn dùng từ cũ. Rà lại vòng 4: toán — đạt cả năm mục; văn phong — không lỗi từ trung bình trở lên, các điểm nhẹ sửa ở vòng 5. Điều phối viên đọc diff phần tác giả từng từ.

**Kiểm cuối (điều phối viên chạy, sau vòng 5):** `forward_refs.py` 0; `sync --check` OK; `git diff --check` sạch; Playwright qua `http.server` và `file://`, 1600×900 và 390×844, ghi chú và bài tập: 0 lỗi console, 0 yêu cầu hỏng, 0 `.katex-error`, 0/81 công thức ghi chú và 0 công thức bài tập cuộn ngang, trang 375 px không cuộn; bản in 0 `.katex-error`. **Kết luận: chấp nhận, chờ tác giả duyệt trước khi commit.**

## Tác giả sửa tay lần hai và vòng 6 — 2026-11-01

**Người dùng:** "tôi đã sửa một ít trong bản của bạn"; giữ vế "chỉ số dưới của $h$ là ngưỡng báo dương tính"; "hãy commit & push sau vòng 6". Tác giả sửa: in đậm **quá khớp**; đưa bất đẳng thức lên ngay sau "bất đẳng thức" ở Định nghĩa 01.18, 01.25; Nhận xét 01.19 chuyển sang cách hiểu theo tần suất (bỏ phần xác suất hậu nghiệm); "lớp giả thuyết" ở Định nghĩa 01.20; bỏ câu "Ứng viên tự nhiên là ERM…" cuối §7. Bổ sung vào `van-phong-tac-gia.md` §6a.

**Vòng 6** (biên tập viên): chỉ các chỗ kéo theo — tiêu đề Nhận xét 01.19; bỏ dẫn chiếu 01.19 ở §9; lời giải Câu hỏi phụ (2) ở §11 đọc theo tần suất; §12 dòng "Tính đo được"; khoảng trắng cuối dòng; bỏ dấu chấm giữa câu sau công thức ở 01.18, 01.25. Bài tập 01.5(d) vẫn dẫn đúng Nhận xét 01.19. Điều phối viên đọc diff so với bản đồng bộ trước đó: không chạm câu chữ tác giả.

**Kiểm cuối:** `forward_refs.py` 0; `sync --check` OK; `git diff --check` sạch; Playwright (HTTP, `file://`, 1600×900, 390×844; ghi chú và bài tập): 0 lỗi console, 0 `.katex-error`, 0 công thức cuộn ngang, trang không cuộn ngang. **Kết luận: chấp nhận; commit và push theo yêu cầu của tác giả.**

## Kiểm tuân thủ nguyên tắc ghi chú mới — quyết định của điều phối viên: **chưa tuân thủ đầy đủ** (2026-11-13)

Yêu cầu của người dùng (2026-11-13): kiểm ghi chú Bài 01–10 theo các nguyên tắc ghi chú hiện hành và ghi bảng phát hiện đầy đủ vào nhật ký từng bài. Chỉ kiểm, chưa sửa ghi chú.

**Tác tử:** người kiểm tuân thủ (chỉ đọc, ghi một tệp báo cáo), `general-purpose`, mô hình `opus` (Claude Opus 5.5), effort `high` (theo lệnh gọi Agent); mười tác tử độc lập, mỗi tác tử một bài, chạy song song. Báo cáo gốc: `planning/lec-01/reviews/kiem-nguyen-tac-2026-11-13.md`.

**Bản được kiểm:** `materials/lec-01/lecture-note.md`, HEAD `25dd982`, tệp không có thay đổi chưa commit. Bài đã được tác giả duyệt (2026-11-01); 23 hàng (#1–#22, #45) thuộc văn bản tác giả, chỉ báo, không sửa câu chữ.

Căn cứ: `../CLAUDE.md` mục "Writing course content" và "The author's voice" (gồm quy tắc 2026-11-04 về trạng thái văn bản và 2026-11-09 về từ giảm nhẹ, giải thích đi thẳng vào ý); `CLAUDE.md` của học phần mục "Lecture notes"; `planning/lec-01/van-phong-tac-gia.md` (§1–§7, bảng thuật ngữ §5, §6b: giả thiết gom ở §2, mục tiêu §1 thành danh sách công thức, $\sup$ cho độ lệch đồng thời); `planning/van-phong.md`, `thuat-ngu.md`, `ky-hieu.md`, `materials/_templates/lecture-note.md`; `no-ai-slop` chế độ Detect. Ngoài phạm vi: dẫn lại toán học, tệp bài tập.

**Kiểm của điều phối viên:** `forward_refs.py` báo 0 trước khi giao việc; script đối chiếu xác nhận mọi trích dẫn ở cột `bằng chứng` là chuỗi con nguyên văn của ghi chú, tại hoặc sát dòng được ghi; đếm mức độ khớp với báo cáo. Điều phối viên kiểm lại #63, #67 (dòng 1057, 1122: câu về trạng thái văn bản) và #30 trên tệp: đúng. #30 hạ xuống `nhẹ`: $\inf$ là kí hiệu tiên quyết chuẩn, sửa bằng một dòng ở Kiến thức tiên quyết.

**Kết luận:** 78 phát hiện (chặn bàn giao 0, nghiêm trọng 3, trung bình 15, nhẹ 60, sau điều chỉnh của điều phối viên). Mọi phát hiện được chấp nhận làm đầu vào cho lượt sửa; chưa phát hiện nào được sửa. Hàng có ghi "văn bản tác giả" hoặc "VBTG" chỉ để báo, không sửa câu chữ của tác giả.

**Câu hỏi mở cho tác giả và chuyển tiếp:**

- #36: gom (O1), (O2), giả thiết khả diễn lên §2 (§6b) va chạm với quy tắc định nghĩa trước khi dùng ($L_S$, ERM định nghĩa ở §5).
- #70: câu cỡ mẫu ở dòng 1143 có nên thành khối mới (Mệnh đề 01.31, đặt cuối nên không đổi số) không.
- #9, #73: câu dẫn "bảng kí hiệu của học phần" (tệp nội bộ) và khối "Quan hệ với giáo trình UML" — áp dụng chung cho mọi bài.

### Bảng phát hiện

| # | mức độ | vị trí | quy tắc | vấn đề | bằng chứng | đề xuất sửa | quyết định |
|---|---|---|---|---|---|---|---|
| 1 | nhẹ | Mở bài, dòng 7 | kiểu chữ | Chữ hoa sau "bao gồm:"; hai định nghĩa (rủi ro kì vọng, rủi ro thực nghiệm) dồn trong một gạch đầu dòng. VBTG — chỉ báo, không sửa câu chữ. | Rủi ro của hàm dự đoán, bao gồm: *Rủi ro kì vọng* (population risk, expected risk) | Viết thường "*rủi ro kì vọng*"; tác giả quyết có tách thành hai gạch con không. | chấp nhận; chưa sửa |
| 2 | nhẹ | Mở bài, dòng 8 | kiểu chữ | Dấu hai chấm thừa trước "là". VBTG — chỉ báo, không sửa câu chữ. | (empirical risk minimization, ERM): là quy tắc chọn hàm dự đoán sai ít nhất | "(empirical risk minimization, ERM) là quy tắc chọn …" | chấp nhận; chưa sửa |
| 3 | nhẹ | Câu hỏi mở đầu, dòng 21 | kiểu chữ | Cụm "trong tình huống này" kẹp giữa hai dấu phẩy làm câu khó đọc; "Nghĩa là" đứng trước danh sách mà thiếu dấu hai chấm. VBTG — chỉ báo, không sửa câu chữ. | Xét hai hàm dự đoán, trong tình huống này, còn gọi là hàm phân lớp (classifier). | "Xét hai hàm dự đoán, trong tình huống này còn gọi là hàm phân lớp (classifier)." và "Nghĩa là:". | chấp nhận; chưa sửa |
| 4 | nhẹ | Mục tiêu học tập dòng 35; §1 dòng 71; §4 dòng 297, 325 | thuật ngữ | "mẫu" chỉ tập huấn luyện, trái bảng thuật ngữ (van-phong-tac-gia §5; thuat-ngu dòng "sample (training set)"). VBTG — chỉ báo, không sửa câu chữ. | nhận mẫu $S$ và trả về hàm dự đoán | "tập huấn luyện": dòng 35 "…, tập huấn luyện, …"; dòng 71 "nhận tập huấn luyện $S$"; dòng 297 "được chọn từ tập huấn luyện"; dòng 325 "Vì tập huấn luyện $S$ ngẫu nhiên". Tác giả quyết. | chấp nhận; chưa sửa |
| 5 | nhẹ | Mục tiêu học tập dòng 36–39; §1 dòng 70; §5 dòng 682; §6 dòng 705, 770; §7 dòng 865, 937 | thuật ngữ | Tên tiếng Anh ghi hai lần: ở mục tiêu học tập (VBTG) và lại ở định nghĩa (loss function, inductive bias, realizable, sample complexity, Bayes risk, excess risk); van-phong §10 chỉ ghi ở lần đầu. | *Rủi ro Bayes* (Bayes risk) của $D$ là | Giữ tiếng Anh tại định nghĩa; tác giả quyết có bỏ ở mục tiêu học tập không. | chấp nhận; chưa sửa |
| 6 | nhẹ | §1 mục 2, dòng 67 | kiểu chữ | Dấu phẩy thừa tách chủ ngữ "trường hợp có hàm gán nhãn … $f$" khỏi vị ngữ. VBTG — chỉ báo, không sửa câu chữ. | $f:\mathcal X\to\mathcal Y$, là một trường hợp riêng | "… $f:\mathcal X\to\mathcal Y$ là một trường hợp riêng …" | chấp nhận; chưa sửa |
| 7 | nhẹ | §1 mục 7 dòng 72; Ví dụ 01.3 dòng 264 | kí hiệu | $\mathbb E_D[\cdot]$ khác dạng $\mathbb E_{Z\sim D}\,\ell(h,Z)$ của `ky-hieu.md` và Định nghĩa 01.1 (dòng 188). VBTG — chỉ báo, không sửa câu chữ. | L_D(h) = \mathbb E_D[\ell(h, Z)] | "L_D(h)=\mathbb E_{Z\sim D}\,\ell(h,Z)"; dòng 264 tương tự. Tác giả quyết. | chấp nhận; chưa sửa |
| 8 | nhẹ | §1 mục 7–8, dòng 72–73 | kiểu chữ | "**Mục tiêu**." có dấu chấm ngoài chữ đậm, "**Tài nguyên.**" có dấu chấm trong chữ đậm; mục 1–6 không có dấu chấm. VBTG — chỉ báo, không sửa câu chữ. | 7. **Mục tiêu**. Với mỗi hàm dự đoán $h$ | "7. **Mục tiêu.** …", thống nhất với mục 8. | chấp nhận; chưa sửa |
| 9 | nhẹ | §2, dòng 87 | câu điều hướng | "bảng kí hiệu của học phần" là tệp nội bộ `planning/ky-hieu.md`, sinh viên không mở được; vế "dùng ngay từ ví dụ ở §3; mỗi kí hiệu khác được đặt tên tại định nghĩa của nó" là câu dẫn mục. Bài 02 §2 (tác giả sửa) có cùng câu. VBTG — chỉ báo, không sửa câu chữ. | Bảng dưới gồm các kí hiệu riêng của bài dùng ngay từ ví dụ ở §3 | Tác giả quyết; đề xuất "Kí hiệu riêng của bài:" và bỏ vế sau dấu chấm phẩy. | chấp nhận; chưa sửa |
| 10 | nhẹ | §2, dòng 94 | nhãn mục | Nhãn "**Đọc lần đầu.**" không gọi tên nội dung (σ-đại số, hàm đo được) và có thể hiểu là "bỏ qua khi đọc lần đầu". VBTG — chỉ báo, không sửa câu chữ. | **Đọc lần đầu.** Mỗi tập $\mathcal X$, $\mathcal Y$, $\mathcal Z$ trong bài đi kèm một σ-đại số | "**σ-đại số và hàm đo được.**" | chấp nhận; chưa sửa |
| 11 | trung bình | §2, dòng 96 | văn bản làm chủ ngữ | "Bài này" làm chủ ngữ (CLAUDE.md học phần cấm); van-phong-tac-gia §6b đổi "Hai giả thiết thống kê" thành "Các giả thiết thống kê"; ngoặc "(phần **Giả thiết.** của các kết quả)" là lời dẫn. VBTG — chỉ báo, không sửa câu chữ. | Bài này sử dụng hai giả thiết thống kê dưới đây (phần **Giả thiết.** của các kết quả). | "Các giả thiết thống kê:" (như Bài 02 §2). | chấp nhận; chưa sửa |
| 12 | trung bình | §3, dòng 103 | rào đón | "đủ nhỏ để tính bằng tay" thuộc loại "dùng để tính tay" mà `../CLAUDE.md` (Content: cut) liệt kê để bỏ. VBTG — chỉ báo, không sửa câu chữ. | Ví dụ sau đủ nhỏ để tính bằng tay. | Bỏ câu; §3 mở thẳng bằng Ví dụ 01.1. | chấp nhận; chưa sửa |
| 13 | nhẹ | §3, Ví dụ 01.1, dòng 108–110 | kiểu chữ | Dấu cuối các gạch đầu dòng không thống nhất (";", ".", "."). VBTG — chỉ báo, không sửa câu chữ. | $\mathcal X=\{1,2,3,4,5\}$ là năm mức của một chỉ số đo; | Dùng ";" ở hai dòng đầu và "." ở dòng cuối. | chấp nhận; chưa sửa |
| 14 | nhẹ | §3, ứng dụng sàng lọc, dòng 163–164 | kiểu chữ | "(false negative - FN)" dùng gạch nối làm dấu phân cách; van-phong §10 quy định "(tên tiếng Anh, viết tắt)". VBTG — chỉ báo, không sửa câu chữ. | Âm tính giả (false negative - FN) | "Âm tính giả (false negative, FN)", "Dương tính giả (false positive, FP)". | chấp nhận; chưa sửa |
| 15 | nhẹ | §3, dòng 164 | kiểu chữ | "khoẻ" (dấu kiểu cũ) trong khi dòng 176 viết "khỏe" (van-phong §12). VBTG — chỉ báo, không sửa câu chữ. | báo dương tính đối với người khoẻ | "người khỏe". | chấp nhận; chưa sửa |
| 16 | nhẹ | §4, Ví dụ 01.2 dòng 201; Ví dụ 01.4 dòng 330 | thuật ngữ | "bản có nhiễu" là thuật ngữ cũ (van-phong-tac-gia §5: "dữ liệu có nhiễu", "trường hợp …"). VBTG — chỉ báo, không sửa câu chữ. | Xét bản có nhiễu của Ví dụ 01.1 | "Xét dữ liệu có nhiễu của Ví dụ 01.1: phân bố $D_\eta$, …". Tác giả quyết. | chấp nhận; chưa sửa |
| 17 | nhẹ | §4, Ví dụ 01.2, dòng 248 | câu điều hướng | Dẫn Phụ lục C.1; chỉ giữ khi người đọc cần mở để lấy số (C.1 có các tổng trung gian $a(t)$, $b(t)$). VBTG — chỉ báo, không sửa câu chữ. | Cùng cách tính cho bảng sau (Phụ lục C.1): | Tác giả quyết: giữ để dẫn tới $a(t)$, $b(t)$, hoặc "Cùng cách tính cho bảng sau:". | chấp nhận; chưa sửa |
| 18 | nhẹ | §4, dòng 258 | cấu trúc khó theo dõi | "bài toán hồi quy … áp dụng khung" là chủ thể trừu tượng; vế "cùng định nghĩa áp dụng cho hồi quy" không có vị ngữ rõ. VBTG — chỉ báo, không sửa câu chữ. | Ta chỉ cần đổi tập nhãn và hàm lỗi, cùng định nghĩa áp dụng cho hồi quy. | "Định nghĩa 01.1 áp dụng cho hồi quy khi đổi tập nhãn và hàm lỗi." | chấp nhận; chưa sửa |
| 19 | nhẹ | §4, Ví dụ 01.3, dòng 264 | câu dẫn công thức | Công thức hiển thị đứng riêng, không có câu dẫn (van-phong §4). VBTG — chỉ báo, không sửa câu chữ. | $$L_D(h_w)=\mathbb E_D\big(\langle w,X\rangle-Y\big)^2$$ | "Rủi ro kì vọng của $h_w$ là $$…$$" | chấp nhận; chưa sửa |
| 20 | nhẹ | §4, dòng 295 | nhắc lại kết quả | Vế sau nhắc lại kết luận ở dòng 282. VBTG — chỉ báo, không sửa câu chữ. | với lớp tuyến tính của Ví dụ 01.3, điều kiện tồn tại mô-men bậc 2 là đủ. | Bỏ vế sau dấu chấm phẩy. | chấp nhận; chưa sửa |
| 21 | nhẹ | §4, dòng 325–326 | danh sách song song | Danh sách chỉ có một gạch, chứa ba câu hỏi; thiếu dấu hai chấm. VBTG — chỉ báo, không sửa câu chữ. | Câu hỏi chính của Học thống kê là | "Câu hỏi chính của Học thống kê là:" rồi ba gạch "Hiệu trên có thể nhỏ đến đâu?", "Với xác suất nào theo $S$?", "Trên họ phân bố $D$ nào?". | chấp nhận; chưa sửa |
| 22 | nhẹ | §4 Ví dụ 01.4 dòng 332 (cùng dòng 255, 464, 913, 953) | kí hiệu | Cùng đại lượng viết $\inf_t$ ở dòng 332 và $\min_t$ ở các dòng khác. VBTG (dòng 332) — chỉ báo, không sửa câu chữ. | $\inf_tL_{D_\eta}(h_t)=L_{D_\eta}(h_3)=0{,}22$ | Thống nhất $\min_t$ cho lớp sáu hàm ngưỡng (Nhận xét 01.26: hai cách viết trùng nhau khi đạt được). Tác giả quyết. | chấp nhận; chưa sửa |
| 23 | nhẹ | Nhiều chỗ: dòng 372–378, 499–504, 525–529, 532–537, 669–674, 810–816, 820–824, 846–850, 1092–1096, 1111–1114, 1356–1359 | công thức một dòng | Công thức ngắn được ngắt bằng `aligned` mà chưa đo; `../CLAUDE.md`: giữ một dòng khi vừa khung, chỉ ngắt khi tràn ở 390 px; van-phong-tac-gia §7 mục 9 để tác giả quyết. | &\quad=\frac16\,\#\{i:\ h_t(x_i)\ne y_i\}. | Đo ở 390 px; công thức vừa khung viết một dòng, ví dụ $L_{S_\eta}(h_t)=\frac16\,\#\{i:\ h_t(x_i)\ne y_i\}$, $\Pr(X\in F)\le\sum_{i=1}^m\Pr(X=x_i)=0$. | chấp nhận; chưa sửa |
| 24 | nhẹ | §5 Ví dụ 01.5 dòng 387, Ví dụ 01.6 dòng 492, Ví dụ 01.7 dòng 556; §6 Ví dụ 01.9 dòng 855; §7 Ví dụ 01.10 dòng 931; §8 Ví dụ 01.11 dòng 1118 | nhãn bước | Nhãn "**Kết luận.**" gọi tên thao tác, không gọi tên kết quả (`../CLAUDE.md` "Step labels"; van-phong-tac-gia §1). Dòng 255 (Ví dụ 01.2) là VBTG, không tính. | **Kết luận.** Ba hàm $h_2$, $h_3$, $h_5$ có cùng rủi ro thực nghiệm | Dòng 387 "**Cùng rủi ro thực nghiệm, khác rủi ro kì vọng.**"; 492 "**Quy tắc chọn quyết định rủi ro.**"; 556 "**Tập nghiệm ERM rỗng.**"; 855 "**Cỡ mẫu cho riêng $D_f$.**"; 931 "**Hàm Bayes trong lớp hàm ngưỡng.**"; 1118 nối vào đoạn trước, không nhãn (xem #66). | chấp nhận; chưa sửa |
| 25 | nhẹ | §5, dòng 390 | công thức thay lời | "tức kì vọng của nó theo $S$ bằng rủi ro kì vọng" mô tả bằng lời một đẳng thức ngắn. | tức kì vọng của nó theo $S$ bằng rủi ro kì vọng. | "…, tức $\mathbb E_S[L_S(h)]=L_D(h)$.", hoặc bỏ vế này vì dòng **Bảo đảm.** nêu ngay sau. | chấp nhận; chưa sửa |
| 26 | nhẹ | §5, Mệnh đề 01.7, dòng 404 | nghĩa tích cực | Vế sau nói điều bảo đảm không cho; dòng 431 đã chỉ ra bằng số ($L_{S_\eta}(h_3)=\tfrac13$, $L_{D_\eta}(h_3)=0{,}22$). | nó không chặn độ lệch $\lvert L_S(h)-L_D(h)\rvert$ trên một tập huấn luyện cụ thể. | Bỏ vế sau dấu chấm phẩy: "Đây là bảo đảm theo kì vọng, so một đại lượng thực nghiệm với một đại lượng tổng thể (population quantity)." | chấp nhận; chưa sửa |
| 27 | trung bình | §5, chứng minh Mệnh đề 01.7, dòng 417 | thuật ngữ | "phân bố biên" ở §2 là $D_{\mathcal X}$ (phân bố của $X$); ở đây lại chỉ phân bố của từng $Z_i$ (mỗi thuật ngữ một nghĩa). | trong đó giả thiết cùng phân bố biên và $L_D(h)<\infty$ được dùng. | "trong đó giả thiết mỗi $Z_i$ có phân bố $D$ và $L_D(h)<\infty$ được dùng." | chấp nhận; chưa sửa |
| 28 | trung bình | §5, dòng 428 (báo trước ở dòng 390) | nhắc lại kết quả | Câu đầu sau $\square$ phát biểu lại đúng Mệnh đề 01.7; câu nói ý nghĩa cho việc học là câu thứ hai. | $\square$ Rủi ro thực nghiệm của một giả thuyết chọn trước khi có tập huấn luyện là ước lượng không chệch của rủi ro kì vọng. | "$\square$ Để ước lượng rủi ro kì vọng của một hàm dự đoán, ta tính rủi ro thực nghiệm của nó trên một tập dữ liệu độc lập với tập huấn luyện dùng để chọn nó." | chấp nhận; chưa sửa |
| 29 | nhẹ | §5 dòng 436; §6 dòng 702 | khẳng định không căn cứ | "đơn giản nhất" là phép so sánh không có căn cứ trong bài. | quy tắc chọn đơn giản nhất là thay $L_D$ chưa biết bằng $L_S$ | Dòng 436: "Dựa trên Mệnh đề 01.7, ta thay $L_D$ chưa biết bằng $L_S$ và chọn giả thuyết có rủi ro thực nghiệm nhỏ nhất."; dòng 702: "Trước hết, xét trường hợp lớp giả thuyết chứa một giả thuyết có rủi ro kì vọng bằng $0$." | chấp nhận; chưa sửa |
| 30 | nghiêm trọng | §5, Định nghĩa 01.8, dòng 446 (dùng lần đầu ở dòng 72, 81, 319) | định nghĩa trước khi dùng | $\inf$ được gọi tên "cận dưới đúng (infimum)" ở dòng 446, sau khi đã dùng ở §1 (dòng 72, 81) và Định nghĩa 01.5 (dòng 319). | trong đó $\inf$ là cận dưới đúng (infimum). | Thêm vào Kiến thức tiên quyết: "- Cận dưới đúng (infimum) $\inf$ của một tập số thực." rồi bỏ câu ở dòng 446; không sửa câu tác giả ở §1. | chấp nhận, hạ mức: nhẹ |
| 31 | trung bình | §5, Định nghĩa 01.8, dòng 439–449 | định nghĩa nhiều thành phần | Định nghĩa có ba thành phần (tập nghiệm ERM, nghiệm ERM, thuật toán ERM) cùng một giả thiết, viết thành đoạn văn (CLAUDE.md học phần: "Multi-part definitions as lists"). | Mỗi phần tử $\hat h$ của tập này là một *nghiệm ERM*. Giả sử tập nghiệm ERM khác rỗng với mọi $S$. | Câu dẫn "Cho lớp giả thuyết $\mathcal H$ và hàm lỗi $\ell$; với mỗi tập huấn luyện $S$:" rồi ba gạch "**Tập nghiệm ERM.** $\arg\min_{h\in\mathcal H}L_S(h)=\{…\}$, với $\inf$ …", "**Nghiệm ERM.** mỗi phần tử $\hat h$ của tập nghiệm ERM.", "**Thuật toán ERM.** khi tập nghiệm ERM khác rỗng với mọi $S$, một thuật toán học $A$ với $A(S)\in\arg\min_{h\in\mathcal H}L_S(h)$ với mọi $S$." | chấp nhận; chưa sửa |
| 32 | nhẹ | §5, dòng 464, 547; §6 dòng 702, 770; §7 dòng 872, 913; §8 dòng 1021 | thuật ngữ | "lớp" đứng trần thay cho "lớp giả thuyết" khi thuật ngữ đã dùng (van-phong-tac-gia §6a). | đúng cho mọi thuật toán ERM trên lớp. | "… trên lớp giả thuyết." Tương tự: "mức tốt nhất trong lớp giả thuyết" (464, 913), "lớp giả thuyết $\mathcal H_+$" (547), "khi lớp giả thuyết chứa" (702), "lớp giả thuyết $\mathcal H$" (770, 872). | chấp nhận; chưa sửa |
| 33 | nhẹ | §5, Ví dụ 01.6, dòng 482 | công thức thay lời | Quy ước về tập rỗng viết bằng lời. | với quy ước cực đại của tập rỗng bằng $0$ và cực tiểu của tập rỗng bằng $6$. | "với quy ước $\max\emptyset=0$ và $\min\emptyset=6$." | chấp nhận; chưa sửa |
| 34 | nhẹ | §5, dòng 495 | công thức thay lời | Câu hỏi mô tả bằng lời hai kì vọng. | kì vọng của $L_S(A(S))$ có bằng kì vọng của $L_D(A(S))$ không? | "**Câu hỏi.** Với một thuật toán ERM $A$, $\mathbb E_S[L_S(A(S))]$ có bằng $\mathbb E_S[L_D(A(S))]$ không?" | chấp nhận; chưa sửa |
| 35 | nhẹ | §5 dòng 515; §7 dòng 862 | câu dẫn công thức | "là đại lượng sau" trỏ xuống khối định nghĩa thay cho gọi tên tại chỗ (../CLAUDE.md "A formula stands where it is named"). | trên chính tập huấn luyện dùng để chọn nó là đại lượng sau. | Dòng 515: "Với hàm học được, ta so rủi ro kì vọng với rủi ro thực nghiệm trên chính tập huấn luyện dùng để chọn nó."; dòng 862: "Mức thấp nhất trên mọi hàm phân lớp đo được là rủi ro Bayes." | chấp nhận; chưa sửa |
| 36 | trung bình | §5, dòng 574–577 (cùng dòng 98, 446, 708) | Giả thiết tập trung ở §2 | (O1), (O2) nêu ở §5, bằng lời, không có công thức, khác khuôn nhãn của Bài 02 §2; giả thiết tập nghiệm ERM khác rỗng (dòng 446) và giả thiết khả diễn (dòng 708) cũng nằm rải; (T1) (dòng 98) không có công thức. van-phong-tac-gia §6b đòi mọi giả thiết ở §2, mỗi mục một công thức; đưa lên §2 lại xung đột với quy tắc định nghĩa trước khi dùng ($L_S$, ERM định nghĩa ở §5). | **(O1)** thuật toán tính được một nghiệm ERM chính xác; | Tối thiểu, theo khuôn Bài 02: "**(O1) Thuật toán trả về một nghiệm ERM chính xác.** $A(S)\in\arg\min_{h\in\mathcal H}L_S(h)$ với mọi $S$." và "**(O2) Thuật toán trả về một nghiệm $\epsilon_{\mathrm{opt}}$-ERM.** $L_S(A(S))\le\inf_{h\in\mathcal H}L_S(h)+\epsilon_{\mathrm{opt}}$ với mọi $S$."; (T1): "$S=(Z_1,\ldots,Z_m)\sim D^m$". Vị trí (§2 hay §5): master và tác giả quyết. | chấp nhận; chưa sửa |
| 37 | nhẹ | §5, dòng 579 | nhận xét hiển nhiên | Câu nói điều đã rõ từ cách viết (O1), (O2), không được dùng lại. | Hai giả thiết này không đặt điều kiện nào lên $D$. | Bỏ câu. | chấp nhận; chưa sửa |
| 38 | nhẹ | §5, dòng 615 | câu điều hướng | Trỏ tới "dòng" của thuật toán (loại "như dòng thứ hai của bảng ở §1" tác giả đã bỏ). | Chọn ngưỡng nhỏ nhất hay lớn nhất ở dòng **Một nghiệm ERM** cho đúng $A_{\min}$ hay $A_{\max}$. | "Chọn ngưỡng nhỏ nhất hay lớn nhất trong tập nghiệm ERM cho đúng $A_{\min}$ hay $A_{\max}$." | chấp nhận; chưa sửa |
| 39 | nhẹ | §5, dòng 617 | cấu trúc khó theo dõi | "một lớp đủ lớn" không định lượng; "nó" xa tiền ngữ "quy tắc chọn khi bằng nhau". | Trên một lớp đủ lớn, nó có thể làm rủi ro thay đổi từ $0$ đến $1$. | "Trên một lớp giả thuyết chứa mọi hàm phân lớp đo được, quy tắc chọn khi bằng nhau có thể làm rủi ro thay đổi từ $0$ đến $1$." | chấp nhận; chưa sửa |
| 40 | nhẹ | §5, Ví dụ 01.8, dòng 630–643 (câu dẫn ở dòng 639) | ví dụ | Ví dụ chỉ nêu thiết lập, không có câu cuối nói ví dụ dùng để làm gì (van-phong §7, §14 mục 8). | Trong ví dụ này: | Thêm một câu cuối nối với Mệnh đề 01.15 (trên mỗi tập huấn luyện, cả $h_{\equiv1}$ và $\mathbb 1_F$ với $F=\{X_1,\ldots,X_m\}$ đều khớp mọi quan sát), hoặc giữ nguyên nếu master coi khối này là khối thiết lập. | chấp nhận; chưa sửa |
| 41 | trung bình | §5, Mệnh đề 01.15, dòng 646–652 (được dẫn ở dòng 675, 1074, 1079) | Giả thiết/Bảo đảm | Dòng **Giả thiết.** không nêu "$D_{\mathcal X}$ không có nguyên tử", trong khi dòng 675, 1074, 1079 gọi đó là giả thiết của Mệnh đề 01.15; cũng không có thành phần tập huấn luyện, dù phần (a) viết "dưới $D$, $L_S(A_{\mathrm{gn}}(S))=0$". | **Phân bố dữ liệu.** $D$, phân bố của $(X,1)$ với $X\sim U[0,1]$. | "**Phân bố dữ liệu.** $D$, phân bố của $(X,1)$ với $X\sim U[0,1]$; $D_{\mathcal X}=U[0,1]$ không có nguyên tử." và thêm "**Tập huấn luyện.** $s\in\mathcal Z^m$ bất kì; dưới $D$, $S\sim D^m$." ("Năm thành phần" thành "Sáu thành phần"). | chấp nhận; chưa sửa |
| 42 | trung bình | §5, chứng minh Mệnh đề 01.15, dòng 664 | câu điều hướng | Câu dẫn Phụ lục cho chi tiết đo được, đúng loại tác giả đã bỏ ("Điều kiện đo được chỉ để … (Phụ lục A)"); Bước 1 không cần câu này để kết luận $A_{\mathrm{gn}}(s)\in\mathcal H$. | Điều kiện đo được của Định nghĩa 01.4 được kiểm ở Phụ lục A(iii). | Bỏ câu. Dẫn Phụ lục A(iii) ở chứng minh Hệ quả 01.29 (dòng 1063) vẫn giữ, vì ở đó tính đo được là một bước của lập luận. | chấp nhận; chưa sửa |
| 43 | nhẹ | §5, dòng 691 | nhận xét bên lề | Đoạn kết mục gộp ba ý độc lập; câu thứ hai không được dùng lại. | Quy tắc chọn khi bằng nhau là một thiên kiến khác, ở mức thuật toán. | Bỏ câu thứ hai; giữ câu giới hạn đầu và câu nối sang §6. | chấp nhận; chưa sửa |
| 44 | nhẹ | §6, dòng 708 | nhắc lại kết quả | Câu đầu phát biểu lại Định nghĩa 01.16. | Trong Định nghĩa 01.16, giá trị nhỏ nhất $0$ phải đạt được tại một phần tử của $\mathcal H$. | Bỏ câu; ví dụ $\inf=0$ không đạt ở Nhận xét 01.17 đã cho thấy điều này. | chấp nhận; chưa sửa |
| 45 | nhẹ | §6, Nhận xét 01.19, dòng 764 | kiểu chữ | "thì" thừa sau dấu phẩy. VBTG — chỉ báo, không sửa câu chữ. | trong 100 lần huấn luyện, thì có khoảng 95 lần | "trong 100 lần huấn luyện, có khoảng 95 lần …" (cách viết đã dùng ở dòng 1187). | chấp nhận; chưa sửa |
| 46 | nhẹ | §6, Định nghĩa 01.20, dòng 772 | công thức thay lời | "bất đẳng thức xác suất của Định nghĩa 01.18" thay cho một công thức ngắn. | sao cho bất đẳng thức xác suất của Định nghĩa 01.18 đúng với mọi $D$ | "sao cho $\Pr_{S\sim D^m}[L_D(A(S))\le\epsilon]\ge1-\delta$ đúng với mọi $D$ …" | chấp nhận; chưa sửa |
| 47 | nhẹ | §6, Nhận xét 01.21, dòng 786 | nguồn trong thân bài | Vế so sánh với UML §3.1 là chú thích nguồn, không phục vụ lập luận. | Trong Định nghĩa 01.20, cũng như ở giáo trình *Understanding Machine Learning: From Theory to Algorithms* | "Trong Định nghĩa 01.20, $m_{\mathcal H}$ được lấy riêng cho từng cặp …"; chuyển tên sách đầy đủ "(*Understanding Machine Learning: From Theory to Algorithms*, Shalev-Shwartz và Ben-David, 2014; viết tắt UML)" sang lần dẫn kế tiếp (dòng 971). | chấp nhận; chưa sửa |
| 48 | nhẹ | §6, Ví dụ 01.9, dòng 809, 818, 826, 835, 844, 853 | nhãn bước | Khuôn "**Bước k: …**" khác các ví dụ còn lại (nhãn đậm gọi tên kết quả) và khác chứng minh ("**Bước k (…).**"). | **Bước 1: rủi ro theo ngưỡng.** | Bỏ "Bước k:", giữ tên: "**Rủi ro theo ngưỡng.**", "**Xác suất rủi ro dương.**", "**Cỡ mẫu khi $\epsilon=0{,}1$, $\delta=0{,}05$.**", … | chấp nhận; chưa sửa |
| 49 | nhẹ | §6 Ví dụ 01.9 dòng 809; §7 Ví dụ 01.10 dòng 903; §8 Ví dụ 01.11 dòng 1097 | cấu trúc khó theo dõi | "sai đúng tại", "đúng tại", "sai tại" dùng "đúng/sai" vừa cho dự đoán vừa cho điều kiện, dễ đọc nhầm. | sai tại $x=1$, $x=2$ và $x=4$ ($\eta=\tfrac25$) | Dòng 903: "báo dương tính tại đúng các mức có $\eta(x)\ge\tfrac12$. Điều kiện này thỏa tại …, không thỏa tại $x=1$, $x=2$ và $x=4$ …"; dòng 809, 1097: "sai tại đúng các mức/điểm …". | chấp nhận; chưa sửa |
| 50 | nhẹ | §6, Ví dụ 01.9, dòng 844 | câu điều hướng | Công thức kì vọng chỉ dựa vào "Theo Phụ lục C.2"; lập luận của C.2 (dòng 1347–1354) đủ ngắn để viết tại chỗ. | **Bước 5: kì vọng.** Theo Phụ lục C.2, | "Với $N=\hat t-3$, ta có $\mathbb EN=\sum_{k=1}^3\Pr(N\ge k)$ và $\Pr(N\ge k)=(1-0{,}2k)^m$, nên" rồi công thức; hoặc giữ dẫn nếu master coi C.2 là chỗ người đọc cần mở. | chấp nhận; chưa sửa |
| 51 | nhẹ | §6, Ví dụ 01.9, dòng 855 | nghĩa tích cực | Câu nói các con số "không phải" $m_{A_{\max}}$ trong khi dạng khẳng định ngắn hơn. | chỉ đủ cho riêng $A_{\max}$ và riêng $D_f$, nên không phải $m_{A_{\max}}(\epsilon,\delta)$ | "Các cỡ mẫu $14$ và $6$ là cỡ mẫu đủ cho cặp $(A_{\max},D_f)$, tức một khẳng định dạng "$\forall D\ \exists m$"." | chấp nhận; chưa sửa |
| 52 | nhẹ | §6, dòng 858 | thuật ngữ | Tính khả diễn là tính chất của cặp $(D,\mathcal H)$ (Nhận xét 01.17), không của lớp giả thuyết. | Dưới $D_\eta$, không lớp nào khả diễn | "Không cặp $(D_\eta,\mathcal H)$ nào khả diễn, nên …" | chấp nhận; chưa sửa |
| 53 | nhẹ | §7, Mệnh đề 01.23, dòng 887–891 | công thức một dòng | Ngắt dòng giữa cặp ngoặc của $\min\{\eta(X),1-\eta(X)\}$. | &\quad=\mathbb E\min\{\eta(X),\\ | Một dòng "L_D^{\mathrm{Bayes}}=L_D(h_{\mathrm{Bayes}})=\mathbb E\min\{\eta(X),1-\eta(X)\}" (đo ở 390 px); nếu tràn, ngắt trước dấu "=" thứ hai. | chấp nhận; chưa sửa |
| 54 | trung bình | §7, dòng 898 | câu điều hướng | "Chứng minh nằm ở Phụ lục B" thuộc loại "Phụ lục B chứng minh …" mà `../CLAUDE.md` liệt kê để bỏ; tiêu đề "— đọc thêm" đã cho biết độ sâu. | Chứng minh nằm ở Phụ lục B: tại từng điểm $x$ | "Ý tưởng chứng minh: tại từng điểm $x$, ta chọn nhãn có rủi ro có điều kiện (conditional risk) nhỏ hơn, rồi lấy kì vọng theo $X$." | chấp nhận; chưa sửa |
| 55 | nhẹ | §7, dòng 943 | nhắc lại kết quả | Lý do rủi ro hữu hạn nhắc lại dòng 295; "ta phải nêu" là một yêu cầu, theo quy ước viết "chúng ta". | Trong phân lớp, mọi rủi ro đều hữu hạn vì $\ell_{0\text{-}1}$ và $\ell_c$ bị chặn | "Khi nói đến rủi ro vượt mức, chúng ta phải nêu đối tượng so sánh. Trong phân lớp, hai rủi ro vượt mức liên hệ qua đẳng thức" | chấp nhận; chưa sửa |
| 56 | nghiêm trọng | §7, dòng 970 (cùng dòng 305, 973, 1009) | định nghĩa trước khi dùng | "học đúng lớp" (thuat-ngu: proper learning) dùng lần đầu ở dòng 970 mà chưa được định nghĩa; dòng 305 (VBTG) chỉ ghi "(proper learning)"; Nhận xét 01.27 dùng làm tiêu đề mà không in nghiêng thuật ngữ. | Rủi ro của đầu ra một thuật toán học đúng lớp luôn ít nhất bằng | "Rủi ro của đầu ra một thuật toán *học đúng lớp* (proper learning), tức $A(S)\in\mathcal H$ như trong Định nghĩa 01.4, luôn ít nhất bằng …" | chấp nhận; chưa sửa |
| 57 | trung bình | §7, dòng 971 | câu điều hướng | "(Bài 02)" dẫn tới bài sau; câu về $\mathcal X$ hữu hạn không phục vụ lập luận chọn đối tượng so sánh. | yêu cầu đó đạt được bằng ERM trên $\mathcal M_{\mathcal X}$ (Bài 02). | Bỏ câu "Khi $\mathcal X$ hữu hạn, …"; nếu tác giả muốn giữ, bỏ "(Bài 02)". | chấp nhận; chưa sửa |
| 58 | nhẹ | §7, dòng 973 | nhắc lại kết quả | Câu đầu nhắc lại lý do (i) ở dòng 970. | không thuật toán đúng lớp nào có rủi ro nhỏ hơn mức này. | Bỏ câu "Vì vậy, …"; giữ "Phần chênh so với rủi ro Bayes là số hạng thứ hai của đẳng thức trên, tức giá của thiên kiến quy nạp." | chấp nhận; chưa sửa |
| 59 | nhẹ | §7, dòng 993, 997 | văn bản làm chủ ngữ | "Định nghĩa 01.25 thay đổi", "Định nghĩa không đòi" là chủ thể trừu tượng; dòng 997 nói điều định nghĩa không đòi. | Định nghĩa không đòi nhãn tất định, nên áp dụng được cho $D_\eta$. | Dòng 997: "Họ này chứa cả các phân bố có nhãn ngẫu nhiên như $D_\eta$."; dòng 993: "So với Định nghĩa 01.18, ba thành phần thay đổi và thứ tự lượng từ giữ nguyên." | chấp nhận; chưa sửa |
| 60 | nhẹ | §7, dòng 996 | công thức thay lời | Biến cố mô tả bằng lời. | Rủi ro vượt mức của $A(S)$ so với $\mathcal H$, tức hiệu trong Định nghĩa 01.5, không quá $\epsilon$. | "$L_D(A(S))-\inf_{h\in\mathcal H}L_D(h)\le\epsilon$ (rủi ro vượt mức so với $\mathcal H$), thay cho $L_D(A(S))\le\epsilon$." | chấp nhận; chưa sửa |
| 61 | trung bình | §7, dòng 1001 | khẳng định không căn cứ | Khẳng định về hàm lỗi không bị chặn không có chứng minh hay nguồn trong bài và không được dùng lại; "nói chung" là từ rào. | yêu cầu này cho mọi phân bố có rủi ro hữu hạn nói chung không thỏa được | Bỏ đoạn; nếu giữ, cần nguồn đã duyệt và điều kiện cụ thể thay cho "nói chung". | chấp nhận; chưa sửa |
| 62 | nhẹ | §8, Hệ quả 01.29, dòng 1049 | Giả thiết/Bảo đảm | Một hệ quả của thiết lập (có từ Mệnh đề 01.15(c)) được xếp vào giả thiết, kèm lời bình về phạm vi dùng; Bước 2 (dòng 1072) đã nêu điều này. | có từ Mệnh đề 01.15(c); chỉ phần (b) dùng thành phần này. | Bỏ gạch "**Tính khả diễn.**"; "Tám thành phần" thành "Bảy thành phần". | chấp nhận; chưa sửa |
| 63 | nghiêm trọng | §8, Hệ quả 01.29, dòng 1057 | trạng thái văn bản | Câu nói điều hệ quả không suy ra được (quy tắc 2026-11-04 trong `../CLAUDE.md`). | nhưng khẳng định đó cần một lập luận cho mọi thuật toán, không suy ra từ hệ quả này. | "Lớp $\mathcal M_{\mathcal X}$ với $\mathcal X=[0,1]$ không học được PAC; chứng minh cần một lập luận cho mọi thuật toán và nằm ngoài phạm vi học phần (UML §5.1)." | chấp nhận; chưa sửa |
| 64 | nhẹ | §8, Ví dụ 01.11, dòng 1088 | nhắc lại kết quả | Vế cuối nhắc lại dòng 1079 ("giữ nguyên nhãn hằng và thuật toán ghi nhớ") và gạch thiết lập ở dòng 1086. | nhãn vẫn hằng và thuật toán vẫn là $A_{\mathrm{gn}}$. | "So với Ví dụ 01.8, mỗi điểm của $\{1,\ldots,5\}$ là một nguyên tử có xác suất $0{,}2$." | chấp nhận; chưa sửa |
| 65 | nhẹ | §8, Ví dụ 01.11, dòng 1104–1106 | công thức một dòng | Dấu tổng tách khỏi số hạng của nó sang dòng sau. | &\quad=0{,}2\sum_{x=1}^5\\ | Một dòng "L_{D_1}(A_{\mathrm{gn}}(S))=0{,}2\sum_{x=1}^5\mathbb 1[x\notin\{X_1,\ldots,X_m\}]"; nếu tràn ở 390 px, ngắt trước "=". | chấp nhận; chưa sửa |
| 66 | nhẹ | §8, Ví dụ 01.11, dòng 1118 | nhắc lại kết quả | Câu đầu sau nhãn nhắc lại dòng 1113 và 1116. | Dưới $D_1$, toàn bộ khối lượng xác suất nằm trên năm nguyên tử, nên kì vọng của rủi ro bằng $0{,}8^m$ và tiến về $0$. | Giữ một câu, nối vào đoạn trước, bỏ nhãn: "Khẳng định $L_D(A_{\mathrm{gn}}(S))=1$ của Mệnh đề 01.15(b) vì vậy cần giả thiết không có nguyên tử." | chấp nhận; chưa sửa |
| 67 | nghiêm trọng | §8, Nhận xét 01.30, dòng 1122 | trạng thái văn bản | Câu nói mệnh đề "không chứng minh" một định lý, đúng mẫu "Chương không chứng minh định lý … nào" bị cấm (2026-11-04). | nên Mệnh đề 01.15 không chứng minh định lý không có bữa trưa miễn phí. | Thay hai câu cuối: "Mệnh đề 01.15 xét một thuật toán ERM cố định và một phân bố, dưới đó hàm hằng $h_{\equiv1}$ cũng là nghiệm ERM với rủi ro $0$; thất bại của $A_{\mathrm{gn}}$ đến từ quy tắc chọn khi bằng nhau." Hoặc đề xuất bỏ cả khối (không tự xóa; §12 dòng 1202 dẫn khối này). | chấp nhận; chưa sửa |
| 68 | trung bình | §8, dòng 1125 | công thức thay lời | Độ lệch đồng thời mô tả bằng lời; van-phong-tac-gia §6b: viết $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$. | cần kiểm soát $L_S(h)-L_D(h)$ đồng thời cho mọi $h\in\mathcal H$. | "… một bảo đảm cho ERM cần chặn $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$." | chấp nhận; chưa sửa |
| 69 | trung bình | §9, dòng 1134 | nghĩa tích cực | Đoạn liệt kê bốn điều định nghĩa không làm; "không xét thời gian tính" là nhận xét tác giả đã bỏ (van-phong-tac-gia §2 mục 4); "không áp dụng khi … không độc lập" là phủ định lồng. | Định nghĩa cũng không xét thời gian tính và không áp dụng khi các quan sát không độc lập cùng phân bố. | "Định nghĩa học PAC bảo đảm cho rủi ro kì vọng $L_D(A(S))$ của hàm học được, so với $\inf_{h\in\mathcal H}L_D(h)$, với xác suất theo $S\sim D^m$ khi các quan sát thỏa (T1). Phần chênh so với rủi ro Bayes không giảm theo $m$: dưới $D_\eta$, hiệu $\min_tL_{D_\eta}(h_t)-L^{\mathrm{Bayes}}_{D_\eta}=0{,}04$ với mọi $m$." Bỏ vế về thời gian tính. | chấp nhận; chưa sửa |
| 70 | trung bình | §9, dòng 1143 | Giả thiết/Bảo đảm | Một kết quả hình thức (cỡ mẫu đủ cho mọi phân bố khả diễn) phát biểu trong văn xuôi, không có **Giả thiết.**/**Bảo đảm.**, chứng minh dẫn sang bài tập ("được trình bày chi tiết trong Bài tập 01.9"). | cỡ mẫu $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$ đủ cho mọi phân bố khả diễn | Đưa vào khối "Mệnh đề 01.31 (Cỡ mẫu của $A_{\max}$ trên lớp hàm ngưỡng) — phác thảo" có Giả thiết/Bảo đảm (khối mới đứng sau Nhận xét 01.30 nên không đổi số khối nào); hoặc viết "Theo Bài tập 01.9, …" nếu master giữ ở mức đọc kết quả. Master quyết. | chấp nhận; chưa sửa |
| 71 | nhẹ | §11, lời giải, dòng 1187 | nghĩa tích cực | Câu cuối nhắc lại "Không." bằng một câu phủ định. | Nó không phải xác suất một dự đoán cụ thể đúng. | Bỏ câu. | chấp nhận; chưa sửa |
| 72 | nhẹ | §12, dòng 1201 | câu điều hướng | "§2.3.1 là phần mở đầu của Bài 02" là chú thích về bài sau; "đã chọn ở §10" là câu dẫn mục. | các bài tập UML §2.4 và §3.5 đã chọn ở §10 | "UML §2.3 (thiên kiến quy nạp), §§3.1–3.2 (…); các bài tập UML §2.4 và §3.5." | chấp nhận; chưa sửa |
| 73 | trung bình | §12, dòng 1204 | câu nguồn gốc | Câu nói nội dung "là của học phần" là câu nguồn gốc (bộ nhớ dự án "No provenance sentences"; `../CLAUDE.md`: nguồn gốc ghi vào `review-log.md`). | Các định nghĩa, kết quả và số hiệu ở đây là của học phần; UML được dẫn theo mục. | Bỏ câu; đổi nhãn thành "**Khác biệt so với UML.**"; danh sách năm khác biệt giữ hay bỏ do tác giả quyết. | chấp nhận; chưa sửa |
| 74 | nhẹ | Phụ lục A(i), dòng 1218 | lời bình kĩ thuật | Câu nói khi nào "chỉ cần" khả tích (loại "only needed so that …"). | Không cần khả tích ở bước này; khả tích chỉ cần khi trừ hai rủi ro hoặc khi dùng Mệnh đề 01.7. | Bỏ câu. | chấp nhận; chưa sửa |
| 75 | nhẹ | Phụ lục A(ii), dòng 1227 | nhắc lại kết quả | Vế so sánh với UML lặp lại dòng 1210. | UML chỉ đòi từng $\ell(h,\cdot)$ đo được. Điều kiện đó không đủ: | "Điều kiện từng $\ell(h,\cdot)$ đo được không đủ: …" | chấp nhận; chưa sửa |
| 76 | nhẹ | Phụ lục A(v), dòng 1247 | nhận xét bên lề | Lưu ý cho bài sau (hội tụ đều), không dùng trong Bài 01. | **(v) Lớp vô hạn.** Với một lớp vô hạn tổng quát | Bỏ mục (v), hoặc chuyển sang bài dùng $\sup_{h\in\mathcal H}\lvert L_S(h)-L_D(h)\rvert$. | chấp nhận; chưa sửa |
| 77 | nhẹ | Phụ lục B, Bước 4, dòng 1299 | phủ định kép | "không tệ hơn" là phủ định khi dạng khẳng định rõ hơn. | Dự đoán $1$ tại $x$ không tệ hơn dự đoán $0$ khi và chỉ khi | "Rủi ro có điều kiện của dự đoán $1$ tại $x$ nhỏ hơn hoặc bằng rủi ro có điều kiện của dự đoán $0$ khi và chỉ khi" | chấp nhận; chưa sửa |
| 78 | nhẹ | Phụ lục B, dòng 1308 | cấu trúc khó theo dõi | "mức thấp nhất mà mọi hàm phân lớp đạt được" có thể đọc là mọi hàm đều đạt mức đó. | Rủi ro Bayes là mức thấp nhất mà mọi hàm phân lớp đạt được | "$\square$ Rủi ro Bayes là cận dưới của rủi ro của mọi hàm phân lớp đo được, và cận này đạt được bằng một quy tắc ngưỡng trên $\eta(x)$; ngưỡng phụ thuộc hàm lỗi." | chấp nhận; chưa sửa |

### Thống kê theo quy tắc (theo báo cáo)

| Quy tắc | Số phát hiện | Số thứ tự |
|---|---|---|
| kiểu chữ | 9 | 1, 2, 3, 6, 8, 13, 14, 15, 45 |
| câu điều hướng | 8 | 9, 17, 38, 42, 50, 54, 57, 72 |
| nhắc lại kết quả | 8 | 20, 28, 44, 55, 58, 64, 66, 75 |
| thuật ngữ | 6 | 4, 5, 16, 27, 32, 52 |
| công thức thay lời (gồm $\sup$) | 6 | 25, 33, 34, 46, 60, 68 |
| cấu trúc khó theo dõi | 4 | 18, 39, 49, 78 |
| nghĩa tích cực | 4 | 26, 51, 69, 71 |
| công thức một dòng | 3 | 23, 53, 65 |
| Giả thiết/Bảo đảm | 3 | 41, 62, 70 |
| kí hiệu | 2 | 7, 22 |
| văn bản làm chủ ngữ | 2 | 11, 59 |
| câu dẫn công thức | 2 | 19, 35 |
| nhãn bước | 2 | 24, 48 |
| khẳng định không căn cứ | 2 | 29, 61 |
| định nghĩa trước khi dùng | 2 | 30, 56 |
| nhận xét bên lề | 2 | 43, 76 |
| trạng thái văn bản | 2 | 63, 67 |
| nhãn mục | 1 | 10 |
| rào đón | 1 | 12 |
| danh sách song song | 1 | 21 |
| định nghĩa nhiều thành phần | 1 | 31 |
| Giả thiết tập trung ở §2 | 1 | 36 |
| nhận xét hiển nhiên | 1 | 37 |
| ví dụ | 1 | 40 |
| nguồn trong thân bài | 1 | 47 |
| câu nguồn gốc | 1 | 73 |
| lời bình kĩ thuật | 1 | 74 |
| phủ định kép | 1 | 77 |
| **Tổng** | **78** | 0 chặn bàn giao, 4 nghiêm trọng, 15 trung bình, 59 nhẹ; 23 dòng VBTG (#1–#22, #45) |

## Sửa ghi chú theo bảng kiểm tuân thủ — quyết định của điều phối viên: **chấp nhận** (2026-11-13)

Yêu cầu của người dùng (2026-11-13): sửa ghi chú Bài 01–10 theo các nguyên tắc ghi chú hiện hành và theo bảng phát hiện trong `reviews/kiem-nguyen-tac-2026-11-13.md`.

**Tác tử** (theo lệnh gọi Agent): người sửa `general-purpose`, mô hình `opus` (Claude Opus 5.5), effort `high`, `no-ai-slop` chế độ Edit; người kiểm lại độc lập, chỉ đọc, `general-purpose`, `opus`, effort `high`, `no-ai-slop` chế độ Detect. Brief chung: không đánh số lại khối, không đổi con số, không sửa bốn điểm toán học trong `planning/diem-toan-can-doc-2026-11-13.md`; văn bản tác giả chỉ được sửa lỗi gõ, dấu câu, viết hoa, chính tả và được thêm nội dung mới không đổi chữ của tác giả.

**Kết quả của người sửa:** văn bản tác giả chỉ sửa dấu câu/viết hoa/chính tả ở #1, #2, #3, #6, #8, #13, #14, #15, #21 (dấu hai chấm). Chờ tác giả: #4, #5, #7, #9, #10, #11, #12, #16–#22 (phần đổi chữ), #45, #73; công thức cho (T1) trong #36. Không sửa: #23, #53, #65 (đo 390 px: bản một dòng tràn), #76 (Bài 02, Bài 03 dẫn Phụ lục A(v)). Mọi hàng khác đã sửa. Thêm vào văn bản tác giả (không đổi chữ nào): gạch $\inf$ ở Kiến thức tiên quyết (#30); §2 thêm bảng kí hiệu bổ sung ($L_S$, $\arg\min$, $\epsilon_{\mathrm{opt}}$), (O1), (O2) và giả thiết khả diễn, mỗi giả thiết một công thức (#36). Khối mới **Mệnh đề 01.31** (cỡ mẫu của $A_{\max}$ trên lớp hàm ngưỡng, phác thảo) ở §9, sau khối có số lớn nhất, không dịch số (#70); `outline.md` cập nhật. `exercises.md` không đổi.

**Kiểm của điều phối viên (lượt 1):** `forward_refs.py` 0; tiêu đề khối giống HEAD trừ Mệnh đề 01.31 và chứng minh của nó (đúng thứ tự đọc); 390 px: 0 công thức tràn.

**Kiểm lại độc lập:** kết luận `cần sửa`. Văn bản tác giả: đạt. Mệnh đề 01.31 dẫn lại đầy đủ và so với lời giải Bài tập 01.9(c): đúng (trường hợp biên $t^\star=K+1$, $k=K$; $\lceil10\ln20\rceil=30$). (O1), (O2), khả diễn khớp Định nghĩa 01.8, 01.12, 01.16; số đếm "Sáu", "Bảy" thành phần khớp danh sách. Hàng nghiêm trọng/trung bình của bảng gốc đã sửa đúng: #27, #28, #30, #31, #36, #41, #42, #54, #56, #57, #61, #63, #67, #68, #69, #70.

| mức độ | vị trí | vấn đề | quyết định |
|---|---|---|---|
| trung bình | Hệ quả 01.29 (câu sửa theo #63) | "nằm ngoài phạm vi học phần" sai: Bài 03 có Hệ quả 03.18, chứng minh đầy đủ | chấp nhận (điều phối viên kiểm `lec-03` dòng 851); đã sửa: "dựa trên định lý không có bữa trưa miễn phí (UML §5.1)" |
| nhẹ | Ví dụ 01.9 (#50) | thiếu lý do của $\mathbb EN=\sum_k\Pr(N\ge k)$; Phụ lục C.2 không còn ai dẫn | chấp nhận phần lý do; giữ C.2 |
| nhẹ | chứng minh Mệnh đề 01.31 | lược bước $\le(1-D_{\mathcal X}(C))^m$ và tính không giảm của $G$ | chấp nhận; đã sửa |
| nhẹ | Lộ trình Mệnh đề 01.31 | câu điều hướng sang lời giải Bài tập 01.9(c) | chấp nhận; đã bỏ |
| nhẹ | câu sau $\square$ của Mệnh đề 01.31 | nhắc lại **Bảo đảm.** | chấp nhận; đã sửa |
| nhẹ | Giả thiết Mệnh đề 01.31 | "với mọi tập con đo được" | chấp nhận; "với σ-đại số gồm mọi tập con" |
| nhẹ | §2 câu dẫn bảng bổ sung | giả thiết khả diễn không dùng kí hiệu của bảng; "nghiệm ERM" chưa giải nghĩa | chấp nhận; đã sửa, và tách giả thiết khả diễn khỏi danh sách giả thiết tối ưu (điều phối viên) |
| nhẹ | §9 (câu sửa theo #69) | "Định nghĩa" làm chủ ngữ; thiếu $\epsilon$, $\delta$ | chấp nhận; đã sửa |
| nhẹ | §7 (ii) | ngoặc dài | chấp nhận; đã sửa |
| nhẹ | `outline.md` | thiếu Mệnh đề 01.31 | chấp nhận; điều phối viên đã thêm |

**Lượt sửa 2 (cùng người sửa):** điều phối viên đọc lại các chỗ đổi: đúng; 390 px: 0 công thức tràn; `forward_refs.py` 0; `git diff --check` sạch.

**Còn mở cho tác giả:** các hàng văn bản tác giả nêu trên; công thức $S=(Z_1,\ldots,Z_m)\sim D^m$ cho (T1); câu "mỗi kí hiệu khác được đặt tên tại định nghĩa của nó" ở §2 nay đứng cạnh bảng kí hiệu bổ sung; gạch $\inf$ thêm vào Kiến thức tiên quyết; #73.

## Bộ trang chiếu (2026-11-15)

Yêu cầu của người dùng (2026-11-15): xây deck 01–10 từ ghi chú; deck tập trung trực quan, ý tưởng chứng minh, kỹ thuật, ví dụ bổ trợ, và thống nhất với ghi chú. Quy định: `CLAUDE.md` § Slide decks. Bản giao việc: `../tools/courses/statistical-learning-theory/2627-1/deck-build/`.

### Tác tử (ghi từ lời gọi công cụ)

| Vai | Loại | Mô hình | Effort | Đầu ra |
|---|---|---|---|---|
| Lập storyboard | general-purpose | opus (Opus 5.5) | high | `storyboard.md` |
| Duyệt cổng storyboard | general-purpose | opus (Opus 5.5) | high | `reviews/deck-storyboard-gate.md` |
| Viết deck | general-purpose | opus (Opus 5.5) | high | `lecture-01-mo-hinh-hoc.html`, `img/lec-01/`, cập nhật `storyboard.md` |
| Duyệt: học viên | general-purpose | opus (Opus 5.5) | high | `reviews/deck-hoc-vien.md` |
| Duyệt: toán học | general-purpose | opus (Opus 5.5) | high | `reviews/deck-toan-hoc.md` |
| Duyệt: chuyên gia | general-purpose | opus (Opus 5.5) | high | `reviews/deck-chuyen-gia.md` |
| Duyệt: sư phạm, no-ai-slop Detect | general-purpose | opus (Opus 5.5) | high | `reviews/deck-su-pham.md` |
| Duyệt: mạch truyện | general-purpose | opus (Opus 5.5) | high | `reviews/deck-mach-truyen.md` |
| Sửa deck (cùng tác tử viết deck, tiếp tục bằng SendMessage) | general-purpose | opus (Opus 5.5) | high | deck, `img/lec-01/`, `storyboard.md` |
| Kiểm lại lượt 1 | general-purpose | opus (Opus 5.5) | high | `reviews/deck-kiem-lai-1.md` |
| Kiểm lại lượt 2 (cùng tác tử kiểm lại, tiếp tục bằng SendMessage) | general-purpose | opus (Opus 5.5) | high | `reviews/deck-kiem-lai-2.md` |

### Quyết định của điều phối viên về storyboard và cổng duyệt

Điều phối viên tính lại V1–V16 (bảng rủi ro dưới $\ell_{0\text{-}1}$ và $\ell_c$, $L^{\mathrm{Bayes}}=0{,}18$ và $0{,}32$, cỡ mẫu $14$, $6$, $30$, $0{,}8^{10}$): đúng. Cổng duyệt: **đạt khi sửa** (0 chặn, 0 nghiêm trọng, 5 trung bình, 14 nhẹ). **Storyboard: chấp nhận khi sửa** theo bảng dưới; người viết deck áp dụng trực tiếp khi viết và cập nhật storyboard.

| Điểm | Quyết định | Lý do |
|---|---|---|
| Mục 11.1 hộp Vấn đề trung tâm | chấp nhận dạng "Câu hỏi:" | câu hỏi thật của bài, trang cuối trả lời |
| Mục 11.2 số trang | chấp nhận phương án (a) gộp 3-04 thành dòng "Kỹ thuật." trên 3-03, và (b) gộp 5-06/5-07; trần 55 trang | tính tuyến tính của kì vọng là kiến thức nền; (c), (d) vượt trần mật độ (cổng duyệt) |
| Mục 11.3 ví dụ mới V4 | chấp nhận | cách dựng: $D_f$, $m=1$, so $h_4$ cố định với $A_{\max}$; $\mathbb E L_S(h_4)=0{,}2=L_{D_f}(h_4)$, $\mathbb E L_S(A_{\max}(S))=0<0{,}36=\mathbb E L_{D_f}(A_{\max}(S))$, khớp $0{,}2(0{,}8^m+0{,}6^m+0{,}4^m)$ tại $m=1$ |
| Mục 11.4 tiếng Anh trên trang tổng quan | chấp nhận; đã ghi thành quy định | — |
| Mục 11.5 chính sách "Kỹ thuật." | chấp nhận; đã ghi thành quy định. Kỹ thuật có trang riêng ở Bài 01: bất đẳng thức hợp (4-04), chặn xác suất bỏ sót (6-06) | — |
| Mục 11.6 mạch 5 dài | chấp nhận | §6–§7 liên tiếp, tách sẽ thành 8 mạch |
| Mục 11.7 Hệ quả 01.29 | yêu cầu sửa: tách phát biểu và ý tưởng chứng minh thành hai trang | quy định "own slide" |
| Mục 11.8 bài tập chỉ từ `exercises.md` | chấp nhận; thêm một bài tập tổng hợp ở mạch 7 (người viết chọn từ `exercises.md`, ghi lựa chọn vào storyboard) | quy định mạch Tổng kết (cổng duyệt, nhẹ) |
| Mục 11.9 hình F4 | chấp nhận năm điểm; chú thích nêu dữ liệu ($m=5$, các $x_i$), không chữ "minh họa" | — |
| Mục 11.10 Mệnh đề 01.23 | chấp nhận; ghi chú diễn giả nói kết quả ở mức đọc thêm | — |
| Mục 11.11 "Diễn giải:" ở 3-08 | yêu cầu sửa: chuyển sang ghi chú diễn giả | quy định "Diễn giải:" chỉ dùng số trên trang |
| Mục 11.13 liên kết Bài 02 | chữ không liên kết; điều phối viên thêm liên kết khi deck 02 có tên tệp | — |
| Mục 11.14 / cổng #4 Mục tiêu | yêu cầu sửa: viết bằng lời, không kí hiệu | định nghĩa trước khi dùng |
| Cổng: 7-03 câu 4 | yêu cầu sửa: hỏi về thứ tự lượng từ ($14$ cho riêng $D_f$ so với $30$ cho mọi $D$ khả diễn), lời giải chỉ dùng ghi chú; bỏ đáp án "Không nhất thiết" | lời giải cũ yếu hơn sự thật; không đưa phân bố mới của người duyệt lên deck |
| Cổng: ghi chú diễn giả có mã nội bộ, câu quy trình | yêu cầu sửa | đã ghi thành quy định |
| Cổng: 3-04 tổng đuôi vô hạn | hết hiệu lực do gộp 3-04; nếu ghi chú diễn giả dùng $\mathbb E N=\sum_k\Pr(N\ge k)$ thì chỉ với $k=1,2,3$ như Phụ lục C.2 | — |
| Cổng: hình F5a/F5b | yêu cầu sửa: đáy trục log $0{,}001$ | dữ liệu xuống dưới $0{,}01$ |
| Cổng: 14 phát hiện nhẹ còn lại | chấp nhận tất cả | — |

**Đề xuất sửa ghi chú/bài tập cho tác giả (chưa sửa):** `exercises.md` dòng 73 có cụm nguồn gốc "(giá trị dựng để luyện tập)", trái quy tắc không ghi câu nguồn gốc; đề xuất bỏ cụm này. Đề xuất thêm câu $14\le m_{A_{\max}}(0{,}1;0{,}05)\le30$ sau Mệnh đề 01.31: không cần nữa (câu hỏi tự kiểm tra 4 đã đổi).

### Bản nháp deck và kiểm của điều phối viên trước khi duyệt

Người viết: 55 trang, chín SVG; áp dụng đủ bảng quyết định (lệch storyboard ghi ở `storyboard.md` mục 14). Điều phối viên chạy `deck_check.py`: console 0, pageerrors 0, failed 0, không `.katex-error`, không tràn; xem bảng ảnh 1600×900. Mật độ: nhiều trang 55–60 âm tiết, 7-01 (65, bảng tổng kết, trần 80) và 7-03 (73, bài tập tổng hợp) vượt mục tiêu; để năm người duyệt đánh giá. **Bản nháp: chấp nhận để duyệt**; đóng băng bản sao trong thư mục nháp của phiên.

### Năm báo cáo duyệt và quyết định của điều phối viên

| Báo cáo | Kết luận | Chặn | Nghiêm trọng | Trung bình | Nhẹ |
|---|---|---:|---:|---:|---:|
| `reviews/deck-hoc-vien.md` | đạt khi sửa | 0 | 0 | 5 | 18 |
| `reviews/deck-toan-hoc.md` | đạt khi sửa | 0 | 1 | 5 | 8 |
| `reviews/deck-chuyen-gia.md` | đạt khi sửa | 0 | 1 | 7 | 10 |
| `reviews/deck-su-pham.md` | đạt khi sửa | 0 | 0 | 6 | 36 |
| `reviews/deck-mach-truyen.md` | đạt khi sửa | 0 | 0 | 6 | 7 |

Điều phối viên đối chiếu các phát hiện nghiêm trọng với deck: dòng cuối 7-02 "$A_{\max}$ đạt bảo đảm khi $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$" đứng ngay dưới dòng bảo đảm bất khả diễn và thiếu "với mọi phân bố khả diễn"; Mệnh đề 01.31 của ghi chú chỉ nói trường hợp khả diễn. Hai báo cáo cùng thấy độc lập. **Chấp nhận.**

**Quyết định chung: chấp nhận mọi phát hiện của năm báo cáo**, trừ các điểm ghi dưới đây. Người sửa là người viết deck (cùng tác tử, tiếp tục bằng SendMessage).

| Phát hiện | Quyết định | Lý do |
|---|---|---|
| 7-02 và ghi chú diễn giả 1-05: thiếu "khả diễn" (toán học, chuyên gia, nghiêm trọng) | yêu cầu sửa: "với mọi phân bố khả diễn trên lớp hàm ngưỡng"; câu ghi chú diễn giả 1-05 dùng "khi", không "chỉ khi" | Mệnh đề 01.31 |
| Màn 390×844 thu nhỏ cả trang (học viên) | yêu cầu sửa: áp dụng chế độ đọc màn hẹp (commit 3e35346): bọc `.slides` trong `.lecture-viewport`, chép script của `lecture-template.html` | quy định mới "Narrow screens" |
| Quy ước đếm âm tiết (học viên) | số viết trong câu (ví dụ "01.15", "500") **có tính**; chỉ bỏ tiêu đề, KaTeX, số trong bảng, nhãn hình, ghi chú diễn giả. Các trang 5-01, 5-06, 6-02, 7-04, 7-06 rút về ≤ 60 | quy định mật độ của rl-plan chỉ miễn số trong bảng |
| 6-03: giả thiết vào ở phần nào (toán học, chuyên gia) | yêu cầu sửa: mặt trang nói đúng (cả hai phần dùng cả hai giả thiết của Mệnh đề 01.15); ghi chú diễn giả viết "Mệnh đề 01.15(a)/(b)" | không mâu thuẫn phát biểu Hệ quả 01.29 của ghi chú; câu chú thích trong chứng minh của ghi chú ghi vào đề xuất cho tác giả |
| ERM xấp xỉ, $\epsilon_{\mathrm{opt}}$, (O1)/(O2) không có trên mặt trang (chuyên gia) | yêu cầu sửa: một dòng trên 3-04 nếu mật độ cho phép, nếu không thì trong ghi chú diễn giả 3-04 | Bài 05 dùng lại (O2) |
| Dòng dẫn mạch cùng khuôn "Người học … được" (sư phạm) | yêu cầu sửa: dòng dẫn nêu thẳng ý cốt lõi mạch đem lại, dạng câu trần thuật về nội dung (mẫu của tác giả: "Tác tử chọn hành động, môi trường cho phản hồi."), không bắt đầu bằng "Người học" | quyết định tác giả 2026-11-14 dòng 4 |
| Ghi chú diễn giả trang tiêu đề mạch theo khuôn "Kế thừa:/Nhiệm vụ:/Kết quả trao đi:" | yêu cầu sửa: câu thường, bỏ nhãn | văn phong |
| 7-05 bảng `Mục | Bài tập` (mạch truyện) | yêu cầu sửa: xếp mỗi bài vào mạch cung cấp kiến thức cuối cùng nó cần | — |
| "Ký hiệu:" | yêu cầu sửa: "Kí hiệu:"; "lôgarit" | chính tả của ghi chú (quy định nhãn đã sửa) |
| `review-log.md` mục 11.5 ghi trang chặn xác suất bỏ sót là 6-06 | ghi chú: ở deck cuối là 6-07 | — |
| 5-06 đứng sau Ví dụ 01.9 dù Nhận xét 01.19 đứng trước trong ghi chú | giữ | bài tập dùng $m\ge14$ của Ví dụ 01.9 |

**Đề xuất sửa ghi chú và bài tập cho tác giả (chưa sửa, cộng dồn):**
1. Chứng minh Hệ quả 01.29 (ghi chú dòng ≈ 1086): câu gán giả thiết cho phần (a)/(b) chưa đúng (cả hai phần dùng cả hai giả thiết của Mệnh đề 01.15); viết "Mệnh đề 01.15(a)/(b)" để khỏi lẫn với phần của hệ quả.
2. Dòng ≈ 1135: "cần chặn sup" đọc như điều kiện cần, trong khi Mệnh đề 01.31 cho bảo đảm không qua chặn sup; đề xuất "một cách đủ là chặn sup".
3. Dòng ≈ 966, 979: "chỉ phụ thuộc lớp" nên là "phụ thuộc $D$ và lớp".
4. Nhận xét 01.19: "khoảng 95 lần" → "ít nhất khoảng 95 lần" (tùy tác giả).
5. Dòng 84, 776: "mini-batch" → "lô nhỏ (mini-batch)" theo `thuat-ngu.md`.
6. `exercises.md` dòng 73: bỏ cụm "(giá trị dựng để luyện tập)".
7. Tùy tác giả: câu "lớp hàm ngưỡng học được PAC" sau Mệnh đề 01.31; dòng "Mục ghi chú: §k" cho từng bài trong `exercises.md`.

### Sửa sau năm báo cáo và quyết định của điều phối viên

Người sửa: 107/110 phát hiện đã sửa, 3 không sửa (bảng từng phát hiện ở `storyboard.md` mục 15). 55 trang, mã trang không đổi; chế độ đọc màn hẹp đã áp dụng; `deck_check.py`: console 0, pageerrors 0, failed 0, `.katex-error` 0; trang không cuộn ngang ở 390 px.

| Điểm | Quyết định | Lý do |
|---|---|---|
| HV13, MT10: trang "Kỹ thuật." đứng sau trang ý tưởng chứng minh (4-03/4-04, 6-06/6-07) | bác bỏ phát hiện (giữ thứ tự) | thứ tự hành trình khái niệm: ý tưởng chứng minh → kỹ thuật; thêm công thức vào 4-03 làm tràn khung |
| SP42 "mini-batch" | không sửa trên deck | deck theo ghi chú; đề xuất sửa ghi chú số 5 |
| HV20, CG3, MT7: ý chỉ đưa được vào ghi chú diễn giả | chấp nhận | mặt trang ở trần mật độ |
| Mật độ: 1-01 (63), 7-03 (65) vượt 60 | chấp nhận ngoại lệ đã ghi trong storyboard | trang bìa có câu luận điểm; bài tổng hợp có "Lời giải:" trên mặt, deck ở trần 55 trang |
| Chữ trong hình rộng F1, F2, F5 ở 390 px còn ≈ 11–12 px | chấp nhận, ghi là giới hạn còn lại | hình co theo bề rộng màn hẹp; vẽ lại dạng đứng nằm ngoài phạm vi lượt này |

Chuyển sang kiểm lại độc lập (toán và mạch truyện trên phần đã đổi).

### Kiểm lại lượt 1 và quyết định

`reviews/deck-kiem-lai-1.md`: **đạt khi sửa**; hai phát hiện nghiêm trọng và 29 phát hiện trung bình đã sửa đúng; 77/79 nhẹ đã sửa. Còn mở: 1 trung bình (nội dung chạm đáy khung ở 1600×900: 6-03, 2-04 do biên tập; 7-01, 6-05 có từ trước) và 9 nhẹ (trong đó 6-07/alt `can-co-mau.svg` so $6$ với $30$ là trộn hai giá trị $\epsilon$). **Quyết định: yêu cầu sửa** cả 10 điểm, cộng đối chiếu "$>\epsilon$" ở 7-06 với ghi chú (do người duyệt mạch truyện Bài 02 nêu). Gửi lại cùng người sửa (lượt 2).

### Kiểm lại lượt 2 và quyết định

`reviews/deck-kiem-lai-2.md`: **đạt khi sửa**; mười điểm lượt 1 đã sửa đúng; `footer_check.py` 0 trang; toán đúng trên trang đổi. Còn mở: 1 trung bình (tiêu đề cột 7-01 "Giả thiết then chốt" lệch quy định) và 4 nhẹ (hàm chỉ báo ở 1-02; "($C$ ngắn nhất)" ở 6-06; $S=(z_1,\ldots,z_m)$ ở 2-01; bảng 7-01 ở 390 px). **Quyết định:** yêu cầu sửa ba điểm nội dung và tiêu đề cột (lượt sửa 3); bảng ở 390 px sửa chung trong `lecture-course.css` (ô bảng `min-width: 4.5em`, commit 56b2226), điều phối viên đo lại: trang không cuộn ngang, bảng cuộn tại chỗ. Về "$>\epsilon$" ở 7-06: ghi chú Bài 01 dòng 1250 viết $\Pr(\lvert L_S-L_D\rvert>\epsilon)$, deck theo ghi chú; Bài 02 viết "$\ge\epsilon$" trong ngữ cảnh của nó; ghi vào đề xuất cho tác giả (thống nhất cách viết giữa hai ghi chú, tùy tác giả).

### Sửa lượt 3 và kiểm cuối của điều phối viên — chấp nhận (2026-11-15)

Lượt 3 (người sửa): tiêu đề cột 7-01 trả về "Giả thiết không được bỏ" (độ rộng cột đặt bằng `<colgroup>` để tiêu đề vừa một dòng, không thêm CSS); 1-02 thêm "hàm chỉ báo (indicator function) $\mathbb 1[\cdot]$"; 6-06 "($C$ ngắn nhất)"; 2-01 $S=(z_1,\ldots,z_m)\sim D^m$. Điều phối viên đọc bốn dòng đổi trong HTML: đúng như yêu cầu, không đổi nội dung toán.

**Kiểm cuối (điều phối viên tự chạy):**
- `deck_check.py --shots` (55 trang): console 0, pageerrors 0, failed 0, `.katex-error` 0; OVERFLOW 0; ở 390 px trang không cuộn ngang (cờ NARROW-H chỉ là công thức/bảng cuộn tại chỗ). Mật độ ≤ 60 trừ 1-01 (luận điểm, ngoại lệ đã ghi), 1-03 (80), 7-01 (69), 7-03 (65, ngoại lệ đã ghi).
- `footer_check.py` (1600×900): 0 trang.
- Ảnh 1600×900 mọi trang (bảng ảnh) và 390×844 kể cả ảnh `-end`: đã xem; bảng 7-01 ở 390 px cuộn tại chỗ sau sửa CSS 56b2226.
- Bàn phím: →, ↓, Space, ← chuyển đúng trang; Esc bật chế độ tổng quan. Sáu liên kết `#/2`…`#/7` của 1-04 đã được người duyệt mạch truyện và người sửa kiểm.
- Trang chỉ mục: thẻ Bài 01 liên kết deck; ghi chú và bài tập mở với `&deck=lecture-01-mo-hinh-hoc.html`, viewer hiện liên kết deck, 0 `.katex-error`, 0 lỗi tải.

**Kết luận của điều phối viên: chấp nhận deck Bài 01.** Giới hạn còn lại: chữ trong hình rộng ≈ 11–12 px ở 390 px; trang 7-06 nêu Bài 02 bằng chữ, liên kết thêm khi deck 02 được duyệt. Đề xuất sửa ghi chú/bài tập cho tác giả: mục "Năm báo cáo duyệt…" (7 điểm) và "$>\epsilon$" ở ghi chú dòng 1250 so với "$\ge\epsilon$" của Bài 02.

### Việc nhỏ còn lại sau xuất bản (ghi 2026-11-16)

`deck_lint.py` (viết sau khi deck 01 được duyệt) báo 7 mục nhẹ trên bản xuất bản: ghi chú diễn giả 151–177 âm tiết ở 1-02, 4-06, 5-12, 6-02, 7-04 (khuyến nghị ≤ 150, không phải trần); dòng dẫn 7-00 27 âm tiết (trần 25); 7-03 65 âm tiết (ngoại lệ đã chấp nhận). Để sửa trong một lượt dọn cuối, sau deck 10 (người sửa → kiểm lại các trang đổi ±2).

Lượt dọn cuối (2026-11-16): người sửa (`general-purpose`, `opus`, effort `high`, theo lệnh gọi Agent) xử lý; kiểm lại (cùng cấu hình, `planning/deck-cleanup-recheck-2026-11-16.md`): **đạt** (0/0/0/1 nhẹ, không bắt buộc). Ghi chú diễn giả 1-02 (151 → 148), 4-06 (154 → 140), 5-12 (177 → 149), 6-02 (161 → 149), 7-04 (151 → 146): bỏ câu lặp mặt trang, câu dẫn chỗ và bình luận kỹ thuật; không mất số, điều kiện hay lời giải. Dòng dẫn 7-00: "Học là chọn hàm có rủi ro gần tốt nhất trong lớp với xác suất cao, từ một cỡ mẫu không phụ thuộc phân bố." (25 âm tiết, bám định nghĩa học của ghi chú; điều phối viên bác bản trung gian "Học là đạt rủi ro …" vì mất "chọn hàm"). `deck_lint.py`: chỉ 7-03 (ngoại lệ); `footer_check.py` 0. **Chấp nhận.**
