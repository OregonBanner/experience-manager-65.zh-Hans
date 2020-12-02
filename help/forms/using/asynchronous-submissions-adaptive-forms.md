---
title: 自适应表单的异步提交
seo-title: 自适应表单的异步提交
description: 了解如何为自适应表单配置异步提交。
seo-description: 了解如何为自适应表单配置异步提交。
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---


# 自适应表单的异步提交{#asynchronous-submission-of-adaptive-forms}

通常，Web表单配置为同步提交。 在同步提交中，用户提交表单时，会将其重定向到确认页、感谢页或提交失败时的错误页。 然而，诸如单页应用程序等现代Web体验正在日益流行，其中网页保持静态，而客户端与服务器交互在后台进行。 您现在可以通过配置异步提交来提供此自适应表单体验。

在异步提交中，当用户提交表单时，表单开发人员将插入一个单独的体验，如重定向到其他表单或网站的单独部分。 作者还可以插入单独的服务，如向其他数据存储发送数据或添加自定义分析引擎。在异步提交时，自适应表单的行为类似于单页应用程序，因为表单在服务器上验证提交的表单数据时不会重新加载或其URL不会更改。

阅读有关自适应表单异步提交的详细信息。

## 配置异步提交{#configure}

为自适应表单配置异步提交：

1. 在自适应表单创作模式中，选择表单容器对象，然后点按![cmpr1](assets/cmppr1.png)以打开其属性。
1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;属性部分，启用&#x200B;**[!UICONTROL 使用异步提交]**。
1. 在&#x200B;**[!UICONTROL 在提交]**&#x200B;部分，选择以下选项之一，在成功提交表单时执行。

   * **[!UICONTROL 重定向到URL]**:在提交表单时重定向到指定的URL或页面。您可以在&#x200B;**[!UICONTROL 重定向URL/路径]**&#x200B;字段中指定URL或浏览以选择页面的路径。
   * **[!UICONTROL 显示消息]**:显示提交表单时的消息。您可以在“显示消息”选项下的文本字段中写入消息。 文本字段支持富文本格式。

1. 点按![check-button1](assets/check-button1.png)以保存属性。

## 异步提交的工作原理{#how-asynchronous-submission-works}

AEM Forms为表单提交提供开箱即用的成功和错误处理程序。 处理函数是基于服务器响应执行的客户端函数。 提交表单时，数据会被传输到服务器进行验证，服务器会向客户端返回一个响应，其中包含有关提交成功或错误事件的信息。 信息作为参数传递给相关处理函数以执行该函数。

此外，表单作者和开发人员可以在表单级别编写规则以覆盖默认处理函数。 有关详细信息，请参阅[使用规则](#custom)覆盖默认处理函数。

让我们首先查看服务器响应，了解成功和错误事件。

### 服务器对提交成功事件{#server-response-for-submission-success-event}的响应

服务器响应提交成功事件的结构如下：

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
* 已选择重定向到页面或显示消息的选项（如表单中所配置）
* 在表单中配置的页面URL或消息内容

成功处理程序读取服务器响应，并相应地重定向到所配置的页面URL或显示一条消息。

### 服务器对提交错误的响应事件{#server-response-for-submission-error-event}

服务器响应的提交错误事件结构如下：

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

提交表单时出错时的服务器响应包括：

* 错误、CAPTCHA失败或服务器端验证的原因
* 错误对象列表，包括验证失败字段的SOM表达式和相应的错误消息

错误处理程序读取服务器响应，并相应地在表单上显示错误消息。

## 使用规则{#custom}覆盖默认处理函数

表单开发人员和作者可以在表单级别在代码编辑器中编写规则以覆盖默认处理函数。 成功和错误事件的服务器响应以表单级别显示，开发人员可以使用规则中的`$event.data`访问该表单。

执行以下步骤以在代码编辑器中编写规则，以处理成功和错误事件。

1. 在创作模式下打开自适应表单，选择任何表单对象，然后点按![edit-rules1](assets/edit-rules1.png)以打开规则编辑器。
1. 在表单对象树中选择&#x200B;**[!UICONTROL 表单]**，然后点按&#x200B;**[!UICONTROL 创建]**。
1. 从模式选择下拉菜单中选择&#x200B;**[!UICONTROL 代码编辑器]**。
1. 在代码编辑器中，点按&#x200B;**[!UICONTROL 编辑代码]**。 点按确认对话框上的&#x200B;**[!UICONTROL 编辑]**。
1. 从&#x200B;**[!UICONTROL 事件]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 成功提交]**&#x200B;或&#x200B;**[!UICONTROL 提交错误]**。
1. 为所选事件编写规则，然后点按&#x200B;**[!UICONTROL 完成]**&#x200B;以保存该规则。

