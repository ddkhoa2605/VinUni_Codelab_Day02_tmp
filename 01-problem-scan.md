# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
> **Phạm vi:** Tập trung toàn bộ vào **VinFast** (bao gồm hạ tầng sạc do V-Green vận hành cho xe VinFast). Bối cảnh: VinFast bàn giao 177.697 ô tô điện tại Việt Nam trong 9 tháng đầu 2026 (VOV, 10/2026); mảng xe máy điện bàn giao 286.039 xe chỉ trong Q2/2026; mạng lưới gần 400 xưởng dịch vụ tại Việt Nam tính đến cuối 2025, chính sách bảo hành lên tới 10 năm.

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | VinFast (xưởng dịch vụ) | Tốn thời gian | Kỹ thuật viên/cố vấn dịch vụ phải tự đọc mã lỗi và log xe, tra tài liệu sửa chữa, rồi lập hồ sơ claim bảo hành gửi hãng. Hồ sơ thiếu thông tin bị trả lại, kéo dài thời gian xe nằm xưởng. *Ước tính: ~400 xưởng × 10 ca bảo hành/ngày × 20 phút tra cứu + lập claim ≈ 1.333 giờ/ngày ≈ 160 FTE.* |
| 2 | VinFast (CSKH / trợ lý chủ xe) | AI có thể tốt hơn | Chủ xe hỏi tổng đài/app các câu lặp lại: đèn cảnh báo trên màn hình nghĩa là gì, sạc ở đâu, đặt lịch xưởng, chính sách thuê/mua pin. Kịch bản trả lời rập khuôn, không đọc được trạng thái xe thực tế, nên phải chuyển tiếp nhiều lần. *Ước tính: mỗi 10.000 yêu cầu/ngày × 6 phút ≈ 1.000 giờ/ngày ≈ 125 tổng đài viên, trong đó ~60% là câu hỏi lặp.* |
| 3 | VinFast / V-Green (sạc) | Lặp lại | Đối soát thủ công các phiên sạc bị lệch (sạc dừng giữa chừng, sai kWh, trừ tiền trùng, chia doanh thu cho trạm nhượng quyền). Mạng lưới >150.000 cổng nên chỉ cần tỷ lệ lỗi nhỏ cũng thành khối việc lớn. *Ước tính: 100k phiên/ngày × 1% lỗi × 10 phút ≈ 167 giờ công/ngày ≈ 20 FTE.* |
| 4 | VinFast (hậu mãi / phụ tùng) | Pain từ người khác | Chủ xe, nhất là tài xế chạy dịch vụ (Limo Green, VF 3, Minio Green), phàn nàn xe nằm xưởng chờ phụ tùng. Lượng tồn kho tại từng xưởng do người lập theo kinh nghiệm, không bám theo số xe đang lưu hành và mẫu lỗi thực tế. *Ước tính: 1.000 xe dịch vụ chờ phụ tùng × 3 ngày × ~1 triệu đ thu nhập/ngày ≈ 3 tỷ đ thu nhập tài xế bị mất mỗi đợt, chưa kể chi phí xe/pin cho mượn.* |
| 5 | VinFast (nhà máy / PDI) | Lặp lại | Kiểm tra ngoại quan (sơn, khe hở, trầy xước) cuối dây chuyền và kiểm tra trước bàn giao (PDI) làm bằng mắt theo checklist, lặp lại trên từng xe. Lỗi lọt tới tay khách thành khiếu nại khi nhận xe. *Ước tính: ~20.000 xe/tháng × 6 phút ≈ 2.000 giờ/tháng ≈ 12 FTE chỉ cho khâu ngoại quan.* |

> **Lưu ý:** Các con số tổn thất là **ước tính dựa trên giả định** (VinFast không công bố số liệu vận hành nội bộ như số ca bảo hành, số cuộc gọi, tỷ lệ lỗi sạc). Công thức được ghi rõ để thay bằng số thật khi có dữ liệu. Dữ kiện công khai tham khảo: VOV và VietnamFinance (doanh số 2026), Mekong ASEAN (mạng lưới xưởng dịch vụ), VnEconomy (quy mô V-Green).

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

