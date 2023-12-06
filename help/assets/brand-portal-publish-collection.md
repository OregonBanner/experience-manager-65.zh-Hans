---
title: 将收藏集发布到Brand Portal
description: 了解如何将收藏集发布和取消发布到Brand Portal。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 30%

---

# 将收藏集发布到Brand Portal {#publish-collections-to-brand-portal}

作为Adobe Experience Manager (AEM) Assets管理员，您可以将收藏集发布到贵组织的AEM Assets Brand Portal实例。 但是，您必须首先将AEM Assets与Brand Portal集成。 有关详细信息，请参阅[使用 Brand Portal 配置 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

如果您在AEM Assets中对原始收藏集进行后续修改，则在再次发布该收藏集之前，这些更改不会反映在Brand Portal中。 此特性可确保在Brand Portal中不会出现进行中的更改。 只有管理员发布的已批准更改才会出现在 Brand Portal 中。

>[!NOTE]
>
>无法将内容片段发布到 Brand Portal。因此，如果您在AEM Author中选择内容片段， **发布到Brand Portal** 操作不可用。
>
>如果将包含内容片段的收藏集从AEM Author发布到Brand Portal，则文件夹中除内容片段之外的所有内容都将复制到Brand Portal界面。

## 将收藏集发布到Brand Portal {#publish-a-collection-to-brand-portal}

1. 在 AEM Assets UI 中，单击 AEM 徽标。
1. 从 **导航** 页面，转到 **资产>收藏集**.
1. 在收藏集控制台中，选择要发布到Brand Portal的收藏集。

   ![select_collection](assets/select_collection.png)

1. 在工具栏中，单击&#x200B;**发布到 Brand Portal**。
1. 在确认对话框中，单击&#x200B;**发布**。
1. 关闭确认消息。
1. 以管理员身份登录到Brand Portal。 已发布的收藏集将显示在“收藏集”控制台中。

   ![已发布的收藏集](assets/published_collection.png)

## 取消发布收藏集 {#unpublish-collections}

您可以取消发布从AEM Assets发布到Brand Portal的收藏集。 取消发布原始收藏集后，Brand Portal用户将无法再使用其副本。

1. 从AEM Assets实例的收藏集控制台中，选择要取消发布的收藏集。

   ![select_collection-1](assets/select_collection-1.png)

1. 在工具栏中，单击&#x200B;**从 Brand Portal 中删除**&#x200B;图标。
1. 在对话框中，单击&#x200B;**取消发布**。
1. 关闭确认消息。收藏集将从 Brand Portal 界面中删除。
