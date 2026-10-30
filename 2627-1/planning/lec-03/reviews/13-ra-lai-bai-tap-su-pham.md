# Rà lại bài tập — sư phạm và `no-ai-slop` Detect (Bài 03, sau vòng sửa)

Người rà độc lập (cùng người rà của `10-bai-tap-su-pham.md`), chỉ đọc, không sửa tệp nào của repo, không commit. Đầu vào: `2627-1/materials/lec-03/exercises.md` hiện tại (đọc toàn bộ 930 dòng), `lec03-ex-round1.diff`, `reviews/11-quyet-dinh-bai-tap.md`, mục 7 "Vòng sửa" của `bai-tap-ghi-chu.md`, `git diff` của ghi chú (hai dòng §10). Dòng dẫn theo tệp hiện tại.

**Phép kiểm đã chạy:** `wc -w` = 9 997; 35 khối `hint`, 12 dòng "Kiểm tra lại."; `grep` "chặt" = 0; "chiều" chỉ còn trong "chiều VC", "số chiều" và "phép nâng chiều" (867, nghĩa số chiều); "Đáp án", "hãy", "!", "rõ ràng", "dễ thấy", "xong" = 0; tên 12 bài so với §10 của ghi chú bằng `diff`: khớp cả 12; câu trên 40 tiếng (công thức tính một từ): còn dòng 213 (41) và 229 (44); nhãn C.1–C.7 mà 03.4(f) dẫn có trong Phụ lục C của ghi chú, và câu cuối Phụ lục C (dòng 1114) khớp lời giải 03.4(f).

## Kết luận

**Giao được.** Mọi phát hiện của báo cáo 10 và mọi mục B1–B2, T1–T7 đã xử lý. Còn 7 điểm nhẹ mới hoặc còn sót, không mục nào chặn bàn giao. Tệp chỉ còn dư 3 tiếng so với trần 10 000, nên người sửa cần giữ mỗi điểm nhẹ trung hòa về độ dài (đề xuất bên dưới có cách bù).

## 1. Trạng thái các mục

### Quyết định 11

| Mục | Trạng thái | Bằng chứng |
|---|---|---|
| B1 "chặt" | ✓ | 589 "… đạt dấu bằng."; 649 "là bất đẳng thức nghiêm ngặt khi $C$ có ít nhất hai điểm không âm … khi $C$ có ít nhất một điểm âm"; `grep chặt` = 0 |
| B2 "theo cả hai chiều" | ✓ | 373 "chứng minh số tham số thực dùng để viết một lớp không là cận trên của chiều VC, và cũng không là cận dưới" |
| T1 Gợi ý 03.9 | ✓ | 675 "Khi $a_l\le0\le b_l$ với mọi $l$, hình chữ nhật chứa $\mathbf e_j$ khi và chỉ khi $b_j\ge1$." |
| T2 §10 ghi chú | ✓ | `git diff`: hai dòng 881–882 đúng văn bản đề xuất; `diff` tên: 12/12 |
| T3 mục tiêu 3 | ✓ | 242 ý (f); lời giải 352–357 dẫn từng giả thiết tới bước và mục C.x |
| T4 vai của $\epsilon$ | ✓ | 216 "Trong (a), (b), (e), $\epsilon$ là cận cho rủi ro vượt mức …; trong (c), $\epsilon$ là độ lệch đều"; 282 "xấp xỉ bằng"; 264 "$0{,}0024999964$" |
| T5 máy tính | ✓ | 218 "dùng máy tính (chia đôi khoảng)" và điều kiện 219–224; 264–265 kiểm $m$, $m-1$ cho cả hai $d$; 267 hai tổng $36{,}9125$, $123{,}6605$ |
| T6 trùng Nhận xét 03.10(iii) | ✓ (cắt) | 373 "(b) Nhận xét 03.10(iii) có một lớp $p$ tham số với chiều VC bằng $1$. Dùng lớp đó và (a) …" |
| T7 §7a | ✓ | 17 vị trí đã tách thành bước có nhãn (ví dụ 03.3(b) 176–198 với `aligned` và đánh số (1)–(3); 03.8(a) Bước 4–7, 626–632; 03.11(c) Bước 1–4, 846–852; 03.11(d) Bước 1–3, 856–860) |

