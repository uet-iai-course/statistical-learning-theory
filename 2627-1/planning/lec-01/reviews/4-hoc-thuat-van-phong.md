# Rà soát 4 — học thuật, sư phạm, văn phong và thuật ngữ (`no-ai-slop` Detect) (2026-10-30)

Kiểm đếm tự động không có vi phạm: không có "phân phối", "kỳ vọng", "hàm mất mát", "ký hiệu", "bất kỳ", "tỷ lệ", "-hoá", "đạo hàm", "học thuộc", "rủi ro tổng thể"; không "hãy", "rõ ràng", "dễ thấy", "tất nhiên", "chúng tôi", dấu chấm than; câu hỏi chỉ ở câu hỏi mở đầu/cuối buổi; giả thiết/giả thuyết đúng nghĩa; đánh số 01.1–01.27, Ví dụ 01.1–01.10, Bài tập 01.1–01.11 đúng thứ tự.

**Kiểm tra của điều phối viên:** phát hiện về Ví dụ 01.10 đúng (hai kì vọng cùng tốc độ $0{,}8^m$, hằng số khác khoảng 3 lần); phát hiện "chấp nhận được" trùng với rà soát 1.

## 1. Văn phong
| mức độ | vị trí | vấn đề | đề xuất sửa |
|---|---|---|---|
| trung bình | toàn bài | ≈ 25 câu trên 40 tiếng (dài nhất ≈ 68), 11 đoạn trên 4 câu (có đoạn 7 câu); `van-phong.md` §9 | Tách câu tại ";" và "nên …"; tách đoạn $A_{\max}/A_{\min}$ (dòng 137) thành ba đoạn; tách Nhận xét 01.15 thành hai đoạn. Ví dụ: dòng 3 (55 tiếng), 434 (48), 582 Bảo đảm (b) Hệ quả 01.26 (≈ 68), 659 (49). |
| trung bình | dòng 11 câu hỏi mở đầu | Chuyển đột ngột sang chi phí bất đối xứng, "Như vậy" khép một ý không do đoạn dẫn tới | Giữ đoạn cho câu hỏi đã đặt (rủi ro 0 so với 0,2); chuyển ý chi phí sang tình huống sàng lọc/Ví dụ 01.3. |
| trung bình | dòng 613 (Ví dụ 01.10, câu kết) | "chậm hơn" sai: cùng tốc độ $0{,}8^m$, hằng số gấp ≈ 3; "tổng quát hóa" dùng như nội động từ; "thật sự" | "kì vọng rủi ro của hàm phân lớp ghi nhớ giảm cùng tốc độ $0{,}8^m$, với hằng số lớn gấp khoảng ba lần; với phân bố có nguyên tử này, kết luận rủi ro bằng $1$ của Mệnh đề 01.13 không còn đúng." |
| trung bình | dòng 13, 61, 143, 155 | Mật độ con trỏ tới phần sau quá cao (3–4 con trỏ/câu) | Mỗi chỗ tối đa một con trỏ; bỏ câu lộ trình ở dòng 13. |
| nhẹ | dòng 3, 162, 276, 574 | "chính xác" lặp như nhịp quen | Bỏ ở 3, 276, 574. |
| nhẹ | dòng 188, 617; "rất giàu/đủ giàu/quá giàu" | Khẩu ngữ "đáng giá", "quy tắc chọn tồi"; "lớp giàu" chưa định nghĩa | "giảm rủi ro"; "một quy tắc chọn khi bằng nhau cụ thể"; "lớp chứa mọi hàm phân lớp đo được". |
| nhẹ | dòng 193 và 204 | Một ý nói hai lần quanh Ví dụ 01.4 | Bỏ một câu; kết ví dụ bằng điều kiện mô-men. |
| nhẹ | dòng 117, 155, 181, 533 | Lời rào "giá trị minh họa" lặp 4 lần | Nói một lần ở dòng 117. |
| nhẹ | dòng 289 | "vượt quá … không quá" rối; nối hai mệnh đề độc lập bằng dấu phẩy | "Hàm trả về có rủi ro vượt mức so với $\mathcal H$ không quá $0{,}05$ chỉ khi chọn $h_3$, tức với xác suất $\tfrac13$ theo $\xi$." |
| nhẹ | dòng 427–429 | Dòng lượng từ là công thức inline đứng riêng sau câu nhãn | Đưa thành công thức hiển thị nằm trong câu. |
| nhẹ | toàn bài | Ít "ta" trong phép tính so với sách | Tùy chọn: "Theo …, ta có …" ở vài bước chứng minh. |

