---
title: 数据保护和数据隐私法规 — Adobe Experience Manager就绪
seo-title: Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations; such as GDPR, CCPA, etc
description: 了解 Adobe Experience Manager 对各种数据保护和数据隐私条例的支持，包括欧盟通用数据保护条例 (GDPR)、加州消费者隐私法案以及如何在实施新的 AEM 项目时实现合规性。
seo-description: Learn about Adobe Experience Manager support for the various Data Protection and Data Privacy Regulations; including the EU General Data Protection Regulation (GDPR), the California Consumer Privacy Act and how to comply when implementing a new AEM project.
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
source-wordcount: '927'
ht-degree: 56%

---

# Adobe Experience Manager数据保护和数据隐私法规已准备就绪 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律建议，也不会代替法律建议。
>
>请咨询您公司的法律部门，以获取关于数据保护和数据隐私条例的建议。

>[!NOTE]
>
>要详细了解 Adobe 对隐私问题的响应以及这对于您这样的 Adobe 客户的意义，请参阅 [Adobe 隐私中心](https://www.adobe.com/cn/privacy.html)。

Adobe 向客户隐私管理员或 AEM 管理员提供文档和过程（在有 API 可用时），用于处理数据保护和数据隐私请求，并帮助我们的客户遵守这些条例。通过所记录的过程，客户将能够从外部门户或服务，手动或者通过调用 API（在可用时）来执行监管请求。

>[!CAUTION]
>
>此处记录的详细信息仅限于Adobe Experience Manager。
>
>其他 Adobe 按需插件的服务以及任何相关隐私请求需要在该服务上采取操作。
>
>有关更多信息，请参阅 [Adobe 隐私中心](https://www.adobe.com/privacy.html)。

## 简介 {#introduction}

Adobe Experience Manager实例以及在其上运行的应用程序都由我们的客户拥有和运行。

因此，GDPR、CCPA 及其他数据保护条例在很大程度上由客户负责。

作为一个非常简单的介绍，数据隐私和保护条例包括下列各方需要遵守的新规则：

* 业务实体 (CCPA) 和/或数据控制方 (GDPR)

* 服务提供商 (CCPA) 和/或数据处理商 (GDPR)

此类条例中的主要条款：

1. 扩展了个人数据的定义，以包括唯一 ID（在可直接和间接识别身份的数据中）。

2. 强化了对同意书的要求。

3. 增加了对删除权利的关注（数据清除）。

4. 数据销售的选择退出。

对于Adobe Experience Manager:

* 实例以及其上运行的应用程序由客户负责和运营。

   * 这实际上意味着客户需要管理监管角色，包括业务实体和服务提供商、数据控制方和数据处理商等等。

   * Adobe Experience Platform Privacy Service 不在 AEM 的工作流中，如下图所述。

* AEM 包括面向客户隐私管理员和/或 AEM 管理员的文档和过程，可手动或通过 API（在可用时）执行隐私监管请求。

* 未添加新的服务或 UI。

   * 而是记载了由处理隐私监管请求的客户 UI/门户使用的过程和 API。

* AEM 不包括任何现成的工具来支持隐私请求工作流。

   * Adobe 向客户隐私管理员和/或 AEM 管理员提供文档和过程，使他们可以手动执行与隐私监管相关的请求。

Adobe正在提供处理与Adobe Experience Manager的访问、删除和选择退出相关的隐私请求的程序。 在某些情况下，提供了可以从客户开发的门户或脚本来调用的 API，用于帮助实现自动处理。

下图说明了隐私请求工作流可能的样子（使用 Adobe Experience Manager 6.5 说明）：

![数据保护和隐私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager和法规就绪性 {#aem-and-regulatory-readiness}

有关AEM产品区域的法规文档，请参阅以下部分。

## AEM Foundation {#aem-foundation}

请参阅 [为AEM Foundation处理数据保护和隐私请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM选择加入聚合使用情况统计信息收集 {#aem-opting-into-aggregate-usage-statistics-collection}

请参阅 [汇总使用情况统计信息收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

请参阅 [AEM Sites — 数据保护和隐私就绪。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

请参阅 [AEM Commerce — 数据保护和隐私就绪](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

请参阅 [AEM Mobile — 数据保护和隐私就绪](/help/mobile/aem-mobile-gdpr-compliance.md).

## AEM与Adobe Target和Adobe Analytics集成 {#aem-integration-with-adobe-target-adobe-analytics}

这些Adobe Experience Manager集成提供了数据保护和隐私（例如，GDPR或CCPA）就绪服务。 Adobe Target 或 Adobe Analytics 中的任何个人数据都不会存储在与集成相关的 AEM 中。
有关更多信息，请参阅：

* [Adobe Target - 隐私概述](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics 数据隐私工作流](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities赋予数据主体数据可移植性、访问权和被遗忘权 [开箱即用API](/help/communities/user-ugc-management-service.md). 这些API允许批量删除和批量导出用户生成的内容，并禁用通过其可授权ID标识的用户帐户。 但是，通过删除CRXDE Lite中的用户节点，可以实现永久删除用户帐户，这就满足了系统轻松选择退出的需要。

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
