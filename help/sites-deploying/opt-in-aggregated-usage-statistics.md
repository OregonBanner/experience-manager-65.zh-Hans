---
title: 选择加入汇总使用情况统计信息收集
seo-title: 选择加入汇总使用情况统计信息收集
description: 了解如何选择汇总的使用情况统计信息。
seo-description: 了解如何选择汇总的使用情况统计信息。
uuid: 8bd0b870-4bea-42e1-8179-e900164591b6
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 075f53cc-146b-4eea-bfbb-54beaed97915
docset: aem65
exl-id: e626bdd8-b7ae-4de5-a0a0-47fb74c080d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# 选择加入汇总使用情况统计信息集合{#opting-into-aggregated-usage-statistics-collection}

## 简介 {#introduction}

您可以通过发送有关如何与AEM进行交互的Adobe统计信息来帮助改进Adobe Marketing Cloud。 此信息不包含有关贵公司网站访客的任何数据，仅用于帮助Adobe交付、支持和改善用户体验。

您可以使用触屏UI或Web控制台来选择启用使用情况统计信息收集。

>[!NOTE]
>
>有各种数据保护和隐私法规；包括（例如，GDPR和CCPA）。 AEM Sites随时准备帮助客户履行其数据保护和隐私合规义务。 本页将指导客户完成选择启用（或禁用）汇总使用情况统计收集的过程。
>
>有关更多信息，另请参阅[Adobe的隐私中心](https://www.adobe.com/privacy.html)。

>[!NOTE]
>
>您还可以随时通过使用[Web Console](/help/sites-deploying/opt-in-aggregated-usage-statistics.md#opt-in-by-using-the-web-console)或不选择AEM选择加入屏幕上的选择加入选项来选择退出。

## 使用触屏UI {#opt-in-by-using-the-touch-ui}选择加入

首次启动AEM时，您可以使用触屏UI选择加入，如下所示：

1. 在AEM导航屏幕上，单击&#x200B;**收件箱**（铃铛）图标。

   ![usage_statisticsnavigationscreen](assets/usage_statisticsnavigationscreen.png)

1. 在下拉列表中，单击“**启用汇总使用情况统计信息收集**”。

   ![usage_statisticsnavigationscreen2](assets/usage_statisticsnavigationscreen2.png)

1. 在选择加入屏幕上，选择“**允许收集汇总的使用情况统计信息**”。

   ![usage_statisticsopt_inscreen](assets/usage_statisticsopt-inscreen.png)

1. 单击“**Done**”。

## 使用Web控制台{#opt-in-by-using-the-web-console}选择加入

您可以通过使用Web控制台选择启用（或选择禁用），如下所示：

1. 在AEM Navigation屏幕上，单击&#x200B;**工具**，然后单击&#x200B;**操作**。

   ![usage_statisticsopshashboard](assets/usage_statisticsopsdashboard.png)

1. 在“操作”窗口中，单击&#x200B;**Web控制台**。

   ![usage_statisticswebconsole](assets/usage_statisticswebconsole.png)

1. 搜索“**汇总使用情况统计信息集合**”。
1. 单击&#x200B;**编辑**&#x200B;图标。

   ![usage_statisticscollectionedit](assets/usage_statisticscollectionedit.png)

1. 选中&#x200B;**Enabled**&#x200B;复选框。 或者，如果要选择退出使用情况统计信息收集，则可以取消选中此复选框。

   ![usage_statisticsselect](assets/usage_statisticsselect.png)

1. 单击&#x200B;**保存**。
