# bundlemgr\_README

# 项目介绍<a name="ZH-CN_TOPIC_0000001054501975"></a>

## 简介<a name="section469617221261"></a>

**轻量级包管理框架子系统**，是鸿蒙系统为开发者提供的安装包管理框架。轻量级包管理框架子系统的由如下模块组成：

![](http://tools.harmonyos.com/mirrors/hpm-image/bundlemgr_README/figures/zh-cn_image_0000001054309949.png)

**图1**  轻量级包管理框架子系统框架图

-   **包扫描器**：用来解析本地预制或者安装的安装包，提取里面的各种信息，供管理子模块进行管理，持久化

-   **包安装子模块**：安装，卸载，升级一个包；Installed一个单独进程的用于创建删除安装目录，具有较高的权限。

-   **包管理子模块**：管理安装包相关的信息

-   **安全子模块**：签名检查、权限授予、权限管理

## 目录<a name="section1464106163817"></a>

轻量级包管理框架子系统源代码目录结构如下图所示：

**表 1**  轻量级包管理框架子系统代码目录结构

<a name="table2977131081412"></a>
<table><thead align="left"><tr id="row7977610131417"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p18792459121314"><a name="p18792459121314"></a><a name="p18792459121314"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p77921459191317"><a name="p77921459191317"></a><a name="p77921459191317"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row1897841071415"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p10698114117583"><a name="p10698114117583"></a><a name="p10698114117583"></a>foundation/appexecfwk/frameworks/bundle_lite</p>
<p id="p86931748213"><a name="p86931748213"></a><a name="p86931748213"></a>foundation/appexecfwk/interfaces/innerkits/bundlemgr_lite</p>
<p id="p11839171152117"><a name="p11839171152117"></a><a name="p11839171152117"></a>foundation/appexecfwk/interfaces/kits/bundle_lite</p>
<p id="p14119113219"><a name="p14119113219"></a><a name="p14119113219"></a>foundation/appexecfwk/services/bundlemgr_lite</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p1169814112585"><a name="p1169814112585"></a><a name="p1169814112585"></a>用户程序运行的包信息、元能力信息、异步事件处理等基本接口</p>
<p id="p12693148215"><a name="p12693148215"></a><a name="p12693148215"></a>用户程序包管理服务对外接口</p>
<p id="p158391810217"><a name="p158391810217"></a><a name="p158391810217"></a>用户程序运行的包信息、元能力信息、异步事件处理机制的实现逻辑</p>
<p id="p64110114210"><a name="p64110114210"></a><a name="p64110114210"></a>用户程序包管理服务实现逻辑</p>
</td>
</tr>
</tbody>
</table>

# 资源文档<a name="ZH-CN_TOPIC_0000001054621947"></a>

## 开发指南<a name="section11441957184310"></a>

编译轻量级包管理框架子系统

-   添加对轻量级包管理框架子系统的编译，以hi3516dv300\_liteos\_a为例
    -   在build/lite/platform/hi3516dv300\_liteos\_a/platform.json中的subsystem\_list字段下面添加appexecfwk，代码如下：

        ```
        {
             "name":"appexecfwk",
             "project": "hmf/appexecfwk/services/bundlemgr_lite",
             "path": "build/lite/config/subsystem/appexecfwk",
             "dir": "foundation/appexecfwk/services/bundlemgr_lite",
             "desc":"Bundle Services Manager",
             "requirement":"yes",
             "default":"yes",
             "selected":"yes"
        },
        ```

    -   在build/lite/platform/hi3516dv300\_liteos\_a/template/ipcamera.json的“template\_subsystem\_list”字段下面添加"appexecfwk"和"aafwk"，代码如下：

        ```
        "template_subsystem_list" : [
             ......
             "distributedschedule",
             "appexecfwk",
             "communication",
             ......
        ],
        ```

    -   在build/lite/config/subsystem/aafwk/BUILD.gn和/build/lite/config/subsystem/appexecfwk/BUILD.gn中添加对用户程序框架中具体组件的编译，如下：

        ```
        import("//build/lite/config/subsystem/lite_subsystem.gni")
        
        lite_subsystem("appexecfwk") {
            subsystem_components = [
                "//foundation/appexecfwk/kits/appkit_lite:appexecfwk_kit_lite",
                "//foundation/appexecfwk/services/bundlemgr_lite:appexecfwk_services_lite",
            ]
        }
        ```

    -   在foundation/aafwk和foundation/appexecfwk下面添加对业务模块的编译，各个模块都有自己的BUILD.gn文件

-   添加完上述的配置后，执行如下命令编译整个系统：

```
python build.py ipcamera -p hi3516dv300_liteos_a -b release
```

运行轻量级包管理服务

-   轻量级包管理服务为BundleMs，服务运行于foudation进程中。
-   BundleMs注册到sa\_manager中，sa\_manager运行于foundation进程中，sa\_manager为BundleMs创建线程运行环境。具体创建BundleMs服务的方式以及使用该服务的方式，可参考[系统服务框架子系统](zh-cn_topic_0000001051589563.md)。
-   在foundation/distributedschedule/services/safwk\_lite/BUILD.gn中添加对bundlems，如下：

```
deps = [
    "//foundation/distributedschedule/services/samgr_lite/samgr_server:server",
    "//base/dfx/lite/liteos-a/source/log:hilog_a_shared",
    "//foundation/appexecfwk/services/bundlemgr_lite:bundlems",
    "//base/security/services/iam_lite:pms_target",
    "//foundation/distributedschedule/services/dtbschedmgr_lite:dtbschedmgr",
]
```

-   刷机后系统启动，BundleMs会随系统启动而启动，在shell中运行如下命令，可以看到foudation进程中包含了libbundlems

## 运行基于AbilityKit开发的Ability<a name="section1012532233211"></a>

-   基于AbilityKit开发的Ability的Demo代码位于foundation/aafwk/frameworks/kits/ability\_lite/test路径下，如有需要修改其中的功能，可在unittest的文件中修改代码或增加代码文件，并在BUILD.gn中做相应的修改。
-   编译该Demo，在shell中执行如下命令，编译成功后，在out/ipcamera\_hi3516dv300\_liteos\_a下面生成libLauncher.so文件：

    ```
    python build.py ipcamera -p hi3516dv300_liteos_a -T //foundation/aafwk/frameworks/kits/ability_lite/test:Launcher
    ```

-   编写config.json，内容如下：

    ```
    {
        "app": {
            "bundleName": "com.huawei.launcher",
            "vendor": "huawei",
            "version": {
                "code": 1,
                "name": "1.0"
            }
        },
        "deviceConfig": {
            "default": {
                "reqSdk": {
                    "compatible": "zsdk 1.0.0",
                    "target": "zsdk 1.0.1"
                },
                "keepAlive": false
            },
        },
        "module": {
            "deviceType": [
                "smartCamera"
            ], 
            "distro": {
                "deliveryWithInstall": true, 
                "moduleName": "Launcher", 
                "moduleType": "entry"
            },
            "abilities": [{
                "name": "MainAbility",
                "icon": "res/drawable/phone.png",
                "label": "test app 1", 
                "launchType": "standard",
                "type": "page",
                "visible": true
            },
            {
                "name": "SecondAbility",
                "icon": "res/drawable/phone.png",
                "label": "test app 2", 
                "launchType": "standard",
                "type": "page",
                "visible": true
            },
            {
                "name": "ServiceAbility",
                "icon": "res/drawable/phone.png",
                "label": "test app 2", 
                "launchType": "standard",
                "type": "service",
                "visible": true
            }
            ]
        }
    }
    ```

-   生成hap包
    -   按照如下目录结构存放文件，res/drawable下面放置资源文件：

        ![](http://tools.harmonyos.com/mirrors/hpm-image/bundlemgr_README/figures/zh-cn_image_0000001054312178.png)

    -   将上述文件打包生成zip包，修改后缀为.hap，例如Launcher.hap

-   安装hap包

    -   将上述hap包放置到指定目录下面
    -   执行安装命令，安装hap包：

    ```
    ./bin/bm install -p /nfs/hap/Launcher.hap
    ```




