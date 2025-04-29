# JavaScript

**let var const的区别**

***执行顺序***

JavaScript是一种属于网络的高级脚本语言,已经被广泛用于Web应用开发,常用来为网页添加各式各样的动态功能,为用户提供更流畅美观的浏览效果。通常JavaScript脚本是通过嵌入在HTML中来实现自身的功能的。

*JavaScript 是脚本语言，浏览器会在读取代码时，逐行地执行脚本代码。而对于传统编程来说，会在执行前对所有代码进行编译。*
*JavaScript 对大小写敏感，会忽略多余的空格*

**JavaScript 注释**
单行注释以 `//` 开头
多行注释以 `/*` 开始，以 `*/` 结尾

**JavaScript 用法**
HTML 中的 Javascript 脚本代码必须位于 **`<script>`** 与 **`</script>`** 标签之间。
`<script>` 标签可被放置在 HTML 页面的 **`<body>`** 或 **`<head>`** 部分中。

```html
    <script>
    // myScript
    </script>
```

也可以把脚本保存到外部文件中，外部文件通常包含被多个网页使用的代码。
外部 JavaScript 文件的文件扩展名是 `.js`。
放在 `<script>` 标签中的脚本与外部引用的脚本运行效果完全一致。
如需使用外部文件，在 `<script>` 标签的 "src" 属性中设置该 `.js` 文件：

```html
    <script src="myScript.js"></script>
```

HTML还提供 `<noscript>` 标签用于无法使用脚本时的替代内容，比方在浏览器禁用脚本时，或浏览器不支持客户端脚本时。只有在浏览器不支持脚本或者禁用脚本时，才会显示 `<noscript>` 元素中的内容

```html
<noscript>抱歉，你的浏览器不支持 JavaScript!</noscript>
```

把JSON或JavaScript对象序列化为JSON字符串 `JSON.stringify()`**.**substring**(**1**,**str**.**length**-**1**)**就可以直接去除引号

将JSON字符串反序列化为一个普通的JavaScript对象 `JSON.parse`

## 基础语法

### 输出

JavaScript 没有任何打印或者输出的函数，不过可以通过不同的方式来输出数据：

* 使用 **window.alert()** 弹出警告框。
* 使用 **document.write()** 方法将内容写到 HTML 文档中。
* 使用 **innerHTML** 写入到 HTML 元素。
* 使用 **console.log()** 写入到浏览器的控制台。

```html
<!DOCTYPE html>
<html>
<body>
    <p id="demo">一个段落</p>
    <button onclick="myFunction()">点我</button>
    <br>

    <!-- 使用 **window.alert()** 弹出警告框。 -->
    <script>
    window.alert('window.alert弹出警告框');
    </script>
    <!-- 使用 **document.write()** 方法将内容写到 HTML 文档中。 -->
    <script>
    document.write('document.write写入 HTML 文档');
    </script>
    <script>
    // 如果在文档已完成加载后执行 document.write，整个 HTML 页面将被覆盖
    function myFunction() {
        document.write('完成加载后执行document.write，整个 HTML 页面将被覆盖');
    }
    </script>
    <!-- 使用 **innerHTML** 写入到 HTML 元素。 -->
    <script>
    document.getElementById("demo").innerHTML = "innerHTML写入到 HTML 元素";
    </script>
    <!-- 使用 **console.log()** 写入到浏览器的控制台。 -->
    <script>
    console.log('console.log写入到浏览器的控制台');
    </script>
</body>
</html>
```

`console.log(typeof a);`
`console.dir(a);`打印对象

**浏览器控制台输出到文件**：

```js
// 先将如下函数输入控制台
// 然后在控制台输入 console.save(数据, 文件名) 调用
(function (console) {
    /**
     * 将数据保存为文件的控制台扩展方法
     * @param {Object|string} data - 要保存的数据（支持对象/JSON/字符串）
     * @param {string} [filename='console.json'] - 文件名（自动识别扩展名）
     */
    console.save = function (data, filename = 'console.json') {
        try {
            // 参数验证
            if (!data) throw new Error('No data provided');
            if (typeof filename !== 'string') throw new Error('Filename must be a string');

            // 智能识别数据类型
            let mimeType = 'text/plain';
            let content = data;
            
            if (typeof data === 'object' && data !== null) {
                mimeType = 'application/json';
                content = JSON.stringify(data, null, 4);
                if (!filename.includes('.')) {
                    filename += '.json';
                }
            }

            // 创建 Blob 并生成 URL
            const blob = new Blob([content], { type: mimeType });
            const url = URL.createObjectURL(blob);

            // 创建虚拟链接
            const a = document.createElement('a');
            a.style.display = 'none';
            a.href = url;
            a.download = filename;
            
            // 添加链接到文档并触发点击
            document.body.appendChild(a);
            a.click();

            // 清理资源
            URL.revokeObjectURL(url);
            document.body.removeChild(a);
        } catch (error) {
            console.error('console.save error:', error);
        }
    };
})(console);
```

## Web APIs

应用程序接口（API，Application Programming Interface）是基于编程语言构建的结构，使开发人员更容易地创建复杂的功能。它们抽象了复杂的代码，并提供一些简单的接口规则直接使用。
Web API是浏览器提供的一套操作浏览器功能和页面元素的API(BOM和DOM)

### DOM(文档对象模型)

文档对象模型（DOM）是一个网络文档的编程接口。它代表页面，以便程序可以改变文档的结构、风格和内容。DOM 将文档表示为节点和对象，这样，编程语言就可以与页面交互。
文档(document)：页面
元素(element)：页面中的标签
节点(node)：网页中所有的内容都是节点（标签、属性、文本、注释等）
![HTML DOM 树](image/javascrpt/DOM.png)

#### 获取HTML元素

**选择器：**

1. **根据id获取：**
   `document.getElemetById('id')`
   返回DOM元素对象；如果没有返回null。
2. **根据标签名获取：**
   `element.getElementByTagName('tagname')`
   *当然document.getElementByTagName也行。*
   返回带有指定标签名的元素对象的集合(伪数组形式)，*哪怕只获取到一个对象也会以伪数组形式储存*。
3. 根据类名获取(html5)：
   `document.getElementByClassName('classname')`
   返回根据类名获取的元素对象的集合。
4. 根据指定CSS选择器获取(html5)：
   `document.querySelector('.classname'/'#id'/'tagname')`
   返回指定选择器的第一个元素对象。
   `document.querySelectorAll('.classname'/'#id'/'tagname')`
   返回指定选择器的所有元素对象的集合。

