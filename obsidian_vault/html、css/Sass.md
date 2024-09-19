定义：一款css预处理器，提供了变量、函数、嵌套等一系列特性，后缀为.scss
Scss为第三代Sass，完全兼容原生Sass
vue项目中导入Scss：npm install -D(开发依赖) sass-loader node-sass  *style* lang=“sass”

Sass变量定义语法：$_variablename_: _value_;

Sass嵌套：利用大括号标识，支持类和属性的嵌套

Sass导入：@import ‘filename’
注：不加后缀，只能导入sass文件，导入后默认放文件开头

Sass混合：@mixin name{}，使用：@include name，相当于结构体
混合函数：@mixin name（$var）{}，可以在括号中写入参数达到函数效果

插值表达式：#{$var}
条件语句：@if name {} @else {}
for语句：@for $var from 1 to(trough) 100{}
each @each $var in *list*{}
while语句 @while $var>1{}
函数：@function name（$var）{@return }

sass继承：@extend *类名*