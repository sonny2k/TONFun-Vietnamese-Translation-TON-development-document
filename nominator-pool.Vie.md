# Pool dành cho nhóm đề cử

## Khởi chạy công cụ xác thực (validator) trong chế độ pool dành cho nhóm đề cử

1. Chuẩn bị phần cứng cho công cụ xác thực - 8 nhân cpu, 64GB ram, ổ cứng SSD 1TB, Địa chỉ IP tĩnh, đường truyền mạng 1Gb/s.

   Để duy trì sự ổn định cho mạng, chúng tôi khuyến khích phân bổ các nút (nodes) xác thực ở những nơi khác nhau trên toàn cầu và không tập trung chúng vào chung một trung tâm dữ liệu.
   Sử dụng https://status.toncenter.com/ để xác định mật độ dày đặc (các nút) ở từng địa điểm. Dựa vào bản đồ, bạn có thể thấy
   các trung tâm dữ liệu có mức sử dụng cao nằm ở Châu Âu, Phần Lan, Đức và thủ đô Paris (Pháp). Vì thế, chúng tôi không khuyến khích sử dụng các bên cung cấp như Hetzner và OVH.

   > Phần cứng của bạn phải có cấu hình tương đương với cấu hình yêu cầu hoặc cao hơn. Đừng chạy công cụ xác thực trên phần cứng thiếu sức mạnh - điều này ảnh hưởng xấu đến mạng và bạn sẽ bị phạt.

   > Kể từ tháng 5 2021, Hetzner đã cấm hành vi đào trên các máy chủ của họ , hiện tại cả thuật toán PoW và PoS đều bị kiểm soát bởi quy tắc này. Việc cài đặt nút bị xem là vi phạm các điều kiện trong thỏa thuận.

   > **Các nhà cung cấp được khuyến nghị:** [amazon](https://aws.amazon.com/), [digitalocean](https://www.digitalocean.com/), [linode](https://www.linode.com/), [alibaba cloud](https://alibabacloud.com/), [latitude](https://www.latitude.sh/).

2. Cài đặt và đồng bộ **mytonctrl** như mô tả trong https://github.com/ton-blockchain/mytonctrl/blob/master/docs/en/manual-ubuntu.md **ở** đoạn 1, 2 và 3.

   [Video instruction](https://ton.org/docs/#/nodes/run-node).

3. Gửi 1 TON tới địa chỉ ví của công cụ xác thực được hiển thị trên danh sách `wl`.

4. Nhập `aw` để kích hoạt ví của công cụ xác thực.

5. Tạo 2 pool (Cho vòng xác thực chẵn và lẻ):
   ```
   new_pool p1 0 1 1000 300000
   new_pool p2 0 1 1001 300000
   ```
   với
    * `p1` là tên của pool;
    * `0` là tỉ lệ % thưởng cho công cụ xác thực (ví dụ: dùng 40 cho 40%);
    * `1` là tối đa đại diện đề cử trong pool (nên <= 40);
    * `1000` là số tiền cọc (stake) tối thiểu của công cụ xác thực (nên >= 1K TON);
    * `300000` là số tiền cọc (stake) tối thiểu của đại diện đề cử (nên >= 10K TON);

   > (!) Cấu hình cho pool không cần phải giống như trên, bạn có thể thêm 1 đơn vị vào tiền cọc của một pool nào đó để làm nó khác với số pool còn lại.

   > (!) Dùng https://tonmon.xyz/ để xác định tiền cọc tối thiểu của công cụ xác thực hiện tại là bao nhiêu.

6. Nhập `pools_list` để hiển thị địa chỉ các pool:

   ```
   pools_list
   Name  Status  Balance  Address
   p1    empty   0        0f98YhXA9wnr0d5XRXT-I2yH54nyQzn0tuAYC4FunT780qIT
   p2    empty   0        0f9qtmnzs2-PumMisKDmv6KNjNfOMDQG70mQdp-BcAhnV5jL
   ```

7. Gửi 1 TON đến mỗi pool và kích hoạt chúng:
   ```
   mg validator_wallet_001 0f98YhXA9wnr0d5XRXT-I2yH54nyQzn0tuAYC4FunT780qIT 1
   mg validator_wallet_001 0f9qtmnzs2-PumMisKDmv6KNjNfOMDQG70mQdp-BcAhnV5jL 1
   activate_pool p1
   activate_pool p2
   ```

8. Nhập `pools_list` để hiện thị các pool:
   ```
   pools_list
   Name  Status  Balance      Address
   p1    active  0.731199733  kf98YhXA9wnr0d5XRXT-I2yH54nyQzn0tuAYC4FunT780v_W
   p2    active  0.731199806  kf9qtmnzs2-PumMisKDmv6KNjNfOMDQG70mQdp-BcAhnV8UO
   ```

9. Mở từng pool qua đường dẫn sau "https://tonscan.org/nominator/<địa_chỉ_của_pool>" và xác minh cấu hình của pool.

10. Gửi tiền từ công cụ xác thực đến từng pool:
    ```
    deposit_to_pool validator_wallet_001 <address_of_pool_1> 1005
    deposit_to_pool validator_wallet_001 <address_of_pool_2> 1005
    ```
    với `1005` là số lượng TON cần gửi. Xin lưu ý rằng 1 TON sẽ được ghi nợ bởi pool cho việc xử lý việc gửi tiền.


11. Gửi tiền từ đại diện đề cử đến từng pool:

    Đi tới đường dẫn của pool (**bước 9**) và nhấp **ADD STAKE**.
    Bạn cũng có thể gửi tiền bằng cách sử dụng **mytonctrl**, Dùng các lệnh dưới đây để thực hiện.

    ```
    mg nominator_wallet_001 <address_of_pool_1> 300001 -C d
    mg nominator_wallet_001 <address_of_pool_2> 300001 -C d
    ```

    > (!) Ví của đại diện đề cử phải được khởi tạo ở chuỗi chính basechain (chuỗi làm việc 0 - workchain 0).

    > (!) Hãy nhớ là ví của công cụ xác thực và ví của đại diện đề cử phải được lưu tách biệt nhau! Ví của công cụ xác thực được lưu trên máy chủ cùng với nút xác thực, để đảm bảo việc xử lý của tất cả giao dịch hệ thống. Ví đại diện đề cử thì được lưu trong ví lạnh của bạn.

    > Để rút lại tiền cọc của đại diện đề cử, gửi một giao dịch với dòng chú giải `w` đến địa chỉ của pool (phải kèm theo 1 TON cho việc xử lý giao dịch). Bạn cũng có thể làm điều này với **mytonctrl**.

13. Kích hoạt chế độ pool:
    ```
    set usePool true
    ```

14. Mời nhóm đề cử khác gửi tiền vào các pool của bạn. Tham gia vào xác thực sẽ tự động diễn ra.
    > (!) Bạn cần có ít nhất 200 TON/tháng trong ví của công cụ xác thực để trả phí hoạt động.

## Cấu hình pool

Nếu bạn muốn tự cho vay thì hãy dùng `new_pool p1 0 1 1000 300000` (tối đa 1 đại diện đề cử, 0% chia thưởng cho công cụ xác thực).

Nếu bạn muốn tạo pool cho nhiều đại diện đề cử thì hãy dùng như sau: `new_pool p1 40 40 10000 10000` (tối đa 40 đại diện đề cử, 40% chia thưởng cho công cụ xác thực, tiền cọc của người tham gia tối thiểu là 10K TON).

## Chuyển đổi công cụ xác thực thường sang chế độ pool cho đại diện đề cử

1. Nhập `set stake 0` để tắt quyền tham gia vào các cuộc tuyển cử.

2. Đợi hai phần tiền cọc được trả về từ cử tri.

3. Hoàn thành các bước trong phần "Khởi chạy công cụ xác thực (validator) trong chế độ pool dành cho nhóm đề cử" bắt đầu từ bước **4th**.
