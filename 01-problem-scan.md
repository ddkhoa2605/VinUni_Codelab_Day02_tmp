# 01 — Problem Scan & Quick Assessment (Vin Smart Future — Vinmec Edition)

---

## 👤 Thông tin cá nhân & Đơn vị thực hiện
* **Kỹ sư AI:** Nguyễn Văn Minh
* **Bộ phận:** Vin Smart Future (Vingroup)
* **Đơn vị hợp tác vận hành:** Hệ thống Y tế Vinmec (Vinmec Healthcare System)
* **Branch Git:** `nguyenvanminh`

---

## 🔍 Phase 1 — SCAN: Quét cơ hội vận hành tại Vinmec (4 Lenses)

Sử dụng phương pháp **4 Lenses** (*Lặp lại, Tốn thời gian, AI có thể làm tốt hơn, Pain từ người khác*) để rà soát toàn diện các chuỗi quy trình nghiệp vụ thủ công, tốn nhiều nhân lực và tiềm ẩn nguy cơ rò rỉ hiệu suất tại Vinmec.

### Bảng quét cơ hội (SCAN Table):

| # | Subsidiary | Lens | Quy trình thủ công & Pain Point vận hành | Thống kê ước tính tổn thất & Rò rỉ hiệu suất |
|:---:|:---:|:---:|:---|:---|
| **1** | **Vinmec** | **Tốn thời gian** *(Time-consuming)* | **Soạn thảo tóm tắt hồ sơ bệnh án xuất viện (Discharge Summary):** Bác sĩ nội trú phải đọc lại toàn bộ kết quả cận lâm sàng (xét nghiệm, CT/MRI), diễn tiến bệnh, thuốc điều trị trong suốt đợt nằm viện để tổng hợp thành văn bản tóm tắt xuất viện bằng ngôn ngữ y khoa chuẩn xác kết hợp hướng dẫn dễ hiểu cho bệnh nhân. | Bác sĩ mất **25–35 phút/hồ sơ**. Với ~250 lượt xuất viện/ngày trên 7 bệnh viện Vinmec, tiêu tốn hơn **120 giờ làm việc chuyên môn cao/ngày**. Gây chậm trễ giờ trả giường (downtime giường bệnh 1.5–2 giờ), làm tăng thời gian chờ của bệnh nhân mới. |
| **2** | **Vinmec** | **Pain từ người khác** *(Stakeholder Pain)* | **Phân loại triệu chứng & Đặt lịch khám chuyên khoa (Intelligent Triage):** Khách hàng liên hệ tổng đài/App MyVinmec mô tả các triệu chứng phức hợp, mơ hồ (đau tức ngực kèm mỏi vai gáy, chóng mặt). Nhân viên CSKH/Call center không có bằng cấp y khoa chuyên sâu dễ xếp sai chuyên khoa (Tim mạch vs Cơ xương khớp vs Thần kinh). | Ước tính **18–22% ca khám ban đầu bị chỉ định sai chuyên khoa**, bệnh nhân phải làm thủ tục chuyển khoa sau lần khám đầu, gây bức xúc, mất thêm 1 ngày chờ đợi, giảm chỉ số hài lòng CSAT xuống dưới 75% và lãng phí công suất phòng khám chuyên gia. |
| **3** | **Vinmec** | **Tốn thời gian & Chi phí cao** *(Time-consuming & Cost)* | **Tự động bóc tách & dịch thuật hồ sơ bệnh án đa ngôn ngữ cho bệnh nhân quốc tế (International Medical Records Translation):** Khách hàng quốc tế (chuyên gia expat, khách du lịch) khi xuất viện yêu cầu toàn bộ bệnh án, kết quả phẫu thuật, xét nghiệm phải dịch sang tiếng Anh chuẩn y khoa để nộp bảo hiểm toàn cầu (Cigna, Allianz, SOS International). Hiện Vinmec phải thuê ngoài dịch thuật thủ công. | Bệnh nhân phải chờ **3–5 ngày làm việc** sau khi ra viện mới nhận được hồ sơ. Chi phí thuê dịch thuật y khoa bên ngoài tốn **300.000–500.000 VND/trang** (trung bình 6–10 triệu VND/bộ hồ sơ 20 trang), tiêu tốn **350–500 triệu VND/tháng/bệnh viện**. Bác sĩ Vinmec mất thêm 30 phút rà soát vì bên ngoài hay dịch sai thuật ngữ lâm sàng. |
| **4** | **Vinmec** | **AI có thể tốt hơn** *(AI-upgrade)* | **Ghi nhận hồ sơ bệnh án qua giọng nói thời gian thực (Clinical Voice-to-EMR):** Trong ca khám ngoại trú, bác sĩ phải vừa thăm khám vừa gõ bàn phím nhập liệu tiền sử, bệnh sử vào hệ thống EMR, làm giảm sự tương tác bằng mắt với người bệnh. | Bác sĩ mất **40% thời gian của một ca khám (khoảng 6–8 phút/ca 15 phút)** chỉ để gõ máy tính. Dễ xảy ra sai sót gõ nhầm liều lượng thuốc, giảm năng suất phục vụ từ 25 bệnh nhân/ngày xuống còn 15 bệnh nhân/ngày/bác sĩ. |
| **5** | **Vinmec** | **Lặp lại & Pain** *(Repetitive & Pain)* | **Chăm sóc và theo dõi tuân thủ phác đồ sau xuất viện (Post-discharge Monitoring):** Điều dưỡng gọi điện thoại định kỳ vào ngày thứ 3 và thứ 7 sau xuất viện để hỏi thăm vết mổ, tác dụng phụ của thuốc và nhắc lịch tái khám. | Tỉ lệ gọi thành công chỉ đạt **35–40%** (khách hàng bận, không nghe số lạ). Ước tính **28% bệnh nhân mạn tính/sau mổ không tái khám đúng hẹn**, tăng tỉ lệ tái nhập viện trong 30 ngày (Readmission rate) lên 8.5%, ảnh hưởng tiêu chuẩn chất lượng quốc tế JCI. |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn lọc **top 3 bài toán** khả thi và có tác động kinh doanh cao nhất từ danh sách trên để phân tích thẻ đánh giá nhanh.

