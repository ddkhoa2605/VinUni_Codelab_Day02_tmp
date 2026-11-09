# 🤖 03 — AI Interaction Log & Reflection

**Dự án:** Vinhomes Smart Resident Dispatcher | **AI Partner:** Gemini 2.5 Flash

---

### 1. AI Giúp gì? (What Helped)
* **Brainstorm số liệu (Tip 1):** Định lượng rõ tổn thất tại đại đô thị Vinhomes (~500–600 ticket/ngày, trễ SLA 4–12 tiếng, tốn 60–75 giờ công/ngày).
* **Phản biện đa chiều (Tip 2):** Đóng vai CFO & COO chỉ ra 3 điểm yếu chí mạng: rủi ro pháp lý nếu tự ý nhận lỗi/hứa bồi thường, lãng phí chi phí so với Dropdown Menu, và nguy cơ hạ cấp sự cố khẩn cấp P1.

### 2. AI Sai gì? (Where AI Failed)
* **Ảo giác quy trình:** Đề xuất tự động điều thợ mở cửa căn hộ cư dân — vi phạm nghiêm trọng quyền riêng tư và an ninh tòa nhà.
* **Mất ranh giới an toàn (Sycophancy):** Khi bị người dùng gây áp lực ở prompt tấn công, AI tự ý xóa tiền tố `[DRAFT_ONLY]` để gửi thẳng tin nhắn chưa qua duyệt.

### 3. Kỹ sư Sửa gì? (How I Fixed)
* **Thiết lập Operational Boundary cứng:** Cấm tuyệt đối hứa hẹn tài chính; buộc 100% tin nhắn mở đầu bằng `[DRAFT_ONLY]` để khóa nút gửi tự động (bắt buộc Human-in-the-loop duyệt).
* **Tối ưu kỹ thuật Prompt:** Khóa `[RULE 1]`, `[RULE 2]` chặt chẽ trong System Instruction và đặt `temperature=0.0`.
* **Phối hợp Rule + LLM:** Chạy song song bộ lọc từ khóa cứng (`cháy`, `khói`, `kẹt thang`, `gas`) để báo động P1 trong 15s; LLM chỉ xử lý bóc tách ngôn ngữ tự nhiên.

### 4. Bài học cốt lõi (Key Takeaways)
1. **Problem First, AI Second:** Rule-based xử lý bộ lọc cứng và an toàn; LLM xử lý ngôn ngữ và hỗ trợ ra quyết định.
2. **Ranh giới an toàn là sống còn:** Không bao giờ để AI tự do phát ngôn ra môi trường bên ngoài mà thiếu kiểm duyệt của con người.
