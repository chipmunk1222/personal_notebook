简介：distinct操作符用在select语句后，自动去除重复元素

语法：
select distinct <columnname> from <tablename>
[where]

distinct可嵌套函数使用：
select count(distinct <columnname>) from <tablename> 