---
title: Live Copy 概述控制台
description: 了解Live Copy概述控制台的基础知识。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 30%

---

# Live Copy 概述控制台{#live-copy-overview-console}

此 **Live Copy概述** 使您能够：

* 跨站点查看/管理继承：

   * 查看Blueprint树和相应的Live Copy结构，以及它们的继承状态
   * 更改继承状态；例如，暂停、恢复
   * 查看Blueprint和Live Copy属性

* 执行转出操作

## 打开 Live Copy 概述 {#opening-the-live-copy-overview}

您可以从以下位置打开 Live Copy 概述：

* [Blueprint 页面（ Sites 控制台）的引用侧面板](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Blueprint 页面的属性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 打开Live Copy概述 — Blueprint页面的引用 {#opening-live-copy-overview-references-for-a-blueprint-page}

可以从&#x200B;**Sites**&#x200B;控制台的&#x200B;**引用**&#x200B;侧面板打开 **Live Copy 概述**：

1. 在&#x200B;**Sites**&#x200B;控制台中，[导航到您的 Blueprint 页面并将其选定。](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)
1. 打开 **[引用](/help/sites-authoring/basic-handling.md#references)** 面板并选择 **活动副本**.

   ![“引用”面板 — 活动副本](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >您还可以先打开引用，然后选择Blueprint。

1. 选择 **Live Copy概述** 用于显示和使用与所选Blueprint相关的所有活动副本的概述。
1. 使用&#x200B;**关闭**&#x200B;以退出，并返回到&#x200B;**Sites**&#x200B;控制台。

### 打开Live Copy概述 — Blueprint页面的属性 {#opening-live-copy-overview-properties-of-a-blueprint-page}

可以在查看 Blueprint 页面的属性时打开 **Live Copy 概述**：

1. 打开相应的 Blueprint 页面的&#x200B;**属性**。
1. 打开 **Blueprint** 选项卡 – **Live Copy 概述**&#x200B;选项会显示在顶部工具栏中：

   ![Blueprint选项卡 — Live Copy概述](assets/chlimage_1-360.png)

1. 选择 **Live Copy概述** 用于显示和使用与当前Blueprint相关的所有活动副本的概述。

   >[!NOTE]
   >
   >有关详细信息，另请参阅知识库文章 [Livecopy状态消息 — 最新/绿色/正在同步](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. 使用&#x200B;**关闭**&#x200B;以退出，并返回到&#x200B;**Sites**&#x200B;控制台。

## 使用 Live Copy 概述 {#using-the-live-copy-overview}

此 **Live Copy概述** 还可用于对Live Copy执行操作：

1. 打开 **Live Copy 概述**。
1. 选择所需的Blueprint或Live Copy页面 — 工具栏将更新以显示可用的操作。 此 [操作](/help/sites-administering/msm.md#terms-used) 是否可用取决于您是否选择 [Blueprint](#actions-for-a-blueprint-page) 或 [live copy](#actions-for-a-live-copy-page) 页面：

### 适用于 Blueprint 页面的操作 {#actions-for-a-blueprint-page}

在选择 Blueprint 页面时，以下操作可用：

![已选择Blueprint — 可用操作](assets/chlimage_1-361.png)

* 编辑

   * 打开Blueprint页面以进行编辑。

* [转出](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 执行转出以将更改从源推送到LiveCopy。

### 适用于 Live Copy 页面的操作 {#actions-for-a-live-copy-page}

在选择Live Copy页面时，以下操作可用：

![已选择Live Copy页面 — 可用操作](assets/chlimage_1-362.png)

* 编辑

   * 打开Live Copy页面以进行编辑。

* [关系状态](#relationship-status)

   * 查看有关状态和继承的信息。

* [同步](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 同步Live Copy以将更改从源拉入Live Copy。

* [重置](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * 重置Live Copy页面以删除所有继承取消，并使页面恢复到与源页面相同的状态。

* [暂停](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * 暂时停用Live Copy与其Blueprint页面之间的实时关系。

* [继续](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 恢复允许您恢复暂停的关系。

* [分离](/help/sites-administering/msm.md#detaching-a-live-copy)

   * 永久删除Live Copy与其Blueprint页面之间的实时关系。

## 关系状态 {#relationship-status}

此 **关系状态** console有两个选项卡，提供了一系列功能：

* [关系状态信息](#relationship-status-information)
* [Live Copy信息](#live-copy-information)

### 关系状态信息 {#relationship-status-information}

此选项卡提供有关Blueprint和Live Copy之间的关系状态的详细信息：

![关系状态信息](assets/chlimage_1-363.png)

### Live Copy信息 {#live-copy-information}

通过此选项卡，可查看和编辑Live Copy配置：

![Live Copy信息](assets/chlimage_1-364.png)
