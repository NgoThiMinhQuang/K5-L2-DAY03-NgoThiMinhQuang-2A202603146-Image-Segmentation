# BÁO CÁO CÁ NHÂN – K5 LEVEL 2 DAY 03: IMAGE SEGMENTATION

**Họ và tên:** Ngô Thị Minh Quang  
**Mã số sinh viên:** 2A202603146  
**Bài thực hành:** K5 – Level 2 – Day 03: Image Segmentation  
**Công cụ thực hiện:** CVAT, SAM3 hỗ trợ phân đoạn ảnh.

---

## 1. KẾT QUẢ THỰC HIỆN BÀI THỰC HÀNH

Trong quá trình thực hiện bài thực hành Image Segmentation, tôi trực tiếp thao tác trên CVAT để thực hiện gán nhãn, phân đoạn các đối tượng và hoàn thiện dữ liệu theo yêu cầu của từng task.

Bài thực hành gồm 9 task với tổng cộng 14 ảnh, bao gồm 3 nhóm chính: Easy Semantic Segmentation, Medium Instance Segmentation và Hard Panoptic Segmentation; cùng 6 checkpoint kiểm tra các trường hợp đặc biệt.

Tôi sử dụng CVAT làm công cụ chính để quản lý và thực hiện annotation. Trong quá trình làm bài, tôi sử dụng SAM3 làm công cụ AI hỗ trợ gợi ý phân đoạn. Tôi trực tiếp kiểm tra các vùng mask, class và ranh giới đối tượng trước khi hoàn thiện dữ liệu. Tôi không sử dụng YOLO hoặc mô hình AI khác để tự động tạo annotation cho bài nộp.

### Danh sách bài thực hành đã hoàn thành

| STT | Task | Số ảnh | Định dạng export |
|---|---|---:|---|
| 1 | Easy Semantic | 3 | Segmentation mask 1.1 |
| 2 | Medium Instance | 3 | COCO 1.0 |
| 3 | Hard Panoptic | 2 | COCO 1.0 |
| 4 | CP1 – Holes | 1 | COCO 1.0 |
| 5 | CP2 – Slice | 1 | COCO 1.0 |
| 6 | CP3 – Thin | 1 | Segmentation mask 1.1 |
| 7 | CP4 – Curb | 1 | Segmentation mask 1.1 |
| 8 | CP5 – Occlusion | 1 | COCO 1.0 |
| 9 | CP6 – Coverage | 1 | Segmentation mask 1.1 |
| | **Tổng cộng** | **14** | **9 ZIP** |

### Kết quả tự đánh giá

| Nhóm bài | Điểm đạt được | Điểm tối đa |
|---|---:|---:|
| Easy Semantic | 17.2 | 20 |
| Medium Instance | 21.6 | 32 |
| Hard Panoptic | 13.8 | 30 |
| **Tổng cộng** | **52.6** | **82** |

Đây là kết quả tự đánh giá theo scorer của bộ bài thực hành, không phải điểm chính thức do giảng viên công bố.

Đối với 6 checkpoint, tôi đã hoàn thành việc tạo dữ liệu, export và kiểm tra cấu trúc. Hiện chưa có kết quả chấm điểm định lượng riêng cho nhóm checkpoint.

---

## 2. QUY TRÌNH THỰC HIỆN VÀ PHƯƠNG PHÁP GÁN NHÃN

Trong quá trình làm bài, tôi thực hiện các thao tác trực tiếp trên CVAT, tập trung vào việc xác định đúng đối tượng, lựa chọn class và thể hiện chính xác ranh giới của từng vùng phân đoạn.

Quy trình thực hiện gồm:

**Bước 1 – Quan sát và nhận diện đối tượng**

Tôi quan sát ảnh gốc, xác định các đối tượng cần gán nhãn, phân biệt từng nhóm class và chú ý những trường hợp đối tượng nằm gần nhau, bị che khuất hoặc có hình dạng phức tạp.

**Bước 2 – Thực hiện annotation trên CVAT**

Tôi sử dụng các công cụ polygon và mask trên CVAT để thực hiện phân đoạn. Khi vẽ, tôi chú ý bám sát đường viền thực tế của đối tượng, tránh tạo vùng mask quá rộng hoặc bỏ sót những phần thuộc đối tượng.

Đối với các vật thể nằm sát nhau, tôi chú ý phân biệt ranh giới để tránh gộp nhầm nhiều đối tượng thành một instance.

**Bước 3 – Sử dụng SAM3 hỗ trợ**

Tôi sử dụng SAM3 để hỗ trợ nhận diện và gợi ý vùng phân đoạn trong quá trình làm bài. Các gợi ý được xem là cơ sở tham khảo; tôi kiểm tra lại hình dạng, phạm vi và class của đối tượng trước khi sử dụng kết quả.

