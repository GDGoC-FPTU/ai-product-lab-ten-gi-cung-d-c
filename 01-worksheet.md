# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | **Xanh SM** | Tốn thời gian | Điều phối viên mất 15-20 phút/lượt xử lý thủ công sự cố tài xế báo pin yếu giữa đường: tra cứu vị trí GPS, tìm trạm sạc trống, soạn tin nhắn chỉ dẫn. |
| 2 | **VinFast** | Lặp lại | Bộ phận tài chính so khớp thủ công hàng nghìn hóa đơn sạc điện từ trạm sạc đối tác mỗi tuần, tốn 2-3 ngày công/tuần và dễ sai sót. |
| 3 | **Vinhomes** | AI có thể tốt hơn | Hệ thống CSKH trên App phản hồi rập khuôn, mất 12 giờ để phân loại và route khiếu nại cư dân đến đúng ban quản lý tòa nhà. |
| 4 | **Vinmec** | Pain từ người khác | Bác sĩ mất 20-30 phút/bệnh nhân viết tóm tắt hồ sơ xuất viện, trích xuất thủ công từ bệnh án điện tử, xét nghiệm và ghi chú lâm sàng. |
| 5 | **Vinpearl** | Tốn thời gian | Bộ phận quản lý khách sạn đọc và phân tích thủ công hàng trăm review trên Booking.com, Agoda mỗi tuần để lọc phàn nàn khẩn cấp, mất 8-10 giờ/tuần. |
| 6 | **VinFast** | AI có thể tốt hơn | Khách hàng mô tả lỗi xe bằng tiếng Việt đời thường, nhân viên CSKH phải tra cứu thủ công để map sang mã lỗi kỹ thuật, mất 10-15 phút/cuộc gọi. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên: **#1 (Xanh SM Sự cố pin), #3 (Vinhomes CSKH), #4 (Vinmec Xuất viện).**

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
│   1. Tài xế gọi tổng đài báo hết pin                        │
│   → 2. Dispatcher tra cứu vị trí GPS xe                     │
│   → 3. Mở Dashboard trạm sạc VinFast tìm trụ trống         │
│   → 4. Soạn tin nhắn hướng dẫn đường đi gửi qua App        │
│   → 5. Gọi đội xe cứu hộ pin di động nếu pin dưới 5%       │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (⏱ 10-12 phút/lượt)            │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4             │
│ (Auto tra cứu trạm sạc + Draft tin nhắn hướng dẫn)         │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ "Giảm thời gian xử lý sự cố từ 15 phút xuống dưới 3 phút" │
│ "Tỉ lệ chỉ dẫn đúng trạm sạc phù hợp đạt ≥ 98%"          │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

## Card #3 — Vinhomes: Phân loại & Điều hướng phản ánh cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Cư dân Vinhomes gửi khiếu nại qua App   │
│ nhưng hệ thống phân loại rập khuôn, mất 12h để route đến   │
│ đúng ban quản lý tòa nhà xử lý.                            │
│ Công ty thành viên: [x] Vinhomes                             │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Nhân viên CSKH: đọc + phân loại thủ công hàng trăm       │
│   phản ánh/ngày                                              │
│ - Cư dân: chờ phản hồi quá lâu (12h)                        │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Cư dân gửi phản ánh qua App                            │
│   → 2. CSKH đọc nội dung, phân loại thủ công               │
│   → 3. Chuyển tiếp đến ban quản lý/bộ phận kỹ thuật        │
│   → 4. Soạn tin nhắn phản hồi cho cư dân                   │
│                                                             │
│ Bước nào tốn nhất? Bước 2-3 (⏱ 8-12 phút/phản ánh)        │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3             │
│ (LLM phân loại + Auto-route + Draft phản hồi)              │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ "Giảm thời gian phản hồi từ 12 giờ xuống dưới 30 phút"     │
│ "Tỉ lệ phân loại đúng danh mục đạt ≥ 95%"                  │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

