I have all the information needed. Let me compile the plan.

# Kế hoạch sửa `2627-1/materials/lec-02/exercises.md` theo văn phong tác giả

Đã đối chiếu mọi trích dẫn trong bài tập với ghi chú Bài 02 đã sửa và ghi chú Bài 01: tất cả các khối được dẫn (Bổ đề 02.2, 02.3, 02.5, 02.6, 02.12; Định lý 02.7, 02.14; Nhận xét 02.8, 02.18; Định nghĩa 02.9, 02.13; Hệ quả 02.10, 02.16; Mệnh đề 02.17; Ví dụ 02.1–02.12; Phụ lục B.1, B.2; câu ôn nhanh 1–3; và các khối Bài 01: Định nghĩa 01.4, 01.16, 01.18, 01.25, 01.28; Nhận xét 01.9, 01.19; Hệ quả 01.29; Mệnh đề 01.7, 01.23; Ví dụ 01.9, 01.10; Bài tập 01.9) đều còn tồn tại trong ghi chú đã sửa. Không có trích dẫn nào trỏ tới nội dung đã bị xóa. Các con số, kết quả và lời giải giữ nguyên.

### bt01 (đầu tệp đến hết Bài tập 02.1)

- **Dòng 3 (đầu tệp):** "Các bài tập dưới đây đi kèm ghi chú Bài 02 và dẫn định nghĩa, kết quả, ví dụ theo số hiệu của ghi chú." — giữ nguyên (đoạn mở đầu tệp, không phải chỉ dẫn điều hướng thừa). Không đổi.
- **Bài tập 02.1 (dòng 7–142):** không có thuật ngữ cũ, không có câu rào đón, không có chỉ dẫn điều hướng thừa. Lời giải đã đi từng bước ("**Bước 1: hiệu hai vế.**", "**Bước 2: khi nào $\mathbb EW=0$.**", …) với `aligned` cho tính toán nhiều bước; các bước tính toán thật sự không bị gộp. Giữ nguyên cấu trúc khối (1 exercise, 3 hint, 1 solution). Không đổi.
- **Dòng 51:** "Vậy khi chỉ biết $\mathbb EV=\mu\le\alpha$, không có cận nào nhỏ hơn $\mu/\alpha$ đúng cho mọi biến không âm có kì vọng $\mu$." — kết luận chặt về tính tối ưu, giữ nguyên.
- **Dòng 82:** "(câu ôn nhanh 1)" — dẫn chiếu hợp lệ để lấy giá trị $\operatorname{Var}V\le\tfrac14$; giữ nguyên.
- **Dòng 141:** "**Kiểm tra lại.**" — bước kiểm số, giữ nguyên.

### bt02-03 (Bài tập 02.2–02.3)

- **Bài tập 02.2 (dòng 144–253):** không có thuật ngữ cũ. Lời giải từng bước với `aligned`; giữ nguyên. Các dòng "Tính độc lập được dùng ở đẳng thức." (193) và "Tính bị chặn được dùng ở đây." (202) là nhận xét sư phạm về bước dùng giả thiết — đúng mục tiêu bài tập, giữ nguyên.
- **Bài tập 02.3 (dòng 255–340):**
  - **Dòng 272 (đề, phần b):** "mọi thuật toán ERM là thuật toán học PAC bất khả tri với $M'(\epsilon,\delta)=…$" → đổi "bất khả tri" thành "bất khả diễn" (quy tắc §5: bất khả tri → bất khả diễn).
  - **Dòng 292 (lời giải):** "Ở Ví dụ 02.7, tỉ lệ lỗi $5\%$ trở xuống có xác suất $0{,}6\%$ cho một ứng viên cố định và $99{,}7\%$ cho ứng viên được chọn." — dẫn Ví dụ 02.7 để lấy con số, hợp lệ; giữ nguyên.
  - **Dòng 298:** "**Đếm biến cố.** Hệ quả 02.16 dùng $2K$ biến cố đuôi. …" — phân tích thực chất, giữ nguyên.

### bt04-05 (Bài tập 02.4–02.5)

