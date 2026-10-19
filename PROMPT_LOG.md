# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG) 
- **Họ và tên: Trần Thanh Nam**  
- **MSSV: 125001516**  
- **Tên đề tài Website:** Landing Page quán cà phê LacHong cafe and tea
- **Công cụ AI đã sử dụng:** Claude, Gemini và GPT
 
## 1. Yêu cầu ban đầu (System/Initial Prompt)
Bạn là một Front-end Developer chuyên nghiệp. Hãy tạo cho tôi một Landing Page tĩnh cho quán cà phê tên "LacHong cafe and tea", phong cách [ấm áp, tối giản, màu nâu - kem], dành cho bài kiểm tra giữa kỳ môn Thiết kế Web.

RÀNG BUỘC BẮT BUỘC:
- Chỉ gồm 3 phần: index.html, style.css, thư mục assets/ (ảnh dùng link Unsplash hoặc placeholder, không dùng ảnh có bản quyền).
- TUYỆT ĐỐI KHÔNG tự viết JavaScript, không tạo file script.js. Chỉ được nhúng thư viện qua CDN. Riêng AOS bắt buộc có đúng 1 dòng khởi tạo AOS.init() theo hướng dẫn chính thức. Ngoài ra không có JS nào khác.
- Danh sách sản phẩm viết tĩnh bằng HTML, không dùng JS để render.

CẤU TRÚC SEMANTIC HTML5 (dùng đúng ngữ nghĩa, hạn chế <div> thừa):
- <header> chứa logo và <nav> menu (Trang chủ, Menu, Về chúng tôi, Đánh giá, Liên hệ)
- <main> chứa các <section>/<article>:
  1. Hero: tiêu đề lớn, slogan, nút CTA "Đặt bàn ngay"
  2. Menu: 6 sản phẩm dạng card (<article>) gồm ảnh (<figure>), tên, mô tả ngắn, giá
  3. Câu chuyện thương hiệu: ảnh + đoạn văn, bố cục 2 cột
  4. Đánh giá khách hàng: 3 card
  5. Giờ mở cửa & Liên hệ
- <footer> chứa địa chỉ, số điện thoại, mạng xã hội, copyright
- Có lang="vi", meta viewport, thuộc tính alt cho mọi ảnh.

CSS:
- Dùng CSS Variables trong :root cho: màu chính, màu phụ, màu nền, màu chữ, font chữ (Google Fonts), spacing (--spacing-sm/md/lg), bo góc (--radius), bóng đổ (--shadow). Toàn bộ file CSS dùng var(...), không hardcode màu lặp lại.
- Layout bằng CSS Grid (danh sách card, dùng repeat(auto-fit, minmax(250px, 1fr))) và Flexbox (header, nav, footer).
- Responsive cho mobile (<768px). Menu mobile dùng kỹ thuật checkbox hack bằng CSS thuần, không JS.
- html { scroll-behavior: smooth; }

HIỆU ỨNG:
- Animate.css (CDN): tiêu đề hero dùng animate__fadeInDown, slogan animate__fadeInUp, nút CTA animate__pulse (lặp vô hạn).
- AOS (CDN css + js): gắn data-aos cho từng section và card, dùng data-aos-delay tăng dần (100, 200, 300) để card hiện lần lượt.
- Tự viết bằng CSS: :hover và :focus cho nút (đổi màu, nhấc lên bằng transform, transition) và cho card (phóng nhẹ + đổ bóng). Thêm :focus-visible rõ ràng.

YÊU CẦU ĐẦU RA:
- Code sạch, có comment tiếng Việt ngắn gọn cho từng khối.
- Xuất đầy đủ nội dung index.html và style.css, nội dung tiếng Việt tự nhiên.

### Kết quả và nhận xét sau lần dựng ban đầu

