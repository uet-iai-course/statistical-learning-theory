# Bài 01: kế hoạch sắp xếp lại thứ tự ghi chú

Yêu cầu của người dùng (2026-10-30), theo thứ tự nhận:

1. "Sắp xếp lại thứ tự, tôi thấy nhiều đoạn hoặc khái niệm được đưa ra trước khi định nghĩa".
2. "Cần làm rõ định nghĩa learning setting: cực tiểu rủi ro kì vọng khi không biết phân bố D nhưng có một tập quan sát lấy mẫu iid từ D (sau khi định nghĩa các khái niệm này)".
3. "Tính ngẫu nhiên của thuật toán không cần đưa ra quá sớm, sẽ làm notation quá phức tạp trong buổi đầu tiên. Có thể viết A(S) thay cho A(S; \xi)". Yêu cầu này thay quyết định 4 của các vòng rà soát trước.

Nguyên tắc: mọi thuật ngữ, kí hiệu và kết quả đánh số được định nghĩa (hoặc giới thiệu kèm nghĩa) trước lần dùng đầu tiên trong thân bài; không đoạn nào dẫn một khối đánh số đứng sau. Ngoại lệ: tiêu đề, danh sách mục tiêu học tập (chỉ bằng lời), và các mục nhìn lại ở cuối ("Câu hỏi cuối buổi và cầu nối", "Tài liệu đọc"). Số trong bài giữ nguyên.

## 1. Kiểm kê trước khi sửa

Số dòng theo bản trước khi sửa (`scratchpad/reorder/lecture-note.md`, 844 dòng). `forward_refs.py` báo 19 lần dẫn tới khối đứng sau; bảng dưới gồm cả các lần dùng thuật ngữ, kí hiệu trước định nghĩa. Tổng: 44 mục.

| Dòng | Thuật ngữ / kí hiệu / khối dùng trước | Định nghĩa ở (dòng) |
|---|---|---|
| 3 | thuật toán học, rủi ro kì vọng $L_D$, rủi ro thực nghiệm $L_S$, ERM, học PAC (có kí hiệu, nghĩa chưa rõ) | 308, 170, 237, 329, 452 |
| 13 | hàm phân lớp ghi nhớ; Mệnh đề 01.15 | 396, 401 |
| 19 | kí hiệu $\mathcal X,\mathcal Y,D,S,\mathcal H,\ell,A$ trong mục tiêu | §1 (52–57) |
| 20, 22 | $\epsilon$, $\delta$ trong mục tiêu | 437, 470 |
| 34 | $\mathcal X$, $\mathcal Y$, thuật toán tất định, điều kiện đo được (ở Kiến thức tiên quyết) | 52, 308 |
| 43 | Mệnh đề 01.15 (lời giải câu hỏi ôn) | 401 |
| 44 | Mệnh đề 01.5 | 257 |
| 45 | Ví dụ 01.8 | 494 |
| 58 | $L_D$ (chỉ có tên) ; rủi ro Bayes (§7) | 170 ; 520 |
| 63 | $\xi$ "được định nghĩa ở §5" | 308 |
| 68–69 | $L_S(h)$, $L_S(A(S;\xi))$ trong bảng đại lượng | 237 |
| 79 | $\ell_{0\text{-}1}$, $\ell_c$, $L_D^c$ (bảng kí hiệu) | 109, 152, 176 |
| 81 | ERM xấp xỉ, $\epsilon_{\mathrm{opt}}$ | 348 |
| 82 | học PAC, $M$, $m_A$, độ phức tạp mẫu | 452, 479 |
| 83 | khả thực, $h^\star$ | 440 |
| 84 | $h_{\mathrm{Bayes}}$, rủi ro Bayes | 530, 520 |
| 85 | thuật toán ghi nhớ $A_{\mathrm{gn}}$ | 396 |
| 86 | cận tổng quát hóa cho mọi thuật toán ERM $\beta$ | 605 |
| 90 | (T1) dẫn Mệnh đề 01.5 | 257 |
| 91 | (T2) dẫn Định nghĩa 01.3 | 227 |
| 92 | (T3) khả thực, Định nghĩa 01.16 | 439 |
| 93 | (T4) học PAC | 452 |
| 95 | (O1)/(O2): nghiệm ERM, ERM xấp xỉ, Định nghĩa 01.12 | 329, 347 |
| 99 | Ví dụ 01.1, Ví dụ 01.2 (câu dẫn trước khối) | 101, 142 |
| 109 | $\ell_c$ "dưới đây" | 152 |
| 119, 127 | "không khả thực", "bản khả thực" | 440 |
| 135 | $A_{\max}$, $A_{\min}$, tập nghiệm ERM, Định nghĩa 01.10 | 329 |
| 137–139 | lập luận ERM trên $D_f$ (dùng ERM) | 329 |
| 145 | rủi ro, nghiệm ERM, Mệnh đề 01.15 | 170, 329, 401 |
| 159 | Ví dụ 01.3; Mệnh đề 01.23(b), ngưỡng tối ưu | 180; 527 |
| 162 | xác suất thất bại (§6), rủi ro kì vọng, "khớp mẫu" (§8) | 437, 170 |
| 231 | học PAC bất khả tri (§7) | 575 |
| 242 | Mệnh đề 01.5 | 257 |
| 296 | $A_{\max}$ trong Nhận xét 01.6 | 135 (chưa có định nghĩa ERM) |
| 311 | $\epsilon$, $\delta$ của §6; $A_{\max}$, $A_{\min}$ | 437; 135 |
| 314 | Ví dụ 01.7 | 361 |
| 342 | Ví dụ 01.6 | 357 |
| 393 | $\mathcal M_{\mathcal X}$ "của Ví dụ 01.2" (dùng được, nhưng ví dụ đặt xa) | 142 |
| 433 | "§7 đo giá này bằng hiệu $0{,}04$" (số chưa tính) | 552 |
| 443 | Nhận xét 01.17 | 445 |
| 470 | Ví dụ 01.8 | 494 |
| 573 | "học được PAC bất khả tri" trước định nghĩa | 575 |
| 598 | "như §8 phát biểu chính thức" (cầu nối trỏ tới khái niệm chưa có) | 604 |
| 619 | (O1), (T3), (T4) trong Hệ quả 01.29 | nhãn của §2 |

