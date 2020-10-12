# Cách sử dụng Nmap

## 1. Giới thiệu về Nmap

Nmap (Network mapper) là một công cụ quét mạng mã nguồn mở và miễn phí. Dùng để khai thác thông tin mạng và kiếm tra bảo mật. Nmap được ưa chuộng bởi có nhiều phương pháp quét, độ tin cậy cao, tích hợp nhiều module và script giúp kiếm tra bảo mật

Nmap sử dụng những kỹ thuật set các cờ trong gói tin IP để xác định máy chủ nào có sẵn trên mạng, cũng như các dịch vụ nào đang mở hoặc đóng và hệ điều hành của máy chủ



## 2. Cài đặt Nmap

Nmap thường được cài đặt sẵn trên các distro Linux chuyên về bảo mật như Kali Linux,...

Nmap cung cấp giao diện dòng lệnh, người dùng có thể tải về và cài đặt Nmap trên các hệ điều khác như Ubuntu, Window, Centos 7...

  + Ubuntu
  ```
  sudo apt-get install nmap
  ```
  
  + Centos 7nmap
  ```
  yum install nmap
  ```
  
  + Window
  
   https://nmap.org/download.html
   
 Ngoài Nmap còn có Zenmap - giao diện đồ họa của Nmap. Giao diện Zenmap cung cấp cho người dùng nhiều tùy chọn quét khác nhau, khả năng lưu kết quả quả những lần scan và so sánh chúng. Xem bản đồ cấu trúc mạng cũng như các cổng đang chạy trên máy chủ...
 
![zenmap](https://user-images.githubusercontent.com/32956424/95675282-37b32800-0be0-11eb-8292-77dbf315cb22.png)
 
 Giao diện Zenmap

## 3. Một số lệnh và tham số cơ bản của Nmap

Một trong những mục đích của Nmap là tìm các host đang online. Thông thường khi kiểm tra 1 host có online hay không, lệnh **ping** sẽ được dùng. Tuy nhiên lệnh ping chỉ kiểm tra được 1 host. Nmap là khắc phục điều đó, quét được nhiều host và cung cấp nhiều tùy chọn hơn thông qua set các cờ

Nmap có thể quét 1 địa chỉ IP. VD:

```
nmap 192.168.10.1
```
hoặc một dải địa chỉ IP:
```
nmap 192.168.10.0/24
```

Nmape một khoảng địa chỉ IP:
```
nmap 192.168.10.1-20
```

Nmap có thể quét theo một list các địa chỉ IP có sẵn. VD
```
nmap -iL IP_List.txt
```



### Các tham số của lệnh Nmap

  + **-p**: quét 1 port cụ thể hoặc một khoảng các port. VD:
  
  Quét port 22: ``` nmap -p 22 192.168.10.1``` 
  
  Quét khoảng port 1 - 100: ```nmap -p 1-100 192.168.10.1```
  
  + **-F**: quét 100 port thông dụng nhất. VD: ```nmap -F 192.168.10.1```
  
  + **-p-**: quét 65535 port. VD: ```nmap -p- 192.168.10.1```
  
  + **-oN**: scan và lưu kết quả vào file. VD: ```nmap -oN output.txt -p- 192.168.10.1```

  + **-sn**: đơn giản là gửi gói tin ICMP Echo Request đến Receiver xem host có online hay không. VD: ```nmap -sn 192.168.10.1```  
  
  + **-O**: kiểm tra hệ điều hành của host. VD: ```nmap -O 192.168.10.1```
  
  + **-sT (TCP Full open scan)**: thực hiện kết nối bằng giao thức TCP tới Receiver với bắt tay 3 bước. Sender sẽ gửi gói tin SYN, nếu port mở thì Receiver sẽ trả lời bằng gói tin SYN + ACK. Khi đó Sender sẽ gửi tiếp gói tin ACK để duy trì kết nối. Nếu Receiver trả lời bằng gói tin RST, tức là port đóng. Nếu không trả lời, tức là gói tin đã bị lọc. Nếu trả về gói tin ICMP cũng bị coi là lọc
  
  + **-sS (TCP Half-open scan)**: cũng giống như Full open scan ở trên, nhưng thay vì Sender sẽ gửi gói tin ACK để duy trì kết nối, thì sẽ gửi gói tin RST để kết thúc kết nối luôn. Cơ chế phản hồi giống như Full open scan. Tuy nhiên cách scan này có thể qua mặt tường lửa hoặc tránh bị ghi lại
  
  + **Inverse TCP Flag scan**: là tên gọi các kỹ thuật scan như NULL Scan, XMAS Scan, FIN Scan... Sender sẽ gửi các gói tin TCP kèm các cờ đặc biệt, sự xuất hiện của các cờ này không đúng với kết nối thông thường, chủ yếu để thăm dò phản ứng của Receiver. Nếu Receiver phản hồi thì port mở hoặc port đã bị lọc. Nếu không phản hồi thì port đóng
    - **-sN (NULL Scan)**: gói tin này không mang cờ.
    - **-sF (FIN Scan)**: cờ FIN thường được dùng khi kết thúc kết nối TCP
    - **-sX (XMAS Scan)**: gói tin mang cả 3 cờ PSH, URG và FIN
    
  + **-sA (ACK Scan)**: Kỹ thuật scan này chủ yếu để thăm dò tường lửa. Sender gửi gói tin có cờ ACK để xem phản hồi của Receiver, nếu không phản hồi thì port đã bị lọc, nếu phản hồi là gói tin RST thì là port không bị lọc
  
  + **-sV**: quét các dịch vụ trên các port
  
  + **-sU (UDP Scan)**: Gửi đi gói tin UDP, nếu Receiver phản hồi lại gói tin UDP thì port mở. Nếu phản hồi là gói tin ICMP thì có thể port đóng hoặc bị lọc
  


## 4. Sử dụng Nmap để scan

