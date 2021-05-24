---
title: 在We.Retail中尝试内容片段
seo-title: 在We.Retail中尝试内容片段
description: 在We.Retail中尝试内容片段
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 21%

---

# 在We.Retail{#trying-out-content-fragments-in-we-retail}中尝试内容片段

内容片段允许您创建渠道中性内容，以及（可能特定于渠道的）变量。 **We.Retail** (在AEM的现成实例中提供)提供了Lofoten中北极 **冲浪** 片段的基本示例。这说明：

* Adobe Experience Manager (AEM) 内容片段[作为独立于页面的资产而创建和管理](/help/assets/content-fragments/content-fragments.md)。这允许您创建渠道中性内容，以及各种（特定于渠道的）变量。

   * 请参阅[在We.Retail](#where-to-find-content-fragments-in-we-retail)中查找内容片段资产的位置

* 然后，在创作内容页面时，您可以[使用这些片段及其变体。](/help/sites-authoring/content-fragments.md)

   * 请参阅[We.Retail](#where-content-fragments-are-used-in-we-retail)中使用内容片段的位置

有关创建、管理、使用和开发内容片段的完整文档：

* 请参阅[更多信息](#further-information)

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-authoring/experience-fragments.md)**&#x200B;是 AEM 中的两个不同功能：
>
>* **内容片段**&#x200B;是可编辑的内容，主要为文本和相关图像。它们是纯内容，不带有任何设计和布局。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。

>
>
体验片段可以包含内容片段形式的内容，反之则不行。

## 在We.Retail {#where-to-find-content-fragments-in-we-retail}中的何处查找内容片段

We.Retail中有几个示例内容片段；通过&#x200B;**Assets**、**文件**、**We.Retail**、**英语**、**体验**&#x200B;导航。

这包括&#x200B;**Roctic Surfing in Lofoten**、一个片段以及相关的可视资产：

* 通过&#x200B;**Assets**、**Files**、**We.Retail**、**English**、**Experiences**、**Lofoten中的艺术冲浪**&#x200B;进行导航：

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

您可以选择和编辑Lofoten **中的**&#x200B;北极冲浪片段：

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

在此，您可以使用选项卡（左侧面板）编辑和管理](/help/assets/content-fragments/content-fragments.md)片段：[

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[](/help/assets/content-fragments/content-fragments-variations.md)** 变量，包括 [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[关联的内容](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[元数据](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## 其中，We.Retail {#where-content-fragments-are-used-in-we-retail}中使用内容片段

为了说明使用内容片段](/help/sites-authoring/content-fragments.md)进行页面创作时，下面提供了几个示例页面，例如：[

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

例如，“站点”页面中引用了“Lofoten **北极冲浪”内容片段：**

* 通过&#x200B;**Sites**、**We.Retail**、**语言硕士**、**英语**、**Experience**&#x200B;进行导航。 然后，打开Lofoten中的&#x200B;**北极冲浪**&#x200B;进行编辑：

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 更多信息 {#further-information}

有关更多详细信息，请参阅：

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * 了解如何创建、编辑和管理内容片段资产。

* [通过内容片段进行页面创作](/help/sites-authoring/content-fragments.md)

   * 在创作页面时使用内容片段。

* [开发AEM — 内容片段的组件](/help/sites-developing/components-content-fragments.md)

   * 内容片段的组件概述。

* [开发和扩展内容片段](/help/sites-developing/customizing-content-fragments.md)

   * 此信息可帮助您开发和扩展内容片段。
