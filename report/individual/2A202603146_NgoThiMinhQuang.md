# Báo cáo thực hành Day 3

- **Mã học viên:** 2A202603146
- **Họ tên:** Ngô Thị Minh Quang
- **Bài thực hành:** K5 · Level 2 · Day03 — Image Segmentation (cá nhân)
- **Ngày / môi trường CVAT local:** Chưa được tôi ghi nhận cụ thể (không có bằng chứng xác minh chi tiết).
- **Công cụ:** Tôi thực hiện trên **CVAT local** và sử dụng **SAM3** là **công cụ AI duy nhất** hỗ trợ gợi ý phân đoạn khi cần.

## 1. Bài đã nộp

Tôi đã hoàn thành và export **9/9 task, 14/14 ảnh** trong thư mục `submissions/` (giữ nguyên các file ZIP hiện tại, không thay đổi annotation/ZIP/Ground Truth).

| Task | File ZIP | Hoàn thành | Điểm tối đa (coach chấm) |
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

**Kết quả tự đánh giá (3 tier, Ground Truth do giảng viên cung cấp, scorer chính thức):**
- Easy Semantic: **17.2/20**
- Medium Instance: **21.6/32**
- Hard Panoptic: **13.8/30**
- **Tổng tự đánh giá: 52.6/82**
- **Sáu checkpoint:** cấu trúc đã kiểm tra (inspect OK), **chưa có điểm định lượng**.

Kết quả trên là tự đánh giá, không phải điểm chính thức của giảng viên. Tôi giữ nguyên toàn bộ kết quả, annotation và ZIP.

### Phương pháp thực hiện (tổng quan)
- Tôi **trực tiếp thao tác trên CVAT** để thực hiện bài thực hành.
- Tôi **vẽ polygon/mask và gán nhãn theo từng đối tượng/vùng** theo đúng schema và `classes.json` của từng task.
- Tôi **chủ động xác định ranh giới, phân biệt class và kiểm tra vùng phân đoạn** (phần nhìn thấy, mức độ phủ, biên) trước khi lưu/export.
- Tôi sử dụng **SAM3 là công cụ AI duy nhất** hỗ trợ gợi ý/nhận diện vùng phân đoạn khi cần. **Tôi không sử dụng YOLO hay bất kỳ mô hình AI nào khác** để tự động tạo annotation.
- **SAM3 chỉ đóng vai trò hỗ trợ gợi ý**; việc kiểm tra, chỉnh lựa chọn (chấp nhận/bỏ qua gợi ý khi áp dụng), gán nhãn và quyết định cuối cùng đối với annotation thuộc trách nhiệm của tôi. Tôi không mô tả toàn bộ annotation là vẽ tay 100% trong các trường hợp có mask được tạo từ gợi ý SAM3.

## 2. Quy trình vẽ và gán nhãn

Quy trình tôi thực hiện (tổng quát) như sau:

1. **Quan sát ảnh gốc:** xem bối cảnh, đối tượng/vùng xuất hiện và các vùng khó (biên, che khuất, chi tiết nhỏ).
2. **Xác định đối tượng và class:** đối chiếu đúng `classes.json`/schema của task (semantic/instance/panoptic) và quy tắc guideline.
3. **Thực hiện vẽ mask trên CVAT:** vẽ polygon/mask theo từng đối tượng (instance/thing) hoặc từng vùng (semantic/stuff) bằng công cụ CVAT, bám phần **nhìn thấy**.
4. **Sử dụng SAM3 hỗ trợ khi cần:** dùng SAM3 để nhận diện và gợi ý vùng phân đoạn; tôi xem xét gợi ý như hỗ trợ, không thay thế bước kiểm tra của tôi. (Tôi không nêu tên/định danh object đầu tiên hay vị trí cụ thể do không có dữ liệu xác minh.)
5. **Kiểm tra ranh giới, che khuất và chi tiết nhỏ:** rà biên, vùng bị che khuất, vật mảnh/vùng lỗ, trường hợp vật sát nhau hoặc cùng class, và độ phủ theo schema.
6. **Kiểm tra lại và lưu/export:** kiểm tra lớp, số object/vùng, biên và tính nhất quán rồi Save và export đúng định dạng (`Segmentation mask 1.1` hoặc `COCO 1.0` theo từng task).

## 3. Khó khăn và xử lý lỗi

### Khó khăn thực tế trong quá trình thực hiện
- **Phân biệt các phương tiện cùng class nằm gần nhau:** khó xác định ranh giới tách instance khi các xe/vật cùng lớp sát hoặc chồng bóng, dễ gộp nhầm hoặc tách chưa đúng.
- **Xử lý vật thể bị che khuất:** cần xác định phần nhìn thấy thuộc cùng một đối tượng hay khác đối tượng, tránh vẽ phần bị che và tránh tách/gộp instance sai.
- **Vẽ các cấu trúc mảnh:** các chi tiết nhỏ/mảnh khó bám biên chính xác, dễ mất nét hoặc lệch vùng khi thao tác mask.
- **Xác định ranh giới road và sidewalk:** ranh giới đôi khi mờ theo màu/ánh sáng; cần dựa vào bó vỉa và chức năng lối đi thay vì chỉ dựa màu bề mặt.
- **Đảm bảo độ phủ mask:** cần phủ đủ vùng nhìn thấy thuộc schema nhưng tránh tô vượt sang lớp/vùng không đúng hoặc bỏ sót vùng hợp lệ.

