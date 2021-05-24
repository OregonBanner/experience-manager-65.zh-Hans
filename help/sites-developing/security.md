---
title: 安全
seo-title: 安全
description: 应用程序安全性在开发阶段启动
seo-description: 应用程序安全性在开发阶段启动
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 安全{#security}

应用程序安全性在开发阶段启动。 Adobe建议应用以下安全最佳实践。

## 使用请求会话{#use-request-session}

遵循最少权限的原则，Adobe建议使用绑定到用户请求的会话和适当的访问控制来完成每个存储库的访问。

## Protect针对跨站点脚本(XSS){#protect-against-cross-site-scripting-xss}

跨站点脚本(XSS)允许攻击者将代码注入其他用户查看的网页中。 恶意Web用户可能会利用此安全漏洞绕过访问控制。

AEM在输出时应用过滤所有用户提供内容的原则。 在开发和测试过程中，防止XSS都是最优先的任务。

AEM提供的XSS保护机制基于[OWASP（Open Web应用程序安全项目）](https://www.owasp.org/)提供的[AntiSamy Java库](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)。 默认AntiSamy配置可在

`/libs/cq/xssprotection/config.xml`

通过覆盖配置文件，您必须根据自己的安全需求调整此配置。 官方的[AntiSamy文档](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)将为您提供实施安全要求所需的所有信息。

>[!NOTE]
>
>我们强烈建议您始终使用AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html)提供的[XSSAPI来访问XSS保护API。

此外，Web应用程序防火墙（如Apache](https://www.modsecurity.org)的[mod_security）可以提供对部署环境安全的可靠、集中的控制，并防止以前未检测到的跨站点脚本攻击。

## 访问Cloud Service信息{#access-to-cloud-service-information}

>[!NOTE]
>
>Cloud Service信息的ACL以及保护实例所需的OSGi设置将作为[生产就绪模式](/help/sites-administering/production-ready.md)的一部分自动执行。 虽然这意味着您无需手动进行配置更改，但仍建议您在部署开始之前先查看配置更改。

当您[将AEM实例与Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md)集成时，您将使用[Cloud Service配置](/help/sites-developing/extending-cloud-config.md)。 有关这些配置的信息以及收集的任何统计信息都存储在存储库中。 如果您使用此功能，我们建议您查看此信息的默认安全性是否与您的要求相符。

Webservicesupport模块将统计信息和配置信息写入：

`/etc/cloudservices`

具有默认权限：

* 创作环境：`contributors`的`read`

* 发布环境：`everyone`的`read`

## Protect反跨站点请求伪造攻击{#protect-against-cross-site-request-forgery-attacks}

有关AEM用于缓解CSRF攻击的安全机制的更多信息，请参阅安全检查表的[Sling反向链接过滤器](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)部分和[CSRF保护框架文档](/help/sites-developing/csrf-protection.md)。
