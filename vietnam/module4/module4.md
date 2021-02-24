# Module 4 - Styling Layers

**Author**: Quách Đồng Thắng

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
*   Ranh giới hành chính của Tp.HCM (trong  [module4.gpkg](data/module4.gpkg)))
*   Các cơ sở y tế Tp.HCM (trong [module4.gpkg](data/module4.gpkg))
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


Figure 4.2: Symbology tab cho dữ liệu vector và raster


#### **Raster rendering: Band rendering**

QGIS offers four different Render types. The choice of renderer depends on the data type. The default render type is Single band grey color. You’ll have to change it to the appropriate type based on the data type. 

*   Multiband color ([https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#multiband-color](https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#multiband-color)) - if the file comes with several bands (e.g. a satellite image with several bands).
*   Paletted/Unique values ([https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#paletted]()) - for single band files that come with an indexed palette (e.g. a digital topographic map) or for general use of palettes for rendering raster layers.
*   Singleband gray ([https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#singleband-gray](https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#singleband-gray)) - (one band of) the image will be rendered as gray. QGIS will choose this renderer if the file is neither multiband nor paletted (e.g. a shaded relief map).
*   Singleband pseudocolor ([https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#label-colormaptab](https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#label-colormaptab)) - this renderer can be used for files with a continuous palette or color map (e.g. an elevation map).
*   Hillshade ([(https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#hillshade-renderer](https://docs.qgis.org/3.16/en/docs/user_manual/working_with_raster/raster_properties.html#hillshade-renderer)) - Creates hillshade from a band.


#### **Vector rendering**

When you load spatial data layers into QGIS Desktop, they are styled with a random Single Symbol rendering. To change this click on Layer->Properties->Style.

There are several rendering choices available from the menu in the upper left corner:

*   Single Symbol – this is the default rendering in which one symbol is applied to all the features in a layer.
*   Categorized – allows you to choose a categorical attribute field to style the layer with. Choose the field, and click Classify and QGIS will apply a different symbol to each unique value in the field. You can also use the Set column expression button to enhance the styling with a SQL expression.
*   Graduated – allows you to classify the data by a numeric field attribute into discrete categories. You can specify the parameters of the classification (classification type and number of classes) and can use the Set column expression button to enhance the styling with a SQL expression.
*   Rule-based – use this to create custom rule based styling. Rules will be based on SQL expressions.
*   Point displacement – if you have a point layer with stacked points, this option can be used to displace the points so they are all visible.
*   Inverted polygons – this is a new renderer that allows a feature polygon to be converted into a mask. For example, a city boundary polygon used with this renderer would become a mask around the city. It also allows for use of Categorized, Graduated and Rule-based renderers and SQL expressions.


## Main content 

### Phase 1: Basic raster and vector symbology

Vector data symbology may vary by transparency, color, rotation, and size.  

#### **Content**

*   Layer properties and symbology menu
*   Types of vector rendering
*   Types of raster rendering (band rendering)

#### **Example 1: Vector rendering**

1. To demonstrate this example, we’ll use two example datasets; 1. [Clinics](https://drive.google.com/file/d/1iJQ1nP0ulA96OhyT9wakRheahYKnNmjc/view?usp=sharing) and 2. [Administrative boundary](https://drive.google.com/file/d/1GiFmr4As5e-yn-4lCqotAzUBHzXU1NS_/view?usp=sharing) of Pampanga province 
2. Add the two vector layers into qgis; Click the Add vector layer button ![alt_text](media/add-vector.png "image_tooltip")
 or use the browser panel. 
3. This is how they render by default. You’ll notice we have a polygon and point layer. The next step is to change the symbology for each of them. Fill colors may not be the same, but that’s not a problem because QGIS selects colors randomly for different instances of the application.

![Default render](media/default-vector-render.png "Default render")

Figure 4.3: Default render

4. Double click the polygon vector layer, which is also the administrative boundary layer of Pampanga province in the Philippines
5. Select the **Symbology Tab** in the menu that appears
6. Change the **Fill color** to **Transparent fill. Tip:** Click the drop down arrow under Fill color
7. The result should be as below. You may notice that the no fill option has no color

![No fill rendering for the polygon](media/no-fill-render.png "No fill rendering for the polygon")

Figure 4.4: No fill rendering for the polygon

8. The next step is to symbolize the point layer which is also the Clinics layer
9. Double click the **Clinics layer** to open the **Layer Properties** dialogue. Change the render type from Single Symbol to **Categorized**, Select the **Value** as amenity. The value represents the field of interest. Specify the Symbol and Color ramp. Then Click classify.

![Layer Properties dialogue](media/vector-style.png "Layer Properties dialogue")

Figure 4.5: Layer Properties dialogue

10. The resulting map should look as below

![Final vector render](media/final-vector-render.png "Final vector render")

Figure 4.6: Final vector render



11.  Remember to arrange the layers in the **Layer Panel** in such a way that the polygon layer is below the point layer. This makes the point layer visible.


#### **Example 2: Raster rendering**

1. Double click the raster layer which is also the population density layer. This also means it’s a normalized dataset and can therefore be visualized as a choropleth map.
2. Select the symbology tab in the menu that appears
3. Change the styling mode to ‘Singleband pseudocolor’

![Symbology menu](media/qgis9.png  "Symbology menu")

Figure 4.7: Symbology menu

4. Specify the interpolation, color ramp and mode. Click classify. The result is a choropleth map showing population density across Pampanga province in the Philippines.

![Population density of Pampanga Province, Philippines](media/hrsl-style.png "Population density of Pampanga Province, Philippines")

Figure 4.8: Population density of Pampanga Province, Philippines

5.  Zoom in to see the new map in finer detail.

![Zoomed-in map](media/zoom-in.png "Zoomed-in map")

Figure 4.9: Zoomed-in map

6. Alternatively, use the **Layer Styling panel**.

#### **Quiz questions**

1. What is layer symbology?
2. Which of the rendering types below are applicable for vector data?
3. What are the types of raster rendering

#### **Quiz answers**

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

4. d. multiband color


### Phase 2: Blending modes and draw effects

#### **Content**

*   Altering symbol structures
*   Altering draw effects and blending modes
*   Impactful visualisation of data

#### **Tutorial**

1. After loading the two layers into QGIS, the canvas will look as below. You’ll notice that both layers have plain styling. This tutorial will explain how to alter draw effects and blending modes for better visualization.
   
![The expected initial workspace](media/initial-workspace.png "The expected initial workspace")

Figure 4.10: The expected initial workspace

2. Open the Layer Properties window, then click the Symbology menu item for the administrative boundaries layer. Tip: Do this by double clicking the layer or use the layer styling panel. Enable the layer styling panel by clicking: View -> Panels -> Layer Styling. 

At the bottom of the Symbology menu, there’s a checkbox for Draw effects. Let’s enable that, and then click the customise effects button ![alt_text](media/customise-effects-button.png "image_tooltip") to its right:

![Layer Properties window and Symbology menu](media/draw-effects.png "Layer Properties window and Symbology menu")

Figure 4.11: Layer Properties window and Symbology menu

3. A new Effects Properties dialog opens

![Effects properties dialogue](media/new-effects-dialog.png "Effects properties dialogue")

Figure 4.12: Effects properties dialogue
   
4. You can see that currently the only effect listed is a Source effect. Source effects aren’t particularly exciting – all they do is draw the original layer unchanged. Change this to a Blur effect by **clicking the Effect type  combo box and selecting Blur**. You can then play around with the blur parameters.

![Select effect type as blur](media/blur-effect.png "Select effect type as blur")

Figure 4.13: Select effect type as blur

5. Apply the settings now, you’ll see that the polygon layer is now blurry. Now we’re getting somewhere!	

![Blurry layer](media/blurry-result.png "Blurry layer")

Figure 4.14: Blurry layer

6. Using the **Effects Properties** dialog again. Let’s try something a bit more advanced. Instead of just a single effect, it’s possible to chain multiple effects together to create different results. Let’s make a traditional drop shadow by adding a **Drop shadow** effect under the **Source** effect.

![Effects properties dialogue](media/drop-shadow.png "Effects properties dialogue")

Figure 4.15: Effects properties dialogue

7. Effects are drawn top-down, so the drop shadow will appear below the source polygons

![Drop shadow effect](media/drop-shadow-result.png "Drop shadow effect")

Figure 4.16: Drop shadow effect

8. You can stack as many effects as you like. For example an **inner glow** over a **source effect**, with a **drop shadow** below everything. Try it out!

Overall, remember that effects can either be applied to an entire layer, or to the individual symbol layers for features within a layer. Basically, the possibilities are almost endless! Python plugins can also extend this further by implementing additional effects.

For more examples about what you can do with Blending Modes and Draw Effects in QGIS, you can check out:
*   Hillshade in QGIS -[https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html](https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html)
*   Mapping Icebergs in QGIS - [https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html](https://bnhr.xyz/2019/02/08/mapping-icebergs-in-qgis.html)

### Phase 3: Data defined overrides and geometry generators

#### **Content**

*   Run a spatial operation within the layer symbology

#### **Tutorial**

A geometry generator is a symbol layer type that lets you use code to create new geometries from existing features, and use the new 'generated' geometries as symbols that can, in turn, have styles applied. This is a powerful feature best explained with an example.

You can use the geometry generator symbology with all layer types (points, lines and polygons). The resulting symbol depends directly on the layer type.

Very briefly, the geometry generator symbology allows you to run some spatial operations within the symbology itself. For example you can run a real centroid spatial operation on a polygon layer without creating a point layer.

Moreover, you have all the styling options to change the appearance of the resulting symbol. Here’s an example tutorial;

1. Double click the administrative boundary layer
2. Click on Simple fill and change the Symbol layer type to Geometry generator. Before you start writing the spatial query, choose the Geometry Type in output. In this example we are going to create centroids for each feature, so change the Geometry Type to Point / Multipoint.

![Centroid operation on administrative boundary layer](media/centroid.png "Centroid operation on administrative boundary layer")

Figure 4.17: Centroid operation on administrative boundary layer

3. When you click on OK you will see that the administrative layer boundary is rendered as a point layer. We have just run a spatial operation within the layer symbology itself.

![Point layer](media/centroid-result.png "Point layer")

Figure 4.18: Point layer

4. Note that an alternative and easier way of writing spatial queries is using the ‘Expressions dialogue’. Click the ![alt_text](media/expression.png "image_tooltip")
 expressions  button to open the 'Expression string builder' dialogue box. Here you’ll have access to an extensive function reference. You can search for a function by name. For example, type centroid in the search bar.
5. With the Geometry generator symbology you can really go over the edge of normal symbology.
6. If you want to go further, write a spatial query to calculate a buffer zone around the point, line or polygon layer. 


#### **Quiz questions**

1.N/A


#### **Quiz answers**

1.N.A

   