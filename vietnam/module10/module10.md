# Module 10 - QGIS plugins

**Author**: Codrina


## Giới thiệu chung

Module này sẽ giới thiệu một số plugin thú vị và hữu dụng nhất mà cộng đồng QGIS đã phát triển và sẵn dùng cho mọi người.


## và học được các kỹ năng sau:**

*   Cách tìm kiếm và cài đặt plugin mới
*   Cách chuyển giữa các plugin repository khác nhau.
*   Các đọc tài liệu plugin và những gì cần tìm.
*   Chi tiết một số chức năng của các plugin thông dụng nhất.


## Các công cụ và tài nguyên cần thiết**

*   [QGIS version 3.16.1 - Hannover](https://qgis.org/en/site/forusers/download.html)


## Yêu cầu về kỹ năng: 

*   Kiến thức cơ bản về vận hành máy tính
*   Nắm vững tất cả các module, vì các plugin được giới thiệu sẽ áp dụng cho nhiều khái niệm/ yếu tố mà bạn đã học trong giáo trình này, như vector, raster, attribute table, các quy tắc bản đồ và nhiều thứ khác.  


## Nội dung chính 


### Phase 1: Giới thiệu plugin**

Một trong nhiều lợi thế của cộng đồng mã nguồn mở - nhà phát triển phần mềm cũng như người dùng - là tốc độ đáng kinh ngạc của sự phát triển và cải tiến, cách mà các ý tưởng mới phát xuất và đưa vào thực tế. 

Như bạn đã thấy trong Module 1, QGIS được thiết kế với kiến trúc 'plugin', cho phép dễ dàng tuỳ chỉnh theo nhu cầu của người dùng bằng cách thêm vào các plugin. Thực tế, QGIS là sự kết hợp của các **core** và **external plugins**. Các core plugins tạo thành cấu trúc chính, được bảo trì bởi QGIS Development Team và luôn được bao gồm trong bản cài đặt, như Processing core plugin, Zonal Statistics hoặc Plugin Manager. Theo thời gian, các external plugin khác nhau có thể biến thành core plugin.  

Tất nhiên, với các nguyên tắc mã nguồn mở, cùng với các tài liệu tuyệt với và chi tiết sẵn dùng và nhiều kênh giao tiếp và các sự kiện chuyên đề, người dùng có thể học cách xây dựng mô5t plugin đế đáp ứng nhu cầu sử dụng. Và đó là một **external plugin**. Trên [trang web](https://plugins.qgis.org/), bạn có thể tìm tất cả các tài liệu cần thiết. Hầu hết các external plugin được viết bằng Python, nhưng cũng có thể viết bằng C++.

Trong phase 1 này, chúng ta sẽ khám phá cách cài đặt QGIS plugin - cách tìm một plugin để giải quyết một yêu cầu cụ thể, cách đọc hiểu các tài liệu và cách báo cho nhà phát triển nếu có lỗi xảy ra trong quá trình sử dụng plugin.


### Plugin manager**

QGIS cung cấp một core plugin cho phép người dùng quản lý, cài đặt, cập nhật và gỡ cài đặt các external plugin. Chức năng này khá trực quan, cung cấp truy cập đầy đủ đến các kho plugin công khai chính thức.

Cần nhấn mạnh rằng các external plugin - chính thức hoặc thử nghiệm - đều là sản phẩm của các nhà phát triển các nhân hoặc tổ chức, và tổ chức QGIS không chịu bất cứ trách nhiệm nào. Tuy nhiên, có một số quy t9a1c mà nhà phát triển phải tuân thủ nếu muốn chia sẻ plugin của họ trên kho lưu trữ chính thức, cũng như các khuyến nghị để được chấp nhận nhanh chóng. Các yêu cầu bao gồm các yếu tố như giấy phép tương thích, tài liệu tối thiểu, xác định rõ ràng các yếu tố phụ thuộc và các yếu tố khác. Các khuyến nghị bao gồm việc kiểm tra xem plugin có trùng lặp với các plugin đã có hay không, lưu trữ mã nguồn rõ ràng, tương thích với tất cả hệ điều hành như Windows, Linux, macOS, và nhiều thứ khác.

Experimental plugins - như được gắn nhãn trong plugin manager - là các plugin đang trong giai đoạn phát triển bản đầu, không bảo đảm sử dụng trơn tru. Chúng được xem là kiểm tra "bằng chứng về khái niệm" và người dùng không được khuyến cáo cài đặt trừ khi có ý định sử dụng cho mục đích thử nghiệm.

Tất nhiên, để xem các experimental plugin, trong Plugin manager settings, chọn  `Show also experimental plugins` (Hình 10.2a). Cũng có thể liệt kê các deprecated plugin, nhưng không được khuyến khích vì các plugin này không còn được bảo trì nữa.

Hai loại plugin đưỢc phân biệt rõ ràng trong Plugin Manager (xem Hình 10.1 và 10.2b)


![Official plugins trong Manager plugin](media/fig101.png "Official plugins trong Manager plugin")

Hình 10.1 - Official plugins trong Manager plugin


![Tuỳ chọn hiển thị experimental plugins](media/fig102_a.png "Tuỳ chọn hiển thị experimental plugins")

Hình 10.2a - Tuỳ chọn hiển thị experimental plugins


![Experimental plugins trong Plugin Manager](media/fig102_b.png "Experimental plugins trong Plugin Manager")

Hình 10.2b - Experimental plugins trong Plugin Manager

Một khía cạnh khác đáng nói là Plugin Manager khá linh hoạt, cho phép các nhà phát triển thêm vào private repository - kho lưu trữ riêng của họ (xem Hình 10.3)


![Thêm private plugin repository vào QGIS](media/fig103.png "Thêm private plugin repository vào QGIS")

Hình 10.3 - Thêm private plugin repository vào QGIS

Điều này là hữu ích, nếu ví dụ, bên trong tổ chức của bạn có nhu cầu nhiều plugin hơn, nhưng không thuân thủ các yêu cầu để có thể đưa lên kho lưu trữ chính thức của QGIS. Bạn có thể tham khảo cách thiết lập plugin repository của riêng bạn trên [GIS OPS](https://gis-ops.com/qgis-3-plugin-tutorial-set-up-a-plugin-repository-explained/). 

Một cách đơn giản hản là zip plugin lại và chia sẻ file zip này để cài đặt plugin. Tuy nhiên, cách này không được khuyến khích.

Ngoài mục Settings, người dùng có thể chú ý là có một số tab khác ở bên trái như `All, Installed, Not installed, New, Invalid, Install from ZIP` 

Sau khi quyết định loại plugin nào sẽ được liệt kê trong Plugin Manager, người dùng có thể chọn `All` để xem tất các các plugin xuất hiện như thế nào trong Plugin Manager. Để minh hoạ, hãy thử tìm `Cartographic Line Generalization` plugin

Như bạn thấy, Plugin Manager có một thanh tìm kiếm để người dùng có thể gõ các tứ khoá tìm kiếm phù hợp với yêu cầu cụ thể. Trong trường hợp của chúng ta, từ khoá là ‘cartographic/cartography’


![Tìm kiếm một plugin cụ thể trong Plugin Manager](media/fig104.png "Tìm kiếm một plugin cụ thể trong Plugin Manager")

Hình 10.4 - Tìm kiếm một plugin cụ thể trong Plugin Manager

Có thể thấy, phía bên phải là các thông tin mô tả plugin. Cấu trúc các thông tin này được chuẩn hoá và bắt buộc phải có cho từng plugin.

Các metadata cho mỗi plugin bao gồm:


1. Tên gọi plugin và phụ đề mô tả chức năng
2. Mô tả - chi tiết mô tả tuỳ thuộc vào nhà phát triển
4. Số lượt download, số sao bình chọn mà plugin nhận được từ cộng đồng;
5. Các từ khoá được chọn bởi nhà phát triển (mà người dùng có thể tìm kiếm bằng các từ khoá này)
7. Một loạt các link quan trọng: trang web, **bug tracker** và code repository
9. Tên của nhà phà triển, cũng như tổ chức liên kết. Đôi khi, tên gọi của dự án mà plugin được phát triển cũng được liệt kê;
10. Phiên bản của plugin với chú thích _stable_ or _experimental_;
11. Hình ảnh đại diện cho plugin

Trong Hình 10.5, các thành phần metadata như trên đều được xác định


![Tài liệu mô tả plugin](media/fig105.png "Tài liệu mô tả plugin")

Hình 10.5 - Tài liệu mô tả plugin

Ở góc phải dưới cửa sổ, chọn ` Install plugin` để cài đặt, và một biểu tượng hoặc menu của Plugin sẽ được thêm vào giao diện QGIS.

Điều quan trọng đề cập ở đây là, thông thường, vì hạn chế về không gian, phần mô tả trong Plugin Manager không bao quát hết. Do đó, để hiểu rõ nhất liệu plugin có đáp ứng nhu cầu hay không, người dùng phải tham khảo tại trang web của plugin. Trong trường hợp của chúng ta, thấy rằng trang chủ của plugin cũng chính là trang code repository - trên Gitlab, nhưng không phải trường hợp nào cũng vậy (xem Hình 10.6)

![Trang chủ của plugin](media/fig106_a.png "Trang chủ của plugin")

Hình 10.6a - Trang chủ của plugin


![Metadata chi tiết trên trang chủ của plugin](media/fig106_b.png "Metadata chi tiết trên trang chủ của plugin")

Figure 10.6b - Metadata chi tiết trên trang chủ của plugin

Một khía cạnh rất quan trọng khác cần nhấn mạnh về thông tin của plugin là trang **bug tracker**. Một hệ thống bug tracker là một ứng dụng phần mềm lưu vết tất cả các sự cố của phần mềm (issues/ bugs). Trong trưỜng hợp này bug tracker được hỗ trợ bởi code repository Github (Hình 10.7)


![Bug tracking system trong Github cho một QGIS plugin](media/fig107.png "Bug tracking system trong Github cho một QGIS plugin")

Figure 10.7 - Bug tracking system trong Github cho một QGIS plugin

Chi tiết cách báo cáo một sự cố phần mềm trên Github nằm ngoài phạm vi của Module này, tuy nhiên cần điểm qua một số điều quan trọng. Đầu tiên, hệ sinh thái mã nguồn mở nói chung và GIS nói riêng hoạt động tốt nhất khi tất cả các bên tham gia đều hoạt động tích cực theo vai trò của học, nghĩa là nhà phát triển sẽ viết code và người dùng kiểm tra và phản hồi các vấn đề/ lỗi nếu có. Nếu tìm kiếm nhanh các bug trackers của [QGIS](https://github.com/qgis/QGIS/issues) hoặc [GRASS](https://github.com/OSGeo/grass/issues), hoặc các phần mềm mã nguồn mở khác, bạn sẻ thấy hoạt động rất mạnh mẽ. Điều này là tốt vì nó cho thấy cộng đồng năng động, và sự tương tác giữa nhà phát triển và người dùng hoạt động bình thường. Thứ hai, trước khi báo cáo một lỗi nào đó, hảy chắn rằng bạn đã tìm kiếm kỹ trên mạng về giải pháp cho vấn đề của bạn, nếu không bạn sẽ bị chê cười vì không dành thời gian làm bài tập!


#### **Câu hỏi**


1. Bạn có cần nhập hoàn chỉnh tên của plugin để tìm trên Plugin Manager?
*   <span style="text-decoration:underline;">Không, chỉ cần nhập keyword. </span>
*   Có. 
2. Các official và experimental plugin có trong cùng một repository?
*   <span style="text-decoration:underline;"> Đúng, miễn là bật tuỳ chọn ‘Show the experimental plugins’ trong Plugin Manager. </span>
*   Sai, các experimental plugin nằm ở repository khác
3. Kể 2 hoặc 3 thông tin mà người dùng có thể tìm thấy trong tài liệu mô tả plugin:
*   Tên và mô tả, số lượt download, trang chủ, code repository, tên của nhà phát triển, tóm tắt mô tả.


### Phase 2:  Một số Plugin thú vị của QGIS **

Plugin có thể được chia thành nhiều loại khác nhau, tuỳ thuộc vào những gì được coi là quan trọng. Sau đây, chúng tôi xác định 02 cách phân loại:

*   Mức độ phát triển
    *   Official - plugin hoạt động ổn định, tài liệu đầy đủ và có thể sử dụng thực sự; 
    *   Experimental - plugin đang ở giai đoạn phát triển ban đầu, phù hợp cho mục đích thử nghiệm;
    *   Deprecated - plugin không được tiếp tục bảo trì, nghĩa là nó không được cập nhật phiên bản mới, nhà phát triển có thể không phản hồi các báo cáo lỗi, chỉ được sử dụng nếu không có cách nào khác để giải quyết vấn đề.
*   Thể loại: 
    *   Vector; 
    *   Raster;
    *   Web;
    *   Database;
    *   Cartography. 

Cần chú ý rằng một số plugin hoạt động như cầu nối cho phép QGIS truy cập đến các CSDL bên ngoài, cliud, dịch vụ, trong trường hợp đó, các yếu tố bổ sung có thể được yêu cầu - như một tài khoản tả tiền cho các dịch vụ, cloud hoặc API key. Một ví dụ minh hoạ là Planet Explorer Plugin từ Planet Inc (Hình 10.8)


![Ví dụ về plugin yêu cầu đăng ký để sử dụng đầy đủ chức năng trong QGIS ](media/fig108.png "Ví dụ về plugin yêu cầu đăng ký để sử dụng đầy đủ chức năng trong QGIS ")

Hình 10.8 - Ví dụ về plugin yêu cầu đăng ký để sử dụng đầy đủ chức năng trong QGIS 

Mặc dù phần mô tả không đề cập đến vấn đề này, trang chủ của plugin sẽ tiết lộ các yêu cầu để plugin hoạt động: “Planet subscription or trial for accessing and downloading Planet imagery. Don't have a subscription? Contact our [team](https://www.planet.com/contact/) to learn more.”

Trong phần tiếp theo, chúng tôi sẽ xác định và cung cấp các ví dụ ngắn cho một số plugin mà chúng tôi cho là hữu dụng. Hãy nhớ rằng đây là một danh sách ngắn trong rất nhiều plugin, vì vậy hãy khám phá thêm nếu muốn.


#### **Discovery**


![Discovery plugin](media/fig109_a.png "Discovery plugin")

Figure 10.9a - Discovery plugin

Discovery là một plugin rất hữu ích, cho phép người dùng tìm kiếm văn bản chứa trong thuộc tính của dữ liệu vector. Plugin hỗ trợ kết nối đến PostgreSQL/PostGIS database, MS SQL Server hoặc geopackage file và tìm văn bản trọng một column xác định. Nó cho phép auto-complete và hỗ trợ các biểu thức truy vấn linh động.

Để thử nghiệm, chúng ta sẽ sử dụng một geopackage file từ Humanitarian Data Exchange có sẵn cho [download](https://data.humdata.org/dataset/hotosm_phl_north_populated_places). Đây là một vector file chứa các địa điểm đông dân cư của Philippines, cùng với tên và dân số. Dữ liệu thô được tải xuống từ OpenStreetMap.

Trong Plugin Manager, cài đặt Discovery plugin, một toolbar mới sẽ hiển thị trong giao diện QGIS. Hãy nhập các tham số: Data source type: Geopackage, name: Philippines, chọn file vừa download và Populated Places layer, search column: name. Chúng ta cũng sẽ yêu cầu các thông tin bổ sung được hiển thị: is_in và population. Trong trường hợp này, nếu có nhiều làng cùng tên nhưng thuộc các tỉnh khác nhau, chúng ta sẽ có thể phân biệt chúng. Các tham số được nhập như hình 10.9b


![Thiết lập Discovery plugin](media/fig109_b.png "Thiết lập Discovery plugin")

Hình 10.9b - Thiết lập Discovery plugin

Chọn OK và hãy thử tìm “San Roque” trên thanh tìm kiếm (Hình 10.9c)


![Sử dụng Discovery để tìm nhanh các thuộc tính của vector layer](media/fig109_c.png "Sử dụng Discovery để tìm nhanh các thuộc tính của vector layer")

Hình 10.9c - Sử dụng Discovery để tìm nhanh các thuộc tính của vector layer

Trong ví dụ này, chúng ta có thể thấy có rất nhiều San Roque populated places ở Philippines, chọn một mục trong danh sách và QGIS sẽ phóng to đến (Hình 10.9d)


![Zoom đến đối tượng được chọn trong thanh tìm kiếm](media/fig109_d.png "Zoom đến đối tượng được chọn trong thanh tìm kiếm")

Hình 10.9d - Zoom đến đối tượng được chọn trong thanh tìm kiếm

Plugin cung cấp khả năng tìm kiếm vector bằng cách tìm kiếm văn bản cùng với nhiều bộ lọc, ví dụ như bounding box hoặc truy vấn SQL

Để có thông tin chi tiết về các khả năng của plugin, cùng với một hướng dẫn toàn diện hơn, truy cập Discover plugin [webpage](https://www.lutraconsulting.co.uk/projects/discovery/). 


#### **Polygon Divider**


![Polygon Divider plugin](media/fig1010_a.png "Polygon Divider plugin")

Hình 10.10a - Polygon Divider plugin

Polygon DivIder là một plugin hữu ích khác hỗ trợ người dùng chia polygon thành một số polygon 'vuông vắn' theo kích thước xác định. 

Công cụ này có thể hữu ích cho nhiều ứng dụng như tách thửa đất, lấy mẫu môi trường,... 


Chúng ta hãy sử dụng công cụ này cho các lớp Tp.HCM và xem kết quả.

Sử dụng Plugin Manager, cài đặt Polygon Divider. Sau khi hoàn thành, một biểu tượng mới sẽ xuất hiện trên QGIS toolbar và một một cửa sổ được mở (Hình 10.10b)


![Polygon Divider plugin window](media/fig1010_b.png "Polygon Divider plugin window")

Hình 10.10b - Polygon Divider plugin window

Chọn input layer là ranh giới hành chính Tp.HCM, lưu kết quả với tên HCMC_PolygonDivider, chọn 1000000 (nghĩa là kích thước các ô chia là 100 ha), chọn left hoặc right để chọn hướng cắt và tolerance = 1. Kết quả như hình 10.10c


![Kết quả chạy Polygon Divider Plugin trên lớp ranh giới hành chính Tp.HCM](media/fig1010_c.png "Kết quả chạy Polygon Divider Plugin trên lớp ranh giới hành chính Tp.HCM")

Hình 10.10c - Kết quả chạy Polygon Divider Plugin trên lớp ranh giới hành chính Tp.HCM


Để tìm hiểu kỹ hơn về các chức năng của plugin, cùng với hướng dẫn toàn diện hơn, truy cập Polygon Divider [webpage](https://github.com/jonnyhuck/RFCL-PolygonDivider). 



#### **Load Them All**


![Load Them All plugin](media/fig1011_a.png "Load Them All plugin")

Figure 10.11a - Load Them All plugin

Đây là một plugin hữu ích khi bạn có nhiều layer (vector và raster) mà bạn cần tải vào QGIS. Plugin cho phép tự động tải tất cả trong một lần, nhưng ưu điểm lớn là nó cung cấp vô số bộ lọc, ví dụ như theo tên, ngày chỉnh sửa, bounding box (nhập toạ độ thủ công), kiểu hình học và nhiều thứ khác.

Để thử nghiệm, chúng ta sẽ tải tất các file trong Module 8 đã học. Đối với vector, chúng ta sẽ chọn các shapefile được chỉnh sửa trước một ngày nào đó, đối với raster chúng ta sẽ chọn bộ lọc theo tên của raster bắt đầu bằng chữu LandCover (Hình 10.11_b)


![Thiết lập tham số cho Load them All plugin (vector và raster)](media/fig1011_b.png "Thiết lập tham số cho Load them All plugin (vector và raster)")

Hình 10.11b - Thiết lập tham số cho Load them All plugin (vector và raster)

Các tham số xác định như trên đại diện cho mô5t ví dụ dựa trên cấu trúc có sẵn. Bạn có thể thay đổi cho phù hợp với các file trên máy tính của bạn.

Kết quả sau khi chạy Loda them All plugin với các tham số trên được thể hiện trong hình 10.11c (vector) và 10.11d (raster)


![Sử dụng Load them All plugin để load nhiều lớp vector](media/fig1011_c.png "Sử dụng Load them All plugin để load nhiều lớp vector")

Hình 10.11c - Sử dụng Load them All plugin để load nhiều lớp vector


![Hình 10.11c - Sử dụng Load them All plugin để load nhiều lớp vector](media/fig1011_d.png "Hình 10.11c - Sử dụng Load them All plugin để load nhiều lớp vector")

Hình 10.11d - Sử dụng Load them All plugin để load nhiều lớp vector


Để tìm hiểu kỹ hơn về các chức năng của plugin, cùng với hướng dẫn toàn diện hơn, truy cập Load the All [webpage](https://github.com/gacarrillor/loadthemall). 



#### **Raster tracer**


![Raster tracer plugin](media/fig1012_a.png "Raster tracer plugin")

Hình 10.12a - Raster tracer plugin

Raster Tracer có thể là plugin rất hữu khi người dùng số hoá trên bản đồ, hay nói cách khác là trích lọc dữ liệu dưới định dạng vector. Hoạt động này thường được thực hiện trên các bản đồ địa hình cũ được scan, tứ đó chúng ta muốn trích lọc các thông tin để lưu trữ, xử lý và trực quan hoá trong các hệ thống thông tin. Một ví dụ điển hình là số hoá bản đồ địa hình để trích lọc các đường đồng mức, tư2 đó xây dựng mô hình 3D


Mặc dù ngày nay, với sự xuất hiện của các mô hình số địa hình thu được từ ảnh vệ tinh, điều này có thể không là vấn đề nữa, nhưng số hoá vẫn được sử dụng rộng rãi. Công dụng nổi bật nhất là trích lọc thông tin từ các bản đồ cũ. Các bản đồ lịch sử cho chúng ta một cửa sổ về quá khức, trước khi chúng ta có vệ tinh để theo dõi biến động rừng và lớp phủ mặt đất. Bởi vì các tài liệu bản đồ này ban đầu ở trên giới, nên để có thể sử dụng các thông tin này với công nghệ hiện đại, chúng ta phải số hoá.   

Sử dụng Plugins Manager, tìm và cài đặt Raster tracer. Plugin bổ sung vào QIGS khả năng bán tự động trong việc theo vết các đối tưỢng tuyến tính của bản đồ raster bên dưới, bằng cách kích chuột vào các điểm uốn của nó trên bản đồ raster. Khi được cài đặt, một biểu tượng mới sẽ xuất hiện trên toolbar. 

Để sử dụng, chúng ta cần ít nhất 2 layer - một raster layer và một là vector layer mà chúng ta sẽ lưu dữ liệu số hoá. Chúng ta đã xác định cho Pampanga một bản đồ địa hình tỉ lệ 1:50k trên trang web chính thư1c của National Mapping and Resources Information Authority. Không may là, mặc dù chúng cho phép truy cập đến [map](http://www.namria.gov.ph/3131-IIIAngelesCity.html), bản đồ này chưa được đăng ký toạ độ. Để phục vục mục đích trình diễn, chúng ta sẽ sử dụng bản đồ này luôn, tuy nhiên, chú ý là trước khi số hoá vector từ bản đồ raster, việc đăng ký toạ độ cho ảnh raster là rất cần thiết. Nếu không, việc số hoá vốn tốn nhiều thời gian sẽ trở nên vô ích.

Đầu tiên, tải lớp Angeles City topographic map vào QGIS (`Layer - Add layer - Add raster layer..`)

Tiếp theo, chúng ta sẽ tạo một vector layer có kiểu là Multistring để lưu trữ các đối tượng tuyến tính được trích lọc từ bản đồ địa hình (Layer - Create Layer - New GeoPackage layer..). Tạo MultiLine vector và lưu với tên là tracer_lines. Chọn EPSG: 3123. Bật chết độ Editing (`Kích chuột phải - Toggle editing`)

Chọn biểu tượng RasterTracer và nhập các tham số như hình 10.12b. Chọn màu của đường đồng mức sử dụng công cụ chọn màu xuất hiện khi kích chuột vào Trace color.


![Nhập các tham số cho RasterTracer](media/fig1012_b.png "Nhập các tham số cho RasterTracer")

Hình 10.12b - Nhập các tham số cho RasterTracer

Bây giờ, tất cả những gì còn lại là bắt đầu số hoá. Sau khi đảm bảo vector đang ở chế độ edit và plugin được kích hoạt, kích vào các điểm uốn của đường đồng mức mà chúng ta muốn trích lọc (Hình 10.12c)


![Kích chuột vào các điểm uốn để vẽ đường sử dụng Raster Tracer](media/fig1012_c.png "Kích chuột vào các điểm uốn để vẽ đường sử dụng Raster Tracer")

Hình 10.12c -  Kích chuột vào các điểm uốn để vẽ đường sử dụng Raster Tracer

Hình 10.12d thể hiện kết quả. 


![Vẽ đường bán tự động theo màu được chỉ định](media/fig1012_d.png "Vẽ đường bán tự động theo màu được chỉ định")

Hình 10.12d - Vẽ đường bán tự động theo màu được chỉ định


#### **Active Fire**


![Active Fire plugin](media/fig1013_a.png "Active Fire plugin")

Hình 10.13a - Active Fire plugin

Tuy nhiên, các plugin không chỉ được thiết kế để làm việc với các dữ liệu mà chúng ta có mà có thể mang đến các dữ liệu được xây dựng bởi các cơ quan, tổ chức hoặc bất cứ người nào chia sẻ chúng thông qua các dịch vụ web chuẩn hoá. 

Một ví dụ điển hình là Active Fire plugin. Nó được phát triển cho phép người dùng QGIS hiển thị một cách nhanh chóng, trực quan và không mất nhiều công sức các đám cháy trong vòng 24h ở bất cứ khu vực nào. Dư4 liệu này được xây dựng bởi NASA và được cung cấp miễn phí cho người dùng. Dữ liệu thô được thu thập từ 2 vệ tinh:  Moderate Resolution Imaging Spectroradiometer ([MODIS](https://modis.gsfc.nasa.gov/)) ([MCD14DL](https://earthdata.nasa.gov/earth-observation-data/near-real-time/firms/c6-mcd14dl)) và Visible Infrared Imaging Radiometer Suite ([VIIRS](https://www.jpss.noaa.gov/viirs.html)) 375 m ([VNP14IMGTDL_NRT](https://earthdata.nasa.gov/earth-observation-data/near-real-time/firms/v1-vnp14imgt) và [VJ114IMGTDL_NRT](https://earthdata.nasa.gov/earth-observation-data/near-real-time/firms/vj114imgtdl-nrt)) trong vòng 24h qua.


Để cài đặt, mở Plugin Manager và tìm kiếm từ khoá fire. Sau khi cài đặt, một biểu tưỢng màu đỏ sẽ xuất hiện trên QGIS toolbar. Khi kích chuột vào, một cửa sổ xuất hiện để cho bạn tuỳ chọn vệ tinh mà bạn muốn xem các pixel xuất hiện đám cháy được xác định trong vòng 24h qua(hình 10.13b)


![Sử dụng Active Fire plugin để tải dữ liệu đám cháy từ NASA trong QGIS](media/fig1013_b.png "Sử dụng Active Fire plugin để tải dữ liệu đám cháy từ NASA trong QGIS")

Hình 10.13b - Sử dụng Active Fire plugin để tải dữ liệu đám cháy từ NASA trong QGIS

Plugin cũng tính toán số lượng các pixel có xuất hiện cháy.


#### **[Qgis2web](https://github.com/tomchadwin/qgis2web)**


![Qgis2web plugin](media/fig1014_a.png "Qgis2web plugin")

Hình 10.14a - Qgis2web plugin

Plugin này cho phép người dùng kết xuất nhanh chóng QGIS porkect thành một **web map**.

Web map là một hiển thị tương tác của thông tin địa lý có thể mở trong trình duyệt web, trên các thiết bị hoặc trong các desktop map viewer. Chúng ta tương tác với các ứng dụng bản đồ dạng này hàng ngày, như OpenStreetMap, Google Maps, Waze, Pokemon Go.

Plugin này cung cấp cho người dùng khả năng chuẩn bị và kết xuất bản đồ một cách nhanh chóng thông qua sử dụng các thư viện như [OpenLayer3](https://openlayers.org/) hoặc [Leaflet](https://leafletjs.com/). Qgis2web cố gắng để chuyển một QGIS project và kết xuất hành HTML, Javascript và CSS để tạo một web map gần giống với QGIS project nhất có thể.

Sau khi cài đặt qgis2web plugin, một biểu tượng mới xuất hiện trên QGIS toolbar. Kích chuột vào biểu tượng để mở ra một cửa os61 mới như hình 10.14b


![Chọn những gì bản đồ sẽ hiện thị trong trình duyệt](media/fig1014_b.png "Chọn những gì bản đồ sẽ hiện thị trong trình duyệt")

Hình 10.14b - Chọn những gì bản đồ sẽ hiện thị trong trình duyệt. 

Giao diện rất trực qua, nhưng cần lưu ý rằng nếu dữ liệu càng nặng, thì thời gian chuẩn bị và kết xuất càng lâu. Sau khi chọn nơi kết xuất, kích chọn export để thư5c hiện (Hình 10.14c)


![QGIS2web chuẩn bị các file và thư mục cần thiết cho sử dụng thư viện OpenLayer 3](media/fig1014_c.png "QGIS2web chuẩn bị các file và thư mục cần thiết cho sử dụng thư viện OpenLayer 3")

Hình 10.14c - QGIS2web chuẩn bị các file và thư mục cần thiết cho sư3 dụng thư viện OpenLayer 3
QGIS2web preparing the necessary files and folders for the OpenLayer 3 web technology

Thư mục được kết xuất chứa nhiều file, tuỳ thuộc vào thư viện bản đồ được chọn - Leaflet hoặc OpenLayer 3. Trong trường hợp OpenLayer3, thư mục được chọn kết xuất chứa các file và thư mục con sau  `images, index.html, layers, resources, styles, webfonts.` Kích đúp vào file index.html để mở trang web map trong trình duyệt, và bạn có thể tuỳ chọn hiển thị các layer trên đó (Hình 10.14d). 


![Mở file index.html trong trình duyệt](media/fig1014_d.png "Mở file index.html trong trình duyệt")

Hình 10.14d - Mở file index.html trong trình duyệt

Bạn có thể thấy rằng, trình duyệt mở web map này từ thư mục trên máy tính (thư mục được chọn để kết xuất từ qgis2web )

Plugin này là một công cụ tuyệt vời để giúp bạn chuẩn bị bản đồ trên web

Để tìm hiểu kỹ hơn về các chức năng của plugin, cùng với hướng dẫn toàn diện hơn, truy cập qgis2web [webpage](https://github.com/tomchadwin/qgis2web). 



#### **DataPlotly**


![DataPlotly plugin](media/fig1015_a.png "DataPlotly plugin")

Hình 10.14a - DataPlotly plugin

DataPlotly plugin được phát triển đặc biệt để hỗ trợ các hiển thị 

The DataPlotly plugin was specifically developed to support interactive plot type visualizations of the loaded vector data in QGIS. The plugin is based on a Python library named Plotly, that is quite powerful providing the possibility to create multitude of interactive, publication-quality graphs: line plots, scatter plots, area charts, bar charts, error bars, box plots, histograms, heatmaps, subplots, multiple-axes, polar charts, and bubble charts. More information on this specific py library is available on the official [website](https://plotly.com/python/). 

Install the plugin using the Plugin Manager and load some vector layers to visualize: 

*   Waterways_3123 (line type);
*   Populated places (point type);

Let us prepare an interactive chart showing how many rivers vs. channels vs. streams vs. drains segments we have in our dataset.

By clicking on the specific pictogram a new window will open, see figure 10.24. 


![alt_text](media/fig1015_b.png "image_tooltip")

Figure 10.15b - DataPlotly window/panel.

Next, set up the parameters, like in figure 10.15c. 


![alt_text](media/fig1015_c.png "image_tooltip")

Figure 10.15c - Setting up the parameters for the pie chart representing types of water lines

Choose waterways_3123 as the vector layer from which to extract the data plotted, grouping field - fclass, Y field - length. If length needs to be calculated, go to the attribute table of the vector layer and write in the field calculator `round($length)`. For more details, see module 8.  Afterwards, select ‘single plot’ at the ploty type and click on the Create plot button, in the lower right-hand side. Your result should look like in figure 10.15d. 


![alt_text](media/fig1015_d.png "image_tooltip")

Figure 10.15d - Waterways types by length pie chart.

When hovering with the mouse over each pie chart segment, a pop-up appears showing the name (taken from fclass column), lengths sum and percentage out of the total. 

One significant functionality of DataPlotly is the connection with the QGIS map canvas. To understand what that is, click on one of the sections of the pie chart. You should see that some features are **automatically** selected in your map canvas (see figure 10.15e). 


![alt_text](media/fig1015_e.png "image_tooltip")

Figure 10.15e - DataPlotly and QGIS map canvas interactive connection testing

That also means that you can interactively update your plot, for example, to show only the selected features. To test, select only a part of the waterways in your map canvas, then go to the DataPlotly, first tab and at plot parameters, tick the ‘only selected features’ option (see figure 10.15f). 


![alt_text](media/fig1015_f.png "image_tooltip")

Figure 10.15f - Interactively update the plot to show only selected features.   

Afterwards, click on the Update plot button at the bottom right-hand side of the DataPlotly window. Results should look approximately as in figure 10.29 (just approximately, because your selection mostly probably differs from the one shown in figure 10.15g). 


![alt_text](media/fig1015_g.png "image_tooltip")

Figure 10.15g - Update the plot to show only the selected features on the map canvas. 

Furthermore, DataPlotly provides the user with an export function - either in a .pdf file or an .html file. The corresponding buttons are in the very low, right-hand side of the DataPlotly window, see figure 10.15h. 


![alt_text](media/fig1015_h.png "image_tooltip")

Figure 10.15h - Export capabilities of DataPlotly


Exporting as HTML file allows the user to prepare a wide variety of data plots ready for web publication (see figure 10.15i).


![alt_text](media/fig1015_i.png "image_tooltip")

Figure 10.15i - Using a browser to open the HTML file exported by DataPlotly.  

The plugin is also very well documented, for the users they provide a help menu for each plot type. You can access it by clicking on the fourth tab on the DataPlotly (see figure 10.15j).


![alt_text](media/fig1015_j.png "image_tooltip")

Figure 10.15j - Help menu for each plot type accessible through the plugin window. 

Due to the direct, interactive link with the QGIS loaded datasets, expressions can also be used when preparing a plot. To test this capability,  we will create a plot base on the Populated places vector layer. Set the following parameters: type: bar plot, layer: populated places, X_field: is_in, Y_field - open the field calculator and insert  `"population" is not null `(see figure 10.15k and figure 10.15l). 


![alt_text](media/fig1015_k.png "image_tooltip")

Figure 10.15k - Opening the field editor in DataPlotly based on attributes of the selected QGIS layer in order to apply an expression for filtering what the plot will display


![alt_text](media/fig1015_l.png "image_tooltip")

Figure 10.15l - Inserting an expression in the field calculator 

The result should look like in figure 10.35. . 


![alt_text](media/fig1015_m.png "image_tooltip")

Figure 10.15m - DataPlotly result of filtering by expression

If we are to interpret this plot, it shows us that among all the provinces where populated places have been registered, the population attribute is different from 0 în only 3 regions, Alaminos, Sual, Pangasian and Bagac. One can easily test this conclusion by looking in the attribute table.

DataPlotly also provides the user with the possibility of creating subplots, which means that multiple plots can be displayed in a single figure. 

To test this functionality, we will use the Population places vector layer. We have the following attributes of interest: `place` = type of place (city, town, village, etc.,` is_in `=  name of province to which it belongs (if known), `population` = (population numbers) and `name `= the name of the place (if known). We will integrate in the same figure, 2 data plots: one to show us how many of the populated places fall into each category of `place `and the second one, how is the population divided by the 4 types of` places. `


![alt_text](media/fig1015_n.png "image_tooltip")

Figure 10.15n - Setting up the parameters for the first plot  - types of settlements by their numbers


![alt_text](media/fig1015_o.png "image_tooltip")

Figure 10.15o - Setting up the parameters for the second plot - types of settlements by population  numbers.


![alt_text](media/fig1015_p.png "image_tooltip")

Figure 10.15p - Subplots in a row

For a detailed description of the plugin capabilities, together with a more comprehensive tutorial, check the DataPlotly [webpage](https://github.com/ghtmtt/DataPlotly). 


#### **QuickMapServices / OpenLayers plugin**


![alt_text](media/fig1016_a1.png "image_tooltip")


![alt_text](media/fig1016_a2.png "image_tooltip")

Figure 10.16a - QuickMapServices plugin; 10.16b - OpenLayers plugin

These 2 plugins are exceptionally useful when a user needs to add basemaps to her/his QGIS project. For example, one wants to see in context the positioning of a new vector layer received, or maybe just to prepare a more attractive cartographic representation for a report. Either the scope, QuickMapServices allows the use to load into their desktop client with only 2 clicks, basemap layers from different provides, such as OpenStreetMap, NASA, Bing or Google Maps. 

Install both plugins using Plugin Manager. In this case, you will notice that they will appear under the Web tab (see figure 10.16b). 


![alt_text](media/fig1016_b.png "image_tooltip")

Figure 10.16b - Location of the QuickMapServices and OpenLayers plugins.

Using them is pretty straight forward, you just click on the layer you want to bring in your map canvas and the plugin will do all the work. Needless to say, that the use of this plugin requires good internet connection, as it uses data served by its providers through standardized web mapping services. 

Figure 10.16c presents the OSM Humanitarian Data Model brought as a basemap for the region of interest used in module 8 and 9, province Pampanga in Philippines. 


![alt_text](media/fig1016_c.png "image_tooltip")

Figure 10.16c - Using OpenLayers plugin. 

Figure 10.16d illustrates the perfect alignment of the basemap loaded in the QGIS map canvas using the OpenLayers plugin. Even though the 2 layers are not in the same projection, QGIS allows projection on-the-fly, so overlay is possible. 


![alt_text](media/fig1016_d.png "image_tooltip")

Figure 10.16d - Loaded vector data (roads) overlaid on to the OSM Humanitarian Data model 

For a detailed description of the plugins capabilities, together with a more comprehensive tutorial, check their webpage: [QuickMapServices](https://nextgis.com/blog/quickmapservices/) and [OpenLayer Plugin](https://github.com/sourcepole/qgis-openlayers-plugin). 


#### **Table2Style**


![alt_text](media/fig1017_a.png "image_tooltip")

Figure 10.17a - The Table to Style plugin

This plugin is useful for situations where there are specific values for pixels within a raster layer that correspond perfectly to a specific color. In this curriculum, we have encountered  such an example, when working with the land cover data (see figure 10.17b). 


![alt_text](media/fig1017_b.png "image_tooltip")

Figure 10.17b - Exemplifying situations where pixel values correspond to an exact colour 

From the provider of this product based on satellite imagery, the pixel values and the associated colours are also made available: 


<table>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td><strong>Color</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>0
   </td>
   <td>#282828
   </td>
   <td>Unknown. No or not enough satellite data available.
   </td>
  </tr>
  <tr>
   <td>20
   </td>
   <td>#FFBB22
   </td>
   <td>Shrubs. Woody perennial plants with persistent and woody stems and without any defined main stem being less than 5 m tall. The shrub foliage can be either evergreen or deciduous.
   </td>
  </tr>
  <tr>
   <td>30
   </td>
   <td>#FFFF4C
   </td>
   <td>Herbaceous vegetation. Plants without persistent stem or shoots above ground and lacking definite firm structure. Tree and shrub cover is less than 10 %.
   </td>
  </tr>
  <tr>
   <td>40
   </td>
   <td>#F096FF
   </td>
   <td>Cultivated and managed vegetation / agriculture. Lands covered with temporary crops followed by harvest and a bare soil period (e.g., single and multiple cropping systems). Note that perennial woody crops will be classified as the appropriate forest or shrub land cover type.
   </td>
  </tr>
  <tr>
   <td>50
   </td>
   <td>#FA0000
   </td>
   <td>Urban / built up. Land covered by buildings and other man-made structures.
   </td>
  </tr>
  <tr>
   <td>60
   </td>
   <td>#B4B4B4
   </td>
   <td>Bare / sparse vegetation. Lands with exposed soil, sand, or rocks and never has more than 10 % vegetated cover during any time of the year.
   </td>
  </tr>
  <tr>
   <td>70
   </td>
   <td>#F0F0F0
   </td>
   <td>Snow and ice. Lands under snow or ice cover throughout the year.
   </td>
  </tr>
  <tr>
   <td>80
   </td>
   <td>#0032C8
   </td>
   <td>Permanent water bodies. Lakes, reservoirs, and rivers. Can be either fresh or salt-water bodies.
   </td>
  </tr>
  <tr>
   <td>90
   </td>
   <td>#0096A0
   </td>
   <td>Herbaceous wetland. Lands with a permanent mixture of water and herbaceous or woody vegetation. The vegetation can be present in either salt, brackish, or fresh water.
   </td>
  </tr>
  <tr>
   <td>100
   </td>
   <td>#FAE6A0
   </td>
   <td>Moss and lichen.
   </td>
  </tr>
  <tr>
   <td>111
   </td>
   <td>#58481F
   </td>
   <td>Closed forest, evergreen needle leaf. Tree canopy >70 %, almost all needle leaf trees remain green all year. Canopy is never without green foliage.
   </td>
  </tr>
  <tr>
   <td>112
   </td>
   <td>#009900
   </td>
   <td>Closed forest, evergreen broad leaf. Tree canopy >70 %, almost all broadleaf trees remain green year round. Canopy is never without green foliage.
   </td>
  </tr>
  <tr>
   <td>113
   </td>
   <td>#70663E
   </td>
   <td>Closed forest, deciduous needle leaf. Tree canopy >70 %, consists of seasonal needle leaf tree communities with an annual cycle of leaf-on and leaf-off periods.
   </td>
  </tr>
  <tr>
   <td>114
   </td>
   <td>#00CC00
   </td>
   <td>Closed forest, deciduous broad leaf. Tree canopy >70 %, consists of seasonal broadleaf tree communities with an annual cycle of leaf-on and leaf-off periods.
   </td>
  </tr>
  <tr>
   <td>115
   </td>
   <td>#4E751F
   </td>
   <td>Closed forest, mixed.
   </td>
  </tr>
  <tr>
   <td>116
   </td>
   <td>#007800
   </td>
   <td>Closed forest, not matching any of the other definitions.
   </td>
  </tr>
  <tr>
   <td>121
   </td>
   <td>#666000
   </td>
   <td>Open forest, evergreen needle leaf. Top layer- trees 15-70 % and second layer- mixed of shrubs and grassland, almost all needle leaf trees remain green all year. Canopy is never without green foliage.
   </td>
  </tr>
  <tr>
   <td>122
   </td>
   <td>#8DB400
   </td>
   <td>Open forest, evergreen broad leaf. Top layer- trees 15-70 % and second layer- mixed of shrubs and grassland, almost all broadleaf trees remain green year round. Canopy is never without green foliage.
   </td>
  </tr>
  <tr>
   <td>123
   </td>
   <td>#8D7400
   </td>
   <td>Open forest, deciduous needle leaf. Top layer- trees 15-70 % and second layer- mixed of shrubs and grassland, consists of seasonal needle leaf tree communities with an annual cycle of leaf-on and leaf-off periods.
   </td>
  </tr>
  <tr>
   <td>124
   </td>
   <td>#A0DC00
   </td>
   <td>Open forest, deciduous broadleaf. Top layer- trees 15-70 % and second layer- mixed of shrubs and grassland, consists of seasonal broadleaf tree communities with an annual cycle of leaf-on and leaf-off periods.
   </td>
  </tr>
  <tr>
   <td>125
   </td>
   <td>#929900
   </td>
   <td>Open forest, mixed.
   </td>
  </tr>
  <tr>
   <td>126
   </td>
   <td>#648C00
   </td>
   <td>Open forest, not matching any of the other definitions.
   </td>
  </tr>
  <tr>
   <td>200
   </td>
   <td>#000080
   </td>
   <td>Oceans, seas. Can be either fresh or salt-water bodies.
   </td>
  </tr>
</table>


When a new dataset - raster or vector - is loaded, QGIS is randomly assigning it a visual representation. It is the user that must define appropriate colours and schemas of the representations. For more information on layers styling, go to module 4. 

To test the table2style plugin, we will use the LandCover2019 raster dataset, used also in module nr.9. By loading the raster into QGIS you should have a restul similar with the one in figure 10.17c.


![alt_text](media/fig1017_c.png "image_tooltip")

Figure 10.17c - QGIS randomly assigns colours to pixel values

As per the data provider, we know that for each pixel value there is a clearly assigned colour  and in the land cover domain, these colours already represent conventions, just as in classic cartography. Forests are represented with a specific kind of green, pastures with another, ocean is depicted with a different kind of blue than inland surface water and so forth. Worst case would be to manually assign all these colours to their respective values. However, the table2style plugin solves this issue automatically, in a matter of seconds. 

Go to Manager plugin and install the table2style plugin. A new icon will appear on your toolbar. Open it by double clicking it. A setting up window should appear, like in figure 10.17d. 


![alt_text](media/fig1017_d.png "image_tooltip")

Figure 10.17d - Table2style window

The plugin requires 2 parameters - a raster layer and an attribute table with pixel values, description label and color codes in one of the three systems: RGB, HSV or Hex. As per our table above, we have Hex codes for the assigned colors. Thus, load the table into QGIS (`Layer - Add layer - Add delimited text layer… `). Of course, it has no geometry. The LandCover values table should look like in figure 10.17e. 


![alt_text](media/fig1017_e.png "image_tooltip")

Figure 10.17e - Attribute table with pixel values, color codes and description for Land Cover

Now, let us take a look at the raster dataset. The table2style works only on a 1-band raster, as it is a one to one connection: pixel value - color code. If more bands are available, judging after the plugin setup window, it would not know which one to choose. However, checking the LandCover2019 layer properties, we notice that there are 3 bands (`Properties - Information - scroll down to Bands`). As we need only Band 1 - discrete classification, we will employ the raster calculator to extract it (`Raster - Raster calculator` and insert in the expression field only "LandCover2019_1band@1" - save the result). For more details on how to work with rasters, check module 9. 

Now, we have all we need to test the plugin. Set up the parameters as in figure 10.17f. 


![alt_text](media/fig1017_f.png "image_tooltip")

Figure 10.17f - Setting up table2style plugin parameters for the Land Cover dataset

The result should look like in figure 10.17g. 


![alt_text](media/fig1017_g.png "image_tooltip")

Figure 10.17g - Automatically styled raster dataset using table2style plugin

For a detailed description of the plugin capab[https://github.com/ptarroso/table2style](https://github.com/ptarroso/table2style)ilities, together with a more comprehensive tutorial, check the Table 2 Style plugin webpage. 


#### **ORS Tools**


![alt_text](media/fig1018_a.png "image_tooltip")

Figure 10.48a - The ORS Tools plugin

For our last presented plugin, we have prepared one to show you the amazing capabilities of the interconnected world of GIS data, tools and services. We have seen previously that there are plugins that can assist us in loading in our QGIS data from other providers without any hassle related to downloading, storing and knowing how to open it (OpenLayers plugin , Active Fire). Yet, the ORS Tools plugin is built to provide access to an outside routing service - the openrouteservice.org, based on OpenStreetMap. 

**Routing** is the process of selecting a path for traffic in a network or between or across multiple selected points. 

The tool set includes routing, isochrones and matrix calculations, either interactive in the map canvas or from point files within the processing framework. 

Using Plugin Manager, install the ORS Tools plugin. A new pictogram will appear on your toolbar. Double click to open (see figure 10.18b). 


![alt_text](media/fig1018_b.png "image_tooltip")

Figure 10.18b - Open ORS Tools window. 

As mentioned, this plugin is using an external database - OpenStreetMap - and external algorithms that are packaged up in service - openrouteservice. In order to be able to connect to this external service, we will need to make an account on their web page and ask for an **API key. **

An API key is a unique identifier used to authenticate a user, developer, or calling program to an API. The API is like a gateway to the insides of a software, a programmatic access to its processes and algorithms. Thus, to use the openrouteservice through QGIS, we will ask for a _key_. 

Proceed with the following steps: 



1. Click on the Sign Up button on the ORS Tools window (figure 10.49). 


![alt_text](media/fig1018_c.png "image_tooltip")

Figure 10.18c - Sign in button

2. Make a free account on the website on the openrouteservice website that opened. 


![alt_text](media/fig1018_d.png "image_tooltip")

Figure 10.18d - Openrouteservice account page 


3. After making the account, you will receive an email informing you of what  you have just gained free access. 


![alt_text](media/fig1018_e.png "image_tooltip")

Figure 10.18e - Email received from openrouteservice

4. Login to your newly made account and request a token. 


![alt_text](media/fig1018_f.png "image_tooltip")

Figure 10.18f - Request openrouteservice token

5. After your token has been created, click on the long alphanumeric string below the name key. A message informing you that it has been copied will appear. 
6. Return to QGIS and insert the copied API key.


![alt_text](media/fig1018_g.png "image_tooltip")

Figure 10.18g - Insert openrouteserviceAPI key into your QGIS

At this point, your QGIS should be ready to calculate routes using openrouteservice and OpenStreetMap. To test its basic capabilities, load into QGIS the Pampanga building layers. Make sure you are working in EPSG 3857 or EPSG:4326. After loading the layer, start inserting the routing points. Open the ORS Tools, and press the green + button (see figure 10.18h). 


![alt_text](media/fig1018_h.png "image_tooltip")

Figure 10.18h - Inserting the routing points using ORS Tools. 

Choose Traveling Salesman routing algorithm and click on apply. After a few moments, a new vector layer has been created: Routes_ORS. 


![alt_text](media/fig1018_i.png "image_tooltip")

Figure 10.18i - Result of running ORS Tools. 

Opening OpenStreetMap, we will notice that  ORS Tools has tried to build a route to touch all points given by clicking on the map. **Please take note! **QGIS has only one layer loaded and that was the building layer and yet now, a new layer has been calculated and automatically added to your map canvas! 


![alt_text](media/fig1018_j.png "image_tooltip")

Figure 10.18j - The calculated route overlaid on top of OpenStreetMap.

The results of ORS Tools highly depend on the quality of the databases used, in this case - the OpenStreetMap. 

The plugin, as well as the openroutingservice, has more to offer but we leave you to discover that in your GIS journey. 


***Philippine-specific***

#### **Azimuth and Distance Plugin**




#### **SRTM Downloader Plugin**




#### **OpenHazardsPH Plugin**



#### **Quiz questions**

1. Can QGIS plugins be run outside the QGIS platform? 
*   _<span style="text-decoration:underline;">No</span>. _
*   _Yes. _
2. In order to use a QGIS plugin one needs to learn how to code. 
*   _<span style="text-decoration:underline;">No.</span>_
*   _Yes. _
3. It is highly recommended that all plugins be installed through the Plugin Manager, even if they could be installed by downloading the zip file and putting it into the right QGIS folder. 
*   _No._
*   _<span style="text-decoration:underline;">Yes. </span>_