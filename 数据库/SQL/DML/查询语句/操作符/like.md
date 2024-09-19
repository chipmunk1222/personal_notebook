
简介：like操作符使用一些特定字符完成指定操作

| 字符 | 含义 |
| ---- | ---- |
| % | 任意多个字符 |
| _ | 单个字符 |
| \[] | 约束条件下的字符，类似于in |
| \[^] | 反约束条件下的字符，类似于not in |
|  |  |
|  |  |
语法：
select<columnname>
from <tablename1>
where <columnname> 
like [pattern]

注：like指定字段只包括string，date等类型，like操作符支持not like
