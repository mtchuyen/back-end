# System Architecture

-  High Concurrency
-  Low Latency

## 3. Understanding Low Latency
***[Ref3]***

Latency is the time taken for a task to complete in time units. 
Latency, in turn determines the overall throughput which is the amount of tasks completed in a given period. Hence we look at the 4 main factors that influence latency:
- Software
- Database
- Infrastructure
- Network

### 3.1. Software
- Là trái tim của hệ thống: nơi mà các logic của nghiệp vụ được tiếp nhận và xử lý, mỗi khi có một request từ client gửi tới server.

Các tiêu chuẩn cần xem xét khi thiết kế Software:
- ***Distributed, Cluster or Monolithic Architecture***: các tiêu chí để xét là: Mức logic của nghiệp vụ, Latency của response (client-server, giữa các nghiệp vụ con...), cơ chế phân phối request (LoadBalance, RoundRobin,...) --> Infrastructure.
- ***Mức logic của nghiệp vụ***: Task có thể được chia nhỏ? Có thể parallel? multi-threading?...

```
Tasks fall into these 3 broad categories:
- Tasks that can be split logically and parallelized; or
- Tasks that cannot be split logically, and has to run as an independent, standalone; or
- Tasks that can be partially split logically and parallelized and the remaining to be executed sequentially
This identification will help in planning and correctly sizing the infrastructure required to host and run your application, especially for performance testing.
```
- ***Cache Static Data Used by Critical Processes***: The principle of caching is to reduce the need to poll the database unnecessarily. You not only reduce the I/O, but you also reduce the overall latency.

## 3.2. Database
Chúng ta nói về Latency, và Latency này có liên quan tới Database:
- Luôn có một khoảng thời gian thực hiện một requests between the application and database.
- Database sẽ thành bottleneck, làm giảm thời gian response của request client-server.

Vì vậy sẽ có một vài tiêu chí để đánh giá, xây dựng Database giúp giảm Latency:
- ***Classify Data as Unstructured vs Structured***: data as structured e.g. transactional-based; data unstructured e.g. session, token, external JSON responses,... --> ***Deciding between NoSQL vs SQL***: NoSQL databases are *optimized and designed* for querying unstructured data
- ***Define A Read-Only and Write-Only Model If Applicable***
- ***Normalize Your Database***
- ***Avoid Storing Binary Files Directly in RDMS***
- ***Keep your SQLs lightweight and Avoid Full Table Scan***
- ***Partition Your Data Logically***

## 3.3. Infrastructure

- ***Lựa chọn môi trường triển khai***: On-premise hay thuê ngoài, Kubernetes hay AWS, hoặc một dịch vụ ngoài (DB, Redis,...)
- ***Server Sizing***: For N sub-tasks that needs to be *truly* parallelized, then ideally, we should provision *N* number of physical cores as well. This will guarantee the most optimal performance.
- ***Storage Strategy***: 
- ***Choice of Load Balancing***: With the exception of SPAs (Single Page Applications), Load Balancers (LB) usually sit in front of your application, so it is the first point of contact when a client makes a request. This *guarantees* High Availability (HA) for each component and that the load is ***evenly distributed across each tier***.
- ***Horizontal Scaling***: As part of handling high concurrency, horizontal scaling is required when the existing resources are insufficient to support.

# Ref

- [Ref3: Designing A High Concurrency, Low Latency System Architecture, Part 1](https://medium.com/@markyangjw/designing-a-high-concurrency-low-latency-system-architecture-part-1-f5f3a5f32e36)
