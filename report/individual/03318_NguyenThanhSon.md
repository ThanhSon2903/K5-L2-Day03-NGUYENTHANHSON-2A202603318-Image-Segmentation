# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2B-03318
- Ngày / CVAT local: 12/11/2026
- Công cụ đã dùng: CVAT

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic | 3 / 3 |  |
| medium_instance | medium_instance.zip | 3 / 3 |  |
| hard_panoptic | hard_panoptic.zip | 1 / 2 |  |
| cp1_holes | cp1_holes.zip | 1 / 1 |  |
| cp2_slice | cp2_slice.zip | 1 / 1 |  |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 |  |
| cp3_thin | cp3_thin.zip | 1 / 1 |  |
| cp4_curb | cp4_curb.zip | 1 / 1 |  |
| cp6_coverage | cp6_coverage.zip | 1 / 1 |  |
| **Tổng tối đa** | | | **** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Object xe ô tô ở khu vực bên trái, nửa dưới ảnh trong task medium_instance.
- Class và quy tắc tôi dùng để chọn biên: Tôi chọn class car. Khi vẽ mask, tôi chỉ annotate phần thân xe thực sự nhìn thấy, cố gắng bám sát đường viền của xe và không lấy thêm phần nền xung quanh. Với những phần bị vật thể khác che khuất, tôi không tự suy đoán phần biên phía sau mà chỉ vẽ phần có thể quan sát được.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Tôi kiểm tra vùng mask được đề xuất bằng cách so sánh với đường viền thực tế của object. Nếu mask bị tràn ra nền hoặc ăn sang object khác, tôi sẽ chỉnh sửa hoặc xóa phần bị sai. Tôi chỉ giữ lại những vùng khớp với object sau khi kiểm tra.
- Nếu không dùng gợi ý: Không dùng gợi ý tự động cho object đầu tiên. Tôi tự xác định class và vẽ mask dựa trên hình dạng, màu sắc và đường biên quan sát được trên ảnh.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: cp2_slice – vùng hai xe nằm gần nhau trong ảnh.

Lỗi thuộc loại: Gộp object.

- - Bằng chứng tôi nhìn thấy: Hai xe là hai object riêng biệt nhưng phần mask ban đầu bị nối hoặc gộp vào nhau, khiến chúng không còn được phân biệt rõ ràng.

- Quy tắc và hành động sửa: Mỗi object phải có một mask riêng, kể cả khi chúng cùng class. Tôi kiểm tra lại ranh giới giữa hai xe, tách phần mask bị gộp và chỉnh lại đường biên để mỗi xe có vùng annotation độc lập.

- -Tôi kiểm tra lại annotation sau khi chỉnh sửa và thực hiện Save. Chưa có kết quả scorer xác nhận sau sửa.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| cp5_occlusion – phần xe bị một vật thể khác che khuất | Chỉ annotate phần xe nhìn thấy hoặc suy đoán và vẽ cả phần bị che | Quan sát trực tiếp các pixel còn nhìn thấy, không có đủ thông tin để xác định chính xác đường biên phía sau vật che | Tôi chọn annotate phần xe nhìn thấy, không tự suy đoán phần bị che. Muốn hỏi coach liệu có trường hợp ngoại lệ nào được phép suy luận mask không? |
| cp4_curb – vùng ranh giới giữa lòng đường và bó vỉa | Thuộc class road hoặc sidewalk | Quan sát sự thay đổi về độ cao, hình dạng và ranh giới giữa mặt đường với phần vỉa hè | Tôi chọn sidewalk đối với phần bề mặt vỉa hè được nâng cao. Tuy nhiên, muốn coach xác nhận cách xử lý phần mép bó vỉa có màu gần giống mặt đường. |
| easy_semantic – vùng vạch kẻ đường trên mặt đường | Annotate thành class road_marking hoặc gộp vào class road | Vạch kẻ có màu sắc và hình dạng riêng, phân biệt được với bề mặt nhựa đường xung quanh | Tôi chọn annotate vạch kẻ theo class riêng nếu class này có trong danh sách nhãn, đồng thời giữ ranh giới sát với phần vạch thực tế. Muốn coach xác nhận cách xử lý các vùng vạch bị mờ hoặc đứt đoạn. |

