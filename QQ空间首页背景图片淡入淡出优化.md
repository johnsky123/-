PK
     á�H��C�<  <     Untitled.md一件事情的发生总是有原因的，当然更多的是对技术本身的追求，一定要搞懂啦，废话不多说，大宝剑直插主题。

起因
以前做过一个xx项目，在登陆界面背景图片中，直接引用了一张大图，css类似于这样(background-image:url(a.jpg))，然后啪啪啪调试了一下，丑恶的面容出来，图片是从上往下一片一片的出来，交互和用户体验差到了极点，特别在网速不好的时候特别明显。（不建议测试图片使用恐怖图片，效果你懂滴，嘿嘿嘿）
有一次突然的机会看到QQ空间背景图片，看到背景图片的显示是那么的优雅，那么的淡然。心里哭着想到，妈的终于找到解决的问题了，但是由于各种不可抗拒的原因一直推迟研究，知道这几天才翻出来，把QQ空间源代码抠出来研究了一番。效果图比较：
![enter image description here](http://images2015.cnblogs.com/blog/801930/201605/801930-20160527103939741-1682934442.png)
![enter image description here](http://images2015.cnblogs.com/blog/801930/201605/801930-20160527104049819-1524255197.png)
具体大家可以自己设置个大图做测试，和进QQ空间登陆首页进行测试

 

原理
佛说有因必有果，所以出现这个状况肯定是有原因的。所以主要原因还是浏览器的渲染问题，浏览器是从上往下进行页面渲染的，当你设置background-image的时候，浏览器就解析这个属性，然后去下载这个图片。但是由于图片一般都不会太小，所以浏览器不可能一次性将文件请求过来，所以请求了多少渲染多少，所以就像拉窗帘式的一点点的下来，直到请求完了，全部渲染完成。通俗一点的例子就是浏览器解析div和table的效果，div是有多少我渲染多少，但是table你必须全部加载完我再渲染

 

研究过程
1.　 首先去QQ空间首页，使用chrome的Network工具监控所有请求的js文件，发现不是很多的混淆后的js文件和一个不断刷新二维码的请求，这样没有找到有用的，值得看的东西（混淆的东西格式化了之后没看出啥玩意，哈哈）。
![enter image description here](http://images2015.cnblogs.com/blog/801930/201605/801930-20160527110149569-966331067.png)
2.　但是俺不气馁，然后在Element中检查dom和style，开始发现好玩的东西了，空间中所使用的背景并不是使用background-image来实现的，它是一个div，然后检查这个div的样式，以及`<img>`标签的样式，然后我不断调试这些样式（就是一个一个的撤销再加载），最后发现当我撤销opacity: 1;样式的时候，背景图片开始淡出了，然后再点又开始淡入，好了，发现重点了！！！
![enter image description here](http://images2015.cnblogs.com/blog/801930/201605/801930-20160527110716553-267844478.png)　　　　
3.　开始仔细关注着几个标签的样式，发现罪魁祸首是css3的opacity和transition属性。前端开发的应该不陌生，一个是透明度，一个是旋转变换（....旋转变换我闭着眼...妈的，都快唱起来了）。可以看效果
![enter image description here](http://images2015.cnblogs.com/blog/801930/201605/801930-20160527111523038-1473081732.png)
4.　作为一个严谨，对自己代码负责的工程师，我将QQ空间的首页拿到不同浏览器进行测试，最主要就是IE，因为其他浏览器装的话，默认都是最新版本，几乎都支持CSS3的属性了，只有IE这个傻Ⅹ才会这么多事，虽然IE6退出了市场，但是IE8-9还是有很多人用的，在IE下测，出现问题了，图片出现再也没有那么装逼的淡出效果了，检查了一下IE8中 渲染不出opacity和transition，IE9渲染不出transition，所以坑爹呀。至于图片不是一块一块加载，稍微查了下QQ空间在页面中写的js，使用的延迟加载。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body{
            margin: 0;
            padding: 0;
            border: 0;
        }
        .backgroundShow{
            position: absolute;
            left: 0;
            top: 0;
            z-index: -1;
            overflow: hidden;
            width: 100%;
            height:100%;
        }
        .backgroundImg{
            position: absolute;
            left: 0;
            top: 0;
            z-index: -2;
        }
        .showImg{
            opacity: 1;
        }
 
        .lay_background_img{
            transition: opacity 2s ease;
            opacity: 0;
        }
    </style>
</head>
<body>
    <div id="showImg" class="backgroundShow">
        <img id="ImgShow" class="lay_background_img backgroundImg">
    </div>
</body>
<script src="lib/test.js"></script>
<script>
    +function(){
        loadImage('http://z.k1982.com/show_img/201303/2013033012383895.jpg',imgLoaded);
    }();
 
    function loadImage(url, callback) {
        var img = new Image();
        img.src = url;
        img.onload = function(){ //图片下载完毕时异步调用callback函数。
            callback.call(img); // 将callback函数this指针切换为img。
        };
    }
 
    function imgLoaded(){
        var img = document.getElementById("ImgShow");
        img.setAttribute("src",this.src);
        if(img.style.opacity!=undefined){
            img.style.opacity=1;
        }
    }
</script>
</html>
```
　废话不说，代码已贡献出来。大家可以直接测试。但是，写了这么多js代码，太烦了，这不是我开发的原则，我要偷懒，越少代码越好。所以我想到插件啦，因为Jquery的普遍运用，我选择了jquery插件，其实其他库和原生插件也考虑的，但是已经写了就先写jquery插件啦。

插件实现
对于插件，我们都要从严谨的角度出发，因为一个成熟的插件是要考虑和完善很多东西的，不能让别人或者自己使用出现千奇百怪的问题，所以这个简单的插件兼容了IE8-9的淡出，而且抛出了一些配置，包括淡出动画时间的问题呀，包括多个动画随机显示功能（属于闲得蛋疼），其他功能大家有兴趣可以自己随机拓展，直接上代码

```
//延迟加载图片
        var imageT;
        var imgObjArr = new Array;
        if(options.isRandom){
            for(var i = 0;i<options.imgArr.length;i++){
                imageT = new Image();
                imageT.src = options.imgArr[i];
                imgObjArr.push(imageT);
            }
        }else {
            imageT = new Image();
            imageT.src = options.imgArr[0];
            imgObjArr.push(imageT);
        }
 
        //动态显示
        imageT.onload =function(){
            console.log(options.isRandom)
            if(options.isRandom){
                var result =Math.round(Math.random() * (options.imgArr.length - 1));
                $("#ImgShow").attr("src",options.imgArr[result]);
            }else{
                $("#ImgShow").attr("src",options.imgArr[0]);
            }
 
            //对于统一不支持css3属性的用jquery的fadeIn解决淡出问题
            if($("body")[0].style.opacity==undefined || $("body")[0].style.transition==undefined){
                $("#divShow").fadeIn(options.imgSecond);
            }else{
                $("#ImgShow").css({"opacity":"1"});
            }
           };
```

PK 
     á�H��C�<  <                   Untitled.mdPK      9   e    