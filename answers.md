### Câu A1 — Input Types

1. `type="email"` → Ô nhập text cơ bản, hiển thị bàn phím có nút @ trên mobile → Tự kiểm tra xem chuỗi nhập vào có ký tự @ và đúng định dạng tên miền không → Dùng cho form đăng ký tài khoản hoặc nhập email để nhận hóa đơn.
2. `type="password"` → Ô nhập text nhưng các ký tự bị che khuất (biến thành dấu chấm hoặc dấu sao) → Không có validation đặc biệt, chủ yếu để bảo mật hiển thị → Dùng để nhập mật khẩu khi đăng nhập tài khoản mua hàng.
3. `type="number"` → Ô text kèm hai nút mũi tên tăng/giảm ở góc, trên mobile hiện bàn phím số → Tự động chặn nhập chữ cái (chỉ nhận số), báo lỗi nếu số nằm ngoài khoảng min/max → Dùng để điều chỉnh số lượng sản phẩm muốn mua trong giỏ hàng.
4. `type="tel"` → Ô nhập text bình thường nhưng tự động gọi bàn phím số khi dùng trên điện thoại → Không tự động validation độ dài (thường phải dùng thêm thuộc tính pattern) → Dùng để nhập số điện thoại người nhận hàng.
5. `type="date"` → Hiển thị một bảng lịch (calendar pop-up) để click chọn ngày tháng → Ngăn người dùng nhập sai định dạng ngày tháng linh tinh → Dùng để người dùng chọn ngày mong muốn giao hàng hoặc nhập ngày sinh nhật nhận khuyến mãi.
6. `type="radio"` → Ô tròn nhỏ, trong một nhóm các tùy chọn thì chỉ được phép tick chọn duy nhất 1 ô → Đảm bảo tính độc quyền của lựa chọn (chọn cái này thì mất cái kia) → Dùng cho phần chọn Phương thức thanh toán (Thanh toán khi nhận hàng / Chuyển khoản ngân hàng).
7. `type="checkbox"` → Ô vuông nhỏ, cho phép tick chọn hoặc bỏ chọn độc lập nhiều ô cùng lúc → Chỉ trả về trạng thái bật/tắt (true/false) → Dùng cho mục tick "Tôi đồng ý với điều khoản dịch vụ" hoặc chọn bộ lọc sản phẩm (tick chọn hãng Apple, Samsung...).
8. `type="file"` → Nút bấm "Choose File" mở ra cửa sổ duyệt file của máy tính/điện thoại → Có thể tự động lọc chỉ cho phép chọn ảnh hoặc video nếu dùng thêm thuộc tính accept → Dùng để khách hàng upload ảnh thực tế khi viết đánh giá (review) sản phẩm.
9. `type="color"` → Ô vuông nhỏ hiển thị màu sắc, click vào sẽ mở ra bảng pha màu (color picker) → Bắt buộc giá trị trả về phải là một mã màu chuẩn HEX → Dùng cho tính năng cho phép khách hàng tự chọn màu sắc custom khi đặt in áo thun theo yêu cầu.
10. `type="search"` → Ô nhập text có tích hợp thêm dấu "x" nhỏ ở góc phải để xóa nhanh nội dung → Kích hoạt nút "Tìm kiếm/Kính lúp" trên bàn phím ảo của điện thoại thay vì nút Enter → Dùng làm thanh tìm kiếm sản phẩm chính ở trên cùng (header) của trang web.

### Câu A2 — Form Validation (Dự đoán và Thực tế)

