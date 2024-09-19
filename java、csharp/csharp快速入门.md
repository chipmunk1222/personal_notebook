- 模板：
```csharp
using System;

namespace HelloWorld
{
  class Program
  {
    static void Main(string[] args)
    {
      Console.WriteLine("Hello World!");    
    }
  }
}
```
- using system：调用类单元，
- namespace ：对代码进行分区管理
- main：封装执行程序
- csharp对大小写敏感
- 不提供大范围到小范围的隐式转换

- 输出：Console.WriteLine(a)
- 输入：string a = Console.Readline()（读入的数据为字符串类型）
- 字符串内插法：string name = $"My full name is: {firstName} {lastName}";
- foreach（type a in arr）{}
- 二维数组：int\[,\] numbers = { {1, 4, 2}, {3, 6, 8} };
- 接口：使用Interface声明接口，使用：调用接口

调试：
- Debug.write()：用于在控制台输出信息
- debug.Assert()：如果条件为false，用于返回错误信息，只在调试模式有效
- debug.Trace()：在调试和发布模式下都生效

Csharp属性：
- 定义：通过预设定get和set属性决定对象I/O流
- public my_method{get return; set}

C#委托：
- 定义：类似于函数指针，通过定义委托方法可以传递函数实例(调用返回值)，
- public delegate int MyDelegate (string s);
- Predicate委托：一种只返回bool类型的泛型委托
- 语法：Predicate \<String> IsString = (s)=>{s.equals(s1)}
	- bool result = IsString(s1)

C#文件读写：
- StreamReader sr = new StreamReader("url");
- string line = sr.ReadLine();
- while((line = sr.ReadLine())!=null){
	- string \[] item  = line.Spilt()
	- MyObj obj = item\[0];
- }
- 通过StreamReader读取文件，通过字符串分割获取字段，通过类型转换构建类对象

api：
- 类型转换：
	- 显示转换：int intvalue = (int)doublevalue
	- Convert方法：将数据转换成相应类型
	- Convert.Toint32()、Convert.Todouble()、Convert.ToString()
	- Parse方法：double d = double.Parse(str)


- 字符串api：
	- public int IndexOf(char value\[,int startindex])：返回对应字符的下标位置
	- public static string Join( string separator, string\[] value ) ：用指定字符连接字符串
	- public string Remove( int startIndex, int count )：从指定下标开始删除字符串
	- public string Replace( string oldValue, string newValue )：将所有指定字符串替换为新字符串
	- public string ToLower()：将字符串转换为小写
	- public string ToUpper()：将字符串转换为大写
	- public string Trim()：移除首尾空格
	- public string\[] Split(string obj)：以参数将字符串分割为数组

- 数组api：
	- 注：数组初始化时编译器会自动隐式初始化默认值
	- 数组属性：Length
	- IndexOf(Array，Object)：返回对象第一次出现的下标
	- Reverse(Array)：逆转数组
	- Sort(Array)：排序

C#集合：
- List(链表)：
	- Add（）：在链表最后添加
	- Delete（）：删除第一个匹配项
	- Sort（）：排序
- ArrayList(动态数组)：
	- 属性：Count：个数
	- public virtual bool Contains( object item )：数组中是否存在包含项
	- public virtual int IndexOf(object)：第一个对象的下标
	- public virtual void Insert( int index, object value )：在下标位置插入值
	- public virtual void Remove( object obj )：删除第一次出现的指定对象
	- Reverse（）：逆转；Sort（）：排序
- HashTable(hash表)：
	- 属性：Count：个数
	- public virtual void Add( object key, object value )：添加键值对
	- public virtual bool ContainsKey( object key )：查询是否存在对应键
	- public virtual void Remove( object key )：删除指定键值元素

- LINQ：
	- var query = from obj in objects
				where obj.val = val and obj.val2 = val2
				select obj
				\[orderby obj.id]
				\[distinct]
- 内置方法查询：
	- var query = obj
				.WHERE(obj => obj.val == val)
				.OrderByDescending(obj.val)
				.Select(obj => obj.val2 = val2)
				\[.Distinct()]
				\[.Sum(r=>r.val)]
				\[.Select(obj => new{a=>obj.val ,b=>obj.val2})]
				