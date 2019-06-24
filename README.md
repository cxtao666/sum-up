# vue和node总结

## js代码注意事项

 当你采用了无分号的代码风格的时候，只需要注意以下情况就不会有上面的问题了：
    当一行代码是以：
        (
        [
        `
        开头的时候，则在前面补上一个分号用以避免一些语法解析错误。
    所以你会发现在一些第三方的代码中能看到一上来就以一个 ; 开头。
  结论：
    无论你的代码是否有分号，都建议如果一行代码是以 (、[、` 开头的，则最好都在其前面补上一个分号。
    有些人也喜欢玩儿一些花哨的东西，例如可以使用 ! ~ 等。



## centos系统

安装yum,vim,nvm

## 包管理工具npm

首先安装nvm，然后再这基础上安装node和npm

- package.json 包描述文件
  - 就是产品的说明书
  - `dependencies` 属性，用来保存项目的第三方包依赖项信息
  - 所以建议每个项目都要有且只有一个 package.json (存放在项目的根目录)
  - 我们可以通过 `npm init [--yes]` 来生成 package.json 文件
  - 同样的，为了保存依赖项信息，我们每次安装第三方包的时候都要加上：`--save` 选项。
- npm 常用命令
  - install
  - uninstall

## node

### 基础介绍

在 Node 中，采用 EcmaScript 进行编码

没有 BOM、DOM

和浏览器中的 JavaScript 不一样

浏览器中的 JavaScript 是没有文件操作的能力的

但是 Node 中的 JavaScript 具有文件操作的能力

### 模块化

使用 require 方法加载 fs 核心模块

- - 在 Node 中没有全局作用域的概念
  - 在 Node 中，只能通过 require 方法来加载执行多个 JavaScript 脚本文件
  - require 加载只能是执行其中的代码，文件与文件之间由于是模块作用域，所以不会有污染的问题
    - 模块完全是封闭的
    - 外部无法访问内部
    - 内部也无法访问外部
  - 模块作用域固然带来了一些好处，可以加载执行多个文件，可以完全避免变量命名冲突污染的问题
  - 但是某些情况下，模块与模块是需要进行通信的
  - 在每个模块中，都提供了一个对象：`exports`
  - 该对象默认是一个空对象
  - 你要做的就是把需要被外部访问使用的成员手动的挂载到 `exports` 接口对象中
  - 然后谁来 `require` 这个模块，谁就可以得到模块内部的 `exports` 接口对象
  - 还有其它的一些规则，具体后面讲，以及如何在项目中去使用这种编程方式，会通过后面的案例来处理
- 核心模块
  - 核心模块是由 Node 提供的一个个的具名的模块，它们都有自己特殊的名称标识，例如
    - fs 文件操作模块
    - http 网络服务构建模块
    - os 操作系统信息模块
    - path 路径处理模块
    - 。。。。
  - 所有核心模块在使用的时候都必须手动的先使用 `require` 方法来加载，然后才可以使用，例如：
    - `var fs = require('fs')

#### 读写模块

```javascript
var fs = require("fs")
```

fs 是 file-system 的简写，就是文件系统的意思

在 Node 中如果想要进行文件操作，就必须引入 fs 这个核心模块

在 fs 这个核心模块中，就提供了所有的文件操作相关的 API

##### fs.readFile的使用

fs.readFile 就是用来读取文件的

```javascript
fs.readFile('.dataa.txt', function (error, data) {
 if (error) {
    console.log('读取文件失败了')
  } else {
    console.log(data.toString())
  }
})
```

2. 读取文件

 第一个参数就是要读取的文件路径

第二个参数是一个回调函数

######   成功

​       data 数据

​        error null

######   失败

​       data undefined没有数据

​         error 错误对象

<Buffer 68 65 6c 6c 6f 20 6e 6f 64 65 6a 73 0d 0a>

文件中存储的其实都是二进制数据 0 1

这里为什么看到的不是 0 和 1 呢？原因是二进制转为 16 进制了

但是无论是二进制01还是16进制，人类都不认识

所以我们可以通过 toString 方法把其转为我们能认识的字符

console.log(data)

console.log(error)

 console.log(data)

 在这里就可以通过判断 error 来确认是否有错误发生

##### fs.writeFile使用

```javascript
fs.writeFile('.data你好.md', '大家好，给大家介绍一下，我是Node.js', function (error)  if (error) {
    console.log('写入失败')
  } else {
    console.log('写入成功了')
  }
})
```

第一个参数：文件路径

 第二个参数：文件内容

 第三个参数：回调函数

​    erro

​    成功：

 文件写入成功

error 是 null

  失败：

文件写入失败

error 就是错误对象

#### http模块

```javascript
var http = require('http')
var server = http.createServer()
server.on('request', function () {
  console.log('收到客户端的请求了')
})
server.listen(3000, function () {
  console.log('服务器启动成功了，可以通过 http:127.0.0.1:3000 来进行访问')
})
```

##### 服务器要干嘛

   提供服务：对 数据的服务

   发请求

   接收请求

   处理请求

   给个反馈（发送响应）

   注册 request 请求事件

   当客户端请求过来，就会自动触发服务器的 request 请求事件，然后执行

##### http模块参数

   request 请求事件处理函数，需要接收两个参数：

######   Request 请求对象

   请求对象可以用来获取客户端的一些请求信息，例如请求路径

###### Response 响应对象

​      响应对象可以用来给客户端发送响应消息

###### response步骤

response 对象有一个方法：write 可以用来给客户端发送响应数据

write 可以使用多次，但是最后一定要使用 end 来结束响应，否则客户端会一直等待

告诉客户端，我的话说完了，你可以呈递给用户了

上面的方式比较麻烦，推荐使用更简单的方式，直接 end 的同时发送响应数据

 res.end('hello nodejs')

根据不同的请求路径发送不同的响应结果

\1. 获取请求路径

​     req.url 获取到的是端口号之后的那一部分路径

​     也就是说所有的 url 都是以  开头的

  \2. 判断路径处理响应

 响应内容只能是二进制数据或者字符串

​     数字

​     对象

​     数组

​     布尔值

##### path模块

- path 模块
- __dirname 和 __filename
  - **动态的** 获取当前文件或者文件所处目录的绝对路径
  - 用来解决文件操作路劲的相对路径问题
  - 因为在文件操作中，相对路径相对于执行 `node` 命令所处的目录
  - 所以为了尽量避免这个问题，都建议文件操作的相对路劲都转为：**动态的绝对路径**
  - 方式：`path.join(__dirname, '文件名')

##### 端口

ip 地址用来定位计算机

端口号用来定位具体的应用程序

 所有需要联网通信的应用程序都会占用一个端口号

```javascript
server.on('request', function (req, res) {
  console.log('收到请求了，请求路径是：' + req.url)
  console.log('请求我的客户端的地址是：', req.socket.remoteAddress, req.socket.remotePort)

  res.end('hello nodejs')
})
```

```javascript
 res.setHeader('Content-Type', 'textplain; charset=utf-8')
  res.end('hello 世界')
```

 在服务端默认发送的数据，其实是 utf8 编码的内容

  但是浏览器不知道你是 utf8 编码的内容

  浏览器在不知道服务器响应内容的编码的情况下会按照当前操作系统的默认编码去解析

  中文操作系统默认是 gbk

  解决方法就是正确的告诉浏览器我给你发送的内容是什么编码的

  在 http 协议中，Content-Type 就是用来告知对方我给你发送的数据内容是什么类型

######  关于Content-Type的类型

[Content-Type]: https:developer.mozilla.orgzh-CN/docs/Web/HTTP/Headers/Content-Type	"HTML"

![ip地址和端口](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\01\ip地址和端口号.png)

#### 重定向

如何在 Node 中实现服务器重定向

- header('location')
  - 301 永久重定向 浏览器会记住
    - a.com b.com
    - a 浏览器不会请求 a 了
    - 直接去跳到 b 了
  - 302 临时重定向 浏览器不记忆
    - a.com b.com
    - a.com 还会请求 a
    - a 告诉浏览器你往 b

### 模板引擎的使用

#### art -template的引入

 art-template
 art-template 不仅可以在浏览器使用，也可以在 node 中使用

 安装：
```javascript
    npm install art-template
```
    该命令在哪执行就会把包下载到哪里。默认会下载到 node_modules 目录中
    node_modules 不要改，也不支持改。

 在 Node 中使用 art-template 模板引擎
 模板引起最早就是诞生于服务器领域，后来才发展到了前端。

 1. 安装 npm install art-template
 2. 在需要使用的文件模块中加载 art-template
    只需要使用 require 方法加载就可以了：require('art-template')
    参数中的 art-template 就是你下载的包的名字
    也就是说你 isntall 的名字是什么，则你 require 中的就是什么
 3. 查文档，使用模板引擎的 API
      默认读取到的 data 是二进制数据
      而模板引擎的 render 方法需要接收的是字符串
      所以我们在这里需要把 data 二进制数据转为 字符串 才可以给模板引擎使用
  4. ![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\02\code\服务端渲染.png)
  5. ![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\02\code\客户端渲染.png)
  ```javascript
  var template = require('art-template')
var fs = require('fs')
 var tplStr = `
 <!DOCTYPE html>
 <html lang="en">
 <head>
   <meta charset="UTF-8">
   <title>Document<title>
 <head>
 <body>
   <p>大家好，我叫：{{ name }}<p>
   <p>我今年 {{ age }} 岁了<p>
   <h1>我来自 {{ province }}<h1>
   <p>我喜欢：{{each hobbies}} {{ $value }} {{each}}<p>
 <body>
 <html>
 `
  fs.readFile('.tpl.html', function (err, data) {
  if (err) {
    return console.log('读取文件失败了')
  }
  var ret = template.render(data.toString(), {
    name: 'Jack',
    age: 18,
    province: '北京市',
    hobbies: [
      '写代码',
      '唱歌',
      '打游戏'
    ],
    title: '个人'
  })

  console.log(ret)
})
![服务端渲染](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\02\服务端渲染.png)
  ```



#### 前端渲染和后端渲染

- 代码风格
- 无分号
  - `(`
  - `[`
  - `
  - 最好前面补分号，避免一些问题
  - 《编写可维护的 JavaScript》
  - 不仅是功能，还要写的漂亮
- 服务端渲染
  - 说白了就是在服务端使用模板引擎
  - 模板引擎最早诞生于服务端，后来才发展到了前端
- 服务端渲染和客户端渲染的区别
  - 客户端渲染不利于 SEO 搜索引擎优化
  - 服务端渲染是可以被爬虫抓取到的，客户端异步渲染是很难被爬虫抓取到的
  - 所以你会发现真正的网站既不是纯异步也不是纯服务端渲染出来的
  - 而是两者结合来做的
  - 例如京东的商品列表就采用的是服务端渲染，目的了为了 SEO 搜索引擎优化
  - 而它的商品评论列表为了用户体验，而且也不需要 SEO 优化，所以采用是客户端渲染

## 

###  模块化

#### module.exports和exports的区分

 在 Node 中，每个模块内部都有一个自己的 module 对象
 该 module 对象中，有一个成员叫：exports 也是一个对象
 也就是说如果你需要对外导出成员，只需要把导出的成员挂载到 module.exports 中

 我们发现，每次导出接口成员的时候都通过 module.exports.xxx = xxx 的方式很麻烦，点儿的太多了
 所以，Node 为了简化你的操作，专门提供了一个变量：exports 等于 module.exports

 var module = {
   exports: {
     foo: 'bar',
     add: function
   }
 }

 也就是说在模块中还有这么一句代码
 var exports = module.exports

 module.exports.foo = 'bar'

 module.exports.add = function (x, y) {
   return x + y
 }

 两者一致，那就说明，我可以使用任意一方来导出内部成员
 console.log(exports === module.exports)

 exports.foo = 'bar'
 module.exports.add = function (x, y) {
   return x + y
 }

 当一个模块需要导出单个成员的时候
 直接给 exports 赋值是不管用的

 exports.a = 123

 exports = {}
 exports.foo = 'bar'

 module.exports.b = 456

 给 exports 赋值会断开和 module.exports 之间的引用
 同理，给 module.exports 重新赋值也会断开

 这里导致 exports !== module.exports
 module.exports = {
   foo: 'bar'
 }

  但是这里又重新建立两者的引用关系
 exports = module.exports

 exports.foo = 'hello'

 {foo: bar}
exports.foo = 'bar'


 {foo: bar, a: 123}
module.exports.a = 123

 exports !== module.exports
 最终 return 的是 module.exports
 所以无论你 exports 中的成员是什么都没用
exports = {
  a: 456
}

 {foo: 'haha', a: 123}
module.exports.foo = 'haha'

 没关系，混淆你的
exports.c = 456

 重新建立了和 module.exports 之间的引用关系了
exports = module.exports

 由于在上面建立了引用关系，所以这里是生效的
 {foo: 'haha', a: 789}
exports.a = 789

 前面再牛逼，在这里都全部推翻了，重新赋值
 最终得到的是 Function
module.exports = function () {
  console.log('hello')
}

------

 真正去使用的时候：
    导出多个成员：exports.xxx = xxx
    导出多个成员也可以：module.exports = {
                        }
    导出单个成员：module.exports

 谁来 require 我，谁就得到 module.exports
 默认在代码的最后有一句：
 一定要记住，最后 return 的是 module.exports
 不是 exports
 所以你给 exports 重新赋值不管用，
 return module.exports

#### 模块化加载

 如果是非路径形式的模块标识

 路径形式的模块：

  ./ 当前目录，不可省略

  ../ 上一级目录，不可省略

  /xxx 几乎不用

  d:/a/foo.js 几乎不用

  首位的 / 在这里表示的是当前文件模块所属磁盘根路径

  .js 后缀名可以省略

 require('./foo.js')

 核心模块的本质也是文件

 核心模块文件已经被编译到了二进制文件中了，我们只需要按照名字来加载就可以了

 require('fs')

 require('http')

 第三方模块

 凡是第三方模块都必须通过 npm 来下载

 使用的时候就可以通过 require('包名') 的方式来进行加载才可以使用

 不可能有任何一个第三方包和核心模块的名字是一样的

 既不是核心模块、也不是路径形式的模块

​    先找到当前文件所处目录中的 node_modules 目录

​    node_modules/art-template

​    node_modules/art-template/package.json 文件

​    node_modules/art-template/package.json 文件中的 main 属性

​    main 属性中就记录了 art-template 的入口模块

​    然后加载使用这个第三方包

​    实际上最终加载的还是文件

​    如果 package.json 文件不存在或者 main 指定的入口模块是也没有

​    则 node 会自动找该目录下的 index.js

​    也就是说 index.js 会作为一个默认备选项

​    

​    如果以上所有任何一个条件都不成立，则会进入上一级目录中的 node_modules 目录查找

​    如果上一级还没有，则继续往上上一级查找

​    。。。

​    如果直到当前磁盘根目录还找不到，最后报错：

​      can not find module xxx

 var template = require('art-template')

 

 注意：我们一个项目有且只有一个 node_modules，放在项目根目录中，这样的话项目中所有的子目录中的代码都可以加载到第三方包

 不会出现有多个 node_modules

 模块查找机制

​    优先从缓存加载

​    核心模块

​    路径形式的文件模块

​    第三方模块

​      node_modules/art-template/

​      node_modules/art-template/package.json

​      node_modules/art-template/package.json main

​      index.js 备选项

​      进入上一级目录找 node_modules

​      按照这个规则依次往上找，直到磁盘根目录还找不到，最后报错：Can not find moudle xxx

​    一个项目有且仅有一个 node_modules 而且是存放到项目的根目录

#### 模块化注意

​     咱们所使用的所有文件操作的 API 都是异步的
 就像你的 ajax 请求一样
 文件操作中的相对路径可以省略 ./
 fs.readFile('data/a.txt', function (err, data) {
   if (err) {
​     return console.log('读取失败')
   }
   console.log(data.toString())
 })

 在模块加载中，相对路径中的 ./ 不能省略
 Error: Cannot find module 'data/foo.js'
 require('data/foo.js')

 require('./data/foo.js')('hello')

 在文件操作的相对路径中
    ./data/a.txt 相对于当前目录
    data/a.txt   相对于当前目录
    /data/a.txt  绝对路径，当前文件模块所处磁盘根目录
    c:/xx/xx...  绝对路径
 fs.readFile('./data/a.txt', function (err, data) {
   if (err) {
     console.log(err)
     return console.log('读取失败')
   }
   console.log(data.toString())
 })

 这里如果忽略了 . 则也是磁盘根目录

**在 Node 没有全局作用域，它是文件模块作用域**

**模块是独立，不能因为 a 加载过 fs 了 b 就不需要，这是错误的理解**

 **正确的做法应该是，a 需要 fs 则 a 就加载 fs ，b 需要 fs 则 b 就加载 fs**

### express的使用

 0. 安装

 1. 引包
```javascript
var express = require('express')
var app = express()

app.use('/public/', express.static('./public/'))

app.use('/static/', express.static('./static/'))

app.use('/node_modules/', express.static('./node_modules/'))

app.get('/about', function (req, res) {

   在 Express 中可以直接 req.query 来获取查询字符串参数

  console.log(req.query)

  res.send('你好，我是 Express!')
})

app.get('/pinglun', function (req, res) {

   req.query

   在 Express 中使用模板引擎有更好的方式：res.render('文件名， {模板对象})

   可以自己尝试去看 art-template 官方文档：如何让 art-template 结合 Express 来使用

})
app.get('/', function (req, res) {

  res.send(`

<!DOCTYPE html>

<html lang="en">

  <head>

    <meta charset="UTF-8" />

​    <title>Document</title>

  </head>

<body>

  <h1>hello Express！你好</h1>

</body>

</html>

`)

})
app.listen(3000, function () {

  console.log('app is running at port 3000.')

})
})
```


 2. 创建你服务器应用程序

​    也就是原来的 http.createServer

 3. 在 Express 中开放资源就是一个 API 的事儿

 公开指定目录

 只要这样做了，你就可以直接通过 /public/xx 的方式访问 public 目录中的所有资源了

4. 模板引擎，在 Express 也是一个 API 的事儿

 得到路径

 当服务器收到 get 请求 / 的时候，执行回调处理函数

 5. app.listen相当于 server.listen

  #### 路由模块

  router.js 路由模块
  职责：
  处理路由
  根据不同的请求方法+请求路径设置具体的请求处理函数
 模块职责要单一，不要乱写
  我们划分模块的目的就是为了增强项目代码的可维护性,提升开发效率

Express 提供了一种更好的方式
 专门用来包装路由的
var express = require('express')

1. 创建一个路由容器
   var router = express.Router()
2. 把路由都挂载到 router 路由容器中,router.get或router.post 处理请求

3. 最后把router.js导入app.js中     var router = require(‘./router’)，采用app.use(router)方式进行挂在app.js中

4. 浏览器收到 HTML 响应内容之后，就要开始从上到下依次解析，

   ​    当在解析的过程中，如果发现：

   ​      link

   ​      script

   ​      img

   ​      iframe

   ​      video

   ​      audio

   ​    等带有 src 或者 href（link） 属性标签（具有外链的资源）的时候，浏览器会自动对这些资源发起新的请求。

      -->

      <!-- 

   ​      注意：在服务端中，文件中的路径就不要去写相对路径了。

   ​      因为这个时候所有的资源都是通过 url 标识来获取的

   ​      我的服务器开放了 /public/ 目录

   ​      所以这里的请求路径都写成：/public/xxx

   ​      / 在这里就是 url 根路径的意思。

   ​      浏览器在真正发请求的时候会最终把 http:127.0.0.1:3000 拼上

   ​      不要再想文件路径了，把所有的路径都想象成 url 地址

   ​    -->

   5. 以前表单是如何提交的？

   ​      表单中需要提交的表单控件元素必须具有 name 属性

   ​      表单提交分为：

   ​        \1. 默认的提交行为

   ​        \2. 表单异步提交

   ​        action 就是表单提交的地址，说白了就是请求的 url 地址

   ​        method 请求方法

   ​            get

   ​            post

   ​     -->

#### 入口js的作用

  app.js 入门模块

   职责：

  **创建服务**

​    **做一些服务相关配置**

   **模板引擎**

   **body-parser 解析表单 post 请求体**

  **提供静态资源服务**

​    **挂载路由**

  **监听端口启动服务**

#### express中使用模板引擎进行

 配置使用 art-template 模板引擎

 第一个参数，表示，当渲染以 .art 结尾的文件的时候，使用 art-template 模板引擎

 express-art-template 是专门用来在 Express 中把 art-template 整合到 Express 中

 虽然外面这里不需要记载 art-template 但是也必须安装

 原因就在于 express-art-template 依赖了 art-template

 Express 为 Response 相应对象提供了一个方法：render

 render 方法默认是不可以使用，但是如果配置了模板引擎就可以使用了

 res.render('html模板名', {模板数据})

 第一个参数不能写路径，默认会去项目中的 views 目录查找该模板文件

 也就是说 Express 有一个约定：开发人员把所有的视图文件都放到 views 目录中

 如果想要修改默认的 views 目录，则可以

 app.set('views', render函数的默认路径)

 配置 body-parser 中间件（插件，专门用来解析表单 POST 请求体）

 parse application/x-www-form-urlencoded

```javascript
var express = require('express')
var bodyParser = require('body-parser')

