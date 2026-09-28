# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_102750.jpg` | Trước rework: một `WRONG_CLASS`, một missing Truck, hai privacy box sai structure và một ca L/model/reference bất đồng | Có đồng thời vật nhỏ, edge fisheye, class đặc biệt và một escalation chưa phân xử; đây là frame có local precision thấp nhất trong báo cáo trước sửa (0.429) | `screenshots/p5_102750_truck_rework.png`, `screenshots/escalation_102750_L1.png`, XML trước/sau, `findings.csv` và ticket QA |
| `adasind_060000.jpg` | Trước rework: hai missing, hai privacy box sai structure; model còn tách rider và sinh nhiều class chồng nhau | Cho thấy lỗi bỏ sót vật vừa qua H=40 và lỗi model khác với lỗi annotator; cần ưu tiên kiểm coverage trước khi đọc chỉ số tổng | Ảnh gốc, overlay `compare.html`, các dòng R7/R9 và L4/L6 trong `findings.csv`, số trước/sau trong `delta.md` |

Giới hạn của kết luận từ ba frame ADASIND: ba ảnh chỉ thuộc B2-mid của một camera, không đại diện đủ ánh sáng, thời tiết, camera, seam hay phân bố class. Teaching reference là bản phục vụ bài học chứ chưa phải gold set. Vì vậy 15 TP, 7 FP, 5 FN và mean IoU 0.867 trước sửa chỉ mô tả slice/thiết lập IoU=0.50 này, không phải điểm đạt cho hệ SVM.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv`: lấy đủ 8 ô front/rear/left/right × normal/hard, chọn frame cách nhau theo thời gian hoặc theo scene ID để không coi nhiều frame liên tiếp của một sự kiện là các ca độc lập, giữ timestamp và calibration, rồi kiểm phân bố ánh sáng, mật độ, class, occlusion, truncated, ego body và seam. Các ca hard được tăng lên 30/camera vì B2-mid cho thấy vật nhỏ/xa, edge và class đặc biệt dễ sai. Đây là mẫu rủi ro có chủ đích để tìm ca cần soi; không phải mẫu ngẫu nhiên đại diện nên không dùng để ước lượng tỷ lệ lỗi toàn bộ 50.000 frame.
