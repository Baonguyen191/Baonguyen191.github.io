# Prompt: Refactor `index.html` sang thẻ semantic HTML5 (`index_new.html`)

Cách dùng: gửi nguyên khối prompt dưới đây cho công cụ AI (ChatGPT, Claude, Gemini...), đính kèm 2 file:

1. `index.html`: trang cần refactor
2. `css/style.css`: để AI kiểm tra CSS có phụ thuộc tên thẻ hay không

---

````text
# C – CONTEXT (Bối cảnh)
Tôi học môn Công nghệ Web. Trang `index.html` của site "BaoNguyen Press" do
tôi tự viết bằng HTML và CSS thuần. Bố cục gồm:
  - đầu trang: tên site, logo, khẩu hiệu, form tìm kiếm;
  - cột trái: menu điều hướng, hộp "Kết nối", hộp "Bài mới";
  - cột phải: ảnh lớn, dải ảnh nhỏ, tiêu đề h1 và các đoạn giới thiệu;
  - chân trang: 4 chuyên mục và dòng bản quyền.
Mọi khối khung trang hiện đều là <div> đặt class: site-header, layout, main,
content, gallery, intro, sidebar, nav, box, box-connect, box-posts,
site-footer. Trang chưa có landmark semantic nên công cụ tìm kiếm và trình
đọc màn hình không phân biệt được đâu là đầu trang, điều hướng, nội dung
chính, nội dung phụ, chân trang.

File `css/style.css` dùng chung cho mọi trang của site. KHÔNG được sửa nó.

Mục tiêu: tạo file mới `index_new.html` dùng thẻ semantic HTML5 để cải thiện
SEO cơ bản. Mở trên trình duyệt, `index_new.html` phải GIỐNG HỆT `index.html`
từng pixel, ở cả màn hình máy tính lẫn điện thoại: cùng bố cục, cùng nội dung.

# R – ROLE (Vai trò)
Bạn là front-end developer nắm vững chuẩn HTML5 của WHATWG (sectioning
content, landmark, content model), CSS selector, style mặc định của trình
duyệt (user agent stylesheet) và SEO on-page cơ bản.
Nguyên tắc làm việc: thay đổi ít nhất, không làm vỡ giao diện.

# A – ACTION (Hành động)
Thực hiện tuần tự 5 bước.

BƯỚC 1 – Phân tích CSS
Đọc `css/style.css` và trả lời hai câu hỏi:
  (1) Có selector nào chứa TÊN THẺ của khối sắp đổi không (ví dụ
      `div.gallery`, `.sidebar > div`)? Nếu có, khối đó phải giữ nguyên thẻ.
  (2) Thẻ semantic định đổi sang có style mặc định nào của trình duyệt khác
      <div> không? Ví dụ <figure> mặc định có margin 1em 40px. CSS hiện tại
      đã ghi đè style đó chưa? Nếu chưa thì KHÔNG dùng thẻ đó.

BƯỚC 2 – Lập bảng ánh xạ
Với từng khối <div>, chọn một cách:
  (a) Đổi sang thẻ semantic, GIỮ NGUYÊN class;
  (b) Giữ <div> vì CSS phụ thuộc tên thẻ hoặc style mặc định, đặt thẻ
      semantic bọc bên trong;
  (c) Giữ <div> vì khối chỉ dùng để dàn trang, không mang nghĩa.
Gợi ý (phải đối chiếu kết quả BƯỚC 1 trước khi áp dụng):
  - .site-header           -> <header>
  - form tìm kiếm          -> thêm role="search"
  - .main                  -> <main>
  - .gallery               -> <figure> (chỉ khi CSS đã đặt margin cho .gallery)
  - .intro                 -> <article>
  - .nav                   -> <nav aria-label="Điều hướng chính">
  - .box-connect, .box-posts -> <aside>, đặt tên bằng aria-labelledby trỏ tới
    id của tiêu đề h2 trong hộp
  - mỗi bài trong "Bài mới" -> bọc nội dung <li> bằng <article>
  - ngày đăng              -> <time datetime="YYYY-MM-DD">, giữ nguyên class
  - .site-footer           -> <footer>
  - .page, .layout, .sidebar -> giữ <div> (.sidebar dùng display: contents
    trên màn hình nhỏ)

