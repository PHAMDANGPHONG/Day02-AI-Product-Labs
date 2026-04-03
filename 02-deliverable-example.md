## Context: Tôi là ai?

Tôi là **Phong**, 21 tuổi, sinh viên năm cuối trường Đại học Công nghệ. Mỗi tuần tôi phải:

Đọc các bài báo khoa học (paper) để hoàn thiện khóa luận tốt hơn.

Viết "Weekly Report" gửi cho giảng viên hướng dẫn (GVHD).

Lên kế hoạch công việc và mục tiêu cho những tuần tiếp theo.

Ngoài ra tôi còn phải trực tiếp code thực nghiệm mô hình trên Kaggle, xử lý dataset, dọn dẹp dữ liệu, và tự quản lý thời gian. Bài toán tôi mang vào lab hôm nay đến từ chính quá trình "chạy nước rút" cho project tốt nghiệp của mình.

# Phase 1 — SCAN: Tìm kiếm cơ hội

Dùng **4 Lenses** để quét

| #  | Lens               | Bài toán |
|----|--------------------|----------|
| 1  | Lặp lại            | Mỗi cuối tuần phải chụp ảnh màn hình log/kết quả train mô hình trên Kaggle để paste vào Word làm báo cáo tiến độ |
| 2  | Lặp lại            | Phải viết email gửi GVHD vào mỗi tối Chủ Nhật để đính kèm report và xin lịch hẹn meeting tuần tới — cùng một format văn phong, chỉ đổi số liệu |
| 3  | Tốn thời gian      | Đọc 2-3 paper tiếng Anh mỗi tuần, mất rất nhiều thời gian để chắt lọc ra phương pháp luận và đối chiếu với mô hình đang làm |
| 4  | AI có thể tốt hơn  | Quá trình tìm kiếm và xử lý lỗi (debug) khi chạy thử mô hình đang làm thủ công tốn hàng giờ, AI có thể phân tích log lỗi nhanh hơn. |
| 5  | Pain từ người khác | Lúc gặp GVHD bị hỏi: "Tuần vừa rồi độ chính xác của model cải thiện được bao nhiêu % so với baseline tuần trước?" mà chưa paste vào report thì không nhớ ngay để trả lời |
| 6  | Tốn thời gian      | Trích xuất và định dạng lại các trích dẫn (citation) từ các bài báo khoa học |


# Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn top 3 từ list:
- **#2 — Tổng hợp Weekly Report cho GVHD**
- **#3 — Đọc và chắt lọc Paper**
- **#4 — Debug lỗi chạy mô hình**

## Card #1 — Tổng hợp Weekly Report cho GVHD

```text
┌──────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                            │
│                                                  │
│ Bài toán: Mỗi tối Chủ Nhật, viết email báo cáo   │
│ tiến độ và xin lịch hẹn GVHD mất 60 phút do      │
│ phải tổng hợp log trên Kaggle và chỉnh format    │
│                                                  │
│ Ai đang đau? Tôi (SV), GVHD (đọc report dài)     │
│                                                  │
│ Workflow hiện tại:                               │
│   1. Mở Kaggle copy log/kết quả thực nghiệm      │
│   → 2. Viết nháp tóm tắt việc đã làm             │
│   → 3. Gạch đầu dòng plan tuần tới               │
│   → 4. Gửi email cho GVHD                        │
│                                                  │
│ Bước nào tốn nhất? Bước 2 & 3 (⏱ 40 min/lần)    │
│                                                  │
│ AI có thể giúp ở bước nào? Bước 2 & 3            │
│ (Biến log kỹ thuật khô khan thành report)        │
│                                                  │
│ Đo thành công bằng gì?                           │
│ Giảm thời gian làm report từ 40 min → 15 min     │
│                                                  │
│ Quick gut: ☑ LLM Feature                        │
└──────────────────────────────────────────────────┘
```

## Card #2 — Đọc và chắt lọc Paper

```text
┌──────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                            │
│                                                  │
│ Bài toán: Đọc 5-7 paper tiếng Anh mỗi tuần mất   │
│ quá nhiều thời gian để tìm ra phần methodology   │
│ và đối chiếu với model đang làm             │
│                                                  │
│ Ai đang đau? Tôi (SV nghiên cứu)                 │
│                                                  │
│ Workflow hiện tại:                               │
│   1. Tải PDF → 2. Đọc Abstract & chắt lọc paper  │
│   → 3. Highlight phần Methodology (đặc biệt là   │
│   phần được cải tiến) → 4.  So sánh với phương   │
│   pháp của mình → 5.Tạo bảng so sánh             |
│   → 6. paste vào report                          |
│                                                  │
│ Bước nào tốn nhất? Bước 2 & 3 (⏱ ~90 min)       │
│                                                  │
│ AI có thể giúp ở bước nào? Bước 3 & 4            │
│ (Trích xuất methodology & tóm tắt ý chính)       │
│                                                  │
│ Đo thành công bằng gì?                           │
│ Giảm thời gian xử lý 1 paper từ 90 min → 25 min  │
│                                                  │
│ Quick gut: ☑ LLM Feature (Summarization)         │
└──────────────────────────────────────────────────┘
```

