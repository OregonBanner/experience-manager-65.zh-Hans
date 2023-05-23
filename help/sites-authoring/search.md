---
title: 完整搜尋
description: 透過全面搜尋，更快找到您的內容。
uuid: 21605b96-b467-4d01-9a64-9d0648d539f1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 4ec15013-f7ab-44d6-8053-ed28b14f95e2
docset: aem65
exl-id: dd65b308-c449-4f64-9f46-0797b922910f
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 52%

---

# 搜索{#searching}

AEM 的创作环境提供了多种内容搜索机制，具体取决于资源类型。

>[!NOTE]
>
>在製作環境外，也可使用其他機制進行搜尋，例如 [查詢產生器](/help/sites-developing/querybuilder-api.md) 和 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## 搜索基础知识 {#search-basics}

可从顶部工具栏中使用搜索功能：

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

1. 開啟 **搜尋** （使用工具列中的放大鏡）並輸入搜尋字詞。 將會提出建議並可加以選取：

   ![s-01](assets/s-01.png)

   默认情况下，搜索结果将被限制在您的当前位置（例如控制台和相关的资源类型）：

   ![screen_shot_2018-03-23at101445](assets/screen_shot_2018-03-23at101445.png)

1. 如果需要，您可以删除位置过滤器（选中要删除的过滤器上的 **X**），以在所有控制台/资源类型之间进行筛选。
1. 將顯示結果，並根據控制檯和相關資源型別分組。

   您可以选择一种特定的资源（用于未来操作），或通过选择所需的资源类型向下展开；例如&#x200B;**查看全部站点**：

   ![screen-shot_2019-03-05at101900](assets/screen-shot_2019-03-05at101900.png)

1. 如果您需要进一步向下展开，请选择“边栏”符号（左上方）以打开侧面板&#x200B;**过滤器和选项**。

   ![](do-not-localize/screen_shot_2018-03-23at101542.png)

   根據資源型別，搜尋將顯示預先定義的搜尋/篩選條件選擇。

   側面板可讓您選取：

   * 保存的搜索
   * 搜尋目錄
   * 标记
   * 搜尋條件；例如，修改日期、發佈狀態、即時副本狀態。

   >[!NOTE]
   >
   >搜尋條件可能有所不同：
   >
   >
   >
   >    * 根據您選取的資源型別，例如Assets和Communities條件具有專業化是可以理解的。
   >    * 您的執行個體為 [搜尋Forms](/help/sites-administering/search-forms.md) 可自訂(適用於AEM內的位置)。


   ![screen-shot_2019-03-05at102509](assets/screen-shot_2019-03-05at102509.png)

1. 您也可以新增其他搜尋詞：

   ![screen-shot_2019-03-05at102613](assets/screen-shot_2019-03-05at102613.png)

1. 使用 **X**（右上方）关闭&#x200B;**搜索**。

>[!NOTE]
>
>在搜尋結果中選取專案時，搜尋條件會持續存在。
>
>当您在搜索结果页面上选择某个项目时，如果使用浏览器后退按钮返回到搜索页面，则搜索条件仍将存在。

## 保存的搜索 {#saved-searches}

除了依各種Facet進行搜尋外，您也可以儲存特定的搜尋設定以供擷取，並用於後續階段：

1. 定義搜尋條件並選取 **儲存**.

   ![screen-shot_2019-03-05at102613-1](assets/screen-shot_2019-03-05at102613-1.png)

1. 指定名称，然后使用&#x200B;**保存**&#x200B;进行确认。

   ![screen-shot_2019-03-05at102725](assets/screen-shot_2019-03-05at102725.png)

1. 在下次访问搜索面板时，您可以从选择器中选择保存的搜索：

   ![screen-shot_2019-03-05at102927](assets/screen-shot_2019-03-05at102927.png)

1. 儲存後，您可以：

   * 使用 **x** （針對已儲存搜尋的名稱）以開始新查詢（不會刪除已儲存搜尋本身）。
   * **編輯已儲存的搜尋**，變更搜尋條件，然後 **儲存** 再來一次。

通过选择保存的搜索并单击搜索面板底部的&#x200B;**编辑保存的搜索**，可以修改保存的搜索。

![screen-shot_2019-03-05at103010](assets/screen-shot_2019-03-05at103010.png)
