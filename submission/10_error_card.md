# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B2 | MISSING | 11 |
| center | B2 | SPURIOUS | 11 |
| center | B4 | DUPLICATE | 1 |
| center | B4 | STRUCTURE | 2 |
| edge | B2 | MISSING | 2 |
| edge | B2 | SPURIOUS | 3 |
| edge | B2 | WRONG_CLASS | 1 |
| mid | B2 | ATTRIBUTE | 1 |
| mid | B2 | MISSING | 5 |
| mid | B2 | SPURIOUS | 16 |
| unknown | B2 | STRUCTURE | 2 |
| unknown | C0 | IGNORE_SCOPE | 1 |
| unknown | C0 | SPURIOUS | 1 |
| unknown | C0 | WRONG_CLASS | 1 |

## Top defects
- SPURIOUS: 31 (ví dụ frame aggregate_48_frames)
- MISSING: 18 (ví dụ frame adasind_060000.jpg)
- STRUCTURE: 4 (ví dụ frame adasind_270517.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: `SPURIOUS` đứng đầu (31), nhưng con số này gộp lỗi learner, model-only và ba dòng calibration nên không được hiểu là 31 lỗi của annotator. Ở learner B2-mid, nguyên nhân có bằng chứng là `E1_annotator_error`: bốn `ignore_region` dùng box thay polygon, một Bike bị gọi Car ở `adasind_086220.jpg`, và xe mép trái bị gọi ThreeWheeler thay vì Truck ở `adasind_102750.jpg`. Nhiều dòng `M_only` là `E4_model_domain`, ví dụ model tách rider thành Bike + Pedestrian hoặc đặt nhiều class lên cùng một xe.
- Cách sửa và ai nhận việc (`owner`): annotator đã sửa các ca P1 trong ZIP rework khóa `CBE9-BB9D`; `delta.md` cho thấy missing về 0 ở cả ba zone và spurious sau sửa còn center=1, mid=0, edge=0. Ca `adasind_102750.jpg/L1` chưa đủ bằng chứng được giao `qa` với action `escalate`; lỗi model-only giao `ai_team` và không chép box model vào nhãn.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `screenshots/p5_086220_bike_rework.png`, `screenshots/p5_102750_truck_rework.png`, `screenshots/escalation_102750_L1.png`; các dòng tương ứng trong `findings.csv`; R01–R06 trong `docs/02-rules-vi.md`; và bảng trước/sau trong `rework/delta.md`.