- **Bài tập 02.4 (dòng 342–420):** không có thuật ngữ cũ. Giữ nguyên.
- **Bài tập 02.5 (dòng 422–491):**
  - **Dòng 443 (gợi ý 2):** "Các giá trị biên được liệt kê ở Phụ lục B.1." — chỉ dẫn điều hướng; các giá trị biên $k=12,32,24,64$ đã được nêu trong lời giải (dòng 450, 453). Cân nhắc cắt cụm "được liệt kê ở Phụ lục B.1" (quy tắc: bỏ chỉ dẫn điều hướng khi người đọc không cần mở để lấy con số). Đây là thay đổi nhẹ, tùy chọn.
  - **Dòng 453:** "Bốn giá trị biên $k=12$, $32$, $24$, $64$ cho độ lệch đúng bằng $0{,}1$ (Phụ lục B.1)." — con số đã nêu trong câu; cụm "(Phụ lục B.1)" là chỉ dẫn điều hướng, cân nhắc cắt (tùy chọn).
  - **Dòng 488:** "Theo Ví dụ 02.7 và Phụ lục B.2, hai tần suất ước lượng $\approx0{,}0059$ và $\approx0{,}9974$." — con số đã nêu; cụm "và Phụ lục B.2" là chỉ dẫn điều hướng, cân nhắc cắt (tùy chọn).
  - **Dòng 490:** "tần suất sẽ quanh $0{,}0109$ và $4{,}9\cdot10^{-4}$ (Phụ lục B.1)." — con số đã nêu; cụm "(Phụ lục B.1)" là chỉ dẫn điều hướng, cân nhắc cắt (tùy chọn).
  - Các dòng 443, 453, 488, 490: nếu giữ thì vẫn hợp lệ (Phụ lục B.1, B.2 còn tồn tại trong ghi chú); chỉ cắt nếu muốn theo đúng quy tắc "bỏ chỉ dẫn điều hướng". Không bắt buộc.

### bt06 (Bài tập 02.6)

- **Dòng 495 (Mức độ):** "cận đồng thời trên một họ vô hạn đếm được cố định trước mẫu." → đổi "trước mẫu" thành "trước khi lấy mẫu" (quy tắc §5: trước mẫu → trước khi lấy mẫu).
- **Dòng 498 (đề):** "cả họ và trọng số được chọn trước khi lấy mẫu." — đã đúng thuật ngữ; giữ nguyên.
- **Dòng 545 (lời giải):** "Bán kính $r_{m,\hat k}$ ngẫu nhiên qua $\hat k$, nhưng mỗi $r_{m,k}$ cố định trước mẫu." → đổi "trước mẫu" thành "trước khi lấy mẫu".
- **Dòng 577 (lời giải):** "Trọng số phải cố định trước mẫu." → đổi "trước mẫu" thành "trước khi lấy mẫu".
- **Dòng 515 (gợi ý 2):** "Dùng dạng đếm được của bất đẳng thức hợp ở đoạn ngay sau Bổ đề 02.12." — dẫn chiếu hợp lệ (đoạn đếm được tồn tại ở dòng 632 ghi chú); giữ nguyên.

### bt07-08 (Bài tập 02.7–02.8)

- **Bài tập 02.7 (dòng 584–662):**
  - **Dòng 584 (tiêu đề):** "trong trường hợp khả thực" → "trong trường hợp khả diễn".
  - **Dòng 586 (Mức độ):** "cỡ mẫu khả thực cho một lớp vô hạn" → "cỡ mẫu khả diễn".
  - **Dòng 589 (đề):** "Giả sử $(D,\mathcal H_{\mathrm{rec}})$ khả thực (Định nghĩa 01.16)" → "khả diễn".
  - **Dòng 657 (lời giải):** "Tức là $176$ quan sát đủ cho mọi phân bố khả thực." → "khả diễn".
