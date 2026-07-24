# 01-problem-scan.md

# AI Product Lab 02 – Problem Scan

**Họ và tên:** Trần Đức Bảo Trung
**MSSV:** 2A202601269

---

# Phase 1 – SCAN

## Opportunity Scan

| # | Subsidiary | Lens             | Problem Description                                                                                                      |
| - | ---------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------ |
| 1 | Xanh SM    | Repetitive       | Điều phối viên phải trả lời nhiều cuộc gọi của tài xế khi xe sắp hết pin và tìm phương án sạc phù hợp.                   |
| 2 | VinFast    | Time-consuming   | Nhân viên kỹ thuật phải đọc hàng trăm báo cáo lỗi xe để phân loại nguyên nhân trước khi sửa chữa.                        |
| 3 | Vinmec     | AI-upgrade       | Bác sĩ mất nhiều thời gian đọc hồ sơ bệnh án dài trước khi khám bệnh.                                                    |
| 4 | Vinhomes   | Stakeholder Pain | Cư dân gửi phản ánh qua nhiều kênh (App, Hotline, Email) khiến bộ phận CSKH xử lý chậm và dễ bỏ sót.                     |
| 5 | Vinpearl   | AI-upgrade       | Khách hàng hỏi thông tin đặt phòng và dịch vụ nhiều lần, chatbot hiện tại chỉ trả lời theo mẫu nên trải nghiệm chưa tốt. |

---

# Phase 2 – QUICK ASSESS

# QUICK PROBLEM CARD #1

### Problem

AI hỗ trợ điều phối xe sạc lưu động cho tài xế Xanh SM khi pin xe điện ở mức nguy hiểm.

**Company**

☑ Xanh SM

### Actor

Điều phối viên (Dispatcher).

### Current Workflow

1. Tài xế gọi tổng đài báo pin yếu.

2. Điều phối viên hỏi vị trí và phần trăm pin.

3. Điều phối viên tìm trạm sạc gần nhất bằng bản đồ.

4. Điều phối viên đánh giá khoảng cách và hướng dẫn tài xế.

5. Nếu tài xế không thể tới trạm, điều phối xe sạc lưu động.

### Bottleneck

Việc đánh giá tình trạng pin và khoảng cách đến trạm sạc hoàn toàn thủ công.

**Thời gian trung bình:** 8–10 phút/lượt.

### AI Opportunity

AI phân tích mức pin, khoảng cách tới trạm và đề xuất:

* Hướng dẫn tới trạm sạc phù hợp.

hoặc

* Điều xe sạc lưu động nếu pin dưới ngưỡng an toàn.

### Success Metric

* Giảm thời gian xử lý từ **10 phút xuống dưới 2 phút**.
* Trên **95%** quyết định điều phối đúng quy tắc vận hành.

### Quick Architecture

☐ No AI

☐ Rule

☑ LLM

☐ Agent

---

# QUICK PROBLEM CARD #2

### Problem

AI tự động tóm tắt hồ sơ bệnh án cho bác sĩ Vinmec.

**Company**

☑ Vinmec

### Actor

Bác sĩ.

### Current Workflow

1. Mở hồ sơ bệnh án.

2. Đọc tiền sử bệnh.

3. Đọc kết quả xét nghiệm.

4. Ghi chú các thông tin quan trọng.

5. Bắt đầu khám.

### Bottleneck

Đọc hồ sơ mất nhiều thời gian.

**Thời gian:** khoảng 15 phút/bệnh nhân.

### AI Opportunity

LLM tóm tắt:

* Tiền sử bệnh.

* Dị ứng.

* Thuốc đang sử dụng.

* Kết quả xét nghiệm bất thường.

### Success Metric

Giảm thời gian đọc hồ sơ từ **15 phút xuống dưới 3 phút**.

### Quick Architecture

☐ No AI

☐ Rule

☑ LLM

☐ Agent

---

# QUICK PROBLEM CARD #3

### Problem

AI tự động phân loại phản ánh cư dân Vinhomes.

**Company**

☑ Vinhomes

### Actor

Nhân viên Chăm sóc khách hàng.

### Current Workflow

1. Nhận phản ánh.

2. Đọc nội dung.

3. Phân loại.

4. Chuyển bộ phận xử lý.

5. Theo dõi kết quả.

### Bottleneck

Phân loại thủ công dễ sai và chậm khi số lượng phản ánh lớn.

**Thời gian:** khoảng 6 phút/ticket.

### AI Opportunity

LLM phân loại nội dung:

* An ninh

* Kỹ thuật

* Vệ sinh

* Thanh toán

* Khác

Sau đó đề xuất bộ phận phù hợp.

### Success Metric

* 90% ticket được phân loại đúng.

* Thời gian giảm từ **6 phút xuống dưới 1 phút**.

### Quick Architecture

☐ No AI

☐ Rule

☑ LLM

☐ Agent

---

# Problem Selected For Deep Dive

Sau khi đánh giá mức độ khả thi, nhóm lựa chọn bài toán:

> **AI hỗ trợ điều phối xe sạc lưu động cho Xanh SM khi xe điện có mức pin nguy hiểm.**

### Lý do lựa chọn

* Quy trình nghiệp vụ rõ ràng.
* Có dữ liệu đầu vào cụ thể (mức pin, vị trí GPS, khoảng cách trạm sạc).
* AI đóng vai trò hỗ trợ ra quyết định, vẫn có Human-in-the-loop.
* Có thể xây dựng Prompt Prototype bằng Gemini.
* Có metric rõ ràng để đánh giá hiệu quả.
