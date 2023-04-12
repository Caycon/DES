# How to DES work:
------
## Tổng quát:
- DES (Data Encryption Standard) là một thuật toán mã hóa đối xứng (symmetric encryption) sử dụng khóa đối xứng có độ dài 56 bit để mã hóa và giải mã dữ liệu. Cơ chế của DES bao gồm các bước chính sau:

  ##### I. Chuẩn bị dữ liệu đầu vào và khóa:  
  - Dữ liệu đầu vào cần được chia thành hai nửa, mỗi nửa có độ dài 32 bit, được ký hiệu là L0 và R0. Khóa cần được chia thành 16 khóa con, mỗi khóa con có độ dài 48 bit, được ký hiệu là K1, K2, ..., K16.

  ##### II. Phân tích khóa:  
  - Khóa ban đầu được phân tích ra thành 16 khóa con để sử dụng trong các vòng lặp tiếp theo. Quá trình này bao gồm hoán vị, thay thế, và xoay bit trên các bit của khóa ban đầu để tạo ra các khóa con K1, K2, ..., K16.

  ##### III. Mã hóa Feistel:  
  - DES thực hiện 16 vòng lặp mã hóa Feistel, trong mỗi vòng lặp, hai nửa dữ liệu (L và R) được xử lý riêng biệt. Nửa R đầu tiên được sao chép sang nửa L, và nửa R được biến đổi theo một hàm f() sử dụng khóa con tương ứng của vòng lặp đó. Hàm f() bao gồm các bước hoán vị, thay thế, mở rộng, và xoay bit, đồng thời được kết hợp với khóa con bằng phép XOR. Sau đó, nửa L và nửa R được hỗn hợp lại với nhau bằng phép XOR.

  ##### IV. Hỗn hợp:  
  - Sau khi hoàn thành các vòng lặp mã hóa Feistel, hai nửa dữ liệu (L16 và R16) được hỗn hợp lại với nhau để tạo ra dữ liệu đã mã hóa. Dữ liệu đã mã hóa có độ dài 64 bit, được kết hợp từ nửa L16 và nửa R16 theo thứ tự R16L16.

  ##### V. Giải mã:  
  - Để giải mã dữ liệu đã mã hóa, cùng một quá trình được thực hiện, nhưng sử dụng các khóa con trong thứ tự ngược lại. Các khóa con K16, K15, ..., K1 được sử dụng theo thứ tự đảo ngược để giải mã dữ liệu đã mã hóa, và kết quả là dữ liệu gốc ban đầu (L0 và R0) được tái tạo lại.  
## Chi tiết:
##### I. Chuẩn bị dữ liệu đầu vào và khóa: 
          1.1. Chuẩn bị dữ liệu đầu vào: Dữ liệu đầu vào cần được chia thành hai nửa, mỗi nửa có độ dài 32 bit. Dữ liệu đầu vào được ký hiệu là L0 và R0, trong đó L0 là 32 bit đầu tiên của dữ liệu đầu vào, và R0 là 32 bit cuối cùng của dữ liệu đầu vào.

          1.2. Chuẩn bị khóa: Khóa ban đầu có độ dài 56 bit. Tuy nhiên, để sử dụng trong các vòng lặp mã hóa Feistel, khóa ban đầu cần được phân tích ra thành 16 khóa con, mỗi khóa con có độ dài 48 bit. Quá trình này bao gồm các bước hoán vị, thay thế, và xoay bit trên các bit của khóa ban đầu để tạo ra các khóa con K1, K2, ..., K16.

            1.2.1. Hoán vị khóa ban đầu: 56 bit của khóa ban đầu được hoán vị theo một bảng hoán vị cụ thể, được ký hiệu là PC-1 (Permutation Choice 1). Quá trình này loại bỏ 8 bit chẵn của khóa ban đầu để giảm độ dài khóa từ 56 bit xuống còn 48 bit.

            1.2.2. Chia khóa hoán vị ra thành hai nửa: Sau khi hoán vị khóa ban đầu, 56 bit của khóa ban đầu được chia thành hai nửa, mỗi nửa gồm 28 bit. Các nửa này được ký hiệu là C0 và D0.

            1.2.3. Xoay bit trên các nửa: Sau đó, các nửa C0 và D0 được xoay trái (hoặc phải) một số bước nhất định, được gọi là shift, để tạo ra các nửa C1, C2, ..., C16 và D1, D2, ..., D16. Số bước shift được xác định bởi một bảng lịch shift cụ thể, tùy thuộc vào vòng lặp mã hóa Feistel tương ứng.

            1.2.4. Ghép nửa C và nửa D lại thành các khóa con: Cuối cùng, từ các nửa C1, C2, ..., C16 và D1, D2, ..., D16 đã được xoay, các khóa con K1, K2, ..., K16 được tạo ra bằng cách kết hợp lại các nửa này theo thứ tự và hoán vị khác nhau, được ký hiệu là PC-2 (Permutation Choice 2). Các khóa con K1, K2, ..., K16 được sử dụng trong các vòng lặp mã hóa Feistel của DES để thực hiện các phép hoán vị và thay thế trên dữ liệu đầu vào.  
