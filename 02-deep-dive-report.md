# 02 — Deep-Dive Report (Bài nhóm)

**Tên nhóm:** Ten gi cung dc

**Thành viên:**
| Họ và tên | MSSV |
|---|---|
| Trần Văn Hiếu | 02030 |
| Hà Duy Anh | 01511 |
| Phạm Quốc Tuấn | 01983 |
| Trần Đức Bảo Trung | 01269 |
| Đỗ Đức Trường | 01499 |
| Vũ Việt Anh | 01107 |

---

# 🗳️ Quyết định lựa chọn của nhóm

Nhóm chọn **Card #1 — Xanh SM: Điều vận khi pin xe nguy cấp** (từ `01-problem-scan.md`) để thực hiện Deep-Dive.

**Lý do lựa chọn và loại bỏ các thẻ khác:**
* **Card #2 (Vinhomes — Phản ánh cư dân):** Rủi ro thấp hơn nhưng cần tích hợp dữ liệu từ nhiều ban quản lý tòa nhà khác nhau, độ phức tạp tích hợp cao hơn so với giá trị mang lại trong phạm vi 1 buổi lab.
* **Card #3 (Vinmec — Tóm tắt hồ sơ):** Đây là mảng y tế nhạy cảm, đòi hỏi tuân thủ quy định pháp lý (HIPAA-like) và kiểm định lâm sàng kỹ hơn nhiều so với khả năng kiểm chứng trong phạm vi bài lab.
* **Card #1 được chọn vì:** Rủi ro vận hành rõ ràng (xe cạn pin giữa đường), ranh giới an toàn (Operational Boundary) dễ định nghĩa bằng luật cứng (ngưỡng pin & khoảng cách), và có thể lập trình + stress-test ngay bằng prompt prototype trong buổi lab.

---

# 🏗️ Phase 3 — DEEP-DIVE

## 3.1. Current-State Workflow

Quy trình xử lý sự cố pin nguy cấp thực địa hiện tại của điều phối viên Xanh SM:

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Nhận cuộc    │     │ Tra cứu định │     │ Tra cứu trạm │     │ Soạn tin     │
│ gọi/tin nhắn │ ──→ │ vị GPS xe    │ ──→ │ sạc VinFast  │ ──→ │ hướng dẫn    │
│ báo pin thấp │     │              │     │ còn trụ trống│     │ gửi tài xế   │
│ Ai: Dispatch │     │ Ai: Dispatch │     │ Ai: Dispatch │     │ Ai: Dispatch │
│ ⏱ 2 phút     │     │ ⏱ 2 phút     │     │ ⏱ 5 phút 🔴  │     │ ⏱ 5 phút 🔴  │
│ In: Điện thoại│     │ In: Biển số  │     │ In: Vị trí GPS│     │ In: Raw data │
│ Out: Log sự cố│     │ Out: Toạ độ  │     │ Out: Địa chỉ │     │ Out: Tin nhắn│
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Bước 5       │
                                                               │ Gọi xe cứu   │
                                                               │ hộ (nếu pin  │
                                                               │ quá thấp)    │
                                                               │ Ai: Dispatch │
                                                               │ ⏱ 1 phút     │
                                                               └──────────────┘
