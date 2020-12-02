---
title: 表单配置基础知识
seo-title: 表单配置基础知识
description: 了解帮助您创建交互式数据捕获应用程序的各种表单服务。
seo-description: 了解帮助您创建交互式数据捕获应用程序的各种表单服务。
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# 配置表单的基础知识{#basics-of-configuring-forms}

Forms服务使您能够创建交互式数据捕获客户端应用程序，这些应用程序通常在Designer中验证、处理、转换和交付表单。 表单作者开发了Forms服务以各种格式呈现的单一表单设计：

* 在Adobe Reader或浏览器中作为PDF
* 作为HTML，在各种浏览器环境中，包括兼容的XHTML 1.0渲染
* 在支持AdobeFlash Player的各种浏览器环境中作为表单指南。

有关Forms服务的详细信息，请参见[服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

使用管理控制台中的“Forms”页面，可以配置“Forms”服务的行为。 这些设置适用于服务的所有调用。 通过AEM forms SDK发送的任何参数都会覆盖管理控制台中设置的设置；但是，它们只影响这种特定的援引。

在管理控制台中更改Forms设置后，单击“保存”。 您无需重新启动服务器，更改即可生效。 但是，在配置缓存模式设置时，可能需要停止和重新启动Forms服务。 （请参阅[启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)。）
