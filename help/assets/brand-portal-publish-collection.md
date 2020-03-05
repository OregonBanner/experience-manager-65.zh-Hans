---
title: 将集合发布到Brand Portal
seo-title: 将集合发布到Brand Portal
description: 了解如何将集合发布和取消发布到Brand Portal。
seo-description: 了解如何将集合发布和取消发布到Brand Portal。
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
translation-type: tm+mt
source-git-commit: 9f923782d3d0a7bdf45b18e8025bd2d083acf77c

---


# Publish collections to Brand Portal {#publish-collections-to-brand-portal}

作为Adobe Experience Manager(AEM)资产管理员，您可以将集合发布到您组织的AEM Assets Brand Portal实例。 但是，您必须先将AEM资产与Brand Portal集成。 有关详细信息，请 [参阅配置AEM资产与Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md)。

如果您在AEM资产中对原始集合进行后续修改，则在您再次发布集合之前，这些更改不会反映在Brand Portal中。 此特性可确保在品牌门户中不提供进行中的更改。 只有管理员发布的已批准更改才可在Brand Portal中使用。

>[!NOTE]
>
>内容片段无法发布到Brand Portal。 因此，如果您在AEM作者上选择内容片段，则“发布 **到品牌门户** ”操作将不可用。
>
>如果包含内容片段的集合从AEM作者发布到Brand Portal，则文件夹中除内容片段之外的所有内容都将被复制到Brand Portal界面。

## 将集合发布到Brand Portal {#publish-a-collection-to-brand-portal}

1. 在AEM资产UI中，单击AEM徽标。
1. From **Navigation** page, go to **Assets > Collections**.
1. 从“集合”控制台中，选择要发布到Brand Portal的集合。

   ![select_collection](assets/select_collection.png)

1. 在工具栏中，单击“ **发布到品牌门户”**。
1. In the confirmation dialog, click **Publish**.
1. 关闭确认消息。
1. 以管理员身份登录到Brand Portal。 已发布的集合在“集合”控制台中可用。

   ![已发布集合](assets/published_collection.png)

## 取消发布集合 {#unpublish-collections}

您可以取消发布从AEM资产发布到Brand Portal的集合。 在取消发布原始集合后，Brand Portal用户将无法再使用其副本。

1. 从AEM资产实例的收藏集控制台中，选择要取消发布的收藏集。

   ![select_collection-1](assets/select_collection-1.png)

1. 在工具栏中，单击“从 **Brand Portal中删除** ”图标。
1. 在对话框中，单击“取 **消发布**”。
1. 关闭确认消息。 集合将从Brand Portal界面中删除。

