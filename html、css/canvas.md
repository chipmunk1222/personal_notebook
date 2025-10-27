# canvas基本使用
1. 引入`canvas`标签
使用`<canvas>`标签，包含`id`、`width`、`height`等属性
```html
    <canvas id="myCanvas" width="300px" height="400px"></canvas>
```
2. `js`渲染`canvas`上下文
```js
const canvas = document.getElementById("mycanvas")
const ctx = canvas.getContext("2d")
```
3. 绘制图形
```js
// 画一个矩形
ctx.fillStyle = "blue"; // 填充颜色
ctx.fillRect(50, 50, 100, 100); // (x, y, width, height)
```
# canvas基本图形
`<canvas>`只支持两种基本图形的绘制：路径和矩形，其他所有图形都是通过其组合形成
## 矩形绘制
`canvas`提供了三种绘制矩形的方式：
1. 绘制一个填充的矩形
```js
ctx.fillRect(x,y,width,height)
```
2. 绘制一个矩形边框
```js
ctx.strokeRect(x,y,width,height)
```
3. 清除矩形区域
```js
ctx.clearRect(x,y,width,height)
```
## 路径绘制
路径绘制总体步骤：
1. 调用`ctx.beginPath()`新建一条路径
2. 设置起始点`ctx.MoveTo()`
3. 绘制路径`ctx.LineTo()`
4. 完成绘制，使用`ctx.fill()`或`ctx.stroke()`完成绘制
>`fill()`会自动闭合而`stroke()`不会自动闭合

绘制不同形状路径的`api`：
- 直线：`lineTo(x,y)`
- 矩形：`rect(x, y, width, height)`
- 圆弧：`arc(x,y,radius,startAngle,endAngle,anticlockwise)`
>默认`x`轴方向为起始角度
- 二次贝塞尔曲线：`quadraticCurveTo(cp1x, cp1y, x, y)`
- 三次贝塞尔曲线：`bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)`

