简介：all（）必须用在比较操作符后，用来和所有的条件比较

语法：
select <columnname>
from <tablename>
where
<columnname> (operator) all( select <columnname> from <tablename> [where])

注：all（）比较的类型必须一致，括号中必须是一个子查询，all（）也可以跨表比较，返回交集或不同记录