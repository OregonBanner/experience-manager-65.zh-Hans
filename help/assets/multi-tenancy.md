---
title: 收藏集、代码片段和代码片段模板的多租户
description: 了解多租户功能如何让您根据客户组织分离CRX存储库中的内容，以防止未经授权的访问。
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---

# 收藏集、代码片段和代码片段模板的多租户 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租户功能允许您根据组织前缀和组织ID在CRX中分隔内容，以保护内容不被其他组织的用户未经授权访问。

[!DNL Adobe Experience Manager Assets] 以不同的路径存储每个组织的数据。 每个特定于组织的路径由组织前缀和组织ID标识，组织ID包含在传统位置，其中不同类型的资产存储在CRX中。

例如，如果您创建一个名为的文件夹， `Demo`， [!DNL Experience Manager] 资产通常将文件夹存储在 `../content/dam/Demo`. 启用多租户后，您现在可以将数据存储在 `../content/dam/<organization prefix>/<organization id>Demo`

例如，如果 [!DNL Adobe Marketing Cloud] 用户 [!DNL Assets] （按需）已分配至 `aodpremium` 组织，则可以使用多租户功能来配置 `../content/dam/<mac>/<aodpremium>Demo` 用于分隔其内容的路径。 在此示例中， `mac` 是组织前缀和 `aodpremium` 是组织ID。

根据用户的组织和ID，此限定路径将显示在 [!DNL Assets] 界面和各种向导，包括用于实施隔离的移动和代码片段创建向导。

多租户功能允许您分隔以下类型的资源和组件：

* 收藏集
* 公共收藏集
* 目录（包括“添加/选择页面”向导）
* 模板
* 代码片段模板
* Lightbox
