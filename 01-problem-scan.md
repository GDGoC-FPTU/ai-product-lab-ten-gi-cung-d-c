# 01 — Problem Scan (Bài cá nhân)

**Họ và tên:** [ĐIỀN TÊN CỦA BẠN]
**MSSV:** [ĐIỀN MSSV]

> Các bài toán bên dưới được chọn lọc từ `03-inspiration-kit.md` (mảng Ô Tô & Di Chuyển Xanh, Đô Thị, Y Tế).

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Xanh SM** | Tốn thời gian | Điều vận thông minh (Smart Dispatching): tối ưu điểm đón taxi điện dựa trên phân tích ngôn ngữ tự nhiên từ tin nhắn tài xế và tọa độ GPS thực tế — bao gồm cả tình huống pin nguy cấp cần điều hướng đến trạm sạc/xe cứu hộ pin. |
| 2 | **VinFast** | AI có thể tốt hơn | Trợ lý hướng dẫn trạm sạc thông minh: tự động đề xuất lịch trình sạc và trạm sạc trống phù hợp với loại cổng sạc (CCS2/GBT) của từng dòng xe (VF5, VF8, VF9). |
| 3 | **VinFast** | Lặp lại | Đối chiếu hóa đơn sạc điện đối tác: so khớp dữ liệu sạc điện hằng tuần từ hàng nghìn trụ sạc liên kết ngoài với hóa đơn thực tế gửi về hệ thống tài chính. |
| 4 | **Vinhomes** | Lặp lại | Phân loại & Điều hướng phản ánh cư dân: phân loại tự động các khiếu nại (mất nước, hỏng đèn, ồn ào) gửi qua App Vinhomes Resident đến đúng ban quản lý từng tòa nhà. |
| 5 | **Vinmec** | Tốn thời gian | Soạn thảo tóm tắt hồ sơ xuất viện (Discharge Summary): trích xuất thông tin lâm sàng từ bệnh án điện tử và ghi chú bác sĩ để soạn bản tóm tắt dễ hiểu cho bệnh nhân. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn top 3 từ danh sách SCAN: **#1 (Xanh SM — Điều vận/pin nguy cấp), #4 (Vinhomes — Phản ánh cư dân), #5 (Vinmec — Tóm tắt hồ sơ).**

## Card #1 — Xanh SM: Điều vận khi pin xe nguy cấp

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Tài xế báo pin nguy cấp (< 5%) giữa đường, điều   │
│ phối viên phải xác định trạm sạc phù hợp hoặc điều xe cứu   │
│ hộ pin di động trước khi xe cạn kiệt hoàn toàn.             │
│ Công ty thành viên: [x] Xanh SM                             │
│                                                             │
│ Ai đang đau (Actor)? Tài xế (rủi ro kẹt đường) và Điều      │
│ phối viên (quá tải giờ cao điểm)                            │
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│   1. Tài xế gọi báo sự cố ──> 2. Tra cứu GPS xe ──>         │
│   3. Tra cứu trạm sạc trống ──> 4. Soạn tin hướng dẫn       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (⏱ 10 phút/lượt)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4              │
│ (tự động tra trạm sạc + soạn nháp tin nhắn hoặc điều xe     │
│ cứu hộ pin nếu pin < 5% và trạm > 5km)                      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian xử lý sự cố từ 15 phút ──> dưới 3 phút.      │
│                                                             │
│ Quick Architecture: [x] LLM Feature                          │
└─────────────────────────────────────────────────────────────┘
```

## Card #2 — Vinhomes: Phân loại & điều hướng phản ánh cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Khiếu nại cư dân (mất nước, hỏng đèn, ồn ào) gửi  │
│ qua App Resident chưa được phân loại và định tuyến tự động. │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau (Actor)? Cư dân (chờ phản hồi) và ban quản lý   │
│ tòa nhà (xử lý thủ công số lượng lớn ticket)                │
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│   1. Cư dân gửi phản ánh ──> 2. Nhân viên đọc & phân loại   │
│   ──> 3. Chuyển đúng ban quản lý ──> 4. Ban quản lý xử lý   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ ~12 giờ/lượt)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3              │
│ (tự động phân loại loại sự cố + định tuyến đúng ban quản lý)│
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian định tuyến từ 12 giờ ──> dưới 2 giờ.         │
│                                                             │
│ Quick Architecture: [x] Rule + LLM Feature                   │
└─────────────────────────────────────────────────────────────┘
```

## Card #3 — Vinmec: Tóm tắt hồ sơ xuất viện

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Bác sĩ mất nhiều thời gian viết tóm tắt hồ sơ     │
│ xuất viện thủ công cho mỗi bệnh nhân.                       │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau (Actor)? Bác sĩ (quá tải), điều dưỡng (chờ hồ sơ)│
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│   1. Xem lại hồ sơ điều trị ──> 2. Tổng hợp chẩn đoán ──>   │
│   3. Viết tóm tắt xuất viện ──> 4. Duyệt & in hồ sơ         │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ 20-30 phút/ca) │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3              │
│ (soạn nháp tóm tắt từ dữ liệu hồ sơ điện tử, bác sĩ duyệt)  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian soạn tóm tắt từ 25 phút ──> dưới 8 phút.     │
│                                                             │
│ Quick Architecture: [x] LLM Feature (bắt buộc HITL duyệt)   │
└─────────────────────────────────────────────────────────────┘
```