Nguyên nhân chính: §2 (bảng kí hiệu, nhãn T1–T4, O1–O2) và §3 (ví dụ xuyên suốt dùng rủi ro, ERM, $A_{\max}/A_{\min}$, ghi nhớ, ngưỡng Bayes) đứng trước các định nghĩa ở §4–§8.

## 2. Thứ tự mới

| Mục | Nội dung | Thay đổi |
|---|---|---|
| Mở đầu | đoạn giới thiệu | các đối tượng nêu bằng lời kèm nghĩa, bỏ kí hiệu $L_D$, $L_S$ |
| Câu hỏi mở đầu | năm mức đo, hai hàm phân lớp | bỏ tên "hàm phân lớp ghi nhớ" và dẫn Mệnh đề 01.15 cũ; mô tả hàm ghi nhớ bằng lời |
| Mục tiêu học tập | năm mục | bỏ kí hiệu $\mathcal X,\ldots,A$, $\epsilon$, $\delta$; thuật ngữ giữ bằng lời |
| Kiến thức tiên quyết | danh sách, hầu chắc chắn, nguyên tử, câu hỏi ôn | đặt tên $U[0,1]$; câu về điều kiện đo được chuyển xuống §2; lời giải câu hỏi ôn bỏ ba lần dẫn tới khối sau |
| §1 Thiết lập bài toán | tám thành phần, bảng cố định/ngẫu nhiên | mục 6: thuật toán tất định, viết $A(S)$; mục 7: giới thiệu $L_D$ kèm nghĩa (kì vọng của $\ell(h,Z)$, $Z\sim D$) và rủi ro Bayes kèm nghĩa; bảng còn hai dòng (cố định; ngẫu nhiên theo $S$), bỏ $\xi$ và $L_S$ |
| §2 Kí hiệu và giả thiết | bảng kí hiệu rút gọn ($D_{\mathcal X}$, $\eta$); đoạn "Đọc lần đầu" (σ-đại số, đo được) đặt trước (T1), (T2) | các kí hiệu khác chuyển về định nghĩa của chúng; bỏ nhãn (T3), (T4), (O1), (O2) khỏi §2: khả thực nêu ở §6, tính đo được nằm trong Định nghĩa 01.4, (O1)/(O2) nêu ở §5 sau ERM xấp xỉ |
| §3 Ví dụ xuyên suốt | Ví dụ 01.1 (thiết lập: $\mathcal X$, $D_{\mathcal X}$, $D_\eta$, $D_f$, lớp hàm ngưỡng, $\ell_{0\text{-}1}$, $S_\eta$, $S_f$); khối ứng dụng ($\ell_c$, $(c_{FP},c_{FN})=(1,4)$, câu hỏi về ngưỡng) | bỏ $A_{\max}/A_{\min}$ và lập luận ERM (về §5); "bản khả thực" thành "bản nhãn tất định"; ví dụ $U[0,1]$ chuyển về §5; bỏ dẫn tới Ví dụ rủi ro và Mệnh đề 01.23(b); bỏ đoạn kết trỏ §6, §8. $\ell_c$ ở lại §3 vì Ví dụ 01.2 (§4) cần nó và nó chỉ dùng đối tượng của §1; ngưỡng Bayes $c_{FP}/(c_{FP}+c_{FN})$ chỉ xuất hiện ở §7 |
| §4 Rủi ro kì vọng và bài toán học thống kê | Định nghĩa 01.1, Ví dụ 01.2–01.3, Nhận xét 01.2, Định nghĩa 01.3, **Định nghĩa 01.4 Thuật toán học** (từ §5, tất định), **Định nghĩa 01.5 Bài toán học thống kê (mới)**, đoạn đọc định nghĩa, **Ví dụ 01.4 (mới, chỉ dùng số đã có: 0,22; 0; 0,2)**, đoạn cầu nối sang rủi ro thực nghiệm | rủi ro thực nghiệm và mệnh đề không chệch chuyển sang §5; Nhận xét "Nguồn ngẫu nhiên nội tại" bị bỏ |
| §5 Rủi ro thực nghiệm và tối thiểu hóa rủi ro thực nghiệm | Định nghĩa 01.6 ($L_S$), Ví dụ 01.5, Mệnh đề 01.7; Định nghĩa 01.8 (ERM, dẫn lại Định nghĩa 01.5) + $A_{\max}/A_{\min}$; Ví dụ 01.6 (+ lập luận $D_f$ từ §3); Nhận xét 01.9 (từ §4); Định nghĩa 01.10; Nhận xét 01.11; Ví dụ 01.7 (phần tập nghiệm rỗng); Định nghĩa 01.12 + phần $\epsilon_{\mathrm{opt}}$ của ví dụ + (O1)/(O2); Thuật toán 01.13; Định nghĩa 01.14; Ví dụ 01.8 (đều trên $[0,1]$); Mệnh đề 01.15; thiên kiến quy nạp | bỏ "§7 đo giá này bằng hiệu $0{,}04$" (số đã có ở §7) |
| §6 Học PAC khả thực | Định nghĩa 01.16 … Ví dụ 01.9 | mở bằng Định nghĩa 01.5; "giả thiết khả thực (realizability assumption)"; câu "thuật toán không nhận $\epsilon,\delta$" chuyển về đây; đoạn mới: Định nghĩa 01.18 làm chính xác Định nghĩa 01.5, và một câu về thuật toán ngẫu nhiên (SGD, Bài 05); bỏ dẫn trước Nhận xét 01.17 và Ví dụ 01.9 |
| §7 Học PAC bất khả tri và quy tắc Bayes | Định nghĩa 01.22 … Nhận xét 01.27 | (iii) viết lại không dùng "học được PAC bất khả tri" trước định nghĩa; nối ngưỡng Bayes với ứng dụng §3; dẫn lại Định nghĩa 01.5 sau Định nghĩa 01.25 và ở đoạn trả lời câu hỏi trung tâm |
| §8 Giới hạn của rủi ro thực nghiệm | Định nghĩa 01.28 … Nhận xét 01.30 | Hệ quả 01.29 giữ (T1) và (O1), mỗi nhãn kèm lời; (T3), (T4) được thay bằng lời (tính khả thực theo Định nghĩa 01.16, điều kiện đo được của Định nghĩa 01.4) |
| §9–§12, Phụ lục | | đánh số lại; bỏ $\xi$ ở §11, §12 và Phụ lục A |