Dự đoán khi user bấm Submit:

   Trường hợp 1 (required):
       *Dự đoán: Form không submit được. Trình duyệt báo lỗi yêu cầu điền dữ liệu (VD: "Please fill out this field").
       *Giải thích:* Do thẻ có thuộc tính `required` bắt buộc người dùng không được để trống ô nhập.
   Trường hợp 2 (type="email"):
       *Dự đoán: Form không submit được. Trình duyệt báo lỗi sai định dạng email (VD: "Please include an '@' in the email address").
       *Giải thích:* HTML5 tự động kiểm tra (validate) `type="email"`, yêu cầu chuỗi tối thiểu phải có ký tự `@` và một tên miền hợp lệ. Chuỗi "abc" vi phạm quy tắc này.
   Trường hợp 3 (min/max):
       *Dự đoán: Form không submit được. Trình duyệt báo lỗi giá trị nhập vào quá lớn (VD: "Value must be less than or equal to 10").
       *Giải thích: Cặp thuộc tính `min="1"` và `max="10"` giới hạn khoảng giá trị hợp lệ. Số 15 vượt quá `max="10"`.
   Trường hợp 4 (pattern):
       *Dự đoán: Form không submit được. Trình duyệt báo lỗi dữ liệu không khớp với định dạng yêu cầu (VD: "Please match the requested format").
       *Giải thích: Thuộc tính `pattern="[0-9]{10}"` sử dụng Regex bắt buộc chuỗi phải bao gồm chính xác 10 chữ số (từ 0 đến 9). Chuỗi "abc123" chứa chữ cái và quá ngắn.
   Trường hợp 5 (minlength):
       *Dự đoán: Form không submit được. Trình duyệt báo lỗi độ dài chuỗi quá ngắn (VD: "Please lengthen this text to 8 characters or more").
       *Giải thích: Thuộc tính `minlength="8"` yêu cầu mật khẩu phải có ít nhất 8 ký tự, nhưng "123" chỉ có 3 ký tự.

2. Kết quả kiểm tra thực tế:
 *(Ảnh chứng minh: `screenshots/a2_validation.jpg`)*
 *So sánh: Kết quả chạy thực tế trên trình duyệt hoàn toàn khớp 100% với các dự đoán ở trên. Khi bấm Submit, trình duyệt sẽ lập tức chặn lại và hiển thị popup cảnh báo màu đỏ ở ngay trường dữ liệu bị lỗi đầu tiên.

 ### Câu A3 — Accessibility

1. Tầm quan trọng của `<label for="email">` đối với Screen Reader:
+ Về mặt kỹ thuật, thuộc tính `for` trong thẻ `<label>` sẽ được liên kết chặt chẽ với thuộc tính `id` của thẻ `<input>`.
+ Khi người khiếm thị sử dụng phần mềm đọc màn hình (Screen Reader) và dùng phím Tab di chuyển đến ô nhập liệu, phần mềm sẽ tự động dò tìm thẻ label được liên kết và đọc to nội dung lên (ví dụ: "Nhập Email, edit text"). 
Nếu không có sự liên kết này, máy đọc sẽ chỉ nói chung chung là "Edit text" và người dùng hoàn toàn mù tịt, không biết phải gõ thông tin gì vào ô đó.
+ (Điểm cộng UX: Việc dùng `for` còn giúp người dùng chuột khi click vào dòng chữ của label thì con trỏ nháy sẽ tự động focus ngay vào ô input).

2. Sử dụng cặp thẻ `<fieldset>` và `<legend>`:
 Khi nào dùng: Cặp thẻ này được sử dụng để gom nhóm các phần tử form có liên quan logic với nhau thành một khối. Nó đặc biệt quan trọng và gần như bắt buộc khi bạn tạo một nhóm các lựa chọn `radio` hoặc `checkbox` để trả lời cho cùng một câu hỏi. `<fieldset>` đóng vai trò làm khung bao bọc, còn `<legend>` làm tiêu đề thông báo cho toàn bộ khối đó.
Ví dụ cụ thể (Nhóm lựa chọn giới tính):
```html
<fieldset>
    <legend>Vui lòng chọn giới tính:</legend>
    
    <input type="radio" id="male" name="gender" value="male">
    <label for="male">Nam</label>
    
    <input type="radio" id="female" name="gender" value="female">
    <label for="female">Nữ</label>
</fieldset>
```

### Câu A4 — Media

