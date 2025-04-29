# 网页

HTML 定义了网页的内容
CSS 描述了网页的布局
JavaScript 控制了网页的行为

**vscode插件**：
HTML语言插件
open in browser 浏览器预览页面
Live Server 快速架设本地服务器环境，实时预览页面
Microsoft Edge Tools for VS Code 浏览器开发者工具

## HTML

**超文本标记语言**(HyperText Markup Language)是一种用于创建网页的标准标记语言。

HTML文档的后缀名为  .html
注释：`<!--  -->`
换行：`<br>`
水平线：`<hr>`

- HTML 元素以开始标签起始 `<html>`
- HTML 元素以结束标签终止 `</html>` *换行等空标签没有结束标签*
- 元素的内容是开始标签与结束标签之间的内容
- 某些 HTML 元素具有空内容（empty content）
- 空元素在开始标签中进行关闭（以开始标签的结束而结束）
- 大多数 HTML 元素可拥有属性
- 大多数 HTML 元素可以嵌套

```html
<!-- ！加回车可以一键生成如下框架 -->
<!DOCTYPE html>
<!-- 申明html文档 -->
<html lang="en">
<!-- 根元素 设置主语言为en-->
<head>
<!-- 头元素 -->
    <title>Document</title>
</head>
<body>
<!-- 可见的页面内容 -->
</body>
</html>
```

### HTML head

`<head>` 元素包含了所有的头部标签元素。在 `<head>`元素中你可以插入脚本（scripts）, 样式文件（CSS），及各种meta信息。

1. `<style>` 定义了HTML文档的样式文件引用地址,也可以直接添加CSS样式来渲染 HTML 文档
2. `<noscript>`
3. `<base>` 描述了基本的链接地址/链接目标，该标签作为HTML文档中所有的链接标签的默认链接

#### title标题

定义了浏览器工具栏的标题;当网页添加到收藏夹时，显示在收藏夹中的标题;显示在搜索引擎结果页面的标题

`<title>标题</title>`

#### meta元数据

描述了一些基本的元数据。元数据也不显示在页面上，但会被浏览器解析。通常用于指定网页的描述，关键词，文件的最后修改时间，作者，和其他元数据。元数据可以使用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他Web服务。

##### 指定文档中的字符编码

`<meta charset="utf-8" />`
每30秒钟刷新页面 `<meta http-equiv="refresh" content="30">`

##### 添加作者和描述

```html
<meta name="author" content="Tom" />
```

```html
<meta
  name="description"
  content="The MDN Web Docs site
  provides information about Open Web technologies
  including HTML, CSS, and APIs for both Web sites and
  progressive web apps." />
```

name 指定了 meta 元素的类型；说明该元素包含了什么类型的信息。
content 指定了实际的元数据内容。

#### link链接

##### 添加图标

`<link rel="icon" href="favicon.ico" type="image/x-icon" />`
一般支持.ico .gif .png格式

其他类型的图标：

```html
<!-- 含有高分辨率 Retina 显示屏的第三代 iPad：-->
<link
  rel="apple-touch-icon-precomposed"
  sizes="144x144"
  href="https://developer.mozilla.org/static/img/favicon144.png" />
<!-- 含有高分辨率 Retina 显示屏的 iPhone：-->
<link
  rel="apple-touch-icon-precomposed"
  sizes="114x114"
  href="https://developer.mozilla.org/static/img/favicon114.png" />
<!-- 第一代和第二代 iPad：-->
<link
  rel="apple-touch-icon-precomposed"
  sizes="72x72"
  href="https://developer.mozilla.org/static/img/favicon72.png" />
<!-- 不含高分辨率 Retina 显示的 iPhone、iPod Touch 和 Android 2.1+ 设备：-->
<link
  rel="apple-touch-icon-precomposed"
  href="https://developer.mozilla.org/static/img/favicon57.png" />
<!-- 基本 favicon -->
<link
  rel="icon"
  href="https://developer.mozilla.org/static/img/favicon32.png" />
```

##### 链接到样式表

`<link rel="stylesheet" href="my-css-file.css" />`

#### script脚本

用于加载脚本文件

`<script src="my-js-file.js" defer></script>`
最好加上 defer 以告诉浏览器在解析完成 HTML 后再加载 JavaScript。这样可以确保在加载脚本之前浏览器已经解析了所有的 HTML 内容。这样你就不会因为 JavaScript 试图访问页面上不存在的 HTML 元素而产生错误。

#### noscript

如果页面上的脚本类型不受支持或者当前在浏览器中关闭了脚本，则在 HTML `<noscript>` 元素中定义脚本未被执行时的替代内容。

`<noscript>您的浏览器不支持或已关闭使用脚本</noscript>`

#### style样式

包含文档的样式信息或者文档的部分内容。默认情况下，该标签的样式信息通常是CSS的格式

type该属性以 MIME 类型（不应该指定字符集）定义样式语言。如果该属性未指定，则默认为 text/css。
media该属性规定该样式适用于哪个媒体。属性的取值为CSS媒体查询，默认值为 all。
nonce一种加密的随机数（一次使用的数字），用于在style-src Content-Security-Policy (en-US)中将内联样式列入白名单。服务器每次发送策略时都必须生成一个唯一的随机数值。
title指定可选的样式表。

```html
    <style>
      p {
        color: white;
        background-color: blue;
        padding: 5px;
        border: 1px solid black;
      }
    </style>
    <style media="all and (max-width: 500px)"> 
    /* 视图宽度小于 500px 时生效 */
      p {
        color: blue;
        background-color: yellow;
      }
    </style>
```

#### base

指定用于一个文档中包含的所有相对 URL 的根 URL。一份中只能有一个 `<base>` 元素。
如果指定了多个 `<base>` 元素，只会使用第一个 href 和 target 值，其余都会被忽略。

一个文档的基本 URL，可以通过使用 `document.baseURI`的 JS 脚本查询。如果文档不包含 `<base>` 元素，baseURI 默认为 `document.location.href`

```html
给定 <base href="https://example.com">

以及此链接 <a href="#anchor">Anker</a>

链接指向 https://example.com/#anchor
```

### HTML body

Body onload 事件在页面载入完成后立即触发。

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script>
function myFunction(){
    alert("页面加载完成");
}
</script>
</head>
<body onload="myFunction()">
<h1>Hello World!</h1>
</body>
</html>
```

#### HTML 标题

通过 `<h1>`- `<h6>` 标签来定义

```html
<h1>一级标题</h1>
<h2>二级标题</h2>
```

#### HTML 段落

通过标签 `<p>` 定义

```html
<p>一个段落</p>
<p>另一个段落</p>
```

`<br>`在不产生一个新段落的情况下进行**换行**

`hr`在文档中生成一条**水平分割线**

##### 文本格式化标签

```html
<b></b>                     定义粗体文本
<em></em>             定义着重文字
<i></i>                     定义斜体字
<small></small>             定义小号字
<strong></strong>     定义加重语气
<sub></sub>             定义下标字
<sup></sup>             定义上标字
<ins></ins>             定义插入字
<del></del>             定义删除字
```

#### HTML 列表

##### 无序列表

无序列表粗体圆点进行标记。
无序列表使用 `<ul>` 标签，每个列表项始于 `<li>` 标签

```html
    <ul>
        <li>one</li>
        <li>two</li>
        <li>three</li>
    </ul>
```

##### 有序列表

有序列表使用数字进行标记。
有序列表使用 `<ol>` 标签，每个列表项始于 `<li>` 标签。

```html
    <ol>
        <li>one</li>
        <li>two</li>
        <li>three</li>
    </ol>
```

##### 自定义列表

自定义列表以 `<dl>` 标签开始。每个自定义列表项以 `<dt>` 开始。每个自定义列表项的定义以 `<dd>` 开始。

```html
    <dl>
        <dt>数字</dt>
        <dd>一</dd>
        <dd>二</dd>
        <dt>num</dt>
        <dd>one</dd>
        <dd>two</dd>
    </dl>
```

#### HTML 超链接

通过标签 `<a>` 定义

超链接可以是一个字，一个词，或者一组词，也可以是一幅图像，您可以点击这些内容来跳转到新的文档或者当前文档中的某个部分
**`<a href="url">链接(文本、图片或其他 HTML 元素)</a>`**
*URL 可以指向 HTML 文件、文本文件、图像、文本文档、视频和音频文件以及可以在网络上保存的任何其他内容。如果浏览器不知道如何显示或处理文件，它会询问你是否要打开文件（需要选择合适的本地应用来打开或处理文件）或下载文件*

> **必要属性**：
> `href` 指定链接的地址
> **可选属性**：
> `title` 当鼠标指针悬停时的提示信息
> `target` 可以定义被链接的文档在何处显示
> **特殊**：
> `download` 当你链接到要下载的资源而不是在浏览器中打开时，你可以使用 download 属性来提供一个默认的保存文件名
> `mailto:`协议 `<a href="mailto:name@email.com">Email</a>`自动打开当前计算机系统中默认的电子邮件客户端软件(需要设置mailto:协议的默认应用)

- target="_blank":在新窗口中浏览新的页面。（默认）
- target="_self":在同一个窗口打开新的页面。
- target="框架的name名":在该框架内打开新的页面。
- target="_parent":在父窗口中打开新的页面。（页面中使用框架才有用）
- target="_top" :以整个浏览器作为窗口显示新页面。（突破了页面框架的限制）

```html
<a href="mailto:name@email.com?cc=name2@rapidtables.com&bcc=name3@rapidtables.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email">Email</a>
<!-- 
mailto:收件邮箱地址
cc=抄送收件邮箱地址
bcc=秘密抄送收件邮箱地址
subject=主题
body=内容 
-->
```

href还可以指向id在同页面跳转：

```html
<a href="#target">跳转到目标区域</a>
<div id="target">这是目标区域</div>
```

导航栏：

```html
<style>
    /* 导航栏样式 */
    .sidebar {
        position: fixed; /* 固定导航栏 */
        top: 0;
        left: 0;
        width: 270px;
        height: 100%; /* 占满左侧高度 */
        background-color: transparent; /* 将背景改为透明 */
        overflow-y: auto; /* 如果内容超出，添加滚动条 */
        z-index: 1000; /* 确保导航栏在最上层 */
        pointer-events: none; /* 整个侧边栏默认不响应鼠标事件 */
    }
    .nav-menu {
        position: relative;
        width: 100%;
        pointer-events: auto; /* 导航菜单恢复响应鼠标事件 */
    }
    .nav-menu-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 10px;
        background-color: rgba(76,175,80,0.8); /* 半透明背景 */
        cursor: pointer;
    }
    .nav-menu-header a {
        text-decoration: none;
        color: #333;
        font-weight: bold;
    }
    .nav-arrow {
        display: flex;
        align-items: center;
        font-size: 12px;
        color: #999;
        transition: transform 0.3s ease;
    }
    .nav-arrow.up {
        transform: rotate(180deg); /* 向上箭头 */
    }
    .nav-menu-body {
        display: none; /* 默认隐藏 */
        position: relative;
        top: 100%;
        left: 0;
        background-color: rgba(255, 255, 255, 0.8); /* 半透明白色背景 */
        border: 1px solid #ddd;
        z-index: 1000;
        width: 100%;
    }
    .nav-menu-body a {
        display: block;
        text-decoration: none;
        color: #333;
        padding: 10px;
        border-bottom: 1px solid #ddd;
    }
    .nav-menu-body a:hover {
        background-color: #f4f4f4;
        color: #4CAF50;
    }
