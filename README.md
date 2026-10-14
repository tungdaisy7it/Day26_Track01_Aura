# Day26_Track01_Aura — AI Adoption & Change Management
**Chương trình:** AI Engineering Track 01 — Day 26 Lab  
**Tên nhóm:** Aura  
**Dự án ứng dụng:** VinStay AI — Trợ lý AI Điều phối & Hỗ trợ Vận hành Căn hộ tại Vinhomes Ocean Park 1  

---

## 1. BẢNG THÀNH VIÊN VÀ ĐÓNG GÓP (MEMBER CONTRIBUTIONS & PEER REVIEW)

| Họ tên | MSSV | Phần phụ trách | Góp ý đã đưa cho nhóm bạn (Chặng 3) |
| :--- | :--- | :--- | :--- |
| **Nguyễn Khánh Duy** | **2A202602403** | **Workflow & Trust Architecture Lead:** Khóa phạm vi bài toán (§4.1); Phân bổ ranh giới Người–AI theo Mollick (§4.2); Tái thiết kế quy trình AS-IS vs TO-BE với 3 thay đổi bắt buộc và kiến trúc tin cậy 5 bước (§4.3); Quản trị Repo Git và tổng hợp kỹ thuật. | **Góp ý cho Nhóm 03 (Dự án EdTech AI):** Quy trình TO-BE của nhóm chưa có cơ chế bàn giao người (Human Handoff) khi AI gặp bài toán khó; đề xuất bổ sung bước QA mẫu ngẫu nhiên 10% và gắn Data Owner cho ngân hàng đề thi thay vì chỉ có AI sinh tự do. |
| **Lê Thanh Tùng** | **2A202602499** | **Readiness & Governance Lead:** Chẩn đoán mức độ sẵn sàng tổ chức theo Gartner-Lite 3 trục (§4.2); Thu thập và phân tích bằng chứng thực tế từ log tương tác và case study ngành (§4.2); Thiết lập Lộ trình 30-60-90 ngày kèm tiêu chí kiểm soát Gate và phân công Owner từng giai đoạn (§4.4). | **Góp ý cho Nhóm 03 (Dự án EdTech AI):** Lộ trình 30-60-90 ngày đang bị viết như một danh sách việc cần làm (to-do list); đề xuất bổ sung tiêu chí nghiệm thu Gate dựa trên chất lượng và tỷ lệ chấm lại của giáo viên thay vì tính theo ngày lịch cứng. |
| **Cao Đức Hiệp** | **2A202602550** | **Change Management & Metrics Lead:** Chẩn đoán điểm nghẽn hành vi người dùng theo ADKAR (§4.2); Thiết lập bảng Dashboard Hành Động 5 tầng đo lường từ sử dụng đến giá trị (bản v1 và v2) (§4.5); Soạn thảo Memo Quyết định 5 phần và giải trình cải tiến (§6.5). | **Góp ý cho Nhóm 03 (Dự án EdTech AI):** Dashboard của nhóm mới chỉ dừng ở Activity metric (số lượt học sinh đặt câu hỏi); đề xuất nâng lên Workflow metric (tỷ lệ học sinh tự giải được bài sau khi xem gợi ý của AI) và bổ sung hành động cụ thể khi chỉ số rơi vào vùng xấu. |

---

## 2. PHẠM VI (SCOPE)
* **Sản phẩm AI:** Trợ lý AI Điều phối & Hỗ trợ Vận hành Căn hộ (VinStay Ops Assistant - Telegram Bot & Mobile Portal).
* **Nhóm người dùng chính:** 15 Field Host (cộng tác viên sinh viên/cư dân đón khách) & 3 Điều phối viên Vận hành CSKH tại Sapphire 1 & 2 (Vinhomes Ocean Park 1).
* **2–4 Quy trình liên quan:** (1) Tra cứu chính sách nhận phòng / quy chế tòa nhà / phí BQL; (2) Tạo lịch hẹn đón khách & đối soát mã OTP vào sảnh; (3) Hướng dẫn xử lý sự cố hiện trường tại sảnh.

---

## 3. NGUYÊN NHÂN GỐC (ROOT CAUSE)
* **Nguyên nhân 1 (Trust & Governance):** AI thiếu cơ chế trích dẫn nguồn văn bản BQL có ngày hiệu lực và chưa có quy chế bảo hiểm rủi ro cho Host khi AI sai sót, dẫn tới tâm lý sợ bị BQL phạt tiền túi (chẩn đoán qua **Gartner-Lite** và **ADKAR - Desire**).
* **Nguyên nhân 2 (Workflow & Boundary):** Chưa phân định ranh giới thẩm quyền theo **Mollick**, thiếu khâu kiểm chứng của con người (Human-in-the-loop) và thiếu vòng phản hồi báo lỗi.
* **Bằng chứng xác thực:** Log hệ thống Telegram Bot tuần 3 ghi nhận 42 lượt hỏi nhưng chỉ có 5 lượt hài lòng (88% ca quay lại gọi điện cho Quản lý ca); đối chiếu bài học từ case study **DWP/GDS** và **Morgan Stanley** về độ tin cậy phải đi trước việc mở rộng quy mô.

