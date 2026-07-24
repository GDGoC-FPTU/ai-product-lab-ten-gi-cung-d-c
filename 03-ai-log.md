# 03-ai-log.md

# AI Product Lab 02 – Reflection

**Họ và tên:** Trần Đức Bảo Trung
**MSSV:** 2A202601269

---

# Phase 6 – Reflection

## 1. AI đã giúp tôi những gì?

Trong buổi Lab, tôi sử dụng ChatGPT và Gemini như một **thought-partner** thay vì để AI làm toàn bộ bài tập.

Ở giai đoạn đầu, AI giúp tôi brainstorm các bài toán vận hành thực tế của các công ty thành viên Vingroup như Xanh SM, VinFast, Vinmec, Vinhomes và Vinpearl. Từ nhiều ý tưởng ban đầu, nhóm lựa chọn bài toán "AI hỗ trợ điều phối xe sạc lưu động cho tài xế Xanh SM khi xe điện sắp hết pin" vì có quy trình rõ ràng, dữ liệu đầu vào xác định và phù hợp để xây dựng Prompt Prototype.

Sau đó, AI hỗ trợ mô tả Current Workflow, xác định Bottleneck, đề xuất Future Workflow, xây dựng Problem Statement theo mô hình 6-field và gợi ý các chỉ số đánh giá (Success Metrics). AI cũng hỗ trợ viết System Prompt, thiết kế Structured Output và xây dựng các Adversarial Test Cases để kiểm tra ranh giới vận hành của mô hình.

Ngoài ra, AI còn hỗ trợ giải thích sự khác nhau giữa Rule-based, LLM Feature và Agentic AI, giúp nhóm lựa chọn kiến trúc phù hợp với phạm vi của bài toán.

---

## 2. AI đã trả lời sai hoặc chưa hợp lý ở điểm nào?

Trong quá trình làm bài, AI đôi khi đề xuất giải pháp quá "thông minh" so với yêu cầu thực tế.

Ví dụ, AI từng đề xuất xây dựng một Agent tự động nhận dữ liệu GPS, tự điều xe sạc lưu động và gửi thông báo trực tiếp cho tài xế mà không cần người xác nhận.

Sau khi phân tích, nhóm nhận thấy giải pháp này không phù hợp vì:

* AI không nên tự động điều xe cứu hộ.
* Điều phối viên vẫn phải là người chịu trách nhiệm cuối cùng.
* Nếu AI dự đoán sai có thể gây ảnh hưởng trực tiếp đến vận hành thực tế.

Ngoài ra, AI cũng từng gợi ý sử dụng mô hình Machine Learning để dự đoán khả năng xe tới được trạm sạc. Tuy nhiên, với bài toán hiện tại chỉ cần sử dụng các quy tắc đơn giản (ví dụ pin dưới 5% và trạm sạc xa hơn 5 km) kết hợp với LLM để giải thích quyết định là đủ, không cần xây dựng mô hình học máy phức tạp.

---

## 3. Tôi đã điều chỉnh Prompt như thế nào?

Để AI hoạt động đúng phạm vi, tôi bổ sung nhiều ràng buộc trong System Prompt.

Cụ thể:

* AI chỉ đóng vai trò **hỗ trợ điều phối viên**, không được tự động gửi lệnh hay thực hiện hành động.
* Mọi phản hồi gửi cho tài xế phải bắt đầu bằng thẻ **[DRAFT_ONLY]** để thể hiện đây chỉ là bản nháp cần được con người phê duyệt.
* Nếu mức pin của xe dưới 5% và trạm sạc ở xa hơn 5 km thì AI phải đề xuất điều xe sạc lưu động, tuyệt đối không được hướng dẫn tài xế tiếp tục di chuyển.
* Nếu thiếu thông tin như vị trí GPS hoặc mức pin, AI phải yêu cầu bổ sung thay vì tự suy đoán.

Nhờ các ràng buộc này, kết quả của mô hình ổn định hơn và phù hợp với quy trình vận hành thực tế.

---

## 4. Bài học rút ra

Qua buổi Lab, tôi nhận thấy AI không thể thay thế hoàn toàn con người trong các quy trình vận hành quan trọng.

Giá trị lớn nhất của AI là hỗ trợ nhân viên đưa ra quyết định nhanh hơn, giảm thời gian xử lý và giảm các công việc lặp lại. Tuy nhiên, để hệ thống hoạt động an toàn cần xác định rõ phạm vi sử dụng, xây dựng các quy tắc vận hành (Operational Boundary), thiết kế Human-in-the-loop và chuẩn bị phương án Fallback khi AI không đủ tự tin hoặc trả lời sai.

Tôi cũng hiểu rằng việc viết Prompt tốt quan trọng không kém việc lựa chọn mô hình AI. Một Prompt có ràng buộc rõ ràng sẽ giúp giảm nguy cơ AI vượt quá quyền hạn và tạo ra kết quả đáng tin cậy hơn trong các hệ thống thực tế.
