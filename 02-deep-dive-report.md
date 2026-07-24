BÀI TOÁN 1 — XANH SM XỬ LÝ SỰ CỐ PIN YẾU/LỖI SẠC
3.1. Current-State Workflow Mapping
Mô tả quy trình hiện tại

Khi xe đang vận hành gặp tình trạng pin yếu, không thể sạc hoặc có nguy cơ dừng giữa đường, tài xế liên hệ Trung tâm Điều vận. Điều phối viên phải thu thập thông tin, kiểm tra vị trí xe, trạng thái pin, tìm phương án xử lý và gửi hướng dẫn cho tài xế.

┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 1 — TÀI XẾ BÁO SỰ CỐ                                          │
│ Actor: Tài xế Xanh SM                                               │
│ Công cụ: Điện thoại / ứng dụng tài xế                               │
│ Input: Biển số, vị trí, mức pin, loại sự cố                         │
│ Output: Ticket hoặc cuộc gọi sự cố                                  │
│ Thời gian: 2 phút                                                   │
└──────────────────────────────┬──────────────────────────────────────┘
                               │ 🔄 Handoff: Tài xế → Điều phối viên
                               ▼
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 2 — XÁC MINH THÔNG TIN XE                                      │
│ Actor: Điều phối viên                                               │
│ Công cụ: Dashboard đội xe, bản đồ GPS                               │
│ Input: Biển số hoặc mã tài xế                                       │
│ Output: Dòng xe, tọa độ, mức pin, trạng thái hoạt động              │
│ Thời gian: 3 phút                                                   │
└──────────────────────────────┬──────────────────────────────────────┘
                               │ 🔄 Handoff: Fleet Dashboard → Dispatcher
                               ▼
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 3 — TÌM PHƯƠNG ÁN XỬ LÝ                            🔴 BOTTLENECK│
│ Actor: Điều phối viên                                               │
│ Công cụ: Bản đồ, dashboard trạm sạc, danh sách cứu hộ               │
│ Công việc:                                                          │
│ - Tìm trạm sạc gần nhất                                             │
│ - Kiểm tra trụ còn hoạt động                                        │
│ - Kiểm tra loại trụ phù hợp với xe                                  │
│ - Ước lượng xe có đủ pin để di chuyển hay không                     │
│ Output: Trạm sạc hoặc phương án cứu hộ                              │
│ Thời gian: 6 phút                                                   │
└──────────────────────────────┬──────────────────────────────────────┘
                               │ 🔄 Handoff: Nhiều hệ thống → Dispatcher
                               ▼
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 4 — SOẠN HƯỚNG DẪN CHO TÀI XẾ                      🔴 BOTTLENECK│
│ Actor: Điều phối viên                                               │
│ Công cụ: Chat nội bộ / ứng dụng tài xế                              │
│ Công việc: Viết địa chỉ, lộ trình, cảnh báo và hướng dẫn xử lý      │
│ Output: Tin nhắn hướng dẫn                                          │
│ Thời gian: 4 phút                                                   │
└──────────────────────────────┬──────────────────────────────────────┘
                               │ 🔄 Handoff: Dispatcher → Tài xế
                               ▼
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 5 — THEO DÕI VÀ ĐÓNG SỰ CỐ                                     │
│ Actor: Điều phối viên                                               │
│ Công cụ: Dashboard / điện thoại                                     │
│ Output: Đã đến trạm, đã cứu hộ hoặc chuyển cấp xử lý                │
│ Thời gian thao tác: 2 phút                                          │
└─────────────────────────────────────────────────────────────────────┘
Tổng thời gian hiện tại
2 + 3 + 6 + 4 + 2 = khoảng 17 phút/lượt

Trong trường hợp dữ liệu GPS, trạng thái trạm sạc hoặc thông tin tài xế thiếu, thời gian có thể tăng lên 20–25 phút/lượt.

