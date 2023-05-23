---
title: 資料保護和資料隱私權法規 — Adobe Experience Manager整備
description: 瞭解Adobe Experience Manager對各種資料保護和資料隱私權法規的支援。 其中包括歐盟一般資料保護規範(GDPR)、加州消費者隱私法，以及在實施新的AEM專案時如何遵守。
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

# Adobe Experience Manager的資料保護與資料隱私權法規整備 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律建议，也不会代替法律建议。
>
>如需資料保護與資料隱私權法規的相關建議，請洽詢貴公司的法律部門。

>[!NOTE]
>
>如需有關Adobe對隱私權問題的回應，以及這對於您身為Adobe客戶所代表之意義的詳細資訊，請參閱 [Adobe隱私權中心](https://www.adobe.com/cn/privacy.html).

Adobe正為客戶隱私權管理員或AEM管理員提供檔案和程式（可用時透過API）以處理資料保護和資料隱私權請求。 它可以協助您符合這些法規。 記錄的程式可讓客戶手動執行監管請求，或從外部入口網站或服務（如果可用）呼叫API來執行監管請求。

>[!CAUTION]
>
>此處記錄的詳細資料僅限於Adobe Experience Manager。
>
>來自其他Adobe隨選服務的資料以及任何相關的隱私權請求需要對該服務採取動作。
>
>如需詳細資訊，請參閱 [Adobe隱私權中心](https://www.adobe.com/cn/privacy.html).

## 简介 {#introduction}

Adobe Experience Manager執行個體以及在其上執行的應用程式是由Adobe客戶所擁有和營運。

因此，GDPR、CCPA 及其他数据保护条例在很大程度上由客户负责。

簡單介紹，資料隱私權和保護法規包括以下角色要遵循的新規則：

* 业务实体 (CCPA) 和/或数据控制方 (GDPR)

* 服务提供商 (CCPA) 和/或数据处理商 (GDPR)

此类条例中的主要条款：

1. 扩展了个人数据的定义，以包括唯一 ID（在可直接和间接识别身份的数据中）。

2. 强化了对同意书的要求。

3. 增加了对删除权利的关注（数据清除）。

4. 数据销售的选择退出。

若為Adobe Experience Manager：

* 实例以及其上运行的应用程序由客户负责和运营。

   * 客戶管理法規角色，包括商業實體和服務提供者、資料控制者和資料處理者等。

   * Adobe Experience Platform Privacy Service不是AEM工作流程的一部分，如下圖所示。

* AEM 包括面向客户隐私管理员和/或 AEM 管理员的文档和过程，可手动或通过 API（在可用时）执行隐私监管请求。

* 未添加新的服务或 UI。

   * 而是记载了由处理隐私监管请求的客户 UI/门户使用的过程和 API。

* AEM不包含任何現成工具來支援隱私權請求工作流程。

   * Adobe會為客戶的隱私權管理員和AEM管理員提供檔案和程式，讓他們手動執行與隱私權法規相關的請求。

Adobe提供處理隱私權請求的程式，這些請求與Adobe Experience Manager的存取、刪除和選擇退出相關。 有時候，可以從客戶開發的入口網站或指令碼中呼叫可用的API，以協助實現自動化。

下图说明了隐私请求工作流可能的样子（使用 Adobe Experience Manager 6.5 说明）：

![数据保护和隐私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager與法規整備 {#aem-and-regulatory-readiness}

如需有關AEM產品領域的監管檔案，請參閱以下各節。

## AEM Foundation {#aem-foundation}

另請參閱 [處理AEM Foundation的資料保護和隱私權請求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM選擇加入彙總使用狀況統計資料收集 {#aem-opting-into-aggregate-usage-statistics-collection}

另請參閱 [彙總的使用狀況統計資料收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

另請參閱 [AEM Sites — 資料保護和隱私權整備。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM商務 {#aem-commerce}

另請參閱 [AEM Commerce — 資料保護和隱私權整備](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

另請參閱 [AEM Mobile — 資料保護和隱私權整備](/help/mobile/aem-mobile-gdpr-compliance.md).

## AEM與Adobe Target和Adobe Analytics的整合 {#aem-integration-with-adobe-target-adobe-analytics}

這些Adobe Experience Manager整合具備資料保護和隱私權（例如GDPR或CCPA）整備服務。 Adobe Target 或 Adobe Analytics 中的任何个人数据都不会存储在与集成相关的 AEM 中。


如需詳細資訊，請參閱下列內容：

* [Adobe Target - 隐私概述](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)

* [Adobe Analytics 数据隐私工作流](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities賦予資料主體資料可攜性、存取許可權及被遺忘的權利 [現成可用的API](/help/communities/user-ugc-management-service.md). 這些API可大量刪除和大量匯出使用者產生的內容，並停用透過其可授權ID識別的使用者帳戶。 不過，透過刪除CRXDE Lite中的使用者節點，即可永久刪除使用者帳戶，滿足輕鬆選擇退出系統的需求。

此外，AEM Communities的「大量調節」主控台可讓擁有特殊許可權的成員尋找及刪除使用者的貢獻和詳細資訊，因此在設計上提供隱私權。 「成員」管理主控台允許將限制到禁止投稿人的程度。 此外，它還授權資料主體刪除他們創作的投稿。

## AEM Forms {#aem-forms}

AEM Forms包含擷取、處理和儲存資料的元件和工作流程，以協調業務流程和完成數位交易。 不同的元件會使用不同的資料存放區，並允許與自訂資料存放區整合。 以下檔案說明存取和處理使用者資料的程式和准則，以支援元件的資料保護和隱私權（例如GDPR或CCPA）工作流程。

* [Forms Portal](/help/forms/using/forms-portal-handling-user-data.md)
* [通信管理](/help/forms/using/correspondence-management-handling-user-data.md)
* [與Adobe Sign整合](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi上以Forms為中心的工作流程](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE工作流程](/help/forms/using/forms-workflow-jee-handling-user-data.md) (僅限AEM Forms JEE)
* [檔案安全性](/help/forms/using/document-security-handling-user-data.md) (僅限AEM Forms JEE)
* [User Management](/help/forms/using/user-management-handling-user-data.md) (僅限AEM Forms JEE)
