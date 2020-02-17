---
title: 将工作流应用于页面
seo-title: 将工作流应用于页面
description: 可以从网站控制台启动工作流，也可以在编辑页面时从 Sidekick 启动工作流。
seo-description: 可以从网站控制台启动工作流，也可以在编辑页面时从 Sidekick 启动工作流。
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 将工作流应用于页面{#applying-workflows-to-pages}

在应用工作流时，您需要指定以下信息：

* 要应用的工作流。

   您可以应用任何工作流（由 AEM 管理员分配且您有权访问的工作流）。
* 可选：

   * 提供有关您启动工作流的原因的备注。
   * 有助于在用户收件箱中识别工作流实例的标题。

>[!NOTE]
>
>AEM 管理员可以使用[其他几种方法](/help/sites-administering/workflows-starting.md)来启动工作流。

## 应用工作流 {#applying-workflows}

可以从网站控制台启动工作流，也可以在编辑页面时从 Sidekick 启动工作流。

The **Status** column in the **Websites** console indicates whether a workflow has been applied to a page:

![工作流状态](assets/workflowstatus.png)

### 从网站控制台启动工作流 {#starting-a-workflow-from-the-websites-console}

1. 打开网站控制台。([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. 在“网站”树中，选择要应用工作流的页面的父项。
1. 在页面列表中，选择相应的页面，然后单击“工作流”。
1. 在“启动工作流”对话框中，选择要应用的工作流。（可选）输入备注和标题。然后，单击“启动”。

### 使用 Sidekick 启动工作流 {#starting-a-workflow-using-sidekick}

1. 打开网站控制台。
1. 打开所需的页面。
1. 从 Sidekick 中选择“工作流”选项卡。
1. Expand the **Workflow** dialog, allowing you to select the **Workflow** and optionally enter **Workflow Title** and **Comment**.

   ![工作流启动sidekick](assets/workflowstartsidekick.png)

1. 单击&#x200B;**启动工作流**&#x200B;以启动新工作流实例，并将您配置的属性和当前页面作为有效负荷。现在，工作流即处于运行状态。

