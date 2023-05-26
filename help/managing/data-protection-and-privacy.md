---
title: 数据保护和数据隐私条例 — Adobe Experience Manager准备工作
description: 了解Adobe Experience Manager对各种数据保护和数据隐私条例的支持。 其中包括欧盟通用数据保护条例(GDPR)、加州消费者隐私法案以及如何在实施新的AEM项目时实现合规性。
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 25%

---

# 用于数据保护和数据隐私法规的Adobe Experience Manager已准备就绪 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律建议，也不会代替法律建议。
>
>请咨询贵公司的法律部门，以获取有关数据保护和数据隐私条例的建议。

>[!NOTE]
>
>有关Adobe对隐私问题的响应以及这对于您这样的Adobe客户有何意义的更多信息，请参阅 [Adobe隐私中心](https://www.adobe.com/cn/privacy.html).

Adobe为客户隐私管理员或AEM管理员提供文档和过程（可用时通过API）以处理数据保护和数据隐私请求。 它可以帮助您遵守这些法规。 记录的过程允许客户手动运行管理法规请求，或者通过从外部门户或服务（如果可用）调用API来运行管理法规请求。

>[!CAUTION]
>
>此处记录的详细信息仅限于Adobe Experience Manager。
>
>来自其他Adobe按需服务的数据以及任何相关的隐私请求要求对该服务执行操作。
>
>有关更多信息，请参阅 [Adobe隐私中心](https://www.adobe.com/cn/privacy.html).

## 简介 {#introduction}

Adobe Experience Manager的实例以及在其上运行的应用程序由Adobe客户负责和运营。

因此，GDPR、CCPA 及其他数据保护条例在很大程度上由客户负责。

作为简单介绍，数据隐私和保护法规包括以下角色需要遵守的新规则：

* 业务实体 (CCPA) 和/或数据控制方 (GDPR)

* 服务提供商 (CCPA) 和/或数据处理商 (GDPR)

此类条例中的主要条款：

1. 扩展了个人数据的定义，以包括唯一 ID（在可直接和间接识别身份的数据中）。

2. 强化了对同意书的要求。

3. 增加了对删除权利的关注（数据清除）。

4. 数据销售的选择退出。

对于Adobe Experience Manager：

* 实例以及其上运行的应用程序由客户负责和运营。

   * 客户管理监管角色，包括业务实体和服务提供商、数据控制方和数据处理商等。

   * Adobe Experience Platform Privacy Service不是AEM工作流的一部分，如下图所示。

* AEM 包括面向客户隐私管理员和/或 AEM 管理员的文档和过程，可手动或通过 API（在可用时）执行隐私监管请求。

* 未添加新的服务或 UI。

   * 而是记载了由处理隐私监管请求的客户 UI/门户使用的过程和 API。

* AEM不包括任何现成的工具来支持隐私请求工作流。

   * Adobe为客户隐私管理员和AEM管理员提供文档和过程，让他们手动运行与隐私法规相关的请求。

Adobe提供了处理与Adobe Experience Manager的访问、删除和选择退出相关的隐私请求的过程。 有时，可以从客户开发的门户或脚本中调用可用的API以帮助实现自动化。

下图说明了隐私请求工作流可能的样子（使用 Adobe Experience Manager 6.5 说明）：

![数据保护和隐私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager和监管准备工作 {#aem-and-regulatory-readiness}

有关AEM产品领域的监管文档，请参阅以下部分。

## AEM Foundation {#aem-foundation}

参见 [处理AEM Foundation的数据保护和隐私请求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM选择收集汇总使用情况统计数据 {#aem-opting-into-aggregate-usage-statistics-collection}

参见 [收集汇总的使用情况统计数据](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

参见 [AEM Sites — 数据保护和隐私就绪。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM商务 {#aem-commerce}

参见 [AEM Commerce — 数据保护和隐私就绪](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

参见 [AEM Mobile — 数据保护和隐私就绪](/help/mobile/aem-mobile-gdpr-compliance.md).

## AEM与Adobe Target和Adobe Analytics的集成 {#aem-integration-with-adobe-target-adobe-analytics}

这些Adobe Experience Manager集成与支持数据保护和隐私（例如，GDPR或CCPA）的服务集成。 Adobe Target 或 Adobe Analytics 中的任何个人数据都不会存储在与集成相关的 AEM 中。


有关更多信息，请参阅以下内容：

* [Adobe Target - 隐私概述](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)

* [Adobe Analytics 数据隐私工作流](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities赋予数据主体数据可移植性、访问权和被遗忘权 [开箱即用的API](/help/communities/user-ugc-management-service.md). 这些API支持批量删除和批量导出用户生成的内容，并禁用通过其可授权ID标识的用户帐户。 但是，通过删除CRXDE Lite中的用户节点，可以永久删除用户帐户，从而解决了从系统中轻松选择退出的需要。

此外，AEM Communities还通过批量审核控制台从设计上提供了隐私权，该控制台允许拥有特权的成员查找和删除用户的参与和详细信息。 “成员”管理控制台允许将限制到禁止投稿人的程度。 此外，它还授权数据主体删除他们创作的稿件。

## AEM Forms {#aem-forms}

AEM Forms包括捕获、处理和存储数据以编排业务流程和完成数字交易的组件和工作流。 不同的组件使用不同的数据存储区，并允许与自定义数据存储区集成。 以下文档介绍了用于访问和处理用户数据的过程和准则，以支持组件的数据保护和隐私（例如，GDPR或CCPA）工作流。

* [Forms Portal](/help/forms/using/forms-portal-handling-user-data.md)
* [通信管理](/help/forms/using/correspondence-management-handling-user-data.md)
* [与Adobe Sign集成](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi上以Forms为中心的工作流](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE工作流](/help/forms/using/forms-workflow-jee-handling-user-data.md) (仅限AEM Forms JEE)
* [Document Security](/help/forms/using/document-security-handling-user-data.md) (仅限AEM Forms JEE)
* [User Management](/help/forms/using/user-management-handling-user-data.md) (仅限AEM Forms JEE)
