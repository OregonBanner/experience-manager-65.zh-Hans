---
title: 可重用组件的描述
description: 包含文件名和依赖项的可重用组件的完整列表，可帮助您在Web应用程序中集成AEM Forms工作区组件。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 9%

---

# 可重用组件的描述 {#description-of-reusable-components}

AEM Forms工作区由 [可重用](/help/forms/using/integrating-html-ws-components-web.md) 以特定方式组织的组件 [文件夹结构](/help/forms/using/folder-structure.md) 在CRX™中。 每个组件在文件夹结构中指定的位置都有模型、视图和模板文件，JavaScript™依赖于其他组件文件、组件侦听的事件以及在AEM Forms工作区中触发这些事件的JavaScript对象。 此处提供了包含组成文件名和依赖关系的可重用组件的完整列表。

## 任务列表 {#tasklist}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
     <li><p>用户搜索</p></li>
     <li><p>任务</p></li>
     <li><p>团队任务</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>JS依赖项</p></td>
   <td>
    <ul>
     <li><p>任务模型</p></li>
     <li><p>团队任务模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>filterSelected — 任务列表模型</p></li>
     <li><p>移除 — 任务列表模型</p></li>
     <li><p>updateQueue — 任务列表模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此组件可以独立于AEM Forms Workspace使用，前提是您从自定义应用程序中为此组件触发filterSelected事件。

## 任务 {#task}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td>
    <ul>
     <li><p>任务列表模型</p></li>
     <li><p>任务操作实用程序</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
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
>工作区调用TaskList模型的fetchTasks函数以创建此组件的任务模型。

