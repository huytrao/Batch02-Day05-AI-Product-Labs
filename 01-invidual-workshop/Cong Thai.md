# Báo cáo Workshop Cá Nhân  
## Mổ sản phẩm AI thật: app → flow → path yếu → sửa

**Sản phẩm phân tích:** Moni trong ứng dụng MoMo  
**Chủ đề:** Phân tích flow AI và đề xuất sửa path yếu nhất  
**Vấn đề chính quan sát được:** Moni đang trả lời thì dừng giữa chừng

---

## 1. Mục tiêu workshop

Mục tiêu của workshop là phân tích một sản phẩm AI đang được tích hợp trong app thật. Thay vì chỉ nhận xét sản phẩm theo cảm tính, báo cáo tập trung vào việc đi theo một luồng sử dụng cụ thể, xác định điểm yếu trong trải nghiệm người dùng và đề xuất một hướng sửa có tính sản phẩm.

Sản phẩm được chọn là **Moni** trong ứng dụng **MoMo**. Đây là một trợ lý AI được tích hợp trong app tài chính, có vai trò hỗ trợ người dùng hỏi đáp, tra cứu và nhận gợi ý liên quan đến tài chính cá nhân hoặc các tính năng trong ứng dụng.

---

## 2. Lý do chọn sản phẩm

MoMo là một ứng dụng tài chính phổ biến tại Việt Nam, có nhiều tình huống sử dụng hằng ngày như chuyển tiền, thanh toán hóa đơn, nạp điện thoại, quản lý giao dịch và theo dõi chi tiêu.

Việc tích hợp AI vào MoMo có tiềm năng tạo ra giá trị lớn vì người dùng có thể hỏi trực tiếp thay vì tự tìm trong nhiều màn hình khác nhau. Nếu hoạt động tốt, Moni có thể giúp người dùng:

- Tiết kiệm thời gian tra cứu thông tin.
- Hiểu rõ hơn về chi tiêu cá nhân.
- Nhận hướng dẫn khi gặp vấn đề trong app.
- Tăng cảm giác app thông minh và cá nhân hóa hơn.

Tuy nhiên, vì MoMo là app tài chính, người dùng cũng kỳ vọng câu trả lời phải rõ ràng, đầy đủ và đáng tin cậy. Do đó, bất kỳ lỗi nào trong quá trình trả lời của AI đều có thể ảnh hưởng trực tiếp đến niềm tin của người dùng.

---

## 3. Quá trình dùng thử

Trong quá trình dùng thử, tôi mở ứng dụng MoMo và sử dụng Moni để đặt một số câu hỏi liên quan đến tài chính cá nhân hoặc hỗ trợ trong app.

Một số dạng câu hỏi có thể dùng để kiểm tra gồm:

1. “Tháng này tôi tiêu nhiều nhất vào khoản nào?”
2. “Tôi có đang chi tiêu nhiều hơn tháng trước không?”
3. “Làm sao để giảm chi tiêu trong tháng tới?”
4. “Tôi muốn kiểm tra giao dịch gần đây thì làm thế nào?”

Kỳ vọng ban đầu là Moni sẽ hiểu câu hỏi, xử lý yêu cầu và trả lời đầy đủ. Tuy nhiên, trong quá trình quan sát, vấn đề nổi bật là **Moni đang trả lời thì dừng lại giữa chừng**.

Câu trả lời không được hoàn thành, không có thông báo lỗi rõ ràng và cũng không có nút để người dùng yêu cầu tiếp tục. Điều này khiến người dùng không biết hệ thống đã trả lời xong, bị lỗi mạng, lỗi AI hay không đủ dữ liệu để tiếp tục.

---

## 4. Flow hiện tại: As-is flow

Flow hiện tại có thể mô tả như sau:

```text
Người dùng mở app MoMo
        ↓
Người dùng vào Moni
        ↓
Người dùng nhập câu hỏi
        ↓
Moni bắt đầu sinh câu trả lời
        ↓
Câu trả lời bị dừng giữa chừng
        ↓
Người dùng không biết phải làm gì tiếp theo
```

Ở phần đầu của flow, trải nghiệm vẫn diễn ra bình thường. Người dùng có thể nhập câu hỏi và thấy Moni bắt đầu phản hồi. Điều này tạo kỳ vọng rằng hệ thống đang xử lý thành công.

