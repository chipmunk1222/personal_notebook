简介：触发器实现在执行某一操作的同时自动执行一些设定的操作

语法：
创建函数：
create or replace function <functioname>()
returns trigger as
$$
begin
[statement]
return [new|old]
end
$$
plpgsql

创建触发器：
create trigger <triggername> [befor|after] <eventname>
on <tablename>
[for each row|for each statement]
excute function <function_name>


删除触发器：
drop trigger <triggername>