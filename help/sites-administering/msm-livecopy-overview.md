---
title: Live Copy概述控制台
seo-title: Live Copy概述控制台
description: 了解Live Copy概述控制台的基础知识。
seo-description: 了解Live Copy概述控制台的基础知识。
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 2%

---


# Live Copy概述控制台{#live-copy-overview-console}

**Live Copy概述**&#x200B;允许您：

* 视图/管理站点间的继承：

   * 视图Blueprint树和相应的Live Copy结构及其继承状态
   * 更改继承状态；例如，暂停、恢复
   * 视图Blueprint和Live Copy属性

* 执行转出操作

## 打开Live Copy概述{#opening-the-live-copy-overview}

您可以从以下位置打开Live Copy概述：

* [蓝图页面的引用侧面板（站点控制台）](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Blueprint页面的属性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 打开Live Copy概述- Blueprint页面{#opening-live-copy-overview-references-for-a-blueprint-page}的引用

可以从&#x200B;**站点**&#x200B;控制台的&#x200B;**引用**&#x200B;侧面板打开&#x200B;**Live Copy概述**:

1. 在&#x200B;**站点**&#x200B;控制台中，[导航到您的Blueprint页面并选择它](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。
1. 打开&#x200B;**[引用](/help/sites-authoring/basic-handling.md#references)**&#x200B;面板并选择&#x200B;**Live Copy**。

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >您还可以先打开引用，然后选择蓝图。

1. 选择&#x200B;**Live Copy概述**&#x200B;以显示和使用与所选蓝图相关的所有Live Copy的概述。
1. 使用&#x200B;**关闭**&#x200B;退出并返回到&#x200B;**站点**&#x200B;控制台。

### 打开Live Copy概述- Blueprint页面{#opening-live-copy-overview-properties-of-a-blueprint-page}的属性

在查看Blueprint页面的属性时，可以打开&#x200B;**Live Copy概述**:

1. 打开相应蓝图页面的&#x200B;**属性**。
1. 打开&#x200B;**Blueprint**&#x200B;选项卡——顶部工具栏中将显示&#x200B;**Live Copy概述**&#x200B;选项：

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. 选择&#x200B;**Live Copy概述**&#x200B;以显示和使用与当前蓝图相关的所有Live Copy的概述。

   >[!NOTE]
   >
   >有关详细信息，另请参阅知识库文章[Live Copy状态消息——最新／绿色／同步](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html)。

1. 使用&#x200B;**关闭**&#x200B;退出并返回到&#x200B;**站点**&#x200B;控制台。

## 使用Live Copy概述{#using-the-live-copy-overview}

**Live Copy概述**&#x200B;还可用于对Live Copy执行操作：

1. 打开&#x200B;**Live Copy概述**。
1. 选择所需的Blueprint或Live Copy页面——工具栏将更新以显示可用的操作。 可用的[操作](/help/sites-administering/msm.md#terms-used)取决于您选择的是[blueprint](#actions-for-a-blueprint-page)还是[Live Copy](#actions-for-a-live-copy-page)页面：

### Blueprint页面{#actions-for-a-blueprint-page}的操作

选择Blueprint页面时，可执行以下操作：

![chlimage_1-361](assets/chlimage_1-361.png)

* 编辑

   * 打开Blueprint页面进行编辑。

* [转出](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 执行转出以将更改从源推送到Live Copy。

### Live Copy页面{#actions-for-a-live-copy-page}的操作

选择Live Copy页面时，可以执行以下操作：

![chlimage_1-362](assets/chlimage_1-362.png)

* 编辑

   * 打开Live Copy页面进行编辑。

* [关系状态](#relationship-status)

   * 视图有关状态和继承的信息。

* [同步](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 同步Live Copy以从源将更改拉入Live Copy。

* [重置](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * 重置Live Copy页面可删除所有继承取消，并将页面恢复为与源页面相同的状态。

* [暂停](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * 临时停用Live Copy与其Blueprint页面之间的Live关系。

* [继续](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 恢复允许您恢复已暂停的关系。

* [分离](/help/sites-administering/msm.md#detaching-a-live-copy)

   * 永久删除Live Copy与其Blueprint页面之间的Live关系。

## 关系状态 {#relationship-status}

**关系状态**&#x200B;控制台具有两个选项卡，提供一系列功能：

* [关系状态信息](#relationship-status-information)
* [Live Copy信息](#live-copy-information)

### 关系状态信息{#relationship-status-information}

此选项卡提供了有关Blueprint和Live Copy之间关系状态的详细信息：

![chlimage_1-363](assets/chlimage_1-363.png)

### Live Copy信息{#live-copy-information}

此选项卡允许您视图和编辑Live Copy配置：

![chlimage_1-364](assets/chlimage_1-364.png)

