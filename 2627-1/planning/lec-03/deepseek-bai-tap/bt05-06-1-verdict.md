VERDICT: chấp nhận

Tôi đã kiểm tra toàn bộ diff và phần `::: exercise Bài tập 03.5` trong `2627-1/materials/lec-03/exercises.md`. Không phát hiện vấn đề nào cần sửa.

## Kiểm tra chi tiết

**1. Phạm vi diff (chỉ sửa trong exercises.md, đúng quy tắc):**
- Dòng 33: "kiểm rằng" → "kiểm tra rằng" (sửa tiếng Việt chuẩn) ✓
- Dòng 114: "khoảng một điểm" → "các khoảng một điểm" (sửa ngữ pháp số nhiều) ✓
- Dòng 178: "kiểm giả thiết" → "kiểm tra giả thiết" ✓
- Dòng 231: "Trên mẫu $S$" → "Trên tập huấn luyện $S$" (đúng thuật ngữ) ✓
- Dòng 436: bỏ "đoạn sau Định lý 03.15" (cắt navigation pointer, đúng quy tắc) ✓
- Dòng 471-472: bỏ câu dẫn tới Bài tập 03.8 (cắt forward pointer) ✓
- Dòng 516: "véc-tơ chỉ thị" → "véc-tơ chỉ báo" (đúng thuật ngữ) ✓
- Dòng 774-856: "khả thực" → "khả diễn", "bất khả tri" → "bất khả diễn" (đúng thuật ngữ) ✓

**2. Bài tập 03.5 — không có thay đổi nào ngoài dòng 436 (cắt navigation pointer, hợp lệ).**

**3. Con số và kết quả trong Bài tập 03.5 đều đúng:**
- $\theta=5\pi$, $\sin(5\pi/2)=1$, $\sin(5\pi/4)=-\sqrt2/2$, $\sin(5\pi/8)\approx0.924$ ✓
- $\rho_{1000}\approx0.187$, $\ln40/2000\approx0.043$ ✓
- $\Pr(\theta>a)\ge(\mu-a)/(1-a)$ với $k=2m$ ✓
- $\frac{1/4-1/8}{1-1/8}=\frac17$ ✓

**4. Trích dẫn đều trỏ tới nội dung còn tồn tại trong ghi chú đã sửa:**
- Nhận xét 03.10(ii),(iii), Định lý 03.15(a), Mệnh đề 03.9, Ví dụ 03.8 — đều tồn tại ✓
- Định lý 02.7(c) — tồn tại trong lec-02 ✓

**5. Thuật ngữ khớp ghi chú:** "khả diễn", "bất khả diễn", "tập huấn luyện", "trước khi lấy mẫu", "véc-tơ chỉ báo" — tất cả đúng. Cụm "sau khi xem mẫu" (dòng 375) khớp nguyên văn với Ví dụ 03.8 của ghi chú, không phải vi phạm.

**6. Không xóa "Lộ trình."** — không có nhãn nào bị xóa trong diff. ✓

**7. Không thêm khẳng định, số liệu, nguồn mới** — diff chỉ đổi từ ngữ. ✓

**8. Không đổi kí hiệu toán, Markdown chỉ dùng $...$ và $$...$$.** ✓

Không có phát hiện sai nào cần bỏ; không có vấn đề nào cần liệt kê cho writer.