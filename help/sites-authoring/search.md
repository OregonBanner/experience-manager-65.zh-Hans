---
title: 搜索
seo-title: 搜索
description: 使用完备的搜索功能更快速地查找您的内容
seo-description: 使用完备的搜索功能更快速地查找您的内容
uuid: 21605b96-b467-4d01-9a64-9d0648d539f1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 4ec15013-f7ab-44d6-8053-ed28b14f95e2
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 96%

---


# 搜索{#searching}

AEM 的创作环境提供了多种内容搜索机制，具体取决于资源类型。

>[!NOTE]
>
>在创作环境以外，还有其他机制可用于进行搜索，例如 [Query Builder](/help/sites-developing/querybuilder-api.md) 和 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)。

## 关于搜索的基础知识 {#search-basics}

搜索在顶部工具栏中可用：

![](do-not-localize/chlimage_1-17.png)

使用搜索边栏可以：

* 搜索特定的关键字、路径或标记。
* 按照特定于资源的条件进行筛选，例如修改日期、页面状态和文件大小等。
* 定义和使用[保存的搜索](#saved-searches) - 均基于以上条件。

>[!NOTE]
>
>显示搜索边栏时，还可以使用热键 `/`（正斜杠）调用搜索。

## 搜索和筛选 {#search-and-filter}

要搜索和筛选您的资源，请执行以下操作：

1. 打开&#x200B;**搜索**（使用工具栏中的放大镜）并输入您的搜索词。将向您提供相关的建议，并且可供您选择：

   ![s-01](assets/s-01.png)

   默认情况下，搜索结果将被限制在您的当前位置（例如控制台和相关的资源类型）：

   ![screen_shot_2018-03-23at101445](assets/screen_shot_2018-03-23at101445.png)

1. 如果需要，您可以删除位置筛选器（选中要删除的筛选器上的 **X**），以在所有控制台/资源类型之间进行筛选。
1. 将会显示结果，并按控制台和相关的资源类型进行分组。

   您可以选择一种特定的资源（用于未来操作），或通过选择所需的资源类型向下展开；例如&#x200B;**查看全部站点**：

   ![screen-shot_2019-03-05at101900](assets/screen-shot_2019-03-05at101900.png)

1. 如果您需要进一步向下展开，请选择“边栏”符号（左上方）以打开侧面板&#x200B;**筛选器和选项**。

   ![](do-not-localize/screen_shot_2018-03-23at101542.png)

   根据资源类型，搜索将显示预定义的搜索/筛选条件选项。

   侧面板允许您选择以下内容：

   * 保存的搜索
   * 搜索目录
   * 标记
   * 搜索条件；例如修改日期、发布状态、LiveCopy 状态。

   >[!NOTE]
   >
   >搜索条件可能会视情况而异：
   >
   >
   >
   >    * 具体视您选择的资源类型而定；例如，资产和社区条件理所当然是专用的；
   >    * 您可以自定义[搜索表单](/help/sites-administering/search-forms.md)实例（对应于在 AEM 中的位置）。


   ![screen-shot_2019-03-05at102509](assets/screen-shot_2019-03-05at102509.png)

1. 您还可以添加其他搜索词：

   ![screen-shot_2019-03-05at102613](assets/screen-shot_2019-03-05at102613.png)

1. 使用 **X**（右上方）关闭&#x200B;**搜索**。

>[!NOTE]
>
>在搜索结果中选择某个项目时，搜索条件会持续保留。
>
>当您在搜索结果页面上选择某个项目时，如果使用浏览器后退按钮返回到搜索页面，则搜索条件仍将存在。

## 保存的搜索 {#saved-searches}

除了按照多方面条件进行搜索以外，您还可以保存特定的搜索配置以供日后检索和使用：

1. 定义搜索条件，然后选择&#x200B;**保存**。

   ![screen-shot_2019-03-05at102613-1](assets/screen-shot_2019-03-05at102613-1.png)

1. 指定名称，然后使用&#x200B;**保存**&#x200B;进行确认。

   ![screen-shot_2019-03-05at102725](assets/screen-shot_2019-03-05at102725.png)

1. 在下次访问搜索面板时，您可以从选择器中选择保存的搜索：

   ![screen-shot_2019-03-05at102927](assets/screen-shot_2019-03-05at102927.png)

1. 在保存之后，您可以执行以下操作：

   * 使用 **x**（针对保存的搜索的名称）以开始新的查询（保存的搜索本身将不会被删除）。
   * **编辑保存的搜索**，更改搜索条件，然后再次&#x200B;**保存**。

通过选择保存的搜索并单击搜索面板底部的&#x200B;**编辑保存的搜索**，可以修改保存的搜索。

![screen-shot_2019-03-05at103010](assets/screen-shot_2019-03-05at103010.png)
