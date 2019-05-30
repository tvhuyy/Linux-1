## 1. Symlink :
### 1.1 Hard link và Soft link trong Linux :
- **Hard link**(liên kết cứng) : là liên kết trong cùng một hệ thống tập tin với hai node entry tương ứng cùng trỏ đến một nội dung vật lý.
  - inode của các tập tin hoàn toàn giống nhau.
  - khi xóa file gốc thì nội dung tập tin hard link không bị mất đi.
  - không thể tạo hard link trên hai partition khác nhau.
  - không thể tạo một hard link tới 1 thư mục.
  - cách tạo hard link : `ln <path/tên file> <tên hard link>`

 - **Soft link**(liên kết mềm) : là liên kết không dùng đến node entry mà chỉ đơn thuần là một shortcut.

   - Soft link tạo ra một inode mới và nội dung của inode này trỏ đến inode của file gốc.
   - Cách tạo soft link : `ln -s <path/tên file> <tên soft link>`
   - nội dung của soft link sẽ bị mất đi khi ta xóa file/folder gốc.
   - soft link có thể liên kết đến một thư mục
   - soft link có thể liên kết đến hai file thuộc hai phân vùng khác nhau
   - để xóa một soft link ta không thêm dấu `/` mà ghi tên của soft link
### 1.2 Tạo soft link tới file cấu hình network interface trên thư mục /root :
- ![alt](https://i.imgur.com/yJUUzmk.png)