---

## 4. CÁCH LÀM MỚI (NEW WORKFLOW & TRUST ARCHITECTURE)
* **Kiến trúc tin cậy (Trust Architecture):** `Kho dữ liệu chuẩn hóa BQL → Trích nguồn văn bản & ngày hiệu lực → QA kiểm tra mẫu 50 ca/tuần → Chuyển người (Human Handoff qua Hotline 60s) → Vòng lặp phản hồi lỗi`.
* **Ba thay đổi bắt buộc:**
  1. *Nguồn kiểm chứng:* 100% câu trả lời của AI bắt buộc đính kèm số hiệu văn bản BQL và ngày hiệu lực.
  2. *Người chịu trách nhiệm:* Phân định ranh giới Mollick — AI tạo bản nháp/tính toán, Field Host kiểm tra nguồn, Quản lý ca trực phê duyệt ngoại lệ và chịu trách nhiệm pháp lý.
  3. *Cách xử lý khi AI không chắc:* Tự động kích hoạt cơ chế ngắt mạch (Circuit-Breaker), khóa câu trả lời tự do và chuyển tiếp cuộc gọi tới Hotline Quản lý ca trong vòng 60 giây; kích hoạt chính sách Bảo hiểm rủi ro vận hành (Risk Waiver).

---

## 5. CHỈ SỐ QUYẾT ĐỊNH (DECISION METRICS)
* **Product-level Metric:** Tỷ lệ phản hồi AI có trích dẫn văn bản quy chế BQL & ngày hiệu lực hợp lệ (Baseline: **0%** $\rightarrow$ Target: **$\ge 98\%$** | Nguồn: Vector DB Audit Log | Owner: **Nguyễn Khánh Duy** | Khi xấu: Khóa chế độ sinh văn bản tự do, chuyển sang FAQ cố định).
* **Workflow-level Metric:** Tỷ lệ ca sự cố được giải quyết tại sảnh không cần leo thang lên Quản lý ca trực (Baseline: **22%** $\rightarrow$ Target: **$\ge 80\%$** | Nguồn: Ticket Escalation Log | Owner: **Lê Thanh Tùng** | Khi xấu: Kích hoạt Quỹ bảo hiểm rủi ro và Quản lý trực tiếp ngồi kèm).
* **Năng suất & Giá trị:** Thời gian giải quyết sự cố tại hiện trường giảm từ **28 phút** xuống **$\le 8$ phút** (Owner: **Cao Đức Hiệp**); Chi phí phạt vi phạm BQL giảm từ **3.500.000 VNĐ/tháng** về **0 VNĐ**.

---

## 6. QUYẾT ĐỊNH (DECISION)
* **Quyết định:** **SỬA (RESTRUCTURE & PILOT RECOVERY)**.
* **Lý do (1 câu):** *Không dừng vì nhu cầu giảm tải cho quản lý ca là sống còn; không mở rộng vội vì độ sẵn sàng dữ liệu chưa đạt — nhóm tập trung tái cấu trúc Kiến trúc tin cậy và chính sách bảo hiểm rủi ro trong phạm vi hẹp tại Sapphire 1 trước khi mở rộng.*
* **Hai thay đổi cốt lõi so với bản v1 sau phản biện:**
  1. *Thay đổi 1:* Bãi bỏ đề xuất đào tạo cơ học, ban hành **"Quỹ bảo hiểm rủi ro vận hành (Risk Waiver Policy)"** bồi hoàn 100% tiền phạt nếu Host làm đúng nguồn AI trích dẫn (giải tỏa điểm nghẽn *Desire*).
  2. *Thay đổi 2:* Chuyển đổi toàn bộ Activity metrics sang **Decision metrics** (Đo lường tỷ lệ First-Contact Resolution và tỷ lệ trích nguồn văn bản) kèm cơ chế ngắt mạch kỹ thuật Circuit-Breaker khi chỉ số rơi vào vùng xấu.

---

## 7. CẤU TRÚC THƯ MỤC DỰ ÁN & TÀI LIỆU CHI TIẾT
```text
Day26_Track01_Aura/
├── README.md                                  # Tài liệu tổng quan (Người chấm mở đầu tiên)
├── dashboard/
│   └── dashboard_hanh_dong_v2.xlsx            # Dashboard Hành Động bản v2 (Có sheet giải trình đối chiếu)
├── memo/
│   └── memo_quyet_dinh.md                     # Memo quyết định áp dụng AI (5 phần theo chuẩn §6.5)
├── v1/
│   └── dashboard_hanh_dong_v1.xlsx            # Dashboard Hành Động bản v1 (Dùng đối chiếu tiêu chí)
├── NGUYEN_KHANH_DUY_WORK.md                  # Hồ sơ công việc chi tiết của Nguyễn Khánh Duy (Workflow & Architecture)
├── LE_THANH_TUNG_WORK.md                     # Hồ sơ công việc chi tiết của Lê Thanh Tùng (Readiness & Governance)
└── CAO_DUC_HIEP_WORK.md                      # Hồ sơ công việc chi tiết của Cao Đức Hiệp (Change Management & Metrics)
```