Bottleneck chính
Điều phối viên phải chuyển qua nhiều dashboard khác nhau.
Trạng thái trạm sạc có thể thay đổi trong thời gian xử lý.
Việc đánh giá xe có đủ pin đến trạm hay không phụ thuộc kinh nghiệm cá nhân.
Tin nhắn hướng dẫn được viết thủ công, dễ thiếu địa chỉ hoặc cảnh báo an toàn.
Nhiều sự cố đồng thời trong giờ cao điểm làm tăng thời gian chờ.
3.2. Problem Statement 6-field
Field	Nội dung chi tiết
1. Actor / Operator	Điều phối viên tại Trung tâm Điều vận Xanh SM. Actor liên quan gồm tài xế, nhân viên cứu hộ và nhân viên vận hành trạm sạc.
2. Current Workflow	Khi nhận cuộc gọi báo pin yếu hoặc lỗi sạc, điều phối viên lấy biển số xe, tra cứu GPS và mức pin trên Fleet Dashboard, mở hệ thống trạm sạc để tìm trụ phù hợp, đánh giá xe có thể tự di chuyển hay cần cứu hộ, sau đó viết và gửi hướng dẫn cho tài xế. Quy trình sử dụng điện thoại, bản đồ nội bộ, Fleet Dashboard, dashboard trạm sạc và ứng dụng nhắn tin.
3. Bottleneck	Bước tìm phương án và soạn hướng dẫn mất khoảng 10 phút/lượt. Điều phối viên phải tổng hợp dữ liệu từ nhiều hệ thống, kiểm tra khoảng cách, loại trụ sạc, trạng thái hoạt động và mức pin trước khi đưa ra phương án.
4. Business Impact	Baseline giả định: 60–80 sự cố/ngày tại một khu vực vận hành lớn. Với 17 phút/lượt, nhóm điều vận sử dụng khoảng 17–23 giờ công/ngày. Thời gian xử lý chậm khiến xe ngừng khai thác lâu hơn, có thể làm hủy cuốc, giảm số chuyến/xe/ngày và ảnh hưởng trải nghiệm của tài xế, hành khách.
5. Success Metric	1. Giảm median handling time từ khoảng 17 phút xuống dưới 4 phút. 2. Ít nhất 95% trường hợp có đầy đủ dữ liệu được đề xuất đúng loại phương án. 3. 100% trường hợp pin dưới ngưỡng an toàn phải yêu cầu con người duyệt và không được tự động chỉ đường đến trạm quá xa. 4. Giảm ít nhất 50% số thao tác chuyển đổi giữa dashboard. 5. Tỉ lệ điều phối viên chấp nhận draft không cần sửa lớn đạt ≥85%.
6. Operational Boundary	AI được phép đọc dữ liệu xe, vị trí, mức pin, trạng thái trạm và tạo phương án ở dạng nháp. AI không được tự gửi lệnh cho tài xế, tự điều động cứu hộ, thay đổi trạng thái trạm sạc hoặc cam kết thời gian cứu hộ. Khi pin dưới ngưỡng an toàn, GPS thiếu, dữ liệu trạm quá cũ hoặc độ tin cậy thấp, hệ thống bắt buộc chuyển sang điều phối viên.
3.3. AI Fit Matrix
Phương án	Vai trò	Đánh giá
Rule / State Machine	Kiểm tra ngưỡng pin, khoảng cách, loại xe, loại cổng sạc và điều kiện an toàn	Bắt buộc sử dụng vì đây là các điều kiện xác định, không nên giao cho LLM suy đoán.
LLM Feature	Tóm tắt báo cáo sự cố và tạo tin nhắn hướng dẫn rõ ràng cho tài xế	Phù hợp nhất cho ngôn ngữ tự nhiên và chuẩn hóa nội dung.
Agentic Loop	Tự gọi nhiều hệ thống, tự chọn phương án và thực thi hành động	Chưa phù hợp ở giai đoạn đầu vì rủi ro hành động sai và quy trình hiện tại tương đối cố định.
Kết luận AI Fit
Giải pháp đề xuất:
Rule/State Machine + API orchestration + LLM drafting + Human approval

Không nên dùng một LLM đơn lẻ để tính toán ngưỡng an toàn. Các điều kiện như mức pin, khoảng cách tối đa và loại trụ sạc phải được kiểm tra bằng code xác định.

Future-State Flow
┌─────────────────────┐
│ 1. Tài xế báo sự cố │
│ qua app hoặc gọi    │
└──────────┬──────────┘
           │
           ▼
