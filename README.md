# Hướng dẫn sử dụng công cụ tạo Trealet

Project sử dụng framework Vuejs, yêu cầu cần có Nodejs để chạy code Javascript và NPM để quản lý và cài đặt các thư viện của Nodejs, bao gồm cả framework Vuejs.

# Hướng dẫn cài đặt

## Nodejs

### Kiểm tra version Nodejs hiện tại tại terminal:
```
node -v
```
Nếu thiết bị hiện tại đã cài đặt Nodejs, hãy bỏ qua bước này và đến bước tiếp theo

### Cài đặt Nodejs:
- Đối với Windows: Download trực tiếp Nodejs bản LTS từ link https://nodejs.org/en/#home-downloadhead
- Đối với Debian và Ubuntu:
```
# Với tài khoản root
curl -fsSL https://rpm.nodesource.com/setup_lts.x | bash -

# Không có quyền root
curl -fsSL https://rpm.nodesource.com/setup_lts.x | sudo bash -
```

## NPM

### Kiểm tra version NPM hiện tại tại terminal:
```
npm -v
```
Nếu thiết bị hiện tại đã cài đặt NPM, hãy bỏ qua bước này và đến bước tiếp theo.

### Cài đặt NPM tại terminal:
```
npm install -g npm
```

# Hướng dẫn chạy chương trình

## Cài đặt thư viện
Sử dụng lệnh dưới đây tại terminal để cài đặt các thư viện cần thiết cho chương trình. Sau khi cài đặt xong, tại thư mục gốc của chương trình sẽ sinh ra một folder mới tên node_modules, chứa file chạy của các thư viện nói trên.
```
npm install
```

## Chạy chương trình
Chạy lệnh dưới đây tại terminal để bắt đầu chạy chương trình. 
```
npm run serve
```
Sau khi hoàn thành, terminal sẽ thông báo: 
```
DONE - Compiled successfully in xxxx ms
App running at:
- Local:   http://localhost:8080/ 
- Network: http://192.168.11.20:8080/
```
Truy cập 1 trong 2 đường link trên để bắt đầu sử dụng chương trình.

# Hướng dẫn sử dụng chương trình

## Cấu trúc streamline

Streamline bao gồm 1 grid và các slide con. 
Grid chung sẽ chứa hình ảnh và thông tin bao quát của các nội dung nhỏ để người dùng có thể chọn nội dung mình muốn xem.
Sau khi click để lựa chọn nội dung mình muốn xem, người dùng sẽ được dẫn sang trang slide của nội dung tương ứng. 

## Cấu trúc file trealet

Dựa trên cấu trúc streamline, file trealet gồm thông tin cho grid và thông tin của các slide con. Các thông tin của slide con này nằm trong trường ```items``` của thông tin grid.
Với mỗi grid hoặc slide, người tạo trealet có thể chỉnh sửa:
- Tên nội dung. VD: Hội họa Phục hưng
- Tác giả. VD: Nhóm 03
- Giới thiệu
- Danh sách nội dung con.

## Tạo file trealet
- Sửa tên file: Chỉnh sửa trường ```File Name``` để cố định tên file sẽ xuất ra. File sau khi xuất sẽ có dạng <tên_file>.trealet
- Sửa tên grid: Chỉnh sửa trường ```Title``` để cố định tên grid chung. Tên của grid trên streamline sẽ mang giá trị này
- Sửa tác giả: Chỉnh sửa trường ```Author``` để cố định tên tác giả trên grid chung. 
- Sửa giới thiệu grid: Chỉnh sửa trường ```Description``` để cố định giới thiệu grid.
- Sửa tên file trealet dẫn sang quiz: Chỉnh sửa trường ```Quiz file name```.

Tại List of Slides, người tạo trealet có thể thêm slide (qua nút Add Slide bên phải bảng), sửa slide cũ (qua nút cây bút ở cột Actions), xóa slide (qua nút thùng rác ở cột Actions) và chỉnh sửa nội dung các ảnh cần được trình chiếu trong slide qua List of pictures (danh sách được hiển thị khi ấn vào nút mũi tên quay xuống ở cột bên phải cùng của bảng)
- Thêm slide: Ấn nút Add Slide để hiển thị modal thêm mới slide. Tại đây có các trường Slide name, Id of slide's photo, Description, tương ứng dùng để chỉnh sửa tên của slide, hình ảnh đại diện (thumbnail) của slide sẽ hiển thị tại grid và giới thiệu của slide. Tại streamline, di chuột vào ảnh của 1 ô trên grid sẽ hiển thị tên và giới thiệu của slide tương ứng. Người dùng nhấn nút Save để lưu lại slide này, hoặc Cancel để dừng việc thêm mới
- Sửa slide: Ấn nút cây bút tại cột Actions để sửa slide tương ứng. Tương tự với thêm Slide, người dùng có thể sửa các trường trong modal hiện lên, ấn Save để lưu thay đổi.
- Xóa slide: Ấn nút thùng rác tại cột Actions để hiện lên modal xác nhận. Đồng ý xóa slide hiện tại với nút Confirm và không đồng ý với nút Cancel.
- Chỉnh sửa danh sách ảnh trình chiếu tại slide: Ấn vào nút mũi tên quay ngược xuống tại cột cuối cùng của bảng để sửa danh sách ảnh của slide tương ứng. Tại đây, người dùng điền danh sách ID của các ảnh, mỗi ID cách nhau bởi 1 dấu phẩy. 
VD: 11274,11242,16194

Người dùng có thể chỉnh sửa số lượng slide hiện lên trên 1 bảng ở trường ```Rows per page``` tại cuối bảng, và nếu số lượng slide hiện tại đã vượt quá số lượng slide trên 1 trang, người dùng có thể ấn 2 mũi tên trái phải ở cuối bảng để lật trang.

- Xuất file: Ấn nút Export ở cuối trang để xuất file.