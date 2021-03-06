前段时间花时间看了大半的《High Performance JavaScript》这本书啊，然后就开始忙项目了，庆幸最忙的一周已经熬过去了。由于空不出时间，这个月写的学习笔记也不多，忙完最苦X的一周，这两天晚上也算是挑灯夜读了...终于是在残血之际将这本书shut down了...
既然读完了，总归是要学到些什么的。说说对这本书的看法先吧，整体的来说，内容还是不错的，就是感觉有点老了（作为前端小白，也可能是自身水平有限，未能体会到其中真意）。看这本书的过程中也是写了挺多代码用以测试的，并且对本书提倡的写法和原先大众的写法的执行分别进行了断点跟踪，对于能实际测出的问题进行理解，当然，下断点跟着执行也看不出的那也没办法咯。对于书中的知识点，这里只是简单的整理出个人所推崇的一部分，当然~ 不喜勿喷。
###针对js文件的加载位置
在HTML文件中 `<script>`标签是可以加在`<head>`区域和`<body>`区域的。这里鉴于JavaScript执行和UI渲染的单线程原因，如果js文件载入会阻塞后面对于页面的解析过程，页面会等到js文件完全加载并运行后才继续执行该做的操作。那么问题就来了，这样可能会出现页面空白or卡顿现象。作为一名前端开发，重要的不仅仅止于实现了需求，应该还有优质的用户体验。那么我们就需要消除用户枯燥的等待，针对这个问题，这里有本兽想到的两种解决方案：
1. 如果js文件没有特殊要求指明需要在页面渲染之前载入及编译完成的，那么选择将js文件放到`</body>`标签前(既所有的页面所呈现内容的后面)，css文件还是放到`<head>`区域(谁也不愿意看一个布局杂乱无章的页面)。这样做就能先让用户看到有布局的页面而不是空白页了，那么也会有人指出：那数据得通过js请求加载进来啊，怎么办呢？可以对数据的加载做排序，急需呈现的接口放前面执行，不是那么需要的可以延后执行，同时做个简单的载入动画or提示。
2. 如果这些js文件有指明需要先执行了，才能更好的展示页面内容，那么就在第一个js或者页面上先放个载入小动画，可以一些有趣的或者萌萌的动画场景。这样也是能较好的避免用户等待的无聊，说不定人家还对这个载入动画更感兴趣呢，这样可提升项目的用户体验感。
最终推荐：将`<script>`标签尽可能的放到`</body>`标签前面加载，以提升用户体验。
###针对js文件的合并
在很多团队开发中，我们可能会将不同功能的代码块分别放置在不同的js文件中，以便于开发过程中众人合作写代码会更加方便，毕竟只需要找对应文件夹或文件而不是在一个很长的文件中找一个方法。这确实是会提高团队开发效率及新人加入后的更容易进行二次开发及维护。那么将这个问题放到页面性能里呢？这正是问题所在，在这本书中指出：Each HTTP request brings with it additional performance overhead,so downloading one single 100 KB file will be faster than downloading four 25 KB files.
下载1个100KB的文件比下载4个25KB的文件要快，而开发过程中区分开各个文件又有很大的好处，那么合并这个问题也就放在开发完后再处理咯，相信这个操作大家都不会陌生吧，现在的前端工具这么丰富，各位习惯用什么压缩就用什么压缩吧~
这里简单提出下，在载入文件方面还可以用到defer和async属性，用于延迟加载和异步加载，在现代浏览器中，大多数是已经支持defer属性了，还没习惯用这个额，也不知道具体会不会存在什么问题。有兴趣的朋友可自行google该知识点，这里件简单提下吧。
现在的框架也大多配合懒加载和按需加载了。
更快速的数据访问
对于浏览器来说，一个标识符所处的位置越深，去读写他的速度也就越慢(对于这点，原型链亦是如此)。这个应该不难理解，简单比喻就是：杂货店离你家越远，你去打酱油所花的时间就越长... 熊孩子，打个酱油那么久，菜早烧焦了 -.-~
如果我们需要在当前函数内多次用到一个变量值，那么我们可以用一个局部变量先将其存储起来，案例如下：

```
//修改前 function showLi(){ var i = 0; for(;i<document.getElementsByTagName("li").length;i++){ //一次访问document console.log(i,document.getElementsByTagName("li")[i]); //三次访问document }; }; //修改后 function showLi(){ var li_s = document.getElementsByTagName("li"); //一次访问document var i = 0; for(;i<li_s.length;i++){ console.log(i,li_s[i]); //三次访问局部变量li_s }; };
```

###DOM操作的优化
众所周知的，DOM操作远比javascript的执行耗性能，虽然我们避免不了对DOM进行操作，但我们可以尽量去减少该操作对性能的消耗。
让我们通过代码解释这个问题：

```
function innerLi_s(){ var i = 0; for(;i<20;i++){ document.getElementById("Num").innerHTML="A"; //进行了20次循环，每次又有2次DOM元素访问：一次读取innerHTML的值，一次写入值 }; };
针对以上方法进行一次改写：
function innerLi_s(){ var content =""; var i = 0; for(;i<20;i++){ content += "A"; //这里只对js的变量循环了20次 }; document.getElementById("Num").innerHTML += content; //这里值进行了一次DOM操作，又分2次DOM访问：一次读取innerHTML的值，一次写入值 };
```

###减少Dom的重绘重排版
元素布局的改变或内容的增删改或者浏览器窗口尺寸改变都将会导致重排，而字体颜色或者背景色的修改则将导致重绘。
对于类似以下代码的操作，据说现代浏览器大多进行了优化(将其优化成1次重排版)：

```
//修改前 var el = document.getElementById("div"); el.style.borderLeft = "1px"; //1次重排版 el.style.borderRight = "2px"; //又1次重排版 el.style.padding = "5px"; //还有1次重排版 //修改后 var el = document.getElementById("div"); el.style.cssText = "border-left:1px;border-right:2px;padding:5px"; //1次重排版
1.Dom先隐藏，操作后再显示 2次重排 (临时的display:none)
2.document.createDocumentFragment() 创建文档片段处理，操作后追加到页面 1次重排
3.var newDOM = oldDOM.cloneNode(true)创建Dom副本，修改副本后oldDOM.parentNode.replaceChild(newDOM,oldDOM)覆盖原DOM 2次重排
```

循环的优化

```
这应该是较多人都知道的写法了，简单带过即可(后面还是用代码+注释形式说明)~
//修改前 var i = 0; for(;i<arr.lengthli++){ //每次循环都需要获取数组arr的length console.log(arr[i]); } //修改后 var i = 0; var len = arr.length; //获取一次数组arr的length for(;i<len;i++){ console.log(arr[i]); } //or var i = arr.length;; for(;i;i--){ console.log(arr[i]); }
```

###合理利用二进制
如：对2取模，则偶数最低位是0，奇数最低位是0，与1进行位与操作的结果是0，奇数的最低位是1，与1进行位与操作的结果是1。
代码如下：

```
.odd{color:red} .even{color:yellow}
<ul> <li>1</li> <li>2</li> <li>3</li> <li>4</li> <li>5</li> <li>6</li> </ul>
var i = 0; var lis = document.getElementsByTagName("li"); var len = lis.length; for(;i<len;i++){ if(i&1){ lis[i].className = "even"; } else{ lis[i].className = "odd"; } };
```

虽说现代浏览器都已经做的很好了，但是本兽觉得这是自己对代码质量的一个追求。并且可能一个点或者两个点不注意是不会产生多大性能影响，但是从多个点进行优化后，可能产生的就会是质的飞跃了~
查看原文