┌──────────────────────────────────┐
│ 2. Hệ thống tự lấy dữ liệu       │
│ - GPS hiện tại                   │
│ - Mức pin                        │
│ - Dòng xe                        │
│ - Mã lỗi                         │
│ - Trạng thái trạm sạc            │
└──────────┬───────────────────────┘
           │
           ▼
┌──────────────────────────────────┐
│ 3. RULE ENGINE                   │
│ - Kiểm tra dữ liệu hợp lệ        │
│ - Loại trụ tương thích           │
│ - Khoảng cách                    │
│ - Ngưỡng pin an toàn             │
└──────────┬───────────────────────┘
           │
           ├──── Pin nguy cấp / dữ liệu thiếu ─────┐
           │                                        ▼
           │                              ┌─────────────────────┐
           │                              │ ↩️ FALLBACK          │
           │                              │ Chuyển Dispatcher    │
           │                              │ xử lý thủ công       │
           │                              └─────────────────────┘
           ▼
┌──────────────────────────────────┐
│ 4. 🔵 AI STEP                    │
│ Tóm tắt tình huống và tạo        │
│ [DRAFT_ONLY] hướng dẫn cho tài xế│
└──────────┬───────────────────────┘
           │
           ▼
┌──────────────────────────────────┐
│ 5. 🟢 HUMAN-IN-THE-LOOP          │
│ Dispatcher kiểm tra:             │
│ - Trạm sạc                       │
│ - Khoảng cách                    │
│ - Mức pin                        │
│ - Nội dung tin nhắn              │
└──────────┬───────────────────────┘
           │
     ┌─────┴─────┐
     │           │
 Phê duyệt    Từ chối/sửa
     │           │
     ▼           ▼
┌──────────┐  ┌───────────────────┐
│ Gửi tài  │  │ ↩️ Dispatcher sửa │
│ xế       │  │ hoặc xử lý tay    │
└────┬─────┘  └───────────────────┘
     │
     ▼
┌──────────────────────────────────┐
│ 6. Theo dõi kết quả và lưu log   │
│ phục vụ đánh giá hệ thống        │
└──────────────────────────────────┘
Fallback Conditions

Hệ thống phải chuyển sang xử lý thủ công khi:

Không lấy được GPS hoặc mức pin.
Dữ liệu trạm sạc quá cũ, ví dụ quá 2 phút.
Không có trạm tương thích trong bán kính an toàn.
Xe báo lỗi hệ thống pin nghiêm trọng.
Pin dưới 5% nhưng trạm đề xuất cách quá 5 km.
Model không tạo được JSON đúng schema.
Confidence thấp hơn ngưỡng được cấu hình.
Điều phối viên từ chối phương án AI.
Phase 5 — Decision Quality
Quyết định: GO — Prototype với scope hẹp
Phạm vi prototype

Chỉ áp dụng cho:

Các xe có dữ liệu GPS và mức pin hợp lệ.
Tình huống pin yếu thông thường.
Khu vực có dữ liệu trạm sạc theo thời gian gần thực.
AI chỉ tạo draft.
Dispatcher luôn là người phê duyệt cuối cùng.
Justification

Bài toán có workflow rõ, tần suất lặp lại cao và có thể đo trực tiếp bằng thời gian xử lý. Phần quyết định an toàn có thể được kiểm soát bằng rule engine, trong khi LLM chỉ đảm nhiệm tóm tắt và tạo nội dung hướng dẫn.

Rủi ro chưa thể loại bỏ hoàn toàn vì dữ liệu GPS, trạng thái trạm và mức pin có thể sai hoặc trễ. Vì vậy, prototype chỉ nên được triển khai theo mô hình decision-support, không phải hệ thống điều phối tự động.

BÀI TOÁN 2 — VINHOMES PHÂN LOẠI VÀ CHUYỂN PHẢN ÁNH CƯ DÂN
3.1. Current-State Workflow Mapping
Mô tả quy trình hiện tại

Cư dân gửi phản ánh qua ứng dụng, hotline, email hoặc quầy lễ tân. Nhân viên CSKH phải đọc nội dung, xác định loại vấn đề, kiểm tra thông tin căn hộ, chuyển đến bộ phận phụ trách và theo dõi phản hồi.

