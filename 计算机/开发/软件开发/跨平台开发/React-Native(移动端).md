# React Native(移动端跨平台开发框架)

必须安装的依赖有：React、[Node](https://nodejs.cn/)、[JDK11](https://www.oracle.com/java/technologies/downloads/#java11) 和 Android Studio。
虽然你可以使用任何编辑器来开发应用（编写 js 代码），但你仍然必须安装 Android Studio 来获得编译 Android 应用所需的工具和环境。

**搭建开发环境**：

`npm i -g react`

1. **安装 Android Studio**
   安装界面中选择"Custom"选项，确保选中了以下几项：
   `Android SDK`、`Android SDK Platform`、`Android Virtual Device`
2. **安装 Android SDK**
   Android Studio 默认会安装最新版本的 Android SDK。目前编译 React Native 应用需要的是Android 13 (Tiramisu)版本的 SDK（注意 SDK 版本不等于终端系统版本，RN 目前支持 android 5 以上设备）。你可以在 Android Studio 的 SDK Manager 中选择安装各版本的 SDK。
   在 SDK Manager 中选择"SDK Platforms"选项卡，然后在右下角勾选"Show Package Details"。展开Android 13 (Tiramisu)选项，确保勾选了下面这些组件：`Android SDK Platform 33`、Intel x86 Atom_64 System Image 然后点击"SDK Tools"选项卡，同样勾中右下角的"Show Package Details"。展开"Android SDK Build-Tools"选项，确保选中了 React Native 所必须的33.0.0版本。你可以同时安装多个其他版本。最后点击"Apply"来下载和安装这些组件。
3. **配置 ANDROID_HOME 环境变量**
   React Native 需要通过环境变量来了解你的 Android SDK 装在什么路径，从而正常进行编译。
   可以在 Android Studio 的"Preferences"菜单中查看 SDK 的真实路径 `~\sdk`
4. **添加到环境变量 Path**
   把这些工具目录路径添加进去：
   `%ANDROID_HOME%\platform-tools`
   `%ANDROID_HOME%\emulator`
   `%ANDROID_HOME%\tools`
   `%ANDROID_HOME%\tools\bin`

**创建新项目**
如果你之前全局安装过旧的react-native-cli命令行工具，请使用 `npm uninstall -g react-native-cli`卸载掉它以避免一些冲突
使用 React Native 内建的命令行工具来创建一个新项目。
这个命令行工具不需要安装，可以直接用 node 自带的npx命令来使用：`npx react-native@latest init 项目文件夹`，可选项目版本 `--version X.XX.X`
当然也可以安装后使用（推荐）：`npm i -g react-native`、`react-native init 文件夹`
*请不要在路径中使用中文、空格等特殊符号（特别注意的是不能在‘桌面’下）。请不要单独使用常见的关键字作为项目名（如 class, native, new, package 等等）。请不要使用与核心模块同名的项目名（如 react, react-native 等）*

**编译并运行 React Native 应用**
*建议使用系统自带的cmd运行*
确保你先运行了模拟器或者连接了真机，
模拟器打开ADB，可以看见端口号，输入 `adb connect 127.0.0.1:5575`（蓝叠模拟器）连接
手机打开USB调试，连接数据线即可
可以使用 `adb devices`确认
*出现emulator-5574   device可能是其他应用调用adb.exe导致,进程管理器中找到adb.exe结束即可(adb kill-server)*

npm start Gradle build daemon disappeared unexpectedly (it may have been killed or may have crashed) 如果你熟悉 Web 开发，Metro 很像 webpack——对于 React Native 应用程序。与 Kotlin 或 Java 不同，JavaScript 不是编译的，React Native 也不是。捆绑与编译不同，但它可以帮助提高启动性能，并将一些特定于平台的 JavaScript 转换为更广泛支持的 JavaScript。

然后在项目文件夹下，`react-native start`，根据提示输入即可。此时打开[android](http://localhost:8081/index.bundle?platform=android)应该可以看见代码
运行没有反应可能因为第一次运行时需要下载大量编译依赖，而网络连接有问题，国内可使用阿里云提供的[maven镜像](https://developer.aliyun.com/mvn/view)将android/build.gradle中的

```gradle
    repositories {
        google()
        mavenCentral()
    }
```

替换为

```gradle
    repositories {
        maven { url 'https://maven.aliyun.com/repository/google' }
        maven { url 'https://maven.aliyun.com/repository/public' }
    }
```

不行可能是8081端口被占用，可以删除进程：`netstat -aon|findstr "8081"`、`tasklist|findstr 上一步查询的PID`、`taskkill /f /t /im 上一步查询的进程`
或者指定其他端口：`npm start -- --port=8088`、`yarn start --port 8088`

## 错误

Execution failed for task ':app:installDebug'.
关闭usb验证应用，并且安装时在手机上点击确认安装

ReferenceError: SHA-1 for file C:\Users\dom\AppData\Roaming\npm\node_modules\react-native\node_modules\metro-runtime\src\polyfills\require.js (C:\Users\dom\AppData\Roaming\npm\node_modules\react-native\node_modules\metro-runtime\src\polyfills\require.js) is not computed.
并且手机上安装的应用出现红屏
npm up
