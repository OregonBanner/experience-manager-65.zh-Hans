---
title: 將工作流程套用至內容頁面
description: 进行创作时，您可以调用工作流以在页面上执行操作；也可以应用多个工作流。
uuid: 652d9a23-907d-43ad-9eef-7ab1d07918cd
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 6472dc94-96e0-4286-8f86-d85726cc843c
docset: aem65
exl-id: e00da2b3-046a-4d93-aed0-07dd8c66899f
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 55%

---

# 将工作流应用于页面{#applying-workflows-to-pages}

进行创作时，您可以调用工作流以在页面上执行操作；也可以应用多个工作流。

套用工作流程時，請指定下列資訊：

* 要应用的工作流。您可以应用任何工作流（您有权访问，由 AEM 管理员分配）。
* （可選）有助於識別使用者收件匣中的工作流程例項的標題。
* 工作流程裝載；這可以是一或多個頁面。

工作流程可從以下位置開始：

* [站点控制台](#starting-a-workflow-from-the-sites-console)。
* [编辑页面时，从“页面信息”](#starting-a-workflow-from-the-page-editor)启动。

>[!NOTE]
>
>另请参阅：
>
>* [如何將工作流程套用至DAM資產](/help/assets/assets-workflow.md).
>* [使用项目工作流](/help/sites-authoring/projects-with-workflows.md)。
>


>[!NOTE]
>
>AEM管理員可以 [使用數種其他方法開始工作流程](/help/sites-administering/workflows-starting.md).

## 從Sites Console啟動工作流程 {#starting-a-workflow-from-the-sites-console}

您可以從下列任一項開始工作流程：

* [“站点”工具栏的“创建”选项](#starting-a-workflow-from-the-sites-toolbar)。
* [“站点”控制台的时间线边栏](#starting-a-workflow-from-the-timeline)。

在這兩種情況下，您都需要：

* [在建立工作流程精靈中指定工作流程詳細資訊](#specifying-workflow-details-in-the-create-workflow-wizard).

### 從網站工具列啟動工作流程 {#starting-a-workflow-from-the-sites-toolbar}

您可以从&#x200B;**站点**&#x200B;控制台的工具栏中启动工作流：

1. 导航到所需的页面并选择该页面。

1. 现在，您可以从工具栏的&#x200B;**创建**&#x200B;选项中选择&#x200B;**工作流**。

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. 此 **建立工作流程** 精靈將協助您 [指定工作流程詳細資訊](#specifying-workflow-details-in-the-create-workflow-wizard).

### 从时间线启动工作流 {#starting-a-workflow-from-the-timeline}

您可以从&#x200B;**时间线**&#x200B;中启动要应用于所选资源的工作流。

1. [选择资源](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources)，然后打开[时间线](/help/sites-authoring/basic-handling.md#timeline)（或打开时间线，然后选择资源）。
1. 可以使用评论字段中的箭头显示&#x200B;**启动工作流**：

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. 此 **建立工作流程** 精靈將協助您 [指定工作流程詳細資訊](#specifying-workflow-details-in-the-create-workflow-wizard).

### 在建立工作流程精靈中指定工作流程詳細資訊 {#specifying-workflow-details-in-the-create-workflow-wizard}

此 **建立工作流程** 精靈將協助您選取工作流程並指定必要的詳細資訊。

開啟 **建立工作流程** 精靈的來源：

* [“站点”工具栏的“创建”选项](#starting-a-workflow-from-the-sites-toolbar)。
* [“站点”控制台的时间线边栏](#starting-a-workflow-from-the-timeline)。

您可以指定詳細資料：

1. 在 **屬性** 步驟，則會定義工作流程的基本選項：

   * **工作流模型**
   * **工作流标题**

      * 您可以指定此執行個體的標題，協助您在稍後階段識別它。

   根據工作流程模型，也可以使用下列選項。 這些功能可在工作流程完成後，保留建立為裝載的封裝。

   * **保留工作流包**
   * **包标题**

      * 您可以指定封裝的標題，以協助識別。
   >[!NOTE]
   >
   >为多资源支持配置了工作流并选择了多个资源时，**保留工作流包**&#x200B;选项可用。[](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)

   完成后，单击&#x200B;**下一步**&#x200B;继续。

   ![wf-52](assets/wf-52.png)

1. 在&#x200B;**范围**&#x200B;步骤中，您可以选择：

   * **添加内容**&#x200B;以打开[路径浏览器](/help/sites-authoring/author-environment-tools.md#path-browser)并选择其他资源；在浏览器中，单击/点按&#x200B;**选择**&#x200B;以将内容添加到工作流实例。

   * 现有资源以查看其他操作：

      * **包括子项**，指定将该资源的子项包含在工作流中。
系统将打开一个对话框，允许您根据以下各项优化选择：

         * 仅包括下级子项.
         * 仅包括已修改的页面.
         * 仅包括已发布的页面.

         任何指定的子項都會新增至將套用工作流程的資源清單中。

      * **移除選取專案** 以從工作流程中移除該資源。

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >如果添加其他资源，则可以使用&#x200B;**返回**，在&#x200B;**属性**&#x200B;步骤中调整&#x200B;**保留工作流包**&#x200B;的设置。

1. 使用&#x200B;**创建**&#x200B;关闭向导并创建工作流实例。通知會顯示在Sites主控台中。

## 從頁面編輯器啟動工作流程 {#starting-a-workflow-from-the-page-editor}

編輯頁面時，您可以選取 **頁面資訊** （從工具列）。 下拉式選單具有選項 **在工作流程中開始**. 此选项将打开一个对话框，您可以在其中指定所需的工作流，如果需要，还可以指定标题：

![wf-54](assets/wf-54.png)