1. Thuộc tính `loading="lazy"` trên thẻ `<img>`:
+ Giải thích: Đây là thuộc tính ra lệnh cho trình duyệt trì hoãn việc tải hình ảnh. Ảnh sẽ không được tải ngay khi mở web, mà chỉ bắt đầu tải khi người dùng cuộn trang (scroll) đến gần vị trí của ảnh đó trên màn hình (viewport).
+ Cải thiện: Giúp tăng tốc độ tải trang ban đầu một cách đáng kể, tiết kiệm dữ liệu mạng (băng thông) cho người dùng, và giảm tải cho máy chủ (server) vì không phải tải những ảnh mà người dùng chưa chắc đã xem tới.
+ Khi nào KHÔNG nên dùng: Tuyệt đối không dùng cho những hình ảnh nằm ngay ở màn hình đầu tiên khi vừa vào web (khu vực "above-the-fold" như Logo, ảnh Banner/Hero đầu trang). Nếu dùng lazy load cho các ảnh này, nó sẽ làm chậm tốc độ hiển thị giao diện chính của trang web.

2. Thẻ `<video>` và thuộc tính `<source>`:
+ Tại sao cần nhiều `<source>`: Mỗi trình duyệt (Chrome, Safari, Firefox, Edge) sử dụng các công nghệ lõi khác nhau nên hỗ trợ các bộ giải mã (codec) video khác nhau. Việc cung cấp nhiều thẻ `<source>` giúp trình duyệt tự động đọc từ trên xuống dưới, định dạng nào nó đọc được thì nó sẽ lấy định dạng đó để phát. Điều này đảm bảo video của bạn chạy được trên mọi thiết bị mà không bị lỗi.
3 format video web phổ biến:
  1. `video/mp4` (Phổ biến nhất, tương thích hầu hết các trình duyệt).
  2. `video/webm` (Định dạng tối ưu cao cho web do Google phát triển, dung lượng nhẹ).
  3. `video/ogg` (Định dạng mã nguồn mở, hỗ trợ tốt trên Firefox).

3. Thuộc tính `alt` (Alternative Text) trên `<img>`:
+ Dùng để làm gì: Có 3 tác dụng chính: (1) Hiển thị dòng chữ thay thế trên màn hình nếu ảnh bị lỗi không tải được. (2) Đọc nội dung ảnh cho người khiếm thị nghe thông qua phần mềm Screen Reader. (3) Giúp bot của Google hiểu nội dung ảnh để SEO (lên top tìm kiếm hình ảnh).
+ Viết `alt` tốt cho 3 trường hợp:
  + Ảnh sản phẩm iPhone 16: `alt="Điện thoại iPhone 16 Pro Max màu Titan Tự nhiên, hiển thị mặt lưng và cụm 3 camera"` (Cần mô tả chi tiết hình dáng, màu sắc sản phẩm để thuyết phục khách hàng/SEO).
  + Ảnh trang trí (decorative): `alt=""` (BẮT BUỘC phải để thẻ alt rỗng. Việc này giúp phần mềm Screen Reader tự động bỏ qua bức ảnh này, tránh đọc rác tai người dùng khiếm thị bằng những thông tin không mang lại ý nghĩa nội dung).
  + Ảnh biểu đồ doanh thu Q1/2026: `alt="Biểu đồ cột cho thấy doanh thu Quý 1 năm 2026 đạt 50 tỷ đồng, tăng trưởng 20% so với cùng kỳ năm ngoái"` (Với ảnh dữ liệu, tuyệt đối không tả hình dáng biểu đồ, mà phải tóm tắt được số liệu và ý nghĩa cốt lõi mà biểu đồ muốn truyền tải).

  ### Câu A5 — So sánh `<figure>` vs `<img>`

