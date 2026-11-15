# Duyệt cổng storyboard — bộ trang chiếu Bài 08

Người duyệt cổng (chỉ đọc), 2026-11-16. Đối tượng: `planning/lec-08/storyboard.md` (toàn bộ, mục 1–15). Đối chiếu:

- nguồn: `materials/lec-08/lecture-note.md` (đọc toàn bộ, kể cả Phụ lục A–F), `materials/lec-08/exercises.md` (Bài tập 08.1, 08.2, 08.3, 08.4, 08.5, 08.6, 08.7, 08.8: đề, gợi ý, lời giải của các phần dùng trên mặt trang);
- quy định: `CLAUDE.md` § Slide decks, `deck-build/common-brief.md` (gồm "Các quy định dễ sót" và các bài học deck 01–06), `deck-build/brief-gate.md`, `deck-build/deck_lint.py` (quy ước đếm: chữ trong ô bảng có tính, số trong bảng và KaTeX không tính; trần 80 chỉ khi tiêu đề chứa "Mục tiêu", "Nội dung" hoặc "tổng kết"), nhật ký yêu cầu 2026-11-13 hàng 1–5;
- khuôn: mục "Bộ trang chiếu" của `lec-05/review-log.md`, `lec-06/review-log.md`, `lec-07/review-log.md`; `lec-07/reviews/deck-storyboard-gate.md`; mục 14 của `lec-06/storyboard.md`; ID trang có thật trong deck đã xuất bản (`L02-5-11`, `L04-6-02`, `L05-3-07`, `L05-4-05`, `L05-4-08`, `L06-4-04`, `L06-4-05`, `L06-5-02`: đã kiểm bằng `grep`); tên Bài 09 ("Học chuỗi và mô hình sinh"); ghi chú Bài 09–10 (chỉ Bài 10 dẫn Mệnh đề 08.12; không ghi chú nào dùng "ghép cặp").