##### II. Phân tích khóa:
          2.1. Hoán vị khóa ban đầu: Khóa ban đầu được hoán vị theo bảng PC-1, trong đó 56 bit của khóa được sắp xếp lại theo một thứ tự mới để loại bỏ 8 bit chẵn và tạo ra hai nửa khóa con, gồm nửa trái C0 (28 bit) và nửa phải D0 (28 bit).

          2.2. Xoay bit trái (hoặc phải): Sau khi hoán vị, hai nửa khóa con C0 và D0 được xoay bit trái (hoặc phải) một số bước nhất định dựa trên bảng lịch shift, để tạo ra các nửa khóa con C1, C2, ..., C16 và D1, D2, ..., D16. Số lượng bước xoay bit được xác định trước và khác nhau trong các vòng lặp, tạo ra tính đa dạng của các khóa con.

          2.3. Tạo khóa con: Sau khi hoàn thành bước xoay bit, các nửa khóa C và D được kết hợp lại và hoán vị theo bảng PC-2 để tạo ra các khóa con K1, K2, ..., K16 có độ dài 48 bit. Quá trình hoán vị này định nghĩa cách các bit của nửa trái và nửa phải khóa con được kết hợp lại để tạo ra các khóa con cuối cùng.  
##### III. Mã hóa Feistel:  
          3.1. Phân chia dữ liệu đầu vào: Dữ liệu đầu vào (64 bit) được chia thành hai nửa, gồm nửa trái (L0) và nửa phải (R0), mỗi nửa có độ dài 32 bit.

          3.2. Sao chép dữ liệu: Nửa phải của dữ liệu (R0) được sao chép sang một biến tạm thời để sử dụng trong quá trình tính toán.

          3.3. Phép mở rộng: Nửa phải của dữ liệu (R0) được mở rộng từ 32 bit lên 48 bit bằng cách áp dụng bảng hoán vị E, trong đó các bit của R0 được lặp lại và xếp theo một thứ tự mới.

          3.4. XOR với khóa con: Khóa con tương ứng với vòng lặp hiện tại (Ki) được XOR với dữ liệu sau khi đã được mở rộng (E(R0)), kết quả là một dãy 48 bit.

          3.5. Thay thế: Dãy 48 bit sau khi XOR với khóa con được chia thành 8 nhóm, mỗi nhóm 6 bit, và được áp dụng bảng thay thế S (Substitution Box) để biến đổi thành dãy 32 bit mới. Mỗi bảng thay thế S có 4 hàng và 16 cột, tương ứng với 4 bit đầu vào và 4 bit đầu ra.

          3.6. Hoán vị: Dãy 32 bit sau khi thay thế S được hoán vị theo bảng hoán vị P, để tạo ra dữ liệu mới (P(S(E(R0) XOR Ki))).

          3.7. XOR với nửa trái: Dữ liệu mới tính toán được XOR với nửa trái của dữ liệu đầu vào (L0), kết quả là nửa phải của dữ liệu đầu vào tiếp theo (R1 = L0 XOR P(S(E(R0) XOR Ki))).

          3.8. Gán lại dữ liệu: Nửa phải (R1) trở thành nửa trái (L1) cho vòng lặp tiếp theo, và nửa phải (R1) trở thành nửa trái (L1) cho vòng lặp tiếp theo, và nửa phải (R1) trở thành nửa trái (L1) cho vòng lặp tiếp theo.
