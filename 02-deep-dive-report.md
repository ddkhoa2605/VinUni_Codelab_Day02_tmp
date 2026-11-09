# 02 — Báo Cáo Phân Tích Chuyên Sâu (Deep-Dive Report)
## Dự án: Vinmec Clinical Discharge Summary Assistant (Trợ lý Soạn thảo Tóm tắt Bệnh án Xuất viện)

---

## 🏛️ 1. Bối cảnh & Lý do lựa chọn bài toán

* **Đơn vị phát triển:** Vin Smart Future (Vingroup)
* **Khách hàng nội bộ:** Khối Vận hành Lâm sàng — Hệ thống Y tế Vinmec (Vinmec Healthcare System)
* **Người thực hiện:** Nguyễn Văn Minh (Branch: `nguyenvanminh`)

Trong hệ sinh thái Vinmec, thủ tục ra viện của bệnh nhân nội trú là một điểm nghẽn nghiêm trọng ảnh hưởng đến chất lượng dịch vụ chuẩn quốc tế (JCI) và hiệu suất khai thác giường bệnh. Bác sĩ nội trú hiện phải dành trung bình **25–35 phút cho mỗi ca xuất viện** chỉ để tra cứu thủ công qua hàng chục trang hồ sơ bệnh án điện tử (EMR), tổng hợp xét nghiệm máu, chẩn đoán hình ảnh (CT/MRI), thuốc đã dùng, sau đó gõ tay bản tóm tắt xuất viện (Discharge Summary) và hướng dẫn dùng thuốc tại nhà. 

Dự án này ứng dụng công nghệ **LLM Feature** để tự động trích xuất thông tin lâm sàng cốt lõi và soạn thảo bản nháp tóm tắt xuất viện chất lượng cao, giúp bác sĩ tiết kiệm thời gian mà vẫn đảm bảo 100% quyền kiểm soát và phê duyệt y khoa.

---

## 🏗️ 2. Quy trình Vận hành Hiện tại (Current-State Workflow)

Quy trình thủ công hiện đang áp dụng tại các khoa nội trú Vinmec:

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Quyết định   │ ──> │ Rà soát & gom│ ──> │ Gõ bản nháp  │ ──> │ Soạn đơn     │
│ cho xuất viện│     │ dữ liệu EMR  │     │ tóm tắt bệnh │     │ thuốc & dặn  │
│              │     │              │     │ án lâm sàng  │     │ dò tại nhà   │
│ Ai: Bác sĩ ĐT│     │ Ai: Bác sĩ ĐT│     │ Ai: Bác sĩ ĐT│     │ Ai: Bác sĩ ĐT│
│ ⏱ 3 phút     │     │ ⏱ 12 phút 🔴 │     │ ⏱ 12 phút 🔴 │     │ ⏱ 5 phút     │
│ In: Khám buồng│    │ In: EMR, PACS│     │ In: Dữ liệu  │     │ In: Dược thư │
│ Out: Y lệnh  │     │ Out: Note tay│     │ Out: Văn bản │     │ Out: Đơn thuốc│
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Bước 5       │
                                                               │ Ký duyệt và  │
                                                               │ giải phóng   │
                                                               │ giường bệnh  │
                                                               │ Ai: Trưởng K │
                                                               │ ⏱ 3 phút     │
                                                               └──────────────┘
