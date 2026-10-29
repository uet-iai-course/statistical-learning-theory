# Rà bài tập — sư phạm, văn phong, thuật ngữ (`no-ai-slop` Detect) (2026-10-30)

Không có lỗi chặn bàn giao; 1 nghiêm trọng (độ dài), 10 trung bình, 14 nhẹ. Văn phong sạch (không câu hỏi tu từ ngoài đề, không lời khen, không "rõ ràng/dễ thấy", không "hãy"); thuật ngữ chính đúng; mọi số hiệu dẫn tới ghi chú đều tồn tại; không có dấu hiệu dịch hay chép bản lời giải. Định dạng khối đạt (11 exercise, 31 hint, 11 solution; tiêu đề thống nhất; mọi lời giải kết bằng "Kiểm tra lại.").

**Kiểm tra của điều phối viên:** "thiên kiến quy nạp" không xuất hiện trong tệp bài tập (0 lần); `thuat-ngu.md` dùng "afin" — điều phối viên đã đổi "affine" → "afin" trong ghi chú.

| mức độ | vị trí | vấn đề | đề xuất sửa |
|---|---|---|---|
| nghiêm trọng | cả tệp | 10 724 tiếng so với kế hoạch 4 500–6 500 (lời giải 6 660, đề 2 340, gợi ý 1 160). | Cắt theo danh sách dưới (≈ 1 700 → ≈ 9 000); dưới 6 500 cần bỏ phần mở rộng ngoài kế hoạch hoặc người dùng chỉnh chỉ tiêu. |
| trung bình | tiêu đề 01.6–01.11 | Không khớp §10 của ghi chú. | Dùng đúng tên §10: "### Bài tập 01.9 (Lớp hình tròn đồng tâm và lớp hàm ngưỡng; UML Bài tập 3.3)". |
| trung bình | 01.1(a) | "Tám thành phần của §1" đếm khác §1 (gộp $\mathcal X,\mathcal Y$; có "Tài nguyên"). | Ghi đúng danh sách của §1. |
| trung bình | 01.3, 01.5(d), 01.2(a), 01.9(c), 01.2(c) | Đề chưa tự đứng: $D_f$ không nhắc lại; 01.5(d) dùng $S_f$, $A_{\max}(S_f)$ không nêu dữ kiện; $A_{\min}$/$A_{\max}$ chỉ định nghĩa cho 5 mức; "đẳng thức phân tích rủi ro vượt mức ở §7" không viết ra. | Thêm câu dữ kiện mỗi chỗ; viết công thức phân tích. |
| trung bình | mục tiêu 5; 01.4, 01.6(c) | Vế "vì sao cần thiên kiến quy nạp" không được đo. | 01.6(c): "giải thích bằng khái niệm thiên kiến quy nạp (§5) vì sao bậc không bị chặn làm mất bảo đảm"; lời giải 1–2 câu. |
| trung bình | mục tiêu 3; 01.3 | Vế "chứng minh tính không chệch" chỉ đo gián tiếp. | Thêm ý ngắn "chứng minh lại Mệnh đề 01.5 khi các $Z_i$ chỉ cùng phân bố, không độc lập", hoặc ghi trong outline rằng (d) thay thế. |
| trung bình | 01.5 Gợi ý 1 | Lộ đáp án (a) (viết sẵn dòng lượng từ và quy tắc phủ định). | Gợi ý 1 chỉ nói hướng. |
| trung bình | 01.11 Gợi ý 1 | Đưa luôn bước then chốt. | Gợi ý 1: "tính rủi ro có điều kiện tại một $x$ cố định như một hàm của $h(x)$"; công thức sang Gợi ý 2. |
| trung bình | 01.2 G3, 01.4 G3, 01.5 G2–G3, 01.8 G3, 01.11 G3 | Gợi ý xếp theo phần, không theo độ mạnh. | Mở mỗi gợi ý bằng "Phần (c)." hoặc thang riêng mỗi phần. |
| trung bình | 01.4(c), 01.11(d), 01.9(c), 01.8, 01.6 | Kí hiệu trùng: $\delta_0$ (với $\delta$), $\eta_0$ (với $\eta_t$, $\eta(x)$), $s$ "mức lớn nhất" (với mẫu $s$), $p_z$ (với $p$), $P$ số đếm vs $P(s)$ tập. | "khối lượng điểm tại 0" bằng lời; $\eta_0\to q$; $s\to k$; $p_z,n_z\to a_z,b_z$; $P(s)\to F_1(s)$. |
| trung bình | toàn tệp | Không có tiếng Anh ở lần đầu; thuật ngữ mới chưa có trong `thuat-ngu.md`; "(UML gọi là lớp singleton)" sai định dạng. | "lớp hàm chỉ thị của một điểm (class of singletons)", "lớp đa thức có ngưỡng (thresholded polynomials)", "hàm dự đoán xác suất (probabilistic label predictor)", "bao hàm–loại trừ (inclusion–exclusion)"; báo cho điều phối viên để bổ sung bảng. |
| trung bình | nhiều đoạn 7–11 câu | Đoạn dài hơn 5 câu. | Tách theo một khẳng định mỗi đoạn. |
| nhẹ | L3, L18, L50, L580, L704, L733 | Câu > 40 tiếng. | Tách. |
| nhẹ | L3 | $D_1$ thừa; ERM, PAC chưa giới thiệu dạng đầy đủ. | Bỏ $D_1$; thêm "(ERM)", "học PAC". |
| nhẹ | L265, 267, 284 | "rủi ro kì vọng có kì vọng 0,16" | "kì vọng theo mẫu của rủi ro kì vọng là …". |
| nhẹ | L18, 40, 52 | "giả định" | "giả thiết". |
| nhẹ | 01.2(c) | "hàm Bayes" | "hàm phân lớp tối ưu Bayes" lần đầu, sau đó "quy tắc Bayes". |
| nhẹ | L757, L778 | "affine" | "afin". |
| nhẹ | L224 | "hai sự kiện" | "hai tính chất". |
| nhẹ | L18 | "tập giá trị" | "miền giá trị". |
| nhẹ | L694 | "cách làm quen thuộc với phân bố liên tục" (ám chỉ bản lời giải) | "như khi $D_{\mathcal X}$ liên tục". |
| nhẹ | L680 | "ảnh gương" | Nói thẳng vị trí vùng lỗi. |
| nhẹ | L64 | Câu kết kiểu cách ngôn | "ngưỡng tăng theo $c_{FP}$". |
| nhẹ | Kiểm tra lại 01.10, 01.11 | Không phải phép kiểm tra. | Thay bằng phép thử hoặc lỗi thường gặp. |
| nhẹ | 01.7(c) | Dẫn tới bài sau (01.9(c)). | Phản ví dụ $\mathcal H=\{h_-\}$, $M\equiv1$. |
| nhẹ | Mức độ 01.4, 01.9 | Thiếu "kiểm tra giả thiết". | Thêm. |

