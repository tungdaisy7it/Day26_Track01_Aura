# HỒ SƠ CÔNG VIỆC & ĐÓNG GÓP CÁ NHÂN (INDIVIDUAL WORK LOG)
**Thành viên:** Lê Thanh Tùng  
**MSSV:** 2A202602499  
**Nhóm:** Aura (Track 01 — Day 26)  
**Vai trò phụ trách chính:** Readiness & Governance Lead  
**Dự án:** VinStay AI — Trợ lý AI Điều phối & Hỗ trợ Vận hành Căn hộ tại Vinhomes Ocean Park 1  

---

## 1. PHẠM VI TRÁCH NHIỆM CHÍNH (ASSIGNED SCOPE)
Trong bài Lab Day 26 (AI Adoption & Change Management), tôi phụ trách toàn bộ mảng đánh giá tổ chức, quản trị rủi ro và lộ trình triển khai:
1. **Chẩn đoán mức độ sẵn sàng tổ chức theo Gartner-Lite 3 trục (§4.2):** Xác định các khoảng trống về Hướng đi (Direction), Dữ liệu & Quản trị (Readiness), và Khả năng duy trì học hỏi từ sai sót (Absorption).
2. **Thu thập & Phân tích bằng chứng thực tế (§4.2):** Khai thác log dữ liệu từ hệ thống bot, thực hiện phỏng vấn nhanh nhân viên thực địa và đối chiếu các bài học thất bại/thành công từ case study quốc tế (DWP/GDS, Morgan Stanley, Klarna).
3. **Thiết kế Lộ trình 30-60-90 ngày theo cơ chế Gate (§4.4):** Chuyển đổi tư duy lộ trình từ "danh sách việc cần làm" sang "các cổng quyết định chất lượng dựa trên bằng chứng", gán rõ Owner chịu trách nhiệm từng mốc.
4. **Đề xuất chính sách Quỹ bảo hiểm rủi ro vận hành (Risk Waiver Policy - §4.3):** Biện pháp then chốt tháo gỡ rào cản tâm lý sợ bị phạt của nhân viên tuyến đầu.
5. **Tham gia phản biện chéo (Chặng 3):** Phản biện trục Lộ trình và Cơ chế kiểm soát cho nhóm bạn.

---

## 2. CHI TIẾT KẾT QUẢ THỰC HIỆN CÁC BƯỚC

### 📌 Bước 2: Chẩn đoán tổ chức bằng Gartner-Lite & Bằng chứng thực tế (§4.2)

#### A. Đánh giá chi tiết 3 trục Gartner-Lite:
| Trục đánh giá | Kết quả | Nhận định thực tế tại VinStay AI |
| :--- | :---: | :--- |
| **1. Direction (Hướng đi chiến lược)** | **ĐẠT** | Ban Giám đốc và đội ngũ vận hành thống nhất rõ mục tiêu: Giảm tải 80% cuộc gọi hỏi quy chế cho Quản lý ca trực, rút ngắn thời gian tiếp đón khách tại sảnh dưới 8 phút. |
| **2. Readiness (Độ sẵn sàng về Dữ liệu & Governance)** | **THIẾU** | **Điểm nghẽn lớn nhất:**<br>- *Dữ liệu:* Kho quy chế của BQL Vinhomes Ocean Park bị lưu rời rạc trong 4 file PDF scan cũ, chưa có ai chịu trách nhiệm chuẩn hóa vector và cập nhật các thông báo mới của BQL sảnh.<br>- *Governance:* Chưa có quy chế phân định trách nhiệm pháp lý khi AI cung cấp thông tin sai lệch dẫn đến bị BQL lập biên bản phạt. |
| **3. Absorption (Khả năng hấp thụ & Vận hành)** | **THIẾU** | Đội ngũ Field Host chưa có kênh phản hồi lỗi (Flagging channel); khi AI trả lời sai, nhân viên chỉ biết bức xúc bỏ dùng chứ hệ thống không thu thập được mẫu lỗi để tái huấn luyện RAG. |

