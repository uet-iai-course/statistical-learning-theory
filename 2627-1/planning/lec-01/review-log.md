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

## Nguồn đã tham khảo

UML (trang PDF): 33–53 (§2.1–2.4, §3.1–3.5), 60–64 (Ch. 5 mở đầu, §5.1, đầu §5.2); tìm từ khóa trên tr. 1–130. Bản lời giải: tr. 1–8 (Ch. 2–3), chỉ để kiểm tra độ khó và chỗ thiếu.

## Phát hiện rà soát — vòng 1 (2026-10-30)

Năm báo cáo trong `reviews/1-hoc-vien.md`, `2-toan-hoc.md`, `3-chuyen-gia-nguon.md`, `4-hoc-thuat-van-phong.md`, `5-mach.md`. Không có lỗi chặn bàn giao. Phát hiện nghiêm trọng (sau khi gộp trùng): thiên kiến quy nạp trên ví dụ rời rạc (rà soát 1, 2); $A_{\max}/A_{\min}$ định nghĩa hai lần (1, 2, 4); thiếu điều kiện $\mathcal X$ vô hạn ở câu Bayes $+\epsilon$ (2, 3, 5); câu hỏi trung tâm không được trả lời tường minh (5); lý do chọn $\inf_{\mathcal H}$ rải và một phần sai (5); "chấp nhận được" hai nghĩa (1, 4); định nghĩa độ phức tạp mẫu dẫn trước và $m_A$ hai nghĩa (1); lý thuyết độ đo không có trong tiên quyết (1); độ dài vượt khoảng 20% (1, 5). Mọi con số đều đúng (rà soát 2).

Điều phối viên đã kiểm lại trên văn bản và bằng tính toán: 2/32 hàm khớp $S_f$; câu dòng 523 ("không biết $\eta$"); câu UML tr. 44 về $m_{\mathcal H}$; câu UML tr. 43–44 bị diễn ý; $S=((1,0),(4,1))$ cho $A_{\min}\to h_2$; tính duy nhất của quy tắc Bayes dưới $D_\eta$; kì vọng $0{,}8^m$ và $0{,}6\cdot0{,}8^m$ cùng tốc độ; hai ví dụ thay thế (mẫu $((1,0),(3,1),(5,1))$; phân bố $Y\equiv1$, $0{,}8^{10}\approx0{,}107$).

**Quyết định:** `reviews/0-quyet-dinh.md` (chấp nhận mọi phát hiện nghiêm trọng và trung bình, trừ các mục hoãn sang bước bài tập; 20 quyết định nội dung; mục tiêu thân bài ≤ 11 000 tiếng).
