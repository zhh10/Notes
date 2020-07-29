### 1. 下面输出什么？如果是在严格模式下呢？
```
var a = function(){
    this.b = 3
}
var c = new a() 
a.prototype.b = 9
var b = 7 
a()

console.log(b)  //3
console.log(c.b) //3
```
如果是严格模式，那么就会报错，因为严格模式下，`this`指向不是`window`，而是`undefined`。

### 2. 输出什么？
```
var a = 0;
if(true){
  var a = 1;
  function a(){};
  var a = 21;
  console.log(a)
}
console.log(a) 
// 21 1
```
新浏览器为了兼容ES3、ES6
- `{}`块级作用域下的`function`，在全局下只声明，不定义（不赋值）
- `{}`出现`function、const、let`创建一个块级上下文

### 3. 不借助变量,交换两个数
```
function swap(a,b){
  a = a + b;
  b = a - b;
  a = a - b;
  return a,b
}
```

### 4. `==`比较，数据转换的规则
```
console.log([] == false)    // true
console.log(![] == false)   // true
```
- 数据类型一样的几个特殊点:
  - `{} == {} //false` 对象比较的是堆内存的地址
  - `[] == [] //false` 
  - `NaN == NaN // false`
- 数据类型不一样的转换规则
  - `null == undefined //true`
  - `字符串 == 对象` 要把对象转换为字符串
  - 剩下如果 `==` 两边数据类型不一致，但是需要转换为数字类型在进行比较
- 把其他数据类型转换为布尔值
  - 基于以下方式可以把其他数据类型转换为布尔
    - `!`转换为布尔值后取反
    - `!!` 转换为布尔值
    - `Boolean(val)`
  - 隐式转换
    - 在循环或者条件判断中，条件处理的结果就是布尔类型值
    
    
  **规定:  只有0、NaN、null、undefined、空字符串 五个值变成布尔的false,其余都是true**
  
### 5. 变量赋值
```
let a = {n:1};
let b = a;
a.x = a = {n:2};
console.log(a.x) // undefined
console.log(b)   // {n:1,x:{n:2}}
```
- **变量赋值都是指针指向过程，先创建值，再创建变量，最后指针关联**
- **带成员访问的优先处理**

1. 先创建`{n:1}`,a指向`{n:1}`的地址
2. b与a指向同一个地址
3. 先创建一个`{n:2}`的地址
4. `{n:1}`中的x指向`{n:2}`,然后a的地址更改为`{n:2}`

### 6. es5与es6的继承有什么不同？
- es5继承，即原型链继承，先创造子类的实例对象this，然后再把父类的方法添加到this上。
- es6继承，即`class`类继承，子类没有自己的this，是通过`constructor`中的`super`继承父类的this，然后对this进行加工。
