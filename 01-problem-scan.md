# 01 — Problem Scan & Quick Cards (Cá nhân)

> Lab 02 — AI Product Scoping · Vin Smart Future
> **Domain của tôi: Vinpearl / VinWonders** (lưu trú, nghỉ dưỡng, công viên giải trí).
> Gồm **Phase 1 (SCAN)** và **Phase 2 (QUICK-ASSESS)**. Các con số thời gian/khối lượng là **ước tính từ quan sát và suy luận hợp lý**, cần được xác thực bằng dữ liệu vận hành thật trước khi cam kết.

---

# 🔍 Phase 1 — SCAN

Quét vận hành của **Vinpearl** (khách sạn, resort) và **VinWonders** (công viên giải trí) bằng 4 lens: **Lặp lại**, **Tốn thời gian**, **AI có thể tốt hơn**, **Pain từ người khác**.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Vinpearl** | Tốn thời gian | Email đặt phòng theo đoàn (Group Booking) từ các công ty lữ hành dài, nhiều yêu cầu lẫn lộn; nhân viên sales phải đọc, trích xuất, tra quỹ phòng và soạn báo giá thủ công (~40 phút/yêu cầu). |
| 2 | **VinWonders** | AI có thể tốt hơn | Tổng đài/chat CSKH trả lời cùng một nhóm câu hỏi (giá vé, giờ mở cửa, trò chơi đang bảo trì, chính sách đổi/hoàn vé…) theo kịch bản rập khuôn, khách phải chờ máy hoặc hỏi lại nhiều lần. |
| 3 | **Vinpearl** | AI có thể tốt hơn | Review trên Booking/Agoda/Google Maps được tổng hợp thủ công; các phàn nàn khẩn cấp ("phòng bẩn", "nhân viên thái độ kém", "mất đồ") đến tay quản lý quá muộn, khách đã check-out. |
| 4 | **Vinpearl** | Lặp lại | Yêu cầu đặc biệt của khách gửi trước ngày lưu trú qua email/tin nhắn (nhận phòng sớm, giường phụ, ăn kiêng, trang trí sinh nhật) được lễ tân đọc và chuyển tay đến buồng phòng, bếp, F&B. |
| 5 | **VinWonders** | Pain từ người khác | Khách phàn nàn xếp hàng lâu, không biết nên chơi trò nào trước; nhân viên hiện trường bị hỏi đi hỏi lại về lộ trình, giờ biểu diễn, thời gian chờ. |
| 6 | **VinWonders** | Lặp lại | Cuối ca, trưởng khu vực viết báo cáo sự cố/bảo trì trò chơi thủ công từ nhiều nguồn (sổ ghi, tin nhắn nhóm) để gửi quản lý vận hành (~30 phút/ca/khu). |

**Top 3 được chọn cho Quick Cards:** #1 (Vinpearl — Group Booking), #2 (VinWonders — trợ lý CSKH vé & thông tin), #3 (Vinpearl — phân loại review & cảnh báo khẩn cấp).

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

