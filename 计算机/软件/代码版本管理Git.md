# Git

[Git](https://git-scm.com/downloads/win)  是代码版本管理⼯具，⽤于记录代码修改历史、创建分⽀、合并分⽀等。

记录每⼀段代码的改动，如果出现问题或者想查看之前的版本， 可以找到任意时间点的代码状态

版本控制、分⽀管理、分布式

## Git 常⽤命令

|   功能  |   命令  |
| --- | --- |
|  配置用户名和邮箱   |  `git config --global user.name 'lain'`</br>`git config --global user.email 'lain@email.com'`|
|查看git配置|`git config --list`|
|初始化仓库|`git init`|
|添加文件到暂存区| `git add 文件名`|
|提交到本地仓库| `git commit -m "提交说明"` |
|推送代码到远程仓库 |`git push origin 分支名`|
|克隆(下载)远程仓库| `git clone 仓库地址`|
|查看状态 |`git status`|
|查看提交历 史 |`git log`|
|创建分支 |`git branch 分支名`|
|切换分支 |`git checkout 分支名`|
|合并分支 |`git merge 分支名`|
|拉取代码 |`git pull origin 分支名`|

可以add某个文件，某个文件夹，或直接add当前仓库下所有文件

```shell
git add 单个文件
git add 文件夹1/ 文件夹2/ ……多个文件夹之间空格隔开
git add .
```

创建一个临时分支以备恢复git branch backup-branch

git log --oneline
git log 输入q回车退出

Git 的 reflog 记录了所有 HEAD 的变动。你可以通过以下命令找到之前的状态git reflog

回退代码到某次 commit `git reset --hard <commit-hash>`

修改最近一次commit的信息 `git commit --amend`

修改最近两个或者两次上的commit信息 `git rebase -i HEAD~2` git rebase -i --root
在弹出的编辑器中，将需要修改的提交前的pick改为edit，然后保存退出。
修改`git commit --amend`
继续当前的 rebase`git rebase --continue`
中止当前的 rebase git rebase --abort
跳过当前的提交git rebase --skip
重复此过程直到所有需要修改的提交都被更新

修改最近一次提交的作者信息git commit --amend --reset-author
完成所有修改后，需要强制推送更改到远程仓库-f
git push origin master --force

查看所有本地和远程 Git 的分支名称`git branch -a`

将本地的 main 分支上的更改推送到名为 origin 的远程仓库 git push origin master:master
如果本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数git push --force origin master

github以前是使用master作为默认分支，后来变成了main（master这个词带有种族歧视的含义）
重命名 master 分支为 main： git branch -m master main   git push -u origin main（-u 参数可以设置远程仓库为默认的上游仓库，这样在未来运行 git push 或 git pull 时，就无需指定远程仓库和分支）
全局方式修改默认分支git config --global init.defaultBranch main
也可以在Github中设置创建仓库时默认的分支名称  `Settins`—`Repositories`改回master

```text
git init //把这个目录变成Git可以管理的仓库
　　git add README.md //文件添加到仓库
　　git add . //不但可以跟单一文件，还可以跟通配符，更可以跟目录。一个点就把当前目录下所有未追踪的文件全部add了 
　　git commit -m "first commit" //把文件提交到仓库
　　git remote add origin git@github.com:timetimes/qsatest.git //关联远程仓库
　　git push -u origin master //把本地库的所有内容推送到远程库上
```

git remote -v

ssh: connect to host github.com port 22: Connection refused
修改 SSH 配置文件来使用端口 443
打开或创建 ~/.ssh/config 文件。
添加以下内容： 

```text
Host github.com
Hostname ssh.github.com
Port 443
```

使用 HTTPS 协议
git remote rm origin
git remote add origin https://github.com/username/repo.git

DNS 配置
清除 DNS 缓存： $ ipconfig /flushdns
修改 hosts 文件，添加 GitHub 的 IP 地址： 140.82.113.4 github.com

假设你在开发一个功能，但只完成了一半，你不想将这些半成品代码提交到版本库。这时，你接到了另一个紧急需求，需要立即处理。你可以使用 _git stash_ 来保存当前的工作进度，然后切换到新的分支去处理新的需求。处理完新需求后，你可以通过 _git stash pop_ 将之前的工作进度恢复到工作区，继续之前的工作。

## GitHub

[GitHub](https://github.com/)：全球化的代码社交云平台

|  功能   |    GitHub   |
| --- | --- |
|   Fork  |  复制项目到个人账户   |
|Star|收藏项目，便于以后查找|
|Watch|订阅项目动态|
|Issues|提交问题或建议，记录开发中的待办事项|
|Pull Request| 提交代码修改供原项目合并|
|Actions| 自动化 CI/CD 工作流 |
|Pages |托管静态网站（如博客或文档）|
|Releases |发布稳定版本，提供下载|
|Webhooks |自动消息通知|

SSH：安全认证和便捷连接
SSH 允许在本地和远程仓库之间安全通信，并省去每次推送或拉取代码时输⼊密码的⿇烦。

```bash
# 配置个⼈信息
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"

# 使⽤ RSA 算法⽣成 SSH 密钥
ssh-keygen -t rsa -C "你的邮箱"
```

添加公钥到远程仓库
GitHub：进⼊ Settings > SSH and GPG keys > New SSH key，粘贴公钥并保存。

测试连接
`ssh -T git@github.com`
如果出现port 22: Connection refused，可以尝试指定端口为443：
`ssh -T -p 443 git@ssh.github.com`

*如果同时使⽤ GitHub 和 Gitee，可以为它们配置不同的 SSH 密钥。 在 ~/.ssh/config ⽂件中添加以下内容*：

```bash
Host github.com
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa

Host gitee.com
	HostName gitee.com
	User git
	IdentityFile ~/.ssh/id_rsa_gitee
```

复制仓库地址 git@github.com:timetimes/qsatest.git

使用Pull Request合并分支
创建拉取请求：在GitHub仓库页面，点击“Pull requests”标签，然后点击“New pull request”按钮。
选择基础分支和比较分支：选择你想合并到的基础分支（通常是master或main分支）和你想合并的比较分支。
检查变更：查看两个分支间的差异，确认你想要合并的更改。
创建拉取请求：点击“Create pull request”，输入标题和描述，然后再次点击“Create pull request”按钮。
代码审查：其他团队成员可以在拉取请求页面上审查代码，并提出意见或建议。
解决冲突（如果有）：如果存在合并冲突，你需要在本地解决冲突，然后推送更改到GitHub。
合并拉取请求：一旦得到审查批准，并解决了所有冲突，点击“Merge pull request”按钮，然后点击“Confirm merge”完成合并

本地合并分支
切换到目标分支：在你的本地仓库中，切换到你想要合并到的分支。 git checkout main
合并分支：使用merge命令合并另一个分支。 git merge feature-branch
解决冲突（如果有）：如果合并过程中出现冲突，需要手动解决冲突，然后提交更改。
推送更改到GitHub：将合并后的更改推送回GitHub。 git push origin main

点击main下拉菜单，点击view all branches可以删除分支

github下载加速网站：
https://gh-proxy.com/
[Github Proxy 文件代理加速](https://github.akams.cn/)

## 其他命令

更新git版本
git --version检查 Git 的当前版本
linux：
sudo apt-get update
sudo apt-get install git
windows：
对于 2.14.1 之前的版本，请从系统中卸载 Git，然后从头开始安装最新版本 Git
git update对于从 2.14.2 到 2.16.1 的版本
git update-git-for-windows 对于 2.16.1 版本

**只克隆Git仓库中的子目录**

首先，创建一个空的目录作为新的仓库，并初始化Git仓库：

```bash
mkdir new-repo
cd new-repo
git init
```

然后，使用以下命令配置Git仓库以启用`git sparse-checkout`特性，并克隆指定的子目录：

```bash
git remote add origin <repository-url>
git config core.sparsecheckout true
echo "<subdirectory-path>" >> .git/info/sparse-checkout
git pull origin master
```

`<repository-url>`是Git仓库的URL，`<subdirectory-path>`是你想克隆的子目录的路径

全局禁用 SSL 证书验证
git config --global http.sslVerify false
重新启用
git config --global http.sslVerify true
