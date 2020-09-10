# AudioManager\_README

# 项目介绍<a name="ZH-CN_TOPIC_0000001054622017"></a>

## 简介<a name="section469617221261"></a>

音频管理模块支持对音频数据的采集和播放，即音频输入输出模块。

在进行应用的开发前，开发者应了解以下基本概念：

-   流媒体技术

    流媒体技术是把连续的影像和声音信息进行编码处理后放在网络服务器上，让浏览者一边下载、一边观看与收听，而不需要等整个多媒体文件下载完成就可以即时观看、收听的技术。


-   视频帧率

    帧率是用于测量显示帧数的度量，帧数就是在每秒钟时间里传输的图片数量。每秒钟帧数 \(FPS\) 越多，所显示的画面就会越流畅。

-   码率

    码率就是数据传输时单位时间传送的数据位数，常用单位是kbps即千位每秒。

-   采样率

    采样率为每秒从连续信号中提取并组成离散信号的采样个数，单位用赫兹（Hz）来表示。


## 目录<a name="section1464106163817"></a>

音频管理模块源代码目录结构如下图所示：

**表 1**  音频模块源代码目录结构

<a name="table2977131081412"></a>
<table><thead align="left"><tr id="row7977610131417"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p18792459121314"><a name="p18792459121314"></a><a name="p18792459121314"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p77921459191317"><a name="p77921459191317"></a><a name="p77921459191317"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row17977171010144"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p2793159171311"><a name="p2793159171311"></a><a name="p2793159171311"></a>foundation/multimedia/frameworks/audio_lite</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p879375920132"><a name="p879375920132"></a><a name="p879375920132"></a>音频模块实现</p>
</td>
</tr>
<tr id="row6978161091412"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p992717142910"><a name="p992717142910"></a><a name="p992717142910"></a>foundation/multimedia/interfaces/kits/audio_lit</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p6793059171318"><a name="p6793059171318"></a><a name="p6793059171318"></a>音频模块对外头文件</p>
</td>
</tr>
</tbody>
</table>

# 使用说明<a name="ZH-CN_TOPIC_0000001054063379"></a>

请参考player和recorder模块readme。

