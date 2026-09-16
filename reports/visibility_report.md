# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 29 skeleton, trung bình 15.31 khớp có v > 0 mỗi người
- Tổng: v=2 168 | v=1 276 | v=0 49

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 26 | 3 | 0 | 10% |
| 1 | left_eye | 21 | 8 | 0 | 28% |
| 2 | right_eye | 22 | 7 | 0 | 24% |
| 3 | left_ear | 10 | 17 | 2 | 59% |
| 4 | right_ear | 13 | 15 | 1 | 52% |
| 5 | left_shoulder | 2 | 27 | 0 | 93% |
| 6 | right_shoulder | 2 | 27 | 0 | 93% |
| 7 | left_elbow | 12 | 15 | 2 | 52% |
| 8 | right_elbow | 13 | 15 | 1 | 52% |
| 9 | left_wrist | 11 | 15 | 3 | 52% |
| 10 | right_wrist | 15 | 12 | 2 | 41% |
| 11 | left_hip | 1 | 27 | 1 | 93% |
| 12 | right_hip | 1 | 27 | 1 | 93% |
| 13 | left_knee | 6 | 15 | 8 | 52% |
| 14 | right_knee | 5 | 16 | 8 | 55% |
| 15 | left_ankle | 5 | 14 | 10 | 48% |
| 16 | right_ankle | 3 | 16 | 10 | 55% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
