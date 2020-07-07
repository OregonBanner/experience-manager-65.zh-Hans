---
title: 通过内容片段进行页面创作
seo-title: 通过内容片段进行页面创作
description: 通过 AEM 内容片段，您可以设计、创建、管理和使用独立于页面的内容
seo-description: 通过 AEM 内容片段，您可以设计、创建、管理和使用独立于页面的内容
uuid: 987de428-8354-4b23-a552-3ea415122184
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4049a7a5-4b33-4462-a25f-3c0daeb6a8a9
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 99%

---


# 通过内容片段进行页面创作{#page-authoring-with-content-fragments}

Adobe Experience Manager (AEM) 内容片段[作为独立于页面的资产而创建和管理](/help/assets/content-fragments/content-fragments.md)。

这允许您创建渠道中性内容，以及各种（特定于渠道的）变量。您随后可以在创作内容页面时使用这些片段及其变量。

结构化内容片段与更新的 JSON 导出程序结合使用时，还可用于通过 Content Services 将 AEM 内容传送到 AEM 页面以外的渠道。

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-authoring/experience-fragments.md)**是 AEM 中的两个不同功能：
>
>* **内容片段**&#x200B;是可编辑的内容，主要为文本和相关图像。它们是纯内容，不带有任何设计和布局。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。

>
>
体验片段可以包含内容片段形式的内容，反之则不行。

>[!CAUTION]
>
>本页必须结合[使用内容片段](/help/assets/content-fragments/content-fragments.md)（及相关页面）一起阅读，因为它不仅介绍了基本术语和概念，还介绍了如何创建和管理片段。

内容片段允许：

* **营销和营销活动策略**

   * 通过集中管理的内容片段审核内容。

* **Creative Pro**

   * 通过与内容片段关联的收藏集跟踪创意资产。

* **撰稿人**

   * 在 AEM 内容片段编辑器中编写。
   * 可以创建内容变量。
   * 可以将相关内容与内容片段关联。
   * 可以使用版本控制/工作流。
   * 可以共享内容片段。
   * 可以集中管理翻译。

* **生成器和旅行管理器**

   * 从 AEM 内的预定义片段和具有创作功能的变量中选择。
   * 可以依赖始终保持最新的片段和关联内容，因为撰稿人和创意人员会在集中管理的片段和资产中进行更新。
   * 可以依赖为了相关性而进行管理的关联媒体内容。
   * 可以快速创建随机内容变量，同时仍然确保这些变量在片段中受到集中管理。

## 将内容片段添加到您的页面 {#adding-a-content-fragment-to-your-page}

1. 打开您的页面进行编辑。

1. 添加&#x200B;**内容片段**&#x200B;组件；通过&#x200B;**组件**&#x200B;浏览器或&#x200B;**插入新组件**。

1. 您可以：

   * 打开&#x200B;**资产**&#x200B;浏览器并筛选&#x200B;**内容片段**（默认为图像）。然后，将所需的片段拖到组件实例上。

   * 选择内容片段组件，然后从工具栏中选择&#x200B;**配置**。在对话框中，您可以打开选择对话框以浏览并选择所需的&#x200B;**内容片段**。
   >[!NOTE]
   >
   >备选方法是将特定的内容片段直接拖到页面上。这将自动创建关联的组件（内容片段）。

1. 最初，将显示&#x200B;**主**&#x200B;元素和&#x200B;**母版**（变量）中的内容。您可以根据需要[选择其他元素和/或变量](#selecting-the-element-or-variation)。

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >有关其他编辑功能的更多信息，另请参阅：
   >
   >
   >
   >    * [响应式布局](/help/sites-authoring/responsive-layout.md)
   >    * [编辑页面内容](/help/sites-authoring/editing-content.md)


### 选择元素或变量 {#selecting-the-element-or-variation}

打开片段的&#x200B;**配置**&#x200B;对话框以配置片段在当前页面上使用。该对话框取决于所使用的组件。

在相应的配置对话框中，您可以选择可用的参数，包括：

* **内容片段**

   指定要使用的片段。

* **显示模式**：

   * **单个文本元素**

   * **多元素**

* **元素**

   * 默认的&#x200B;**主元素**&#x200B;将始终可用。
   * 如果片段是通过适当的模板创建的，将有可选择的元素可用。

   >[!NOTE]
   >
   >有哪些元素可用取决于所使用的模板。

