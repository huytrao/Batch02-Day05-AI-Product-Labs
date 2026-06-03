## 1. Product Slices Exploration

Để giải quyết bài toán tìm kiếm đồ ăn tại Ocean Park 1, dưới đây là đề xuất 3 lát cắt (slices) với các định hướng tiếp cận khác nhau để team cân nhắc:

### Slice A — Quick Open+Cuisine Finder (Tìm quán đang mở cửa)
* **Target User:** Cư dân cần biết chính xác quán nào đang mở cửa trong vòng 30 phút tới để đến ăn hoặc mua mang về.
* **Core Task:** Xác định trạng thái hoạt động thực tế của quán ăn dựa trên dữ liệu hỗn hợp.
* **AI Decision:** Sử dụng AI để tổng hợp dữ liệu thời gian mở cửa từ Google Maps, các bài đăng gom đơn trên Facebook và báo cáo từ người dùng (user reports) nhằm suy diễn (infer) mức độ tin cậy "Open Now".
* **Output:** Top 3 địa điểm "Đang mở cửa" kèm điểm số tin cậy (confidence score) và một câu lý giải ngắn gọn.
* **Failure Mitigation:** Hiển thị các nguồn dữ liệu gốc + gợi ý số điện thoại hotline hoặc nút nhờ cộng đồng xác minh hộ.

### Slice B — Fast Delivery Suggestion (Gợi ý giao hàng nhanh) — **[CHOSEN]**
* **Target User:** Cư dân bận rộn tại Ocean Park 1 muốn đặt đồ ăn giao tận cửa và yêu cầu nhận hàng nhanh chóng trong vòng 30–45 phút.
* **Core Task:** Kết hợp các tín hiệu thời gian giao hàng (ETA) từ nhiều app và báo cáo thực tế để chọn ra quán tối ưu tốc độ.
* **AI Decision:** Sử dụng AI/Heuristics để kết hợp các tín hiệu ETA từ ShopeeFood/GrabFood với các báo cáo giao hàng gần nhất của cư dân trong khu vực nhằm dự đoán thời gian giao hàng thực tế (Expected ETA) và đề xuất 2 lựa chọn tốt nhất.
* **Output:** 2 nhà hàng được đề xuất kèm thời gian ETA dự đoán, mức độ tin cậy và một ghi chú ngắn (Ví dụ: *"Có sẵn tài xế, món chuẩn bị nhanh"*).
* **Failure Mitigation:** Hiển thị các phương án thay thế như tự đến lấy (pickup) và quay về luồng yêu cầu người dùng xác nhận lại.

### Slice C — Dietary Filtered Suggest (Bộ lọc chế độ ăn đặc biệt)
* **Target User:** Cư dân hoặc khách ghé thăm Ocean Park 1 có nhu cầu ăn chay (Vegetarian) hoặc ăn thuần hồi giáo (Halal).
* **Core Task:** Sàng lọc và xác thực các quán có thực đơn phù hợp dựa trên đánh giá của cộng đồng.
* **AI Decision:** Sử dụng AI để quét và phân tích nội dung từ các nguồn dữ liệu tổng hợp nhằm gắn tag thực đơn (menu tags) và kiểm chứng mức độ "chuẩn vị/uy tín" thông qua thảo luận cộng đồng.
* **Output:** Top 3 địa điểm ăn chay/Halal đã được xác thực kèm theo các đoạn trích bằng chứng (evidence) từ bài đánh giá.
* **Failure Mitigation:** Trích dẫn trực tiếp câu chữ của nguồn cấp dữ liệu và cho phép người dùng gửi phản hồi sửa đổi (correction) nếu AI gắn tag sai.

---

## 2. Selection Rationale (Lý do chọn Slice B)

Team mình quyết định chọn **Slice B — Fast Delivery Suggest** làm trọng tâm phát triển cho bản Prototype. Lý do cốt lõi bao gồm:
1. **Tính khả thi cao trong thời gian ngắn (6 tiếng):** Phạm vi tác vụ hẹp (narrow task), các tín hiệu đầu vào từ các nền tảng giao hàng (ShopeeFood/Grab) rất rõ ràng và dễ giả lập bằng dữ liệu mẫu (fake data) trong SQLite.
2. **Giá trị Demo cao:** Đánh trúng nỗi đau thực tế của cư dân (giao hàng trễ, app báo một đằng shipper đi một nẻo). Luồng trải nghiệm ngắn gọn, trực quan, rất phù hợp để chạy Demo 3 phút.

---

## 3. Auto / Aug Decision (Quyết định Tự động hóa vs. Trợ lực)

* **Quyết định:** **Conditional Automation với sự hỗ trợ đắc lực của Augmentation (Tự động hóa có điều kiện kèm trợ lực con người)**.
* **Vai trò của AI (AI suggests):** Dự đoán khả năng giao hàng, tính toán Expected ETA và đề xuất ra 2 phương án tối ưu nhất.
* **Vai trò của Con người (User decides):** Người dùng chủ động kiểm tra các nguồn chứng cứ (evidence), mức độ tin cậy được hiển thị và bấm xác nhận đơn hàng.
* **Lý do:** Quyết định đặt đồ ăn có mức độ rủi ro trung bình (giao trễ gây đói bụng, bực mình, lãng phí thời gian). Việc hiển thị minh bạch nguồn dữ liệu giúp người dùng làm chủ quyết định, tránh việc AI tự động đặt đơn khi dữ liệu có độ nhiễu cao.

