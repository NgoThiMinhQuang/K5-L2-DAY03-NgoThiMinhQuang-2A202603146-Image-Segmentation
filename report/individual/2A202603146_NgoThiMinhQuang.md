# Báo cáo thực hành Day 3

**Ghi chú:** Tôi hoàn thiện báo cáo này dựa trên dữ liệu và kết quả thực tế của bài làm (ZIP đã export, kết quả kiểm tra cấu trúc, tự đánh giá, đối chiếu lỗi). Với những thông tin trải nghiệm cá nhân chưa có bằng chứng hoặc chưa được tôi xác nhận, tôi ghi rõ là **chưa được xác minh**; tôi không bịa trải nghiệm và không ghi là đã sửa nếu thực tế tôi không sửa.

- Mã học viên theo lớp: **2A202603146**
- Họ tên: **Ngô Thị Minh Quang**
- Ngày / CVAT local: **Chưa được xác minh** (tôi chưa ghi nhận cụ thể ngày thực hiện và phiên bản/môi trường CVAT local).
- Công cụ đã dùng: **CVAT local; tôi sử dụng SAM3 như công cụ hỗ trợ trong quá trình annotation**. Việc tôi có dùng thêm công cụ/gợi ý nào khác hay không: **chưa được xác minh**. (Các công cụ khác, nếu có, tôi chỉ dùng để hỗ trợ kiểm tra, phân tích và hoàn thiện báo cáo.)

## 1. Bài đã nộp