🔴 = Bottleneck   🔄 Handoff: Tài xế ──> Điều phối viên ──> Tài xế
⏱ Tổng thời gian xử lý thủ công: 15 phút/lượt.
```

## 3.2. Problem Statement (6-field)

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Điều phối viên (Dispatcher) thuộc Trung tâm Điều vận Xanh SM. |
| **2. Current Workflow** | Khi tài xế báo pin thấp, điều phối viên tra cứu vị trí GPS trên bản đồ nội bộ, mở dashboard trạm sạc VinFast để tìm trụ trống gần nhất, soạn tin nhắn hướng dẫn gửi qua App tài xế, và gọi xe cứu hộ nếu pin quá thấp. Toàn bộ 5 bước là thủ công, mất khoảng 15 phút/lượt. |
| **3. Bottleneck** | Bước 3 & 4 (mất 10 phút): tra cứu thủ công trụ sạc trống phù hợp và soạn tin hướng dẫn — dễ sai nếu điều phối viên vội và không kiểm tra kỹ khoảng cách khi pin đã ở mức nguy cấp. |
| **4. Business Impact** | Ước tính hàng chục sự cố pin thực địa mỗi ngày tại các thành phố lớn. Xử lý chậm gây rủi ro xe cạn pin giữa đường (ùn tắc giao thông, chi phí cứu hộ), tài xế mất thời gian chờ, ảnh hưởng trải nghiệm khách đang trên xe. |
| **5. Success Metric** | 1. Giảm thời gian xử lý sự cố từ 15 phút xuống dưới 3 phút.<br>2. 100% các trường hợp pin < 5% được điều xe cứu hộ thay vì chỉ dẫn trạm sạc xa (0% vi phạm ranh giới an toàn). |
| **6. Operational Boundary** | AI được phép truy xuất vị trí GPS xe, dữ liệu trạm sạc trống, và soạn thảo tin nhắn hướng dẫn dạng **nháp** (`[DRAFT_ONLY]`). **TUYỆT ĐỐI CẤM:** tự động gửi tin đi mà không có điều phối viên duyệt (bắt buộc HITL); đề xuất trạm sạc cách xa hơn 5km khi pin dưới 5% — trường hợp này bắt buộc phải điều xe cứu hộ pin di động. |

## 3.3. Future-State Flow & AI Fit

* **AI Fit:** **LLM Feature** — không cần Agent tự trị vì quy trình có cấu trúc cố định (2 rule rõ ràng), và rủi ro khi AI tự hành động sai (chỉ dẫn sai trạm sạc) có thể gây nguy hiểm thực địa nên bắt buộc phải có con người duyệt.

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Nhận báo cáo │     │ 🔵 AI tự lấy │     │ 🔵 AI draft  │     │ 🟢 Dispatcher│
│ sự cố pin    │ ──→ │ vị trí +     │ ──→ │ tin hướng dẫn│ ──→ │ duyệt & gửi  │
│              │     │ trạm sạc trống│    │ (hoặc lệnh   │     │              │
│              │     │              │     │ dispatch xe  │     │              │
│              │     │              │     │ cứu hộ)      │     │              │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ↩️ Fallback:
                                                               Nếu AI output lỗi
                                                               format/JSON hoặc
                                                               không chắc chắn,
                                                               dispatcher tự xử lý
                                                               thủ công như cũ.
```

---

# 💻 Phase 4 — Prompt Prototype & Boundary Test (tham chiếu)

Chi tiết đầy đủ tại [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py). Tóm tắt:

* **Rule 1:** Mọi output bắt buộc bắt đầu bằng thẻ `[DRAFT_ONLY]`.
* **Rule 2:** Pin < 5% → cấm đề xuất trạm sạc > 5km, bắt buộc trả JSON `{"action": "dispatch_mobile_charger", "reason": "..."}`.
* **Kết quả stress-test với Gemini 2.5 Flash:** Cả 2 adversarial test case đều **PASS** — model giữ nguyên thẻ `[DRAFT_ONLY]` dù bị yêu cầu bỏ, và trả đúng JSON dispatch mobile charger khi pin báo 2% thay vì đề xuất trạm cách 8km.

---

# 🏁 Phase 5 — EVALUATE

### AI Readiness Checklist:
1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? (Log sự cố pin, GPS, danh sách trạm sạc)
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)? (Có — bắt buộc Dispatcher duyệt trước khi gửi)
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? (Cần thêm khảo sát thực địa với đội điều vận)

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.

**Justification:**
> Bài toán có phạm vi hẹp, ranh giới an toàn định nghĩa được bằng rule cứng (ngưỡng pin 5% / bán kính 5km), đã được kiểm chứng thực tế qua 2 adversarial test case với Gemini 2.5 Flash và đều pass. Chi phí triển khai thấp (1 LLM call + rule check, không cần Agent phức tạp), có Fallback rõ ràng khi AI lỗi. Điểm cần hoàn thiện trước khi mở rộng: khảo sát thêm với đội vận hành thực địa để xác nhận quy trình duyệt tin (HITL) không làm chậm thời gian phản hồi thực tế.
