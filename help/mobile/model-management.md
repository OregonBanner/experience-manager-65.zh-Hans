---
title: 模型概述
description: 了解如何使用模型管理，其中涉及创建和管理用于与最终数据对象关联的模型。
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 50785534-5784-4354-b123-5e640b7c0242
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# 模型概述{#models-overview}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

模型管理涉及创建和管理用于与最终数据对象关联的模型。 每个模型都包含便于创建和渲染对象所需的所有属性和字段定义。

模型管理涉及创建 **模型**， **实体**、和 **空间**. 下图说明了AEM内容和模型之间的关系。

![chlimage_1-81](assets/chlimage_1-81.png)

## 内容模型 {#the-content-model}

模型描述内容类型并指示哪些信息对本机应用程序可用。 它是对构成内容的内容的内容的描述。 内容模型是有关如何构建内容的规则。 内容模型包括哪些数据可用、哪些资产可用、资产和数据之间的关系、与其他内容模型的关系以及可用的元数据。

模型还可以作为一种将现有AEM内容转换为本机移动设备应用程序可以轻松使用的对象的方法。

Content Services为常见对象(如资源、资源收藏集、HTML页面、应用程序配置和独立于渠道的页面)提供了一些现成的模型。 它们可以配置，因此可以满足特定客户需求而无需AEM开发工作。

用户可以创建自己的模型。 这样可创建尚未由AEM管理的新内容类型。 模型创建是使用现有基元类型通过UI完成的。

下图说明了AEM Mobile应用程序的内容模型以及如何将实体、文件夹和空间分配给应用程序。

![chlimage_1-82](assets/chlimage_1-82.png)

### 模型 {#the-models}

模型用于确定如何创建图元。 它们定义实体中可用的内容以及如何从AEM内容生成数据。 在开始使用空间、文件夹和实体之前，您应该熟悉如何创建和管理模型。

>[!NOTE]
>
>模型存在于应用程序之外，因为多个应用程序可以使用该模型。
>

要在功能板和存储库中创建和管理模型，请参阅 **[模型](/help/mobile/administer-mobile-apps.md)**.

### 内容模型中的实体 {#entities-in-content-model}

实体是内容模型的实例。 实体通过Content Services API向客户端库公开，并为本机应用程序提供了一种独立于渠道的方式访问内容。

如果存在AEM内容，则使用模型和AEM内容源生成实体。 例如，页面实体是从AEM页面和页面模型生成的独立于渠道和布局的对象。

对实体的引用内容所做的更改会导致对实体的更改。 例如，如果 *cq：page* 将更新，然后基于该页面的任何实体也会更新。

要从模型创建自定义实体，请参阅 **[使用实体](/help/mobile/spaces-and-entities.md)**.

>[!NOTE]
>
>如果模型未与现有AEM内容相对应，例如客户创建了模型，则会显示UI，以便客户能够创建实体。
>

### 内容模型中的空间 {#spaces-in-content-model}

空间用于组织实体以便于访问。 空间可以包含一个或多个实体类型，也可以包含子文件夹。

在AEM端，空间是一种管理相关实体的便捷方式。 它也可用于分配授权权限。 可以对空间进行授权，从而保护该空间中的实体。

*例如*，

用户有三个实体的常规分类。 一个仅供内部使用，另一个已批准用于公共使用，还有第三个用于许多应用程序使用的公共实体。 为了便于管理，用户创建了三个空间，即 *内部*， *公共* （包含英语和法语内容），以及 *公共* 管理下述适当实体：

* /content/entities/internal
* /content/entities/public/en
* /content/entities/public/fr
* /content/entities/common

向空间提供服务端点，以便本地客户端库可以请求空间内容的列表。 此“列表”将作为JSON对象返回。

请参阅 **[空间和实体](/help/mobile/spaces-and-entities.md)** 创建和发布空间。

>[!NOTE]
>
>空间可供许多应用程序使用，而应用程序则可使用许多空间。

### 内容模型中的文件夹 {#folders-in-content-model}

利用文件夹，用户可根据需要组织实体并促进更细微的ACL控制。 空间可以包含文件夹，以帮助进一步组织空间的内容和资源。 用户可以在空间下创建自己的层次结构。

要创建和管理空间中的文件夹，请参阅 **[使用空间中的文件夹](/help/mobile/spaces-and-entities.md)**.
