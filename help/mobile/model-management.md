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
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---


# 模型概述{#models-overview}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

模型管理涉及创建和管理模型，以便与最终数据对象关联。 每个模型将包括为便于对象的创建和呈现而需要的所有属性和字段定义。

模型管理涉及创建&#x200B;**模型**、**实体**&#x200B;和&#x200B;**空格**。 下图说明AEM内容与模型之间的关系。

![chlimage_1-81](assets/chlimage_1-81.png)

## 内容模型{#the-content-model}

模型描述内容类型，并表示哪些信息将对本机应用程序可用。 它是内容组成部分的描述。 内容模型是如何构建内容的规则。 内容模型包括可用数据、可使用资产、资产与数据之间的关系、与其他内容模型的关系以及可用元数据。

模型还可以将现有AEM内容转换为本机移动应用程序可轻松使用的对象。

Content Services将为常见对象(如资产、资产集合、HTML页面、应用程序配置和渠道独立页面)提供一些现成模型。 这些功能将可配置，因此无需AEM开发工作即可满足特定客户需求。

用户可以创建自己的模型。 这允许创建尚未由AEM管理的新内容类型。 模型创建是使用现有基元类型通过UI完成的。

下图说明了AEM Mobile应用程序的内容模型以及如何将实体、文件夹和空间分配给应用程序。

![chlimage_1-82](assets/chlimage_1-82.png)

### 型号{#the-models}

模型用于确定如何创建图元。 它们定义实体中可用的内容，以及如何从AEM内容生成该数据。 在开始使用空格、文件夹和实体之前，您应熟悉创建和管理模型。

>[!NOTE]
>
>模型存在于应用程序之外，因为多个应用程序可以使用它。


请参阅&#x200B;**[模型](/help/mobile/administer-mobile-apps.md)**&#x200B;以在仪表板和存储库中创建和管理模型。

### 内容模型{#entities-in-content-model}中的实体

实体是内容模型的实例。 实体通过Content Services API公开到客户端库，并为本机应用程序以独立于渠道的方式访问内容提供了一种方法。

如果存在AEM内容，则使用模型和AEM内容源生成实体。 例如，页面实体是从AEM页面和页面模型生成的与渠道和布局无关的对象。

对实体的引用内容所做的更改将导致对实体进行更改。 例如，如果&#x200B;*cq:page*&#x200B;已更新，则基于该页面的所有实体也将更新。

请参阅&#x200B;**[使用实体](/help/mobile/spaces-and-entities.md)**&#x200B;从模型创建自定义实体。

>[!NOTE]
>
>如果模型与现有AEM内容不对应，例如客户创建了新模型，则将有一个UI，这样客户可以创建新实体。


### 内容模型{#spaces-in-content-model}中的空格

空间用于组织实体以便轻松访问。 空间可包含一个或多个实体类型，并可包含子文件夹。

在AEM方面，空间是管理相关实体的便捷方式。 它还可用于分配授权权限。 可以对空间进行授权，然后该空间将保护该空间中的实体。

*例如*,

用户具有三个实体的一般分类。 一个仅供内部使用，另一个获准供公众使用，第三个适用于许多应用程序使用的常见实体。 为便于管理，用户创建三个空格，即&#x200B;*internal*、*public*（同时包含英语和法语内容）和&#x200B;*common*，用于管理如下所述的适当实体：

* /content/entities/internal
* /content/entities/public/cn
* /content/entities/public/fr
* /content/entities/common

服务终点将被提供给该空间，以便本机客户端库可以请求空间内容的列表。 此“列表”将作为JSON对象返回。

有关创建和发布空间的信息，请参阅&#x200B;**[空格和实体](/help/mobile/spaces-and-entities.md)**。

>[!NOTE]
>
>一个空间可供许多应用程序使用，而一个应用程序可以使用多个空间。

### 内容模型{#folders-in-content-model}中的文件夹

文件夹允许用户根据需要组织实体，并有助于更精细的ACL控制。 空间可以包含文件夹，以帮助进一步组织空间的内容和资产。 用户可以在空间下创建自己的层次结构。

请参阅&#x200B;**[使用空间中的文件夹](/help/mobile/spaces-and-entities.md)**&#x200B;以创建和管理空间中的文件夹。
