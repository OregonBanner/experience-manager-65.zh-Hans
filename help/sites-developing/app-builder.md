---
title: 扩展 [!DNL Adobe Experience Manager] 6.5使用Adobe Developer App Builder。
description: 扩展 [!DNL Adobe Experience Manager] 6.5使用Adobe Developer App Builder。
exl-id: 8221c2db-82d4-43df-ad38-e8e7831541ac
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# 扩展 [!DNL Adobe Experience Manager] 使用Adobe Developer App Builder {#extend-using-app-builder}

## 什么是App Builder for AEM {#project-appbuilder}

新的Adobe Developer App Builder为开发人员提供了一个可扩展性框架，以便轻松扩展AEM功能。

App Builder提供了一个统一的第三方可扩展性框架，用于集成和创建扩展Adobe Experience Manager的自定义体验。 借助这个基于Adobe基础架构的完整可扩展性框架，开发人员可以构建自定义微服务，跨Adobe解决方案和IT栈栈的其余部分扩展和集成Adobe Experience Manager。

App Builder为客户提供了一种方法，可用于在各种用例中轻松扩展Adobe Experience Manager：

* 中间件可扩展性 — 将外部系统与Adobe应用程序连接起来，以构建自定义连接器，或使用预建的集成套件。
* 核心服务可扩展性 — 通过自定义功能和业务逻辑扩展默认行为，扩展核心应用程序功能。
* 用户体验可扩展性 — 扩展核心体验以支持业务要求或构建特定于客户的数字资产、店面和后台应用程序。

App Builder自2020年夏季起通过Adobe开发人员预览版向企业客户和合作伙伴提供。 App Builder的正式发布日期(GA)计划于2021年12月发布。 Adobe欢迎开发人员通过Adobe的 [试用计划](https://developer.adobe.com/app-builder/trial/).

>[!NOTE]
>
>对于希望使用App Builder的AEMas a Cloud Service客户，请参阅 [使用Adobe Developer App Builder扩展Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html?lang=en).

## 架构 {#architecture}

Adobe Developer App Builder不是开箱即用的解决方案，而是提供通用、一致、标准化的开发平台，用于扩展Adobe云解决方案(例如AEM)，包括：

* Adobe Developer控制台 — 用于自定义微服务和扩展开发，允许开发人员在访问创建插件和集成所需的所有工具和API时构建和管理项目。
* 开发人员工具 — 开源工具、SDK和库，允许开发人员轻松构建自定义扩展和集成。 使用React Spectrum(Adobe的UI工具包)为所有Adobe应用程序使用一个通用UI。
* 服务 — 用于在Adobe的无服务器平台上托管基础架构的I/O运行时，以及用于基于事件的集成的I/O事件。 Adobe还为存储数据和文件提供开箱即用支持。
* Adobe Experience Cloud — 开发人员可以提交要在其Experience Cloud组织中发布的扩展和集成。然后，系统管理员可以审核、管理和批准这些扩展。 发布后，您的自定义App Builder扩展和工具可以与其他Adobe Experience Cloud应用程序一起找到。

下图说明了基于App Builder构建的标准应用程序如何使用这些功能：

![架构](assets/appbuilder-architecture.jpg)

有关App Builder架构的更多详细信息，请参阅 [架构概述](https://developer.adobe.com/app-builder/docs/guides/).

## App Builder入门 {#additional-resources}

为了帮助您开始使用App Builder，我们创建了一系列文档来帮助您开始：

* [App Builder快速入门](https://developer.adobe.com/app-builder/docs/getting_started/)

## 继续学习文档 {#appbuilder-documentation}

App Builder为开发人员提供视频和文档，包括指南和参考文档，以帮助您开始开发自己的自定义应用程序：

* [App Builder文档](https://developer.adobe.com/app-builder/docs/overview/)
* [App Builder视频](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## 试用其中一个示例应用程序 {#appbuilder-codesamples}

准备好开始开发了吗？ 有许多示例应用程序可帮助您快速上手：

* [Adobe Developer网站上的应用程序生成器代码实验室](https://developer.adobe.com/app-builder/docs/resources/)

