# Duyệt deck Bài 05 — Vai 5: mạch truyện và liên kết (2026-11-15)

Bản duyệt: `2627-1/lecture-05-ha-gradient-ngau-nhien.html` (đóng băng, 55 trang). Đối chiếu: `materials/lec-05/lecture-note.md`, `exercises.md`, `planning/lec-05/storyboard.md` (mục 3, 7, 12, 14, 16), quyết định cuối `review-log.md` mục "Bộ trang chiếu", deck Bài 01–04. Chỉ đọc; không sửa deck, hình, storyboard, ghi chú.

## Kiểm tra máy đã chạy

- `deck_lint.py`: 1 phát hiện, `L05-7-04 | SYLL60 | 68 > 60` (ngoại lệ đã được điều phối viên chấp nhận).
- Playwright (1600×900, máy chủ `localhost:8766`): `#/2`…`#/7` mở đúng `L05-2-00`…`L05-7-00`; bấm từng liên kết trên `L05-1-04` cũng tới đúng sáu trang tiêu đề mạch. Hai liên kết viewer trên `L05-7-07` (`lecture-note.md`, `exercises.md`, cả hai có `&deck=lecture-05-ha-gradient-ngau-nhien.html`) trả 200, tiêu đề đúng Bài 05, viewer hiện liên kết "Bộ trang chiếu" trỏ về deck này, không có yêu cầu lỗi, console không lỗi.
- Script nháp (thư mục nháp của vai): liệt kê nhãn khối và số hiệu được dẫn trên từng mặt trang; kiểm từ khóa mạch có trên mặt trang nội dung của mạch.
- Trang Bài 06 ở `L05-7-08` là dòng chữ, không liên kết, giống dòng "Bài 05: …" của deck 04 (`L04-7-07`); tên khớp tiêu đề ghi chú Bài 06.

## Bảng chức năng từng trang và đối chiếu trang → mục ghi chú

