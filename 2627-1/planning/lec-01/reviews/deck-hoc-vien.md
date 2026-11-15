# Duyệt deck Bài 01 — vai học viên cao học (`hoc-vien`)

Ngày: 2026-11-15. Bản đóng băng: `2627-1/lecture-01-mo-hinh-hoc.html` (55 trang). Chỉ đọc; không sửa deck, SVG, storyboard, ghi chú.

## Cách làm

- Đọc deck như người nghe lần đầu, đã đọc trước ghi chú (`materials/lec-01/lecture-note.md`). Đối chiếu storyboard (mục 14, ngoại lệ mật độ) và quyết định cuối `review-log.md`, mục "Bộ trang chiếu".
- Chạy `deck_check.py --shots` vào thư mục nháp của vai (`…/scratchpad/lec-01/rv-hoc-vien/`): slides=55, console=0, pageerrors=0, failed=0, `.katex-error`=0, overflow=0 mọi trang, narrowWide=0. Đã xem ảnh 1600×900 của cả 55 trang (bảng ghép) và ảnh 390×844 của một số trang dày (7-01, 5-08, 6-05, 2-03).
- Đếm mật độ: số máy cho mọi trang; đếm lại bằng tay mọi trang ≥ 50 âm tiết (bảng cuối tệp).

## Bảng phát hiện

| mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| trung bình | L01-2-02 | $D_\eta$ và $D_f$ xuất hiện trên mặt trang mà chưa được định nghĩa. Người học phải tự đoán rằng $D_\eta$ là phân bố có $D_{\mathcal X}$ đều và nhãn 1 với xác suất $\eta(x)$. Hai phân bố này dùng suốt deck. | "Dữ liệu có nhiễu từ $D_\eta$: $S_\eta=…$"; "Dữ liệu tất định từ $D_f$, $f=h_3$". Định nghĩa $D_\eta(y\mid x)=\eta(x)^y(1-\eta(x))^{1-y}$ chỉ có trong ghi chú diễn giả. Ghi chú bài giảng, Ví dụ 01.1, nêu rõ hai phân bố. | Viết hai dòng cuối thành: "$D_\eta$: nhãn $1$ với xác suất $\eta(x)$; tập huấn luyện $S_\eta=…$" và "$D_f$: $y=f(x)$ chắc chắn, $f=h_3$; tập huấn luyện $S_f=…$". Mật độ hiện 21, còn dư chỗ. |
| trung bình | L01-2-04 | Câu hỏi "tính $L^c_{D_\eta}(h_2)$" không làm được chỉ từ mặt trang. Trang chỉ có công thức cho $L_{D_\eta}(h_t)$ dưới $\ell_{0\text{-}1}$, và $L^c_{D_\eta}(h_3)=0{,}37$ được cho mà không có phép tính. Lời giải "$0{,}2\,(4\cdot0+1{,}6)$" nhảy qua công thức có trọng số. | "Tại $t=3$: … $L^c_{D_\eta}(h_3)=0{,}37$"; "**Lời giải:** $0{,}2\,(4\cdot0+1{,}6)=0{,}32$". Dạng $0{,}2[c_{FN}\sum_{x<t}\eta+c_{FP}\sum_{x\ge t}(1-\eta)]$ chỉ có trong ghi chú diễn giả. | Thêm một dòng "Dưới $\ell_c$: nhân tổng thứ nhất với $c_{FN}=4$, tổng thứ hai với $c_{FP}=1$", hoặc viết $L^c_{D_\eta}(h_3)=0{,}2\,(4\cdot0{,}25+0{,}85)=0{,}37$ ngay trên trang (mật độ 27, còn dư chỗ). |
| trung bình | L01-5-11 | Câu định nghĩa vòng vo, khó hiểu tại chỗ. Một dòng gói hai khái niệm và chỉ vào "vế trái", "ngoặc đầu" của một công thức chưa đọc. | "Rủi ro vượt mức (excess risk) của $h$: so với rủi ro Bayes ở vế trái, so với $\mathcal H$ ở ngoặc đầu." Ghi chú, Định nghĩa 01.24, viết hai gạch đầu dòng rõ ràng. | "Rủi ro vượt mức (excess risk) của $h$ so với $\mathcal H$: $L_D(h)-\inf_{h'\in\mathcal H}L_D(h')$; so với rủi ro Bayes: $L_D(h)-L_D^{\mathrm{Bayes}}$. Hai đại lượng liên hệ qua:" rồi đến công thức hiển thị. |
| trung bình | L01-6-01 | Câu định nghĩa thiếu động từ chính, nên người học không biết $\beta$ phải thỏa điều gì. Điều kiện "hàm lỗi 0–1, $\mathcal Y=\{0,1\}$" của Định nghĩa 01.28 không có trên mặt trang. Người học chỉ suy ra được điều kiện này từ dòng sau ("vì $L_D\le1$ với $\ell_{0\text{-}1}$"). | "Cận tổng quát hóa cho mọi thuật toán ERM trên $\mathcal H$: $\beta(m,\delta)$ với mọi ERM $\hat A$, mọi $D$, $m$, $\delta$," (ghi chú, Định nghĩa 01.28: "Cho … hàm lỗi 0–1 … Một hàm $\beta$ … được gọi là … nếu"). | "Với $\ell_{0\text{-}1}$, hàm $\beta(m,\delta)$ là cận tổng quát hóa cho mọi thuật toán ERM trên $\mathcal H$ nếu với mọi thuật toán ERM $\hat A$, mọi $D$, $m$, $\delta$:" |
| trung bình | toàn deck (390×844) | Ở 390×844, RevealJS thu cả trang 1280×720 về bề rộng ≈ 380 px (tỉ lệ ≈ 0,3), không cuộn. Chữ thân ≈ 8–9 px, chỉ số KaTeX nhỏ hơn: khó đọc nếu không phóng to. Không tràn, không chồng, nên máy không báo. | Ảnh `narrow-049-L01-7-01.png`, `narrow-035-L01-5-08.png`, `narrow-009-L01-2-03.png`; cấu hình `scrollActivationWidth:null`. Lỗi đến từ khung kỹ thuật chung (CSS và cấu hình lấy từ rl-plan), không riêng deck này. | Điều phối viên quyết định ở mức học phần: bật chế độ cuộn của RevealJS ở màn hẹp, hoặc chấp nhận và ghi vào `review-log.md` rằng màn hẹp cần xoay ngang hay phóng to. |
| nhẹ | L01-1-02 | Trang quy ước dùng $D$, $h$, $X$, $Y$, $\mathcal X$, $\mathcal Y$ trước khi đặt tên: (T1) nói "theo $D$" và $\eta$ dùng $X$, $Y$, nhưng chưa nói $D$ là phân bố dữ liệu hay $\mathcal X$, $\mathcal Y$ là tập đầu vào và tập nhãn. Trang 2-01 mới nêu các đối tượng này. | "(T1) … theo $D$."; "$\eta(x)=\Pr(Y=1\mid X=x)$"; "$z=(x,y)\in\mathcal Z=\mathcal X\times\mathcal Y$". | Viết thêm vài chữ trong dòng "Ký hiệu:": "$\mathcal X$ tập đầu vào, $\mathcal Y$ tập nhãn; $(X,Y)\sim D$ phân bố dữ liệu". Hoặc ghi rõ trong ghi chú diễn giả rằng 2-01 định nghĩa đầy đủ. |
| nhẹ | L01-1-06 | Mặt trang dùng hàm chỉ báo $\mathbb 1[\cdot]$ lần đầu mà không có tên tiếng Việt và tiếng Anh. Tên "hàm chỉ báo (indicator)" chỉ có trong ghi chú diễn giả. | "$h_3(x)=\mathbb 1[x\ge3]$". Ghi chú bài giảng, Câu hỏi mở đầu, gọi tên ngay tại chỗ. | Thêm "$\mathbb 1[\cdot]$: hàm chỉ báo (indicator)" vào dòng "Nhắc lại:" của 1-02, hoặc thêm cụm ngắn trên 1-06. |
| nhẹ | L01-3-04 | Cụm "$\ne\emptyset$, với mọi $S$" đọc như một khẳng định, trong khi đây là điều kiện để thuật toán ERM được định nghĩa. Ghi chú diễn giả có ví dụ tập nghiệm rỗng, nên người học dễ hiểu sai. | "Thuật toán ERM trả về một phần tử của tập nghiệm ERM $\arg\min_{h\in\mathcal H}L_S(h)\ne\emptyset$, với mọi $S$." | "Khi $\arg\min_{h\in\mathcal H}L_S(h)\ne\emptyset$ với mọi $S$, thuật toán ERM trả về một phần tử của tập nghiệm ERM." |
| nhẹ | L01-3-05 | Hàng "$\hat t$ của $A_{\max}$" ($6,6,3,4,5$) không có lời giải thích trên mặt trang hay trong ghi chú diễn giả của trang này. Quy tắc $\hat t=\min\{x_i:y_i=1\}$ (hoặc $6$) chỉ có trong ghi chú diễn giả của 3-04. | Bảng của 3-05; ghi chú diễn giả 3-05 không nói vì sao $X_1=1$ cho $\hat t=6$. | Thêm vào ghi chú diễn giả: "Với một quan sát, $A_{\max}$ chọn $\hat t=X_1$ khi $Y_1=1$, và $\hat t=6$ khi $Y_1=0$." |
| nhẹ | L01-3-07 | Mặt trang không nói $E(t)$ là gì cho đến dòng lời giải "$L_S(h_t)=E(t)/7$". Nghĩa "số lỗi của $h_t$" chỉ có trong ghi chú diễn giả. | "Thuật toán 01.13: $c_y(x)=…$, $E(1)=\sum_xc_0(x)$, …" | "Thuật toán 01.13 tính số lỗi $E(t)$ của $h_t$: …" (thêm 5 âm tiết, trang hiện có 19). |
| nhẹ | L01-4-01 | (i) "σ-đại số" lần đầu trên mặt trang, không có "(σ-algebra)" và không được nhắc lại. (ii) Trang không nói thẳng $A_{\mathrm{gn}}(S)=\mathbb 1_F$ khi $Y=1$, nên dòng "$h_{\equiv1}$ và $\mathbb 1_F$ cùng khớp" chưa nối với thuật toán vừa định nghĩa. | "$\mathcal X=[0,1]$ với σ-đại số Borel"; "Trên mỗi $S$, $h_{\equiv1}$ và $\mathbb 1_F$ …". | (i) "σ-đại số (σ-algebra) Borel". (ii) "Trên mỗi $S$, $A_{\mathrm{gn}}(S)=\mathbb 1_F$ với $F=\{X_1,\ldots,X_m\}$; $h_{\equiv1}$ cũng khớp mọi quan sát." |
| nhẹ | L01-4-03 | Kí hiệu chữ thường $s$, $x_i$ xuất hiện cạnh chữ hoa $S$, $X_i$ mà không giải thích. Trên 4-01, $F=\{X_1,\ldots,X_m\}$; ở bước 3 lại là $\Pr(X=x_i)$. | "1. $A_{\mathrm{gn}}(s)=1$ trên một tập hữu hạn …"; "$\Pr(X\in F)\le\sum_{i=1}^m\Pr(X=x_i)=0$". | Thêm vào bước 1 "với mỗi tập huấn luyện cố định $s=((x_i,y_i))_{i\le m}$", hoặc dùng thống nhất $S$, $X_i$. |
| nhẹ | L01-4-03 → 4-04; L01-6-06 → 6-07 | Trang ý tưởng chứng minh dùng kỹ thuật trước trang "Kỹ thuật." định nghĩa nó: "bất đẳng thức hợp" ở 4-03 (bước 3), dạng chặn xác suất bỏ sót ở 6-06. Người nghe lần đầu gặp tên kỹ thuật trước khi thấy phát biểu. | 4-03: "bất đẳng thức hợp và giả thiết không có nguyên tử cho …"; trang 4-04 đứng sau. | Đặt trang "Kỹ thuật." trước trang ý tưởng chứng minh, hoặc thêm vào bước 3 một cụm ngắn "(xác suất của hợp không vượt tổng các xác suất)". |
| nhẹ | L01-5-01 | Dòng số "$0{,}999^{500}\approx0{,}61$" không gắn với $\epsilon$ trên mặt trang. Người học không biết con số này giải thích điều gì. Ý "$\epsilon$ cho phép bỏ qua vùng có khối lượng nhỏ" chỉ có trong ghi chú diễn giả. | "Nếu mức 3 chỉ chiếm $0{,}001$ dân số, $500$ quan sát bỏ sót nó với xác suất $0{,}999^{500}\approx0{,}61$." | Thêm vế "; sai ở mức đó chỉ tốn $0{,}001\le\epsilon$" (khoảng 5 âm tiết; trang 59, nên rút chữ ở dòng $\delta$). |
| nhẹ | L01-5-04 | Câu định nghĩa $m_A$ bị cắt thành hai đoạn `<p>` có khoảng cách giữa hai đoạn. Trên ảnh, "nhỏ nhất sao cho" đứng riêng rồi mới đến "bất đẳng thức học PAC …", nên câu trông như hai ý tách rời. | Ảnh `wide-031-L01-5-04.png`. | Gộp thành một đoạn, hoặc dùng `<br>`. |
| nhẹ | L01-5-07 | "Hàm Bayes" dùng ở dòng Ví dụ trước khi trang 5-08 định nghĩa "hàm phân lớp tối ưu Bayes". | "**Ví dụ.** Hàm Bayes là $\mathbb 1[x\in\{3,5\}]$". | "Chọn nhãn như vậy tại mỗi mức cho $\mathbb 1[x\in\{3,5\}]$, với rủi ro …". |
| nhẹ | L01-5-10 | "Ngưỡng" có hai nghĩa trên cùng trang: ngưỡng $t$ trên $x$ của hàm ngưỡng $h_t$ và ngưỡng trên $\eta(x)$. Câu hỏi "đặt ngưỡng báo dương tính ở đâu" không nói là ngưỡng nào. | "**Câu hỏi:** nên đặt ngưỡng báo dương tính ở đâu …"; "Ngưỡng $\tfrac{c_{FP}}{c_{FP}+c_{FN}}=\tfrac15$". | "Ngưỡng trên $\eta(x)$: $\tfrac{c_{FP}}{c_{FP}+c_{FN}}=\tfrac15$" (như 7-03 đã viết "ngưỡng trên $\eta(x)$"). |
| nhẹ | L01-6-01 | Nhãn "Trực quan." gắn cho câu trả lời của "Câu hỏi:", nên người đọc lẫn trực quan với lời đáp. | "**Trực quan.** Với cặp $(A_{\mathrm{gn}},D)$ của Mệnh đề 01.15, khoảng cách tổng quát hóa bằng $1$ trên mọi $S$, nên không có." | Bỏ nhãn (câu đáp đứng sau câu hỏi, dạng fragment), hoặc dùng "Gợi ý:". |
| nhẹ | L01-6-05 | (i) Dòng "Trực quan." dùng $t^\star$, $K$ trước dòng "Giả thiết:" định nghĩa chúng. (ii) "khối lượng" lần đầu trên mặt trang, không có "(probability mass)" (`thuat-ngu.md`: "lần đầu kèm tiếng Anh"). | "**Trực quan.** $A_{\max}$ chỉ sai ở các mức $t^\star,\ldots,\hat t-1$; … khối lượng lớn hơn $\epsilon$." | Đổi thứ tự (Giả thiết trước, hoặc Trực quan nói bằng lời "từ ngưỡng đúng đến ngưỡng chọn"); viết "khối lượng xác suất (probability mass)". |
| nhẹ | L01-6-06 | Bước 3 dùng ngầm $L_D(h_{\hat t})\le G(k)\le\epsilon$, tức tính "ngắn nhất" của $C$ cho khối $\{t^\star,\ldots,k-1\}$ có khối lượng $\le\epsilon$. Mặt trang không nêu điều này, nên người học vấp ở chỗ "và $L_D\le\epsilon$". | "3. Có quan sát trong $C$ thì $\hat t\le k$ và $L_D\le\epsilon$". | "… thì $\hat t\le k$, nên $L_D\le D_{\mathcal X}(\{t^\star,\ldots,k-1\})\le\epsilon$ ($C$ ngắn nhất)." |
| nhẹ | L01-6-07 | Dấu chấm cuối công thức xuống dòng riêng ở 1600×900. | Ảnh `wide-047-L01-6-07.png`: "$m\ge\ln(1/\delta)/\epsilon$" rồi "." ở dòng dưới. | Đưa dấu chấm vào trong `$…$` hoặc bỏ dấu chấm. |
| nhẹ | L01-7-01 | Hàng cuối của bảng chạm vùng chân trang ở 1600×900: đáy của $\lceil\ln(1/\delta)/\epsilon\rceil$ cách dòng chân trang khoảng 15 px. Không chồng chữ, nhưng sát. | Ảnh `wide-049-L01-7-01.png`. | Cho công thức cột 1 hàng cuối không ngắt dòng, hoặc bớt chữ hàng 01.23, để bảng thấp thêm một dòng. |
| nhẹ | L01-7-03 | "cùng tập từ" chưa được giải thích trên mặt trang. Cách biểu diễn thư bằng véc-tơ từ đã được chuyển sang ghi chú diễn giả, nên người học không biết $x$ là gì. | "Hai thư cùng tập từ có thể khác nhãn, …" (`exercises.md` dòng 14 mô tả $x\in\{0,1\}^p$). | Ở dòng dữ kiện, viết "$x$: tập từ có mặt trong thư" (khoảng 6 âm tiết; trang đang là ngoại lệ 73, nên bù bằng cách rút "Lọc thư rác (spam filtering):" thành "Thư rác (spam):"). |