Tuy nhiên, khi câu trả lời bị dừng đột ngột, flow bị gãy. Người dùng không nhận được kết luận cuối cùng và cũng không được hướng dẫn cách xử lý tiếp theo.

Các vấn đề trong flow hiện tại gồm:

- Không có trạng thái báo lỗi rõ ràng.
- Không biết câu trả lời đã hoàn thành hay chưa.
- Không có nút “Tiếp tục trả lời”.
- Không có nút “Tạo lại câu trả lời”.
- Không có gợi ý để người dùng hỏi lại.
- Không giải thích nguyên nhân bị dừng.

Vì vậy, người dùng bị rơi vào trạng thái bị kẹt trong flow.

---

## 5. Path yếu nhất

Path yếu nhất của Moni là:

> **Moni bắt đầu trả lời nhưng dừng giữa chừng, không có thông báo lỗi, không có nút tiếp tục và không có cách sửa rõ ràng cho người dùng.**

Đây là path yếu nhất vì nó phá vỡ kỳ vọng cơ bản nhất khi dùng chatbot AI: người dùng hỏi và mong nhận được một câu trả lời hoàn chỉnh.

Ví dụ:

```text
User: Tháng này tôi tiêu nhiều nhất vào khoản nào?

Moni: Dựa trên các giao dịch gần đây của bạn, khoản chi tiêu lớn nhất có thể là...
```

Sau đó câu trả lời dừng lại.

Trong tình huống này, người dùng không biết:

- Moni đã trả lời xong hay chưa.
- Moni có đang gặp lỗi kỹ thuật không.
- Câu hỏi có quá khó không.
- App có thiếu quyền truy cập dữ liệu không.
- Có nên gửi lại câu hỏi không.
- Phần câu trả lời trước đó có đáng tin không.

Vấn đề không chỉ là câu trả lời thiếu nội dung. Vấn đề lớn hơn là **người dùng không có đường đi tiếp trong sản phẩm**.

---

## 6. Tác động đến trải nghiệm người dùng

Lỗi “đang trả lời thì dừng” có ảnh hưởng lớn đến trải nghiệm người dùng, đặc biệt trong bối cảnh app tài chính.

Thứ nhất, nó làm giảm niềm tin vào AI. Người dùng có thể cảm thấy Moni chưa ổn định, chưa đáng tin hoặc chưa đủ thông minh để hỗ trợ các tác vụ quan trọng.

Thứ hai, nó làm người dùng mất thời gian. Thay vì nhận được câu trả lời ngay, người dùng phải hỏi lại, thoát ra vào lại hoặc tự tìm thông tin trong app.

Thứ ba, nó tạo cảm giác không kiểm soát. Người dùng không biết lỗi nằm ở đâu và không biết hành động tiếp theo nên là gì.

Thứ tư, trong lĩnh vực tài chính cá nhân, câu trả lời thiếu hoàn chỉnh có thể gây khó chịu hơn so với các chatbot thông thường. Khi hỏi về chi tiêu, giao dịch hoặc tiền bạc, người dùng cần thông tin rõ ràng, đầy đủ và có thể kiểm chứng.

Do đó, đây không nên được xem là một bug nhỏ. Đây là một điểm gãy trong trải nghiệm sản phẩm AI.

---

## 7. Đề xuất flow mới: To-be flow

Flow mới cần xử lý tốt hơn khi Moni bị dừng giữa chừng.

```text
Người dùng nhập câu hỏi
        ↓
Moni bắt đầu trả lời
        ↓
Hệ thống kiểm tra trạng thái sinh câu trả lời
        ↓
Nếu trả lời thành công:
        → Hiển thị câu trả lời đầy đủ
        → Gợi ý hành động tiếp theo

Nếu câu trả lời bị gián đoạn:
        → Hiển thị thông báo lỗi rõ ràng
        → Cho phép tiếp tục trả lời
        → Cho phép tạo lại câu trả lời
        → Lưu phần nội dung đã sinh
```

Khi câu trả lời bị dừng, app nên hiển thị thông báo như:

> “Câu trả lời của Moni chưa hoàn tất. Bạn muốn tiếp tục không?”

