约束条件：判断字段对应记录是否符合条件

初始化：
create table <tablename>(
<columnname1> <datetype1>,
<columnname2> <datetype2> check([condition]),
check(<columnname1>[operator][condition])
)

修改：
alter table <tablename>
add constraint <constraintname> check(<columnname1>[operator][conditon])


删除：
alter table <tablename>
drop constraint<constraintname> 