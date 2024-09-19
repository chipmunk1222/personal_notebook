JSON（javascript object nonation）：javascript对象标记语言
- json是一种纯文字格式，主要用于数据存储和传输
- json特性：所有字面量都要用引号包裹

JSON VS XML：json格式比XML更简洁，更容易被解释，更容易被获取

JSON类型：string，decimal，boolean，null，array，object

JSON方法：
- JSON.parse()：将JSON格式转换成javascript
- JSON对象转换为javascript对象，数组转化为数组
- 自定义转化：JSON.parse（function(key,value)）{表达式 return }
- JSON.stringify()：将javascript对象转化为JSON格式的字符串
- localStorage.setitem("objname",obj)：将JSON格式存储到本地，对象名为objname
- localStorage.getitem("objname")：在本地读取JSON数据

JSON文件读取：
- foreach读取转化为javascript后的对象时，x只对应对象的键，myobj.x读取值