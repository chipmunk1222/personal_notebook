`dotEnv`是一个非常常用的`Node`模块，其作用是将环境变量从`.env`文件加载到`process.env`中
其作用是帮助管理和保护一些敏感配置信息，如数据库连接字符串、`API`密钥等

# 使用dotEnv
## 安装依赖
首先，安装`dotenv`模块
```
npm install dotenv
```
## 配置.env文件
在项目根目录中创建一个`.env`文件，并添加环境变量
```js
DB_HOST=localhost
DB_USER=root
DB_PASS=s1mpl3
```
### 加载环境变量
由于`dotenv`会自动将`.env`文件中的配置信息添加到`process.env`中，所以在需要的地方引入`dotenv`的`config`配置项，就可以调用相关信息了
```js
require('dotenv').config();  //commonjs
import 'dotenv/config'

console.log(process.env.DB_HOST); // 输出 'localhost'
console.log(process.env.DB_USER); // 输出 'root'
console.log(process.env.DB_PASS); // 输出 's1mpl3'
```