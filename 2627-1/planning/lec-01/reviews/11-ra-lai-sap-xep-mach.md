# Rà lại sau tái cấu trúc — thứ tự, mạch, liên kết (2026-10-30)

`forward_refs.py`: 0. Đọc tuần tự: không còn chỗ dùng trước định nghĩa trong thân bài (ba điểm ranh giới nhỏ: B1, B8, B9). Không có lỗi chặn bàn giao hay nghiêm trọng. Ba yêu cầu của người dùng: (1) đạt; (2) đạt phần lớn (thiếu B2); (3) đạt.

| mức độ | vị trí | vấn đề | đề xuất sửa |
|---|---|---|---|
| trung bình | B1. §2 dòng 72, 77 | Bảng kí hiệu còn $\mathcal M_{\mathcal X}$; câu dẫn "dùng ngay từ ví dụ ở §3" sai (dùng lần đầu ở Ví dụ 01.8, §5). | Bỏ dòng khỏi bảng §2; định nghĩa $\mathcal M_{\mathcal X}$ ngay trước hoặc ở đầu Ví dụ 01.8. |
| trung bình | B2. Định nghĩa 01.5, đoạn đọc (dòng 228), dòng 474–476 | "$D$ chưa biết" chưa thành hệ quả hình thức: $A$ chọn trước, không phụ thuộc $D$, nên yêu cầu phải đúng với mọi $D$; lượng từ $\forall D$ của học PAC không được nối về Định nghĩa 01.5. | Thêm vào Định nghĩa 01.5: "$A$ được chọn trước khi lấy mẫu và không phụ thuộc $D$, nên yêu cầu phải đúng với mọi $D$ có thể xảy ra"; đoạn đọc: "…nhỏ đến đâu, với xác suất nào theo $S$, và cho những $D$ nào"; dòng 476: "lượng từ $\forall D$ đứng sau $\exists A\,\exists M$ là cách viết hình thức của việc $D$ chưa biết trong Định nghĩa 01.5". |
| trung bình | B3. Định nghĩa 01.5 dòng 221; `thuat-ngu.md` | "bài toán học thống kê" chưa có trong bảng; ngoặc ghi hai tên tiếng Anh; dùng xen "bài toán học". | Một tên tiếng Anh "(statistical learning problem)"; thống nhất "bài toán học thống kê" hoặc nói một lần "bài toán học" là tên rút gọn; điều phối viên thêm vào `thuat-ngu.md`. |
| nhẹ | B4. Định nghĩa 01.5 dòng 223 | "$\ge0$" trong công thức dễ đọc nhầm thành điều kiện; định nghĩa không dùng "tối thiểu hóa". | Chỉ hiển thị hiệu; "(hiệu này không âm vì $A(S)\in\mathcal H$)"; thêm "Mục tiêu là tối thiểu hóa rủi ro kì vọng trên $\mathcal H$ khi không tính được $L_D$." |
| nhẹ | B5. Dòng 476 | Câu về thuật toán ngẫu nhiên ghép vào đoạn nối không liên quan. | Tách đoạn riêng hoặc đặt sau dòng 474. |
| nhẹ | B6. Dòng 501, 635 | "tất định" thừa. | Bỏ ở hai chỗ; giữ ở dòng 57, 63, 709. |
| nhẹ | B7. Dòng 441 | Không nói đây là phần tiếp của câu trả lời câu hỏi mở đầu. | Thêm nửa câu. |
| nhẹ | B8. Dòng 77, 82, 86, 146 | "đo được", "σ-đại số" dùng trước "Đọc lần đầu". | Đưa "Đọc lần đầu" lên trước bảng §2 hoặc chuyển "(measurable)" về dòng 77. |
| nhẹ | B9. Dòng 102–118 | $D_\eta$, $D_f$, $f$ trong bảng trước câu định nghĩa. | Gọi tên ngay ở câu dẫn dòng 102. |
| nhẹ | B10 | Câu > 40 tiếng ở văn mới/chuyển chỗ: dòng 3 (52), 84 (59), 604 (48), 315 (43), 677 (41), 711 (43). | Tách. |
| nhẹ | B11 | Đoạn 6 câu: dòng 228, 441, 474, 579. | Tách (228 gộp với B2). |
| nhẹ | B12. Dòng 437 | Colon reveal cụt "Thiên kiến quy nạp có giá: …". | "Lớp giả thuyết có thể không chứa hàm dự đoán tốt nhất; đó là giá của thiên kiến quy nạp." |
| nhẹ | B13. Cuối §3 | Kết trong khối `application`, không câu kết văn xuôi. | Tùy chọn: một câu "Câu hỏi về ngưỡng cần rủi ro kì vọng và quy tắc Bayes; §4 định nghĩa rủi ro." |

Đạt: liên kết sau khi chuyển chỗ (dòng 210, 218, 236, 302, 315, 327, 441, 476, 592, 604); không câu mồ côi; bảng §1 hai dòng khớp các dẫn chiếu; câu kết §4–§8; không còn $\xi$; không văn bản làm chủ ngữ, không "hãy"; số hiệu bài tập dẫn khớp.