#### B. Bằng chứng thực nghiệm (Empirical Evidence) thu thập được:
* **Bằng chứng 1 — Audit Log tương tác hệ thống:** Tôi đã rà soát log của Telegram Bot trong tuần thứ 3 thử nghiệm: Có 42 lượt tra cứu phát sinh nhưng chỉ có 5 lượt nhận được đánh giá tích cực. Đáng chú ý, có 6 truy vấn liên quan đến việc "chuyển đồ cồng kềnh qua sảnh", AI đều trả lời "được phép tự do" dựa trên tài liệu chung của năm 2024, trong khi quy chế mới của phân khu Sapphire từ tháng 08/2026 đã yêu cầu đặt cọc 2.000.000 VNĐ trước 24h. Hậu quả là 1 Field Host bị BQL sảnh S1.02 lập biên bản phạt.
* **Bằng chứng 2 — Phỏng vấn nhanh Field Host:** Khi tôi phỏng vấn 3 bạn Host thường trực tại sảnh Sapphire 1, cả 3 đều chia sẻ: *"Bọn em thà gọi thẳng anh Quản lý ca trực mất 10 phút chờ còn hơn tin bot. Nếu tin bot mà bảo vệ phạt tiền triệu thì bọn em lấy đâu ra tiền bù!"*. Điều này khẳng định vấn đề không nằm ở kỹ năng dùng app mà nằm ở niềm tin và rủi ro tài chính.
* **Bằng chứng 3 — Bài học từ Case Study quốc tế (Morgan Stanley & DWP/GDS):** 
  - *Morgan Stanley:* AI chỉ được triển khai thành công khi 100% dữ liệu nghiên cứu được kiểm chứng bởi đội ngũ chuyên gia nội bộ và có nguồn trích dẫn tuyệt đối chính xác trước khi đưa ra cho chuyên viên tư vấn tài chính.
  - *DWP / GDS (Vương quốc Anh):* Việc đo lường hiệu quả AI dựa trên log tác vụ thực tế trong quy trình luôn phản ánh đúng giá trị hơn là số liệu tự khai hay số lượt đăng nhập bề nổi.

---

### 📌 Bước 4: Thiết kế Lộ trình 30-60-90 ngày theo cơ chế Gate (§4.4)
Tôi thiết kế lộ trình theo nguyên tắc: **Gate chỉ được thông qua khi chất lượng, hành vi và giá trị đạt mục tiêu đã xác nhận — không phải khi hết số ngày trên lịch.**

```text
[LỘ TRÌNH 30 - 60 - 90 NGÀY THEO CƠ CHẾ CỔNG KIỂM SOÁT BẰNG CHỨNG]

Giai đoạn 1: 0 - 30 Ngày                   Giai đoạn 2: 31 - 60 Ngày                   Giai đoạn 3: 61 - 90 Ngày
CHỨNG MINH VẤN ĐỀ & NIỀM TIN               CHỨNG MINH CHẤT LƯỢNG & NĂNG SUẤT           ĐÁNH GIÁ GATE 3 & MỞ RỘNG
┌─────────────────────────────────┐        ┌─────────────────────────────────┐         ┌─────────────────────────────────┐
│ • Pilot hẹp tại Sapphire 1      │        │ • Bật kiểm tra QA 50 mẫu/tuần   │         │ • Đánh giá 5 tầng Dashboard v2  │
│ • Chuẩn hóa dữ liệu Vector BQL  │───────>│ • Theo dõi tỷ lệ First-Contact  │────────>│ • So sánh chi phí phạt BQL = 0đ │
│ • Ban hành Quỹ bảo hiểm rủi ro  │        │ • Kích hoạt Circuit-Breaker     │         │ • Quyết định nhân rộng Zenpark  │
│ • Bật trích nguồn & ngày hiệu lực│       │ • Đo thời gian xử lý ≤8 phút    │         │   hoặc Sửa / Dừng               │
└─────────────────────────────────┘        └─────────────────────────────────┘         └─────────────────────────────────┘
           │                                          │                                           │
           ▼                                          ▼                                           ▼
[GATE 1 - Tiêu chí thông qua]              [GATE 2 - Tiêu chí thông qua]               [GATE 3 - Tiêu chí thông qua]
- 100% tài liệu có Data Owner              - First-Contact Resolution ≥80%             - CSAT đón khách ≥4.8/5.0
- Tỷ lệ trích nguồn đạt ≥98%               - Thời gian xử lý ≤8 phút                   - Tiền phạt BQL = 0 VNĐ
- 100% Host ký nhận Risk Waiver            - Không có ca phạt BQL do AI                - Tỷ lệ tuân thủ quy trình ≥90%
Owner phụ trách: Lê Thanh Tùng             Owner phụ trách: Nguyễn Khánh Duy           Owner phụ trách: Cao Đức Hiệp
```

