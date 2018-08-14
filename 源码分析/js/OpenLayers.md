## js源码分析——OpenLayers ##
##需求来源
webgis全套打通
##参考手册
[http://www.openLayers.cn/cnapi/files/OpenLayers/BaseTypes-js.html](http://www.openLayers.cn/cnapi/files/OpenLayers/BaseTypes-js.html)     
OpenLayers是开源webgis的js产品，开源决定了其广泛的包容性。
##源码地址
[https://github.com/kalaslib/shares/tree/master/源码分析/js](https://github.com/kalaslib/shares/tree/master/源码分析/js)     
选择OpenLayers.debug-2.12-Release.js
##类继承结构
[https://github.com/kalaslib/shares/tree/master/源码分析/js](https://github.com/kalaslib/shares/tree/master/源码分析/js)     
选择OpenLayers.xmind    
XMind为思维导图绘画工具，可前往[下载](https://www.xmind.net/zen/thank-you-for-downloading/)  
> ######与SuperMap对比  
> SuperMap.js为北京超图公司的产品，不了解的可以查看[上一篇：js源码分析——SuperMap](http://www.baidu.com)    
> 从类结构可以看出，OpenLayer与SuperMap非常相似，本人在分析源码时这种感觉非常强烈，最后惊觉，SuperMap大部分结构完全抄自OpenLayer，个别方法在OpenLayer标明作者，但在SuperMap中一模一样存在。    
> 所以OpenLayer有更完备的结构，代码量也是SuperMap三倍以上。
####主要模块
	- Map 			地图，根据DOM元素的ID添加地图实例，低版本浏览器使用SVG,正常则是Cavas
	- Layer			图层，主要分三类，矢量底图Grid，点位图层Markers，矢量要素Vector
	- Marker		点位，由图标img、标签babel组成，通过图标改变，切换正常、选中等状态，img元素决定了大数据量点位时会很卡（每次加载图片都重新发起http请求）
	- Feature		矢量要素，有点、线、矩形、圆、多边形等矢量图形，大数据量或做动画时可用点代替点位
	- Popup			气泡，即点位或要素的弹窗，根据输入的html和基点在地图方位，从不同方向展示
	- Geometry		地理要素，图形的基础集合，有点、线、多边形等
	- Handler		事件，除了正常的DOM事件，集中在画图和拖拽事件
	- Control		控件，地图上的各类操作面板，有导航、鹰眼、鼠标、图层切换、选中、表格线、定位等超过30种控件
	- Format		转化器，接受XMl、Json、Text等格式的数据进行格式转化，因SVG是用xml描述逻辑的，Cavas则是js
	- Filter 		过滤器，筛选点位、要素达到控制效果
	- Strategy		策略，地图的整体事件，有刷新、聚合、修复、保存等
####其他基本要素
	- Projection 	坐标系，坐标系转换完全依赖于开源gis坐标系转换的Proj4js.js库
	- Bounds		范围，左下、右上两点组成
	- LonLat		经纬，经度和纬度组成
	- Pixel			像素，平面坐标
	- Size			图标大小，长、宽
	- Style			矢量样式，与Cavas样式完全一一对应
	- Icon			图标样式，图标的地址、旋转等
	- Event			事件，点击、双击等
	- Rule			规则，统一的样式属性
	- Tile			瓦片，图片、网格
	- Renderer		渲染方式，Cavas、SVG
	- Protocal		协议，Js、Http
	- Util			工具类
####定制要素
	- Grid			Bing、KaMap、WorldWind、ArcGis93Rest的父类，定制展示级别，分辨率，瓦片地址，边界范围
	- Markers		DHMarkers的父类，定制点位的选中、高亮、显藏、聚合、标记、层高
	- Vector		DHVector的父类，定制要素的选中、高亮、显藏、标记
	- Marker		DHMarker、DHText、DHCloseableText、DHCloseIcon、DHDrawClosableText的父类，定制点位的图标大小、文本标签
	- FramedCloud	DHFramedCloud的父类，定制气泡的大小、平移、方位、关闭键等效果
	- Point			DHPoint的父类，定制点的拖拽、鼠标、滚轮等事件
	- Path			DHPath的父类，定制线段的拖拽、重画、返回等事件
	- RegularPolygon DHRegularPolygon、DHCircle的父类，定制多边形、圆的选择、范围判断等事件
	- Control		DHOverviewMap、DHPanZoomBar、DHModifyFeature、DHNavigation、DHDrawFeature的父类，定制鹰眼、导航、绘画等
	- Icon			DHIcon的父类，定制图标的边框、旋转、阴影等样式
##总结
OpenLayers是一个大而全的优秀的开源地图js包，在es6语法下也更新很快，npm引入使用即可。