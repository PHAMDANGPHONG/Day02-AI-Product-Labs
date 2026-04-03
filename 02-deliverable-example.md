# Deliverable 2: 02-deep-dive-report.md
**Bài toán:** Đọc, trích xuất Methodology từ Paper tiếng Anh và đối chiếu với model Moondream2

---

## Phase 4 — DEEP-DIVE (Phân tích chuyên sâu)

### 4.1 Current-State Workflow (Luồng công việc hiện tại)

Luồng xử lý hàng tuần để cập nhật kiến thức từ các paper mới:

```text
┌─────────────┐     ┌─────────────┐     ┌──────────────┐     ┌──────────────────┐
│ Bước 1      │     │ Bước 2      │     │ Bước 3       │     │ Bước 4           │
│ Tìm paper   │     │ Chọn 2-3    │     │ Đọc sâu và   │     │ So sánh với      │
│             │ ──→ │ paper/tuần  │ ──→ │ tìm phần nổi │ ──→ │ phương pháp của  │
│ Ai: Phong   │     │ Ai: Phong   │     │ bật          │     │ mình             │
│ ⏱ 10 min    │     │ ⏱ 10 min   │     │ Ai: Phong    │     │ Ai: Phong       │
│ In: ArXiv   │     │ In: 50+ ppr │     │ ⏱ 40 min 🔴 │     │ ⏱ 40 min 🔴    │
│ Out: 50+ ppr│     │ Out: 2-3 ppr│     │ In: 2-3 ppr  │     │ In: Repo cá nhân │
└─────────────┘     └─────────────┘     └──────────────┘     └──────────────────┘
                                                                      │
                                                                      ▼
                                             ┌──────────────────┐     ┌──────────────────┐
                                             │ Bước 6           │     │ Bước 5           │
                                             │ Ghi lại và paste │ ─── │ Tóm tắt bản so   │
                                             │ vào report       │     │ sánh             │
                                             │ Ai: Phong        │     │ Ai: Phong        │
                                             │ ⏱ 10 min         │     │ ⏱ 15 min         │
                                             └──────────────────┘     └──────────────────┘

🔴 = Bottleneck (Điểm nghẽn)
⏱ Tổng thời gian: ~125 phút / chu trình (trung bình ~90 phút để hoàn thành việc phân tích sâu 1 paper)
```

**Ghi chú bottleneck:**
* Bước 3 và Bước 4 chiếm phần lớn thời gian (80 phút). Đọc sâu một tài liệu học thuật tiếng Anh để mò ra đúng phần Methodology cốt lõi rất dễ gây kiệt sức.
* Việc đối chiếu chéo (cross-reference) giữa các kỹ thuật trong paper mới với cấu trúc của repo cá nhân đòi hỏi sự tập trung cao độ, dễ bị "ngợp" thông tin.

---

### 4.2 Problem Statement & Metrics (6-field)

| Field | Nội dung |
|-------|----------|
| **Actor / Operator** | Phong (Sinh viên nghiên cứu). |
| **Current Workflow** | Tìm paper trên ArXiv → Chọn lọc 2-3 paper → Đọc sâu tìm Methodology → Đối chiếu kỹ thuật với repo cá nhân → Tóm tắt → Ghi report. Tổng cộng 6 bước, thủ công 100%. |
| **Bottleneck** | Bước 3 & 4: Đọc sâu paper tiếng Anh và đối chiếu kiến trúc chiếm tới 80 phút. Các paper thường rất dài và rườm rà, khó tìm nhanh phần trọng tâm về Visual Question Answering (VQA). |
| **Impact** | Mất quá nhiều thời gian (3-4 tiếng mỗi tuần chỉ để xử lý vài paper), làm chậm tiến độ viết code, chạy experiment và hoàn thiện report nghiên cứu. |
| **Success Metric** | Giảm tổng thời gian đọc hiểu và so sánh 1 paper từ 90 phút xuống **dưới 20 phút**. |
| **Operational Boundary** | AI được phép đọc file PDF và nhận context của model Moondream2 để tóm tắt và trích xuất. AI **KHÔNG** được tự ý bịa ra (hallucinate) các phương pháp không có trong paper. Phong phải là người đọc và duyệt lại bản tóm tắt cuối cùng trước khi đưa vào report. |

**Sub-goals Decomposition:**
* *TRƯỚC khi dùng AI:* Lọc và tải đúng file PDF của paper cần đọc. Soạn sẵn một file text mô tả ngắn gọn kiến trúc hiện tại để làm "System Prompt" cho AI.
* *TRONG khi dùng AI:* Review các điểm methodology mà AI trích xuất để đảm bảo không bỏ sót keyword quan trọng về VQA.

**Metrics:**

| Loại | Metric | Ngưỡng (Threshold) |
|------|--------|--------|
| **Efficiency (Thời gian)** | Thời gian đọc sâu, so sánh và tóm tắt 1 paper | 90 phút → < 20 phút |
| **Quality (Chất lượng)** | Tỉ lệ trích xuất đúng phương pháp cốt lõi | Không bỏ sót thông tin quan trọng (Review thủ công đạt 100% khớp ý tưởng) |

---

### 4.3 Research

**Existing solution:**
* **ChatPDF / SciSpace:**
    * *Điểm mạnh:* Cho phép upload PDF và hỏi đáp trực tiếp, tìm thông tin cực nhanh.
    * *Điểm yếu:* Thiếu context cá nhân. Các công cụ này chỉ hiểu nội dung trong paper đó, không tự động biết "phương pháp của mình" là gì để đối chiếu sâu trừ khi phải prompt rất dài và thủ công mỗi lần.

