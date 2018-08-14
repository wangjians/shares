## js源码分析——SuperMap ##
##需求来源
webgis全套打通
##参考手册
[http://iclient.supermapol.com/libs/iclient8c/apidoc/files/SuperMap/Map-js.html](http://iclient.supermapol.com/libs/iclient8c/apidoc/files/SuperMap/Map-js.html)         
SuperMap.js为北京超图公司的产品，以上链接内有开发指南、示范程序、类参考，也有类结构图，但模糊不清。
##源码地址
[https://github.com/kalaslib/shares/tree/master/源码分析/js](https://github.com/kalaslib/shares/tree/master/源码分析/js)     
选择SuperMap-6.1.3-10027.js
##类继承结构
[https://github.com/kalaslib/shares/tree/master/源码分析/js](https://github.com/kalaslib/shares/tree/master/源码分析/js)     
选择SuperMap.xmind，黑框为正常结构，红框为业务定制    
XMind为思维导图绘画工具，可前往[下载](https://www.xmind.net/zen/thank-you-for-downloading/)
####主要模块
	- Map 			地图，根据DOM元素的ID添加地图实例，低版本浏览器使用SVG,正常则是Cavas
	- Layer			图层，主要分三类，矢量底图CanvasLayer，点位图层Markers，矢量要素Vector
	- Marker		点位，由图标img、标签babel组成，通过图标改变，切换正常、选中等状态，img元素决定了大数据量点位时会很卡（每次加载图片都重新发起http请求）
	- Feature		矢量要素，有点、线、矩形、圆、多边形等矢量图形，大数据量或做动画时可用点代替点位
	- Popup			气泡，即点位或要素的弹窗，根据输入的html和基点在地图方位，从不同方向展示
	- Geometry		地理要素，图形的基础集合，有点、线、多边形等
	- Handler		事件，除了正常的DOM事件，集中在画图和拖拽事件
	- Control		控件，地图上的各类操作面板，有导航、鹰眼、鼠标、图层切换等
	- REST			服务端地图，通过服务器端封装了大量图层操作，所以一个简单搭建了tomcat跑着5个jar包的超图gis服务器卖8000块
####其他基本要素
	- Projection 	坐标系，坐标系转换完全依赖于开源gis坐标系转换的Proj4js.js库
	- Bounds		范围，左下、右上两点组成
	- LonLat		经纬，经度和纬度组成
	- Pixel			像素，平面坐标
	- Size			图标大小，长、宽
	- Style			矢量样式，与Cavas样式完全一一对应
	- Icon			图标样式，图标的地址、旋转等
	- Util			工具类
####定制要素
	- CanvasLayer	Baidu,acgis,edushi,google,tianditu的父类，定制展示级别，分辨率，瓦片地址，边界范围
	- Markers		DHMarkers的父类，定制点位的选中、高亮、显藏、聚合、标记、层高
	- Vector		DHVector的父类，定制要素的选中、高亮、显藏、标记
	- Marker		DHMarker、DHText、DHCloseableText、DHCloseIcon、DHDrawClosableText的父类，定制点位的图标大小、文本标签
	- FramedCloud	DHFramedCloud的父类，定制气泡的大小、平移、方位、关闭键等效果
	- Point			DHPoint的父类，定制点的拖拽、鼠标、滚轮等事件
	- Path			DHPath的父类，定制线段的拖拽、重画、返回等事件
	- RegularPolygon DHRegularPolygon、DHCircle的父类，定制多边形、圆的选择、范围判断等事件
##总结
看得出，总体SuperMap类的设计还是非常完备的，基本可满足企业产品化定制，但仅仅是完备，总体功能偏少，接下来研究另一个更出名的开源产品[点击前往下一篇js源码分析——OpenLayers](http://www.baidu.com)