🔴 = Bottlenecks (Bước 2 & Bước 3)
🔄 = Handoff giữa Bác sĩ điều trị ➔ Bác sĩ Trưởng khoa ➔ Điều dưỡng hành chính ➔ Thu ngân viện phí
⏱ Tổng thời gian xử lý thủ công: 35 phút/bệnh nhân.
```

---

## 📋 3. Problem Statement (Chuẩn 6-Field của Vin Smart Future)

| Trường thông tin (Field) | Nội dung chi tiết |
|:---|:---|
| **1. Actor / Operator** | **Bác sĩ điều trị nội trú (Attending Physician)** tại các chuyên khoa (Nội khoa, Ngoại khoa, Nhi khoa, Sản khoa) thuộc Hệ thống Y tế Vinmec. |
| **2. Current Workflow** | Bác sĩ ra y lệnh xuất viện ➔ Mở phần mềm EMR rà soát tiền sử bệnh, diễn biến lâm sàng 5-7 ngày nằm viện, chỉ số xét nghiệm, kết quả chẩn đoán hình ảnh ➔ Gõ thủ công văn bản tóm tắt quá trình điều trị ➔ Kê toa thuốc về nhà và viết lời dặn chế độ ăn/tập luyện ➔ In ấn, ký tay và gửi hồ sơ sang phòng Kế hoạch tổng hợp/Trưởng khoa duyệt. |
| **3. Bottleneck** | **Bước 2 & Bước 3 (mất 24 phút/hồ sơ):** Đọc quét dữ liệu phi cấu trúc từ nhiều tab phân hệ EMR và gõ tổng hợp văn bản tóm tắt y khoa vừa chính xác về mặt lâm sàng, vừa dễ hiểu cho người bệnh. |
| **4. Business Impact** | - Mỗi ngày toàn hệ thống Vinmec tiếp nhận ~250 lượt xuất viện, tiêu tốn **120–140 giờ công chuyên môn cao** chỉ cho việc hành chính.<br>- Chậm trễ giải phóng giường (bed turnover delay) từ 1.5 – 2 giờ/ca, khiến bệnh nhân mới nhập viện phải chờ ở khoa Cấp cứu hoặc phòng lưu trú.<br>- Chi phí cơ hội do bác sĩ bị quá tải giấy tờ, giảm thời gian thăm khám trực tiếp cho các ca bệnh nặng. |
| **5. Success Metric** | **1. Hiệu suất thời gian:** Rút ngắn thời gian soạn thảo tóm tắt xuất viện từ 35 phút xuống **dưới 5 phút/bệnh nhân** (Giảm ≥ 85% thời gian thủ công).<br>**2. Chất lượng & Tuân thủ:** Tỉ lệ bản draft được bác sĩ giữ nguyên hoặc chỉ chỉnh sửa nhỏ (< 10% từ ngữ) đạt **≥ 90%**.<br>**3. Tiêu chuẩn JCI:** 100% hồ sơ xuất viện có đầy đủ 6 trường thông tin bắt buộc theo quy định của Joint Commission International. |
| **6. Operational Boundary (Ranh giới vận hành sống còn)** | - **BẮT BUỘC TIỀN TỐ DRAFT `[DRAFT_ONLY]`:** Mọi đầu ra của AI chỉ được coi là bản nháp nội bộ. AI **TUYỆT ĐỐI KHÔNG ĐƯỢC PHÉP** tự động in ấn, gửi vào App MyVinmec của bệnh nhân hoặc đóng hồ sơ bệnh án nếu chưa có **chữ ký số xác nhận của Bác sĩ điều trị (Human-in-the-loop 100%)**.<br>- **RANH GIỚI KÊ ĐƠN THUỐC:** AI **KHÔNG ĐƯỢC TỰ Ý THAY ĐỔI** loại thuốc hoặc liều lượng đã được chỉ định trong đợt điều trị; chỉ được phép tổng hợp từ đơn thuốc gần nhất mà bác sĩ đã duyệt.<br>- **RANH GIỚI BẢO MẬT DỮ LIỆU Y TẾ:** Toàn bộ thông tin định danh cá nhân nhạy cảm (Tên, CCCD, Số điện thoại) phải được che (de-identification) qua cổng bảo mật nội bộ Vin Smart Future trước khi xử lý ngôn ngữ. |

---

## 🚀 4. Future-State Flow & Kiến Trúc AI Fit

### 4.1. Ma trận lựa chọn kiến trúc (AI-Fit Matrix)
* [ ] **Rule-based / State-machine:** Không phù hợp vì dữ liệu bệnh án là ngôn ngữ tự nhiên phi cấu trúc, văn phong ghi chép của mỗi bác sĩ khác nhau.
* [x] **LLM Feature (ĐƯỢC CHỌN):** Phù hợp nhất. LLM vượt trội trong việc đọc hiểu ngữ cảnh y khoa, tóm tắt diễn tiến dài ngày thành bản tóm tắt súc tích, trích xuất thực thể y khoa (thuốc, triệu chứng, chỉ số sinh tồn) theo khuôn mẫu cố định.
* [ ] **Autonomous Multi-Agent Loop:** Không áp dụng vì ngành y tế đòi hỏi tính tiền định (deterministic), minh bạch và có thể truy vết. Việc thả nổi cho Agent tự động lập kế hoạch và ra quyết định độc lập tiềm ẩn nguy cơ sai sót y khoa nghiêm trọng.

### 4.2. Quy trình Vận hành Tương lai (Future-State Flow)

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Bác sĩ bấm   │ ──> │ 🔵 AI trích  │ ──> │ 🔵 AI soạn   │ ──> │ 🟢 Bác sĩ    │
│ "Tạo tóm tắt │     │ xuất tự động │     │ thảo draft   │     │ review, sửa  │
│ xuất viện"   │     │ dữ liệu EMR  │     │ có nhãn      │     │ nhanh & ký số│
│              │     │ (Lab, Thuốc) │     │ [DRAFT_ONLY] │     │ (HITL)       │
│ ⏱ 5 giây     │     │ ⏱ 10 giây    │     │ ⏱ 15 giây    │     │ ⏱ 3 phút     │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Bước 5       │
                                                               │ Phát hành hồ │
                                                               │ sơ & giải    │
                                                               │ phóng giường │
                                                               │ ⏱ 1 phút     │
                                                               └──────────────┘
                                                                      │
                                                                      ▼
                                                               ↩️ Fallback Plan:
                                                               Nếu AI timeout (> 30s)
                                                               hoặc lỗi kết nối, hệ thống
                                                               bung form nhập liệu truyền thống
                                                               để bác sĩ gõ tay như cũ.
```

