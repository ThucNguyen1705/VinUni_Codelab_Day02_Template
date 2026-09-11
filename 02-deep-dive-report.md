# 02 — Báo Cáo Phân Tích Sâu (Deep-Dive Report): AI Diagnostic Copilot cho VinFast

**Dự án:** Trợ lý AI Chẩn đoán Sơ bộ Lỗi Kỹ thuật từ Ngôn ngữ Tự nhiên Tiếng Việt (VinFast AI Diagnostic Copilot)  
**Đơn vị thực hiện:** Nhóm Kỹ sư AI Product — Vin Smart Future (Vingroup)  
**Khối nghiệp vụ bảo trợ:** Khối Dịch vụ Hậu mãi & Xưởng Dịch vụ VinFast (VinFast After-sales & Service Centers)  

---

## 🏛️ 1. Bối cảnh & Lý do lựa chọn bài toán

VinFast đang trong giai đoạn phát triển bùng nổ về số lượng xe điện lưu hành (VF3, VF5, VF6, VF7, VF8, VF9) tại thị trường Việt Nam và quốc tế. Hệ thống Xưởng Dịch vụ (Service Center) tiếp nhận trung bình hơn 3.000 lượt xe bảo dưỡng, kiểm tra sự cố mỗi ngày.

Một trong những thách thức vận hành lớn nhất tại xưởng là **khâu tiếp nhận ban đầu**:
* Khách hàng là người tiêu dùng phổ thông, khi xe có hiện tượng bất thường thường diễn đạt bằng các từ tượng thanh, cảm tính mang tính phương ngữ (ví dụ: *"vào cua nghe tiếng lục cục bên phụ"*, *"qua gờ giảm tốc kêu cụp cụp ở gầm"*, *"đạp ga xe rung bần bật"*, *"màn hình hiện rùa vàng nhưng điều hòa vẫn mát rượi"*).
* Cố vấn dịch vụ (Service Advisor) thường là các nhân sự trẻ, không thể thuộc hết hàng nghìn mã lỗi DTC (Diagnostic Trouble Codes) và các cụm linh kiện phức tạp của xe điện. Họ mất nhiều thời gian tra cứu sách hướng dẫn sửa chữa (Service Manual), thậm chí phải nhờ thợ cả lái thử xe nhiều lần mới xác định được xe hỏng ở đâu.
* Hậu quả: Thời gian tiếp nhận kéo dài 25–40 phút/xe, gây ùn tắc tại quầy, chẩn đoán nhầm cụm linh kiện làm tăng chi phí bảo hành và giảm chỉ số hài lòng khách hàng (CSAT).

Nhóm quyết định phát triển **AI Diagnostic Copilot** để hỗ trợ cố vấn dịch vụ phiên dịch tức thì từ mô tả triệu chứng của khách hàng sang nhóm mã lỗi kỹ thuật chuẩn và khuyến nghị các bài test thực địa cần làm.

---

## 🏗️ 2. Quy trình Vận hành Hiện tại (Current-State Workflow Mapping)

Quy trình tiếp nhận và chẩn đoán thủ công hiện tại tại Xưởng Dịch vụ VinFast:

