# 03 — AI Log & Reflection

## Mục tiêu sử dụng AI

Tôi dùng AI như một thought-partner để mở rộng danh sách pain point, phản biện mức độ phù hợp của AI, và soạn thử cấu trúc đầu ra cho bài toán phân tích lý do hủy chuyến của Xanh SM. AI không được dùng để thay thế việc xác định workflow, metric hay operational boundary của tôi.

## AI đã hỗ trợ gì

AI giúp tôi chuyển một ý tưởng còn chung chung — “phân tích hủy chuyến” — thành scope nhỏ hơn: đọc ghi chú, tóm tắt, gán nhãn theo taxonomy cố định và đưa các case không chắc chắn cho nhân viên review. AI cũng gợi ý các metric có thể kiểm chứng như thời gian xử lý mỗi case, tỷ lệ gán nhãn đúng, và tỷ lệ case cần review lại.

## Điểm AI trả lời chưa tốt hoặc có rủi ro

Ở lần brainstorm đầu, AI đề xuất tự động điều chỉnh giá, gửi ưu đãi hoặc thay đổi thuật toán điều phối dựa trên lý do hủy chuyến. Tôi loại bỏ các đề xuất này vì chúng có tác động trực tiếp đến khách hàng, doanh thu và sự công bằng với tài xế; chúng không phù hợp với dữ liệu text ngắn và không cần thiết cho prototype đầu tiên.

AI cũng có xu hướng đưa ra các con số vận hành nghe hợp lý nhưng không có nguồn dữ liệu nội bộ. Vì vậy, các con số trong bài (ví dụ mục tiêu 90% phân loại đúng) được ghi rõ là **mục tiêu prototype**, không phải số liệu thực tế của Xanh SM. Trước khi triển khai thật, nhóm cần lấy mẫu log đã ẩn danh và đo baseline thủ công.

## Tôi đã sửa prompt và đặt ranh giới thế nào

Tôi thay yêu cầu mở “hãy đề xuất cách xử lý hủy chuyến” bằng yêu cầu có cấu trúc: chỉ chọn một nhãn trong danh sách, trích câu bằng chứng, và trả về `needs_human_review` khi thiếu thông tin hoặc không chắc chắn. AI không được tự gửi tin nhắn, thay đổi giá, khóa tài khoản hoặc điều phối cuốc xe.

Trong prototype Gemini đi kèm, tôi tiếp tục kiểm tra hai ranh giới an toàn: mọi phản hồi phải là bản nháp `[DRAFT_ONLY]`; nếu xe có pin dưới 5% thì phải yêu cầu xe sạc di động thay vì gợi ý đi tới trạm sạc xa. Các test adversarial cố tình yêu cầu mô hình bỏ qua những ranh giới này.

## Kết luận

AI hữu ích nhất khi bị giới hạn trong một bước hẹp, có đầu vào/đầu ra rõ và có người chịu trách nhiệm duyệt kết quả. Với Xanh SM, LLM nên đóng vai trò tóm tắt và phân loại dữ liệu ngôn ngữ; các hành động làm thay đổi trải nghiệm khách hàng hoặc vận hành đội xe phải do rule và con người kiểm soát.
