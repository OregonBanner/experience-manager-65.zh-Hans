---
title: 可重用组件描述
seo-title: 可重用组件描述
description: 可重用组件的完整列表，包含文件名和依赖项，可帮助您将AEM Forms工作区组件集成到Web应用程序中。
seo-description: 可重用组件的完整列表，包含文件名和依赖项，可帮助您将AEM Forms工作区组件集成到Web应用程序中。
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 9%

---

# 可重用组件{#description-of-reusable-components}的描述

AEM Forms工作区由[可重用](/help/forms/using/integrating-html-ws-components-web.md)组件组成，这些组件组织在CRX™中的特定[文件夹结构](/help/forms/using/folder-structure.md)中。 每个组件在文件夹结构中指定的位置都有模型、视图和模板文件，JavaScript™依赖于其他组件文件，组件侦听的事件以及在AEM Forms工作区中触发这些事件的JavaScript对象。 此处提供了包含组成文件名和依赖项的可重用组件的完整列表。

## 任务列表 {#tasklist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>tasklist.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td>
    <ul>
     <li><p>UserSearch</p></li>
     <li><p>任务</p></li>
     <li><p>团队任务</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td>
    <ul>
     <li><p>任务模型</p></li>
     <li><p>团队任务模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>filterSelected - tasklist模型</p></li>
     <li><p>移除 — 任务列表模型</p></li>
     <li><p>updateQueue - tasklist模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果您从自定义应用程序中触发此组件的filterSelected事件，则此组件可以独立于AEM Forms工作区使用。

## 任务 {#task}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>task.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td>
    <ul>
     <li><p>任务列表模型</p></li>
     <li><p>taskactions实用程序</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>submitComplete — 任务模型</p></li>
     <li><p>拒绝 — 任务模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>工作区调用TaskList模型的fetchTasks函数，以便为此组件创建任务模型。

