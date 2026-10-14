# HỒ SƠ CÔNG VIỆC & ĐÓNG GÓP CÁ NHÂN (INDIVIDUAL WORK LOG)
**Thành viên:** Nguyễn Khánh Duy  
**MSSV:** 2A202602403  
**Nhóm:** Aura (Track 01 — Day 26)  
**Vai trò phụ trách chính:** Workflow & Trust Architecture Lead  
**Dự án:** VinStay AI — Trợ lý AI Điều phối & Hỗ trợ Vận hành Căn hộ tại Vinhomes Ocean Park 1  

---

## 1. PHẠM VI TRÁCH NHIỆM CHÍNH (ASSIGNED SCOPE)
Trong bài Lab Day 26 (AI Adoption & Change Management), tôi chịu trách nhiệm dẫn dắt và thực thi các nội dung kỹ thuật trọng tâm:
1. **Khóa phạm vi bài toán (§4.1):** Định vị chính xác sản phẩm AI, nhóm người dùng tuyến đầu, 3 quy trình then chốt và vấn đề đo lường được.
2. **Chẩn đoán ranh giới công việc Người – AI theo Mollick (§4.2):** Áp dụng lý thuyết Jagged Frontier để phân tách rõ việc nào thuộc về con người, việc nào AI hỗ trợ và việc nào tự động hóa có kiểm soát.
3. **Tái thiết kế quy trình AS-IS vs TO-BE (§4.3):** Vẽ sơ đồ so sánh trực quan, đảm bảo đủ **3 thay đổi bắt buộc** (Nguồn kiểm chứng • Người chịu trách nhiệm • Xử lý khi AI không chắc).
4. **Xây dựng Kiến trúc Tin cậy (Trust Architecture - §4.3):** Thiết lập chuỗi 5 mắt xích bảo đảm chất lượng dữ liệu và cơ chế ngắt mạch kỹ thuật (Circuit-Breaker).
5. **Tham gia phản biện chéo (Chặng 3):** Trực tiếp kiểm tra quy trình của nhóm bạn và đóng góp giải pháp bổ sung khâu bàn giao người (Human Handoff).

---

## 2. CHI TIẾT KẾT QUẢ THỰC HIỆN CÁC BƯỚC

### 📌 Bước 1: Khóa phạm vi bài toán cụ thể (§4.1)
Tôi đã cùng nhóm xác lập một phạm vi hẹp, có thể quan sát và đo lường trực tiếp, không nói chung chung về "ứng dụng AI cho doanh nghiệp":
* **Sản phẩm AI:** Trợ lý AI Điều phối & Hỗ trợ Vận hành Căn hộ (VinStay Ops Assistant tích hợp qua Telegram Bot và Web Portal trên di động).
* **Nhóm người dùng chính:** 15 Field Host (sinh viên VinUni & cư dân làm việc bán thời gian theo ca đón khách) và 3 Điều phối viên Vận hành CSKH tại phân khu Sapphire 1 & 2 (Vinhomes Ocean Park 1).
* **3 Quy trình cốt lõi:**
  1. *Quy trình 1 — Tra cứu quy chế tòa nhà & chính sách BQL:* Phí sử dụng tiện ích (bể bơi, BBQ), quy định thẻ cư dân thang máy, cọc chuyển đồ, khung giờ được phép phát sinh tiếng ồn.
  2. *Quy trình 2 — Tạo lịch hẹn đón khách & đối soát mã OTP sảnh:* Xác thực khách thuê từ ứng dụng, đồng bộ giờ đón với bảo vệ sảnh S1.02 và S2.05.
  3. *Quy trình 3 — Xử lý sự cố hiện trường tại sảnh (Field Incident):* Khách trễ hẹn quá 15 phút, lỗi mật mã khóa cửa căn hộ, tranh chấp phí phát sinh ngoài hợp đồng.
* **Vấn đề đo lường được:** Sau 3 tuần triển khai, tỷ lệ sử dụng bot sụt giảm còn 12% (1.8/15 ca trực active); 88% thắc mắc vẫn chuyển thành cuộc gọi cho Quản lý ca trực, làm tắc nghẽn hỗ trợ trung bình 28 phút/lượt.

---

### 📌 Bước 2: Chẩn đoán ranh giới Người — AI theo Mollick (§4.2)
Tôi áp dụng mô hình **Jagged Frontier (Ethan Mollick)** để phân định ranh giới công việc, chấm dứt tình trạng thả nổi chatbot:
* **Vùng 1: Người làm (Human Territory — Giữ quyền quyết định & chịu trách nhiệm):**
  * *Nội dung:* Phê duyệt các khoản miễn giảm phí cọc cho khách, quyết định hướng xử lý khi xảy ra xung đột với BQL sảnh, đại diện pháp lý và ký nhận biên bản bàn giao phòng.
  * *Nguyên tắc:* AI tuyệt đối không được tự động ra quyết định tài chính hoặc pháp lý.
