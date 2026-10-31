# Nguồn của học phần

| Tệp | Vai trò | Trạng thái |
|---|---|---|
| `blueprint.md` | Cấu trúc chi tiết 10 bài do người dùng cung cấp (2026-10-29): câu hỏi trung tâm, kết quả đề xuất, kế hoạch chứng minh, bài tập gốc, phân bổ thời gian, bài đọc. Là bản đồ nguồn cấp học phần; đọc mục của bài trước khi lập kế hoạch. | Có |
| `uml/understanding-machine-learning-theory-algorithms.pdf` | **Nguồn chính.** Shai Shalev-Shwartz và Shai Ben-David (2014), *Understanding Machine Learning: From Theory to Algorithms*, Cambridge University Press. Bản PDF do tác giả cung cấp tại trang sách, chỉ dùng cá nhân: không commit, không công bố lại, không chép đoạn văn vào ghi chú. | Có (người dùng tải thủ công 2026-10-29; 449 trang; SHA-256 `5ad0c69c922e47e423f6b469e8cfbaf07beae6933185af746b670911a8d163f2`) |
| `uml-sections.md` | Bảng tra mục UML → trang PDF cho từng bài | Có |
| `uml/MLbookSol.pdf` | *Understanding Machine Learning — Solution Manual*, Alon Gonen (biên tập Dana Rubinstein), 2014-11-17; lời giải chương 13–14 do Shai Shalev-Shwartz viết. 67 trang, phủ chương 2–25 (không có 26, 31). Tài liệu dành cho giảng viên: chỉ dùng để đối chiếu lời giải bài tập UML; không commit, không công bố, không chép lời giải. | Có (người dùng chép 2026-10-30; SHA-256 `a332ffe95b046818035b7e8bf5cfe7ca4f780ee5be11780f6156889eabb4fd34`) |

Số mục UML trong `blueprint.md` đã được đối chiếu với mục lục của nhà xuất bản (`https://assets.cambridge.org/97811070/57135/toc/9781107057135_toc.pdf`) ngày 2026-10-29: mọi mục được dẫn đều tồn tại với đúng tên chủ đề. Số định lý, số trang và số bài tập UML chỉ được dẫn sau khi kiểm tra trực tiếp trên PDF.

## Nguồn bổ sung (bài 07–10)

| Nguồn | Bài | Truy cập |
|---|---|---|
| Hardt, Recht, Singer (2016), *Train faster, generalize better: Stability of stochastic gradient descent*, ICML | 08 | PMLR v48, mở |
| Bartlett, Foster, Telgarsky (2017), *Spectrally-normalized margin bounds for neural networks*, NeurIPS | 07 (tùy chọn) | NeurIPS proceedings, mở; bản arXiv:1706.08498v2 tải về `supp/bartlett-foster-telgarsky-2017.pdf` (2026-10-31; 24 trang; SHA-256 `5674595cb6e6b13c`…), chỉ dùng phát biểu định lý và thảo luận |
| Kingma, Welling (2014), *Auto-Encoding Variational Bayes*, ICLR | 09 | arXiv:1312.6114, mở |
| Sutton, Barto (2018), *Reinforcement Learning: An Introduction*, 2nd ed., Chương 13 | 10 | Bản nháp do tác giả cung cấp |
| Kirkpatrick và cộng sự (2017), *Overcoming catastrophic forgetting in neural networks*, PNAS | 10 (tùy chọn) | PNAS; bản arXiv:1612.00796 |

Tệp nhị phân trong `sources/` bị `.gitignore` loại khỏi Git.
