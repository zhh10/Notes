# loader 
```
module:{
  rules:[{
    test:/\.js$/,
    use:[path.resolve(__dirname,'loader','loader3.js'),
         path.resolve(__dirname,'loader','loader2.js'),
         path.resolve(__dirname,'loader','loader1.js')]
  }]
}
```
- 正常调用顺序是`loader1,loader2,loader3`,但真正调用的顺序是`loader3(pitch)、loader2(pitch)、loader1(pitch)、loader1、loader2、loader3`,如果其中任何一个`pitching loader`返回了值就相当于它以及它右边的`loader`已经执行完毕
- 如果`loader2 pitch`返回了值，接下来只有`loader3`被执行
- `loader`根据返回值可以分为两种，一种是返回JS代码(有`module.exports`)的`loader`,还有不能作为最左边的其他`loader`

**loader/loader1.js**
```
function loader(source){
    console.log('loader1')
    return source+1
}
loader.pitch = function(remainingRequest,previousRequest,data){
    console.log(remainingRequest,previousRequest,data)
    data.name = 'pitch1'
    console.log('pitch1')
}
module.exports = loader
```
**loader/loader2.js**
```
function loader(source){
    console.log('loader2')
    return source + '//2'
}
loader.pitch = function(remainingRequest,previousRequest,data){
    console.log('remainingRequet=',remainingRequest)
    console.log('previousRequest=',previousRequest)
    console.log('pitch2')
}
module.exports = loader
```
**loader/loader3.js**
```
function loader(source){
    console.log('loader3')
    return source + '//3'
}

loader.pitch = function(){
    console.log('loader3')
}
module.exports = loader
```

# plugin
- 是一个独立模块
- 对外暴露一个JS函数
- 函数原型(prototype)上定义了一个注入`compiler`对象的`apply`方法，`apply`函数中需要通过`compiler`对象挂载的`webpack`钩子，钩子的回调中能拿到当前编译的`compilation`对象，如果是异步编译插件中可以拿到回调`callback`
- 完成自定义编译流程并处理`compilation`对象的内部数据
- 如果是异步编程插件的话，数据处理完成后执行`callback`回调

## 开发基本形式
```
class BasicPlugin{
    constructor(pluginOptions){
        this.options = pluginOptions
    }
    // 原型(prototype)上定义了一个注入`compiler`对象的`apply`方法
    apply(compiler){
        compiler.plugin('emit',function(compilation,callback){
            console.log(compilation)
            callback()
        })
    }
}
module.exports = BasicPlugin                                                                                                                                                                                                                                                                                                              
```

## compiler对象
`compiler`对象是`webpack`的编译器对象，`compiler`对象会在启动`webpack`的时候一次性初始化，`compiler`对象中包含了所有`webpack`可自定义操作的配置，例如 `loader` 的配置，`plugin `的配置，`entry `的配置等各种原始` webpack` 配置等。

## compilation对象
compilation对象实例继承于compiler，compilation 对象代表了一次单一的版本 webpack 构建和生成编译资源的过程。当运行 webpack 开发环境中间件时，每当检测到一个文件变化，一次新的编译将被创建，从而生成一组新的编译资源以及新的 compilation 对象。一个 compilation 对象包含了 当前的模块资源、编译生成资源、变化的文件、以及 被跟踪依赖的状态信息。编译对象也提供了很多关键点回调供插件做自定义处理时选择使用。

Compiler 和 Compilation 的区别在于：Compiler 代表了整个 Webpack 从启动到关闭的生命周期，而 Compilation 只代表一次新的编译。
