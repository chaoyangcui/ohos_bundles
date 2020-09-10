# crypto\_README

# 数据加解密模块<a name="ZH-CN_TOPIC_0000001054143192"></a>

## 简介<a name="section469617221261"></a>

数据加解密模块，配合轻量级ACE开发框架子系统，提供支持RSA及AES加解密功能的js api。

## 目录<a name="section1464106163817"></a>

```
base
├──security   安全子系统根目录  
└──── frameworks
      ├── crypto_lite    数据加解密模块
           ├── cipher
                ├── BUILD.gn    cipher模块编译配置
                ├── include     cipher模块头文件目录
                └── src         cipher模块源文件目录
           ├── js
                ├── builtin
                     ├── BUILD.gn    js对接模块编译配置
                     ├── include     js对接模块头文件目录
                     └── src         js对接模块源文件目录
           └── LICENSE     开源LICENSE文件
```

## 约束<a name="section0560184083217"></a>

目前仅支持Hi3516DV300版本。



