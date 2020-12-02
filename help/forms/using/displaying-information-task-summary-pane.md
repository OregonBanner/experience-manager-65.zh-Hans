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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# 在“任务摘要”窗格中显示信息{#displaying-information-in-the-task-summary-pane}

在AEM Forms工作区中打开任务时，“任务摘要”窗格可显示任务的摘要。 任务的这一额外相关信息为AEM Forms工作区的最终用户增加了更多价值。

AEM Forms工作区允许您在“任务摘要”窗格中显示您选择的网页。 可以创建一个流程，以使用工作台显示“任务汇总”窗格。

1. 在Workbench中创建分配任务流程。 有关分配任务操作的详细信息，请参阅[工作台帮助](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)中的服务参考主题。

   >[!NOTE]
   >
   >如果存在TaskSummary URL，则默认情况下将打开“任务摘要”视图，而非“表单”视图。 在这种情况下，即使用户在“指定”任务中启用“以最大化模式打开表单”选项，表单也不会以最大化模式打开。

1. 配置任务摘要URL字段。 您可以指定文本值、模板、变量或XPath表达式。
1. 以下是显示“任务摘要”页面信息的示例。

   * 登录到`https://'[server]:[port]'/lc/crx/de`的CRXDE Lite环境。
   * `Create a node`**SampleSummary** ` under `/` with type `contentt:`. In the properties of this node, add `unstructuredsling:resourceTypeSampleSummaryPERM_WORKSPACE_` of type String and value ``. In the Access Control List of this node, add an entry for `` allowing `USERjcr:read` privileges.`
   * `Create a folder`**示** 例摘要 `/apps`下。在`/apps/SampleSummary`的访问控制列表中，为`PERM_WORKSPACE_USER`添加允许`jcr:readprivileges`的条目。
   * `Create a file `html.esp` at `/apps/`. For example, add the following lines in `SampleSummaryhtml.esp`.`

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

   * 在分配任务步骤中，将任务摘要url的值设置为`/lc/content/SampleSummary.html`。
   * 在AEM Forms工作区中打开与此分配任务步骤关联的任务时，`/apps/SampleSummary`的`html.esp`将呈现在任务摘要窗格中。
