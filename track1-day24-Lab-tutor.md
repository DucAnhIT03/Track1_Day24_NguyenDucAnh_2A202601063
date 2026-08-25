---
day: "D24"
level: "beginner"
title: "Track 1 - Day 24 — AI Product Financial Model Lab: từ Giả định đến Stress-test 3 Kịch bản"
author: "VinUni Codelab"
updated: "2026-08-26"
category: "AI Product Management"
duration: 90
outcomes: ["Xác định đủ 5 cấu phần chi phí của AI Product, đặc biệt là AI Hidden Costs (Labeling, Retraining, Human QA, Compliance)","Tính toán chính xác Unit Economics (CAC, LTV dựa trên Gross Margin %, LTV/CAC ratio, CAC Payback Period)","Thiết lập giả định tài chính 3 kịch bản (Optimistic, Base, Pessimistic với shock factor 1.5x Churn & CAC)","Thực hiện stress-test dòng tiền trên file Excel 3-Tab để đảm bảo Pessimistic Runway >= 12 tháng","Viết Decision Note bảo vệ logic chọn ARPU, CAC và AI Hidden Costs trước nhà đầu tư / hội đồng"]
workMode: "individual"
description: "Mỗi học viên áp dụng mô hình tài chính sản phẩm AI lên chính dự án mình đang build: điền giả định Tab 1, kiểm chứng Unit Economics Tab 2, stress-test 3 kịch bản P&L Tab 3 và viết Decision Note bảo vệ."
supportedOs: ["macOS","Linux","Windows"]
commonErrors: ["Bỏ trống hoặc điền AI Hidden Costs = 0 (quên chi phí Labeling, Model Retraining)","Tính LTV dựa trên Doanh thu thô (Revenue) thay vì Lãi gộp (Gross Margin)","Kịch bản Pessimistic không có shock thực sự (Pessimistic copy nguyên từ Base)","Bịa số CAC siêu rẻ hoặc ARPU ảo để làm đẹp tỷ lệ LTV/CAC","Pessimistic Runway < 12 tháng mà không có phương án cắt giảm chi phí hay gọi thêm vốn","Viết Decision Note mơ hồ, không có căn cứ hoặc benchmark chứng minh"]
prerequisites: ["Đã tham gia bài giảng Day 24 (Burn Rate, Runway, 5 Cost Components, Unit Economics, NPV, IRR, 3-Scenario Stress Test)","Có một dự án AI đang build (dự án nhóm hoặc cá nhân từ Day 16-17)","Có file Excel template Day24-AI-Product-Finance-Model.xlsx"]
requiredTools: ["File Excel Day24-AI-Product-Finance-Model.xlsx","Phần mềm Microsoft Excel hoặc Google Sheets","Deck bài giảng Day 24 & Handbook để tra cứu benchmark","Tài khoản GitHub để nộp bài"]
requiresSubmission: true
---

# Track 1 - Day 24 — AI Product Financial Model Lab: từ Giả định đến Stress-test 3 Kịch bản

> 90 phút · Bài cá nhân, nộp bài cá nhân · Làm trên chính dự án bạn đang build · Trọng tâm là Phase 1–4; Phase 5 kiểm tra & hoàn thiện.

**Họ tên:** ........................................ · **Dự án:** ........................................

## 0. Đọc trước khi làm (3 phút)

**Bài này làm gì?** Bạn đóng vai PM / Founder của chính dự án AI mình đang build và đi một chuỗi quyết định tài chính: xác định cấu trúc chi phí & doanh thu $\rightarrow$ tính toán Unit Economics (CAC, LTV, Margin) $\rightarrow$ lập dự phóng P&L và stress-test 3 kịch bản (Optimistic, Base, Pessimistic) trên file Excel $\rightarrow$ viết Decision Note bảo vệ giả định trước VC / Nhà đầu tư.

**Từ ngữ sẽ gặp liên tục** (đọc một lần là đủ):

