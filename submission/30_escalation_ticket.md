# Escalation ticket

## Ticket 1

- **Frame:** `adasind_102750.jpg`, learner `L1` trong bản khóa đầu (`x424.05–458.50, y936.04–980.52`).
- **Ảnh chụp:** `submission/screenshots/escalation_102750_L1.png`.
- **Expected impact:** learner thấy một vật thật và gán `ThreeWheeler`; model cũng thấy cùng geometry nhưng gán `Truck`; teaching reference không có box. Nếu tự xóa theo reference, có thể biến một reference defect thành lỗi annotator; nếu giữ sai class, thống kê spurious/class cũng bị lệch một ca center.
- **Owner:** `qa`.
- **Recommendation:** QA/Lab Coach mở ảnh full-resolution và nếu có thể xem frame lân cận để phân biệt thùng chở hàng với khoang chở người; sau đó chốt `Truck`/`ThreeWheeler` hoặc sửa teaching reference. Tạm giữ annotation, không dùng kết quả model làm quyết định cuối.
