Tôi đã đọc toàn bộ phần Phụ lục (dòng 1066–1141). Giờ tôi kiểm tra từng phát hiện trong báo cáo phản biện.

**Phát hiện 1 (trung bình, dòng 1077): "Lộ trình." còn sót trong chứng minh Phụ lục A.**

Dòng 1077: `**Lộ trình.** Tính $\varphi(0)$, $\varphi'(0)$, chặn $\varphi''$, rồi dùng khai triển Taylor với phần dư Lagrange tại $0$.`

Báo cáo nói tác giả đã bỏ "Lộ trình" ở hai chứng minh trong thân bài (Hệ quả 02.16, Mệnh đề 02.17). Kiểm tra diff: đúng vậy, diff cho thấy `**Lộ trình.** Một bước tất định trên biến cố $r$-đại diện, rồi Định lý 02.14.` đã bị xóa ở chứng minh Hệ quả 02.16, và `**Lộ trình.** Tính xác suất để một giả thuyết xấu khớp mẫu, cộng trên các giả thuyết xấu bằng bất đẳng thức hợp, rồi dùng tính khả thực để nghiệm ERM khớp mẫu.` đã bị xóa ở chứng minh Mệnh đề 02.17.

Tuy nhiên, cần xem xét kỹ. "Lộ trình" là một nhãn bước (step label). Theo quy tắc văn phong §1: "Step labels in examples are used only for distinct computations." Nhưng "Lộ trình" ở đây là một bước mô tả đường đi của chứng minh, không phải một phép tính. Nó là một dạng "navigation/forward pointer" — nó báo trước các bước sẽ làm. Điều này phù hợp với việc tác giả đã bỏ "Lộ trình" ở hai chứng minh khác trong thân bài.

Tuy nhiên, cần lưu ý: đây là một phát hiện hợp lệ về tính nhất quán. Tác giả đã bỏ "Lộ trình" ở hai chứng minh trong thân bài, nên để nhất quán, "Lộ trình" ở Phụ lục A cũng nên bỏ. Đây là một phát hiện hợp lệ.

**Phát hiện 2 (trung bình, dòng 1138): Dẫn chiếu điều hướng sang tài liệu khác còn sót.**

Dòng 1138: `Với lớp hữu hạn, điều kiện đo được nêu ở Phụ lục A(v) của Bài 01 tự thỏa.`

Báo cáo nói tác giả đã bỏ dẫn chiếu tương tự "như ở Phụ lục A(iv) của Bài 01" ở dòng 1141. Kiểm tra diff: đúng vậy, diff cho thấy `như ở Phụ lục A(iv) của Bài 01` đã bị xóa khỏi dòng 1141 (thuật toán ERM).

Tuy nhiên, đây là điểm cần xem xét kỹ theo kế hoạch của điều phối viên. Kế hoạch phu-luc mục 1 nói rõ:

> **Dòng 1148** — "Với lớp hữu hạn, điều kiện đo được nêu ở **Phụ lục A(v) của Bài 01** tự thỏa." → **ứng viên giữ** (dẫn chiếu cần để định danh điều kiện đo được); nếu cắt thì chỉ bỏ "của Bài 01" và giữ "Phụ lục A(v)". *§2.2: giữ dẫn chiếu khi người đọc phải mở để lấy phát biểu.*

Vậy theo kế hoạch của điều phối viên, dòng 1138 (trong diff là dòng 1148) là **ứng viên giữ** — dẫn chiếu cần để định danh điều kiện đo được. Người đọc phải mở Phụ lục A(v) của Bài 01 để lấy phát biểu của điều kiện đo được. Đây là dẫn chiếu hợp lệ theo §2.2.

Báo cáo phản biện đề xuất "Bỏ cụm 'nêu ở Phụ lục A(v) của Bài 01', giữ ý 'tự thỏa'". Điều này **trái với kế hoạch của điều phối viên**, vốn nói rõ đây là ứng viên giữ. Vậy phát hiện này là **sai** — nó mâu thuẫn với kế hoạch đã được duyệt.

