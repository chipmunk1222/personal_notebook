0、引入CDN或安装依赖
CDN： <script src="https://cdnjs.cloudflare.com/ajax/libs/echarts/5.5.0/echarts.min.js" integrity="sha512-k37wQcV4v2h6jgYf5IUz1MoSKPpDs630XGSmCaCCOXxy2awgAWKHGZWr9nMyGgk3IOxA1NxdkN8r1JHgkUtMoQ==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>

依赖：
npm install echarts --save
import * as echarts from 'echarts'；

1、准备一个具备宽高的容器

2、初始化
- let mychart = echart.init(document.queryselector(DOM容器))
3、添加配置项
- mychart.setOption({option})