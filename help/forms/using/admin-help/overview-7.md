---
title: 配置表单的基础知识
seo-title: 配置表单的基础知识
description: 了解可帮助您创建交互式数据捕获应用程序的各种表单服务。
seo-description: 了解可帮助您创建交互式数据捕获应用程序的各种表单服务。
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 配置表单{#basics-of-configuring-forms}的基础知识

Forms服务允许您创建交互式数据捕获客户端应用程序，以验证、处理、转换和交付通常在Designer中创建的表单。 表单作者开发了Forms服务以各种格式呈现的单个表单设计：

* 在Adobe Reader中或浏览器中作为PDF
* 作为HTML（在各种浏览器环境中），包括兼容的XHTML 1.0渲染
* 作为表单指南(在支持AdobeFlash Player的各种浏览器环境中)。

有关Forms服务的其他信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

使用管理控制台中的Forms页面，可以配置Forms服务的行为。 这些设置适用于服务的所有调用。 通过AEM Forms SDK发送的任何参数都会覆盖管理控制台中设置的设置；但是，它们只影响这一特定的援引。

在管理控制台中更改Forms设置后，单击保存。 您无需重新启动服务器，更改即可生效。 但是，在配置缓存模式设置时，您可能需要停止并重新启动Forms服务。 （请参阅[启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)。）
