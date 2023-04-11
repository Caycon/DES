# Des
## Tổng quan:
- `DES`, viết tắt của `Data Encryption Standard`, là một thuật toán mã hóa đối xứng (`symmetric encryption`) được phát triển bởi Cục Tiêu Chuẩn Hoa Kỳ (NIST) vào năm 1970. `DES là một trong những thuật toán mã hóa cổ điển nhất và đã được sử dụng rộng rãi trong quá khứ. Tuy nhiên, do kích thước khóa ngắn (`56 bit`) đã bị lỗi thời và có các vấn đề về bảo mật, nên `DES` không còn được coi là an toàn cho các ứng dụng hiện đại.

- `DES` sử dụng phương pháp mã hóa đối xứng, trong đó cùng một khóa được sử dụng để mã hóa và giải mã dữ liệu. Khối dữ liệu gốc được chia thành các khối 64 bit và sau đó qua một loạt các phép hoán vị (`permutation`), hoán đổi (`substitution`) và xoay (`rotation`) để tạo ra đầu ra mã hóa. Mỗi khối dữ liệu 64 bit được mã hóa trong một vòng lặp (`round`) của thuật toán, và quá trình này được lặp lại 16 lần để tạo ra mã hóa hoàn chỉnh.

- Một điểm đáng lưu ý của `DES` là kích thước khóa ngắn, chỉ 56 bit. Điều này khiến `DES` dễ dàng bị tấn công bằng các cuộc tấn công `brute-force`, trong đó tất cả các khóa khả thi có thể thử nghiệm trong một thời gian hợp lý để tìm ra khóa đúng. Do đó, `DES` không còn được coi là an toàn và đã được thay thế bằng các thuật toán mã hóa mạnh hơn như AES (`Advanced Encryption Standard`) có khóa dài hơn.

- Tuy nhiên, `DES` vẫn được sử dụng trong một số hệ thống cũ hoặc trong các ứng dụng đặc biệt nơi các yêu cầu bảo mật không cao. Nếu bạn đang xem xét sử dụng `DES` trong dự án hoặc ứng dụng của mình, bạn nên tìm hiểu kỹ về các hạn chế và khuyến cáo của thuật toán này và cân nhắc sử dụng các thuật toán mã hóa mạnh hơn và an toàn hơn như `AES`.  
## Cách hoạt động:
- DES (`Data Encryption Standard`) là một thuật toán mã hóa đối xứng, tức là cùng một khóa được sử dụng cho cả quá trình mã hóa và giải mã dữ liệu. Dưới đây là mô tả cơ bản về cách DES hoạt động:

    + Bước chuẩn bị: Khóa được chuẩn bị trước đó, với độ dài `56 bit`, gồm `8 byte`. Khóa này được chia thành `16 subkey` (khóa con) có độ dài 48 bit mỗi khóa con thông qua các bước hoán vị và hoán đổi.

    + Bước khởi tạo: Dữ liệu cần được mã hóa được chia thành các khối 64 bit (8 byte) mỗi khối. Mỗi khối dữ liệu sau đó được đưa qua một bước hoán vị ban đầu (initial permutation) để chuẩn bị cho quá trình mã hóa chính.

    + Bước mã hóa: Quá trình mã hóa gồm 16 vòng lặp (rounds). Trong mỗi vòng lặp, khối dữ liệu 64 bit được chia thành hai nửa, mỗi nửa có độ dài 32 bit. Một nửa dữ liệu được giữ lại làm nửa trái (left half), nửa còn lại được đưa qua một bước mở rộng (expansion) để tăng kích thước từ 32 bit lên 48 bit, sau đó được XOR với một subkey tương ứng (khóa con) của vòng lặp đó. Kết quả sau đó được đưa qua các hộp hoán đổi (substitution boxes hoặc S-boxes), là các bảng hoán đổi có sẵn trong thuật toán DES, để thay thế 48 bit dữ liệu đầu vào thành 32 bit dữ liệu đầu ra. Sau đó, dữ liệu này được đưa qua một bước hoán vị (permutation) và sau đó được XOR với nửa phải (right half) của dữ liệu trước đó.

    + Bước hoàn tất: Sau khi đã hoàn thành 16 vòng lặp mã hóa, hai nửa của dữ liệu cuối cùng được hoán đổi với nhau, sau đó được đưa qua bước hoán vị cuối cùng (final permutation) để tạo ra đầu ra mã hóa cuối cùng có độ dài 64 bit.

- Quá trình giải mã trong DES tương tự với quá trình mã hóa, chỉ khác là thứ tự của các khóa con được sử dụng ngược lại, từ khóa con thứ 16 đến khóa con thứ 1, và không có bước mở rộng dữ liệu trong quá trình giải mã.

- Lưu ý là DES đã bị lỗi thời và không được coi là an toàn cho các ứng dụng hiện đại do độ
