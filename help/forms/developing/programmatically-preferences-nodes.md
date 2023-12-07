---
title: 以编程方式管理PreferencesNodes
description: 使用首选项管理器服务API (Java)以编程方式管理首选项节点。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# 以编程方式管理首选项节点 {#programmatically-managing-the-preferencesnodes}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

本主题介绍如何使用首选项管理器服务API (Java)以编程方式管理首选项节点。

您可以从管理员UI手动更改配置设置。 要更改选项，请导航至 `Home>Settings>User Management> Configuration>Manual Configuration`. 导入 `config.xml` 进行更改后，您会注意到除了在节点进行的更改之外的所有更改 `/Adobe/Adobe Experience Manager Forms/Config/UM persist` 都迷路了。 用户管理导入和导出预览不支持更改其他组件的配置设置。 现在，可以使用进行这些更改 `PreferencesManagerServiceClient` API。

**步骤摘要**&#x200B;要以编程方式管理首选项节点，请执行以下步骤：

1. 包括项目文件。
1. 创建PreferencesManagerService客户端
1. 调用相应的角色或权限操作

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建PreferencesManagerService客户端**

必须先创建PreferencesManagerService客户端，然后才能以编程方式执行用户管理PreferencesManagerService操作。 使用Java API可通过创建PreferencesManagerServiceClient对象来实现这一点。

**调用相应的角色或权限操作**

创建服务客户端后，可以调用Preferences Manager操作。 服务客户端允许您读取和设置权限。
