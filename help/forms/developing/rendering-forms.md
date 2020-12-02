---
title: 呈现Forms
seo-title: 呈现Forms
description: 'null'
seo-description: 'null'
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---


# 呈现Forms{#rendering-forms}

**关于Forms服务**

Forms服务允许您创建交互式数据捕获客户端应用程序，这些应用程序通常在Designer中验证、处理、转换和交付表单。 表单作者可以开发单个表单设计，Forms服务在各种浏览器环境以PDF、SWF或HTML格式呈现。

当最终用户请求表单时，客户端应用程序将请求发送到Forms服务，后者以适当的格式返回表单。 Forms服务一收到请求，就会将数据与表单设计合并，然后以所需格式发送表单。 表单服务输出是交互式表单，通常是PDF文档。 交互式表单使用户能够填写表单上的字段。

根据客户端应用程序的类型，您可以将表单写入客户端Web浏览器或将表单另存为PDF文件。 基于Web的应用程序可以将表单写入Web浏览器。 桌面应用程序可将表单另存为PDF文件。 要演示如何向Web浏览器和PDF文件写出，请按照以下方式组织位于“渲染Forms”*部分的快速开始:*

* Java API强类型（SOAP模式）示例是Java servlet。
* Web服务(Java Base64)示例是Java servlet。
* Web服务(MTOM)示例是控制台应用程序(并非所有快速开始都有MTOM示例)。

>[!NOTE]
>
>有关创建使用java servlet调用Forms服务的Web应用程序的信息，请参阅[创建呈现Forms的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)。

您可以通过以下两种方式之一将表单设计（XDP文件）或PDF文档传递到Forms服务：

* 可以使用URL值引用表单设计。 此方法涉及使用`URLSpec`对象。 使用`URLSpec`对象的`setContentRootURI`方法将内容根传递给Forms服务。 表单设计名称(`formQuery`)作为单独的参数传递。 将这两个值连接起来，以获得对表单设计的绝对引用。 (位于&#x200B;*渲染Forms*&#x200B;部分的大多数快速开始都使用此方法。)
* 您可以将包含表单设计的`com.adobe.idp.Document`传递给Forms服务。 名为`renderPDFForm2`和`renderHTMLForm2`的两种新方法接受包含表单设计的`com.adobe.idp.Document`对象。 (请参阅[将文档传递给Forms服务](/help/forms/developing/passing-documents-forms-service.md)

您可以使用Forms服务完成以下任务:

* 渲染交互式PDF forms。 (请参阅[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)。)
* 在客户端渲染表单。 (请参阅[在客户端渲染Forms](/help/forms/developing/rendering-forms-client.md)。)
* 根据片段呈现表单。 (请参阅[根据片段渲染Forms](/help/forms/developing/rendering-forms-based-fragments.md)。)
* 渲染启用权限的表单。 (请参阅[启用渲染权限的Forms](/help/forms/developing/rendering-rights-enabled-forms.md)。)
* 以HTML形式呈现表单。 (请参阅[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)。)
* 使用自定义CSS文件呈现HTMLForms([使用自定义CSS文件呈现HTMLForms](/help/forms/developing/rendering-html-forms-using-custom.md)。)
* 处理提交的表单。 (请参阅[处理已提交的Forms](/help/forms/developing/handling-submitted-forms.md)。)
* 使用已提交的XML数据创建PDF文档。 (请参阅[使用已提交的XML文档创建PDF数据](/help/forms/developing/creating-pdf-documents-submitted-xml.md)。)
* 预填表单。 (请参阅[使用可流动布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
* 传递文档。 (请参阅[将文档传递给Forms服务](/help/forms/developing/passing-documents-forms-service.md)
* 计算表单数据。 （请参阅[计算表单数据](/help/forms/developing/calculating-form-data.md)。）
* 优化应用程序。 (请参阅[优化Forms服务的性能](/help/forms/developing/optimizing-performance-forms-service.md)。)

   ***提示&#x200B;**:Adobe开发者网站包含以下文章，其中讨论如何创建调用Forms服务并呈现表单的ASP.NET应用程序。请参阅[创建表单呈现ASP.NET应用程序](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)。*

