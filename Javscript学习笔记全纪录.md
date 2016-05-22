
#javascript学习笔记全记录
 
##    1.就是用来修改样式的,修改的是行内样式。任何样式都能够修改。
##    2.css里面怎么写js就怎么写。
##    3.任何元素都能加事件；事件都要小写
###js的三大组成部分：
1.ECMAScript——核心解释器，把js代码转换成计算机可以读懂的语言
2.DOM——Document  object model 文档对象模型
          增删改查文档节点
3.BOM——browser object model 浏览器对象模型
          完全不兼容
特别的问题：
 0、document.ready和document.load有什么区别？
      document.ready比onload要快，要先加载
          页面加载完成有两种事件，一是ready，表示文档结构已经加载完成（不包含图片等非文字媒体文件），二是onload，指示页面包含图片等文件在内的所有元素都加载完成。
 
 1.调用一个函数总是返回一个值，如果没有指定这个值则返回undefined;
 2.对象引用问题（Date,json,arr）
    var arr = [1,2];
var arr2 = arr;
arr2.push(5);
document.write(arr+'<br />');//[1,2,5]
document.write(arr2);//[1,2,5]
###js的数据类型：
     数字类型（number）,字符串（string）,布尔值（booleans），未定义（undefined），对象（object）
     基本数据类型：数字类型（number）,字符串（string）,布尔值（booleans），未定义（undefined）
     复合数据类型：对象（object）
数据类型转化：
     1.强制数据类型转化
          转整数：parseInt();
          转小数：parseFloat();
          弱转化：number();//严格转化
     2.隐式数据类型转化
          +：字符串拼接==》12+'5'='125';
          -*/%:字符串转数字==》'12'-5=7;
          ++:字符串转NaN==》var i='12';i++;typeOf(i)=='number';    
函数：有返回值，返回值，返回值
###函数返回值：
     1.函数没有返回值，返回undefined
     2.函数有return，但是没有值，返回undefined;
     3.return后面的代码不执行
     还有一个特殊的是 "函数function(){}"
          1.函数分定义阶段和调用阶段
          2.在哪里定义不重要，重要的是在哪里调用
          *3.只要函数名能出现的地方，都可以放函数本身
##函数传参：
     函数不设置参数接收的话可以调取arguments[i]获取到参数
--------------
###字符串：
     字符串定义： var i=0;
                var str='abc';
     *字符串拼接：
        var name = 'leo';
    var age = 19;
    var hobby = '妹子';
    var you = '你';
    var str = you+'是帅气的'+name+'，今年'+age+'岁，性别男，爱好'+hobby;
操作样式的2种方法：
    .     方便灵活
   []能使用变量参数，点能做的它都可以做
循环：操作一组元素的时候使用
     ①条件循环
     while(i<5){
          执行语句；
          i++;
     }
当i不满足条件的时候的，循环自动终止；
     ②固定次数循环
     //循环5次
     for(var i=0;i<5;i++){
          执行语句；
     }
 
for循环小知识：
     continue        跳出当次循环
     break           阻断后面的循环
##函数的作用域
1.全局变量=公用卫生间
2.局部变量=次卧卫生间
     局部变量 全局无法使用
     局部声明变量不加var的话就变成全局变量（不推荐使用）
     window.a=123;
3.闭包=次卧的可以用自己的卫生间，也可以用公用卫生间；
 
##闭包：变量作用域
 
预解析（从上至下，从左至右）
     1、先把变量声明 全部提前，赋值不动
     2、函数也有预解析，直接提前
     3、预解析 不会脱离函数作用域，也不会冲出script标签 最多提到自己标签的顶部
代码执行顺序 见一个script解析执行一个，执行完了 在执行下一个
 
预解析的时候，函数和变量重名的时候，函数覆盖变量
执行代码的时候，有表达式的为大，会覆盖掉同名的函数值，最后读取变量的值；
var a=function(){
     alert(1);
};
function a(){
      alert(2);
}
     a();
预解析的时候a=function a(){alert(2)}
正常执行代码时候a=function(){alert(1)};覆盖了上面的值
所以弹1(表达式为大)
if语句和switch语句
     不适用break会导致case穿越，且不会报错
     switch(条件){
    case 条件可能的取值1:
        执行的语句1;
        break;
    case 条件可能的取值2:
            执行的语句2;
            break;
    default:
        默认的情况;
    break;
     }
 
     if(判断条件1){
          判断条件1成立执行 语句1
     }else if(判断条件2 ){
          判断条件2成立执行 语句2
     }else{
          以上判断条件都不成立的情况这条语句
     }
     
     if语句的简写形式：
          1.
          var a=500;
          if(a==500){
               alert('吃大餐');
          }
          可以简写成：a==500&&alert('吃大餐');
          2.三目运算符
          条件成立不？执行语句1:执行语句2;
