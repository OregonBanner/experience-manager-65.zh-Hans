---
title: Live copy概述控制台
seo-title: Live copy概述控制台
description: 了解Live copy概述控制台的基础知识。
seo-description: 了解Live copy概述控制台的基础知识。
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Live copy概述控制台{#live-copy-overview-console}

Live **Copy概述使您** 能够：

* 查看／管理站点间的继承：

   * 查看Blueprint树和相应的Live Copy结构，以及它们的继承状态
   * 更改继承状态；例如，暂停，继续
   * 查看Blueprint和Live copy属性

* 执行转出操作

## 打开Live copy概述 {#opening-the-live-copy-overview}

您可以从以下位置打开Live copy概述：

* [Blueprint页面的引用侧面板（站点控制台）](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Blueprint页面的属性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 打开Live copy概述- Blueprint页面的引用 {#opening-live-copy-overview-references-for-a-blueprint-page}

可 **以从站点控制台的“** 引用 **** ”侧面板打开Live copy概 **述** :

1. 在“站 **点** ”控制台 [中，导航到您的Blueprint页面并将其选中](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. Open the **[References](/help/sites-authoring/basic-handling.md#references)**panel and select **Live Copies**.

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >您还可以先打开引用，然后选择蓝图。

1. 选 **择Live copy概述** ，以显示和使用与选定蓝图相关的所有Live Copy的概述。
1. 使用 **关闭** ，退出并返回站点控 **制台** 。

### 打开Live copy概述- Blueprint页面的属性 {#opening-live-copy-overview-properties-of-a-blueprint-page}

在查 **看Blueprint页面的属性时** ，可以打开Live copy概述：

1. 为相 **应的Blueprint页面** ，打开属性。
1. 打开 **Blueprint** 选项卡——顶部工 **具栏中将显示Live copy概述** :

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. 选 **择Live copy概述** ，以显示和使用与当前Blueprint相关的所有Live Copy的概述。

   >[!NOTE]
   >
   >有关详细信息，另请参阅知识库文章 [Live copy状态消息——最新／绿色／同步](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html)。

1. 使用 **关闭** ，退出并返回站点控 **制台** 。

## 使用Live copy概述 {#using-the-live-copy-overview}

Live **Copy概述** ，还可用于对Live copy执行以下操作：

1. Open the **Live Copy Overview**.
1. 选择所需的Blueprint或Live Copy页面——工具栏将更新以显示可用的操作。 可 [用的操作](/help/sites-administering/msm.md#terms-used) ，取决于您是选择Blueprint [还是](#actions-for-a-blueprint-page) Live Copy页 [](#actions-for-a-live-copy-page) :

### Blueprint页面的操作 {#actions-for-a-blueprint-page}

选择Blueprint页面时，可执行以下操作：

![chlimage_1-361](assets/chlimage_1-361.png)

* 编辑

   * 打开Blueprint页面进行编辑。

* [转出](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 执行转出以将更改从源推送到Live Copy。

### Live copy页面的操作 {#actions-for-a-live-copy-page}

选择Live copy页面时，可执行以下操作：

![chlimage_1-362](assets/chlimage_1-362.png)

* 编辑

   * 打开Live copy页面进行编辑。

* [关系状态](#relationship-status)

   * 查看有关状态和继承的信息。

* [同步](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 同步Live Copy以将更改从源拉到Live Copy。

* [重置](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * 重置Live copy页面可删除所有继承取消，并将页面返回到与源页面相同的状态。

* [暂停](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * 临时停用Live copy与其Blueprint页面之间的Live关系。

* [继续](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 恢复允许您恢复已暂停的关系。

* [分离](/help/sites-administering/msm.md#detaching-a-live-copy)

   * 永久删除Live copy与其Blueprint页面之间的Live关系。

## 关系状态 {#relationship-status}

“关 **系状态** ”控制台有两个选项卡，提供一系列功能：

* [关系状态信息](#relationship-status-information)
* [Live copy信息](#live-copy-information)

### 关系状态信息 {#relationship-status-information}

此选项卡提供了有关Blueprint和Live copy之间关系状态的详细信息：

![chlimage_1-363](assets/chlimage_1-363.png)

### Live copy信息 {#live-copy-information}

此选项卡允许您查看和编辑Live copy配置：

![chlimage_1-364](assets/chlimage_1-364.png)

