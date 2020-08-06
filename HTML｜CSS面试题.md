### 1. 块级元素、行内块元素、行内元素都有哪些，它们有什么区别
- 块级元素有`div、p、h`等，行内块元素有`img、input`标签，行内元素有`span、text、a`标签。
- 块级元素默认独占一行
- 行内块元素和行内元素默认宽度由自身内容撑开
- 行内块元素可以设置宽高、行高以及顶底边距
- 行内元素不可设置宽高，只能设置水平margin,垂直方向无效

### 2. 盒子模型都有哪些
- W3C标准盒模型

一个块的总宽度 = width + margin(左右) + padding(左右) + border(左右)

- IE怪异盒模型

一个块的总宽度 = width + margin(左右)   width包含了padding左右和border左右值
```
border-box:box-sizing
```

### 3. 如何让元素隐藏
- `display:none`
- `visibility:hidden`
- `opacity:0`

`display:none`让整个元素直接消失，会引起页面回流。而`visibility:hidden`和`opacity:0`在网页中的位置还在，只会造成页面重绘，不会引起页面回流。两者的区别在于`opacity`可以用在动画`transition`过渡上，而`visibility`不可以

### 4. 响应式布局可以怎么做
1. `width/height`设置百分比
2. 设置`vw/vh`
3. 设置`flex`弹性布局
4. `rem/em`
5. 使用媒体查询

### 5. 常用的浏览器及其内核
1. IE: Trident 
2. 火狐: Gecko
3. Chrome、safari: Webkit
4. Opera: Presto 

### 6. 对标签语义化的理解
1. 合适的标签做合适的事情
2. 方便后期开发和维护，具有可读性
3. 丢失样式时能够让页面呈现出清晰的结构
4. 有利于SEO和搜索引擎建立良好的沟通

### 7. img标签的`alt`和`title`
- `alt`: 图片的代替文字
- `title`: 图片的解析文字

### 8. CSS如何画一个三角形
```
<style>
  #app{
    width:0;
    height:0;
    border:100px solid black;
    border-color:transparent transparent black black;
  }
</style>
<body>
  <div id='app'></div>
</body>
```
### 9. 对浏览器内核的理解
主要分成两部分：
1. 渲染引擎
2. JS执行引擎
- 渲染引擎: 负责取得html、img、css，以及计算网页的显示方式，然后输出至显示器。由于不同内核对网页的语法解释会有不同，所以渲染的效果也不相同
- JS执行引擎: 解释和执行JS来实现网页的动态效果

### 10. 什么是BFC
### 11. 表单可以跨域吗？
form表单可以跨域，但是ajax不可以。因为原页面用form提交到另一个域名之后，原页面的脚本无法获取新页面中的内容。所以浏览器认为是安全的。而ajax是可以读取响应内容的，因此浏览器不能允许你这样做。浏览器这个策略的本质是: 一个域名的JS，在未经允许的情况下，不得读取另一个域名的内容，但浏览器并不阻止你向另一个域名发送请求。

### 12. 为什么要初始化CSS样式？
因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没有对CSS初始化往往会出现浏览器之间的页面显示差异。

