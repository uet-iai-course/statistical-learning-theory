# Bài tập Bài 09 — Rà soát toán học (người rà 2)

Đối tượng: `lec09-ex-frozen.md` (992 dòng, 9 927 tiếng theo `wc -w`; trùng byte với `2627-1/materials/lec-09/exercises.md`, đã kiểm bằng `cmp`). Căn cứ đã đọc:

- ghi chú đã duyệt và Bài 02, 05 (Định lý 02.7, Định nghĩa 05.10, Mệnh đề 05.3(a), Thuật toán 05.11, Định lý 05.14, Hệ quả 05.15);
- UML tr. 356 (§24.8, bài 1–3);
- MLbookSol tr. 61–64 (chương 24);
- mục "Bài tập — quyết định" trong `review-log.md`.

Script tính lại ở `reviews09/r2/ex/`: `e6.py`, `e6b.py`, `e6c.py` (09.6) và `e79.py` (09.7, 09.9). Các script này nạp lại `exp_lec09_bigram.py`. Chỉ đọc repo, không commit.

## Tổng kết theo mức

| Mức | Số phát hiện |
|---|---|
| chặn bàn giao | 0 |
| nghiêm trọng | 0 |
| trung bình | 0 |
| nhẹ | 4 |

Tôi đã tự giải lại mọi bài và mọi ý. Mọi chứng minh đúng, mọi giả thiết đã nêu là đủ, và mọi số khớp. Riêng hai tỉ số ở 09.6(a) Bước 1 làm tròn sai (F1). Ba phát hiện nhẹ còn lại thuộc về cách phát biểu.

Bốn điểm được giao kiểm riêng:
- **Bài 09.7.** Kết quả đúng: thác triển lồi, quy ước $\varphi=0$, (G1) tại mọi điểm của $W$, $G=2\sqrt3$, cận $\le0{,}0715$. Mô phỏng 20 hạt giống cho $0{,}000135$, khớp con số $0{,}00014$.
- **Bài 09.9.** Đúng; hai trường hợp cho cận $3\epsilon$ và $2\epsilon$.
- **Lời giải UML.** Không chép bản lời giải. 09.9(c) dùng cách chia trường hợp khác bản lời giải ($2\epsilon_m$ thay cho $\sqrt\epsilon$) và cho tốc độ $\ln m/\sqrt m$ thay cho $\tilde O(m^{-1/4})$. 09.8(b) dùng phép tách tổng bình phương, không khai triển $\mathbb E[x_ix_j]$.
- **Đề UML.** Đề trung thành với PDF. 09.10(c) còn sửa một chỗ hổng của UML: khi có $\nu_y=0$ thì bài toán với ràng buộc $c_y>0$ không có nghiệm.

## Từng bài

