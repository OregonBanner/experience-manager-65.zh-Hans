---
title: 获取摘要URL中的任务变量
seo-title: 获取摘要URL中的任务变量
description: 如何重复使用任务相关信息并生成摘要URL以汇总或描述任务。
seo-description: 如何重复使用任务相关信息并生成摘要URL以汇总或描述任务。
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 获取摘要URL中的任务变量 {#getting-task-variables-in-summary-url}

摘要页面显示与任务相关的信息。 本文介绍如何在摘要页面中重复使用与任务相关的信息。

在此范例编排中，员工会提交一个休假申请表。 然后，申请表将转至员工经理进行批准。

1. 为resourcesType **Employees/PtoApplication创建示例HTML渲染器(html.esp)**。

   呈示器假定要在节点上设置以下属性：

   * ename
   * empid
   * 原因
   * 持续时间
   **注意**:此呈示器是摘要页面模板。

   此呈示器的以下示例代码包含在：

   `apps/Employees/PtoApplication/html.esp`

   ```
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

1. 修改编排，从提交的表单数据中提取四个属性。 之后，在CRX中创建Employees/PtoApplication类 **型的节点**，并填充属性。

   1. 创建流程， **创建PTO汇总** ，并在编排“分配任务”操作之 **** 前将其用作子流程。
   1. 在新流 **程中，将EmployeeName**、 **employeeID、ptoReason**、DaysName和EmployeeName中的Total DaysName和NedNode ************ （总天数）定义为输入变量。 这些变量将作为提交的表单数据传递。

      还定义一个输出变量**ptoNodePath **，它将在设置摘要Url时使用。

   1. 在创 **建PTO汇总流程中** ，使用 **set value** component在**nodeProperty **(**nodeProps**)映射中设置输入详细信息。

      此映射中的键应与上一步中在HTML渲染器中定义的键相同。

      此外，在图中 **添加一个sling:resourceType** , **其值为Employees/PtoApplication** 。

   1. 在创建PTO **摘要流程中** ，使用 **ContentRepositoryConnector服务中的子进** 程storeContent **** 。 此子进程创建CRX节点。

      它需要三个输入变量：

      * **文件夹路径**:创建新CRX节点的路径。 将路径设置为 **/内容**。
      * **节点名称**:将输入变量nodeName指定到此字段。 这是唯一的节点名称字符串。
      * **节点类型**:将类型定义为 **nt:unstructured**。 此过程的输出是nodePath。 nodePath是新创建节点的CRX路径。 ndoePath将是创建PTO汇总流程的 **最终输出** 。
   1. 将提交的表单数据(**employeeName**、 **employeeID**、 **Reason和totalDaysReason**********)作为新流程创建PTO汇总输入传递至新流程。 将输出视为 **ptoSummaryNodePath**。


1. 将摘要Url定义为包含服务器详细信息和 **ptoSummaryNodePath的XPath表达式**。

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

在AEM Forms工作区中，打开任务时，摘要Url将访问CRX节点，HTML渲染器将显示摘要。

可以更改摘要布局，而无需修改该过程。 HTML渲染器会相应地显示摘要。

**[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)**
