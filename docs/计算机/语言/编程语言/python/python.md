# python

Python 是一个高层次的结合了解释性、编译性、互动性和面向对象的脚本语言。

文件扩展名为 `.py`

*Python2中默认的编码格式是ASCII，在文件开头加入 `# coding=utf-8`即可修改；而Python3开始默认使用utf-8编码*

安装[python](https://www.python.org/downloads/) *在安装过程中，请务必勾选“Add Python to PATH”选项，以便自动配置环境变量，否则需要自己设置。*
Vscode扩展：Python、Python Debugger

python运行机制： 首先将.py文件编译成字节码，存储在.pyc文件中（该字节码在虚拟机上运行非cpu）。当python程序第二次运行时，首先程序会在硬盘中寻找.pyc文件，如果找到直接运行，否则重复上述过程。
由于引入了字节码，其加载速度比之前的.py文件有所提高，而且还可以实现源码隐藏，一定程度上可以反编译

`__pycache__`文件夹下保存着 .pyc/.pyo 文件

.py
最常见的Python代码文件后缀名，官方称Python源代码文件。

.ipynb
ipynb是Jupyter Notebook文件的扩展名，它代表"IPython Notebook"。

.pyi
.pyi文件是Python中的类型提示文件，用于提供代码的静态类型信息。
一般用于帮助开发人员进行类型检查和静态分析。

.pyc
.pyc是Python字节码文件的扩展名，用于存储已编译的Python源代码的中间表示形式，因为是二进制文件所以我们无法正常阅读里面的代码。
.pyc文件包含了已编译的字节码，它可以更快地被Python解释器加载和执行，因为解释器无需再次编译源代码。
.pyd

.pyd是Python扩展模块的扩展名，用于表示使用C或C++编写的二进制Python扩展模块文件。
.pyd文件是编译后的二进制文件，它包含了编译后的扩展模块代码以及与Python解释器交互所需的信息。
此外，.pyd文件通过import语句在Python中导入和使用，就像导入普通的Python模块一样。
由于C或C++的执行速度通常比纯Python代码快，可以使用扩展模块来优化Python代码的性能，尤其是对于计算密集型任务。

.pyw
.pyw是Python窗口化脚本文件的扩展名。
它表示一种特殊类型的Python脚本文件，用于创建没有命令行界面（即控制台窗口）的窗口化应用程序。
一般情况下，运行Python脚本会打开一个命令行窗口，其中显示脚本输出和接受用户输入。但是，对于某些应用程序，如图形用户界面（GUI）应用程序，不需要命令行界面，而是希望在窗口中显示交互界面。这时就可以使用.pyw文件。

.pyx
.pyx是Cython源代码文件的扩展名。
Cython是一种编译型的静态类型扩展语言，它允许在Python代码中使用C语言的语法和特性，以提高性能并与C语言库进行交互。

## 代码

### 代码编写规范

格式

编码与特殊字符
使用换行符（LF）换行，而非 CRLF 或 CR。（编辑器默认）
在每个文件的末尾使用一个换行符。（编辑器默认）
使用不带字节顺序标记的 UTF-8 编码。（编辑器默认）
使用制表符代替空格进行缩进。（编辑器默认）

缩进
每个缩进的缩进级别必须大于包含该缩进的代码块的缩进级别。

请在数组、字典和枚举的最后一行使用逗号，这样，在添加新元素时就不需要修改最后一行了，既能让版本控制中的重构更容易，也会让 Diff 也更美观。
单行列表中不需要行尾逗号，故在此情况下不要添加逗号。

用两个空行来包围函数和类定义
函数内部使用一个空行来分隔每个逻辑片段。

把每行代码控制在100个字符以内。

要避免将多个语句放在一行当中，包括条件语句，该规则的唯一例外便是三元运算符

如果你的 `if` 语句特别长，亦或如果一条语句是嵌套的三元表达式，把它们拆分成多行可以提高可读性。由于这几行连续的代码仍属于同一个表达式，故应该缩进两级而非一级。

避免在表达式和条件语句中使用括号，除非需要修改操作顺序或者将语句拆分多行编写，否则只会降低可读性

推荐使用英文布尔运算符，简单易懂，也可以在布尔运算符周围使用括号来消除歧义，这样还可以使长表达式更有可读性

使用pass语句代替

## 基础语法

> 展示语法格式：
> `<变量名> [: 类型] [= <初始值>]`
> 其中尖括号引用的内容表示必须填写，并把尖括号内的东西换成该填入的字符，方括号表示可选填写

Python 与其他语言最大的区别就是，Python 的代码块不使用大括号 `{}` 而是 **`缩进`** 来控制类，函数以及其他逻辑判断。缩进的空白数量是可变的，但是所有代码块语句必须包含相同的缩进空白数量

Python语句中一般以新行作为语句的结束符，但是我们可以使用斜杠 `\` 将一行的语句分为多行显示。语句中包含 [], {} 或 () 括号就不需要使用多行连接符。

Python 可以使用引号( ' )、双引号( " )、三引号( ''' 或 """ ) 来表示字符串，引号的开始与结束必须是相同类型的。其中三引号可以由多行组成，编写多行文本的快捷语法，常用于文档字符串，在文件的特定地点，被当做注释。

函数之间或类的方法之间用空行分隔，表示一段新的代码的开始。类和函数入口之间也用一行空行分隔，以突出函数入口的开始。空行与代码缩进不同，空行并不是Python语法的一部分。书写时不插入空行，Python解释器运行也不会出错。但是空行的作用在于分隔两段不同功能或含义的代码，便于日后代码的维护或重构。

Python可以在同一行中使用多条语句，语句之间使用分号(;)分割

在Python中，如果一行代码过长，可以使用多种方法来换行继续写，以提高代码的可读性。以下是一些常用的换行方法：
在行末尾添加反斜杠（\）可以将代码分成多行。
括号内的多行表达式或元素会被视为一行。
可以使用加号（+）连接多行字符串。
三引号可以定义包含多行文本的字符串。

```python
print("这是一个非常长的字符串，\
它跨越了多行。")

numbers = [
1, 2, 3,
4, 5, 6,
7, 8, 9
]

message = "这是一个非常长的消息，" + \
"它跨越了多行。"

message = """这是一个非常长的消息，
它跨越了多行。
"""
```

### 注释与注解

```python
# 单行注释

'''
多行注释
'''

"""
多行注释
"""
```

Python3.0之后加入新特性Decorators，以@为标记修饰function和class。

```python
# 注解对代码没有任何影响，仅仅是方便程序员阅读
# 函数注解：申明函数参数中变量类型，与返回值类型
def add(x: int, y: int) -> int:
    return x+y

# 变量注解：
a2: int = 123 # a2为int型变量，赋值为123
```

### 输入和输出

input("输入文字")

Python两种输出值的方式: 表达式语句和 print() 函数。
第三种方式是使用文件对象的 write() 方法，标准输出文件可以用 sys.stdout 引用。
如果你希望输出的形式更加多样，可以使用 str.format() 函数来格式化输出值。
如果你希望将输出的值转成字符串，可以使用 repr() 或 str() 函数来实现。

### 变量

Python 是动态语言，变量不需要类型声明。

每个变量在内存中创建，都包括变量的标识，名称和数据这些信息。
每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。
等号 = 用来给变量赋值。

Python允许你同时为多个变量赋值。

```python
a = 1
a, b = 2, a # 序列解包。利用元组或列表（可迭代对象）实现的，省略了括号
print(a, b) # 输出2 1，因此可以使用 a,b=b,a 交换两变量值

a = b = 1 # 链式赋值。由于不可变数据类型链式赋值指向同一地址，会一起更改，所以不要使用

a, *b, c = [1, 2, 3, 4, 5] # 使用星号表达式。将一个可迭代对象的剩余值赋给一个变量
print(a, b, c)  # 输出 1 [2, 3, 4] 5
```

#### Python 保留字符

下面的列表显示了在Python中的保留字。这些保留字不能用作常数或变数，或任何其他标识符名称。
所有 Python 的关键字只包含小写字母。

同时Python 的标准库提供了 keyword 模块，可以输出当前版本的所有关键字

```python
import keyword
print(keyword.kwlist)
```

<table>
    <tr>
        <td>and</td>
        <td>assert</td>
        <td>break</td>
        <td>class</td>
        <td>continue</td>
        <td>def</td>
    </tr>
    <tr>
        <td>del</td>
        <td>elif</td>
        <td>else</td>
        <td>except</td>
        <td>exec</td>
        <td>finally</td>
    </tr>
    <tr>
        <td>for</td>
        <td>from</td>
        <td>global</td>
        <td>if</td>
        <td>import</td>
        <td>in</td>
    </tr>
    <tr>
        <td>is</td>
        <td>lambda</td>
        <td>not</td>
        <td>or</td>
        <td>pass</td>
        <td>print</td>
    </tr>
    <tr>
        <td>raise</td>
        <td>return</td>
        <td>try</td>
        <td>while</td>
        <td>with</td>
        <td>yield</td>
    </tr>
</table>

#### 变量名

**标识符**：

> 第一个字符必须是字母表中字母或下划线 _ 。
> 标识符的其他的部分由字母、数字和下划线组成。
> 标识符对大小写敏感。

*在 Python 3 中，可以用中文作为变量名，非 ASCII 标识符也是允许的了。*

变量名，即变量的标识符

变量名只能用“_ ”，数字，字母组成，不可以是空格或者特殊字符（#？< . , $￥*~！）
不能以数字开头
保留字符不能被使用
变量名区分大小写

通常使用驼峰式命名法、下划线分隔单词，且变量名具有实际意义。如：（studentName或student_name）
类：大驼峰命名法 StudentName
变量和函数：蛇形命名法 student_name
常量：全大写 ALL_CAPS
私有字段：前缀下划线的小驼峰命名法 _camelCase

#### 常量

在Python中，常量是指在程序执行期间其值不会发生变化的特殊变量。尽管Python没有内置的常量类型，但我们可以通过一些约定和设计模式来模拟常量的行为。（有的语言会使用关键字定义常量）

**使用变量声明常量**：
常量的名称应全部大写

```python
PI = 3.14159
```

这种方法虽然简单，但只是一个约定，并不能阻止常量被重新赋值。

**使用模块定义常量**：
创建一个名为constants.py的文件，并在其中定义所有的常量。然后，在其他模块中导入constants模块来使用这些常量

```python
# constants.py
PI = 3.14159

# main.py
import constants
```

使用类封装常量
可以创建一个包含常量的类，并将这些常量作为类属性。这种方法的优点是可以利用类的封装特性，防止常量被意外修改。

```python
# constants.py
class Constants:
	PI = 3.14159

# main.py
from constants import Constants
```

使用装饰器或特殊方法实现常量
通过使用装饰器，我们可以定义一个将常量注入到全局命名空间的函数。

```python
# constants.py
def constant(name, value):
    globals()[name] = value

constant('PI', 3.14159)

# main.py
from constants import PI
```

创建一个const.py模块，并在其中定义一个 `_const`类，该类通过重写 `__setattr__`方法来防止常量被重新赋值

```python
# const.py
class _const:
	class ConstError(TypeError): pass
	def __setattr__(self, key, value):
		if key in self.__dict__:
			raise self.ConstError("Can't rebind const (%s)" % key)
		self.__dict__[key] = value

import sys
sys.modules[__name__] = _const()

# main.py
import const
```

### 数据类型

Python 中的变量不需要声明。每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。
Python 中，变量就是变量，它没有类型，我们所说的"类型"是变量所指的内存中对象的类型。

不可变数据类型：Number（数字）、String（字符串）、Tuple（元组）
可变数据类型：List（列表）、Dictionary（字典）、Set（集合）

隐式类型转换 - 自动完成 两种不同类型的数据进行运算，较低数据类型（如整数）就会转换为较高数据类型（如浮点数）以避免数据丢失
显式类型转换 - 需要使用类型函数来转换 int()、float()、str()等

通常用len统计个数

#### 数字

- 整型(int) - 通常被称为是整型或整数，是正或负整数，不带小数点。Python3 整型是没有限制大小的，可以当作 Long 类型使用，所以 Python3 没有 Python2 的 Long 类型。布尔(bool)是整型的子类型。
- 浮点型(float) - 浮点型由整数部分与小数部分组成，浮点型也可以使用科学计数法表示（2.5e2 = 2.5 x 102 = 250）
- 复数( (complex)) - 复数由实数部分和虚数部分构成，可以用a + bj,或者complex(a,b)表示， 复数的实部a和虚部b都是浮点型。

1）divmod() 函数把除数和余数运算结果结合起来，返回一个包含商和余数的元组(a // b, a % b)。
2)abs() 函数返回数字的绝对值。
3)pow() 方法返回 xy（x的y次方）的值。
4)round（x,n）返回浮点数x四舍五入后保留n位小数的值
5)nim(),max()会返回给定序列的最小/最大值

#### 字符串

转义字符串

| **转义序列** | **转义为**                                         |
| ------------------ | -------------------------------------------------------- |
| `\n`             | 换行(line feed,LF)                                       |
| `\t`             | 水平制表符（tab）                                        |
| `\r`             | 回车（carriage return,CR）                               |
| `\a`             | 警报（蜂鸣/响铃）                                        |
| `\b`             | 退格键（Backspace）                                      |
| `\f`             | 换页符（form feed,FF）                                   |
| `\v`             | 垂直制表符（tab）                                        |
| `\"`             | 双引号                                                   |
| `\'`             | 单引号                                                   |
| `\\`             | 反斜杠                                                   |
| `\uXXXX`         | Unicode UTF-16 码位 `XXXX` （16进制，不区分大小写）   |
| `\UXXXXXX`       | Unicode UTF-32 码位 `XXXXXX` （16进制，不区分大小写） |

f字符串{{}}转义{}

''/""
b"Hello world!" 这里的’b’代表二进制（bytes）的意思，它告诉Python这个字符串是以字节序列的形式表示的，而不是普通字符串
字符串是由Unicode码点序列构成的，而字节序列则是由8位字节构成的。因此，当我们需要表示一些非Unicode的文本数据时，就需要使用字节序列。
如果你想要将一个字符串转换成字节序列，你可以使用字符串的encode()方法
可以使用decode()方法将一个字节序列转换成字符串.如果字节序列中包含了一些不符合编码要求的字节，那么它就无法被正确地转换成字符串

在Python中，r字符串前缀是一种特殊的字符串前缀，用于表示原始字符串。当一个字符串以r前缀开始时，它将被视为原始字符串，其中的转义字符将被忽略。

当字符串前加上字母f，这表示该字符串是一个格式化字符串（f-string）。这是Python 3.6及更高版本中引入的一种新特性，允许在字符串内部直接插入变量和表达式的值

内插字符串 $""

chr() 用一个范围在 range（256）内的（就是0～255）整数作参数，返回一个对应的字符。
ord() 函数是 chr() 函数（对于8位的ASCII字符串）的配对函数，它以一个字符（长度为1的字符串）作为参数，返回对应的 ASCII 数值。
oct() 函数将一个整数转换成8进制字符串。
hex() 函数用于将10进制整数转换成16进制，以字符串形式表示。
len() 方法返回对象（字符、列表、元组等）长度或项目个数。
str()返回一个对象的string格式。
**str也内置了很多对字符串进行操作的函数：**
string.upper()转换string 中的小写字母为大写
string.lower()转换string 中的小写字母为小写
string.capitalize()把字符串的第一个字符大写
string.find(str,beg=0, end=len(string)) 检测 str 是否包含在 string 中，如果 beg 和end 指定范围，则检查是否包含在指定范围内，如果是返回 开始的索引值，否则返回-1
string.join(seq)以 string 作为分隔符，将 seq 中所有的元素(的字符串表示)合并为一个新的字符串
string.rfind(str,beg=0,end=len(string) ) 类似于 find()函数，不过是从右边开始查找.

s[start:stop:step]左包右不包  没填留空时，表示字符串最开始那个位置
`s[:-1]`表示从开始到倒数第二个字符的所有字符，s=s[:-1]即删除最后一个字符

字符串根据第一个字符的编码比较

Python replace方法把字符串中的old（旧字符串） 替换成new(新字符串)，如果指定第三个参数max，则设置替换次数不超过 max 次。

```python
str.replace(old, new[, max])
```

Python的translate函数与replace函数一样，用于替换字符串的一部分。Translate只能处理单个字符，但translate可以同时进行多个替换任务。在使用translate函数进行转换之前。需要一个翻译表table，翻译表用于表示字符的替换关系，这个翻译表可以通过maketrans()方法获得。这个翻译表可翻译字符数为256，翻译表中的字符都要包含在ASCII码表（含扩展）中。translate()方法语法为：

```python
str.translate(table)
```

re.sub 替换字符串

我们可以使用正则表达式来替换字符串。Python的re库就是常用的正则表达式匹配库（建议学一学很有用）。re库使用见模式匹配。这里主要使用re.sub函数替换字符串。re.sub()方法需要传入两个参数。第一个参数是一个字符串，用于取代发现的匹配。第二个参数是一个字符串，即正则表达式。sub()方法返回替换完成后的字符串。
re.sub(pattern, repl, text)
`re.sub(r'[\/\\\:\*\?\'\"\<\>\|\#. ]', '_', name)`

转换为列表

str.format()

>>> "{} {}".format("hello", "world")    # 不设置指定位置，按默认顺序
>>> 'hello world'
>>>
>>

>>> "{0} {1}".format("hello", "world")  # 设置指定位置
>>> 'hello world'
>>>
>>

>>> "{1} {0} {1}".format("hello", "world")  # 设置指定位置
>>> 'world hello world'
>>>
>>
>
> ### 数字格式化
>
> **^**, **<**, **>** 分别是居中、左对齐、右对齐，后面带宽度， **:** 号后面带填充的字符，只能是一个字符，不指定则默认是用空格填充。
>
> **+** 表示在正数前显示 **+**，负数前显示 **-**；** ** （空格）表示在正数前加空格
>
> b、d、o、x 分别是二进制、十进制、八进制、十六进制。
>
> 此外我们可以使用大括号 **{}** 来转义大括号

- eval()函数：将字符串转换为Python表达式并计算返回结果。也就是说，它一般用于计算并返回单个表达式的值，并返回执行结果。
- exec()函数：用于动态执行Python代码。也就是说，它可以执行任何字符串类型的Python代码，但是没有返回值。

可能存在危险（任何内容都可能被执行，而不仅仅是简单条件，如果用户输入被包含在内，可能会被滥用）

#### 元组

#### 列表

创建列表可以直接 $l=[]$ 和使用函数 $l=list()$
可以通过 $list(range())$ 快速创建等差整数列表

list.append(obj)在列表末尾添加新的对象
list.extend(seq)在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）
list.insert(index,obj)将对象插入列表
list.pop([index=-1])移除列表中的一个元素（默认最后一个元素），并且返回该元素的值
list.remove(obj)移除列表中某个值的第一个匹配项
list.reverse()反向列表中元素
list.sort(cmp=None,key=None, reverse=False)对原列表进行排序
list.count(obj)统计某个元素在列表中出现的次数

copy

sort 是 list 的一个方法，而 sorted 可以对所有可迭代的对象进行排序操作

```python
list.sort(key=None, reverse=False)
```

- key -- 用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
- reverse -- 排序规则，**reverse = True** 降序， **reverse = False** 升序（默认）
  没有返回值，但是会对列表的对象进行排序

```python
lt.sort(key=lambda x:x[1],reverse=True) 
```

对于列表，可以使用list.index()方法结合max()函数来找到最大值的索引。对于NumPy数组，可以使用np.argmax()函数来获取最大值的索引。

列表去重：list(set(list_1)
字典在 Python 3.7 及以上版本中保持插入顺序
去重并保持顺序：list(dict.fromkeys(lst))
[unique_list.append(item) for item in lst if item not in unique_list]

#### 字典

dict.clear()删除字典内所有元素
dict.copy()返回一个字典的浅复制
dict.fromkeys(seq[, val])创建一个新字典，以序列 seq 中元素做字典的键，val 为字典所有键对应的初始值
dict.get(key,default=None)返回指定键的值，如果值不在字典中返回default值(如果使用dict[key]，如果值不在字典中会报错)
dict.has_key(key)如果键在字典dict里返回true，否则返回false
dict.items()以列表返回可遍历的(键, 值) 元组数组
dict.keys()以列表返回一个字典所有的键
dict.update(dict2)把字典dict2的键/值对更新到dict里
dict.values()以列表返回字典中的所有值
pop(key[,default])删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。否则，返回default值。
popitem()返回并删除字典中的最后一对键和值。

`erase` 方法

直接迭代字典会返回字典的键，而不是键值对
可以使用 .items() 方法来迭代键值对

```python
for key in dict:
for key, value in dict.itrms():
```

```python
# 实现对字典的切片操作
def dict_slice(adict, start, end):
    keys = adict.keys()
    dict_slice = {}
    for k in list(keys)[start:end]:
        dict_slice[k] = adict[k]
    return dict_slice

def dict_slice(adict, start, end):
    return {k: adict[k] for k in list(adict.keys())[start:end]}
```

#### 集合

**map()** 是 Python 内置的高阶函数，它接收一个函数和一个或多个可迭代对象（如列表），并通过将函数依次作用于可迭代对象的每个元素，返回一个包含函数返回值的新迭代器

add(x)元素x添加到集合s中，如果元素已存在，则不进行任何操作。
remove(x)将元素x从集合s中移除，如果元素不存在，则会发生错误。
len() 计算集合s元素个数。
clear() 清空集合s。
pop()随机移除元素
symmetric_difference()返回两个集合中不重复的元素集合
union()返回两个集合的并集
symmetric_difference_update()移除当前集合中在另外一个指定集合相同的元素，并将另外一个指定集合中不同的元素插入到当前集合中。
difference()返回多个集合的差集

#### 数据类型转换

隐式（自动）类型转换 - 自动完成
显式（强制）类型转换 - 需要使用类型函数来转换

对两种不同类型的数据进行运算，较低数据类型（整数）就会转换为较高数据类型（浮点数）以避免数据丢失
使用 int()、float()、str() 等预定义函数来执行显式类型转换
会丢失非法字符，int表现为取整。。。

#### 枚举Enum类型

枚举类是一种特殊的数据类型，用于表示一组具有离散取值的常量。它将常量与有意义的名字关联起来，使得代码更易读、更易维护。枚举类的每个成员都有一个唯一的名称和一个关联的值。
在代码中使用枚举来代替魔术数字（不明确的常量值）可以增加代码的可读性。枚举为常量提供了有意义的名字，使得代码更容易理解。
枚举成员的名称通常应该使用大写字母，以便与常规变量和函数名称区分开。
枚举成员是不可变的，一旦创建就不能更改其值。这有助于确保枚举成员的稳定性，并防止意外的修改。
两个枚举成员的名称不能相同

在Python中，使用内置模块 `enum`来创建和使用枚举类。

```python
from enum import Enum

class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3
```

定义枚举类，可以通过成员名来访问枚举成员 `print(Color.RED)`
获取枚举成员的关联值，可以使用成员的value属性 `print(Color.RED.value)`
枚举成员可以使用相等运算符进行比较。可以直接比较枚举成员，而不必比较它们的值。
使用 `for`循环来迭代枚举类的所有成员。
根据枚举成员的值来获取成员本身 `color = Color(1)`

默认情况下，枚举允许多个名称作为同一个值的别名。若不想如此，可以使用 unique() 装饰器：

```python
from enum import Enum, unique
@unique
class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3
```

如果具体的枚举值无所谓是什么，可以使用 auto:

```python
from enum import Enum

class Color(Enum):
    RED = auto()
    GREEN = 2
    BLUE = 3
```

### 表达式与运算符

表达式是由一些值和运算符组成的式子，例如 `10 + 2`

#### 算术运算符

| 运算符 | 描述                                |
| ------ | ----------------------------------- |
| +      | 加 - 两个对象相加                   |
| -      | 减 - 得到负数或是一个数减去另一个数 |
| *      | 乘 - 两个数相乘或重复的字符串       |
| /      | 除 - x 除以 y                       |
| %      | 取模 - 返回除法的余数               |
| **     | 幂 - 返回x的y次幂                   |
| //     | 取整除 - 往小的方向取整数           |

#### 比较运算符

| 运算符 | 描述                            |
| ------ | ------------------------------- |
| ==     | 等于 - 比较对象是否相等         |
| !=     | 不等于 - 比较两个对象是否不相等 |
| >      | 大于 - 返回x是否大于y           |
| <      | 小于 - 返回x是否小于y           |
| >=     | 大于等于 - 返回x是否大于等于y。 |
| <=     | 小于等于 - 返回x是否小于等于y。 |

所有比较运算符返回1(True)表示真，返回0(False)表示假
可以连续比较：如 `3>2>1`，在c语言中是先比较 `3>2`值为1，然后 `1>1`为假；在python中 `3>2>1`为真

#### 赋值运算符

| 运算符 | 描述                                                 | 实例                                             |
| ------ | ---------------------------------------------------- | ------------------------------------------------ |
| =      | 简单的赋值运算符                                     | c = a + b 将 a + b 的运算结果赋值为 c            |
| +=     | 加法赋值运算符                                       | c += a 等效于 c = c + a                          |
| -=     | 减法赋值运算符                                       | c -= a 等效于 c = c - a                          |
| *=     | 乘法赋值运算符                                       | c *= a 等效于 c = c * a                          |
| /=     | 除法赋值运算符                                       | c /= a 等效于 c = c / a                          |
| %=     | 取模赋值运算符                                       | c %= a 等效于 c = c % a                          |
| **=    | 幂赋值运算符                                         | c **= a 等效于 c = c ** a                        |
| //=    | 取整除赋值运算符                                     | c //= a 等效于 c = c // a                        |
| :=     | 海象运算符，可在表达式内部为变量赋值。Python3.8 新增 | 在这个示例中，赋值表达式可以避免调用 len() 两次: |

#### 位运算符

位运算符是把数字看作二进制来进行计算

| 运算符 | 描述                                                                                          |
| ------ | --------------------------------------------------------------------------------------------- |
| &      | 按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0                    |
| \|     | 按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1                                    |
| ^      | 按位异或运算符：当两对应的二进位相异时，结果为1                                               |
| ~      | 按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1                                  |
| <<     | 左移动运算符：运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数，高位丢弃，低位补0 |
| >>     | 右移动运算符：把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数          |

#### 逻辑运算符

| 运算符 | 逻辑表达式 | 描述                                                                   |
| ------ | ---------- | ---------------------------------------------------------------------- |
| and    | x and y    | 布尔"与" - 如果 x 为 False，x and y 返回 x 的值，否则返回 y 的计算值。 |
| or     | x or y     | 布尔"或" - 如果 x 是 True，它返回 x 的值，否则它返回 y 的计算值。      |
| not    | not x      | 布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。 |

#### 成员运算符

| 运算符 | 描述                                                  |
| ------ | ----------------------------------------------------- |
| in     | 如果在指定的序列中找到值返回 True，否则返回 False     |
| not in | 如果在指定的序列中没有找到值返回 True，否则返回 False |

#### 成员身份运算符

| 运算符 | 描述                                        | 实例                                                                           |
| ------ | ------------------------------------------- | ------------------------------------------------------------------------------ |
| is     | is 是判断两个标识符是不是引用自一个对象     | x is y , 类似 id(x) == id(y) 如果引用的是同一个对象则返回 True，否则返回 False |
| is not | is not 是判断两个标识符是不是引用自不同对象 | x is not y ，类似  id(x) != id(y) 如果引用的不是同一个对象则返回结果 True     |

*is 与 == 区别：is 用于判断两个变量引用对象是否为同一个， == 用于判断引用变量的值是否相等*。

#### 运算符的优先级

| 运算符                                                 | 描述                                                   |
| ------------------------------------------------------ | ------------------------------------------------------ |
| () [] {}                                               | 括号                                                   |
| x[index], x[index:index], x(arguments...), x.attribute | 读取，切片，调用，属性引用                             |
| **                                                     | 指数                                                   |
| ~ + -                                                  | 按位翻转, 一元加号和减号 (最后两个的方法名为 +@ 和 -@) |
| * / % //                                               | 乘，除，取模和取整除                                   |
| + -                                                    | 加法减法                                               |
| >> <<                                                  | 右移，左移运算符                                       |
| &                                                      | 位 'AND'                                               |
| ^\|                                                    | 位运算符                                               |
| <= < > >=                                              | 比较运算符                                             |
| <> == !=                                               | 等于运算符                                             |
| = %= /= //= -= += *= **=                               | 赋值运算符                                             |
| is is not                                              | 身份运算符                                             |
| in not in                                              | 成员运算符                                             |
| not and or                                             | 逻辑运算符                                             |

### 语句

语句一般来说都可以嵌套

#### 条件语句

**if – elif – else**：（可以没有elif或else，也可以有多个elif）

```python
# 如果 "condition_1" 为 True 将执行 "statement_block_1" 块语句
if <condition_1>:
    <statement_block_1>
# 如果 "condition_1" 为False，将判断 "condition_2"
# 如果"condition_2" 为 True 将执行 "statement_block_2" 块语句 
elif <condition_2>:
    <statement_block_2>
# 如果 "condition_2" 为False，将执行"statement_block_3"块语句
else:   
    <statement_block_3>
```

**match...case**：（Python 3.10 增加）

```python
# match 后的对象会依次与 case 后的内容进行匹配
# 如果匹配成功，则执行匹配到的表达式，否则跳过
match subject:
    case <pattern_1>:
        <action_1>
    case <pattern_2>:
        <action_2>
    case <pattern_3>:
        <action_3>
    case _: # _ 可以匹配一切
        <action_wildcard>
```

#### 循环语句

**while-else**：（可以没有else）

```python
# condition为真，执行statements语句
# 有时需要设置条件恒为True实现死循环（控制台使用CTRL+C来退出当前的无限循环）
while <condition>:
    <statements>
# condition为假，执行additional_statements语句
else:
    <additional_statements>
```

**for-in-else**：遍历（可以没有else）

```python
# iterable必须是可迭代对象，如一个列表或者一个字符串
# 循环可以遍历iterable，得到每一个item
for <item> in <iterable>:
    <statements>
# 遍历完iterable中的所有元素后执行一段代码
else:
    <additional_statements>

# 可以使用内置 range() 函数快速创建一个可迭代的数字序列 range([start=0,] stop[, step=1])
for i in range(10):
    print(i, end='')
```

循环控制语句：
**break** 语句 跳出 for 和 while 的循环体（如果循环嵌套，只会跳出一层循环）。如果循环中止，任何对应的循环 else 块将不执行。
**continue** 语句 跳过当前循环块中的剩余语句，然后继续进行下一轮循环。
return

**推导式**：
`int_list = [int(x) for x in str_list]`

### 函数

  函数本质上就是一堆代码的集合，这些代码共同构成某些功能
  把某段常用的代码保存成函数是一个良好的习惯，这样做可以减少代码数量，提高代码复用率

```python
def <方法名称>([参数列表]):
    <方法体>
```

参数可以写很多个，每个参数之间使用逗号分隔 （可选参数）

返回值其实就是一个函数的计算结果，使用 `return` 关键字表示返回值
当结果产生时函数就没必要继续执行了，所以 `return` 关键字还会停止函数的执行

单星号参数用于接收任意数量的位置参数，并将其存储在一个元组中。
双星号参数用于接收任意数量的关键字参数，并将其存储在一个字典中。

#### lambda匿名函数

lambda 函数是一种小型、匿名的、内联函数，它可以具有任意数量的参数，但只能有一个表达式，不需要使用 def 关键字定义完整函数

```python
lambda arguments: expression
```

- `lambda`是 Python 的关键字，用于定义 lambda 函数。
- `arguments` 是参数列表，可以包含零个或多个参数，但必须在冒号(`:`)前指定。
- `expression` 是一个表达式，用于计算并返回函数的结果。

> 将lambda函数赋值给一个变量，通过这个变量间接调用该lambda函数
> 将lambda函数赋值给其他函数，从而将其他函数用该lambda函数替换
> 将lambda函数作为**参数传递**给其他函数

```python
x = lambda a, b : a * b
print(x(5, 6))

numbers = [1, 2, 3, 4, 5]
# map(function, iterable, ...)
squared = list(map(lambda x: x**2, numbers))
print(squared)  # 输出: [1, 4, 9, 16, 25]
```

### 类

面向对象技术简介
类(Class): 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。==对象是类的实例==。
方法：==方法是类中定义的函数==。
类变量：类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体之外。类变量通常不作为实例变量使用。
数据成员：类变量或者实例变量用于处理类及其实例对象的相关的数据。
方法重写：如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。
局部变量：定义在方法中的变量，只作用于当前实例的类。
实例变量：在类的声明中，属性是用变量来表示的，这种变量就称为实例变量，实例变量就是一个用 self 修饰的变量。
继承：即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。例如，有这样一个设计：一个Dog类型的对象派生自Animal类，这是模拟"是一个（is-a）"关系（例图，Dog是一个Animal）。
实例化：创建一个类的实例，类的具体对象。
对象：通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法。

```python
class MyClass:
    """一个简单的类实例"""
    i = 12345
    def f(self):
        return 'hello world'
 
# 实例化类
x = MyClass()
 
# 访问类的属性和方法
print("MyClass 类的属性 i 为：", x.i)
print("MyClass 类的方法 f 输出为：", x.f())
```

类有一个名为 __init__() 的特殊方法（构造方法），该方法在类实例化时会自动调用
类的方法与普通的函数只有一个特别的区别——它们必须有一个额外的第一个参数名称, self 不是 python 关键字,按照惯例它的名称是 self。
在类的内部，使用 def 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 self, 且为第一个参数，self 代表的是类的实例。

继承
Python 支持类的继承，如果一种语言不支持继承，类就没有什么意义。派生类的定义如下所示:

```python
class DerivedClassName(BaseClassName):
    <statement-1>
    .
    .
    .
    <statement-N>
```

子类（派生类 DerivedClassName）会继承父类（基类 BaseClassName）的属性和方法。
多继承
Python有限的支持多继承形式。多继承的类定义形如下例:

```py
class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    .
    .
    .
    <statement-N>
```

需要注意圆括号中父类的顺序，若是父类中有相同的方法名，而在子类使用时未指定，python从左至右搜索 即方法在子类中未找到时，从左到右查找父类中是否包含方法。

如果你的父类方法的功能不能满足你的需求，你可以在子类重写你父类的方法

类属性与方法
类的私有属性
__private_attrs：两个下划线开头，声明该属性为私有，不能在类的外部被使用或直接访问。在类内部的方法中使用时 self.__private_attrs。

类的方法
在类的内部，使用 def 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 self，且为第一个参数，self 代表的是类的实例。

self 的名字并不是规定死的，也可以使用 this，但是最好还是按照约定使用 self。

类的私有方法
__private_method：两个下划线开头，声明该方法为私有方法，只能在类的内部调用 ，不能在类的外部调用。self.__private_methods。

类的专有方法：
__init__ : 构造函数，在生成对象时调用
__del__ : 析构函数，释放对象时使用
__repr__ : 打印，转换
__setitem__ : 按照索引赋值
__getitem__: 按照索引获取值
__len__: 获得长度
__cmp__: 比较运算
__call__: 函数调用
__add__: 加运算
__sub__: 减运算
__mul__: 乘运算
__truediv__: 除运算
__mod__: 求余运算
__pow__: 乘方

创建实例：

```python
class Blog:
   def __init__(self,num):
       print("a new object num is",num)
       self.value = num
   
   def __str__(self):
       return str(self.value+3)
 
# 循环建立四个对象，locals()函数可以将字符串转换为变量名！
#具体的操作和含义我并不清楚，大家可以自行百度～
for i in range(1,5):
    locals()['blog_'+str(i)] = Blog(i)
```

`type()` 函数是Python的一个内置函数，通常用来查看一个对象的类型。但是，它也可以用来动态创建类。`type()` 函数可以接收三个参数：类名（字符串）、父类元组和属性字典。

```python
for i in range(5):
    class_name = f"DynamicClass{i}"

    class_attributes = {
        "attribute": i,
        "method": lambda self: f"Method of {self.__class__.__name__}"
    }

    new_class = type(class_name, (object,), class_attributes)
    instance = new_class()
    print(instance.method())
```


`dir()`函数返回一个包含对象中所有属性和方法的列表。然后，我们可以使用循环来遍历这个列表，并对每个属性进行操作。

`hasattr (object, name)` 判断对象是否包含对应的属性


﻿setattr()、getattr()、hasattr()函数


#### 对象保存（数据持久化）

对象保存是指将内存中的对象转换为可存储或传输的形式，并在需要时恢复为对象的过程。在实际开发中，对象保存很常见，它可以用于数据持久化，数据传输，或者在不同的系统之间共享对象。

1)**Pickle** 是Python标准库中用于对象保存的模块。它可以将对象序列化为字节流，以便存储或传输，并且能够将字节流反序列化为原始对象。

```python
import pickle

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person = Person("Alice", 25)

# 保存对象到文件
with open("person.pickle", "wb") as file:
    pickle.dump(person, file)

# 从文件中加载对象
with open("person.pickle", "rb") as file:
    loaded_person = pickle.load(file)

print(loaded_person.name)  # 输出：Alice
print(loaded_person.age)  # 输出：25
```

**dill**库[[#dill（对象序列化）]]，作为pickle的加强版，提供了更加强大和灵活的序列化功能

```python
import dill

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# 创建一个Person实例
person = Person("Alice", 30)

# 序列化实例到文件
with open('person_instance.dill', 'wb') as f:
    dill.dump(person, f)

# 反序列化实例
with open('person_instance.dill', 'rb') as f:
    new_person = dill.load(f)
```

2)**JSON**（JavaScript Object Notation）是一种轻量级的数据交换格式。它以文本形式来表示结构化数据，并且易于阅读和理解。在Python中，可以通过内置的json模块来实现对象的JSON保存和加载。
JSON与Pickle相比，具有平台无关性，可以被多种编程语言解析和生成。然而，JSON只能保存一些基本的数据类型，例如整数、浮点数、字符串、布尔值、数组和字典等。

```python
import json

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person = Person("Alice", 25)

# 将对象保存为JSON字符串
person_json = json.dumps(person.__dict__)

# 将JSON字符串保存到文件
with open("person.json", "w") as file:
    file.write(person_json)

# 从文件中加载JSON字符串并转换为对象
with open("person.json", "r") as file:
    loaded_person_json = file.read()
    loaded_person_dict = json.loads(loaded_person_json)
    loaded_person = Person(**loaded_person_dict)

print(loaded_person.name)  # 输出：Alice
print(loaded_person.age)  # 输出：25
```

3)如果需要保存大量数据并进行高效查询，可以使用数据库来完成。在Python中，可以使用内置的**sqlite3**模块来操作SQLite数据库。
SQLite是一种嵌入式数据库引擎，它不需要单独的服务器进程，而是将整个数据库作为一个文件存储在磁盘上。SQLite支持标准的SQL语法，并提供了轻量级的事务支持。

```python
import sqlite3

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person = Person("Alice", 25)

# 连接数据库并创建表格
conn = sqlite3.connect("person.db")
cursor = conn.cursor()
cursor.execute("CREATE TABLE IF NOT EXISTS persons (name TEXT, age INTEGER)")

# 将对象保存到数据库
cursor.execute("INSERT INTO persons VALUES (?, ?)", (person.name, person.age))
conn.commit()

# 从数据库中加载对象
cursor.execute("SELECT * FROM persons")
loaded_person_row = cursor.fetchone()
loaded_person = Person(*loaded_person_row)

print(loaded_person.name)  # 输出：Alice
print(loaded_person.age)  # 输出：25

# 关闭数据库连接
cursor.close()
conn.close()
```

4)**CSV**文件
如果想将对象保存为表格形式，可以使用CSV（逗号分隔值）文件。Python提供了csv模块，方便我们进行CSV文件的读写操作。

