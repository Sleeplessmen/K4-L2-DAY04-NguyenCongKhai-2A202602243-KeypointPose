# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 27 skeleton, trung bình 15.19 khớp có v > 0 mỗi người
- Tổng: v=2 159 | v=1 251 | v=0 49

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 24 | 3 | 0 | 11% |
| 1 | left_eye | 19 | 8 | 0 | 30% |
| 2 | right_eye | 20 | 7 | 0 | 26% |
| 3 | left_ear | 10 | 15 | 2 | 56% |
| 4 | right_ear | 12 | 14 | 1 | 52% |
| 5 | left_shoulder | 2 | 25 | 0 | 93% |
| 6 | right_shoulder | 2 | 25 | 0 | 93% |
| 7 | left_elbow | 12 | 13 | 2 | 48% |
| 8 | right_elbow | 12 | 14 | 1 | 52% |
| 9 | left_wrist | 11 | 13 | 3 | 48% |
| 10 | right_wrist | 14 | 11 | 2 | 41% |
| 11 | left_hip | 1 | 25 | 1 | 93% |
| 12 | right_hip | 1 | 25 | 1 | 93% |
| 13 | left_knee | 6 | 12 | 9 | 44% |
| 14 | right_knee | 5 | 14 | 8 | 52% |
| 15 | left_ankle | 5 | 12 | 10 | 44% |
| 16 | right_ankle | 3 | 15 | 9 | 56% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