Thực ra, cần phân biệt: dòng 1141 bị bỏ "như ở Phụ lục A(iv) của Bài 01" là một dẫn chiếu khác — nó chỉ là "như ở" (so sánh tương tự), không phải dẫn chiếu cần để lấy phát biểu. Còn dòng 1138 "điều kiện đo được nêu ở Phụ lục A(v) của Bài 01" là dẫn chiếu cần để định danh điều kiện đo được — người đọc phải mở để lấy phát biểu. Hai trường hợp khác nhau. Vậy phát hiện 2 là **sai** theo kế hoạch của điều phối viên.

**Phát hiện 3 (nhẹ, dòng 1070): Câu mở đầu là con trỏ điều hướng.**

Dòng 1070: `Bước 4 của chứng minh Bổ đề 02.6 cần bất đẳng thức một biến dưới đây.`

Báo cáo đề xuất "Cân nhắc viết lại không dẫn mục, hoặc giữ nếu cần định hướng người đọc". Đây là một phát hiện nhẹ, mang tính cân nhắc. Câu này giới thiệu mục đích của Phụ lục A — nó giải thích vì sao bất đẳng thức này được trình bày. Đây là một câu giới thiệu ngữ cảnh, không hẳn là con trỏ điều hướng thuần túy. Nó nói "Bước 4 của chứng minh Bổ đề 02.6 cần..." — đây là lời giải thích mục đích, giúp người đọc hiểu vì sao phần này tồn tại. Tôi đánh giá đây là một phát hiện nhẹ, có thể giữ hoặc bỏ. Không phải lỗi nghiêm trọng.

**Phát hiện 4 (nhẹ, dòng 1106): Câu kết là con trỏ điều hướng.**

Dòng 1106: `$\square$ Thay $u=\tau(b-a)$ vào Bước 3 của chứng minh Bổ đề 02.6, ta được $\mathbb Ee^{\tau(V-\mathbb EV)}\le e^{\varphi(u)}\le e^{\tau^2(b-a)^2/8}$.`

Báo cáo đề xuất "Cân nhắc bỏ cụm 'vào Bước 3 của chứng minh Bổ đề 02.6'". Đây là một phát hiện nhẹ. Câu này kết nối kết quả của Phụ lục A với Bước 3 của chứng minh Bổ đề 02.6 — nó cho thấy cách dùng kết quả. Đây là một dẫn chiếu ngược để hoàn tất phép tính. Cụm "vào Bước 3 của chứng minh Bổ đề 02.6" là một con trỏ điều hướng. Tuy nhiên, nó cũng mang ý nghĩa kết nối phép tính. Đây là phát hiện nhẹ, có thể cân nhắc.

Giờ tôi tổng hợp đánh giá:

- **Phát hiện 1 (dòng 1077, "Lộ trình.")**: Hợp lệ. Tác giả đã bỏ "Lộ trình" ở hai chứng minh trong thân bài, nên để nhất quán nên bỏ ở Phụ lục A. Đây là phát hiện đúng.

- **Phát hiện 2 (dòng 1138, dẫn chiếu Phụ lục A(v))**: **Sai**. Trái với kế hoạch của điều phối viên, vốn xác định đây là ứng viên giữ (dẫn chiếu cần để định danh điều kiện đo được). Bỏ phát hiện này.

- **Phát hiện 3 (dòng 1070)**: Nhẹ, mang tính cân nhắc. Câu này giải thích mục đích của Phụ lục A, không phải con trỏ điều hướng thuần túy. Có thể giữ. Không phải lỗi bắt buộc.

- **Phát hiện 4 (dòng 1106)**: Nhẹ, mang tính cân nhắc. Cụm "vào Bước 3 của chứng minh Bổ đề 02.6" là con trỏ điều hướng nhưng cũng kết nối phép tính. Có thể cân nhắc bỏ cụm này.

Vậy trong 4 phát hiện, chỉ có phát hiện 1 là chắc chắn hợp lệ và cần sửa. Phát hiện 2 là sai (trái kế hoạch). Phát hiện 3 và 4 là nhẹ, mang tính cân nhắc.