###运算符
算数运算符    +-*/%
赋值运算符    = += -= /= *= %=
比较运算符    <><= >= == === != !==(三等号：数据类型和值都完全相等的情况下才是true;)
逻辑运算符    &&  ||  ！取反
运算优先级    ()
return
     后面的代码不执行了
     用函数的返回值代替执行结果
###定时器：
先开后关
     开启：setInterval(function(){}||fn,300);有返回值
     清除：clearInterval(定时器名);
     setTimeout(fn,300);
     clearTimeout(定时器名);
###定时器的问题：
    1.循环里面加定时器，定时器里面用i 的问题
          用闭包解决
    2.定时器函数不能放括号
          否则会undefined;因为函数没有返回值，返回一个undefined
    3.定时器里面不能用this  当事件发生的时候先把this存下来，而不是在定时器里直接用this （定时器里面的this指向window）;
          在定时器外面：var _this=this;
    例子：
        延迟选项卡
     2.第一次起作用的时候要等一个定时器的时间；解决：封装成函数，先调用一次
###日期对象：
     特殊用法：
          var oData=new Data(oData.getTime()时间戳);
          时间戳是毫秒数
          里面放置时间戳也可以获得，时间戳转化得来的时间
     获取日期对象：
     var oDate=new Date();
     var year=oDate.getFullYear();
     var month=oDate.getMonth()+1;小1
     var day=oDate.getDay();//获取星期(0，1，2，3，4，5，6)
     var date=oDate.getDate();
     var hour=oDate.getHours();
     var mintues=oDate.getMinutes();
     var seconds=oDate.getSeconds();
     oDate.getTime();获取时间戳
     设置日期对象：
     var oDate= new Date();
     oDate.setFullYear(2017,0,1);设置：年，月，日
     oDate.setHours(0,0,0,0);设置：时，分，秒，毫秒
     oDate.getTime();
###经典案例：获取到本月最后一天是星期几？
    var arr=['星期日','星期一','星期二','星期三','星期四','星期五','星期六'];
    var oDate=new Date();
    oDate.setMonth(oDate.getMonth()+1);//设置日期到下个月
    oDate.setDate(0);//获取到上个月的最后一天
    var week=oDate.getDay();
    alert(arr[week]);
##数组常用方法：增，删，改，查     9
     var arr=[12,5,8];
     arr.push(0);向后添加==》arr=[12,5,8,0];
     arr.unshift(0);向前添加==》arr=[0,12,5,8];
     arr.pop();数组后删除一位==》arr=[12,5];
     arr.shift();数组前删除一位==》arr=[5,8];
     arr.join('-');数组连接成字符串==》'12-5-8';
     arr.splice('开始位置','几位','元素');具备‘增删改’
          for(){}时候需要i--;
          增加：arr.splice(1,0,3);==》arr=[12,3,5,8];
          删除：arr.splice(1,1);==》arr=[5,8];
          修改：arr.splice(1,1,3);==》arr=[12,3,8];
     arr.reverse;数组反转==》arr=[8,5,12];
     arr.concat();数组连接
     arr.sort(function(n1,n2){
              return n1-n2; 由小到大的排序
              return n2-n1; 由大到小的排序
               n1n2可以是对象的某个具体属性值比较
     })
##字符串常用方法：7
     var str='welcome to zhinengshe'
     str.charAt(0);==>w  //查找位置范围相应字符 
     str.indexOf('e');==>1【UA检测】
     str.lastIndexOf('e');==>20【判断文件名】
     找到相对应的元素返回元素位置
     找不到元素的位置返回-1
     str.split(' ');分割成数组==》['welcome','to','zhinengshe'];
     str.substring('开始位置','结束位置'不包含结束位置);截字符串
     str.substring(0,1);==>'w'
     str.substring(0,str.length-1);把最后一个字母去掉
     str.toUpperCase();转成大写；
     str.toLowerCase();转成小写；
     str.charCodeAt(位置);返回指定位置的字符编码
     String.fromCharCode(字符编码);返回对应字符编码的字符
     str.replace('要更换的'，'更换的');
          注意：字符串的比较 其实就是编码大小的比较
