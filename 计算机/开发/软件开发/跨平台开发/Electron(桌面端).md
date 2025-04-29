# Electron(桌面端跨平台开发框架)

Electron是一个基于 Chromium 和 Node.js 使用 JavaScript、HTML 和 CSS 构建桌面应用程序的框架。
可以仅使用JavaScript创建跨平台应用(windows/linux/macos)

因为相当于塞了Chromium一个浏览器，因此相比原生开发缺点是应用体积大、使用内存多，底层交互性能差

* **安装：**`npm i electron`
* **运行：**
  1. 首先创建一个文件夹并初始化 npm 包`npm init`
  2. 在 package.json 中指定 `"main": "main.js"`作为Electron 应用的入口
  3. 要执行这个脚本，需要在 package.json 的 scripts 字段中添加一个 `"start": "electron ."`。这个命令会告诉 Electron 在当前目录下寻找主脚本，并以开发模式运行它(也可以使用nodemon修改后自动重启，命令改为 `"start": "nodemon --exc electron ."`)
  4. 最后在终端输入 `npm start`运行

npm init
cnpm install --save-dev electron

cnpm install --save-dev @electron-forge/cli
npx electron-forge import