# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 9 | 4 | 2 | 5 | 8 | MISSING (4) |
| mid | 8 | 0 | 3 | 4 | 10 | SPURIOUS (3) |
| edge | 3 | 1 | 2 | 2 | 0 | WRONG_CLASS (1) |

## Nhận xét

- Với người gán nhãn (L), **center** gãy nhiều nhất về bỏ sót: 4 missing trên 9 reference; **mid** không thiếu nhưng có 3 spurious; **edge** có 1 missing, 2 spurious và lỗi chính là một ca `WRONG_CLASS`. Ở IoU=0.50, toàn slice có TP=15, FP=7, FN=5; mean IoU của các TP là 0.867. Nhãn yếu nhất theo recall có mẫu là `Truck` (1/3 = 0.333); `Car` và `ignore_region` có precision 0 vì chỉ xuất hiện ở phía export, nhưng đây không phải kết luận chất lượng tổng quát.
- Model (M) gãy mạnh nhất ở **mid**, với 4 missing và 10 thừa; center có 5 missing và 8 thừa. Các cụm M-only cho thấy model hay tách rider thành `Pedestrian` + `Bike`, gán nhiều class lên cùng một xe và sinh box rất lớn. Méo fisheye, vật nhỏ/xa, che khuất và vùng blur làm class/geometry khó hơn. Đây chỉ là ba frame B2-mid và teaching reference chưa phải gold set; IoU sweep còn cho thấy kết quả đổi theo ngưỡng (ví dụ L mid từ 8 matched ở 0.50 xuống 7 ở 0.70), nên không dùng các số này làm ngưỡng đạt.
