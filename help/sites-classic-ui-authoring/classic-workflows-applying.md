---
title: 将工作流程应用于页面
description: 工作流可以从“网站”控制台启动，或者在编辑页面时从Sidekick启动。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: d8b604c5-a6da-47c4-9422-b519e224c7ca
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 15%

---

# 将工作流程应用于页面{#applying-workflows-to-pages}

在应用工作流时，您需要指定以下信息：

* 要应用的工作流。

  您可以应用任何工作流（您有权访问，由 AEM 管理员分配）。
* 可选：

   * 一个注释，为您提供有关启动工作流的原因的信息。
   * 帮助标识用户收件箱中的工作流实例的标题。

>[!NOTE]
>
>AEM管理员可以使用以下方式启动工作流 [其他几种方法](/help/sites-administering/workflows-starting.md).

## 应用工作流 {#applying-workflows}

工作流可以从“网站”控制台启动，或者在编辑页面时从Sidekick启动。

此 **状态** 中的列 **网站** 控制台指示工作流是否已应用于页面：

![workflowstatus](assets/workflowstatus.png)

### 从网站控制台启动工作流 {#starting-a-workflow-from-the-websites-console}

1. 打开“网站”控制台。 ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. 在网站树中，选择要应用工作流的页面的父页面。
1. 在页面列表中，选择页面，然后单击“工作流”。
1. 在启动工作流对话框中，选择要应用的工作流。 或者，输入评论和标题。 然后，单击“Start（开始）”。

### 使用Sidekick启动工作流 {#starting-a-workflow-using-sidekick}

1. 打开“网站”控制台。
1. 打开所需的页面。
1. 从Sidekick中选择Workflow选项卡。
1. 展开 **工作流** 对话框，允许您选择 **工作流** （可选）输入 **工作流标题** 和 **注释**.

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. 单击 **启动工作流** ，以启动新的工作流实例，其中使用您配置的属性和当前页面作为有效负载。 现在工作流正在运行。
