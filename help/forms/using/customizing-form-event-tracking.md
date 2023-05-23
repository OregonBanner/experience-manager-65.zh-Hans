---
title: 自訂表單事件追蹤
seo-title: Customizing form event tracking
description: 如果使用者在欄位上花費超過60秒，則會觸發欄位瀏覽事件，並將欄位的詳細資訊傳送到Adobe SiteCatalyst。
seo-description: If a user spends more than 60 seconds on a field, a fieldvisit event is triggered and the details of the field are sent to Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# 自訂表單事件追蹤 {#customizing-form-event-tracking}

下列現成事件會在啟用Analytics的最適化表單中受到追蹤：

<table>
 <tbody>
  <tr>
   <th>Event</th>
   <th>可用變數</th>
  </tr>
  <tr>
   <td>轉譯</td>
   <td>formName， formTitle， formInstance， source</td>
  </tr>
  <tr>
   <td>捨棄</td>
   <td>formName、formTitle、formInstance、panelName、panelTitle</td>
  </tr>
  <tr>
   <td>保存</td>
   <td>formName， formTitle， formInstance， panelName， source</td>
  </tr>
  <tr>
   <td>提交</td>
   <td>formName， formTitle， formInstance， source</td>
  </tr>
  <tr>
   <td>错误</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle</td>
  </tr>
  <tr>
   <td>帮助</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName、formTitle、panelName、panelTitle</td>
  </tr>
 </tbody>
</table>

## 自訂欄位造訪事件逾時 {#customizing-the-field-visit-event-timeout}

在預設AEM表單設定中，如果使用者在欄位上花費超過60秒，則 `fieldvisit` 事件會觸發，而欄位的詳細資料會傳送至Adobe Analytics。 您可以在AEM設定控制檯(/system/console/configMgr)的AEM Forms Analytics設定下自訂欄位時間追蹤基準線，以增加或減少逾時限制。

## 自訂追蹤事件 {#customizing-the-tracking-events}

您可以修改 `trackEvent`中可用的函式 `/libs/afanalytics/js/custom.js` 檔案來自訂事件追蹤。 每當要追蹤的事件以最適化表單發生時， `trackEvent`函式已呼叫。 此 `trackEvent` 函式接受兩個引數： `eventName`和 `variableValueMap`.

您可以評估下列專案的值： *事件名稱* 和 *variableValueMap* 引數來變更事件的追蹤行為。 例如，您可以選擇在發生特定數量的錯誤事件後，將資訊傳送至Analytics伺服器。 您也可以選擇執行下列任何自訂專案：

* 您可以在傳送事件之前設定臨界值時間。
* 您可以維護狀態以決定動作，例如， *fieldVisit* 根據上一個事件的時間戳記推送一個虛擬事件。
* 您可以使用 `pushEvent` 將事件傳送至analytics伺服器的函式 *.*

* 您可以選擇完全不將事件推送至分析伺服器。

### 样本 {#sample}

在下列範例中， *錯誤* 每個的事件 *fieldName* 屬性已維護。 只有在再次發生錯誤時，才會將事件傳送至Analytics伺服器。

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## 自訂面板造訪事件 {#customizing-the-panelvisit-event}

在預設的AEM Forms設定中，每60秒後，會檢查包含最適化表單的視窗是否處於作用中狀態。 如果視窗處於作用中狀態， `panelVisit`事件會觸發至Adobe Analytics。 它有助於確定檔案或表單是否作用中，並計算在相應表單或檔案上的逗留時間。

>[!NOTE]
>
>用來存取活動和計算逗留時間的事件名稱為「panelVisit」。 此事件與上表所列面板瀏覽事件不同。

您可以修改scheduleHeartBeatCheck函式，該函式可在 `/libs/afanalytics/js/custom.js` 檔案來變更或停止定期傳送至Adobe Analytics的事件。
