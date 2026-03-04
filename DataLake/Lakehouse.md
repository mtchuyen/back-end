## Các thành phần cần có của 1 Open Lakehouse
Các thành phần này là cần thiết để có thể xây dựng hệ thống trên **hạ tầng riêng (On-premise)**
- **Hợp nhất (Unified):** Mỗi khách hàng (tenant) chỉ có một **"Lake"** duy nhất. Mọi dữ liệu từ các phòng ban khác nhau đều đổ về đây, giúp loại bỏ tình trạng dữ liệu bị phân tán (data silos).
- **Lối tắt (Shortcuts)**: Tính năng cần thiết cho phép kết nối với dữ liệu ở các nơi khác mà không cần sao chép hay di chuyển dữ liệu đó về **Lake**.
- **Mở và Tương thích:** hỗ trợ các định dạng mở như Delta Parquet, giúp các công cụ phân tích (Power BI, Spark, SQL) có thể truy cập cùng một bản sao dữ liệu.

#### 1. Lớp Lưu trữ (Core Storage)
- **Vai trò:** Đóng vai trò là "Cái hồ" chứa toàn bộ dữ liệu thô và dữ liệu đã xử lý.

**MinIO** cung cấp lưu trữ đối tượng (Object Storage) tương thích hoàn toàn với S3 API. Nó cực kỳ nhanh, nhẹ và có thể chạy trên các máy chủ vật lý hoặc Kubernetes.

#### 2. Định dạng bảng (Table Format):
- **Vai trò:** Để dữ liệu không chỉ là những tệp tin rời rạc mà có cấu trúc như bảng SQL, Hỗ trợ giao dịch ACID (thêm/sửa/xóa dữ liệu mà không làm hỏng file) và "Time Travel" (truy vấn lại dữ liệu tại một thời điểm trong quá khứ).

Có thể dùng các "Open Table Formats" này làm nền móng:
- **Delta Lake**: Do Databricks khởi xướng, cung cấp tính năng giao dịch ACID và quản lý phiên bản dữ liệu.
- **Apache Iceberg**: Một định dạng bảng mở cực kỳ phổ biến, hỗ trợ bởi nhiều công cụ như Snowflake và Cloudera. Sử dụng Apache Iceberg làm định dạng lưu trữ chính để đảm bảo tính mở.

**Apache Iceberg** Hiện đang là lựa chọn hàng đầu cho On-premise vì tính trung lập (không bị ràng buộc vào một công ty cụ thể) và hiệu suất cực tốt khi quản lý các bảng dữ liệu khổng lồ.

#### 3. Công cụ truy vấn và Kết nối (Query Engines)**
Để truy cập dữ liệu từ **hồ** mà không cần sao chép (nạp vào Database truyền thống), có thể dùng các bộ máy truy vấn phân tán:
- **Trino**: Cho phép chạy SQL trên nhiều nguồn dữ liệu khác nhau (HDFS, S3, SQL DB) tại chỗ, giống như cách OneLake kết nối dữ liệu đa đám mây. Dùng Trino để kết nối các nguồn dữ liệu cũ về một điểm duy nhất.
- **Dremio**: Cung cấp giao diện hồ dữ liệu dễ dùng và lớp tăng tốc dữ liệu, có phiên bản cộng đồng miễn phí.
- **StarRocks**: Nếu bạn cần tốc độ truy vấn cực nhanh cho các báo cáo thời gian thực (OLAP), StarRocks là lựa chọn mã nguồn mở vượt trội hiện nay.

**Trino (trước đây là PrestoSQL)**: Rất mạnh trong việc kết nối nhiều nguồn dữ liệu khác nhau. Bạn có thể dùng Trino để join một bảng trong MinIO với một bảng trong SQL Server hiện có của công ty mà không cần di chuyển dữ liệu (tương tự Shortcuts của OneLake).

#### 4. Quản trị và Danh mục dữ liệu (Governance & Catalog)
- **Vai trò**: biến các công cụ rời rạc thành một hệ sinh thái. Nó giúp bạn quản lý tập trung: Ai được quyền xem dữ liệu nào, dòng chảy dữ liệu ra sao (Lineage) trên toàn bộ hạ tầng On-premise.

Để đạt được tính năng "hợp nhất" và "duy nhất", cần một lớp quản trị tập trung:
- **Unity Catalog (OSS)**: Phiên bản mã nguồn mở của Databricks giúp quản lý quyền truy cập, dòng dữ liệu (lineage) và danh mục dữ liệu trên toàn hệ thống.
- **Apache Gravitino**: Một giải pháp danh mục dữ liệu liên kết, cho phép quản lý dữ liệu từ nhiều nguồn khác nhau (tương tự tính năng Shortcuts của OneLake).
