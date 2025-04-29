# ai

## ai围棋等

## ai绘画

stable diffusion+controlNet

文生图

图生图：
ai生成二维码

## chat

## ai声音

RVC（Retrieval based Voice Conversion）是一个开源工具，它基于VITS（Voice Inverse Text-to-Speech）语音合成系统，能够实现实时声音变换。
https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI
N卡用户请下载RVCXXXXNvidia.7z
A卡I卡用户请下载RVXXXXAMD_Intel.7z

hugging face下载地址: 
Hugging Face 是一个知名的开源库和平台，专注于机器学习和人工智能领域。它提供了丰富的预训练模型、工具和资源，帮助开发者和研究人员更高效地进行深度学习任务 
https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main  

虚拟声卡软件（如果有声卡则不用）
voicemeeter推荐:https://voicemeeter.com/ 提供两条虚拟线路，还可以混音，有控制面板
vbcable https://vb-audio.com/Cable/ 只提供虚拟线路，每个安装程序提供一条线路
声音设置-录制，界面第一条通道选择麦克风（格式一般MME延迟低）
声音设置-播放，界面A1中选择播放设备
A是监听；B是输出。第一条通道是本音；第三条通道是变音
安装后在 声音设置-录制，把虚拟设备设置为默认（声卡同理设为默认即可）

打开RVC图形界面（go-realtime-GUI.bat），输入设备选择麦克风，输出设备选择虚拟声卡的虚拟通道(VoiceMeeter Input (VB-Audio VoiceMeeter VAIO) (Windows DirectSound))。男变女调高音调；女变男降低音调；性别不变则不用变，然后点击开始转换即可。

安卓使用RVC：声卡+OTG线+手机
电脑声卡+转换器+手机
安卓模拟器（安卓拨号软件）

B站up制作的[入梦AI变声器](https://rmsys.top/AI.html)