# 01 — Problem Scan & Quick Cards (Vin Smart Future)

> **Lưu ý về số liệu:** Mọi con số trong file này là **ước tính giả định** của tôi (không phải dữ liệu nội bộ Vingroup). Mỗi con số đều ghi kèm công thức `số lượt × thời gian` để có thể kiểm chứng và điều chỉnh khi có baseline thật.

---

# 🔍 Phase 1 — SCAN

Dùng 4 lenses: **Lặp lại · Tốn thời gian · AI có thể tốt hơn · Pain từ người khác**.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Vinpearl** | Tốn thời gian | Nhân viên Reservation đọc, dịch và phân loại thủ công các ghi chú "yêu cầu đặc biệt" (dị ứng, nôi em bé, đón sân bay, trang trí kỷ niệm...) viết tự do bằng nhiều ngôn ngữ trong booking từ OTA (Booking.com, Agoda, Trip.com...), rồi chuyển cho từng bộ phận. *Ước tính: ~130 yêu cầu/ngày/resort × 10 phút = ~22 giờ công/ngày; ~4% yêu cầu bị bỏ sót.* |
| 2 | **Xanh SM** | Lặp lại | Tổng đài hỗ trợ tài xế trả lời đi trả lời lại các câu hỏi về chính sách thu nhập, thưởng theo tuần, phí phạt — chính sách thay đổi thường xuyên nên tổng đài viên phải tra văn bản. *Ước tính: 2.000 cuộc/ngày × 5 phút = ~167 giờ công/ngày; ~60% là câu hỏi lặp lại.* |
| 3 | **Xanh SM** | Pain từ người khác | Đội Chất lượng dịch vụ xem xét thủ công đánh giá ≤2 sao (đọc bình luận, nghe ghi âm, xem GPS) để quyết định xử lý tài xế; tồn đọng lâu, tài xế phàn nàn bị xử lý oan. *Ước tính: 600 ca/ngày × 12 phút = 120 giờ công/ngày; tồn đọng 5–7 ngày.* |
| 4 | **VinFast** | AI có thể tốt hơn | Hotline trạm sạc công cộng: khách báo "trụ không nhận sạc", tổng đài viên hỏi theo kịch bản cứng, tra mã lỗi thủ công rồi mới hướng dẫn hoặc điều kỹ thuật. *Ước tính: 800 cuộc/ngày × 8 phút = ~107 giờ công/ngày; khoảng một nửa là lỗi khách tự khắc phục được.* |
| 5 | **Vinmec** | Tốn thời gian | Điều phối viên khách quốc tế dịch và tóm tắt hồ sơ bệnh sử gửi từ nước ngoài (Anh/Hàn/Nhật) trước khi bác sĩ tiếp nhận. *Ước tính: 40 hồ sơ/ngày × 45 phút = 30 giờ công/ngày; bác sĩ nhận hồ sơ trễ 1–2 ngày.* |
| 6 | **VinWonders** | Pain từ người khác | Tìm trẻ lạc: phụ huynh mô tả tại quầy thông tin, nhân viên truyền bộ đàm từng khu. *Ước tính: ~15 ca/ngày cao điểm × 25 phút tìm.* → Ghi nhận nhưng **không phù hợp với LLM**: nên giải quyết bằng quy trình + vòng tay QR cho trẻ (No AI). |

---

# 🃏 Phase 2 — QUICK-ASSESS

Chọn top 3: **#1 (Vinpearl yêu cầu đặc biệt)**, **#3 (Xanh SM xét đánh giá xấu)**, **#4 (VinFast hotline trạm sạc)**.

## Quick Problem Card #1 — Vinpearl: Yêu cầu đặc biệt đa ngôn ngữ trong booking OTA

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Ghi chú yêu cầu đặc biệt viết tự do, đa ngôn ngữ trong booking OTA bị xử lý chậm và thỉnh thoảng bị bỏ sót, khiến khách không được đáp ứng khi đến resort. |
| **Công ty thành viên** | [x] Khác: **Vinpearl** |
| **Ai đang đau (Actor)?** | Nhân viên Reservation (quá tải mùa cao điểm); khách (yêu cầu bị bỏ sót, nghiêm trọng nhất là dị ứng); F&B / Housekeeping (nhận thông tin thiếu hoặc muộn). |
| **Workflow thủ công hiện tại** | 1. Lọc booking có ghi chú → 2. Đọc & dịch ghi chú → 3. Phân loại, xác định bộ phận & có tính phí không → 4. Nhập trace vào PMS & báo bộ phận → 5. Phản hồi/xác nhận với khách |
| **Bước tốn thời gian/lỗi nhất** | Bước 2–3 (⏱ 5 / 10 phút mỗi lượt) — dịch sai, sót khi 1 ghi chú có nhiều yêu cầu. |
| **AI hỗ trợ ở bước nào?** | Bước 2–3: dịch + tách từng yêu cầu + phân loại bộ phận + gắn mức ưu tiên; soạn nháp trace (bước 4) và tin phản hồi khách (bước 5). |
| **Metric thành công** | Thời gian xử lý từ **10 phút → ≤2 phút/lượt**; **100%** ghi chú có dị ứng/y tế được gắn cờ ưu tiên cao; phân loại đúng bộ phận **≥90%**. |
| **Quick Architecture** | [ ] No AI [ ] Rule [x] **LLM** [ ] Agent |