┌────────────────────────────────────────────────────────────────────┐
│ BƯỚC 1 — CƯ DÂN GỬI PHẢN ÁNH                                      │
│ Actor: Cư dân                                                      │
│ Kênh: Vinhomes Resident, email, hotline, quầy lễ tân              │
│ Input: Văn bản, ảnh, video, ghi âm                                 │
│ Output: Ticket mới                                                 │
│ Thời gian hệ thống: dưới 1 phút                                    │
└──────────────────────────────┬─────────────────────────────────────┘
                               │ 🔄 Handoff: Cư dân → CSKH
                               ▼
┌────────────────────────────────────────────────────────────────────┐
│ BƯỚC 2 — NHÂN VIÊN ĐỌC VÀ TÓM TẮT                     🔴 BOTTLENECK│
│ Actor: Nhân viên CSKH                                              │
│ Công cụ: CRM, email, ứng dụng cư dân                               │
│ Công việc: Đọc toàn bộ phản ánh và xem file đính kèm              │
│ Output: Tóm tắt vấn đề                                             │
│ Thời gian: 4 phút                                                  │
└──────────────────────────────┬─────────────────────────────────────┘
                               ▼
┌────────────────────────────────────────────────────────────────────┐
│ BƯỚC 3 — PHÂN LOẠI VÀ XÁC ĐỊNH MỨC ƯU TIÊN             🔴 BOTTLENECK│
│ Actor: Nhân viên CSKH                                              │
│ Công việc:                                                         │
│ - Chọn nhóm sự cố                                                  │
│ - Đánh giá khẩn cấp                                                │
│ - Xác định tòa/khu/căn hộ                                          │
│ Output: Category, priority, SLA                                    │
│ Thời gian: 3 phút                                                  │
└──────────────────────────────┬─────────────────────────────────────┘
                               │ 🔄 Handoff: CSKH → Bộ phận xử lý
                               ▼
┌────────────────────────────────────────────────────────────────────┐
│ BƯỚC 4 — CHUYỂN TICKET ĐẾN BỘ PHẬN PHỤ TRÁCH           🔴 BOTTLENECK│
│ Actor: Nhân viên CSKH                                              │
│ Bộ phận: Kỹ thuật, an ninh, vệ sinh, kế toán, pháp chế...          │
│ Output: Ticket được gán cho đội xử lý                              │
│ Thời gian: 2 phút                                                  │
└──────────────────────────────┬─────────────────────────────────────┘
                               ▼
┌────────────────────────────────────────────────────────────────────┐
│ BƯỚC 5 — BỘ PHẬN CHUYÊN MÔN KIỂM TRA VÀ XỬ LÝ                      │
│ Actor: Nhân viên vận hành                                          │
│ Output: Kết quả xử lý hoặc yêu cầu bổ sung thông tin               │
│ Thời gian tiếp nhận ban đầu: 5 phút                                │
└──────────────────────────────┬─────────────────────────────────────┘
                               │ 🔄 Handoff: Bộ phận xử lý → CSKH
                               ▼
┌────────────────────────────────────────────────────────────────────┐
│ BƯỚC 6 — CSKH SOẠN PHẢN HỒI CHO CƯ DÂN                             │
│ Actor: Nhân viên CSKH                                              │
│ Output: Tin nhắn xác nhận hoặc cập nhật trạng thái                 │
│ Thời gian: 3 phút                                                  │
└────────────────────────────────────────────────────────────────────┘
Tổng thời gian thao tác
1 + 4 + 3 + 2 + 5 + 3 = khoảng 18 phút/ticket

Đây là thời gian thao tác, không bao gồm thời gian chờ bộ phận chuyên môn xử lý. Do queue và handoff, phản ánh có thể mất vài giờ mới được tiếp nhận đúng bộ phận.