1. Cách 1: Chỉ dùng thẻ `<img>` độc lập
+ Khi nào dùng: Dùng cho những hình ảnh thông thường, chèn trực tiếp vào luồng văn bản, hình ảnh mang tính chất trang trí, hoặc icon không cần có dòng chú thích văn bản (caption) đi kèm. Nếu bức ảnh này bị dịch chuyển đi chỗ khác hoặc ẩn đi, nó không làm hỏng cấu trúc hay thay đổi quá nhiều ý nghĩa của nội dung xung quanh.
2 ví dụ thực tế:
  1. Ảnh Avatar (ảnh đại diện) của một người dùng trong phần danh sách bình luận.
  2. Các icon nhỏ trên giao diện (như icon giỏ hàng, kính lúp tìm kiếm) hoặc ảnh Logo của website đặt trên thanh điều hướng (Header).

2. Cách 2: Dùng `<figure>` kết hợp `<figcaption>`
+ Khi nào dùng: Dùng cho những hình ảnh đóng vai trò là một "khối nội dung độc lập" quan trọng (như biểu đồ, ảnh sản phẩm, hình minh họa khoa học). Thẻ `<figure>` đóng vai trò như một cái khung gom nhóm bức ảnh và dòng chú thích lại thành một khối thống nhất. Nhờ có `<figcaption>`, Google Bot và phần mềm đọc màn hình (Screen Reader) sẽ hiểu chính xác đoạn text đó là chú thích giải nghĩa dành riêng cho bức ảnh, cực kỳ tốt cho SEO và Accessibility.
2 ví dụ thực tế:
  1. Trình bày một biểu đồ thống kê trong bài báo cáo tài chính, kèm dòng chú thích "Biểu đồ 1: Tăng trưởng doanh thu năm 2026" ở ngay bên dưới.
  2. Trình bày một khối thẻ sản phẩm (Product Card) trên web bán hàng, bao gồm ảnh chụp sản phẩm ở trên và phần chú thích là tên sản phẩm kèm giá tiền ở dưới (giống hệt code ví dụ của đề bài).

### Giải thích Bài B1 — Form Đăng ký

Tại sao HTML không thể validate "Confirm Password" (Xác nhận mật khẩu)?
Các thuộc tính Validation của HTML5 (như `pattern`, `minlength`, `maxlength`, `required`...) hoạt động độc lập và tĩnh trên từng thẻ `<input>` riêng lẻ. HTML5 chỉ có thể kiểm tra xem định dạng người dùng nhập vào có khớp với quy tắc đã thiết lập cho chính ô đó hay không. 
Nó hoàn toàn không có cơ chế động để lấy dữ liệu từ ô input `password` mang đi so sánh chéo với dữ liệu của ô input `confirm_password`. Để làm được việc "kiểm tra hai chuỗi nhập vào có giống hệt nhau không", bắt buộc phải sử dụng ngôn ngữ lập trình kịch bản là JavaScript để xử lý logic và bắt sự kiện.

### Giải Bài C1 — Debug Form

Lỗi 1: Dòng 2 – Input "Tên" không có `<label for="...">`, thiếu `id` và `name`, vi phạm accessibility và best practice.
Sửa: `<label for="name">Tên:</label> <input type="text" id="name" name="name" required>`

Lỗi 2: Dòng 1 – Thẻ `<form>` thiếu thuộc tính `action` và `method`, vi phạm best practice (trình duyệt không biết gửi dữ liệu đi đâu và bằng cách nào).
Sửa: `<form action="#" method="POST">`

Lỗi 3: Dòng 4 – Input "Email" lạm dụng `placeholder` thay cho `<label>` (người dùng screen reader sẽ không đọc được tiêu đề). Thiếu `id`, `name` và validation bắt buộc.
Sửa: `<label for="email">Email:</label> <input type="email" id="email" name="email" placeholder="Email của bạn" required>`

Lỗi 4: Dòng 6, 7 – Cặp input "Mật khẩu" không có `<label>`, thiếu `id`, `name` và không có validation độ dài tối thiểu (`minlength`).
Sửa: 
`<label for="pwd">Mật khẩu:</label> <input type="password" id="pwd" name="pwd" placeholder="Mật khẩu" required minlength="8">`
`<label for="pwd_confirm">Nhập lại mật khẩu:</label> <input type="password" id="pwd_confirm" name="pwd_confirm" placeholder="Nhập lại mật khẩu" required minlength="8">`

