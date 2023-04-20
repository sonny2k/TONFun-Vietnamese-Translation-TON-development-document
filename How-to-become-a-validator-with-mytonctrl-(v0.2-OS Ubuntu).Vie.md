# Làm thế nào để trở thành đại diện xác thực (validator) với mytonctrl (phiên bản 0.2, Hệ điều hành Ubuntu)

### 1. Cài đặt mytonctrl:
1. Tải về mã cài đặt. Chúng tôi khuyến nghị cài đặt công cụ này dưới quyền người dùng cục bộ, không nên dưới quyền người dùng Root. Ví dụ của chúng tôi sử dụng một tài khoản người dùng cục bộ:

```sh
wget https://raw.githubusercontent.com/ton-blockchain/mytonctrl/master/scripts/install.sh
```

![wget output](https://raw.githubusercontent.com/ton-blockchain/mytonctrl/master/screens/manual-ubuntu_wget-ls_ru.png)

2. Khởi chạy mã cài đặt với quyền quản trị viên:

```sh
sudo bash install.sh -m full
```


### 2. Kiểm tra khả năng vận hành:
1. Chạy **mytonctrl** từ tài khoản người dùng cục bộ cho việc cài đặt ở bước 1:

```sh
mytonctrl
```

2. Kiểm tra trạng thái **mytonctrl**, cho từng trường hợp cụ thể sau:

* **mytoncore status**: hiện màu xanh lá.
* **Local validator status**: hiện màu xanh lá.
* **Local validator out of sync**. Ban đầu sẽ xuất hiện một số lớn. Khi công cụ xác thực vừa tạo liên lạc với những công cụ xác thực khác, con số ban nãy sẽ vòng quay đâu đó 250k. Khi sự đồng bộ tiếp tục diễn ra, con số sẽ hạ xuống. Khi số này rơi về dưới 20, công cụ xác thực đã được đồng bộ.

![status](https://raw.githubusercontent.com/ton-blockchain/mytonctrl/master/screens/mytonctrl-status.png)

3. Hãy nhìn vào danh sách các ví đang khả dụng. Trong ví dụ của chúng tôi, ví **validator_wallet_001** được tạo trong quá trình cài đặt **mytonctrl**:

![wallet list](https://raw.githubusercontent.com/ton-blockchain/mytonctrl/master/screens/manual-ubuntu_mytonctrl-wl_ru.png)


### 3. Gửi số lượng đồng coin bắt buộc tới ví và kích hoạt nó:
Đi tới **tonmon.xyz** > **Participant stakes** và kiểm tra xem số lượng đồng coin tối thiểu để tham gia vào một vòng tuyển cử là bao nhiêu.

* Lệnh `vas` giúp hiển thị lịch sử chuyển tiền
* Lệnh `aw` giúp kích hoạt ví

![account history](https://raw.githubusercontent.com/ton-blockchain/mytonctrl/master/screens/manual-ubuntu_mytonctrl-vas-aw_ru.png)


### 4. Giờ thì công cụ xác thực của bạn đã đủ điều kiện hoạt động
**mytoncore** sẽ tự động gia nhập vào cuộc tuyển cử. Nó chia số dư ví làm hai phần và sử dụng chúng như sự đánh cược để tham gia vào các cuộc tuyển cử. Bạn cũng có thể tự chỉnh khối lượng tiền cọc (stake):

`set stake 50000` — chỉnh khối lượng cọc lên 50k đồng coin. Nếu tiền cược được chấp nhận và nút (node) của chúng ta trở thành công cụ xác thực thì tiền cược này chỉ có thể được rút vào lần tuyển cử thứ hai (căn cứ vào điều lệ của toàn bộ cử tri).

![setting stake](https://raw.githubusercontent.com/ton-blockchain/mytonctrl/master/screens/manual-ubuntu_mytonctrl-set_ru.png)

Hãy tự do dùng lệnh help nếu bạn gặp bất kỳ khúc mắc gì.

Để kiểm tra lịch sử ghi chép (logs) của **mytoncrl**, mở `~/.local/share/mytoncore/mytoncore.log` cho tài khoản người dùng cục bộ hoặc `/usr/local/bin/mytoncore/mytoncore.log` cho tài khoản người dùng Root.

![logs](https://raw.githubusercontent.com/ton-blockchain/mytonctrl/master/screens/manual-ubuntu_mytoncore-log.png)
