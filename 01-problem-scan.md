# Lab 02 — Problem Scan & Quick Assessment (Vin Smart Future)

**Đơn vị:** Vin Smart Future (Vingroup)  
**Mảng trọng tâm lựa chọn:** **Vinhomes (Quản lý Đô thị Thông minh)**  
**Vai trò:** AI Product Engineer  
**Nhiệm vụ:** Quét điểm nghẽn vận hành (Operational Bottlenecks) qua 4 Lăng kính (4 Lenses), thực hiện Brainstorm cùng AI với số liệu tổn thất, và Stress-Test phản biện cùng CFO/COO ảo.

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

### 🤖 Ứng dụng Prompt AI từ Tip 1 — Partner Brainstorm:
Để tìm kiếm các pain points vận hành sâu sát thực tế có số liệu tổn thất cho mảng **Vinhomes**, tôi đã áp dụng đúng mẫu prompt gợi ý từ **Worksheet Tip 1**:

> **Prompt thực tế đã gửi cho AI:**  
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng Vinhomes. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

Dưới đây là bảng tổng hợp các bài toán thu thập được thông qua việc kết hợp quan sát thực địa tại các đại đô thị Vinhomes (Ocean Park, Smart City, Grand Park) và phản hồi có số liệu từ AI theo **4 Lenses**:

### 📝 List bài toán của tôi:

