# Hi3518ev300介绍<a name="ZH-CN_TOPIC_0000001054508081"></a>

项目介绍

## 简介<a name="section469617221261"></a>

海思（上海）媒体软件开发包用于适配不同芯片复杂的底层处理，为“媒体子系统”提供基础的多媒体处理功能。主要功能有：音视频采集、音视频编解码、音视频输出、视频前处理、封装、解封装、文件管理、存储管理、日志系统等。该软件包功能对应"媒体子系统"框架中红色框标注部分，如图1所示。所对应的目录为：vendor\\hisi\\hi35xx。

**图 1**  多媒体子系统框架图<a name="fig108579114217"></a>  
![](http://tools.harmonyos.com/mirrors/hpm-image/hi3518ev300_README/figures/多媒体子系统框架图.png "多媒体子系统框架图")

## 目录<a name="section1464106163817"></a>

海思（上海）媒体软件开发包目录结构如表1所示：

**表 1**  hardware目录结构

<a name="table15811112718910"></a>
<table><thead align="left"><tr id="row1181112718915"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p28116271096"><a name="p28116271096"></a><a name="p28116271096"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p28111727292"><a name="p28111727292"></a><a name="p28111727292"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row581122715917"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p7463423141214"><a name="p7463423141214"></a><a name="p7463423141214"></a>hi35xx\hardware</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p164391323161216"><a name="p164391323161216"></a><a name="p164391323161216"></a>媒体南向接口实现、框架及芯片对接层库目录</p>
</td>
</tr>
</tbody>
</table>

**表 2**  hi35xx\_init目录结构

<a name="table78291813141320"></a>
<table><thead align="left"><tr id="row10829191361312"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p8829813111314"><a name="p8829813111314"></a><a name="p8829813111314"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p1182901301317"><a name="p1182901301317"></a><a name="p1182901301317"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row98296133139"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p582915130134"><a name="p582915130134"></a><a name="p582915130134"></a>hi35xx\hi35xx_init\hi3516dv300</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p1882971311313"><a name="p1882971311313"></a><a name="p1882971311313"></a>编译打包16dv300内核镜像的编译脚本</p>
</td>
</tr>
<tr id="row1316718286548"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p167506431548"><a name="p167506431548"></a><a name="p167506431548"></a>hi35xx\hi35xx_init\hi3518ev300</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p5165122819547"><a name="p5165122819547"></a><a name="p5165122819547"></a>编译打包18ev300内核镜像的编译脚本</p>
</td>
</tr>
</tbody>
</table>

**表 3**  hi3516dv300目录结构

<a name="table2977131081412"></a>
<table><thead align="left"><tr id="row7977610131417"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p18792459121314"><a name="p18792459121314"></a><a name="p18792459121314"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p77921459191317"><a name="p77921459191317"></a><a name="p77921459191317"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row17977171010144"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p1881003717317"><a name="p1881003717317"></a><a name="p1881003717317"></a>hi35xx\hi3516dv300</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p879375920132"><a name="p879375920132"></a><a name="p879375920132"></a>Hi3516DV300芯片驱动软件，包括：媒体驱动子目录、媒体用户态库子目录、uboot的差异化内容目录、NOTICE文件</p>
</td>
</tr>
<tr id="row6978161091412"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p98744311516"><a name="p98744311516"></a><a name="p98744311516"></a>hi35xx\hi3516dv300\module_init\lib</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p6793059171318"><a name="p6793059171318"></a><a name="p6793059171318"></a>Hi3516DV300芯片媒体各模块驱动对应的库、LICENSE文件</p>
</td>
</tr>
<tr id="row6978201031415"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p6687137121713"><a name="p6687137121713"></a><a name="p6687137121713"></a>hi35xx\hi3516dv300\module_init\src</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p528302241710"><a name="p528302241710"></a><a name="p528302241710"></a>内核驱动初始化源代码、LICENSE文件</p>
</td>
</tr>
<tr id="row1897841071415"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p16793185961315"><a name="p16793185961315"></a><a name="p16793185961315"></a>hi35xx\hi3516dv300\soc\lib</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p14793959161317"><a name="p14793959161317"></a><a name="p14793959161317"></a>Hi3516DV300芯片的媒体库文件、LICENSE文件</p>
</td>
</tr>
<tr id="row1137581942013"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p19370171952013"><a name="p19370171952013"></a><a name="p19370171952013"></a>hi35xx\hi3516dv300\uboot\out\boot</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p137061910203"><a name="p137061910203"></a><a name="p137061910203"></a>采用hi35xx\third_party\uboot\u-boot-2020.01和hi35xx\hi3516dv300\uboot\reg\reg_info_hi3516dv300.bin编译成的uboot、README文件</p>
</td>
</tr>
<tr id="row1337421962012"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p837021982012"><a name="p837021982012"></a><a name="p837021982012"></a>hi35xx\hi3516dv300\uboot\reg</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p237031917201"><a name="p237031917201"></a><a name="p237031917201"></a>uboot配置文件、LICENSE文件</p>
</td>
</tr>
<tr id="row135651424162014"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p1072784514202"><a name="p1072784514202"></a><a name="p1072784514202"></a>hi35xx\hi3516dv300\uboot\secureboot_ohos</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p189415151506"><a name="p189415151506"></a><a name="p189415151506"></a>鸿蒙OS安全启动相关的编译脚本</p>
</td>
</tr>
<tr id="row656518242203"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p2900950132013"><a name="p2900950132013"></a><a name="p2900950132013"></a>hi35xx\hi3516dv300\uboot\secureboot_release</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p589812504207"><a name="p589812504207"></a><a name="p589812504207"></a>生成安全uboot的源代码、License目录</p>
</td>
</tr>
</tbody>
</table>

**表 4**  hi3518ev300目录结构

<a name="table1769285811814"></a>
<table><thead align="left"><tr id="row186921858681"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p106927581786"><a name="p106927581786"></a><a name="p106927581786"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p1769220581982"><a name="p1769220581982"></a><a name="p1769220581982"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row169217585818"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p2692758986"><a name="p2692758986"></a><a name="p2692758986"></a>hi35xx\hi3518ev300</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p116926581288"><a name="p116926581288"></a><a name="p116926581288"></a>Hi3518EV300芯片驱动软件，包括：媒体驱动子目录、媒体用户态库子目录、uboot的差异化内容目录、NOTICE文件</p>
</td>
</tr>
<tr id="row1269285819817"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p169219587818"><a name="p169219587818"></a><a name="p169219587818"></a>hi35xx\hi3518ev300\module_init\lib</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p1269210581689"><a name="p1269210581689"></a><a name="p1269210581689"></a>Hi3518EV300芯片媒体各模块驱动对应的库、LICENSE文件</p>
</td>
</tr>
<tr id="row86931358986"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p36937581882"><a name="p36937581882"></a><a name="p36937581882"></a>hi35xx\hi3518ev300\module_init\src</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p136931158287"><a name="p136931158287"></a><a name="p136931158287"></a>内核驱动初始化源代码、LICENSE文件</p>
</td>
</tr>
<tr id="row20693958681"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p11693258181"><a name="p11693258181"></a><a name="p11693258181"></a>hi35xx\hi3518ev300\soc\lib</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p1369315585818"><a name="p1369315585818"></a><a name="p1369315585818"></a>Hi3518EV300芯片的媒体库文件、LICENSE文件</p>
</td>
</tr>
<tr id="row369335817820"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p16931583815"><a name="p16931583815"></a><a name="p16931583815"></a>hi35xx\hi3518ev300\uboot\out\boot</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p269345817814"><a name="p269345817814"></a><a name="p269345817814"></a>采用hi35xx\third_party\uboot\u-boot-2020.01和hi35xx\hi3518ev300\uboot\reg\reg_info_hi3518ev300.bin编译成的uboot、README文件</p>
</td>
</tr>
<tr id="row769365813812"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p1669317585818"><a name="p1669317585818"></a><a name="p1669317585818"></a>hi35xx\hi3518ev300\uboot\reg</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p1469315585813"><a name="p1469315585813"></a><a name="p1469315585813"></a>uboot配置文件、LICENSE文件</p>
</td>
</tr>
<tr id="row9693185816812"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p126935586810"><a name="p126935586810"></a><a name="p126935586810"></a>hi35xx\hi3518ev300\uboot\secureboot_ohos</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p5693458781"><a name="p5693458781"></a><a name="p5693458781"></a>鸿蒙OS安全启动相关的编译脚本</p>
</td>
</tr>
<tr id="row26932581085"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p18693658184"><a name="p18693658184"></a><a name="p18693658184"></a>hi35xx\hi3518ev300\uboot\secureboot_release</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p106931358586"><a name="p106931358586"></a><a name="p106931358586"></a>生成安全uboot的源代码、License目录</p>
</td>
</tr>
</tbody>
</table>

**表 5**  middleware目录结构

<a name="table9651175972417"></a>
<table><thead align="left"><tr id="row1965112590241"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p146513596248"><a name="p146513596248"></a><a name="p146513596248"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p10651859192419"><a name="p10651859192419"></a><a name="p10651859192419"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row16653185915240"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p20653155942417"><a name="p20653155942417"></a><a name="p20653155942417"></a>hi35xx\middleware\source\common</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p1065385913243"><a name="p1065385913243"></a><a name="p1065385913243"></a>南向组件公共模块库目录</p>
</td>
</tr>
<tr id="row186531759192419"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p1865345914243"><a name="p1865345914243"></a><a name="p1865345914243"></a>hi35xx\middleware\source\component</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p19653205992414"><a name="p19653205992414"></a><a name="p19653205992414"></a>南向组件非公共模块库目录</p>
</td>
</tr>
<tr id="row6653125952412"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p5653105910248"><a name="p5653105910248"></a><a name="p5653105910248"></a>hi35xx\middleware\source\thirdparty</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p17653135914241"><a name="p17653135914241"></a><a name="p17653135914241"></a>南向插件依赖第三方开源软件目录</p>
</td>
</tr>
</tbody>
</table>

**表 6**  platform目录结构

<a name="table397031661516"></a>
<table><thead align="left"><tr id="row109701916151514"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p16971121616153"><a name="p16971121616153"></a><a name="p16971121616153"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p17971616151513"><a name="p17971616151513"></a><a name="p17971616151513"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row12971131610154"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p79972101107"><a name="p79972101107"></a><a name="p79972101107"></a>hi35xx\platform</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p1099791016102"><a name="p1099791016102"></a><a name="p1099791016102"></a>hi35xx平台驱动</p>
</td>
</tr>
</tbody>
</table>

**表 7**  third\_party目录结构

<a name="table16381640161517"></a>
<table><thead align="left"><tr id="row33814041510"><th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.1"><p id="p163812401154"><a name="p163812401154"></a><a name="p163812401154"></a>名称</p>
</th>
<th class="cellrowborder" valign="top" width="50%" id="mcps1.2.3.1.2"><p id="p163854019151"><a name="p163854019151"></a><a name="p163854019151"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row12381640101512"><td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.1 "><p id="p14505145412188"><a name="p14505145412188"></a><a name="p14505145412188"></a>hi35xx\third_party\uboot\u-boot-2020.01</p>
</td>
<td class="cellrowborder" valign="top" width="50%" headers="mcps1.2.3.1.2 "><p id="p14381240161511"><a name="p14381240161511"></a><a name="p14381240161511"></a>uboot开源代码</p>
</td>
</tr>
</tbody>
</table>

## 约束<a name="section0364124983015"></a>

当前支持Hi3518EV300、Hi3516DV300芯片。

## 许可协议<a name="section1478215290"></a>

## hi3516dv300许可说明<a name="section172811306502"></a>

-   hi35xx\\hi3516dv300\\module\_init\\lib和hi35xx\\hi3516dv300\\soc\\lib里面为海思（上海）的自研库，遵循海思（上海）的LICENSE，这两个目录下均有LICENSE文件，LICENSE文件结尾可以看到版权信息：

    ```
    Copyright (C) 2020 Hisilicon (Shanghai) Technologies Co., Ltd. All rights reserved.
    ```

-   hi35xx\\hi3516dv300\\module\_init\\src目录下为海思（上海）自研代码，使用基于Apache License Version 2.0许可的Hisilicon \(Shanghai\) 版权声明，在该目录下有Apache License Version 2.0的LICENSE文件，许可信息和版权信息通常可以在文件开头看到：

    ```
     / *Copyright (c) 2020 HiSilicon (Shanghai) Technologies CO., LIMITED. Licensed under the Apache License,* ... * / 
    ```

-   hi35xx\\hi3516dv300\\uboot\\reg为海思（上海）的二进制文件，遵循海思（上海）的LICENSE，该目录下有LICENSE文件，LICENSE文件结尾可以看到：

    ```
    Copyright (C) 2020 Hisilicon (Shanghai) Technologies Co., Ltd. All rights reserved.
    ```

-   hi35xx\\hi3516dv300\\uboot\\out\\boot是由u-boot-2020.01和reg\_info\_hi3516dv300.bin编译成的uboot二进制文件，完全遵从u-boot-2020.01的整体协议，具体请参看hi35xx\\third\_party\\uboot\\u-boot-2020.01\\Licenses目录下的README。
-   hi35xx\\hi3516dv300\\uboot\\secureboot\_release为安全uboot的开源代码，其中自研的部分使用基于GPL许可的Hisilicon \(Shanghai\) 版权声明，在该目录下有License目录，许可信息和版权信息通常可以在文件开头看到：

    ```
     / *Copyright (c) 2020 HiSilicon (Shanghai) Technologies CO., LIMITED. 
       *
       * This program is free software; you can redistribute  it and/or modify it
       * under  the terms of  the GNU General  Public License as published by the
       * Free Software Foundation;  either version 2 of the  License, or (at your
       * option) any later version.
       * ... * / 
    ```


-   hi35xx\\hi3516dv300\\NOTICE文件描述了使用到的三款开源软件：Das U-Boot 2020.01、mbed TLS 2.16.6、fdk-aac v2.0.1。

## hi3518ev300许可说明<a name="section172983094910"></a>

-   hi35xx\\hi3518ev300\\module\_init\\lib和hi35xx\\hi3518ev300\\soc\\lib里面为海思（上海）的自研库，遵循海思（上海）的LICENSE，这两个目录下均有LICENSE文件，LICENSE文件结尾可以看到版权信息：

    ```
    Copyright (C) 2020 Hisilicon (Shanghai) Technologies Co., Ltd. All rights reserved.
    ```

-   hi35xx\\hi3518ev300\\module\_init\\src目录下为海思（上海）自研代码，使用基于Apache License Version 2.0许可的Hisilicon \(Shanghai\) 版权声明，在该目录下有Apache License Version 2.0的LICENSE文件，许可信息和版权信息通常可以在文件开头看到：

    ```
     / *Copyright (c) 2020 HiSilicon (Shanghai) Technologies CO., LIMITED. Licensed under the Apache License,* ... * / 
    ```

-   hi35xx\\hi3518ev300\\uboot\\reg为海思（上海）的二进制文件，遵循海思（上海）的LICENSE，该目录下有LICENSE文件，LICENSE文件结尾可以看到：

    ```
    Copyright (C) 2020 Hisilicon (Shanghai) Technologies Co., Ltd. All rights reserved.
    ```

-   hi35xx\\hi3518ev300\\uboot\\out\\boot是由u-boot-2020.01和reg\_info\_hi3518ev300.bin编译成的uboot二进制文件，完全遵从u-boot-2020.01的整体协议，具体请参看hi35xx\\third\_party\\uboot\\u-boot-2020.01\\Licenses目录下的README。
-   hi35xx\\hi3518ev300\\uboot\\secureboot\_release为安全uboot的开源代码，其中自研的部分使用基于GPL许可的Hisilicon \(Shanghai\) 版权声明，在该目录下有License目录，许可信息和版权信息通常可以在文件开头看到：

    ```
     / *Copyright (c) 2020 HiSilicon (Shanghai) Technologies CO., LIMITED. 
       *
       * This program is free software; you can redistribute  it and/or modify it
       * under  the terms of  the GNU General  Public License as published by the
       * Free Software Foundation;  either version 2 of the  License, or (at your
       * option) any later version.
       * ... * / 
    ```

-   hi35xx\\hi3518ev300\\NOTICE文件描述了使用到的三款开源软件：Das U-Boot 2020.01、mbed TLS 2.16.6、fdk-aac v2.0.1。

## third\_party许可说明<a name="section148702720527"></a>

hi35xx\\third\_party\\uboot\\u-boot-2020.01为uboot开源代码，遵循软件版本自带的开源许可声明，具体请参看hi35xx\\third\_party\\uboot\\u-boot-2020.01\\Licenses目录下的README。