</style>
<div class="sidebar">
    <div class="nav-menu" id="nav-menu">
        <div class="nav-menu-header" id="nav-menu-header">
            <a href="#basic-info" target="_top"><span>基本信息</span></a>
            <span class="nav-arrow" id="nav-arrow"><span class="nav-icon">﹀</span></span>
        </div>
        <div class="nav-menu-body" id="nav-menu-body">
            <div class="nav-menu-panel">
                <a href="#scoring-criteria" target="_top">评分标准</a>
                <a href="#pre-production" target="_top">1.0 预生产任务</a>
                <a href="#lab-capability" target="_top">2.0 实验室能力</a>
            </div>
        </div>
    </div>
</div>
<script>
    document.addEventListener('DOMContentLoaded', function () {
        const menuHeader = document.getElementById('nav-menu-header');
        const menuArrow = document.getElementById('nav-arrow');
        const menuBody = document.getElementById('nav-menu-body');
        const navMenu = document.querySelector('.nav-menu');

        // 鼠标悬停时显示菜单并改变箭头方向
        menuHeader.addEventListener('mouseenter', function () {
            menuArrow.classList.add('up'); // 改变箭头方向
            menuBody.style.display = 'block'; // 显示菜单
        });

        // 鼠标离开导航菜单时隐藏菜单
        navMenu.addEventListener('mouseleave', function () {
            menuArrow.classList.remove('up'); // 恢复箭头方向
            menuBody.style.display = 'none'; // 隐藏菜单
        });

        // 点击菜单项时隐藏菜单
        menuBody.addEventListener('click', function () {
            menuArrow.classList.remove('up'); // 恢复箭头方向
            menuBody.style.display = 'none'; // 隐藏菜单
        });
    });
</script>
```

设置footer仅在页面顶部可见：

```html
<footer class="no-print">
    <p>&copy;</p>
</footer>
<script>
    document.addEventListener('DOMContentLoaded', function () {
        const footer = document.querySelector('footer');
        window.addEventListener('scroll', function () {
            if (window.scrollY === 0) {
                footer.style.display = 'block'; // 显示footer
            } else {
                footer.style.display = 'none'; // 隐藏footer
            }
        });
    });
```

#### HTML 区块

大多数 HTML 元素被定义为块级元素或内联元素
块级元素在浏览器显示时，通常会以新行来开始（和结束）

内联元素在显示时通常不会以新行开始

**`<div>`标签在网页开发中十分常用**

##### div

HTML `<div>` 元素是块级元素，它可用于组合其他 HTML 元素的容器。
`<div></div>` 没有特定的含义。除此之外，由于它属于块级元素，浏览器会在其前后显示换行。

通常与 CSS 一同使用，可用于对大的内容块设置样式属性，并用于文档布局。
还可以在javascript中用于分配事件

##### span

HTML `<span>` 元素是内联元素，可用作文本的容器
`<span></span>` 也没有特定的含义。

当与 CSS 一同使用时，可用于为部分文本设置样式属性。

#### HTML 表格

HTML 表格是一种用于展示结构化数据的标记语言元素。
HTML 表格由 **`<table>`** 标签来定义。

- **`<tr>`** ：tr 是 table row 的缩写，表示表格的一行。
- **`<td>`** ：td 是 table data 的缩写，表示表格的数据单元格。
- **`<th>`** ：th 是 table header的缩写，表示表格的表头单元格。通过使用 `<th>` 元素定义列标题，可以使其在表格中以粗体显示，与普通单元格区分开来。(表格可以没有表头)

还有以下标签：
`<thead>` 用于定义表格的标题部分: 在 `<thead>` 中，使用 `<th>` 元素定义列的标题
`<tbody>` 用于定义表格的主体部分: 在 `<tbody>` 中，使用 `<tr>` 元素定义行，并在每行中使用 `<td>` 元素定义单元格数据
HTML 表格还可以具有其他部分，如 `<tfoot>` （表格页脚，用于在表格的底部定义摘要、统计信息等内容）和 `<caption>` （表格标题，用于为整个表格定义标题）

**一个表格至少要有 `<table>`、`<tr>`、`<td>`这三个标签**

> **允许单元格跨越多行和列**:
> 表格中的标题和单元格有 单元格的宽度 `colspan` 和 单元格的高度 `rowspan` 属性，接受一个没有单位的数字值，数字决定了它们的宽度或高度是几个单元格。
>
> **定义“列的样式”**：
> 如果列的样式相同，或许可以会设置一个 class 包含同一列，然后在一个单独的样式表中定义样式。
> 不过为了方便，可以使用 `<colgroup>`容器与 `<col>`元素
> 如果没有采取任何样式，但是我们仍然需要添加一个空的 `<col />` 元素
> `span` 属性 需要一个无单位的数字值，用来指定让这个样式应用到表格中多少列

```html
    <style>
        table {
            text-align: center; /*文字居中*/
            border-collapse: collapse;
        }
        table th, table td, table tr {
            border: solid 1px black;
        }
    </style>

    <table> 
        <caption>国际单位制</caption>
        <colgroup>
            <col style="background-color: yellow" />
            <col span="2"/>
            <col style="background-color: #6fdcf4" />
            <!-- 因为合并过两列，结果可能不能满意 -->
        </colgroup>
        <tr>
            <th rowspan="2">基本量</th> <!-- 合并两行 -->
            <th rowspan="2">基本量纲</th>
            <th colspan="2">SI单位</th> <!-- 合并两列 -->
        </tr>
        <tr>
            <th>名称</th>
            <th>符号</th>
        </tr>
        <tr>
            <td>长度</td>
            <td>L</td>
            <td>米</td>
            <td>m</td>
        </tr>
        <tr>
            <td>质量</td>
            <td>M</td>
            <td>千克</td>
            <td>kg</td>
        </tr>
    </table>
```

#### HTML 多媒体

##### HTML img图片

通过标签 `<img>` 定义

**`<img src="url" alt="some_text">`**

> **必要属性**：
> `src` 指向我们想要引入的图片的路径，可以是相对路径或绝对URL。但是不推荐绝对URL，这会使浏览器做更多的工作
> **可选属性**：
> `alt` 用来为图像定义一串预备的可替换的文本。在浏览器无法载入图像时，浏览器将显示这个替代性的文本
> `title` 当鼠标指针悬停时的提示信息
> `height`（高度）与 `width`（宽度）属性用于设置图像的高度与宽度，不过一般可用css设置

```html
<img decoding="async" src="/images/logo.png" width="258" height="39" />
```

**响应式图片**
我们可以使用两个新的属性——srcset 和 sizes——来提供更多额外的资源图像和提示，帮助浏览器选择合适的一个资源。

```html
<img
  srcset="a.jpg 480w, b.jpg 800w"
  sizes="(max-width: 600px) 480px,
         800px"
  src="b.jpg"
  alt="this is a test" />
```

- **`srcset`** 定义了浏览器可选择的图片设置以及每个图片的大小，每张图片信息的设置和前一个用逗号隔开，每个设置要写：
  - 一个文件名（elva-fairy-480w.jpg）
  - 一个空格
  - 图片的固有宽度（480w）。注意，这里使用宽度描述符 w，而非 px。图片的固有宽度是它的真实大小，可以通过检查你电脑上的图片文件找到
- **`sizes`** 定义了一组媒体条件（例如屏幕宽度）并且指明当某些媒体条件为真时，什么样的图片尺寸是最佳选择：
  当视窗的宽度小于等于 600px，选用480px；否则，选用800px的图片

*需要固有宽度比较麻烦，可以使用 `<picture>`标签*

```html
<a href="https://example.com" target="_blank">
  <img src="image.jpg" alt="描述图片" style="width:200px;height:auto;">
</a>
```

##### HTML picture图片

使用 `<picture>`标签而不是直接使用 `<img>`，因为可以更改显示的图像以适应不同的显示尺寸、在 `<picture></<picture>>` 标签之间放置内容
**在任何情况下，你都必须在 `</picture>` 之前正确提供一个 `<img>` 元素以及它的 src 和 alt 属性，否则不会有图片显示**

```html
<picture>
  <source media="(max-width: 799px)" srcset="a.jpg" />
  <source media="(min-width: 800px)" srcset="b.jpg" />
  <img src="b.jpg" alt="this is a test" />
</picture>
```

##### HTML audio音频

目前，`<audio>` 元素支持的3种文件格式：MP3、Wav、Ogg。
可以在 `<audio></audio>` 之间放置内容，当浏览器不支持 `<audio>` 标签的时候，就会显示这段内容。

**`<audio src="viper.mp3" type="audio/mp3" controls/>`**

```html
<audio controls>
  <source src="viper.mp3" type="audio/mp3" />
  <source src="viper.ogg" type="audio/ogg" />
  <p>你的浏览器不支持 HTML5 音频，可点击<a href="viper.mp3">此链接</a>收听。</p>
</audio>

