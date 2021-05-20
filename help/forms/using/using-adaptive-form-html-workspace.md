---
title: 在HTML工作区中使用自适应表单
seo-title: 在HTML工作区中使用自适应表单
description: 在HTML工作区中使用自适应表单
seo-description: 在HTML工作区中使用自适应表单
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# 在HTML工作区中使用自适应表单{#using-an-adaptive-form-in-html-workspace}

AEM Forms on JEE提供了在HTML工作区中使用自适应表单的功能。

由于您可以在流程设计期间选择XDP，因此添加了从现有自适应表单AEM存储库进行浏览的功能。 该功能使流程设计人员能够在起始点和任务中配置自适应表单。

## 流程设计体验{#process-design-experience}

执行以下操作，以便在流程设计中使用自适应表单：

* 在分配任务和开始点中，在将表单资产分配给任务时，您可以浏览到CRX存储库中的自适应表单资产。
* 在“分配任务/起始点工作台”属性工作表中，您可以隐藏自适应表单的顶级/全局工具栏。
* 您可以在自适应表单中将新的操作配置文件用于渲染和提交操作。

### LiveCycle应用程序导出和导入{#livecycle-application-export-and-import}

由于自适应表单位于AEM存储库中，因此LiveCycle应用程序导出仅包含所用自适应表单的引用。 因此，LiveCycle应用程序的导出和导入是一个分两步的过程。 LiveCycle应用程序包括进程定义等。 包含自适应表单的单独包将从AEM导出为ZIP文件。 导入时，LiveCycle应用程序会通过Workbench导入，自适应表单会通过AEM导入。

## HTML工作区{#user-experience-of-adaptive-form-in-html-workspace}中自适应表单的用户体验

HTML工作区除了提供用于移动表单的控件之外，还提供了一些特定于表单的自适应控件。 当用户打开任务或开始点时，用户可以在HTML工作区中添加附件、保存、签名、提交和导航自适应表单。 具体如下：

1. 要附加文件，请使用任务附件，与Mobile Forms中的情况一样。 自适应表单的任何“文件附件”类型按钮均处于隐藏状态。

1. 要保存自适应表单，请单击&#x200B;**保存**，与Mobile Forms中的情况一样。 自适应表单的任何“保存类型”按钮均处于隐藏状态。

1. 要提交自适应表单，请使用&#x200B;**Submit**&#x200B;按钮或可用的路由操作，与Mobile Forms中的情况一样。 自适应表单的任何提交类型按钮均处于隐藏状态。

1. **自适应表单全局工具栏可见性**:如果流程设计器隐藏全局/顶级工具栏，则工具栏和按钮不会显示在自适应表单上。

1. **自适应Forms的工作区导航控件**:在HTML工作区中，提供了“下一个/上一个”按钮以及自适应表单的“保存”、“提交”和“路由操作”按钮。单击下一步/上一步按钮以导航HTML工作区中自适应表单的面板。 “下一个/上一个”按钮提供深层导航，与自适应表单的“移动设备”视图中的导航控件类似。

1. **自适应表单的eSign服务和摘要组件**:摘要组件在HTML工作区中不可操作。换言之，如果自适应表单具有摘要组件，则它在工作区中不可见。 工作区用户在HTML工作区中单击“提交”或路由操作，而不是“设计”组件中的“自动提交”。 在文档签名后，它将显示为平面签名文档。 单击&#x200B;**Submit**&#x200B;或路由操作以关闭/完成任务或起点。\
   从eSign服务服务器收集已签名文档，并将数据xml文件转发到该过程的下一步。

## 在流程设计中使用自适应表单的步骤{#steps-to-use-adaptive-forms-in-process-design}

1. 打开Adobe Experience Manager Forms Workbench。

1. 转到&#x200B;**文件>新建>应用程序**&#x200B;或使用现有应用程序创建应用程序。

   ![创建新应用程序](assets/create_new_appl.png)

   创建新应用程序

1. 在应用程序中创建进程或使用现有进程。

   ![创建新流程](assets/create_new_process.png)

   创建新流程

1. 创建起始点或分配任务并双击该任务。
1. 在&#x200B;**[!UICONTROL 演示与数据]**&#x200B;部分下，选择&#x200B;**[!UICONTROL 使用CRX资产]**，然后单击资产前面的省略号。

   ![使用CRX资产](assets/use_crx_asset.png)

   使用CRX资产

1. 选择通过管理资产UI创建的自适应表单，然后单击&#x200B;**[!UICONTROL 确定]**。

   ![选择自适应表单](assets/selecting_form.png)

   选择自适应表单

   >[!NOTE]
   >
   >有关创建自适应表单的详细信息，请参阅[创建自适应表单](../../forms/using/creating-adaptive-form.md)。
   >
   >
   >有关创建进程的详细信息，请参阅[创建和管理进程](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html)。
