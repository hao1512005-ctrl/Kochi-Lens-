# SOFTWARE REQUIREMENT SPECIFICATION (SRS)

## Chức năng: Quản lý Sản phẩm (Product Information Management - PIM)

---

# 1. Giới thiệu

## 1.1. Mục đích

Tài liệu này mô tả các yêu cầu phần mềm cho chức năng Quản lý Sản phẩm (PIM) trong hệ thống website bán thiết bị ngành ảnh của công ty Kochi Lens.

## 1.2. Phạm vi

Chức năng PIM cho phép quản lý thông tin sản phẩm, biến thể (màu sắc, kích thước), và tồn kho theo thời gian thực, phục vụ cho việc hiển thị sản phẩm và xử lý đơn hàng.

---

# 2. Mô hình hóa quy trình (Business Flow)

## 2.1. Actors

* Admin: Quản lý sản phẩm và biến thể
* Customer: Xem và mua sản phẩm
* Warehouse Staff: Quản lý tồn kho

## 2.2. Use Case Diagram

```mermaid
usecaseDiagram
actor Admin
actor Customer
actor "Warehouse Staff" as Warehouse

Admin --> (Create Product)
Admin --> (Update Product)
Admin --> (Delete Product)
Admin --> (Manage Variants)
Admin --> (Update Inventory)

Customer --> (View Products)
Customer --> (View Product Detail)
Customer --> (Select Variant)
Customer --> (Add to Cart)

Warehouse --> (Check Inventory)
Warehouse --> (Update Inventory)

(Select Variant) --> (Check Inventory)
(Add to Cart) --> (Check Inventory)
```

## 2.3. Activity Flow

### Luồng chính

1. Khách hàng truy cập hệ thống
2. Xem danh sách sản phẩm
3. Chọn sản phẩm
4. Chọn biến thể (màu, kích thước)
5. Hệ thống kiểm tra tồn kho
6. Nếu còn hàng → cho phép thêm vào giỏ
7. Khách hàng thêm vào giỏ
8. Tiến hành thanh toán
9. Thanh toán thành công
10. Tạo đơn hàng
11. Cập nhật tồn kho

### Luồng thay thế

* Nếu hết hàng → hiển thị thông báo hết hàng
* Nếu biến thể không tồn tại → không cho chọn

---

# 3. Đặc tả chức năng (Functional Requirements)

## 3.1. User Stories - Admin

* Là Admin, tôi muốn tạo sản phẩm mới để bán hàng
* Là Admin, tôi muốn chỉnh sửa thông tin sản phẩm
* Là Admin, tôi muốn xóa sản phẩm
* Là Admin, tôi muốn quản lý biến thể sản phẩm
* Là Admin, tôi muốn cập nhật tồn kho

## 3.2. User Stories - Customer

* Là khách hàng, tôi muốn xem danh sách sản phẩm
* Là khách hàng, tôi muốn xem chi tiết sản phẩm
* Là khách hàng, tôi muốn chọn biến thể
* Là khách hàng, tôi muốn biết tình trạng tồn kho
* Là khách hàng, tôi muốn thêm sản phẩm vào giỏ

## 3.3. User Stories - Warehouse Staff

* Là nhân viên kho, tôi muốn kiểm tra tồn kho
* Là nhân viên kho, tôi muốn cập nhật tồn kho

## 3.4. Functional Requirements chi tiết

* Hệ thống phải cho phép tạo, sửa, xóa sản phẩm
* Hệ thống phải hỗ trợ nhiều biến thể cho một sản phẩm
* Hệ thống phải kiểm tra tồn kho theo biến thể
* Hệ thống phải cập nhật tồn kho theo thời gian thực
* Hệ thống không cho phép mua sản phẩm hết hàng
* Hệ thống hiển thị trạng thái tồn kho

---

# 4. Đặc tả dữ liệu (Data Schema)

## 4.1. Partner (Khách hàng)

* PartnerID (INT)
* Name (VARCHAR)
* TaxCode (VARCHAR)
* Address (TEXT)
* Phone (VARCHAR)
* Email (VARCHAR)

## 4.2. Product

* ProductID (INT)
* Name (VARCHAR)
* SKU (VARCHAR)
* Barcode (VARCHAR)
* Price (DECIMAL)
* VAT (FLOAT)
* Description (TEXT)
* CreatedAt (DATETIME)

## 4.3. Product Variant

* VariantID (INT)
* ProductID (INT)
* Color (VARCHAR)
* Size (VARCHAR)
* Stock (INT)
* Price (DECIMAL)

## 4.4. Order

* OrderID (INT)
* OrderNumber (VARCHAR)
* PartnerID (INT)
* Status (VARCHAR)
* TotalAmount (DECIMAL)
* CreatedAt (DATETIME)

---

# 5. Yêu cầu phi chức năng (Non-functional Requirements)

* Hiệu năng: Hệ thống phải phản hồi dưới 2 giây
* Khả dụng: Hệ thống hoạt động 24/7
* Bảo mật: Dữ liệu khách hàng phải được bảo vệ
* Khả mở rộng: Hỗ trợ số lượng lớn sản phẩm

---

# 6. Kết luận

Chức năng PIM đóng vai trò quan trọng trong hệ thống, đảm bảo quản lý sản phẩm và tồn kho chính xác, hỗ trợ hiệu quả cho quá trình bán hàng và xử lý đơn hàng.
