# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_060000.jpg
- L4 mid SPURIOUS
- L6 mid SPURIOUS
- R7 center MISSING
- R9 center MISSING
## adasind_086220.jpg
- L5+R1 mid ATTRIBUTE
- L4 center SPURIOUS
- R4 center MISSING
## adasind_102750.jpg
- L1 center SPURIOUS
- L5+R2 edge WRONG_CLASS
- L6 mid SPURIOUS
- L7 edge SPURIOUS
- R5 center MISSING

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 9 | 5 | 4 | 2 |
| mid | 8 | 8 | 0 | 3 |
| edge | 3 | 2 | 1 | 2 |
