---
title: 集合、片段和片段模板的多租户
description: 了解多租赁功能如何让您根据客户组织隔离CRX存储库中的内容，以防止未经授权的访问。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---


# 集合、片段和片段模板的多租户 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租赁功能允许您根据组织前缀和组织ID在CRX中隔离内容，以防止其他组织的用户对内容进行未经授权的访问。

[!DNL Adobe Experience Manager Assets] 将每个组织的数据存储在不同的路径中。 每个特定于组织的路径都由组织前缀和组织ID标识，这些ID包含在传统位置中，在传统位置，不同类型的资产会存储在CRX中。

例如，如果您创建了名为的文件夹， `Demo`则资 [!DNL Experience Manager] 产通常会在上存储该文件夹 `../content/dam/Demo`。 启用多租赁后，您现在可以在 `../content/dam/<organization prefix>/<organization id>Demo`

例如，如果对于 [!DNL Adobe Marketing Cloud] 分配给 [!DNL Assets] 组织的（按需）用户，您可以使用多租 `aodpremium` 赁功能配置路径以隔离其 `../content/dam/<mac>/<aodpremium>Demo` 内容。 在此示例中， `mac` 是组织前缀 `aodpremium` 和组织ID。

根据用户的组织和ID，此限定路径显示在界面和各种向导中， [!DNL Assets] 包括用于实施隔离的“移动”和“片段”创建向导。

通过多租赁功能，您可以隔离以下类型的资产和组件：

* 收藏集
* 公共集合
* 目录（包括添加／选择页面向导）
* 模板
* 片段模板
* Lightbox
