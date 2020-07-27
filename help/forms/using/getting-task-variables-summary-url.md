---
title: 在摘要URL中获取任务变量
seo-title: 在摘要URL中获取任务变量
description: 如何重用有关任务的信息并生成摘要URL以汇总或描述任务。
seo-description: 如何重用有关任务的信息并生成摘要URL以汇总或描述任务。
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# 在摘要URL中获取任务变量 {#getting-task-variables-in-summary-url}

摘要页显示与任务相关的信息。 本文介绍如何在摘要页面中重用与任务相关的信息。

在此例程安排中，员工提交了休假申请表。 然后，申请表将转至员工经理进行审批。

1. 为资源类型员工/PtoApplication创建示例HTML **渲染器(html.esp)**。

   呈示器假定要在节点上设置以下属性：

   * ename
   * empid
   * 原因
   * 持续时间

   >[!NOTE]
   >
   >此呈现器是摘要页面模板。

   此呈示器的以下示例代码包含在：

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

1. 修改业务流程以从提交的表单数据中提取四个属性。 之后，在CRX中创建Employees/PtoApplication类 **型的节点**，并填充属性。

   1. 在业务流程 **中分配任务** 操作之前，创建流程创建 **PTO汇总，并将其用作子流** 程。
   1. 在新 **流程中**，将 **EmployeeName**、EmployeeID、PtoReason **、DaysName、********** AdobeName和EmployeeName定义为输入变量。 这些变量将作为提交的表单数据传递。

      还定义一个输 **出变量** ptoNodePath，在设置摘要Url时将使用它。

   1. 在创 **建PTO汇总** 过程中，使 **用设置值组件** ，在nodeProperty **(nodeProps)映射中******&#x200B;设置输入详细信息。

      此映射中的键应与上一步中在HTML渲染器中定义的键相同。

      此外，在 **图中添加** sling:resourceType键 **和值Employees/** PtoApplication。

   1. 在创建PTO **摘要流程** 中，使 **用ContentRepositoryConnector** 服务中 **的子流程storeContent** 。 此子进程创建CRX节点。

      它需要三个输入变量：

      * **文件夹路径**: 创建新CRX节点的路径。 将路径设置为 **/内容**。
      * **节点名称**: 将输入变量nodeName指定到此字段。 这是唯一的节点名称字符串。
      * **节点类型**: 将类型定义 **为nt:unstructured**。 此过程的输出为nodePath。 nodePath是新创建节点的CRX路径。 ndoePath将是创建PTO汇总流程 **的最终输** 出结果。
   1. 将提交的表单数据(**employeeName**、 **employeeID、** ptoDaysReason **和totalDaysAds)作为输入传递**********&#x200B;至新流程，创建PTO摘要。 将输出取为 **ptoSummaryNodePath**。


1. 将摘要Url定义为XPath表达式，其中包含服务器详细信息以 **及ptoSummaryNodePath**。

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

在AEM Forms工作区中，打开任务时，摘要Url将访问CRX节点，HTML呈现器将显示摘要。

可以更改摘要布局，而无需修改流程。 HTML渲染器会相应地显示摘要。