---

### 📇 QUICK PROBLEM CARD #1: Soạn thảo Tóm Tắt Hồ Sơ Xuất Viện (Discharge Summary)

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                       │
│                                                                             │
│ Bài toán (1 câu): Bác sĩ nội trú mất quá nhiều thời gian đọc lại EMR để      │
│ soạn thảo tóm tắt bệnh án xuất viện, làm chậm tiến độ giải phóng giường bệnh.│
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes                  │
│                     [x] Vinmec   [ ] Khác (Ghi rõ)________                  │
│                                                                             │
│ Ai đang đau (Actor)? Bác sĩ điều trị (quá tải), Bệnh nhân (chờ xuất viện)  │
│                                                                             │
│ Workflow thủ công hiện tại (5 bước):                                        │
│   1. Mở EMR bệnh nhân ──> 2. Đọc tổng hợp xét nghiệm & thuốc điều trị       │
│   ──> 3. Gõ bản tóm tắt lâm sàng ──> 4. Soạn lời dặn dùng thuốc tại nhà     │
│   ──> 5. Ký tên & chuyển phòng Kế hoạch tổng hợp duyệt                      │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 25 phút/hồ sơ)               │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3, 4                          │
│ (Trích xuất tự động dữ liệu EMR -> Draft bản tóm tắt & lời dặn bệnh nhân)   │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│   "Giảm thời gian soạn tóm tắt từ 30 phút ──> dưới 5 phút/bệnh nhân.        │
│    100% hồ sơ có chữ ký xác nhận của Bác sĩ phụ trách (Human-in-the-loop)." │
│                                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM Feature  [ ] Agent         │
└─────────────────────────────────────────────────────────────────────────────┘
```

* **Lý do AI Fit:** Cần khả năng xử lý ngôn ngữ tự nhiên (NLP) để tổng hợp các ghi chú rời rạc của bác sĩ lâm sàng và kết quả cận lâm sàng thành đoạn văn mạch lạc, chuẩn y khoa. Ranh giới vận hành: Bắt buộc gắn tag `[DRAFT_ONLY]`, cấm gửi trực tiếp cho bệnh nhân nếu chưa có chữ ký số của bác sĩ.

---

### 📇 QUICK PROBLEM CARD #2: Phân Loại Triệu Chứng & Điều Hướng Lịch Khám Ban Đầu

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                       │
│                                                                             │
│ Bài toán (1 câu): Khách hàng mô tả triệu chứng mơ hồ qua app/tổng đài dẫn   │
│ đến việc nhân viên CSKH xếp nhầm chuyên khoa khám, gây lãng phí thời gian.  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes                  │
│                     [x] Vinmec   [ ] Khác (Ghi rõ)________                  │
│                                                                             │
│ Ai đang đau (Actor)? Bệnh nhân (mất công đi lại), CSKH (áp lực phân loại)  │
│                                                                             │
│ Workflow thủ công hiện tại (4 bước):                                        │
│   1. Tiếp nhận mô tả triệu chứng từ bệnh nhân qua điện thoại / tin nhắn     │
│   ──> 2. CSKH tra cứu bảng hướng dẫn chuyên khoa nội bộ                     │
│   ──> 3. Đoán chuyên khoa phù hợp và mở lịch bác sĩ còn trống               │
│   ──> 4. Xác nhận đặt hẹn và gửi SMS thông báo cho khách hàng               │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 8 phút, tỉ lệ xếp sai 20%)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3                            │
│ (Phân tích NLP triệu chứng bệnh nhân -> Gợi ý top 2 chuyên khoa phù hợp)    │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│   "Giảm tỉ lệ xếp sai chuyên khoa từ 20% ──> dưới 3%.                       │
│    Rút ngắn thời gian chốt lịch khám từ 8 phút ──> dưới 2 phút."            │
│                                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM Feature  [ ] Agent         │
└─────────────────────────────────────────────────────────────────────────────┘
```

