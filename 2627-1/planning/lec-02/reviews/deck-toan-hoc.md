# Duyệt deck Bài 02 — Vai 2 `toan-hoc` (độ chính xác toán học, thống nhất với ghi chú)

Bản duyệt: `2627-1/lecture-02-bat-dang-thuc-tap-trung.html` (55 trang, bản đóng băng), năm SVG trong `2627-1/img/lec-02/`. Đối chiếu: `materials/lec-02/lecture-note.md`, `exercises.md`, `materials/lec-01/lecture-note.md` (dữ liệu $S_\eta$, $D_f$), deck Bài 01 (trang "Kỹ thuật." của bất đẳng thức hợp và xác suất bỏ sót), quyết định "Bộ trang chiếu" trong `review-log.md`.

Cách kiểm: đọc mã HTML (mặt trang và ghi chú diễn giả) và mã SVG; tính lại bằng Python (`math`, tổng nhị thức chính xác) mọi con số trên mặt trang, trong ghi chú diễn giả, trong nhãn và tọa độ SVG. Kịch bản: thư mục nháp `…/scratchpad/lec-02/rv-toan-hoc/check.py`, `svg.py`. Không chụp ảnh màn hình (ngoài phạm vi vai; điều phối viên đã chạy `deck_check.py`).

## 1. Kết quả tính lại

**Mọi con số đều khớp** (sai khác chỉ ở chữ số làm tròn cuối). Các nhóm đã kiểm:

- Ví dụ 02.1: bảng $L_{D_\eta}(h_t)=0{,}52;0{,}32;0{,}22;0{,}32;0{,}28;0{,}48$; $S_\eta$ trùng Bài 01 (dòng 160), $L_{S_\eta}(h_3)=\tfrac13$; bảng hiệu $-0{,}02;0{,}0133;0{,}1133;0{,}18;0{,}0533;0{,}02$.
- Xác suất đuôi: hai phía $0{,}61889$, $0{,}021148$, $8{,}941\cdot10^{-4}$; đuôi trên $0{,}39369$, $0{,}013362$, $6{,}926\cdot10^{-4}$; $\Pr(\mathrm{Bin}(100;0{,}22)\ge22)=0{,}5391$.
- Markov $0{,}6875$; Chebyshev $17{,}16/m$ và $25/m$; Hoeffding $2e^{-2}=0{,}27067$, $2e^{-4}=0{,}03663$; ngưỡng $m\le107$ ($0{,}23364<0{,}23531$; $0{,}23148>0{,}23065$); tỉ số $8{,}13$; $11{,}85$; $12{,}80$.
- Bổ đề Hoeffding, $\tau=2$: $1{,}54929\le e^{0{,}5}=1{,}64872$.
- Ví dụ 02.5: $0{,}042947$, $[0{,}00705;0{,}09295]$, $0{,}038702$, $0{,}0887$. Cỡ mẫu $500$; $184{,}44\to185$; $25\,000$; $380{,}05\to381$.
- Ví dụ 02.6 và Nhận xét 02.11: $2e^{-8}=6{,}71\cdot10^{-4}$; $(1-10^{-4})^{100}=0{,}99005$; $2e^{-2/m^3}$.
- Ví dụ 02.7: $\Pr(\mathrm{Bin}(1000;0{,}07)\le50)=0{,}0059296$; $1-(1-p)^{1000}=0{,}99739$.
- Bài tập 02.4: $2e^{-3{,}2}=0{,}08152$; $22/1024=0{,}02148$; $0{,}62358$; $0{,}99244$; $81{,}52$; ngưỡng $K=88$ (ghi chú diễn giả 5-07).
- $r_m^{+}$ với $m=1000$, $\delta=0{,}05$: $0{,}03870$; $0{,}05147$; $0{,}06165$; $0{,}07037$; $0{,}07587$; cận trên $0{,}1204$, $0{,}1259$.
- Hệ quả 02.16: $1096{,}13\to1097$; $2r_6=1{,}3516$; Ví dụ 02.10: $1430{,}92\to1431$; $A_{\min}$ trên $S_\eta$ trả về $h_2$ (tập ERM $\{h_2,h_3,h_5\}$), rủi ro vượt mức $0{,}10$.
- Trường hợp khả diễn: $47{,}87\to48$; $36{,}89\to37$; $29{,}96\to30$; $0{,}8^{13}=0{,}05498$, $0{,}8^{14}=0{,}04398$.
- Bảng Ví dụ 02.12 (cả 14 ô) và năm điểm mỗi đường của `hai-toc-do.svg` ($39;77;153;381;761$ và $415;1659;6636;41\,471;165\,881$).
- Bài tập 02.8: $139{,}82\to140$; $2935{,}0039\to2936$; $279{,}64\to280$; $11\,740{,}02\to11\,741$. Chebyshev $K/(4\delta\epsilon^2)=2\,000\,000$.
- Bài tập 02.11: $17\,538{,}04\to17\,539$; kiểm tra $0{,}0999973\le0{,}1$. Bài tập 02.3: $1522{,}17\to1523$. Bài tập 02.1(f): $2000$, $738$. Câu hỏi cuối buổi: $0{,}045536$, $0{,}1255$.

