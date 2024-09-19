vite搭建：npm create vite@latest my-vue-app -- --template vue

进入vite项目：
- 安装依赖：npm i
- 启动服务器·：npm run dev

vite打包：npm run build

vite特点：
- 支持热替换、热更新（实时响应修改）
- 模块化打包：相对于webpack效率更高
- vite项目导入模块需要指定后缀名

vite对比webpack：
- webpack原理：将所有模块打包，再将打包内容送入服务器
- vite原理：先启动服务器，再直接在服务器上调用模块，渲染页面
- vite解决了开发阶段速度太低的问题，模块越多，项目越复杂，vite优势越大