***获取特殊元素(html、head、body)***
*当然可以先指定id再通过id选择器获取，或者通过标签名获取，不过提供了更方便的方法：*

* 获取html标签：`document.documentElement`
* 获取head标签：`document.head`
* 获取body标签：`document.body`

#### DOM操作元素

**1.操作元素内容：**
`element.innerText`：非标准 不识别HTML标签 去除空格和换行
`element.innerHTML`：W3C标准(推荐使用) 识别HTML标签 保留空格和换行 (会重新加载html，一些动态绑定的事件或样式会失效) 可以获取元素里面的内容

*但是使用innerHTML时，正因为识别HTML标签，有 `<<`、`<>`符号会有问题（但是 `>>`不会），这时可以使用innerText*

```html
    <div>
        div标签
        <p>p标签</p>
    </div>
    <script>
        var div = document.querySelector('div');
        console.log(div.innerText);
        // div标签 p标签
        console.log(div.innerHTML);
        // div标签
        // <p>p标签</p>
        div.innerHTML = new Date();
    </script>
```

**2.操作元素属性：**
`element.attribute`
attribute包括：src、href、id、alt、title等

```html
    <button>切换图片</button>
    <br>
    <img src="a.jpg" alt="a" title="a">

    <script>
        var btn = document.querySelector('button');
        var img = document.querySelector('img');
        var flag = 0;

        btn.onclick = function() {  // 这是一个点击事件
            if (flag==0) {
                img.src = 'b.jpg';
                img.alt = 'b';
                img.title = 'b';
                flag = 1;
            }
            else {
                img.src = 'a.jpg';
                img.alt = 'a';
                img.title = 'a';
                flag = 0;
            }
        }
    </script>
```

**3.操作表单元素：**
`element.attribute`
attribute包括：stype、value、checked、selected、disabled等

```html
    <button>按钮</button>
    <input type="text" value="请输入内容">
    <script>
        var btn = document.querySelector('button');
        var input = document.querySelector('input');

        btn.onclick = function() {
            input.value = '已提交';  // 修改表单显示的值
            // 如果只需要提交一次，之后禁用：
            this.disabled = true;   // this指向函数的调用者，在这里指btn
        }
    </script>
```

**4.操作元素样式：**
`element.style`:行内样式操作
`element.className`:类名样式操作

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }
        .div {
            width: 100px;
            height: 100px;
            background-color: green;
        }
        .change {
            width: 500px;
            height: 500px;
            background-color: red;
        }
    </style>
</head>
<body>
    <div class="div"></div>
    <script>
        var div = document.querySelector('div');
        div.onclick = function() {
            this.style.width = '400px';
            this.style.backgroundColor = 'purple';
            this.className = 'change';
            // element.className会删除原来的类名，如果需要保留原来的类名，可以：
            // if (flag==0) {
            //     this.className += ' change';  // 注意这里要有一个空格
            //     flag = 1;
            // }

            // 原来的类名比较少，可以直接：
            // this.className = 'div change';
        }
        // 发现最后width = 400px height: 500px backgroundColor = purple
        // 可以知道html与js都是逐行执行，并且行内样式css权重高（element.style>element.className）
        // 因为element.className本质只是更改了类名
    </script>
</body>
</html>
```

**5.操作自定义属性：**

`element.getAttribute('data-attribute')`：获取自定义属性
`element.setAttribute('data-attribute', 'newAttribute')`：更改自定义属性
`element.removeAttribute('data-attribute')`：删除自定义属性
其实不止能操作自定义属性，也可以操作原有属性（注意的是类名使用class而不是className），但是不推荐

*H5规范自定义属性以 `date-`开头，如 `date-attribute`*
*然后就可以使用 `element.dateset.attribute`获取自定义属性*

#### 节点操作元素

利用父子兄弟节点关系获取元素
逻辑性比DOM获取元素强、更简单，但兼容性差

节点有节点类型(nodeType)、节点名称(nodeName)、节点值(nodeValue)三个基本属性

* 元素节点 nodeType 为1
* 属性节点 nodeType 为2
* 文本节点 nodeType 为3 （文本节点包括文字、空格、换行等）

---

**节点获取元素**：

* 父节点：
  **`node.parentNode`获取离节点最近的父节点，如果找不到返回null**
* 子节点：
  **`node.children`获取所有的子元素节点的集合**
  *`node.childNodes`获取所有子节点（包括文本节点等）的即时更新的集合|我们一般只需要元素节点，因此很少使用|*

  ```html
      <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
          <li>5</li>
      </ul>
      <script>
          var a = document.querySelector('ol');
          // 第一个子节点 a.firstElementChild也行但有兼容性问题
          console.log(a.children[0]);
          // 最后一个子节点 a.lastElementChild也行但有兼容性问题
          console.log(a.children[a.children.length - 1]);
      </script>
  ```
* 兄弟节点：
  `node.nextSibling`获取下一个兄弟节点（包括文本节点等）
  `node.previousSibling`获取上一个兄弟节点（包括文本节点等）

  ```html
      <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      </ul>
      <script>
          var a = document.querySelector('li');

          // 获取下一个兄弟元素节点 也可以nextElementSibling但兼容性差
          // 所以可以自己封装一个函数：
          function getNextElementSibling(element) {
              var el = element;
              while (el = el.nextSibling) {
                  if (el.nodeType === 1) {
                      return el;
                  }
              }
              return null;
          }

          console.log(getNextElementSibling(a));
      </script>
  ```

---

**动态创建节点：**

`document.createElement('tagname')`创建元素节点 `document.createTextNode`创建文本节点
`element.innerHTMl = ''`DOM添加元素内容的方法，相当于创建并添加了节点
`document.write()`如果页面加载完毕，会导致页面重绘（所以一般不使用）

```html
    <script>
        // innerHTML拼接字符串的方式
        function f1() {
            var d1 = +new Date();
            for (var i = 0; i <= 10000; i++) {
                document.body.innerHTML += '<a>hi</a>';
            }
            var d2 = +new Date();
            console.log(d2 - d1);
        }
        // createElement方法
        function f2() {
            var d1 = +new Date();
            for (var i = 0; i <= 10000; i++) {
                var div = document.createElement('a');
                div.innerHTML = 'hi'
                document.body.appendChild(div);
            }
            var d2 = +new Date();
            console.log(d2 - d1);
        }
        // innerHTML数组的方式
        function f3() {
            var d1 = +new Date();
            var arr = [];
            for (var i = 0; i <= 10000; i++) {
                arr.push('<a>hi</a>');
            }
            document.body.innerHTML = arr.join('');
            var d2 = +new Date();
            console.log(d2 - d1);
        }
        f1(); //61478ms
        // f2(); //67ms
        // f3(); //37ms
        // 创建比较多个元素时innerHTMl效率比createElement高，同时注意应使用数组的方式
    </script>
