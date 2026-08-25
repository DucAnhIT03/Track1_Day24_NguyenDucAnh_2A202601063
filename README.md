# 🎓 VinUniversity AI Talent Program — Track 1: AI Product Management
## Day 24: AI Product Financial Model & Unit Economics Lab

> **Mục tiêu:** Giúp học viên chuyển hóa ý tưởng sản phẩm AI từ Day 16–17 thành một mô hình tài chính khả thi, tính toán chính xác Unit Economics (CAC, LTV, Gross Margin), và thực hiện stress-test 3 kịch bản để chứng minh khả năng sinh tồn (Runway ≥ 12 tháng).

---

## 📂 Cấu Trúc Repository (Repository Layout)

```text
Day24-Track1-AI-Product-Financial-Model-Lab/
├── README.md                              # Hướng dẫn chung & Quy cách nộp bài
├── track1-day24-Lab-tutor.md              # Đề bài bài tập chi tiết (VLearn Markdown Contract)
├── Day24-AI-Product-Finance-Model.xlsx    # Template Excel Mô hình Tài chính 3 Tabs chính thức
├── Day24-AI-Product-Handbook.pdf          # Tài liệu Handbook hướng dẫn & Benchmark tài chính AI
└── slides/                                # THƯ MỤC CHỨA SLIDE DECK TƯƠNG TÁC (90 PHÚT)
    ├── index.html                         # Giao diện Slide tương tác chính (mở trên trình duyệt)
    ├── css/
    │   └── styles.css                     # Style hiệu ứng Glassmorphic UI
    └── js/
        ├── data.js                        # Dữ liệu 5 Phase bài Lab
        ├── timer.js                       # Bộ đếm thời gian thực tế
        └── slides.js                      # Điều hướng Slide & Dynamic Island
```

---

## 🚀 Hướng Dẫn Sử Dụng Tài Nguyên

### 1. Dành cho Giảng viên / Coach (Slide Trình Chiếu):
* Mở thư mục `slides/` và chạy trực tiếp file [`slides/index.html`](slides/index.html) trên bất kỳ trình duyệt web nào (Chrome, Edge, Safari).
* Slide deck tích hợp bộ đếm thời gian (Timer Engine), Dynamic Island control bar và phím tắt điều hướng (`Arrow Left/Right`, `Space` để pause/start timer).

### 2. Dành cho Học viên (Làm Bài Tập):
* **Bước 1:** Đọc kỹ hướng dẫn đề bài tại file [`track1-day24-Lab-tutor.md`](track1-day24-Lab-tutor.md).
* **Bước 2:** Mở file Excel template [`Day24-AI-Product-Finance-Model.xlsx`](Day24-AI-Product-Finance-Model.xlsx) và thực hiện theo 5 Phase:
  * **Phase 0 (10'):** Khai báo Persona & Chọn mô hình thu tiền Hybrid Pricing.
  * **Phase 1 (20'):** Điền 100% ô màu vàng tại Tab 1 (Nhớ quy tắc `AI Hidden Costs >= 30% API Cost`).
  * **Phase 2 (15'):** Kiểm chứng Tab 2 đạt `LTV/CAC > 3.0` (tính trên Gross Margin) và `Payback < 12m`.
  * **Phase 3 (20'):** Đổi scenario Tab 3 sang `Pessimistic`, đảm bảo `Pessimistic Runway >= 12 tháng`.
  * **Phase 4 (25'):** Viết đoạn **Decision Note (200–300 từ)** bảo vệ các giả định.
* **Tham khảo Handbook:** Mở file [`Day24-AI-Product-Handbook.pdf`](Day24-AI-Product-Handbook.pdf) để tra cứu các chỉ số benchmark ngành (SaaS/AI metrics).

---

## 📌 Quy Cách Nộp Bài Cá Nhân

Mỗi học viên tạo một Repository cá nhân trên GitHub theo cấu trúc:

```text
Track1_Day24_MHV_HoVaTen/
├── README.md               # Ghi Họ tên, MSSV, Tên dự án & Đoạn văn Decision Note
└── [HoVaTen]_Day24.xlsx    # File Excel 3 Tabs đã hoàn thiện các kịch bản
```

### 🎯 Rubric Đánh Giá (100 Điểm):
1. **Giả định Tab 1 (30đ):** Điền 100% ô màu vàng, `AI Hidden Costs >= 30% API Cost`.
2. **AI Cost Awareness (25đ):** Tính đủ Data Labeling, Retraining (~20%), QA & Compliance.
3. **Unit Economics (20đ):** LTV tính bằng Gross Margin %, Base `LTV/CAC > 3.0` & `Payback < 12m`.
4. **Stress-testing (15đ):** Pessimistic Churn/CAC ≥ 1.5x Base, `Runway >= 12 tháng`.
5. **Nộp bài & Decision Note (10đ):** Lập luận chặt chẽ, nộp đúng hạn trước 13:00.

---

### 🏛️ VinUniversity Codelab
* **Program:** AI Talent Incubation
* **Track:** Track 1 — AI Product Management