## 2. Mẫu cấm (`no-ai-slop`)
| mức độ | vị trí | vấn đề | đề xuất sửa |
|---|---|---|---|
| trung bình | dòng 155, 289, 359, 434, 451, 626, 696 | Lời bình về nguồn gốc nội dung với "học phần" làm chủ ngữ ("đây là bổ sung của học phần"…) | Viết thành nội dung toán ("UML không đưa $\xi$ vào định nghĩa; ở đây xác suất lấy theo cả $S$ và $\xi$"); gom ghi chú khác biệt với UML vào §12 hoặc `review-log.md`. |
| trung bình | dòng 676 | "Phụ lục này ghi…" (văn bản làm chủ ngữ) | Mở bằng nhu cầu: "Các định nghĩa học PAC chỉ có nghĩa khi các biến cố trong dấu $\Pr$ đo được; ba điều kiện dưới đây bảo đảm điều đó." |
| trung bình | dòng 292 | Dẫn đường thay cho nhu cầu ("Các bài sau chặn…") | "Nhận xét 01.5 cho thấy $\mathbb E_S[L_S(A(S))]$ có thể khác $\mathbb E_S[L_D(A(S))]$; hiệu giữa hai rủi ro của hàm học được cần một tên riêng." |
| nhẹ | dòng 3 (câu cuối), 110, 628 | Câu dẫn đường, nói tầm quan trọng | Bỏ câu cuối dòng 3; rút dòng 110 còn một câu; dòng 628 mở thẳng bằng quyết định đầu tiên. |
| nhẹ | dòng 401 | "cho thấy vai trò" không nói vai trò gì | "Trong Mệnh đề 01.13, lớp $\mathcal H$ chứa hàm phân lớp ghi nhớ; chọn lớp hàm ngưỡng trước khi thấy mẫu loại hàm đó." (kết hợp sửa của rà soát 1). |
| nhẹ | dòng 13 | "Câu trả lời hấp dẫn nhưng sai là:" | Có thể giữ (theo blueprint); hoặc "Một lập luận sai thường gặp cho rằng…". |
| nhẹ | dòng 143, 586, 630, 664 | Vật vô tri làm động từ của người ("đọc", "làm việc đó") | "phát biểu lại", "chứng minh", "cho thấy". |

