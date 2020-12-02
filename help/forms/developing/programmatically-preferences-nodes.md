---
title: 以编程方式管理PreferencesNodes
seo-title: 以编程方式管理PreferencesNodes
description: 'null'
seo-description: 'null'
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# 以编程方式管理首选项节点{#programmatically-managing-the-preferencesnodes}

本主题介绍如何使用Preferences Manager Service API(Java)以编程方式管理Preferences节点。

您可以从管理员UI中手动更改配置设置。 要更改选项，请导航到`Home>Settings>User Management> Configuration>Manual Configuration`。 进行更改后导入`config.xml`，您会注意到除在节点`/Adobe/Adobe Experience Manager Forms/Config/UM persist`所做更改外的所有更改都丢失。 用户管理导入和导出的预览不支持更改其他组件的配置设置。 现在，可以使用`PreferencesManagerServiceClient` API进行这些更改。

**步骤摘**&#x200B;要要以编程方式管理首选项节点，请执行以下步骤：

1. 包括项目文件。
1. 创建PreferencesManagerService客户端
1. 调用适当的角色或权限操作

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建PreferencesManagerService客户端**

在以编程方式执行用户管理首选项管理器服务操作之前，必须创建PreferencesManager服务客户端。 使用Java API，可通过创建PreferencesManagerServiceClient对象来完成此操作。

**调用适当的角色或权限操作**

创建服务客户端后，即可调用“首选项管理器”操作。 服务客户端允许您读取和设置权限。
