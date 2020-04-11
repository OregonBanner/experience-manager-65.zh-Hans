---
title: 自定义进程实例列表
seo-title: 自定义进程实例列表
description: 如何自定义在AEM Forms工作区中的进程实例中显示的属性。
seo-description: 如何自定义在AEM Forms工作区中的进程实例中显示的属性。
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 自定义进程实例列表 {#customizing-the-listing-of-process-instances}

进程实例列表显示在AEM Forms工作区的“跟踪”选项卡中。

在进程实例列表中，对于每个进程实例，AEM Forms工作区显示该实例的某些属性。 以下属性可用于每个进程实例。 这些属性作为属性存储在流程实例组件模型中，并可在其视图和模板中使用。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>描述</td>
   <td>进程实例的说明。</td>
  </tr>
  <tr>
   <td>启动器</td>
   <td>进程实例的启动器名称。</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>进程实例的启动器ID。</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>进程完成时的时间戳。</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>进程实例的ID。</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 =启动<br /> 1 =运行<br /> 2 =完成3 =完成<br /> 4 =终止<br /> 5 =终止<br /> 6 =暂停7 =暂停<br /><br /><br /> 8 =取消暂停</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>进程的名称。</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>进程开始时的时间戳。</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>进程变量对象的数组。 每个进程变量对 <strong>象都包含</strong> name <strong>（进程变量的名称）、</strong> value<strong> （进程变量的值）和type</strong> （进程变量的类型）。</td>
  </tr>
 </tbody>
</table>

**示例:**

要在进程 `description` 实例卡中显示进程实例的属性，请执行以下步骤。

1. 按照AEM Forms工 [作区自定义的常规步骤操作](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 执行以下操作：

   1. 将/libs/ws/js/runtime/templates/processinstance.html复制到/apps/ws/js/runtime/templates/（如果它不存在）。 单击“ **全部保存**”。
   1. 在processinstance.html中添加进程说明div，类为“processDescription”。

   ```
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 执行以下操作：

   1. 打开/apps/ws/js/registry.js进行编辑。
   1. 搜索并替换为 `text!/lc/libs/ws/js/runtime/templates/processinstance.html`应用 `text!/lc/`**程序&#x200B;**/ws/js/runtime/templates/processinstance.html。

1. 上述更改可能需要通过以下方式在样式表/apps/ws/css/newStyle.css中添加条目来更新CSS文件：

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
