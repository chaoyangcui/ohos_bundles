# appspawn\_README

# 应用孵化模块<a name="ZH-CN_TOPIC_0000001054063214"></a>

## 简介<a name="section469617221261"></a>

应用孵化模块，appspawn进程，配合轻量级元能力框架子系统，通过轻量级IPC机制接收来自AMS的消息，根据消息解析结果启动元能力进程AbilityMain并赋予其对应权限。

模块二进制部署在/bin/appspawn。

## 目录<a name="section15884114210197"></a>

```
base
├──startup    启动恢复子系统根目录  
└──── services
      ├── appspawn_lite    应用孵化模块
           ├── BUILD.gn    应用孵化模块编译配置
           ├── include     应用孵化模块头文件目录
           ├── LICENSE     开源LICENSE文件
           ├── moduletest  应用孵化模块自测试代码目录
           └── src         应用孵化模块源文件目录
```

## 约束<a name="section12212842173518"></a>

目前仅支持Hi3516DV300和Hi3518EV300版本。



