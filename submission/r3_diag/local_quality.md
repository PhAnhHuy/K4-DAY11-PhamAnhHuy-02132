# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `70ca9446b3bbf1eedabb5a7afd9424f63c13ba035302073c8861e2c75568bc69`; slice `B2-mid`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_060000.jpg, adasind_086220.jpg, adasind_102750.jpg. Frame thiếu trong export: không.
TP=15; FP=7; FN=5; số lần đối chiếu=26; mean IoU của TP=0.867.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.577 | 0.923 | 0.846 |
| precision | 0.682 | 0.633 | 0.000 |
| recall | 0.750 | 0.454 | 0.000 |
| jaccard | 0.556 | 0.427 | 0.000 |
| dice | 0.714 | 0.509 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 3 | 0 | 1 | 0.962 | 1.000 | 0.750 | 0.750 | 0.857 |
| Car | 0 | 1 | 0 | 0.962 | 0.000 | 0.000 | 0.000 | 0.000 |
| Pedestrian | 3 | 0 | 1 | 0.962 | 1.000 | 0.750 | 0.750 | 0.857 |
| ThreeWheeler | 8 | 2 | 1 | 0.885 | 0.800 | 0.889 | 0.727 | 0.842 |
| Truck | 1 | 0 | 2 | 0.923 | 1.000 | 0.333 | 0.333 | 0.500 |
| ignore_region | 0 | 4 | 0 | 0.846 | 0.000 | 0.000 | 0.000 | 0.000 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_060000.jpg | 8 | 2 | 2 | 0.667 | 0.800 | 0.800 |
| adasind_086220.jpg | 4 | 1 | 1 | 0.667 | 0.800 | 0.800 |
| adasind_102750.jpg | 3 | 4 | 2 | 0.375 | 0.429 | 0.600 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | ignore_region | <missing> |
|---|---:|---:|---:|---:|---:|---:|---:|
| Bike | 3 | 0 | 0 | 0 | 0 | 0 | 1 |
| Car | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Pedestrian | 0 | 0 | 3 | 0 | 0 | 0 | 1 |
| ThreeWheeler | 0 | 0 | 0 | 8 | 0 | 0 | 1 |
| Truck | 0 | 0 | 0 | 1 | 1 | 0 | 1 |
| ignore_region | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| <extra> | 0 | 1 | 0 | 1 | 0 | 4 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
