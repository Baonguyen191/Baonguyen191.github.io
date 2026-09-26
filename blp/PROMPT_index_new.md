# Prompt: Refactor `index.html` sang thẻ semantic HTML5 (`index_new.html`)

Cách dùng: gửi nguyên khối prompt dưới đây cho công cụ AI (ChatGPT, Claude, Gemini...), kèm 2 file đính kèm:

1. `index.html` (trang cần refactor)
2. `css/style.css` (để AI biết selector nào phụ thuộc tên thẻ)

---

````text
# C – CONTEXT (Bối cảnh)
Tôi học môn Công nghệ Web. Tôi có trang `index.html` dựng từ template
"Blakletterpress" (freewebsitetemplates.com). Toàn bộ khung trang dùng <div>
với id/class: #page, #header, #motto, #logo, #searchbar, #contents, #main,
#gallery, .body, #sidebar, #navigation, .section, #connect, #posts, #footer,
#featured, #footnote. Trang không có thẻ semantic nào nên công cụ tìm kiếm
và trình đọc màn hình không phân biệt được đâu là đầu trang, điều hướng,
nội dung chính, nội dung phụ, chân trang.

File `css/style.css` dùng chung cho mọi trang (about, news, blog...).
Tôi KHÔNG được sửa file CSS này.

Mục tiêu: tạo file mới `index_new.html` dùng thẻ semantic HTML5 để cải thiện
SEO cơ bản. Khi mở trên trình duyệt, `index_new.html` phải trông GIỐNG HỆT
`index.html` từng pixel: cùng bố cục, cùng nội dung hiển thị.

# R – ROLE (Vai trò)
Bạn là front-end developer nắm vững chuẩn HTML5 của WHATWG, các thẻ
sectioning (header, nav, main, article, section, aside, footer, figure),
cơ chế CSS selector và độ ưu tiên (specificity), cùng SEO on-page cơ bản.
Bạn sửa mã theo nguyên tắc: thay đổi ít nhất, không làm vỡ giao diện.

# A – ACTION (Hành động)
Thực hiện tuần tự 5 bước.

BƯỚC 1 – Phân tích CSS
Đọc `css/style.css`. Liệt kê MỌI selector có chứa TÊN THẺ đi kèm id/class,
ví dụ `#main div.body`, `#sidebar div.section`, `#navigation > div`,
`#gallery > div`, `#footer > div`, `#contents h3`, `#posts h5`.
Phần tử nào khớp các selector này thì KHÔNG được đổi tên thẻ, nếu không
CSS sẽ mất tác dụng và giao diện bị vỡ.

BƯỚC 2 – Lập bảng ánh xạ
Với từng khối <div> của trang, quyết định:
  (a) Đổi tên thẻ sang thẻ semantic, GIỮ NGUYÊN id và class; hoặc
  (b) Giữ <div> vì CSS phụ thuộc tên thẻ, rồi đặt thẻ semantic Ở BÊN TRONG
      (thẻ bọc mới không có id/class nên không ảnh hưởng CSS); hoặc
  (c) Giữ nguyên <div> vì khối chỉ dùng để dàn trang, không mang nghĩa.
Gợi ý ánh xạ (kiểm tra lại với kết quả BƯỚC 1 trước khi áp dụng):
  - #header              -> <header>
  - form tìm kiếm        -> thêm role="search" cho <form>
  - #main                -> <main>
  - #gallery             -> <figure> (nhóm ảnh minh hoạ)
  - div.body             -> giữ <div>, bọc nội dung bên trong bằng <article>
  - #navigation          -> <nav>
  - #connect, #posts     -> <aside> (div.section bên ngoài giữ nguyên)
  - mỗi mục tin trong #posts -> bọc nội dung <li> bằng <article>
  - #footer              -> <footer>
  - #page, #contents, #motto, #logo -> giữ <div>

