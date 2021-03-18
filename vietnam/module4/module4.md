# Module 4 - Styling Layers

**Tác giả**: Ketty

**Biên dịch và bản địa hoá**: Quách Đồng Thắng



## Giới thiệu chung

Module này sẽ hướng dẫn bạn cách thay đổi hiển thị trực quan bản đồ bằng cách lựa chọn các biểu tưỢng (symbol), màu sắc thích hợp và sử dụng các hiệu ứng thích hợp. Kết thúc module, bạn sẽ nắm được các khái niệm niệm như symbology và style của bản đồ. Ngoài ra, bạn sẽ học các kỹ năng sau; 

*   styling layers 
*   symbology cơ bản cho vector/ raster và cách áp dụng cho một layer.
*   blending mode và draw effect
*   sử dụng các công thức để chạy một chức năng xử lý không gian 


## Các công cụ và tài nguyên cần thiết

*   Máy tính
*   Kết nối Internet
*   QGIS 3.16 hoặc mới hơn
*   HCMC_border (trong  [module4.gpkg](data/module4.gpkg)))
*   HCMC_clinics (trong [module4.gpkg](data/module4.gpkg))
*   [Tp.HCM High Resolution Settlement Layer](data/HRSL_HCMC_Population.tif)

## Kỹ năng cần có

*   Kiến thức cơ bản về vận hành máy tính
*   Nắm vững tất cả các Module đã học
  


## Tham khảo thêm

