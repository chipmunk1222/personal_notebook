[[#^a3d3cd]] 普通容器
[[#^cf10c0]] 表格容器
[[#^ddded9]] 图片容器
[[#^a257af]] 警示栏容器
[[#^88c405]] 按钮容器
[[#^4515c0]] 进度条容器
[[#^cf2891]] 分页栏
[[#^6c15b8]] 列表组
[[#^a25674]] 卡片
[[#^a04152]] 标签

- 容器号码由小到大：-sm，-md，-lg，-xl，-xxl
- 封装的特殊颜色：蓝色：-primary，绿色：-success，红色：-danger，浅蓝：-info，黄色：-warning，灰色：active/secondary，白色：light，黑色：dark
- 规则：属性类必须和模板类同时存在

普通容器模板： ^a3d3cd
- .container：响应式固定容器
- .container-fluid：行内容器
容器样式：
- .h1~.h6  .display-1~.display-6：大小
- -pt-1~5：内边距
- -mt-1~5：外边距
- .justify-content-center(end)：调整位置
- .active/disabled：高亮/隐藏
- -bg-（color）：颜色
- -text-（color）：文本颜色
- 网格布局：将一个屏幕宽度分为12份，通过每个网格占的份数决定宽度
- 外层使用.row包括，内层每一个网格使用.col-（大小）决定占比

表格容器： ^cf10c0
- 模板：.table 
- 参数：-striped：白灰间隔，-bordered：带框表格，-hover：悬停变灰，-.（封装颜色）：对应背景
- 表格横向滚轮：.table-respective-(大小)

图片容器： ^ddded9
- 类型：.rounded：圆角，.rounded-circle：椭圆：.img-thumbnail：限定大小为边框
- 位置：.float-start：左浮动，.float-end：右浮动，.mx-auto .d-block：居中
- 适应：.img-fluid：使图片适应宽高

警示栏容器： ^a257af
- 模板：.alert .alert-（color）
- 警示栏链接（内部超链接，使链接样式自动匹配）：.alert-link
- 关闭警示栏（内部按钮，使按钮触发后自动关闭栏目）：外部：.alert-dismissible，内部：class=”btn-close“ data-bs-dismiss="alert"
- 动态关闭界面：.fade .show

按钮容器： ^88c405
- 适用于按钮，超链接，输入
- 模板：.btn .btn-（color）.btn-(size)
- 外轮廓按钮：.btn-outline-(color)
- 全宽按钮：外部：.d-grid（gap-(num)），内部：btn-block
- 按钮激活：.active .disabled
- 等待中按钮：按钮内部（spinner-border spinner-border-sm）
按钮组：
- 模板：.btn-group-(size)
- 纵向排布：.btn-group-vertical
- 下拉按钮组（点击按钮出现下拉选项）：外部：.btn-group ，内部.dropdown-toggle   data-bs-toggle=".dropdown"，按钮内部：.dropdown-menu，条目：.dropdown-item
下拉按钮：
- 外层：.dropdown
- 下拉内容分割线：hr属性，.dropdown-divider
- 下拉内容标题：.dropdown-header
- 侧边显示：.dropdown .dropend/.dropstart
- 侧下方显示：.dropdown-menu .dropdown-menu-end
- 上方显示：.dropup
折叠按钮：
- 模板：data-bs-toggle="collapse" data-bs-target="#demo"，内部：id="demo" .collapse
- 单个显示：内部：data-bs-parent=“#外部容器id”

进度条容器： ^4515c0
- 模板：外层：.progress style="height:(num)"，内层：.progress-bar style="width:(num)"
- 条纹进度条：.progress-bar-striped
- 动态条纹进度条：.progress-bar-striped .progress-bar-animated
- 多段进度条：外层内封装多个progress-bar
旋转进度条：
- 模板：.spinner-border
- 不同颜色的进度条：.spinner-border .text-(color)
- 生长进度条：.spinner-grow .text-(color)

分页栏： ^cf2891
- 建议使用列表属性包括
- 模板：外层：.pagination，内层：.page-item，超链接：.page-link
- 按钮高亮/无效：.acative/.disabled
- 位置：.justfy-content-center(end)
- 特殊分页栏：外层：.breadcrumb，内层：.breadcrumb-item

列表组容器： ^6c15b8
- 模板：外层：.list-group，内层：.list-group-item
- 创建超链接列表组：ul换为div，li换为a，内层添加：.list-group-item-action
- 清除外部框：外层：list-group-flush
- 列表编号：.list-group-numbered
- 横向列表：.list-group-horizontal
- 列表材质：.list-group-item-(color)

卡片容器： ^a25674
- 模板：外层：.card，内层：.card-header，.card-body，.card-footer
- 标题：.card-title
- 内容：.card-text
- 链接：.card-link
- 图片：.card-img-top
- 文字覆盖图片：内层：.card-img-overlay

标签（文字后的信息标签，可写于元素内部）： ^a04152
- 模板：.badge bg-（color）
- 圆角标签 .rounded-pill

导航菜单：
- 模板：外层：.nav，内层：.nav-item，超链接：.nav-link
- 位置：.justify-content-(center/end)
- 纵向导航：.flex-column
- 激活：.nav-link .active/.disabled
- 按钮填充：.nav .nav-pills
- tab栏：.nav-link data-bs-toggle="tab" href="#id" 目标容器：外层：.tab-content，内层：.tab-pane
- 动态显示tab栏：data-bs-toggle="pill"
导航栏：
- 模板：外层：nav-bar，内层列表：navebar-nav，列表项：nav-item，超链接：nav-link
- 超链接内衬图片：超链接：.navbar-brand
- 超链接内折叠按钮：class="navbar-toggler", data-bs-toggle="collapse" and data-bs-target="#thetarget_"

旋转图片（carousel），弹出栏（modal），提示工具（tooltips），提示标签（popover），滚动监控（scrollspy），弹出式侧边栏（offcanvas）

各种实体工具（utilities）
黑色模式（dark mode）
弹性窗（flex）

表单（forms）
网格（grid）