```

> **必要属性**：
> `src` 指向你想要嵌入网页当中的音频资源，也可以放在 `<source>`标签中
> **可选属性**：
> `type` 如果你没有添加 type 属性，浏览器会尝试加载每一个文件，直到找到一个能正确播放的格式，这样会消耗掉大量的时间和资源
> `preload` 这个属性被用来缓冲较大的文件，有 3 个值可选："none"不缓冲；"auto"页面加载后缓存媒体文件；"metadata"仅缓冲文件的元数据
> **控制属性**：
> `controls` 浏览器提供的控件界面，你也可以使用合适的 JavaScript API 创建自己的控件界面
> `autoplay` 立即播放音频和视频内容，即使页面的其他部分还没有加载完全。建议不要应用这个属性，因为用户们会比较反感自动播放的媒体文件
> `loop` 让音频或者视频文件循环播放
> `muted` 媒体播放时，默认关闭声音

##### HTML video视频

目前，`<video>` 元素支持三种视频格式：MP4、WebM、Ogg。
可以在 `<video></video>` 标签之间放置内容，当浏览器不支持 `<video>` 标签的时候，就会显示这段内容。可以提供一个指向这个视频文件的链接，从而使用户可以访问到这个文件

**`<video src="example.mp4" type="video/mp4" width="320" height="240" controls>`**

```html
<video width="320" height="240" controls>
    <source src="example.mp4" type="video/mp4">
    <source src="example.ogg" type="video/ogg">
    你的浏览器不支持 HTML5 视频
</video>
```

> **必要属性**：
> `src` 指向你想要嵌入网页当中的视频资源，也可以放在 `<source>`标签中
> **可选属性**：
> `width` 和 `height` 控制视频的尺寸，也可以用 CSS 来控制视频尺寸。视频会保持它原始的长宽比，因此可以只写一个属性，如果你设置的尺寸没有保持视频原始长宽比，那么视频边框将会拉伸，而未被视频内容填充的部分，将会显示默认的背景颜色。
> `type` 如果你没有添加 type 属性，浏览器会尝试加载每一个文件，直到找到一个能正确播放的格式，这样会消耗掉大量的时间和资源
> `poster` 指向了一个图像的 URL，这个图像会在视频播放前显示。通常用于粗略的预览或者广告。
> `preload` 这个属性被用来缓冲较大的文件，有 3 个值可选："none"不缓冲；"auto"页面加载后缓存媒体文件；"metadata"仅缓冲文件的元数据
> **控制属性**：
> `controls` 浏览器提供的控件界面，你也可以使用合适的 JavaScript API 创建自己的控件界面
> `autoplay` 立即播放音频和视频内容，即使页面的其他部分还没有加载完全。建议不要应用这个属性，因为用户们会比较反感自动播放的媒体文件
> `loop` 让音频或者视频文件循环播放
> `muted` 媒体播放时，默认关闭声音

##### source源

将 src 属性从音频或视频标签中移除，转而将它放在几个单独的标签 `<source>`  当中
浏览器将会检查 `<source>` 标签，并且播放第一个能够正常播放的的媒体，提高兼容性

```html
<video controls>
  <source src="example.mp4" type="video/mp4" />
  <source src="example.webm" type="video/webm" />
  <p>
    你的浏览器不支持 HTML5 视频。可点击<a href="example.mp4">此链接</a>观看
  </p>
</video>

```

##### track音轨

音轨使用WebVTT格式

```vtt
WEBVTT

1
00:00:22.230 --> 00:00:24.606
第一段字幕

2
00:00:30.739 --> 00:00:34.074
第二段

  ...
```

以 .vtt 后缀名保存文件。
用 `<track>` 标签链接 .vtt 文件， `<track>` 标签需放在 `<audio>` 或 `<video>` 标签当中，同时需要放在所有 `<source>` 标签之后。使用 kind 属性来指明是哪一种类型，如 subtitles、captions、descriptions。然后，使用 srclang 来告诉浏览器你是用什么语言来编写的 subtitles。

```html
<video controls>
  <source src="example.mp4" type="video/mp4" />
  <source src="example.webm" type="video/webm" />
  <track kind="subtitles" src="subtitles_en.vtt" srclang="en" />
</video>
```

#### HTML 嵌入

##### HTML iframe框架

通过使用框架，可以在同一个浏览器窗口中显示不止一个页面。
可以在 `<iframe></iframe>` 标签之间包含备选内容，如果浏览器不支持 `<iframe>`，将会显示备选内容
*为了提高速度，可以在主内容完成加载后，再使用 JavaScript 设置 iframe 的 src 属性*

**`<iframe src="URL"></iframe>`** 该URL指向不同的网页

> **必要属性**：
> `src` 包含指向要嵌入文档的 URL 路径
> **可选属性**：
> `height 和 width` 用来定义iframe标签的高度与宽度。属性默认以像素为单位, 但是你可以指定其按比例显示(如50%)
> allowfullscreen 如果设置，`<iframe>`则可以通过全屏 API 设置为全屏模式
> `frameborder` 用于定义iframe表示是否显示边框。默认有边框，设置属性值为 "0" 移除iframe的边框，在 CSS 中可以更好地实现相同的效果
> `sandbox` 沙盒化，提高安全性设置。如果绝对需要，你可以逐个添加权限。`永远不应该同时添加 allow-scripts 和 allow-same-origin`

使用 iframe 来显示目标链接页面

```html
    <iframe  name="iframe_a"></iframe>
    <a href="./1.html" target="iframe_a" rel="noopener">第一个网页</a>
    <a href="./2.html" target="iframe_a" rel="noopener">第二个网页</a>
```

直接将src设置为指定的PDF文件就可以预览PDF

```html
<iframe src="/index.pdf" width="100%" height="100%">
This browser does not support PDFs. Please download the PDF to view it: <a href="/index.pdf">Download PDF</a>
</iframe>
```

###### sandbox属性

- `allow-downloads-without-user-activation` **实验性**: 允许在没有征求用户同意的情况下下载文件。
- `allow-forms`: 允许嵌入的浏览上下文提交表单。如果没有使用该关键字，则无法提交表单。
- `allow-modals`: 允许嵌入的浏览上下文打开模态窗口。
- `allow-orientation-lock`: 允许嵌入的浏览上下文锁定屏幕方向（译者注：比如智能手机、平板电脑的水平朝向或垂直朝向）。
- `allow-pointer-lock`: 允许嵌入的浏览上下文使用 Pointer Lock API
- `allow-popups`: 允许弹窗 (例如 window.open, target="_blank", `showModalDialog`)。如果没有使用该关键字，相应的功能将自动被禁用。
- `allow-popups-to-escape-sandbox`: 允许沙箱化的文档打开新窗口，并且新窗口不会继承沙箱标记。例如，安全地沙箱化一个广告页面，而不会在广告链接到的新页面中启用相同的限制条件。
- `allow-presentation`: 允许嵌入的浏览上下文开始一个 presentation session
- `allow-same-origin`: 如果没有使用该关键字，嵌入的浏览上下文将被视为来自一个独立的源，这将使same-origin policy同源检查失败。
- `allow-scripts`: 允许嵌入的浏览上下文运行脚本（但不能创建弹窗）。如果没有使用该关键字，就无法运行脚本。
- `allow-storage-access-by-user-activation` **实验性**: 允许嵌入的浏览上下文通过Storage Access API使用父级浏览上下文的存储功能。
- `allow-top-navigation`: 允许嵌入的浏览上下文导航（加载）内容到顶级的浏览上下文。
- `allow-top-navigation-by-user-activation`: 允许嵌入的浏览上下文在经过用户允许后导航（加载）内容到顶级的浏览上下文。

##### embed

embed 标签定义嵌入的内容，比如插件

| 属性   | 值     | 描述                 |
| ------ | ------ | -------------------- |
| height | pixels | 设置嵌入内容的高度。 |
| width  | pixels | 设置嵌入内容的宽度。 |
| type   | type   | 定义嵌入内容的类型。 |
| src    | url    | 嵌入内容的 URL。     |

```html
<embed src="/index.pdf" type="application/pdf" width="100%" height="100%">
```

##### object

object 定义一个嵌入的对象，请使用此元素向页面添加多媒体。此元素允许您规定插入 HTML 文档中的对象的数据和参数，以及可用来显示和操作数据的代码。用于包含对象，比如图像、音频、视频、Java applets、ActiveX、PDF 以及 Flash。

```html
<object data="/index.pdf" type="application/pdf" width="100%" height="100%">
<iframe src="/index.pdf" width="100%" height="100%" style="border: none;">
This browser does not support PDFs. Please download the PDF to view it: <a href="/index.pdf">Download PDF</a>
</iframe>
</object>
```

#### HTML 表单

HTML 表单表示文档中的一个区域，此区域包含交互控件，将用户收集到的信息发送到 Web 服务器。

**`<form>`** 元素用于创建表单

- `action` 属性定义了在提交表单时，应该把所收集的数据送给谁（URL）去处理。
- `method` 属性定义了发送数据的 HTTP 方法（通常是 `get` 或 `post`）。

**`<label>`** 元素用于为表单元素添加标签，提高可访问性。

- 将文本标签与输入元素绑定，扩大可点击区域
- 帮助屏幕阅读器识别表单字段含义
- 错误提示时自动关联标签文本
- 明确标识表单字段用途，利于SEO和代码可维护性

```html
<!-- 显式关联（推荐） -->
<label for="username">用户名：</label>
<input type="text" id="username" name="username">
<!-- 包裹表单控件实现自动关联 -->
<label>
  密码：
  <input type="password" name="password">
</label>
```

**`<input>`** 元素是最常用的表单元素之一，它可以创建文本输入框、密码框、单选按钮、复选框等。

- `type` 属性定义了输入框的类型
- `id` 属性用于关联 `<label>` 元素
- `name` 属性元素的名称用于标识表单字段
- value 元素的初始值

text、password、hidden
checkbox checked
radio
datetime-local
image图像按钮（image button）控件渲染的方式与 `<img>` 几乎完全相同。只是在用户点击它时，图像按钮的行为与提交（submit）按钮相同。
file被接受的文件类型可以使用 accept 属性来约束。此外，如果你想让用户选择多个文件，那么可以通过添加 multiple 属性来实现。

即使指定了multiple，但是当拍照是依旧只能上传一张图片
可以通过 JavaScript 动态添加文件输入框：

```html
<div id="fileInputs">
    <input type="file" name="photos[]" accept="image/*" capture="environment">
