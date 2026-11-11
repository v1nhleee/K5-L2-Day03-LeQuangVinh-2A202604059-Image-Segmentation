# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202604059
- Ngày / CVAT local: 11/11/2026 / CVAT local running (Docker container)
- Công cụ đã dùng: CVAT thủ công (Manual Polygon/Brush), không dùng SAM

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | chưa có | 0 / 1 | 3 |
| cp2_slice | chưa có | 0 / 1 | 3 |
| cp5_occlusion | chưa có | 0 / 1 | 3 |
| cp3_thin | chưa có | 0 / 1 | 3 |
| cp4_curb | chưa có | 0 / 1 | 3 |
| cp6_coverage | chưa có | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000181542.jpg`, object ở góc trái phía trước (vùng bbox `[186.21, 132.53, 123.16, 329.47]`, ID 6).
- Class và quy tắc tôi dùng để chọn biên: Class `person`. Quy tắc chọn biên: Vẽ polygon bao bọc sát mép vai, tay và chân người; tách rời với phần xe bus đằng sau. Ở ranh giới bị che khuất bởi xe khác, dừng polygon tại mép vật cản cắt qua chứ không đoán phần bị che ngầm.
- Nếu dùng gợi ý sau đó: không dùng; vẫn giải thích một quyết định gán nhãn của mình: Hoàn toàn vẽ thủ công bằng Polygon tool, chấm các điểm nút linh hoạt để ôm đường cong viền cơ thể người.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `medium_instance`, ảnh `000000181542.jpg`, vùng đối tượng nằm ngang phía dưới giữa ảnh (`bbox [267.0, 112.0, 373.0, 132.0]`).
- Lỗi thuộc loại: gộp-tách (Crowd overlap / Is-Crowd).
- Bằng chứng tôi nhìn thấy: Hàng xe ô tô đỗ xa nhau liên tục bị dính sát đường biên pixel, nếu tách từng chiếc polygon nhỏ sẽ bị lỗi biên nhiễu và đè nhãn.
- Quy tắc và hành động sửa: Chuyển đối tượng sang RLE Mask (counts), gán thuộc tính `iscrowd: 1` cho cả dải xe đỗ xa để gộp thành 1 đối tượng duy nhất theo đúng chuẩn COCO Format.
- Sau sửa đã Save và export lại chưa?: Đã Save và export lại file ZIP thành công.
- Kết quả kiểm tra tự động: chưa có điểm.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | `medium_instance` / `000000458325.jpg` (vùng xe ô tô bị che khuất `bbox [485.3, 199.76, 154.7, 143.74]`) | Có nên tách riêng 2 xe đè lên nhau hay vẽ nối liền thành 1 xe duy nhất? | Dựa trên mép cửa kính và viền đèn xe, thấy rõ 2 khung xe riêng biệt. Quyết định: Tách thành 2 instance `car` riêng (ID 45 và ID 46) cắt tại đường biên che khuất (`occluded: false`). |
| 2 | `hard_panoptic` / `000000350023.jpg` (dải nền trời tiếp giáp hàng cây `bbox [0.0, 0.0, 638.1, 294.23]`) | Vẽ Sky chèn đè lên mép cây (rồi cho Tree đè lên Sky) hay cắt gọt Sky lề đường kẽ lá? | Áp dụng quy tắc Z-order / Layering của Panoptic Segmentation: Background vẽ phủ trước, Foreground/Vegetation phủ lên sau. Quyết định: Vẽ khối Sky hình chữ nhật/polygon lớn làm background làm nền, không tỉa từng kẽ lá. |
| 3 | `hard_panoptic` / `000000460147.jpg` (vùng dải cây bên phải `bbox [427.52, 244.85, 184.23, 161.91]`) | Gán nhãn `vegetation` (stuff) hay tách thành từng tán cây `building/tree` (thing)? | Dựa trên quy tắc Panoptic, cây tán lớn dạng nền không phân biệt được số lượng cụ thể gán là stuff. Quyết định: Vẽ chung vùng tán lá thành class `vegetation` (ID 62) liền khối. |
