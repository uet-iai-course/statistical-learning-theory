# Duyệt deck Bài 01 — Vai 2 `toan-hoc` (độ chính xác toán học, thống nhất với ghi chú)

Đối tượng: `2627-1/lecture-01-mo-hinh-hoc.html` (55 trang, bản đóng băng), chín SVG trong `img/lec-01/`. Đối chiếu: `materials/lec-01/lecture-note.md`, `materials/lec-01/exercises.md`, quyết định mục "Bộ trang chiếu" của `review-log.md`. Chỉ đọc; không sửa deck, SVG, storyboard, ghi chú.

## 1. Tính lại các con số

Tính lại bằng phân số đúng và liệt kê đủ trường hợp (script trong thư mục nháp của vai, `verify.py`). Mọi con số dưới đây **đúng**.

| Đại lượng (trang) | Giá trị trên deck | Kết quả tính lại |
|---|---|---|
| $L_{D_\eta}(h_t)$, $t=1..6$ (2-04, 3-01, SVG `rui-ro-nguong`) | $0{,}52;0{,}32;0{,}22;0{,}32;0{,}28;0{,}48$ | đúng |
| $L^c_{D_\eta}(h_t)$, $(c_{FP},c_{FN})=(1,4)$ (2-04) | $0{,}52;0{,}32;0{,}37;0{,}92;1{,}12;1{,}92$ | đúng; $0{,}2(0{,}25+0{,}85)=0{,}22$, $0{,}2(4\cdot0{,}25+0{,}85)=0{,}37$, $0{,}2(4\cdot0+1{,}6)=0{,}32$ |
| số lỗi trên $S_\eta$, $L_{S_\eta}(h_t)$ (3-01) | $3,2,2,3,2,3$; $\tfrac12,\tfrac13,\ldots$ | đúng |
| $L_{D_\eta}(h_5)-L_{S_\eta}(h_5)$ (3-06) | $-\tfrac4{75}$ | đúng ($\approx-0{,}053$) |
| bảng $m=1$ dưới $D_f$ (3-05) | $\hat t=6,6,3,4,5$; $L_{D_f}=0{,}6;0{,}6;0;0{,}2;0{,}4$; trung bình $0{,}36$ | đúng; khớp $0{,}2(0{,}8+0{,}6+0{,}4)=0{,}36$; kiểm thêm $m=2,3$ bằng liệt kê: $0{,}232$, $0{,}1584$, khớp công thức Phụ lục C.2 |
| $\mathbb E_S L_{D_f}(A_{\max}(S))$ tại $m=10$ (ghi chú 3-05) | $\approx0{,}0227$ | đúng ($0{,}022705$) |
| Bài tập 01.2(a) (3-07) | $c_0=(1,1,0,1,1,0)$, $c_1=(0,0,1,1,0,1)$, $E=(4,3,2,3,3,2,3)$, $\{h_3,h_6\}$ | đúng |
| Bài tập 01.2(b) (ghi chú 3-07) | $L_D(h_3)=0{,}29$, $L_D(h_6)=0{,}45$, $\min=L_D(h_4)=0{,}25$, chênh $0{,}16$ | đúng |
| $0{,}999^{500}$ (5-01) | $\approx0{,}61$ | $0{,}6064$, đúng |
| $0{,}8^{13},0{,}8^{14}$; $0{,}6^5,0{,}6^6$ (5-05) | $0{,}0550;0{,}0440$; $0{,}0778;0{,}0467$ | đúng; $0{,}6^{14}\approx0{,}00078<0{,}001$ (chú thích hình) đúng |
| $0{,}2\min\{\tfrac14,\tfrac34\}$ (5-07) | $0{,}05$ | đúng |
| $L^{\mathrm{Bayes}}_{D_\eta}$ (5-07), $L^c$ Bayes (5-10) | $0{,}18$; $0{,}32$ | đúng |
| $\lvert2\cdot0{,}4-1\rvert\cdot0{,}2$ (ghi chú 5-09) | $0{,}04$ | đúng |
| phân rã rủi ro vượt mức (5-11) | $0{,}14=0{,}10+0{,}04$ | đúng |
| Bài tập 01.4(a) (4-05) | $0{,}3$ | đúng |
| Ví dụ 01.11 (6-04) | $5\cdot0{,}2\cdot0{,}8^m=0{,}8^m$, $0{,}8^{10}\approx0{,}107$ | đúng; kiểm liệt kê $m=2$: $0{,}64$ |
| $\lceil10\ln20\rceil$, $e^{-3}$, $e^{-2{,}9}$ (6-05, 6-07) | $30$; $0{,}0498$; $0{,}0550$ | đúng ($29{,}957$) |
| Bài tập 01.1(d) (7-03) | ngưỡng $\tfrac45$ | đúng |

