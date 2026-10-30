# Bài 01: rà các khối hình thức

Yêu cầu của người dùng (2026-10-30), theo thứ tự nhận:

1. "Viết lại định nghĩa 01.5 sao cho gãy gọn hơn, các giả thiết cần liệt kê (gạch đầu dòng) thay vì viết trong đoạn văn rất khó theo dõi." (đã làm)
2. "Gạch đầu dòng 'chọn trước khi lấy mẫu' không song song với các gạch đầu dòng khác." (đã làm)
3. "Sau khi sửa hãy rà lại các phát biểu định nghĩa, định lý khác." (tệp này; vòng 1 ở §1–§3, vòng 2 ở §4)

Mẫu cần theo: khối Định nghĩa 01.5 hiện tại. Một câu dẫn ngắn, rồi danh sách gạch đầu dòng; mỗi nhãn in đậm là tên một thành phần (cụm danh từ), kết thúc bằng dấu chấm; mọi dòng cùng khuôn nội dung (kí hiệu, mô tả, vai trò); công thức nằm trong dòng liên quan. Quy định: `van-phong.md` §3a, §9a; `thuat-ngu.md`; `ky-hieu.md`. Các kết quả giữ hai dòng "**Giả thiết.**" và "**Bảo đảm.**"; khi một dòng có từ ba ý trở lên, các ý thành danh sách song song có nhãn ngay dưới dòng đó. Các phần (a)(b)(c) của bảo đảm giữ nhãn cũ (được dẫn ở chỗ khác là 01.15(a), 01.23(b), …), mỗi phần một câu.

Nội dung toán giữ nguyên: cùng giả thiết, cùng lượng từ và thứ tự lượng từ, cùng bất đẳng thức, hằng số và tham chiếu; số và tên khối không đổi.

## 1. Kiểm kê

Có 30 khối được đánh số (16 định nghĩa, 3 mệnh đề, 1 hệ quả, 1 thuật toán, 9 nhận xét). Phụ lục không có khối kết quả riêng, chỉ có chứng minh của Mệnh đề 01.23.

