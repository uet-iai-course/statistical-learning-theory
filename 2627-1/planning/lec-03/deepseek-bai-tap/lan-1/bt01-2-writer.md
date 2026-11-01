Đã xác minh trên tệp. Các phát hiện về thuật ngữ là thật.

Vị trí "khả thực": dòng 776, 801, 842, 858 (với 842 và 858 trong lời giải 03.11(b)/(d)). Vị trí "bất khả tri": dòng 781. Mọi chỗ này trích dẫn hoặc gắn với Định nghĩa 01.16 (ghi chú gọi "Khả diễn", lecture-note dòng 97) hoặc Định lý 03.17 (ghi chú dùng "bất khả diễn"). Vi phạm quy tắc `van-phong-tac-gia.md` ("khả thực"→"khả diễn", "bất khả tri"→"bất khả diễn") và không khớp với ghi chú đã sửa. Trong khi đó bản diff writer nộp chỉ có một sửa đổi "kiểm"→"kiểm tra" (dòng 33, hợp lệ và giữ lại). Vì thế bản diff chưa đạt yêu cầu phiên.

VERDICT: yêu cầu sửa

Việc xác minh trên tệp xác nhận phát hiện về thuật ngữ; dưới đây là các sửa cần làm (dùng `replace_text_file` với đoạn khớp chính xác). Thay đổi "kiểm" → "kiểm tra" (dòng 33) là hợp lệ, giữ nguyên, không đụng tới.

1. Dòng 776 (đề 03.11(a), bullet — tên + thuật ngữ, trỏ Định nghĩa 01.16):
   - Hiện có: `- **Khả thực.** $(D,\mathcal H)$ khả thực (Định nghĩa 01.16).`
   - Đích: `- **Khả diễn.** $(D,\mathcal H)$ khả diễn (Định nghĩa 01.16).`

2. Dòng 781 (đề 03.11(c), khớp Định lý 03.17(b)):
   - Hiện có: `...không học được PAC và không học được PAC bất khả tri.`
   - Đích: `...không học được PAC và không học được PAC bất khả diễn.`

3. Dòng 801 (lời giải 03.11(a), Bước 1):
   - Hiện có: `...nên $(D_f,\mathcal H)$ khả thực.`
   - Đích: `...nên $(D_f,\mathcal H)$ khả diễn.`

4. Dòng 842 (lời giải 03.11(b), Bước 2):
   - Hiện có: `...$\ge\tfrac17$ với một phân bố khả thực tập trung trên $C$: đây là Định lý 03.17(a).`
   - Đích: `...$\ge\tfrac17$ với một phân bố khả diễn tập trung trên $C$: đây là Định lý 03.17(a).`

5. Dòng 858 (lời giải 03.11(d), Bước 2):
   - Hiện có: `...với mọi $A$ có $D$ khả thực với $\Pr[L_D(A(S))>\tfrac18]\ge\tfrac17>\delta$.`
   - Đích: `...với mọi $A$ có $D$ khả diễn với $\Pr[L_D(A(S))>\tfrac18]\ge\tfrac17>\delta$.`

Các phát hiện khác đã tự kiểm: mọi trích dẫn khối đánh số trong bài tập (Ví dụ/Mệnh đề/Định lý/Hệ quả/Bổ đề 03.x và kết quả Bài 01–02) đều trỏ tới nội dung còn tồn tại trong ghi chú đã sửa; cấu trúc khối `::: exercise` / `::: hint` / `::: solution`, số lượng khối, mọi con số và kết quả được giữ nguyên; các lời giải đều mang nhãn "Lời giải" và đi từng bước với `aligned` cho tính toán nhiều bước; các nhãn "**Lộ trình.**"/câu lộ trình đầu chứng minh không bị xóa. Sau 5 sửa trên (đúng từ, đúng vị trí), bản sửa mới có thể chấp nhận.