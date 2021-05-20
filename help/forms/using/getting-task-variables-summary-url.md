---
title: 在摘要URL中获取任务变量
seo-title: 在摘要URL中获取任务变量
description: 如何重复使用有关任务的信息并生成摘要URL以汇总或描述任务。
seo-description: 如何重复使用有关任务的信息并生成摘要URL以汇总或描述任务。
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# 在摘要URL {#getting-task-variables-in-summary-url}中获取任务变量

摘要页显示与任务相关的信息。 本文介绍了如何重复使用摘要页面中与任务相关的信息。

在此编排示例中，员工提交了休假申请表。 然后，申请表将转至员工经理进行审批。

1. 为resourceType **Employees/PtoApplication**&#x200B;创建示例HTML渲染器(html.esp)。

   呈现器假定要在节点上设置以下属性：

   * name
   * empid
   * 原因
   * 持续时间

   >[!NOTE]
   >
   >此渲染器是摘要页面模板。

   此渲染器的以下示例代码包含在中：

   `apps/Employees/PtoApplication/html.esp`

   ```html
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. 修改编排以从提交的表单数据中提取四个属性。 之后，在CRX中创建类型为&#x200B;**Employees/PtoApplication**&#x200B;的节点，并填充属性。

   1. 创建流程&#x200B;**创建PTO摘要**&#x200B;并在业务流程中的&#x200B;**分配任务**&#x200B;操作之前将其用作子流程。
   1. 将&#x200B;**employeeName**、**employeeID**、**ptoReason**、**totalDays**&#x200B;和&#x200B;**nodeName**&#x200B;定义为新流程中的输入变量。 这些变量将作为提交的表单数据进行传递。

      此外，还定义一个输出变量&#x200B;**ptoNodePath**，该变量将在设置摘要Url时使用。

   1. 在&#x200B;**创建PTO摘要**&#x200B;流程中，使用&#x200B;**set value**&#x200B;组件在&#x200B;**nodeProperty**(**nodeProps**)映射中设置输入详细信息。

      此映射中的键应与上一步中HTML渲染器中定义的键相同。

      此外，在映射中添加值为&#x200B;**Employees/PtoApplication**&#x200B;的&#x200B;**sling:resourceType**&#x200B;键。

   1. 使用&#x200B;**创建PTO摘要**&#x200B;流程中&#x200B;**ContentRepositoryConnector**&#x200B;服务的子进程&#x200B;**storeContent**。 此子进程会创建一个CRX节点。

      它需要三个输入变量：

      * **文件夹路径**:创建新CRX节点的路径。将路径设置为&#x200B;**/content**。
      * **节点名称**:将输入变量nodeName分配给此字段。这是唯一的节点名称字符串。
      * **节点类型**:将类型定义 **为nt:unstructured**。此进程的输出为nodePath。 nodePath是新创建节点的CRX路径。 ndoePath将是&#x200B;**创建PTO**&#x200B;摘要流程的最终输出。
   1. 将提交的表单数据（**employeeName**、**employeeID**、**ptoReason**&#x200B;和&#x200B;**totalDays**）作为输入传递给新流程&#x200B;**创建PTO摘要**。 将输出作为&#x200B;**ptoSummaryNodePath**。


1. 将摘要Url定义为XPath表达式，其中包含服务器详细信息以及&#x200B;**ptoSummaryNodePath**。

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

在AEM Forms工作区中，打开任务时，摘要Url将访问CRX节点，而HTML渲染器将显示该摘要。

无需修改流程，即可更改摘要布局。 HTML渲染器会相应地显示摘要。