| Khối | Vấn đề | Thay đổi |
|---|---|---|
| Định nghĩa 01.1 (Hàm lỗi và rủi ro kì vọng) | không | giữ nguyên: gọn |
| Nhận xét 01.2 (Tính khả tích) | không | giữ nguyên: thẳng |
| Định nghĩa 01.3 (Phân bố có rủi ro hữu hạn) | không | giữ nguyên: một câu |
| Định nghĩa 01.4 (Thuật toán học) | không | giữ nguyên: gọn |
| Định nghĩa 01.5 (Bài toán học thống kê) | là mẫu | giữ nguyên: mẫu |
| Định nghĩa 01.6 (Rủi ro thực nghiệm) | không | giữ nguyên: một công thức |
| Mệnh đề 01.7 (Tính không chệch) | "Giả thiết." dồn bốn ý vào một đoạn: mẫu (dạng yếu của (T1)), giả thuyết cố định, (T2), $L_D(h)<\infty$; nhãn "(T2)," đứng trơ đầu câu | "Giả thiết." thành danh sách bốn dòng: Mẫu huấn luyện, Giả thuyết được xét, Hàm lỗi, Rủi ro kì vọng. "Bảo đảm." giữ nguyên (một công thức và một câu) |
| Định nghĩa 01.8 (ERM) | lượng từ "với mọi $S$" đứng sau công thức; giả thiết "khác rỗng với mọi mẫu" chen giữa; khuôn câu khác Định nghĩa 01.12 | giữ dạng đoạn (ba khái niệm nối tiếp nhau, không phải ba thành phần song song); đưa "với mọi mẫu $S$" lên trước công thức hiển thị; câu thuật toán ERM cùng khuôn với Định nghĩa 01.12 |
| Nhận xét 01.9 (Giả thuyết chọn theo mẫu) | không | giữ nguyên: thẳng |
| Định nghĩa 01.10 (Khoảng cách tổng quát hóa) | không | giữ nguyên: một công thức |
| Nhận xét 01.11 (Sự tồn tại nghiệm ERM) | không | giữ nguyên: thẳng |
| Định nghĩa 01.12 (ERM xấp xỉ) | lượng từ "với mọi mẫu $S$" đứng sau công thức, tách thành một dòng riêng; câu dẫn không nêu $\mathcal H$, $\ell$ như Định nghĩa 01.8 | câu dẫn "Cho lớp giả thuyết $\mathcal H$, hàm lỗi $\ell$ và $\epsilon_{\mathrm{opt}}\ge0$"; "nếu với mọi mẫu $S$," đứng trước công thức, cùng khuôn với Định nghĩa 01.8 |
| Thuật toán 01.13 (ERM cho lớp hàm ngưỡng) | "Đầu vào." và "Đầu ra." mỗi dòng ba ý nối bằng dấu chấm phẩy, khuôn không song song (công thức; cụm danh từ; câu) | "Đầu vào." thành ba dòng: Mẫu, Lớp giả thuyết, Hàm lỗi; "Đầu ra." thành ba dòng: Rủi ro thực nghiệm, Tập nghiệm ERM, Một nghiệm ERM. Các nhãn khác giữ nguyên |
| Định nghĩa 01.14 (Thuật toán ghi nhớ) | hai trường hợp của hàm (điểm trong mẫu, điểm ngoài mẫu) dồn vào một câu có dấu chấm phẩy | hai trường hợp thành hai dòng: Điểm trong mẫu, Điểm ngoài mẫu |
| Mệnh đề 01.15 (Hàm phân lớp ghi nhớ) | "Giả thiết." sáu ý trong hai câu; "Bảo đảm." ba phần (a)(b)(c) nằm liền trong một đoạn, phần (a) gồm hai câu | "Giả thiết." thành năm dòng: Tập đầu vào, Phân bố dữ liệu, Lớp giả thuyết, Hàm lỗi, Thuật toán; cỡ mẫu chuyển sang câu dẫn của "Bảo đảm." ("đúng với mọi cỡ mẫu $m\ge1$ và mọi mẫu", theo `van-phong.md` §11); "Bảo đảm." thành danh sách (a)(b)(c), mỗi phần một câu |
| Định nghĩa 01.16 (Tính khả thực) | không | giữ nguyên: một câu |
| Nhận xét 01.17 (Khả thực là tính chất của cặp) | không | giữ nguyên: thẳng |
| Định nghĩa 01.18 (Học PAC khả thực) | ba lượng từ "với mọi" ($\epsilon,\delta$; $D$; $m$) chen giữa một câu dài trước công thức | ba lượng từ thành ba dòng: Tham số độ chính xác và xác suất thất bại, Phân bố dữ liệu, Cỡ mẫu; thứ tự giữ nguyên ($\exists M$ trước, rồi $\epsilon,\delta$, $D$, $m$); công thức sau danh sách |
| Nhận xét 01.19 (Độ tin cậy lấy theo mẫu) | không | giữ nguyên: thẳng |
| Định nghĩa 01.20 (Độ phức tạp mẫu) | hai đại lượng ($m_A$, $m_{\mathcal H}$) trong một đoạn dài; lượng từ "với mọi $D$ … và mọi $m\ge m_0$" chen giữa | hai dòng cùng khuôn "kí hiệu là …": Độ phức tạp mẫu của thuật toán, Độ phức tạp mẫu của lớp; công thức $m_{\mathcal H}$ nằm trong dòng thứ hai |
| Nhận xét 01.21 (Độ phức tạp mẫu của thuật toán và của lớp) | không | giữ nguyên: thẳng |
| Định nghĩa 01.22 (Rủi ro Bayes) | không | giữ nguyên: gọn |
| Mệnh đề 01.23 (Quy tắc Bayes) | "Giả thiết." năm ý trong một đoạn, "(T2)," đứng trơ đầu câu; "Bảo đảm." (b) gồm bốn câu, hai câu về tính duy nhất và một câu về loại bảo đảm lẫn vào (b) | "Giả thiết." thành năm dòng: Phân bố dữ liệu, Xác suất có điều kiện của nhãn 1, Hàm lỗi, Đối tượng so sánh, Mẫu huấn luyện; "Bảo đảm." thành danh sách (a)(b), mỗi phần một câu; các câu còn lại đứng sau danh sách, mở bằng câu gọi tên ngưỡng của từng phần (xem §3) |
| Định nghĩa 01.24 (Rủi ro vượt mức) | không | giữ nguyên: hai câu |
| Đoạn dẫn vào Định nghĩa 01.25 ("vì ba lý do") | (i) và (ii) chung một đoạn, (iii) tách đoạn; (iii) mở bằng "Vì vậy", tức là kết luận chứ không phải lý do | "vì hai lý do"; danh sách **(i)**, **(ii)**; (iii) thành đoạn kết không nhãn, mở bằng "Vì vậy …" |
| Định nghĩa 01.25 (Học PAC bất khả tri) | như Định nghĩa 01.18 | cùng cấu trúc với Định nghĩa 01.18: ba dòng Tham số độ chính xác và xác suất thất bại, Phân bố dữ liệu, Cỡ mẫu; chỉ khác dòng phân bố (rủi ro hữu hạn thay cho khả thực), hàm lỗi và biến cố; câu cuối "một thuật toán học PAC bất khả tri cho $\mathcal H$" thay cho "một thuật toán như vậy" |
| Nhận xét 01.26 (Cận dưới đúng) | không | giữ nguyên: thẳng |
| Nhận xét 01.27 (Học đúng lớp và học ngoài lớp) | không | giữ nguyên: thẳng |
| Định nghĩa 01.28 (Cận tổng quát hóa cho mọi thuật toán ERM) | lượng từ $\forall\hat A$ nằm trong câu, có mệnh đề chêm "tức với mọi quy tắc …" trước công thức; ba lượng từ còn lại ở dòng công thức | đưa $\forall\hat A$ vào dòng lượng từ (đứng đầu, đúng thứ tự cũ); câu "trong đó" sau công thức: "$\hat A$ là một thuật toán ERM bất kì trên $\mathcal H$ (…), còn $D$ là một phân bố bất kì trên $\mathcal X\times\mathcal Y$" |
| Hệ quả 01.29 (Rủi ro thực nghiệm nhỏ không đủ) | "Giả thiết." bảy ý trong ba câu, khuôn câu khác nhau ("với (T1): …", "(O1): …", "Phần (b) dùng …"); "Bảo đảm." (a)(b) liền một đoạn | "Giả thiết." thành tám dòng: Tập đầu vào, Phân bố dữ liệu, Lớp giả thuyết, Hàm lỗi, Mẫu huấn luyện, Thuật toán, Tính khả thực, Cận tổng quát hóa; các dòng Tập đầu vào, Phân bố dữ liệu, Lớp giả thuyết, Hàm lỗi chép theo Mệnh đề 01.15 (cùng thiết lập Ví dụ 01.8); dòng Phân bố dữ liệu ghi cả hai phần dùng $D$; dòng Thuật toán nêu riêng thuật toán của từng phần (xem §5); "Bảo đảm." thành danh sách (a)(b), câu về UML §5.1 đứng sau |
| Nhận xét 01.30 (Không có bữa trưa miễn phí) | không | giữ nguyên: thẳng |