---

### 📌 Đề xuất then chốt: Chính sách Quỹ bảo hiểm rủi ro vận hành (Risk Waiver Policy)
Nhận thấy đây là "nút thắt cổ chai" khiến toàn bộ dự án bị tê liệt, tôi đã trực tiếp soạn thảo và bảo vệ đề xuất chính sách bồi hoàn rủi ro:
* **Nội dung cam kết:** Nếu Field Host thực hiện đúng quy trình chuẩn (Hỏi AI $\rightarrow$ Đọc nguồn kiểm chứng $\rightarrow$ Làm theo hướng dẫn) mà vẫn phát sinh sự cố bị BQL tòa nhà lập biên bản xử phạt tài chính, Công ty cam kết **chi trả 100% chi phí xử phạt** thông qua Quỹ rủi ro vận hành nội bộ.
* **Hiệu lực tác động:** Giải tỏa 100% nỗi sợ cá nhân của Field Host (điểm nghẽn *Desire* theo ADKAR), chuyển đổi tâm lý từ "sợ dùng AI bị phạt" sang "an tâm dùng AI vì có tổ chức bảo vệ".

---

### 📌 Đóng góp trong Chặng 3: Phản biện chéo cho Nhóm 03 (Dự án EdTech AI)
* **Nội dung tôi phản biện:** Nhóm 03 lập lộ trình 30-60-90 ngày theo hình thức liệt kê danh sách đầu việc cứng nhắc: "Ngày 1-30 xây dựng mô hình, ngày 31-60 đưa vào 5 trường học, ngày 61-90 nhân rộng toàn quốc". Lộ trình này không có tiêu chí vượt Gate, không có điều kiện dừng lại nếu học sinh phản ánh sai sót.
* **Đề xuất cụ thể của tôi:** Yêu cầu Nhóm 03 phải gắn tiêu chí Gate kiểm soát chất lượng: Chỉ cho phép chuyển sang giai đoạn nhân rộng nếu tỷ lệ bài giải sai sót được kiểm định bởi giáo viên dưới 2%; nếu chưa đạt tiêu chí này, bắt buộc giữ nguyên ở giai đoạn thử nghiệm để sửa chữa thuật toán.

---

## 3. TỰ ĐÁNH GIÁ VÀ CAM KẾT ĐÓNG GÓP
* **Mức độ hoàn thành:** 100% khối lượng công việc được phân công.
* **Tính đồng bộ:** Lộ trình 30-60-90 ngày và chính sách Quỹ bảo hiểm rủi ro là điểm tựa vận hành vững chắc cho quy trình TO-BE của Nguyễn Khánh Duy và các chỉ số đo lường trong Dashboard của Cao Đức Hiệp.
* **Chữ ký xác nhận:** *Lê Thanh Tùng*
