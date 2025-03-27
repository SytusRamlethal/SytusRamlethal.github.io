---
title: Node.js
published: 2025-03-28
description: ''
image: ''
tags: [Node.js]
category: '前端'
draft: false 
lang: 'zh-CN'
---
# Fs 文件系统模块

Fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。

* fs.readFile()，用来读取指定文件中的内容；

* fs.writeFile()，用来向指定的文件中写入内容。

```javascript
// 原生 JS 导入 fs 模块
const fs = require('fs')
```

## fs.readFile()的语法格式

本方法可以读取指定文件中的内容：

```javascript
fs.readFile('./table.txt', options, callback)
```

* 参数1：必选参数，字符串格式，表示文件的路径；

* 参数2：可选参数，表示以什么编码格式来读取文件；

* 参数3：必选参数，文件读取完成后，通过回调函数拿到读取的结果。

```javascript
const fs = require('fs')
const { readFile } = fs

readFile('./test.txt', 'utf8', (err, data) => {
    console.log(err);
    console.log('=======');
    console.log(data);
})
```

## fs.writeFile()的语法格式

本方法可以向指定文件写入内容：

```javascript
fs.writeFile('./test.txt', data, options, callBack)
```

1. 必选参数，文件路径；

2. 必选参数，表示写入的内容；

3. 可选参数，表示以什么格式写入；

4. 必选参数，执行回调函数。

```javascript
const fs = require('fs')
fs.writeFile(('./test.txt'), "Hello World", 'utf8', (err) => {
    console.log(err)
})
```

# http模块

## 创建web服务器的基本步骤

1. 导入 http 模块；

2. 创建 web 服务器实例；

3. 为服务器绑定 request 事件，监听客户端的请求；

4. 启动服务器。

### 导入http模块

```javascript
const http = require('http')
```

### 创建web服务器实例

调用 http.createServer() 的方法，则可快速创建一个 web 服务器实例：

```javascript
const server = http.createServer()
```

### 为服务器实例绑定request事件

绑定 request 事件，则可监听客户端发送过来的网络请求。

只要服务器收到了客户端的请求，就会调用通过 server.on() 为服务器绑定的 request 事件处理函数。

Req 中存有客户端相关的数据或属性。

Res 中存有服务器相关的数据或属性。

```javascript
server.on('request', (req, res) => {
    // 只要有客户端请去访问我们自己的服务器，就会触发 request 事件，从而调用这个事件处理函数
    console.log('Someone vist our web server.')
})
```

### 启动服务器

调用服务器实例的 .listen() 方法，即可启动当前的 web 服务器实例：

```javascript
server.listen(80, () => {
    console.log('This server is running')
})
```

### 完整代码

```javascript
const http = require('http')

const server = http.createServer()

server.on('request', (req, res) => {
    console.log('Someone vist our web server');
})

server.listen('80', () => {
    console.log('running');
})
```

# 模块化

模块化是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元。

简易理解，就是遵守固定的规则，把一个大文件拆成独立并相互依赖的多个小模块。

## Node.js 中模块的分类

1. 内置模块：由 Node.js 官方提供，例如 fs、path、http 等；

2. 自定义模块：用户创建的每个 JS 文件，都是自定义模块；

3. 第三方模块：由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载.

## 加载模块

使用 require() 方法，可以加载需要的模块：

```javascript
const fs = require('fs')

const custom = require('./custom.js')
```

## 模块作用域

在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制。叫做模块作用域。

## 向外共享模块作用域中的成员

### module对象

在每个 JS 自定义模块中都有一个 module 对象，它里面存储了和当前模块有关的信息。

#### module.exports

在自定义模块中，可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用。

外界用 require() 方式导入自定义模块时，得到的就是 module.exports 所指向的对象。

```javascript
module.exports = {
    username: 'zs',
    say: () => {
        console.log('Hello');
    }
}
```

使用 require() 方法导入模块时，导入的结果，永远以 module.exports 指向的对象为准。

Exports 对象和 module.exports 指向同一个对象，但导出结果，永远以 module.exports 为准。