Số mục (§1–§12) giữ nguyên, nên các dẫn "§k" trong `exercises.md` vẫn đúng.

## 3. Bỏ nguồn ngẫu nhiên nội tại $\xi$

Mọi thuật toán học trong Bài 01 là ánh xạ tất định từ mẫu vào giả thuyết, viết $A(S)$; xác suất trong định nghĩa học PAC lấy theo $S\sim D^m$.

| Chỗ | Trước | Sau |
|---|---|---|
| §1 mục 6, đoạn sau danh sách, bảng | "nguồn ngẫu nhiên riêng", dòng "ngẫu nhiên theo $S$ và $\xi$" | thuật toán tất định; bảng hai dòng |
| §2 bảng kí hiệu | $\xi\in\Xi$, $A(S;\xi)$ | bỏ |
| Định nghĩa 01.4 (thuật toán học) | $A_m:\mathcal Z^m\times\Xi\to\mathcal H$, đo được theo $(s,\xi,z)$ | $A_m:\mathcal Z^m\to\mathcal H$, đo được theo $(s,z)$ |
| Nhận xét "Nguồn ngẫu nhiên nội tại" (cũ 01.8) | khối riêng | bỏ; một câu sau Định nghĩa 01.18 về thuật toán ngẫu nhiên (SGD, Bài 05) |
| Ví dụ 01.6 (nghiệm ERM trên mẫu sàng lọc) | dòng "chọn đều ngẫu nhiên" (trung bình $0{,}82/3\approx0{,}273$, xác suất $\tfrac13$) | bỏ dòng và câu đi kèm; thêm một câu: một quy tắc chọn $h_3$ khi bằng nhau đạt $0{,}22$ (giữ khoảng $0{,}22$–$0{,}32$ của §5, §9) |
| Định nghĩa 01.8, 01.10, 01.12 | "mọi $S$ và mọi $\xi$", $(S,\xi)$ | "mọi $S$", $S$ |
| Định nghĩa 01.18, 01.25 và đoạn lượng từ | $\Pr_{S\sim D^m,\ \xi}$, "theo $S$ và $\xi$" | $\Pr_{S\sim D^m}$, "theo $S$" |
| Nhận xét 01.19 | "(và rút $\xi$)" | bỏ |
| §5 đoạn thiên kiến, §7 các đoạn, Nhận xét 01.27 | $A(S;\xi)$ | $A(S)$ |
| §11 lời giải | "(và của $\xi$, nếu có)", "dòng thứ ba" | bỏ; "dòng thứ hai" |
| §12 quan hệ với UML | "xác suất lấy theo cả mẫu và $\xi$" | bỏ |
| Phụ lục A(ii), A(iv) | Tonelli trên $\mathcal Z^m\times\Xi$; điều kiện cho $\{\xi:A_m(s)=h\}$ | trên $\mathcal Z^m$; bỏ vế về $\xi$ |
| `exercises.md` Bài tập 01.1(b) và lời giải | ba loại, "ngẫu nhiên theo $S$ và $\xi$" | hai loại |
| `exercises.md` Bài tập 01.5 (ba dòng lượng từ), 01.7 (gợi ý, lời giải (a)), 01.10 | $\Pr_{S\sim D^m,\ \xi}$, $A(S;\xi)$ | $\Pr_{S\sim D^m}$, $A(S)$ |