**Bao phủ mục tiêu:** 1 đủ (01.1); 2 đủ (01.2, 01.1(d), 01.11); 3 một phần (01.3); 4 đủ (01.5, 01.7–01.10); 5 một phần (thiếu thiên kiến quy nạp). Mức độ nghiêng về chứng minh (9 bài).

**Danh sách cắt (≈ 1 700 tiếng):** 01.1 lời giải (a) thành bảng 3 cột, bỏ câu thừa (~250); 01.2 bỏ câu tính mẫu, gộp công thức, bỏ lặp ở Kiểm tra lại và Gợi ý 2 (~150); 01.3 (d) dẫn lại (a), bỏ câu thừa (~120); 01.4 (~130); 01.5 Gợi ý 1 và câu lặp (~135); 01.6 phần đo được một dòng (~80); 01.7 (~60); 01.8 bỏ công thức tổng quát, bảng băm, 0,2441, $m\ge44$, so sánh $A_{\mathrm{sg}}/B$ (~180); 01.9 (c) áp dụng (b) thay vì chứng minh lại (~250); 01.10 (~90); 01.11 (~165); L3 (~25); gộp công thức bị bẻ quá nhỏ (~80). Phần mở rộng ngoài kế hoạch: 01.9(d) ~270, 01.11(d) ~280, nửa sau 01.8(c) ~350, 01.2(d) ~350 (dữ liệu gốc của kế hoạch), 01.3(c) ~250.
