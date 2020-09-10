# 介绍<a name="ZH-CN_TOPIC_0000001054301947"></a>

## 简介<a name="section11660541593"></a>

**轻量级元能力框架子系统**，是OpenHarmony为开发者提供的一套开发鸿蒙应用的开发框架。轻量级元能力框架子系统由如下模块组成：

**图1**  轻量级元能力框架子系统框架图

![](http://tools.harmonyos.com/mirrors/hpm-image/ability_README/figures/zh-cn_image_0000001054467912.png)

Ability是应用所具备的能力的抽象，一个应用可以包含一个或多个Ability。Ability分为两种类型：FA（Feature Ability）和AA（Atomic Ability）。

-   **FA**：由三方基于元能力框架开发的、实现单一功能的有UI界面的程序实体，用于支持与用户交互的能力。一个Page实例可以包含一组相关页面，每个页面用一个AbilitySlice实例表示。Page模板是Feature Ability唯一支持的模板。用户可以基于JavaScript语言开发FA，也可以基于C/C++语言开发FA。

    -   Page模板的Ability的生命周期流转图

    **图2**  Ability生命周期流转图

    ![](http://tools.harmonyos.com/mirrors/hpm-image/ability_README/figures/zh-cn_image_0000001054627908.png)Page模板的Ability生命周期各状态解析

    -   **UNINITIALIZED**：未初始状态，为临时状态，Ability创建后会直接调用Init初始化，进入INITIAL状态；

    -   **INITIAL**：初始化状态，也表示停止状态，表示当前Ability未运行，调用Start后进入INACTIVE，同时回调开发者的OnSatrt生命周期回调；

    -   **INACTIVE**：未激活状态，表示当前窗口已显示但是无焦点状态，由于Window暂未支持焦点的概念，当前状态与ACTIVE一致。调用Active后进入ACTIVE，同时回调开发者的OnActive生命周期回调；调用Background后进入BACKGROUND，同时回调开发者的OnBackground生命周期回调；

    -   **ACTIVE**：前台激活状态，表示当前窗口已显示，并获取焦点。调用Inactive后进入INACTIVE；

    -   **BACKGROUND**: 后台状态，表示当前Ability退到后台。调用Active后进入ACTIVE，同时回调开发者的OnActive生命周期回调；调用Stop后进入INITIAL，同时回调开发者的OnStop生命周期回调；

    -   **AbilitySlice**

        一个使用Page模板的Ability由AbilitySlice构成，AbilitySlice是单个页面及其控制逻辑的总和。一个Page可以包含多个AbilitySlice，此时，这些页面提供的业务能力应当是高度相关的。Page模板的Ability与AbilitySlice的关系如下图：

        **图3 **Ability与AbilitySlice的关系图

        ![](http://tools.harmonyos.com/mirrors/hpm-image/ability_README/figures/zh-cn_image_0000001054307881.gif)


-   **AA**：由三方基于元能力框架开发的、实现单一功能的无UI界面的支持后台任务的程序实体。AA与FA的区别是，AA无UI界面。仅对系统服务有依赖关系，AA之间不存在依赖关系 。Service模板是AA支持的模板。
-   **注册Ability**

    Ability的模板通过在清单文件中注册时指定。如下所示，开发者可以配置Ability元素的type属性，其取值page、service分别代表Page模板、Service模板。

    ```
    "module": {
           ......
            "abilities": [
                {
    		"name": "default",
    		"type": "pages",
                    "label": "sdfasf"
                }
            ], ’
          ......
     }
    ```


-   **AbilityKit**：元能力的开发框架，运行在开发者的应用程序进程中，和AbilityMs通过IPC通信，开发者基于该框架开发自己的Ability。

-   **AbilityMs**：元能力运行管理服务，元能力生命周期的调度统一由AbilityMs管理。
-   **AppSpawn：**进程孵化器，元能力进程由AppSpawn负责孵化并拉起。

## 目录<a name="section1464106163817"></a>

轻量级元能力框架子系统源代码目录结构如下图所示：

**表 1**  轻量级元能力框架子系统源代码目录结构

<a name="table2977131081412"></a>
<table><thead align="left"><tr id="row7977610131417"><th class="cellrowborder" valign="top" width="36.18%" id="mcps1.2.3.1.1"><p id="p18792459121314"><a name="p18792459121314"></a><a name="p18792459121314"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="63.82%" id="mcps1.2.3.1.2"><p id="p77921459191317"><a name="p77921459191317"></a><a name="p77921459191317"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row17977171010144"><td class="cellrowborder" valign="top" width="36.18%" headers="mcps1.2.3.1.1 "><p id="p2793159171311"><a name="p2793159171311"></a><a name="p2793159171311"></a>foundation/aafwk/frameworks/ability_lite</p>
</td>
<td class="cellrowborder" valign="top" width="63.82%" headers="mcps1.2.3.1.2 "><p id="p879375920132"><a name="p879375920132"></a><a name="p879375920132"></a>元能力框架核心代码</p>
</td>
</tr>
<tr id="row6978161091412"><td class="cellrowborder" valign="top" width="36.18%" headers="mcps1.2.3.1.1 "><p id="p0780163617556"><a name="p0780163617556"></a><a name="p0780163617556"></a>foundation/aafwk/frameworks/want_lite</p>
</td>
<td class="cellrowborder" valign="top" width="63.82%" headers="mcps1.2.3.1.2 "><p id="p6793059171318"><a name="p6793059171318"></a><a name="p6793059171318"></a>元能力之间通信的实体</p>
</td>
</tr>
<tr id="row1897841071415"><td class="cellrowborder" valign="top" width="36.18%" headers="mcps1.2.3.1.1 "><p id="p20749155715720"><a name="p20749155715720"></a><a name="p20749155715720"></a>foundation/aafwk/interfaces/kits</p>
</td>
<td class="cellrowborder" valign="top" width="63.82%" headers="mcps1.2.3.1.2 "><p id="p14793959161317"><a name="p14793959161317"></a><a name="p14793959161317"></a>元能力框架对外接口</p>
</td>
</tr>
<tr id="row965423512587"><td class="cellrowborder" valign="top" width="36.18%" headers="mcps1.2.3.1.1 "><p id="p12654103516589"><a name="p12654103516589"></a><a name="p12654103516589"></a>foundation/aafwk/interfaces/kits/ability_lite</p>
</td>
<td class="cellrowborder" valign="top" width="63.82%" headers="mcps1.2.3.1.2 "><p id="p12658142611466"><a name="p12658142611466"></a><a name="p12658142611466"></a>元能力运行管理服务对外接口</p>
</td>
</tr>
<tr id="row673463115813"><td class="cellrowborder" valign="top" width="36.18%" headers="mcps1.2.3.1.1 "><p id="p127343312581"><a name="p127343312581"></a><a name="p127343312581"></a>foundation/aafwk/interfaces/kits/want_lite</p>
</td>
<td class="cellrowborder" valign="top" width="63.82%" headers="mcps1.2.3.1.2 "><p id="p191041469363"><a name="p191041469363"></a><a name="p191041469363"></a>元能力之间通信的实体对外接口</p>
</td>
</tr>
<tr id="row164593855812"><td class="cellrowborder" valign="top" width="36.18%" headers="mcps1.2.3.1.1 "><p id="p1864523835812"><a name="p1864523835812"></a><a name="p1864523835812"></a>foundation/aafwk/services/abilitymgr_lite</p>
</td>
<td class="cellrowborder" valign="top" width="63.82%" headers="mcps1.2.3.1.2 "><p id="p4645133805811"><a name="p4645133805811"></a><a name="p4645133805811"></a>元能力运行管理服务</p>
</td>
</tr>
<tr id="row35051315317"><td class="cellrowborder" valign="top" width="36.18%" headers="mcps1.2.3.1.1 "><p id="p991413565611"><a name="p991413565611"></a><a name="p991413565611"></a>foundation/aafwk/services/abilitymgr_lite/tools</p>
</td>
<td class="cellrowborder" valign="top" width="63.82%" headers="mcps1.2.3.1.2 "><p id="p0793185971316"><a name="p0793185971316"></a><a name="p0793185971316"></a>元能力调测工具</p>
</td>
</tr>
</tbody>
</table>

## 约束<a name="section1718733212019"></a>

-   语言版本
    -   C++11版本或以上

-   框架针对不同的芯片平台和底层OS能力，规格有所区别
    -   Cortex-M RAM/ROM：
        -   RAM：建议大于20K
        -   ROM:  \> 300K （包含ACE，UIKit及引擎等强相关子系统）

    -   Cortex-A RAM/ROM:
        -   RAM：建议大于2M
        -   ROM：\> 2M （包含ACE，UIKit及引擎等强相关子系统）



# 使用<a name="ZH-CN_TOPIC_0000001054621964"></a>

## 编译轻量级元能力框架子系统<a name="section36321223144015"></a>

-   添加对轻量级元能力框架子系统的编译，以hi3516dv300\_liteos\_a为例
    -   在build/lite/platform/hi3516dv300\_liteos\_a/platform.json中的subsystem\_list字段下面添加aafwk，代码如下：

        ```
        {
             "name":"aafwk",
             "project":"hmf/aafwk/services/abilitymgr_lite",
             "path":"build/lite/config/subsystem/aafwk",
             "dir":"foundation/aafwk/services/abilitymgr_lite",
             "desc":"Ability Services Manager",
             "requirement":"yes",
             "default":"yes",
             "selected":"yes"
        },
        ```

    -   在build/lite/platform/hi3516dv300\_liteos\_a/template/ipcamera.json的“template\_subsystem\_list”字段下面添加"aafwk"，代码如下：

        ```
        "template_subsystem_list" : [
             ......
             "distributedschedule",
             "aafwk",
             "communication",
             ......
        ],
        ```

    -   在build/lite/config/subsystem/aafwk/BUILD.gn中添加对用户程序框架中具体组件的编译，如下：

        ```
        import("//build/lite/config/subsystem/lite_subsystem.gni")
        
        lite_subsystem("aafwk") {
            subsystem_components = [
                "//foundation/aafwk/frameworks/kits/ability_lite:aafwk_abilitykit_lite",
                "//foundation/aafwk/frameworks/kits/ability_lite:aafwk_abilityMain_lite",
                "//foundation/aafwk/services/abilitymgr_lite:aafwk_services_lite",
                "//foundation/aafwk/frameworks/kits/tools_lite:tools_lite",
                "//foundation/aafwk/frameworks/kits/ability_lite/test:aafwk_testapp_lite",
            ]
        }
        ```

    -   在foundation/aafwk下面添加对业务模块的编译，各个模块都有自己的BUILD.gn文件

-   添加完上述的配置后，执行如下命令编译整个系统：

    ```
    python build.py ipcamera -p hi3516dv300_liteos_a -b release
    ```

    运行轻量级元能力运行管理服务

    -   轻量级元能力运行管理服务为AbilityMs，服务运行于foudation进程中。
    -   AbilityMs注册到sa\_manager中，sa\_manager运行于foundation进程中，sa\_manager为AbilityMs创建线程运行环境。具体创建AbilityMs服务的方式以及使用该服务的方式，可参考[系统服务框架子系统](zh-cn_topic_0000001051589563.md)。
    -   在foundation/distributedschedule/services/safwk\_lite/BUILD.gn中添加对abilityms，如下：

        ```
        deps = [
            "//foundation/distributedschedule/services/samgr_lite/samgr_server:server",
            "//base/dfx/lite/liteos-a/source/log:hilog_a_shared",
            "//foundation/aafwk/services/abilitymgr_lite:abilityms",
            "//base/security/services/iam_lite:pms_target",
            "//foundation/distributedschedule/services/dtbschedmgr_lite:dtbschedmgr",
        ]
        ```

    -   刷机后系统启动，AbilityMs会随系统启动而启动，在shell中运行如下命令，可以看到foudation进程中包含了libabilityms


## 运行基于AbilityKit开发的Ability<a name="section18459401331"></a>

-   包安装完成后，通过如下命令，运行Demo

```
./bin/aa start -p com.huawei.launcher -n MainAbility
```



