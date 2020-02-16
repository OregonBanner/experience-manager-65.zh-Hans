---
title: 模型概述
seo-title: 模型概述
description: 'null'
seo-description: 'null'
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 模型概述{#models-overview}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

模型管理包括创建和管理模型，以便与最终数据对象关联。 每个模型将包括为便于创建和呈现对象而需要的所有属性和字段定义。

模型管理涉及创 **建模型**、 **实体**&#x200B;和 **空间**。 下图说明了AEM内容与模型之间的关系。

![chlimage_1-81](assets/chlimage_1-81.png)

## 内容模型 {#the-content-model}

模型描述内容类型并指示哪些信息可供本机应用程序使用。 它是内容组成部分的描述。 内容模型是如何构建内容的规则。 内容模型包括哪些数据可用、哪些资产可用、资产与数据之间的关系、与其他内容模型的关系以及可用元数据。

模型还用作将现有AEM内容转换为可供本机移动应用程序轻松使用的对象的方法。

内容服务将为常见对象（如资产、资产集合、HTML页面、应用程序配置和渠道独立页面）提供一些现成模型。 这些组件将可进行配置，因此无需AEM开发工作即可满足特定客户需求。

用户可以创建自己的模型。 这允许创建尚未由AEM管理的新内容类型。 模型创建是通过使用现有基元类型的UI完成的。

下图说明了AEM Mobile应用程序的内容模型以及如何将实体、文件夹和空间分配给应用程序。

![chlimage_1-82](assets/chlimage_1-82.png)

### The Models {#the-models}

模型用于确定如何创建图元。 它们定义实体中可用的内容以及该数据从AEM内容生成的方式。 在开始使用空间、文件夹和实体之前，您应该熟悉创建和管理模型。

>[!NOTE]
>
>模型存在于应用程序之外，因为多个应用程序可以使用它。


请参 **[阅模型](/help/mobile/administer-mobile-apps.md)**，以在仪表板和存储库中创建和管理模型。

### 内容模型中的实体 {#entities-in-content-model}

实体是内容模型的实例。 实体通过Content Services API暴露到客户端库，并为本机应用程序以独立于渠道的方式访问内容提供了一种方法。

对于现有AEM内容，将使用模型和AEM内容源生成实体。 例如，页面实体是从AEM页面和页面模型生成的与渠道和布局无关的对象。

对实体的引用内容所做的更改将导致对实体进行更改。 例如，如果更 *新了cq:page* ，则基于该页面的所有实体也将更新。

请参 **[阅使用实体](/help/mobile/spaces-and-entities.md)**，从模型创建自定义实体。

>[!NOTE]
>
>如果模型与现有AEM内容不对应，例如客户创建了新模型，则将有一个UI，这样客户可以创建新实体。


### 内容模型中的空格 {#spaces-in-content-model}

空间用于组织实体以便轻松访问。 空间可以包含一个或多个实体类型，并且可以包含子文件夹。

在AEM端，空间是管理相关实体的便捷方式。 它还可用于分配授权权限。 可以对空间进行授权，然后该空间将保护该空间中的实体。

*例如*,

用户有三个实体的一般分类。 一个仅供内部使用，另一个只供公共使用，第三个只供许多应用程序使用的公共实体使用。 为了便于管理，用户创建了三个空间： *internal*、 *public* （同时包含英语和法语内容）和 *common* ，以便管理如下所述的相应实体：

* /content/entities/internal
* /content/entities/public/cn
* /content/entities/public/fr
* /content/entities/common

服务端点将被提供给该空间，这样本机客户端库可以请求空间内容的列表。 此“列表”将作为JSON对象返回。

请参 **[阅空间和实体](/help/mobile/spaces-and-entities.md)**，以创建和发布空间。

>[!NOTE]
>
>一个空间可供许多应用程序使用，而一个应用程序可以使用多个空间。

### 内容模型中的文件夹 {#folders-in-content-model}

文件夹允许用户根据需要组织实体，并便于更精细的ACL控制。 空间可以包含文件夹以帮助进一步组织空间的内容和资产。 用户可以在空间下创建自己的层次结构。

请参 **[阅使用空间中的文件夹](/help/mobile/spaces-and-entities.md)**，以在空间中创建和管理文件夹。
