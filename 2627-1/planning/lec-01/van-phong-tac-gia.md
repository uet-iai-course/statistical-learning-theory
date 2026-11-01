# Văn phong của tác giả: phân tích bản sửa Bài 01, phần mở đầu đến hết §4

Nguồn: `git diff HEAD -- 2627-1/materials/lec-01/lecture-note.md` (bản sửa tay của tác giả, 2026-11-01), so với bản HEAD `70f9c7b` do tác tử viết. Tệp này dùng làm chuẩn để sửa §5–§12 và Phụ lục của Bài 01, và về sau cho các bài khác. Các trích dẫn ghi dạng *HEAD → bản sửa*.

## 1. Bố cục: tách ý thành danh sách và công thức hiển thị

Tác giả tách thành danh sách những ý *song song* (các đối tượng, các phần tử dữ liệu, các trường hợp, các ví dụ). Chuỗi lập luận nhân quả ("Vì … nên … Do đó …") vẫn được giữ thành đoạn văn (xem đoạn sau Định nghĩa 01.4, đoạn cuối §4).

- **Liệt kê thay cho chuỗi "Thứ nhất… Thứ hai… Thứ ba…".** Đoạn mở bài với ba đối tượng (rủi ro, ERM, PAC) thành ba gạch đầu dòng; "hai loại lỗi" FN/FP thành hai gạch; ví dụ các hàm lỗi sau Định nghĩa 01.1 thành danh sách mở bằng "Ví dụ:"; phần "Đầu vào và nhãn" của Ví dụ 01.1 thành ba gạch.
- **Dữ liệu cụ thể viết ra từng phần tử.** Tập huấn luyện của câu hỏi mở đầu được liệt kê $(x_1,y_1)=(1,0)$, …; hai hàm phân lớp viết thành $h_1(x)=\mathbb 1[x\ge3]$, $h_2(x)=\mathbb 1[x\ge4]$ thay cho lời mô tả.
- **Công thức thay cho lời.** Tác giả thêm công thức ở mọi chỗ HEAD chỉ nói bằng lời: $L_D(h)=\mathbb E_D[\ell(h,Z)]$ hiển thị ngay ở §1 mục 7; $D(x,y)=D_{\mathcal X}(x)D(y\mid x)$; dạng Bernoulli $D_\eta(y\mid x)=\eta(x)^y(1-\eta(x))^{1-y}$; dạng phân trường hợp của $D_f(y\mid x)$; công thức $P(Y\ne h_t(X)\mid X=x)$ theo hai trường hợp trong Ví dụ 01.2; $\hat t=\hat t(S)$ trong Ví dụ 01.4; $D(Y=f(x)\mid X=x)=1$ cho trường hợp nhãn tất định.
- **Công thức một dòng khi vừa.** HEAD ngắt `&L_D(h_w)\\ &\quad\le …` thành hai dòng; tác giả viết lại trên một dòng (`L_D(h_w)\le …`, `L_{D_\eta}(h_t) &=0{,}2\Big[…`). Chỉ ngắt khi công thức thật sự dài.
- **Bỏ bớt nhãn bước thừa.** Trong Ví dụ 01.3, nhãn "**Lấy kì vọng.**" và "**Kết luận.**" bị bỏ, hai bước nối thành mạch văn; nhãn "**Chặn hàm lỗi trên từng quan sát.**" đổi thành "**Rủi ro bị chặn.**" (gọi tên kết quả, không mô tả thao tác). Nhãn bước vẫn giữ khi ví dụ có nhiều phép tính độc lập (Ví dụ 01.2, 01.4).
- **Câu hỏi cho người học.** Tác giả thêm "**Câu hỏi.** Tại sao không nên đo chất lượng của hàm dự đoán trên tập huấn luyện?" ngay sau Định nghĩa 01.1, và viết câu hỏi mở đầu thành câu hỏi mở "Hiệu quả của hai hàm phân lớp này như thế nào?" thay cho câu hỏi đã gợi sẵn đáp án ("Vì sao có thể chỉ một trong hai…"). Câu hỏi chính của Học thống kê ở cuối Định nghĩa 01.5 cũng thành danh sách câu hỏi.
- **In đậm ý then chốt, in nghiêng thuật ngữ mới.** **học có nghĩa là gì**, **tối thiểu hóa rủi ro kì vọng**; *quan sát*, *hàm dự đoán*, *tập huấn luyện*, *ước lượng không chệch*, *hàm lỗi có trọng số* ở lần đầu xuất hiện.

## 2. Lựa chọn nội dung: những gì tác giả bỏ

