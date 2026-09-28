# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Chói sáng, vật xa/nhỏ, nhiều lớp che khuất và đối tượng gần seam trước-trái/phải | Méo fisheye và thay đổi tỷ lệ làm dễ bỏ sót hoặc vẽ box không bám phần nhìn thấy | Giữ ảnh fisheye gốc, độ phân giải, `camera_id=front`, timestamp, phiên bản intrinsic/extrinsic và lens mask | Annotator làm độc lập, QA thứ hai kiểm theo rule; bất đồng class/ignore/seam phải được adjudicator chốt và lưu decision log |
| rear | Vật sát đuôi xe, người/xe đi vào khi lùi, thiếu sáng và seam sau-trái/phải | Thân xe có thể che ảnh; vật vào rìa nhanh và bị truncated mạnh | Giữ ảnh gốc, lens mask, vùng ego body, `camera_id=rear`, timestamp và calibration dùng để chiếu BEV | Review riêng camera sau; soát cả object box và ignore region, rồi phân xử các ca sát thân xe trước khi đưa vào gold |
| left | Xe máy/người đi sát hông, che khuất, méo mạnh và seam trước-trái/sau-trái | Box thay đổi lớn theo vị trí; cùng vật có thể đồng thời xuất hiện ở camera kề | Giữ ảnh gốc chưa crop/resize, `camera_id=left`, timestamp đồng bộ và phiên bản calibration/seam mask | Một reviewer độc lập kiểm ca normal/hard; ca seam phải mở cùng frame camera kề và ghi quyết định giữ hai box hay liên kết |
| right | Xe máy/người đi sát hông, truncated ở rìa và seam trước-phải/sau-phải | Vùng nhìn bên hông hẹp theo hướng chuyển động và dễ nhầm hai lần xuất hiện là duplicate | Giữ ảnh gốc chưa biến đổi, `camera_id=right`, timestamp đồng bộ và calibration/seam mask | QA độc lập theo cùng guideline với camera trái; adjudicator xử lý bất đồng và kiểm tính nhất quán hai phía |

- **Khi cần refresh gold set:** đổi camera/lens hoặc vị trí lắp; cập nhật intrinsic/extrinsic, phép chiếu BEV hay seam mask;
  đổi taxonomy/rule/ignore policy; hoặc khi dữ liệu mới cho thấy phân bố ánh sáng, thời tiết, địa điểm hay lỗi khác rõ rệt
  so với bộ gold hiện tại. Mỗi lần refresh phải lưu phiên bản và review lại các ca bị ảnh hưởng.
- **Ca seam/cross-camera:** một xe máy xuất hiện đồng thời ở camera `front` và `right` tại seam trước-phải. Trước khi
  ghép hai box hoặc coi là `DUPLICATE`, cần timestamp đồng bộ, camera ID, intrinsic/extrinsic, vùng seam/BEV transform
  và policy output đích. Tạm giữ hai annotation gốc và lưu cặp đối tượng cùng quyết định của reviewer.
- **Giới hạn bằng chứng:** peer agreement hoặc quality report của ADASIND chỉ phản ánh một camera và một tập ảnh nhỏ;
  nó không bao phủ góc nhìn, ego body, méo rìa, seam, calibration hay phân bố normal/hard riêng của bốn camera.
  Vì vậy từng camera phải có mẫu và review độc lập trước khi bộ reference được gọi là gold cho hệ SVM.

> Cập nhật sau P4: B2-mid cho thấy learner bỏ sót nhiều nhất ở center (4/9 reference trước rework), có 3 spurious ở mid và một ca wrong-class ở edge; model có 10 thừa và 4 thiếu ở mid. Các tín hiệu này được dùng để tăng trọng số hard case vật nhỏ/xa, méo và class đặc biệt trong kế hoạch, nhưng không thay thế review riêng từng camera. Teaching reference ADASIND vẫn không được coi là gold set bốn camera.