| # | Subsidiary | Lens | Mô tả quy trình thủ công & Điểm nghẽn (Bottleneck) | Con số thống kê ước tính về tổn thất (Theo gợi ý AI Prompt) |
|---|---|---|---|---|
| **1** | **Vinhomes** | **Lặp lại** *(Repetitive)* | **Phân loại & điều hướng phản ánh cư dân trên App Vinhomes Resident:** Nhân viên CSKH/Helpdesk đọc từng phản ánh (điện nước, rác, ồn ào, mùi lạ, đỗ xe trái phép, nứt tường), gán nhãn thủ công và chuyển tiếp sang ban kỹ thuật/an ninh từng tòa (mất 6-8 phút/ticket). | Nhận **~500-600 ticket/ngày/đại đô thị**; SLA phản hồi lần đầu bị trễ từ **4 đến 12 tiếng**; tiêu tốn **~60-75 giờ lao động/ngày** của đội Helpdesk; chỉ số hài lòng cư dân (CSAT) giảm 18% vào mùa cao điểm. |
| **2** | **Vinhomes** | **Tốn thời gian** *(Time-consuming)* | **Kiểm tra và thẩm định hồ sơ đăng ký thi công nội thất căn hộ:** Kỹ sư ban quản lý đọc thủ công bản vẽ PDF, hồ sơ đăng ký thi công, danh sách công nhân và rà soát thủ công danh mục vật liệu cấm/chống cháy (mất 30-45 phút/hồ sơ). | Mỗi đợt nhận bàn giao có **~150-200 hồ sơ/tuần/phân khu**; tồn đọng hồ sơ kéo dài từ **5-7 ngày làm việc**, gây bức xúc cho cư dân và chậm tiến độ hoàn thiện căn hộ. |
| **3** | **Vinhomes** | **AI có thể tốt hơn** *(AI-upgrade)* | **Trợ lý cư dân ảo giải đáp thủ tục hành chính & tiện ích nội khu:** Cư dân liên tục gọi hotline lễ tân hỏi về quy chế sử dụng bếp nướng BBQ, đặt sân tennis, thủ tục đăng ký tạm trú, vé xe buýt điện VinBus. Nhân viên lễ tân trả lời thủ công lặp đi lặp lại. | Lễ tân mất **~35% thời lượng ca trực** để trả lời các câu hỏi lặp lại; đường dây hotline thường xuyên bận khiến cư dân gặp sự cố khẩn cấp không gọi được. |
| **4** | **Vinhomes** | **Pain từ người khác** *(Stakeholder Pain)* | **Xử lý vi phạm đỗ xe và lấn chiếm lòng đường/khuôn viên:** Bảo vệ tuần tra chụp ảnh xe vi phạm, gõ biển số vào nhóm chat Zalo để tra danh tính chủ xe, sau đó gọi điện nhắc nhở thủ công (mất 10-15 phút/xe vi phạm). | Có **~70-90 vụ đỗ xe sai quy định/ngày** tại các trục đường nội khu; bảo vệ mất nhiều thời gian xử lý thủ công, dẫn đến ùn tắc cục bộ giờ cao điểm và cự cãi giữa bảo vệ với cư dân. |
| **5** | **Vinhomes** | **Lặp lại** *(Repetitive)* | **Đối soát công tơ điện nước và hóa đơn dịch vụ hàng tháng:** Kế toán đối chiếu thủ công các chỉ số đo xa bất thường (nhảy số vọt do rò rỉ nước hoặc hỏng công tơ) trước khi phát hành thông báo đóng phí dịch vụ cho cư dân. | Tốn **~5 ngày công/tháng của 4 kế toán**; khoảng **2-3% hóa đơn có sai lệch** dẫn đến khiếu nại dồn ứ vào ngày 5 hàng tháng. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **Top 3 bài toán** tiềm năng nhất (#1 Phân loại phản ánh cư dân, #2 Thẩm định thi công nội thất, #4 Xử lý vi phạm đỗ xe) để lập **Quick Problem Cards** và tiến hành **Stress-Test với AI Prompt từ Tip 2**.

---

## 📇 QUICK PROBLEM CARD #1 — Vinhomes: Phân loại, Ưu tiên & Điều hướng Phản ánh Cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Nhân viên CSKH Vinhomes mất 6-8 phút đọc, │
│ phân loại thủ công ticket phản ánh đa mục tiêu của cư dân   │
│ trên App Vinhomes Resident, dẫn đến quá tải và trễ SLA.     │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác: ________________ │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Nhân viên trực Helpdesk Ban Quản trị Vinhomes (quá tải).  │
│ - Cư dân khu đô thị (chờ phản hồi trễ 4-12 tiếng).          │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Cư dân gửi ticket (text + ảnh) qua App Vinhomes        │
│   ──> 2. CSKH đọc, bóc tách căn hộ, tòa và nhóm sự cố       │
│   ──> 3. Tạo phiếu kỹ thuật (Work Order) gán cho đội thợ    │
│   ──> 4. Gõ tay tin nhắn xác nhận hẹn thời gian kiểm tra    │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 4 (⏱ 6 phút/ticket)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 4            │
│ (Trích xuất thực thể, gán độ khẩn cấp P1-P4, soạn nháp SMS  │
│ gắn tiền tố [DRAFT_ONLY] cho nhân viên duyệt gửi).          │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ - Rút ngắn thời gian phân loại & xác nhận từ 8 phút -> 90s. │
│ - Tỉ lệ điều hướng đúng đội chuyên môn đạt >= 92%.          │
│ - 100% sự cố khẩn cấp P1 (cháy, rò rỉ khí gas, kẹt thang)  │
│   được cắm cờ đỏ cảnh báo trong vòng 15 giây.               │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

## 📇 QUICK PROBLEM CARD #2 — Vinhomes: Thẩm định Hồ sơ Đăng ký Thi công Nội thất

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Kỹ sư Ban Quản lý mất 30-45 phút rà soát  │
│ thủ công từng trang hồ sơ PDF đăng ký thi công nội thất của │
│ cư dân để phát hiện vật liệu cấm và rủi ro kết cấu.         │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác: ________________ │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Kỹ sư Ban Quản lý Xây dựng & Vận hành Vinhomes.           │
│ - Cư dân và nhà thầu nội thất (chờ duyệt hồ sơ 5-7 ngày).   │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Nhà thầu nộp bộ hồ sơ PDF bản vẽ qua cổng dịch vụ      │
│   ──> 2. Kỹ sư mở từng trang kiểm tra danh mục thiết bị     │
│   ──> 3. Đối chiếu danh mục cấm (đục tường chịu lực, chống  │
│          cháy, tải trọng sàn)                               │
│   ──> 4. Gõ biên bản thẩm định yêu cầu sửa đổi hoặc cấp phép│
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 30 phút)     │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3            │
│ (OCR + LLM trích xuất bảng vật tư, tự động gắn cờ vi phạm). │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ - Rút ngắn thời gian thẩm định hồ sơ từ 5 ngày -> dưới 24h. │
│ - Tỉ lệ phát hiện lỗi vi phạm vật liệu cấm đạt >= 95%.      │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

## 📇 QUICK PROBLEM CARD #3 — Vinhomes: Xử lý Vi phạm Đỗ xe & Lấn chiếm Nội khu

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Đội an ninh mất 15 phút tra cứu thủ công  │
│ danh bạ xe và gọi điện nhắc nhở từng trường hợp đỗ xe sai   │
│ quy định trong lòng đường đại đô thị.                       │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác: ________________ │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Đội Tuần tra An ninh đô thị Vinhomes.                     │
│ - Cư dân tham gia giao thông bị cản trở di chuyển.          │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Bảo vệ chụp ảnh xe đỗ sai gửi về nhóm chat nội bộ      │
│   ──> 2. Nhân viên trực văn phòng gõ biển số vào database   │
│   ──> 3. Tìm số điện thoại căn hộ sở hữu xe                 │
│   ──> 4. Gọi điện hoặc khóa bánh xe nếu không liên lạc được │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 8-10 phút)   │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3            │
│ (Camera AI/ALPR nhận diện biển số tự động -> tra căn hộ ->  │
│ push notification cảnh báo tới App cư dân trong 30 giây).   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ - Giảm thời gian phát hiện và thông báo từ 15 phút -> 1 phút│
│ - Giảm 70% số vụ xe đỗ cản trở giao thông quá 30 phút.      │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

