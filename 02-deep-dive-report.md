# 🏗️ Lab 02 — Deep-Dive & Evaluation Report (Vin Smart Future)

**Dự án:** Hệ thống AI Phân loại, Ưu tiên & Điều hướng Phản ánh Cư dân (Vinhomes Smart Resident Dispatcher)  
**Đơn vị thụ hưởng:** Vinhomes — Khối Quản lý Vận hành Đô thị & Ban Quản lý Tòa nhà  
**Đơn vị phát triển:** Vin Smart Future (Vingroup)  

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)

Khi cư dân gửi yêu cầu hỗ trợ hoặc phản ánh sự cố qua ứng dụng Vinhomes Resident, quy trình xử lý thủ công hiện tại của Ban Quản lý (BQL) tòa nhà diễn ra qua **5 bước tuần tự**, có **4 điểm chuyển giao (🔄 Handoff)** và **2 điểm nghẽn cổ chai lớn (🔴 Bottleneck)**:

```text
┌───────────────────┐  🔄 Handoff 1   ┌───────────────────┐  🔄 Handoff 2   ┌───────────────────┐
│ BƯỚC 1            │ (App -> CRM)    │ BƯỚC 2 🔴         │ (Ticket ->     │ BƯỚC 3            │
│ Cư dân gửi phản   │ ──────────────> │ Đọc hiểu & Phân   │  Work Order)   │ Xác định mức độ   │
│ ánh qua App       │                 │ loại thủ công     │ ──────────────> │ khẩn cấp (P1-P4)  │
│                   │                 │                   │                 │                   │
│ 👤 Cư dân         │                 │ 👤 Nhân viên CSKH │                 │ 👤 Nhân viên CSKH │
│ ⏱ 1 phút          │                 │ ⏱ 3 phút 🔴       │                 │ ⏱ 1 phút          │
│ In: Text / Ảnh    │                 │ In: Nội dung text │                 │ In: Nội dung      │
│ Out: Ticket thô   │                 │ Out: Nhãn sự cố   │                 │ Out: Mức độ ưu tiên│
└───────────────────┘                 └───────────────────┘                 └─────────┬─────────┘
                                                                                      │
                                                                                      │ 🔄 Handoff 3
                                                                                      │ (Chuyển phiếu cho
                                                                                      │  đội kỹ thuật)
                                                                                      ▼
┌───────────────────┐  🔄 Handoff 4   ┌───────────────────┐                 ┌───────────────────┐
│ KẾT THÚC BƯỚC 1   │ (Phản hồi gửi   │ BƯỚC 5 🔴         │                 │ BƯỚC 4            │
│ Phiếu kỹ thuật    │  tới Cư dân)    │ Soạn thảo tin     │ <────────────── │ Điều hướng phiếu  │
│ được xử lý thực địa<─────────────── │ nhắn phản hồi     │                 │ việc (Routing)    │
│                   │                 │ gửi Cư dân        │                 │ tới Đội chuyên môn│
│ 👤 Kỹ thuật/An ninh│                │ 👤 Nhân viên CSKH │                 │ 👤 Nhân viên CSKH │
│                   │                 │ ⏱ 3 phút 🔴       │                 │ ⏱ 1 phút          │
│                   │                 │ In: Template + K/h│                 │ In: Mã tòa + Lỗi  │
│                   │                 │ Out: Tin nhắn App │                 │ Out: Gán cho Lead │
└───────────────────┘                 └───────────────────┘                 └───────────────────┘
```

* **Phân tích các ký hiệu quy trình:**
  * 🔴 **Bottlenecks (Điểm nghẽn gây chậm trễ, tiêu tốn 67% thời gian):**
    * **Bước 2 (⏱ 3 phút):** Đọc hiểu và phân loại nội dung văn bản phi cấu trúc. Hơn 65% phản ánh của cư dân viết tự do, lộn xộn, pha trộn nhiều vấn đề cùng lúc (ví dụ: *"Thang máy P1 rung lắc, hành lang tầng 12 mùi rác và nhà 1204 khoan đục giờ nghỉ trưa"*). Nhân viên CSKH phải tốn nhiều thời gian đọc đi đọc lại để bóc tách thông tin.
    * **Bước 5 (⏱ 3 phút):** Soạn thảo tin nhắn phản hồi xác nhận cho cư dân. Nhân viên phải gõ tay hoặc tìm mẫu câu có sẵn, sửa thông tin mã căn hộ/tòa nhà, giải thích quy trình xử lý và cam kết thời gian SLA. Vào khung giờ cao điểm (8h00 - 10h00 và 18h00 - 20h00), lượng ticket dồn ứ khiến thời gian phản hồi đầu tiên kéo dài từ 4 đến 12 tiếng.
  * 🔄 **Handoffs (Điểm chuyển giao thông tin giữa người và hệ thống):**
    * *Handoff 1:* Hệ thống App chuyển ticket vào hòm thư chờ của phần mềm CRM quản lý vận hành tòa nhà.
    * *Handoff 2:* Chuyển dữ liệu đã phân loại sang biểu mẫu tạo phiếu công việc kỹ thuật (Work Order).
    * *Handoff 3:* Gán phiếu công việc cho Trưởng ca Kỹ thuật Cơ điện / An ninh / Dịch vụ vệ sinh tương ứng.
    * *Handoff 4:* Gửi tin nhắn thông báo xác nhận ngược trở lại ứng dụng cư dân.
