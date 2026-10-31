# Bài 10 — Gradient chính sách và học liên tục

Trong Bài 01–09, dữ liệu được rút từ một phân bố $D$ cố định, không phụ thuộc thuật toán học. Ở Bài 09, thuật toán chọn phân bố biến phân để lấy kì vọng trong cận dưới bằng chứng, nhưng dữ liệu vẫn rút từ $D$.

Câu hỏi trung tâm của bài, nêu ở cuối Bài 09, là điều gì thay đổi khi thuật toán học tương tác với môi trường và khi nhiệm vụ thay đổi theo thời gian. Phần A (§4–§6) xét *học tăng cường* (reinforcement learning) qua *gradient chính sách* (policy gradient) và thuật toán REINFORCE, với hữu hạn trạng thái (state) và hành động (action) và số bước cố định. Phần B (§7–§9) xét *học liên tục* (continual learning). Phương pháp tác nhân–phê bình (actor–critic) và chính sách dạng mạng nơ-ron nằm ngoài bài.

## Câu hỏi mở đầu

Một robot bắt đầu ở trạng thái $s_0$ và chọn một trong hai hành động. Hành động $1$ đưa robot tới trạng thái $s_1$ với xác suất $0{,}8$ và tới trạng thái $s_2$ với xác suất $0{,}2$; hành động $0$ đổi chỗ hai xác suất này. Nếu robot chọn hành động $1$ với xác suất $q$, nó tới $s_1$ với xác suất $0{,}8q+0{,}2(1-q)=0{,}2+0{,}6q$, bằng $0{,}5$ khi $q=0{,}5$ và $0{,}74$ khi $q=0{,}9$. Phân bố của các trạng thái robot quan sát được, và của các phần thưởng nó nhận, phụ thuộc xác suất $q$ mà robot đang học.

Một mô hình một tham số $w$ được huấn luyện trên môi trường A rồi trên môi trường B. Trên A, rủi ro kì vọng của mô hình là $L_A(w)=w^2/2$, nhỏ nhất tại $w=0$; trên B, rủi ro kì vọng là $L_B(w)=(w-1)^2/2$, nhỏ nhất tại $w=1$. Sau môi trường A, mô hình có $w=0$ và $L_A=0$. Huấn luyện tiếp chỉ trên dữ liệu của B đưa $w$ tới $1$, và rủi ro trên môi trường A tăng từ $0$ lên $\tfrac12$.

**Câu hỏi.** Trong mỗi tình huống, giả thiết nào của Bài 01 về mẫu huấn luyện không còn đúng? Có thể gộp mọi quan sát đã thu thành một mẫu rồi dùng các cận của Bài 02–08 không?

Các quan sát của robot không tạo thành một mẫu $S\sim D^m$ như (T1), vì phân bố của chúng thay đổi theo $q$ và trạng thái ở bước sau phụ thuộc hành động ở bước trước. Khi dữ liệu đã thu, trung bình các phần thưởng là một số cố định, không chứa $q$, nên đạo hàm của nó theo $q$ bằng $0$, dù phần thưởng kì vọng đổi khi $q$ đổi; đạo hàm của phần thưởng kì vọng vẫn ước lượng được từ dữ liệu (§5). Ở tình huống thứ hai, dữ liệu của A không còn khi học B nên không gộp được; nếu giữ được, mẫu gộp phục vụ rủi ro trung bình của hai môi trường (§7). Không $w$ nào cho cả hai rủi ro bằng $0$, nên cần một điểm thỏa hiệp (§8).

## Mục tiêu học tập

Sau bài này, người học có thể:

1. Mô tả bài toán tối ưu chính sách trên một quá trình quyết định Markov tầm nhìn hữu hạn và chỉ ra đại lượng nào ngẫu nhiên, theo phân bố nào.
2. Chứng minh đồng nhất thức gradient log và công thức gradient chính sách theo quỹ đạo, nêu điều kiện đổi chỗ đạo hàm và kì vọng, và kiểm tra công thức bằng đạo hàm trực tiếp.
3. Chứng minh rằng tổng phần thưởng từ bước hiện tại và giá trị nền không phụ thuộc hành động giữ kì vọng của ước lượng gradient; tính phương sai trong trường hợp nhỏ và đưa ra một giá trị nền gây chệch.
4. Đặc tả một giao thức học liên tục và tính độ chính xác phân lớp trung bình cuối cùng, chuyển đổi ngược và độ quên từ một ma trận đánh giá theo một quy ước nêu rõ.
5. Giải thích, dựa trên ví dụ hai nhiệm vụ bậc hai và các phản ví dụ của bài, vì sao các cận cho phân bố cố định, cho mục tiêu lồi và cho hối tiếc tĩnh không trực tiếp giải quyết hai bài toán.

## Kiến thức tiên quyết

- **Từ Bài 01.** (T1), (T2); hàm lỗi và rủi ro kì vọng (Định nghĩa 01.1); bài toán học thống kê (Định nghĩa 01.5); rủi ro thực nghiệm (Định nghĩa 01.6); giả thuyết chọn theo mẫu (Nhận xét 01.9); rủi ro vượt mức (Định nghĩa 01.24).
- **Từ Bài 02.** Bất đẳng thức Hoeffding (Định lý 02.7); (T3) và đoạn sau Nhận xét 02.8 về miền $[a,b]$; cận tin cậy Hoeffding cho một giả thuyết cố định (Hệ quả 02.10).
- **Từ Bài 05.** Dưới gradient (Định nghĩa 05.2); phép chiếu (Định nghĩa 05.7); oracle gradient ngẫu nhiên và lịch sử (Định nghĩa 05.10); kì vọng có điều kiện theo lịch sử (Bổ đề 05.12); bất đẳng thức một bước (Mệnh đề 05.13); giả thiết (C) và cận kì vọng cho hạ gradient ngẫu nhiên có chiếu (Định lý 05.14); độ dài bước theo số vòng lặp (Hệ quả 05.15).
- **Từ Bài 08.** Điểm dừng xấp xỉ của SGD trên hàm mục tiêu trơn (Mệnh đề 08.12).
- **Từ Bài 09.** Mô hình xác suất (Định nghĩa 09.2); entropy (Định nghĩa 09.7); phân bố hậu nghiệm (Định nghĩa 09.10); ước lượng gradient log (Ví dụ 09.12, Bước 4); gradient theo đường đi không chệch (Mệnh đề 09.15, Phụ lục B của Bài 09).
- **Xác suất và giải tích.** Kì vọng có điều kiện và tính chất tháp cho biến rời rạc; quy tắc dây chuyền; định lý hội tụ bị chặn (chỉ Phụ lục A).

**Câu hỏi ôn nhanh.**

1. Một hàm lỗi nhận giá trị trong $[0,1]$. Với $m=500$ quan sát độc lập và $\delta=0{,}05$, tính bán kính $\sqrt{\ln(2/\delta)/(2m)}$ của Hệ quả 02.10(b). Giả thuyết $h$ phải thỏa điều kiện gì?
2. Với $s(\theta)=1/(1+e^{-\theta})$, tính $s'(\theta)$, $\frac{d}{d\theta}\ln s(\theta)$ và $\frac{d}{d\theta}\ln\big(1-s(\theta)\big)$.

::: solution Lời giải câu hỏi ôn nhanh
1. Với $\delta=0{,}05$, $\ln(2/\delta)=\ln40\approx3{,}6889$ và $2m=1000$, nên bán kính là $\sqrt{0{,}0036889}\le0{,}0608$. Giả thuyết $h$ phải cố định, không phụ thuộc mẫu (Nhận xét 01.9).
2. Theo quy tắc dây chuyền, $s'(\theta)=e^{-\theta}/(1+e^{-\theta})^2=s(\theta)\big(1-s(\theta)\big)$. Chia cho $s$: $\frac{d}{d\theta}\ln s=1-s$. Vì $1-s$ có đạo hàm $-s(1-s)$, ta có $\frac{d}{d\theta}\ln(1-s)=-s$.
:::

## 1. Thiết lập bài toán

Mỗi bài toán của Bài 10 có bảy thành phần.

**Phần A: tối ưu chính sách.** Một *tác tử* (agent) tương tác với môi trường qua các *lượt* (episode) cùng số bước. Ở mỗi bước, tác tử quan sát *trạng thái* của môi trường, chọn một *hành động* theo một *chính sách* (policy), tức một phân bố trên các hành động tại mỗi trạng thái, và nhận một *phần thưởng* (reward).

- **Dữ liệu.** Các lượt, mỗi lượt là một dãy trạng thái, hành động và phần thưởng (§4).
- **Cơ chế lấy mẫu.** Hành động rút theo chính sách hiện tại, trạng thái kế tiếp theo quy luật của môi trường; các lượt độc lập khi chính sách cố định.
- **Lớp mô hình.** Một họ chính sách có tham số, khả vi theo tham số; tác tử chọn tham số (§4).
- **Thuật toán.** Phương pháp đi lên theo gradient ước lượng từ các lượt (§5).
- **Mục tiêu.** Tổng phần thưởng kì vọng của một lượt, cần làm lớn.
- **Đối tượng so sánh.** Cận trên đúng của mục tiêu trên họ chính sách.
- **Tài nguyên.** Số lượt.

**Phần B: học liên tục.** Một mô hình nhận dữ liệu của $K$ *nhiệm vụ* (task) theo thứ tự, mỗi nhiệm vụ có một phân bố riêng.

- **Dữ liệu.** Một mẫu cho mỗi nhiệm vụ (§7).
- **Cơ chế lấy mẫu.** Mẫu của nhiệm vụ $k$ độc lập cùng phân bố $D_k$; các $D_k$ khác nhau.
- **Lớp mô hình.** Một tập tham số $W$ như Bài 05–08.
- **Thuật toán.** Phương pháp huấn luyện tuần tự, có thể giữ một phần dữ liệu cũ hoặc phạt độ lệch khỏi tham số cũ (§8).
- **Mục tiêu.** Rủi ro nhỏ trên mọi nhiệm vụ đã gặp (§7).
- **Đối tượng so sánh.** Mô hình huấn luyện chung trên mọi dữ liệu, hoặc mô hình riêng cho từng nhiệm vụ (§7).
- **Tài nguyên.** Bộ nhớ cho dữ liệu cũ; thông tin về nhiệm vụ của quan sát khi dự đoán (§7).

Các đại lượng chia theo nguồn ngẫu nhiên như bảng dưới.

| Loại | Phần A | Phần B |
|---|---|---|
| Cố định | môi trường, họ chính sách | $D_1,\ldots,D_K$, thứ tự nhiệm vụ |
| Ngẫu nhiên | các lượt, các tham số, các ước lượng gradient | các mẫu, dữ liệu cũ được giữ, mẫu kiểm tra |
| Tất định | mục tiêu tại một tham số cố định | rủi ro của từng nhiệm vụ tại một tham số cố định |

Ở Phần A, tham số tại cập nhật thứ $j$ ngẫu nhiên, nên phân bố của lượt thứ $j$ phụ thuộc các lượt trước qua tham số đó; đây là chỗ (T1) không còn đúng. Ở Phần B, mỗi mẫu thỏa (T1) với phân bố của nó, nhưng không có một $D$ chung.

## 2. Kí hiệu và giả thiết

Bảng dưới gom các kí hiệu chung; kí hiệu khác được đặt tên tại chỗ dùng.

| Kí hiệu | Ý nghĩa |
|---|---|
| $\theta\in\Theta$ | tham số của chính sách; $\Theta$ là một tập mở của một không gian Euclid |
| $\eta_j$, $T$ | độ dài bước tại cập nhật $j$, số cập nhật (như $\eta_t$ của Bài 05; chỉ số $j$ vì $t$ là bước trong lượt) |
| $w\in W$, $\ell$, $L_D$ | tham số, tập tham số, hàm lỗi, rủi ro kì vọng (Phần B, như Bài 05) |
| $K$ | số nhiệm vụ (Phần B) |
| $\ln$ | logarit tự nhiên |

Giả thiết (T1) được thay bằng giả thiết về môi trường ở Phần A (§4) và về dữ liệu của từng nhiệm vụ ở Phần B (§7). Không kết quả nào của Phần A giả sử mục tiêu là hàm lõm; Phần B dùng hàm bậc hai lồi ngặt (§8) và giả thiết (C) như Bài 05 (§9).

## 3. Ví dụ xuyên suốt

::: example Ví dụ 10.1 (Bài toán bandit hai hành động với chính sách sigmoid)
**Thiết lập.** Bài toán chọn một trong hữu hạn hành động có phần thưởng chưa biết được gọi là *bài toán bandit* (multi-armed bandit). Ở đây một lượt có đúng một bước và không có trạng thái. Tác tử chọn hành động $A\in\{0,1\}$ và nhận phần thưởng tất định $r(1)=3$ hoặc $r(0)=1$ (giá trị giả định). Chính sách chọn hành động $1$ với xác suất
$$
\pi_\theta(1)=\frac1{1+e^{-\theta}},\qquad\theta\in\mathbb R,
$$
và hành động $0$ với xác suất $\pi_\theta(0)=1-\pi_\theta(1)$. Đại lượng ngẫu nhiên duy nhất là hành động $A$.

**Bước 1: phần thưởng kì vọng.** Ta gọi $J(\theta)=\mathbb E_{A\sim\pi_\theta}r(A)$ là phần thưởng kì vọng của chính sách. Ở đây
$$
\begin{aligned}
J(\theta)&=3\,\pi_\theta(1)\\
&\quad+1\cdot\big(1-\pi_\theta(1)\big)\\
&=1+2\,\pi_\theta(1).
\end{aligned}
$$

**Bước 2: giá trị tại $\theta=\ln3$.** Vì $e^{-\ln3}=\tfrac13$, ta có $\pi_\theta(1)=1/(1+\tfrac13)=\tfrac34$. Do đó $J(\ln3)=1+\tfrac32=\tfrac52$.

**Bước 3: đạo hàm trực tiếp.** Theo câu ôn nhanh 2, $\frac{d}{d\theta}\pi_\theta(1)=\pi_\theta(1)\big(1-\pi_\theta(1)\big)$, nên $J'(\theta)=2\,\pi_\theta(1)\big(1-\pi_\theta(1)\big)$. Tại $\theta=\ln3$,
$$
J'(\ln3)=2\cdot\tfrac34\cdot\tfrac14=\tfrac38 .
$$

**Kết luận.** $J(\theta)<3$ với mọi $\theta$ và $J(\theta)\to3$ khi $\theta\to\infty$, nên cận trên đúng $3$ không đạt. Đạo hàm tính được vì $J$ có dạng đóng, chứa $r(0)$ và $r(1)$; ở §5, ta tính lại $\tfrac38$ chỉ từ các hành động rút được và các phần thưởng quan sát được.
:::

::: application Hệ thống đề xuất với hai nội dung
**Thiết lập.** Một hệ thống đề xuất hiển thị nội dung $1$ hoặc $0$ cho mỗi người dùng đến; người dùng nhấp với xác suất chưa biết, $0{,}6$ với nội dung $1$ và $0{,}4$ với nội dung $0$ (giá trị giả định). Phần thưởng bằng $1$ khi người dùng nhấp, $0$ khi không. Chính sách giống Ví dụ 10.1; với chính sách cố định, mỗi người dùng là một lượt độc lập.

**Câu hỏi thực hành.** (i) Có ước lượng không chệch của đạo hàm phần thưởng kì vọng từ một lần hiển thị không? (ii) Nếu mỗi lần hiển thị được cộng thêm một khoản cố định $c=10$, chính sách tốt nhất có đổi không, và ước lượng ở (i) thay đổi thế nào? Câu trả lời ở §6.
:::

## 4. Quá trình quyết định Markov và mục tiêu của chính sách

Robot của câu hỏi mở đầu chọn hành động ở nhiều bước, và hành động ở một bước quyết định trạng thái ở bước sau.

::: definition Định nghĩa 10.1 (Quá trình quyết định Markov tầm nhìn hữu hạn và chính sách ngẫu nhiên khả vi)
Cho một tập trạng thái hữu hạn $\mathcal S$, một tập hành động hữu hạn $\mathcal A$ và một độ dài lượt $H\in\mathbb N$.

