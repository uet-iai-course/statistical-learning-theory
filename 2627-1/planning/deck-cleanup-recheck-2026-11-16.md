# Kiểm lại lượt dọn cuối (deck 01, 02, 06), 2026-11-16

Vai: kiểm lại toán học và mạch truyện, chỉ đọc. Đối chiếu `git diff` so với HEAD của ba deck; ghi chú bài giảng Bài 01, deck 02 (trang ý tưởng chứng minh). Dòng dẫn L01-7-00 kiểm theo câu đính chính của điều phối viên, đã có trong tệp: "Học là chọn hàm có rủi ro gần tốt nhất trong lớp với xác suất cao, từ một cỡ mẫu không phụ thuộc phân bố."

## 1. Câu bị cắt và câu viết lại (deck 01)

| Trang | Thay đổi | Nội dung bị mất? | Chỗ còn giữ / đối chiếu ghi chú |
|---|---|---|---|
| L01-1-02 | bỏ "trong ghi chú" | Không | chỉ là lời dẫn nguồn; nghĩa giữ nguyên (Định nghĩa 01.4) |
| L01-4-06 | bỏ "Thiên kiến quy nạp là một cam kết về dạng của hàm dự đoán." | Không | mặt trang: "Chọn lớp giả thuyết trước khi có tập huấn luyện là một thiên kiến quy nạp" và "Lớp hàm ngưỡng cam kết dự đoán không giảm theo $x$"; ghi chú dòng 697–699 |
| L01-5-12 | bỏ "Ba dòng là ba thay đổi …" | Không | câu điều hướng |
| L01-5-12 | bỏ "khi hàm lỗi bị chặn, mọi phân bố đều thỏa" | Không | mặt trang L01-1-02 (T2): "khi $\ell$ không bị chặn, rủi ro kì vọng phải hữu hạn"; ghi chú dòng 311; thuộc loại "commentary on technicalities" |
| L01-5-12 | bỏ "và hiệu $0{,}04$ không giảm khi $m$ tăng" | Không | mặt trang L01-5-11: "$0{,}04$ do $(D,\mathcal H)$, không do $h$; không giảm khi $m$ tăng"; ghi chú dòng 985 |
| L01-6-02 | bỏ "Theo (a), với mỗi $\delta$, $\beta(m,\delta)$ không tiến về $0$ khi $m\to\infty$." | Không | suy ra ngay từ mặt trang (a) "$\beta(m,\delta)\ge1$, $\forall m,\delta$"; ghi chú dòng 1066 |
| L01-6-02 | "Định lý đó khẳng định với mỗi thuật toán có …" → "Theo định lý đó, mỗi thuật toán có …" | Không | đúng nghĩa Nhận xét 01.30 (ghi chú dòng 1132); "nó" chỉ rõ thuật toán |
| L01-6-02 | "Thiết lập là của" → "Thiết lập của"; "một thuật toán ERM bất kì" → "thuật toán ERM bất kì" | Không | lượng từ "bất kì" giữ |
| L01-7-04 | bỏ "(bảng nguồn ngẫu nhiên, §1)" | Không | trỏ điều hướng; câu trả lời đủ (ghi chú dòng 1233) |
| L01-7-00 | dòng dẫn mới | — | 25 âm tiết (deck_lint, deck_check đếm 25); trần thuật; khớp ghi chú dòng 1026–1031: "$L_D(A(S))\le\inf_{h}L_D(h)+\epsilon$ với xác suất ít nhất $1-\delta$ … khi $m$ vượt một ngưỡng không phụ thuộc phân bố" |

## 2. Deck 02, L02-7-01

- "Chernoff, dây cung, $\min_\tau$": khớp L02-3-05 (bước 1 Chernoff, bước 2 bổ đề Hoeffding với dây cung ở L02-3-03, bước 3 chọn $\tau=4m\epsilon/(b-a)^2$, là điểm nhỏ nhất của số mũ bậc hai theo ghi chú diễn giả).
- "đảo cận Hoeffding": khớp L02-4-03 (bước 3 Định lý 02.7, bước 4 giải $2e^{-2mr^2}=\delta$) và kỹ thuật L02-4-04 "Đảo cận đuôi thành bán kính và cỡ mẫu".

## 3. Deck 06, L06-5-04

Bỏ các thẻ `<span style="white-space:nowrap">…</span>` thì tệp trùng từng byte với HEAD: chữ không đổi. Ảnh chụp: công thức cuối dòng giữ dấu chấm đi kèm ở cả 1600 và 390 px.

## 4. Mạch ±2 trang

L01-4-04…5-00, 5-11…6-03, 6-07…7-02, 7-03…7-05; L02-6-08…7-03; L06-5-02…5-06 (chỉ đổi markup): không đứt mạch. Ghi chú diễn giả L01-4-06 nay mở bằng "Lớp $\mathcal M_{\mathcal X}$ không cam kết gì", đối lại câu mặt trang về lớp hàm ngưỡng. Dòng dẫn L01-7-00 khớp luận điểm bìa và hai dòng đầu L01-7-02.

## 5. Kiểm máy

- `deck_lint.py`: deck 01 chỉ báo `L01-7-03 | SYLL60 | 65 > 60` (đã biết); deck 02, 06: 0.
- `footer_check.py` (http://localhost:8766/2627-1/…): 0 trang chạm chân trang ở cả ba deck.
- `deck_check.py` (L01-6-07, 7-00, 7-01; L02-7-01; L06-5-04): console 0, lỗi trang 0, yêu cầu hỏng 0, `.katex-error` 0, không tràn ngang trang (docScrollW 390).
- Ảnh đã xem: 01:7-00, 02:7-01 (cả `-end`), 06:5-04 (cả `-end`) ở 1600×900 và 390×844, trong thư mục nháp `cleanup-recheck/`.
- `no-ai-slop` Detect trên các câu đã sửa: không mẫu nào.

## 6. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | L01-7-00 | "chọn hàm … từ một cỡ mẫu" có thể đọc nhầm "chọn từ một mẫu" (bìa dùng "chọn từ tập huấn luyện"); dấu phẩy trước "từ" giúp đọc đúng | "Học là chọn hàm có rủi ro gần tốt nhất trong lớp với xác suất cao, từ một cỡ mẫu không phụ thuộc phân bố." | không bắt buộc; giữ nguyên được. Nếu muốn rõ hơn mà vẫn ≤ 25 âm tiết: "…với xác suất cao, khi cỡ mẫu vượt ngưỡng không phụ thuộc phân bố" là 26 âm tiết, nên cần bỏ thêm một âm tiết ở chỗ khác |

Kết luận: **đạt**. Không phát hiện chặn bàn giao, nghiêm trọng hay trung bình.