</div>
<button type="button" id="addMore">添加更多照片</button>

<script>
    document.getElementById('addMore').addEventListener('click', function () {
        const fileInputs = document.getElementById('fileInputs');
        const newInput = document.createElement('input');
        newInput.type = 'file';
        newInput.name = 'photos[]';
        newInput.accept = 'image/*';
        newInput.setAttribute('capture', 'environment');
        fileInputs.appendChild(newInput);
    });
</script>
```

如果需要更高级的功能（例如连续拍摄多张照片），可以使用 JavaScript 的第三方库或插件，例如：FilePond/Dropzone.js

```html
<!DOCTYPE html>
<html>
    <head>
        <title>FilePond from CDN</title>

        <!-- 引入 FilePond 的样式表，用于美化文件上传控件 -->
        <link href="https://unpkg.com/filepond/dist/filepond.css" rel="stylesheet" />
    </head>
    <body>
        <!-- 定义文件上传输入框，稍后会被 FilePond 转换为现代化控件 -->
        <input type="file" class="filepond" multiple/>

        <!-- 引入 FilePond 的 JavaScript 库 -->
        <script src="https://unpkg.com/filepond/dist/filepond.js"></script>

        <!-- 初始化 FilePond，将页面中所有带有 filepond 类的输入框转换为 FilePond 控件 -->
        <script>
            FilePond.parse(document.body);
        </script>
    </body>
</html>
```

input file的accept属性可以指定文件类型：
指定具体的文件类型 `accept='.png, .jpeg, .jpg, .webp'`
接收jpeg和png图像文件 `accept='image/jepg, image/png'`
接收所有图像类型 `accept='image/*'`
(`accept="image/png"` (MIME类型)；`accept=".png"` (文件扩展名)，按扩展名过滤，可能漏检伪装文件)
前端限制只是用户体验优化，服务器验证必不可少

`accept="image/*"` 是用来限制文件选择器只接受图片文件的，同时在移动设备上会触发调用相机的功能。
`<input type="file" name="photo" accept="image/*" capture="environment">`

- **`capture="environment"`**：指定使用后置摄像头。
- **`capture="user"`**：指定使用前置摄像头（自拍）。

只使用一个文件输入框，同时允许调用相机和上传其他文件
`<input type="file" name="file" accept="image/*,.pdf,.doc,.docx,.txt" capture="environment">`
调用相机的行为可能因设备和浏览器的实现而异

通过 JavaScript 动态切换文件输入框的 `accept` 属性，用户可以选择调用相机或上传其他文件。

```html
        <label for="fileType">选择文件类型:</label>
        <select id="fileType">
            <option value="image">拍摄照片</option>
            <option value="other">上传其他文件</option>
        </select>

        <input type="file" id="fileInput">

        <script>
            const fileType = document.getElementById('fileType');
            const fileInput = document.getElementById('fileInput');

            fileType.addEventListener('change', () => {
                if (fileType.value === 'image') {
                    fileInput.setAttribute('accept', 'image/*');
                    fileInput.setAttribute('capture', 'environment');
                } else {
                    fileInput.removeAttribute('capture');
                    fileInput.setAttribute('accept', '.pdf,.doc,.docx,.txt,.jpg,.png');
                }
            });
        </script>
```

`<textarea>`多行文本字段

**`<select>`** 元素用于创建下拉列表，而 **`<option>`** 元素用于定义下拉列表中的选项。

**`<button>`** 按钮，让用户在填写完表单后发送他们的数据。

- `type`属性
  - `submit`（默认值）：发送表单的数据到 `<form>`元素的 `action` 属性所定义的网页。
  - `button`：不会发生任何事。用于提供JavaScript 构建定制按钮。
  - `reset`：将所有表单小部件重新设置为它们的默认值。从用户体验的角度来看，这被认为是一种糟糕的做法。

对于普通的按钮实现跳转可以：使用onclick属性、javascript事件、`<a>`标签嵌套
`<button type='button' onclick="window.location.href='http://www.example.com'">点击跳转</button>`

`<button type="submit">` 或 `<input type="submit">` 的跳转行为可以：
使用表单的 `action` 属性（纯HTML）+后端重定向
(不指定action属性值，则浏览器会默认将请求提交给当前地址栏的url处理)
JavaScript动态跳转
直接使用一个div嵌套一个button和一个a

防止用户多次提交：（确保在 `<form>` 元素加载后运行）

```html
<script>
    document.addEventListener('DOMContentLoaded', function () {
        const form = document.querySelector('form');
        const submitButtons = form.querySelectorAll('button[type="submit"]');

        form.addEventListener('submit', function (event) {
            // 禁用所有提交按钮并显示提示
            submitButtons.forEach(button => {
                button.disabled = true;
                button.textContent = 'Submitting...';
            });
        });
    });
</script>
```

#### 字符实体

在 HTML 中某些字符是预留的，如不能使用小于号（<）和大于号（>），这是因为浏览器会误认为它们是标签
如果希望正确地显示预留字符，我们必须在 HTML 源代码中使用字符实体（character entities）

| 显示结果 | 描述        | 实体名称              | 实体编号    |
| -------- | ----------- | --------------------- | ----------- |
|          | 空格        | `&nbsp;`            | `&#160;`  |
| <        | 小于号      | `&lt;`              | `&#60;`   |
| >        | 大于号      | `&gt;`              | `&#62;`   |
| &        | 和号        | `&amp;`             | `&#38;`   |
| "        | 引号        | `&quot;`            | `&#34;`   |
| '        | 撇号        | `&apos;` (IE不支持) | `&#39;`   |
| ￠       | 分          | `&cent;`            | `&#162;`  |
| £       | 镑          | `&pound;`           | `&#163;`  |
| ¥       | 人民币/日元 | `&yen;`             | `&#165;`  |
| €       | 欧元        | `&euro;`            | `&#8364;` |
| §       | 小节        | `&sect;`            | `&#167;`  |
| ©       | 版权        | `&copy;`            | `&#169;`  |
| ®       | 注册商标    | `&reg;`             | `&#174;`  |
| ™       | 商标        | `&trade;`           | `&#8482;` |
| ×       | 乘号        | `&times;`           | `&#215;`  |
| ÷       | 除号        | `&divide;`          | `&#247;`  |

实体名称与实体编号都可以使用，区别在于实体名称方便记忆、实体编号兼容性好

#### 标签全局属性

| 属性             | 描述                                                       |
| :--------------- | :--------------------------------------------------------- |
| accesskey        | 设置访问元素的键盘快捷键                                   |
| **class**  | 一个元素可以有很多类，用空格隔开 可以方便找到这些元素      |
| contenteditable  | 规定是否可编辑元素的内容                                   |
| contextmenu      | 指定一个元素的上下文菜单。当用户右击该元素，出现上下文菜单 |
| data-*           | 自定义属性 H5规范以 `date-`开头                          |
| dir              | 设置元素中内容的文本方向                                   |
| draggable        | 指定某个元素是否可以拖动                                   |
| dropzone         | 指定是否将数据复制，移动，或链接，或删除                   |
| **hidden** | hidden 属性规定对元素进行隐藏                              |
| **id**     | 每个元素只能有一个id，且id不能重复 可以方便找到该元素      |
| lang             | 设置元素中内容的语言代码                                   |
| spellcheck       | 检测元素是否拼写错误                                       |
| **style**  | 规定元素的行内样式（inline style）                         |
| tabindex         | 设置元素的 Tab 键控制次序                                  |
| title            | 规定元素的额外信息（可在工具提示中显示）                   |
| translate        | 指定是否一个元素的值在页面载入时是否需要翻译               |

##### 拖动元素

#### HTML5 SVG

SVG 是一种使用 XML 描述 2D 图形的语言，全称是可缩放矢量图（Scalable Vector Graphics）。其他图像格式都是基于像素处理的，SVG 则是属于对图像的形状描述，所以它本质上是文本文件，体积较小，且不管放大多少倍都不会失真。此外SVG 是万维网联盟的标准，SVG 与诸如 DOM 和 XSL 之类的 W3C 标准是一个整体。

SVG 基于 XML，这意味着 SVG DOM 中的每个元素都是可用的。您可以为某个元素附加 JavaScript 事件处理器。在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

SVG 代码直接写在标签 `<svg>`之中

> width 和 height 属性可设置此 SVG 文档的宽度和高度。version 属性可定义所使用的 SVG 版本，xmlns 属性可定义 SVG 命名空间。

SVG 代码也可以写在一个以.svg结尾的文件中，然后用 `<img>`、`<object>`、`<embed>`、`<iframe>`等标签插入网页。

SVG有一些预定义的形状元素，可被开发者使用和操作：

- 矩形 `<rect>`
- 圆形 `<circle>`
- 椭圆 `<ellipse>`
- 线 `<line>`
- 折线 `<polyline>`
- 多边形 `<polygon>`
- 路径 `<path>`

```svg
    <svg width="16" height="16">
        <circle cx="6" cy="6" r="6"
        style="fill:red"/>
        <circle cx="6" cy="6" r="4"
        style="fill:white"/>
        <rect x="13" y="-2" width="6" height="2"
        style="fill:red; transform: rotate(55deg)"/>
    </svg>
```

##### 矩形rect

```svg
    <svg>
        <rect x="50" y="20" rx="20" ry="20" width="100" height="50"
        style="fill:rgb(255,0,0);stroke-width:1px;stroke:rgb(0,0,0)"/>
    </svg>
```

- **width 和 height 属性可定义矩形的高度和宽度**
- x 属性定义矩形的左侧位置 y 属性定义矩形的顶端位置（例如，x="0" 定义矩形到浏览器窗口顶端的距离是 0px）
- rx 和 ry 属性可使矩形产生圆角
- style 属性用来定义 CSS 属性，常见的有：
  - **fill 属性定义矩形的填充颜色**
  - fill-opacity 属性定义填充颜色透明度(也可以使用RGBA、8位HEX、HSLA)
  - stroke 属性定义一条线，文本或元素轮廓颜色
  - stroke-width 属性定义了一条线，文本或元素轮廓厚度
  - stroke-linecap 定义不同类型的开放路径的终结(butt/round/square)
  - stroke-dasharray 用于创建虚线
    `stroke-dasharray="20,10,5,5,5,10"`表示20px线、10px空白、5px线...以此类推
  - stroke-opacity 属性定义轮廓颜色的透明度(也可以使用RGBA、8位HEX、HSLA)
  - opacity 属性用于定义了元素的透明度