* **🔵 AI Steps:** Trích xuất tự động dữ liệu xét nghiệm bất thường, chẩn đoán ICD-10, tóm tắt quá trình điều trị, đề xuất chế độ chăm sóc tại nhà.
* **🟢 Human-in-the-loop (HITL):** Bác sĩ kiểm tra lại bản draft, chỉnh sửa nếu cần và thực hiện ký số.
* **↩️ Fallback Strategy:** Hệ thống lưu tự động bản lưu tạm (draft recovery), chuyển về giao diện EMR truyền thống nếu xảy ra sự cố mạng.

---

## 🏁 5. Đánh Giá Độ Sẵn Sàng (AI Readiness) & Quyết Định Cuối Cùng

### 5.1. Bảng kiểm độ sẵn sàng (AI Readiness Checklist):
1. **Dữ liệu mẫu sạch:** [x] **ĐẠT.** Vinmec đã chuẩn hóa hệ thống bệnh án điện tử EMR tập trung trên toàn hệ sinh thái, có sẵn hàng chục nghìn hồ sơ xuất viện mẫu đã được nghiệm thu đạt chuẩn JCI.
2. **Khả năng kiểm soát rủi ro:** [x] **ĐẠT.** Rủi ro y khoa được triệt tiêu hoàn toàn nhờ quy trình ký duyệt số bắt buộc của Bác sĩ điều trị (AI không bao giờ hành động tự chủ).
3. **Mức độ sẵn sàng của Stakeholders:** [x] **ĐẠT.** Đội ngũ bác sĩ và lãnh đạo bệnh viện rất mong muốn cắt giảm thủ tục hành chính để tập trung cứu chữa bệnh nhân.

---

### 5.2. Quyết định của Ban Giám Đốc Vin Smart Future:

# 👉 **QUYẾT ĐỊNH: GO (BẮT ĐẦU XÂY DỰNG PROTOTYPE)**

### 💡 Lý giải quyết định (Justification):
1. **Giá trị kinh tế và vận hành đo lường được ngay (High ROI):** Tiết kiệm **~120 giờ công/ngày** của các bác sĩ đầu ngành, tương đương cắt giảm chi phí vận hành hàng tỷ đồng mỗi năm; giảm thời gian xoay vòng giường bệnh thêm 1.5 giờ giúp Vinmec phục vụ thêm hàng trăm bệnh nhân nội trú mỗi tháng.
2. **Kiến trúc kỹ thuật tinh gọn, khả thi cao:** Ứng dụng LLM Feature kết hợp Prompt Engineering có cấu trúc JSON và hệ thống kiểm soát ranh giới (`[DRAFT_ONLY]`) không đòi hỏi huấn luyện lại mô hình nền tảng phức tạp, có thể triển khai thử nghiệm (PoC) trong vòng 2 tuần.
3. **Mức độ an toàn tuyệt đối:** Ranh giới vận hành chặt chẽ và cơ chế Human-in-the-loop bảo đảm không có bất kỳ rủi ro pháp lý hay y khoa nào đối với thương hiệu Vinmec.

