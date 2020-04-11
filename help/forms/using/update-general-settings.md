---
title: 更新常规设置
seo-title: 更新常规设置
description: 更新AEM Forms应用程序设置（如“主页”屏幕）并获取“起点”和“附件”选项
seo-description: 更新AEM Forms应用程序设置（如“主页”屏幕）并获取“起点”和“附件”选项
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 更新常规设置{#updating-general-settings}

通过AEM Forms应用程序的常规设置，可以指定获取附件、脱机模式、登录屏幕、默认类别和自动保存频率等设置。

## 更新应用程序中的“常规”设置 {#working-with-the-form}

当您将应用程序与AEM Forms服务器同步时，所有表单和定义的任务都将下载到您的移动设备上。

现成的AEM Forms应用程序解决方案在同步应用程序时不会下载与每个表单关联的附件。

在“常规”选项卡中，更改下载附件、脱机模式、登录屏幕、自动保存和同步设置。 您可以更改应 [用程序的](../../forms/using/home-screen.md) “主页”屏幕。

**导览至“设置”屏幕上的“常规”选项卡**

1. 要转到“设置”屏幕，请点按“主页”屏幕左上角的“菜单”按钮，然后点按 **设置**。
1. 在设置屏幕中，点按常规选项卡。

   ![AEM Forms应用程序中的常规设置](assets/gen-settings-1.png)

   “常规设置”屏幕

   >[!NOTE]
   >
   >这些选项在不同的移动设备上的显示可能不同。

### 常规设置 {#general-settings}

您可以对应用程序的设置进行以下更改。

* **提取任务附件**:指定在将每个任务下载到您的应用程序时是否下载关联的附件。
* **脱机模式**:启用或禁用AEM Forms应用程序的脱机服务。 有关详 [细信息，请参阅在脱机模式下](/help/forms/using/work-offline-mode.md) 。
* **登陆屏幕**:为应用程序设置开始位[置(主屏幕](../../forms/using/home-screen.md))。
可用选项：

   * 表单
   * 任务
   * 收藏夹

* **默认类别**:允许您选择要在主屏幕中显示的表单类别。 选择“全部”后，您可以在主屏幕中看到所有表单。 类别会根据应用程序中加载的表单进行填充。 根据在AEM Forms服务器中指定的表单设置，在应用程序中提供表单。

* **自动保存频率**:设置移动应用程序在本地保 [存表单数据的频率](../../forms/using/autosave-data-app.md) 。
* **同步频率**:在联机模式下设置移 [动应用程序与](../../forms/using/sync-app.md) AEM Forms服务器同步的频率。
   **清除本地数据**:清除数据库，包括所有用户的设置和本地数据以及设备中的文件存储。

>[!NOTE]
>
>清除缓存会立即将您从应用程序中注销。
>
>但是，系统会提示您确认清除缓存操作。
