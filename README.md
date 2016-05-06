## FTP

#### 1. Khái niệm

**FTP** là giao thức dùng để truyền file và được xây dựng chuẩn theo tiêu chuẩn TCP.  FTP sử dụng 2 cổng gồm: cổng 20 để truyền dữ liệu (data port) và cổng 21 dùng để truyền câu lệnh (command port).

#### 2. Hoạt động của FTP

##### a. Chế độ ActiveFTP

<img src="http://i0.wp.com/vnitnews.com/wp-content/uploads/2015/11/tong-quan-ve-giao-thuc-ftp-01.png" />

Ở ActiveFTP, Client lắng nghe các kết nối dữ liệu từ Server qua cổng M, nó sẽ gửi các lệnh qua cổng M tới server từ cổng mà nó đang lắng nghe (21). Mặc định thì M=N, Server sẽ thiết lập kênh truyền dữ liệu qua cổng 20.

##### b. Chế độ PassiveFTP

<img src="http://i1.wp.com/vnitnews.com/wp-content/uploads/2015/11/tong-quan-ve-giao-thuc-ftp-02.png" />

Trường hợp client ở đằng sau firewall và không cho phép các kết nối TCP, PassiveFTP được sử dụng trong trường hợp này. Khi đó, client sẽ sử dụng một kết nối điều khiển gửi một câu lệnh PASV tới server yêu cầu port truyền data của server. Sau khi nhận được Port của server, client sẽ sử dụng một cổng random để kết nối dữ liệu vào bằng cổng bất kỳ của mình đến port vừa nhận được.