## Mật độ

Số máy (`deck_check.py`, quy ước: token có chữ cái; số ngoài bảng như "01.15", "500" không tính) cho mọi trang:

| Trang | Âm tiết | Trang | Âm tiết | Trang | Âm tiết | Trang | Âm tiết |
|---|---|---|---|---|---|---|---|
| 1-01 | 60* | 2-05 | 47 | 4-03 | 56 | 5-08 | 48 |
| 1-02 | 60 | 3-00 | 43 | 4-04 | 40 | 5-09 | 47 |
| 1-03 | 80 (trần 80) | 3-01 | 20 | 4-05 | 49 | 5-10 | 44 |
| 1-04 | 39 | 3-02 | 54 | 4-06 | 60 | 5-11 | 35 |
| 1-05 | 25* | 3-03 | 49 | 5-00 | 43 | 5-12 | 59 |
| 1-06 | 51 | 3-04 | 52 | 5-01 | 59 | 6-00 | 39 |
| 2-00 | 43 | 3-05 | 43 | 5-02 | 54 | 6-01 | 49 |
| 2-01 | 57 | 3-06 | 57 | 5-03 | 50 | 6-02 | 60 |
| 2-02 | 21 | 3-07 | 19 | 5-04 | 54 | 6-03 | 51 |
| 2-03 | 60 | 4-00 | 40 | 5-05 | 40 | 6-04 | 52 |
| 2-04 | 27 | 4-01 | 47 | 5-06 | 59 | 6-05 | 51 |
| 6-06 | 39 | 6-07 | 34 | 7-00 | 18 | 7-01 | 65 (trần 80) |
| 7-02 | 53 | 7-03 | 73** | 7-04 | 60 | 7-05 | 45 |
| 7-06 | 58 | | | | | | |

