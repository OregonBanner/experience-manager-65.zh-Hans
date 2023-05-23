---
title: 将收藏集发布到 Brand Portal
seo-title: Publish collections to Brand Portal
description: 瞭解如何發佈和取消發佈集合到Brand Portal。
seo-description: Learn how to publish and unpublish collections to Brand Portal.
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
feature: Brand Portal
role: User
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 36%

---

# 将收藏集发布到 Brand Portal {#publish-collections-to-brand-portal}

身為Adobe Experience Manager (AEM) Assets管理員，您可以將集合發佈至貴組織的AEM Assets Brand Portal執行個體。 不過，您必須先整合AEM Assets與Brand Portal。 有关详细信息，请参阅[使用 Brand Portal 配置 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

如果您在AEM Assets中對原始集合進行後續修改，則在您再次發佈集合之前，這些變更不會反映在Brand Portal中。 此特性可確保進行中的變更不會出現在Brand Portal中。 只有管理员发布的已批准更改才会出现在 Brand Portal 中。

>[!NOTE]
>
>无法将内容片段发布到 Brand Portal。因此，如果您在AEM作者上選取內容片段，則 **發佈至Brand Portal** 動作無法使用。
>
>如果從AEM Author將包含內容片段的集合發佈到Brand Portal，則除了內容片段以外，資料夾的所有內容都會複製到Brand Portal介面。

## 將集合發佈至Brand Portal {#publish-a-collection-to-brand-portal}

1. 在 AEM Assets UI 中，单击 AEM 徽标。
1. 在&#x200B;**导航**&#x200B;页面中，转到 **Assets > 收藏集**。
1. 在集合控制檯中，選取您要發佈至Brand Portal的集合。

   ![select_collection](assets/select_collection.png)

1. 在工具栏中，单击&#x200B;**发布到 Brand Portal**。
1. 在确认对话框中，单击&#x200B;**发布**。
1. 关闭确认消息。
1. 以管理員身分登入Brand Portal。 已发布的收藏集将显示在“收藏集”控制台中。

   ![已发布的收藏集](assets/published_collection.png)

## 取消发布收藏集 {#unpublish-collections}

您可以取消發佈從AEM Assets發佈到Brand Portal的集合。 取消發佈原始集合後，Brand Portal使用者將無法再使用其副本。

1. 從AEM Assets例項的集合控制檯中，選取您要取消發佈的集合。

   ![select_collection-1](assets/select_collection-1.png)

1. 在工具栏中，单击&#x200B;**从 Brand Portal 中删除**&#x200B;图标。
1. 在对话框中，单击&#x200B;**取消发布**。
1. 关闭确认消息。收藏集将从 Brand Portal 界面中删除。