BƯỚC 3 – Bổ sung SEO cơ bản (chỉ những thứ KHÔNG hiển thị)
  - Thêm <meta name="description"> tiếng Việt, 120–160 ký tự, đúng nội dung
    trang.
  - Được thêm id cho tiêu đề h2 để aria-labelledby trỏ tới.
  - Giữ nguyên lang="vi", title, viewport và thuộc tính alt đang có (alt đã
    mô tả đúng ảnh).

BƯỚC 4 – Viết `index_new.html`
Ràng buộc BẮT BUỘC:
  1. KHÔNG sửa `css/style.css`, KHÔNG thêm <style> hay thuộc tính style.
  2. GIỮ NGUYÊN mọi class, href, src, width, height, alt, name, value,
     action, method, placeholder, aria-label đang có.
  3. GIỮ NGUYÊN 100% văn bản hiển thị, thứ tự khối, số ảnh, số liên kết.
     Không thêm, bớt, dịch hay sửa chính tả nội dung.
  4. GIỮ NGUYÊN cấp tiêu đề: h1 (nội dung chính), h2 (hộp sidebar), h3
     (bài mới, chuyên mục chân trang).
  5. Chỉ một <main> và một <h1>. Không đặt <main> trong <aside>, <nav>,
     <header> hay <footer>.
  6. Mỗi landmark cùng loại (nhiều <aside>) phải có tên riêng.
  7. Giữ thụt lề bằng tab như file gốc.

BƯỚC 5 – Tự kiểm tra
  - Mỗi khối đã đổi thẻ: nêu selector CSS đang áp dụng và xác nhận vẫn khớp.
  - Mỗi thẻ semantic mới: nêu style mặc định của trình duyệt và xác nhận CSS
    đã ghi đè, hoặc style đó không làm thay đổi hiển thị.
  - So văn bản hiển thị của hai file: phải trùng khớp tuyệt đối.
  - Kiểm tra lồng thẻ đúng content model HTML5.

# F – FORMAT (Định dạng đầu ra)
Trả lời theo đúng 4 phần:

PHẦN 1 – KẾT QUẢ PHÂN TÍCH CSS
Trả lời hai câu hỏi ở BƯỚC 1.

PHẦN 2 – BẢNG ÁNH XẠ
| # | Khối (class) | Thẻ cũ | Thẻ mới | Cách làm (a/b/c) | Lý do ngữ nghĩa / SEO |

PHẦN 3 – FILE HOÀN CHỈNH
Toàn bộ `index_new.html` trong một khối mã.

PHẦN 4 – CHECKLIST
Ràng buộc 1–7 ở BƯỚC 4: mỗi mục ghi "Đạt" kèm một câu giải thích.

# T – TONE (Giọng văn)
Tiếng Việt, ngắn gọn, chính xác. Giữ nguyên thuật ngữ tiếng Anh (semantic,
landmark, selector, user agent stylesheet, content model). Không lời khen,
không mở đầu, không kết luận thừa.
````

---

## Kiểm chứng kết quả AI trả về

1. **Giao diện giống hệt:** chụp màn hình `index.html` và `index_new.html` cùng kích thước, ở cả bề rộng máy tính (1240px) và điện thoại, rồi so sánh từng pixel. Có thể dùng tính năng chụp toàn trang của Chrome DevTools (Ctrl+Shift+P, gõ "Capture full size screenshot").
2. **HTML hợp lệ:** kiểm tra `index_new.html` bằng https://validator.w3.org/.
3. **Landmark:** mở Chrome DevTools, tab Elements, bảng Accessibility. Cây phải có `banner`, `search`, `main`, `navigation`, hai `complementary` có tên riêng, và `contentinfo`.
4. **SEO:** chạy Lighthouse (mục SEO và Accessibility) cho cả hai file rồi so điểm.
