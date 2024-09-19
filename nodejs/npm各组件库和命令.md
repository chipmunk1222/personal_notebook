nodeJS和CDN的区别：CDN通过网络资源发布从而增加访问速度，nodeJS通过将资源包添加入node_modules中的依赖。但对于新项目需要重新引入包（具体npm install讲node_modules中的包引入到依赖中）

创建vue项目：vue create {filename} 需要超管权限
			npm create/init vue@latest  使用vite创建
运行vue测试项目：npm run serve
运行vue生产项目：npm build serve
打包vue项目：npm run build
注：
- vue创建项目时必须要超管权限
- vue项目中必须确保缩进正确

换源安装依赖：
- 删除已有的源：npm(yarn) config delete registry
    - npm(yarn) config delete disturl
- 注：不知道npm发什么病，有时候换完源后要在删掉已有的源才能替换
- 换源：yarn config set registry https://registry.npmmirror.com --global
	- yarn config set disturl https://npmmirror.com/dist --global
- 清缓存：yarn cache clean
- 装依赖：yarn install
- 运行：yarn run dev

快速原型开发：
- 定义：对单个vue组件进行快速测试
- 安装命令：npm install -g @vue/cli-service-global
- 测试语法：vue serve ./src/App

加入element-ui插件：npm i element-ui --save
- --save：将对应包装进package.json依赖里

项目打包发布：
- 本地发布：
	- 1、npm run build打包项目
	- 2、使用npm install express-generator -g安装express
	- 3、express expressDemo （expressDemo是项目名）创建一个项目
	- 4、cd expressDemo进入项目
	- 5、npm install安装依赖
	- 6、将dist内部文件复制到新文件的public中
	- 7、npm start运行项目
	- 8、输入 http://localhost:3000浏览项目