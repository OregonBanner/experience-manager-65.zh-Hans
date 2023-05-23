---
title: 使用Launches開發未來版本的內容
description: Launch可讓您有效率地開發未來版本的內容。 它們可讓您進行變更，以備將來發佈，同時維護您目前的頁面。
uuid: 4bbd9865-735d-4232-b69c-b64193ac5d83
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e145afd8-7391-47aa-b389-16fb303749d0
docset: aem65
exl-id: b25d3f8e-5687-49ab-95e1-19ec75c87f6e
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 27%

---

# 启动项{#launches}

啟動可讓您有效率地開發未來版本的內容。

建立啟動後，您就可以進行變更，以備將來發佈（同時保留目前的頁面）。 編輯和更新啟動頁面後，您會將啟動頁面升級回來源，然後啟動來源頁面（頂層）。 提升會將啟動內容復寫回來源頁面，並且可以手動或自動完成（取決於建立和編輯啟動時設定的欄位）。

例如，您線上商店的季節性產品頁面會每季更新，讓精選產品與目前季節一致。 若要準備下一次每季更新，您可以建立適當網頁的啟動。 整個季度，啟動副本中累積了以下變更：

* 因正常維護任務而發生的來源頁面變更。 這些變更會自動在啟動頁面中複製。
* 直接在啟動頁面上執行的編輯，為下一季做準備。

当下一季度到来时，您需要提升启动页面，以便发布源页面（包含更新的内容）。您可以提升所有页面，也可以仅提升已修改的页面。

啟動也可以是：

* 為多個根分支建立。 雖然您可以建立整個網站的啟動（並在那裡進行變更），但這並不實際，因為需要複製整個網站。 當涉及數百甚至數千個頁面時，複製動作和之後促銷任務所需的比較都會影響系統需求和效能。
* 巢狀（啟動內的啟動），可讓您從現有的啟動建立啟動，讓作者能夠利用已進行的變更，而不必針對每個啟動多次進行相同的變更。

本節說明如何建立、編輯和提升（以及如有需要） [刪除](/help/sites-authoring/launches-creating.md#deleting-a-launch))從Sites主控台內啟動頁面，或 [啟動主控台](#the-launches-console)：

* [创建启动项](/help/sites-authoring/launches-creating.md)
* [编辑启动项](/help/sites-authoring/launches-editing.md)
* [提升启动项](/help/sites-authoring/launches-promoting.md)

## 啟動 — 事件順序 {#launches-the-order-of-events}

啟動可讓您有效地開發內容，以供日後發行的一或多個已啟用的網頁使用。

啟動可讓您：

* 创建源页面的副本：

   * 副本是您的启动项。
   * 顶级源页面称为&#x200B;**生产**。

      * 來源頁面可從多個（單獨的）分支取得。

   ![chlimage_1-111](assets/chlimage_1-111.png)

* 编辑启动项配置：

   * 新增或移除啟動項的頁面和/或分支。
   * 编辑启动项属性；例如&#x200B;**标题**、**启动日期**、**生产就绪**&#x200B;标记。

* 您可以手動或自動升級和發佈內容：

   * 手动:

      * 將啟動內容提升回 **Target** （來源頁面）。
      * 從來源發佈內容（升級回原版後）頁面。
      * 升級所有頁面，或僅升級已修改的頁面。
   * 自动 – 这涉及以下各项：

      * **启动**（**起始**）**日期**&#x200B;字段：可在创建或编辑启动项时设置此字段。

      * 此 **生產就緒** 標幟：這只能在編輯啟動時設定。
      * 如果 **生產就緒** 旗標已設定，啟動會自動升級至指定上的生產頁面 **Launch**(**即時**) **日期**. 提升后，生产页面会自动发布。\
         如果未设置日期，该标记将不起作用。


* 并行更新源页面和启动页面：

   * 对源页面所做的更改会自动体现在启动副本中（如果进行了继承设置，即设置为 Live Copy）。
   * 可以在不中断这些自动更新或源页面的情况下对启动副本进行更改。

   ![chlimage_1-112](assets/chlimage_1-112.png)

* [建立巢狀啟動](/help/sites-authoring/launches-creating.md#creating-a-nested-launch)  — 啟動中的啟動：

   * 來源是現有的啟動。
   * 您可以 [提升巢狀啟動](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch) 至任何目標；這可以是父啟動或頂層來源頁面（生產）。

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!CAUTION]
   >
   >删除启动项时，将会删除该启动项本身及其所有下级嵌套启动项。

>[!NOTE]
>
>要创建和编辑启动项，需要拥有 `/content/launches` 的访问权限 – 与默认组 `content-authors` 的权限相同。
>
>如果您遇到任何问题，请联系您的系统管理员。

>[!CAUTION]
>
>不支援在Launch頁面上重新排序元件。
>
>頁面升級時，將會反映任何內容變更，但元件位置不會變更。


### 啟動主控台 {#the-launches-console}

「啟動」主控台提供啟動的總覽，並可讓您對列出的啟動執行動作。 可以通过以下方式访问该控制台：

* **工具**&#x200B;控制台：**工具**、**站点**、**启动项**。

* 或直接使用 [https://localhost:4502/libs/launches/content/launches.html](https://localhost:4502/libs/launches/content/launches.html)

## 在參照（網站主控台）中啟動 {#launches-in-references-sites-console}

1. 在 **網站** 主控台，導覽至啟動項的來源。
1. 開啟 **引用** 欄並選取來源頁面。
1. 選取 **啟動**，則會列出現有的啟動項：

   ![screen-shot_2019-03-05at121901-1](assets/screen-shot_2019-03-05at121901-1.png)

1. 点按/单击相应的启动项，此时将显示可执行的操作列表：

   ![screen-shot_2019-03-05at121952-1](assets/screen-shot_2019-03-05at121952-1.png)
