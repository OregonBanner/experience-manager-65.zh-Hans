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
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 在HTML工作区中使用自适应表单{#using-an-adaptive-form-in-html-workspace}

JEE上的AEM Forms提供在HTML Workspace中使用自适应表单的功能。

由于您可以在流程设计过程中选择XDP，因此已添加从现有自适应表单AEM存储库中浏览的功能。 该功能使流程设计人员能够在起始点和任务中配置自适应表单。

## 流程设计体验 {#process-design-experience}

执行以下操作，使自适应表单能用于流程设计：

* 在分配任务和起始点中，当将表单资产分配给任务时，您可以浏览到CRX存储库中的自适应表单资产。
* 在“分配任务／起始点工作台”属性工作表中，可以隐藏自适应表单的顶级／全局工具栏。
* 您可以在自适应表单中为渲染和提交操作使用新的操作配置文件。

### LiveCycle应用程序导出和导入 {#livecycle-application-export-and-import}

由于自适应表单位于AEM存储库中，因此LiveCycle应用程序导出仅包含所使用自适应表单的引用。 因此，LiveCycle应用程序的导出和导入是一个分两步的过程。 LiveCycle应用程序包括进程定义等。 包含自适应表单的单独包将作为AEM的ZIP文件导出。 导入时，LiveCycle应用程序将通过Workbench导入，自适应表单将通过AEM导入。

## HTML工作区中自适应表单的用户体验 {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace除了为移动表单提供的控件外，还提供了一些特定于表单的自适应控件。 当用户打开任务或起始点时，用户可以在HTML Workspace中添加附件、保存、签署、提交和导航自适应表单。 以下是具体内容：

1. 要附加文件，请使用任务附件，就像移动表单中一样。 自适应表单的任何“文件附件”类型按钮都将隐藏。

1. 要保存自适应表单，请单 **击“保存**”，就像在移动表单中一样。 自适应表单的任何“保存类型”按钮都将隐藏。

1. 要提交自适应表单，请使用“提 **交** ”按钮或路由可用的操作，就像在移动表单中一样。 自适应表单的任何“提交类型”按钮都将隐藏。

1. **自适应表单全局工具栏可见性**:如果流程设计人员隐藏了全局／顶级工具栏、工具栏和按钮，则这些按钮不会显示在自适应表单上。

1. **自适应表单的工作区导航控件**:在HTML工作区中，“下一个”/“上一个”按钮以及“保存”、“提交”和“路由操作”按钮均可用。 单击“下一步”/“上一步”按钮，在HTML Workspace中导航自适应表单的面板。 “下一步”/“上一步”按钮提供深层导航，这与自适应表单的“移动”视图中的导航控件类似。

1. **自适应表单的电子签名服务和摘要组件**:摘要组件在HTML Workspace中不可操作。 换句话说，如果自适应表单具有摘要组件，则它在工作区中不可见。 工作区用户单击HTML Workspace中的“提交”或路由操作，而不是“设计”组件中的“自动提交”。 在文档签名后，它将显示为平面签名文档。 单击 **提交** ，或通过路由操作关闭／完成任务或起始点。\
   从eSign服务器收集已签名文档，并将data xml文件转发到该过程的下一步。

## 在流程设计中使用自适应表单的步骤 {#steps-to-use-adaptive-forms-in-process-design}

1. 打开Adobe Experience Manager Forms Workbench。

1. 转到“文 **件”>“新建”>“应用程序** ”，或使用现有应用程序创建应用程序。

   ![创建新应用程序](assets/create_new_appl.png)

   创建新应用程序

1. 创建进程，或在应用程序中使用现有进程。

   ![创建新流程](assets/create_new_process.png)

   创建新流程

1. 创建起点或分配任务，然后双击它。
1. 在“演示 **[!UICONTROL 和数据]** ”部分下，选择 **[!UICONTROL 使用CRX资产]** ，然后单击资产前面的省略号。

   ![使用CRX资产](assets/use_crx_asset.png)

   使用CRX资产

1. 选择通过“管理资产”UI创建的自适应表单，然后单击“确 **[!UICONTROL 定”]**。

   ![选择自适应表单](assets/selecting_form.png)

   选择自适应表单

   >[!NOTE]
   >
   >有关创建自适应表单的详细信息，请参 [阅创建自适应表单](../../forms/using/creating-adaptive-form.md)。
   >
   >
   >有关创建进程的详细信息，请参阅 [创建和管理进程](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html)。

