## DataLake
Trong thế giới dữ liệu, thực tế chỉ có 3 khái niệm chính liên quan đến "Lake" và "Warehouse" cần phân biệt. 

Hãy tưởng tượng dữ liệu giống như **nước**, chúng ta sẽ thấy sự tiến hóa như sau:

**1. Data Warehouse (Kho dữ liệu) - "Nước đóng chai"**

Đây là mô hình cũ nhất (từ những năm 1980).

- **Cách hoạt động:** Dữ liệu phải được làm sạch, lọc tạp chất và đóng chai cẩn thận trước khi đưa vào kho. Bạn chỉ có thể đưa nước tinh khiết (dữ liệu có cấu trúc) vào đây.
- **Ưu điểm**: Cực kỳ ngăn nắp, truy vấn (uống nước) rất nhanh và an toàn.
- **Nhược điểm**: Chi phí lưu trữ đắt đỏ, khó thay đổi (muốn đổi loại chai phải làm lại từ đầu).

**2. Data Lake (Hồ dữ liệu) - "Hồ nước tự nhiên"**

Ra đời cùng với thời Hadoop (khoảng 2010). Đây chính là dạng lưu trữ tương tự với với HDFS.

- **Cách hoạt động**: Mọi loại nước (dữ liệu thô, video, hình ảnh, file CSV, log máy chủ) cứ đổ hết vào một cái hồ khổng lồ. Chưa cần biết dùng làm gì, cứ lưu lại đã.
- **Ưu điểm**: Lưu trữ cực rẻ, chứa được mọi định dạng.
- **Nhược điểm**: Rất dễ biến thành **"Data Swamp" (Đầm lầy dữ liệu)** vì nước quá bẩn, lẫn lộn, không ai tìm được gì bên trong nếu không có sơ đồ.

**3. Data Lakehouse (Nhà hồ) - "Hồ có hệ thống lọc và vòi nước"**

Đây là mô hình hiện đại nhất (giống OneLake hay bộ công cụ Iceberg/Trino). Nó là sự kết hợp của hai loại trên.
- **Cách hoạt động**: Bạn vẫn để nước trong hồ (giá rẻ), nhưng bạn lắp thêm một hệ thống quản lý (như Iceberg) và các vòi nước thông minh (như Trino).
- **Ưu điểm**: Vừa lưu trữ được nhiều, rẻ như Data Lake, nhưng lại có thể truy vấn nhanh và quản lý chặt chẽ như Data Warehouse.

**Bảng phân biệt nhanh:**

| Đặc điểm	| Data Warehouse	| Data Lake (Hadoop)	| Data Lakehouse
| --- | --- | --- | --- | 
| Loại dữ liệu	| Chỉ dữ liệu có cấu trúc (Bảng)	| Mọi loại (Thô, ảnh, tệp...)	| Mọi loại, nhưng quản lý như Bảng
| Chi phí	| Rất đắt	| Rẻ	| Rẻ
| Tốc độ truy vấn	| Rất nhanh	| Chậm	| Nhanh
| Tính ngăn nắp	| Rất cao	| Thấp (Dễ thành đầm lầy)	| Cao
| Công cụ ví dụ	| SQL Server, Oracle	| HDFS, S3	| OneLake, Iceberg + Trino

Hệ thống được xây dựng với **Hadoop + Iceberg + Trino** chính là biến cái **Data Lake (Hồ nước)** thành một **Lakehouse (Nhà hồ)** hiện đại!

### Hệ thống trả phí OneLake
OneLake là hồ dữ liệu (data lake) hợp nhất và duy nhất cho toàn bộ tổ chức, được tích hợp sẵn trong nền tảng Microsoft Fabric.

Để dễ hình dung, Microsoft thường gọi OneLake là "OneDrive cho dữ liệu". Nếu OneDrive là nơi lưu trữ mọi tệp văn bản (Word, Excel) cho cá nhân, thì OneLake là nơi lưu trữ tất cả dữ liệu phân tích của một doanh nghiệp tại một vị trí logic duy nhất.

**OneLake nằm ở đâu?**
OneLake chính là một Data Lakehouse. Nó dùng cái "hồ" (Azure Storage) để chứa dữ liệu, nhưng nó ép dữ liệu phải tuân theo các chuẩn mực ngăn nắp để bạn dùng như một **"kho" (Warehouse)** mà không cần di chuyển đi đâu cả.