##Math的常用方法：9
     Math.round();四舍五入
     Math.random();获取0-1之间的随机数字，不包含1本身
     Math.floor();向下取整数
     Math.ceil();向上取整；
     Math.max();获取最大数字
     Math.min();获取最小数字；
     Math.abs();获取绝对值；
     Math.sqrt();幂
     Math.pow();开方
##闭包（匿名函数自执行、封闭空间）变量作用域
    1.命名冲突
        商量
    2.i的问题
for(var i=0;i<arr.length;i++){
      (function(index){
          直接用index代替i
      })(i);
}
        a)循环里面用事件，事件里面用i,i变成长度而不是对应的i的值 0 1 2
        b)循环里面加定时器，定时器里面用i
    左边小括号里面用的是匿名函数的定义，右边的小括号是函数的调用
    (function(){ })();
json={};
    JSON.stringify(json)   -> 普通json变成标准json版字符串
    JSON.parse(str) ->  把字符串变成json
    兼容：IE8+ chrome FF
        后台返回的是'{}'字符串的json
eval:把字符串变成可以执行JS代码，把结果放过去
eval解析json必须加括号;不然会报错
var str1='({"name":"shiyou","age":20})';
    alert(eval(str1).name); ==>shiyou
    ////////
    var str2='{"name":"shiyou","age":20}';
    //直接eval一个'json'会报错(Uncaught SyntaxError: Unexpected token :)
    //必须eval 的时候加上小括号
    alert(eval('('+str2+')').age);
 
var json={a:5,b:5,c:5};
delete json.a;可以移除a和它的值
它值兼容ie9以上的浏览器
<select></select>
先创建 ，后添加
var opt = new Option('text'，'value');    //创建选项
oS.options.add(opt)                             //添加
oS.options.remove(下表||opt);           //删除
 
selectedIndex 获取选中的那个项 下标
oS.options[oS.options.selectedIndex].value/text
 
注意1：<option value="北京">北京</option>一定要加value  
注意2：事件oS.onchange=function(){};
对象引用：
     1、基本数字类型：number,string,undefined,boolean
          赋值就是复制；
          var a = 12;
       var b =a ;
       b=b+2;
       a的值还是不变
     2、对象引用
          1）赋值不会复制，对象比较不相等，看起来一样也不行
     var oDate1=new Date();
     var oDate2=new Date();
     oDate1 !==oDate2
     
          2）一个东西改变，另外一个东西也跟着改变
          案例1：
          var a = [12,5,8]; //对象
    var b =a;
    b.pop();
    alert(a);
    给b赋值了a对象，a,b同时指向了同一个对象
     当一个改变了，对象就会发生改变；
案例2：
     var oDate = new Date();
    var oDate2 = oDate;
    oDate2.setFullYear(2020);
    alert(oDate)
###'use strict'严格模式
解决的问题
1.变量必须加var
2.不允许 if 里面定义函数，必须顶层定义
3.严格模式干掉了with
 
####严格模式特性
1.必须写use strict 不能是其它单词 否则不起作用
2.use strict 有作用范围 只针对当前函数起作用
3.只针对 当前自己 script标签起作用
4.只针对当前js文件起作用
各种表达式：
     1.逗号表达式：优先级特别低用（）括起，读取后面的
          var a = (12,5);
         alert(a);//5
     ————————
     同样读取最后一个，走else
           if(undefined,true,false,32,0){
        alert('ok');
    }else{
        alert('不ok');   
    }
 
     2.||：比较懒，碰到真的就返回
     var a=0||5;
     alert(a);结果5
 
     3.&&：比较勤快，得查完，有一个假就都是假的
DOM     增，删，改，查
oUl.children         获取UL的子节点         有length的属性
oUl.children[0]    获取UL第1个子节点     使用比较多
oUl.children[oUl.children.length-1]    获取Ul的最后一个子节点    使用比较多
 
oUl.parentNode    获取Ul的父节点    body,HTML,document
 
oUl.firstElementChild||oUl.firstChild    首个节点（first）    "firstChild 低版本IE6 -8
firstElementChild 高级浏览器"
oUl.lastElementChild||oUl.lastChild    最后一个字节点    同上
 
oLi.previousElementSibling||oLi.previousSibling    获取上一个兄弟节点    相对自己
oLi.nextElementSibling||oLi.nextSibling    获取下一个兄弟节点    相对自己
 
var oLi=document.createElement('li');    创建一个li的节点    创建赋值添加3个步骤
oLi.innerHTML=''    给它赋值   
oUl.appendChild(oLi);    插入到oUl里面去（向后插入）常用   
oUl.insertBefore(要插的元素,插到哪里)    插入到某个元素前面去   
 