**Bước 4 – Kiểm tra và hoàn thiện dữ liệu**

Sau khi annotation, tôi kiểm tra lại các vùng phân đoạn, nhãn class, số lượng đối tượng và những vị trí có khả năng bị bỏ sót hoặc gán nhãn chưa chính xác.

**Bước 5 – Lưu và export**

Tôi lưu kết quả trên CVAT và xuất dữ liệu theo định dạng yêu cầu của từng task. Sau đó, tôi kiểm tra cấu trúc các file ZIP trước khi đưa vào thư mục submissions.

Đối với object đầu tiên trong Medium Instance, hiện tôi không có đủ dữ liệu lịch sử thao tác để xác định chính xác ảnh, vị trí, class và thứ tự thực hiện trước khi sử dụng gợi ý SAM3. Vì vậy, tôi không đưa ra một mô tả cụ thể chưa được xác minh.

---

## 3. KHÓ KHĂN, LỖI PHÁT HIỆN VÀ CÁCH XỬ LÝ

Trong quá trình thực hiện, tôi gặp một số khó khăn liên quan đến việc xác định ranh giới đối tượng, phân biệt các instance cùng class và xử lý dữ liệu khi import/export.

### 3.1. Khó khăn trong quá trình annotation

**Đối tượng nằm gần nhau hoặc có ranh giới không rõ ràng**

Một số phương tiện xuất hiện sát nhau, khiến việc xác định ranh giới giữa các đối tượng trở nên khó khăn. Nếu không phân biệt chính xác, các vùng mask có thể bị gộp hoặc tạo ra nhiều instance không cần thiết.

Tôi chú ý quan sát hình dạng, đường viền và vị trí của từng đối tượng để xác định phạm vi phân đoạn phù hợp.

**Đối tượng bị che khuất**

Khi một phần đối tượng bị vật thể khác che khuất, việc xác định phạm vi mask cần tuân thủ quy tắc về occlusion. Đây là trường hợp cần phân biệt giữa một đối tượng bị che khuất và nhiều đối tượng độc lập.

**Các cấu trúc mảnh**

Những chi tiết nhỏ như cột, biển báo hoặc các cấu trúc mảnh đòi hỏi độ chính xác cao hơn khi xác định đường biên. Việc sử dụng công cụ vẽ không phù hợp có thể khiến mask bị thiếu hoặc lệch khỏi đối tượng.

**Ranh giới road và sidewalk**

Một số khu vực có màu sắc và chất liệu bề mặt tương tự nhau. Tôi cần chú ý đến ranh giới chức năng giữa lòng đường và vỉa hè thay vì chỉ dựa vào sự khác biệt về màu sắc.

### 3.2. Sự cố kỹ thuật khi import annotation

Trong quá trình import dữ liệu Semantic Segmentation vào CVAT, tôi gặp lỗi:

`Label 'background' is not registered for this task.`

Sau khi kiểm tra, tôi xác định vấn đề liên quan đến nhãn background trong file annotation không được đăng ký tương ứng trong danh sách label của task CVAT.

Tôi kiểm tra lại cấu hình nhãn và định dạng dữ liệu, sau đó xử lý việc import theo cấu trúc nhãn phù hợp để tiếp tục quy trình làm bài.

Đây là lỗi kỹ thuật liên quan đến quá trình import annotation, không phải lỗi chất lượng mask đã được sửa.

### 3.3. Kết quả hậu kiểm

Sau khi hoàn thành dữ liệu, tôi sử dụng công cụ inspect và đối chiếu kết quả tự đánh giá để kiểm tra chất lượng.

Một số hạn chế được ghi nhận:

- Easy Semantic: IoU của class sidewalk còn thấp, đạt 0.483.
- Medium Instance: số lượng instance dự đoán nhiều hơn Ground Truth, có 52 false positive và 7 false negative.
- Hard Panoptic: một số class như bicycle và sidewalk có PQ bằng 0; class person đạt PQ 0.177.

Tôi giữ nguyên 9 file ZIP đã export cuối cùng, không thực hiện chỉnh sửa annotation sau giai đoạn hoàn thành. Vì vậy, các lỗi chất lượng phát hiện trong quá trình hậu kiểm được ghi nhận là hạn chế còn tồn tại, không phải lỗi đã được sửa.

---

## 4. BA TÌNH HUỐNG ĐẶC BIỆT CẦN LƯU Ý KHI GÁN NHÃN

Trong quá trình nghiên cứu guideline và thực hiện các checkpoint, tôi tập trung vào ba trường hợp có khả năng gây nhầm lẫn khi phân đoạn.

### Tình huống 1 – CP1 Holes: Khoảng trống bên trong đối tượng

**Vấn đề:**