**SVG (tọa độ và nhãn):** kiểm từng tệp theo phép đổi tọa độ của trục.

- `rui-ro-nguong.svg`: trục $y=272-326{,}67\,r$; mọi điểm (chấm tròn $\tfrac12,\tfrac13$; ô vuông $0{,}52\ldots0{,}48$) đúng đến $0{,}1$ px.
- `that-bai-df.svg`: $y=76+68(-\log_{10}p)$, $x=90+24{,}5m$; hai đường $0{,}8^m$, $0{,}6^m$, mức $\delta$ ($y=164{,}5$), các vạch $m=6$, $m=14$ đúng.
- `can-co-mau.svg`: $y=110+86{,}67(-\log_{10}p)$, $x=90+15{,}3125m$; ba đường $0{,}8^m$, $0{,}6^m$, $e^{-0{,}1m}$, mức $\delta$ ($y=222{,}8$), các vạch $6$, $14$, $30$ đúng.
- `eta-nguong.svg`, `eta-hai-nguong.svg`: cột $\eta=0,\tfrac14,\tfrac34,\tfrac25,1$ và hai đường $\tfrac12$ ($y=125$), $\tfrac15$ ($y=176$) đúng; hàng dự đoán $0,0,1,0,1$ và $0,1,1,1,1$ đúng.
- `rui-ro-vuot-muc.svg`: ba mốc $0{,}18$, $0{,}22$, $0{,}32$ tại $x=248{,}5$, $326{,}5$, $521{,}5$ đúng.
- `ghi-nho.svg`: năm điểm $0{,}12;0{,}31;0{,}47;0{,}68;0{,}90$ tại đúng vị trí; hàm ghi nhớ vẽ đúng (bằng $1$ chỉ tại năm điểm).
- `hai-ham-nguong.svg`, `vung-loi.svg`: nội dung đúng.
- Không công thức nào bị vẽ vào SVG.

## 2. Bảng thống nhất trang → khối ghi chú

Ký hiệu cột "Thống nhất": ✓ khớp; số trong ngoặc là số phát hiện ở §3.

