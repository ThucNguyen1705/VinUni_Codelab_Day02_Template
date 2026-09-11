# 🔍 Phase 1 — SCAN & Phase 2 — QUICK-ASSESS: Vin Smart Future

> **Họ và tên sinh viên:** Nguyễn Đức Minh  
> **Mã số sinh viên (MSSV):** 2A202602891  
> **Vị trí công tác:** AI Product Engineer — Vin Smart Future (Vingroup)  
> **Đơn vị phối hợp:** Khối Phát triển Trạm sạc & Khối Dịch vụ Thông minh VinFast  
> **Đề tài lựa chọn:** **Đề xuất Trạm sạc & Lộ trình Tối ưu từ Điểm A đến Điểm B Nhanh nhất cho Xe điện VinFast**

---

## 🏛️ Bối cảnh nghiệp vụ: Tôi là ai?

Tôi là **Nguyễn Đức Minh** (MSSV: `2A202602891`), AI Product Engineer tại **Vin Smart Future**. Đơn vị của tôi được giao nhiệm vụ phối hợp trực tiếp với **Khối Phát triển Trạm sạc VinFast (VinFast Charging Network)** và **Trung tâm Điều hành Di chuyển Thông minh** để giải quyết bài toán cốt lõi và thực tế nhất của mọi chủ xe điện VinFast (VF5, VF8, VF9):

> **"Tôi đang ở điểm A và muốn lái xe đến điểm B. Nếu dung lượng pin hiện tại không đủ để chạy thẳng, hệ thống phải tự động tính toán: Tôi nên dừng sạc ở trạm nào dọc đường, và sạc trong bao lâu để tổng thời gian hành trình (Thời gian lái xe + Thời gian sạc) từ A đến B là NGẮN NHẤT?"**

Hiện nay, các ứng dụng bản đồ phổ biến như Google Maps chỉ phục vụ xe xăng (không biết mức pin % SoC của xe, không biết vị trí các trụ sạc VinFast dọc lộ trình, và không biết trụ nào đang trống hay kín chỗ). Điều này buộc tài xế phải vừa lái xe vừa tự mở App VinFast để dò tìm trạm thủ công, dẫn đến việc chọn nhầm trạm sạc chậm hoặc phải đi đường vòng (detour) xa xôi, làm chuyến đi bị kéo dài thêm 30 – 60 phút.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (4 Lenses)

Áp dụng **4 Lăng kính (4 Lenses)** để rà soát toàn bộ chuỗi giá trị vận hành của các công ty thành viên Vingroup:

| # | Đơn vị (Subsidiary) | Lăng kính (Lens) | Mô tả bài toán & Điểm nghẽn vận hành | Tổn thất ước tính (Impact) |
|---|---------------------|------------------|---------------------------------------|----------------------------|
| 1 | **VinFast** | **AI có thể tốt hơn (AI-upgrade)** | **Định tuyến & Đề xuất trạm sạc từ A đến B nhanh nhất:** Tài xế xe điện (VF5, VF8, VF9) mất nhiều thời gian tự tra cứu thủ công xem nên dừng sạc ở trạm nào dọc đường đi từ điểm A đến điểm B để tổng thời gian hành trình là ngắn nhất mà không phải đi đường vòng. | Mất 15–20 phút tự dò trạm; chuyến đi dài bị kéo dài thêm 30–60 phút do chọn sai trạm sạc chậm hoặc trạm hết chỗ. |
| 2 | **VinFast** | **Lặp lại (Repetitive)** | **So khớp hóa đơn và dữ liệu sạc điện đối tác:** Bộ phận kế toán phải so khớp thủ công hàng trăm nghìn giao dịch sạc tại các trạm sạc nhượng quyền/đối tác ngoài của VinFast với hóa đơn điện lực EVN và sao kê ngân hàng. | Tốn 80+ giờ công/tháng của 3 nhân viên tài chính; độ trễ đối soát 5-7 ngày; sai lệch số liệu phát hiện muộn. |
| 3 | **Xanh SM (GSM)** | **Tốn thời gian (Time-consuming)** | **Điều phối và gán lộ trình cuốc xe đa phương thức:** Điều phối viên can thiệp thủ công khi hành khách thay đổi điểm đến hoặc gặp điểm ùn tắc giao thông giờ cao điểm, tính toán lại giá cước và điểm sạc giữa ca của tài xế. | Mất 8–10 phút/trường hợp can thiệp; giảm 15% năng suất phục vụ khách vào giờ tan tầm. |
| 4 | **Vinhomes** | **Lặp lại (Repetitive)** | **Tiếp nhận và phân luồng phản ánh kỹ thuật cư dân:** Ban quản lý tòa nhà phải đọc thủ công hàng nghìn phản ánh qua App Vinhomes Resident (hỏng bóng đèn sảnh, áp lực nước yếu, kẹt cửa thang máy) để gán cho các tổ kỹ thuật phù hợp. | Mất 4–6 tiếng để tiếp nhận và chuyển giao phản ánh; tỷ lệ cư dân phàn nàn về tốc độ phản hồi chậm tăng 22%. |
| 5 | **Vinmec** | **Pain từ người khác (Stakeholder Pain)** | **Tóm tắt hồ sơ bệnh án xuất viện (Discharge Summary):** Bác sĩ điều trị phải dành 20-30 phút sau ca trực để tổng hợp các kết quả xét nghiệm, chẩn đoán hình ảnh và đơn thuốc thành bản tóm tắt xuất viện dễ hiểu cho bệnh nhân. | Bác sĩ kiệt sức do việc hành chính; bệnh nhân chờ đợi trung bình 45 phút để hoàn tất thủ tục ra viện. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Thẻ bài toán (Quick Cards)

