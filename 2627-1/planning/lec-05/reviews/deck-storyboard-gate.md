# Duyệt cổng storyboard — bộ trang chiếu Bài 05

Người duyệt cổng (chỉ đọc), 2026-11-15. Đối tượng: `planning/lec-05/storyboard.md` (toàn bộ, mục 1–15). Đối chiếu: `materials/lec-05/lecture-note.md`, `materials/lec-05/exercises.md`, `CLAUDE.md` § Slide decks, `deck-build/common-brief.md` (gồm "Các quy định dễ sót" và "Bài học từ năm báo cáo duyệt deck 01"), `brief-gate.md`, mục "Bộ trang chiếu" của `lec-0{1,2,3,4}/review-log.md`, mục 14 của `lec-04/storyboard.md`, deck đã xuất bản `lecture-01-mo-hinh-hoc.html` (và `lecture-04-phan-tich-sai-so.html` cho tiền lệ tiêu đề), `planning/diem-toan-can-doc-2026-11-13.md` mục 3. `no-ai-slop` chế độ Detect cho văn bản dự kiến; phần Outline/Threads/Concept của `quill` làm bảng kiểm thứ tự khái niệm, thuật ngữ, kí hiệu.

Script độc lập (thư mục nháp `/tmp/claude-1000/-data-tqlong-lectures/8b2132a8-acd0-44df-9be8-dfd28f705b6b/scratchpad/lec-05/gate/`): `num.py` (tính lại V1–V26, F3, F4), `syl.py` (âm tiết mặt trang), `notes.py` (âm tiết ghi chú diễn giả). Không đọc `count.py`, `num.py` của người lập storyboard trước khi tính.

## Kết luận

**Đạt khi sửa.** 0 chặn bàn giao, 1 nghiêm trọng, 12 trung bình, 21 nhẹ.

Mọi con số V1–V26 tính lại khớp ghi chú và tệp bài tập. Phát biểu của Mệnh đề 05.13, Định lý 05.14, Hệ quả 05.15, 05.16 khớp ghi chú; Hệ quả 05.19 thiếu ba thành phần giả thiết trên mặt trang (T6). Hai lỗi dữ liệu hình: trục không chứa hết dữ liệu ở F3 và F4 (T1, T2). Phát hiện nghiêm trọng duy nhất là câu luận điểm ở trang bìa (N1).

## 1. Tính lại số (V1–V26, F1–F5)

| Mục | Kết quả tính lại | Khớp |
|---|---|---|
| V1, V7 | $L_S(w_3)=0{,}063858$; $i_3=1,2,3$: $0{,}071030$; $0{,}102142$; $0{,}069380$; trung bình $0{,}080851$; GD $0{,}061359$; $\nabla L_S(w_3)=(-0{,}25183;0{,}11984)$, chuẩn trước chiếu $1{,}13237$ | có |
| V2, V3, V4, V5, V6 | $\tfrac23$; $(-2,0)$, $(0,2)$, $(0,0)$, $(-\tfrac23,\tfrac23)$; $0{,}5<0{,}6$; $0{,}76537$, $-0{,}12132$; $(18,0)$ | có |
| Phụ lục D | $M$, $c$ đúng; nghiệm không ràng buộc $(1{,}06;-0{,}92)$, chuẩn $1{,}40357$, $L_S=0{,}006667$; $\kappa=0{,}134956$, $w^*=(0{,}74733;-0{,}66445)$, $L_S(w^*)=0{,}0611167$ | có |
| V8 | $0{,}505340$; $0{,}058628$ ($0{,}003437$); $0{,}420040$ ($0{,}176434$); vế trái $1{,}328906$; vế phải $1{,}501903$, không chiếu $1{,}328906$ | có |
| Bài tập 05.2(c) (ghi chú diễn giả 4-02) | $\lVert w_3-w^*\rVert=0{,}0586$, $\lVert w_4-w^*\rVert=0{,}1112$ với $i_3=1$: ra xa $w^*$ | có |
| V9, V26 | $400$; $1600$; $6400$; $\eta^*=0{,}00625$; $4{,}000625$; thừa số $1{,}25$, $5{,}05$; $Q(\eta)$ tại mười điểm: $0{,}629$; $0{,}3205$; $0{,}17225$; $0{,}125$; $0{,}1$; $0{,}125$; $0{,}2125$; $0{,}40625$; $0{,}505$; $0{,}803125$ | có (xem T1 về trục) |
| V10, V11 | $10^4$, $0{,}05$, $10^{10}$; $\sum\eta_t=19{,}638036$, $\sum\eta_t^2=0{,}497205$, vế phải $0{,}228009$ | có |
| V12 | $G=2{,}25$, $\eta=0{,}0277778$, $RG/\sqrt T=0{,}140625$; lặp 1600 bước: điểm lặp trong $[-1{,}5;-1]$, $\bar w=-1{,}005625$, $f(\bar w)=0{,}500032$; $s=-0{,}121320$; $w_{25}=-1{,}1268$, $w_{26}=-1{,}1198$ | có |
| V13, V14, V15 | $-0{,}5$; $0{,}7$; $-1{,}7$; $0{,}086977$; $1{,}69$; $164$; $12{,}80625$; $0{,}025/T$; $\psi=2w-0{,}2$, $L_S(0{,}1)-0{,}25=0{,}16$ | có |
| V16, V17, V18 | $640\,000$, $400$, $4\cdot10^6$; $T(b)=1600;\ 475;\ 194;\ 124;\ 106$, số quan sát $1600;\ 1900;\ 3104;\ 7936;\ 27\,136$; $0{,}9875^{1600}=1{,}817\cdot10^{-9}$, $\bar w=0{,}95$, $L_S=0{,}0025$, $L_D=1{,}9025$ | có |
| V19–V24 | $(0{,}5;-0{,}5)$, kiểm tra $2=1+1$; chín ô và trung bình $0{,}845985$, ba hàng $0{,}71623$; $0{,}88053$; $0{,}94119$, $\mathbb EL_S(w_2)=0{,}55556$, $0{,}494439$; $Q=0{,}0625$, $0{,}25$; $b=30$, $150$, $T=110$ (đúng theo số học chính xác), $3300$, $16\,500$; $\log_220=4{,}3219$, $32\,000$, $m<121\,600$ | có |
| Bài tập 05.4(b) (ghi chú diễn giả 4-10) | $\eta=0{,}01$: $2500$; $\eta=0{,}00625$: $1600$, cực đại của $\eta(2\epsilon-\eta G^2)$ | có |
| F1, F2, F5 | trục chứa hết dữ liệu: F1 phải $f(1{,}6)=2{,}4336<2{,}5$; F5 $f(-2)=1{,}5<1{,}6$, điểm gãy $1{,}265625$ | có |
| F3 | elip $L_S=0{,}063858$: trị riêng $\tfrac13$, $\tfrac23$, véc-tơ riêng $(-0{,}8;0{,}6)$, $(0{,}6;0{,}8)$, bán trục $0{,}41421$, $0{,}29289$ đúng; **khoảng $y$ của elip là $[-1{,}2616;-0{,}5784]$**, khoảng $x$ là $[0{,}6849;1{,}4351]$ | bán trục có; trục $y$ không (T2) |
| F4 | **$Q(0{,}1)=0{,}803125>0{,}8$**, số hạng $8\eta$ chạm $0{,}8$ | không (T1) |