| Từ | Nghĩa đơn giản |
|---|---|
| **Burn Rate** | Tốc độ đốt tiền mặt ròng hàng tháng ($\text{Chi ra} - \text{Thu vào}$) |
| **Runway** | Số tháng sống sót với tiền mặt hiện tại ($\text{Cash} / \text{Burn Rate}$) |
| **COGS** | Chi phí biến đổi trực tiếp để phục vụ 1 khách hàng (API + Server + Hidden Costs) |
| **AI Hidden Costs** | Chi phí ẩn của AI: Data Labeling, Model Retraining (~20%/năm), Human QA, Compliance |
| **Gross Margin (%)** | Tỷ lệ lãi gộp $(\text{Revenue} - \text{COGS}) / \text{Revenue}$ |
| **CAC** | Chi phí Sales & Marketing để thu hút 1 khách hàng mới |
| **LTV** | Lợi nhuận gộp tích lũy 1 khách mang lại $= \text{ARPU} \times \text{Gross Margin \%} \times (1/\text{Churn})$ |
| **LTV / CAC Ratio** | Tỷ lệ sức khỏe đơn vị (Tiêu chuẩn vàng VC: $> 3.0$) |
| **CAC Payback** | Số tháng để lãi gộp thu hồi đủ chi phí CAC ($< 12 \text{ tháng}$) |
| **Pessimistic Stress-test** | Kịch bản xấu nhất: Churn tăng 1.5x, CAC tăng 1.5x, ARPU giảm $\rightarrow$ kiểm tra Runway $\ge 12\text{m}$ |

**Làm ở đâu?** Toàn bộ bài làm thực hiện trên file Excel `Day24-AI-Product-Finance-Model.xlsx` kết hợp viết văn bản Decision Note. Bài nộp cuối là một repository cá nhân chứa file Excel và file `README.md` (xem mục 10).

**Cứ 1 phase xong là có 1 "gate"** — ô kiểm tra nhỏ tự đối chiếu. Qua gate thì đi tiếp, không qua thì gọi coach.

## 1. Đề bài và cách làm

Dự án AI của bạn có thể có tính năng hay, RAG/Agent chạy mượt ở Day 23. Nhưng trả lời được câu này chưa:

> **Sản phẩm của bạn tốn bao nhiêu tiền để phục vụ 1 khách hàng, có lãi trên từng khách không, và công ty sẽ sống sót được bao nhiêu tháng nếu thị trường gặp biến cố xấu nhất?**

Nếu mô hình tài chính không sống được, sản phẩm tốt đến mấy cũng vỡ trận khi scale. Vì vậy bài lab đi theo chuỗi bắt buộc:

```text
Phạm vi & Mô hình thu tiền → Giả định đầu vào (Tab 1) → Kiểm chứng Unit Economics (Tab 2)
→ Stress-test P&L 3 Kịch bản (Tab 3) → Viết Decision Note bảo vệ
```

| Phase | Thời gian | Câu hỏi trung tâm | Đầu ra |
|---|---:|---|---|
| 0. Chốt phạm vi | 10 phút | Dự án nào, persona nào, mô hình thu tiền gì? | Khai báo mô hình kinh doanh |
| 1. Giả định đầu vào | 20 phút | Cost components & Pricing đặt bao nhiêu? | Tab 1 (Assumptions) hoàn chỉnh |
| 2. Kiểm chứng Unit Economics | 15 phút | LTV/CAC có > 3 và Payback < 12m không? | Tab 2 (Unit Economics) HEALTHY |
| 3. Stress-test 3 Kịch bản | 20 phút | Khi biến cố xấu xảy ra, Runway có $\ge 12$ tháng? | Tab 3 (P&L & ROI) kiểm chứng |
| 4. Viết Decision Note | 15 phút | Căn cứ nào bảo vệ các con số trước VC? | Decision Note 2-3 đoạn |
| 5. Tự soi lỗi & nộp | 10 phút | Bài có mắc 6 lỗi kinh điển nào không? | File Excel + Repo nộp bài |

### Luật của bài lab

1. **Chỉ điền vào ô màu vàng tại Tab 1.** Tất cả ô còn lại là công thức tự động.
2. **LTV phải tính trên Gross Margin.** Tuyệt đối không lấy Revenue thô nhân số tháng ở lại.
3. **Hidden Costs $\ge 30\%$ API Cost.** Không được điền chi phí ẩn bằng 0.
4. **Pessimistic phải có shock thực sự.** Churn tăng $\ge 1.5x$, CAC tăng $\ge 1.5x$ so với Base.
5. **Số liệu phải có căn cứ/benchmark.** Không bịa số ảo để làm đẹp chỉ số LTV/CAC.

---

