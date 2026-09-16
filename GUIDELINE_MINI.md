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

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `, người có ID = `, khớp `và`

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:

### Ca 2 - ảnh

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:

### Ca 3 - ảnh

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:
-

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `______` (bạn `___%` / họ `___%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**:
- Luật mới bổ sung vào mục 2 sau khi thống nhất:
