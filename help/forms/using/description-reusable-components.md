---
title: 可重用组件的说明
seo-title: 可重用组件的说明
description: 可重用组件的完整列表（包含文件名和依赖关系），可帮助您将AEM Forms工作区组件集成到Web应用程序中。
seo-description: 可重用组件的完整列表（包含文件名和依赖关系），可帮助您将AEM Forms工作区组件集成到Web应用程序中。
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 可重用组件的说明 {#description-of-reusable-components}

AEM Forms工作区由可重用的组 [件组成](/help/forms/using/integrating-html-ws-components-web.md) ，这些组件在CRX [](/help/forms/using/folder-structure.md) ™中以特定的文件夹结构组织。 每个组件在文件夹结构中指定的位置都有模型、视图和模板文件，JavaScript™依赖于其他组件文件，组件监听的事件以及在AEM Forms工作区中触发这些事件的JavaScript对象。 此处提供了具有组成文件名和依赖关系的可重用组件的完整列表。

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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
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
>此组件可以独立于AEM Forms工作区使用，前提是您从自定义应用程序中为此组件触发filterSelected事件。

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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
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
>工作区调用TaskList模型的fetchTasks函数，以创建此组件的任务模型。

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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
   <td>
    <ul>
     <li><p>已获取——任务列表模型 </p></li>
     <li><p>删除——任务列表模型 </p></li>
     <li><p>updateQueue —— 任务列表模型 </p></li>
     <li><p>teamQueues已获取——任务列表模型 </p></li>
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
     <li><p>扩展：滤镜视图</p> </li>
     <li><p>字段：queue :{ name, qid, isDefault, type }</p> </li>
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
>TeamFilter获取指示已从TaskList组件中选择的任务的事件。 尽管这些组件共享模型类，但没有其他依赖关系。

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
     <li><p>历史记录实用程序</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件聆听(事件姓名——触发器)</p> </td>
   <td>
    <ul>
     <li><p>forwarded -任务模型</p> </li>
     <li><p>共享-任务模型</p> </li>
     <li><p>已咨询-任务模型</p> </li>
     <li><p>拒绝-任务模型</p> </li>
     <li><p>废弃-任务模式</p> </li>
     <li><p>已解锁-任务模型</p> </li>
     <li><p>锁定-任务模型</p> </li>
     <li><p>索赔-任务模型</p> </li>
     <li><p>更改：选定任务——任务列表模型</p> </li>
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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
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
>此组件使用某些其他组件的模型类，如StartPointList、StartPoint和任务。 除此依赖关系外，CategoryList还可以单独使用。

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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
   <td>
    <ul>
     <li><p>更改-类别模型 </p></li>
     <li><p>childrenIchated -类别模型 </p></li>
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
     <li><p>起始点视图</p></li>
     <li><p>startpointlist模型</p></li>
     <li><p>起点模型</p></li>
     <li><p>任务模型</p></li>
     <li><p>任务模型</p></li>
     <li><p>任务列表模型</p></li>
     <li><p>团队任务模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件聆听(事件姓名——触发器)</p></td>
   <td>
    <ul>
     <li><p>类别：选定——类别列表模型 </p></li>
     <li><p>allStartpointsIcated - categorylist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList和CategoryList组件共享模型类，因此前者取决于后者。 CategoryList访问显示哪个类别开始点的相关信息。 要单独使用StartPointList，请模拟CategoryList中的事件触发器。

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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
   <td><p>change-startpoint模型 </p></td>
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
   <td><p>事件聆听(事件姓名——触发器)</p> </td>
   <td>
    <ul>
     <li><p>类别：选定——类别列表模型</p> </li>
     <li><p>change:invokedTask - startpointlist模型</p> </li>
     <li><p>change:formUrl -任务模型</p> </li>
     <li><p>起点：选定——起点列表模型</p> </li>
     <li><p>forwarded -任务模型</p> </li>
     <li><p>废弃-任务模式</p> </li>
     <li><p>已解锁-任务模型</p> </li>
     <li><p>锁定-任务模型</p> </li>
     <li>attachmentURLFechetd -任务模型</li>
     <li>newAttachment -任务模型</li>
     <li>prepareForSubmitComplete -任务模型 </li>
     <li><p>submitComplete -任务模型</p> </li>
     <li><p>allStartpointsIcated - categorylist模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess和StartPointList组件共享模型类。 此组件变得相关，您可以从StartPointList中选择一个起点。

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
   <td><p>进程名模型</p></td>
  </tr>
  <tr>
   <td><p>事件聆听(事件姓名——触发器)</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist model </p></li>
     <li><p>获取的：进程名称——进程名称列表模型 </p></li>
     <li><p>change - processnamelist model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList不依赖于其他组件。 但是，它在内部取决于ProcessInstanceList模型类，而ProcessInstanceList模型类又取决于其他组件。 因此，ProcessNameList使用许多模型类，如ProcessInstanceList、ProcessInstance、TaskList、Teamtask和任务。 除了这些依赖关系外，ProcessNameList还可以单独使用。

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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
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
   <td><p>进程名模型</p></td>
  </tr>
  <tr>
   <td><p>事件聆听(事件姓名——触发器)</p></td>
   <td>
    <ul>
     <li><p>进程名称：选定——进程名称列表模型 </p></li>
     <li><p>进程名称：获取的实例——进程名列表模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList需要ProcessNameList中的事件，用于指示用于获取和显示实例的进程名。 要单独使用ProcessInstanceList，请单独模拟事件触发器。

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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
   <td><p>change-processinstance模型 </p></td>
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
     <li><p>进程名模型</p></li>
     <li><p>历史记录实用程序</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>事件聆听(事件姓名——触发器)</p></td>
   <td>
    <ul>
     <li><p>进程名称：选定——进程名称列表模型 </p></li>
     <li><p>进程实例：选定——进程实例列表模型 </p></li>
     <li><p>tasks获取的——进程实例模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory需要ProcessInstanceList中的事件，指示将显示哪个进程实例的历史记录。 除此依赖关系外，该组件还可以单独使用。

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
   <td><p>事件聆听(事件姓名——触发器)</p> </td>
   <td>
    <ul>
     <li><p>outOfficeSettingsIchated - outfofice模型</p> </li>
     <li><p>outOfficeSettingsSaved - outofice模型</p> </li>
     <li><p>processesIchated - outofice模型</p> </li>
     <li><p>principalSelected —— 主要搜索视图</p> </li>
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
   <td><p>事件聆听(事件姓名——触发器)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - sharequeue模型</p> </li>
     <li><p>queueAccessRequested - sharequeue模型</p> </li>
     <li><p>grantedUsersReached - sharequeue模型</p> </li>
     <li>accessibleUsersIchated - sharequeue模型</li>
     <li><p>queueAccessRevoded - sharequeue模型</p> </li>
     <li><p>queueAccessRemoved —— 共享队列模型</p> </li>
     <li><p>principalSelected —— 主要搜索视图</p> </li>
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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
   <td>
    <ul>
     <li><p>preferences获取的——提交模型 </p></li>
     <li><p>settingUpdated - uisettings模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings可单独使用。

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

## 用户信息 {#userinfo}

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
   <td><p>事件聆听(事件姓名——触发器)</p> </td>
   <td>
    <ul>
     <li>userImageUrlIchated - userinfo模型</li>
     <li>sessionRenewed - userinfo模型 <br /> </li>
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
   <td><p>事件聆听(事件姓名——触发器)</p></td>
   <td><p>newWsError —— 错误模型 </p></td>
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
   <td><p>事件聆听(事件姓名——触发器)</p> </td>
   <td>
    <ul>
     <li>principalSearched - principalsearch模型</li>
     <li>outOfOfficeInfoIched —— 用户搜索模型</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 搜索模板 {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>模型</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>查看</p> </td>
   <td><p>search模板（在searchtemplatelist.js中） </p> </td>
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
   <td><p>事件聆听(事件姓名——触发器)</p> </td>
   <td><p>templateRechated- search模板模型</p> </td>
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
   <td><p>search模板模型</p> </td>
  </tr>
  <tr>
   <td><p>事件聆听(事件姓名——触发器)</p> </td>
   <td><p>change - searchtemplatelist模型</p> </td>
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
   <td><p>事件聆听(事件姓名——触发器)</p> </td>
   <td><p>searchTemplate:selected - searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>
