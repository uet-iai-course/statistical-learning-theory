# Rà soát 5 — mạch và móc nối (Bài 02, bản đóng băng 2026-10-30)

Người rà độc lập, chỉ đọc (general-purpose, opus, high). Đã đọc toàn văn, blueprint §A và Lecture 2–4, `van-phong.md` §2, §6, §8, `outline.md`, §8–§12 của Bài 01 và mọi chỗ "Bài 02" trong Bài 01. `forward_refs.py`: 0. Không có lỗi chặn bàn giao.

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | cuối §6, §7, §8 (dòng 729, 848, 950) | Ba mục kết thúc bằng một khối, không có câu văn xuôi kết mục (CLAUDE.md; van-phong §8) | `:::` rồi `## 7.`; `:::` rồi `## 8.`; `:::` rồi `## 9.` | Sau Nhận xét 02.15: Định lý 02.14 chưa so $L_D(\hat h)$ với $\min L_D$; sau Ví dụ 02.10: $1097$, $1431$ tỉ lệ $1/\epsilon^2$; sau Nhận xét 02.18: điều bài chưa trả lời |
| trung bình | dòng 410 | "mọi cỡ mẫu dưới đây nhân thêm $(b-a)^2$" quá rộng (Mệnh đề 02.17 chỉ 0–1) | — | Chỉ các cỡ mẫu dựa trên Định lý 02.7; với $\ell_c$ hệ số $16$ |
| trung bình | §1, §2, Ví dụ 02.1 | $\ell_c$ nhắc ba lần như danh mục, thân bài không tính gì; $D_f$, $\mathcal M_{\mathcal X}$ cũng nêu sớm (xung đột QĐ 1 với quy tắc định nghĩa trước khi dùng) | dòng 70, 99; dùng duy nhất dòng 410 | Bỏ $\ell_c$ khỏi phần đầu, giới thiệu ở dòng 410; có thể chuyển $D_f$ sang §8, $\mathcal M_{\mathcal X}$ sang §7 |
| trung bình | Hệ quả 02.16(c) | $\epsilon$ đổi nghĩa (độ lệch → mức rủi ro vượt mức) không báo; ba nghĩa chỉ nói ở Ví dụ 02.12 | "$2r_m\le\epsilon$" | Một câu sau Hệ quả 02.16 và sau Mệnh đề 02.17 |
| trung bình | ranh giới §5/§6 (dòng 531, 569, 573) | Cùng ý "Hệ quả 02.10 chỉ cho $h$ cố định" nói ba lần liền | ba câu trích | Bỏ một hoặc hai câu, hoặc đưa Ví dụ 02.6, Nhận xét 02.11 lên sau Định lý 02.7 |
| trung bình | Ví dụ 02.4 Bước 3, Kết luận | "Hoeffding có thể kém Chebyshev" dễ đọc thành Chebyshev tốt hơn ở $\delta$ thường dùng; Chebyshev không phụ thuộc phân bố chỉ thắng khi cận còn trên khoảng $0{,}23$ | $0{,}25$ so với $0{,}2707$; $738$ so với $2000$ | Nói rõ phạm vi; ở $\delta=0{,}05$ Hoeffding cần ít hơn |
| trung bình | Nhận xét 02.18; §9 cuối | Hứa Bài 03 cho cận dưới; blueprint Bài 03 chỉ phát biểu định lý cơ bản, hoãn chứng minh tính cần | "một cận dưới phải lập luận cho mọi thuật toán (Bài 03)" | "Bài 03 phát biểu, không chứng minh…" hoặc bỏ số bài |
| trung bình | §9; §11 | Câu hỏi trung tâm và câu hỏi mở đầu không được khép lại ở cuối bài | dòng 954–964 | Mở §9 bằng một câu ghép bốn cỡ mẫu và nhắc $8{,}9\%$ / $12\%$ |
| nhẹ | §8 | Bốn khối liền nhau không có câu dẫn | dòng 907–909, 946–948 | Câu dẫn trước Ví dụ 02.12 và Nhận xét 02.18 |
| nhẹ | §9 đoạn 3–4, cuối | Lặp con số của Ví dụ 02.4, Nhận xét 02.11, 02.18 | — | Dẫn số khối thay vì chép số |
| nhẹ | Khối ứng dụng và Ví dụ 02.8 Bước 1 | Lập luận lấy điều kiện viết hai lần | — | Giữ chi tiết ở Ví dụ 02.8 |
| nhẹ | Ví dụ 02.3 Bước 5, Ví dụ 02.4 Bước 4 | Cỡ mẫu Chebyshev tính ở hai độ lệch khác nhau | $500$ so với $2000$/$100\,000$ | Dùng cùng độ lệch $0{,}1$ ($500$, $25\,000$ so với $185$, $381$) |
| nhẹ | §5 | 2 842 tiếng so với dự toán 2 400 | — | Cắt phản ví dụ đuôi nặng, phép kiểm số, rút Nhận xét 02.8 |
| nhẹ | §4→§5 | $\alpha$ → $\epsilon$ cho cùng độ lệch không báo | "$\alpha=0{,}1$" và "$\epsilon=0{,}1$" | Nửa câu trước Định lý 02.7 |
| nhẹ | dòng 470, 511, 652 | "bán kính" dùng trước khi có tên tiếng Anh | — | Đặt "bán kính tin cậy (confidence radius)" ở Hệ quả 02.10 |
| nhẹ | Ví dụ 02.9, 02.11 | $A_{\min}$, $A_{\max}$, $S_\eta$ không nhắc nghĩa | dòng 803, 898, 900 | Dòng trong bảng §2 |
| nhẹ | chữ $k$ | Bốn nghĩa | Ví dụ 02.2, 02.7 | Đổi chỉ số ở Ví dụ 02.7 |
| nhẹ | Cầu nối | "nửa không gian" thiếu tiếng Anh | dòng 1003 | "(halfspace)" |
| nhẹ | Nhận xét 02.11, §9 | "Bài 05–06": hàm lỗi không bị chặn được xử lý ở Bài 06 | blueprint 6.3–6.4 | "Bài 06, với hàm lỗi lồi, Lipschitz trên miền bị chặn" |
| nhẹ | Liên tục với Bài 01 | Bài 01 viết "$>\epsilon$", Bài 02 chốt "$\ge$" không nói | Bài 01 dòng 998 | Nửa câu ở dòng 134 |
| nhẹ | §10 | `exercises.md` chưa tồn tại (đúng quy trình) | — | Người viết bài tập giữ đúng 11 tên |

