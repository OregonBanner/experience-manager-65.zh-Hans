---
title: 可重複使用元件的說明
seo-title: Description of reusable components
description: 包含檔案名稱和相依性之可重複使用元件的完整清單，可協助您在網頁應用程式中整合AEM Forms工作區元件。
seo-description: A complete list of reusable components with filenames and dependencies, to help you integrate AEM Forms workspace component in your web applications.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 9%

---

# 可重複使用元件的說明 {#description-of-reusable-components}

AEM Forms工作區由 [可重複使用](/help/forms/using/integrating-html-ws-components-web.md) 以特定方式組織的元件 [資料夾結構](/help/forms/using/folder-structure.md) 在CRX™中。 每個元件在資料夾結構中指定的位置都有模型、檢視和範本檔案、JavaScript™對其他元件檔案的相依性、元件偵聽的事件以及在AEM Forms工作區中觸發這些事件的JavaScript物件。 此處提供包含檔案名稱和相依性的可重複使用元件的完整清單。

## 任務清單 {#tasklist}

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
   <td><p>需要元件</p></td>
   <td>
    <ul>
     <li><p>UserSearch</p></li>
     <li><p>任务</p></li>
     <li><p>團隊任務</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>任務模型</p></li>
     <li><p>teamtask模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>filterSelected — 工作清單模型</p></li>
     <li><p>移除 — 工作清單模型</p></li>
     <li><p>updateQueue — 工作清單模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>若您從自訂應用程式中為此元件觸發filterSelected事件，則可獨立於AEM Forms工作區使用此元件。

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
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>工作清單模型</p></li>
     <li><p>工作動作公用程式</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>submitComplete — 任務模型</p></li>
     <li><p>拒絕 — 任務模型</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Workspace會呼叫TaskList模型的fetchTasks函式，以建立此元件的Task模型。

## 篩選清單 {#filterlist}

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
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>已擷取 — 工作清單模型 </p></li>
     <li><p>移除 — 工作清單模型 </p></li>
     <li><p>updateQueue — 工作清單模型 </p></li>
     <li><p>refreshedQueue — 工作清單模型 </p></li>
     <li><p>filterSelected — 工作清單模型</p></li>
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
   <td><p>需要元件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td>
    <ul>
     <li><p>欄位：佇列：{ name， qid， isDefault， type}</p> </li>
     <li><p>欄位：查詢：字串</p> </li>
     <li><p>欄位： parentView： filterlist view</p> </li>
     <li><p>欄位： parentModel：工作清單模型</p> </li>
     <li><p>欄位：公用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>聆聽的事件</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

## 團隊佇列 {#teamqueues}

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
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>已擷取 — 工作清單模型 </p></li>
     <li><p>移除 — 工作清單模型 </p></li>
     <li><p>updateQueue — 工作清單模型 </p></li>
     <li><p>teamQueuesFetched — 工作清單模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 團隊篩選 {#teamfilter}

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
   <td><p>需要元件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td>
    <ul>
     <li><p>延伸：篩選檢視</p> </li>
     <li><p>欄位：佇列：{ name， qid， isDefault， type }</p> </li>
     <li><p>欄位：查詢：字串</p> </li>
     <li><p>欄位：parentView ：篩選清單檢視</p> </li>
     <li><p>欄位：parentModel：工作清單模型</p> </li>
     <li><p>欄位：公用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>聆聽的事件</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter會取得事件，指出已從TaskList元件中選取哪個任務。 雖然這些元件共用模型類別，但沒有其他相依性。

## 任務詳細資訊 {#taskdetails}

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
   <td><p>需要元件</p> </td>
   <td><p>大部分的公用程式類別</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>表單演算公用程式</p> </li>
     <li><p>附註公用程式</p> </li>
     <li><p>附件公用程式</p> </li>
     <li><p>工作動作公用程式</p> </li>
     <li><p>歷程記錄公用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>已轉送 — 任務模型</p> </li>
     <li><p>共用 — 任務模型</p> </li>
     <li><p>已諮詢 — 任務模型</p> </li>
     <li><p>已拒絕 — 任務模型</p> </li>
     <li><p>已放棄 — 任務模型</p> </li>
     <li><p>unlocked — 任務模型</p> </li>
     <li><p>鎖定 — 任務模型</p> </li>
     <li><p>已申請 — 任務模型</p> </li>
     <li><p>變更：選取的工作 — 工作清單模型</p> </li>
     <li><p>變更：formUrl — 任務模型</p> </li>
     <li>attachmentURLFetched — 任務模型</li>
    </ul>
    <ul>
     <li>newAttachment — 任務模型</li>
     <li><p>taskHistoryFetched — 任務模型</p> </li>
     <li>prepareForSubmitComplete — 任務模型</li>
     <li><p>submitComplete — 任務模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 類別清單 {#categorylist}

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
   <td><p>startprocess.html （在路由資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>类别</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>favoritecategoryfactory模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched — 類別清單模型 </p></li>
     <li><p>新增 — 類別清單模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此元件使用某些其他元件的模型類別，例如StartPointList、StartPoint和Task。 除了此相依性之外，CategoryList也可獨立使用。

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
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>categorylist模型</p></li>
     <li><p>startpointlist模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>已變更 — 類別模型 </p></li>
     <li><p>childrenFetched — 類別模型 </p></li>
     <li><p>category：selected - categorylist model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## 起點清單 {#startpointlist}

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
   <td><p>startprocess.html （在路由資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>類別模型</p></li>
     <li><p>favoritecategoryfactory模型</p></li>
     <li><p>allcategoryfactory模型</p></li>
     <li><p>起點檢視</p></li>
     <li><p>startpointlist模型</p></li>
     <li><p>起點模型</p></li>
     <li><p>任務模型</p></li>
     <li><p>任務模型</p></li>
     <li><p>工作清單模型</p></li>
     <li><p>teamtask模型</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>category：selected - categorylist model </p></li>
     <li><p>allStartpointsFetched — 類別清單模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList和CategoryList元件共用模型類別，因此前者取決於後者。 CategoryList會存取顯示哪些類別起點的相關資訊。 若要獨立使用StartPointList，請從CategoryList模擬事件觸發程式。

## 起點 {#startpoint}

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
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>任務模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>變更 — 起點模型 </p></td>
  </tr>
 </tbody>
</table>

## Startprocess {#startprocess}

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
   <td><p>需要元件</p> </td>
   <td>
    <ul>
     <li><p>大部分的公用程式類別</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td>
    <ul>
     <li><p>類別模型</p> </li>
     <li><p>favoritecategoryfactory模型</p> </li>
     <li><p>allcategoryfactory模型</p> </li>
     <li><p>表單演算公用程式</p> </li>
     <li><p>附註公用程式</p> </li>
     <li><p>附件公用程式</p> </li>
     <li><p>工作動作公用程式</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>category：selected - categorylist model</p> </li>
     <li><p>change：invokedTask - startpointlist模型</p> </li>
     <li><p>變更：formUrl — 任務模型</p> </li>
     <li><p>起點：選取 — 起點清單模型</p> </li>
     <li><p>已轉送 — 任務模型</p> </li>
     <li><p>已放棄 — 任務模型</p> </li>
     <li><p>unlocked — 任務模型</p> </li>
     <li><p>鎖定 — 任務模型</p> </li>
     <li>attachmentURLFetched — 任務模型</li>
     <li>newAttachment — 任務模型</li>
     <li>prepareForSubmitComplete — 任務模型 </li>
     <li><p>submitComplete — 任務模型</p> </li>
     <li><p>allStartpointsFetched — 類別清單模型</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess和StartPointList元件共用模型類別。 當您從StartPointList選取起點時，此元件會變得相關。

## ProcessnameList {#processnamelist}

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
   <td><p>tracking.html （在路由資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>processname模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>新增 — 程式名稱清單模型 </p></li>
     <li><p>已擷取：processnames - processnamelist模型 </p></li>
     <li><p>變更 — 程式名稱清單模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList不依存於其他元件。 但是，它在內部依賴於ProcessInstanceList模型類別，而模型類別又依賴其他元件。 因此，ProcessNameList使用許多模型類別，例如ProcessInstanceList、ProcessInstance、TaskList、Teamtask和Task。 除了這些相依性之外，ProcessNameList也可以單獨使用。

## Processname {#processname}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
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
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>processinstancelist模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>變更 — processname model </p></td>
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
   <td><p>tracking.html （在路由資料夾中）</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>processname模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>processname：selected - processnamelist model </p></li>
     <li><p>processname：instancesfetched - processnamelist模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList預期來自ProcessNameList的事件，指出擷取和顯示執行個體的程式名稱。 若要單獨使用ProcessInstanceList，請個別模擬事件觸發程式。

## Processinstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>模型</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>查看</p></td>
   <td><p>processnamelist.js內的processname</p></td>
  </tr>
  <tr>
   <td><p>模板</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>工作清單模型</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>變更 — processinstance model </p></td>
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
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td>
    <ul>
     <li><p>processname模型</p></li>
     <li><p>歷程記錄公用程式</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>processname：selected - processnamelist model </p></li>
     <li><p>processinstance：selected - processinstancelist模型 </p></li>
     <li><p>tasksFetched - processinstance模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory預期來自ProcessInstanceList的事件，指出將顯示哪個程式執行個體的歷史記錄。 除了此相依性之外，元件也可獨立使用。

## 辦公室外 {#outofoffice}

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
   <td><p>需要元件</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>使用者搜尋檢視</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched — 辦公室模型</p> </li>
     <li><p>outOfOfficeSettingsSaved — 辦公室模型</p> </li>
     <li><p>processefetched — 辦公室模型</p> </li>
     <li><p>principalSelected - principalSearch檢視</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice可獨立使用。

## 共用佇列 {#sharequeue}

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
   <td><p>需要元件</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>使用者搜尋檢視</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted — 共用模型</p> </li>
     <li><p>queueAccessRequested — 共用模型</p> </li>
     <li><p>grantedUsersFetched — 共用模型</p> </li>
     <li>accessibleUsersFetched — 共用模型</li>
     <li><p>queueAccessRevoced — 共用模型</p> </li>
     <li><p>queueAccessRemoved — 共用模型</p> </li>
     <li><p>principalSelected - principalSearch檢視</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue可獨立使用。

## UIS設定 {#uisettings}

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
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td>
    <ul>
     <li><p>偏好設定已擷取 — 使用者設定模型 </p></li>
     <li><p>settingUpdated — 設定模型 </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings可獨立使用。

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
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>聆聽的事件</p></td>
   <td><p>NA</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation可單獨使用。

## 使用者資訊 {#userinfo}

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
   <td><p>需要元件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - userinfo模型</li>
     <li>sessionRevened — 使用者資訊模型 <br /> </li>
     <li>sessionExpired — 使用者資訊模型 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo可單獨使用。

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
   <td><p>需要元件</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>JS相依性</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p></td>
   <td><p>newWsError — 錯誤模型 </p></td>
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
   <td><p>需要元件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td>
    <ul>
     <li>principalSearch - principalsearch模型</li>
     <li>outOfOfficeInfoFetched — 使用者搜尋模型</li>
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
   <td><p>searchtemplate （在searchtemplatelist.js中） </p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td><p>templateFetched- searchtemplate模型</p> </td>
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
   <td><p>tracking.html （在路由資料夾中）</p> </td>
  </tr>
  <tr>
   <td><p>需要元件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td><p>searchtemplate model</p> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td><p>變更 — searchtemplatelist模型</p> </td>
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
   <td><p>需要元件</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>JS相依性</p> </td>
   <td>NA<br /> </td>
  </tr>
  <tr>
   <td><p>已監聽的事件（事件名稱 — 觸發器）</p> </td>
   <td><p>searchTemplate：selected - searchtemplate模型</p> </td>
  </tr>
 </tbody>
</table>