| Bài | Đánh giá | Ghi chú kiểm |
|---|---|---|
| 09.1 | ✓ | (a) $0{,}02$, $\ln50$, độ bối rối $2{,}6591$; $0{,}128$, $2{,}0557$, $1{,}6719$. (c) $0{,}40$ và $0{,}69$. (d) $27/12\,800$; phân bố hình học với tham số $\tfrac14$; $\mathbb En=4$; phép kiểm $27/256$. Lập luận dùng Mệnh đề 09.3(c) cho mỗi độ dài cố định là đúng. |
| 09.2 | ✓ | (a) Có $k+1$ cửa sổ; hai cửa sổ rời nhau khi và chỉ khi $i'-i\ge k+1$. (b)(i) Ngữ cảnh của $u_{j+r}$ chứa $x_j$ ở vị trí $k-r+1$. Mọi khớp khác cần hai giá trị liên tục có chỉ số khác nhau bằng nhau, nên có xác suất $0$. (b)(ii) Với cách gán độc lập, $f^{k-1}$ đúng chính xác; với hoán vị thì là xấp xỉ, và đề có ghi điều này. (b)(iii) $5{,}12\cdot10^{-7}$; $0{,}25$. (c) Bỏ $u_{a-k},\ldots,u_{a-1}$ và $u_{b+1},\ldots,u_{b+k}$, còn $3972$ cửa sổ. (d) Kiểm đúng từng giả thiết. |
| 09.3 | ✓ | (a) Jensen: giá được dùng ở Bước 1, tính lõm ngặt ở Bước 3. (b) $1{,}0397$; $1{,}0986$; $0{,}0589$; chiều ngược $0{,}0566$. (c) $+\infty$; $\tfrac12\ln2=0{,}3466$. (d) $(b-1)\ln2$: $2{,}0794$; $4{,}8520$. |
| 09.4 | ✓ | (a) Chứng minh trực tiếp, điều kiện dấu bằng đúng. (b) $\varphi_0(1{,}5)=0{,}129518$, $\varphi_0(0{,}5)=0{,}352065$, $p=0{,}240792$, $\ln p=-1{,}42382$, hậu nghiệm $0{,}731059$. ELBO $-1{,}54394$ với khe $0{,}12012$; ELBO $-1{,}51199$ với khe $0{,}08817$; KL $=0{,}088184$. (c) ELBO $-1{,}73709$, khe $0{,}31326=-\ln0{,}731059$; trường hợp $v=3$ cho $-\infty$. |
| 09.5 | ✓ | (a) $\tfrac38$ và $\tfrac7{12}$; trọng số $\tfrac14$ và $\tfrac1{12}$. (b) Giả thiết đủ. (c) $c=\tfrac13$, $\tilde p=(\tfrac34,\tfrac14)$; giả thiết $\mathrm H(\tilde p)<\infty$ cần cho Mệnh đề 09.8 và đã nêu. (d) Đúng cả hai chiều. Phép kiểm với Ví dụ 09.6: $\tfrac16$ và $\tfrac12$. |
| 09.6 | ✓ (F1, F2, F3) | Mọi số trong đề khớp script (bảng ở dưới). Lập luận về sai số chuẩn theo hạt giống, so với hai nhóm độc lập, là đúng. $K_{\mathtt A}=0{,}039380$ và $\tfrac{199}{200}K_{\mathtt A}=0{,}039183$ khớp $0{,}0392$. **Về $c=0{,}087$:** con số này là giá trị nhỏ nhất của $10$ mô hình, chỉ phụ thuộc các mẫu huấn luyện, và các mẫu huấn luyện độc lập với từng mẫu kiểm tra. Mỗi mô hình có xác suất nhỏ nhất $\ge0{,}0872$, nên miền $[0,\ln(1/0{,}087)]$ chứa miền của nó. Cận Hoeffding $0{,}234496\le0{,}2345$ vì vậy hợp lệ khi lấy điều kiện theo mẫu huấn luyện. Lời giải (b), Bước 1 đã nói ý này. Một cận dưới không phụ thuộc dữ liệu cho làm trơn cộng một thì nhỏ hơn nhiều: $\ge1/(m+4)$ cho kí tự đầu và $\ge1/(199m+4)$ cho xác suất chuyển. Không bắt buộc ghi điều này. |
| 09.7 | ✓ | (a) $g'(\tfrac14)=-3{,}5$; $\tilde g$ thuộc lớp $C^1$ với đạo hàm không giảm, nên lồi; $\tilde F=F$ trên một lân cận của $W$. Định nghĩa 05.10 đòi $F:\mathbb R^p\to\mathbb R$ lồi và (G1), (G2) chỉ trên $W$, nên quy ước $\varphi=0$ khi $\sigma\le0$ hợp lệ (đo được); Thuật toán 05.11 chỉ gọi oracle tại $w_t\in W$. (b) Lân cận $U$ của Gợi ý 2 mở, nằm trong $\Phi$; các cận ở dòng 681–684 đúng; $\mathbb EM=2C_0$; theo Mệnh đề 05.3(a), $\nabla F=\nabla\tilde F\in\partial\tilde F$ trên $W$. (c) $\mathbb E\varphi_\sigma^2=b^2+3\sigma^2+e^2+2\sigma e$; tổng bằng $(5\mu^2-12\mu+8)+(7\sigma^2+1/\sigma^2-4)$ (Monte Carlo tại $(0{,}7;0{,}6)$: $3{,}3445$, so với $3{,}3478$); trên lưới, giá trị lớn nhất trên $W$ là $12$. (d) $R=\sqrt{4{,}25}$, $\eta=0{,}0059512$, $RG/\sqrt T=\sqrt{51}/100=0{,}071414\le0{,}0715$. Theo Hệ quả 05.15(b), $F_R=\min_WF$ vì mọi $u\in W$ cách $w_1$ không quá $R$. $\min F=2{,}265512=-\ln p_\theta(2)$. Tỉ số với cận khoảng $529$ (bài ghi "khoảng $500$"). (e) $96{,}07$; $G=10{,}2015$. |
| 09.8 | ✓ (F4) | (a), (b), (c) đúng; $3{,}2$; phép kiểm với $m=2$ đúng. |
| 09.9 | ✓ | Gợi ý 2 và Bước 2: $\mathrm{KL}\le\chi^2$. Trường hợp $\theta^\star>2\epsilon_m$: $\hat\theta>\epsilon_m$ và $1-\hat\theta\ge\tfrac13$, cho cận $3\epsilon_m<2\epsilon_m(1+\ln2)\le B_m$. Trường hợp $\theta^\star\le2\epsilon_m$: hàm $y\ln(y(m+2))$ tăng khi $y\ge1/(m+2)$ (thật ra tăng ngay từ $y\ge e^{-1}/(m+2)$), và số hạng thứ hai $\le2\epsilon_m$ nhờ $1-\hat\theta\ge\tfrac12$. Số: $\epsilon=0{,}1456141$; $0{,}0439449$; $0{,}0136810$; $B=1{,}278877$; $0{,}481468$; $0{,}180916$, đều làm tròn lên đúng. Phân vị nhị thức chính xác: $0{,}02098$; $0{,}00201$; $0{,}000196$. Cận $\chi^2$ đều: $1{,}872$ với $m=10^4$. |
| 09.10 | ✓ | (a) $\nu_v=\sum_iq_i(v)$, $\sum\nu=m$. (b) Đẳng thức đúng. (c) Khi $\nu_y=0$, cận trên đúng không đạt được; với $\nu=(2,1,1)$: $-6\ln2=-4{,}158883$, $4\ln\tfrac13=-4{,}394449$, hiệu $0{,}235566=4\cdot0{,}058892$. |