| Trang | Mục ghi chú | Vai trò trong mạch | Kết nối vào | Kết nối ra |
|---|---|---|---|---|
| 1-01 | đoạn mở, §7, §11 | bìa, luận điểm | Bài 04 (ghi chú diễn giả) | 1-05 |
| 1-02 | Tiên quyết | nhắc lại $\operatorname{opt}_S$, (O2), sai số ước lượng, (T1), Markov, tính chất tháp | Bài 01, 02, 04 | 3-07 (tháp), 6-03 (Markov), 7-01 (sai số ước lượng); (O2) không dùng lại trên mặt trang |
| 1-03 | Mục tiêu học tập | năm mục tiêu | — | mạch 2–6 |
| 1-04 | toàn bài, §14 | mục lục `#/2`…`#/7` | — | các trang tiêu đề mạch |
| 1-05 | đoạn mở | một hộp "Câu hỏi:" | — | 7-03 |
| 1-06 | Câu hỏi mở đầu, §3 khối ứng dụng | ví dụ dẫn nhập, câu hỏi thực hành | 1-05 | 3-05 (số ba quan sát), 4-09 (lời đáp $10^4$ bước) |
| 2-00 | §1–§4 | tiêu đề mạch | 1-06 | 2-02 |
| 2-01 | §1, §3 (Ví dụ 05.1) | thiết lập, ví dụ xuyên suốt | 1-06 | 2-04, 3-03 |
| 2-02 | §4 (Định nghĩa 05.1) | vấn đề (0–1, bản lề), trực quan, định nghĩa, lồi hữu hạn | 2-00 | 2-03, 4-04 bước 5 |
| 2-03 | §4 (Định nghĩa 05.2) | dưới gradient, dưới vi phân, hình | 2-02 | 2-04 |
| 2-04 | §4 (Mệnh đề 05.3, Ví dụ 05.3) | quy tắc tính; trung bình của gradient rút đều | 2-03, 2-01 | 2-05, 3-03, 6-03 |
| 2-05 | §4 (Ví dụ 05.2) | ví dụ bản lề | 2-04 (c) | 2-06, 2-07 |
| 2-06 | §4 (Định nghĩa 05.4, Mệnh đề 05.5) | $G$ chặn chuẩn dưới gradient | 2-05 | 3-01 (cận $G$ cần tập bị chặn) |
| 2-07 | Bài tập 05.1(d) | bài tập | 2-04 (b), 2-05 | — |
| 3-00 | §5–§6 | tiêu đề mạch | 2-06 | 3-01, 3-03 |
| 3-01 | §5 (Định nghĩa 05.7, Ví dụ 05.4) | vì sao chiếu; định nghĩa; số | 2-06 | 3-02 |
| 3-02 | §5 (Bổ đề 05.8) | chiếu không làm xa | 3-01 | 4-02 bước 1 |
| 3-03 | §6 (Định nghĩa 05.10, Ví dụ 05.5) | oracle, (G1), (G2) | 1-06, 2-04 | 3-04, 3-06 |
| 3-04 | §6 (Thuật toán 05.9, 05.11) | hai thuật toán, $\bar w_T$ | 3-02, 3-03 | 3-05 |
| 3-05 | §6 (Ví dụ 05.6), Phụ lục D | ba bước, $L_S$ tăng | 1-06, 3-04 | 3-08, 4-02 |
| 3-06 | §6 (Bổ đề 05.12) | trung bình của $g_t$ khi biết lịch sử | 3-04 | 3-07, 4-04 bước 3 |
| 3-07 | chứng minh Bổ đề 05.12, Phụ lục B | kỹ thuật | 3-06, 1-02 | 3-08, 4-04 |
| 3-08 | Bài tập 05.3(b) | bài tập, kiểm (c) bằng số | 3-05, 3-07 | 4-01 (ô $1{,}3289$, ghi chú diễn giả), 5-04 |
| 4-00 | §7 | tiêu đề mạch | (thiếu câu nối trên mặt trang, xem P3) | 4-01 |
| 4-01 | §7 (Mệnh đề 05.13) | bất đẳng thức một bước | 3-02 | 4-02 |
| 4-02 | chứng minh 05.13, Ví dụ 05.7 | ý tưởng chứng minh | 3-02, 3-05 | 4-04 bước 1 |
| 4-03 | §2 (C), §7 (Định lý 05.14) | cận kì vọng | 4-01, 3-03 | 4-04, 4-06 |
| 4-04 | chứng minh 05.14 | ý tưởng chứng minh, chỗ dùng giả thiết | 4-01, 3-06, 2-02 | 4-05, 5-01…5-04 (bước 3, 4) |
| 4-05 | chứng minh 05.14 bước 2, 5 | kỹ thuật | 4-04 | 4-09 |
| 4-06 | Ví dụ 05.8 bước 3 | trực quan độ dài bước, hình | 4-03 | 4-07 |
| 4-07 | §7 (Hệ quả 05.15) | phát biểu | 4-06 | 4-08, 6-03, 7-01 |
| 4-08 | chứng minh 05.15, Ví dụ 05.8 | ý tưởng chứng minh, số vòng lặp | 4-07 | 4-10, 6-03 |
| 4-09 | Hệ quả 05.16, Ví dụ 05.9 | GD; lời đáp câu hỏi 1-06 | 3-04, 4-07, 1-06 | 5-01, 6-04 |
| 4-10 | Bài tập 05.4(c) | bài tập | 4-07, 4-08 | — |
| 5-00 | §8 | tiêu đề mạch | 4-04 | 5-01…5-03 |
| 5-01 | Ví dụ 05.10 | bỏ tính lồi | 4-04 bước 3, 4-09 | 7-02 (ghi chú diễn giả) |
| 5-02 | Ví dụ 05.11 | bỏ (G2) | 4-04 bước 4 | 7-02 (ghi chú diễn giả) |
| 5-03 | Ví dụ 05.12, 05.13 | điểm lặp cuối; oracle chệch | 4-03, 4-07 | 7-03 |
| 5-04 | Bài tập 05.3(c) | bỏ tính độc lập | 3-08, 3-06 | 7-02 |
| 6-00 | §9–§10 | tiêu đề mạch | (câu nối chỉ ở ghi chú diễn giả, xem P4) | 6-01 |
| 6-01 | §9 (Định nghĩa 05.18) | thuật toán có nguồn ngẫu nhiên riêng | 3-04 | không trang nào dùng lại câu "đúng theo cặp $(S,\xi)$" (P4) |
| 6-02 | §9 (Hệ quả 05.19) | $\operatorname{opt}_s$ theo kì vọng, xác suất cao | 4-07, 1-02 | 6-03 |
| 6-03 | chứng minh 05.19, Ví dụ 05.14 | ý tưởng chứng minh, giá $1/\delta'^2$ | 2-04, 4-07, 1-02 | 7-04 |
| 6-04 | §10 (Mệnh đề 05.20) | lô nhỏ | 4-09 | 6-05 |
| 6-05 | Ví dụ 05.15 | bảng $T(b)$ | 6-04 | 6-06 |
| 6-06 | Bài tập 05.5(b) | bài tập | 6-05 | — |
| 7-00 | §11–§14 | tiêu đề mạch | — | 7-01 |
| 7-01 | §13 | ví dụ $\operatorname{opt}_S$ nhỏ, $L_D$ lớn | 4-07, 1-02 | 7-03 dòng cuối |
| 7-02 | §7–§10 | bảng tổng kết | mạch 4–6 | — |
| 7-03 | §11 | trả lời vấn đề trung tâm | 1-05 | — |
| 7-04 | Bài tập 05.5(d) | bài tập tổng hợp, đề | 6-03 | 7-05 |
| 7-05 | lời giải 05.5(d) | lời giải trên mặt trang | 7-04 | — |
| 7-06 | §6, §7 | tự kiểm tra | 3-03, 4-03, 4-04 | — |
| 7-07 | §12, `exercises.md` | bài tập về nhà, liên kết viewer | — | viewer |
| 7-08 | §13, §14 | tài liệu, Bài 06 | — | Bài 06 |

