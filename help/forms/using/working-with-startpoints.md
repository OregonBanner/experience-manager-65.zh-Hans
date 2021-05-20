---
title: 使用起点
seo-title: 使用起点
description: 在Workbench中定义的移动设备中使用AEM Forms进程的步骤。
seo-description: 在Workbench中定义的移动设备中使用AEM Forms进程的步骤。
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 使用起点{#working-with-startpoints}

起始点会调用在Workbench中创建的进程。 它与表单相关联，表单提交时会调用该进程。

>[!NOTE]
>
>术语起点、开始过程和表单在指代此概念时可互换使用。

要从AEM Forms应用程序启动进程，您需要在进程中具有类型为&#x200B;**Workspace**&#x200B;的起点。 此外，您还需要为起点选择&#x200B;**[!UICONTROL 在移动设备工作区中可见]**&#x200B;选项。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**启动在Workbench中定义的流程**

1. 要查看AEM Forms应用程序中可用的起点，请转到[主屏幕](../../forms/using/home-screen.md)。
1. 默认情况下，在&#x200B;**[!UICONTROL Home]**&#x200B;屏幕上，将显示&#x200B;**[!UICONTROL 所有Forms]**&#x200B;列表。

   起始点与表单关联。 点按列表中关联的起始点表单以将其打开。

   将打开与起始点关联的表单。

1. 在&#x200B;**[!UICONTROL Startpoint]**&#x200B;窗体中输入详细信息。

   可以使用[attachment](../../forms/using/add-attachments.md)按钮向此任务添加注释。

1. 填写表单后，点按&#x200B;**[!UICONTROL Submit]**&#x200B;按钮。

如果应用程序处于脱机状态，则表单及其数据会保存在“发件箱”文件夹中。

如果应用程序处于联机状态，则该任务将与AEM Forms服务器同步，并分配给进程中指定的用户。

要处理任务列表中的任务，请参阅[打开任务](/help/forms/using/open-task.md)。