## Bảng số (Bài tập 09.6; tính lại từ script)

| Đại lượng | Bản đóng băng | Tính lại |
|---|---|---|
| Hiệu (độ lệch chuẩn), $m=1$; $5$; $50$; $500$ | $0{,}0316$ ($0{,}0130$); $0{,}0067$ ($0{,}0035$); $0{,}00071$ ($0{,}00040$); $0{,}00008$ ($0{,}00005$) | $0{,}031566$ ($0{,}012951$); $0{,}006709$ ($0{,}003545$); $0{,}000711$ ($0{,}000396$); $0{,}000082$ ($0{,}000051$) ✓ |
| Sai số chuẩn | $0{,}0041$; $0{,}0011$; $0{,}00013$; $0{,}000016$ | $0{,}0040954$; $0{,}0011209$; $0{,}0001252$; $0{,}0000160$ ✓ |
| Tỉ số | $7{,}7$; **$6{,}1$**; **$5{,}6$**; $5{,}1$ | $7{,}708$; **$5{,}985$**; **$5{,}681$**; $5{,}119$ (F1) |
| Độ lệch chuẩn của lỗi kiểm tra, $m=50$ (làm trơn; mô hình thật) | $0{,}0041$; $0{,}0040$ | $0{,}0040957$; $0{,}0040471$ ✓ |
| Hai nhóm độc lập | $0{,}0018$; tỉ số $0{,}4$ | $0{,}001811$; $0{,}39$ ✓ |
| Xác suất nhỏ nhất của 10 mô hình, $m=50$ | $\ge0{,}087$ | $0{,}0872$ ✓ |
| $p_{\mathrm{alt}}$ trừ mô hình thật | $0{,}0392$ ($0{,}0012$) | với $m=50$: $0{,}039180$ ($0{,}001246$) ✓; với $m=1$: $0{,}039073$ (F2) |
| $p_{\mathrm{alt}}$ trừ mô hình làm trơn, $m=50$ | — | $0{,}038469$ ($0{,}001350$), nhỏ nhất $0{,}0364$ (F3) |
| Đường chéo học được; mô phỏng số cặp giữ nguyên | $0{,}595$; $0{,}605$; $0{,}592$; $0{,}600$; $23{,}3$; $3{,}06$; $5{,}9\%$ | trùng; $23{,}298$; $3{,}057$; $5{,}94\%$ (hạt giống riêng) ✓ |
| (c) Tỉ lệ giữ nguyên trên 200 chuỗi | $0{,}597$ ($0{,}586$–$0{,}621$) | $0{,}597$ [$0{,}586$; $0{,}621$] (bộ sinh `default_rng(1000+seed)`) ✓ |
| Hoeffding | $2{,}4418\cdot0{,}09603\le0{,}2345$; gấp $57$ lần | $0{,}234496$; $57{,}3$ ✓ |
| Kiểm 09.6, $(18-23{,}3)/3{,}06$; $39\cdot0{,}46$; $0{,}0392/0{,}0012$ | $-1{,}7$; $17{,}9$; $33$ | $-1{,}73$; $17{,}94$; $32{,}7$ ✓ |

