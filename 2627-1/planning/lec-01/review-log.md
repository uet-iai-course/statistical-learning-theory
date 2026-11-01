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