##### IV. Hỗn hợp:
   - Sau khi hoàn tất 16 vòng lặp mã hóa Feistel, hai nửa dữ liệu cuối cùng (L16 và R16) được hỗn hợp lại để tạo thành dữ liệu đã mã hóa. Quá trình hỗn hợp trong DES bao gồm các bước sau:

          4.1. Ghép nối dữ liệu: Nửa dữ liệu cuối cùng L16 và R16 được ghép nối lại với nhau, thường theo thứ tự L16 trước và R16 sau, để tạo thành dữ liệu đã mã hóa gồm 64 bit.

          4.2. Hoán vị đảo ngược: Sau khi ghép nối dữ liệu, một bước hoán vị đảo ngược được thực hiện trên dữ liệu đã ghép nối. Bước này là một hoán vị trên 64 bit dữ liệu, được xác định bởi một bảng hoán vị cụ thể, được ký hiệu là IP-1 (Inverse Initial Permutation). Bảng hoán vị IP-1 là hoán vị đảo ngược của bảng hoán vị IP được sử dụng ở bước ban đầu của quá trình mã hóa.

          4.3. Kết quả mã hóa: Sau khi hoàn thành hoán vị đảo ngược, dữ liệu đã mã hóa (có độ dài 64 bit) được tạo ra. Đây là kết quả của quá trình mã hóa DES, có thể được truyền đi hoặc lưu trữ tùy vào ứng dụng cụ thể.
##### V. Giải mã:  
   - Quá trình giải mã trong DES là quá trình ngược lại của quá trình mã hóa, sử dụng các khóa con được sử dụng trong quá trình mã hóa theo thứ tự ngược lại. Quá trình giải mã bao gồm các bước sau:

          5.1. Chuẩn bị dữ liệu đã mã hóa: Dữ liệu đã mã hóa được đưa vào quá trình giải mã. Độ dài của dữ liệu đã mã hóa là 64 bit.

          5.2. Hoán vị ban đầu: Một bước hoán vị được áp dụng lên dữ liệu đã mã hóa, được xác định bởi một bảng hoán vị cụ thể, được ký hiệu là IP (Initial Permutation). Bảng hoán vị IP là bảng hoán vị được sử dụng trong bước ban đầu của quá trình mã hóa.

          5.3. Phân tích dữ liệu đã mã hóa: Sau khi hoán vị ban đầu, dữ liệu đã mã hóa được chia thành hai nửa, mỗi nửa có độ dài 32 bit, được ký hiệu là L0 và R0, tương ứng với các nửa dữ liệu ban đầu trước khi mã hóa.

          5.4. Mã hóa Feistel ngược: Quá trình giải mã trong DES sử dụng các khóa con trong quá trình mã hóa theo thứ tự ngược lại (K16, K15, ..., K1). Mỗi vòng lặp của quá trình mã hóa Feistel được thực hiện ngược lại trong quá trình giải mã, bao gồm các phép biến đổi như hoán vị, thay thế, xoay bit, ... được áp dụng lên nửa dữ liệu L và R theo thứ tự từ K16 đến K1.

          5.5. Hỗn hợp: Sau khi hoàn tất 16 vòng lặp mã hóa Feistel ngược, hai nửa dữ liệu cuối cùng (L16 và R16) được hỗn hợp lại với nhau để tạo ra dữ liệu đã giải mã.

          5.6. Hoán vị đảo ngược: Cuối cùng, một bước hoán vị đảo ngược được thực hiện trên dữ liệu đã giải mã, được xác định bởi bảng hoán vị IP-1 (Inverse Initial Permutation), là hoán vị đảo ngược của bảng hoán vị IP được sử dụng ở bước ban đầu của quá trình mã hóa.

   -  Quá trình giải mã trong DES đảm bảo tính ngược lại của quá trình mã hóa, giúp khôi phục lại dữ liệu gốc từ dữ liệu đã mã hóa bằng cách sử dụng các khóa con trong thứ tự ngược lại.
