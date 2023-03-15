---
title: 自定义流程实例列表
seo-title: Customizing the listing of process instances
description: 如何在AEM Forms工作区中自定义流程实例中显示的属性。
seo-description: How-to customize the properties displayed in process instance in AEM Forms workspace.
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
exl-id: b27ffe92-8491-43a0-bf42-613eb39a606e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# 自定义流程实例列表 {#customizing-the-listing-of-process-instances}

流程实例列表显示在AEM Forms工作区的“跟踪”选项卡中。

在流程实例列表中，对于每个流程实例，AEM Forms工作区显示该实例的一些属性。 以下属性适用于每个进程实例。 这些属性作为属性存储在流程实例组件模型中，并可用于其视图和模板。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>描述</td>
   <td>流程实例的描述。</td>
  </tr>
  <tr>
   <td>发起者</td>
   <td>进程实例的启动器名称。</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>进程实例的发起者的ID。</td>
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
   <td>processinstancestatus</td>
   <td>0 =已启动<br /> 1 =正在运行<br /> 2 =完成<br /> 3 =正在完成<br /> 4 =已终止<br /> 5 =终止<br /> 6 =已暂停<br /> 7 =暂停<br /> 8 =取消暂停</td>
  </tr>
  <tr>
   <td>processname</td>
   <td>进程名称。</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>进程启动时的时间戳。</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>进程变量的对象数组。 每个进程变量对象包含 <strong>name</strong> （流程变量的名称）， <strong>值</strong> （流程变量的值），以及<strong> type</strong> （流程变量的类型）。</td>
  </tr>
 </tbody>
</table>

**示例:**

要显示 `description` 属性，请执行以下步骤。

1. 请遵循 [AEM Forms工作区自定义的一般步骤](/help/forms/using/generic-steps-html-workspace-customization.md).
1. 执行以下操作：

   1. 如果/libs/ws/js/runtime/templates/processinstance.html不存在，请将其复制到/apps/ws/js/runtime/templates/。 单击 **全部保存**.
   1. 通过类= &#39;processDescription&#39; inprocessinstance.html添加进程描述div。

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 执行以下操作：

   1. 打开/apps/ws/js/registry.js进行编辑。
   1. 搜索和替换 `text!/lc/libs/ws/js/runtime/templates/processinstance.html`替换为 `text!/lc/`**应用程序**/ws/js/runtime/templates/processinstance.html.

1. 通过以以下方式在样式表/apps/ws/css/newStyle.css中添加条目，上述更改可能需要更新CSS文件：

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
