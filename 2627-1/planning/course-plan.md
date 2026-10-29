# Kế hoạch biên soạn ghi chú bài giảng và bài tập

Lập ngày 2026-10-29 từ `sources/blueprint.md`. Tệp nội bộ, không liên kết từ trang chỉ mục.

## 1. Phạm vi và sản phẩm

Mười bài lý thuyết cho học viên cao học, mỗi bài 150 phút (140 phút giảng và 10 phút nghỉ). Mỗi bài có hai sản phẩm công khai và hai tệp quy trình:

| Tệp | Nội dung |
|---|---|
| `materials/lec-NN/lecture-note.md` | Ghi chú bài giảng: chương giáo trình tự đọc được, theo cấu trúc 15 thành phần ở mục 3 |
| `materials/lec-NN/exercises.md` | Bộ bài tập đầy đủ có gợi ý và lời giải |
| `planning/lec-NN/outline.md` | Dàn ý, chuỗi kết quả, ánh xạ nguồn UML theo mục, bảng thuật ngữ Việt–Anh của bài, phân bổ thời gian 140 phút |
| `planning/lec-NN/review-log.md` | Báo cáo rà soát, quyết định, các mục UML đã tham khảo, sai khác so với blueprint |

Hình vẽ (nếu cần) là SVG trong `img/lec-NN/`. Bộ trang chiếu chỉ làm khi người dùng yêu cầu. Bốn buổi chữa bài tập và bốn bài kiểm tra nằm ngoài phạm vi đợt này.

Tệp dùng chung cho cả học phần: `planning/thuat-ngu.md` (bảng thuật ngữ Việt–Anh thống nhất, mở rộng dần qua từng bài) và `planning/ky-hieu.md` (bảng kí hiệu chung theo blueprint mục A).

## 2. Nguồn

- **UML là nguồn chính** (`sources/uml/`). Số mục trong blueprint đã khớp với mục lục của nhà xuất bản. Khi có PDF, tác tử phân tích nguồn đối chiếu thêm số định lý và số bài tập trước khi dẫn.
- Blueprint quyết định câu hỏi trung tâm, chuỗi kết quả, độ sâu chứng minh và bài tập gốc của từng bài. Kết quả trong ghi chú đánh số cục bộ theo bài (`Định lý 02.3`), không dùng số định lý UML.
- Không dịch hoặc chép đoạn văn UML. Ghi chú trình bày lại bằng lập luận và ví dụ riêng; mỗi mục ghi rõ mục UML tương ứng ở phần "Tài liệu đọc".
- Bài 07–10 cần nguồn bổ sung (xem `sources/README.md`); chỉ tải khi người dùng đồng ý.

| Bài | Câu hỏi trung tâm | UML (đã đối chiếu mục lục) | Nguồn bổ sung |
|---|---|---|---|
| 01 | Học nghĩa là gì? Rủi ro, ERM, PAC | §§2.1–2.3, §§3.1–3.2; đọc thêm §5.1 | — |
| 02 | Cần bao nhiêu dữ liệu cho lớp hữu hạn? | Phụ lục B.1–B.4, §§4.1–4.2; đọc thêm B.5 | — |
| 03 | Lớp vô hạn học được khi nào? Chiều VC | §§6.1–6.5, §9.1; đọc thêm Ch. 28 | Định lý Radon (phụ lục tự soạn) |
| 04 | Chọn độ phức tạp mô hình: phân rã sai số, SRM | §5.2, §§7.1–7.2, §§11.1–11.2; đọc thêm §7.3 | — |
| 05 | Tối ưu ngẫu nhiên: GD, SGD có chiếu | §9.2, §§12.1–12.2, §§14.1–14.3; đọc thêm §§12.3, 14.4 | — |
| 06 | Từ tối ưu đến học: chính quy hóa và ổn định | §14.5, §§13.1–13.3; đọc thêm §13.4 | — |
| 07 | Đo độ phức tạp mạng nơ-ron: Rademacher | §§20.1–20.5, §§26.1–26.2; đọc thêm §26.3 | Bartlett–Foster–Telgarsky (phát biểu) |
| 08 | Ổn định của SGD và khái quát hóa trong học sâu | Ch. 13, §20.6; đọc thêm Ch. 31 | Hardt–Recht–Singer (bắt buộc) |
| 09 | Học phân phối và chuỗi: tự hồi quy, ELBO | §24.1, §24.4 | Kingma–Welling (bắt buộc) |
| 10 | Gradient chính sách và học liên tục | §§21.1–21.3 | Sutton–Barto Ch. 13 (bắt buộc); Kirkpatrick và cộng sự (tùy chọn) |

## 3. Chuẩn trình bày ghi chú