- **Prompt đã dùng:** Toàn bộ yêu cầu ban đầu ở trên.
- **Kết quả AI tạo ra:** Mã nguồn `index.html`, `style.css` cho landing page với hero, 6 sản phẩm, câu chuyện thương hiệu, 3 đánh giá, giờ mở cửa, biểu mẫu liên hệ và footer. Trang sử dụng CSS Variables, Grid/Flexbox, menu mobile bằng checkbox, Animate.css và AOS qua CDN.
- **Nhận xét & Tinh chỉnh của SV:** Tôi không chỉ dựa vào lời AI khẳng định đã đáp ứng đề. Tôi tiếp tục yêu cầu rà soát riêng cấu trúc semantic, thư viện hiệu ứng và khả năng dùng bàn phím. Qua các lần rà soát, mã ban đầu còn delay card bị lặp, card chưa nhận focus bằng Tab và checkbox menu mobile bị ẩn bằng `display: none`. Các sửa đổi cụ thể được ghi bên dưới.

## 2. Quá trình tinh chỉnh & Giải quyết sự cố

### Lần 1: Rà soát Semantic HTML5

**Prompt đã dùng:**

> Rà soát index.html: chỉ ra chỗ nào đang dùng <div> mà có thể thay bằng thẻ semantic (header, nav, main, section, article, figure, footer, aside) và sửa lại. Đảm bảo có đủ 5 thẻ bắt buộc.

**Kết quả AI tạo ra:**

- Đổi `<div class="hero-content">` thành `<header class="hero-content">`, sửa cả thẻ đóng; giữ nguyên class và CSS.
- Đối chiếu đề, xác nhận đủ `<header>`, `<nav>`, `<main>`, `<section>` hoặc `<article>`, `<footer>`. Trang còn dùng `<figure>` cho ảnh.
- Kiểm tra bằng trình phân tích HTML: các thẻ đóng/mở khớp nhau, chỉ có một `<main>`.

**Nhận xét & Tinh chỉnh của SV:**

Qua rà soát, phần giới thiệu hero chứa tiêu đề và slogan vẫn dùng `div`; tôi yêu cầu AI xem lại ngữ nghĩa thay vì chỉ đếm số loại thẻ. Đổi khối này thành `header` phù hợp với vai trò giới thiệu của section. Tuy nhiên, không phải `div` nào cũng cần thay: `.menu-grid`, `.review-grid`, `.footer-content` phục vụ bố cục; `.card-body` nhóm nội dung trong article; các `div` trong `dl` nhóm cặp `dt`/`dd` hợp lệ. Tôi giữ các khối này, không ép thêm `section` hoặc `aside` chỉ để tăng số thẻ.

### Lần 2: Kiểm tra Animate.css, AOS và giới hạn JavaScript

**Prompt đã dùng:**

> Rà soát việc tích hợp Animate.css và AOS: đảm bảo CDN đúng, AOS.init() chỉ có 1 dòng, các card hiện lần lượt, hero có animate. Kiểm tra không còn JS tự viết nào.

**Kết quả AI tạo ra:**

- Kiểm tra cả ba CDN, đều trả HTTP 200:
  - `https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css`
  - `https://unpkg.com/aos@2.3.1/dist/aos.css`
  - `https://unpkg.com/aos@2.3.1/dist/aos.js`
- Giữ đúng một dòng `<script>AOS.init();</script>`, đặt sau script thư viện AOS.
- Sửa delay của 6 card menu từ `100, 200, 300, 100, 200, 300` thành `100, 200, 300, 400, 500, 600` ms. Ba card đánh giá giữ `100, 200, 300` ms.
- Xác nhận hero có `animate__animated`, `animate__fadeInDown`, `animate__fadeInUp`; nút CTA có `animate__pulse` và `animate__infinite`.
- Kiểm tra HTML không có script khác ngoài AOS và dòng khởi tạo; không có event handler inline hoặc URL `javascript:`.

**Nhận xét & Tinh chỉnh của SV:**

Lỗi thực tế là delay của card thứ 4 quay lại 100 ms, nên chưa tăng dần xuyên suốt danh sách sản phẩm. Yêu cầu kiểm tra “card hiện lần lượt” đã buộc AI sửa ba giá trị cuối thành 400, 500, 600 ms thay vì chỉ xác nhận có thuộc tính `data-aos-delay`. Phần CDN và giới hạn JavaScript vốn đã đúng nên được giữ nguyên. Tôi không ghi nhận lỗi “AI thêm JS thừa” vì lần kiểm tra này không tìm thấy lỗi đó. Kết quả mới xác minh mã nguồn và khả năng tải CDN; hiệu ứng khi cuộn vẫn cần xem trực tiếp trên trình duyệt.

