icon图标库：
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" integrity="sha512-DTOQO9RWCH3ppGqcWaEA1BIZOC6xxalwEsw9c2QQeAIftl+Vegovlnee1c9QX4TctnWMn13TZye+giMm8e2LwA==" crossorigin="anonymous" referrerpolicy="no-referrer" />

<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.15.4/css/all.css" integrity="sha384DyZ88mC6Up2uqS4h/KRgHuoeGwBcD4Ng9SiP4dIRy0EXTlnuz47vAwmeGwVChigm" crossorigin="anonymous"/>

<link rel="stylesheet" href="https://lf3-cdn-tos.bytecdntp.com/cdn/expire-1-M/font-awesome/4.7.0/css/font-awesome.min.css">

或者：
css布局大纲（血泪总结）：
- 1、优先确定大盒子的内部元素表示方式，基本为flex
- 2、进一步确定盒子内部排列方式，如行列，溢出操作
- 3、通过修改position属性改变盒子整体位置布局
- 4、设置宽高等，确保万无一失
- 5、内外边距等在盒子整体完成部署后更容易修改
注：
- flex弹性盒影响范围只限于一级关系，对于vue2组件，由于内部需要再写div，故需注意
- 当flex-direction为列时，align-items和justify-content相应调换

特性：
- css布局方向设置默认顺序：上右下左
- 标准盒模型的padding和border属性会撑起整个盒子，使其宽高不同于设置的大小
- 可使用bix-size使盒模型宽高固定
- * { -webkit-box-sizing: border-box;
	-moz-box-sizing: border-box; 
	box-sizing: border-box; 
	}

display：
- 表示元素显示方式
- block：元素块状排列
- inline：元素在行内依序排列
- none：元素隐藏
- inline-block：使用网格铺满页面
- flex：弹性盒模型

弹性盒对齐方式：
- align-items：按照非排列方向的布局页对齐
- justify-content：按照盒子排列方向上的内部对齐方式
- flex： \[grow] \[shrink] \[basis]：依次表示指定弹性盒的增长、缩小比例（0为固定长度）和默认大小，默认 0 1 auto

width、height：
- 设置元素占据空间大小
- 左右外边距可用auto居中
- 用max-height可以更好地处理小窗口的情况
- 百分比宽度，使元素宽度始终占据容器的百分比

position：
- 设置元素显示位置
- stactic：默认属性，不会被特殊定位
- relative：相对于目前为止，可使用上右下左属性定位（相对于最近元素的位置）
- fixed：固定位置，其余部分相当于relative，
- absolute：相对于最近的祖先元素的位置，可使用上右下左定位

float：
- 实现相对于已有元素（文字）的环绕
- 可使用上左下右定位
clear：
- 清除元素的float环绕
overflow：
- 解决环绕元素边框超出原元素的问题
- hidden：不可见，visible：可见

transition：
- 模板：transition：property Duration timing-function
- transition-property：添加动画的属性
- transition-Duration：动画持续时间
- transition-timing-function：动画加速控制（ease-in：加速，ease-out：减速，ease-in-out：双端变速）

transform：
- 模板：transform：方法（像素）
- transform利用矩阵坐标实现盒子相对于当前位置的转换