Tác giả bỏ mọi câu không phục vụ trực tiếp mạch chính. Các loại đã bỏ:

1. **Câu rào đón về số liệu.** "các số này chỉ để minh họa", "Phân bố là giá trị giả định để minh họa, không phải số liệu lâm sàng", "Chi phí này cũng là giá trị giả định".
2. **Câu điều hướng, báo trước hoặc dẫn mục.** "Các khái niệm từ §4 đến §8 được tính trên ví dụ này…", "rủi ro kì vọng được định nghĩa chính xác ở §4, quy tắc Bayes ở §7", "Các giả thiết còn lại được nêu ở chỗ chúng được dùng lần đầu. Tính đo được… nằm ở §4. Giả thiết tối ưu nằm ở §5…", "Ba câu hỏi này được trả lời ở §6 và §7; từ đây ta gọi tắt…", "như dòng thứ hai của bảng ở §1", "Hai giả thiết… được dẫn bằng nhãn trong dòng **Giả thiết.**…".
3. **Lời bình về chi tiết kĩ thuật lý thuyết độ đo** (định nghĩa σ-đại số, hàm đo được, điều kiện đo được trong định nghĩa thì giữ). "Khi $\mathcal X$, $\mathcal Y$ hữu hạn và mọi tập con được coi là đo được… điều kiện kỹ thuật", "Điều kiện đo được chỉ để $L_D(A(S))$ là một biến ngẫu nhiên, và tự thỏa khi … (Phụ lục A)", định nghĩa nguyên tử và phân bố không có nguyên tử ở phần tiên quyết, "một số trong $[0,\infty]$".
4. **Nhận xét bên lề, không dùng lại.** Đoạn "giá trị dự đoán dương không phải một rủi ro" (dẫn Phụ lục C.4); câu về hàm lỗi log và Bài 02 trong Nhận xét 01.2; "Mẫu là một dãy, nên một quan sát có thể lặp lại"; "Mọi thuật toán học trong bài là tất định"; "thời gian tính chưa được xét"; rủi ro Bayes như đối tượng so sánh thứ hai ở §1 (được giới thiệu khi cần, ở §7); "Chưa cần bất đẳng thức tập trung".
5. **Chú thích phạm vi dùng của tiên quyết.** "(chỉ dùng trong chứng minh ở Phụ lục B)", "(chỉ dùng trong bài tập)", "tính tuyến tính đúng cho mọi tổng hữu hạn biến ngẫu nhiên khả tích, không cần độc lập".
6. **Câu nói hiển nhiên về tính ngẫu nhiên.** "Không có mẫu, nên mọi đại lượng đều cố định" (Ví dụ 01.2, 01.3), "Vì thuật toán tất định, nguồn ngẫu nhiên duy nhất là mẫu".
7. **Đoạn tự hỏi tự đáp.** "Hai hàm có tốt như nhau vì đều phân lớp hoàn hảo trên mẫu huấn luyện không? Không: …" cùng ví dụ cực đoan về hàm ghi nhớ ngay trong câu hỏi mở đầu (để dành cho §5).
8. **Mục tiêu học tập gọn hơn.** Bỏ "với đúng thứ tự lượng từ; phân biệt tham số độ chính xác với xác suất thất bại" và "chỉ ra bước hỏng khi giả thuyết được chọn theo mẫu".

Tác giả **không** bỏ khối đánh số nào (Định nghĩa 01.1–01.5, Nhận xét 01.2, Ví dụ 01.1–01.4 còn đủ) và **không** đổi con số nào. Các câu bị bỏ là câu trong mạch văn và nhận xét phụ bên trong khối.

## 3. Những gì tác giả thêm

- **Ý nghĩa thực hành nối với học máy hiện đại.** Dòng mới trong bảng nguồn ngẫu nhiên ở §1: thuật toán có thể sinh đại lượng ngẫu nhiên $\xi$ (lấy mẫu mini-batch), $A(S;\xi)$, $L_D(A(S;\xi))$.
- **Cách viết xác suất có điều kiện tường minh.** $D(Y=y\mid X=x)>0$, $D(y\mid x)$, hai phiên bản của phân bố nhãn.
- **Lời giải thích trực giác ngắn trước định nghĩa.** "Chất lượng của một hàm dự đoán $h$ phải được đo trên quan sát mới lấy mẫu từ $D$." (một câu, thay cho ba câu ở HEAD).
- **Câu tóm lại.** "Tóm lại, mục tiêu là **tối thiểu hóa rủi ro kì vọng** trên $\mathcal H$ khi không tính được $L_D$."
- **Nhiều tên tiếng Anh khi có nhiều tên thông dụng.** (population risk, expected risk), (labeling function, target function), viết tắt FN, FP.

