# QA review · B4-center

Mã khóa: F688-0B1A

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_270517.jpg | L5 | R06 | Vùng che biển số của ThreeWheeler được xuất dưới dạng `box ignore_region`; R06 yêu cầu mỗi ignore region là polygon có đúng một `reason`. `reason=privacy_or_policy` hợp lệ nhưng shape cần đổi sang polygon bám vùng che. |
| adasind_271039.jpg | L14 và L5 | R02 | L14 nằm gần như hoàn toàn bên trong L5 và cùng bao một người mặc áo trắng, tạo hai box `Pedestrian` cho một vật. Giữ một box bám toàn bộ phần nhìn thấy và bỏ box trùng. |
| adasind_295948.jpg | L5 | R06 | Vùng che biển số trên xe tải được xuất dưới dạng `box ignore_region`; cần polygon `privacy_or_policy` bám vùng che thay vì hình chữ nhật bao dư nền. |

Phạm vi review: chỉ dùng ảnh gốc, luật v1.0.0 và bản export đã khóa `F688-0B1A`; chưa dùng teaching reference. Các `lens_border`/`ego_body` chính trong ba frame đã là polygon. L4 ở `adasind_295948.jpg` là người rất gần camera, chạm biên phải và đã có `truncated=true`, nên không ghi thành lỗi chỉ vì box lớn.

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