- **Phân bố trạng thái đầu.** Một phân bố $\mu_0$ trên $\mathcal S$; cố định, không phụ thuộc tham số của chính sách.
- **Luật chuyển trạng thái.** Với mỗi cặp $(s,a)$, một phân bố $P(\cdot\mid s,a)$ trên $\mathcal S$, với $P(s'\mid s,a)$ là xác suất tới $s'$ khi chọn $a$ ở $s$; cố định, không phụ thuộc tham số của chính sách.
- **Hàm phần thưởng.** Một hàm tất định $r:\mathcal S\times\mathcal A\to[r_{\min},r_{\max}]$; cố định, bị chặn.
- **Chính sách.** Một họ $\{\pi_\theta:\theta\in\Theta\}$, mỗi $\pi_\theta(\cdot\mid s)$ là một phân bố trên $\mathcal A$, và $\theta\mapsto\pi_\theta(a\mid s)$ khả vi trên $\Theta$ với mọi $(s,a)$; tác tử chọn $\theta$.

Bộ $(\mathcal S,\mathcal A,\mu_0,P,r,H)$ được gọi là một *quá trình quyết định Markov* (Markov decision process, MDP) *tầm nhìn hữu hạn* (finite horizon); mỗi $\pi_\theta$ là một *chính sách ngẫu nhiên* (stochastic policy) khả vi.
:::

Tên "Markov" chỉ việc phân bố của trạng thái kế tiếp chỉ phụ thuộc trạng thái và hành động hiện tại. Tác tử không biết $\mu_0$, $P$, $r$ và chỉ chọn $\theta$; phần thưởng của các bước được cộng lại, không nhân *hệ số chiết khấu* (discount factor). Phần thưởng cũng có thể ngẫu nhiên, như ở khối ứng dụng của §3, với hai điều kiện: khi biết trạng thái và hành động của bước đó, phân bố của nó không phụ thuộc $\theta$, và nó không ảnh hưởng tới các bước sau. Khi đó các kết quả của §5–§6 vẫn đúng với $r(s,a)$ là kì vọng có điều kiện của phần thưởng, theo tính chất tháp.

*Chính sách bảng* $\pi_\theta(1\mid s)=1/(1+e^{-\theta_s})$ trên $\mathcal A=\{0,1\}$, với một tham số $\theta_s\in\mathbb R$ cho mỗi trạng thái, thỏa định nghĩa; Ví dụ 10.1 là trường hợp một trạng thái và $H=1$. *Chính sách tất định* (deterministic policy) $\pi_\theta(1\mid s)=\mathbb 1[\theta_s>0]$ không khả vi tại $\theta_s=0$; phần thưởng kì vọng khi đó là hàm bậc thang của $\theta$, có gradient bằng $0$ ở mọi điểm gradient tồn tại.

Tập hành động $\mathcal A$ khác bảng chữ của Bài 09 và thuật toán $A$; độ dài lượt $H$ (chữ nghiêng) khác entropy $\mathrm H$ và lớp $\mathcal H$.

::: definition Định nghĩa 10.2 (Quỹ đạo, tổng phần thưởng và mục tiêu của chính sách)
Cho một MDP tầm nhìn hữu hạn và một chính sách $\pi_\theta$ như Định nghĩa 10.1.

- **Quỹ đạo.** Một *quỹ đạo* (trajectory) là $\tau=(s_0,a_0,\ldots,s_{H-1},a_{H-1})$, một phần tử của tập hữu hạn $\mathcal T=(\mathcal S\times\mathcal A)^H$. Quỹ đạo ngẫu nhiên $(S_0,A_0,\ldots,S_{H-1},A_{H-1})$ sinh theo $S_0\sim\mu_0$, $A_t\sim\pi_\theta(\cdot\mid S_t)$, $S_{t+1}\sim P(\cdot\mid S_t,A_t)$.
- **Phân bố quỹ đạo.** Xác suất $p_\theta(\tau)$ của quỹ đạo $\tau$, cho bởi công thức ngay dưới danh sách.
- **Tổng phần thưởng.** *Tổng phần thưởng* (return) của $\tau$ là $R(\tau)=\sum_{t=0}^{H-1}r(s_t,a_t)$, trong $[Hr_{\min},Hr_{\max}]$; $r_t=r(S_t,A_t)$ là phần thưởng ngẫu nhiên ở bước $t$.
- **Mục tiêu.** $J(\theta)=\mathbb E_{\tau\sim p_\theta}R(\tau)$, tức $\sum_{\tau\in\mathcal T}p_\theta(\tau)R(\tau)$. Bài toán *tối ưu chính sách* (policy optimization) là tìm $\theta$ làm $J(\theta)$ lớn; đối tượng so sánh là $\sup_{\theta\in\Theta}J(\theta)$.

Xác suất của quỹ đạo là
$$
\begin{aligned}
p_\theta(\tau)&=\mu_0(s_0)\\
&\quad\cdot\textstyle\prod_{t=0}^{H-1}\pi_\theta(a_t\mid s_t)\\
&\quad\cdot\textstyle\prod_{t=0}^{H-2}P(s_{t+1}\mid s_t,a_t).
\end{aligned}
$$
:::

Lấy tổng lần lượt theo $a_{H-1}$, $s_{H-1}$, …, $s_0$, ta thấy $p_\theta$ là một hàm xác suất trên $\mathcal T$; $s_H$ không xuất hiện vì không có phần thưởng ở bước $H$. Ở Bài 01, hàm lỗi $\ell(h,z)$ phụ thuộc $h$ còn $D$ thì không; ở đây phân bố $p_\theta$ của dữ liệu phụ thuộc tham số, còn $R(\tau)$ thì không.

Quỹ đạo $\tau$ khác dung sai $\tau$ của Bài 04, nhãn $\tau_i$ của Bài 07 và chỉ số ngẫu nhiên $\tau$ của Mệnh đề 08.12; trạng thái $S_t$ luôn có chỉ số, khác mẫu $S$.

::: example Ví dụ 10.2 (Quá trình quyết định Markov hai bước)
**Thiết lập.** $\mathcal S=\{s_0,s_1,s_2\}$, $\mu_0$ đặt khối lượng $1$ tại $s_0$, $\mathcal A=\{0,1\}$, $H=2$. Từ $s_0$, luật chuyển như câu hỏi mở đầu: hành động $1$ tới $s_1$ với xác suất $0{,}8$ và tới $s_2$ với xác suất $0{,}2$; hành động $0$ ngược lại. Phần thưởng cho trong bảng (giá trị giả định). Chính sách bảng với $\theta=(\theta_{s_0},\theta_{s_1},\theta_{s_2})$; các hành động và trạng thái $S_1$ là ngẫu nhiên. Ở đây $s_1$, $s_2$ là tên trạng thái; trạng thái ở bước $1$ là $S_1\in\{s_1,s_2\}$.

| Trạng thái | $r(s,1)$ | $r(s,0)$ |
|---|---|---|
| $s_0$ | $0$ | $1$ |
| $s_1$ | $3$ | $1$ |
| $s_2$ | $0$ | $1$ |

**Bước 1: tám quỹ đạo tại $\theta=0$.** Mọi xác suất chọn hành động bằng $\tfrac12$. Quỹ đạo $(s_0,1,s_1,1)$ có xác suất $\tfrac12\cdot0{,}8\cdot\tfrac12=0{,}2$ và tổng phần thưởng $0+3=3$. Tính tương tự cho cả tám quỹ đạo:

| Quỹ đạo | $p_0(\tau)$ | $R(\tau)$ |
|---|---|---|
| $(s_0,1,s_1,1)$ | $0{,}2$ | $3$ |
| $(s_0,1,s_1,0)$ | $0{,}2$ | $1$ |
| $(s_0,1,s_2,1)$ | $0{,}05$ | $0$ |
| $(s_0,1,s_2,0)$ | $0{,}05$ | $1$ |
| $(s_0,0,s_1,1)$ | $0{,}05$ | $4$ |
| $(s_0,0,s_1,0)$ | $0{,}05$ | $2$ |
| $(s_0,0,s_2,1)$ | $0{,}2$ | $1$ |
| $(s_0,0,s_2,0)$ | $0{,}2$ | $2$ |

**Bước 2: bước cuối.** Ở $s_1$, phần thưởng kì vọng của bước cuối là $\tfrac12\cdot3+\tfrac12\cdot1=2$; ở $s_2$, là $\tfrac12\cdot0+\tfrac12\cdot1=\tfrac12$.

**Bước 3: hai hành động đầu.** Tổng phần thưởng kì vọng khi chọn hành động $1$ ở $s_0$ là $0+0{,}8\cdot2+0{,}2\cdot\tfrac12=1{,}7$; khi chọn hành động $0$, là $1+0{,}2\cdot2+0{,}8\cdot\tfrac12=1{,}8$.

**Bước 4: mục tiêu.** $J(0)=\tfrac12\cdot1{,}7+\tfrac12\cdot1{,}8=1{,}75$. Tổng trên bảng của Bước 1 cho cùng giá trị: $0{,}6+0{,}2+0+0{,}05+0{,}2+0{,}1+0{,}2+0{,}4=1{,}75$.

**Kết luận.** Xác suất tới $s_1$ bằng $0{,}2+0{,}6\,\pi_\theta(1\mid s_0)$, nên phân bố của $S_1$, tức của dữ liệu ở bước sau, phụ thuộc $\theta_{s_0}$.
:::

Mỗi số hạng của $J(\theta)$ chứa xác suất của chính sách và của môi trường. Tác tử biết $\pi_\theta$ nhưng không biết $\mu_0$, $P$, $r$, nên không tính được $J$ hay đạo hàm của nó bằng công thức.

## 5. Gradient chính sách và thuật toán REINFORCE

Ở câu hỏi mở đầu, đạo hàm theo $q$ của trung bình các phần thưởng đã nhận bằng $0$. Để ước lượng $\nabla J(\theta)$ từ các lượt, chúng ta cần viết đạo hàm của một kì vọng theo một phân bố phụ thuộc $\theta$ thành kì vọng của một đại lượng tính được trên quỹ đạo. Với một họ hàm xác suất $p_\theta$, ta gọi $\nabla_\theta\ln p_\theta$ là *gradient log* (score function) và tập các $\tau$ có $p_\theta(\tau)>0$ là *giá* (support) của $p_\theta$; Ví dụ 09.12, Bước 4 đã dùng ước lượng gradient log cho biến Bernoulli.

::: lemma Bổ đề 10.3 (Đồng nhất thức gradient log) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Tập giá trị.** $\mathcal T$ hữu hạn, không phụ thuộc $\theta$.
- **Phân bố.** Với mỗi $\theta$ trong tập mở $\Theta$, $p_\theta$ là một hàm xác suất trên $\mathcal T$.
- **Tính khả vi.** Với mọi $\tau\in\mathcal T$, hàm $\theta\mapsto p_\theta(\tau)$ khả vi trên $\Theta$.

**Bảo đảm.** Đồng nhất thức, đúng với mọi $\theta\in\Theta$; không có mẫu.

- **(a) Gradient của xác suất.** Nếu $p_\theta(\tau)>0$ thì $\nabla_\theta p_\theta(\tau)=p_\theta(\tau)\nabla_\theta\ln p_\theta(\tau)$; nếu $p_\theta(\tau)=0$ thì $\nabla_\theta p_\theta(\tau)=0$.
- **(b) Kì vọng bằng không.** $\mathbb E_{\tau\sim p_\theta}\nabla_\theta\ln p_\theta(\tau)=0$, kì vọng lấy trên giá của $p_\theta$.
:::

::: proof Chứng minh Bổ đề 10.3
**Lộ trình.** Quy tắc dây chuyền và tính chất của điểm cực tiểu cho (a); lấy đạo hàm của $\sum_\tau p_\theta(\tau)=1$ cho (b). Đồng nhất thức then chốt là $\nabla\sum_\tau p_\theta(\tau)=\nabla1=0$.

**Bước 1: phần (a), dùng $\Theta$ mở.** Nếu $p_\theta(\tau)>0$, quy tắc dây chuyền cho $\nabla\ln p_\theta(\tau)=\nabla p_\theta(\tau)/p_\theta(\tau)$. Nếu $p_\theta(\tau)=0$, hàm không âm $\theta'\mapsto p_{\theta'}(\tau)$ đạt giá trị nhỏ nhất tại $\theta$, một điểm trong của $\Theta$, nên gradient của nó tại đó bằng $0$.

**Bước 2: phần (b), dùng $\mathcal T$ hữu hạn, không phụ thuộc $\theta$.** Tổng $\sum_{\tau\in\mathcal T}p_\theta(\tau)=1$ với mọi $\theta$, trên cùng một tập chỉ số hữu hạn, nên đạo hàm từng số hạng:
$$
\begin{aligned}
0&=\textstyle\sum_{\tau\in\mathcal T}\nabla p_\theta(\tau)\\
&=\textstyle\sum_{\tau:\,p_\theta(\tau)>0}p_\theta(\tau)\nabla\ln p_\theta(\tau)\\
&=\mathbb E_{\tau\sim p_\theta}\nabla\ln p_\theta(\tau),
\end{aligned}
$$
trong đó dòng thứ hai dùng (a).

$\square$ Tích của gradient log với một hằng số có kì vọng $0$; §6 dùng điều này để trừ một hằng số khỏi tổng phần thưởng mà không đổi kì vọng của ước lượng.
:::

Ví dụ dưới đây bỏ các giả thiết về tập giá trị.

::: example Ví dụ 10.3 (Giá phụ thuộc tham số)
**Thiết lập.** Hành động $A$ có phân bố đều trên $[0,\theta]$, $\theta>0$, tức mật độ $p_\theta(a)=\mathbb 1[0\le a\le\theta]/\theta$; phần thưởng $r(a)=a$. Tập giá trị vô hạn, và với mỗi $a>0$, hàm $\theta\mapsto p_\theta(a)$ nhảy tại $\theta=a$.

**Bước 1: đạo hàm đúng.** $J(\theta)=\mathbb EA=\theta/2$, nên $J'(\theta)=\tfrac12$.

**Bước 2: kì vọng của gradient log.** Trên giá, $\ln p_\theta(a)=-\ln\theta$, có đạo hàm $-1/\theta$. Kì vọng của gradient log bằng $-1/\theta\ne0$, nên kết luận (b) sai.

**Bước 3: phần thưởng nhân gradient log.** $\mathbb E[A\cdot(-1/\theta)]=-\tfrac12$, ngược dấu với $J'(\theta)$.

**Kết luận.** Khi $\theta$ tăng, giá $[0,\theta]$ nhận thêm khối lượng xác suất ở đầu mút, và gradient log bỏ sót phần này.
:::

Trong $p_\theta(\tau)$, chỉ các thừa số của chính sách phụ thuộc $\theta$; Bổ đề 10.3 cùng sự kiện này cho định lý chính của Phần A.

::: theorem Định lý 10.4 (Gradient của mục tiêu chính sách theo quỹ đạo) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Môi trường.** Một MDP tầm nhìn hữu hạn (Định nghĩa 10.1): $\mu_0$ và $P$ không phụ thuộc $\theta$; $r$ tất định, bị chặn.
- **Chính sách.** Họ $\{\pi_\theta:\theta\in\Theta\}$ như Định nghĩa 10.1, với $\Theta$ mở.
- **Quỹ đạo.** $\tau=(S_0,A_0,\ldots,S_{H-1},A_{H-1})\sim p_\theta$ như Định nghĩa 10.2.

**Bảo đảm.** Đồng nhất thức, đúng với mọi $\theta\in\Theta$; không có mẫu. Đặt
$$
\begin{aligned}
&\hat g(\tau)\\
&=R(\tau)\sum_{t=0}^{H-1}\nabla_\theta\ln\pi_\theta(A_t\mid S_t).
\end{aligned}
$$
Khi đó $J$ khả vi trên $\Theta$ và $\nabla J(\theta)=\mathbb E_{\tau\sim p_\theta}\hat g(\tau)$. Do đó $\hat g(\tau)$ của một lượt là một ước lượng không chệch của $\nabla J(\theta)$; trung bình trên $m$ lượt độc lập cũng không chệch, với ma trận hiệp phương sai chia cho $m$. Định lý không chặn phương sai và không nói gì về điểm cực đại của $J$.
:::

Đại lượng $\nabla_\theta\ln\pi_\theta(A_t\mid S_t)$ xác định với xác suất $1$, vì $A_t$ chỉ nhận các giá trị có $\pi_\theta(A_t\mid S_t)>0$. Kí hiệu $\hat g$ ở đây là ước lượng gradient, khác ứng viên chọn theo mẫu xác thực ở Bài 02 và Bài 04.