Tôi đã hoàn thành và export 9/9 task với 14/14 ảnh, lưu trong `submissions/` (tôi giữ nguyên các file ZIP này, không thay đổi sau khi export). Khi tôi kiểm tra cấu trúc bằng `python scripts/inspect_submissions.py --dir submissions`, kết quả là **9/9 OK, 0 lỗi**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `submissions/easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `submissions/medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `submissions/hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | `submissions/cp1_holes.zip` | 1 / 1 | 3 |
| cp2_slice | `submissions/cp2_slice.zip` | 1 / 1 | 3 |
| cp5_occlusion | `submissions/cp5_occlusion.zip` | 1 / 1 | 3 |
| cp3_thin | `submissions/cp3_thin.zip` | 1 / 1 | 3 |
| cp4_curb | `submissions/cp4_curb.zip` | 1 / 1 | 3 |
| cp6_coverage | `submissions/cp6_coverage.zip` | 1 / 1 | 3 |
| **Tổng tối đa** | | **14 / 14** | **100** |

**Tự đánh giá (ba tier, Ground Truth do giảng viên cung cấp, scorer chính thức):** easy_semantic **17.2/20**, medium_instance **21.6/32**, hard_panoptic **13.8/30** → **Tổng 52.6/82** (chỉ 3 tier). **Sáu checkpoint chưa có Ground Truth/tiêu chí chấm định lượng chính thức tương ứng nên chưa được chấm định lượng** (cấu trúc 6/6 OK). **Tôi không tự nhận đạt 100/100.** Chi tiết: `reports/final_testing/FINAL_SCORE_REPORT.md`.

Export lỗi: **Chưa được xác minh** (tôi chưa ghi nhận cụ thể việc có gặp lỗi export ở task/ảnh nào, trạng thái đã Save hay việc đã báo coach hay chưa).

## 2. Một quyết định trước khi dùng gợi ý

**Yêu cầu rubric/mục này:** ghi object đầu tiên tôi tự vẽ ở `medium_instance` trước khi xem đề xuất tự động cho object đó (ảnh/vị trí, class, quy tắc biên) và cách tôi xử lý gợi ý sau đó (nếu có).

**Mức độ đáp ứng / giới hạn thông tin:** Tôi có sử dụng **SAM3 như công cụ hỗ trợ trong quá trình annotation**, nhưng tôi **chưa có bằng chứng/ghi nhận cụ thể** để xác minh việc tôi đã tự vẽ hoàn toàn object đầu tiên trước gợi ý và các quyết định chi tiết tương ứng. Tôi **không bịa** thao tác hay trải nghiệm chưa được xác minh.

- Ảnh, vị trí và object Medium đầu tiên tôi tự vẽ: **Chưa được xác minh** (chưa xác định được ảnh cụ thể trong `000000181542.jpg` / `000000373353.jpg` / `000000458325.jpg`, vị trí/object).
- Class và quy tắc tôi dùng để chọn biên: **Chưa được xác minh**. (Nguyên tắc bài: class thuộc `person/bicycle/car/motorcycle/bus/truck`, biên bám phần nhìn thấy của object, không vẽ phần bị che/bối cảnh — đây là quy tắc tham chiếu, không phải ghi nhận quyết định cụ thể của tôi.)
- Khi tôi dùng SAM3/gợi ý sau đó: vùng gợi ý sai/đúng, hành động tôi sửa/giữ và lý do: **Chưa được xác minh** (chưa ghi nhận cụ thể). Tôi không ghi "không dùng" vì tôi có sử dụng SAM3 hỗ trợ.
- Nếu không dùng gợi ý: **Không áp dụng** (tôi có dùng SAM3 hỗ trợ). Quyết định gán nhãn cụ thể khác của tôi: **chưa được xác minh**.

## 3. Một lỗi tôi tìm thấy và sửa

**Yêu cầu rubric/mục này:** nêu một lỗi **có thật** đã tìm thấy và cách sửa (task/ảnh/vùng, loại, bằng chứng, quy tắc/hành động, Save/export). Nếu chưa sửa được phải ghi rõ, không ghi "đã sửa" khi chưa sửa.

**Mức độ đáp ứng / giới hạn thông tin:** Tôi **đã xác nhận không sửa annotation trên CVAT sau khi hoàn thành/export** và tôi **giữ nguyên 9 ZIP**. Tôi **không có bằng chứng xác minh** một lỗi cụ thể do tôi phát hiện trong quá trình làm (trước export cuối) cùng các thao tác sửa tương ứng; do đó tôi **không bịa** lỗi hay thao tác sửa. (Các sai lệch được nêu dưới đây chỉ là tham chiếu từ đối chiếu hậu kiểm với GT/scorer, không phải ghi nhận tôi đã phát hiện và sửa trong lúc làm.)

- Task/ảnh/vùng: **Chưa được xác minh** là lỗi tôi tự phát hiện trong quá trình làm. (Tham chiếu đối chiếu hậu kiểm: `medium_instance` có dấu hiệu nhiều instance thừa/FP, đặc biệt ảnh `000000373353.jpg` — `reports/error_localization/ERROR_LOCALIZATION.md`.)
- Lỗi thuộc loại: **Chưa được xác minh** (quan sát thực tế của tôi trong lúc làm chưa được ghi nhận). Tham chiếu hậu kiểm cho thấy thiếu-thừa vật/gộp-tách/biên (FP 52, submitted 116 vs GT 71).
- Bằng chứng tôi nhìn thấy: **Chưa được xác minh** (chưa ghi nhận bằng chứng cụ thể tôi quan sát trên CVAT trong quá trình làm).
- Quy tắc và hành động sửa: **Tôi không thực hiện sửa trên CVAT sau khi hoàn thành** (giữ nguyên kết quả/ZIP). Hướng xử lý phù hợp theo quy tắc (nếu sửa): xóa mask thừa, gộp mảnh cùng object, tách mask gộp nhiều object, chỉnh biên theo phần nhìn thấy. Việc tôi từng thử sửa trong quá trình làm trước khi export cuối hay không: **chưa được xác minh**.
- Sau sửa đã Save và export lại chưa? **Không áp dụng/không thực hiện** (tôi không sửa sau khi hoàn thành; ZIP hiện tại được giữ nguyên). Việc có lần Save/export lại nào khác trong quá trình làm: **chưa được xác minh**.

Kết quả liên quan (tự đánh giá): tôi đã tự đánh giá 3 tier bằng Ground Truth do giảng viên cung cấp và scorer chính thức → easy_semantic 17.2/20 (mIoU 0.787), medium_instance 21.6/32 (P@0.5 0.55, R@0.5 0.90, TP/FP/FN 64/52/7), hard_panoptic 13.8/30 (PQ 0.408) — **tổng 52.6/82** (chưa phải điểm cuối trên 100). Tôi không tự ghi PASS/top 3/bonus và không đưa file ground truth vào fork. (Các công cụ khác, nếu có, tôi chỉ dùng để hỗ trợ kiểm tra, phân tích và hoàn thiện báo cáo.)

## 4. Ba ca chưa chắc hoặc đã cân nhắc

**Yêu cầu rubric/mục này:** nêu ba ca (vùng cụ thể) có hai cách hiểu, kèm quy tắc/chứng cứ và quyết định hoặc câu hỏi cho coach (ca đã quyết định được cũng hợp lệ; không cần là lỗi).

**Mức độ đáp ứng / giới hạn thông tin:** Tôi **chưa có ghi nhận xác thực** về ba ca tôi đã cân nhắc trong quá trình làm; tôi **không tự tạo tình huống cá nhân** hay bịa trải nghiệm. Các ca dưới đây được nêu như **tình huống phân vân điển hình theo quy tắc/guideline của bài** (tham chiếu ảnh/vị trí trong dữ liệu) để đối chiếu quy tắc — **không khẳng định** là trải nghiệm đã xảy ra của tôi. Quyết định/câu hỏi của tôi cho từng ca: **chưa được xác minh**.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. cp4_curb — `data/checkpoints/cp4_curb/images/7d83710e-4697c3b2.jpg` (ranh road/sidewalk) — *ca tham chiếu theo guideline, chưa xác minh là tôi đã cân nhắc* | (a) Phân chia theo màu bề mặt nhựa/bê tông; (b) Phân chia theo bó vỉa/chức năng lối đi | `CHECKPOINTS.md`: ranh road–sidewalk theo bó vỉa và chức năng, không quyết định chỉ theo màu. `guideline-mini-sheet`/`GUIDE.md` | **Chưa được xác minh** (quyết định thực tế của tôi hoặc câu hỏi tôi muốn hỏi coach). |
| 2. cp5_occlusion — `data/checkpoints/cp5_occlusion/images/000000336232.jpg` (vật bị che) — *ca tham chiếu theo guideline, chưa xác minh là tôi đã cân nhắc* | (a) Tách thành hai object/ID khi bị vật khác che khuất; (b) Giữ một instance cho các phần nhìn thấy của cùng một vật | `CHECKPOINTS.md`: giữ một instance cho các phần nhìn thấy; không vẽ phần bị che; không tách ID vì bị che | **Chưa được xác minh** (quyết định thực tế của tôi hoặc câu hỏi tôi muốn hỏi coach). |
| 3. easy_semantic — `817bca71-00000000.jpg` (ranh road/sidewalk, vùng sidewalk/vegetation) — *ca tham chiếu theo guideline/đối chiếu hậu kiểm, chưa xác minh là tôi đã cân nhắc* | (a) Gom vùng theo màu/texture giống nhau; (b) Tách đúng lớp theo chức năng (road vs sidewalk) và phủ đúng vùng vegetation nhìn thấy | `GUIDE.md`: ranh road–sidewalk theo chức năng/bó vỉa; semantic phủ vùng nhìn thấy đúng lớp. Khi đối chiếu lại, sidewalk IoU thấp/FP-FN đáng kể trên ảnh này (`reports/final_testing/`, `reports/error_localization/`). | **Chưa được xác minh** (quyết định thực tế của tôi hoặc câu hỏi tôi muốn hỏi coach). |

---
**Ghi chú:** Tôi giữ nguyên kết quả và điểm số tự đánh giá **52.6/82** (3 tier) cùng các hạn chế đã phát hiện; tôi không thay đổi annotation/ZIP/điểm. Những thông tin chưa được xác minh nêu trên cần được tôi đối chiếu và bổ sung nếu có bằng chứng thực tế.
