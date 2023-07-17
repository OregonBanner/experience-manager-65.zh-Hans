---
title: 使用起点
description: 通过Workbench中定义的移动设备使用Adobe Experience Manager Forms进程的步骤。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
source-git-commit: 60924e7ee204e43a2ff833fbc394beca8db9c9d9
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 使用起点{#working-with-startpoints}

起点调用在Workbench中创建的进程。 它与表单相关联，该表单在提交表单时调用该流程。

>[!NOTE]
>
>在引用此概念时，术语起点、开始过程和形式可互换使用。

要从Adobe Experience Manager (AEM) Forms应用程序启动流程，您必须具有类型的起点 **工作区** 在您的流程中。 此外，您必须选择 **[!UICONTROL 在移动工作区中可见]** 起始点选项。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**要启动在Workbench中定义的流程，请执行以下操作**

1. 要查看AEM Forms应用程序中可用的起点，请转到 [主屏幕](../../forms/using/home-screen.md).
1. 在 **[!UICONTROL 主页]** 屏幕，默认情况下， **[!UICONTROL 所有Forms]** 将显示列表。

   起点与表单相关联。 点按列表中与表单关联的起点以将其打开。

   与起点关联的表单打开。

1. 请在以下位置输入详细信息 **[!UICONTROL 起点]** 表单。

   您可以使用将注释添加到此任务 [附件](../../forms/using/add-attachments.md) 按钮。

1. 填写表单后，点按 **[!UICONTROL 提交]** 按钮。

如果应用程序处于离线状态，则表单及其数据将保存在“发件箱”文件夹中。

如果应用程序处于联机状态，则任务将与AEM Forms Server同步，并分配给进程中指定的用户。

要使用任务列表中的任务，请参阅 [打开任务](/help/forms/using/open-task.md).
