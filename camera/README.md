# Camera\_README

# 介绍<a name="ZH-CN_TOPIC_0000001054063377"></a>

## 基本概念<a name="section175012297491"></a>

相机是HarmonyOS多媒体进程提供的服务之一，提供了相机的录像、预览、拍照功能，支持多用户并发取流。

在进行应用的开发前，开发者应了解以下基本概念：

-   视频帧

    视频流指的是将一系列图片数据按照固定时间间隔排列形成的数据流，每一张图片数据成为一帧，这样的一帧称为视频帧。

-   帧速率\(FPS: Frames Per Second\)

    视频播放每秒钟刷新图片的速度，或是视频每秒的帧数，帧速率越高，视频的观感越流畅。

-   分辨率

    每一帧的图片信息都是由像素点组成的，分辨率描述了一张图片中像素点的个数。例如1920\*1080\(1080P\)，是指图片宽1920像素，高1080像素。


## 运作机制<a name="section193961322175011"></a>

-   多媒体服务进程

    多媒体服务作为系统服务，在系统启动时由Init进程拉起，并初始化和分配媒体硬件资源（内存/显示硬件/图像传感器/编解码器等）。初始化过程解析配置文件，确定了多媒体各个服务的能力和资源上限，通常由OEM厂商通过配置文件进行配置。相机服务在多媒体进程初始化时有以下配置项：

    -   内存池：所有媒体服务依赖于内存池中的内存轮转运行
    -   图像传感器：包括了传感器类型、分辨率、ISP等
    -   图像处理器：分辨率、码率、图像翻转等
    -   图像编码器：编码格式、码率、分辨率等


