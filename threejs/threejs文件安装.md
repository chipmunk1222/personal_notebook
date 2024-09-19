结构标准：html文件，javascript文件，public文件（可选）
- main.js:import * as THREE from 'three';

项目安装：
1、使用npm进行本地安装
npm install --save three
npm install --save-dev vite
通过vite构建：
npx vite
2、使用CDN的方式导入
<script type="importmap"> { "imports": { "three": "https://cdn.jsdelivr.net/npm/three@<v0.149.0>/build/three.module.js", "three/addons/": "https://cdn.jsdelivr.net/npm/three@<v0.149.0>/examples/jsm/" } } </script>
运行本地服务器：
npx serve
