---
title: 使用AEM Headless获得首个体验的路径
description: 在AEM无头开发人员历程的这一部分中，您将了解在AEM中实施首个无头体验的步骤（包括规划注意事项），并了解尽可能使路径顺畅的最佳实践。
source-git-commit: 0458a811b5bd062abbe8a42ec141bc786491e19e
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 0%

---

# 使用AEM Headless获得首个体验的路径 {#path-to-first-experience}

在 [AEM Headless开发人员历程,](overview.md) 您将了解在AEM中实施首个无头体验的步骤（包括规划注意事项），并了解如何尽可能顺利地实现路径的最佳实践。

## 迄今为止的故事 {#story-so-far}

在AEM无头历程的上一个文档中， [AEM Headless快速入门](getting-started.md) 您学习了无头CMS的基本理论，您现在应该：

* 了解AEM无头功能的基础知识。
* 了解使用AEM无头功能的先决条件。
* 请注意AEM无头集成级别。
* 能够根据范围定义项目。

本文基于这些基础知识，以便您了解如何准备自己的AEM无头项目。

## 目标 {#objective}

本文档可帮助您了解实施第一个项目所需的步骤。 阅读完该文档后，您应：

* 了解设计内容时的重要规划注意事项。
* 了解在AEM中实施无头的步骤。
* 了解需要哪些必要工具和AEM配置。
* 了解最佳实践，以使您的无头历程顺畅、保持内容生成的高效性，并确保内容快速交付。

## 要求 {#requirements}

在继续阅读本文档之前，请确保您已审阅了AEM Headless Developer历程中的上一文档， [AEM Headless快速入门](getting-started.md) 确保您：

* 满足所列要求。
* 已考虑过您自己的项目定义，包括范围、角色和性能。

## 成功规划 {#planning-for-success}

要启动您的第一个AEM无头项目，您需要确保拥有一个内容模型，该模型将支持您要在所有渠道中进行的个性化和更新。

除了AEM之外，如果您要构建客户端应用程序，以便针对对AEM的API调用测试客户端，还需要确保设置了正确的开发环境。

### 定义内容模型和API {#defining-models}

您希望跨渠道提供一致的体验并管理个性化的营销活动，以便您能够将每个渠道和每个渠道的表面视为其自己要交付到的独特内容结构。 但是，让每个渠道都有自己的内容模型，将是一项艰巨的任务。

相反，您应该根据组织原则（如品牌和产品层次结构、商品或表面类别或客户历程中的步骤）考虑不同表面上的内容的关联方式。 例如，如果您有一组支持您制造的特定品牌的汽车的表面，您可能希望首先建立一个内容模型，以了解将对整个汽车都适用的一般信息，然后拥有更多特定元素，例如在汽车开始时遇到服务问题时需要的内容。 这种模型将强制继承一般汽车品牌内容，同时允许基于所需特定上下文的班次。 它还有助于将来管理此内容的更新，因为您可以根据各种角色来实施控制，例如整个汽车品牌的整体营销人员或产品经理，以及负责“起动车”体验的作者。

在您拥有内容模型并清晰查看需要显示内容的各种客户端后，您需要确保将与访问各种内容模型相关的GraphQL/API已发布到所有需要此内容的客户端。 如何访问特定内容有不同的选项。 您可以请求特定的静态内容段，以便缓存内容并提高性能。 您还可以请求动态生成的内容，这将需要进行更多处理。 确保客户能够利用最有效满足其业务需求的API。

## 了解您的环境 {#understanding-environments}

在AEM中，环境有三种类型：开发、暂存和生产。

开发环境（您可以有多个环境）是进行实验和尝试创意的安全场所。 在项目的初始阶段，Adobe建议使用开发环境来尝试各种内容模型，并查看哪些内容为曲面提供预期输出。

无头项目的暂存环境用于在新的AEM产品版本推出到生产之前对其进行验证。 在此处保留生产内容模型的最新列表和内容的子集，以便您能够渲染JSON文件以比较它们的输出，这样当您进行更改或AEM版本引入更改时，即使进行更改，也能提供相同的输出

内容作者在生产环境中创建和管理其实际内容。 生产中的模型更改必须谨慎进行，并要考虑向后兼容性。

在开发阶段，建议您使用开发和暂存环境。 在进行性能测试时，您将需要迁移到生产环境。

### 开发人员与内容作者的合作 {#cooperation}

开发人员需要使用填充的内容模型设置AEM开发环境。 开发人员开发客户端，该客户端将在内容作者仍在创建内容时从AEM无标题中使用内容。 这就是为什么API定义非常重要的原因。 通过利用AEM SDK，开发人员可以创建测试挂接，以便创建客户端和单元测试，以确保客户端能够正确呈现内容。

内容作者根据在暂存环境中定义的内容模型创建内容。 使用内容片段创作工具，作者将创建新的内容片段或编辑现有的内容片段。 在发布内容之前，作者可以与开发人员合作将内容模型推送到开发环境中，或者仅为作者设置开发人员环境以预览内容在客户端的外观，从而预览其在客户端的外观。

## 设置 {#setup}