## 2. Phát biểu kết quả so với ghi chú

| Kết quả | Trang | Giả thiết | Loại bảo đảm, đại lượng | Nhận xét |
|---|---|---|---|---|
| Mệnh đề 05.13 | 4-01 | $W$ khác rỗng, đóng, lồi; $w,g$, $\eta>0$, $w^+$; $u\in W$ | tất định, không dùng tính lồi của $F$ hay xác suất; dấu bằng khi $W=\mathbb R^p$ | khớp |
| Định lý 05.14 | 4-03 | (C); (G1), (G2) với $G$; Thuật toán 05.11, $w_1$ tất định, $\eta$ hằng, $T\ge1$; $u\in W$ tất định | kì vọng theo $\xi_1,\ldots,\xi_{T-1}$; độ chênh tối ưu tại $\bar w_T$ | khớp; "hàm mà oracle không chệch" chỉ ở ghi chú diễn giả (gợi ý ở T5) |
| Hệ quả 05.15 | 4-07 | như Định lý 05.14; $G,R>0$; $\eta=R/(G\sqrt T)$ | kì vọng theo $\xi$; (a), (b) $F_R$, (c) $T\ge R^2G^2/\epsilon^2$; $T$ cố định trước | khớp |
| Hệ quả 05.16 | 4-09 | thiếu "$R>0$", "$u\in W$" | tất định | L5 |
| Hệ quả 05.19 | 6-02 | thiếu $w_1\in W$, $G>0$, ánh xạ oracle $\varphi(w,i)=v(w,z_i)$ và tên Thuật toán 05.11; có $W$ bị chặn, $\ell\ge0$ lồi, $\lVert v\rVert\le G$, rút có hoàn lại, $\eta$ | (a) kì vọng theo $\xi$ với mọi $s$; (b) xác suất theo $\xi$, $\delta'$ khác $\delta$; đại lượng $\operatorname{opt}_s(\bar w_T)$ | T6 |
| Mệnh đề 05.20 [O] | 6-04 | (G1); $\sigma^2$, $G_F$ trên $W$; $b$ lần rút độc lập | kì vọng theo $\bar\xi$ | khớp; mức đọc thêm ở ghi chú diễn giả |
| Bổ đề 05.8, 05.12; Mệnh đề 05.3, 05.5 | 3-02, 3-06, 2-04, 2-06 | đủ | tất định / hầu chắc chắn | khớp; xem L21 về chép ghi chú |

Bảng tổng kết 7-01 và trang 7-02 rút gọn mất giả thiết (T7, T12).

## 3. Điểm toán học mở #3 (Ví dụ 05.12) ở 5-03

