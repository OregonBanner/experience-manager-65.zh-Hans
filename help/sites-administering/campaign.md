---
title: 将AEM 6.5与Adobe Campaign集成
description: 了解AEM 6.5对Adobe Campaign集成的支持。
uuid: 6113279e-d1f5-46c3-ac94-50270fa55060
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fd96f30c-0616-445e-adb9-050d52862ffc
exl-id: ab41e540-1d43-4fc2-99d4-621ff2290e77
source-git-commit: 6fe5e617ceac3c97a77de2d574ec370f30887330
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 将AEM 6.5与Adobe Campaign集成{#integrating-with-adobe-campaign}

了解AEM 6.5对Adobe Campaign集成的支持。

Adobe Campaign是一套解决方案，可让您在所有线上和线下渠道之间个性化并投放营销活动。

>[!NOTE]
>
>本文档介绍了如何将Adobe Campaign与AEM 6.5、内部部署或AMS托管的AEM解决方案集成。
>
>有关将Adobe Campaign与AEMas a Cloud Service(云原生的AEM解决方案)集成的详细信息， [请参阅此文档。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/campaign.html)

## 与 Adobe Campaign Classic 集成 {#acc}

Adobe Campaign Classic (ACC)有许多版本。 是否支持与AEM集成取决于您实施的ACC版本，以及AEM是否安装在Adobe管理服务(AMS)的内部部署中。

| ACC版本 | 与AEM 6.5集成 <br>内部部署 | 与AEM 6.5集成<br>AMS |
|---|---|---|
| [v7](https://experienceleague.adobe.com/docs/campaign-classic.html) | 支持 | 支持 |
| [v8](https://experienceleague.adobe.com/docs/campaign-v8.html) | 支持 | 支持 |
| Web UI* | 支持 | 支持 |

*Adobe Campaign Classic的Web UI预计在2023年底之前提供。

以下文档介绍了如何将AEM与Adobe Campaign Classic集成。

* [与Adobe Campaign Classic集成](/help/sites-administering/campaignonpremise.md)  — 了解有关配置集成的分步详细信息。

以下附加文档介绍了如何使用集成。

* [电子邮件核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)  — 了解可用于在AEM中创作Campaign内容的标准电子邮件组件。
* [Adobe Campaign Classic集成故障诊断](/help/sites-administering/troubleshooting-campaignintegration.md)  — 了解如何修复AEM-ACC集成的最常见问题。

## 与Adobe Campaign Standard集成 {#acs}

集成 [Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html) 带AEM的(ACS)取决于AEM是否安装在Adobe管理服务(AMS)的内部部署中。

| 与AEM 6.5集成 <br>内部部署 | 与AEM 6.5集成<br>AMS |
|---|---|
| 支持 | 支持 |
| 支持 | 支持 |

以下文档介绍了如何将AEM与Adobe Campaign Standard集成。

* [与Adobe Campaign Standard集成](/help/sites-administering/campaignstandard.md)

以下附加文档介绍了如何使用集成。

* [电子邮件核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)
