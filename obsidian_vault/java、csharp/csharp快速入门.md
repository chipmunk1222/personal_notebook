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
- 不提供大范围到小范围的强制转换（只能强转）

- 输出：Console.WriteLine(a)
- 输入：string a = Console.Readline()（读入的数据为字符串类型）
- 字符串内插法：string name = $"My full name is: {firstName} {lastName}";
- foreach（type a in arr）{}
- 二维数组：int\[,\] numbers = { {1, 4, 2}, {3, 6, 8} };

调试：
- Debug.write()：用于在控制台输出信息
- debug.Assert()：如果条件为false，用于返回错误信息，只在调试模式有效
- debug.Trace()：在调试和发布模式下都生效

Csharp属性：
- 定义：通过预设定get和set属性决定对象I/O流
- public my_method(){get return; set}