```

**添加节点**：
`node.appendChild(child)`在子节点列表追加节点
`node.insertBefore(child, 指定节点)`在指定子节点前添加节点

**删除节点：**

`node.remove()`删除一个节点
`node.removeChild(child)`删除一个子节点

**复制节点：**
`node.cloneNode()`复制一份节点

```html
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
    </ul>
    <script>
        var a = document.querySelector('li');
        // 如果括号内为空或false，是浅拷贝，只克隆节点本身，不克隆里面的子节点
        console.log(a.cloneNode()); // <li></li>
        // 如果括号内为true，是深拷贝，克隆节点的所有内容
        console.log(a.cloneNode(true)); // <li>1</li>
    </script>
```

#### 事件

1. 事件源（事件被触发的对象）
2. 事件类型（事件如何触发）
3. 事件处理程序（函数赋值的方式）

**注册事件：**

* **传统注册方式** `btn.onclick = function() {}`
  最后注册的处理函数会覆盖之前注册的处理函数

  ```html
      <button id="btn">这是一个按钮</button>
      <script>
          var btn = document.getElementById('btn'); // 获取事件源 btn

          btn.onclick = function() { // 注册事件 btn.onclick(鼠标点击)
              alert('鼠标点击');  // 添加事件处理程序 function
          }

          // 当然也可以：document.getElementById('btn').onclick = function() { alert('鼠标点击'); }

      </script>

      <!-- 也有一种简单的写法: <button onclick="alert('鼠标点击')">这是一个按钮</button> --> 


      <!-- 当然可以使用自定义的函数（在<script>标签中定义）: -->
      <!-- <button onclick="f(this)">这是一个按钮</button>
      <script>
          function f(a) { 
              console.log(a.innerHTML);
              alert('鼠标点击'); 
          }
      </script> -->
  ```
* **方法监听方式** `addEventListener(type, listener[, useCapture])`
  *注意事件类型没有 `on`*
  可以按注册顺序依次执行处理函数

  ```html
      <button id="btn">这是一个按钮</button>
      <script>
          var btn = document.getElementById('btn'); // 获取事件源 btn

          btn.addEventListener('click', function() {
              alert('鼠标点击');
          })
          btn.addEventListener('click', function() {
              alert('事件监听');
          })
      </script>
  ```

---

**删除事件：**
传统注册方式:`eventTarget.onclick = null`
方法监听方式:`eventTarget.removeEventListener(type, listener[, useCapture])`

```html
    <button id="btn">这是一个按钮</button>
    <script>
        var btn = document.getElementById('btn'); // 获取事件源 btn
        // 传统注册方式
        btn.onclick = function() {
            alert('hi');
            btn.onclick = null;
        }
        // 方法监听方式
        btn.addEventListener('click', f)
        function f() {
            alert('鼠标点击');
            btn.removeEventListener('click', f);
        }   
    </script>
```

---

DOM事件流：事件在元素节点之间的传播顺序（事件捕获阶段、当前目标阶段、事件冒泡阶段）
*冒泡原理：（以鼠标点击为例）在父节点绑定一个鼠标点击事件，那么点击子节点也会触发该事件*

**事件对象：**
`eventTarget.onclick = function(event) {}`
`btn.addEventListener('click', function(event) {})`
event叫做事件对象(名字可以随便取)；有事件才有事件对象

```html
    <button id="btn">这是一个按钮</button>
    <script>
        var btn = document.getElementById('btn'); // 获取事件源 btn

        btn.onclick = function(e) {
            console.log(e); // 事件对象

            console.log(e.target); // 触发事件的对象
            console.log(this);  // 绑定事件的对象 也可以e.currentTarget
        }
    </script>
```

事件对象常用方法：

| 属性、方法              | 说明                       |
| :---------------------- | -------------------------- |
| `e.target`            | 返回触发事件的对象         |
| `e.type`              | 返回事件的类型             |
| `e.preventDefault()`  | 阻止默认事件(比如链接跳转) |
| `e.stopPropagation()` | 阻止冒泡                   |

---

为多个元素添加事件监听器可以使用循环：

```javascript
divs.forEach(e => {
    e.addEventListener('click', () => {
        e.innerHTML += 1;
    });
});
```

如果添加的事件相同，还可以利用冒泡原理委派事件：

```javascript
divsBox.addEventListener('click', () => {
    alert('hi');
});
```

##### 鼠标事件

* 鼠标左键点击 `onclick`
* 鼠标经过 `onmouseover`
* 鼠标离开 `onmouseout`
* 获得鼠标焦点 `onfocus`
* 失去鼠标焦点 `onblur`
* 鼠标移动 `onmousemove`
* 鼠标左键或右键弹起 `onmouseup`
* 鼠标左键或右键按下 `onmousedown`
* 鼠标右键菜单 `contextmemu`一般用于禁用默认事件
* 鼠标选中 `selectstart`一般用于禁用默认事件

| 鼠标事件对象  | 说明                          |
| ------------- | ----------------------------- |
| `e.clientX` | 鼠标在浏览器窗口可视区的x坐标 |
| `e.clientY` | 鼠标在浏览器窗口可视区的y坐标 |
| `e.pageX`   | 鼠标在页面文档的x坐标         |
| `e.pageY`   | 鼠标在页面文档的y坐标         |
| `e.screenX` | 鼠标在电脑屏幕的x坐标         |
| `e.screenY` | 鼠标在电脑屏幕的y坐标         |

###### 选中复制时不触发点击事件

选中复制时会触发单击事件，可以判断是否选中内容：

```javascript
function getSelected() {
    if (window.getSelection) {
        return window.getSelection().toString();
    } else if (document.getSelection) {
        return document.getSelection().toString();
    } else {
        var selection = document.selection && document.selection.createRange();
        if (selection.text) {
            return selection.text.toString();
        }
        return "";
    }
}
// if (!getSelected()){当没有选中内容时才执行}
```

##### 键盘事件

* 某个按键松开时触发 `onkeyup`*不区分大小写*
* 某个按键按下时触发 `onkeydown`*不区分大小写*
* 某个按键按下时触发（不识别功能键 如ctrl、shift、箭头等）`onkeypress`*区分大小写*

*执行顺序 `keydown`-->`keypress`-->`keyup`*

键盘事件对象：
`keyCode`返回该键的ASCII值
`key`可以直接返回该键的值，但有兼容性问题

```html
    <script>
        document.onkeyup = function(e) {
            console.log(e.key);
        }
    </script>
