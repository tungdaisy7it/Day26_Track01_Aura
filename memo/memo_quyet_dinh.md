# MEMO QUYẾT ĐỊNH ÁP DỤNG AI (AI ADOPTION DECISION MEMO)
**Dự án:** VinStay AI — Trợ lý AI Điều phối & Hỗ trợ Vận hành Căn hộ tại Vinhomes Ocean Park 1  
**Nhóm:** Aura (Track 01 — Day 26)  
**Ngày lập:** 14/10/2026  
**Người phụ trách chính:** Cao Đức Hiệp (Metrics & Decision Lead) | Phối hợp: Nguyễn Khánh Duy (Workflow Lead), Lê Thanh Tùng (Readiness Lead)  

---

## 1. VẤN ĐỀ VÀ NGUYÊN NHÂN GỐC (PROBLEM STATEMENT & ROOT CAUSE)

### A. Hiện trạng vấn đề
Sau 3 tuần triển khai thử nghiệm Trợ lý AI (VinStay Ops Assistant) cho 15 Field Host (cộng tác viên sinh viên/cư dân dẫn khách) và 3 Điều phối viên tại phân khu Sapphire 1 & 2 (Vinhomes Ocean Park 1):
* **Tỷ lệ sử dụng sụt giảm nghiêm trọng:** Chỉ còn 12% truy vấn được thực hiện qua bot (1.8/15 ca trực active). 
* **Tắc nghẽn điều phối:** 88% thắc mắc và sự cố vẫn dồn về nhóm Zalo nội bộ hoặc gọi điện thoại trực tiếp cho Trưởng ca vào khung giờ cao điểm (14h00 – 16h00 cuối tuần), gây nghẽn điều phối trung bình 28 phút/lượt.
* **Hậu quả nghiệp vụ:** Phát sinh 4 biên bản phạt từ Ban Quản lý (BQL) tòa nhà (tổng số tiền 3.500.000 VNĐ) do Host nắm sai quy chế mang đồ cồng kềnh qua thang khách và quy định đăng ký thẻ cư dân tạm.

### B. Nguyên nhân gốc đã chẩn đoán
Khác với nhận định ban đầu của ban điều hành ("nhân viên lười hoặc thiếu kỹ năng sử dụng công nghệ"), việc đào sâu chẩn đoán đã xác định **2 nguyên nhân gốc cốt lõi**:
1. **Thiếu Kiến trúc Tin cậy & Trích dẫn Nguồn kiểm chứng (Trust Architecture Gap):** Trợ lý AI đưa ra câu trả lời tổng hợp nhưng không kèm trích dẫn văn bản quy chế cụ thể của BQL, không có số hiệu văn bản và ngày hiệu lực. Bản thân quy chế giữa các phân khu (Sapphire, Zenpark, Pavilion) có sự khác biệt lớn. Khi AI trả lời sai dẫn đến việc Field Host bị bảo vệ sảnh lập biên bản phạt, **Field Host phải tự bỏ tiền túi đền bù mà không có cơ chế khiếu nại**. Do đó, Field Host chọn cách an toàn là gọi thẳng Quản lý.
2. **Thiếu Quy chuẩn Phân công Người — AI & Cơ chế Bàn giao (Governance & Handoff Gap):** Hệ thống được thả nổi như một chatbot tự do, chưa phân định ranh giới việc nào AI được tự động trả lời, việc nào cần người kiểm chứng và việc nào tuyệt đối thuộc thẩm quyền con người. Khi AI gặp câu hỏi phức tạp hoặc dữ liệu mâu thuẫn, hệ thống không có luồng ngắt mạch (Circuit-breaker) để tự động chuyển tiếp cho Điều phối viên, dẫn đến tình trạng AI "bịa chuyện" (Hallucination) gây mất niềm tin hoàn toàn.

---

## 2. FRAMEWORK ĐÃ DÙNG VÀ BẰNG CHỨNG (DIAGNOSTIC FRAMEWORKS & EVIDENCE)

Nhóm Aura đã áp dụng kết hợp 3 framework bổ trợ lẫn nhau, cùng hướng tới việc giải quyết điểm nghẽn niềm tin:

### A. Gartner-Lite (Độ sẵn sàng của tổ chức)
* **Direction (Hướng đi):** **ĐẠT.** Mục tiêu giải phóng sức lao động cho quản lý và rút ngắn thời gian tiếp đón khách tại sảnh được toàn bộ đội ngũ đồng thuận.
* **Readiness (Độ sẵn sàng):** **THIẾU NGHIÊM TRỌNG.** 
  - *Dữ liệu:* Kho quy chế BQL bị phân mảnh ở 4 file PDF cũ, chưa có Data Owner chịu trách nhiệm chuẩn hóa vector database khi BQL ra thông báo mới.
  - *Governance:* Chưa có quy chế bồi hoàn rủi ro (Risk Waiver Policy) cho nhân viên tuyến đầu khi làm đúng khuyến nghị của AI.
