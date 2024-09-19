*变量引用/创建

$+变量名（所有非常量）可使用{ }操作符
MY_NAME = "my name"
echo "it is my $MY_NAME"

shell获取字符串长度
str = “123545”
echo "${#str}

环境变量 export  variable
只读变量 readonly variable

变量引用 echo “${str}”

变量增删改
	赋值  n=1
			 v1=${n}
	修改 c=1
			c=2
	删除		unset c
	