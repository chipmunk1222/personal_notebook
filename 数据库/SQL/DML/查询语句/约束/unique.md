约束条件：禁止某一字段重复出现相同记录

初始化：
create table <tablename>(
<columnname1> <datetype1> unique,
<columnname2> <datetype2> ，
unique(columnname1)
)

修改：
alter table <tablename>
add constraint <constraintname>
unique(<columnname1>,<columnname2>)

删除：
alter table <tablename>
drop constraint<constraintname>