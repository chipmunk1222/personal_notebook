- java特点：
- 所有代码得包含在类中，每一个文件应该包含main（）方法
- 对大小写敏感
- 不提供大范围向小范围的自动转换（只能强转）
- 转换方法：Convert.To(type)（a）
- 模板：
public class Main {
  public static void main(String[] args) {
    System.out.println("Hello World");
  }
}
- 输出：System.out.println()
- 输入：引包：
import java.util.Scanner;
Scanner s = new Scanner(System.in);
```java
 int a = s.nextInt();  
 String c = s.nextLine()
```
- 直接输入：char a = input.next()（读入的数据为字符串类型）
- 输入整行：shtring a = input.nextLine()
- 输入整形：int a = input.nextInt()
- "for-each" 表达式：for（type a : arr）{}
- 二维数组：int\[\]\[\] numbers = { {1, 4, 2}, {3, 6, 8} };
- .equals()方法：比较内容，== 比较类型+值