>更多细节，参考`nodemon`官方网址 [nodemon - npm (npmjs.com)](https://www.npmjs.com/package/nodemon)

# 概述
`nodemon`可以在`node`服务器内容更改时自动重启服务器，从而避免反复的手动中断并重启的繁琐过程，节省了手动重启的流程，从而优化开发过程。从前端的视角来看有点像`vite`的热更新，只不过`nodemon`是在服务器层面。~~所以为什么node官方不直接引入这个东西，虽然全局安装后也差不多~~
安装`nodemon`后，`nodemon`相当于在`node`中套了一层外壳，无需任何改动，`node`创建的服务器就会自动重启，当然，也可以添加一些相关的配置
# 在项目中使用nodemon
## 安装
**全局安装：**
```
npm install -g nodemon
```
全局安装后能在计算机任何地方使用该依赖，比如随手打开的`cli`命令行中
**本地安装：**
```
npm install --save-dev nodemon
```
本地安装后只能在项目路径下使用该依赖，由于`nodemon`只在开发环境中使用，所以用`--save-dev`只将其引入到开发环境即可，本地安装的好处是可以在`package.json`中直接修改配置文件

## nodemon配置
### 启动nodemon
**全局启动：**
全局安装`nodemon`后可在命令行中全局启动
```
nodemon [your node app]
```
也可以指定`host`和端口号
```
nodemon ./server.js localhost 8080
```
**本地配置启动：**
在`pakeage.json`中添加如下命令
```json
{
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  }
}
```
然后运行：
```
npm run dev
```
### nodemon配置
`nodemon`支持局部和全局配置文件，通常被命名为`nodemon.json`在命令行中使用 -- config file 来指定配置文件
配置优先级如下：
- command line arguments
- local config
- global config

配置文件接收`json`格式的键值对
```json
{
  "verbose": true,
  "ignore": ["*.test.js", "**/fixtures/**"],
  "execMap": {
    "rb": "ruby",
    "pde": "processing --sketch={{pwd}} --run"
  }
}
```
更多配置项见[nodemon/doc/sample-nodemon.md at master](https://github.com/remy/nodemon/blob/master/doc/sample-nodemon.md)

> 如果在本地不想用`nodemon.json`配置，可以将配置文件写在`package.json`中，但如果本地有`nodemon.json`文件，那`package.json`中的配置就会被忽略
> 本地`package.json`配置项被包含在`nodemonConfig`字段中

### nodemon配置项一览
`nodemon`完整配置项：
```json
{
  "watch": ["src", "config"],
  "ignore": ["node_modules", "test"],
  "exec": "node --inspect app.js",
  "ext": "js,json",
  "env": {
    "NODE_ENV": "development"
  },
  "delay": "2500",
  "restartable": "rs",
  "verbose": true,
}
```
**配置项详解**：
- `watch:`指定要监视的目录(如果不配置则默认监视根目录)
- `ignore:`指定要忽略的目录
- `exec：`配置执行命令，用于在启动项目前调用`node --inspect app.js`表示启动`node`调试模式，`app.js`为服务器启动文件（可以使用`execMap`来设置不同编程语言的执行方式）
- `ext:`指定要监视的文件类型（扩展名）
- `env:`设置环境变量
- `delay:`设置文件变化到重新启动的延时~~（防抖？）~~
- `restartable:`设置重启命令，输入这个命令可以手动重启
- `verbose:`启动详细的日志输出模式

**在命令行中配置**
可以使用命令行对`nodemon`进行配置
使用`nodemon -h`查看帮助
![[Pasted image 20250111151304.png]]
参数配置：
```
nodemon -w src -i node_modules -e js,json -d 2.5 -x "node --inspect" app.js
```
- `-w或-watch:`指定要监视的目录
- `-i或-ignore：`指定要忽略的目录
- `-x或-exec：`表示执行的文件
- `-e或-ext：`表示监视的文件后缀
- `-d或-delay：`设置重启时间

## 模块化nodemon
除了通过配置文件或者命令行，nodemon还支持模块化使用，从而更灵活地控制`Nodemon`的行为以及响应
首先创建一个入口文件夹`nodemon-setup.js`
然后配置`package,json`
```json
{
  "name": "my-node-project",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "start": "node app.js",
    "dev": "node nodemon-setup.js"
  },
  "devDependencies": {
    "nodemon": "^2.0.7"
  }
}

```
在`nodemon-setup.js`添加配置项
```js
var nodemon = require('nodemon');

nodemon({
  script: 'app.js',
  ext: 'js json'
});

nodemon.on('start', function () {
  console.log('App has started');
}).on('quit', function () {
  console.log('App has quit');
  process.exit();
}).on('restart', function (files) {
  console.log('App restarted due to: ', files);
});
```
通过`npm run dev`就可以模块化使用`nodemon`