Bottleneck chính
Nhân viên phải đọc nhiều phản ánh có nội dung dài hoặc không rõ ràng.
Cư dân có thể mô tả nhiều vấn đề trong cùng một ticket.
Phân loại không đồng nhất giữa các nhân viên.
Ticket chuyển sai bộ phận phải trả lại và route lại.
Phản ánh liên quan an toàn có thể bị xếp nhầm mức ưu tiên.
Câu trả lời xác nhận thường được soạn thủ công và lặp lại.
3.2. Problem Statement 6-field
Field	Nội dung chi tiết
1. Actor / Operator	Nhân viên CSKH Vinhomes là người tiếp nhận, đọc, tóm tắt, phân loại và chuyển phản ánh. Actor liên quan gồm cư dân, ban quản lý tòa nhà, đội kỹ thuật, an ninh, vệ sinh, kế toán và pháp chế.
2. Current Workflow	Phản ánh được gửi từ nhiều kênh vào CRM. Nhân viên CSKH đọc nội dung và file đính kèm, xác định tòa/căn hộ, tóm tắt vấn đề, chọn category và priority, gán ticket đến bộ phận phụ trách, sau đó gửi phản hồi xác nhận cho cư dân.
3. Bottleneck	Bước đọc, tóm tắt, phân loại và route mất khoảng 9 phút/ticket. Chất lượng phụ thuộc kinh nghiệm của nhân viên; phản ánh mơ hồ, chứa nhiều vấn đề hoặc có yếu tố cảm xúc dễ bị phân loại sai.
4. Business Impact	Baseline giả định: một khu đô thị tiếp nhận 800–1.200 phản ánh/ngày. Với khoảng 9 phút cho khâu triage, nhu cầu có thể lên tới 120–180 giờ công/ngày. Ticket chuyển sai làm kéo dài SLA, tăng số lần cư dân liên hệ lại và làm giảm mức hài lòng.
5. Success Metric	1. Ít nhất 85% ticket thông thường được tạo bản tóm tắt và đề xuất category trong dưới 10 giây. 2. Macro F1 phân loại category đạt ≥0,90 trên tập test đã gán nhãn. 3. Recall của nhóm khẩn cấp đạt ≥0,98. 4. Giảm thời gian triage trung vị từ 9 phút xuống dưới 2 phút/ticket. 5. Giảm ticket route sai ít nhất 40% so với baseline. 6. Không có ticket pháp lý, tài chính hoặc an toàn nào được tự động đóng.
6. Operational Boundary	AI được phép tóm tắt, trích xuất thông tin, đề xuất category, priority, bộ phận nhận và tạo phản hồi xác nhận dạng draft. AI không được kết luận trách nhiệm pháp lý, xác nhận bồi thường, điều chỉnh phí, hủy khoản thu, hứa thời hạn xử lý chưa được hệ thống SLA xác nhận hoặc tự động đóng ticket. Các ticket liên quan cháy nổ, bạo lực, y tế, mất an ninh, tranh chấp, tài chính và pháp lý bắt buộc phải chuyển người phụ trách.
3.3. AI Fit Matrix
Phương án	Vai trò	Đánh giá
Rule / State Machine	Route các trường hợp có keyword rõ, xác định SLA cố định, kiểm tra dữ liệu bắt buộc	Hữu ích nhưng không đủ cho phản ánh dài, mơ hồ hoặc dùng nhiều cách diễn đạt.
LLM Feature	Tóm tắt, trích xuất entity, phân loại ngữ nghĩa và tạo draft phản hồi	Phù hợp nhất cho phần xử lý ngôn ngữ.
Agentic Loop	Tự trao đổi với cư dân, tự truy vấn nhiều hệ thống và tự đóng ticket	Chưa nên dùng trong prototype vì có nguy cơ đưa cam kết sai hoặc thực hiện hành động vượt quyền.
Kết luận AI Fit
Giải pháp đề xuất:
Rule-based safety router + LLM triage assistant + Human confirmation

Phân loại khẩn cấp nên có hai lớp:

Rule engine nhận diện các tín hiệu an toàn rõ ràng.
LLM đánh giá nội dung ngữ nghĩa và tạo đề xuất.

Nếu một trong hai lớp xác định ticket có rủi ro cao, ticket phải được chuyển sang hàng chờ ưu tiên cho con người.

Future-State Flow
┌───────────────────────────┐
│ 1. Cư dân gửi phản ánh    │
│ text / image / audio      │
└─────────────┬─────────────┘
              ▼
┌──────────────────────────────────┐
│ 2. Tiền xử lý                    │
│ - Speech-to-text nếu có audio    │
│ - Lấy metadata tòa/căn hộ        │
│ - Kiểm tra file và dữ liệu thiếu │
└─────────────┬────────────────────┘
              ▼
┌──────────────────────────────────┐
│ 3. RULE SAFETY CHECK             │
│ Cháy, khói, bạo lực, y tế,       │
│ mất an ninh, rò điện, rò gas...  │
└─────────────┬────────────────────┘
              │
       Trường hợp khẩn cấp
              │
              ▼
