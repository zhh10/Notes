### 1. Vue中key的原理？
有key便于diff算法的更新，key的唯一性，直接通过新子节点的key查询是否存在于旧子节点中，能让算法更快地找到更新的dom，需要注意的是，key要具有唯一性，而且注意不要使用随机数或者index，因为diff是同级比较。

### 2. v-show与v-if有什么区别？使用场景分别是什么？
- v-show控制的是display属性，适合频繁切换；若v-show为false，display为none；若为true，display为原来的值。
- v-if为false，是直接删除节点，有较高的切换开销。

### 3. 怎么给Vue定义全局的方法
- 挂载到Vue中的prototype
- 利用全局混入Mixin 

### 4. 使用Vue渲染大量数据时应该怎么优化？
使用ES6中的`Object.freeze`，对于data或Vuex里使用freeze冻结了的数据，vue不会做getter和setter的切换，可以让性能大幅提升。

### 5. Vue实例会在什么时候被销毁
- v-if为false
- 路由跳转的时候
- 没有使用`keep-alive`的组件切换

### 6. keep-alive的理解
`keep-alive`是Vue提供的一个抽象组件，用来对组件进行缓存，从而节省性能。

### 7. 虚拟Dom的作用
虚拟Dom的最终目标是将虚拟节点渲染到视图上，但如果直接使用虚拟节点覆盖旧节点，会有很多不必要的Dom操作，造成性能浪费，为了避免不必要的Dom操作，将虚拟Dom与上一次渲染视图所使用的旧虚拟Dom做对比，找出需要更新的节点进行Dom操作。

**虚拟Dom的优势**

- 因为虚拟Dom本质是一个JS对象，具有跨平台的优势：浏览器、小程序、Node
- Dom操作将其耗费性能，而创建一个JS对象性能耗费较低，将Dom对比操作放在JS层，提高了效率

### 8. v-if和v-for的优先级是什么，如果这两个同时出现，那应该怎么优化才能得到更好的性能？
v-for的优先级比v-if高，所以会优先v-for，再v-if，如果不处理，性能将造成浪费。

**解决办法:**

- 使用template
```
<template v-if="isShow">
  <div v-for="(item,index) in List" :key="item.id">{{item}}</div>
</template>
```
- 使用计算属性

### 9. Vue实现强制刷新
- this.$forceUpdate 
```
<button @click="reflash">刷新</button>

methods:{
  reflash(){
    this.$forceUpdate()
  }
}
```
- v-if配合$nextTick
```
<div v-if="reload">
  <div>这是页面内容</div>
  <button @click="reflash">刷新</button>
</div>

data(){
  reload:true
},
methods:{
  reflash(){
    this.reload = false
    this.$nextTick(()=>{
      this.reload = true
    })
  }
}
```
### 10. Vue中的data必须是一个函数
因为Js的特性导致，在component中，data必须以函数的形式存在，不可以是对象。组件中的data写成一个函数，数据以函数返回值的形式定义，这样在复用组件的时候，都会返回一个新的data，相当于每个组件实例都有自己私有的数据空间，它们只负责各自维护的数据，不会造成混乱。

### 11. assets和static的区别

- 相同点: assets和static两个都是存放静态资源文件，项目中所需要的资源文件图片、字体图标、样式文件都可以放在两个文件中。
- 不同点: assets中存放的静态资源文件在项目文件打包时，会将assets中放置的静态资源文件进行打包上传，会进行压缩体积，代码格式化，而压缩后的静态资源文件最终也会被放置在static文件中跟着index.html一同上传到服务器。static中放置的静态资源文件直接上传至服务器，避免了压缩直接进行上传，因为static中的资源文件没进行打包压缩，所以文件的体积也就相对于assets中打包后的文件提交较大点。在服务器中就会占据更大的空间。

第三方的资源文件可以放置在static中，因为这些引入的第三方文件已经经过处理了，我们不再需要处理，直接上传。

### 12. 解决Vue初始化页面闪动问题
在vue初始化之前，由于 div 是不归 vue 管的，所以我们写的代码在还没有解析的情况下会容易出现花屏现象，看到类似于 {{message}} 的字样，虽然一般情况下这个时间很短暂，但是我们还是有必要让解决这个问题的。使用`v-cloak`指令，`v-cloak`这个指令保持在元素上直到关联实例结束编译，可以解决闪烁问题。
```
[v-cloak]{
  display:none
}
```
```
<div v-cloak></div>
```
编译结束，v-cloak消失，display显示正常。
或者:
```
<div style="display:none;" :style="{display:block}"></div>
```
### 13. Vue中如何检测数组变化?
- 进行劫持的方式，重写数组的方法
- 进行原型链重写，调用数组原API时，会通知依赖更新，如果新进来的值中包含着引用类型，还会继续对其进行监控。

### 14. computed不需要deep？
因为computed内部是放在模版`{{}}`里的，
