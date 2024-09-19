nodeJS和CDN的区别：CDN通过网络资源发布从而增加访问速度，nodeJS通过将资源包添加入node_modules中的依赖。但对于新项目需要重新引入包（具体npm install讲node_modules中的包引入到依赖中）

创建vue项目：vue create {filename} 需要超管权限
	$ npm create vue@latest 直接创建
运行vue测试项目：npm run serve
运行vue生产项目：npm build serve
注：
- vue创建项目时必须要超管权限
- vue项目中必须确保缩进正确

加入element-ui插件：npm i element-ui --save
- --save：将对应包装进package.json依赖里

CDN：
Vue：
-  开发版本包<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
- 生产版本包<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16"></script>

Element-ui组件库引入：
<!-- 引入样式 -->
- <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css"> 
<!-- 引入组件库 -->
- <script src="https://unpkg.com/element-ui/lib/index.js"></script>

Jquery：
- <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>