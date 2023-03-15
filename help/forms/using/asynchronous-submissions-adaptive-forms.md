---
title: 异步提交自适应表单
seo-title: Asynchronous submission of adaptive forms
description: 了解如何为自适应表单配置异步提交。
seo-description: Learn to configure asynchronous submission for adaptive forms.
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
feature: Adaptive Forms
exl-id: bd0589e2-b15a-4f0e-869c-2da4760b1ff4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# 异步提交自适应表单{#asynchronous-submission-of-adaptive-forms}

传统上，Web窗体配置为同步提交。 在同步提交时，当用户提交表单时，会被重定向到确认页面、感谢页面或在提交失败的情况下被重定向到错误页面。 但是，像单页应用程序这样的现代Web体验正在变得流行起来，这是因为网页保持静态，而客户端 — 服务器交互发生在后台。 您现在可以通过配置异步提交来通过自适应表单提供此体验。

在异步提交中，当用户提交表单时，表单开发人员会插入单独的体验，例如重定向到网站的其他表单或单独的部分。 作者还可以插入单独的服务，如将数据发送到不同的数据存储库，或者添加自定义分析引擎。在异步提交的情况下，自适应表单的行为类似于单页应用程序，因为当在服务器上验证提交的表单数据时，表单不会重新加载或其URL不会更改。

请阅读以了解有关自适应表单中异步提交的详细信息。

## 配置异步提交 {#configure}

要为自适应表单配置异步提交，请执行以下操作：

1. 在自适应表单创作模式下，选择表单容器对象并点按 ![cmppr1](assets/cmppr1.png) 以打开其属性。
1. 在 **[!UICONTROL 提交]** 属性部分，启用 **[!UICONTROL 使用异步提交]**.
1. 在 **[!UICONTROL 提交时]** 部分，选择以下选项之一以在成功提交表单时执行。

   * **[!UICONTROL 重定向到URL]**：在提交表单时重定向到指定的URL或页面。 您可以指定URL或浏览来选择 **[!UICONTROL 重定向URL/路径]** 字段。
   * **[!UICONTROL 显示消息]**：在表单提交时显示消息。 您可以在“显示消息”选项下方的文本字段中写入消息。 文本字段支持富文本格式。

1. 点按 ![check-button1](assets/check-button1.png) 以保存属性。

## 异步提交的工作方式 {#how-asynchronous-submission-works}

AEM Forms为表单提交提供开箱即用的成功和错误处理程序。 处理程序是根据服务器响应执行的客户端功能。 当提交表单时，数据被传输到服务器进行验证，服务器将响应返回到客户端，其中包含有关提交的成功或错误事件的信息。 信息作为参数传递给相关处理程序以执行函数。

此外，表单作者和开发人员可以在表单级别编写规则以覆盖默认处理程序。 有关更多信息，请参阅 [使用规则覆盖默认处理程序](#custom).

让我们首先查看服务器响应中的成功和错误事件。

### 提交成功事件的服务器响应 {#server-response-for-submission-success-event}

提交成功事件的服务器响应结构如下：

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
* 已选择选项，用于重定向到页面或显示表单中配置的消息
* 页面URL或消息内容，如表单中所配置

成功处理程序读取服务器响应，并相应地重定向到配置的页面URL或显示消息。

### 提交错误事件的服务器响应 {#server-response-for-submission-error-event}

提交错误事件的服务器响应结构如下：

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

在提交表单时出现错误时，服务器响应包括：

* 错误原因，验证码或服务器端验证失败
* 错误对象列表，其中包括验证失败的字段的SOM表达式和相应的错误消息

错误处理程序会读取服务器响应，并在表单上显示相应的错误消息。

## 使用规则覆盖默认处理程序 {#custom}

表单开发人员和作者可以在表单级别在代码编辑器中编写规则以覆盖默认处理程序。 成功和错误事件的服务器响应在表单级别公开，开发人员可以使用进行访问 `$event.data` 在规则中。

执行以下步骤以在代码编辑器中编写规则以处理成功和错误事件。

1. 在创作模式下打开自适应表单，选择任意表单对象，然后点按 ![edit-rules1](assets/edit-rules1.png) 以打开规则编辑器。
1. 选择 **[!UICONTROL 表单]** 在表单对象树中，然后点按 **[!UICONTROL 创建]**.
1. 选择 **[!UICONTROL 代码编辑器]** 从模式选择下拉列表中。
1. 在代码编辑器中，点按 **[!UICONTROL 编辑代码]**. 点按 **[!UICONTROL 编辑]** 在确认对话框中。
1. 选择 **[!UICONTROL 提交成功]** 或 **[!UICONTROL 提交时出错]** 从 **[!UICONTROL 事件]** 下拉菜单。
1. 为所选事件编写规则并点按 **[!UICONTROL 完成]** 以保存规则。