## 4. Câu chữ và giọng văn

- **Chủ ngữ là người làm hoặc đối tượng toán học, động từ trực tiếp.** "Thuật toán học không được phép biết phân bố $D(z)$ hay $D(y\mid x)$ mà chỉ được sử dụng tập huấn luyện $S$" thay cho "Thuật toán học chỉ thấy mẫu $S$, không thấy $D$, …"; "Đầu vào của thuật toán học không phải là phân bố $D$ mà là tập huấn luyện" thay cho "Thuật toán học không nhận $D$".
- **Giải thích bằng ngôn ngữ thường của người dạy.** "luôn báo dương tính với mọi người", "luôn báo âm tính" thay cho "không báo ai"; "mỗi lần rút không ra số 3" thay cho "tránh số 3"; "nếu chỉ nhìn vào tập huấn luyện, ta không biết nên lựa chọn hàm nào trong $\{h_3,h_4\}$".
- **Từ nối giải thích.** "Nghĩa là", "Ví dụ:", "Tương tự,", "Để cho gọn,", "Do đó,", "Tóm lại,", "Trong trường hợp này,", "Nói chung,".
- **Câu dài hơn một chút nhưng một ý.** Tác giả chấp nhận câu dài nếu nó giải thích đủ điều kiện ("…nhỏ nhất có thể mà không biết $D$"), thay vì cắt thành nhiều câu cụt kiểu HEAD ("Thuật toán học không nhận $D$. Điều kiện đo được chỉ để…").
- **Gọi tên ngành.** "Học thống kê" (viết hoa) như tên một ngành: "ba đối tượng chính của Học thống kê", "Câu hỏi chính của Học thống kê là".

## 5. Thuật ngữ tác giả đổi

| HEAD (tác tử) | Bản sửa (tác giả) | Ghi chú cho phần còn lại |
|---|---|---|
| mẫu huấn luyện, mẫu | **tập huấn luyện**, tập mẫu quan sát | đổi khi chỉ dữ liệu huấn luyện; giữ "cỡ mẫu", "lấy mẫu", "mẫu $S_f$" khi gọi tên mẫu cụ thể |
| khả thực (realizable) | **khả diễn** | đổi toàn bộ §6–§12, Phụ lục |
| bất khả tri (agnostic) | **bất khả diễn** | "học PAC bất khả diễn" |
| hàm chỉ thị | **hàm chỉ báo** | |
| phân bố đồng thời | **phân bố liên hợp** | |
| bản có nhiễu / bản nhãn tất định | dữ liệu có nhiễu / dữ liệu tất định; trường hợp nhãn tất định | |
| rút từ $D$ | lấy mẫu từ $D$ (một chỗ; chỗ khác vẫn giữ "rút từ") | không bắt buộc |
| trước khi phát biểu bất kì cận nào | … bất kì mệnh đề nào | |
| điều kiện mô-men | điều kiện tồn tại mô-men bậc 2 | |
| đối tượng so sánh (comparator) | mục 7 §1 chỉ còn "Mục tiêu" | khái niệm vẫn dùng ở §7 |

## 6. Điểm trình bày không đưa vào chuẩn (chờ tác giả quyết)

Các điểm sau trong bản sửa có thể là thói quen gõ hoặc lỗi gõ; phần còn lại **không** bắt chước, và chúng được báo lại cho tác giả thay vì tự sửa trong §0–§4.

- Dấu cách trước dấu hỏi ("học có nghĩa là gì ?", "như thế nào ?", "nhỏ đến đâu ?"). Chính tả tiếng Việt không đặt dấu cách ở đây.
- `$D_{\mathcal X}$(x)` trong bảng kí hiệu §2: chữ (x) nằm ngoài công thức.
- `$\ell_{0–1}$` (gạch nối dài) ở sau Định nghĩa 01.1, trong khi chỗ khác viết `\ell_{0\text{-}1}`.
- "phân phối của tập mẫu quan sát" ở đoạn mở bài, trong khi toàn bài dùng "phân bố".
- `$s\sim D^m$` (chữ thường) sau Định nghĩa 01.4, trong khi biến ngẫu nhiên là $S$.
- "nên lựa chọn về hàm nào" (thừa "về") ở Ví dụ 01.4.
- §1 mục 2: dòng "Trường hợp có *hàm gán nhãn* …" bắt đầu bằng chữ hoa sau dấu chấm phẩy, thụt hai dấu cách nên hiển thị nối liền mục 2.
- Định nghĩa 01.5 vẫn ghi "**Mẫu huấn luyện.**" trong khi §1 mục 3 đã đổi thành "Tập huấn luyện".
- Câu hỏi mở đầu gọi tập huấn luyện là $D$, trùng kí hiệu phân bố $D$ dùng trong toàn bài (bài dùng $S$).
- Câu hỏi mở đầu gọi hai hàm là $h_1$, $h_2$, trong khi ở lớp hàm ngưỡng (Ví dụ 01.1) $h_1\equiv1$ và hai hàm này là $h_3$, $h_4$.
- `D(y|x)`, `P(Y=1|X=x)` dùng `|` và `P` trong khi chỗ khác dùng `\mid` và `\Pr`.
- "phân bố liên hợp" chưa kèm tiếng Anh (joint distribution); trong thống kê Bayes "liên hợp" còn dùng cho *conjugate* (phân bố tiên nghiệm liên hợp).

