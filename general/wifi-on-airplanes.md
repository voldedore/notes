# Chúng ta lướt web ở độ cao 10 000 mét như thế nào?

Lướt internet ở độ cao 10 km thực tế là điều mà chúng ta mong đợi khi bay. Theo nghiên cứu Du khách Toàn cầu 2018 (Nguyên văn: [2018 Global Traveler](https://www.gogoair.com/learning-center/2018-global-traveler-research-study/)), 94% du khách trên quả địa cầu này cảm thấy rằng trên chuyến bay của họ có dịch vụ wifi sẽ tăng trải nghiệm bay của họ và 30% trong số đó rõ ràng là quan tâm đến dịch vụ này khi đặt vé máy bay.

![10 quan tâm khi đặt vé máy bay](https://miro.medium.com/max/1306/0*OiNjMo2GsbQWQEoq)

> Nguồn: 2018 Global Traveler 

Hiện tại, các hãng hàng không thu $17 mỗi hành khách chi phí các dịch vụ như thức ăn hay bán lẻ trên chuyến bay. Nếu có cả wifi trên chuyến bay, hành khách sẽ phải trả thêm $4 và điều này sẽ mang về thêm khoảng 30 tỉ đô vào doanh thu cho các hãng hàng không vào năm 2035.

Vì thế, sẽ không bất ngờ khi các hãng hàng không trên thế giới đang chạy đua nhau để trang bị wifi trên các chuyến bay của họ. Nhưng làm thế nào một hãng hàng không có thể đáp ứng được cái thứ xa xỉ hiện đại đó cho khách hàng khi họ đang di chuyển gần 1000 km/h và ở độ cao xấp xỉ 10 000 mét trên mặt nước biển?

Có hai cách để chúng ta đem internet về với các phi cơ.

## Hệ thống Air to ground (ATG)

Hệ thống này, vào thủa ban sơ lúc nó được phát triển, hoạt động như thể mạng di động mà chúng ta đang sử dụng như trên điện thoại. Nhưng không giống các trạm phát sóng di động chủ yếu phát tín hiệu xuống, các tháp này cung cấp internet cho các phi cơ bằng cách [phát tín hiệu lên phía trên](https://fortune.com/2017/08/10/how-does-wifi-work-on-planes/). Các antenne được bố trí ngay bụng máy bay sẽ thu tín hiệu này và truyền đến máy chủ cũng được đặt trên máy bay. Server này có modem để có thể chuyển đổi tín hiệu ở tần số radio thành tín hiệu máy tính và ngược lại, cung cấp internet cho khách bay thông qua các access points đặt bên trong phi cơ. Thông tin được trao đổi giữa antenne của máy bay và các tháp thu phát sóng trong suốt hành trình bay. Tiếp đên, các tháp phát sóng được kết nối vào các trung tâm vận hành được quản bởi các nhà cung cấp dịch vụ y như các ISP di động.

![Ground-based towers projecting signal upward.](https://miro.medium.com/max/530/0*z8wD2ixUwoZwqZdV)

> Các tháp phát sóng chiếu tín hiệu lên phía trên. Nguồn: [ThePointsGuy](https://thepointsguy.com/2015/11/how-in-flight-wi-fi-works/).

![ATG-4 của hãng cung cấp GoGo bao gồm 2 antenne chính ngay dưới bụng máy bay, 2 antenne bên hông, một server và một dàn các router wifi bên trong máy bay.](https://miro.medium.com/max/1000/0*r-18bsHXs3IJhpae)

> ATG-4 của hãng cung cấp GoGo bao gồm 2 antenne chính ngay dưới bụng máy bay, 2 antenne bên hông, một server và một dàn các router wifi bên trong máy bay.

Hình trên mô tả hệ thống ATG-4 của GoGo, hiện được sử dụng ở các hãng hàng không của Hoa Kỳ. Tầm phủ sóng của GoGo kéo dài xuyên suốt Bắc Mỹ với hệ thống tầm 200 tháp.

Hệ thống ATG có 2 khuyết điểm lớn như sau:

1. Do hoạt động trên băng tần thấp (800MHz), nên chỉ có thể cung cấp được tốc độ tối đa cho mỗi chuyến bay vào khoảng 10 Mbps. Để so sánh thì [tốc độ internet bình quân](https://www.speedtest.net/reports/united-states/2018/#fixed) của Hoa Kỳ gần 100 Mbps. Khi có nhiều người dùng cùng lúc, tốc độ cho mỗi người dùng chỉ đủ để check mail, và thậm chí là để check mail thì có khi cũng phải chờ trong vô vọng.

2. Tầm phủ sóng khá lẻ tẻ, vì sẽ có ít tháp phát sóng hơn như trong hoang mạc hoặc là không có tháp nào như ở ngoài đại dương mênh mông. Việc này khiến cho hệ thống ATG không phải là sự lựa chọn phổ biến trong các chuyến bay quốc tế.

## Hệ thống (dựa trên) vệ tinh

Hệ thống vệ tinh phức tạp hơn ATG, nhưng đem lại tốc độ nhanh hơn và đáng tin cậy hơn.

Thay vì nằm dưới bụng, các antenne được trang bị trên đỉnh máy bay. Các antennes này thu tín hiệu từ các vệ tinh bay quanh trái đất. Nhưng vì cả đôi chúng nó (cái phi cơ của chúng ta và cái vệ tinh) đều di chuyển, và bọn chúng di chuyển không phải với một tốc độ chậm, và đôi khi chúng cách nhau đến 22 ngàn dặm (tức là đâu đó gần 36 ngàn cây số), nên các antenne này cần phải [liên tục tinh chỉnh vị trí](http://concourse.gogoair.com/gogo-international-ku-band-satellite-internet-work/) của chúng để có thể thu được tín hiệu. Như vậy, ngoài các server và các wifi AP, một thiết bị khác có nhiệm vụ điều khiển antenne dựa trên vị trí và tốc độ chuyến bay. Các vệ tinh được kết nối với các trạm trên mặt đất. Các trạm trên mặt đất sẽ được kết nối vào các trung tâm vận hành quản bởi các nhà cung cấp dịch vụ.

![Hệ thống hoạt động dựa trên các vệ tinh của GoGo gồm các antenne vệ tinh, một server, Kandu, để điều chỉnh các antenne, Modman để chuyển đổi tín hiệu và nhiều AP bên trong phi cơ.](https://miro.medium.com/max/1044/0*UBVkYwA5QSV0nqc9)

> Hệ thống hoạt động dựa trên các vệ tinh của GoGo gồm các antenne vệ tinh, một server, Kandu, để điều chỉnh các antenne, Modman để chuyển đổi tín hiệu và nhiều AP bên trong phi cơ.

Hai ưu điểm chính của hệ thống internet dựa trên vệ tinh: 

1. Vùng phủ sóng xem như là toàn cầu (trừ 2 cực). Với các chuyến bay dài, antenne có thể phải điều chỉnh vị trí để kết nối với vệ tinh khác, nhưng thường thì chỉ một lần thôi. Việc này rõ ràng biến hệ thống này được sử dụng rộng rãi trong các chuyến bay quốc tế.

2. Nó hoạt động trên tần số cao hơn, cung cấp băng thông rộng hơn và tốc độ cao hơn. Hai [dãy băng tần](https://www.getconnected.aero/2017/09/lkuka-band-satellites-mean/) chính dùng cho internet vệ tinh là Ku-band (12-18GHz) và Ka-band (26-40GHz). Hai băng này cho băng thông từ 30-100Mbps cho mỗi phi cơ, tất nhiên là cao hơn mức 10Mbps của ATG.

Tuy vậy, hệ thống này có ba điểm trừ:

1. Đắt đỏ. Về mặt trang thiết bị, bảo trì cũng như băng thông đều tốn nhiều chi phí hơn hệ thống ATG. Nên các hãng hàng không nhỏ hay các hãng nội địa sẽ ít dùng hệ thống này.

2. Khoảng cách mà dữ liệu di chuyển là cực kì xa, sẽ làm tăng độ trễ (latency). Độ trễ là thời gian mà dữ liệu di chuyển từ nguồn phát đến đích tính bằng ms (mili giây). Mặc dù tốc độ tổng thể cao hơn, khi bạn click vào một link, trang web sẽ delay một khoảng khá lớn trước khi load, và khi nó bắt đầu load được rồi thì gần như nó sẽ load ngay tức khắc. Hệ thống ATG, ngược lại, lại load gần như ngay lập tức do có độ trễ thấp, nhưng lại tốn gần như là mãi mãi để hoàn thành. Xem thêm infographic về khoảng cách đáng kinh ngạc khi truyền dữ liệu (~70 ngàn cây số).

3. Ngoài các chi phí về trang thiết bị, bảo trì thì một chi phí tiềm tàng khác đó là nhiên liệu. Khi nó có vẻ như là không đáng kể, các antenne đổi hình dạng (do nó phải điều chỉnh để connect tới các v ệ tinh) vô tình sẽ giảm hiệu quả khí động học của máy bay. Hiện nay, các nhà cung cấp đang cố gắng để giảm kích cỡ của các antenne lại để giảm chi phí. Antenne 2Ku mới nhất của GoGo chỉ dày 4 inches (đâu đó 10 cm), sẽ tạo ra ít ma sát hơn.

Dịch từ https://onezero.medium.com/what-makes-it-possible-to-browse-the-internet-at-35-000-feet-1afaea83eb5