# Rà bài tập — chính xác toán học (2026-10-30)

Người rà tự giải từng bài trước, rồi mới xem bản lời giải; tính lại mọi con số bằng phân số chính xác và liệt kê trường hợp nhỏ. **Không có lỗi chặn bàn giao hay nghiêm trọng; không con số nào sai.** Kết luận từng bài: 01.1, 01.3, 01.4, 01.6–01.11 đúng (01.9 tốt nhất: xử lý nguyên tử đúng, $m_{A_{\max}}(0{,}1;0{,}05)=29$ đúng hai chiều; 01.11 tránh lỗi của bản lời giải UML ở 3.8(3)); 01.2(d) và 01.5(d) cần sửa. Gợi ý đúng và xếp từ yếu đến mạnh. 01.6–01.11 khớp UML 2.1, 3.1, 3.2, 3.3, 3.6, 3.8; lời giải là lập luận riêng.

**Kiểm tra của điều phối viên:** mẫu $((1,0))$ có tập nghiệm ERM $(1,\infty)$ trên lớp $\{h_t:t\in\mathbb R\}$, không có max; dưới $D_\eta$ mọi $h_t$ có rủi ro $\ge0{,}22$. Hai phát hiện trung bình đúng.

| mức độ | vị trí | vấn đề | đề xuất sửa |
|---|---|---|---|
| trung bình | 01.2(d), đề và lời giải | Đề khẳng định "chọn ngưỡng lớn nhất" xác định một thuật toán; sai trên lớp $\{h_t:t\in\mathbb R\}$ khi tập nghiệm chứa $(x_{(m)},\infty)$ (ví dụ mẫu $((1,0))$). Lời giải chỉ kết luận "trên mẫu này". | Đề: "vì sao trên $S'$ quy tắc ngưỡng nhỏ nhất không chọn được hàm nào, còn quy tắc ngưỡng lớn nhất chọn được; quy tắc sau có xác định một thuật toán trên mọi mẫu không?" Lời giải: không (mẫu toàn nhãn 0); cần quy ước, ví dụ $t=x_{(m)}+1$ khi tập nghiệm không bị chặn trên. |
| trung bình | 01.5(d), câu 2 | "trong bài toán sàng lọc dưới hàm lỗi 0–1" — ghi chú mô tả sàng lọc là bài toán có nhiễu ($D_\eta$); dưới $D_\eta$ mọi $h\in\mathcal H$ có $L\ge0{,}22>0{,}1$, nên câu 2 không đúng tuyệt đối. | Thêm điều kiện: đúng khi $(D,\mathcal H)$ khả thực (như $D_f$); dưới $D_\eta$ là bảo đảm bất khả tri $L_D\le\inf_hL_D(h)+0{,}1=0{,}32$. Hoặc sửa đề thành "bản khả thực $D_f$". |
| nhẹ | 01.1(a) | "Tám thành phần của §1" liệt kê lệch §1 của ghi chú (gộp $\mathcal X,\mathcal Y$; có "Tài nguyên"); lời giải nhiệt độ thiếu tài nguyên. | Liệt kê đúng §1; thêm "tài nguyên: cỡ mẫu $m$". |
| nhẹ | 01.4(c) | "Vì $Y=1$, $A_{\mathrm{gn}}(s)=\mathbb 1_F$" chỉ đúng với mẫu mọi nhãn bằng 1. | "với mẫu có mọi nhãn bằng 1, tức hầu chắc chắn dưới $D$". |
| nhẹ | 01.9(b) | Không nêu điều kiện đo được (T4) của $A_\circ$ (01.6 có). | Một câu: $\hat r$ đo được theo $s$. |
| nhẹ | 01.8(a) | "$O(m)$ với bảng băm" là thời gian kì vọng. | "$O(m)$ kì vọng với bảng băm, hoặc $O(m\log m)$ bằng sắp xếp". |
| nhẹ | 01.8(c) | Bước lấy kì vọng ngầm dùng $\mathbb E\binom N2=\sum_{j<k}\Pr(E_j\cap E_k)$. | Thêm nửa câu nêu $\mathbb EN=\sum_j\Pr(E_j)$ và $\mathbb E\binom N2=\sum_{j<k}\Pr(E_j\cap E_k)$. |
| nhẹ | Tiêu đề 01.6–01.11 | Tệp bài tập chỉ ghi "(UML Bài tập x.y)", §10 của ghi chú có thêm tên mô tả. | Thống nhất tiêu đề giữa hai tệp. |

Danh sách kiểm tra số (đều OK): 01.1 ngưỡng 4/5; 01.2 mọi bảng ($c_0$, $c_1$, $E$, $L_S$, $a$, $b$, $L_D$, Bayes 0,25 và 0,37, $L^c_D$, lỗi có trọng số, rủi ro vượt mức 0,04/0,20/0,12/0,14, bảng (d)); 01.3 ($\mathbb E L_D$, $\mathbb E L_S$ của $A_1$, $A_2$, liệt kê $m=1,2,3$); 01.4 ($0{,}3$; $\tfrac12+2^{-(m+1)}$); 01.5; 01.7 ($M'=1005$, $8$); 01.8 (30, $0{,}9^{30}$, $e^{-3}$, Bonferroni $0{,}2437$, đầy đủ $0{,}24412$, $m\ge44$); 01.9 ($0{,}9^{29}$, $0{,}9^{28}$, $0{,}899^{28}$, $e^{-2{,}9}$); 01.10 ($0{,}9^m$); 01.11 ($\eta_0$, khoảng cách $\ge1/10$).