## 筛选列表 {#filterlist}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>已获取 — 任务列表模型 </p></li>
     <li><p>移除 — 任务列表模型 </p></li>
     <li><p>updateQueue — 任务列表模型 </p></li>
     <li><p>refreshedQueue — 任务列表模型 </p></li>
     <li><p>filterSelected — 任务列表模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 过滤器 {#filter}

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
   <td><p>JS依赖项</p> </td>
   <td>
    <ul>
     <li><p>字段： queue：{ name， qid， isDefault， type}</p> </li>
     <li><p>字段：查询：字符串</p> </li>
     <li><p>字段： parentView： filterlist view</p> </li>
     <li><p>字段： parentModel：任务列表模型</p> </li>
     <li><p>字段：实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已收听的事件</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

## 团队队列 {#teamqueues}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>已获取 — 任务列表模型 </p></li>
     <li><p>移除 — 任务列表模型 </p></li>
     <li><p>updateQueue — 任务列表模型 </p></li>
     <li><p>teamQueuesFetched — 任务列表模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 团队筛选器 {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>型号</p> </td>
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
   <td><p>JS依赖项</p> </td>
   <td>
    <ul>
     <li><p>扩展：过滤器视图</p> </li>
     <li><p>字段：queue ：{ name， qid， isDefault， type }</p> </li>
     <li><p>字段：查询：字符串</p> </li>
     <li><p>字段：parentView：filterlist view</p> </li>
     <li><p>字段：parentModel：任务列表模型</p> </li>
     <li><p>字段：实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已收听的事件</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter获取用于指示已从TaskList组件中选择哪个任务的事件。 尽管这些组件共享模型类，但并没有其他依赖关系。

## 任务详细信息 {#taskdetails}

<table>
 <tbody>
  <tr>
   <td><p>型号</p> </td>
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
   <td><p>大多数实用程序类</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖项</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>表单渲染实用程序</p> </li>
     <li><p>注释实用程序</p> </li>
     <li><p>附件实用程序</p> </li>
     <li><p>任务操作实用程序</p> </li>
     <li><p>历史记录实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li><p>转发 — 任务模型</p> </li>
     <li><p>共享 — 任务模型</p> </li>
     <li><p>已咨询 — 任务模型</p> </li>
     <li><p>已拒绝 — 任务模型</p> </li>
     <li><p>已放弃 — 任务模型</p> </li>
     <li><p>unlocked — 任务模型</p> </li>
     <li><p>已锁定 — 任务模型</p> </li>
     <li><p>已声明 — 任务模型</p> </li>
     <li><p>更改：已选择任务 — 任务列表模型</p> </li>
     <li><p>change：formUrl — 任务模型</p> </li>
     <li>attachmentURLFetched — 任务模型</li>
    </ul>
    <ul>
     <li>newAttachment — 任务模型</li>
     <li><p>taskHistoryFetched — 任务模型</p> </li>
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
   <td><p>型号</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>startprocess.html（在route文件夹中）</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>类别</p></td>
  </tr>
  <tr>
   <td><p>JS依赖项</p></td>
   <td>
    <ul>
     <li><p>favoritecategoryfactory模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched — 类别列表模型 </p></li>
     <li><p>添加 — 类别列表模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此组件使用某些其他组件（如StartPointList、StartPoint和Task）的模型类。 除了此依赖项之外，还可以单独使用CategoryList。

## 类别 {#category}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td>
    <ul>
     <li><p>类别列表模型</p></li>
     <li><p>startpointlist模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>已更改 — 类别模型 </p></li>
     <li><p>childrenFetched — 类别模型 </p></li>
     <li><p>类别：已选择 — 类别列表模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 起点列表 {#startpointlist}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>startpointlist.js</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>startprocess.html（在route文件夹中）</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖项</p></td>
   <td>
    <ul>
     <li><p>类别模型</p></li>
     <li><p>favoritecategoryfactory模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
     <li><p>起点</p></li>
     <li><p>startpointlist模型</p></li>
     <li><p>起点模型</p></li>
     <li><p>任务模型</p></li>
     <li><p>任务模型</p></li>
     <li><p>任务列表模型</p></li>
     <li><p>团队任务模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>类别：已选择 — 类别列表模型 </p></li>
     <li><p>allStartpointsFetched — 类别列表模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList和CategoryList组件共享模型类，因此前者依赖于后者。 CategoryList访问有关显示哪些类别起点的信息。 要单独使用StartPointList，请从CategoryList模拟事件触发器。

## 起点 {#startpoint}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td><p>任务模型</p></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td><p>更改 — 起点模型 </p></td>
  </tr>
 </tbody>
</table>

## 启动进程 {#startprocess}

<table>
 <tbody>
  <tr>
   <td><p>型号</p> </td>
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
     <li><p>大多数实用程序类</p> </li>
     <li><p>用户搜索</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JS依赖项</p> </td>
   <td>
    <ul>
     <li><p>类别模型</p> </li>
     <li><p>favoritecategoryfactory模型</p> </li>
     <li><p>allcategoryfactory模型</p> </li>
     <li><p>表单渲染实用程序</p> </li>
     <li><p>注释实用程序</p> </li>
     <li><p>附件实用程序</p> </li>
     <li><p>任务操作实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li><p>类别：已选择 — 类别列表模型</p> </li>
     <li><p>change：invocedTask - startpointlist模型</p> </li>
     <li><p>change：formUrl — 任务模型</p> </li>
     <li><p>起点：选定的 — 起点列表模型</p> </li>
     <li><p>转发 — 任务模型</p> </li>
     <li><p>已放弃 — 任务模型</p> </li>
     <li><p>unlocked — 任务模型</p> </li>
     <li><p>已锁定 — 任务模型</p> </li>
     <li>attachmentURLFetched — 任务模型</li>
     <li>newAttachment — 任务模型</li>
     <li>prepareForSubmitComplete — 任务模型 </li>
     <li><p>submitComplete — 任务模型</p> </li>
     <li><p>allStartpointsFetched — 类别列表模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess和StartPointList组件共享模型类。 从StartPointList中选择起点时，此组件将变得相关。

## 进程名称列表 {#processnamelist}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td><p>processname model</p></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist模型 </p></li>
     <li><p>fetched：processnames - processnamelist模型 </p></li>
     <li><p>更改 — 进程名称列表模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList不依赖于其他组件。 但是，它在内部依赖于ProcessInstanceList模型类，而模型类又依赖于其他组件。 因此，ProcessNameList使用许多模型类，如ProcessInstanceList、ProcessInstance、TaskList、Teamtask和Task。 除了这些依赖项之外，还可以单独使用ProcessNameList。

## 进程名称 {#processname}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>processname （在processnamelist.js中）</p></td>
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
   <td><p>JS依赖项</p></td>
   <td><p>processinstancelist模型</p></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td><p>更改 — processname model </p></td>
  </tr>
 </tbody>
</table>

## 进程实例列表 {#processinstancelist}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td><p>processname model</p></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>processname：selected - processnamelist模型 </p></li>
     <li><p>processname：instancesfetched - processnamelist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList需要ProcessNameList中的一个事件，该事件指示用于获取和显示实例的进程名称。 要单独使用ProcessInstanceList，请单独模拟事件触发器。

## 进程实例 {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td><p>任务列表模型</p></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td><p>更改 — processinstance model </p></td>
  </tr>
 </tbody>
</table>

## Processinstancehistory {#processinstancehistory}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td>
    <ul>
     <li><p>processname model</p></li>
     <li><p>历史记录实用程序</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>processname：selected - processnamelist模型 </p></li>
     <li><p>processinstance：selected - processinstancelist模型 </p></li>
     <li><p>tasksFetched - processinstance模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory需要ProcessInstanceList中的一个事件，用于指示将显示哪个进程实例的历史记录。 除此之外，还可以独立使用组件。

## 外出 {#outofoffice}

<table>
 <tbody>
  <tr>
   <td><p>型号</p> </td>
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
   <td><p>用户搜索</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖项</p> </td>
   <td><p>用户搜索视图</p> </td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched — 办公室模型</p> </li>
     <li><p>outOfOfficeSettingsSaved — 办公室外展模型</p> </li>
     <li><p>processesFetched - outoffice模型</p> </li>
     <li><p>principalSelected - principalsearch视图</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice可以独立使用。

## Sharequeue {#sharequeue}

<table>
 <tbody>
  <tr>
   <td><p>型号</p> </td>
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
   <td><p>用户搜索</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖项</p> </td>
   <td><p>用户搜索视图</p> </td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted — 共享模型</p> </li>
     <li><p>queueAccessRequested — 共享模型</p> </li>
     <li><p>grantedUsersFetched — 共享模型</p> </li>
     <li>accessibleUsersFetched — 共享模型</li>
     <li><p>queueAccessRevoced — 共享模型</p> </li>
     <li><p>queueAccessRemoved — 共享模型</p> </li>
     <li><p>principalSelected - principalsearch视图</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue可以单独使用。

## UIS设置 {#uisettings}

<table>
 <tbody>
  <tr>
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td>
    <ul>
     <li><p>preferencesFetched — 查询模型 </p></li>
     <li><p>settingUpdated — 用户设置模型 </p></li>
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
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>已收听的事件</p></td>
   <td><p>NA</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>可以单独使用AppNavigation。

## 用户信息 {#userinfo}

<table>
 <tbody>
  <tr>
   <td><p>型号</p> </td>
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
   <td><p>JS依赖项</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - userinfo模型</li>
     <li>sessionRevened - userinfo模型 <br /> </li>
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
   <td><p>型号</p></td>
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
   <td><p>JS依赖项</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p></td>
   <td><p>newWsError — 错误模型 </p></td>
  </tr>
 </tbody>
</table>

## 用户搜索 {#usersearch}

<table>
 <tbody>
  <tr>
   <td><p>型号</p> </td>
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
   <td><p>JS依赖项</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p> </td>
   <td>
    <ul>
     <li>principalSearch - principalsearch模型</li>
     <li>outOfOfficeInfoFetched — 用户搜索模型</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SearchTemplate {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>型号</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>searchtemplate （在searchtemplatelist.js中） </p> </td>
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
   <td><p>JS依赖项</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p> </td>
   <td><p>templateFetched — 搜索模板模型</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateList {#searchtemplatelist}

<table>
 <tbody>
  <tr>
   <td><p>型号</p> </td>
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
   <td><p>JS依赖项</p> </td>
   <td><p>搜索模板模型</p> </td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p> </td>
   <td><p>更改 — searchtemplatelist模型</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateDetails {#searchtemplatedetails}

<table>
 <tbody>
  <tr>
   <td><p>型号</p> </td>
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
   <td><p>JS依赖项</p> </td>
   <td>无<br /> </td>
  </tr>
  <tr>
   <td><p>事件已侦听（事件名称 — 触发器）</p> </td>
   <td><p>searchTemplate：selected - searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>
