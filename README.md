# 📱 NHK Mobile - Hệ Thống Website Thương Mại Điện Tử

**NHK Mobile** là nền tảng thương mại điện tử chuyên kinh doanh thiết bị di động và phụ kiện công nghệ. Hệ thống được xây dựng theo kiến trúc Client - Server bằng PHP thuần (PDO) và MySQL, cung cấp trải nghiệm mua sắm trọn vẹn cho khách hàng (tìm kiếm thông minh, lọc sản phẩm động, so sánh cấu hình, tính trả góp, áp dụng mã giảm giá, chiết khấu hạng thành viên, thanh toán đa phương thức) đồng thời trang bị hệ thống quản trị (Admin Dashboard) và công cụ chẩn đoán vận hành trực quan.

---

## 📋 Mục lục
1. [Giới thiệu tổng quan](#-giới-thiệu-tổng-quan)
2. [Công nghệ & Kiến trúc hệ thống](#-công-nghệ--kiến-trúc-hệ-thống)
3. [Thành viên nhóm & Phân công nhiệm vụ](#-thành-viên-nhóm--phân-công-nhiệm-vụ)
4. [Danh sách chức năng hệ thống](#-danh-sách-chức-năng-hệ-thống)
5. [Thiết kế Cơ sở dữ liệu](#-thiết-kế-cơ-sở-dữ-liệu)
6. [Điểm nhấn kỹ thuật](#-điểm-nhấn-kỹ-thuật-technical-highlights)
7. [Hướng dẫn cài đặt & Chạy trên WampServer](#-hướng-dẫn-cài-đặt--chạy-trên-wampserver)

---

## 📖 Giới thiệu tổng quan

Dự án giải quyết bài toán số hóa quy trình bán lẻ điện thoại di động với 2 phân hệ chính:
* **Phân hệ Khách hàng (Storefront):** Giao diện hiện đại theo phong cách tối giản (*Apple Aesthetic*), hỗ trợ khách hàng tra cứu sản phẩm nhanh chóng, đối chiếu thông số kỹ thuật giữa nhiều dòng máy, tính toán phương án mua trả góp, quản lý giỏ hàng theo phiên làm việc kết hợp đồng bộ cơ sở dữ liệu và đặt hàng trực tuyến.
* **Phân hệ Quản trị (Admin Panel):** Cung cấp bức tranh toàn cảnh về doanh thu, đơn đặt hàng, tồn kho, bảo hành/IMEI và phân hạng khách hàng thân thiết (CRM), giúp quản trị viên vận hành cửa hàng chính xác và hiệu quả.

---

## 🛠 Công nghệ & Kiến trúc hệ thống

* **Môi trường Web Server:** WampServer (Apache, PHP 8.2, MySQL)
* **Back-end:** PHP 8.2 thuần sử dụng PDO (*PHP Data Objects*), kiến trúc phân tách module nghiệp vụ rõ ràng (xác thực & phân quyền, xử lý giỏ hàng, kết nối CSDL, API bất đồng bộ & Webhook)
* **Cơ sở dữ liệu:** MySQL (`web_ban_dien_thoai`)
* **Front-end:** HTML5, CSS3 (Bootstrap 5, Bootstrap Icons, Responsive Design, hiệu ứng Micro-interactions & Scroll Reveal), JavaScript (Fetch API / AJAX)
* **Bảo mật & Quản lý trạng thái:**
  * Cấu hình bảo mật máy chủ Apache: tắt Directory Listing, ẩn thông tin server, thiết lập các Security Headers (`X-Content-Type-Options`, `X-Frame-Options`, `X-XSS-Protection`, `Referrer-Policy`), chặn truy cập trực tiếp vào các tệp cấu hình, dữ liệu SQL, tài liệu và nhật ký hệ thống.
  * Mã hóa mật khẩu một chiều bằng thuật toán `BCRYPT` (`password_hash` / `password_verify`).
  * Chống tấn công SQL Injection triệt để bằng PDO `Prepared Statement`.
  * Quản lý phiên đăng nhập, danh sách so sánh và giỏ hàng qua `$_SESSION` kết hợp đồng bộ cơ sở dữ liệu.

---

## 👥 Thành viên nhóm & Phân công nhiệm vụ

| STT | Họ và Tên | MSSV | Vai trò | Chức năng đảm nhiệm | Kỹ thuật áp dụng chính |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 1 | **Lê Tuấn Dũng** | [24211TT4229] | Backend & Database | **Tài khoản người dùng:** Đăng ký, Đăng nhập, Cập nhật thông tin cá nhân, Đổi mật khẩu, Xem lịch sử đơn hàng.<br>**Danh sách & Bộ lọc sản phẩm:** Hiển thị sản phẩm theo danh mục, Phân trang (Pagination), Sắp xếp theo giá/độ phổ biến, Lọc động theo giá/thương hiệu/dung lượng.<br>**Admin - Quản lý sản phẩm:** Thêm/sửa/xóa sản phẩm, Quản lý danh mục, Upload hình ảnh.<br>**Tính năng nâng cao & Bảo mật:** Danh sách yêu thích (Wishlist), Gửi email tự động (khôi phục mật khẩu & xác nhận đơn hàng), Thiết kế CSDL & Cấu hình bảo mật hệ thống. | Xây dựng truy vấn SQL động (*Dynamic SQL*), phân trang tối ưu bằng `OFFSET`, chống SQL Injection bằng PDO Prepared Statement, băm mật khẩu `BCRYPT`, bảo mật `Session` và cấu hình bảo mật Apache. |
| 2 | **Nguyễn Tuấn Anh** | [24211TT3636] | Front-end & UI/UX | **Trang chủ:** Hero Banner quảng cáo, Hiển thị danh sách sản phẩm nổi bật, sản phẩm bán chạy, sản phẩm gợi ý.<br>**Chi tiết & So sánh sản phẩm:** Hiển thị bộ ảnh, mô tả chi tiết, giá bán, số lượng tồn kho, hệ thống đánh giá & bình luận sao, sản phẩm liên quan, bảng tính trả góp và so sánh cấu hình tối đa 3 sản phẩm.<br>**Tìm kiếm thông minh:** Tìm kiếm theo từ khóa & Gợi ý tự động tức thì (Autocomplete).<br>**Admin - Cấu hình & Liên hệ:** Quản lý thông tin cửa hàng (Hotline, Email, Địa chỉ, Banner trang chủ). | Thiết kế giao diện Apple Aesthetic với hiệu ứng Micro-interactions & Scroll Reveal, tối ưu truy vấn trang chủ (`is_featured`, `LIMIT`), bóc tách chuỗi thông số kỹ thuật bằng `explode()` & Regex, thuật toán gợi ý chéo (*Cross-selling*), tích hợp AJAX trả về `JSON`. |
| 3 | **Nguyễn Quốc Anh Hòa** | [24211TT0714] | Business Logic & Admin | **Giỏ hàng & Khuyến mãi:** Thêm/xóa/cập nhật số lượng, Lưu & đồng bộ giỏ hàng DB, Tính tổng tiền tự động, Áp dụng mã giảm giá (Coupon) trực tiếp bằng AJAX, Tính chiết khấu theo hạng thành viên (Bronze, Silver, Gold, Diamond).<br>**Đặt hàng (Checkout) & Tra cứu:** Thu thập & kiểm tra thông tin nhận hàng, Thanh toán đa phương thức (COD / Tiền mặt tại cửa hàng / Giả lập Online qua Webhook), Xác nhận & theo dõi trạng thái đơn hàng.<br>**Admin & Kiểm thử hệ thống:** Dashboard thống kê (tổng đơn hàng, tổng doanh thu, biểu đồ doanh thu ngày/tháng), Xuất báo cáo, Quản lý đơn hàng (cập nhật trạng thái giao hàng), Quản lý người dùng (khóa/mở tài khoản) & Kiểm tra sức khỏe hệ thống. | Quản lý State giỏ hàng đa chiều `$_SESSION['cart']` kết hợp đồng bộ CSDL, xử lý Transaction ghi dữ liệu quan hệ 2 bảng (`orders` & `order_items`) bằng `PDO::lastInsertId()`, tích hợp Fetch API & Webhook JSON. |

---

## ✅ Danh sách chức năng hệ thống

### 1. Phân hệ Khách hàng (Storefront)
- [x] **Trang chủ:** Hiển thị Banner quảng cáo, danh sách sản phẩm nổi bật, sản phẩm bán chạy và sản phẩm gợi ý.
- [x] **Danh mục & Bộ lọc:** Lọc động theo danh mục/thương hiệu, khoảng giá, dung lượng; sắp xếp theo giá hoặc độ phổ biến; phân trang tối ưu tốc độ tải.
- [x] **Tìm kiếm thông minh:** Tìm kiếm chính xác theo từ khóa và gợi ý kết quả tức thì (Autocomplete) ngay trên thanh điều hướng.
- [x] **Chi tiết & So sánh sản phẩm:** Hiển thị hình ảnh sắc nét, mô tả chi tiết, thông số kỹ thuật dạng chip, số lượng tồn kho, đánh giá & bình luận sao, sản phẩm liên quan, bảng tính trả góp và so sánh đối chiếu tối đa 3 sản phẩm cùng lúc.
- [x] **Giỏ hàng & Khuyến mãi:** Thêm/sửa/xóa số lượng sản phẩm, tự động tính tổng tiền, áp dụng mã giảm giá bằng AJAX không cần tải lại trang và tự động trừ chiết khấu theo hạng thành viên (`Bronze` 0%, `Silver` 2%, `Gold` 5%, `Diamond` 8%).
- [x] **Đặt hàng & Thanh toán:** Nhập thông tin giao hàng, kiểm tra dữ liệu đầu vào, hỗ trợ thanh toán COD, thanh toán tiền mặt tại cửa hàng và giả lập thanh toán trực tuyến qua Webhook.
- [x] **Tài khoản & Tra cứu:** Đăng ký, đăng nhập, cập nhật thông tin cá nhân, đổi mật khẩu, xem lịch sử mua hàng, tra cứu trạng thái vận chuyển đơn hàng và xem thông tin liên hệ cửa hàng.

### 2. Phân hệ Quản trị viên (Admin Panel)
- [x] **Dashboard & Báo cáo:** Thống kê tổng số đơn hàng, tổng doanh thu, biểu đồ thống kê doanh thu theo ngày/tháng và xuất báo cáo thống kê.
- [x] **Quản lý sản phẩm & danh mục:** Thêm, sửa, xóa sản phẩm, quản lý danh mục và upload hình ảnh sản phẩm.
- [x] **Quản lý đơn hàng:** Xem danh sách đơn đặt hàng và cập nhật trạng thái xử lý (`Chờ xác nhận` ➔ `Đang giao` ➔ `Hoàn thành`).
- [x] **Quản lý người dùng:** Xem danh sách tài khoản khách hàng, quản lý phân hạng thành viên và khóa / mở khóa quyền truy cập.
- [x] **Cấu hình & Bảo trì hệ thống:** Cập nhật Hotline, địa chỉ cửa hàng, Banner trang chủ, khôi phục dữ liệu mẫu và chạy công cụ kiểm tra, chẩn đoán trạng thái vận hành toàn hệ thống.

### 3. Tính năng nâng cao & Định hướng mở rộng
- [x] Danh sách sản phẩm yêu thích (Wishlist).
- [x] Hệ thống gửi email HTML tự động (khôi phục mật khẩu và xác nhận tiếp nhận đơn hàng).
- [ ] Tích hợp bản đồ chỉ đường tương tác, Chatbox AI tư vấn tự động và triển khai (Deploy) lên Cloud Server.

---

## 🗄 Thiết kế Cơ sở dữ liệu

Hệ thống sử dụng cơ sở dữ liệu MySQL tên **`web_ban_dien_thoai`** (bảng mã `utf8mb4_unicode_ci`) với các nhóm bảng chính:
* **Nhóm Tài khoản & Phân quyền:** `users` (thông tin khách hàng, hạng thành viên `membership_tier`, trạng thái khóa/mở), `admins` (tài khoản quản trị), `password_resets` (mã token khôi phục mật khẩu), `admin_logs` (nhật ký thao tác quản trị).
* **Nhóm Sản phẩm & Tương tác:** `products` (thông tin máy, giá, tồn kho, thông số `specs`, đánh giá trung bình), `reviews` (bình luận & chấm sao của khách hàng), `wishlists` (danh sách yêu thích).
* **Nhóm Giỏ hàng & Đơn hàng:** `cart_items` (đồng bộ giỏ hàng theo phiên & người dùng), `orders` (thông tin hóa đơn, phương thức thanh toán, trạng thái giao hàng, cờ mua trả góp), `order_items` (chi tiết từng sản phẩm thuộc đơn hàng).
* **Nhóm Hậu mãi & Nội dung:** `warranties` (thông tin bảo hành), `imeis` (quản lý mã IMEI thiết bị), `repair_history` (lịch sử sửa chữa), `news` (tin tức công nghệ), `chatbot_rules` (kịch bản phản hồi tự động).

---

## 🌟 Điểm nhấn kỹ thuật (Technical Highlights)

### 1. Truy vấn SQL động & Chống SQL Injection — *Lê Tuấn Dũng*
Thay vì viết nhiều câu lệnh query rời rạc cho từng tổ hợp bộ lọc, hệ thống khởi tạo truy vấn động kết hợp **PDO Prepared Statement** để nối điều kiện linh hoạt và ngăn chặn triệt để lỗ hổng SQL Injection:
```php
$sql = "SELECT * FROM products WHERE 1=1";
$params = [];

if ($category) {
    $sql .= " AND category = ?";
    $params[] = $category;
}
if ($search) {
    $sql .= " AND name LIKE ?";
    $params[] = "%$search%";
}

$stmt = $pdo->prepare($sql);
$stmt->execute($params);
```

### 2. Bảo mật xác thực & Cấu hình Apache — *Lê Tuấn Dũng*
Mật khẩu người dùng được mã hóa một chiều bằng thuật toán **BCRYPT** (`password_hash` / `password_verify`) trước khi lưu vào cơ sở dữ liệu, kết hợp cấu hình Apache tắt Directory Listing, bổ sung các Security Headers và chặn truy cập trực tiếp vào các tệp cấu hình, kịch bản SQL hoặc tệp nhật ký hệ thống:
```php
$stmt = $pdo->prepare("SELECT * FROM users WHERE email = ? OR fullname = ?");
$stmt->execute([$email_or_user, $email_or_user]);
$user = $stmt->fetch();

if ($user && password_verify($password, $user['password'])) {
    $_SESSION['user_id'] = $user['id'];
    $_SESSION['user_fullname'] = $user['fullname'];
}
```

### 3. Tìm kiếm gợi ý Real-time với AJAX & JSON — *Nguyễn Tuấn Anh*
Nâng cao trải nghiệm người dùng (UX) bằng API trả về kết quả tìm kiếm ngay lập tức định dạng `JSON` thông qua **Fetch API / AJAX** khi người dùng đang nhập từ khóa mà không cần tải lại trang:
```php
$q = $_GET['q'] ?? '';
$stmt = $pdo->prepare("SELECT id, name, image, price FROM products WHERE name LIKE ? LIMIT 5");
$stmt->execute(["%$q%"]);

echo json_encode($stmt->fetchAll(PDO::FETCH_ASSOC));
```

### 4. Tối ưu tải trang chủ, Bóc tách thông số & Gợi ý chéo — *Nguyễn Tuấn Anh*
* **Tối ưu truy vấn trang chủ:** Kết hợp cờ trạng thái `is_featured` và mệnh đề `LIMIT 8` thay vì truy vấn toàn bộ bảng sản phẩm, giúp tăng tốc độ phản hồi trang chủ.
* **Bóc tách thông số & So sánh cấu hình:** Chuỗi thông số kỹ thuật thô từ cơ sở dữ liệu được tách bằng `explode()` kết hợp Regex để tự động phân loại thành các tiêu chí chuẩn (RAM, Bộ nhớ trong, Chip xử lý, Camera, Màn hình, Pin) phục vụ trang chi tiết và bảng so sánh đối chiếu 3 sản phẩm.
* **Gợi ý bán thêm (Cross-selling):** Truy vấn các sản phẩm cùng danh mục (`category`) nhưng loại trừ `id` sản phẩm đang xem để gợi ý sản phẩm tương tự.

### 5. Quản lý giỏ hàng Session & Áp dụng Coupon bất đồng bộ — *Nguyễn Quốc Anh Hòa*
Lưu trữ trạng thái giỏ hàng trực tiếp trên mảng đa chiều `$_SESSION['cart']` kết hợp cơ chế đồng bộ với cơ sở dữ liệu khi người dùng đăng nhập, giúp thao tác cập nhật diễn ra tức thì và giảm tải I/O cho database. Đồng thời tích hợp **Fetch API** để kiểm tra và áp dụng mã giảm giá trực tiếp trên giao diện giỏ hàng:
```php
if (!isset($_SESSION['cart'][$productId])) {
    $_SESSION['cart'][$productId] = [
        'name'  => $product['name'],
        'price' => $product['price'],
        'image' => $product['image'],
        'qty'   => 1
    ];
} else {
    $_SESSION['cart'][$productId]['qty']++;
}
```

### 6. Đảm bảo toàn vẹn dữ liệu đặt hàng & Webhook thanh toán — *Nguyễn Quốc Anh Hòa*
Trong luồng thanh toán, hệ thống tự động tính toán chiết khấu hạng thành viên kết hợp mã giảm giá, sau đó sử dụng `PDO::lastInsertId()` để lấy mã hóa đơn vừa tạo ở bảng `orders` làm khóa ngoại liên kết lưu toàn bộ chi tiết giỏ hàng vào bảng `order_items`, đồng thời hỗ trợ cập nhật trạng thái thanh toán tự động qua Webhook:
```php
$sqlOrder = "INSERT INTO orders (customer_name, customer_phone, customer_address, total_price, status, payment_method, user_id, is_installment) 
             VALUES (?, ?, ?, ?, 'Chờ xác nhận', ?, ?, ?)";
$stmtOrder = $pdo->prepare($sqlOrder);
$stmtOrder->execute([$name, $phone, $address, $finalTotal, $payment, $userId, $isInstallmentVal]);

$orderId = $pdo->lastInsertId();

$sqlItem = "INSERT INTO order_items (order_id, product_id, product_name, price, quantity) VALUES (?, ?, ?, ?, ?)";
$stmtItem = $pdo->prepare($sqlItem);
foreach ($cartItems as $pid => $item) {
    $stmtItem->execute([$orderId, $pid, $item['name'], $item['price'], (int)$item['qty']]);
}
```

---

## ⚙️ Hướng dẫn cài đặt & Chạy trên WampServer

### 1. Yêu cầu môi trường
* **WampServer** (khuyến nghị bản 64-bit, tích hợp **Apache**, **PHP 8.2** và **MySQL**).
* **PHP Extensions cần bật:** `pdo`, `pdo_mysql`, `mbstring`, `json`, `session`, `gd` *(Nhấp chuột trái vào biểu tượng WampServer dưới khay hệ thống ➔ **PHP** ➔ **PHP extensions** để kiểm tra và kích hoạt)*.
* **Apache Modules cần bật:** `headers_module` và `rewrite_module` *(Nhấp chuột trái vào biểu tượng WampServer ➔ **Apache** ➔ **Apache modules** để kích hoạt các quy tắc bảo mật)*.

### 2. Các bước cài đặt

**Bước 1: Đưa mã nguồn vào thư mục `www` của WampServer**
```bash
# Mặc định thư mục gốc của WampServer 64-bit nằm tại C:\wamp64\www
cd C:\wamp64\www
git clone [Link-repository-cua-nhom] nhk-mobile
```
*(Nếu tải mã nguồn dạng file nén ZIP, hãy giải nén toàn bộ vào đường dẫn `C:\wamp64\www\BE_Project`).*

**Bước 2: Khởi động WampServer & Tạo Cơ sở dữ liệu**
1. Mở ứng dụng **WampServer**, đợi biểu tượng chữ **W** dưới khay hệ thống (System Tray) chuyển sang **màu xanh lá** (tất cả dịch vụ Apache & MySQL đã sẵn sàng).
2. Truy cập **phpMyAdmin** tại địa chỉ `http://localhost/phpmyadmin` (tài khoản mặc định: `root`, mật khẩu để trống).
3. Tạo một cơ sở dữ liệu mới có tên `web_ban_dien_thoai` (chọn bảng mã `utf8mb4_unicode_ci`).
4. Chọn cơ sở dữ liệu `web_ban_dien_thoai` ➔ chuyển sang tab **Import** ➔ chọn kịch bản SQL khởi tạo cơ sở dữ liệu của dự án và nhấn **Import / Go**.

**Bước 3: Cấu hình kết nối Database**
Kiểm tra thông số kết nối PDO trong module cấu hình database của dự án cho khớp với WampServer:
```php
$host = 'localhost';
$dbname = 'web_ban_dien_thoai';
$username = 'root';
$password = ''; // Mặc định trên WampServer để trống
```

**Bước 4: Khởi chạy & Kiểm tra hệ thống**
Mở trình duyệt và truy cập các đường dẫn sau:
* **Trang khách hàng:** `http://localhost/BE_Project/`.