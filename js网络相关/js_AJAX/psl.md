定义：公共后缀列表工具包
依赖安装：npm install --save psl
导入：let psl = require('psl')

获取当前域名：document.domain

const parse = psl.parse('url')：解析url
parse.tld：顶级域名(com,cn...)
parse.sld：次级域名(com.cn左边部分)
parse.domain：tld+sld
parse.subdomain：域名左边部分

psl.get('url')：获取域名
psl.isValid('url')：检测域名是否合法