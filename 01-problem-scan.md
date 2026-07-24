# 01 — Problem Scan: AI Product Scoping (Vin Smart Future)

> **Bài cá nhân — Phase 1 (SCAN) & Phase 2 (QUICK-ASSESS)**

---

## 🏛️ Bối cảnh: Tôi là ai?

Tôi là AI Engineer tại **Vin Smart Future** (Vingroup). Nhiệm vụ của tôi là quét qua hoạt động vận hành của các công ty thành viên Vingroup, tìm kiếm các pain point có thể tối ưu hóa bằng trí tuệ nhân tạo, từ đó đề xuất các giải pháp AI khả thi nhất cho Ban Giám Đốc.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Dùng **4 Lenses** quét qua vận hành của các công ty thành viên Vingroup.

| # | Subsidiary (Công ty thành viên) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | **Xanh SM** | Tốn thời gian | Điều phối viên mất 15-20 phút/lượt xử lý thủ công sự cố tài xế báo pin yếu giữa đường: tra cứu vị trí GPS, tìm trạm sạc trống gần nhất, soạn tin nhắn chỉ dẫn đường đi cho tài xế. |
| 2 | **VinFast** | Lặp lại | Bộ phận tài chính phải so khớp thủ công hàng nghìn hóa đơn sạc điện từ các trạm sạc đối tác liên kết với dữ liệu nội bộ hệ thống mỗi tuần, dễ sai sót và tốn 2-3 ngày công/tuần. |
| 3 | **Vinhomes** | AI có thể tốt hơn | Hệ thống CSKH trên App Vinhomes Resident phản hồi cư dân bằng mẫu rập khuôn, mất trung bình 12 giờ để phân loại và route khiếu nại đến đúng ban quản lý tòa nhà. Cư dân phàn nàn về tốc độ xử lý chậm. |
| 4 | **Vinmec** | Pain từ người khác | Bác sĩ mất 20-30 phút/bệnh nhân để viết tóm tắt hồ sơ xuất viện (Discharge Summary), phải trích xuất thủ công từ bệnh án điện tử, xét nghiệm và ghi chú lâm sàng. Bác sĩ phàn nàn vì quá tải hành chính. |
| 5 | **Vinpearl** | Tốn thời gian | Bộ phận quản lý khách sạn phải đọc và phân tích thủ công hàng trăm review trên Booking.com, Agoda, Google Maps mỗi tuần để lọc phàn nàn khẩn cấp (phòng bẩn, thái độ nhân viên...), mất 8-10 giờ/tuần. |
| 6 | **VinFast** | AI có thể tốt hơn | Khách hàng gọi hotline mô tả lỗi xe bằng tiếng Việt đời thường (VD: "xe đi qua gờ giảm tốc kêu cụp cụp ở bánh trước"), nhân viên CSKH phải tra cứu thủ công để map sang mã lỗi kỹ thuật, mất 10-15 phút/cuộc gọi. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 từ danh sách SCAN: **#1 (Xanh SM Sự cố pin), #3 (Vinhomes CSKH), #4 (Vinmec Xuất viện).**

---

