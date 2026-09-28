# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao? Không tự coi là `DUPLICATE`: mỗi box có thể hợp lệ trong annotation space của camera riêng. Cần rule cross-camera quy định output đích là giữ cả hai, chọn một hay hợp nhất ở BEV. Chỉ quyết định sau khi có `camera_id`, timestamp đồng bộ, intrinsic/extrinsic và seam mask; trước đó giữ hai annotation gốc.
2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera. Giữ cùng track ID khi identity còn liên tục và có thể nhận ra là cùng vật. Thêm keyframe khi geometry hoặc attribute thay đổi đáng kể; đặt Outside khi vật rời trường nhìn và mở lại khi guideline cho phép. Muốn nối qua hai camera cần timestamp, calibration, vùng overlap/seam, thứ tự chuyển động và policy re-identification/output; chỉ giống hình hoặc gần vị trí là chưa đủ.
3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm? Ở `adasind_086220.jpg`, learner L5/reference R1, reference đặt `truncated=true` còn nhóm xác nhận chiếc ThreeWheeler chỉ sát mép và vẫn nhìn đủ. Nhóm giữ `false`, ghi `keep_with_reason` và đề xuất R05a thay vì sửa theo reference một cách máy móc. Nếu làm lại, tôi sẽ zoom và lưu crop đường bao sát biên ngay trước khi khóa, đồng thời kiểm tra toàn bộ `privacy_or_policy` là polygon để tránh vòng rework cấu trúc.
