# Quan sát vạch ô đỗ

- Hai vạch `parking_line` rõ nhất trong export là đoạn sơn chéo ở tiền cảnh giữa ảnh
  (`406.67,652.75 → 530.52,720.00`) và đoạn sơn chéo ở tiền cảnh bên phải
  (`696.46,621.83 → 960.00,685.61`). Lớp phủ cho thấy hai polyline này bám phần sơn nhìn thấy và mỗi vạch phân cách
  hai ô đỗ kề nhau.
- Không gán hàng rào và mép dải nền sáng chạy ngang phía sau xe đỏ làm `parking_line`, vì chúng là biên xa của bãi,
  không phải vạch sơn tạo ranh giới một ô đỗ riêng lẻ.
- Export hiện có hai polygon `free_space`. Khi chồng XML lên ảnh, polygon lớn phủ cả lối trống lẫn một phần các ô đỗ
  ở tiền cảnh; polygon còn lại là một dải hẹp men theo hàng vạch ở giữa ảnh. Vì `free_space` của bài chỉ là phần mặt
  đường trống nhìn thấy của **lối xe chạy**, hai polygon này có khả năng đang rộng hơn phạm vi cần gán và cần soát lại
  trong CVAT. Dù giữ hay sửa, polygon chỉ mô tả ảnh tĩnh, không chứng minh vùng lái xe an toàn.
- Ca cần người soát kiểm lại trước khi coi P0 hoàn tất: polyline dài
  (`0.00,542.50 → 960.00,508.09`) và polyline (`0.00,504.09 → 415.10,495.72`) chạy gần ngang qua nhiều ô. Chúng có
  thể là đường kết thúc hàng ô hoặc biên của lối xe chạy, không phải một vạch phân chia hai ô riêng lẻ. Ngoài ra cần
  thu hẹp `free_space` về phần lối xe chạy, tránh bao cả vùng nằm giữa các vạch của ô đỗ tiền cảnh.
