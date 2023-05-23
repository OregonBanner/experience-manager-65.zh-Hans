---
title: 自訂處理序執行個體清單
seo-title: Customizing the listing of process instances
description: 如何自訂AEM Forms工作區中流程例項顯示的屬性。
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

# 自訂處理序執行個體清單 {#customizing-the-listing-of-process-instances}

流程例項清單會顯示在AEM Forms工作區的「追蹤」標籤中。

在程式執行個體清單中，AEM Forms工作區會針對每個程式執行個體顯示該執行個體的某些屬性。 下列屬性適用於每個程式執行個體。 這些屬性作為屬性儲存在流程例項元件模型中，並可用於其檢視和範本。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>说明</td>
   <td>程式執行個體的描述。</td>
  </tr>
  <tr>
   <td>發起人</td>
   <td>處理序執行個體的啟動器名稱。</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>處理序執行個體的發起者ID。</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>程式完成時的時間戳記。</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>程式執行個體的ID。</td>
  </tr>
  <tr>
   <td>processinstancestatus</td>
   <td>0 =已啟動<br /> 1 =執行中<br /> 2 =完成<br /> 3 =完成<br /> 4 =已終止<br /> 5 =終止<br /> 6 =已暫停<br /> 7 =暫停<br /> 8 =取消暫停</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>處理序的名稱。</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>程式啟動時的時間戳記。</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>程式變數的物件陣列。 每個處理序變數物件包含 <strong>名稱</strong> （程式變數的名稱）， <strong>值</strong> （程式變數的值），以及<strong> type</strong> （程式變數的型別）。</td>
  </tr>
 </tbody>
</table>

**示例:**

若要顯示 `description` 屬性（位於流程執行個體卡片中），請執行以下步驟。

1. 請遵循 [AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md).
1. 执行以下操作：

   1. 將/libs/ws/js/runtime/templates/processinstance.html複製到/apps/ws/js/runtime/templates/ （如果它不存在）。 按一下 **全部儲存**.
   1. 以class = &#39;processDescription&#39; inprocessinstance.html新增處理序描述div。

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 执行以下操作：

   1. 開啟/apps/ws/js/registry.js進行編輯。
   1. 搜尋和取代 `text!/lc/libs/ws/js/runtime/templates/processinstance.html`替換為 `text!/lc/`**應用程式**/ws/js/runtime/templates/processinstance.html.

1. 上述變更可能需要透過下列方式在樣式表/apps/ws/css/newStyle.css中新增專案，以更新CSS檔案：

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