### 22 phát hiện của báo cáo 10

| # | Phát hiện (báo cáo 10) | Trạng thái | Bằng chứng |
|---|---|---|---|
| 1 | nghiêm trọng: "chặt" hai nghĩa ở 03.8 | ✓ | như B1 |
| 2 | nghiêm trọng: "chiều" nghĩa "hướng" ở 03.5(c) | ✓ | như B2; quét toàn tệp sạch |
| 3 | trung bình: tên 03.4, 03.5 lệch §10 | ✓ | như T2 |
| 4 | trung bình: mục tiêu 3 đo một phần | ✓ | như T3 |
| 5 | trung bình: vai của $\epsilon$ ở 03.4 | ✓ | như T4 |
| 6 | trung bình: 03.4(a) cần máy tính, bỏ bước | ✓ | như T5 |
| 7 | trung bình: 03.5(b),(c) trùng Nhận xét 03.10 | ✓ | như T6 |
| 8 | trung bình: §7a, 17 đoạn dồn ý | ✓ | như T7. 03.10(a) còn một câu, xem phát hiện mới N5 |
| 9 | nhẹ: 03.2(a) chép Mệnh đề 03.6 | ✓ | 98 "và chỉ ra chỗ khác với chứng minh Mệnh đề 03.6"; 114 "chỉ các bất đẳng thức đổi thành nghiêm ngặt"; lời giải rút còn hai bước |
| 10 | nhẹ: kí hiệu | ✓ | $\mathcal H^{(6)}_{\mathrm{thr}}$ khai báo ở 16; $\mathcal H'$ ở 610 (gợi ý) và 628 (lời giải, trước khi dùng); $\mathcal H^{0/1}_{\le k}$ ở 542; $h_{\equiv0}$ ở 5, dùng ở 713, 759; $\mathcal H^p_{\mathrm{ball}}$ ở 870. $h_\varnothing$ (03.9, kế thừa Bài tập 02.7) và $g_0$ (tên phần tử của $\mathcal G$, 600) giữ theo đề xuất |
| 11 | nhẹ: thuật ngữ tiếng Anh lần đầu | ✓ | 5 mẫu bóng, rủi ro vượt mức, độc lập afin, đơn hình; 392 nguyên tử (atom); 713 *hội đơn điệu* (monotone conjunction); 775 phân bố biên (marginal distribution) |
| 12 | nhẹ: 03.6(e) lạc chủ đề | ✓ | đã cắt |
| 13 | nhẹ: câu đề 03.6(c), thiếu dẫn chéo 03.8 | ✓ | 470 "Suy ra khi áp dụng lặp lại …"; 474 "Bài tập 03.8(a) chứng minh bất đẳng thức của (d) bằng quy nạp." |
| 14 | nhẹ: "Kiểm tra lại" không kiểm | ✓ | 659 kiểm trên $\mathcal H_{\mathrm{thr}}$, $C=\{1,2,3\}$; 03.5 bỏ Bước 4 cũ, giữ một phép kiểm (456) |
| 15 | nhẹ: 03.1(c) bỏ lỡ liên hệ $\mathcal H^1_{\mathrm{aff}}$ | ✓ | 90 "Thêm hai hàm hằng vào $\mathcal H^{\pm}_{\mathrm{thr}}$ ta được $\mathcal H^1_{\mathrm{aff}}$ …, khớp Bước 4" |
| 16 | nhẹ: 03.4(c) trùng câu cuối chứng minh; trùng nhãn "Bước" | ✓ (còn một chỗ nhỏ) | 229 dẫn "Câu cuối của chứng minh Định lý 03.15"; 291, 293 "Bước 1 của chứng minh (mẫu bóng)", "Bước 4 của chứng minh (Hoeffding)". Nhãn ghép mới "Bước 2: Bước 1 …" còn vụng, xem N2 |
| 17 | nhẹ: 03.4(e) không dẫn Ví dụ 03.10 | ✓ | 240 "Như Ví dụ 03.10 với $q=3$" |
| 18 | nhẹ: vế "phát biểu định lý cơ bản" | ✓ | 781 "Phát biểu sáu khẳng định tương đương của Định lý 03.17(b) …"; lời giải 852 khớp danh sách (1)–(6) của ghi chú |
| 19 | nhẹ: gợi ý theo độ mạnh | ✓ | 671 (03.9 Gợi ý 1 chỉ còn hướng, tập cụ thể sang Gợi ý 2, 675); 717/721 (03.10 "chia cho $8$" sang Gợi ý 2); 787/791 (03.11 ý lấy trung bình sang Gợi ý 2) |
| 20 | nhẹ: câu trên 40 tiếng | phần lớn ✓ | các dòng cũ 206, 318, 602, 655 và đoạn mở đầu đã tách; còn 213 (41 tiếng) và 229 (44 tiếng) mới, xem N6 |
| 21 | nhẹ: §9a, cách diễn đạt | ✓ | 58, 64, 206, 323, 422, 444, 454, 628 ("số hạng này bằng $0$"), 380 ("So sánh với") đều đã viết lại theo đề xuất; câu ở dòng cũ 303 đã bỏ |
| 22 | nhẹ (độ dài) | ✓ | 9 997 tiếng; sáu chỗ cắt đề xuất đều đã làm |

