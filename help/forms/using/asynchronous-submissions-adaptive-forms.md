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
source-git-commit: 8bc99ed3817398ae358d439a5c1fcc90bbd24327

---


# 自适应表单的异步提交{#asynchronous-submission-of-adaptive-forms}

Web表单通常配置为同步提交。 在同步提交中，用户提交表单时，会将其重定向到确认页面、感谢页面或提交失败时的错误页面。 但是，诸如单页应用程序等现代Web体验正在获得广泛的使用，当Web页保持静态时，客户端与服务器的交互在后台进行。 您现在可以通过配置异步提交来为此体验提供自适应表单。

在异步提交中，当用户提交表单时，表单开发人员将插入一个单独的体验，如重定向到其他表单或网站的单独部分。 作者还可以插入单独的服务，如将数据发送到其他数据存储或添加自定义分析引擎。在异步提交的情况下，自适应表单的行为类似于单页应用程序，因为表单不会重新加载或在服务器上验证提交的表单数据时其URL不会更改。

阅读有关自适应表单中异步提交的详细信息。

## 配置异步提交 {#configure}

要为自适应表单配置异步提交，请执行以下操作：

1. 在自适应表单创作模式中，选择表单容器对象，然后点 ![按cmppr1](assets/cmppr1.png) 以打开其属性。
1. 在“提交 **[!UICONTROL 属性]** ”部分，启用“ **[!UICONTROL 使用异步提交”]**。
1. 在“提交 **[!UICONTROL 时]** ”部分，选择以下选项之一以在成功提交表单时执行。

   * **[!UICONTROL 重定向到URL]**:在提交表单时重定向到指定的URL或页面。 您可以指定URL或浏览以在“重定向URL/路径”字段中选择页 **[!UICONTROL 面的路径]** 。
   * **[!UICONTROL 显示消息]**:在提交表单时显示消息。 您可以在“显示消息”选项下的文本字段中写入消息。 文本字段支持富文本格式。

1. 点 ![按check-button1](assets/check-button1.png) 以保存属性。

## 异步提交的工作原理 {#how-asynchronous-submission-works}

AEM Forms为表单提交提供开箱即用的成功和错误处理程序。 处理程序是基于服务器响应执行的客户端函数。 当提交表单时，数据被传输到服务器以进行验证，服务器将向客户端返回响应，其中包含有关提交成功或错误事件的信息。 该信息作为参数传递给相关处理函数以执行该函数。

此外，表单作者和开发人员可以在表单级别编写规则以覆盖默认处理函数。 有关详细信息，请参阅 [使用规则覆盖默认处理函数](#custom)。

让我们首先查看服务器对成功和错误事件的响应。

### 针对提交成功事件的服务器响应 {#server-response-for-submission-success-event}

服务器对提交成功事件的响应的结构如下：

```
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
* 选中的选项可重定向到页面或显示表单中配置的消息
* 在表单中配置的页面URL或消息内容

成功处理程序读取服务器响应，并相应地重定向到所配置的页面URL或显示一条消息。

### 针对提交错误事件的服务器响应 {#server-response-for-submission-error-event}

服务器响应提交错误事件的结构如下：

```
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

* 错误原因、CAPTCHA失败或服务器端验证失败
* 错误对象列表，包括验证失败的字段的SOM表达式和相应的错误消息

错误处理程序读取服务器响应，并相应地在表单上显示错误消息。

## 使用规则覆盖默认处理函数 {#custom}

表单开发人员和作者可以在表单级别在代码编辑器中编写规则以覆盖默认处理函数。 针对成功和错误事件的服务器响应在表单级别显示，开发人员可以在规则中使用 `$event.data` 该表单访问。

执行以下步骤以在代码编辑器中编写规则来处理成功和错误事件。

1. 在创作模式下打开自适应表单，选择任何表单对象，然后点 ![按edit-rules1](assets/edit-rules1.png) 以打开规则编辑器。
1. 在“表 **[!UICONTROL 单对象]** ”树中选择表单，然后点按 **[!UICONTROL 创建]**。
1. 从模 **[!UICONTROL 式选择下拉菜单中选择代码编辑器]** 。
1. 在代码编辑器中，点按编 **[!UICONTROL 辑代码]**。 在确 **[!UICONTROL 认对话框中]** ，点按编辑。
1. 从“事 **[!UICONTROL 件]** ”下拉 **[!UICONTROL 菜单中选择“提交成]** 功 **** ”或“提交时出错”。
1. 为选定事件编写规则，然后点按 **[!UICONTROL 完成]** ，以保存该规则。

