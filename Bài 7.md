## 1. Phân quyền trong linux :
### 1.1 Khái niệm :
- Trong Linux, khi nói đến phân quyền là chúng ta sẽ nghĩ ngay đến 3 quyền hạn cơ bản của một user/group nào đó trên một file/folder nào đó bao gồm :
  - **r** (read) - quyền đọc file/folder
  - **w** (write) - quyền ghi/sửa nội dung file/folder
  - **x** (execute) - quyền thực thi (truy cập) thư mục. Đối với thư mục thì bạn cần phải có quyền execute thì mới dùng lệnh cd để truy cập vào được
### 1.2 Thay đổi quyền :
- Chỉ có user có quyền root hoặc owner user của dile mới có thể thay đổi quyền của file đó.
- sử dụng lệnh `chmod` để thay đổi quyền :
```sh
 chmod <mode> file_name
  ```
trong đó "mode" có thể được viết theo 2 cách là symbolic hoặc octal.
|     | **Symbolic mode** | **Octal mode ** |
|----------------|------------------------------|----------------------|
|Mô tả | Trong cách này chúng ta có thể thêm "op",(+), bớt (-),gán (=) các quyền "permissions" (r w x) cho từng nhóm đối tượng "who" (u g o) - (owner user, group, other user) | Trong cách này mỗi quyền được thể hiện bằng một số tương ứng -:0,x:1,w:2,r:4. Quyền của mỗi nhóm đối tượng thể hiện ở tổng của các thành phần. Khi gán quyền phải gán cho cả 3 nhóm |
Cách dùng | Mode = (who) + (op) + (permissions) | Ví dụ 644 rw-r-r- ; 751 rwxr-x-x ; 775 rwxrwxr-x |
 Ví dụ | chmod g-w notice.txt Bỏ quyền write trên group | chmod 66 notice.txt,6 = rw- có nghĩa là owner user có quyền đọc ghi file, 4 = r-- nghĩa là group chỉ có quyền đọc file, 4 = r-- nghĩa là other user cũng chỉ có quyền đọc file |
  Ghi chú | Ưu điểm là chúng ta có thể kế thừa quyền cũ | Cách này không thể kế thừa quyền cũ nhưng bù lại cú pháp ngắn gọn dễ dùng |
  ----
### 1.3 Cách xem phân quyền của một file : 
- Trong Linux, cách đơn giản nhất để xem phân quyền của một file là sử dụng lệnh `ls -l` Output của câu lệnh trên sẽ có dạng như sau : `-rwxr-x-r-x 1 user group`
  - Kí tự `-` đầu tiên để chỉ loại file, `-` với file thông thường, `d` với thư mục, `c` với thiết bị, `l` với liên kết (liên kết tới một file khác).
  - 3 kí tự rwx đầu tiên là quyền hạn của **Owner**, ở đây Owner sẽ có mọi quyền với file.
  - 3 kí tự r-x ở giữa là quyền hạn của **Group**, ở đây Group sẽ có quyền đọc và quyền dùng lệnh `cd`
  - 3 kí tự r-x cuối cùng là quyền hạn của **Other**, tương tự như Group ở trên sẽ có quyền đọc và dùng lệnh `cd`
  - Số nguyên đi sau quyền hạn để chỉ số lượng liên kết tới file, ở đây `1` có nghĩa là file này không có liên kết tượng trưng mà củ có một liên kết cứng duy nhất trỏ tới chính nó.
  - Cuối cùng là 2 thông tin nói về chủ sở hữu và nhóm sở hữu, ở đây là người dùng `user` và nhóm `group`

## 2. Cài package trên Centos :
### 2.1 Cài đặt bằng lệnh yum :
- Lệnh cài đặt EPEL Repository bằng YUM : `yum install epel-release`
- cài đặt từ lênh `yum` có 2 dạng : yum từ internet và yum từ local hoặc dvd. 
  - Đối với yum từ internet đòi hỏi máy chủ phải kết nối internet và thực hành lệnh : `yum -y install httpd`
  - nếu yum từ dvd thì trước hết phải cấu hình đường dẫn để yum. Dùng lệnh mount để mount đĩa dvd `mount /dev/cdrom/media/` - sau đó tạo tập tin dvd.repo trong đường dẫn **"/etc/yum.repos.d"** có nội dung như sau
**[dvd]
name=Local Repository
baseurl=file:///media
gpgcheck=0
enabled=1**
kế tiếp dùng lệnh `yum -y install httpd` như trên để cài.
### 2.2 Cài đặt phần mềm từ RPM
- Các phiên bản Red Hat như CentOS có gói cài đặt chuyên biệt là các file .rpm (RedHat Packet Manager)
- Cấu trúc file RPM như sau :
<tên gói>-<phiên bản>-<bản phân phối>.<nhóm linux>.<linux distro>.<kiến trúc>.rpm
- một số tham số với lệnh rpm :
**-i**  <gói> _cài đặt,_  
**-e**  <tên phần mềm> _gỡ bỏ (erase),_  
**-U**  <gói> _cập nhật gói (gỡ gói cũ và cài gói mới),_  
**-q**  <tên phần mềm> _in ra tên, phiên bản, release, nếu đã được cài,_  
**-qi**  <tên phần mềm> _in ra thông tin của phần mềm nếu đã được cài_  
**-V**  <tên gói> _kiểm tra tính toàn vẹn_  
**–nodeps**  _không kiểm tra các gói phụ thuộc khi cài đặt và cập nhật cũng như gỡ bỏ_  
**–force** _cài đặt, cập nhật và bỏ cũ_  
**–import** <_PUBKEY>_ _Nhập_ GPG Key (/etc/pki/rpm-gpg/RPM-GPG-KEY-CENTOS-<version>)  
**–replacefiles** _giải quyết khi có đụng độ trong việc ghi files cho gói cài đặt_
- một số lệnh rpm cơ bản :
**rpm –ivh**: lệnh cài đặt phần mềm có phần mở rộng là rpm. Khi cài đặt bằng rpm có thể bị vấn đề gói phụ thuộc. Nếu bỏ qua gói phụ thuộc thì chỉ cần thêm tham số –nodeps  
**rpm –qa**: truy vấn tất cả các phần mềm rpm được cài đặt trong hệ thống. Nếu muốn truy vấn một phần mềm cụ thể nào đó có cài đặt trong hệ thống hay không thì dùng lệnh “rpm qa:grep tenphanmem” với a là all (tất cả), q là query (truy vấn)  
**rpm –qf**: Nếu có một danh sách tập tin, muốn biết tập tin đó thuộc phần mềm rpm nào thì dùng lệnh “rpm –qf duongdantaptin”.
**rpm -qi**: xem thông tin phần mềm rpm đã được cài đặt
**rpm -qip** : xem thông tin phần mềm chưa được cài đặt, vừa mới tải về
**rpm -qlp** : liệt kê nội dung của gói phần mềm xem có những gì
**rpm –qRp**: kiểm tra các gói phụ thuộc của gói phần mềm cần cài đặt
**rpm –Uvh**: Khi thực hiện lệnh này, hệ thống kiểm tra xem phần mềm có được cài đặt hay chưa. Nếu chưa cài đặt thì hệ thống sẽ cài, còn nếu đã cài đặt rồi thì kiểm tra xem đã cũ chưa, nếu cũ thì cập nhật mới.  
**rpm –qc**: xem các tập tin cấu hình của phầm mềm. Ví dụ muốn xem các tập tin cấu hình của httpd thi dùng lệnh “rpm –qc httpd”
**rpm –qd**: xem các tập tin hướng dẫn của phần mềm.
