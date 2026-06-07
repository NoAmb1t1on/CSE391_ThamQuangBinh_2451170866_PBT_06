# PBT_06:
---
## TRACK A - BOOTSTRAP 5
### Phần A:
#### Câu A1(tuan_4_css_frameworks - bootstrap - 02_grid_system - 3. Cú pháp cơ bản):

| Kích thước | Số cột | Box layout|
|------------|--------|-----------|
| <768px | 1 cột | 4 hàng (Box 1-4 xếp dọc) |
| 768px - 991px | 2 cột | 2 hàng (Mỗi hàng 2 box) |
| ≥992px | 4 cột | 1 hàng (4 box nằm ngang) |

#### Câu A2(tuan_4_css_frameworks - bootstrap - 04_utilities - 3. Display, Spacing):
1. Giải thích `d-none d-md-block`:
    - `d-none`: Ẩn element trên mọi màn hình (display: none).
    - `d-md-block`: Hiện element dạng block từ kích thước màn hình md (≥ 768px) trở lên.
    - Kết luận: Element này chỉ hiển thị trên tablet và desktop, ẩn trên mobile.
2. 5 Spacing utilities:
    - `mt-3`: Margin-top: 1rem (16px).
    - `px-4`: Padding-left và Padding-right: 1.5rem (24px).
    - `mb-auto`: Margin-bottom: auto (đẩy element lên trên).
    - `p-5`: Padding 3rem (48px) cho cả 4 phía.
    - `ms-2`: Margin-start (trái): 0.5rem (8px).
3. Sự khác nhau về Container:
    - `.container`: Có `max-width` thay đổi theo từng breakpoint, tự động căn giữa.
    - `.container-fluid`: Luôn `full-width` (100% màn hình) ở mọi kích thước.
    - `.container-md`: `Full0-width` dưới `md` (< 768px), từ `md` trở lên sẽ có `max-width` cố định.
### Phần C:
#### Câu C1:
1. Để đổi màu `$primary` từ xanh mặc định sang `#E63946`, bạn không nên can thiệp trực tiếp vào file CSS đã biên dịch (`bootstrap.min.css`). Thay vào đó, quy trình chuẩn là sử dụng SASS (SCSS).
    - Quy trình:
      - Công cụ cần thiết: * Node.js (để cài đặt gói Bootstrap).
      - Trình biên dịch SASS (thường tích hợp trong các build tool như Vite, Webpack hoặc Gulp).
      - File cần modify:
        - Tạo một file SCSS riêng (ví dụ: `custom.scss`).
        - Trong file `custom.scss`, bạn khai báo lại giá trị biến trước khi import file Bootstrap:
          ```scss
          $primary: #E63946; 
          @import "node_modules/bootstrap/scss/bootstrap";
          ```
          - Sử dụng file `custom.scss` này thay cho file CSS mặc định.
2. Không nên override trực tiếp (`.btn-primary { background: red; }`) vì:
  - Khả năng bảo trì: Khi bạn update phiên bản Bootstrap, các ghi đè thủ công có thể bị lỗi hoặc xung đột. Dùng SASS giúp biến đổi toàn bộ hệ thống (buttons, links, badges, alerts) sử dụng màu primary một cách đồng bộ.
  - Tính kế thừa: Khi thay đổi biến $primary, Bootstrap tự động tính toán các màu sắc liên quan (như màu hover, màu active, màu chữ tương phản) để đảm bảo tính thẩm mỹ và dễ đọc. Việc viết CSS thủ công khiến bạn mất đi sự hỗ trợ thông minh này.
#### Câu C2:
- HTML:
```html
<nav class="navbar">
  <div class="logo">Brand</div>
  <ul class="nav-links"><li>Home</li><li>Products</li></ul>
</nav>

<div class="card">
  <img src="product.jpg" alt="Product">
  <h3>Product Name</h3>
  <button>Buy Now</button>
</div>
```
- CSS:
```css
/* Navbar */
.navbar { display: flex; justify-content: space-between; padding: 1rem; }
@media (max-width: 768px) { .nav-links { display: none; } } /* Cần JS để toggle */

/* Card */
.card { border: 1px solid #ddd; padding: 16px; border-radius: 8px; transition: 0.3s; }
.card:hover { box-shadow: 0 4px 8px rgba(0,0,0,0.1); }
```
- **So Sánh**:

| Tiêu chí | CSS Thuần | Bootstrap |
|----------|-----------|-----------|
|Số dòng | ~50-80 dòng | ~0 dòng (chỉ dùng class) |
| Thời gian phát triển | 30 - 60 phút | 5 - 10 phút |
| Khả năng tùy biến | Rất cao, kiểm soát tuyệt đối | Cần dùng SASS hoặc override class |

- Khi nào NÊN và KHÔNG NÊN dùng Bootstrap:
    - NÊN dùng Bootstrap khi:
        - Dự án cần tốc độ: Bạn cần build một bản prototype hoặc MVP (Minimum Viable Product) để đưa cho khách hàng xem ngay lập tức.
        - eam không chuyên về design: Bootstrap cung cấp một "Design System" có sẵn, giúp giao diện trông chuyên nghiệp và nhất quán mà không cần designer vẽ từng pixel.
        - Dự án Admin/Dashboard: Các dự án quản trị nội bộ thường có cấu trúc lặp lại, Bootstrap xử lý cực tốt các thành phần này (tables, forms, modals).
    - KHÔNG NÊN dùng Bootstrap khi:
        - Website có thiết kế độc bản (Brand identity cao): Nếu thiết kế của bạn rất khác lạ, việc cố ép Bootstrap theo ý muốn sẽ tốn công sức hơn là viết CSS thuần (bạn phải "gỡ" các style mặc định trước khi viết cái mới).
        - Cần tối ưu dung lượng (Performance): Bootstrap mang theo một lượng lớn code CSS/JS. Nếu bạn chỉ cần một vài component đơn giản, việc import cả thư viện là lãng phí (làm chậm tốc độ tải trang).
        - Đang học lập trình Frontend: Nếu bạn mới bắt đầu, hãy tránh xa framework cho đến khi bạn thuần thục CSS Flexbox, Grid và cách xử lý Responsive. Nếu không, bạn sẽ trở thành "thợ dán class" và mất đi tư duy cốt lõi về layout.

---

## TRACK B - TAILWINDCSS
### Phần A:
#### Câu A1(tuan_4_css_frameworks - tailwind_css - 01_utility_first):
- Thành phần Container bao ngoài:
    - flex → display: flex;
    - items-center → align-items: center;
    - justify-between → justify-content: space-between;
    - p-4 → padding: 1rem; (16px)
    - bg-white → background-color: #ffffff;
    - shadow-md → box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1); (đổ bóng cỡ vừa)
    - rounded-lg → border-radius: 0.5rem; (8px)
    - hover:shadow-xl → box-shadow tăng lên cỡ lớn khi di chuột vào phần tử
    - transition-shadow → transition-property: box-shadow; (chỉ tạo hiệu ứng mượt cho đổ bóng)
    - duration-300 → transition-duration: 300ms; (thời gian chạy hiệu ứng là 300 mili giây)
- Thành phần Ảnh đại diện (img):
    - w-16 → width: 4rem; (64px)
    - h-16 → height: 4rem; (64px)
    - rounded-full → border-radius: 9999px; (bo tròn hoàn toàn thành hình tròn)
    - object-cover → object-fit: cover; (ảnh không bị méo, tự co giãn vừa khung)
- Thành phần Khối văn bản (div con):
    - ml-4 → margin-left: 1rem; (16px)
    - flex-1 → flex: 1 1 0%; (giúp khối văn bản giãn ra chiếm nốt không gian trống còn lại)
    - text-lg → font-size: 1.125rem; (18px)
    - font-semibold → font-weight: 600; (chữ đậm vừa)
    - text-gray-800 → color: #1f2937; (màu chữ xám đậm)
    - truncate → overflow: hidden; text-overflow: ellipsis; white-space: nowrap; (ẩn chữ thừa và thay bằng dấu ... trên 1 dòng)
    - text-sm → font-size: 0.875rem; (14px)
    - text-gray-500 → color: #6b7280; (màu chữ xám nhạt)
