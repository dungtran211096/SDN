# SOFTWARE DEFINED NETWORK
### Mục lục
[I. Mở đầu](#begin)

[II. Kiến trúc SDN](#architecture)
- [2.1 Tầng Data](#data)
- [2.2 Tầng Control](#control)
- [2.3 Tầng management](#mana)

[III. Ưu điểm và nhược điểm](#spot)
- [3.1 Sự khác nhau giữa mạng SDN so với mạng IP](#sdnvsip)
- [3.2 Ưu, nhươc điểm của mạng SDN](#compare)

[IV. Platform](#platform)
- [4.1 10 SDN platform](#example)
- [4.2 Opendaylight](#opendaylight)

==================================================

<a name="begin"></a>
## I. Mở đầu
  Mô hình mạng tăng nhanh một cách chóng mặt. Số người sử dụng internet tăng nhăng. Nhưng số lượng thiết bị kết nối internet còn tăng nhanh chóng mặt hơn cả thế vì do xu hướng *internet of thing*.

Sự cấp thiết về một công nghệ mạng mới  nâng cao tốc độ truyền tải mạng và dễ quản lí cấu hình, vì vậy SDN ra đời là cần thiết.

  Theo *Open Networking Foundation (ONF)* định nghĩa: SDN là kiến trúc mạng linh động, dễ dàng quản lý, hiệu quả về chi phí, có khả năng đáp ứng cao, lý tưởng cho các ứng dụng đòi hỏi băng thông lớn và có tính năng động cao.

Kiến trúc này tách biệt hai cơ chế đang tồn tại trong kiến trúc mạng hiện tại là cơ chế điều khiển (control plane) và cơ chế chuyển tiếp (data plane), cho phép phần điều khiển có khả năng lập trình được và hạ tầng bên dưới trở nên trừu tượng với các ứng dụng và các dịch vụ mạng. 

<img src=https://imgur.com/a/TtTNs>
