# Guideline patch

- **Rule mới đề xuất:** Bổ sung R05a: không suy `truncated=true` chỉ vì cạnh box chạm biên ảnh. Chỉ đặt `true` khi đường bao nhìn thấy của vật thực sự bị vòng kính hoặc khung ảnh cắt; nếu toàn bộ silhouette vẫn nhìn thấy nhưng box sát biên do méo fisheye, giữ `false`. Ca khó phải lưu crop và được QA xác nhận.
- **Áp dụng cho:** attribute `truncated` ở zone `edge`, đặc biệt vật lớn sát vòng kính/biên ảnh.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R05 định nghĩa “bị cắt bởi vòng kính hoặc biên”, nhưng chưa nói rõ chạm biên theo tọa độ box có tự động đồng nghĩa bị cắt hay phải dựa vào silhouette. Điều này tạo bất đồng thật tại `adasind_086220.jpg`, learner L5/reference R1.
- **`rules_version` mới:** v1.0.0 → v1.1.0.
- **Hiệu lực từ:** vòng annotation tiếp theo, chỉ sau khi Lab Coach/QA duyệt; không hồi tố thay đổi bản khóa `70CA-9446`.
