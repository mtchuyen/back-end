## Các thành phần cần có của 1 Open Lakehouse

1 Lakehouse là nơi chứa file (Data Lake), cho phép truy vấn SQL nhanh như một kho dữ liệu (Data Warehouse). Sự kết hợp này được gọi là Lakehouse.

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
- HDFS truyền thống thường lưu file CSV/Parquet rời rạc, khiến việc quản lý khó khăn.
- **Iceberg** biến các thư mục trên HDFS thành các bảng có cấu trúc chuyên nghiệp, hỗ trợ cập nhật (Update/Delete) và tự động quản lý sơ đồ dữ liệu (Schema evolution) – giống hệt cách OneLake quản lý Delta Tables.


#### 3. Công cụ truy vấn và Kết nối (Query Engines)**
Để truy cập dữ liệu từ **hồ** mà không cần sao chép (nạp vào Database truyền thống), có thể dùng các bộ máy truy vấn phân tán:
- **Trino**: Cho phép chạy SQL trên nhiều nguồn dữ liệu khác nhau (HDFS, S3, SQL DB) tại chỗ, giống như cách OneLake kết nối dữ liệu đa đám mây. 
- **Dremio**: Cung cấp giao diện hồ dữ liệu dễ dùng và lớp tăng tốc dữ liệu, có phiên bản cộng đồng miễn phí.
- **StarRocks**: Nếu bạn cần tốc độ truy vấn cực nhanh cho các báo cáo thời gian thực (OLAP), StarRocks là lựa chọn mã nguồn mở vượt trội hiện nay.

**Trino (trước đây là PrestoSQL)**: Rất mạnh trong việc kết nối nhiều nguồn dữ liệu khác nhau. Bạn có thể dùng Trino để join một bảng trong MinIO với một bảng trong SQL Server hiện có của công ty mà không cần di chuyển dữ liệu (tương tự Shortcuts của OneLake).

Dùng Trino để kết nối các nguồn dữ liệu cũ về một điểm duy nhất (tính năng hợp nhất dữ liệu giống OneLake)
- **Kết nối HDFS:** Trino sử dụng Hive Connector để đọc trực tiếp dữ liệu từ HDFS mà không cần chạy MapReduce.
- **Tính năng tương tự Shortcuts của OneLake**: Trino cho phép thực hiện truy vấn liên kết (Federated Query). Bạn có thể JOIN dữ liệu đang nằm trên HDFS với dữ liệu trong SQL Server, Oracle hoặc PostgreSQL của công ty chỉ bằng một câu lệnh SQL duy nhất.


#### 4. Quản trị và Danh mục dữ liệu (Governance & Catalog)
- **Vai trò**: biến các công cụ rời rạc thành một hệ sinh thái. Nó giúp bạn quản lý tập trung: Ai được quyền xem dữ liệu nào, dòng chảy dữ liệu ra sao (Lineage) trên toàn bộ hạ tầng On-premise.

Để đạt được tính năng "hợp nhất" và "duy nhất", cần một lớp quản trị tập trung:
- **Unity Catalog (OSS)**: Phiên bản mã nguồn mở của Databricks giúp quản lý quyền truy cập, dòng dữ liệu (lineage) và danh mục dữ liệu trên toàn hệ thống.
- **Apache Gravitino**: Một giải pháp danh mục dữ liệu liên kết, cho phép quản lý dữ liệu từ nhiều nguồn khác nhau (tương tự tính năng Shortcuts của OneLake).
- **Hive Metastore**: Là tiêu chuẩn để lưu trữ siêu dữ liệu (metadata) trên Hadoop, giúp các công cụ như Spark, Trino biết được bảng dữ liệu nằm ở đâu trên HDFS.
- **Project Nessie**: Nếu bạn muốn tính năng "Git cho dữ liệu" (tạo nhánh, trộn dữ liệu - tương tự các tính năng nâng cao của Microsoft Fabric), Nessie hoạt động rất tốt với Iceberg trên hạ tầng On-premise.

#### 5. Xử lý dữ liệu với Apache Spark
Apache Spark để xử lý ETL. Spark có khả năng đọc/ghi cực tốt vào HDFS và hỗ trợ đầy đủ các định dạng bảng mở (Iceberg, Delta Lake).

### Mô hình kiến trúc đề xuất:
- **Lưu trữ**: HDFS (vốn có của bạn).
- **Định dạng**: Apache Iceberg (lưu trên HDFS).
- **Metadata**: Hive Metastore.
- **Truy vấn & Kết nối**: Trino (Đây là lớp quan trọng nhất để tạo ra trải nghiệm giống OneLake - một điểm truy cập cho mọi nguồn dữ liệu).
- **Bảo mật**: Apache Ranger để phân quyền chi tiết (ai được xem cột nào, dòng nào) trên toàn bộ hệ thống.

