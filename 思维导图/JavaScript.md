# JavaScript

##  变量声明var和赋值

### 单一var模式

- var a,b,c,d,e;
- var a=10,b=20,c=30,d=40;

## 打印

### 控制台输出console.log()

### document.write()

## 数据类型

### 原始值（存放在stack)

- Number
- Boolean
- string
- underfined
- null

### 引用值（存放在heap）

- array
- object
- function
- data
- Regre

## typeof

### number

### boolean

### object

### underfind

### function

### string

### 返回的是字符串

## 对象

### 定义方式

- 自变量｛｝ 
- 构造函数
- Object.create

### indexOf

- 返回位置
- 不存在返回-1

##  数组

### 定义方式

- 自定量[] 
- 构造函数

	- new Array() 

### 改变原数组

- push
- pop删除
- unshift

	- 在前面增加

- shift

	- 从前面删除

- reverse
- sort

	-  arr.sort().reverse()
	- arr.sort(function(){})

		- 必须是两形参
		- 看返回值

			- 当返回值为负数时，那么前面的数放在前面
			- 为正数，后面的数在前面
			- 为0，不动

- splice

	- splice（从第几位开始，截取多少的长度，在切口处添加新的数据）
	- 可以用负数

### 不改变原数组

- concat

	- 连接两个数组

		- arr.concat(arr1)

- join

	- arr.join("-")

- split
-  slice
- toString 

### 类数组

- 属性为索引（数字）属性，必须有length属性，最好加上push方法

	- push:Array.prototype.push
	- splice:Array.prototype.splice

### 数组去重

### arr.length

### indexOf

- 返回位置
- 不存在返回-1

## 运算符

### +

- 输运运算、字符串连接
- 任何数据类型加字符串都等于字符串

### ++

- ++a

	- a=a+1

- a++

	- 先执行a再++

		- 示例：var b=++ a - 1 + a++

### +=

- a+=10

### *=、/=、%=、

## 比较运算符

### >、<、==、<=、>=、！=

## 逻辑运算符

### &&、||、！

- var a = 0 && 2 + 2 

	- 先看第一表达式转化成布尔值的结果，如果结果为真，那么它会看第二个表达式转换成布尔值的结果，然后如果只有两个表达式的话，只看到第二个表达式，就可以返回该表达式的值了
	-  短路语句

		- 2>1 && document.write('航哥很帅')

### 条件语句