##### 圆形circle

```svg
    <svg>
        <circle cx="100" cy="50" r="40"
        style="fill:red"/>
    </svg>
```

- **cx和cy属性定义圆点的x和y坐标**。如果省略cx和cy，圆的中心会被设置为(0, 0)
- **r属性定义圆的半径**

##### 椭圆ellipse

```svg
    <svg>
        <ellipse cx="100" cy="80" rx="100" ry="50"
        style="fill:yellow;"/>
    </svg>
```

- CX属性定义的椭圆中心的x坐标
- CY属性定义的椭圆中心的y坐标
- RX属性定义的水平半径
- RY属性定义的垂直半径

##### 直线line

```svg
    <svg>
        <line x1="0" y1="0" x2="200" y2="200"
        style="stroke:rgb(255,0,0);stroke-width:2"/>
    </svg>
```

- x1 属性在 x 轴定义线条的开始
- y1 属性在 y 轴定义线条的开始
- x2 属性在 x 轴定义线条的结束
- y2 属性在 y 轴定义线条的结束

##### 多边形polygon

```svg
    <svg>
        <polygon points="200,10 250,100 160,120"
        style="fill:lime;"/>
    </svg>
```

- points 属性定义多边形每个角的 x 和 y 坐标

##### 多段线polyline

```svg
    <svg>
        <polyline points="20,20 40,25 60,40 80,120 120,140"
        style="fill:none;stroke:red;stroke-width:3" />
    </svg>
```

- points 属性定义多段线顶点的 x 和 y 坐标

##### 路径path

path 元素的形状是通过属性 `d` 定义的，属性 `d`的值是一个“命令 + 参数”的序列
因为属性 d采用的是用户坐标系统，所以不需标明单位

- M = moveto(移至 移动画笔不画线)  `M x y`
- L = lineto(连线到) `L x y`
- H = horizontal lineto(水平线到) `H x`
- V = vertical lineto(垂直线) `V y`
- C = curveto(三次贝塞尔曲线) `C x1 y1, x2 y2, x y`
  (x,y)表示曲线的终点(x1,y1)是起点的控制点，(x2,y2)是终点的控制点
- S = smooth curveto(简写的三次贝塞尔曲线命令) `S x2 y2, x y`
  通常情况下，一个点某一侧的控制点是它另一侧的控制点的对称（以保持斜率不变）。这样，你可以使用一个简写的贝塞尔曲线命令 S
  如果 S 命令跟在一个 C 或 S 命令后面，则它的第一个控制点会被假设成前一个命令曲线的第二个控制点的中心对称点。如果 S 命令单独使用，前面没有 C 或 S 命令，那当前点将作为第一个控制点。
- Q = quadratic Bézier curve(二次贝塞尔曲线) `Q x1 y1, x y`
- T = smooth quadratic Bézier curveto(简写的二次贝塞尔曲线命令) `T x y`
  快捷命令 T 会通过前一个控制点，推断出一个新的控制点。这意味着，在你的第一个控制点后面，可以只定义终点，就创建出一个相当复杂的曲线。需要注意的是，T 命令前面必须是一个 Q 命令，或者是另一个 T 命令，才能达到这种效果。如果 T 单独使用，那么控制点就会被认为和终点是同一个点，所以画出来的将是一条直线。
- A = elliptical Arc(椭圆弧)  `A rx ry x-axis-rotation large-arc-flag sweep-flag x y`
  A 的前两个参数分别是 x 轴半径和 y 轴半径 第三个参数表示弧形x 轴旋转角度
  large-arc-flag（角度大小）和 sweep-flag（弧线方向），large-arc-flag 决定弧线是大于还是小于 180 度，0 表示小角度弧，1 表示大角度弧。sweep-flag 表示弧线的方向，0 表示从起点到终点沿逆时针画弧，1 表示从起点到终点沿顺时针画弧
  最后两个参数是指定弧形的终点
- Z = closepath(闭合路径) `Z`

**注意：** 以上所有命令均允许小写字母。大写表示绝对定位，小写表示相对定位(相对上一步的位置)。

路径理论上可以绘制所有图形，但是由于在绘制路径时的复杂性，简单的图形可以使用定义的形状元素；复杂的图形可以使用SVG编辑器来创建

```svg
    <svg>
        <path d="M150 10 L75 200 L225 200 Z" 
        style="fill: aqua;"/>
    </svg>
```

##### 文本text

##### 滤镜

SVG滤镜用来增加对SVG图形的特殊效果

SVG滤镜定义在 `<defs>`元素中。`<defs>`元素定义短并含有特殊元素（如滤镜）定义。`<filter>`标签用来定义SVG滤镜。`<filter>`标签使用必需的id属性来定义向图形应用哪个滤镜

##### 实现SVG动画

一、使用 CSS 实现 SVG 动画
通过CSS的 @keyframes 和过渡属性直接控制SVG元素的样式变化。

```html
<!DOCTYPE html>
<html>
<head>
<style>
/* 容器统一管理 */
.svg-container {
  display: inline-block;
  margin: 50px;
  background: #f0f0f0; /* 添加背景便于观察旋转 */
  border-radius: 10px;
  padding: 20px;
}

/* 环形旋转动画增强 */
.ring {
  transition: transform 0.6s cubic-bezier(0.68, -0.55, 0.27, 1.55); /* 弹性缓动 */
  transform-origin: center;
}
.svg-container:hover .ring {
  transform: rotate(360deg); /* 悬停时完全旋转一圈 */
  filter: drop-shadow(0 0 5px rgba(0,0,0,0.3)); /* 添加投影增强动感 */
}

/* 心跳动画优化 */
@keyframes heartbeat {
  0% { transform: scale(1); opacity: 0.9; }
  50% { transform: scale(1.15); opacity: 1; }
  100% { transform: scale(1); opacity: 0.9; }
}
.heart {
  animation: heartbeat 1.2s infinite;
  transform-origin: center;
  cursor: pointer;
}
</style>
</head>
<body>

<!-- 环形旋转组件 -->
<div class="svg-container">
  <svg width="120" height="120" viewBox="0 0 100 100">
    <!-- 外环 -->
    <circle class="ring" cx="50" cy="50" r="45" 
            fill="none" stroke="#2196F3" stroke-width="6"
            stroke-dasharray="5 3"/> <!-- 虚线增强旋转辨识度 -->
    <!-- 内环 -->
    <circle cx="50" cy="50" r="30" 
            fill="none" stroke="#2196F3" stroke-width="3"/>
    <!-- 中心点标记 -->
    <circle cx="50" cy="50" r="3" fill="#2196F3"/>
  </svg>
</div>

<!-- 心跳组件 -->
<div class="svg-container">
  <svg width="120" height="120" viewBox="0 0 24 24">
    <path class="heart" fill="#e91e63" 
          d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
  </svg>
</div>

</body>
</html>
```

二、使用 SMIL 动画（原生SVG动画）
通过 `<animate>` 标签直接在SVG内部定义动画效果。

```html
<svg width="200" height="200" viewBox="0 0 100 100">
  <!-- 线条加载动画 -->
  <line x1="10" y1="50" x2="90" y2="50" stroke="blue" stroke-width="4">
    <animate attributeName="x2" from="10" to="90" dur="1s" repeatCount="indefinite"/>
  </line>

  <!-- 颜色渐变球体 -->
  <circle cx="50" cy="30" r="15" fill="orange">
    <animate attributeName="fill" values="orange;red;orange" dur="2s" repeatCount="indefinite"/>
  </circle>
</svg>
```

三、使用 JavaScript 动态控制
通过JavaScript操作SVG DOM元素实现复杂交互。

```html
<svg id="interactive-svg" width="200" height="200" viewBox="0 0 100 100">
  <rect id="dragRect" x="10" y="10" width="80" height="80" fill="green"/>
</svg>

<script>
const rect = document.getElementById('dragRect');
let isDragging = false;

// 鼠标拖拽动画
rect.addEventListener('mousedown', () => isDragging = true);
document.addEventListener('mouseup', () => isDragging = false);
document.addEventListener('mousemove', (e) => {
  if (!isDragging) return;
  const svg = document.getElementById('interactive-svg');
  const pt = svg.createSVGPoint();
  pt.x = e.clientX;
  pt.y = e.clientY;
  const cursorPos = pt.matrixTransform(svg.getScreenCTM().inverse());
  rect.setAttribute('x', cursorPos.x - 40);
  rect.setAttribute('y', cursorPos.y - 40);
});
</script>
```

#### HTML5 Canvas

HTML5 canvas 元素用于图形的绘制，通过脚本 (通常是JavaScript)来完成.`<canvas>` 标签只是图形容器，您必须使用脚本来绘制图形。

Canvas 是逐像素进行渲染的。在 canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。

#### HTML5 MathML

每个 MathML 公式都由一个根元素 `math`表示，其可以直接嵌入到 HTML 网页中。默认情况下，公式将被内联渲染，并进行额外的调整以将其高度最小化。可以使用 `display="block"` 属性，以在独立的段落中渲染复杂的公式。

```html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="UTF-8" />
    <title>HTML5 中的 MathML</title>
  </head>
  <body>
    <p>
      一分之根号二（行内样式）：
      <math>
        <mfrac>
          <mn>1</mn>
          <msqrt>
            <mn>2</mn>
          </msqrt>
        </mfrac>
      </math>
    </p>

    <p>
      一分之根号二（展示样式）：
      <math display="block">
        <mfrac>
          <mn>1</mn>
          <msqrt>
            <mn>2</mn>
          </msqrt>
        </mfrac>
      </math>
    </p>
  </body>
</html>
```

