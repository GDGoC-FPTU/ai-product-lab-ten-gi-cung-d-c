# 03 — AI Log & Reflection: Nhật ký chiêm nghiệm AI

> **Bài cá nhân — Phase 6 (REFLECTION)**
>
> **Họ và tên:** [Điền tên của bạn]
> **MSSV:** [Điền MSSV]

---

## 🤖 1. AI giúp gì trong buổi Lab hôm nay?

Trong suốt buổi Lab, tôi đã sử dụng AI (Gemini, ChatGPT) làm **thought-partner** (trợ lý đồng hành tư duy) cho nhiều tác vụ khác nhau:

### a) Brainstorm ý tưởng bài toán (Phase 1 — SCAN)
Tôi dùng prompt sau để brainstorm các pain point vận hành cho Vingroup:

> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng Xanh SM và VinFast. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

**Kết quả:** AI đã gợi ý được 8 bài toán khá sát thực tế, trong đó bài toán "xử lý sự cố pin tài xế Xanh SM" là ý tưởng mà tôi chọn để phát triển tiếp. AI giúp tôi tiết kiệm khoảng 15-20 phút brainstorm so với việc tự nghĩ từ đầu.

### b) Viết System Prompt cho Prototype (Phase 4)
Tôi nhờ AI hỗ trợ viết System Prompt nghiêm ngặt cho dispatcher co-pilot của Xanh SM. AI giúp tôi cấu trúc lại các quy tắc ranh giới an toàn (Operational Boundaries) một cách rõ ràng và logic hơn, đặc biệt là cách diễn đạt Rule 1 (DRAFT_ONLY tag) và Rule 2 (Critical Battery Threshold) sao cho LLM tuân thủ chặt chẽ.

### c) Stress-Test ranh giới an toàn
Tôi sử dụng AI để nghĩ ra các prompt tấn công (adversarial inputs) nhằm kiểm tra xem ranh giới an toàn của System Prompt có bị phá vỡ hay không. AI gợi ý các kịch bản tấn công mà tôi chưa nghĩ tới, ví dụ: yêu cầu AI bỏ qua tag DRAFT_ONLY bằng cách giả vờ là lệnh từ quản lý cấp cao.

---

## ❌ 2. AI sai gì? (Hallucination & Lỗi logic)

### Lỗi 1: Hallucination về số liệu thống kê
Khi tôi hỏi AI về số lượng sự cố pin trung bình/ngày của Xanh SM tại Hà Nội, AI trả lời rất tự tin rằng *"theo báo cáo Q3/2025 của GSM, trung bình có 120 sự cố pin/ngày"*. Tuy nhiên, **con số này hoàn toàn bịa đặt** — AI không có quyền truy cập dữ liệu nội bộ của Xanh SM và không có "báo cáo Q3/2025" nào cả. Đây là hiện tượng **hallucination** điển hình: AI tự tin đưa ra thông tin sai lệch kèm nguồn trích dẫn không tồn tại.

**Hậu quả tiềm ẩn:** Nếu tôi sử dụng con số 120 sự cố/ngày vào báo cáo mà không kiểm chứng, toàn bộ phân tích Business Impact và ước tính ROI sẽ bị sai lệch, dẫn đến quyết định đầu tư sai.

### Lỗi 2: Đề xuất kiến trúc quá phức tạp
Ban đầu khi tôi mô tả bài toán xử lý sự cố pin, AI đề xuất sử dụng **Multi-Agent System** với 3 agent riêng biệt (Agent tra cứu GPS, Agent tra cứu trạm sạc, Agent soạn tin nhắn) phối hợp qua một Orchestrator. Giải pháp này quá phức tạp, tốn kém, và **không cần thiết** cho một quy trình có cấu trúc cố định 5 bước. Một LLM Feature đơn giản với System Prompt nghiêm ngặt đã đủ giải quyết bài toán.

---

## 🔧 3. Sửa đổi ra sao? (Điều chỉnh prompt & bổ sung ranh giới)

### Sửa lỗi Hallucination:
Tôi điều chỉnh prompt bằng cách thêm ràng buộc rõ ràng:

> *"Khi đưa ra con số thống kê, hãy ghi rõ đây là 'ước tính' hoặc 'giả định'. KHÔNG ĐƯỢC trích dẫn báo cáo hoặc nguồn dữ liệu mà bạn không chắc chắn tồn tại. Nếu không có dữ liệu, hãy nói thẳng 'Tôi không có dữ liệu thực tế cho số liệu này'."*

**Kết quả:** Sau khi điều chỉnh, AI bắt đầu sử dụng cách diễn đạt cẩn thận hơn như *"ước tính khoảng 60-100 sự cố/ngày (con số giả định, cần xác minh với team vận hành)"* thay vì đưa ra con số cụ thể giả mạo.

### Sửa lỗi kiến trúc phức tạp:
Tôi thêm ngữ cảnh và ràng buộc vào prompt:

> *"Bài toán này có quy trình cố định 5 bước, input/output rõ ràng. Hãy ưu tiên giải pháp ĐƠN GIẢN NHẤT có thể (LLM Feature hoặc Rule-based). CHỈ đề xuất Agent/Multi-Agent khi có bằng chứng rõ ràng rằng giải pháp đơn giản không đủ."*

**Kết quả:** AI chuyển sang đề xuất LLM Feature đơn giản, phù hợp hơn nhiều với quy mô và độ phức tạp thực tế của bài toán.

---

## 💡 4. Bài học rút ra

1. **AI là trợ lý, không phải chuyên gia:** AI rất giỏi brainstorm và cấu trúc ý tưởng, nhưng tuyệt đối không nên tin mù quáng vào số liệu thống kê mà AI đưa ra — luôn cần kiểm chứng với nguồn dữ liệu thực tế.

2. **Prompt càng cụ thể, output càng tốt:** Khi tôi chỉ nói "hãy đề xuất giải pháp AI", AI có xu hướng over-engineer (đề xuất Multi-Agent). Khi tôi thêm ràng buộc "ưu tiên giải pháp đơn giản nhất", output lập tức trở nên thực tế và khả thi hơn.

3. **Ranh giới an toàn cần được test bằng code:** Chỉ viết System Prompt trên giấy là chưa đủ. Việc lập trình Adversarial Test Cases bằng Python và chạy thử nghiệm trực tiếp (như Phase 4) mới thực sự chứng minh được ranh giới có vững hay không.
