# 启动引导模块<a name="ZH-CN_TOPIC_0000001054781918"></a>

## 简介<a name="section469617221261"></a>

启动引导模块，init进程，内核完成初始化后加载的第一个用户态进程，启动后解析/etc/init.cfg配置文件，并根据解析结果拉起其他系统关键进程，同时分别赋予其对应权限。

二进制文件部署在/bin/init。

## 目录<a name="section15884114210197"></a>

```
base
├──startup    启动恢复子系统根目录  
└──── services
      └── init_lite       启动引导模块
          ├── BUILD.gn    启动引导模块编译配置
          ├── include     启动引导模块头文件目录
          ├── LICENSE     开源LICENSE文件
          ├── moduletest  启动引导模块自测试代码目录
          └── src         启动引导模块源文件目录
vendor
└──huawei
        └──camera
                └──init_configs  启动引导模块配置文件目录（json格式，部署于/etc/目录下）
```

## 约束<a name="section12212842173518"></a>

目前仅支持Hi3516DV300和Hi3518EV300版本。

## 启动引导模块配置文件<a name="section1464106163817"></a>

启动引导模块配置文件包含了所有需要由init进程启动的系统关键服务的服务名、可执行文件路径、权限和其他属性信息，该文件位于代码仓库/vendor/huawei/camera/init\_configs目录，部署在/etc/下，文件名称为init.cfg，采用json格式，文件大小目前限制在100KB以内。

init进程启动后首先读取/etc/init.cfg，然后解析其json内容，并根据解析结果依次加载系统服务。配置文件格式和内容说明如下所示：

```
{
    "jobs" : [{
            "name" : "pre-init",      -------- 在init之前执行的job，可以放置一些启动进程之前的预操作（如新建文件夹等）
            "cmds" : [                -------- 当前job支持的命令集合，命令名称（10字节以内）和后面参数（32字节以内）之间有且只能有一个空格
                "mkdir /testdir",      -------- 创建文件夹命令，mkdir和目标文件夹之间有且只能有一个空格
                "chmod 0700 /testdir", -------- 修改权限命令，chmod 权限 目标  之间间隔有且仅有一个空格，权限必须为0xxx格式
                "chown 99 99 /testdir",-------- 修改属组命令，chown uid gid 目标  之间间隔有且仅有一个空格
                "mkdir /testdir2",
                "mount vfat /dev/mmcblk0p0 /testdir2 noexec nosuid" -------- mount命令，格式为：mount 文件系统类型 source target flags data
                                                                    -------- flags当前仅支持nodev、noexec、nosuid和rdonly，各项均以一个空格分开
            ]
        }, {
            "name" : "init",          -------- job名称当前仅支持识别“pre-init”、“init”和“post-init”
            "cmds" : [                -------- 单个job目前最多支持30条cmd
                "start service1",     -------- 启动服务命令1
                "start service2"      -------- 启动服务命令2（可以根据需要调整命令在数组中的顺序，init进程将根据解析顺序依次执行）
             ]
        }, {
             "name" : "post-init",    -------- 在init之后执行的 job，可以放置一些启动进程之后的操作
             "cmds" : []
        }
    ],
    "services" : [{                         -------- service集合（数组形式），包含了init进程需要启动的所有系统服务（当前最多支持100个服务）
            "name" : "service1",            -------- 当前服务的服务名，须确保非空且长度在32字节以内
            "path" : "/bin/process1"        -------- 当前服务的可执行文件全路径，须确保非空且长度在64字节以内
            "uid" : 1,                      -------- 当前服务进程的uid值
            "gid" : 1,                      -------- 当前服务进程的gid值
            "once" : 0,                     -------- 当前服务进程是否为一次性进程
                                                     0 --- 当前服务非一次性进程，当进程因任何原因退出时，init收到SIGCHLD信号后将重新启动该服务进程
                                                   非0 --- 当前服务为一次性进程，当进程因任何原因退出时，init不会重新启动该服务进程
            "importance" : 1,               -------- 当前服务是否为关键系统进程
                                                     0 --- 当前服务非关键系统进程，当进程因任何原因退出时，init不会做系统复位操作
                                                   非0 --- 当前服务为关键系统进程，当进程因任何原因退出时，init收到SIGCHLD信号后进行系统复位重启
            "caps" : [0, 1, 2, 5]           -------- 当前服务所需的capability值，根据安全子系统已支持的capability，评估所需的capability，遵循最小权限原则配置（当前最多可配置100个值）
    }, {
            "name" : "service2",            -------- 下一个需要init启动的服务。此处服务的顺序与启动顺序无关，启动顺序取决于上面job中的cmd顺序。
            "path" : "/bin/process2",
            "uid" : 2,
            "gid" : 2,
            "once" : 1,
            "importance" : 0,
            "caps" : [ ]
        }
    ]
}
```

需要注意的是，init.cfg文件的修改需要保持json格式不被破坏，否则init进程解析失败后不会启动任何服务。对于配置的服务权限（uid/gid/capability）需要符合安全子系统要求且遵循权限最小原则。另外，对于once和importance项均为0的服务，若其在4分钟内连续退出次数超过4次，则init将终止重新启动该服务的操作。

