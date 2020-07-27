---
title: 自定义表单事件跟踪
seo-title: 自定义表单事件跟踪
description: 如果用户在某个字段上花费的时间超过60秒，则会触发字段访问事件，并将字段的详细信息发送到Adobe SiteCatalyst。
seo-description: 如果用户在某个字段上花费的时间超过60秒，则会触发字段访问事件，并将字段的详细信息发送到Adobe SiteCatalyst。
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# 自定义表单事件跟踪 {#customizing-form-event-tracking}

开箱即用，在启用分析的自适应表单中跟踪以下事件:

<table>
 <tbody>
  <tr>
   <th>事件</th>
   <th>可用变量</th>
  </tr>
  <tr>
   <td>渲染</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>放弃</td>
   <td>formName、formTitle、formInstance、panelName、panelTitle</td>
  </tr>
  <tr>
   <td>保存</td>
   <td>formName、formTitle、formInstance、panelName、source</td>
  </tr>
  <tr>
   <td>提交</td>
   <td>formName, formTitle, formInstance, source</td>
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

## 自定义字段访问事件超时 {#customizing-the-field-visit-event-timeout}

在默认的AEM表单设置中，如果用户在某个字段上花费的时间超过 `fieldvisit` 60秒，则会触发事件，并将字段的详细信息发送给AdobeAnalytics。 您可以在AEM配置控制台(/system/console/configMgr)的AEM FormsAnalytics配置下自定义字段时间跟踪基线，以增加或减少超时限制。

## 自定义跟踪事件 {#customizing-the-tracking-events}

您可以修改文 `trackEvent`件中的可 `/libs/afanalytics/js/custom.js` 用函数以自定义事件跟踪。 每当跟踪的事件以自适应形式出现时，都会调 `trackEvent`用该函数。 该函 `trackEvent` 数接受两个参数： `eventName`和 `variableValueMap`。

您可以评估eventName *和variable* ValueMap *参数的值* ，以更改事件的跟踪行为。 例如，在发生一定数量的错误事件后，您可以选择将信息发送到分析服务器。 您还可以选择执行以下任意自定义：

* 您可以在发送事件之前设置阈值时间。
* 您可以维护一个状态以决定操作，例 *如* fieldVisit根据上一个事件的时间戳推送虚拟事件。
* 您可以使用该函 `pushEvent` 数将事件发送到分析服务器 *。*

* 您完全可以选择不将事件推送到分析服务器。

### 示例 {#sample}

在以下示例中，将保留每 *个fieldName* 属性的 *错误事件* 的状态。 仅当再次发生错误时，事件才会发送到分析服务器。

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## 自定义面板访问事件 {#customizing-the-panelvisit-event}

在默认AEM Forms设置中，每60秒会检查一次包含自适应表单的窗口是否处于活动状态。 如果窗口处于活动状态， `panelVisit`则事件将触发到AdobeAnalytics。 它有助于确定文档或表单是活动的，并计算在相应表单或文档上花费的时间。

>[!NOTE]
>
>用于确定事件和计算所花费时间的活动名称为“panelVisit”。 此事件与上表所列的面板访问事件不同。

您可以修改文件中可用的scheduleHeartBeatCheck函 `/libs/afanalytics/js/custom.js` 数，以定期间隔更改或停止发送给Adobe事件的此Analytics。
