## 1. Các câu lệnh làm việc cơ bản trong Linux:
### 1.1 ls (List):
- lệnh `ls` để liệt kê nội dung file hoặc thư mục trong thư mục hiện hành. thường có các option
  - `-a` : xem tất cả các file và thư mục ẩn
  - `-l` : xem thông tin chi tiết bao gồm ACL (access control list), kích cỡ, ngày tháng cập nhật, chủ sở hữu,..
  - `-p` : thêm slash (`/`) để đánh dấu các thư mục
  - `-R` : xem cả cây thư mục
  ![alt](https://i.imgur.com/yCJTXsN.png)
### 1.2 mkdir (make directory)
- cú pháp `mkdir <tên thư mục mới>` để tạo một thư mục mới.
### 1.3 pwd (print working directory)
- `pwd` dùng để in ra đường dẫn đầy đủ đến thư mục hiện hành
### 1.4 cd (change directory)
- `cd <thư mục>` dùng để chuyển đến một thư mục cho phiên làm việc hiện tại.
### 1.5 rmdir (remove directory)
- `rmdir <thư mục>` để xóa một thư mục
### 1.6 rm (remove)
- `rm <tên file>` để xóa file, có thể dùng option `-r <tên thư mục>` để xóa thư mục và toàn bộ dữ liệu trong thư mục đó.
### 1.7 cp (copy)
- `cp <file nguồn> <file đích>` để sao chép file từ vị trí nguồn đến vị trí đích. có thể sử dụng option `-r` để sao chép thư mục.
### 1.8 mv (move)
- `mv <nguồn> <đích>` để di chuyển một file hoặc thư muc từ vị trí này sang vị trí khác. Lệnh này cũng dùng để đổi tên file hoặc thư mục nếu như `<nguồn>` và `<đích>` là cùng một thư mục.
### 1.9 cat (concatenate and print files)
- `cat <tên file>` để đọc và in nội dung của file ra màn hình.
### 1.10 less (print LESS)
- `less <tên file>` để in ra nội dung của một file theo từng trang trong trường hợp nội dung của file quá lớn và phải đọc theo trang. Bạn có thể dùng `Ctrl F` để chuyển trang tiếp và `Ctrl B` để chuyển về trang trước.
### 1.11 grep
- `grep <chuỗi> <tên file>` để tìm kiếm nội dung của file theo chuỗi cung cấp. Bạn có thể dùng `grep -i <chuỗi> <tên file>` để tìm kiếm không phân biệt hoa thường hoặc `grep -r <chuỗi> <tên thư mục>` để tìm kiếm trong toàn thư mục.
### 1.12 find
- `find <thư mục> -name <tên file>` để tìm kiếm file trong `<thư mục>` theo `<tên file>`.
- Cũng có thể dùng `find <thư mục> -iname <tên file>` để tìm kiếm không phân biệt hoa thường.
### 1.13 help
- `<câu lệnh> --help` để xem thông tin trợ giúp và các tùy chỉnh của câu lệnh.
### 1.14 whatis (what is the command)
- `whatis <tên câu lệnh>` để hiển thị mô tả về câu lệnh.
### 1.15 touch
- `touch <tên file.định dạng>` để tạo file kèm theo định dạng của nó.

## 2. Trình editor VIM
### 2.1 Giới thiệu và cài đặt :
- Vim là một trong những trình bien soạn dòng lệnh mạnh và phổ biến nhất. Nó chỉ sẵn có trên nền của Linux và Unix, nhưng sau đó cũng xuất hiện trên cả Windows.
- Giao diện của nó thì gọn gàng và đơn giản, và bạn có thể kết hợp các phím để thực hiện các công việc như copy-paste, tìm kiếm và thay thế, xóa một số dòng, và nhiều chức năng khác nữa.
- Ưu điểm của VIM là mọi thao tác đều có thể thực hiện thông qua các phím tắt, vì vậy bạn không cần dùng tới con chuột khi dùng VIM nữa.
- để cài đặt ta dùng lệnh `apt-get install vim`
### 2.2 Một số chức năng trong VIM
- Trong Vim chúng ta có thể edit nhiều file cùng 1 lúc bằng cách sử dụng buffers (bộ đệm) : 
  -  Chúng ta mở nhiều file để edit :
    
    ```
        vim test.sh test1.sh test2.sh
    
    ```
    - Chúng ta có thế xem buffers bằng cách : ( Insert Mode)
    
    ```
       :buffers
     1 %a   "test.sh"                      line 1
     2      "test1.sh"                     line 0
     3      "test2.sh"                     line 0
       Press ENTER or type command to continue
    
    ```
    
  - Để chuyển qua file edit tiếp theo trong buffers ta dùng :bn hoặc :b + tên file
    
    ```
    :bn Chuyển tới file edit tiếp theo trong buffers
    :b + tên file : chuyển tới file muốn edit
    
    ```
    
   - Dưới đây là một số câu lệnh để quản lí buffers:
      - : ls - Liệt kê tất cả các file giống lệnh :buffers
      - : bn - Chuyển sang file tiếp theo
      - : bp - Chuyển sang file trước đó
      - : bfirst - Chuyển tới file đầu tiên
      - : blast - Chuyển tới file cuối cùng
      - : bdelete - Xóa file hiện tại
      - : badd - Mở một file với tên file theo sau
      - : e - Chỉnh sửa một file trong một buffers mới và chuyển sang nó.
- Chúng ta có thể edit file dễ dàng hơn bằng cách sử dụng chắc năng windows song song trong vim

```
:sp: Chia 2 file thành 2 cửa sổ theo chiều ngang
:vs: Chia 2 file thành 2 cửa sổ theo chiều dọc 

```

   -  Note: Có thể đánh số trước :sp , :vs để chỉnh kích thước của cửa sổ mới

```
 ctrl-ww: Thay đổi trỏ chuột sang cửa sổ tiếp theo
 ctrl-wc: Đóng cửa sổ hiện tại
 ctrl-w +: Tăng kích thước của cửa sổ hiện tại
 ctrl-w-: Giảm kích thước cửa sổ hiện tại
 ctrl-w =: Đặt tất cả các cửa sổ bằng kích thước
 ctrl-wn: Mở một cửa sổ mới với một bộ đệm mới

```

   - Cũng giống như windows chúng ta có thể mở các tab trong vim một cách dễ dàng bằng cách dùng command

```
 :tabnew

```

- Một số câu lệnh quản lí tab thường dùng :

```
  :tabclose : Đóng tab hiện tại 
  :tabn or (gt) : chuyển tới tab kế tiếp
  :tabp or (gT): chuyển về tab trước
  :tabs: liệt kê các tab hiện có 
```
`
 - Một số lệnh chi tiết khi sử dụng VIM 
   +  Tìm kiếm một từ khóa : (trong normal mode)
   `/tên từ khóa `
   + Hoặc chúng ta có thể tìm kiếm và thay thế theo cách sau :
   `:%/host/testvim/gc`
      - Sau đó hệ thống sẻ hỏi chúng ta :
      `replace with testvim (y/n/a/q/l/^ E/^Y) ?`   `y -> done`
      - Sau khi hoàn tất các việc chỉnh sửa, ta có thể lưu lại hoặc thoát :
      ```
      :q - Thoát khỏi VIM
      :q! - Thoát không cần lưu
      :w - lưu file
      :w! - ghi đè file (bắt buộc)
      :wq - lưu file rồi thoát
      ```

## 3. Luồng dữ liệu và các cậu lệnh điều hướng dòng dữ liệu :

### 3.1 Luồng dữ liệu
- Các chương trình trong Linux sẽ tự động được kết nối với 3 luồng dữ liệu khi chúng được thực thi.
  - **stdin** (standart input) : đây là luồng sẽ đưa dữ liệu vào chương trình để xử lý.
  - **stdout** (standard output) : luồng này dùng để xuất dữ liệu ra màn hình hiển thị sau quá trình thực thi hoàn tất mà không gặp lỗi.
  - **stderr** (standard error) : luồng này có chức năng tương tự stdout, tuy nhiên nó chỉ dùng để in các thông báo lỗi và đồng thời khi đó tín hiệu lỗi cũng được gửi tới hệ điều hành.
- Ngoài ra, tùy theo chương trình mà luồng **stdout** sẽ được thay thế bằng tệp tin hoặc máy in ... Việc liên kết các chương trình sẽ là việc đưa dữ liệu đầu ra của chương trình trước đến thẳng đầu vào của chương trình sau mà không để dữ liệu được in ra màn hình hiển thị hoặc file.
### 3.2 Các dạng điều hướng dòng dữ liệu

#### Chuyển hướng tới file

-   Là một trong 2 cách chuyển hướng đơn giản nhất, với cách này, dữ liệu đầu ra sẽ được lưu vào file thay vì in ra màn hình hiển thị.
-   Để chuyển hướng 1 câu lệnh tới file, Linux cung cấp cho người sử dụng 2 cú pháp:  `<`  (ghi nội dung ra file từ điểm bắt đầu, nếu file đã có nội dung thì ghi đè) và  `<<`  (tương tự  `<`  nhưng thay vì ghi đè lên nội dung cũ thì sẽ ghi từ điểm kết thúc của nội dung cũ)
-   Một vài VD:

> Ghi nội dung ra file, nếu file không tồn tại thì một file mới sẽ được tạo

![](https://viblo.asia/uploads/5f6d88b9-89bb-487f-8e7a-1e493abcaec5.png)

> Ghi đè nội dung file cũ

![](https://viblo.asia/uploads/b51344d4-6176-4410-8dc9-1107311f927e.png)

> Thêm nội dung cho file cũ

![](https://viblo.asia/uploads/13fae0d8-e191-4fd9-8b50-117472ef0f04.png)

#### Chuyển hướng từ file

-   Là cách chuyển hướng đơn giản còn lại, đi cùng với  **Chuyển hướng tới file**, cách này giống với việc đọc dữ liệu từ file và sử dụng dữ liệu đó làm đầu vào cho chương trình.
-   Chỉ có một ký hiệu duy nhất cho cách này là  `<`
-   VD:

> Trong VD này, nội dung của file được dùng làm đầu vào của câu lệnh  `wc`, có thể thấy rõ được sự khác biệt của 2 lần thực thi là lần 1 thì đầu vào là 1 file, lần 2 thì đầu vào chỉ là nội dung của file (output của  `wc`  không còn tên file nữa)

![](https://viblo.asia/uploads/57f86a5d-3a2c-4efe-a456-4b87e555d438.png)

#### Chuyển hướng tới  **stderr**

-   Thông thường, khi một câu lệnh gặp lỗi, thông tin lỗi sẽ hiển thị luôn lên màn hình cùng với các dữ liệu đầu ra
-   Linux cung cấp ký hiệu  `2>`  để đưa nội dung thông báo lỗi ra file thay vì màn hình hiển thị.
-   VD:

> Cũng tương tự như  **chuyển hướng tới file**, nhưng ở đây chỉ có thông báo lỗi được đưa vào file

![](https://viblo.asia/uploads/222251bf-842b-48aa-bb43-49ee27445edd.png)

#### Chuyển hướng tới câu lệnh khác

-   Sự chuyển hướng đặc biệt nhất, đưa đầu ra của một câu lệnh tới câu lệnh khác như đầu vào
-   Sử dụng ký hiệu  `|`  để chuyển hướng
-   Một vài VD:

![](https://viblo.asia/uploads/eb9e8879-7cec-4ec2-916f-0b4e4880a019.png)

