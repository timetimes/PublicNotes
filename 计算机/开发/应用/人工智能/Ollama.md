# Ollama

Ollama 是一款开创性的人工智能（AI）和机器学习（ML）工具平台，它极大地简化了 AI 模型的开发和使用过程。

Ollama 能自动识别并充分利用 Windows 系统中的最优硬件资源。无论你是配备了 NVIDIA GPU、AMD GPU，还是 CPU 支持 AVX、AVX2 这样先进的指令集，Ollama 都能实现针对性优化，确保 AI 模型更加高效地运行。
在进行 AI 开发时，以往常常需要搭建虚拟机或配置复杂的软件环境，而 Ollama 无需虚拟化
Ollama 为用户提供了丰富的 AI 模型库

## 在 Windows 上使用 Ollama

1. 访问 [Ollama Windows](https://ollama.com/download/windows) 页面，下载`OllamaSetup.exe`安装程序并安装（或[Ollama github](https://github.com/ollama/ollama/releases)）
2. 点击 Ollama 图标，运行后会在任务栏托盘中驻留一个图标
3. 执行命令 `ollama run [modelname]` 来运行 Ollama，并加载模型。Ollama 将开始初始化，并自动从 Ollama 模型库中拉取并加载所选模型。
	具体模型名称可以参考文档[Ollama model](https://ollama.com/search)
5. 加载好文本模型后，就可以直接在命令行里输入文字开始与模型「对话」
	如果你想使用图像处理模型，如 LLaVA 1.6，可以使用以下命令来加载该模型：ollama run llava1.6
6. 连接到 Ollama API：我们不可能只通过命令行来使用，将应用程序连接到 Ollama API 是一个非常重要的步骤。
	Ollama API 的默认地址是http://localhost:11434，可以在安装 Ollama 的系统中直接调用
	如果要在网络中提供服务，可以修改 API 的侦听地址和端口
	Ollsma API 默认无访问限制，可以修改API访问范围，让API仅监听本地回环地址：`ollama serve --host 127.0.0.1`
	或者使用防火墙屏蔽11434端口
7. 安装图形化界面[open webUI](https://docs.openwebui.com/)，需要先下载[[../../../软件/容器Docker|容器Docker]]。默认端口3000
	局域网调用： https://局域网ip:3000 ，外网可以使用内网穿透或公网ip服务器

```shell
# 查看 Ollama 版本
ollama -v

# 运行模型。如果没有则拉取下载模型
ollama run [modelname]
# 停止模型
ollama stop llama3.2
 
# 列出已安装的模型
ollama list
# 列出当前加载的模型
ollama ps
 
# 删除指定模型
ollama rm [modelname]
# 从模型文件创建模型
ollama create mymodel -f ./Modelfile
# 拉取模型（更新模型）
ollama pull llama3.2
# 复制模型
ollama cp llama3.2 my-model
 
# 模型存储路径
# C:\Users\<username>\.ollama\models

# Ollama API
# 请求
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt": "Why is the sky blue?"
}'
# 响应
{
  "model": "llama3.2",
  "created_at": "2023-08-04T08:52:19.385406455-07:00",
  "response": "The",
  "done": false
}
```

```python
# pip install ollama
# ollama.chat(model='llama3.2', messages=[{'role': 'user', 'content': 'Why is the sky blue?'}])
# ollama.generate(model='llama3.2', prompt='Why is the sky blue?')
# ollama.list()
# ollama.show('llama3.2')
# ollama.delete('llama3.2')
# ollama.ps()

# generate方法
import ollama
prompt = 'Why is the sky blue?'
resp = ollama.generate(model='llama3.2', prompt=prompt).response
print(resp)

# chat方法
import ollama
stream = ollama.chat(
    model='deepseek-coder',
    messages=[{'role': 'user', 'content': '你是谁？'}],
)
print(response['message']['content'])

# 自定义客户端
from ollama import Client
client = Client(
    host='http://localhost:11434',
    headers={'x-some-header': 'some-value'}
)
response = client.chat(model='deepseek-coder', messages=[
    {
        'role': 'user',
        'content': '你是谁?',
    }],
	stream=True,  # 流式响应
)
# 逐块打印响应内容
for chunk in stream:
    print(chunk['message']['content'], end='', flush=True)
```
