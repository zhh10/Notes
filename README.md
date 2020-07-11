# mind-Mapping 前端学习的思维导图

前端JS、ES6、CSS3、HTML5、模块化、包管理器、Vue、React、Node等知识点的思维导图分享
## CSS3 
  - Selection 
    - Relationship Selectors
    - Attribute Selectors
    - Pseudo-Element Selectors
    - Pseudo-Chinese Selectors
  - border
    - border-radius
    - box-shadow 
    - border-image 
  - background 
    - background-image 
    - background-size
    - background-repeat 
    - background-position
    - background-origin
    - background-clip
    - background-attachment 
    - liner-gradient 
    - radial-gradient 
  - text 
    - text-shadow 
    - white-space 
    - word-break
    - text-ident/vertical-align/line-heihgt 
    - columns
  - 盒模型
    - W3C标准模型
    - IE6怪异模型
  - overflow 
  - transition 
  - flex
  - animation
  - transform 
  - translate及perspective
  - 响应式布局
    - 媒体查询
## JavaScript
  - 变量声明var和赋值
  - 数据类型
  - typeof
  - 数组
    - 类数组
  - 运算符
    - 比较运算符
    - 逻辑运算符
  - 类型转换
    - 隐式类型转换
    - 显式类型转换
  - 函数
  - 预编译
  - 作用域
  - 闭包
  - 立即执行函数
  - 对象
  - 包装类
  - 原型
    - 原型链
    - this指向
  - 继承
    - 传统原型链继承
    - 借用构造函数
    - 共享原型
    - 圣杯模式
  - 对象的枚举
    - for-in 
    - hasOwnProperty 
    - instanceof
  - this指向
  - arguments
  - 克隆
    - 浅层克隆
    - 深层克隆
  - try-catch 
    - e.message
    - e.error
    - e.name 
  - ES5严格模式
    - use strict 
    - 禁用
      - 禁用function.callee\caller
      - 变量赋值之前必须先声明
      - 拒绝重复属性和参数
      - 全局作用域下this等于undefined
  - DOM操作
    - 增
    - 删
    - 改
    - 查
    - Element节点
  - Date
    - 方法
    - 定时器
  - DOM基本操作
  - 脚本化CSS
  - 事件
  - 事件处理模型
    - 冒泡
    - 捕获
  - 事件对象
    - 事件源对象
    - 事件委托
  - 事件分类
    - 鼠标
    - 键盘
    - 移动端
    - 文本操作
    - 窗口操作
  - JSON
  - 异步加载JS
  - RegExp正则表达式

## ES6
  - 概述
    - ES、JS、NodeJS的区别
  - 块级绑定
    - var
    - let
    - const
  - 字符串和正则表达式
    - 更好的Unicode支持
    - 更多的字符串API
    - 正则的粘连标记
    - 模块字符串
    - 模块字符串标记
  - 函数
    - 参数默认值
    - 剩余参数
    - 展开运算符
    - 明确函数的双重用途
    - 箭头函数
  - 解构
    - 对象解构
    - 数组解构
    - 参数解构
  - 对象
    - 新增的对象字面量语法
    - Object新增的API
    - 构造函数的语法糖
    - 类的其他书写方式
    - 类的继承
    - 抽象类
  - 符号
    - 普通符号
    - 共享符号
    - 知名符号
  - 异步处理
    - 事件循环
    - 事件和回调函数的缺陷
    - 异步处理的通用模型
    - Promise的基本使用
    - Promise的串联处理
    - Promise的其他API
    - async和await
  - Fetch API
    - 概述
    - 基本使用
    - Request对象
    - Response对象
    - Headers对象
    - 文件上传
  - 迭代器与生成器
    - 迭代器
    - 可迭代协议
    - 生成器
  - 更多的集合类型
    - Set
    - Map
    - WeakSet 和 WeakMap
  - 代理与反射
    - 属性描述符
    - Reflect
    - Proxy代理
  - 新增的数组API
    - 静态方法
    - 动态方法

## 模块化
  - 前端发展中遇到的问题
  - CommonJS 
    - nodejs
    - 模块导入导出
    - CommonJS规范
    - nodeJS对CommonJS的实现
  - AMD规范与CMD规范
  - ES6模块化
    - 依赖预声明
    - 同源策略保护
    - 基本导入导出
    - 默认导入导出
    - 基本导出与默认导出的不同
## Webpack 
  - Webpack核心功能
    - 在浏览器端实现模块化
    - 模块化兼容性
      - Webpack同时兼容ES6模块化以及CommonJS
    - 编译结果分析
      - 使用立即执行函数，避免全局污染
      - 将对象作为变量，key为代码文件的路径
      - eval里的代码会放在另一个环境中去执行
    - 配置文件
      - 配置文件通过modules.exports导出（因为要运行文件，而webpack在node环境中） 
      - 设置配置文件
        - 默认webpack.config.js
        - npx webpack --config xx.js
      - 相关配置属性
        - mode
        - entry
        - output 
    - devtool配置
      - source map源码地图
    - 编译过程
      - 初始化
      - 编译
        - 创建chunk
        - 模块记录
          - 从入口模块开始
          - 检查缓存记录
          - 进行语法分析（此时不运行文件） 
          - AST抽象语法树分析
          - 保存在dependencies中
          - 替换依赖函数
          - 保存转换后的模块代
          - 根据dependencies的内容递归加载模块
        - 产生chunk assets资源列表
        - 合并chunk assets
    - 入口与出口
      - path 
      - entry
      - output 
        - [] 命名规则
        - 使用[hash]、[chunkhash] 解决缓存问题
    - loader
      - loader本质是一个函数，功能为转换成JS代码
      - 在AST之前调用
      - 从上到下匹配，从后到前执行
      - 使用CommonJS,因为在node环境中，要运行
    - plugin 
      - 将功能嵌入到webpack编译流程中
      - compiler对象，内部创建compilation
    - 区分环境
  - 常用扩展
    - 清除输出目录
      - clean-webpack-plugin
    - 自动生成页面
      - html-webpack-plugin 
    - 复制静态资源
      - copy-webpack-plugin 
    - 开发服务器
      - webpack-dev-server 
    - 普通文件处理 
      - file-loader
      - url-loader 
    - 解决路径问题
      - pluginPath 
        - 本质是一个字符串
        - __webpack__require_p (一些loader和plugin会用到)
    - webpack内置插件
      - DefinePlugin 
      - BannerPlugin 
      - PrividePlugin 
  - CSS工程化
    - 概述
      - 解决类名冲突
      - 解决重复样式
      - 解决CSS文件细分问题
