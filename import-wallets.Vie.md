# Nhập ví

MyTonCtrl có thể vận hành với nhiều loại hợp đồng ví khác nhau: wallet-v1, wallet-v3, [lockup-wallet](https://github.com/ton-blockchain/lockup-wallet-contract/tree/main/universal), vân vân...

Đôi khi đây thậm chí là cách đơn giản nhất để thực hiện với hợp đồng.

## Nhập bằng mã khóa riêng tư
Hãy cứ nhập vào console nếu bạn biết mã khóa riêng tư:
```
iw <wallet-addr> <wallet-secret-key>
```
`wallet-secret-key` ở đây là mã khóa riêng tư có định dạng base64

## Nhập bằng cụm từ khóa gợi nhớ
Nếu bạn biết cụm từ khóa gợi nhớ (gồm 24 chữ cái như `tattoo during ...`) thì làm như sau:
1) Cài đặt nodejs
2) Cài đặt https://github.com/ton-blockchain/mnemonic2key:
```
git clone https://github.com/ton-blockchain/mnemonic2key.git

cd mnemonic2key

npm install
```
3) Chạy `node index.js word1 word2 ... word24 [address]`, `word1`, `word2` ... ở đây là cụm từ khóa gợi nhớ của bạn và `address` là địa chỉ hợp đồng ví của bạn
4) Đoạn mã sẽ sinh ra `wallet.pk` và `wallet.addr`, hãy sửa tên của chúng thành `imported_wallet.pk` và `imported_wallet.addr`
5) Sao chép cả hai tệp vào `~/.local/share/mytoncore/wallets/`
6) Mở mytonctrl console và hiển thị danh sách ví bằng lệnh `wl`
7) Kiểm tra rằng ví đã được nhập và có số dư đúng đắn
8) Giờ bạn có thể gửi tiền bằng lệnh `mg` (Nhập `mg` để đọc tài liệu hỗ trợ)