Mặt trang 5-03 viết "Điểm lặp cuối (last iterate): $f(w_t)=0{,}1=\eta G^2/2$ với mọi $t$" và "Định lý 05.14 chặn $f(\bar w_T)$: $\bar w_T=0$ khi $T$ chẵn, và $0\le0{,}025/T+0{,}1$". Toán đúng: GD với dưới gradient $\operatorname{sign}(w)$ là oracle tất định thỏa (G1), (G2) với $G=1$; $u=0$, $\lVert w_1-u\rVert^2/(2\eta T)=0{,}01/(0{,}4T)$. Trường hợp $T$ lẻ ở ghi chú diễn giả: $f(\bar w_T)=0{,}1/T\le0{,}025/T+0{,}1$ với mọi $T\ge1$. Deck không chép câu kết luận của Ví dụ 05.12 (dòng 1030) nhưng không mâu thuẫn số nào của ghi chú, và trùng với cách đọc mà chính ghi chú dùng ở §11 (dòng 1204: "trong khi điểm lặp trung bình bằng $0$ khi $T$ chẵn"). Ý kiến: chấp nhận; điều phối viên ghi độ lệch so với câu dòng 1030 vào `review-log.md`, chờ tác giả.

## 4. Câu chữ bài tập rút gọn (mục 11, điểm 17)

| Trang | Bài | Đủ ý | Ghi chú |
|---|---|---|---|
| 2-07 | 05.1(d) | đúng nguyên văn | — |
| 3-08 | 05.3(b) | đủ: "vế phải của (a)" thành "vế phải của Bổ đề 05.12(c)" là cùng đại lượng $\mathbb E\langle\psi(w_2),w_2-u\rangle$; dòng thiết lập "Thiết lập của Ví dụ 05.6, $u=w^*$; …rút đều có hoàn lại" giữ đủ bốn thành phần (mẫu, oracle, $W$, $w_1$, $\eta$ có trên 3-05) | số của $w^*$ chỉ ở 3-05, ba trang trước (L8) |
| 4-10 | 05.4(c) | đúng nguyên văn | — |
| 5-04 | 05.3(c) | đủ | — |
| 6-06 | 05.5(b) | đủ ý câu hỏi; dòng thiết lập bỏ "(Hệ quả 05.16 với $G=G_F$)" | L15 |
| 7-03 | 05.5(d) | đúng nguyên văn | — |

Lời giải trên mặt trang khớp lời giải trong `exercises.md`; 7-04 bỏ một điều kiện của dòng kết luận (T8).

## 5. Mật độ và trang chép ghi chú

Đếm độc lập (`syl.py`, cùng quy ước của storyboard: số viết trong câu có tính, ô bảng chỉ có số không tính) khớp mục 15 của storyboard, trừ 6-05: dòng "Bảng" có nhãn cột "Số quan sát" và "GD" (deck_check đếm chữ trong bảng), nên khoảng $53$ thay cho $49$, vẫn dưới trần. 7-01 đếm $74$/80, 7-06 $45$/80. Một trang vượt trần: 7-03 ($68$, dưới $1{,}5$ lần trần, có lý do). Dòng chạm trần 20: 3-08 dòng 2, 6-01 dòng 1, 6-05 dòng 4–5. Không trang nào quá 6 dòng hay 3 công thức hiển thị.

Ghi chú diễn giả (`notes.py`, bỏ công thức và dòng nguồn): vượt 150 ở 1-06 ($154$), 2-01 ($157$), 7-07 ($180$); trang tiêu đề mạch vượt 100 ở 3-00 ($101$), 4-00 ($111$), 6-00 ($106$); trang chứng minh đều dưới 250 (4-04: $157$). Con số "(~170)", "(~200)" ghi trong storyboard cao hơn số đếm.

Trang chép khối ghi chú gần nguyên văn, không có trực quan trên mặt trang: 2-04 (Mệnh đề 05.3 đủ ba phần và giả thiết), 2-06 (Định nghĩa 05.4 và Mệnh đề 05.5 đủ hai phần), 3-06 (Bổ đề 05.12 đủ (a)–(c), phần (c) lặp đúng công thức của 3-07), 6-01 (Định nghĩa 05.18 kể cả điều kiện đo được). Mức độ nhẹ hơn Bài 04 vì các khối này là công cụ ngắn; đề xuất ở L21.