```python
import csv

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

persons = [
    Person("Alice", 25),
    Person("Bob", 30),
]

# 将对象保存到CSV文件
with open("persons.csv", "w", newline="") as file:
    writer = csv.writer(file)
    for person in persons:
        writer.writerow([person.name, person.age])

# 从CSV文件中加载对象
loaded_persons = []
with open("persons.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        loaded_persons.append(Person(row[0], int(row[1])))

for person in loaded_persons:
    print(person.name, person.age)
```

5)**YAML**（YAML Ain’t Markup Language）是一种人类可读的数据序列化格式。它以简洁、清晰的结构来表示数据，并且支持复杂的数据类型，如列表、字典、甚至嵌套的数据结构。在Python中，可以使用pyyaml库来处理YAML文件。

```python
import yaml

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person = Person("Alice", 25)

# 将对象保存到YAML文件
with open("person.yaml", "w") as file:
    yaml.dump(person.__dict__, file)

# 从YAML文件中加载对象
with open("person.yaml", "r") as file:
    loaded_person_dict = yaml.load(file, Loader=yaml.SafeLoader)
    loaded_person = Person(**loaded_person_dict)

print(loaded_person.name)  # 输出：Alice
print(loaded_person.age)  # 输出：25
```

### 异常处理

*异常*指程序运行错误；*错误*指程序运行和程序逻辑错误

异常即是一个事件，该事件会在程序执行过程中发生，影响了程序的正常执行。
一般情况下，在Python无法正常处理程序时就会发生一个异常。
当Python脚本发生异常时我们需要捕获处理它，否则程序会终止执行。
所有异常处理可以提高代码的稳健性。

```python
try:
	<语句>        # 运行别的代码
except <名字>：
	<语句>        # 如果在try部份引发了'name'异常
except <名字>，<数据>:
	<语句>        # 如果引发了'name'异常，获得附加的数据
else:
	<语句>        # 如果没有异常发生
```

你可以不带任何异常类型使用except捕获所有发生的异常。但这不是一个很好的方式，我们不能通过该程序识别出具体的异常信息。因为它捕获所有的异常。
你也可以使用相同的except语句来处理多个异常信息

```python
try:
	<语句>
finally:
	<语句>    # 无论是否发生异常都将执行
```

一个异常可以带上参数，可作为输出的异常信息参数

我们可以使用raise语句自己触发异常raise语法格式如下：
`raise [Exception [, args [, traceback]]]`

用户自定义异常

```python
class Networkerror(RuntimeError):
    def __init__(self, arg):
        self.args = arg
```

| 异常名称                  | 描述                                               |
| ------------------------- | -------------------------------------------------- |
| BaseException             | 所有异常的基类                                     |
| SystemExit                | 解释器请求退出                                     |
| KeyboardInterrupt         | 用户中断执行(通常是输入^C)                         |
| Exception                 | 常规错误的基类                                     |
| StopIteration             | 迭代器没有更多的值                                 |
| GeneratorExit             | 生成器(generator)发生异常来通知退出                |
| StandardError             | 所有的内建标准异常的基类                           |
| ArithmeticError           | 所有数值计算错误的基类                             |
| FloatingPointError        | 浮点计算错误                                       |
| OverflowError             | 数值运算超出最大限制                               |
| ZeroDivisionError         | 除(或取模)零 (所有数据类型)                        |
| AssertionError            | 断言语句失败                                       |
| AttributeError            | 对象没有这个属性                                   |
| EOFError                  | 没有内建输入,到达EOF 标记                          |
| EnvironmentError          | 操作系统错误的基类                                 |
| IOError                   | 输入/输出操作失败                                  |
| OSError                   | 操作系统错误                                       |
| WindowsError              | 系统调用失败                                       |
| ImportError               | 导入模块/对象失败                                  |
| LookupError               | 无效数据查询的基类                                 |
| IndexError                | 序列中没有此索引(index)                            |
| KeyError                  | 映射中没有这个键                                   |
| MemoryError               | 内存溢出错误(对于Python 解释器不是致命的)          |
| NameError                 | 未声明/初始化对象 (没有属性)                       |
| UnboundLocalError         | 访问未初始化的本地变量                             |
| ReferenceError            | 弱引用(Weak reference)试图访问已经垃圾回收了的对象 |
| RuntimeError              | 一般的运行时错误                                   |
| NotImplementedError       | 尚未实现的方法                                     |
| SyntaxError               | Python 语法错误                                    |
| IndentationError          | 缩进错误                                           |
| TabError                  | Tab 和空格混用                                     |
| SystemError               | 一般的解释器系统错误                               |
| TypeError                 | 对类型无效的操作                                   |
| ValueError                | 传入无效的参数                                     |
| UnicodeError              | Unicode 相关的错误                                 |
| UnicodeDecodeError        | Unicode 解码时的错误                               |
| UnicodeEncodeError        | Unicode 编码时错误                                 |
| UnicodeTranslateError     | Unicode 转换时错误                                 |
| Warning                   | 警告的基类                                         |
| DeprecationWarning        | 关于被弃用的特征的警告                             |
| FutureWarning             | 关于构造将来语义会有改变的警告                     |
| OverflowWarning           | 旧的关于自动提升为长整型(long)的警告               |
| PendingDeprecationWarning | 关于特性将会被废弃的警告                           |
| RuntimeWarning            | 可疑的运行时行为(runtime behavior)的警告           |
| SyntaxWarning             | 可疑的语法的警告                                   |
| UserWarning               | 用户代码生成的警告                                 |

### 文件和数据格式化

open() 方法用于打开一个文件，并返回文件对象。
在对文件进行处理过程都需要使用到这个函数，如果该文件无法被打开，会抛出 OSError。
注意：使用 open() 方法一定要保证关闭文件对象，即调用 close() 方法。

open(file, mode='r'[, buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None])

* file: 必需，文件路径（相对或者绝对路径）。
* mode: 可选，文件打开模式
* buffering: 设置缓冲
* encoding: 一般使用utf8
* errors: 报错级别
* newline: 区分换行符
* closefd: 传入的file参数类型
* opener: 设置自定义开启器，开启器的返回值必须是一个打开的文件描述符。

| 模式 | 描述                                                                                                                                                               |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| t    | 文本模式 (默认)。                                                                                                                                                  |
| x    | 写模式，新建一个文件，如果该文件已存在则会报错。                                                                                                                   |
| b    | 二进制模式。                                                                                                                                                       |
| +    | 打开一个文件进行更新(可读可写)。                                                                                                                                   |
| U    | 通用换行模式（**Python 3 不支持** ）。                                                                                                                       |
| r    | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。                                                                                                   |
| rb   | 以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。一般用于非文本文件如图片等。                                                           |
| r+   | 打开一个文件用于读写。文件指针将会放在文件的开头。                                                                                                                 |
| rb+  | 以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。一般用于非文本文件如图片等。                                                                         |
| w    | 打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。                                           |
| wb   | 以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。   |
| w+   | 打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。                                             |
| wb+  | 以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。     |
| a    | 打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。             |
| ab   | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
| a+   | 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。                                 |
| ab+  | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。                                             |

file.close()关闭文件。关闭后文件不能再进行读写操作。

file.flush()刷新文件内部缓冲，直接把内部缓冲区的数据立刻写入文件, 而不是被动的等待输出缓冲区写入。

file.fileno()返回一个整型的文件描述符(file descriptor FD 整型), 可以用在如os模块的read方法等一些底层操作上。

file.isatty()如果文件连接到一个终端设备返回 True，否则返回 False。

**file.read([size])**从文件读取指定的字节数，如果未给定或为负则读取所有。

file.readline([size])读取整行，包括 "\n" 字符。

file.readlines([sizeint])读取所有行并返回列表，若给定sizeint>0，返回总和大约为sizeint字节的行, 实际读取值可能比 sizeint 较大, 因为需要填充缓冲区。

file.seek(offset[, whence])移动文件读取指针到指定位置

file.tell()返回文件当前位置。

file.truncate([size])
从文件的首行首字符开始截断，截断文件为 size 个字符，无 size 表示从当前位置截断；截断之后后面的所有字符被删除，其中 windows 系统下的换行代表2个字符大小。

**file.write(str)**将字符串写入文件，返回的是写入的字符长度。

file.writelines(sequence)向文件写入一个序列字符串列表，如果需要换行则要自己加入每行的换行符。

```
fs=open('','w',encoding='utf8')
fs.write()
fs.close()

with open() as fs: //不需要close
```

#### 替换字符串

```

def alter(file,old_str,new_str):
    """
    替换文件中的字符串
    :param file:文件名
    :param old_str:就字符串
    :param new_str:新字符串
    :return:
    """
    file_data = ""
    with open(file, "r", encoding="utf-8") as f:
        for line in f:
            if old_str in line:
                line = line.replace(old_str,new_str)
            file_data += line
    with open(file,"w",encoding="utf-8") as f:
        f.write(file_data)
 
alter("file1", "09876", "python")


import os
def alter(file,old_str,new_str):
    """
    将替换的字符串写到一个新的文件中，然后将原文件删除，新文件改为原来文件的名字
    :param file: 文件路径
    :param old_str: 需要替换的字符串
    :param new_str: 替换的字符串
    :return: None
    """
    with open(file, "r", encoding="utf-8") as f1,open("%s.bak" % file, "w", encoding="utf-8") as f2:
        for line in f1:
            if old_str in line:
                line = line.replace(old_str, new_str)
            f2.write(line)
    os.remove(file)
    os.rename("%s.bak" % file, file)
 
alter("file1", "python", "测试")


import re,os
def alter(file,old_str,new_str):
 
    with open(file, "r", encoding="utf-8") as f1,open("%s.bak" % file, "w", encoding="utf-8") as f2:
        for line in f1:
            f2.write(re.sub(old_str,new_str,line))
    os.remove(file)
    os.rename("%s.bak" % file, file)
alter("file1", "admin", "password")

def alter(file,list_alter):
    file_data = ""
    with open(file, "r", encoding="utf-8") as f:
        for line in f:
            for i in range(len(list_alter[0])):
                if list_alter[0][i] in line:
                    line = line.replace(list_alter[0][i],list_alter[1][i])
            file_data += line
    return file_data

```

### 导入库

模块module：一个.py 文件就是个模块，由函数和类组成；
包package：多个模块放在一个文件夹，就是一个包；
库library：只是一个通俗的说法，平时说的库既可以是一个模块也可以是一个包 。

**直接导入库**：

```python
import math

print(math.sin(1))
```

*也可以导入库时起别名*：

```python
import math as m

print(m.sin(1))
```

**通过名称直接导入函数**：

```python
from math import sin as s, cos

print(s(1), cos(1))
```

**导入库中所有函数**：

```python
from math import *

print(sin(1))
```

如果需要导入自己的 `moduleA.py`模块，只需要 `import moduleA`，而不是 ~`import moduleA.py`~
为了便于导库，在写 `moduleA.py`时需要使用 `if __name__ == '__main__':`，如：

```python
a = 10
if __name__ == '__main__':
    print(a)
# 否则在另一个文件中导库时，会执行print(a)操作

# 为了形式简便，通常定义main函数
def main():
	a = 10
	print(a)
if __name__ == '__main__':
	main()
```

如果需要导入自己的 `packageA` 包中的  `moduleA.py` 模块可以使用 `import packageA.moduleA`
直接使用~`import packageA`~ 是无法识别的，需要定义一个 `__init__.py` 文件初始化

```python
# __init__.py
__version__ = '1.0.0'
__author__ = 'lain'

from . import moduleA

__all__ = ['moduleA']

# moduleA.py
print(10)

# main.py
import pacageA
```

## python标准

### python内置函数

Python 解释器自带的函数叫做内置函数，这些函数可以直接使用，不需要导入某个模块

#### 入门函数

**`input([prompt])`** 接受一个标准输入数据，返回为 string 类型

- prompt: 提示信息，可选

```python
name = input("请输入用户名")

a,b,c = (input("请输入三角形三边的长：").split()) # 因为是字符串类型，可以使用字符串分割函数
```

**`print(*objects, sep=' ', end='\n', file=None, flush=False)`** 将 objects 打印输出至 file 指定的文本流，以 sep 分隔并在末尾加上 end

- objects: 输出对象。可以一次输出多个对象，此时需要用 , 分隔 *如果没有给出 objects，将只写入 end*
- sep: 用来间隔多个对象，默认值是一个空格
- end: 用来设定以什么结尾，默认值是换行符 \n
- file: 要写入的文件对象 *file 参数必须是一个具有 write(string) 方法的对象；如果参数不存在或为 None，则将使用 sys.stdout*
- flush: 输出缓冲通常由 file 确定。 但是，如果 flush 为真值，流将被强制刷新

```python
a = 10
print('a+2=', a+2, sep='') # 控制台输出，设置没有间隔

with open('1.txt', 'a') as f:       # 打开文件
    print('hello world', file=f)    # 写入文件

from time import sleep
for i in range(10):
    print(i, end='', flush=True)    # 强制刷新流
    sleep(0.2)  
```

`help()`启动内置的帮助系统

#### 数学函数

sum()
max()
min()
divmod()

**`abs(x)`** 返回一个数的绝对值

- 参数可以是整数、浮点数或任何实现了 `__abs__()` 的对象。 如果参数是一个复数，则返回它的模。

```python
print(abs(-1.25))

print(abs(2+3j))

class Data:
    def __abs__(self):
        return 10
print(abs(Data()))
```

pow()
round()

#### 数据类型函数

int()
str()
bool()
float()
tuple()
list()
dict()
set()

#### 序列迭代器函数

len()
slice()
sorted()
reverse()
filter()
all()
any()
iter()
next()
range()
enumerate()
zip()
map()

#### 对象函数

id()
type()
isinstance()
issubclass()
staticmethod()
super()

#### 对象操作函数

format()
repr()
eval()
exec()
open()

#### 对象属性函数

setattr()
getattr()
hasattr()
delattr()
property()
vars()

### python标准库

**文本**
string：通用字符串操作
re：正则表达式操作
difflib：差异计算工具
textwrap：文本填充
unicodedata：Unicode字符数据库
stringprep：互联网字符串准备工具
readline：GNU按行读取接口
rlcompleter：GNU按行读取的实现函数
struct：将字节解析为打包的二进制数据
codecs：注册表与基类的编解码器
**数据类型**
datetime：基于日期与时间工具
calendar：通用月份函数
collections：容器数据类型
collections.abc：容器虚基类
heapq：堆队列算法
bisect：数组二分算法
array：高效数值数组
weakref：弱引用
types：内置类型的动态创建与命名
copy：浅拷贝与深拷贝
reprlib：交替repr()的实现
**数学**
numbers：数值的虚基类
math：数学函数
cmath：复数的数学函数
decimal：定点数与浮点数计算
fractions：有理数
random：生成伪随机数
**函数式编程**
itertools：为高效循环生成迭代器
functools：可调用对象上的高阶函数与操作
operator：针对函数的标准操作
**文件与目录**
os.path：通用路径名控制
fileinput：从多输入流中遍历行
stat：解释stat()的结果
filecmp：文件与目录的比较函数
tempfile：生成临时文件与目录
glob：Unix风格路径名格式的扩展
fnmatch：Unix风格路径名格式的比对
linecache：文本行的随机存储
shutil：高级文件操作
macpath：MacOS 9路径控制函数
**持久化**
pickle：Python对象序列化
copyreg：注册机对pickle的支持函数
shelve：Python对象持久化
marshal：内部Python对象序列化
dbm：Unix“数据库”接口
sqlite3：针对SQLite数据库的API2.0
**压缩**
zlib：兼容gzip的压缩
gzip：对gzip文件的支持
bz2：对bzip2压缩的支持
lzma：使用LZMA算法的压缩
zipfile：操作ZIP存档
tarfile：读写tar存档文件
**加密**
hashlib：安全散列与消息摘要
hmac：针对消息认证的键散列
**操作系统工具**
os：多方面的操作系统接口
io：流核心工具
time：时间的查询与转化
argparser：命令行选项、参数和子命令的解析器
optparser：命令行选项解析器
getopt：C风格的命令行选项解析器
logging：Python日志工具
logging.config：日志配置
logging.handlers：日志处理器
getpass：简易密码输入
curses：字符显示的终端处理
curses.textpad：curses程序的文本输入域
curses.ascii：ASCII字符集工具
curses.panel：curses的控件栈扩展
platform：访问底层平台认证数据
errno：标准错误记号
ctypes：Python外部函数库
**并发**
threading：基于线程的并行
multiprocessing：基于进程的并行
concurrent：并发包
concurrent.futures：启动并行任务
subprocess：子进程管理
sched：事件调度
queue：同步队列
select：等待I / O完成
dummy_threading：threading模块的替代（当_thread不可用时）
_ thread：底层的线程API（threading基于其上）
_ dummy_thread：_ thread模块的替代（当_thread不可用时）
**进程间通信**
socket：底层网络接口
ssl：socket对象的TLS / SSL填充器
asyncore：异步套接字处理器
asynchat：异步套接字命令 / 响应处理器
signal：异步事务信号处理器
mmap：内存映射文件支持
**互联网**
email：邮件与MIME处理包
json：JSON编码与解码
mailcap：mailcap文件处理
mailbox：多种格式控制邮箱
mimetypes：文件名与MIME类型映射
base64：RFC3548：Base16、Base32、Base64编码
binhex：binhex4文件编码与解码
binascii：二进制码与ASCII码间的转化
quopri：MIMEquoted - printable数据的编码与解码
uu：uuencode文件的编码与解码
**互联网协议与支持**
webbrowser：简易Web浏览器控制器
cgi：CGI支持
cgitb：CGI脚本反向追踪管理器
wsgiref：WSGI工具与引用实现
urllib：URL处理模块
urllib.request：打开URL连接的扩展库
urllib.response：urllib模块的响应类
urllib.parse：将URL解析成组件
urllib.error：urllib.request引发的异常类
urllib.robotparser：robots.txt的解析器
http：HTTP模块
http.client：HTTP协议客户端
ftplib：FTP协议客户端
poplib：POP协议客户端
imaplib：IMAP4协议客户端
nntplib：NNTP协议客户端
smtplib：SMTP协议客户端
smtpd：SMTP服务器
telnetlib：Telnet客户端
uuid：RFC4122的UUID对象
socketserver：网络服务器框架
http.server：HTTP服务器
http.cookies：HTTPCookie状态管理器
http.cookiejar：HTTP客户端的Cookie处理
xmlrpc：XML - RPC服务器和客户端模块
xmlrpc.client：XML - RPC客户端访问
xmlrpc.server：XML - RPC服务器基础
ipaddress：IPv4 / IPv6控制库
**多媒体**
audioop：处理原始音频数据
aifc：读写AIFF和AIFC文件
sunau：读写Sun AU文件
wave：读写WAV文件
chunk：读取IFF大文件
colorsys：颜色系统间转化
imghdr：指定图像类型
sndhdr：指定声音文件类型
ossaudiodev：访问兼容OSS的音频设备
**国际化**
gettext：多语言的国际化服务
locale：国际化服务
**编程框架**
turtle：Turtle图形库
cmd：基于行的命令解释器支持
shlex：简单词典分析
**Tk图形用户接口**
tkinter：Tcl / Tk接口
tkinter.ttk：Tk主题控件
tkinter.tix：Tk扩展控件
tkinter.scrolledtext：滚轴文本控件
**开发工具**
pydoc：文档生成器和在线帮助系统
doctest：交互式Python示例
unittest：单元测试框架
unittest.mock：模拟对象库
test：Python回归测试包
test.support：Python测试工具套件
venv：虚拟环境搭建
**调试**
bdb：调试框架
faulthandler：Python反向追踪库
pdb：Python调试器
timeit：小段代码执行时间测算
trace：Python执行状态追踪
**运行时**
sys：系统相关的参数与函数
sysconfig：访问Python配置信息
builtins：内置对象
main：顶层脚本环境
warnings：警告控制
contextlib：with状态的上下文工具
abc：虚基类
atexit：出口处理器
traceback：打印或读取一条栈的反向追踪
future：未来状态定义
gc：垃圾回收接口
inspect：检查存活的对象
site：址相关的配置钩子（hook）
fpectl：浮点数异常控制
distutils：生成和安装Python模块
**解释器**
code：基类解释器
codeop：编译Python代码
**导入模块**
imp：访问import模块的内部
zipimport：从ZIP归档中导入模块
pkgutil：包扩展工具
modulefinder：通过脚本查找模块
runpy：定位并执行Python模块
importlib：import的一种实施
Python语言
parser：访问Python解析树
ast：抽象句法树
symtable：访问编译器符号表
symbol：Python解析树中的常量
token：Python解析树中的常量
keyword：Python关键字测试
tokenize：Python源文件分词
tabnany：模糊缩进检测
pyclbr：Python类浏览支持
py_compile：编译Python源文件
compileall：按字节编译Python库
dis：Python字节码的反汇编器
pickletools：序列化开发工具
**其他**
formatter：通用格式化输出
Windows相关
msilib：读写Windows的Installer文件
msvcrt：MS VC + + Runtime的有用程序
winreg：Windows注册表访问
winsound：Windows声音播放接口
Unix相关
posix：最常用的POSIX调用
pwd：密码数据库
spwd：影子密码数据库
grp：组数据库
crypt：Unix密码验证
termios：POSIX风格的tty控制
tty：终端控制函数
pty：伪终端工具
fcntl：系统调用fcntl()和ioctl()
pipes：shell管道接口
resource：资源可用信息
nis：Sun的NIS的接口
syslog：Unix 日志服务

#### random（随机）

seed()随机数种子、random()生成一个0到~1~的随机符点数、randint()生成一个指定范围内的整数、getrandbits()生成一个k比特长的随机整数、randrange()从指定范围内，按指定基数递增的整数集合中 获取一个随机数、uniform()生成一个指定范围内的随机符点数、choice()从序列中获取一个随机元素、shuffle()将一个列表中的元素打乱、sample()从指定序列中随机获取指定长度的片断

