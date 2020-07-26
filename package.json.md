### 简单版的package.json

当我们新建一个项目时，使用 `yarn init -y `或 `npm init -y` 命令后，在项目目录下会新增一个 `package.json`文件，内容如下：
```
{
  "name": "xxxx", # 项目名称
  "version": "1.0.0", # 项目版本（格式：大版本.次要版本.小版本）
  "description": "", # 项目描述
  "main": "index.js", # 入口文件
  "scripts": { # 指定运行脚本命令的 npm 命令行缩写
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [], # 关键词
  "author": "", # 作者
  "license": "ISC" # 许可证
}
```
### 必备属性(`name`&`version`)
- `name`
- `version`

组成`npm`模块的唯一标识

### name字段
`name`字段不能与其他模块名重复，我们可以执行以下命令查看模块名是否已经被使用：
```
npm view <packageName>
```
### `version`字段
`npm`包中的模块版本都需要遵循 `SemVer` 规范，该规范的标准版本号采用 X.Y.Z 的格式，其中 X、Y 和 Z 均为非负的整数，且禁止在数字前方补零：
- `X`是主版本号：修改了不可兼容的API
- `Y`是次版本号：新增了向下兼容的功能
- `Z`是修订号：修正了向下兼容的问题

当某个版本改动比较大、并非稳定而且可能无法满足预期的兼容性需求时，我们可能要先发布一个**先行版本**。

先行版本号可以加到`主版本号.次版本号.修订号`的后面，通过 `-` 号连接一连串以句点分隔的标识符和版本编译信息：
- 内部版本`alpha`
- 公测版本`beta`
- 正式版本的候选版本`rc`即 Release candiate）

```
npm view <packageName> version // 查看某个版本的最新版本

npm view <packageName> versions //查看某个版本的所有版本
```

### 描述信息(`description`&`keywords`)
- `description`字段用于添加模块的描述信息，便于用户了解该模块
- `keywords`字段用于给模块添加关键字

### 安装项目依赖(`dependencies`&`devDependencies`)
- `dependencies`字段指定了项目`运行`所依赖的模块（生产环境使用）
  - `antd`
  - `react`
  - `moment`
- `devDependencies`字段指定了项目`开发`所需要的模块（开发环境使用）
  - `webpack`
  - `typescript`
  - `babel`
```
npm install <pageage> --save //写入dependencies

npm install <pageage> --save-dev //写入devDependencies
```
```
yarn add <pageage> //写入dependencies

yarn add <pageage> --dev //写入devDependencies
```

### 简化终端命令（scripts）
`scripts` 字段是 `package.json` 中的一种元数据功能，它接受一个对象，对象的属性为可以通过 `npm run` 运行的脚本，值为实际运行的命令（通常是终端命令），如：
```
"scripts":{
    "start":"node index.js"
}
```
将终端命令`scripts`字段，既可以记录它们又可以轻松实现重用。

### 定义项目入口(`main`)
`main`字段是`package.json`中的另一种元数据功能，它可以用来指定加载的入口文件。假如你的项目是一个`npm`包，当用户安装你的包后，`require('my-module')`返回的是`main`字段中所列出文件的`module.exports`属性。

当不指定`main`字段，默认值是模块根目录下面的`index.js`文件。

### 指定项目node版本(`engines`)
有时候，新拉一个项目的时候，由于和其他开发使用的`node`版本不同，导致会出现很多奇奇怪怪的问题（如某些依赖安装报错、依赖安装完项目跑步起来等）。

为了实现项目开箱即用的伟大理想，这时候可以使用 `package.json` 的 `engines` 字段来指定项目 `node` 版本：
```
"engines":{
    "node":">= 8.16.0"
}
```
该字段也可以指定适用的 npm 版本:
```
"engines":{
    "npm":">= 6.9.0"
}
```
**需要注意的是，engines属性仅起到一个说明的作用，当用户版本不符合指定值时也不影响依赖的安装。**

### 自定义命令(`bin`)
用过`vue-cli`、`create-react-app`等脚手架的朋友们，就可以使用类似`vue create/create-react-app`之类的命令，其实这和`package.json`中的`bin`字段有关。

`bin`字段用来指定各个内部命令对应的可执行文件的位置。当`package.json `提供了 `bin` 字段后，即相当于做了一个命令名和本地文件名的映射。

当用户安装带有` bin `字段的包时，
- 如果是全局安装，`npm` 将会使用符号链接把这些文件链接到`/usr/local/node_modules/.bin/`；
- 如果是本地安装，会链接到`./node_modules/.bin/`。

如果要使用` my-app-cli` 作为命令时，可以配置以下` bin` 字段：
```
"bin":{
    "my-app-cli":"./bin/cli.js"
}
```
上面代码指定，`my-app-cli` 命令对应的可执行文件为` bin `子目录下的 `cli.js`，因此在安装了 `my-app-cli` 包的项目中，就可以很方便地利用 npm执行脚本：
```
"scripts":{
    start:"node node_modules/.bin/my-app-cli"
}
```
怎么看起来和 `vue create/create-react-app`之类的命令不太像？原因：
- 当需要 `node` 环境时就需要加上` node` 前缀
- 如果加上 `node` 前缀，就需要指定 `my-app-cli` 的路径 -> `node_modules/.bin`，否则 `node my-app-cli`会去查找当前路径下的 `my-app-cli.js`，这样肯定是不对。

若要实现像 `vue create/create-react-app`之类的命令一样简便的方式，则可以在上文提到的 `bin` 子目录下可执行文件`cli.js` 中的第一行写入以下命令： 
```
#!/usr/bin/env node 
```
这行命令的作用是告诉系统用 `node` 解析，这样命令就可以简写成 `my-app-cli` 了。

### 开发环境解决跨域问题(proxy)
在做前后端分离的项目的时候，调用接口时则会遇到遇到跨域的问题，当在开发环境中，可以通过配置`pageage.json`中的`proxy`来解决跨域问题。
```
{
    "proxy":"http://localhost:9800"
    // 配置要请求的服务器地址
}
```
### 根据开发环境采用不同的全局变量值（自定义字段）
```
"scripts":{
    "start":"NODE_ENV=development node scripts/start.js",
    "build":"NODE_ENV=production node scripts/build.js"
}
```
项目启动起来后，在代码中我们可以通过`process.env.NODE_ENV`访问到`NODE_ENV`的值
```
let sentryUrl;
if(process.env.NODE_ENV === 'development'){
    sentryUrl = 'xxxxx'
}else{
    sentryUrl = 'yyyyy'
}
```
