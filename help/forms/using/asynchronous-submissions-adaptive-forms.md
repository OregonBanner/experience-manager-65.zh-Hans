---
title: 异步提交自适应表单
seo-title: 异步提交自适应表单
description: 了解如何为自适应表单配置异步提交。
seo-description: 了解如何为自适应表单配置异步提交。
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
feature: 自适应表单
exl-id: bd0589e2-b15a-4f0e-869c-2da4760b1ff4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# 异步提交自适应表单{#asynchronous-submission-of-adaptive-forms}

传统上，Web表单配置为同步提交。 在同步提交中，当用户提交表单时，会将用户重定向到确认页面、感谢页面，或者在提交失败时，会重定向到错误页面。 但是，诸如单页应用程序等现代Web体验越来越受欢迎，其中网页保持静态，而客户端 — 服务器交互在后台进行。 您现在可以通过配置异步提交，为此体验提供自适应表单。

在异步提交中，当用户提交表单时，表单开发人员会插入一个单独的体验，如重定向到其他表单或网站的单独部分。 作者还可以插入单独的服务，如将数据发送到其他数据存储或添加自定义分析引擎。在异步提交时，自适应表单的行为与单页应用程序类似，因为表单不会重新加载或在服务器上验证提交的表单数据后其URL不会更改。

请阅读有关自适应表单中异步提交的详细信息。

## 配置异步提交 {#configure}

要配置自适应表单的异步提交，请执行以下操作：

1. 在自适应表单创作模式中，选择表单容器对象，然后点按![cmppr1](assets/cmppr1.png)以打开其属性。
1. 在&#x200B;**[!UICONTROL Submission]**&#x200B;属性部分中，启用&#x200B;**[!UICONTROL 使用异步提交]**。
1. 在&#x200B;**[!UICONTROL 在提交]**&#x200B;部分中，选择以下选项之一，以在成功提交表单时执行。

   * **[!UICONTROL 重定向到URL]**:在表单提交时重定向到指定的URL或页面。您可以在&#x200B;**[!UICONTROL 重定向URL/路径]**&#x200B;字段中指定URL或浏览以选择页面的路径。
   * **[!UICONTROL 显示消息]**:在表单提交时显示消息。您可以在“显示消息”选项下方的文本字段中写入消息。 文本字段支持富文本格式。

1. 点按![check-button1](assets/check-button1.png)以保存属性。

## 异步提交的工作原理{#how-asynchronous-submission-works}

AEM Forms为表单提交提供了开箱即用的成功和错误处理程序。 处理程序是基于服务器响应执行的客户端函数。 在提交表单时，数据被传输到服务器进行验证，服务器会向客户端返回响应，其中包含有关提交的成功或错误事件的信息。 该信息作为参数传递给相关处理程序以执行该函数。

此外，表单作者和开发人员可以在表单级别编写规则以覆盖默认处理程序。 有关更多信息，请参阅[使用规则](#custom)覆盖默认处理程序。

让我们首先查看服务器对成功事件和错误事件的响应。

### 提交成功事件{#server-response-for-submission-success-event}的服务器响应

提交成功事件的服务器响应的结构如下：

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

成功提交表单时的服务器响应包括：

* 表单数据格式类型：XML或JSON
* XML或JSON格式的表单数据
* 选择了重定向到页面或显示消息的选项，该选项在表单中进行了配置
* 表单中配置的页面URL或消息内容

成功处理程序读取服务器响应并相应地重定向到配置的页面URL或显示消息。

### 针对提交错误事件的服务器响应{#server-response-for-submission-error-event}

服务器响应提交错误事件的结构如下：

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

表单提交出错时的服务器响应包括：

* 错误、CAPTCHA或服务器端验证失败的原因
* 错误对象列表，包括验证失败的字段的SOM表达式和相应的错误消息

错误处理程序读取服务器响应，并相应地在表单上显示错误消息。

## 使用规则覆盖默认处理程序 {#custom}

表单开发人员和作者可以在表单级别的代码编辑器中编写规则，以覆盖默认处理程序。 成功事件和错误事件的服务器响应在表单级别显示，开发人员可以在规则中使用`$event.data`访问表单级别。

执行以下步骤以在代码编辑器中写入规则以处理成功事件和错误事件。

1. 在创作模式下打开自适应表单，选择任意表单对象，然后点按![edit-rules1](assets/edit-rules1.png)以打开规则编辑器。
1. 在“表单对象”树中选择&#x200B;**[!UICONTROL 表单]** ，然后点按&#x200B;**[!UICONTROL 创建]**。
1. 从模式选择下拉列表中选择&#x200B;**[!UICONTROL 代码编辑器]**。
1. 在代码编辑器中，点按&#x200B;**[!UICONTROL 编辑代码]**。 点按确认对话框上的&#x200B;**[!UICONTROL 编辑]** 。
1. 从&#x200B;**[!UICONTROL 事件]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 成功提交]**&#x200B;或&#x200B;**[!UICONTROL 提交中的错误]**。
1. 为选定事件编写规则，然后点按&#x200B;**[!UICONTROL Done]**&#x200B;以保存规则。
