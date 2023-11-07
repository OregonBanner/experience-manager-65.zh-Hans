---
title: 在摘要URL中获取任务变量
description: 如何重用有关任务的信息并生成摘要URL以摘要或描述任务。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# 在摘要URL中获取任务变量 {#getting-task-variables-in-summary-url}

摘要页面显示与任务相关的信息。 本文介绍了如何在摘要页面中重用与任务相关的信息。

在此示例业务流程中，员工提交休假申请表。 然后，申请表将转至员工的经理进行审批。

1. 为resourceType创建示例HTML渲染器(html.esp) **员工/Pto应用程序**.

   渲染器假定在节点上设置以下属性：

   * ename
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

1. 修改编排，以从提交的表单数据中提取四个属性。 之后，在CRX中创建类型的节点 **员工/Pto应用程序**，并填充属性。

   1. 创建流程 **创建PTO摘要** 并将其用作之前 **分配任务** 在编排中进行操作。
   1. 定义 **employeeName**， **employeeID**， **ptoReason**， **totalDays**、和 **nodeName** 作为新流程中的输入变量。 这些变量将作为提交的表单数据传递。

      还定义一个输出变量 **Ptonodepath** ，在设置摘要URL时使用。

   1. 在 **创建PTO摘要** 流程，使用 **设置值** 用于在中设置输入详细信息的组件 **节点属性**(**nodeProps**)映射。

      此映射中的键应与上一步中HTML渲染器中定义的键相同。

      此外，添加 **sling：resourceType** 键值 **员工/Pto应用程序** 在地图上。

   1. 使用子流程 **storeContent** 从 **contentrepositorconnector** 中的服务 **创建PTO摘要** 进程。 此子进程将创建一个CRX节点。

      它需要三个输入变量：

      * **文件夹路径**：创建新CRX节点的路径。 将路径设置为 **/content**.
      * **节点名称**：将输入变量nodeName分配给此字段。 这是一个唯一的节点名称字符串。
      * **节点类型**：将类型定义为 **nt：unstructured**. 此进程的输出为nodePath。 nodePath是新创建节点的CRX路径。 ndoePath将成为 **创建PTO** 摘要流程。

   1. 传递提交的表单数据(**employeeName**， **employeeID**， **ptoReason**、和 **totalDays**)作为新进程的输入 **创建PTO摘要**. 将输出视为 **ptoSummaryNodePath**.

1. 将摘要URL定义为包含服务器详细信息的XPath表达式，以及 **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

在AEM Forms工作区中，当您打开任务时，摘要URL将访问CRX节点，并且HTML渲染器会显示摘要。

无需修改流程即可更改摘要布局。 HTML呈现器可正确显示摘要。