* **Absorption (Khả năng hấp thụ):** **THIẾU.** Chưa thiết kế kênh phản hồi lỗi (Flagging feedback loop) để hệ thống học từ các ca xử lý sai.

### B. Mollick (Jagged Frontier — Ranh giới công việc Người & AI)
Tái định nghĩa lại 3 vùng ranh giới:
* **Vùng Người làm (Human Territory):** Giữ quyền phê duyệt cuối cùng về chi phí đền bù, miễn giảm phí cọc, xử lý khủng hoảng với BQL sảnh và chịu trách nhiệm pháp lý.
* **Vùng AI hỗ trợ (Centaur/Cyborg Territory):** AI trích lục nhanh điều khoản quy chế, tính toán chi phí cọc/phí lưu trú phát sinh và soạn sẵn bản nháp tin nhắn; **Field Host kiểm tra tính chính xác của nguồn trích dẫn trước khi bấm xác nhận gửi**.
* **Vùng AI tự động (Automated Territory):** Chỉ tự động hóa việc đồng bộ lịch hẹn xem phòng và gửi mã OTP qua Zalo ZNS khi dữ liệu đã chuẩn hóa 100%.

### C. ADKAR (Điểm nghẽn cá nhân người dùng)
* **Awareness (Nhận thức):** ĐẠT (Host hiểu AI giúp tra cứu nhanh).
* **Desire (Động lực/Mong muốn):** **NGHẼN NẶNG NHẤT.** Host sợ bị BQL phạt tiền túi và sợ mất uy tín với khách khi AI trả lời sai.
* **Knowledge & Ability:** ĐẠT (Giao diện Telegram/Mobile Web rất dễ bấm).
* **Reinforcement (Duy trì hành vi):** **NGHẼN.** Đánh giá KPI của Host chỉ đo số lượt dẫn phòng, không gắn liền với việc tuân thủ quy trình chuẩn hóa.

### D. Bằng chứng thực tế (Empirical Evidence)
1. **Dữ liệu Log tương tác:** Audit log trên Telegram Bot cho thấy trong tuần thứ 3, có 42 lượt hỏi nhưng chỉ có 5 lượt bấm "Hài lòng", 8 lượt người dùng gõ câu lệnh "bot trả lời linh tinh", sau đó Host chuyển sang gọi điện thoại cho Quản lý ca.
2. **Đối chiếu thực tiễn ngành (Case Study):** Bài học từ **DWP / GDS** và **Morgan Stanley** chỉ ra rằng việc mở rộng quy mô (Scale) khi độ tin cậy và nguồn kiểm chứng chưa hoàn thiện sẽ dẫn tới sụp đổ niềm tin người dùng. Đo lường giá trị thực tế từ log quy trình luôn đáng tin hơn số lượt login bề nổi.

---

## 3. ÍT NHẤT 2 THAY ĐỔI SAU PHẢN BIỆN CHÉO (POST-PEER REVIEW CHANGES)

Tại Chặng 3, nhóm Aura đã tiến hành phản biện chéo với **Nhóm 03** và tiếp nhận 2 đóng góp quan trọng để nâng cấp từ bản v1 lên bản v2:

1. **Thay đổi 1 — Bãi bỏ đào tạo cơ học, ban hành "Quỹ bảo hiểm rủi ro vận hành" (Risk Waiver Policy):**
   * *Trước phản biện (Bản v1):* Đề xuất mở thêm 2 buổi workshop hướng dẫn kỹ năng viết prompt cho Field Host (mắc lỗi thường gặp §5.3: mặc định giải quyết bằng đào tạo).
   * *Góp ý từ nhóm bạn:* Phân tích ADKAR cho thấy nhân viên kẹt ở *Desire* (sợ rủi ro mất tiền phạt) chứ không phải thiếu kiến thức (*Knowledge*). Đào tạo không thể giải quyết được nỗi sợ bị phạt tiền.
   * *Sau phản biện (Bản v2):* Ban hành chính sách: **Nếu Field Host thao tác đúng theo quy trình và trích dẫn văn bản được AI cung cấp mà vẫn bị BQL xử phạt, Công ty cam kết trích Quỹ rủi ro chi trả 100% tiền phạt**. Điều này giải tỏa triệt để rào cản tâm lý của Host.
