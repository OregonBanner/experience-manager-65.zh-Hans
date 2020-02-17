---
title: 处理页面版本
seo-title: 处理页面版本
description: 创建、比较和恢复页面版本
seo-description: 创建、比较和恢复页面版本
uuid: 29e049f0-532c-4e3b-b64f-5be88ee6b08c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1368347a-9b65-4cfc-87e1-62993dc627fd
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50

---


# 处理页面版本{#working-with-page-versions}

版本控制可创建页面在特定时间点的“快照”。使用版本控制，您可以执行下列操作：

* 创建页面的版本。
* 将页面恢复到之前的版本，例如，为了撤消您对页面所做的更改。
* 将页面的当前版本与之前版本进行比较，并突出显示文本和图像中的差异。

## 创建新版本 {#creating-a-new-version}

您可以通过以下方式创建某个版本的资源：

* [时间轴边栏](#creating-a-new-version-timeline)
* [创建](#creating-a-new-version-create-with-a-selected-resource)选项（在选择某资源时）

### 创建新版本 - 时间轴 {#creating-a-new-version-timeline}

1. 导航以显示要为其创建版本的页面。
1. 在[选择模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
1. 打开&#x200B;**时间轴**&#x200B;列。
1. 单击/点按评论字段旁边的箭头以显现以下选项：

   ![screen-shot_2019-03-05at112335](assets/screen-shot_2019-03-05at112335.png)

1. 选择&#x200B;**另存为版本**。
1. 根据需要输入&#x200B;**标签**&#x200B;和&#x200B;**评论**。

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. 通过&#x200B;**创建**&#x200B;确认新版本。

   时间轴中的信息将进行更新以指示该新版本。

### 创建新版本 - 通过选定的资源创建 {#creating-a-new-version-create-with-a-selected-resource}

1. 导航以显示要为其创建版本的页面。
1. 在[选择模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
1. 从工具栏中选择&#x200B;**创建**。
1. 此时将打开一个对话框。您可以根据需要输入&#x200B;**标签**&#x200B;和&#x200B;**评论**：

   ![screen_shot_2012-02-15at105050am](assets/screen_shot_2012-02-15at105050am.png)

1. 通过&#x200B;**创建**&#x200B;确认新版本。

   将会打开时间轴，并且其信息会更新以指示新版本。

## 还原到某个页面版本 {#reverting-to-a-page-version}

创建了版本之后，即可以根据需要还原到该版本。

>[!NOTE]
>
>恢复页面时，创建的版本将包含在新分支中。
>
>举例说明：

>1. 为任意页面创建版本。
>1. 初始的标签和版本节点名称将表示为 1.0、1.1、1.2，以此类推。
1. 恢复第一个版本；即 1.0。
1. 再次创建新版本。
1. 此时生成的标签和节点名称将表示为 1.0.0、1.0.1、1.0.2，以此类推。



还原到之前的版本：

1. 导航以显示要还原到之前版本的页面。
1. 在[选择模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
1. 打开“**时间轴**”列，然后选择“**显示全部**”或“**版本**”。将列出所选页面的所有版本。
1. 选择要还原到的版本。将显示可能的选项：

   ![screen-shot_2019-03-05at112505](assets/screen-shot_2019-03-05at112505.png)

1. 选择“**还原到此版本**”。将恢复到所选版本，并在时间轴中更新信息。

## 预览版本 {#previewing-a-version}

您可以预览特定版本：

1. 导航以显示要进行比较的页面。
1. 在[选择模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
1. 打开&#x200B;**时间轴**&#x200B;列，然后选择&#x200B;**显示全部**&#x200B;或&#x200B;**版本**。
1. 将列出页面版本。选择要预览的版本：

   ![screen-shot_2019-03-05at112505-1](assets/screen-shot_2019-03-05at112505-1.png)

1. 选择&#x200B;**预览**。该页面将显示在新选项卡中。

   >[!CAUTION]
   如果页面发生移动，将无法再对移动前制作的任何版本执行预览。
   * 如果您遇到问题，请检查页面的[时间轴](/help/sites-authoring/basic-handling.md#timeline)以查看页面是否已被移动。


## 将页面的某个版本与当前版本进行比较 {#comparing-a-version-with-current-page}

要将页面的之前版本与当前版本进行比较，请执行以下操作：

1. 导航以显示要进行比较的页面。
1. 在[选择模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)中选择页面。
1. 打开&#x200B;**时间轴**&#x200B;列，然后选择&#x200B;**显示全部**&#x200B;或&#x200B;**版本**。
1. 将列出页面版本。选择要进行比较的版本：

   ![screen-shot_2019-03-05at112505-2](assets/screen-shot_2019-03-05at112505-2.png)

1. 选择&#x200B;**与当前比较**。此时将打开[页面差异](/help/sites-authoring/page-diff.md)，并显示存在的差异。

## 时间扭曲 {#timewarp}

时间扭曲是一项功能，旨在模拟过去特定时间某个页面的&#x200B;*已发布*&#x200B;状态。

由于内容创建是一个持续的协作过程，时间扭曲的目的是允许作者随时间跟踪已发布的网站，以了解内容的更改情况。 此功能使用页面版本来确定发布环境的状态。

要执行此操作：

* 系统会查找在选定时间处于活动状态的页面版本。
* 这表示显示的版本是在“时间扭曲”中选择的时间点&#x200B;*之前*&#x200B;创建/激活的。
* 当导航到已删除的页面时，也会呈现该页面——只要该页面的旧版本仍在存储库中可用。
* 如果没有找到发布的版本，则时间扭曲会还原到该页面在创作环境中的当前状态（这是为了防止出现错误/404 页面，此页面将阻止您进行浏览）。

### 使用时间扭曲 {#using-timewarp}

时间扭曲是页面编辑器的一种[模式](/help/sites-authoring/author-environment-tools.md#page-modes)。要启动此模式，只需像切换任何其他模式一样切换此模式即可。

1. 为希望启动时间扭曲的页面启动编辑器，然后在模式选择中选择&#x200B;**时间扭曲**。

   ![wwpv-01](assets/wwpv-01.png)

1. 在出现的对话框中，设置目标日期和时间，然后单击或点按&#x200B;**设置日期**。如果未选择时间，则默认将使用当前时间。

   ![wwpv-02](assets/wwpv-02.png)

1. 将根据设置的日期显示该页面。时间扭曲模式通过窗口顶部的蓝色状态栏来指示。使用该状态栏中的链接可选择新的目标日期，或退出时间扭曲模式。

   ![wwpv-03](assets/wwpv-03.png)

### 时间扭曲限制 {#timewarp-limitations}

时间扭曲会尽力在选定的时间点重制页面。 但是，由于AEM中内容的连续创作非常复杂，这并不总是可能。 使用时间扭曲时，应牢记这些限制。

* **时间扭曲基于已发布的页面工作** -时间扭曲仅在您之前已发布页面时才会完全正常工作。 如果没有，时间扭曲将在创作环境显示当前页面。
* **时间扭曲使用页面版本** -如果您导航到已从存储库删除的页面，则如果该页面的旧版本仍在存储库中可用，则该页面将正确呈现。
* **删除的版本影响时间扭曲** -如果从存储库中删除版本，则时间扭曲无法显示正确的视图。

* **时间扭曲是只读的** -您无法编辑页面的旧版本。 旧版本仅供查看。如果要恢复旧版本，则必须使用[恢复](#reverting-to-a-page-version)功能手动恢复。

* **时间扭曲仅基于页面内容** -如果用于呈现网站的元素（如代码、css、资源／图像等）已发生更改，则视图将与其原来的样子不同，因为这些项目不在存储库中进行版本控制。

>[!CAUTION]
时间扭曲设计为一种工具，可帮助作者理解和创建其内容。 它不用作审计日志或用于法律目的。