| Trang | Khối ghi chú | Thống nhất |
|---|---|---|
| L01-1-01 | đoạn mở đầu, §7 đoạn cuối | ✓ |
| L01-1-02 | Kiến thức tiên quyết, §2 (T1), (T2) | (T2) thiếu vế rủi ro hữu hạn (8) |
| L01-1-03 | Mục tiêu học tập | ✓ |
| L01-1-04 | §1–§9 | ✓ |
| L01-1-05 | câu hỏi trung tâm; ghi chú diễn giả tóm §4–§9 | ghi chú diễn giả: "chỉ khi" (4), thiếu "khả diễn" (1) |
| L01-1-06 | Câu hỏi mở đầu | ✓ |
| L01-2-01 | §1 (tám thành phần, bảng nguồn ngẫu nhiên), Định nghĩa 01.4 | ✓ |
| L01-2-02 | §3, Ví dụ 01.1 | dữ liệu ✓; $D_\eta$, $D_f$ chưa định nghĩa trên mặt trang (13) |
| L01-2-03 | ứng dụng sàng lọc (§3), Định nghĩa 01.1, ví dụ sau định nghĩa | ✓ |
| L01-2-04 | Ví dụ 01.2, Phụ lục C.1 | ✓ |
| L01-2-05 | Định nghĩa 01.5, Ví dụ 01.4 | ✓ |
| L01-3-01 | Định nghĩa 01.6, Ví dụ 01.5 | ✓ |
| L01-3-02 | Mệnh đề 01.7, đoạn sau chứng minh | dòng cuối thiếu $S\sim D_\eta^6$ (3) |
| L01-3-03 | chứng minh Mệnh đề 01.7; Bài tập 01.3(a) | ✓ |
| L01-3-04 | Định nghĩa 01.8, quy tắc chọn, Ví dụ 01.6; ghi chú diễn giả: Nhận xét 01.11, Ví dụ 01.7, Định nghĩa 01.12 | ✓ |
| L01-3-05 | Nhận xét 01.9 (ví dụ dựng mới, $m=1$, khớp quyết định 11.3 của cổng) | ✓ |
| L01-3-06 | Định nghĩa 01.10 và đoạn sau, Nhận xét 01.9 | ✓ (ghi chú diễn giả: (12)) |
| L01-3-07 | Bài tập 01.2(a), Thuật toán 01.13 | ✓ |
| L01-4-01 | Định nghĩa 01.14, Ví dụ 01.8 | $\mathcal M_{\mathcal X}$ thu hẹp về $[0,1]$ (6) |
| L01-4-02 | Mệnh đề 01.15 | ✓ |
| L01-4-03 | chứng minh Mệnh đề 01.15 | ✓; ghi chú diễn giả (5) |
| L01-4-04 | chứng minh Mệnh đề 01.15 Bước 3 | ✓ |
| L01-4-05 | Bài tập 01.4(a) | ✓ |
| L01-4-06 | §5, các đoạn sau chứng minh Mệnh đề 01.15 | ✓ |
| L01-5-01 | §6 đoạn đầu | ✓ |
| L01-5-02 | Định nghĩa 01.16, 01.18, Nhận xét 01.17 | ✓ |
| L01-5-03 | §6, đoạn thứ tự lượng từ | ✓ |
| L01-5-04 | Định nghĩa 01.20, Nhận xét 01.21 | ✓ |
| L01-5-05 | Ví dụ 01.9 | ✓ |
| L01-5-06 | Bài tập 01.5(d) câu 4, (e); Nhận xét 01.19 | ✓ |
| L01-5-07 | §7 đoạn đầu, Định nghĩa 01.22, Ví dụ 01.10 (phần hàm lỗi 0–1) | (6) |
| L01-5-08 | Mệnh đề 01.23 [O] | ✓ |
| L01-5-09 | ý tưởng sau Mệnh đề 01.23, Phụ lục B | ✓ |
| L01-5-10 | Ví dụ 01.10 (phần $\ell_c$), Mệnh đề 01.23(b) | ✓ |
| L01-5-11 | Định nghĩa 01.24 và đoạn sau | (10) |
| L01-5-12 | Định nghĩa 01.25, Nhận xét 01.26, 01.27 | ✓ |
| L01-6-01 | Định nghĩa 01.28 và câu hỏi sau | ✓ |
| L01-6-02 | Hệ quả 01.29, Nhận xét 01.30 | thiếu nhãn (O1) (9) |
| L01-6-03 | chứng minh Hệ quả 01.29 | giả thiết vào sai bước (2) |
| L01-6-04 | Ví dụ 01.11 | ✓ |
| L01-6-05 | Mệnh đề 01.31 [S], đoạn sau | ✓ |
| L01-6-06 | chứng minh Mệnh đề 01.31 | ✓ |
| L01-6-07 | chứng minh Mệnh đề 01.31 (bước cuối), Ví dụ 01.9 | ✓ |
| L01-7-01 | §5–§9 | ✓; ghi chú diễn giả (5) |
| L01-7-02 | §7 đoạn cuối, §11 | bỏ giả thiết khả diễn (1); bỏ không có nguyên tử (7) |
| L01-7-03 | Bài tập 01.1(d) | dữ liệu đề chưa đủ trên mặt trang (11) |
| L01-7-04 | §11, Ví dụ 01.6, 01.9, Nhận xét 01.19, Mệnh đề 01.31 | ✓ |
| L01-7-05 | §10, `exercises.md` | số bài khớp; (14) |
| L01-7-06 | §12 | ✓; tên Bài 02 khớp `lec-02/lecture-note.md` |
| L01-k-00 (6 trang mạch) | — | ✓ |

**Số hiệu và tên kết quả:** mọi số hiệu dẫn trên mặt trang và trong ghi chú diễn giả (Định nghĩa 01.3, 01.4, 01.5; Mệnh đề 01.7, 01.15, 01.23, 01.31; Hệ quả 01.29; Thuật toán 01.13; Ví dụ 01.3, 01.6, 01.7, 01.9, 01.11; Nhận xét 01.17, 01.19, 01.21, 01.26, 01.27, 01.30; Bài tập 01.1–01.10 với đúng phần) đều trỏ đúng khối có cùng nội dung. Mức chứng minh [O] (Mệnh đề 01.23) và [S] (Mệnh đề 01.31) được nêu ở ghi chú diễn giả. Kí hiệu ($L_D$, $L_S$, $L^c_D$, $D_\eta$, $D_f$, $S_\eta$, $S_f$, $\tilde S_f$, $h_t$, $\hat t=\hat t(S)$, $A_{\min}$, $A_{\max}$, $A_{\mathrm{gn}}$, $h_{\equiv1}$, $\mathbb 1_F$, $\mathcal M_{\mathcal X}$, $D_1$, $h^\star$, $t^\star$, $G$, $C$, $\beta$, $m_A$, $m_{\mathcal H}$) trùng ghi chú.