Top 3 được chọn: **#1 Claim bảo hành**, **#2 Trợ lý chủ xe**, **#3 Đối soát sạc**. Đây là các bài có nhiều xử lý văn bản/log nhất, nơi cần so sánh rõ Rule và LLM. Bài #4 (dự báo phụ tùng) và #5 (thị giác máy tính QC) là bài toán ML truyền thống, để dành cho vòng sau.

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Kỹ thuật viên mất nhiều thời gian chẩn đoán lỗi và│
│   lập hồ sơ claim bảo hành; hồ sơ thiếu thông tin bị trả lại│
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau? Kỹ thuật viên + cố vấn dịch vụ tại xưởng (trực │
│   tiếp); bộ phận duyệt bảo hành tại hãng; chủ xe chờ xe     │
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│   1. Tiếp nhận xe, ghi mô tả lỗi của khách                  │
│   ──> 2. Cắm máy chẩn đoán, đọc mã lỗi (DTC) + log xe       │
│   ──> 3. Tra tài liệu sửa chữa/bản tin kỹ thuật, xác định   │
│      nguyên nhân + linh kiện cần thay                       │
│   ──> 4. Lập claim bảo hành (mô tả, mã lỗi, ảnh, công lao   │
│      động) gửi hãng ──> 5. Chờ duyệt / bổ sung hồ sơ        │
│                                                             │
│ Bước tốn thời gian/lỗi nhất: Bước 3 + 4 (⏱ ~20 phút/ca);    │
│   claim thiếu thông tin bị trả lại → thêm 1–2 ngày          │
│ AI hỗ trợ ở đâu: Bước 3 (RAG trên tài liệu sửa chữa + lịch  │
│   sử ca tương tự → gợi ý nguyên nhân), bước 4 (soạn nháp    │
│   claim đúng mẫu, kiểm tra thiếu trường trước khi gửi)      │
│                                                             │
│ Metric:                                                     │
│   • Thời gian tra cứu + lập claim: 20 phút → dưới 7 phút/ca │
│   • Tỷ lệ claim bị trả lại do thiếu thông tin: đo baseline  │
│     → giảm 50%                                              │
│   • Gợi ý nguyên nhân đúng trong top-3: ≥ 80% (đối chiếu    │
│     kết luận cuối của kỹ thuật viên)                        │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
│   (LLM + RAG; kỹ thuật viên luôn là người quyết định)       │
└─────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Tổng đài/app trả lời chủ xe theo kịch bản rập     │
│   khuôn, không đọc được trạng thái xe, chuyển tiếp nhiều lần│
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau? Chủ xe (chờ máy, hỏi lại nhiều lần); tổng đài  │
│   viên (khối lượng câu hỏi lặp lớn)                         │
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│   1. Chủ xe gọi/nhắn (đèn cảnh báo, sạc, lịch xưởng, pin)   │
│   ──> 2. Tổng đài viên hỏi lại số VIN, mẫu xe, tình trạng   │
│   ──> 3. Tra kịch bản/FAQ, trả lời chung chung              │
│   ──> 4. Không giải quyết được → chuyển xưởng/kỹ thuật      │
│   ──> 5. Ghi nhận ticket thủ công                           │
│                                                             │
│ Bước tốn thời gian/lỗi nhất: Bước 2–4 (⏱ ~6 phút/cuộc;      │
│   ~60% là câu hỏi lặp lại)                                  │
│ AI hỗ trợ ở đâu: Bước 2–3. Trợ lý trên app nhận diện xe qua │
│   tài khoản, giải thích cảnh báo theo đúng mẫu xe, tìm trạm │
│   sạc, đặt lịch xưởng; chuyển người khi có dấu hiệu an toàn │
│                                                             │
│ Metric:                                                     │
│   • Tỷ lệ yêu cầu tự giải quyết không cần người: ≥ 50%      │
│   • Thời gian phản hồi đầu tiên: phút → dưới 10 giây        │
│   • 100% câu hỏi liên quan an toàn (pin quá nhiệt, mất phanh│
│     ...) được chuyển người/cứu hộ ngay — không ngoại lệ     │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [x] Agent │
│   (LLM cho hỏi đáp; Agent có giới hạn cho đặt lịch/tìm trạm)│
└─────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Nhân viên đối soát thủ công các phiên sạc bị lệch │
│   (dừng giữa chừng, sai kWh, trừ tiền trùng, chia doanh thu │
│   cho trạm nhượng quyền).                                   │
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [x] Khác: V-Green (vận hành│
│                                      trạm sạc cho VinFast)  │
│                                                             │
│ Ai đang đau? Kế toán/đối soát; chủ xe VinFast bị trừ sai    │
│   tiền; nhà đầu tư nhượng quyền chờ quyết toán              │
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│   1. Xuất log phiên sạc từ trụ + giao dịch thanh toán       │
│   ──> 2. Khớp từng dòng (Excel/SQL) ──> 3. Lọc dòng lệch    │
│   ──> 4. Tra nguyên nhân (log trụ, ticket khách, sự cố mạng)│
│   ──> 5. Hoàn tiền/điều chỉnh + cập nhật quyết toán         │
│                                                             │
│ Bước tốn thời gian/lỗi nhất: Bước 4 (⏱ ~10 phút/case lệch)  │
│ AI hỗ trợ ở đâu: Bước 2–3 dùng rule khớp tự động; bước 4    │
│   dùng phát hiện bất thường + LLM đọc log/ticket để đề xuất │
│   nguyên nhân và hướng xử lý                                │
│                                                             │
│ Metric:                                                     │
│   • Tỷ lệ phiên khớp tự động: đo baseline → ≥ 98%           │
│   • Thời gian xử lý mỗi case lệch: 10 phút → dưới 3 phút    │
│   • Thời gian quyết toán nhượng quyền: tháng → tuần         │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent │
│   (Rule cho 95%+ phần khớp; LLM chỉ cho phần ngoại lệ)      │
└─────────────────────────────────────────────────────────────┘
```

### 🧪 Kết quả stress-test (góc nhìn CFO / Trưởng phòng Vận hành)

| Card | Điểm yếu chính | Vì sao rule-based có thể đủ | Kết luận |
|---|---|---|---|
| #1 Claim bảo hành | Baseline 20 phút/ca và tỷ lệ claim bị trả lại chưa đo. Rủi ro LLM gợi ý sai nguyên nhân, kỹ thuật viên tin theo. Rủi ro gian lận bảo hành nếu AI "viết đẹp" claim. | Mapping mã lỗi → quy trình sửa có sẵn trong tài liệu; form claim bắt buộc đủ trường có thể chặn hồ sơ thiếu. | Rule đủ cho kiểm tra thiếu trường. LLM có giá trị ở chỗ mô tả lỗi của khách và ghi chú kỹ thuật là văn bản tự do, cần đối chiếu với nhiều tài liệu. AI chỉ gợi ý và soạn nháp, **không duyệt claim**. |
| #2 Trợ lý chủ xe | Rủi ro an toàn cao nhất: trả lời sai về cảnh báo pin/phanh có thể gây nguy hiểm. Metric "tự giải quyết" có thể bị đẩy lên bằng cách né chuyển người. | Cây FAQ + nút bấm trên app xử lý được phần lớn câu hỏi về trạm sạc, lịch xưởng. | Cần rule cứng ưu tiên trên LLM cho mọi từ khóa an toàn. Phải đo song song tỷ lệ khách hài lòng và tỷ lệ gọi lại trong 48 giờ. |
| #3 Đối soát sạc | Lý do dùng AI yếu nhất: giá trị chủ yếu nằm ở chuẩn hóa log và pipeline dữ liệu. | Khớp giao dịch là việc thuần rule-based. Đối soát tài chính phải xác định được và kiểm toán được. | LLM không được tự quyết hoàn tiền, chỉ gợi ý nguyên nhân cho ca ngoại lệ. Có thể làm phần rule trước, chưa cần AI. |

**→ Đề xuất mang sang Phase 3:** **Card #1 (Claim bảo hành)**. Người dùng là nội bộ (kỹ thuật viên), nên rủi ro thấp hơn so với trợ lý trả lời trực tiếp chủ xe. LLM thật sự hơn rule ở bước đọc mô tả lỗi tự do và đối chiếu tài liệu. Ranh giới vận hành rõ ràng: AI gợi ý và soạn nháp, con người chẩn đoán và hãng duyệt. Metric đo được ngay từ dữ liệu claim lịch sử.

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Ai đang thực hiện tác vụ hằng ngày? |
| **2. Current Workflow** | Mô tả tóm tắt quy trình thủ công hiện tại và công cụ sử dụng. |
| **3. Bottleneck** | Bước nào chậm, lỗi, hoặc cần xử lý ngôn ngữ tự động nhiều nhất? |
| **4. Business Impact** | Tổn thất thực tế đo bằng thời gian, chi phí, hoặc SLA của Vingroup. |
| **5. Success Metric** | AI giải quyết được thì đạt ngưỡng số mấy? (Ví dụ: *"85% vé được phân loại dưới 10s"*). |
| **6. Operational Boundary** | AI được phép làm gì, TUYỆT ĐỐI không được làm gì, điểm nào cần duyệt? |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Viết lý giải chi tiết tại đây*

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*