## 1.Kernel
### 1.1 Khái niệm : 
 `Kernel` là những phần mềm, ứng dụng ở mức thấp (_low-level_) trong hệ thống, có khả năng thay đổi linh hoạt để phù hợp với phần cứng. Chúng tương tác với tất cả ứng dụng và hoạt động trong chế độ user mode, cho phép các quá trình khác – hay còn gọi là server, nhận thông tin từ các thành phần khác qua inter-process communication (IPC).
### 1.2 Các loại Kernel khác nhau :
- Về bản chất, có nhiều cách để xây dựng cấu trúc và biên dịch 1 bộ kernel nhất định từ đầu. Nhìn chung, với hầu hết các kernel hiện nay, chúng ta có thể chia ra làm 3 loại: _monolithic_, _microkernel_, và _hybrid_. Linux sử dụng kernel monolithic trong khi OS X (XNU) và Windows 7 sử dụng kernel hybrid.
- **Microkernel** : có đầy đủ tính năng cần thiết để quản lý bộ vi xử lý, bộ nhớ và IPC. Có rất nhiều thứ khác trong máy tính có thể được nhìn thấy, tiếp xúc và quản lý trong chế độ người dùng. Microkernel có tính linh hoạt khá cao, vì vậy bạn không phải lo lắng khi thay đổi 1 thiết bị nào đó, ví dụ như card màn hình, ổ cứng lưu trữ... hoặc thậm chí là cả hệ điều hành. Microkernel với những thông số liên quan footprint rất nhỏ, tương tự với bộ nhớ và dung lượng lưu trữ, chúng còn có tính bảo mật khá cao vì chỉ định rõ ràng những tiến trình nào hoạt động trong chế độ user mode, mà không được cấp quyền như trong chế độ giám sát - supervisor mode.
- **Hybrid Kernel** : Khác với 2 loại kernel trên, Hybrid có khả năng chọn lựa và quyết định những ứng dụng nào được phép chạy trong chế độ user hoặc supervisor. Thông thường, những thứ như driver và file hệ thống I/O sẽ hoạt động trong chế độ user mode trong khi IPC và các gói tín hiệu từ server được giữ lại trong chế độ supervisor. Tính năng này thực sự rất có ích vì chúng đảm bảo tính hiệu quả của hệ thống, phân phối và điều chỉnh công việc phù hợp, dễ quản lý.
### 1.3 Linux Kernel
- Linux sử dụng **Monolithic Kernel** : Có chức năng bao quát rộng hơn so với microkernel, không chỉ tham gia quản lý bộ vi xử lý, bộ nhớ, IRC, chúng còn can thiệp vào trình điều khiển driver, tính năng điều phối file hệ thống, các giao tiếp qua lại giữa server... Monolithic tốt hơn khi truy cập tới phần cứng và đa tác vụ, bởi vì nếu 1 chương trình muốn thu thập thông tin từ bộ nhớ và các tiến trình khác, chúng cần có quyền truy cập trực tiếp và không phải chờ đợi các tác vụ khác kết thúc. Nhưng đồng thời, chúng cũng là nguyên nhân gây ra sự bất ổn vì nhiều chương trình chạy trong chế độ supervisor mode hơn, chỉ cần 1 sự cố nhỏ cũng khiến cho cả hệ thống mất ổn định. 
- **Ưu điểm** :
  - Truy cập trực tiếp đến các phần cứng.
  - Dễ dàng xử lý các tín hiệu và liên lạc giữa nhiều thành phần với nhau.
  - Nếu được hỗ trợ đầy đủ, hệ thống phần cứng sẽ không cần cài đặt thêm driver cũng như phần mềm khác.
  - Quá trình xử lý và tương tác nhanh hơn vì không cần phải chờ đợi
 - **Nhược điểm** : 
   - Tiêu tốn nhiều footprint cài đặt và lưu trữ.
   - Tính bảo mật kém hơn vì tất cả đều hoạt động trong chế độ giám sát - supervisor mode.