**Ý tưởng chứng minh:** 3-03, 4-03, 5-09, 6-06 đúng bước, đúng tên bất đẳng thức then chốt (tính tuyến tính; bất đẳng thức hợp; tối thiểu hóa từng điểm và $\mathbb E[\mathbb E[U\mid X]]=\mathbb E[U]$; $1-x\le e^{-x}$), giả thiết vào đúng bước. Trong 6-06, "khối đầu ngắn nhất $C=\{t^\star,\ldots,k\}$ có $D_{\mathcal X}(C)>\epsilon$" trùng với $k$ lớn nhất có $G(k)\le\epsilon$ của ghi chú (khi $G(K+1)>\epsilon$). Riêng 6-03: phát hiện (2). Phản ví dụ khi bỏ giả thiết (3-03/3-05 bỏ "$h$ không phụ thuộc $S$"; 4-03/6-04 bỏ "không có nguyên tử"; 5-04 bỏ "mọi $m\ge m_0$") đúng.

## 3. Phát hiện

| # | mức độ | trang chiếu | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|---|
| 1 | nghiêm trọng | L01-7-02 (dòng 5); L01-1-05 (ghi chú diễn giả, dòng 5) | Phát biểu rút gọn của Mệnh đề 01.31 bỏ giả thiết khả diễn. Đặt ngay sau dòng 1 (bảo đảm bất khả diễn $L_D(A(S))\le\inf_hL_D(h)+\epsilon$), câu đọc thành: $A_{\max}$ đạt bảo đảm bất khả diễn với $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$, điều này sai (Bài tập 01.10(b): thuật toán cùng quy tắc thất bại dưới nhãn có nhiễu). | Deck: "Trên lớp hàm ngưỡng, $A_{\max}$ đạt bảo đảm khi $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$."; ghi chú diễn giả 1-05: "cấu trúc của lớp hàm ngưỡng cho cỡ mẫu $\lceil\ln(1/\delta)/\epsilon\rceil$". Ghi chú, Mệnh đề 01.31, Giả thiết: "$D$ … với $(D,\mathcal H)$ khả diễn"; quy định "a compact statement may drop wording, never a condition". | 7-02: "Trên lớp hàm ngưỡng, với mọi phân bố khả diễn, $A_{\max}$ đạt bảo đảm học PAC khi $m\ge\lceil\ln(1/\delta)/\epsilon\rceil$." 1-05: thêm "trong trường hợp khả diễn". |
| 2 | trung bình | L01-6-03 (bước 1, bước 4, ghi chú diễn giả) | Giả thiết "không có nguyên tử" được gắn chỉ cho phần (b) của Hệ quả 01.29, nhưng bước 1 của phần (a) cũng cần nó: khoảng cách tổng quát hóa bằng $1$ dùng $L_D(A_{\mathrm{gn}}(S))=1$, tức Mệnh đề 01.15(b). Ghi chú diễn giả "lớp chứa hàm phân lớp ghi nhớ qua phần (a), không có nguyên tử qua phần (b)" đặt cạnh các bước gắn nhãn (a), (b) của hệ quả nên đọc thành phần (a), (b) của hệ quả. | Deck bước 1: "khoảng cách tổng quát hóa bằng $1$ trên mọi $S$ (giả thiết lớp chứa hàm ghi nhớ)"; bước 4: "(giả thiết không có nguyên tử)". Ghi chú, chứng minh Hệ quả 01.29, Bước 1: "Theo Mệnh đề 01.15(a)(b), khoảng cách tổng quát hóa bằng $1-0=1$"; câu cuối "qua phần (a) … qua phần (b)" chỉ phần của Mệnh đề 01.15. | Bước 1: "(giả thiết lớp chứa hàm ghi nhớ và không có nguyên tử, Mệnh đề 01.15(a)(b))". Ghi chú diễn giả: "lớp chứa hàm phân lớp ghi nhớ qua Mệnh đề 01.15(a), không có nguyên tử qua Mệnh đề 01.15(b); phần (a) của hệ quả dùng cả hai, phần (b) dùng Mệnh đề 01.15(b), (c)". Xem thêm Đề xuất sửa ghi chú 1. |
| 3 | trung bình | L01-3-02 (dòng cuối) | Kì vọng $\mathbb E_S[L_S(h_3)]=0{,}22$ không ghi phân bố của $S$. Dòng "Ví dụ." ngay trên trang xét $D_f$, và dưới $D_f$ thì $\mathbb E_S[L_S(h_3)]=L_{D_f}(h_3)=0$; con số $0{,}22$ chỉ đúng với $S\sim D_\eta^6$. | Deck: "Trên một tập cụ thể vẫn lệch: $L_{S_\eta}(h_3)=\tfrac13$, trong khi $\mathbb E_S[L_S(h_3)]=0{,}22$." Ghi chú, đoạn sau chứng minh Mệnh đề 01.7: "$\mathbb E_{S\sim D_\eta^6}\big[L_S(h_3)\big]=L_{D_\eta}(h_3)=0{,}22$". | Viết "$\mathbb E_{S\sim D_\eta^6}[L_S(h_3)]=L_{D_\eta}(h_3)=0{,}22$". |
| 4 | trung bình | L01-1-05 (ghi chú diễn giả, dòng 2) | "chỉ khi" biến điều kiện đủ của Mệnh đề 01.7 thành điều kiện cần; khẳng định này sai (ví dụ thuật toán hằng, hay một $A(S)$ không phụ thuộc thực sự vào $S$, vẫn không chệch). Ghi chú chỉ nói "nói chung" không bằng. | Deck: "$L_S(h)$ là ước lượng không chệch của $L_D(h)$ chỉ khi $h$ không phụ thuộc $S$." Ghi chú, Nhận xét 01.9: "Do đó, nói chung, $\mathbb E_S[L_S(A(S))]\ne\mathbb E_S[L_D(A(S))]$". Trang 7-02 viết đúng: "khi $h$ không phụ thuộc $S$; với $h=A(S)$ thì nói chung không". | Dùng đúng câu của 7-02. |
| 5 | trung bình | L01-4-03 (ghi chú diễn giả); L01-7-01 (ghi chú diễn giả) | Lẫn $L_{D_1}(A_{\mathrm{gn}}(S))$ (biến ngẫu nhiên) với kì vọng của nó theo $S$. Rủi ro kì vọng của hàm ghi nhớ trên năm điểm không bằng $0{,}8^m$; kì vọng theo $S$ của nó bằng $0{,}8^m$. Đây đúng là phân biệt "đại lượng cố định / ngẫu nhiên" mà bài nhấn mạnh. | 4-03: "trên năm điểm đồng khả năng, rủi ro kì vọng của hàm ghi nhớ là $0{,}8^m$"; 7-01: "hàm ghi nhớ trên năm điểm có nguyên tử cho rủi ro kì vọng $0{,}8^m$". Ghi chú, Ví dụ 01.11: "$\mathbb E_S\big[L_{D_1}(A_{\mathrm{gn}}(S))\big]=5\cdot0{,}2\cdot0{,}8^m=0{,}8^m$". | "… kì vọng theo $S$ của rủi ro kì vọng của hàm ghi nhớ là $\mathbb E_S[L_{D_1}(A_{\mathrm{gn}}(S))]=0{,}8^m$". |
| 6 | trung bình | L01-4-01 (dòng 2); L01-5-07; L01-6-04 | $\mathcal M_{\mathcal X}$ được định nghĩa trên mặt trang chỉ cho $\mathcal X=[0,1]$, rồi dùng lại cho $\mathcal X=\{1,\ldots,5\}$ (5-07: định nghĩa rủi ro Bayes; 6-04). Ghi chú định nghĩa $\mathcal M_{\mathcal X}$ cho mọi tập đầu vào có σ-đại số. Ở 5-07, định nghĩa rủi ro Bayes cũng không nêu "hàm lỗi 0–1, $\mathcal Y=\{0,1\}$" của Định nghĩa 01.22 (ý này chỉ có ở ghi chú diễn giả). | 4-01: "Lớp $\mathcal M_{\mathcal X}$: mọi hàm phân lớp đo được $[0,1]\to\{0,1\}$." Ghi chú, Ví dụ 01.8: "Với một tập đầu vào $\mathcal X$ có σ-đại số, kí hiệu $\mathcal M_{\mathcal X}$ là lớp mọi hàm phân lớp đo được $\mathcal X\to\{0,1\}$." Định nghĩa 01.22: "Cho tập nhãn $\mathcal Y=\{0,1\}$, hàm lỗi 0–1 …". | 4-01: "Lớp $\mathcal M_{\mathcal X}$: mọi hàm phân lớp đo được $\mathcal X\to\{0,1\}$, ở đây $\mathcal X=[0,1]$." 5-07: "Rủi ro Bayes (Bayes risk) dưới $\ell_{0\text{-}1}$ chỉ phụ thuộc $D$:". |
| 7 | nhẹ | L01-7-02 (dòng 4) | Câu tóm tắt Mệnh đề 01.15 bỏ giả thiết không có nguyên tử, giả thiết mà 6-04 vừa chỉ ra là cần thiết (trên $\mathcal M_{\mathcal X}$ với $\mathcal X$ hữu hạn, kì vọng rủi ro của hàm ghi nhớ tiến về $0$). | Deck: "$L_S$ nhỏ không đủ: trên $\mathcal M_{\mathcal X}$, một nghiệm ERM có $L_S=0$ và $L_D=1$." Ghi chú, Mệnh đề 01.15, Giả thiết: "$D_{\mathcal X}=U[0,1]$ không có nguyên tử". | "… trên $\mathcal M_{\mathcal X}$ với $\mathcal X=[0,1]$ và $X\sim U[0,1]$, một nghiệm ERM có $L_S=0$ và $L_D=1$." |
| 8 | nhẹ | L01-1-02 (dòng (T2)) | Nhãn (T2) trên mặt trang thiếu vế "khi hàm lỗi không bị chặn, $L_D(h)<\infty$". Vế này chỉ ở ghi chú diễn giả. Trong bài, hàm lỗi trên mọi trang kết quả đều bị chặn và 3-02 ghi riêng $L_D(h)<\infty$, nên không có kết luận nào sai. | Deck: "(T2) Hàm lỗi $\ell(h,z)\ge0$ đo được theo $z$, với mọi giả thuyết $h$." Ghi chú §2: "**(T2) Hàm lỗi.** $\ell\ge0$ và $\ell(h,\cdot)$ đo được với mọi $h\in\mathcal H$; khi hàm lỗi không bị chặn, ta cần $L_D(h)<\infty$." | Thêm "; khi $\ell$ không bị chặn, $L_D(h)<\infty$." |
| 9 | nhẹ | L01-6-02 (Giả thiết, Bảo đảm (b)) | Ghi chú dẫn nhãn (O1) cho thuật toán ERM chính xác; deck chỉ viết "thuật toán ERM" và không định nghĩa (O1)/(O2) trên mặt trang (chỉ ở ghi chú diễn giả 3-04). Bảo đảm (b) không nêu "dưới phân bố khả diễn $D$". | Ghi chú, Hệ quả 01.29: "gồm thiết lập của Ví dụ 01.8 cùng (T1) và (O1)"; Bảo đảm (b): "Dưới phân bố khả diễn $D$ của Ví dụ 01.8, …". | Giả thiết: "thuật toán ERM chính xác ($\hat A$ bất kì ở (a), $A_{\mathrm{gn}}$ ở (b))"; (b): "dưới $D$ khả diễn, $\Pr_S[\ldots]=0$ …". Nhãn (O1) có thể để ở ghi chú diễn giả nếu không nêu trên mặt trang trước đó. |
| 10 | nhẹ | L01-5-11 (dòng 1) | Định nghĩa rủi ro vượt mức rút gọn bỏ hai điều kiện của Định nghĩa 01.24: $L_D(h)<\infty$ và "trong phân lớp" cho rủi ro vượt mức so với rủi ro Bayes. Trang chỉ dùng phân lớp với $\ell_{0\text{-}1}$ nên không có con số nào sai. | Ghi chú, Định nghĩa 01.24: "một hàm dự đoán $h$ với $L_D(h)<\infty$ … so với rủi ro Bayes, trong phân lớp, là …". | "Rủi ro vượt mức (excess risk) của $h$ trong phân lớp: …". |
| 11 | nhẹ | L01-7-03 | Mặt trang thiếu hai dữ kiện của đề Bài tập 01.1: hàm phân lớp báo $1$ là chặn thư; $x\in\{0,1\}^p$. Lời giải "chặn nhầm là dương tính giả" cần dữ kiện thứ nhất. | Đề Bài tập 01.1: "Nhãn $y=1$ nếu thư là thư rác; hàm phân lớp báo $1$ nghĩa là chặn thư." | Dòng 1: "… $y=1$ là thư rác, báo $1$ là chặn thư; …". |
| 12 | nhẹ | L01-3-06 (ghi chú diễn giả) | "Dòng thứ tư" chỉ câu "Do đó trên chính tập huấn luyện …", nhưng nếu đếm cả công thức hiển thị thì đó là dòng thứ năm. | Mặt trang: p "Khoảng cách…", công thức, p "Ngẫu nhiên…", p "Kì vọng…", p "Do đó…". | Trích nội dung thay cho số dòng: "Câu 'trên chính tập huấn luyện dùng để chọn hàm, $L_S$ có thể đánh giá thấp $L_D$' trả lời …". |
| 13 | nhẹ | L01-2-02 | $D_\eta$, $D_f$ xuất hiện trên mặt trang ("Dữ liệu có nhiễu từ $D_\eta$") nhưng công thức $D_\eta(y\mid x)$, $D_f(y\mid x)$ chỉ ở ghi chú diễn giả. Bảng $\eta$, $f$ đủ để tính, nhưng tên phân bố chưa được định nghĩa. | Ghi chú, Ví dụ 01.1: "$D_\eta(y\mid x)=\eta(x)^y(1-\eta(x))^{1-y}$ … $D_f(y\mid x)=\ldots$". | Thêm nửa dòng: "$D_\eta$: nhãn $1$ với xác suất $\eta(x)$; $D_f$: nhãn $f(x)$". |
| 14 | nhẹ | L01-7-05 | Bài tập 01.8(b) dùng kỹ thuật chặn xác suất bỏ sót của mạch 6 và cận $\lceil\ln(1/\delta)/\epsilon\rceil$, nhưng xếp ở dòng "Học PAC" (mạch 5); ghi chú diễn giả của chính trang nói 01.8 và 01.9 dùng cùng kỹ thuật. | Lời giải Bài tập 01.8(b): "$(1-\rho)^m<(1-\epsilon)^m\le e^{-\epsilon m}$". | Chuyển 01.8 sang dòng "Rủi ro thực nghiệm nhỏ và bảo đảm học", hoặc giữ và để vai mạch truyện quyết định. |

