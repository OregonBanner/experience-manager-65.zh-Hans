---
title: 更新常规设置
seo-title: 更新常规设置
description: 更新AEM Forms应用程序设置（如“主页”屏幕）并获取“起始点”和“附件”选项
seo-description: 更新AEM Forms应用程序设置（如“主页”屏幕）并获取“起始点”和“附件”选项
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---


# 更新常规设置{#updating-general-settings}

通过AEM Forms应用程序的常规设置，可以指定提取附件、脱机模式、登录屏幕、默认类别和自动保存频率等设置。

## 更新应用程序{#working-with-the-form}中的“常规”设置

当您将应用程序与AEM Forms服务器同步时，所有表单和定义的任务均下载到您的移动设备上。

现成的AEM Forms应用程序解决方案在同步应用程序时不会下载与每个表单关联的附件。

在“常规”选项卡中，更改下载附件、脱机模式、登录屏幕、自动保存和同步设置。 您可以更改应用程序的[主屏幕](../../forms/using/home-screen.md)。

**导航到“设置”屏幕上的“常规”选项卡**

1. 要转到“设置”屏幕，请点按“主页”屏幕左上角的“菜单”按钮，然后点按&#x200B;**设置**。
1. 在设置屏幕中，点按常规选项卡。

   ![AEM Forms应用程序中的常规设置](assets/gen-settings-1.png)

   “常规设置”屏幕

   >[!NOTE]
   >
   >这些选项在不同移动设备上的显示方式可能不同。

### 常规设置 {#general-settings}

您可以对应用程序的设置进行以下更改。

* **提取任务附件**:指定在将每个任务下载到您的应用程序时是否下载关联的附件。
* **脱机模式**:为AEM Forms应用程序启用或禁用脱机服务。有关详细信息，请参阅[在脱机模式下工作](/help/forms/using/work-offline-mode.md)。
* **登录屏幕**:为应用程序设置开始[位置](../../forms/using/home-screen.md)（主屏幕）。可用选项：

   * 表单
   * 任务
   * 收藏夹

* **默认类别**:允许您选择要在主屏幕中显示的表单类别。选择“全部”后，您可以在主屏幕中看到所有表单。 类别根据应用程序中加载的表单进行填充。 Forms在应用程序中根据AEM Forms服务器中指定的表单设置可用。

* **自动保存频率**:设置移动应用程序以数据 [方式保存表单的](../../forms/using/autosave-data-app.md) 频率。
* **同步频率**:设置在线模式下移动 [应用程](../../forms/using/sync-app.md) 序与AEM Forms服务器同步的频率。
   **清除本地数据**:清除存储库，包括所有用户的设置和本地数据以及设备中的文件数据。

>[!NOTE]
>
>清除缓存将立即将您从应用程序中注销。
>
>但是，系统将提示您确认清除缓存操作。