```



**浏览器打印设置文件名**（ctrl+P无法指定）

```html
<!-- 引入 html2pdf 库 -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<button onclick="exportToPDF()">打印并保存为 PDF</button>

<script>
function exportToPDF() {
  const element = document.body; // 要打印的内容区域
  const filename = "自定义文件名.pdf"; // 指定文件名
  
  html2pdf()
    .set({
      filename: filename,      // 设置文件名
      image: { type: 'jpeg', quality: 0.98 }, // 图片质量
      html2canvas: { scale: 2 }, // 渲染精度
      jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' } // PDF格式
    })
    // orientation: 'landscape' } // 设置为横屏
    .from(element)
    .save();
}
</script>
```

### BOM(浏览器对象模型)

浏览器对象模型（**B**rowser **O**bject **M**odel (BOM)）允许 JavaScript 与浏览器对话。

#### BOM事件

**窗口加载事件**
`window.addEventListener('load', function() {})`
`window.onload = function() {}`
当文档内容加载完成触发该事件
*利用窗口加载事件可以把JS代码放在html的任何位置（包括html外）*

**DOM加载事件**
`document.addEventListener('DOMContentLoaded', function() {})`
当DOM加载完成触发（不包括样式表、图片、flash等）
*如果图片较多加载时间长，可以优化用户体验*

**调整窗口大小事件**
`window.addEventListener('resize', function() {})`
`window.onresize = function() {}`
当窗口大小发生像素变化触发
*可以利用该事件完成响应式布局*

#### 定时器

创建定时器
`window.setTimeout(调用函数, 延时时间ms)`window可省略，延时时间省略默认0
延时时间后触发该事件
*因为页面中常常有多个定时器，为方便区分可以给定时器取名（标识符），如：`var time1 = setTime(f, 3000)`*

删除定时器
`window.clearTimeout(timeoutID)`window可省略，timeoutID为取的名字

---

创建定时器
`window.setInterval(调用函数, 间隔时间ms)`window可省略，延时时间省略默认0
每隔间隔时间调用一次函数

删除定时器
`window.clearInterval(intervalID)`window可省略，intervalID为取的名字

#### location对象

| location属性、方法 | 返回值                                                      |
| ------------------ | ----------------------------------------------------------- |
| `href`           | 整个URL                                                     |
| `host`           | 主机/域名                                                   |
| `port`           | 端口号                                                      |
| `pathname`       | 路径                                                        |
| `search`         | 参数                                                        |
| `hash`           | 片段                                                        |
| `assign()`       | 重定向页面（可以后退）                                      |
| `replace()`      | 替换当前页面（不能后退）                                    |
| `reload()`       | 重新加载页面（F5）<br />如果参数为true为强制刷新（ctrl+F5） |

#### navigator对象

***96***

#### history对象

### Web本地存储

数据存储在用户浏览器中、设置读取方便、刷新不丢失数据

`sessionStorage`容量大约5M
`localStorage`容量大约20M

只能存储字符串，可以将对象 `JSON.stringify()`编码后存储

#### window.sessionStorage

用于临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据。

1. 生命周期为关闭浏览器窗口
2. 同一个页面下数据可以共享
3. 以键值对的形式存储

`sessionStorage.setItem(key, value)`存储数据/更改数据
`sessionStorage.getItem(key)`获取数据
`sessionStorage.removeItem(key)`删除数据
`sessionStorage.clear()`删除所有数据（谨慎使用）

#### window.localStorage

用于长久保存整个网站的数据，保存的数据没有过期时间，直到手动去除。
*处于安全考虑如果储存密码等数据不要使用localStorage*

1. 生命周期永久存在，除非手动删除
2. 可以多页面共享
3. 以键值对的形式存储

`localStorage.setItem(key, value)`存储数据/更改数据
`localStorage.getItem(key)`获取数据
`localStorage.removeItem(key)`删除数据
`localStorage.clear()`删除所有数据（谨慎使用）

#### HTML5 Web IndexedDB

ndexedDB 是一种基于浏览器的 NoSQL 数据库，用于在客户端持久化存储大量结构化数据。

### webgl

### webgpu

### 什么是 Web Worker？

当在 HTML 页面中执行脚本时，页面的状态是不可响应的，直到脚本已完成。

web worker 是运行在后台的 JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 web worker 在后台运行。

if(typeof(Worker)!=="undefined")
{
    // 是的! Web worker 支持!
    // 一些代码.....
}
else
{
    //抱歉! Web Worker 不支持
}

### Server-Sent 事件 - 单向消息传递

Server-Sent 事件指的是网页自动获取来自服务器的更新。

以前也可能做到这一点，前提是网页不得不询问是否有可用的更新。通过服务器发送事件，更新能够自动到达。

### HTML5 WebSocket

WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。

WebSocket 使得客户端和服务器之间的数据交换变得更加简单，允许服务端主动向客户端推送数据。在 WebSocket API 中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输。

在 WebSocket API 中，浏览器和服务器只需要做一个握手的动作，然后，浏览器和服务器之间就形成了一条快速通道。两者之间就直接可以数据互相传送。

现在，很多网站为了实现推送技术，所用的技术都是 Ajax 轮询。轮询是在特定的的时间间隔（如每1秒），由浏览器对服务器发出HTTP请求，然后由服务器返回最新的数据给客户端的浏览器。这种传统的模式带来很明显的缺点，即浏览器需要不断的向服务器发出请求，然而HTTP请求可能包含较长的头部，其中真正有效的数据可能只是很小的一部分，显然这样会浪费很多的带宽等资源。

HTML5 定义的 WebSocket 协议，能更好的节省服务器资源和带宽，并且能够更实时地进行通讯。

![](https://www.runoob.com/wp-content/uploads/2016/03/ws.png)

浏览器通过 JavaScript 向服务器发出建立 WebSocket 连接的请求，连接建立以后，客户端和服务器端就可以通过 TCP 连接直接交换数据。

## AJAX

AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）

浏览器与服务器之间动态数据交互

* 不刷新页面更新网页
* 在页面加载后从服务器请求数据
* 在页面加载后从服务器接收数据
* 在后台向服务器发送数据

我们常常用子线程来完成一些可能消耗时间足够长以至于被用户察觉的事情，比如读取一个大文件或者发出一个网络请求。因为子线程独立于主线程，所以即使出现阻塞也不会影响主线程的运行。但是子线程有一个局限：一旦发射了以后就会与主线程失去同步，我们无法确定它的结束，如果结束之后需要处理一些事情，比如处理来自服务器的信息，我们是无法将它合并到主线程中去的。
为了解决这个问题，JavaScript 中的异步操作函数往往通过回调函数来实现异步任务的结果处理。回调函数就是一个函数，在我们启动一个异步任务的时候就告诉它：等你完成了这个任务之后要干什么。这样一来主线程几乎不用关心异步任务的状态。

```html
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8"> 
<title>AJAX</title> 
</head>
<body>

