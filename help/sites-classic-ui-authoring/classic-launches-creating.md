---
title: 创建启动项
description: 建立啟動項，以更新現有網頁的新版本，以供日後啟用。 建立Launch時，您可以指定標題和來源頁面。
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 8ab21067-c19a-4faa-8bf0-cd9f21f6df70
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 25%

---

# 创建启动项{#creating-launches}

建立啟動項，以更新現有網頁的新版本，以供日後啟用。 在创建启动项时，需要指定标题和源页面：

* 標題會顯示在 **Sidekick**，作者可從中存取縮圖，進而加以處理。
* 來源頁面的子頁面預設會包含在啟動中。 您可以視需要只使用來源頁面。
* 依預設， [即時副本](/help/sites-administering/msm.md) 當來源頁面變更時，會自動更新啟動頁面。 您可以指定建立靜態副本以防止自動變更。

（可选）您可以指定启 **动日期** （和时间）以定义何时提升和激活启动页面。 但是，启 **动日期仅与生产就绪标** 志结合使用(请 **参阅编辑启动配置**[](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration));要使动作实际自动发生，必须同时设置这两个操作。

## 建立啟動 {#creating-a-launch}

下列程式會建立啟動。

1. 開啟網站管理頁面([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))。
1. 按一下 **新增……** 則 **新增啟動項……**.
1. 在 **建立啟動項** 對話方塊中，指定下列屬性的值：

   * **啟動項標題**：啟動項的名稱。 此名稱對作者應有意義。
   * **來源頁面**：要建立啟動項的頁面路徑。 依預設，會包含所有子頁面。
   * **排除子頁面**：選取此選項可僅針對來源頁面而非子頁面建立啟動。 依預設，不會選取此選項。
   * **保持同步**：選取此選項，可在來源頁面變更時自動更新啟動頁面的內容。 這是透過將啟動設為 [即時副本](/help/sites-administering/msm.md).
   * **启动日期**：激活启动副本的日期和时间（取决于&#x200B;**生产就绪**&#x200B;标记；请参阅[启动项 – 事件的顺序](/help/sites-authoring/launches.md#launches-the-order-of-events)）。

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. 单击&#x200B;**创建**。

## 刪除啟動項 {#deleting-a-launch}

您也可以刪除啟動項。

1. 在 [啟動主控台](/help/sites-classic-ui-authoring/classic-launches.md)，選取所需的啟動。
1. 按一下 **刪除**  — 需要確認：

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >刪除巢狀啟動時，您應該先刪除較低層級。
