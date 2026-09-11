# 🔍 Phase 1 — SCAN & Phase 2 — QUICK-ASSESS: Vin Smart Future

> **Họ và tên sinh viên:** Nguyễn Quang Minh  
> **Mã số sinh viên (MSSV):** 2A202602891  
> **Vị trí công tác:** AI Product Engineer — Vin Smart Future (Vingroup)  
> **Đơn vị phối hợp:** Khối Phát triển Trạm sạc & Khối Dịch vụ Thông minh VinFast  
> **Đề tài lựa chọn:** **VinFast — Trợ lý hướng dẫn trạm sạc thông minh và tối ưu hóa cổng sạc (CCS2/GBT)**

---

## 🏛️ Bối cảnh nghiệp vụ: Tôi là ai?

Tôi là **Nguyễn Quang Minh** (MSSV: `2A202602891`), AI Product Engineer tại **Vin Smart Future**. Đơn vị của tôi được giao nhiệm vụ phối hợp trực tiếp với **Khối Phát triển Trạm sạc VinFast (VinFast Charging Network)** và **Trung tâm Trải nghiệm Khách hàng VinFast** để nâng cao trải nghiệm sạc xe điện thông minh cho toàn bộ người dùng xe điện VinFast (từ các dòng xe đô thị như VF3, VF5 đến các dòng SUV cao cấp VF8, VF9).

Trong quá trình đồng hành cùng đội ngũ kỹ thuật thực địa và đường dây nóng CSKH của VinFast, tôi ghi nhận một điểm nghẽn nghiêm trọng: Khi xe gần cạn pin hoặc di chuyển đường dài, tài xế thường xuyên phải tự tìm trạm sạc trên ứng dụng hoặc bản đồ bên thứ ba, nhưng khi tới nơi lại gặp tình trạng trạm sạc quá tải, hết trụ trống hoặc trụ sạc không tương thích công suất/chuẩn cổng sạc (CCS2 DC siêu nhanh vs GBT / AC Type 2). Tình trạng này gây ức chế tâm lý cực lớn (Range Anxiety - nỗi lo cạn pin), thậm chí dẫn đến các vụ xe cạn kiệt pin giữa đường và phải gọi cứu hộ khẩn cấp.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (4 Lenses)

Áp dụng **4 Lăng kính (4 Lenses)** để rà soát toàn bộ chuỗi giá trị vận hành của các công ty thành viên Vingroup nhằm phát hiện các điểm nghẽn (bottlenecks) có thể cải tiến bằng AI:

| # | Đơn vị (Subsidiary) | Lăng kính (Lens) | Mô tả bài toán & Điểm nghẽn vận hành | Tổn thất ước tính (Impact) |
|---|---------------------|------------------|---------------------------------------|----------------------------|
| 1 | **VinFast** | **AI có thể tốt hơn (AI-upgrade)** | **Trợ lý hướng dẫn trạm sạc thông minh:** Tài xế xe điện (VF5, VF8, VF9) mất nhiều thời gian tự tìm trạm sạc còn trống và phù hợp chuẩn cổng sạc (CCS2/GBT, công suất 11kW/30kW/60kW/150kW/250kW). Cần tự động đề xuất lịch trình sạc tối ưu theo tình trạng pin (SoC) và lộ trình di chuyển. | Mất 15–20 phút/lần tìm trạm sạc; rò rỉ ~12% năng lượng do đi lạc trạm hoặc xếp hàng chờ trụ sạc. Nguy cơ cạn kiệt pin giữa đường. |
| 2 | **VinFast** | **Lặp lại (Repetitive)** | **So khớp hóa đơn và dữ liệu sạc điện đối tác:** Bộ phận kế toán phải so khớp thủ công hàng trăm nghìn giao dịch sạc tại các trạm sạc nhượng quyền/đối tác ngoài của VinFast với hóa đơn điện lực EVN và sao kê ngân hàng. | Tốn 80+ giờ công/tháng của 3 nhân viên tài chính; độ trễ đối soát 5-7 ngày; sai lệch số liệu phát hiện muộn. |
| 3 | **Xanh SM (GSM)** | **Tốn thời gian (Time-consuming)** | **Điều phối và gán lộ trình cuốc xe đa phương thức:** Điều phối viên can thiệp thủ công khi hành khách thay đổi điểm đến hoặc gặp điểm ùn tắc giao thông giờ cao điểm, tính toán lại giá cước và trạm sạc giữa ca của tài xế. | Mất 8–10 phút/trường hợp can thiệp; giảm 15% năng suất phục vụ khách vào giờ tan tầm. |
| 4 | **Vinhomes** | **Lặp lại (Repetitive)** | **Tiếp nhận và phân luồng phản ánh kỹ thuật cư dân:** Ban quản lý tòa nhà phải đọc thủ công hàng nghìn phản ánh qua App Vinhomes Resident (hỏng bóng đèn sảnh, áp lực nước yếu, kẹt cửa thang máy) để gán cho các tổ kỹ thuật phù hợp. | Mất 4–6 tiếng để tiếp nhận và chuyển giao phản ánh; tỷ lệ cư dân phàn nàn về tốc độ phản hồi chậm tăng 22%. |
| 5 | **Vinmec** | **Pain từ người khác (Stakeholder Pain)** | **Tóm tắt hồ sơ bệnh án xuất viện (Discharge Summary):** Bác sĩ điều trị phải dành 20-30 phút sau ca trực để tổng hợp các kết quả xét nghiệm, chẩn đoán hình ảnh và đơn thuốc thành bản tóm tắt xuất viện dễ hiểu cho bệnh nhân. | Bác sĩ kiệt sức do việc hành chính; bệnh nhân chờ đợi trung bình 45 phút để hoàn tất thủ tục ra viện. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Thẻ bài toán (Quick Cards)