```javascript
console.log(module.exports === exports ) // true

module.exports = {
    user: 'zs'
}
exports = {
    name: 'ls'
}

console.log(module.exports) // { user: 'zs' }
```

## CommonJS 模块化规范

Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖。

1. 每个模块内部，module 变量代表当前模块；

2. Module 变量是一个对象，它的 exports 属性是对外的接口；

3. 加载某个模块，其实时加载该模块的 module.exports 属性。require() 方法用于加载模块。

# Express

Express 是基于 Node.js 平台，快速、开放、极简的 Web 开发框架。

Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的。

它的本质是 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。

## 创建基本的 Web 服务器

```javascript
// 导入 express
const express = require('express')
// 创建 web 服务器
const app = express()
// 调用 app.listen(端口号，启动成功后的回调函数)，启动服务器
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1:80')
})
```

## 监听 GET 和 POST 请求

通过 app.get() 方法，可以监听客户端的 GET 请求；通过 app.post() 方法，可以监听看客户端的 POST 请求：

```javascript
 // 参数1：客户端请求的 URL 地址
 // 参数2：请求对应的处理函数
 //    req：请求对象（包含了与请求相关的属性与方法）
 //    res：响应对象（包含了与响应相关的属性与方法）
 app.get('请求URL', (req, res) => {
     /* 处理函数 */
 })
  app.post('请求URL', (req, res) => {
     /* 处理函数 */
 })
```

## 把内容响应给客户端

通过 res.send() 方法，可以把处理好的内容，发送给客户端：

```javascript
 app.get('/user', (req, res) => {
     res.send({ name: 'zs', age: 20 })
 })
  app.post('/user', (req, res) => {
     res.send('请求成功')
 })
```

## 获取 URL 中携带的查询参数

通过 req.query 对象，可访问到客户端通过查询字符串的形式，发送到服务器的参数：

```javascript
app.get('/', (req, res) => {
    // req.query 默认是一个空对象
    // 客户端使用 ?name=zs&age=20 这种查询字符串形式，发送到服务器的参数
    // 可以通过 req.query 对象访问到，例如：
    // req.query.name req.query.age
    console.log(req.query)
    // { "name": "zs", "age": "20" }
})
```

## 获取 URL 中的动态参数

通过 req.params 对象，可以访问 URL 中，通过：匹配到的动态参数：

```javascript
// URL 地址中，可以通过 ：参数名 的形式，匹配动态参数值
app.get('/user/:id', (req, res) => {
    // req.params 默认是一个空对象
    // 里面存放着通过 ：动态匹配到的参数值
    console.log(req.params)
    // user/100
    // 打印结果： { "id": "100" }
})
```

## 托管静态资源

### express.static()

Express 提供了一个非常好用的函数，叫做 express.static() ，通过它，可以非常方便快捷地创建一个静态资源服务器，比如，通过以下代码就可以将 piblic 目录下的图片、CSS 文件、 JS 文件对外开放访问：

```javascript
app.use(express.static('public'))
// http://localhost:3000/images/bg.jpg
// http://localhost:3000/css/style.css
// http://localhost:3000/js/login.js
```

注意：Express 在指定的静态目录中查找文件，并对外提供资源的访问路径。所以，存放静态文件的目录名不会出现在 URL 中。

### 挂载路径前缀

如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下的方式：

```javascript
app.use('/public', express.static('public'))
// http://localhost:3000/public/images/bg.jpg
// http://localhost:3000/public/css/style.css
// http://localhost:3000/public/js/login.js
```

## Express 中的路由

Express 中的路由分3部分组成，分别是请求的类型、请求的 UPL 地址、处理函数：

```javascript
const express = require('express')

const app = express()

app.[请求类型]([URL地址], [处理函数])
```

### 路由的匹配过程

每当一个请求到达服务器后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。

在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的 URL 同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理。

1. 按照定义的先后顺序进行匹配；

2. 请求类型和请求的 URL 同时匹配成功，才会调用对应的处理函数。

### 模块化路由

为了方便对路由进行模块化管理，express 不建议将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块。

