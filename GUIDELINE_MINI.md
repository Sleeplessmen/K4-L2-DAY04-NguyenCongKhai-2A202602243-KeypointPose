# Mini guideline - nhóm: solo | người gán: Nguyễn Công Khải | ngày: 16-09-2026

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống                                        | Luật nhóm bạn chọn                                                                                                                        | Vì sao                                                                                                                               | Ảnh minh họa |
| ------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------ |
| Hông của người mặc quần áo dài                    | v = 1, đặt chấm ước lượng                                                                                                                 | Bị che bởi vật (quần áo) nhưng vẫn trong khung ảnh thì áp dụng rule v = 1 (bị che, còn trong khung).                                 |
| Tai bị tóc hoặc mũ bảo hiểm che một phần          | v = 1, đặt chấm ước lượng                                                                                                                 | Che một phần vẫn được xem là "bị che" thì v = 1 (không dùng v = 0 vì keypoint vẫn trong khung).                                      |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Keypoint dưới hông (đùi, đầu gối, mắt cá): v = 0 (không đặt chấm). Keypoint từ hông trở lên: v = 1 (nếu bị che) hoặc v = 2 (nếu nhìn thấy | Áp dụng rule: ra ngoài mép thì v = 0. Nếu keypoint không xuất hiện trong khung (ví dụ: mắt cá chân bị cắt mất), không đặt chấm.      |
| Cổ tay nằm sau tay lái / sau thân mình            | v = 1, đặt chấm ước lượng                                                                                                                 | Bị che bởi vật/phần cơ thể khác nhưng vẫn trong khung thì v = 1.                                                                     |
| Hai người chồng lên nhau                          | Keypoint bị che bởi người khác: v = 1. Keypoint không bị che: v = 2                                                                       | Áp dụng rule bị che: nếu keypoint vẫn trong khung nhưng bị đối tượng khác chặn thì v = 1.                                            |
| Người nhỏ đến mức nào thì không gán nữa           | Ngưỡng: chiều cao bounding box < 20px thì bỏ qua (không gán 17 điểm). Từ 20px trở lên: gán đủ 17 điểm (dù v = 0/1/2)                      | Tham khảo COCO: keypoint quá nhỏ (dưới ~10-20px) không đáng tin cậy cho model. Lưu ý: không xóa điểm, chỉ không gán nếu dưới ngưỡng. |
| Đặt trạng thái cho từng điểm                      | Quyết định riêng cho từng điểm. Chỉ dùng Occluded (`v = 1`) khi vẫn còn cơ sở suy ra vị trí khớp.                                         | Đảm bảo tính chính xác: nếu không có cơ sở ước lượng vị trí, không nên gán `v = 1` vì sẽ gây nhiễu cho model.                        |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_01`, người phụ nữ bên trái, khớp `LEFT_ELBOW` và `LEFT_WRIST`

- Mơ hồ ở chỗ nào: Khay bánh pizza cỡ lớn che khuất hoàn toàn cẳng tay và cổ tay trái của người phục vụ. Khó xác định chính xác cổ tay đang gập lên đỡ đáy khay pizza hay đang buông xuôi/ép sát vào tạp dề phía sau khay.
- Bạn quyết thế nào: Gán `v = 1` và đặt chấm ước lượng cho `LEFT_WRIST` ngay dưới tâm/vành khay pizza, `LEFT_ELBOW` gập góc nhọn hướng sang hông trái.
- Vì sao: Tư thế hai người bưng chung khay bánh đưa ra phía trước tạo ra cơ sở vật lý rõ ràng: lực nâng khay đòi hỏi cẳng tay phải hướng vào nâng đáy khay, kết hợp với vị trí bắp tay nhìn thấy được cho phép suy luận hình học góc khuỷu và cổ tay. Trường hợp này hoàn toàn đủ "cơ sở suy ra vị trí khớp" theo luật của nhóm.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu đánh `v = 0` (cho rằng bị che mất hoàn toàn nên không chấm), model sẽ học sai cấu trúc động học của hành vi bê/đỡ vật thể, mất khả năng dự đoán khớp tay khi tương tác với đồ vật lớn phía trước ngực.

### Ca 2 - ảnh `train_06`, khớp `NOSE`, `LEFT_EYE` và `RIGHT_EYE`

- Mơ hồ ở chỗ nào: Người lái xe quay lưng 180° và đội mũ bảo hiểm trùm kín đầu màu vàng. Cả 3 điểm vùng mặt bị che khuất hoàn toàn bởi chính hộp sọ và lớp vỏ mũ bảo hiểm.
- Bạn quyết thế nào: Gán `v = 1` và chấm ước lượng vị trí mắt/mũi ở nửa trước bán cầu mũ bảo hiểm theo trục đối xứng đầu.
- Vì sao: Dựa vào độ nghiêng của mũ, cổ và tư thế lái xe thẳng về phía trước, hướng nhìn và kích thước đầu người được cố định rõ ràng. Vẫn có cơ sở hình học vững chắc để nội suy vị trí giải phẫu bên trong.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu đánh `v = 0`, model sẽ nhầm lẫn giữa việc khuôn mặt bị cắt ra ngoài mép ảnh với việc tự che khuất do góc quay, gây lỗi nghiêm trọng khi huấn luyện mô hình ước lượng góc xoay đầu.

### Ca 3 - ảnh `train_03`, người đàn ông bên trái, khớp `LEFT_ELBOW` và `LEFT_WRIST`

- Mơ hồ ở chỗ nào: Người đàn ông bên trái đứng nép sát phía sau người đàn ông mặc áo khoác da. Toàn bộ nửa thân trái, đặc biệt từ vai trái dọc xuống khuỷu tay và cổ tay trái, bị cơ thể người phía trước che khuất hoàn toàn; không có bất kỳ điểm lộ nào của cánh tay trái.
- Bạn quyết thế nào: Đánh `v = 0` (không đặt chấm cho `LEFT_WRIST` và `LEFT_ELBOW`).
- Vì sao: Bàn tay và cẳng tay của người này có quá nhiều bậc tự do không bị ràng buộc: tay có thể đang buông thõng, gập sau lưng, hoặc đút túi quần. Trường hợp này hoàn toàn không có dấu vết hình ảnh hay ràng buộc vật lý để suy đoán.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu cố tình chấm bừa một vị trí giả định rồi gán `v = 1`, model sẽ học nhầm tọa độ ảo, sinh ra hiện tượng đoán mò và gây nhiễu gradient khi học về các ca che khuất phức tạp giữa người với người.
-

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `______` (bạn `___%` / họ `___%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**:
- Luật mới bổ sung vào mục 2 sau khi thống nhất:
