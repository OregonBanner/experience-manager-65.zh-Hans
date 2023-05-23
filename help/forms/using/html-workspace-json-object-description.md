---
title: AEM Forms工作區JSON物件說明
seo-title: AEM Forms workspace JSON object description
description: LiveCycleAEM Forms工作區中使用的JSON JavaScript物件的相關概念資訊，用於自訂、擴充功能、修改和重複使用。
seo-description: Conceptual information about the JSON JavaScript objects used in LiveCycle AEM Forms workspace for customization, extension, modification, and reuse.
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2109'
ht-degree: 2%

---

# AEM Forms工作區JSON物件說明 {#aem-forms-workspace-json-object-description}

AEM Forms工作區中使用的JSON物件說明如下。

1. 类别

   類別會顯示在工作區的啟動流程標籤中。 這些類別可用來分類起點。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>name</td>
   <td>F</td>
   <td>類別名稱</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>類別ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>说明<br type="_moz" /> </td>
   <td>F</td>
   <td>類別說明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentoid<br type="_moz" /> </td>
   <td>F</td>
   <td>包含父類別的oid<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>起始點清單<br type="_moz" /> </td>
   <td>T</td>
   <td>包含類別中存在的所有起點的清單</td>
  </tr>
  <tr>
   <td>categorylist</td>
   <td>T</td>
   <td>包含類別的直接子類別清單<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>所有「起點」和「我的最愛」是在使用者端上定義的類別。 我的最愛類別包含使用者標示為我的最愛的所有起點。 「所有起點」類別包含所有起點。

1. 起點

   叫用時可使用起點從工作區啟動程式。

   | **属性** | **僅限使用者端** | **评论** |
   |---|---|---|
   | categoryId | F | 它包含起點所屬類別的ID。 |
   | 说明 | F | 它包含起點的說明。 |
   | name | F | 它包含起點的名稱。 |
   | serializedImageTicket | F | 它包含與起點對應的影像票證。 此影像票證用於起點的imageUrl欄位中，以從伺服器取得起點的影像。 |
   | serviceName | F | 它包含起點的服務名稱。 |
   | startpointId | F | 它包含起點ID。 |
   | isFavorite | T | 表示起點是否為我的最愛。 如果起點為最愛，則為True，否則為False。 |
   | isDefaultImage | T | 表示是否有為處理指定的影像。 如果沒有與處理程式相關聯的影像，則為True，否則為false。 |
   | 任務 | T | 它包含在叫用起點時建立的任務。 |
   | imageUrl | T | 它包含與起點對應的影像URL。 |

1. 任务

   任務會指派給使用者/群組，並包含可填入資料的使用者介面 — 表單或指南（已棄用）。 當使用者被指派任務時，他們將會獲得完成和提交的表單或指南。