**Ví dụ:**

| Thành phần	| Microsoft OneLake (SaaS)	| Giải pháp On-premise (Open Source)| 
| --- | --- | --- |
| Lưu trữ	  | Azure Data Lake Gen2	| MinIO, HDFS
| Định dạng	| Delta | Parquet	Apache Iceberg / Delta Lake
| Truy vấn	| SQL | Endpoint / Spark	Trino / StarRocks
| Quản trị	| Fabric | Admin / Purview	Unity Catalog (OSS) / Amundsen
| Hạ tầng	  | Microsoft quản lý	| Kubernetes (K8s) hoặc Bare-metal

- **OneLake:** Là một "chiếc xe nguyên chiếc" do Microsoft sản xuất. Bạn chỉ việc lái và trả phí thuê xe hàng tháng.
- **HDFS + Iceberg + Trino:** Là bạn tự mua "động cơ, khung gầm, bánh xe" về để đóng thành một chiếc xe tương tự trên chính "sân nhà" (On-premise) của mình.

## Ví dụ:
Hãy tưởng tượng bạn đang quản lý một **thư viện khổng lồ** (chính là hệ thống dữ liệu của bạn). Thay vì sách, chúng ta có các tệp dữ liệu.

Đây là cách các thành phần phối hợp với nhau để biến "kho chứa tệp" thành một "Lakehouse" chuyên nghiệp:

### 1. HDFS (Cái giá sách)
HDFS đơn giản là những chiếc **giá sách cực lớn**. Nó chỉ có nhiệm vụ giữ các tệp tin an toàn. 

Nhưng nếu chỉ có giá sách, bạn sẽ thấy hàng triệu tờ giấy nằm lộn xộn, rất khó tìm.

### 2. Hive Metastore (Cuốn sổ mục lục)
Để biết cuốn sách nào nằm ở giá nào, tầng mấy, bạn cần một **cuốn sổ mục lục.**

- **Nhiệm vụ**: Nó ghi lại rằng: "Bảng dữ liệu Khách hàng nằm ở thư mục /data/customer trên HDFS".

Nếu không có cuốn sổ này, các công cụ khác sẽ bị "mù", không biết dữ liệu ở đâu mà tìm.

### 3. Apache Iceberg (Cách đóng tập hồ sơ)
Thay vì để dữ liệu là những tờ giấy rời rạc (như file CSV), Iceberg giúp bạn **đóng chúng thành những tập hồ sơ (Folder)** có bìa, có số trang và có lịch sử chỉnh sửa.

**Ví dụ: **Nếu bạn lỡ tay xóa một trang trong tập hồ sơ, Iceberg cho phép bạn "quay ngược thời gian" để lấy lại trang đó. Nó giúp dữ liệu trên HDFS trở nên ngăn nắp và khó bị hỏng hơn.

### 4. Apache Spark (Bác thợ làm việc)
Spark giống như một bác thợ cực khỏe và nhanh.
- **Nhiệm vụ:** Bác ấy vào kho (HDFS), mở cuốn sổ mục lục (Hive Metastore) để tìm tập hồ sơ (Iceberg). Sau đó bác ấy thực hiện các công việc nặng nhọc như: tổng hợp số liệu, dọn dẹp dữ liệu bẩn, hoặc chuyển dữ liệu từ chỗ này sang chỗ khác.

### 5. Trino (Người quản gia thông minh - Giống OneLake nhất)
Đây là nhân vật quan trọng nhất để tạo ra trải nghiệm "Lakehouse". Trino giống như một người quản gia đứng ở cửa thư viện.

Bạn (người dùng) **không** cần chạy vào kho, **không** cần gặp bác thợ Spark. Bạn chỉ cần đứng ở cửa và **hỏi Trino**: "Cho tôi biết tổng doanh thu tháng 10".

Trino sẽ tự nhìn vào cuốn sổ mục lục, chạy vào kho lấy dữ liệu và trả kết quả cho bạn ngay lập tức.

**Đặc biệt:** Nếu bạn có một ít dữ liệu ở "kho hàng xóm" (ví dụ SQL Server), Trino cũng có thể chạy sang đó lấy về rồi gộp chung với dữ liệu ở HDFS để trả lời bạn. Đây chính là tính năng **Shortcuts**.


### Quy trình chạy thực tế sẽ như thế này:
- **Dữ liệu thô** đổ vào **HDFS** (Giá sách).
- Bác thợ **Spark** đến dọn dẹp và đóng gói chúng thành định dạng **Iceberg** (Tập hồ sơ ngăn nắp).
- Vị trí của tập hồ sơ này được ghi vào **Hive Metastore** (Sổ mục lục).
- Khi sếp cần xem báo cáo, sếp hỏi người quản gia **Trino**. Trino tra sổ, lấy dữ liệu từ HDFS và hiện lên màn hình cho sếp.
