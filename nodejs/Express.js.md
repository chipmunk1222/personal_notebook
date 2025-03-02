`express.js`是一款基于`Node.js`的`Web`平台框架，用于简化和加快`Node`服务器的开发，用于简化`http`请求的处理。
`express.js`用一种结构化的方式定义不同`URL`路径和处理函数，可以更有效地组织和管理路由
`express.js`是一个轻量且灵活的框架，其核心功能极少，可以通过中间件对其进行扩展

`Express.js`官方网址：[Express (expressjs.com.cn)](https://www.expressjs.com.cn/)
# 使用Express
## 导入依赖
`express`是基于`node`的服务器构建框架，故首先使用`npm init`创建一个`node`项目
```
npm init
```
然后通过`npm`安装`express`
```
npm install express --save
```
## 服务器创建
1. 通过`const express = require('express')`引入`express`模块
2. 创建一个`express`实例`app`，定义服务器端口号`3000`
3. 定义一个处理`GET`请求的路由，`req`和`res`参数等同于`node`中的参数
4. 通过`app.listen(port,func)`启动服务器并监听对应端口
```javascript
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```
>`express`官方还提供了一些快速构建工具如`express-generator`来快速生成`express`应用·，不过这只是众多方法中的一种，可以不使用它

## Express路由
### 基本路由
路由定义了服务器的一些信息处理模式，处理了对应`URL`下的`http`请求
**路由基本格式：**
```js
app.Method(Path,Handler)
```
其中`app`为创建的`express`实例，`Method`包括`GET`、`POST`、`PUT`和`DELETE`，`Handler`中包括`(req,res)`两个默认参数，`req`表示前端传入数据的参数，`res`表示服务器将要返回的数据
**样例：**
**前端请求：**
```js
const response = await fetch('/welcome', {
	method: 'POST', 
	headers: { 
		'Content-Type': 'application/json' 
	}, 
	body: JSON.stringify({ username })
});
```
**后端代码：**
```node
const express = require('express');
const app = express();
const port = 3000;

app.use(express.json());

app.post('/welcome', (req, res) => {
  const { username } = req.body;
  res.json({ message: `Welcome, ${username}!` });
});

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```
### Router模块化路由
在`express`中通过`Router()`创建路由模块，从而更好地组织和管理路由
**模块创建**
首先，在`routes`文件中创建一个模块，命名为`user.js`
```js
const express = require('express');
const router = express.Router();

// 应用级中间件：记录请求时间
router.use((req, res, next) => {
  console.log('时间:', Date.now());
  next();
});

// 路由级中间件：仅应用于 /users/:id 路由
router.use('/users/:id', (req, res, next) => {
  console.log('用户ID:', req.params.id);
  next();
});

// 路由处理
router.get('/', (req, res) => {
  res.send('用户主页');
});

router.get('/:id', (req, res) => {
  res.send(`用户ID: ${req.params.id}`);
});

module.exports = router;
```
上述案例中由三个部分组成，分别是全局中间件、路由中间件以及处理函数，中间件同样使用`router.use()`注册
 1. **全局中间件：** 上述案例中第一个部分为全局中间件，在当前路由模块调用时就会触发
 2. **路由中间件：** 仅在进入对应路由时触发
 3. **处理函数：** 定义指定`URL`路径下的处理函数
最后导出模块
>中间件执行完后需要使用`next()`来控制中间件的流动，`next`为第三个默认参数
>如果对某个路由有多个处理函数，可以直接向后写，通过`next()`交接控制权


**模块调用**
在`app.js`中引入并使用这个路由模块
```js
const usersRouter = require('./routes/users');

// 使用路由器
app.use('/users', usersRouter);
```
## Express静态资源托管
`express`静态资源托管提供了对诸如图像、`CSS`、`Javascript`等静态资源的托管，使用`express.static`中间件函数来完成
```node
express.static(root,[options])
```
通过`app.use()`注册中间件
```javascript
app.use(express.static('public'))
```
这样就可以访问`public`目录中的所有静态资源文件了
```plain-text
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
```
>如果要使用多个静态资源目录，请多次调用 `express.static` 中间件函数

同时`express`还支持创建虚拟`url`来存放静态资源（添加前缀）
```javascript
app.use('/static', express.static('public'))
```
结果是这样的：
```plain-text
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html
```
最后，可以使用`__dirname`来使用项目绝对路径定义资源路径，从而增加安全性
```javascript
const path = require('path')
app.use('/static', express.static(path.join(__dirname, 'public')))
```
先引入`node`中的`path`模块，然后`join`项目绝对路径和`public`文件夹从而导入路径

## Express中间件
### express.json()
使用`Express.use(json)`后，传入的请求（`req`）中信息会被自动解析为`json`格式，这样，就可以直接使用`req.body`访问传入的数据了
```js
app.use(express.json())
```
### cookieParser()
基础的`Express`中并不提供在`request`参数中解析`cookies`的能力，然而在应用中验证用户权限又是非常常见的一个功能，因此需要使用`cookieParser`中间件，这样就能直接使用`req`里的`cookies`了
安装依赖：
```
npm install cookie-parser
```
在`index.js`中引入：
```js
import cookieParser from 'cookie-parser'
app.use(cookieParser())
```
### bodyParser
在`node`后端中对于上传的文件有一定的要求，例如默认图片资源等就不能超过`100KB`，使用`bodyParser`可以修改上传资源大小上限
安装依赖：
```
npm install body-parser
```
在`index.js`中引入：
```js
app.use(bodyParser.json({ limit: '10mb' }));
app.use(bodyParser.urlencoded({ limit: '10mb', extended: true }));
```
### cors
用来解决浏览器跨域问题的中间件
安装依赖：
```
npm install cors
```
在`index.js`中调用：
```js
app.use(
  cors({
    origin: process.env.CLIENT_ORIGIN || 'http://localhost:5137',
    credentials: true,
  })
);
```
## 常见的Express-Api
**Response：**
- `res.send()：`返回响应信息，接受`String`、`Json`、`html`等格式，会自动解析并设置`Content-Type`响应头
- `res.json()：`自动转化并返回`Json`格式信息，与`.send()`方法类似
- `res.set()：`设置响应头的相关信息
- `res.status():`设置响应行的状态码
- `res.end():`立即结束响应并不返回数据
- `res.cookie(name,value[,options])`：设置`http-cookie`

**Request：**
- `req.cookies：`解析请求头中的`cookie`（需要安装`cookie-parser`中间件）
- `req.xxx：`在`request`参数中可以设置自定义参数，这一般在路由中间件函数中操作，方便后续使用（例如，手动添加`req.user`以存储用户信息）