Chọn Top 3 bài toán từ Phase 1 để đánh giá sơ bộ độ khả thi: **Card #1 (VinFast Trợ lý trạm sạc thông minh), Card #2 (VinFast Đối soát sạc đối tác), Card #3 (Vinhomes Tiếp nhận phản ánh cư dân).**

---

### 📇 QUICK PROBLEM CARD #1: VinFast — Trợ lý hướng dẫn trạm sạc thông minh (Đề tài được chọn)

```text
┌─────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                           │
│                                                                                 │
│ Bài toán (1 câu): Tài xế xe điện VinFast (VF5, VF8, VF9) cần trợ lý tự động đề   │
│ xuất lộ trình và trạm sạc còn trụ trống, đúng chuẩn cổng (CCS2/GBT) theo SoC.   │
│                                                                                 │
│ Công ty thành viên: [x] VinFast   [ ] Xanh SM   [ ] Vinhomes                    │
│                     [ ] Vinmec    [ ] Khác ___________________                  │
│                                                                                 │
│ Ai đang đau (Actor)? Tài xế xe điện VinFast, Điều phối viên kỹ thuật trạm sạc    │
│                                                                                 │
│ Workflow thủ công hiện tại (5 bước):                                            │
│   1. Tài xế thấy xe báo pin yếu (< 20%) trên màn hình táp-lô                    │
│   ──> 2. Mở App VinFast/Google Maps tìm các trạm sạc xung quanh bán kính        │
│   ──> 3. Tự lọc thủ công trạm có cổng CCS2/GBT và còn trụ khả dụng             │
│   ──> 4. Lái xe đến trạm (thường xuyên gặp trạm đã kín chỗ hoặc đang bảo trì)   │
│   ──> 5. Gọi hotline cứu hộ khẩn cấp nếu xe cạn kiệt pin dọc đường              │
│                                                                                 │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 15 - 20 phút/lượt xử lý)          │
│                                                                                 │
│ AI có thể can thiệp ở bước nào? Bước 2, 3 & 4                                   │
│ (AI tự động trích xuất SoC, vị trí GPS, dòng xe -> Tra cứu API trạm sạc real-   │
│  time -> Soạn bản nháp lộ trình sạc tối ưu kèm cổng sạc chính xác cho tài xế)   │
│                                                                                 │
│ Thước đo thành công (Metric có số):                                             │
│   - Giảm thời gian tìm và xác nhận trạm sạc từ 18 phút ──> dưới 2 phút.          │
│   - Tỷ lệ gợi ý trạm sạc chính xác chuẩn cổng (CCS2/GBT) và còn trụ trống: >= 98%│
│   - Tỷ lệ sự cố cạn kiệt pin giữa đường cần xe sạc lưu động cứu hộ: giảm 85%.   │
│                                                                                 │
│ Quick Architecture: [x] LLM Feature kết hợp Rule-based Constraint Engine        │
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
**QUICK PROBLEM CARD #1 — VinFast: Trợ lý hướng dẫn trạm sạc thông minh và tối ưu hóa cổng sạc (CCS2/GBT)**

### ❌ Lý do loại bỏ các thẻ khác:
1. **Loại bỏ Card #2 (VinFast Đối soát sạc đối tác):**
   - **Bản chất bài toán:** Đây thuần túy là bài toán tích hợp dữ liệu (ETL) và so khớp định danh (deterministic matching) theo mã giao dịch, số kWh và số tiền.
   - **Tại sao không dùng LLM?** Dùng LLM cho bài toán số học tài chính có nguy cơ xảy ra ảo giác (hallucination) và chi phí API không cần thiết. Một script Python/SQL chạy batch job với rule-based logic giải quyết bài toán này tốt hơn, chính xác 100% và tiết kiệm hơn.
2. **Loại bỏ Card #3 (Vinhomes Tiếp nhận phản ánh cư dân):**
   - **Đặc thù bài toán:** Dù bài toán xử lý ngôn ngữ tự nhiên tốt, nhưng phạm vi dữ liệu nội bộ liên quan đến thông tin bảo mật căn hộ, khiếu nại tranh chấp quyền sở hữu có độ rủi ro pháp lý cao nếu AI sinh lời giải sai lệch. Ngoài ra, quy trình nghiệp vụ mang tính back-office, không tạo ra tác động trực tiếp và cấp thiết bằng sự cố tài xế xe điện có nguy cơ nằm đường vì cạn pin.

### 🎯 Lý do Card #1 là ứng viên hoàn hảo cho Vin Smart Future:
1. **Tính cấp thiết thời gian thực (Real-time Mission-Critical):** Trực tiếp giải quyết nỗi đau lớn nhất của người dùng xe điện VinFast (Range Anxiety), ảnh hưởng trực tiếp đến uy tín thương hiệu quốc gia của VinFast.
2. **AI Fit hoàn hảo:** Kết hợp giữa dữ liệu phi cấu trúc (ngôn ngữ tài xế yêu cầu qua giọng nói/text) và dữ liệu có cấu trúc từ hệ thống xe (SoC, vị trí GPS, dòng xe VF5/VF8/VF9) để tổng hợp ra chỉ dẫn sạc thông minh, thân thiện.
3. **Ranh giới an toàn rõ ràng (Strict Operational Boundary):** Bắt buộc phải có cơ chế Human-in-the-loop (tài xế xác nhận lộ trình), cơ chế an toàn pin nguy cấp (< 5% thì cấm hướng dẫn trạm xa > 5km mà phải điều xe cứu hộ sạc pin di động), và gắn thẻ `[DRAFT_ONLY]` để tránh can thiệp ngoài tầm kiểm soát.
