---
title: 集合、片段和片段模板的多租约
description: 了解多租赁功能如何让您根据客户组织隔离CRX存储库中的内容，以防止未经授权的访问。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 集合、片段和片段模板的多租约 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

通过多租赁功能，您可以根据组织前缀和组织ID在CRX中隔离内容，以保护内容免受其他组织用户的未授权访问。

Adobe Experience Manager(AEM)资产会将每个组织的数据存储在不同的路径中。 每个组织特定路径都由组织前缀和组织ID标识，这些ID包含在CRX中存储不同类型资产的传统位置中。

例如，如果您创建了名为的文件夹， `Demo`则AEM资产通常会在上存储该文件夹 `../content/dam/Demo`。 启用多租赁后，您现在可以在 `../content/dam/<organization prefix>/<organization id>Demo`

例如，如果 [!DNL Adobe Marketing Cloud] AEM资产（按需）的用户已分配到组织 `aodpremium` ，则可以使用多租赁功能配置路径以隔离其 `../content/dam/<mac>/<aodpremium>Demo` 内容。 在此示例中， `mac` 是组织前缀， `aodpremium` 也是组织ID。

根据用户的组织和ID，此限定路径显示在AEM资产界面和各种向导中，包括用于实施隔离的移动和代码片断创建向导。

通过多租赁功能，您可以隔离以下类型的资产和组件：

* 收藏集
* 公共集合
* 目录（包括添加／选择页面向导）
* 模板
* 代码片断模板
* Lightbox