2. **Thay đổi 2 — Tái cấu trúc Dashboard từ Activity sang Workflow Metric & Cơ chế Ngắt mạch (Circuit-Breaker):**
   * *Trước phản biện (Bản v1):* Dashboard đo số lượt login và số câu hỏi/ngày; cột "Khi chỉ số xấu" chỉ ghi chung chung là "nhắc nhở nhân viên".
   * *Góp ý từ nhóm bạn:* Chỉ số đo lường không gắn với quyết định tác chiến; cần đẩy lên tầng 4 và tầng 5 theo quy chuẩn bài học.
   * *Sau phản biện (Bản v2):* Chuyển thành **"Tỷ lệ ca xử lý hoàn tất tại sảnh không cần gọi quản lý"** (Target $\ge 80\%$) và **"Tỷ lệ phản hồi có nguồn kiểm chứng"** (Target $\ge 98\%$). Cột "Khi chỉ số xấu" thiết lập cơ chế kỹ thuật: Nếu tỷ lệ trích nguồn $<95\%$, hệ thống tự động khóa chế độ AI sinh văn bản tự do, chuyển toàn bộ câu hỏi sang Hotline Điều phối viên trong vòng 60 giây.

---

## 4. QUYẾT ĐỊNH CHÍNH THỨC (FINAL DECISION)

### 👉 QUYẾT ĐỊNH: **SỬA (RESTRUCTURE & PILOT RECOVERY)**

* **Lý do (1 câu duy nhất):**  
  > *"Không dừng dự án vì bài toán giảm tải tắc nghẽn cho đội ngũ quản lý là nhu cầu sống còn; nhưng không mở rộng (Scale) vì mức sẵn sàng dữ liệu và niềm tin chưa đạt — nhóm quyết định tái cấu trúc triệt để Kiến trúc tin cậy và chính sách bảo hiểm rủi ro trong phạm vi hẹp tại Sapphire 1 trước khi xem xét mở rộng."*

---

## 5. CÁC BƯỚC TIẾP THEO VÀ PHÂN CÔNG OWNER (NEXT STEPS & ROADMAP)

| Mốc thời gian | Trọng tâm công việc | Đầu ra bắt buộc (Deliverables) | Người chịu trách nhiệm (Owner) |
| :--- | :--- | :--- | :--- |
| **0 – 30 Ngày**<br>*(Chứng minh vấn đề & Niềm tin)* | - Chuẩn hóa kho văn bản quy chế BQL Sapphire 1 & 2 thành dạng số có siêu dữ liệu ngày hiệu lực.<br>- Tích hợp tính năng bắt buộc trích nguồn vào bot.<br>- Ban hành văn bản chính sách Bảo hiểm rủi ro vận hành (Risk Waiver). | - Kho dữ liệu Vector DB đã gắn nhãn Data Owner.<br>- Tỷ lệ phản hồi AI có trích nguồn đạt $\ge 98\%$.<br>- 100% Host ký nhận chính sách bảo hiểm rủi ro. | **Lê Thanh Tùng**<br>*(Readiness & Governance Lead)* |
| **31 – 60 Ngày**<br>*(Chứng minh chất lượng & Năng suất)* | - Triển khai quy trình QA kiểm định ngẫu nhiên 50 truy vấn/tuần.<br>- Thiết lập cơ chế ngắt mạch tự động đẩy cuộc gọi sang Quản lý ca nếu thời gian tra cứu $>8$ phút.<br>- Khảo sát đo lường lại điểm nghẽn ADKAR sau 30 ngày áp dụng chính sách mới. | - Tỷ lệ First-Contact Resolution đạt $\ge 80\%$.<br>- Thời gian xử lý sự cố giảm từ 28 phút xuống $\le 8$ phút.<br>- Báo cáo audit chất lượng tuần có xác nhận của QA. | **Nguyễn Khánh Duy**<br>*(Workflow & AI Architect)* |
| **61 – 90 Ngày**<br>*(Đánh giá Gate & Quyết định Mở rộng)* | - Đánh giá toàn diện 5 tầng Dashboard v2.<br>- So sánh chi phí phạt BQL và điểm CSAT khách thuê so với mốc ban đầu.<br>- Họp Gate 3 quyết định có đóng gói nhân rộng sang phân khu Zenpark và Pavilion hay không. | - Bảng tổng kết tài chính (giảm tiền phạt BQL về 0 VNĐ, CSAT $\ge 4.8/5.0$).<br>- Biên bản nghiệm thu Gate 3 trình Giám đốc Vận hành. | **Cao Đức Hiệp**<br>*(Change & Metrics Lead)* |
