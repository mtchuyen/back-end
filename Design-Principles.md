## Design Principles vs Design Patterns

***Design Principles***:

Nguyên tắc thiết kế (Design Principles) là một tập những quy tắc, quy chuẩn để giúp bạn có thể xây dựng và thiết kế hệ thống một cách tốt nhất, dễ dàng phát triển, bảo trì và vận hành tốt.
+ Nói chung, những nguyên tắc này không giới hạn vô một ngôn ngữ, nền tảng nào, và không đề cập cụ thể implementation như thế nào trên một ngôn ngữ. 

***Design Pattern***

Dịch ra Tiếng Việt là mẫu thiết kế. Mẫu thiết kế nó cụ thể hơn, chi tiết hơn, nói tới việc làm sao để implement. Trong mẫu thiết kế đó, class xây dựng như thế nào, cụ thể thằng này kế thừa thằng kia ra sao. Mẫu thiết kế được đúng kết, rút ra từ quá trình implement lâu dài. Trong quá trình implement lâu dài, chúng ta gặp những bài toán khác nhau. Ứng với mỗi bài toán đó, mình sẽ có một cách implement làm sao để hiệu quả nhất, khi đó cha ông, anh chị đi trước đúc kết được một mẫu thiết kế.

Khi học mẫu thiết kế, chúng ta nên đi từ bài toán. Cụ thể, khi mình gặp tình huống blabla-usecase này. Mình nghĩ: à, mẫu thiết blublu-pattern chuyên để giải quyết bài toán này. Sau đó mình xem cụ thể đối với mẫu thiết kế đó, trong ngôn ngữ này thì sẽ code ra sao.
+ Ví dụ: mẫu thiết kế hướng đối tượng. Gặp bài toán khi một hệ thống chỉ cần tạo ra một đối tượng từ class đó thôi –> nghĩ tới mẫu/pattern Singleton liền, việc implement thì tùy ngôn ngữ sẽ khác nhau. Gặp bài toán mà giải quyết nó cần trải qua nhiều step, mỗi step đó tùy loại đội tượng sẽ chạy theo kiểu khác nhau –> Mẫu/pattern template.



| Design Principles | Design Patterns |
| --- | --- |
| Các nguyên tắc, nguyên lý trong thiết kế | Là các khuôn mẫu thiết kế |
| đưa ra cho bạn những gợi ý để giải quyết một vấn đề | Đưa ra cho bạn chi tiết cách để giải quyết vấn đề đó | 
| Không đề cập cụ thể implementation như thế nào trên một ngôn ngữ | Nói tới việc làm sao để implement | 


#### Một số liệt kê Design theo từng loại:
Note: Bảng này không phải là sự ánh xạ theo hàng (row) với các tên tương ứng, tạo bảng này để dễ nhìn hơn khi so sánh giữa `Principles` và `Patterns`

| Design Principles | Design Patterns |
| --- | --- |
| Package Cohesion Principles: REP, CRP, CCP |  Creational Patterns: Factory, Abstract Factory, Singleton, ...
| Package Coupling principle: ADP, SDP, SAP | Structural Patterns: Adapter, Bridge, Filter,...
| DRY, KISS, YAGNI, Boy Scout Rule | Behavioral Patterns: Chain of Responsibilities, Interpreter, Iterator, ...
| Class Design principles: SOLID | ...
| ... | ...