Áp dụng mục A của blueprint, viết bằng tiếng Việt học thuật theo `../CLAUDE.md` và `CLAUDE.md` của học phần. Mười lăm thành phần theo đúng thứ tự, đặt tiêu đề tiếng Việt:

1. Câu hỏi mở đầu và động cơ (kèm một câu trả lời hấp dẫn nhưng sai)
2. Mục tiêu học tập (3–5 năng lực quan sát được)
3. Kiến thức tiên quyết và câu hỏi ôn nhanh
4. Thiết lập bài toán (dữ liệu, cơ chế lấy mẫu, thuật toán học, mục tiêu, đối tượng so sánh, tài nguyên; nêu rõ đại lượng nào ngẫu nhiên)
5. Kí hiệu và giả thiết (tách giả thiết thống kê khỏi giả thiết tối ưu)
6. Ví dụ xuyên suốt (một ví dụ tính tay, một ứng dụng thực tế)
7. Định nghĩa (định nghĩa hình thức, diễn giải, ví dụ, phản ví dụ)
8. Kết quả (bổ đề, mệnh đề, định lý, hệ quả theo đúng vai trò)
9. Chứng minh (lộ trình, bất đẳng thức then chốt, chỗ dùng từng giả thiết, hệ quả cho việc học)
10. Thuật toán (khi có)
11. Ví dụ tính toán và phản ví dụ (ít nhất một cận số và một lần bỏ giả thiết)
12. Ý nghĩa, tác động và giới hạn
13. Bài tập (danh sách ngắn trỏ sang `exercises.md`)
14. Câu hỏi cuối buổi và cầu nối sang bài sau
15. Tài liệu đọc (trước buổi, sau buổi, mở rộng; dẫn theo mục)

Quy ước bổ sung:

- **Độ sâu chứng minh** ghi trong tiêu đề khối: *chứng minh đầy đủ* [F], *phác thảo* [S], *đọc thêm* [O]. Chứng minh kỹ thuật dài đưa vào mục "Phụ lục" cuối ghi chú.
- **Hộp giả thiết và hộp bảo đảm** cho mỗi phát biểu hình thức: hai dòng in đậm "Giả thiết." và "Bảo đảm." trong khối định lý (kỳ vọng hay xác suất cao; đại lượng thực nghiệm hay tổng thể; phụ thuộc vào cỡ mẫu, số chiều, số vòng lặp, độ tin cậy, chuẩn). Không cần sửa trình đọc.
- **Đánh số** một bộ đếm chung tăng theo thứ tự đọc cho định nghĩa, kết quả, nhận xét và thuật toán trong mỗi bài; ví dụ và bài tập có bộ đếm riêng. Số của blueprint được đối chiếu trong `outline.md` (quyết định của điều phối viên, Bài 01).
- **Kí hiệu** theo bảng chung của blueprint: $L_D$, $L_S$, $m$ là cỡ mẫu, $d$ là chiều VC, $p$ là số chiều đặc trưng. Mẫu `_templates/lecture-note.md` và ghi chú giữ chỗ hiện dùng $R$, $\hat R_S$, $n$ sẽ được sửa theo bảng này.
- Thời lượng giảng của blueprint chỉ ghi trong `outline.md`, không đưa vào nội dung sinh viên đọc.
- Danh sách kiểm tra mục E của blueprint là tiêu chí rà soát bắt buộc.

## 4. Chuẩn bài tập

- `exercises.md` gồm các bài gốc trong blueprint (mục x.5 của từng bài) và bài chọn từ phần Exercises của chương UML tương ứng, ghi rõ số bài UML đã kiểm tra trên PDF. Bài gốc và bài trích UML được tách rõ.
- Mỗi bài có mục tiêu đo, mức độ (khái niệm, tính toán, chứng minh, kiểm tra giả thiết, thực nghiệm tùy chọn), gợi ý và lời giải đầy đủ có dòng kiểm tra lại.
- **Công bố (quyết định của người dùng, 2026-10-30):** trang web hiển thị đề bài, các gợi ý giải và lời giải đầy đủ; gợi ý (`::: hint`) và lời giải (`::: solution`) mặc định thu gọn. Một bài có thể có nhiều gợi ý theo mức tăng dần, mỗi gợi ý một khối `hint` riêng. Bài thực nghiệm chỉ mô tả giao thức (tập kiểm tra tách riêng, nhiều lần chạy); không tạo notebook nếu người dùng không yêu cầu.
- Bài tập được soạn sau khi ghi chú của bài đã qua rà soát, để dùng đúng số hiệu và kí hiệu.
- **Bản lời giải UML** (`sources/uml/MLbookSol.pdf`) chỉ dùng để đối chiếu. Tác tử toán tự giải mỗi bài UML được chọn trước, rồi mới so với bản lời giải; chỗ khác nhau được giải quyết bằng lập luận và ghi vào `review-log.md` (bản lời giải cũng có thể sai). Lời giải trong `exercises.md` viết lại bằng lập luận riêng, không dịch hay chép bản lời giải. Không có lời giải sẵn cho Ch. 26 và Ch. 31.