## Card #1 — Vinpearl: Soạn báo giá cho yêu cầu đặt phòng theo đoàn

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Hỗ trợ nhân viên sales Vinpearl đọc email │
│ đặt phòng đoàn và soạn NHÁP phản hồi báo giá nhanh, đúng    │
│ quỹ phòng và đúng chính sách giảm giá.                      │
│ Công ty thành viên: [x] Khác: Vinpearl                      │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên sales/đặt phòng đoàn (quá    │
│ tải email), công ty lữ hành (chờ báo giá lâu, dễ chuyển     │
│ sang đối thủ).                                              │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Nhận email đoàn từ công ty lữ hành ──> 2. Đọc và ghi   │
│   tay ngày/số phòng/số khách/yêu cầu đặc biệt ──> 3. Tra    │
│   quỹ phòng trống + giá trên hệ thống ──> 4. Soạn email     │
│   báo giá, áp mức giảm theo chính sách ──> 5. Trao đổi qua  │
│   lại điều chỉnh, xin quản lý duyệt nếu khách đòi giảm sâu  │
│                                                             │
│ Bước tốn thời gian/lỗi nhất? Bước 2–4 (⏱ ~30 phút/yêu cầu, │
│ tổng ~40 phút/yêu cầu; dễ sai số phòng hoặc hứa vượt mức    │
│ giảm giá cho phép)                                          │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 và 4: trích    │
│ xuất yêu cầu có cấu trúc và soạn nháp email; sales kiểm     │
│ tra, sửa rồi mới gửi. Bước 3 vẫn dùng dữ liệu hệ thống.     │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Giảm thời gian từ nhận email đến có nháp báo giá từ       │
│   ~40 phút ──> dưới 5 phút;                                 │
│   ≥ 90% yêu cầu được trích xuất đúng ngày/số phòng/số khách;│
│   0 email có mức giảm > 5% khi chưa quản lý duyệt;          │
│   100% email có sales duyệt trước khi gửi.                  │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

**Stress-test (góc nhìn CFO / Trưởng vận hành) và phản hồi:**
- *Rule-based có đủ không?* Việc tra quỹ phòng, tính giá và áp trần giảm 5% là **logic cố định**, nên phải làm bằng hệ thống/code. LLM chỉ đáng dùng cho phần **đọc email tự do** và **viết nháp thân thiện**; trần 5% cần được kiểm lại bằng code, prompt chỉ là lớp bảo vệ thứ hai.
- *Điểm yếu metric:* "dưới 5 phút" và "~40 phút" là ước tính; cần đo baseline thật từ log thời gian phản hồi email trước khi cam kết.
- *Rủi ro:* AI hứa quá số phòng còn trống, bịa giá, hoặc đồng ý giảm sâu theo lời khách ("giám đốc đã duyệt miệng") → bắt buộc chỉ dùng dữ liệu hệ thống, mọi mức giảm > 5% phải chuyển quản lý, và AI không bao giờ tự gửi.

---

## Card #2 — VinWonders: Trợ lý CSKH về vé & thông tin công viên

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Tự động trả lời các câu hỏi lặp lại của   │
│ khách về giá vé, giờ mở cửa, trò chơi đang bảo trì, và      │
│ chuyển người thật khi liên quan đến tiền/khiếu nại.         │
│ Công ty thành viên: [x] Khác: VinWonders                    │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên tổng đài/chat CSKH (trả lời  │
│ trùng lặp), khách (chờ máy lâu, nhận thông tin cũ).         │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách gọi/nhắn hỏi ──> 2. CSKH tra bảng giá, lịch      │
│   hoạt động, thông báo bảo trì ──> 3. Soạn câu trả lời      │
│   ──> 4. Nếu liên quan đổi/hoàn vé thì chuyển cấp trên      │
│                                                             │
│ Bước tốn thời gian/lỗi nhất? Bước 2–3: tra nhiều nguồn      │
│ rời rạc, dễ trả lời sai giá/giờ (⏱ ~4 phút/lượt)            │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3: tra cứu từ  │
│ kho thông tin chính thức và soạn câu trả lời; câu hỏi về    │
│ hoàn tiền/khiếu nại chuyển thẳng cho người.                 │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Tự xử lý đúng ≥ 70% câu hỏi thông tin trong < 30 giây;    │
│   thời gian chờ trung bình giảm từ ~4 phút ──> < 1 phút;    │
│   0 câu trả lời sai giá vé/giờ mở cửa so với dữ liệu gốc.   │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