在AEM中开始使用无头功能之前，您需要确保已启用所有必需的功能。 此部分概述了所需内容。 在 [AEM Headless开发人员历程。](#overview.md)

您还可以选择将 [其他资源](#additional-resources) ，以了解有关各个主题的详细信息。

### 配置 {#configuration}

1. 启用内容片段
1. 启用GraphQL
1. 设置Headless SDK

## 实施您的第一个AEM Headless应用程序

以下是使用AEM实施首个无头应用程序以交付内容所需的内容概述。 如何执行这些步骤将在无头开发人员历程的后面部分详细介绍。

1. 创建内容片段模型
1. 创建内容片段
1. 使用GraphQL查询内容

## 最佳实践 {#best-practices}

一个无头项目不仅因为技术的实施而成功，而且因为良好的规划和项目管理。 对于内容作者和开发人员而言，在规划项目时请牢记以下一些最佳实践。

### 组织内容 {#organizing-content}

* 使结构尽可能复杂，但尽量保持简单。 更简单的内容结构有助于简化内容管理并提高系统性能。
* 在您的策略中优先重复使用内容。 创建可以在多个较高级别模型和渠道中重复使用的子模型和内容引用。
* 使内容结构尽可能不言而喻，以便内容作者能够快速学习和适应创作任务。
* 如果您具有访问限制，请尝试将内容模型与访问要求保持一致。
* 当您具有访问权限要求时，这些要求应会驱动您的内容层次结构。 将内容分组在一起，由同一组人员编辑。
* 将类似内容分组到文件夹中。
   * 内容作者更有可能复制并粘贴现有内容以创建新内容。 因此，在同一文件夹中执行此操作会提高效率。
   * AEM允许按文件夹设置允许的模型，以便 **新建** 按钮将仅显示该位置支持的模型。
* 如果在模型中设置了根文件夹，则可以简化新内容片段的内联内容片段编辑器创建过程。 然后，从业者不必选择位置，只需提供名称，即可开始编辑新引用。

### 创作内容 {#authoring}

* 对于特定于渠道的内容版本，请考虑使用内容片段变量。 根据内容主控同步变量，以简化内容更改管理。
* 邀请其他内容制作者审阅内容并提供带有注释和评论的反馈，这些内容和评论可在内容片段编辑器中使用，并在内容片段Admin Console中全局跨片段使用。
* 尽可能少地使用必备元素，保持移动。 强制元素可以阻止工作流。

### 创作全局内容 {#localization}

* 建立内容翻译规则和管理。 要减少系统负载，请将转换建立为可以以较长时间间隔运行的异步进程。 为本地化质量控制和错误修复留出时间。
* 利用您的翻译技术系统提供的所有功能，这些功能可与AEM集成，如翻译记忆库。
* 了解富媒体内容（如图像和视频）是否需要本地化。

## 下一步 {#what-is-next}

现在，您已完成AEM Headless开发人员历程的这一部分，接下来您应该：

* 了解设计内容时的重要规划注意事项。
* 了解在AEM中实施无头的步骤。
* 了解需要哪些必要工具和AEM配置。
* 了解最佳实践，以使您的无头历程顺畅、保持内容生成的高效性，并确保内容快速交付。

我们希望您以此基础知识为基础，充分了解AEM Headless的强大功能和灵活性，以便您能够将其用于自己的项目。 要实现此目的，您可以选择。

### 选择您自己的冒险 {#choose-your-path}

无论您的学习风格如何，Adobe都希望您在开始使用AEM Headless项目时取得成功。

* 如果您希望继续 **了解无头概念和AEM无头技术**，则您应该通过下一步审阅文档来继续您的AEM无头历程 [如何将内容建模为AEM内容模型](model-your-content.md) 其中，您了解如何在AEM中构建内容结构模型。
* 如果您愿意 **学习**，您可以跳转到 [AEM Headless动手操作入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) 在这里，您将通过实施一个简单的项目来公开AEM无头内容，从而直接进入AEM开发。

## 其他资源 {#additional-resources}

虽然建议您通过审阅文档来进入无头开发历程的下一部分 [如何将内容建模为AEM内容模型，](model-your-content.md) 以下是一些其他可选资源，可更深入地了解本文档中提到的某些概念，但无需继续进行无头历程。

* [AEM无头翻译历程](/help/journey-headless/translation/overview.md)  — 此文档历程使您能够广泛了解无头技术、AEM如何提供无头内容以及如何翻译无头内容。
* [AEM Sites无头开发](/help/sites-developing/headless/introduction.md)  — 简要介绍AEM Headless开发人员的发展方向以及必要的功能
* [AEM无头Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 使用这些动手实践教程探索如何使用各种选项通过AEM将内容交付到无头端点，并选择适合您的选项。
* [使用GraphQL API的无头内容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses)  — 请阅读本课程，概述在AEM中实施的GraphQL API。 需要通过AdobeID进行身份验证。
* [AEM指南WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  — 此GitHub项目包括高亮显示AEM GraphQL API的示例应用程序。
* [Headless快速入门指南](/help/sites-developing/headless/introduction.md#getting-started)  — 为已了解AEM的用户快速介绍AEM无头功能。
* [创建内容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 有关内容片段模型的技术文档
* [创建内容片段](/help/assets/content-fragments/content-fragments.md)  — 有关内容片段的技术文档
* [使用GraphQL查询内容](/help/assets/content-fragments/graphql-api-content-fragments.md)  — 有关GraphQL API的技术文档

<!-- HM-Links
* [Introduction to the Architecture of Adobe Experience Manager as a Cloud Service](/help/overview/architecture.md) - A complete overview of AEM's architecture
* [Headless Getting Started Guide](/help/implementing/developing/headless/introduction.md#getting-started) - A quick introduction to AEM's headless features for users already knowledgeable of AEM.
* [Create Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md) - Technical documentation on Content Fragment Models
* [Create Content Fragments](/help/assets/content-fragments/content-fragments.md) - Technical documentation on Content Fragments
* [Query content with GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) - Technical documentation on the GraphQL API

-->