- **Bài tập 02.8 (dòng 664–747):**
  - **Dòng 666 (Mức độ):** "cỡ mẫu khả thực và bất khả tri cho cùng một lớp" → "cỡ mẫu khả diễn và bất khả diễn".
  - **Dòng 669 (đề):** "Giả sử $(D,\mathcal H_{\mathrm{conj}})$ khả thực (Định nghĩa 01.16)" → "khả diễn".
  - **Dòng 675 (đề):** "mọi phân bố khả thực" → "khả diễn".
  - **Dòng 677 (đề):** "dưới một phân bố khả thực" → "khả diễn".
  - **Dòng 689 (gợi ý 3):** "Dưới phân bố khả thực, $\min_hL_D(h)=0$." → "khả diễn".
  - **Dòng 705 (lời giải):** "**Cỡ mẫu khả thực.**" → "**Cỡ mẫu khả diễn.**".
  - **Dòng 707 (lời giải):** "Lớp hữu hạn với $K=3^p+1$, cố định trước mẫu." → "trước khi lấy mẫu".
  - **Dòng 726 (lời giải):** "**So với cỡ mẫu bất khả tri.**" → "**So với cỡ mẫu bất khả diễn.**".
  - **Dòng 730 (lời giải):** "Hệ quả 02.16 đúng cho mọi $D$, kể cả $D$ khả thực." → "khả diễn".
  - **Dòng 740 (lời giải):** "cỡ mẫu khả thực tăng $2$ lần, cỡ mẫu bất khả tri tăng khoảng $4$ lần." → "cỡ mẫu khả diễn tăng $2$ lần, cỡ mẫu bất khả diễn tăng khoảng $4$ lần.".
  - **Dòng 744 (lời giải):** "Nhận xét 02.18 bàn tính cần thiết của tốc độ này." — dẫn chiếu hợp lệ (Nhận xét 02.18 còn tồn tại); giữ nguyên.

### bt09-10 (Bài tập 02.9–02.10)

- **Bài tập 02.9 (dòng 749–826):**
  - **Dòng 784 (lời giải):** "Hàm lỗi 0–1 là hàm chỉ thị của $B_h=\{(x,y):\ h(x)\ne y\}$" → đổi "hàm chỉ thị" thành "hàm chỉ báo" (quy tắc §5: hàm chỉ thị → hàm chỉ báo).
- **Bài tập 02.10 (dòng 828–905):**
  - **Dòng 902 (lời giải):** "Định nghĩa 01.18 cần một hàm $M(\epsilon,\delta)$ dùng chung cho mọi $D$ khả thực." → "khả diễn".
  - **Dòng 902 (lời giải):** "Trong trường hợp bất khả tri (Định nghĩa 01.25)" → "bất khả diễn".

### bt11 (Bài tập 02.11 đến hết tệp)

- **Dòng 909 (Mức độ):** "cỡ mẫu bất khả tri khi hàm lỗi nhận giá trị trong một đoạn $[a,b]$." → "cỡ mẫu bất khả diễn".
- **Dòng 914 (đề):** "mọi thuật toán ERM trên $\mathcal H$ là thuật toán học PAC bất khả tri (Định nghĩa 01.25)" → "bất khả diễn".
- **Dòng 922 (đề, phần b):** "$\ell_c(h,(x,y))$ bằng $1$ khi $h(x)=1$, $y=0$, bằng $4$ khi $h(x)=0$, $y=1$, và bằng $0$ khi $h(x)=y$." — mô tả ba trường hợp bằng lời; theo quy tắc "viết công thức thay mô tả bằng lời" và "các trường hợp của xác suất có điều kiện viết thành công thức", có thể viết lại thành công thức phân trường hợp (ví dụ $\ell_c(h,(x,y))=4\cdot\mathbb 1[h(x)=0,y=1]+\mathbb 1[h(x)=1,y=0]$). Đây là cải thiện văn phong tùy chọn; không bắt buộc, và không được đổi giá trị (1, 4, 0).
- **Dòng 978 (lời giải):** "Trước khi làm tròn, $17\,538{,}04=16\cdot1096{,}13$, đúng $16$ lần giá trị của Ví dụ 02.9." — dẫn Ví dụ 02.9 để lấy con số, hợp lệ; giữ nguyên.

### chung (quy tắc áp dụng cho mọi phần)