* **Lý do AI Fit:** Ngôn ngữ bệnh nhân miêu tả mang tính đời thường, phi cấu trúc. LLM hiểu ngữ cảnh ngữ nghĩa tốt hơn nhiều so với hệ thống tìm kiếm từ khóa (keyword search). Ranh giới: AI chỉ gợi ý chuyên khoa khám lâm sàng, TUYỆT ĐỐI không chẩn đoán bệnh thay bác sĩ và phải cảnh báo gọi cấp cứu 115 nếu phát hiện triệu chứng đột quỵ / nhồi máu cơ tim.

---

### 📇 QUICK PROBLEM CARD #3: Tự Động Bóc Tách & Dịch Thuật Bệnh Án Cho Bệnh Nhân Quốc Tế

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                       │
│                                                                             │
│ Bài toán (1 câu): Bệnh nhân quốc tế phải chờ 3-5 ngày và tốn hàng chục triệu│
│ để dịch thuật bệnh án sang tiếng Anh nộp bảo hiểm toàn cầu (Cigna, Allianz).│
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes                  │
│                     [x] Vinmec   [ ] Khác (Ghi rõ)________                  │
│                                                                             │
│ Ai đang đau (Actor)? Khách quốc tế (chờ đợi), Bác sĩ & Thư ký y khoa        │
│                                                                             │
│ Workflow thủ công hiện tại (5 bước):                                        │
│   1. Thu gom hồ sơ EMR tiếng Việt (chẩn đoán, xét nghiệm, mổ) sau ra viện   │
│   ──> 2. Gửi tài liệu scan sang đơn vị dịch thuật y khoa bên ngoài          │
│   ──> 3. Chờ công ty ngoài dịch thủ công (mất 3-5 ngày làm việc)            │
│   ──> 4. Bác sĩ Vinmec rà soát lại lỗi sai thuật ngữ y khoa lâm sàng        │
│   ──> 5. Ký đóng dấu bệnh viện và gửi chuyển phát cho bệnh nhân             │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2, 3 & 4 (⏱ Chờ 3-5 ngày, lỗi từ ngữ) │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3, 4                          │
│ (Trích xuất EMR -> Dịch thuật AI chuẩn MeSH/SNOMED -> Bác sĩ chỉ cần duyệt) │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│   - Rút ngắn thời gian bàn giao hồ sơ từ 3-5 ngày ──> dưới 30 phút (99%).   │
│   - Cắt giảm 85% chi phí dịch ngoài, tiết kiệm 350-500 triệu VND/tháng/BV.  │
│                                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM Feature  [ ] Agent         │
└─────────────────────────────────────────────────────────────────────────────┘
```

* **Lý do AI Fit:** LLM y khoa chuyên sâu vượt trội trong việc hiểu ngữ cảnh bệnh án tiếng Việt và dịch chuyển tự động sang danh mục thuật ngữ y khoa quốc tế chuẩn hóa (MeSH, SNOMED-CT, ICD-10), loại bỏ các lỗi dịch ngô nghê của các công ty dịch thuật thông thường. Ranh giới vận hành: Bản dịch AI bắt buộc gắn nhãn `[DRAFT_ONLY]` và yêu cầu Bác sĩ phụ trách hoặc Điều phối viên quốc tế của Vinmec ký xác nhận trước khi đóng dấu phát hành chính thức cho bệnh nhân (HITL 100%).

---

## 🗳️ Lựa chọn đề tài cho Deep-Dive (Phase 3)
* **Bài toán được ưu tiên lựa chọn:** **Quick Problem Card #1 — Soạn thảo Tóm Tắt Hồ Sơ Bệnh Án Xuất Viện (Vinmec Discharge Summary)**.
* **Lý do:** Bài toán giải quyết trực tiếp điểm nghẽn lớn nhất của đội ngũ bác sĩ tinh hoa tại Vinmec, có tác động giải phóng công suất giường bệnh ngay lập tức, và thể hiện rõ nét tư duy thiết lập **Operational Boundary (Human-in-the-loop y tế)** cực kỳ đắt giá trong bài đánh giá của môn học.