Tổng: 30 khối; 12 khối sửa (01.7, 01.8, 01.12, 01.13, 01.14, 01.15, 01.18, 01.20, 01.23, 01.25, 01.28, 01.29) và một đoạn dẫn (trước 01.25); 18 khối giữ nguyên.

## 2. Nhãn dùng chung

Cùng một thành phần mang cùng một nhãn trong mọi khối:

| Thành phần | Nhãn | Khối |
|---|---|---|
| tập đầu vào | **Tập đầu vào.** | 01.15, 01.29 |
| phân bố | **Phân bố dữ liệu.** | 01.5, 01.15, 01.18, 01.23, 01.25, 01.29 |
| mẫu | **Mẫu huấn luyện.** (thuật toán: **Mẫu.**) | 01.5, 01.7, 01.23, 01.29; 01.13 |
| lớp | **Lớp giả thuyết.** | 01.13, 01.15, 01.29 |
| hàm lỗi | **Hàm lỗi.** | 01.7, 01.13, 01.15, 01.23, 01.29 |
| thuật toán | **Thuật toán.** | 01.15, 01.29 |
| $\epsilon,\delta$ | **Tham số độ chính xác và xác suất thất bại.** (theo `thuat-ngu.md` dòng 109–110 và `ky-hieu.md` dòng 18) | 01.18, 01.25 |
| $m$ | **Cỡ mẫu.** | 01.18, 01.25 (ở 01.15, cỡ mẫu nằm trong câu dẫn của "Bảo đảm.") |