## 6. Bảng phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | 1-01 (N1) | Luận điểm khẳng định không điều kiện rằng mỗi bước kéo điểm lặp về phía điểm so sánh; sai với chính ví dụ của deck | Storyboard mục 2: "Mỗi bước hạ gradient ngẫu nhiên kéo điểm lặp về phía điểm so sánh, kèm một lượng nhiễu tỉ lệ với bình phương độ dài bước." Ghi chú §7 dòng 718: khoảng cách "thay đổi một lượng $-2\eta\langle g,w-u\rangle+\eta^2\lVert g\rVert^2$"; 4-01 chỉ nói "kéo về phía $u$ khi $\langle g,w-u\rangle>0$"; Bài tập 05.2(c) (ghi chú diễn giả 4-02): bước $i_3=1$ đưa khoảng cách tới $w^*$ từ $0{,}0586$ lên $0{,}1112$ | "Sau mỗi bước hạ gradient ngẫu nhiên, bình phương khoảng cách tới một điểm so sánh thay đổi một số hạng tỉ lệ với độ dài bước và tăng thêm một số hạng tỉ lệ với bình phương độ dài bước. Lấy trung bình các điểm lặp, cận của độ chênh tối ưu kì vọng tỉ lệ nghịch với căn bậc hai của số vòng lặp." Sửa cùng câu ở ghi chú diễn giả 1-01 (L1) |
| trung bình | 4-06, hình F4 (T1) | Trục dọc không chứa hết dữ liệu | Mục 8: "trục dọc tuyến tính $[0;0{,}8]$"; V26: $Q(0{,}1)=0{,}8031$, số hạng $8\eta=0{,}8$ tại $\eta=0{,}1$ | Trục dọc $[0;0{,}9]$ (vạch giữ nguyên), hoặc trục ngang dừng ở $0{,}09$ |
| trung bình | 3-05, hình F3 (T2) | Elip mức vượt khung dưới | Mục 8: trục $[-0{,}1;1{,}5]\times[-1{,}1;0{,}2]$; elip tâm $(1{,}06;-0{,}92)$ với bán trục $0{,}4142$ theo $(-0{,}8;0{,}6)$, $0{,}2929$ theo $(0{,}6;0{,}8)$ có $y\in[-1{,}2616;-0{,}5784]$ | Trục $y$ $[-1{,}3;0{,}2]$ (tỉ lệ bằng nhau giữ được); khung phóng to quanh $w_3$ là bắt buộc (L22) |
| trung bình | 2-02 (T3) | Hành trình khái niệm đảo bước: Định nghĩa 05.1 đứng trước mọi ví dụ; ví dụ lồi/không lồi chỉ ở ghi chú diễn giả và ở 2-03 | Mục 7, hàng "Hàm lồi": ví dụ ở 2-03, phát biểu ở 2-02; quy định "problem → intuition → example → statement … not reordered"; tiền lệ T5 của cổng Bài 04 | Thêm trước dòng định nghĩa: "**Ví dụ.** $f(w)=(w^2-1)^2$: $f(0)=1>\tfrac12f(-1)+\tfrac12f(1)=0$, không lồi." (khoảng 5 âm tiết, trang lên $59$, 6 dòng) |
| trung bình | 3-03; 3-06, 4-09, 6-04 (T4) | Khái niệm chính (oracle) mở bằng định nghĩa, không có câu nối trên mặt trang từ cụm phép chiếu; ba chỗ nối giữa cụm khác chỉ ở ghi chú diễn giả (bài học deck 01) | 3-03 dòng 1 là "**Định nghĩa 05.10.**"; ghi chú §6 dòng 516: "Một gradient của $L_S$ tốn $m$ gradient trên từng quan sát … SGD thay nó bằng một véc-tơ ngẫu nhiên rẻ hơn, có trung bình đúng"; dòng 653 (trước Bổ đề 05.12), 909 (trước Hệ quả 05.16), 1123 (đầu §10) không lên mặt trang 3-06, 4-09, 6-04 | 3-03: dòng mở "Gradient của $L_S$ tốn $m$ gradient trên một quan sát; oracle thay nó bằng một véc-tơ ngẫu nhiên rẻ, có trung bình đúng.", bù chữ bằng cách chuyển công thức $\varphi(w,i)$ của dòng Ví dụ 05.5 sang dòng đầu 3-05 (đã nhắc oracle). 3-06: "Để chặn $\mathbb E\langle g_t,w_t-u\rangle$, cần trung bình của $g_t$ khi các lần rút trước đã biết." 4-09: "GD là oracle tất định, $g_t=v(w_t)$." 6-04: "Ví dụ 05.9 so hai đầu mút: một quan sát và cả tập." Điều phối viên đếm lại |
| trung bình | 4-03, 6-02 (T5) | "Trực quan." nhắc lại một bước chứng minh (bài học deck 02); ở 6-02 còn dùng $\operatorname{opt}_s$ trước khi $s$ được đặt | 4-03: "Cộng $T$ bất đẳng thức một bước: khoảng cách triệt tiêu, $\tfrac\eta2\lVert g_t\rVert^2$ cộng dồn" trùng Bước 2 của 4-04 và trang 4-05; 6-02: "$\operatorname{opt}_s\ge0$, nên bất đẳng thức Markov đổi cận kì vọng thành cận xác suất" trùng Bước 3 của 6-03 | 4-03: cách đọc vế phải, ví dụ "**Trực quan.** Vế phải là khoảng cách ban đầu chia cho tổng độ dài bước $\eta T$, cộng phần $\eta G^2/2$ mà mỗi bước góp."; và dòng cuối "Đại lượng được chặn: độ chênh tối ưu của $F$, hàm mà oracle không chệch, tại $\bar w_T$." 6-02: "**Trực quan.** Cận kì vọng không quá $\delta'\epsilon_{\mathrm{opt}}$ thì nhiều nhất một phần $\delta'$ số lần chạy có sai số tối ưu từ $\epsilon_{\mathrm{opt}}$ trở lên." (bằng lời, trước dòng giả thiết) |
| trung bình | 6-02 (T6) | Hệ quả 05.19 trên mặt trang thiếu giả thiết | Ghi chú dòng 1063–1066: "$G>0$", "$w_1\in W$", "$\varphi(w,i)=v(w,z_i)$", "Thuật toán 05.11 với $\eta=R/(G\sqrt T)$; đầu ra $\bar w_T$"; storyboard 6-02 chỉ có "$i_t$ đều, có hoàn lại; $\eta=R/(G\sqrt T)$" | Dòng 2: "…; SGD có chiếu (Thuật toán 05.11), $w_1\in W$, $\varphi(w,i)=v(w,z_i)$, $i_t$ đều, có hoàn lại; $\eta=R/(G\sqrt T)$, $G>0$." Bù chữ nhờ T5 |
| trung bình | 7-01 (T7) | Cột "Giả thiết không được bỏ" rút gọn mất giả thiết khi đặt cạnh kết quả khác (bài học deck 01) | Hàng Hệ quả 05.15: "$\eta=R/(G\sqrt T)$, $T$ chọn trước" (thiếu (C), (G1), (G2)); hàng Hệ quả 05.19: "rút có hoàn lại; $W$ bị chặn" (thiếu $\ell$ lồi, không âm, $\lVert v\rVert\le G$); ghi chú diễn giả tự nói "giữ mọi giả thiết" | "(C), (G1), (G2); $\eta=R/(G\sqrt T)$, $T$ chọn trước"; "$\ell\ge0$ lồi, $\lVert v\rVert\le G$; rút có hoàn lại; $W$ bị chặn". Giữ trần 80 bằng cách rút cột ý tưởng chứng minh (ví dụ "tổng triệt tiêu, lịch sử, lồi hữu hạn" → "tổng triệt tiêu, lịch sử"; Bước 5 đã ở 4-04) |
| trung bình | 7-04 (T8) | Dòng kết luận bỏ điều kiện so sánh chi phí | `exercises.md` lời giải 05.5(d) Bước 4: "Nếu một lần tính hàm lỗi tốn ngang một gradient trên một quan sát, cách này rẻ hơn …"; storyboard đặt điều kiện này chỉ ở ghi chú diễn giả | "**Kết luận:** nếu một lần tính hàm lỗi tốn ngang một gradient, ít hơn $640\,000$ khi $32\,000+5m<640\,000$, tức $m<121\,600$." (35 → khoảng 45) |
| trung bình | 7-06 (T9) | Bài tập 05.7 xếp sai mạch | Bài 05.7(c): "GD với gradient này làm gì?" cần GD (Thuật toán 05.9, mạch 3); mục tiêu của bài là mục tiêu học tập 5 ("bỏ tính lồi thì cực tiểu địa phương không còn là cực tiểu toàn cục"); "cực tiểu địa phương" lên mặt trang lần đầu ở 5-01 (Ví dụ 05.10); quy tắc "mạch cung cấp kiến thức cuối cùng bài đó cần" | Chuyển 05.7 sang hàng "5. Vai trò của từng giả thiết": $05.3,\ 05.6,\ 05.7$; sửa câu tương ứng ở ghi chú diễn giả 7-06 |
| trung bình | 4-04, ghi chú diễn giả (T11) | Câu tự mâu thuẫn về chỗ dùng giả thiết | "Mỗi giả thiết vào đúng một bước, nên bỏ một giả thiết làm hỏng đúng bước đó: tính lồi ở Bước 3 và 5"; ghi chú dòng 817: "Tính lồi của $F$ là điều kiện để (G1) thỏa được" | "(G1) vào Bước 3, (G2) vào Bước 4, tính lồi của $F$ và $W$ vào Bước 5 và là điều kiện để (G1) thỏa được; bỏ một giả thiết làm hỏng bước tương ứng." |
| trung bình | 7-02 (T12) | Dòng một bước viết như đẳng thức, trong khi có phép chiếu chỉ có bất đẳng thức | "Mỗi bước: $\lVert w_t-u\rVert^2$ giảm $2\eta\langle g_t,w_t-u\rangle$, tăng $\eta^2\lVert g_t\rVert^2$"; Mệnh đề 05.13: dấu bằng chỉ khi $W=\mathbb R^p$ | "Mỗi bước: $\lVert w_{t+1}-u\rVert^2\le\lVert w_t-u\rVert^2-2\eta\langle g_t,w_t-u\rangle+\eta^2\lVert g_t\rVert^2$; $L_S$ có thể tăng." (ít chữ hơn) |
| trung bình | 6-07; bảng mạch (T13) | Mạch 6 ứng với §9, §10, §13, không liên tiếp; mạch 7 ghi §11–§14, trùng §13 | Mục 3: mạch 6 "§9–§10, §13", mạch 7 "§11–§14"; quy định "a strand maps to consecutive note sections" | Ý kiến ở mục 11, điểm 6 dưới đây: đặt trang ví dụ này đầu mạch 7 (sau 7-00, trước 7-01), hoặc giữ và ghi độ lệch vào `review-log.md` |
| nhẹ | 1-01, ghi chú diễn giả (L1) | Cùng lỗi với N1 | "bình phương khoảng cách tới một điểm so sánh giảm một lượng tỉ lệ với độ dài bước" | "thay đổi một số hạng tỉ lệ với độ dài bước, dương khi bước đi về phía điểm so sánh," |
| nhẹ | 3-01 (chú thích F2), 3-02 (L2) | $\pi$ dùng trước khi đặt | Chú thích F2: "$\langle\theta-\pi,u-\pi\rangle\approx-0{,}1213$"; mặt trang 3-01 chỉ viết $\operatorname{proj}_W(\theta)$; dòng "Trực quan." của 3-02 đứng trước dòng Bổ đề đặt $\pi$ | Dòng ví dụ 3-01: "$\pi=\operatorname{proj}_W(\theta)\approx(0{,}7071;-0{,}7071)$" |
| nhẹ | 3-04 (L4) | Phương pháp mới mở bằng tên và giả mã, không bằng giới hạn cụ thể của bước trước (`rl-plan/CLAUDE.md`, "A new method opens with the concrete limit…") | Dòng cuối 3-04: "Chi phí trên $L_S$: vòng GD tốn $m$ gradient …, vòng SGD tốn một." | Đưa dòng chi phí lên đầu trang |
| nhẹ | 4-09 (L5) | Giả thiết Hệ quả 05.16 thiếu $R>0$, $u\in W$ | Ghi chú dòng 916–917 | "…$\eta=R/(G\sqrt T)$, $R>0$; $u\in W$, $\lVert w_1-u\rVert\le R$." |
| nhẹ | 7-02, 7-01 (L6) | Dòng rút gọn thiếu $u\in W$; "kì vọng" không ghi "theo $\xi$" | 7-02 dòng 2: "…$\lVert w_1-u\rVert\le R$: $\mathbb EF(\bar w_T)-F(u)\le RG/\sqrt T$" | "$u\in W$, $\lVert w_1-u\rVert\le R$"; "kì vọng theo $\xi$" |
| nhẹ | 5-03 (L7) | Thứ tự thẻ ngược thứ tự ghi chú | Thẻ trái Ví dụ 05.13, thẻ phải Ví dụ 05.12; ghi chú: 05.12 (dòng 1021) trước 05.13 (dòng 1033) | Đổi chỗ hai thẻ, hoặc ghi lý do ("ba giả thiết trước, đầu ra sau") vào `review-log.md` |
| nhẹ | 3-08 (L8) | Người học không có số của $u$ trên trang; câu lời giải không nói trung bình hàng là gì | Dòng 1: "Thiết lập của Ví dụ 05.6, $u=w^*$"; dòng 3: "bằng trung bình ba hàng …" | "$u=w^*\approx(0{,}7473;-0{,}6645)$"; "bằng trung bình của $\langle\psi(w_2),w_2-u\rangle$ theo ba hàng: …" |
| nhẹ | 5-04 (L9) | Dòng cuối lời giải không nêu kết luận | "Bước 3 cần vế trái $\ge\mathbb EL_S(w_2)-L_S(u)\approx0{,}4944$." | Thêm "mà vế trái bằng $0$." |
| nhẹ | 7-04 (L10) | Tiền tố tiêu đề "Lời giải:" không có trong danh sách | Tiêu đề "Lời giải: nhiều lần chạy độc lập"; tiền lệ deck 04: "Bài tập: phản ví dụ bỏ hệ số $K$, lời giải" | "Bài tập: nhiều lần chạy độc lập, lời giải" |
| nhẹ | 4-06, F4 (L11) | Nhãn hình đặt tên cho hai số hạng, trái quy ước của chính storyboard | Mục 8: nhãn "khoảng cách", "nhiễu"; mục 6, quy ước cuối và mục 11 điểm 15: không đặt tên hai số hạng | Bỏ nhãn chữ; `figcaption` nêu kiểu nét: "nét đứt: $R^2/(2\eta T)$; nét chấm: $\eta G^2/2$; nét liền: tổng" |
| nhẹ | 7-05 (L12) | Câu hỏi 4 dùng thuật ngữ chưa lên mặt trang nào | "xáo trộn lại sau mỗi vòng" chỉ ở ghi chú diễn giả 3-03, 5-04 (mục 10) | Ghi "(random reshuffling)" ở 7-05, hoặc đổi câu 4 thành câu về giả thiết độc lập của Định nghĩa 05.10 |
| nhẹ | 1-03 (L13) | Mục tiêu 1 bỏ phạm vi "trên một hàm mục tiêu lồi"; mục tiêu 2 thành "Kiểm tra tính không chệch có điều kiện khi biết lịch sử", không rõ kiểm cho cách rút nào | Ghi chú dòng 32–33 | Giữ "cho hàm lồi" ở mục tiêu 1 và "cho cách rút có hoàn lại" ở mục tiêu 2; bù chữ bằng cách rút từ nối ở các mục tiêu khác ("chỉ rõ" → "chỉ"); trần 80, mỗi dòng ≤ 20, điều phối viên đếm lại |
| nhẹ | 1-06 (L14) | Câu hỏi bỏ vế thứ hai của câu hỏi mở đầu mà 4-09 trả lời | Ghi chú dòng 20: "… và cần bao nhiêu bước để đạt một độ chênh tối ưu cho trước?" | "**Câu hỏi:** SGD bảo đảm gì cho $L_S$ sau $T$ bước, và cần bao nhiêu bước?" (58) |
| nhẹ | 6-06 (L15) | Dòng thiết lập bỏ nguồn của số bước GD | `exercises.md` 05.5: "GD cần $R^2G_F^2/\epsilon^2$ bước (Hệ quả 05.16 với $G=G_F$)" | Thêm "(Hệ quả 05.16)" |
| nhẹ | 1-06, 2-01, 7-07; 3-00, 4-00, 6-00 (L16) | Ghi chú diễn giả dài quá mức đã chốt; 2-01 chép bảng nguồn ngẫu nhiên §1, 7-07 chép đoạn "Quan hệ với UML" §14 | Số đếm ở mục 5; quyết định T6/T8 của Bài 04 (≤ 150); `rl-plan/CLAUDE.md`: trang tiêu đề mạch 40–100 | 2-01: bỏ câu liệt kê tám thành phần; 7-07: giữ ba khác biệt (phép chiếu, cận mô-men, mọi $u$) và câu Bài 06; ba trang tiêu đề mạch cắt câu kết quả trao đi trùng dòng dẫn |
| nhẹ | mục 7, hàng "Dưới gradient" (L17) | Bảng hành trình mô tả sai trang 2-03 | "2-03 ($\lvert w\rvert=\max\{w,-w\}$: quy tắc (c) trên một chiều)", nhưng 2-03 không dùng quy tắc (c), Mệnh đề 05.3 chỉ có ở 2-04 | "2-03 ($\lvert w\rvert$: mọi $\lvert v\rvert\le1$ cho cận dưới tại $0$)" |
| nhẹ | 2-00, 4-00 (L18) | Dòng dẫn mạch dùng thuật ngữ nặng hoặc chủ ngữ trừu tượng làm việc của người | Mạch 2: "…nằm trên siêu phẳng afin của mỗi dưới gradient…"; mạch 4: "…chính cận đó chọn độ dài bước theo số vòng lặp" | Mạch 2: "Với hàm lồi, thông tin tại một điểm cho một cận dưới trên toàn không gian."; mạch 4: "Cộng các bất đẳng thức một bước cho cận kì vọng; độ dài bước theo số vòng lặp được chọn từ chính cận đó." |
| nhẹ | 1-06, 7-00, 1-04 ghi chú diễn giả (L19) | `no-ai-slop` Detect: tương phản nhị phân; câu điều hướng, mạch làm chủ ngữ | 1-06: "Bảo đảm của SGD vì vậy là một cận kì vọng tại trung bình các điểm lặp, không phải sự giảm ở từng bước."; 7-00: "Mạch cuối gom các giả thiết không được bỏ, trả lời vấn đề trung tâm cho cả bài, làm một bài tập …, rồi tự kiểm tra và giao bài tập."; 1-04: "Mạch 2 cho … Mạch 3 giữ … Mạch 4 là … Mạch 5 bỏ … Mạch 6 áp dụng …" | 1-06: bỏ vế "không phải …" (ghi chú dòng 24 không có); 7-00: nêu nội dung, ví dụ "Các cận của bài cần (C), (G1), (G2) và các lần rút độc lập; Bài tập 05.5(d) ghép cận kì vọng với bất đẳng thức Markov."; 1-04: chấp nhận được trên trang nội dung, có thể gộp thành hai câu |
| nhẹ | 3-07 (L20) | Không nối với kỹ thuật một dòng gần nhất đã có | Mục 14: Bài 04, 6-02 "Lấy điều kiện theo tập huấn luyện rồi bỏ điều kiện" ghi "không dùng"; tính chất tháp đã dùng ở Bài 01 (Mệnh đề 01.23) | Một câu ở ghi chú diễn giả 3-07: cùng cơ chế lấy điều kiện rồi bỏ điều kiện của Bài 04, nay theo lịch sử các lần rút |
| nhẹ | 2-04, 2-06, 3-06, 6-01 (L21) | Trang chép khối ghi chú, công cụ không có trực quan trên mặt trang | Mục 5 ở trên; 2-06 có trực quan ("mỗi bước dài không quá $\eta G$") chỉ ở ghi chú diễn giả | 2-06: thêm "**Ý nghĩa:** theo (b), mỗi bước hạ gradient dài không quá $\eta G$." (khoảng 11, trang lên 59); 3-06: viết (a) thành "$w_t\in W$, là hàm của $\xi_1,\ldots,\xi_{t-1}$"; 6-01: điều kiện đo được sang ghi chú diễn giả chỉ khi điều phối viên chấp nhận (ghi chú giữ nó trong định nghĩa, nên mặc định giữ) |
| nhẹ | 3-05, F3 (L22) | Khung phóng to ghi "có thể" trong khi bốn điểm $w_4$, điểm GD và $w^*$ nằm trong một ô cỡ $0{,}25$ | Mục 8: "Cụm điểm quanh $w_3$ có thể phóng to trong một khung nhỏ"; toạ độ V7 | Khung phóng to bắt buộc, nhãn số chỉ trong khung |

