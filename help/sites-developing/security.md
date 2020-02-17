---
title: 安全
seo-title: 安全
description: 应用程序安全性在开发阶段开始
seo-description: 应用程序安全性在开发阶段开始
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 安全{#security}

应用程序安全性在开发阶段开始。 Adobe建议应用以下安全最佳实践。

## 使用请求会话 {#use-request-session}

Adobe建议，按照Leas权限原则，通过使用绑定到用户请求的会话和适当的访问控制来完成每个存储库的访问。

## 防止跨站点脚本(XSS) {#protect-against-cross-site-scripting-xss}

跨站点脚本(XSS)使攻击者能够将代码注入其他用户查看的网页中。 恶意Web用户可能会利用该安全漏洞绕过访问控制。

AEM在输出时应用过滤所有用户提供的内容的原则。 在开发和测试过程中，防止XSS的优先级最高。

AEM提供的XSS保护机制基于 [OWASP（开放Web应用程序安全项目）提供的AntiSamy Java库](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)[](https://www.owasp.org/)。 默认的AntiSamy配置位于

`/libs/cq/xssprotection/config.xml`

通过覆盖配置文件，您必须根据自己的安全需求调整此配置。 官方 [AntiSamy文档将为您提供所需的所有信息](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) ，以便实施您的安全要求。

>[!NOTE]
>
>我们强烈建议您始终使用AEM提供的 [XSSAPI访问XSS保护API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html)。

此外，Web应用程序防火墙(如Apache的 [mod_security](https://www.modsecurity.org))可以提供对部署环境安全的可靠、集中的控制，并防止以前未被检测到的跨站点脚本攻击。

## 访问云服务信息 {#access-to-cloud-service-information}

>[!NOTE]
>
>云服务信息的ACL以及保护实例所需的OSGi设置作为生产就绪模式的一部分进行 [了自动化](/help/sites-administering/production-ready.md)。 这意味着您无需手动更改配置，但仍建议您在部署开始之前先查看这些更改。

将AEM实 [例与Adobe Marketing cloud集成后](/help/sites-administering/marketing-cloud.md) ，您可以使 [用云服务配置](/help/sites-developing/extending-cloud-config.md)。 有关这些配置的信息以及收集的任何统计信息都存储在存储库中。 如果您使用此功能，则建议您查看此信息的默认安全性是否符合您的要求。

Web服务支持模块在以下位置写入统计信息和配置信息：

`/etc/cloudservices`

具有默认权限：

* 创作环境： `read` for `contributors`

* 发布环境： `read` for `everyone`

## 防止跨站点请求伪造攻击 {#protect-against-cross-site-request-forgery-attacks}

有关AEM用于缓解CSRF攻击的安全机制的详细信息，请参阅安全核对清单的 [Sling Referrer Filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) ( [Sling引荐过滤器)部分和](/help/sites-developing/csrf-protection.md)CSRF保护框架文档。