# 03 — AI Log & Reflection (Bài cá nhân)

**Họ và tên:** [ĐIỀN TÊN CỦA BẠN]
**MSSV:** [ĐIỀN MSSV]

---

## 🤖 AI giúp gì?

Trong buổi lab, tôi dùng Claude (Claude Code) làm thought-partner xuyên suốt quá trình:
* Viết `SYSTEM_PROMPT` nghiêm ngặt cho vai trò dispatcher co-pilot của Xanh SM, cụ thể hóa 2 ranh giới an toàn (thẻ `[DRAFT_ONLY]` bắt buộc, và rule pin < 5% → không đề xuất trạm > 5km, phải điều xe cứu hộ).
* Viết code Python hoàn thiện hàm `evaluate_prompt()` gọi Gemini 2.5 Flash SDK (`google-genai`), có fallback sang SDK cũ `google-generativeai` nếu SDK mới không import được.
* Hỗ trợ debug khi chạy script bị lỗi `API key not valid` — AI giúp phát hiện ra nguyên nhân thực sự không phải do code mà do tôi copy nhầm key sai định dạng.

## ❌ AI sai gì?

Ban đầu khi tôi dán một API key sai định dạng (không phải key Gemini thật, dạng `AQ.Ab8...` thay vì `AIzaSy...`) vào biến môi trường, AI đã đưa ra kết luận khá chắc chắn rằng đây "không phải Gemini API key hợp lệ" dựa trên format quen thuộc. Tuy nhiên sau đó khi tôi test thực tế, key đó **lại chạy được** — cho thấy AI đã đưa ra nhận định hơi vội dựa trên format cũ mà nó biết, trong khi Google có thể đã cập nhật định dạng key mới mà AI chưa cập nhật kịp. Đây là một dạng "hallucination nhẹ" về kiến thức đã lỗi thời (outdated knowledge) chứ không phải AI bịa chuyện hoàn toàn.

## 🔧 Sửa đổi ra sao?

Tôi yêu cầu AI thực sự chạy thử script (thay vì chỉ suy đoán) để xác nhận key có hoạt động hay không, thay vì tin tưởng hoàn toàn vào nhận định lý thuyết ban đầu. Bài học rút ra: khi làm việc với AI về mã nguồn có thể kiểm chứng được (chạy thử, test case), nên luôn ưu tiên chạy thực tế để xác minh thay vì chỉ dựa vào suy luận của AI. Ngoài ra tôi cũng học được cách không nên dán API key thật vào file trong repo (README.md) hay lặp lại nhiều lần trong chat — AI đã cảnh báo đúng về rủi ro bảo mật này và tôi đã sửa lại (revert README.md, khuyến nghị thu hồi/tạo key mới).
