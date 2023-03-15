---
title: “通信管理：故障排除”
seo-title: Correspondence Management Troubleshooting
description: 通信管理疑难解答
seo-description: Correspondence Management Troubleshooting
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 6%

---

# 通信管理：故障排除 {#correspondence-management-troubleshooting}

## 保存书信时出错 {#errors-when-saving-a-letter}

### 带有 OS 剪贴板 {#issue}

保存信件时显示以下错误之一：

* 文本模块的数据绑定不存在
* 请提供以下内容所需的属性信息

### 原因 {#reason}

由于以下原因之一，可能会发生这些错误：

* 数据字典已绑定到字母，但服务器上不存在。
* 数据字典绑定到字母，但名称中包含下划线(_)。

### 解决方法 {#workaround}

确保您在书信中使用的数据字典位于服务器上，并且其名称中没有下划线(_)。

## 预览信件时出错 {#error-when-previewing-a-letter}

### 带有 OS 剪贴板 {#issue-1}

预览信件时，即使信件中之前未发布的文本资产已发布，也会显示错误“加载信件时出错：无法从XML输入导入资产”。

### 解决方法 {#workaround-1}

使用以下步骤重置发布实例上的信件缓存，然后重试查看信件：

1. 转到 **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** 并以管理员身份登录。
1. 选择 **通信管理配置**.
1. In **通信管理配置**，禁用 **启用书信缓存**&#x200B;然后单击&#x200B;**保存。**
1. 启用 **启用书信缓存** 然后单击 **保存**.
1. 重试查看书信。