\* Dòng vượt 20 âm tiết (bìa 39, hộp Vấn đề trung tâm 25): ngoại lệ đã ghi ở `storyboard.md` mục 14.
\** Vượt trần 60, dưới 1,5 lần trần: ngoại lệ đã ghi ở `storyboard.md` mục 14 (bài tập tổng hợp có lời giải trên mặt trang, deck ở trần 55 trang).

**Đếm tay các trang ≥ 50.** Tôi đếm lại 1-01, 1-02, 1-03, 1-06, 2-01, 2-03, 3-02, 3-04, 3-06, 4-02, 4-03, 4-06, 5-01, 5-02, 5-03, 5-04, 5-06, 5-12, 6-02, 6-03, 6-04, 6-05, 7-01, 7-02, 7-03, 7-04, 7-06. Theo cùng quy ước, số đếm tay khớp số máy ±1. Ví dụ 6-02: 62 token, trừ "01.15" và "01.29" còn 60. Nếu tính cả số ngoài bảng (số hiệu kết quả, "500", "0,001"…), năm trang vượt 60 từ 1 đến 3 âm tiết: 5-01 (61), 5-06 (61), 6-02 (62), 7-04 (62), 7-06 (63). Tôi theo quy ước của công cụ nên không ghi đây là phát hiện. Điều phối viên chốt quy ước khi đếm lại.

