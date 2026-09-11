# 01 — Problem Scan & Quick Problem Cards

## Phase 1 — SCAN

| # | Công ty thành viên | Lens | Vấn đề vận hành |
|---|---|---|---|
| 1 | Xanh SM | Tốn thời gian | Nhân viên vận hành phải đọc thủ công ghi chú tài xế và lịch sử hỗ trợ để xác định lý do khách hủy chuyến. |
| 2 | Vinhomes | Lặp lại | CSKH đọc và phân loại phản ánh cư dân (mất nước, thang máy, tiếng ồn, vệ sinh) trước khi chuyển đúng đội xử lý. |
| 3 | Vinpearl | Pain từ stakeholder | Quản lý ca khó phát hiện kịp thời các review nghiêm trọng như phòng bẩn, mất đồ hoặc sự cố dịch vụ. |
| 4 | VinFast | AI-upgrade | Khách mô tả triệu chứng xe bằng tiếng Việt tự do nhưng ticket thường được chuyển sai nhóm kỹ thuật. |
| 5 | VinUni | Lặp lại | Sinh viên nhận lỗi từ autograder nhưng vẫn phải hỏi lại trợ giảng để hiểu nguyên nhân và cách sửa. |

## Phase 2 — QUICK-ASSESS

### Quick Problem Card #1 — Xanh SM: Cancellation Intelligence Copilot

| Hạng mục | Nội dung |
|---|---|
| Bài toán | Đọc ghi chú tự do về các chuyến bị hủy, trích bằng chứng, phân loại nguyên nhân, phát hiện pattern và soạn insight nội bộ cho đội vận hành. |
| Công ty | Xanh SM (GSM) |
| Actor | Chuyên viên vận hành chất lượng dịch vụ và quản lý ca. |
| Workflow hiện tại | 1) Xuất log hủy chuyến cuối ngày → 2) Đọc ghi chú rời rạc từ tài xế/CSKH → 3) Tự diễn giải và gán nhãn → 4) Tổng hợp Excel theo khu vực/giờ → 5) Viết báo cáo thủ công cho quản lý. |
| Bottleneck | Ghi chú tiếng Việt tự do, viết tắt và thiếu ngữ cảnh khiến việc diễn giải, tìm bằng chứng và nhận ra pattern mất khoảng 3 phút/case. |
| AI hỗ trợ | LLM tóm tắt từng case, gán nhãn, trích câu bằng chứng, nêu độ tin cậy; trên tập case đã ẩn danh, LLM tạo nháp insight về pattern theo thời gian/khu vực. Nhân viên duyệt case không chắc chắn và mọi insight trước khi sử dụng. |
| Metric | Ít nhất 90% case được gán nhãn đúng; giảm thời gian phân tích từ 3 phút xuống dưới 20 giây/case; bản báo cáo ngày có ít nhất 3 insight kèm bằng chứng và được quản lý duyệt. |
| Quick architecture | LLM Feature + rule kiểm tra taxonomy và ngưỡng chuyển human review; không dùng agent tự trị. |

### Quick Problem Card #2 — Vinhomes: Điều hướng phản ánh cư dân

| Hạng mục | Nội dung |
|---|---|
| Bài toán | Phân loại và tạo nháp ticket cho phản ánh của cư dân để chuyển đúng đội xử lý. |
| Công ty | Vinhomes |
| Actor | Nhân viên CSKH và ban quản lý tòa nhà. |
| Workflow hiện tại | 1) Nhận phản ánh từ app → 2) Đọc nội dung/ảnh → 3) Xác định tòa và loại sự cố → 4) Tạo ticket → 5) Chuyển kỹ thuật hoặc an ninh. |
| Bottleneck | Phản ánh viết tự do, thiếu thông tin và dễ phân loại sai; khoảng 8 phút/ticket. |
| AI hỗ trợ | Tóm tắt nội dung, nhận diện tòa nhà/loại việc/mức độ khẩn và soạn ticket nháp. |
| Metric | 85% ticket được route đúng từ lần đầu; giảm thời gian tạo ticket từ 8 phút xuống dưới 1 phút. |
| Quick architecture | LLM Feature; rule ưu tiên cho từ khóa nguy hiểm như cháy, rò điện, kẹt thang máy. |

### Quick Problem Card #3 — Vinpearl: Cảnh báo review dịch vụ khẩn cấp

| Hạng mục | Nội dung |
|---|---|
| Bài toán | Đọc review mới và gắn cờ các phản ánh có khả năng cần quản lý ca can thiệp ngay. |
| Công ty | Vinpearl / VinWonders |
| Actor | Quản lý trải nghiệm khách hàng và quản lý ca. |
| Workflow hiện tại | 1) Nhân viên mở từng kênh review → 2) Đọc nội dung → 3) Chép case đáng chú ý → 4) Nhắn quản lý → 5) Theo dõi phản hồi. |
| Bottleneck | Dễ bỏ sót review dài, đa ngôn ngữ hoặc đăng ngoài giờ; khoảng 5 phút/review. |
| AI hỗ trợ | Tóm tắt review, nhận diện chủ đề và mức độ nghiêm trọng, tạo danh sách case cần review. |
| Metric | Phát hiện 95% review nghiêm trọng trong vòng 5 phút; giảm thời gian đọc/sàng lọc 60%. |
| Quick architecture | LLM Feature; không tự phản hồi công khai hoặc hứa bồi thường. |

## Lựa chọn đề xuất

Tôi đề xuất nhóm chọn **Xanh SM — Cancellation Intelligence Copilot**. Đây là tác vụ phân tích nội bộ, không ra quyết định thời gian thực cho tài xế hoặc khách hàng. LLM phù hợp vì đầu vào là ghi chú tự do, không đồng nhất; mô hình cần diễn giải ngữ cảnh, trích bằng chứng và tổng hợp pattern, thay vì chỉ khớp từ khóa. Đầu ra vẫn được giới hạn bằng taxonomy nhãn, ngưỡng tin cậy và human review, nên scope có baseline rõ ràng và rủi ro vận hành thấp để bắt đầu prototype.
