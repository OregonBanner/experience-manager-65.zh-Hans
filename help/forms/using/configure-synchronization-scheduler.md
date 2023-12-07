---
title: 配置同步计划程序
description: 了解如何迁移和同步资源、配置同步计划程序以及使用文件夹排列资源。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# 配置同步计划程序 {#configuring-the-synchronization-scheduler}

默认情况下，同步计划程序每3分钟运行一次，以同步通过LiveCycleWorkbench 11在存储库中修改和更新的所有资源。 同步过程完成后，包含表单和资源的应用程序将显示在AEM Forms用户界面中。

## 更改同步计划程序的时间间隔 {#change-interval-of-the-synchronization-scheduler}

执行以下步骤以更改同步计划程序的时间间隔：

1. 登录到AEM Configuration Manager。 配置管理器的URL为 `https://'[server]:[port]'/lc/system/console/configMgr`

1. 找到并打开 **FormsManager配置** 捆绑。

1. 指定新的值 **同步计划程序频率** 选项。

   频率单位为分钟。 例如，要将调度程序配置为每60分钟运行一次，请指定60。

## 同步资产 {#synchronizing-assets}

您可以使用 **从存储库同步资源** 用于手动同步资产的选项。 执行以下步骤可手动同步资源：

1. 登录到AEM Forms。 默认URL为 `https://'[server]:[port]'/lc/aem/forms/`.

   ![AEM Forms用户界面](assets/aem_forms_ui.png)

   **图：** *AEM Forms用户界面*

1. 单击 ![aem6forms_sync](assets/aem6forms_sync.png) 图标。 如果在最后配置的路径中没有任何资源，则显示对话框，如下所示。 单击 **开始** 以启动同步。

   ![“同步”对话框](assets/migrate-and-syncronize.png)

   **图：** *“同步”对话框*

## 同步错误疑难解答 {#troubleshooting-synchronization-error}

您可以在工作流设计器(LiveCycle工作台)中创建新的应用程序。

如果新创建的应用程序和位于/content/dam/formsanddocuments的文件夹具有相同的名称，则出现错误&#39;&#39;*根级别已存在与此应用程序同名的资产。*“”已记录。

要解决冲突，请重命名应用程序，然后手动同步资源。

![资源同步对话框中的冲突](assets/sync-conflict.png)

**图：** *资源同步对话框中的冲突*
