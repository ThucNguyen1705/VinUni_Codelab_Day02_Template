# Phase 1 & Phase 2 — Problem Scan & Quick Assess (Vin Smart Future)

**Kỹ sư thực hiện:** Kỹ sư AI Product (Vin Smart Future)  
**Đơn vị:** Vin Smart Future — Khối Công nghệ Vingroup  
**Dự án trọng tâm:** Hỗ trợ khối Vận hành Dịch vụ Sau bán hàng (After-sales) của **VinFast**  

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội tối ưu hóa bằng AI

Sử dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI có thể tốt hơn, Pain từ người khác) để quét qua toàn bộ các hoạt động vận hành của các công ty thành viên Vingroup:

| # | Subsidiary | Lens | Mô tả ngắn bài toán & Pain Point thực tế |
|---|---|---|---|
| **1** | **VinFast** | **AI có thể tốt hơn / Pain từ người khác** | **Chẩn đoán sơ bộ lỗi xe từ mô tả tiếng Việt của khách hàng:** Khách hàng mô tả bằng ngôn ngữ cảm tính đời thường (*"xe đi qua gờ giảm tốc kêu cụp cụp ở bánh trước"*, *"xe báo rùa vàng nhưng điều hòa vẫn mát"*). Cố vấn dịch vụ non trẻ mất 20–30 phút để tra cứu sổ tay kỹ thuật (Service Manual) và map sang mã lỗi chuẩn (DTC). |
| **2** | **Xanh SM** | **Tốn thời gian & Khẩn cấp** | **Điều phối cứu hộ sạc pin thực địa:** Tài xế taxi điện báo hết pin giữa đường, điều phối viên mất 15 phút vừa tra cứu vị trí GPS, vừa tìm trụ sạc trống hoặc thủ công gọi xe sạc lưu động. |
| **3** | **Vinhomes** | **Lặp lại** | **Phân loại & phân luồng phản ánh cư dân:** Hàng nghìn phản ánh mỗi ngày qua App Vinhomes Resident (hỏng đèn hành lang, rác thải, tiếng ồn) cần nhân viên đọc và chuyển thủ công về đúng ban quản lý từng tòa. |
| **4** | **Vinmec** | **Tốn thời gian** | **Soạn thảo tóm tắt hồ sơ xuất viện (Discharge Summary):** Bác sĩ mất 20–30 phút/bệnh nhân để tóm tắt các kết quả xét nghiệm, chẩn đoán lâm sàng và đơn thuốc thành ngôn ngữ dễ hiểu cho bệnh nhân ra viện. |
| **5** | **VinFast** | **Lặp lại** | **Đối chiếu hóa đơn sạc điện đối tác:** Bộ phận tài chính mất 3 ngày mỗi tuần để đối soát thủ công hàng chục nghìn phiên sạc đối tác ngoài với dữ liệu thanh toán. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn top 3 bài toán tiềm năng nhất từ danh sách trên để phân tích sơ bộ:

---

