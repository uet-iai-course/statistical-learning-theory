# Rà soát 5 — mạch và móc nối (2026-10-30)

Số tiếng (`wc -w`): thân bài 12 645, phụ lục 953; theo mục §3 972, §4 1 728, §5 2 280, §6 1 646, §7 1 477, §8 947, §9 470, §10 394, §11 412. Câu hỏi mở đầu được trả lời ở cuối Ví dụ 01.6 (phần đầu), đoạn mở §6 và đầy đủ ở §11.

**Kiểm tra của điều phối viên:** T1 đúng (không có câu "học nghĩa là…"); T2 đúng (dòng 523: "thuật toán học không biết $\eta$, nên đối tượng so sánh … là $\inf_{\mathcal H}$" — thuật toán cũng không biết $\inf_{\mathcal H}L_D$).

Bảng vai trò các mục: thứ tự chung đúng (khả thực §6 → bất khả tri §7 → giới hạn §8), ví dụ xen giữa các kết quả, $D_\eta$/$D_f$ tách rõ (ngoại lệ dòng 365), đoạn kết §3–§5 tốt, cầu nối sang Bài 02 chính xác.

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | T1 · đoạn dẫn, cuối §7, đầu §9 | Câu hỏi trung tâm "Học nghĩa là gì?" không được phát biểu; luận điểm không có câu trả lời tường minh. | Không có câu "học nghĩa là…"; đoạn kết §7 chỉ nói "đã đủ để phát biểu một bảo đảm học". | Đoạn dẫn nêu câu hỏi trung tâm; cuối §7 thêm 2–3 câu trả lời theo luận điểm của outline: rủi ro kì vọng không vượt mức tốt nhất trong $\mathcal H$ cộng $\epsilon$, với xác suất ≥ $1-\delta$ theo mẫu, khi $m$ vượt một ngưỡng không phụ thuộc phân bố; rủi ro thực nghiệm nhỏ tự nó không bảo đảm điều đó (§8). |
| nghiêm trọng | T2 · §7: cuối chứng minh Mệnh đề 01.20 (dòng 523), sau Định nghĩa 01.21, sau Định nghĩa 01.22 | Lý do chọn $\inf_{\mathcal H}L_D$ thay cho $L_D^{\mathrm{Bayes}}$ rải ba chỗ, một phần sai ("không biết $\eta$"). Lý do thật chỉ xuất hiện ở dòng 556. | | Bỏ vế "không biết $\eta$". Gom vào một đoạn ngay trước Định nghĩa 01.22: (i) học đúng lớp không vượt được $\inf_{\mathcal H}$, khoảng 0,04 của Ví dụ 01.9 không giảm theo $m$; (ii) ngay cả học ngoài lớp, mốc Bayes không bảo đảm được cho mọi $D$ khi $\mathcal X$ vô hạn với cỡ mẫu đều theo $D$ (UML §5.1; xem rà soát 3); (iii) vậy $\inf_{\mathcal H}$ là mốc mạnh nhất đạt được không phụ thuộc phân bố, giá phải trả là số hạng xấp xỉ (thiên kiến quy nạp, §5). Rút câu dòng 556 về một câu trỏ lại. |
| trung bình | T3 · §11 dòng 662 | Câu hỏi mở đầu trả lời bằng chuỗi sự kiện, không nói điều đó thành gì trong ngôn ngữ PAC. | dừng ở "rủi ro của một nghiệm ERM có thể bằng 1" | Thêm: không quy tắc nào chọn đúng $h_3$ trên mọi mẫu; bảo đảm hứa xác suất gặp mẫu kiểu $S_f$ đủ nhỏ ($0{,}8^m\le0{,}05$ khi $m\ge14$, Ví dụ 01.8) và phải đúng cho mọi $D$. |
| trung bình | T4 · Định nghĩa 01.18 | Dùng Định nghĩa 01.22 trước khi xuất hiện. | dòng 440, 444 | Ở §6 chỉ phát biểu cho khả thực; sau Định nghĩa 01.22 thêm một câu mở rộng. |
| trung bình | T5 · Nhận xét 01.7, Ví dụ 01.6 | Nhận xét 01.7 dùng tập nghiệm ERM và "rủi ro vượt" trước khi có; 0,273 xuất hiện ba lần (Nhận xét 01.7, Ví dụ 01.6, Phụ lục C.4). | dòng 289, 324–326 | Nhận xét 01.7 giữ phần nguyên tắc ($\Pr$ theo $S$ và $\xi$, SGD ở Bài 05), trỏ tới Ví dụ 01.6; trong Ví dụ 01.6 cột "$L_{D_\eta}(h)-0{,}22$" chưa đặt tên, Định nghĩa 01.21 gọi lại. |
| trung bình | T6 · Nhận xét 01.5 | Dùng hai cặp số chưa chứng minh (Mệnh đề 01.13, Ví dụ 01.8); Ví dụ 01.8 lại trỏ ngược, thành vòng. | dòng 273, 466 | Giữ khẳng định tổng quát và cách sửa bằng mẫu độc lập; thay cặp số bằng "Mệnh đề 01.13 và Ví dụ 01.8 sẽ cho hai trường hợp cụ thể". |
| trung bình | T7 · §5: Định nghĩa 01.12, Ví dụ 01.7 | ERM xấp xỉ chen giữa Thuật toán 01.11 và câu nối dẫn vào Mệnh đề 01.13. | dòng 313, 349–365 | Đặt Định nghĩa 01.12 và Ví dụ 01.7 ngay sau Nhận xét 01.10; rồi Ví dụ 01.6, Thuật toán 01.11, câu nối, Mệnh đề 01.13. |
| trung bình | T8 · cuối §7 → đầu §8 | Đoạn kết §7 nêu chỗ thiếu "thuật toán nào, cỡ mẫu bao nhiêu", §8 trả lời câu khác. | dòng 570, 574 | Viết lại: ứng viên tự nhiên là ERM, Mệnh đề 01.13 đã cho thấy ERM trên lớp quá giàu không đạt; §8 nói chính xác điều đó; câu hỏi định lượng để Bài 02. |
| trung bình | T9 · §9 đoạn 4 | Cận $\lceil\ln(1/\delta)/\epsilon\rceil=30$ "cho mọi phân bố khả thực" đã là độ phức tạp mẫu không phụ thuộc phân bố, làm yếu cầu nối và làm trước việc Bài 02. | dòng 630, 664 | Bỏ hoặc rút còn một câu trỏ Bài tập 01.9 (cận một chiều không mở rộng được; Bài 02 cho phương pháp chung). |
| trung bình | Độ dài | Thân bài 12 645 so với trần 10 500; tổng ≈ 13 600 so với ≈ 12 000. | | Danh sách cắt dưới đây. |
| nhẹ | N1 · cuối §6 | Câu kết không nói đã có được gì. | dòng 471 | Mở bằng: đã có định nghĩa và một phép tính chính xác cho một phân bố. |
| nhẹ | N2 · cuối §8 | "Kiểm soát đồng thời mọi giả thuyết" chưa giải thích tại chỗ. | dòng 620 | Thêm "vì $\hat h$ chọn theo $S$ (Nhận xét 01.5)". |
| nhẹ | N3 · Định nghĩa 01.8, Hệ quả 01.26 | Câu dẫn Định nghĩa 01.8 là biển chỉ đường; Hệ quả 01.26 không gọi tên khoảng cách tổng quát hóa. | dòng 292, 577 | Câu dẫn từ Nhận xét 01.5; gọi tên trong giả thiết của Hệ quả 01.26. |
| nhẹ | N4 · Ví dụ 01.1, khối application §3 | Tính sẵn $L_{D_f}=0{,}2(\hat t-3)$ và nêu trước ngưỡng Bayes có trọng số, trái outline. | dòng 137, 155 | Chuyển công thức sang Ví dụ 01.8; khối application chỉ trỏ Ví dụ 01.3 và Mệnh đề 01.20(b). |
| nhẹ | N5 · dòng 365 | Không nêu phân bố của cặp 0,22/0,32. | | "trên $S_\eta$, dưới $D_\eta$". |
| nhẹ | N6 · cầu nối §11 | Phát biểu như kế hoạch, chưa nối câu hỏi mở đầu của Bài 02. | dòng 664 | Kết bằng câu hỏi "Không biết $D$, cần bao nhiêu quan sát để…, khi $\mathcal H$ hữu hạn?"; gắn hai tình huống ($h$ cố định trên mẫu độc lập; $\hat h$ chọn từ $\lvert\mathcal H\rvert$ ứng viên). |
| nhẹ | N7 · `outline.md` mục 2, 4, 5 | Outline còn số phương án B. | | Điều phối viên đổi outline sang số A. |