Lỗi 5: Dòng 9 – Input "Phone" dùng sai `type="text"` thay vì `type="tel"`. Dùng cứng thuộc tính `value` để làm chữ gợi ý thay vì dùng `placeholder`. Thiếu `<label>`, `id`, `name`.
Sửa: `<label for="phone">Phone:</label> <input type="tel" id="phone" name="phone" placeholder="0901234567" pattern="[0-9]{10}">`

Lỗi 6: Dòng 11 – Thẻ `<select>` không có `<label for="...">` đi kèm, thiếu `id` để liên kết với label và thiếu `name` để gửi dữ liệu.
Sửa: `<label for="city">Thành phố:</label> <select id="city" name="city">`

Lỗi 7: Dòng 12, 13 – Các thẻ `<option>` bên trong dropdown bị thiếu thuộc tính `value`, vi phạm best practice (cần chuẩn hóa dữ liệu gửi lên server thay vì gửi text tiếng Việt có dấu).
Sửa: 
`<option value="hn">Hà Nội</option>`
`<option value="hcm">TP.HCM</option>`

Lỗi 8: Dòng 16 đến 18 – Phần "Tôi đồng ý điều khoản" có `<label>` nhưng lại thiếu mất thẻ `<input type="checkbox">` để người dùng thực sự tick vào.
Sửa: `<input type="checkbox" id="terms" name="terms" required> <label for="terms">Tôi đồng ý điều khoản</label>`

### Giải bài C2

1. Pattern regex cho CMND/CCCD và Số tài khoản:
+ CMND/CCCD (đúng 12 chữ số): `pattern="[0-9]{12}"`
+ Số tài khoản (10-15 chữ số): `pattern="[0-9]{10,15}"`

2. HTML5 validation đủ an toàn cho ứng dụng ngân hàng chưa? Tại sao?
+ KHÔNG đủ an toàn.
+ Tại sao: HTML5 Validation chỉ hoạt động ở phía Client (trình duyệt). Bất kỳ ai cũng có thể mở Developer Tools (F12) để tự tay xóa bỏ các thuộc tính bảo vệ (`required`, `pattern`, `maxlength`...) trong mã HTML. Hơn nữa, kẻ tấn công có thể bỏ qua hoàn toàn giao diện web, dùng các công cụ như Postman để gửi trực tiếp dữ liệu độc hại thẳng lên Server.

3. 3 loại validation mà HTML5 KHÔNG THỂ làm được (phải dùng JavaScript):
1.  Kiểm tra chéo (Cross-field Validation): So sánh dữ liệu giữa 2 ô input khác nhau (VD: So sánh ô "Mật khẩu" và "Xác nhận mật khẩu" xem có khớp nhau không).
2.  Kiểm tra logic nghiệp vụ phức tạp: Kiểm tra tính hợp lệ của số thẻ tín dụng theo thuật toán Luhn, hoặc tính tuổi chính xác từ ngày sinh để xem đã đủ 18 tuổi chưa.
3.  Kiểm tra bất đồng bộ với Database (Async/API Validation): Tự động gửi API lên server để kiểm tra xem Email hoặc số CCCD này đã từng được đăng ký trong hệ thống hay chưa ngay khi người dùng vừa gõ xong.

4. 2 rủi ro bảo mật nếu chỉ validate trên Frontend mà không validate Backend:
1.  Tấn công phá hoại hệ thống (Injection): Hacker có thể gửi các đoạn mã SQL độc hại (SQL Injection) để đánh cắp, thay đổi hoặc xóa sạch cơ sở dữ liệu ngân hàng.
2.  Lỗ hổng logic nghiệp vụ (Business Logic Flaw): Hacker có thể cố tình sửa đổi dữ liệu gửi đi (VD: chuyển số tiền âm `-1.000.000đ` để tài khoản của mình được cộng tiền). Nếu Backend không kiểm tra lại và từ chối, hệ thống sẽ gặp thiệt hại nghiêm trọng.