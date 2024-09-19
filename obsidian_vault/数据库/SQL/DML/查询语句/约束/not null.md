约束条件：禁止某一字段出现空记录

初始化：
create table <tablename>(
<columnname1> <datetype1> not null,
<columnname2> <datetype2> not null
)

修改：
alter table <tablename>
alter column <columnname> set not null

删除：
alter table <tablename>
alter column <columnname> drop not null
