---
title: 集合、片段和片段模板的多租户
description: 了解多租赁功能如何让您根据客户组织隔离CRX存储库中的内容，以防止未经授权的访问。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# 集合、片段和片段模板的多租户 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租赁功能允许您根据组织前缀和组织ID在CRX中隔离内容，以防止其他组织的用户对内容进行未经授权的访问。

Adobe Experience Manager资产会将每个组织的数据存储在不同的路径中。 每个特定于组织的路径都由组织前缀和组织ID标识，这些ID包含在传统位置中，在传统位置，不同类型的资产会存储在CRX中。

例如，如果您创建了名为的文 `Demo`件夹，则Experience Manager资产通常会在上存储该文件夹 `../content/dam/Demo`。 启用多租赁后，您现在可以在 `../content/dam/<organization prefix>/<organization id>Demo`

例如，如果资产 [!DNL Adobe Marketing Cloud] （按需）的用户已分配到组织 `aodpremium` ，则可以使用多租赁功能配置路径以 `../content/dam/<mac>/<aodpremium>Demo` 隔离其内容。 在此示例中， `mac` 是组织前缀 `aodpremium` 和组织ID。

根据用户的组织和ID，此限定路径显示在“资产”界面和各种向导中，包括用于实施隔离的“移动”和“片段”创建向导。

通过多租赁功能，您可以隔离以下类型的资产和组件：

* 收藏集
* 公共集合
* 目录（包括添加／选择页面向导）
* 模板
* 片段模板
* Lightbox
