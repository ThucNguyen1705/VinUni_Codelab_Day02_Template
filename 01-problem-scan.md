# 01 - Problem Scan & Quick Problem Cards (Vin Smart Future)

* **Tên nhóm:** Vin Smart Innovators (Nhóm 02)
* **Họ và tên thành viên:** Nguyễn Văn Quân
* **Mã SV / Email:** quan02495@vinuni.edu.vn
* **Nhánh cá nhân (Branch):** `quan02495`
* **Vai trò:** AI Product Engineer — Vin Smart Future

---

## 🔍 Phase 1 — SCAN: Bảng Quét Cơ Hội Vận Hành (4 Lenses)

Dưới góc nhìn của kỹ sư AI tại Vin Smart Future, tôi đã rà soát các quy trình vận hành thực địa xuyên suốt các công ty thành viên Vingroup và xác định 5 bài toán/điểm nghẽn tiềm năng sau:

| # | Công ty thành viên | Lens áp dụng | Mô tả ngắn bài toán & Điểm nghẽn vận hành |
|---|--------------------|--------------|--------------------------------------------|
| 1 | **Vinhomes** | Lặp lại (Repetitive) | Phân loại tự động và điều phối yêu cầu/sự cố kỹ thuật của cư dân qua App Vinhomes Resident đến đúng tổ kỹ thuật (Cơ điện, Xây dựng, Cây xanh). |
| 2 | **VinFast** | AI-upgrade (AI có thể tốt hơn) | Trợ lý tiền chẩn đoán lỗi xe và dự đoán mã lỗi kỹ thuật OBD-II từ mô tả ngôn ngữ tự nhiên tiếng Việt của chủ xe điện (VF5, VF8, VF9). |
| 3 | **Vinmec** | Tốn thời gian (Time-consuming) | Trích xuất dữ liệu lâm sàng từ bệnh án điện tử (EMR) để soạn thảo bản tóm tắt hồ sơ xuất viện (Discharge Summary) và hướng dẫn dặn dò cho bệnh nhân. |
| 4 | **Vinpearl / VinWonders** | Tốn thời gian (Time-consuming) | Bóc tách yêu cầu đặt phòng đoàn MICE (Group Booking RFP) từ email đại lý du lịch lữ hành, đối chiếu chính sách giá B2B để soạn báo giá tự động. |
| 5 | **Xanh SM (GSM)** | Pain từ người khác (Stakeholder Pain) | Phân tích tự động nguyên nhân hủy chuyến của khách hàng từ ghi chú tài xế và ghi âm cuộc gọi để tìm ra các "điểm mù" hạ tầng và điều vận. |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Tôi lựa chọn **Top 3 bài toán khả thi nhất** từ danh sách trên để phân tích sâu qua Thẻ Đánh Giá Nhanh:

---

### 📌 QUICK PROBLEM CARD #1: Vinhomes — Điều phối phản ánh cư dân thông minh

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Tự động phân loại nội dung khiếu nại,     │
│ đánh giá mức độ khẩn cấp (P1-P4) và điều phối yêu cầu       │
│ kỹ thuật của cư dân đến đúng tổ bảo trì tòa nhà.            │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau (Actor)? Lễ tân / Điều phối viên BQL Tòa nhà    │
│ (quá tải gõ vé, dễ nhầm lẫn) và Cư dân (chờ đợi lâu).       │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Cư dân gửi phản ánh tự do qua App Vinhomes Resident    │
│   → 2. Lễ tân đọc từng tin nhắn, phân tích nội dung         │
│   → 3. Đăng nhập hệ thống ERP, chọn tổ kỹ thuật phụ trách   │
│   → 4. Bấm gán vé thủ công và gọi bộ đàm báo đội bảo trì    │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 8-10 min/vé) │
│ (Thường xuyên gán nhầm giữa tổ Cơ điện và tổ Xây dựng)      │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3:           │
│ LLM đọc ngôn ngữ tự nhiên -> Trích xuất loại sự cố, vị trí, │
│ mức độ khẩn cấp -> Tự động route và draft thông báo kỹ thuật│
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ 1. Giảm thời gian điều phối vé từ 10 phút xuống < 30 giây.  │
│ 2. Tỉ lệ gán chính xác tổ kỹ thuật đạt >= 95%.              │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

