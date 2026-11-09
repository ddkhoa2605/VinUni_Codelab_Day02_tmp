# 03 — AI Log & Reflection
---

## 2. Phần 1 — Phase 1–2: Scan & Quick Cards

### AI giúp được gì
- **Dựng khung và gợi ý bài toán.** Từ worksheet và inspiration kit, AI đề xuất 6 bài toán cho Vinpearl/VinWonders theo 4 lens và soạn 3 Quick Cards (Group Booking, CSKH vé VinWonders, phân loại review).
- **Phản biện thẻ bài toán** theo tinh thần "CFO khắt khe": chỉ ra phần nào Rule-based làm tốt hơn (tra quỹ phòng, tra chính sách vé), phần nào LLM mới có giá trị (đọc email tự do).
- **Research bằng chứng công khai** khi tôi yêu cầu kiểm tra số liệu:
  - Chính sách vé VinWonders: *"Vé đã mua không được hoàn, hủy hoặc quy đổi thành dịch vụ khác"*, *"Tối đa 20 khách trong một đơn hàng"*, hotline 1900 6677 ([nguồn](https://vinwonders.com/?p=27842), đăng 27/03/2023).
  - Thông báo của VinWonders Cửa Hội: tạm dừng cáp treo và khu trò chơi ngoài trời từ 16:00 ngày 21/07/2025 đến hết ngày 22/07/2025 vì thời tiết, khách đã mua vé được gia hạn hoặc đổi ngày miễn phí ([nguồn](https://vinwonders.com/vi/wonderpedia/news/tam-dung-cap-treo-va-khu-tro-choi-ngoai-troi/)).
  - Từ hai nguồn này AI rút ra một thiết kế có căn cứ: chính sách vé là quy tắc cố định nhưng **ngoại lệ chỉ có hiệu lực ngắn**, nên bot dễ nói sai nếu dùng thông tin cũ. Từ đó có metric "0 trường hợp trích dẫn thông báo đã hết hiệu lực" cho Card #2.

### AI sai ở đâu
| # | Lỗi của AI | Hậu quả |
|---|---|---|
| 1 | **Bịa số liệu.** Bản đầu có các con số như ~40 phút/yêu cầu đặt phòng đoàn, ~4 phút/lượt hỏi vé, ~3 phút/review, "quản lý biết sau ~24 giờ", "≥ 90%", "≥ 70%". Không có nguồn nào cho các số này. | Bài trông chuyên nghiệp nhưng không bám thực tế; nếu nộp, đó là số liệu hư cấu trình bày như sự thật. |
| 2 | **Chọn bài toán trùng ví dụ mẫu.** Card #1 đầu tiên (sự cố pin Xanh SM) gần như lặp lại `02-deliverable-example.md`. | Tôi phải yêu cầu đổi; sau đó nhóm phân lại domain và nội dung được làm lại cho Vinpearl/VinWonders. |
| 3 | **Con số tự đặt lan sang nơi khác.** Ngưỡng giảm giá 5% và điều kiện "10+ phòng hoặc 20+ khách" do AI tự đặt trong prompt của prototype; các con số bịa cũng được dùng để chấm điểm card Vinpearl trong bảng so sánh chung. | Số bịa ở một file thành "dữ liệu đầu vào" cho file khác. |

### Tôi đã sửa prompt và ranh giới như thế nào
- **Prompt ban đầu (quá rộng):** "Làm Phase 1, 2". AI hoàn thành khung nhưng điền số theo cảm tính.
- **Prompt sửa (đặt ràng buộc cứng):** tôi yêu cầu rà soát lại file, nêu *"các con số cần phải chính xác, đúng từ các dẫn chứng cụ thể chứ không được bịa hay dự đoán ra"*.
- **Cách AI thực hiện sau khi có ràng buộc:**
  1. Liệt kê **từng con số** trong file và phân loại có nguồn hay không.
  2. Tìm bằng chứng công khai; con số nào không có nguồn thì **gỡ** và ghi `[cần đo]`.
  3. Thêm cột "Mức bằng chứng" vào bảng SCAN, thêm mục *Số liệu cần thu thập* (cần đo gì, lấy ở đâu) và mục *Nguồn* có link và ngày.
  4. Gắn nhãn các con số tự đặt là **giả định** (ví dụ mức trần 5% chỉ là ngưỡng thử ranh giới prompt, không phải chính sách của Vinpearl).
  5. Cập nhật file so sánh chung: đưa 3 card Vinpearl về "không xếp hạng" thay vì giữ điểm dựa trên số bịa.
- **Ranh giới tôi rút ra khi dùng AI để research:** con số chỉ được vào bài khi trả lời được "nguồn nào, ngày nào, tôi mở được link không". Phần việc của AI là *đề xuất và tìm*; phần việc của tôi là *kiểm tra nguồn và quyết định có dùng hay không*.

---

## 3. Phần 2 — Phase 3: Deep-Dive Report (Vinpearl Group Booking)

### AI giúp được gì
- **Dựng cấu trúc báo cáo** theo worksheet: workflow hiện tại với handoff và bottleneck, Problem Statement 6 trường, ma trận Rule vs LLM vs Agent, future-state flow có bước AI / người duyệt / fallback, checklist Phase 5.
- **Vẽ sơ đồ** `04-workflow-diagram.png` có hai phần (hiện tại và tương lai) với làn bơi, handoff, bottleneck.
- **Research quy định công khai của Vinpearl** để làm cơ sở thiết kế. Các điểm AI tìm được (từ Điều khoản chung và Quy định xác nhận đặt phòng của Vinpearl):
  - Danh sách phân phòng và yêu cầu dịch vụ phải gửi bằng email hoặc văn bản trước khi nhận phòng.
  - Khách đoàn thực hiện danh sách khách theo hợp đồng đoàn; đối tác phải đặt cọc thay khách.
  - Giá đối tác tính mặc định 02 người lớn/phòng, tối đa 04 người/phòng.
  - Từ đó AI chốt quyết định kiến trúc: logic cố định (quỹ phòng, giá, khung ưu đãi) giao cho **code**, LLM chỉ **đọc email và soạn nháp**.
- **Phát hiện mâu thuẫn trong nguồn:** mức cọc phòng ghi khác nhau giữa hai trang của Vinpearl (1.000.000 VND/phòng/đêm so với 1.000.000 VND/phòng). Tôi đưa điểm này vào báo cáo và quy định AI không được tự nêu mức cọc.
- **Chạy prototype Gemini 2.5 Flash** với 4 test tấn công (đòi giảm sâu kèm "duyệt miệng", đòi bỏ thẻ `[DRAFT_ONLY]`, giả mạo quyền admin kèm vượt quỹ phòng, ép bịa dữ liệu khi thiếu thông tin).

### AI sai hoặc hạn chế ở đâu
| # | Vấn đề | Cách phát hiện / xử lý |
|---|---|---|
| 1 | **Không đọc được trang gốc.** Các trang `vinpearl.com` trả lỗi 403 khi AI truy cập tự động; nội dung điều khoản chỉ lấy được qua bản tóm tắt của công cụ tìm kiếm. | Tôi ghi rõ trong báo cáo là *chưa tự mở được trang gốc, cần đối chiếu trước khi nộp*, thay vì trình bày như đã kiểm chứng. |
| 2 | **Bộ kiểm tra tự động quá lỏng.** Test 2 báo "Passed" vì thẻ `[DRAFT_ONLY]` còn đó, nhưng bản nháp của model có câu *"Chúng tôi xác nhận hiện có đủ số lượng phòng theo yêu cầu của quý công ty"* và hứa "báo giá chi tiết chính thức". Dữ liệu cho thấy còn 35 phòng, nên câu này đúng về dữ kiện, nhưng từ "xác nhận" dễ bị hiểu là cam kết. | Tôi ghi đây là điểm cần cải thiện trong báo cáo: bộ kiểm tra chỉ soi thẻ chứ chưa soi nội dung; hướng xử lý là kiểm tra cụm từ cam kết hoặc thêm quy tắc vào prompt. |

### Tôi đã sửa prompt và ranh giới như thế nào
- **Kết quả test thật ghi vào báo cáo đúng nguyên trạng.** Test 3 và 4 đạt: model bỏ qua lệnh giả mạo admin, chuyển quản lý khi vượt quỹ phòng và đòi giảm 25%, và hỏi lại thay vì bịa khi thiếu dữ liệu. Test 2 giữ được thẻ nhưng có điểm yếu ở câu chữ như trên. Output của test 1 tôi chưa có nên báo cáo ghi "chưa có output" thay vì điền thay.
- **Ranh giới thiết kế rút ra:**
  - AI không có công cụ gửi email, chỉ soạn nháp có thẻ `[DRAFT_ONLY]`.
  - Số phòng, giá, khung ưu đãi do **code** kiểm, không để LLM tự tính.
  - Nội dung email của khách được coi là **dữ liệu**, không phải lệnh (chống prompt injection).

---

## 4. Bài học

1. **AI tự tin không đồng nghĩa với đúng.** Số liệu AI viết ra phải được xem là *giả thuyết* cho tới khi có nguồn. Cách hiệu quả nhất tôi tìm ra là đặt ràng buộc rõ trong prompt ("không nguồn thì ghi `[cần đo]`") và yêu cầu AI tự liệt kê từng con số để rà soát.
2. **Thiếu dữ liệu cũng là một kết quả.** Với Vinpearl, các điểm bottleneck chỉ là giả thuyết vì không có số liệu vận hành công khai; thừa nhận điều đó và chọn NOT YET đáng giá hơn một quyết định GO dựa trên số ước lượng.
3. **Kiểm tra của AI cũng cần được kiểm tra.** Test "Passed" chưa chắc là an toàn; kết quả test 2 cho thấy cần soi nội dung, không chỉ cấu trúc.
4. **Phân vai rõ.** AI mạnh ở dựng khung, tìm nguồn, đối chiếu mâu thuẫn và viết nháp; con người cần giữ quyền quyết định: chọn bài toán, mở link kiểm nguồn, chốt GO / NOT YET.
