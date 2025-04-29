# wallpaperengine

软件的使用十分简单，主要记录壁纸制作方法
*设置——常规——热键——可以设置alt+x隐藏桌面图标*

参考官方文档：[Wallpaper Engine - Designer Documentation](https://docs.wallpaperengine.io/en/)

在软件左下角打开壁纸编辑器
把文件拖入壁纸编辑器，会自动在 `wallpaper_engine\projects\myprojects\` （workshop上下载的壁纸所在的的文件夹为`\SteamLibrary\steamapps\workshop\content\431960`）下创建项目副本和一个`project.json` 文件（储存壁纸有关信息）
在 编辑——更改项目设置 中可以修改项目名称以及设置预览图片或GIF

## Scene Wallpapers 场景壁纸

图片：jepg、png、tga、gif
Wallpaper Engine 支持不同类型的资产，最常见的是图像、文本层、粒子系统、声音甚至 3D 模型。

打开壁纸引擎编辑器后，您将看到编辑器的欢迎界面。您只需将想要动画化的图片拖放到“创建壁纸”按钮中即可开始
在您开始导入任何图像之前，请首先确保您的主要背景图像代表一个真实的屏幕分辨率。本指南中使用的示例图像为 1920 x 1080，这是计算机屏幕上最常用的分辨率。

**给图片层添加效果**：
我们将首先使用水波纹效果来动画化水面：
在右侧，点击效果部分中的添加按钮。一个弹出窗口将打开，您可以从其中查看所有已安装的效果。选择水波纹效果，并通过点击确定按钮进行确认。
我们可以通过绘制不透明度蒙版来限制效果只作用于图像的水域。在添加效果后，点击不透明度蒙版部分中的画笔按钮。
绘画时，您可以在左下角使用value值（目前在编辑器中被翻译为数量）和size大小滑块。通过降低值，您可以降低您绘制区域中水波纹的感知强度。将其设置为 0，可以完全擦除您意外绘制覆盖的任何区域。遮罩将通过显示值较低的区域较暗和值较高的区域较亮来表示这些变化。
尝试擦除任何不需要的区域，例如意外生成的海岸线区域，通过将强度设置为 0 并逐渐减少远处水波的强度。这将产生比在所有地方都涂上最大值更为逼真的效果。

为图片中的树线添加摇摆效果，模仿风吹动树木：
像之前一样在效果区域点击添加按钮，添加树叶摇摆效果。可以降低速度并稍微调整方向
类似可以创建蒙版。

创建云移动动画：
使用水流效果来动画化云朵。与之前两种效果不同，这种效果没有不透明度蒙版，而是有一个流动图。

**图层添加组件**：
Wallpaper Engine 支持不同类型的资产组件，最常见的是图像、文本层、粒子系统、声音甚至 3D 模型。点击编辑器顶部的“创意工坊”——“在创意工坊浏览组件”，可以订阅组件

首先，点击屏幕左侧的“添加资产”按钮。这将打开默认安装的所有资产的概览。点击“光束”，选择“光束 1（旧版）”，并按视频下所示点击“确定”进行确认。
使用句柄移动、旋转和缩放组件

文本层可以包含动态内容，需要了解场景脚本知识。我们将使用时钟预设，这是一个可以轻松添加到您壁纸的可配置时钟，是一个文本层。和之前一样，点击左侧的添加资源按钮，从列表中选择时钟预设，并确认选择。
将字体更改为“Alcubierre”，这是默认字体之一。我们还略微减小了点大小值，这是字体的大小。对于文本层，我们通常建议使用此属性更改大小，而不是像之前处理光束那样更改实际的比例，这会导致最佳的字体渲染并增加字体的清晰度。
由于时钟依赖于 SceneScript，在编辑器中时钟实际上不会运行，它只会显示一个静态预览（默认为 12:34）。您可以通过点击编辑器顶部的运行预览按钮来打开时钟，或者在添加时钟或预览壁纸后预览壁纸。

壁纸引擎还允许你在资产列表中创建层次结构。这使你能够将资产附加到另一个父资产上。如果父资产被移动、旋转或缩放，其所有子资产也会相应地变化。
创建层次结构，只需将一个资产拖放到列表中的另一个资产的右侧上即可

**添加用户选项**：
壁纸引擎允许用户通过用户属性进一步自定义您的壁纸。用户属性让您可以为用户提供选项，进一步调整和自定义壁纸的各个细节，包括完全隐藏壁纸中的对象。

**场景选项**：
镜头抖动

绑定用户属性
编写脚本

**发布壁纸**：
点击编辑器顶部的“创意工坊”并选择“在创意工坊上分享壁纸”来启动上传过程。这完全是可选的

### 木偶变形

皮影扭曲是使用壁纸引擎为角色和一些物体创建复杂动画的高级方法。皮影扭曲是一个多步骤的过程，需要您拥有一个单独的图像层，其中包含您想要动画化的角色或物体的剪影。

1. 创建和导入适合木偶扭曲的卡通人物剪影。
2. 建立角色的几何形状。
3. 创建角色的骨架。
4. 通过改变角色的“权重”来改善角色的肢体。
5. 动画化角色。
6. 将角色放置到场景中。

编辑操作变形：
自动创建几何图形。您可以使用细分滑块增加网格的细分数量。
几何设置提供了一些高级设置，允许您微调木偶扭曲的几何形状。通过点击“锁定顶点编辑的几何形状”按钮，您可以锁定自动生成的几何形状，并通过“编辑拓扑”功能重新排列几何网格来进一步修改它。但如果您对生成的网格满意，通常可以跳过此步骤。

在建立角色的整体几何形状后，我们现在需要告诉壁纸引擎角色模型中哪些关节是可移动的，在编辑器中这些关节被称为骨骼。点击角色扭曲概述中的骨骼部分创建按钮开始操作。
您可以定义多个骨骼和一到多个根骨骼，这些根骨骼将作为动画中的参考点。您可以通过在角色上点击特定点来创建骨骼，Wallpaper Engine 将在最后一个骨骼和当前骨骼之间绘制连接。如果您首先选择一个骨骼然后创建新的骨骼，连接将在这两个点之间创建。还可以通过高级设置进一步调整骨骼的行为，但这些功能仅限于更高级的教程。
根骨骼用于定义质心或几乎不可移动的点。通常，您会将其设置在角色的中心或脚部。通常，每个角色或对象只应使用一个根骨骼，但如果您正在处理包含多个独立对象或角色的图像，则应为每个对象或角色创建一个根骨骼。

下一步是定义我们角色的各个肢体/“区域”。一旦骨骼配置完成，您可以在“权重”部分点击“编辑”按钮。壁纸引擎将尝试识别壁纸的不同肢体和区域，每个肢体和区域都由一个与之前步骤中创建的特定骨骼相关联的单独颜色表示。“权重”定义了每个骨骼对角色每个点的具体影响程度。

最后一步是创建木偶扭曲过程中的动画。这是通过在创建的单独骨骼上使用时间轴动画来完成的。您可以通过点击木偶扭曲概述中的“创建”按钮，然后在动画列表中点击“添加”按钮来开始。可以为一个对象创建多个动画
移动下方动画窗口中的动画帧，改变骨骼位置自动创建关键帧
由于我们正在使用循环模式动画，因此我们将在每个骨骼的第一帧和最后一帧创建关键帧，就像我们开始时做的那样，以确保动画始终从结束的地方开始，以防止任何突然跳转到第一帧。

可以对多个图像层进行上述操作，以实现更精美的效果。

### repkg

壁纸引擎 PKG 解包器/TEX 转换器

[repkg](https://github.com/notscuffed/repkg/releases)

打开Wallpaper,右键需要导出.mpkg文件的壁纸
选择->预渲染.高性能。视频裁剪->保存原始宽高
将.mpkg文件导出保存到repkg.exe所在文件夹下
新建文本文件，输入下面内容

```bat
@echo off
setlocal

for /f "delims=" %%F in ('dir /b *.mpkg') do (
    set "name=%%F"
    goto :found
)
:found

set "basename=%name%"

ren "%basename%" "scene.pkg"

.\RePKG.exe extract .\scene.pkg

del scene.pkg

endlocal
```

修改后缀名为bat，双击运行
将.mpkg文件变成MP4格式保存到output文件夹中，并删除原.mpkg文件

## Web Wallpapers 网页壁纸

通过 [[../语言/其他语法/HTML,CSS|HTML,CSS]]和 [[../语言/编程语言/JavaScript/JavaScript|JavaScript]]创建壁纸
确保在开始导入之前，将您的 HTML 文件和所有相关文件放置在专用的项目文件夹中。
各个文件夹和文件的位置对于项目根目录来说没有硬性要求，但为了良好的编程习惯，建议将对应的文件和文件夹整理成合理的结构


```text
.
└── myprojects
		├── images
		├── js
		├── css
		├── font
		└── index.html
```

将项目根目录的index.html拖入wallpaper编辑器新建项目小窗即可，wallpaper将自动导入inedx.html同级目录的所有文件

壁纸引擎公开了您可以使用它来为基于网页的壁纸添加额外功能的接口：用户自定义、音频可视化、支持硬件的 RGB 效果、用户可配置的帧率限制等。视频文件也可以成为您基于网页的壁纸的一部分，尽管仅支持.webm、.ogg 和.ogv 视频文件。
创建基于网络的壁纸时，除非绝对必要，请避免从网络加载任何重要的壁纸文件。您应将任何图像、HTML、CSS 和 JavaScript 文件（包括 JavaScript 框架）与您的壁纸捆绑在一起，以确保所有文件都本地加载。这确保了如果用户暂时离线或服务器因任何原因无法访问，您的壁纸不会损坏。

### 用户自定义属性

壁纸引擎允许您通过向项目中添加所谓的用户属性，使壁纸的部分可由用户配置。当用户在壁纸引擎已安装标签页中选择您的壁纸时，这些用户属性将显示在右侧。

您可以在 Wallpaper Engine 编辑器中打开您的网页项目，导航到顶部菜单的“编辑”选项，并选择“更改项目设置”。然后，您可以点击“添加属性”按钮创建新的属性。

 颜色（ `color` ）：颜色选择器
滑块（ `slider` ）：允许用户在指定范围内选择数字的滑块
复选框（ `bool` ）：一个处于开启或关闭状态的复选框
组合（ `combo` ）：一个下拉选择器，每个元素都有一个文本和一个隐藏的值
文本输入框（ `textinput` ）
文件（ `file` ）：用于导入图片或视频的文件选择器
目录（ `directory` ）：用于批量导入图片或视频文件的目录选择器

您可以使用 wallpaperPropertyListener 和其 `applyUserProperties` ，该监听器会在用户更改您添加到壁纸的属性或壁纸首次加载时触发。该事件仅包含已更改值的属性，因此始终检查属性是否包含在内很重要，如下例所示（ `yourproperty` 和 `anotherproperty` 应替换为您的属性的实际键）。

```js
window.wallpaperPropertyListener = {
    applyUserProperties: function(properties) {
        if (properties.yourproperty) {
            // Do something with yourproperty
        }
        if (properties.anotherproperty) {
            // Do something with anotherproperty
        }
        // Add more properties here
    },
};
```

```js
if (properties.customcolor) {
     // Convert the custom color to 0 - 255 range for CSS usage
     var customColor = properties.customcolor.value.split(' ');
     customColor = customColor.map(function(c) {
         return Math.ceil(c * 255);
    });
    var customColorAsCSS = 'rgb(' + customColor + ')';
    // Do something useful with the value here or assign it to a global variable
}
if (properties.customtext) {
    var mySliderValue = properties.customtext.value;
    // Do something useful with the value here or assign it to a global variable
}
if (properties.customslider) {
    var mySliderValue = properties.customslider.value;
    // Do something useful with the value here or assign it to a global variable
}
if (properties.customcheckbox) {
    var mySliderValue = properties.customcheckbox.value;
    // Do something useful with the value here or assign it to a global variable
}
if (properties.customcombo) {
    var mySliderValue = properties.customcombo.value;
    // Do something useful with the value here or assign it to a global variable
}
if (properties.customimage) {
    // Read the file
    var customImageFile = 'file:///' + properties.customimage.value;
}
if (properties.customrandomdirectory) {
    //customrandomdirectory 配置ID
    if (properties.customrandomdirectory.value) {
        // Directory set
    } else {
        // No directory set
    }
}
```

#### 属性显示条件

特别地，如果您添加了大量属性，属性列表可能会迅速变得难以导航，对用户来说。使用显示条件，您可以有条件地隐藏某些属性，并且仅在它们相关时才显示它们。
例如，假设您已经在您的壁纸中添加了一个时钟，并且想要为您的壁纸添加两个选项：一个选项可以完全禁用时钟，另一个选项可以在 24 小时制和 12 小时制时钟系统之间切换。在这种情况下，当时钟被禁用时隐藏 24 小时选项是有意义的，因为在这种情况下，该选项对用户来说不再相关。
在我们的情况下，我们希望将可见性依赖于 `showclock` 的值，因此我们将显示条件设置为依赖于该属性的 `value` 为 `true` ：

```js
showclock.value == true
```

#### 属性翻译

您可以为您的属性和属性值创建翻译，以便您的网页壁纸更容易被全球观众访问。壁纸引擎将根据壁纸引擎设置中的“常规”选项卡中配置的语言动态加载适当的语言。

翻译属性时，打开 `project.json` 并添加一个新对象 `localization` 到 `properties` 旁边。此对象包含每个语言的简写符号成员（检查 `wallpaper_engine` 安装目录下的 `locale` 目录中的文件，以获取所有当前可用的语言）。
确保所有标签都以 `ui_` 开头，否则壁纸引擎将无法识别它们为可翻译标记。

```json
{
    "file" : "index.html",
    "general" : 
    {
        "properties" : 
        {
            "backgroundcolor" : 
            {
                "index" : 0,
                "options" : 
                [
                    {
                        "label" : "ui_background_color_red",
                        "value" : "255 0 0"
                    },
                    {
                        "label" : "ui_background_color_green",
                        "value" : "0 255 0"
                    },
                    {
                        "label" : "ui_background_color_blue",
                        "value" : "0 0 255"
                    }
                ],
                "order" : 100,
                "text" : "ui_backgroundcolor",
                "type" : "combo",
                "value" : "255 0 0"
            },
        },
        "localization" : 
        {
            "en-us" :
            {
                "ui_backgroundcolor" : "Background color",
                "ui_background_color_red" : "Red",
                "ui_background_color_green" : "Green",
                "ui_background_color_blue" : "Blue"
            },
            "de-de" :
            {
                "ui_backgroundcolor" : "Hintergrundfarbe",
                "ui_background_color_red" : "Rot",
                "ui_background_color_green" : "Grün",
                "ui_background_color_blue" : "Blau"
            },
            "zh-chs" :
            {
                "ui_backgroundcolor" : "背景颜色",
                "ui_background_color_red" : "红色",
                "ui_background_color_green" : "绿色",
                "ui_background_color_blue" : "蓝色"
            }
        },
    },
    "title" : "Test Project",
    "type" : "web"
}
```

### 音频可视化

壁纸引擎允许您处理左右音频通道的音量级别，并使用这些级别来可视化用户系统上正在播放的音频。每个通道将音频频率分为 64 部分。每一部分代表音频的一个频率范围：低频代表低音，高频代表高音音域。

以下示例提供了一个非常基本的音频可视化预览的完整实现。您可以轻松地将此内容复制粘贴到一个空的 `.html` 文件中，导入到壁纸引擎中，它应该立即工作。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <style>
        body { margin:0; padding:0; }
        html, body { width:100%; height:100%; overflow:hidden; }
        canvas { height:100vh; width:100vw }
    </style>
    </head>
    <body>
        <canvas id="AudioCanvas"></canvas>
        <script>
        let audioCanvas = null;
        let audioCanvasCtx = null;
        function wallpaperAudioListener(audioArray) {
            // Clear the canvas and set it to black
            audioCanvasCtx.fillStyle = 'rgb(0,0,0)';
            audioCanvasCtx.fillRect(0, 0, audioCanvas.width, audioCanvas.height);

            // Render bars along the full width of the canvas
            var barWidth = Math.round(1.0 / 128.0 * audioCanvas.width);
            var halfCount = audioArray.length / 2;

            // Begin with the left channel in red
            audioCanvasCtx.fillStyle = 'rgb(255,0,0)';
            // Iterate over the first 64 array elements (0 - 63) for the left channel audio data
            for (var i = 0; i < halfCount; ++i) {
                // Create an audio bar with its hight depending on the audio volume level of the current frequency
                var height = audioCanvas.height * Math.min(audioArray[i], 1);
                audioCanvasCtx.fillRect(barWidth * i, audioCanvas.height - height, barWidth, height);
            }

            // Now draw the right channel in blue
            audioCanvasCtx.fillStyle = 'rgb(0,0,255)';
            // Iterate over the last 64 array elements (64 - 127) for the right channel audio data
            for (var i = halfCount; i < audioArray.length; ++i) {
                // Create an audio bar with its hight depending on the audio volume level
                // Using audioArray[191 - i] here to inverse the right channel for aesthetics
                var height = audioCanvas.height * Math.min(audioArray[191 - i], 1);
                audioCanvasCtx.fillRect(barWidth * i, audioCanvas.height - height, barWidth, height);
            }
        }

        // Get the audio canvas once the page has loaded
        audioCanvas = document.getElementById('AudioCanvas');
        // Setting internal canvas resolution to user screen resolution
        // (CSS canvas size differs from internal canvas size)
        audioCanvas.height = window.innerHeight;
        audioCanvas.width = window.innerWidth;
        // Get the 2D context of the canvas to draw on it in wallpaperAudioListener
        audioCanvasCtx = audioCanvas.getContext('2d');

        // Register the audio listener provided by Wallpaper Engine.
        window.wallpaperRegisterAudioListener(wallpaperAudioListener);
        </script>
    </body>
</html>
```

### 帧率限制

性能在壁纸方面非常重要，您应该确保在您的网页壁纸中渲染任何复杂内容时，使用帧率限制。
您可以使用 wallpaperPropertyListener 来获取用户配置的当前帧率限制。当您的壁纸加载时以及用户更改应用程序的常规配置时，此事件会被触发。

### RGB 硬件支持

## Video Wallpapers  视频壁纸

直接把mp4文件拖入壁纸编辑器即可

## exe应用壁纸

直接把exe文件拖入壁纸编辑器即可
