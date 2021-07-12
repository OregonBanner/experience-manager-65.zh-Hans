---
title: 配置同步调度程序
seo-title: 配置同步调度程序
description: 了解如何迁移和同步资产、配置同步调度程序以及使用文件夹来排列资产。
seo-description: 了解如何迁移和同步资产、配置同步调度程序以及使用文件夹来排列资产。
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
role: Admin
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 配置同步调度程序 {#configuring-the-synchronization-scheduler}

默认情况下，同步计划程序每3分钟运行一次，以通过LiveCycle工作台11同步存储库中修改和更新的所有资产。 同步过程完成后，包含表单和资源的应用程序将在AEM Forms用户界面中可见。

## 更改同步调度程序的间隔 {#change-interval-of-the-synchronization-scheduler}

执行以下步骤以更改同步调度程序的间隔：

1. 登录到AEM Configuration Manager。 配置管理器的URL是`https://'[server]:[port]'/lc/system/console/configMgr`

1. 找到并打开&#x200B;**FormsManagerConfiguration**&#x200B;包。

1. 为&#x200B;**同步调度程序频率**&#x200B;选项指定新值。

   频率的单位是分钟。 例如，要将调度程序配置为每60分钟运行一次，请指定60。

## 同步资产 {#synchronizing-assets}

您可以使用&#x200B;**从存储库同步资产**&#x200B;选项来手动同步资产。 请执行以下步骤以手动同步资产：

1. 登录AEM Forms。 默认URL为`https://'[server]:[port]'/lc/aem/forms/`。

   ![AEM Forms用户界面](assets/aem_forms_ui.png)

   **图：** *AEM Forms用户界面*

1. 单击工具栏中的![aem6forms_sync](assets/aem6forms_sync.png)图标。 如果您在最后配置的路径上没有任何资产，则会出现如下所示的对话框。 单击&#x200B;**启动**&#x200B;以启动同步。

   ![“同步”对话框](assets/migrate-and-syncronize.png)

   **图：** *“同步”对话框*

## 同步错误疑难解答 {#troubleshooting-synchronization-error}

您可以在工作流设计器(LiveCycle工作台)中创建新应用程序。

如果新创建的应用程序和位于/content/dam/formsanddocuments的文件夹具有相同的名称，则根级别上已存在与此应用程序同名的资产，出现错误“*。*“ ”。

要解决冲突，请重命名应用程序，然后手动同步资产。

![“资产同步”对话框中的冲突](assets/sync-conflict.png)

**图：** *“资产同步”对话框中的冲突*
