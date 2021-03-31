---
title: 集合、片段和片段模板的多租赁
description: 了解多租赁功能如何让您根据客户组织隔离CRX存储库中的内容，以防止未经授权的访问。
contentOwner: AG
role: 架构师、管理员、领导者
feature: 收藏集
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 1%

---


# 集合、片段和片段模板的多租户{#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租赁功能允许您根据组织前缀和组织ID在CRX中隔离内容，以保护内容免遭其他组织的用户未经授权的访问。

[!DNL Adobe Experience Manager Assets] 将每个组织的数据存储在不同的路径中。每个组织特定路径由组织前缀和组织ID标识
这包括在CRX中存储不同类型资源的传统位置中。

例如，如果您创建名为`Demo`的文件夹，[!DNL Experience Manager]资产通常会将该文件夹存储在`../content/dam/Demo`。 启用多租赁后，您现在可以在`../content/dam/<organization prefix>/<organization id>Demo`存储数据

例如，对于分配给`aodpremium`组织的[!DNL Assets]（按需）的[!DNL Adobe Marketing Cloud]用户，您可以使用多租赁功能配置`../content/dam/<mac>/<aodpremium>Demo`路径以隔离其内容。 在此示例中，`mac`是组织前缀，`aodpremium`是组织ID。

根据用户的组织和ID，此限定路径显示在[!DNL Assets]界面和各种向导中，包括用于强制隔离的“移动”和“代码片断”创建向导。

通过多租赁功能，您可以隔离以下类型的资产和组件：

* 收藏集
* 公共集合
* 目录（包括“添加/选择页面”向导）
* 模板
* 片段模板
* Lightbox