## 2. Cấu hình ổ đĩa khi cài đặt CentOS :
### 2.1 Khi cấu hình ổ đĩa để cài đặt OS sẽ có 3 phân vùng cần thiết :
  - `/boot`: là phân vùng chứa các file boot khởi động của CentOS (bao gồm linux kernel và các tập tin sử dụng trong boot loader).
  - `/swap`: là phân vùng tương tự như Virtual RAM trên Windows. Nên để phân vùng gấp đôi RAM của máy. Nếu hệ thống bị quá tải RAM mà không có `swap` thì sẽ dẫn đến tình trạng máy bị Crash.
  - `/`: là phân vùng root của hệ thống.
### 2.2 Các phân vùng sẽ được phân chia theo các kỹ thuật:
- **Standard partion** : Hệ thống phân vùng cài đặt mẫu dành cho Linux thường có dạng như sau :
  - 12 - 20GB để cài hệ điều hành, và được gán với ký tự / `(root)`
  - 1 phân vùng nhỏ hơn được dùng để tăng thêm bộ nhớ ảo của RAM - `swap`
  - Phần còn lại dành cho việc lưu trữ dữ liệu và các thành phần khác `/home`
- **Btrfs** : Btrfs là thế hệ tiếp theo của hệ thống tập tin trên Linux, được xây dựng dựa trên hệ thống tập tin COW B-tree. Nó cải thiện không gian cũng như thời gian so với các hệ thống tập tin khác ( ext2, ext3, ext4 ... ) và tăng khả năng quản lý. Btrfs giải quyết các vấn đề còn thiếu trên các hệ thống tập tin cũ như: snapshot, checksum dữ liệu, phân vùng và mở rộng trực tiếp. Do vậy, Btrfs rất phù hợp để hoạt động với server dựa vào hiệu suất làm việc cao, khả năng tạo snapshot nhanh chóng cũng như hỗ trợ nhiều tính năng đa dạng khác.
- **LVM** : Logical Volume Manager là phương pháp cho phép ấn định không gian đĩa cứng thành những logical Volume khiến cho việc thay đổi kích thước trở nên dễ dàng hơn (so với partition). Với kỹ thuật Logical Volume Manager (LVM) bạn có thể thay đổi kích thước mà không cần phải sửa lại table của OS.
- **LVM within provisioning** : Chức năng này cho phép chúng ta cấp động dữ liệu cho người dùng.
## 3. Quá trình boot trong CentOS :
### 3.1 Power On
- BIOS là một phần mềm được cài sẵn vào chip ROM nằm trên bo mạch chủ.
- Khi nhấn nút khởi động nguồn, chương trình BIOS sẽ chạy đầu tiên. BIOS sẽ thực hiện một công việc gọi là POST nhằm kiểm tra phần cứng.
- Khi quá trình POST kết thúc thành công, BIOS sẽ tìm kiếm và khởi chạy một hệ điều hành chứa trong ổ cứng, USB…Sau đó phần còn lại của quá trình khởi động được kiểm soát bởi hệ điều hành.
### 3.2 Master Boot Record (MBR)
- Sector đầu tiên của một thiết bị lưu trữ được gọi là MBR.
- BIOS sẽ đọc MRB của thiết bị này để nạp vào bộ nhớ một chương trình rất nhỏ. Chương trình nhỏ này sẽ định vị và khởi động boot loader – đây là chương trình chịu trách nhiệm cho việc tìm và nạp nhân (kernel) của hệ điều hành.
- Đến giai đoạn này, máy tính sẽ không truy cập vào bất kì phương tiện lưu trữ nào. Các thông tin về ngày tháng, thời gian và các thiết bị ngoại vi quan trọng nhất được nạp từ CMOS.
### 3.3 Boot Loader
- Boot loader sẽ nằm trong Master Boot Record (MBR). Khi khởi động Linux, boot loader có trách nhiệm nạp kernel và Initial RAM Disk (có chứa một số tệp quan trọng và trình điều khiển thiết bị cần thiết để khởi động hệ thống) vào bộ nhớ.
- Bood loader bao gồm hai giai đoạn:
  - **Giai đoạn thứ nhất:** 
    - Đối với các hệ thống sử dụng BIOS/MBR, boot loader nằm tại sector đầu tiên của bộ nhớ hay còn gọi là Master Boot Record (MBR). Kích thước của MBR vào khoảng 512 bytes. Trong giai đoạn này boot loader kiểm tra các phân vùng để tìm ra phân vùng chứa hệ điều hành. Khi tìm thấy phân vùng khởi động, nó sẽ tìm một boot loader như là GRUB và tải nó vào RAM.
     - Đối với các hệ thống sử dụng EFI/UEFI, các firmware UEFI sẽ đọc dữ liệu Boot Manager để tìm các ứng dụng UEFI. Firmware sẽ chạy ứng dụng UEFI
