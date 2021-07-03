---
title: 收藏集、片段和代码片段模板的多租户
description: 了解多租户功能如何让您根据客户组织来分隔CRX存储库中的内容，以防止未经授权的访问。
contentOwner: AG
role: Architect, Admin, Leader
feature: 收藏集
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 1%

---

# 收藏集、片段和代码片段模板的多租户 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租户功能允许您根据组织前缀和组织ID在CRX中分隔内容，以防止其他组织的用户对内容进行未经授权的访问。

[!DNL Adobe Experience Manager Assets] 将每个组织的数据存储在不同的路径中。每个特定于组织的路径由组织前缀和组织ID来标识
CRX中存储不同类型资产的传统位置中包含的附加内容。

例如，如果您创建名为`Demo`的文件夹，则[!DNL Experience Manager]资产会将该文件夹传统上存储在`../content/dam/Demo`。 启用多租户后，您现在可以在`../content/dam/<organization prefix>/<organization id>Demo`存储数据

例如，如果[!DNL Assets]（按需）的[!DNL Adobe Marketing Cloud]用户已分配给`aodpremium`组织，则可以使用多租户功能配置`../content/dam/<mac>/<aodpremium>Demo`路径以分隔其内容。 在此示例中，`mac`是组织前缀，`aodpremium`是组织ID。

根据用户的组织和ID，此限定路径显示在[!DNL Assets]界面和各种向导中，包括用于强制隔离的“移动”和“代码片段创建”向导。

多租户功能允许您隔离以下类型的资产和组件：

* 收藏集
* 公共收藏集
* 目录（包括“添加/选择页面”向导）
* 模板
* 代码片段模板
* Lightbox