┌──────────────────────────────────┐
│ 🟢 Chuyển ngay người trực vận hành│
│ Không chờ LLM tự động route      │
└──────────────────────────────────┘

Trường hợp thông thường:
              │
              ▼
┌──────────────────────────────────┐
│ 4. 🔵 AI STEP                    │
│ - Tóm tắt phản ánh               │
│ - Trích xuất tòa/căn hộ          │
│ - Đề xuất category               │
│ - Đề xuất priority               │
│ - Đề xuất bộ phận xử lý          │
│ - Tạo draft xác nhận             │
└─────────────┬────────────────────┘
              ▼
┌──────────────────────────────────┐
│ 5. VALIDATION LAYER              │
│ - JSON đúng schema?              │
│ - Category thuộc taxonomy?       │
│ - Có nhiều vấn đề trong ticket?  │
│ - Confidence đủ cao?             │
└─────────────┬────────────────────┘
              │
       ┌──────┴───────┐
       │              │
 Confidence cao    Confidence thấp /
 ticket thường     nội dung nhạy cảm
       │              │
       ▼              ▼
┌────────────────┐  ┌──────────────────────────┐
│ 6. 🟢 CSKH xem │  │ ↩️ FALLBACK              │
│ và xác nhận    │  │ Chuyển CSKH phân loại tay│
└───────┬────────┘  └──────────────────────────┘
        ▼
┌──────────────────────────────────┐
│ 7. Route đến bộ phận phụ trách   │
│ và gửi phản hồi đã được duyệt    │
└─────────────┬────────────────────┘
              ▼
┌──────────────────────────────────┐
│ 8. Lưu kết quả chỉnh sửa của     │
│ CSKH làm dữ liệu đánh giá        │
└──────────────────────────────────┘
Fallback Conditions

Chuyển sang xử lý thủ công khi:

Nội dung thiếu thông tin tòa, căn hộ hoặc vị trí.
Ticket chứa từ hai vấn đề độc lập trở lên.
Model trả category ngoài taxonomy.
Confidence thấp hơn ngưỡng.
File đính kèm không đọc được.
Phản ánh liên quan tài chính, pháp lý, tranh chấp hoặc bồi thường.
Có dấu hiệu đe dọa an toàn, cháy nổ, y tế hoặc an ninh.
Cư dân yêu cầu gặp trực tiếp quản lý.
JSON output không hợp lệ.
Kết quả của rule engine và LLM mâu thuẫn.
Phase 5 — Decision Quality
Quyết định: NOT YET — Thu thập dữ liệu và xác lập baseline trước
Justification

Bài toán phù hợp với AI vì phần lớn công việc là đọc hiểu, tóm tắt và phân loại ngôn ngữ tự nhiên. Tuy nhiên, việc triển khai ngay có ba vấn đề:

Chưa xác nhận có taxonomy category thống nhất giữa các khu đô thị.
Chưa có tập ticket lịch sử đã được gán nhãn sạch để đo F1, recall khẩn cấp và tỉ lệ route sai.
Nội dung phản ánh có thể chứa dữ liệu cá nhân, tranh chấp, tài chính hoặc thông tin nhạy cảm.

Vì vậy, dự án chưa nên tự động route production ngay. Trước tiên cần:

- Chuẩn hóa category và priority taxonomy
- Lấy tập dữ liệu ticket đã ẩn danh
- Đo baseline hiện tại
- Gán nhãn tập test bởi ít nhất hai nhân viên vận hành
- Chạy shadow mode
- So sánh AI suggestion với quyết định thật của CSKH
Điều kiện chuyển từ NOT YET sang GO

Có thể chuyển sang GO với scope hẹp khi đạt:

Tối thiểu khoảng 3.000–5.000 ticket lịch sử đã được làm sạch.
Có taxonomy thống nhất và owner cho từng category.
Có ít nhất 500–1.000 ticket test độc lập.
Macro F1 đạt từ 0,90.
Recall nhóm khẩn cấp đạt từ 0,98.
Có cơ chế ẩn dữ liệu cá nhân và phân quyền truy cập.
Hệ thống chỉ chạy ở chế độ suggestion, chưa tự động đóng ticket.