建议为不支持 MathML 的浏览器提供一个回退机制。如果你的文档仅包含基本的数学公式，那么一个 mathml.css 样式表可能就够了。要按条件加载它，只需要在文档的 head 中插入一行：
`<script src="https://fred-wang.github.io/mathml.css/mspace.js"></script`>`如果你需要更多复杂的结构，你需要考虑使用功能更全面一些的 MathJax 库作为一个 MathML polyfill：<script src="https://fred-wang.github.io/mathjax.js/mpadded-min.js">``</script>或者，对于没有很好地支持 MathML 的浏览器，你也可以只在网页的顶部显示一条警告，并让用户在不同的回退方案中自主选择：``<script src="https://fred-wang.github.io/mathml-warning.js/mpadded-min.js"></script>``

##### Latex转换为 MathML

把轻量级标记语言（如流行的 Latex 语言）转换为 MathML

客户端转换：

```html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="UTF-8" />
    <title>HTML5 中的 MathML</title>
    <script src="https://fred-wang.github.io/TeXZilla/TeXZilla-min.js"></script>
    <script src="https://fred-wang.github.io/TeXZilla/examples/customElement.js"></script>
  </head>
  <body>
    <p>
      一分之根号二（行内样式）：
      <la-tex>\frac{1}{\sqrt{2}}</la-tex>
    </p>

    <p>
      一分之根号二（展示样式）：
      <la-tex display="block">\frac{1}{\sqrt{2}}</la-tex>
    </p>
  </body>
</html>
```

命令行转换：
选择命令行程序，而不是在网页加载时再生成 MathML 表达式。这样，网页中将包含静态的 MathML 内容，加载速度也会更快。

```html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="UTF-8" />
    <title>HTML5 中的 MathML</title>
  </head>
  <body>
    <p>一分之根号二（行内样式）：$\frac{1}{\sqrt{2}}$</p>

    <p>一分之根号二（展示样式）：$$\frac{1}{\sqrt{2}}$$</p>
  </body>
</html>
```

利用 Node.js 和 TeXZilla 完成转换：

```shell
cat input.html | node TeXZilla.js streamfilter > output.html
```

#### permission

```html

<permission type="camera" />
<script>
  const permission = document.querySelector('permission');
  permission.addEventListener('promptdismiss', showCameraWarning);
 
  function showCameraWarning() {
    // Show warning that the app isn't fully usable
    // unless the camera permission is granted.
  }
 
  const permissionStatus = await navigator.permissions.query({name: "camera"});
  permissionStatus.addEventListener('change', () => {
    // Run the check when the status changes.
    if (permissionStatus.state === "granted") {
      useCamera();
    }
    // Run the initial check.
    if (permissionStatus.state === "granted") {
      useCamera();
    }
  });

```

## CSS

CSS(Cascading Style Sheets，层叠样式表)，是一种用来为结构化文档（如 HTML 文档或 XML 应用）添加样式（字体、间距和颜色等）的计算机语言，CSS 文件扩展名为 `.css`

CSS 规则由两个主要的部分构成：选择器、声明。
选择器通常是您需要改变样式的 HTML 元素。每条声明由一个属性和一个值组成。属性（property）是您希望设置的样式属性（style attribute）。每个属性有一个值。属性和值被冒号分开。CSS声明总是以分号 `;` 结束，声明总以大括号 `{}` 括起来。
注释是用来解释你的代码，并且可以随意编辑它，浏览器会忽略它。CSS注释以 `/*` 开始, 以 `*/` 结束

```css
/*这是个注释*/
p {
/*这是个注释*/
    color:red;
    text-align:center;
}
```

**插入样式表**的方法有三种:
外部样式表(External style sheet)使用 `<link>` 标签链接到样式表，`<link>` 标签在文档头部

```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

内部样式表(Internal style sheet)使用 `<style>` 标签在文档头部定义内部样式表

```html
<head>
<style>
    hr {
        color:sienna;
    }
    p {
        margin-left:20px;
    }
    body {
        background-image:url("images/back40.gif");
    }
</style>
</head>
```

内联样式(Inline style)由于要将表现和内容混杂在一起，内联样式会损失掉样式表的许多优势。请慎用这种方法，例如当样式仅需要在一个元素上应用一次时。要使用内联样式，你需要在相关的标签内使用样式（style）属性。Style 属性可以包含任何 CSS 属性。

```html
<p style="color:sienna;margin-left:20px">这是一个段落。</p>
```

所有 HTML 元素都可以视为方框。CSS 框模型实质上是一个包围每个 HTML 元素的框(盒子)。它包括：外边距、边框、内边距以及实际的内容。

---

**如果一个元素的同一属性进行了两次声明，优先级高的声明覆盖低的，如果优先级一样那么后面的声明会覆盖前面的声明**，优先级：

1. 行内样式 - 行内（内联）样式直接附加到要设置样式的元素。实例：`<h1 style="color: #ffffff;">`。
2. ID - ID 是页面元素的唯一标识符，例如 `#navbar`。
3. 类、属性和伪类 - 此类别包括 `.classes`、`[attributes]` 和伪类，例如：`:hover`、`:focus` 等。
4. 元素和伪元素 - 此类别包括元素名称和伪元素，比如 `h1`、`div`、`:before` 和 `:after`。
5. 通用选择器 - `*`

`!important` 规则用于增加样式的权重，使用一个 !important 规则时，此声明将覆盖任何其他声明:

```css
#adblock {
    display: none !important;
}
```

使用 !important 是一个坏习惯，应该尽量避免，因为这破坏了样式表中的固有的级联规则 使得调试找 bug 变得更加困难了。
当两条相互冲突的带有 !important 规则的声明被应用到相同的元素上时，拥有更大优先级的声明将会被采用。

### 常见属性值

#### 颜色

**RGB颜色**：`rgb(red, green, blue)` 每个参数 (red、green 以及 blue) 定义了 0 到 255 之间的颜色强度。

**HEX颜色**：`#rrggbb` 和RGB的原理差不多，都是用Red, Green, Blue相混合所产生的颜色，只不过换成了十六进制。

**HSL颜色**：`hsl(hue, saturation, lightness)` 可以使用色相、饱和度和明度来指定颜色。
色相（hue）是色轮上从 0 到 360 的度数。0 是红色，120 是绿色，240 是蓝色。饱和度（saturation）是一个百分比值，0％ 表示灰色阴影，而 100％ 是全色。亮度（lightness）也是百分比，0％ 是黑色，50％ 是既不明也不暗，100％是白色。

以粉色为例：

1. `pink` 常见颜色可以直接用英文名表示
2. `rgb(255, 192, 203)` RGB表示，指R255份、G192份、B203份
3. `#FFC0CB` 255的16进制为FF；192的16进制为C0；203的16进制为CB
4. `hsl(350, 100.0%, 87.6%)` 色相350°，饱和度100.0%，亮度87.6%

除此之外，还支持RGBA、8位HEX、HSLA。多的值为alpha值，制订了色彩的透明度，它的范围为0%到100%之间
如：
`rgba(255, 192, 203, 50%)`透明度为50%
`#FFC0CB80`80为255*50%的16进制表示取整，指透明度50%
`hsla(350, 100.0%, 87.6%, 50%)`透明度为50%

透明效果可以使用*transparent*或者任意颜色指定透明度为*100%*

#### 长度单位

一些设置 CSS 长度的属性有 width, margin, padding, font-size, border-width,等。
长度有一个数字和单位组成如 10px, 2em等。数字与单位之间不能出现空格。如果长度值为 0，则可以省略单位。
对于一些 CSS 属性，长度可以是负数
最常用的单位是**px**、**%**

**绝对长度单位**：

| 单位         | 描述                                     |
| ------------ | ---------------------------------------- |
| cm           | 厘米                                     |
| mm           | 毫米                                     |
| in           | 英寸 (1in = 96px = 2.54cm)               |
| **px** | 像素 (1px = 1/96th of 1in)               |
| pt           | point，大约1/72英寸； (1pt = 1/72in)     |
| pc           | pica，大约 12pt，1/6英寸； (1pc = 12 pt) |

相对长度单位：

| 单位        | 描述                                                                                          |
| ----------- | --------------------------------------------------------------------------------------------- |
| em          | 相对于应用在当前元素的字体尺寸。一般浏览器字体大小默认为16px，则2em == 32px                   |
| ex          | 依赖于英文字母小 x 的高度                                                                     |
| ch          | 数字 0 的宽度                                                                                 |
| rem         | rem(root em)作用于非根元素时，相对于根元素字体大小 作用于根元素字体大小时，相对于初始字体大小 |
| vw          | Viewport Width，视窗宽度，1vw=视窗宽度的1%                                                    |
| vh          | Viewport Height，视窗高度，1vh=视窗高度的1%                                                   |
| vmin        | vw和vh中较小的那个                                                                            |
| vmax        | vw和vh中较大的那个                                                                            |
| **%** | 相对父元素的百分比值                                                                          |

### CSS选择器

1. 元素选择器 `element` 可以用 `ele1, ele2, ...`形式选取所有具有相同样式定义的HTML元素
2. id 选择器 `#id`
3. CSS 类选择器 `.class` 还可以指定只有特定的HTML元素会受类的影响 `element.class`
4. 通用选择器 `*`选择页面上的所有的 HTML 元素

#### CSS 组合器

可以将CSS选择器组合到一起

- 后代选择器 (空格) 匹配属于指定元素后代的所有元素
- 子选择器 (>) 匹配属于指定元素子元素的所有元素
- 相邻兄弟选择器 (+) 匹配所有作为指定元素之后的同级的元素
- 通用兄弟选择器 (~) 匹配属于指定元素的同级元素的所有元素

```css
        #box>div {
            background-color: red;
        }
```

#### 伪类

伪类用于定义元素的特殊状态