::: proof Chứng minh Định lý 10.4
**Lộ trình.** Đạo hàm một tổng hữu hạn, áp dụng Bổ đề 10.3(a), rồi viết $\ln p_\theta(\tau)$ thành tổng và bỏ các số hạng không phụ thuộc $\theta$. Đồng nhất thức then chốt là $\nabla p_\theta=p_\theta\nabla\ln p_\theta$ trên giá.

**Bước 1 (dùng $\mathcal S$, $\mathcal A$, $H$ hữu hạn).** Mỗi $p_\theta(\tau)$ là tích các hàm khả vi $\pi_\theta(a_t\mid s_t)$ với các hằng số. Do đó $J(\theta)=\sum_\tau p_\theta(\tau)R(\tau)$, một tổng hữu hạn, khả vi, và $\nabla J(\theta)=\sum_\tau R(\tau)\nabla p_\theta(\tau)$.

**Bước 2 (Bổ đề 10.3(a); $\mathcal T$ hữu hạn, không phụ thuộc $\theta$).** Bỏ các số hạng ngoài giá và thay $\nabla p_\theta=p_\theta\nabla\ln p_\theta$:
$$
\begin{aligned}
&\nabla J(\theta)\\
&=\textstyle\sum_{\tau:\,p_\theta(\tau)>0}p_\theta(\tau)R(\tau)\\
&\qquad\cdot\nabla\ln p_\theta(\tau)\\
&=\mathbb E_{\tau\sim p_\theta}\big[R(\tau)\nabla\ln p_\theta(\tau)\big].
\end{aligned}
$$

**Bước 3 (dùng $\mu_0$, $P$ không phụ thuộc $\theta$).** Trên giá, mọi thừa số của $p_\theta(\tau)$ dương, và vẫn dương với tham số gần $\theta$ vì chúng liên tục. Lấy logarit:
$$
\begin{aligned}
&\ln p_\theta(\tau)=\ln\mu_0(s_0)\\
&\quad+\textstyle\sum_{t=0}^{H-1}\ln\pi_\theta(a_t\mid s_t)\\
&\quad+\textstyle\sum_{t=0}^{H-2}\ln P(s_{t+1}\mid s_t,a_t).
\end{aligned}
$$
Số hạng thứ nhất và thứ ba không phụ thuộc $\theta$, nên $\nabla\ln p_\theta(\tau)=\sum_t\nabla\ln\pi_\theta(a_t\mid s_t)$. Thay vào Bước 2 ta được $\nabla J(\theta)=\mathbb E\hat g(\tau)$.

$\square$ Ước lượng chỉ cần $R(\tau)$, quan sát được, và gradient log của chính sách, tính được từ $\pi_\theta$; không cần biết $\mu_0$, $P$, $r$. Đạo hàm của trung bình thực nghiệm ở câu hỏi mở đầu bằng $0$ vì nó thiếu thừa số gradient log, thừa số mang ảnh hưởng của $\theta$ lên phân bố dữ liệu.
:::

::: remark Nhận xét 10.5 (Đổi chỗ đạo hàm và kì vọng khi tập quỹ đạo vô hạn)
Khi trạng thái hay hành động liên tục, tổng ở Bước 1 của chứng minh thành tích phân.

**Giả thiết.** Phần thưởng bị chặn và ba điều kiện sau.

- **Mật độ.** Quỹ đạo có mật độ $p_\theta(\tau)$ theo một độ đo nền không phụ thuộc $\theta$.
- **Khả vi.** Với mọi $\tau$, hàm $\theta\mapsto p_\theta(\tau)$ khả vi liên tục trên $\Theta$.
- **Hàm trội.** Với mỗi $\theta_0\in\Theta$ có một lân cận $U$ và một hàm khả tích $\Lambda\ge0$ với $\lvert R(\tau)\rvert\,\lVert\nabla_\theta p_\theta(\tau)\rVert\le\Lambda(\tau)$ cho mọi $\theta\in U$ và mọi $\tau$.

**Bảo đảm.** Đồng nhất thức: $J$ khả vi, $\nabla J(\theta)=\mathbb E[R(\tau)\nabla\ln p_\theta(\tau)]$, và Bước 3 cho lại công thức của Định lý 10.4 khi $\mu_0$, $P$ không phụ thuộc $\theta$ (Phụ lục A). Chính sách Gauss thỏa ba điều kiện (Phụ lục A, Bước 6). Ví dụ 10.3 vi phạm điều kiện khả vi, vì giá của mật độ di chuyển theo $\theta$.
:::

::: example Ví dụ 10.4 (Gradient chính sách trên bài toán bandit hai hành động)
**Thiết lập.** Ví dụ 10.1 tại $\theta=\ln3$, nên $\pi_\theta(1)=\tfrac34$ và $J'(\ln3)=\tfrac38$. Một lượt gồm một hành động $A$; $H=1$.

**Bước 1: gradient log.** Theo câu ôn nhanh 2, $\frac{d}{d\theta}\ln\pi_\theta(1)=1-\pi_\theta(1)=\tfrac14$ và $\frac{d}{d\theta}\ln\pi_\theta(0)=-\pi_\theta(1)=-\tfrac34$. Gộp hai trường hợp, gradient log bằng $A-\pi_\theta(1)$.

**Bước 2: hai giá trị của ước lượng.** Ước lượng của Định lý 10.4 là $\hat g=r(A)\big(A-\pi_\theta(1)\big)$:

- khi $A=1$ (xác suất $\tfrac34$): $\hat g=3\cdot\tfrac14=0{,}75$;
- khi $A=0$ (xác suất $\tfrac14$): $\hat g=1\cdot(-\tfrac34)=-0{,}75$.

**Bước 3: kì vọng.**
$$
\begin{aligned}
\mathbb E\hat g&=\tfrac34\cdot0{,}75+\tfrac14\cdot(-0{,}75)\\
&=0{,}375=\tfrac38,
\end{aligned}
$$
đúng đạo hàm trực tiếp của Ví dụ 10.1.

**Bước 4: kiểm Bổ đề 10.3(b).** Kì vọng của gradient log là $\tfrac34\cdot\tfrac14+\tfrac14\cdot(-\tfrac34)=0$.

**Kết luận.** Mỗi lần rút, ước lượng nhận $\pm0{,}75$, gấp đôi đạo hàm về độ lớn, và với xác suất $\tfrac14$ có dấu ngược với đạo hàm; phương sai của nó được xét ở §6.
:::

::: example Ví dụ 10.5 (Gradient của quá trình quyết định Markov hai bước)
**Thiết lập.** Ví dụ 10.2 tại $\theta=0$, với bảng tám quỹ đạo ở Bước 1 của ví dụ đó.

**Bước 1: gradient log của chính sách bảng.** $\ln\pi_\theta(a\mid s)$ chỉ phụ thuộc $\theta_s$; theo Ví dụ 10.4, Bước 1, tọa độ $\theta_s$ của gradient bằng $a-\tfrac12$ tại $\theta=0$, các tọa độ khác bằng $0$.

**Bước 2: đạo hàm theo $\theta_{s_0}$.** Theo Định lý 10.4, tọa độ này bằng $\sum_\tau p_0(\tau)R(\tau)(a_0-\tfrac12)$. Tổng của $p_0(\tau)R(\tau)$ trên bốn quỹ đạo có $a_0=1$ và trên bốn quỹ đạo có $a_0=0$ là
$$
\begin{aligned}
&0{,}2\cdot3+0{,}2\cdot1\\
&\quad+0{,}05\cdot0+0{,}05\cdot1=0{,}85,\\
&0{,}05\cdot4+0{,}05\cdot2\\
&\quad+0{,}2\cdot1+0{,}2\cdot2=0{,}9 .
\end{aligned}
$$
Do đó $\partial J/\partial\theta_{s_0}=\tfrac12\cdot0{,}85-\tfrac12\cdot0{,}9=-0{,}025$.

**Bước 3: đạo hàm theo $\theta_{s_1}$ và $\theta_{s_2}$.** Tọa độ $\theta_{s_1}$ chỉ khác $0$ trên bốn quỹ đạo qua $s_1$, với thừa số $a_1-\tfrac12$:
$$
\begin{aligned}
&0{,}2\cdot3\cdot\tfrac12-0{,}2\cdot1\cdot\tfrac12\\
&+0{,}05\cdot4\cdot\tfrac12\\
&-0{,}05\cdot2\cdot\tfrac12\\
&=0{,}3-0{,}1+0{,}1-0{,}05\\
&=0{,}25 .
\end{aligned}
$$
Tương tự, qua $s_2$: $0-0{,}025+0{,}1-0{,}2=-0{,}125$. Sai phân hữu hạn của $J$ cho cùng véc-tơ $(-0{,}025;\,0{,}25;\,-0{,}125)$.

**Kết luận.** Tăng $\theta_{s_0}$ làm $J$ giảm, dù hành động $1$ dẫn tới $s_1$, nơi có phần thưởng $3$, vì hành động $1$ mất $1$ ở bước đầu và chỉ được thêm $(0{,}8-0{,}2)(2-\tfrac12)=0{,}9$ ở bước sau; do đó $\partial J/\partial\theta_{s_0}=\tfrac14(1{,}7-1{,}8)$.
:::

Ví dụ dưới đây bỏ giả thiết luật chuyển không phụ thuộc $\theta$, dùng ở Bước 3 của chứng minh Định lý 10.4.

::: example Ví dụ 10.6 (Luật chuyển phụ thuộc tham số)
**Thiết lập.** Như Ví dụ 10.2, trừ luật chuyển từ $s_0$: với mọi hành động, robot tới $s_1$ với xác suất $q=1/(1+e^{-\theta_{s_0}})$, chẳng hạn vì $\theta_{s_0}$ điều khiển cả động cơ. Tại $\theta=0$, $q=\tfrac12$ và $J=\tfrac12+\tfrac12\cdot2+\tfrac12\cdot\tfrac12=1{,}75$.

**Bước 1: đạo hàm đúng theo $\theta_{s_0}$.** Phần thưởng ở bước đầu có kì vọng $1-\pi_\theta(1\mid s_0)$, đạo hàm $-\tfrac14$. Phần thưởng ở bước sau có kì vọng $2q+\tfrac12(1-q)$, đạo hàm $\tfrac32\,q(1-q)=0{,}375$. Tổng: $0{,}125$.

**Bước 2: kì vọng của ước lượng.** Tọa độ $\theta_{s_0}$ của ước lượng của Định lý 10.4 là $(r_0+r_1)(A_0-\tfrac12)$. Ở đây $S_1$ không phụ thuộc $A_0$, nên $r_1$ độc lập với $A_0$ và $\mathbb E[r_1(A_0-\tfrac12)]=\mathbb Er_1\cdot\mathbb E(A_0-\tfrac12)=0$. Còn lại số hạng của $r_0=r(s_0,A_0)$; cộng xác suất nhân phần thưởng nhân gradient log trên hai giá trị của $A_0$:
$$
\begin{aligned}
&\tfrac12\cdot0\cdot\tfrac12+\tfrac12\cdot1\cdot(-\tfrac12)\\
&=-0{,}25 .
\end{aligned}
$$

**Kết luận.** Ước lượng ngược dấu với đạo hàm thật, vì nó bỏ sót gradient của $\ln P(S_1\mid s_0,A_0)$ ở Bước 3 của chứng minh.
:::

Dùng ước lượng của Định lý 10.4 với tham số mới sau mỗi lượt, ta được thuật toán dưới đây.

::: algorithm Thuật toán 10.6 (REINFORCE với một cập nhật mỗi lượt)
**Đầu vào.** Bốn thành phần sau.

- **Môi trường.** Một MDP tầm nhìn hữu hạn để chạy các lượt; $\mu_0$, $P$, $r$ chưa biết.
- **Chính sách.** Họ $\pi_\theta$ của Định nghĩa 10.1, với $\Theta$ là cả không gian tham số (như chính sách bảng).
- **Độ dài bước.** Một dãy tất định $\eta_1,\ldots,\eta_T>0$, với $T\ge1$.
- **Khởi tạo.** $\theta_1\in\Theta$, tất định.

**Cập nhật.** Với $j=1,\ldots,T$:

1. chạy chính sách $\pi_{\theta_j}$ một lượt, ghi quỹ đạo $\tau_j=(S_0,A_0,\ldots,S_{H-1},A_{H-1})$ và các phần thưởng;
2. tính $\hat g_j=R(\tau_j)\sum_{t=0}^{H-1}\nabla\ln\pi_{\theta_j}(A_t\mid S_t)$;
3. đặt $\theta_{j+1}=\theta_j+\eta_j\hat g_j$.

**Đầu ra.** $\theta_{T+1}$. Thuật toán không cần mô hình của môi trường.
:::

Khi biết $\tau_1,\ldots,\tau_{j-1}$, tham số $\theta_j$ cố định và $\tau_j\sim p_{\theta_j}$, nên $\mathbb E[\hat g_j\mid\tau_1,\ldots,\tau_{j-1}]=\nabla J(\theta_j)$ theo Định lý 10.4; đây là điều kiện không chệch của Bài 05 ở dạng đi lên. Viết mỗi lượt như một hàm của $\theta_j$ và một biến ngẫu nhiên $\xi_j$, với $\xi_1,\xi_2,\ldots$ độc lập cùng phân bố, ta được nguồn ngẫu nhiên và ánh xạ oracle như Định nghĩa 05.10 (Bài tập 10.3). Điều còn thiếu là (C): Định nghĩa 05.10 và Định lý 05.14 cần $-J$ lồi.

::: example Ví dụ 10.7 (Điểm dừng cực tiểu của mục tiêu chính sách)
**Thiết lập.** $H=2$. Từ $s_0$, hành động $1$ đưa tới $s_1$ và hành động $0$ đưa tới $s_2$, tất định. Phần thưởng $r(s_1,1)=1$, $r(s_2,0)=0{,}6$, các phần thưởng khác bằng $0$ (giá trị giả định). Tác tử không phân biệt được các trạng thái, chẳng hạn vì cảm biến cho cùng một số đo, nên dùng một tham số chung: $\pi_\theta(1\mid s)=q=1/(1+e^{-\theta})$ với mọi $s$, $\theta\in\mathbb R$.

**Bước 1: mục tiêu.** Phần thưởng $1$ cần chọn hành động $1$ hai lần, phần thưởng $0{,}6$ cần chọn hành động $0$ hai lần, nên $J=q^2+0{,}6(1-q)^2$.

**Bước 2: điểm dừng.** $\frac{dJ}{dq}=2q-1{,}2(1-q)=3{,}2q-1{,}2$, bằng $0$ tại $q=0{,}375$, tức $\theta=\ln0{,}6\approx-0{,}5108$. Vì $\frac{dJ}{d\theta}=\frac{dJ}{dq}\,q(1-q)$, đạo hàm theo $\theta$ cũng bằng $0$ tại đó.

**Bước 3: loại điểm dừng.** $J$ là hàm bậc hai lồi theo $q$, nên $q=0{,}375$ là điểm cực tiểu, với $J=0{,}375$. Theo $\theta$, đạo hàm bậc hai tại đó bằng $3{,}2\,\big(q(1-q)\big)^2\approx0{,}1758>0$.

**Bước 4: hai điểm xuất phát.** Khi đi lên theo gradient đúng, không ước lượng, từ $\theta=-1$ ($q\approx0{,}2689$), tham số $\theta$ giảm và $J\to0{,}6$. Từ $\theta=-0{,}4$ ($q\approx0{,}4013$), $\theta$ tăng và $J\to1$, cận trên đúng, không đạt.

**Kết luận.** $-J$ không lồi theo $\theta$, nên Định lý 05.14 không áp dụng, và kết quả phụ thuộc điểm xuất phát. Chứng minh Mệnh đề 08.12 chỉ dùng kì vọng và phương sai có điều kiện theo lịch sử, ở đây là các lượt trước. Khi $J$ là $\beta$-trơn và bị chặn trên, ước lượng có phương sai có điều kiện bị chặn và độ dài bước hằng $\eta\le1/\beta$, mệnh đề áp dụng cho $F=-J$, nhưng chỉ bảo đảm điểm dừng xấp xỉ, đúng loại điểm của Bước 3.
:::

Định lý 10.4 không bảo đảm Thuật toán 10.6 tới cực đại của $J$, và theo Ví dụ 10.4, mỗi ước lượng có thể ngược dấu với gradient.

