## Flex 布局
#####Flex是Flexible Box的缩写 意为弹性布局，用来为盒状模型提供最大的灵活性，任何一个容器都可以指定为Flex布局。
#####方法 
在容器中 加上  display :flex  
#######重要的事情说一遍  webkit 加上webkit 前缀
行内元素使用 flex布局   display：inline-flex
![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)
####采用Flex容器 ，简称“容器”它的所有子元素自动成为容器成员，成为Flex 项目
容器中存在两根轴， 水平的主轴  和垂直的交叉轴，主轴的开始位置叫做main start   结束位置叫做 main end,交叉轴开始的位置叫做cross start 结束位置叫做  cross end  ,项目默认沿主轴排列，单个项目占据的主轴空间叫做main size  占据的交叉轴空间叫做 cross size
####容器的属性
######flex-direction
#####flex-wrap
#####flex-flow
#####justify-content
#####align-items
#####align-content
####flex-firection属性
### flex-direction
flex-direction 属性决定主轴的方向
（即项目的排列方向）
它总共包括四个属性  row||row-reverse||column||column-reverse;
![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)
row   水平方向  起点在左端。
row-reverse   水平方向 ，起点在右端
column 垂直方向  起点在上边
column-reverse 垂直方向  起点在下边
###flex-wrap
flex-wrap 属性默认都排在一条线上，如果一条线排不下，换行。
#####它有三个属性值  nowrap ||  wrap || wrap-reverse
######nowrap   为默认值  不换行
#####wrap     换行，第一行在上方
#####wrap-reverse  换行 ，第一行在下方
###flex-flow 
 flex-flow 是flex-direction 属性和flex-wrap属性的简写形式默认值为 row nowrap
###  justify-content
 justify-content属性定义了项目在主轴上的对齐方式。
 其包含五个属性。
 flex-start    ||  flex-end   ||  center   ||   space-between || space-around;
 flex-start  左对齐
 flex-end   右对齐 
 cneter  居中
 spance-between  两端对齐 ，项目之间的间隔都相等
 spance -around:  项目两侧的间隔相等。 所以项目之间的间隔比项目与边框的间隔大一倍。
###align-items
 align-items属性定义项目在交叉轴上如何对齐。
flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)
## 项目属性
### order  flex-grow flex-shrink  flex-basis  flex   align-self  
####order属性定义项目的排列顺序 。数值越小，排列越靠前，默认值为0.
####flex-grow属性定义项目的放大比例，默认为0 ,即如果存在剩余空间 ，也不放大。
####flex-shrink属性定义了项目的缩小比例，默认为1 ，如果空间不足，改项目将缩小。
####flex-basis 定义了在分配多余空间之前，项目占据的主轴空间。浏览器根据这个属性计算主轴是否有多余空间，它的默认值为 auto.
###flex 属性 
flex 属性是flex -grow ,flex-shrink,  和 flex-basis 的简写  其默认值 为 0  1   auto  
###align-self 属性 
align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性，默认值为 auto,继承父元素的 align-items属性，如果没有父元素，则等同于 stretch 
## 对 垂直对齐  vertical-align的一些认识
从  w3c的解释中可看出  
vertical - align  属性 会影响到由内联元素产生的行内框的垂直位置 
#####首先说明一下  vertical-align 的使用前提
这个便签只能用于 行内元素和表单单元格元素，因此对于那些块级元素  并不能使用   
####text-align  属性让块级元素中的内联文本水平对齐  
###baseline
一个元素的基线与父元素的基线对齐，这个是默认值，这是在默认段落行高一样的情况下可说，假如是替换元素，那么这就是与图像的基线对齐。

 


