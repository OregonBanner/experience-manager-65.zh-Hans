---
title: Live Copy 概述控制台
seo-title: Live Copy Overview Console
description: 瞭解Live Copy概述控制檯的基本概念。
seo-description: Learn about the basics of the Live Copy Overview Console.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 28%

---

# Live Copy 概述控制台{#live-copy-overview-console}

此 **即時副本概觀** 可讓您：

* 檢視/管理網站間的繼承：

   * 檢視Blueprint樹狀結構和對應的即時副本結構，以及其繼承狀態
   * 變更繼承狀態；例如，暫停、繼續
   * 檢視Blueprint和即時副本屬性

* 執行轉出動作

## 打开 Live Copy 概述 {#opening-the-live-copy-overview}

您可以从以下位置打开 Live Copy 概述：

* [Blueprint 页面（站点控制台）的引用侧面板](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Blueprint 页面的属性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 開啟即時副本總覽 — Blueprint頁面的引用 {#opening-live-copy-overview-references-for-a-blueprint-page}

可以从&#x200B;**站点**&#x200B;控制台的&#x200B;**引用**&#x200B;侧面板打开 **Live Copy 概述**：

1. 在 **網站** 主控台， [導覽至您的Blueprint頁面並加以選取](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. 開啟 **[引用](/help/sites-authoring/basic-handling.md#references)** 面板並選取 **即時副本**.

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >您也可以先開啟參照，然後選取Blueprint。

1. 選取 **即時副本概觀** 以顯示及使用與所選Blueprint相關之所有即時副本的概觀。
1. 使用&#x200B;**关闭**&#x200B;以退出，并返回到&#x200B;**站点**&#x200B;控制台。

### 開啟即時副本概觀 — Blueprint頁面的屬性 {#opening-live-copy-overview-properties-of-a-blueprint-page}

可以在查看 Blueprint 页面的属性时打开 **Live Copy 概述**：

1. 打开相应的 Blueprint 页面的&#x200B;**属性**。
1. 打开 **Blueprint** 选项卡 – **Live Copy 概述**&#x200B;选项将显示在顶部工具栏中：

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. 選取 **即時副本概觀** 以顯示和使用與目前Blueprint相關之所有即時副本的概觀。

   >[!NOTE]
   >
   >如需詳細資訊，另請參閱知識庫文章 [即時副本狀態訊息 — 最新/綠色/同步中](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. 使用&#x200B;**关闭**&#x200B;以退出，并返回到&#x200B;**站点**&#x200B;控制台。

## 使用 Live Copy 概述 {#using-the-live-copy-overview}

此 **即時副本概觀** 也可用於對即時副本執行動作：

1. 打开 **Live Copy 概述**。
1. 選取所需的Blueprint或即時副本頁面 — 工具列將更新以顯示可用的操作。 此 [動作](/help/sites-administering/msm.md#terms-used) 是否可用取決於您是否選取 [Blueprint](#actions-for-a-blueprint-page) 或 [即時副本](#actions-for-a-live-copy-page) 頁面：

### 适用于 Blueprint 页面的操作 {#actions-for-a-blueprint-page}

在选择 Blueprint 页面时，以下操作可用：

![chlimage_1-361](assets/chlimage_1-361.png)

* 编辑

   * 開啟Blueprint頁面以進行編輯。

* [转出](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 執行轉出以將變更從來源推送到LiveCopy。

### 适用于 Live Copy 页面的操作 {#actions-for-a-live-copy-page}

當您選取即時副本頁面時，以下動作可供使用：

![chlimage_1-362](assets/chlimage_1-362.png)

* 编辑

   * 開啟即時副本頁面以進行編輯。

* [关系状态](#relationship-status)

   * 檢視狀態和繼承的相關資訊。

* [同步](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 同步即時副本，以將變更從來源提取到即時副本。

* [重置](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * 重設即時副本頁面以移除所有繼承取消，並讓頁面恢復到與來源頁面相同的狀態。

* [暂停](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * 暫時停用即時副本與其Blueprint頁面之間的即時關係。

* [继续](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 「繼續」可讓您恢復暫停的關係。

* [分离](/help/sites-administering/msm.md#detaching-a-live-copy)

   * 永久移除即時副本與其Blueprint頁面之間的即時關係。

## 关系状态 {#relationship-status}

此 **關係狀態** console有兩個標籤，提供一系列功能：

* [關係狀態資訊](#relationship-status-information)
* [即時副本資訊](#live-copy-information)

### 關係狀態資訊 {#relationship-status-information}

此標籤提供有關Blueprint與即時副本之間關係狀態的詳細資訊：

![chlimage_1-363](assets/chlimage_1-363.png)

### 即時副本資訊 {#live-copy-information}

此索引標籤可讓您檢視和編輯即時副本設定：

![chlimage_1-364](assets/chlimage_1-364.png)