```text
┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│ Bước 1          │      │ Bước 2          │      │ Bước 3          │
│ Khách mang xe   │      │ Cố vấn dịch vụ  │      │ Tra cứu sổ tay  │
│ đến & mô tả lỗi │ ───> │ ghi chép thủ    │ ───> │ kỹ thuật & hỏi  │
│ bằng tiếng Việt │      │ công vào sổ     │      │ ý kiến thợ cả   │
│                 │      │                 │      │                 │
│ Actor: Khách    │      │ Actor: Cố vấn   │      │ Actor: Cố vấn   │
│ ⏱ 5 phút        │      │ ⏱ 5 phút        │      │ ⏱ 15 phút 🔴    │
│ In: Lời nói     │      │ In: Lời nói     │      │ In: Ghi chép tay│
│ Out: Âm thanh   │      │ Out: Note thô   │      │ Out: Nhóm lỗi   │
└─────────────────┘      └─────────────────┘      └─────────────────┘
                                                           │
                                                           ▼ 🔄 Handoff
┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│ Bước 6          │      │ Bước 5          │      │ Bước 4          │
│ Lập phiếu tiếp  │      │ Báo cáo kết quả │      │ Kỹ thuật viên   │
│ nhận & gửi báo  │ <─── │ cho cố vấn dịch │ <─── │ cắm máy OBD2    │
│ giá cho khách   │      │ vụ tại quầy     │      │ hoặc lái thử xe │
│                 │      │                 │      │                 │
│ Actor: Cố vấn   │      │ Actor: Kỹ thuật │      │ Actor: Kỹ thuật │
│ ⏱ 5 phút        │      │ ⏱ 3 phút        │      │ ⏱ 15 phút 🔴    │
│ In: Kết luận kt │      │ In: Máy đo      │      │ In: Xe vật lý   │
│ Out: Báo giá    │      │ Out: DTC / Lỗi  │      │ Out: Xác nhận   │
└─────────────────┘      └─────────────────┘      └─────────────────┘

🔴 = Điểm nghẽn cổ chai (Bottlenecks) tại Bước 3 và Bước 4
🔄 Handoff = Chuyển giao thông tin từ Cố vấn dịch vụ sang Kỹ thuật viên xưởng
⏱ Tổng thời gian xử lý tiếp nhận: ~45 - 50 phút / lượt xe
```

### Phân tích chi tiết Bottlenecks & Handoff:
* **🔴 Bottleneck 1 (Bước 3 - Mất 15 phút):** Cố vấn dịch vụ phải lật giở tài liệu kỹ thuật hoặc tra cứu portal nội bộ của VinFast để tìm xem mô tả của khách ứng với cụm linh kiện nào (Hệ thống treo trước/sau, rotuyn cân bằng, motor điện, inverter, hay hệ thống làm mát pin).
* **🔴 Bottleneck 2 (Bước 4 - Mất 15 phút):** Do thông tin ban đầu mơ hồ, Kỹ thuật viên phải tốn thời gian lái thử xe vào các đoạn đường gồ ghề hoặc cắm máy scan toàn bộ xe để dò tìm mã lỗi.
* **🔄 Handoff:** Thông tin tam sao thất bản từ lời khách kể -> cố vấn ghi chép -> kỹ thuật viên đọc lại, làm tăng nguy cơ chẩn đoán sai lệch.

---

## 🎯 3. Bản Tuyên Bố Bài Toán (Problem Statement - 6 Fields)

Bảng tuyên bố bài toán theo chuẩn kỹ thuật của **Vin Smart Future**:

| Trường thông tin | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Cố vấn dịch vụ (Service Advisor) tại quầy tiếp nhận và Kỹ thuật viên (Technician) tại Xưởng Dịch vụ VinFast. |
| **2. Current Workflow** | Khách hàng mang xe đến xưởng và mô tả hiện tượng hỏng hóc bằng tiếng Việt. Cố vấn ghi chép, tra cứu sổ tay kỹ thuật thủ công, chuyển giao cho kỹ thuật viên cắm máy quét OBD2 hoặc lái thử để xác nhận lỗi, sau đó lập báo giá sửa chữa. Quy trình 6 bước, mất 45–50 phút/xe. |
| **3. Bottleneck** | Bước 2, 3 và 4: Khách hàng mô tả mơ hồ, từ ngữ dân dã không khớp với thuật ngữ kỹ thuật chuẩn. Cố vấn mất 15–20 phút để đối chiếu sổ tay; kỹ thuật viên mất thêm 15 phút mò mẫm thử nghiệm vật lý. |
| **4. Business Impact** | Mỗi xưởng tiếp nhận ~60 xe/ngày. Việc chẩn đoán sơ bộ chậm gây ùn tắc kéo dài 20 giờ làm việc/ngày của cả đội ngũ; tỷ lệ chẩn đoán nhầm phụ tùng ban đầu là 12%, gây lãng phí chi phí bảo hành ước tính hàng tỷ đồng mỗi năm cho VinFast và giảm điểm CSAT dịch vụ. |
| **5. Success Metric** | **1. Rút ngắn thời gian:** Giảm thời gian chẩn đoán sơ bộ ban đầu từ 25 phút xuống dưới **5 phút**.<br>**2. Độ chính xác:** Tỷ lệ AI gợi ý đúng cụm chi tiết hoặc mã lỗi tiềm năng đạt **> 85%**.<br>**3. CSAT:** Nâng chỉ số hài lòng của khách hàng tại khâu tiếp nhận từ 3.8 lên **> 4.5/5.0 sao**. |
| **6. Operational Boundary (Ranh giới cấm)** | **Quyền hạn:** AI được phép trích xuất thực thể, gợi ý top 3 nguyên nhân kỹ thuật khả dĩ, đề xuất các bước test vật lý cho thợ.<br>**CẤM TUYỆT ĐỐI:**<br>1. AI không được tự ý xuất lệnh thay thế phụ tùng hoặc chốt báo giá cho khách (Bắt buộc Human-in-the-loop: Kỹ thuật viên phải ký duyệt).<br>2. Mọi kết quả do AI tạo ra đều phải gắn thẻ `[DRAFT_ONLY]` ở đầu để tránh hệ thống tự động đẩy sang phần mềm kế toán/kho linh kiện.<br>3. Nếu mô tả liên quan đến các lỗi an toàn nghiêm trọng (Phanh - Brake, Hệ thống lái - Steering, Pin cao áp - HV Battery, Cháy nổ) -> Bắt buộc kích hoạt cảnh báo đỏ `CRITICAL_SAFETY_WARNING` và yêu cầu dừng xe kiểm tra khẩn cấp. |

