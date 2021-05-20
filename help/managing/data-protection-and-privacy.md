---
title: 数据保护和数据隐私法规 — Adobe Experience Manager就绪
seo-title: Adobe Experience Manager为数据保护和数据隐私法规做好准备；例如GDPR、CCPA等
description: '了解Adobe Experience Manager对各种数据保护和数据隐私法规的支持；包括欧盟《通用数据保护条例》(GDPR)、《加州消费者隐私法案》，以及实施新AEM项目时如何遵守这些法案。 '
seo-description: '了解Adobe Experience Manager对各种数据保护和数据隐私法规的支持；包括欧盟《通用数据保护条例》(GDPR)、《加州消费者隐私法案》，以及实施新AEM项目时如何遵守这些法案。 '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---

# Adobe Experience Manager数据保护和数据隐私法规的准备工作{#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律建议，也不会代替法律建议。
>
>请咨询贵公司的法律部门，以获取有关数据保护和数据隐私法规的建议。

>[!NOTE]
>
>有关Adobe对隐私问题的响应以及这对Adobe客户有何影响的更多信息，请参阅[Adobe的隐私中心](https://www.adobe.com/privacy.html)。

Adobe将提供文档和规程（如果有API），以便客户隐私管理员或AEM管理员处理数据保护和数据隐私请求，并帮助我们的客户遵守这些法规。 记录的过程将允许客户手动执行法规请求，或通过从外部门户或服务调用API（如果可用）来执行法规请求。

>[!CAUTION]
>
>此处记录的详细信息仅限于Adobe Experience Manager。
>
>来自其他Adobe点播服务的数据以及任何相关的隐私请求，将要求对该服务采取相应的操作。
>
>有关详细信息，请参阅[Adobe的隐私中心](https://www.adobe.com/privacy.html)。

## 简介 {#introduction}

Adobe Experience Manager实例以及在其上运行的应用程序都由我们的客户拥有和运行。

因此，数据保护法规（如GDPR、CCPA等）在很大程度上由客户负责。

作为非常简短的介绍，数据隐私和保护法规包括了新的规则，这些规则将遵循以下角色：

* 业务实体(CCPA)和/或数据控制者(GDPR)

* 服务提供商(CCPA)和/或数据处理者(GDPR)

这些条例的主要规定是：

1. 扩展了对个人数据的定义，以包含所有唯一ID;直接和间接可识别数据中。

2. 增强了同意要求。

3. 增加了对删除权限（数据擦除）的关注。

4. 选择退出数据销售。

对于Adobe Experience Manager:

* 这些实例以及在其上运行的应用程序都归客户所有和操作。

   * 这实际上意味着客户可以管理法规角色，包括业务实体和服务提供商、数据控制者和数据处理者等。

   * 如下图所示，Adobe Experience Platform Privacy Service将不属于AEM工作流的一部分。

* AEM包含有关客户隐私管理员和/或AEM管理员执行隐私法规请求的文档和程序；手动或通过API（如果可用）。

* 未添加新服务或UI。

   * 而是记录了过程和API，以供处理隐私法规请求的客户UI/门户使用。

* AEM将不包含任何用于支持隐私请求工作流的现成工具。

   * Adobe将为客户的隐私管理员和/或AEM管理员提供文档和程序，使他们能够手动执行与隐私法规相关的请求。

Adobe正在提供处理与Adobe Experience Manager的访问、删除和选择退出相关的隐私请求的程序。 在某些情况下，可以从客户开发的门户或脚本中调用一些可用的API，以帮助实现自动化。

下图说明了隐私请求工作流的外观(使用Adobe Experience Manager 6.5进行了说明):

![数据保护和隐私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager和法规就绪{#aem-and-regulatory-readiness}

有关AEM产品区域的法规文档，请参阅以下部分。

## AEM Foundation {#aem-foundation}

请参阅[处理AEM Foundation的数据保护和隐私请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

## AEM选择加入聚合使用情况统计信息集合{#aem-opting-into-aggregate-usage-statistics-collection}

请参阅[汇总使用情况统计信息集合](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)。

## AEM Sites {#aem-sites}

请参阅[AEM Sites — 数据保护和隐私就绪。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

请参阅[AEM Commerce — 数据保护和隐私就绪](/help/sites-administering/gdpr-compliance-commerce.md)。

## AEM Mobile {#aem-mobile}

请参阅[AEM Mobile — 数据保护和隐私就绪](/help/mobile/aem-mobile-gdpr-compliance.md)。

## AEM与Adobe Target和Adobe Analytics的集成{#aem-integration-with-adobe-target-adobe-analytics}

这些Adobe Experience Manager集成提供了数据保护和隐私（例如，GDPR或CCPA）就绪服务。 AEM中不存储与集成相关的来自Adobe Target或Adobe Analytics的个人数据。
有关更多信息，请参阅：

* [Adobe Target — 隐私概述](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics数据隐私工作流程](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities通过[现成API](/help/communities/user-ugc-management-service.md)赋予数据主体访问其数据可移植性、访问权和被遗忘权。 这些API允许批量删除和批量导出用户生成的内容，并禁用通过其可授权ID标识的用户帐户。 但是，通过删除CRXDE Lite中的用户节点，可以实现永久删除用户帐户，这就满足了系统轻松选择退出的需要。

此外，AEM Communities还通过其批量审核控制台提供了设计隐私，该控制台允许特权成员查找和删除用户贡献和详细信息。 “成员管理”控制台允许限制为禁止参与者。 此外，它授权数据主体删除其创作的稿件。

## AEM Forms {#aem-forms}

AEM Forms包含可捕获、处理和存储数据以编排业务流程和完成数字交易的组件和工作流。 不同的组件使用不同的数据存储，并且还允许与自定义数据存储相集成。 以下文档介绍了访问和处理用户数据以支持组件的数据保护和隐私（例如，GDPR或CCPA）工作流的过程和准则。

* [Forms Portal](/help/forms/using/forms-portal-handling-user-data.md)
* [通信管理](/help/forms/using/correspondence-management-handling-user-data.md)
* [与Adobe Sign集成](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi上以Forms为中心的工作流](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE工作流](/help/forms/using/forms-workflow-jee-handling-user-data.md) (仅限AEM Forms JEE)
* [文档安全](/help/forms/using/document-security-handling-user-data.md) (仅限AEM Forms JEE)
* [用户管理](/help/forms/using/user-management-handling-user-data.md) (仅限AEM Forms JEE)
