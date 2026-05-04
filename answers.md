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

**1. Tầm quan trọng của `<label for="email">` đối với Screen Reader:**
* Về mặt kỹ thuật, thuộc tính `for` trong thẻ `<label>` sẽ được liên kết chặt chẽ với thuộc tính `id` của thẻ `<input>`.
* Khi người khiếm thị sử dụng phần mềm đọc màn hình (Screen Reader) và dùng phím Tab di chuyển đến ô nhập liệu, phần mềm sẽ tự động dò tìm thẻ label được liên kết và đọc to nội dung lên (ví dụ: "Nhập Email, edit text"). 
* Nếu không có sự liên kết này, máy đọc sẽ chỉ nói chung chung là "Edit text" và người dùng hoàn toàn mù tịt, không biết phải gõ thông tin gì vào ô đó.
* *(Điểm cộng UX: Việc dùng `for` còn giúp người dùng chuột khi click vào dòng chữ của label thì con trỏ nháy sẽ tự động focus ngay vào ô input).*

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