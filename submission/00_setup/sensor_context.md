# Sensor context

- **Rig:** ADASIND không kèm tài liệu rig chi tiết. Từ ba ảnh của slice `B2-mid`, chỉ có thể xác nhận đây là một
  camera fisheye nhìn ra đường; chưa đủ bằng chứng để kết luận chính xác vị trí, độ cao hay hướng lắp camera trên xe.
- **`ego_body`:** Cả ba frame đều có phần tay/cánh tay người lái và một phần tay lái hoặc thân xe xuất hiện sát mép
  trái, chủ yếu ở nửa dưới ảnh. Chỉ vùng nhìn thấy này mới được cân nhắc cho `ego_body`; không suy diễn phần nằm ngoài
  khung hình.
- **Vòng kính:** Vùng ảnh hợp lệ có dạng gần tròn, nằm gần giữa khung hình, gần chạm hai mép trái/phải và chiếm phần
  lớn chiều cao. Phần ngoài vòng kính là vùng tối rõ nhất ở phía trên, phía dưới và các góc; chưa có calibration để
  suy ra góc nhìn hay khoảng cách thật.
