# Kiểm lại sau biên tập — deck Bài 01, lượt 2 (2026-11-15)

Vai: kiểm lại sau biên tập (chỉ đọc). Đối tượng: `2627-1/lecture-01-mo-hinh-hoc.html` (bản lưu khi kiểm: `recheck2/deck-l2-snapshot.html` trong thư mục nháp của phiên, trùng tệp trong REPO lúc chạy máy) và `img/lec-01/can-co-mau.svg`, `vung-loi.svg`. Căn cứ: `reviews/deck-kiem-lai-1.md` mục 5, `storyboard.md` mục 15 phần "Lượt 2", tin nhắn của điều phối viên, `REPO/CLAUDE.md` § Slide decks, ghi chú bài giảng. `no-ai-slop` chế độ Detect cho câu mới.

Cách làm: đọc lại mặt trang và ghi chú diễn giả của 19 trang có thay đổi (1-02, 1-06, 2-04, 3-00, 3-01, 4-01, 5-00, 5-05, 5-07, 5-12, 6-00, 6-03, 6-05, 6-06, 6-07, 7-00, 7-01, 7-02, 7-04), đối chiếu với nội dung lượt 1 đã trích trong `deck-kiem-lai-1.md`; chạy `footer_check.py` và `deck_check.py --shots`; xem ảnh 1600×900 và 390×844 (kể cả `-end`) của chín trang sát đáy cùng 6-07.

## 1. Mười điểm còn mở của lượt 1

| Điểm (lượt 1) | Trạng thái | Bằng chứng |
|---|---|---|
| Trung bình: nội dung chạm đáy khung (6-03, 2-04, 7-01, 6-05; thêm 1-06, 3-01, 4-01, 5-07, 6-06 theo `footer_check.py`) | đã sửa | `footer_check.py`: "0 slide(s) touching footer/frame bottom". Ảnh 1600×900 của chín trang: dòng cuối cách chân trang rõ, không đè nút điều hướng. Xem phát hiện 1, 2, 3 về chỗ bớt chữ. |
| 2-04: ngoặc chen giữa câu và công thức | đã sửa | "… khi $Y=0$, nên" + công thức; ghi chú vẫn có "$L_{D_\eta}$ là trường hợp $c_{FN}=c_{FP}=1$". |
| 7-01: Hệ quả 01.29 thiếu loại bảo đảm | đã sửa | "Hệ quả 01.29 (tất định): $\beta\ge1$". |
| 7-00: dòng dẫn nói về bài | đã sửa | "Học là chọn hàm có rủi ro gần mức tốt nhất trong lớp với xác suất cao, khi cỡ mẫu vượt ngưỡng chung cho mọi phân bố." Khớp câu cuối §7 của ghi chú. |
| Ghi chú 3-00, 5-00, 6-00: "Phần này" làm chủ ngữ | đã sửa | Chủ ngữ là "Rủi ro thực nghiệm", "Hai định nghĩa học PAC", "Phản ví dụ hàm phân lớp ghi nhớ". |
| Ghi chú 7-04: "khoảng 95 lần" | đã sửa | "có ít nhất khoảng 95 lần", khớp 5-06. |
| 7-02: "không ước lượng không chệch" | đã sửa | "không là ước lượng không chệch của $L_D(h)$". |
| 1-02: (T2) thiếu chủ ngữ; ghi chú chỉ dẫn "định nghĩa ở phần sau" | đã sửa | "khi $\ell$ không bị chặn, rủi ro kì vọng phải hữu hạn"; ghi chú "$L_D(h)=\mathbb E_{Z\sim D}\,\ell(h,Z)<\infty$". |
| Ghi chú 6-07, alt và `<desc>` của `can-co-mau.svg`: trộn hai $\epsilon$ | đã sửa | Ghi chú: "Ở cùng $\epsilon=0{,}1$, … $m=14$, sớm hơn cận … tại $m=30$ …; cận chung ở $\epsilon=0{,}25$ là $\lceil4\ln20\rceil=12$." Alt, `<desc>` và chú giải trong hình ghi "$\epsilon=0{,}1$" cho đường cận. |
| Dấu câu rơi xuống dòng riêng ở 390 px | đã sửa | 6-03 bước 3 và (b), 5-12 hai gạch đầu dòng, 5-05, 7-01: dấu câu nằm trong `$…$`. |

## 2. Toán trên các trang đã đổi