<p>回调函数等待 3 秒后执行。</p>
<p id="demo"></p>
<script>
function print() {
    document.getElementById("demo").innerHTML="AJAX!";
}
setTimeout(print, 3000);
</script>

</body>
</html>
```

### axios库

基于XMLHttpRequest封装，代码简单，使用量大

引入axios.js:`<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>`

**对服务器数据操作：**
请求方法(GET/POST/PUT/DELETE/PATCH)

```javascript
    axios({
        url:'目标资源地址', 
        method:'GET', // 默认方法为GET，可以省略
        params:{
            参数名:值    // 添加查询参数相当于url:'目标资源地址?参数名=值'
        }
    }).then(result => {
        // console.log(result);
        // 对服务器返回数据处理
    })
```

```javascript
    axios({
        url:'目标资源地址',
        method:'请求方法',
        data:{
            参数名:值
        }
    }).then(result => {
    })
```

## 跨域

* 跨域并不是请求发不出去，请求能发出去，服务端能收到请求并正常返回结果，只是结果**被浏览器拦截**了
* 那为什么拦截呢，我们应该先了解一下什么是**同源策略**
* MDN上的解释：同源策略是一个重要的安全策略，它用于限制一个origin的文档或者它加载的脚本如何能与另一个源的资源进行交互。它能**帮助阻隔恶意文档，减少可能被攻击的媒介**
* 具体的限制（三限制）：
  * 同源策略限制了来自不同源的 `JavaScript` 脚本对当前 `DOM`对象读和写的操作
  * 同源策略限制了来自不同源的站点读取当前的 `Cookie`、`LocalStorage` 等数据
  * 同源策略限制了通过 `XMLHttpRequest`等方式将站点的数据发送给不同源的站点
* 能使的标签（能跨域请求资源的标签）：
  * `<script src="..."></script>`
  * `<link rel="stylesheet" href="...">`
  * 通过 `<img>`展示图片
  * 通过 `<video>`和 `<audio>`播放的多媒体资源
  * 通过 `<iframe>`载入的任何资源

👉何为同源

* 如果两个 URL 的协议（Protocol），域名（domain），端口（port）都相同的话，则这两个 URL 是*同源*
  * 协议：定义了数据如何在计算机内和之间进行交换的规则的系统。例如：`http`，`https`
  * 域名：可以通过DNS解析为IP地址 （这里即使两个不同的域名指向同一个IP地址，也是属于不同源的）
  * 端口：http默认使用80端口，https默认使用443端口

## Node.js(跨平台js运行环境)

* Node.js 是一个开源服务器环境
* Node.js 是免费的
* Node.js 在各种平台 (Windows, Linux, Unix, Mac OS X 等)上运行
* Node.js 在服务器上使用JavaScript

安装：
windows可以直接在官网下载
linux(debian/unbutu)`apt install nodejs npm`

需要安装node环境，可以输入 `node -v`判断是否安装成功
输入 `node test.js`即可执行js代码

### 模块

每个js文件都可以看作一个模块
模块化可以提高代码复用性

CommonJS标准（node.js默认）

**导出：**

```js
module.exports = {
    对外属性名1: 值1,
    对外属性名2: 值2
}
```

**导入：**

```js
const 属性名 = require('模块名或路径') // 内置模块用模块名；自定义模块用文件路径
const { 属性名1, 属性名2 } = require('模块名或路径')
```

---

ECMAScript标准（需要在运行模块文件夹新建 `package.json`文件，并设置 `{"type": "module"}`）

```js
export default {
    对外属性名1: 值1,
    对外属性名2: 值2
}
```

**导入：**

```js
import 属性名1, 属性名2 from '模块名或路径'
```

#### fs模块(读写文件)

*加载fs模块：`const fs = require('fs')`*

**写入文件内容：**

```js
fs.writeFile('文件路径', '写入内容', err => {   // err是错误
    // 写入后的回调函数
})
```

**读取文件内容：**

```js
fs.readFile('文件路径', '写入内容', (err, data) => {   //data是文件内容的Buffer数据流 data.toString()转换成字符串
    // 读取后的回调函数
})
```

---

```js
const fs = require('fs')

fs.writeFile('./test.txt', 'hello world', err => {
    if (err) console.log(err)
    else console.log('写入成功')
})
```

#### path模块(操作文件路径)

*加载path模块：`const path = require('path')`*

在node.js代码中，最好使用绝对路径

`__dirname`内置变量，当前模块的绝对路径
`path.join()`会使用特定平台的分隔符拼接路径片段

```js
// 将url地址映射为文件路径
const url = req.url
const fpath = path.join(__dirname, url)
```

#### http模块(创建web服务器)

*加载http模块：`const http = require('http')`*

创建web服务：

```js
const http = require('http')
const server = http.createServer()

server.on('request', (req, res) => { // req请求对象 res响应对象
    // 请求的地址req.url  请求的类型req.method
    res.setHeader('Content-Type', 'text/plain;charset=utf-8')
    res.end('你好') // 向客户端响应内容
})

