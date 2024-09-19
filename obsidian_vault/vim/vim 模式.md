# 命令行操作
:q 退出
:w 保存
:q! 退出（不保存）
:qw 保存并退出
:e {filement} 切换文件
:ls 显示进程
:help 获得帮助
ctrl+D 获得命令列表
tab 自动补全命令
# 移动操作
hjkl 左下上右
w 下一个单词头
e 单词尾
b 上一个单词头
$ 行末
0 行头
^ 行头字符
number {motion} 
3w 下三个单词头
gg 页头
G 页末
numberG 对应行
# 插入操作
a 光标前插入
i 光标后插入
A 文末插入
o 往后插入一行
O 往前插入一行
# 撤销操作
u 撤销最后一次操作
U 恢复某一行到起始状态
ctrl+R 撤销最后一次撤销
# 删除操作
x 删除单个字符
d {motion}
dw 删除一个字符
de 从光标处删除一个单词
dd 从光标处删除一行
number {motion}
3dd 删除3行
# 修改操作
r 修改单个字符
R 进入修改模式
ce 修改光标后单词,保留空格（删除光标后单词，进入插入模式）
cw 修改光标后单词,不保留空格（删除光标后单词，进入插入模式）
c$ 修改光标后一行
# 查询操作
/ {word} 往后查找最近的单词
? {word} 往前查找最近的单词
n 重复往后查找单词
N 重复往前查找单词
ctrl+o 回到上次查找位置
ctrl+I 回到最新查找位置
ctrl+% 查找(), \[ ] ,{}匹配
# 替换操作
:s/old/new 将本行最近一个old替换成new
:s/old/new/g 将本行全部old替换成new
:s/old/new/gc 全部替换同时询问
:#,#s/old/new/g （\#代表行号）将对应行号之间old替换成new
:%s/old/new/g 将全文old替换成new


# 外文本操作
:!+command vim 模式下读取外部命令
:w text 将文件保存到text文件中
:!+command w text 将命令结果保存到text文件中
v选择文本 :w text 将选择文本保存到text文件中
:r filement 合并文本并插入
:r !ls 插入ls返回结果

# 复制粘贴操作
v motion 选中文本
y 复制选中的文本
p 粘贴文本
yw 复制一个单词
yy 复制一行
3yy 复制三行


# 设置操作
:set number 显示行数
:set ic (ignore case) 忽略大小写
:set noic 不忽略大小写
\\c 单词忽略大小写搜索
:set hls 高亮搜索
:set nohls 取消高亮
:set is 显示部分匹配
no+option 取消设置

