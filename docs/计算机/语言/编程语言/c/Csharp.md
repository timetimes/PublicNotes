# C#

[C# | Microsoft Learn](https://learn.microsoft.com/zh-cn/dotnet/csharp)是一个由微软（Microsoft）开发的面向对象的编程语言
C# 语言是适用于 .NET平台（免费的跨平台开源开发环境）的最流行语言。
C# 编程是基于 C 和 C++ 编程语言的

C# 文件的后缀为 `.cs`

```c#
// 单行注释
/* 多行注释 */
using System;

class Hello
{
    static void Main()
    {
        // This line prints "Hello, World" 
        Console.WriteLine("Hello, World");
    }
}
```

当没有顶级语句时，名为 `Main` 的静态方法将充当 C# 程序的入口点

- C# 区分大小写
- 分号 (`;`) 定义语句的结束，使用大括号（`{` 和 `}`）控制语句的块范围
	空格并不重要。但是，为了便于阅读，使用缩进来强化 `{` 和 `}`声明的块范围。
- C# 是一种强类型语言， 声明的每个变量都有一个在编译时已知的类型

Vscode配置C#编程环境：
1. 安装Vscode和[.NetCore SDK](https://dotnet.microsoft.com/en-us/learn/dotnet/hello-world-tutorial/install)（终端输入`dotnet -h`检测是否安装）
2. Vscode搜索并安装C#、C# Dev Kit、C/C++三个插件
3. 在Vscode终端中输入`dotnet new console`，继续在终端中输入`dotnet run`
4. 按下键盘`Ctrl+Shift+P`，选择`.Net:Generate Assets for build and Debug`即可

## 程序结构

## 基础语法

标识符是用来识别类、变量、函数或任何其它用户定义的项目。在 C# 中，类的命名必须遵循如下基本规则：

- 标识符必须以字母、下划线或 @ 开头，后面可以跟一系列的字母、数字（ 0 - 9 ）、下划线（ _ ）、@。
- 标识符中的第一个字符不能是数字。
- 标识符必须不包含任何嵌入的空格或符号，比如 ? - +! # % ^ & * ( ) [ ] { } . ; : " ' / \。
- 标识符不能是 C# 关键字。除非它们有一个 @ 前缀。 例如，@if 是有效的标识符，但 if 不是，因为 if 是关键字。
- 标识符必须区分大小写。大写字母和小写字母被认为是不同的字母。
- 不能与C#的类库名称相同。

关键字是 C# 编译器预定义的保留字。这些关键字不能用作标识符，但是，如果您想使用这些关键字作为标识符，可以在关键字前面加上 @ 字符作为前缀。

### 数据类型

在C#中，数据类型主要分为两大类：值类型（Value Types）和引用类型（Reference Types）。
此外，C#还支持指针类型（Pointer Types），但指针类型通常用于不安全代码（unsafe code）中。

|**类型**|**示例**|
|---|---|
|值类型|`int`, `float`, `char`, `bool`, `struct`|
|引用类型|`string`, `class`, `array`, `delegate`|
|指针类型|`int*`, `char*`（仅用于不安全代码）|
|其他类型|元组、匿名类型|

#### 值类型

值类型变量可以直接分配给一个值。它们是从类 `System.ValueType` 中派生的
值类型的变量直接存储数据，而不是存储对数据的引用。值类型通常存储在栈上（除非它们是类的一部分）。

1.1 简单类型（Simple Types）
整数类型：
sbyte（8位有符号整数，范围：-128 到 127）
byte（8位无符号整数，范围：0 到 255）
short（16位有符号整数，范围：-32,768 到 32,767）
ushort（16位无符号整数，范围：0 到 65,535）
int（32位有符号整数，范围：-2,147,483,648 到 2,147,483,647）
uint（32位无符号整数，范围：0 到 4,294,967,295）
long（64位有符号整数，范围：-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807）
ulong（64位无符号整数，范围：0 到 18,446,744,073,709,551,615）
浮点类型：
float（32位单精度浮点数，精度约6-9位小数）
double（64位双精度浮点数，精度约15-17位小数）
字符类型：
char（16位Unicode字符）
布尔类型：
bool（布尔值，true 或 false）
1.2 枚举类型（Enum Types）
枚举类型是由一组命名常量定义的值类型。例如：

```c#
enum Days { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday }
```

1.3 结构类型（Struct Types）
结构类型是用户定义的值类型，可以包含字段、方法、属性等。例如：

```c#
struct Point
{
    public int X;
    public int Y;
}
```

1.4 可空值类型（Nullable Value Types）
可空值类型允许值类型具有null值。例如：

```c#
int? nullableInt = null;
```

#### 引用类型

引用类型的变量存储的是对数据的引用（内存地址），而不是数据本身。引用类型的数据通常存储在堆上。
2.1 类类型（Class Types）
内置类：
object（所有类型的基类）
string（字符串类型，不可变）
用户定义类：

```c#
class Person
{
    public string Name;
    public int Age;
}
```

2.2 接口类型（Interface Types）
接口定义了一组方法或属性的契约，类可以实现接口。例如：

```c#
interface IAnimal
{
    void MakeSound();
}
```

2.3 数组类型（Array Types）
数组是相同类型元素的集合。例如：

```c#
int[] numbers = new int[5];
```

2.4 委托类型（Delegate Types）
委托是一种引用方法的类型，类似于函数指针。例如：

```c#
delegate void MyDelegate(string message);
```

2.5 动态类型（Dynamic Types）
dynamic类型在编译时不进行类型检查，而是在运行时解析。例如：

```c#
dynamic myVar = 10;
myVar = "Hello";
```

2.6 字符串类型（String Type）
string是一个特殊的引用类型，用于表示文本。例如：

```c#
string name = "John";
```

C# string 字符串的前面可以加 @（称作"逐字字符串"）将转义字符（\）当作普通字符对待
@ 字符串中可以任意换行，换行符及缩进空格都计算在字符串长度之内

#### 指针类型

指针类型用于存储变量的内存地址，通常用于不安全代码（unsafe code）中。例如：

```c#
unsafe
{
    int x = 10;
    int* ptr = &x;
}
```

#### 其他类型

元组是一种轻量级数据结构，可以存储多个值。例如：

```c#
var person = (Name: "John", Age: 30);
```

匿名类型用于临时存储数据。例如：

```c#
var person = new { Name = "John", Age = 30 };
```

#### 数据类型转换

隐式类型转换和显式类型转换

(int)
intValue.ToString()

### 变量

变量定义`<data_type> <variable_list>;`
变量初始化`variable_name = value;`
变量可以在声明时被初始化（指定一个初始值）

变量的作用域定义了变量的可见性和生命周期

常量是固定值，程序执行期间不会改变。常量可以是任何基本数据类型。
常量可以被当作常规的变量，只是它们的值在定义后不能被修改。
`const <data_type> <constant_name> = value;`

### 运算符

### 语句

语句都可以嵌套

#### 判断语句

if
if...else
switch

#### 循环语句

while
do while
for/foreach

循环控制语句
break
continue

### 输出

如果在字符串的左引号前添加 `$`，则可以在大括号之间的字符串内包括变量

```c#
string aFriend = "Bill";
aFriend = "Maira";
Console.WriteLine($"Hello {aFriend}");
```

### 顶级语句

在 C# 9.0 版本中，引入了顶级语句（Top-Level Statements）的概念，这是一种新的编程范式，允许开发者在文件的顶层直接编写语句，而不需要将它们封装在方法或类中。

文件限制：顶级语句只能在一个源文件中使用。如果在一个项目中有多个使用顶级语句的文件，会导致编译错误。
程序入口：如果使用顶级语句，则该文件会隐式地包含 Main 方法，并且该文件将成为程序的入口点。
作用域限制：顶级语句中的代码共享一个全局作用域，这意味着可以在顶级语句中定义的变量和方法可以在整个文件中访问。
顶级语句在简化代码结构、降低学习难度和加快开发速度方面具有显著优势，特别适合于编写简单程序和脚本。

## 独特的 C# 功能

[语言集成查询 (LINQ)](https://learn.microsoft.com/zh-cn/dotnet/csharp/linq/) 提供一种基于模式的通用语法来查询或转换任何数据集合。 LINQ 统一了查询内存中集合、结构化数据（例如 XML 或 JSON）、数据库存储，甚至基于云的数据 API 的语法。
 以下查询查找平均学分大于 3.5 的所有学生：

```c#
var honorRoll = from student in Students
                where student.GPA > 3.5
                select student;
```