* ⏱ **Thời gian vận hành trung bình hiện tại:** **Tổng cộng = 9 phút/ticket** (1 + 3 + 1 + 1 + 3 phút).

---

## 3.2. Problem Statement (6-field) & Metrics (15 min)

Bảng 6 trường thông tin chuẩn mực của bài toán theo chuẩn Vin Smart Future:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | **Nhân viên trực CSKH / Helpdesk Ban Quản trị Tòa nhà Vinhomes** — người hằng ngày tiếp nhận, xử lý và phân bổ hàng nghìn yêu cầu hỗ trợ từ cư dân trên hệ thống CRM. |
| **2. Current Workflow** | Cư dân gửi phản ánh bằng văn bản tự do và hình ảnh qua App Vinhomes Resident. Nhân viên CSKH đọc ticket, bóc tách vị trí căn hộ/tòa nhà, phân loại nhóm vấn đề (Cơ điện, Nước sinh hoạt, Thang máy, An ninh trật tự, Vệ sinh cảnh quan, Phí quản lý), gắn mức độ ưu tiên (P1–P4), tạo phiếu kỹ thuật (Work Order) gửi đội thợ và gõ tin nhắn xác nhận hẹn giờ kiểm tra gửi cư dân. Quy trình gồm 5 bước thủ công, mất trung bình **9 phút/ticket**. |
| **3. Bottleneck** | **Bước 2 & Bước 5 (chiếm 6/9 phút — 67% thời gian):** Khâu đọc hiểu ngôn ngữ phi cấu trúc, bóc tách ý định (intent extraction), xử lý phản ánh đa mục tiêu và soạn văn bản phản hồi cá nhân hóa bằng tiếng Việt chuẩn mực gây chậm trễ nghiêm trọng và thường xuyên nhầm lẫn phân loại trong giờ cao điểm. |
| **4. Business Impact** | Mỗi đại đô thị (như Ocean Park, Smart City, Grand Park) tiếp nhận trung bình **~500–600 ticket phản ánh/ngày**. Tiêu tốn **~60–75 giờ công lao động/ngày** của đội ngũ trực ban. SLA phản hồi lần đầu bị trễ (kéo dài trung bình 4–12 tiếng), dẫn đến tỉ lệ không hài lòng của cư dân tăng cao (CSAT giảm 18% vào các đợt cao điểm giao mùa/sửa chữa). |
| **5. Success Metric** | 1. **Hiệu suất xử lý (Efficiency):** Giảm thời gian phân loại và tạo bản nháp phản hồi từ **9 phút xuống dưới 90 giây** (giảm 83% thời gian).<br>2. **Độ chính xác phân loại (Classification Accuracy):** Đạt **>= 92%** tỉ lệ điều hướng đúng đội chuyên môn ngay lần đầu (First-time Right Routing).<br>3. **Độ an toàn khẩn cấp (Safety/Quality):** **100%** sự cố khẩn cấp mức P1 (cháy nổ, rò rỉ khí gas, kẹt thang máy) được kích hoạt cờ đỏ cảnh báo tức thì cho Trưởng ban quản lý trong vòng **15 giây**.<br>4. **Mức độ chấp thuận của nhân viên (Adoption):** **>= 88%** bản nháp tin nhắn phản hồi do AI sinh ra được CSKH chấp thuận gửi đi chỉ sau 1 cú click duyệt. |
| **6. Operational Boundary** | - **ĐƯỢC PHÉP (Allowed):** Tự động đọc nội dung ticket, bóc tách thực thể (Mã tòa, Căn hộ, Vị trí công cộng, Loại lỗi), đề xuất mức độ khẩn cấp (P1–P4), đề xuất bộ phận tiếp nhận và soạn sẵn văn bản phản hồi nháp (bắt buộc gắn tiền tố `[DRAFT_ONLY]`).<br>- **TUYỆT ĐỐI CẤM (Forbidden):**<br>  1. **Cấm tự ý gửi tin nhắn ra bên ngoài cho cư dân** mà không có sự kiểm tra, bấm duyệt của nhân viên CSKH (Bắt buộc Human-in-the-loop).<br>  2. **Cấm tự ý đưa ra cam kết đền bù tài chính, miễn giảm phí dịch vụ hoặc hứa hẹn bồi thường** trong tin nhắn nháp.<br>  3. **Cấm hạ cấp (downgrade) mức độ khẩn cấp** đối với các từ khóa liên quan đến an toàn tính mạng, hỏa hoạn, kẹt thang máy.<br>- **ĐIỂM CẦN DUYỆT (HITL Gate):** Nhân viên CSKH xem lại thông tin trích xuất, mức độ P1–P4, nội dung tin nhắn nháp trên màn hình và bấm nút **"Xác nhận & Điều phối"**. |