var app = express()

app.use('/public/', express.static('./public/'))
app.engine('html', require('express-art-template'))
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
var comments = [{
    name: '张三',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三2',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三3',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三4',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  },
  {
    name: '张三5',
    message: '今天天气不错！',
    dateTime: '2015-10-16'
  }
]

app.get('/', function (req, res) {
  res.render('index.html', {
    comments: comments
  })
})

app.get('/post', function (req, res) {
  res.render('post.html')
})

app.post('/post', function (req, res) {
   1. 获取表单 POST 请求体数据
   2. 处理
   3. 发送响应

   req.query 只能拿 get 请求参数
   console.log(req.query)

  var comment = req.body
  comment.dateTime = '2017-11-5 10:58:51'
  comments.unshift(comment)

   res.send
   res.redirect
   这些方法 Express 会自动结束响应
  res.redirect('/')
   res.statusCode = 302
   res.setHeader('Location', '/') 
})

 app.get('/pinglun', function (req, res) {
   var comment = req.query
   comment.dateTime = '2017-11-5 10:58:51'
   comments.unshift(comment)
   res.redirect('/')
    res.statusCode = 302
    res.setHeader('Location', '/')
 })

app.listen(3000, function () {
  console.log('running...')
})


```



#### **crud**的使用

  数据操作文件模块

 职责：操作文件中的数据，只处理数据，不关心业务

  这里才是我们学习 Node 的精华部分：奥义之所在

  封装异步 API

 咱们所使用的所有文件操作的 API 都是异步的

 就像你的 ajax 请求一样

 文件操作中的相对路径可以省略 ./

 fs.readFile('data/a.txt', function (err, data) {

   if (err) {

​     return console.log('读取失败')

   }

   console.log(data.toString())

 })

 在模块加载中，相对路径中的 ./ 不能省略

 Error: Cannot find module 'data/foo.js'

 require('data/foo.js')

 require('./data/foo.js')('hello')

 在文件操作的相对路径中

​    ./data/a.txt 相对于当前目录

​    data/a.txt   相对于当前目录

​    /data/a.txt  绝对路径，当前文件模块所处磁盘根目录

​    c:/xx/xx...  绝对路径

 fs.readFile('./data/a.txt', function (err, data) {

   if (err) {

​     console.log(err)

​     return console.log('读取失败')

   }

   console.log(data.toString())

 })

 这里如果忽略了 . 则也是磁盘根目录



#### 中间件的使用

##### 中间件的作用

   解析表单 get 请求体

   解析表单 post 请求体

   解析 Cookie

   处理 Session

  使用模板引擎

```
var http = require('http')
var url = require('url')

var cookie = require('./middlewares/cookie')
var postBody = require('./middlewares/post-body')
var query = require('./middlewares/query')
var session = require('./middlewares/session')

var server = http.createServer(function (req, res) {
   解析表单 get 请求体
   解析表单 post 请求体
   解析 Cookie
   处理 Session
   使用模板引擎
   console.log(req.query)
   console.log(req.body)
   console.log(req.cookies)
   console.log(req.session)

   解析请求地址中的 get 参数
   var urlObj = url.parse(req.url, true)
   req.query = urlObj.query
  query(req, res)

   解析请求地址中的 post 参数
   req.body = {
     foo: 'bar'
   }
  postBody(req, res)

   解析 Cookie
   req.cookies = {
     isLogin: true
   }
  cookie(req, res)

   配置 Session
   req.session = {}
  session(req, res)

   配置模板引擎
  res.render = function () {
    
  }

  if (req.url === 'xxx') {
     处理
     query、body、cookies、session、render API 成员
  } else if (url === 'xx') {
     处理
  }


   上面的过程都是了为了在后面做具体业务操作处理的时候更方便
})

server.listen(3000, function () {
  console.log('3000. running...')
})

```

##### 中间件中next的使用

 中间件：处理请求的，本质就是个函数

 在 Express 中，对中间件有几种分类

 当请求进来，会从第一个中间件开始进行匹配

​    如果匹配，则进来

​       如果请求进入中间件之后，没有调用 next 则代码会停在当前中间件

​       如果调用了 next 则继续向后找到第一个匹配的中间件

​    如果不匹配，则继续判断匹配下一个中间件

​    

 不关心请求路径和请求方法的中间件

 也就是说任何请求都会进入这个中间件

 中间件本身是一个方法，该方法接收三个参数：

​    Request 请求对象

​    Response 响应对象

​    next     下一个中间件

 当一个请求进入一个中间件之后，如果不调用 next 则会停留在当前中间件

 所以 next 是一个方法，用来调用下一个中间件的

 调用 next 方法也是要匹配的（不是调用紧挨着的那个）

##### next传参

​      return res.status(500).send('Server Error')

​       当调用 next 的时候，如果传递了参数，则直接往后找到带有 四个参数的应用程序级别中间件

​       当发生错误的时候，我们可以调用 next 传递错误对象

​       然后就会被全局错误处理中间件匹配到并处理之

```javascript
var express = require('express')
var fs = require('fs')

var app = express()

 app.get('/abc', function (req, res, next) {
   console.log('abc')
    req.foo = 'bar'
   req.body = {}
   next()
 })

 app.get('/abc', function (req, res, next) {
   console.log(req.body)
   console.log('abc 2')
 })

app.get('/', function (req, res, next) {
  fs.readFile('.d/sa./d.sa/.dsa', function (err, data) {
    if (err) {
       return res.status(500).send('Server Error')
       当调用 next 的时候，如果传递了参数，则直接往后找到带有 四个参数的应用程序级别中间件
       当发生错误的时候，我们可以调用 next 传递错误对象
       然后就会被全局错误处理中间件匹配到并处理之
      next(err)
    }
  })
})

app.get('/', function (req, res, next) {
  console.log('/ 2')
})



app.get('/a', function (req, res, next) {
  fs.readFile('./abc', function (err, data) {
    if (err) {
       return res.status(500).send('Server Error') 
      next(err)
    }
  })
})

app.use(function (req, res, next) {
  res.send('404')
})

 配置错误处理中间件
app.use(function (err, req, res, next) {
  res.status(500).send(err.message)
})

app.listen(3000, function () {
  console.log('app is running at port 3000.')
})


```



### promise解决异步问题
#### promise的使用

![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\04\code\promiseAPI代码图示.png)

![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\04\code\promise链式调用.png)

![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\04\code\promise容器概念.png)

```
var fs = require('fs')

var p1 = new Promise(function (resolve, reject) {
  fs.readFile('./data/a.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

var p2 = new Promise(function (resolve, reject) {
  fs.readFile('./data/b.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

var p3 = new Promise(function (resolve, reject) {
  fs.readFile('./data/c.txt', 'utf8', function (err, data) {
    if (err) {
      reject(err)
    } else {
      resolve(data)
    }
  })
})

p1
  .then(function (data) {
    console.log(data)
     当 p1 读取成功的时候
     当前函数中 return 的结果就可以在后面的 then 中 function 接收到
     当你 return 123 后面就接收到 123
          return 'hello' 后面就接收到 'hello'
          没有 return 后面收到的就是 undefined
     上面那些 return 的数据没什么卵用
     真正有用的是：我们可以 return 一个 Promise 对象
     当 return 一个 Promise 对象的时候，后续的 then 中的 方法的第一个参数会作为 p2 的 resolve
     
    return p2
  }, function (err) {
    console.log('读取文件失败了', err)
  })
  .then(function (data) {
    console.log(data)
    return p3
  })
  .then(function (data) {
    console.log(data)
    console.log('end')
  })

```



```
var fs = require('fs')

function pReadFile(filePath) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filePath, 'utf8', function (err, data) {
      if (err) {
        reject(err)
      } else {
        resolve(data)
      }
    })
  })
}

pReadFile('./data/a.txt')
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/b.txt')
  })
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/c.txt')
  })
  .then(function (data) {
    console.log(data)
  })