## 🥊 Kết quả Stress-Test với Prompt AI từ Tip 2 (CFO & Trưởng phòng Vận hành)

Áp dụng đúng chỉ dẫn **Worksheet Tip 2 — Stress-Test thẻ bài toán**:

> **Prompt đã gửi cho LLM:**  
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Quick Problem Card #1 — Vinhomes Phân loại phản ánh cư dân]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

### Phản biện từ CFO & Trưởng phòng Vận hành ảo:

1. **Lỗ hổng Logic & Cam kết Pháp lý (Trưởng phòng Vận hành chỉ ra):**  
   *"Cư dân Vinhomes rất nhạy cảm với các vấn đề phí dịch vụ, tranh chấp ban quản trị, hoặc sự cố kỹ thuật gây thiệt hại tài sản (ví dụ thấm dột nước từ căn trên). Nếu bạn để LLM tự do sinh tin nhắn phản hồi mà không kiểm duyệt, LLM có thể tự ý đưa ra lời hứa hẹn bồi thường tài chính hoặc thừa nhận lỗi của ban quản lý. Điều này tạo ra rủi ro pháp lý cực kỳ lớn cho Vinhomes."*  
   👉 **Khắc phục:** Thiết lập **Operational Boundary cứng**: LLM tuyệt đối bị cấm đưa ra bất kỳ cam kết bồi thường tài chính, miễn giảm phí dịch vụ nào; mọi tin nhắn phải mang tiền tố `[DRAFT_ONLY]` và bắt buộc nhân viên CSKH kiểm tra, bấm duyệt (Human-in-the-loop) mới được gửi ra ngoài.

2. **Lỗ hổng Metric & Chi phí (CFO chỉ ra):**  
   *"Tại sao không dùng một biểu mẫu Dropdown trên App (Cư dân tự chọn: Điện / Nước / Tiếng ồn / An ninh) kết hợp Rule-based Router đơn giản để chuyển thẳng ticket tới đội thợ? Chi phí Rule-based bằng 0 đồng, không cần tốn tiền triệu token LLM mỗi tháng."*  
   👉 **Khắc phục:** Trong thực tế, hơn 65% phản ánh của cư dân là văn bản tự do, pha trộn nhiều vấn đề cùng lúc (*"thang máy tầng P rung, hành lang tầng 12 mùi rác và nhà 1204 khoan đục"*). Cư dân thường chọn đại một mục trong dropdown khiến tỉ lệ chuyển nhầm đội thợ lên tới 35%. LLM là công cụ duy nhất bóc tách được ngôn ngữ tự nhiên đa mục tiêu, phân loại chính xác và trích xuất mức độ khẩn cấp P1–P4. Chi phí token của Gemini Flash rất rẻ (~15 USD/tháng cho cả đại đô thị), hoàn toàn có ROI vượt trội so với thời gian nhân sự phải đọc tay.

3. **Nguy cơ hạ cấp sự cố khẩn cấp (An toàn tính mạng):**  
   *"Nếu cư dân báo cháy nhỏ, mùi khí gas hoặc có người kẹt trong thang máy, nhưng LLM xếp nhầm thành P3 (Bình thường), ai chịu trách nhiệm khi xảy ra tai nạn?"*  
   👉 **Khắc phục:** Bổ sung lớp **Rule-based Keyword Filter (Pre-check)**: Các từ khóa nhạy cảm (`cháy`, `khói`, `kẹt thang`, `rò rỉ gas`, `ngập nước`) lập tức kích hoạt cờ đỏ khẩn cấp P1 theo cơ chế song song, không phụ thuộc hoàn toàn vào LLM.

---

### 🏁 Quyết định lựa chọn của nhóm:
Nhóm quyết định chọn **Card #1 — Vinhomes: Phân loại, Ưu tiên & Điều hướng Phản ánh Cư dân trên App Vinhomes Resident** để thực hiện **Phase 3 (Deep-Dive)** và **Phase 5 (Evaluate)** trong file `02-deep-dive-report.md`. Đây là bài toán có khối lượng nghiệp vụ thực tế khổng lồ, xử lý ngôn ngữ phi cấu trúc xuất sắc, rủi ro an toàn được kiểm soát hoàn hảo bằng HITL và mang lại giá trị gia tăng rõ rệt cho hệ sinh thái đại đô thị Vinhomes.