## Card #1 — Xanh SM: Xử lý sự cố tài xế báo pin yếu giữa đường

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Tài xế Xanh SM báo cáo pin yếu/hết pin  │
│ giữa đường, cần điều phối viên hỗ trợ tìm trạm sạc gần    │
│ nhất hoặc gọi xe cứu hộ pin di động.                        │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Điều phối viên (Dispatcher): quá tải vào giờ cao điểm     │
│ - Tài xế: phải chờ đợi lâu, mất cuốc, stress               │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tài xế gọi tổng đài điều vận báo hết pin               │
│   → 2. Dispatcher tra cứu vị trí GPS xe trên bản đồ nội bộ │
│   → 3. Dispatcher mở Dashboard trạm sạc VinFast tìm trụ    │
│         sạc trống phù hợp loại cổng sạc gần nhất            │
│   → 4. Dispatcher soạn tin nhắn hướng dẫn đường đi chi tiết │
│         gửi qua App tài xế                                   │
│   → 5. Gọi đội xe cứu hộ pin di động nếu pin dưới 5%       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 3-4 (⏱ 10-12 phút/lượt) — Tra cứu trạm sạc trống     │
│ phù hợp + Soạn tin nhắn hướng dẫn đường đi bằng tay.       │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 3-4: Tự động lấy vị trí GPS → Tra cứu API trạm sạc   │
│ trống → Soạn draft tin nhắn hướng dẫn đường đi.             │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ "Giảm thời gian xử lý sự cố từ 15 phút xuống dưới 3 phút" │
│ "Tỉ lệ chỉ dẫn đúng trạm sạc phù hợp đạt ≥ 98%"          │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
│ (LLM tự động soạn draft tin nhắn + tra cứu API trạm sạc)    │
└─────────────────────────────────────────────────────────────┘
```

---

## Card #3 — Vinhomes: Phân loại & Điều hướng phản ánh cư dân trên App

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Cư dân Vinhomes gửi khiếu nại/phản ánh  │
│ qua App nhưng hệ thống phân loại rập khuôn, mất 12h để     │
│ route đến đúng ban quản lý tòa nhà xử lý.                  │
│ Công ty thành viên: [x] Vinhomes                             │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Nhân viên CSKH Vinhomes: phải đọc + phân loại thủ công   │
│   hàng trăm phản ánh/ngày                                   │
│ - Cư dân: chờ phản hồi quá lâu (12h), mất niềm tin         │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Cư dân gửi phản ánh qua App Vinhomes Resident          │
│   → 2. Nhân viên CSKH đọc nội dung, phân loại thủ công     │
│         (mất nước, hỏng đèn, ồn ào, vi phạm nội quy...)    │
│   → 3. Chuyển tiếp phản ánh đến Ban quản lý tòa nhà        │
│         hoặc bộ phận kỹ thuật tương ứng                      │
│   → 4. Soạn tin nhắn phản hồi cho cư dân xác nhận đã tiếp  │
│         nhận                                                 │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2-3 (⏱ 8-12 phút/phản ánh) — Đọc hiểu nội dung       │
│ phản ánh viết tự do bằng tiếng Việt, phân loại đúng danh    │
│ mục và route đến đúng bộ phận xử lý.                        │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 2-3: LLM tự động phân loại phản ánh theo danh mục     │
│ + Route đến đúng ban quản lý + Draft tin nhắn phản hồi.     │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ "Giảm thời gian phản hồi cư dân từ 12 giờ xuống dưới       │
│  30 phút"                                                    │
│ "Tỉ lệ phân loại đúng danh mục phản ánh đạt ≥ 95%"        │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
│ (LLM phân loại văn bản tiếng Việt + auto-route)              │
└─────────────────────────────────────────────────────────────┘
```

---

## Card #4 — Vinmec: Soạn thảo tóm tắt hồ sơ xuất viện cho bác sĩ

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #4                                       │
│                                                             │
│ Bài toán (1 câu): Bác sĩ Vinmec mất 20-30 phút/bệnh nhân  │
│ để viết thủ công bản tóm tắt hồ sơ xuất viện (Discharge    │
│ Summary) từ nhiều nguồn dữ liệu lâm sàng rời rạc.          │
│ Công ty thành viên: [x] Vinmec                               │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Bác sĩ điều trị: quá tải hành chính, giảm thời gian      │
│   dành cho bệnh nhân                                         │
│ - Bệnh nhân: chờ lâu mới được xuất viện                     │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Bác sĩ mở hệ thống bệnh án điện tử (EMR), đọc lại    │
│      toàn bộ ghi chú lâm sàng, kết quả xét nghiệm, chẩn   │
│      đoán hình ảnh                                           │
│   → 2. Tổng hợp thủ công các thông tin quan trọng: chẩn    │
│         đoán, phác đồ điều trị, thuốc đã dùng, kết quả     │
│   → 3. Soạn thảo bản tóm tắt xuất viện bằng ngôn ngữ dễ   │
│         hiểu cho bệnh nhân và gia đình                       │
│   → 4. Kiểm tra lại, ký xác nhận và in/gửi cho bệnh nhân  │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 1-3 (⏱ 20-25 phút/bệnh nhân) — Đọc, tổng hợp từ     │
│ nhiều nguồn dữ liệu rời rạc và soạn thảo văn bản.          │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 1-3: LLM trích xuất tự động từ EMR → Tổng hợp →       │
│ Soạn draft bản tóm tắt xuất viện bằng ngôn ngữ dễ hiểu.    │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ "Giảm thời gian soạn tóm tắt xuất viện từ 25 phút xuống   │
│  dưới 5 phút"                                               │
│ "Tỉ lệ draft được bác sĩ chấp nhận không cần sửa đạt ≥85%"│
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
│ (LLM trích xuất + tổng hợp dữ liệu y tế, BẮT BUỘC bác sĩ │
│  phê duyệt trước khi gửi — Human-in-the-loop)               │
└─────────────────────────────────────────────────────────────┘
```
