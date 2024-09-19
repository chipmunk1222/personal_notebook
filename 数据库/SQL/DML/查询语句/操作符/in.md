简介：用来过滤指定范围内的记录

语法：
select <colunmnname>
from <tablename>
where <columnname> 
in (<value1>,<value2>,<value3>)

跨表指定：
select<columnname1>
from <tablename1>
where <columnname1>
in(select  <columnname2> from <tablename2> where [condition])

注：in操作符支持not in操作