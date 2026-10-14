# NHẬT KÝ CÔNG VIỆC & ĐÓNG GÓP DỰ ÁN VINSTAY AI
**Thành viên:** Cao Đức Hiệp  
**MSSV:** 2A202602550  
**Team:** Aura  
**Vai trò cốt lõi (Core Role):** Backend & Data / AI Engineer  
**Dự án:** VinStay AI — Hệ điều hành Cho thuê & Vận hành Căn hộ Tinh gọn (Asset-Light) tại Vinhomes Ocean Park

---

## 1. PHẠM VI TRÁCH NHIỆM TRONG DỰ ÁN VINSTAY AI (TECHNICAL SCOPE)

### A. Tầng Dịch vụ Lõi Backend & AI Agent (FastAPI / LangGraph)
- **LangGraph Matching Agent:** Xây dựng StateGraph, các Node xử lý và Tool calling lọc căn hộ theo ngân sách trần, vị trí tòa, số phòng ngủ và tiện ích nội thất; kiểm soát độ trễ phản hồi LLM < 2 giây.
- **Dynamic Pricing Engine:** Phát triển module tính toán giá thuê biến đổi theo ngày thường/cuối tuần và mùa cao điểm du lịch biển hồ tại Ocean Park.
- **Cơ sở Dữ liệu & Tìm kiếm Vector (Supabase PostgreSQL / Prisma):** Thiết kế database schema quản lý căn hộ, lịch đặt phòng, trạng thái phòng (`available`, `holding`, `rented`, `unlisted`) và tích hợp pgvector để tìm kiếm căn hộ tương đồng ngữ nghĩa.

### B. Bảo mật Dữ liệu & Pipeline OCR CCCD (Data Privacy & Compliance)
- **Zero-Storage Ephemeral OCR:** Hiện thực hóa quy trình bóc tách thông tin cá nhân từ ảnh chụp Căn cước công dân (CCCD) để tự động điền vào hợp đồng thuê điện tử.
- **Tuân thủ Nghị định 13/2023/NĐ-CP:** Thiết lập cơ chế tiêu hủy ảnh CCCD tức thì khỏi bộ nhớ đệm (RAM/Disk) ngay sau khi trích xuất dữ liệu thành công; tuyệt đối không lưu trữ ảnh giấy tờ tùy thân của khách thuê trên server.
- **Tự động hóa Khai báo Tạm trú:** Cấu trúc hóa dữ liệu khách thuê sẵn sàng xuất file định dạng chuẩn phục vụ đăng ký tạm trú với Công an xã Đa Tốn / Gia Lâm trong vòng 2 giờ.

---

## 2. ĐÓNG GÓP CHI TIẾT TRONG BÀI LAB DAY 25 (AI TEAM LAB)

### 📌 Phase 1: Danh sách Stakeholder độc lập (Góc nhìn Dữ liệu, Backend & An ninh)
Trong bước làm việc cá nhân, tôi đã tự liệt kê 6 stakeholder cụ thể gắn liền với kiến trúc dữ liệu và an toàn thông tin:
1. **Công an khu vực / Cảnh sát phụ trách cư trú KĐT Ocean Park:** Bên tiếp nhận hồ sơ tạm trú; cần dữ liệu số hóa chuẩn xác, minh bạch.
2. **Khách thuê lo ngại rủi ro rò rỉ dữ liệu cá nhân:** Cần bằng chứng cam kết về cơ chế Zero-Storage OCR để an tâm chụp ảnh CCCD.
3. **Đơn vị cung cấp hạ tầng Cloud & LLM API (OpenAI / Anthropic):** Đảm bảo tính sẵn sàng (99.9% Uptime) và chi phí vận hành token tối ưu.
4. **20 Chủ nhà gửi độc quyền căn hộ:** Cung cấp thông tin chi tiết về giá trần, nội thất và quy chế căn hộ để nạp vào Database.
5. **Mentor công nghệ AI20K (VinUni):** Đánh giá độ tin cậy của Matching Agent và kiểm tra bộ benchmark đo lường độ trễ hệ thống.
6. **Mạng lưới Field Host dự phòng:** Cần hệ thống backend gửi thông báo ca trực tự động qua Webhook / Push API không bị chậm trễ.

