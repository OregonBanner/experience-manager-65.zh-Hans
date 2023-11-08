---
title: 异步提交自适应表单
description: 了解如何为自适应表单配置异步提交。
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms
exl-id: bd0589e2-b15a-4f0e-869c-2da4760b1ff4
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 13%

---

# 异步提交自适应表单{#asynchronous-submission-of-adaptive-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/asynchronous-submissions-adaptive-forms.html) |
| AEM 6.5 | 本文 |

传统上，Web窗体配置为同步提交。 在同步提交中，当用户提交表单时，他们将被重定向到确认页面、感谢页面，或者如果提交失败，则被重定向到错误页面。 但是，单页应用程序等现代Web体验越来越受欢迎，这是因为在后台进行客户端 — 服务器交互时，网页保持静态。 现在，您可以通过配置异步提交为自适应表单提供此体验。

在异步提交中，当用户提交表单时，表单开发人员会插入单独的体验，例如重定向到网站的其他表单或单独的部分。 作者还可以插入单独的服务（如将数据发送到不同的数据存储）或添加自定义分析引擎。 如果是异步提交，则自适应表单的行为与单页应用程序类似，因为当在服务器上验证提交的表单数据时，表单不会重新加载或其URL不会更改。

请阅读以了解有关自适应表单中异步提交的详细信息。

## 配置异步提交 {#configure}

要为自适应表单配置异步提交，请执行以下操作：

1. 在自适应表单创作模式下，选择表单容器对象并点按 ![cmppr1](assets/cmppr1.png) 以打开其属性。
1. 在 **[!UICONTROL 提交]** 属性部分，启用 **[!UICONTROL 使用异步提交]**.
1. 在 **[!UICONTROL 在提交时]** 部分，选择下列选项之一以在成功提交表单时执行。

   * **[!UICONTROL 重定向到URL]**：在提交表单时重定向到指定的URL或页面。 您可以指定URL或浏览以选择页面的路径 **[!UICONTROL 重定向URL/路径]** 字段。
   * **[!UICONTROL 显示消息]**：在表单提交时显示消息。 您可以在“显示消息”选项下方的文本字段中写入消息。 文本字段支持富文本格式。

1. 点按 ![check-button1](assets/check-button1.png) 以保存属性。

## 异步提交的工作方式 {#how-asynchronous-submission-works}

AEM Forms 为表单提交提供现成的成功和错误处理程序。处理程序是根据服务器响应执行的客户端函数。在提交表单时，数据被传输到服务器进行验证，服务器将响应返回到客户端，其中包含有关提交的成功或错误事件的信息。 该信息作为参数传递给相关处理程序以执行该函数。

此外，表单作者和开发人员可以在表单级别编写规则以覆盖默认处理程序。 有关更多信息，请参阅 [使用规则覆盖默认处理程序](#custom).

让我们首先查看服务器响应中的成功和错误事件。

### 提交成功事件的服务器响应 {#server-response-for-submission-success-event}

针对提交成功事件的服务器响应的结构如下所示：

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

如果表单提交成功，则服务器响应包括：

* 表单数据格式类型：XML或JSON
* XML或JSON格式的表单数据
* 已选择选项，用于重定向到页面或显示表单中配置的消息
* 页面URL或消息内容，如表单中所配置

成功处理程序读取服务器响应，并相应地重定向到配置的页面URL或显示消息。

### 提交错误事件的服务器响应 {#server-response-for-submission-error-event}

针对提交错误事件的服务器响应的结构如下所示：

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

如果表单提交中存在错误，则服务器响应包括：

* 错误原因，验证码或服务器端验证失败
* 错误对象列表，其中包括验证失败的字段的SOM表达式和相应的错误消息

错误处理程序会读取服务器响应，并在表单上显示相应的错误消息。

## 使用规则覆盖默认处理程序 {#custom}

表单开发人员和作者可以在代码编辑器中在表单级别编写规则以覆盖默认处理程序。 成功和错误事件的服务器响应在表单级别公开，开发人员可以使用进行访问 `$event.data` 在规则中。

执行以下步骤以在代码编辑器中编写规则以处理成功和错误事件。

1. 在创作模式下打开自适应表单，选择任意表单对象，然后点击 ![edit-rules1](assets/edit-rules1.png) 以打开规则编辑器。
1. 选择 **[!UICONTROL 表单]** 在表单对象树中，然后点按 **[!UICONTROL 创建]**.
1. 选择 **[!UICONTROL 代码编辑器]** 从模式选择下拉列表中。
1. 在代码编辑器中，点按 **[!UICONTROL 编辑代码]**. 点按 **[!UICONTROL 编辑]** 在确认对话框中。
1. 选择 **[!UICONTROL 提交成功]** 或 **[!UICONTROL 提交时出错]** 从 **[!UICONTROL 事件]** 下拉菜单。
1. 为所选事件编写规则并点击 **[!UICONTROL 完成]** 以保存规则。