1. 创建路由模式对应的 JS 文件；

2. 调用 express.Router() 函数创建路由对象；

3. 向路由对象上挂载具体的路由；

4. 使用 module.exports 向外共享路由对象；

5. 使用 app.use() 函数注册路由模块。

#### 创建路由模块

```javascript
// 该文件是 user.js
const express = require('express')      // 1.导入 express
const router = express.Router()         // 2.创建路由对象

router.get('/user/list', (req, res) => {// 3.挂载获取用户列表路由
    res.send('Get user list.')
}) 

router.post('/user/add', (req, res) => {// 4.挂载添加用户的路由
    res.send('Add new user.')
})

module.exports = router                 // 5.向外导出路由对象
```

#### 注册路由模块

```javascript
// 1.导入路由模块
const userRouter = require('./router/user.js')
// 2.使用 app.use() 注册路由模块
// 注意：app.use() 函数的作用，就是来注册全局中间件
app.use(userRouter)
// eg: http://127.0.0.1:8080/user/list
```

#### 为路由模块添加前缀

类似于托管静态资源时，为静态资源统一挂载访问前缀一样，路由模块添加前缀的方式也非常简单：

```javascript
app.use('/api', userRouter)
// eg: http://127.0.0.1:8080/api/user/list
```

## Express 中间件

中间件（*Middleware*），特指业务流程的中间处理环节。

### 调用流程

当一个请求到达 Express 的服务器后，可以连续调用多个中间件，从而对这次请求进行预处理。

### 中间件的格式

Express 的中间件，本质上就是一个 function 处理函数，Express 中间件的格式如下：

```javascript
const express = require('express')
const app = express()

app.get('/', (req, res, next) => {
    next()                        // 中间件
})
app.listen(300)
```

注意：中间件函数的形参列表中，必须包含 next 参数。而路由处理函数中只包含 req 和 res。

### next 函数的作用

next 函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

### 定义中间件函数

```javascript
// 常量 mw 所指向的，就是一个中间件函数
const mw = (req, res, next) => {
    console.log('一个简单的中间件函数')
    // 当中间件的业务处理完毕后，必须调用 next() 函数
    // 表示把流转关系转交给下一个中间件或路由
    next()
}
```

### 全局生效的中间件

客户端发起的任何请求，到达服务器后，都会触发的中间件，叫做全局生效的中间件。

通过调用 app.use(中间件函数)，则可定义一个全局生效的中间件：

```javascript
const mw = (req, res, next) => {
    console.log('中间件函数')
    next()
}

// 全局生效的中间件
app.use(mw)
```

#### 简化形式

```javascript
app.use((req, res, next) => {
    console.log('中间件函数')
    next()
})
```

#### 定义多个全局中间件

可以使用 app.use() 连续定义多个全局中间件。客户端请求到达服务器之后，会按照定义的先后顺序依次进行调用：

```javascript
app.use((req, res, next) => {
    console.log('1')
    next()
})

app.use((req, res, next) => {
    console.log('2')
    next()
})

app.get('/user', (req, res) => {
    res.send('User page.')
})
```

### 局部生效的中间件

不适用 app.use() 定义的中间件，叫做局部生效的中间件：

```javascript
const mw = (req, res, next) => {
    console.log('中间件函数')
}

// mw 这个中间件只在当前路由中生效，这种用法属于局部生效的中间件
app.get('/', mw, (req, res) => {
    res.send('Home page')
})
```

#### 定义多个局部中间件

可以通过两种等价的方式，使用多个局部中间件：

```javascript
// 以下两种写法完全等价
app.get('/', mw1, mw2, (req, res) => { res.send('Home page') })
app.get('/'m [mw1, mw2], (req, res) => { res.send('Home page') })
```

### 中间件的作用

多个中间件之间，共享同一份 req 和 res。基于这样的特性，我们可以在上游的中间件中，统一为 req 或 res 对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

### 5个注意事项

1. 在路由之间注册中间件；

2. 客户端发送过来的请求，可以调用多个中间件进行处理；

