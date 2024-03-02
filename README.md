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

Các thanh ghi đoạn được sử dụng như là địa chủ cơ sở của các lệnh trong chương trình, Stack và dữ liệu. 4 thanh ghi đoạn bao gồm:
+ CS (Code Segment): Chứa địa chỉ bắt đầu của code trong chương trình.
+ DS (Data Segment): Chứa địa chỉ của các biến khai báo trong chương trình.
+ SS (Stack Segment): CHứa địa chỉ của bộ nhớ Stack dùng trong chương trình.
+ ES (Extra Segment): Chứa địa chỉ cơ số bổ sung cho các biến bộ nhớ.

Note: Đối với các thanh ghi là 32, 64 bit. Ta ghi thêm E trước các thanh ghi 16bit.. EAX, EBX, ECX,..
2. Sử dụng ngắt(Interrput) trong chương trình assembly

Ngắt (Interrupt) là các tín hiệu mà các thành phần trong hệ thống, như: thiết bị ngoại vi, hệ điều hành, chương trình người sử dụng, ..., gửi đến vi xử lý (họ Intel) mỗi khi nó cần trao đổi thông tin với vi xử lý hay cần được sự phục vụ từ vi xử lý. Có nhiều loại ngắt, bao gồm: Ngắt phần cứng, ngắt phần mềm, ngắt bên trong, ngắt không chắn được( ngắt có độ ưu tiên cao nhất). Ở đây ta tập trung ngắt mềm.

Ngắt mềm là các ngắt được phát sinh trong hệ điều hành và chương trình người sử dụng, điều này thường thấy trong assembly. Hệ thống ngắt mềm trong máy tính gồm 256 ngắt được đánh số từ 0 đến 255, và được gọi là số hiệu ngắt. Mỗi ngắt mềm tương ứng với một chương trình con gọi là chương trình con phục vụ ngắt.

Hợp ngữ cung cấp lệnh Int để gọi các chương trình ngắt mềm khi cần. Như vậy khi hệ thống nhận một yêu cầu ngắt n sẽ là (Int n)

a. Lệnh Int: Như đã nói, lệnh int dùng để gọi các chương trình ngắt mềm. Trong các chương trình ngắt mềm, có thể thực hiện nhiều chức năng khác nhau, mỗi chức năng thồn qua một con số, số hiệu hàm của ngắt. Do đó, cần gọi ngắt chương trình phải chỉ rõ ngắt ở hàm nào, bằng cách được số hiệu hàm vào thanh ghi AH.
Ví dụ 1:
      
      Mov Ah, 01; gọi ngắt 21h với hàm 01.
      Int 21h ;  01 của ngắt 21h.
Ví dụ 2:

        Mov        Ah, 02                           ; đặt số hiệu hàm cần gọi vào AH

        Mov        DH, 10                        ; cung cấp dữ liệu vào thứ nhất vào DH

        Mov        DL, 20                        ; cung cấp dữ liệu vào thứ hai vào DL

        Int           10h                             ; gọi ngắt 10h với hàm 02. Hàm/ngắt này không

                                                            ; trả về dữ liệu kết quả.
b. Hàm ngắt 21h

Ngắt 21h của MSDOS là ngắt thường được sử dụng nhất đối với các hàm vào/ra kí tự xâu/ kí tự cơ bản. Chức năng của mỗi ngắt, mỗi hàm là khác nhau.

Ví dụ 1: In ra màn hình kí tự A:

            Mov          Ah, 02

            Mov          Dl, ‘A’                  ;có thể viết lệnh  Mov   Dl, 41h      

            Int             21h                       ; 41h là mã ASCII của kí tự A