## 7. Ý kiến về các điểm của mục 11 (điều phối viên quyết định)

1. **05.5(b) thay 05.5(a) ở 6-06:** đồng ý; (b) dùng cả $\sigma^2=15$ của 6-05. Đồng ý đề xuất sửa `exercises.md` (bỏ "giá trị giả định").
2. **55 trang:** giữ 55. Không phương án nào trong (a)–(c) tốt hơn; các sửa ở trên không thêm trang.
3. **Không có trang ý tưởng chứng minh cho công cụ:** đồng ý, cùng chính sách Bài 02–04. Bổ đề 05.8 được dùng ở Bước 1 của 4-02, nên lộ trình phác thảo ở ghi chú diễn giả 3-02 là đủ.
4. **Định nghĩa 05.6 chỉ ở ghi chú diễn giả:** đồng ý; không trang nào dùng trên mặt trang.
5. **Thứ tự trong §6:** đồng ý (cùng mục), ghi vào `review-log.md`; L4 làm cho 3-04 mở bằng giới hạn chi phí.
6. **Câu hỏi cuối buổi thành trang ví dụ 6-07:** đồng ý dạng "Ví dụ: …" và vị trí sau mọi trang dùng Hệ quả 05.15(b). Về ánh xạ mạch (T13), nghiêng về đặt trang này đầu mạch 7 (trước 7-01 hoặc ngay trước 7-02): mạch 6 thành §9–§10, mạch 7 thành §11–§14, và dòng cuối của 7-02 ("Đại lượng được chặn: $\operatorname{opt}_S$, không phải $L_D$") có số liệu ngay trước nó. Nếu giữ ở mạch 6 thì ghi độ lệch "mạch 6 gồm §13" vào `review-log.md`.
7. **Khối ứng dụng §3 vào 1-06:** đồng ý.
8. **Mục tiêu 1-03:** đồng ý rút câu chữ, trừ hai chỗ mất phạm vi (L13).
9. **7-03 68 âm tiết:** đồng ý ngoại lệ (dưới 90). Bài tập 05.4(b) không thay được vì chỉ dùng mạch 4.
10. **Điểm toán #3:** đồng ý (mục 3 ở trên).
11. **Đo ở 390 px:** đồng ý; thêm 6-02 (công thức xác suất với điều kiện $T$ dài) và hàng đầu bảng 7-01.
12. **Trang sát trần:** đồng ý; sau T4, T5, T6, T8, L14, L21 điều phối viên đếm lại 3-03, 3-06, 4-03, 6-02, 6-04, 7-04, 1-06, 2-06.
13. **Ghi chú diễn giả dẫn bài sau:** đồng ý (chỉ trong ghi chú diễn giả; đã kiểm ghi chú Bài 06, 08, 10 có dùng "lịch sử", "tổng triệt tiêu", Định lý 05.14, Mệnh đề 05.13, "hối tiếc").
14. **Liên kết hai chiều:** đồng ý.
15. **"Tiến bộ", "nhiễu bước":** đồng ý; nhãn "nhiễu" của F4 trái điểm này (L11).
16. **Dẫn UML §14.2 ở 2-03:** đồng ý.
17. **Câu chữ bài tập rút gọn:** đồng ý; giữ đủ ý (mục 4), thêm L8, L15.