**SVG** (tọa độ tính lại từ dữ liệu):

- `tap-trung.svg`: mọi cột đúng vị trí $102+451\,k/m$ và chiều cao theo hàm xác suất nhị thức (thang $262{,}5$, $1050$, $1312{,}5$ px trên đơn vị); màu và gạch chéo đúng biến cố $\lvert k/m-0{,}22\rvert\ge0{,}1$, kể cả các cột biên $k=12,32$ ($m=100$) và $k=24,64$ ($m=200$); dải $0{,}12$–$0{,}32$ đúng tọa độ.
- `markov.svg`: đường chéo, hàm bậc thang, chấm đặc tại $(\alpha,\alpha)$, chấm rỗng tại $(\alpha,0)$, hai miền gạch chéo đúng.
- `day-cung.svg`: đường cong $e^{2w}$ trên $[-0{,}22;0{,}78]$, hai đầu mút $0{,}644$ và $4{,}759$, dây cung tại $w=0$ cao $1{,}549$, vạch $1{,}649$: đúng thang $412{,}5$ px/đơn vị ngang và $64$ px/đơn vị dọc.
- `ban-kinh-theo-K.svg`, `hai-toc-do.svg`: mọi điểm lệch dưới $0{,}1$ px so với giá trị tính lại.

**Ý tưởng chứng minh:** các bước của 2-05, 3-03, 3-05, 4-03, 5-04, 5-10, 6-03 đúng thứ tự của chứng minh trong ghi chú; bất đẳng thức then chốt đúng tên (Markov, dây cung và Taylor, Chernoff, bổ đề Hoeffding, bất đẳng thức hợp); giả thiết vào đúng bước. Phản ví dụ (bản sao một quan sát, biến $m^2$ với xác suất $1/m^2$, Bài tập 02.4, Bài tập 02.1(e) ở ghi chú diễn giả) đúng.

## 2. Bảng thống nhất trang → khối ghi chú

