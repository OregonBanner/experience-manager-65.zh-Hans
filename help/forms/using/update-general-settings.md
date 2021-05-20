---
title: 更新常规设置
seo-title: 更新常规设置
description: 更新AEM Forms应用程序设置（如“主页”屏幕），并获取“起点和附件”选项
seo-description: 更新AEM Forms应用程序设置（如“主页”屏幕），并获取“起点和附件”选项
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---

# 更新常规设置{#updating-general-settings}

通过AEM Forms应用程序的常规设置，您可以指定设置，如获取附件、脱机模式、登陆屏幕、默认类别和自动保存频率。

## 更新应用程序{#working-with-the-form}中的“常规”设置

将应用程序与AEM Forms服务器同步后，所有表单和定义的任务都会下载到您的移动设备。

开箱即用的AEM Forms应用程序解决方案不会在同步应用程序时下载与每个表单关联的附件。

在“常规”选项卡中，更改下载附件、脱机模式、登陆屏幕、自动保存和同步设置。 您可以更改应用程序的[主屏幕](../../forms/using/home-screen.md)。

**导航到设置屏幕上的常规选项卡**

1. 要转到“设置”屏幕，请点按主屏幕左上角的“菜单”按钮，然后点按&#x200B;**Settings**。
1. 在设置屏幕中，点按常规选项卡。

   ![AEM Forms应用程序中的常规设置](assets/gen-settings-1.png)

   “常规设置”屏幕

   >[!NOTE]
   >
   >这些选项在不同移动设备上的显示方式可能不同。

### 常规设置 {#general-settings}

您可以对应用程序的设置进行以下更改。

* **获取任务附件**:指定在将每个任务下载到您的应用程序时是否下载关联的附件。
* **脱机模式**:启用或禁用AEM Forms应用程序的离线服务。有关详细信息，请参阅[在脱机模式下工作](/help/forms/using/work-offline-mode.md)。
* **登陆屏幕**:为应用程序设置开始位置([主屏幕](../../forms/using/home-screen.md))。可用选项：

   * 表单
   * 任务
   * 收藏夹

* **默认类别**:允许您选择要在主屏幕中显示的表单类别。选择“全部”后，您可以在主屏幕中看到所有表单。 类别是根据应用程序中加载的表单来填充的。 Forms基于AEM Forms服务器中指定的表单设置，在应用程序中可用。

* **自动保存频率**:要设置移动设备应用程序逐 [渐保存表单数据的](../../forms/using/autosave-data-app.md) 频率。
* **同步频率**:在联机模式下设置移动设 [备应用程](../../forms/using/sync-app.md) 序与AEM Forms服务器同步的频率。
   **清除本地数据**:清除数据库，包括设备中所有用户的设置和本地数据以及文件存储。

>[!NOTE]
>
>清除缓存会立即将您从应用程序中注销。
>
>但是，系统将提示您确认清除缓存操作。