**Case study:**
* **Dùng LLM có Context Window lớn (Gemini 1.5 Pro / Claude 3.5 Sonnet):**
    * *Họ làm gì:* Upload trực tiếp file PDF của paper cùng với file `README.md` hoặc tài liệu mô tả kiến trúc vào chung một phiên chat. Yêu cầu LLM đóng vai trò Research Assistant, trích xuất Methodology và lập bảng so sánh điểm khác biệt.
    * *Kết quả:* LLM thực hiện so sánh đối chiếu kỹ thuật (như cơ chế Attention, cách encode ảnh/text) cực kỳ chính xác.

**Bài học rút ra cho bài toán của mình:**
Không cần xây dựng hệ thống phức tạp, chỉ cần thiết kế một **Prompt Template** chuẩn, đính kèm file PDF và context của Moondream2. Giải pháp là **LLM Feature (Boost)**.

---

### 4.4 Future-State Flow + AI Fit

**1. AI Fit Check:**
Bài toán nằm ở ô: **Complexity thấp + Ambiguity cao → LLM Feature**
*(Workflow chỉ là nhét text vào và lấy text ra (complexity thấp), nhưng việc tóm tắt và so sánh kỹ thuật học thuật đòi hỏi khả năng xử lý ngôn ngữ và suy luận sâu (ambiguity cao)).*

**2. Future-State Flow:**

```text
┌─────────────┐     ┌─────────────┐       ┌──────────────────┐
│ Bước 1      │     │ Bước 2      │       │ Bước 3           │
│ Tìm & Chọn  │ ──→ │ 🔵 AI đọc    │  ──→ │ 🔵 AI đối chiếu với │
│ 2-3 paper   │     │ paper & trích│      │ phương pháp của  │
│ Ai: Phong   │     │ xuất phần nổi bật │  │ mình           │
│ ⏱ 20 min    │     │ ⏱ 5-10 min      │   │ ⏱ 5-10 min       │
└─────────────┘     └─────────────┘        └──────────────────┘
                                                      │
                                                      ▼
                    ┌─────────────┐     ┌──────────────────┐
                    │ Bước 5      │     │ Bước 4           │
                    │ Paste vào   │ ─── │ 🟢 tóm tắt      │
                    │ Report      │     │                  │
                    │ Ai: Phong   │     │ Ai: Phong        │
                    │ ⏱ 5 min     │     │ ⏱ 10 min        │
                    └─────────────┘     └──────────────────┘
                    
➡️ Fallback: Nếu AI tóm tắt sai lệch hoặc tối nghĩa →  tự mở PDF ra đọc phần Methodology (nhưng ít nhất AI đã chỉ ra nó nằm ở trang nào, vẫn tiết kiệm thời gian).
```
*Tổng thời gian mới cho việc xử lý 1 paper (sau khi đã chọn): ~20-25 phút (Giảm từ 90 phút).*

**3. Underspecification Check:**

| Điều chưa rõ | Hậu quả | Cách tìm ra |
|---|---|---|
| AI có nhầm lẫn thuật ngữ của paper với các mô hình khác không? | Tóm tắt sai kiến trúc, dẫn đến so sánh sai lệch | Đọc chéo lại Abstract của paper trong 2 phút để verify output của AI. |
| Độ dài của paper vượt quá context limit? | Báo lỗi hoặc AI cắt bớt thông tin quan trọng ở phần sau. | Sử dụng các mô hình hỗ trợ >100k tokens. |

---

## Phase 5 — EVALUATE (Đánh giá & Quyết định)

### G4. Decision Quality

**AI Readiness Checklist:**

| # | Câu hỏi | Kết quả | Ghi chú |
|---|---------|---------|---------|
| 1 | Có data/input đủ chất lượng? | **Yes** | File PDF paper từ ArXiv rất chuẩn, text extract dễ dàng. |
| 2 | Có metric rõ? | **Yes** | 90 phút → ~25 phút. |
| 3 | Sai thì hậu quả có chấp nhận được? | **Yes** | Phong là người review cuối, sai thì tự đọc lại, rủi ro có thể chấp nhận. |
| 4 | User sẵn sàng dùng AI? | **Yes** | Phong rất muốn thoát khỏi việc đọc chữ chay. |
| 5 | Có resource để maintain? | **Yes** | Chỉ cần dùng Web UI của các AI sẵn có (Gemini/ChatGPT/Claude), không cần code app riêng. |

**Optimization Check:**
* **Lợi ích:** Tiết kiệm ~70 phút cho mỗi paper. Có thêm thời gian để tập trung vào việc implement code.
* **Rủi ro:** AI "hallucinate" ra các layer hoặc loss function không có trong paper để cố làm cho bài so sánh trông logic.

**Quyết định:**
**GO (Thực hiện ngay lập tức)**

**Justify (Lý do):**
Bài toán đáp ứng 5/5 tiêu chí Readiness. Rủi ro tác động kinh doanh/vận hành là bằng không do đây là workflow cá nhân (research). Chỉ cần tạo một Prompt Template cố định và áp dụng ngay trong tuần tới để đo lường thực tế xem thời gian có giảm đúng xuống ~25 phút như kỳ vọng hay không.
