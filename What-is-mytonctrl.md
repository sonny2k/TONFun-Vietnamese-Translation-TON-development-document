## Nó là gì?
Console này bao gồm `fift`,`lite-client` và `validator-engine-console`. Nó được tạo ra để giúp thuận tiện hơn cho việc quản lý ví, miền và bên xác thực trên hệ điều hành Linux.

![](https://raw.githubusercontent.com/ton-blockchain/mytonctrl/master/screens/mytonctrl-status.png)

## Các chức năng
- [x] Hiển thị trạng thái của mạng TON
- [x] Quản lý các ví cục bộ
	- [x] Tạo ví cục bộ
	- [x] Kích hoạt ví cục bộ
	- [x] Hiển thị các ví cục bộ
	- [x] Nhập thông tin ví từ tệp (đuôi .pk)
	- [x] Lưu địa chỉ ví vào tệp (đuôi .addr)
	- [x] Xóa ví cục bộ
- [x] Hiển thị trạng thái tài khoản
	- [x] Hiển thị số dư tài khoản
	- [x] Hiển thị lịch sử của tài khoản
	- [x] Hiển thị trạng thái của tài khoản từ dấu trang
- [x] Chuyển tài sản tới ví
	- [x] Chuyển một khoảng cố định
	- [x] Chuyển toàn bộ (all)
	- [x] Chuyển toàn bộ và ngừng kích hoạt ví (alld)
	- [x] Chuyển tài sản tới ví trong dấu trang
	- [x] Chuyển tài sản tới ví qua một chuỗi các ví tự hủy
- [x] Quản lý dấu trang
	- [x] Thêm tài khoản vào dấu trang
	- [x] Hiển thị dấu trang
	- [x] Xóa dấu trang
- [x] Quản lý lời mời
	- [x] Hiển thị lời mời
	- [x] Biểu quyết cho đề xuất
	- [x] Biểu quyết tự động cho những đề xuất đã được biểu quyết trước đó
- [x] Quản lý miền
	- [x] Thuê miền mới
	- [x] Hiển thị miền đã thuê
	- [x] Hiển thị trạng thái miền
	- [x] Xóa miền
	- [ ] Gia hạn miền tự động
- [x] Điều khiển công cụ xác thực
	- [x] Tham gia vào quá trình tuyển cử của một công cụ xác thực
	- [x] Trả về thông tin cá cược + tiền thưởng
	- [x] Tự động chạy lại công cụ xác thực khi công cụ bị chấm dứt bất thường (systemd)
	- [x] Gửi thông kê xác thực tới https://toncenter.com

## Danh sách các hệ thống được chạy thử nghiệm
```
Ubuntu 16.04 LTS (Xenial Xerus) - Error: TON compilation error
Ubuntu 18.04 LTS (Bionic Beaver) - OK
Ubuntu 20.04 LTS (Focal Fossa) - OK
Debian 8 - Error: Unable to locate package libgsl-dev
Debian 9 - Error: TON compilation error
Debian 10 - OK
```

## Tổng quan về các đoạn mã cài đặt
- `toninstaller.sh`: Dùng để Tạo bản sao mã nguồn của `TON` và `mytonctrl` vào thư mục `/usr/src/ton` và `/usr/src/mytonctrl`, Biên dịch các chương trình và ghi chúng vào `/usr/bin/`.
- `mytoninstaller.py`: Dùng để cấu hình công cụ xác thực và `mytonctrl`; Sinh ra đoạn khóa kết nối cho công cụ xác thực.

## Các chế độ cài đặt
Có ha chế độ cài đặt: `lite` và `full`. Chúng đều **biên dịch** và cài đặt các thành phần của `TON`. Tuy nhiên bản `lite` không cấu hình hay chạy nút (node)/công cụ xác thực (validator).

## Cài đặt trên Ubuntu
1. Tải về và thực thi đoạn mã `install.sh` với chế độ cài đặt mà bạn mong muốn. Trong quá trình cài đặt, đoạn mã sẽ cần bạn cung cấp mật khẩu người dùng cao nhất (superuser) nhiều lần.
```sh
wget https://raw.githubusercontent.com/ton-blockchain/mytonctrl/master/scripts/install.sh
sudo bash install.sh -m <mode>
```

2. Đã xong. Giờ bạn có thể thử chạy `mytonctrl` console rồi đấy.
```sh
mytonctrl
```


## Cài đặt cho Debian
1. Tải về và thực thi đoạn mã `install.sh` với chế độ cài đặt mà bạn mong muốn. Trong quá trình cài đặt, đoạn mã sẽ cần bạn cung cấp mật khẩu người dùng cao nhất (superuser) nhiều lần.
```sh
wget https://raw.githubusercontent.com/ton-blockchain/mytonctrl/master/scripts/install.sh
su root -c 'bash install.sh -m <mode>'
```

2. Đã xong. Giờ bạn có thể thử chạy `mytonctrl` console rồi đấy.
```sh
mytonctrl
```

## Chẩn đoán dữ liệu từ xa
Lúc mặc định, `mytonctrl` gửi thống kê xác thực tới máy chủ https://toncenter.com.
Việc nhận diện những bất thường xảy ra trong mạng, cũng như nhanh chóng gửi phản hồi tới các lập trình viên là điều cần thiết.
Để tắt chẩn đoán dữ liệu từ xa trong lúc cài đặt, sử dụng cờ `-t`:
```sh
sudo bash install.sh -m <mode> -t
```

Để tắt chẩn đoán dữ liệu từ xa sau khi đã cài đặt, Làm như sau:
```sh
MyTonCtrl> set sendTelemetry false
```

## Khu vực quản lý cho web admin
Để điều khiển nút (node)/công cụ xác thực (validator) qua trình duyệt, bạn cần phải đặt thêm mô-đun:
`mytonctrl` -> `installer` -> `enable JR`

Kế tiếp, bạn phải tạo mật khẩu kết nối:
`mytonctrl` -> `installer` -> `setwebpass`

Đã sẵn sàng. Giờ bạn có thể truy cập https://tonadmin.org và đăng nhập với thông tin của bạn.
git: https://github.com/igroman787/mtc-jsonrpc

## Bản sao cục bộ cho toncenter
Để thiết lập một bản sao https://toncenter.com cục bộ trên máy chủ của bạn, hãy cài đặt thêm mô-đun:
`mytonctrl` ->` installer` -> `enable PT`

Đã sẵn sàng. Một bản sao cục bộ cho toncenter đang khả dụng tại `http://<server-ip-address>:8000`
git: https://github.com/igroman787/pytonv3

## Đường dẫn hữu ích
1. https://github.com/ton-blockchain/mytonctrl/blob/master/docs/en/manual-ubuntu.md
2. https://ton.org/docs/