### Lần 3: Bổ sung hover, focus và thao tác bàn phím

**Prompt đã dùng:**

> Thêm hiệu ứng :hover, :focus, :focus-visible cho tất cả nút, link menu và card. Dùng transition mượt, đảm bảo vẫn dùng được bằng bàn phím.

**Kết quả AI tạo ra:**

- Bổ sung các trạng thái `:focus`, `:focus-visible` còn thiếu cho nút, link menu và card; dùng outline với `currentColor` để đánh dấu focus.
- Thêm `tabindex="0"` cho card menu và card đánh giá để chúng nhận focus bằng Tab.
- Bổ sung transition cho màu nền của link; dùng thuộc tính `translate` cho hiệu ứng nhấc nút/card, tách khỏi `transform` của Animate.css/AOS. Khai báo transition của card AOS bao gồm opacity, transform, translate và bóng đổ.
- Mở rộng hiệu ứng ảnh sản phẩm sang trạng thái focus.
- Trên mobile, thay cách ẩn checkbox bằng vùng 1 px có `clip-path`, để checkbox vẫn nhận focus. Thêm dấu focus trên nhãn menu; checkbox có thể bật/tắt bằng Space.
- Dùng `visibility: hidden` khi menu đóng, `visibility: visible` khi mở để link ẩn không nằm trong thứ tự Tab.
- Kiểm tra mã: card có `tabindex`, đủ selector trạng thái theo yêu cầu, CSS có số ngoặc mở/đóng khớp nhau. Không thêm JavaScript.

**Nhận xét & Tinh chỉnh của SV:**

CSS ban đầu đã có hover nhưng card chỉ có `:focus-within`, trong khi card chưa có phần tử nhận focus. Vì vậy, viết selector thôi chưa đủ để người dùng bàn phím tiếp cận card. Yêu cầu “vẫn dùng được bằng bàn phím” dẫn đến việc bổ sung `tabindex="0"` và focus rõ ràng. Một vấn đề khác là checkbox menu mobile dùng `display: none`, khiến người dùng không thể Tab tới để mở menu; cách ẩn mới giữ được khả năng focus. Menu đóng cũng cần loại link ẩn khỏi thứ tự Tab, không chỉ thu chiều cao về 0.

Tôi giữ ràng buộc không viết JavaScript cho tương tác này. Card chỉ nhận focus để đọc và hiển thị hiệu ứng, không bị gán vai trò nút khi không có hành động. Việc đổi sang `translate` nhằm tránh dùng chung `transform` với thư viện animation. Các kiểm tra đã thực hiện là kiểm tra mã, chưa chứng minh toàn bộ trải nghiệm thực tế: cần thử Tab, Shift+Tab, Space trên mobile, Enter trên link/nút và xem hiệu ứng cuộn trước khi nộp.

## 3. Đánh giá cá nhân về quá trình Vibe Coding

### AI đã hỗ trợ ở phần nào?

AI hỗ trợ dựng cấu trúc trang, viết CSS bố cục, gắn thư viện hiệu ứng và rà soát các đoạn lặp như danh sách card. Tôi dùng các lượt yêu cầu riêng để kiểm tra từng nhóm tiêu chí, thay vì chấp nhận ngay bản đầu tiên.

### Bài học khi đặt prompt

- Nêu ràng buộc kiểm tra được: “chỉ một dòng `AOS.init();`”, “không JS tự viết”, “đủ 5 thành phần semantic”, “vẫn dùng được bằng bàn phím”.
- Yêu cầu AI chỉ rõ vị trí chưa phù hợp rồi sửa. Trường hợp delay lặp và checkbox bị `display: none` cho thấy trang có hiệu ứng chưa có nghĩa là đã đúng yêu cầu.
- Giữ phần mã đang đúng. Không thay mọi `div` bằng thẻ semantic, không thêm thư viện hoặc JavaScript cho việc CSS đã làm được.
- Phân biệt kiểm tra mã với kiểm thử trình duyệt. HTTP 200 xác nhận CDN truy cập được tại thời điểm kiểm tra; selector và thuộc tính đúng chưa đủ để khẳng định giao diện, animation và bàn phím hoạt động hoàn toàn như mong muốn.
