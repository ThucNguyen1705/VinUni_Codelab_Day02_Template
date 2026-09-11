# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

> **Học viên thực hiện:** Nguyễn Đức Minh  
> **Mã số sinh viên (MSSV):** 2A202602891  
> **Vị trí:** AI Product Engineer — Vin Smart Future (Vingroup)  
> **Đề tài lựa chọn:** **Hệ thống Đề xuất Trạm sạc & Lộ trình Tối ưu từ A đến B Nhanh nhất cho Xe điện VinFast**

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

---

# 🔍 Phase 1 — SCAN (Cá nhân)

Sử dụng **4 Lenses** rà soát hoạt động vận hành của các công ty thành viên Vingroup để ghi nhận 5 bài toán thực tế:

### 📝 List bài toán của tôi:
| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **VinFast** | **AI có thể tốt hơn** | **Định tuyến & Đề xuất trạm sạc từ A đến B nhanh nhất:** Tự động tính toán điểm dừng sạc tối ưu dọc đường để tổng thời gian hành trình (lái xe + sạc) là ngắn nhất mà không phải đi đường vòng. |
| 2 | **VinFast** | **Lặp lại** | **So khớp hóa đơn và dữ liệu sạc điện đối tác:** Tự động so khớp dữ liệu hàng trăm nghìn phiên sạc ngoài của VinFast với hóa đơn EVN và sao kê ngân hàng. |
| 3 | **Xanh SM** | **Tốn thời gian** | **Điều phối và gán lộ trình cuốc xe đa phương thức:** Tự động điều chỉnh cuốc xe khi hành khách đổi điểm đến giữa chừng hoặc gặp ùn tắc giờ cao điểm. |
| 4 | **Vinhomes** | **Lặp lại** | **Tiếp nhận và phân luồng phản ánh kỹ thuật cư dân:** Tự động phân loại nội dung phản ánh qua App Vinhomes Resident về đúng tổ kỹ thuật từng tòa nhà. |
| 5 | **Vinmec** | **Pain từ người khác** | **Tóm tắt hồ sơ bệnh án xuất viện:** Tự động trích xuất thông tin bệnh án để soạn thảo tóm tắt xuất viện dễ hiểu cho bệnh nhân, giảm tải việc bàn giấy cho bác sĩ. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân)

