## FTP

### 1. Khái niệm

**FTP** là giao thức dùng để truyền file và được xây dựng chuẩn theo tiêu chuẩn TCP. 
 
FTP sử dụng 2 cổng gồm: 
- Cổng 20 để truyền dữ liệu (data port)
- Cổng 21 dùng để truyền câu lệnh (command port) 

Hoạt động theo mô hình Server-Client.

### 2. Mô hình hoạt động

<img src="http://i.imgur.com/M0DK4I4.png" />

Như đã nói ở trên, FTP hoạt động theo mô hình Client-Server.

#### a. Các kênh hoạt động trong FTP

Mặc dù giao thức này sử dụng kết nối TCP, nhưng nó không chỉ dùng một kênh TCP như phần lớn các giao thức truyền thông khác. Mô hình FTP chia quá trình truyền thông giữa bộ phận Server với bộ phận client ra làm hai kênh logic:
- Kênh Điều khiển: Nó dùng để giao tiếp TCP giữa client với Server 
- Kênh Dữ liệu: Kênh này để client và server có thể trao đổi, truyền dữ liệu cho nhau. Khi dữ liệu được truyền xong, kênh này sẽ bị ngắt

#### b. Các tiến trình

<img src="http://www.rhyshaden.com/images/ftp1.gif" />

Do các chức năng điều khiển và dữ liệu sử dụng các kênh khác nhau, nên mô hình hoạt động của FTP cũng chia phần mềm trên mỗi thiết bị ra làm hai thành phần logic tương ứng với mỗi kênh.
- Thành phần Protocol Interpreter (PI) là thành phần quản lý kênh điều khiển, với chức năng phát và nhận lệnh.
- Thành phần Data Transfer Process (DTP) có chức năng gửi và nhận dữ liệu giữa phía client với server. 
- Ngoài ra, cung cấp cho tiến trình bên phía người dùng còn có thêm thành phần thứ ba là giao diện người dùng FTP - thành phần này không có ở phía server.

##### Trên Server


Các tiến trình phía server bao gồm hai giao thức:
- Server Protocol Interpreter (Server-PI): chịu trách nhiệm quản lý kênh điều khiển trên server. Nó lắng nghe yêu cầu kết nối hướng tới từ users trên cổng dành riêng. Khi kết nối đã được thiết lập, nó sẽ nhận lệnh từ phía User-PI, trả lời lại, và quản lý tiến trình truyền dữ liệu trên server.
- Server DataTransfer Process (Server-DTP): làm nhiệm vụ gửi hoặc nhận file từ bộ phận User-DTP. Server-DTP vừa làm nhiệm thiết lập kết nối kênh dữ liệu và lắng nghe một kết nối kênh dữ liệu từ user. Nó tương tác với server file trên hệ thống cục bộ để đọc và chép file.

##### Trên Client


- User Protocol Interpreter (User-PI): chịu trách nhiệm quản lý kênh điều khiển phía client. Nó khởi tạo phiên kết nối FTP bằng việc phát ra yêu cầu tới phía Server-PI. Khi kết nối đã được thiết lập, nó xử lý các lệnh nhận được trên giao diện người dùng, gửi chúng tới Server-PI, và nhận phản hồi trở lại. Nó cũng quản lý tiến trình User-DTP.
- User Data Transfer Process (User-DTP): là bộ phận DTP nằm ở phía người dùng, làm nhiệm vụ gửi hoặc nhận dữ liệu từ Server-DTP. User-DTP có thể thiết lập hoặc lắng nghe yêu cầu kết nối kênh dữ liệu trên server. Nó tương tác với thiết bị lưu trữ file phía client.
- User Interface: cung cấp giao diện xử lý cho người dùng. Nó cho phép sử dụng các lệnh đơn giản hướng người dùng, và cho phép người điều khiển phiên FTP theo dõi được các thông tin và kết quả xảy ra trong tiến trình.

### 3. Hoạt động của FTP

#### a. Chế độ ActiveFTP

<img src="http://i0.wp.com/vnitnews.com/wp-content/uploads/2015/11/tong-quan-ve-giao-thuc-ftp-01.png" />

Ở ActiveFTP, Client lắng nghe các kết nối dữ liệu từ Server qua cổng M, nó sẽ gửi các lệnh qua cổng M tới server cổng đang lắng nghe lệnh (21). Mặc định thì M=N, Server sẽ thiết lập kênh truyền dữ liệu qua cổng 20.

##### b. Chế độ PassiveFTP

<img src="http://i1.wp.com/vnitnews.com/wp-content/uploads/2015/11/tong-quan-ve-giao-thuc-ftp-02.png" />

Trường hợp client ở đằng sau Firewall và không cho phép các kết nối TCP, PassiveFTP được sử dụng trong trường hợp này. Khi đó, client sẽ sử dụng một kết nối điều khiển gửi một câu lệnh PASV tới server yêu cầu port truyền data của server. Sau khi nhận được Port của server, client sẽ sử dụng một cổng random để kết nối dữ liệu vào bằng cổng bất kỳ của mình đến port vừa nhận được.