| Trang | Khối ghi chú | Kí hiệu, giả thiết, số hiệu, dữ liệu | Lệch |
|---|---|---|---|
| 1-01 | đoạn mở đầu, Định lý 02.14 | khớp | — |
| 1-02 | Kiến thức tiên quyết, §2 | khớp | "$\epsilon$ độ chính xác" (P11) |
| 1-03 | Mục tiêu học tập (6 mục) | khớp thứ tự | — |
| 1-04, 1-05 | đoạn mở đầu | khớp | ghi chú diễn giả 1-05 (P13) |
| 1-06 | Câu hỏi mở đầu; ứng dụng §3 | khớp ($m=1000$, $5\%$, $1000$ ứng viên) | — |
| 2-01 | §1 mục 6; §2 (T1)–(T4), (O1) | khớp | lượng từ (T2)/(T3) (P10) |
| 2-02 | Ví dụ 02.1; §4 đoạn đầu | khớp dữ liệu, $\mathrm{Bin}(m;0{,}22)$ | — |
| 2-03 | Định nghĩa 02.1, Ví dụ 02.2, Phụ lục B.1 | khớp số | đuôi dưới chưa nêu (P9) |
| 2-04 | Bổ đề 02.2, 02.3 | khớp hằng số, $\bar\mu_m=\mathbb E\bar V_m=\frac1m\sum\mu_i$ | "với mọi $i$" (P10) |
| 2-05 | chứng minh Bổ đề 02.2, 02.3; Bài tập 02.1(a) | khớp | — |
| 2-06 | Ví dụ 02.3 | khớp toàn bảng | — |
| 3-01 | Định nghĩa 02.4, Bổ đề 02.5 | hằng số đúng | gộp (a), (b) (P5) |
| 3-02 | Bổ đề 02.6 | khớp; ví dụ $\tau=2$ mới, đúng (N1 của storyboard) | — |
| 3-03 | chứng minh Bổ đề 02.6, Phụ lục A | khớp | — |
| 3-04 | Định lý 02.7, Nhận xét 02.8, Ví dụ 02.4 Bước 1–3, đoạn $\ell_c$ | khớp | — |
| 3-05 | chứng minh Định lý 02.7 | khớp | — |
| 4-01 | Định nghĩa 02.9 và hai đoạn sau | khớp, $0{,}539$ | khoảng tin cậy (P8) |
| 4-02 | Hệ quả 02.10 | khớp bốn phần, hằng số, "mọi $D$" | — |
| 4-03 | chứng minh Hệ quả 02.10 | khớp | — |
| 4-04 | chứng minh Hệ quả 02.10 Bước 3–5; Ví dụ 02.4 Bước 4 | khớp | — |
| 4-05 | Ví dụ 02.5 | khớp | — |
| 4-06 | Ví dụ 02.6, Nhận xét 02.11 | khớp ($M=m^2$) | (P7) |
| 5-01 | Ví dụ 02.7, Phụ lục B.2 | khớp | — |
| 5-02 | Định nghĩa 02.13 và bảng sau | khớp | — |
| 5-03 | Định lý 02.14 và đoạn sau | khớp ba phần | — |
| 5-04 | chứng minh Định lý 02.14; Bổ đề 02.12 | khớp | (P6) |
| 5-05 | chứng minh Định lý 02.14 Bước 3–4; §9 | khớp | — |
| 5-06, 5-07 | Bài tập 02.4 và lời giải | khớp dữ liệu và kết quả | — |
| 5-08 | Ví dụ 02.8, Nhận xét 02.15 | khớp | "khoảng $0{,}005$" (đã ghi ở review-log) |
| 5-09 | Hệ quả 02.16, Ví dụ 02.9, 02.10 | khớp hằng số, "đồng thời cho mọi nghiệm ERM" | ví dụ thiếu xác suất (P1) |
| 5-10, 5-11 | chứng minh Hệ quả 02.16 | khớp | — |
| 5-12 | Bài tập 02.3(a) | nguyên văn câu hỏi | — |
| 6-01 | §8 đoạn đầu; chứng minh Mệnh đề 02.17 Bước 1; Ví dụ 02.11 Bước 4 | khớp | thiếu "hàm lỗi 0–1" (P12) |
| 6-02 | Mệnh đề 02.17 | khớp sáu giả thiết, ba phần | — |
| 6-03 | chứng minh Mệnh đề 02.17 | khớp | — |
| 6-04 | Ví dụ 02.11 | khớp bốn số và phạm vi | — |
| 6-05 | Ví dụ 02.12, Phụ lục B.3 | khớp 14 ô | — |
| 6-06 | Nhận xét 02.18; §12 | khớp | thiếu "hàm lỗi 0–1" (P12) |
| 6-07 | Bài tập 02.8(c)(d) | khớp số | — |
| 6-08 | §9 | khớp | — |
| 7-01 | §4–§9 | khớp | Chebyshev "độc lập" (P4) |
| 7-02 | đoạn mở đầu, §9 | khớp số | thiếu loại bảo đảm (P2) |
| 7-03 | Bài tập 02.11 | khớp kết quả | (P3) |
| 7-04 | §11 | khớp lời giải | — |
| 7-05 | §10 | khớp 11 bài | — |
| 7-06 | §12 | khớp mục UML, tên Bài 03 | — |

