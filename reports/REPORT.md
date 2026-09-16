# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: **Nguyễn Công Khải** Nhóm: **solo** Ngày: **16-09-2026**

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số                       |        Giá trị |
| ---------------------------- | -------------: |
| Số ảnh đã gán                |             20 |
| Số skeleton                  |             29 |
| v=2 / v=1 / v=0              | 168 / 276 / 49 |
| Thời gian trung bình mỗi ảnh |         6 phút |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. left_shoulder
2. right_shoulder
3. left_hip (và right_hip)

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

- Có. Những khớp bị che (v=1) chủ yếu là **left_shoulder, right_shoulder, left_hip, right_hip** vì chúng thường bị che bởi cơ thể người khác, tay, hoặc vật thể xung quanh (ví dụ: áo dài, balo, xe mô tô). Nhìn chung, các khớp ở thân trên (vai, hông) dễ bị che hơn các khớp ở chân (gối, cổ chân) do góc chụp và tương tác giữa các đối tượng.

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số                | Trước rework | Sau rework |
| --------------------- | -----------: | ---------: |
| OKS trung bình        |        0.943 |      0.942 |
| OKS@0.50              |        0.931 |      1.000 |
| OKS@0.75              |        0.931 |      1.000 |
| Lỗi `dao_trai_phai`   |            0 |          0 |
| Lỗi `nham_nguoi`      |            0 |          0 |
| Lỗi `xoa_khop_bi_che` |            2 |          0 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- train_13.jpg: Thêm 2 skeleton cho 2 người bị bỏ sót (người thứ 3 và 4).
- train_12.jpg: Sửa `left_knee` và `left_ankle` của người thứ 2 từ `v=0` thành `v=1`.
- Lý do:
  - Ở `train_13.jpg`: 2 người bị mờ do ánh sáng kém, nhưng vẫn nhìn thấy vai, đầu, và chân => quyết định là không được bỏ sót.
  - Ở `train_12.jpg`: Khớp gối và khớp cổ chân bị che bởi xe, nhưng theo quan sát thông thường thì vẫn nằm trong phạm vi của frame => `v=1`.

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->

## 3. Kiểm chéo

Bạn cùng nhóm: **không có**

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm: không có

| Khớp | Bạn |  Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| ---- | --: | --: | ---: | ------------------------------------ |
|      |     |     |      |                                      |
|      |     |     |      |                                      |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất: không có

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số         | yolo26n-pose gốc | Sau fine-tune |   Chênh |
| -------------- | ---------------: | ------------: | ------: |
| pose_mAP50     |           0.8450 |        0.8450 | +0.0000 |
| pose_mAP50-95  |           0.6853 |        0.6908 | +0.0055 |
| pose_precision |           0.9734 |        0.9792 | +0.0058 |
| pose_recall    |           0.8462 |        0.8462 | +0.0000 |
| box_mAP50-95   |           0.8119 |        0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?

- Chỉ số pose_mAP50-95 tăng từ 0.6853 lên 0.6908 (tức là tăng 0.55%).
- Vì chỉ số này tăng nên model không bị giảm chất lượng tổng thể. Tuy nhiên, với tập train rất nhỏ (chỉ 20 ảnh), việc tăng nhẹ này cho thấy các nhãn bạn gán có độ chính xác tốt, giúp model tinh chỉnh nhẹ các khớp cụ thể trong ngữ cảnh của tập dữ liệu này mà không làm hỏng đi các đặc trưng tổng quát đã học từ COCO.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm _người_ dễ hơn hay tìm _khớp_ dễ hơn? Vì sao?

- box_mAP50-95 sau fine-tune là 0.8041; pose_mAP50-95 sau fine-tune là 0.6908 => Chênh lệch: 0.1133 (hay 11.33%).
- Model tìm người (box) dễ hơn tìm khớp (pose). Việc xác định một vùng hình chữ nhật bao quanh cơ thể người (Object Detection) đơn giản hơn rất nhiều so với việc định vị chính xác vị trí pixel của 17 khớp xương nhỏ, đặc biệt là khi các khớp này có thể bị che khuất, tự che khuất, hoặc xoay người ở những tư thế khó.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43 (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?

- Ảnh có OKS thấp nhất: train_06 với chỉ số OKS chỉ đạt 0.639.
- Thông thường, nhãn của tôi (con người) sẽ đúng (hoặc gần đúng nhất sau khi đã qua cổng Gold duyệt lỗi). Tôi dựa vào cấu trúc giải phẫu học thực tế của cơ thể người trên ảnh để xác định rõ khớp trái/phải và vị trí bị che khuất, trong khi model dễ bị đánh lừa bởi góc chụp hoặc quần áo trùng màu nền dẫn tới đoán lệch vị trí hoặc đảo lộn bộ phận.

5. Ảnh bạn gán tệ nhất có _cũng_ là ảnh model đoán tệ nhất không? Nếu có, điều đó nói gì về bức ảnh đó?

- Ảnh train_06 có điểm OKS đối chiếu giữa bạn và model thấp nhất (0.639), và đây cũng chính là ảnh có sự bất đồng lớn nhất.
- Nếu một bức ảnh khiến cả người gán nhãn lẫn model đều bối rối hoặc cho kết quả tệ nhất, điều đó chứng tỏ đây là một ảnh rất khó. Ảnh này thường có các đặc điểm: góc chụp cực đoan (ví dụ từ trên xuống, nằm rạp), đối tượng bị che khuất nghiêm trọng, thiếu ánh sáng, hoặc có nhiều người đứng chen chúc đè lên nhau làm chồng chéo các khớp.

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

- **Ảnh**: `train_01.jpg`
- **Người**: Người phụ nữ phục vụ bên trái.
- **Keypoint**: `left_knee`
- **Bằng chứng nhìn thấy**: Vị trí thân dưới của người phụ nữ từ ngang đùi trở xuống bị cắt bởi mép dưới của ảnh, hoàn toàn không có bất kỳ pixel đủ để làm cơ sở kết luận vị trí của khớp đầu gối.
- **Lý do chọn `v=0` mà không phải `v=1`**: Dù cơ thể về mặt vật lý vẫn nằm sau vật cản trong khung hình, nhưng theo quy tắc của nhóm, trạng thái v = 1 chỉ được gán khi người gán nhãn còn cơ sở giải phẫu rõ ràng để định vị khớp. Tại tư thế đứng bị che kín toàn bộ nửa dưới và không thấy điểm tiếp đất của bàn chân, ta không thể biết chắc khớp gối đang đứng thẳng, hơi chùng hay khuỵu sang bên, dẫn đến việc ước lượng sẽ hoàn toàn là không có cơ sở.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->