Kèm theo các nút hành động:

- **Tiếp tục trả lời**
- **Tạo lại câu trả lời**
- **Rút gọn câu trả lời**
- **Hỏi lại theo cách khác**
- **Báo lỗi**

Với các câu hỏi liên quan đến dữ liệu tài chính, Moni cũng nên hiển thị phạm vi dữ liệu, ví dụ:

> “Dựa trên giao dịch trong 30 ngày gần nhất.”

Điều này giúp người dùng hiểu câu trả lời được tạo dựa trên nguồn dữ liệu nào và có thể đánh giá độ tin cậy của phản hồi.

---

## 8. Product decision

Product decision được đề xuất là:

> **Khi Moni đang trả lời nhưng bị dừng giữa chừng, hệ thống không được để người dùng bị kẹt. Cần có trạng thái lỗi rõ ràng, nút tiếp tục trả lời, nút tạo lại câu trả lời và cơ chế lưu lại phần nội dung đã sinh ra.**

Lý do chọn hướng này là vì vấn đề chính không chỉ nằm ở năng lực trả lời của AI, mà nằm ở cách sản phẩm xử lý khi AI gặp lỗi hoặc bị gián đoạn.

Một AI có thể gặp lỗi, nhưng sản phẩm cần thiết kế để người dùng vẫn biết chuyện gì đang xảy ra và có thể tiếp tục thao tác. Khi có thông báo rõ ràng và các nút hành động cụ thể, người dùng sẽ cảm thấy hệ thống minh bạch và đáng tin hơn.

---

## 9. Gợi ý cải tiến giao diện

Một số cải tiến cụ thể có thể áp dụng:

### 9.1. Thêm trạng thái phản hồi

Moni nên có trạng thái rõ ràng khi đang xử lý:

```text
Moni đang phân tích câu hỏi...
Moni đang tạo câu trả lời...
Câu trả lời chưa hoàn tất.
```

Điều này giúp người dùng hiểu hệ thống đang ở bước nào.

### 9.2. Thêm nút “Tiếp tục trả lời”

Nếu AI bị dừng, nút **Tiếp tục trả lời** nên xuất hiện ngay dưới câu trả lời dang dở. Đây là hành động quan trọng nhất vì nó giúp người dùng không cần nhập lại từ đầu.

### 9.3. Thêm nút “Tạo lại câu trả lời”

Trong trường hợp câu trả lời bị lỗi hoặc không hợp lý, người dùng có thể chọn tạo lại câu trả lời mới.

### 9.4. Lưu lại phần câu trả lời đã sinh

Nếu Moni đã trả lời được một phần, phần đó không nên bị mất. Hệ thống nên lưu lại nội dung cũ và tiếp tục từ điểm bị dừng.

### 9.5. Cho phép người dùng báo lỗi

Một nút **Báo lỗi** có thể giúp đội sản phẩm thu thập các trường hợp Moni bị dừng để cải thiện hệ thống.

---

## 10. Kết luận

Qua quá trình phân tích Moni trong MoMo, tôi nhận thấy vấn đề lớn nhất không nằm ở việc Moni có AI hay không, mà nằm ở trải nghiệm khi AI trả lời không hoàn chỉnh.

Path yếu nhất là tình huống Moni đang trả lời thì dừng giữa chừng. Đây là một điểm gãy nghiêm trọng vì người dùng không nhận được câu trả lời đầy đủ và cũng không biết phải làm gì tiếp theo.

Đề xuất quan trọng nhất là thiết kế lại flow xử lý lỗi. Khi Moni bị dừng, hệ thống cần thông báo rõ ràng, cho phép tiếp tục trả lời, tạo lại câu trả lời và lưu lại nội dung đã sinh. Đây là cải tiến nhỏ về giao diện nhưng có tác động lớn đến trải nghiệm người dùng và độ tin cậy của sản phẩm AI.

Một sản phẩm AI tốt không chỉ cần trả lời đúng trong happy path, mà còn cần xử lý tốt khi gặp lỗi. Với Moni, việc sửa path “đang trả lời thì dừng” sẽ giúp sản phẩm trở nên rõ ràng, đáng tin và hữu ích hơn đối với người dùng.