```text
┌─────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1 (ĐỀ TÀI ĐƯỢC CHỌN)                                        │
│                                                                                 │
│ Bài toán (1 câu): Chủ xe VinFast (VF5, VF8, VF9) cần hệ thống tự động đề xuất     │
│ trạm sạc bám sát đường đi và lộ trình từ A đến B có tổng thời gian NGẮN NHẤT.    │
│                                                                                 │
│ Công ty thành viên: [x] VinFast   [ ] Xanh SM   [ ] Vinhomes                    │
│                     [ ] Vinmec    [ ] Khác ___________________                  │
│                                                                                 │
│ Ai đang đau (Actor)? Chủ xe VinFast lái xe đường dài, Tài xế dịch vụ Xanh SM    │
│                                                                                 │
│ Workflow thủ công hiện tại (5 bước):                                            │
│   1. Nhập điểm đến B trên Google Maps xem khoảng cách và lộ trình               │
│   ──> 2. Nhìn mức pin % SoC táp-lô nhẩm tính thấy không đủ pin chạy thẳng đến B  │
│   ──> 3. Tự mở thêm App VinFast dò tìm các trạm sạc nằm gần tuyến đường A ──> B │
│   ──> 4. Bấm vào từng trạm kiểm tra xem có trụ DC sạc nhanh và còn chỗ không    │
│   ──> 5. Lái xe theo phán đoán cá nhân -> Nguy cơ trạm kín chỗ hoặc đi đường vòng│
│                                                                                 │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 13 - 15 phút mò mẫm thủ công)     │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3 & 4                             │
│ (AI tự động trích xuất SoC, vị trí GPS A và B, dòng xe -> Tính trạm sạc bám     │
│  sát tuyến đường có công suất cao nhất và còn trụ trống -> Soạn lộ trình nháp)  │
│                                                                                 │
│ Đo thành công bằng gì (Metric có số)?                                           │
│   - Giảm thời gian tìm và lên kế hoạch trạm sạc từ 15 phút ──> dưới 2 giây.      │
│   - Giảm ít nhất 35% tổng thời gian chờ sạc và đi đường vòng cho chuyến đi.     │
│   - 100% trạm đề xuất khớp chuẩn cổng sạc (CCS2/GBT) và có trụ sạc trống.       │
│                                                                                 │
│ Quick Architecture: [x] LLM Feature kết hợp Deterministic Route Solver (EVRP)   │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm / Cá nhân Scoping)

## 3.1. Current-State Workflow Mapping
* 🔴 **Bottleneck 1:** Tra cứu thủ công trạm sạc dọc tuyến đường A ──> B trên bản đồ (7 phút).
* 🔴 **Bottleneck 2:** Lọc cổng sạc công suất cao (150kW-250kW) và kiểm tra trụ trống (6 phút).
* 🔄 **Handoff:** Chuyển đổi thủ công giữa Google Maps và App VinFast.
* ⏱ **Tổng thời gian tra cứu:** 16 – 18 phút; nguy cơ chuyến đi bị kéo dài thêm 30 – 60 phút do chọn sai trạm.

## 3.2. Problem Statement (6-field) — Chuẩn Vin Smart Future

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Chủ xe điện VinFast (VF5, VF8, VF9) cần đi từ điểm A đến điểm B nhanh nhất; Trợ lý Điều hướng VinFast trên xe. |
| **2. Current Workflow** | Tài xế dùng Google Maps xem đường, tự mở App VinFast dò tìm trạm sạc, tự nhẩm tính pin và chọn trạm theo cảm tính. Quy trình thủ công mất 16–18 phút. |
| **3. Bottleneck** | Google Maps không biết pin xe; tài xế không biết ghé trạm nào thì tổng thời gian lái xe + thời gian sạc là ngắn nhất, dễ bị đi đường vòng xa. |
| **4. Business Impact** | Hơn 65% tài xế bị mất thêm 30–60 phút cho mỗi chuyến đi dài; làm gia tăng tâm lý lo lắng cạn pin (Range Anxiety). |
| **5. Success Metric** | 1. Giảm 35% tổng thời gian chờ sạc và đi đường vòng.<br>2. Thời gian phản hồi tính toán lộ trình dưới 2 giây.<br>3. 100% trạm đề xuất đúng chuẩn cổng xe và còn trụ trống. |
| **6. Operational Boundary** | 1. Mọi đề xuất phải có thẻ `[DRAFT_ONLY]` để tài xế bấm xác nhận (HITL).<br>2. Khi pin < 5%, cấm dẫn đi trạm sạc > 5km, bắt buộc trả về lệnh cứu hộ: `{"action": "dispatch_mobile_charger"}`.<br>3. Luôn duy trì mức pin đệm dự phòng $\ge 10\%$. |

## 3.3. Future-State Flow & AI Fit
* **AI Fit:** **LLM Feature + Deterministic Routing Engine** (Giải thuật toán học tính chính xác thời gian và lượng pin; LLM đóng vai trò Co-pilot giao tiếp tự nhiên).
* **Quy trình tương lai:** Tài xế nhập điểm B $\to$ Hệ thống tính trạm sạc bám sát đường đi có công suất lớn nhất còn trụ trống $\to$ AI Co-pilot soạn lộ trình `[DRAFT_ONLY]` $\to$ Tài xế bấm "Bắt đầu" $\to$ Điều hướng A ──> Trạm sạc $S^*$ ──> B nhanh nhất.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE

Đã triển khai và vượt qua toàn bộ các bài kiểm thử tự động tại [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng mô hình **Google Gemini Flash**:
* Thực thi 100% các ranh giới an toàn: `[DRAFT_ONLY]` và `dispatch_mobile_charger` khi pin < 5%.
* Vượt qua toàn bộ các Adversarial Test Cases (Tấn công prompt).

---

# 🏁 Phase 5 — EVALUATE

### AI Readiness Checklist:
1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test (Dữ liệu telemetry xe qua eSIM và API trạm sạc OCPP).
2. [x] Rủi ro khi AI sai nằm trong tầm kiểm soát (qua cơ chế duyệt HITL và Fallback offline).
3. [x] Stakeholders sẵn sàng nâng cấp tính năng thông qua bản cập nhật phần mềm OTA trên xe.

### Quyết định cuối cùng:
# 🟢 QUYẾT ĐỊNH: GO (BẮT ĐẦU XÂY DỰNG MVP)

**Justification (Lý giải quyết định):**
1. Giải quyết triệt để bài toán sống còn lớn nhất của chủ xe điện: Đi từ A đến B nhanh nhất, không còn nỗi lo cạn pin hay chờ sạc.
2. Khả thi kỹ thuật cao: Tích hợp trực tiếp lên phần mềm xe VinFast qua OTA, không phát sinh chi phí phần cứng.
3. Tạo lợi thế cạnh tranh vượt trội cho thương hiệu xe điện VinFast.

---

# 📝 Phase 6 — REFLECTION

*Xem chi tiết nhật ký phản ánh quá trình làm việc cùng AI làm Thought-Partner tại file [03-ai-log.md](03-ai-log.md).*