## 2. Đầu vào và tài nguyên

- **File Excel template:** `Day24-AI-Product-Finance-Model.xlsx` (nằm trong thư mục `track1-day24`).
- **Deck & Handbook Day 24:** Tra cứu benchmark SaaS/AI (Bessemer, KeyBanc, YC data).
- **Dự án bạn đang build từ Day 16–17.**

---

## 3. Phase 0 — Chốt phạm vi & Mô hình thu tiền · 10 phút

**Làm** — xác định rõ 4 thông tin cốt lõi:

1. **Dự án:** Sản phẩm AI bạn đang build là gì?
2. **Target Customer / Persona:** Ai là người trả tiền (B2B SME, B2C, Enterprise)?
3. **Mô hình Doanh thu (Revenue Model):** Chọn 1 trong 4 loại: SaaS Subscription (MRR), Consumption (Usage-based), Transactional, hoặc **Hybrid** (Base fee + Overage).
4. **TAM (Total Addressable Market):** Ước tính tổng số khách hàng tiềm năng kèm nguồn logic.

:::decision{title="Lựa chọn Mô hình Pricing"}
Với sản phẩm AI, mô hình **Hybrid (Phí cố định + Phí theo usage)** là an toàn nhất để vừa có doanh thu dự đoán được (predictable MRR) vừa chống bẫy lỗ trên các "Power Users".
:::

**Ghi lại ở đâu:** Mục `00 — Mô hình Kinh doanh` trong bài nộp.

---

## 4. Phase 1 — Giả định Đầu vào (Tab 1 Assumptions) · 20 phút

**Kiến thức cần dùng**

- **5 Cost Components**: Cloud Infrastructure, Model API, R&D/Salaries, Sales & Marketing, và **AI Hidden Costs**.
- **AI Hidden Costs (Tảng băng chìm)**: Data Labeling, Model Retraining (~20% build cost/năm), Human-in-the-loop QA, Compliance.

### 1. Điền 6 phần ô màu vàng tại Tab 1 (15')

**Làm** — Mở file Excel `Day24-AI-Product-Finance-Model.xlsx`, nhập số liệu vào cả 3 cột (`Optimistic`, `Base`, `Pessimistic`):

| Section | Chỉ số | Hướng dẫn điền số |
|---|---|---|
| **1. Product & Pricing** | ARPU (VNĐ/khách/tháng)<br>Adoption rate (%/tháng)<br>TAM (số khách) | ARPU đặt theo benchmark giá thị trường.<br>Adoption rate từ 0.1% - 0.5%/tháng.<br>TAM từ 10,000 - 1,000,000 khách. |
| **2. COGS** | API cost / khách / tháng<br>AI Hidden Costs / khách<br>Infrastructure / khách | Tính API cost theo token ước tính.<br>**Hidden Costs $\ge 30\%$ API Cost**.<br>Infra server/VectorDB per user. |
| **3. Customer Behavior** | Monthly Churn Rate (%) | B2B SaaS: 2-5%; B2C: 5-8%; AI product: 5-10%.<br>**Pessimistic Churn $\ge 1.5 \times$ Base Churn**. |
| **4. Sales & Marketing** | CAC (VNĐ/khách mới) | CAC = Tổng Marketing & Sales / Khách mới.<br>**Pessimistic CAC $\ge 1.5 \times$ Base CAC**. |
| **5. Fixed Costs** | Salaries<br>Office, tools, admin<br>Marketing budget | Lương team hàng tháng.<br>Chi phí cố định văn phòng, SaaS tools.<br>Ngân sách Marketing chạy Ads. |
| **6. Investment** | Initial Investment<br>Initial Cash | Vốn build MVP ban đầu.<br>Tổng tiền mặt dự trữ hiện có. |

:::caution{title="Rủi ro Chi phí ẩn (Hidden Costs Trap)"}
Hầu hết founder AI thất bại vì chỉ tính tiền API OpenAI mà quên tiền data labeling, retrain model và thuê người QA kiểm duyệt output. Bỏ trống ô Hidden Costs sẽ bị trừ 10 điểm rubric!
:::

**Ghi lại ở đâu:** Tab 1 file Excel `[Tên]_Day24.xlsx`.