3. 执行完中间件的业务代码之后，不要忘记调用 next() 函数；

4. 为了防止代码逻辑混乱，调用 next() 函数之后不要再写额外的代码；

5. 连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象。

### 中间件的分类

Express 官方把常见的中间件用法，分成了5大类：

1. 应用级别的中间件；

2. 路由级别的中间件；

3. 错误级别的中间件；

4. 错误级别的中间件；

5. 第三方中间件。

#### 应用级别的中间件

听过 app.use() 或 app.get() 或 app.post()，绑定到 app 实例上的中间件，叫做应用进别的中间件：

```javascript
const mw = (req, res, next) => {
    console.log('中间件函数')
}

// mw 这个中间件只在当前路由中生效，这种用法属于局部生效的中间件
app.get('/', mw, (req, res) => {
    res.send('Home page')
})
```

#### 路由级别的中间件

绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不过，应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上：

```javascript
const app = express()
const router = express.Router()

router.use((req, res, next) => {
    console.log('Time:', Date.now())
    next()
})

app.use('/', router)
```

#### 错误级别的中间件

专门用来捕获整个项目中发生异常的错误，从而防止项目异常崩溃的问题。

```javascript
(err, req, res, next) => {}
```

```javascript
app.get('/', (req, res) => {
    throw new Error('服务器内部发生错误')
    res.send('Home page')
})

app.use((err, req, res, next) => {
    console.log('发生了错误：' + err.message)
    res.send('Error!' + err.message)
})
```

注意：错误级别中间件，必须注册在所有路由之后。

#### Express 内置的中间件

自 Express 4.16.0 版本开始，Express 内置了3个常用的中间件，极大提高了 Express 项目的开发效率和体验：

1. express.static 快速托管静态资源的内置中间件，例如：HTML 文件、图片、CSS 样式等（无兼容性）；

2. express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本可用）；

3. express.urlendoded 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本可用）。

```javascript
app.use(express.json())
app.use(express.urlendoded({ extended: false }))
```

#### 第三方的中间件

非 Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。

### 自定义中间件

```javascript
// 导入 express
const express = require('express')
// 创建 web 服务器
const app = express()
// 导入 NodeJS 内置的 querystring 模块
const qs = require('querystring')

app.use((req, res, next) => {
    // 定义变量，用来存储客户端发送过来的请求体数据（如果数据量大，客户端会分批发送，需要手动拼接）
    let str = ''
    req.on('data', (chunk) => {
        // 拼接请求体数据，隐式转换为字符串
        str += chunk
    })
    // 监听 req 对象的 end 事件（请求体发送完毕后自动触发）
    req.on('end', () => {
        // 打印完整的请求体数据
        console.log(str);
        const body = qs.parse(str)
        console.log(body);
        // 把解析出来的请求体对象，挂载为 req.body 属性
        req.body = body
        // 执行后续业务逻辑
        next()
    })
})

app.post('/user', (req, res) => {
    // res.send('ok')
    res.send(req.body)
})

app.listen(8080, () => {
    console.log('express server running at http://127.0.0.1:8080')
})
```

## CORS 跨域资源共享

### 接口的跨域问题

解决接口跨域问题的方案主要有两种：

1. CORS（主流的解决方案，推荐使用）；

2. JSONP（有缺陷的解决方案：只支持 GET 请求）。

### 使用 CORS 中间件解决跨域问题

cors 是 Express 的一个第三方中间件。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。

```javascript
const cors = require('cors') // 导入中间件
app.use(cors)                // 在路由之前配置中间件
```

### 什么是 CORS

CORS（Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，这些 HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源。

浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了 CORS 相关的 HTTP 响应头，就可以解除浏览器端的跨域访问限制。

### CORS 的注意事项

1. CORS 主要在服务器端进行配置。客户端浏览器无须做任何额外的配置，即可请求开启了 CORS 的接口；

2. CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务器端口。

### CORS 响应头部 - Acess-Control-Allow-Origin

响应头部中可以携带一个 Access-Control-Allow-Origin 字段：