**Thứ tự so với ghi chú.** Bảy mạch ứng với các mục liên tiếp (§1–§4, §5–§6, §7, §8, §9–§10, §11–§14) và đi theo thứ tự mục. Trong một mục có hai chỗ đổi thứ tự khối (P8). Trong mạch 7, trang §13 (7-01) đứng trước các trang §11, §12 theo quyết định T13.

**Đề kiểm theo bản giao việc.**
- Câu hỏi trung tâm của từng mạch có trên mặt trang trước nửa sau của mạch: mạch 2 (2-00, 2-02), mạch 4 (4-00, 4-01), mạch 5 (5-00), mạch 6 (6-00) đạt; mạch 3 chỉ nêu nửa oracle ở dòng dẫn, nửa phép chiếu nêu ở dòng đầu 3-01 (P5).
- "Vấn đề trung tâm" mở đầu một hộp "Câu hỏi:" (1-05); 7-03 trả lời cho cả bài (cận $RG/\sqrt T$, số vòng lặp, xác suất cao, ứng dụng, đại lượng được chặn). Đạt.
- Mạch "Tổng kết" không có khái niệm mới. Phân bố $D$ của 7-01 là dữ liệu mới của câu hỏi cuối buổi §13, dùng khái niệm đã có (đã chốt T13).
- Bảng `Mục | Bài tập` (7-07) khớp `exercises.md`: đủ 05.1–05.12, mỗi bài một lần, mỗi bài ở mạch cung cấp kiến thức cuối cùng (05.3 ở mạch 5 vì phần (c); 05.8 ở mạch 4 vì phần (d) dùng $G$ của Ví dụ 05.9; 05.7 ở mạch 5 theo quyết định). Mạch 3 không có hàng là đúng quy tắc.
- Không xem trước bài sau trên mặt trang: đạt (các câu về Bài 06, bài ổn định, hối tiếc, gradient chính sách chỉ ở ghi chú diễn giả; 7-08 nêu tên Bài 06 theo quy định).
- Không trùng lặp đáng kể; một chỗ lặp nhẹ ở 7-01/7-03 (P10).

