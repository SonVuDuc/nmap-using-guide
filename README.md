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

Nmap có thể quét 1 địa chỉ IP hoặc một dải địa chỉ IP. VD:

```
nmap 192.168.10.1
```
hoặc
```
nmap 192.168.10.0/24
```

Nmap có thể quét theo một list các địa chỉ IP có sẵn. VD
```
nmap -iL IP_List.txt
```

### Các tham số của lệnh Nmap

  + -sn: đơn giản là gửi gói tin ICMP Echo Request đến host xem host có online hay không. VD: ```nmap -sn 192.168.10.1```  
  
  + -O: kiểm tra hệ điều hành của host. VD: ```nmap -O 192.168.10.1```
  
  + -sT (TCP Connect scan): thực hiện kết nối bằng giao thức TCP tới host với bắt tay 3 bước. Máy người dùng sẽ gửi gói tin SYN, nếu port mở thì máy đích sẽ trả lời bằng gói tin SYN + ACK. Khi đó máy người dùng sẽ gửi tiếp gói tin ACK để duy trì kết nối. Nếu máy đích trả lời bằng gói tin RST, tức là port đóng. Nếu không trả lời, tức là gói tin đã bị lọc. Nếu trả về gói tin ICMP cũng bị coi là lọc
  
  + -

## 4. Sử dụng Nmap để scan