Không bài tập nào dựa vào thuật toán ngẫu nhiên. Bài tập 01.11 dùng hàm dự đoán xác suất (đồng xu khi dự đoán), không phải thuật toán ngẫu nhiên; các thuật toán trong bài đó đã là tất định.

## 4. Bảng đánh số cũ → mới

Bộ đếm chung (định nghĩa, kết quả, nhận xét, thuật toán):

| Cũ | Mới | Khối |
|---|---|---|
| 01.1 | 01.1 | Định nghĩa: hàm lỗi và rủi ro kì vọng |
| 01.2 | 01.2 | Nhận xét: tính khả tích |
| 01.3 | 01.3 | Định nghĩa: phân bố có rủi ro hữu hạn |
| 01.7 | 01.4 | Định nghĩa: thuật toán học |
| — | 01.5 | Định nghĩa: bài toán học thống kê (mới) |
| 01.4 | 01.6 | Định nghĩa: rủi ro thực nghiệm |
| 01.5 | 01.7 | Mệnh đề: tính không chệch |
| 01.10 | 01.8 | Định nghĩa: ERM |
| 01.6 | 01.9 | Nhận xét: giả thuyết chọn theo mẫu |
| 01.9 | 01.10 | Định nghĩa: khoảng cách tổng quát hóa |
| 01.8 | — | Nhận xét: nguồn ngẫu nhiên nội tại (bỏ) |
| 01.11 … 01.30 | 01.11 … 01.30 | giữ số |