Chọn Top 3 bài toán từ Phase 1 để đánh giá sơ bộ độ khả thi: **Card #1 (VinFast Lộ trình & Điểm sạc tối ưu từ A đến B), Card #2 (VinFast Đối soát sạc đối tác), Card #3 (Vinhomes Tiếp nhận phản ánh cư dân).**

---

### 📇 QUICK PROBLEM CARD #1: VinFast — Đề xuất trạm sạc & Lộ trình tối ưu từ A đến B nhanh nhất (Đề tài được chọn)

```text
┌─────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                           │
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
│   1. Nhập điểm đến B trên Google Maps xem khoảng cách và lộ trình đường đi      │
│   ──> 2. Nhìn mức pin % SoC táp-lô nhẩm tính thấy không đủ pin chạy thẳng đến B  │
│   ──> 3. Tự mở thêm App VinFast dò tìm các trạm sạc nằm gần tuyến đường A ──> B │
│   ──> 4. Bấm vào từng trạm kiểm tra xem có trụ DC sạc nhanh và còn chỗ không    │
│   ──> 5. Lái xe theo phán đoán cá nhân -> Nguy cơ trạm kín chỗ hoặc đi đường vòng│
│                                                                                 │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 13 - 15 phút mò mẫm thủ công)     │
│                                                                                 │
│ AI có thể can thiệp ở bước nào? Bước 2, 3 & 4                                   │
│ (AI tự động trích xuất SoC, vị trí GPS A và B, dòng xe -> Tính trạm sạc bám     │
│  sát tuyến đường có công suất cao nhất và còn trụ trống -> Soạn lộ trình nháp)  │
│                                                                                 │
│ Thước đo thành công (Metric có số):                                             │
│   - Giảm thời gian tìm và lên kế hoạch trạm sạc từ 15 phút ──> dưới 2 giây.      │
│   - Giảm ít nhất 35% tổng thời gian chờ sạc và đi đường vòng cho chuyến đi.     │
│   - 100% trạm đề xuất khớp chuẩn cổng sạc (CCS2/GBT) và có trụ sạc trống.       │
│                                                                                 │
│ Quick Architecture: [x] LLM Feature kết hợp Deterministic Route Solver (EVRP)   │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #2: VinFast — Đối chiếu và so khớp hóa đơn sạc điện đối tác

```text
┌─────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                           │
│                                                                                 │
│ Bài toán (1 câu): Đối chiếu tự động dữ liệu phiên sạc tại các trạm đối tác      │
│ bên ngoài với hóa đơn điện tử EVN và chứng từ ngân hàng.                         │
│                                                                                 │
│ Công ty thành viên: [x] VinFast   [ ] Xanh SM   [ ] Vinhomes                    │
│                     [ ] Vinmec    [ ] Khác ___________________                  │
│                                                                                 │
│ Ai đang đau (Actor)? Nhân viên kế toán & Chuyên viên quản lý đối tác trạm sạc   │
│                                                                                 │
│ Workflow thủ công hiện tại (4 bước):                                            │
│   1. Xuất file log sạc từ hệ thống IoT trạm đối tác (CSV/Excel)                 │
│   ──> 2. Tải hóa đơn điện tử từ EVN và bảng sao kê ngân hàng                     │
│   ──> 3. Dùng hàm VLOOKUP / Python script đối chiếu từng mã giao dịch, số kWh   │
│   ──> 4. Gửi email xác nhận công nợ và điều chỉnh sai lệch cho đối tác          │
│                                                                                 │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ 30 - 45 phút/báo cáo ngày)           │
│ AI có thể can thiệp ở bước nào? Bước 3 & 4 (OCR hóa đơn + Rule match)           │
│                                                                                 │
│ Thước đo thành công: Giảm thời gian đối soát từ 7 ngày xuống còn dưới 4 giờ.   │
│ Quick Architecture: [x] Rule-based ETL + OCR (Không cần LLM phức tạp)           │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #3: Vinhomes — Tiếp nhận và phân luồng phản ánh kỹ thuật cư dân

