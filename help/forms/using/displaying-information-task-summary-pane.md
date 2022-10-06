---
title: 在“任务摘要”窗格中显示信息
seo-title: Displaying information in the Task Summary pane
description: 在AEM Forms工作区中，可以配置“任务摘要”窗格以汇总任务或显示任何其他网页。
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 在“任务摘要”窗格中显示信息 {#displaying-information-in-the-task-summary-pane}

在AEM Forms工作区中打开任务时，“任务摘要”窗格可以显示该任务的摘要。 任务的这一附加相关信息可为AEM Forms工作区的最终用户带来更多价值。

AEM Forms工作区允许您在“任务摘要”窗格中显示您选择的网页。 可以创建一个流程，以使用Workbench显示“任务摘要”窗格。

1. 在Workbench中创建分配任务流程。 有关“分配任务”操作的更多详细信息，请参阅 [Workbench帮助](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >如果存在“任务摘要”URL，则默认情况下会打开“任务摘要”视图，而不是“表单”视图。 在这种情况下，即使用户在“分配任务”中启用“以最大化模式打开表单”选项，表单也不会以最大化模式打开。

1. 配置任务摘要URL字段。 您可以指定文字值、模板、变量或XPath表达式。
1. 下面显示“任务摘要”页上的信息示例。

   * 登录CRXDE Lite环境： `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**示例摘要** ` under `/content` with type `nt：非结构化`. In the properties of this node, add `sling:resourceType` of type String and value `示例摘要`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `Create a folder`**示例摘要** 在 `/apps`. 在 `/apps/SampleSummary`，为添加条目 `PERM_WORKSPACE_USER` 允许 `jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * 将任务摘要url的值设置为 `/lc/content/SampleSummary.html` 分配任务步骤中。
   * 当在AEM Forms工作区中打开与此“分配任务”步骤关联的任务时， `html.esp` at `/apps/SampleSummary` 呈现在任务摘要窗格中。
