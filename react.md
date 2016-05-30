## react 实战
###html模板
使用React 的网页源码，结构大致如下。

```
<!DOCTYPE html>
<html>
  <head>
    <script src="../build/react.js"></script>
    <script src="../build/react-dom.js"></script>
    <script src="../build/browser.min.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/babel">
      // ** Our code goes here! **
    </script>
  </body>
</html>
```
上面代码有两个地方要注意，首先，最后一个<script>标签type属性为 text/babel  .这是因为 React独有的JSX语法，跟js不兼容。凡是使用JSX的地方，都要加上 type="text/babel"
其次，上面代码一共用了 三个库  react.js  react-dom.js   Browser.js，他们必须首先加载。其中react.js是React的核心库，react-dom.js是提供与DOM相关的功能，Browser.js的作用是将JsX语法转为javascript语法，这一步很消耗时间，实际上线的时候，应该将它放到服务器完成。
###ReactDOM.render()
ReactDOM.render是React的最基本方法，用于将模板转为HTML语言，并插入指定的DOM节点。
ReactDOM.render(
<h1>Hello,world</h1>,
document.getElementById('example'));
上面代码将一个h1标题，插入 example节点  
###JSX语法
上一节的代码，HTMl语言直接写在JavaScript语言之中，不加任何引号，这就是 jsx的语法，它允许HTML与js的混写
var names=['Alice','Emily','Kate'];
ReactDOM.render(
<div>{
  names.map(function(name){
    return <div>Hello,{name}!</div>
  })
}
)

