# 3DES- Triple DES.  
--------
## Nguyên tắc hoạt động:
- `3DES (Triple Data Encryption Standard)` là một thuật toán mã hóa đối xứng được sử dụng trong lĩnh vực bảo mật thông tin. Nó là một biến thể của thuật toán mã hóa DES (Data Encryption Standard) được phát triển vào những năm 1970 bởi Viện Tiêu chuẩn và Công nghệ Quốc gia Hoa Kỳ (NIST). DES ban đầu được sử dụng rộng rãi, nhưng sau này đã trở nên không an toàn trước các cuộc tấn công hiện đại.

- `3DES` sử dụng khóa đối xứng có độ dài `168 bit` (hoặc `112 bit` trong một biến thể khác) và hoạt động trên khối dữ liệu có độ dài 64 bit. Nó hoạt động theo nguyên tắc của mã hóa đối xứng, trong đó cùng một khóa được sử dụng để mã hóa và giải mã dữ liệu. Tuy nhiên, 3DES sử dụng cơ chế lặp lại ba lần để tăng tính bảo mật, trong đó dữ liệu được mã hóa ba lần với ba khóa khác nhau.

- Cụ thể, quá trình mã hóa 3DES gồm ba bước chính:

  - `Mã hóa với khóa 1 (K1)`: Dữ liệu được `mã hóa` với khóa đầu tiên (K1) bằng thuật toán DES.

  - `Giải mã với khóa 2 (K2)`: Kết quả của bước 1 được `giải mã` bằng khóa thứ hai (K2) bằng thuật toán DES.

  - `Mã hóa lại với khóa 3 (K3)`: Kết quả của bước 2 được `mã hóa` lần nữa bằng khóa thứ ba (K3) bằng thuật toán DES.

- Kết quả cuối cùng là dữ liệu đã được mã hóa theo 3DES và có độ bảo mật cao hơn so với DES truyền thống. 3DES vẫn được sử dụng trong một số ứng dụng bảo mật thông tin, nhưng ngày càng ít được sử dụng hơn do tốc độ mã hóa chậm hơn so với các thuật toán mã hóa hiện đại như AES (Advanced Encryption Standard).  
-------
## Keying option:  
- `Keying option 1`: cả 3 key[1, 2, 3] đều độc lập, độ dài an toàn là 56 bit mỗi key. Tuy nhiên nó vẫn dễ bị tấn công bởi [`meet-in-the-middle attack`](https://en.wikipedia.org/wiki/Meet-in-the-middle_attack).
- `Keying option 2`: key1= key3, key2 độc lập, độ dài hoàn hảo của key là 56 bit. Tuy nhiên giống như `Keying option 1` nó dễ bị tấn công bới `meet-in-the-middle attack`.  
- `Keying option 3`: cả 3 key đều giống nhau, khi ấy 3DES= DES. Vì sau bước 1 và 2 thì bản ciphertext= plantext.  
- Lý do độ an toàn mỗi key chỉ là 56 bit chứ không phải 64 bit vì:
  - Khi sử dụng khóa 64 bit trong 3DES, 8 bit cuối cùng của mỗi khóa không được sử dụng. Điều này làm giảm bộ khóa thực sự xuống còn 56 bit, giống như trong thuật toán DES gốc. Điều này làm tăng khả năng tấn công brute-force, trong đó kẻ tấn công thử từng giá trị cho 56 bit khóa để tìm ra giá trị khóa chính xác. Với khóa 64 bit, không gian khóa khả dĩ chỉ có 2^56 giá trị khác nhau, điều này đã bị cho là không đủ an toàn đối với bảo mật hiện đại.

  - Trong khi đó, khi sử dụng khóa 56 bit, không gian khóa khả dĩ là 2^56 giá trị khác nhau, đây được cho là mức độ bảo mật đáng tin cậy. Tuy nhiên, cũng cần lưu ý rằng 3DES đang dần được thay thế bằng thuật toán AES với khóa dài hơn (128 bit, 192 bit, 256 bit) để đảm bảo tính bảo mật cao hơn và tốc độ xử lý nhanh hơn trong các ứng dụng bảo mật hiện đại.