---

## 🚀 4. Quy Trình Tương Lai Tích Hợp AI (Future-State Flow & AI Fit)

### 4.1. Xác định mức độ phù hợp AI (AI-Fit Matrix)
* **Lựa chọn:** **LLM Feature (Copilot hỗ trợ cố vấn dịch vụ)**.
* **Lý do không dùng Rule-based thông thường:** Ngôn ngữ tiếng Việt đời thường của khách hàng vô cùng phong phú, chứa nhiều từ địa phương, từ tượng thanh (*"ro ro"*, *"cục cục"*, *"rít rít"*), ngữ pháp phi cấu trúc. Hệ thống if-else truyền thống hoàn toàn bất lực trong việc bao quát các ngữ cảnh này.
* **Lý do không dùng Autonomous Agent:** Khâu sửa chữa ô tô liên quan trực tiếp đến tính mạng con người và tài sản lớn. Một sai lầm ảo giác (hallucination) của AI có thể dẫn đến việc bỏ sót lỗi phanh gây tai nạn. Do đó, mô hình phù hợp nhất là **Copilot trợ lý hỗ trợ con người**, đặt con người làm trung tâm phê duyệt (Human-in-the-loop).

### 4.2. Sơ đồ Quy trình tương lai (Future-State Flowchart)

```text
┌─────────────────┐      ┌─────────────────────────┐      ┌─────────────────────────┐
│ Bước 1          │      │ Bước 2                  │      │ Bước 3                  │
│ Khách mang xe   │      │ 🔵 AI Diagnostic Copilot│      │ 🟢 Cố vấn dịch vụ       │
│ đến & mô tả     │ ───> │ Phân tích triệu chứng,  │ ───> │ Review kết quả AI, chọn │
│ bằng tiếng Việt │      │ map DTC & gợi ý test    │      │ gói kiểm tra & in lệnh  │
│                 │      │                         │      │                         │
│ Actor: Khách    │      │ Actor: Gemini 2.5 Flash │      │ Actor: Cố vấn (HITL)    │
│ ⏱ 3 phút        │      │ ⏱ 5 giây                │      │ ⏱ 2 phút                │
│ Out: Text thô   │      │ Tag: [DRAFT_ONLY]       │      │ Quyết định: DUYỆT       │
└─────────────────┘      └─────────────────────────┘      └─────────────────────────┘
                                                                       │
                                                                       ▼
                                                          ┌─────────────────────────┐
                                                          │ Bước 4                  │
                                                          │ Kỹ thuật viên kiểm tra  │
                                                          │ đúng chi tiết trọng tâm │
                                                          │ theo hướng dẫn của AI   │
                                                          │                         │
                                                          │ Actor: Kỹ thuật viên    │
                                                          │ ⏱ 5 - 10 phút           │
                                                          └─────────────────────────┘
                                                                       │
                                                                       ▼
                                                          ┌─────────────────────────┐
                                                          │ ↩️ Fallback Plan        │
                                                          │ Nếu AI phản hồi sai     │
                                                          │ hoặc không tự tin       │
                                                          │ (< 70%), chuyển sang quy│
                                                          │ trình khám xe truyền    │
                                                          │ thống bằng thợ cả.      │
                                                          └─────────────────────────┘

🔵 = Bước AI xử lý tự động (AI Step)
🟢 = Bước con người thẩm định và duyệt (Human-in-the-loop)
↩️ = Kế hoạch dự phòng (Fallback Plan)
⏱ Tổng thời gian tiếp nhận rút xuống: ~10 - 15 phút (Giảm hơn 65% thời gian)
```

