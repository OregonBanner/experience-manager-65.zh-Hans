---
title: 在We.Retail中试用内容片段
seo-title: 在We.Retail中试用内容片段
description: 'null'
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: 759d2dd8d12861757bf7f54b77d8d3ca170887fe
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 21%

---


# 在We.Retail{#trying-out-content-fragments-in-we-retail}中尝试内容片段

内容片段允许您创建渠道中性内容，以及(可能特定于渠道的)变量。 **We.Retail** (如AEM的现成实例中所述)提供了Lofotenas的Arctic Surfing片 **段的** 基本示例。这说明：

* Adobe Experience Manager (AEM) 内容片段[作为独立于页面的资产而创建和管理](/help/assets/content-fragments/content-fragments.md)。这允许您创建渠道中性内容，以及各种（特定于渠道的）变量。

   * 请参阅[在We.Retail](#where-to-find-content-fragments-in-we-retail)中查找内容片段资产的位置

* 然后，在创作](/help/sites-authoring/content-fragments.md)内容页面时，您可以[使用这些片段及其变体。

   * 请参阅[We.Retail](#where-content-fragments-are-used-in-we-retail)中使用内容片段的位置

有关创建、管理、使用和开发内容片段的完整文档：

* 请参阅[其他信息](#further-information)

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-authoring/experience-fragments.md)**&#x200B;是 AEM 中的两个不同功能：
>
>* **内容片段**&#x200B;是可编辑的内容，主要为文本和相关图像。它们是纯内容，不带有任何设计和布局。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。

>
>
体验片段可以包含内容片段形式的内容，反之则不行。

## 在We.Retail{#where-to-find-content-fragments-in-we-retail}中查找内容片段的位置

We.Retail中有几个示例内容片段；通过&#x200B;**资产**、**文件**、**We.Retail**、**英语**、**体验**&#x200B;进行导航。

这包括Lofoten的&#x200B;**北极冲浪**、一个片段以及相关的视觉资产：

* 通过&#x200B;**资产**、**文件**、**We.Retail**、**英语**、**体验**、**Lofoten中的艺术冲浪**&#x200B;进行导航：

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

您可以选择并编辑Lofoten **中的**&#x200B;北极冲浪片段：

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

在此，您可以使用选项卡（左侧面板）编辑和管理[片段：](/help/assets/content-fragments/content-fragments.md)

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[变](/help/assets/content-fragments/content-fragments-variations.md)** 量，包括 [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[关联的内容](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[元数据](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## We.Retail {#where-content-fragments-are-used-in-we-retail}中使用内容片段的位置

要说明使用内容片段](/help/sites-authoring/content-fragments.md)创作[页面，下面提供了几个示例页面，例如：

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

例如，Lofoten **中的**&#x200B;北极冲浪内容片段在“站点”页面中引用：

* 通过&#x200B;**Sites**、**We.Retail**、**语言母版**、**英语**、**Experience**&#x200B;进行导航。 然后打开Lofoten **北极冲浪网进行编辑：**

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 更多信息 {#further-information}

有关详细信息，请参阅：

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * 了解如何创建、编辑和管理内容片段资产。

* [通过内容片段进行页面创作](/help/sites-authoring/content-fragments.md)

   * 在创作页面时使用内容片段。

* [开发AEM —— 内容片段组件](/help/sites-developing/components-content-fragments.md)

   * 内容片段组件概述。

* [开发和扩展内容片段](/help/sites-developing/customizing-content-fragments.md)

   * 帮助您开发和扩展内容片段的信息。