Một đối tượng có thể xuất hiện các khoảng trống hoặc lỗ bên trong hình dạng tổng thể. Nếu chỉ dựa vào đường viền bên ngoài, người thực hiện có thể nhầm lẫn giữa phần bên trong đối tượng và vùng nền.

**Hai cách hiểu có thể gặp:**

- Cách 1: Loại bỏ toàn bộ phần trống bên trong khỏi mask.
- Cách 2: Giữ mask liên tục theo phạm vi đối tượng, không tự ý cắt các khoảng trống theo quy tắc của checkpoint.

**Nguyên tắc áp dụng:**

Theo quy tắc CP1 Holes, các cửa sổ và khoảng trống được yêu cầu giữ bên trong mask, không tự ý cắt bỏ.

**Bài học:**

Tôi cần phân biệt rõ đặc điểm hình học của đối tượng với những vùng nền thực sự, đồng thời tuân thủ quy tắc riêng của checkpoint.

### Tình huống 2 – CP2 Slice: Các phương tiện cùng class nằm sát nhau

**Vấn đề:**

Nhiều phương tiện có thể xuất hiện cạnh nhau, thậm chí có phần hình ảnh tiếp giáp hoặc chồng lấn do góc chụp.

**Hai cách hiểu có thể gặp:**

- Cách 1: Gộp các phương tiện cùng class thành một vùng mask.
- Cách 2: Tạo mask riêng cho từng phương tiện độc lập.

**Nguyên tắc áp dụng:**

Theo CP2 Slice, các phương tiện liền kề nhưng là những đối tượng khác nhau phải được tách thành các instance riêng biệt.

**Bài học:**

Tôi cần quan sát cấu trúc từng phương tiện, xác định ranh giới và tránh gộp nhiều đối tượng thành một instance chỉ vì chúng có cùng class.

### Tình huống 3 – CP5 Occlusion: Đối tượng bị che khuất

**Vấn đề:**

Một đối tượng có thể bị một đối tượng khác che khuất một phần. Khi đó, hình ảnh quan sát được không thể hiện đầy đủ hình dạng ban đầu của đối tượng.

**Hai cách hiểu có thể gặp:**

- Cách 1: Tách phần đối tượng nhìn thấy thành nhiều mask riêng.
- Cách 2: Xem các phần nhìn thấy thuộc cùng một đối tượng là một instance duy nhất.

**Nguyên tắc áp dụng:**

Theo CP5 Occlusion, một đối tượng bị chia cắt về mặt hình ảnh do vật thể khác che khuất vẫn được tính là một mask duy nhất; đồng thời phải xác định đúng số lượng instance.

**Bài học:**

Tôi cần phân biệt sự gián đoạn về mặt hình ảnh với sự tồn tại của nhiều đối tượng độc lập. Đây là yếu tố quan trọng để đảm bảo tính nhất quán trong Instance Segmentation.

---

## 5. TỰ ĐÁNH GIÁ VÀ KINH NGHIỆM RÚT RA

Qua bài thực hành, tôi hiểu rõ hơn sự khác biệt giữa Semantic Segmentation, Instance Segmentation và Panoptic Segmentation.

Tôi nhận thấy độ chính xác của annotation phụ thuộc nhiều vào khả năng nhận diện đối tượng, xác định ranh giới và áp dụng đúng quy tắc của từng class.

Việc sử dụng SAM3 giúp hỗ trợ quá trình nhận diện và gợi ý vùng phân đoạn, tuy nhiên kết quả vẫn cần được kiểm tra theo guideline. Công cụ hỗ trợ không thay thế trách nhiệm của người thực hiện trong việc đánh giá và kiểm soát chất lượng dữ liệu.

Những điểm tôi cần cải thiện trong các bài thực hành tiếp theo gồm:

- Nâng cao độ chính xác khi vẽ các đường biên phức tạp.
- Kiểm soát tốt hơn số lượng instance, hạn chế tình trạng dự đoán thừa.
- Chú ý hơn đến các class có ranh giới tương tự nhau.
- Kiểm tra kỹ vùng bị che khuất và những cấu trúc nhỏ.
- Đối chiếu kết quả với guideline trước khi export dữ liệu.

**Kết luận:** Tôi đã hoàn thành việc xây dựng và export dữ liệu cho 9 task với tổng cộng 14 ảnh, đồng thời thực hiện kiểm tra cấu trúc các file bài nộp. Qua bài thực hành, tôi có thêm kinh nghiệm về quy trình annotation trên CVAT, cách sử dụng công cụ hỗ trợ phân đoạn và những yêu cầu về chất lượng dữ liệu trong Image Segmentation.

Tôi nhận thức được một số hạn chế còn tồn tại trong kết quả tự đánh giá và sẽ tiếp tục cải thiện độ chính xác, tính nhất quán trong những bài thực hành tiếp theo.