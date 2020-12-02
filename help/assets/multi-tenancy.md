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


# 集合、片段和片段模板的多租户{#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租赁功能允许您根据组织前缀和组织ID在CRX中隔离内容，以防止其他组织的用户对内容进行未经授权的访问。

[!DNL Adobe Experience Manager Assets] 将每个组织的数据存储在不同的路径中。每个组织特定路径由组织前缀和组织ID标识
它包含在传统位置，在该位置，不同类型的资源存储在CRX中。

例如，如果您创建名为`Demo`的文件夹，[!DNL Experience Manager]资产通常会将该文件夹存储在`../content/dam/Demo`。 启用多租赁后，您现在可以在`../content/dam/<organization prefix>/<organization id>Demo`存储数据

例如，如果[!DNL Assets]（按需）的[!DNL Adobe Marketing Cloud]用户被分配给`aodpremium`组织，则可以使用多租赁功能配置`../content/dam/<mac>/<aodpremium>Demo`路径以隔离其内容。 在此示例中，`mac`是组织前缀，`aodpremium`是组织ID。

根据用户的组织和ID，此限定路径显示在[!DNL Assets]界面和各种向导中，包括用于强制隔离的“移动”和“代码片断”创建向导。

通过多租赁功能，您可以隔离以下类型的资产和组件：

* 收藏集
* 公共集合
* 目录（包括添加／选择页面向导）
* 模板
* 片段模板
* Lightbox