`no-ai-slop` chế độ Detect đã nạp. Script tính lại và đếm âm tiết: thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-08/gate/` (`num.py` phân số chính xác cho ví dụ Huber, `num2.py` số thực, `cnt.py`, `cnt2.py` đếm âm tiết).

## 1. Kết luận

**Đạt khi sửa.** 0 chặn bàn giao, 1 nghiêm trọng, 13 trung bình, 17 nhẹ.

Mọi con số V1–V26 tính lại độc lập khớp storyboard, ghi chú và tệp bài tập (mục 2). Bốn hình có trục chứa hết dữ liệu. Phát biểu của Bổ đề 08.4, Mệnh đề 08.5, Định lý 08.6, Hệ quả 08.7, 08.8, Mệnh đề 08.10, 08.12 trên mặt trang giữ đủ giả thiết, lượng từ, hằng số và loại bảo đảm của ghi chú (mục 3); hai chỗ cần sửa là dòng Nhận xét 08.11 (thiếu $G=1$ và giả thiết, dùng (T3) chưa định nghĩa) và dòng "cận tăng theo hàm mũ" ở 7-02 (mất điều kiện độ dài bước hằng). Không trang nào chuyển kết quả lồi sang mạng ReLU vượt ghi chú.

Phát hiện nghiêm trọng duy nhất (N1): theo quy ước đếm hiện hành, ba trang vượt trần ngay trong storyboard (1-06 $63$, 7-01 $\approx94$–$103$/80, 7-04 $\approx88$), và câu "Bài 07 đã chấp nhận $87$ theo cùng cách tính" ở mục 15 sai: cổng duyệt Bài 07 xếp 7-01 $82$/80 là nghiêm trọng (N1), và điều phối viên yêu cầu cắt về $\approx70$ (`lec-07/review-log.md`, bảng quyết định, dòng N1).

## 2. Tính lại con số

| Mã | Đối tượng | Kết quả tính lại | Khớp |
|---|---|---|---|
| V1 | 1-06, tỉ số cận/khoảng cách | $0{,}5/0{,}045=11{,}11$; $100/0{,}919=108{,}81$ | có |
| V2 | Ví dụ 08.1 | đạo hàm $0;-1;-\tfrac12;-1;-1;1$; $w_2..w_7=0;\tfrac12;\tfrac34;\tfrac54;\tfrac74;\tfrac54$; $5/\sqrt{10\,001}=0{,}0499975$ | có |
| V3 | một bước ghép cặp (2-05) | $w_2=(0,\tfrac12,\tfrac12,\tfrac12)$, $w'_2=(0,\tfrac12,\tfrac12,-\tfrac12)$; $\tfrac38-\tfrac18=\tfrac14$; ghép cặp $\tfrac14$; hai dãy độc lập $\tfrac38$ với $7/6/3$ cặp cho $0/\tfrac12/1$ | có |
| V4 | Ví dụ 08.2 (2-06, F1) | $w'_t=0;0;-\tfrac12;0;\tfrac12;0;0$; $\Delta_t=0;0;1;\tfrac34;\tfrac34;\tfrac74;\tfrac54$; đạo hàm tại $w'_t$: $0;1;-1;-1;1;0$ | có |
| V6 | Ví dụ 08.3 | $(\tfrac12,1,\tfrac32)$, $(1,1,3)$, $(2,2,4)$ | có |
| V7 | Bài tập 08.3(a) | $\lvert\Gamma(0{,}2)-\Gamma(-0{,}2)\rvert=0{,}8$ với $\eta=3$ | có |
| V8 | hằng số $2G$ | $\tfrac32$, $\tfrac12$ | có |
| V9 | Ví dụ 08.4 (liệt kê chính xác) | $\tfrac14$; $\tfrac{29}{64}$ (nhóm $3$ và $\tfrac12+\tfrac34+1+2$); $\tfrac{228\,203}{262\,144}=0{,}870525$; dãy $(2,3,1,4,4,4)$: $w_7=2$, $w'_7=-1$ | có |
| V10 | Bài tập 08.1(c), $\eta=1$ | $\tfrac12$; $\tfrac{13}{16}$; chỉ $(4,1)$ hụt $2$, $(4,2)$ hụt $1$; kiểm $\eta=\tfrac12$ cho $\tfrac{29}{64}$ | có |
| V11 | Ví dụ 08.5 | $0{,}001$; $t/200$ | có |
| V13, V14 | Hệ quả 08.7, Bài tập 08.7(b) | $39{,}975$; $0{,}025(T-1)$: $0{,}25;4;39{,}975$; $\psi=0{,}030107;0{,}284340;0{,}475000$; $q^{11}=0{,}8708$, $q^{161}=0{,}1320$, $q^{1600}=1{,}8\cdot10^{-9}$; $T\le161$, $T\le80$ | có |
| V15 | Ví dụ 08.7 | $\eta^*=0{,}028868$; cận $0{,}086600$; $0{,}079055$; $0{,}072457$; $0{,}070711$ (làm tròn lên $0{,}0708$); $T^*=7071{,}07$; $B(T^*)=0{,}095706$ (làm tròn lên $0{,}0958$); $B(5000)=B(10^4)=0{,}099995$; $B(2\cdot10^4)=0{,}137495$; $B(5\cdot10^4)=0{,}279995$; tỉ số $\sqrt3$: $1{,}73208$ | có |
| V16 | Bài tập 08.8(b) | $3535{,}53$, $0{,}120701$; $17\,677{,}67$, $0{,}080709$ | có |
| V18 | Ví dụ 08.8 (F4) | $\Delta_2=0{,}00099998$; $\Delta_3/\Delta_2=1{,}0999999$; $\Delta_{21}=0{,}006116$, $\Delta_{41}=0{,}041139$, $\Delta_{57}=0{,}1886$, $\Delta_{58}=0{,}207316$ (đầu tiên $>0{,}2$), $\Delta_{61}=0{,}275281$, $\Delta_{81}=1{,}529034$, $\Delta_{101}=2{,}879307$, $\Delta_{200}=3{,}141585$ | có |
| V19 | sau Mệnh đề 08.10; Nhận xét 08.11 | $1{,}1^{100}=13\,780{,}6$; $275{,}59$; $33{,}369$ | có |
| V20 | sau Mệnh đề 08.12 | $0{,}0152726$ | có |
| V21 | Ví dụ 08.9 | $\eta=1$: $0{,}02$ rồi $0$; $\eta=2$: $0{,}04$; $\eta=3$: $0{,}06\ldots3{,}84$ | có |
| V22 | Ví dụ 08.10 | $\pm0{,}49$; bản lề $1{,}49$, $1{,}01$ | có |
| V23 | Bài tập 08.3(d) | $\ln(0{,}5/\Delta_2)=6{,}2146$; $1{,}087758$; $65{,}20$; $1{,}087758^{74}\Delta_2=0{,}5051$; $\tau=68$ ($\Delta_{67}=0{,}482$, $\Delta_{68}=0{,}528$) | có |
| V24 | Bài tập 08.5 | $0{,}4$; $0{,}6931$; $0{,}5032$; $10/(1+e)=2{,}689$; $0{,}4\cdot1{,}5^2=0{,}9$; $10^5\log_{10}1{,}1=4139{,}27$ | có |
| V25, V26 | §12; câu ôn nhanh | $0{,}8$; $28{,}184\le28{,}19$; $0{,}011276$; $3367/4096=0{,}82202$ | có |

**Hình (trục chứa hết dữ liệu).** F1: $w\in[-1;2]$ chứa $-\tfrac12\ldots\tfrac74$; dải bước khác biệt giữa $t=2$–$3$ và $5$–$6$ đúng (bước $t$ đưa $w_t$ tới $w_{t+1}$); mũi tên tại $t=3,6,7$ ứng với $\Delta=1,\tfrac74,\tfrac54$. F2: trục dọc $[0{,}01;200]$ chứa $0{,}045\ldots100$. F3: trục dọc $[0;0{,}30]$ chứa $B(1000)=B(5\cdot10^4)=0{,}279995$; hai số hạng ở đầu mút $0{,}25\to0{,}005$, $0{,}004995\to0{,}249995$. F4: trục dọc lôgarit $[0{,}0005;5]$ chứa $0{,}001\ldots\pi$. Chi tiết nhẹ ở L13.

## 3. Phát biểu so với ghi chú

| Kết quả | Trang | Đối chiếu |
|---|---|---|
| Bổ đề 08.4 | 2-08 | $f$ lồi, $\beta$-trơn trên toàn $\mathbb R^p$; $0\le\eta\le2/\beta$; $W$ khác rỗng, đóng, lồi; (a), (b) hai bất đẳng thức, (c); tất định. Khớp. Dòng "Trực quan." viết $f''$ (L4). |
| Mệnh đề 08.5 | 3-01 | (S), (G); $s,i,z'$ cố định; ghép cặp; $0<\eta_t\le2/\beta$; (I); (a) tất định mọi $\xi$, $t$ và dạng cộng; (b) kì vọng theo $\xi$ với tập huấn luyện cố định. Khớp. |
| Định lý 08.6 | 4-01 | (T1), (T2), (S), (G); $W$ khác rỗng, đóng, lồi; $w_1\in W$ tất định; $0<\eta_t\le2/\beta$ tất định; $\xi$ độc lập với $S$; đầu ra $w_{T+1}$; (a) mọi $s,i,z',z$; (b); (c) trị tuyệt đối, kì vọng theo $(S,\xi)$. Khớp. |
| Hệ quả 08.7 | 4-05 | Khớp (hệ số tổng quát và dạng bước hằng; cùng số chặn khoảng cách tổng quát hóa kì vọng). Không có trang ý tưởng chứng minh (T6). |
| Hệ quả 08.8 | 5-01 | (T1), (T2), (S), (G), $W$, $w_1$, (R), $\eta$ hằng $\le2/\beta$, đầu ra $\bar w_T$; (a); (b) giữ điều kiện $\eta^*\le2/\beta$. Khớp. $\operatorname{opt}_S$ chưa định nghĩa trên mặt trang (T9). |
| Mệnh đề 08.10 | 6-02 | "như Mệnh đề 08.5" với (S′) thay (S), $\eta_t>0$ bất kì tất định; (a), (b), (c), dạng bước hằng. Khớp. |
| Nhận xét 08.11 | 6-03 | Thiếu $G=1$ và ba giả thiết; (T3) chưa định nghĩa trên mặt trang (T8). |
| Mệnh đề 08.12 | 6-04 | Bốn thành phần giả thiết và bảo đảm khớp; $W=\mathbb R^p$ ngầm trong phép cập nhật (chấp nhận). |
| Nhãn (X), (S′), (I), (R) | 2-02 | Đúng nhãn hiện hành của ghi chú §2; (T3) không có trên 2-02 (T8). |

## 4. Ý kiến về các điểm ở mục 11 (điều phối viên quyết định)

1. **Mạch 2 gộp §1–§5.** Đồng ý giữ (khuôn Bài 07). Mục 11.1 ghi "28 phút", bảng mạch và mục 6 cộng ra $30$ phút (L1).
2. **Hệ quả 08.7 không có trang ý tưởng chứng minh.** Không đồng ý giữ như vậy: hệ quả có hàng riêng ở 7-01 và là đầu vào của Hệ quả 08.8, nên theo quy định "mỗi kết quả chính có trang Ý tưởng chứng minh riêng". Đề nghị thêm trang (53 trang, trong trần 55); thời lượng bù như mục 11.2 đề xuất. Trang mới cũng là nơi đặt dòng "đổi thứ tự lấy tổng" (hiện chỉ ở ghi chú diễn giả).
3. **Mệnh đề 08.12, Nhận xét 08.11 không có trang ý tưởng chứng minh.** Đồng ý (đọc thêm). Đề nghị thêm: dòng Nhận xét 08.11 chuyển hẳn sang ghi chú diễn giả 6-03 (T8).
4. **Trang "Kỹ thuật." cho ghép cặp.** Không thêm trang (ghi chú Bài 09–10 không dùng lại; cùng lý do Bài 07 không làm trang McDiarmid). Nhưng dòng Jensen ở 2-05 là một kỹ thuật, không phải trực quan: mục 14 tự ghi nó là kỹ thuật "một dòng ('Trực quan.')". Đề nghị đổi nhãn dòng đó thành "**Kỹ thuật.**", nêu dạng chung và chỗ dùng ("Dùng khi so hai kì vọng của một thuật toán ngẫu nhiên trên hai đầu vào; dùng lại ở Định lý 08.6, Hệ quả 08.7, Mệnh đề 08.10"), giữ dòng "Trực quan." về phân bố từng lần chạy. Kỹ thuật này được dùng bốn lần trong bài và trong Bài tập 08.1(a), (b), 08.6. Đổi tiêu đề thành "Ghép cặp" là tùy chọn; tôi nghiêng về giữ tiêu đề hiện tại vì trang còn chứa ví dụ.
5. **Câu chữ bài tập rút gọn.** Đồng ý, trừ 7-03/7-04: câu hỏi (d)(i) đang nằm trên trang lời giải; chuyển câu hỏi lên 7-03 (L11).
6. **Câu nối vào mạch 4 nằm trong dòng "Trực quan." của 4-01.** Không đồng ý (T5): câu đó là Bước 1 của chứng minh, trái bài học deck 02.
7. **Bài tập tổng hợp 08.5(c), (d)(i).** Đồng ý.
8. **Mục tiêu 2.** Giữ điều kiện chính xác (T10), như quyết định Bài 05 giữ "hàm lồi".
9. **Luận điểm bìa.** Không chọn bản $66$ hay bản $43$ (T11). Bản $43$ thay điều kiện bằng "đủ nhỏ" và mất cơ chế; bản $66$ dài hơn mọi bài trước (Bài 07 đã rút $65\to47$). Đề nghị bản $60$ âm tiết, giữ cả điều kiện và cơ chế:
   "Với hàm lỗi lồi, trơn, có gradient bị chặn và độ dài bước không vượt hai lần nghịch đảo hằng số trơn, hai lần chạy hạ gradient ngẫu nhiên trên hai mẫu lân cận tách nhau chậm, nên khoảng cách tổng quát hóa kì vọng không vượt một hằng số nhân tổng các độ dài bước chia cho cỡ mẫu."
   ("mẫu lân cận" là thuật ngữ Bài 06; trang bìa được miễn quy tắc định nghĩa trước.)
10. **Bảng `Mục | Bài tập` ba hàng.** Đồng ý; đã kiểm: 08.2(c) cần câu sau Hệ quả 08.8 ("hai cận cho hai đầu ra không cộng được"), 08.4 cần Mệnh đề 08.12, 08.6 cần Ví dụ 08.6.
11. **Hàm lỗi bản lề, mạng ReLU chỉ ở ghi chú diễn giả 2-02.** Đồng ý. Thêm (T3) lên 2-02 thay vào (T8).
12. **Công thức cần đo ở 390 px.** Đồng ý.
13. **Trung vị $54$.** Không đạt; cắt cụ thể ở mục 6 (N1).
14. **"SGD" trong tiêu đề.** Chấp nhận theo tên kết quả của ghi chú; xem L15.
15. **F2, F4 và chân trang.** Đồng ý; đề xuất cắt ở mục 6 đã chuyển dòng tỉ lệ đổi nhãn khỏi 4-04.
16. **Thứ tự trong §9.** Đồng ý.
17. **Kí hiệu.** Đồng ý; thêm $g_t$ ba nghĩa (L9).
18. **(a), (b), (c) viết thường.** Đồng ý.

## 5. Bảng phát hiện

`mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa`

| Mã | Mức độ | Trang chiếu | Vấn đề | Bằng chứng | Đề xuất sửa |
|---|---|---|---|---|---|
| N1 | nghiêm trọng | 1-06, 7-01, 7-04; trung vị | Theo quy ước đếm hiện hành, ba trang vượt trần ngay trong storyboard; mục 15 khuyến nghị giữ 7-01 dựa trên một tiền lệ không có; trung vị $54$ không đạt. | `deck_lint.py` dòng 5: "words in tables count"; storyboard mục 15: 1-06 $63$, 7-01 $103$/80, 7-04 $89$ ("Kể cả chữ trong bảng"); đếm độc lập chữ trong bảng: 7-01 $94$, 7-04 $31$ (cộng $57$ ngoài bảng). Mục 15: "Bài 07 đã chấp nhận $87$ theo cùng cách tính"; `lec-07/review-log.md`: "N1 (nghiêm trọng): 1-06 ≈ 82, 2-06 ≈ 68, 7-01 ≈ 82/80 … yêu cầu sửa"; `lec-07/review-log.md`: "cắt về trung vị ≈ 52". | Cắt theo mục 6; người viết deck chạy `deck_lint.py` sau mỗi đợt. Sửa câu sai ở mục 15. |
| T1 | trung bình | 2-04 | Khái niệm ghép cặp mở bằng định nghĩa. | Mặt trang dòng 1: "**Định nghĩa 08.2.** Hai lần chạy ghép cặp (coupled runs): …"; ghi chú §4 mở bằng "Để so hai lần chạy bước theo bước, ta cho chúng dùng chung mọi lựa chọn ngẫu nhiên."; `lec-07/review-log.md`: "2-09 không mở bằng định nghĩa". | Thêm dòng mở: "Định nghĩa 06.9 so hai kì vọng theo $\xi$; để so bước theo bước, hai lần chạy dùng chung mọi lựa chọn ngẫu nhiên." Bù: gộp hai dòng bước chung/khác biệt (mục 6). |
| T2 | trung bình | 2-03 | Cận một vòng không nêu đại lượng được chặn. | "Một vòng, mỗi hồ sơ một lần: cận $5/\sqrt{10^4+1}\approx0{,}05$ (Nhận xét 06.3)."; ghi chú §3: "cho cận … cho rủi ro vượt mức kì vọng (Nhận xét 06.3)"; bài học deck 02: giữ đại lượng được chặn. | "… cận rủi ro vượt mức kì vọng $5/\sqrt{10^4+1}\le0{,}0500$ (Nhận xét 06.3)." Bù: bỏ tiêu đề thẻ h3 ($5$ âm tiết), dùng nhãn in đậm trong thẻ. |
| T3 | trung bình | 2-05 | Kỹ thuật ghép cặp và Jensen mang nhãn "Trực quan." (xem mục 4, điểm 4). | Mặt trang dòng 2: "Hai lần chạy trên cùng không gian của $\xi$; theo bất đẳng thức Jensen: …"; mục 14: "một dòng ('Trực quan.')". $a$, $b$ chưa được gọi tên. | Dòng 2 thành "**Kỹ thuật.** Ghép cặp: hai biến $a$, $b$ trên cùng không gian của $\xi$, $\lvert\mathbb E_\xi a-\mathbb E_\xi b\rvert\le\mathbb E_\xi\lvert a-b\rvert$; dùng khi so hai kì vọng của một thuật toán ngẫu nhiên trên hai đầu vào." |
| T4 | trung bình | 2-08, 2-10, 2-11 | Ba trang liên tiếp trình bày cùng một lập luận hệ số góc một chiều; 2-08 "Trực quan." trùng lời giải 2-11. | 2-08: "hệ số góc … là $1-\eta f''\in[1-\eta\beta,1]$; tính lồi cho cận trên $1$, $\eta\le2/\beta$ cho cận dưới $-1$"; 2-11 Lời giải: "$(1-\eta)(u-v)\le\Gamma(u)-\Gamma(v)\le u-v$ … Tính không giảm (từ tính lồi) cho cận trên; $\eta\le2$ cho cận dưới". | Giữ 2-08 một dòng ngắn "Một chiều, khi $f$ khả vi hai lần: hệ số góc của $\Gamma$ nằm trong $[1-\eta\beta,1]\subset[-1,1]$." và chuyển phần "tính lồi cho … cận dưới" sang ghi chú diễn giả; 2-11 giữ lời giải đầy đủ. |
| T5 | trung bình | 4-01 | "Trực quan." nhắc lại Bước 1 của chứng minh, đồng thời làm câu nối mạch 3→4. | "**Trực quan.** Hai lần chạy gần nhau thì, theo (L), hàm lỗi gần nhau tại mọi $z$."; chứng minh Định lý 08.6, Bước 1–2; `common-brief.md`: "'Trực quan.' nêu cơ chế hoặc cách đọc kết quả (đơn vị, trường hợp cực biên), không nhắc lại phát biểu hay một bước chứng minh". | Dòng đầu (không nhãn, câu nối): "Mệnh đề 08.5 chặn $\mathbb E\Delta_{T+1}$; theo (L), hiệu hàm lỗi tại mọi $z$ không quá $G\Delta_{T+1}$." "**Trực quan.** Gấp đôi ngân sách độ dài bước thì cận gấp đôi; gấp đôi cỡ mẫu thì cận giảm một nửa." (cách đọc đơn vị đã có ở mục 4 cột (a)). Bù: "(b) ổn định đều, $\epsilon_{\mathrm{stab}}(m)$ bằng số đó" thành "(b) $\epsilon_{\mathrm{stab}}(m)$ bằng số đó". |
| T6 | trung bình | 4-05 | Kết quả chính không có trang ý tưởng chứng minh (mục 4, điểm 2). | 7-01 có hàng Hệ quả 08.7; quy định "Mỗi kết quả chính có trang 'Ý tưởng chứng minh' riêng". | Thêm "Ý tưởng chứng minh: tính ổn định của điểm lặp trung bình", ba bước của ghi chú (tam giác; Mệnh đề 08.5(b) cho $t-1$ bước; đổi thứ tự lấy tổng, $\eta_k$ xuất hiện $T-k$ lần) và (L), Định lý 06.10. |
| T7 | trung bình | 6-07 | $\tau$ dùng trên mặt trang mà chỉ được định nghĩa ở ghi chú diễn giả. | Lời giải: "$\tau-2>65{,}2$, nên $\tau\ge68$"; ghi chú diễn giả: "Kí hiệu $\tau$ là chỉ số đầu tiên có $\Delta_\tau>\tfrac12$." | Đề bài: "Suy ra chỉ số đầu tiên $\tau$ có $\Delta_\tau>\tfrac12$ nằm trong một khoảng …". |
| T8 | trung bình | 6-03 (và 2-02) | Dòng Nhận xét 08.11 dùng (T3) chưa có trên mặt trang, bỏ $G=1$ và ba giả thiết; dòng $275{,}6$ thiếu $G=1$. | "Nhận xét 08.11 (đọc thêm): thêm (T3) và $\eta_t\le c/t$; với $\beta=10$, $c=1$, $m=10^4$, $T=10^6$: $\le33{,}37>1$."; ghi chú: "$G$-Lipschitz trên $\mathbb R^p$", "$\eta_t$ không tăng", "SGD không chiếu", "Với $\beta=10$, $c=1$, $G=1$, …". 2-02 không có (T3). | Chuyển dòng Nhận xét 08.11 sang ghi chú diễn giả (đã có công thức đầy đủ ở đó); dòng $275{,}6$ thêm "$G=1$". Thêm "(T3) $\ell(w,z)\in[0,1]$" lên 2-02 cho đủ danh sách §2. |
| T9 | trung bình | 5-01 | $\operatorname{opt}_S$ và $\tilde w$ xuất hiện lần đầu trên mặt trang mà không có nghĩa. | "**Nhắc lại:** Mệnh đề 06.5(b): $\mathbb EL_D(\tilde w)-\inf_WL_D\le\ldots+\mathbb E\operatorname{opt}_S(\tilde w)$"; mục 12 ghi 5-01 "đưa vào" $\tilde w$, $\operatorname{opt}_S$. | "Nhắc lại: với đầu ra $\tilde w$ và sai số tối ưu thực nghiệm $\operatorname{opt}_S$ (Định nghĩa 04.2), Mệnh đề 06.5(b): …". |
| T10 | trung bình | 1-03 | Mục tiêu 2 thay điều kiện chính xác bằng "độ dài bước nhỏ" (mục 4, điểm 8). | "Chứng minh bước gradient không giãn với hàm lồi, trơn và độ dài bước nhỏ."; ghi chú, Mục tiêu 2: "khi độ dài bước không vượt hai lần nghịch đảo hằng số trơn"; Ví dụ 08.3, 08.9 cho thấy ngưỡng chặt. | Mục tiêu 2: "Chứng minh bước gradient không giãn khi hàm lồi, trơn và độ dài bước không vượt hai lần nghịch đảo hằng số trơn." ($23$). Bù để còn $\le80$: mục tiêu 1 "Mô tả hai lần chạy ghép cặp; tính khoảng cách giữa chúng." ($12$), mục tiêu 3 bỏ "kì vọng" cuối ($19$), mục tiêu 5 "Kiểm tra giả thiết, tách kết quả chứng minh được khỏi phỏng đoán." ($13$): tổng $12+23+19+15+13=82$; nếu cần đúng $80$, mục tiêu 4 "Chọn số bước, độ dài bước từ cận ổn định và cận tối ưu." ($14$) và chấp nhận $81$, hoặc điều phối viên ghi ngoại lệ $\le85$ như Bài 05 giữ "hàm lồi". |
| T11 | trung bình | 1-01 | Luận điểm $66$ âm tiết; bản ngắn $43$ thay điều kiện bằng "đủ nhỏ" (mục 4, điểm 9). | Mục 2; `lec-07/review-log.md`: "bản một câu 47 âm tiết". | Bản $60$ âm tiết ở mục 4, điểm 9. |
| T12 | trung bình | 7-02 | "cận tăng theo hàm mũ" mất điều kiện; với $\eta_t=c/t$ cận tăng theo đa thức. Dòng đầu chưa trả lời thẳng "như thế nào". | "Không lồi: cận tăng theo hàm mũ; …"; ghi chú §10: "Mệnh đề 08.10 (tăng theo hàm mũ với độ dài bước hằng)"; đoạn sau Mệnh đề 08.10: "$\eta_t=c/t$ … tăng theo đa thức của $T$". | "Không lồi: cận tăng theo hàm mũ của ngân sách độ dài bước; …". Dòng 1 mở bằng "Thuật toán tác động qua ngân sách độ dài bước:" rồi công thức. Dòng 2 thêm "với $10^4$ hồ sơ". |
| T13 | trung bình | 5-04 | Trang chép gần nguyên Định nghĩa 08.9 và mở bằng định nghĩa; trang ở trần $60$. | Ba dòng định nghĩa trên mặt trang trùng ba gạch đầu dòng của ghi chú; ghi chú có câu dẫn "Chọn số bước, thêm số hạng phạt và để quá trình huấn luyện tự chọn nghiệm là ba cách khác nhau điều khiển đầu ra". | Dòng mở: "Ba cách điều khiển đầu ra của một thuật toán huấn luyện:"; ba dòng ngắn, mỗi dòng tên thuật ngữ, tiếng Anh, $\le8$ âm tiết; điều kiện "chọn trước khi chạy hoặc bằng mẫu xác thực độc lập" giữ; dòng cuối thêm "(Mệnh đề 06.11)" sau $\frac{2G^2}{\lambda m}$. Ước $\approx48$. |
| L1 | nhẹ | mục 11.1 | "12 trang, 28 phút" trái bảng mạch ($30$ phút). | Bảng mạch hàng 2; cộng thời lượng mục 6: $30$. | Sửa thành $30$ phút. |
| L2 | nhẹ | 1-02 | $w_1$ và $\xi$ dùng trước khi có nghĩa. | "(T2): $\ell\ge0$, $\ell(w,\cdot)$ đo được, $L_D(w_1)<\infty$"; "$\mathbb E_\xi\ell(A(s;\xi),z)$". | "$L_D(w_1)<\infty$ tại khởi tạo $w_1$"; "$\xi$: nguồn ngẫu nhiên riêng của $A$". |
| L3 | nhẹ | 2-01 | $\bar w_T$ không có tên trên mặt trang. | "Đầu ra $A(S;\xi)=w_{T+1}$ (điểm lặp cuối, last iterate) hoặc $\bar w_T$". | "… hoặc điểm lặp trung bình $\bar w_T$". |
| L4 | nhẹ | 2-08 | "Trực quan." viết $f''$ trong khi bổ đề không cần khả vi hai lần. | Ghi chú diễn giả 2-08: "Bổ đề không cần $f$ khả vi hai lần." | Thêm "khi $f$ khả vi hai lần" (T4 đã gồm). |
| L5 | nhẹ | 4-02 | Dòng "Nhắc lại:" nêu kỹ thuật không dùng trong chứng minh này. | "**Nhắc lại:** Định lý 06.10 dựa trên lập luận đổi vai (Bài 06)."; các bước 1–4 chỉ dùng Định lý 06.10 như một kết quả (đã nhắc ở 1-02). | Bỏ dòng; tên kỹ thuật vào ghi chú diễn giả ($-9$ âm tiết). |
| L6 | nhẹ | 5-02 | Bước 2 thiếu (G) trong ngoặc giả thiết. | "(Định lý 05.14; (S), $W$ lồi, (R))"; Phụ lục C Bước 2: (G2) với hằng số $G$ theo (G). | "(Định lý 05.14; (S), (G), $W$ lồi, (R))". |
| L7 | nhẹ | 5-03, F3 | "nhỏ nhất $0{,}0958$" là giá trị làm tròn lên của $0{,}095706$. | Ví dụ 08.7: "Bảng ghi cận (làm tròn lên)". | "nhỏ nhất $\le0{,}0958$"; chấm F3 vẽ tại $0{,}0957$, nhãn "≤ 0,0958". |
| L8 | nhẹ | 6-01 | "Chỉ $i_1=i$" mơ hồ. | Ghi chú: "$i_1=i$ và $i_t\ne i$ với mọi $t\ge2$". | Viết đúng như ghi chú. |
| L9 | nhẹ | 3-02, 6-04 | $g_t$ có hai nghĩa trên mặt trang (gradient tại $z_i$; gradient ngẫu nhiên); ghi chú có ba nghĩa (thêm Bước 4 chứng minh Định lý 08.6). | 3-02 bước 2; 6-04 giả thiết. | Deck theo ghi chú; ghi chú diễn giả 6-04 nói rõ nghĩa mới; đề xuất sửa ghi chú ở mục 7. |
| L10 | nhẹ | 6-06 | "Kết luận:" rút mất điều kiện "chỉ lớp ra được huấn luyện … hàm lỗi logistic"; $\Theta_1$, $\Theta_2$ chưa có nghĩa. | Ghi chú, cuối Ví dụ 08.10. | "áp dụng khi lớp ẩn cố định, chỉ lớp ra được huấn luyện"; "ma trận lớp ẩn $\Theta_1$, lớp ra $\Theta_2$". |
| L11 | nhẹ | 7-03, 7-04 | Câu hỏi (d)(i) đặt trên trang lời giải; $J$, $\chi(x)$ chưa có nghĩa trên mặt trang. | 7-04: "(d)(i) Cố định lớp ẩn, … cận ổn định và cái giá?"; 7-03 "$J=2$"; 7-04 "$G=\sup_x\lVert\chi(x)\rVert$". | Câu hỏi (d)(i) lên 7-03; "$J=2$ lớp"; "$\chi(x)$: véc-tơ đặc trưng ngẫu nhiên của Ví dụ 07.3". |
| L12 | nhẹ | 3-00…7-00 | Dòng dẫn mạch 4 và 7 thiếu điều kiện so với cách đặt cạnh kết quả khác. | Mạch 4: "tăng không nhanh hơn tổng các độ dài bước chia cho cỡ mẫu"; mạch 7: "khi hàm lỗi lồi, trơn" (thiếu gradient bị chặn, điều kiện độ dài bước). | Mạch 4: "Với hàm lỗi lồi, trơn, khoảng cách tổng quát hóa kì vọng bị chặn bởi một hằng số nhân tổng độ dài bước chia cho cỡ mẫu." (đếm lại $\le25$); mạch 7 thêm "có gradient bị chặn". |
| L13 | nhẹ | F4 | Vạch trục ngang $2;21;41;58;81;101$ lẫn vạch đều và vạch đánh dấu điểm. | Mục 8, F4. | Vạch $2;21;41;61;81;101$; điểm $t=58$ đánh dấu bằng chấm và nhãn. |
| L14 | nhẹ | 7-06 | Mục 15 ghi trần 80 cho 7-06; `deck_lint.py` dùng 60 vì tiêu đề "Bài tập về nhà" không khớp mẫu. | `deck_lint.py`: `cap = 80 if re.search(r'Mục tiêu|Nội dung|[Tt]ổng kết', title)`. | Ghi trần 60 (7-06 đếm $49$, vẫn đạt). |
| L15 | nhẹ | 4-01, 4-02, 5-01, 5-02, 6-04 | Tiêu đề trộn "SGD" trong khi tiêu đề mạch dùng "hạ gradient ngẫu nhiên". | Workspace CLAUDE.md: "Titles never mix languages when a clear Vietnamese phrase exists"; mục 11.14. | Điều phối viên quyết; nếu giữ tên kết quả của ghi chú, chỉ giữ ở 4-01 (tên Định lý 08.6), các tiêu đề khác dùng "hạ gradient ngẫu nhiên". |
| L16 | nhẹ | ghi chú diễn giả 2-08, 2-10, 7-00, 1-04 | Siêu ngôn (interpretive metadiscourse) và câu điều hướng (`no-ai-slop` Detect). | 2-08: "Câu trực quan đọc bổ đề trong trường hợp một chiều"; 2-10: "Cột 'Lõm' cho thấy …", "Dòng cuối nêu chỗ còn thiếu"; 7-00: "Bài có một bổ đề …", "sau đó là câu trả lời cho vấn đề trung tâm, một bài tập …"; 1-04: "Cuối cùng, các phản ví dụ cho thấy …". | Nêu thẳng nội dung: 2-10 "Không có tính lồi, bước gradient giãn với mọi độ dài bước dương, dù hàm vẫn $1$-trơn."; 7-00 bỏ câu liệt kê trang sau; không lấy "Bài" làm chủ ngữ. |
| L17 | nhẹ | ghi chú diễn giả 4-01 | Liệt kê phủ định (negative listing) thay cho nghĩa dương của bảo đảm. | "không có cận với xác suất cao, và cận chặn trị tuyệt đối của kì vọng, không chặn kì vọng của trị tuyệt đối". | Một câu dương: "Bảo đảm theo kì vọng theo $(S,\xi)$, cho $\lvert\mathbb E[L_D-L_S]\rvert$"; giới hạn "không có cận với xác suất cao" để ở 7-01 như §10. |

## 6. Cắt cụ thể để đạt trần và hạ trung vị

Số ước bằng `cnt.py` trên câu chữ đề xuất; người viết deck đếm lại bằng `deck_lint.py`.

| Trang | Hiện | Cắt | Ước sau |
|---|---:|---|---:|
| 1-06 | 63 | "mỗi nhãn bị lật" → "nhãn lật" ($-2$); cột "Số vòng" → "Vòng" ($-1$); "**Câu hỏi:** đại lượng nào quyết định khoảng cách?", phần "chỉ số bước thay đổi" vào ghi chú diễn giả ($-4$) | 56 |
| 7-01 | ≈94–103/80 | bỏ chữ "kì vọng theo $\xi$", "kì vọng theo $(S,\xi)$" ở ô Kết quả, thay bằng chỉ số dưới trong công thức ($\mathbb E_\xi\Delta_{T+1}$, $\lvert\mathbb E_{S,\xi}[\ldots]\rvert$, $\mathbb E_{S,\xi}L_D(\bar w_T)$): loại bảo đảm vẫn hiện trên mặt bảng ($-12$); "hai loại bước, tổng triệt tiêu" → "hai loại bước" ($-2$); "trung bình các $\Delta_t$" → "trung bình $\Delta_t$" ($-1$). Nếu vẫn $>80$: tách bảng hai trang như Bài 06 (7-01/7-02) | ≈78–82 |
| 7-04 | ≈88 | ô "$W$ lồi" bỏ "($W$ là toàn bộ không gian tham số)" vào ghi chú diễn giả ($-6$); "Ba giả thiết tối ưu không thỏa (Ví dụ 08.10), nên $0{,}4$ không có căn cứ" → "Ba giả thiết không thỏa (Ví dụ 08.10): $0{,}4$ không có căn cứ." ($-4$); câu hỏi (d)(i) lên 7-03 ($-15$); lời giải (d)(i) một dòng ($\le16$) | ≈57 |
| 2-04 | 53 | thêm dòng mở T1 ($+14$); gộp hai dòng bước chung/khác biệt ($-6$); dòng "ngân sách độ dài bước" giữ thuật ngữ, bỏ "$\sum_{t=1}^T\eta_t$" lặp ở 3-01 | ≈58 |
| 2-09 | 54 | dòng "Kỹ thuật." bỏ vế "với $f=-\tfrac12w^2$, $q_u$ không có cực tiểu" vào ghi chú diễn giả ($-7$) | 47 |
| 4-02 | 55 | L5 ($-9$) | 46 |
| 4-03 | 53 | bỏ "Diễn giải:" (trùng dòng "$1$ sau một vòng, $100$ sau $100$ vòng"; ý "vượt $1$ từ vòng thứ hai" vào ghi chú diễn giả) ($-11$) | 42 |
| 4-04 | 59 | dòng tỉ lệ đổi nhãn vào ghi chú diễn giả (cùng lý do hàm lỗi 0–1 không Lipschitz) ($-12$) | 47 |
| 5-04 | 60 | T13 | ≈48 |
| 6-02 | 53 | dòng "Bước hằng: …" vào ghi chú diễn giả; dạng bước hằng đã dùng ở 6-03 ($-7$) | 46 |
| 6-03 | 57 | dòng Nhận xét 08.11 vào ghi chú diễn giả (T8) ($-20$) | ≈37 |
| 6-04 | 55 | số $0{,}0153$ của hồi quy logistic vào ghi chú diễn giả; giữ "**Bảo đảm:** tính dừng (stationarity), theo kì vọng" ($-10$) | ≈45 |
| 7-05 | 59 | câu 4 → "Cận ở câu 3 có chặn hiệu lỗi phân lớp không?" ($-6$) | 53 |
| 7-07 | 58 | gộp dòng "Sau buổi học: Hardt, Recht và Singer (2016), §…" với dòng tài liệu đầy đủ ($-6$) | 52 |

Sau các cắt này có khoảng $20$ trên $40$ trang nội dung $\le50$ âm tiết, nên trung vị $\approx50$–$51$, khớp mức Bài 06 ($49$) và Bài 07 ($\approx52$). Trang chép ghi chú nhiều nhất là 5-04 (Định nghĩa 08.9), 6-04 (đủ bốn thành phần của một kết quả đọc thêm), 2-04 và 2-07 (định nghĩa). 2-07 chấp nhận được vì dòng ví dụ dấu bằng và hàm lõm là phần giải thích. 6-06 chép Ví dụ 08.10 ở mức chấp nhận được vì 7-04 dùng lại ba sự kiện đó.

## 7. Đề xuất sửa ghi chú (bổ sung mục 13 của storyboard)

| Mức độ | Vị trí | Vấn đề | Đề xuất |
|---|---|---|---|
| nhẹ | chứng minh Mệnh đề 08.5 Bước 2; chứng minh Định lý 08.6 Bước 4; Mệnh đề 08.12 | $g_t$ ba nghĩa: $\nabla\ell(w_t,z_i)$, $\nabla\ell(w_t,z_{i_t})$, gradient ngẫu nhiên của $F$ | Đổi tên cục bộ ở một chỗ (ví dụ $\gamma_t$ ở Bước 2 của Mệnh đề 08.5) hoặc thêm dòng "Kí hiệu" vào bảng §2 |
| nhẹ | mục 13 storyboard, hàng 1 | đồng ý đề xuất thêm điều kiện độ dài bước vào đoạn sau Câu hỏi mở đầu | — |

## 8. Kiểm liên tục (bảng kiểm Outline/Threads/Concept của quill)

- Thứ tự khái niệm theo mục ghi chú: §1–§13 ánh xạ vào bảy mạch liên tiếp. Lệch nhỏ chấp nhận được: Thuật toán 08.1 (§4) lên 2-01 trước §2–§3; Ví dụ 08.1 Bước 3 dùng phép cập nhật của Thuật toán 05.11 nên không cần Thuật toán 08.1.
- Thuật ngữ: khớp bảng mục 10 và `thuat-ngu.md` ("hai lần chạy ghép cặp", "bước chung", "bước khác biệt", "ngân sách độ dài bước", "hệ số giãn", "đồng bức", "tỉ lệ đổi nhãn dự đoán"). Mỗi thuật ngữ có tiếng Anh ở lần đầu trên trang nội dung.
- Kí hiệu: $\Delta_t$ khác nghĩa với Bài 05 đã ghi ở ghi chú diễn giả 2-04. $g_t$ có hai nghĩa (L9). Kí hiệu chưa có nghĩa trên mặt trang: $\tau$ (T7), (T3) (T8), $\operatorname{opt}_S$, $\tilde w$ (T9), $w_1$, $\xi$ ở 1-02 (L2), $\Theta_1$, $\Theta_2$ (L10), $J$, $\chi$ (L11).
- Mạch nối trên mặt trang: 2→3 (2-10 dòng cuối) đạt; 3→4 cần dòng nối riêng ở 4-01 (T5); 4→5 (4-05 dòng đầu, 5-01 "Nhắc lại:") đạt; 5→6 (6-01 mở bằng phản ví dụ) đạt; 6→7 (6-06 "Kết luận:") đạt.
- Kỹ thuật: nhắc lại đúng tên và ID của bài trước (tổng triệt tiêu `L05-4-05`, cân hai số hạng `L05-4-08`, kì vọng có điều kiện theo lịch sử `L05-3-07`). Dòng lập luận đổi vai ở 4-02 thừa (L5). Ghép cặp cần nhãn "Kỹ thuật." (T3).
- Không trang nào dẫn kết quả của trang sau hay bài sau trên mặt trang. 6-04 ghi chú diễn giả và mục 4 nói "Bài 10 dùng lại" chỉ trong storyboard, không lên mặt trang (đúng).