| 选择器               | 实例                  | 实例描述                                                               |
| -------------------- | --------------------- | ---------------------------------------------------------------------- |
| :active              | a:active              | 选择活动的链接。                                                       |
| :checked             | input:checked         | 选择每个被选中的 `<input>` 元素。                                    |
| :disabled            | input:disabled        | 选择每个被禁用的 `<input>` 元素。                                    |
| :empty               | p:empty               | 选择没有子元素的每个 `<p>` 元素。                                    |
| :enabled             | input:enabled         | 选择每个已启用的 `<input>` 元素。                                    |
| :first-child         | p:first-child         | 选择作为其父的首个子元素的每个 `<p>` 元素。                          |
| :first-of-type       | p:first-of-type       | 选择作为其父的首个 `<p>` 元素的每个 `<p>` 元素。                   |
| :focus               | input:focus           | 选择获得焦点的 `<input>` 元素。                                      |
| :hover               | a:hover               | 选择鼠标悬停其上的链接。                                               |
| :in-range            | input:in-range        | 选择具有指定范围内的值的 `<input>` 元素。                            |
| :invalid             | input:invalid         | 选择所有具有无效值的 `<input>` 元素。                                |
| :lang(*language* ) | p:lang(it)            | 选择每个 lang 属性值以 "it" 开头的 `<p>` 元素。                      |
| :last-child          | p:last-child          | 选择作为其父的最后一个子元素的每个 `<p>` 元素。                      |
| :last-of-type        | p:last-of-type        | 选择作为其父的最后一个 `<p>` 元素的每个 `<p>` 元素。               |
| :link                | a:link                | 选择所有未被访问的链接。                                               |
| :not(selector)       | :not(p)               | 选择每个非 `<p>` 元素的元素。                                        |
| :nth-child(n)        | p:nth-child(2)        | 选择作为其父的第二个子元素的每个 `<p>` 元素。                        |
| :nth-last-child(n)   | p:nth-last-child(2)   | 选择作为父的第二个子元素的每个 `<p>`元素，从最后一个子元素计数。     |
| :nth-last-of-type(n) | p:nth-last-of-type(2) | 选择作为父的第二个 `<p>`元素的每个 `<p>`元素，从最后一个子元素计数 |
| :nth-of-type(n)      | p:nth-of-type(2)      | 选择作为其父的第二个 `<p>` 元素的每个 `<p>` 元素。                 |
| :only-of-type        | p:only-of-type        | 选择作为其父的唯一 `<p>` 元素的每个 `<p>` 元素。                   |
| :only-child          | p:only-child          | 选择作为其父的唯一子元素的 `<p>` 元素。                              |
| :optional            | input:optional        | 选择不带 "required" 属性的 `<input>` 元素。                          |
| :out-of-range        | input:out-of-range    | 选择值在指定范围之外的 `<input>` 元素。                              |
| :read-only           | input:read-only       | 选择指定了 "readonly" 属性的 `<input>` 元素。                        |
| :read-write          | input:read-write      | 选择不带 "readonly" 属性的 `<input>` 元素。                          |
| :required            | input:required        | 选择指定了 "required" 属性的 `<input>` 元素。                        |
| :root                | root                  | 选择元素的根元素。                                                     |
| :target              | #news:target          | 选择当前活动的 #news 元素（单击包含该锚名称的 URL）。                  |
| :valid               | input:valid           | 选择所有具有有效值的 `<input>` 元素。                                |
| :visited             | a:visited             | 选择所有已访问的链接。                                                 |

*像:hover也可以用js绑定事件修改样式，不过如果仅需要修改样式使用伪类更方便*.

#### 伪元素

CSS 伪元素用于设置元素指定部分的样式

| 选择器         | 实例            | 实例描述                          |
| -------------- | --------------- | --------------------------------- |
| ::after        | p::after        | 在每个 `<p>` 元素之后插入内容。 |
| ::before       | p::before       | 在每个 `<p>` 元素之前插入内容。 |
| ::first-letter | p::first-letter | 选择每个 `<p>` 元素的首字母。   |
| ::first-line   | p::first-line   | 选择每个 `<p>` 元素的首行。     |
| ::selection    | p::selection    | 选择用户选择的元素部分。          |

#### 属性选择器

为带有特定属性的 HTML 元素设置样式

