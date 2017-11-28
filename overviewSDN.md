# SOFTWARE DEFINED NETWORK
### Mục lục
[I. Mở đầu](#begin)
- [1.1 Giới thiệu](#introduce)
- [1.2 Mục đích](#intention)

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
<a name="introduce"></a>
### 1.1 Giới thiệu
  Mô hình mạng tăng nhanh một cách chóng mặt. Số người sử dụng internet tăng nhăng. Nhưng số lượng thiết bị kết nối internet còn tăng nhanh chóng mặt hơn cả thế vì do xu hướng *internet of thing*.

Sự cấp thiết về một công nghệ mạng mới  nâng cao tốc độ truyền tải mạng và dễ quản lí cấu hình, vì vậy SDN ra đời là cần thiết.

  Theo *Open Networking Foundation (ONF)* định nghĩa: SDN là kiến trúc mạng linh động, dễ dàng quản lý, hiệu quả về chi phí, có khả năng đáp ứng cao, lý tưởng cho các ứng dụng đòi hỏi băng thông lớn và có tính năng động cao.

Kiến trúc này tách biệt hai cơ chế đang tồn tại trong kiến trúc mạng hiện tại là cơ chế điều khiển (control plane) và cơ chế chuyển tiếp (data plane), cho phép phần điều khiển có khả năng lập trình được và hạ tầng bên dưới trở nên trừu tượng với các ứng dụng và các dịch vụ mạng. 

<img src=https://i.imgur.com/j5ZcoIA.png>

<a name="intention"></a>

### 1.2 Mục đích
SDN dừng sự tích hợp theo chiều dọc bằng cách chia thành phần control plane và data plane. Điều này làm cho các switch trở thành thiết bị chuyển tiếp đơn giản hơn và được cài đăt trong logically centralized controller. Điều này làm tăng tốc độ mạng. Nhờ chia thành 2 phần như vậy dễ quản lý và cấu hình tập trung. Tiết kiệm công sức và thời gian rất nhiều. 

Tập trung hóa điều khiển trong môi trường nhiều nhà cung cấp thiết bị: phần mềm điều khiển SDN có thể điều khiển bất kì thiết bị nào cho phép OpenFLow từ bất cứ nhà cung cấp nào. ( bao gồm switch, router, và các switch ảo)

Giảm sự phức tạp thông qua việc tự động hóa: kiến trúc SDN cung cấp một framework : OpenFlow quản lý mạng tự động và linh hoạt. Từ framework này có thể phát triển các công cụ tư động hóa các nhiệm vụ hiện đang được thực hiện bằng tay.

Gia tăng độ tin cậy và khả năng an ninh mạng.

Khái niệm SDN đặt ra 2 vấn đề khi triển khai thực tế: Cần phần có một kiến trúc logic chung cho tất cả các switch, router và các thiết bị mạng khác được quản lý bởi SDN Controller. Kiến trúc này có thể được triển khai bằng nhiều cách khác nhau trên các thiết bị của các nhà cung cấp khác nhau và phụ thuộc vào nhiều loại thiết bị mạng, miễn là SDN controller thấy được chức năng chuyển mạch thống nhất. Một giao thức chuẩn, bảo mật để giao tiếp giữa SDN controller và các thiết bị mạng như switch hay router mạng.

<a name="architecture"></a>
## II. Kiến trúc SDN
<img src=https://i.imgur.com/RhZmJ8Y.png>

<a name="data"></a>
### 2.1 Tầng data
Tầng Data là tầng thấp nhất trong mô hình SDN. Tầng Data bao gồm hai lớp:

- **Network infrastructure (NF)** : là lớp dưới cùng của tầng data. NF bao gồm các thiết bị chuyển tiếp. Các thiết bị này có thể là hardware switch hoặc software switch. Điều này phụ thuộc vào mục đích của chuyển tiếp gói tin.
- **Southbound interface (SI)** : là lớp dùng để giao tiếp giữa tầng control và tầng data. Các thông tin cần được truyền đi giữa 2 tầng trên gồm:<ul><li>Lệnh xử lý gói tin</li>
  <li>Thông báo các gói tin đến trên các node mạng.</li>
  <li>Thông báo các trạng thái thay đổi. Vd. Các liên kết đi lên hoặc đi xuống.</li>
  <li>Cung cấp thông tin thống kê. Vd. Bộ đệm lưu lượng</li>
  </ul>
 
 <a name="control"></a>
 ### 2.2 Tầng control
 Tầng Control là tầng nằm giữa trong mô hình SDN. Tầng này đóng vai trò là bộ não của SDN. Tầng Control có 3 lớp:
 - **Network hypervisors** :  cho phép các máy ảo khác nhau chia sẻ cùng một nguồn tài nguyên hardware
 - **Network operating system** : thông thường chạy các core services như:<ul><li> Topology services: xác định làm thế nào để các thiết bị chuyển tiếp kết nối được với nhau và xây dựng những gì đã biết như là đồ thị topology. VD: Với lệnh switch để gửi LLDP packets hoặc các gói chuyên dụng khác và tìm ra điểm đến của các gói tin.</li>  <li> Inventory services : Thường được sử dụng để theo dõi các thiết bị được kích hoạt SDN và ghi lại thông tin cơ bản của chúng. Vd: Phiên bản của Openflow và nó có thể support gì.</li><li> Statistics services : Được dùng để đọc thông tin counter cung cấp cho các thiết bị chuyển tiếp như là traffic counters trong flow interface và flow tables.</li><li> Host tracking : Tìm địa chỉ IP như địa chỉ Mac của localhost trong mạng. Thông thường bằng cách chặn các packets hoặc không kết hợp với máy ảo scheduling platform.</li></ul>
 - **Northbound interface (NF)** : gần như là một hệ sinh thái phần mềm, NI không phải là một phần cứng như SI. Tầng control cung cấp một abstraction cơ bản cho tầng trên cùng là tầng application để có thể giao tiếp với nhau. NI là giao diện tĩnh cho phép sử dụng tiêu chuẩn HTTPs gọi trực tiếp đến tầng control.
 
 <img src=https://i.imgur.com/Iih3J0P.png>
 
 **Eastbound/Westbound**: là trường hợp đặc biệt của interfaces được yêu cầu bởi các bộ điều khiển phân phối. Mỗi controller triển khai east/west bound API riêng cho mình. Các hàm thực hiện của những interfaces này gồm nhập/xuất dữ liệu giữa các controller, thuật toán cho mô hình dữ liệu thống nhất, và khả năng giám sát/ thông báo. Giống như SI và NI, east/westbound APIs là các thành phần cần thiết
của bộ điều khiển phân phối. East/westbound dùng để xác định và cung cấp khả năng tương thích chung và khả năng tương tác giữa các bộ điều khiển khác nhau.