---

## 4. Detailed Four Paths (Xây dựng 4 kịch bản vận hành)

Để chuẩn bị cho cấu trúc cơ sở dữ liệu và kịch bản demo, dưới đây là chi tiết 4 đường đi của dữ liệu đối với **Slice B**:

### 4.1. Happy Path (Luồng lý tưởng)
* **Bối cảnh:** Dữ liệu đầu vào đồng nhất, tín hiệu từ Grab/ShopeeFood ổn định, không có bài phàn nàn nào gần đây về việc thiếu tài xế tại phân khu.
* **Hành vi người dùng:** Người dùng mở ứng dụng, chọn tính năng "Giao nhanh".
* **Hệ thống xử lý:** Hệ thống truy vấn SQLite, AI phân tích thấy dữ liệu đồng nhất → Tính toán ETA dự kiến là 35 phút (Confidence: **HIGH**).
* **Kết quả:** Hệ thống hiển thị 2 quán (ví dụ: *Bánh Mì PewPew* và *Phở Thìn Ocean Park*). Người dùng thấy thông tin minh bạch, bấm vào link nguồn và chuyển hướng đặt hàng thành công.

### 4.2. Low Confidence Path (Luồng tin cậy thấp)
* **Bối cảnh:** Dữ liệu có sự xung đột. Ví dụ: App Grab báo ETA là 25 phút, nhưng trên nhóm cư dân Facebook cách đây 15 phút có 2 bài đăng phàn nàn: *"Khu vực OP1 đang mưa lớn, tìm shipper rất khó, đơn hàng bị treo"*.
* **Hành vi người dùng:** Người dùng bấm tìm kiếm "Giao nhanh" vào giờ cao điểm/lúc thời tiết xấu.
* **Hệ thống xử lý:** AI phát hiện tín hiệu mâu thuẫn giữa API giả lập và bài đăng thực tế của cộng đồng. Hệ thống không ẩn quán ăn đi nhưng hạ điểm tin cậy xuống.
* **Kết quả:** Giao diện hiển thị biểu tượng cảnh báo màu vàng (Badge: **Low Confidence**) kèm ghi chú: *"Hệ thống phát hiện có phản ánh chậm trễ do thời tiết từ Facebook. ETA dự kiến có thể kéo dài từ 45-60 phút"*. Người dùng tự cân nhắc rủi ro trước khi bấm đặt.

### 4.3. Failure Path (Luồng thất bại)
* **Bối cảnh:** AI dự đoán quán ăn A giao rất nhanh (ETA 30 phút, Confidence High) do dữ liệu lịch sử tốt. Tuy nhiên, thực tế quán A đột ngột đóng cửa sửa chữa hoặc hết nguyên liệu mà không cập nhật trên app hệ thống, dẫn đến việc đơn hàng thực tế bị hủy hoặc kéo dài >60 phút.
* **Hành vi người dùng:** Người dùng gặp phải tình trạng đơn hàng bị treo hoặc bị hủy sau khi đặt theo gợi ý.
* **Hệ thống xử lý:** Hệ thống ghi nhận log sai lệch dữ liệu (mismatch) giữa dự đoán và thực tế thông qua nút báo cáo của người dùng.
* **Kết quả:** Giao diện lập tức hiển thị thông báo xin lỗi công khai, kích hoạt phương án cứu vãn (fallback): Gợi ý hotline gọi trực tiếp cho chủ quán, hiển thị danh sách các quán thay thế ở ngay chân tòa nhà (có thể đi bộ ra lấy) và gửi log lỗi này về cho **Evidence Owner (Member B)** để cập nhật lại trọng số nguồn dữ liệu.

### 4.4. Correction Path (Luồng hiệu chỉnh)
* **Bối cảnh:** Một quán ăn trong danh sách vừa đổi định vị từ tòa S1 sang tòa S2 hoặc đổi hotline đặt hàng trực tiếp nhưng hệ thống chưa cập nhật.
* **Hành vi người dùng:** Người dùng phát hiện thông tin hiển thị bị sai lệch (ví dụ: quán đã đóng cửa hoặc đổi menu). Người dùng nhấn vào nút "Báo lỗi thông tin" trên giao diện.
* **Hệ thống xử lý:** Hệ thống hiển thị một form biểu mẫu tinh gọn để người dùng nhanh chóng tick chọn lỗi (Sai vị trí / Sai trạng thái mở cửa / Điện thoại không liên lạc được).
* **Kết quả:** Ngay sau khi submit, hệ thống cập nhật local cache để tạm thời hạ xếp hạng hoặc ẩn quán đó trong phiên tìm kiếm của các user khác tại phân khu đó. Đồng thời, một ticket dữ liệu sẽ được tự động gắn flag và gửi thẳng đến phân khu quản lý của **Evidence Owner** để kiểm chứng và cập nhật lại database gốc.