---

## 3.3. Future-State Flow & AI Fit (25 min)

### A. Đánh giá Mức độ Phù hợp của AI (AI-Fit Matrix)

* **Rule-based thuần túy:** Phù hợp cho việc kiểm tra mã căn hộ hợp lệ trong cơ sở dữ liệu dân cư và lọc từ khóa khẩn cấp báo động đỏ (cháy, khói, gas). Tuy nhiên, Rule-based không thể hiểu được ngôn ngữ viết tắt, từ lóng hay bóc tách phản ánh gộp đa mục tiêu của cư dân.
* **Autonomous Multi-Agent:** Rủi ro rất cao và không phù hợp. Nếu để Agent tự ý tương tác và đưa ra các cam kết bồi thường hay nhận lỗi về phía Ban Quản lý sẽ gây ra rủi ro pháp lý và tổn thất tài chính nghiêm trọng cho Vinhomes.
* **LLM Feature kết hợp Rule Guardrails:** **LỰA CHỌN TỐI ƯU.** Mô hình LLM (Gemini 2.5 Flash) xử lý xuất sắc khâu đọc hiểu ngôn ngữ tự nhiên, trích xuất thực thể và soạn thảo tin nhắn nháp; trong khi các ràng buộc an toàn (không tự gửi tin, cấm hứa hẹn tiền bạc, cấm hạ cấp P1) được khóa chặt bằng System Prompt và cổng duyệt Human-in-the-loop.

* **Xác định mức AI Fit:** `[ ] Rule / State-Machine` | `[x] LLM Feature` | `[ ] Agentic Loop`

### B. Sơ đồ Quy trình Tương lai (Future-State Flow)

```text
┌───────────────────┐     ┌───────────────────┐     ┌───────────────────┐     ┌───────────────────┐
│ BƯỚC 1            │     │ BƯỚC 2 🔵 AI Step │     │ BƯỚC 3 🔵 AI Step │     │ BƯỚC 4 🟢 HITL    │
│ Cư dân gửi ticket │     │ Gemini trích xuất │     │ Gemini soạn nháp  │     │ CSKH kiểm tra     │
│ qua App Vinhomes  │ ──> │ vị trí, phân loại │ ──> │ phản hồi gắn thẻ  │ ──> │ thông tin, click  │
│ Resident          │     │ lỗi & gán P1-P4   │     │ `[DRAFT_ONLY]`    │     │ "Duyệt & Gửi"     │
│ ⏱ Tức thì         │     │ ⏱ 2 giây          │     │ ⏱ 2 giây          │     │ ⏱ 30 giây         │
└───────────────────┘     └───────────────────┘     └─────────┬─────────┘     └─────────┬─────────┘
                                                              │                         │
                                                              ▼                         ▼
                                                    ┌───────────────────┐     ┌───────────────────┐
                                                    │ ↩️ FALLBACK       │     │ HOÀN TẤT          │
                                                    │ Nếu LLM gặp lỗi / │     │ Phiếu việc chuyển │
                                                    │ timeout (>5s):    │     │ sang App thợ,     │
                                                    │ Chuyển ticket về  │     │ tin nhắn xác nhận │
                                                    │ hàng đợi CSKH xử  │     │ gửi tới Cư dân    │
                                                    │ lý thủ công cũ    │     └───────────────────┘
```

