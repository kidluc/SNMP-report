Báo cáo về SNMP
==========

I. Tìm hiểu về SNMP
- SNMP (Simple Network Management Protocol) là giao thức kiểm tra, thu thập thông tin từ nhiều hệ thống khác nhau bằng việc sử dụng giao thức UDP (giao thức không yêu cầu xác nhận hai chiều để tăng tốc độ truyền tải t hông tin), hỗ trợ vận hành các thiết bị đang sử dụng SNMP hoạt động một cách tối ưu, nhận thông tin cảnh báo mạng nếu có sự cố xảy ra.
- SNMP có 3 version là:
-- SNMP version 1 chuẩn của giao thức SNMP được định nghĩa trong RFC 1157 và là một chuẩn đầy đủ của IETF. Vấn đề bảo mật của SNMP v1 dựa trên nguyên tắc cộng đồng, không có nhiều password, chuổi văn bản thuần và cho phép bất kỳ một ứng dụng nào đó dựa trên SNMP có thể hiểu các hiểu các chuổi này để có thể truy cập vào các thiết bị quản lý. Có 3 tiêu chuẩn trong: read-only, read-write và trap
-- SNMP version 2: phiên bản này dựa trên các chuổi “community”. Do đó phiên bản này được gọi là SNMPv2c, được định nghĩa trong RFC 1905, 1906, 1907, và đây chỉ là bản thử nghiệm của IETF. Mạc dù chỉ là thử nghiệm nhưng nhiều nhà sản xuất đã đưa nó vào thực nghiệm.
-- SNMP version 3: là phiên bản tiếp theo được IETF đưa ra bản đầy đủ. Nó được khuyến nghị làm bản chuẩn, được định nghĩa trong RFC 1905, RFC 1906, RFC 1907, RFC 2571, RFC 2572, RFC 2573, RFC 2574 và RFC 2575. Nó hổ trợ các loại truyền thông riêng tư và có xác nhận giữa các thực thể.
- SNMP có 2 thành phần chính là:
-- SNMP Manager: Là máy tính chạy chương trình quản lý mạng cũng có thể được coi là một NMS (Network Management Station). Nhiệm vụ của SNMP Manager là truy vấn các agent và  xử lý thông tin nhận được từ agent.
-- SNMP Agent: Là chương trình chạy trên thiết bị mạng cần được quản lý. Nhiệm vụ của agent là thu thập thông tin của thiết bị và lưu trữ nó lại vào một database là "management information base **MIB** ". Nếu được manager yêu cầu thì agent sẽ gửi lại nhưng thông tin trong MIB lại cho SNMP Manager.
- SNMP Manager có 2 kiểu truy vấn dữ liệu từ SNMP Agent là:
-- Polling: SNMP Manager gửi các yêu cầu truy vấn thông tin đến agent qua port 161
-- Trapping: Agent sẽ gửi các thông tin cảnh báo đến cho SNMP Management System nếu có lỗi hoặc sự cố xảy ra.
- SNMP OID: hay Object identifiers là một định nghĩa tên của đối tượng.
 Tên thường ở 2 dạng: số hay các chữ có ý nghĩa nào đó về đối tượng. Trong dạng này hay dạng kia, tên thường khó nhớ hay bất tiện
 - SNMP MIB: là cơ sở dữ liệu dùng phục vụ cho Manager và Agent nhằm phục vụ việc truy vấn thông tin của manager.
- SNMP có các câu lệnh giao thức sau:
**snmpget** : SNMP Management gửi một GET message đến agent để yêu cầu một giá trị của OID. Câu lệnh này sẽ nhận được một RESPONSE message gồm các data mà agent đã lưu trữ trong MIB
**snmpgetnext**: SNMP Manager đưa ra một dãy các lệnh để lấy thông tin từ một nhóm trong MIB. Agent sẽ lần lượt trả lời tất cả các đối tượng có trong câu truy vấn của ”get-next” tương tự như ”get”, cho đến khi nào hết các đối tượng trong dãy
**snmpbulkget**: Câu lệnh này gửi đi một dãy các câu lệnh GETNEXT và nhận về lượng thông tin chứa nhiều dữ liệu nhất có thể mà gói thông tin cho phép.
**snmpset**: Câu lệnh này để thay đổi giá trị của một đối tượng hoặc thêm một hàng mới vào bảng. Đối tượng này cần phải được định nghĩa trong MIB là ”read-write” hay ”write-only”
**snmptrap**: SNMP agent gửi một *trap message* đến manager để thông báo tình trạng hiện có của thiết bị.
**snmpinform**: lệnh này để xác nhận đã nhận được gói trap mesager mà manager gửi trả về cho agent qua INFORM message nếu không agent sẽ tiếp tục gửi cho manager gói *Trap message*

II. Mô hình lab
![](imgs/20170919-145600.png)

III. Cài đặt cacti giám sát traffix.
Mô hình cài đặt
![](imgs/20170919-145942.png)

B1: Cài đặt LAMP và các gói package phụ trợ trên SNMP Manager

``` sudo apt-get install apache2 mysql-server-5.6 php5 libapache2-mod-php5 ```

B2: Cài đặt SNMP Agent trên các SNMP Managed Machine.
``` apt install snmp snmpd cacti-spine -y```

B3: Cài đặt cacti trên SNMP manager system


