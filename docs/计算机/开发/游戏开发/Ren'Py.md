# Ren'Py

[Ren'Py](https://github.com/renpy/renpy) 是一款开源的视觉小说引擎

下载[Ren'Py](https://www.renpy.org/latest.html)

[Ren'Py参考文档 ](https://doc.renpy.cn/zh-CN/)
运行renpy.exe引擎自带一个教学项目和一个示例项目

## 项目

ctrl+D

### 创建一个新项目

在启动器(launcher)界面选择“创建新项目”创建一个新项目。
如果这是你第一次创建项目，Ren’Py可能会要求你选择一个项目目录。

使用Vscode进行文本编辑，需要下载Ren'Py Language插件
编辑  `script.rpy` 文件。默认内容为：

```renpy
# 游戏的脚本可置于此文件中。

# 声明此游戏使用的角色。颜色参数可使角色姓名着色。

define e = Character("艾琳")


# 游戏在此开始。

label start:

    # 显示一个背景。此处默认显示占位图，但您也可以在图片目录添加一个文件
    # （命名为 bg room.png 或 bg room.jpg）来显示。

    scene bg room

    # 显示角色立绘。此处使用了占位图，但您也可以在图片目录添加命名为
    # eileen happy.png 的文件来将其替换掉。

    show eileen happy

    # 此处显示各行对话。

    e "您已创建一个新的 Ren'Py 游戏。"

    e "当您完善了故事、图片和音乐之后，您就可以向全世界发布了！"

    # 此处为游戏结尾。

    return
```

可以修改script.rpy里的内容，回到启动器(launcher)主界面，选择“启动项目”运行。

### 项目结构

创建的项目中game目录下会包含下列目录和文件。

|  目录   |  作用   |
| --- | --- |
|  audio/   |   保存音频文件  |
|cache/|包含缓存文件 </br> 创作者不需要编辑|
|gui/|保存GUI使用的图片文件|
|images/|保存图片文件|
|tl/|保存翻译文件|

gui.rpy所有GUI相关变量都定义在该文件中
options.rpy配置和构筑相关变量，一部分环境设定配置，以及一部分GUI的变量都定义在该文件中
screens.rpy界面都定义在该文件中。创作者可以编辑该文件，实现高级GUI定制化
**script.rpy**该文件用于在剧情脚本，并可以引入其他脚本文件。 创作者也可以根据需要添加删减 `.rpy` 文件。
.rpyc这些文件是 `.rpy` 文件编译后的产物，用于节省加载时间。 如果不删除对应 `.rpy` 文件，仅修改这些文件是没有效果的。

### 发布项目

检查Ren’Py版本更新——检查脚本——**打包**——测试——**发布**

打包 构建发行版——选择合适的分发包——构建 即可
安卓 网络问题，根据报错浏览器手动下载并移动到相应位置

## renpy语法

Ren’Py游戏脚本由 `game/` 目录下众多扩展名为 `.rpy` 的文件组成。Ren’Py会依次检查每一个文件(按照他们路径的Unicode码顺序)，并把文件内容用作脚本。
总之，把一份脚本打散成多个文件，与一份脚本保存在一个大文件中，两种方法是等效的。
为了提高加载速度，Ren’Py启动时会把 `.rpy` 文件编译为 `.rpyc` 文件。
文件名必须以字母或者数字开头，并且开头不能用“00”，因为“00”开头的文件是Ren’Py内部使用的。

### 变量

define语句用于：在初始化阶段给一个全局变量赋值；设定游戏配置项变量
用define语句定义的变量会被当作一个常量，在存档时不会被保存，不应被修改。
*define语句可以放在脚本文件的任何位置，但一般建议放在脚本文件的开头（顶级位置）。*

```renpy
# 定义一个名为Sylvie的角色
define s = Character("Sylvie")

label start:
    s "Hello, world!"
    return
```

default语句用于给一个在游戏初始化时未定义的全局变量赋值。
所有用default定义的变量在存档时都会被自动保存。
*default语句可以放在脚本文件的任何位置，但一般建议放在脚本文件的开头（顶级位置），界面变量除外。*

```renpy
# 定义一个名为Sylvie的角色
define s = Character("Sylvie")
# 定义初始好感度为0
default love = 0

label start:
    s "Hello, world!"
    $ love += 10    # 好感度加10
    return
```

### 脚本标签

Ren'Py中所有的游戏流程代码都会分别写进数个脚本标签中。脚本标签类似于Python中的函数，用于跳转或调用。

**label语句**
我们使用 label 语句来定义一个脚本标签，然后是标签名，后面可紧跟一对小括号以添加参数，若没有参数则括号可以省略。参数的写法、作用域等与Python函数相似。

```renpy
label sample_label(content):

    "[content]"

    return
```

一些标签名有特殊的作用，如控制主控流程。常见的特殊标签名有以下这些：
- start 默认情况下，Ren'Py在游戏启动后会跳转至这个标签。
- quit 若该标签存在，当用户退出游戏时该标签内容会被调用。
- after_load 若该标签存在，当游戏读档后会调用这个标签内容。其可能被用于游戏内容更新后的数据修复。
- splashscreen 若该标签存在，游戏首次运行时，在主菜单出现前，该标签内容会被调用。
- before_main_menu 若该标签存在，在主菜单出现前，该标签内容会被调用。

Ren'Py中共有两种脚本标签：全局脚本标签 与 局部脚本标签。我们一般用的就是全局脚本标签。
全局脚本标签在所有脚本文件中通用，不能重名；而局部脚本标签则可以重名，但是需要关联一个全局脚本标签
在定义局部脚本标签时，我们只需要在标签名前添加一个 `.` 即可，表示这是一个局部脚本标签而非全局脚本标签，它会与上面最近的一个全局脚本标签自动关联。

1. 一个局部脚本标签只能关联一个全局脚本标签，而一个全局脚本标签可以关联多个局部脚本标签。
2. 在一个全局脚本标签中可以直接访问与之关联的局部脚本标签，而想要访问其它全局脚本标签关联的局部脚本标签则需要使用 `global.local` 的形式来访问。
3. 在一个局部脚本标签中可以直接访问与之关联同一个全局脚本标签的另一局部脚本标签，而想要访问其它全局脚本标签关联的局部脚本标签依然需要使用 `global.local` 的形式来访问。

```renpy
label start:

  "这是全局脚本标签start，游戏从这里开始"

  call .local_label
  call global_label.local_label

  return

label .local_label:
  "这是局部脚本标签.local_label，关联start全局脚本标签"
  return

label global_label:
  "这是全局脚本标签global_label"
  call .local_label
  return

label .local_label:
  "这是局部脚本标签.local_label，关联global_label全局脚本标签"
  return
```

**call语句**
`call` 语句用于让主控流程进入某一脚本标签中，并在执行完这次调用后，回到原本调用的位置。
call语句后面接一个标签名，表示让主控流程进入指定的脚本标签中。若指定的脚本标签要传入参数，则在标签名后紧跟一对小括号以传参。传参方式与Python函数传参方式完全相同。

```renpy
label start:

    "游戏开始"

    call sample_label("HelloWorld!")

    "游戏结束"

    return


label sample_label(content):
    "[content]"
    return
```

**jump语句**
jump 语句用于让主控流程进入某一脚本标签中，并顺势执行下去。后面接一个标签名，表示让主控流程进入指定的脚本标签中
jump语句中指定的脚本标签不能传参。但你可以给指定的脚本标签添加默认值参数：

```renpy
label start:
    "游戏开始"

    jump sample_label

    "游戏结束"

    return

# 添加默认参数
label sample_label(content="HelloWorld!"):
    "[content]"
    return
```

**return语句**
`return` 语句标志着一段标签代码块的结束。后面还可接一个返回值，返回值储存在变量 `_return` 中。
Ren'Py特性：在一个脚本标签结束后如果没有添加return语句，且下面还有其它脚本标签，则主控流程将直接进入下面的脚本标签，一直到遇到return语句才结束。若下面所有的脚本标签都没有添加return语句则会一直进入到最后一个脚本标签才结束。
任何脚本标签结束后都应该添加return语句

### 对话

Ren'Py为我们提供了简便快捷的say语句来方便演示对话。

**say语句**一般有以下几种形式：

1. 一个单一字符串，表示显示的内容。一般用作旁白。
2. 由两个字符串组成，前面的字符串表示发言人的名字，后面的表示显示的内容。
3. 表示显示的内容的字符串用三引号引起，方便显示长段文本。
4. 由一个角色对象和一个字符串组成，角色对象控制发言展现的形式，字符串则是显示的内容。这种形式也是最为常用的。

```renpy
label start:

    "我很紧张"

    "我" "我喜欢你！"

    "希尔薇" "这是真的吗？！" with vpunch

    return
```

有些say语句会在原有基础上加上一个 `with` 从句，后跟上一个转场来实现一些演出效果。`vpunch` 是一个内置转场，可以达到让窗口抖动的效果。

我们一般使用 `Character` 函数构建一个角色对象。

Character函数支持很多参数，常用的如下：（以 `who` 为前缀的参数表示人名的样式，以 `what` 为前缀的参数表示文本的样式。）

- **name**
    - 角色的名字。如果该参数是一个字符串，则在对话中显示为角色名；如果为 `None`，则不显示名字，可用于旁白。
- **kind**
    - 新建角色的基底角色类型。通常取值为 `adv` 或 `nvl`。
        - `adv`：文本显示在对话框中。
        - `nvl`：文本显示在屏幕中间。
- **image**
    - 与角色关联的图像标签名，类型为字符串。
- **who_color**
    - 角色名的颜色，通常为一个表示颜色的十六进制数的字符串。
- **what_color**
    - 对话文本的颜色，通常为一个表示颜色的十六进制数的字符串。
- **what_prefix**
    - 在显示对话内容之前添加的前缀字符串。
- **what_suffix**
    - 在显示对话内容之后添加的后缀字符串。
- **who_prefix**
    - 在显示角色名字之前添加的前缀字符串。
- **who_suffix**
    - 在显示角色名字之后添加的后缀字符串。
- **dynamic**
    - 如果为 `True`，则角色名 `name` 应是一个包含 Python 表达式的字符串。该表达式会在每行对话执行前进行计算，计算结果将作为角色名。
- **condition**
    - 如果给定，该参数应是一个包含 Python 表达式的字符串。如果表达式结果为 `False`，则对话不会发生，即 `say` 语句不会执行。
- **ctc**
    - 用于“点击继续”提示的可展现部件。如果使用了其他特殊提示，则可能不会显示。

转义符：

- `\` -> `\\`
- `'` -> `\'`
- `"` -> `\"`
- `%` -> `\%` 或 `%%`
- `{` -> `{{`
- `[` -> `[[`
- `【` -> `【【`

内插字符
Ren'Py支持在文本中插入一个表达式并计算表达式的值，使用一对方括号修饰

```renpy
define s = Character("Sylvie")
default point = 1

label start:
    s "我的名字是[s.name]"
    "当前好感度为[point]"

    return
```

内插字符还支持一些特殊转换标记。
- `!i` 表示在字符串中进行二次插值
- `!u` 会强制把英文文本转换成大写。
- `!l` 会强制把英文文本转换为小写。
- `!c` 会强制把英文文本首字母转换为大写。

文本标签
在Ren'Py中，我们采用文本标签来实现对文本的特殊效果。类似html
文本标签由一对大括号和一个标签名以及相应参数组成，不同的标签名及参数有不同的效果。 `"{tag=arg}text{/tag}"`

`a`

锚点标签的作用就是“传送”，能够引导玩家进入不同的地方。它拥有多个参数，下面来一一介绍：

- jump

当入参为 `jump` 时，会进入其冒号后指定的脚本标签。

```renpy
label start:
    "点{a=jump:dianwo}我{/a}进入"
    return

label dianwo:
    "已进入"
    return
```
- call

当入参为 `call` 时，会调用其冒号后指定的脚本标签。


```renpy
label start:
    "点{a=call:dianwo}我{/a}进入"
    "出来了"
    return

label dianwo:
    "已进入"
    return
```
  
- show

当入参为 `show` 时，会显示其冒号后指定的界面，这里涉及到一个新的概念“界面”，我们不展开讨论。

- URL

当入参部分是一个URL（或者说网站链接）时，会自动启动浏览器打开链接。

```renpy
label start:
    "{a=https://www.bilibili.com/video/BV1uT4y1P7CX/}点我涩涩{/a}"
    return
```

alpha文本标签指定一个透明度，渲染范围为自身及其闭合标签内的文本。透明度是一个介于0.0和1.0之间的数值，分别对应完全透明和完全不透明。

```renpy
label start:

    "{alpha=0.8}总觉得......{/alpha}"
    "{alpha=0.5}要消失了呢......{/alpha}"
    "{alpha=0.3}......{/alpha}"

    return
```

b
  
粗体标签，将自身及其闭合标签内的文本渲染为粗体。

i

斜体标签将自身及其闭合标签之间的文本渲染为斜体。

s

删除线标签在其自身及其闭合标签之间的文本上画一条删除线。

u

下划线标签在其自身及其闭合标签之间的文本添加下划线。

color

颜色文本标签将自身及其闭合标签内的文本渲染为特定的颜色值。颜色值使用 `#rgb` `#rgba` `#rrggbb` `#rrggbbaa` 格式之一。

cps

cps标签用于指定其闭合标签内的文本每秒钟显示的字符数，若带 `*`，则表示当前速度的倍数。

```renpy
label start:
    "{cps=30}时间要开始加速了！{/cps}"
    return
```

font

字体标签将标签自身及其闭合区间之间的文本渲染为指定的字体。入参即使用的字体文件名或路径。

image

图片标签会在文本中内插一个图像。（可以用于插入表情包）

size

字号标签改变了其自己及其闭合标签内的文本字号。若参数为整数则表示文本大小，若为一个 `*` 加一个浮点数的形式则表示为当前文本大小的倍数大小。

fast

fast标签只能用于对话中（即say语句），改标签为自闭和标签，在该标签前面的文本内容会立即显示。

```renpy
label start:
    "你说"
    "什么？！{fast}"
    return
```

nw

nw标签同样只能用于对话中（即say语句），是一个自闭合标签，该标签前的那行文本内容在显示一次后会立刻消失，显示下一句话。

```renpy
label start:
    "什么东西？{nw}"
    "？可恶"
    return
```

若指定参数，则表示等待对应的秒数后再执行文本消失。

```renpy
label start:
    "你好？{nw=2}"
    "怎么不说话呢？"
    return
```

### python

Ren’Py使用Python程序语言编写，并且支持在Ren’Py脚本中包含Python语句。

**python语句**包含一个Python的语句块(block)

```python
python:
    player_health = max(player_health - damage, 0)
    if enemy_vampire:
        enemy_health = min(enemy_health + damage, enemy_max_health)
```

**单行Python语句**
`$ flag = True`

```python
label start:
    $ player_name = renpy.input("请输入你的名字：")
	"我的名字是[player_name]"
```

**init python语句** 本质上是多行Python语句，但在初始化阶段运行。可以用于定义类和函数，或者初始化样式、配置变量、持久化数据。
init python语句支持设定运行优先级，可以在 `init` 和 `python` 之间可以放一个运行优先级数值。如果没有指定优先级，默认使用0。
init python语句按照优先级数值从低到高的顺序运行。优先级相同的情况下，按照文件名的Unicode字符顺序。
为了避免与Ren'Py引擎产生冲突，最好选用 `[-999, 999]` 范围内的数作为优先级。原则上，负整数的优先级主要用在库和配置，普通的init python语句应该使用0或者正整数作为优先级。

```renpy
init python:
	pass
	
init 1 python:
	pass
```

## rpy

```python
label start:

    "希尔维亚" "嗨！今天的课怎么样？"

    "我" "挺好的……"

    "我当然不会承认，上课的时候内容只是左耳进右耳出。"

    "我" "你现在要回家了吗？要不要跟我一起走？"

    "希尔维亚" "当然！"
```

第一行是一个 [label语句](https://doc.renpy.cn/zh-CN/label.html#label-statement)。label语句常用于在程序中给某个脚本点命名。在这个例子中，我们创建了一个名为 `start` 的标签。start标签是特殊的，因为当用户点击主菜单的“开始游戏”时，Ren’Py脚本会从这个标签开始运行。
其他行是 [say语句](https://doc.renpy.cn/zh-CN/dialogue.html#say-statement)。say语句有两种格式。一种格式是，一行单独字符串(双引号开头，双引号结束，中间文字)，用于表现主视角角色的陈述或者内心想法。另一种格式有两个字符串组成。常用于对话，第一个字符串是说话角色名字，第二个字符串是该角色正在说的话。
注意，所有say语句都要用4个空格(半角)缩进.这是因为say语句属于同一个标签语句下的语句块(block)
当文本自身包含双引号时，需要使用反斜杠作为转义符。

### 角色(character)

每当角色说话时，你需要反复输入角色名字。在一个对话为主的游戏中，这可能是很繁重的工作。
Ren’Py允许你在开头就定义角色。这可以使你用一个短名关联一个角色，并且能够改变角色名字显示的颜色。

```python
define s = Character('希尔维亚', color="#c8ffc8")
define m = Character('我', color="#c8c8ff")

label start:

    s "嗨！今天的课怎么样？"

    m "挺好的……"

    "我当然不会承认，上课的时候内容只是左耳进右耳出。"

    s "你现在要回家了吗？要不要跟我一起走？"

    m "当然！"
```

### 图像(image)

Ren’Py会在images目录下搜索图像文件，图像可以被放在images目录的子目录中。
Ren’Py能使用PNG或者WEBP文件作为角色美术资源，JPG、JPEG、PNG或者WEBP文件作为背景美术资源。

```python
define s = Character('希尔维亚', color="#c8ffc8")
define m = Character('我', color="#c8c8ff")

label start:

    scene bg meadow

    "不久之后，我们就抵达了牧场，也是我们俩人出生的地方"

    "我就是在这样的风景环绕之中成长起来的。这里的秋天格外秀美。"

    "童年时，我们经常在牧场里玩耍，所以这里满满充斥着回忆。"

    m "嗨……唔……"

    show sylvie green smile

    "她把脸转向我，上面挂着微笑。她看起来兴致高昂。我觉得自己刚才的紧张情绪已经消散。"

    "我得问问她！"

    m "嗯呣……你是否可以……"

    m "你是否可以做我的视觉小说画师？"

    show sylvie green surprised

    "沉默。"
```

`scene` 语句清除了所有图像并显示了一个背景图像
`show` 语句在背景上显示了一个精灵(sprite)， 并根据预设改变展示的精灵

给定tag标签时，每次只能展示一副图像。当拥有同样tag标签的第二副图像需要展示时，它会直接替换第一副图像。
`bg meadow` tag标签是“bg”，属性是“meadow”。按照习惯，背景图像应该使用的bg作为tag标签
`sylvie green smile` tag标签是“sylvie”，属性是“green”和“smile”

Ren’py将使用除去扩展名后，强制字母变为小写的文件名来作为图象名。（即使图像在子目录中，也只使用文件名定义图像名，忽略目录名）
例如： “bg meadow.jpg” -> `bg meadow`
有时候，制作者可能不想让Ren’Py自动定义图像。这时image语句就能派上用场。它应该出现在文件最顶层(不缩进，在label标签前面)，为图像文件指定对应的图像名称。例如：

```python
image eileen happy = "eileen_happy_blue_dress.png"
```

```python
image a:
	".png"
	zoom = 1.5
```

当某个角色离开但场景不变化时，你才需要使用hide语句。

as

### 转场(transition)

转场切换用于显示在最后一个交互(对话、菜单或来源于其他语句的转场)发生后，到下一个scene、show或hide语句运行之间。

```python
define s = Character('希尔维亚', color="#c8ffc8")
define m = Character('我', color="#c8c8ff")

label start:

    scene bg meadow
    with fade

    "不久之后，我们就抵达了牧场，也是我们俩人出生的地方。"

    "我就是在这样的风景环绕之中成长起来的。这里的秋天格外秀美。"

    "童年时，我们经常在牧场里玩耍，所以这里满满充斥着回忆。"

    m "嗨……唔……"

    show sylvie green smile
    with dissolve

    "她把脸转向我，上面挂着微笑。她看起来兴致高昂。我觉得自己刚才的紧张情绪已经消散。"

    "我得问问她！"

    m "嗯……你是否可以……"

    m "你是否可以做我的视觉小说画师？"
```

当在多个scene、show、hide语句之后有一个转场效果，将对以上所有语句都有效，如：

```python
    scene bg meadow
    show sylvie green smile
    with dissolve
```


|  转场名   |  转场效果   |
| --- | --- |
|   `None`  |   无转场  |
|`dissolve`|溶解|
|`fade`|褪色|

### 位置(position)

图像在展示时默认水平居中，图像底部与界面底部相接。

```python
     show sylvie green smile at right
```

为了重新调整图像位置，需要在show语句中添加一个at分句。at分句指定了图像的展示位置。Ren’Py中包含了多个域定义的位置关键字: `left` 表示界面左端， `right` 表示屏幕右端， `center` 表示水平居中(默认位置)， `truecenter` 表示水平和垂直同时居中。

创作者可以自己定义位置关键字，甚至复杂的位置移动

### 音乐和音效

大多数Ren’Py游戏都会播放背景音乐。音乐播放需要使用play music语句。play music语句将语句中指定的文件名识别为一个音频文件并播放。Ren’Py跟识别音频文件名并在game目录下寻找关联文件。音频文件应该是opus、ogg vorbis或者mp3格式的文件。

    play music "audio/illurock.ogg"

更换音乐时，我们可以使用一个fadeout and fadein分句，fadeout and fadein分句用于旧音乐的淡出和新音乐的淡入。

    play music "audio/illurock.ogg" fadeout 1.0 fadein 1.0

queue music语句表示，在当前音乐播放完毕后播放的音频文件。

    queue music "audio/next_track.opus"

音乐播放可以使用stop music语句停止，这个语句也可选用fadeout分句。

    stop music

音效可以使用play sound语句来播放。与音乐不同，音效不会循环播放。

    play sound "audio/effect.ogg"

在 `game/audio` 目录中的音频文件，如果其文件名去掉文件扩展名后符合Python变量的命名规则(以字母开头且仅包含英文字母、数字或下划线)， 则可以直接不带引号，直接使用文件名播放音频文件。例如，存在一个音频文件game/audio/illurock.ogg

    play music illurock

vioce

### pause语句

pause语句可以让整个Ren’Py进程暂停，直到出现鼠标单击事件。

    pause

如果pause语句中给定一个数字，就只会暂停数字对应的秒数。

    pause 3.0

### 结束游戏

通过运行return语句，你可以结束游戏，而不需要做其他任何事。在此之前，最好设置一些东西能够提示游戏已经结束，并且可能的话给用户一个结局数字或者结局名称。

```python
    ".:. Good 结局。"
	
    return
```

### menu，label和jump语句

menu语句能够给玩家提供一个分支选项:

```python
  
    s "当然，不过，什么是\"视觉小说\"？"

menu:

    "是一种视频游戏。":
        jump game

    "是一种互动小说。":
        jump book

label game:

    m "是一种可以在电脑和主机上玩的视频游戏。"

    jump marry

label book:

    m "就像一种可以在电脑和主机上阅读的互动式图书。"

    jump marry

label marry:

    "那么，我们已经成为视觉小说创作二人组了。"
```

如果label后面相关的语句块(block)之后没有jump语句，Ren’Py会顺序执行后面的语句。最后的jump语句在技术上不是必须的，不过带上一个会让游戏流程显得更清晰。

游戏目录中任意后缀为 .rpy 的文件中都可以定义label。对于Ren’Py来说文件名无关紧要，只有文件里的label才是重点。你可以认为，所有这些rpy文件的合集等价于一个很大的rpy文件，用于跳转和转换控制。
只使用一个script.rpy文件定义所有label结构混乱，最好可以按章节分chapter1.rpy文件
为了便于管理，可以把所有.rpy文件放在一个scripts文件夹下

### 使用default、Python和if语句实现flag(标识)

上面那些语句已经足以用于制作某些游戏，其他一些游戏则需要保存数据及提取数据。例如，制作者需要游戏记下玩家做出的一个选择，先返回主线流程中，并在后面的流程中根据之前的选择出现对应的游戏变动，这是个合理的需求。这就是Ren’Py支持内嵌Python代码的原因。

## GUI(图形用户接口)定制

### 简单GUI定制化

`options.rpy` 文件中有一堆配置项会被GUI使用。

`config.name` 窗口标题和GUI需要显示游戏标题的地方
`gui.show_name`这个配置项应该被设置为False，用于在画面主菜单中隐藏标题名字和版本号。
`config.version`游戏版本号
`gui.about` 在关于(about)界面上的附加文本内容。如果你想要展示多行的credits(制作人员信息)，可以使用 \n\n 换行。

```python
define config.name = _('Old School High School')

define gui.show_name = True

define config.version = "1.0"

define gui.about = _("Created by PyTom.\n\nHigh school backgrounds by Mugenjohncel.")

# gui.about的定义可以使用3个双引号

define gui.about = _("""\
Created by PyTom.

High school backgrounds by Mugenjohncel.""")
```


|路径     |  作用   |
| --- | --- |
|  `gui/main_menu.png`   |   用于主菜单的所有界面背景的图片文件  |
|`gui/game_menu.png`|用于游戏菜单所有界面背景的图片文件|
| `gui/window_icon.png` |窗口图标|

 可以直接修改相应文件
 
 注意，改变gui/window_icon.png后，只对游戏正在运行时的图标有效。
 想要改变Windows平台的“.exe”文件和mac平台的应用程序图标

### 中级GUI定制化

很多修改都可以通过在 `gui.rpy` 文件中编辑配置项实现

修改字号 `define gui.text_size = 22`

gui/textbox.png 文本窗口的背景

define gui.text_color = "#402000"link
该项设置对话文本颜色。

define gui.text_font = "ArchitectsDaughter.ttf"link
该项设置对话文本、菜单、输入和其他游戏内文字的字体。字体文件需要存在于game目录中。

(译者注：“ArchitectsDaughter”字体不支持中文。后续截图中使用的是类似效果的“方正咆哮体”。)

define gui.text_size = 33link
设置对话文本字号。无论增大或缩小字号都需要注意符合文本显示区域的空间限制。

define gui.name_text_size = 45link
设置角色名字的文字字号。

gui/button/choice_idle_background.png

该图片用作，未获取到焦点时，选项按钮的背景。

gui/button/choice_hover_background.png

该图片用作，获取到焦点，选项按钮的背景。

gui/overlay/main_menu.png

主菜单界面的叠加图片。

gui/overlay/game_menu.png

“游戏菜单类”界面，包括读档、存档、preference(环境设定)、关于(about)、help(帮助)等，使用的叠加图片。在“The Question”游戏中，同一个叠加图像用在包括主菜单等各种界面上。

gui/overlay/confirm.png

用在选择确认界面暗化背景的叠加图片。

### 高级定制化

更多高级定制化可以通过定制化 `screens.rpy` 文件实现