```javascript
Access-Control-Allow-Origin: <origin> | *
```

其中，origin 参数的值指定了允许访问该资源的外域 URL。

例如，下面的字段值将只允许来自 https://sytusramlethal.github.io/ 的请求：

```javascript
res.setHeader("Access-Control-Allow-Origin", "https://sytusramlethal.github.io/")
```

如果制定了 Access-Control-Allow-Origin 字段的值为通配符 \* ，表示允许来自任何域的请求：

```javascript
res.setHeader("Access-Control-Allow-Origin", "*")
```

### CORS 响应头部 - Acess-Control-Allow-Header

默认情况下，CORS 仅支持客户端向服务器发送如下的9个请求头：

1. Accept;

2. Accept-Language;

3. Content-Language;

4. DPR;

5. Downlink;

6. Save-Data;

7. Viewport-Width;

8. Width;

9. Content-Type。

如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Acess-Control-Allow-Header 对额外的请求头进行声明，否则这次请求会失败。

```javascript
// 多个请求头之间使用英文的都好进行分割
res.setHeader("Access-Control-Allow-Header", "Content-Type, X-Custom-Header")
```

### CORS 响应头部 - Acess-Control-Allow-Methods

默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。

如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Acess-Control-Allow-Methods 来指明实际请求所允许使用的 HTTP 方法。

```javascript
res.setHeader("Access-Control-Allow-Methods", "POST, GET, DELETE, HEAD")
// 允许所有方法
res.setHeader("Access-Control-Allow-Methods", "*")
```

### CORS 请求的分类

客户端在请求 CORS 接口时，根据请求方式和请求头的不同，可以将 CORS 的请求分为两大类：

1. 简单请求；

2. 预检请求。

#### 简单请求

同时满足：

1. 请求方式：GET、POST、HEAD 三者之一；

2. HTTP 头部信息不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width、Content-Type。

#### 预检请求

符合以下任意一个条件：

1. 请求方式为 GET、POST、HEAD 之外的请求类型；

2. 请求头中包含自定义头部字段；

3. 向服务器发送了 application/json 格式的数据。

在浏览器与服务器正式通信前，浏览器会发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以只一次的 OPTION 请求被称为“预检请求”。服务器成功响应遇见请求后，才会发送真正的请求，并且携带真实数据。

#### 简单请求和预检请求的区别

简单请求的特点：客户端与服务器之间只会发生一次请求。

预检请求的特点：客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求。

### JSONP 接口

概念：浏览器通过 \<script> 标签的 src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做 JSONP。

1. JSONP 不属于真正的 AJAX 请求，因为它没有使用 XMLHttpRequest 对象；

2. JSONP 仅支持 GET 请求，不支持其他请求。

#### 创建 JSONP 接口的注意事项

如果项目中已经配置了 CORS 跨域资源共享，为了防止冲突，必须在配置 CORS 中间件前声明 JSONP 的接口。否则 JSONP 接口会被处理成开启了 CORS 的接口：

```javascript
// 优先创建 JSONP 接口，使其不会被处理成 CORS 接口
app.get('/api/jsonp', (req, res) => {})
// 再配置 CORS 中间件
app.use(cors())
```

#### 实现 JSONP 接口的步骤

1. 获取客户端发送过来的回调函数名字；

2. 得到要通过 JSONP 形式发送给客户端的数据；

3. 根据前两步得到的数据，拼接出一个函数调用的字符串；

4. 把上一步拼接得到的字符串，响应给客户端的 \<script> 标签进行解析执行。

```javascript
app.get('/api/jsonp', (req, res) => {
    //1.获取客户端发送过来的回调函数名字
    const funcName = req.query.callback
    //2.得到要通过 JSONP 形式发送给客户端的数据
    const data = { name: 'zs', age: 20 }
    //3.根据前两步得到的数据，拼接出一个函数调用的字符串
    const scriptStr = `${funcName}(${JSON.stringify(data)})`
    //4.把上一步拼接得到的字符串，响应给客户端的 <script> 标签进行解析执行
    res.send(scriptStr)
})
```