- $4\ln20=11{,}98$, nên $\lceil4\ln20\rceil=12$; kiểm: $e^{-0{,}25\cdot12}=e^{-3}=0{,}0498\le0{,}05$, $e^{-0{,}25\cdot11}=0{,}064>0{,}05$. Đúng.
- 5-07: bỏ phép tính trên mặt trang, giữ "$\ge0{,}05$"; ghi chú: "$0{,}2\cdot\min\{\tfrac14,\tfrac34\}=0{,}05$". Đúng (Nhận xét 01.17). Rủi ro Bayes $0{,}2(\tfrac14+\tfrac14+\tfrac25)=0{,}18$ không đổi.
- 6-03: bước (a) "theo Mệnh đề 01.15, $L_S=0$ và $L_D=1$"; bước (b) "$L_D(A_{\mathrm{gn}}(S))=1>\epsilon$: $m_{A_{\mathrm{gn}}}=\infty$". Đúng; không còn gán giả thiết cho từng phần trên mặt trang, nên không mâu thuẫn Hệ quả 01.29. Ghi chú diễn giả nêu đủ: cả hai phần dùng cả hai giả thiết.
- 6-06 bước 3: "rủi ro $\le\epsilon$ (bước 2)". Đúng: rủi ro bằng $G(\hat t)\le G(k)=D_{\mathcal X}(\{t^\star,\ldots,k-1\})\le\epsilon$ vì $C$ ngắn nhất. Ghi chú diễn giả có chuỗi này. Xem phát hiện 3 về cách dẫn lý do.
- 6-05: "$>\epsilon$" thay "lớn hơn $\epsilon$"; "mọi $\epsilon,\delta\in(0,1)$, $D$ như trên, $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$". Lượng từ "mọi" vẫn bao cả ba biến, khớp Mệnh đề 01.31.
- 7-01: hàng Hệ quả 01.29 bỏ "trên $\mathcal M_{\mathcal X}$"; cột giữa "như Mệnh đề 01.15" gồm $\mathcal H=\mathcal M_{\mathcal X}$. Đủ điều kiện.
- `vung-loi.svg`: chỉ đổi khung (viewBox 640×182); nhãn và vị trí khối $C$, $t^\star$, $k$, $\hat t$ khớp chứng minh phác thảo của Mệnh đề 01.31.

## 3. Mạch truyện (trang đổi ±2)

- **5-07 sau khi bớt chữ:** trang vẫn hiểu được tại chỗ. Mức 2 có khối lượng $0{,}2$ (ví dụ sàng lọc, 2-02), và hình trên cùng trang cho $\eta(2)=\tfrac14$. Câu "$L_D(A(S))\le\epsilon$ không đạt khi $\epsilon<0{,}05$" vẫn nối 5-06 sang định nghĩa rủi ro Bayes. "Chọn như vậy cho $\mathbb 1[x\in\{3,5\}]$" vẫn liền với dòng Trực quan ngay trên.
- **6-03:** hiểu được; lộ trình (a) → biến cố tất định → (b) giữ nguyên. Giả thiết của Mệnh đề 01.15 ở 4-02 và "Giả thiết: như Mệnh đề 01.15" ở 6-02 ngay trước, nên dẫn số hiệu là đủ trên trang ý tưởng chứng minh.
- **6-06:** hiểu được nếu người đọc nối "ngắn nhất" ở bước 2 với chặn $\le\epsilon$ ở bước 3. Đây là bước mà phát hiện HV20 của lượt trước đã yêu cầu viết ra (phát hiện 3).
- **7-00 → 7-01 → 7-02:** dòng dẫn mới và dòng đầu 7-02 cùng diễn đạt câu trả lời (một bằng lời, một bằng công thức), không mâu thuẫn. 1-01 cũng dùng câu luận điểm này, nên bài mở và kết bằng cùng một ý.
- **3-01, 4-01, 1-06:** thứ tự ý không đổi. Xem phát hiện 2 và 4 về kí hiệu mất phần giới thiệu trên mặt trang.
- **7-01, tiêu đề cột "Giả thiết then chốt":** xem phát hiện 1.

## 4. Kiểm tra máy

- `footer_check.py` (1600×900): 0 trang.
- `deck_check.py --shots`: slides=55, console=0, pageerrors=0, failed=0, `.katex-error`=0, overflow=0.
- Mật độ: trên 60 chỉ có 1-03 (80, trần 80), 7-01 (69, trần 80), 7-03 (65, ngoại lệ đã ghi).
- Ảnh 390×844: trang không cuộn ngang; công thức rộng cuộn tại chỗ. Riêng 7-01 xem phát hiện 5.

