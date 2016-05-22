###flex 实例练习
###   先说一道面试题 
####一
两个div   出现如下图的原因是什么  ，以及如何处理 
![enter image description here](http://images2015.cnblogs.com/blog/933778/201604/933778-20160422190330257-1034408415.jpg)
两个div都设置了  display ：inline-block属性  ，在这里要注意   inline-block 默认的是基线对齐的，而inline-block  的基线 又跟文本基线一致，所以在内容不同的时候不能水平对齐的，这是出现上述问题的原因，在这里只需用 vertical-align显示的声明一下  top/bottom/middle对齐 即可   ,下面要好好的扯扯基线的内容 。
####1在没有文字的情况下
   容器的margin-bottom下边缘。与容器内部的元素没有一毛钱的关系。
####2  在有文字的情况下
 最后一行文字的下边缘，和文字块（p,h）的 margin padding 没有关系  ##这里注意  是最后一行的文字   ，无论文字在什么子对象容器内，在什么位置都没有关系，浏览器会找到最后一行文字对齐底部
 ![enter image description here](http://images2015.cnblogs.com/blog/933778/201604/933778-20160422190331695-1984072728.jpg)
 ![enter image description here](http://images2015.cnblogs.com/blog/933778/201604/933778-20160422190332757-592728431.jpg)
 这里要说一下 display:inline-block  出现两个div 中间的出现4px间隙问题  这个问题是因为我们在写代码的时候的换行符导致的
 解决的办法  在 display  : inline-block 的父元素中设置样式 font-size :0; letter-spacing:-4px;    然后再设置  子元素 div 中的  font-size 和 letter-spacing( 字符间距   默认值为 normal)；
 问题已经解决 ；
###下面介绍  flex  实例问题  
  ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071328.png)
  如上图  一枚筛子 最多能放 九个点  那么下面我们  分别从  1 到 9   用 flex  进行布局
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071301.png)
 div{  display : flex; }
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071302.png)
 div{ display : flex ; justfy-content:center;}
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071303.png)
 div{display：flex ;   justfy-conten:flex-end;}
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071304.png)
 div{display:flex;align-items:center;}
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071305.png)
 div{display:flex;align-items:center;justify-conten:center;}
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071306.png)
 div{display:flex;justfy-align:center;align-items:flex-end}
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071307.png)
 div{display:flex; justfy-align:flex-end;align-items:flex-end;}
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071308.png)
 div{display:flex;justify-content:space-between;}
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071309.png)
 div{display:flex;flex-direction:column;justify-content:space-between;
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071310.png)}
 div{display:flex;flex-direction:column;justify-content:space-between;align-items:center};
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071311.png)
 div{display:flex;flex-direction:column;justify-conten:space-between;}
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071312.png)
 div{display:flex;}  btn2{display:flex;center;align-self:center;}
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071313.png)
 div{display:flex;justify-content:space-between;} btn2{align-self:flex-end}
 ![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071314.png)
 .box {
  display: flex;
}

.item:nth-child(2) {
  align-self: center;
}

.item:nth-child(3) {
  align-self: flex-end;
}
![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071315.png)
.box {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-end;
  align-content: space-between;
}
![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071316.png)

```
<div class="box">
  <div class="column">
    <span class="item"></span>
    <span class="item"></span>
  </div>
  <div class="column">
    <span class="item"></span>
    <span class="item"></span>
  </div>
</div>
.box {
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
}
```

.column {
  flex-basis: 100%;
  display: flex;
  justify-content: space-between;
}
![enter image description here](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071320.png)
.box {
  display: flex;
  flex-wrap: wrap;
}

