---
title: “通信管理：疑难解答»
seo-title: 通信管理疑难解答
description: 通信管理疑难解答
seo-description: 通信管理疑难解答
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 通信管理：疑难解答 {#correspondence-management-troubleshooting}

## 保存字母时出错 {#errors-when-saving-a-letter}

### 问题 {#issue}

保存字母时显示以下错误之一：

* 文本模块不存在数据绑定
* 请提供以下内容所需的属性信息

### 原因 {#reason}

这些错误可能由于以下原因之一而发生：

* 数据字典绑定到该字母，但服务器上不存在。
* 数据字典绑定到字母，但名称中有下划线(_)。

### 解决方法 {#workaround}

确保您在字母中使用的数据字典在服务器上存在，并且其名称中没有下划线(_)。

## 预览字母时出错 {#error-when-previewing-a-letter}

### 问题 {#issue-1}

预览字母时，出现错误“加载字母时出错：无法从XML输入导入资产”，即使在发布字母中以前未发布的文本资产时也是如此。

### 解决方法 {#workaround-1}

使用以下步骤重置发布实例上的字母缓存，然后重试查看字母：

1. 转到并 **`https://[server]:[port]/[contextPath]/system/console/configMgr`** 以管理员身份登录。
1. 选择 **对应管理配置**。
1. 在“对 **应管理配置”中**，禁用“ **启用字母缓存”,**&#x200B;然后单击&#x200B;**“保存”。**
1. 启用 **字母缓存** ，然后单击 **保存**。
1. 重试查看字母。