- if(条件){执行语句}
- if(条件1）{执行语句1}else if(条件2）{执行语句2}else{执行语句3}
- switch语句

	- switch、case、break

- break、continue

### 循环

- for(var i = 0;i < 10; i++){执行语句}
- var i = 0;for(;i<10;){执行语句;i++}
-  while(条件){执行} 
- do{执行语句}while(条件)

	- 先执行再判断

## 类型转换

### 隐式类型转换

- isNaN() 

	- 内部先Number() 再判断

- ++/--、+/-

	- 先调用Number() 
	- 当+两侧有一个是字符串，就调用String()

- */%

	- 调用Number()

- &&、||、！

	- 转化成Boolean值

- <、>、<=、>=
- ==、！=

### 显式类型转换

- Number()
- parseInt(string)把里面的数变成整数
-  parserFloat(string)
- String()
- Boolean()
- toString(radix)

	- demo.toString()

		- underfind不可用
		- null不可用

### 不发生类型转换的

- ===、！==

	- ===绝对等于
	- ！== 绝对不等于

##  函数

### function test(){}

### 命名函数表达式

- var test = function abd(){ } 

### 匿名函数表达式

- var demo = function (){}

### function sum(a,b,c,d)

- 相当于在里面var a,b,c,d
- 内置实参列表argments

	- 映射

- 形式参数长度 sum.length

### 返回：return 

### 全局变量、局部变量

- 底层可以调用外层的、外层的不可以调用底层的

## 预编译

### 前奏

- mply global暗示全局变量：任何变量未经声明，此变量就为全局对象所有。一切声明的全局变量，都是window的属性；window就是全局的域
- var a=b=123  自右向左，连续赋值，b是未经声明的
- 函数里是局部变量

### 预编译发生在函数执行的前一刻

### 函数体系——四部曲

- 1、创建AO对象  Activation Object(执行期上下文）

	- AO｛｝

- 2、找形参和变量声明，将变量和形参名作为AO对象属性名，值为underfined

	- AO｛a:underfind,b:underfined｝

- 3、将实参值和形参统一

	- AO｛a:1,b:underfined｝

- 4、在函数体里面找函数声明，值赋予函数体

	- AO｛a:function(){},b:underfined,d:function d(){}｝

### 只看声明

### 全局

- GO对象（Global Object）

## 作用域

### 在函数运行前一刻，会创建一个执行期上下文的内部对象（AO），一个执行期上下文定义了一个函数执行时的环境，函数每次执行时对应的执行上下文都是独一无二的，所以多次调用一个函数会导致创建多个执行上下文，当函数执行完毕，它所产生的执行上下文被销毁。

### 每个js函数都是一个对象，对象中有些函数我们可以访问，但有些不可以。[[scope]]就是其中一个,[[scope]]指的是我们所说的作用域，其中存储了运行期上下文的集合。  作用域链

### 查找变量：从作用域的顶端依次向下查找（AO放在最顶端）

## 闭包

### 当内部函数被保存到外部时，将会生成闭包。闭包会导致原有作用域链不释放，造成内存泄漏

### 作用

- 实现公有变量（累加器）
- 可以做缓存（存储结构）
- 可以实现封装，属性私有化
- 模块化开发，防止污染全局变量

## 立即执行函数

### 针对初始化功能的函数

- var num =（function (a,b,c){var d = a+b+c*2;return d;}(1,2,3)）

### 只有表达式才能被执行符号执行

- 函数声明不能被执行

	- function test(){}()不能被执行
	- var test = function (){}()可以被执行，执行一次永久放弃

## 对象

### this

### 增删改查

- 增加：myz.wife = ''chen"
- 删

	- delete myz.wife 

### 可以加函数 var myz = {getMarried:function(){}}

### 创建方法

- 1、var obj = {}  对象字面量/对象直接量
- 2、构造函数

	- 系统自带的构造函数 new Object( ) 

		- var obj = new Object(     )

	- 自定义

		- function person()this.a=a;this.b=b} 

			- var person1 = new person() 

## 包装类

### 原始值加属性：新建后销毁

### new Number() 

### new String() 

### new Boolean() 

## 原型

### 原型是function对象的一个属性，它定义了构造函数制造出的对象的公共祖先。通过该构造函数的产生的对象，可以继承该原型的属性和方法。原型也是对象。

- Person.prototype 是祖先
- 利用原型特点和概念，可以提取公有属性
- 对象查看原型：__proto__

	- 起到链接的作用

- 对象如何查看对象的构造函数：constructor

### 原型链

- 增删改查

	- 增
	- 删

		- 通过自个删除delete

	- 改

		- 通过自个更改

- 绝大多数对象最终都会继承自Object.prototype

	- Object.create(null)例外
	- Object.create(underfined)例外

- Object.create(原型)

### 改变函数运行时的this指向

- call
- apply

	- 传入数组

### document.write

- 调用原型的toString方法

### toString()

- num.toString() ---> new Number(num).toString()

	- 调用Number.prototype.toString

### 私有化变量  在functon里用var不用this

## 继承

### 传统形式

- 原型链

	- Son.prototype = new Father() 
	- 过多继承没用的属性

### 借用构造函数

- Father.call(this,name,age)
- 不能继承借用构造函数的原型
- 每次构造函数都要都多走一个函数

### 共享原型

- Son.prototype = Father.prototype
-  不能随便改动自己的原型

### 圣杯模式

- F为中介

## 命名空间

### 对象中的对象

## 对象的枚举

### for in 循环

- 实现对象的遍历
- for (var pop in obj){}

### hasOwnProperty

- 一旦延展到Object.prototype不返回
- 自身拥有的，不是继承过来的
- Object.getOwnProperty() 
- Object.keys() 

### in

- 自身拥有的+继承过来的

### instanceof 

- A instanceof B 

	- A对象   是不是   B构造函数构造出来的
	- 看A对象的原型链上  有没有  B的原型

## this

### 函数预编译过程 this--> window

### 全局作用域里 this -->window

### call/apply 可以改变函数运行时的this指向

### obj.func()；func()里面的this指向obj

## arguments

### argument.callee

- 指代的就是函数自己
- 可用在立即执行函数  递归

### func.caller

- 在哪个环境被调用

## 克隆

### 浅层克隆

### 深层克隆

- 遍历对象
- 判断是不是原始值

	- typeof

		- object是引用值

- 判断是数组还是对象

	- instanceof 
	- toString

		- Object.prototype.toString.call()

	- constructor

- 建立相应的数组或对象
- 递归

## 条件判断

### 是 ？

### 否 ：

### var num = 1>0  ?  2+2  : 1+1  

## try catch

### try{}catch(e){} finally{}

- e.message
- e.error
- e.name

	- EvalError:eval()的使用与定义不一致
	- RangeErrir:数值越界
	- ReferenceError:非法或不能识别的引用数值
	- SyntaxError:发生语法解析错误
	- TypeError:操作数类型错误
	- URIError：URI处理函数使用不当

## es5.0严格模式

### use strict

- 全局严格模式
- 局部函数内严格模式

### with(){}

- 改变原型作用域链的最顶端

### 禁用

- 不能使用arguments.callee
- 不能用function.caller
- 不能使用with(){} 
- 变量赋值之前必须声明
- 局部this必须被赋值

	- 预编译this不再指向window

- 拒绝重复属性和参数

	- es3里面重复参数不报错

## DOM

### Document Object Model 

### DOM定义了表示和修改文档所需的方法。DOM对象即为宿主对象，由浏览器厂商定义，用来操作html和xml功能的一类对象的集合。也有人称DOM是对HTML以及XML的标准编程接口

### 查

- document
- document.getElementById
- document.getElementByTagName
- document.getElementByName
- document.getElementClassName
- CSS选择器document.querySelectior

	- 是静态的，之后对document结构的改变不会影响到之前取到的结果

- CSS选择器document.querySelectiorAll

### 增

- document.createElement创建元素节点
- document.createTextNode创建文本节点
- document.createComment创建注释节点
- document.createDocumentFragment创建文档碎片节点

### 插

- PARENTNODE.appendChild

	- 是剪切操作

- PARENTNODE.insertBefore(a,b)

	- 在b之前插入a

### 删

- parent.removeChild
- child.remove

### 替换

- parent.replaceChild(new,origin)

### Element节点

- 属性

	- innerHTML

		- 覆盖
		- 追加

			- +=

	- innerText/textContent

		-  取出来
		- div.innerText = '123' 覆盖

- 方法

	- ele.setAttribute

		- div.setAttribute('class','demo') 前面是属性名，后面是属性值

	- ele.getAttribute

		- div.getAttribute('id')

## Date() 

###  Date对象属性

- constructor
- prototype

### 方法

- Date() 返回当日的日期和时间
-  getDate() 从Date对象返回一个月中的某一天
- getDay() 从Date对象返回一周中的某一天
- getMonth()  从Date对象中返回月份
- getFullYear() 从Date对象以四位数字返回年份
- getHours()  返回Date对象的小时
- getMinutes()  返回Date对象的分钟
- getSeconds() 返回Date对象的秒数
- getMilliseconds() 返回Date对象的毫秒数
- 很有用： getTime() 返回1970年1月1日至今的毫秒数
- setDate() 设置Date对象月的某一天
- setMonth()  设置月份
- setFullYear()  设置年份
- setHours()  设置小时
- setMinutes()  设置分钟
- setSeconds()  设置秒钟
- setMilliseconds()  设置毫秒
- setTime()  以毫秒数设置时间

### var date = new Date() 

- 记录了这一时刻的时间，不动

### 定时器

- setInterval(function,1000) 应该叫定时循环器

	- 每隔1000毫秒运行一次
	- 会返回数字作为唯一标识
	- function可以改成字符串“console log('a')”

- 清除定时器clearInterval
- setTimeout(function,1000)

	- 推迟执行，只执行一次

- clearTimeout(timer)

## DOM基本操作

### 查看滚动条的滚动距离

- window.pageXOffset/pageYOffset

	- IE8以及IE8以下不兼容

- document.body/documentElemt.scrollLeft/scrollTop

	-   IE8和IE8以下的浏览器
	- 一个不为0另一个必为0

### 查看视口的尺寸

- window.innerWidth/innerHeight

	- IE8及IE8以下不兼容
	- 包含滚动条

- document.documentElements.clientWidth/clientHeight

	- 标准模式下，任意浏览器都兼容
	- 不包含滚动条

- document.body.clientWidth/clientHeight

	- 适用于怪异模式下的浏览器

### 查看元素的几何尺寸

- domEle.getBoundingClientRet() 

	- 返回一个对象，对象里有left,top,right,bottom
	- left和top代表该元素左上角的X和Y坐标，right和Bottom 代表元素右下角的X和Y坐标

- dom.offsetWidth\dom.offsetHeight

### 查看元素位置

- dom.offsetLeft/dom.offsetTop

	- 对于无定位父级的元素，返回相对文档的坐标。对于有定位父级的元素，返回相对于最近的有定位的父级的坐标。
	- 忽悠自身定位元素，求的距离有定位的父级的距离

### dom.offsetParent

- 返回最近有定位的父级

### 让滚动条滚动(将x,y坐标传入）

- window

	- scroll()
	- scrollTo()
	- scrollBy() 

		- 会做累加，有快速阅读的功能

## 脚本化CSS

### 读写元素CSS属性

- don.style.prop

	- 可读写行间样式，只能是获取行间，行间没有就没有

		- 遇到float这样的保留字属性，前面加css   float--> cssFloat
		- 复性元素必须拆解  background-color --> backgroundColor

### 只读操作

- window.getComputedStyle(ele,null)

	- 返回的都是绝对值，没有相对单位
	- 当前元素所展示的一切CSS展示值，包括默认值
	- 返回权重最高，最终展示的
	- IE8及以下不兼容
	- 可以查伪元素

		- window.getComputedStyle(ele,"after")

- IE独有

	- elem.getcurrentStype[prop]

### 修改

- 提前编写好变化后的CSS属性
- onclick后 修改className即可

## 事件

### div.onxxx = function(){} 

- 基本等于写在行间上
- this指向dom元素本身

### obj.addEventListener(事件类型,处理函数,false)

- IE9以下不兼容
- 事件类型

	- click 

- 能执行多次，但是看function的地址
- this指向dom元素本身

### obj.attachEvent('on'+事件类型,处理函数）

- IE独有
- 一个事件同样可以绑定多个处理程序
- this指向window 

### 解除事件绑定

- ele.onclick = null/false/''
-  ele.removeEventListener(type,fn,false)
- ele.detachEvent('on'+type,fn)
- 若绑定匿名函数，则无法解除

## 事件处理模型

### 事件冒泡

- 结构上（非视觉上）嵌套关系的元素，会存在事件冒泡的功能，即同一事件，自子元素冒泡向父元素。（自底向上）  

### 事件捕获（只有Chrome)

- 结构上（非视觉上）嵌套关系的元素，会存在事件冒泡的功能，即同一事件，自父元素冒泡向子元素（事件源元素） 。（自顶向下）

### 触发顺序：先捕获，后冒泡

###  focus、blur、change、submit、reset、select等事件不冒泡

### 取消冒泡

- W3C标准

	- event.stopPropagation()

		- 但不支持IE9以下版本

			- div.onlick = function(e){e.stopPropagation();}

- IE独有

	- event.cancelBubble = true;

### 阻止默认

- 默认事件

	- 表单提交、a标签跳转、右键菜单等

- return false 

	- 以对象属性的方式注册的事件才失效

- event.preventDefault()

	- W3C标注 IE9以下不兼容

- event.returnValue = false 

	- 兼容IE 

## 事件对象

### event || window.event 用于IE 

### 事件源对象

- event.target 火狐只有这个
- event.srcElement IE只有这个

### 事件委托

- 利用事件冒泡，和事件源对象进行处理
- 优点：

	- 不需要循环所有元素
	- 当有新的子元素时不需要重新绑定事件

## 事件分类

### 鼠标事件

- onclick敲击=mousedown + mouseup

	- 只能监听左键，左右键只有mousedown和mouseup

- onmousemove
- onmousedown

	- e.button记录是哪个键

- onmouseup

	- 左键0 滚动轮1 右键2

- oncontextmenu右键菜单事件
- onmouseover鼠标在里面
- onmouseout鼠标在外面
- onmouseenter鼠标在里面
- onmouseleave鼠标在外面

### 键盘事件

-  onkeydown能相应任意按键
- onkeyup
- onkeypress只能字符类键盘按键
- 按住连续触发
- keydown>keypress>keyup

### 移动端

- ontouchstart
- ontouchmove
- ontouchend

### 文本类操作事件

- oninput

	- 里面文本有变化就触发

- onfocus

	- 聚焦后失去焦点，如果有发生改变就触发

- onblur
- onchange

### 窗口操作类事件

- onscroll

	- 滚动条滚动触发

- onload

## JSON

### JSON.parse()

- string -- > json

### JSON.stringify()

- json --> string

## 异步加载js 

### 三种方案

- defer异步加载

	- 等dom文档全部解析完才会被执行，只有IE能用，也可以将代码写到内部

- saync异步加载

	- 加载完就执行，只能加载外部脚本，不能把js写在script标签里

- 创建script，插入到DOM中，加载完毕后callback

## RegExp正则表达式

### str.test() 

### reg.match()

### 修饰符

- /abcd/i 忽略大小写

	- ignoreCase忽略大小写

- g

	- 执行全局匹配

- m

	- 执行多行匹配

### var reg = /abc/i

### var reg = new RegExp('abc','i')

### str.match(reg)

## web发展历史

### 

## false

### undefind

### null

### NaN

### ""

### 0

### false

## typeof

### number

### string

### boolean

### object

### function

## 编程形式

### 面对过程

### 面对对象

## JS运行三部曲

### 语法分析

- 通篇扫描一遍，不执行

### 预编译

### 解释执行

## DOM操作

### var div = document.createElement('div')

###  var p = document.createElement('p')

### div.setAttribute('class',example')

### p.setAttribute('class','slogan')

### var text = document.createTextNode('最帅')

### p.appendChild(text)

### div.appnedChild(p)

### document.body.appendChild(div)

## 封装insertAfter

### Element.prototype.insertAfter = function(targetNode,afterNode)

### {var beforNode = afterNode.nextElementSibling;}

### if(beforeNode == null){this.appendChild(targetNode;)else{this.insertBefore(targetNode,beforeNode)}}

## 语言

### 编译

- 通篇翻译再执行
- 快、没法跨平台

### 解释

- 一般翻译一边执行
- 稍微慢，可跨平台

*XMind: ZEN - Trial Version*