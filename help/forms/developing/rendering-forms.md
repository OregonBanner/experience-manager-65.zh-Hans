---
title: 呈现Forms
seo-title: Rendering Forms
description: 使用Forms服务创建交互式数据捕获客户端应用程序，这些应用程序验证、处理、转换并交付通常在Designer中创建的表单。 表单作者可以开发一个表单设计，Forms服务会在各种浏览器环境中以PDF、SWF或HTML形式呈现该设计。
seo-description: Use the Forms service to create interactive data capture client applications that validate, process, transform, and deliver forms typically created in Designer. Form authors can develop a single form design that the Forms service renders in PDF, SWF, or HTML in various browser environments.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# 呈现Forms {#rendering-forms}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

**关于Forms服务**

Forms服务允许您创建交互式数据捕获客户端应用程序，这些应用程序验证、处理、转换并交付通常在Designer中创建的表单。 表单作者可以开发一个表单设计，Forms服务会在各种浏览器环境中以PDF、SWF或HTML形式呈现该设计。

当最终用户请求表单时，客户端应用程序将请求发送至Forms服务，该服务以适当格式返回表单。 Forms服务一收到请求，就会将数据与表单设计合并，然后以所需的格式交付表单。 表单服务输出是交互式表单，通常是PDF文档。 交互式表单使用户能够填写表单上的字段。

根据客户端应用程序的类型，可以将表单写入客户端Web浏览器或将表单另存为PDF文件。 基于Web的应用程序可以将表单写入Web浏览器。 桌面应用程序可以将表单另存为PDF文件。 要演示如何向Web浏览器和PDF文件写出，可以从 *呈现Forms* 部分按以下方式组织：

* Java API强类型（SOAP模式）示例是一个Java servlet。
* Web服务(Java Base64)示例是一个Java servlet。
* Web服务(MTOM)示例是控制台应用程序（并非所有快速启动都有MTOM示例）。

>[!NOTE]
>
>有关创建使用Java Servlet调用Forms服务的Web应用程序的信息，请参阅 [创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md).

您可以使用以下两种方式之一将表单设计（XDP文件）或PDF文档传递到Forms服务：

* 您可以使用URL值引用表单设计。 此方法涉及使用 `URLSpec` 对象。 使用将内容根传递到Forms服务 `URLSpec` 对象的 `setContentRootURI` 方法。 窗体设计名称( `formQuery`)作为单独的参数传递。 将这两个值连接起来以获得对窗体设计的绝对引用。 (大多数快速入门都位于 *呈现Forms* 部分使用此方法。)
* 您可以传递 `com.adobe.idp.Document` 其中包含表单设计到Forms服务。 两个名为的新方法 `renderPDFForm2` 和 `renderHTMLForm2` 接受 `com.adobe.idp.Document` 包含表单设计的对象。 (请参阅 [将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)

您可以使用Forms服务完成这些任务：

* 呈现交互式PDF forms。 (请参阅 [呈现交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* 在客户端渲染表单。 (请参阅 [在客户端渲染Forms](/help/forms/developing/rendering-forms-client.md).)
* 根据片段渲染表单。 (请参阅 [基于片段渲染Forms](/help/forms/developing/rendering-forms-based-fragments.md).)
* 渲染启用权限的表单。 (请参阅 [渲染启用权限的Forms](/help/forms/developing/rendering-rights-enabled-forms.md).)
* 将表单渲染为HTML。 (请参阅 [将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md).)
* 使用自定义CSS文件渲染HTMLForms ([使用自定义CSS文件渲染HTMLForms](/help/forms/developing/rendering-html-forms-using-custom.md).)
* 处理提交的表单。 (请参阅 [处理提交的Forms](/help/forms/developing/handling-submitted-forms.md).)
* 使用提交的XML数据创建PDF文档。 (请参阅 [使用提交的XML数据创建PDF文档](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* 预填充表单。 (请参阅 [使用可流布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* 传递文档。 (请参阅 [将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)
* 计算表单数据。 (请参阅 [计算表单数据](/help/forms/developing/calculating-form-data.md).)
* 优化应用程序。 (请参阅 [优化Forms服务的性能](/help/forms/developing/optimizing-performance-forms-service.md).)
