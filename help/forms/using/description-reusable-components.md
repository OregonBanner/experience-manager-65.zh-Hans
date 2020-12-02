---
title: 可重用组件的描述
seo-title: 可重用组件的描述
description: 包含文件名和依赖项的可重复使用组件的完整列表，可帮助您将AEM Forms工作区组件集成到您的Web应用程序中。
seo-description: 包含文件名和依赖项的可重复使用组件的完整列表，可帮助您将AEM Forms工作区组件集成到您的Web应用程序中。
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 9%

---


# 可重用组件{#description-of-reusable-components}的说明

AEM Forms工作区由[可重用](/help/forms/using/integrating-html-ws-components-web.md)组件组成，这些组件在CRX™中以特定的[文件夹结构](/help/forms/using/folder-structure.md)组织。 每个组件在文件夹结构中指定的位置都有模型、视图和模板文件，JavaScript™依赖于其他组件文件，组件监听的事件以及在AEM Forms工作区触发这些事件的JavaScript对象。 此处提供具有组成文件名和相关性的可重用组件的完整列表。

## TaskList {#tasklist}

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
     <li><p>用户搜索</p></li>
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
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>filterSelected —— 任务列表模型</p></li>
     <li><p>删除——任务列表模型</p></li>
     <li><p>updateQueue —— 任务列表模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>只要您从自定义应用程序为此组件触发filterSelected事件，此组件可以独立于AEM Forms工作区使用。

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
     <li><p>任务操作实用程序</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>submitComplete -任务模型</p></li>
     <li><p>拒绝-任务模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>工作区调用TaskList模型的fetchTasks函数，为此组件创建任务模型。

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
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>已获取——任务列表模型 </p></li>
     <li><p>删除——任务列表模型 </p></li>
     <li><p>updateQueue —— 任务列表模型 </p></li>
     <li><p>refreshedQueue —— 任务列表模型 </p></li>
     <li><p>filterSelected —— 任务列表模型</p></li>
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
     <li><p>字段：队列：{ name, qid, isDefault, type}</p> </li>
     <li><p>字段：查询:字符串</p> </li>
     <li><p>字段：parentView:过滤器列表视图</p> </li>
     <li><p>字段：parentModel:任务列表模型</p> </li>
     <li><p>字段：实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件聆听</p> </td>
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
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>已获取——任务列表模型 </p></li>
     <li><p>删除——任务列表模型 </p></li>
     <li><p>updateQueue —— 任务列表模型 </p></li>
     <li><p>teamQueuesReched —— 任务列表模型 </p></li>
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
     <li><p>扩展：过滤器视图</p> </li>
     <li><p>字段：队列：{ name, qid, isDefault, type }</p> </li>
     <li><p>字段：查询:字符串</p> </li>
     <li><p>字段：parentView:过滤器列表视图</p> </li>
     <li><p>字段：parentModel:任务列表模型</p> </li>
     <li><p>字段：实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件聆听</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter获取指示已从TaskList组件中选择哪个任务的事件。 尽管这些组件共享模型类，但没有其他依赖关系。

