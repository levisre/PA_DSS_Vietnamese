#Tiêu chuẩn An toàn dữ liệu cho ứng dụng thanh toán - Payment Application Data Security Standards (PA DSS) #

##Mục lục##

[Khái niệm](#definion)

[Phạm vi của PA DSS](#scope)

[Yêu cầu 1. Không lưu trữ toàn bộ dữ liệu thẻ, mã xác thực hoặc các dữ liệu khác dùng để xác thực (CAV2, CID, CVC2, CVV2, PIN number)](#req1)

[Yêu cầu 2. Bảo vệ dữ liệu thẻ khi lưu trữ](#req2)

[Yêu cầu 3. Cung cấp các tính năng xác thực an toàn](#req3)

[Yêu cầu 4. Ghi log hoạt động của ứng dụng thanh toán](#req4)

[Yêu cầu 5. Phát triển các ứng dụng thanh toán an toàn](#req5)

[Yêu cầu 6. Bảo vệ khi truyền tải qua mạng không dây](#req6)

[Yêu cầu 7. Kiểm tra bảo mật cho các ứng dụng thanh toán và luôn duy trì cập nhật](#req7)

[Yêu cầu 8. Tính tương thích với các mô hình mạng an toàn](#req8)

[Yêu cầu 9. Không lưu trữ dữ liệu thẻ trên các server có kết nối internet](#req9)

[Yêu cầu 10. Tính tương thích với các cơ chế truy cập từ xa an toàn đến ứng dụng thanh toán](#req10)

[Yêu cầu 11. Mã hóa các traffic quan trọng khi truyền tải trên đường mạng công cộng](#req11)

[Yêu cầu 12. Bảo vệ tất cả các truy cập bằng quyền quản trị không sử dụng console](#req12)

[Yêu cầu 13. Tạo lập và duy trì bản hướng dẫn triển khai dịch vụ phù hợp với PA DSS cho khách hàng, nhà bán lẻ, hoặc đối tác tích hợp dịch vụ](#req13)

[Yêu cầu 14. Giao trách nhiệm đảm bảo PA DSS cho cá nhân, duy trì chương trình đào tạo cho từng cá nhân, khách hàng, nhà bán lẻ, hoặc đối tác tích hợp](#req14)

##<a id="definion"/>Khái niệm##

The PCI Payment Application  Data Security  Standard (PA DSS) là bộ tiêu chuẩn được đặt ra để xác định các yêu cầu bảo mật và quy trình đánh giá cho nhà phát triển các ứng dụng thanh toán. Các ứng dụng thanh toán đáp ứng được theo chuẩn PA DSS sẽ giúp cho các ứng dụng này được sử dụng trong môi trường tương thích với chuẩn PCI DSS. 

##<a id="scope"/>Phạm vi của PA DSS##

PA DSS áp dụng cho tất cả các nhà phát triển phần mềm và những cá nhân, tổ chức khác đang phát triển các ứng dụng  thanh toán mà có tính năng lưu trữ, xử lý, và truyền tải dữ liệu thẻ hoặc các dữ liệu xác thực quan trọng khác, 

Phạm vi đánh giá PA DSS bao gồm:

1. Tất cả các tính năng của ứng dụng
    - Các hoạt động thanh toán End-to-end (xác thực và thanh toán)

    - Nhập/xuất dữ liệu

    - Xử lý lỗi

    - Giao diện và các kết nối đến các file, hệ thống, ứng dụng thanh toán hoặc các thành phần ứng dụng khác

    - Tất cả các luồng xử lý dữ liệu thẻ

    - Các phương thức mã hóa

    - Các phương thức xác thực

2.	Tất cả các hướng dẫn mà nhà cung cấp ứng dụng cần để cung cấp cho khách hàng, các bên cần tích hợp/nhà phân phối để đảm bảo:

    - Khách hàng biết cách để triển khải ứng dụng thanh toán trong môi trường tuân thủ PCI DSS

    - Khách hàng được thông báo rằng một vài thành phần trong ứng dụng thanh toán hoặc các cấu hình  có thể không phù hợp với PCI DSS.

    >   Lưu ý rằng nhà cung cấp ứng dụng cũng cần phải cung cấp những hướng dẫn kể cả khi có các trường hợp sau:


    - Không thể được xử lý bởi nhà cung cấp ứng dụng một khi ứng dụng đó được cài đặt bởi khách hàng

    - Trách nhiệm thuộc về khách hàng, không phải nhà cung cấp ứng dụng.

3.	Bao gồm tất cả các nền tảng cho các phiên bản ứng dụng thanh toán đã được kiểm tra (liệt kê tất cả các nền tàng được sử dụng). 

4.	Bao gồm tất cả các công cụ được sử dụng bởi ứng dụng thanh toán để truy cập dữ liệu thẻ (các công cụ tạo report, công cụ ghi log,vv...)

5.	Bao gồm tất cả các thành phần có liên quan đến ứng dụng thanh toán, các thành phần của bên thứ 3 (thư viện, framework, các phần mềm khác,...)

6.	Bao gồm tất cả các dạng ứng dụng thanh toán khác  cần thiết để thiết lập một môi trường thanh toán hoàn chỉnh.

7.	Bao gồm cả phương pháp quản lý phiên bản  của nhà cung cấp ứng dụng.

Ý nghĩa các từ viết tắt có thể gặp trong tài liệu

- PIN : Personal Indentify Number, Mã số xác thực cá nhân

- PAN: Personal Account Number, Số tài khoản cá nhân

- SAD: Sensitive Authentication Data, Dữ liệu xác thực quan trọng


### <a id="req1"/>Yêu cầu 1. Không lưu trữ toàn bộ dữ liệu thẻ, mã xác thực  hoặc các dữ liệu khác dùng để xác thực (CAV2, CID, CVC2, CVV2, PIN number) ###

1.1.	Không được lưu trữ các thông tin xác thực quan trọng sau khi quá trình xác thực hoàn tất (kể cả khi đã được mã hóa. Nếu như nhận được các dữ liệu xác thực quan trọng, phải xử lý sao cho các dữ liệu này không thể truy cập và khôi phục lại  sau khi quá trình xác thực hoàn tất. 
Các thông tin xác thực quan trọng được mô tả  ở các phần 1.1.1 đến 1.1.3

*Yêu cầu này gắn liền với phần 3.2 trong PCI DSS*

1.1.1.	Không được lưu trữ toàn bộ nội dung của thẻ thanh toán ( bao gồm  dải từ  ở mặt sau của thẻ,  các thông tin lưu trong chip nhớ, hoặc các nơi khác) sau khi xác thực.
Ghi chú: Trong các nghiệp vụ tài chính phổ biến, các dữ liệu sau có thể được dữ lại để tiếp tục sử dụng:

- Tên chủ thẻ

- Số tài khoản cá nhân (PAN)

- Ngày hết hạn

- Mã dịch vụ

Để giảm thiểu rủi ro,  chỉ lưu trữ những dữ liệu này khi nghiệp vụ tài chính yêu cầu.
Ví dụ các thông tin không được phép lưu trữ sau khi kết thúc quá trình xác thực:

- Các thông tin thanh toán đầu vào

- Tất cả các nhật kí (ví dụ:  Lịch sử giao dịch,  thông tin gỡ lỗi, các thông báo lỗi,...)

- Các file lưu trữ lịch sử

- Các file lưu trữ thông tin gỡ lỗi

- Các bản mẫu database khác

- Các nội dung trong database

*Yêu cầu này gắn liền với phần 3.2.1 trong PCI DSS*.

1.1.2.	Không lưu trữ mã xác nhận của thẻ hoặc các giá trị được sử dụng để xác thực (ví dụ như cụm 3 số hoặc 4 số được in ở mặt trước hoặc mặt sau  của thẻ, dùng trong các trường hợp thanh toán không quẹt thẻ) sau khi quá trình xác thực hoàn tất. Các thông tin liên quan khác không được phép lưu trữ giống mục 1.1.1

*Yêu cầu này gắn liền với phần 3.2.2 trong PCI DSS*

1.1.3.	Không được lưu trữ mã định danh cá nhân (PIN Number) hoặc cụm mã PIN được mã hóa sau khi hoàn tất quá trình xác thực. Các thông tin liên quan khác không được phép lưu trữ giống mục .1.1.1

*Yêu cầu này gắn liền với phần 3.2.3 trong PCI DSS*

1.1.4.	Tiễn hành xóa an toàn với tất cả dữ liệu lấy từ thẻ (lưu trữ trên dải từ hoặc những thông tin tương đương được lưu trên chip nhớ), mã xác nhận của thẻ, PIN lưu lại bởi những phiên bản trước của ứng dụng thanh toán, và phải tuân theo chuẩn xóa bỏ dữ liệu an toàn dành cho môi trường doanh nghiệp, ví dụ như danh sách các sản phẩm được liệt kê bởi NSA, hoặc các chuẩn riêng của từng quốc gia.

Ghi chú: Phần này chỉ được áp dụng nếu như các phiên bản trước của phần mềm thanh toán có lưu truex các dữ liệu thẻ quan trọng

1.1.5.	Không lưu trữ các thông tin thẻ quan trọng trên hệ thống của nhà sản xuất. Nếu như bất cứ một thông tin quan trọng nào (thông tin trước khi xác thực) cần được sử dụng trong quá trình đebug và khắc phục sự cố, thì cần phải tuân thủ những điều sau:

- Các thông tin xác thực quan trọng chỉ được sử dụng khi muốn giải quyết một vấn đề cụ thể

- Những thông tin đó phải được lưu trữ ở một nơi được xác định rõ ràng, và được giới hạn truy cập

- Chỉ được phép thu thập một phần nhỏ thông tin thẻ (những thông tin cần thiết) để khắc phục sự cố.

- Những thông tin xác thực quan trọng  phải được mã hóa, sử dụng các thuật toán mã hóa mạnh trong khi lưu trữ

- Dữ liệu sau khi được sử dụng cần phải được xóa ngay lập tức, bao gồm cả:

	- File log

	- Các file debug

	- Các nguồn thông tin khác nhận được từ khách hàng

*Yêu cầu này gắn liền với phần 3.1 trong PCI DSS*

###<a id="req2"/>Yêu cầu 2. Bảo vệ dữ liệu thẻ khi lưu trữ

2.1.	Nhà phát triển ứng dụng phải cung cấp hướng dẫn cho khách hàng về việc xóa an toàn các dữ liệu thẻ sau khi hết thời hạn lưu trữ do khách hàng định sẵn.

*Yêu cầu này gắn liền với phần 3.1 trong PCI DSS*

2.2.	Che bới số tài khoản cá nhân (Personal Account Number – PAN) khi hiển thị (6 kí tự đầu hoặc 4 kí tự cuối là số lượng kí tự tôi đa được phép hiện thỉ), Thêm vào đó, chỉ có cá nhân có yêu cầu về nghiệp vụ tài chính hợp lý mới được phép xem nhiều hơn 6 kí tự đầu/4 kí tự cuối của PAN.

*Yêu cầu này gắn liền với phần 3.3 trong PCI DSS*

2.3.	Tiến hành xử lý để PAN không thể đọc được ở bất cứ nới nào chúng được lưu trữ (bao gồm dữ liệu trên các thiết bị lưu trữ di động, các thiết bị backup, trong log file) bằng cách sử dụng bất cứ phương pháp nào trong các phương pháp dưới đấy;
- Sử dụng thuật toán băm (hashing) mạnh (hash toàn bộ PAN)

- Xóa bỏ bớt một phần của PAN (các mã hash không thể được dùng để thay thế cho các phần đã bị xóa bỏ của PAN).

- Sử dụng token

- Sử dụng các thuật toán mã hóa mạnh kèm keo một cơ chế quản lý và phân phối khóa.

*Yêu cầu này gắn liền với phần 3.4 trong PCI DSS*

2.4.	Ứng dụng thanh toán phải bảo vệ các khóa được sử dụng trong quá trìnhmã hóa dữ liệu thẻ để chống lại việc bị làm lộ hoặc sử dụng sai mục đích.

*Yêu cầu này gắn liền với phần 3.5 trong PCI DSS*

2.5.	Ứng dụng thanh toán phải thiết lập một cơ chế quản lý và phân phối khóa được sử dụng cho các khóa tham gia vào quá trình mã hóa dữ liệu thẻ. Bào gồm ít nhất một trong các mục dưới đây:

2.5.1. Tạo các khóa mạnh

2.5.2. Bảo vệ quá trình phân phối khóa

2.5.3. Bảo vệ nơi lưu trữ khóa

2.5.4. Tiến hành thay đôi khóa mới cho những khóa đã hết hạn sử dungj(ví dụ, sau mootj khoảng thời gian nhất định, hoặc là sau một số lượng nhất định các dữ liệu được mã hóa bởi khóa đã có), được xcas định vởi nhà cung cấp ứng dụng, hoặc đơn vị sở hữu khóa, dựa trên các tài liệu hướng dẫn và các ví dụ thực tế của doanh nghiệp (ví dụ, tài liệu NIST Special Publication 800-57)

2.5.5. Thảy đổi hoặc loại bỏ khóa (ví dụ, lwuux trữ, hủy bỏ, vô hiệu hóa), khi tính khả dụng của khóa bị yếu đi (ví dụ, nhân viên biết về khóa đó nghỉ việc,...) hoặc khóa bị nghi ngờ là đã bị lộ.

Ghi chú: Với các khóa đã bị vô hiệu hóa hoặc bị thay đổi vẫn cần được giữ lại, thì những khóa này cần phải lưu trữ một cách an toàn, sử dụng thuật toán mã hóa. Những kháo đã được lưu trữ đó chỉ được sử dụng phục vụ cho mục đích giải mã hoặc xác thực.

2.5.6 Nếu như ứng dụng thanh toán hỗ trợ các hoạt động quản lý khóa dưới dạng plain text thủ công, những hoạt động đó cần phải được tham gia thực hiện và kiểm soát đọc lập từ  nhiều bên.

2.5.7. Ngăn chặn các hoạt động thay đổi khóa trái phép.

2.6. 	Cung cấp một cơ chế đảm bảo rằng bất cứ các khóa hoặc các chương trình mã hóa nào được lwuu trữ trong ứng dụng thanh toán đều không thể phục hội được, dựa trên các tiêu chuẩn áp dụng cho doanh nghiệp. 

Những khóa này là những khóa được dùng để mã hóa hoặc xác thực dữ liệu thẻ.

Ghi chú: Yêu cầu này chỉ dành cho các ứng dụng - hoặc các phiên bản trước đó của ứng dụng - có sử dụng khóa để mã hóa dữ liệu thẻ.

###<a id="req3"/>Yêu cầu 3. Cung cấp các tính năng xác thực an toàn###

3.1.	Ứng dụng thanh toán phải hỗ trợ  và bắt buộc việc sử dụng Unique User ID và phải bảo mật việc xcas thực cho tất cả các tác vụ truy cập dưới quyền quản trị, hoặc tất cả các truy cập vào dữ liệu thẻ. Việc xác thực an toàn bắt buộc phải được áp dụng cho tất cả các tài khoản được tạo ra, hoặc được quản lý bởi úng dụng, hoặc được tạo ra khi cài đặt hoàn tất, hoặc các thay đổi sau cài đặt

Chi chú: Khái niệm "Các thay đổi sau cài đặt" ở trong yêu cầu 3 được mô tả là tất cả các thay đổi của ứng dụng mà dẫn đến việc tài khoản người dùng bị khôi phục về các cấu hình mặc định, thay đổi các cấu hình của tài khoản đang tồn tại, các thay đổi tạo ra các tài khoản mới, hoặc là tạo mới lại các tài khoản đang tồn tại

Ứng dụng phải thực hiện các phần từ 3.1.1 đến 3.1.11 dưới đây

3.1.1. Ứng dụng thanh toán không sử dụng (hoặc không yêu cầu sử dụng) tài khoản admin mặc định ở các phần mềm liên quan khác (ví dụ, ứng dụng thanh toán không được sử dụng tài khoản admin của hệ thống database)

*Yêu cầu này gắn liền với phần 2.1 tỏng PCI DSDS.

3.1.2. Ứng dụng phải bắt buộc thay đổi tất cả các mật khẩu mặc định của tất cả các tài khoản được tạo ra và quản lý bởi ứng dụng, hay sau khi quá trình cài đặt kết thú, hoặc các thay đổi sau cài đặt.

Điều này áp dụng cho tất cả các loại tài khoản, bao gồm cả tài khoản user, tài khoản của ứng dụng và các dịch vụ, tài khoản được sử dụng bởi nhà cung cấp cho mục đích hỗ trợ kĩ thuật .

Ghi chú: Ngay sau quá trình cài đặt và các thay đổi sau cài đặt, ứng dụng phải có cơ chế ngăn chặn toàn bộ việc sử dụng các tài khoản built in cho đến khi mật khẩu mặc định được thay đổi

3.1.3. ứng dụng thanh toán tiến hành tạo ID riêng biệt và duy nhất cho từng tài khoản người dùng.

*Yêu cầu này gắn liền với phần 8.1. trong PCI DSS*.

3.1.4 Ứng dụng thanh toán phải có ít nhật một trong số các phương pháp dưới đây để thực hiện xác thực cho tất cả người dùng:

- 	Các thông tin người dùng biết, ví dụ như mật khẩu

-	Các thông tin người dừng sở hữu, ví dụ như thiết bị tạo token, hoặc smart card

-	Các thông tin mô tả người dùng, ví dụ như các thông tin cá nhân

*Yêu cầu này gắn liền với phần 8.2 trong PCI DSS*

3.1.5. Ứng dụng thanh toán không yêu cầu sử dụng các nhóm tài khoản, hay các tài khoản dùng chung, các tên tài khoản và mật khẩu phổ biến

*Yêu cầu này gắn liền với phần 8.5 trong PCI DSS*

3.1.6. Ứng dụng thanh toán yêu cầu mật khẩu phải đáp ứng những điều kiện sau:

- Yêu cầu độ dài ít nhất 7 kí tự

- Bao gồm cả kí tự chữ và số

Hoặc là, ít nhất phải yêu cầu mật khẩu phải có độ phức tạp và độ mạnh tương đương với các yêu cầu kể trên,

3.1.7. Ứng dụng thanh toán yêu cầu người dùng phải thay đổi mật khẩu ít nhất 90 ngày 1 lần.
*Yêu cầu này gắn liền với phần 8.2.4 trong PCI DSS*,

3.1.8. Ứng dụng thanh toán lưu giữ lịch sử đặt mật khẩu và yêu cầu rằng mật khẩu mới phải khác so với bất kì 1 trong 4 mật khẩu được sử dụng gần nhất.

*Yêu cầu này gắn liền với phần 8.2.5 trong PCI DSS*.

3.1.9. Ứng ựng thanh toán giới hạn số lần truy cập bằng cách khóa tài khoản người dùng nếu như xác thực thất bại sau không quá 6 lần liên tiếp

Yêu cầu nay gắn liền với phần 8.1.6 trong PCI DSS*.

3.1.10. Ứng dụng thanh toán có xác định thời gian khóa tối thiểu là 30 phút hoặc cho đến khi nguwofi quản trị mở khóa cho User ID.

*Yêu cầu này gắn liền với phần 8.1.7 trong PCI DSS*.

3.1.11. Trong phiên làm việc của ứng dụng thanh toán, nếu như không có thao tác nào xảy ra trong nhiều hơn 15 phút, ứng dụng tự động yêu cầu người dùng phải xác thực lại để tái kích hoạt phiên làm việc.

*Yêu cầu này gắn liền với phần 8.1.8 trong PCI DSS*.

3.2.	Nhà phát triển phần mêm phải cung cấp hướng dẫn cho khách hàng về việc tất cả các truy cập đến PC, server, database bằng ứng dụng thanh toán phải yêu cầu một unique user ID và các bước xác thực an toàn

*Yêu cầu này gắn liền với phần 8.1 và 8.2 trong PCI DSS*.

3.3.	Bảo vệ tất cả các mật khẩu trong ứng dụng thanh toán )bao gồm cả mật khẩu người dùng và mật khẩu ứng dụng), trong quá trình truyền tải và lưu trữ.

*Yêu cầu này gắn liền với phần 8.2.1 trong PCI DSS*.

3.3.1. Sử dụng các thuật toán mã hóa mạnh để mã hoắ mật khẩu, khiến chúng không thể bị đọc được trong suốt quá trình truyền tải.

3.3.2. Sử dụng một phương thuật toán mã hóa một chiều mạnh, dựa trên các tiêu chuẩn được công bố rộng rãi để mã hóa toàn bộ mật khẩu trong ứng dụng thanh toán khiến chúng không thể đọc được trong quá trình lưu trữ

Mỗi mật khẩu phải có một biến input đặc biệt được nối với mật khẩu trước khi áp dụng biện pháp mã hóa (salt).

Ghi chú: biến input không cần phải khó đoán được hoặc phải giữu bí mật.

.3.4.	Ứng dụng thanh toán phải giới hạn truy cập đến các tính năng/tài nguyên cần sử dụng, và phải bắt buocj có ít nhát các quyền hạn cho những tài khoản built-in:
- Mặc định, tất cả các ứng dụng, dịch vụ chỉ được phép truy cập đến những tính năng, dịch vụ được xác định là cần thiết cho hoạt động của ứng dụng, dịch vụ đó.

- Mặc định, tất cả các tải khoản ứng dụng, dịch vụ chỉ được cấp phép các quyền tối thiểu được gán cho từng loại tính năng, tài nguyên cần thiết cho hoạt động của ứng dụng, dịch vụ đó.

*Yêu cầu này gắn liền với phần 7 trong PCI DSS*.

###<a id="req4"/>Yêu cầu 4. Ghi log hoạt động của ứng dụng thanh toán###

4.1.	Ngay sau khi hoàn thành cài đặt, trạng thái mặc định của ứng dụng được cài đặt phải ghi log lại toàn bộ các truy cập của người dùng và có thể đưa la mối liên kết tất cả các hoạt động với từng cá nhân riêng lẻ.

*Yêu cầu này gắn liền với phần 10.1 trong PCI DSS*.

4.2.	Ứng dụng thanh toán phải cung cấp một quá trình kiểm tra tự động để tái cấu trúc lại những sự kiện dưới đây:

4.2.1. Tất cả những cá nhân độc lập truy cập đến dữ liệu thẻ của họ từ ứng dụng

4.2.2.	Tất cả những hành động được thực hiện bởi các cá nhân có quyền quản trị được gán trong ứng dụng.

4.2.3.	Các truy cập đến quá trình kiểm tra được quản lý bởi ứng dụng hay được thực hiện bởi chính ứng dụng đó.

4.2.4. Các truy cập truy cập không hợp lệ

4.2.5. Việc sử dụng, hoặc thay đổi đến phương pháp định danh và xác thực của ứng dung, bao goomf cả việc tạo lập các tài khoản mới, cố gắng chiếm quyền,..., và tất cả các thay đổi, thêm, sửa, xóa đến các tài khoản trong ứng dụng bằng quyền root hoặc quyền quản trị.

4.2.6. Việc khởi tạo, dừng, hoặc tạm dừng việc ghi log quá trình kiểm tra của ứng dụng.

4.2.7. Việc tạo mới hoặc xóa các đối tượng ở system-level, ngay trong ứng dụng, hoặc được thực hiện bởi ứng dụng.

4.3.	Ứng dụng thanh toán phải ghi lại ít nhất các dề mục kiểm tra sau, đối với mỗi sự kiện:
*Yêu cầu này gắn liền với phần 10.3 trong PCI DSS*.

4.3.1. ĐỊnh danh người dùng

4.3.2. Loại sự kiện

4.3.3. Thời gian

4.3.4. Kết quả của thao tác (thành công hay thất bại).

4.3.5. Mô tả sự kiện

4.3.6. Định danh hoặc tên của những dữ liệu, thành phần hệ thống, tài nguyên bị ảnh hưởng.

4.4. Ứng dụng thanh toán phải tương thích với công việc ghi log tập trung

Ghi chú: Ví dụ về tính năng này có thể bao gồm việc :

- Ghi log thông qua các chuẩn chung về log file. như Commom Log File System (CLFS, syslog, delimited text, vv...

- Cung cấp tinh năng và tài liệu để thực hiện chuyển đôi định dạng log của ứng dụng thành định dạng log chuẩn, phù hợp cho các tác vụ ghi log tập trung.

*Yêu cầu này gắn liền với phần 10.5.3 trong PCI DSS*.

###<a id="req5"/>Yêu cầu 5: Phát triển các ứng dụng thanh toán an toàn###

5.1.	Nhà phát triển ứng dụng cần xác định và triển khai một quá trình để đảm bảo an toàn cho quá trình phát triển ứng dụng thanh toán, bao gồm:

- Ứng dụng thanh toán được phát triển để tương thích với  chuẩn PCI DSS và PA DSS (ví dụ, xác thực an toàn và ghi log).

- Quá trình phát triển phải dựa trên các tiêu chuẩn dành cho doanh nghiệp.

- An toàn thông tin phải đi kèm theo suốt quá trình phát triển ứng dụng

- Phải luôn có quá trình rà soát kiểm tra về mặt bảo mật trong quá trình release ứng dụng hoặc cập nhật phiên bản ứng dụng.

*Yêu cầu này gắn liền với phần 6.3 trong PCI DSS*.

5.1.1. Các PAN thật không được dùng trong quá trình phát triển hoặc kiểm thử.

*Yêu cầu này gắn liền với phần 6.4.3 trong PCI DSS*. 

5.1.2. Dữ liệu và các tài khoản dùng thử đều phải được xóa bỏ trước khi release cho khách hàng

*Yêu cầu này gắn liền với phần 6.4.4 trong PCI DSS*.

5.1.3. Các tài khoản, User ID, mật khẩu tùy chọn trong ứng dụng thanh toán đều phải bị loạt bỏ trước khi release cho khách hàng.

*Yêu cầu này gắn liền với phần 6.3.1 trong PCI DSS*.

5.1.4. Code của ứng dụng thanh toán phải được review lại trước khi release cho khách hàng, nếu như có bất kì sự thay đổi quan trọng nào, để xác định bất cứ những rủi ro về code nào (kiểm tra bằng cách thủ công hoặc tự động), để đảm bảo được ít nhất: 
- Việc xem xét các thay đổi về code phải được thực hiện bởi một đơn vị độc lập, chứ không phảido người viết code. và đơn vị thực hiện xem xét code phải có kiến thức về code review và kinh nghiệm về secure coding.

- Code review để đảm bảo được code được viết dựa theo các hướng dẫn về Secure Coding (xem yêu cầu 5.2).

- Các phần sửa lỗi phải được áp dụng ngay rồi mới release.

- Kết của của việc review code cũng phải được xem xét và chấp thuận bởi nhà quản lý rồi mwosi được phép release sản phẩm.

- Biên bản của kết quả review code có bao gồm xác nhận từ cấp quản lý, thông tin về tác giả của code, người review, những chỉnh sửa đã được áp dụng, trước khi release.

Ghi chú: Yêu cầu về code review này áp dụng cho tất cả các thành phần của ứng dụng thanh toán (cả các ứng dụng nội bộ và các ứng dụng web được công khai( cũng như một phần của quá trình phát triển hệ thống. Phần code review có thể được tiến hành bởi những đơn vị có kinh nghiệm ngay trong tổ chức, hoặc các bên thứ 3.

*Yêu cầu này gắn liền với phần 6.3.2 trong PCI DSS*.

5.1.5. Áp dụng các phương pháp quản lý mã nguồn an toàn (secure source-control) để đảm bảo tính toàn vẹn của mã nguồn trong quá trình phát triển.

5.1.6. Ứng dụng thanh toán được phát triển dựa trên các test case thực tế được áp dụng cho doanh nghiệp về kĩ thuật secure coding, bao gồm:

- Phát triển ứng dụng yêu cầu ít quyền hạn về môi trường thực thi

- Phát triên ứng dụng mặc định theo nguyên lý fail-safe( tất cả các tác vụ mặc định đều phải bị disable noại trừ các tác vụ được xác định từ đầu trong quá trình thiết kế).

- Phát triển ứng dụng để đảm bảo việc xử lý truy cập từ nhiều nguồn, bao gồm cả các thao tác input lạ như multi-channel input.

5.1.6.1. Các kĩ thuật viết code bao gồm việc mô tả cách xử lý PAN hoặc SAD trong bộ nhớ.

5.1.7. Cung cấp các khóa đào tạo về secure coding và phát phát triển sản phẩm an toàn cho các developer ít nhất mỗi năm một lần, cũng như các nội dung phù hợp với công việc của developer và các công nghê được sử dụng, ví dụ:

- Thiết kế ứng dụng an toàn

- Các kĩ thuật secure coding để phòng tránh các điểm yếu code phổ biến (ví dụ, hướng dẫn của nhà cung cấp, OWASP Top 10, SANS CWE Top 25, CERT Secure Coding, vv...)

- Cách xử lý các dữ liệu quan trọng trong bộ nhớ.

- Review Code

- Các kĩ thuật kiểm tra bảo mật (ví dụ, các kĩ thuật pentest)

- Các kí thuật đánh giá rủi ro.

Ghi chú: Việc đào tạo cho developer có thể được thực hiện bởi nguồn lực lộ bộ, hoặc là các bên thứ 3.

5.1.7.1.  Luôn luôn thực hiện việc cập nhật các chương trình đào tạo mới để phù hợp với các công nghệ và các phương pháp phát triển mới.

5.2. Phát triển tất cả các ứng dụng thanh toán phải phòng chống được các điểm yếu về code phổ biến trong quy trình phát triển phần mềm.

*Yêu cầu này gắn liền với phần 6.5 trong PCI DSS*

Ghi chú, các yêu cầu từ 5.2.1 đến 5.2.6 dưới đây, áp dung cho tất cả các dạng ứng dụng (kể cả ứng dụng nội bộ lẫn ứng dụng công khai)

5.2.1.  Các kĩ thuật injection, phổ biến nhất là SQL Injection. Cũng cần quan tâm đến OS Command Injection, LDAP và XPath Injection, hoặc các phương pháp injection khác.

5.2.2. Buffer Overflow

5.2.3. Mất an toàn trong việc lưu trữ các dữ liệu mã hóa

5.2.4. Các kết nối/giao tiếp không an toàn

5.2.5. Error Handling/ Exception Handling không hợp lý

5.2.6. Tất cả các điểm yếu được liệt kê ở mức độ rủi ro cao, trong quy trình xác định điểm yếu ở Yêu cầu 7.1 trong PA DSS

Ghi chú: Các yêu cầu từ 5.2.7 đến 5.2.10 dưới đây, áp dụng cho các ứng dụng dựa trên nền web hoặc các giao diện của ứng dụng

5.2.7. Cross Site Scripting (XSS)

5.2.8. Các tác vụ quản lý truy cập (access control) không phù hợp vú dụ như tham chiếu trực tiếp các object không an toàn, không thể ngăn chặn việc truy cập URL, truy cập chồng chéo các thư mục.

5.2.9. Cross Site Request Forgery (CSRF)

5.2.10. Thất bại trong việc xác thực và quản lý session.

5.3.	Nhà phát triển ứng dụng phải  tuân theo quy trình quản lý các thay đổi, cho tất cả các thay đổi của ứng dụng. Quy trình quản lý thay đổi phải tuân thủ theo quy trình phát triển cũng như release sản phẩm (được định nghĩa trong Yêu cầu 5.1 của PA DSS). và bao gồm cả các phần sau (*Yêu cầu này gắn liền với phần 6.4.5 trong PA DSS):

5.3.1. Lập bản ghi chép về sự ảnh hưởng được tạo ra với các thay đổi được áp dụng. 

5.3.2.  Lập bản ghi chép về các thay đổi được chấp thuận bởi một đơn vị có thẩm quyền

5.3.3. Kiểm tra tính năng để đảm bảo rằng các thay đổi đó không gây ảnh hưởng gì đến việc bảo mật của toàn hệ thống.

5.3.4. Kiểm tra để đảm bảo rằng luôn luôn có sự chuẩn bị để khôi phục haotj động của ứng dụng đối với mối lần thay đổi. Ví dụ như, Nếu việc áp dụng các thy đổi thất bại, hoặc thay đổi gây ảnh hưởng đến các vấn đề bảo mật, thì ứng dụng đó phải có khả năng "rollback", quay trở về trạng thái ổn định trước đó.

5.4.	Nhà phát triển ứng dụng thanh toán phải thực hiện việc ghi chép và tuâ thủ theo một phương pháp đánh số phiên bản như là một phần của quá trình phát triển hệ thồng.. Phương pháp đánh số phiên bản này phải tuân theo quy trình trong phần PA DSS Program Guide và phải bao gồm tối thiểu là những yêu cầu dưới đây:
5.4.1.  Phương pháp đánh số phiên bản phải định nghieax được các thành phần cụ thể của phiên bản được sử dụng, như mô tả sau:

- Chi tiết về các thành phần trong một số phiên bản mẫu tuân theo các yêu cầu được liệt kê trong PA DSS Program Guide.

- Định dạng của số phiên bản, bao gồm số lượng các phần tử, các khoảng ngăn cách, các bộ kí tự, vv... (bao gồm các kí tự số, chứ và các kí tự đặc biệt).

- Định nghĩa của các phần tử được hiển thị trong số phiên bản (ví dụ, loại thay đổi, major version, minor version, maintenance release, kí tự viết tắt, vv...)

- Định nghĩa các phần tử đánh đấu việc sử dụng kí tự viết tắt.

5.4.2. Phương pháp đánh số phiên bản phải làm rõ được loại thay đổi và tầm ảnh hưởng của chúng trong ứng dụng, dựa trên PA DSS Program Guide, bao gồm:

- Mô tả tất cả các loại thay đổi và tầm ảnh hưởng của chúng trong ứng dụng. 

- Xác định củ thể và định nghĩa rõ ràng cho các thay đổi mà:

- Không làm thay đổi đến hoạt động của ứng dụng hoặc các thành phần liên quan

- Có ảnh hưởng đến hoạt động của ứng dụng nhưng không gây ảnh hưởng đến các vấn đề bảo mật và các yêu cầu của PA DSS

- Có ảnh hưởng đến các tính năng bảo mật hoặc các yêu cầu của PA DSS.

- Cách mà các loại thay đổi tác động đến số phiên bản.

5.4.3. Phương pháp đánh số phiên bản phải đặc biệt xác định được khi nào wldcard được sử dụng, và nếu được sử dụng thì sử dụng như thế nào. Cần phải có những yêu cầu sau đây:

- Chi tiết về cách sử dụng kí tự viết tắt trong phương pháp đánh số phiên bản

- Wild card không bao giờ được sử dụng cho bất cứ thay đổi nào mà gây ra ảnh hưởng đến các vấn đề bảo mật hoặc các yêu cầu PA DSS.

- Bất cứ phần tử nào của số phiên bản được sử dụng để biểu thị cho các thay đổi khong ảnh hưởng đến bảo mật (bao gồm các phần tử là kí tự viết tắt), không được phép sử dụng để biểu thị cho các thay đổi ảnh hưởng đến bảo mật.

- Các phần tử là kí tự viết tắt không được phép dừng để biểu thị cho các thay đổi ảnh hưởng đến bảo mật. Bất cứ một phần tử trong số phiên bản nào hiển thị ở phía sau một phần tử là kí tự viết tắt cũng không được phép dùng để biểu thị cho các thay đổi ảnh hưởng đến bảo mật.

5.4.4. Phương pháp đánh số phiên bản được công bố bởi nhà phát triển ứng dụng phải có mối liên hệ với khách hàng và các nhà tích hợp/ nhà phân phối.

5.4.5. Một vài nhà phát triển ứng dụng có thêm cả một phương pháp đánh số phiên bản khách được sử dụng nội bộ (phục vụ cho quá trình phát triển ứng dụng) khác với phương pháp được sử dụng trong quá trình release chính thức. Trong trường hợp này, thì cần phải có các tài liệu mô tả chi tiết cho những phương pháp đó, cũng như mối liên hệ giữa chúng.

5.4.6. Nhà phát triển ứng dụng phải có một quy trình để kiểm tra việc cập nhật ứng dụng để đảm bảo sự tương thích với phương pháp đánh số phiên bản trước khi release sản phẩm.

5.5.  Các kí thuật đánh giá rủi ro (ví dụ, lên danh sách các mối hiểm họa có thể gây ra cho ứng dụng), được sử dụng để xác định việc mất an toàn trong mô hình bảo mật được áp dụng hay các lỗ hổn hiện hữu xuyên suốt quá trình phát triển ứng dụng. Quy trình đánh giá rủi ro phải bao gồm những phần sau:

- Bao quát toàn bộ các tính năng của ứng dụng thanh toán, và không chỉ giới hạn lại các tính năng ảnh hưởng đến bảo mật, hay các tính năng đã được coi là tin cậy

- Đánh giá cách thức xử lý của ứng dụng, cơ chế hoạt động, cơ chế lưu trữ và xử lý dữ liệu,...

- Xác định các thành phần trong ứng dụng thanh toán mà có tương tác với PAN hoặc SAD hoặc môi trường dữ liệu thẻ. cũng như thất cả các thành phân tương tác từ bên ngoài với ứng dụng mà có thể dẫn tới việc thất thoát dữ liệu thẻ.

- Lập danh sách các mối đe dọa và các lỗ hổng hiện hữu thu thập được từ quá trình phân tích cơ chế xử lý dữ liệu thẻ, và đánh giá mức độ rủi ro (ví dụ, cao, trung bình, hay thấp) cho từng đối tượng tìm được.

- Cung cấp các phương pháp sửa lỗi và ngăn chặn sự cố xuyên suốt quá trình phát triển ứng dụng.

- Lập biên bản lại quá trình đánh giá rủi ro để nhà quản lý xem xét và chấp thuận.

5.6.	Nhà phát triển ứng dụng phải thực hiện một quy trình để lập tài liệu và xác minh cho phiên bản cuối cùng trước khi release, và tất cả các bản cập nhật sau đó của ứng dụng.

Tài liệu này bao gồm

- Chữ kí của các đơn vị có thẩm quyền để chấp thuận việc release ứng dụng hay release các bản cập nhật ứng dụng

- Xác nhận rằng nhà phát triển đã tuẩn thủ đúng quy trình an toàn khi phát triển ứng dụng.

###<a id="req6"/>Yêu cầu 6. Bảo vệ khi truyền tải qua mạng không dây###

6.1. Đối với các ứng dụng thanh toán sử dụng mạng không ddaaay, thay đổi các tất cả các thông số mặc định của nhà sản xuất cho các thiết bị mạng, bao gồm cả khóa mã hóa mặc định của mạng không dây, mật khẩu, SNMP Community String.

*Yêu cầu này gắn liền với phần 1.2.3 và 2.1.1 trong PCI DSS*.

6.2. Đối với các ứng dụng thanh toán sử dụng mạng khôn dây, các ứng dụng nhày phải tương thích với ác tiêu chuẩn dành cho doanh nghiệp (ví dụ IEEE 802.11i) để sử dụng các phương pháp mã hóa và xác thực mạnh trong quá trình truyền tải dữ liệu

Ghi chú: Không được phép sử dụng WEP

*Yêu cầu này gắn liền với phần 4.1.1 trong PCI DSS*.

6.3. Cung cấp các hướng dẫn cho khách hàng về việc sử dụng an toàn amngj không đây.

Ghi chú: Yêu cầu này áp dụng cho tất cả các ứng dụng được thiết kế để sử dụng trên đường mạng không dây.

*Yêu cầu này gắn liền với phần 1.2.3, 2.1.1, 4.1.1 trong PCI DSS*

###<a id="req7"/>Yêu cầu 7. Kiểm tra bảo mật cho các ứng dụng thanh toán và luôn duy trì cập nhật ứng dụng.###

7.1.	Nhà phát triển ứng dụng phải lập ra một quy trình để xác định và quản lý điểm yếu, theo các tiêu chí dưới đây (Ghi chú: tất cả các phần mềm hoặc hệ thống có liên quan (được cung cấp cùng ứng dụng thanh toán, hoặc được yêu cầu phải có khi vận hành ứng dụng thanh toán (ví dụ, web server, các thư viện và chương trình của bên thứ ba) đều nằm trong phạm vi của quy trình này)

7.1.1. Xác định các lỗ hổng bảo mật mới dựa trên các nguồn đáng tin cậy, hoặc là cập nhật các thông tin bảo mật.

7.1.2. Xếp hạng rủi ro cho tất cả các điểm yếu được tìm thấy, bao gồm tất cả các điểm yếu có trong tất cả các phần mềm hoặc hệ thống có liên quan (được cung cấp cùng ứng dụng thanh toán, hoặc được yêu cầu phải có khi vận hành ứng dụng thanh toán

7.1.3. Kiểm tra bảo mật cho ứng dụng thanh toán và cập nhật để sửa lỗi cho tất cả các điểm yếu đang tồn tại cho đến khi release.

7.2.	Nhà phát triển ứng dụng phải thiết lập một quy trình để định kì phát triển và áp dụng các bản vá bảo mật hoặc các bản nâng cấp.

7.2.1. Các bản vá và các bản cập nhật phải được cung cấp cho khách hàng theo một phương pháp an toàn, đáng tin cậy

7.2.2. Các bản vá và các bản cập nhật phải được cung cấp cho khách hàng theo một phương pháp đảm bảo sự toàn vẹn.

7.2.3. Cung cấp hướng dẫn cho khách hàng về việc cài đặt an toàn các bản vá và các bản cập nhật

7.3.	 Phải có phần "Release Note" cho tất cả các bản cập nhậ của ứng dụng, mô tả chi tiết và tác dụng của bản cập nhật, cũng như số phiên bản thay đổi như thế nào.

###<a id="req8"/>Yêu cầu 8. Tính tương thích với các mô hình mạng an toàn###

8.1. Ứng dụng thanh toán phải có thể triển khai được trong một mô hình mạng an toàn. Ứng dụng không gây xung đột với các thiết bị, ứng dụng, hoặc các cấu hình trong môi trường đang áp dụng chuẩn PCI DSS.

*Yêu cầu này gắn liền với phần 1,3,4,5,6 trong PCI DSS*.

8.2. Ứng dụng thanh toán chỉ được sử dụng các thành phần thực sự cần thiết cho việc hoạt động (dịch vụ, giao thức, tiến trình nền, các phần mềm và phần cứng liên quan, các thành phần khác), bao gồm cả những thành phần được cung cấp bởi bên thứ ba, nếu chúng được coi là an toàn. 

Ghi chú: SSL và các bản TLS cũ không được coi là các giao thức bảo mật an toàn. Ứng dụng thanh toán không được phép sử dụng hoặc hỗ trợ sử dụng SSL hoặc TLS phiên bản cũ. Ứng dụng cũng có sử dụng hoặc hỗ trợ sử dụng TLS thì không cho phép sử dụng SSL trong trường hợp failback.

*Yêu cầu này gắn liền với phần 2.2.3 trong PCI DSS*.

8.3. Ứng dụng thanh toán không được phép sử dụng các dịch vụ và sản phẩm có thể gây xung đột hoặc không tương thích với việc sử dụng các công nghệ xác thực nhiều bước.

Ghi chú: Xác thực nhiều bước yêu cầu phải có ít nhất từ 2 đến 3 cơ chế xác thực (xem ở dưới) được sử dụng cho việc xác thực. Sử dụng một phương pháp xác thực 2 lần (ví dụ, sử dụng 2 mật khẩu riêng biệt) không được coi là xác thực nhiều bước. Các phương pháp xác thực là:

- Các thông tin người dùng biết, ví dụ như mật khẩu

- Các thông tin người dừng sở hữu, ví dụ như thiết bị tạo token, hoặc smart card

- Các thông tin mô tả người dùng, ví dụ như các thông tin cá nhân

###<a id="req9"/>Yều cầu 9. Không lưu trữ dữ liệu thẻ  trên các server có kết nối internet###

9.1 	Bất cứ web server hoặc các thành phần phục vụ lưu trữ dữ liệu thẻ (ví dụ, database server) không được nằm chung trên 1 server, cũng như các thành phần phục vụ lưu trữ dữ liệu thẻ không được nằm chung vùng mạng với Webserver.

*Yêu cầu này gắn liền với phần 1.3.7 trong PCI DSS*.

###<a id="req10"/>Yêu cầu 10. Tính tương thích với các cơ chế truy cập từ xa an toàn đến ứng dụng thanh toán###

10.1.	Các phương pháp xác thực nhiều bước cần phải được áp dụng cho tất cả các truy cập từ xa đến ứng dụng thanh toán xuất phát từ các nguồn nằm ngoài không gian hoạt động của khách hàng. 

*Yêu cầu này gắn liền với phần 8.3 trong PCI DSS*.

10.2 	Tất cả các hoạt động truy cập từ xa đến ứng dụng thanh toán đều phải thwucj hiện một cách an toàn, dựa trên các tiêu chí dưới đây:

10.2.1. Nếu như các bản cập nhật cho ứng dụng thanh toán được phân phối bằng cách truy cập từ xa vào hệ thống khách hàng, nhà phát triển phẩn mềm phải nói với khách hàng rằng chỉ bật tính năng truy cập từ xa khi có yêu cầu từ nhà phát triển, và tắt đi ngay lập tức sau khi quá trình cập nhật kết thức.

Thay vào đó, nếu như phân phối các bản cập nhật thông qua VPN hoặc các kết nối tốc độ cao, thì nhà phát triển phần mềm phải khuyến nghị cho khách hàng để cấu hình firewall an toàn để bảo vệ cho các kết nối "Always On".

*Yêu cầu này gắn liền với phần 1 và 12.3.9 trong PCI DSS*.

10.2.2. Nếu như nhà phát triển hoặc đơn vị tích hợp/nhà bán lẻ có thể truy cập từ xa vào ứng dụng thanh toán của khách hàng,l thì một mã ác thực cá nhân đặc biệt (có thể là mật khẩu) cần phải được gán cho từng khách ahngf riêng biệt.

*Yêu cầu này gắn liền với phần 8.6.1 trong PCI DSS*.

10.2.3. Việc truy cập từ xa đến ứng dụng thanh toán của khách hàng bởi nhà phát triển hoặc đơn vị tích hợp/nhà bán lẻ, hoặc chính khcachs hàng, đều phải được thiết lập một cách an toàn, ví dụ:

- Thay đổi tất cả các tùy chỉnh mặc định ở chương trình tạo kết nối truy cập từ xa (ví dụ, thay đôi rmaatj khẩu mặc định và sử dụng một mật khẩu riêng biệt cho mỗi khách hàng)

- CHỉ cho phép kết nối từ những địa chỉ IP/MAC đã được xác định trước.

- Sử dụng các kiểu xác thực mạnh, và mật khẩu phức tạp cho quá trình đăng nhập (xem từ phần 3.1.1 đến 3.1.11 trong PA DSS)

- Bật các tính năng mã hóa dữ liệu khi truyền tải, dựa theo yêu cầu PA DSS 12.1.

- Tiến hành khóa tài khoản sau một số lần nhất định thực hiện đăng nhập thất bại. (Xem phần 3.1.1 đến 3.1.11 trong PA DSS).

- Thực hiện kết nối vào VPN thông qua một file firewall trước khi cho phép truy cập.

- Bật tính năng ghi log truy cập

- Giới hạn truy cập vào không gian riêng của khách hàng đối với từng cá nhân được cấp quyền.

*Yêu cầu này gắn liền với phần 2, 8, 10 trong PCI DSS*.

###<a id="req11"/>Yêu cầu 11. Mã hóa các traffic quan trọng khi truyền tải trên đường mạng công cộng###

11.1. 	Nếu như ứng dụng thanh toán có gửi, hoặc hỗ trợ gửi dữ liệu thẻ thông qua đường mạng công cộng, thì ứng dụng thanh toán phải hỗ trợ việc sử dụng các thuật toán mã hóa mạnh và các giao thức an toàn để bảo vệ cho các dữ liệu thẻ quan trong ctrong quá trình truyền tải qua các môi trường mạng công cộng, bao gồm tối thiểu các điều sau:

- Chỉ chấp nhận các trusted key và các trusted certificate.

- Giao thức được sử dụng chỉ hổ trợ các phiên bản và các cấu hình an toàn.

- Phải đảm bảo độ mạnh trong các phương pháp mã hóa được sử dụng

Ghi chú: SSL và các phiên bản TLS cũ không được coi là an toàn. Các ứng dụng thanh toán không được phép sử dụng hoặc hỗ trợ việc sử dụng SSL và các phiên bản TLS cũ. Các ứng dụng sử dụng TLS không được cho phép sử dụng SSL trong trường hợp failback.

Ví dụ về danh sách các mạng công cộng bao gồm:

- Mạng internet

- Các kết nối không dây, bao gồm acr WIfi 802.11 và Bluetooth

- Mạng di động, ví dụ: Mạng GSM hoặc CDMA

- GPRS/3G/4G,...

- Mạng dữ liệu truyền tải thông qua vệ tinh

*Yêu cầu này gắn liền với phần 4.1 trong PCI DSS*

11.2.	Nếu như ứng dụng thanh toán hỗ trợ việc gửi nhận PAN thông qua việc nhắn tin đến end-user (ví dụ, email, các dịch vụ instant messaging, chat), ứng dụng thanh toán phải cung cấp một giải pháp để khiến PAN không thể bị đọc được hoặc sử dụng một thuận toán mã hóa mạnh, hoặc phải chỉ định một thuật toán mã hóa mạnh để mã hóa PAN.

*Yêu cầu này gắn liền với phần 4.2 trong PCI DSS*

###<a id="req12"/>Yêu cầu 12. Bảo vệ tất cả các truy cập bằng quyền quản trị không sử dụng console###

12.1. 	Nếu ứng dụng thanh toán có hỗ trợ việc truy cập bằng quyền quản trị không sử dụng console, tiến hành mã háo tất cả các truy cập này bằng các phương pháp mã hóa mạnh

Ghi chú: Các giao thức dạng clear text như Telnet hay rlogin không được phép sử dụng trong các tác vụ truy cập bằng quyền quản trị

SSL và các phiên bản TLS cũ không được coi là các phương pháp mã hóa mạnh. Các ứng dụng thanh toán không được phép sử dụng, hoặc hỗ trợ sử dungjSSL hoặc các phiên bản TLS cũ. Ứng dụng có sử dụng TLS không được cho phép sử dụng SSL trong trường hợp failback.

*Yêu cầu này gắn liền với phần 2.3 trong PCI DSS*

12.1.1	Hướng dẫn khách hàng mã hóa toàn bộ các truy cập quản trị không sử dụng console bằng các phương pháp mã hóa mạnh, cho các ứng dụng quản lý dựa trên nền web hoặc các truy cập quản trị không sử dụng console khác.

Ghi chú: Các giao thức dạng clear text như  Telnet hay rlogin không được phép sử dụng trong các tác vụ truy cập bằng quyền quản trị.

*Yêu cầu này gắn liền với phần 2.3 trong PCI DSS*.

12.2.	Sử dụng phương pháp xác thực nhiều bước cho tất cả các cá nhân thực hiện truy cập quản trị không sử dụng console.

Ghi chú: Xác thực nhiều bước yêu cầu sử dụng ít nhất hai trên ba phương thwucs xác thực. (Xem Yêu cầu 3.1.4 để biết thêm về các phương pháp xác thực). 

*Yêu cầu này gắn liền với phần 8.3 trong PCI DSS*.

###<a id="req13"/>Yêu cầu 13. Tạo lập và duy trì bản hướng dẫn triên khai dịch vụ phù hợp với PA DSS cho khách hàng, nhà bán lẻ, hoặc đối tác tích hợp dịch vụ###

13.1. 	Phát triển, duy trì và phân phối một bản Hướng dẫn triển khai dịch vụ phù hợp với chuẩn PA DSS cho khách hàng, nhà bán lẻ, hoặc đối tác tích hợp dịch vụ, bao gồm đủ những yếu tố sau:

13.1.1. Cung cấp đẩy đủ các thông tin của ứng dụng cho khách hàng, nhà bán lẻ, hoặc đối tác tích hợp.

13.1.2. Liệt kê tất cả các yêu cầu trong tài liệu này, bất cứ khi nào bản Hướng dẫn triển khai được tham chiếu

13.1.3. Thực hiện đánh giá ít nhất mỗi năm một lần hoặc khi có thay đổi trên ứng dụng, hoặc thay đổi trên các yêu cầu PA DSS, tiến hành cập nhật tài liệu để đảm bảo rằng các biên bản đánh giá luôn được đồng bộ với những thay đổi làm ảnh hưởng đến ứng dụng, cũng như các yêu cầu được mô tả trong tài liệu này.

###<a id="req14"/>Yêu cầu 14. Giao trách nhiệm đảm bảo PA DSS cho cá nhân, duy trì chương trình đào tạo cho từng cá nhân, khách hàng, nhà bán lẻ, hoặc đối tác tích hợp###

14.1. Cung cấp các khóa đào tạo về an toàn thông tin và PA DSS cho các cá nhân chịu trách nhiệm đảm bảo PA DSS trong tổ chức của nhà phát triển ứng dụng, ít nhất một lần mỗi năm.

14.2. Gán quyền hạn và trách nhiệm cho từng cá nhân trong tổ chức của nhà phát triển ứng dụng, cho các tác vụ sau:

- Chịu trách nhiệm việc đảm bảo triển khai và đáp ứng đầy đủ tất cả các quy yêu cầu của PA DSS

- Đảm bảo cập nhật đầy đủ khi có thay đổi trong PCI DSS và PA DSS Program Guide

- Đảm bảo việc thực hiện secure coding luôn luôn được tuân thủ.

- Đảm bảo rằng các đối tác tích hợp/nhà bán lẻ luôn nhận được các chương trình đào tạo sử dụng, và các nguồn tài nguyên hỗ trợ khác (tài liệu, hỗ trợ trực tiếp,...).

- Đảm bảo rằng tất cả những cá nhân chịu trách nhiệm cho từng hạng mục trong quá trình triển khai PA DSS, bao gồm cả các developer, đều nhận được các khóa đào tạo kiến thức về PA DSS.

14.3. Phát triển, duy trì các chương trình đào tạo, chia sẻ kinh nghiệm cho các đối tác tích hợp và các nhà bán lẻ. Việc đào tạo phải bao gồm tối thiểu các nội dung dưới đây:

- Làm thế nào để triển khai sử dụng ứng dụng thanh toán và các hệ thống có liên quan khi muốn xây dựng hệ thống tương thích với PCI DSS.

- Bao hàm tất cả các tiêu chí được ghi lại trong phần Hướng dẫn chiển khai PA DSS xuyên suốt tài liệu này (và phần phụ lục A).

14.3.1. Tiến hành kiểm tra các chương trình, tài liệu đào tạo ít nhất mỗi năm một lần, cũng như khi có sự thay đổi ở ứng dụng, hoặc khi có sự thay đổi trong các tiêu chuẩn PA DSS.

Cập nhật các nguồn tài nguyên phục vụ việc đào tạo để luôn luôn giữ cho chúng luôn theo kịp với các phiên bản mới của ứng dụng thanh toán, cũng như các thay đổi trong bộ tiêu chuẩn PA DSS.