## 6. Tổng phần thưởng từ bước $t$ và giá trị nền

Trong Ví dụ 10.4, đạo hàm bằng $\tfrac38$ còn ước lượng nhận $\pm0{,}75$. Hai cách sửa ước lượng giữ nguyên kì vọng và có thể giảm phương sai: bỏ các phần thưởng nhận trước một hành động khỏi số hạng của hành động đó, và trừ một *giá trị nền* (baseline), tức một đại lượng không phụ thuộc hành động đang xét.

Với $t=0,\ldots,H-1$, *tổng phần thưởng từ bước $t$* (reward-to-go) là $R_{\ge t}=\sum_{t'=t}^{H-1}r_{t'}$, với $R_{\ge0}=R(\tau)$. *Lịch sử* đến bước $t$ là bộ $\mathcal F_t=(S_0,A_0,\ldots,A_{t-1},S_t)$ gồm các biến quan sát được trước $A_t$; kì vọng có điều kiện theo $\mathcal F_t$ là theo bộ này. Ở Bài 05, lịch sử là σ-đại số, và điều kiện hóa trước lần rút thứ $t$ dùng $\mathcal F_{t-1}$ (Bổ đề 05.12); bộ $\mathcal F_t$ ở đây đóng vai đó. Chính sách chỉ nhìn trạng thái hiện tại, nên khi biết $\mathcal F_t$, hành động $A_t$ có phân bố $\pi_\theta(\cdot\mid S_t)$.

::: proposition Mệnh đề 10.7 (Tổng phần thưởng từ bước $t$) — phác thảo (chi tiết ở Phụ lục B)
**Giả thiết.** Như Định lý 10.4.

**Bảo đảm.** Đồng nhất thức, đúng với mọi $\theta\in\Theta$; không có mẫu.

- **(a) Phần thưởng trước hành động.** Với $t'<t$, $\mathbb E\big[r_{t'}\nabla\ln\pi_\theta(A_t\mid S_t)\big]=0$.
- **(b) Ước lượng mới.** $\nabla J(\theta)$ bằng kì vọng của $\sum_{t=0}^{H-1}R_{\ge t}\nabla\ln\pi_\theta(A_t\mid S_t)$.

Mệnh đề không khẳng định ước lượng ở (b) có phương sai nhỏ hơn.
:::

::: proof Chứng minh Mệnh đề 10.7 (phác thảo)
**Lộ trình.** Điều kiện hóa theo lịch sử trước hành động $t$, như Bổ đề 05.12. Đồng nhất thức then chốt là $\sum_a\nabla\pi_\theta(a\mid s)=\nabla1=0$.

**Bước 1 (dùng chính sách chỉ phụ thuộc trạng thái hiện tại).** Khi biết $\mathcal F_t$, $A_t\sim\pi_\theta(\cdot\mid S_t)$. Theo Bổ đề 10.3 cho họ $\pi_\theta(\cdot\mid s)$ trên tập hữu hạn $\mathcal A$,
$$
\begin{aligned}
&\mathbb E\big[\nabla\ln\pi_\theta(A_t\mid S_t)\,\big|\,\mathcal F_t\big]\\
&=\textstyle\sum_a\nabla\pi_\theta(a\mid S_t)=0 .
\end{aligned}
$$

