## 1. Kiến trúc Linux :
- Kiến trúc của hệ điều hành linux được chia làm 4 hàng gồm :
Người dùng (User) -> Shell, ứng dụng, tiện ích -> Nhân Kernel -> Phần cứng.
### 1.1 Hạt nhân (Kernel) :
- Là trung tâm điều khiển của hệ điều hành Linux, chứa các mã nguồn điều khiển hoạt động của toàn bộ hệ thống. Hạt nhân được phát triển không ngừng, thường có 2 phiên bản mới nhất : 1 bản phát triển mới nhất và 1 bản ổn định mới nhất. Kernel được thiết kế theo module, do vậy kích thước rất nhỏ. Kernel chỉ tải bộ phận cần thất lên bộ nhớ, các bộ phận khác được tải lên nếu có nhu cầu sử dụng. Nhờ vậy, so với các hệ điều hành khác, Linux không sử dụng lãng phí bộ nhớ.
- Kernel được xem là trái tim của hệ điều hành Linux, ban đầu được phát triển cho các CPU Intel 80386. Điểm mạnh của loại của loại CPU này là khả năng quản lý bộ nhớ . Kernel của Linux có thể truy xuất tới toàn bộ tính năng phần cứng của máy. Yêu cầu của các chương trình cần rất nhiều bộ nhớ , trong khi hệ thống có ít bộ nhớ , hệ điều hành sử dụng không gian đĩa hoán đổi (swap space) để lưu trữ các dữ liệu xử lí của chương trình. Swap space cho phép ghi các trang của bộ nhớ xuất các vị trí dành sẵn trong đĩa và xem nó như phần mở rộng của vùng nhớ chính . Bên cạnh sử dụng swap space, Linux hỗ trợ đặc tính sau :

  -   Bảo vệ vùng nhớ giữa các tiến trình, điều này không cho phép một tiến trình làm tắt toàn bộ hệ thống
  -   Chỉ tải các chương trình khi có yêu cầu
### 1.2 Shell :
Shell cung cấp tập lệnh cho người dùng thao tác với kernel để thực hiện công việc. Shell đọc các lệnh từ người dùng và xử lí. Ngoài ra shell còn cung cấp một số đặc tính khác như : Chuyển hướng xuất nhập, ngôn ngữ lệnh để tạo các tập tin lệnh tương tự tập tin bat trong DOS.

Có nhiều loại shell được dùng trong Linux. Điểm quan trọng để phân biệt các shell với nhau là bộ lệnh của mỗi shell.

Shell sử dụng trong Linux là GNU Bourne Again Shell (bash). Shell này là shell phát triển từ Bourne Shell, là shell sử dụng chính trong các hệ thống Unix, với nhiều tính năng mới như : Điều khiển các tiến trình , history , tên tập tin dài…
### 1.3 Các tiện ích :
Các tiện ích được người dùng thường xuyên sử dụng. Nó dùng cho nhiều thứ như thao tác tập tin , đĩa , nén , sao lưu… Tiện ích có thể thông qua câu lệnh hoặc giao diện đồ họa. Hầu hết các tiện ích trong Linux là sản phẩm của chương trình GNU. Linux có sẵn rất nhiều tiện ích như trình biên dịch , gỡ lỗi , soạn văn bản… Tiện ích có thể được sử dụng bởi người dùng hoặc hệ thống . Một số tiện ích được xem là chuẩn trong hệ thống Linux như passwd , ls , ps , vi…
### 1.4 Ứng dụng :
Khác với tiện ích, các ứng dụng như các chương trình word , hệ quản trị cơ sở dữ liệu,…là các chương trình có độ phức tạp lớn và được nhà sản xuất viết ra.

## 2. Khái niệm về Bash, SH SHell, Terminal

### 2.1 Terminal :
- **Terminal** là một chương trình phần mềm được cài đặt sẵn trên hệ điều hành Linux cho phép người dùng có thể giao tiếp máy tính thông qua việc chạy các câu lệnh. Chình vì vậy Terminal còn được gọi là một chương trình giao diện cửa sổ dùng lệnh (command line interface).
### 2.2 Shell :
- **Shell** là chương trình giữa bạn và Linux ( hay nói chính xác hơn là giữa bạn với nhân Linux). Mỗi lệnh bạn gõ ra sẽ được Shell diễn dịch rồi chuyển tới nhân Linux. Nói một cách dễ hiểu Shell là bộ diễn dịch ngôn ngữ lệnh, ngoài ra nó còn tận dụng triệt để các trình tiện ích và chương trình ứng dụng có trên hệ thống.
### 2.3 SH :
- **SH** do Steven Bourne viết, đó là Shell nguyên thủy có mặt trên hầu hết các hệ thống Unix/Linux... Nó rất hữu dụng cho việc lập trình Shell nhưng nó không xử lý tương tác người dùng như các Shell khác.
### 2.4 Bash :
- Đây là phần mở rộng của sh, nó kế thừa những gì sh đã có và phát huy những gì sh chưa có. Nó có giao diện lập trình rất mạnh và linh hoạt, cùng với giao diện dễ dùng. Đây là shell được cài đặt mặc định trên các hệ thống Linux.
## 3. Các biến môi trường :
- Một khái niệm quan trọng trên linux đó là môi trường (_environment_) được định nghĩa qua các biến môi trường. Một số biến được đặt bởi hệ thống, số khác do bạn đặt, hoặc set bởi shell (các lệnh) hay một chương trình nào đó được load.
- Một biến môi trường có tên là một dãy chữ cái và nhận một giá trị nhất định, giá trị này có thể là số, chữ, tên file, thiết bị (_device_) hay một kiểu dữ liệu nào đó.
- **biến $PATH** Biến `PATH`cho thấy đường dẫn tới các thư mục chứa câu lệnh (_chương trình_) để chạy khi bạn gõ trên terminal, các mục cách nhau dấu “:” ví dụ /usr/local/sbin; /usr/local/bin...
- **HOME** đường dẫn tới thư mục home của người dùng hiện tại, để tiện lợi hơn bạn có thể thay bằng dấu `~` trong nhiều trường hợp.
- **TERM** (terminal)
- **DISPLAY**: số (mã) màn hình mặc định các ứng dụng đồ họa sẽ chạy trên đó.
## 4. Các tập tin : /etc/profile , /etc/bashrc , ~/.bashrc , ~/.bash_profile
- `~/.profile` là nơi đặt những thứ áp dụng cho toàn bộ phiên của bạn, chẳng hạn như các chương trình bạn muốn bắt đầu khi bạn đăng nhập (nhưng không phải là các chương trình đồ họa, chúng đi vào một tệp khác) và định nghĩa biến môi trường.
- `~/.bashrc` là nơi để đưa những thứ chỉ áp dụng để bash chính nó, chẳng hạn như bí danh và định nghĩa chức năng, tùy chọn trình báo và cài đặt nhanh. (bạn cũng có thể đặt các rằng buộc chính ở đó, nhưng đối với bash chúng thường đi vào ~/.inputrc )
- `~/.bash_profile` có thể được sử dụng thay vì `~/.profile`, nhưng nó chỉ được đọc bởi bash, không phải bởi bất kì trình báo nào khác. (điều này chủ yếu là một mối quan tâm nếu bạn muốn các tệp khởi tạo của bạn hoạt động trên nhiều máy và shell đăng nhập của bạn không bị bash trên tất cả chúng). Đây là một nơi hợp lý để bao gồm `~/.bashrc` nếu trình báo tương tác.