1. **Thuật ngữ theo §5 của `van-phong-tac-gia.md`** (đổi toàn bộ trong tệp):
   - "khả thực" → "khả diễn" (13 chỗ: dòng 584, 586, 589, 657, 666, 669, 675, 677, 689, 705, 730, 740, 902).
   - "bất khả tri" → "bất khả diễn" (7 chỗ: dòng 272, 666, 726, 740, 902, 909, 914).
   - "hàm chỉ thị" → "hàm chỉ báo" (1 chỗ: dòng 784).
   - "trước mẫu" → "trước khi lấy mẫu" (4 chỗ: dòng 495, 545, 577, 707).
   - Các thuật ngữ khác đã đúng: "tập huấn luyện" (không có "mẫu huấn luyện"), "phân bố" (không có "phân bố đồng thời"), "dữ liệu có nhiễu" (không có "bản có nhiễu"), "Lời giải" (không có "Đáp án"). Không cần đổi.
2. **Giữ nguyên cấu trúc khối và số khối:** mỗi bài tập giữ đúng 1 `::: exercise`, các `::: hint` và 1 `::: solution`; không thêm/bớt khối. Đã kiểm: 11 bài, mỗi bài đúng số khối như hiện tại.
3. **Lời giải từng bước:** giữ nguyên các bước "**Bước 1/2/3…**" và `aligned` cho tính toán nhiều bước; không gộp bước tính toán thật sự, chỉ gộp bước tầm thường. Không đổi cấu trúc bước hiện có.
4. **Không xóa nhãn "**Lộ trình.**"** — bài tập không có nhãn này (chỉ ghi chú có); không thêm, không xóa.
5. **Giữ mọi con số, kết quả, nhãn và khối đánh số** mà bài tập trích dẫn; chỉ cắt câu, không cắt kết quả. Không thêm khẳng định, số liệu hay nguồn mới.
6. **Markdown chỉ dùng `$...$` và `$$...$$`**; không đổi kí hiệu toán.
7. **Chỉ dẫn điều hướng:** các dẫn chiếu tới khối đánh số (Định nghĩa/Định lý/Ví dụ/Nhận xét/Bổ đề/Hệ quả/Mệnh đề/Phụ lục/câu ôn nhanh) đều trỏ tới nội dung còn tồn tại trong ghi chú đã sửa — giữ nguyên. Riêng các cụm "(Phụ lục B.1)", "(Phụ lục B.2)" ở dòng 443, 453, 488, 490 là chỉ dẫn điều hướng có thể cắt (con số đã nêu trong câu), nhưng không bắt buộc.
8. **Tên tiếng Anh ở lần đầu:** đã có sẵn (ERM, PAC, pairwise uncorrelated, covariance, axis-aligned rectangle, literal, weighted union bound, AM–GM, standard error, random seed, failure frequency, single precision, …); không cần thêm.
9. **Câu rào đón, nhận xét bên lề, câu nhắc lại kết quả:** không phát hiện câu nào cần cắt trong bài tập; các nhận xét "Tính độc lập được dùng ở đây", "Tính bị chặn được dùng ở đây" là nội dung mục tiêu của bài tập, giữ nguyên.
10. **no-ai-slop:** không phát hiện mẫu slop (không có câu mở đầu rào đón, không có kết thúc tổng kết thừa, không có in đậm trang trí thừa); các "**Kiểm tra lại.**" là bước kiểm số thực chất, giữ nguyên.

**Tóm tắt thay đổi bắt buộc:** 25 chỗ đổi thuật ngữ (13 "khả thực"→"khả diễn", 7 "bất khả tri"→"bất khả diễn", 1 "hàm chỉ thị"→"hàm chỉ báo", 4 "trước mẫu"→"trước khi lấy mẫu"). **Thay đổi tùy chọn:** cắt 4 cụm chỉ dẫn Phụ lục B.1/B.2 (dòng 443, 453, 488, 490); viết lại mô tả $\ell_c$ thành công thức (dòng 922). Không đổi con số, kết quả, cấu trúc khối hay kí hiệu toán.