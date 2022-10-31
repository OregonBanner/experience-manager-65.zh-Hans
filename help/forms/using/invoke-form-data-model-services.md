---
title: 用于从自适应表单调用表单数据模型服务的API
seo-title: API to invoke form data model service from adaptive forms
description: 说明可用于从自适应表单字段中调用以WSDL编写的Web服务的invokeWebServices API。
seo-description: Explains the invokeWebServices API that you can use to invoke web services written in WSDL from within an adaptive form field.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms
exl-id: cf037174-3153-486f-85b1-c974cd5a1ace
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 用于从自适应表单调用表单数据模型服务的API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概述 {#overview}

AEM Forms允许表单作者通过从自适应表单字段中调用在表单数据模型中配置的服务，进一步简化和增强表单填充体验。 要调用数据模型服务，您可以在可视编辑器中创建规则，或使用 `guidelib.dataIntegrationUtils.executeOperation` 代码编辑器中的API [规则编辑器](/help/forms/using/rule-editor.md).

本文档重点介绍如何使用 `guidelib.dataIntegrationUtils.executeOperation` 用于调用服务的API。

## 使用API {#using-the-api}

的 `guidelib.dataIntegrationUtils.executeOperation` API从自适应表单字段内调用服务。 API语法如下所示：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

的结构 `guidelib.dataIntegrationUtils.executeOperation` API指定有关服务操作的详细信息。 结构的语法如下所示。

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API结构指定了有关服务操作的以下详细信息。

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>指定表单数据模型标识符、操作标题和操作名称的结构</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>指定表单数据模型的存储库路径（包括其名称）</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>指定要执行的服务操作的名称</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>将一个或多个表单对象映射到服务操作的输入参数</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>将一个或多个表单对象映射到服务操作中的输出值以填充表单字段<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>根据服务操作的输入参数返回值。 它是用作回调函数的可选参数。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>如果成功回调函数无法根据输入参数显示输出值，则显示一条错误消息。 它是用作回调函数的可选参数。<br /> </td>
  </tr>
 </tbody>
</table>

## 调用服务的示例脚本 {#sample-script-to-invoke-a-service}

以下示例脚本使用 `guidelib.dataIntegrationUtils.executeOperation` 用于调用的API `getAccountById` 在 `employeeAccount` 表单数据模型。

的 `getAccountById` 操作采用 `employeeID` 表单字段作为输入 `empId` 参数和返回相应员工的员工名称、帐号和帐户余额。 输出值将填充在指定的表单字段中。 例如， `name` 参数会填充在 `fullName` 表单元素和值 `accountNumber` 参数 `account` 表单元素。

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## 将API与回调函数结合使用 {#using-the-api-callback}

您还可以使用 `guidelib.dataIntegrationUtils.executeOperation` 具有回调函数的API。 API语法如下所示：

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

回调函数可以 `success` 和 `failure` 回调函数。

### 包含成功和失败回调函数的示例脚本 {#callback-function-success-failure}

以下示例脚本使用 `guidelib.dataIntegrationUtils.executeOperation` 用于调用的API `GETOrder` 在 `employeeOrder` 表单数据模型。

的 `GETOrder` 操作采用 `Order ID` 表单字段作为输入 `orderId` 参数和返回订单量值(在 `success` 回调函数。  如果 `success` 回调函数不返回订单数量， `failure` 回调函数显示 `Error occured` 消息。

>[!NOTE]
>
>如果您使用 `success` 回调函数中，输出值不会填充在指定的表单字段中。

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