-   关键类的解释

    应用通过持有下面4个类，配置和使用Camera的功能，包括了Camera类和它的三个异步回调类，三类回调分别对应了不同类型的异步处理场景，详见[表1](#table486418149411)。

    **表 1**  关键类的解释

    <a name="table486418149411"></a>
    <table><thead align="left"><tr id="row19864414104115"><th class="cellrowborder" valign="top" width="22.322232223222326%" id="mcps1.2.4.1.1"><p id="p128641914114112"><a name="p128641914114112"></a><a name="p128641914114112"></a>对象</p>
    </th>
    <th class="cellrowborder" valign="top" width="44.34443444344435%" id="mcps1.2.4.1.2"><p id="p1386471410411"><a name="p1386471410411"></a><a name="p1386471410411"></a>用途</p>
    </th>
    <th class="cellrowborder" valign="top" width="33.33333333333333%" id="mcps1.2.4.1.3"><p id="p1486541484116"><a name="p1486541484116"></a><a name="p1486541484116"></a>举例</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row138651914104113"><td class="cellrowborder" valign="top" width="22.322232223222326%" headers="mcps1.2.4.1.1 "><p id="p1886515147416"><a name="p1886515147416"></a><a name="p1886515147416"></a>Camera</p>
    </td>
    <td class="cellrowborder" valign="top" width="44.34443444344435%" headers="mcps1.2.4.1.2 "><p id="p48653148414"><a name="p48653148414"></a><a name="p48653148414"></a>对相机进行静态配置（通过配置类），触发相机基本功能</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p986510145416"><a name="p986510145416"></a><a name="p986510145416"></a>拍照/录像/预览</p>
    </td>
    </tr>
    <tr id="row98656144413"><td class="cellrowborder" valign="top" width="22.322232223222326%" headers="mcps1.2.4.1.1 "><p id="p13865161412412"><a name="p13865161412412"></a><a name="p13865161412412"></a>CameraDeviceCallback</p>
    </td>
    <td class="cellrowborder" valign="top" width="44.34443444344435%" headers="mcps1.2.4.1.2 "><p id="p1986517141413"><a name="p1986517141413"></a><a name="p1986517141413"></a>处理相机硬件状态变化</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p286531413419"><a name="p286531413419"></a><a name="p286531413419"></a>可用/不可用</p>
    </td>
    </tr>
    <tr id="row167872310411"><td class="cellrowborder" valign="top" width="22.322232223222326%" headers="mcps1.2.4.1.1 "><p id="p196793230419"><a name="p196793230419"></a><a name="p196793230419"></a>CameraStateCallback</p>
    </td>
    <td class="cellrowborder" valign="top" width="44.34443444344435%" headers="mcps1.2.4.1.2 "><p id="p14679823144110"><a name="p14679823144110"></a><a name="p14679823144110"></a>处理camera自身状态变化</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p6679102354112"><a name="p6679102354112"></a><a name="p6679102354112"></a>创建/释放</p>
    </td>
    </tr>
    <tr id="row886581414118"><td class="cellrowborder" valign="top" width="22.322232223222326%" headers="mcps1.2.4.1.1 "><p id="p1865614194116"><a name="p1865614194116"></a><a name="p1865614194116"></a>FrameStateCallback</p>
    </td>
    <td class="cellrowborder" valign="top" width="44.34443444344435%" headers="mcps1.2.4.1.2 "><p id="p1865171420410"><a name="p1865171420410"></a><a name="p1865171420410"></a>处理帧状态的变化</p>
    </td>
    <td class="cellrowborder" valign="top" width="33.33333333333333%" headers="mcps1.2.4.1.3 "><p id="p486541444119"><a name="p486541444119"></a><a name="p486541444119"></a>拍照开始和结束/帧率发生变化</p>
    </td>
    </tr>
    </tbody>
    </table>

-   流的传递

    Surface是多媒体传递音视频的基本数据结构，Camera一般作为Surface中数据的生产者，在不同的场景下有特定的消费者。

    相机的预览和录像输出均为视频流，拍照输出为图像帧，二者均通过Surface类进行传递。Surface类可以屏蔽进程内/跨进程的场景，进行多媒体信息流的传递。

    以录像为例，用户首先创建Recorder实例，并从Recorder中获取对应Surface，再将此Surface传递给Camera实例，此时Camera将作为生产者向Surface注入视频流，而Recorder作为消费者从Surface中取出视频流进行保存，用户的行为类似桥接，把二者通过Surface连接起来。

    类似的，用户也可以自行创建Surface传递给Camera实例，并实现消费者逻辑（例如通过网络传输视频流，或是将拍照的帧数据保存成图片文件）。

    图形图像模块也通过Surface从Camera获取流资源，具体步骤详见[图形图像开发指导](zh-cn_topic_0000001051770388.md)。

-   相机运行流程
    1.  Camera创建流程

        本进程通过CameraManager创建Camera实例，并从服务端绑定camera设备，创建成功后异步通知user。类之间的时序图如下：

        **图 1**  Camera创建时序图<a name="fig9882125184416"></a>  
        

        ![](http://tools.harmonyos.com/mirrors/hpm-image/camera_README/figures/zh-cn_image_0000001054080622.png)


    1.  Camera录像/预览流程

        用户首先通过CameraKit创建Camera，然后FrameConfig类对录像或者预览帧属性进行配置。录像/预览时序如下：

        **图 2**  Camera录像/预览时序图<a name="fig642695404512"></a>  
        

        ![](http://tools.harmonyos.com/mirrors/hpm-image/camera_README/figures/zh-cn_image_0000001054400647.png)



# 安装<a name="ZH-CN_TOPIC_0000001054143316"></a>

相机相关动态库安装到设备/usr/lib中

# 使用<a name="ZH-CN_TOPIC_0000001054302035"></a>

使用场景

使用Camera产生图片帧（拍照）。

接口说明

**表 1**  API列表

<a name="table2069447114914"></a>
<table><thead align="left"><tr id="row4903852104914"><th class="cellrowborder" valign="top" width="14.93%" id="mcps1.2.4.1.1"><p id="p2903252174918"><a name="p2903252174918"></a><a name="p2903252174918"></a>类名</p>
</th>
<th class="cellrowborder" valign="top" width="61.660000000000004%" id="mcps1.2.4.1.2"><p id="p1595113912507"><a name="p1595113912507"></a><a name="p1595113912507"></a>接口名</p>
</th>
<th class="cellrowborder" valign="top" width="23.41%" id="mcps1.2.4.1.3"><p id="p15951597508"><a name="p15951597508"></a><a name="p15951597508"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row492815717494"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1592812716495"><a name="p1592812716495"></a><a name="p1592812716495"></a>CameraKit</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p1492837144919"><a name="p1492837144919"></a><a name="p1492837144919"></a>int32_t GetCameraIdList(std::list&lt;string&gt; cameraList)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p2092807134919"><a name="p2092807134919"></a><a name="p2092807134919"></a>获取cameraId列表</p>
</td>
</tr>
<tr id="row11928157114912"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p139287774911"><a name="p139287774911"></a><a name="p139287774911"></a>CameraKit</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p9928107174915"><a name="p9928107174915"></a><a name="p9928107174915"></a>CameraAbility&amp; GetCameraAbility(string cameraId)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p139281171494"><a name="p139281171494"></a><a name="p139281171494"></a>获取指定camera的能力</p>
</td>
</tr>
<tr id="row119282719496"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p159288734914"><a name="p159288734914"></a><a name="p159288734914"></a>CameraKit</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p99280794913"><a name="p99280794913"></a><a name="p99280794913"></a>void RegisterCameraDeviceCallback(CameraDeviceCallback* callback, EventHandler* handler)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p8928197134910"><a name="p8928197134910"></a><a name="p8928197134910"></a>注册camera设备状态回调</p>
</td>
</tr>
<tr id="row4928673496"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p14928770497"><a name="p14928770497"></a><a name="p14928770497"></a>CameraKit</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p14928197194915"><a name="p14928197194915"></a><a name="p14928197194915"></a>void UnregisterCameraDeviceCallback(CameraDeviceCallback* callback)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p17929197134913"><a name="p17929197134913"></a><a name="p17929197134913"></a>去注册camera设备状态回调</p>
</td>
</tr>
<tr id="row16929187104912"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p6929157184911"><a name="p6929157184911"></a><a name="p6929157184911"></a>CameraKit</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p1192910704914"><a name="p1192910704914"></a><a name="p1192910704914"></a>void CreateCamera(string cameraId, CameraStateCallback* callback, EventHandler* handler)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p12929167154912"><a name="p12929167154912"></a><a name="p12929167154912"></a>创建camera实例</p>
</td>
</tr>
<tr id="row592967184912"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p9929127134915"><a name="p9929127134915"></a><a name="p9929127134915"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p0929107204913"><a name="p0929107204913"></a><a name="p0929107204913"></a>string GetCameraId()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p1592914710490"><a name="p1592914710490"></a><a name="p1592914710490"></a>获取cameraID</p>
</td>
</tr>
<tr id="row13929197104913"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p16929167134913"><a name="p16929167134913"></a><a name="p16929167134913"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p15929175491"><a name="p15929175491"></a><a name="p15929175491"></a>CameraConfig&amp; GetCameraConfig()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p19298714917"><a name="p19298714917"></a><a name="p19298714917"></a>获取camera配置信息</p>
</td>
</tr>
<tr id="row1892918764915"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p69291072495"><a name="p69291072495"></a><a name="p69291072495"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p5930172494"><a name="p5930172494"></a><a name="p5930172494"></a>FrameConfig&amp; GetFrameConfig(int32_t type)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p19301176495"><a name="p19301176495"></a><a name="p19301176495"></a>获取捕获帧类型</p>
</td>
</tr>
<tr id="row893019794915"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p893016714919"><a name="p893016714919"></a><a name="p893016714919"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p1093067134915"><a name="p1093067134915"></a><a name="p1093067134915"></a>void Configure(CameraConfig&amp; config)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p1493037114912"><a name="p1493037114912"></a><a name="p1493037114912"></a>配置camera</p>
</td>
</tr>
<tr id="row11930197174917"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p4930197184914"><a name="p4930197184914"></a><a name="p4930197184914"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p19304717492"><a name="p19304717492"></a><a name="p19304717492"></a>void Release()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p189301479494"><a name="p189301479494"></a><a name="p189301479494"></a>释放camera</p>
</td>
</tr>
<tr id="row109304717499"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p4930873496"><a name="p4930873496"></a><a name="p4930873496"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p1893017720490"><a name="p1893017720490"></a><a name="p1893017720490"></a>int TriggerLoopingCapture(FrameConfig&amp; frameConfig)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p149307754918"><a name="p149307754918"></a><a name="p149307754918"></a>开始循环帧捕获</p>
</td>
</tr>
<tr id="row19306794915"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p6930167194910"><a name="p6930167194910"></a><a name="p6930167194910"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p139311577499"><a name="p139311577499"></a><a name="p139311577499"></a>void StopLoopingCapture()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p693115764914"><a name="p693115764914"></a><a name="p693115764914"></a>停止循环帧捕获</p>
</td>
</tr>
<tr id="row593116713492"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1193187174913"><a name="p1193187174913"></a><a name="p1193187174913"></a>Camera</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p1493111713496"><a name="p1493111713496"></a><a name="p1493111713496"></a>int32_t TriggerSingleCapture(FrameConfig&amp; frameConfig)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p1193137104919"><a name="p1193137104919"></a><a name="p1193137104919"></a>抓图</p>
</td>
</tr>
<tr id="row1693112711491"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p89312716494"><a name="p89312716494"></a><a name="p89312716494"></a>CameraConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p199312784912"><a name="p199312784912"></a><a name="p199312784912"></a>void SetFrameStateCallback(FrameStateCallback* callback, EventHandler* handler);</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p49312714495"><a name="p49312714495"></a><a name="p49312714495"></a>设置帧状态回调</p>
</td>
</tr>
<tr id="row9931076492"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p59317784917"><a name="p59317784917"></a><a name="p59317784917"></a>CameraConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p17931197124912"><a name="p17931197124912"></a><a name="p17931197124912"></a>static CameraConfig* CreateCameraConfig()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p5931177164912"><a name="p5931177164912"></a><a name="p5931177164912"></a>创建camera配置信息实例</p>
</td>
</tr>
<tr id="row29321744917"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1093219716492"><a name="p1093219716492"></a><a name="p1093219716492"></a>CameraAbility</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p12932979493"><a name="p12932979493"></a><a name="p12932979493"></a>std::list&lt;Size&gt; GetSupportedSizes(int format)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p1493210764918"><a name="p1493210764918"></a><a name="p1493210764918"></a>根据类型获取支持输出图像尺寸大小</p>
</td>
</tr>
<tr id="row189321074495"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p2932197124912"><a name="p2932197124912"></a><a name="p2932197124912"></a>CameraAbility</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p493217724915"><a name="p493217724915"></a><a name="p493217724915"></a>std::vector&lt;int32_t&gt; GetSupportedAeMode()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p20932873499"><a name="p20932873499"></a><a name="p20932873499"></a>获取支持的ae模式</p>
</td>
</tr>
<tr id="row1093217710493"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p793227114916"><a name="p793227114916"></a><a name="p793227114916"></a>CameraAbility</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p4932877496"><a name="p4932877496"></a><a name="p4932877496"></a>std::list&lt;uint32_t&gt; GetSupportedParameters()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p89328714913"><a name="p89328714913"></a><a name="p89328714913"></a>获取支持的参数</p>
</td>
</tr>
<tr id="row1193267184910"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1393214717492"><a name="p1393214717492"></a><a name="p1393214717492"></a>CameraAbility</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p119321477495"><a name="p119321477495"></a><a name="p119321477495"></a>std::list&lt;T&gt; GetParameterRange(uint32_t key)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p139331079491"><a name="p139331079491"></a><a name="p139331079491"></a>获取支持的参数范围</p>
</td>
</tr>
<tr id="row593318734911"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p12933147144918"><a name="p12933147144918"></a><a name="p12933147144918"></a>CameraAbility</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p179339710494"><a name="p179339710494"></a><a name="p179339710494"></a>std::list&lt;uint32_t&gt; GetSupportedResults()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p49335784911"><a name="p49335784911"></a><a name="p49335784911"></a>获取支持返回值</p>
</td>
</tr>
<tr id="row1693312712498"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1093313713491"><a name="p1093313713491"></a><a name="p1093313713491"></a>CameraAbility</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p169335784914"><a name="p169335784914"></a><a name="p169335784914"></a>std::list&lt;uint32_t&gt; GetSupportedProperties()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p11933777493"><a name="p11933777493"></a><a name="p11933777493"></a>获取支持的属性</p>
</td>
</tr>
<tr id="row693313718499"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1793318714492"><a name="p1793318714492"></a><a name="p1793318714492"></a>CameraAbility</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p119331677496"><a name="p119331677496"></a><a name="p119331677496"></a>T GetPropertyValue(uint32_t key)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p19933117174911"><a name="p19933117174911"></a><a name="p19933117174911"></a>获取支持的属性对应的值</p>
</td>
</tr>
<tr id="row0933197134920"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1493310764917"><a name="p1493310764917"></a><a name="p1493310764917"></a>CameraDevice</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p493313724915"><a name="p493313724915"></a><a name="p493313724915"></a>CameraDeviceCallback()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p993416724915"><a name="p993416724915"></a><a name="p993416724915"></a>获取指定属性对应的值</p>
</td>
</tr>
<tr id="row12934137134912"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p2093410794920"><a name="p2093410794920"></a><a name="p2093410794920"></a>CameraDevice</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p293414794920"><a name="p293414794920"></a><a name="p293414794920"></a>void OnCameraAccessPrioritiesChanged​(std::string cameraId)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p59341879494"><a name="p59341879494"></a><a name="p59341879494"></a>camera设备构造函数</p>
</td>
</tr>
<tr id="row093418712498"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p159341779492"><a name="p159341779492"></a><a name="p159341779492"></a>CameraDevice</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p1493411774912"><a name="p1493411774912"></a><a name="p1493411774912"></a>void OnCameraStatus​(std::string cameraId, int32_t status)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p1393419715491"><a name="p1393419715491"></a><a name="p1393419715491"></a>camera设备状态变化时的回调</p>
</td>
</tr>
<tr id="row109348711497"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p993419724914"><a name="p993419724914"></a><a name="p993419724914"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p993418720497"><a name="p993418720497"></a><a name="p993418720497"></a>CameraStateCallback​()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p693511794919"><a name="p693511794919"></a><a name="p693511794919"></a>camera状态回调</p>
</td>
</tr>
<tr id="row159358717497"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1992012253527"><a name="p1992012253527"></a><a name="p1992012253527"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p29351077497"><a name="p29351077497"></a><a name="p29351077497"></a>void OnConfigured​(Camera&amp; camera)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p093515774914"><a name="p093515774914"></a><a name="p093515774914"></a>camera配置成功回调</p>
</td>
</tr>
<tr id="row9935147184918"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p117291328135211"><a name="p117291328135211"></a><a name="p117291328135211"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p19935174496"><a name="p19935174496"></a><a name="p19935174496"></a>void OnConfigureFailed​(Camera&amp; camera,int32_t errorCode)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p159352077495"><a name="p159352077495"></a><a name="p159352077495"></a>camera配置失败回调</p>
</td>
</tr>
<tr id="row1935279498"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1514619311525"><a name="p1514619311525"></a><a name="p1514619311525"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p493512744915"><a name="p493512744915"></a><a name="p493512744915"></a>void OnCreated​(Camera&amp; camera)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p1493511784914"><a name="p1493511784914"></a><a name="p1493511784914"></a>camera创建成功回调</p>
</td>
</tr>
<tr id="row189351877493"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p172071933175218"><a name="p172071933175218"></a><a name="p172071933175218"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p129361977498"><a name="p129361977498"></a><a name="p129361977498"></a>void OnCreateFailed​(std::string cameraId,int32_t errorCode)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p2936197114919"><a name="p2936197114919"></a><a name="p2936197114919"></a>camera创建失败回调</p>
</td>
</tr>
<tr id="row49361570491"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p89451235135218"><a name="p89451235135218"></a><a name="p89451235135218"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p693617764911"><a name="p693617764911"></a><a name="p693617764911"></a>void OnFatalError​(Camera&amp; camera,int32_t errorCode)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p119361972491"><a name="p119361972491"></a><a name="p119361972491"></a>camera内部错误回调</p>
</td>
</tr>
<tr id="row20936472491"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p61213391523"><a name="p61213391523"></a><a name="p61213391523"></a>CameraStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p793697174919"><a name="p793697174919"></a><a name="p793697174919"></a>void OnReleased​(Camera&amp; camera)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p49361719495"><a name="p49361719495"></a><a name="p49361719495"></a>camera释放回调</p>
</td>
</tr>
<tr id="row159361179493"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p10936147194918"><a name="p10936147194918"></a><a name="p10936147194918"></a>FrameStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p9936279496"><a name="p9936279496"></a><a name="p9936279496"></a>FrameStateCallback​()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p49367718499"><a name="p49367718499"></a><a name="p49367718499"></a>帧状态回调</p>
</td>
</tr>
<tr id="row1893617744916"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p136968511524"><a name="p136968511524"></a><a name="p136968511524"></a>FrameStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p209379744911"><a name="p209379744911"></a><a name="p209379744911"></a>void OnFrameFinished(Camera&amp; camera, FrameConfig&amp; frameConfig, FrameResult&amp; frameResult)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p19374724913"><a name="p19374724913"></a><a name="p19374724913"></a>拍照帧完成回调</p>
</td>
</tr>
<tr id="row093719718495"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p772975317527"><a name="p772975317527"></a><a name="p772975317527"></a>FrameStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p189371471498"><a name="p189371471498"></a><a name="p189371471498"></a>void OnFrameError​(Camera&amp; camera, FrameConfig&amp; frameConfig, int32_t errorCode, FrameResult&amp; frameResult)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p109371778497"><a name="p109371778497"></a><a name="p109371778497"></a>拍照帧异常回调</p>
</td>
</tr>
<tr id="row10937137174911"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p2640155519527"><a name="p2640155519527"></a><a name="p2640155519527"></a>FrameStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p493718719491"><a name="p493718719491"></a><a name="p493718719491"></a>void OnFrameProgressed​(Camera&amp; camera, FrameConfig&amp; frameConfig, FrameResult&amp; frameResult)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p993797154912"><a name="p993797154912"></a><a name="p993797154912"></a>拍照帧处理中回调</p>
</td>
</tr>
<tr id="row1993720734914"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p4477357205213"><a name="p4477357205213"></a><a name="p4477357205213"></a>FrameStateCallback</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p493797104919"><a name="p493797104919"></a><a name="p493797104919"></a>void OnFrameStarted​(Camera&amp; camera, FrameConfig&amp; frameConfig,long frameNumber,long timestamp)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p6937187174919"><a name="p6937187174919"></a><a name="p6937187174919"></a>拍照帧开始回调</p>
</td>
</tr>
<tr id="row179381979499"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p169381975499"><a name="p169381975499"></a><a name="p169381975499"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p1793867124910"><a name="p1793867124910"></a><a name="p1793867124910"></a>int32_t GetFrameConfigType()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p1993817744915"><a name="p1993817744915"></a><a name="p1993817744915"></a>获取帧配置类型</p>
</td>
</tr>
<tr id="row793817784912"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p69381724914"><a name="p69381724914"></a><a name="p69381724914"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p149382077496"><a name="p149382077496"></a><a name="p149382077496"></a>std::list&lt;HarmonyOS::Surface&gt; GetSurfaces()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p893867114919"><a name="p893867114919"></a><a name="p893867114919"></a>获取帧配置的surface</p>
</td>
</tr>
<tr id="row69388774911"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p39389717494"><a name="p39389717494"></a><a name="p39389717494"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p1193887164919"><a name="p1193887164919"></a><a name="p1193887164919"></a>int32_t GetAeMode()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p11938147204915"><a name="p11938147204915"></a><a name="p11938147204915"></a>获取AE模式</p>
</td>
</tr>
<tr id="row1893819724917"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1393816784919"><a name="p1393816784919"></a><a name="p1393816784919"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p19938673491"><a name="p19938673491"></a><a name="p19938673491"></a>Rect&amp; GetAeRect()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p109391871498"><a name="p109391871498"></a><a name="p109391871498"></a>获取AE位置</p>
</td>
</tr>
<tr id="row1493918784920"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1493915711493"><a name="p1493915711493"></a><a name="p1493915711493"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p293913714492"><a name="p293913714492"></a><a name="p293913714492"></a>int32_t GetImageRotation()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p193914717495"><a name="p193914717495"></a><a name="p193914717495"></a>获取图片旋转状态</p>
</td>
</tr>
<tr id="row593947174913"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p49390718495"><a name="p49390718495"></a><a name="p49390718495"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p159399764917"><a name="p159399764917"></a><a name="p159399764917"></a>T Get(uint32_t key)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p993997184920"><a name="p993997184920"></a><a name="p993997184920"></a>获取指定key对应的值</p>
</td>
</tr>
<tr id="row993977164919"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p89391473492"><a name="p89391473492"></a><a name="p89391473492"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p59393719494"><a name="p59393719494"></a><a name="p59393719494"></a>std::list&lt;uint32_t&gt; GetKeys()</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p189401377499"><a name="p189401377499"></a><a name="p189401377499"></a>获取当前key列表</p>
</td>
</tr>
<tr id="row109401570498"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p294019712492"><a name="p294019712492"></a><a name="p294019712492"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p19940170499"><a name="p19940170499"></a><a name="p19940170499"></a>void AddSurface(HarmonyOS::AGP::UISurface&amp; surface);</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p11940197144915"><a name="p11940197144915"></a><a name="p11940197144915"></a>添加surface</p>
</td>
</tr>
<tr id="row994018711492"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p1094016718493"><a name="p1094016718493"></a><a name="p1094016718493"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p139411279498"><a name="p139411279498"></a><a name="p139411279498"></a>void RemoveSurface(HarmonyOS::AGP::UISurface&amp; surface);</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p39415717494"><a name="p39415717494"></a><a name="p39415717494"></a>删除surface</p>
</td>
</tr>
<tr id="row39411376494"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p12941187154916"><a name="p12941187154916"></a><a name="p12941187154916"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p2094117710491"><a name="p2094117710491"></a><a name="p2094117710491"></a>void SetAeMode(int32_t aeMode, Rect&amp; rect)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p169411675494"><a name="p169411675494"></a><a name="p169411675494"></a>配置AE模式</p>
</td>
</tr>
<tr id="row39411878493"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p109412716491"><a name="p109412716491"></a><a name="p109412716491"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p5941117104918"><a name="p5941117104918"></a><a name="p5941117104918"></a>void SetImageRotation(int32_t degrees)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p169411076498"><a name="p169411076498"></a><a name="p169411076498"></a>配置图片旋转状态</p>
</td>
</tr>
<tr id="row8941187114912"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p0941207114910"><a name="p0941207114910"></a><a name="p0941207114910"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p209413713492"><a name="p209413713492"></a><a name="p209413713492"></a>void SetParameter(uint32_t key, const T value)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p094114764917"><a name="p094114764917"></a><a name="p094114764917"></a>配置指定参数</p>
</td>
</tr>
<tr id="row11942779494"><td class="cellrowborder" valign="top" width="14.93%" headers="mcps1.2.4.1.1 "><p id="p69421777498"><a name="p69421777498"></a><a name="p69421777498"></a>FrameConfig</p>
</td>
<td class="cellrowborder" valign="top" width="61.660000000000004%" headers="mcps1.2.4.1.2 "><p id="p1294277154912"><a name="p1294277154912"></a><a name="p1294277154912"></a>void GetParameter(uint32_t key, const T value)</p>
</td>
<td class="cellrowborder" valign="top" width="23.41%" headers="mcps1.2.4.1.3 "><p id="p5942107204910"><a name="p5942107204910"></a><a name="p5942107204910"></a>获取指定key对应的参数</p>
</td>
</tr>
</tbody>
</table>

约束与限制

无。

开发步骤

1.  实现设备状态回调的派生类，用户在设备状态发生变更（如新插入相机设备/相机掉线）时，自定义操作。

    ```
    class SampleCameraDeviceCallback : public CameraDeviceCallback {
        void onCameraStatus(std::string cameraId, int32_t status) override
        {
            //do something when camera is available/unavailable
        }
    };
    ```

2.  实现帧事件回调的派生类，这里在拿到帧数据以后将其转存为文件。

    ```
    class TestFrameStateCallback : public FrameStateCallback {
        void OnFrameFinished(Camera &camera, FrameConfig &fc, FrameResult &result) override
        {
            cout << "Receive frame complete inform." << endl;
            if (fc.GetFrameConfigType() == FRAME_CONFIG_CAPTURE) {
                cout << "Capture frame received." << endl;
                list<Surface *> surfaceList = fc.GetSurfaces();
                for (Surface *surface : surfaceList) {
                    SurfaceBuffer *buffer = surface->AcquireBuffer();
                    if (buffer != nullptr) {
                        char *virtAddr = static_cast<char *>(buffer->GetVirAddr());
                        if (virtAddr != nullptr) {
                            SampleSaveCapture(virtAddr, buffer->GetSize());
                        }
                        surface->ReleaseBuffer(buffer);
                    }
                    delete surface;
                }
                delete &fc;
            }
        }
    };
    ```

3.  实现相机状态回调的派生类，当相机状态发生变化（配置成功/失败，创建成功/失败\)时，自定义操作。

    ```
    static void SampleSaveCapture(const char *p, uint32_t size)
    {
        cout << "Start saving picture" << endl;
        struct timeval tv;
        gettimeofday(&tv, NULL);
        struct tm *ltm = localtime(&tv.tv_sec);
        if (ltm != nullptr) {
            ostringstream ss("Capture_");
            ss << "Capture" << ltm->tm_hour << "-" << ltm->tm_min << "-" << ltm->tm_sec << ".jpg";
    
            ofstream pic("/tmp/" + ss.str(), ofstream::out | ofstream::trunc);
            cout << "write " << size << " bytes" << endl;
            pic.write(p, size);
            cout << "Saving picture end" << endl;
        }
    }
    
    class TestFrameStateCallback : public FrameStateCallback {
        void OnFrameFinished(Camera &camera, FrameConfig &fc, FrameResult &result) override
        {
            cout << "Receive frame complete inform." << endl;
            if (fc.GetFrameConfigType() == FRAME_CONFIG_CAPTURE) {
                cout << "Capture frame received." << endl;
                list<Surface *> surfaceList = fc.GetSurfaces();
                for (Surface *surface : surfaceList) {
                    SurfaceBuffer *buffer = surface->AcquireBuffer();
                    if (buffer != nullptr) {
                        char *virtAddr = static_cast<char *>(buffer->GetVirAddr());
                        if (virtAddr != nullptr) {
                            SampleSaveCapture(virtAddr, buffer->GetSize());
                        }
                        surface->ReleaseBuffer(buffer);
                    }
                    delete surface;
                }
                delete &fc;
            }
        }
    };
    ```

4.  创建CameraKit，用于创建和获取camera信息。

    ```
    CameraKit *camKit = CameraKit::GetInstance();
    list<string> camList = camKit->GetCameraIdList();
    string camId;
    for (auto &cam : camList) {
        cout << "camera name:" << cam << endl;
        const CameraAbility *ability = camKit->GetCameraAbility(cam);
        /* find camera which fits user's ability */
        list<CameraPicSize> sizeList = ability->GetSupportedSizes(0);
        if (find(sizeList.begin(), sizeList.end(), CAM_PIC_1080P) != sizeList.end()) {
            camId = cam;
            break;
        }
    }
    ```

5.  创建Camera实例。

    ```
    EventHandler eventHdlr; // Create a thread to handle callback events
    SampleCameraStateMng CamStateMng(eventHdlr);
    
    camKit->CreateCamera(camId, CamStateMng, eventHdlr);
    ```

6.  根据[步骤1](zh-cn_topic_0000001050754209.md#li378084192111)、[步骤2](zh-cn_topic_0000001050754209.md#li8716104682913)、[步骤3](zh-cn_topic_0000001050754209.md#li6671035102514)中的回调设计，camera实例创建成功后会进行配置操作，主流程中app需要设计同步机制。

    ```
    void OnCreated(Camera &c) override
    {
        cout << "Sample recv OnCreate camera." << endl;
        auto config = CameraConfig::CreateCameraConfig();
        config->SetFrameStateCallback(&fsCb_, &eventHdlr_);
        c.Configure(*config);
        cam_ = &c;
    }
    
    void Capture()
    {
        if (cam_ == nullptr) {
            cout << "Camera is not ready." << endl;
            return;
        }
        FrameConfig *fc = new FrameConfig(FRAME_CONFIG_CAPTURE);
        Surface *surface = Surface::CreateSurface();
        if (surface == nullptr) {
            delete fc;
        }
        surface->SetWidthAndHeight(1920, 1080); /* 1920:width,1080:height */
        fc->AddSurface(*surface);
        cam_->TriggerSingleCapture(*fc);
    }
    ```