## Card #4 — Vinmec: Soạn thảo tóm tắt hồ sơ xuất viện

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #4                                       │
│                                                             │
│ Bài toán (1 câu): Bác sĩ Vinmec mất 20-30 phút/bệnh nhân  │
│ viết thủ công bản tóm tắt xuất viện từ nhiều nguồn dữ liệu │
│ lâm sàng rời rạc.                                           │
│ Công ty thành viên: [x] Vinmec                               │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Bác sĩ điều trị: quá tải hành chính                       │
│ - Bệnh nhân: chờ lâu mới được xuất viện                     │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Bác sĩ mở EMR, đọc ghi chú lâm sàng + xét nghiệm     │
│   → 2. Tổng hợp thông tin quan trọng thủ công              │
│   → 3. Soạn bản tóm tắt xuất viện bằng ngôn ngữ dễ hiểu   │
│   → 4. Kiểm tra, ký xác nhận và gửi cho bệnh nhân          │
│                                                             │
│ Bước nào tốn nhất? Bước 1-3 (⏱ 20-25 phút/bệnh nhân)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1-3             │
│ (LLM trích xuất EMR + Tổng hợp + Draft tóm tắt)            │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ "Giảm thời gian soạn tóm tắt từ 25 phút xuống dưới 5 phút"│
│ "Tỉ lệ draft bác sĩ chấp nhận không cần sửa đạt ≥ 85%"    │
│                                                             │
│ Quick Architecture: [x] LLM Feature (BẮT BUỘC bác sĩ       │
│ phê duyệt — Human-in-the-loop)                              │
└─────────────────────────────────────────────────────────────┘
```

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = 15 phút/lượt**.

**Bài toán được chọn: Xanh SM — Xử lý sự cố tài xế báo pin yếu giữa đường**

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Nhận cuộc    │     │ Tra cứu định │     │ Tra cứu trạm │     │ Soạn văn bản │
│ gọi sự cố    │ ──→ │ vị GPS xe   │ ──→ │ sạc VinFast  │ ──→ │ hướng dẫn    │
│              │     │              │     │ còn trụ trống│     │ gửi tài xế   │
│ Ai: Dispatch │     │ Ai: Dispatch │     │ Ai: Dispatch │     │ Ai: Dispatch │
│ ⏱ 2 phút     │     │ ⏱ 2 phút     │     │ ⏱ 5 phút 🔴  │     │ ⏱ 5 phút 🔴  │
│ 🔄 Handoff:  │     │ In: Biển số  │     │ In: Vị trí   │     │ In: Raw data │
│ Tài xế →     │     │ Out: Toạ độ  │     │ Out: Địa chỉ │     │ Out: SMS     │
│ Dispatcher   │     │ GPS          │     │ trạm sạc     │     │ hướng dẫn    │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Bước 5       │
                                                               │ Gọi xe cứu   │
                                                               │ hộ (nếu cần) │
                                                               │ Ai: Dispatch │
                                                               │ ⏱ 1 phút     │
                                                               └──────────────┘
🔴 = Bottlenecks (Bước 3, 4)
🔄 = Handoff (Bước 1: Tài xế → Dispatcher)
⏱ Tổng thời gian xử lý thủ công: 15 phút/lượt.
```

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Điều phối viên (Dispatcher) thuộc Trung tâm Điều vận Xanh SM. |
| **2. Current Workflow** | Khi tài xế báo hết pin, điều phối viên tra cứu vị trí GPS trên bản đồ nội bộ, mở Dashboard trạm sạc VinFast để tìm trụ sạc trống gần nhất phù hợp loại cổng sạc, viết tin nhắn chỉ dẫn đường đi gửi qua App tài xế, và gọi cứu hộ nếu pin dưới 5%. 5 bước, hoàn toàn thủ công, mất 15 phút/lượt. |
| **3. Bottleneck** | Bước 3 & 4 (mất 10 phút): Tra cứu thủ công trụ sạc trống phù hợp dòng xe (VF5/VFe34/VF8) và soạn thảo tin nhắn hướng dẫn đường đi chi tiết bằng Tiếng Việt. |
| **4. Business Impact** | Mỗi ngày có ~80 sự cố pin thực địa tại Hà Nội. Gây lãng phí 20 giờ làm việc/ngày của team điều vận. Tăng thời gian chờ của tài xế, rò rỉ doanh thu ~15% do xe không thể đón khách. |
| **5. Success Metric** | 1. Giảm tổng thời gian xử lý sự cố từ 15 phút xuống dưới 3 phút. 2. Tỉ lệ hướng dẫn đúng địa điểm và đúng loại trụ sạc phù hợp đạt 98%. |
| **6. Operational Boundary** | AI được phép truy xuất API định vị xe, API trạm sạc VinFast trống, tự động soạn tin nhắn hướng dẫn dạng nháp (draft). **CẤM:** AI không được tự động gửi tin mà không có Dispatcher phê duyệt (Bắt buộc HITL); không được đề xuất trạm sạc xa hơn 5km khi pin dưới 5%. |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [x] **LLM Feature** (Không cần Agent tự trị vì quy trình có cấu trúc cố định, rủi ro khi điều phối sai trạm sạc có thể khiến xe cạn pin giữa đường).
* **Future-State Flow:**

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Nhận cuộc    │     │ 🔵 Auto-pull │     │ 🔵 AI draft  │     │ 🟢 Dispatch  │
│ gọi sự cố    │ ──→ │ vị trí &     │ ──→ │ SMS chỉ dẫn  │ ──→ │ click duyệt  │
│              │     │ trạm sạc     │     │ & chỉ đường  │     │ & gửi tài xế │
│              │     │ trống        │     │              │     │              │
│ ⏱ 1 phút     │     │ ⏱ 5 giây     │     │ ⏱ 10 giây    │     │ ⏱ 30 giây    │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ↩️ Fallback:
                                                               Nếu AI draft lỗi
                                                               hoặc confidence
                                                               thấp, Dispatcher
                                                               tự viết tay lại
                                                               như quy trình cũ.