**Stress-test (đóng vai CFO + Trưởng phòng Vận hành khắt khe):**
- *"Rule-based bắt từ khóa là đủ, cần gì AI?"* → Không đủ: ghi chú đa ngôn ngữ (EN/KO/ZH/RU), viết tắt (`bday`, `HM`), phủ định (`no need for baby cot`). Tuy vậy, **rule từ khóa dị ứng vẫn được giữ làm lưới an toàn** song song với LLM.
- *"Tiết kiệm 22 giờ công/ngày có đáng không?"* → Giá trị chính nằm ở trải nghiệm khách và rủi ro sức khỏe (dị ứng), không chỉ ở giờ công.
- *"Metric 100% là phi thực tế với LLM."* → Đúng, 100% không đến từ riêng LLM mà từ tổ hợp LLM + rule từ khóa + nhân viên duyệt.

## Quick Problem Card #2 — Xanh SM: Xét đánh giá ≤2 sao để xử lý tài xế

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Đội Chất lượng mất nhiều thời gian gom chứng cứ cho mỗi đánh giá xấu nên tồn đọng lâu và quyết định xử lý tài xế thiếu nhất quán. |
| **Công ty thành viên** | [x] **Xanh SM** |
| **Ai đang đau (Actor)?** | Chuyên viên Chất lượng dịch vụ; tài xế (chờ lâu, bị xử lý oan); khách (không được phản hồi kịp). |
| **Workflow thủ công hiện tại** | 1. Nhận đánh giá ≤2 sao → 2. Đọc bình luận + nghe ghi âm cuộc gọi → 3. Xem lại GPS/lịch sử chuyến → 4. Đối chiếu quy chế, chọn mức xử lý → 5. Thông báo tài xế & phản hồi khách |
| **Bước tốn thời gian/lỗi nhất** | Bước 2–4 (⏱ 9 / 12 phút mỗi lượt). |
| **AI hỗ trợ ở bước nào?** | Tóm tắt bình luận + transcript ghi âm, gợi ý điều khoản quy chế liên quan. **Không** được đề xuất hay quyết định mức phạt. |
| **Metric thành công** | Tồn đọng từ **5–7 ngày → <24 giờ**; thời gian xét từ **12 → 4 phút/ca**; tỉ lệ tài xế khiếu nại thành công giảm từ ~15% xuống **<8%**. |
| **Quick Architecture** | [ ] No AI [ ] Rule [x] **LLM** (kèm speech-to-text) [ ] Agent |

**Stress-test:**
- Quyết định ảnh hưởng trực tiếp thu nhập tài xế → rủi ro công bằng và thiên kiến, bắt buộc con người quyết định.
- Speech-to-text tiếng Việt nhiều giọng vùng miền có thể sai → phải đo tỉ lệ lỗi trước khi tin vào bản tóm tắt.
- Nhiều đánh giá 1 sao do lỗi app/giá cước chứ không do tài xế → cần bước phân loại nguyên nhân trước.

## Quick Problem Card #3 — VinFast: Hotline báo lỗi trụ sạc công cộng

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Khách báo "trụ không nhận sạc" phải chờ tổng đài viên tra mã lỗi thủ công, nhiều ca đơn giản vẫn bị điều kỹ thuật ra hiện trường. |
| **Công ty thành viên** | [x] **VinFast** |
| **Ai đang đau (Actor)?** | Tổng đài viên; chủ xe đang chờ ở trạm; kỹ thuật viên hiện trường bị điều đi cho lỗi tự khắc phục được. |
| **Workflow thủ công hiện tại** | 1. Nhận cuộc gọi, hỏi mã trụ & dòng xe → 2. Tra trạng thái trụ trên dashboard → 3. Tra mã lỗi trong tài liệu kỹ thuật → 4. Hướng dẫn khách thao tác hoặc khởi động lại trụ từ xa → 5. Không được thì tạo phiếu điều kỹ thuật |
| **Bước tốn thời gian/lỗi nhất** | Bước 2–3 (⏱ 5 / 8 phút mỗi lượt). |
| **AI hỗ trợ ở bước nào?** | Chủ yếu là tra bảng: mã lỗi trụ → hướng dẫn xử lý. |
| **Metric thành công** | Thời gian xử lý từ **8 → 3 phút/cuộc**; giảm **30%** phiếu điều kỹ thuật cho lỗi tự khắc phục được. |
| **Quick Architecture** | [ ] No AI [x] **Rule** [ ] LLM [ ] Agent |

**Stress-test:** Mã lỗi trụ sạc là dữ liệu có cấu trúc → một **cây quyết định rule-based** tự động hiển thị hướng dẫn theo mã lỗi đã giải quyết được phần lớn bài toán, rẻ và dễ kiểm chứng hơn LLM. Chỉ nên cân nhắc LLM nếu đo được phần lớn cuộc gọi không có mã lỗi.

---

# 🗳️ Đề xuất bài toán cho Deep-Dive

**Chọn Card #1 — Vinpearl: Yêu cầu đặc biệt đa ngôn ngữ trong booking OTA.**

- **Vì sao chọn:** bottleneck nằm đúng ở phần xử lý ngôn ngữ tự nhiên đa ngôn ngữ (thế mạnh thật sự của LLM), luồng xử lý cố định, rủi ro kiểm soát được bằng nhân viên duyệt.
- **Loại Card #2:** quyết định ảnh hưởng thu nhập tài xế, phụ thuộc chất lượng speech-to-text chưa được đo → rủi ro công bằng cao, cần thêm dữ liệu.
- **Loại Card #3:** rule-based giải quyết tốt hơn → không cần AI (Problem First, AI Second).