**Stress-test và phản hồi:**
- *Rule-based có đủ không?* Giá vé, giờ mở cửa, bảng trò chơi là **dữ liệu có cấu trúc**; tra bằng database/FAQ là đủ, LLM chỉ nên diễn đạt lại và hiểu câu hỏi tự do. → Kiến trúc **lai**: lấy dữ liệu bằng rule/API, LLM chỉ viết câu trả lời dựa trên dữ liệu đó.
- *Rủi ro:* LLM bịa giá hoặc giờ → câu trả lời phải trích từ nguồn chính thức; không được tự quyết định hoàn/đổi vé hay hứa bồi thường, chuyển người thật.

---

## Card #3 — Vinpearl: Phân loại review & cảnh báo phàn nàn khẩn cấp

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Tự động đọc review khách sạn trên các OTA │
│ và Google Maps, phân loại chủ đề/mức nghiêm trọng, và báo   │
│ ngay quản lý khi có phàn nàn khẩn cấp.                      │
│ Công ty thành viên: [x] Khác: Vinpearl                      │
│                                                             │
│ Ai đang đau (Actor)? Quản lý khách sạn/bộ phận trải nghiệm  │
│ khách (đọc review thủ công), khách (không được phản hồi).   │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Nhân viên mở từng nền tảng đọc review mới ──> 2. Gắn   │
│   nhãn chủ đề vào bảng tính ──> 3. Báo quản lý phàn nàn     │
│   nặng ──> 4. Soạn phản hồi công khai                       │
│                                                             │
│ Bước tốn thời gian/lỗi nhất? Bước 1–3: đọc rời rạc nhiều    │
│ nền tảng, báo muộn (⏱ ~1 ngày từ lúc review đến lúc quản lý │
│ biết; ~3 phút/review)                                       │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–4: phân loại   │
│ chủ đề + mức nghiêm trọng, cảnh báo tức thì, soạn NHÁP phản │
│ hồi để người duyệt.                                         │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Thời gian từ review đến lúc quản lý biết phàn nàn khẩn    │
│   cấp: ~24 giờ ──> < 1 giờ;                                 │
│   ≥ 90% phàn nàn khẩn cấp được gắn đúng nhãn (kiểm trên     │
│   bộ review đã gán nhãn tay);                               │
│   100% phản hồi công khai có người duyệt trước khi đăng.    │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

**Stress-test và phản hồi:**
- *Rule-based có đủ không?* Từ khóa ("bẩn", "mất đồ") bắt được ca rõ ràng nhưng bỏ sót review mỉa mai, tiếng Anh/Hàn/Trung hoặc viết lách → LLM có giá trị thật ở đây. Nên chạy thử song song với rule từ khóa để so sánh.
- *Rủi ro:* phản hồi công khai sai giọng điệu hoặc hứa đền bù có thể gây khủng hoảng truyền thông → AI chỉ soạn nháp, không tự đăng, không hứa bồi thường; sự cố an toàn/pháp lý chuyển quản lý ngay.
- *Vấn đề dữ liệu:* cần bộ review lịch sử đã gán nhãn để đo độ chính xác; nếu chưa có thì kết luận có thể là **NOT YET** cho tới khi gán nhãn đủ mẫu.

---

## 🗳️ Bài toán ưu tiên triển khai prototype

**Card #1 (Vinpearl — Group Booking)** được chọn cho Phase 4 vì:
- Đầu vào là văn bản tự do (phù hợp LLM) nhưng đầu ra có cấu trúc, đo được (thời gian, độ chính xác trích xuất).
- Có ranh giới rõ, kiểm thử được bằng prompt: không gửi khi chưa duyệt (`[DRAFT_ONLY]`), trần giảm giá 5%, không xác nhận vượt quỹ phòng.
- Rủi ro khi AI sai nằm trong tầm kiểm soát nhờ bước duyệt của sales (HITL) và quy tắc chuyển quản lý.
- Card #2 nên bắt đầu bằng tra cứu dữ liệu có cấu trúc (rule/API) trước khi thêm LLM; Card #3 cần bộ review đã gán nhãn để đo độ chính xác trước khi triển khai.
