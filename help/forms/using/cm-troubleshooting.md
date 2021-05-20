---
title: “通信管理：故障排除”
seo-title: 通信管理疑难解答
description: 通信管理疑难解答
seo-description: 通信管理疑难解答
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: 通信管理
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 6%

---

# 通信管理：{#correspondence-management-troubleshooting}故障排除

## 保存信件{#errors-when-saving-a-letter}时出错

### 带有 OS 剪贴板 {#issue}

保存信件时显示以下错误之一：

* 文本模块不存在数据绑定
* 请提供以下内容所需的属性信息

### 原因 {#reason}

由于以下原因之一，可能会发生这些错误：

* 数据字典绑定到信件，但服务器上不存在。
* 数据字典绑定到该字母，但名称中带有下划线(_)。

### 解决方法 {#workaround}

确保您在信件中使用的数据字典在服务器上存在，且其名称中不带下划线(_)。

## 预览信件{#error-when-previewing-a-letter}时出错

### 带有 OS 剪贴板 {#issue-1}

预览信件时，出现错误“加载信件时出错：无法从XML输入导入资产”，即使在信件中发布了之前未发布的文本资产时也是如此。

### 解决方法{#workaround-1}

使用以下步骤重置发布实例上的信件缓存，然后重试查看信件：

1. 转到&#x200B;**`https://'[server]:[port]'/[contextPath]/system/console/configMgr`**&#x200B;并以管理员身份登录。
1. 选择&#x200B;**通信管理配置**。
1. 在&#x200B;**通信管理配置**&#x200B;中，禁用&#x200B;**启用信件缓存**，然后单击&#x200B;**保存。**
1. 启用&#x200B;**启用字母缓存**，然后单击&#x200B;**保存**。
1. 重试查看信件。
