## 1. Cấu trúc thư mục trong CentOS:
- /root : đây là nơi bắt đầu của tất cả các file và thư mục. Chỉ có root user mới có quyền ghi trong thư mục này.
- /bin : **Chương trình của người dùng**. Thư mục này chứa các chương trình thực thi. Các chương trình chung của Linux được sử dụng bởi tất cả người dùng được lưu ở đây. Ví dụ : ps, ls, ping,...
- /sbin : **Chương trình hệ thống**. Cũng giống như /bin, /sbin cũng chứa các trương trình thực thi, nhưng chúng là chương trình của admin, dành cho việc bảo trì hệ thống. Ví dụ như: reboot, fdisk, iptables,...
- /etc : **Các file cấu hình**. Thư mục này chứa các file cấu hình của các chương trình, đồng thời nó còn chứa các shell script dùng để khởi động hoặc tắt các chương trình khác. Ví dụ : /etc/logrolate.conf , /etc/resolv.conf
- /dev : **Các file thiết bị**. Các phân vùng ổ cứng, thiết bị ngoại vi như USB, ổ đĩa cắm ngoài, hay bất cứ thiết bị nào gắn kèm vào hệ thống đều được lưu ở đây. Ví dụ: */dev/sdb1* là tên của USB bạn vừa cắm vào máy, để mở được USB này bạn cần sử dụng lệnh mount với quyền root: `# mount/dev/sdb1/tmp`
- /tmp : **Các file tạm**. Thư mục này chứa các file tạm thời được tạo bởi hệ thống và các người dùng. Các file lưu trong thư mục này sẽ bị xóa khi hệ thống restart.
- /proc : **Thông tin về các tiến trình**. Thông tin về các tiến trình đang chạy sẽ được lưu trong `/proc` dưới dạng một hệ thống file thư mục mô phỏng. Ví dụ thư mục con `/proc/{pid}` chứa các thông tin về tiến trình có ID là pid (pid ~ process ID). Ngoài ra đây cũng là nơi lưu thông tin về các tài nguyên đang sử dụng của hệ thống như: /proc/version , /proc/uptime ,...
- /var : **File về biến của chương trình**. Thông tin về các biến của hệ thống được lưu trong thư mục này. Như thông tin về log file: `/var/log` , các gói và cơ sở dữ liệu `/var/lib` ,...
- /usr : **Chương trình của người dùng**. Chứa các thư viện, file thực thi, tài liệu hướng dẫn và mã nguồn mở cho chương trình chạy ở lv2 của hệ thống. Trong đó :
           + `/usr/bin` chứa các file thực thi của người dùng như: at, awk, cc, less.... Nếu bạn không tìm thấy chúng trong /bin hãy tìm trong /usr/bin.
           + `/usr/sbin` chứa các file thực thi của hệ thống dưới quyền admin như : atd, cron, sshd...Nếu bạn không tìm thấy chúng trong /sbin thì hãy tìm trong thư mục này.
           + `/usr/lib/` chứa các thư viện cho các chương trình trong /usr/bin và /usr/sbin.
           + `/usr/local` chứa các chương trình của người dùng được cài từ mã nguồn. Ví dụ như bạn cài apache từ mã nguồn, nó sẽ được lưu dưới /usr/local/apache2
