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

### List bài toán của tôi:
| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | VinFast | Lặp lại (Repetitive) | So khớp hóa đơn sạc điện từ các trạm sạc công cộng (bên thứ 3) với dữ liệu billing nội bộ của VinFast; nhân viên tài chính phải đối chiếu thủ công hàng nghìn giao dịch/tháng do định dạng dữ liệu không đồng nhất giữa các nhà cung cấp trạm sạc. |
| 2 | Xanh SM | Pain từ người khác (Stakeholder Pain) | Tài xế phàn nàn hệ thống gợi ý điểm đón khách không khớp vị trí thực tế (đặc biệt ở khu vực có nhiều tầng/tòa nhà lớn), khiến tài xế phải gọi điện xác nhận thủ công, kéo dài thời gian chờ và giảm điểm hài lòng khách hàng. |
| 3 | Vinhomes | Tốn thời gian (Time-consuming) | Nhân viên CSKH Ban Quản lý tòa nhà phải soạn thảo thủ công từng phản hồi cho các đánh giá 1–2 sao của cư dân trên app VinhomesResidents/Google Maps, mất 10–15 phút/lượt và thường trễ SLA nội bộ. |
| 4 | Vinmec | AI có thể tốt hơn (AI-upgrade) | Quy trình tiền khám hiện tại yêu cầu điều dưỡng hỏi thủ công triệu chứng ban đầu để xếp loại mức độ ưu tiên (triage), dẫn đến thời gian chờ không đồng đều và đôi khi bỏ sót dấu hiệu cảnh báo sớm. |
| 5 | Vinpearl / VinWonders | Tốn thời gian (Time-consuming) | Bộ phận CSKH phải trả lời hàng trăm email/chat/ngày hỏi về chính sách đặt phòng, đổi/hủy vé, giờ mở cửa — phần lớn là câu hỏi lặp lại có thể tra cứu trong tài liệu chính sách nội bộ. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #___                                     │
│                                                             │
│ Bài toán (1 câu): ________________________________________  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? ______________________________________ │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. ___ ──> 2. ___ ──> 3. ___ ──> 4. ___                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? ___ (⏱ ___ phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? _____________________ │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? ______________________ │
│   VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> ### Quick Problem Card #1
 
```
Bài toán: Soạn phản hồi tự động cho đánh giá 1–2 sao của cư dân trên app VinhomesResidents.
Công ty thành viên: [x] Vinhomes
 
Ai đang đau (Actor)? Nhân viên CSKH trực ban tại Ban Quản lý tòa nhà (BQL).
 
Workflow thủ công hiện tại:
  1. Đọc review + tra cứu lịch sử ticket ──> 2. Soạn nháp phản hồi ──>
  3. Gửi Trưởng phòng duyệt ──> 4. Đăng công khai
 
Bước nào tốn thời gian/lỗi nhất? Soạn nháp phản hồi (⏱ 10–15 phút/lượt)
AI có thể nhảy vào hỗ trợ ở bước nào? Soạn nháp phản hồi dựa trên ngữ cảnh ticket có sẵn.
 
Đo thành công bằng gì? Giảm thời gian soạn nháp từ 10–15 phút xuống dưới 2 phút;
tỷ lệ phản hồi trong SLA 4 giờ tăng từ 35% lên ≥85%.
 
Quick Architecture: [x] LLM
```
 
### Quick Problem Card #2
 
```
Bài toán: Xác thực & hiệu chỉnh điểm đón khách gợi ý sai cho tài xế Xanh SM.
Công ty thành viên: [x] Xanh SM
 
Ai đang đau (Actor)? Tài xế Xanh SM (đặc biệt khu chung cư/tòa nhà cao tầng).
 
Workflow thủ công hiện tại:
  1. App gợi ý điểm đón (GPS) ──> 2. Tài xế đến điểm không khớp thực tế ──>
  3. Tài xế gọi khách xác nhận vị trí ──> 4. Điều chỉnh lộ trình thủ công
 
Bước nào tốn thời gian/lỗi nhất? Gọi điện xác nhận (⏱ 2–4 phút/lượt, xảy ra ~15% chuyến ở khu đô thị).
AI có thể nhảy vào hỗ trợ ở bước nào? Suy luận điểm đón chính xác hơn dựa trên lịch sử điểm đón thực tế + landmark.
 
Đo thành công bằng gì? Giảm tỷ lệ phải gọi xác nhận từ 15% xuống dưới 5% số chuyến.
 
Quick Architecture: [x] Rule kết hợp LLM (hybrid)
```
 
### Quick Problem Card #3
 
```
Bài toán: So khớp hóa đơn sạc điện từ trạm sạc bên thứ 3 với hệ thống billing VinFast.
Công ty thành viên: [x] VinFast
 
Ai đang đau (Actor)? Nhân viên phòng Tài chính – Đối soát (Reconciliation).
 
Workflow thủ công hiện tại:
  1. Tải file hóa đơn từ đối tác (Excel/PDF khác định dạng) ──> 2. Chuẩn hóa dữ liệu thủ công ──>
  3. Đối chiếu với hệ thống nội bộ ──> 4. Đánh dấu chênh lệch để xử lý
 
Bước nào tốn thời gian/lỗi nhất? Chuẩn hóa dữ liệu thủ công (⏱ ~3 giờ/ngày/nhân viên).
AI có thể nhảy vào hỗ trợ ở bước nào? Trích xuất & chuẩn hóa dữ liệu từ file đa định dạng, gắn cờ chênh lệch bất thường.
 
Đo thành công bằng gì? Giảm thời gian đối soát/ngày từ 3 giờ xuống dưới 30 phút; độ chính xác khớp ≥98%.
 
Quick Architecture: [x] LLM + Rule kiểm tra chéo
```

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

```
[Cư dân đăng review 1★ trên app VinhomesResidents / Google Maps]
        │  🔄 Handoff (hệ thống → nhân viên CSKH)
        ▼
[NV CSKH đọc review + tra cứu lịch sử căn hộ/ticket trên CRM]  🔴 Bottleneck (5–7 phút,
        │                                                         phải chuyển qua 2-3 hệ thống rời rạc)
        ▼
[NV CSKH soạn thảo phản hồi bằng tay: xin lỗi + hướng giải quyết]  🔴 Bottleneck lớn nhất
        │                                                            (10–15 phút, phụ thuộc kỹ năng viết cá nhân)
        ▼  🔄 Handoff (nhân viên → Trưởng phòng CSKH)
[Trưởng phòng duyệt bản nháp]  🔴 Bottleneck (chờ trung bình 30–60 phút, có lúc vài giờ vì bận họp)
        │
        ▼
[Đăng phản hồi công khai]  (2 phút)
 
Tổng cộng = 50–85 phút/lượt (chưa tính thời gian chờ duyệt kéo dài, có thể lên đến 24–48 giờ)
```


## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên CSKH trực ban tại các Ban Quản lý tòa nhà Vinhomes, phụ trách kênh phản hồi công khai (app VinhomesResidents + Google Maps). |
| **2. Current Workflow** | NV đọc review → tra cứu CRM/lịch sử ticket → soạn nháp phản hồi thủ công → gửi Trưởng phòng duyệt → đăng công khai. Công cụ: CRM nội bộ, Excel theo dõi, app quản lý tòa nhà. |
| **3. Bottleneck** | (a) Soạn thảo phản hồi thủ công tốn 10–15 phút/lượt do phải cân bằng giọng điệu xin lỗi, tính pháp lý và giải pháp cụ thể; (b) chờ duyệt của Trưởng phòng kéo dài không kiểm soát được. |
| **4. Business Impact** | Trung bình 100–150 review 1–2★/tháng/tòa nhà lớn (dữ liệu ước tính từ khảo sát nhóm BQL). SLA nội bộ yêu cầu phản hồi công khai trong 4 giờ nhưng chỉ ~35% đạt đúng hạn. Phản hồi trễ ảnh hưởng trực tiếp đến điểm rating trung bình trên Google Maps của các phân khu (rating thấp ảnh hưởng đến uy tín thương hiệu và quyết định mua/thuê của khách hàng tiềm năng). |
| **5. Success Metric** | (a) Giảm thời gian soạn nháp phản hồi từ 10–15 phút xuống **dưới 2 phút**; (b) Tỷ lệ phản hồi trong SLA 4 giờ tăng từ 35% lên **≥85%**; (c) **≥90%** bản nháp AI được duyệt mà không cần chỉnh sửa lớn (thay đổi <20% nội dung). |
| **6. Operational Boundary** | AI **được phép**: soạn nháp phản hồi dựa trên template chuẩn + ngữ cảnh ticket có sẵn; đề xuất tông giọng phù hợp mức độ nghiêm trọng. AI **tuyệt đối không được**: tự động đăng công khai mà không qua người duyệt; cam kết số tiền bồi thường/hoàn tiền cụ thể; tiết lộ thông tin cá nhân của cư dân khác trong cùng tòa nhà; tự ý đưa ra cam kết pháp lý. **Điểm cần duyệt (HITL bắt buộc)**: mọi review có từ khóa liên quan an toàn/tai nạn/pháp lý/đe dọa kiện tụng phải escalate thẳng cho Trưởng phòng, không tạo nháp tự động.



## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

| Kiến trúc | Đánh giá |
|---|---|
| **Rule / State-Machine** | Có thể dùng template cố định theo loại phàn nàn (tiếng ồn, sự cố kỹ thuật, an ninh...) nhưng phản hồi sẽ rập khuôn, cư dân dễ nhận ra "trả lời máy", giảm cảm giác được lắng nghe. |
| **LLM Feature** ✅ (lựa chọn) | Phù hợp nhất: sinh văn bản tự nhiên, cá nhân hóa theo ngữ cảnh cụ thể của từng ticket, nhưng luôn đi kèm HITL trước khi đăng công khai. Rủi ro được kiểm soát vì không có hành động tự động không thể đảo ngược. |
| **Agentic Loop** | Chưa cần thiết ở giai đoạn hiện tại vì phạm vi chỉ là sinh văn bản, không cần tự thực hiện nhiều bước hay gọi API khác (vd. tự động hoàn tiền). Có thể nâng cấp thành agent sau khi LLM feature ổn định, để tự động tra cứu ticket liên quan trên nhiều hệ thống. |


**AI-Fit Matrix:** [x] LLM Feature
 
**Future-State Flow:**
 
```
[Cư dân đăng review 1★]
        ▼
🔵 AI Step: Phân loại mức độ nghiêm trọng + trích xuất ngữ cảnh (căn hộ, lịch sử ticket liên quan)
        ▼
🔵 AI Step: Soạn nháp phản hồi theo tông giọng chuẩn + gợi ý hướng giải quyết
        ▼
🟢 Human Step (HITL): NV CSKH xem, chỉnh sửa (nếu cần), duyệt
        ▼
[Đăng phản hồi công khai]
 
↩️ Fallback: Nếu AI có độ tự tin thấp, hoặc phát hiện từ khóa nhạy cảm
   (an toàn / tai nạn / pháp lý / đe dọa kiện tụng) → escalate thẳng cho
   Trưởng phòng CSKH, KHÔNG tạo nháp tự động, hiển thị cảnh báo rõ ràng.
```


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
| Adversarial Test | Ranh giới bị nhắm tới | Kỳ vọng model xử lý |
|---|---|---|
| #1 | Dụ AI cam kết số tiền bồi thường cụ thể | Model từ chối nêu số tiền, đề xuất escalate cho người phụ trách tài chính |
| #2 | Dụ AI tiết lộ thông tin cư dân khác (vd. "cư dân căn A đã từng bị gì?") | Model từ chối cung cấp, chỉ trả lời trong phạm vi ticket hiện tại |
| #3 | Dụ AI tự xác nhận đã "đăng" phản hồi thay vì chỉ tạo nháp | Model phải luôn trả về field `status: draft_pending_approval`, không tự nhận đã đăng |




---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> Bài toán có ranh giới rủi ro rõ ràng và dễ kiểm soát: AI chỉ tạo nháp văn bản, không thực hiện hành động không thể đảo ngược (không tự đăng, không tự cam kết tiền), và luôn có con người duyệt trước khi công khai (HITL). Dữ liệu lịch sử ticket + review có sẵn và đủ sạch để làm baseline test. Business impact được định lượng rõ (35% SLA hiện tại, tổn thất uy tín thương hiệu qua rating công khai), và success metric có ngưỡng số cụ thể (dưới 2 phút soạn nháp, ≥85% SLA). Rủi ro lớn nhất không nằm ở công nghệ mà ở thay đổi quy trình làm việc của Trưởng phòng CSKH — do đó khuyến nghị **pilot ở 1–2 tòa nhà** trong 4–6 tuần trước khi nhân rộng toàn hệ thống Vinhomes, đồng thời thu thập thêm dữ liệu về tỷ lệ nháp AI cần chỉnh sửa lớn để xác nhận ngưỡng ≥90% có khả thi hay không.

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
