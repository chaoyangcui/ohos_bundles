# 项目介绍<a name="ZH-CN_TOPIC_0000001054621862"></a>

## 简介<a name="section469617221261"></a>

为系统内业务组件提供故障、用户行为、功耗统计三类事件打点接口，支持对事件进行序列化。

## 架构<a name="section15884114210197"></a>

1.  事件打点时通过CreateEvent接口先创建一个事件；
2.  通过AddData2Event接口向事件中添加数据；
3.  添加完成后通过ReportEvent接口上报事件；
4.  Event组件检查参数有效性后，对事件进行二进制序列化处理（序列化方案需要与HOS的HiEvent序列化方案兼容，以支持事件在云端统一解析），将事件转换为结构化数据；
5.  Event调用Output组件的OutputEvent接口将事件写入文件，每次新写文件时，先向事件文件中加入公共头信息；
6.  事件上报手机侧的处理由Upload组件被动或主动定时完成；

    **图 1**  Hievent流程图<a name="fig153121737203314"></a>  
    ![](http://tools.harmonyos.com/mirrors/hpm-image/hievent_README/figures/Hievent流程图.png "Hievent流程图")


