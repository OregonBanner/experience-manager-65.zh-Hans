---
title: AEM Forms数据集成
seo-title: AEM Forms数据集成
description: 数据集成允许您将AEM Forms与不同的数据源相集成，并创建表单数据模型以创建和使用自适应表单和交互式通信。
seo-description: 数据集成允许您将AEM Forms与不同的数据源相集成，并创建表单数据模型以创建和使用自适应表单和交互式通信。
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
translation-type: tm+mt
source-git-commit: 4e0709031aca030e50840811a9b3717f3cb20340
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# [!DNL AEM Forms] 数据集成 {#aem-forms-data-integration}

![](do-not-localize/data-integeration.png)

企业基础架构包括不同的后端系统或数据源，如数据库、Web服务、REST服务、OData服务和CRM解决方案。 他们共同打造了一个信息系统，为企业应用程序提供数据，以执行日常业务。 另一方面，应用程序会捕获数据并将其发回以更新数据源。

[!DNL AEM Forms] 自适应表单和交互式通信等应用程序需要与数据源集成，以在呈现表单和创建交互式通信的同时获取客户数据。 在某些情况下，当根据自适应表单中的用户输入从数据源获取数据时。 此外，可以回写提交的自适应表单数据以更新各个数据源。

虽然分布式模块化系统有其自身的优势，但挑战在于跨数据源集成和创建数据关联。 数据集成是功能高效的企业基础架构的关键，该基础架构具有与业务数据交换应用程序连接的不同数据源。

## 数据集成概述 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] 数据集成允许配置不同数据源并将其与之连接 [!DNL AEM Forms]。 它提供了直观的用户界面，以创建跨连接数据源的业务实体和服务的统一数据表示模式。 统一的表示形式称为表单数据模型，是JSON模式的扩展。 表单数据模型中的实体称为数据模型对象。 表单数据模型允许您：

* 从连接的数据源访问数据模型对象、属性和服务。
* 创建自定义数据模型对象和属性
* 在数据源内和数据源之间建立数据模型对象之间的关联。
* 调用查询模型对象服务以向数据源或向数据源写入数据。

创建表单数据模型后，您可以在各种自适应表单和交互式通信工作流中使用它，例如：

* 创建基于表单数据模型的自适应表单和交互式通信
* 预填自适应表单和配置数据源的交互式通信
* 使用自适应表单规则调用数据源服务／操作
* 将提交的自适应表单数据写入数据源

## 数据集成入门 {#get-started-with-data-integration}

实施数据集成的第一步是识别和配置数据源，这些数据源存储您希望在自适应表单和交互式通信用例中使用的信息。 接下来，您创建一个表单数据模型，它使用来自一个或多个数据源的数据模型对象、属性和服务。 您可以基于表单数据模型创建自适应表单和交互式通信，其中交互式通信中的自适应表单字段或占位符绑定到相应的数据源属性。

[!DNL AEM Forms] 还允许您创建独立于数据源的表单数据模型，并稍后将表单数据模型中的数据模型对象和属性与数据源关联或绑定。 它消除了在处理表单数据模型时对数据源的任何依赖。

请查看以下内容，开始、了解并实施数据集成。

* [配置数据源](../../forms/using/configure-data-sources.md)
* [创建表单数据模型](../../forms/using/create-form-data-models.md)
* [使用表单数据模型](../../forms/using/work-with-form-data-model.md)
* [使用表单数据模型](../../forms/using/using-form-data-model.md)