## 8. Liên tục (bảng kiểm Outline/Threads/Concept)

- **Thứ tự khái niệm:** đúng thứ tự §1–§10 của ghi chú, trừ hai đảo cục bộ đã nêu (Thuật toán 05.9 sau Định nghĩa 05.10, điểm 5; thẻ 05.13 trước 05.12, L7) và ánh xạ §13 (T13). Không trang nào dẫn kết quả của trang sau.
- **Định nghĩa trước khi dùng:** bảng mục 12 đúng, trừ $\pi$ (L2), $\operatorname{opt}_s$ ở dòng "Trực quan." 6-02 (T5) và "xáo trộn lại sau mỗi vòng" ở 7-05 (L12).
- **Thuật ngữ:** "điểm lặp trung bình", "độ chênh tối ưu", "sai số tối ưu thực nghiệm", "oracle gradient ngẫu nhiên", "kì vọng", "lôgarit", "véc-tơ" thống nhất với ghi chú và `thuat-ngu.md`; tiếng Anh ở lần đầu đúng bảng mục 10.
- **Kí hiệu:** $\eta$ không chỉ số, $\delta'$ khác $\delta$, $s$/$S$ theo đúng ghi chú (Hệ quả 05.19 viết $s$); $\sigma^2$ của lô khác $\sigma^2(x)$ Bài 04 (ghi chú diễn giả).
- **Mạch mở và đóng:** câu hỏi trung tâm của 1-05 được 7-02 trả lời theo $T$ (cận $RG/\sqrt T$, số vòng lặp, giá $1/\delta'^2$); câu hỏi thực hành của 1-06 được 4-09 trả lời; "một bước SGD có thể làm $L_S$ tăng" (1-06, 3-05) được 4-01, 4-03, 7-05 câu 1 khép lại.
- **Kỹ thuật:** hai trang "Kỹ thuật." mới (3-07, 4-05) chưa có ở Bài 01–04 (mục 14 của storyboard Bài 04 và grep các storyboard trước); tên đúng; L20 về nối với kỹ thuật một dòng của Bài 04.

## 9. Đề xuất sửa ghi chú

Không có đề xuất mới. Đồng ý ba đề xuất ở mục 13 của storyboard; về điểm #3, ghi chú §11 (dòng 1204) đã đọc theo điểm lặp trung bình, nên sửa câu dòng 1030 theo đề xuất của người kiểm chỉ làm Ví dụ 05.12 khớp §11.
