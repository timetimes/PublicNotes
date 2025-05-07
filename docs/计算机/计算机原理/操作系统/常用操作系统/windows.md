# windows

## 控制台

[终端控制代码 (ANSI/VT100) Terminal Codes 简介 (转载翻译)_vt100 ansi-CSDN博客](https://blog.csdn.net/NAzi_1911/article/details/120660034)
[控制台虚拟终端序列 - Windows Console | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/console/console-virtual-terminal-sequences)

## powershell

cmd

Cmd中的where命令
在PowerShell中执行where命令无效。 在PowerShell中where命令对应的是Where-Object命令，优先级比where.exe高。CMD里的where命令本来全名就是where.exe，只不过可以省略.exe而已。所以实现需要CMD里的where命令功能显式地使用where.exe。
检查代理程序路径`where.exe python`

以管理员权限运行 CMD
mklink /D C:\Users\dom\.elan\toolchains\my-lean4 C:\Users\dom\.elan\toolchains\stable

在 PowerShell 中使用 `cmd /c`
cmd /c mklink /D C:\Users\dom\.elan\toolchains\my-lean4 C:\Users\dom\.elan\toolchains\stable


Windows 的 CMD 或 PowerShell 默认不会保存永久历史，关闭窗口后就清空了，相比之下，macOS 或 Linux 会保存在 .bash_history 或 .zsh_history 中。
但在同一个会话中你可以：按 ↑ 和 ↓ 键查看历史命令；
cmd：使用 doskey /history 显示当前会话的命令历史。
PowerShell 使用：Get-History

## WSL

[安装 WSL | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/install)

WSL（Windows Subsystem for Linux）是微软开发的一项技术，允许用户在Windows系统中直接运行完整的Linux环境，无需虚拟机。通过操作系统级虚拟化，WSL将Linux子系统无缝嵌入Windows，提供原生Linux命令行工具、软件包管理器及应用程序支持。它具有轻量化、文件系统集成、良好的交互性及开发效率提升等优点，消除了Windows与Linux之间的隔阂，尤其适合开发者和需在Windows平台上使用Linux工具的用户。

在WSL中重置root密码是一个简单的过程。以下是详细步骤：
以管理员身份运行PowerShell： 打开PowerShell并以管理员身份运行。
wsl -s
切换到root用户： 在PowerShell中执行以下命令，将默认用户切换为root： wsl --user root
重置root密码： 运行以下命令来修改root密码： passwd root 输入新密码并确认。
将默认用户切换回普通用户： 如果需要，将默认用户切换回普通用户，使用以下命令： `ubuntu config --default-user <your-username>`

cat ../../../../etc/shadow

1）启用 WSL 功能
打开开始菜单，在开始菜单中输入 启用或关闭 Windows 功能，在弹出的窗口中勾选 虚拟机平台 和 适用于 Linux 的 Windows 子系统，确定之后重启系统。
输入 `wsl --install` 或 `wsl --update` 即可安装 WSL 相关的组件
2） 安装 Ubuntu
打开 Microsoft Store，搜索 Ubuntu下载并启动

1. 使用 [Windows 终端](https://learn.microsoft.com/zh-cn/windows/terminal/install)支持你想要安装的任意数量的命令行，并允许你在多个标签或窗口窗格中打开它们并在多个 Linux 发行版或其他命令行（PowerShell、命令提示符、Azure CLI 等）之间快速切换。 可使用独特的配色方案、字体样式、大小、背景图像和自定义键盘快捷键来完全自定义终端。
2. 使用vscode的终端
3. 通过访问 Windows“开始”菜单并键入已安装的发行版的名称，可以直接打开 Linux 发行版。
4. 在 cmd或 PowerShell 中，可以输入已安装的发行版的名称。

wsl --help 查看帮助

`wsl -l -v` 查看wsl并显示有关所有分发版的详细信息
 wsl -l -o 显示适合通过 'wsl --install' 安装的可用分发版列表

`wsl -d <Distribution Name>`启动分发版
wsl -t 关闭
wsl --shutdown 立即终止所有正在运行的分发版
 
 `wsl -s <Distribution Name>` 将分发版设置为默认值
 wsl -u 用户名 登入默认分发版的用户

wsl --unregister取消注册分发版并删除根文件系统

wsl --update更新wsl
wsl --uninstall卸载wsl

wsl --export Ubuntu-22.04 D:\temp\Ubuntu-22.04.tar备份子系统
wsl --import Ubuntu-22.04 C:\WSL D:\temp\Ubuntu-22.04.tar 还原子系统

通过 \\wsl.localhost\ 访问 Linux 文件时将使用 WSL 分发版的默认用户。 因此，任何访问 Linux 文件的 Windows 应用都具有与默认用户相同的权限。
Linux 访问 Windows 文件
可以直接使用/mnt/{Windows盘符}进入对应的盘中

Ubuntu子系统的文件通常位于 `C:\Users\<你的用户名>\AppData\Local\Packages` 目录下
WSL的配置文件通常位于 `C:\Users\<你的用户名>\.wslconfig`

wsl的Vmmem进程非常占资源，用完wsl及时wsl --shutdown关闭

### 运行 Linux GUI 应用

[使用 WSL 运行 Linux GUI 应用 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/tutorials/gui-apps)

```PowerShell
wsl --update   # 更新
wsl --shutdown # 重启
```

进入发行版终端
安装适用于 Linux 的 Microsoft Edge 浏览器：

```bash
## Setup
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/
sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/edge stable main" > /etc/apt/sources.list.d/microsoft-edge-beta.list'
sudo rm microsoft.gpg
## Install
sudo apt update
sudo apt install microsoft-edge-beta
```

可以输入 `microsoft-edge` 或者在windows“开始”菜单中启动

### 配置远程桌面

sudo apt update
sudo apt upgrade


sudo apt-get install xrdp

Windows 默认的远程桌面服务（RDP）占用 `3389` 端口
sudo nano /etc/xrdp/xrdp.ini
[globals]
port=3390  # 修改此处
sudo service xrdp restart

hostname -I获取ip
RDP输入ip:3390

### 工具

图吧工具箱
DiskGenius   给C盘扩容

## 微软工具

### PowerToys

[Microsoft PowerToys | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/powertoys/)

Microsoft PowerToys 是一组实用工具，可帮助高级用户调整和简化其 Windows 体验，从而提高工作效率。

[Always On Top](https://learn.microsoft.com/zh-cn/windows/powertoys/always-on-top) 使你能够使用快捷键 (⊞ Win+Ctrl+T) 将窗口固定在其他窗口之上。
File Locksmith](https://learn.microsoft.com/zh-cn/windows/powertoys/file-locksmith) 是一个 Windows shell 扩展，用于检查哪些文件正在使用中以及由哪些进程使用。 右键单击 File Explorer 中的一个或多个选定文件，并选择**使用 Locksmith 解锁**。

### Process Monitor

[Process Monitor](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon)）（ProcMon）是微软 Sysinternals 套件中的一款强大的系统级工具，用于监控 **实时的文件系统、注册表、进程和网络活动**。 
下载并解压 `Procmon.zip`

双击运行 `Procmon.exe`（建议右键管理员身份运行）
启动后，默认会显示系统中所有活动，非常多，需要过滤。
- 
点击顶部工具栏的 Filter（过滤器）按钮或按快捷键 `Ctrl + L`
-设置过滤规则，例如要监控 VSCode 是否创建了特定路径下的文件
Path contains C:\Users\YourName\Documents\Projects\ then Include

过滤器设好后，点击工具栏左上角的“开始捕捉”按钮（`Ctrl + E`）
Process Monitor 会实时记录：
- 哪个进程（如 `Code.exe`, `WeChat.exe`, `explorer.exe`）
- 在什么时间
- 访问了什么文件路径
- 是创建、读取、写入，还是删除

点击“停止捕捉”按钮以免日志过多
可右键某一条，选择“Jump To”来查看原始位置
- 