Không phát hiện con số sai nào trên mặt trang, trong ghi chú diễn giả hay trong SVG.

## 4. Đề xuất sửa ghi chú

1. **Chứng minh Hệ quả 01.29, đoạn cuối** (nhẹ). Câu "Hai giả thiết của Mệnh đề 01.15 được dùng: lớp chứa hàm phân lớp ghi nhớ qua phần (a), và $D_{\mathcal X}$ không có nguyên tử qua phần (b)" nằm trong chứng minh có hai phần (a), (b) của chính hệ quả, nên dễ đọc thành phần của hệ quả, và cách đọc đó sai cho phần (a). Đề xuất: "… qua Mệnh đề 01.15(a), và $D_{\mathcal X}$ không có nguyên tử qua Mệnh đề 01.15(b)." Deck đã chép sự mập mờ này (phát hiện 2).
2. **Nhận xét 01.19 và lời giải câu hỏi phụ (2) của §11** (nhẹ, tùy tác giả). "trong 100 lần huấn luyện, thì có khoảng 95 lần …" đọc xác suất $1-\delta$ như một giá trị đúng; bảo đảm là "ít nhất $1-\delta$". Đề xuất: "có ít nhất khoảng 95 lần". Deck (5-06, 7-04) theo đúng ghi chú.

## 5. Kết luận

0 chặn bàn giao, 1 nghiêm trọng, 5 trung bình, 8 nhẹ. Mọi con số, đẳng thức, hằng số và tọa độ SVG đều đúng; số hiệu và kí hiệu thống nhất với ghi chú. Các phát hiện là chỗ phát biểu rút gọn bỏ giả thiết hoặc phân bố lấy mẫu (1, 3, 7–10), chỗ giả thiết vào sai bước (2), và chỗ lẫn đại lượng ngẫu nhiên với kì vọng của nó (4, 5).

**Kết luận: đạt khi sửa.**