Thứ tự khái niệm theo thứ tự mục của ghi chú (§1–§2 → 2-01; §4 → mạch 2; §5 → mạch 3–4; §6–§7 → mạch 5; §8–§9 → mạch 6). Số hiệu kết quả trên mặt trang đúng khối ghi chú cùng số và nội dung. Bất đẳng thức hợp và xác suất bỏ sót có trang "Kỹ thuật." ở deck Bài 01 (dòng 384, 744), nên "Nhắc lại:" ở 5-04 và 6-01 hợp lệ.

## 3. Phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L02-5-09 (P1) | Ví dụ bỏ loại bảo đảm và điều kiện cỡ mẫu: cận $0{,}32$ đọc như khẳng định tất định | "$M=\lceil1096{,}1\rceil=1097$; $L_{D_\eta}(\hat h)\le0{,}32$." — ghi chú Ví dụ 02.9 Bước 1: "với ít nhất $1097$ quan sát, mọi nghiệm ERM có $L_{D_\eta}(\hat h)\le0{,}22+0{,}1=0{,}32$ với xác suất ít nhất $0{,}95$" | "$M=1097$: khi $m\ge1097$, với xác suất ít nhất $0{,}95$, mọi nghiệm ERM có $L_{D_\eta}(\hat h)\le0{,}32$." |
| trung bình | L02-7-02 (P2) | Gạch đầu dòng 3 và 4 bỏ "với xác suất ít nhất $1-\delta$"; gạch 4 không nói bảo đảm cho đại lượng nào | "Mọi nghiệm ERM có rủi ro vượt mức không quá $\epsilon$ khi $m\ge2\ln(2K/\delta)/\epsilon^2$." ; "Khả diễn: $m\ge\ln(K/\delta)/\epsilon$, …" — ghi chú Hệ quả 02.16(a),(c), Mệnh đề 02.17(c): "với xác suất ít nhất $1-\delta$" | Gạch 3: "… không quá $\epsilon$ với xác suất ít nhất $1-\delta$ khi …". Gạch 4: "Khả diễn: $m\ge\ln(K/\delta)/\epsilon$ cho mọi nghiệm ERM $L_D(\hat h)\le\epsilon$ với xác suất ít nhất $1-\delta$; tăng như …" (nếu vượt trần, rút cụm "tăng như …" vì đã ở 6-06) |
| nhẹ | L02-7-03 (P3) | Phần (a) bỏ giả thiết của bài tập; phép tính hiển thị không khớp số lôgarit làm tròn | "Phần (a): với $a\le\ell\le b$, …"; "$\ln240\approx5{,}4806$: $2\cdot16\cdot5{,}4806/0{,}01\approx17\,538{,}04$" — `exercises.md` Bài tập 02.11: "(T1), (T4), (T2) với $a\le\ell(h,z)\le b$ …, trong đó $0\le a<b$"; $2\cdot16\cdot5{,}4806/0{,}01=17\,537{,}92$, còn $17\,538{,}04$ ứng với $\ln240=5{,}480639$ | "Phần (a): (T1), (T4), $0\le a\le\ell\le b$, …"; giữ số theo `exercises.md` (xem Đề xuất 1) |
| nhẹ | L02-7-01 (P4) | Cột "Giả thiết không được bỏ" ghi "độc lập" cho Chebyshev, trong khi 2-05 nói chỉ cần không tương quan từng đôi | "Markov, Chebyshev … $V\ge0$; độc lập"; 2-05: "chỉ cần các $V_i$ không tương quan từng đôi"; ghi chú chứng minh Bổ đề 02.3 Bước 2 | "$V\ge0$; không tương quan từng đôi (Chebyshev (b))" |
| nhẹ | L02-3-01 (P5) | Phát biểu gộp hai phần của Bổ đề 02.5: giả thiết độc lập đặt cho cả cận Markov hàm mũ, mất ý (a) đúng cho mọi $V$ và (b) đúng với mọi $\tau\in\mathbb R$ | "**Giả thiết:** $\alpha\in\mathbb R$, $\tau>0$; $V=\sum_{i=1}^mV_i$ với $V_i$ độc lập." — ghi chú Bổ đề 02.5: "(a) $V$ là một biến ngẫu nhiên bất kì"; "(b) Với mọi $\tau\in\mathbb R$" | Tách nhãn trong công thức: "(a) mọi $V$, $\tau>0$: $\Pr(V\ge\alpha)\le e^{-\tau\alpha}\mathbb Ee^{\tau V}$; (b) $V_i$ độc lập: $\mathbb Ee^{\tau V}=\prod_i\mathbb Ee^{\tau V_i}$" |
| nhẹ | L02-5-04 (P6) | "biến cố hỏng" chưa được định nghĩa trên mặt trang; "vế phải gấp $K$ lần" mơ hồ vì công thức có hai vế phải | "biến cố hỏng nằm trong $\bigcup_hB_h$"; "khi mọi $B_h$ trùng nhau, vế phải gấp $K$ lần xác suất của hợp" — ghi chú Bổ đề 02.12: "khi $B_1=\cdots=B_K$, vế phải bằng $K$ lần vế trái" (vế phải là $\sum\Pr(B_h)$, không phải $2Ke^{-2mr^2}$) | "$\{S$ không là $r$-đại diện$\}\subseteq\bigcup_hB_h$"; "khi mọi $B_h$ trùng nhau, $\sum_h\Pr(B_h)$ gấp $K$ lần xác suất của hợp" |
| nhẹ | L02-4-06 (P7) | Cột trái không nói số $6{,}7\cdot10^{-4}$ là áp dụng sai; "Lưu ý:" bỏ miền $\epsilon$ và "khi $m\to\infty$" của ghi chú | "Hoeffding, $m=100$: $2e^{-8}\approx6{,}7\cdot10^{-4}$"; "không có $g(m,\epsilon)\to0$ …" — ghi chú Ví dụ 02.6 Bước 4 "áp dụng sai Định lý 02.7"; Nhận xét 02.11 "với mọi $\epsilon\in(0,1]$ … tiến về $0$ khi $m\to\infty$" | "Hoeffding (áp dụng sai): …"; "không có $g(m,\epsilon)\to0$ khi $m\to\infty$, $\epsilon\in(0,1]$, chặn …" |
| nhẹ | L02-4-01 (P8) | Khoảng tin cậy viết là "thêm cận dưới", có thể đọc thành hai bảo đảm riêng ở mức $1-\delta$ | "Khoảng tin cậy (confidence interval): thêm cận dưới $\underline L_\delta(S)\le L_D(h)$." — ghi chú Định nghĩa 02.9: $\Pr[\underline L_\delta(S)\le L_D(h)\le\overline L_\delta(S)]\ge1-\delta$ | "Khoảng tin cậy: $\Pr[\underline L_\delta(S)\le L_D(h)\le\overline L_\delta(S)]\ge1-\delta$ với mọi $D$." |
| nhẹ | L02-2-03 (P9) | Đuôi dưới không có trên mặt trang, nhưng 3-04 ("mỗi đuôi một phía") và 4-03 ("đuôi dưới cho (c)") dùng | "Xác suất đuôi … hai phía …, đuôi trên …" — ghi chú Định nghĩa 02.1 có ba dạng | Thêm "đuôi dưới $\Pr(V-\mathbb EV\le-\epsilon)$" hoặc "Nhắc lại:" một dòng ở 3-04 |
| nhẹ | L02-2-01, L02-2-04 (P10) | Lượng từ rút gọn: (T2)/(T3) thiếu "với mọi $h\in\mathcal H$, $z\in\mathcal Z$"; Bổ đề 02.3(b) thiếu "với mọi $i$" | "$\ell(h,\cdot)\ge0$ đo được; $\ell(h,z)\in[0,1]$"; "$\operatorname{Var}V_i\le\sigma^2$" — ghi chú §2 (T3), Bổ đề 02.3(b) | Thêm "$\forall h,z$" và "$\forall i$" |
| nhẹ | L02-1-02 (P11) | $\epsilon$ được gọi chung là "độ chính xác", trong khi ghi chú §2 cho ba nghĩa theo mục | "$\epsilon$ độ chính xác" — ghi chú §2: "độ lệch … ở §4–§6; mức rủi ro vượt mức ở §7; mức rủi ro ở §8" | "$\epsilon$ độ lệch hoặc độ chính xác, nghĩa nêu khi dùng" (6-05 đã có "Lưu ý:" ba nghĩa) |
| nhẹ | L02-6-01, L02-6-06 (P12) | Hai đẳng thức chỉ đúng với hàm lỗi 0–1 nhưng mặt trang không ghi | 6-01: "$\Pr(L_S(h)=0)=(1-L_D(h))^m$"; 6-06: "$\operatorname{Var}L_S(h)=L_D(h)(1-L_D(h))/m$" — ghi chú Mệnh đề 02.17 "hàm lỗi 0–1", Nhận xét 02.18 "với hàm lỗi 0–1" | Thêm "hàm lỗi 0–1" vào câu dẫn của mỗi trang |
| nhẹ | L02-1-05 ghi chú diễn giả (P13) | Hai gạch cuối bỏ "với xác suất ít nhất $1-\delta$" | "mọi nghiệm ERM có rủi ro vượt mức không quá $\epsilon$ khi …"; "Khi lớp giả thuyết khả diễn, $m\ge\ln(K/\delta)/\epsilon$ đủ." | Thêm loại bảo đảm như P2 |
| nhẹ | `tap-trung.svg`, khung $m=6$ (P14) | Cột rộng $36$ px của $k=2$ ($k/m=0{,}333$) phủ qua vạch $0{,}32$ vào nền dải; dễ đọc thành "nửa trong dải" dù cột gạch chéo đúng | rect x=234,33 đến 270,33, vạch dải x=246,3 | Thu hẹp cột khung $m=6$ (chẳng hạn $20$ px) để mỗi cột nằm trọn một phía vạch |

