---
title: 数据保护和数据隐私法规-Adobe Experience Manager就绪性
seo-title: Adobe Experience Manager为数据保护和数据隐私法规做好准备；如GDPR、CCPA等
description: '了解Adobe Experience Manager对各种数据保护和数据隐私法规的支持；包括欧盟一般数据保护规定(GDPR)、加利福尼亚消费者隐私法，以及实施新AEM项目时如何遵守这些规定。 '
seo-description: '了解Adobe Experience Manager对各种数据保护和数据隐私法规的支持；包括欧盟一般数据保护规定(GDPR)、加利福尼亚消费者隐私法，以及实施新AEM项目时如何遵守这些规定。 '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---


# Adobe Experience Manager数据保护和数据隐私法规的就绪性 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律咨询，不能代替法律咨询。
>
>请咨询您的公司的法律部门，以获取有关数据保护和数据隐私法规的建议。

>[!NOTE]
>
>有关Adobe对隐私问题的回应以及这对Adobe客户意味着什么的更多信息，请参 [阅Adobe隐私中心](https://www.adobe.com/privacy.html)。

Adobe提供文档和过程（如果有API），让客户隐私管理员或AEM管理员处理数据保护和数据隐私请求并帮助客户遵守这些规定。 记录的过程将允许客户手动或通过调用API（如果可用）从外部门户或服务执行法规要求。

>[!CAUTION]
>
>此处记录的详细信息仅限于Adobe Experience Manager。
>
>来自其他Adobe点播服务的数据，连同任何相关的隐私请求，都需要对该服务采取相应的操作。
>
>有关详细信息，请 [参阅Adobe隐私中心](https://www.adobe.com/privacy.html)。

## 简介 {#introduction}

Adobe Experience Manager的实例及其上运行的应用程序由我们的客户拥有和操作。

因此，GDPR、CCPA等数据保护法规在很大程度上是客户的责任。

作为非常简短的介绍，数据隐私和保护法规包括新规则，其后将遵循：

* 业务实体(CCPA)和／或数据控制者(GDPR)

* 服务提供商(CCPA)和／或数据处理者(GDPR)

本条例的主要规定是：

1. 扩展了个人数据的定义，以包含所有唯一ID;直接和间接可识别数据。

2. 加强同意要求。

3. 增加了对删除权限（数据擦除）的关注。

4. 选择退出数据销售。

Adobe Experience Manager:

* 客户拥有并操作在这些实例上运行的应用程序。

   * 这有效地意味着客户管理法规角色，包括业务实体和服务提供商、数据管理者和数据处理者等。

   * 如下图所示，Adobe Experience Platform Privacy Service将不是AEM工作流程的一部分。

* AEM包括客户隐私管理员和／或AEM管理员执行隐私法规请求的文档和过程；手动或通过API（如果可用）。

* 未添加新服务或UI。

   * 相反，过程和API已记录在案，供处理隐私法规请求的客户UI/门户使用。

* AEM不会包含任何现成工具来支持隐私请求工作流。

   * Adobe将为客户的隐私管理员和／或AEM管理员提供文档和过程，允许他们手动执行与隐私法规相关的请求。

Adobe正在提供处理与Adobe Experience Manager的访问、删除和选择退出相关的隐私请求的程序。 在某些情况下，可以从客户开发的门户或脚本中调用API来帮助实现自动化。

下图说明了隐私请求工作流的外观(使用Adobe Experience Manager6.5进行说明):

![数据保护和隐私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager和监管就绪性 {#aem-and-regulatory-readiness}

有关AEM产品区域的法规文档，请参阅以下各节。

## AEM基础 {#aem-foundation}

请参 [阅处理AEM Foundation的数据保护和隐私请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

## AEM选择加入聚合使用统计信息收集 {#aem-opting-into-aggregate-usage-statistics-collection}

请参 [阅汇总使用情况统计信息收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)。

## AEM Sites {#aem-sites}

请参 [阅AEM Sites-数据保护和隐私就绪性。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

请参 [阅AEM商务——数据保护和隐私就绪](/help/sites-administering/gdpr-compliance-commerce.md)。

## AEM Mobile {#aem-mobile}

请参 [阅AEM Mobile-数据保护和隐私就绪](/help/mobile/aem-mobile-gdpr-compliance.md)。

## AEM与Adobe Target和Adobe Analytics集成 {#aem-integration-with-adobe-target-adobe-analytics}

Adobe Experience Manager的这些集成包括数据保护和隐私（例如，GDPR或CCPA）就绪服务。 Adobe Target或Adobe Analytics的个人数据不存储在与集成相关的AEM中。
有关更多信息，请参阅：

* [Adobe Target-隐私概述](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics数据隐私工作流程](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities赋予数据主体数据可移植性、访问权和通过开箱即用 [的API被遗忘的权利](/help/communities/user-ugc-management-service.md)。 这些API支持批量删除和批量导出用户生成的内容，并禁用通过其可授权ID标识的用户帐户。 但是，通过删除CRXDE Lite中的用户节点，可以实现用户帐户的永久删除，这就满足了从系统中轻松退出的需要。

此外，AEM Communities优惠隐私的设计是因为它的“批量审核”控制台，允许特权会员查找和删除用户的贡献和详细信息。 会员管理控制台允许限制到禁止参与者的程度。 此外，它授权数据主体删除由它们创作的稿件。

## AEM Forms {#aem-forms}

AEM Forms包括捕获、处理和存储数据以编排业务流程和完成数字交易的组件和工作流。 不同的组件使用不同的数据存储，并允许与自定义数据存储集成。 以下文档介绍了访问和处理用户数据以支持组件数据保护和隐私（例如，GDPR或CCPA）工作流的过程和准则。

* [Forms门户](/help/forms/using/forms-portal-handling-user-data.md)
* [通信管理](/help/forms/using/correspondence-management-handling-user-data.md)
* [与Adobe Sign集成](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [以Forms为中心的OSGi工作流](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms·吉工作流](/help/forms/using/forms-workflow-jee-handling-user-data.md) (仅限AEM Forms·吉)
* [文档安全](/help/forms/using/document-security-handling-user-data.md) (仅限AEM FormsJEE)
* [用户管理](/help/forms/using/user-management-handling-user-data.md) (仅限AEM FormsJEE)