## 2. Phủ mục tiêu sau các chỗ cắt

| Mục tiêu | Bài đo | Nhận xét |
|---|---|---|
| 1 | 03.2, 03.3, 03.7, 03.9, 03.10, 03.12 | Đủ. 03.3 mất trường hợp $p=3$ nhưng (a) vẫn đo cận dưới tổng quát; "nhận ra lập luận chỉ có một phần" vẫn ở 03.2(c) |
| 2 | 03.1, 03.6 (tùy chọn), 03.8 | Đủ. Bỏ 03.6(e) không mất vế nào (dạng đóng khi $m<d$ đã có trong ghi chú) |
| 3 | 03.4(c), (d), (f); thêm 03.5(c) Bước 4 | **Nay đủ.** (f) phủ (T1), tính bị chặn, (T5), (M); (c) phủ nguồn hằng số; (d) phủ lý do không lấy bất đẳng thức hợp trên các cách gán nhãn của mẫu |
| 4 | 03.4(a), (b), (e) | Đủ |
| 5 | 03.5(a), (b), (c); 03.11 | **Nay đủ.** Ba phản ví dụ, cùng vế phát biểu định lý cơ bản (03.11(c), lời giải Bước 4) |

## 3. Kiểm tra các đoạn đã đổi

- **§7a:** các lời giải mới hoặc viết lại đều một bước một ý, có nhãn bước và công thức hiển thị cho phép tính nhiều bước (03.3(b), 03.4(a), 03.4(c) Bước 1–5, 03.8(a), 03.11). Còn hai chỗ nhỏ: 03.10(a) chỉ dẫn bài khác (N5); 03.4(b) Bước 2 không ghi phép tính ra $13{,}881$, $13{,}804$ (bản đóng băng cũng vậy; dòng sau đã cho $m/d$; không ghi thành phát hiện).
- **§9a:** không có lời thuật lại, phủ định kép, câu chẻ hay câu chuyển ý mơ hồ trong các đoạn đã đổi. Các nhãn danh sách mới (03.6(a) 492–494; 03.11(a) 775–777; 03.12(b) 922–924) song song nhau.
- **Thuật ngữ, kí hiệu:** khớp ghi chú; tên lớp mới khai báo trước khi dùng (mục 10 ở trên). Chỉ còn một kí hiệu chưa định nghĩa: $a_i$ ở 355 (N1).
- **Tên bài:** 12/12 khớp §10.
- **Độ dài:** 9 997 ≤ 10 000.