Không có phát hiện chặn bàn giao hay nghiêm trọng: không có hằng số, lượng từ, một phía/hai phía hay số liệu nào sai; các lệch đều là rút gọn bỏ điều kiện hoặc loại bảo đảm.

## 4. Đề xuất sửa ghi chú (và tệp bài tập)

1. **`exercises.md`, lời giải Bài tập 02.11(b) Bước 2–3 (nhẹ).** Với $\ln240\approx5{,}4806$ hiển thị, $2\cdot16\cdot5{,}4806/0{,}01=17\,537{,}92$, không phải $17\,538{,}04$; số $17\,538{,}04$ đúng với $\ln240=5{,}48064$. Đề xuất ghi $\ln240\approx5{,}48064$ (kết quả $17\,539$ không đổi). Tương tự "$17\,538{,}04=16\cdot1096{,}13$" nên là "$\approx$". Deck 7-03 giữ số của tệp bài tập.
2. Ví dụ 02.8 "khoảng $0{,}005$" (giá trị $0{,}0055$): đã có trong `review-log.md`, không lặp.

## Kết luận

**đạt khi sửa** — 0 chặn bàn giao, 0 nghiêm trọng, 2 trung bình (5-09, 7-02: thiếu loại bảo đảm xác suất cao), 12 nhẹ.