## 3. Thuật ngữ
| mức độ | vị trí | vấn đề | đề xuất sửa |
|---|---|---|---|
| nghiêm trọng | dòng 440 (Định nghĩa 01.18), 549 (Định nghĩa 01.22) | "Chấp nhận được" hai nghĩa, dùng trước định nghĩa; không có tiếng Anh; chưa có trong `thuat-ngu.md` | Định nghĩa 01.18 viết tường minh họ $\mathcal D$ cho từng thiết lập; nếu giữ tên, chỉ một nghĩa, định nghĩa sớm (sau Nhận xét 01.2), thêm "(admissible)"; hoặc thay bằng "phân bố có rủi ro hữu hạn" (tự giải thích, không đụng "admissible" của lý thuyết quyết định). |
| trung bình | dòng 398, 574, 577, 582, 590 | "lựa chọn ERM" là tên thứ tư; "cận tổng quát hóa cho mọi lựa chọn ERM" dài | Dùng "thuật toán ERM": "*cận tổng quát hóa cho mọi thuật toán ERM*". |
| trung bình | dòng 289, 314, 359 và toàn bài | "UML" không bao giờ viết đầy đủ; "Ch." | Lần đầu viết đầy đủ tên sách, tác giả, năm, "viết tắt UML"; "Chương". |
| trung bình | dòng 127, 176 | "Bản bất khả tri" gán thuộc tính thiết lập học cho một phân bố | "*Bản có nhiễu* (không khả thực), phân bố $D_\eta$". |
| trung bình | dòng 56, 536, 542 | "mốc tham chiếu", "mốc so sánh" thay cho "đối tượng so sánh" đã chốt | "đối tượng so sánh". |
| nhẹ | dòng 380 | "Sự kiện then chốt" (dễ lẫn "biến cố") | "Tính chất then chốt". |
| nhẹ | dòng 448 | "cực tiểu" chỉ dành cho điểm cực tiểu | "giá trị nhỏ nhất". |
| nhẹ | dòng 468, 613, 719, 730 | "khối lượng" chưa giới thiệu | "khối lượng xác suất (probability mass)" lần đầu; thêm vào bảng. |
| nhẹ | dòng 468, 626 | "Cận đúng" lẫn với sup/inf; "khoảng cách 0,04" lẫn với khoảng cách tổng quát hóa | "một cận có hiệu lực với mọi phân bố"; "hiệu $0{,}04$". |
| nhẹ | dòng 242, 488, 624 | "đại lượng tổng thể" chưa có trong bảng | Thêm vào `thuat-ngu.md`. |
| nhẹ | dòng 13, 367, 372, 401, 620; mục tiêu 5 | Biến thể trôi: "hàm ghi nhớ", "nghiệm ERM ghi nhớ", "ERM ghi nhớ" | Hai tên cố định: "thuật toán ghi nhớ $A_{\mathrm{gn}}$" và "hàm phân lớp ghi nhớ $A_{\mathrm{gn}}(S)$". |
| nhẹ | Định nghĩa 01.14 | Tiêu đề "Giả thiết khả thực" nhưng định nghĩa tính chất "khả thực" | Tiêu đề "Tính khả thực", thêm "(realizable)". |
| nhẹ | nhiều chỗ | Tiếng Anh không ở lần dùng đầu: rủi ro vượt mức, xác suất thất bại, bất khả tri, không chệch, thiên kiến quy nạp, độ phức tạp mẫu; không bao giờ có tiếng Anh: bất đẳng thức tập trung, tính chất tháp, hàm lỗi log, cận dưới đúng, hạ gradient ngẫu nhiên (SGD), bất đẳng thức hợp, hội tụ đều | Thêm tiếng Anh ở lần đầu trong thân bài (`van-phong.md` §10). |
| nhẹ | dòng 549 | "*thuật toán học PAC bất khả tri* (agnostic PAC learning)" gắn sai đối tượng | Chuyển tiếng Anh sang cụm "học được PAC bất khả tri". |
| nhẹ | dòng 582; Nhận xét 01.15; $n_y(x)$ | $\varepsilon$ gần trùng $\epsilon$; dùng $n$ (học phần tránh) | Đổi hàm cận thành $\beta$; chỉ số $k$; $c_y(x)$. |
| nhẹ | dòng 730 | Tiêu đề C.2 lệch cách gọi đã chốt | "C.2 Kì vọng theo mẫu của rủi ro kì vọng của $A_{\max}$ dưới $D_f$". |
| nhẹ | dòng 173 | "giá trị dự đoán dương (precision)" chưa có trong bảng | Thêm vào `thuat-ngu.md`. |

