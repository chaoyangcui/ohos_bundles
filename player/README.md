# Player\_README

# 模块介绍<a name="ZH-CN_TOPIC_0000001054622027"></a>

音视频播放模块支持音视频播放业务的开发，主要包括音视频文件和音视频流播放、音量和播放进度控制等。

在进行应用的开发前，开发者应了解以下基本概念：

-   流媒体技术

    流媒体技术是把连续的影像和声音信息进行编码处理后放在网络服务器上，让浏览者一边下载、一边观看与收听，而不需要等整个多媒体文件下载完成就可以即时观看、收听的技术。


-   视频帧率

    帧率是用于测量显示帧数的度量，帧数就是在每秒钟时间里传输的图片数量。每秒钟帧数 \(FPS\) 越多，所显示的画面就会越流畅。

-   码率

    码率就是数据传输时单位时间传送的数据位数，常用单位是kbps即千位每秒。

-   采样率

    采样率为每秒从连续信号中提取并组成离散信号的采样个数，单位用赫兹（Hz）来表示。


# 安装指导<a name="ZH-CN_TOPIC_0000001054063391"></a>

播放相关动态库安装到设备/usr/lib中

# 使用说明<a name="ZH-CN_TOPIC_0000001054383351"></a>

1.  实现PlayerCallback回调，通过SetPlayerCallback函数进行绑定，用于事件处理。

    ```
    class TestPlayerCallback : public PlayerCallback{ 
        void OnPlaybackComplete() override 
        { 
            //此处实现代码用于处理文件播放完成的事件 
        } 
        void OnError(int32_t errorType, int32_t errorCode) override 
        { 
            //此处实现代码处理错误事件 
        } 
        void OnInfo(int type, int extra) override 
        { 
            //此处实现代码处理普通事件 
        } 
        void OnRewindToComplete() override 
        { 
            //此处实现代码处理进度控制完成的事件 
        } 
    };
    
    ```

2.  创建Player实例，设置播放源并开始播放。

    ```
    Player *player = new Player(); 
    std::shared_ptr<PlayerCallback> callback = std::make_shared<TestPlayerCallback>(); 
    player->SetPlayerCallback(callback);//设置player回调 
    std::string uri(filePath);//此处filePath为本地文件路径 
    Source source(uri);//保存uri到source实例 
    player->SetSource(source);//将source设置到player 
    player->SetVideoSurface(surface);//设置播放窗口
    player->Prepare();//准备播放 
    player->Play();//开始播放
    ```

3.  根据场景需要进行播放控制。

    ```
    player->SetVolume(lvolume, rvolume);//设置左右声道声音 
    player->EnableSingleLooping(true);//设置循环播放 
    player->Pause();//暂停 
    player->Play();//继续播放
    ```

4.  播放任务结束后，进行资源释放。

    ```
    player->Stop(); //停止播放
    player->Release();//释放资源
    ```