## Danh sách cắt (≈ 1 900 tiếng, theo thứ tự giá trị)

1. Chứng minh Mệnh đề 01.20 ([O], 319 tiếng) chuyển vào Phụ lục B, gộp với "tính không duy nhất" và "rủi ro Bayes"; thân bài giữ lộ trình hai câu và câu kết (≈ 280). Lệch outline, cần điều phối viên chấp nhận; nếu không, rút còn ≈ 170 tiếng.
2. §10: mỗi bài chỉ số, tên, mục tiêu đo (≈ 200).
3. §9: đoạn 1 chỉ giữ phân biệt bảo đảm lớp/thuật toán; đoạn 3 bỏ phần lặp Nhận xét 01.5; đoạn 4 theo T9; đoạn 5 rút một mệnh đề (≈ 165).
4. Gom các câu "khác UML" thành một đoạn "Khác biệt với UML" ở §12, mỗi chỗ cũ giữ "(bổ sung của học phần)" (≈ 120).
5. Mệnh đề 01.13: giả thiết trỏ "Thiết lập của Ví dụ 01.2"; Bước 4 trích thay vì viết lại; bỏ câu kết trùng (≈ 100).
6. §8: đoạn mở nói trước Bảo đảm; gộp Bước 1 vào Bước 2; giả thiết Hệ quả 01.26 chép lại thiết lập; câu đầu Nhận xét 01.27 (≈ 120).
7. Ví dụ 01.1: chuyển công thức $L_{D_f}$ sang Ví dụ 01.8, bỏ câu cuối lặp bảng §1 (≈ 85).
8. Nhận xét 01.7 và 01.5: bỏ minh họa bằng số (≈ 115).
9. Khối application: bỏ phần nêu trước ngưỡng Bayes (≈ 55).
10. Đoạn sau Định nghĩa 01.18: hai câu (≈ 50).
11. Ví dụ 01.3 đoạn cuối: một mệnh đề (≈ 30).
12. Còn lại (≈ 250): đoạn sau Định nghĩa 01.12; Cauchy–Schwarz của Ví dụ 01.4 một dòng; phần không duy nhất trong Bảo đảm của Mệnh đề 01.20; câu $A_{\min}$ ở Ví dụ 01.8; đoạn kết §5 dòng 403; Nhận xét 01.19 và 01.23; câu hỏi mở đầu đoạn 3; Ví dụ 01.10.

Mọi yếu tố bắt buộc vẫn còn sau các cắt. **Nhận định:** khung mạch tốt; không có lỗi chặn bàn giao; hai lỗi nghiêm trọng (T1, T2) sửa được bằng ≈ 150 tiếng ở cuối §7.
