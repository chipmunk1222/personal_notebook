简介：在where从句中使用，用来过滤条件范围内的记录

语法：
select <columnname1>,<columnname2>
from <tablename>
where <columnname1> 
between 1 and 10000

注：between后的操作符支持多种格式，大多数情况下包括边界，如果是’string%‘，不包括右边界，between操作符支持not between操作