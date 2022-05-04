# Introduce
Phần này sẽ tập trung vào ***Object Oriented Design*** 

(Ref.4)Ngày xửa ngày xưa, người ta nói rằng:

> Proper Object Oriented Design makes a developer's life easy, whereas bad design makes it a disaster

Vâng ***good*** design sẽ làm cho cuộc sống của lập trình viên dễ dàng hơn. Vậy làm sao để có một good design ? Chúng ta có những nguyên lý (principles).
> Principles: Là một tập hợp các hướng dẫn giúp chúng ta tránh các thiết kế xấu.


## Tại sao cần tuân thủ 1 nguyên lý trong lập trình:

Tuân thủ nguyên lý (principles) giống như cơ thể có 1 bộ khung xương (nguyên lý tốt thì khung xương đẹp vững chắc,...) vậy nên cần chọn 1 nguyên lý phù hợp với dự án.
> (Ref.4)Việc viết code theo các nguyên lý giúp cho code trở nên trong sáng, dễ đọc, dễ test và quan trọng nhất là dễ maintain hơn rất nhiều. Và chúng ta đều biết, trong vòng đời của một phần mềm, thời gian code chỉ chiếm 20-40% còn lại là thời gian dành cho maintain: thêm/bớt chức năng, fix bug...

Chung quy lại vẫn là để KHÔNG bị ***Bad code***.

(Ref.1) Theo Robert C. Martin, một trong những đồng tác giả của Agile Manifesto, có ba đặc điểm của thiết kế xấu cần tránh:
- ***Rigidity (cứng nhắc)***: Đề cập đến là việc khó khăn khi sửa đổi ứng dụng vì mọi thay đổi liên quan đến quá nhiều phần của hệ thống.
- ***Fragility (phá vỡ)***: Đây là sự phát sinh lỗi trong ứng dụng do những thay đổi trong các phần khác.
- ***Immobility (bất động)***: Đây là việc hệ thống không thể sử dụng thêm một thành phần trong phần mềm khác vì nó quá phụ thuộc vào ứng dụng hiện tại.

(MTC)Nhưng trong (Ref.2) phần ***Bad code*** liệt kê là:
- Rigid. Is the code rigid? Does it have a straight jacket of overbearing types and parameters, that making modification difficult?
- Fragile. Is the code fragile? Does the slightest change ripple through the code base causing untold havoc?
- Immobile. Is the code hard to refactor? Is it one keystroke away from an import loop?
- ***Complex***. Is there code for the sake of having code, are things over-engineered?
- ***Verbose***. Is it just exhausting to use the code? When you look at it, can you even tell what this code is trying to do?

## Các nhóm Design Principles
Trong cuốn "Agile Software Development: Principles, Patterns, and Practices", Uncle Bob đã tổng hợp lại 11 nguyên lý và chia chúng làm 3 nhóm:

***Class Design principles – bao gồm 5 nguyên lý***

- (SRP) Single Responsibility Principle
- (OCP) Open Closed Principle
- (LSP) Liskov Substitution Principle
- (DIP) Dependency Inversion Principle
- (ISP) Interface Segregation Principle

> viết tắt là S.O.L.I.D (hoặc SOLID)

***Package Cohesion Principles - bao gổm 3 nguyên lý***

- (REP) Reuse-Release Equivalence Principle
- (CRP) Common Reuse Principle
- (CCP) Common Closure Principle


***Package Coupling principle - bao gồm 3 nguyên lý***
- (ADP) Acyclic Dependencies Principle
- (SDP) Stable Dependencies Principle
- (SAP) Stable Abstractions Principle


***Ngoài ra còn có các nguyên lý khác như***
- (DRY) Don't Repeat Yourself
- (KISS) Keep It Simple Stupid ...

## Nguyên tắc KISS 
Source: (Ref.8)

***KISS = Keep It Simple Stupid***

KISS có nhiều biến thể khác nhau như "Keep It Short and Simple", "Keep It Simple and Straightforward" và "Keep It Small and Simple".

Tựu chung lại, hàm ý của nó vẫn hướng về một sự đơn giản và rõ ràng trong mọi vấn đề. Và như vậy, sự đơn giản là mục đích trọng tâm trong thiết kế, còn những cái phức tạp không cần thiết thì nên tránh.

Trong lập trình, KISS nghĩa là hãy làm cho mọi thứ (mã lệnh của bạn) trở nên đơn giản và dễ nhìn hơn. Hãy chia nhỏ vấn đề ra những bài toán nhỏ đơn giản hơn, viết mã để xử lý nó, biến nó thành các lớp và các hàm riêng biệt, đừng để một lớp hay một phương thức có hàng trăm dòng lệnh, hãy để nó trở về con số chục thôi.

Đừng viết những lớp hay phương thức theo kiểu spaghetti hay all-in-one (tất cả trong một) như dao thụy sĩ, hãy để mọi thứ thật đơn giản để bạn luôn có thể hiểu được, và kết hợp chúng với nhau để giải quyết được các bài toán lớn.

