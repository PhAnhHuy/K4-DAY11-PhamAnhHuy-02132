# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 5 | 9 | 4 | 0 | 2 | 1 |
| mid | 8 | 8 | 0 | 0 | 3 | 0 |
| edge | 2 | 3 | 1 | 0 | 2 | 0 |

## Findings action=rework
- adasind_060000.jpg L4 SPURIOUS: đã sửa
- adasind_060000.jpg L6 SPURIOUS: đã sửa
- adasind_060000.jpg R7 MISSING: đã sửa
- adasind_060000.jpg R9 MISSING: đã sửa
- adasind_086220.jpg L4 SPURIOUS: đã sửa
- adasind_086220.jpg R4 MISSING: đã sửa
- adasind_086220.jpg IR_box_413_1003 STRUCTURE: không áp dụng
- adasind_086220.jpg IR_box_337_981 STRUCTURE: không áp dụng
- adasind_102750.jpg L5+R2 WRONG_CLASS: đã sửa
- adasind_102750.jpg L6 SPURIOUS: đã sửa
- adasind_102750.jpg L7 SPURIOUS: đã sửa
- adasind_102750.jpg R5 MISSING: đã sửa
- adasind_060000.jpg L4 SPURIOUS: đã sửa
- adasind_060000.jpg L6 SPURIOUS: đã sửa
- adasind_060000.jpg R7+M6 MISSING: đã sửa
- adasind_060000.jpg R9 MISSING: đã sửa
- adasind_086220.jpg L4+M8 SPURIOUS: đã sửa
- adasind_086220.jpg R4 MISSING: đã sửa
- adasind_102750.jpg L5 SPURIOUS: đã sửa
- adasind_102750.jpg L6 SPURIOUS: đã sửa
- adasind_102750.jpg L7 SPURIOUS: đã sửa
- adasind_102750.jpg R2+M2 MISSING: đã sửa
- adasind_102750.jpg R5+M8 MISSING: đã sửa

## Diễn giải

- Bản rework khóa `CBE9-BB9D` tăng matched center từ 5 lên 9 và edge từ 2 lên 3; missing ở center/mid/edge đều về 0. Spurious giảm center 2→1, mid 3→0 và edge 2→0.
- Hai finding `IR_box_413_1003` và `IR_box_337_981` hiện “không áp dụng” vì nhóm đã kiểm tra trực tiếp rồi xóa hai annotation không cần thiết, thay vì đổi chúng thành polygon. Các vùng privacy cần giữ ở ba frame đều đã là polygon với `reason=privacy_or_policy`.
- Một spurious center còn lại là `adasind_102750.jpg/L1`: learner và model cùng thấy vật nhưng bất đồng class, teaching reference không có. Ca này được giữ và chuyển QA trong `30_escalation_ticket.md`; không sửa chỉ để làm đẹp chỉ số.