### 📇 QUICK PROBLEM CARD #1 (Lựa chọn Deep-Dive)

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                   │
│                                                                         │
│ Bài toán (1 câu): Khách hàng mô tả triệu chứng xe bằng tiếng Việt cảm   │
│ tính, cố vấn dịch vụ mất nhiều thời gian tra cứu và map sang mã lỗi DTC.│
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  [ ] Vinmec │
│                                                                         │
│ Ai đang đau (Actor)? Cố vấn dịch vụ (Service Advisor), Thợ kỹ thuật,    │
│ và Khách hàng phải chờ đợi lâu tại xưởng dịch vụ VinFast.               │
│                                                                         │
│ Workflow thủ công hiện tại (5 bước):                                    │
│   1. Khách mang xe vào xưởng, mô tả hiện tượng hỏng hóc bằng lời nói.   │
│   ──> 2. Cố vấn dịch vụ ghi chép tay tóm tắt triệu chứng.               │
│   ──> 3. Cố vấn tra cứu thủ công Service Manual / hỏi kỹ thuật viên già. │
│   ──> 4. Kỹ thuật viên lái thử hoặc cắm máy scan OBD2 đọc mã lỗi.       │
│   ──> 5. Lập phiếu báo giá & lệnh sửa chữa (Work Order).                │
│                                                                         │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 20-30 phút/lượt)        │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3                         │
│ (Trích xuất thực thể triệu chứng -> Gợi ý mã lỗi DTC & checklist kiểm tra)│
│                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                   │
│   Giảm thời gian chẩn đoán tiếp nhận ban đầu từ 25 phút ──> dưới 5 phút.│
│   Độ chính xác gợi ý đúng nhóm bộ phận hư hỏng đạt > 85%.               │
│                                                                         │
│ Quick Architecture: [x] LLM Feature (Copilot hỗ trợ cố vấn dịch vụ)     │
└─────────────────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #2

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                   │
│                                                                         │
│ Bài toán (1 câu): Tài xế Xanh SM báo xe sắp cạn pin thực địa cần chỉ dẫn│
│ trạm sạc gần nhất hoặc điều xe cứu hộ sạc pin di động khẩn cấp.         │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  [ ] Vinmec │
│                                                                         │
│ Ai đang đau (Actor)? Tài xế Xanh SM (lo lắng chết máy giữa đường) và    │
│ Điều phối viên trung tâm (Dispatchers) bị quá tải cuộc gọi khẩn cấp.   │
│                                                                         │
│ Workflow thủ công hiện tại (4 bước):                                    │
│   1. Nhận cuộc gọi khẩn từ tài xế báo % pin và vị trí.                 │
│   ──> 2. Tra cứu tọa độ xe và tìm trụ sạc VinFast còn trống trong bán kính.│
│   ──> 3. Soạn tin nhắn hướng dẫn đường đi hoặc liên hệ xe cứu hộ sạc pin│
│   ──> 4. Gửi thông báo đến App tài xế.                                  │
│                                                                         │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 12-15 phút/cuộc gọi)    │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3                         │
│ (Tự động hóa phân tích vị trí -> Kiểm tra pin -> Draft lệnh điều vận)   │
│                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                   │
│   Rút ngắn thời gian xử lý sự cố từ 15 phút ──> dưới 3 phút.            │
│                                                                         │
│ Quick Architecture: [x] LLM Feature (với Boundary kiểm soát pin < 5%)   │
└─────────────────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #3

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                   │
│                                                                         │
│ Bài toán (1 câu): Phản ánh của cư dân Vinhomes gửi qua App không được   │
│ phân loại tự động, gây chậm trễ xử lý sự cố tại các tòa nhà.            │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  [ ] Vinmec │
│                                                                         │
│ Ai đang đau (Actor)? Cư dân Vinhomes (chờ xử lý lâu) và Nhân viên CSKH  │
│ trực quầy Ban Quản Lý (ngập trong hàng nghìn ticket/ngày).              │
│                                                                         │
│ Workflow thủ công hiện tại (4 bước):                                    │
│   1. Cư dân gửi nội dung phản ánh qua App kèm ảnh chụp.                 │
│   ──> 2. Nhân viên CSKH đọc nội dung và phân loại loại sự cố (Điện/Nước)│
│   ──> 3. Forward ticket đến đội kỹ thuật của tòa nhà tương ứng.         │
│   ──> 4. Phản hồi tin nhắn xác nhận tiếp nhận đến cư dân.               │
│                                                                         │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ trung bình trễ 4-6 tiếng)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 4                         │
│ (Phân loại văn bản tự động -> Auto-route ticket -> Draft phản hồi)      │
│                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                   │
│   90% ticket được phân luồng tự động trong vòng dưới 30 giây.           │
│                                                                         │
│ Quick Architecture: [x] Rule + LLM Classifier                           │
└─────────────────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Đánh giá và Lựa chọn Bài toán Deep-Dive

Nhóm thống nhất chọn **Quick Problem Card #1: VinFast — Trợ lý AI Chẩn đoán Sơ bộ Lỗi xe từ Mô tả Tiếng Việt** để tiến hành Deep-Dive vì:
1. **Giá trị kinh doanh lớn:** VinFast đang mở rộng thần tốc với hàng trăm xưởng dịch vụ trên toàn quốc. Đội ngũ cố vấn dịch vụ mới tuyển dụng thiếu kinh nghiệm nhận diện bệnh xe, việc có AI Copilot sẽ nâng cao ngay lập tức chỉ số hài lòng khách hàng (CSAT) sau bán hàng.
2. **AI-Fit rõ ràng:** Khách hàng mô tả lỗi bằng ngôn ngữ tự nhiên không có cấu trúc, rất phong phú đa dạng (từ tượng thanh, phương ngữ Bắc - Trung - Nam). Đây là thế mạnh tuyệt đối của Large Language Models (LLM) mà các hệ thống mã lỗi Rule-based truyền thống không xử lý được.
3. **Ranh giới an toàn kiểm soát được:** AI chỉ đóng vai trò Trợ lý đề xuất (Copilot/Draft), kỹ thuật viên xưởng luôn là người kiểm tra vật lý và chốt phương án cuối cùng (Human-in-the-loop).
