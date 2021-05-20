---
title: 自定义表单事件跟踪
seo-title: 自定义表单事件跟踪
description: 如果用户在字段上花费的时间超过60秒，则会触发字段访问事件，并将字段的详细信息发送到Adobe SiteCatalyst。
seo-description: 如果用户在字段上花费的时间超过60秒，则会触发字段访问事件，并将字段的详细信息发送到Adobe SiteCatalyst。
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 自定义表单事件跟踪{#customizing-form-event-tracking}

开箱即用地在启用了分析的自适应表单中跟踪以下事件：

<table>
 <tbody>
  <tr>
   <th>事件</th>
   <th>可用变量</th>
  </tr>
  <tr>
   <td>render</td>
   <td>formName， formTitle， formInstance， source</td>
  </tr>
  <tr>
   <td>放弃</td>
   <td>formName， formTitle， formInstance， panelName， panelTitle</td>
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
   <td>formName， formTitle， fieldName， fieldTitle， panelTitle</td>
  </tr>
  <tr>
   <td>帮助</td>
   <td>formName， formTitle， fieldName， fieldTitle， panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName， formTitle， fieldName， fieldTitle， panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName， formTitle， panelName， panelTitle</td>
  </tr>
 </tbody>
</table>

## 自定义字段访问事件超时{#customizing-the-field-visit-event-timeout}

在默认的AEM表单设置中，如果用户在字段上花费超过60秒，则会触发`fieldvisit`事件，并将字段的详细信息发送到Adobe Analytics。 您可以在AEM配置控制台(/system/console/configMgr)的AEM Forms Analytics配置下自定义字段时间跟踪基线，以增加或减少超时限制。

## 自定义跟踪事件{#customizing-the-tracking-events}

您可以修改`/libs/afanalytics/js/custom.js`文件中可用的`trackEvent`函数，以自定义事件跟踪。 每当以自适应形式发生被跟踪的事件时，都会调用`trackEvent`函数。 `trackEvent`函数接受两个参数：`eventName`和`variableValueMap`。

您可以计算&#x200B;*eventName*&#x200B;和&#x200B;*variableValueMap*&#x200B;参数的值，以更改事件的跟踪行为。 例如，您可以选择在发生一定数量的错误事件后将信息发送到Analytics服务器。 您还可以选择执行以下任意自定义：

* 您可以在发送事件之前设置阈值时间。
* 您可以维护状态以决定操作，例如，*fieldVisit*&#x200B;根据最后一个事件的时间戳推送虚拟事件。
* 您可以使用`pushEvent`函数将事件发送到Analytics服务器&#x200B;*。*

* 您完全可以选择不将事件推送到Analytics服务器。

### 示例 {#sample}

在以下示例中，维护每个&#x200B;*fieldName*&#x200B;属性的&#x200B;*error*&#x200B;事件的状态。 仅当再次发生错误时，才会将事件发送到Analytics服务器。

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## 自定义Panelvisit事件{#customizing-the-panelvisit-event}

在默认的AEM Forms设置中，每60秒会检查一次包含自适应表单的窗口是否处于活动状态。 如果窗口处于活动状态，则会向Adobe Analytics触发`panelVisit`事件。 它有助于确定文档或表单是否处于活动状态，并计算在相应表单或文档上花费的时间。

>[!NOTE]
>
>用于获取活动并计算逗留时间的事件名称为“panelVisit”。 此事件与上表所列的面板访问事件不同。

您可以修改`/libs/afanalytics/js/custom.js`文件中可用的scheduleHeartBeatCheck函数，以定期更改或停止发送到Adobe Analytics的此事件。