## 4. Phát hiện mới hoặc còn sót

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | 03.4(f), dòng 355 (N1) | Kí hiệu $a_i$ lấy từ Phụ lục C, chưa định nghĩa trong bài tập; ý (c) của chính bài này viết đầy đủ số hạng | 355: "các số hạng $\sigma_ia_i$ nằm trong $[-1,1]$" | "các số hạng $\sigma_i(\ell(h,Z'_i)-\ell(h,Z_i))$ nằm trong $[-1,1]$" (không đổi số tiếng theo `wc -w`) |
| nhẹ | 03.4(c), dòng 291, 293 (N2) | Nhãn ghép hai chữ "Bước" liền nhau, dễ đọc nhầm hai hệ đánh số | 291: "**Bước 2: Bước 1 của chứng minh (mẫu bóng).**"; 293: "**Bước 3: Bước 4 của chứng minh (Hoeffding).**" | "**Bước 2: mẫu bóng (Bước 1 của chứng minh).**", "**Bước 3: Hoeffding (Bước 4 của chứng minh).**" (cùng số tiếng) |
| nhẹ | 03.2(c), dòng 132 (N3) | Sau khi rút gọn, lời dẫn Ví dụ 03.3 chỉ còn "so với", không nói ví dụ đó cho thấy điều gì | 132: "điều đó không cho $d\le4$ (so với Ví dụ 03.3, Bước 2)" | "(Ví dụ 03.3, Bước 2: một tập ba điểm không bị tách trọn dù $d=3$)" (+7 tiếng; bù bằng cách bỏ "Với $d=11$, cận này là $6$." ở 860) |
| nhẹ | 03.9 "Kiểm tra lại", dòng 695 (N4) | Câu bị cắt mất lý do: $\mathcal H^1_{\mathrm{rec}}$ có thêm $h_\varnothing$, nên cần một lý do để nói chiều VC vẫn bằng của $\mathcal H_{\mathrm{int}}$ | 695: "$\mathcal H^1_{\mathrm{rec}}$ là lớp khoảng đóng thêm $h_\varnothing$, và $2p=2$ khớp Mệnh đề 03.6." | "…thêm $h_\varnothing$; trên tập hữu hạn, $h_\varnothing$ trùng một khoảng một điểm nằm ngoài tập, nên $2p=2$ khớp Mệnh đề 03.6." (+12 tiếng; bù bằng cách bỏ câu cuối 928 "Cận trên $p+2=3$ không đạt khi $p=1$.", 8 tiếng, và phần "có độ dài dương," ở 928) |
| nhẹ | 03.10(a), dòng 729 (N5) | Đề yêu cầu "Chứng minh" nhưng lời giải chỉ dẫn Bài tập 02.8(a); phần lập luận một câu của bản đóng băng đã bị cắt để giữ độ dài | 729: "**(a) Số hàm.** Theo Bài tập 02.8(a), $\lvert\mathcal H^p_{\mathrm{conj}}\rvert=3^p+1$." | Cách trung hòa độ dài: đổi đề 705 thành "Nhắc lại từ Bài tập 02.8(a): $\lvert\mathcal H^p_{\mathrm{conj}}\rvert\le3^p+1$." Hoặc khôi phục câu lý do (mỗi biến có ba khả năng, mọi $L$ chứa cặp $x_j,\bar x_j$ cho hàm $0$) và bù độ dài ở chỗ khác |
| nhẹ | dòng 213, 229 (N6) | Hai câu mới dài 41 và 44 tiếng | 229: "Câu cuối của chứng minh Định lý 03.15 nêu hai nguồn của hằng số $8$ trong $\rho_m^2$; tính số mũ ở mỗi bước để kiểm lại tỉ số $16$ …" | 229: thay dấu chấm phẩy bằng dấu chấm ("… trong $\rho_m^2$. Tính số mũ …"). 213 để nguyên được (dòng Mục tiêu, liệt kê) |
| nhẹ | toàn tệp (N7) | Chỉ còn dư 3 tiếng so với trần 10 000; mọi sửa thêm có thể làm vượt | `wc -w` = 9 997 | Áp N1, N2, N6 (không đổi độ dài) trước. Với N3–N5, chỉ áp kèm phần bù đã ghi; chạy lại `wc -w` |

## Đếm theo mức độ (vòng rà lại)

- chặn bàn giao: 0
- nghiêm trọng: 0
- trung bình: 0
- nhẹ: 7