- /home : **Thư mục của người dùng**. Thư mục này chứa tất cả các file cá nhân của từng người dùng. Ví dụ: /home/john, /home/marie
- /boot : **Các file khởi động**. Tất cả các file yêu cầu khi khởi động như initrd, vmlinux. grub được lưu tại đây. Ví dụ vmlixuz-2.6.32-24-generic
- /lib  **Thư viện hệ thống**. Chứa các thư viện hỗ trợ cho các file thực thi trong /bin và /sbin. Các thư viện này thường có tên bắt đầu bằng ld* hoặc lib*.so.*. Ví dụ như ld-2.11.1.so hay libncurses.so.5.7
- /opt : **Các ứng dụng phụ tùy chọn**. Tên thư mục này nghĩa là optional (tùy chọn), nó chứa các ứng dụng thêm vào từ các nhà cung cấp độc lập khác. các ứng dụng này có thể được cài ở /opt hoặc một thư mục con của /opt
- /mnt : **Thư mục để mount**. Đây là thư mục tạm để mount các file hệ thống. Ví dụ như # mount/dev/sda2/mnt
- /media : **Các thiết bị gắn có thể gỡ bỏ**. Thư mục tạm này chứa các thiết bị như CdRom /media/cdrom. Floppy /media/floopy hay các phân vùng đĩa cứng /media/Data (hiểu như là ổ D:/Data trong Windows)
- /srv : **Dữ liệu của các dịch vụ khác**. Chứa dữ liệu liên quan đến các dịch vụ máy chủ như /srv/svs, chứa các dữ liệu liên quan đến CVS.
## 2. SeLinux - vì sao thường tắt SeLinux
- **SELinux** (**Security-Enhanced Linux**) là một mô đun bảo mật ở nhân của Linux, cung cấp cơ chế hỗ trợ các chính sách bảo mật kiểm soát truy cập (access control) , bao gồm các điều khiển truy nhập bắt buộc theo Bộ Quốc phòng Hoa Kỳ (MAC).
- SELinux có 3 chế độ hoạt động cơ bản, trong đó  **Enforcing**  là chế độ mặc định khi cài đặt. Tuy nhiên, có một bộ định tính bổ sung của các mục tiêu hoặc các ml kiểm soát cách các quy tắc SELinux phổ biến được áp dụng, với mục tiêu là mức độ ít nghiêm ngặt hơn.

  +   **Enforcing**: Chế độ mặc định sẽ cho phép và thực thi chính sách bảo mật SELinux trên hệ thống, từ chối các hành động truy cập và ghi nhật ký
  +   **Permissive**: Trong chế độ Permissive, SELinux được kích hoạt nhưng sẽ không thực thi chính sách bảo mật, chỉ cảnh báo và ghi lại các hành động. Chế độ Permissive hữu ích cho việc khắc phục sự cố SELinux
  +   **Disabled**: SELinux bị vô hiệu hóa hoặc bị tắt đi.
- ### Trường hợp nào cần vô hiệu hóa SELinux:
  + Việc bảo mật trên Linux là rất cần thiết, tuy nhiên có những trường hợp nó lại gây ra sự phiền phức khi bạn muốn cài một phần mềm mà phần mềm đó lại cần can thiệp sâu vào hệ thống Linux. 
## 3.Trên máy ảo CentOS :
### 3.1 Thiết lập IP tĩnh cho card mạng : 

- sử dungj lệch `nmcli d` để xem danh sách card mạng và lệnh `ip a` để xem chi tiết địa chỉ ip của những card mạng đó.
 
![alt](https://i.imgur.com/tQCZdaQ.png)

- Hiện tại máy đang có 3 card mạng : lo(loopback),ens33,ens34. Trong đó :
  - Card ens33 đã được cấu hình nhân IP DHCP cấp : 192.168.59.131
  - Card ens34 đang disconected, chúng ta sẽ cấu hình IP static cho card này.
- thiết lập IP tĩnh cho card **ens34**, sử dụng lệnh `vi /etc/sysconfig/network-scripts/ifcfg-ens34` :

![alt](https://i.imgur.com/UxucG8Q.png)

- restart lại network để lưu cấu hình bằng lệnh : `service network restart`
- Sau khi cấu hình, xem lại trạng thái card mạng và địa chỉ ip:
![alt](https://i.imgur.com/WOM3VrH.png)

- Card ens34 đã được cấu hình IP static.
### 3.2 Cấu hình đổi port SSH
- Truy cập vào file cấu hình SSH : `vi /etc/ssh/sshd_config` và chỉnh sửa port thành 2020

![alt](https://i.imgur.com/grBeR9D.png)
- Sau đó tiến hành tắt SELinux và Firewall:
`vi /etc/selinux/config` đổi giá trị SELINUX=disabled
![alt](https://i.imgur.com/sBAzxOk.png)
`systemctl disable firewalld
systemctl stop firewalld`

![alt](https://i.imgur.com/0eHGf2k.png)

- Khởi động lại máy để cấu hình được thực thi. Việc config ssh chỉ cần khởi động lại dịch vụ ssh: `systemctl restart sshd.service` , nhưng vì cấu hình tắt SELinux nên cần khởi động lại máy , gõ lệnh : `reboot`
### 3.3 Cấu hình ssh sử dụng keypair :
- B1: Tạo Keypair.( nếu đã có ssh key rồi thì bảo qua bước này).
  - gõ lệnh: `ssh-keygen`
- B2: Copy public lên server. trên máy user:
`cat ~/.ssh/id_rsa.pub ssh root@10.55.55.113 -p 2020 "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/ssh && cat >> ~/.ssh/authorized_keys"`
- B3: tắt đăng nhập bằng password :
  - `vi /etc/ssh/sshd_config`, chỉnh **PasswordAuthentication yes** thành **PasswordAuthentication no**.
- B4: Restart dịch vụ ssh trên server centos
- gõ lệnh : `systemctl restart sshd.service`