*   QGIS Symbology - [https://docs.qgis.org/3.16/en/docs/training_manual/basic_map/symbology.html](https://docs.qgis.org/3.16/en/docs/training_manual/basic_map/symbology.html)
*   Style Sharing Repository - [https://www.gislounge.com/qgis-style-sharing-repository/](https://www.gislounge.com/qgis-style-sharing-repository/)
*   Styles - [https://plugins.qgis.org/styles/](https://plugins.qgis.org/styles/)
*   Style Hub - [https://style-hub.github.io/](https://style-hub.github.io/)
*   Hillshade in QGIS -[https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html](https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html)
*   Mapping Icebergs in QGIS - [https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html](https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html)


## Giới thiệu chuyên đề

Hãy bắt đầu bằng một ví dụ: 

Tưởng tượng bạn đến một thành phố mới, với vai trò là một khách du lịch, đi chơi hoặc đi công việc. Thành phố có một loạt các địa điểm mà bạn nhất định phải đến hoặc tham quan, bao gồm các bảo tàng, quán cá phê, bãi biển, đài tưởng niệm, cửa hàng bán đồ lưu niệm địa phương và chợ. Bạn cầm một bản đồ giấy thể hiện vị trí của các địa điểm này. Các địa điểm này đểu được đánh dấu chấm đỏ. Theo bạn, bản đồ này có dễ cho chuyến du lịch của bạn ở thành phố này không? Tôi e là không

Đó là lý do vì sao việc tạo "bản đồ với các ký hiệu và màu sắc khác nhau" luôn luôn quan trọng. Những gì bạn thấy trong bản đồ của mình sau khi áp dụng các khái niệm tạo kiểu (styling) là một thể hiện trực quan, sinh động về dữ liệu mà bạn đang làm việc.


### Các Panels, Tabs và Render types quan trọng

#### **Layer Styling Panel** 

Panel này có thể xem là một shortcut đến một số chức năng của layer properties. Nó giúp bạn thiết lập hiển thị cho layer nhanh chóng và thuận tiện, và hiển thị trực quan các hiệu ứng tức thì mà không cần truy cập vào layer properties.

Ngoài việc tránh phải mở cửa sở layer properties, nó cũng tránh tình trạng lộn xộn trong việc hiển thị từng cửa sổ ứng với từng thao tác chọn màu, chỉnh sửa hiệu ứng, hiển thị nhãn,... Ví dụ, khi bạn nhấn nút chọn màu trong Layer Styling Panel, bảng chọn màu được hiển thị ngay bên trong panel thay vì hiện thêm một cửa sổ mới

Trong Layer Styling Panel, chọn một layer cần thiết lập hiển thị:

*   Thiết lập symbology, transparency (độ trong suốt) và histogram cho raster layer. Các tuỳ chọn này cũng có trong cửa sổ Raster Properties
*   ([https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#raster-properties-dialog](https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#raster-properties-dialog)). 
    * Truy cập Raster Properties bằng cách kích đúp chuột vào Raster Layer -> General
*   Thiết lập symbology và label. Các tuỳ chọn này cũng có trong Vector Properties Dialog ([https://docs.qgis.org/3.16/en/docs/user_manual/working_with_vector/vector_properties.html#vector-properties-dialog](https://docs.qgis.org/3.16/en/docs/user_manual/working_with_vector/vector_properties.html#vector-properties-dialog)). 
    * Truy cập Vector Properties Dialog bằng cách kích đúp chuột vào Vector Layer -> General
*   Bạn có thể undo, redo các style đã áp dụng cho layer
  
Mộ chức năng mạnh mẽ khác của panel này là tuỳ chọn Live update. Nếu được chọn, các thay đổi sẽ được hiển thị ngay tức thì trên map canvas mà không cần nhấn nút Apply

Để kích hoạt panel này, vào View->Panels, chọn Layer Styling



![alt_text](media/layer-styling.png "image_tooltip")

Figure 4.1: Layer Styling Panel


#### **Symbology Tab trong Layers Properties**

Để truy cập Symbology Tab, kích đúp chuột vào Layer để mở cửa sổ Layer Properties-> Chọn Symbology

Tại đây, bạn có thể thiết lập hiển thị cho các kênh ảnh (đối với dữ liệu raster) như render type, band, mix/max values, color rendering và resampling. Hình bên dưới lần lượt thể hiện các symbology tabs cho dữ liệu vector và dữ liệu raster;


![alt_text](media/style-vector.png "image_tooltip")

![alt_text](media/style-raster.png "image_tooltip")


Figure 4.2: Symbology cho dữ liệu vector và raster


#### **Raster rendering: Band rendering**

QGIS cung cấp 04 kiểu hiển thị (render) dữ liệu raster. Lựa chọn cách hiển thị nào tuỳ thuộc vào loại dữ liệu. Loại render mặc định là đơn kênh (màu xám). Bạn sẽ phải thay đổi kiểu hiển thị thích hợp tuỳ vào loại dữ liệu.

*   Multiband color - Màu đa kênh ([https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#multiband-color](https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#multiband-color)) - nếu raster có nhiểu kênh ảnh (ví dụ như ảnh vệ tinh được chụp ở nhiều kênh phổ khác nhau).
*   Paletted/Unique values ([https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#paletted]()) - đối với ảnh đơn kênh (đơn phổ) với một bảng màu được đánh chỉ mục - indexed palette (ví dụ bản đồ địa hình số) hoặc cho các trường hợp chung sử dụng palette để hiển thị raster.
*   Singleband gray - xám đơn kênh ([https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#singleband-gray](https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#singleband-gray)) - (một kênh của) ảnh sẽ được hiển thị dưới dạng màu xám. QGIS sẽ chọn kiểu hiển thị này nếu raster không phải là ảnh đa kênh hoặc palette (ví dụ như bản đồ dạng shaded relief)
*   Singleband pseudocolor -  màu giả đơn kênh([https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#label-colormaptab](https://docs.qgis.org/3.16/en/docs/user-_manual/working_with_raster/raster_properties.html#label-colormaptab)) - cách hiển thị này có thể được dùng cho các raster với raster có bảng màu liên tục hoặc các bản đồ màu (ví dụ như bản đồ độ cao)
*   Hillshade ([(https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#hillshade-renderer](https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#hillshade-renderer)) - Tạo hillshade từ một kênh ảnh.


#### **Vector rendering**

Khi bạn tải các lớp dữ liệu không gian trong QGIS Desktop, chúng được gán style Single Symbol với màu ngẫu nhiên. Để thay đổi, kích vào Layer->Properties->Style 


Có nhiều tuỳ chọn hiển thị:

*   Single Symbol – Đây là kiểu hiển thị mặc định với một symbol (kiểu đường, màu sắc) áp dụng cho tất cả các đối tượng của layer.
*   Categorized – cho phép chọn một thuộc tính phân loại để tạo stlye cho layer. Sau khi chọn thuộc tính phân loại, chọn Classify để QGIS áp dụng các symbol khác nhau tương ứng với từng giá trị khác nhau của thuộc tính được chọn. Bạn cũng có thể chọn chức năng tính toán giá trị thuộc tính thông qua các biểu thức SQL. 
*   Graduated – cho phép phân lớp dữ liệu bởi một trường thuộc tính dạng số thành các nhóm riêng biệt. Bạn có thể chọn các tham số choa việc phân lớp (cách phân lớp và số lớp) và có thể chọn chức năng tính toán giá trị thuộc tính thông qua các biểu thức SQL. 
*   Rule-based – dùng để tạo một style dựa trên luật do người dùng định nghĩa. Các luật này có cấu trúc dựa trên biểu thức SQL.
*   Point displacement – nếu bạn có một lớp điểm với các điểm xếp chồng lên nhau, tuỳ chọn này có thể được sử dụng để dời vị trí các điểm sao cho tất cả điểm đều được hiển thị.
*   Inverted polygons – Đây là một cách hiển thị mới, cho phép một đối tượng polygon được chuyển đổi thành một mặt nạ. Ví dụ, một polygon thể hiện ranh giới thành phố sử dụng cách hiển thị này sẽ trở thành một mặt nạ xung quanh thành phố. Nó cũng cho phép sử dụng thêm các cách hiển thị khác như Categorized, Graduated và Rule-based, cũng như sử dụng các biểu thức SQL.  


## Nội dung chính 

### Phase 1: Symbology cơ bản cho raster và vector

Symbology cho dữ liệu vector có thể thay đổi dựa vào độ trong suốt, màu sắc, góc quay và kích thước.

#### **Nội dung**

*   Layer properties và symbology menu
*   Các loại hiển thị Vector
*   Các loại hiển thị raster(band rendering)

#### **Ví dụ 1: Hiển thị Vector**

1. Để minh hoạ cho ví dụ này, chúng ta sẽ sử dụng 02 tập dữ liệu mẫu; HCMC_clinics và HCMC_border (trong module4.gpkg).
2. Thêm 02 lớp vector này vào QGIS; Kích chọn nút Add vector layer ![alt_text](media/add-vector.png "image_tooltip") hoặc sử dụng Browser Panel. 
3. Đây là cách chúng hiển thị theo mặc định. Bạn chú ý là chúng ta có một lớp dạng vùng (polygon) và một lớp dạng điểm (point). Bước tiếp theo là thay đổi symbology cho từng lớp này. Fill color có thể không trùng nhau, nhưng không vấn đề gì bởi vì QGIS chọn màu ngẫu nhiên cho các lớp dữ liệu.

![Default render](media/default-vector-render.png "Default render")

Hình 4.3: Hiển thị mặc định

4. Kích đúp chuột vào lớp polygon, chính là ranh giới hành chính của Tp.HCM. 
5. Chọn **Symbology Tab** 
6. Thay đổi **Fill color** thành **Transparent fill. Mẹo:** Kích vào mũi tên chỉ xuống, phía dưới Fill color
7. Kết quả như hình bên dưới. Bạn có thể thấy là không có màu nền.

![Polygon không có màu nền](media/no-fill-render.png "Polygon không có màu nền")

Hình 4.4: Polygon không có màu nền

8. Bước tiếp theo là định nghĩa symbology cho point layer (lớp HCMC_clinics)
9. Kích đúp chuột vào lớp **HCMC_clinics** để mở cửa sổ **Layer Properties** . Đổi kiểu hiển thị Single Symbol thành **Categorized**, chọn  **Value** là amenity. Chọn Symbol và Color ramp, sau đó chọn Classify 

![Layer Properties dialogue](media/vector-style.png "Layer Properties dialogue")

Hình 4.5: Layer Properties dialogue

10. Kết quả như hình bên dưới

![Kết quả hiển thị vector](media/final-vector-render.png "Kết quả hiển thị vector")

Hình 4.6: Kết quả hiển thị vector



11.  Cần nhớ sắp xếp các layer trong **Layer Panel** sao cho polygon layer nằm bên dưới point layer để point layer không bị che khuất.


#### **Ví dụ 2: Raster rendering**

1. Kích đúp chuột vào raster layer, chính là lớp mật độ dân số (population density). Đây cũng dữ liệu được chuẩn hoá để có thể hiển thị dưới dạng một choropleth map.
2. Chọn tab Symbology
3. Chọn kiểu styling là ‘Singleband pseudocolor’

![Symbology menu](media/qgis9.png  "Symbology menu")

Hình 4.7: Symbology menu

4. Chọn phương pháp nội suy (interpolation), color ramp và mode. Chọn classify. Kết quả là một choropleth map hiển thị mật độ dân số của Tp.HCM

![Mậ độ dân số Tp.HCM](media/hrsl-style.png "Mật độ dân số Tp.HCM")

Hình 4.8: Mật độ dân số Tp.HCM

5.  Phóng to bản đồ để hiển thị chi tiết hơn.

![Bản đồ phóng to](media/zoom-in.png "Bản đồ phóng to")

Hình 4.9: Bản đồ phóng to

6. Ngoài ra, có thể sử dụng **Layer Styling panel** để thiết lập hiển thị cho raster. 

#### **Câu hỏi**

1. Layer symbology là gì ?
2. Phương pháp hiển thị nào là thích hợp cho dữ liệu vector?
3. Các loại hiển thị dữ liệu raster?

#### **Các phương án trả lời**

1. a. graphical element represented as a marker, stroke or fill 
   b. a pointer to the original data
   c. a repository of different color schemes

2. a. single symbol renderer
   b. no symbols renderer
   c. categorized renderer
   d. graduated renderer
   e. proportional symbol 
   f. proportional symbol
   g. point cluster renderer 

3. a. singleband pseudocolor
   b. singleband gray
   c. paletted
   d. multiband color


### Phase 2: Blending modes và draw effects

#### **Nội dung**

*   Thay đổi cấu trúc symbol
*   Thay đổi draw effects and blending modes
*   Trực quan hoá dữ liệu

#### **Hướng dẫn**

1. Sau khi tải 02 layer vào QGIS, map canvas sẽ như hình bên dưới. Bạn có thể thấy là cả 02 layer đều có style đơn giản. Hướng dẫn này sẽ giải thích cách thay đổi draw effects và blending modes để trực quan hoá tốt hơn 
   
![Workspace ban đầu](media/initial-workspace.png "Workspace ban đầu")

Hình 4.10: Workspace ban đầu

2. Mở cửa sổ Layer Properties, chọn Symbology cho lớp ranh giới hành chính. Mẹo: kích đúp chuột vào layer hoặc sử dụng Layer Styling Panel. Kích hoạt Layer Styling Panel bằng cách: View -> Panels -> Layer Styling.

Ở dưới Symbology menu, có một checkbox Draw Effects. Kích chọn checkbox này và kích chọn nút tuỳ chỉnh hiệu ứng ![alt_text](media/customise-effects-button.png "image_tooltip") ở bên phải:

![Layer Properties window và Symbology menu](media/draw-effects.png "Layer Properties window và Symbology menu")

Hình 4.11: Layer Properties window và Symbology menu

3. Cửa sổ Effects Properties xuất hiện

![Effects properties dialogue](media/new-effects-dialog.png "Effects properties dialogue")

Hình 4.12: Effects properties dialogue
   
4. Bạn có thể thấy chỗ Effect type Source effect được chọn mặc định. Source effect không thú vị lắm - nó chỉ đơn giản là vẽ lại layer mà không thay đổi gì cả. Hãy chọn Blur effect bằng cách **kích vào combobox Effec type và chọn Blur**. Bạn có thể thử thiết lập các tham số cho tuỳ chọn Blur
   
![Chọn Effect Type la Blur](media/blur-effect.png "Chọn Effect Type la Blur")

Hình 4.13: Chọn Effect Type la Blur

1. Chọn Apply, bạn có thể thấy polygon layer lúc này bị mờ.

![Layer với hiệu ứng mờ](media/blurry-result.png "Layer với hiệu ứng mờ")

Hình 4.14: Layer với hiệu ứng mờ

6. Trở lại  **Effects Properties**. Hãy thử nâng cao hơn một chút. Thay vì chỉ chọn một hiệu ứng, có thể chọn cùng lúc nhiều hiệu ứng khác nhau. Hãy chọn thêm hiệu ứng **Drop shadow**

![Effects properties dialogue](media/drop-shadow.png "Effects properties dialogue")

Hình 4.15: Effects properties dialogue

7. Các hiệu ứng sẽ được vẽ từ trên xuống, do đó Drop shadow sẽ hiển thị bên dưới source polygon

![Hiệu ứng Drop shadow](media/drop-shadow-result.png "Hiệu ứng Drop shadow")

Hình 4.16: Hiệu ứng Drop shadow

8. Bạn có thể thêm bao nhiêu hiệu ứng tuỳ ý. Ví dụ một **inner glow** trên  **source effect**, với **drop shadow** ở dưới cùng. Hãy làm thử để xem kết quả thế nào!

Nhìn chung, hãy nhớ rằng các hiệu ứng có thể được áp dụng cho toàn bộ layer hoặc cho các symbol riêng lẻ cho các đối tượng trong một layer. Về cơ bản, các khả năng gần như là vô tận! Các Python plugin cũng có thể bổ sung nhiều hiệu ứng khác nữa..

Để xem thêm ví dụ về những gì có thể làm với Blending Modes và Draw Effects trong QGIS, bạn có thể tham khảo tại đây:
*   Hillshade in QGIS -[https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html](https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html)
*   Mapping Icebergs in QGIS - [https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html](https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html)

### Phase 3: Data defined overrides và geometry generators

#### **Nội dung**

*   Chạy một tính toán không gian trong layer symbology

#### **Hướng dẫn**

A geometry generator là một dạng symbol layer cho phép sử dụng mã để tạo các đối tượng hình học mới từ các đối tượng đã có, và sử dụng các đối tượng hình học mới tạo này như các symbol để tạo style cho layer. Đây là một tính năng mạnh mẽ được giải thích tốt nhất bằng một ví dụ.

Bạn có thể sử dụng geometry generator symbology với tất cả các loại layer (point, line và polygon). Symbol kết quả phụ thuộc trực tiếp vào loại layer.

Rất ngắn gọn, geometry generator symbology cho phép bạn chạy tính toán không gian trong chính symbology. Ví dụ: bạn có thể chạy ra lớp tâm của polygon mà không cần tạo thêm một lớp điểm.

Hơn nữa, bạn có tất cả các tùy chọn styling để thay đổi hiển thị của symbol kết quả. Đây là một hướng dẫn ví dụ;

1. Kích đúp chuột vào HCMC_border layer
2. Kích vào Simple fill và đổi Symbol layer type thành Geometry generator. Trước khi bạn bắt đầu viết câu truy vấn không gian, chọn loại đối tượng đầu ra. Trong ví dụ này chúng ta sẽ tạo tâm điểm của mỗi đối tượng polygon, do đó loại đối tượng là Point/ Multipoint.

![Tính toán tâm của từng polygon trên HCMC_border layer](media/centroid.png "Tính toán tâm của từng polygon trên HCMC_border layer")

Hình 4.17: Tính toán tâm của từng polygon trên HCMC_border layer

3. Khi bạn kích chọn OK, bạn sẽ thấy HCMC_border layer được hiển thị dưới dạng một point layer. Chúng ta vừa chạy một tính toán không gian ngay trong layer symbology.

![Point layer](media/centroid-result.png "Point layer")

Hình 4.18: Point layer

4. Chú ý là một cách thay thế và nhanh hơn là viết các truy vấn không gian sử dụng ‘Expressions dialogue’. Kích vào nút bấm ![alt_text](media/expression.png "image_tooltip") để mở hộp thoại 'Expression string builder'. Tại đây bạn sẽ có quyền truy cập vào tham chiếu chức năng mở rộng. Bạn có thể tìm kiếm một hàm bằng tên. Ví dụ, gõ centroid trong thanh tìm kiếm.
5. Với Geometry generator symbology bạn thực sự có thể vượt qua ranh giới của symbology thông thường.
6. Nếu bạn muốn thực hành thêm, hãy viết một cây truy vấn không gian để tính buffer zone cho lớp điểm, đượng hoặc vùng.


#### **Câu hỏi**

1.N/A


#### **Trả lời**

1.N.A

   