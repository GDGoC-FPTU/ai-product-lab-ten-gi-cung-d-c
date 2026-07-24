# 02-deep-dive-report.md

# AI Product Lab 02 – Deep Dive Report

## Group Information


* **Tên nhóm:** Tên gì cũng được
* **Thành viên 1:** Trần Đức Bảo Trung - 2A202601269
* **Thành viên 2:** Hà Duy Anh - 2A200601511
* **Thành viên 3:** Đỗ Đức Trường - 2A200601499
* **Thành viên 4:** Trần Văn Hiếu - 2A200602030
* **Thành viên 5:** Vũ Việt Anh - 2A200601107
* **Thành viên 4:** Phạm Quốc Tuấn - 2A200601983

---

# Project Selected

## AI Mobile Charging Dispatcher for Xanh SM

### Problem Statement

Xây dựng hệ thống AI hỗ trợ điều phối viên Xanh SM ra quyết định xử lý khi xe điện sắp hết pin, giúp giảm thời gian xử lý và hạn chế trường hợp xe hết pin giữa đường.

---

# Phase 3.1 – Current State Workflow

## Current Workflow

```
Driver phát hiện pin yếu
        │
        ▼
Gọi tổng đài Xanh SM
        │
        ▼
Dispatcher hỏi vị trí GPS và % pin
        │
        ▼
Dispatcher mở Google Maps /
Hệ thống tìm trạm sạc
        │
        ▼
Dispatcher tự đánh giá
khoảng cách tới trạm
        │
        ▼
Nếu đủ pin → hướng dẫn tới trạm
Nếu không đủ → điều xe sạc lưu động
        │
        ▼
Thông báo tài xế
```

---

## Workflow Analysis

| Step              | Average Time |
| ----------------- | ------------ |
| Nhận cuộc gọi     | 1 phút       |
| Xác minh vị trí   | 2 phút       |
| Kiểm tra pin      | 1 phút       |
| Tìm trạm sạc      | 3 phút       |
| Đưa ra quyết định | 2 phút       |
| Tổng cộng         | **9 phút**   |

---

## Handoff

* Driver → Dispatcher
* Dispatcher → Navigation System
* Dispatcher → Mobile Charging Team

---

## Bottleneck

🔴 Dispatcher phải tự đánh giá:

* Pin còn bao nhiêu.
* Xe có tới được trạm hay không.
* Khoảng cách an toàn.
* Có nên gọi xe cứu hộ.

Đây là bước mất thời gian nhất.

---

# Phase 3.2 – Problem Statement (6 Fields)

| Field                    | Description                                                                                                                                                     |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Actor / Operator**     | Dispatcher Xanh SM                                                                                                                                              |
| **Current Workflow**     | Dispatcher tiếp nhận cuộc gọi, xác minh vị trí, kiểm tra pin, tìm trạm sạc và quyết định điều phối thủ công.                                                    |
| **Bottleneck**           | Đánh giá khoảng cách và khả năng xe tới được trạm sạc hoàn toàn dựa trên kinh nghiệm nhân viên.                                                                 |
| **Business Impact**      | Tăng thời gian xử lý, tài xế phải chờ lâu, có nguy cơ xe hết pin giữa đường gây gián đoạn dịch vụ.                                                              |
| **Success Metric**       | 95% yêu cầu được xử lý dưới **2 phút**, giảm thời gian từ **9 phút xuống dưới 2 phút**.                                                                         |
| **Operational Boundary** | AI chỉ được phép đề xuất phương án. Dispatcher phải là người phê duyệt cuối cùng. Nếu pin dưới 5% và trạm xa hơn 5 km thì AI phải đề xuất điều xe sạc lưu động. |

---

# Phase 3.3 – Future State Workflow

```
Driver gửi yêu cầu
        │
        ▼
AI nhận:
• GPS
• % pin
• Loại xe
        │
        ▼
🔵 AI đánh giá
Pin + khoảng cách
        │
        ▼
Đề xuất:

• Đi tới trạm sạc

hoặc

• Điều xe sạc lưu động
        │
        ▼
🟢 Dispatcher Review
        │
        ▼
Gửi hướng dẫn cho tài xế
```

---

## AI Fit Matrix

### Rule-based

Có thể kiểm tra:

* Pin < 5%
* Khoảng cách > 5 km

Ưu điểm

* Nhanh
* Chính xác

Nhược điểm

* Không giải thích được lý do.
* Không hỗ trợ giao tiếp với tài xế.

---

### LLM Feature ✅

LLM dùng để:

* Giải thích quyết định.
* Soạn tin nhắn cho tài xế.
* Hỏi thêm thông tin còn thiếu.
* Hỗ trợ Dispatcher.

---

### Agent

Chưa cần thiết.

Hệ thống chỉ cần AI hỗ trợ ra quyết định.

Không cần Agent tự hành.

---

## AI Classification

☐ Rule Only

☑ LLM Feature

☐ Agentic Loop

---

# Human in the Loop (HITL)

Dispatcher luôn là người phê duyệt cuối cùng trước khi:

* Điều xe cứu hộ.
* Điều xe sạc lưu động.
* Gửi hướng dẫn cho tài xế.

AI không được phép tự động thực hiện các hành động trên.

---

# Fallback Strategy

Nếu AI:

* Không xác định được vị trí.
* Không đọc được % pin.
* Không chắc chắn.

Thì hệ thống sẽ:

1. Yêu cầu Dispatcher nhập thủ công.
2. Hoặc chuyển sang quy trình điều phối truyền thống.

Không được phép tự ý suy đoán dữ liệu.

---

# Phase 5 – Evaluate

## AI Readiness Checklist

☑ Có dữ liệu GPS.

☑ Có dữ liệu phần trăm pin.

☑ Có dữ liệu vị trí trạm sạc.

☑ Có Human-in-the-loop.

☑ Có quy trình fallback.

☑ Stakeholder sẵn sàng thử nghiệm.

---

# Final Decision

☑ **GO**

Prototype được phép triển khai với phạm vi nhỏ.

---

# Justification

Nhóm lựa chọn GO vì bài toán có phạm vi rõ ràng, dữ liệu đầu vào xác định (GPS, mức pin, vị trí trạm sạc) và AI chỉ đóng vai trò hỗ trợ quyết định thay vì thay thế con người.

Chi phí triển khai thấp do chỉ cần tích hợp Gemini để phân tích và sinh phản hồi, kết hợp với dữ liệu GPS hiện có của Xanh SM. Quy trình vẫn đảm bảo Human-in-the-loop nên rủi ro khi AI đưa ra khuyến nghị sai được kiểm soát.

Kỳ vọng sau khi triển khai:

* Giảm thời gian xử lý từ khoảng **9 phút xuống dưới 2 phút**.
* Trên **95%** yêu cầu được xử lý đúng quy trình.
* Giảm nguy cơ xe điện hết pin giữa đường.
* Nâng cao trải nghiệm của tài xế và tối ưu hiệu quả điều phối.