Các trần khác: mọi trang ≤ 6 dòng nội dung và ≤ 1 công thức hiển thị (máy). Dòng dài nhất ngoài hai ngoại lệ là 24 âm tiết, ở các `strand-lead` (trần 25). Các dòng 20 âm tiết (5-11, 6-03, 6-05) nằm đúng trần. Mỗi trang có tối đa 1 hộp chữ.

**Kết luận về mật độ:** không trang nào vượt trần mà thiếu ngoại lệ đã ghi.

## Nhận xét chung của người học

- Các trang ý tưởng chứng minh (3-03, 4-03, 5-09, 6-03, 6-06) theo được. Mỗi bước ghi giả thiết vào ở đâu và bỏ giả thiết thì hỏng ở bước nào. Chỗ vấp duy nhất là bước 3 của 6-06 (đã ghi ở bảng).
- Các ví dụ tính tay (2-04, 3-05, 5-05, 6-04) đủ chậm khi có bảng hoặc hình đi kèm. Hai chỗ nhanh quá là 2-04 (hàm lỗi có trọng số) và hàng $\hat t$ ở 3-05.
- Hình giúp hiểu thật: hai hàm ngưỡng (1-06), rủi ro thực nghiệm và rủi ro kì vọng theo $t$ (3-01), $0{,}8^m$ và $0{,}6^m$ trên thang log (5-05), khối $C$ (6-06), ba mốc rủi ro vượt mức (5-11).
- Ở 1600×900, chữ trong mọi hình đọc được. Chữ trên trang không tràn, không chồng.

**Kết luận:** đạt khi sửa. Có 0 phát hiện chặn bàn giao, 0 nghiêm trọng, 5 trung bình, 18 nhẹ.

## Đề xuất sửa ghi chú

Không có. Mọi chỗ cần sửa ở trên thuộc deck. Ghi chú bài giảng đã có đủ định nghĩa mà deck cần dẫn: $D_\eta$, $D_f$ (Ví dụ 01.1), hai rủi ro vượt mức (Định nghĩa 01.24), điều kiện hàm lỗi 0–1 của Định nghĩa 01.28.