Vì có ít nhất một phát hiện hợp lệ cần sửa (phát hiện 1), tôi sẽ yêu cầu sửa. Tuy nhiên, cần cân nhắc mức độ. Phát hiện 1 là mức "trung bình" và hợp lệ. Phát hiện 3, 4 là nhẹ.

Tôi sẽ yêu cầu sửa với danh sách cụ thể, bỏ phát hiện 2 (sai).

VERDICT: yêu cầu sửa

Danh sách sửa:
1. **Dòng 1077** — bỏ dòng "**Lộ trình.** Tính $\varphi(0)$, $\varphi'(0)$, chặn $\varphi''$, rồi dùng khai triển Taylor với phần dư Lagrange tại $0$." để nhất quán với việc tác giả đã bỏ "Lộ trình" ở chứng minh Hệ quả 02.16 và Mệnh đề 02.17 trong thân bài.

Các phát hiện khác:
- Phát hiện 2 (dòng 1138) — **bỏ**: trái với kế hoạch của điều phối viên (ứng viên giữ, dẫn chiếu cần để định danh điều kiện đo được).
- Phát hiện 3 (dòng 1070) — nhẹ, không bắt buộc; câu này giải thích mục đích của Phụ lục A, có thể giữ.
- Phát hiện 4 (dòng 1106) — nhẹ, không bắt buộc; có thể cân nhắc bỏ cụm "vào Bước 3 của chứng minh Bổ đề 02.6" nhưng không bắt buộc.

VERDICT: yêu cầu sửa

**Lí do:** Phát hiện 1 (dòng 1077, nhãn "**Lộ trình.**" còn sót trong chứng minh Phụ lục A) là hợp lệ — tác giả đã bỏ nhãn "Lộ trình" ở hai chứng minh trong thân bài (Hệ quả 02.16 và Mệnh đề 02.17, theo diff), nên để nhất quán cần bỏ ở Phụ lục A. Đây là một sửa bắt buộc.

**Danh sách sửa cụ thể cho writer:**

| Vị trí | Văn bản hiện có | Văn bản đích |
|---|---|---|
| dòng 1077 | `**Lộ trình.** Tính $\varphi(0)$, $\varphi'(0)$, chặn $\varphi''$, rồi dùng khai triển Taylor với phần dư Lagrange tại $0$.` | (xóa dòng) |

**Các phát hiện bị bỏ (sai):**

- **Phát hiện 2 (dòng 1138)** — bỏ. Kế hoạch của điều phối viên (mục phu-luc, mục 1) xác định rõ dòng này là **ứng viên giữ**: dẫn chiếu "Phụ lục A(v) của Bài 01" cần để định danh điều kiện đo được, người đọc phải mở để lấy phát biểu (§2.2). Đề xuất "bỏ cụm 'nêu ở Phụ lục A(v) của Bài 01'" trái với kế hoạch đã duyệt. Khác với dòng 1141 (bị bỏ "như ở Phụ lục A(iv) của Bài 01") — đó là dẫn chiếu so sánh tương tự, không phải dẫn chiếu để lấy phát biểu.

**Các phát hiện nhẹ (không bắt buộc, để writer cân nhắc):**

- **Dòng 1070** — "Bước 4 của chứng minh Bổ đề 02.6 cần bất đẳng thức một biến dưới đây." Đây là câu giải thích mục đích của Phụ lục A, không phải con trỏ điều hướng thuần túy; có thể giữ.
- **Dòng 1106** — cụm "vào Bước 3 của chứng minh Bổ đề 02.6" là con trỏ điều hướng nhưng cũng kết nối phép tính; có thể cân nhắc bỏ cụm này, nhưng không bắt buộc.

**Xác nhận các mục đạt của báo cáo phản biện:** đúng — mọi khối đánh số, con số, kết quả, công thức còn nguyên và khớp (B.1/B.2/B.3 đối chiếu với Ví dụ 02.2, 02.3, 02.12); không thêm khẳng định mới; KaTeX hợp lệ; thuật ngữ §5 đã áp dụng đúng ("khả diễn" dòng 1130, "phân bố liên hợp" dòng 1062).