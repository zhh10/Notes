### 官网
```
sass-lang.com/install
```

### 变量 Variables
- $符号
```
$primary-color:#1259b5;
$primary-border:1px solid $primary-color;

div.box{
    color:$primary-color
}
h1.page-header{
    border:$primary-border;
}
```
### 嵌套 Nesting
```
.nav{
    height:100px;
    ul{
        margin:0;
        li{
            float:left;
            list-style:none;
            padding:5px;
        }
    }
}
```
### 嵌套时调用父选择器
- &符号
```
.nav{
    height:100px;
    ul{
        margin:0;
        li{
            float:left;
            list-style:none;
            padding:5px;
            a{
                display:block;
                color:#000;
                padding:5px;
                &:hover{
                    background-color:#0d2f7e;
                    color:#fff;
                }
            }
        }
    }
}
```
### 嵌套属性
```
body{
    font:{
        size:15px;
        weight:bold
    }
}
.nav{
    border:1px solid #000{
        left:0;
        right:0;
    }
}
```
### 混合 Mixin
- @mixin
- @include
```
@mixin 名字(参数1，参数2){
    ...
}
```
```
@mixin alert{
    color:#8a6d3b;
    background-color:#fcf8e3;
    a{
        color:#000;
    }
}

.alert-warning{
    @include alert ;
}

// 翻译成css 
.alert-warning{
    color:#8a6d3b;
    background-color:#fcf8e3;
}
.alert-warning a{
    color:#000;
}
```

### Mixin里的参数
```
@mixin alert($text-color,$background){
    color:$text-color;
    background-color:$background;
    a{
        color:darken($text-color,10);
    }
}

.alert-warning{
    @include alert(#8a6d3b,#fcf8e3)
}
.alert-info{
    @include alert($background:#fcf8e3,$text-color:#8a6d3b)
}
```
### 继承/扩展 —— inheritance
- @inheritance
```
.alert{
    padding:15px;
}
.alert-info{
    @extend .alert; // 与alert相关的样式也会被继承过来
    background:#d9edf7;
}

//翻译成css
.alert .alert-info{
    padding:15px;
}
.alert-info{
    background:#d9edf7;
} 
```
### Partials与@import
- @import 把其他的css文件包含进来
- Particals要用下划线开头，这样不会去编译它
```
// _base.scss
body{
    margin:0;
    padding:0;
}
```
```
@import "base";
```
### 列表
```
border{
    1px solid #000;
}
padding:{
    (5px 10px) (5px 0)
}
padding{
    5px 10px,5px 0
}
```
### interpolation
```
$name:'info';
$attr:'border';
.alert-#{$name}{
    #{$attr}-color:#ccc;
}
```
### 控制指令 Control Directives
#### @if
```
@if 条件 {
    ...
} 
```
```
$use-prefixes:true;
.rounded{
    @if $use-prefixes{
        -webkit-border-radius:5px;
        -moz-border-radius:5px;
        -ms-border-radius:5px;
        -o-border-radius:5px;
    }
    border-raduis:5px;
}
```
```
body{
    @if $theme == dark{
        background-color:black;
    }@else if @theme == light{
        background-color:white;
    }@else{
        background-color:grey;
    }
}
```
#### @for 
```
@for $var from <开始值> through <结束值> {
    
}
```
```
@for $var from <开始值> to <结束值>{
    
} 
```
```
$columns : 4;
// 值到4的时候停止
@for $i from 1 through $columns{
    .col-#{$i}{
        width:100%/$columns * $i;
    }
}

// 值到3的时候停止
@for $i from 1 to $columns{
    .col-#{$i}{
        width:100%/$columns * $i;
    }
}
```
#### @each
```
@each $var in $list {
    
}
```
```
$icons: success error warning;
@each $icon in $icons {
    .icon-#{$icon}{
        background-image:url(../images/icons/#{$icon}.png)
    }
}
```
#### @while
```
@while 条件{
    
}
```
```
$li:6;
@while $li>0 {
    .item-#{$i}{
        width:5px * $i;
    }
    $i : $i - 2;
}
```

### 用户自定义的函数 function
```
@function 名称(参数1，参数2){
    
}
```