Các số của những bài khác ghi ở bảng "Từng bài"; tất cả khớp.

## Bảng phát hiện

| mức độ | vị trí | vấn đề | bằng chứng | đề xuất sửa |
|---|---|---|---|---|
| nhẹ | Bài 09.6, Lời giải (a), Bước 1: bảng dòng 572–573 và câu dòng 576 | Hai tỉ số làm tròn sai. Câu ví dụ có phép chia sai: $0{,}00071/0{,}00013=5{,}46$, không phải $5{,}6$. | Tính từ số chưa làm tròn: $0{,}006709/0{,}0011209=5{,}985$ và $0{,}000711/0{,}0001252=5{,}681$. | Bảng: $6{,}1\to6{,}0$, $5{,}6\to5{,}7$. Dòng 576: "$0{,}00040/3{,}162\approx0{,}000125$ và $0{,}00071/0{,}000125\approx5{,}7$". Không thêm tiếng. |
| nhẹ | Bài 09.6, đề, dòng 538 | "Trên mười mẫu kiểm tra" không nói mẫu của dòng $m$ nào. Mẫu kiểm tra phụ thuộc $m$, vì mẫu huấn luyện được rút trước từ cùng bộ sinh. Hai số $0{,}0392$ và $0{,}0012$ là của $m=50$. | $m=50$: $0{,}039180$ ($0{,}001246$); $m=1$: $0{,}039073$. | "Trên mười mẫu kiểm tra của dòng $m=50$" (thêm 3 tiếng). |
| nhẹ | Bài 09.6, Lời giải (a), Bước 5, dòng 602 | Ý (iii) hỏi lỗi kiểm tra có phân biệt được *mô hình học được* với $p_{\mathrm{alt}}$ không, nhưng lời giải chỉ so $p_{\mathrm{alt}}$ với mô hình thật. Người đọc phải tự suy ra câu trả lời. | Đề dòng 546; tính lại: $p_{\mathrm{alt}}$ trừ mô hình làm trơn là $0{,}0385$ ($0{,}0013$), nhỏ nhất $0{,}0364$. | Thay câu cuối bằng "…nên một mẫu kiểm tra $200$ chuỗi tách được $p_{\mathrm{alt}}$ khỏi mô hình thật và khỏi mô hình học được" (thêm 5 tiếng). |
| nhẹ | Bài 09.8, dòng 748 | UML Bài tập 24.1 chỉ yêu cầu chứng minh ước lượng phương sai bị chệch. Ý (a) (dẫn ra ước lượng) và số ở (b) cũng do học phần thêm, nhưng dòng 748 chỉ ghi "Ý (c) do học phần thêm". Tương tự, 09.9(c), với điều kiện $\epsilon_m\le\tfrac16$ và hằng số $B_m$, là bản cụ thể hóa của câu "bound the true risk", nhưng không được ghi. | UML tr. 356, bài 1–2. | Dòng 748: "Ý (a), (c) và số ở (b) do học phần thêm" (thêm 5 tiếng). Dòng 805, nếu còn chỗ: "Ý (c) cụ thể hóa yêu cầu của UML." |

**Ngân sách chữ.** Ba sửa F2–F4 thêm khoảng $13$ tiếng, nên tệp lên khoảng $9\,940$ tiếng, vẫn dưới $10\,000$. Nếu muốn giữ mức cũ, cắt câu "Hiệu giảm khoảng chín lần từ $m=50$ đến $m=500$." ở dòng 576 ($11$ tiếng; con số chín lần cũng chỉ đúng xấp xỉ, $8{,}7$).