server.listen(3000, () => {         // 设置端口号
    console.log('web 服务已启动')
})
// 执行代码后就可以在浏览器中使用http://localhost:3000
// 终端中ctrl + c 终止web服务
```

### 包

包是将模块、代码等其他资料聚合成的一个文件夹

这个文件夹的根目录下必须有 `package.json`文件记录包的信息
以下是一些常见的清单内容：

```json
{
    "name": "软件包名称",
    "version": "版本号",
    "description": "包的简短描述",
    "main": "软件包入口/默认为index.js",
    "author": "作者",
    "license": "软件包许可证书"
}
```

#### npm软件包管理器

下载和管理软件包
`npm init -y`初始化清单文件（得到package.json，有则跳过）
`npm i 软件包名称`(install)下载软件包，`npm i 包名@版本号`指定版本
`npm up 软件包名称`(update,upgrate)更新软件包
`npm uni 软件包名称`(unstall)删除软件包

npm安装所有依赖（安装所有所需软件包）
在相应文件夹的终端输入 `npm i`下载package.json中记录的所有软件包

全局软件包（本机所有项目可用）
`npm i -g 软件包名称`安装

–save/-S 会把依赖包名称添加到 package.json 文件 dependencies 下
–save-dev/-D 会把依赖包名称添加到 package.json 文件 devDependencies下

`npm config get registry`查看npm下载源
`npm config set registry=https://registry.npm.taobao.org`修改npm下载源
`npm config set registry=https://registry.npmjs.org`恢复默认源
还可以通过安装cnpm，推荐这种方式是因为不会影响npm命令 `npm i -g cnpm --registry=https://registry.npm.taobao.org`之后就可以用cnpm替换npm命令，如 `cnpm i 软件包名称`

`npx 软件包 项目路径` 会自动查找当前依赖包中的可执行文件，如果找不到，就会去 `PATH` 里找。如果依然找不到，就会帮你安装。比如使用一次就不怎么使用的包，非常浪费磁盘空间，而使用npx命令用完会自动删除

---

`npm ls`(list)列出当前文件夹已安装的包 只显示顶层依赖，`npm ls -all`则会显示所有依赖
`npm out 软件包`(outdated)检查更新，如果没有指定软件包则会查看当前文件夹所有软件包更新，指定 `npm out -g`则会检查全局软件包

在vscode中，资源管理器里可以打开npm脚本
在这里可以查看对应文件夹中的npm脚本并运行

#### yarn包管理器

