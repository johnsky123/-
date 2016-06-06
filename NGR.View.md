## NGR.View
NGR.View是室内地图API的核心部分，它会被用来在页面上创建室内地图并维护其的状态。
简单用例：
var map=NGR.view('map',{
center:[31,121],
zoom:21
});
####创建地图

```
NGR.View( HTML Element || String || id || <Map Options> options)
```
描述  ：在指定的元素上初始化室内地图，id 可以使一个HTMLElement ,也可以是某个元素的 id ,在初始化时，可以指定一些可选的选项。
####选项
######与授权相关的选项
AppKey    String 类型   默认为null   描述 由开放平台分配的APPKey
####与地图状态相关的选项
 center  zoom   layers  minZoom  maxZoom  
 maxBounds   这些的默认值都为 null   
#####与交互相关的选项
dragging   touchZoom   scrollWheelZoom   doubleClickZoom  box Zoom   closePopupOnClick  
这些值的类型都为布尔值 默认值都为 true 
######与键盘导航相关的选项
keyboard  值为boolean  默认为 true  次选项可以使用地图能够获取焦点并允许用户使用键盘的方向键进行导航
keyboardPanOffset  指定使用键盘方向键移动地图时每次平移的像素数
keyboardZoomOffset  指定当使用 + -  缩放地图时每次缩放的级数
####与控件相关的选项
zoomControl
指定是否默认加载地图缩放控件
####事件
可以通过下面的方法来订阅事件
click  dbclick  mousedown  mouseup mouseover mouseout mousemove contextmenu focus blur 
preclick load upload viewreset movestart move moveend drag dragend zoomstatrt zoomend zoomlevelchange resize autopanstart layeradd layerremove pupupen popupclose 
###与修改地图状态相关的方法
setView( )  setZoom ( ) zoomIn( ) zoomOut( )
setZoomAround( )   fitBounds( ) panTo( )
panInsideBounds( ) panBy( ) setMaxBounds( )
setMinZoom( )
setMaxZoom( )
remove( )
####与获取地图状态相关的方法
getCenter( )  getZoom( ) getMinZoom( ) getMaxZoom ( )   getBounds( ) getBoundsZoom( )
getSize( )返回当前地图容器的大小   getContainer( )  返回当前地图所在的容器
####与图层和控件相关的方法

addLayer(  ) 向地图中添加给定的图层
removeLayer( ) 从地图中移除给定的图层
hasLayer( ) 如果给定的图层已经被添加到了地图中则返回 true  
eachLayer (  ) 遍历室内地图中的所有图层，可以为遍历函数指定一个可选的上下文环境
openPopup( ) 关闭地图上所欲现存的气泡并打开一个新的气泡
openPopup( )使用特定的选项配置并在啊地图上特定位置打开弹出气泡
closePopup( )关闭所有使用openPopup 打开的气泡，或指定一个要关闭的气泡
addControl  添加一个指定的地图控件
removeControl 移除指定的地图控件
####与坐标转换相关的方法
latLngToContainerPoint( )  返回与给定地理坐标相对应的地图容器坐标点
containerPointToLatLng( )返回与给定屏幕坐标相对应的地理坐标点
mouseEventContainerPoint( )
返回鼠标事件相对于地图容器的像素坐标点
mouseEventToLatLng( )返回鼠标实际对应的地理坐标点
###与渲染相关的方法
render(  )    将地图缩放到合适的大小并渲染地图
clear （ ）清空所有的图层
###NGR.Marker
用来向地图中添加一个标记
例如 ：   NGR.marker( [31.1,121.1]).addTo(map);
###创建方法
NGR.marker( )使用给定的地理坐标和选项创建并实例化一个标记
####选项
icon    类型    NGR.Icon 用来渲染Marker的图标 可以查看NGR.Icon 的文档来获取更多的相关文档，如果没有指定，则默认为NGR.Icon.Deafult( )
clickable 如果设为false Marker 将不会响应任何鼠标事件
draggable配置Marker能否被鼠标或触摸拖动
keyboard 配置Marker 是否可以通过tab获取焦点并通过Enter点击
title  alt   zIndexOffset  opacity  riseOnHover  如果被设为true Marker 会在被鼠标覆盖是移至最上方。
riseOffset  riseOnHover   属性要使用zIndex 值
####交互处理器

交互处理器是Marker 实例的一个属性，可以通过它在运行时可以改变交互行为，启用或关闭诸如拖动之类的操作  例如  marker.dragging.disable( )
###NGR.Popup
popup被用来在地图上某个特定点打开一个气泡，可以使用map.openPopup( )以单例模式打开一个气泡，或使用map.addLayer( )添加气泡，
如果只想在Marker点击时打开一个气泡，只需执行这行代码：
marker.bindPopup( popupContent).openPopup( )
也可以使用稍微复杂的方法

```
var popup = NGR.popup( )
                .setLatLng( latlng)
                .setContent('<p>Hello World</p')
                .openOn(map)
```
### NGR.ImageOverlay
用来在地图上的特定区域内显示一张图片，该类实现了ILayer接口。
用法 ：   var  img =" path/to/image.png",
bounds=[[31,121],[32,122]];
NGR.imageOverlay(img,bounds).addTo(map);
###选项 opacity   
图片浮层的透明度
###NGR.LayerGroup
layerGroup 可以将多个图层归为一组，可以将这个组添加到地图中去。添加后任何对组的操作都将反映在地图上。
简单用例
NGR.layerGroup( [marker1,marker2]).addLayer(marker3).addTo(map)
###NGR.FeatureLayer
NGR.FeatureLayer 可以解析由开放平台提供的数据，为其赋予样式并将其转换为地图图层，设定样式时，可以以编程的方式动态设定，也可以通过配置文件的方式进行设定。
用法：
NGR.featureLayer(data,{
styleConfig:config
}).addTo(map);
###创建方法
NGR.featureLayer( ) 根据给定的图层数据和选项创建地图图层

###选项  
styleConfig   样式配置对象
layer_type   显示指定图层类型，覆盖数据中携带的图层类型
pointToLayer   指定地图数据中“点”数据类型的处理函数，该函数要求返回一个图层，如果没有指定，默认将“点”转换为  Marker   函数的参数  feature为开发平台提供 的内容，latlng为点的地理坐标。
style   指定地图数据的样式处理函数或样式内容。若提供一个函数，则要求返回一个包含渲染样式的object   若提供的是一个object  则直接包含渲染样式。

