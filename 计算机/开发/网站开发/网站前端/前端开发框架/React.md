# React(前端开发框架)

React 是一个用于构建用户界面的 JAVASCRIPT 库

安装：`npm i -g react react-dom`最好全局安装

使用：引入react、react

`npm i -g tar create-react-app`一定全局安装

## JSX

JavaScript XML语法扩展

使用JSX就和HTML一样直观、简洁，但比HTML更严格，因此：

推荐使用 `const element = <h1>Hello, world!</h1>;`

而不是 `const element = React.createElement('h1', nll, 'hello world')`

您的组件也无法返回多个JSX标记。您必须将它们包装到共享的父级中 `<br />`、`<div></div>`、`<></>`

同时标签必须有结束符，如：`<br />`、`<img />`

```xml

    <>

      <h1>About</h1>

      <p>Hello there.<br/>How do you do?</p>

    </>

```

JSX 允许使用大括号“转义”到 JavaScript 中，以便您可以从代码中嵌入一些变量并将其显示给用户

```xml

      <img

        className="avatar"

        src={user.imageUrl}

        alt={'Photo of ' + user.name}

        style={{

          width: user.imageSize,

          height: user.imageSize

        }}

      />

```