Bộ đếm ví dụ:

| Cũ | Mới | Ví dụ |
|---|---|---|
| 01.1 | 01.1 | sàng lọc theo ngưỡng (chỉ phần thiết lập) |
| 01.3 | 01.2 | rủi ro kì vọng của các hàm ngưỡng |
| 01.4 | 01.3 | hồi quy tuyến tính |
| — | 01.4 | bài toán học trong ví dụ sàng lọc (mới) |
| 01.5 | 01.5 | rủi ro thực nghiệm trên mẫu cỡ 6 |
| 01.7 | 01.6 | các nghiệm ERM trên mẫu sàng lọc |
| 01.6 | 01.7 | cận dưới đúng không đạt được |
| 01.2 | 01.8 | phân bố đều trên $[0,1]$ với nhãn hằng |
| 01.8 | 01.9 | xác suất thất bại và cỡ mẫu |
| 01.9 | 01.10 | quy tắc Bayes trong ví dụ sàng lọc |
| 01.10 | 01.11 | ghi nhớ khi phân bố có nguyên tử |

Bài tập 01.1–01.11 giữ số và tên. `outline.md` và `review-log.md` còn dùng số cũ; bảng trên là ánh xạ để cập nhật chúng.

## 5. Kiểm kê sau khi sửa

`forward_refs.py`: 0. Đọc lại theo bảng ở mục 1 (và quét lần đầu xuất hiện của 70 thuật ngữ, kí hiệu): không còn thuật ngữ, kí hiệu hay khối nào dùng trước định nghĩa trong thân bài. Còn lại, đều thuộc ngoại lệ hoặc là tên mục: tiêu đề bài; danh sách mục tiêu (thuật ngữ bằng lời); tiêu đề §4, §6, §7 gọi tên khái niệm của chính mục đó; các chỉ dẫn mục kiểu "§6 và §7 trả lời hai câu hỏi này" không kèm thuật ngữ chưa định nghĩa.

## 6. Vòng rà lại 11 và 12 (2026-10-30)

Áp dụng mọi phát hiện của `reviews/11-ra-lai-sap-xep-mach.md` (B1–B13) và `reviews/12-ra-lai-sap-xep-toan.md`; không đổi số hiệu.

- $\mathcal M_{\mathcal X}$ rời bảng §2, được định nghĩa ở câu đầu Ví dụ 01.8 (lần dùng đầu tiên). "Đọc lần đầu" lên trước (T1), (T2) và nêu nghĩa của σ-đại số, đo được.
- Định nghĩa 01.5: một tên tiếng Anh "(statistical learning problem)"; điều kiện rủi ro hữu hạn (Định nghĩa 01.3) nằm trong định nghĩa; công thức chỉ còn hiệu, "không âm vì $A(S)\in\mathcal H$" viết bằng lời; thêm: $A$ chọn trước khi lấy mẫu, không phụ thuộc $D$, nên yêu cầu phải đúng với mọi $D$; câu "tối thiểu hóa rủi ro kì vọng trên $\mathcal H$ khi không tính được $L_D$". Đoạn đọc: thêm "trên họ phân bố $D$ nào" và tên rút gọn "bài toán học".
- §6: $\forall D$ sau $\exists A\,\exists M$ được nối về Định nghĩa 01.5; câu về thuật toán ngẫu nhiên viết lại thành "Khi Bài 05 mở rộng Định nghĩa 01.4 …" và đứng thành đoạn riêng trước Nhận xét 01.19.
- Nối §6 với câu hỏi mở đầu; câu kết văn xuôi sau khối ứng dụng §3; bỏ "tất định" thừa ở Ví dụ 01.9 và chứng minh Hệ quả 01.29; sửa câu "Thiên kiến quy nạp có giá: …"; tách các câu trên 40 tiếng và các đoạn 6 câu được nêu.
- Toán: "(cỡ $m=4$)" ở Ví dụ 01.4; điều kiện đo được của Định nghĩa 01.4 cũng làm $L_S(A(S))$ đo được (ghi ở đoạn sau Định nghĩa 01.6, không dẫn trước); Phụ lục A bỏ "theo thứ tự chúng xuất hiện"; `exercises.md` Bài tập 01.1(a): "ERM dưới $\ell_c$ trên $\mathcal H$, với một quy tắc chọn khi bằng nhau cố định".