* **变量**

   * 默认主 **视图** 将始终可用。
   * 如果变量是为片段而创建的，将有可选择的变量可用。

* **段落**：指定要包含的段落范围：

   * **全部**
   * **范围**：例如 `1`、`3-5`、`9-*`

      * **将标题处理为它们自己的段落**

* **将标题处理为它们自己的段落**

### 到片段编辑器的快速连接 {#quick-connection-to-fragment-editor}

您可以打开片段源，以使用组件工具栏中的&#x200B;**编辑**&#x200B;图标编辑（资产）。这将允许您[编辑和管理内容片段](/help/assets/content-fragments/content-fragments.md)。

>[!CAUTION]
>
>通常情况下，编辑片段源将会影响引用该内容片段的所有页面。

### 添加中间内容 {#adding-in-between-content}

当指定的内容片段被添加到页面时，在片段的每个 HTML 段落之间（和顶部/底部）会有一个&#x200B;**将组件拖动到此处**&#x200B;占位符。

这允许您在片段内容[中间](/help/assets/content-fragments/content-fragments.md#inbetweencontent)的任何可用位置添加额外内容（即中间内容），而无需更改根片段。

对于中间内容，您可以：

* 从[组件浏览器](/help/sites-authoring/author-environment-tools.md#components-browser)添加组件。
* 从[资产浏览器](/help/sites-authoring/author-environment-tools.md#assets-browser)添加资产。
* 使用[关联内容](#using-associated-content)作为中间内容的源。

>[!CAUTION]
>
>中间内容是页面内容。它不会存储在内容片段中。

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>您还可以[在片段本身中插入可视资产（图像）](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)。
>
>在片段本身中插入的可视资产会附加到片段中的前一段落后面。这意味着无法在可视资产与前一段落之间放置中间内容。

>[!CAUTION]
>
>在将中间内容添加到页面上的内容片段之后，更改基础内容片段的结构（例如在内容片段编辑器中）可能会导致错误/意外的结果。
>
>在发生此问题时，中间内容会按原样保留：
>
>* 中间组件在片段流的组件序列中具有一个绝对位置。即使片段中段落的内容发生更改，此位置也不会变化。
>
>  
这可能使其看起来像是相对位置发生了更改一样，因为中间段落与它们旁边的（片段）段落之间没有上下文关系。
>* 除非两个段落结构产生冲突；在这种情况下，将不会显示中间内容（尽管它在内部依然存在）。

>



### 使用关联内容 {#using-associated-content}

如果您有与 [内容片段关联的](/help/assets/content-fragments/content-fragments-assoc-content.md)[内容](/help/assets/content-fragments/content-fragments.md) ，则这些资产将从侧面板（在将片段放置到内容页面后）中可用。 关联内容实际上是中间内容的 [特殊内容源](#adding-in-between-content)。

>[!NOTE]
>
>可以通过多种方法向片段和/或页面中添加[可视资产（例如图像）](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)。

>[!NOTE]
>
>如果您在一个页面中拥有多个内容片段，**关联内容**&#x200B;选项卡将显示适用于所有片段的资产。

在将具有关联内容的片段添加到页面之后，将会在侧面板中打开一个新的选项卡（**关联内容**）。

从此处，您可以将资产拖到所需的位置（可以是一个现有的组件，或是将在其中创建合适组件的所需位置）：

![cfm-6420-03](assets/cfm-6420-03.png)

### 插入到片段中的资产 {#assets-inserted-into-the-fragment}

如果已在片段本身中插入资产（例如图像），则页面编辑器中用于编辑这些资产的选项会受到限制。 <!-- Removed link as it was a 404 on helpx -->

例如，您可以对图像执行以下操作

* 裁剪、旋转或翻转图像。
* 添加标题或替换文本。
* 指定大小。
* 您还可以配置布局。

移动、复制和删除等其他更改必须在片段编辑器中进行。

### 发布 {#publishing}

片段需要发布，才能在您已发布的网页中使用。

* 可于[在资产控制台中创建片段](/help/assets/content-fragments/content-fragments.md#publishingandreferencingafragment)之后发布的片段。
* 如果在当前发布的页面中使用了&#x200B;*未发布的片段*，那么也可以在这一时候发布该片段。

