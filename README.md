# Reverse-Engineering
1. Các thanh ghi: Là các phần tử có khả năng lưu trữ thông tin với dung lượng 8,16,32,64 bit

Phân loại thanh ghi:
+ Thanh ghi tổng quát: chủ yếu dùng để lưu trữ dữ liệu trong quá trình thực thi chương trình, nhưng mỗi thanh ghi có một số chức năng riêng.
+ Thanh ghi điều khiển: Các bit của nó quy định tác vụ của các đơn vị chức năng của máy tính.
+ Thanh ghi trạng thái: Lưu thông tin mô tả trạng thái.

AX register: Ngoài chức năng lưu trữ dữ liệu, nó còn được CPU dùng trong phép nhân chia.

BX register: Lưu trữ địa chỉ của 1 thủ tục hay biến, nó cũng được dùng thực hiện các phép dời chuyển số học và dữ liệu.

DX register: Có vai trò đặc biệt trong phép nhân và phép chia ngoài chức năng lưu trữ dữ liệu.

CX register: Thanh ghi này dùng làm bộ đếm trong các vòng lặp. Các lệnh tự động lặp lại và sau mỗi lần lặp giá trị của CX tự động giảm đi 1. Thường dùng chứa số lần dịch, quay trong các lệnh dịch, quay thanh ghi.

Note: Các thanh ghi A,B,C,DX có thể được chia thành  A,B,C,DH và  A,B,C,DL với các chức năng khác nhau.