```



#### 异步封装API

![](D:\后台\14--Nodejs教程精讲（7天）\nodejs资料（7天）\04\code\回调函数.png)

在crud中对文件进行读取，数据处理api的封装，后导给router.js进行调用

## mongodb的使用

- MongoDB 数据库
  - MongoDB 的数据存储结构
    - 数据库
    - 集合（表）
    - 文档（表记录）
- MongoDB 官方有一个 mongodb 的包可以用来操作 MongoDB 数据库
  - 这个确实和强大，但是比较原始，麻烦，所以咱们不使用它
- mongoose
  - 真正在公司进行开发，使用的是 mongoose 这个第三方包
  - 它是基于 MongoDB 官方的 mongodb 包进一步做了封装
  - 可以提高开发效率
  - 让你操作 MongoDB 数据库更方便

### mongodb的使用步骤

 **创建一个模型**

 **就是在设计数据库**

 **MongoDB 是动态的，非常灵活，只需要在代码中设计你的数据库就可以了**

 **mongoose 这个包就可以让你的设计编写过程变的非常的简单**

1. 连接数据库，指定连接的数据库不需要存在，当你插入第一条数据之后就会自动被创建出来

2.  设计文档结构（表结构），字段名称就是表结构中的属性名称，约束的目的是为了保证数据的完整性，不要有脏数据

3.  将文档结构发布为模型

      mongoose.model 方法就是用来将一个架构发布为 model

      第一个参数：传入一个大写名词单数字符串用来表示你的数据库名称

   ​                mongoose 会自动将大写名词的字符串生成 小写复数 的集合名称

   ​                例如这里的 User 最终会变为 users 集合名称

      第二个参数：架构 Schema

     

      返回值：模型构造函数

   4.当我们有了模型构造函数之后，就可以使用这个构造函数对 users 集合中的数据为所欲为了（增删改查）

   ```javascript
   var mongoose = require('mongoose')
   
   var Schema = mongoose.Schema
   mongoose.connect('mongodb:localhost/itcast')
   
   var userSchema = new Schema({
     username: {
       type: String,
       required: true  必须有
     },
     password: {
       type: String,
       required: true
     },
     email: {
       type: String
     }
   })
   
   var User = mongoose.model('User', userSchema)
   
   #region /新增数据
   **********************
   var admin = new User({
     username: 'zs',
     password: '123456',
     email: 'admin@admin.com'
   })
   
   admin.save(function (err, ret) {
     if (err) {
       console.log('保存失败')
     } else {
       console.log('保存成功')
       console.log(ret)
     }
   })
   **********************
   #endregion /新增数据
   **********************
   
   
   
   
   **********************
   #region /查询数据
   **********************
   
   User.find({
     username: 'zs'
   }, function (err, ret) {
     if (err) {
       console.log('查询失败')
     } else {
       console.log(ret)
     }
   })
   
   User.findOne({
     username: 'zs'
   }, function (err, ret) {
     if (err) {
       console.log('查询失败')
     } else {
       console.log(ret)
     }
   })
   **********************
   #endregion /查询数据
   **********************
   
   
   
   **********************
   #region /删除数据
   **********************
   User.remove({
     username: 'zs'
   }, function (err, ret) {
     if (err) {
       console.log('删除失败')
     } else {
       console.log('删除成功')
       console.log(ret)
     }
   })
   **********************
   #endregion /删除数据
   **********************
   
   
   **********************
   #region /更新数据
   **********************
   User.findByIdAndUpdate('5a001b23d219eb00c8581184', {
     password: '123'
   }, function (err, ret) {
     if (err) {
       console.log('更新失败')
     } else {
       console.log('更新成功')
     }
   })
   **********************
   #endregion /更新数据
   **********************
   
   ```

   

```javascript
User.findOne({ username: 'aaa' }, function (user) {
  if (user) {
    console.log('已存在')
  } else {
    new User({
      username: 'aaa',
      password: '123',
      email: 'dsadas'
    }).save(function () {
      
    })
  }
})

User.findOne({
    username: 'aaa'
  })
  .then(function (user) {
    if (user) {
       用户已存在，不能注册
      console.log('用户已存在')
    } else {
       用户不存在，可以注册
      return new User({
        username: 'aaa',
        password: '123',
        email: 'dsadas'
      }).save()
    }
  })
  .then(function (ret) {
  })

User.find({
  username: 'zs'
}, function (err, ret) {
  if (err) {
    console.log('查询失败')
 } else {
    console.log(ret)
  }
})
```