- Thành phần Nút bấm (button):
    - px-4 → padding-left: 1rem; padding-right: 1rem; (16px)
    - py-2 → padding-top: 0.5rem; padding-bottom: 0.5rem; (8px)
    - bg-blue-500 → background-color: #3b82f6; (màu nền xanh dương)
    - text-white → color: #ffffff; (màu chữ trắng)
    - rounded-md → border-radius: 0.375rem; (6px)
    - hover:bg-blue-600 → background-color: #2563eb; (đổi sang xanh đậm hơn khi di chuột vào)
    - focus:ring-2 → box-shadow tạo thêm một vòng viền dày 2px xung quanh nút khi nhấn/tab vào
    - focus:ring-blue-300 → định nghĩa màu cho vòng viền khi focus là màu xanh nhạt (#93c5fd)
#### Câu A2(tuan_4_css_frameworks - bootstrap - 04_utilities - 3. Display, Spacing):
1. Prefix Responsive:
    - Bootstrap sử dụng Breakpoint Infixes để điều khiển layout theo nguyên tắc Mobile-first:
        - md: ($\ge 768px$): Dùng cho thiết bị Tablet.
        - lg: ($\ge 992px$): Dùng cho thiết bị Laptop.
        - xl: ($\ge 1200px$): Dùng cho thiết bị màn hình lớn.
    - VD: md:grid-cols-2 lg:grid-cols-4
        - Màn hình $< 768px$: Sử dụng cấu trúc mặc định.
        - Màn hình $\ge 768px$: Áp dụng 2 cột.
        - Màn hình $\ge 992px$: Áp dụng 4 cột.
2. State Modifiers
    - Theo tài liệu Bootstrap, việc quản lý trạng thái khác với cách dùng prefix của Tailwind: Hover/Focus/Active: Được tích hợp sẵn trong các lớp component (ví dụ: .btn:hover, .form-control:focus). Đối với Utility, Bootstrap tập trung vào trạng thái tĩnh. Việc tùy biến trạng thái cho Utility thường cần can thiệp qua SASS (05_customization.md).
3. Class ẩn/hiện
    - Để ẩn trên mobile và hiện dạng flex từ tablet trở lên, bạn sử dụng bộ utility display:
```html
<div class="d-none d-md-flex">...</div>
```
### Phần C:
#### Câu C1:
- Css thuần:
```css
.card {
  width: 300px;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.card:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 20px rgba(0, 0, 0, 0.2);
}

.image-container {
  overflow: hidden;
  border-radius: 4px;
}

.image-container img {
  width: 100%;
  display: block;
  transition: transform 0.3s ease;
}

.image-container:hover img {
  transform: scale(1.1);
}

.buy-btn {
  margin-top: 15px;
  padding: 10px 20px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.buy-btn:hover {
  background-color: #2980b9;
  color: #fff;
  transform: scale(1.05);
}
```
- Chuyển đổi sang Tailwind:
```html
<div class="w-[300px] p-[15px] border border-[#ddd] rounded-[8px] shadow-[0_4px_6px_rgba(0,0,0,0.1)] transition-all duration-300 ease-in-out hover:-translate-y-2 hover:shadow-[0_12px_20px_rgba(0,0,0,0.2)]">
  <div class="overflow-hidden rounded-[4px] group">
    <img class="w-full block transition-transform duration-300 ease-in-out group-hover:scale-110" src="product.jpg" alt="Product">
  </div>
  <button class="mt-[15px] px-[20px] py-[10px] bg-[#3498db] text-white border-none rounded-[4px] cursor-pointer transition-all duration-300 ease-in-out hover:bg-[#2980b9] hover:scale-105">
    Buy Now
  </button>
</div>
```
1. HTML file size (CSS thuần vs Tailwind HTML)
    - CSS thuần: File HTML cực kỳ gọn nhẹ vì cấu trúc chỉ chứa các tên class ngắn (`class="card"`, `class="buy-btn"`).
    - Tailwind HTML: Dung lượng file HTML sẽ nặng hơn rất nhiều (thường gấp 2 đến 3 lần) do phải gánh một lượng lớn các class tiện ích dài dằng dặc nối đuôi nhau để định hình giao diện.
2. Maintainability
    - Dễ đọc: CSS thuần thắng. Khi nhìn vào file HTML của CSS thuần, cấu trúc phân cấp rất sạch sẽ và tường minh. Trong khi đó, Tailwind tạo ra những "bức tường chữ" (class soup) khiến người mới nhìn vào rất dễ hoa mắt.
    - Dễ sửa: Tailwind thắng tuyệt đối trong thực tế:
        - Với CSS thuần, khi bạn sửa `.buy-btn`, nguy cơ cao là tất cả các nút bấm khác trên toàn hệ thống sử dụng class này cũng bị đổi theo (dễ sinh lỗi dây chuyền). Hoặc khi chuyển giao dự án, bạn sẽ mất thời gian tìm xem file `.css nằm ở đâu để sửa.
        - Với Tailwind, bạn sửa trực tiếp tại chỗ trên thẻ HTML đó. Sửa phần tử nào chỉ ảnh hưởng đúng phần tử đó (được cô lập hoàn toàn), không sợ làm vỡ layout ở các trang khác.
3. Reusability:
    - CSS thuần: Tái sử dụng bằng cách gọi lại tên class (`.card`, `.buy-btn`) ở bất kỳ file HTML nào có liên kết với file CSS đó.
    - Tailwind CSS: Có hai cách chính để tái sử dụng:
        - Tái sử dụng cấp Component: Cắt đoạn HTML đó ra thành một Component riêng biệt (React, Vue, Blade component) rồi gọi lại `<ProductCard />`.
        - Dùng `@apply` trong file CSS: Bạn gom các utility classes lại thành một class tùy chỉnh trong file CSS cấu hình:

```css
.custom-card {
  @apply w-[300px] p-[15px] border border-[#ddd] rounded-[8px] shadow-sm transition-all duration-300;
}
```

#### Câu C2:
1. Tailwind CSS file cuối cùng NHỎ HƠN Bootstrap CSS vì:
    - Bootstrap (Component-driven): File CSS chứa sẵn toàn bộ mã nguồn của mọi component (`.modal`, `.carousel`, `.btn`,...). Dù dự án chỉ dùng một vài class, trình duyệt vẫn phải tải về toàn bộ file CSS mặc định nặng khoảng 150KB+.
    - Tailwind CSS (Utility-first): Thay vì tăng tiến tuyến tính, hệ thống class của Tailwind sẽ chạm ngưỡng bão hòa (các class cơ bản như `flex`, `pt-4` được tái sử dụng liên tục ở nhiều trang). File CSS production cuối cùng cực kỳ nhẹ, thường chỉ khoảng 10KB - 50KB.
2. Giải thích Tailwind PurgeCSS
    - Cơ chế hoạt động: Trình biên dịch JIT quét toàn bộ các file code (`.html`, `.js`, `.jsx`) theo thời gian thực. Bạn gõ class nào trong HTML, JIT mới sinh ra thuộc tính CSS tương ứng cho class đó.
    - Nó loại bỏ gì? Loại bỏ tất cả các class không được sử dụng trong mã nguồn. Hàng vạn class tiện ích dư thừa về màu sắc, kích thước mặc định của thư viện sẽ bị xóa bỏ hoàn toàn khỏi file CSS cuối cùng.
3. KHÔNG nên dùng TailwindCSS khi:
    - Tình huống 1: Nội dung động từ trình soạn thảo (User-Generated Content). Khi làm trang tin tức, blog sử dụng WordPress hoặc CKEditor. Văn bản thô sinh ra từ DB (thẻ `<h2>`, `<p>)` không thể chèn class Tailwind trực tiếp, trong khi Tailwind mặc định lại reset sạch style của các thẻ này.\
    - Tình huống 2: Xây dựng thư viện UI Component đóng gói (npm package). Khi viết một bộ widget độc lập để chia sẻ giữa nhiều dự án khác nhau (có dự án dùng Bootstrap, có dự án dùng CSS thuần). Dùng Tailwind ở lõi sẽ ép dự án tiêu thụ phải cài đặt và cấu hình build-tool đồng bộ, gây phụ thuộc phức tạp.
