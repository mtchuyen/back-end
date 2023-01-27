## Memory

1. physical memory
2. virtual memory 

## Cache hard:
Cache L1, L2,...

## Cache soft
### 1. TLB Cache: translation lookaside buffer 
1.1. iTLB cache.
1.2. dTLB Cache.

### 2. Multi-level cache:
1. L1:
L1 cache can be had:
- L1.instruction cache
- L1.data cache
- L1.iTLB cache
- L1.dTLB cache
2. L2:
L2 cache can be had:
- L2.iTLB cache
- L2.dTLB cache
- L2.unified (all kind cache at L2: iTLB, dTLB, and other...)


## Cache app
https://levelup.gitconnected.com/the-art-of-caching-for-backend-applications-38350f95def6

### Key features of a cache
Các thông số thường dùng để đặc tả cache của một app:

- type of cache: you can choose to store data in a `local` or `distributed` cache
- data to store: you can choose between storing data as is or compiling it to save time for future usages in your app
- filling strategy: you can implement a lazy or eager cache depending on your use case the strategy chosen could improve or ruin your performance
- size of cache: you need to know the amount of data you are going to store because it will define the number of cache entries you can store
- keys: you should pay attention to the key or keys you use to store your data so ***it’s searchable*** the way you need it. (Điều này thường ít được chú ý trong các cache app được thiết kế đơn giản, nhưng với các loại cache phức tạp thì ảnh hưởng rất lớn)
- TTL (time to live): is another essential parameter that defines how long data will be stored in the cache
- eviction policy: this policy decides when a particular key will be removed from the cache to store new data

Tham khảo thêm ở [đây](https://github.com/mtchuyen/Golang-Tips/blob/master/Golang-connect-to-another/Cache.md)

### Local or distributed cache

***A distributed cache*** works across a network and multiple machines access it, it’s useful to scale applications and to share data between different servers supporting huge applications. 
- The typical way to implement these caches is to install an instance or a cluster of a specific cache engine server. 
- These systems are meant to scale horizontally so it’s very common for them to have some features `like` clustering and sharding out of the box.

***Which one is better (Local or distributed)?*** 
> It depends on your use case… Because we have thousands of use cases for a cache, you have thousands of options to choose from. 

### filling strategy: Choosing the best

When we talk about the filling strategy, we are talking about ***the way data will be inserted into the cache***. 
Here we have two ways to do it: ***eager or lazy***.

***what about a hybrid approach?*** Great question! For sure you can combine both strategies and, in most cases, it’s the best option if you want to get the most performance without missing any data.

### Khóa (keys)
Khía cạnh quan trọng nhất là các `khóa (keys)` phải *có thể* ***tìm kiếm được*** cho ứng dụng của bạn.
- Xin chú ý là: ***Khóa-keys phải có khả năng tìm kiếm được*** (nếu không cache-items đó vô tác dụng)

Hãy ghi nhớ điều này, bạn nên điều chỉnh các khóa của mình theo cách ứng dụng của bạn sẽ truy xuất dữ liệu.
- VD: Nếu app của bạn muốn lấy data theo trường `product_id` thì `khóa-keys` nên được thiết kế dựa vào trường này. Lúc này, `key` trong cặp `key-value` là `product-info:123`

Nếu ứng dụng của bạn cần nhiều tham số, bạn có thể nối tất cả các tham số cần thiết để tạo khóa của mình.
- Ở ví dụ trên, ta cần phân biệt thêm data tách bởi ngôn ngữ (Eng, Spanish,...) thì ta có thể tạo các keys là `product-info:123:en` và `product-info:123:spa`

A common `pitfall` when choosing keys is storing ***huge amounts*** of data inside the same key.
- To avoid this problem you can split your cache into several keys with specific information depending on how your application will use it.

### What is the best technology for my cache?