<table>
 <tbody>
  <tr>
   <td>属性<br /> </td>
   <td>僅限使用者端<br /> </td>
   <td>评论<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>當任務為lc8任務時，任務類別為「LC8」，否則為「標準」。<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>它包含任務完成時的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>它包含可向其諮詢任務的群組ID。 它在流程設計期間設定。<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>其中包含建立任務時的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>F</td>
   <td>它包含建立任務的使用者ID。<br /> </td>
  </tr>
  <tr>
   <td>目前指定任務<br /> </td>
   <td>F</td>
   <td>它包含有關目前任務指派的詳細資訊。<br /> </td>
  </tr>
  <tr>
   <td>期限<br /> </td>
   <td>F</td>
   <td>其中包含任務到達截止日期的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>说明<br /> </td>
   <td>F</td>
   <td>它包含任務的說明。<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>它包含任務的顯示名稱。<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>它包含任務可轉送到的群組ID。 它在流程設計期間設定。<br /> </td>
  </tr>
  <tr>
   <td>指示<br /> </td>
   <td>F</td>
   <td>它包含任務的指示。<br /> </td>
  </tr>
  <tr>
   <td>islocked<br /> </td>
   <td>F</td>
   <td>如果任務已鎖定，則為True。<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>如果必須開啟工作表單才能完成工作，則為True。<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>如果為true，則開啟任務時，表單會首次完成畫面。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>如果為true，則必須選取路由以完成任務。<br /> </td>
  </tr>
  <tr>
   <td>isshowAttachments<br /> </td>
   <td>F</td>
   <td>如果為true，則會顯示附件。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>如果為true，則從起始點建立任務。<br /> </td>
  </tr>
  <tr>
   <td>isvisible<br /> </td>
   <td>F</td>
   <td>如果任務顯示在工作區中，則為True。<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>下一個提醒的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>优先级<br /> </td>
   <td>F</td>
   <td>它包含任務的優先順序。<br /> 1 =最高優先順序<br /> 2 =高優先順序<br /> 3 =一般優先順序<br /> 4 =低優先順序<br /> 5 =最低優先順序<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>工作所屬之程式例項的ID。<br /> </td>
  </tr>
  <tr>
   <td>processinstancestatus<br /> </td>
   <td>F</td>
   <td>任務的程式執行個體的狀態。<br /> </td>
  </tr>
  <tr>
   <td>remindentcount<br /> </td>
   <td>F</td>
   <td>它包含任務的提醒計數。<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>它包含與任務相關的路由清單。 使用者可以從路由清單中選取任一路由，以完成任務。<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>它包含任務完成時選取的路由名稱。<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>它包含與任務對應的影像票證。 此影像票證用於任務的imageUrl欄位中，用於從伺服器取得任務的影像。<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>它包含任務的服務名稱。<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>它包含任務的服務標題。<br /> </td>
  </tr>
  <tr>
   <td>状态<br /> </td>
   <td>F</td>
   <td>1 =已建立（從起點建立任務。）<br /> 2 =建立與儲存（從起點建立並儲存任務）。<br /> 3 =已指派（任務在程式啟動後指派給使用者。）<br /> 4 =指派和儲存（指派和儲存任務）。<br /> 100 =已完成（任務已完成。）<br /> 101 =已截止（任務已達到截止日期）。<br /> 102 =已終止<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>它包含流程設計期間的工作集名稱。<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>它包含任務摘要url。<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>它是任務的存取控制清單。<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>任務的ID。<br /> </td>
  </tr>
  <tr>
   <td>updatetime<br /> </td>
   <td>F</td>
   <td>上次更新任務的時間戳記。<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>它包含任務的表單url。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>它包含任務表單型別。 使用此欄位，任務會在使用者端上呈現為pdf、swf表單等。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>如果為true，則可在工作區中看到路由動作。<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>如果為true，則工作區中會顯示前進、諮詢、共用等動作。<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>如果為true，則可將表單離線。 這僅適用於pdf表單。<br /> </td>
  </tr>
  <tr>
   <td>supportssave<br /> </td>
   <td>T</td>
   <td>如果為true，則使用者可以儲存任務。<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>此物件包含用於透過Reader提交PDF表單的選項，以防PDF表單不包含提交按鈕。<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>表示是否有為處理指定的影像。 如果沒有與處理程式相關聯的影像，則為True，否則為false。<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>它包含在任務詳細資訊的歷史記錄標籤中使用的任務清單。<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>如果登入的使用者是任務的擁有者，則為真。<br /> </td>
  </tr>
  <tr>
   <td>availableCommand<br /> </td>
   <td>T</td>
   <td>其中包含可對任務執行的所有動作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>它包含任務可用的所有路由動作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>它包含forward、share和consult等命令（如果可用於任務）。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>它包含鎖定、解鎖、放棄、返回、宣告等可用命令。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>它包含有關任務的程式執行個體的資訊。<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>它包含流程變數的物件陣列（如果存在）。<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>它包含任務之程式執行個體的擱置任務清單。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>它是物件的陣列。 每個物件都包含有關路由的詳細資訊及其對應的確認訊息（如果存在）。<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>它是任務表單資料的url。<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>這是協力廠商應用程式表單的設定。<br /> </td>
  </tr>
  <tr>
   <td>已提交<br /> </td>
   <td>T</td>
   <td>如果任務已提交，則為真。<br /> </td>
  </tr>
  <tr>
   <td>附件<br /> </td>
   <td>T</td>
   <td>工作的附件清單。<br /> </td>
  </tr>
  <tr>
   <td>个指定任务<br /> </td>
   <td>T</td>
   <td>任務的指派清單。<br /> </td>
  </tr>
 </tbody>
</table>