### 📌 Phase 2: Bản nháp Pitch & Trách nhiệm RACI
- **Bản nháp Pitch cá nhân (Góc nhìn Dữ liệu & An ninh thông tin):**
  > *"Kính gửi BQL Ocean Park: VinStay AI giải quyết bài toán an ninh cư trú bằng công nghệ AI khớp căn chuẩn xác và Zero-Storage OCR CCCD. Chúng tôi tự động hóa trích xuất thông tin khách thuê hợp pháp trong 15 giây mà không lưu trữ ảnh CCCD, sẵn sàng chuyển thông tin khai báo tạm trú tức thì. Khách không thể tự ý vào tòa nhà nếu không có mã đặt chỗ và Field Host bảo lãnh đón sảnh. Đề xuất buổi làm việc 30 phút để kiểm tra hệ thống bảo mật và cơ chế cấp quyền."*
- **Trách nhiệm trong ma trận RACI:**
  - **Accountable (A) - Chịu trách nhiệm chính:**
    * *Đầu việc 2:* Xây dựng LangGraph Matching Agent & Dynamic Pricing.
    * *Đầu việc 3:* Xây dựng Zero-Storage OCR CCCD & Ký số điện tử.
  - **Responsible (R) - Thực hiện trực tiếp:**
    * *Đầu việc 4:* Phối hợp cùng Frontend tích hợp APIs tra cứu All-in Cost.
    * *Đầu việc 5:* Tham gia thiết lập 50 Golden Test Cases và đo lường độ trễ trên backend.

### 📌 Phase 4: Đánh giá Team Health & Cam kết Growth Plan 30 ngày
- **Điểm tự chấm sức khỏe nhóm (Team Health):**
  * *Chất lượng AI:* **4.0/5** (Matching logic và pipeline backend chạy ổn định, độ trễ tốt).
  * *Tiến độ:* **4.5/5** (Đạt chỉ tiêu các Sprint đúng hạn).
  * *Tinh thần team:* **4.5/5** (Nhóm phối hợp ăn ý, xử lý blocker kỹ thuật nhanh).
  * *Tốc độ ra sản phẩm:* **3.0/5** (Điểm thấp nhất vì mỗi lần sửa prompt/code đều phải test tay thủ công qua Swagger/Postman, chưa có test tự động).
- **Cam kết hành động trong Growth Plan 30 ngày:**
  * **Hành động phụ trách (Owner):** Xây dựng bộ dataset 50 golden test cases cho Matching Agent và thiết lập script chạy eval tự động trên GitHub Actions (CI/CD).
  * **Deadline:** 27/10/2026.
  * **Kết quả đo lường (Dấu hiệu hoàn thành):** Script `pytest tests/eval/` chạy tự động trên mỗi Pull Request; độ chính xác khớp căn (Precision/Recall) đạt **≥ 90%** trên 50 cases kiểm thử.

---

## 3. HƯỚNG DẪN TỰ PUSH COMMIT ĐÓNG GÓP LÊN GITHUB (DÀNH CHO HIỆP)
Để tài khoản GitHub của bạn (`Cao Đức Hiệp`) có commit và hiển thị trong danh sách Contributors của repo `Track1_Day25_Aura_VinStayAI`, bạn có thể thực hiện trên máy của mình:

```bash
# 1. Clone repo về máy (nếu chưa clone)
git clone https://github.com/tungdaisy7it/Track1_Day25_Aura_VinStayAI.git
cd Track1_Day25_Aura_VinStayAI

# 2. Tạo branch cá nhân
git checkout -b feature/hiep-backend-data

# 3. Thêm file CAO_DUC_HIEP_WORK.md vào thư mục và commit
git add CAO_DUC_HIEP_WORK.md
git commit -m "docs(hiep): add backend architecture task log and automated eval plan"

# 4. Push lên GitHub
git push -u origin feature/hiep-backend-data
```
*Sau đó tạo Pull Request trên giao diện web GitHub và merge vào `main` để lịch sử đóng góp hiển thị trọn vẹn!*