## 6a. Bổ sung từ lần sửa thứ hai của tác giả (trên bản §5–hết đã viết lại, 2026-11-01)

- **Công thức ngay tại chỗ được gọi tên.** Định nghĩa 01.18, 01.25: "sao cho bất đẳng thức $$\Pr_{S\sim D^m}[\ldots]\ge1-\delta$$ đúng với mọi lựa chọn của ba thành phần sau", thay cho "bất đẳng thức dưới đây … Bất đẳng thức đó là".
- **Giải thích bằng cách hiểu tích cực, cụ thể, thay cho liệt kê điều "không phải".** Nhận xét 01.19: bỏ hai câu "không phải xác suất hậu nghiệm…, cũng không phải xác suất chẩn đoán…", thay bằng "có thể hiểu theo nghĩa: trong 100 lần huấn luyện, thì có khoảng 95 lần tìm được giả thuyết $A(S)$ có rủi ro nhiều nhất là $\epsilon$".
- **Bỏ câu nhắc lại kết quả đã có.** Cuối §7: bỏ "Ứng viên tự nhiên là ERM, nhưng … (Mệnh đề 01.15(b))".
- **Gọi đủ tên thuật ngữ** ("lớp giả thuyết", không "lớp") và in đậm khái niệm then chốt (**quá khớp**).

## 7. Quy tắc rút ra cho người sửa §5–§12 và Phụ lục

1. Mỗi đoạn một ý. Từ ba ý song song trở lên thì dùng danh sách; dữ liệu và hàm cụ thể viết ra bằng công thức.
2. Viết công thức cho mọi đại lượng được mô tả bằng lời khi công thức ngắn hơn hoặc rõ hơn; công thức một dòng khi vừa khung.
3. Bỏ câu rào đón, câu điều hướng ("ở §…", "Phụ lục … chứng minh"), câu nói hiển nhiên về tính ngẫu nhiên, câu tự hỏi tự đáp, chi tiết đo được không dùng cho mạch chính, nhận xét bên lề không được dùng lại. Chỉ giữ một dẫn chiếu khi người đọc thật sự cần mở nơi được dẫn (ví dụ dẫn một định nghĩa hay ví dụ đã có số để lấy con số).
4. Không xóa khối đánh số (bài tập dẫn số của chúng); rút gọn nội dung bên trong. Đề xuất xóa cả khối thì ghi vào báo cáo, không tự xóa.
5. Không đổi con số, giả thiết hay bảo đảm của kết quả; có thể diễn đạt lại.
6. Dùng thuật ngữ ở §5 của tệp này. Thêm "**Câu hỏi.**" cho người học ở chỗ có hiểu lầm hay gặp, không quá một câu hỏi cho mỗi mục. Câu hỏi của tác giả đôi khi gợi hướng ("Tại sao không nên…"); khi tác tử viết thì nên đặt câu hỏi trung tính và trả lời ngay trong đoạn sau, rồi nối lại nếu câu trả lời nằm xa.
9. Công thức gộp một dòng có thể cuộn ngang ở 390 px; tác giả quyết định giữa "một dòng" và "ngắt dòng cho điện thoại" (câu hỏi mở, 2026-11-01).
7. Giọng: chủ ngữ là thuật toán, hàm, người học ("ta"), động từ trực tiếp; từ nối giải thích ("Nghĩa là", "Do đó", "Tóm lại"); in nghiêng thuật ngữ mới, in đậm ý then chốt (dùng tiết kiệm).
8. Các quy tắc của học phần vẫn đứng trên: định nghĩa trước khi dùng (`forward_refs.py` báo 0), dòng **Giả thiết.**/**Bảo đảm.** cho mọi kết quả, ví dụ từng bước (`van-phong.md` §7a), `no-ai-slop`.
