Jquery是一个基本的javascript库，封装了DOM，html/css，AJAX等方法使javascript的操作更简洁
Jquery CDN调用：<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>

Jquery语法：
- 模板：$(selector).action()
- Jquery选择器：选择方法等同于CSS选择器
- 单事件触发：$(selector).events(){action()}
- 多事件触发：$(selector).on({events1(){action};{events2{action}}})
	
Jquery事件：
- Jquery事件引用头：$(document).ready(function(){})：确认事件加载完毕后执行Jquery语句
- hide（speed，callback）：隐藏（事件，触发事件）
- show（speed，callback）：显示
- toggle（speed，callback）：触发（显示或隐藏）
- fadeIn（speed，callback）：渐进消失
- fadeout（speed，callback）：渐进出现
- fadeToggle（speed，callback）：渐进触发
- fadeTo（speed，opacity，callback）：渐进变为固定透明度
- slidedown(speed,callback)：下拉幻灯片
- slideup（speed，callback）：上拉幻灯片
- slidetoggle（speen，callback）：触发菜单
- animate（{style：value，style：value}，speed，callback）：动画
- 注：Jquery动画支持串行执行
- stop(stopall,gotoend)：停止动画，stopall：true表示停止所有待执行动画，gotoend表示是非执行完当前动画
- 链式动画：通过将事件链式添加从而实现事件的链式触发

Jqueryhtml：
- text（）：返回文字内容
- html（）：返回html标签
- val（）：返回value值，如input栏中
- attr（“属性名”）：返回标签属性
- 注：在括号中添加字符串可以修改对应标签值
- append（）：元素后添加
- prepend（）：元素前添加
- remove（）：移除标签元素
- empty（）：清空子元素
- addclass（），removeclass（），toggleclass（）：添加移除类
- css("属性名"（”属性值“）)：返回对应属性值（修改属性值）
- width()：宽度，innerwidth（）：宽度加内边距，outerwidth（）：宽度加内边距加边框