---

### 📌 QUICK PROBLEM CARD #2: VinFast — Tiền chẩn đoán lỗi kỹ thuật xe điện

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Hỗ trợ Cố vấn Dịch vụ phân tích mô tả     │
│ tiếng Việt của chủ xe để dự đoán cụm mã lỗi kỹ thuật OBD-II │
│ và chuẩn bị trước phụ tùng thay thế tại xưởng dịch vụ.      │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau (Actor)? Cố vấn Dịch vụ xưởng (Service Advisor) │
│ và Khách hàng sử dụng xe điện VinFast.                      │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách hàng gọi hotline/nhắn tin mô tả hiện tượng lạ    │
│   → 2. Cố vấn hỏi đi hỏi lại nhiều câu để xác minh triệu    │
│        chứng, dòng xe, phiên bản phần mềm FOTA              │
│   → 3. Cố vấn mở cẩm nang tra cứu mã lỗi nghi vấn           │
│   → 4. Viết phiếu tiếp nhận xe và tra cứu tồn kho phụ tùng  │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 15-20 min)   │
│ (Mô tả mơ hồ dẫn đến đoán sai phụ tùng cần chuẩn bị)        │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3:           │
│ LLM phân tích văn phong tiếng Việt đời thường -> RAG tra    │
│ cẩm nang VinFast Service Manual -> Dự đoán Top 3 mã lỗi     │
│ nghi vấn và danh mục linh kiện cần kiểm tra sẵn.            │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ 1. Giảm thời gian tư vấn đặt hẹn từ 15 phút xuống < 3 phút. │
│ 2. Tỉ lệ linh kiện sẵn sàng trong kho khi xe tới đạt >= 85%.│
│                                                             │
│ Quick Architecture: [x] LLM Feature (RAG Tra cứu kỹ thuật)  │
└─────────────────────────────────────────────────────────────┘
```

---

### 📌 QUICK PROBLEM CARD #3: Vinmec — Soạn thảo nháp tóm tắt hồ sơ xuất viện

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Tự động trích xuất thông tin lâm sàng từ  │
│ bệnh án điện tử để soạn bản nháp "Tóm tắt xuất viện" và     │
│ hướng dẫn dặn dò dùng thuốc dễ hiểu cho bệnh nhân.          │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau (Actor)? Bác sĩ điều trị / Bác sĩ nội trú       │
│ (quá tải thời gian hành chính) và Bệnh nhân/Người nhà.      │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Bệnh nhân có quyết định xuất viện                      │
│   → 2. Bác sĩ mở EMR, đọc lại toàn bộ lịch sử xét nghiệm,   │
│        kết quả chẩn đoán hình ảnh và các y lệnh điều trị    │
│   → 3. Gõ tay bản tóm tắt quá trình điều trị theo mẫu Bộ Y Tế│
│   → 4. Soạn lời dặn dò uống thuốc và chế độ ăn tại nhà      │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 25-35 min/bn) │
│ (Dễ sai sót chỉ số hoặc sót cảnh báo tương tác thuốc)       │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3:           │
│ LLM đọc có cấu trúc dữ liệu EMR -> Tóm tắt bệnh sử lâm sàng │
│ -> Soạn nháp đơn dặn dò có gắn cờ cảnh báo tương tác thuốc. │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ 1. Giảm thời gian làm hồ sơ từ 30 phút xuống < 5 phút       │
│    (Bác sĩ chỉ cần review và ký duyệt điện tử).             │
│ 2. 100% hồ sơ xuất viện kiểm tra tự động tương tác thuốc.   │
│                                                             │
│ Quick Architecture: [x] LLM Feature (Strict Summarization)  │
└─────────────────────────────────────────────────────────────┘
```