| 方法                                                                                 | 描述                                                                                                                                                                                                         |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [seed()](https://www.runoob.com/python3/python3-func-number-seed.html)                  | 初始化随机数生成器                                                                                                                                                                                           |
| getstate()                                                                           | 返回捕获生成器当前内部状态的对象。                                                                                                                                                                           |
| setstate()                                                                           | state 应该是从之前调用 getstate() 获得的，并且 setstate() 将生成器的内部状态恢复到 getstate() 被调用时的状态。                                                                                               |
| getrandbits(k)                                                                       | 返回具有 k 个随机比特位的非负 Python 整数。 此方法随 MersenneTwister 生成器一起提供，其他一些生成器也可能将其作为 API 的可选部分提供。 在可能的情况下，getrandbits() 会启用 randrange() 来处理任意大的区间。 |
| [randrange()](https://www.runoob.com/python3/ref-random-randrange.html)                 | 从 range(start, stop, step) 返回一个随机选择的元素。                                                                                                                                                         |
| [randint(a, b)](https://www.runoob.com/python3/ref-random-randint.html)                 | 返回随机整数 N 满足 a <= N <= b。                                                                                                                                                                            |
| [choice(seq)](https://www.runoob.com/python3/python3-func-number-choice.html)           | 从非空序列 seq 返回一个随机元素。 如果 seq 为空，则引发 IndexError。                                                                                                                                         |
| choices(population, weights=None, *, cum_weights=None, k=1)                          | 从 population 中选择替换，返回大小为 k 的元素列表。 如果 population 为空，则引发 IndexError。                                                                                                                |
| [shuffle(x[, random])](https://www.runoob.com/python3/python3-func-number-shuffle.html) | 将序列 x 随机打乱位置。                                                                                                                                                                                      |
| sample(population, k, *, counts=None)                                                | 返回从总体序列或集合中选择的唯一元素的 k 长度列表。 用于无重复的随机抽样。                                                                                                                                   |
| [random()](https://www.runoob.com/python3/python3-func-number-random.html)              | 返回 [0.0, 1.0) 范围内的下一个随机浮点数。                                                                                                                                                                   |
| [uniform()](https://www.runoob.com/python3/python3-func-number-uniform.html)            | 返回一个随机浮点数 N ，当 a <= b 时 a <= N <= b ，当 b < a 时 b <= N <= a 。                                                                                                                                 |
| triangular(low, high, mode)                                                          | 返回一个随机浮点数 N ，使得 low <= N <= high 并在这些边界之间使用指定的 mode 。 low 和 high 边界默认为零和一。 mode 参数默认为边界之间的中点，给出对称分布。                                                 |
| betavariate(alpha, beta)                                                             | Beta 分布。 参数的条件是 alpha > 0 和 beta > 0。 返回值的范围介于 0 和 1 之间。                                                                                                                              |
| expovariate(lambd)                                                                   | 指数分布。 lambd 是 1.0 除以所需的平均值，它应该是非零的。                                                                                                                                                   |
| gammavariate()                                                                       | Gamma 分布（ 不是伽马函数） 参数的条件是 alpha > 0 和 beta > 0。                                                                                                                                             |
| gauss(mu, sigma)                                                                     | 正态分布，也称高斯分布。 mu 为平均值，而 sigma 为标准差。 此函数要稍快于下面所定义的 normalvariate() 函数。                                                                                                  |
| lognormvariate(mu, sigma)                                                            | 对数正态分布。 如果你采用这个分布的自然对数，你将得到一个正态分布，平均值为 mu 和标准差为 sigma 。 mu 可以是任何值，sigma 必须大于零。                                                                       |
| normalvariate(mu, sigma)                                                             | 正态分布。 mu 是平均值，sigma 是标准差。                                                                                                                                                                     |
| vonmisesvariate(mu, kappa)                                                           | 冯·米塞斯分布。 mu 是平均角度，以弧度表示，介于0和 2*pi 之间，kappa 是浓度参数，必须大于或等于零。 如果 kappa 等于零，则该分布在 0 到 2*pi 的范围内减小到均匀的随机角度。                                 |
| paretovariate(alpha)                                                                 | 帕累托分布。 alpha 是形状参数。                                                                                                                                                                              |
| weibullvariate(alpha, beta)                                                          | 威布尔分布。 alpha 是比例参数，beta 是形状参数。                                                                                                                                                             |

#### time（时间）

time库是Python中处理时间的标准库;提供获取系统时间并格式化输出功能;提供系统级精确计时功能，用于程序性能分析

* 时间处理函数：time()、gmtime()、localtime()、ctime()
* 时间格式化函数：mktime()、strftime()、strptime()
* 计时函数：sleep()、perf_counter()

1.时间获取：
（1）time函数
获取当前时间戳（从世界标准时间的1970年1月1日00：00：00开始到当前这一时刻为止的总秒数），即计算机内部时间值，浮点数。

（2）localtime（）函数和gmtime()函数
Python提供了可以获取结构化时间的localtime（）函数和gmtime函数

获取当前时间，表示为计算机可处理的时间格式（struct_time格式）

localtime()函数和gmtime()函数都可将时间戳转换为以元组表示的时间对象（struct_time格式)，但是localtime()函数得到的是当地时间，gmtime()函数得到的是世界统一时间。

格式如下所示：

localtime([secs])

gmtime([secs])

其中secs是一个表示时间戳的浮点数，若不提供该参数，默认以time（）函数获取的时间戳作为参数。

（3）ctime（）函数（与asctime（）函数为一对互补函数）
读取当前时间并以易读方式表示，返回字符串。

ctime（）函数用于将一个时间戳（以s为单位的浮点数）转换为“Sat Jan 13 21:56:34 2018"这种形式（若该函数未收到参数，则默认以time.time()作为参数），转换成的形式为”星期 月份 当月号 时分秒 年份“。

 时间格式化：
将时间以合理的方式展示出来

格式化：类似字符串格式化，需要有展示模板

展示模板由特定的格式化控制符组成

（1）strftime（）函数（将时间格式输出为字符串，与strptime函数互补）。strftime(格式，时间 )主要决定时间的输出格式
strftime()函数借助时间格式控制符来输出格式化的时间字符串，其中%a,%d,%b等是time库预定义的用于控制不同时间或时间成分的格式控制符。

    time库中常用的时间格式控制符及其说明如下所示

时间格式控制符	说明
%Y	四位数的年份，取值范围为0001~9999,如1900
%m	月份（01~12），例如10
%d	月中的一天（01~31）例如：25
%B	本地完整的月份名称，比如January
%b	本地简化的月份名称，比如Jan
%a	本地简化的周日期，Mon~Sun,例如Wed
%A	本地完整周日期，”Monday~Sunday,例如Wednesday
%H	24小时制小时数（00~23),例如：12
%l	12小时制小时数（01~12），例如：7
%p	上下午，取值为AM或PM
%M	分钟数（00~59），例如26
%S	秒（00~59），例如26
strftime()函数有两条参数，其中一个为tpl(格式化的模板字符串参数，用来定义输出效果），另一个为ts(是计算机内部时间类型变量）

（2）strptime()函数，strptime(字符串，格式），主要将该格式的字符串输出为struct_time.
strptime(str,tpl)tpl(是格式化模板字符串，用来定义输入效果）

str是字符串形式的时间值，所以他的格式为前面为字符串，后面为字符串的格式，然后输出的格式为struct_time。
在对时间的理解上，我们可以这样认为：在计算机中为了表达时间，它其实只有一个浮点数，前面提到的这个浮点数是从1970年1月1日开始的，然后为了让其他的程序能够更好的处理这个浮点数，我们把它定义一个程序能够理解的格式，这个格式就是用gmtime来获取的struct_time格式。

struct_time格式，它包含了许多元素，这些元素的值都是通过浮点数来提供的。

反过来，我们也可以使用一个字符串赋予一个时间给我们的strptime类型，然后并由这个类型进一步生成浮点数。

程序计时：
程序计时应用广泛

程序计时指测量起止动作所经历时间的过程

测量时间指的是能够记录时间的流逝: perf_counter()获取计算机中CPU也就是中央处理器以其频率运行的时钟纳秒计算，非常精确。

产生时间函数:sleep

让程序去休眠或者产生一定的时间

perf_counter()返回一个CPU级别的精确时间计数值，单位为秒，由于这个计数值起点不确定，连续调用差值才有意义

sleep（s)  s拟休眠的时间，单位是秒，可以是浮点数

#### re（正则表达式）

[[../../其他语法/正则表达式|正则表达式]]是一个特殊的字符序列，它能帮助你方便的检查一个字符串是否与某种模式匹配。
Python 自1.5版本起增加了re 模块，它提供 Perl 风格的正则表达式模式。

`re.match(pattern, string, flags=0)`
 尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，match() 就返回 none

 `re.search(pattern, string, flags=0)`
 扫描整个字符串并返回第一个成功的匹配

- pattern	匹配的正则表达式
- string	要匹配的字符串。
- flags	标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等

`re.sub(pattern, repl, string, count=0, flags=0)`
替换字符串中的匹配项

- pattern : 正则中的模式字符串。
- repl : 替换的字符串，也可为一个函数。
- string : 要被查找替换的原始字符串。
- count : 模式匹配后替换的最大次数，默认 0 表示替换所有的匹配。

`re.compile(pattern[, flags])`
用于编译正则表达式，生成一个正则表达式（ Pattern ）对象，可以给 match() 、 search() 以及 findall 等函数使用。

- pattern : 一个字符串形式的正则表达式
- flags : 可选，表示匹配模式，比如忽略大小写，多行模式等，具体参数为：

`re.findall(string[, pos[, endpos]])`
在字符串中找到正则表达式所匹配的所有子串，并返回一个列表，如果有多个匹配模式，则返回元组列表，如果没有找到匹配的，则返回空列表。
**注意：** match 和 search 是匹配一次，findall 是匹配所有。

- string : 待匹配的字符串。
- pos : 可选参数，指定字符串的起始位置，默认为 0。
- endpos : 可选参数，指定字符串的结束位置，默认为字符串的长度。

`re.finditer(pattern, string, flags=0)`
和 findall 类似，在字符串中找到正则表达式所匹配的所有子串，并把它们作为一个迭代器返回

`re.split(pattern, string[, maxsplit=0, flags=0])`
split 方法按照能够匹配的子串将字符串分割后返回列表

- pattern	匹配的正则表达式
- string	要匹配的字符串。
- maxsplit	分隔次数，maxsplit=1 分隔一次，默认为 0，不限制次数。
- flags	标志位，用于控制正则表达式的匹配方式

| flags修饰符 | 描述                                                           |
| ----------- | -------------------------------------------------------------- |
| re.I        | 使匹配对大小写不敏感                                           |
| re.L        | 做本地化识别（locale-aware）匹配                               |
| re.M        | 多行匹配，影响 ^ 和 $                                          |
| re.S        | 使 . 匹配包括换行在内的所有字符                                |
| re.U        | 根据Unicode字符集解析字符。这个标志影响 \w, \W, \b, \B.        |
| re.X        | 该标志通过给予你更灵活的格式以便你将正则表达式写得更易于理解。 |

#### turtle（绘图）

*想象有一只海龟在窗体正中心，在画布上游走，走过的轨迹形成了绘制的图形，海龟由程序控制，可以自由改变颜色、方向宽度等*
使用 turtle 之前需要先在代码的最前面导入turtle这个模块。为了让完成绘图后画布不消失，需要在程序的最后添加 turtle.mainloop()

```python
# 导入turtle
import turtle  

# (--------中间写绘图过程----------)

# 让画布一直存在，这句代码需要放在最后
turtle.mainloop()
```

**画布**：

> `turtle.screensize(canvwidth=None, canvheight=None, bg=None)` 画布的宽(单位像素), 高, 背景颜色
> `turtle.setup(宽度, 高度)` - 设置画布的宽度和高度
> width, height: 输入宽和高为整数时, 表示像素; 为小数时, 表示占据电脑屏幕的比例
> (startx, starty): 这一坐标表示 矩形窗口左上角顶点的位置, 如果为空,则窗口位于屏幕中心
> `turtle.title(标题)` - 设置标题
>
> `turtle.clear()`清空turtle窗口，但是turtle的位置和状态不会改变;`turtle.reset()`清空窗口，重置turtle状态为起始状态

```python
turtle.setup(800, 600)
turtle.title('hello')
```

**设置画笔**：

> `turtle.pencolor(颜色)` - 设置画笔画出的线的颜色（颜色名称如'red' 或 HEX颜色如'#555' 或RGB颜色元组如(0.2, 0.8, 0.55)）
> `turtle.width(线宽)` - 设置线宽
> `turtle.speed(速度值)` - 设置笔移动的速度（速度值是1-10逐渐变快，0速度最大。如果数字大于10或小于0.5，则设置为0）
> `turtle.hideturtle()` - 隐藏箭头显示 `turtle.showturtle()`

*画笔对应的光标默认是在画布的中心，方向默认是水平向右。*

**控制笔移动**：

> `turtle.forward(距离) / turtle.fd(距离)` - 控制笔前进指定距离
> `turtle.back(距离)/turtle.bk(距离)` - 控制笔后退指定距离
> `turtle.goto(x坐标, y坐标)/ turtle.setx(x坐标) / turtle.sety(y坐标)` - 控制笔移动到指定位置（坐标原点在画布的中心）
> `turtle.home()` - 笔回到初始状态（回到初始位置和初始方向）

**控制笔的方向**：

笔的方向默认水平向右，所以前进的时候笔是往右移动的，后退笔向左移动。在移动之前改变笔的方向，前进和后退的代码就会改变移动轨迹。

> `turtle.left(角度)` - 向左旋转指定角度lt
> `turtle.right(角度)` - 向右旋转指定角度rt
> `turtle.setheading(角度)` - 设置绝对角度值指定度数seth

**抬起笔和放下笔**：

有的时候移动笔不需要在画布上留下痕迹，那在移动笔之前需要先抬起笔。

> `turtle.up()` - 抬起笔
> `turtle.down()` - 放下笔

**画圆**：

1.画圆环

`turtle.circle(半径, [角度/多边形边数])` - 画完整的圆/指定角度对应的圆弧/圆正切内多边形
当半径值为正数时，圆心在当前位置/小海龟左侧；当角度值为正数时，顺小海龟当前方向绘制

2.画实心圆

`turtle.dot(直径, 颜色)` - 直径为指定值的画实心圆

**填充**：

在使用填充的时候需要注意，写代码的时候先写需要填充的轮廓对应的代码。再在轮廓代码前面开始填充，轮廓代码的后面结束填充。

> `turtle.fillcolor(颜色)` - 设置填充颜色
> `turtle.begin_fill()` - 开始填充
> `turtle.end_fill()` - 结束填充

```python
# 设置填充颜色
turtle.fillcolor('orange')
# 开始填充
turtle.begin_fill()

# ========以下代码是画需要填充的轮廓对应的代码（一个三角形）========
turtle.width(3)
turtle.forward(200)
turtle.left(120)
turtle.forward(120)
turtle.home()
# ==========================================================

# 结束填充
turtle.end_fill()
```

**文字**：

> `turtle.write(文字内容, font=(字体名称, 字体大小, 文字类型))`

```python
# 字体类型：normal、bold、italic
turtle.pencolor('pink')
turtle.write('你输入的文字', font=('宋体', 40, 'bold'))
```

#### tkinter（UI）

Tkinter： Tkinter 模块(Tk 接口)是 Python 的标准 Tk GUI 工具包的接口.

创建一个GUI程序:
1、导入 Tkinter 模块(import tkinter或from tkinter import *，前者需要使用 `tkinter.Tk()`，后者只需要 `Tk()`)
2、创建控件
3、指定这个控件的 master， 即这个控件属于哪一个
4、告诉 GM(geometry manager) 有一个控件产生了。

```python
from tkinter import *   # 导库

window = Tk()   # 创建窗口
window.title('标题') # 指定窗口标题
window.geometry('300x200+100+100')    # 窗口的宽度为300像素，高度为200像素，并将窗口的左上角坐标设定为(100, 100)
# 如果需要将窗口打开在屏幕的特定位置，可以使用winfo_screenwidth和winfo_screenheight方法来确定屏幕的宽度和高度:
# screen_width = window.winfo_screenwidth()
# screen_height = window.winfo_screenheight()
# window_width = 300
# window_height = 200
# x_position = int((screen_width/2) - (window_width/2))
# y_position = int((screen_height/2) - (window_height/2))
# window.geometry(f"{window_width}x{window_height}+{x_position}+{y_position}")

window.mainloop()   # 进入消息循环

# window.destroy() # 删除窗口
```

##### tkinter 组件

|     控件     | 功能                                                          |
| :----------: | ------------------------------------------------------------- |
|    Button    | 按钮控件；在程序中显示按钮。                                  |
|    Canvas    | 画布控件；显示图形元素如线条或文本                            |
| Checkbutton | 多选框控件；用于在程序中提供多项选择框                        |
|    Entry    | 输入控件；用于显示简单的文本内容                              |
|    Frame    | 框架控件；在屏幕上显示一个矩形区域，多用来作为容器            |
|    Label    | 标签控件；可以显示文本和位图                                  |
|   Listbox   | 列表框控件；在Listbox窗口小部件是用来显示一个字符串列表给用户 |
|  Menubutton  | 菜单按钮控件，用于显示菜单项。                                |
|     Menu     | 菜单控件；显示菜单栏,下拉菜单和弹出菜单                       |
|   Message   | 消息控件；用来显示多行文本，与label比较类似                   |
| Radiobutton | 单选按钮控件；显示一个单选的按钮状态                          |
|    Scale    | 范围控件；显示一个数值刻度，为输出限定范围的数字区间          |
|  Scrollbar  | 滚动条控件，当内容超过可视化区域时使用，如列表框。.           |
|     Text     | 文本控件；用于显示多行文本                                    |
|   Toplevel   | 容器控件；用来提供一个单独的对话框，和Frame比较类似           |
|   Spinbox   | 输入控件；与Entry类似，但是可以指定输入范围值                 |
| PanedWindow | 一个窗口布局管理的插件，可以包含一个或者多个子控件。          |
|  LabelFrame  | 一个简单的容器控件。常用于复杂的窗口布局。                    |
| tkMessageBox | 用于显示你应用程序的消息框。                                  |

---

**标准属性**:所有控件的共同属性

|   属性   | 描述     |
| :-------: | -------- |
| Dimension | 控件大小 |
|   Color   | 控件颜色 |
|   Font   | 控件字体 |
|  Anchor  | 锚点     |
|  Relief  | 控件样式 |
|  Bitmap  | 位图     |
|  Cursor  | 光标     |

---

**几何管理**:Tkinter控件有特定的几何状态管理方法，管理整个控件区域组织

| 几何方法 | 描述 |
| -------- | ---- |
| grid()   | 网格 |
| pack()   | 包装 |
| place()  | 位置 |

```python
#几何管理器(1)-----网格管理器
'''
网格管理器将小构件，放在一个不可见网格的每个单元内。可以将小构件放在某个特定的行和列内，也可以使
用rowspan和columnspan参数将小构件放在多行和多列中。
'''

from tkinter import *

class GridManagerDemo:
    window = Tk()
    window.title("Grid Manager Demo")

    message = Message(window, text = "This Message widget occupies three rows and two columns")
    message.grid(row = 1, column = 1, rowspan = 3, columnspan = 2)

    Label(window, text = "First Name:").grid(row = 1, column = 3)
    Entry(window).grid(row = 1, column = 4, padx = 5, pady = 5)

    Label(window, text = "Last Name:").grid(row = 2, column = 3)
    Entry(window).grid(row = 2, column = 4)

    Button(window, text = "Get Name").grid(row = 3, padx = 5, pady = 5,column = 4, sticky = E)

    window.mainloop()

GridManagerDemo()
```

```python
#几何管理器(2)-----包管理器
'''
包含管理器将小构件依次的一个放置在另一个的顶部或将他们一个挨着一个的放置。
'''

#第一种
from tkinter import *

class PackManagerDemo:
    def __init__(self):
        window = Tk()
        window.title("Pack Mananger Demo 1")

        Label(window, text = "Blue", bg="blue").pack()
        # fill通过X，Y，BOTH 来填充水平，垂直，或者两个方向的空间
        #expand告诉管理器分配额外的空间给小构件
        Label(window, text = "Red", bg = "red").pack(fill = BOTH, expand = 1)
        Label(window, text = "Green", bg = "green").pack(fill = BOTH)

        window.mainloop()

PackManagerDemo()

#第二种
class PackManagerDemoWithSide:
    window = Tk()
    window.title("Pack Manager Demo 2")

    #side可以是LEFT, RIGHT, TOP, BOTTOM,默认是TOP。
    Label(window, text = "Blue", bg="blue").pack(side = LEFT)
    Label(window, text = "Red", bg = "red").pack(side = LEFT, fill = BOTH, expand = 1)
    Label(window, text = "Green", bg = "green").pack(side = LEFT, fill = BOTH)

    window.mainloop()
  
PackManagerDemoWithSide()
```

```python
#几何管理器(3)-----位置管理器
'''
位置管理器将小构件放在绝对位置上。
'''

from tkinter import *

class PlaceManagerDemo:
    def __init__(self):
        window = Tk()
        window.title("Place Manager Demo")

        Label(window, text = "Blue", bg = "blue").place(x = 20, y = 20)
        Label(window, text = "Red", bg = "red").place(x = 50, y = 50)
        Label(window, text = "Green", bg = "green").place(x = 80, y = 80)

        window.mainloop()

PlaceManagerDemo()
```

###### Button

`w = Button ( master, option=value, ... )`

- master: 按钮的父容器。
- options: 可选项，即该按钮的可设置的属性。这些选项可以用键 = 值的形式设置，并以逗号分隔。

| 序号 | 可选项 & 描述                                                                                          |
| ---- | :----------------------------------------------------------------------------------------------------- |
| 1    | **activebackground**当鼠标放上去时，按钮的背景色                                                 |
| 2    | **activeforeground**当鼠标放上去时，按钮的前景色                                                 |
| 3    | **bd**按钮边框的大小，默认为 2 个像素                                                            |
| 4    | **bg**按钮的背景色                                                                               |
| 5    | **command**按钮关联的函数，当按钮被点击时，执行该函数                                            |
| 6    | **fg**按钮的前景色（按钮文本的颜色）                                                             |
| 7    | **font**文本字体                                                                                 |
| 8    | **height**按钮的高度                                                                             |
| 9    | **highlightcolor**要高亮的颜色                                                                   |
| 10   | **image**按钮上要显示的图片                                                                      |
| 11   | **justify**显示多行文本的时候,设置不同行之间的对齐方式，可选项包括LEFT, RIGHT, CENTER            |
| 12   | **padx**按钮在x轴方向上的内边距(padding)，是指按钮的内容与按钮边缘的距离                         |
| 13   | **pady**按钮在y轴方向上的内边距(padding)                                                         |
| 14   | **relief**边框样式，设置控件3D效果，可选的有：FLAT、SUNKEN、RAISED、GROOVE、RIDGE。默认为 FLAT。 |
| 15   | **state**设置按钮组件状态,可选的有NORMAL、ACTIVE、 DISABLED。默认 NORMAL。                       |
| 16   | **underline**下划线。默认按钮上的文本都不带下划线。取值就是带下划线的字符串索引                  |
| 17   | **width**按钮的宽度，如未设置此项，其大小以适应按钮的内容（文本或图片的大小）                    |
| 18   | **wraplength**限制按钮每行显示的字符的数量                                                       |
| 19   | **text**按钮的文本内容                                                                           |
| 19   | **anchor**锚选项，控制文本的位置，默认为中心                                                     |

|    方法    | 描述                                                                     |
| :--------: | ------------------------------------------------------------------------ |
| deselect() | 清除单选按钮的状态                                                       |
|  flash()  | 在激活状态颜色和正常颜色之间闪烁几次单选按钮，但保持它开始时的状态。     |
|  invoke()  | 可以调用此方法来获得与用户单击单选按钮以更改其状态时发生的操作相同的操作 |
|  select()  | 设置单选按钮为选中。                                                     |

```python
import tkinter
 
window = tkinter.Tk()
 
B = tkinter.Button(window, activebackground = '#008000', activeforeground = '#FF0000', bd = 4, bg = '#7FFFD4', command = window.quit, fg = '#800080', text ="退出", underline = 0)
B.pack()
window.mainloop()
```

**如果需要给 `command`中的函数传参：**
可以使用 `partial`封装

```python
from tkinter import *
from functools import partial

a = 10

def f(x):
    print(x)
 
window = Tk()
Button(window, command = partial(f, a), text = '打印a').pack()
window.mainloop()
```

###### Canvas

`w = Canvas ( master, option=value, ... )`

- master: 按钮的父容器。
- options: 可选项，即该按钮的可设置的属性。这些选项可以用键 = 值的形式设置，并以逗号分隔。

| 序号 | 可选项 & 描述                                                                                                         |
| ---- | --------------------------------------------------------------------------------------------------------------------- |
| 1    | **bd**边框宽度，单位像素，默认为 2 像素。                                                                       |
| 2    | **bg**背景色                                                                                                    |
| 3    | **confine**如果为 true (默认), 画布不能滚动到可滑动的区域外。                                                   |
| 4    | **cursor**光标的形状设定，如arrow, circle, cross, plus 等                                                       |
| 5    | **height**高度                                                                                                  |
| 6    | **highlightcolor**要高亮的颜色                                                                                  |
| 7    | **relief**边框样式,可选值为 FLAT、SUNKEN、RAISED、GROOVE、RIDGE。 默认为 FLAT。                                 |
| 8    | **scrollregion**一个元组tuple(w, n, e, s)，定义了画布可滚动的最大区域，w 为左边，n 为头部，e 为右边，s 为底部。 |
| 9    | **width**画布在 X 坐标轴上的大小。                                                                              |
| 10   | **xscrollincrement**用于滚动请求水平滚动的数量值。                                                              |
| 11   | **xscrollcommand**水平滚动条，如果画布是可滚动的，则该属性是水平滚动条的 .set（）方法。                         |
| 12   | **yscrollincrement**类似 xscrollincrement, 但是垂直方向。                                                       |
| 13   | **yscrollcommand**垂直滚动条，如果画布是可滚动的，则该属性是垂直滚动条的 .set（）方法。                         |

**Canvas 组件支持以下标准选项：**

arc − 创建一个扇形

```py
coord =10,50,240,210
arc = canvas.create_arc(coord, start=0, extent=150, fill="blue")
```

image − 创建图像

```py
filename =PhotoImage(file ="sunshine.gif")
image = canvas.create_image(50,50, anchor=NE, image=filename)
```

line − 创建线条

```py
line = canvas.create_line(x0, y0, x1, y1,..., xn, yn, options)
```

oval − 创建一个圆

```py
oval = canvas.create_oval(x0, y0, x1, y1, options)
```

polygon − 创建一个至少有三个顶点的多边形

```py
oval = canvas.create_polygon(x0, y0, x1, y1,...xn, yn, options)
```

#### urllib（爬虫）

Python urllib 库用于操作网页 URL，并对网页的内容进行抓取处理。

- urllib.request - 打开和读取 URL。
- urllib.error - 包含 urllib.request 抛出的异常。
- urllib.parse - 解析 URL。
- urllib.robotparser - 解析 robots.txt 文件。

使用封装好的[[#requests|request库]]更方便
具体应用参考[[../../../计算机安全/网络安全/Python网络爬虫|Python网络爬虫]]

urllib.request：

rs = urllib.request.urlopen('http://www.baidu.com')
print(type(rs))
HTTPResponse类型
con = response.read(5)
读5个字节
con1 = response.readline()
读取一行
con2 = response.readlines()
按行读

print(response.getcode())
返回状态码（200正确）
print(response.geturl())
返回url地址
print(response.getheaders())
返回响应头

下载网页、图片、视频
urllib.request.urlretrieve(url='文件url地址',filename='保存路径')

#### SQLite3（数据库）

SQLite 是一个用 C 语言编写的小巧嵌入式数据库，它的数据库就是一个文件，不需要单独的服务器进程或操作系统，不需要配置

[[../../其他语法/数据库查询语言|SQL语法]]

```python
import sqlite3 # 导入sqlite3模块

# 创建与数据库的连接，返回一个Connection对象与数据库进行交互。
# 数据库文件的格式是filename.db，如果数据库文件不存在，那么会被自动创建。
conn = sqlite3.connect('test.db')
print ("数据库打开成功")
# 还可以在内存中创建数据库，只要输入特殊参数值:memory:即可，该数据库只存在于内存中，不会生成本地数据库文件。
# conn = sqlite3.connect(':memory:')
#创建一个游标 cursor对象
cur = conn.cursor()


# 游标对象的.execute()方法可以执行sql命令
# 建表的sql语句
sql_text_1 = '''CREATE TABLE scores
           (姓名 TEXT,
            班级 TEXT,
            性别 TEXT,
            成绩 NUMBER);'''
try:
    # 执行sql语句
    cur.execute(sql_text_1)
    print ("数据表创建成功")
except:
    print ("数据表已存在")


# 提交改动
conn.commit()
# 回滚改动
# conn.rollback()


# 插入单条数据
sql_text_2 = "INSERT INTO scores VALUES('A', '一班', '男', 94)"
cur.execute(sql_text_2)
# 插入多条数据
data = [('B', '一班', '女', 87),
        ('C', '一班', '男', 84),
        ]
cur.executemany('INSERT INTO scores VALUES (?,?,?,?)', data)
conn.commit()

# 执行多个 SQL 语句。它首先执行 COMMIT 语句，然后执行作为参数传入的 SQL 脚本。所有的 SQL 语句应该用分号 ; 分隔。
# cur.executescript(sql_script)

# 返回自数据库连接打开以来被修改、插入或删除的数据库总行数。
print(conn.total_changes)


# 查询数据
sql_text_3 = "SELECT * FROM scores"
cur.execute(sql_text_3)
# 获取所有查询结果
print(cur.fetchall())
# 获取查询结果的下一行
# cur.fetchone()
# 获取查询结果的下一行组
# cur.fetchmany(size=2)


# 关闭连接，关闭前需要手动提交改动
conn.close()
```

```text
+----+-----+--------+------+------+
| id | 姓名 | 班级   | 性别  | 成绩 |
+----+-----+--------+------+------+
| 1  |  A  |  一班   |  男  | 94   |
| 2  |  B  |  一班   |  女  | 87   |
| 3  |  C  |  一班   |  男  | 84   |
+----+-----+--------+------+------+
```

## python第三方库

### Python管理工具

- Python 版本管理
- 包管理
- 环境管理（主要涉及虚拟环境）
- 包构建
- 包发布

#### pip包管理工具

pip 是 Python 包管理工具，该工具提供了对 Python 包的查找、下载、安装、卸载的功能。
（在Python终端中输入命令）

目前如果你在 python.org 下载最新版本的安装包，则是已经自带了该工具。
如果你的系统中没有pip/pip3命令，或者不小心卸载了(`python -m pip uninstall pip`):

- windows:`py -m ensurepip --upgrade`
  此时只能使用 `python -m pip -V`或 `pip3 -V`
  `python -m pip --upgrade pip`更新后就可以正常使用 `pip -V`
- linux:`python -m ensurepip --upgrade`;也可以在root/sudo身份下，运行 `apt install python3-pip`
- macOS:`python -m ensurepip --upgrade`

---

大多数系统将 python 命令默认指向 Python 2。Python 3 发布后，为了兼容性，许多系统将 python3 命令指向 Python 3，而 python 仍然指向 Python 2。pip与pip3同理。
因此在较老版本的Linux中应注意使用python3和pip3命令

*`pip --version`/`pip -V`查看已安装的版本和路径
`pip --help`/`pip -h`查看帮助
`pip install -U pip`升级pip*

2. **`pip install 包名`** 安装包（可以通过使用 ==, >=, <=, >, < 来指定一个版本号。也可以同时指定多个包名）
3. `pip install --upgrade 包名`升级包
4. `pip uninstall 包名`卸载包
5. `pip list`列出已安装的包
   1. `-o`查看可升级的包
   2. `-l`只列出在虚拟环境中安装的包
   3. `--not-required`列出那些不是已安装包的依赖项的包
   4. `--format <list_format>`设置输出格式，可选的值有 columns(默认), freeze, json 或 legacy
6. `pip list | findstr 包名`在所有已安装的包中查找该包名
7. `pip show 包名`显示包的详细信息

---

可以使用 `pip install -i 下载源`临时更换下载源，如：
清华[https://pypi.tuna.tsinghua.edu.cn/simple](https://pypi.tuna.tsinghua.edu.cn/simple)
阿里[https://mirrors.aliyun.com/pypi/simple/](https://mirrors.aliyun.com/pypi/simple/)
中科大[https://mirrors.bfsu.edu.cn/pypi/web/simple/](https://mirrors.bfsu.edu.cn/pypi/web/simple/)
豆瓣[https://pypi.doubanio.com/simple/](https://pypi.doubanio.com/simple/)

如果需要直接更改默认源，使用 `pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple`命令

或者更改配置文件：Unix/Linux/MacOS创建 ~/.pip/pip.conf 文件；Windows创建 %APPDATA%\pip\pip.ini 文件，添加以下内容：

```ini
[global]
index-url = https://mirrors.aliyun.com/pypi/simple/
```

---

如果一个项目需要安装很多库，可以将他们放入一个文件 requirements.txt
requirements.txt 文件内容格式

```txt
包名1==版本号1
包名2==版本号2      #指定版本号
包名3               #不指定版本号
```

使用 `pip freeze > requirements.txt`自动导出requirements.txt文件（`--all`包括自带包pip等;`-l`只列出在虚拟环境中安装的包）
使用 `pip install -y -r requirements.txt`批量安装（`-y`自动全部同意，`-r`读取文件）
使用 `pip uninstall -y -r requirements.txt`批量卸载

---

批量更新所有可更新的包：

```python
import pkg_resources
from subprocess import call
 
for packages in [dist.project_name for dist in pkg_resources.working_set]:
    call("pip3 install --upgrade " + ''.join(packages) + ' --user', shell=True)
```

---

*查看并删除不被依赖的库*
`pip list --not-required --format freeze > unrequirements.txt`然后打开txt文件，手动排除pip等需要的库
`pip uninstall -y -r unrequirements.txt`

*卸载包时查看并删除依赖库*
`pip uninstall`不会删除对应的依赖包，可以 `pip show`查看依赖然后手动删除
也可以使用下面代码

```python
import os
# 白名单，避免被误删
WHITELIST = ['pip', 'setuptools']
# 需要删除的模块列表
REMOVELIST = []

def get_requires(module_name):
    """
    查看一个模块的依赖
    :param module_name: 模块名
    :return: module_name 所依赖的模块的列表
    """
    with os.popen('pip show %s' % module_name) as p:
        requires = p.readlines()
        if not len(requires):
            return []

        reqs = ''
        for line in requires:
            if not line.startswith('Requires:'):
                continue
            reqs = line.strip()
  
        requires = reqs.split(':')[-1].replace(' ', '').strip()
        if requires:
            requires = requires.split(',')
        else:
            requires = []
        return requires


def get_required_bys(module_name):
    """
    查看一个模块被哪些模块依赖
    :param module_name: 模块名
    :return: module_name 被依赖的模块的列表
    """
    with os.popen('pip show %s' % module_name) as p:
        req_by = p.readlines()
        if not len(req_by):
            return []

        required = ''
        for line in req_by:
            if not line.startswith('Required-by:'):
                continue
            required = line.strip()
  
        req_by = required.split(':')[-1].replace(' ', '').strip()
        if req_by:
            req_by = req_by.split(',')
        else:
            req_by = []
        return req_by


def install(name):
    os.system(f'pip install {name}')


def get_all_requires(module_name):
    """
    递归地获取一个模块所有的依赖
    :param module_name: 模块名称
    :return: None
    """
    dependents = get_requires(module_name)
    for package in dependents:
        if package in WHITELIST:
            #print(f'[{package}] in white list')
            continue
        get_all_requires(package)
    REMOVELIST.append(module_name)


def remove(module_name):
    print('Scanning packages...')
    get_all_requires(module_name)
    s_packages =  ','.join(REMOVELIST)
    print(f'[INFO]Found packages: {s_packages}\n')

    for package in REMOVELIST:
        req_bys = get_required_bys(package)
        print('[INFO]removing:', package)
        #print(package, 'is required by:', req_bys)
        flag = True
        for req_by in req_bys:
            if req_by not in REMOVELIST:
                flag = False
                print(f'[NOTICE]As "{package}" is required by "{req_by}" which is not in {REMOVELIST}, skipped...\n')
                break
        if flag:
            print('\n')
            #os.system('pip uninstall -y %s' % package)


if __name__ == '__main__':
    pkg_name = input('请输入要卸载的第三方模块包: ')
    #install(pkg_name)
    remove(pkg_name)
```

---

报错Fatal error in launcher: Unable to create process using xxx

更改了python的安装路径和环境变量或者修改了虚拟环境的路径

`python -m pip install -U --force-reinstall pip`重装pip即可
删除虚拟环境重新创建

#### venv虚拟环境

有可能需要使用一个包的不同版本
在打包成exe文件时配置所需包，而不是打包电脑中所有包，减少体积

虚拟环境就是一个独立的环境（文件夹），用于存放所需的包和开发工具

8. `python -m venv 虚拟环境文件夹名`创建虚拟环境，会创建一个文件夹
9. `source 文件夹名/bin/active`(linux、macos)
   `文件夹名/scripts/activate`(windows)
   命令行前出现 `(虚拟环境名)`代表激活成功
10. `deactivate` 退出虚拟环境
11. 删除虚拟环境，直接删除虚拟环境所在的目录就可以

### Jupyter

`pip install jupyter` 安装 Jupyter notebook 应用程序(Ipython解释器的基于 Web 的界面)
终端输入 `jupyter notebook` 运行(`jupyter notebook --port <port_number>`指定端口)

首次使用可以 `pip install jupyterlab-language-pack-zh-CN` 下载中文包
`jupyter notebook` 运行后在setting——language修改为中文

可以使用ipykernel把一个包虚拟环境安装成jupyter内核（内核≠虚拟环境，内核就指向虚拟环境）
`python -m ipykernel install --user --name=内核真名 --display-name 在内核选择时显示的内核假名`
`jupyter kernelspec remove 内核名称` 删除指定内核

后缀名为 `.ipynb`的 `JSON`格式文件
在文件中可以实现：

1. 编程时具有「语法高亮」、缩进、tab补全的功能。
2. 可直接通过浏览器运行代码，同时在代码块下方展示运行结果。
3. 以富媒体格式展示计算结果。富媒体格式包括：HTML，LaTeX，PNG，SVG等。
4. 对代码编写说明文档或语句时，支持Markdown语法。
5. 支持使用LaTeX编写数学性说明。

在Vscode下载Jupyter插件后可以直接在Vscode中打开ipynb文件，不需要运行jupyter notebook在浏览器中打开

### 运算工具

#### numpy（数组运算）

NumPy(Numerical Python) 是 Python 语言的一个扩展程序库，支持大量的维度数组与矩阵运算，此外也针对数组运算提供大量的数学函数库。

b = a.copy()
np.pi
np.e
np.power()
np.arange(起始值，结束值，间隔)
np.linspace(起始值，结束值，起始值和结束值之间的个数)
np.logspac

np.zeros(长度),ones 初始化
利用多重赋值技巧可以批量初始化 `a,b,c=np.zeros([3,10])`

在使用np.frompyfunc构造ufunc时，numpy后台实际上是把原函数调用了多次，调用次数等于x为维度，每次调用顺次取x中一个元素。所以，此时的x已经失去了数组的那些特性，比如shape属性，它就成一个单独的数字了

**numpy.asfarray()** 函数用于将输入转换为浮点型数组。输入可以是标量、列表、元组、列表的元组、元组的元组、ndarray 等

将多维转换为一维

```python
import numpy as np
mulArrays = [[1,2,3],[4,5,6],[7,8,9]]

np.array(mulArrays).flatten()
np.concatenate(mulArrays.reshape((-1,1),order="F"))
sum(mulArrays,[])
[i for arr in mulArrays for i in arr]
reduce(operator.add, mulArrays)
chain.from_iterable(mulArrays)
```

将一维转换为多维

```python
array1 = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9])
array1.reshape(3,3)
```

弱类型语言，a.b复杂度高，应m = a.b,不要反复查询（对于java a.b 按地址访问复杂度）

```python
numpy.savetxt(fname, X, fmt='%.18e', delimiter=' ', newline='\n', header='', footer='', comments='# ', encoding=None)[source]a = numpy.array([[1,2],[3,4]])
s = str(a)
a.savetxt()
```

**数组各种复制或查看的比较**:

```python
import numpy as np

# 数组各种复制或查看的比较
a = np.array([1, 2, 3])
b = a
c = a.copy()
d = a.view()
e = np.array(a)
f = np.asarray(a)

print('b是a吗？', b is a)  # b是a吗？ True
print('b是以a为基础建立的吗', b.base is a)  # b是以a为基础建立的吗 False
print('c是a吗？', c is a)  # c是a吗？ False
print('c是以a为基础建立的吗', c.base is a)  # c是以a为基础建立的吗 False
print('d是a吗？', d is a)  # d是a吗？ False
print('d是以a为基础建立的吗', d.base is a)  # d是以a为基础建立的吗 True
print('e是a吗？', e is a)  # e是a吗？ False
print('e是以a为基础建立的吗', e.base is a)  # e是以a为基础建立的吗 False
print('f是a吗？', f is a)  # f是a吗？ True
print('f是以a为基础建立的吗', f.base is a)  # f是以a为基础建立的吗 False
a[0] = 4
print('b[0]:', b[0])  # b[0]: 4
print('c[0]:', c[0])  # c[0]: 1
print('d[0]:', d[0])  # d[0]: 4
print('e[0]:', e[0])  # e[0]: 1
print('f[0]:', f[0])  # f[0]: 4
# 特别的：
# 可以用np.array(arr, dtype=float)改变数组中的数据类型
print('a数组中的数据类型', a.dtype)  # a数组中的数据类型 int32
print('e数组中的数据类型', e.dtype)  # e数组中的数据类型 int32
print('f数组中的数据类型', f.dtype)  # f数组中的数据类型 int32
d = np.array(a, dtype=float)
e = np.asarray(a, dtype=float)
print('更改后e数组中的数据类型', e.dtype)  # 更改后e数组中的数据类型 float64
print('更改后f数组中的数据类型', f.dtype)  # 更改后f数组中的数据类型 int32
print('e是a吗？', e is a)  # e是a吗？ False
print('e是以a为基础建立的吗', e.base is a)  # e是以a为基础建立的吗 False
print('f是a吗？', f is a)  # f是a吗？ False
print('f是以a为基础建立的吗', f.base is a)  # f是以a为基础建立的吗 False
```

##### 例子：生成质数表

```python
import numpy as np

primeArr = np.array([2],dtype=int)

for i in range(3, 10000, 2):
    flag = 1
    for j in range(3, int(np.sqrt(i)) + 1, 2):
        if(i % j == 0):
            flag = 0
            break
    if(flag):
        primeArr = np.append(primeArr, [i])

if __name__ == '__main__':
    print(primeArr)
    with open("primeArr.py", "w") as file:
        file.write('import numpy')
        file.write('\n\n')
        file.write('primeArr = numpy.array([')
        for element in primeArr:
            file.write(str(element) + ',')
        file.write('])')
```

因为数组很大，如果 `file.write(str(primeArr))`结果为 `[   2    3    5...994999679973]`
如果仅仅需要打印数组，可以使用 `np.savetxt('primeArr.txt', prime, fmt='%d')`

#### scipy（科学计算）

SciPy 是一个开源的 Python 算法库和数学工具包，是基于 Numpy 的科学计算库，包含的模块有最优化、线性代数、积分、插值、特殊函数、快速傅里叶变换、信号处理和图像处理、常微分方程求解和其他科学与工程中常用的计算。

| 模块名            | 功能               | 参考文档                                                                      |
| ----------------- | ------------------ | ----------------------------------------------------------------------------- |
| scipy.cluster     | 向量量化           | [cluster API](https://docs.scipy.org/doc/scipy/reference/cluster.html)           |
| scipy.constants   | 常量               | [constants API](https://docs.scipy.org/doc/scipy/reference/constants.html)       |
| scipy.fft         | 快速傅里叶变换     | [fft API](https://docs.scipy.org/doc/scipy/reference/fft.html)                   |
| scipy.integrate   | 积分               | [integrate API](https://docs.scipy.org/doc/scipy/reference/integrate.html)       |
| scipy.interpolate | 插值               | [interpolate API](https://docs.scipy.org/doc/scipy/reference/interpolate.html)   |
| scipy.io          | 数据输入输出       | [io API](https://docs.scipy.org/doc/scipy/reference/io.html)                     |
| scipy.linalg      | 线性代数           | [linalg API](https://docs.scipy.org/doc/scipy/reference/linalg.html)             |
| scipy.misc        | 图像处理           | [misc API](https://docs.scipy.org/doc/scipy/reference/misc.html)                 |
| scipy.ndimage     | N 维图像           | [ndimage API](https://docs.scipy.org/doc/scipy/reference/ndimage.html)           |
| scipy.odr         | 正交距离回归       | [odr API](https://docs.scipy.org/doc/scipy/reference/odr.html)                   |
| scipy.optimize    | 优化算法           | [optimize API](https://docs.scipy.org/doc/scipy/reference/optimize.html)         |
| scipy.signal      | 信号处理           | [signal API](https://docs.scipy.org/doc/scipy/reference/signal.html)             |
| scipy.sparse      | 稀疏矩阵           | [sparse API](https://docs.scipy.org/doc/scipy/reference/sparse.html)             |
| scipy.spatial     | 空间数据结构和算法 | [spatial API](https://docs.scipy.org/doc/scipy/reference/spatial.html)           |
| scipy.special     | 特殊数学函数       | [special API](https://docs.scipy.org/doc/scipy/reference/special.html)           |
| scipy.stats       | 统计函数           | [stats.mstats API](https://docs.scipy.org/doc/scipy/reference/stats.mstats.html) |

##### constants常量

提供了许多内置的常量，如pi

```python
from scipy import constants

print(constants.pi) // 圆周率
// print(dir(constants)) // 使用dir()函数来查看constants模块包含了哪些常量
```

##### special 特殊函数

##### optimize优化算法

提供了常用的最优化算法函数实现，我们可以直接调用这些函数完成我们的优化问题

迭代法解方程 `root(fun, x0)` fun为函数；x0为根的初始猜测

##### 解方程

线性方程组

```
from sympy import symbols, Eq, solve

x, y = symbols('x y')
eq1 = Eq(x + y, 3)
eq2 = Eq(2 * x - y, 1)

sol = solve((eq1, eq2), (x, y))

print(sol)
```

非线性方程

```
import scipy.optimize as opt

def equation(x):
    return x**2 - 4

# 使用二分法求解方程
sol = opt.bisect(equation, 0, 3)

print(sol)
```

隐函数方程

##### 微分方程

```
import numpy as np
from scipy.integrate import odeint
import matplotlib.pyplot as plt
 
# 定义微分方程
def model(y, t):
    V, E = y
    dV_dt = -V * (1 - V ** 2) * E
    dE_dt = V * (28 - E)
    return [dV_dt, dE_dt]
 
# 初始条件和时间范围
y0 = [0.0, 1.0]  # 初始状态[V0, E0]
t = np.linspace(0, 200, 1001)  # 时间范围
 
# 使用odeint解微分方程
solution = odeint(model, y0, t)
 
# 画图
plt.figure()
plt.plot(t, solution[:, 0], label='V(t)')
plt.plot(t, solution[:, 1], label='E(t)')
plt.xlabel('t')
plt.ylabel('Value')
plt.title('Solution of the differential equations')
plt.legend()
plt.show()
```

##### misc

scipy在新版本的misc库中弃用(imread，imresize，imsave)函数
解决办法1：降低scipy的版本 `pip install scipy==1.2.1`
解决方法2：更换库

```python
# from scipy import misc 
# img = misc.imread(image_path)
import imageio
img = imageio.imread(image_path)

# from scipy import misc 
# scaled_temp = misc.imresize(cropped_temp, (image_size, image_size), interp='bilinear')
from skimage.transform import resize 
scaled_temp = resize(cropped_temp,output_shape=(image_size, image_size))

# from scipy import misc 
# misc.imsave(output_filename, scaled_temp)
import imageio 
imageio.imwrite(output_filename,scaled_temp)
```

##### ndimage

```python
import scipy.ndimage as nd
img_array_rotate = nd.rotate(img_array, 10, cval = 0.01, reshape = False)
# 把图片数组逆时针旋转10度
```

##### SymPy（符号计算）

SymPy 是一个由 Python 语言编写的符号计算库。
SageMath 便是将 SymPy 作为其子模块，然后再加入其他模块，构建出一个功能齐全的数学软件。

处理数学对象的计算称为符号计算。在符号计算中，数学对象是精确表示的，而不是近似的，未计算的数学表达式会以符号形式保留。
例如：数值计算结果无法精确地表示出 sin⁡π，只能用一个很小的浮点数 (1.22×10−16) 表示，而符号计算结果则得出 sin⁡π=0

计算机代数系统（Computer Algebra System，缩写作：CAS）是进行符号运算的软件。在计算机代数系统中运算的对象是数学表达式

#### numba、Cython

python由于它动态解释性语言的特性，跑起代码来相比java、c++要慢很多，尤其在做科学计算的时候，十亿百亿级别的运算，让python的这种劣势更加凸显。

numba是一款可以将python函数编译为机器代码的JIT编译器，经过numba编译的python代码（仅限数组运算），其运行速度可以接近C或FORTRAN语言。

JIT 即时编译技术是在运行时（runtime）将调用的函数或程序段编译成机器码载入内存，以加快程序的执行。
python之所以慢，是因为它是靠CPython编译的，numba的作用是给python换一种编译器。numba 就是通过 JIT 加速了 python 代码

Numba是一款可以将python函数编译为机器代码的JIT编译器，经过Numba编译的python代码（仅限数组运算），其运行速度可以接近C或FORTRAN语言。普通python语言靠CPython编译的，但是Numba使用Jit编译器可以直接将一个函数转化为机器码。

使用numpy数组做大量科学计算时
使用for循环时

明确指定数据类型加速才快
如np.array([], np.float64)

### 可视化

**Matplotlib、Pyecharts、Seaborn、Plotly、Bokeh**

#### matplotlib（数据可视化）

Matplotlib 是 Python 的绘图库，它能让使用者很轻松地将数据图形化，并且提供多样化的输出格式。

- `plot()`：用于绘制线图和散点图
- `scatter()`：用于绘制散点图
- `bar()`：用于绘制垂直条形图和水平条形图
- `hist()`：用于绘制直方图
- `pie()`：用于绘制饼图
- `imshow()`：用于绘制图像
- `subplots()`：用于创建子图

```python
import matplotlib as mpl
# 指定默认字体：解决plot不能显示中文问题
mpl.rcParams['font.sans-serif'] = ['Microsoft YaHei']
# 解决保存图像是负号'-'显示为方块的问题
mpl.rcParams['axes.unicode_minus'] = False

# 黑体 SimHei
# 微软雅黑 Microsoft YaHei
# 微软正黑体 Microsoft JHengHei
# 新宋体 NSimSun
# 新细明体 PMingLiU
# 细明体 MingLiU
# 标楷体 DFKai-SB
# 仿宋 FangSong
# 楷体 KaiTi
# 仿宋-GB2312 FangSong_GB2312
# 楷体-GB2312 KaiTi_GB2312
```

```python
# 使用原始字符串和 $ 符号在 matplotlib 中显示希腊字母
plt.title(r"$\alpha$")
# 使用 `chr()` 函数
plt.title(chr(945))
# 在 Python 3 及以上版本可以直接使用希腊字母
plt.title("α")
```

##### Pyplot

画各种静态图

```python
# 设置一个 1200 x 600 的画布
plt.figure(figsize=(12, 6))
# 全局设置画布大小 1280 x 720 像素
plt.rcParams['figure.figsize']=(12.8, 7.2)
# 使用样式表文件style.mpstyle，文件内容：figure.figsize:12.8,7.2
plt.style.use('style.mpstyle')
```

将画布保存为'xiang.png'，还可以保存为jpg、svg格式图片
plt.savefig('xiang.png')

###### plot()

`plot([x], y, [fmt], [x2], y2, [fmt2], ..., **kwargs)`

- `x, y`：点或线的节点，x 为 x 轴数据，y 为 y 轴数据，数据可以列表或数组
- `fmt`：可选，定义基本格式 `'[marker][line][color]'`
  - 标记样式：'.' 点标记，',' 像素标记(极小点)，'o' 实心圈标记，'v' 倒三角标记，'^' 上三角标记，'>' 右三角标记，'<' 左三角标记...
  - 线的类型：'‐' 实线，'‐‐' 破折线，'‐.' 点划线，':' 虚线。
  - 标记和线的颜色：'b' 蓝色，'m' 洋红色，'g' 绿色，'y' 黄色，'r' 红色，'k' 黑色，'w' 白色，'c' 青绿色，'#008000' RGB 颜色符串。多条曲线不指定颜色时，会自动选择不同颜色
- `**kwargs`：可选，用在二维平面图上，设置指定属性，如标签，线的宽度等
  - `marker`标记样式;`ms`标记的大小;`mfc`标记内部的颜色;`mec`标记边框的颜色
  - `ls`线的类型;`c`线的颜色;`lw`线的宽度

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(0,4*np.pi,0.1)
y = np.sin(x)

plt.plot(x, y, '.-', mfc='#fff', mec='g', c='b', lw=1)
plt.show()
```

绘制多个图形 `plt.subplot()`

```python
import matplotlib.pyplot as plt
 
# 第一个图形的数据
x1 = [1, 2, 3, 4]
y1 = [10, 20, 25, 30]
 
# 第二个图形的数据
x2 = [1, 2, 3, 4]
y2 = [15, 25, 10, 30]
 
# 创建图形
plt.figure()
 
# 绘制第一个图形
plt.subplot(2, 1, 1)  # 表示2行1列的子图，当前为第1个
plt.plot(x1, y1, 'r-')  # 'r-'表示红色实线
plt.title('First Plot')  # 添加标题
 
# 绘制第二个图形
plt.subplot(2, 1, 2)  # 表示2行1列的子图，当前为第2个
plt.plot(x2, y2, 'b-')  # 'b-'表示蓝色实线
plt.title('Second Plot')  # 添加标题
 
# 显示图形
plt.show()

# --------------设置子图标题-----------------
# 创建一个2x2的子图网格
fig, axes = plt.subplots(2, 2)
 
# 为每个子图设置标题
axes[0, 0].set_title('第一个子图的标题')
axes[0, 1].set_title('第二个子图的标题')
axes[1, 0].set_title('第三个子图的标题')
axes[1, 1].set_title('第四个子图的标题')
 
# 显示图形
plt.show()
```

可以通过指定 `plt.xlim()` 和 `plt.ylim()` 来设置绘图区域的x轴和y轴范围 `axis`
`plt.xticks()` 和 `plt.yticks()` 调整x轴和y轴的标签值
`plt.xlabel` 设置坐标轴标题
hold on\hold off\drawnow
xticks(ticks, [labels], **kwargs)
ticks：数组类型，用于设置X轴刻度间隔
[labels]：数组类型，用于设置每个间隔的显示标签
**kwargs：用于设置标签字体倾斜度和颜色等外观属性。

```python
import matplotlib.pyplot as plt
import matplotlib.animation as animation
import numpy as np
 
# 初始化数据
x = np.arange(0, 2*np.pi, 0.01)
y = np.sin(x)
line, = plt.plot(x, y)
 
# 更新数据的函数
def update(data):
    global x, y
    y = np.sin(x + data * 2 * np.pi / 100)
    line.set_ydata(y)
    return line,
 
# 创建动画
def animate(data):
    anim = animation.FuncAnimation(plt.gcf(), update, frames=range(100), interval=100)
    plt.show()
 
# 运行动画
animate(0)

#---matlab
x = linspace(0, 2*pi, 100); % 创建一个线性空间向量
y = sin(x); % 计算正弦值
 
figure; % 创建一个新的图形窗口
axis([0 2*pi -1 1]); % 设置坐标轴范围
hold on; % 保持当前图形，以便添加新的数据
 
for i = 1:length(x)
    plot(x(1:i), y(1:i), 'r-'); % 绘制到当前点的正弦曲线
    drawnow; % 强制图形更新
    pause(0.05); % 暂停一小段时间以创建动画效果
end
hold off; % 关闭hold状态
```

figure对象 `fig=plt.figure(figsize=(6,3))` figsize设置窗口大小
图例通过 `plt.legend()`实现，标题通过 `plt.suptitle("这是图像标题")`和 `plt.title("这是子图标题")`实现（其实是调用了当前figure对象的suptitle方法）
获取默认窗口标题 `fig.canvas.manager.window.windowTitle()` 修改窗口标题可以使用 `fig.canvas.set_window_title("这是窗口标题")` 或 `fig.canvas.manager.window.setWindowTitle("这是窗口标题")`

```python
import matplotlib as mpl

mpl.rcParams["font.sans-serif"] = ["SimHei"]
mpl.rcParams["axes.unicode_minus"] = False

import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-2*np.pi,2*np.pi,200)
y = np.sin(x)
y1 = np.cos(x)

plt.plot(x,y,label = r"$\sin(x)$")
# 用r”$text1$”对文本内容text进行渲染，有r表示该字符串是raw strings，字符串按照TeX规范进行解析
plt.plot(x,y1,label = r"$\cos(x)$")

plt.legend()
plt.title("正弦函数和余弦函数的折线图") # 添加标题
plt.show()
```

`matplotlib.pyplot.grid(b=None, which='major', axis='both', )`
b：可选，默认为 None，可以设置布尔值，true 为显示网格线，false 为不显示，如果设置 **kwargs 参数，则值为 true。
which：可选，可选值有 'major'、'minor' 和 'both'，默认为 'major'，表示应用更改的网格线。
axis：可选，设置显示哪个方向的网格线，可以是取 'both'（默认），'x' 或 'y'，分别表示两个方向，x 轴方向或 y 轴方向。
**kwargs：可选，设置网格样式，可以是 color='r', linestyle='-' 和 linewidth=2，分别表示网格线的颜色，样式和宽度。

###### imshow()

imshow() 函数是 Matplotlib 库中的一个函数，用于显示图像。
imshow() 函数常用于绘制二维的灰度图像或彩色图像。
imshow() 函数可用于绘制矩阵、热力图、地图等。

`imshow(X, cmap=None, norm=None, aspect=None, interpolation=None, alpha=None, vmin=None, vmax=None, origin=None, extent=None, shape=None, filternorm=1, filterrad=4.0, imlim=None, resample=None, url=None, *, data=None, **kwargs)`

**参数说明：**

- `X`：输入数据。可以是二维数组、三维数组、PIL图像对象、matplotlib路径对象等。
- `cmap`：颜色映射。用于控制图像中不同数值所对应的颜色。可以选择内置的颜色映射，如 `gray`、`hot`、`jet`等，也可以自定义颜色映射。
- `norm`：用于控制数值的归一化方式。可以选择 `Normalize`、`LogNorm`等归一化方法。
- `aspect`：控制图像纵横比（aspect ratio）。可以设置为 `auto`或一个数字。
- `interpolation`：插值方法。用于控制图像的平滑程度和细节程度。可以选择 `nearest`、`bilinear`、`bicubic`等插值方法。
- `alpha`：图像透明度。取值范围为0~1。
- `origin`：坐标轴原点的位置。可以设置为 `upper`或 `lower`。
- `extent`：控制显示的数据范围。可以设置为 `[xmin, xmax, ymin, ymax]`。
- `vmin`、`vmax`：控制颜色映射的值域范围。
- `filternorm 和 filterrad`：用于图像滤波的对象。可以设置为 `None`、`antigrain`、`freetype`等。
- `imlim`： 用于指定图像显示范围。
- `resample`：用于指定图像重采样方式。
- `url`：用于指定图像链接。

```python
import matplotlib.pyplot as plt
import numpy as np

# 生成一个二维随机数组
img = np.random.rand(10, 10)
# 绘制灰度图像
plt.imshow(img, cmap='gray')
# 隐藏坐标轴  
plt.axis('off')
# 显示图像
plt.show()
```

##### animation

`FuncAnimation(fig, func, frames, init_func, interval, blit)`
主要参数的含义如下

- fig: 绘制动图的画布名称
- func: 回调函数，每次更新时调用，即下边程序定义的函数update，可以在这个方法中更新 line2d 对象。
- frames: 真个动画 frame 的取值范围，在函数运行时，其值会传递给函数 update(n) 的形参 n。
- init_func: 自定义开始帧，即传入刚定义的函数init,初始化函数。
- interval: frame之间的更新频率，以 ms 计。

用 FuncAnimation 生成的动图，如果要存 mp4，需要安装 ffmpeg，如果要存 gif，需要安装 imagemagick
ani.save("animation.mp4", fps=20, writer="ffmpeg")
ani.save("animation.gif", fps=50, writer="imagemagick")

```python
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.animation import FuncAnimation

fig = plt.figure()
ax = fig.add_subplot(1, 1, 1)

x = np.linspace(0, 2 * np.pi, 5000)
y = np.exp(-x) * np.cos(2 * np.pi * x)
line, = ax.plot(x, y, color="cornflowerblue", lw=3)
ax.set_ylim(-1.1, 1.1)

# 清空当前帧
def init():
    line.set_ydata([np.nan] * len(x))
    return line,

# 更新新一帧的数据
def update(frame):
    line.set_ydata(np.exp(-x) * np.cos(2 * np.pi * x + float(frame)/100))
    return line,

# 调用 FuncAnimation
ani = FuncAnimation(fig
                   ,update
                   ,init_func=init
                   ,frames=200
                   ,interval=2
                   ,blit=True
                   )

ani.save("animation.gif", fps=25, writer="imagemagick")
```

#### Seaborn（matplotlib封装）

Seaborn 是基于 Python 且非常受欢迎的图形可视化库，在 Matplotlib 的基础上，进行了更高级的封装，使得作图更加方便快捷。

```python
import seaborn as sns
import matplotlib.pyplot as plt

# 设置主题和颜色调色板
sns.set_theme(style="darkgrid", palette="pastel")
# 示例数据
products = ["Product A", "Product B", "Product C", "Product D"]
sales = [120, 210, 150, 180]
# 创建柱状图
sns.barplot(x=products, y=sales)
# 添加标签和标题
plt.xlabel("Products")
plt.ylabel("Sales")
plt.title("Product Sales by Category")
# 显示图表
plt.show()
```

`sns.set_theme(style="whitegrid", palette="pastel")`
主题（style）：darkgrid（默认）：深色网格主题；whitegrid：浅色网格主题；dark：深色主题，没有网格；white：浅色主题，没有网格；ticks：深色主题，带有刻度标记
模板（context）：paper：适用于小图，具有较小的标签和线条；notebook（默认）：适用于笔记本电脑和类似环境，具有中等大小的标签和线条；talk：适用于演讲幻灯片，具有大尺寸的标签和线条；poster：适用于海报，具有非常大的标签和线条
调色板（palette）：分类色板：deep, muted, **pastel**, bright, dark, colorblind.；连续色板：rocket,**crest**,mako,flare；离散色板：vlag,icefire；自定义：单色渐变sns.color_palette('Blues')

1. 散点图 - sns.scatterplot()
2. 折线图 - sns.lineplot()
3. 柱状图 - sns.barplot()
4. 箱线图 - sns.boxplot()
5. 热力图 - sns.heatmap()
6. 小提琴图 - sns.violinplot()

计数图 - countplot
散点图stripplot/swarmplot
回归图regplot/lmplot

#### pynimate（ 动态排序图）

输入的数据必须是pandas数据结构DataFrame：

```csv
time, col1, col2, col3  
2012   1     2     1  
2013   1     1     2  
2014   2     1.5   3  
2015   2.5   2     3.5
```

```python
from matplotlib import pyplot as plt  
import pandas as pd  
import pynimate as nim  

df = pd.DataFrame(  
    {  
        "time": ["1960-01-01", "1961-01-01", "1962-01-01"],  
        "Afghanistan": [1, 2, 3],  
        "Angola": [2, 3, 4],  
        "Albania": [1, 2, 5],  
        "USA": [5, 3, 4],  
        "Argentina": [1, 4, 5],  
    }  
).set_index("time")  
# df = pd.read_csv('data'csv').set_index('time')

# 定义画布
cnv = nim.Canvas()
# 设置插值频率为5d，可自定义调节
bar = nim.Barplot(df, "%Y-%m-%d", "5d")  
# 使用回调函数接收对应格式化的年月信息
bar.set_time(callback=lambda i, datafier: datafier.data.index[i].year) 
# 添加条形图到画布
cnv.add_plot(bar)  
cnv.animate()  
plt.show()

# 两种格式存储，git和mp4(需要安装相应的库)
cnv.save("file", 24, "gif")
# cnv.save("file", 24, "mp4")
```

#### mayavi（3D可视化）

#### Plotly(可交互)

[Plotly Python 绘图库 ](https://plotly.com/python/) 是一个开源的代码库，它基于 plot.js，而后者基于 d3.js。

可以生成交互式图表。图表以 JavaScript 对象表示法(JSON) 数据格式存储，以便可以使用其他编程语言读取。图表可以导出为各种光栅和矢量图像格式

`pip install plotly`
`pip install jupyter` 安装 Jupyter notebook 应用程序

Plotly中绘制图像有在线和离线两种方式，在线绘图需要注册账号获取API key。
离线绘图又有plotly.offline.plot()和plotly.offline.iplot()两种方法，前者是以离线的方式在当前工作目录下生成html格式的图像文件，并自动打开；后者是在jupyter notebook中专用的方法，即将生成的图形嵌入到后缀名为 `.ipynb`的 `JSON`格式文件中

在.ipynb文件中运行下列代码：

```python
import plotly
import plotly.graph_objs as go

'''初始化jupyter notebook中的绘图模式'''
plotly.offline.init_notebook_mode()

'''绘制一个基本的折线图，控制其尺寸为1600x600'''
plotly.offline.iplot([{'x': [1, 2, 3], 'y': [5, 2, 7]}],
                    image_height=600,
                    image_width=1600)
```

```python
import numpy as np
import plotly
import plotly.graph_objs as go

'''创建仿真数据'''
N = 100
random_x = np.linspace(0, 1, N)
random_y0 = np.random.randn(N)+5
random_y1 = np.random.randn(N)
random_y2 = np.random.randn(N)-5

'''构造trace0'''
trace0 = go.Scatter(
    x = random_x,
    y = random_y0,
    mode = 'markers',
    name = 'markers'
)

'''构造trace1'''
trace1 = go.Scatter(
    x = random_x,
    y = random_y1,
    mode = 'lines+markers',
    name = 'lines+markers'
)

'''构造trace2'''
trace2 = go.Scatter(
    x = random_x,
    y = random_y2,
    mode = 'lines',
    name = 'lines'
)

'''将所有trace保存在列表中'''
data = [trace0, trace1, trace2]

'''构造layout对象，设置标题和图例'''
layout = go.Layout(
    title={
        'text': "Plotly",
        'x':0.5,
        'y':0.9,
        'xanchor': 'center',
        'yanchor': 'top'},
    legend={
        'x':1,
        'y':1},
)

'''构造figure对象'''
fig = go.Figure(data=data,layout=layout)

'''启动绘图'''
plotly.offline.init_notebook_mode()
plotly.offline.iplot(fig, filename='scatter-mode')
```

#### Pyecharts(可交互)

[ pyecharts](https://05x-docs.pyecharts.org/#/zh-cn/prepare)是一个基于 ECharts 的 Python 数据可视化库，它允许用户使用 Python 语言生成各种类型的交互式图表和数据可视化。
ECharts 是一个使用 JavaScript 实现的由百度开源的可视化库，而 Pyecharts 则是 ECharts 的 Python 封装，使得在 Python 中使用 ECharts 变得更加方便。

`pip install pyecharts`

```python
from pyecharts import options as opts
from pyecharts.charts import Bar

# 准备数据
x_data = ['一月', '二月', '三月', '四月', '五月']
y_data = [10, 20, 15, 25, 30]

# 创建柱状图
bar_chart = Bar()
bar_chart.add_xaxis(x_data)
bar_chart.add_yaxis("销售额", y_data)

# 配置全局属性
bar_chart.set_global_opts(
    title_opts=opts.TitleOpts(title="月度销售额柱状图", subtitle="副标题"),
    xaxis_opts=opts.AxisOpts(name="月份"),
    yaxis_opts=opts.AxisOpts(name="销售额（万元）"),
    legend_opts=opts.LegendOpts(pos_left="center", pos_top="top"),
    toolbox_opts=opts.ToolboxOpts(),
    tooltip_opts=opts.TooltipOpts(trigger="axis", axis_pointer_type="cross"),
)

# 渲染图表，生成本地 HTML 文件
bar_chart.render("global_options_bar_chart.html")
```

#### VPython（3D图形和动画）

VPython，全称为Visual Python，是一个用于创建3D图形和动画的Python库。它为用户提供了简单易用的工具，用于绘制3D图形、创建动画效果和交互式应用程序。

### Shapely(处理几何关系)

Shapely 是一个用于处理几何对象的 Python 库，用于使用广泛部署的 GEOS 库中的函数进行平面特征的集合论分析和操作。GEOS 是 Java 拓扑套件（JTS）的移植，是 PostgreSQL RDBMS 空间扩展 PostGIS 的几何引擎。

Shapely是一个平面几何库，在几何分析中忽略了z，只有z值不同的坐标图元是不能相互区分的

Shapely 实现的几何对象的基本类型是点、曲线和曲面。

```python
from shapely.geometry import Point, LineString, Polygon
from shapely.geometry import LinearRing, box
import matplotlib.pyplot as plt

# 创建基本几何对象，在所有构造函数中数字值被转换为float类型
point = Point(0, 0)                      # 点
line = LineString([(0,0), (1,1), (2,0)]) # 折线
polygon = Polygon([(0,0), (1,5), (3,3)]) # 多边形

ring = LinearRing([(0, 0), (1, 1), (1, 0)])　# 线性环
box = box(0.0, 0.0, 1.0, 1.0)　# 矩形多边形

# 可视化
plt.figure(figsize=(8,4))
plt.subplot(131).scatter(*point.xy); plt.title("Point")
plt.subplot(132).plot(*line.xy); plt.title("Line")
plt.subplot(133).plot(*polygon.exterior.xy); plt.title("Polygon")
plt.show()
# 在jupyter中直接写几何对象名称即可显示，不过只显示一个
polygon
```

构造函数也接受另一个实例，从而产生一个副本

```python
Point(point)
LineString(line)
LineString(ring)
LinearRing(ring)
LinearRing(line)
Polygon(polygon)
Polygon(line)
Polygon(ring)
Polygon(box)
```

几何对象具有面积（area）、长度（length）、坐标（coords）和边界（bounds）属性

集合

```python
a = Point(1, 1).buffer(1.5)
b = Point(2, 1).buffer(1.5)
# 交集
a.intersection(b)
a&b
# 并集
a.union(b)
a|b
# 差集
a.difference(b)
a-b
# 异或
a.symmetric_difference(b)
a^b
(a|b)-(a&b) # 图形一样但是 (a^b)==((a|b)-(a&b)) 为False

a and b # a
a or b # b
```

```python
from shapely.geometry import MultiPoint, MultiLineString, MultiPolygon
points = MultiPoint([(0.0, 0.0), (1.0, 1.0)]) # 点的集合
lines = MultiLineString([((0, 0), (1, 1)), ((-1, 0), (1, 0))]) # 线条的集合
polygons = MultiPolygon([polygon, s, t]) # 多边形的集合
# Empty空特征可以通过调用各种没有参数的构造函数来创建。空特征几乎不支持任何操作。

point1 = Point(0,0)
point2 = Point(1,1)
points==(point1|point2) # True
```

多点集合的成员可以通过 `geoms` 属性或使用 `in` 或 `list()` 的迭代器协议来访问

object.minimum_clearance
返回一个节点被移动以产生无效几何体的最小距离。
object.distance(other)
返回到另一个几何对象的最小距离
object.hausdorff_distance(other)
返回到另一个几何体的Hausdorff距离（float）。两个几何体之间的Hausdorff距离是任何一个几何体上的一个点与另一个几何体上的最近点之间的最远距离。
object.representative_point( )
返回一个便宜的计算点，保证在几何对象内

坐标值通过coords、x、y和 z属性访问

object.interpolate(distance[, normalized=False])
返回一个沿线性几何对象的指定距离的点。线性特征（如 LineStrings 和 MultiLineStrings ）
ip = LineString([(0, 0), (0, 1), (1, 1)]).interpolate(1.5)
object.project(other[, normalized=False])
返回沿这个几何对象到离另一个对象最近的点的距离。如果(normalized arg)为True，返回归一化为对象长度的距离
LineString([(0, 0), (0, 1), (1, 1)]).project(ip)

[Shapely 用户手册](https://www.heywhale.com/mw/project/62754e8fd0bd1f00173f1cee)
object.has_z
如果该特征不仅有 x 和 y ，而且还有3D（或所谓的2.5D）几何形状的 z 坐标，则返回True。
object.is_ccw
如果坐标是按逆时针顺序排列的，则返回True（边界是一个有正号的区域）。这个方法只适用于 LinearRing 对象。
object.is_empty
如果该特征的 interior 和 boundary（以点集术语）与空集重合，则返回True。
object.is_ring
如果该特征是一个封闭的、简单的 LineString，返回True。一个封闭的特征的 boundary 与空集重合。
object.is_simple
如果该特征不与自身交叉，则返回True。简单性测试只对 LineStrings 和 LinearRings 有意义。
object.is_valid
如果一个特征在1的意义上是 "有效 "的，则返回True。有效性测试只对 Polygons 和 MultiPolygons 有意义。对于其他类型的几何体，总是返回 True。

object.eq(other)
如果两个对象是相同的几何类型，并且两个对象的坐标精确匹配，则返回 True。
object.eals(other)
如果对象的集合论边界、内部和外部与另一个对象的集合论边界、内部和外部相吻合，则返回True。
object.almost_equals(other[, decimal=6])
如果对象在所有点上都近似等于另一个对象，并达到指定的小数位精度，则返回True。
object.contains(other)
如果其他物体的任何点都不在物体的外部，并且其他物体的内部至少有一个点在物体的内部，则返回True。
object.within(other)
如果对象的边界和内部只与对方的内部相交（而不是其边界或外部），则返回True。
object.covers(other)
如果其他物体的每一个点都是物体内部或边界上的一个点，则返回True。这与object.contains(other)相似，只是这不需要其他的内部点位于对象的内部。
object.covered_by(other)
如果对象的每一个点都是其他对象的内部或边界上的一个点，则返回True。这等同于other.cover(object)。
object.crosses(other)
如果对象的内部与另一个对象的内部相交，但不包含它，并且相交的尺寸小于一个或另一个对象的尺寸，则返回True。
object.disjoint(other)
如果对象的边界和内部与另一个对象的边界和内部完全不相交，则返回True。
object.intersects(other)
如果对象的边界或内部以任何方式与其他对象相交，则返回True。
object.intersects(other)
如果对象的边界或内部以任何方式与其他对象相交，则返回True。
object.touches(other)
如果对象至少有一个共同点，并且其内部没有与对方的任何部分相交，则返回True。

object.relate(other)
返回一个对象的内部、边界、外部与另一个几何对象的关系的DE-9IM矩阵的字符串表示。
object.relate_pattern(other, pattern)
如果几何体之间关系的DE-9IM字符串代码满足模式，则返回True，否则返回False。

object.boundary
返回一个低维对象，代表该对象的集合理论边界。
object.centroid
返回对象的几何中心点（点）的表示。
object.difference(other)
返回构成此几何对象的、不构成另一对象的点的表示。
object.intersection(other)
返回此对象与其他几何对象的交集的表示。
object.symmetric_difference(other)
返回本对象中不在其他几何对象中的点的表示，以及其他对象中不在本几何对象中的点的表示。
object.union(other)
返回这个对象和另一个几何对象的点的联合的表示。

object.buffer(distance, resolution=16, cap_style=1, join_style=1, mitre_limit=5.0, single_sided=False)
返回该几何对象给定距离内的所有点的近似表示。
object.convex_hull
返回包含对象中所有点的最小的凸形 Polygon 的表示，除非对象中的点的数量少于3。对于两个点，凸面体塌陷为 LineString ；对于1个点，为 Point。
object.envelope
返回包含该对象的点或最小的矩形多边形（边与坐标轴平行）的表示。
object.minimum_rotated_rectangle
返回包含该对象的一般最小边界矩形。与包络线不同，这个矩形不受约束地与坐标轴平行。如果对象的凸壳是一个退化体（线或点），将返回这个退化体。
object.parallel_offset(distance, side, resolution=16, join_style=1, mitre_limit=5.0)
返回一个LineString或MultiLineString几何体在其右边或左边与对象的距离。此方法仅适用于 LinearRing 和 LineString 对象。
object.simplify(tolerance, preserve_topology=True)
返回几何对象的简化表示。
shapely.affinity.affine_transform(geom, matrix)
返回一个使用仿射变换矩阵的变换几何体。系数矩阵matrix以列表或元组的形式提供，对于二维或三维变换，分别有6或12项。
shapely.affinity.rotate(geom, angle, origin='center', use_radians=False)
返回一个在二维平面上旋转的几何体。旋转的角度可以用度数（默认）或者通过设置use_radians=True来指定弧度。
shapely.affinity.scale(geom, xfact=1.0, yfact=1.0, zfact=1.0, origin='center')
返回一个按比例排列的几何体，沿着每个维度都有相应的缩放系数。
shapely.affinity.skew(geom, xs=0.0, ys=0.0, origin='center', use_radians=False)
返回一个倾斜的几何体，沿着x和y维度的角度进行剪切。
shapely.affinity.translate(geom, xoff=0.0, yoff=0.0, zoff=0.0)
返回一个沿各维度偏移的平移的几何体。

### 文件处理

#### pandas（数据处理）

##### Excel

读取文件：

```python
import pandas as pd
# 需要下载xlrd(.xls) 或 openpyxl(.xlsx)
df = pd.read_excel(r'example.xlsx', sheet_name='Sheet1', index_col=None, header=0, usecols=[0,2])
# 当只读取一个sheet时，返回的是DataFrame对象
# 'r'是转义字符，避免路径中的'\'被转译，也可以不加'r'，但要变为'/'
# sheet_name 导入指定sheet的表格，默认读取第一个sheet

# index_col，header 指定行、列索引 行索引默认None，列索引默认0
# header可以设置为None(0，1，2作为索引名）或者具体的行(header=0)
# index_col可以设置为None(0，1，2作为索引名）或者具体的列(index_col=2，会将那一列的值取出作为列名)或者False(0，1，2作为索引名）

# usecols 指定需要导入的列。也支持usecols=[‘列名’]

# 获取全部数据：df.values，获取全部数据，返回类型为ndarray（二维）。


# 在DataFrame中，空值默认是NaN
# 1)读取 Excel 时禁用 NaN，空单元格变为空字符串 ""
# df = pd.read_excel("input.xlsx", keep_default_na=False)
# 2)替换所有 NaN 为 None（适合 Python 原生处理）
# df = df.where(pd.notnull(df), None)
# 3)或者替换为自定义值（如空字符串）
# df = df.fillna("")
# 4)逐行处理，将 NaN 替换为 None
# for row in df.itertuples(index=False):
#     cleaned_row = [None if pd.isna(x) else x for x in row]
#     data_list.append(cleaned_row)
```

写入文件：

```python
import pandas as pd

# 创建一个简单的DataFrame
# 可以是字典、二维数组、Series、DataFrame 或其他可转换为 DataFrame 的对象。
data = {
'Name': ['Alice', 'Bob', 'Charlie'],
'Age': [25, 30, 22],
'City': ['New York', 'London', 'Paris']
}
df = pd.DataFrame(data)

# 将DataFrame导出到Excel文件 
# index=False参数表示在导出的Excel文件中不包含DataFrame的索引列。
df.to_excel('output.xlsx', index=False)
```

对较长的文本内容美化：

```python
import pandas as pd
from openpyxl import Workbook
from openpyxl.utils import get_column_letter
from openpyxl.styles import Alignment

# 创建一个示例 DataFrame
data = {
    "列1": ["短文本", "较长的文本内容需要换行显示"],
    "列2": ["Another short text", "Another long text that needs wrapping"]
}
df = pd.DataFrame(data)

# 将 DataFrame 写入 Excel 文件
excel_file = "output.xlsx"
df.to_excel(excel_file, index=False)

# 使用 openpyxl 调整列宽和设置文本换行
from openpyxl import load_workbook

# 加载刚刚保存的 Excel 文件
wb = load_workbook(excel_file)
ws = wb.active

# 遍历所有列，设置列宽自适应
for col in ws.columns:
    max_length = 0
    col_letter = get_column_letter(col[0].column)  # 获取列字母
    for cell in col:
        try:
            if cell.value:  # 计算单元格内容的长度
                max_length = max(max_length, len(str(cell.value)))
        except:
            pass
	# +2 添加一些额外空间显示，并且限制最大列宽为50防止过长
    adjusted_width = min(max_length + 2, 50)
    ws.column_dimensions[col_letter].width = adjusted_width

# 设置文本换行和对齐方式
for row in ws.iter_rows():
    for cell in row:
        cell.alignment = Alignment(wrap_text=True, vertical="top", horizontal="left")

# 保存修改后的 Excel 文件
wb.save(excel_file)
```

`openpyxl` 支持在Excel中插入图片，但图片会浮动在单元格上方，不会随单元格自动调整位置。
`xlsxwriter` 适用于创建新Excel文件，支持直接插入图片到指定位置。
`xlwings` 通过Excel应用程序接口操作，适合需要精确控制图片位置的场景。

添加超链接

```python
value_cell = sheet.cell(row=row_num, column=2, value=row_data[1])
value_cell.hyperlink = url # 添加超链接
value_cell.font = Font(color="0000FF", underline="single")  # 设置为蓝色并带下划线
```

#### pillow（图像处理）

图像处理库
`pip install pillow`

Image 是 Pillow 最常用的类

##### 创建图像实例

1. **通过文件创建 Image 对象**

```python
from PIL import Image

image = Image.open('python-logo.png')  # 创建图像实例
# 查看图像实例的属性
# format 图像格式;size 图像的 (宽,高) 元组;mode 常见模式，默认 RGB 真彩图像
print(image.format, image.size, image.mode)

image.show() # 显示图像
```

```python
Image.open('python-logo.png').convert('L') # RGB、L灰度图
rotated_image = image.rotate(45)  # 旋转45度
默认旋转中心是图像的中心，逆时针旋转。如果需要顺时针旋转，可以传递负角度。
```

2. 从打开文件中读取
   可以从文件对象读取而不是文件名，但文件对象必须实现 read( ) ，seek( ) 和 tell( ) 方法，并且是以二进制模式打开。

```python
from PIL import Image
with open("hopper.ppm", "rb") as fp:
    im = Image.open(fp)
```

1. 从 string 二进制流中读取
   要从字符串数据中读取图像，需使用 io 类：

```python
import io
from PIL import Image

im = Image.open(io.StringIO(buffer))
```

注意：在读取图像 header 之前将文件倒回（使用 seek(0) ）。

1. 从tar文件中读取

```python
from PIL import TarIO

fp = TarIO.TarIO("Imaging.tar", "Imaging/test/lena.ppm")
im = Image.open(fp)
```

##### 读写图像

1. **格式转换并保存图像**

```python
import os
from PIL import Image

image_path='python-logo.png' # 图片位置
f, e = os.path.splitext(image_path) # 获取文件名与后缀
outfile = f + ".jpg"
if image_path != outfile:
    try:
        Image.open(image_path).save(outfile) # 修改文件格式
    except IOError:
        print("cannot convert", image_path)
```

如果图片mode是RGBA那么会出现异常,因为 JPG 不支持透明度。要么丢弃Alpha , 要么保存为.png
save() 函数有两个参数，如果文件名没有指定图片格式，那么第二个参数是必须的，他指定图片的格式

2. 创建缩略图

```python
import os
from PIL import Image

image_path = 'python-logo.png'  # 图片位置
size = (128, 128)  # 文件大小
f, e = os.path.splitext(image_path)  # 获取文件名与后缀
outfile = f + ".thumbnail"
if image_path != outfile:
    try:
        im = Image.open(image_path)
        im.thumbnail(size)  # 设置缩略图大小
        im.save(outfile, "JPEG")
    except IOError:
        print("cannot convert", image_path)
```

##### 剪贴，粘贴、合并图像

1）**从图像复制子矩形**

```python
box = (100, 100, 400, 400)
region = im.crop(box)
# 图像基于左上角为（0,0）的坐标
# 定义box元组，box 坐标为 (左，上，右，下）。示例中为 300 * 300 像素。
```

2）处理子矩形并将其粘贴回来

```python
region = region.transpose(Image.ROTATE_180) # 颠倒180度
box = (400, 400, 700, 700)  # 粘贴位置，像素必须吻合，300 * 300
im.paste(region, box)
```

3）**分离和合并通道**
Pillow 允许处理图像的各个通道，例如RGB图像有R、G、B三个通道。 split 方法分离图像通道，如果图像为单通道则返回图像本身。merge 合并函数采用图像的 mode 和 通道元组为参数，将它们合并成新图像。

```python
r, g, b = im.split()
im = Image.merge("RGB", (b, g, r))
```

##### 几何变换

PIL.Image.Image 包含调整图像大小 resize() 和旋转 rotate() 的方法。前者采用元组给出新的大小，后者采用逆时针方向的角度。

```python
# 调整大小为(128, 128)
out = im.resize((128, 128))
# 逆时针旋转 45度
out = out.rotate(45)
# 水平左右翻转 Image.FLIP_TOP_BOTTOM/Image.ROTATE_90/Image.ROTATE_180
im.transpose(Image.FLIP_LEFT_RIGHT)
```

##### 颜色变换

```python
im = Image.open("hopper.ppm").convert("L") # 转换为灰阶图像
```

##### 图像增强

1）Filters 过滤器
ImageFilter 模块有很多预定义的增强过滤器

```python
from PIL import ImageFilter
out = im.filter(ImageFilter.DETAIL)
```

2）像素点处理
point() 方法可用于转换图像的像素值（如对比度），在大多数情况下，可以将函数对象作为参数传递格此方法，它根据函数返回值对每个像素进行处理。

```python
# 每个像素点扩大1.2倍
out = im.point(lambda i: i * 1.2)
```

3）处理单独通道

```python
# 将通道分离
source = im.split()
R, G, B = 0, 1, 2

# 选择红色小于100的区域
mask = source[R].point(lambda i: i < 100 and 255)
# 处理绿色
out = source[G].point(lambda i: i * 0.7)
# 粘贴已处理的通道，红色通道仅限于<100
source[G].paste(out, None, mask)
# 合并图像
im = Image.merge(im.mode, source)
```

4）高级增强
其他图像增强功能可以使用 ImageEnhance 模块中的类。从图像创建后，可以使用 ImageEnhance 快速调整图片的对比度、亮度、饱和度和清晰度。

```python
from PIL import ImageEnhance

enh = ImageEnhance.Contrast(im)  # 创建调整对比度对象
# 参数是一个浮点数。1.0是原始图像，更高的值增加对比度，更低的值降低。
enh.enhance(1.3).show() # 增加30%对比度

# ImageEnhance.Contrast(im) 对比度  
# ImageEnhance.Color(im) 色彩饱和度  
# ImageEnhance.Brightness(im) 亮度  
# ImageEnhance.Sharpness(im) 清晰度
```

##### 动态图像

Pillow 支持一些动态图像处理（如FLI/FLC，GIF等格式）。TIFF文件同样可以包含数帧图像。
打开动态图像时，PIL 会自动加载序列中的第一帧。你可以使用 seek 和 tell 方法在不同的帧之间移动。

```python
from PIL import Image

im = Image.open("animation.gif")
im.seek(1) # 跳到第二帧

try:
    while 1:
        im.seek(im.tell()+1)  # tell() 获取当前帧的索引号
except EOFError: # 当读取到最后一帧时，Pillow抛出EOFError异常。
    pass # 结束
```

```python
# 保存动态图像
im.save(out, save_all=True, append_images=[im1, im2, ...])
```

##### ImageDraw

ImageDraw 用于在图像上直接绘制文本、形状等内容。

```python
from PIL import Image, ImageDraw, ImageFont

# 打开图像
im = Image.open("test.jpg")

# 创建 ImageDraw 对象
draw = ImageDraw.Draw(im)

# 设置字体并绘制文本
try:
    font = ImageFont.truetype("arial.ttf", 40)  # 字体文件路径和字号
except IOError:
	# 回退到默认字体，默认字体可以通过default_font.font_variant(size=20)调整字号
    font = ImageFont.load_default()

title = "Hello, Pillow!"
# 在 (10, 10) 处绘制文本，默认颜色为白色
draw.text((10, 10), title, fill="red", font=font)

# 显示图像
im.show()
```

##### PSDraw

PSDraw 用于生成 PostScript 文件。PostScript 是一种页面描述语言，常用于打印和出版领域。
不过一般直接使用ImageDraw

```python
from PIL import Image
from PIL import PSDraw

im = Image.open("test.jpg")
# 定义要绘制的标题文本
title = "hopper"
# 定义了图像绘制的区域，单位为点（1 点 = 1/72 英寸）
box = (1*72, 2*72, 7*72, 10*72)

# 创建一个 PostScript 绘图对象，默认输出到标准输出（`sys.stdout`）
## 可以改成 `PSDraw.PSDraw(f)` 输出到文件
## 或者在控制台输入 `python test.py >  output.ps` 重定向输出到文件
## 再使用 PostScript 查看器（如 Ghostscript）打开生成的output.ps文件查看
ps = PSDraw.PSDraw()

# 开始一个新的 PostScript 文档，并设置文档标题
ps.begin_document(title)

# 在指定的 box 区域内绘制图像，分辨率为 75 DPI
ps.image(box, im, 75)
# 在图像周围绘制一个矩形框
ps.rectangle(box)

# 设置字体为 HelveticaNarrow-Bold，字号为 36 点
ps.setfont("HelveticaNarrow-Bold", 36)
# 在坐标 (3*72, 4*72) 处绘制标题文本
ps.text((3*72, 4*72), title)
```

##### 配置加载器 draft

某些解码器允许在从文件中读取图像时对其进行操作。这通常可用于创建缩略图时（当速度比质量更重要）加速解码并打印到单色激光打印机（仅需灰阶图像时）。

draft() 方法操作已打开但尚未加载的图像，使其尽可能匹配给定的模式和大小。它通过重新配置图像解码器来完成。仅适用于JPEG和MPO文件。使用 draft() 快速解码图像：

```python
from PIL import Image

im = Image.open('test.jpg')
print("original =", im.mode, im.size)

im.draft("L", (100, 100))
print("draft =", im.mode, im.size)
```

### 图形界面GUI

使用标准库 [[#tkinter]] ，可以绘制简单的GUI

小型项目和原型开发：wxPython；大型项目和商业应用：PyQt；跨平台和兼容性：PyGTK

#### pyqt5（Qt）

PyQt是一个功能强大的Python绑定库，可以与Qt图形库协同工作。Qt是一种跨平台的应用程序和界面框架，提供了丰富的图形控件、布局管理、事件处理和网络功能等。PyQt使用Qt的C++库将其封装成Python可用的模块，为Python开发者提供了创建功能丰富的GUI应用程序的能力。

PyQt5 不再提供常用Qt工具，比如**图形界面开发工具Qt Designer**、国际化翻译工具Liguist 如果开发中使用到这些，必须自行安装Qt工具(PyQt5-tools)。

下面给出了常用模块的列表 −

- **QtCore** − 其他模块使用的核心非 GUI 类
- **QtGui** − 图形用户界面组件
- **QtMultimedia** − 低级多媒体编程类
- **QtNetwork** − 网络编程类
- **QtOpenGL** − OpenGL 支持类
- **QtScript** − 用于评估 Qt 脚本的类
- **QtSql** − 使用 SQL 进行数据库集成的类
- **QtSvg** − 显示 SVG 文件内容的类
- **QtWebKit** − 用于呈现和编辑 HTML 的类
- **QtXml** − 处理 XML 的类
- **QtWidgets** − 用于创建经典桌面风格 UI 的类
- **QtDesigner** − 用于扩展 Qt Designer 的类

PyQt 兼容所有流行的操作系统，包括 Windows、Linux 和 Mac OS。

**Canvas 组件支持以下标准选项：**

arc − 创建一个扇形

```py
coord =10,50,240,210
arc = canvas.create_arc(coord, start=0, extent=150, fill="blue")
```

image − 创建图像

```py
filename =PhotoImage(file ="sunshine.gif")
image = canvas.create_image(50,50, anchor=NE, image=filename)
```

line − 创建线条

```py
line = canvas.create_line(x0, y0, x1, y1,..., xn, yn, options)
```

oval − 创建一个圆

```py
oval = canvas.create_oval(x0, y0, x1, y1, options)
```

polygon − 创建一个至少有三个顶点的多边形

```py
oval = canvas.create_polygon(x0, y0, x1, y1,...xn, yn, options)
```

#### wxPython（wxWidgets）

wxPython是一个开源的Python绑定库，能够让Python开发者使用wxWidgets框架创建GUI应用程序。wxWidgets是一个跨平台的C++应用程序框架，提供了大量的GUI控件和工具，可以在多个平台上构建本地界面。

#### PyGTK（GTK+）

PyGTK是一个用于Python的GTK+绑定库，允许Python开发者使用GTK+工具包创建GUI应用程序。GTK+是一个世界知名的开源GUI开发工具包，被广泛应用于Linux桌面环境和GNOME桌面环境。

#### Kivy

Kivy 是一个用于开发跨平台应用程序的 Python 框架
可以使用[[#Buildozer]]打包apk

Kivy 默认使用英文字体，因此需要手动指定支持中文的字体文件：
将字体文件（如 [msyh.ttf](msyh.ttf)）放入你的 Kivy 项目目录中

```python
from kivy.app import App
from kivy.uix.label import Label
from kivy.core.text import LabelBase

# 注册中文字体
LabelBase.register(name='ChineseFont', fn_regular='msyh.ttf')

class MyApp(App):
    def build(self):
        # 使用中文字体
        return Label(text="你好，Kivy！", font_name='ChineseFont')
	
	def show_popup(self, instance):
		# 创建 Popup
		popup = Popup(
			title="你好，Kivy！",  # 设置标题
			title_font='ChineseFont',  # 设置标题字体
			content=Label(text="这是一个弹窗。"),  # 设置内容
			size_hint=(0.8, 0.4)  # 设置大小
		)
		popup.open()

if __name__ == "__main__":
    MyApp().run()
```

**BeeWare**
**Flet**

### 游戏开发

  Panda3D
  cocos2d

#### Pygame

Pygame是一个流行的Python库，用于开发视频游戏。它是免费的、开源的、跨平台的简单直接媒体库（SDL）的封装器。Pygame提供的SDL功能的抽象化使得使用Python开发多媒体应用程序变得非常容易。

每个游戏的核心都是一个循环，将其称为“游戏循环”。这个循环一直在不断运行，一遍又一遍地完成游戏工作所需的所有事情。每次循环显示一次游戏当前画面，称为帧。
FPS（Frames Per Second）代表每秒帧数，也叫帧率。这意味着游戏循环每秒应发生多少次。
Pygame游戏循环，主要是：处理外部输入；更新游戏对象位置或状态；渲染

pygame默认是采用的笛卡尔坐标系。左上角的顶点是(0,0)

```python
import pygame

pygame.init()  # 初始化 pygame 模块
pygame.mixer.init() #声音初始化

WIDTH = 360  # 游戏窗口的宽度
HEIGHT = 480 # 游戏窗口的高度
FPS = 30 # 帧率
# # 获取当前屏幕分辨率
# screen_info = pygame.display.Info()
# SCREEN_WIDTH = screen_info.current_w
# SCREEN_HEIGHT = screen_info.current_h

# pygame.Color(r, g, b, a=255)
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)

screen = pygame.display.set_mode((WIDTH, HEIGHT))  # 初始化显示窗口并设置尺寸
# screen = pygame.display.set_mode((0, 0), pygame.FULLSCREEN) # 全屏显示
pygame.display.set_caption("Hello World")  # 设置游戏窗口标题栏文字
# icon = pygame.image.load("icon.png").convert_alpha()
# pygame.display.set_icon(icon) # 设置窗口的新图标
# background = pygame.image.load("background.jpg")
# screen.blit(background, (0, 0)) # 设置背景图片
# pygame.display.flip()

clock = pygame.time.Clock() # 创建一个clock时钟对象

# 游戏循环
running = True
while running:
	# 设置FPS为30
    clock.tick(FPS)

    for event in pygame.event.get():  # 从Pygame的事件队列中取出事件
        if event.type == pygame.QUIT:  # 获得事件类型，并逐类响应
			# 退出游戏，也可以使用sys.exit()强制退出程序
            running = False 
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:  # 按ESC退出
                running = False
			
	screen.fill(BLACK) # 填充背景色（可选）
	# draw
    pygame.display.update()  # 可更新指定区域（默认更新所有修改过的区域）
    # pygame.display.flip() # 强制更新整个屏幕（所有像素）

# 关闭 Pygame 库的函数。确保所有 Pygame 模块都被正确地取消初始化
pygame.quit()
```

```python
# 屏幕尺寸和模式
pygame.display.set_mode(size, flags, depth, display, vsync)
pygame.display.Info()
# 窗口标题和图标
pygame.display.set_caption()
pygame.display.set_icon()
pygame.display.get_caption()
# 图标的感知和刷新
pygame.display.get_active()
pygame.display.flip()
pygame.display.update()

# 加载图片
pygame.image.load()

screen.fill(color) # 显示窗口背景填充为color颜色，采用RGB色彩体系
screen.blit(src, dest) #将一个图像绘制在另一个图像上，即将src绘制到dest位置上
```

###### 精灵

2D游戏能屏幕上看到的所有对象都是精灵。在Pygame中，精灵是对象类型。

Pygame精灵都必须拥有两个属性： `image` （外观）和 `rect` （矩形坐标）

```python
class Player(pygame.sprite.Sprite):
    def __init__(self):
        # 调用父类的初始化方法
		super().__init__()
		# 创建一个简单的50 x 50正方形并用颜色填充
        self.image = pygame.Surface((50, 50))
        self.image.fill(GREEN)
		# 将精灵放在屏幕中心
        self.rect = self.image.get_rect() # 包围image的矩形
        self.rect.center = (WIDTH / 2, HEIGHT / 2)
	
    def update(self):
        self.rect.x += 5
        if self.rect.left > WIDTH:
            self.rect.right = 0
```

精灵组是精灵的集合，可以同时对所有精灵进行操作。

```python
# 创建精灵组
all_sprites = pygame.sprite.Group()
# 实例化
player = Player()
# 把添加进精灵组
all_sprites.add(player)

while running:
	pass
	# 刷新精灵组
	all_sprites.update()
	# 把精灵组绘制在屏幕上
	all_sprites.draw(screen)
	pass
```

设置图片为精灵的image
*一般把游戏资源保存在文件夹如img中*

```python
import pygame
import os

# 获得当前代码文件所在的文件夹路径
game_folder = os.path.dirname(__file__)
# 获得img文件夹
img_folder = os.path.join(game_folder, 'img')
# 获得p1_jump.png图片
player_img = pygame.image.load(os.path.join(img_folder, 'p1_jump.png')).convert()

class Player(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
		# 设置图片为精灵的image
        self.image = player_img
		# 设置角色的初始位置
        self.rect = self.image.get_rect(center=(WIDTH//2, HEIGHT//2))
	
	# 精灵移动时同步移动图片image
    def display(self, screen):
        screen.blit(self.image, self.rect)
	# 精灵旋转时同步旋转图片image
	def rotate(self, angle):
        self.image = pygame.transform.rotate(self.image, angle)
        self.rect = self.image.get_rect(center=self.rect.center)
```

`ballrect.move(x,y)`矩形移动一个偏移量(x,y)，即在横轴方向移动x像素，纵轴方向移动y像素

**碰撞检测函数** spritecollide(sprite, group, dokill, collided = None) -> Sprite_list

##### 事件

事件本质上是一种封装后的数据类型（对象）
`pygame.event.EventType` 是Pygame的一个类，表示事件类型

```python
while True:
   for event in pygame.event.get():
      if event.type == pygame.QUIT:
         pygame.quit()
         sys.exit()
      if event.type == pygame.KEYDOWN:
         key = pygame.key.name(event.key)
         print (key, "Key is pressed")
         if event.key == pygame.K_UP:
             print('↑')
```

**pygame.QUIT 事件**
用户点击“关闭”按钮的事件，但一般情况下，它并不会自动关闭，有时可能出现未响应的情况，除非我们关闭Python。

**键盘事件**
pygame.KEYDOWN 按下键盘
pygame.KEYUP 释放键盘

event.key

| 按键 | 名称            |
| ---- | --------------- |
| ↑   | pygame.K_UP     |
| ↓   | pygame.K_DOWN   |
| ←   | pygame.K_LEFT   |
| →   | pygame.K_RIGHT  |
| 空格 | pygame.K_SPACE  |
| esc  | pygame.K_ESCAPE |

| pygame.key.get_pressed()      | 获取所有键盘按钮的状态         |
| ----------------------------- | ------------------------------ |
| pygame.key.get_mods()         | 确定哪些修改键正在被按下       |
| pygame.key.set_repeat()       | 控制被按下的键的重复方式       |
| pygame.key.get_repeat()       | 查看持有的按键是如何重复的     |
| pygame.key.name()             | 获取一个键的标识符的名称。     |
| pygame.key.key_code()         | 从一个键的名称中获取键的标识符 |
| pygame.key.start_text_input() | 开始处理Unicode文本输入事件    |
| pygame.key.stop_text_input()  | 停止处理Unicode文本输入事件    |

```python
while True:
	for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
			# 检测按下事件，实现点击跳跃
	         if event.key == pygame.K_SPACE:
				player.jump()

    # 实时检测键盘状态，实现长按移动
    keys = pygame.key.get_pressed()
    if keys[pygame.K_a]:
        player.moveLeft()
    if keys[pygame.K_d]:
        player.moveRight()
```

```python
# 强制捕获键盘事件:
pygame.event.set_grab(True)  # 强制捕获所有输入事件
pygame.key.set_repeat(100, 50)  # 启用按键重复（100ms 延迟，50ms 间隔）

# 某些输入法（如中文输入法）可能会拦截键盘事件
```

**鼠标事件**
MOUSEBUTTONDOWN 按下鼠标
MOUSEBUTTONUP 释放鼠标
MOUSEMOTION 划过窗口

要精确到是左击还是右击，需要用到pygame.mouse.get_pressed()函数，它返回的是一个列表。其中第一项（索引[0]）是代表左键是否按下，第三项（索引[2]）是代表右键是否按下，它们的值都是布尔运算值
获取鼠标位置，要用event.pos方法，得到的是一个表示坐标的元组

```python
if event.type == pygame.MOUSEMOTION:
   pos=event.pos # 或者pos=pygame.mouse.get_pos()
   print ("x = {}, y = {}".format(pos[0], pos[1]))
```

| pygame.key.get_pressed           | 获取鼠标按键的状态             |
| -------------------------------- | ------------------------------ |
| pygame.mouse.get_pos()           | 获取鼠标光标的位置             |
| pygame.mouse.get_rel()           | 获取鼠标的移动量               |
| pygame.mouse.set_pos()           | 设置鼠标光标的位置             |
| pygame.mouse.set_visible()       | 隐藏或显示鼠标光标             |
| pygame.mouse.get_visible()       | 获取鼠标光标的当前可见状态。   |
| pygame.mouse.get_focused()       | 检查显示器是否正在接收鼠标输入 |
| pygame.mouse.set_cursor()        | 设置鼠标光标的图像             |
| pygame.mouse.set_system_cursor() | 将鼠标光标设置为一个系统变体   |

Pygame定义了以下系统光标：

| pygame.SYSTEM_CURSOR_ARROW     | 箭头                       |
| ------------------------------ | -------------------------- |
| pygame.SYSTEM_CURSOR_IBEAM     | i-beam                     |
| pygame.SYSTEM_CURSOR_WAIT      | wait                       |
| pygame.SYSTEM_CURSOR_CROSSHAIR | 十字线                     |
| pygame.SYSTEM_CURSOR_SIZENWSE  | 指向西北和东南的双箭头     |
| pygame.SYSTEM_CURSOR_SIZENESW  | 指向东北方和西南方的双箭头 |
| pygame.SYSTEM_CURSOR_SIZEWE    | 指向西方和东方的双箭头     |
| pygame.SYSTEM_CURSOR_SIZENS    | 指向南北的双箭头           |
| pygame.SYSTEM_CURSOR_SIZEALL   | 四个箭头                   |
| pygame.SYSTEM_CURSOR_NO        | 划线的圆圈或十字骨         |
| pygame.SYSTEM_CURSOR_HAND      | 手                         |

```python
# 设置游戏窗口的光标为十字线
pygame.mouse.set_cursor(pygame.SYSTEM_CURSOR_CROSSHAIR)
```

##### 其他

绘制图形：
任何一个图形绘制后，会返回一个矩形Rect类表示该形状
pygame.Rect  表达一个矩形区域的类，用于存储坐标和长度信息Pygame利用Rect类来操作图形/图像等元素 四个参数 left，top，width，height

```python
pygame.draw.rect(screen, red, pygame.Rect(100, 30, 60, 60), width=0)
pygame.draw.polygon(screen, blue, ((25,75),(76,125),(275,200),(350,25),(60,280)), width=0)
pygame.draw.circle(screen, white, (180,180), 60, width=0)
pygame.draw.ellipse(screen, green, (250, 200, 130, 80), width=0) 
pygame.draw.line(screen, red, (10,200), (300,10), 4, width=1)
# arc/lines/aaline/aalines
```

```python
img = pygame.image.load('pygame.png')
while True:
	pass
	rect = img.get_rect()
	rect.center = 200, 150
	screen.blit(img, rect)
```

`pygame.image.save(screen, "circles.png")` 可以将Surface对象的内容保存到一个图像文件中

显示文本：

当前机器中安装的字体列表可以通过 `fonts = pygame.font.get_fonts()` 获得

```python
font = pygame.font.SysFont(none, 36) # none指默认字体，可以指定主体如"Arial"
font1 = pygame.font.SysFont('chalkduster.ttf', 72) # 字体文件也可以
txtsurf = font.render('Hello World', True, BLUE)
while True:
	pass
	screen.blit(txtsurf,(WIDTH - txtsurf.get_width() // 2, HEIGHT - txtsurf.get_height() // 2))
```

| bold()          | 获取或设置字体是否应该以黑体呈现。     |
| --------------- | -------------------------------------- |
| italic()        | 获取或设置字体是否应该以斜体形式呈现。 |
| underline()     | 获取或设置字体是否应以下划线呈现。     |
| render()        | 在一个新的Surface上绘制文本            |
| size()          | 计算渲染文字所需的尺寸                 |
| set_underline() | 控制是否用下划线来渲染文本             |
| get_underline() | 检查文本是否带下划线。                 |
| set_bold()      | 启用加粗文本的假渲染                   |
| get_bold()      | 检查文本是否会被渲染成粗体             |
| set_italic()    | 启用斜体文字的假渲染                   |
| metrics()       | 获取每个字符的度量值                   |
| get_italic()    | 检查文本是否会被渲染成斜体             |
| get_linesize()  | 获取字体文本的行间距                   |
| get_height()    | 获取字体的高度                         |
| get_ascent()    | 获取字体的上升高度                     |
| get_descent()   | 获取字体的下降值                       |

Rect

| copy()              | 返回一个新的矩形，其位置和大小与原矩形相同。                           |
| ------------------- | ---------------------------------------------------------------------- |
| move()              | 返回一个按给定偏移量移动的新矩形。x和y参数可以是任何整数，正数或负数。 |
| move_ip()           | 与Rect.move()方法相同，但在原地操作。                                  |
| inflate(x,y)        | 返回一个新的矩形，其大小由给定的偏移量改变。负值会缩小矩形。           |
| inflate_ip(x, y)    | 和Rect.inflate()方法一样，但在原地操作。                               |
| clamp(Rect)         | 返回一个新的矩形，该矩形被移动到完全在参数Rect的内部。                 |
| clip(Rect)          | 返回一个新的矩形，该矩形被裁剪成完全在参数 Rect 内。                   |
| union(Rect)         | 返回一个新的矩形，该矩形完全覆盖两个提供的矩形的面积。                 |
| union_ip(Rect)      | 与 Rect.union() 方法相同，但在原地操作。                               |
| contains(Rect)      | 当参数完全在Rect里面时返回true。                                       |
| collidepoint((x,y)) | 如果给定的点在矩形内，返回真。                                         |
| colliderect(Rect)   | 如果两个矩形的任何部分重叠，返回真。                                   |

ransform

| flip()                    | 垂直和水平方向的翻转                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------- |
| scale()                   | 调整大小到新的分辨率                                                                                    |
| rotate()                  | 旋转一个图像                                                                                            |
| rotozoom()                | 缩放和旋转的过滤                                                                                        |
| scale2x()                 | 专门的图像倍增器                                                                                        |
| smoothscale()             | 将一个曲面平滑地扩展到一个任意的尺寸                                                                    |
| get_smoothscale_backend() | 返回正在使用的smoothscale过滤器的版本 – ‘GENERIC’, ‘MMX’, or ‘SSE’ 。                            |
| set_smoothscale_backend() | 设置平滑尺度过滤器的版本为 – ‘GENERIC’, ‘MMX’, 或 ‘SSE’之一。                                    |
| chop()                    | 获取一个去除内部区域的图像的副本                                                                        |
| laplacian()               | 查找曲面中的边缘                                                                                        |
| average_surfaces()        | 从许多表面中找出平均的表面。                                                                            |
| Average_color()           | 找出一个曲面的平均颜色                                                                                  |
| threshold()               | 找出一个曲面中哪些像素在 “search_color “或 “search_surf “的阈值范围内，以及有多少像素在阈值范围内。 |

声音对象
混合器通道

##### Pygame小游戏

###### 人物移动射击

```python
import pygame
import math
import random

pygame.init()
SCREEN_WIDTH, SCREEN_HEIGHT = 480, 360
FPS = 30
# 获取当前屏幕分辨率
screen_info = pygame.display.Info()
SCREEN_WIDTH = screen_info.current_w
SCREEN_HEIGHT = screen_info.current_h

# 颜色定义
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)
YELLOW = (255,255,0)
CYAN = (0,255,255)
GRAY = (128, 128, 128)

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Player Movement Demo")
clock = pygame.time.Clock()

# 加载字体
font = pygame.font.Font(None, 36)

class Platform(pygame.sprite.Sprite):
    '''
    平台
    '''
    def __init__(self, x, y, width, height):
        super().__init__()
        self.image = pygame.Surface((width, height))
        self.image.fill(GRAY)
        self.rect = self.image.get_rect()
        self.rect.x = x
        self.rect.y = y

class Player(pygame.sprite.Sprite):
    '''
    玩家
    '''
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill(GREEN)
		# 设置角色的初始位置
        self.rect = self.image.get_rect(center=(SCREEN_WIDTH//2, SCREEN_HEIGHT//2))
        # 设置角色的初始速度和加速度
        self.velocity_x = 0                 # 水平速度
        self.acceleration_x = 0.5           # 水平加速度
        self.frictionAacceleration_x = 0.1  # 水平摩擦力加速度
        self.max_velocity = 5               # 最大速度
        self.velocity_y = 0                 # 垂直速度
        self.acceleration_y = 1             # 重力加速度
        self.jump_velocity = -15  # 跳跃速度
        self.on_ground = False  # 是否在地面上
        self.max_jump_count = 2 # 最大跳跃次数
        self.jump_count = self.max_jump_count # 剩余跳跃次数

    def jump(self):
        if self.jump_count > 0:  # 如果还有跳跃次数
            self.velocity_y = self.jump_velocity
            self.jump_count -= 1  # 减少跳跃次数
            self.on_ground = False  # 标记为不在平台上
	
    def moveLeft(self):
        self.velocity_x = max(-self.max_velocity, self.velocity_x - self.acceleration_x)
        self.rect.x += self.velocity_x

    def moveRight(self):
        self.velocity_x = min(self.max_velocity, self.velocity_x + self.acceleration_x)
        self.rect.x += self.velocity_x

    def update(self):
        # 更新角色的位置和速度
        self.velocity_y += self.acceleration_y
        self.rect.y += self.velocity_y
        # 控制角色不超出屏幕边缘
        if self.rect.y >= SCREEN_HEIGHT - self.rect.height:
            self.rect.y = SCREEN_HEIGHT - self.rect.height
            self.velocity = 0
        # 模拟摩擦力（逐渐减速）
        if self.velocity_x > 0:
            self.velocity_x = max(0, self.velocity_x - self.frictionAacceleration_x)
        elif self.velocity_x < 0:
            self.velocity_x = min(0, self.velocity_x + self.frictionAacceleration_x)

        # 边界检测（水平方向）
        # 如果角色超出左边界
        if self.rect.left < 0:
            self.rect.left = 0  # 限制位置
            self.velocity_x = -self.velocity_x  # 反转速度
        # 如果角色超出右边界
        if self.rect.right > SCREEN_WIDTH:
            self.rect.right = SCREEN_WIDTH  # 限制位置
            self.velocity_x = -self.velocity_x  # 反转速度

        # 碰撞检测（与平台）
        self.on_ground = False
        for platform in platforms:
            if self.rect.colliderect(platform.rect):
                if self.velocity_y > 0:  # 下落时碰到平台
                    self.rect.bottom = platform.rect.top
                    self.velocity_y = 0
                    self.on_ground = True
                    self.jump_count = self.max_jump_count
                elif self.velocity_y < 0:  # 上升时碰到平台
                    self.rect.top = platform.rect.bottom
                    self.velocity_y = 0

class Bullet(pygame.sprite.Sprite):
    '''
    子弹
    '''
    def __init__(self, start_x, start_y, target_x, target_y, colour, damage, radius, velocity):
        super().__init__()
        self.damage = damage
        self.radius = radius  # 子弹半径
        self.gravity = 0 # 重力加速度
        self.velocity = velocity
        self.image = pygame.Surface((self.radius * 2, self.radius * 2), pygame.SRCALPHA)
        pygame.draw.circle(self.image, colour, (self.radius, self.radius), self.radius)
        self.rect = self.image.get_rect(center=(start_x, start_y))
      
        # 计算子弹飞行方向
        dx = target_x - start_x
        dy = target_y - start_y
        distance = math.hypot(dx, dy)  # 计算两点间距离
        if distance == 0:
            self.velocity_x = 0
            self.velocity_y = 0
        else:
            self.velocity_x = dx / distance * self.velocity  # 速度向量
            self.velocity_y = dy / distance * self.velocity

    def update(self):
        self.rect.x += self.velocity_x
        self.rect.y += self.velocity_y
        # 应用重力
        self.velocity_y += self.gravity
        # 如果子弹飞出屏幕，移除它
        if self.rect.right < 0 or self.rect.left > SCREEN_WIDTH or self.rect.bottom < 0 or self.rect.top > SCREEN_HEIGHT:
            self.kill()

class Enemy(pygame.sprite.Sprite):
    '''
    敌人
    '''
    def __init__(self, health):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface((40, 40))
        self.image.fill(YELLOW)
        self.rect = self.image.get_rect()
        self.rect.x = random.randint(0, SCREEN_WIDTH - self.rect.width)
        self.rect.y = random.randint(50, 200)
        self.health = health  # 敌人生命值
        self.velocity_x = random.choice([-1, 1]) * random.uniform(0.5, 2)  # 随机水平速度
        self.velocity_y = random.uniform(0.5, 1)  # 随机垂直速度

    def update(self):
        # 随机移动
        self.rect.x += self.velocity_x
        self.rect.y += self.velocity_y
      
        # 边界检测
        if self.rect.left < 0 or self.rect.right > SCREEN_WIDTH:
            self.velocity_x = -self.velocity_x  # 反转水平方向
        if self.rect.top < 0 or self.rect.bottom > SCREEN_HEIGHT:
            self.velocity_y = -self.velocity_y  # 反转垂直方向

        # 碰撞检测（与平台）
        self.on_ground = False
        for platform in platforms:
            if self.rect.colliderect(platform.rect):
                if self.velocity_y > 0:  # 下落时碰到平台
                    self.rect.bottom = platform.rect.top
                    self.velocity_y = 0
                    self.on_ground = True
                elif self.velocity_y < 0:  # 上升时碰到平台
                    self.rect.top = platform.rect.bottom
                    self.velocity_y = 0

player = Player()
all_sprites = pygame.sprite.Group(player)
bullets = pygame.sprite.Group()  # 子弹组
enemies = pygame.sprite.Group()  # 敌人组
platforms = pygame.sprite.Group()  # 平台组
max_bullets = 10  # 最大子弹数量
score = 0  # 初始得分

# 创建平台
platforms.add(Platform(0, SCREEN_HEIGHT - 40, SCREEN_WIDTH, 40))  # 底部平台
platforms.add(Platform(SCREEN_WIDTH // 2 - 50, SCREEN_HEIGHT - 150, 100, 20))  # 中间平台
platforms.add(Platform(100, SCREEN_HEIGHT - 250, 100, 20))  # 顶部平台
all_sprites.add(platforms)

# 敌人生成计时器
max_enemies = 6
enemy_spawn_time = 0
enemy_spawn_interval = 2000  # 每 2 秒生成一个敌人（单位：毫秒）

running = True
while running:
    clock.tick(FPS)
  
    # 处理事件
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE or event.key == pygame.K_w or event.key == pygame.K_UP:
                player.jump()
            elif event.key == pygame.K_ESCAPE:  # 按下 ESC 键
                running = False
        elif event.type == pygame.MOUSEBUTTONDOWN:  # 鼠标点击事件
            if event.button == 1:  # 左键点击
                # 获取鼠标点击位置
                mouse_x, mouse_y = event.pos
                # 检查子弹数量
                if len(bullets) < max_bullets:
                    # 发射子弹
                    bullet = Bullet(player.rect.centerx, player.rect.centery, mouse_x, mouse_y, RED, 1, 5, 20)
                    all_sprites.add(bullet)
                    bullets.add(bullet)
            if event.button == 3:  # 右键点击
                # 获取鼠标点击位置
                mouse_x, mouse_y = event.pos
                # 检查子弹数量
                if len(bullets) < max_bullets:
                    # 发射子弹
                    bullet = Bullet(player.rect.centerx, player.rect.centery, mouse_x, mouse_y, BLUE, 2, 10, 10)
                    all_sprites.add(bullet)
                    bullets.add(bullet)
  
    # 实时检测键盘状态
    keys = pygame.key.get_pressed()
    if keys[pygame.K_a] or keys[pygame.K_LEFT]:
        player.moveLeft()
    if keys[pygame.K_d] or keys[pygame.K_RIGHT]:
        player.moveRight()

    # 更新精灵逻辑
    all_sprites.update()

    # 检测子弹与敌人的碰撞
    hits = pygame.sprite.groupcollide(bullets, enemies, True, False)
    for bullet, enemy_list in hits.items():
        for enemy in enemy_list:
            enemy.health -= bullet.damage  # 减少敌人生命值
            if enemy.health <= 0:  # 如果敌人生命值为 0
                enemy.kill()  # 移除敌人
                score += 10  # 增加得分

    # 随时间生成敌人
    current_time = pygame.time.get_ticks()
    if current_time - enemy_spawn_time > enemy_spawn_interval:
        if len(enemies) < max_enemies:
            enemy = Enemy(3)
            all_sprites.add(enemy)
            enemies.add(enemy)
        enemy_spawn_time = current_time  # 重置计时器
  
    # 清屏 + 绘制
    screen.fill(WHITE)
    all_sprites.draw(screen)
    # 绘制得分
    score_text = font.render(f"Score: {score}", True, BLACK)
    screen.blit(score_text, (10, 10))
  
    pygame.display.flip()

pygame.quit()
```

###### Flappy Bird

```python
import pygame
import random

pygame.init()
SCREEN_WIDTH, SCREEN_HEIGHT = 360, 512
FPS = 60
# screen_info = pygame.display.Info()
# SCREEN_WIDTH = screen_info.current_w
# SCREEN_HEIGHT = screen_info.current_h

# 颜色定义
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
YELLOW = (255, 255, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)
EARTH_TONE = (199,97,20)

screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Flappy Bird")
clock = pygame.time.Clock()

# 加载字体
font = pygame.font.Font(None, 36)

# 加载图片（使用纯色方块代替图片）
bird_img = pygame.Surface((34, 24))
bird_img.fill(YELLOW)
pipe_img = pygame.Surface((52, 1000))
pipe_img.fill(GREEN)
background_img = pygame.Surface((SCREEN_WIDTH, SCREEN_HEIGHT))
background_img.fill(BLUE)
ground_h = 50
ground_img = pygame.Surface((SCREEN_WIDTH, ground_h))
ground_img.fill(EARTH_TONE)

class Bird(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = bird_img
        self.rect = self.image.get_rect()
        self.rect.center = (SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2)  # 小鸟初始位置在屏幕中间
        self.speed_y = 0
        self.gravity = 0.5
        self.flap_power = -8  # 小鸟上升的力量

    def update(self):
        self.speed_y += self.gravity
        self.rect.y += self.speed_y

        # 限制小鸟移动范围
        if self.rect.top < 0:
            self.rect.top = 0
        if self.rect.bottom > SCREEN_HEIGHT - ground_h:  # 地面高度
            self.rect.bottom = SCREEN_HEIGHT - ground_h
            self.speed_y = 0

    def flap(self):
        self.speed_y = self.flap_power  # 向上飞

class Pipe(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pipe_img
        self.rect = self.image.get_rect()
        self.rect.x = SCREEN_WIDTH
        self.passed = False  # 标记小鸟是否已通过该管道

    def update(self):
        self.rect.x -= 3  # 管道向左移动
        if self.rect.right < 0:  # 管道移出屏幕后移除
            self.kill()

# 创建精灵组
all_sprites = pygame.sprite.Group()
pipes = pygame.sprite.Group()

# 创建小鸟
bird = Bird()
all_sprites.add(bird)

# 游戏变量
score = 0
running = True
game_over = False

# 管道生成计时器
pipe_spawn_time = 0
pipe_spawn_interval = 5000  # 每 5 秒生成一对管道（单位：毫秒）

while running:
    clock.tick(FPS)
  
    # 处理事件
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE and not game_over:  # 按下空格键
                bird.flap()
            if event.key == pygame.K_r and game_over:  # 按下 R 键重新开始
                # 重置游戏
                all_sprites.empty()
                pipes.empty()
                bird = Bird()
                all_sprites.add(bird)
                score = 0
                game_over = False
  
    if not game_over:
        # 更新精灵逻辑
        all_sprites.update()

        # 生成管道
        current_time = pygame.time.get_ticks()
        if current_time - pipe_spawn_time > pipe_spawn_interval:
            gap_y = random.randint(SCREEN_HEIGHT // 4, SCREEN_HEIGHT * 3 // 4)  # 随机生成空隙位置
            pipe_top = Pipe()  # 上管道
            pipe_bottom = Pipe()  # 下管道
            gap = 60
            pipe_top.rect.bottom = gap_y - gap  # 上管道底部位置
            pipe_bottom.rect.top = gap_y + gap  # 下管道顶部位置
            all_sprites.add(pipe_top)
            all_sprites.add(pipe_bottom)
            pipes.add(pipe_top)
            pipes.add(pipe_bottom)
            pipe_spawn_time = current_time

        # 检测小鸟与管道的碰撞
        if pygame.sprite.spritecollide(bird, pipes, False):
            game_over = True

        # 检测小鸟掉出屏幕
        if bird.rect.bottom >= SCREEN_HEIGHT - ground_h:  # 地面高度
            game_over = True

        # 检测得分（小鸟通过管道）
        for pipe in pipes:
            if pipe.rect.right < bird.rect.left and not pipe.passed:
                pipe.passed = True
                score += 0.5  # 每对管道得 1 分

    # 清屏 + 绘制
    screen.blit(background_img, (0, 0))  # 绘制背景
    all_sprites.draw(screen)
    screen.blit(ground_img, (0, SCREEN_HEIGHT - ground_h))  # 绘制地面

    # 绘制得分
    score_text = font.render(f"Score: {int(score)}", True, WHITE)
    screen.blit(score_text, (10, 10))

    # 游戏结束画面
    if game_over:
        game_over_text = font.render("Game Over", True, WHITE)
        restart_text = font.render("Press R to Restart", True, WHITE)
        screen.blit(game_over_text, (SCREEN_WIDTH // 2 - 80, SCREEN_HEIGHT // 2 - 50))
        screen.blit(restart_text, (SCREEN_WIDTH // 2 - 100, SCREEN_HEIGHT // 2))

    pygame.display.flip()

pygame.quit()
```

###### 双人乒乓

```python
import pygame
import random

# 初始化pygame
pygame.init()

# 设置窗口大小
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Ping Pong - 2 Player")

# 定义颜色
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)

# 加载字体
font = pygame.font.Font(None, 36)

class Ball(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        # 定义小球属性
        self.ball_radius = 15
        self.image = pygame.Surface((self.ball_radius * 2, self.ball_radius * 2), pygame.SRCALPHA)
        pygame.draw.circle(self.image, RED, (self.ball_radius, self.ball_radius), self.ball_radius)
        self.rect = self.image.get_rect()
        self.reset()  # 初始化小球位置和速度
        self.ball_dx = random.choice([-1, 1]) * random.randrange(3, 5)  # 随机水平速度
        self.ball_dy = random.choice([-1, 1]) * random.randrange(3, 5)  # 随机垂直速度

    def reset(self):
        # 重置小球位置和速度
        self.rect.center = (SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2)
        self.ball_dx = random.choice([-1, 1]) * random.randrange(3, 5)
        self.ball_dy = random.choice([-1, 1]) * random.randrange(3, 5)

    def update(self):
        # 移动小球
        self.rect.x += self.ball_dx
        self.rect.y += self.ball_dy

        # 小球碰撞检测（与屏幕上下边界）
        if self.rect.top <= 0 or self.rect.bottom >= SCREEN_HEIGHT:
            self.ball_dy = -self.ball_dy

class Paddle(pygame.sprite.Sprite):
    def __init__(self, x, y, up_key, down_key):
        super().__init__()
        # 定义挡板属性
        self.paddle_width = 15
        self.paddle_height = 100
        self.image = pygame.Surface((self.paddle_width, self.paddle_height))
        self.image.fill(WHITE)
        self.rect = self.image.get_rect()
        self.rect.center = (x, y)
        self.paddle_speed = 10
        self.up_key = up_key
        self.down_key = down_key

    def update(self):
        # 处理挡板移动
        keys = pygame.key.get_pressed()
        if keys[self.up_key] and self.rect.top > 0:
            self.rect.y -= self.paddle_speed
        if keys[self.down_key] and self.rect.bottom < SCREEN_HEIGHT:
            self.rect.y += self.paddle_speed

def circle_rect_collision(circle, rect):
    """
    检测圆形与矩形的碰撞
    :param circle: 圆形对象（需包含 rect 和 radius 属性）
    :param rect: 矩形对象（需包含 rect 属性）
    :return: 是否碰撞
    """
    # 找到矩形上距离圆心最近的点
    closest_x = max(rect.rect.left, min(circle.rect.centerx, rect.rect.right))
    closest_y = max(rect.rect.top, min(circle.rect.centery, rect.rect.bottom))

    # 计算圆心与最近点的距离
    distance_x = circle.rect.centerx - closest_x
    distance_y = circle.rect.centery - closest_y
    distance_squared = distance_x ** 2 + distance_y ** 2

    # 判断是否碰撞
    return distance_squared < circle.ball_radius ** 2

# 创建精灵组
all_sprites = pygame.sprite.Group()
paddles = pygame.sprite.Group()

# 创建小球和挡板
ball = Ball()
paddle_left = Paddle(30, SCREEN_HEIGHT // 2, pygame.K_w, pygame.K_s)  # 左侧挡板，W/S 控制
paddle_right = Paddle(SCREEN_WIDTH - 30, SCREEN_HEIGHT // 2, pygame.K_UP, pygame.K_DOWN)  # 右侧挡板，上下箭头控制
all_sprites.add(ball)
all_sprites.add(paddle_left)
all_sprites.add(paddle_right)
paddles.add(paddle_left)
paddles.add(paddle_right)

# 得分变量
score_left = 0
score_right = 0

# 游戏主循环
running = True
clock = pygame.time.Clock()
while running:
    clock.tick(60)
    screen.fill(BLACK)

    # 处理事件
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # 更新精灵逻辑
    all_sprites.update()

    # 检测小球与挡板的碰撞
    for paddle in paddles:
        if circle_rect_collision(ball, paddle):
            ball.ball_dx = -ball.ball_dx  # 小球反弹

    # 检测小球掉出屏幕
    if ball.rect.left <= 0:  # 小球掉出左侧
        score_right += 1  # 右侧得分
        ball.reset()  # 重置小球
    elif ball.rect.right >= SCREEN_WIDTH:  # 小球掉出右侧
        score_left += 1  # 左侧得分
        ball.reset()  # 重置小球

    # 绘制精灵
    all_sprites.draw(screen)

    # 绘制得分
    score_text = font.render(f"{score_left} : {score_right}", True, WHITE)
    screen.blit(score_text, (SCREEN_WIDTH // 2 - 40, 10))

    # 更新屏幕
    pygame.display.flip()

pygame.quit()
```

### manim（动画）

3Blue1Brown的动画制作引擎[Manim Community](https://docs.manim.community/en/stable/)

2. [manim](https://github.com/leekunhwee/manim)：命令行输入 `python -m pip install manim`
3. [miktex](https://miktex.org/download)：详见latex安装
4. [ffmpeg](https://www.gyan.dev/ffmpeg/builds/)：下载解压后将../bin/目录添加进用户环境变量（此为音视频流处理软件)

`manim ./1.py -p` 渲染文件中的场景 -p指渲染后预览；路径后加场景的类名可以精确匹配渲染的场景；-qk,-qp,-qh默认,-qm,-ql 4k（3840x2160 60FPS）、2k（2560x1440 60FPS）、高（1920x1080 60FPS）、中（1280x720 30FPS）、低（854x480 15FPS）画质；-s 输出视频的最后一帧；--format gif 输出gif格式的动画

```python
from manim import *
 
class ManimCELogo(Scene):
    def construct(self):
        self.camera.background_color = "#ece6e2"
        logo_green = "#87c2a5"
        logo_blue = "#525893"
        logo_red = "#e07a5f"
        logo_black = "#343434"
        ds_m = MathTex(r"\mathbb{M}", fill_color=logo_black).scale(7)
        ds_m.shift(2.25 * LEFT + 1.5 * UP)
        circle = Circle(color=logo_green, fill_opacity=1).shift(LEFT)
        square = Square(color=logo_blue, fill_opacity=1).shift(UP)
        triangle = Triangle(color=logo_red, fill_opacity=1).shift(RIGHT)
        logo = VGroup(triangle, square, circle, ds_m)  # order matters
        logo.move_to(ORIGIN)
        self.add(logo)
```

```python
from manim import *

class Example(Scene):
    def construct(self):
        # 创建坐标系
        axe = Axes(
            x_range=[-1, 3, 1],  # x轴范围从-1到3，步长为1
            y_range=[-1, 9, 2],  # y轴范围从-1到9，步长为2
            axis_config={
                # 加长特定数字的刻度线
                "numbers_with_elongated_ticks": [0, -3, 3],
                "font_size": 20,
                # 坐标轴显示标签，也可以通过axe = Axes().add_coordinates()实现
                "include_numbers": True,
            },
            x_axis_config={
                "color": RED,  # x轴颜色为红色
                "stroke_width": 5,  # x轴线条宽度
                "include_tip": True,  # 显示箭头
                "tip_shape": ArrowSquareTip, # 箭头形状
				"tip_length": 0.3,  # 箭头长度
            },
            y_axis_config={
                "color": BLUE,  # y轴颜色为蓝色
                "stroke_width": 1.5,  # y轴线条宽度
                "include_tip": True,  # 显示箭头
                "tip_shape": StealthTip,  # 箭头形状
            },
        )

        # 添加坐标轴标签
        labels = axe.get_axis_labels(
            Tex("x").scale(0.7), Text("y").scale(0.45)
        )

        # 绘制函数图像 y = x^2
        graph = axe.plot(lambda x: x ** 2, x_range=[0.01, 2.8], use_smoothing=False)
        # 为函数图像添加标签
        graph_label = axe.get_graph_label(
            graph=graph,  # 指定函数图像
            label=Tex(r"$x^2$").scale(0.7),  # 标签内容
            direction=RIGHT  # 标签位置（相对于函数图像）UP、DOWN、LEFT
        )
		# # 手动设置标签
        # graph_label = Tex(r"$x^2$").scale(0.7)
        # graph_label.move_to(axe.c2p(2.5, 7.2))
        # # graph_label.next_to(graph, RIGHT, buff=0.2)

        # 在函数图像上创建一个黄色的点，x=2
        dot = Dot(
            point=axe.i2gp(x=2, graph=graph),
            color=YELLOW
        )

        # 在坐标系中创建一个绿色的点，坐标为 (2, 2)
        dot_axes = Dot(axe.coords_to_point(2, 2), color=GREEN)

        # 从坐标系的原点到点 (2, 2^2) 绘制两条线
        lines = axe.get_lines_to_point(axe.i2gp(x=2, graph=graph))
        # lines = axe.get_lines_to_point(axe.c2p(2,4)) # coords_to_point

        # 将所有对象组合成一个组
        example_group = VGroup(axe, labels, graph, graph_label, dot, dot_axes, lines)

        # 将组添加到场景中
        self.add(example_group)
	
# 箭头形状:
# ArrowTriangleTip三角形箭头(默认);ArrowTriangleFilledTip填充的三角形箭头;ArrowSquareTip方形箭头;ArrowSquareFilledTip填充的方形箭头;ArrowCircleTip圆形箭头;ArrowCircleFilledTip填充的圆形箭头;StealthTip\stealth 箭头;StealthTipFilled填充的 StealthTip 箭头;自定义箭头形状，可以通过继承 ArrowTip 类来实现

# from manim import RegularPolygon
# class CustomArrowTip(ArrowTip, RegularPolygon):
#      def __init__(self, length=0.35, **kwargs):
#          RegularPolygon.__init__(self, n=5, **kwargs)
#          self.width = length
#          self.stretch_to_fit_height(length)

# from manim import Polygon
# class CustomArrowTip(ArrowTip, Polygon):
#      def __init__(self, length=0.35, **kwargs):
#         points = [
#             (1.0000, 0.0000, 0.0),
#             (0.3090, 0.2245, 0.0),
#             (0.3090, 0.9511, 0.0),
#             (-0.1180, 0.3633, 0.0),
#             (-0.8090, 0.5878, 0.0),
#             (-0.3819, 0.0000, 0.0),  
#             (-0.8090, -0.5878, 0.0),
#             (-0.1180, -0.3633, 0.0)
#             (0.3090, -0.9511, 0.0),
#             (0.3090, -0.2245, 0.0) 
#         ]
#         Polygon.__init__(self, *points, **kwargs)
#         self.scale(length / max(self.get_width(), self.get_height())) 
```

**scene**（提供播放的场景）的方法：self.
add/remove 从scene中添加或移除若干个mobject
play 播放若干个animation动画
wait 让画面等待一段时间s，默认等待1s
camera 相机
camera.background_color = BLUE 设置摄像机的背景颜色，参数可为：预设颜色如RED、RGB颜色如[0.1, 0.2, 0.5]、十六进制颜色如'#FF5733'、浮点颜色如Color(0.2, 0.4, 0.7)
camera.frame_width/camera.frame_height 相机的视野范围

**mobject**（场景中的各种物体）：物体的绝对坐标即中心的坐标，默认为(0,0,0)
图形：
Dot([x,y,z]) 点
Line([0,0,0],[1,1,0]) 线
Arrow 箭头
DashedLine 虚线
Circle(color=RED fill_color/stroke_color,fill_opacity=1,radius=1) 圆
Ellipse(height=4,width=4/5) 椭圆
Arc(angle=PI / 6, start_angle=PI * 1.5, radius=2) 30度圆弧，半径2，从270度开始绘制
Triangle 等边三角形
Square(side_length=1) 正方形
Rectangle(color=RED,height=4,width=4/5,fill_opacity=0.5) 矩形
RoundedRectangle(corner_radius=0.2, width=1.5, height=1) 圆角矩形
Polygon 依次连接传入的坐标点列表，绘制任意多边形
RegularPolygon(n=6)  # 正六边形
图形的样式属性：
stroke_width：图形边框的粗细
color：图形的颜色
fill_color：图形的填充色
fill_opacity：填充色的透明度
文本和公式：
Text("hello world") 一般用于单行的文本
Paragraph("hello","world") 一般用于多行的文本
MarkupText("`<u>`下划线`</u>`")  一般用于富文本显示，类似HTML
Tex(r"$a^2 + b^2 = c^2$") 基于Tex主要是用来显示数学公式。Tex默认只支持显示英文
BulletedList 会将传入的多个字符串以列表的方式排列起来
Title 自动显示在顶部
文本属性和方法：
Text("hello world", color=RED) 颜色
Text("hello world").set_color_by_gradient((RED, GREEN)) 渐变色
Text("databook.top", t2c={"data": BLUE, "book": RED, "top": GREEN})可以用 t2c属性来设置特定字符的颜色（t2f：按字符设置字体t2s：按字符设置斜体t2w：按字符设置粗体）。对于 Tex对象来说，虽然没有 t2c属性，也可以通过 set_color_by_tex方法来设置特定字符的颜色
Text("数学", font="STXingkai") font属性设置字体
Text("manim", font_size=20) 通过 font_size属性设置字号
Text("BOLD font weight", weight=BOLD) 粗体
Text("ITALIC font", slant=ITALIC) 斜体
图片：
ImageMobject("images/test.png") 插入图片可以是 jpg/png/gif ，但 gif只会显示第一帧，height/width方法获取图片长宽。invert=True 表示反色
VGroup() 将某些物体视为一个整体
坐标轴：
NumberLine 数轴是最基本的一维坐标系
NumberPlane 实数平面
ComplexPlane 复平面
PolarPlane 极坐标系
Axes() 二维笛卡尔坐标轴，通过height和width两个参数可以控制坐标轴的长和宽，x_range和y_range来指定坐标轴每个维度的范围，x_axis_config。默认生成的坐标轴是没有刻度的，长度和宽度为各自屏幕的长度宽度减2。Axes的get_graph方法绘制function图像如function=lambda x : np.sin(x)，axe.i2gp(x=1,graph=sin_graph)方法得到图像点的绝对坐标
ThreeDAxes() 三维空间的笛卡尔坐标轴

move_to([1,0,0]) 绝对坐标、另一个物体，默认为中心，可选参数aligned_edge=RIGHT/LEFT/UP/DOWN/OUT/IN物体的右/左/上/下/外/内边界（可以复合，如UR指右上）
set_x,set_y,set_z 分别设置x,y,z坐标，可选参数direction
set_opacity 设置物体透明度
center() 移动到场景中心
to_edge(RIGHT,buff=0) 移动到场景的边界，参数为RIGHT/LEFT/UP/DOWN，可选参数buff表示与边界的间隙默认为0.5
to_corner(UR,buff=0) 移动到场景的角落，参数为UL/UR/DL/DR，可选参数buff
shift() 相对于自身移动一个单位，参数为RIGHT/LEFT/UP/DOWN
next_to() 相邻于另一个物体，可选参数direction、buff
align_to(s,UP) 在direction侧对齐于另一个物体
match_x,match_y,match_z 物体的坐标于另一个物体相匹配
除坐标属性外还有match_color/match_width/match_height
get_center/get_x/get_y/get_z 获取物体中心点坐标
get_left/get_right/get_top/get_bottom 获取物体边界中心点坐标
get_corner() 获取物体角落坐标，参数为UL/UR/DL/DR
rotate(45 * DEGREES) 逆时针旋转物体 run_time=2
copy() 得到物体的副本
animate.to_edge(RIGHT,buff=1) 将移动的方法变成动画从而传入play中播放

**animation**（作用于物体上的动画）：
Create 创建图形，绘制时图形逐步显示
Write 用在文字的创建上，绘制文字时逐个显示文字
FadeIn/FadeOut 淡入、淡出
Uncreate一般用在擦除图形
Unwrite一般用在擦除文字
ReplacementTransform 从原图形/文字直接变换成新的图形/文字
TransformFromCopy 保留原图形/文字的变换

MoveAlongPath 可以让元素沿着任意的函数轨迹来运动
TracedPath可以设置保留运动轨迹的效果
通过 LaggedStart控制组合的多个动画之间的启动时间间隔
通过 Succession控制多个动画顺序执行，它能够保证上一个执行成功后才执行下一个

### chardet（编码检测）

chardet 是一个 Python 库，用于检测文本数据的字符编码。它可以自动识别文本的字符编码，在处理各种不同编码的文本数据时避免出现乱码或其他问题。chardet 的工作原理是分析文本数据中的字符分布和统计信息，然后根据这些信息来猜测文本的编码方式。

pip install chardet

```python
import chardet
 
text = b'This is a sample text.'
result = chardet.detect(text)
print(result) # {'encoding': 'ascii', 'confidence': 1.0, 'language': ''}
```

### web开发

  **Diango
  Pyramid
  flask**

#### SQLAlchemy

  sqlalchemy是一个python语言实现的的针对关系型数据库的orm库。可用于连接大多数常见的数据库，比如Postges、MySQL、SQLite、Oracle等

SQLAlchemy提供了两种主要的使用模式

1. SQL表达式语言（SQLAlchemy Core）
2. ORM

#### FastAPI

FastAPI 是一个用于构建 API 的现代、快速（高性能）的 web 框架，专为在 Python 中构建 RESTful API 而设计。

#### Mkdocs（markdown静态网站）

  MkDocs是一个快速、简单、华丽的静态网站生成器，适用于构建项目文档。文档源文件以Markdown编写，并使用一个YAML文件来进行配置。

 安装：==`pip install mkdocs`==
 使用 `mkdocs --version` 检查是否安装成功

**初始化项目**：==`mkdocs new <项目名>`==
生成一个<项目名>文件夹，里面有 `mkdocs.yml`配置文件，以及一个名为 `docs`的文件夹，它将包含你的文档文件。现在 `docs`文件夹只包含一个名为 `index.md`的文档页面。
直接在当前目录下运行 `mkdocs new .` 命令将已有的文件夹初始化为 MkDocs 项目而不创建新文件夹
`index.md` 文件不需要显式添加到 `nav` 配置中，因为它会自动作为主页加载。

MkDocs附带一个内置的开发服务器，可以让你在处理文档时预览文档。
确保 `mkdocs.yml`配置文件位于同一目录中
运行==`mkdocs serve`==命令启动服务器，在浏览器中打开 `http://127.0.0.1:8000/`，你将看到显示的默认主页

**主题**：
配置文件 `mkdocs.yml`
`site_name: <站点名称>`
添加 `nav`设置来管理每个页面导航的顺序、标题和嵌套情况
添加 `theme`设置（MkDocs的默认主题为mkdocs，还内置readthedocs主题）
可以在MkDocs[community wiki](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes)中找到第三方主题列表

```yml
site_name: MkLorum
nav:
- Home: index.md
- User Guide:
    - Writing your docs: writing-your-docs.md
    - Styling your docs: styling-your-docs.md
- About:
    - License: license.md
    - Release Notes: release-notes.md
theme: readthedocs
```

也可以自定义主题，自定义主题至少包含一个 `main.html`文件

```yml
theme:
    name: null
    custom_dir: 'custom_theme/'
```

默认情况下，MkDocs使用MkDocs favicon图标。 要使用不同的图标，请在docs_dir中创建一个img子目录，并将自定义的favicon.ico文件复制到该目录。 MkDocs将自动检测并使用该文件作为你的favicon图标。

**自定义**：
可以添加css和JavaScript文件到 `docs`目录进一步调整样式
在 `docs`目录下添加文件：

```text
.
├─ docs/
│  ├─ stylesheets/
│  │  └─ extra.css
│  └─ javascripts/
│     └─ extra.js
└─ mkdocs.yml
```

然后在 `mkdocs.yml`中添加以下内容：

```yml
extra_css:
  - stylesheets/extra.css
  
extra_javascript:
  - javascripts/extra.js
```

**插件**：
在使用插件之前，必须将其安装在系统上。 如果您使用的是MkDocs附带的插件，则在安装MkDocs时会安装它。 但是，要安装第三方插件，您需要确定相应的软件包名称并使用 `pip`进行安装

```bash
pip install mkdocs-foo-plugin
```

使用插件：[第三方插件](https://wdk-docs.github.io/mkdocs-docs/plugins/)
plugins配置选项应包含构建站点时要使用的插件列表。 每个“插件”必须是分配给插件的字符串名称（请参阅给定插件的文档以确定其“名称”）。 此处列出的插件必须已经安装。

```yml
plugins: - search
```

某些插件可能提供自己的配置选项。 如果要设置任何配置选项，则可以嵌套给定插件支持的任何选项的键/值映射

```yml
plugins:
    - search:
        lang: en
        foo: bar
```

开发插件：
插件必须用Python编写
插件需要打包为Python库（分布在PyPI上，与MkDocs分开），每个插件必须通过setuptools entry_point注册为插件。

==数学公式支持==：

```yml
markdown_extensions:
  - pymdownx.arithmatex

extra_javascript:
  - https://cdn.jsdelivr.net/npm/mathjax@2/MathJax.js?config=TeX-AMS-MML_HTMLorMML
```

```yml
markdown_extensions:
  - pymdownx.arithmatex:  # 启用数学公式扩展
      generic: true  # 使用通用数学公式渲染器

extra_css:
- themes/css/custom.css
- themes/css/simpleLightbox.min.css
- themes/css/pied_piper.css
- https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.9/katex.min.css
 
extra_javascript:
- themes/js/custom.js
- themes/js/simpleLightbox.min.js
- themes/js/optionalConfig.js
- themes/js/mermaidloader.js
- themes/js/umlconvert.js
- themes/js/mathjax.js
- themes/js/katex.js
- https://cdn.jsdelivr.net/npm/mermaid@10.6.1/dist/mermaid.min.js
- https://cdnjs.cloudflare.com/ajax/libs/flowchart/1.17.1/flowchart.min.js
- https://cdnjs.cloudflare.com/ajax/libs/raphael/2.3.0/raphael.min.js
- https://cdnjs.cloudflare.com/ajax/libs/underscore.js/1.13.6/underscore-min.js
- https://cdn.jsdelivr.net/npm/@mermaid-js/mermaid-mindmap@9.3.0/dist/diagram-definition.0faef4c2.min.js
- https://cdn.jsdelivr.net/npm/markdown-it-plantuml@1.4.1/index.min.js
- https://cdnjs.cloudflare.com/ajax/libs/webfont/1.6.28/webfontloader.js
- https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.2.0/es5/tex-mml-chtml.js
- https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.2.0/es5/tex-chtml.js
- https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.2.0/es5/tex-chtml-full.js
- https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.2.0/es5/tex-svg-full.js
- https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.9/katex.min.js
- https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.9/contrib/auto-render.min.js
```

**生成网站**：==`mkdocs build --clean`== --clean参数用于删除陈旧的文件

如果已经在GitHub上托管代码，那么使用GitHub Pages来发布网站再方便不过了。
使用GitHub Actions可以自动部署网站。在库的根目录下新建一个GitHub Actions workflow，比如：.github/workflows/ci.yml，并粘贴入以下内容：

```yml
name: ci
on:
  push:
    branches:
      - master
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: 3.x
      - run: pip install mkdocs-material
      - run: mkdocs gh-deploy --force
```

此时，当一个新的提交推送到 `master`或 `main`时，我们的静态网站的内容将自动生成并完成部署。网站将在不久后部署到 `<username>.github.io/<repository>`

如果是倾向于手动部署网站，请在包含 `mkdocs.yml`文件的目录中运行以下命令：
`mkdocs gh-deploy --force`

---

[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)是MkDocs的一个使用人数众多主题
可以使用 `pip install mkdocs-material` 来完成安装

[Material for MkDocs - Material for MkDocs 中文文档](https://mkdoc-material.llango.com/)

添加内容到 `mkdocs.yml`以配置

最小配置：

```yml
theme:
  name: material
```

高级设置：

- 修改颜色
- 修改字体
- 修改语言
- 修改logo图片和icon图标
- 设置导航
- 设置站内搜索
- 设置访问统计
- 设置versioning
- 设置头部(header)
- 设置底部(footer)
- 添加Github库(repository)
- 添加评论系统

```yml
theme:
  name: material  # 使用 Material 主题
  language: zh  # 设置站点语言为中文
  favicon: assets/favicon.png  # 设置网站标签页图标
  icon:
    logo: logo  # 设置站点 logo 图标
  font:
    text: Roboto  # 正文字体
    code: Roboto Mono  # 代码字体

  features:
    # - navigation.instant  # 启用即时导航功能
    - navigation.sections  # 启用导航部分功能
    - navigation.tabs  # 启用导航标签功能
    - content.code.copy  # 启用代码块复制功能
    - navigation.tracking  # 启用导航跟踪功能

  palette:
    - media: "(prefers-color-scheme: light)"
      scheme: default
      primary: white  # 浅色模式主色调
      accent: purple  # 浅色模式强调色
      toggle:
        icon: material/weather-sunny # 设置浅色模式下的切换按钮图标
        name: 切换到深色模式  # 设置浅色模式下的切换按钮名称
      
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      primary: black  # 深色模式主色调
      accent: pink  # 深色模式强调色
      toggle:
        icon: material/weather-night  # 设置深色模式下的切换按钮图标
        name: 切换到浅色模式  # 设置深色模式下的切换按钮名称

  static_templates:
    - 404.html  # 自定义 404 页面

  include_search_page: false  # 不包含 MkDocs 的搜索页面
  search_index_only: true  # 仅包含搜索索引
```

---

MkDocs Minify是Mkdocs的HTML、js、css最小化插件，可以节约空间
HTML压缩通过**htmlmin2**实现，JS压缩通过**jsmin**实现，CSS压缩通过**csscompressor**实现。
（`htmlmin -csHk <input.html> [output.html]`）

`pip install mkdocs-minify-plugin`

在 `plugins`配置项中加入 `minify`

```yml
plugins:
  - search
  - minify:
      minify_html: true
      minify_js: true
      minify_css: true
```

#### Django（Web 框架）

Django 是一个由 Python 编写的一个开放源代码的 Web 应用框架。
Django 本身基于 MVC ，即 Model（模型）+ View（视图）+ Controller（控制器）设计模式
Django 提供了一个强大的 ORM（对象关系映射），允许开发者通过 Python 代码来定义和操作数据库模型，而无需直接使用 SQL。这使得数据库操作更加抽象和易于管理。

[Django](https://docs.djangoproject.com/zh-hans)

windows `pip install Django`
linux `sudo pip3 install Django`

**初始化项目**：`django-admin startproject <项目名>`
(或 `python -m django startproject <项目名>`)
在项目文件夹下**启动开发服务器**（进入项目文件夹`cd <项目名>`）：`python manage.py runserver 0.0.0.0:8000`

> 0.0.0.0 表示开放外界访问，8000指端口。

需要先编辑 `settings.py`中的ALLOWED_HOSTS添加 服务器ip /127.0.0.1开放访问

```python
ALLOWED_HOSTS = ['127.0.0.1', 'example.com', '123.45.67.89',]
ALLOWED_HOSTS = ['*'] # 允许所有 IP 地址访问（在开发环境中）
```

```text
项目名/	  # 项目根目录										.
├─ 项目名  # 主应用开发目录
│   ├─ __init__.py   # 包的初始化文件
│   ├─ asgi.py       # 异步编程模式的web对象
│   ├─ settings.py   # 开发配置文件，包括数据库账号密码等配置
│   ├─ urls.py       # 总路由文件，用于绑定url映射
│   └─ wsgi.py       # wsgi服务器的入口文件，manage.py runserver调用的就是wsgi
└─ manage.py         # 项目的入口程序，提供一系列脚手架
```

启动wsgi服务后还会多一个db.sqlite3数据库文件[[#SQLite3（数据库）]]

##### 核心组件的使用

一个 Django 项目由多个应用（App）组成,
（按功能模块合理规划 App；对于简单的静态页面（如关于页、主页），可直接在项目层处理无需创建 App ）
**创建应用** `python manage.py startapp <app名>`

> 注册应用：在 `settings.py` 中的INSTALLED_APPS添加应用

```text
app名/
├─ migrations
│      └─ __init__.py
├─ __init__.py
├─ admin.py
├─ apps.py
├─ models.py
├─ tests.py
└─ views.py   # 接收http的request对象
```

*以下以项目 `myproject`，应用 `blog`为例*：

**数据库**：
在 `models.py` 中设计数据库表

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField(default='暂未填写')
    file = models.FileField(upload_to='uploads/%Y/%m/%d/', blank=True, null=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title
```

CharField：用于存储字符串。
IntegerField：用于存储整数。不过很多时候不如使用CharField
DateField：用于存储日期。
ForeignKey：用于定义多对一关系。related_name 是 Django 的 ForeignKey 字段的一个可选参数，用于定义反向关系的名称。它允许你通过关联模型访问主模型的所有相关对象。
related_name='files' 的作用是允许你通过 Post 模型访问所有关联的 PostFile 对象。例如：
```python
# 获取一个 Post 对象
post = Post.objects.get(id=1)

# 通过 related_name 获取所有关联的 PostFile 对象
files = post.files.all()
```
JSONField
TextField
boll
img
FileField：有一个file.url可以得到相对路径，使用 request.build_absolute_uri(file.url) 将相对路径转换为完整的 URL
可以使用 `JSONField` 或 `ManyToManyField` 来存储多个文件路径

- null=True：允许数据库字段存储 `NULL` 值。
- blank=True：允许 Django 表单验证时字段可以为空。

某些字段（如 CharField 或 IntegerField）可能需要显式设置默认值default
或者在前端表单中提供默认值 value=""

~~如DateTimeField需要一个 `datetime` 对象作为默认值~~
~~`from datetime import datetime`~~
~~`default=datetime(2025, 1, 1, 0, 0)`~~
~~如果您希望默认值始终是当前时间，可以使用 `default=datetime.now()`~~
~~(datetime.date()返回具有同样 year, month 和 day 值的 date 对象)~~

~~对于 IntegerField~~
~~直接提供一个整数作为默认值 `default=0`~~

在视图设置：

```python
        try:
            # 验证并格式化日期 %Y-%m-%dT%H:%M
            # 将字符串转换为 datetime 对象。
            if date:
                date = datetime.strptime(date, '%Y-%m-%d')
            # datetime 对象的.date() 方法，提取日期部分返回datetime.date 对象
        
            # 将字符串转换为数字
			integer = int(integer)
        except (ValueError, TypeError):
            date = None  # 如果格式不正确，设置为 None
			integer = None
```

如果数据很多，可以使用字典data传输数据，并且
```python
    if request.method == 'POST':
        date = {
            'title' : request.POST.get('title'),
            'content' : request.POST.get('content'),
        }
        # 批量设置空字符串为None
        for key, value in data.items():
            if value == '':
                data[key] = None
                
        files = {
            'file' : request.FILES.get('file'),
        }
			
		post = Post(**data, **files)
```

如果需要修改数据，可以：

```python
def post_edit(request, pk):
    post = get_object_or_404(Post, pk=pk)
        if request.method == 'POST':
            data = {
                # 如果某个字段未提交，设置默认值
                'title' : request.POST.get('title', post.title),
            }
            files = {}
            for key, value in {**data, **files}.items():
                setattr(post, key, value)
            post.save()

# urls.py
path('<int:pk>/edit/', views.post_edit, name='post_edit'),
```


```html
<input type="text" name="FactoryRepClosing" value="{{ post.factory_rep_closing }}">
<input type="datetime-local" name="Auditfinishtime" value="{{ post.audit_finish_time|date:'Y-m-d\\TH:i' }}"></td>

<div class="radio-group">
    <label><input type="radio" name="a1" value="A" {% if post.pre_production_a1 == 'A' %}checked{% endif %}>A</label>
    <label><input type="radio" name="a1" value="B" {% if post.pre_production_a1 == 'B' %}checked{% endif %}>B</label>
    <label><input type="radio" name="a1" value="C" {% if post.pre_production_a1 == 'C' %}checked{% endif %}>C</label>
    <label><input type="radio" name="a1" value="D" {% if post.pre_production_a1 == 'D' %}checked{% endif %}>D</label>
    <label><input type="radio" name="a1" value="NA" {% if post.pre_production_a1 == 'NA' %}checked{% endif %}>NA</label>
</div>

{% if post.a1_text %}
<textarea name="a1_text" rows="2">{{ post.a1_text }}</textarea>
{% else %}
<textarea name="a1_text" rows="2"></textarea>
{% endif %}
```

复制一条数据

```python
def qsa_copy(request, pk):
    # 获取原始对象
    original_post = get_object_or_404(Post, pk=pk)
    # 将对象转换为字典
    post_data = model_to_dict(original_post)
    # 移除主键字段以避免冲突
    post_data.pop('id', None)
    # 创建新对象
    new_post = Post.objects.create(**post_data)
    return redirect('qsa_edit', pk=new_post.pk)
```

```shell
python manage.py makemigrations  # 生成迁移文件
python manage.py migrate         # 应用迁移到数据库
```

如果迁移出问题，可以尝试删除migrations文件夹下除__init__.py的其他文件如0001_initial.py，再重新迁移。仍然不行可以尝试删除数据库文件再迁移

关于文件的说明和优化方案：

```python
# 按照年月日创建文件夹：upload_to='uploads/%Y/%m/%d/'

# 按用户ID分目录：upload_to=user_upload_path
def user_upload_path(instance, filename):
    return f'uploads/user_{instance.user.id}/{filename}'

# 哈希文件名： upload_to=hash_filename
import hashlib
def hash_filename(instance, filename):
    ext = filename.split('.')[-1]
    hash_name = hashlib.md5(filename.encode()).hexdigest()[:8]
    return f'files/{hash_name}.{ext}'

# 按年+哈希：uploads/2024/abc123de.jpg
from django.utils import timezone
def smart_upload_path(instance, filename): 
    return f'uploads/{timezone.now().year}/{hashlib.md5(filename.encode()).hexdigest()[:6]}.{filename.split(".")[-1]}'
```

默认使用db.sqlite3数据库文件作为数据库
在settings.py 文件中找到 DATABASES 配置项可以修改

如果需要使用mysql 数据库：
安装 mysql
创建 MySQL 数据库 `create database 数据库名称 default charset=utf8;`( ORM 无法操作到数据库级别，只能操作到数据表)
修改DATABASES为

```python
DATABASES = { 
    'default': 
    { 
        'ENGINE': 'django.db.backends.mysql',    # 数据库引擎
        'NAME': 'data', # 数据库名称
        'HOST': '127.0.0.1', # 数据库地址，本机 ip 地址 127.0.0.1 
        'PORT': 3306, # 端口 
        'USER': 'root',  # 数据库用户名
        'PASSWORD': '123456', # 数据库密码
    }  
}
```

安装mysqlclient驱动 `pip install mysqlclient`即可
如果安装pymysql驱动 `pip install pymysql`，需要告诉 Django 使用 pymysql 模块连接 mysql 数据库：

```python
# 在与 settings.py 同级目录下的 __init__.py 中引入模块和进行配置  
import pymysql  
pymysql.install_as_MySQLdb()
```

**配置视图（View）**
在 `views.py` 中处理业务逻辑

```python
# from django.http import HttpResponse
# def index(request):
#     return HttpResponse("Hello, world.")

# from django.shortcuts import render
# def index(request):
#     return render(request, 'index.html')

from django.shortcuts import render
from .models import Post

def post_list(request):
    posts = Post.objects.all()
    return render(request, 'blog/post_list.html', {'posts': posts})
```

HttpResponse
render渲染
redirect后端重定向

|属性|描述|
|---|---|
|字段属性|模型中定义的字段（如 CharField, ForeignKey 等）。|
|Meta 类|定义模型的元数据（如数据库表名、排序规则等）。|
|objects|默认的模型管理器（用于数据库查询，如 Post.objects.all()）。|
|pk|主键的快捷访问方式（如 post.pk 对应 post.id）。|
|_meta|提供模型的元信息（如字段列表、关联关系等）。|

|实例方法|描述|
|---|---|
|save(**kwargs)|保存对象到数据库（新建或更新）。|
|delete(**kwargs)|从数据库删除对象。|
|refresh_from_db(fields=None)|从数据库重新加载对象的最新数据。|
|clean()|自定义数据验证逻辑（需手动调用或通过 full_clean() 触发）。|
|full_clean()|执行完整验证（字段验证、clean() 方法、唯一性检查）。|
|get_FOO_display()|获取 choices 字段的可读值（FOO 为字段名，如 get_status_display()）。|
|get_absolute_url()|定义对象的详情页 URL（常用于模板或重定向）。|
|`__str__()`|定义对象的字符串表示（用于控制台、Admin 界面等）。|

post.save()
post.delete()

|类方法|描述|
|---|---|
|objects.all()|返回所有对象的 QuerySet。|
|objects.filter(**kwargs)|返回符合条件的 QuerySet（如 Post.objects.filter(author=user)。|
|objects.get(**kwargs)|返回单个对象（找不到或找到多个时抛异常）。|
|objects.create(**kwargs)|创建并保存新对象（等价于 Model().save()）。|
|objects.update(**kwargs)|批量更新符合条件的对象。|
|objects.order_by(*fields)|对查询结果排序（如 Post.objects.order_by('-created_at')。|

`post =Post.objects.all()`返回数据库中所有 `Post` 对象
`post =get_object_or_404(Post, pk=pk)`返回主键（`pk`）匹配的唯一一个对象,若对象不存在则返回 404 页面
`post =Post.objects.filter(id__in=post_ids)`返回 `id` 在 `post_ids` 列表中的所有对象

html `action="{% url 'submit_form' %}"`：指定表单提交到Django的 `submit_form`路由，不指定默认提交当前路由

```python
def form_submit(request):
    if request.method == 'POST':
        # 处理数据...
        return redirect('success')  # 使用URL命名
    return render(request, 'form.html')

def success_page(request):
    return render(request, 'success.html')
```

获取单个值：request.POST.get('键')
获取多选框/多选列表的值（返回列表）：request.POST.getlist('键')

网页动态化（**模板**）：
需要向Django说明模板文件的路径
一般可以创建一个文件夹存放templates模板，然后修改settings.py中的 TEMPLATES 中的 DIRS 为 `[os.path.join(BASE_DIR, 'templates')]`
(BASE_DIR是项目根目录，也可以使用相对路径直接 `['templates']`)

在view.py中：返回一个字典 `{'HTML变量名':views变量名}`

```python
    views_name = 'Django'
    context = {
        'name': views_name,
        'views_list': [1, 2, 3, 4]
    }
    return render(request, 'index.html', context)
```

HTML：`{{ 变量名 }}`

```html
<p>{{ name }}</p>
```

如果 `views_name`是列表，可以用 `.`  索引下标取出对应的元素，如 `views_name.0`
如果 `views_name`是列表，可以用 `.`  键标取出对应的元素，如 `views_name.name`

在 Django 模板中直接访问以下划线开头的属性（如 `post._meta.fields`）会触发 `TemplateSyntaxError`，因为 Django 模板系统出于安全考虑禁止访问这类内部属性。
可以在views中获取模型字段信息，再传递给模板。

==模板过滤器==可以在变量被显示前修改它：`{{ 变量名 | 过滤器:可选参数 }}`，过滤器可以套接

- `add`：将一个值加到变量上。`{{ forloop.counter|add:10 }}`
- `default`：如果变量为空或不存在，则返回默认值。`{{ variable|default:"默认值" }}`
- `length`：返回变量的长度。
  `{{ my_list|length }}`
- `lower`：将字符串转换为小写。

  `{{ "HELLO"|lower }}`
- `upper`：将字符串转换为大写。

  `{{ "hello"|upper }}`
- `truncatechars`：截断字符串到指定字符数，并添加省略号。

  {{ "This is a long text"|truncatechars:10 }}
- `title`：将字符串转换为标题格式（每个单词首字母大写）。

  {{ "hello world"|title }}
- `date`：格式化日期。

  {{ my_date|date:"Y-m-d" }}
- `time`：格式化时间。

  {{ my_time|time:"H:i:s" }}
- `timesince`：返回从某个时间到现在的时间间隔。

  {{ my_date|timesince }}
- `first`：返回列表的第一个元素。

  {{ my_list|first }}
- `last`：返回列表的最后一个元素。

  {{ my_list|last }}
- `slice`：对列表进行切片。

  {{ my_list|slice:":3" }}
- `dictsort`：根据字典的某个键对列表排序。

  {{ my_dict_list|dictsort:"key_name" }}
- `yesno`：根据布尔值返回自定义的文本。

  {{ is_active|yesno:"是,否,未知" }}
- `default_if_none`：如果变量为 `None`，返回默认值。

  {{ variable|default_if_none:"无数据" }}
- `escape`：对字符串进行 HTML 转义。

  `{{ "<script>"|escape }}`
- `safe`：标记字符串为安全的 HTML，不会被转义。

  `{{ "<b>bold</b>"|safe }}`
- `linebreaks`：将换行符转换为 `<br>` 标签。

  {{ "Line1\nLine2"|linebreaks }}
- `floatformat`：格式化浮点数。

  {{ 3.14159|floatformat:2 }}
- `addslashes`：为字符串添加反斜杠。

  {{ "O'Reilly"|addslashes }}
- `filesizeformat`：格式化文件大小。

  {{ file.size|filesizeformat }}
- `urlencode`：对字符串进行 URL 编码。

  {{ "Hello World"|urlencode }}

**自定义过滤器**

如果内置过滤器无法满足需求，可以创建自定义过滤器。示例：

在 templatetags 文件夹中创建自定义过滤器

```python
# 在 templatetags 文件夹中创建自定义过滤器
from django import template

register = template.Library()

@register.filter
def multiply(value, arg):
    return value * arg

# 在模板中使用：{{ 5|multiply:3 }}
```

注释标签：{# 这是一个注释 #}
==if/else 标签==
支持嵌套，接受 and 、 or 、 not 关键字

```html
{% if condition1 %}
   ... display 1
{% elif condition2 %}
   ... display 2
{% else %}
   ... display 3
{% endif %}
```

==for 标签==
{% for %} 允许我们在一个序列上迭代。给标签增加一个 reversed 使得该列表被反向迭代

```html
{% for athlete in athlete_list %}
{# % for athlete in athlete_list reversed % #}
    <li>{{ athlete.name }}</li>
{% endfor %}
```

遍历字典可以 `{% for i,j in views_dict.items %}` 得到键和值
在 {% for %} 标签里可以通过 {{forloop}} 变量获取循环序号
可选的 {% empty %} 从句：在循环为空的时候执行

`{{ forloop.counter }}` 输出当前循环迭代的计数器值，从 1 开始计数。

==include 标签==
{% include %} 标签允许在模板中包含其它的模板的内容。
`{% include "nav.html" %}`

csrf_token 用于form表单中，作用是跨站请求伪造保护。
如果不用 ` {% csrf_token %}` 标签，在用 form 表单时，要再次跳转页面会报 403 权限错误。

在模板文件的顶部添加 `{% load static %}`，如果有继承在 `{% extends 'base.html' %}`之后添加
然后通过静态文件夹在Django模板中引用CSS样式/js
`<link rel="stylesheet" href="{% static 'css/styles.css' %}">`

可以自定义标签和过滤器

==模板继承==
模板可以用继承的方式来实现复用，减少冗余内容。
网页的头部和尾部内容一般都是一致的，我们就可以通过模板继承来实现复用。
父模板用于放置可重复利用的内容，子模板继承父模板的内容，并放置自己的内容。
通常 `{% extends "base.html" %}`统一网页结构

```html
{% block 名称 %} 
预留给子模板的区域，可以设置设置默认内容
{% endblock 名称 %}
```

```html
{% extends "父模板路径"%}

{% block 名称 %}
内容 
{% endblock 名称 %}
```

```html
<!-- blog/post_list.html -->
<!DOCTYPE html>
<html>
<head>
    <title>帖子列表</title>
</head>
<body>
    <h1>所有帖子</h1>
  
    {% for post in posts %}
        <div style="border: 1px solid #ccc; padding: 10px; margin-bottom: 20px;">
            <h2>{{ post.title }}</h2>
            <p>{{ post.content }}</p>
            <p>创建时间：{{ post.created_at }}</p>
          
            {% if post.file %}
                <p>附件：
                    <a href="{{ post.file.url }}" target="_blank">
                        {{ post.file.name|cut:"uploads/" }}
                    </a>
                </p>
            {% endif %}
        </div>
    {% endfor %}
  
    <a href="{% url 'create_post' %}">新建帖子</a>
</body>
</html>
```

**配置路由（URL）**
项目路由（`myproject/urls.py`）：

```python
from django.contrib import admin
from django.urls import include, path
from myapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('blog/', views.post_list, name='post_list'),
]
```

name用于url  ''

配置路由还可以使用应用路由的方式：
在app目录下新建 `urls.py`

```python
# blog/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.post_list, name='post_list'),
]

# myproject/urls.py
from django.urls import include, path

urlpatterns = [
    path('blog/', include('blog.urls')),
]
```

**Admin 管理工具**Django 提供了基于 web 的管理工具。
可以通过命令 `python manage.py createsuperuser` 创建超级用户(需要先应用迁移到数据库)
在浏览器中访问 `http://127.0.0.1:8000/admin`，输入用户名密码登录(lain       lain123456)

修改settings文件，可改为中文

```python
LANGUAGE_CODE = 'zh-Hans'
 
TIME_ZONE = 'Asia/Shanghai'
```

注册模型到 Admin（`blog/admin.py`）

```python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

##### 常用功能

**静态文件处理**
配置静态文件（settings.py）：
一般静态文件存放在统一的文件夹下，命名为'/static/'、'/files/'等

```python
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']
```

1. **`STATIC_URL = '/files/'`**

   - 定义了静态文件的 URL 前缀。当你在模板中引用静态文件时，Django 会使用这个 URL 前缀。例如，如果你有一个静态文件 `logo.png`，它的 URL 将是 `http://<your-domain>/files/logo.png`。
   - 这是静态文件在浏览器中访问的路径。
2. **`STATICFILES_DIRS = [BASE_DIR / 'files']`**

   - 指定了静态文件的目录路径。Django 会在这个目录中查找静态文件。

也可以使用路由实现：

```python
# 开发环境下提供静态文件服务
if settings.DEBUG:
    urlpatterns += static('/files/', document_root=settings.BASE_DIR / 'files')
```

`https://ip:端口/static/文件` 即可访问静态文件

STATIC_ROOT 是 collectstatic 命令收集所有静态文件的目标目录。
通常，这个目录不应该与 STATICFILES_DIRS 中的目录重叠。

生产环境需运行 python manage.py collectstatic 收集静态文件。

**表单处理**
==使用Django 表单类==，在 forms.py 中定义表单：
表单可以自定义(forms.Form)，也可以由模型Models创建(forms.ModelForm)
forms.py的好处: 所有的表单在一个文件里，非常便于后期维护，比如增添或修订字段。

使用`ModelForm`可以自动帮助我们处理表单字段的显示和保存。在提交失败后，`ModelForm`会自动将字段值回填到表单中。

```python
from django import forms
from .models import Post

class PostForm(forms.ModelForm):
    # 可以通过声明方式指定字段，就像在常规 `Form` 中一样
    # your_name = forms.CharField(label="Your name", max_length=100)
    class Meta:
        model = Post   # 指定关联的模型
        exclude = ['']
        # fields = ['title', 'content', 'file']   # 指定表单包含的字段
        # 或者排除某些字段：exclude = ['pub_date'] （谨慎使用，避免安全风险）
        # 自定义字段的标签
        # labels = {
        #     'title': '文章标题', # 将标题字段的标签改为 "文章标题"
        #     'content': '内容',
        # }
        # 自定义字段的输入控件
        # widgets = {
        #     'content': forms.Textarea(attrs={'rows': 4}),
        # }

# class NameForm(forms.Form):
#    your_name = forms.CharField(label="Your name", max_length=100)
```

Form 类的常用属性

1. **`fields`**  
    包含表单中所有字段的字典，键是字段名称，值是字段对象。
2. **`errors`**  
    一个字典，包含表单验证失败的错误信息，键是字段名称，值是错误信息列表。
3. **`is_valid()`**  
    方法，用于验证表单数据是否合法，返回布尔值。
4. **`cleaned_data`**  
    在表单验证成功后，包含清理后的数据的字典。
5. **`as_p()` / `as_table()` / `as_ul()`**  
    用于将表单渲染为 HTML 的方法，分别以 `<p>`、`<table>` 或 `<ul>` 格式输出。
6. **`non_field_errors()`**  
    返回与表单整体相关的错误，而不是特定字段的错误。
    
字段的常用属性

7. **`label`**  
    字段的标签，用于在表单中显示。
8. **`required`**  
    是否为必填字段，默认为 `True`。
9. **`initial`**  
    字段的初始值。
10. **`help_text`**  
    字段的帮助文本，用于提示用户。
11. **`widget`**  
    用于指定字段的渲染小部件（如 `TextInput`、`Textarea` 等）。
12. **`error_messages`**  
    自定义字段验证失败时的错误信息。
13. **`validators`**  
    字段的额外验证器列表。
14. **`max_length` / `min_length`**  
    对字符串字段的最大长度和最小长度限制。
15. **`choices`**  
    用于下拉选择字段，定义可选值的列表或元组。
16. **`disabled`**  
    如果设置为 `True`，字段将被禁用，用户无法修改其值。

**`labels`** 可以修改字段的标签。
如果希望全局修改字段的默认标签（在所有表单中生效），可以直接在模型中设置 `verbose_name`

```python
# models.py
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=100, verbose_name='文章标题')  # 默认标签为 "文章标题"
    content = models.TextField(verbose_name='正文内容')
```

**`widget`** 来修改默认的输入控件

```python
# 单选
forms.RadioSelect()
# 多选
forms.CheckboxSelectMultiple()
# 自定义输入控件属性（如添加 CSS 类）
forms.RadioSelect(attrs={'class': 'custom-radio'}),
```

也可以直接修改model

| 模型字段                                | 默认控件               | 如何修改表单字段/控件                                                                                             |
| --------------------------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `models.CharField`                    | `TextInput`          | 使用 `widget=forms.Textarea` 改为文本框，或添加属性：`attrs={'class': 'custom-class'}`                       |
| `models.TextField`                    | `Textarea`           | 修改行数：`widget=forms.Textarea(attrs={'rows': 5})`                                                            |
| `models.BooleanField`                 | `CheckboxInput`      | 改为单选框：自定义为 `ChoiceField`，并设置 `widget=forms.RadioSelect(choices=[(True, '是'), (False, '否')])` |
| `models.IntegerField`                 | `NumberInput`        | 限制范围：`forms.IntegerField(min_value=0, max_value=100)`                                                      |
| `models.EmailField`                   | `EmailInput`         | 添加验证正则：`widget=forms.EmailInput(attrs={'pattern': '.*@example\.com'})`                                   |
| `models.DateField`                    | `DateInput`          | 使用日期选择器：`widget=forms.DateInput(attrs={'type': 'date'})`                                                |
| `models.DateTimeField`                | `DateTimeInput`      | 使用 `SplitDateTimeWidget`：`widget=forms.SplitDateTimeWidget`                                                |
| `models.ForeignKey`                   | `Select`             | 改为单选框：`widget=forms.RadioSelect`，或限制选项：`queryset=Model.objects.filter(...)`                      |
| `models.ManyToManyField`              | `SelectMultiple`     | 改为多选框列表：`widget=forms.CheckboxSelectMultiple`                                                           |
| `models.FileField`                    | `ClearableFileInput` | 限制文件类型：`widget=forms.ClearableFileInput(attrs={'accept': 'image/*', 'multiple': True})`                                    |
| `models.ImageField`                   | `ClearableFileInput` | 同 `FileField`，需配合 Pillow 库使用。                                                                          |
| 含有 `choices` 选项字段 | `Select`             | 改为单选框：`widget=forms.RadioSelect`，或下拉框：`widget=forms.Select(attrs={...})`                          |

使用forms.RadioSelect将Select转换为`RadioSelect` 控件时，可能会多出一个空选项：
1）如果模型字段设置了 `blank=True` 或 `null=True`，Django 会自动在表单中生成一个空选项（`-----`）
2）表单字段显式设置 `required=False`，也会生成空选项。
3）如果字段是外键（`ForeignKey`），默认会添加空选项 `-----`（可通过 `empty_label=None` 关闭）
可以在模型中禁止空值（`blank=False,  default='A'`），或在表单中设置 `required=True`；如果是外键字段，设置 `empty_label=None`。还可以在表单的 `__init__` 方法中强制移除空选项

```python
        widgets = {
            # 横向单选框：添加 CSS 类
            'category': forms.RadioSelect(attrs={
                'class': 'radio-horizontal',  # 横向布局的 CSS 类
            }),
            # 固定行数的文本框
            'content': forms.Textarea(attrs={
                'rows': 4,                   # 指定行数
                'class': 'fixed-textarea',    # 限制高度的 CSS 类
            }),
        }


# forms.py
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    class Meta:
        model = Article
        fields = '__all__'  # 包含所有字段

    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        # 遍历所有字段
        for field_name, field in self.fields.items():            
            # 针对 TextField，设置为固定行数的文本框
            if isinstance(field, forms.CharField) and isinstance(field.widget, forms.Textarea):
                field.widget.attrs.update({
                    'rows': 4,
                    'class': 'fixed-textarea'
                })


# 直接设置widget有问题，可以在dynamic_fields.py循环生成widgets

#     str1 = '''
# widgets = {
# '''   
#     for field in dynamic_fields:
#         choices = field.get('choices')
#         name = field.get('name')
#         if choices:
#             str1 += f"    \"{name}\": forms.RadioSelect(attrs={{\"class\": \"radio-horizontal\"}}),\n"
#     str1 += '}'
#     print(str1)
```

```css
/* 横向单选框 */
.radio-horizontal div {
  list-style: none;      /* 移除默认列表符号 */
  padding-left: 0;       /* 移除左内边距 */
  display: flex;         /* 横向排列 */
  gap: 1rem;             /* 选项间距 */
  flex-wrap: wrap;       /* 允许换行 */
  display: inline-block; /* 横向排列选项 */
}
/* 固定高度的文本框 */
.fixed-textarea {
  max-height: 200px;     /* 最大高度 */
  overflow-y: auto;      /* 内容溢出时显示滚动条 */
  resize: vertical;      /* 允许垂直调整大小 */
  width: 100%;           /* 填充父容器宽度 */
  box-sizing: border-box;/* 避免溢出 */
}
```

如果您想进一步自定义字段，可以指定内部 `Meta` 类的 `labels`、`help_texts` 和 `error_messages` 属性

在视图中添加函数处理表单提交：

```python
from django.shortcuts import redirect
from .forms import PostForm

def create_post(request):
    if request.method == 'POST':
        form = PostForm(request.POST, request.FILES)
        if form.is_valid():
            form.save()
            # # 暂存表单数据但不提交到数据库
            # post = form.save(commit=False)
            # # 添加表单中没有的字段
            # post.created_at = timezone.now()     # 当前时间

            # 遍历form字段
            # for field_name in form.cleaned_data:
            #     if field_name in ['sorce', 'result']:
            #         field_value = form.cleaned_data[field_name]

            # # 保存到数据库
            # post.save()
            return redirect('post_list')
    else:
        form = PostForm()
    return render(request, 'blog/create_post.html', {'form': form})
```

路由中添加：

```python
path('create/', views.create_post, name='create_post'),
```

```html
<!-- blog/create_post.html -->
<!DOCTYPE html>
<html>
<head>
    <title>创建帖子</title>
</head>
<body>
    <h1>创建新帖子</h1>
    <form method="post" enctype="multipart/form-data">
        {% csrf_token %}
      
        {{ form.as_p }}
      
        {% if form.errors %}
            <div style="color: red;">
                {% for field in form %}
                    {% for error in field.errors %}
                        <p>{{ field.label }}: {{ error }}</p>
                    {% endfor %}
                {% endfor %}
            </div>
        {% endif %}
      
        <button type="submit">提交</button>
        <a href="{% url 'post_list' %}">返回列表</a>
    </form>
</body>
</html>
```

`{{ form.as_p }}` 是一个用于快速渲染表单的模板语法，它会将 Django 表单的字段自动转换为 HTML 的 `<p>` 标签包裹的段落格式。
手动渲染字段:

```html
    <div class="field">
        {{ form.title.label_tag }}
        {{ form.title }}
        {{ form.title.errors }}
    </div>
    <div class="field">
        {{ form.content.label_tag }}
        {{ form.content }}
        {{ form.content.errors }}
    </div>


    {% for radio in form.gender %}
      <label class="radio">
        {{ radio.tag }} {{ radio.choice_label }}
      </label>
    {% endfor %}
    
    {% for choice in form.gender %}
      <div class="radio-option">
        {{ choice.tag }}
        <label for="{{ choice.id_for_label }}">{{ choice.choice_label }}</label>
      </div>
    {% endfor %}
```

如果==不使用 Django 的表单类==，可以直接在视图 `views.py`中手动处理表单数据：

```python
from django.shortcuts import render, redirect
from .models import Post

def create_post(request):
    errors = []
    if request.method == 'POST':
        title = request.POST.get('title')
        content = request.POST.get('content')
        file = request.FILES.get('file')  # 获取上传的文件
      
        # 验证字段
        if not title:
            errors.append("标题不能为空")
        if not content:
            errors.append("内容不能为空")
      
        if not errors:
            # 保存到数据库
            Post.objects.create(title=title, content=content, file=file)
            return redirect('post_list')  # 重定向到帖子列表页面
  
    return render(request, 'blog/create_post.html', {'errors': errors})
```

**`Post.objects.create()`**：
一行代码直接创建并保存对象到数据库，适合字段较少且无需中间操作的场景。

**`post = Post()` + `post.save()`**：
分两步操作，适用于需要先修改对象属性再保存的情况

```python
		data = {
			'title' : request.POST.get('title'),
			'content' : request.POST.get('content'),
			'file' : request.FILES.get('file'),
		}
		for key, value in data.items():
            if value == '':
                data[key] = None
        post = Post(**data)
        post.save()
```

还需修改create_post.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>创建帖子</title>
</head>
<body>
    <h1>创建新帖子</h1>
    <form method="post" enctype="multipart/form-data">
        {% csrf_token %}
      
        <label for="title">标题:</label>
        <input type="text" id="title" name="title" required>
        <br>
      
        <label for="content">内容:</label>
        <textarea id="content" name="content" rows="5" required></textarea>
        <br>
      
        <label for="file">上传文件:</label>
        <input type="file" id="file" name="file">
        <br>
      
        {% if errors %}
            <div style="color: red;">
                {% for error in errors %}
                    <p>{{ error }}</p>
                {% endfor %}
            </div>
        {% endif %}
      
        <button type="submit">提交</button>
        <a href="{% url 'post_list' %}">返回列表</a>
    </form>
</body>
</html>
```

==自定义表单模板==：新建一个文件，在views.py中导入，再处理逻辑

```python
# dynamic_fields.py
dynamic_fields = [
    {"type": "text", "name": "name", "label": "用户名", "vlaue": "请输入用户名"},
    {"type": "password", "name": "password", "label": "密码"},
    {"type": "number", "name": "age", "label": "年龄"},
    {"type": "checkbox", "name": "subscribe", "label": "性别", "checked" : True},
    {"type": "radio", "name": "gender", "label": "性别", "choices": ["male", "female"], "choices_label": ["男", "女"], "checked": "female"},
    {"type": "select", "name": "country", "label": "性别", "choices": ["CN", "USA"]},
    {"type": "textarea", "name": "bio", "label": "个人简介"},
    {"type": "file", "name": "profile_picture", "label": "头像", "multiple": False},
]
# 可以通过循环生成
# dynamic_fields = []
# dynamic_fields.append()

import re

# 预编译正则表达式（提高效率）
invalid_char_pattern = re.compile(r'[/\\:*?"<>|#. ]+')  # 非法字符集
valid_var_pattern = re.compile(r'^[a-zA-Z_][a-zA-Z0-9_]*$')  # 合法变量名规则

for dynamic_field in dynamic_fields:
    # 1. 替换非法字符为下划线，并合并连续下划线
    cleaned = invalid_char_pattern.sub('_', dynamic_field['name'])
    # 2. 去除首尾下划线
    cleaned = cleaned.strip('_')
    # 3. 处理空值（例如原名为纯非法字符）
    if not cleaned:
        cleaned = 'field'  # 默认值
  
    # 4. 检查变量名合法性，仅在需要时添加前缀/后缀
    if valid_var_pattern.match(cleaned):
        # 已经是合法变量名，无需处理
        final_name = cleaned
    else:
        # 不合法时添加前缀和后缀
        final_name = f'd{cleaned}y'  # 添加 d 和 y 确保合法性
  
    dynamic_field['name'] = final_name
# with open('dynamic_fields.py', 'w', encoding= 'utf-8') as fs:
#     fs.write('dynamic_fields = '+str(dynamic_fields))

if __name__ == '__main__':
    str = '''
from django.db import models
import hashlib
from django.utils import timezone
import os

def hash_filename(instance, filename):
    return f'files/{timezone.now().year}/{timezone.now().month}/{timezone.now().day}/{hashlib.md5(filename.encode()).hexdigest()[:6]}.{filename.split(".")[-1]}'

class Post(models.Model):

'''

    for dynamic_field in dynamic_fields:
        type = dynamic_field.get('type')
        name = dynamic_field.get('name')
        if type == 'text':
            str += f'    {name} = models.CharField(max_length=255, null=True, blank=Tru, verbose_name= "{label}")\n'
        elif type  == 'radio':
            str += f'    {name} = models.CharField(max_length=255, choices=[("A", "A"), ("B", "B"), ("C", "C"), ("D", "D"), ("NA", "NA")], verbose_name= "{label}", blank=False,  default="A")\n'
        elif type  == 'textarea':
            str += f'    {name} = models.TextField(null=True, blank=True, verbose_name= "{label}")\n'
        elif type  == 'file':
            str += f'    {name} = models.FileField(upload_to=hash_filename , null=True, blank=True, verbose_name= "{label}")\n'
  
    # print(str)
    with open('models.py', 'w', encoding= 'utf-8') as fs:
        fs.write(str)



# views.py
from mqsa.dynamic_fields import dynamic_fields 

        ...
        for dynamic_field in dynamic_fields:
            type = dynamic_field.get(type)
            name = dynamic_field.get(name)
            if type == 'text':
                data.update({name: request.POST.get(name)})
        ...
        # 创建 Post 实例
        post = Post(**data, **sorces, **files)
        post.save()
```

html可以如下，当然也可以使用django表单更方便

```html
    <form method="post" enctype="multipart/form-data" class="form" id="create-post-form">
        {% csrf_token %}
      
        {% for field in fields %}
        <div class="form-group">
        <label for="{{ field.name }}">{{ field.label }}</label>
        {% if field.type == "text" %}
            {% if field.value %}
            {% if field.required %}
            <input type="text" name="{{ field.name }}" class="form-control" value="{{ field.value }}" required>
            {% else %}
            <input type="text" name="{{ field.name }}" class="form-control">
            {% endif %}
        {% else %}
            {% if field.required %}
            <input type="text" name="{{ field.name }}" class="form-control" required>
            {% else %}
            <input type="text" name="{{ field.name }}" class="form-control">
            {% endif %}
        {% endif %}
        {% elif field.type == "password" %}
        <input type="password" name="{{ field.name }}" class="form-control">
        {% elif field.type == "number" %}
        <input type="number" name="{{ field.name }}" class="form-control">
        {% elif field.type == "file" %}
            {% if field.multiple %}
            <input type="file" name="{{ field.name }}" class="form-control" multiple>
            {% else %}
            <input type="file" name="{{ field.name }}" class="form-control">
            {% endif %}
        {% elif field.type == "checkbox" %}
            {% if field.checked %}
            <input type="checkbox" name="{{ field.name }}" class="form-control" checked>
            {% else %}
            <input type="checkbox" name="{{ field.name }}" class="form-control">
            {% endif %}
        {% elif field.type == "radio" %}
            {% for choice in field.choices %}
                {% if choice == field.checked %}
                <input type="radio" name="{{ field.name }}" value="{{ choice }}" checked>{{ choice }}
                {% else %}
                <input type="radio" name="{{ field.name }}" value="{{ choice }}">{{ choice }}
                {% endif %}
            {% endfor %}
        {% elif field.type == "select" %}
        <select name="{{ field.name }}" class="form-control">
            {% for choice in field.choices %}
            <option value="{{ choice }}">{{ choice }}</option>
            {% endfor %}
        </select>
        {% elif field.type == "textarea" %}
            {% if field.rows %}
            <textarea name="{{ field.name }}" class="form-control" rows="{{ field.rows }}"></textarea>
            {% else %}
            <textarea name="{{ field.name }}" class="form-control"></textarea>
            {% endif %}
        {% elif field.type == "email" %}
        <input type="email" name="{{ field.name }}" class="form-control">
        {% elif field.type == "hidden" %}
        <input type="hidden" name="{{ field.name }}" value="{{ field.value }}">
        {% elif field.type == "range" %}
        <input type="range" name="{{ field.name }}" class="form-control">
        {% elif field.type == "search" %}
        <input type="search" name="{{ field.name }}" class="form-control">
        {% elif field.type == "datetime-local" %}
        <input type="datetime-local" name="{{ field.name }}" class="form-control">
        {% elif field.type == "time" %}
        <input type="time" name="{{ field.name }}" class="form-control">
        {% elif field.type == "datetime" %}
        <input type="datetime" name="{{ field.name }}" class="form-control">
        {% elif field.type == "month" %}
        <input type="month" name="{{ field.name }}" class="form-control">
        {% elif field.type == "week" %}
        <input type="week" name="{{ field.name }}" class="form-control">
        {% elif field.type == "color" %}
        <input type="color" name="{{ field.name }}" class="form-control">
        {% elif field.type == "url" %}
        <input type="url" name="{{ field.name }}" class="form-control">
        {% elif field.type == "tel" %}
        <input type="tel" name="{{ field.name }}" class="form-control">
        {% endif %}
        </div>
        {% endfor %}
     
        <div class="form-actions">
            <button type="submit" class="btn btn-primary">提交</button>
            <a href="{% url 'post_list' %}" class="btn btn-secondary">返回列表</a>
        </div>
    </form>
```

return render(request, 'blog/create_post.html', {"fields": dynamic_fields.dynamic_fields})

**CSRF（跨站请求伪造）保护机制**：
确保 `settings.py` 中启用了 `CsrfViewMiddleware`中间件
确保表单的 `action` 属性指向正确的 URL，并且该 URL 与 CSRF Token 的作用域一致。

确保表单包含 `{% csrf_token %}`CSRF 防护

```python
from django.views.decorators.csrf import csrf_protect

@csrf_protect
def my_view(request):
```

为特定视图禁用 CSRF（仅用于测试）

```python
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def my_view(request):
```

**分页展示**

```python
from django.core.paginator import Paginator
from django.shortcuts import render

def post_list(request):
    posts = Post.objects.all()
    # posts = Post.objects.all().order_by('-id') # 按照 ID 倒序排列，从新到旧
    paginator = Paginator(posts, 10)  # 每页显示 10 条数据
    page_number = request.GET.get('page')
    page_obj = paginator.get_page(page_number)
    return render(request, 'blog/post_list.html', {'posts': page_obj})
```

```html
{% for post in posts %}
# ......
{% endif %}

<div class="pagination">
    {% if posts.has_previous %}
        <a href="?page=1">« First</a>
        <a href="?page={{ posts.previous_page_number }}">Previous</a>
    {% endif %}

    {% for num in posts.paginator.page_range %}
        {% if posts.number == num %}
            <span class="active">{{ num }}</span>
        {% else %}
            <a href="?page={{ num }}">{{ num }}</a>
        {% endif %}
    {% endfor %}

    {% if posts.has_next %}
        <a href="?page={{ posts.next_page_number }}">Next</a>
        <a href="?page={{ posts.paginator.num_pages }}">Last »</a>
    {% endif %}
```

**添加编号**
编号规则是 `QSA<YYYYMMDD><两位编号>-<复制次数>`

```python
# models.py
qsa_number = models.CharField(max_length=20, unique=True, null=True, blank=True)  # 新增字段，用于保存编号

# views.py
from datetime import datetime

def generate_qsa_number():
    """
    生成唯一的 QSA 编号，格式为 QSA<YYYYMMDD><两位编号>_1
    """
    today = datetime.now().strftime('%Y%m%d')  # 获取当前日期，格式为 YYYYMMDD
    prefix = f"QSA{today}"  # 编号前缀

    # 查询当天已有编号
    existing_qsas = Post.objects.filter(qsa_number__startswith=prefix).values_list('qsa_number', flat=True)

    # 提取当天的最大编号
    max_number = 0
    for qsa_number in existing_qsas:
        try:
            main_part, _ = qsa_number.rsplit('_', 1)  # 分离主部分和复制次数
            number = int(main_part[len(prefix):])  # 提取两位编号
            max_number = max(max_number, number)
        except ValueError:
            continue  # 忽略格式不正确的编号

    # 生成新的编号
    new_number = max_number + 1
    return f"{prefix}{str(new_number).zfill(2)}-1"
```

```python
from django.forms.models import model_to_dict

@permission_required('mqsa.add_post')
def qsa_copy(request, pk):
    # 获取原始对象
    original_post = get_object_or_404(Post, pk=pk)

    # 检查原始对象是否有编号
    if not original_post.qsa_number:
        # 如果编号不存在，生成一个新的编号
        original_post.qsa_number = generate_qsa_number()
        original_post.save()

    # 提取原始编号
    original_number = original_post.qsa_number

    # 分离编号的主部分和复制次数
    main_part, suffix = original_number.rsplit('_', 1)
    new_suffix = int(suffix) + 1  # 复制次数递增
    new_qsa_number = f"{main_part}-{new_suffix}"  # 生成新的编号

    # 将对象转换为字典
    post_data = model_to_dict(original_post)
    post_data.pop('id', None)  # 移除主键字段以避免冲突
    post_data['qsa_number'] = new_qsa_number  # 更新编号

    # 创建新对象
    new_post = Post.objects.create(**post_data)

    return redirect('qsa_edit', pk=new_post.pk)  # 跳转到编辑页面
```

**用户认证**
登录视图示例：

```python
from django.contrib.auth import authenticate, login

def user_login(request):
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('home')
    return render(request, 'login.html')
```

**REST API** API用于前后端分离项目
使用Django REST Framework生成REST API风格的API
安装 DRF：`pip install djangorestframework`

[Postman](https://www.postman.com/downloads/)是一款常用的 API 测试工具，可以方便地进行接口测试、调试和文档编写。

以books应用为例：

```python
# myproject/settings.py 配置项目设置
INSTALLED_APPS = [
    ...
    'rest_framework',
    'books.apps.BooksConfig'
]

REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.AllowAny'
    ]
}

# books/models.py  定义数据模型
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.CharField(max_length=100)
    published_date = models.DateField()
    isbn = models.CharField(max_length=13, unique=True)
    price = models.DecimalField(max_digits=6, decimal_places=2)

    def __str__(self):
        return self.title

# books/serializers.py  创建序列化器
from rest_framework import serializers
from .models import Book

class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = ['id', 'title', 'author', 'published_date', 'isbn', 'price']

# books/views.py 构建视图集
from rest_framework import viewsets
from .models import Book
from .serializers import BookSerializer

class BookViewSet(viewsets.ModelViewSet):
    queryset = Book.objects.all().order_by('-published_date')
    serializer_class = BookSerializer

# books/urls.py  配置路由
from django.urls import include, path
from rest_framework import routers
from books import views

router = routers.DefaultRouter()
router.register(r'books', views.BookViewSet)

urlpatterns = [
    path('api/', include(router.urls)),
    path('api-auth/', include('rest_framework.urls'))
]

# myproject/urls.py
from django.urls import include, path

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('api.urls')),
]
```

```bash
python manage.py makemigrations
python manage.py migrate
```

==RESTful API 端点说明==

| HTTP方法 | URL           | 功能描述       | 示例请求体 (JSON)                        |
| -------- | ------------- | -------------- | ---------------------------------------- |
| GET      | /api/books/   | 获取所有书籍   | 无需请求体                               |
| POST     | /api/books/   | 创建新书       | `{"title":"...", "author":"...", ...}` |
| GET      | /api/books/1/ | 获取ID=1的书籍 | 无需请求体                               |
| PUT      | /api/books/1/ | 更新ID=1的书籍 | `{"title":"新版书名", ...}`            |
| DELETE   | /api/books/1/ | 删除ID=1的书籍 | 无需请求体                               |

==前端调用示例 (JavaScript)==

```javascript
// 获取所有书籍
fetch('/api/books/')
  .then(response => response.json())
  .then(data => {
    console.log('所有书籍:', data);
    // 渲染到页面
    data.forEach(book => {
      document.getElementById('book-list').innerHTML += `
        <div class="book-item">
          <h3>${book.title}</h3>
          <p>作者: ${book.author}</p>
          <p>价格: ¥${book.price}</p>
        </div>
      `;
    });
  })
  .catch(error => console.error('获取失败:', error));

// 创建新书
const newBook = {
  title: 'JavaScript高级程序设计',
  author: 'Nicholas C. Zakas',
  published_date: '2023-10-01',
  isbn: '9787121430879',
  price: 99.80
};

fetch('/api/books/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(newBook)
})
.then(response => {
  if (!response.ok) throw new Error('创建失败');
  return response.json();
})
.then(data => console.log('创建成功:', data))
.catch(error => console.error('错误:', error));

// 更新书籍
const updatedData = {
  price: 89.90  // 调整价格
};

fetch('/api/books/1/', {  // 假设ID=1
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(updatedData)
})
.then(response => response.json())
.then(data => console.log('更新后数据:', data))
.catch(error => console.error('更新失败:', error));

// 删除书籍
fetch('/api/books/1/', {
  method: 'DELETE'
})
.then(response => {
  if (response.status === 204) {
    console.log('删除成功');
  }
})
.catch(error => console.error('删除失败:', error));
```

html示例：

```html
<!DOCTYPE html>
<html>
<head>
    <title>图书管理系统</title>
</head>
<body>
    <h1>图书列表</h1>
    <div id="book-list"></div>

    <script>
        // 获取所有书籍
        fetch('http://127.0.0.1:8000/api/books/')
            .then(response => response.json())
            .then(data => {
                const listDiv = document.getElementById('book-list');
                data.forEach(book => {
                    listDiv.innerHTML += `
                        <div style="border:1px solid #ccc; padding:10px; margin:10px">
                            <h3>${book.title}</h3>
                            <p>作者：${book.author}</p>
                            <p>价格：¥${book.price}</p>
                        </div>
                    `;
                });
            })
            .catch(error => console.error('错误:', error));
    </script>
</body>
</html>
```

##### 生产环境部署

**使用 Gunicorn 运行 Django**

```bash
pip install gunicorn
gunicorn myproject.wsgi:application --bind 0.0.0.0:8000 --workers 4
```

**配置 Nginx 反向代理**
在 `/etc/nginx/sites-available/myproject` 中添加配置：

```nginx
server {
    listen 80;
    server_name example.com;

    location /static/ {
        root /path/to/your/project;
    }

    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
    }
}
```

**安全设置**
关闭 Debug 模式：修改 `settings.py`

```python
DEBUG = False
ALLOWED_HOSTS = ['example.com']
```

配置 HTTPS：使用 Let's Encrypt 生成 SSL 证书。

**跨域问题（CORS）**

安装 `django-cors-headers` 并配置：

```python
# settings.py
INSTALLED_APPS = [
    ...
    'corsheaders',
]

MIDDLEWARE = [
    ...
    'corsheaders.middleware.CorsMiddleware',
]

CORS_ALLOWED_ORIGINS = [
    'https:example.com',  # 添加你的域名
]
# CORS_ALLOW_ALL_ORIGINS = True  # 开发环境临时允许所有域名
```

**用户认证系统**
Django 的 `django.contrib.auth` 已提供完整的用户认证和权限管理模块，无需额外创建应用即可直接使用。

```python
# settings.py
INSTALLED_APPS = [
    # ...
    'django.contrib.auth',     # 用户认证核心功能
    'django.contrib.contenttypes',  # 权限依赖
    # ...
]

# 登录后重定向路径 如果没有设置，默认重定向到/accounts/login/页面
LOGIN_REDIRECT_URL = '/dashboard/'
# 登录页面路径
LOGIN_URL = '/login/'
```

```python
# 项目的urls.py
urlpatterns = [
    # 其他 URL 配置...
    path('accounts/', include('django.contrib.auth.urls')),  # 引入认证相关 URL
]
```

这会自动提供以下视图：

- `/accounts/login/`：登录页面
- `/accounts/logout/`：登出页面
- `/accounts/password_change/`：修改密码页面
- `/accounts/password_reset/`：重置密码页面

直接在现有视图函数或类视图上使用装饰器即可实现权限控制
如 `@login_required`、`@permission_required`

```python
# views.py（现有应用的视图文件）
from django.contrib.auth.decorators import login_required, permission_required

@login_required   # 必须登录
def dashboard(request):
    return render(request, 'dashboard.html')

@permission_required('blog.publish_post')   # 需要特定权限
def publish_post(request):
    return HttpResponse("文章已发布")
```

Django 会为每个模型自动生成以下默认权限：使用 `应用名.权限` 指定

1. `add_<modelname>`：添加模型实例的权限。
2. `change_<modelname>`：更改模型实例的权限。
3. `delete_<modelname>`：删除模型实例的权限。
4. `view_<modelname>`（从 Django 2.1 开始）：查看模型实例的权限

Django 默认会寻找 login.html 作为登录页面模板

```html
<!-- templates\registration\login.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .login-container {
            background-color: #ffffff;
            padding: 20px 30px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 300px;
            text-align: center;
        }
        .login-container h2 {
            margin-bottom: 20px;
            color: #333333;
        }
        .login-container form {
            display: flex;
            flex-direction: column;
        }
        .login-container form input {
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #cccccc;
            border-radius: 4px;
            font-size: 14px;
        }
        .login-container form button {
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 16px;
            cursor: pointer;
        }
        .login-container form button:hover {
            background-color: #45a049;
        }
        .login-container a {
            display: block;
            margin-top: 10px;
            color: #4CAF50;
            text-decoration: none;
            font-size: 14px;
        }
        .login-container a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="login-container">
        <h2>Login</h2>
        <form method="post">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit">Login</button>
        </form>
        <a href="{% url 'password_reset' %}">Forgot Password?</a>
    </div>
</body>
</html>
```

登录的有效期取决于后端会话配置，通常由 Django 的会话框架控制。默认情况下，Django 使用基于 cookie 的会话，默认有效期为浏览器关闭时失效（会话 cookie）。 如果需要更改会话有效期，可以在 Django 的 `settings.py` 文件中设置 `SESSION_COOKIE_AGE`，以秒为单位。例如：`SESSION_COOKIE_AGE = 3600` 表示会话有效期为 1 小时。
Django 的默认登出视图 (`LogoutView`) 只接受 `POST` 请求，模板中使用表单而不是登出链接，确保登出操作通过 `POST` 请求完成

```html
<form method="post" action="{% url 'logout' %}" style="display: inline;">
    {% csrf_token %}
    <button type="submit" class="btn">登出</button>
</form>
```

可以通过 Django 管理后台（`/admin/`）为用户分配权限或分组

如果项目需要 ==高度定制化用户系统==（如扩展用户字段、自定义权限逻辑），可以新建一个应用（如 `users`）来集中管理
如果默认权限不足，你可以为模型定义自定义权限。
修改登出后的界面

```python
# users/views.py
from django.shortcuts import render

def logout_success(request):
    return render(request, 'registration/logout_success.html')

# users/urls.py
    # ...
    path('logout/success/', views.logout_success, name='logout_success'),
```

```html
<!-- templates/registration/logout_success.html -->
<!DOCTYPE html>
<html>
<head>
    <title>登出成功</title>
</head>
<body>
    <h2>您已成功登出</h2>
    <a href="{% url 'login' %}">重新登录</a>
</body>
</html>
```

实现注册功能

```python
# users/models.py
from django.contrib.auth.models import AbstractUser

class CustomUser(AbstractUser):
    phone = models.CharField(max_length=15, blank=True, verbose_name='手机号')
    
    class Meta:
        verbose_name = '用户'
        verbose_name_plural = '用户管理'
        permissions = [
            ("publish_post", "允许发布文章"),
            ("edit_others_post", "可编辑他人文章"),
        ]


# settings.py
AUTH_USER_MODEL = 'users.CustomUser'


# users/views.py
from django.contrib.auth.views import LoginView
from django.views.generic import CreateView
from .forms import CustomUserCreationForm

class CustomLoginView(LoginView):
    template_name = 'users/login.html'

class SignUpView(CreateView):
    form_class = CustomUserCreationForm
    template_name = 'users/signup.html'
    success_url = '/login/'
```

```html
<!-- templates/auth/login.html -->
<form method="post">
  {% csrf_token %}
  {{ form.as_p }}
  <button type="submit">登录</button>
</form>
```

django用户管理模块基本操作

用户注册

```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import UserCreationForm
from django.contrib.auth import login

def signup(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()
            login(request, user)
            return redirect('mqsa_list')  # 登录后跳转到某个页面
    else:
        form = UserCreationForm()
    return render(request, 'registration/signup.html', {'form': form})
```

```python
#注册新用户
from django.contrib.auth.models import User
user = User.objects.create_user(username='123', email='', password='123')
user.save()
```

```python
from django.contrib.auth.models import Group, Permission

# 创建编辑组并分配权限
editors_group, created = Group.objects.get_or_create(name='编辑组')
edit_permission = Permission.objects.get(codename='edit_others_post')
editors_group.permissions.add(edit_permission)


user = User.objects.get(username='john')
user.groups.add(editors_group)
```

**异步文件上传**

```html
<!-- HTML部分 -->
<div class="upload-group">
  <label>合同附件：</label>
  <div class="drop-zone">
    拖拽文件到这里或点击选择
    <input type="file" class="async-upload" style="display:none;" multiple>
  </div>
  <div class="upload-status"></div>
</div>

<style>
/* 基础样式 */
.upload-group {
  margin: 20px 0;
  padding: 15px;
  border: 1px solid #ddd;
}

.drop-zone {
  border: 2px dashed #ccc;
  padding: 20px;
  text-align: center;
  margin: 10px 0;
  transition: all 0.3s;
}

.drop-zone.dragover {
  border-color: #2196F3;
  background-color: #f5fbff;
}

.upload-item {
  margin: 10px 0;
  padding: 10px;
  border: 1px solid #eee;
}

.progress-bar {
  width: 200px;
  height: 20px;
  background-color: #f0f0f0;
  display: inline-block;
  vertical-align: middle;
}

.progress {
  width: 0%;
  height: 100%;
  background-color: #4CAF50;
  transition: width 0.3s ease;
}

.btn-cancel {
  margin-left: 10px;
  padding: 2px 8px;
  background-color: #ff4444;
  color: white;
  border: none;
  cursor: pointer;
}
</style>

<script>
// 初始化所有上传控件
document.querySelectorAll('.async-upload').forEach(input => {
  initFileUpload(input);
});

function initFileUpload(input) {
  const container = input.closest('.upload-group');
  const dropZone = container.querySelector('.drop-zone');
  const statusDiv = container.querySelector('.upload-status');
  
  // 点击触发文件选择
  dropZone.addEventListener('click', () => input.click());
  
  // 拖拽事件处理
  dropZone.addEventListener('dragover', (e) => {
    e.preventDefault();
    dropZone.classList.add('dragover');
  });

  dropZone.addEventListener('dragleave', () => {
    dropZone.classList.remove('dragover');
  });

  dropZone.addEventListener('drop', (e) => {
    e.preventDefault();
    dropZone.classList.remove('dragover');
    const files = Array.from(e.dataTransfer.files);
    if (files.length > 0) {
      handleFileUpload(files, statusDiv, getUploadOptions(input));
    }
  });

  // 文件选择事件
  input.addEventListener('change', async function(e) {
    const files = Array.from(e.target.files);
    if (files.length === 0) return;
    await handleFileUpload(files, statusDiv, getUploadOptions(input));
  });
}

// 获取上传配置
function getUploadOptions(input) {
  return {
    fileType: input.dataset.fileType,
    maxSize: 10 * 1024 * 1024, // 10MB
    allowedTypes: ['image/', 'application/pdf'],
    endpoint: '/async_upload/' // Django上传端点
  };
}

// 完整的上传处理函数
async function handleFileUpload(files, statusDiv, options) {
  // 清空之前的错误提示
  statusDiv.querySelectorAll('.error').forEach(el => el.remove());

  // 验证文件
  for (const file of files) {
    if (file.size > options.maxSize) {
      showError(statusDiv, `文件 ${file.name} 超过${options.maxSize/1024/1024}MB限制`);
      return;
    }
    if (!options.allowedTypes.some(type => file.type.startsWith(type))) {
      showError(statusDiv, `文件类型 ${file.type} 不被支持`);
      return;
    }
  }

  // 逐个上传文件
  for (const file of files) {
    const formData = new FormData();
    formData.append('file', file);
    formData.append('file_type', options.fileType);
  
    // 创建上传状态条目
    const statusItem = createStatusItem(file);
    statusDiv.appendChild(statusItem);

    try {
      const xhr = new XMLHttpRequest();
      statusItem.xhr = xhr; // 存储xhr引用
    
      // 创建取消按钮
      const cancelBtn = statusItem.querySelector('.btn-cancel');
      cancelBtn.onclick = () => {
        xhr.abort();
        statusItem.remove();
      };

      await new Promise((resolve, reject) => {
        xhr.upload.addEventListener('progress', (e) => {
          if (e.lengthComputable) {
            const percent = Math.round((e.loaded / e.total) * 100);
            updateProgress(statusItem, percent, '上传中...');
          }
        });

        xhr.onreadystatechange = () => {
          if (xhr.readyState === XMLHttpRequest.DONE) {
            if (xhr.status === 200) {
              const response = JSON.parse(xhr.responseText);
              if (response.status === 'success') {
                statusItem.dataset.fileKey = response.file_key;
                updateProgress(statusItem, 100, '上传完成');
                resolve();
              } else {
                updateProgress(statusItem, 0, response.message, true);
                reject(new Error(response.message));
              }
            } else {
              updateProgress(statusItem, 0, `上传失败: ${xhr.status}`, true);
              reject(new Error(`HTTP错误: ${xhr.status}`));
            }
          }
        };

        xhr.onerror = () => {
          updateProgress(statusItem, 0, '网络错误', true);
          reject(new Error('网络错误'));
        };

        xhr.open('POST', options.endpoint);
        xhr.setRequestHeader('X-Requested-With', 'XMLHttpRequest');
        xhr.send(formData);
      });
    } catch (error) {
      console.error('上传失败:', error);
      if (!error.message.includes('abort')) {
        showError(statusDiv, error.message);
      }
    }
  }
}

// 创建状态条目
function createStatusItem(file) {
  const div = document.createElement('div');
  div.className = 'upload-item';
  div.innerHTML = `
    <div class="file-info">
      <span class="filename">${file.name}</span>
      <span class="file-size">(${(file.size/1024/1024).toFixed(2)}MB)</span>
    </div>
    <div class="progress-container">
      <div class="progress-bar">
        <div class="progress" style="width: 0%"></div>
      </div>
      <span class="status-text">等待上传...</span>
      <button class="btn-cancel">取消</button>
    </div>
  `;
  return div;
}

// 更新进度显示
function updateProgress(item, percent, text, isError = false) {
  const progressBar = item.querySelector('.progress');
  const statusText = item.querySelector('.status-text');
  
  progressBar.style.width = `${percent}%`;
  statusText.textContent = text;
  statusText.style.color = isError ? '#ff4444' : '#666';
  
  if (percent === 100) {
    item.querySelector('.btn-cancel').remove();
  }
}

// 显示错误信息
function showError(container, message) {
  const div = document.createElement('div');
  div.className = 'error';
  div.style.color = '#ff4444';
  div.textContent = message;
  container.appendChild(div);
}

// 表单提交时收集所有file_key
document.querySelector('form').addEventListener('submit', function(e) {
  const fileKeys = [];
  document.querySelectorAll('.upload-item').forEach(item => {
    if (item.dataset.fileKey) {
      fileKeys.push(item.dataset.fileKey);
    }
  });
  
  // 添加隐藏字段
  const input = document.createElement('input');
  input.type = 'hidden';
  input.name = 'file_keys';
  input.value = JSON.stringify(fileKeys);
  this.appendChild(input);
});
</script>
```

```python
# views.py
from django.views.decorators.http import require_POST

@require_POST
@login_required
def submit_form(request):
    try:
        file_keys = json.loads(request.POST.get('file_keys', '[]'))
        for key in file_keys:
            # 验证并移动文件
            record = TempUpload.objects.get(
                file_key=key,
                user=request.user
            )
            # 实际移动操作（示例使用本地文件系统）
            os.rename(
                os.path.join(settings.TEMP_FILE_ROOT, record.file_path),
                os.path.join(settings.MEDIA_ROOT, record.file_path)
            )
            # 创建业务模型记录
            Document.objects.create(
                user=request.user,
                file_type=record.file_type,
                file=record.file_path
            )
            record.delete()
        return HttpResponseRedirect('/success/')
    except Exception as e:
        return JsonResponse({'status': 'error', 'message': str(e)})
```

##### 完整的示例

完整的示例，并进行了改进和美化，仅供测试
后续可参考REST API、更改数据库和生产环境部署的部分

初始化项目：`django-admin startproject myproject`
创建应用 ：`python manage.py startapp blog`

```text
myproject/
│  # 手动创建，保存资源文件.myproject/settings.py、templates/blog/xxx.html
├─ assets/
│   ├─ css/
│   ├─ fonts/
│   ├─ images/
│   └─ js/
├─ myproject/
│   ├─ __init__.py
│   ├─ asgi.py 
│   ├─ settings.py
│   ├─ urls.py
│   └─ wsgi.py
├─ blog/        # 应用目录
│	├─ migrations
│	│      └─ __init__.py
│	├─ __init__.py
│	├─ admin.py
│	├─ apps.py
│	├─ models.py
│	├─ tests.py
│	├─ views.py
│	│  # 手动创建，保存表单.blog/views.py、models.py、templates/blog/xxx.html
│	├─ dynamic_fields.py
│	└─ urls.py   # 手动创建，分路由文件.myproject/urls.py
├─ files/        # 手动创建，保存用户上传的文件.blog/views.py、models.py
├─ temp_files/   # 手动创建，保存临时文件.blog/views.py、models.py
│   # 手动创建，保存各应用的模板文件.myproject/settings.py、blog/views.py
├─ templates/  
│    └─ blog/
└─ manage.py 
```

修改myproject/settings.py文件：

```python
# 测试环境可以填*，允许所有ip
ALLOWED_HOSTS = ['*']

# 注册应用
INSTALLED_APPS = [
    ...
    'blog',
]

TEMPLATES = [
    {
        ...
        'DIRS': [os.path.join(BASE_DIR, 'templates'),
         os.path.join(BASE_DIR, 'static').replace('\\', '/')],
		...
    },
]

# 静态文件的 URL 前缀
STATIC_URL = '/static/'
# 静态文件的根目录（可选，通常用于 collectstatic）
STATIC_ROOT = BASE_DIR / 'staticfiles'
# 额外的静态文件目录（可选）
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'assets').replace('\\', '/'),
]
```

### 网络爬虫

  requests
  **scrapy**
  pyspider
  beautifuisoup4
  selenium
  lxml

#### requests（网络爬虫）

见[[../../../计算机安全/网络安全/Python网络爬虫|Python网络爬虫]]

#### beautifulsoup

### dill（对象序列化）

```python
import dill

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# 创建一个Person实例
person = Person("Alice", 30)

# 序列化实例到文件
with open('person_instance.dill', 'wb') as f:
    dill.dump(person, f)

# 反序列化实例
with open('person_instance.dill', 'rb') as f:
    new_person = dill.load(f)
```

### pywin32

提供对windows win32 api的调用

### 打包

py2exe

打包时最好使用包虚拟环境，减小Size

#### PyInstaller

PyInstaller是一个开源的Python打包工具，可以将Python程序转换为独立的可执行文件。它支持Windows、Linux和macOS平台，能够将Python程序打包成一个或多个文件，这些文件可以在没有Python解释器的环境中运行。`pip install pyinstaller`

命令行界面，切换到Python脚本所在的目录，运行 `pyinstaller -F app.py`

#### auto-py-to-exe

auto-py-to-exe是一个图形用户界面(GUI)工具，它简化了使用PyInstaller打包Python程序的过程。它提供了一个直观的界面，用户可以通过简单的操作来配置和打包Python程序。 `pip install auto-py-to-exe`

命令行界面，运行 `auto-py-to-exe`  即可打开图形化界面

#### Buildozer

Buildozer 是一个将[[#Kivy]] 应用程序打包成 APK 的工具

Buildozer 主要是为 Linux 和 macOS 设计的，在 Windows 系统上可以使用：WSL、Docker、虚拟机

更新系统并安装依赖项:

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y python3-pip python3-setuptools python3-virtualenv git zip unzip openjdk-17-jdk

pip install buildozer
```

初始化 Buildozer：
在项目目录下运行命令 `buildozer init`（老版本linux使用 `python3 -m buildozer init`）
这会生成一个 buildozer.spec 文件。

```ini
`source.include_exts`：确保包含所有需要的文件
`requirements`：添加 `kivy` 和其他依赖项
`title` 和 `package.name`：设置应用程序的名称和包名
```

运行命令 `buildozer -v android debug` 打包 APK：这会在 `bin` 目录下生成一个 APK 文件

### rich（终端美化）

> Rich 是一个 Python 库，用于向终端写入带颜色和样式的丰富文本，以及显示高级内容，如表格、Markdown 和语法高亮的代码。

基于 rich 的 print 方法输出的内容都是带颜色、带重点的，相比于Python自带的 print 有明显的优势

```python
from rich import print as rprint
rprint("Hello, [bold magenta]World[/bold magenta]!", ":vampire:", locals())
```

#### 控制台

**Console 控制台输出**

```python
from rich.console import Console
# 构造一个控制台对象
console = Console()

# console.print会将文字自动换行以适合终端宽度。可以通过style自定义颜色和样式
console.print("Hello", "World!", style="bold red")
console.print("FOO", style="white on blue")
# 可以使用类似bbcode的标记语言
console.print("[blue underline]Looks like a link")
console.print("Where there is a [bold cyan]Will[/bold cyan] there [u]is[/u] a [i]way[/i].")
# 将名称放在两个冒号之间即可在控制台输出中插入表情符号，或使用Unicode编码
console.print(":smiley: :vampire: :pile_of_poo: :thumbs_up: \U0001F600")
# 创建一个可点击的链接
console.print("Google", style="link https://google.com")
```

**Console 控制台记录**

```python
from rich.console import Console
console = Console()

test_data = [
    {"jsonrpc": "2.0", "method": "sum", "params": [None, 1, 2, 4, False, True], "id": "1",},
    {"jsonrpc": "2.0", "method": "notify_hello", "params": [7]},
    {"jsonrpc": "2.0", "method": "subtract", "params": [42, 23], "id": "2"},
]

console.log(test_data, log_locals=True)
```

**打印 JSON**
`print_json()` 方法将格式化和样式化包含 JSON 的字符串

```python
from rich.console import Console
console = Console()
console.print_json('[false, true, null, "foo"]')
# 也可以记录一个 `JSON` 对象并打印
from rich.json import JSON
console.log(JSON('["foo", "bar"]'))
```

也可以通过命令行使用 `python -m rich.json cats.json` 美化打印 JSON

低级输出
console.out("Locals", locals())

Rules
console.rule("[bold red]Chapter 2")

Status
python -m rich.status

打印print和日志log支持一个 `justify` 参数，“default、“left”、“right”、“center”或“full”。
左对齐会将文本右侧填充空格，而默认对齐则不会。只有当您使用 style 参数设置背景颜色时，您才会注意到这种差别。
打印print支持 `overflow`参数，“fold”，“crop”，“ellipsis”或“ignore”。当打印的文本大于可用空间时，把任何多余的字符放在下一行；在行尾截断文本；在行尾截断文本并插入省略号字符...；忽视

 控制台样式
 控制台有一个 style 属性，您可以使用它来应用您打印的所有内容的样式。默认情况下 style 为 None

```python
from rich.console import Console
blue_console = Console(style="white on blue")
blue_console.print("I'm blue")
```

控制台类有一个 `input()` 方法，它的工作方式与 Python 内置的 `input()` 函数相同，但可以使用 Rich 可以打印的任何内容作为提示

```python
from rich.console import Console
console = Console()
console.input("What is [i]your[/i] [bold red]name[/]? :smiley: ")
```

控制台类可以将写入的内容导出为文本、svg 或 html。

```python
from rich.console import Console
from rich.terminal_theme import MONOKAI

# 告诉 Rich保存任何你 `print()` 或 `log()` 的数据的副本
console = Console(record=True)
# 保存svg
console.save_svg("example.svg", theme=MONOKAI)
# 设置主题为MONOKAI（可以自己构建rich.terminal_theme.TerminalTheme实例作为主题）
# 可以print(rich.terminal_theme)找到terminal_theme.py查看有哪些主题
```

您可以告诉控制台对象将内容写入文件，通过在构造函数中设置 `file` 参数——它应该是一个用于写入文本的文件对象。您可以使用此方法将内容写入文件，而输出永远不会出现在终端上。

```python
import sys
from rich.console import Console
from datetime import datetime

with open("report.txt", "wt") as report_file:
    console = Console(file=report_file)
    console.rule(f"Report Generated {datetime.now().ctime()}")
```

如果您有一些长输出需要向用户展示，可以使用分页器来显示。分页器通常是操作系统上的一个应用程序，它至少支持按键滚动，但通常还支持上下滚动文本和其他功能。

```python
from rich.__main__ import make_test_card
from rich.console import Console

console = Console()
with console.pager():
    console.print(make_test_card())
```

#### 显示高级内容

**表格**

```python
from rich.console import Console
from rich.table import Column, Table

console = Console()

table = Table(show_header=True, header_style="bold magenta")
table.add_column("Date", style="dim", width=12)
table.add_column("Title")
table.add_column("Production Budget", justify="right")
table.add_column("Box Office", justify="right")
table.add_row(
    "Dev 20, 2019", "Star Wars: The Rise of Skywalker", "$275,000,000", "$375,126,118"
)
table.add_row(
    "May 25, 2018",
    "[red]Solo[/red]: A Star Wars Story",
    "$275,000,000",
    "$393,151,347",
)
table.add_row(
    "Dec 15, 2017",
    "Star Wars Ep. VIII: The Last Jedi",
    "$262,000,000",
    "[bold]$1,332,539,889[/bold]",
)

console.print(table)
```

**Markdown**

```python
MARKDOWN = """
# This is an h1

Rich can do a pretty *decent* job of rendering markdown.

1. This is a list item
2. This is another list item
"""
from rich.console import Console
from rich.markdown import Markdown

console = Console()
md = Markdown(MARKDOWN)
console.print(md)
```

在终端中显示了 readme 文件：`python -m rich.markdown README.md`

**语法突出显示**
构造一个 Syntax 对象并将其打印到控制台

```python
from rich.console import Console
from rich.syntax import Syntax

my_code = '''
def iter_first_last(values: Iterable[T]) -> Iterable[Tuple[bool, bool, T]]:
    """Iterate and generate a tuple with a flag for first and last value."""
    iter_values = iter(values)
    try:
        previous_value = next(iter_values)
    except StopIteration:
        return
    first = True
    for value in iter_values:
        yield first, False, previous_value
        first = False
        previous_value = value
    yield first, True, previous_value
'''
syntax = Syntax(my_code, "python", theme="monokai", line_numbers=True)
console = Console()
console.print(syntax)
```

#### 进度条

官方范例：`python -m rich.progress`

简单进度条

```python
import time
from rich.progress import track

for i in track(range(20), description="Processing..."):
    time.sleep(0.5)  # Simulate work being done
```

多进程进度条

```python
import time
from rich.progress import Progress

with Progress() as progress:
    task1 = progress.add_task("[red]Downloading...", total=100)
    task2 = progress.add_task("[green]Processing...", total=100)
    task3 = progress.add_task("[cyan]Cooking...", total=100)

    while not progress.finished:
        progress.update(task1, advance=0.5)
        progress.update(task2, advance=0.3)
        progress.update(task3, advance=0.9)
        time.sleep(0.02)
```

默认情况下，进度信息将每秒刷新 10 次。您可以通过在构造函数的 `Progress` 参数中使用 `refresh_per_second` 参数来设置刷新率。如果知道您的更新不会那么频繁，应将其设置为低于 10。

### 人工智能相关

应用见[[../../../开发/应用/人工智能/Python神经网络编程#实际应用：手写数字MNIST|手写数字MNIST]]

  scikit -learn、mxnet

sk擅长机器学习
Torch、tensor擅长深度学习
natural language toolkie 自然语言处理工具
spacy高级自然语言处理

#### PyTorch

PyTorch 是一个开源的机器学习库，主要用于进行计算机视觉（CV）、自然语言处理（NLP）、语音识别等领域的研究和开发。

`pip install torch`

使用 `numpy_1=tensor_1.numpy()`将 Tensor 转换成NumPy数组
使用 `tensor_1 = torch.from_numpy(numpy_1)` 将NumPy数组转换成 Tensor

##### 保存和加载模型

在实际应用的时候不可能每次都先进行训练然后再使用，所以就得先将之前训练好的模型保存下来，然后在需要用到的时候加载一下直接使用。
模型的本质是一堆用某种结构存储起来的参数，所以在保存的时候有两种方式，一种方式是直接将整个模型保存下来，之后直接加载整个模型，但这样会比较耗内存；另一种是只保存模型的参数，之后用到的时候再创建一个同样结构的新模型，然后把所保存的参数导入新模型。

5. `torch.save `：把序列化的对象保存到硬盘。它利用了 Python 的 pickle 来实现序列化。模型、张量以及字典都可以用该函数进行保存；
6. `torch.load`：采用 pickle 将反序列化的对象从存储中加载进来。
7. `torch.nn.Module.load_state_dict`：采用一个反序列化的 state_dict加载一个模型的参数字典。

在 PyTorch 2.6 中，将 `torch.load` 中的 `weights_only` 参数的默认值从 `False` 更改为 `True`。将 `torch.load` 重新运行并将 `weights_only` 设置为 `False` 可能会成功，但它可能导致任意代码执行。仅当您从可信来源获得文件时才这样做。

**加载/保存状态字典(推荐做法)**：

```python
# 保存的代码：通常会用 .pt 或者 .pth 后缀来保存模型
torch.save(model.state_dict(), PATH)
# 加载的代码：
model = TheModelClass(*args, **kwargs)
model.load_state_dict(torch.load(PATH))
model.eval()
```

**加载/保存整个模型**：

```python
# 保存：
torch.save(model, PATH)
# 加载：
model = torch.load(PATH)
model.eval()
```

在 CPU 上加载在 GPU 上训练的模型：

```python
device = torch.device('cpu')
model = TheModelClass(*args, **kwargs)
model.load_state_dict(torch.load(PATH, map_location=device))
```

在 GPU 上加载模型在GPU上保存模型:

```python
device = torch.device('cuda')
model = TheModelClass(*args, **kwargs)
model.load_state_dict(torch.load(PATH)
model.to(device)
```

在 GPU 上加载模型在CPU上保存模型:

```python
device = torch.device("cuda")
model = TheModelClass(*args, **kwargs)
model.load_state_dict(torch.load(PATH, map_location="cuda:0"))  # Choose whatever GPU device number you want
model.to(device)
```

#### openCV

#### 数据集

**sklearn**(scikit-learn)
1、鸢尾花数据集（Iris Dataset）：包含150朵鸢尾花的数据集，每朵花属于三个不同的物种，可以用于各种分类任务的练习。
2、手写数字数据集（Digits Dataset）：包含8x8像素的手写数字图像数据集，涵盖数字0到9
3、乳腺癌数据集（Breast Cancer Dataset）：用于乳腺癌诊断的数据集，包含从乳腺块的数字化图像中计算的特征
4、葡萄酒数据集（Wine Dataset）：包含来自三种不同葡萄品种的葡萄酒的化学分析结果。
5、糖尿病数据集（Diabetes Dataset）：用于糖尿病患者的数据集，包含十个基线变量，如年龄、性别、体重指数、平均血压和六项血清测量。

```python
from sklearn.datasets import load_iris
# load_iris/load_digits/load_breast_cancer/load_wine/load_diabetes

iris = load_iris()
X, y = iris.data, iris.target
```

**Statsmodels**

**PyTorch**
1、MNIST 数据集:-包含手写数字（0到9）的灰度图像。
2、CIFAR-10 数据集:包含 10 个不同类别的彩色图像。
3、Fashion MNIST 数据集:包含了 10 种不同的时尚物品的灰度图像。
4、ImageNet 数据集:包含大量类别的图像，用于图像分类任务。

```python
import torchvision.datasets as datasets

mnist_train = datasets.MNIST(root="./data", train=True, download=True)
mnist_test = datasets.MNIST(root="./data", train=False, download=True)
# MNIST/CIFAR10/FashionMNIST/ImageNet
```

**Tensorflow Datasets**

```python
import tensorflow_datasets as tfds
mnist, info = tfds.load("mnist", with_info=True)
# mnist/cifar10/imdb_reviews/fashion_mnist/tf_flowers
```

**Keras**

[MNIST 数据集](http://yann.lecun.com/exdb/mnist/)MNIST数据集来自美国国家标准与技术研究所, National Institute of Standards and Technology (NIST)。训练集（training set）由来自250个不同人手写的数字构成，其中50%是高中学生，50%来自人口普查局（the Census Bureau）的工作人员。测试集（test set）也是同样比例的手写数字数据，但保证了测试集和训练集的作者集不相交。
MNIST数据集一共有7万张图片，其中6万张是训练集，1万张是测试集。每张图片是28 × 28 的0 − 9的手写数字图片组成。每个图片是黑底白字的形式，黑底用0表示，白字用0-1之间的浮点数表示，越接近1，颜色越白。
MNIST是一个非常经典的手写数字数据集，许多库都包括它。当然除了导入库以外也可以自行下载对应的csv文件使用。

#### jieba（中文分词）

Jieba库是优秀的中文分词第三方库，中文文本需要通过分词获得单个的词语。

Jieba库的分词原理：利用一个中文词库，确定汉字之间的关联概率，汉字间概率大的组成词组，形成分词结果。除了分词，用户还可以添加自定义的词组。

 **1）精确模式：** 就是把一段文本精确地切分成若干个中文单词，若干个中文单词之间经过组合，就精确地还原为之前的文本。其中**不存在冗余**单词。

 **2）全模式：** 将一段文本中所有可能的词语都扫描出来，可能有一段文本它可以切分成不同的模式，或者有不同的角度来切分变成不同的词语，在全模式下，Jieba库会将各种不同的组合都挖掘出来。分词后的信息再组合起来 **会有冗余** ，不再是原来的文本。

 **3）搜索引擎模式：** 在精确模式基础上，对发现的那些长的词语，我们会对它再次切分，进而适合搜索引擎对短词语的索引和搜索。 **也有冗余** 。jieba.lcut(seg_str)   # 精简模式，返回一个列表类型的结果
jieba.lcut(seg_str, cut_all=True)   # 全模式，使用 'cut_all=True' 指定
jieba.lcut_for_search(seg_str)   # 搜索引擎模式

输入字符串，返回列表

## 调用其他编程语言

### c语言

**直接调用c的可执行程序**:

```python
import os

if __name__ == '__main__':
    c = 'a.exe' // windows .exe | linux .out
    os.system(c)
```

python调用c的lib库，可以调用c的函数

导入c动态库：

```python
from ctypes import *

test = CDLL("./a.dll")
test.main()     // 可以调用c的函数，包括main函数
// 需要稍微注意，print(test.main())会同时打印main中的printf函数以及返回值
// 不知道为什么，int没有指定返回值在c中返回1，python返回-1363263091 还有viod 
// 不知道为什么，有时返回-1462550131，无法复现
// 而且传参数不对也不报错
```

将C打包成模块

```python
from distutils.core import setup, Extension #这里要用到distutils库
module1 = Extension('Test', sources = ['test.c']) #打包文件为test.c，这里没有设置路径，所有.c文件和setup.py放在同一目录下
setup (name = 'Test', #打包名
       version = '1.0', #版本
       description = 'This is a demo package', #说明文字
       ext_modules = [module1])
```

python setup.py build --compiler msvc # 编译代码
python setup.py build --compiler msvc install # 编译代码并直接将包放入当前python环境的包的路径以供调用