## FilterList {#filterlist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>filterlist.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>filterlist.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>已获取 — 任务列表模型 </p></li>
     <li><p>移除 — 任务列表模型 </p></li>
     <li><p>updateQueue - tasklist模型 </p></li>
     <li><p>refresedQueue - tasklist模型 </p></li>
     <li><p>filterSelected - tasklist模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 筛选器 {#filter}

<table>
 <tbody>
  <tr>
   <td><p>查看</p> </td>
   <td><p>filter.js</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>filter.html</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td>
    <ul>
     <li><p>字段：队列：{ name， qid， isDefault， type}</p> </li>
     <li><p>字段：查询：字符串</p> </li>
     <li><p>字段：parentView:过滤器列表视图</p> </li>
     <li><p>字段：parentModel:任务列表模型</p> </li>
     <li><p>字段：实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件侦听</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

## TeamQueues {#teamqueues}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>teamqueues.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>teamqueues.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>已获取 — 任务列表模型 </p></li>
     <li><p>移除 — 任务列表模型 </p></li>
     <li><p>updateQueue - tasklist模型 </p></li>
     <li><p>teamQueuesIchated - tasklist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## TeamFilter {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>teamfilter.js</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>teamfilter.html</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td>
    <ul>
     <li><p>扩展：过滤视图</p> </li>
     <li><p>字段：queue :{ name， qid， isDefault， type }</p> </li>
     <li><p>字段：查询：字符串</p> </li>
     <li><p>字段：parentView :过滤器列表视图</p> </li>
     <li><p>字段：parentModel :任务列表模型</p> </li>
     <li><p>字段：实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件侦听</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter会获取事件，指示从TaskList组件中选择了哪个任务。 尽管这些组件共享模型类，但没有其他依赖项。

## 任务详细信息 {#taskdetails}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>tasklist.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>taskdetails.js</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>taskdetails.html</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td><p>大多数实用工具类</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>窗体渲染实用程序</p> </li>
     <li><p>注释实用程序</p> </li>
     <li><p>附件实用程序</p> </li>
     <li><p>taskactions实用程序</p> </li>
     <li><p>历史实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li><p>转发 — 任务模型</p> </li>
     <li><p>共享 — 任务模型</p> </li>
     <li><p>已咨询 — 任务模型</p> </li>
     <li><p>被拒绝 — 任务模型</p> </li>
     <li><p>放弃 — 任务模型</p> </li>
     <li><p>已解锁 — 任务模型</p> </li>
     <li><p>锁定 — 任务模型</p> </li>
     <li><p>已声明 — 任务模型</p> </li>
     <li><p>更改：已选择任务 — 任务列表模型</p> </li>
     <li><p>change:formUrl — 任务模型</p> </li>
     <li>attachmentURLFeched — 任务模型</li>
    </ul>
    <ul>
     <li>newAttachment — 任务模型</li>
     <li><p>taskHistoryIchated — 任务模型</p> </li>
     <li>prepareForSubmitComplete — 任务模型</li>
     <li><p>submitComplete — 任务模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 类别列表 {#categorylist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>startprocess.html（在路由文件夹中）</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>类别</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td>
    <ul>
     <li><p>favoritecategorfactory模型</p></li>
     <li><p>allcategorfactory模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>allStartpointsIcated - categorylist模型 </p></li>
     <li><p>add - categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此组件使用某些其他组件（如StartPointList、StartPoint和Task）的模型类。 除此依赖项外， CategoryList还可单独使用。

## 类别 {#category}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>category.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td>
    <ul>
     <li><p>类别列表模型</p></li>
     <li><p>startpointlist模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>已更改 — 类别模型 </p></li>
     <li><p>childrenIcketed — 类别模型 </p></li>
     <li><p>类别：选定 — 类别列表模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## StartPointList {#startpointlist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>startpointlist.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>startprocess.html（在路由文件夹中）</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td>
    <ul>
     <li><p>类别模型</p></li>
     <li><p>favoritecategorfactory模型</p></li>
     <li><p>allcategorfactory模型</p></li>
     <li><p>startpoint视图</p></li>
     <li><p>startpointlist模型</p></li>
     <li><p>起点模型</p></li>
     <li><p>任务模型</p></li>
     <li><p>任务模型</p></li>
     <li><p>任务列表模型</p></li>
     <li><p>团队任务模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>类别：选定 — 类别列表模型 </p></li>
     <li><p>allStartpointsIcated - categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList和CategoryList组件共享模型类，因此前者取决于后者。 CategoryList访问有关显示哪个类别起点的信息。 要单独使用StartPointList，请模拟CategoryList中的事件触发器。

## StartPoint {#startpoint}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>startpoint.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>任务模型</p></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td><p>更改 — 起点模型 </p></td>
  </tr>
 </tbody>
</table>

## StartProcess {#startprocess}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>categorylist.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>startprocess.js</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>startprocess.html</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td>
    <ul>
     <li><p>大多数实用工具类</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td>
    <ul>
     <li><p>类别模型</p> </li>
     <li><p>favoritecategorfactory模型</p> </li>
     <li><p>allcategorfactory模型</p> </li>
     <li><p>窗体渲染实用程序</p> </li>
     <li><p>注释实用程序</p> </li>
     <li><p>附件实用程序</p> </li>
     <li><p>taskactions实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li><p>类别：选定 — 类别列表模型</p> </li>
     <li><p>change:invikedTask - startpointlist模型</p> </li>
     <li><p>change:formUrl — 任务模型</p> </li>
     <li><p>startpoint:selected - startpointlist模型</p> </li>
     <li><p>转发 — 任务模型</p> </li>
     <li><p>放弃 — 任务模型</p> </li>
     <li><p>已解锁 — 任务模型</p> </li>
     <li><p>锁定 — 任务模型</p> </li>
     <li>attachmentURLFeched — 任务模型</li>
     <li>newAttachment — 任务模型</li>
     <li>prepareForSubmitComplete — 任务模型 </li>
     <li><p>submitComplete — 任务模型</p> </li>
     <li><p>allStartpointsIcated - categorylist模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess和StartPointList组件共享模型类。 从StartPointList中选择起始点时，此组件会变得相关。

## ProcessNameList {#processnamelist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>tracking.html（在路由文件夹中）</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>过程名称模型</p></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist模型 </p></li>
     <li><p>已获取：processnames -processnamelist模型 </p></li>
     <li><p>更改 — 流程名称列表模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList不依赖于其他组件。 但是，在内部它取决于ProcessInstanceList模型类，而ProcessInstanceList模型类又取决于其他组件。 因此，ProcessNameList使用许多模型类，如ProcessInstanceList、ProcessInstance、TaskList、Teamtask和Task。 除了这些依赖关系外，ProcessNameList还可以单独使用。

## ProcessName {#processname}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>processname（在processnamelist.js中）</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>processname.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>过程实例列表模型</p></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td><p>更改 — processname模型 </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceList {#processinstancelist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>processinstancelist.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>tracking.html（在路由文件夹中）</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>过程名称模型</p></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>processname:selected -processnamelist模型 </p></li>
     <li><p>processname:instanceceated - processnamelist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList需要ProcessNameList中的一个事件，该事件指示用于获取和显示实例的进程名称。 要单独使用ProcessInstanceList，请单独模拟事件触发器。

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>processnamelist.js中的processname</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>任务列表模型</p></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td><p>更改 — 处理实例模型 </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceHistory {#processinstancehistory}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>processinstancehistory.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>processinstancehistory.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td>
    <ul>
     <li><p>过程名称模型</p></li>
     <li><p>历史实用程序</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>processname:selected -processnamelist模型 </p></li>
     <li><p>processinstance:selected -processinstancelist模型 </p></li>
     <li><p>tasksIgated - processinstance模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory需要ProcessInstanceList中的事件，以指示要显示哪个进程实例的历史记录。 除此依赖关系外，组件还可以单独使用。

## OutofOffice {#outofoffice}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>outofoffice.html</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td><p>用户搜索视图</p> </td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li><p>outOfficeSettingsItched - outoffice模型</p> </li>
     <li><p>outOfficeSettingsSaved - outfofice模型</p> </li>
     <li><p>processesIchated - outoffice模型</p> </li>
     <li><p>principalSelected - principalsearch视图</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice可以独立使用。

## ShareQueue {#sharequeue}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>sharequeue.html</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td><p>用户搜索视图</p> </td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGreaded - sharequeue模型</p> </li>
     <li><p>queueAccessRequested - sharequeue模型</p> </li>
     <li><p>grandedUsersIchated - sharequeue模型</p> </li>
     <li>accessibleUsersIched - sharequeue模型</li>
     <li><p>queueAccessRevoded - sharequeue模型</p> </li>
     <li><p>queueAccessRemoved - sharequeue模型</p> </li>
     <li><p>principalSelected - principalsearch视图</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue可以单独使用。

## UISettings {#uisettings}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>uisettings.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>preferencesIcated — 提交模型 </p></li>
     <li><p>settingUpdated - uisettings模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings可以单独使用。

## AppNavigation {#appnavigation}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>appnavigation.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>事件侦听</p></td>
   <td><p>NA</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation可以单独使用。

## UserInfo {#userinfo}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>userinfo.html</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li>userImageUrlIcated - userinfo模型</li>
     <li>sessionRextended - userinfo模型<br /> </li>
     <li>sessionExpired - userinfo模型 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo可以单独使用。

## WSError {#wserror}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>wserror.html</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p></td>
   <td><p>newWsError — 错误模型 </p></td>
  </tr>
 </tbody>
</table>

## UserSearch {#usersearch}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>usersearch.html</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li>principalSearch - principalsearch模型</li>
     <li>outOfOfficeInfoIched - usersearch模型</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SearchTemplate {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>searchtemplate（在searchtemplatelist.js中） </p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p> </td>
   <td><p>templateIcked-searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateList {#searchtemplatelist}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>tracking.html（在路由文件夹中）</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td><p>searchtemplate模型</p> </td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p> </td>
   <td><p>更改 — searchtemplatelist模型</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateDetails {#searchtemplatedetails}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>searchtemplatedetails.js</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>searchtemplatedetails.html</p> </td>
  </tr>
  <tr>
   <td><p>需要组件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td>NA<br /> </td>
  </tr>
  <tr>
   <td><p>侦听的事件（事件名称 — 触发器）</p> </td>
   <td><p>searchTemplate:selected - searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>