```text
┌─────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                           │
│                                                                                 │
│ Bài toán (1 câu): Phân loại tự động nội dung văn bản phản ánh của cư dân        │
│ Vinhomes và điều hướng chính xác về tổ bảo trì kỹ thuật / ban quản lý tòa nhà.  │
│                                                                                 │
│ Công ty thành viên: [ ] VinFast   [ ] Xanh SM   [x] Vinhomes                    │
│                     [ ] Vinmec    [ ] Khác ___________________                  │
│                                                                                 │
│ Ai đang đau (Actor)? Nhân viên CSKH Ban quản trị khu đô thị, Cư dân             │
│                                                                                 │
│ Workflow thủ công hiện tại (4 bước):                                            │
│   1. Cư dân nhập nội dung phản ánh trên App Vinhomes Resident                   │
│   ──> 2. Điều phối viên đọc nội dung phản ánh, xem ảnh chụp đính kèm            │
│   ──> 3. Gán thẻ phân loại (Điện / Nước / Thang máy / An ninh) và chọn tòa nhà  │
│   ──> 4. Tạo phiếu Ticket giao việc cho kỹ thuật viên hiện trường               │
│                                                                                 │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 5 - 10 phút/ticket vào cao điểm) │
│ AI có thể can thiệp ở bước nào? Bước 2 & 3 (Text Classification & Auto-routing) │
│                                                                                 │
│ Thước đo thành công: Phân loại đúng 95% ticket trong vòng dưới 15 giây.         │
│ Quick Architecture: [x] LLM Classifier / Text Embedding                         │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn đề tài Deep-Dive

### ✅ Bài toán được lựa chọn:
**QUICK PROBLEM CARD #1 — VinFast: Đề xuất Trạm sạc & Lộ trình Tối ưu từ A đến B Nhanh nhất cho Xe điện VinFast**

### ❌ Lý do loại bỏ các thẻ khác:
1. **Loại bỏ Card #2 (VinFast Đối soát sạc đối tác):** Thuần túy là tác vụ so khớp bảng tính (ETL) theo mã giao dịch, nên dùng script Python/SQL định danh thay vì dùng LLM tốn kém và dễ ảo giác số học.
2. **Loại bỏ Card #3 (Vinhomes Tiếp nhận phản ánh cư dân):** Là tác vụ back-office nội bộ, rủi ro pháp lý cao về thông tin cư dân, không mang tính cấp thiết thời gian thực bằng việc hỗ trợ người lái xe trên đường.

### 🎯 Lý do Card #1 mang tính chiến lược cho Vin Smart Future:
1. **Giải quyết trực diện nhu cầu sống còn:** Trả lời trực tiếp câu hỏi tài xế cần nhất: *"Đi đường nào và dừng sạc ở đâu nhanh nhất?"*.
2. **AI Fit hoàn hảo:** Kết hợp giữa giải thuật tìm đường có ràng buộc pin (Deterministic Routing Solver) và LLM Co-pilot để tương tác tự nhiên, giải thích chiến lược sạc và hiển thị trực quan lên màn hình xe.
3. **Ranh giới an toàn rõ ràng (Operational Boundary):** Bắt buộc nhãn `[DRAFT_ONLY]` để tài xế xác nhận (HITL), và cơ chế khẩn cấp khi pin nguy cấp `< 5%` kích hoạt cứu hộ `dispatch_mobile_charger`.