oUl.removeChild(要移除的元素);    删除掉某个元素  
 
节点.cloneNode()    克隆某个元素    "cloneNode（true）深度克隆
移除id:节点.removeAttribute('id');"
 
window.onscroll    滚动事件    当鼠标滚动的时候发生
window.onresize    窗口事件    当窗口缩小/放大的时候
 
##滚动距离    配合滚动事件
var scrollTop=document.documentElement.scrollTop||document.body.scrollTop
 
获取可视区宽高
document.documentElement.clientHeight    可视区的高度   
document.documentElement.clientWidth    可视区的宽度   
 
offsetHeight(占位物体)（live事件）    物体盒模型高度    border+padding+height
offsetWidth(占位物体)（live事件）    物体盒模型宽度    border+padding+width
 
offsetparent    定位父级    如果没有定位父级则是body
parentNode      结构父级
 
offsetTop(占位物体)    物体盒模型最外边距离定位父级的top值    如果没有定位父级则是相对body
offsetLeft(占位物体)    物体盒模型最外边距离定位父级的left值    如果没有定位父级则是相对body
 
getAttribute('属性')    获取行间自定义属性   
setAttribute('属性'，'属性值');    设置行间属性值    对应使用
removeAttribute('属性')    移除属性   
###form 表单
     关于表单
    提交数据
    action  提交的地址 数据提交到哪里
    method    提交方式
     get    默认表单的提交方式  ?user=leo&age=19
                get的方式数据在url里面 明文串  不安全
                比较小      32k
 
            post    数据量        1G    不在url传输    相对安全
 
     name    名字    必须加name
 
###post与get 区别
get            数据量小  方便    利于分享     不安全
post        数据量大  没法分享    相对安全
更安全的方式
https  相对安全
cache 缓存
###冒泡机制
     特性
    1.冒泡不管 父级有没有事件 都会冒泡
    2.冒泡跟css无关  跟元素位置无关 ——》parentNode
 
    子级元素 一层一层将事件 往父级和父级的父级和父级的父级的父级和...一直到头
    取消冒泡，谁触发的冒泡，在哪里取消
    ev.cancelBubble = true;
    cancel：取消
    Bubble：冒泡
    什么时候出问题什么时候用，没事别瞎瞎取消
    一般情况下，我们碰不到冒泡的情况， 等碰到了在想着去取消；
###this的问题：
     this有问题的情况
1.attachEvent 事件绑定的时候，(addEventListener没有this问题 onclick方式也没问题)
2.定时器中用this(this指向window)
3.行间事件中用函数 函数里面用this
4. 函数嵌套调用this
ev||event事件：
var oEvent=ev||event;  事件兼容的写法ev 是FF用，event是chrome和IE用
 
##页面坐标
oEvent.clientX    鼠标在可视区中距离body左边的距离（当有滚动距离的时候需要加上）
oEvent.clientY    鼠标在可视区中距离body上边的距离（当有滚动距离的时候需要加上）
ev.pageX不兼容ie678
ev.pageX=ev.clientX+scrollLeft;
ev.pageY=ev.clientY+scrollTop;
 
oEvent.cancelBubble=true;    取消事件冒泡为真
 
oEvent.keyCode    键值（通过判断键值，可以有些操作）
 
onkeydown    当键盘按下的时候（例子：键盘控制div行走）
onkeyup    当键盘抬起的时候
down和up的问题    输入框输入的内容是onkeyup的时候进去的
 
oEvent.ctrlKey&shiftKey&altKey    布尔值,判断ctrl时候有
 
document.oncontextmenu    右键事件（如果阻止右键事件，可以自定义右键事件）
 
return false；    阻止浏览器的默认事件的发生
 
oEvent.preventDefault();    addEventListener的情况下阻止默认事件发生
事件监听：能让一个obj上面能绑定多个事件   
obj.addEventListener('事件'，'函数'，false);
①标准浏览器中使用
②事件前面不需要加on
③函数可以放有名字的函数，也可以放匿名的函数
④false 是冒泡阶段绑定事件，默认也是冒泡绑定
⑤函数里面不能用return false 来阻止浏览器默认事件的发生，改为用
   oEvent.preventDefault();
 
obj.attachEvent('事件'，'函数')
①低版本浏览器中使用
②事件前面要加on
③IE浏览器只支持冒泡，所以没有false和true的说法
④函数里面用this会失效
 