## 5. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L01-7-01 (và ghi chú 7-00, 7-01) | Tiêu đề cột mới lệch quy định ràng buộc của khóa: `REPO/CLAUDE.md` § Slide decks, mục Conclusion strand, ghi bảng tổng kết là `Kết quả \| Giả thiết không được bỏ \| Ý tưởng chứng minh`. "Giả thiết then chốt" nói ít hơn: tiêu chí "bỏ thì kết luận sai" chỉ còn trong ghi chú diễn giả. Người duyệt không có quyền nới quy định. | `<th>Giả thiết then chốt</th>`; ghi chú 7-01: "Cột giữa ghi giả thiết then chốt, tức giả thiết mà bỏ đi thì kết luận sai"; ghi chú 7-00: "gom lại theo giả thiết then chốt" | Giữ đúng "Giả thiết không được bỏ" (cả ở ghi chú 7-00, 7-01). Bù dòng tiêu đề thêm bằng cách thu một hàng, ví dụ đặt độ rộng cột (`<col>`) để cột giữa đủ chứa tiêu đề trên một dòng, hoặc đưa "(kì vọng)" của hàng 01.7 về cùng dòng với công thức. Đổi tên cột chỉ khi tác giả sửa quy định. |
| nhẹ | L01-1-06 (kéo theo 2-02) | Hàm chỉ báo bị bỏ khỏi mặt trang 1-06 (sửa của HV7 lượt trước bị lùi lại). $\mathbb 1[\cdot]$ được dùng trên mặt 1-06 và 2-02 mà không có giới thiệu, thuật ngữ tiếng Anh "indicator" cũng không lên mặt trang. Quy định: "every symbol … on a slide face is introduced on an earlier slide … or recalled"; "English terms: in parentheses at first use on a content slide". | 1-06: "$h_3(x)=\mathbb 1[x\ge3]$ và $h_4(x)=\mathbb 1[x\ge4]$"; ghi chú 1-06: "Hàm chỉ báo (indicator) $\mathbb 1[p]$ …" | Thêm vào dòng "Kí hiệu:" của 1-02 cụm "hàm chỉ báo (indicator) $\mathbb 1[\cdot]$". 1-02 đang ở 53 âm tiết, thêm khoảng 4 âm tiết. Chạy lại `footer_check.py`. |
| nhẹ | L01-6-06 (bước 3) | Lý do của chặn "$\le\epsilon$" chỉ dẫn "(bước 2)", nên người đọc phải tự suy từ "ngắn nhất". HV20 lượt trước yêu cầu viết bước này ra; chặn trung gian nay chỉ còn trong ghi chú diễn giả. | "Có quan sát trong $C$ thì $\hat t\le k$ và rủi ro $\le\epsilon$ (bước 2)" | Thay "(bước 2)" bằng "($C$ ngắn nhất)", cùng độ dài, nêu thẳng lý do. |
| nhẹ | L01-3-01 | Sau khi bỏ "trên $S=(z_1,\ldots,z_m)$", $z_i$ trong định nghĩa $L_S(h)$ không còn gắn với $S$ trên mặt trang nào. 2-01 chỉ viết "$S\sim D^m$". | "Rủi ro thực nghiệm (empirical risk) $L_S(h)=\frac1m\sum_{i=1}^m\ell(h,z_i)$" | Viết ở 2-01 "Tập huấn luyện $S=(z_1,\ldots,z_m)\sim D^m$". Công thức không tính vào số âm tiết, và 2-01 không sát đáy. |
| nhẹ | L01-7-01 ở 390×844 | Bỏ nhóm ngoặc làm bảng co lọt bề rộng màn hẹp thay vì cuộn ngang tại chỗ. Cột giữa còn khoảng 3–6 kí tự mỗi dòng ("Giả / thiết / then / chốt", "$S;$ / $Z_i\sim$ / $D$"), chữ khó đọc. | `recheck2/check/narrow-*-L01-7-01*.png` | Đặt độ rộng tối thiểu cho bảng này (ví dụ một lớp riêng trong `lecture-course.css` với `min-width` khoảng 640 px) để bảng cuộn ngang tại chỗ như các bảng rộng khác. Nếu không, ghi là giới hạn còn lại. |

`no-ai-slop` Detect trên các câu mới (dòng dẫn 7-00, ghi chú 3-00, 5-00, 6-00, 5-07, 6-07, 7-04): không thấy mẫu cấm, câu rào đón, câu chỉ dẫn hay câu nói về chính văn bản. Một chỗ đọc vấp nhẹ, không mở phát hiện: ghi chú 6-00 "trên lớp hàm ngưỡng, có cấu trúc, $A_{\max}$ có một bảo đảm học" (có thể viết "trên lớp hàm ngưỡng, nhờ cấu trúc thứ tự, …").

## 6. Kết luận

Mười điểm còn mở của lượt 1 đã sửa đúng; `footer_check.py` báo 0 trang, `deck_check.py` sạch; toán trên các trang đổi đúng. Ba ý chuyển sang ghi chú diễn giả không làm 5-07, 6-03 khó hiểu; 6-06 nên ghi thẳng lý do. Còn mở: 0 chặn bàn giao, 0 nghiêm trọng, 1 trung bình (tiêu đề cột 7-01 lệch quy định "Giả thiết không được bỏ"), 4 nhẹ (1-06 hàm chỉ báo, 6-06 lý do, 3-01 $z_i$, 7-01 ở 390 px).

**Kết luận: đạt khi sửa.**
