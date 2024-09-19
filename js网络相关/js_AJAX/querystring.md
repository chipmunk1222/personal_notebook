依赖安装：npm i querystring
导入：import qs from ‘querystring’

定义：用以处理地址栏数据的第三方库，通常与mockjs绑定使用

地址栏格式化：
querystring.parse(str\[, sep\[, eq\[, options]]])：将url地址解析为json格式
- 参数：sep：连接符，默认为&；eq：判断符，默认为=
- 样例：'foo=bar&abc=xyz&abc=123' => {foo:bar,abc:\[xyz,123]}
querystring.stringify(obj\[, sep\[, eq\[, options]]])：将json格式数据转化为url字符串类型