obj.removeEventListener('事件'，'函数'，false);    标准浏览器的删除事件的写法
obj.detachEvent('事件'，'函数');    IE6-8移除绑定事件的写法
 
addEvent(obj,sEv,fn);    封装好的事件绑定函数
removeEvent(obj,sEv,fn);    移除绑定事件的封装函数
 
oEvent.detail    "火狐下存储滚轮方向信息，当它为正值，滚轮是向下的，为负值的时候滚轮是向上的"
oEvent.wheelDelta(得了她)    "IE&chrome下存储滚轮方向信息的，当它为正值的时候,滚轮向上，为负值的时候滚轮向下"
 
##事件委托:给父级加事件 ，然后寻找事件发生源  
oEvent.srcElement （chrome、IE）    谁触发了这个事件的元素(触发事件的源元素)
oEvent.target （Firefox）    同上，触发事件的源元素
兼容写法：var oSrc=oEvent.srcElement||oEvent.target;   
oSrc这个变量就是触发事件的源元素的兼容版   
 
判断标签名
oSrc.tagName  触发事件的事件源的标签名 全部大写
oSrc.tagName == 'INPUT'&&oSrc.value
 
onmouseover和onmoverout的问题
oEvent.fromElement（chrome、IE）    从哪里移动进来的元素
oEvent.relatedTarget（FF）    火狐的写法还是一样的
 
oEvent.toElement（chrome、IE）    从哪里移出去的元素
oEvent.relatedTarget（FF）    火狐的写法还是一样的
兼容写法：
     var oFrom=oEvent.fromElement||oEvent.relatedTarget;
     var oTo=oEvent.toElement||oEvent.relatedTarget;  
判断oDiv 是否包含了oForm
if(oDiv.contains(oForm)){return}
###cookie 保存数据     
cookie 设置  查看cookie  F12->resource  ->cookies
     特点：
          1、不能跨域
                    同一个域名下所有文件共享cookie
                    不同域名之间——不共享
          2、容量下4k
          3、不安全（隐私数据别存cookie）
          4、有有效期
                    默认是 session  浏览器 退出 会话结束
                    也可以为cookie设置日期，不过某些浏览器还是会选择性删除的
                    *数据超出有效期，就会删除
### cookie的设置
      function setCookie(name,value,data){
    var oDate =new Date();
    oDate.setDate(oDate.getDate()+data);
    document.cookie=name+'='+value+';expires='+oDate;
} 
###cookie的获取
function getCookie(name){
    var arr=document.cookie.split('; ');
    for(var i=0;i<arr.length;i++){
        if(name==arr[i].split('=')[0]){
            return arr[i].split('=')[1];
        }
    }
    return '';//为了和上面return的数据类型的一致性
}
cookie的移除：设置日期过期就自动清除
function removeCookie(name){
    setCookie(name,0,-1);
}
###常用事件：
 
onclick
点击事件
onmouseover
onmouseout
当鼠标移入事件
当鼠标移除事件
onmouseenter    
onmouseleave    
当鼠标移入事件（已做了冒泡阻止）
当鼠标移除事件（已做了冒泡阻止）浏览器有时会发神经的不支持
onmousedown
onmousemove
onmouseup
    鼠标按下事件
    鼠标按下并移动时触发
    当鼠标按下并抬起的时候触发
onfocus
onblur 
聚焦的时候触发obj.focus();这个方法可以触发onfocus事件里的逻辑发生失去焦掉的时候触发
onload
onerror
    当加载完成后发生（图片）
    加载失败时候触发（图片）
onkeydown    
onkeyup    
键盘按下的时候触发
键盘抬起的时候触发
oncontextmenu
右键事件（环境上下文事件）
onchange
select的选择事件
onresize
窗口大小更改事件
onscroll
滚动条滚动事件
onsubmit 
表单提交事件
oninput
 
onpropertychange 
在input的值发生改变的时候触发，IE9不兼容
同oninput的事件意思几乎相同，只是在IE下使用，不兼容IE9故而放弃
DOMContentLoaded
 
 
onreadystatechange
还要判断document.readyState==complete
FF chrome 高级浏览（统称：ready事件）只能事件绑定addEventListener
 
    IE6-IE8（统称：ready事件）只能事件绑定attachEvent()
onmousewheel 
DOMMouseScroll
     chrome IE  滚动事件
    （Firefox）当滚轮滚动的事件
posted @ 2016-05-21 14:10 施佑的小小世界 阅读(...) 评论(...) 编辑 收藏
刷新页面返回顶部
公告
Copyright ©2016 施佑的小小世界