Giữ dạng đoạn cho Định nghĩa 01.8 và 01.12: ba khái niệm của 01.8 nối tiếp nhau (tập nghiệm, phần tử, thuật toán), và 01.12 chỉ có một khái niệm; danh sách sẽ phải lặp lại tên khái niệm vừa in nghiêng. Hai định nghĩa dùng chung câu "Một thuật toán học $A$ được gọi là … trên $\mathcal H$ nếu với mọi mẫu $S$," rồi công thức hiển thị.

## 3. Điểm mở của vòng 1 (đã giải quyết ở vòng 2)

- Mệnh đề 01.23: hai câu về tính duy nhất ("Nói chung hàm tối ưu không duy nhất. Khi $\eta(X)$ bằng ngưỡng …") trước đây nằm trong phần (b), sau vòng 1 đứng sau danh sách (a)(b), nên được đọc là áp dụng cho cả hai phần. Người điều phối chỉ ra thêm hai lỗi: chữ "ngưỡng" chưa được gọi tên trước câu đó, và cụm "như dưới $D_\eta$" không đúng cho (b) với mọi chi phí (với $(c_{FP},c_{FN})=(1,3)$, ngưỡng $\tfrac14=\eta(2)$).
- **Cách giải quyết.** Câu đầu sau danh sách gọi tên ngưỡng của từng phần: "Ngưỡng trên $\eta(x)$ là $\tfrac12$ trong (a) và $c_{FP}/(c_{FP}+c_{FN})$ trong (b)." Câu về tính duy nhất giữ nguyên nội dung, nay đúng cho cả hai phần vì ngưỡng đã gọi tên riêng. Câu ví dụ chỉ khẳng định cho $D_\eta$ với $\ell_{0\text{-}1}$ (ngưỡng $\tfrac12$) và với $\ell_c$ khi $(c_{FP},c_{FN})=(1,4)$ (ngưỡng $\tfrac15$); các giá trị $\eta=(0,\tfrac14,\tfrac34,\tfrac25,1)$ không trùng hai ngưỡng này. Câu "Bảo đảm là về đại lượng tổng thể." giữ nguyên ở cuối.

## 4. Vòng 2

Góp ý của người điều phối sau vòng 1, tất cả đã sửa trong ghi chú:

1. Mệnh đề 01.23: gọi tên ngưỡng của từng phần; câu ví dụ giới hạn ở $\ell_{0\text{-}1}$ và $\ell_c$ với $(c_{FP},c_{FN})=(1,4)$ (§3).
2. Đoạn trước Định nghĩa 01.25: "vì hai lý do", danh sách **(i)**, **(ii)**, rồi đoạn kết "Vì vậy …" không nhãn.
3. Công thức của Định nghĩa 01.18 gộp thành một dòng. Ở 01.25, công thức một dòng rộng 376 px và cách ngắt sau $\big]$ rộng 303 px, trong khi khung ở 390 px rộng 270 px, nên công thức ngắt trước dấu $\le$ (vừa 270 px); người điều phối đồng ý.
4. Định nghĩa 01.18 và 01.25: nhãn "Tham số độ chính xác và xác suất thất bại." thay cho "Sai số và xác suất thất bại.", khớp `thuat-ngu.md` và đoạn ngay sau 01.18.
5. Mệnh đề 01.15: bỏ dòng "Cỡ mẫu" khỏi "Giả thiết."; câu dẫn "Năm thành phần sau, gồm thiết lập của Ví dụ 01.8 cùng thuật toán ghi nhớ."; "Bảo đảm." mở bằng "Ba khẳng định sau là tất định, đúng với mọi cỡ mẫu $m\ge1$ và mọi mẫu."
6. Hệ quả 01.29: thêm dòng "Phân bố dữ liệu." (viết lại sau khi người điều phối duyệt vòng 2, vì bản đầu hàm ý phần (a) không dùng $D$: "Phần (b) xét $D$ này. Phần (a) dùng $D$ làm phản ví dụ: $\beta$ phải đúng với mọi phân bố (Định nghĩa 01.28), nên phải đúng với $D$.", khớp Bước 1 của chứng minh, nơi Mệnh đề 01.15(a)(b) dưới $D$ cho khoảng cách tổng quát hóa bằng $1$); dòng "Thuật toán." mở bằng $\hat A$; "Tập đầu vào." và "Hàm lỗi." chép đúng 01.15; câu dẫn "Tám thành phần sau, …".
7. Định nghĩa 01.20: dòng thứ hai theo khuôn dòng thứ nhất ("$m_{\mathcal H}(\epsilon,\delta)$ là giá trị nhỏ nhất của …"); câu dẫn tách đôi, bỏ hai chữ "và" liên tiếp.
8. Định nghĩa 01.14: nhãn "Điểm trong mẫu." thay cho "Điểm của mẫu.".
9. Định nghĩa 01.28: câu "trong đó" rút gọn ("$\hat A$ là một thuật toán ERM bất kì trên $\mathcal H$ (…), còn $D$ là một phân bố bất kì trên $\mathcal X\times\mathcal Y$"); dòng lượng từ và miền của $D$ giữ nguyên.

## 5. Vòng 3

Góp ý của người điều phối sau vòng 2, tất cả đã sửa trong ghi chú:

1. Hệ quả 01.29, dòng "Phân bố dữ liệu." rút về một câu: "$D$, phân bố của $(X,1)$ với $X\sim U[0,1]$; cả hai phần đều dùng $D$ này." Ý phản ví dụ chuyển vào câu thứ hai của Bước 1 trong chứng minh, nêu cả cặp: "Cặp $(A_{\mathrm{gn}},D)$ là phản ví dụ: bất đẳng thức của Định nghĩa 01.28 phải đúng với mọi thuật toán ERM và mọi phân bố, nên phải đúng với $\hat A=A_{\mathrm{gn}}$ và $D$." Bản vòng 2 bỏ qua $A_{\mathrm{gn}}$ và lấy $\beta$ làm chủ ngữ của "đúng".
2. Hệ quả 01.29, dòng "Thuật toán.": "Thuật toán ERM chính xác theo (O1), thỏa điều kiện đo được của Định nghĩa 01.4: $\hat A$ bất kì trong Định nghĩa 01.28 ở phần (a), $A_{\mathrm{gn}}$ (Mệnh đề 01.15(a)) ở phần (b)." Bản vòng 2 gợi ý sai rằng (b) đúng cho một thuật toán ERM bất kì; thuật toán ERM trả về $h_{\equiv1}$ là thuật toán học PAC trên $D$.
3. Tên của $\epsilon$: §6 (câu "Bảo đảm cũng phải cho phép …") nay gọi $\epsilon$ là "tham số độ chính xác (accuracy parameter)" ngay lần đầu, thay cho "sai số"; đoạn sau Định nghĩa 01.18 bỏ cụm tiếng Anh lặp lại. Nhãn ở 01.18 và 01.25 vì vậy dùng một thuật ngữ đã nêu trước đó.
4. Mệnh đề 01.23: đoạn sau danh sách (a)(b) tách đôi. Đoạn 1 gồm câu ngưỡng và câu về tính duy nhất; đoạn 2 gồm ví dụ $D_\eta$ và "Bảo đảm là về đại lượng tổng thể."
5. Định nghĩa 01.28: ngoặc trong câu "trong đó" viết thành "(ứng với một quy tắc chọn khi bằng nhau bất kì thỏa điều kiện đo được của Định nghĩa 01.4)".
6. Thêm (tự phát hiện khi chụp ở 390 px): công thức hiển thị trong phần (a) của Mệnh đề 01.23 nằm trong gạch đầu dòng từ vòng 1, nên khung hẹp hơn (230 px) và dòng "$=\mathbb E\min\{\eta(X),1-\eta(X)\}$" rộng 261 px bị cuộn ngang. Dòng đó ngắt sau dấu phẩy thành "$=\mathbb E\min\{\eta(X),$" và "$1-\eta(X)\}.$"; nội dung không đổi. Công thức hiển thị duy nhất còn cuộn ngang ở 390 px là một dòng trong chứng minh Mệnh đề 01.23 ở Phụ lục B (271 so với 286 px), có từ trước các vòng này và không thuộc phạm vi.

