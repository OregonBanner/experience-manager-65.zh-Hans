---
title: “通信管理：故障排除”
description: 了解如何处理在AEM Forms环境中保存信件过程中出现的错误。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# 通信管理：疑难解答 {#correspondence-management-troubleshooting}

## 保存书信时出错 {#errors-when-saving-a-letter}

### 问题 {#issue}

保存信件时显示以下错误之一：

* 文本模块不存在数据绑定
* 提供以下内容所需的属性信息

### 原因 {#reason}

由于以下原因之一，可能发生这些错误：

* 数据字典已绑定到书信，但服务器上不存在。
* 数据字典与字母绑定，但名称中包含下划线(_)。

### 解决方法 {#workaround}

确保您在书信中使用的数据字典在服务器上存在，并且其名称中没有下划线(_)。

## 预览信件时出错 {#error-when-previewing-a-letter}

### 问题 {#issue-1}

预览信件时，即使信件中之前未发布的文本资产已发布，也会显示错误“加载信件时出错：无法从XML输入导入资产”。

### 解决方法 {#workaround-1}

使用以下步骤重置发布实例上的信件缓存，然后重试查看信件：

1. 转到 **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** 并以管理员身份登录。
1. 选择 **通信管理配置**.
1. 在 **通信管理配置**，禁用 **启用书信缓存**&#x200B;然后单击&#x200B;**保存。**
1. Check **启用书信缓存** 然后单击 **保存**.
1. 重试查看书信。
