## Flow Phân Tích Dữ Liệu

1. **Khám phá dữ liệu ban đầu (Exploratory Data Analysis - EDA)**
   - Kiểm tra kích thước dữ liệu, số dòng/cột, kiểu dữ liệu.
   - Phát hiện và xử lý giá trị thiếu, dữ liệu trùng lặp.
   - Tổng quan các cột đặc biệt (`ID`, `Z_CostContact`, `Z_Revenue`) để quyết định có sử dụng hay loại bỏ.

2. **Tiền xử lý dữ liệu**
   - One-hot encoding cho các biến phân loại → chuẩn bị cho phân tích & mô hình hóa.
   - Gộp lại các cột liên quan để đơn giản hóa phân tích:
     - `Education`, `Marital` → nhóm lại theo trạng thái chính.
     - `AcceptedCmp*` → tạo `AcceptedCmpTotal`.
     - `Mnt*` → có thể gộp thành `MntTotal` nhưng tùy mục tiêu giữ nguyên để phân tích chi tiết.
   - Loại bỏ các cột không cần thiết (như `Z_CostContact`, `Z_Revenue`).

3. **Phân tích phân bố dữ liệu**
   - Boxplot & Violinplot cho các cột dạng số, ngoại trừ biến nhị phân.
   - Nhận xét:
     - Các biến nhân khẩu học (`Age`, `Customer_Days`, `Income`) phân bố khá đều.
     - Các biến chi tiêu (`Mnt*`) và hành vi mua sắm (`Num*Purchases`, `NumWebVisitsMonth`) tập trung nhiều ở giá trị thấp.
   - Không loại bỏ outlier ở nhóm chi tiêu cao vì đây là những khách hàng tiềm năng quan trọng.

4. **Phân tích các biến phân loại**
   - Countplot cho các biến object (`Education`, `Marital`...).
   - Đánh giá sự cân bằng hay chênh lệch giữa các nhóm khách hàng.

5. **Phân tích tương quan**
   - Sử dụng ma trận tương quan Kendall để xử lý biến nhị phân.
   - Nhận xét chính:
     - Nhóm chi tiêu sản phẩm (`MntWines`, `MntMeatProducts`, `MntFruits`, `MntFishProducts`, `MntSweetProducts`, `MntGoldProds`) có tương quan cao với nhau → khách hàng có xu hướng chi tiêu đa dạng.
     - `Teenhome`, `Kidhome`, và `Customer_Days` có tương quan cao với `NumDealsPurchases` và `NumWebVisitsMonth`.
     - `NumDealsPurchases` và `NumWebVisitsMonth` có tương quan với `MntTotal` thấp hơn so với `NumCatalogPurchases`, `NumStorePurchases`, `NumWebPurchases`.
     - Đặc biệt: `Kidhome` và `NumWebVisitsMonth` còn có tương quan âm với `MntTotal`.