[Yarn](http://yarnpkg.com/)是 Facebook 提供的替代 npm 的工具，可以加速 node 模块的下载
`npm install -g yarn`
安装完 yarn 之后就可以用 yarn 代替 npm 了

yarn install
yarn add
yarn list
yarn update

### express包(创建web网站/API接口服务器)

基于node.js中的http模块进一步封装而成，能提高开发效率

安装：`npm i express`

**创建服务器：**

```js
const express = require('express')
const app = express()

app.listen(3000, () => {
    console.log('express server running at http://127.0.0.1:3000')
})
```

**监听get/post请求：**

```js
app.get('请求url', function(req, res) {}) // 如app.get('/', function(req, res) {})
app.post('请求url', function(req, res) {})
```

*把内容响应给客户端：*`res.send()`方法，可以发送html标签如 ``res.send(`<a href="/${newFilename}">查看</a>`)``
也可以使用如 `res.sendFile(__dirname + '/index.html')`渲染整个html文件

*客户端发送的查询参数：*`req.query`
*url中的动态参数：*`req.params`

**托管静态资源：**

```js
app.use(express.static('./files')) // 存放资源的文件夹
```

这样就可以访问文件夹中的资源，如 `http://127.0.0.1:3000/image/1.png`
可以托管多个文件夹，按托管顺序依次查找所需资源

#### nodemon包(自动重启服务)

当代码被修改后nodemon可以自动重启项目，不需要手动关闭再重启

安装：`npm i -g nodemon`
使用：将 `node app.js`替换为 `nodemon app.js`即可

#### 路由

在Express中，路由指客户端请求与服务器处理函数之间的映射关系
路由处理函数形参包含req、res

格式：`app.MTHOD(PATH, HANDLER)`
像app.get(url, function(req, res) {})之类都是路由

**模块化路由：**
创建路由模块：

```js
var express = require('express')
var router = express.Router()   // 创建路由对象

// 挂载获取用户列表的路由
// 通过http://127.0.0.1:3000/user/list访问
router.get('/user/list', function (req, res) {
    res.send('Get user list.')
})
// 挂载添加用户的路由
router.post('/user/add', function (req, res) {
    res.send('Add new user.')
})

module.exports = router // 向外导出路由对象
```

使用路由模块：

```js
const userRouter = reqire('创建的路由模块路径') // 导入路由

app.use(userRouter) // 注册路由模块
// 改为app.use('/api', userRouter) 需要通过http://127.0.0.1:3000/api/user/list访问
```

#### 中间件

本质就是一个function处理函数，形参包含req、res、next
多个中间件共享同一req、res

next函数是实现多个中间件连续调用的关键，把处理关系转交给下一个中间件或路由

**定义中间件：**

```js
const mw = function (req, res ,next) {
    console.log('这是一个中间件')
    next()  // 转交给下一个中间件或路由
}
```

1. 应用级中间件（绑定在app上）：
   通过 `app.use(中间件函数)`注册为*全局生效中间件*
   客户端任何请求都会调用该中间件

   在路由中添加中间件mw：`app.MTHOD(PATH, mw, HANDLER)`，该中间件仅在该路由中调用（*局部生效中间件*）；先调用中间件再调用路由
   还可以 `app.MTHOD(PATH, mw1, mw2, HANDLER)`调用多个中间件
2. 路由级中间件（绑定router在上）
3. 错误级别中间件：
   专门捕获异常的中间件，含有四个形参err、req、res、next，如：

   ```js
   app.use(function (err, req, res, next) {
        console.log('Error！' + err.message)
        res.send('发生了错误：' + err.message)
   })
   ```
4. Express内置中间件(express.static,express.json,express.urlencoded):
   解析请求体都是用于POSR请求
   `app.use(express.json())`解析JSON格式请求体  通过req.body访问
   `app.use(express.urlencoded({ extended: false }))`解析URL-encoded格式请求体  通过req.body访问
5. 第三方中间件：
   *body-parser中间件：*
   `npm i body-parser`安装中间件；`app.use(require('body-parser').urlencoded({ extended: false }))`使用
   因为express.urlencoded是基于body-parser进一步封装而成，因此只是举例没必要使用body-parser

#### cors中间件(解决跨域问题)

GET、POST不支持跨域请求，解决方法：CORS（推荐）、JSONP（只支持get）

安装：`npm i cors`
使用：
`const cors = require('cors')`
`app.use(cors())`

**设置cors响应头** Access-Control-Allow-
`res.setHeader('Access-Control-Allow-Origin', 'url')`只允许来自url（可以使用通配符，如 `'*'`为允许来自任何域的请求）的请求
`res.setHeader('Access-Control-Allow-Headers', '请求头1, 请求头2')`默认CORS仅支持客户端发送9个请求头，需要使用该方法声明额外请求头，否则会请求失败
`res.setHeader('Access-Control-Allow-Methods', '请求方式')`默认CORS仅支持GET、POST、HEAD请求，如果需要使用PUT、DELETE等方式，需要设置（可以使用 `'*'`允许所有请求方法）

#### JSONP(解决跨域问题)

只支持get请求
原理与CORS不同，没有使用XMLHttpRequest对象
出于兼容性考虑，可以同时配置CORS、JSONP，但是必须在配置CORS前声明JSONP
需要指定 `dataType: 'jsonp'`

```js
app.get('/api/jsonp', (req, res) => {
    // 得到函数名称
    const funcName = req.query.callback
    // 定义要发送到客户端的数据对象
    const data = { name: 'x', age: 22}
    // 拼接出一个函数的调用
    const scriptStr = `${funcName}(${JSON.stringify(data)})`
    // 把拼接的字符串响应给客户端
    res.send(scriptStr)
})
```

#### multer中间件(解决file表单问题)

接收表单信息时，如text表单可以直接接收
要传递file表单时，前端需要添加 `enctype="multipart/form-data"`，但是后端不能直接接受文件，甚至会导致原本能接收的text表单也无法接收

multer中间件可以解决这个问题

安装：`npm i multer`
使用：`const multer = require('multer')`
`const upload = multer({ dest: 'files/' })`'files/'是文件存放路径，如果没有会自动创建
`app.post('/post', upload.single('file'), (req, res) => {})`'file'是前端设置的file表单的name值

使用成功后，可以通过 `req.file`获取文件信息:`req.file.filename`文件名

这个文件默认是没有后缀名的，如果需要可以：

```js
// 通过fs模块重命名文件来添加后缀名
if (req.file) {
    fs.renameSync(`./files/${req.file.filename}`, `./files/${req.file.filename + '.png'}`)
}
```

#### 实现传递表单文件

### APIDOC

### Webpack(静态模块打包工具)

webpack 是一个用于现代 JavaScript 应用程序的 静态模块打包工具。当 webpack 处理应用程序时，它会在内部从一个或多个入口点构建一个 依赖图(dependency graph)，然后将你项目中所需的每一个模块组合成一个或多个 bundles，它们均为静态资源，用于展示你的内容。

### 连接MySQL

安装驱动 `npm i mysql`

**连接数据库**:`mysql.createConnection({})`

```javascript
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : '123456',
  database : 'test'
});
 
connection.connect();
 
connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});
```

数据库连接参数说明：

| 参数                         | 描述                                                                                |
| ---------------------------- | ----------------------------------------------------------------------------------- |
| **host**               | 主机地址 （默认：localhost）                                                        |
| **user**               | 用户名                                                                              |
| **password**           | 密码                                                                                |
| **port**               | 端口号 （默认：3306）                                                               |
| **database**           | 数据库名                                                                            |
| charset                      | 连接字符集（默认：'UTF8_GENERAL_CI'，注意字符集的字母都要大写）                     |
| localAddress                 | 此IP用于TCP连接（可选）                                                             |
| socketPath                   | 连接到unix域路径，当使用 host 和 port 时会被忽略                                    |
| timezone                     | 时区（默认：'local'）                                                               |
| connectTimeout               | 连接超时（默认：不限制；单位：毫秒）                                                |
| stringifyObjects             | 是否序列化对象                                                                      |
| typeCast                     | 是否将列值转化为本地JavaScript类型值 （默认：true）                                 |
| queryFormat                  | 自定义query语句格式化方法                                                           |
| supportBigNumbers            | 数据库支持bigint或decimal类型列时，需要设此option为true （默认：false）             |
| bigNumberStrings             | 强制bigint或decimal列以JavaScript字符串类型返回（默认：false）                      |
| dateStrings                  | 强制timestamp,datetime,data返回字符串类型，而不是JavaScript Date类型（默认：false） |
| debug                        | 开启调试（默认：false）                                                             |
| **multipleStatements** | 是否许一个query中有多个MySQL语句 （默认：false）                                    |
| flags                        | 用于修改连接标志                                                                    |
| ssl                          | 使用ssl参数或一个包含ssl配置文件名称的字符串，目前只捆绑Amazon RDS的配置文件        |

#### 数据库操作(CURD)

**查询数据**:

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({   
  host     : 'localhost',   
  user     : 'root',  
  password : '123456',   
  port: '3306',   
  database: 'test' 
}); 
 
connection.connect();
 
var  sql = 'SELECT * FROM websites';
//查
connection.query(sql,function (err, result) {
        if(err){
          console.log('[SELECT ERROR] - ',err.message);
          return;
        }
 
       console.log('--------------------------SELECT----------------------------');
       console.log(result);
       console.log('------------------------------------------------------------\n\n');  
});
 
connection.end();
```

**插入数据**:

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({   
  host     : 'localhost',   
  user     : 'root',  
  password : '123456',   
  port: '3306',   
  database: 'test' 
}); 
 
connection.connect();
 
var  addSql = 'INSERT INTO websites(Id,name,url,alexa,country) VALUES(0,?,?,?,?)';
var  addSqlParams = ['菜鸟工具', 'https://c.runoob.com','23453', 'CN'];
//增
connection.query(addSql,addSqlParams,function (err, result) {
        if(err){
         console.log('[INSERT ERROR] - ',err.message);
         return;
        }  
 
       console.log('--------------------------INSERT----------------------------');
       //console.log('INSERT ID:',result.insertId);  
       console.log('INSERT ID:',result);  
       console.log('-----------------------------------------------------------------\n\n');  
});
 
connection.end();
```

**更新数据**:

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({   
  host     : 'localhost',   
  user     : 'root',  
  password : '123456',   
  port: '3306',   
  database: 'test' 
}); 
 
connection.connect();
 
var modSql = 'UPDATE websites SET name = ?,url = ? WHERE Id = ?';
var modSqlParams = ['菜鸟移动站', 'https://m.runoob.com',6];
//改
connection.query(modSql,modSqlParams,function (err, result) {
   if(err){
         console.log('[UPDATE ERROR] - ',err.message);
         return;
   }  
  console.log('--------------------------UPDATE----------------------------');
  console.log('UPDATE affectedRows',result.affectedRows);
  console.log('-----------------------------------------------------------------\n\n');
});
 
connection.end();
```

**删除数据**:

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({   
  host     : 'localhost',   
  user     : 'root',  
  password : '123456',   
  port: '3306',   
  database: 'test' 
}); 
 
connection.connect();
 
var delSql = 'DELETE FROM websites where id=6';
//删
connection.query(delSql,function (err, result) {
        if(err){
          console.log('[DELETE ERROR] - ',err.message);
          return;
        }  
 
       console.log('--------------------------DELETE----------------------------');
       console.log('DELETE affectedRows',result.affectedRows);
       console.log('-----------------------------------------------------------------\n\n');  
});
 
connection.end();
```

## JavaScript 库

在网页中添加JavaScript 库有两种方式：
- 直接把库下载到本地，然后 `<script src="jquery-1.10.2.min.js"></script>`导入
- 使用CDN（内容分发网络） `<script src="https://cdn.staticfile.net/jquery/1.10.2/jquery.min.js">` 引用

### jQuery

jQuery 是一个 JavaScript 库，十分经典，不过如今有点过时

### Three.js

Three.js是基于原生WebGL封装运行的三维引擎

可以下载 [Three.js](https://threejs.org/?_blank)
或者使用CDN `<script src="http://www.yanhuangxueyuan.com/threejs/build/three.js"></script>`

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>第一个three.js文件_WebGL三维场景</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      /* 隐藏body窗口区域滚动条 */
    }
  </style>
  <!--引入three.js三维引擎-->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<body>
  <script>
    /**
     * 创建场景对象Scene
     */
    var scene = new THREE.Scene();
    /**
     * 创建网格模型
     */
    // var geometry = new THREE.SphereGeometry(60, 40, 40); //创建一个球体几何对象
    var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
    var material = new THREE.MeshLambertMaterial({
      color: 0x0000ff
    }); //材质对象Material
    var mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
    scene.add(mesh); //网格模型添加到场景中
    /**
     * 光源设置
     */
    //点光源
    var point = new THREE.PointLight(0xffffff);
    point.position.set(400, 200, 300); //点光源位置
    scene.add(point); //点光源添加到场景中
    //环境光
    var ambient = new THREE.AmbientLight(0x444444);
    scene.add(ambient);
    // console.log(scene)
    // console.log(scene.children)
    /**
     * 相机设置
     */
    var width = window.innerWidth; //窗口宽度
    var height = window.innerHeight; //窗口高度
    var k = width / height; //窗口宽高比
    var s = 200; //三维场景显示范围控制系数，系数越大，显示的范围越大
    //创建相机对象
    var camera = new THREE.OrthographicCamera(-s * k, s * k, s, -s, 1, 1000);
    camera.position.set(200, 300, 200); //设置相机位置
    camera.lookAt(scene.position); //设置相机方向(指向的场景对象)
    /**
     * 创建渲染器对象
     */
    var renderer = new THREE.WebGLRenderer();
    renderer.setSize(width, height);//设置渲染区域尺寸
    renderer.setClearColor(0xb9d3ff, 1); //设置背景颜色
    document.body.appendChild(renderer.domElement); //body元素中插入canvas对象
    //执行渲染操作   指定场景、相机作为参数
    renderer.render(scene, camera);
  </script>
</body>
</html>
```

### particles.js 

particles.js 是一个轻量级的 JavaScript 库，用于在网页上创建粒子效果。
这个库非常简单易用，不依赖其他库，并且响应式设计，意味着它可以在不同尺寸的屏幕上都能很好地工作。particles.js 通过在 HTML 的 `<canvas>`元素上绘制粒子，来创建吸引人的背景效果或者其他视觉效果。

[Js粒子背景生成器_背景动效可视化工具_H5炫酷粒子动画代码](https://www.bootstrapmb.com/h5bg)

首先，你需要在你的项目中引入 `particles.js`。你可以通过 `CDN` 直接引入，也可以下载到本地。

```js
<script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
```
`https://cdnjs.cloudflare.com/ajax/libs/particlesjs/2.2.3/particles.min.js`

接下来，在你的 `HTML` 文件中创建一个容器，用于放置粒子效果：

```html
<!-- 为了方便观察可以设置背景颜色background-color为black -->
<div id="particles-js"></div>
```

然后，在 JavaScript 中配置和初始化 particles.js：

```js
<!-- 在 JavaScript 中配置和初始化 particles.js -->
<script>
  particlesJS("particles-js", {
    // 粒子的基本配置
    particles: {
      number: {
        value: 80,  // 粒子数量
        density: {
          enable: true,
          value_area: 800,  // 粒子分布密度
        },
      },
      color: {
        value: "#ffffff",  // 粒子颜色
      },
      shape: {
        type: "circle",  // 粒子形状，支持 circle（圆形）等
        stroke: {
          width: 0,
          color: "#000000",
        },
        polygon: {
          nb_sides: 5,
        },
      },
      opacity: {
        value: 0.5,  // 粒子透明度
        random: false,
        anim: {
          enable: false,
          speed: 1,
          opacity_min: 0.1,
          sync: false,
        },
      },
      size: {
        value: 3,  // 粒子大小
        random: true,
        anim: {
          enable: false,
          speed: 40,
          size_min: 0.1,
          sync: false,
        },
      },
      line_linked: {
        enable: true,
        distance: 150,  // 粒子间连线的距离
        color: "#ffffff",  // 粒子间连线的颜色
        opacity: 0.4,  // 粒子间连线的透明度
        width: 1,  // 粒子间连线的宽度
      },
      move: {
        enable: true,
        speed: 6,  // 粒子运动速度
        direction: "none",
        random: false,
        straight: false,
        out_mode: "out",
        bounce: false,
        attract: {
          enable: false,
          rotateX: 600,
          rotateY: 1200,
        },
      },
    },
    // 交互性的配置
    interactivity: {
      detect_on: "canvas",
      events: {
        onhover: {
          enable: true,
          mode: "repulse",  // 鼠标悬停效果
        },
        onclick: {
          enable: true,
          mode: "push",  // 鼠标点击效果
        },
        resize: true,
      },
      modes: {
        grab: {
          distance: 400,
          line_linked: {
            opacity: 1,
          },
        },
        bubble: {
          distance: 400,
          size: 40,
          duration: 2,
          opacity: 8,
          speed: 3,
        },
        repulse: {
          distance: 200,
          duration: 0.4,
        },
        push: {
          particles_nb: 4,
        },
        remove: {
          particles_nb: 2,
        },
      },
    },
    retina_detect: true,
  });
</script>
```