- **Giai đoạn thứ hai:** Boot loader nằm trong thư mục /boot. Một màn hình hiển thị cho phép chúng ta chọn OS để khởi động. Sau đó boot loader sẽ nạp kernel của hệ điều hành đó vào bộ nhớ RAM và chuyển quyền điều khiển máy tính cho kernel này.
### 3.4 Linux kernel được nạp và khởi chạy
- Boot loader sẽ nạp hạt nhân và các file system RAM vào bộ nhớ hệ thống để kernel có thể sử dụng trực tiếp. Khi hạt nhận được nạp vào bộ nhớ RAM, nó ngay lập tức khởi tạo và cấu hình bộ nhớ máy tính hoặc tất cả các phần cứng được gắn vào.
### 3.5 Inital RAM Disk
- Các INITRD cung cấp một giải pháp: một tập các chương trình nhỏ sẽ được thực thi khi kernel vừa mới được khởi chạy. Các chương trình nhỏ này sẽ dò quét phần cứng của hệ thống và xác định xem kernel cần được hỗ trợ thêm những gì để có thể quản lý được các phần cứng đó. Chương trình INITRD có thể nạp thêm vào kernel các module bổ trợ. Khi chương trình INITRD kết thúc thì quá trình khởi động Linux sẽ tiếp diễn.
### 3.6 Các run level và service
- init là tiến trình đầu tiên chạy trong hệ thống Linux: ID của tiến trình này là 1.
- File cấu hình runlevel /etc/inittab
  -   Runlevel 0: tắt hệ thống
  -   Runlevel 1: chế độ đơn người sử dụng
  -   Runlevel 2: chế độ multi user
  -   Runlevel 3: chế độ đa người dùng không có giao diện đồ họa
  -   Runlevel 4: không sử dụng
  -   Runlevel 5: chế độ đa người dùng có giao diện đồ họa
  -   Runlevel 6: reboot hệ thống
## 4. Nơi lưu trữ các Package trong CentOS Project
- **CentOS** sử dụng `yum` để tương tác với kho hệ thống và cài đặt phụ thuộc, và cũng bao gồm một công cụ cấp thấp hơn được gọi là `rpm`, cho phép bạn tương tác với từng gói.
- **Yellow Dog Updater, Modified (YUM)** : Công cụ YUM được phát triển cho hệ thống Yellow Dog Linux như là một thay thế cho Yellow Dog Updater (yup). RedHat tìm thấy công cụ YUM là một bổ sung có giá trị cho hệ thống của họ. Ngày nay, YUM là gói mặc định và kho lưu trữ công cụ quản lý cho một số hệ điều hành.
- Để tương tác với `yum` có thể sử dụng các lệnh dưới đây :
  - **yum install package-name(s)**
  - **yum remove package-name(s)**
  - **yum search search-pattern**
  - **yum deplist package-name(s)**
  - **yum check-update**
  - **yum info package-name(s)**
  - **yum reinstall package-name(s)**
  - **yum localinstall local-rpm-file**
  - **yum update optional-package-name(s)**
  - **yum upgrade**
- **Tập tin /etc/yum.conf** : Tập tin nằm ở thư mục /etc/yum.conf cung cấp tùy chọn cấu hình hệ thống cho YUM, cũng như thông tin về kho. Thông tin kho lưu trữ cũng có thể nằm trong các tập tin kết thúc bằng .repo trong tập tin /etc/yum.repos.d
