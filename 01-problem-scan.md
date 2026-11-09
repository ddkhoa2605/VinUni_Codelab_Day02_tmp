# Problem Scan — Vin Smart Future × Xanh SM (GSM)

Tôi là **Truyền**, AI Engineer tại **Vin Smart Future**. Phạm vi khảo sát là vận hành taxi điện Xanh SM tại Việt Nam. Các nguồn công khai của GSM dùng tên **Green SM**.

## Phase 1 — SCAN

Các bước dưới đây là giả thuyết về phần việc nhân viên có thể đang làm thủ công khi gặp ca ngoại lệ. Nguồn công khai xác nhận kênh hoặc loại nghiệp vụ tương ứng. Cần xác minh quy trình, mức tự động hóa và điểm nghẽn với đội vận hành.

| # | Lens chính | Quy trình và điểm nghẽn giả định | Cơ hội ứng dụng AI và căn cứ công khai |
|---|---|---|---|
| 1 | Lặp lại | **Xác minh điểm đón khi đặt taxi qua tổng đài.** Tổng đài viên nghe mô tả như “cổng phụ bệnh viện”, dò bản đồ, hỏi lại cổng hoặc chiều đường rồi nhập điểm đón. Địa chỉ nói theo mốc dễ buộc nhân viên nhập lại và có thể khiến tài xế đến sai vị trí. | Nhận dạng giọng nói và trích xuất địa danh, sau đó dùng bản đồ để gợi ý điểm đón. Tổng đài viên xác nhận với khách trước khi tạo chuyến. [Hướng dẫn đặt taxi qua tổng đài Green SM](https://www.greensm.com/vn-vi/news/so-dien-thoai-tong-dai-taxi-xanh-sm-tren-toan-quoc-hotline-24-7) |
| 2 | Tốn thời gian | **Tra soát phản ánh bị trừ tiền hai lần.** CSKH thu mã chuyến và chứng từ, rồi phối hợp với nhóm thanh toán để so giao dịch với sổ chuyến. Ca thiếu mã tham chiếu hoặc có khoản tạm giữ khiến nhân viên phải tìm và đối chiếu thêm. | OCR trích trường từ ảnh biên nhận, quy tắc so khớp giao dịch từ nguồn có thẩm quyền. Nhân viên xác minh chênh lệch và duyệt kết luận. [Trung tâm giải đáp Green SM, mục 3.7](https://www.greensm.com/vn-vi/helps) |
| 3 | Pain từ người khác | **Tìm đồ khách bỏ quên khi thiếu mã chuyến.** CSKH thu mô tả món đồ, dò các chuyến theo thời gian và điểm trả, rồi liên hệ tài xế để kiểm tra. Khách có thể phải mô tả lại nhiều lần và tài xế mất thời gian xác minh. | Trích xuất mốc giờ, địa điểm và mô tả đồ vật từ hội thoại để lọc chuyến và xếp hạng ứng viên. CSKH xác minh danh tính trước khi phối hợp trả đồ. [Trung tâm giải đáp Green SM, mục 2.13](https://www.greensm.com/vn-vi/helps) |
| 4 | Lặp lại | **Rà soát hồ sơ ứng tuyển tài xế taxi trước phỏng vấn.** Nhân viên tuyển dụng đọc ảnh giấy phép lái xe, so với thông tin đăng ký, ghi nhận mục thiếu và gọi yêu cầu bổ sung. Ảnh mờ hoặc trường thông tin lệch khiến hồ sơ phải kiểm tra lại. | OCR đọc trường giấy phép, quy tắc đánh dấu ảnh khó đọc hoặc thông tin thiếu và lệch. Nhân viên kiểm tra ảnh gốc và quyết định hồ sơ đủ điều kiện. [Quy trình ứng tuyển tài xế taxi Green SM](https://tuyentaixe.xanhsm.com/taxi) |
| 5 | AI có thể tốt hơn | **Làm rõ yêu cầu sửa chữa ngoài lịch bảo dưỡng.** Với phiếu chỉ ghi “xe báo lỗi”, đầu mối đội xe hoặc xưởng phải đọc mô tả, xem ảnh cảnh báo và gọi lại hỏi điều kiện phát sinh trước khi chuyển kỹ thuật viên. Phiếu thiếu dữ kiện làm chậm bàn giao. | AI trích triệu chứng và mã cảnh báo từ ghi chú hoặc ảnh, rồi đề xuất câu hỏi bổ sung theo danh mục kỹ thuật. Kỹ thuật viên xác định mức độ khẩn và hướng xử lý. [Hướng dẫn đặt lịch bảo dưỡng và sửa chữa trên Green SM Driver](https://www.greensm.com/vn-vi/news/huong-dan-dat-lich-bao-duong-sua-chua-xe-qua-ung-dung-green-sm-driver-1) |

### Ước tính thời gian và chi phí tại điểm nghẽn

Kịch bản minh họa cho **một cụm vận hành trong một tháng**. Số lượt chỉ tính các ca thuộc phạm vi mô tả ở từng dòng. Khối lượng, phút xử lý và đơn giá **100.000 đồng/giờ công** đều là giả định để lập mô hình, chưa có số đo nội bộ. Khoảng thấp–cao phản ánh hai giả định về số phút làm việc trực tiếp tại điểm nghẽn, với khối lượng ca giữ cố định.

| # | Ca giả định/tháng | Phút thủ công/ca | Giờ công tại điểm nghẽn/tháng | Chi phí giờ công quy đổi/tháng |
|---|---:|---:|---:|---:|
| 1 | 1.200 cuộc đặt xe có điểm đón mơ hồ | 2–4 | 40–80 giờ | 4–8 triệu đồng |
| 2 | 360 phiếu nghi thu hai lần cần tra soát | 10–20 | 60–120 giờ | 6–12 triệu đồng |
| 3 | 240 phiếu đồ bỏ quên thiếu mã chuyến | 8–16 | 32–64 giờ | 3,2–6,4 triệu đồng |
| 4 | 600 hồ sơ cần rà soát giấy phép | 6–12 | 60–120 giờ | 6–12 triệu đồng |
| 5 | 180 phiếu sửa chữa thiếu mô tả triệu chứng | 10–20 | 30–60 giờ | 3–6 triệu đồng |

Giờ công = số ca × phút xử lý trực tiếp mỗi ca ÷ 60. Ví dụ, 360 phiếu tra soát × 10–20 phút ÷ 60 = 60–120 giờ. Cột chi phí quy đổi toàn bộ thời gian tại điểm nghẽn. Phần tiết kiệm thực tế là chênh lệch giữa hai luồng xử lý sau khi tính cả thời gian nhân viên kiểm tra gợi ý AI và xử lý ca ngoại lệ.

**Cách kiểm chứng.** Đếm ca đủ điều kiện trong 4 tuần theo mã cuộc gọi, phiếu hoặc hồ sơ. Đo phút làm việc trực tiếp ở đúng bước trong bảng bằng nhật ký thao tác hoặc bấm giờ trên mẫu có nhiều ca làm việc và mức độ phức tạp. Dùng khối lượng, thời gian trung bình và đơn giá nội bộ đo được để tính lại từng dòng.

## Phase 2 — QUICK-ASSESS

Chọn **#1, #2 và #4** để đánh giá trước. Cả ba có đầu ra đối chiếu được với dữ liệu gốc, lần lượt là điểm đón khách xác nhận, trạng thái giao dịch và trường giấy phép do nhân viên kiểm tra. Các mốc thời gian trước thử nghiệm lấy trung điểm của dải giả định ở Phase 1. Các mốc sau thử nghiệm là mục tiêu pilot.

### Card #1 — Xác minh điểm đón qua tổng đài

| Trường | Nội dung |
|---|---|
| Actor | Tổng đài viên đặt xe. Khách và tài xế chịu ảnh hưởng khi điểm đón sai. |
| Workflow giả định | Nghe khách mô tả → dò mốc trên bản đồ → hỏi lại và xác nhận điểm đón → nhập thông tin để tạo chuyến. |
| Bottleneck | Dò và xác nhận cổng hoặc chiều đường, khoảng **3 phút/ca**. |
| AI hỗ trợ | Nhận dạng giọng nói, trích mốc địa điểm và hiển thị các điểm đón phù hợp để tổng đài viên xác nhận với khách. Khi gợi ý thiếu chắc chắn, tổng đài viên tiếp tục tra cứu thủ công. |
| Metric | Giảm thời gian trung bình ở bước dò và xác nhận từ 3 xuống **≤2 phút/ca**, với **≥98%** điểm đón được nhập khớp điểm khách xác nhận trên mẫu kiểm tra. |
| Quick Architecture | Nhận dạng giọng nói + LLM trích xuất + tra cứu bản đồ. Tổng đài viên xác nhận điểm đón và tạo chuyến. |

### Card #2 — Tra soát nghi thu cước hai lần

| Trường | Nội dung |
|---|---|
| Actor | Nhân viên CSKH và nhân viên đối soát thanh toán. |
| Workflow giả định | Nhận phiếu và chứng từ → tìm chuyến và giao dịch liên quan → so mã, số tiền, thời điểm và trạng thái → xác minh kết luận và phản hồi. |
| Bottleneck | Đọc chứng từ và khớp với bản ghi giao dịch, khoảng **15 phút/phiếu**. |
| AI hỗ trợ | OCR trích số tiền, thời điểm và mã tham chiếu từ chứng từ đã che dữ liệu thẻ nhạy cảm. Quy tắc dùng mã giao dịch khi có, hoặc đưa danh sách cần kiểm tra khi chỉ khớp số tiền và thời điểm. Nhân viên xem bản ghi gốc khi thiếu hoặc trùng kết quả. |
| Metric | Giảm thời gian trung bình ở bước đọc và so khớp từ 15 xuống **≤8 phút/phiếu**, với **≥98%** kết quả so khớp đề xuất được xác nhận đúng và có đề xuất cho **≥70%** phiếu đủ điều kiện. Tính thời gian trên mọi phiếu pilot, kể cả phiếu xử lý thủ công. |
| Quick Architecture | OCR + Rule. Quyền duyệt kết luận và hoàn tiền thuộc người có thẩm quyền. |

### Card #4 — Rà soát giấy phép lái xe trong hồ sơ ứng tuyển

| Trường | Nội dung |
|---|---|
| Actor | Nhân viên tuyển dụng và ứng viên tài xế taxi. |
| Workflow giả định | Nhận hồ sơ → kiểm tra ảnh giấy phép → so với thông tin ứng tuyển và checklist → yêu cầu bổ sung hoặc chuyển bước phỏng vấn. |
| Bottleneck | Đọc ảnh, so trường và ghi nhận chỗ thiếu hoặc lệch, khoảng **9 phút/hồ sơ**. |
| AI hỗ trợ | OCR trích họ tên, hạng bằng và ngày hết hạn. Quy tắc đánh dấu trường thiếu hoặc lệch theo checklist hiện hành. Nhân viên xem ảnh gốc khi chữ mờ, độ tin cậy thấp hoặc có sai khác. |
| Metric | Giảm thời gian trung bình ở bước kiểm tra từ 9 xuống **≤5 phút/hồ sơ** và phát hiện **≥95%** hồ sơ thiếu hoặc lệch trường bắt buộc trên mẫu đã được tuyển dụng gán nhãn. |
| Quick Architecture | OCR + Rule. Nhân viên phê duyệt hồ sơ theo quy trình tuyển dụng. |