Không sửa: cách ngắt công thức của Định nghĩa 01.25.

## 6. Vòng 4

1. §6, câu về $\epsilon$. Chưa có chỗ nào trong §6 gọi một "mức mục tiêu", nên câu không dùng cụm đó. Đoạn mở §6 đã nêu hiệu $L_D(A(S))-\inf_{h\in\mathcal H}L_D(h)$ của Định nghĩa 01.5, nên câu gọi thẳng hiệu đó: "Bảo đảm cũng phải cho phép hiệu $L_D(A(S))-\inf_{h\in\mathcal H}L_D(h)$ đạt tới một lượng $\epsilon>0$, gọi là tham số độ chính xác (accuracy parameter)." Bảo đảm cho phép một sai lệch, và $\epsilon$ là độ lớn của sai lệch đó; trong trường hợp khả thực, $\inf=0$ và câu khớp biến cố $L_D(A(S))\le\epsilon$ của Định nghĩa 01.18.
2. Phụ lục B, Bước 1 của chứng minh Mệnh đề 01.23: công thức hiển thị rộng 286 px so với khung 271 px ở 390 px. Hai tích $\mathbb 1[g(X)=0]\,\Pr(Y=1\mid X)$ và $\mathbb 1[g(X)=1]\,\Pr(Y=0\mid X)$ ngắt thành hai dòng, thừa số thứ hai viết $\cdot\Pr(\cdots)$ ở dòng sau; nội dung không đổi. Đã thử các cách giữ nguyên mỗi tích trên một dòng (thụt "$\;$" thay cho "$\quad$": 272 px; chỉ ngắt tích thứ hai: vừa đúng 271 px, không còn lề); cách được chọn cho 257 px. Sau khi sửa, cả 41 công thức hiển thị của ghi chú (đã mở mọi khối thu gọn) không còn cuộn ngang ở 390 px, qua HTTP và `file://`.

## 7. Vòng 5

1. §6, câu về $\epsilon$: "Trên các mẫu còn lại, bảo đảm chỉ đòi hiệu $L_D(A(S))-\inf_{h\in\mathcal H}L_D(h)$ không vượt quá một lượng $\epsilon>0$, gọi là tham số độ chính xác (accuracy parameter)." Bản vòng 4 ("đạt tới một lượng $\epsilon$") dễ đọc thành hiệu chạm $\epsilon$. Cụm "Trên các mẫu còn lại" nối với câu trước (bảo đảm phải cho phép thất bại với xác suất $\delta$ theo mẫu).
2. Mệnh đề 01.23, sau danh sách (a)(b): đoạn 1 gồm câu ngưỡng, câu về tính duy nhất và câu ví dụ $D_\eta$ (để "điều kiện này" trỏ về câu ngay trước trong cùng đoạn); đoạn 2 chỉ còn "Bảo đảm là về đại lượng tổng thể."
3. Mục tiêu học tập 4: "phân biệt tham số độ chính xác với xác suất thất bại", thay cho "… với tham số độ tin cậy", theo `thuat-ngu.md` (độ tin cậy là $1-\delta$, xác suất thất bại là $\delta$). Danh sách mục tiêu không dùng kí hiệu, nên câu không kèm $\epsilon$, $\delta$.

Không sửa: các chỗ ngắt dòng công thức (01.23(a), Phụ lục B, 01.25) và câu "Cặp $(A_{\mathrm{gn}},D)$ là phản ví dụ".