```

* 🔵 **AI Step:** Bước 2-3 — LLM tự động tra cứu API + soạn draft tin nhắn.
* 🟢 **Human Step (HITL):** Bước 4 — Dispatcher phê duyệt trước khi gửi.
* ↩️ **Fallback:** Nếu LLM trả về lỗi hoặc tin nhắn không hợp lệ, Dispatcher tự soạn thủ công.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? → **Có.** Hệ thống điều vận Xanh SM đã ghi log tọa độ GPS xe, lịch sử sự cố pin, và dữ liệu trạm sạc VinFast real-time qua API.
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)? → **Có.** Mọi tin nhắn AI soạn đều phải qua Dispatcher duyệt trước khi gửi (HITL). Nếu AI sai, Dispatcher tự viết thủ công (Fallback).
3. [x] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? → **Có.** Team Điều vận Xanh SM đang quá tải (~80 sự cố/ngày), rất mong muốn được hỗ trợ giảm tải.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> **Quyết định GO** vì các lý do sau:
>
> 1. **Bài toán cụ thể, có metric rõ ràng:** Giảm thời gian xử lý từ 15 phút → 3 phút, tiết kiệm ~17 giờ công/ngày cho team điều vận.
> 2. **Giải pháp đơn giản mà hiệu quả:** Chỉ cần LLM Feature (không cần Agent phức tạp), sử dụng API sẵn có của VinFast (GPS + trạm sạc).
> 3. **Rủi ro thấp:** Mọi output AI đều qua bước duyệt của Dispatcher (HITL), có Fallback rõ ràng. Ranh giới an toàn đã được stress-test thành công bằng Gemini (2/2 adversarial test PASS).
> 4. **Chi phí hợp lý:** Gemini Flash API chi phí thấp (~$0.01/1000 requests), ước tính chi phí vận hành chỉ ~$24/tháng cho 80 sự cố/ngày.
> 5. **Dữ liệu sẵn sàng:** Hệ thống điều vận đã có log GPS, API trạm sạc real-time — không cần thu thập thêm dữ liệu mới.

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