**Tính liên tục với deck 01–04.**
- Nhắc lại $\operatorname{opt}_S$ (Định nghĩa 04.2), (O2), Markov (Bổ đề 02.2), sai số ước lượng (Định nghĩa 04.1), (T1): khớp số hiệu và nội dung của ghi chú Bài 01, 02, 04. Cách viết (O2) ngắn hơn deck 04 (P12).
- Kỹ thuật: hai kỹ thuật mới (3-07, 4-05) có trang riêng; tên trùng danh sách storyboard mục 14. Tiêu đề hai trang này theo khuôn "Kỹ thuật: …", khác deck 01–04 (P6). Kỹ thuật "thêm bớt kì vọng rồi bình phương" của Bài 04 và "lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện" của Bài 04 chỉ được nhắc ở ghi chú diễn giả (3-03, 3-07, 6-04), không có dòng "Nhắc lại:" trên mặt trang (P7).
- Bìa: deck 01–04 dùng một câu luận điểm; deck 05 dùng hai câu (P1).
- Mạch 7: deck 01–04 mở bằng "Bảng tổng kết"; deck 05 mở bằng một trang ví dụ (P10).

## Bảng phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | 1-01 (P1) | Luận điểm bìa gồm hai câu, 98 âm tiết; quy định và deck 01–04 dùng một câu. Câu thứ nhất khó theo ("tăng không quá một số hạng tỉ lệ với độ dài bước, có thể âm, cộng một số hạng …"). | `CLAUDE.md` § Slide decks: "cover (title, one-sentence thesis, …)"; bìa 01–04 mỗi bìa một câu (ví dụ L04: "Trên một dãy lớp lồng nhau, rủi ro thực nghiệm luôn chọn lớp lớn nhất, …"). | Một câu giữ nội dung của §7: "Với hàm mục tiêu lồi và độ dài bước chọn theo số vòng lặp, độ chênh tối ưu kì vọng tại trung bình các điểm lặp của hạ gradient ngẫu nhiên tỉ lệ nghịch với căn bậc hai của số vòng lặp." Câu về bất đẳng thức một bước để ở ghi chú diễn giả 1-01 (đã có). |
| trung bình | 3-08, 4-02, 5-04, 6-06, 7-04 (P2) | Mặt trang dẫn số hiệu của ví dụ hoặc bài tập mà không trang nào trước đó mang số đó, nên người nghe không tìm được khối được dẫn trong deck. | 3-08 "thiết lập của Ví dụ 05.6", 4-02 "Bước thứ hai của Ví dụ 05.6": trang 3-05 có tiêu đề "Ví dụ: ba bước hạ gradient ngẫu nhiên có chiếu", không có "Ví dụ 05.6". 7-04 "như Ví dụ 05.14", "640 000 bước của Ví dụ 05.14": 6-03 ghi "**Ví dụ.** $R=1$, $G=4$, …". 6-06 "Thiết lập của Ví dụ 05.15": 6-05 không mang số. 5-04 "thiết lập của Bài tập 05.3(b)": 3-08 không mang số. | Ghi số ở trang nguồn: 3-05 dòng đầu "**Ví dụ 05.6.** Oracle của Ví dụ 05.5 …"; 6-03 "**Ví dụ 05.14.** $R=1$, …"; 6-05 dòng đầu "**Ví dụ 05.15.** $G_F^2=1$, …"; 3-08 "**Câu hỏi:** (Bài tập 05.3(b)) thiết lập …" hoặc ghi số trong tiêu đề theo khuôn deck trước nếu có. Cách khác: thay lời dẫn bằng tên ("thiết lập của ví dụ ba bước"). |
| trung bình | 4-00, 4-01 (P3) | Câu nối giữa mạch 3 và mạch 4 không có trên mặt trang: không câu nào nói mạch 4 kế thừa hai bổ đề nào và còn thiếu gì. Dòng dẫn mạch 4 chỉ nói bước tiếp theo. Hai bổ đề chỉ xuất hiện lại ở bước 1 của 4-02 và bước 3 của 4-04. | 4-00: "Cộng các bất đẳng thức một bước cho cận kì vọng; độ dài bước theo số vòng lặp được chọn từ chính cận đó."; câu nối chỉ ở ghi chú diễn giả 4-00: "Bổ đề phép chiếu và bổ đề lịch sử là hai công cụ; chứng minh chính ghép chúng với tính lồi." `common-brief.md`: "Câu nối giữa hai mạch … phải có trên mặt trang". | Đổi dòng dẫn mạch 4 (≤ 25 âm tiết): "Phép chiếu, kì vọng theo lịch sử và tính lồi ghép lại cho cận kì vọng tại trung bình các điểm lặp." (22 âm tiết); câu về độ dài bước đã có trên 4-06. |
| trung bình | 6-00, 6-01, 6-02 (P4) | Câu nối vào mạch 6 và liên hệ với (O2) chỉ có ở ghi chú diễn giả. (O2) được nhắc lại ở 1-02 nhưng không xuất hiện lại trên mặt trang nào; cụm từ khóa "sai số tối ưu thực nghiệm" của mạch 6 không có trên mặt trang nội dung nào của mạch (chỉ có kí hiệu $\operatorname{opt}_s$). Câu "Bảo đảm theo $\xi$ đúng với mọi $S$ cố định thì đúng theo cặp" của 6-01 không được trang nào dùng lại. | Ghi chú §9, đoạn mở: "Hệ quả 05.15 chặn …; với $F=L_S$, đó là $\operatorname{opt}_S(\bar w_T)$ …, còn Bài 01 đặt hai mức (O1), (O2) tất định cho bộ giải. SGD là một thuật toán ngẫu nhiên …"; đoạn sau Ví dụ 05.14: "Mức (O2) … SGD chỉ đạt mức này với xác suất ít nhất $1-\delta'$ theo $\xi$." Các câu này nằm ở ghi chú diễn giả 6-00, 6-02. Script từ khóa: "sai số tối ưu thực nghiệm" → 0 trang của mạch 6. | Thêm một dòng ở đầu 6-01 (54 âm tiết, có thể rút dòng "Lớp hàm điểm số …" xuống ghi chú diễn giả): "Với $F=L_S$, Hệ quả 05.15 chặn sai số tối ưu thực nghiệm $\operatorname{opt}_S(\bar w_T)$; đầu ra là biến ngẫu nhiên khi $S$ cố định." Thêm vào 6-03 dòng "**Ý nghĩa:**" hoặc một dòng riêng: "(O2) đòi $\operatorname{opt}_s\le\epsilon_{\mathrm{opt}}$ tất định; SGD đạt mức này với xác suất ít nhất $1-\delta'$ theo $\xi$, với mọi $s$, nên cũng theo cặp $(S,\xi)$." |
| trung bình | 3-00 (P5) | Dòng dẫn mạch 3 chỉ nêu kết quả của nửa sau (oracle); phép chiếu, chiếm 3-01, 3-02 và đứng đầu từ khóa, không có trong dòng dẫn. | 3-00: "Khi biết các lần rút trước, gradient trên một quan sát rút đều có trung bình là một dưới gradient của rủi ro thực nghiệm."; từ khóa "phép chiếu · oracle gradient ngẫu nhiên · …". | "Chiếu không làm xa điểm nào của tập tham số; gradient một quan sát rút đều có trung bình là dưới gradient." (22 âm tiết). |
| trung bình | 3-07, 4-05 (P6) | Tiêu đề trang kỹ thuật theo khuôn "Kỹ thuật: …", không có trong danh sách tiền tố của quy định và khác deck 01–04, nơi trang kỹ thuật mang tên kỹ thuật làm tiêu đề. | 3-07 "Kỹ thuật: kì vọng có điều kiện theo lịch sử", 4-05 "Kỹ thuật: tổng triệt tiêu và trung bình các điểm lặp". `CLAUDE.md` § Titles: tiền tố "Ví dụ: …", "Bài tập: …", "Chứng minh: …", "Ý tưởng chứng minh: …". Deck trước: L01-4-04 "Bất đẳng thức hợp", L03-5-06 "Đối xứng hóa và mẫu bóng", L04-4-04 "Chia xác suất thất bại theo trọng số". | "Kì vọng có điều kiện theo lịch sử"; "Tổng triệt tiêu và trung bình các điểm lặp" (nhãn "**Kỹ thuật.**" trên mặt trang giữ nguyên). |
| nhẹ | 3-07, 6-04 (P7) | Liên hệ với kỹ thuật của Bài 04 chỉ ở ghi chú diễn giả. 3-07 giống kỹ thuật "lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện" (L04-6-02); dòng "Kỹ thuật." của 6-04 là kỹ thuật "thêm bớt kì vọng rồi bình phương; mỗi số hạng chéo một lý do" (L04-3-03). | Ghi chú diễn giả 3-07: "Cơ chế giống cách lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện ở Bài 04"; storyboard mục 14: "gần với đẳng thức …, không nhắc tên". `CLAUDE.md` § Techniques: deck sau nhắc lại kỹ thuật bằng tên. | 3-07, thay dòng "Đẳng thức đầu: …" bằng "Đẳng thức đầu: tính chất tháp, như cách lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện (Bài 04)." 6-04: "**Kỹ thuật.** Thêm bớt kì vọng rồi bình phương (Bài 04): $e_j$ không tương quan, số hạng chéo bằng $0$." |
| nhẹ | 2-04/2-05, 3-03/3-04 (P8) | Thứ tự khối trong một mục lệch ghi chú: Ví dụ 05.3 (2-04) đứng trước Ví dụ 05.2 (2-05); Định nghĩa 05.10 (3-03) đứng trước Thuật toán 05.9 (3-04). Người đọc ghi chú song song thấy số hiệu đi lùi. | Ghi chú §4: Ví dụ 05.2 dòng 283, Ví dụ 05.3 dòng 310; §6: Thuật toán 05.9 dòng 518, Định nghĩa 05.10 dòng 539. | Giữ bố cục (có lý do sư phạm) nhưng ghi lý do trong storyboard mục 16; hoặc đưa dòng Ví dụ 05.3 của 2-04 sang sau 2-05. Thứ tự mục vẫn đúng, nên không bắt buộc. |
| nhẹ | 2-06, 5-01…5-03, 6-02 (P9) | Ba từ khóa mạch không có trên mặt trang nội dung của mạch: "hằng số Lipschitz" (mạch 2), "tính lồi" (mạch 5), "xác suất cao" (mạch 6). | Script từ khóa: 0 trang cho mỗi cụm. Tên Mệnh đề 05.5 trong ghi chú: "Hằng số Lipschitz và chuẩn của dưới gradient"; deck 2-06: "Tính Lipschitz và chuẩn của dưới gradient". | 2-06 tiêu đề theo tên khối: "Hằng số Lipschitz và chuẩn của dưới gradient"; 5-01 dòng cuối: "… (G1) hỏng: bỏ tính lồi, bước 3 hỏng."; 6-02 "(b) bảo đảm với xác suất cao: với $\epsilon_{\mathrm{opt}}>0$, …". |
| nhẹ | 7-00, 7-01, 7-03 (P10) | Mạch Tổng kết mở bằng trang ví dụ (quyết định T13), khác deck 01–04 (mở bằng "Bảng tổng kết"); dòng dẫn 7-00 không báo trước ví dụ này. Dòng "Kết luận:" của 7-01 và dòng cuối của 7-03 gần như trùng nhau. | 7-01: "cận chặn $\operatorname{opt}_S$; chặn $L_D$ cần thêm một cận thống kê."; 7-03: "Đại lượng được chặn là $\operatorname{opt}_S$; chặn $L_D$ cần thêm một cận thống kê." L01-7-01…L04-7-01 đều là "Bảng tổng kết". | Giữ vị trí theo T13; đổi dòng cuối 7-03 thành lời đáp có số: "Đại lượng được chặn là $\operatorname{opt}_S$: $\operatorname{opt}_S\approx0{,}0025$ trong khi sai số ước lượng $\approx0{,}9025$." hoặc bỏ dòng "Kết luận:" của 7-01 vì 7-03 đã nói. |
| nhẹ | 1-02, 6-03, 7-01 (P11) | Hai nhắc lại ở 1-02 dùng xa nơi dùng: sai số ước lượng chỉ dùng ở 7-01 (sau 50 trang), Markov ở 6-03 (sau 40 trang). | 7-01: "sai số ước lượng $\approx1{,}9025-1=0{,}9025$"; 6-03 bước 3: "Markov và (a)". Bài học deck 04: "'Nhắc lại:' đứng trước công thức dùng nó". | 7-01 (28 âm tiết) thêm "**Nhắc lại:** sai số ước lượng $L_D(w)-\inf_WL_D$ (Định nghĩa 04.1)."; 6-03 bước 3 viết "bất đẳng thức Markov (Bổ đề 02.2)". 1-02 có thể giữ hoặc rút. |
| nhẹ | 1-02 (P12) | Cách viết (O2) ngắn hơn deck 04 và thiếu đầu ra: "$\operatorname{opt}_S\le\epsilon_{\mathrm{opt}}$" không nói $\operatorname{opt}_S$ của điểm nào. | L04-2-04: "(O2) $L_S(\hat h)\le\inf_{h\in\mathcal H}L_S(h)+\epsilon_{\mathrm{opt}}$, tức $\operatorname{opt}_S(\hat h)\le\epsilon_{\mathrm{opt}}$"; ghi chú Bài 01 dòng 111: "$L_S(A(S))\le\inf L_S+\epsilon_{\mathrm{opt}}$ với mọi $S$". | "(O2): $\operatorname{opt}_S(A(S))\le\epsilon_{\mathrm{opt}}$ với mọi $S$ (Bài 01)." |
| nhẹ | 4-09 (P13) | Lời đáp câu hỏi mở đầu 1-06 ("cần bao nhiêu bước?") ở dòng "Kết luận:" 4-09 không nối lại câu hỏi trên mặt trang; chỉ ghi chú diễn giả nói "Đây là câu trả lời cho câu hỏi thực hành của ví dụ mở đầu". | 1-06 "**Câu hỏi:** SGD bảo đảm gì cho $L_S$ sau $T$ bước, và cần bao nhiêu bước?"; 4-09 "**Kết luận:** SGD tính $10^4$ gradient …". | "**Kết luận:** với $10^6$ hồ sơ của ví dụ mở đầu, SGD tính $10^4$ gradient …" |
| nhẹ | 6-04 (P14) | Dòng nối đầu 6-04 nêu lại Ví dụ 05.9 nhưng không nói lô nhỏ đem gì mới. | 6-04: "Ví dụ 05.9 so một quan sát với cả tập huấn luyện mỗi bước."; ghi chú §10: "Ví dụ 05.9 so hai đầu mút … Lô nhỏ lấy trung bình $b$ gradient ngẫu nhiên ở mỗi bước, và trung bình đó đổi hằng số $G$ trong cận." | "Ví dụ 05.9 so hai đầu mút: một quan sát và cả tập huấn luyện mỗi bước; lô nhỏ nằm giữa và đổi hằng số $G$." |
| nhẹ | 3-04, 4-05 (P15) | Tên tiếng Anh của hai thuật ngữ mà deck sau sẽ nhắc bằng tên không có ở lần dùng đầu: "tổng triệt tiêu (telescoping sum)", "độ dài bước (step size, learning rate)". | Ghi chú, đoạn mở: "tổng triệt tiêu (telescoping sum)"; Câu hỏi mở đầu: "độ dài bước (step size, learning rate; còn gọi là tốc độ học)". Grep deck: 0 lần "telescoping", 0 lần "step size". | 4-04 bước 2 hoặc 4-05: "Tổng triệt tiêu (telescoping sum)"; 3-04: "độ dài bước (step size, learning rate) $\eta>0$ hằng". |

## Kết luận

Số phát hiện: chặn bàn giao 0, nghiêm trọng 0, trung bình 6 (P1–P6), nhẹ 9 (P7–P15).

Thứ tự mạch khớp thứ tự mục của ghi chú. Liên kết `#/N` và liên kết viewer đúng, bảng `Mục | Bài tập` khớp `exercises.md`, và hai trang "Vấn đề trung tâm" đúng vai. Cần sửa: câu nối trên mặt trang vào mạch 4 và mạch 6 (gồm liên hệ với (O2)), số hiệu của các ví dụ và bài tập được dẫn, dòng dẫn mạch 3, tiêu đề hai trang kỹ thuật theo khuôn deck 01–04, bìa một câu.

**đạt khi sửa**

## Đề xuất sửa ghi chú

Không có. Mọi chỗ lệch nêu trên nằm ở deck; ghi chú đã có các câu nối cần thiết (§9 đoạn mở và đoạn sau Ví dụ 05.14, §10 đoạn mở).