## Nguyên tắc YAGNI:
Source: (Ref.8)

***YAGNI = You Aren’t Gonna Need It***

Là những lập trình viên, đôi khi chúng ta suy nghĩ quá nhiều về tương lai của dự án nên chúng ta code thêm thật nhiều tính năng “phòng khi chúng ta cần đến nó” hay “Cuối cùng chúng ta sẽ dùng đến nó”. Ý nghĩ này sai hoàn toàn. Bạn đã không cần đến nó thì bạn sẽ không cần đến nó trong hầu hết tất cả các trường hợp! “You Aren’t Gonna Need It!”.

Nếu bạn nghĩ một chức năng sẽ hữu dụng trong tương lai, hãy cứ bình tĩnh và xem lại những công việc đang chờ bạn giải quyết ngay. Bạn không thể lãng phí thời gian của mình để code những tính năng mà bạn sẽ phải sửa nó hay thay đổi nó bởi vì nó không phù hợp với nhu cầu của khách hàng, hay trong trường hợp xấu nhất là nó sẽ không được sử dụng đến.

> tốt nhất là hãy giải quyết thành công vấn đề hiển hiện trước mắt đã, khách hàng không vẽ việc cho bạn thì bạn cũng đừng tự vẽ việc cho mình

## Nguyên tắc DRY:
Source: (Ref.8)

***DRY = Don’t Repeat Yourself***

Nguyên tắc DRY chỉ ra rằng nếu chúng ta đang muốn viết nhiều đoạn code giống nhau ở nhiều chỗ khác nhau, thay vì copy và paste đoạn code đó, chúng ta hãy đưa đoạn code đó vào một phương thức riêng sau đó gọi phương thức này từ những chỗ chúng ta cần gọi.

Quen quen đúng không, vì nó giống như tính chất kế thừa trong lập trình hướng đối tượng OOP mà chúng ta đã quá quen thuộc rồi 


## Design Principles có liên quan gì đến Design Patterns không ???
Câu trả lời là có, nhưng có chút khác biệt.
- ***Principles***: là các hướng dẫn, mang tính trừu tượng nhiều hơn.
- ***Patterns***: là những ví dụ cụ thể hóa, cung cấp các giải pháp tái sử dụng đến các vấn đề thực tế. Patterns tốt nên tuân thủ tốt Principles.

## Design Principles vs Design Patterns

***Design Principles***:

Nguyên tắc thiết kế (Design Principles) là một tập những quy tắc, quy chuẩn để giúp bạn có thể xây dựng và thiết kế hệ thống một cách tốt nhất, dễ dàng phát triển, bảo trì và vận hành tốt.
+ Nói chung, những nguyên tắc này không giới hạn vô một ngôn ngữ, nền tảng nào, và không đề cập cụ thể implementation như thế nào trên một ngôn ngữ. 

***Design Pattern***

Dịch ra Tiếng Việt là mẫu thiết kế. Mẫu thiết kế nó cụ thể hơn, chi tiết hơn, nói tới việc làm sao để implement. Trong mẫu thiết kế đó, class xây dựng như thế nào, cụ thể thằng này kế thừa thằng kia ra sao. Mẫu thiết kế được đúng kết, rút ra từ quá trình implement lâu dài. Trong quá trình implement lâu dài, chúng ta gặp những bài toán khác nhau. Ứng với mỗi bài toán đó, mình sẽ có một cách implement làm sao để hiệu quả nhất, khi đó cha ông, anh chị đi trước đúc kết được một mẫu thiết kế.
> "Each pattern describes a ***problem which occurs over and over again*** in our environment, and then describes the core of the solution to that problem, in such a way that you can use this solution a million times over, without ever doing it the same way twice" (Alexander et al. 1977).

- Each pattern focuses on a recurring *problem* and offers a ***particular solution*** for such a *problem*.
- A Pattern is not a complete solution, but rather ***a starting point for the solution***, you have to tweak it a little here and there to make it for your needs.

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

## Ref
- [Ref.1:Nguyên lý SOLID là gì...](https://viblo.asia/p/nguyen-ly-solid-la-gi-dependency-injection-la-gi-bWrZnX4b5xw)
- [Ref.2:SOLID Go Design](https://dave.cheney.net/2016/08/20/solid-go-design)
- [Ref.4:Sơ lược Object Oriented Design Principles](https://viblo.asia/p/so-luoc-object-oriented-design-principles-MdZGAQODGox)
- Ref.7: https://viblo.asia/p/tim-hieu-ve-mot-so-nguyen-tac-thiet-ke-trong-lap-trinh-GrLZD0bOZk0
- [Ref.8:Những nguyên tắc, định luật thông dụng khi lập trình](https://viblo.asia/p/nhung-nguyen-tac-dinh-luat-thong-dung-khi-lap-trinh-gGJ59g2DZX2)
- Ref.9: https://kickoff.tech/courses/oop-design-patterns-vietnamese/