## TaskDetails {#taskdetails}

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
   <td><p>大多数实用程序类</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>formrendering实用程序</p> </li>
     <li><p>注释实用程序</p> </li>
     <li><p>附件实用程序</p> </li>
     <li><p>任务操作实用程序</p> </li>
     <li><p>历史实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p> </td>
   <td>
    <ul>
     <li><p>forwarded -任务模型</p> </li>
     <li><p>共享-任务模型</p> </li>
     <li><p>已咨询-任务模型</p> </li>
     <li><p>拒绝-任务模型</p> </li>
     <li><p>废弃-任务模型</p> </li>
     <li><p>已解锁-任务模型</p> </li>
     <li><p>锁定-任务模型</p> </li>
     <li><p>索赔-任务模型</p> </li>
     <li><p>更改：已选定任务——任务列表模型</p> </li>
     <li><p>change:formUrl -任务模型</p> </li>
     <li>attachmentURLFechetd -任务模型</li>
    </ul>
    <ul>
     <li>newAttachment -任务模型</li>
     <li><p>taskHistoryRecated -任务模型</p> </li>
     <li>prepareForSubmitComplete -任务模型</li>
     <li><p>submitComplete -任务模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## CategoryList {#categorylist}

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
   <td><p>startprocess.html（在route文件夹中）</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>类别</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td>
    <ul>
     <li><p>favoritecategoryfactory模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsRecited - categorylist模型 </p></li>
     <li><p>add - categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此组件使用一些其他组件(如StartPointList、StartPoint和任务)的模型类。 除此依赖关系外，CategoryList还可以单独使用。

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
     <li><p>categorylist模型</p></li>
     <li><p>startpointlist模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>更改-类别模型 </p></li>
     <li><p>childrenRected -类别模型 </p></li>
     <li><p>类别：选定——类别列表模型 </p></li>
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
   <td><p>startprocess.html（在route文件夹中）</p></td>
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
     <li><p>favoritecategoryfactory模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
     <li><p>起点视图</p></li>
     <li><p>startpointlist模型</p></li>
     <li><p>起点模型</p></li>
     <li><p>任务模型</p></li>
     <li><p>任务模型</p></li>
     <li><p>任务列表模型</p></li>
     <li><p>团队任务模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>类别：选定——类别列表模型 </p></li>
     <li><p>allStartpointsRecited - categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList和CategoryList组件共享模型类，因此前者取决于后者。 CategoryList访问显示类别开始点的相关信息。 要单独使用StartPointList，请模拟CategoryList中的事件触发器。

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
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td><p>更改——起始点模型 </p></td>
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
     <li><p>大多数实用程序类</p> </li>
     <li><p>用户搜索</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td>
    <ul>
     <li><p>类别模型</p> </li>
     <li><p>favoritecategoryfactory模型</p> </li>
     <li><p>allcategoryfactory模型</p> </li>
     <li><p>formrendering实用程序</p> </li>
     <li><p>注释实用程序</p> </li>
     <li><p>附件实用程序</p> </li>
     <li><p>任务操作实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p> </td>
   <td>
    <ul>
     <li><p>类别：选定——类别列表模型</p> </li>
     <li><p>change:invocedTask - startpointlist模型</p> </li>
     <li><p>change:formUrl -任务模型</p> </li>
     <li><p>起点：已选——起始点列表模型</p> </li>
     <li><p>forwarded -任务模型</p> </li>
     <li><p>废弃-任务模型</p> </li>
     <li><p>已解锁-任务模型</p> </li>
     <li><p>锁定-任务模型</p> </li>
     <li>attachmentURLFechetd -任务模型</li>
     <li>newAttachment -任务模型</li>
     <li>prepareForSubmitComplete -任务模型 </li>
     <li><p>submitComplete -任务模型</p> </li>
     <li><p>allStartpointsRecited - categorylist模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess和StartPointList组件共享模型类。 此组件变得相关，您从StartPointList中选择一个起点。

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
   <td><p>tracking.html（在route文件夹中）</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>processname模型</p></td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>添加——进程名列表模型 </p></li>
     <li><p>已提取：进程名称——进程名列表模型 </p></li>
     <li><p>更改——进程名列表模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList不依赖于其他组件。 但是，在内部它取决于ProcessInstanceList模型类，而ProcessInstanceList模型类又取决于其他组件。 因此，ProcessNameList使用许多模型类，如ProcessInstanceList、ProcessInstance、TaskList、Teamtask和任务。 除了这些依赖关系外，ProcessNameList还可以单独使用。

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
   <td><p>processinstancelist模型</p></td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td><p>change - processname模型 </p></td>
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
   <td><p>tracking.html（在route文件夹中）</p></td>
  </tr>
  <tr>
   <td><p>需要组件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p></td>
   <td><p>processname模型</p></td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>processname:selected - processnamelist模型 </p></li>
     <li><p>进程名称：已获取实例——进程名列表模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList需要ProcessNameList中的事件，用于指示用于读取和显示实例的进程名称。 要单独使用ProcessInstanceList，请单独模拟事件触发器。

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>processnamelist.js中的进程名</p></td>
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
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td><p>change - processinstance模型 </p></td>
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
     <li><p>processname模型</p></li>
     <li><p>历史实用程序</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>processname:selected - processnamelist模型 </p></li>
     <li><p>processinstance:selected - processinstancelist模型 </p></li>
     <li><p>tasksReacted - processinstance模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory需要ProcessInstanceList中的事件，指示将显示哪个进程实例的历史记录。 除此依赖关系外，组件还可以单独使用。

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
   <td><p>用户搜索</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td><p>用户搜索视图</p> </td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p> </td>
   <td>
    <ul>
     <li><p>outOfficeSettingsIchated - outoffice模型</p> </li>
     <li><p>outOfficeSettingsSaved - outofice模型</p> </li>
     <li><p>processesRiched - outofice模型</p> </li>
     <li><p>principalSelected —— 主搜索视图</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice可单独使用。

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
   <td><p>用户搜索</p> </td>
  </tr>
  <tr>
   <td><p>JS依赖关系</p> </td>
   <td><p>用户搜索视图</p> </td>
  </tr>
  <tr>
   <td><p>事件听取(事件名称——触发器)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGrated - sharequeue模型</p> </li>
     <li><p>queueAccessRequested - sharequeue模型</p> </li>
     <li><p>grantedUsersRected - sharequeue模型</p> </li>
     <li>accessibleUsersReached - sharequeue模型</li>
     <li><p>queueAccessRevoded - sharequeue模型</p> </li>
     <li><p>queueAccessRemoved - sharequeue模型</p> </li>
     <li><p>principalSelected —— 主搜索视图</p> </li>
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
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td>
    <ul>
     <li><p>preferencesRecated —— 怀疑模型 </p></li>
     <li><p>settingUpdated - uisetings模型 </p></li>
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
   <td><p>事件聆听</p></td>
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
   <td><p>事件听取(事件名称——触发器)</p> </td>
   <td>
    <ul>
     <li>userImageUrlRected - userinfo模型</li>
     <li>sessionRextended - userinfo model <br /> </li>
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
   <td><p>事件听取(事件名称——触发器)</p></td>
   <td><p>newWsError - wserror模型 </p></td>
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
   <td><p>事件听取(事件名称——触发器)</p> </td>
   <td>
    <ul>
     <li>principalSearchd - principalsearch模型</li>
     <li>outOfOfficeInfoIched —— 用户搜索模型</li>
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
   <td><p>事件听取(事件名称——触发器)</p> </td>
   <td><p>templateReched- search模板模型</p> </td>
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
   <td><p>tracking.html（在route文件夹中）</p> </td>
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
   <td><p>事件听取(事件名称——触发器)</p> </td>
   <td><p>更改-searchtemplatelist模型</p> </td>
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
   <td><p>事件听取(事件名称——触发器)</p> </td>
   <td><p>searchTemplate:selected - searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>