**Bước 2 (tính chất tháp).** Với $t'<t$, $r_{t'}=r(S_{t'},A_{t'})$ là hàm của $\mathcal F_t$, nên đưa được ra ngoài kì vọng có điều kiện; theo Bước 1, $\mathbb E\big[r_{t'}\nabla\ln\pi_\theta(A_t\mid S_t)\big]=0$. Đó là (a).

**Bước 3.** Trong số hạng thứ $t$ của Định lý 10.4, viết $R(\tau)=\sum_{t'<t}r_{t'}+R_{\ge t}$ và bỏ các số hạng có kì vọng $0$ theo (a). Ta được (b).

$\square$ Bước 1–2 được viết bằng tổng trên các lịch sử ở Phụ lục B. Hành động ở bước $t$ không ảnh hưởng tới các phần thưởng nhận trước nó, nên các phần thưởng này chỉ thêm nhiễu vào số hạng của hành động đó.
:::

::: corollary Hệ quả 10.8 (Giá trị nền không làm đổi kì vọng của ước lượng) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Môi trường và chính sách.** Như Định lý 10.4.
- **Giá trị nền.** Với mỗi $t$, một hàm $b_t(\mathcal F_t)$ của lịch sử, thường chỉ phụ thuộc $S_t$; nó không phụ thuộc $A_t$ hay các biến sau $A_t$.
- **Khả tích.** Các tập hữu hạn (mọi kì vọng hữu hạn).

**Bảo đảm.** Đồng nhất thức, đúng với mọi $\theta\in\Theta$:
$$
\begin{aligned}
&\nabla J(\theta)\\
&=\mathbb E\textstyle\sum_{t=0}^{H-1}\big(R_{\ge t}-b_t(\mathcal F_t)\big)\\
&\qquad\cdot\nabla\ln\pi_\theta(A_t\mid S_t).
\end{aligned}
$$
:::

::: proof Chứng minh Hệ quả 10.8
**Lộ trình.** Bước 2 của chứng minh Mệnh đề 10.7 với $b_t(\mathcal F_t)$ thay cho $r_{t'}$; đồng nhất thức then chốt vẫn là $\sum_a\nabla\pi_\theta(a\mid s)=0$.

**Bước 1 (dùng giả thiết giá trị nền).** $b_t(\mathcal F_t)$ là hàm của $\mathcal F_t$, nên theo tính chất tháp và Bước 1 của chứng minh Mệnh đề 10.7,
$$
\begin{aligned}
&\mathbb E\big[b_t(\mathcal F_t)\nabla\ln\pi_\theta(A_t\mid S_t)\big]\\
&=\mathbb E\Big[b_t(\mathcal F_t)\textstyle\sum_a\nabla\pi_\theta(a\mid S_t)\Big]\\
&=0 .
\end{aligned}
$$

**Bước 2.** Trừ các số hạng này khỏi Mệnh đề 10.7(b).

$\square$ Hệ quả cho phép chọn giá trị nền để làm phương sai nhỏ; ví dụ dưới đây cho thấy một lựa chọn tùy ý cũng có thể làm phương sai lớn hơn.
:::

::: example Ví dụ 10.8 (Phương sai với bốn giá trị nền)
**Thiết lập.** Ví dụ 10.4: $\pi_\theta(1)=\tfrac34$, $r(1)=3$, $r(0)=1$. Với hằng số $b$, ước lượng là $\hat g_b=(r(A)-b)(A-\tfrac34)$; theo Hệ quả 10.8, mọi $\hat g_b$ có kì vọng $\tfrac38$.

**Bước 1: công thức phương sai.** $\hat g_b$ bằng $(3-b)\cdot\tfrac14$ với xác suất $\tfrac34$ và $(1-b)(-\tfrac34)$ với xác suất $\tfrac14$, nên
$$
\begin{aligned}
\operatorname{Var}(\hat g_b)&=\tfrac34\big(\tfrac{3-b}4\big)^2+\tfrac14\big(\tfrac{3(1-b)}4\big)^2\\
&\quad-\big(\tfrac38\big)^2 .
\end{aligned}
$$

**Bước 2: bốn giá trị.** Với $b=\tfrac52=J(\ln3)$, hai giá trị là $\tfrac18$ và $\tfrac98$, và phương sai là $\tfrac3{256}+\tfrac{81}{256}-\tfrac{36}{256}=\tfrac3{16}$. Bảng ghi hai giá trị của $\hat g_b$ và phương sai cho cả bốn trường hợp.

| $b$ | $A=1$ | $A=0$ | $\operatorname{Var}\hat g_b$ |
|---|---|---|---|
| $0$ | $\tfrac34$ | $-\tfrac34$ | $\tfrac{27}{64}$ |
| $\tfrac52$ | $\tfrac18$ | $\tfrac98$ | $\tfrac3{16}$ |
| $\tfrac32$ | $\tfrac38$ | $\tfrac38$ | $0$ |
| $5$ | $-\tfrac12$ | $3$ | $\tfrac{147}{64}$ |

**Bước 3: giá trị nền tốt nhất.** Đạo hàm của phương sai theo $b$ là $-\tfrac3{32}(3-b)-\tfrac9{32}(1-b)$, bằng $0$ tại $b^*=\tfrac32$; tổng quát, $b^*=r(1)\big(1-\pi_\theta(1)\big)+r(0)\pi_\theta(1)$. Phương sai bằng $0$ ở đây vì $b^*$ làm hai giá trị của ước lượng bằng nhau.

**Kết luận.** Giá trị nền $b=J$ giảm phương sai từ $\tfrac{27}{64}$ xuống $\tfrac3{16}$ nhưng không tốt nhất, còn $b=5$ làm phương sai tăng hơn năm lần.
:::

::: example Ví dụ 10.9 (Giá trị nền phụ thuộc hành động)
**Thiết lập.** Như Ví dụ 10.8, nhưng giá trị nền là $\kappa A$ với hằng số $\kappa$, phụ thuộc hành động vừa rút.

**Bước 1: kì vọng.** Vì $\mathbb E[A(A-\tfrac34)]=\tfrac34\cdot\tfrac14=\tfrac3{16}$, kì vọng của $(r(A)-\kappa A)(A-\tfrac34)$ là $\tfrac38-\tfrac{3\kappa}{16}$.

**Bước 2: hai giá trị của $\kappa$.** Với $\kappa=1$, kì vọng là $\tfrac3{16}$; với $\kappa=2$, kì vọng là $0$. Với giá trị nền bằng chính $r(A)$, ước lượng luôn bằng $0$.

**Kết luận.** $\kappa A$ không là hàm của lịch sử trước hành động, nên Bước 1 của chứng minh Hệ quả 10.8 hỏng và ước lượng bị chệch.
:::

::: example Ví dụ 10.10 (Tổng phần thưởng từ bước $t$ trên quá trình hai bước)
**Thiết lập.** Ví dụ 10.2 tại $\theta=0$. Ba ước lượng một lượt: (i) $\hat g$ của Định lý 10.4; (ii) ước lượng của Mệnh đề 10.7(b); (iii) như (ii), trừ giá trị nền $b_t(\mathcal F_t)$ bằng tổng phần thưởng kì vọng còn lại từ trạng thái hiện tại: $1{,}75$ ở $s_0$, $2$ ở $s_1$, $\tfrac12$ ở $s_2$ (Ví dụ 10.2, Bước 2 và 4). Cả ba có kì vọng $(-0{,}025;\,0{,}25;\,-0{,}125)$ theo Định lý 10.4, Mệnh đề 10.7 và Hệ quả 10.8. Bước 3 dùng một biến thể của quá trình, nêu tại chỗ.

**Bước 1: một phương sai.** Tọa độ $\theta_{s_1}$ của (ii), $r_1(A_1-\tfrac12)$ trên các quỹ đạo qua $s_1$, nhận $\tfrac32$ và $-\tfrac12$ với xác suất $\tfrac14$ mỗi giá trị và $0$ với xác suất $\tfrac12$; phương sai của nó là $\tfrac{10}{16}-\tfrac1{16}=0{,}5625$.

**Bước 2: bảng phương sai.** Tính như Bước 1 trên tám quỹ đạo (bảng của Ví dụ 10.2, Bước 1):

| | $\theta_{s_0}$ | $\theta_{s_1}$ | $\theta_{s_2}$ |
|---|---|---|---|
| (i) | $\tfrac{1619}{1600}$ | $\tfrac{11}{16}$ | $\tfrac{79}{320}$ |
| (ii) | $\tfrac{1619}{1600}$ | $\tfrac9{16}$ | $\tfrac3{64}$ |
| (iii) | $\tfrac{197}{800}$ | $\tfrac1{16}$ | $\tfrac1{64}$ |

Cột $\theta_{s_0}$ của (i) và (ii) trùng nhau vì $R_{\ge0}=R(\tau)$. Tổng ba phương sai, tức vết của ma trận hiệp phương sai, là $1{,}94625$; $1{,}62125$; $0{,}324375$: giá trị nền theo trạng thái giảm nó sáu lần so với (i) và khoảng năm lần so với (ii).

**Bước 3: một trường hợp phương sai tăng.** Đổi ví dụ: ở $s_0$, cả hai hành động cho phần thưởng $-2$ và đưa tới $s_1$, xác suất chọn ở $s_0$ không phụ thuộc $\theta$; ở $s_1$, phần thưởng là $3$ và $1$, $\theta=0$. Gradient chỉ có tọa độ $\theta_{s_1}$. Ước lượng (i) bằng $(-2+3)\cdot\tfrac12=\tfrac12$ hoặc $(-2+1)(-\tfrac12)=\tfrac12$, phương sai $0$. Ước lượng (ii) bằng $3\cdot\tfrac12=\tfrac32$ hoặc $1\cdot(-\tfrac12)=-\tfrac12$, với kì vọng $\tfrac12$ và phương sai $\tfrac12(\tfrac94+\tfrac14)-\tfrac14=1$. Phần thưởng $-2$ ở bước đầu đóng vai giá trị nền tốt nhất cho bước sau, $b^*=3\cdot\tfrac12+1\cdot\tfrac12=2$ theo công thức của Ví dụ 10.8.

**Kết luận.** Cùng một kì vọng, phương sai có thể giảm (Bước 2) hoặc tăng (Bước 3) tùy bài toán.
:::

::: remark Nhận xét 10.9 (Giá trị nền có tham số và giá trị nền tính từ chính lượt đang dùng)
(i) Giá trị nền $b_\vartheta(S_t)$ với tham số riêng $\vartheta$, cố định khi sinh lượt, giữ ước lượng không chệch. Khi cài đặt, ước lượng thường được tính bằng gradient theo $\theta$ của $\big(R_{\ge t}-b\big)\ln\pi_\theta(A_t\mid S_t)$. Nếu giá trị nền dùng chung tham số với chính sách, $b=b_\theta(S_t)$, gradient này có thêm số hạng $-\nabla b_\theta(S_t)\ln\pi_\theta(A_t\mid S_t)$. Kì vọng có điều kiện của số hạng đó bằng $\nabla b_\theta(S_t)$ nhân entropy $\mathrm H\big(\pi_\theta(\cdot\mid S_t)\big)$, tức $\ln2\approx0{,}6931$ với bài toán bandit hai hành động, $b_\theta=\theta$, $\theta=0$. Do đó giá trị nền phải được coi là hằng số khi lấy đạo hàm.

(ii) Giá trị nền dùng hành động hay phần thưởng từ bước $t$ trở đi của chính lượt đang dùng, chẳng hạn $R(\tau)$ hay $r(A_t)$, không là hàm của $\mathcal F_t$, nên vi phạm giả thiết của Hệ quả 10.8. Phần thưởng nhận trước bước $t$ thì hợp lệ, như phần thưởng $-2$ ở Ví dụ 10.10, Bước 3. Trung bình phần thưởng của các lượt trước là hằng số khi biết các lượt đó, nên cũng hợp lệ; ví dụ dưới đây dùng nó.
:::

::: example Ví dụ 10.11 (Dịch phần thưởng trong bài toán đề xuất)
**Thiết lập.** Khối ứng dụng ở §3 tại $\theta=0$. Với $H=1$, tổng phần thưởng là $R(\tau)=c+X$, với nhấp $X\in\{0,1\}$ và $c\in\{0,10\}$. Ước lượng một lượt $(R(\tau)-b)(A-\tfrac12)$, với hằng số $b$, không chệch dù phần thưởng ngẫu nhiên (đoạn sau Định nghĩa 10.1); đó là câu trả lời cho câu (i).

**Bước 1: gradient không đổi.** $J(\theta)=c+0{,}6\,\pi_\theta(1)+0{,}4\big(1-\pi_\theta(1)\big)$, nên $J'(0)=0{,}2\cdot\tfrac14=0{,}05$ với mọi $c$. Cộng $c$ chỉ dịch $J$: trong họ sigmoid, $J$ vẫn tăng theo $\theta$ và tiến tới cận trên đúng $c+0{,}6$ khi $\pi_\theta(1)\to1$.

**Bước 2: phương sai khi $b=0$.** Vì $(A-\tfrac12)^2=\tfrac14$, phương sai bằng $\tfrac14\mathbb ER(\tau)^2-0{,}05^2$. Ta có $\mathbb EX=\tfrac12$ và $X^2=X$, nên $\mathbb E(c+X)^2=c^2+c+\tfrac12$. Do đó
$$
\begin{aligned}
&c=0\colon\ \tfrac14\cdot\tfrac12-0{,}0025\\
&\qquad=0{,}1225,\\
&c=10\colon\ \tfrac14\cdot110{,}5-0{,}0025\\
&\qquad=27{,}6225 .
\end{aligned}
$$

**Bước 3: phương sai khi $b=J(0)=c+\tfrac12$.** Khi đó $(R(\tau)-b)^2(A-\tfrac12)^2=\tfrac14(X-\tfrac12)^2$, có kì vọng $\tfrac1{16}$, nên phương sai bằng $0{,}0625-0{,}0025=0{,}06$ với cả hai giá trị của $c$.

**Bước 4: thí nghiệm của học phần** (Phụ lục C). Chạy $100$ lần Thuật toán 10.6, với $R(\tau_j)$ thay bằng $R(\tau_j)-b_j$ khi có giá trị nền $b_j$, trung bình phần thưởng các lượt trước. Với $c=10$ và không giá trị nền, $49$ lần chạy kết thúc với xác suất chọn nội dung $1$ dưới $0{,}5$; có giá trị nền, hay với $c=0$, không lần nào.

**Kết luận.** Dịch phần thưởng không đổi bài toán nhưng nhân phương sai của ước lượng một lượt khoảng $225$ lần.
:::

Các kết quả trên là đồng nhất thức. Khi chính sách cố định, các lượt thỏa (T1), và bất đẳng thức Hoeffding cho một cận với xác suất cao.

::: example Ví dụ 10.12 (Cận Hoeffding cho đánh giá một chính sách cố định)
**Thiết lập.** Ví dụ 10.2 với một $\theta$ cố định trước khi chạy; $m=1000$ lượt độc lập; $\delta=0{,}05$. Tổng phần thưởng $R(\tau_j)\in[0,4]$, vì phần thưởng ở bước đầu thuộc $\{0,1\}$ và ở bước sau thuộc $\{0,1,3\}$.

**Bước 1: tính độc lập.** Với $\theta$ cố định, $R(\tau_1),\ldots,R(\tau_m)$ độc lập cùng phân bố với kì vọng $J(\theta)$, tức thỏa (T1).

**Bước 2: bán kính.** Áp dụng Hệ quả 02.10(b) cho $R(\tau_j)/4\in[0,1]$ rồi nhân bán kính với $4$ (đoạn sau Nhận xét 02.8):
$$
\begin{aligned}
4\sqrt{\ln40/2000}&\approx4\cdot0{,}042947\\
&\le0{,}1718 .
\end{aligned}
$$
Với xác suất ít nhất $0{,}95$ theo các lượt, trung bình $\frac1m\sum_jR(\tau_j)$ cách $J(\theta)$ không quá $0{,}1718$.

**Bước 3: cỡ mẫu.** Bán kính không quá $0{,}05$ khi $4\sqrt{\ln40/(2m)}\le0{,}05$, tức $m\ge16\ln40/(2\cdot0{,}05^2)\approx11\,804{,}4$; cần ít nhất $11\,805$ lượt.

**Bước 4: giả thiết bị vi phạm.** Nếu $\theta$ do Thuật toán 10.6 chọn từ chính các lượt này, $\theta$ phụ thuộc mẫu như giả thuyết chọn theo mẫu (Nhận xét 01.9), và cận không áp dụng.

**Kết luận.** Đánh giá một chính sách cố định là bài toán ước lượng trung bình như ở Bài 02.
:::

## 7. Giao thức học liên tục và ma trận đánh giá

Ở tình huống thứ hai của câu hỏi mở đầu, mỗi môi trường là một nhiệm vụ với phân bố riêng, và dữ liệu đến theo thứ tự. Để so sánh các phương pháp, chúng ta cần nói rõ thuật toán được phép giữ gì từ các nhiệm vụ trước, và kết quả được đo ở đâu, lúc nào.

::: definition Định nghĩa 10.10 (Giao thức học liên tục)
Cho tập quan sát $\mathcal Z$, tập tham số $W$, hàm lỗi $\ell$ thỏa (T2) và số nhiệm vụ $K\ge2$. Một *giao thức học liên tục* gồm các thành phần sau.

- **Dãy nhiệm vụ.** Các phân bố $D_1,\ldots,D_K$ trên $\mathcal Z$; cố định, chưa biết. Nhiệm vụ $k$ có rủi ro kì vọng $L_k(w)=L_{D_k}(w)$.
- **Dữ liệu.** Mẫu $S^{(k)}\sim D_k^{m_k}$ của nhiệm vụ $k$, độc lập với các mẫu khác, đến theo thứ tự $k=1,\ldots,K$.
- **Ngân sách bộ nhớ** (memory budget). Số $M\ge0$: khi học nhiệm vụ $k$, thuật toán thấy $S^{(k)}$, tham số hiện tại và không quá $M$ quan sát cũ.
- **Tham số.** $w^{(0)}$ là tham số khởi tạo; $w^{(k)}$ là tham số sau nhiệm vụ $k$.
- **Định danh nhiệm vụ** (task identity). Quy định thuật toán có được biết quan sát thuộc nhiệm vụ nào khi dự đoán hay không.
- **Đánh giá.** Một mẫu kiểm tra cho mỗi nhiệm vụ, độc lập với mọi dữ liệu huấn luyện và với bộ nhớ.
:::

Các mẫu, bộ nhớ, nguồn ngẫu nhiên của thuật toán và các mẫu kiểm tra là ngẫu nhiên. Hai giao thức chỉ khác $M$ hay định danh nhiệm vụ là hai bài toán khác nhau. Tình huống thứ hai của câu hỏi mở đầu là một giao thức với $K=2$, $M=0$. Huấn luyện một lần trên mọi dữ liệu có sẵn từ đầu là tối thiểu hóa rủi ro thực nghiệm cho rủi ro trung bình $\frac1K\sum_kL_k$ (khi các mẫu cùng cỡ), không phải học liên tục.

::: definition Định nghĩa 10.11 (Ma trận đánh giá và các độ đo của học liên tục)
Cho một giao thức học liên tục với $K$ nhiệm vụ và các tham số $w^{(1)},\ldots,w^{(K)}$.

- **Ma trận đánh giá** (evaluation matrix). $\mathrm{acc}_{k,i}$ là *độ chính xác phân lớp* của $w^{(k)}$ trên mẫu kiểm tra của nhiệm vụ $i$, tức $1$ trừ rủi ro thực nghiệm với hàm lỗi 0–1 trên mẫu đó; $\mathrm{acc}^\circ_i$ là độ chính xác phân lớp của mô hình huấn luyện từ $w^{(0)}$ chỉ trên nhiệm vụ $i$.
- **Độ chính xác phân lớp trung bình cuối cùng** (final average accuracy). $\frac1K\sum_{i=1}^K\mathrm{acc}_{K,i}$.
- **Chuyển đổi ngược** (backward transfer). $\frac1{K-1}\sum_{i=1}^{K-1}(\mathrm{acc}_{K,i}-\mathrm{acc}_{i,i})$; âm khi các nhiệm vụ sau làm giảm độ chính xác phân lớp trên nhiệm vụ cũ.
- **Chuyển đổi xuôi** (forward transfer). $\frac1{K-1}\sum_{i=2}^{K}(\mathrm{acc}_{i,i}-\mathrm{acc}^\circ_i)$; dương khi các nhiệm vụ trước giúp học nhiệm vụ $i$.
- **Độ quên** (forgetting measure). Với $i<K$, $\max_{i\le k\le K}\mathrm{acc}_{k,i}-\mathrm{acc}_{K,i}\ge0$, từ đỉnh đến cuối; độ quên trung bình lấy trên $i=1,\ldots,K-1$.
:::

Mỗi $\mathrm{acc}_{k,i}$ là một ước lượng trên mẫu kiểm tra độc lập với $w^{(k)}$, nên Hệ quả 02.10 cho một khoảng tin cậy cho từng ô. Với hàm lỗi khác, ta thay $\mathrm{acc}$ bằng rủi ro kiểm tra và đổi chiều các so sánh. Các công thức ở trên là quy ước của học phần; ví dụ dưới đây cho thấy một quy ước gần với quy ước này cho độ quên âm.

*Quên thảm họa* (catastrophic forgetting) chỉ trường hợp độ chính xác phân lớp trên một nhiệm vụ cũ giảm về gần mức của một mô hình chưa học nhiệm vụ đó.

::: example Ví dụ 10.13 (Ma trận đánh giá của ba nhiệm vụ)
**Thiết lập.** $K=3$; ma trận đánh giá cho trong bảng, hàng là thời điểm $k$, cột là nhiệm vụ $i$; $\mathrm{acc}^\circ=(0{,}85;\,0{,}90;\,0{,}85)$. Mọi số là giá trị giả định. Bước 5 dùng ma trận thứ hai, chỉ khác hàng 3.

| $k$ | $i=1$ | $i=2$ | $i=3$ |
|---|---|---|---|
| $1$ | $0{,}85$ | $0{,}30$ | $0{,}40$ |
| $2$ | $0{,}90$ | $0{,}92$ | $0{,}45$ |
| $3$ | $0{,}80$ | $0{,}75$ | $0{,}88$ |

**Bước 1: độ chính xác phân lớp trung bình cuối cùng.** $(0{,}80+0{,}75+0{,}88)/3=0{,}81$.

**Bước 2: chuyển đổi ngược.** $\tfrac12\big[(0{,}80-0{,}85)+(0{,}75-0{,}92)\big]=-0{,}11$.

**Bước 3: độ quên.** Nhiệm vụ 1 đạt đỉnh $0{,}90$ ở hàng 2, nên độ quên là $0{,}90-0{,}80=0{,}10$; nhiệm vụ 2: $0{,}92-0{,}75=0{,}17$; trung bình $0{,}135$.

**Bước 4: chuyển đổi xuôi.** $\tfrac12\big[(0{,}92-0{,}90)+(0{,}88-0{,}85)\big]=0{,}025$.

**Bước 5: ma trận thứ hai.** Đổi hàng 3 thành $(0{,}83;\,0{,}95;\,0{,}88)$. Chuyển đổi ngược thành $\tfrac12\big[(0{,}83-0{,}85)+(0{,}95-0{,}92)\big]=0{,}005$; độ quên, lấy cực đại tới hàng $K$, là $0{,}07$ và $0$. Lấy cực đại chỉ tới hàng $K-1$ cho độ quên âm $0{,}92-0{,}95=-0{,}03$ ở nhiệm vụ 2.

**Kết luận.** Độ quên trung bình $0{,}135$ khác đối của chuyển đổi ngược vì nhiệm vụ 1 đạt đỉnh sau khi học nhiệm vụ 2. Với ma trận thứ hai, độ quên ở nhiệm vụ 2 bằng $0$ hay $-0{,}03$ tùy hàng cuối của phép lấy cực đại.
:::

Ma trận đánh giá chỉ ghi độ chính xác phân lớp của các tham số mà một thuật toán đi qua; nó không cho biết tham số nào có rủi ro nhỏ trên mọi nhiệm vụ cùng lúc.

## 8. Hai nhiệm vụ xung đột, chính quy hóa tham số và phát lại

Ở câu hỏi mở đầu, huấn luyện tiếp chỉ trên môi trường B đưa rủi ro trên môi trường A từ $0$ lên $\tfrac12$. Hai nhiệm vụ *xung đột* khi không tham số nào cực tiểu hóa đồng thời hai rủi ro. Hai cách giữ rủi ro trên nhiệm vụ cũ nhỏ là phạt độ lệch khỏi tham số cũ và trộn dữ liệu cũ vào lúc huấn luyện.

::: definition Định nghĩa 10.12 (Phát lại và chính quy hóa tham số)
Cho một giao thức học liên tục, nhiệm vụ đang học $k\ge2$, tham số $w^{(k-1)}\in W\subseteq\mathbb R^p$ và rủi ro thực nghiệm $L_{S^{(k)}}$ của nhiệm vụ $k$.

- **Phát lại** (replay). Một *bộ đệm phát lại* (replay buffer) $\mathcal B$ gồm không quá $M$ quan sát của các nhiệm vụ trước; $w^{(k)}$ là một điểm cực tiểu, đúng hay gần đúng, của $(1-\alpha)L_{S^{(k)}}(w)+\alpha L_{\mathrm{buf}}(w)$, với *tỉ lệ phát lại* $\alpha\in[0,1)$ chọn trước và $L_{\mathrm{buf}}$ là rủi ro thực nghiệm trên $\mathcal B$.
- **Chính quy hóa tham số** (parameter regularization). $w^{(k)}$ là một điểm cực tiểu của $L_{S^{(k)}}(w)+\frac\lambda2(w-w^{(k-1)})^\top\Omega(w-w^{(k-1)})$, với $\lambda\ge0$ và ma trận $\Omega$ đối xứng nửa xác định dương, thường là đường chéo với các phần tử gọi là *trọng số tầm quan trọng* (importance weight); $\Omega=I$, ma trận đơn vị, cho phạt bình phương khoảng cách.
- **Tinh chỉnh** (fine-tuning). Trường hợp $\alpha=0$ hoặc $\lambda=0$: chỉ dùng dữ liệu mới, xuất phát từ $w^{(k-1)}$.
:::

Phát lại cần $M>0$; chính quy hóa tham số chỉ cần lưu $w^{(k-1)}$ và $\Omega$. Với $M$ hữu hạn, $L_{\mathrm{buf}}$ chỉ xấp xỉ rủi ro cũ. Bộ đệm $\mathcal B$ khác bán kính $B$ của Bài 05.

::: proposition Mệnh đề 10.13 (Hai nhiệm vụ xung đột buộc một đánh đổi) — chứng minh đầy đủ
**Giả thiết.** Ba thành phần sau.

- **Hai nhiệm vụ.** $W=\mathbb R$; rủi ro kì vọng $L_A(w)=w^2/2$ và $L_B(w)=(w-1)^2/2$ cho trước, không có mẫu.
- **Tham số cũ.** $w^{(1)}=0$, điểm cực tiểu của $L_A$.
- **Chính quy hóa.** $\lambda\ge0$ và $\Omega=1$.

**Bảo đảm.** Tất định, với các rủi ro kì vọng cho trước.

- **(a) Cận dưới.** Với mọi $w\in\mathbb R$, $\sqrt{2L_A(w)}+\sqrt{2L_B(w)}\ge1$ và $L_A(w)+L_B(w)\ge\tfrac14$, dấu bằng ở bất đẳng thức sau chỉ tại $w=\tfrac12$. Không $w$ nào làm cả hai rủi ro bằng $0$.
- **(b) Tinh chỉnh.** Cực tiểu hóa $L_B$ cho $w=1$ và $L_A(1)=\tfrac12$.
- **(c) Chính quy hóa tham số.** $L_B(w)+\frac\lambda2w^2$ có điểm cực tiểu duy nhất $w_\lambda=\frac1{1+\lambda}$, với $L_A(w_\lambda)=\frac1{2(1+\lambda)^2}$ giảm theo $\lambda$ và $L_B(w_\lambda)=\frac{\lambda^2}{2(1+\lambda)^2}$ tăng theo $\lambda$.
- **(d) Phát lại với rủi ro cũ đầy đủ.** $(1-\alpha)L_B(w)+\alpha L_A(w)$ có điểm cực tiểu $1-\alpha$, trùng $w_\lambda$ khi $\alpha=\frac\lambda{1+\lambda}$.
:::

::: proof Chứng minh Mệnh đề 10.13
**Lộ trình.** Bất đẳng thức tam giác cho phần đầu của (a); hoàn thành bình phương và đạo hàm của hàm bậc hai lồi ngặt cho phần còn lại.

**Bước 1: phần (a).** $\sqrt{2L_A(w)}=\lvert w\rvert$, $\sqrt{2L_B(w)}=\lvert w-1\rvert$, và theo bất đẳng thức tam giác $\lvert w\rvert+\lvert1-w\rvert\ge1$. Hoàn thành bình phương:
$$
\begin{aligned}
&L_A(w)+L_B(w)\\
&=\tfrac12\big(w^2+(w-1)^2\big)\\
&=\big(w-\tfrac12\big)^2+\tfrac14,
\end{aligned}
$$
nhỏ nhất bằng $\tfrac14$, chỉ tại $w=\tfrac12$; hai rủi ro không thể cùng bằng $0$.

**Bước 2: phần (b) và (c).** $L_B$ nhỏ nhất tại $w=1$, với $L_A(1)=\tfrac12$. Đạo hàm của $L_B(w)+\frac\lambda2w^2$ là $(w-1)+\lambda w$, bằng $0$ tại $w_\lambda=\frac1{1+\lambda}$, và đạo hàm bậc hai $1+\lambda>0$. Thay $w_\lambda$ và $w_\lambda-1=-\frac\lambda{1+\lambda}$ vào $L_A$, $L_B$.

**Bước 3: phần (d).** Đạo hàm $(1-\alpha)(w-1)+\alpha w$ bằng $0$ tại $w=1-\alpha$, bằng $\frac1{1+\lambda}$ khi $\alpha=\frac\lambda{1+\lambda}$.

$\square$ Phạt $\frac\lambda2w^2$ đúng bằng $\lambda L_A(w)$, vì $L_A$ là hàm bậc hai có tâm $w^{(1)}$ và độ cong $1$; do đó (c) và (d) cho cùng điểm cực tiểu.
:::

Mệnh đề 10.13 chỉ xét hai hàm bậc hai; nó không nói gì về phương pháp học liên tục cho mạng nơ-ron. Ta gọi *tính bền vững* (stability) là việc rủi ro trên nhiệm vụ cũ ít tăng, và *tính mềm dẻo* (plasticity) là việc rủi ro trên nhiệm vụ mới nhỏ. Theo (a), không điểm nào làm cả hai rủi ro bằng $0$; theo (c), tăng $\lambda$ làm $L_A$ giảm và $L_B$ tăng. Hiện tượng này được gọi là *đánh đổi bền vững–mềm dẻo* (stability–plasticity trade-off); $\lambda$ hay $\alpha$ chỉ chọn một vị trí trên đánh đổi đó. "Bền vững" ở đây khác tính ổn định của thuật toán ở Bài 06 và Bài 08.

::: example Ví dụ 10.14 (Năm hệ số chính quy hóa)
**Thiết lập.** Mệnh đề 10.13(c) với $\lambda\in\{0,\tfrac13,1,3,9\}$.

**Bước 1: điểm cực tiểu và hai rủi ro.** Với $\lambda=\tfrac13$: $w_\lambda=\tfrac34$, $L_A=\tfrac12\cdot\tfrac9{16}=\tfrac9{32}$, $L_B=\tfrac12\cdot\tfrac1{16}=\tfrac1{32}$. Bảng ghi cả năm giá trị.

| $\lambda$ | $w_\lambda$ | $L_A(w_\lambda)$ | $L_B(w_\lambda)$ |
|---|---|---|---|
| $0$ | $1$ | $\tfrac12$ | $0$ |
| $\tfrac13$ | $\tfrac34$ | $\tfrac9{32}$ | $\tfrac1{32}$ |
| $1$ | $\tfrac12$ | $\tfrac18$ | $\tfrac18$ |
| $3$ | $\tfrac14$ | $\tfrac1{32}$ | $\tfrac9{32}$ |
| $9$ | $\tfrac1{10}$ | $\tfrac1{200}$ | $\tfrac{81}{200}$ |

**Bước 2: tổng hai rủi ro.** Theo thứ tự trong bảng: $\tfrac12$; $\tfrac5{16}$; $\tfrac14$; $\tfrac5{16}$; $\tfrac{41}{100}$. Tổng nhỏ nhất $\tfrac14$ đạt tại $\lambda=1$, đúng cận dưới của Mệnh đề 10.13(a).

**Bước 3: phát lại tương ứng.** $\alpha=\lambda/(1+\lambda)$ lần lượt bằng $0$; $\tfrac14$; $\tfrac12$; $\tfrac34$; $\tfrac9{10}$.

**Kết luận.** Tăng $\lambda$ đổi rủi ro trên nhiệm vụ mới lấy rủi ro trên nhiệm vụ cũ, và không giá trị nào cho cả hai bằng $0$; chọn $\lambda$ cần một tiêu chí nêu trước, như các độ đo của §7.
:::

::: remark Nhận xét 10.14 (Phạt bậc hai có trọng số theo tầm quan trọng) — đọc thêm
(i) Cho một mô hình xác suất $p_w(y\mid x)$ trên tập nhãn hữu hạn, với hàm lỗi log như Bài 09. *Ma trận thông tin Fisher* (Fisher information matrix) của nhiệm vụ A tại $w^{(1)}$ là
$$
\begin{aligned}
\mathcal I_A&=\mathbb E\big[\nabla\ln p_w(Y\mid X)\\
&\qquad\cdot\nabla\ln p_w(Y\mid X)^\top\big],
\end{aligned}
$$
với gradient theo $w$ tại $w^{(1)}$, $X$ theo phân bố đầu vào của nhiệm vụ A và $Y\sim p_{w^{(1)}}(\cdot\mid X)$. Theo Bổ đề 10.3(b), gradient log có kì vọng $0$ khi biết $X$, nên $\mathcal I_A$ là ma trận hiệp phương sai của nó. Với hai nhiệm vụ, phương pháp *củng cố trọng số đàn hồi* (elastic weight consolidation, EWC) của Kirkpatrick và cộng sự (2017) là chính quy hóa tham số với $\Omega$ là đường chéo của ma trận Fisher. Các tác giả dẫn ra phép phạt này từ một *xấp xỉ Laplace* (Laplace approximation) cho phân bố hậu nghiệm sau nhiệm vụ A.

(ii) Khi $\lambda\Omega$ bằng ma trận Hesse của rủi ro cũ tại $w^{(1)}$, phạt bậc hai là phần bậc hai của khai triển Taylor quanh điểm cực tiểu $w^{(1)}$. Với hàm lỗi log và mô hình chứa phân bố thật, tại tham số thật, ma trận Fisher bằng ma trận Hesse của rủi ro. Bỏ các phần tử ngoài đường chéo có thể làm mất tính mềm dẻo, như ví dụ dưới đây.
:::

::: example Ví dụ 10.15 (Phạt đường chéo trên hai tham số)
**Thiết lập.** $W=\mathbb R^2$, $L_A(w)=\tfrac12(w_1+w_2)^2$, $L_B(w)=\tfrac12(w_1-w_2-2)^2$ (hàm giả định); $w^{(1)}=(0,0)$, một điểm cực tiểu của $L_A$.

**Bước 1: hai nhiệm vụ không xung đột.** Tại $w=(1,-1)$, cả hai rủi ro bằng $0$.

**Bước 2: phạt đầy đủ.** Ma trận Hesse của $L_A$ là $\begin{pmatrix}1&1\\1&1\end{pmatrix}$, và phạt bậc hai với $\Omega$ bằng ma trận này là $\frac\lambda2(w_1+w_2)^2=\lambda L_A(w)$. Với mọi $\lambda>0$, điểm $(1,-1)$ làm cả hai số hạng bằng $0$, nên là điểm cực tiểu.

**Bước 3: phạt đường chéo.** Đường chéo của ma trận Hesse cho $\Omega=I$: cực tiểu hóa $\tfrac12(w_1-w_2-2)^2+\tfrac\lambda2(w_1^2+w_2^2)$. Với $\lambda>0$, hàm này lồi ngặt và không đổi khi thay $(w_1,w_2)$ bằng $(-w_2,-w_1)$, nên điểm cực tiểu duy nhất có dạng $(v,-v)$. Thay $w=(v,-v)$: số hạng thứ nhất thành $\tfrac12(2v-2)^2=2(v-1)^2$, số hạng phạt thành $\lambda v^2$; đạo hàm theo $v$ bằng $0$ tại $v=\frac2{2+\lambda}$.

**Bước 4: hai giá trị.** Tại điểm cực tiểu, $L_A=0$ và $L_B=2(v-1)^2$. Với $\lambda=1$: $v=\tfrac23$, $L_B=\tfrac29\approx0{,}2222$. Với $\lambda=4$: $v=\tfrac13$, $L_B=\tfrac89\approx0{,}8889$.

**Kết luận.** Phạt đường chéo phạt cả hướng $(1,-1)$, dọc theo đó $L_A$ không đổi, nên tạo ra một đánh đổi không có trong bài toán gốc.
:::

::: example Ví dụ 10.16 (Phát lại với bộ đệm hữu hạn)
**Thiết lập.** Nhiệm vụ A: $Z\sim N(0,1)$, $\ell(w,z)=\tfrac12(w-z)^2$, nên $L_A(w)=\tfrac12(w^2+1)$, nhỏ nhất bằng $\tfrac12$. Nhiệm vụ B có rủi ro $L_B(w)=\tfrac12(w-1)^2$, coi như biết đủ. Tỉ lệ phát lại $\alpha=\tfrac12$. Bộ đệm gồm $M$ quan sát độc lập $Z_1,\ldots,Z_M$ của nhiệm vụ A, nguồn ngẫu nhiên duy nhất.

**Bước 1: rủi ro cũ đầy đủ.** Điểm cực tiểu của $\tfrac12L_B+\tfrac12L_A$ là $w=\tfrac12$, với $L_A(\tfrac12)=\tfrac58$.

**Bước 2: bộ đệm $M$ quan sát.** Với $L_{\mathrm{buf}}(w)=\frac1M\sum_i\tfrac12(w-Z_i)^2$, đạo hàm của $\tfrac12L_B+\tfrac12L_{\mathrm{buf}}$ là $\tfrac12(w-1)+\tfrac12(w-\bar Z_M)$, với $\bar Z_M$ là trung bình của bộ đệm. Điểm cực tiểu là $w_M=\tfrac12+\tfrac12\bar Z_M$.

**Bước 3: độ lệch theo kì vọng.** Vì $\mathbb Ew_M=\tfrac12$ và $\operatorname{Var}\bar Z_M=1/M$,
$$
\begin{aligned}
&\mathbb EL_A(w_M)-L_A(\tfrac12)\\
&=\tfrac12\big(\mathbb Ew_M^2-\tfrac14\big)\\
&=\tfrac12\operatorname{Var}(w_M)=\tfrac1{8M}.
\end{aligned}
$$
Với $M=1$, $10$, $100$: $0{,}125$; $0{,}0125$; $0{,}00125$. Với tỉ lệ $\alpha$ bất kì, $w_M=(1-\alpha)+\alpha\bar Z_M$ và độ lệch là $\alpha^2/(2M)$.

**Kết luận.** Rủi ro cũ kì vọng là $\tfrac58+\tfrac1{8M}$; nó giảm về giá trị $\tfrac58$ của điểm thỏa hiệp khi $M$ tăng, không về $\min L_A=\tfrac12$. Thí nghiệm của học phần (Phụ lục C) dùng một mô hình hồi quy khác, có rủi ro tổng thể trên A là $\tfrac12(w^2+0{,}25)$. Sau nhiệm vụ B, rủi ro kiểm tra trên A giảm từ $0{,}624$ khi tinh chỉnh xuống $0{,}331$; $0{,}256$; $0{,}252$ với $M=5$, $50$, $1000$, về giá trị $0{,}25$ của điểm thỏa hiệp, không về $0{,}125$.
:::

Mọi rủi ro cũ trong §8 là hàm bậc hai; với rủi ro khác, phạt bậc hai chỉ xấp xỉ rủi ro cũ quanh $w^{(1)}$.

## 9. Học trực tuyến, hối tiếc và độ quên

*Học trực tuyến* (online learning; UML Chương 21) cũng xét dữ liệu đến theo thời gian, nhưng đo thuật toán bằng *hối tiếc* (regret). Chúng ta cần biết hối tiếc nhỏ có kéo theo độ quên nhỏ không.

::: definition Định nghĩa 10.15 (Học trực tuyến và hối tiếc tĩnh)
Cho tập tham số $W\subseteq\mathbb R^p$ khác rỗng, đóng, lồi, hàm lỗi $\ell$ và số vòng $T$. Học trực tuyến gồm các thành phần sau.

- **Dãy quan sát.** $z_1,\ldots,z_T\in\mathcal Z$ tùy ý, có thể do một đối thủ chọn; không có giả thiết thống kê.
- **Vòng $t$.** Thuật toán chọn $w_t\in W$ chỉ dựa vào $z_1,\ldots,z_{t-1}$, rồi nhận $z_t$ và chịu hàm lỗi $\ell(w_t,z_t)$.
- **Hối tiếc.** Với điểm so sánh $u\in W$ cố định, $\mathrm{Regret}_T(u)=\sum_{t=1}^T\ell(w_t,z_t)-\sum_{t=1}^T\ell(u,z_t)$; *hối tiếc tĩnh* (static regret) là $\sup_{u\in W}\mathrm{Regret}_T(u)$.
:::

Hối tiếc "tĩnh" dùng một điểm so sánh cho cả $T$ vòng. Khi nó tăng chậm hơn $T$, hàm lỗi trung bình theo thời gian vượt hàm lỗi trung bình của điểm cố định tốt nhất không quá một lượng tiến về $0$, và có thể thấp hơn. Nó khác rủi ro vượt mức (Định nghĩa 01.24), một kì vọng theo một $D$, và khác độ quên (Định nghĩa 10.11), đo trên dữ liệu cũ sau khi học xong. Chữ $t$ ở đây là vòng của thuật toán, như Bài 05.

::: remark Nhận xét 10.16 (Cận hối tiếc của hạ gradient trực tuyến)
**Giả thiết.** $\ell(\cdot,z)$ lồi với mọi $z$; $w_1\in W$ tất định; $w_{t+1}=\operatorname{proj}_W(w_t-\eta v_t)$ với $v_t\in\partial\ell(w_t,z_t)$ và $\lVert v_t\rVert\le G$ với mọi $t$.

**Bảo đảm.** Tất định, với mọi dãy $z_1,\ldots,z_T$ và mọi $u\in W$ có $\lVert w_1-u\rVert\le R$:
$$
\mathrm{Regret}_T(u)\le\frac{R^2}{2\eta}+\frac{\eta G^2T}2,
$$
và vế phải bằng $RG\sqrt T$ khi $\eta=R/(G\sqrt T)$, như Hệ quả 05.15. Chứng minh cộng bất đẳng thức một bước (Mệnh đề 05.13) cho hàm $\ell(\cdot,z_t)$ ở vòng $t$, như chứng minh Định lý 05.14 nhưng không lấy kì vọng (UML §21.3, với $w_1=0$).
:::

::: remark Nhận xét 10.17 (Học trực tuyến, học liên tục và dịch chuyển phân bố)
Ba khái niệm sau chồng lên nhau nhưng không đồng nghĩa.

- **Học trực tuyến.** Một dãy quyết định, đo bằng hối tiếc so với một điểm cố định (Định nghĩa 10.15).
- **Học liên tục.** Một dãy nhiệm vụ, đo bằng ma trận đánh giá trên mọi nhiệm vụ đã gặp (Định nghĩa 10.11).
- **Dịch chuyển phân bố** (distribution shift). Phân bố huấn luyện khác phân bố lúc dùng mô hình, kể cả với một lần huấn luyện.

:::

::: example Ví dụ 10.17 (Hối tiếc tĩnh nhỏ và độ quên lớn)
**Thiết lập.** $W=[0,1]$, $\ell(w,z)=\tfrac12(w-z)^2$, $T=1000$; dãy cố định $z_t=0$ với $t\le500$ (nhiệm vụ A) và $z_t=1$ với $t>500$ (nhiệm vụ B). Rủi ro trên nhiệm vụ A là $L_A(w)=\tfrac12w^2$.

**Bước 1: điểm so sánh tốt nhất.** $\sum_t\ell(u,z_t)=250u^2+250(1-u)^2$ nhỏ nhất tại $u=\tfrac12$, bằng $125$; do đó hối tiếc tĩnh bằng hối tiếc so với $u=\tfrac12$.

**Bước 2: cận của Nhận xét 10.16.** Với $w_1=0$, $\lVert w_1-u\rVert\le1=R$, và $\lvert w-z\rvert\le1=G$. Với $\eta=1/\sqrt{1000}$, $\mathrm{Regret}_T(u)\le\sqrt{1000}\le31{,}63$ với mọi $u\in W$.

**Bước 3: hạ gradient với $\eta=1/\sqrt T$.** Cộng hàm lỗi trên $1000$ vòng (tính bằng máy), hối tiếc bằng $-116{,}97$; nó âm vì thuật toán theo kịp từng nửa dãy. Điểm cuối $w_{T+1}\approx1$, nên $L_A(w_{T+1})\approx\tfrac12$.

**Bước 4: hạ gradient với $\eta_t=1/t$.** Khi đó $w_{t+1}=(1-\tfrac1t)w_t+\tfrac1tz_t$, nên theo quy nạp $w_{t+1}$ là trung bình của $z_1,\ldots,z_t$; cận của Bước 2 không áp dụng vì độ dài bước thay đổi. Tính trên $1000$ vòng, hối tiếc bằng $0{,}19$; $w_{T+1}=\tfrac12$ và $L_A(w_{T+1})=\tfrac18$.

**Kết luận.** Hai thuật toán có hối tiếc dưới $31{,}63$ nhưng rủi ro cuối trên nhiệm vụ A là $\tfrac12$ và $\tfrac18$. Hối tiếc cộng hàm lỗi tại thời điểm của từng vòng, nên cận hối tiếc tĩnh không phải cận cho độ quên.
:::

Nhận xét 10.16 chặn hối tiếc tĩnh trên mọi dãy; độ quên thì chưa có cận nào trong bài.

## 10. Ý nghĩa, tác động và giới hạn

Khi tác tử tương tác với môi trường, phân bố $p_\theta$ của dữ liệu phụ thuộc tham số đang học, nhưng gradient của mục tiêu vẫn ước lượng được không chệch từ một lượt nhờ gradient log của chính sách (Định lý 10.4). Khi nhiệm vụ thay đổi, bài toán chỉ xác định khi có giao thức và ma trận đánh giá (Định nghĩa 10.10, 10.11), và hai nhiệm vụ xung đột buộc $L_A+L_B\ge\tfrac14$ trong ví dụ bậc hai (Mệnh đề 10.13).

Rủi ro kì vọng trở thành tổng phần thưởng kì vọng ở Phần A và một ma trận đánh giá ở Phần B; mẫu cố định trở thành các lượt sinh bởi chính sách hiện tại hay một dãy mẫu từ $D_1,\ldots,D_K$. Bổ đề 10.3, Định lý 10.4, Mệnh đề 10.7 và Hệ quả 10.8 là đồng nhất thức, không có mẫu; Mệnh đề 10.13 và Nhận xét 10.16 là tất định; bảo đảm với xác suất cao duy nhất là Ví dụ 10.12, cho một chính sách cố định trước khi chạy. Chưa có cận hội tụ nào cho REINFORCE và chưa có định lý học liên tục tổng quát.

Các giới hạn chính như sau.

- **Phương sai cao.** Giá trị nền tùy ý có thể tăng phương sai (Ví dụ 10.8); trong Ví dụ 10.11, dịch phần thưởng $c=10$ nhân phương sai khoảng $225$ lần.
- **Mục tiêu không lõm.** Điểm dừng có thể là điểm cực tiểu (Ví dụ 10.7).
- **Giả thiết về môi trường.** Luật chuyển phụ thuộc tham số làm ước lượng ngược dấu (Ví dụ 10.6).
- **Phụ thuộc giao thức và quy ước.** Đổi quy ước đo có thể cho độ quên âm (Ví dụ 10.13).
- **Phát lại hữu hạn.** Trong Ví dụ 10.16, bộ đệm $M$ quan sát thêm $\tfrac1{8M}$ vào rủi ro cũ theo kì vọng.
- **Hối tiếc và độ quên.** Hối tiếc âm đi cùng rủi ro cuối $\tfrac12$ trên nhiệm vụ cũ (Ví dụ 10.17).

## 11. Bài tập

Đề, gợi ý và lời giải nằm trong [tệp bài tập của Bài 10](material-viewer.html?doc=materials/lec-10/exercises.md); bảy bài đầu là bài gốc, hai bài sau chọn từ UML.

1. **Bài tập 10.1** (Thuật toán REINFORCE cho bài toán bandit hai hành động): mục tiêu 2, 3.
2. **Bài tập 10.2** (Giá trị nền hợp lệ và giá trị nền gây chệch): mục tiêu 3.
3. **Bài tập 10.3** (Các giả thiết của Định lý 05.14 trong tối ưu chính sách): mục tiêu 5.
4. **Bài tập 10.4** (Độ chính xác phân lớp trung bình cuối cùng, chuyển đổi và độ quên từ một ma trận đánh giá): mục tiêu 4.
5. **Bài tập 10.5** (Hai nhiệm vụ bậc hai với ba hệ số chính quy hóa): mục tiêu 5.
6. **Bài tập 10.6** (Thiết kế một so sánh giữa tinh chỉnh và phát lại): mục tiêu 4.
7. **Bài tập 10.7** (Năm câu hỏi tổng kết cho hai thiết lập khác): mục tiêu 1, 5.
8. **Bài tập 10.8** (Chuyển từ học trực tuyến sang học theo lô; UML Bài tập 21.5): mục tiêu 5.
9. **Bài tập 10.9** (Mẹo nhân đôi; UML Bài tập 21.4; tùy chọn): mục tiêu 5.

## 12. Câu hỏi cuối buổi và tổng kết học phần

**Câu hỏi.**

(a) Trong bài toán bandit hai hành động với chính sách sigmoid, đặt $r(1)=2$, $r(0)=0$ và $\theta=0$. Tính $J'(0)$ bằng đạo hàm trực tiếp, hai giá trị của ước lượng gradient log với giá trị nền $0$, và kiểm rằng kì vọng của ước lượng bằng $J'(0)$.

(b) Giá trị nền được đặt bằng chính phần thưởng vừa nhận, $r(A)$. Ước lượng có còn không chệch không?

(c) Tham số $\theta_{s_0}$ của robot trong câu hỏi mở đầu điều khiển cả động cơ, nên xác suất tới $s_1$ phụ thuộc $\theta_{s_0}$. Có thể dùng Thuật toán 10.6 mà không sửa không?

(d) Trong Mệnh đề 10.13, lấy $\lambda=\tfrac14$. Tính $w_\lambda$, $L_A(w_\lambda)$, $L_B(w_\lambda)$ và tỉ lệ phát lại $\alpha$ cho cùng điểm cực tiểu.

(e) Một thuật toán trực tuyến có hối tiếc tĩnh âm trên dãy của Ví dụ 10.17. Có suy ra rủi ro cuối của nó trên nhiệm vụ A nhỏ không?

(f) **Tổng kết học phần.** Với bốn bài toán (phân lớp có giám sát, ước lượng mật độ, tối ưu chính sách và học liên tục), nêu quá trình sinh dữ liệu, mục tiêu, đối tượng so sánh, các đại lượng ngẫu nhiên và các giả thiết của Bài 01–08 cần thay đổi.

::: solution Lời giải câu hỏi cuối buổi
**(a)** Tại $\theta=0$, $\pi_0(1)=\tfrac12$ và $J(\theta)=2\pi_\theta(1)$, nên $J'(0)=2\cdot\tfrac12\cdot\tfrac12=\tfrac12$. Ước lượng $r(A)(A-\tfrac12)$ bằng $1$ khi $A=1$ và $0$ khi $A=0$, với kì vọng $\tfrac12\cdot1+\tfrac12\cdot0=\tfrac12$ (Định lý 10.4).

**(b)** Không. Ước lượng luôn bằng $0$, nên kì vọng $0\ne J'$; giá trị nền phụ thuộc hành động vi phạm giả thiết của Hệ quả 10.8 (Ví dụ 10.9).

**(c)** Không. Bước 3 của chứng minh Định lý 10.4 dùng giả thiết luật chuyển không phụ thuộc $\theta$; khi giả thiết này hỏng, ước lượng bị chệch, và ở Ví dụ 10.6 nó ngược dấu, $-0{,}25$ so với $0{,}125$.

**(d)** $w_\lambda=1/(1+\tfrac14)=\tfrac45$, $L_A=\tfrac12\cdot\tfrac{16}{25}=\tfrac8{25}$, $L_B=\tfrac12\cdot\tfrac1{25}=\tfrac1{50}$, và $\alpha=\tfrac14/\tfrac54=\tfrac15$.

**(e)** Không. Ở Ví dụ 10.17, thuật toán có hối tiếc $-116{,}97$ kết thúc ở $w\approx1$ với $L_A\approx\tfrac12$, gần giá trị lớn nhất của $L_A$ trên $W$.

**(f)** Phân lớp có giám sát dùng (T1) với một $D$ cố định; ước lượng mật độ bỏ (T3) vì hàm lỗi log không bị chặn, và bỏ (T1) với chuỗi thời gian; tối ưu chính sách bỏ (T1) và (C); học liên tục thay $D$ bằng một dãy $D_1,\ldots,D_K$ có giới hạn truy cập. Năm thành phần của từng bài toán được liệt kê ở Phụ lục D.
:::

## 13. Tài liệu đọc

- **Trước buổi học:** R. S. Sutton, A. G. Barto (2018), *Reinforcement Learning: An Introduction*, bản thứ hai, §13.1–13.3 (xấp xỉ chính sách, định lý gradient chính sách, REINFORCE).
- **Sau buổi học:** Sutton, Barto, §13.4 (REINFORCE có giá trị nền) và §2.8 (thuật toán gradient cho bài toán bandit); UML §21.1–21.3 (học trực tuyến, hối tiếc, tối ưu lồi trực tuyến).
- **Mở rộng:** J. Kirkpatrick và cộng sự (2017), *Overcoming catastrophic forgetting in neural networks*, PNAS, phần đặt vấn đề và phương pháp; Sutton, Barto, §13.5 (phương pháp tác nhân–phê bình) và §13.7 (hành động liên tục).

**Quan hệ với nguồn.** Các định nghĩa, kết quả và số hiệu ở đây là của học phần; Sutton và Barto, UML và bài báo của Kirkpatrick và cộng sự được dẫn theo mục. Các khác biệt chính:

- **Thiết lập.** Sutton và Barto xét lượt dài ngẫu nhiên, trạng thái đầu cố định, và phát biểu định lý gradient chính sách dưới dạng tỉ lệ ($\propto$); học phần dùng độ dài lượt $H$ cố định, phân bố trạng thái đầu bất kì và một đẳng thức (Định lý 10.4).
- **Kí hiệu.** Sutton và Barto viết phần thưởng $R_{t+1}$ sau $A_t$ và $G_t$ cho tổng từ bước $t$; học phần viết $r_t$ và $R_{\ge t}$, vì $G$ là hằng số Lipschitz từ Bài 05.
- **Thuật toán và giá trị nền.** Khung REINFORCE của Sutton và Barto cập nhật tham số ở từng bước trong lượt và dùng $G_t$, tức ước lượng của Mệnh đề 10.7(b); Thuật toán 10.6 dùng $R(\tau)$ và cập nhật sau mỗi lượt. Sutton và Barto cho phép giá trị nền là biến ngẫu nhiên không thay đổi theo hành động, trong dạng tổng trên mọi hành động; với ước lượng lấy mẫu, học phần nêu điều kiện "là hàm của lịch sử trước hành động" kèm phản ví dụ (Ví dụ 10.9). Học phần không nêu khẳng định hội tụ nào cho REINFORCE.
- **Củng cố trọng số đàn hồi.** Học phần chỉ dùng động cơ và dạng phạt có trọng số của bài báo; ma trận Fisher ở Nhận xét 10.14 theo định nghĩa chuẩn. Phát lại trong thí nghiệm Atari của bài báo là phát lại kinh nghiệm (experience replay) của thuật toán học tăng cường, khác Định nghĩa 10.12.
- **Độ đo học liên tục.** Ma trận đánh giá và các độ đo ở Định nghĩa 10.11 là quy ước của học phần; không nguồn nào của học phần định nghĩa chúng.

## Phụ lục

### A. Đổi chỗ đạo hàm và kì vọng khi tập quỹ đạo vô hạn

Các điều kiện ở đây là của Nhận xét 10.5: mật độ $p_\theta(\tau)$ theo một độ đo nền $\nu$ không phụ thuộc $\theta$, tính khả vi liên tục của $\theta\mapsto p_\theta(\tau)$ với mọi $\tau$, hàm trội $\Lambda$, và phần thưởng bị chặn như Định nghĩa 10.1, nên $\lvert R(\tau)\rvert\le C_R$ với một hằng số $C_R$ và $J(\theta)=\int R(\tau)p_\theta(\tau)\,d\nu(\tau)$ hữu hạn. Kí hiệu $D_eJ$ là đạo hàm theo hướng đơn vị $e$.

::: proof Chứng minh khẳng định của Nhận xét 10.5
**Lộ trình.** Như chứng minh Mệnh đề 09.15 ở Phụ lục B của Bài 09, với hàm $\theta\mapsto R(\tau)p_\theta(\tau)$ thay cho hàm trên đường nhiễu: định lý giá trị trung bình trên từng $\tau$, định lý hội tụ bị chặn cho đạo hàm theo hướng, hội tụ bị chặn lần nữa cho tính liên tục, rồi "đạo hàm riêng liên tục kéo theo khả vi". Bất đẳng thức then chốt là cận $\Lambda(\tau)$ cho thương sai phân. Điều kiện khả vi đóng vai điều kiện (i) của Mệnh đề 09.15: tập điểm không khả vi không được phụ thuộc tham số.

**Bước 1 (định lý giá trị trung bình; dùng điều kiện khả vi).** Cố định $\theta_0\in\Theta$, lấy $U$, $\Lambda$ như điều kiện hàm trội và thu nhỏ $U$ thành một quả cầu mở tâm $\theta_0$ bán kính $\Delta_0$. Với hướng đơn vị $e$ và $0<\lvert\Delta\rvert<\Delta_0$, hàm một biến $\rho\mapsto R(\tau)p_{\theta_0+\rho e}(\tau)$ khả vi trên đoạn nối $0$ và $\Delta$ với mọi $\tau$. Theo định lý giá trị trung bình, có $\rho_\tau$ giữa $0$ và $\Delta$ với
$$
\begin{aligned}
&\frac{R(\tau)\big(p_{\theta_0+\Delta e}(\tau)-p_{\theta_0}(\tau)\big)}\Delta\\
&=R(\tau)\big\langle\nabla p_{\theta_0+\rho_\tau e}(\tau),e\big\rangle .
\end{aligned}
$$
Bước này cần tính khả vi tại mọi điểm của đoạn với cùng một $\tau$. Điều kiện đó loại Ví dụ 10.3: với $a$ trong khoảng của $\theta$ đang xét, hàm $\theta\mapsto\mathbb 1[a\le\theta]/\theta$ nhảy tại $\theta=a$.

**Bước 2 (hàm trội).** Điểm $\theta_0+\rho_\tau e$ nằm trong $U$, nên thương sai phân ở Bước 1 có trị tuyệt đối không quá $\Lambda(\tau)$, với $\int\Lambda\,d\nu<\infty$.

**Bước 3 (hội tụ bị chặn).** Thương sai phân của $J$ bằng tích phân của thương sai phân ở Bước 1. Khi $\Delta\to0$, thương sai phân tiến tới $R(\tau)\langle\nabla p_{\theta_0}(\tau),e\rangle$ với mọi $\tau$, và bị chặn bởi $\Lambda(\tau)$. Định lý hội tụ bị chặn cho
$$
\begin{aligned}
&D_eJ(\theta_0)\\
&=\int R(\tau)\big\langle\nabla p_{\theta_0}(\tau),e\big\rangle\,d\nu(\tau).
\end{aligned}
$$

**Bước 4 (tính liên tục và khả vi).** Với $\theta_k\to\theta_0$ trong $U$, $\nabla p_{\theta_k}(\tau)\to\nabla p_{\theta_0}(\tau)$ theo tính khả vi liên tục, và $\lvert R(\tau)\rvert\lVert\nabla p_{\theta_k}(\tau)\rVert\le\Lambda(\tau)$. Hội tụ bị chặn cho tính liên tục của các đạo hàm riêng của $J$ tại $\theta_0$. Một hàm có mọi đạo hàm riêng liên tục trên một tập mở thì khả vi trên đó, nên $J$ khả vi và $\nabla J(\theta)=\int R(\tau)\nabla p_\theta(\tau)\,d\nu(\tau)$.

**Bước 5 (gradient log).** Trên tập $\{\tau:p_\theta(\tau)>0\}$, $\nabla p_\theta(\tau)=p_\theta(\tau)\nabla\ln p_\theta(\tau)$. Ngoài tập đó, $\theta$ là điểm cực tiểu của hàm không âm khả vi $\theta'\mapsto p_{\theta'}(\tau)$ trên tập mở $\Theta$, nên $\nabla p_\theta(\tau)=0$, như Bổ đề 10.3(a). Do đó $\nabla J(\theta)=\mathbb E_{\tau\sim p_\theta}[R(\tau)\nabla\ln p_\theta(\tau)]$; với $R\equiv1$ và $\Lambda$ là hàm trội cho $\lVert\nabla p_\theta\rVert$, ta được $\mathbb E\nabla\ln p_\theta(\tau)=0$.

**Bước 6 (chính sách Gauss).** Xét $\mathcal S$ hữu hạn, $\mathcal A=\mathbb R$, $A_t\sim N(\mu_\theta(S_t),\omega^2)$ với $\theta\mapsto\mu_\theta(s)$ khả vi liên tục và $\omega>0$ cố định, luật chuyển không phụ thuộc $\theta$. Gọi $\mathcal N_\omega$ là mật độ của $N(0,\omega^2)$. Mật độ quỹ đạo là tích của $\mu_0(s_0)$, các thừa số $\mathcal N_\omega(a_t-\mu_\theta(s_t))$ và các xác suất chuyển; chỉ các thừa số Gauss phụ thuộc $\theta$. Do đó
$$
\begin{aligned}
&\nabla p_\theta(\tau)\\
&=p_\theta(\tau)\textstyle\sum_t\frac{a_t-\mu_\theta(s_t)}{\omega^2}\nabla\mu_\theta(s_t).
\end{aligned}
$$
Trên một quả cầu đóng $\bar U\subset\Theta$ quanh $\theta_0$, các hàm liên tục $\lvert\mu_\theta(s)\rvert$ và $\lVert\nabla\mu_\theta(s)\rVert$ bị chặn bởi một hằng số $C_\mu$ với mọi $s$, vì $\mathcal S$ hữu hạn. Vì $(a-\mu)^2\ge a^2/2-\mu^2$, mỗi thừa số Gauss không quá $e^{C_\mu^2/(2\omega^2)}\mathcal N_\omega(0)\,e^{-a_t^2/(4\omega^2)}$, và $\lvert a_t-\mu_\theta(s_t)\rvert\le\lvert a_t\rvert+C_\mu$. Nhân với $\lvert R\rvert\le C_R$, ta được một hàm trội $\Lambda(\tau)$ bằng một đa thức của $\lvert a_0\rvert,\ldots,\lvert a_{H-1}\rvert$ nhân tích các hàm $e^{-a_t^2/(4\omega^2)}$ và các xác suất của môi trường; hàm này khả tích. Tính khả vi liên tục theo $\theta$ suy ra từ tính khả vi liên tục của $\mu_\theta$.

$\square$ Với tập quỹ đạo hữu hạn, các Bước 1–4 là đạo hàm của một tổng hữu hạn, như Bước 1 của chứng minh Định lý 10.4. Với mật độ, điều kiện cần kiểm là hàm trội, và giá của mật độ không được di chuyển theo $\theta$.
:::

### B. Chi tiết chứng minh Mệnh đề 10.7

Cố định $t$. Mỗi quỹ đạo $\tau$ được tách thành ba phần: lịch sử $\mathbf o=(s_0,a_0,\ldots,a_{t-1},s_t)$, một giá trị của $\mathcal F_t$; hành động $a_t$; và phần sau $\mathbf o^+=(s_{t+1},a_{t+1},\ldots,s_{H-1},a_{H-1})$, rỗng khi $t=H-1$.

::: proof Chứng minh chi tiết Mệnh đề 10.7
**Lộ trình.** Viết $p_\theta(\tau)$ thành tích theo ba phần, lấy tổng theo phần sau, rồi dùng $\sum_a\nabla\pi_\theta(a\mid s)=0$.

**Bước 1 (phân tích xác suất; dùng chính sách chỉ phụ thuộc trạng thái hiện tại).** Theo Định nghĩa 10.2,
$$
\begin{aligned}
p_\theta(\tau)&=\Pr\nolimits_\theta(\mathbf o)\,\pi_\theta(a_t\mid s_t)\\
&\quad\cdot\Pr\nolimits_\theta(\mathbf o^+\mid\mathbf o,a_t),
\end{aligned}
$$
trong đó $\Pr_\theta(\mathbf o)$ là tích của $\mu_0(s_0)$ với các thừa số của chính sách và của luật chuyển trước bước $t$, và $\Pr_\theta(\mathbf o^+\mid\mathbf o,a_t)$ là tích các thừa số còn lại, bằng $1$ khi phần sau rỗng. Thừa số của $a_t$ là $\pi_\theta(a_t\mid s_t)$, không phụ thuộc phần còn lại của lịch sử. Lấy tổng lần lượt theo $a_{H-1}$, $s_{H-1}$, …, $s_{t+1}$, ta có $\sum_{\mathbf o^+}\Pr_\theta(\mathbf o^+\mid\mathbf o,a_t)=1$.

**Bước 2 (lấy tổng phần sau).** Với một hàm $f$ bất kì của lịch sử, mọi tổng là hữu hạn, và các số hạng có xác suất $0$ bị bỏ:
$$
\begin{aligned}
&\mathbb E\big[f(\mathcal F_t)\nabla\ln\pi_\theta(A_t\mid S_t)\big]\\
&=\textstyle\sum_{\mathbf o}\Pr_\theta(\mathbf o)f(\mathbf o)\\
&\quad\cdot\textstyle\sum_a\pi_\theta(a\mid s_t)\nabla\ln\pi_\theta(a\mid s_t)\\
&=\textstyle\sum_{\mathbf o}\Pr_\theta(\mathbf o)f(\mathbf o)\\
&\quad\cdot\textstyle\sum_a\nabla\pi_\theta(a\mid s_t),
\end{aligned}
$$
với tổng trong lấy trên các $a$ có $\pi_\theta(a\mid s_t)>0$; đẳng thức thứ nhất dùng Bước 1, đẳng thức thứ hai dùng Bổ đề 10.3(a).

**Bước 3 (Bổ đề 10.3).** Các $a$ có $\pi_\theta(a\mid s_t)=0$ có $\nabla\pi_\theta(a\mid s_t)=0$ theo Bổ đề 10.3(a), nên tổng trong bằng $\sum_{a\in\mathcal A}\nabla\pi_\theta(a\mid s_t)=\nabla1=0$. Do đó kì vọng ở Bước 2 bằng $0$.

**Bước 4 (kết luận).** Với $f=r_{t'}$, $t'<t$, một hàm của lịch sử, ta được (a). Với $f=b_t(\mathcal F_t)$, ta được Bước 1 của chứng minh Hệ quả 10.8. Phần (b) suy ra từ (a) như Bước 3 của phác thảo.

$\square$ Chứng minh chỉ dùng việc chính sách chọn $a_t$ theo trạng thái hiện tại và tính hữu hạn của các tập. Giả thiết $\mu_0$, $P$ không phụ thuộc $\theta$ không cần ở đây; nó chỉ cần ở Định lý 10.4, mà Mệnh đề 10.7(b) dùng làm điểm xuất phát.
:::

### C. Giao thức thí nghiệm

Các số của Ví dụ 10.11 và 10.16 là kết quả thí nghiệm cho một thiết lập. Giao thức dưới đây đủ để tái lập chúng; chỉ cần thư viện NumPy, và cả hai phần chạy trong khoảng hai giây.

**Phần REINFORCE.**

- **Bài toán.** Khối ứng dụng của §3: xác suất nhấp $0{,}6$ (nội dung $1$) và $0{,}4$ (nội dung $0$); phần thưởng bằng nhấp cộng $c$, $c\in\{0,10\}$. Mọi số là giá trị giả định.
- **Thuật toán.** Thuật toán 10.6 với $H=1$, $\theta_1=0$, $\eta_j=0{,}1$, $T=2000$: $\theta_{j+1}=\theta_j+\eta_j\big(R(\tau_j)-b_j\big)\big(A_j-\pi_{\theta_j}(1)\big)$. Giá trị nền $b_j=0$ (không giá trị nền), hoặc $b_j$ là trung bình phần thưởng của các lượt $1,\ldots,j-1$, bằng $0$ khi $j=1$; giá trị nền này hợp lệ theo Nhận xét 10.9(ii).
- **Cách rút.** Ở mỗi cập nhật, rút một số đều $U$ trên $[0,1)$ và chọn $A_j=1$ khi $U<\pi_{\theta_j}(1)$; rồi rút một số đều $U'$ và đặt nhấp bằng $1$ khi $U'$ nhỏ hơn xác suất nhấp của nội dung đã chọn.
- **Đại lượng.** $\pi_{\theta_{T+1}}(1)$; trung bình, độ lệch chuẩn (chia cho số lần chạy trừ $1$), nhỏ nhất, lớn nhất qua các lần chạy và số lần chạy kết thúc dưới $0{,}5$. Đại lượng là tham số, tính đúng, nên không cần mẫu kiểm tra.
- **Lặp lại.** $100$ hạt giống $0,\ldots,99$; mỗi hạt giống khởi tạo bộ sinh `numpy.random.default_rng`, và các số đều rút theo thứ tự trên.
- **Kết quả.** Với $c=0$: $0{,}969$ (độ lệch chuẩn $0{,}011$, từ $0{,}928$ đến $0{,}986$) không giá trị nền, $0{,}970$ ($0{,}009$; $0{,}938$–$0{,}985$) có giá trị nền. Với $c=10$: $0{,}509$ ($0{,}498$; $0{,}001$–$1{,}000$; $49$ lần chạy dưới $0{,}5$) không giá trị nền, $0{,}969$ ($0{,}009$; $0{,}932$–$0{,}986$) có giá trị nền.

**Phần phát lại.** Mô hình ở đây khác mô hình của Ví dụ 10.16.

- **Dữ liệu.** $x\sim N(0,1)$; nhiệm vụ A: $y=\zeta$; nhiệm vụ B: $y=x+\zeta$, với nhiễu $\zeta\sim N(0;\,0{,}25)$, độ lệch chuẩn $0{,}5$. Mỗi nhiệm vụ có $1000$ quan sát huấn luyện và $10\,000$ quan sát kiểm tra, rút độc lập. Mọi số là giá trị giả định.
- **Mô hình và hàm lỗi.** $y=wx$ với hàm lỗi $\tfrac12(y-wx)^2$; rủi ro tổng thể $\tfrac12(w^2+0{,}25)$ trên A, nhỏ nhất bằng $0{,}125$, và $\tfrac12\big((w-1)^2+0{,}25\big)$ trên B.
- **Thuật toán.** Một vòng SGD trên A theo thứ tự quan sát, $\eta=0{,}02$, từ $w=0$; rồi một vòng trên B. Với phát lại, bộ đệm gồm $M\in\{0,5,50,1000\}$ quan sát của A, chọn đều không hoàn lại; mỗi bước trên B lấy trung bình gradient của quan sát B và của một quan sát rút đều, có hoàn lại, từ bộ đệm, tức $\alpha=\tfrac12$.
- **Đại lượng và tham chiếu.** Rủi ro trên mẫu kiểm tra của A và B sau nhiệm vụ B; $w$ cuối. Điểm thỏa hiệp $w=\tfrac12$ cho rủi ro tổng thể $0{,}25$ trên cả hai nhiệm vụ.
- **Lặp lại.** $20$ hạt giống $0,\ldots,19$; thứ tự rút cố định trong mỗi hạt giống: dữ liệu huấn luyện của A, của B, mẫu kiểm tra A, mẫu kiểm tra B, bộ đệm, rồi các chỉ số phát lại.
- **Làm tròn.** Số đo làm tròn đến giá trị gần nhất, ba chữ số thập phân.

Sau nhiệm vụ A, $w$ trung bình bằng $0{,}011$. Bảng ghi $w$ cuối (độ lệch chuẩn qua $20$ lần chạy) và rủi ro trên mẫu kiểm tra của A (trung bình; nhỏ nhất – lớn nhất). Rủi ro trên mẫu kiểm tra của B, trung bình, là $0{,}126$; $0{,}218$; $0{,}248$; $0{,}255$ theo thứ tự các hàng.

| $M$ | $w$ cuối | Rủi ro A | Khoảng |
|---|---|---|---|
| $0$ | $0{,}998$ ($0{,}049$) | $0{,}624$ | $0{,}490$–$0{,}695$ |
| $5$ | $0{,}614$ ($0{,}198$) | $0{,}331$ | $0{,}158$–$0{,}721$ |
| $50$ | $0{,}509$ ($0{,}073$) | $0{,}256$ | $0{,}186$–$0{,}315$ |
| $1000$ | $0{,}498$ ($0{,}087$) | $0{,}252$ | $0{,}178$–$0{,}336$ |

### D. Lời giải câu (f): bốn bài toán của học phần

Mỗi bài toán được mô tả bằng năm thành phần của câu (f) ở §12.

*Phân lớp có giám sát (Bài 01–08).*

- **Quá trình sinh dữ liệu.** $S\sim D^m$ theo (T1).
- **Mục tiêu.** $L_D(h)$ nhỏ, với hàm lỗi 0–1 (Bài 01–04, 07) hay hàm lỗi lồi hoặc trơn thay cho hàm lỗi 0–1 (Bài 05–06, 08).
- **Đối tượng so sánh.** $\inf_{h\in\mathcal H}L_D(h)$ (Định nghĩa 01.24) hoặc rủi ro Bayes (Định nghĩa 01.22).
- **Đại lượng ngẫu nhiên.** $S$, $A(S)$, $L_S(h)$, nguồn ngẫu nhiên của thuật toán (Định nghĩa 05.18).
- **Giả thiết cần đổi.** Không; đây là thiết lập của các cận như Định lý 02.14, 03.15, 04.11, 07.11, và của Bài 05–06, 08 khi thêm các giả thiết tối ưu của từng bài, như (C), (G1), (G2).

*Ước lượng mật độ (Bài 09).*

- **Quá trình sinh dữ liệu.** $S\sim D^m$; với dữ liệu chuỗi, mỗi quan sát là cả một chuỗi (Thiết lập A của Định nghĩa 09.1).
- **Mục tiêu.** $L_D(\theta)=\mathbb E[-\ln p_\theta(X)]$ nhỏ.
- **Đối tượng so sánh.** $\inf_\theta L_D(\theta)$, bằng entropy của $D$ khi lớp chứa phân bố thật (Mệnh đề 09.8).
- **Đại lượng ngẫu nhiên.** $S$, ước lượng hợp lý cực đại.
- **Giả thiết cần đổi.** (T3) (hàm lỗi trong $[0,1]$), và (T2) khi có mật độ; cận cho hàm lỗi bị chặn cần một cận dưới cho xác suất của mô hình (Ví dụ 09.4). Với một chuỗi thời gian (Thiết lập B của Định nghĩa 09.1), (T1) cũng không thỏa, vì các cửa sổ chồng lấn phụ thuộc nhau.

*Tối ưu chính sách (Phần A).*

- **Quá trình sinh dữ liệu.** $\tau_j\sim p_{\theta_j}$, với $\theta_j$ phụ thuộc các lượt trước; các bước trong lượt phụ thuộc nhau.
- **Mục tiêu.** $J(\theta)$ lớn.
- **Đối tượng so sánh.** $\sup_\theta J(\theta)$, có thể không đạt.
- **Đại lượng ngẫu nhiên.** Các lượt, các $\theta_j$, các ước lượng gradient.
- **Giả thiết cần đổi.** (T1), trừ khi đánh giá một chính sách cố định (Ví dụ 10.12), và (C) vì $-J$ không lồi (Ví dụ 10.7).

*Học liên tục (Phần B).*

- **Quá trình sinh dữ liệu.** $S^{(k)}\sim D_k^{m_k}$ đến theo thứ tự, với bộ nhớ không quá $M$ quan sát cũ.
- **Mục tiêu.** Các độ đo của ma trận đánh giá theo một quy ước nêu trước.
- **Đối tượng so sánh.** Mô hình huấn luyện chung, bị giới hạn bởi đánh đổi (Mệnh đề 10.13), hoặc các mô hình riêng.
- **Đại lượng ngẫu nhiên.** Các mẫu, bộ đệm, các mẫu kiểm tra, nguồn ngẫu nhiên của thuật toán.
- **Giả thiết cần đổi.** (T1) với một $D$ thành một dãy $D_1,\ldots,D_K$; cận hối tiếc không đo độ quên (Ví dụ 10.17).
