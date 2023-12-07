---
title: 自定义表单事件跟踪
description: 如果用户在字段上花费的时间超过60秒，则会触发fieldvisit事件，并将字段的详细信息发送到Adobe SiteCatalyst。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# 自定义表单事件跟踪 {#customizing-form-event-tracking}

在支持Analytics的自适应表单中，现成可跟踪以下事件：

<table>
 <tbody>
  <tr>
   <th>事件</th>
   <th>可用变量</th>
  </tr>
  <tr>
   <td>渲染</td>
   <td>formName， formTitle， formInstance， source</td>
  </tr>
  <tr>
   <td>放弃</td>
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

## 自定义字段访问事件超时 {#customizing-the-field-visit-event-timeout}

在默认的AEM表单设置中，如果用户在字段上花费的时间超过60秒，则 `fieldvisit` 触发事件，并将字段的详细信息发送到Adobe Analytics。 您可以在AEM配置控制台(/system/console/configMgr)的AEM Forms Analytics配置下自定义字段时间跟踪基线，以增加或减少超时限制。

## 自定义跟踪事件 {#customizing-the-tracking-events}

您可以修改 `trackEvent`中可用的函数 `/libs/afanalytics/js/custom.js` 文件，以自定义事件跟踪。 每当以自适应表单发生被跟踪的事件时， `trackEvent`调用函数。 此 `trackEvent` 函数接受两个参数： `eventName`和 `variableValueMap`.

您可以计算 *事件名称* 和 *variableValueMap* 用于更改事件的跟踪行为的参数。 例如，您可以选择在发生一定数量的错误事件后将信息发送到Analytics服务器。 您还可以选择执行以下任何自定义设置：

* 您可以在发送事件之前设置阈值时间。
* 您可以维护状态以决定操作，例如， *fieldVisit* 根据上一个事件的时间戳推送一个虚拟事件。
* 您可以使用 `pushEvent` 用于将事件发送到analytics服务器的函数 *.*

* 您可以选择根本不将事件推送到Analytics服务器。

### 样本 {#sample}

在以下示例中，省/自治区/直辖市 *错误* 事件（属于每个） *fieldName* 属性已维护。 仅当再次发生错误时，才会将该事件发送到Analytics服务器。

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## 自定义面板访问事件 {#customizing-the-panelvisit-event}

在默认的AEM Forms设置中，每60秒后，会检查包含自适应表单的窗口是否处于活动状态。 如果窗口处于活动状态， `panelVisit`事件会触发到Adobe Analytics。 它有助于确定文档或表单是否处于活动状态，并计算在相应表单或文档上花费的时间。

>[!NOTE]
>
>用于确定活动和计算逗留时间的事件名称为“panelVisit”。 此事件与上表中所列的面板访问事件不同。

您可以修改中提供的scheduleHeartBeatCheck函数 `/libs/afanalytics/js/custom.js` 文件，用于定期更改或停止发送给Adobe Analytics的此事件。
