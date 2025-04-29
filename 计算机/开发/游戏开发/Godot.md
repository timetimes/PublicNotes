# Godot

Godot引擎是一款免费、功能齐全、跨平台的游戏引擎。帮助你创作2D和3D游戏。
虽然是游戏引擎，但是用来制作一般软件也是没有问题的（一般使用control节点）。

Godot本身由C++写就。
在场景面板的节点上点击右键并选择“添加脚本”，来创建或附加一个新的脚本到我们的节点上。Godot 提供了四种游戏编程语言：GDScript、C# 以及通过 GDExtension 技术提供的 C 和 C++。还有更多社区支持的语言，但这四个是官方所支持的语言。
GDScript是专为Godot开发的脚本语言，语法和Python高度相似，并提供了诸多方便Godot的语法糖。
C#是游戏引擎常用语言，性能更好。

[Godot下载](https://godotengine.org/download/windows/)
目前同一版本号的Godot又会分为两个版本。图中上方是“标准版”，下方的`.NET`版是提供C#支持的版本。
要使用C#编写脚本必须用.NET版，但是.NET版也支持使用GDScript

[Godot Engine 简体中文文档](https://docs.godotengine.org/zh-cn)

任何游戏引擎都是围绕着构建程序所用的抽象运转的。在 Godot 中，游戏就是一棵由**节点nodes**构成的**树tree**，树又可以结合起来构成**场景scenes**。然后你还可以将这些节点连起来，让它们通过**信号signals**进行通信。

nodes：Godot中一切都是节点
scenes：把一些nodes捆绑在一起重复利用。可以嵌套使用

**资源网站**
[开源素材的整合站](https://godotengine.cn/)：国内的开源素材的整合站，制作游戏时不再因为找可商用素材花费大量时间
[godot工坊](https://godot.pro/#)：国内的 Godot 论坛，包含文档、教程、资源、答疑等板块。
[itch](https://itch.io/)：国外的独立游戏交流平台，有很多资源和工具，还能玩其他作者的游戏。
[kenney](https://www.kenney.nl/)：国外的资源网站，上千免费资源任你使用，大多是 low poly 或像素风。
[Game UI](https://www.gameuidatabase.com/)：国外的游戏 UI 网站，主要用来学习和参考。
[Godot.A.L](https://godotassetlibrary.com/)：一个国外的 Godot 资源网站，看起来比 Godot 自带的资源网站高级一些。
[Godot Market Place](https://godotmarketplace.com/)：国外的 Godot 资源市场，类似上一个，包含付费内容。

## GDScript语法

GDScript 是一门面向对象的指令式编程语言，专为 Godot 构建，是游戏开发者为游戏开发所制作的，目的是节省编写游戏代码的时间。

GDScript 用缩进来做代码块结构，看上去像 Python，然而实际上这两者的原理截然不同。GDScript 的设计灵感是从 Squirrel、Lua、Python 等诸多语言中得到的。

**脚本结构**:

```GDScript
extends Control

# 在节点第一次进入场景树时执行
func _ready():
    pass # 用方法体替换这里

# 每一帧执行一次，'delta' 指上一帧和这一帧的间隔时间
func _process(delta):
    pass
```

以下假设有Python基础，相似的语法简述，重点在于不同的特性或函数：

### 基本语法

井号 `#` 表示注释

#### 变量和数据类型

数据类型：整数（int）、浮点数（float）、布尔（bool）、字符串（String）

在GDScript中，你不需要声明变量的数据类型，它会根据赋值自动推断数据类型
`var` 关键字定义新变量

```GDScript
var name = "Godot"
```

强类型变量：采用类似Python变量注解的形式，不过不能存放其他类型的数据

```GDScript
var name: str = "Godot"
```

推导类型：每次都加上一个冒号和类型会比较麻烦，所以 GDScript 提供了一种语法
这个语法要求变量必须有初始值，毕竟 GDScript 需要根据初始值才能去推导变量的类型

```GDScript
var name:= "Godot"
```

枚举类型：

```GDScript
enum 星期 {
    星期一,
    星期二,
    星期三,
    星期四,
    星期五,
    星期六,
    星期日,
}
```

结合强类型语法 `var 今天: 星期 = 星期.星期一`

常量使用 `const` 关键字定义，语法格式与变量相同。由于常量不允许被修改，所以在定义时必须给它一个值。

字符串切片
可以使用original_string.substr(0, original_string.length() - 1)删除最后一个字符

#### 语句

match语句不需要case：

```GDScript
match x:
    1:
        pass
    _:
		pass
```

#### 函数

使用func定义函数

#### 类

`extends` 关键字定义了这个脚本所继承或扩展的类
GDScript 仅支持单继承，就是说子类只能继承自一个父类

`[class_name <abc>] extends <bcd>`

### 生命周期

节点的生命周期是指节点从出生（创建）到死亡（删除）的过程，这个过程中有几个关键的时间点，我们可以在这些时间点编写我们的逻辑代码，承载这些代码的方法就被称为生命周期方法。

`_enter_tree`在节点进入到场景树时执行，也就是节点出现时执行。
**`_ready`** 当节点完全准备好时执行。
`_exit_tree `当节点离开场景树时执行，且子节点优先执行。

（`_enter_tree` 会最先执行，且父节点优先执行，而 `_ready` 最后执行，且父节点排在最后。）

**`_process`** 每个画面帧时执行。这个方法需要有个参数，Godot 默认参数名是 `delta`，它表示当前帧和上一帧之间间隔的时长，单位是秒
`_physics_process` 类似画面帧，游戏中进行物理效果模拟时也是一帧一帧进行的，不过这个帧不等于画面帧，Godot 默认是每秒 60 物理帧，同样他也有个 delta 参数，表示上一个物理帧与当前物理帧之间的间隔时长。

（ `delta` 参数，使用这个方法可以平衡不同帧率对游戏的影响， 例如`position.x += 60 * delta`）

### 获取输入

大部分游戏都支持多种输入方式,使用 or 运算同时判断多个按键输入，但这必定会很麻烦
打开引擎主界面菜单中的`项目` -> `项目设置` -> `输入映射` 选项卡，，我们可以在这里添加按键映射

在代码中，我们可以使用 `Input.is_action_pressed("动作名称")` 来获取某个动作对应的按键是否被按下

线性输入：游戏手柄上有一些可以“输入一半”的键，比如摇杆和扳机，这时候就可以使用 `Input.get_action_strength("动作名称")` 来获取一个小数数值，范围是 0 ~ 1，表示按键移动的强度。

成对输入：有时候我们会需要成对的输入，例如操控船只的加速和减速，我们可以使用 `Input.get_axis("反方向动作","正方向动作")` 来获取一个 -1 ~ 1 的值
或者有些两个轴的输入，例如玩家的上下左右移动，可以使用 Input.get_vector("-x动作","+x动作","-y动作","+y动作") 来获取到一个 Vector2 类型的值，其中的 x 和 y 的范围是 -1 ~ 1。

鼠标的按键输入可以直接使用输入映射功能。如果要获取鼠标的位置，则可以使用 `get_global_mouse_position()` 获取鼠标在 2D 世界中的坐标。如果要获取鼠标的移动速度，则需要使用 `_input` 生命周期方法：
```GDScript
func _input(event):
    if is_instance_of(event,InputEventMouseMotion):
        print(event.velocity)
```

### 节点操作

**获取节点**：`$节点路径`。其实有一个和它功能相同的方法，叫做 `get_node`，不过 `$` 符号用起来更方便。
某些节点需要在其他位置反复通过 `$"XXX"` 语法访问，这时候 $ 符号后面长长的路径就会成为累赘。
如果这个节点的名称在场景中是唯一的，那么就可以右键节点勾选上 唯一名称
此时即可在代码中通过 `%"节点的唯一名称"` 语法来获取这个节点
在引擎中直接把节点拖到代码界面会自动得到$节点路径

**添加节点**：`$ABC.add_child(新节点)` 给 ABC 节点添加子节点

**删除节点**：删除节点有两个方法：`free` 和 `queue_free`。
建议使用 `queue_free` 来删除节点，方法名中的 queue 是队列的意思，可以理解成排队，也就是说这是让节点排队删除，而不是立刻删除。
而 `free` 则是立刻删除节点，在调用 `free` 时，Godot 就会立刻删除这个节点，容易造成报错。

### 信号

**连接信号**：在 Godot 引擎界面中可以双击信号来连接到某个脚本上的方法

断开连接：调用信号的 disconnect 方法就可以断开某个与方法的连接

在脚本中使用 `signal` 关键字定义信号
`signal <信号名>([参数列表])`

定义的信号需要手动触发，使用 `emit` 方法
`<信号名>.emit()`

信号可以向外界反应自身的状态，但这不是节点之间的唯一通信途径，别忘了我们可以直接使用 `<节点变量>.属性或方法` 这种形式修改其他节点的属性或是调用其他节点的方法。

### 组

Godot 中的组，作用是给节点打标签。
选中一个节点后，在屏幕右边的节点选项卡的分组页面中即可给节点分配组

可以使用节点对象的 `is_in_group` 方法判断节点是否属于某个组

虽然应该不常用，但如果你想要使用代码操纵节点的组，可以使用 `add_to_group` 方法把节点添加到一个组中，或使用 `remove_from_group` 从组中移除节点

### 注解

在 Godot 4 中，注解（Annotations）被引入为一种为代码添加元数据的方法，它们可以影响代码如何被引擎处理。

1. `@export`： 使一个变量变得可以在编辑器中编辑。你可以为它指定一个类型，以更改编辑器中的显示方式。  
    `@export var health: int = 100`
2. `@onready`： 延迟初始化一个变量，直到节点被添加到场景树中。  
    `@onready var player = get_node("Player")`
3. `@tool`：使脚本在编辑器模式下运行，而不仅仅是游戏运行时。  
    `@tool`
    `extends Node`
4. `@icon`：为脚本设置一个图标

## 引擎

在Script界面鼠标悬停在类和方法上可以显示帮助文档，ctrl点击类和方法可以直接打开文档方便查看

### 项目设置

“项目——项目设置” 中有一些常用的功能：

**常规选项卡**
修改窗口大小：显示——窗口——大小 ——视口宽度/高度
更改图标：应用 —— 配置 —— 图标
取消/修改启动画面：应用 —— 启动画面
定义层名称：层名称（开发周期长时，以免在设置层的时候忘记层的分类）
更改Windows图标：搜索windows原生图标 或者 打开高级设置后，应用 —— 配置 ——windows原生图标
定义鼠标光标：显示——鼠标光标

**输入映射选项卡**
在这里添加新动作，并给动作添加一个或更多事件（键盘、鼠标、手柄）
*添加事件时会自动监听，方便找到需要的事件*

全局选项卡

### 常用节点

2D场景：2D游戏的根节点
3D场景：3D游戏的根节点

label：文本节点
前往视口右侧的“检查器”面板。点击 Text 属性下方的字段，然后键入“Hello World”。

在编辑器中连接信号
我们希望将按钮的“pressed”信号连接到我们的 Sprite2D，并且我们想要调用一个新函数来打开和关闭其运动
将一个脚本附加到 Sprite2D 节点
你可以在“节点”面板中连接信号。选择 Button 节点，然后在编辑器的右侧，单击检查器旁边名为“节点”的选项卡。停靠栏显示所选节点上可用的信号列表。双击“pressed”信号，打开节点连接窗口。

HTTPRequest
HTTP 请求可以用来与 Web 服务器以及其他非 Godot 程序通信。
与 Godot 的其他网络功能（例如高阶多人游戏）相比，HTTP 请求的额外开销更大，起步也更慢，所以并不适合实时通信，也不善于进行多人游戏中常见的大量较小更新的发送。
然而，HTTP 提供了与外部 Web 资源的互操作性，并且非常适合发送和接收大量数据，例如传输游戏资产等文件。

### 自动加载

打开菜单栏中【项目】【项目设置】界面，点击其中的【自动加载】选项卡
在最上面的路径中填写需要被加载的 PackedScene 路径或点击后面的文件夹按钮来选择一个 PackedScene 后，再给它起个名字即可点击最后的添加按钮
同时注意自动加载列表中有一个全局变量按钮，当勾选了这个东西时即可在代码中的任意位置通过前面的名称使用这个节点或脚本的实例

### 导出游戏

如果使用c#

第一次导出游戏时，需要设置导出模板：（steam等数字平台已经安装，不需要）
快速设置中修改为联网模式；编辑器——管理导出模板——下载
可以复制镜像url在通过代理加速下载文件，然后编辑器——管理导出模板——从文件安装

项目——导出——添加 选择导出平台
windows 启用内嵌PCK 游戏会导出一个单独的文件

编辑器——编辑器设置——导出
windows——rcedit 选择下载好的rcedit

## 教程案例

### 官方案例

[godot-demo-projects](https://github.com/godotengine/godot-demo-projects/tree/master)

#### Dodge the Creeps

[dodge_the_creeps](https://github.com/godotengine/godot-demo-projects/tree/master/2d/dodge_the_creeps)

下载 [dodge_the_creeps_2d_assets.zip](https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/dodge_the_creeps_2d_assets.zip)。请解压归档文件，将 `art/` 和 `fonts/` 目录移动到你的项目目录。

这个游戏是针对竖屏模式设计的，所以我们需要调整游戏窗口的大小。点击_项目 -> 项目设置_打开项目设置窗口，然后在左栏中打开_显示 -> 窗口_选项卡，将“视口宽度”设置为 `480`，并将“视口高度”设置为 `720`。
另外，滚动到该小节的底部，在拉伸选项中，将模式设置为 `canvas_items`，将比例设置为 `keep`。这样就可以保证在不同大小的屏幕上，游戏都能够进行一致的比例缩放。

在这个项目中，我们将制作 3 个独立的场景：`Player`、`Mob` 以及 `HUD`，我们将把这些场景合并成游戏的 `Main` 场景。

**Player玩家场景**：（在文件系统窗口右键新建场景）
选择 Area2D 玩家对象根节点。一般而言，场景的根节点应该反映对象所需的功能
通过双击节点名称将其名称更改为 `Player`
在将任何子节点添加到 `Player` 节点之前，我们要确保不会通过点击它们来意外移动它们或调整它们的大小。选择该节点并单击锁右侧的图标（编组所选节点）。

右击 `Player` 节点选择添加一个子节点 AnimatedSprite2D。`AnimatedSprite2D` 将处理我们的玩家的外观和动画。
在检查器中找到 `Sprite Frames` 属性，在 `Animation` 选项卡下，点击 "[空]" -> "新建 SpriteFrames"。
点击您刚刚创建的 `SpriteFrames` 以打开“精灵帧”面板：
在左侧是一个动画列表。点击“默认”选项，将其重命名为“walk”。然后点击“添加动画”按钮创建第二个名为“up”的动画。在“文件系统”选项卡中找到玩家图像 - 它们位于您之前解压的 `art` 文件夹中。将每个动画的两个图像（命名为 `playerGrey_walk[1/2]` 和 `playerGrey_walk[2/2]` ）拖放到对应动画的“动画帧”面板侧。可以点击播放测试并修改FPS调整动画速度。
玩家图像对于游戏窗口来说有点过大，需要缩小它们。点击 `AnimatedSprite2D` 节点，可以在检查器 `Node2D` 标签中，将 `Scale` 属性设置为 `(0.5, 0.5)`。

最后，在 Player 下添加一个 CollisionShape2D 作为子节点，以确定玩家的“攻击框”，或者说碰撞范围。
在检查器中“Shape”的旁边点击“[空]”->“新建 CapsuleShape2D”添加形状，使用两个控制柄，调整形状大小以覆盖精灵

**Player场景脚本**：（右键Player，添加脚本）
添加玩家的动作、动画，并将其设置为检测碰撞

变量 `speed` 上使用 `export` 关键字，这样我们就可以在“检查器”中设置其值。对于希望能够像节点的内置属性一样进行调整的值，这可能很方便。

当节点进入场景树时，`_ready()` 函数被调用

可以使用 `_process()` 函数定义玩家将执行的操作。`_process()` 在每一帧都被调用
点击项目 -> 项目设置打开项目设置窗口，然后单击顶部的输入映射选项卡。在顶部栏中键入“move_right”，然后单击“添加”按钮以添加该 `move_right` 动作。
我们需要为这个操作分配一个按键。单击右侧的“+”图标，打开事件管理器窗口。
会自动选中“监听输入...”区域。按下键盘上的“右方向”键
选择“确定”按钮。现在“右方向”键与 `move_right` 动作关联了
重复这些步骤以再添加三个映射：`move_left` 映射到左箭头键 ；`move_up` 映射到向上箭头键；`move_down` 映射到向下箭头键。
使用 `Input.is_action_pressed()` 来检测是否按下了某个键
使用 `clamp()` 来防止它离开屏幕
`$` 是 `get_node()` 的简写

现在玩家可以移动了，我们需要根据方向更改 AnimatedSprite2D 所播放的动画。我们的“walk”动画显示的是玩家向右走。向左移动时就应该使用 `flip_h` 属性将这个动画进行水平翻转。我们还有向上的“up”动画，向下移动时就应该使用 `flip_v` 将其进行垂直翻转。
在游戏开始时隐藏玩家

我们希望 `Player` 能够检测到何时被敌人击中，但是我们还没有任何敌人！没关系，因为我们将使用Godot的 信号_功能来使其正常工作。
在脚本顶部添加以下内容。如果你使用的是 GDScript，请将其添加到 `extends Area2D` 之后。
选中 `Player` 节点，然后点击“检查器”选项卡旁边的“节点”选项卡，就可以查看玩家可以发出的信号列表
请注意自定义的“hit”信号也在其中！由于敌人将是 `RigidBody2D` 节点，所以需要 `body_entered(body: Node2D)` 信号。当物体接触到玩家时就会发出这个信号。点击“连接...”就会出现“连接信号”窗口。

最后再为玩家添加一个函数，用于在开始新游戏时调用来重置玩家。

**Mob怪物场景**：
添加根节点：RigidBody2D
添加子节点：AnimatedSprite2D、CollisionShape2D、VisibleOnScreenNotifier2D
设置编组所选节点，使其无法被选中

选择 Mob 节点，并在检查器的 RigidBody2D 部分中把它的 Gravity Scale 属性设置为 0。这样可以防止怪物向下坠落。
在 RigidBody2D 部分下方的 CollisionObject2D 部分下，展开 Collision 分组并取消选中 Mask 属性里的 1。这将确保怪物们不会相互碰撞。

设置 AnimatedSprite2D的 3 个动画：fly、swim、walk
为每个单独动画设置 动画速度 属性，将三个动画的对应动画速度值都调整为 3
可以使用 动画速度 输入区域右侧的“播放动画”按钮预览动画
这些小怪的图像也要缩小。请将 `AnimatedSprite2D` 的 `Scale` 属性设为 `(0.75, 0.75)`

为碰撞添加一个 `CapsuleShape2D`。为了使形状与图像对齐，你需要将 `Rotation` 属性设为 `90`（在“检查器”的“Transform”下）

将 `VisibleOnScreenNotifier2D` 节点完全包裹敌人

**Mob场景脚本**：
在 `_ready()` 中，我们从三个动画类型中随机选择一个播放

最后一步是让怪物在超出屏幕时删除自己。将 `VisibleOnScreenNotifier2D` 节点的 `screen_exited()` 信号连接到 `Mob` 上

**Main游戏主场景**：
创建新场景并添加一个 Node 节点，命名为 Main。（我们之所以使用 Node 而不是 Node2D，是因为这个节点会作为处理游戏逻辑的容器使用。本身是不需要 2D 功能的。）

点击实例化按钮（由链条图标表示）并选择保存的 `player.tscn`，或者直接把 `player.tscn`文件拖入Main场景中

添加 `Main` 的子节点：
Timer（改名为 MobTimer）——控制怪物产生的频率
Timer（改名为 ScoreTimer）——每秒增加分数
Timer（改名为 StartTimer）——在开始之前给出延迟
Marker2D（改名为 StartPosition）——表示玩家的起始位置
设置每个 Timer 节点的 Wait Time 属性（值以秒为单位）：
MobTimer：0.5；ScoreTimer：1；StartTimer：2
此外，将 StartTimer 的 One Shot 属性设置为“启用”，并将 StartPosition 节点的 Position 设置为 (240, 450)。

`Main` 节点将产生新的生物，我们希望它们出现在屏幕边缘的随机位置。 
添加一个 `Main` 的子节点Path2D并改名为 MobPath
当你选择 `Path2D` 时，你将在编辑器顶部看到一些新按钮
选择添加顶点按钮，并单击以添加拐角点来绘制路径。可使用网格捕捉和用智能捕捉，使点对齐到网格。（以顺时针的顺序绘制路径，否则小怪会向外而非向内生成！）
在图像上放置点 4 后，点击 `闭合曲线` 按钮

现在已经定义了路径，添加一个 PathFollow2D 节点作为 `MobPath` 的子节点，并将其命名为 `MobSpawnLocation`。 该节点在移动时，将自动旋转并沿着该路径，因此我们可以使用它沿路径来选择随机位置和方向。

**Main 脚本**：
在脚本的顶部，我们使用 `@export var mob_scene: PackedScene` 来允许我们选择要实例化的 Mob 场景。

单击 `Main` 节点，就可以在“检查器”的“Script Variables”（脚本变量）下看到 `Mob Scene` 属性
将 `mob.tscn` 从“文件系统”面板拖放到 Mob Scene 属性里

然后选中“场景”面板中 `Main` 节点下的 `Player` 场景实例，切换到侧边栏的“节点”面板。请确保“节点”面板中的“信号”选项卡处于选中状态。
你可以看到 `Player` 的信号列表。找到 `hit` 信号并双击（或右键选择 "Connect..."）将会打开信号连接窗口。接下来创建用于在游戏结束时进行一些处理的 `game_over` 函数。在信号连接窗口底部的 “Receiver Method” 框中输入 “game_over”，并点击 “Connect”。

将每个 Timer 节点（`StartTimer`、`ScoreTimer` 和 `MobTimer`）的 `timeout()` 信号连接到主脚本。`StartTimer` 将启动其他两个计时器。`ScoreTimer` 将使得分加 1。

将对 `new_game` 的调用添加至 `_ready()`
指定 `Main` 作为我们的“主场景”（文件系统右键设置主场景）——游戏启动时自动运行的场景。
当你确定一切正常时，在 `_ready()` 中删除对 `new_game()` 的调用，使用 `pass` 替代它。

**HUD游戏信息显示场景**：
创建新场景，添加一个 CanvasLayer 节点并命名为 HUD
CanvasLayer 节点可以让我们在游戏的其他部分的上一层绘制 UI 元素，这样它所显示的信息就不会被任何游戏元素（如玩家或敌人）所覆盖。

HUD 中需要显示以下信息：
得分，由 ScoreTimer 更改。
消息，例如“Game Over”或“Get Ready!”
“Start”按钮来开始游戏。
UI 元素的基本节点是 Control。要创建 UI，我们需使用 Control 下的两种节点：Label 和 Button
创建 `HUD` 的子节点：名为分数标签 ScoreLabel 的 Label；名为消息 Message 的 Label；名为开始按钮 StartButton 的 Button；名为信息计数器 MessageTimer 的 Timer

点击 `ScoreLabel` 并在“检查器”的 `Text` 字段中键入一个数字。`Control` 节点的默认字体很小，不能很好地缩放。游戏资产包中有一个叫作“Xolonium-Regular.ttf”的字体文件。 使用此字体需要执行以下操作：
在“Theme Overrides > Fonts”（主题覆盖 > 字体）中选择“加载”，然后选中“Xolonium-Regular.ttf”文件。
字体尺寸仍然太小，请在“Theme Overrides > Font Sizes”（主题覆盖 > 字体大小）下将其增加到 `64`。当 `ScoreLabel` 完成此操作后，请重复对 `Message` 和 `StartButton` 节点做同样的修改。
拖动节点可以手动放置节点排列，也可以使用“锚点预设（Anchor Preset）”进行更精确的定位

ScoreLabel
添加文本 0。
将“Horizontal Alignment”和“Vertical Alignment”设置为 Center。
为“Anchor Preset”选择 Center Top。（可以搜索属性名）
Message
添加文本 Dodge the Creeps!。
将“Horizontal Alignment”和“Vertical Alignment”设置为 Center。
将“Autowrap Mode”设置为 Word，否则标签只会有一行。
在“Control - Layout/Transform”中将“Size X”设置为 480，使用屏幕的完整宽度。
为“Anchor Preset”选择 Center。
StartButton
添加文本 Start。
在“Control - Layout/Transform”中将“Size X”设置为 200、“Size Y”设置为 100，在边框和文本之间添加间距。
为“Anchor Preset”选择 Center Bottom。
在“Control - Layout/Transform”中将“Position Y”设置为 580。
在 MessageTimer 中，将 Wait Time 设置为 2 并将 One Shot 属性设置为“启用”

将 `StartButton` 的 `pressed()` 信号与 `MessageTimer` 的 `timeout()` 信号连接到 `HUD` 节点上

在 `Main` 场景中实例化 `HUD` 场景

现在我们需要将 `HUD` 功能与我们的 `Main` 脚本连接起来。这需要在 `Main` 场景中添加一些内容：
在“节点”选项卡中，点击“连接信号”窗口中的“选取”按钮，选择 `new_game()` 方法或在窗口的“接收方法”下面输入“new_game”，将 HUD 的 `start_game` 信号连接到 Main 节点的 `new_game()` 函数。请确认脚本中 `func new_game()` 的旁边出现了一个绿色的连接图标。

在 `Mob` 场景中，选择根节点，点击旁边的“节点”标签（与节点信号相同的位置），在“信号”旁边点击“分组”以打开分组概览，以及“+”按钮以打开“创建新分组”对话框。
将组命名为 `mobs` 并点击“确定”以添加新的场景组。现在所有怪物都将位于“怪物”组中。

**背景、音乐、键盘控制**：
默认的灰色背景不是很吸引人，那么我们就来改一下颜色。一种方法是使用 ColorRect节点。将其设为 `Main` 下的第一个节点，这样这个节点就会绘制在其他节点之后。`ColorRect` 只有一个属性：`Color`（颜色）。选择一个你喜欢的颜色，然后在视口顶部的工具栏或者检查器中选择“布局”->“锚点预设”->“整个矩形”（Layout -> Anchors Preset -> Full Rect），使其覆盖屏幕。
如果你有背景图片，你也可以通过使用 TextureRect 节点来添加

添加两个 AudioStreamPlayer节点作为 `Main` 的子节点。将其中一个命名为 `Music`，将另一个命名为 `DeathSound`。 在每个节点选项上，点击 `Stream` 属性，选择 `加载`，然后选择相应的音频文件；或者直接把音频文件拖到`Stream` 属性位置。
自动导入音频时 `Loop` 设置是禁用的。如果希望音乐无缝循环，请单击流文件的下拉箭头，选择 `唯一化`，然后再单击流文件并选中 `Loop` 框。
要播放音乐，请在 `new_game()` 函数中添加 `$Music.play()`，在 `game_over()` 函数中添加 `$Music.stop()`。最后，在 `game_over()` 函数中添加 `$DeathSound.play()`。

当游戏使用键盘控制，可以方便地按键盘上的键来启动游戏。一种方法是使用 `Button` 节点的 “Shortcut”（快捷键）属性。
选择“项目 -> 项目设置”，然后单击“输入映射”选项卡。与创建移动输入动作的方式相同，创建一个名为 `start_game` 的新输入操作，并为 Enter 添加按键映射。
在 HUD 场景中，选择 StartButton 并在检查器中找到它的 Shortcut（快捷方式）属性。通过在框中单击来创建一个新的 快捷键 资源，打开 Events（事件） 数组并通过单击 Array[InputEvent] (size 0) 向其添加一个新的数组元素。
创建一个新的 InputEventAction并将其命名为 `start_game`
这样，开始按钮出现后，你就可以点击它或按 Enter 来启动游戏

#### Squash the Creep

[Squash the Creep](https://github.com/godotengine/godot-3d-dodge-the-creeps)

下载 [squash_the_creeps_start_1.1.0.zip](https://github.com/godotengine/godot-3d-dodge-the-creeps/releases/download/1.1.0/squash_the_creeps_start_1.1.0.zip)

打开 Godot 项目管理器，然后点击导入按钮。打开文件浏览器并点击该文件夹所包含的 `project.godot` 文件

起始项目中包含一个图标和两个文件夹：`art/` 和 `fonts/`。你可以在里面找到游戏中我们会用到的艺术资产和音乐。
art/里面有两个 3D 模型，`player.glb` 和 `mob.glb`，一些模型使用的材质，以及一首音乐。

**Main主场景**：main.tscn
以普通的 Node 作为其根创建主场景，命名为 `Main`

添加一个地板，以防止角色掉落。 
添加`Main`的子节点StaticBody3D ，重命名为 `Ground`；添加`Ground`的子节点 CollisionShape3D
选中 CollisionShape3D，转到检查器，然后单击 Shape（形状）属性旁边的 <空> 字段。创建一个新的 BoxShape3D。
视口中会显示盒子的线框和三个橙色的小点。你可以点击并拖动这些点来进行交互，编辑形状的范围。我们也可以在检查器中精确设置尺寸。点击 BoxShape3D 展开资源，将 Size 设置为 X 轴 60，Y 轴 2 和 Z 轴 60。
碰撞形状是不可见的。我们需要添加一个与之配套的视觉层。选择 Ground 节点并添加一个 MeshInstance3D 作为其子节点。
在检查器中，点击 Mesh 旁边的字段，创建一个 BoxMesh 资源，创建一个可见的立方体
再次设置大小，点击立方体图标展开资源，并将其 Size 设置为 60、2、60。由于立方体资源使用的是大小（size）而不是范围（extents），我们需要使用这些值，以便它与我们的碰撞形状相匹配。
`Ground` 的 transform.position.y 应当是 -1

现在来添加一个平行光，让我们的整个场景不全都是灰色的。选择 Main 节点，然后添加一个子节点 DirectionalLight3D。
移动并旋转 DirectionalLight3D 节点。通过单击并拖动操作器的绿色箭头将该节点往上移动，然后单击并拖动红色弧线以围绕 X 轴旋转它，直到地面被照亮。
在检查器中，勾选复选框打开Shadow -> Enabled

**Player 场景**：
创建一个 CharacterBody3D 节点来当根节点，命名为 `Player`

为角色的 3D 模型创建一个基本的装备。稍后我们将在播放动画时通过代码旋转模型。
新建一个 Node3D节点作为 `Player` 的子节点，并将其命名为 `Pivot`
然后在文件系统面板中，双击展开 `art/` 文件夹，将 `player.glb` 拖放到 `Pivot` 节点上
这样应该就会把这个模型实例化为 `Pivot` 的子项。你可以将其重命名为 `Character`

我们的角色需要一个碰撞形状才能与环境相碰撞。再次选中 Player 节点并添加 CollisionShape3D 子节点。在检查器中，为 Shape 属性新建一个 SphereShape3D。
拖动视口中的橙色点，将其缩小一点。我的球体半径约为 `0.8` 米。然后，向上移动碰撞体，使其底部与网格平面大致对齐。
为了使形状移动更容易，你可以通过点击 `Character` 或 `Pivot` 节点旁边的眼睛图标来切换模型的可见性

在输入映射中创建五个动作`move_left`、`move_right`、`move_forward`、`move_back`、`jump`（向左移动、向右移动、向前移动、向后移动、跳跃）

**Player脚本**：在弹出窗口中，先将模板设置为 空

回到**Main场景**：
在`Main` 场景中实例化 `Player`场景

添加摄像机
新建一个Main的子节点 Marker3D，命名为 CameraPivot
选中 CameraPivot，然后为其添加一个 Camera3D 子节点。
在选中 Camera 时，左上角会出现一个预览复选框。你可以单击预览游戏中的摄像机投影视角
在视口上方的工具栏中，单击视图，然后单击2 个视口。
在底视图上，选择你的 Camera3D 并通过点击勾选框打开相机预览
在顶视图中，确保选择了你的 Camera3D，然后将相机在 Z 轴上移动约 19 个单位（拖动蓝色箭头）
选中 CameraPivot 并将其围绕 X 周旋转 -45 度（使用红色的圆圈）。
可以点击右上角运行该场景（或按F6），然后按方向键来移动角色。
因为透视投影的缘故，我们会在角色的周围看到一些空白区域。在这个游戏中，我们要使用的是正交投影，从而更好地展示游戏区域，让玩家更易于识别距离。
再次选中 Camera，然后在检查器 中将 Projection（投影）设为 Orthogonal（正交）、将 Size（大小）设为 19。角色现在看起来应该更加扁平，背景应该被地面充满。

**Mob场景**：
用 CharacterBody3D 节点作为根节点来创建场景。命名为 Mob。添加一个 Node3D 节点作为其子项，将其命名为 Pivot。将 mob.glb 文件从文件系统面板拖放到 Pivot 上，这样就把怪物的 3D 模型添加到了场景之中。可以将新创建的 `mob` 节点重命名成 `Character`

我们的实体需要一个碰撞形状才能工作。右键点击场景的根节点 Mob，然后点击添加子节点CollisionShape3D。在检查器中为 Shape（形状）属性分配一个 BoxShape3D。
调整一下它的大小，来更好地框住 3D 模型。可以单击并拖动橙色的小点来进行。
碰撞盒应该接触地面，并且比模型稍微瘦一点点。即便玩家的球体只接触了这个碰撞盒的角落，物理引擎也会判定发生了碰撞。如果盒子比 3D 模型要大一点，你可能距离怪物还有一定的距离就死了，玩家就会觉得不公平。

怪物离开屏幕之后，我们就不再需要它了，所以我们可以把它删除。Godot 有一个可以检测对象离开屏幕的节点，VisibleOnScreenNotifier3D ，我们就要用它来销毁我们的小怪。
选中 Mob 节点，并为其添加一个 VisibleOnScreenNotifier3D 作为子项。这回出现的就是一个粉色的框。这个框完全离开屏幕后，该节点就会发出信号。使用橙色的点来调整大小，让它覆盖住整个 3D 模型。

**Mob 脚本**：
将 VisibleOnScreenNotifier3D 节点的 screen_exited 信号连接到 Mob 上

再次回到**Main场景**：
修改游戏的分辨率：游戏默认的窗口大小是 `1152x648`。我们要把它设成 `720x540`
项目 -> 项目设置 找到 Display -> Window（显示 -> 窗口）。在右侧将 Width（宽度）设为 720、Height（高度）设为 540

创建怪物生成路径：
与 2D 游戏教程中所做的一样，你要设计一条路径，使用 PathFollow3D 节点在路径上随机取位置。不过在 3D 中，路径绘制起来会有一点复杂。我们希望它是围绕着游戏视图的，这样怪物就会在屏幕外出现。但绘制的路径也同样不会在摄像机预览中出现。
我们可以用一些占位网格来确定视图的界限。你的视口应该还是分成两个部分的，底部是相机预览。选中 Camera3D 节点，然后点击底部视口的预览复选框。
让我们来添加一些占位网格。为 Main 节点新建一个 Node3D 节点作为子项，命名为 Cylinders。我们会用它将圆柱体进行分组。添加一个 MeshInstance3D 节点作为其子项
在检查器中，为 Mesh（网格）属性赋值 CylinderMesh（圆柱体网格）。
使用视口左上角的菜单（三个点处，原本是透视模式），将上面的视口设为正交顶视图。或者你也可以按小键盘的 7。
地面栅格可能有一点分散注意力。你可以在工具栏的视图菜单中点击查看栅格进行开关
你现在要沿着地平面移动圆柱体，看底部视口的相机预览。我推荐使用网格捕捉来做这件事。你可以通过点击工具栏上的磁铁图标或按 Y 键来切换。
将圆柱体移到相机视图的左上角，使其正好在视野之外。
我们将创建网格的副本，并将它们放置在游戏区域周围。按 Ctrl + D（来复制节点。你也可以在场景面板中右击节点，选择制作副本。沿着蓝色 Z 轴向下移动副本，直到它正好在摄像机的预览范围之外。
按住 Shift 键选择两个圆柱体，并点击未选择的那个圆柱体，然后复制它们。拖拽红色的 X 轴，将它们移动到右侧。
白色的有点难以看清，让我们给它们一个全新的材质，让它们凸显出来。我们可以同时更新所有四个圆柱体。在场景面板中选中所有网格实例。要实现全选，可以先点击第一个，然后按住 Shift 点击最后一个。
在检查器中，展开 Material（材质）部分，为 0 号插槽分配一个 StandardMaterial3D。点击球体图标来打开材质资源。展开 Albedo（反照率）部分将颜色设为与背景色存在对比的颜色，比如亮橙色。
添加一个 Path3D 节点作为 Main 的子节点。在工具栏中会出现四个图标。点击添加点工具，即带有绿色“+”号的图标。
单击每个圆柱体的中心以创建一个点。然后，单击工具栏中的闭合曲线图标以关闭路径。如果有任何一点偏离，你可以单击并拖动它以重新定位它。
要对它的随机位置进行采样，我们需要一个 PathFollow3D 节点。添加 PathFollow3D 作为 Path3D 的子项。将两个节点分别重命名为 SpawnLocation 和 SpawnPath。 

**Main脚本**：
右键点击 `Main` 节点，为它附加一个新脚本
选中 Main 节点。将 mob.tscn 从文件系统面板拖到检查器的 Mob Scene 槽中。

为 Main 新建一个 Timer 节点作为子节点。将其命名为 MobTimer
在检查器中，将其 Wait Time（等待时间）设为 0.5 秒，然后打开 Autostart（自动开始）
MobTimer，在右侧的节点面板中双击 timeout 信号，将它连接到 Main 节点。

**跳跃与踩扁怪物**：
物理实体可以访问两个互补的属性：层和遮罩。层（Layer）定义的是该对象位于哪些物理层上。
遮罩（Mask）控制的是该实体会监听并检测的层，会影响碰撞检测。希望两个实体能够发生交互时，你需要让其中至少一个的遮罩与另一个（的层）相对应。
让我们来为物理层命名。打开项目 -> 项目设置。
在左侧的菜单中找到层名称 -> 3D 物理。你可以在右侧看到层的列表，每一层右侧都有一个字段，可以用来设置名称。将前三层分别命名为 player、enemies、world（玩家、敌人、世界）。
在 Main 场景中选中 Ground 节点。在检查器中展开 Collision（碰撞）部分。你可以看到，该节点的层和遮罩在这里以按钮网格的形式排列。
地面是世界的一部分，所以我们希望它属于第三层。点击 Layer 中的第一个点亮的按钮将其关闭，打开第三层（点击右侧三个点可以查看设置的层名）。然后点击关闭 Mask。Mask 属性可以让节点监听与其他物理对象的交互，但它不是实现碰撞所必须的。Ground 不需要监听任何东西；它存在的意义是防止生物下落。
选中 Player 节点，将其 Collision -> Mask 设为“enemies”和“world”。Layer 属性可以保持默认，因为第一个层就是“player”层。
选中 Mob 节点。将其 Collision -> Layer 设为“enemies”，然后取消 Collision -> Mask 的设置，让遮罩为空。这些设置意味着怪物可以互相穿越。如果你希望怪物之间会发生碰撞和滑动，请打开“enemies”遮罩。小怪并不需要遮罩“world”层，因为它们只会沿着 XZ 平面移动。我们是故意不去为它们添加重力影响的。

跳跃机制本身只需要两行代码。打开 Player 脚本

接下来让我们来添加踩扁机制。我们会让玩家在怪物身上弹起，并同时消灭它们。
我们需要检测与怪物的碰撞，并和与地板的碰撞相区分。要这么做，我们可以使用 Godot 的分组标签功能。
再次打开 mob.tscn 场景，选中 Mob 节点，就能在右侧的Node面板中看到信号的列表。Node面板有两个选项卡：你已经使用过的Signals，以及Groups它允许你为节点添加标签。
单击这个选项卡就会出现一个输入框，可以填写标签的名称。在这个输入框中输入“mob”（小怪）并单击添加按钮。
回到 Player脚本来编写踩扁和弹跳。
打开 mob.gd 脚本。在脚本顶部，我们要定义一个新的信号叫作 squashed（被踩扁）。你可以在底部添加 squash 函数，在里面发出这个信号并销毁这个怪物。

**杀死玩家**：
我们希望玩家在地板上移动时死亡，但如果他们在空中，则不会死亡。我们可以使用向量数学来区分这两种碰撞。但是，我们将使用 Area3D 节点，该节点适用于命中框。

回到 player.tscn 场景，添加一个新的 Area3D 子节点。把它命名为 MobDetector（小怪检测器）。添加一个 CollisionShape3D 节点作为它的一个子节点。在检查器中，给它指定一个圆柱体形状。
你可以降低圆柱体的高度并将其向上移动到角色的顶部。这样，当玩家跳跃时，形状会太高，敌人无法与之碰撞。
你还希望圆柱体比球体更宽。这样一来，玩家在碰撞之前就会被击中，并被推到怪物的碰撞盒之上。圆柱体越宽，玩家就越容易被杀死。
接下来，再次选择 MobDetector 节点，并在检查器中， 关闭 其 Monitorable 属性。这使得其他物理节点无法检测到这个区域。补充的 Monitoring 属性允许它检测碰撞。然后，清除 Collision -> Layer，并将掩码设置为“enemies”层。

在节点选项卡中，双击 body_entered 信号并将其连接到 Player

打开 main.tscn 场景，选中 Player 节点，然后在节点面板中把 hit 信号连接到 Main 节点。

**计分、播放音乐、重启游戏**：
在主场景中，添加一个新的 Control 节点作为 Main 的子项，命名为 UserInterface。你会被自动切换到 2D 屏幕，可以在这里编辑你的用户界面 User Interface（UI）。 使用视图右边的锚点预设整个矩形
创建子节点名为分数标签 ScoreLabel 的 Label
在检查器中将该 Label 的 Text 设为类似“Score: 0”的占位内容。
向下滚动到 Theme Overrides（主题覆盖）然后展开 Colors（颜色）并点击 Font Color（字体颜色）旁边的黑框来为文字着色
最后单击视口中的文本，将其拖到合适位置，或者使用锚点预设。

再次选中 UserInterface 节点。在检查器中为 Theme -> Theme 创建一个新的主题资源
单击这个资源就会在底部面板中打开主题编辑器。会展示使用你的主题资源时内置 UI 控件的外观。默认情况下，主题只有寥寥几个属性：Default Base Scale（默认基础缩放）、Default Font（默认字体）、Default Font Size（默认字体大小）。
在文件系统面板中，展开 fonts 目录，单击我们包含在项目里的 Montserrat-Medium.ttf 文件并将其拖放到Default Font（默认字体）上。文本就又会出现在主题预览中了。
文本有一点小。将Default Font Size（默认字体大小）设置为 22 像素即可增大文本的大小。

我们下一步是进行计分。为 ScoreLabel 附加一个新的脚本，并在其中定义 score（分数）变量。
打开 `main.gd` 脚本添加代码
回到 score_label.gd 脚本，定义回调函数  `_on_mob_squashed()`

我们现在就要添加死亡后重玩的能力。玩家死亡后，我们会在屏幕上现实一条消息并等待输入。
回到 main.tscn 场景，选中 UserInterface 节点，添加 ColorRect 节点作为其子项并命名为 Retry（重试）。该节点会使用单一色彩填充矩形，我们用它来覆盖画面，达到变暗的效果。
要使其覆盖整个视口，可以使用工具栏中 锚点预设 菜单。点击打开，并应用整个矩形命令。
让我们修改它的颜色，把游戏区域变暗。选中 Retry，在检查器中将 Color（颜色）设置为透明的暗色。要实现整个效果，可以在取色器中将 A 滑动条拖到左边。它控制的是颜色的 Alpha 通道，也就是不透明度。
接下来，添加一个 Label 的节点作为 Retry 的子节点并且设置他的 Text 为“Press Enter to retry”。将其移动至屏幕中央，并且选择 Anchor Preset -> Center（锚点预设 > 居中）

打开 `main.gd` 脚本

要添加音乐，让音乐在后台连续播放，我们就要用到 Godot 的另一项特性：自动加载。
要播放音频，只需往场景里添加一个 AudioStreamPlayer 节点，然后为它附加一个音频文件。启动场景时，就会自动播放。然而，如果重新加载了场景，比如我们在重玩的时候就这么干了，这些音频节点也会被重置，音乐也就会从头开始播放。
你可以使用自动加载功能来让 Godot 在游戏开始时自动加载节点或场景，不依赖于当前场景。你还可以用它来创建能够全局访问的对象。
新建场景创建一个 AudioStreamPlayer 节点然后将其重命名为 MusicPlayer（音乐播放器）
我们在 art/ 目录中包含了一条音乐音轨 House In a Forest Loop.ogg。单击并把它拖放到检查器中的 Stream（流）属性上。同时要打开 Autoplay，这样音乐就会在游戏开始时自动播放了。
将这个场景保存为 `music_player.tscn`
们必须将其注册为自动加载。转到项目 -> 项目设置…菜单，然后点击全局 -> 自动加载选项卡 路径输入框中需要输入场景的路径。单击文件夹图标打开文件浏览器，然后双击 music_player.tscn。接下来，单击右侧的添加按钮，将该节点进行注册。music_player.tscn 现在会被加载到任何你打开或播放的场景中。

**角色动画**：
打开玩家场景，选中 Player 节点，然后添加一个 AnimationPlayer 节点
动画停靠面板就会出现在底部面板中
点击动画 -> 新建 将动画命名为“float”（漂浮）
我们希望让这个动画在游戏开始时自动开始播放，而且还应该循环播放。要执行此操作，你可以单击动画工具栏上的自动播放按钮（自动播放）和循环箭头。
在面板右上角将动画的时长设为 `1.2` 秒。（单击并拖拽右下角的滑动条，即可将时间线进行缩放。）
使用动画播放器节点，你可以对所需任意数量的节点的大多数属性做动画。请注意检查器中属性旁的钥匙图标。在上面单击就可以创建一个关键帧，即对应属性的一对时间与值。关键帧会被插入到时间线上的时间光标处。
让我们来开始插入帧吧。这里，我们要为 Character 节点的位置（position）和旋转（rotation）做动画。选中 Character 并在检查器中展开 Transform 栏。单击 Position 和 Rotation 旁的钥匙图标，创建默认选择 RESET（重置）轨道
编辑器中会出现两个轨道，各有一个代表关键帧的菱形图标。
你可以在菱形滑块上单击并拖动，以移动它们的时间。将位置（position ）帧移动到 0.3 秒处，将旋转（rotation ）帧移动到 0.1 秒处。（在左上角输入动画位置0.3，时间光标将移动至动画位置，拖动菱形滑块可以自动吸附）
在 检查器 中，将 Position 的 Y 轴设置为 0.65 米，将 Rotation 的 X 轴设置为 8。为这两个属性分别创建一个关键帧。将position的关键帧移动到 `0.7` 秒，将Rotation的关键帧移动到 `0.5` 秒
将时间光标移动到动画结尾，即 `1.2` 秒。将 Y 平移量设为约 `0.35`、X 旋转量设为 `-9` 度。再次为这两个属性添加帧。
单击播放按钮即可预览结果，单击停止按钮停止播放。

你可以看到引擎通过在关键帧之间插值来生成连续动画。不过目前，生成的动作非常机械。这是因为默认的插值是线性的，会导致持续的过渡，并且与现实世界中生物的移动方式不同。我们可以使用缓动曲线来控制关键帧之间的过渡。
单击并拖拽，框选时间线上的前两个帧。可以在检查器中同时编辑这两个帧的属性，其中就有一个属性叫做 Easing（缓动）。单击并拖动曲线，把它往左拉。这样就会让他实现缓出，也就是说，一开始变得快，然后时间光标越接近下一个关键帧就变得越慢。
将缓动效果应用于旋转轨迹中的第二个关键帧。
对第二个平移关键帧执行相反操作，将其拖动到右侧。
如果这个生物离地面太近了，你可以将 `Pivot` 向上移动，达成偏移的目的。

我们可以使用代码来根据玩家的输入控制动画的播放。让我们在角色移动时修改动画的速度吧。点击 Player 旁的脚本图标打开其脚本。

在 Godot 中还有一个很好的动画技巧：只要你使用类似的节点结构，你就可以把它们复制到不同的场景中。例如，Mob 和 Player 场景都有 Pivot 和 Character 节点，所以我们可以在它们之间复用动画。
打开 Player 场景，选择 AnimationPlayer 节点，然后点击动画 > 管理动画...。点击 float 动画旁边的 将动画复制到剪贴板 按钮（两个小方块）。点击“确定”关闭窗口。
然后打开 mob.tscn，创建一个 AnimationPlayer 子节点并且选中它。点击 动画 > 管理动画，然后新建库，你应该看到信息“将创建全局库”。文本框处留白然后点击确定。点击粘贴图标（剪贴板）后就会出现在窗口中。点击确定关闭窗口。


### 横板平台冒险

Brackeys频道：https://www.youtube.com/watch?v=LOhfqjmasi0
B站搬运翻译：BV17Z421J7uF

游戏素材
Creative Commons Zero ([CC0](http://creativecommons.org/publicdomain/zero/1.0/)) license

| 文件夹    |   存放  |
| --- | --- |
|   assets  |   资产素材  |
|scenes|场景|
|scripts|代码|

分类：创建node节点重命名，并把同类型的节点放在其中

1. 把所有素材放在assets文件夹中
2. 在scenes文件夹中创建一个名为Game的场景，根节点选择2D场景
3. 此时运行项目并选择当前场景就可以打开一个空白的窗口
4. 新建场景名为player，根节点搜索选择CharacterBody2D
	1. 创建CharacterBody2D的子节点搜索选择AnimatedSprite2D（*添加动态纹理*）
	2. 在检查器窗口中找到AnimatedSprite2D节点的Animation中新建SpriteFrame
	3. 点击SpriteFrame自动打开SpriteFrames窗口，点击从精灵表中添加帧，选择res://assets/sprites/knight.png，设置8×8的立绘表格，按顺序点击每一帧添加动画添加（像素风需要在项目设置中禁用纹理平滑）。然后可以给动画命名idle并设置自动播放。添加其他动画。
	4. 创建CharacterBody2D的子节点搜索选择 CollisionObject2D （*添加碰撞体积*）
	5. 在检查器窗口中找到CollisionObject2D节点的shape新建circleshape，设置合适的大小和位置与立绘重合
5. 回到场景Game，把场景player拖动到场景Game之中
	1. 创建2D场景的子节点搜索选择 Camera2D
	2. 在检查器窗口中找到Camera2D设置zomm为4,4以缩小摄像机视角
	3. 把Camera2D拖到player场景节点上，变为其子节点即可实现镜头跟随。注意把摄像头中心拖到人物中心，还可以在Camera2D检查器窗口启用位置平滑功能
	4. 创建2D场景的子节点搜索选择 StaticBody2D
	创建CharacterBody2D的CollisionObject2D子节点，并设置shape为worldboundaryshape2D，移动到合适位置
6. 在场景player中设置根节点的脚本，使用默认移动模板，并修改路径到scripts文件夹中
7. 回到场景Game，删除为测试脚本临时创建的地面StaticBody2D节点，创建TileMapLayer节点
	1. 在TileMapLayer检查器窗口，新建tile set并设置tile size点击，点击tile set自动打开tile set/tile map窗口
	2. 将res://assets/sprites/world_tileset.png拖入tile set窗口的图片源，点击确认自动创建。（可以通过橡皮工具删除图块，然后生成一个更大的图块）
	3. 点击tile map窗口使用画笔工具就可以在场景中绘制
	4. 在检查器窗口中找到TileMapLayer，点击Physics Layers添加元素。在tile set窗口的绘制属性可以给图块添加物理层，还可以设置物理层的具体形状大小

	设置z轴确保渲染顺序

	
```GDScript
extends Sprite2D

var speed = 400
var angular_speed = PI


func _process(delta):
	rotation += angular_speed * delta

	var velocity = Vector2.UP.rotated(rotation) * speed

	position += velocity * delta
```

监听玩家的输入

```GDScript
extends Sprite2D

var speed = 400
var angular_speed = PI


func _process(delta):
	var direction = 0
	if Input.is_action_pressed("ui_left"):
		direction = -1
	if Input.is_action_pressed("ui_right"):
		direction = 1

	rotation += angular_speed * direction * delta

	var velocity = Vector2.ZERO
	if Input.is_action_pressed("ui_up"):
		velocity = Vector2.UP.rotated(rotation) * speed

	position += velocity * delta
```

### 软件开发

#### 计算器

目标：基本复制windows自带的计算器
*可以安装powertoys工具，里面有屏幕标尺和屏幕取色工具，帮助我们更好地复制*
*直接取色只能取聚焦的颜色，想取一般颜色和按下颜色可以截图再取色*

分析UI ：
横向显示框
竖向排列的（网格排列的数字按钮、网格排列的运算符按钮）

一般制作软件只需要Control类：
- Control类是所有 UI 相关节点的基类
- 其中继承Control 类的 Container类是所有 GUI 容器的基础节点

**计算器界面**：
项目 - 项目设置 - 显示 - 窗口设置尺寸约为 480 * 720

```text
.
└─ Control
		└─ PanelContainer
				└─ MarginContainer
						└─ VBoxContainer
								├─ Label
								└─ HBoxContainer
										├─ GridContainer
										│		└─ Button * 12
										└─ GridContainer2
												└─ Button * 8
```

（*锚点预设、水平 /垂直对齐扩展均在工具栏中视图右边*）
先创建上述所有节点，但是暂时只创建一个Button
把Control、PanelContainer锚点预设设置为填充整个矩形
Label设置Layout最小尺寸Custom Minimum Size y为大概200px。水平对齐方式HorizontalAlignment改为右对齐，垂直对齐方式VerticalAlignmen改为居中。自动换行AutowrapMode改为。启用Clip Text，设置Text OverrunBehavior为Ellipsis。设置Theme Overrides-Font Size字号为40px。
HBoxContainer设置垂直对齐扩展
GridContainer、GridContainer2 设置水平对齐扩展
GridContainer、GridContainer2 的Layout-Container Sizing-Stretch Ratio 值均默认是1，代表以1的比例划分空间。把它们分别改为3、2
先随意修改button text只是为了可见，同时设置水平 /垂直对齐扩展。复制该节点，在GridContainer下粘贴11个，在GridContainer下粘贴8个（*使用快捷键ctrl+shift+v粘贴同级节点*）。
分别修改button text为“7，8，9，4，5，6，1，2，3，0，.，（”、“ ←，C，×，÷，＋，－，），=”
GridContainer、GridContainer2 分别设置列数Columns为3、2
MarginContainer 设置Theme Overrides-Constants 修改页面边距大约分别为5、6、5、6

**脚本**：
为了简化脚本，忽略括号按钮的功能
把所有button的pressed信号绑定

 ```GDScript
 extends Control

var str := ""

func _ready() -> void:
	print("hello")
	$PanelContainer/MarginContainer/VBoxContainer/Label.set_text("hi")

func _physics_process(delta: float) -> void:
	$PanelContainer/MarginContainer/VBoxContainer/Label.set_text(str)

func eval(str):
	var sum := 0
	var nums := [""]
	var flag := 0
	var operator := []
	for s in str:
		match s:
			"＋":
				operator.append(0)
				flag += 1
				nums.append("")
			"－":
				operator.append(1)
				flag += 1
				nums.append("")
			"×":
				operator.append(2)
				flag += 1
				nums.append("")
			"÷":
				operator.append(3)
				flag += 1
				nums.append("")
			_:
				nums[flag] += s
	print(nums)
				
	for k in range(flag+1):
		nums[k] = nums[k].to_float()

	for i in range(flag):
		if (2 in operator) or (3 in operator):
			if operator[i] == 2:
				nums[i] *= nums[i+1]
				nums[i+1] = 0
				operator[i] = 0
			elif operator[i] == 3:
				nums[i] /= nums[i+1]
				nums[i+1] = 0
				operator[i] = 0
				
	print(nums)
	
	for i in range(flag):
			if operator[i] == 0:
				nums[i+1] += nums[i]
			elif operator[i] == 1:
				nums[i+1] = nums[i] - nums[i+1]

	return nums[flag]

func _on_button_pressed() -> void:
	print(7)
	str += "7"

func _on_button_2_pressed() -> void:
	print(8)
	str += "8"

func _on_button_3_pressed() -> void:
	print(9)
	str += "9"

func _on_button_4_pressed() -> void:
	print(4)
	str += "4"

func _on_button_5_pressed() -> void:
	print(5)
	str += "5"

func _on_button_6_pressed() -> void:
	print(6)
	str += "6"

func _on_button_7_pressed() -> void:
	print(1)
	str += "1"

func _on_button_8_pressed() -> void:
	print(2)
	str += "2"

func _on_button_9_pressed() -> void:
	print(3)
	str += "3"

func _on_button_10_pressed() -> void:
	print(0)
	str += "0"

func _on_button_11_pressed() -> void:
	print(".")
	str += "."

func _on_button_12_pressed() -> void:
	print("(")

func _on_button_pressed2() -> void:
	print("←")
	str = str.substr(0, str.length() - 1)

func _on_button_2_pressed2() -> void:
	print("C")
	str = ""
	$PanelContainer/MarginContainer/VBoxContainer/Label.set_text("")

func _on_button_3_pressed2() -> void:
	print("×")
	str += "×"

func _on_button_4_pressed2() -> void:
	print("÷")
	str += "÷"

func _on_button_5_pressed2() -> void:
	print("＋")
	str += "＋"

func _on_button_6_pressed2() -> void:
	print("－")
	str += "－"

func _on_button_7_pressed2() -> void:
	print("）")

func _on_button_8_pressed2() -> void:
	print("=")
	str = str(eval(str))
	$PanelContainer/MarginContainer/VBoxContainer/Label.set_text(str)
```

**界面美化**：
主题在Theme里修改，由于继承关系，只需要改变父节点子节点也会自动改变
子节点的Theme会覆盖父节点的Theme，而且对于具体的节点Theme Overrides会覆盖Theme

Control节点检查器面板 Theme-新建Theme，然后点击新建的Theme，即可在下方打开主题面板
主题面板右上角可以添加项目类型，然后在下方可以添加主题属性然后新建属性资源并修改（不仅可以在主题面板中修改，还可以在检查器面板修改）
添加PanelContainer项目类型，在下方添加panel，新建StyleBoxFlat，修改编辑颜色BG Color约为#202020
添加Button项目类型，在下方添加
font_size，字号改为24
focus，新建空的StyleBox，避免有聚焦框
hover，新建StyleBoxFlat，修改颜色BG Color为#323232，倒角Corner Radius均为5px
normal，新建StyleBoxFlat，修改颜色BG Color为#3c3c3c，倒角Corner Radius均为5px
pressed，新建StyleBoxFlat，修改颜色BG Color为#202020，倒角Corner Radius均为5px

希望运算符按钮的颜色与数字按钮不同，同样的做法，在GridContainer2节点检查器面板 Theme-新建Theme
添加Button项目类型
hover，新建StyleBoxFlat，修改颜色BG Color为#3c3c3c
normal，新建StyleBoxFlat，修改颜色BG Color为#323232

希望等号的颜色为红色，直接修改Button的Theme Overrides-Styles
hover，新建StyleBoxFlat，修改颜色BG Color为#e89376
normal，新建StyleBoxFlat，修改颜色BG Color为#ffa180
pressed，新建StyleBoxFlat，修改颜色BG Color为#d2866c

作为一个软件有游戏引擎的启动画面太违和了，可以在项目——项目设置——应用——启动画面中关闭

## 项目效果