:::checkpoint{title="GATE 1 — Giả định Tab 1 đầy đủ"}
Bạn qua gate khi: 100% ô màu vàng cả 3 kịch bản tại Tab 1 đều có số, Hidden Costs $\ge 30\%$ API Cost, và Pessimistic Churn/CAC cao hơn Base ít nhất 1.5 lần.
:::

---

## 5. Phase 2 — Kiểm chứng Unit Economics (Tab 2) · 15 phút

**Kiến thức cần dùng**

- **LTV tính trên Gross Margin**: $\text{LTV} = \text{ARPU} \times \text{Gross Margin \%} \times (1/\text{Churn})$.
- **2 Tiêu chuẩn vàng VC**: $\text{LTV}/\text{CAC} > 3.0$ và $\text{CAC Payback} < 12 \text{ tháng}$.

### 1. Kiểm tra 4 chỉ số tại Cột Base (10')

**Làm** — Bấm sang **Tab 2 (Unit Economics)**, đối chiếu các ô kết quả tự động ở cột **Base**:

| Chỉ số | Công thức tự động | Ngưỡng an toàn (Benchmark) |
|---|---|---|
| **Gross Margin %** | $(\text{ARPU} - \text{COGS}) / \text{ARPU}$ | $\ge 50\% - 60\%$ |
| **LTV** | $\text{Gross Profit} \times (1/\text{Churn})$ | Phải tính trên Gross Profit, không tính trên Revenue |
| **LTV / CAC Ratio** | $\text{LTV} / \text{CAC}$ | **$> 3.0$ (Tiêu chuẩn vàng VC)** |
| **CAC Payback** | $\text{CAC} / \text{Gross Profit hàng tháng}$ | **$< 12 \text{ tháng}$** |

### 2. Tinh chỉnh nếu chỉ số UNHEALTHY (5')

Nếu cột Base báo `UNHEALTHY` ($\text{LTV}/\text{CAC} < 3$ hoặc $\text{Payback} > 12\text{m}$), quay lại Tab 1 điều chỉnh theo 3 hướng:
* Tăng ARPU (bổ sung tính năng giá trị cao).
* Giảm CAC (chuyển bớt sang inbound/content marketing).
* Giảm Churn (cải thiện trải nghiệm giữ chân người dùng ở Day 23).

:::checkpoint{title="GATE 2 — Unit Economics đạt chuẩn HEALTHY"}
Bạn qua gate khi: Tab 2 cột Base trả ra kết quả LTV/CAC > 3.0 và CAC Payback < 12 tháng.
:::

---

## 6. Phase 3 — Stress-test 3 Kịch bản & ROI (Tab 3) · 20 phút

**Kiến thức cần dùng**

- **NPV > 0** và **IRR $\ge 20\%$** chứng minh dự án đáng làm hơn gửi ngân hàng.
- **Pessimistic Runway $\ge 12$ tháng** đảm bảo công ty sống sót qua biến cố thị trường.

### 1. Kiểm tra kịch bản Base (10')

**Làm** — Chuyển sang **Tab 3 (P&L & ROI)**:
1. Đảm bảo ô chọn Scenario (C4) đang ở **Base**.
2. Kiểm tra 3 chỉ số tài chính dự án cuối bảng:
   - **NPV > 0** (Net Present Value dương).
   - **IRR $\ge 20\%$** (Tỷ suất sinh lời nội bộ $> 20\%$).
   - **Project Payback < 24 tháng** (Hoàn vốn toàn bộ dự án).

### 2. Stress-test kịch bản Pessimistic (10')

**Làm**
1. Đổi ô chọn Scenario (C4) sang **Pessimistic**.
2. Quan sát dòng **Cash Position (Tiền mặt tích lũy)** từ Month 1 đến Month 12:
   - Tiền mặt không được bị âm ($\mathbf{< 0}$) trước Month 12.
   - Kết luận **Runway $\ge 12$ tháng**.

Nếu tiền mặt bị âm ở Month 6-8, quay lại Tab 1 cắt giảm chi phí cố định (Fixed Cost) hoặc tăng tiền mặt dự trữ ban đầu (Initial Cash).

:::checkpoint{title="GATE 3 — Stress-test thành công"}
Bạn qua gate khi: Cột Base có NPV > 0, IRR >= 20%; đổi sang Pessimistic thì Runway đạt ít nhất 12 tháng không bị âm vốn.
:::

---

## 7. Phase 4 — Viết Decision Note bảo vệ mô hình · 15 phút

