## ES6 与 commonJS的差异
1. `commonJS`输出的值是值的拷贝，即原来模块中的值改变不会影响已经加载的该值，es6模块化是静态分析，动态引用，输出的是值的引用，值改变，引用也改变，即原来模块中的值改变，则该加载的值也改变。
2. `commonJS`模块是运行时加载，es6模块是编译时输出接口。
3. `commonJS`加载的是整个模块，即将所有的接口全部加载进来，es6可以单独加载其中某个接。
4. `commonJS`中的this指向当前模块，es6模块化的this指向undefined。

es6模块化运行机制与`commonJS`不一样，JS引擎对脚本静态分析的时候，遇到模块加载命令`import`，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块去取值，es6模块化不会缓存运行结果，而是动态地去加载的模块取值，而且变量总是绑定在其所在的模块。

## commonJS 规范
Node在解析JS模块时，会先按文本读取内容，然后将模块内容进行包裹，在外层包裹了一个`function`,传入变量。

commonJS规范是在代码运行时同步阻塞地加载模块，在执行代码过程中遇到`require(X)`会停下来等待，直到新的模块加载完成后再继续执行接下来的代码。

```
function require(modulePath){
    //1. 将modulePath转化为绝对路径
    // D:\Users\NodeJS\myModule.js
    // 2. 判断是否该模块已经有缓存
    if(require.cache["D:\User\NodeJS\myModule.js"]){
        return require.cache["D:\User\NodeJS\myModule.js"]
    }
    // 3. 读取文件内容
    // 4. 包裹到一个函数中
    function _temp(module,exports,require,__dirname,__filename){
        console.log("当前模块路径",__dirname)
        console.log("当面模块文件",__dirname)
        exports.c = 3 
        module.exports = {
            a:1,
            b:2
        }
        this.m = 5
    }
    // 5. 创建module对象
    module.exports = {} 
    const exports = module.exports 
    
    __temp.call(module.exports, module, exports, require, module.path, module.filename)
    
    return module.exports;
    }
    require.cache = {};
    
}
```

## commonJS的缓存
> 文件查询挺耗时的，还有在实际开发中，模块可能包含副作用代码，例如在模块顶层执行`addEventListener`,如果require过程中被重复执行多次可能会出现问题。

commonJS中的缓存可以解决重复查找和重复执行的问题。以绝对路径为`key`，`module`对象为`value`写入`cache`。在读取模块的时候会优先判断是否已在缓存中，如果在，直接返回`module.exports`，如果不在，则会进入模块查找的流程。

```
//a.js 
module.exports = {
    foo:1
}

// main.js
const a1 = require('./a.js')
a1.foo = 2;

const a2 = require('./a.js')


console.log(a2.foo) //2
console.log(a1 === a2) //true
```