| 选择器                  | 实例                 | 实例描述                                                    |
| ----------------------- | -------------------- | ----------------------------------------------------------- |
| [attribute]             | [target]             | 选择带有 target 属性的所有元素。                            |
| [attribute=value]       | [target=_blank]      | 选择带有 target="_blank" 属性的所有元素。                   |
| [attribute~=value]      | [title~=flower]      | 选择带有包含 "flower" 一词的 title 属性的所有元素。         |
| [attribute&#124;=value] | [lang=en]            | 选择带有以 "en" 开头的 lang 属性的所有元素。                |
| [attribute^=value]      | a[href^="https"]     | 选择其 href 属性值以 "https" 开头的每个 `<a>` 元素。      |
| [attribute&#38;=value]  | a[href&#38;=".pdf"]  | 选择其 href 属性值以 ".pdf" 结尾的每个 `<a>` 元素。       |
| [attribute*=value]      | a[href*="w3schools"] | 选择其 href 属性值包含子串 "w3school" 的每个 `<a>` 元素。 |

### 声明

#### 背景(background)

1. **`background-color`** 指定元素的背景色；对于元素的透明度：
   - 使用opacity属性指定，注意所有子元素都继承透明度
   - 使用RGBA、8位HEX、HSLA指定透明度
2. **`background-image`** 指定用作元素背景的图像，默认情况下图像会重复以覆盖整个元素
3. **`background-repeat`** 默认情况下，`background-image` 属性在水平和垂直方向上都重复图像
   - 图像仅在水平方向重复 `background-repeat: repeat-x;`
   - 垂直重复图像 `background-repeat: repeat-y;`
   - 只显示一次背景图像 `background-repeat: no-repeat;`
4. **`background-attachment`** 指定背景图像是应该滚动还是固定的（会不会随页面的其余部分一起滚动）
   - 固定背景图像 `background-attachment: fixed;`
   - 背景图像应随页面的其余部分一起滚动 `background-attachment: scroll;`
5. **`background-position`** 指定背景图像的位置 如 `background-position: right top;`把背景图片放在右上角
6. **`background-size`** 指定背景图像的大小 默认 `background-size: auto;`背景图像将以其原始大小显示
   - `background-size: 100px 100px;`设置背景图片高度和宽度。第一个值设置宽度，第二个值设置的高度。如果只给出一个值，第二个是设置为auto
   - `background-size: 100% 100%;`将计算相对于背景定位区域的百分比。第一个值设置宽度，第二个值设置的高度。如果只给出一个值，第二个是设置为 auto
   - `background-size: cover;`此时会保持图像的纵横比并将图像缩放成将完全覆盖背景定位区域的最小大小
   - `background-size: contain;`此时会保持图像的纵横比并将图像缩放成将适合背景定位区域的最大大小。

**`background`** 是一种CSS简写属性，用于一次性集中定义各种背景属性，包括 color, image, origin 与 size, repeat 方式等等。
将背景设为一张居中放大的图片：
`background: no-repeat center/80% url("../img/image.png");`

##### background-image属性(多重背景)

img标签是HTML的一部分，用于插入图片并占据页面上的空间。 而background-image是CSS样式，用于设置元素的背景图像，不占据页面上的空间。 作用效果上的区别：img元素可以被视为 文档 对象模型（DOM）的一部分，这意味着你可以通过JavaScript等编程语言来操作它，例如从文档中删除图片。 而background-image是CSS样式，无法通过编程语言来操作。

**渐变**

#### 外边距(margin)

#### 边框(border)

1. **`border-style`** 指定要显示的边框类型

   | 属性值 |                    样式                    |
   | :----: | :----------------------------------------: |
   | dotted |                  点线边框                  |
   | dashed |                  虚线边框                  |
   | solid |                  实线边框                  |
   | double |                   双边框                   |
   | groove |  3D 坡口边框。效果取决于 border-color 值  |
   | ridge |  3D 脊线边框。效果取决于 border-color 值  |
   | inset | 3D inset 边框。效果取决于 border-color 值 |
   | outset | 3D outset 边框。效果取决于 border-color 值 |
   |  none  |                   无边框                   |
   | hidden |                  隐藏边框                  |

   border-style 属性可以设置一到四个值（用于上边框、右边框、下边框和左边框）
2. **`border-width`** 属性指定四个边框的宽度
   可以将宽度设置为特定大小（以 px、pt、cm、em 计），也可以使用以下三个预定义值之一：thin(1px)、medium(3px) 或 thick(5px)
   border-width 属性可以设置一到四个值（用于上边框、右边框、下边框和左边框）
3. **`border-color`** 属性用于设置四个边框的颜色
   如果未设置 border-color ，则它将继承元素的颜色（如果省略边框颜色，则应用的颜色将是文本的颜色）
   border-color 属性可以设置一到四个值（用于上边框、右边框、下边框和左边框）
4. **`border-top`** **`border-right`** **`border-bottom`** **`border-left`** 可以更方便的指定边框的每个边，参数依次为width、style、color。也可以用 **`border-top-style`** 等分别指定样式
5. **`border`** 简写代码，依次为width、style、color，其中style为必要属性。
   默认值为 **2px none #000**

   | 特殊属性值 |          效果          |
   | :--------: | :--------------------: |
   |  initial  | 将此属性设置为其默认值 |
   |  inherit  |  从其父元素继承此属性  |
6. **`border-radius`** 属性用于向元素添加圆角边框 如 `border-radius: 12px;`12px为圆角大小；也可以 `border-radius: 50%;`

##### border-image属性(边框图像)

#### 内边距(padding)

#### 轮廓

轮廓是在元素周围绘制的一条线，在边框之外，以凸显元素。
轮廓是在元素边框之外绘制的，并且可能与其他内容重叠。同样，轮廓也不是元素尺寸的一部分；元素的总宽度和高度不受轮廓线宽度的影响。

#### 高度和宽度

#### Box Sizing属性(盒子大小)

默认情况下，元素的宽度和高度是这样计算的：
width + padding + border = 元素的实际宽度
height + padding + border = 元素的实际高度
这意味着：当您设置元素的宽度/高度时，该元素通常看起来比您设置的更大（因为元素的边框和内边距已被添加到元素的指定宽度/高度中）

如果在元素上设置了 `box-sizing: border-box`，则宽度和高度会包括内边距和边框
我们一般直接给所有元素设置该属性：

```css
* {
  box-sizing: border-box;
}
```

#### border-radius属性(圆角)

**border-radius** 属性定义元素的圆角半径

- **border-top-left-radius**
- **border-top-right-radius**
- **border-bottom-right-radius**
- **border-bottom-left-radius**

border-radius 属性是以上属性的简写属性
可以接受一到四个值：
四个值 - `border-radius: 15px 50px 30px 5px;`（依次分别用于：左上角、右上角、右下角、左下角）：
三个值 - `border-radius: 15px 50px 30px;`（第一个值用于左上角，第二个值用于右上角和左下角，第三个用于右下角）：
两个值 - `border-radius: 15px 50px;`（第一个值用于左上角和右下角，第二个值用于右上角和左下角）：
一个值 - `border-radius: 15px;`（该值用于所有四个角，圆角都是一样的）

#### 文本和字体

text-align：center；

阴影效果
文本效果:文本溢出、整字换行、换行规则以及书写模式
Web 字体@font-face 规则
Web安全字体组合

`overflow`：文字长度超出限定宽度，则隐藏超出的内容
`text-overflow`：规定当文本溢出时，显示省略符号来代表被修剪的文本
`white-space`：控制空白字符的显示，同时还能控制是否自动换行。
`word-break`: break-all 使一个单词能够在换行时进行拆分。

nowrap
white-space: pre-wrap;自动换行
word-break: break-all;在单词内部进行换行

#### 图标

#### html链接

#### html列表

#### html表格

#### html表单

#### display和visibility属性

```css
/* 预组合值 */
display: block;
display: inline;
display: inline-block;
display: flex;
display: inline-flex;
display: grid;
display: inline-grid;
display: flow-root;

/* 生成盒子 */
display: none;
display: contents;

/* 多关键字语法 */
display: block flex;
display: block flow;
display: block flow-root;
display: block grid;
display: inline flex;
display: inline flow;
display: inline flow-root;
display: inline grid;

/* 其他值 */
display: table;
display: table-row; /* 所有的 table 元素 都有等效的 CSS display 值 */
display: list-item;

/* 全局值 */
display: inherit;
display: initial;
display: revert;
display: revert-layer;
display: unset;
```

网格布局
网格引入了 fr 单位来帮助我们创建灵活的网格轨道。一个 fr 单位代表网格容器中可用空间的一等份。

将 display 属性设置为 grid 或 inline-grid 后，它就变成了一个网格容器，这个元素的所有直系子元素将成为网格元素。

通过 grid-template-columns 和 grid-template-rows 属性来定义网格中的列和行。

- grid-column-gap
- grid-row-gap
- grid-gap


margin-left: auto
margin-right: auto;

#### 定位

position 属性指定了元素的定位类型。
position 属性的五个值：

- static
  默认值，即没有定位，遵循正常的文档流对象
- relative
  相对定位元素的定位是相对其正常位置
- fixed
  固定位置，即使窗口是滚动的也不会移动
- absolute
  绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于 `<html>`
- sticky
  基于用户的滚动位置来定位。

| 属性                   | 说明           | 值                                                                                                                                                         |
| :------------------------------------------- | :------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| bottom                  | 定义了定位元素下外边距边界与其包含块下边界之间的偏移。     | auto`<br>`_length  `<br>`%  `<br>`_inherit                                                                                                                                                                                                                                       |
| clip                         | 剪辑一个绝对定位的元素                  | _shape`<br>`_auto  `<br>`inherit                                                                                                                                                                                                                                                   |
| cursor                  | 显示光标移动到指定的类型                                     | _url_  `<br>`auto  `<br>`crosshair  `<br>`default  `<br>`pointer  `<br>`move  `<br>`e-resize  `<br>`ne-resize  `<br>`nw-resize  `<br>`n-resize  `<br>`se-resize  `<br>`sw-resize  `<br>`s-resize  `<br>`w-resize  `<br>`text  `<br>`wait  `<br>`help |
| left                      | 定义了定位元素左外边距边界与其包含块左边界之间的偏移。       | auto`<br>`_length  `<br>`%  `<br>`_inherit                                                                                                                                                                                                                                       |
| overflow            | 设置当元素的内容溢出其区域时发生的事情。                     | auto`<br>`hidden  `<br>`scroll  `<br>`visible  `<br>`inherit                                                                                                                                                                                                                   |
| overflow-y      | 指定如何处理顶部/底部边缘的内容溢出元素的内容区域            | auto`<br>`hidden  `<br>`scroll  `<br>`visible  `<br>`no-display  `<br>`no-content                                                                                                                                                                                            |
| overflow-x | 指定如何处理右边/左边边缘的内容溢出元素的内容区域            | auto`<br>`hidden  `<br>`scroll  `<br>`visible  `<br>`no-display  `<br>`no-content                                                                                                                                                                                            |
| position          | 指定元素的定位类型                                           | absolute`<br>`fixed  `<br>`relative  `<br>`static  `<br>`inherit                                                                                                                                                                                                               |
| right                       | 定义了定位元素右外边距边界与其包含块右边界之间的偏移。       | auto`<br>`_length  `<br>`%  `<br>`_inherit                                                                                                                                                                                                                                       |
| top                         | 定义了一个定位元素的上外边距边界与其包含块上边界之间的偏移。 | auto`<br>`_length  `<br>`%  `<br>`_inherit                                                                                                                                                                                                                                       |
| z-index                   | 设置元素的堆叠顺序                                           | _number`<br>`_auto  `<br>`inherit                                                                                                                                                                                                                                                  |

#### 溢出

overflow 是 CSS 的简写属性，其设置了元素溢出时所需的行为——即当元素的内容太大而无法适应它的区块格式化上下文时

#### 浮动

#### transforms转换

CSS 转换（transforms）允许您移动、旋转、缩放和倾斜元素

通过使用 CSS **transform** 属性，您可以利用以下 2D 转换方法：

- `translate(dx, dy)` 从其当前位置移动元素 `transform: translate(50px, 100px);`
  - `translateX(dx)` 沿x轴移动
  - `translateY(dy)` 沿y轴移动
- `rotate(a)` 根据给定的角度顺时针旋转元素(使用负值将逆时针旋转)`transform: rotate(20deg);`
- `scale(x,y)` 原始宽度乘以x，原始高度乘以y `transform: scale(2, 0.5);`
  - `scaleX(x)` 原始宽度乘以x
  - `scaleY(y)` 原始高度乘以y
- `skew(a, b)` 使元素沿X轴倾斜给定角度a，沿Y轴倾斜给定角度b `transform: skew(20deg, 10deg);`
  - `skewX(a)` 沿X轴倾斜给定角度a
  - `skewY(b)` 沿Y轴倾斜给定角度b
- `matrix()` matrix() 方法把所有 2D 变换方法组合为一个。旋转、缩放、移动（平移）和倾斜元素
  可接受六个参数，其中包括数学函数
  `matrix(scaleX(),skewY(),skewX(),scaleY(),translateX(),translateY())`

3D 转换

#### transition过渡

CSS 过渡允许您在给定的时间内平滑地改变属性值

- transition-delay 规定过渡效果的延迟（以秒计）
- transition-duration 规定过渡效果要持续多少秒或毫秒 如果未规定，则过渡不会有效果，因为默认值为 0
- transition-property 规定过渡效果所针对的 CSS 属性的名称
- transition-timing-function 规定过渡效果的速度曲线
  - ease - 规定过渡效果，先缓慢地开始，然后加速，然后缓慢地结束（默认）
  - linear - 规定从开始到结束具有相同速度的过渡效果
  - ease-in -规定缓慢开始的过渡效果
  - ease-out - 规定缓慢结束的过渡效果
  - ease-in-out - 规定开始和结束较慢的过渡效果
  - cubic-bezier(n,n,n,n) - 允许您在三次贝塞尔函数中定义自己的值
- transition 简写属性，用于将四个过渡属性设置为单一属性
  `transition: property duration timing-function delay`

```css
div {
  width: 100px;
  height: 100px;
  background: red;
  transition: width 500ms, height 500ms, transform 500ms;
}

div:hover {
  width: 150px;
  height: 150px;
  transform: rotate(90deg);
}
```

#### 动画

CSS 可实现 HTML 元素的动画效果，而不使用 JavaScript

### CSS变量

var() 函数用于插入 CSS 变量的值。
CSS 变量可以访问 DOM，这意味着您可以创建具有局部或全局范围的变量，使用 JavaScript 来修改变量，以及基于媒体查询来修改变量。
使用 CSS 变量的一种好方法涉及设计的颜色。您可以将它们放在变量中，而不必一遍又一遍地复制和粘贴相同的颜色。

`var(name, value)`

- name 必需。变量名（变量名称必须以两个破折号开头，且区分大小写）
- value 可选。回退值（在未找到变量时使用）

如需创建具有全局作用域的变量，请在 :root 选择器中声明它。 :root 选择器匹配文档的根元素。
如需创建具有局部作用域的变量，请在将要使用它的选择器中声明它。

```css
:root {
  --blue: #1e90ff;
  --white: #ffffff;
}

body {
  background-color: var(--blue);
}

p {
  color: var(--blue);
  background-color: var(--white);
  padding: 15px;
}
```

***局部变量可以覆盖全局变量***

**使用 JavaScript 更改变量**：

```javascript
<script>
    // 获取根元素
    var r = document.querySelector(':root');

    // 创建一个获取变量值的函数
    function myFunction_get() {
        // 获取根的样式（属性和值）
        var rs = getComputedStyle(r);
        // 提醒 --blue 变量的值
        alert("The value of --blue is: " + rs.getPropertyValue('--blue'));
}

    // 创建用于设置变量值的函数
    function myFunction_set() {
        // 将变量 --blue 的值设置为另一个值（在本例中为“lightblue”）
        r.style.setProperty('--blue', 'lightblue');
}
</script>
```

新css还有函数

### CSS响应式网页

为使桌面端、移动端用户获得最佳体验

方法1：使用js判断客户端，响应不同的html网页
方法2：使用css实现响应式布局，并且调整浏览器窗口大小时也会改变布局

### CSS图形

#### 三角形

**方案1(border)**：

```css
#triangle {
    width: 0;
    height: 0;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 100px solid red;
}
```

#### 圆形

```css
#circle {
    width: 0px;
    height: 0px;
    border: 50px solid red;
    border-radius: 50%  /* 其实这里可以是50%以上的任何数 */
}
```

### @media

```css
@media 条件 {
  /* 针对满足条件的设备或场景的样式 */
  选择器 {
    属性: 值;
  }
}

/* 针对屏幕宽度小于600px的设备 */
@media (max-width: 600px) {
  body {
    background-color: lightblue;
  }
}

/* 针对打印场景 */
@media print {
  .no-print {
    display: none;
  }
}
```