---

## 🛡️ 5. Ranh Giới Vận Hành & Kịch Bản Kiểm Thử An Toàn (Operational Guardrails)

Để đảm bảo hệ thống tuyệt đối an toàn và tuân thủ chuẩn Vin Smart Future:

1. **Guardrail 1 — Thẻ kiểm soát bản nháp (`[DRAFT_ONLY]`):**
   Mọi phản hồi phân tích chẩn đoán của AI bắt buộc phải mở đầu bằng tiền tố `[DRAFT_ONLY]`. Điều này ngăn chặn việc hệ thống ERP xưởng dịch vụ tự động xuất kho linh kiện hoặc gửi hóa đơn thanh toán cho khách hàng mà chưa qua tay cố vấn.
2. **Guardrail 2 — Cảnh báo An toàn Tối cao (`CRITICAL_SAFETY_WARNING`):**
   Khi phát hiện bất kỳ dấu hiệu nào liên quan đến **Mất phanh, Kẹt chân ga, Khói/Mùi khét từ cụm Pin cao áp, hoặc Mất trợ lực lái**, AI phải lập tức gắn cờ cảnh báo nguy hiểm cấp 1, yêu cầu ngắt cầu dao khẩn cấp và không cho phép khách hàng tự lái xe vào xưởng.
3. **Guardrail 3 — Giới hạn Phạm vi (Strict Scope):**
   AI từ chối trả lời mọi câu hỏi nằm ngoài phạm vi kỹ thuật xe VinFast (ví dụ: không tư vấn pháp luật bảo hiểm, không so sánh tiêu cực với các hãng xe đối thủ).

---

## 🏁 6. Đánh Giá Sẵn Sàng & Quyết Định Dự Án (Phase 5 — EVALUATE)

### 6.1. Bảng kiểm tra độ sẵn sàng (AI Readiness Checklist):
* [x] **Dữ liệu mẫu/logs sạch:** VinFast đã có cơ sở dữ liệu hàng trăm nghìn phiếu sửa chữa (DTC codes, linh kiện đã thay, mô tả của khách) trên hệ thống DMS (Dealer Management System).
* [x] **Rủi ro nằm trong tầm kiểm soát:** Thiết kế kiến trúc 100% tuân thủ **Human-in-the-loop**; cố vấn và kỹ thuật viên luôn là người chịu trách nhiệm cuối cùng. Có Fallback rõ ràng.
* [x] **Stakeholders sẵn sàng:** Ban Giám đốc Khối Dịch vụ Hậu mãi VinFast đang rất nóng lòng muốn giảm thời gian chờ đợi của khách hàng tại các xưởng trọng điểm (Hà Nội, TP.HCM, Đà Nẵng).

---

### 6.2. Quyết định cuối cùng:
# 🟢 **GO (BẮT ĐẦU TRIỂN KHAI BẢN MẪU PROTOTYPE)**

### 6.3. Lý giải quyết định (Justification):
1. **Hiệu quả đầu tư (ROI) vượt trội:** Dự án giải quyết trực tiếp bài toán quá tải tại các xưởng dịch vụ VinFast. Việc rút ngắn 20 phút/lượt tiếp nhận giúp mỗi xưởng tăng công suất phục vụ thêm 25–30% mà không cần tuyển thêm nhân sự.
2. **Tính khả thi kỹ thuật cao:** Sử dụng mô hình **Gemini 2.5 Flash** với chi phí token cực thấp, độ trễ phản hồi dưới 2 giây và khả năng hiểu tiếng Việt ngữ cảnh sâu sắc vượt trội.
3. **Kiểm soát an toàn tuyệt đối:** Dự án không giao quyền tự quyết (no autonomous action) cho AI, do đó rủi ro pháp lý và an toàn kỹ thuật được kiểm soát ở mức 0.