### Sự cố kỹ thuật: import nhãn background trong CVAT
Tôi **không có ghi nhận/bằng chứng xác minh** về việc tôi gặp sự cố kỹ thuật import nhãn `background` trong CVAT trong quá trình làm bài; do đó tôi **không thể mô tả sự cố hay cách xử lý thực tế cụ thể** cho trường hợp này và tôi không bịa thao tác. Nếu có phát sinh, nguyên tắc xử lý là đảm bảo bộ nhãn đúng theo `classes.json`/cấu hình task trước khi annotate và export.

### Phân biệt lỗi đã xử lý và lỗi chỉ phát hiện khi hậu kiểm
- **Lỗi tôi đã xử lý trong quá trình làm:** tôi không có ghi nhận cụ thể, có bằng chứng xác minh từng trường hợp đã chỉnh sửa trước khi export cuối; vì vậy tôi **không khẳng định** đã xử lý một lỗi cụ thể nào.
- **Lỗi chỉ phát hiện khi hậu kiểm:** những sai lệch được nhận thấy khi đối chiếu tự đánh giá với Ground Truth/scorer chính thức (ví dụ: medium_instance có dấu hiệu FP/instance thừa, P@0.5 0.55, R@0.5 0.90, TP/FP/FN 64/52/7; hard_panoptic có các lớp PQ thấp như sidewalk/bicycle/person/traffic light/motorcycle; easy_semantic có sidewalk IoU thấp) thuộc nhóm **chỉ phát hiện khi hậu kiểm**.
- Tôi **đã không sửa annotation/ZIP trên CVAT sau khi hoàn thành** (giữ nguyên kết quả nộp). Do đó tôi **không ghi** là đã sửa annotation nếu tôi không thực hiện.

## 4. Ba trường hợp phân tích

Tôi phân tích ba trường hợp theo guideline của bài (CP1, CP2, CP5), nêu hai khả năng xử lý, nguyên tắc áp dụng và cách xác định phương án đúng.

### CP1 — Holes (vùng lỗ bên trong đối tượng) — `data/checkpoints/cp1_holes/images/000000144300.jpg`
- **Hai khả năng xử lý:** (a) Coi vùng lỗ/kính/chi tiết hở bên trong vật là một phần cần được thể hiện đúng theo mask của đối tượng (giữ/loại đúng theo quy tắc nhìn thấy của vật); (b) Bỏ qua hoặc tô lấp vùng lỗ như thể nó thuộc đặc phần đặc của đối tượng.
- **Nguyên tắc guideline:** giữ đúng chi tiết/kính (vùng lỗ/không đặc) bên trong mask theo quy tắc task; phân biệt **chi tiết bên trong vật** và **lỗ nền thật** nhìn xuyên qua (`CHECKPOINTS.md` — cp1_holes).
- **Cách tôi xác định phương án đúng:** tôi dựa vào phần **nhìn thấy thực tế** trên ảnh, kiểm tra biên trong–ngoài của vật và chỉ gán theo quy tắc lớp/đối tượng của trạm; không suy đoán phần không nhìn thấy, ưu tiên nhất quán giữa vùng đặc của vật và vùng hở/kính theo guideline.

### CP2 — Slice (các phương tiện cùng class nằm sát nhau) — `data/checkpoints/cp2_slice/images/000000017627.jpg`
- **Hai khả năng xử lý:** (a) Tách thành **hai instance riêng** cho hai phương tiện dù cùng class và nằm sát nhau; (b) Gộp thành một mask/instance duy nhất vì cùng class và biên tiếp xúc.
- **Nguyên tắc guideline:** **cùng class không đồng nghĩa cùng instance**; mỗi vật đếm được cần được tách đúng thành instance riêng khi chúng là các đối tượng khác nhau (`CHECKPOINTS.md` — cp2_slice).
- **Cách tôi xác định phương án đúng:** tôi quan sát ranh tiếp xúc, hình dạng và tính liên tục của từng phương tiện, xác định số lượng đối tượng thực tế và vẽ/tách mask theo từng instance; ưu tiên biên bám phần nhìn thấy của từng xe thay vì gộp theo màu hay độ gần.

### CP5 — Occlusion (đối tượng bị che khuất) — `data/checkpoints/cp5_occlusion/images/000000336232.jpg`
- **Hai khả năng xử lý:** (a) Giữ **một instance** cho các phần **nhìn thấy** của cùng một vật dù bị vật khác che khuất ở giữa; (b) Tách thành hai instance/ID khác nhau hoặc vẽ cả phần bị che khuất.
- **Nguyên tắc guideline:** **giữ một instance cho các phần nhìn thấy** của cùng vật; **không vẽ phần bị che** và **không tách ID chỉ vì bị che** (`CHECKPOINTS.md` — cp5_occlusion).
- **Cách tôi xác định phương án đúng:** tôi xác định các mảng nhìn thấy có thuộc cùng một đối tượng hay không dựa trên ngữ cảnh và tính nhất quán của vật, chỉ gán mask cho phần nhìn thấy và giữ cùng ID/instance cho cùng vật; không suy đoán hình dạng phía sau vật che.

## 5. Xác nhận giữ nguyên kết quả

- Tôi giữ nguyên **9 task, 14 ảnh** và **toàn bộ 9 file ZIP** trong `submissions/`.
- Kết quả tự đánh giá giữ nguyên: **Easy 17.2/20, Medium 21.6/32, Hard 13.8/30, Tổng 52.6/82**. **Sáu checkpoint chưa có điểm định lượng.**
- Tôi **không thay đổi annotation, ZIP hoặc Ground Truth**. Những nội dung tôi không có bằng chứng xác minh được nêu rõ trong báo cáo và tôi không bịa thao tác cá nhân.