BƯỚC 3 – Bổ sung SEO cơ bản (chỉ những thứ KHÔNG hiển thị trên trang)
  - <html lang="en"> vì nội dung trang là tiếng Anh.
  - <meta name="description" content="..."> mô tả trang, 120–160 ký tự.
  - Thay alt chung chung ("Img", "LOGO", "SiteName", "Text") bằng mô tả
    đúng nội dung ảnh. Ảnh chứa chữ thì alt ghi lại đúng chữ trong ảnh.
  - Liên kết không có chữ (icon mạng xã hội, icon ở footer) thêm aria-label
    mô tả đích đến.
  - Ô tìm kiếm thêm aria-label="Search".
  - Trang có nhiều <aside> nên mỗi <aside> cần tên riêng: thêm aria-label
    trùng với tiêu đề h2 của khối đó.

BƯỚC 4 – Viết `index_new.html`
Ràng buộc BẮT BUỘC:
  1. KHÔNG sửa `css/style.css`, KHÔNG thêm <style> hay thuộc tính style.
  2. GIỮ NGUYÊN mọi id, class, href, src, width, height, target, action,
     method, onBlur, onFocus.
  3. GIỮ NGUYÊN 100% văn bản hiển thị, thứ tự các khối, số lượng ảnh và
     liên kết. Không thêm, bớt, dịch hay sửa chính tả nội dung.
  4. GIỮ NGUYÊN cấp tiêu đề (h1, h2, h5). Đổi cấp tiêu đề sẽ đổi kiểu chữ
     do CSS định dạng theo tên thẻ.
  5. Chỉ một <main> và một <h1> trong trang.
  6. KHÔNG thêm <meta name="viewport">: trang có bề rộng cố định 960px,
     thêm viewport sẽ làm trang bị tràn ngang trên điện thoại.
  7. Giữ comment "Website template by freewebsitetemplates.com".
  8. Giữ thụt lề bằng tab như file gốc.

BƯỚC 5 – Tự kiểm tra
  - Với mỗi selector ở BƯỚC 1, xác nhận vẫn khớp đúng phần tử như trong
    file gốc.
  - So sánh văn bản hiển thị của hai file: phải trùng khớp tuyệt đối.
  - Kiểm tra lồng thẻ hợp lệ theo content model HTML5 (ví dụ: <li> chỉ
    nằm trong <ul>/<ol>, không đặt <main> bên trong <aside>).

# F – FORMAT (Định dạng đầu ra)
Trả lời theo đúng 4 phần:

PHẦN 1 – SELECTOR PHỤ THUỘC TÊN THẺ
Danh sách selector tìm được ở BƯỚC 1.

PHẦN 2 – BẢNG ÁNH XẠ
| # | Khối (id/class) | Thẻ cũ | Thẻ mới | Cách làm (a/b/c) | Lý do ngữ nghĩa / SEO |

PHẦN 3 – FILE HOÀN CHỈNH
Toàn bộ `index_new.html` trong một khối mã.

PHẦN 4 – CHECKLIST TỰ KIỂM TRA
Mỗi ràng buộc 1–8 ở BƯỚC 4 ghi "Đạt" kèm một câu giải thích.

# T – TONE (Giọng văn)
Tiếng Việt, ngắn gọn, chính xác. Thuật ngữ tiếng Anh (semantic, selector,
specificity, landmark, content model) giữ nguyên. Không lời khen, không mở
đầu, không kết luận thừa.
````

---

## Cách kiểm chứng kết quả AI trả về

1. **Giao diện giống hệt:** mở `index.html` và `index_new.html` cạnh nhau, hoặc chụp màn hình cả hai ở cùng kích thước rồi so sánh từng pixel.
2. **HTML hợp lệ:** kiểm tra `index_new.html` bằng https://validator.w3.org/.
3. **Landmark semantic:** Chrome DevTools, tab Elements, bảng Accessibility: cây phải có `banner`, `search`, `main`, `navigation`, `complementary`, `contentinfo`.
4. **SEO:** Chrome DevTools, tab Lighthouse, chạy mục SEO và Accessibility cho cả hai file rồi so điểm.