1. 过滤器

   篩選器基本上是使用者或群組的佇列。 當任務指派給使用者/群組時，任務會新增到對應的佇列中。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>如果佇列是登入使用者的預設佇列，則為True，否則為false。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>name<br type="_moz" /> </td>
   <td>F</td>
   <td>佇列擁有者的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>佇列的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>类型</td>
   <td>F</td>
   <td>它包含佇列的型別。<br /> 0 — 使用者佇列。<br /> 1. 共用佇列。<br /> 2. 群組佇列。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>T</td>
   <td>這包含與篩選器相關聯的查詢。 此查詢用於從完整工作清單中搜尋工作。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任務</td>
   <td>T</td>
   <td>它包含屬於篩選器的所有任務清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 郵件答錄機

   您可以管理您的休假排程，並控制您休假時指派給您的任務流程。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong><br type="_moz" /> </td>
   <td><strong>僅限使用者端</strong><br type="_moz" /> </td>
   <td><strong>评论</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含使用者休假排程的陣列物件。 在每個排程物件中，startDate欄位包含排程的開始日期，而dendDate欄位包含排程的結束日期。 如果排程中的endDate為Null，則表示使用者尚未排程休假排程的結束日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesigned<br type="_moz" /> </td>
   <td>F</td>
   <td>如果使用者不在辦公室，則沒有主要指定，則為True。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果使用者不在辦公室，則為真。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含使用者指派為主要指定的使用者的詳細資訊。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含用於特定程式的「不在辦公室」指定的物件陣列。 在每個流程特定的指定物件中，processName包含流程的名稱，如果沒有指派使用者給對應的流程，則isNotDesigned為true，如果沒有指派使用者給對應的流程，則userDesigned為null。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>程式<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含使用者可用的所有程式清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含最初擷取之使用者的初始休假設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含修改過的「不在辦公室」設定。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含截至目前登入使用者所搜尋的使用者清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 程式執行個體

   透過工作區或工作台叫用程式時，會建立程式執行個體。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>说明<br type="_moz" /> </td>
   <td>F</td>
   <td>程式執行個體的描述<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>發起人</td>
   <td>F</td>
   <td>程式執行個體的發起人名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>處理序執行個體的啟動器識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>處理完成時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>程式執行個體的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processinstancestatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =已啟動<br /> 1 =執行中<br /> 2 =完成<br /> 3 =完成<br /> 4 =已終止<br /> 5 =終止<br /> 6 =已暫停<br /> 7 =暫停<br /> 8 =取消暫停<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>處理序的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>程式啟動時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>程式變數的物件陣列。 每個流程變數物件包含名稱（流程變數的名稱）、值（流程變數的值）和型別（流程變數的型別）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>工作清單<br type="_moz" /> </td>
   <td>T</td>
   <td>此程式執行個體產生的任務。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 进程名称

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>程式的主要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>程式的次要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>處理序的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>程式標題。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>此程式的程式執行個體清單。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任務指派物件

   任務指派物件包含有關任務指派的資訊。 以下是任務指派的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>assignmentcreatetime<br type="_moz" /> </td>
   <td>F</td>
   <td>建立此任務指派時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmenttype<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =初始指派<br /> 1 =轉寄（任務已轉寄給任務的目前所有者。）<br /> 2 =返回（任務已由任務的先前所有者返回給任務的目前所有者。）<br /> 3 =已申請（任務已由任務的目前所有者申請）。<br /> 4 =提升（提升後任務已指派給任務的目前擁有者。）<br /> 5 =管理員已指派（任務已由管理員指派給任務的目前擁有者。）<br /> 6 =已諮詢（已諮詢任務給任務的目前所有者。）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentupdatetime<br type="_moz" /> </td>
   <td>F</td>
   <td>更新此任務指派時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>任務目前擁有者的佇列識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwer<br type="_moz" /> </td>
   <td>F</td>
   <td>任務目前擁有者的名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>任務目前擁有者的ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任務ACL物件

   任務ACL物件包含有關轉送、共用、諮詢等許可權的資訊。 任務的。 以下是工作ACL的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可新增附件至工作。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可將附註新增至任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可宣告任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可參閱任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可轉送任務。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則可共用任務。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任務附件

   附件可新增至任務。 附件可以是附件和附註型別。 以下是附件物件的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>建立附件時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>已新增附件的使用者ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>新增附件的使用者名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>说明<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的說明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>檔案名稱<br type="_moz" /> </td>
   <td>F</td>
   <td>附件名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>上次修改附件時的時間戳記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>附註擴展<br type="_moz" /> </td>
   <td>F</td>
   <td>如果為true，則附註為延伸（長）附註。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>許可權<br type="_moz" /> </td>
   <td>F</td>
   <td>與附件相關聯的許可權。 allowRead欄位用於讀取許可權，allowWrite用於寫入許可權，allowDelete用於刪除許可權。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>大小<br type="_moz" /> </td>
   <td>F</td>
   <td>附件大小（位元組）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>要新增附件的任務識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>类型<br type="_moz" /> </td>
   <td>F</td>
   <td>型別是檔案的附件，型別是註記的註記。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>根據使用者的UI設定，其中包含附件建立日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化的附件說明。 用於顯示AEM Forms工作區附件說明中出現的特殊字元。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化的附件名稱。 用於顯示AEM Forms工作區附件名稱中出現的特殊字元。 這僅供附註使用。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 用户

   以下是使用者物件的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>僅限使用者端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>地址<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的位址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的通用名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>说明<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的說明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMembershies<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者群組的清單。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的顯示名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的電子郵件識別碼。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果使用者不在辦公室，則為真。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>姓氏<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的姓氏。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>名字<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的名字。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的組織名稱。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>郵寄地址<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的郵寄地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>电话<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的聯絡電話。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephonnumber<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的聯絡電話。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>使用者的登入識別碼。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