* **Vùng 2: AI hỗ trợ (Centaur / Cyborg Territory — AI làm bản nháp, Người kiểm chứng):**
  * *Nội dung:* Khi Field Host nhận thắc mắc từ khách (VD: "Có được mang thú cưng vào Sapphire 1 không?"), AI trích xuất nhanh điều 14 Quy chế BQL ban hành ngày 15/08/2026, tóm tắt điều kiện và soạn sẵn mẫu tin nhắn phản hồi lịch sự.
  * *Nguyên tắc:* Field Host bắt buộc phải đọc lại, kiểm tra số hiệu văn bản trước khi bấm gửi khách.
* **Vùng 3: AI tự động (Automated Territory — Tự động hóa có kiểm soát):**
  * *Nội dung:* Tự động kích hoạt tin nhắn gửi mã OTP cho khách thuê trước giờ hẹn 30 phút và gửi thông báo nhắc lịch cho Field Host. Chỉ áp dụng cho tác vụ chuẩn hóa 100%, lặp lại và không có rủi ro pháp lý.

---

### 📌 Bước 3: Thiết kế lại quy trình (AS-IS vs TO-BE) & Kiến trúc Tin cậy (§4.3)

#### Sơ đồ đối chiếu quy trình AS-IS vs TO-BE:
```text
[QUY TRÌNH CŨ - AS-IS]
Khách hỏi tại sảnh ───> Host lúng túng ───> Hỏi thử AI Bot ───> AI trả lời không trích nguồn
                                                │
                                                ▼ (Host sợ bị phạt tiền)
                                          Bỏ qua bot ───> Gọi điện cho Quản lý ca ───> Nghẽn 28 phút!

====================================================================================================

[QUY TRÌNH MỚI - TO-BE]
Khách hỏi tại sảnh ───> Host tra cứu Bot chuẩn ───> AI trả lời ĐÍNH KÈM SỐ HIỆU VĂN BẢN & NGÀY HIỆU LỰC
                                                            │
                     ┌──────────────────────────────────────┴──────────────────────────────────────┐
                     ▼                                                                             ▼
           [ĐỘ TIN CẬY CAO ≥95%]                                                         [AI KHÔNG CHẮC CHẮN <95%]
Host kiểm tra nguồn trong 30 giây                                                 Kích hoạt CIRCUIT-BREAKER tức thì
Host bấm xác nhận gửi cho khách                                                   Hệ thống chuyển máy Hotline Quản lý ca (60s)
(Được bảo vệ bởi Quỹ bảo hiểm rủi ro)                                             Quản lý trả lời & Hệ thống ghi log để học lỗi
```

#### Thiết kế 5 mắt xích Kiến trúc Tin cậy (Trust Architecture):
1. **Nguồn dữ liệu (Source of Truth):** 100% tài liệu quy chế BQL Vinhomes Ocean Park được số hóa thành vector database, có gán nhãn người phụ trách (Data Owner) và thời hạn cập nhật hàng tháng.
2. **Trích nguồn bắt buộc (Source Citation):** Mọi câu trả lời của AI đều có cấu trúc: `[Nội dung tóm tắt] + [Căn cứ: Điều X, Quy chế BQL S1-S2 ban hành DD/MM/YYYY] + [Link mở PDF gốc]`.
3. **QA mẫu ngẫu nhiên (Sample Quality Audit):** Định kỳ mỗi tuần kiểm định ngẫu nhiên 50 truy vấn để rà soát tỷ lệ hallucination.
4. **Chuyển người (Human Handoff):** Khi AI nhận diện độ tự tin dưới ngưỡng an toàn, hệ thống tự động rung máy và chuyển tiếp cuộc gọi tới Hotline Quản lý ca trực trong vòng 60 giây.
5. **Vòng phản hồi (Feedback Loop):** Nút bấm báo lỗi "Sai thực tế" trên bot để chuyển ca lỗi về cho Data Owner cập nhật lại dữ liệu ngay trong vòng 2 giờ.

---

### 📌 Đóng góp trong Chặng 3: Phản biện chéo cho Nhóm 03 (Dự án EdTech AI)
* **Nội dung tôi phản biện:** Nhóm 03 xây dựng Trợ lý AI giải bài tập cho học sinh nhưng quy trình TO-BE thả nổi hoàn toàn cho AI trả lời mà không có bước kiểm soát giáo viên. Nếu AI giải sai công thức hoặc ra kết quả ảo tưởng, học sinh sẽ tiếp thu sai lệch.
* **Đề xuất cụ thể của tôi:** Yêu cầu Nhóm 03 bổ sung khâu **Human-in-the-loop**: Chỉ tự động hiển thị đáp án với các bài toán đã có trong ngân hàng đề chuẩn; đối với câu hỏi mở hoặc dạng bài mới, AI chỉ đưa ra gợi ý bước giải (hints), đồng thời gửi cảnh báo cho Giáo viên phụ trách môn kiểm duyệt trước khi học sinh xem.

---

## 3. TỰ ĐÁNH GIÁ VÀ CAM KẾT ĐÓNG GÓP
* **Mức độ hoàn thành:** 100% khối lượng công việc được phân công.
* **Tính đồng bộ:** Các kết quả phân tích về Mollick và quy trình TO-BE ăn khớp hoàn toàn với chẩn đoán Gartner-Lite của Lê Thanh Tùng và Dashboard chỉ số của Cao Đức Hiệp.
* **Chữ ký xác nhận:** *Nguyễn Khánh Duy*