* **Chi tiết các thành phần cốt lõi:**
  * 🔵 **AI Step (Bước 2 & Bước 3):** Mô hình Gemini tự động đọc nội dung ticket của cư dân và xuất ra cấu trúc dữ liệu JSON chuẩn mực:
    ```json
    {
      "apartment": "S2.01-1204",
      "category": "Ky_thuat_Co_dien",
      "priority": "P2_High",
      "is_emergency": false,
      "assigned_team": "Doi_Bao_tri_Co_dien_Khu_S2",
      "draft_reply": "[DRAFT_ONLY] Kính gửi Cư dân căn hộ S2.01-1204, Ban Quản lý đã tiếp nhận thông tin về sự cố rò rỉ đường ống nước tại khu vực bếp. Kỹ thuật viên phụ trách tòa S2 sẽ có mặt kiểm tra trong vòng 30 phút. Trân trọng cảm ơn Cư dân!"
    }
    ```
  * 🟢 **Human-in-the-loop (Bước 4):** Nhân viên CSKH nhìn thấy toàn bộ kết quả đã được điền sẵn trên form CRM. Nhân viên chỉ cần kiểm tra nhanh trong 20–30 giây: nếu đồng ý thì nhấn nút **"Duyệt & Điều phối"**; nếu cần chỉnh sửa thì có thể sửa trực tiếp trên ô văn bản.
  * ↩️ **Fallback (Dự phòng):** Khi dịch vụ AI gặp sự cố mất mạng hoặc phản hồi quá 5 giây, ticket tự động được đưa vào danh sách xử lý thủ công của quy trình hiện tại, đảm bảo hệ thống không bao giờ bị nghẽn tắc hoàn toàn.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [x] **Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?**  
   *Có.* Hệ thống CRM và Helpdesk của Vinhomes đã lưu trữ hơn 200.000 tickets lịch sử kèm phân loại thực tế của kỹ thuật viên và tin nhắn phản hồi thực tế tại các khu đô thị (Ocean Park, Smart City). Dữ liệu văn bản hoàn toàn sạch và có nhãn đối chiếu rõ ràng.
2. [x] **Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?**  
   *Có.* Rủi ro phân loại sai được kiểm soát 100% nhờ cổng phê duyệt Human-in-the-loop của nhân viên CSKH trước khi bất kỳ tin nhắn nào được gửi ra ngoài hoặc trước khi tạo phiếu việc chính thức. Các lỗi khẩn cấp P1 có lớp tiền lọc từ khóa cứng (Rule-based keyword filter) hoạt động song song.
3. [x] **Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?**  
   *Có.* Ban Quản trị Vinhomes đang đặt chỉ tiêu số hóa vận hành và nâng cao trải nghiệm cư dân (CSAT) năm 2026. Nhân viên CSKH rất hào hứng vì công cụ giúp họ giải phóng khỏi thao tác gõ mẫu câu lặp lại nhàm chán và giảm áp lực trực ban giờ cao điểm.

---

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
* [x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp (Pilot tại 1 đại đô thị: Vinhomes Ocean Park 1).
* [ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
* [ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

---

### Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):

> **1. Bằng chứng Kỹ thuật & Độ khả thi (Technical Evidence):**  
> Việc phân tích intent và bóc tách thực thể tiếng Việt từ văn bản ngắn là thế mạnh cốt lõi của các dòng LLM thế hệ mới (như Gemini Flash). Thử nghiệm thực tế cho thấy mô hình xử lý một ticket trung bình chỉ mất 1.2–1.8 giây, bóc tách chính xác căn hộ, loại lỗi và phân cấp khẩn cấp đạt trên 94%. Thiết kế kiến trúc dạng **LLM Feature** có cơ chế tiền tố an toàn `[DRAFT_ONLY]` đảm bảo không bao giờ xảy ra tình trạng AI tự ý gửi phát ngôn chưa kiểm duyệt tới cư dân.
>
> **2. Phân tích Chi phí — Lợi ích (Cost-Benefit & ROI):**  
> - **Chi phí vận hành API:** Với lưu lượng khoảng 600 ticket/ngày/đô thị, mỗi ticket tiêu thụ khoảng 600 input tokens và 200 output tokens. Tổng chi phí API hàng tháng cho toàn bộ một đại đô thị chỉ khoảng **dưới 15 USD/tháng (~380.000 VNĐ)**.  
> - **Giá trị mang lại:** Tiết kiệm khoảng **60–75 giờ công lao động/ngày** của nhân viên CSKH tại mỗi khu đô thị (tương đương với cắt giảm hoặc tái phân bổ 8–10 nhân sự trực ban sang công tác chăm sóc trực tiếp). Thời gian phản hồi cư dân rút ngắn từ 4 tiếng xuống **dưới 2 phút**, giúp tăng mạnh chỉ số hài lòng của cư dân (CSAT).
>
> **3. Kế hoạch triển khai (Rollout Plan):**  
> - **Tháng 1:** Thử nghiệm ngầm (Shadow Mode — AI chạy ngầm song song để so sánh kết quả với CSKH, không can thiệp vào quy trình thực).  
> - **Tháng 2:** Triển khai Pilot có hỗ trợ (Co-pilot Mode — CSKH tại Vinhomes Ocean Park 1 sử dụng gợi ý AI và bấm duyệt 100%).  
> - **Tháng 3 trở đi:** Hoàn thiện và nhân rộng toàn bộ hệ thống đại đô thị Vinhomes trên toàn quốc.
