# 网络爬虫

当想获取网站的数据，而网站没有提供API或有限制时，可以使用网络爬虫技术

**网络爬虫的合法性**：

使用[[../../语言/编程语言/python/python|Python3]]进行爬虫开发

## 网站

### robots.txt

[robots.txt](https://www.robotstxt.org/)是一个君子协定，告诉搜索引擎，你可以爬取收录我的什么页面，不可以爬取和收录我的那些页面。

robots文件必须要存放在网站的根目录下（域名/robots.txt）

```txt
user-agent:用户代理
Disallow:禁止爬取的目录
```

### Sitemap网站地图

网站提供的[Sitemap](https://www.sitemaps.org/)文件可以帮助爬虫定位网站最新的内容

### 识别网站技术

detectem模块

Docker splash、cli

### 网站所有者

`pip install python-whois`

```python
import whois
print(whois.whois('xxx.com'))
```

## 基础爬虫

### urllib库

#### 下载网页

```python
import urllib.request

def download(url):
    return urllib.request.urlopen(url).read()
```

如果网页出错，可以修改代码捕获urllib抛出的异常：

```python
import urllib.request
from urllib.error import URLError, HTTPError, ContentTooShortError

def download(url):
    print('Downloading:', url)
    try:
        html = urllib.request.urlopen(url).read()
    except (URLError, HTTPError, ContentTooShortError) as e:
        print('Download error:', e.reason)
        html = None
    return html
```

#### 重试下载

当异常是5xx错误时有可能是暂时性的，给代码添加自动重试下载功能：

```python
import urllib.request
from urllib.error import URLError, HTTPError, ContentTooShortError

def download(url, num_retries=2):
    print('Downloading:', url)
    try:
        html = urllib.request.urlopen(url).read()
    except (URLError, HTTPError, ContentTooShortError) as e:
        print('Download error:', e.reason)
        html = None
        if num_retries >0:
            if hasattr(e, 'code') and 500 <= e.code <600:
                return download(url, num_retries - 1)
    return html
```

#### 设置用户代理

默认情况下，urllib使用Python-urllib/3.x作为用户代理（其中3.x是当前Python版本号）。
一些网站会默认封禁这个默认的用户代理，因此需要修改：

```python
import urllib.request
from urllib.error import URLError, HTTPError, ContentTooShortError

def download(url, user_agent='wswp', num_retries=2):
    print('Downloading:', url)
    request = urllib.request.Request(url)
    request.add_header('user-agent', user_agent)
    try:
        html = urllib.request.urlopen(url).read()
    except (URLError, HTTPError, ContentTooShortError) as e:
        print('Download error:', e.reason)
        html = None
        if num_retries >0:
            if hasattr(e, 'code') and 500 <= e.code <600:
                return download(url, num_retries - 1)
    return html 
```

查看自己的用户代理：
f12 -网络 -刷新浏览器 -找到并点击要访问的网站 
标头-请求标头 中就有user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36 Edg/113.0.1774.57

```python
headers = {
    'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36 Edg/113.0.1774.57'
}
```

#### 设置字符编码

将二进制转换为字符串数据（一般utf-8）：`response.read().decode('utf-8')`
使用网站维护者在响应头中推荐的编码格式，否则使用utf-8：

```python
    try:
        resp = urllib.request.urlopen(request)
        cs = resp.headers.get_content_charset()
        if not cs:
            cs = 'utf-8'
        html = resp.read().decode(cs)
```

也可以使用chardet库猜测编码格式：

### requests库

[[../../语言/编程语言/python/python#requests（网络爬虫）|requests]]是对urllib库的封装，更加简单易用
下载`pip install requests`

## 数据抓取

正则表达式
`re.findall(r'<td class="w2p_fw">(.*?)</td>', html)`

BeautifulSoup

lxml

## 下载缓存

## 并发下载

## 动态内容

## 表单交互

## 验证码处理

## Scrapy

## 解决问题

### 绕过 Cloudflare

[bypass-cloudflare](https://github.com/bright-cn/bypass-cloudflare?tab=readme-ov-file)

Cloudflare 的[Web应用防火墙（WAF）](https://www.cloudflare.com/application-services/products/waf/)通过其全球网络来保护 Web 应用免受 DDoS 和零日攻击。它能实时阻止攻击，并利用专有算法，根据多种特征来识别并阻止恶意机器人，包括：

- [**TLS 指纹**](https://www.bright.cn/blog/web-data/tls-fingerprinting)：JA3 指纹用来识别客户端及其功能、配置，以验证客户端是否是真实用户。
- **[HTTP/2 指纹](https://www.blackhat.com/docs/eu-17/materials/eu-17-Shuster-Passive-Fingerprinting-Of-HTTP2-Clients-wp.pdf)**：利用 HTTP/2 参数与已知的机器人特征进行匹配。
- **HTTP 细节**：检查头部信息和 Cookie 以识别疑似机器人的配置。
- **JavaScript 指纹**：收集浏览器、操作系统和硬件信息，以区分机器人与真实用户。
- **行为分析**：通过机器学习监测请求频率、鼠标移动、空闲时间等来检测机器人。

一旦 Cloudflare 检测到可疑的机器人活动，就会发起背景 JavaScript 挑战；若无法通过则会要求输入 CAPTCHA。


使用代理解决方案
Cloudflare 会根据同一 IP 发送过多请求来识别并阻止机器人。为避免这一点，可以使用[优质住宅代理](https://www.bright.cn/proxy-types/residential-proxies)。但如果对方还会检测 User-Agent，则需要进行相应的伪造。

伪造 HTTP 头
[HTTP 头](https://www.bright.cn/blog/web-data/http-headers-for-web-scraping)可以暴露客户端的详细信息。Cloudflare 会利用它们来区分真实浏览器和只发送少数头部信息的爬虫。大多数爬虫工具都允许你修改头部来模拟真实浏览器。常见的头部包括：

User-Agent 头会暴露所用浏览器与操作系统。
Referer 头来验证请求的来源
Accept 头用于声明客户端可处理的内容类型。

实施 CAPTCHA 解决服务
当其他检测手段都无法确定客户端是否可信时，Cloudflare 可能会向可疑客户端展示 CAPTCHA。它的 Turnstile 系统通常提供轻量级的无交互挑战，但在必要时也会切换为需人工输入的交互式 CAPTCHA。很多服务使用真人或其他方式来解决这些验证码。可参阅我们的[最佳 CAPTCHA 解决方案](https://www.bright.cn/blog/web-data/best-captcha-solvers)文章，筛选最适合自己的服务。

---


1.user-agent
2.封ip（短时间访问次数过多等不合理的行为）
3.验证码
4.动态加载网页
5.数据加密

---

编码解码

UNICODE

import parse
可以将中文转换为对应unicode编码
urllib.parse.quote('')
url = 'https://www.baidu.com/s?wd='

```a
search = urllib.parse.quote('计算机')
url = url + seach
```

如果要转换多个中文参数

data = {
    'wd':'周杰伦'
    'sex':'男'
}

data = urllib.parse.urlencode(data)
url = url + data

---

f12 网络 找接口sug
post请求的参数必须编码为二进制
request = urllib.request.Request(url='*url地址*',data='*post请求的参数*',headers='*请求头*')

url = 'https://fanyi.baidu.com/sug'

data = {
    'kw':'spider'
}

data = urllib.parse.urlencode(data).encode('utf-8')

request = urllib.request.Request(url=url,data=data,headers=headers)

可以发现返回的是json结构，因此：
import json

obj = json.loads(content)
print(obj)

**请求头**

有时ua也不能返回正确的数据
用同样的方法得到完整的请求头：
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,zh-HK;q=0.7,en-GB;q=0.6,en-US;q=0.5
Acs-Token: 1685816822934_1685816842086_McWk7oIn1dUXO27lBjap4nCd8tlP90GnHes+YTW0iDDQCHTw1h1qCrSkfQB3jkgjmOX25AfhgwW5dxqT3jSYusj5TVawZlyc5ybnjZIGK9OMApZf6GCPw0SsA8fTwgvviEY8ffmKZLHNIPlj/QMLoOTX5H/g/q0Nq8fPmq3CR5z2vxCje3B4T7QeFRZzE2y49g8TzkQ2TseVAQ+uqw0+bc95uqE16dcHBMpNNY9tmNN0Y6sJU2s2w+PeEtV4XgHSzq7tm4sNHi5VpiOcGfmc90OfU3O9ig+qbpCK9NDj/+1km7qOyo9nj3m+totMikLw/FkTns9yhlxWsVshLeUByMtR0t9VfpXKQCElChRfr2Bt7nzYaOvCXuDvrb7RObW2IZc6IcRGrjAdHl/DxqkkEUKkx8mAom4MVUAsnN3At5kfKZ3AbI7dTMDMhGaFPsidQuoTn8YOrlwR2Iu/4511CNtPRjQZrUCJEBExEsauBV4GBVR2ZwxoL4qjhbCVTcCXtM3iCJFR7Bgtb8v8J6+aCQ==
Connection: keep-alive
Content-Length: 153
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: BIDUPSID=1253FB2CA3931415DB8494657CE6B52A; PSTM=1628423774; __yjs_duid=1_7a446c7712bfa66fa85cf7fb9e2fca141628623980117; BDUSS=lmeWZyMVFmZklCOUtsT242dzNiUnA5a1ZMMlVSeUJGNTgwUWo3aVlsVjFpRzVpRVFBQUFBJCQAAAAAAQAAAAEAAADt7MkUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHX7RmJ1-0ZiRm; BDUSS_BFESS=lmeWZyMVFmZklCOUtsT242dzNiUnA5a1ZMMlVSeUJGNTgwUWo3aVlsVjFpRzVpRVFBQUFBJCQAAAAAAQAAAAEAAADt7MkUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHX7RmJ1-0ZiRm; REALTIME_TRANS_SWITCH=1; FANYI_WORD_SWITCH=1; HISTORY_SWITCH=1; SOUND_SPD_SWITCH=1; SOUND_PREFER_SWITCH=1; BAIDU_WISE_UID=wapp_1668874030305_692; BAIDUID=8098E37881913930D9EEB66DCB594605:FG=1; APPGUIDE_10_0_2=1; __bid_n=18750e75ed392163b85de0; BAIDUID_BFESS=8098E37881913930D9EEB66DCB594605:FG=1; ZFY=T8JOatPxONa7N7hbSuqzB6ZSwbxM:BPmWcEV:BnaJeDFI:C; delPer=0; PSINO=7; H_PS_PSSID=38516_36543_38687_38540_38797_38767_38810_38821_38751_38639_38764_26350_38619; BA_HECTOR=05ah2k00842ga1a5a081812s1i7muvf1m; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; kleck=ecbb536e4d8bc81ffad294f236559d01; APPGUIDE_10_6_2=1; Hm_lvt_64ecd82404c51e03dc91cb9e8c025574=1685164020,1685816672; Hm_lpvt_64ecd82404c51e03dc91cb9e8c025574=1685816826; ab_sr=1.0.1_ODk0MWIzMGIwNDE3YWUyMjczZWExMTcxOGUwMjkzNGQwZjgwOWNhOWI3ODBjYmRkNTNiODEwNzNlMDc0YTQxMTAzNzY5YWJlZGU3ZDMxMDI3MWFmZDcxZjJlNjdhOTExM2RlZTY0NDAyMGU4NDc4NjBkYzQ0NDFkZTgzZTM2YmExM2U4ZDMzNDg1OWM4ZGZmOWJjZjA2MGY1ODljOTAxZjJlN2Y5MTNhMzJmN2Q3ZDA3ZDFiMTFkNTdhMDc5OGQ1
Host: fanyi.baidu.com
Origin: https://fanyi.baidu.com
Referer: https://fanyi.baidu.com/
sec-ch-ua: "Microsoft Edge";v="113", "Chromium";v="113", "Not-A.Brand";v="24"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36 Edg/113.0.1774.57
X-Requested-With: XMLHttpRequest

其中accept-encoding: gzip, deflate, br和
以冒号开头的
要删掉
可以用正则表达式查找(.*): (.*)、替换'$1':'$2',转换为字典形式

不过大多数网站只需要cookie和user-agent就足够了

---

ajax的get

保存json数据
open默认使用gbk编码，要保存汉字请指定utf-8编码
fp = open('douban.json', 'w', encoding='utf-8')
fp.write(content)

with open('douban.json', 'w', encoding='utf-8') as fp:
    fp.write(content)

保存前10页（ajax）
观察接口的规律，然后用循环

def create_request(page):
    base_url = 'https://movie.douban.com/j/chart/top_list?type=11&interval_id=100%3A90&action=&'
    data = {
        'start': (page - 1) * 20,
        'limit': 20
    }
    data = urllib.parse.urlencode(data)
    url = base_url + data

    headers = {
        'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36 Edg/113.0.1774.57'
    }

    request = urllib.request.Request(url=url, headers=headers)
    return request

def get_content(request):
    response = urllib.request.urlopen(request)
    content = response.read().decode('utf-8')
    return content

def download(page, content):
    with open('douban_' + str(page) + '.json', 'w', encoding='utf-8') as fp:
        fp.write(content)

if __name__ == '__main__':
    start_page = int(input('起始的页面'))
    end_page = int(input('结束的页面'))

    for page in range(start_page, end_page+1):
        request = create_request(page)
        content = get_content(request)
        download(page, content)

获取的json数据在vscode中可以使用shift+alt+f格式化

ajax的post相似

可以在标头看请求方式get/post
有X-Requested-With: XMLHttpRequest说明是ajax

---

异常
1.实际开发中不能直接讲代码的报错抛给用户，而是通过异常处理的形式给出提示。2.如果有异常不处理，程序会挂起，异常后的代码都不会执行。这样影响实际程序的使用。

1.虽然try....except捕捉了异常 ，程序不会报代码的错误。但是注意异常代码后面的代码不会执行了，可以用try...finally替代。

2.一个 try 语句可能包含多个except子句，分别来处理不同的特定的异常。但只有一个分支会被执行，类似else

3.如果在执行try子句的过程中发生了异常，那么try子句余下的部分将被忽略。如果异常的类型和 except 之后的名称相符，那么对应的except子句将被执行。最后执行 try 语句之外的代码。

import urllib.error

try:
    可能出错的地方
except urllib.error.HTTPError:
    print('http错误')
except urllib.error.URLError:
    print('url错误')


如上一个案例可改为：

for page in range(start_page, end_page+1):
        try:
            request = create_request(page)
            content = get_content(request)
            download(page, content)
        except urllib.error.HTTPError:
             print('爬取第' + str(page) + '页时出现http错误')
        except urllib.error.URLError:
             print('爬取第' + str(page) + '页时出现url错误')

---

**cookie登陆**
需要绕过登陆，进入页面

cookie
referer
使用登陆后的cookie

**handler**
动态cookie、代理 不能定制

代理(可以使用快代理的免费代理)
proxies = {
    'http':'60.167.102.111:1133'
}
handler = urllib.request.ProxyHandler(proxies=proxies)
opener = urllib.request.build_opener(handler)
response = opener.open(request)
content = response.read().decode('utf-8')

代理池(增加随机性，不容易被封)

import random

proxies_pool = [
    {'http':'60.167.102.111:1133'},
    {'http':'114.232.110.10:8888'}
]

proxies = random.choice(proxies_pool)

---

xpath

浏览器插件xpath helper帮助确认xpath路径，如果只需要文本数据，甚至可以直接在插件中复制粘贴
f12 元素 右键可以直接复制xpath

必须有结束标签
安装lxml

from lxml import etree

本地文件tree = etree.parse('文件路径')
服务器响应文件tree = etree.HTML(response.read().decode('UTF-8'))
tree.xpath(xpath路径)

nodename

选取此节点的所有子节点

/

从当前节点选取直接子节点

//

从当前节点选取子孙节点

.

选取当前节点

. .

选取当前节点的父节点

@

选取属性

*

任何元素

* 通配符
/	从根节点选取（取子节点）。
//	从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置（取子孙节点）。
@class	选取属性。
[@id=""]
[@class=""]
text() 获取标签中内容

模糊查询
//div[contains(@id,"he")]
//div[start-with(@id,"he")]
内容查询
//div/h1/text()
逻辑运算
//div[@id="head" and @class="s_down"]
//title | //price

---

selenium
**驱动真实的浏览器**
下载相应浏览器驱动
edge<https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/>
Chrome<http://chromedriver.storage.googleapis.com/index.html>
解压得到.exe文件，不需要任何操作，移动到py文件夹下即可
下载的浏览器驱动器放在Python 安装路径下的 Scripts 目录
如果你不知道你的python解释器所在文件夹在哪，可以在命令行输入：py -0p（会显示出python解释器所在文件夹）

在函数内执行的浏览器操作，在函数执行完毕之后，程序内所有的步骤都结束了，关于这段程序的进程也就结束了，浏览器包含在内；如果将浏览器全局后，打开浏览器不在函数内部，函数里面的程序执行完是不会关闭浏览器的。
把打开浏览器的操作放在函数外部/设置全局driver = ''/设置option.add_experimental_option("detach", True)
浏览器厂家提供的浏览器源生驱动文件（chromedriver.exe）自身逻辑设置引起的，方法运行完会自动关闭回收方法中定义的局部变量dr。如果不想让自动关闭方法中的局部变量对象dr，可以像代码3那样在变量名称前加个global声明下这是全局变量dr，或者把dr的定义像代码1那样定义到方法体的外面相当于全局变量。
最新的4.9.1自动关闭浏览器，改为4.1.1就可以

from selenium import webdriver 
from selenium.webdriver.common.by import By

driver = webdriver.Edge()

def baidu():
    url = 'https://www.baidu.com'
    driver.get(url)
    driver.find_element(By.ID, 'kw').send_keys('你好')
    driver.find_element(By.ID, 'su').click()


baidu()

元素定位
from selenium.webdriver.common.by import By

driver.find_element(By.XPATH,'XPATH')
driver.find_element(By.CLASS_NAME,'CLASS_NAME')
driver.find_element(By.CSS_SELECTOR,'CSS_SELECTOR')
driver.find_element(By.ID,'ID')
driver.find_element(By.LINK_TEXT,'LINK_TEXT')
driver.find_element(By.PARTIAL_LINK_TEXT,'PARTIAL_LINK_TEXT')
driver.find_element(By.TAG_NAME,'TAG_NAME')
如果你查找的是多个元素，只需要将其中的find_element替换成find_elements即可。

js是javascript，是可以独以运行的脚本；不使用selenium的方法，进行页面元素的点击、输入、拖拽等等操作，像如果对js使用很熟练，那么也就完全不需要管上面的定位方式。全部可以使用js来实现页面元素的各种操作。
像滚动条拖拽是没法用元素定位操作的，只能使用js
.execute_script('')

控制浏览器操作
控制浏览器窗口大小
driver.set_window_size(480, 800)

浏览器后退，前进
后退 driver.back()

前进 driver.forward()

刷新
driver.refresh() # 刷新

driver.find_element_by_id("kw").clear() # 清楚文本 driver.find_element_by_id("kw").send_keys("selenium") # 模拟按键输入 driver.find_element_by_id("su").click() # 单机元素
可以在搜索框模拟回车操作search_text = driver.find_element_by_id('kw') search_text.send_keys('selenium') search_text.submit()
size： 返回元素的尺寸。

text： 获取元素的文本。

get_attribute(name)： 获得属性值。

is_displayed()： 设置该元素是否用户可见。

perform()： 执行所有 ActionChains 中存储的行为；
context_click()： 右击；
double_click()： 双击；
drag_and_drop()： 拖动；
move_to_element()： 鼠标悬停。

key_down(Keys.SHIFT)
.key_up(Keys.SHIFT)

保存图片：
可以调用urllib或request
免二次请求，selenium直接保存图片可以通过selenium的execute_script方法，注入一段脚本令网页所有img都转换为base64格式，如此一来图片的二进制信息就被编码为base64写在了`<img>`的src属性中。

from selenium.webdriver.common.action_chains import ActionChains



每一个浏览器访问网站时，都会带上特定的指纹特征，网站会解析这些特征，从而判断这次访问是不是自动化程序。

一个最广为人知的特征是window.navigator.webdriver，该特征直接标明此浏览器是webdriver程序。当一个浏览器通过selenium启动后，在开发者工具中输入这个属性，会发现被标为 true， 而手工打开的浏览器是 false。
实际上，浏览器被检测为webdriver程序的特征并不止这一个，这意味着，就算你通过修改属性，也不一定能绕过网站的检测。

我们可以通过 sannysoft <https://bot.sannysoft.com/>来检测浏览器指纹，如果浏览器是通过selenium等自动化程序打开的，访问这个网址后会有很多特征暴露这些指纹，这些特征的值和手工打开后的值是不一样的，因此可以很轻易被别人检测出来。

execute_cdp_cmd(self, cmd, cmd_args)方法可以用来执行Chrome开发这个工具命令。
cdp即Chrome DevTools Protocal, Chrome开发者工具协议
https://chromedevtools.github.io/devtools-protocol/tot/Emulation

execute_cdp_cmd('Page.addScriptToEvaluateOnNewDocument',{'source':"""Object.defineProperty(navigator, 'webdriver', {get: () => undefined})"""})

from selenium.webdriver.support.wait import WebDriverWait

WebDriverWait(driver, timeout=3).until(some_condition)
WebDriverWait(driver, timeout=3).until(lambda d: d.find_element(By.TAG_NAME,"p"))

控制已经打开的浏览器

命令行
start msedge.exe --remote-debugging-port=9527 --user-data-dir="F:\selenium"
9527 "F:\selenium" 可自定义

import os
os.popen(r'start msedge.exe --remote-debugging-port=9527 --user-data-dir="F:\selenium"') # 环境变量 os.system

或者直接转换到egde可执行文件路径下，可以edge://version/查看
os.chdir(r'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe')
os.popen('msedge --remote-debugging-port=9527 --user-data-dir="F:\selenium"')

不过一般不这么做，因为我们并不需要每次打开新的浏览器。

可以创建一个快捷方式，目标为`"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" --remote-debugging-port=9527 --user-data-dir="F:\selenium"`

```python
from selenium import webdriver
from selenium.webdriver.edge.options import Options

op = Options()
op.add_experimental_option('debuggerAddress','127.0.0.1:9527')
dr = webdriver.Edge(options=op)
```

---

requests

import requests

url = ''
response = requests.get(url=url) # RESPONSE类型
response.text
response.url
response.content
response.status_code
response.headers


headers{

}
data = {}
response = requests.get(url=url,params=data,headers=headers)
content = response.text

response = request.post(url,headers,data,proixies)

---

淘宝
图片 产品名称 价格

---