**Làm** — Viết 2–3 đoạn văn (khoảng 200–300 từ) bảo vệ mô hình tài chính theo khung cấu trúc:

1. **Lý do chọn ARPU & CAC:** Trích dẫn benchmark thị trường hoặc đối thủ tương đương giải thích vì sao chọn mức giá và chi phí đó.
2. **Bảo vệ AI Hidden Costs:** Giải thích các chi phí ẩn đã tính (Data labeling bao lâu retrain 1 lần, ai làm QA).
3. **Kết luận Sức khỏe & Plan B:** Tóm tắt LTV/CAC, Payback và phương án ứng phó nếu kịch bản Pessimistic xảy ra.

:::goal{title="Mẫu Decision Note tham khảo"}
"Chúng tôi đặt mức giá ARPU 299,000 VNĐ/tháng dựa trên benchmark các tool SaaS e-commerce tại VN, với CAC 600,000 VNĐ qua kênh Ads Facebook. Để bảo vệ Gross Margin 76.5%, chúng tôi dự trù 20,000 VNĐ/user cho AI Hidden Costs (labeling & retrain model 3 tháng/lần). Kịch bản Base đạt LTV/CAC = 4.77 và Payback 2.6 tháng. Trong kịch bản Pessimistic (Churn 15%, CAC 1M), Runway vẫn đạt 14 tháng nhờ lượng tiền mặt dự trữ 500M VNĐ."
:::

:::checkpoint{title="GATE 4 — Decision Note thuyết phục"}
Bạn qua gate khi: Decision Note giải thích rõ căn cứ chọn ARPU, CAC, Hidden Costs và nêu được thời gian Runway kịch bản Pessimistic.
:::

---

## 8. Phase 5 — Tự soi lỗi & nộp bài · 10 phút

**Làm** — Đối chiếu 6 câu tự kiểm tra trước khi nộp:

- [ ] Tab 1 điền đủ 100% ô màu vàng cho cả 3 kịch bản?
- [ ] AI Hidden Costs $\ge 30\%$ API Cost (không điền bằng 0)?
- [ ] LTV tính dựa trên Gross Margin (không tính trên Doanh thu thô)?
- [ ] Pessimistic Churn & CAC cao hơn Base ít nhất 1.5 lần?
- [ ] Tab 2 Base LTV/CAC > 3.0 và CAC Payback < 12 tháng?
- [ ] Tab 3 Pessimistic Runway $\ge 12$ tháng?

---

## 9. Quy tắc dùng AI

Được dùng AI để:
- Tra cứu benchmark ARPU, CAC, Churn rate của các ngành SaaS/AI tương đương.
- Gợi ý danh mục AI Hidden Costs phù hợp với dạng sản phẩm.

Không được dùng AI để:
- Điền thay các giả định tài chính cốt lõi.
- Bịa số ảo để vượt qua các gate kiểm tra.

---

## 10. Nộp bài

Mỗi học viên nộp bài theo cấu trúc thư mục cá nhân:

```text
Track1_Day24_MHV_HoVaTen/
├── README.md               # Họ tên, MSSV, tên dự án, Decision Note
└── [HoVaTen]_Day24.xlsx    # File Excel tài chính 3 Tabs đã hoàn thành
```

### Năm gate đánh giá (Rubric)

| Gate | Đạt khi | Dấu hiệu chưa đạt |
|---|---|---|
| 1. Giả định Tab 1 | 100% ô màu vàng có số, Hidden Costs $\ge 30\%$ API Cost | Bỏ trống ô màu vàng, Hidden Costs = 0 |
| 2. Unit Economics | LTV tính bằng Gross Margin, Base LTV/CAC > 3.0 | LTV tính bằng Revenue thô, LTV/CAC < 3.0 |
| 3. Stress-testing | Pessimistic Churn/CAC $\ge 1.5x$ Base, Runway $\ge 12\text{m}$ | Pessimistic = Base, Tiền mặt bị âm trước Month 12 |
| 4. Decision Note | Có căn cứ/benchmark bảo vệ ARPU, CAC & Hidden Costs | Viết mơ hồ, không có căn cứ |
| 5. Nộp bài | Nộp file Excel 3 Tabs + README.md đúng tên repo | Nộp sai tên file hoặc thiếu file Excel |
