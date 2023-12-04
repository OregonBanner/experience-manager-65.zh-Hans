---
title: 更新常规设置
seo-title: Updating general settings
description: 更新AEM Forms应用程序设置（如主屏幕）并获取起点和附件选项
seo-description: Update AEM Forms app settings such as the Home screen and fetch Startpoints and attachments options
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# 更新常规设置{#updating-general-settings}

通过AEM Forms应用程序的常规设置，您可以指定获取附件、离线模式、登录屏幕、默认类别和自动保存频率等设置。

## 更新应用程序中的常规设置 {#working-with-the-form}

将应用程序与AEM Forms服务器同步时，所有表单和定义的任务都会下载到您的移动设备。

现成的AEM Forms应用程序解决方案在应用程序同步时不会下载与每个表单关联的附件。

在“常规”选项卡中，更改下载附件、脱机模式、登录屏幕、自动保存和同步设置。 您可以更改 [主屏幕](../../forms/using/home-screen.md) 应用程序的ID。

**导航到设置屏幕上的常规选项卡**

1. 要转到“设置”屏幕，请选择“主页”屏幕左上角的菜单按钮，然后选择“选择” **设置**.
1. 在“设置”屏幕中，选择“常规”选项卡。

   ![AEM Forms应用程序中的常规设置](assets/gen-settings-1.png)

   “常规设置”屏幕

   >[!NOTE]
   >
   >这些选项在不同的移动设备上可能显示得不同。

### 常规设置 {#general-settings}

您可以对应用程序的设置进行以下更改。

* **获取任务附件**：指定在将每个任务下载到应用程序时是否下载关联的附件。
* **脱机模式**：启用或禁用AEM Forms应用程序的离线服务。 请参阅 [在脱机模式下工作](/help/forms/using/work-offline-mode.md) 以了解详细信息。
* **登陆屏幕**：设置开始位置([主屏幕](../../forms/using/home-screen.md))。
可用选项：

   * Forms
   * 任务
   * 收藏夹

* **默认类别**：用于选择要在主屏幕中显示的表单类别。 选择全部时，您可以在主屏幕中看到所有表单。 系统会根据应用程序中加载的表单填充类别。 Forms在应用程序中可用，具体取决于在AEM Forms服务器中指定的表单设置。

* **自动保存频率**：设置 [移动应用程序保存表单数据](../../forms/using/autosave-data-app.md) 本地。
* **同步频率**：设置 [移动应用程序已同步](../../forms/using/sync-app.md) AEM Forms服务器处于在线模式。
  **清除本地数据**：清除数据库，包括来自设备的所有用户的设置和本地数据以及文件存储。

>[!NOTE]
>
>清除缓存将会立即将您从应用程序中注销。
>
>但是，系统将提示您确认清除缓存操作。
