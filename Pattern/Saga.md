## 1.Saga Pattern

Saga Pattern là một mẫu thiết kế (design pattern) dùng để **quản lý** giao dịch (transaction) phân tán. 

Trong kiến trúc Microservices, nếu một quy trình nghiệp vụ cần đi qua nhiều service độc lập (mỗi service có database riêng), Saga giúp đảm bảo tính **nhất quán của dữ liệu**.

Thay vì rollback toàn bộ, hệ thống sẽ thực hiện các thao tác **bù đắp (compensation)** để đảo ngược bước trước đó nếu xảy ra lỗi.


#### Ví dụ Quy trình Đặt hàng

Hãy tưởng tượng hệ thống bán hàng online của bạn có 3 bước xử lý trên các service khác nhau:
- **Bước 1: Payment Service:** Trừ tiền trong tài khoản.
- **Bước 2: Inventory Service:** Trừ số lượng hàng trong kho.
- **Bước 3: Shipping Service:** Tạo đơn hàng vận chuyển.

**Nếu không dùng Saga:** Nếu `bước 3 (Shipping)` lỗi, khách hàng đã bị trừ tiền `(bước 1)` và hàng trong kho đã bị trừ `(bước 2)`, dẫn đến sai lệch dữ liệu và trải nghiệm tồi tệ.

**Nếu dùng Saga Pattern:** Nếu bước 3 lỗi, hệ thống sẽ `tự động gọi` các hàm "bù đắp" (Compensating Transactions) theo thứ tự ngược lại:
- Bước bù đắp 2: Hoàn lại hàng vào kho.
- Bước bù đắp 1: Hoàn lại tiền cho khách hàng.
*Kết quả:* Dữ liệu được đưa về trạng thái ban đầu một cách an toàn.


## 2.Các thuật ngữ kỹ thuật

**1. Transaction:** Chuỗi thao tác trên dữ liệu, đảm bảo ACID (Atomicity, Consistency, Isolation, Durability). Ví dụ: Chuyển tiền từ tài khoản A sang B trong ngân hàng; nếu trừ A thành công nhưng cộng B lỗi → rollback.

**2. Distributed Transaction:** Transaction diễn ra trên nhiều service hoặc cơ sở dữ liệu riêng biệt, cần compensation hoặc eventual consistency. Ví dụ: Đặt hàng online: Payment Service trừ tiền, Inventory Service trừ tồn kho, Notification Service gửi email.

**3. Saga Pattern:** Design pattern quản lý distributed transaction bằng cách thực hiện compensation khi bước tiếp theo thất bại. Ví dụ: Inventory Service báo hết hàng → Payment Service hoàn tiền.

**4. Compensation (Bù đắp):** Hoàn tác một bước đã commit nếu bước khác thất bại. Ví dụ: Payment Service đã trừ tiền nhưng Inventory Service lỗi → Payment Service hoàn tiền.

**5. Event (Sự kiện):** Thông điệp bất đồng bộ giữa các service, báo trạng thái transaction. Ví dụ: Payment Service gửi “PaymentSuccess”, Inventory Service lắng nghe và trừ tồn kho.

**6. Orchestrator:** Thành phần trung tâm trong Orchestration Saga, điều phối các bước và rollback khi cần. Ví dụ: Orchestrator gửi lệnh trừ tiền → trừ tồn kho → rollback nếu cần.

**7. Partial Failure (Lỗi một phần):** Một bước trong distributed transaction thất bại, các bước khác đã commit. Ví dụ: Payment Service trừ tiền thành công nhưng Inventory Service báo hết hàng.

**8. Consistency (Tính nhất quán):** Dữ liệu luôn thỏa mãn ràng buộc và quy tắc nghiệp vụ sau transaction. Ví dụ: Sau khi đặt hàng, tổng tiền khách trừ = tổng giá đơn, tồn kho giảm đúng số lượng.

**9. Eventual Consistency (Nhất quán cuối cùng):** Hệ thống sẽ trở nên nhất quán theo thời gian, không cần ngay lập tức. Ví dụ: Payment Service commit trước, Inventory Service commit sau, cuối cùng trạng thái tổng thể đúng.

**10. Idempotency (Tính lặp lại an toàn):** Thực hiện thao tác nhiều lần mà không gây sai lệch dữ liệu, tránh duplicate event. Ví dụ: Event “PaymentSuccess” gửi 2 lần → Payment Service chỉ trừ tiền 1 lần.

**11. Orchestration Saga:** Triển khai Saga Pattern với orchestrator trung tâm điều phối các bước. Ví dụ: Orchestrator ra lệnh Payment → Inventory → Notification; rollback nếu Inventory lỗi.

**12. Event-Driven Saga:** Triển khai Saga Pattern, mỗi service tự quản lý transaction, phát/lắng nghe event, không cần trung tâm. Ví dụ: Payment gửi “PaymentSuccess” → Inventory trừ tồn kho → Inventory gửi “InventoryFailed” → Payment hoàn tiền.

