### 1. 在浏览器地址栏中输入一个页面地址，按下回车键发生了什么？
1. 浏览器将url地址补充完整：没有书写协议，添加上协议
2. 浏览器对url地址进行url编码：如果url地址中出现非ASCII字符，则浏览器会对其进行编码
3. 浏览器构造一个没有消息体的GET请求，发送至服务器，等待服务器的响应，此时浏览器标签页往往会出现一个等待的图标
4. 服务器接收到请求，将一个HTML页面代码组装到消息体中，响应给浏览器
5. 浏览器拿到服务器的响应后，丢弃掉当前页面，开始渲染消息体的html代码。浏览器之所以直到这是一个html代码，是因为服务器的响应头指定了消息类型为text/html
6. 浏览器在渲染页面的过程中，发现有其他的嵌入资源，如CSS、JS、图片等
7. 浏览器使用不阻塞渲染的方式，重新向服务器发送对该资源的请求，拿到响应结果后根据Content-Type做相应处理
8. 当所有的资源都已下载并处理后，浏览器触发window.onload事件

### 2. AJAX请求
```
var xhr = new XMLHttpRequest() //创建发送请求的对象
xhr.onreadystatechange = function(){
    // 当请求状态发生改变时运行的函数
    // 0: 刚刚创建好了请求对象，但还未配置请求（未调用open方法）
    // 1: open方法已被调用
    // 2: send方法已被调用
    // 3: 正在接收服务器的响应消息体
    // 4: 服务器响应的所有内容均已接收完毕
    
    // xhr.responseText： 获取服务器响应的消息体文本

    // xhr.getResponseHeader("Content-Type") 获取响应头Content-Type
}
xhr.setRequestHeader('Content-Type','application/json') //设置请求头
xhr.open('请求方法','URL地址') //配置请求
xhr.send('请求体内容') //构建请求体 发送到服务器
```
### 3. get和post的区别
1. get请求的数据会跟在url后面
2. post请求把提交的数据放置在http的请求体中
3. 因为浏览器对url的长度有所限制，所以get请求的传输数据就受到了限制
4. post方法提交的数据没有限制
5. post安全性要比get高，因为get提交数据将以明文出现在浏览器中，以key/valu对的序列附加在url中