## 5. Quy trình cho mỗi bài

Theo chính sách tác tử trong `../CLAUDE.md`; mọi tác tử Opus 5.5, mức `high`; điều phối viên duyệt sau mỗi bước.

| Bước | Vai trò | Ghi tệp |
|---|---|---|
| 1. Lập kế hoạch | Dàn ý, chuỗi kết quả, ví dụ xuyên suốt, phân bổ thời gian, rủi ro; tạo `outline.md` | Có (chỉ planning) |
| 2. Phân tích nguồn | Đối chiếu blueprint với các mục UML: kết quả, giả thiết, hằng số, cách dẫn dắt, bài tập UML phù hợp; báo cáo chỗ blueprint khác UML | Không |
| 3. Soạn ghi chú | Một người viết, theo từng phần ≤ ~150 dòng, `no-ai-slop` Edit | Có |
| 4. Rà soát độc lập | (a) học viên cao học; (b) chính xác toán học: tự chứng minh lại, tính lại mọi hằng số và cận số; (c) chuyên gia lý thuyết học và trung thành nguồn: lượng từ, giả thiết, không chép UML, không bịa số hiệu; (d) học thuật–sư phạm và `no-ai-slop` Detect; (e) mạch và móc nối | Không |
| 5. Sửa | Một biên tập viên hợp nhất báo cáo, ghi đề xuất không áp dụng | Có |
| 6. Rà lại | Toán trên phần đã sửa; mạch trên phần đã sửa và ranh giới mục | Không |
| 7. Bài tập | Soạn `exercises.md`, rồi rà độc lập: toán (giải lại từng bài) và sư phạm | Có |
| 8. Kiểm định cuối | Trình đọc ở 1600×900, 390×844, bản in, `file://`; không lỗi KaTeX; đồng bộ `material-local-data.js`; cập nhật thẻ trong `index.html` | Có |

## 6. Thứ tự và mốc

1. **Chuẩn bị** (trước khi viết): có PDF UML; cập nhật `CLAUDE.md` của học phần theo mục 3–4; viết lại mẫu ghi chú và mẫu bài tập; tạo `thuat-ngu.md`, `ky-hieu.md`; thay thẻ giữ chỗ bằng 10 thẻ bài (trạng thái `Chưa có` cho đến khi bài qua rà soát).
2. **Bài 01 làm thí điểm**, gồm ghi chú và bài tập. Người dùng duyệt độ dài, giọng văn, mức chi tiết chứng minh và cách trình bày hộp giả thiết/bảo đảm; điều chỉnh chuẩn trước khi làm tiếp.
3. **Bài 02–04** (PAC, tập trung độ đo, VC, SRM), khớp buổi chữa bài 1–2 và hai bài kiểm tra đầu.
4. **Bài 05–06** (SGD, ổn định).
5. **Bài 07–08** (mạng nơ-ron, ổn định của SGD), cần Hardt–Recht–Singer và Bartlett–Foster–Telgarsky.
6. **Bài 09–10** (mô hình sinh, học tăng cường, học liên tục), cần Kingma–Welling, Sutton–Barto và Kirkpatrick và cộng sự.

Mỗi bài viết tuần tự vì bài sau dẫn số hiệu và kí hiệu của bài trước. Commit theo từng bài khi người dùng cho phép.

## 7. Rủi ro

- **PDF UML** đã có (`sources/uml/`), kèm bảng tra trang `sources/uml-sections.md`. Số định lý và số bài tập UML vẫn phải đối chiếu tại bước phân tích nguồn của từng bài.
- **Hằng số trong cận:** blueprint ghi một số cận với hằng số phổ quát $C$ (Định lý 3.5) hoặc hằng số cụ thể (Định lý 7.2). Tác tử toán phải kiểm tra hằng số đúng với chứng minh trình bày, hoặc giữ $C$ và nói rõ.
- **Nội dung ngoài UML** (bài 07–10, phần ổn định đều ở bài 06): ghi nhãn nguồn bổ sung, không gán cho UML.
- **Lời giải công khai:** người dùng đã quyết định công bố gợi ý và lời giải (thu gọn). Vì lời giải bài UML trở thành công khai, chúng phải được viết lại hoàn toàn bằng lập luận riêng, không bám câu chữ của bản lời giải.
