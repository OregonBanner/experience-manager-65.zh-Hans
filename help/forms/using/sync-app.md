---
title: 同步应用程序
seo-title: 同步应用程序
description: 将移动设备上的AEM Forms应用程序与AEM Forms服务器同步。
seo-description: 将移动设备上的AEM Forms应用程序与AEM Forms服务器同步。
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# 同步应用程序{#synchronizing-the-app}

## 同步应用程序{#synchronizing-the-app-1}

应用程序中的表单将从AEM Forms服务器下载。 表格将在“任务”和“Forms”选项卡下下载。 从表单创建的草稿将在“草稿”选项卡中下载，从任务创建的草稿将在“任务”选项卡中下载。 对于OSGi服务器上的独立表单，表单和草稿将分别下载到Forms和草稿选项卡中。

完成并提交表单后，如果该应用程序处于联机状态，则该表单会立即上传回AEM Forms服务器。 同步应用程序时，将从服务器获取表单。 但是，如果应用程序处于联机状态，草稿会立即与服务器同步。

默认情况下，当您与AEM Forms服务器联机时，每15分钟同步一次应用程序。 但是，您可以选择更改同步频率。 或者，您也可以随时手动同步应用程序。

**手动同步应用程序**

点按主屏幕右下角的同步按钮![sync-app](assets/sync-app.png)。

**更改同步频率**

1. 要转到“设置”屏幕，请点按主屏幕左上角的菜单按钮，然后点按&#x200B;**Settings**。
1. 在设置屏幕中，点按常规选项卡。

   ![“常规设置”窗口中的同步频率设置](assets/gen-settings-2.png)

1. 在同步频率选项中，点按同步频率右侧的值。
1. 在下拉列表中，选择新的同步频率。

### 技术规范{#technical-specifications}

* 将离线应用程序数据提交到AEM Forms服务器的主要逻辑包含在runtime/offline/util/offline.js中。
* 在.js中，对processOfflineSubmittedSavedTasks(...)函数的调用会将已保存/已提交的任务发送到服务器。 它还可处理同步过程中的任何错误或冲突。 如果提交任务失败，则应用程序上的任务将标记为失败。 此外，任务仍保留在发件箱中。
* syncSubmittedTask()和syncSavedTask()函数对各个任务执行操作。
* 当用户选择将脱机状态同步到服务器或通过后台线程自动同步后，任务列表组件会启动对processOfflineSubmittedSavedTasks()函数的调用。
