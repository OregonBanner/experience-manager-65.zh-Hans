---
title: 使用Adobe开发人员应用程序生成器扩展 [!DNL Adobe Experience Manager] 6.5。
description: 使用Adobe开发人员应用程序生成器扩展 [!DNL Adobe Experience Manager] 6.5。
source-git-commit: aab7d4aaf11b6aef3b729f906259a76c152fd6f0
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# 使用Adobe开发人员应用程序生成器扩展[!DNL Adobe Experience Manager] {#extend-using-app-builder}

## 什么是App Builder for AEM {#project-firefly}

新的Adobe开发人员应用程序生成器为开发人员提供了一个扩展框架，以便轻松扩展AEM功能。

App Builder提供了统一的第三方可扩展性框架，用于集成和创建可扩展Adobe Experience Manager的自定义体验。 借助基于Adobe基础架构的完整扩展性框架，开发人员可以构建自定义微服务，跨Adobe解决方案和IT堆栈的其余部分扩展和集成Adobe Experience Manager。

应用程序生成器为客户提供了一种在各种用例中轻松扩展Adobe Experience Manager的方法：

* 中间件可扩展性 — 将外部系统与构建自定义连接器的Adobe应用程序连接，或利用一套预先构建的集成。
* 核心服务可扩展性 — 通过使用自定义特性和业务逻辑扩展默认行为，扩展核心应用程序功能。
* 用户体验可扩展性 — 扩展核心体验以支持业务需求或构建特定于客户的数字资产、店面和后台应用程序。

自2020年夏季以来，企业客户和合作伙伴可以通过我们的开发人员预览来使用应用程序生成器（以前称为项目Firefly）。 应用程序生成器的正式发布(GA)计划于2021年12月正式发布。 我们欢迎开发人员通过我们的[试用程序](http://adobe.ly/appbuilder-trial)来试用应用程序生成器。

>[!NOTE]
>
> 对于要使用应用程序生成器的AEMCloud Service客户，请转到[使用Adobe开发人员应用程序生成器将Adobe Experience Manager扩展为Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/configuring-and-extending/app-builder.html)。

## 架构 {#architecture}

Adobe开发人员应用程序生成器不提供现成的解决方案，而是提供了一个通用、一致、标准化的开发平台，用于扩展Adobe云解决方案，例如AEM，包括：

* Adobe开发人员控制台 — 用于自定义微服务和扩展开发，允许开发人员在构建和管理项目的同时访问他们创建插件和集成所需的所有工具和API。
* 开发人员工具 — 开源工具、SDK和库，允许开发人员轻松构建自定义扩展和集成。 使用React Spectrum(Adobe的UI工具包)为所有Adobe应用程序提供一个通用UI。
* 服务 — 用于在无服务器平台上托管基础架构的I/O运行时，以及用于基于事件的集成的I/O事件。 我们还提供了用于存储数据和文件的开箱即用支持。
* Adobe Experience Cloud — 开发人员可以提交要在其Experience Cloud组织中发布的扩展和集成。然后，系统管理员可以审核、管理和批准这些扩展。 发布后，您的自定义App Builder扩展和工具可以与其他Adobe Experience Cloud应用程序一起找到。

下图说明了在应用程序生成器上构建的标准应用程序如何利用这些功能：

![架构](assets/firefly-architecture.jpg)

有关应用程序生成器架构的更多详细信息，请参阅[架构概述](https://www.adobe.io/project-firefly/docs/guides/)。

## 应用程序生成器入门 {#additional-resources}

为了帮助您开始使用应用程序生成器，我们创建了一系列文档来帮助您开始：

* [应用程序生成器快速入门](https://www.adobe.io/project-firefly/docs/getting_started/)

## 继续学习文档 {#appbuilder-documentation}

应用程序生成器为开发人员提供视频和文档，包括指南和参考文档，可帮助您开始开发自己的自定义应用程序：

* [应用程序生成器文档](https://www.adobe.io/project-firefly/docs/overview/)
* [应用程序生成器视频](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## 试用其中一个示例应用程序 {#appbuilder-codesamples}

准备好开始开发了吗？ 我们提供了许多示例应用程序，帮助您快速前进：

* [Adobe开发人员网站上的应用程序生成器代码实验室](https://www.adobe.io/project-firefly/docs/resources/)

## 支持 {#support}

对于开发人员支持类型的请求，我们鼓励开发人员使用我们的[Experience League论坛](https://experienceleaguecommunities.adobe.com/t5/project-firefly/ct-p/project-firefly)。