## 4. Sư phạm
| mức độ | vị trí | vấn đề | đề xuất sửa |
|---|---|---|---|
| trung bình | Mục tiêu 2 so với §10 | Không bài tập nào đo "rủi ro Bayes, rủi ro vượt mức; ngưỡng tối ưu khi chi phí bất đối xứng" | Mở rộng Bài tập 01.2 với bảng $\eta(x)$ mới: $h_{\mathrm{Bayes}}$ dưới $\ell_{0\text{-}1}$ và $\ell_c$, rủi ro vượt mức so với $\mathcal H$ và so với Bayes; hoặc thêm vào câu hỏi phụ cuối buổi. |
| trung bình | dòng 137, 347 | $A_{\max}$ đổi nghĩa giữa bài (trùng rà soát 1) | Định nghĩa một lần cho mọi mẫu; dạng tường minh dưới $D_f$ là hệ quả. |
| trung bình | dòng 409–431, 475–479, 401 | Rủi ro Bayes chỉ định nghĩa trong văn xuôi; thiên kiến quy nạp chỉ một câu, không phản ví dụ | Khối `definition` cho rủi ro Bayes (có thể gộp vào Định nghĩa 01.21); thiên kiến quy nạp thêm phản ví dụ $\mathcal M_{\mathcal X}$ (Ví dụ 01.2). |
| nhẹ | Ví dụ 01.7, 01.2 | Thiếu câu cuối nói ví dụ chứng tỏ gì | Thêm một câu. |
| nhẹ | §10 | Liên kết `exercises.md` chưa có tệp | Kiểm tra khi có tệp. |
| nhẹ | dòng 648 | Bài tập 01.11 mô tả mơ hồ | Nêu cụ thể yêu cầu UML 3.8 ý cuối. |

## 5. Quy ước khối
| mức độ | vị trí | vấn đề | đề xuất sửa |
|---|---|---|---|
| trung bình | Mệnh đề 01.13, Hệ quả 01.26 | Dòng "Giả thiết." chứa định nghĩa mới ($A_{\mathrm{gn}}$; "cận tổng quát hóa …") | Định nghĩa $A_{\mathrm{gn}}$ trước Mệnh đề 01.13 (hoặc trong Ví dụ 01.2); khối `definition` riêng cho cận trước Hệ quả 01.26 (đổi số các khối sau). |
| trung bình | dòng 99–106 | Nhãn (T1)–(T4), (O1) không được kết quả nào dẫn | Dẫn nhãn trong dòng "Giả thiết." hoặc bỏ nhãn. |
| nhẹ | dòng 40, 656 | Đáp án ôn nhanh và lời giải cuối buổi nằm trong khối `hint` | Dùng `::: solution Lời giải câu hỏi ôn nhanh` / `… cuối buổi`. |
| nhẹ | Mệnh đề 01.13 vs 01.20, Hệ quả 01.26 | Ý Bảo đảm đánh 1–3 và (a)(b) không thống nhất | (a)(b)(c) thống nhất, sửa các trích dẫn. |
| nhẹ | dòng 440 | Định nghĩa 01.18 mở bằng "Cố định" | "Cho …". |
| nhẹ | dòng 548 | Một khối định nghĩa hai khái niệm | Tách "chấp nhận được"/"rủi ro hữu hạn" ra đặt sớm hơn. |
| nhẹ | dòng 591–596, 732–735 | `aligned` cho một quan hệ | Công thức hiển thị thường. |

**Đạt:** mỗi định nghĩa chính có đoạn đọc lại, ví dụ, phản ví dụ; ví dụ xen giữa kết quả; có trường hợp bỏ giả thiết; có cận bằng số; bốn phát biểu hình thức đủ Giả thiết/Bảo đảm; tiêu đề có số, tên, độ sâu; chứng minh có lộ trình, chỗ dùng giả thiết, $\square$ và câu ý nghĩa. **Nhận định:** gần văn phong sách ở các điểm cốt lõi; khác rõ nhất ở độ đặc (câu, đoạn dài), con trỏ tới phần sau, lời bình nguồn gốc. Một phát hiện nghiêm trọng ("chấp nhận được"); không có lỗi chặn bàn giao.
