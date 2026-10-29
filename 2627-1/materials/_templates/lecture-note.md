# Bài NN — Tên bài

Một đoạn dẫn ngắn: bài này trả lời câu hỏi trung tâm nào và kế thừa kết quả nào của bài trước.

## Câu hỏi mở đầu

Một hiện tượng cụ thể mà bài sẽ giải thích, kèm một câu trả lời hấp dẫn nhưng sai và lý do nó sai. Không dùng câu hỏi tu từ; câu hỏi được nêu thì phải được trả lời trong bài.

## Mục tiêu học tập

Sau bài này, người học có thể:

- (3–5 năng lực quan sát được: định nghĩa, suy ra, chứng minh, tính, chẩn đoán, so sánh.)

## Kiến thức tiên quyết

- Kết quả cần dùng, dẫn số hiệu bài trước (`Định lý 02.3`) hoặc phát biểu lại ngắn gọn.

**Câu hỏi ôn nhanh.** Hai đến ba câu kiểm tra kiến thức tiên quyết, có đáp số ngắn trong khối gợi ý.

## 1. Thiết lập bài toán

Dữ liệu, cơ chế lấy mẫu, thuật toán học, mục tiêu, đối tượng so sánh, tài nguyên. Nêu rõ đại lượng nào ngẫu nhiên và ngẫu nhiên theo phân bố nào.

## 2. Kí hiệu và giả thiết

| Kí hiệu | Ý nghĩa | Miền hoặc kiểu |
|---|---|---|
| $S=(Z_1,\ldots,Z_m)\sim D^m$ | mẫu huấn luyện độc lập cùng phân bố | $\mathcal Z^m$ |
| $L_D(h)$, $L_S(h)$ | rủi ro kì vọng, rủi ro thực nghiệm | $[0,\infty)$ |

Chỉ thêm kí hiệu riêng của bài; kí hiệu chung theo `planning/ky-hieu.md`. Tách giả thiết thống kê (lấy mẫu, miền giá trị của hàm lỗi) khỏi giả thiết tối ưu (lồi, trơn, Lipschitz).

## 3. Ví dụ xuyên suốt

Một ví dụ nhỏ tính được bằng tay và một ứng dụng thực tế; cả bài quay lại hai ví dụ này.

## 4. Tên mục nội dung

### 4.1 Nhu cầu và trực giác

Bài toán cụ thể chưa giải được bằng công cụ đã có; mô tả bằng lời điều khái niệm sắp định nghĩa nắm bắt.

### 4.2 Định nghĩa

::: definition Định nghĩa NN.1 (Tên khái niệm)
Định nghĩa hình thức: miền, kiểu của mọi đối tượng, giả thiết.
:::

Diễn giải bằng lời, một ví dụ và một phản ví dụ.

### 4.3 Kết quả và chứng minh

Câu dẫn: kết quả cần gì và trả lời câu hỏi nào của mục.

::: theorem Định lý NN.2 (Tên gọi) — chứng minh đầy đủ
**Giả thiết.** Cơ chế lấy mẫu, miền giá trị của hàm lỗi, lớp giả thuyết, đối tượng so sánh.

**Bảo đảm.** Phát biểu; loại bảo đảm (kì vọng hay xác suất ít nhất $1-\delta$; đại lượng thực nghiệm hay tổng thể); phụ thuộc vào $m$, số chiều, số vòng lặp, $\delta$, chuẩn.
:::

::: proof Chứng minh Định lý NN.2
**Lộ trình.** Các bước chính và bất đẳng thức then chốt.

**Bước 1.** … (nêu chỗ dùng giả thiết nào)

**Bước 2.** …

$\square$ Một câu về ý nghĩa của kết quả đối với việc học.
:::

::: example Ví dụ NN.1 (Tính cận bằng số)
Dữ kiện đầy đủ, tính từng bước, kết quả số, một dòng kiểm tra lại.
:::

::: remark Nhận xét NN.3 (Khi bỏ giả thiết)
Phản ví dụ cho thấy kết luận sai khi bỏ một giả thiết.
:::

Kết thúc mục bằng một đoạn văn xuôi, không dùng nhãn: kết quả đã thu được (dẫn số hiệu), điều còn thiếu, và mục sau giải quyết điều đó thế nào.

## 5. Thuật toán

(Khi bài có thuật toán.)

::: algorithm Thuật toán NN.4 (Tên)
**Đầu vào.** … **Khởi tạo.** … **Cập nhật.** … **Đầu ra.** … **Điều kiện dừng.** … **Chi phí.** …
:::

## 6. Ý nghĩa, tác động và giới hạn

Kết quả bảo đảm điều gì, không bảo đảm điều gì, và giúp quyết định thực hành nào.

## 7. Bài tập

Bộ bài tập đầy đủ, có gợi ý và lời giải, nằm trong tệp bài tập của bài. Danh sách ngắn các bài và mục tiêu đo của từng bài.

## 8. Câu hỏi cuối buổi và cầu nối

**Câu hỏi:** một câu chẩn đoán ngắn.

Một đoạn nêu câu hỏi còn mở mà bài sau giải quyết.

## 9. Tài liệu đọc

- **Trước buổi học:** UML §… (mục, không dẫn số trang).
- **Sau buổi học:** …
- **Mở rộng:** …

## Phụ lục

Chứng minh kỹ thuật dài (phác thảo [S] được hoàn thiện tại đây) và các bổ đề phụ.
