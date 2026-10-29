# Rà soát 2 — chính xác toán học (2026-10-30)

Người rà chứng minh lại mọi kết quả và tính lại mọi con số bằng số hữu tỉ chính xác, liệt kê đủ mọi mẫu dưới $D_f$ với $m\le6$. **Mọi con số đều đúng; mọi chứng minh đứng vững.** Không có lỗi chặn bàn giao.

**Kiểm tra của điều phối viên:** $S=((1,0),(4,1))$ có tập nghiệm ERM $\{h_2,h_3,h_4\}$, nên $A_{\min}$ chọn $h_2$ (rủi ro 0,2): câu ở §11 chỉ đúng trên $S_f$. Dưới $D_\eta$, $\eta$ không bằng $\tfrac12$ hay $\tfrac15$ ở điểm nào, nên quy tắc Bayes duy nhất. Cả hai phát hiện đúng.

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nghiêm trọng | §5 cuối (sau Mệnh đề 01.13) và §11 đoạn kết | "Lớp hàm ngưỡng loại hàm ghi nhớ … thay vì vô số hàm khớp mẫu" sai trên $\mathcal X=\{1..5\}$: 2/32 hàm khớp $S_f$, đó là $h_3,h_4$; $A_{\mathrm{gn}}(S_f)=\mathbb 1[x\ge4]=h_4\in\mathcal H$. "Vô số" và "rủi ro 1" chỉ đúng khi $\mathcal X=[0,1]$. | đếm bằng script | Nói rõ so với $\mathcal X$ liên tục (Ví dụ 01.2). Nếu giữ $\mathcal X$ hữu hạn, dùng mẫu có $x=3,5$ dương nhưng không có $x=4$: $A_{\mathrm{gn}}=\mathbb 1[x\in\{3,5\}]\notin\mathcal H$, $L_{D_f}=0{,}2$. Bỏ "vô số". |
| trung bình | §11 đoạn kết ("$A_{\min}$ chọn $h_3$…, $A_{\max}$ chọn $h_4$…") | Chỉ đúng khi mẫu chứa cả $x=2$ và $x=4$ (như $S_f$). | $S=((1,0),(4,1))$: $A_{\min}\to h_2$ (0,2); $S=((1,0),(2,0),(5,1))$: $A_{\max}\to h_5$ (0,4) | "Trên $S_f$, …" hoặc thêm điều kiện. |
| trung bình | Mệnh đề 01.20, Bảo đảm (b), câu cuối "Hàm tối ưu không duy nhất" | Sai với $D_\eta$ (duy nhất). | Phụ lục B | "nói chung không duy nhất…; duy nhất (sai khác tập xác suất 0) khi $\Pr(\eta(X)=\text{ngưỡng})=0$". |
| trung bình | Sau Định nghĩa 01.22 (câu về Bayes $+\epsilon$) | Chỉ đúng khi $\mathcal X$ vô hạn (trùng rà soát 3). | NFL cần $\lvert\mathcal X\rvert>2m$ | Thêm "khi $\mathcal X$ vô hạn". |
| trung bình | Mệnh đề 01.13, Bảo đảm 1 và Bước 1–2 | Chưa kiểm tính đo được đồng thời $(s,\xi,z)\mapsto\ell(A_m(s;\xi),z)$ mà Định nghĩa 01.6 đòi; Phụ lục A(iii) có nhưng không được trích; Hệ quả 01.26(a) dựa vào bước này. | | Thêm câu trích Phụ lục A(iii). |
| trung bình | Định nghĩa 01.9 "(khi tập nghiệm khác rỗng)" so với Ví dụ 01.7 | Lượng từ mơ hồ, đọc theo một cách thì mâu thuẫn Ví dụ 01.7; Định nghĩa 01.12 dựa vào cách đọc này. | | "Giả sử $\arg\min_{\mathcal H}L_S\ne\emptyset$ với mọi $S$. Thuật toán $A$ là thuật toán ERM nếu…"; Ví dụ 01.7: "giả thiết này không thỏa, nên không có thuật toán ERM". |
| nhẹ | Nhận xét 01.19 | $m_A=\infty$ thực ra với mọi $\epsilon\in(0,1)$ (lấy $Y\equiv1$, $L_D(h_6)=1$). | | Thêm câu. |
| nhẹ | Mệnh đề 01.4 | Với $\ell\ge0$ đẳng thức đúng không cần khả tích; Bước 1 chỉ chứng minh đo được. | | Ghi giả thiết $L_D(h)<\infty$ chỉ để hai vế là số thực; tiêu đề Bước 1 "đo được". |
| nhẹ | Ví dụ 01.10 | Đổi hai thứ cùng lúc (nguyên tử và nhãn 0); không cô lập giả thiết không có nguyên tử. | C.3 | Dùng $Y\equiv1$ trên $\{1..5\}$: $\mathbb E_SL_D(A_{\mathrm{gn}}(S))=0{,}8^m\approx0{,}107$ tại $m=10$; hoặc nói rõ đã đổi cả phân bố nhãn. |
| nhẹ | §9 cận $\lceil\ln(1/\delta)/\epsilon\rceil$ | Cần nêu thuật toán ($A_{\max}$); ERM bất kì chỉ có $2(1-\epsilon)^m$. Kiểm tra thêm: trên $\{1..5\}$, $m_{A_{\max}}(0{,}1;0{,}05)=29$, $m_{A_{\max}}(0{,}25;0{,}05)=11$. | | "…với lớp hàm ngưỡng và thuật toán $A_{\max}$". |
| nhẹ | Nhận xét 01.25 | "Khi $\mathcal X$ hữu hạn… tự thỏa" cần σ-đại số mọi tập con và thuật toán tất định (hoặc $\{\xi:A(s;\xi)=h\}$ đo được). | | Thêm điều kiện. |
| nhẹ | Phụ lục A(iii) | Cần nửa câu: σ-đại số Borel của $\mathcal Z^m\times[0,1]$ trùng σ-đại số tích (không gian khả li). | | Thêm. |
| nhẹ | Phụ lục B "Tính không duy nhất" | Chiều "khi và chỉ khi" cần $L_D(g)-L_D(h_{\mathrm{Bayes}})=\mathbb E[\lvert2\eta(X)-1\rvert\mathbb 1[g(X)\ne h_{\mathrm{Bayes}}(X)]]$ (với $\ell_c$: trọng số $\lvert c_{FN}\eta-c_{FP}(1-\eta)\rvert$). | | Thêm công thức. |
| nhẹ | Mệnh đề 01.20 Bước 2 | "tức khi $g=h_{\mathrm{Bayes}}$" đọc như "khi và chỉ khi". | | "…chẳng hạn khi $g=h_{\mathrm{Bayes}}$". |
| nhẹ | Ví dụ 01.1 so với Thuật toán 01.11 | Định nghĩa đầu của $A_{\max}$ không phải ERM trên mọi mẫu ($S=((1,1),(2,0),(3,0))$ cho $h_1$, $L_S=\tfrac23>\tfrac13$). | | Định nghĩa thẳng là ngưỡng lớn nhất/nhỏ nhất trong tập nghiệm ERM (trùng rà soát 1). |
| nhẹ | Hệ quả 01.26 Giả thiết | "mọi quy tắc chọn khi bằng nhau" phải đo được. | | Thêm "đo được". |
| nhẹ | Định nghĩa 01.16 so với 01.18; $m_0\in\mathbb N$ | Kí hiệu $m_A$ hai nghĩa; $0\in\mathbb N$? | | $\mathbb N=\{1,2,\dots\}$; tên khác ở Định nghĩa 01.16. |
| nhẹ | Sau Định nghĩa 01.14 | "mọi nghiệm ERM có rủi ro thực nghiệm bằng 0" chỉ với xác suất 1. | | Thêm. |
| nhẹ | §4 precision | Lí do chặt: $D\mapsto L_D(h)$ affine theo hỗn hợp, precision thì không; precision không xác định khi $\Pr(h=1)=0$. | ví dụ $D_1,D_2$ | Tùy chọn. |
| nhẹ | Định nghĩa 01.21 | $L_D^{\mathrm{Bayes}}$ chỉ cho phân lớp; phân tích cần $\inf_{\mathcal H}L_D<\infty$. | | Ghi "(phân lớp)"; thêm điều kiện rủi ro hữu hạn. |

Danh sách kiểm tra số (≈ 40 mục) đều OK, gồm mọi bảng rủi ro, $a(t)$, $b(t)$, tập nghiệm ERM, $0{,}273$, $1/6$, $n_0$/$n_1$/$E$, Ví dụ 01.7, Nhận xét 01.15, Ví dụ 01.8 (0,8^m, 0,6^m, 14, 6, 0,0227, 4,4%), Ví dụ 01.9, Ví dụ 01.10 (0,0644), §9 (30), câu hỏi ôn và cuối buổi.
