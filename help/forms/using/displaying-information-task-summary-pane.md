---
title: 在“任务摘要”窗格中显示信息
seo-title: 在“任务摘要”窗格中显示信息
description: 在AEM Forms工作区中，可以配置“任务摘要”窗格以汇总任务或显示任何其他网页。
seo-description: 在AEM Forms工作区中，可以配置“任务摘要”窗格以汇总任务或显示任何其他网页。
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 在“任务摘要”窗格中显示信息 {#displaying-information-in-the-task-summary-pane}

在AEM Forms工作区中打开任务时，“任务摘要”窗格可以显示任务的摘要。 此任务的附加相关信息为AEM Forms工作区的最终用户增加了更多价值。

AEM Forms工作区允许您在“任务摘要”窗格中显示您选择的网页。 可以创建一个流程，以使用Workbench显示“任务汇总”窗格。

1. 在Workbench中创建分配任务流程。 有关分配任务操作的更多详细信息，请参阅工作台帮助中的服务 [参考主题](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)。

   >[!NOTE]
   >
   >如果存在TaskSummary URL，则默认情况下将打开任务摘要视图，而不是表单视图。 在这种情况下，即使用户在“分配”任务中启用“以最大化模式打开表单”选项，表单也不会以最大化模式打开。

1. 配置任务摘要URL字段。 您可以指定文本值、模板、变量或XPath表达式。
1. 以下是显示“任务摘要”页面信息的示例。

   * 登录CRXDE Lite环境，网址为 `https://'[server]:[port]'/lc/crx/de`。
   * `Create a node`**SampleSummary **/` under `contentt:` with type `unstructuredsling:`. In the properties of this node, add `resourceTypeSampleSummaryPERM_WORKSPACE_` of type String and value ``. In the Access Control List of this node, add an entry for `` allowing `USERjcr:read` privileges.`
   * `Create a folder`**示例摘要&#x200B;**，位于`/apps`下。 在的访问控制列表`/apps/SampleSummary`中，添加一个允许`PERM_WORKSPACE_USER`的条目`jcr:readprivileges`。
   * `Create a file `html.esp` at `/apps/`. For example, add the following lines in `SampleSummaryhtml.esp`.`

   ```
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

   * 设置任务摘要url的值，如分配 `/lc/content/SampleSummary.html` 任务步骤中所示。
   * 在AEM Forms工作区中打开与此分配任务步骤关联的任务时，将在任务摘要 `html.esp` 窗 `/apps/SampleSummary` 格中显示“位置”。