**Đã kiểm, không có vấn đề:** đủ 15 thành phần (không có thuật toán); câu hỏi mở đầu được trả lời ở Ví dụ 02.5 và 02.8; giả thiết (T3), (T4), (O1)/(O2), khả thực nêu đúng chỗ; mọi lời hứa của Bài 01 được giữ (Ví dụ 02.6, Nhận xét 02.11, Ví dụ 02.10, §7–§8, Nhận xét 02.15, Hệ quả 02.16(c), §12); cầu nối sang Bài 03 cụ thể, không nói trước chiều VC; ví dụ sàng lọc và ứng dụng mẫu xác thực đi suốt bài, trừ $\ell_c$.

**Bản đồ mạch (tóm tắt):** §4 cần chặn độ lệch → Markov, Chebyshev → cần mọi mô-men; §5 → Hoeffding, cận tin cậy, hai phản ví dụ → chỉ cho $h$ cố định; §6 → bất đẳng thức hợp, Định lý 02.14, $12\%$ → (thiếu câu chuyển); §7 → Hệ quả 02.16, $1097$, $1431$ → (thiếu); §8 → khả thực, $48/30/14$, bảng $K$ → (kết bằng khối); §9–§12 khớp thân bài.

**Kết luận của người rà:** mạch chính chặt chẽ; một lỗi nghiêm trọng về kết mục; đề xuất yêu cầu sửa các mục trung bình.