## Card #3 — Debug lỗi chạy mô hình
```text
┌──────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                            │
│                                                  │
│ Bài toán: Tìm và fix lỗi khi train/test mô       │
│ hình trên dataset VizWiz tốn hàng giờ tra cứu    │
│ trên StackOverflow hoặc tài liệu                 │
│                                                  │
│ Ai đang đau? Tôi (người trực tiếp code)          │
│                                                  │
│ Workflow hiện tại:                               │
│   1. Mô hình báo lỗi (VD: dimension mismatch)    │
│   → 2. Copy mã lỗi → 3. Search Google            │
│   → 4. Đọc các thread giải pháp                  │
│   → 5. Sửa code và chạy lại thử                  │
│                                                  │
│ Bước nào tốn nhất? Bước 3 & 4 (⏱ 30-60 min/lỗi) │
│                                                  │
│ AI có thể giúp ở bước nào? Bước 3, 4, 5          │
│ (Phân tích lỗi dựa trên context code hiện tại)   │
│                                                  │
│ Đo thành công bằng gì?                           │
│ Giảm thời gian tìm giải pháp bug từ 45 min       │
│ → dưới 10 min                                    │
│                                                  │
│ Quick gut: ☑ Agent (cần đọc context code, log)   │
└──────────────────────────────────────────────────┘
```

---

# Phase 3 — PITCH-CHALLENGE-VOTE

## Cards bị loại

| Card bị loại | Lý do |
|--------------|-------|
| #1 — Tổng hợp Weekly Report cho GVHD | Tác động thấp đến kết quả nghiên cứu. Việc tối ưu nó chỉ giúp tiết kiệm thời gian viết, nhưng không giúp cải thiện độ chính xác của mô hình hay chiều sâu của luận văn |
| #3 — Debug lỗi chạy mô hình | Độ tin cậy thấp. AI dễ gây ra "hallucination" khi giải quyết các lỗi logic sâu hoặc lỗi môi trường đặc thù, có thể làm tốn thời gian hơn nếu sửa sai hướng. |

### Bài học rút ra từ quá trình đánh giá (Lessons Learned)

#### A. Ưu tiên "Gốc" hơn "Ngọn"
Tự động hóa những việc râu ria (viết email, format báo cáo) mang lại cảm giác thảnh thơi giả tạo. Bài học lớn nhất là AI nên được dùng để **thông minh hóa bộ não** (như Card #2: thẩm thấu Methodology từ paper) 
#### B. Quản trị rủi ro: "Verify, don't just Trust"
Đừng biến AI thành "người quyết định" trong các khâu kỹ thuật trọng yếu. Với các hệ thống model phức tạp, AI chỉ đóng vai trò tư vấn hướng đi. Người nghiên cứu phải nắm vững logic để kiểm soát các gợi ý, tránh việc sa lầy vào những lỗi sai dây chuyền do AI tạo ra khi nó không hiểu hết bối cảnh phần cứng.

#### C. Đánh giá Chi phí cơ hội (Opportunity Cost)
Thời gian ngồi tinh chỉnh Prompt để AI làm những việc vụn vặt đôi khi còn lâu hơn tự làm tay.
# Phase 4 — DEEP-DIVE (team)

# Phase 5 — EVALUATE (team)

# Phase 6 — AI Support Log (Log Phase Reflection)

| Câu hỏi | Trả lời |
|---------|---------|
| AI giúp gì? | Gợi ý cấu trúc 4 Lenses để quét vấn đề; Brainstorm nhanh các "nỗi đau" tiềm ẩn trong lab; Dự thảo sơ bộ các bước trong Workflow cho từng Card |
| AI sai ở đâu? | Đưa ra các con số thời gian (60p, 90p) chỉ mang tính ước lượng lý thuyết; Các giải pháp cho Card #3 (Debug) quá màu hồng, chưa tính đến việc lỗi do server Kaggle hoặc CUDA mismatch mà AI không can thiệp được |
| Nhóm phải sửa gì bằng tay? | Card #1: Phải ngồi bấm giờ thực tế lúc soạn email để ra số 40 phút; Card #2: Tự phân loại lại các mục cần trích xuất (Methodology, Baseline) vì AI tóm tắt quá dàn trải; Card #3: Xác định rõ ranh giới (boundary) là AI chỉ gợi ý hướng fix, không được để AI tự sửa code trực tiếp. |
| Prompt hay nhất? | "Đóng vai một Researcher, hãy so sánh phương pháp của Paper A với kiến trúc model và lập bảng các điểm khác biệt về Layer Tuning." |
